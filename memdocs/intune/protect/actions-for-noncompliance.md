---
title: Messaggio e azioni per i dispositivi non conformi con Microsoft Intune - Azure | Microsoft Docs
description: Creare un messaggio di posta elettronica di notifica da inviare ai dispositivi non conformi. Se un dispositivo viene contrassegnato come non conforme, è possibile aggiungere azioni, ad esempio un periodo di tolleranza al termine del quale il dispositivo deve essere conforme, o creare una pianificazione per bloccare l'accesso finché il dispositivo non è conforme. Queste operazioni possono essere eseguite con Microsoft Intune in Azure.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5a98b57fe8cc2d9d2af3c0095297eb676796029f
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/21/2020
ms.locfileid: "80085218"
---
# <a name="automate-email-and-add-actions-for-noncompliant-devices-in-intune"></a>Automatizzare la posta elettronica e aggiungere azioni per i dispositivi non conformi in Intune

Per i dispositivi che non soddisfano le regole o i criteri di conformità, è possibile aggiungere **Azioni per la non conformità**. Questa funzionalità consente di configurare una sequenza di azioni in ordine temporale, ad esempio l'invio di messaggi di posta elettronica all'utente finale o azioni di altro tipo.

## <a name="overview"></a>Panoramica

Per impostazione predefinita, quando Intune rileva un dispositivo che non è conforme, lo contrassegna immediatamente come non conforme. Quindi l'[accesso condizionale](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal) di Azure Active Directory (AD) blocca il dispositivo. Quando un dispositivo non è conforme, la funzionalità **Azioni per la non conformità** consente inoltre di decidere cosa fare. Ad esempio, si può decidere di non bloccare immediatamente il dispositivo e di concedere all'utente un periodo di tolleranza per adeguarsi ai criteri di conformità.

Sono disponibili diversi tipi di azioni:

- **Invia un messaggio di posta elettronica all'utente finale**: è possibile personalizzare la notifica di posta elettronica prima di inviarla all'utente finale. È possibile personalizzare i destinatari, l'oggetto e il corpo del messaggio, inclusi il logo aziendale e le informazioni di contatto.

    Intune include inoltre le informazioni sul dispositivo non conforme nella notifica di posta elettronica.

- **Blocca in remoto il dispositivo non conforme**: per i dispositivi non conformi, è possibile impostare un blocco remoto. All'utente viene quindi richiesto un PIN o una password per sbloccare il dispositivo. Sono disponibili altre informazioni sulla funzionalità [Blocco remoto](../remote-actions/device-remote-lock.md).

- **Contrassegna il dispositivo come non conforme**: è possibile creare una pianificazione (in numero di giorni) dopo la quale il dispositivo viene contrassegnato come non conforme. È possibile configurare l'azione in modo che venga applicata immediatamente oppure concedere all'utente un periodo di tolleranza entro il quale dovrà adeguarsi ai criteri di conformità.

- **Retire the noncompliant device** (Ritira dispositivo non conforme): Questa azione rimuovere tutti i dati aziendali dal dispositivo e rimuovere il dispositivo dalla gestione di Intune. Per impedire la cancellazione accidentale di un dispositivo, questa azione supporta una pianificazione minima di 30 giorni. Questa azione è supportata dalle piattaforme seguenti:
  - Android
  - iOS
  - macOS
  - Windows 10 Mobile
  - Windows Phone 8.1 e versioni successive

  Altre informazioni sul [ritiro dei dispositivi](../remote-actions/devices-wipe.md#retire).
  
  Questo articolo illustra come:

- Creare un modello di notifica tramite messaggio
- Creare un'azione per la non conformità, ad esempio l'invio di un messaggio di posta elettronica o il blocco remoto di un dispositivo


## <a name="before-you-begin"></a>Prima di iniziare

- Per configurare le azioni per la mancata conformità è necessario aver creato almeno un criterio di conformità dei dispositivi. Per creare criteri di conformità dei dispositivi, vedere le piattaforme seguenti:

  - [Android](compliance-policy-create-android.md)
  - [Profili di lavoro Android](compliance-policy-create-android-for-work.md)
  - [iOS](compliance-policy-create-ios.md)
  - [macOS](compliance-policy-create-mac-os.md)
  - [Windows](compliance-policy-create-windows.md)

- Per usare i criteri di conformità per impedire ai dispositivi di usare le risorse aziendali, è necessario aver configurato l'accesso condizionale di Azure AD. Vedere [Accesso condizionale in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal) o [Modi comuni per usare l'accesso condizionale con Intune](conditional-access-intune-common-ways-use.md) per informazioni aggiuntive.

## <a name="create-a-notification-message-template"></a>Creare un modello di messaggio di notifica

Per inviare il messaggio di posta elettronica agli utenti, creare un modello di messaggio di notifica. Quando un dispositivo risulta non conforme, i dettagli immessi nel modello vengono visualizzati nel messaggio di posta elettronica inviato agli utenti.

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selezionare **Dispositivi** > **Criteri di conformità** > **Notifiche** > **Crea notifica**.
3. In *Informazioni di base* specificare le informazioni seguenti:

   - **Nome**
   - **Oggetto**
   - **Message**

