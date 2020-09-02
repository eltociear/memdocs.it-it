---
title: Configurare la registrazione di Intune per i dispositivi di proprietà aziendale Android Enterprise con profilo di lavoro
titleSuffix: Microsoft Intune
description: Informazioni su come registrare i dispositivi Android Enterprise di proprietà aziendale con profilo di lavoro in Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 7/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: shthilla
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9a19a78002d0655cf63a8b757ea252fb8992603f
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915263"
---
# <a name="set-up-intune-enrollment-of-android-enterprise-corporate-owned-devices-with-work-profile"></a>Configurare la registrazione di Intune dei dispositivi di proprietà aziendale Android Enterprise con profilo di lavoro

I dispositivi di proprietà aziendale Android Enterprise con un profilo di lavoro sono dispositivi per singoli utenti destinati all'uso personale e aziendale.

Gli utenti finali possono mantenere separati il proprio lavoro e i dati personali ed essere certi che i dati e le applicazioni personali rimangano privati. Gli amministratori possono controllare alcune impostazioni e funzionalità per l'intero dispositivo, tra cui:

- Impostazione dei requisiti per la password del dispositivo
- Controllo del roaming dei dati e Bluetooth
- Configurazione della protezione dal ripristino delle impostazioni predefinite

Intune consente di distribuire app e impostazioni in dispositivi di proprietà aziendale Android Enterprise con profilo di lavoro. Per informazioni dettagliate su Android Enterprise, vedere [Requisiti per Android](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012).

## <a name="device-requirements"></a>Requisiti dei dispositivi

I dispositivi devono soddisfare questi requisiti per essere gestiti come dispositivi di proprietà aziendale con profilo di lavoro Android Enterprise:

- Sistema operativo Android versione 8.0 e successive.
- I dispositivi devono eseguire una distribuzione di Android che include la connettività Google Mobile Services (GMS). I dispositivi devono includere GMS e devono essere in grado di connettersi a GMS.

## <a name="set-up-android-enterprise-corporate-owned-work-profile-device-management"></a>Configurare la gestione dei dispositivi di proprietà aziendale con profilo di lavoro Android Enterprise

Per configurare la gestione dei dispositivi di proprietà aziendale con profilo di lavoro Android Enterprise, seguire questa procedura:

