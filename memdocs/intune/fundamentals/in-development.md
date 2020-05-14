---
title: In fase di sviluppo - Microsoft Intune
titleSuffix: ''
description: Funzionalità di Microsoft Intune in fase di sviluppo
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 04/28/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7827c85585d630f64ba9c6d342b6275fca506b1d
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906965"
---
# <a name="in-development-for-microsoft-intune"></a>In fase di sviluppo per Microsoft Intune

Per supportare gli utenti nella preparazione e pianificazione, questa pagina illustra gli aggiornamenti e le funzionalità dell'interfaccia utente di Intune che sono in fase di sviluppo ma non ancora rilasciati. Oltre alle informazioni contenute in questa pagina: 

- Se sono previste azioni prima di una modifica, verrà pubblicato un post complementare nel Centro messaggi di Office.
- Quando una funzionalità entra in produzione, sia in versione anteprima sia disponibile a livello generale, la descrizione della funzionalità viene spostata da questa pagina alla [pagina delle novità](whats-new.md).
- Questa pagina e la [pagina delle novità](whats-new.md) vengono aggiornate periodicamente. Consultarla a intervalli regolari per ulteriori aggiornamenti.
- Vedere la [roadmap di Microsoft 365](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS) per informazioni sulle sequenze temporali e i risultati finali strategici.

> [!NOTE]
> Questa pagina riflette le attuali previsioni su funzionalità di Intune che verranno introdotte in una versione futura. Le date e le singole funzionalità potrebbero cambiare. Questa pagina non descrive tutte le funzionalità in fase di sviluppo.

**Feed RSS**: è possibile sapere quando questa pagina viene aggiornata copiando e incollando l'URL seguente nel lettore di feed: `https://docs.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us`

**Questo articolo è stato aggiornato l'ultima volta nella data indicata sotto al titolo precedente**.

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

### <a name="support-for-multiple-accounts-in-company-portal-for-mac---5779449----"></a>Supporto di più account nel Portale aziendale per Mac<!-- 5779449  -->
Il Portale aziendale nei dispositivi macOS ora memorizza nella cache gli account utente, semplificando l'accesso. Non è più necessario che gli utenti eseguano l'accesso al Portale aziendale ogni volta che avviano l'applicazione. Se nella cache sono memorizzati più account, il Portale aziendale visualizzerà anche un selettore di account, in modo che gli utenti non debbano immettere il nome utente. 

### <a name="auto-update-vpp-available-apps---3640511----"></a>Aggiornamento automatico delle app disponibili per VPP<!-- 3640511  -->
Le app che vengono pubblicate come disponibili per il Volume Purchase Program (VPP) di Apple verranno aggiornate automaticamente quando **Aggiornamenti automatici delle app** è abilitata per il token VPP. Attualmente le app disponibili per il Volume Purchase Program di Apple non vengono aggiornate automaticamente. Gli utenti finali devono accedere al Portale aziendale e reinstallare l'app quando è disponibile una versione aggiornata. Tuttavia le app obbligatorie supportano gli aggiornamenti automatici.

### <a name="customize-self-service-device-actions-in-the-company-portal--4393379----"></a>Personalizzare le azioni self-service nel Portale aziendale<!--4393379  -->
Sarà possibile personalizzare le azioni del dispositivo self-service disponibili che vengono visualizzate per gli utenti finali nell'app e nel sito Web Portale aziendale. Per contribuire a evitare le azioni non previste nel dispositivo, sarà possibile configurare queste impostazioni per l'app Portale aziendale selezionando **Amministrazione del tenant** > **Personalizzazione** > **Crea** > **Nascondi le funzionalità**. Sono disponibili le azioni seguenti:
- Nascondi il pulsante **Rimuovi** nei dispositivi Windows aziendali.
- Nascondi il pulsante **Ripristina** nei dispositivi Windows aziendali.
- Nascondi il pulsante **Ripristina** nei dispositivi iOS aziendali.
- Nascondi il pulsante **Rimuovi** nei dispositivi iOS aziendali.

Per altre informazioni, vedere [Azioni self-service che l'utente può eseguire nel dispositivo dal Portale aziendale](../apps/company-portal-app.md#user-self-service-device-actions-from-the-company-portal).

### <a name="unified-delivery-of-azure-ad-enterprise-or-office-online-applications-in-the-company-portal--4404429---"></a>Distribuzione unificata di applicazioni Azure AD Enterprise o Office Online nel Portale aziendale<!--4404429 -->
Sarà possibile alternare (**Nascondi** o **Mostra**) la visualizzazione di applicazioni Azure AD Enterprise o Office Online nel Portale aziendale. Ogni utente visualizzerà l'intero catalogo applicazioni dal servizio Microsoft scelto. Per impostazione predefinita, ogni origine di app aggiuntiva verrà impostata su **Nascondi**. Questa funzionalità verrà applicata inizialmente nel sito Web Portale aziendale della versione 2005, e successivamente verrà supportata nei Portali aziendali Windows, iOS/iPadOS e macOS. Per trovare questa impostazione in futuro, nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) selezionare **Amministrazione del tenant** > **Personalizzazione**. Per informazioni correlate, vedere [Come personalizzare le app Portale aziendale Intune, il sito Web Portale aziendale e l'app Intune](../apps/company-portal-app.md).

