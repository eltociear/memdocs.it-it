---
title: Messaggio e azioni per i dispositivi non conformi con Microsoft Intune - Azure | Microsoft Docs
description: Creare un messaggio di posta elettronica di notifica da inviare ai dispositivi non conformi. Aggiungere azioni da applicare ai dispositivi che non soddisfano i criteri di conformità. Le azioni possono includere un periodo di tolleranza per ottenere la conformità, bloccare l'accesso alle risorse di rete o ritirare il dispositivo non conforme.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/19/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.reviewer: samyada
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 330dd566599d6bdb1fa667d8797878ea8c92f098
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/19/2020
ms.locfileid: "85093726"
---
# <a name="configure-actions-for-noncompliant-devices-in-intune"></a>Configurare azioni per i dispositivi non conformi in Intune

Per i dispositivi che non soddisfano le regole o i criteri di conformità, è possibile aggiungere **Azioni per la non conformità**. Questa funzionalità consente di configurare una sequenza di azioni in ordine temporale, ad esempio l'invio di messaggi di posta elettronica all'utente finale o azioni di altro tipo.

## <a name="overview"></a>Panoramica

Per impostazione predefinita, ogni criterio di conformità include l'azione per la non conformità di **Contrassegna il dispositivo come non conforme** con una pianificazione di zero giorni (**0**). Il risultato di questa impostazione predefinita si ha quando Intune rileva un dispositivo che non è conforme e lo contrassegna immediatamente come non conforme. Dopo che un dispositivo è stato contrassegnato come non conforme, l'[accesso condizionale](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal) di Azure Active Directory (AD) può bloccare il dispositivo.

Configurando **Azioni per la non conformità** si ottiene la flessibilità necessaria per decidere quali operazioni eseguire sui dispositivi non conformi e quando eseguire questa operazione. Si potrebbe, ad esempio, scegliere di non bloccare immediatamente il dispositivo e di concedere all'utente un periodo di tolleranza per adeguarsi ai criteri di conformità.

Per ogni azione impostata, è possibile configurare una pianificazione che determini quando l'azione avrà effetto. La pianificazione è un numero di giorni trascorsi i quali il dispositivo viene contrassegnato come non conforme. È anche possibile configurare più istanze di un'azione. Quando si impostano più istanze di un'azione in un criterio, l'azione viene eseguita nuovamente in corrispondenza dell'ora pianificata successiva se il dispositivo rimane non conforme.

Non tutte le azioni sono disponibili per tutte le piattaforme.

## <a name="available-actions-for-noncompliance"></a>Azioni disponibili per la mancata conformità

Di seguito sono riportate le azioni disponibili per la non conformità. Se non diversamente specificato, ogni azione è disponibile per tutte le piattaforme supportate da Intune:

- **Contrassegna il dispositivo come non conforme**: Per impostazione predefinita, questa azione è impostata per ogni criterio di conformità e ha una pianificazione di zero (**0**) giorni, contrassegnando immediatamente i dispositivi come non conformi.

  Quando si modifica la pianificazione predefinita, viene fornito un periodo di tolleranza in cui un utente può risolvere i problemi o adeguarsi ai criteri di conformità senza essere contrassegnato come non conforme.

