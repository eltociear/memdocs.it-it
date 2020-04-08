---
title: In fase di sviluppo - Microsoft Intune
titleSuffix: ''
description: Funzionalità di Microsoft Intune in fase di sviluppo
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 04/06/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3f53096f25b4bb05b80d11246ac2fa01486f6e42
ms.sourcegitcommit: 252e718dc58da7d3e3d3a4bb5e1c2950757f50e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/07/2020
ms.locfileid: "80808181"
---
# <a name="in-development-for-microsoft-intune---april-2020"></a>In fase di sviluppo per Microsoft Intune - Aprile 2020

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

### <a name="update-to-android-app-configuration-policies---6113334----"></a>Aggiornamento dei criteri di configurazione delle app Android<!-- 6113334  -->
I criteri di configurazione delle app Android verranno aggiornati per consentire agli amministratori di selezionare il tipo di registrazione del dispositivo prima di creare un profilo di configurazione dell'app. È in corso l'aggiunta della funzionalità per tenere conto dei profili certificato basati sul tipo di registrazione (Profilo di lavoro o Proprietario del dispositivo).  Al rilascio, si verificherà quanto segue:

- Per impostazione predefinita, i criteri esistenti creati prima del rilascio di questa funzionalità che non hanno profili certificato associati useranno il tipo di registrazione del dispositivo Profilo di lavoro e profilo di Proprietario del dispositivo.
- Per impostazione predefinita, i criteri esistenti creati prima del rilascio di questa funzionalità con profili certificato associati useranno il tipo Solo profilo di lavoro.
- Se viene creato un nuovo profilo e si seleziona il tipo di registrazione del dispositivo Profilo di lavoro e profilo di Proprietario del dispositivo, non sarà possibile associare un profilo certificato ai criteri di configurazione dell'app.
- Se viene creato un nuovo profilo ed è selezionato il tipo Solo profilo di lavoro, è possibile usare i criteri di certificato del profilo di lavoro creati con la configurazione del dispositivo.
- Se viene creato un nuovo profilo e si seleziona il tipo Solo proprietario del dispositivo, è possibile usare i criteri di certificato del proprietario del dispositivo creati con la configurazione del dispositivo.

I criteri esistenti non consentiranno di correggere o emettere nuovi certificati.

Verranno aggiunti anche i profili di configurazione di posta elettronica Gmail e Nine che funzioneranno per entrambi i tipi di registrazione Profilo di lavoro e Proprietario del dispositivo, incluso l'uso di profili certificato per entrambi i tipi di configurazione di posta elettronica.  Eventuali criteri per Gmail o Nine creati nell'ambito della configurazione del dispositivo per i profili di lavoro continueranno a essere applicati al dispositivo e non è necessario spostarli nei criteri di configurazione delle app.

Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) è possibile trovare i criteri di configurazione delle app selezionando **App** > **Criteri di configurazione dell'app**. Per altre informazioni sui criteri di configurazione delle app, vedere [Criteri di configurazione delle app per Microsoft Intune](../apps/app-configuration-policies-overview.md).

### <a name="microsoft-teams-is-now-included-in-the-office-365-suite-for-macos---5903936----"></a>Microsoft Teams è ora incluso nella famiglia di prodotti Office 365 per macOS<!-- 5903936  -->
Gli utenti a cui viene assegnato Microsoft Office per macOS in Microsoft Endpoint Manager riceveranno ora Microsoft Teams oltre alle app Microsoft Office esistenti (Word, Excel, PowerPoint, Outlook e OneNote). Intune rileverà i dispositivi Mac esistenti nei quali sono installate altre app Office per macOS e tenterà di installare Microsoft Teams in occasione della successiva sincronizzazione del dispositivo con Intune. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) è possibile trovare **Famiglia di prodotti Office 365** per macOS selezionando **App** > **macOS** > **Aggiungi**. Per altre informazioni, vedere [Assegnare Office 365 a dispositivi macOS con Microsoft Intune](../apps/apps-add-office365-macos.md).

