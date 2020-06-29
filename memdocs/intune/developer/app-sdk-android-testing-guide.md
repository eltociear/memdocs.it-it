---
title: Guida al testing di Microsoft Intune App SDK per sviluppatori di Android
description: La Guida al testing di Microsoft Intune App SDK per Android è utile per testare le app Android gestite da Intune.
keywords: SDK
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 4ef8f421-9610-4d34-a464-cc02eb1578a9
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: dd4ece62215d48f3481923e099feecc992d7aa6d
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/19/2020
ms.locfileid: "85093371"
---
# <a name="microsoft-intune-app-sdk-for-android-developers-testing-guide"></a>Guida al testing di Microsoft Intune App SDK per sviluppatori di Android

La Guida al testing di Microsoft Intune App SDK per Android è progettata per agevolare le operazioni di test per le app Android gestite da Intune.

## <a name="demo-tenant-setup"></a>Configurazione del tenant demo
Se non si dispone già di un tenant con la società, è possibile creare un tenant demo con o senza dati pre-generati. Per accedere a Microsoft CDX, è necessario registrarsi come [partner Microsoft](https://partner.microsoft.com/en-us/business-opportunities/why-microsoft). Per creare un nuovo account:
1. Passare al [sito di creazione del tenant Microsoft CDX](https://cdx.transform.microsoft.com/my-tenants/create-tenant) e creare un tenant di Microsoft 365 Enterprise.
2. [Configurare Intune](../fundamentals/setup-steps.md) per abilitare la gestione di dispositivi mobili (MDM).
3. [Creare gli utenti](../fundamentals/users-add.md).
4. [Creare i gruppi](../fundamentals/groups-add.md).
5. [Assegnare le licenze](../fundamentals/licenses-assign.md) appropriate per i test.


## <a name="azure-portal-policy-configuration"></a>Configurazione dei criteri del portale di Azure
[Creare e assegnare criteri di protezione delle app](../apps/app-protection-policies.md) nel [pannello Intune del portale di Azure](https://portal.azure.com/?feature.customportal=false#blade/Microsoft_Intune_Apps/MainMenu/14/selectedMenuItem/Overview). È anche possibile creare e assegnare i [criteri di configurazione delle app](../apps/app-configuration-policies-overview.md) nel pannello Intune.

> [!NOTE]
> Se l'app non è elencata nel portale di Azure, è possibile impostarla come destinazione con un criterio selezionando l'opzione **Altre app** e specificando il nome del pacchetto nella casella di testo.

## <a name="test-cases"></a>Test case

I test case seguenti illustrano le procedure di configurazione e conferma. Usare questi test per verificare la nuova app Android integrata.

### <a name="required-pin-and-corporate-credentials"></a>PIN obbligatorio e credenziali aziendali

È possibile richiedere un PIN per accedere alle risorse aziendali. È anche possibile imporre l'autenticazione aziendale prima che gli utenti possano usare le app gestite. Ecco come:

1. Impostare **Richiedi PIN per l'accesso** e **Richiedi credenziali aziendali per l'accesso** su **Sì**. Per altre informazioni, vedere [Impostazioni dei criteri di protezione delle app di Android in Microsoft Intune](../apps/app-protection-policy-settings-android.md#access-requirements).
2. Confermare le condizioni seguenti:
    - All'avvio dell'app verrà visualizzato un prompt per l'input del PIN oppure l'utente di produzione che è stato usato durante la registrazione nel Portale aziendale.
    - Se non viene visualizzato un prompt di accesso valido, è possibile che il manifesto Android non sia configurato correttamente, in modo specifico i valori per l'integrazione di ADAL (Azure Active Directory Authentication Library), ovvero SkipBroker ClientID e Authority.
    - Se non vengono visualizzati prompt, la causa potrebbe essere un valore `MAMActivity` integrato in modo non corretto. Per altre informazioni su `MAMActivity`, vedere [Manuale dello sviluppatore di Microsoft Intune App SDK per Android](app-sdk-android.md).

> [!NOTE] 
> Se il test precedente non funziona, è probabile che avranno esito negativo anche i test seguenti. Controllare l'integrazione di [SDK](app-sdk-android.md#sdk-integration) e [ADAL](app-sdk-android.md#configure-azure-active-directory-authentication-library-adal).

### <a name="restrict-transferring-and-receiving-data-with-other-apps"></a>Limitare il trasferimento e la ricezione di dati con altre app
È possibile controllare il trasferimento dei dati tra le applicazioni gestite aziendali come indicato di seguito:

1. Impostare **Consenti all'app di trasferire i dati ad altre app** su **App gestite da criteri**.
2. Impostare **Consenti all'app di ricevere i dati da altre app** su **Tutte le app**. 

Questi criteri condizionano l'uso di finalità e provider di contenuti.
3. Confermare le condizioni seguenti:
    - L'apertura da un'app non gestita nell'app funziona correttamente.
    - È consentita la condivisione del contenuto tra l'app e le app gestite.
    - La condivisione dall'app ad app non gestite (ad esempio Chrome) è bloccata.


#### <a name="restrict-receiving-data-from-other-apps"></a>Limitare la ricezione dei dati da altre app

1. Impostare **Invia i dati dell'organizzazione ad altre app** su **Tutte le app**.
2. Impostare **Ricevi dati da altre app** su **App gestite da criteri**. 
3. Confermare le condizioni seguenti:
    - L'invio di un'app non gestita dall'app funziona correttamente.
    - È consentita la condivisione del contenuto tra l'app e le app gestite.
    - La condivisione da app non gestite (ad esempio, Chrome) all'app è bloccata.

Se l'app richiede [controlli 'Apri da' integrati](app-sdk-android.md#opening-data-from-a-local-or-cloud-storage-location), è possibile controllare la funzionalità **Apri da** come indicato di seguito:

1. Impostare **Ricevi dati da altre app** su **App gestite da criteri**. 
2. Impostare **Apri dati nei documenti dell'organizzazione** su **Blocca**. 
3. Confermare le condizioni seguenti:
    - L'apertura è limitata solo alle posizioni gestite appropriate.

### <a name="restrict-cut-copy-and-paste"></a>Limitare le operazioni taglia, copia e incolla
È possibile limitare gli Appunti di sistema per le applicazioni gestite nel modo seguente:

1. Impostare **Limita le operazioni taglia, copia e incolla con le altre app** su **App gestite da criteri con Incolla in**.
2. Confermare le condizioni seguenti:
    - La copia di testo dalla propria app in un'app non gestita (ad esempio Messaggi) viene bloccata.

### <a name="prevent-save"></a>Impedire il salvataggio
Se l'app richiede [controlli Salva con nome integrati](app-sdk-android.md#example-data-transfer-between-apps-and-device-or-cloud-storage-locations), è possibile controllare la funzionalità **Salva con nome** come indicato di seguito:

1. Impostare **Impedisci 'Salva con nome'** su **Sì**.
2. Confermare le condizioni seguenti:
    - Il comando Salva è limitato solo alle posizioni gestite appropriate.

### <a name="file-encryption"></a>Crittografia file
È possibile crittografare i dati nel dispositivo come indicato di seguito:

1. Impostare **Crittografa dati app** su **Sì**.
2. Confermare le condizioni seguenti:
    - Nessun effetto sul comportamento normale dell'applicazione.

### <a name="prevent-android-backups"></a>Impedire backup in Android
È possibile controllare i backup dell'app come indicato di seguito:

1. Se sono state impostate [limitazioni per il backup integrato](app-sdk-android.md#protecting-backup-data), impostare **Impedisci backup in Android** su **Sì**.
2. Confermare le condizioni seguenti:
    - I backup sono limitati.

### <a name="wipe"></a>Cancellazione
È possibile cancellare in remoto le app gestite dai messaggi di posta elettronica e dai documenti aziendali che le contengono. I dati personali vengono decrittografati quando non sono più amministrati. Ecco come:

1. Dal portale di Azure [eseguire una cancellazione](../apps/apps-selective-wipe.md).
2. Se l'app non è registrata per qualsiasi gestore di cancellazione, verificare le condizioni seguenti:
    - Si verifica una cancellazione completa dell'app.
3. Se l'app è registrata per `WIPE_USER_DATA` o `WIPE_USER_AUXILARY_DATA`, verificare le condizioni seguenti:
    - Il contenuto gestito viene rimosso dall'app. Per altre informazioni, vedere [Manuale dello sviluppatore di Intune App SDK per Android - Cancellazione selettiva](app-sdk-android.md#selective-wipe).

### <a name="multi-identity-support"></a>Supporto di più identità
L'integrazione del [supporto di più identità](app-sdk-android.md#multi-identity-optional) è una modifica ad alto rischio che deve essere testata accuratamente. I problemi più comuni si verificano a causa dell'impostazione non corretta dell'identità attiva (a livello di `Context` o di thread) o perché si tiene traccia in modo improprio delle identità dei file (`MAMFileProtectionManager`).

Verificare almeno quanto segue:

- I criteri per **Salva con nome** funzionano correttamente per le identità gestite.
- Le limitazioni per le operazioni copia e incolla vengono applicate correttamente nel passaggio dal contesto gestito a quello personale.
- Vengono crittografati solo i dati appartenenti all'identità gestita e i file personali non vengono modificati.
- La cancellazione selettiva in fase di l'annullamento della registrazione rimuove solo i dati dell'identità gestita.
- All'utente finale viene richiesto di eseguire l'avvio condizionale quando passa da un account non gestito a un account gestito (solo la prima volta).

### <a name="app-configuration-optional"></a>Configurazione delle app (facoltativa)
Il comportamento delle app gestite può essere configurato. Se l'app utilizza eventuali impostazioni di configurazione delle app, è necessario verificare che l'app gestisca correttamente tutti i valori che possono essere impostati dall'amministratore. È possibile creare e assegnare i [criteri di configurazione dell'app](../apps/app-configuration-policies-overview.md) in Intune.