4. In *Informazioni di base* configurare anche le opzioni seguenti per la notifica, che hanno tutte l'impostazione predefinita *Attivato*:

   - **Intestazione del messaggio di posta elettronica: includere il logo dell'azienda**
   - **Piè di pagina del messaggio di posta elettronica: includere il nome dell'azienda**
   - **Piè di pagina del messaggio di posta elettronica: includere le informazioni sul contatto**

   Il logo che si carica nell'ambito della personalizzazione del Portale aziendale viene usato per i modelli di posta elettronica. Per altre informazioni sulla personalizzazione del Portale aziendale, vedere [Personalizzazione dell'identità aziendale](../apps/company-portal-app.md#customizing-the-user-experience).

   ![Esempio di messaggio di notifica di Intune relativo alla conformità](./media/actions-for-noncompliance/actionsfornoncompliance-1.PNG)

   Selezionare **Avanti** per continuare.

5. In **Rivedi e crea** esaminare le configurazioni per assicurarsi che il modello di messaggio di notifica sia pronto per l'uso. Selezionare **Crea** per completare la creazione della notifica.

> [!NOTE]
> È anche possibile selezionare un modello di notifica esistente creato in precedenza e usare **Modifica** per modificare le informazioni e aggiornare il modello.

## <a name="add-actions-for-noncompliance"></a>Aggiungere azioni per la mancata conformità

Quando si crea un criterio di conformità del dispositivo, Intune crea automaticamente un'azione per la non conformità. Se un dispositivo non soddisfa i criteri di conformità, questa azione lo contrassegna come non conforme. È possibile personalizzare il periodo di tempo in cui il dispositivo rimane contrassegnato come non conforme. Questa azione non può essere rimossa.

Oltre all'azione predefinita per contrassegnare i dispositivi come non conformi, è possibile aggiungere azioni facoltative quando si crea un criterio di conformità o se ne aggiorna uno esistente.

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selezionare **Dispositivi** > **Criteri di conformità** > **Criteri**, selezionare uno dei criteri e quindi selezionare **Proprietà**.

   Non esiste ancora un criterio? Creare un criterio per [Android](compliance-policy-create-android.md), [iOS](compliance-policy-create-ios.md), [Windows](compliance-policy-create-windows.md) o un'altra piattaforma.

   > [!NOTE]
   > Attualmente i dispositivi JAMF e i dispositivi selezionati con i gruppi di dispositivi non possono ricevere le azioni di conformità.

3. Selezionare **Azioni per la mancata conformità** > **Aggiungi**.

4. Selezionare l'**azione**:

   - **Invia un messaggio di posta elettronica all'utente finale**: quando il dispositivo non è conforme, scegliere di inviare un messaggio di posta elettronica all'utente. Inoltre:
     - Scegliere il **modello di messaggio** creato in precedenza
     - Immettere eventuali **destinatari aggiuntivi** selezionando i gruppi

   - **Blocca in remoto il dispositivo non conforme**: quando il dispositivo non è conforme, bloccare il dispositivo. Questa azione obbliga l'utente a immettere un PIN o un passcode per sbloccare il dispositivo.

   - **Retire the noncompliant device** (Ritira dispositivo non conforme): quando il dispositivo non è conforme, rimuovere tutti i dati aziendali dal dispositivo e rimuovere il dispositivo dalla gestione di Intune. Per impedire la cancellazione accidentale di un dispositivo, questa azione supporta una pianificazione minima di **30** giorni.

5. Configurare i valori per l'opzione **Pianifica**: immettere il numero di giorni (da 0 a 365) dal rilevamento della non conformità, dopo cui attivare l'azione nei dispositivi degli utenti. Il *ritiro del dispositivo non conforme* supporta un minimo di 30 giorni. Dopo questo periodo di tolleranza, è possibile applicare un criterio di [accesso condizionale](conditional-access-intune-common-ways-use.md). Se si immette **0** (zero) come numero di giorni, l'accesso condizionale viene applicato **immediatamente**. Ad esempio, se un dispositivo non è conforme, usare l'accesso condizionale per bloccare immediatamente l'accesso alla posta elettronica, a SharePoint e ad altre risorse dell'organizzazione.

   Quando si crea un criterio di conformità, viene creata automaticamente l'azione **Contrassegna il dispositivo come non conforme**, che viene impostata su **0** giorni (immediatamente). Con questa azione, durante l'archiviazione del dispositivo ne viene valutata immediatamente la conformità. Se si usa anche l'accesso condizionale, questo viene applicato immediatamente. Se si vuole consentire un periodo di tolleranza, modificare il valore di **Pianifica** nell'azione **Contrassegna il dispositivo come non conforme**.

  Nei criteri di conformità si vuole, ad esempio, anche inviare una notifica all'utente. A questo scopo, è possibile aggiungere l'azione **Invia un messaggio di posta elettronica all'utente finale**. In questa azione **Invia messaggio** si imposta **Pianifica** su due giorni. Se il dispositivo o l'utente finale viene ancora valutato come non conforme il giorno due, il messaggio di posta elettronica viene inviato il giorno due. Se si vuole inviare nuovamente il messaggio di posta elettronica all'utente il giorno cinque della mancata conformità, aggiungere un'altra azione e impostare **Pianifica** su cinque giorni.

   Per altre informazioni sulla conformità e sulle azioni predefinite, vedere la [panoramica della conformità](device-compliance-get-started.md).

6. Al termine, selezionare **Aggiungi** > **OK** per salvare le modifiche.

## <a name="next-steps"></a>Passaggi successivi

[Monitorare i criteri](compliance-policy-monitor.md).
