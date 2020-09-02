---
title: Impostazioni personalizzate - Dispositivi Windows Holographic for Business - Microsoft Intune | Microsoft Docs
description: Aggiungere o creare un profilo personalizzato per usare le impostazioni OMA-URI per i dispositivi che eseguono Windows Holographic for Business in Microsoft Intune, incluso Microsoft Hololens. È possibile configurare le impostazioni del provider del servizio di configurazione (CSP) dei criteri AllowFastReconnect, AllowVPN, AllowUpdateService, UpdateServiceURL, RequireUpdatesApproval, ApprovedUpdates e ApplicationLaunchRestrictions.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.article: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.topic: reference
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3928cd13b5368c8ab196a67669cb3a9f7d3fc2e9
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/26/2020
ms.locfileid: "88910027"
---
# <a name="use-custom-settings-for-windows-holographic-for-business-devices-in-intune"></a>Usare le impostazioni personalizzate per i dispositivi Windows Holographic for Business in Intune

Con Microsoft Intune è possibile aggiungere o creare impostazioni personalizzate per i dispositivi Windows Holographic for Business usando i "profili personalizzati". I profili personalizzati sono una funzionalità di Intune. Sono progettati per aggiungere impostazioni dei dispositivi e funzionalità non incluse in Intune.

I profili personalizzati Windows Holographic for Business usano impostazioni Open Mobile Alliance Uniform Resource Identifier (OMA-URI) per configurare funzionalità diverse. Tali impostazioni vengono in genere usate dai produttori di dispositivi mobili per controllare le funzionalità del dispositivo.