### <a name="search-the-intune-docs-from-the-company-portal---1736480---"></a>Ricerca nella documentazione di Intune dal Portale aziendale<!-- 1736480 -->
Ora è possibile eseguire ricerche nella documentazione di Intune direttamente dall'app Portale aziendale per macOS. Nella barra dei menu selezionare **Guida** > **Cerca** e immettere le parole chiave della ricerca per trovare rapidamente risposte alle domande.

### <a name="company-portal-for-android-will-guide-users-to-get-apps-after-work-profile-enrollment----6103999----"></a>Il Portale aziendale per Android consente agli utenti di ottenere le app dopo la registrazione del profilo di lavoro <!-- 6103999  -->
È in corso il miglioramento delle linee guida all'interno del Portale aziendale, in modo da facilitare la ricerca e l'installazione di app per gli utenti.  Dopo aver eseguito la registrazione nella gestione del profilo di lavoro, gli utenti visualizzeranno un messaggio che informa che è possibile trovare le app suggerite nella versione con badge di Google Play. Gli utenti visualizzeranno anche un nuovo collegamento **Scarica app** nel cassetto del Portale aziendale sul lato sinistro. Per dare più spazio a queste esperienze nuove e migliorate, la scheda **App** verrà rimossa. 

### <a name="android-company-portal-user-experience---5736084---"></a>Esperienza utente per il Portale aziendale Android<!-- 5736084 -->
Nella versione 2005 del Portale aziendale Android gli utenti finali di dispositivi Android che ricevono un avviso, un blocco o una cancellazione da un criterio di protezione delle app visualizzeranno una nuova esperienza utente. Al posto dell'esperienza corrente con finestra di dialogo corrente, gli utenti finali visualizzeranno un messaggio a tutta pagina che include il motivo dell'avviso, blocco o cancellazione e i passaggi per risolvere il problema. Per altre informazioni, vedere [Esperienza di protezione delle app per dispositivi Android](../apps/app-protection-policy.md#app-protection-experience-for-android-devices) e [Impostazioni dei criteri di protezione delle app di Android in Microsoft Intune](../apps/app-protection-policy-settings-android.md).


<!-- ***********************************************-->
## <a name="device-configuration"></a>Configurazione del dispositivo

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

### <a name="configure-system-extensions-on-macos-devices---6255624----"></a>Configurare le estensioni del sistema nei dispositivi macOS<!-- 6255624  -->
Nei dispositivi macOS è possibile creare un profilo di estensioni del kernel per configurare impostazioni a livello del kernel (**Dispositivi** > **Profili di configurazione** > **macOS** per la piattaforma > **Estensioni del kernel** per il profilo). Apple prevede di impostare come deprecate le estensioni del kernel e di sostituirle con estensioni del sistema in una versione futura. Le estensioni del sistema vengono eseguite nello spazio dell'utente e non consentono l'accesso al kernel. L'obiettivo è aumentare la protezione e garantire un maggior controllo a livello dell'utente finale, limitando nel contempo gli attacchi a livello del kernel. Sia le estensioni del kernel sia le estensioni del sistema consentono agli utenti di installare estensioni delle app che incrementano la capacità nativa del sistema operativo.

In Intune è possibile configurare le estensioni del kernel e le estensioni del sistema (**Dispositivi** > **Profili di configurazione** > **macOS** per la piattaforma > **Estensioni del sistema** per il profilo). Le estensioni del kernel sono valide per la versione 10.13.2 e versioni successive. Le estensioni del sistema sono valide per la versione 10.15 e versioni successive. Da macOS 10.15 a macOS 10.15.4, le estensioni del kernel e le estensioni del sistema possono essere eseguite simultaneamente. 

Per informazioni sulle estensioni del kernel nei dispositivi macOS, vedere [Aggiungere le estensioni del kernel macOS](../configuration/kernel-extensions-overview-macos.md).

Si applica a:
- macOS 10.15 e versioni successive

<!-- ***********************************************-->
## <a name="device-enrollment"></a>Registrazione del dispositivo

### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344---"></a>I dispositivi BYOD (Bring Your Own Device) possono usare la VPN per la distribuzione<!--5015344 -->
È possibile che questa funzionalità venga posticipata.

### <a name="automated-device-sync-interval-down-to-12-hours--3077535---"></a>Intervallo di sincronizzazione automatica dei dispositivi ridotto a 12 ore<!--3077535 -->
Per la Registrazione automatica dei dispositivi di Apple, l'intervallo di sincronizzazione automatica dei dispositivi tra Intune e Apple Business Manager verrà ridotto da 24 a 12 ore. Per altre informazioni sulla sincronizzazione, vedere [Sincronizzare i dispositivi gestiti](../enrollment/device-enrollment-program-enroll-ios.md#sync-managed-devices).

### <a name="autopilot-support-for-hololens-2-devices--6305220--"></a>Supporto dei dispositivi Hololens 2 in Autopilot<!--6305220-->
Windows Autopilot supporterà i dispositivi Hololens 2. Per altre informazioni sull'uso di Autopilot in Intune, vedere [Registrare dispositivi Windows in Intune con Windows Autopilot](../enrollment/enrollment-autopilot.md).

### <a name="enrollment-restrictions-will-support-scope-tags--4209550---"></a>Le restrizioni di registrazione supporteranno i tag di ambito<!--4209550 -->
Sarà possibile assegnare tag di ambito alle restrizioni di registrazione. A tale scopo accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Dispositivi** > **Restrizioni registrazione** > **Crea restrizione**. Creare uno dei due tipi di restrizione. Verrà visualizzata la pagina **Tag di ambito**.

### <a name="shared-ipads-for-business--6367326---"></a>IPad condivisi per le aziende<!--6367326 -->
Sarà possibile usare Intune e Apple Business Manager per configurare in modo semplice e sicuro l'iPad condiviso, in modo che più dipendenti possano condividere i dispositivi. [iPad condiviso](https://developer.apple.com/education/shared-ipad/) di Apple offre un'esperienza personalizzata per più utenti, pur proteggendo i dati dei singoli utenti. Tramite un ID Apple gestito gli utenti possono accedere alle loro app, ai dati e alle impostazioni personali dopo aver eseguito l'accesso a qualsiasi iPad condiviso nell'organizzazione. iPad condiviso funziona con le identità federate.

Per visualizzare questa funzionalità passare all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Dispositivi** > **iOS** > **Registrazione di iOS** > **Token del programma di registrazione** > scegliere un token** > **Profili** > **Crea profilo** > **iOS**. Nella pagina **Impostazioni di gestione** selezionare **Registra senza affinità utente**. Verrà visualizzata l'opzione **iPad condiviso**.

**Si applica a:** macOS 13.4 e versioni successive. In questa versione è stato aggiunto il supporto per le sessioni temporanee con iPad condiviso, in modo che gli utenti possano accedere a un dispositivo senza un ID Apple gestito. Al momento della disconnessione, il dispositivo cancella tutti i dati dell'utente e torna a essere immediatamente pronto per l'uso, eliminando la necessità di una cancellazione del dispositivo stesso. 

<!-- ***********************************************-->
## <a name="device-management"></a>Gestione dei dispositivi

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>Supporto degli script di PowerShell per dispositivi BYOD<!-- 1862833  -->
Gli script di PowerShell supporteranno i dispositivi registrati con Azure AD in Intune. Per altre informazioni su PowerShell, vedere [Usare gli script di PowerShell nei dispositivi Windows 10 in Intune](../apps/intune-management-extension.md). Questa funzionalità non supporta i dispositivi che eseguono Windows 10 Home Edition.

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics includerà il log dei dettagli del dispositivo<!--6014987  -->
I log dei dettagli dei dispositivi di Intune saranno disponibili in **Report** > **Log Analytics**. È possibile correlare i dettagli dei dispositivi per creare query personalizzate e cartelle di lavoro di Azure.


### <a name="macos-script-support---6376978----"></a>Supporto degli script per macOS<!-- 6376978  -->
Il supporto degli script per macOS è ora disponibile a livello generale. Verrà aggiunto anche il supporto degli script assegnati dall'utente e dei dispositivi macOS registrati con Registrazione automatica del dispositivo di Apple (in precedenza Device Enrollment Program). Per altre informazioni, vedere [Usare gli script della shell nei dispositivi macOS in Intune](../apps/macos-shell-scripts.md).

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## <a name="monitor-and-troubleshoot"></a>Monitorare e risolvere i problemi

### <a name="power-bi-compliance-report-template-v20---636958----"></a>Modello di report di conformità Power BI V2.0<!-- 636958  -->
Gli amministratori potranno aggiornare il modello di report di conformità di Power BI da V1.0 a V2.0. V2.0 includerà una struttura migliorata e aggiornamenti ai calcoli e ai dati esposti come parte del modello. Per informazioni correlate, vedere [Connettersi al data warehouse con Power BI](../developer/reports-proc-get-a-link-powerbi.md).

<!-- ***********************************************-->
<!--
## Role-based access control
-->

<!-- ***********************************************-->
## <a name="security"></a>Sicurezza

### <a name="derived-credentials-support-for-disa-purebred-on-android-devices--4839592---"></a>Supporto di credenziali derivate per DISA Purebred nei dispositivi Android<!--4839592 -->
È possibile usare *DISA Purebread* come provider di [credenziali derivate](../protect/derived-credentials.md) nei dispositivi Android Enterprise completamente gestiti (**Amministrazione del tenant** > **Connettori e i token** > **Credenziali derivate**). Verrà incluso il supporto per il recupero di una credenziale derivata per DISA Purebred. Sarà possibile usare una credenziale derivata per l'autenticazione di app, Wi-Fi, VPN o la firma S/MIME e/o la crittografia, se supportata dalle app. 

In aprile Intune ha aggiunto il supporto per *Entrust Datacard* e *Intercede* come provider per le credenziali derivate. 

### <a name="privacy-preferences-settings-for-macos-devices---2934232---"></a>Impostazioni delle preferenze per la privacy per i dispositivi macOS<!-- 2934232 --> 
Nella versione di macOS Catalina 10.15 Apple ha aggiunto nuovi miglioramenti alla sicurezza e alla privacy. Per impostazione predefinita, le applicazioni e i processi non riescono ad accedere a dati specifici senza il consenso utente. Se gli utenti non forniscono il consenso, le applicazioni e i processi potrebbero non funzionare. In Intune verrà aggiunto il supporto per le impostazioni che permettono agli amministratori IT di accettare o rifiutare il consenso per l'accesso ai dati per conto degli utenti finali nei dispositivi che eseguono macOS 10.14 e versioni successive. Queste impostazioni garantiscono che le applicazioni e i processi continuino a funzionare correttamente e riducono il numero di richieste visualizzate dagli utenti finali.


### <a name="duplicate-your-policies-in-endpoint-security---5892558-----"></a>Duplicare i criteri in Endpoint Security<!-- 5892558   -->
Sarà possibile selezionare un criterio creato nel nodo Endpoint Security dell'interfaccia di amministrazione di Microsoft Endpoint Manager e quindi duplicarlo per creare una copia.  I criteri che è possibile duplicare includono quelli creati per: 

- Antivirus
- Crittografia del disco
- Firewall
- Rilevamento di endpoint e risposta
- Riduzione della superficie di attacco
- Protezione account

La duplicazione creerà una copia del criterio originale, che potrà quindi essere rinominato e modificato. La copia non includerà le assegnazioni dell'originale.

### <a name="send-push-notifications-as-an-action-for-non-compliance----1733150-----"></a>Inviare notifiche push come azione per la mancata conformità <!-- 1733150   -->
Per le piattaforme iOS e Android, verrà aggiunta una nuova azione per la mancata conformità, che invierà una notifica push dell'app tramite l'app Portale aziendale. Gli utenti potranno fare clic sulle notifiche e verrà avviata l'app Portale aziendale, in cui verrà indicato il motivo della non conformità. Gli amministratori potranno configurare questa nuova azione per la mancata conformità nell'interfaccia di amministrazione di Microsoft Endpoint Manager passando a **Dispositivi** > **Criteri di conformità** > **Crea criterio** e quindi selezionando *Azione* per inviare una notifica push dell'app. 

### <a name="new-profile-for-endpoint-security-firewall-policy---5653324-----"></a>Nuovo profilo per il criterio firewall di Endpoint Security<!-- 5653324   -->
Come anteprima, viene introdotto un profilo aggiuntivo per Windows 10 e versioni successive al criterio Firewall in Endpoint Security di Intune (**Endpoint Security** > **Firewall** > **Crea criterio** > selezionare **Windows 10 e versioni successive**). 

Ogni istanza di questo nuovo profilo supporta fino a 150 *regole Microsoft Defender Firewall* personalizzate. Il profilo delle regole Microsoft Defender Firewall consente di definire regole di Windows Firewall granulari, per autorizzare o bloccare le porte e le applicazioni in Windows 10.

<!-- ***********************************************-->
## <a name="notices"></a>Notifiche

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Vedere anche

Per informazioni dettagliate sugli ultimi sviluppi, vedere [Novità di Microsoft Intune](whats-new.md).