- **Invia un messaggio di posta elettronica all'utente finale**: Questa azione Invia una notifica di posta elettronica all'utente.
Quando si abilita questa azione:

  - Selezionare un *modello del messaggio di notifica*  inviato da questa azione. [Creare un modello di messaggio di notifica](#create-a-notification-message-template) prima di poterne assegnare uno a questa azione. Quando si crea la notifica personalizzata, è possibile personalizzare l'oggetto, il corpo del messaggio e includere il logo della società, il nome della società e altre informazioni di contatto.
  - Scegliere di inviare il messaggio a destinatari aggiuntivi selezionando uno o più gruppi di Azure AD.

Quando viene inviato il messaggio di posta elettronica, Intune include le informazioni sul dispositivo non conforme nella notifica di posta elettronica.

- **Blocca in remoto il dispositivo non conforme**: Usare questa azione per emettere un blocco remoto di un dispositivo. All'utente viene quindi richiesto un PIN o una password per sbloccare il dispositivo. Sono disponibili altre informazioni sulla funzionalità [Blocco remoto](../remote-actions/device-remote-lock.md).

  Questa azione è supportata dalle piattaforme seguenti:
  - Android:
    - Amministratore dispositivo Android
    - Proprietario dispositivo Android Enterprise
    - Profilo di lavoro di Android Enterprise
    - Dispositivi in modalità tutto schermo di Android Enterprise
  - iOS/iPadOS
  - macOS
  - Windows 10 Mobile
  - Windows Phone 8.1 e versioni successive

- **Retire the noncompliant device** (Ritira dispositivo non conforme): Questa azione rimuovere tutti i dati aziendali dal dispositivo e rimuovere il dispositivo dalla gestione di Intune. Per impedire la cancellazione accidentale di un dispositivo, questa azione supporta una pianificazione minima di **30** giorni.

  Questa azione è supportata dalle piattaforme seguenti:
  - Android:
    - Amministratore dispositivo Android
    - Proprietario dispositivo Android Enterprise
    - Profilo di lavoro di Android Enterprise
  - iOS/iPadOS
  - macOS
  - Windows 10 Mobile
  - Windows Phone 8.1 e versioni successive

  Altre informazioni sul [ritiro dei dispositivi](../remote-actions/devices-wipe.md#retire).

- **Invia una notifica push all'utente finale**: Configurare questa azione per inviare una notifica push relativa alla non conformità a un dispositivo tramite l'app Portale aziendale o Intune sul dispositivo.

  Questa azione è supportata dalle piattaforme seguenti:
  - Android:
    - Amministratore dispositivo Android
    - Proprietario dispositivo Android Enterprise
    - Profilo di lavoro di Android Enterprise
  - iOS/iPadOS

  La notifica push viene inviata la prima volta che un dispositivo viene sincronizzato con Intune e non è conforme ai criteri di conformità. Quando un utente seleziona la notifica, viene aperta l'app Portale aziendale o l'app Intune e vengono visualizzate informazioni sul motivo per cui non sono conformi. L'utente può quindi intervenire per risolvere il problema. I dettagli del messaggio sulla non conformità vengono generati da Intune e non possono essere personalizzati.

  > [!IMPORTANT]
  > Intune, l'app Portale aziendale e l'app Microsoft Intune non possono garantire il recapito di una notifica push. Le notifiche potrebbero essere visualizzate dopo alcune ore di ritardo. Questo include il momento in cui gli utenti hanno disattivato le notifiche push.
  >
  > Non fare affidamento su questo metodo di notifica per i messaggi urgenti.

  Ogni istanza dell'azione invia una notifica una sola volta. Per inviare di nuovo la stessa notifica da un criterio, configurare istanze aggiuntive dell'azione nel criterio, ognuna con una pianificazione diversa.
  
  Ad esempio, è possibile pianificare la prima azione per zero giorni, quindi aggiungere una seconda istanza dell'azione impostata su tre giorni. Questo ritardo prima della seconda notifica offre all'utente alcuni giorni per risolvere il problema ed evitare la seconda notifica.

  Per evitare di inviare agli utenti troppi messaggi duplicati, rivedere e semplificare i criteri di conformità che includono una notifica push per la non conformità ed esaminare le pianificazioni per evitare troppe ripetizioni delle notifiche per lo stesso problema.

  Tenere in considerazione:
  - Per un singolo criterio che include più istanze di un set di notifiche push per lo stesso giorno, viene inviata solo una notifica singola per quel giorno.

  - Quando più criteri di conformità includono le stesse condizioni di conformità e includono l'azione di notifica push con la stessa pianificazione, Intune invia più notifiche allo stesso dispositivo nello stesso giorno.

## <a name="before-you-begin"></a>Prima di iniziare

È possibile [aggiungere azioni per la non conformità](#add-actions-for-noncompliance) quando si configurano i criteri di conformità dei dispositivi o in un secondo momento modificando il criterio. È possibile aggiungere altre azioni a ciascun criterio per soddisfare le proprie esigenze. Tenere presente che ogni criterio di conformità include automaticamente l'azione predefinita per la mancata conformità che contrassegna i dispositivi come non conformi, con una pianificazione impostata su zero giorni.

Per usare i criteri di conformità per impedire ai dispositivi di usare le risorse aziendali, è necessario aver configurato l'accesso condizionale di Azure AD. Vedere [Accesso condizionale in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal) o [Modi comuni per usare l'accesso condizionale con Intune](conditional-access-intune-common-ways-use.md) per informazioni aggiuntive.

Per creare criteri di conformità dei dispositivi, vedere le linee guida seguenti specifiche per le piattaforme:

- [Android](compliance-policy-create-android.md)
- [Profili di lavoro Android](compliance-policy-create-android-for-work.md)
- [iOS](compliance-policy-create-ios.md)
- [macOS](compliance-policy-create-mac-os.md)
- [Windows](compliance-policy-create-windows.md)

## <a name="create-a-notification-message-template"></a>Creare un modello di messaggio di notifica

Per inviare il messaggio di posta elettronica agli utenti, creare un modello di messaggio di notifica. Quando un dispositivo risulta non conforme, i dettagli immessi nel modello vengono visualizzati nel messaggio di posta elettronica inviato agli utenti.

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selezionare **Sicurezza degli endpoint** > **Conformità del dispositivo** > **Notifiche** > **Crea la notifica**.
3. In *Informazioni di base* specificare le informazioni seguenti:

   - **Nome**
   - **Oggetto**
   - **Message**

4. In *Informazioni di base* configurare anche le opzioni seguenti per la notifica:

   - **Intestazione del messaggio di posta elettronica - Includere il logo dell'azienda** (impostazione predefinita = *Abilita*) - Il logo che si carica nell'ambito della personalizzazione del Portale aziendale viene usato per i modelli di posta elettronica. Per altre informazioni sulla personalizzazione del Portale aziendale, vedere [Personalizzazione dell'identità aziendale](../apps/company-portal-app.md#customizing-the-user-experience).
   - **Piè di pagina del messaggio di posta elettronica: includere il nome dell'azienda** (impostazione predefinita = *Abilita*)
   - **Piè di pagina del messaggio di posta elettronica: includere le informazioni sul contatto** (impostazione predefinita = *Abilita*)
   - **Portale aziendale collegamento sito Web** (impostazione predefinita = *Disabilita*) - Con l'impostazione *Abilita*, il messaggio di posta elettronica include un collegamento al sito Web del Portale aziendale.

   > [!div class="mx-imgBorder"]
   > ![Esempio di messaggio di notifica di Intune relativo alla conformità](./media/actions-for-noncompliance/actionsfornoncompliance-1.PNG)

   Selezionare **Avanti** per continuare.

5. In **Rivedi e crea** esaminare le configurazioni per assicurarsi che il modello di messaggio di notifica sia pronto per l'uso. Selezionare **Crea** per completare la creazione della notifica.

> [!NOTE]
> È anche possibile selezionare un modello di notifica esistente creato in precedenza e usare **Modifica** per modificare le informazioni e aggiornare il modello.

## <a name="add-actions-for-noncompliance"></a>Aggiungere azioni per la mancata conformità

Quando si crea un criterio di conformità del dispositivo, Intune crea automaticamente un'azione per la non conformità. Se un dispositivo non soddisfa i criteri di conformità, questa azione lo contrassegna come non conforme. È possibile personalizzare il periodo di tempo in cui il dispositivo rimane contrassegnato come non conforme. Questa azione non può essere rimossa.

È possibile aggiungere azioni opzionali quando si crea un criterio di conformità o si aggiorna un criterio esistente.

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

   - **Retire the noncompliant device** (Ritira dispositivo non conforme): quando il dispositivo non è conforme, rimuovere tutti i dati aziendali dal dispositivo e rimuovere il dispositivo dalla gestione di Intune.

   - **Invia una notifica push all'utente finale**: Configurare questa azione per inviare una notifica push relativa alla non conformità a un dispositivo tramite l'app Portale aziendale o Intune sul dispositivo.

5. Configurare i valori per l'opzione **Pianifica**: immettere il numero di giorni (da 0 a 365) dal rilevamento della non conformità, dopo cui attivare l'azione nei dispositivi degli utenti. Il *ritiro del dispositivo non conforme* supporta un minimo di 30 giorni. Dopo questo periodo di tolleranza, è possibile applicare un criterio di [accesso condizionale](conditional-access-intune-common-ways-use.md). Se si immette **0** (zero) come numero di giorni, l'accesso condizionale viene applicato **immediatamente**. Ad esempio, se un dispositivo non è conforme, usare l'accesso condizionale per bloccare immediatamente l'accesso alla posta elettronica, a SharePoint e ad altre risorse dell'organizzazione.

   Quando si crea un criterio di conformità, viene creata automaticamente l'azione **Contrassegna il dispositivo come non conforme**, che viene impostata su **0** giorni (immediatamente). Con questa azione, durante l'archiviazione del dispositivo ne viene valutata immediatamente la conformità. Se si usa anche l'accesso condizionale, questo viene applicato immediatamente. Se si vuole consentire un periodo di tolleranza, modificare il valore di **Pianifica** nell'azione **Contrassegna il dispositivo come non conforme**.

   Nei criteri di conformità si vuole, ad esempio, anche inviare una notifica all'utente. A questo scopo, è possibile aggiungere l'azione **Invia un messaggio di posta elettronica all'utente finale**. In questa azione **Invia messaggio** si imposta **Pianifica** su due giorni. Se il dispositivo o l'utente finale viene ancora valutato come non conforme il giorno due, il messaggio di posta elettronica viene inviato il giorno due. Se si vuole inviare nuovamente il messaggio di posta elettronica all'utente il giorno cinque della mancata conformità, aggiungere un'altra azione e impostare **Pianifica** su cinque giorni.

   Per altre informazioni sulla conformità e sulle azioni predefinite, vedere la [panoramica della conformità](device-compliance-get-started.md).

6. Al termine, selezionare **Aggiungi** > **OK** per salvare le modifiche.

## <a name="next-steps"></a>Passaggi successivi

[Monitorare i criteri](compliance-policy-monitor.md).