### <a name="group-targeting-support-for-customization-pane----4722837----"></a>Supporto dell'assegnazione di gruppi nel riquadro Personalizzazione <!-- 4722837  -->
Sarà possibile assegnare le impostazioni nel riquadro Personalizzazione a gruppi di utenti. Dal portale di Intune selezionare **App client** > **Personalizzazione**. Per altre informazioni, vedere [Come personalizzare le app Portale aziendale Intune, il sito Web Portale aziendale e l'app Intune](company-portal-app.md].

<!-- ***********************************************-->
## <a name="device-configuration"></a>Configurazione del dispositivo

### <a name="wired-network-device-configuration-profiles-for-macos-devices---3508686----"></a>Profili di configurazione della rete cablata per i dispositivi macOS<!-- 3508686  -->
Sarà disponibile un nuovo profilo di configurazione del dispositivo macOS che configura le reti cablate (**Configurazione dispositivo** > **Profili** > **Crea profilo** > **MacOS** per la piattaforma > **Rete cablata** per il tipo di profilo). Usare questa funzionalità per creare profili 802.1x per gestire le reti cablate e distribuire tali reti nei dispositivi macOS.

Si applica a:
- macOS

### <a name="device-configuration-profile-settings-and-values-will-be-updated-for-windows-platforms---4091122---"></a>Le impostazioni e i valori del profilo di configurazione del dispositivo verranno aggiornati per le piattaforme Windows<!-- 4091122 -->
Quando si creano profili di configurazione dei dispositivi per le piattaforme Windows (**Dispositivi** > **Profili di configurazione** > **Crea profilo** > qualsiasi opzione **Windows** per la piattaforma), alcune impostazioni e i relativi valori sono diversi da quelli del provider CSP e potrebbero generare confusione. I nomi delle impostazioni e i relativi valori verranno aggiornati in modo da essere più chiari.

Si applica a:

- Profilo di configurazione dei dispositivi Windows 10 e versioni successive
- Profili di configurazione dei dispositivi Windows Holographic for Business
- Profili di configurazione dei dispositivi Windows 8.1
- Profili di configurazione dei dispositivi Windows Phone 8.1

### <a name="configure-the-microsoft-defender-atp-app-for-macos-----5520115----"></a>Configurare l'app Microsoft Defender ATP per macOS  <!-- 5520115  -->
A breve sarà possibile configurare le [impostazioni](../protect/endpoint-protection-macos.md) per l'app Microsoft Defender ATP per i dispositivi che eseguono macOS come parte di un profilo di configurazione di un dispositivo Endpoint Protection (**Dispositivi** > **Profili di configurazione** > **Crea profilo**, selezionare **macOS** per *Piattaforma* e quindi **Endpoint Protection** per *Tipo di profilo*). Per la configurazione del dispositivo macOS saranno presenti otto impostazioni. 

Defender ATP è supportato in macOS 10.13 (High Sierra) e versioni successive e l'app [Microsoft Defender ATP](../apps/apps-advanced-threat-protection-macos.md) deve essere distribuita nel dispositivo *dopo* l'applicazione di queste impostazioni. Le impostazioni devono essere inviate al dispositivo prima della distribuzione dell'app. Le versioni beta di macOS non saranno supportate.

### <a name="new-filevault-setting-for-macos-endpoint-protection-device-configuration-policy---5459801-----"></a>Nuova impostazione FileVault per i criteri di configurazione del dispositivo Endpoint Protection per macOS<!-- 5459801   -->
È in corso l'aggiunta di una nuova impostazione alla categoria FileVault nel modello di [Endpoint Protection per macOS](../protect/endpoint-protection-macos.md): Nascondi la chiave di ripristino (**Dispositivi** > **Profili di configurazione** > **Crea profilo**, selezionare **macOS** per *Piattaforma* e quindi **Endpoint Protection** per *Tipo di profilo*). Questa impostazione nasconde la chiave personale all'utente finale durante la crittografia FileVault 2. Un utente di un dispositivo può visualizzare la chiave di ripristino personale in qualsiasi momento dall'app Portale aziendale di iOS o dal sito Web del portale aziendale per il dispositivo macOS crittografato. Per visualizzare la chiave di ripristino personale, può passare ai dettagli del dispositivo e fare clic su *Ottieni la chiave di ripristino*.

Questa impostazione non sarà disponibile nei criteri creati in precedenza. Per configurare questa impostazione e poterla usare, sarà necessario ricreare i criteri di FileVault. 

### <a name="send-push-notifications-as-an-action-for-non-compliance----1733150-----"></a>Inviare notifiche push come azione per la mancata conformità <!-- 1733150   -->
Per le piattaforme iOS e Android, verrà aggiunta una nuova azione per la mancata conformità che invierà una notifica push dell'app tramite l'app Portale aziendale. Gli utenti possono fare clic sulle notifiche e verrà avviata l'app Portale aziendale in cui verrà indicato il motivo per cui non sono conformi. Gli amministratori potranno configurare questa nuova azione per la mancata conformità nell'interfaccia di amministrazione di Microsoft Endpoint Manager passando a **Dispositivi** > **Criteri di conformità** > **Crea criterio** e quindi selezionando *Azione* per inviare una notifica push dell'app.

### <a name="pre-release-testing-for-managed-google-play-apps---2681933----"></a>Test della versione preliminare per le app gestite di Google Play<!-- 2681933  -->
Le organizzazioni che usano [percorsi di test chiusi di Google Play per i test di versioni non definitive dell'app](https://support.google.com/googleplay/android-developer/answer/3131213) potranno gestire questi percorsi con Intune. Sarà possibile assegnare in modo selettivo le app line-of-business pubblicate nei percorsi di pre-produzione di Google Play ai gruppi pilota per eseguire i test. In Intune sarà anche possibile verificare se per un'app è stato pubblicato un percorso di test di compilazione di pre-produzione, oltre a poter assegnare tale percorso a gruppi di utenti o di dispositivi di AAD. Questa funzionalità è disponibile per tutti gli scenari di Android Enterprise attualmente supportati (profilo di lavoro, completamente gestito e dedicato). Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) è possibile aggiungere un'app Google Play gestita selezionando **App** > **Android** > **Aggiungi**. Per altre informazioni, vedere [Aggiungere app di Google Play gestite a dispositivi Android Enterprise con Intune](../apps/apps-add-android-for-work.md).

### <a name="manage-smime-settings-for-outlook-on-android---6517085-----"></a>Gestire le impostazioni S/MIME per Outlook in Android<!-- 6517085   -->
Sarà possibile usare i criteri di configurazione delle app per gestire l'impostazione S/MIME per Outlook nei dispositivi che eseguono Android Enterprise. Sarà anche possibile scegliere se consentire o meno agli utenti del dispositivo di abilitare o disabilitare S/MIME nelle impostazioni di Outlook. Per usare i criteri di configurazione delle app per Android, nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) passare ad **App** > **Criteri di configurazione dell'app**  > **Aggiungi** > **Dispositivi gestiti**.

### <a name="additional-options-in-sso-and-sso-app-extension-profiles-on-iosipados-devices---6504155----"></a>Opzioni aggiuntive nei profili SSO e di estensione dell'app per l'accesso SSO nei dispositivi iOS/iPadOS<!-- 6504155  -->
Nei dispositivi iOS/iPadOS è possibile:

- Nei profili SSO (**Dispositivi** > **Profili di configurazione** > **Crea profilo** > **iOS/iPadOS** per la piattaforma > **Funzionalità del dispositivo** per il profilo > **Single Sign-On**), impostare il nome dell'entità Kerberos sul nome dell'account di gestione degli account di sicurezza (SAM) nei profili SSO. 
- Nei profili di estensione dell'app per l'accesso SSO (**Dispositivi** > **Profili di configurazione** > **Crea profilo** > **iOS/iPadOS** per la piattaforma > **Funzionalità del dispositivo** per il profilo > **Estensione dell'app per l'accesso Single Sign-On**), configurare l'estensione Microsoft Azure AD iOS/iPadOS con meno clic usando un nuovo tipo di estensione dell'app per l'accesso Single Sign-On. È possibile abilitare l'estensione Azure AD per i dispositivi condivisi e inviare i dati specifici dell'estensione all'estensione.

Si applica a:
- iOS/iPadOS 13.0+

Per altre informazioni sull'uso di Single Sign-On nei dispositivi iOS/iPadOS, vedere [Panoramica dell'estensione dell'app Single Sign-On](../configuration/device-features-configure.md#single-sign-on-app-extension) ed [Elenco delle impostazioni di Single Sign-On](../configuration/ios-device-features-settings.md#single-sign-on-app-extension).

<!-- ***********************************************-->
## <a name="device-enrollment"></a>Registrazione del dispositivo

### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344---"></a>I dispositivi BYOD (Bring Your Own Device) possono usare la VPN per la distribuzione<!--5015344 -->
Il nuovo profilo di Autopilot **Ignora il controllo della connettività al dominio** consente di distribuire dispositivi aggiunti ad Azure AD ibrido senza accedere alla rete aziendale usando il proprio client VPN Win32 di terze parti. Per visualizzare il nuovo interruttore, passare all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Dispositivi**  > **Windows** > **Registrazione Windows** > **Profili di distribuzione** > **Crea profilo** > **Configurazione guidata**.

<!-- ***********************************************-->
## <a name="device-management"></a>Gestione dei dispositivi

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>Supporto degli script di PowerShell per dispositivi BYOD<!-- 1862833  -->
Gli script di PowerShell supporteranno i dispositivi registrati con Azure AD in Intune. Per altre informazioni su PowerShell, vedere [Usare gli script di PowerShell nei dispositivi Windows 10 in Intune](../apps/intune-management-extension.md). Questa funzionalità non supporta i dispositivi che eseguono Windows 10 Home Edition.

### <a name="script-support-for-macos-devices---4280361----"></a>Supporto degli script per i dispositivi macOS<!-- 4280361  -->
Sarà possibile aggiungere e distribuire script nei dispositivi macOS. Questo supporto consente di configurare i dispositivi macOS oltre le normali possibilità usando le funzionalità MDM native nei dispositivi macOS.

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics includerà il log dei dettagli del dispositivo<!--6014987  -->
I log dei dettagli dei dispositivi di Intune saranno disponibili in **Report** > **Log Analytics**. È possibile correlare i dettagli dei dispositivi per creare query personalizzate e cartelle di lavoro di Azure.

### <a name="push-notification-when-device-ownership-type-is-changed---5575875----"></a>Notifica push quando cambia il tipo di proprietà del dispositivo<!-- 5575875  -->
Sarà possibile configurare una notifica push da inviare agli utenti del portale aziendale sia Android che iOS quando il tipo di proprietà del dispositivo cambia da personale ad aziendale come servizio di cortesia per la privacy. Questa impostazione è disponibile in Microsoft Endpoint Manager selezionando **Amministrazione tenant** > **Personalizzazione**. Per altre informazioni sull'impatto della proprietà dei dispositivi sugli utenti finali, vedere [Modificare la proprietà del dispositivo](../enrollment/corporate-identifiers-add.md#change-device-ownership).

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



