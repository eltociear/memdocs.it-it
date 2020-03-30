---
title: In fase di sviluppo - Microsoft Intune
titleSuffix: ''
description: Funzionalità di Microsoft Intune in fase di sviluppo
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/21/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 18b42dffc2c34adea1f70c4587b5eb5384d0a778
ms.sourcegitcommit: 795e8a6aca41e1a0690b3d0d55ba3862f8a683e7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/24/2020
ms.locfileid: "80220133"
---
# <a name="in-development-for-microsoft-intune---march-2020"></a>In fase di sviluppo per Microsoft Intune - Marzo 2020

Per supportare gli utenti nella preparazione e pianificazione, questa pagina illustra gli aggiornamenti e le funzionalità dell'interfaccia utente di Intune che sono in fase di sviluppo ma non ancora rilasciati. Oltre alle informazioni contenute in questa pagina: 

- Se sono previste azioni prima di una modifica, verrà pubblicato un post complementare nel Centro messaggi di Office.
- Quando una funzionalità entra in produzione, sia in versione anteprima sia disponibile a livello generale, la descrizione della funzionalità viene spostata da questa pagina alla [pagina delle novità](whats-new.md).
- Questa pagina e la [pagina delle novità](whats-new.md) vengono aggiornate periodicamente. Consultarla a intervalli regolari per ulteriori aggiornamenti.
- Vedere la [roadmap di Microsoft 365](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS) per informazioni sulle sequenze temporali e i risultati finali strategici.

> [!NOTE]
> Questa pagina riflette le attuali aspettative sulle funzionalità di Intune che verranno introdotte in una versione futura. Le date e le singole funzionalità potrebbero cambiare. Questa pagina non descrive tutte le funzionalità in fase di sviluppo.

**Feed RSS**: è possibile sapere quando questa pagina viene aggiornata copiando e incollando l'URL seguente nel lettore di feed: `https://docs.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us`

<!--
## What's coming to Intune in the Azure portal 
## What's coming to Intune apps
## Notices
-->

<!-- Common categories:  
## App management
## Device configuration
## Device enrollment
## Device management
## Intune apps
## Monitor and troubleshoot
## Role-based access control
## Security

-->
 
<!-- ***********************************************-->
## <a name="app-management"></a>Gestione delle app

### <a name="company-portal-for-ios-to-support-landscape-mode--6048329----"></a>Portale aziendale per iOS per supportare la modalità orizzontale<!--6048329  -->
Gli utenti potranno registrare i dispositivi, trovare le app e ottenere supporto IT usando l'orientamento dello schermo preferito. L'app rileverà automaticamente l'orientamento adattandosi allo schermo in modalità verticale o orizzontale, a meno che gli utenti non blocchino lo schermo in modalità verticale.

### <a name="improved-sign-in-experience-in-company-portal-for-android---6103997----"></a>Esperienza di accesso aggiornata nel Portale aziendale per Android<!-- 6103997  -->
È in corso l'aggiornamento del layout di diverse schermate di accesso nell'app Portale aziendale per Android per rendere l'esperienza più moderna, semplice e pulita per gli utenti.

<!-- ***********************************************-->
## <a name="device-configuration"></a>Configurazione del dispositivo

### <a name="wired-network-device-configuration-profiles-for-macos-devices---3508686----"></a>Profili di configurazione della rete cablata per i dispositivi macOS<!-- 3508686  -->
Sarà disponibile un nuovo profilo di configurazione del dispositivo macOS che configura le reti cablate (**Configurazione dispositivo** > **Profili** > **Crea profilo** > **MacOS** per la piattaforma > **Rete cablata** per il tipo di profilo). Usare questa funzionalità per creare profili 802.1x per gestire le reti cablate e distribuire tali reti nei dispositivi macOS.

Si applica a:
- macOS