Windows Holographic for Business rende disponibili molte impostazioni dei provider di servizi di configurazione (CSP). Per una panoramica sui provider di servizi di configurazione, vedere [Introduzione ai provider di servizi di configurazione per i professionisti IT](/windows/configuration/provisioning-packages/how-it-pros-can-use-configuration-service-providers). Per i provider di servizi di configurazione specifici supportati da Windows Holographic, vedere [Provider di servizi di configurazione supportati in Windows Holographic](/windows/client-management/mdm/configuration-service-provider-reference#hololens).

Se si sta cercando una determinata impostazione, tenere presente che il [profilo di restrizione del dispositivo Windows Holographic for Business](device-restrictions-windows-holographic.md) contiene numerose impostazioni predefinite. Pertanto, potrebbe non essere necessario immettere valori personalizzati.

Questo articolo descrive come creare un profilo personalizzato per i dispositivi Windows Holographic for Business. Contiene anche un elenco delle impostazioni OMA-URI consigliate.

## <a name="before-you-begin"></a>Prima di iniziare

[Creare un profilo personalizzato di Windows 10](custom-settings-configure.md#create-the-profile).

## <a name="custom-oma-uri-settings"></a>Impostazioni OMA-URI personalizzate

**Aggiungi**: Immettere le impostazioni seguenti:

- **Nome**: Immettere un nome univoco per l'impostazione OMA URI per identificarla nell'elenco delle impostazioni.
- **Descrizione**: immettere una descrizione che offra una panoramica dell'impostazione e altri dettagli importanti.
- **OMA-URI (maiuscole/minuscole)** : immettere l'OMA-URI da usare come impostazione.
- **Tipo di dati**: selezionare il tipo di dati da usare per questa impostazione OMA-URI. Le opzioni disponibili sono:

  - Stringa
  - Stringa (file XML)
  - Data e ora
  - Intero
  - A virgola mobile
  - Boolean
  - Base64 (file)

- **Valore**: immettere il valore dati da associare all'impostazione OMA-URI immessa. Il valore varia a seconda del tipo di dati selezionato. Ad esempio, se si seleziona **Data e ora**, selezionare il valore dalla selezione data.

Dopo aver aggiunto alcune impostazioni, è possibile selezionare **Esporta**. **Esporta** crea un elenco di tutti i valori aggiunti in un file con valori delimitati da virgole (file con estensione csv).

## <a name="recommended-custom-settings"></a>Impostazioni personalizzate consigliate

Le impostazioni seguenti sono utili per i dispositivi che eseguono Windows Holographic for Business:

### <a name="allowfastreconnect"></a>[AllowFastReconnect](/windows/client-management/mdm/policy-csp-authentication#authentication-allowfastreconnect)

> [!div class="mx-tableFixed"]
> |URI OMA|Tipo di dati|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Authentication/AllowFastReconnect|Intero<br/>0 - non consentito<br/>1 - consentito (impostazione predefinita)|

### <a name="allowupdateservice"></a>[AllowUpdateService](/windows/client-management/mdm/policy-csp-update#update-allowupdateservice)

> [!div class="mx-tableFixed"]
> |URI OMA|Tipo di dati|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Update/AllowUpdateService|Intero<br/>0 - servizio di aggiornamento non consentito <br/>1 - servizio di aggiornamento consentito (impostazione predefinita)|

### <a name="allowvpn"></a>[AllowVPN](/windows/client-management/mdm/policy-csp-settings#settings-allowvpn)

> [!div class="mx-tableFixed"]
> |URI OMA|Tipo di dati|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Settings/AllowVPN|Intero<br/>0 - non consentito<br/>1 - consentito (impostazione predefinita)|

### <a name="requireupdateapproval"></a>[RequireUpdateApproval](/windows/client-management/mdm/policy-csp-update#update-requireupdateapproval)

> [!div class="mx-tableFixed"]
> |URI OMA|Tipo di dati|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Update/RequireUpdateApproval|Questa impostazione è disponibile in RS5 (build 17763) e versioni precedenti. A partire da 19H1 (build 18362), usare [Windows Update per le aziende](../protect/windows-update-for-business-configure.md).<br/><br/>Intero<br/>0 - non configurato. Il dispositivo installa tutti gli aggiornamenti applicabili.<br/>1 - il dispositivo installa solo gli aggiornamenti sia applicabili sia inclusi nell'elenco degli aggiornamenti approvati. Impostare questo criterio su 1 se il personale IT vuole controllare la distribuzione degli aggiornamenti nei dispositivi, ad esempio quando sono necessari test prima della distribuzione.|

### <a name="scheduledinstalltime"></a>[ScheduledInstallTime](/windows/client-management/mdm/policy-csp-update#update-scheduledinstalltime)

> [!div class="mx-tableFixed"]
> |URI OMA|Tipo di dati|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Update/ScheduledInstallTime|Intero da 0 a 23, dove 0 = 12 AM e 23 = 11 PM<br/>Il valore predefinito è 3.|

### <a name="updateserviceurl"></a>[UpdateServiceURL](/windows/client-management/mdm/policy-csp-update#update-updateserviceurl)

> [!div class="mx-tableFixed"]
> |URI OMA|Tipo di dati|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Update/UpdateServiceUrl|Questa impostazione è disponibile in RS5 (build 17763) e versioni precedenti. A partire da 19H1 (build 18362), usare [Windows Update per le aziende](../protect/windows-update-for-business-configure.md).<br/><br/>Stringa<br/>URL - il dispositivo verifica la disponibilità di aggiornamenti dal server WSUS all'URL specificato.<br/>Non configurato - il dispositivo verifica la disponibilità di aggiornamenti da Microsoft Update.|

### <a name="approvedupdates"></a>[ApprovedUpdates](/windows/client-management/mdm/update-csp)

> [!div class="mx-tableFixed"]
> |URI OMA|Tipo di dati|
> |---|---|
> |./Vendor/MSFT/Update/ApprovedUpdates/*GUID*<br/><br/>**Importante**<br/>È necessario leggere e accettare i contratti di licenza con l'utente finale per conto degli utenti finali. La mancata accettazione rappresenta una violazione degli obblighi legali e contrattuali.|Nodo per le approvazioni degli aggiornamenti e l'accettazione del contratto di licenza con l'utente finale per conto dell'utente finale.<br/><br/>Per altre informazioni, vedere [Update CSP](/windows/client-management/mdm/update-csp) (Provider del servizio di configurazione Update).|

### <a name="applicationlaunchrestrictions"></a>[ApplicationLaunchRestrictions](/windows/client-management/mdm/applocker-csp)

> [!div class="mx-tableFixed"]
> |URI OMA|Tipo di dati|
> |----|---|
> |./Vendor/MSFT/AppLocker/ApplicationLaunchRestrictions/*Grouping*/*ApplicationType*/Policy<br/><br/>**Importante**<br/>L'articolo dedicato al provider del servizio di crittografia AppLocker usa esempi XML con caratteri di escape. Per configurare le impostazioni con profili personalizzati di Intune, è necessario usare XML semplice.|Stringa<br/>Per altre informazioni, vedere [AppLocker CSP](/windows/client-management/mdm/applocker-csp) (Provider del servizio di configurazione AppLocker).|

### <a name="deletionpolicy"></a>[DeletionPolicy](/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |URI OMA|Tipo di dati|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/DeletionPolicy|Intero<br/>0: eliminare immediatamente quando il dispositivo torna a uno stato senza utenti attivi in quel momento<br/>1: eliminare al raggiungimento della soglia di capacità di archiviazione (impostazione predefinita)<br/>2: eliminare al raggiungimento sia della soglia di capacità di archiviazione che della soglia di inattività del profilo|

### <a name="enableprofilemanager"></a>[EnableProfileManager](/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |URI OMA|Tipo di dati|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/EnableProfileManager|Boolean<br/>True: abilita<br/>False: disabilita (impostazione predefinita)|

### <a name="profileinactivitythreshold"></a>[ProfileInactivityThreshold](/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |URI OMA|Tipo di dati|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/ProfileInactivityThreshold|Intero<br/>Il valore predefinito è 30.|

### <a name="storagecapacitystartdeletion"></a>[StorageCapacityStartDeletion](/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |URI OMA|Tipo di dati|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/StorageCapacityStartDeletion|Intero<br/>Il valore predefinito è 25.|

### <a name="storagecapacitystopdeletion"></a>[StorageCapacityStopDeletion](/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |URI OMA|Tipo di dati|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/StorageCapacityStopDeletion|Intero<br/>Il valore predefinito è 50.|

## <a name="find-the-policies-you-can-configure"></a>Individuare i criteri che è possibile configurare

È possibile trovare un elenco completo di tutti i provider di servizi di configurazione (CSP) supportati da Windows Holographic in [Provider di servizi di configurazione supportati in Windows Holographic](/windows/client-management/mdm/configuration-service-provider-reference#hololens). Non tutte le impostazioni sono compatibili con tutte le versioni di Windows Holographic. La tabella in [CSPs supported in Windows Holographic](/windows/client-management/mdm/configuration-service-provider-reference#hololens) (Provider di servizi di configurazione in Windows Holographic) elenca le versioni supportate per ogni provider.

Intune, inoltre, non supporta tutte le impostazioni elencate in [CSPs supported in Windows Holographic](/windows/client-management/mdm/configuration-service-provider-reference#hololens) (Provider di servizi di configurazione in Windows Holographic). Per verificare se Intune supporta l'impostazione desiderata, aprire l'articolo relativo all'impostazione. La pagina di ogni impostazione mostra le operazioni supportate. Per usare Intune, l'impostazione deve supportare l'operazione **Add** o **Replace**.

## <a name="next-steps"></a>Passaggi successivi

[Assegnare il profilo](device-profile-assign.md) e [monitorarne lo stato](device-profile-monitor.md).

Creare un [profilo personalizzato nei dispositivi Windows 10](custom-settings-windows-10.md).

Altre informazioni sui [profili personalizzati](custom-settings-configure.md) in Intune.