1. Per preparare la gestione dei dispositivi mobili è necessario [impostare l'autorità MDM (Mobile Device Management) su **Microsoft Intune**](../fundamentals/mdm-authority-set.md). Questa opzione viene impostata una sola volta, ovvero quando si configura per la prima volta Intune per la gestione dei dispositivi mobili.
2. [Connettere l'account del tenant di Intune all'account di Google Play gestito](connect-intune-android-enterprise.md).
3. [Creare un profilo di registrazione.](#create-an-enrollment-profile)
4. [Creare un gruppo di dispositivi](#create-a-device-group).
5. [Registrare i dispositivi di proprietà aziendale con profilo di lavoro](#enroll-the-corporate-owned-work-profile-devices).

### <a name="create-an-enrollment-profile"></a>Creare un profilo di registrazione

> [!NOTE]
> I token per i dispositivi di proprietà aziendale con un profilo di lavoro non scadranno automaticamente. Se un amministratore decide di revocare un token, il profilo associato non verrà visualizzato in **Dispositivi** > **Android** > **Registrazione Android** > **Corporate-owned devices with work profile (Preview)** (Dispositivi di proprietà aziendale con profilo di lavoro - anteprima). Per visualizzare tutti i profili associati a token attivi e inattivi, fare clic su **Filtro** e selezionare le caselle per gli stati dei criteri "Attivo" e "Inattivo". 

È necessario creare un profilo di registrazione in modo che gli utenti possano registrare i dispositivi di proprietà aziendale con profilo di lavoro. Il profilo creato fornisce un token di registrazione (stringa casuale) e un codice a matrice (codice QR). A seconda del sistema operativo Android e della versione del dispositivo, per [registrare il dispositivo dedicato](#enroll-the-corporate-owned-work-profile-devices) è possibile usare il token o un codice a matrice.

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) e scegliere **Dispositivi** > **Android** > **Registrazione Android** > **Corporate-owned devices with work profile (Preview)** (Dispositivi di proprietà aziendale con profilo di lavoro - anteprima).
2. Scegliere **Crea profilo** e compilare i campi.
    - **Nome**: digitare un nome che verrà usato per l'assegnazione del profilo al gruppo di dispositivi dinamico.
    - **Descrizione**: Aggiungere una descrizione del profilo (facoltativo).
3. Scegliere **Avanti**.
5. Nella pagina **Rivedi e crea** scegliere **Crea** per creare i criteri.

### <a name="create-a-device-group"></a>Creare un gruppo di dispositivi

È possibile assegnare le app e i criteri a gruppi di dispositivi assegnati o dinamici. Per configurare gruppi di dispositivi di Azure AD dinamici per popolare automaticamente i dispositivi registrati con un profilo di registrazione specifico, seguire questa procedura:

1. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) scegliere **Gruppi** > **Tutti i gruppi** > **Nuovo gruppo**.
2. Nel pannello **Gruppo** compilare i campi obbligatori come segue:
    - **Tipo di gruppo**: Sicurezza
    - **Nome gruppo**: digitare un nome intuitivo, ad esempio Factory 1
    - **Tipo di appartenenza**: Dispositivo dinamico
3. Scegliere **Aggiungi query dinamica**.
4. Nel pannello **Regole di appartenenza dinamica** compilare i campi come segue:
    - **Aggiungi regola di appartenenza dinamica**: Regola semplice
    - **Aggiungi dispositivi dove**: enrollmentProfileName
    - Nella casella centrale scegliere **Uguale a**.
    - Nell'ultimo campo immettere il nome del profilo di registrazione creato in precedenza.
    Per altre informazioni sulle regole di appartenenza dinamica, vedere [Regole di appartenenza dinamica per i gruppi in Azure Active Directory](/azure/active-directory/users-groups-roles/groups-dynamic-membership). 
5. Scegliere **Aggiungi query** > **Crea**.

### <a name="revoke-tokens"></a>Revocare i token

è possibile far scadere immediatamente il token o il codice a matrice. Il token o codice a matrice non sarà più utilizzabile. È possibile usare questa opzione se:
  - il token o codice a matrice viene condiviso accidentalmente con un'entità non autorizzata
  - si completano tutte le registrazioni e il token o codice a matrice non è più necessario

La revoca di un token o codice a matrice non avrà alcun effetto sui dispositivi già registrati.

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) e scegliere **Dispositivi** > **Android** > **Registrazione Android** > **Corporate-owned devices with work profile (Preview)** (Dispositivi di proprietà aziendale con profilo di lavoro - anteprima).
2. Scegliere il profilo che si vuole usare.
3. Scegliere **Token**.
5. Per revocare il token, scegliere **Revoca il token** > **Sì**.

## <a name="enroll-the-corporate-owned-work-profile-devices"></a>Registrare i dispositivi di proprietà aziendale con profilo di lavoro

Gli utenti possono ora [registrare i dispositivi di proprietà aziendale con profilo di lavoro](android-dedicated-devices-fully-managed-enroll.md).

> [!NOTE]
> L'app **Microsoft Intune** verrà installata automaticamente durante la registrazione di un dispositivo di proprietà aziendale con profilo di lavoro.  Questa app è obbligatoria per la registrazione e non può essere disinstallata. 

## <a name="managing-apps-on-android-enterprise-corporate-owned-work-profile-devices"></a>Gestire le app nei dispositivi di proprietà aziendale con profilo di lavoro Android Enterprise

Nei dispositivi di proprietà aziendale con profilo di lavoro Android Enterprise è possibile installare soltanto app con il tipo di assegnazione [impostato su Obbligatoria](../apps/apps-deploy.md#assign-an-app). Le app vengono installate da Google Play Store gestito allo stesso modo dei dispositivi con profilo di lavoro Android Enterprise.

Le app vengono aggiornate automaticamente sui dispositivi gestiti quando lo sviluppatore pubblica un aggiornamento in Google Play.

Per rimuovere un'app dai dispositivi di proprietà aziendale con profilo di lavoro Android Enterprise, è possibile eseguire una delle operazioni seguenti:
- Eliminare la distribuzione dell'app obbligatoria.
- Creare una distribuzione di disinstallazione per l'app.

## <a name="next-steps"></a>Passaggi successivi
- [Distribuire app Android](../apps/apps-deploy.md)
- [Aggiungere criteri di configurazione di Android](../configuration/device-profiles.md)