### <a name="improved-user-interface-experience-when-creating-configuration-profiles-on-iosipados-and-macos-devices---5569008-5569039-5569057-5569110-5569116-5569131-5569139-5569153-5859984----"></a>Esperienza migliorata dell'interfaccia utente per la creazione dei profili di configurazione nei dispositivi iOS/iPadOS e macOS<!-- 5569008-5569039-5569057-5569110-5569116-5569131-5569139-5569153-5859984  -->
L'esperienza per la creazione di un profilo per i dispositivi iOS/iPadOS o macOS nell'interfaccia di amministrazione di Endpoint Manager verrà aggiornata. Questa modifica ha effetto sui profili di configurazione dei dispositivi elencati di seguito (**Dispositivi** > **Profili di configurazione** > **Crea profilo** > **iOS** o **macOS** per la piattaforma):

- Personalizzata: iOS/iPadOS, macOS
- Funzionalità del dispositivo: iOS/iPadOS, macOS
- Limitazioni del dispositivo: iOS/iPadOS, macOS
- Endpoint Protection: macOS
- Estensioni: macOS
- File delle preferenze: macOS

### <a name="improved-user-interface-experience-when-creating-oemconfig-configuration-profiles-on-android-enterprise-devices---5568645-----"></a>Esperienza migliorata dell'interfaccia utente per la creazione dei profili di configurazione OEMConfig nei dispositivi Android Enterprise<!-- 5568645   -->
L'esperienza per la creazione o la modifica di un profilo OEMConfig per i dispositivi Android Enterprise nell'interfaccia di amministrazione di Endpoint Manager verrà aggiornata. Nell'esperienza aggiornata sarà disponibile una panoramica di riepilogo delle impostazioni configurate. Questa modifica ha effetto sul profilo di configurazione del dispositivo di OEMConfig (**Dispositivi** > **Profili di configurazione** > **Crea profilo** > **Android Enterprise** per la piattaforma > **OEMConfig** per il tipo di profilo).

Questa funzionalità si applica a:
- Android Enterprise 

### <a name="device-configuration-profile-settings-and-values-will-be-updated-for-windows-platforms---4091122---"></a>Le impostazioni e i valori del profilo di configurazione del dispositivo verranno aggiornati per le piattaforme Windows<!-- 4091122 -->
Quando si creano profili di configurazione dei dispositivi per le piattaforme Windows (**Dispositivi** > **Profili di configurazione** > **Crea profilo** > qualsiasi opzione **Windows** per la piattaforma), alcune impostazioni e i relativi valori sono diversi da quelli del provider CSP e potrebbero generare confusione. I nomi delle impostazioni e i relativi valori verranno aggiornati in modo da essere più chiari.

Si applica a:

- Profilo di configurazione dei dispositivi Windows 10 e versioni successive
- Profili di configurazione dei dispositivi Windows Holographic for Business
- Profili di configurazione dei dispositivi Windows 8.1
- Profili di configurazione dei dispositivi Windows Phone 8.1

### <a name="improved-user-interface-experience-when-creating-device-restrictions-profiles-on-android-and-android-enterprise-devices---5841361---"></a>Esperienza migliorata dell'interfaccia utente per la creazione dei profili di limitazioni dei dispositivi in dispositivi Android e Android Enterprise<!-- 5841361 -->
L'esperienza per la creazione di un profilo per i dispositivi Android e Android Enterprise nell'interfaccia di amministrazione di Endpoint Manager verrà aggiornata. Questa modifica ha effetto sui profili di configurazione dei dispositivi seguenti (**Dispositivi** > **Profili di configurazione** > **Crea profilo** > **Amministratore di dispositivi Android** o **Android Enterprise** per la piattaforma):

- Limitazioni dei dispositivi: Amministratore dispositivo Android
- Limitazioni dei dispositivi: Proprietario del dispositivo Android Enterprise
- Limitazioni dei dispositivi: Profilo di lavoro di Android Enterprise

Per altre informazioni sulle restrizioni dei dispositivi che è possibile configurare, vedere [Amministratore di dispositivi Android](../configuration/device-restrictions-android.md) e [Android Enterprise](../configuration/device-restrictions-android-for-work.md).

### <a name="configure-the-microsoft-defender-atp-app-for-macos-----5520115----"></a>Configurare l'app Microsoft Defender ATP per macOS  <!-- 5520115  -->
A breve sarà possibile configurare le [impostazioni](../protect/endpoint-protection-macos.md) per l'app Microsoft Defender ATP per i dispositivi che eseguono macOS come parte di un profilo di configurazione di un dispositivo Endpoint Protection (**Dispositivi** > **Profili di configurazione** > **Crea profilo**, selezionare **macOS** per *Piattaforma* e quindi **Endpoint Protection** per *Tipo di profilo*). Per la configurazione del dispositivo macOS saranno presenti otto impostazioni. 

Defender ATP è supportato in macOS 10.13 (High Sierra) e versioni successive e l'app [Microsoft Defender ATP](../apps/apps-advanced-threat-protection-macos.md) deve essere distribuita nel dispositivo *dopo* l'applicazione di queste impostazioni. Le impostazioni devono essere inviate al dispositivo prima della distribuzione dell'app. Le versioni beta di macOS non saranno supportate.

### <a name="new-filevault-setting-for-macos-endpoint-protection-device-configuration-policy---5459801-----"></a>Nuova impostazione FileVault per i criteri di configurazione del dispositivo Endpoint Protection per macOS<!-- 5459801   -->
È in corso l'aggiunta di una nuova impostazione alla categoria FileVault nel modello di [Endpoint Protection per macOS](../protect/endpoint-protection-macos.md): Nascondi la chiave di ripristino (**Dispositivi** > **Profili di configurazione** > **Crea profilo**, selezionare **macOS** per *Piattaforma* e quindi **Endpoint Protection** per *Tipo di profilo*). Questa impostazione nasconde la chiave personale all'utente finale durante la crittografia FileVault 2. Un utente di un dispositivo può visualizzare la chiave di ripristino personale in qualsiasi momento dall'app Portale aziendale di iOS o dal sito Web del portale aziendale per il dispositivo macOS crittografato. Per visualizzare la chiave di ripristino personale, può passare ai dettagli del dispositivo e fare clic su *Ottieni la chiave di ripristino*.

Questa impostazione non sarà disponibile nei criteri creati in precedenza. Per configurare questa impostazione e poterla usare, sarà necessario ricreare i criteri di FileVault. 

### <a name="configure-delivery-optimization-agent-when-downloading-win32-app-content---5410945----"></a>Configurare l'agente di ottimizzazione recapito durante il download del contenuto dell'app Win32<!-- 5410945  -->
Sarà possibile configurare l'agente di ottimizzazione recapito per scaricare il contenuto dell'app Win32 in background o in primo piano in base all'assegnazione. Per le app Win32 esistenti, il contenuto continuerà a essere scaricato in background. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) selezionare **App** > **Tutte le app** > *selezionare l'app Win32* > **Proprietà**. Selezionare l'opzione **Modifica** accanto ad **Assegnazioni**.  Modificare l'assegnazione selezionando **Includi** nell'area **Modalità** della sezione **Richiesto**.  Quando diventerà disponibile, la nuova impostazione sarà visibile nella sezione **Impostazioni app**. Per altre informazioni sull'ottimizzazione recapito, vedere [Gestione delle app Win32 - Ottimizzazione recapito](../apps/apps-win32-app-management.md#delivery-optimization).

<!-- ***********************************************-->
<!--## Device enrollment-->

<!-- ***********************************************-->
## <a name="device-management"></a>Gestione dei dispositivi

### <a name="change-primary-user-for-windows-devices----3794742---"></a>Modificare l'utente primario per i dispositivi Windows <!-- 3794742 -->
Sarà possibile modificare l'utente primario per i dispositivi Windows ibridi e aggiunti ad Azure AD. A tale scopo, passare a **Intune** > **Dispositivi** > **Tutti i dispositivi** > scegliere un dispositivo **Proprietà** > **Utente primario**.

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>Supporto degli script di PowerShell per dispositivi BYOD<!-- 1862833  -->
Gli script di PowerShell supporteranno i dispositivi registrati con Azure AD in Intune. Per altre informazioni su PowerShell, vedere [Usare gli script di PowerShell nei dispositivi Windows 10 in Intune](../apps/intune-management-extension.md). Questa funzionalità non supporta i dispositivi che eseguono Windows 10 Home Edition.

### <a name="new-information-in-device-details---5604099---"></a>Nuove informazioni nei dettagli del dispositivo<!-- 5604099 -->
Le informazioni seguenti saranno presenti nella pagina **Panoramica** per i dispositivi:

- Capacità di archiviazione (quantità di spazio di archiviazione fisico nel dispositivo)
- Capacità di memoria (quantità di memoria fisica nel dispositivo)

### <a name="script-support-for-macos-devices---4280361----"></a>Supporto degli script per i dispositivi macOS<!-- 4280361  -->
Sarà possibile aggiungere e distribuire script nei dispositivi macOS. Questo supporto consente di configurare i dispositivi macOS oltre le normali possibilità usando le funzionalità MDM native nei dispositivi macOS.

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
<!--
## Monitor and troubleshoot
-->

<!-- ***********************************************-->
<!--
## Role-based access control
-->

<!-- ***********************************************-->
## <a name="security"></a>Sicurezza

### <a name="derived-credentials-support-on-android-fully-managed-devices--4839592--"></a>Supporto di credenziali derivate nei dispositivi Android completamente gestiti<!--4839592-->
Sarà possibile usare credenziali derivate nei dispositivi Android Enterprise completamente gestiti. Verrà incluso il supporto per il recupero di una credenziale derivata per Entrust Datacard, Intercede e DISA Purebred. Sarà possibile usare una credenziale derivata per l'autenticazione di app, Wi-Fi, VPN o la firma S/MIME e/o la crittografia, se supportata dalle app.

### <a name="privacy-preferences-settings-for-macos-devices---2934232---"></a>Impostazioni delle preferenze per la privacy per i dispositivi macOS<!-- 2934232 --> 
Nella versione di macOS Catalina 10.15 Apple ha aggiunto nuovi miglioramenti alla sicurezza e alla privacy. Per impostazione predefinita, le applicazioni e i processi non riescono ad accedere a dati specifici senza il consenso utente. Se gli utenti non forniscono il consenso, le applicazioni e i processi potrebbero non funzionare. In Intune verrà aggiunto il supporto per le impostazioni che permettono agli amministratori IT di accettare o rifiutare il consenso per l'accesso ai dati per conto degli utenti finali nei dispositivi che eseguono macOS 10.14 e versioni successive. Queste impostazioni garantiscono che le applicazioni e i processi continuino a funzionare correttamente e riducono il numero di richieste visualizzate dagli utenti finali.

### <a name="updated-ui-text-and-labels-for-windows-10-endpoint-protection-profile-settings---5983747---"></a>Testo ed etichette dell'interfaccia utente aggiornati per le impostazioni del profilo di Endpoint Protection per Windows 10<!-- 5983747 -->
È in corso l'aggiornamento del testo per le varie impostazioni configurate come profili di configurazione dei dispositivi Windows 10 per rendere più comprensibili l'uso previsto delle impostazioni e i risultati.

Le impostazioni che verranno aggiornate includono i profili di configurazione dei dispositivi Windows 10 per:

- [Limitazioni del dispositivo](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus) > Microsoft Defender Antivirus  
- [Endpoint Protection](../protect/endpoint-protection-windows-10.md) > Microsoft Defender Antivirus

Le impostazioni supportate con Intune non cambiano. Si tratta solo di un aggiornamento del testo dell'interfaccia utente dell'interfaccia di amministrazione di Microsoft Endpoint Management.

<!-- ***********************************************-->
## <a name="notices"></a>Notifiche

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Vedere anche

Per informazioni dettagliate sugli ultimi sviluppi, vedere [Novità di Microsoft Intune](whats-new.md).
