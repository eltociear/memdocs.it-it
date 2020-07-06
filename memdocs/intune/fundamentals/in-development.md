---
title: In fase di sviluppo - Microsoft Intune
titleSuffix: ''
description: Funzionalità di Microsoft Intune in fase di sviluppo
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/26/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 14b571c069fd2484e7e3fd5f2841f6e5884ecc80
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/27/2020
ms.locfileid: "85502681"
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

### <a name="update-to-device-icons-in-company-portal-and-intune-apps-on-android---6057023----"></a>Aggiornamento alle icone del dispositivo nel Portale aziendale e nelle app di Intune in Android<!-- 6057023  -->
Viene eseguito un aggiornamento delle icone del dispositivo nel Portale aziendale e nelle app di Intune nei dispositivi Android per creare un aspetto più moderno e in linea con Microsoft Fluent Design System. Per informazioni correlate, vedere [Aggiornamento delle icone nell'app Portale aziendale per iOS/iPadOS e macOS](../fundamentals/whats-new-app-ui.md#update-to-icons-in-company-portal-app-for-iosipados-and-macos-). 

### <a name="smime-for-outlook-on-ios-and-android-enterprise-devices-managed-without-enrollment---6517155----"></a>S/MIME per Outlook nei dispositivi iOS e Android Enterprise gestiti senza registrazione<!-- 6517155  -->
Sarà possibile abilitare S/MIME per Outlook nei dispositivi iOS e Android Enterprise usando i criteri di configurazione delle app per i dispositivi gestiti senza registrazione. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) selezionare **App** > **Criteri di configurazione dell'app** > **Aggiungi** > **Dispositivi gestiti**. Inoltre, è possibile scegliere se consentire agli utenti di modificare questa impostazione in Outlook. Per altre informazioni sulle impostazioni di configurazione di Outlook, vedere [Impostazioni di configurazione di Microsoft Outlook](../apps/app-configuration-policies-outlook.md).

### <a name="ios-company-portal-will-support-apples-automated-device-enrollment-without-user-affinity---7282707----"></a>Il Portale aziendale per iOS supporterà la registrazione automatica dei dispositivi di Apple senza affinità utente<!-- 7282707  --> 
Il Portale aziendale per iOS sarà supportato nei dispositivi registrati con la registrazione automatica dei dispositivi di Apple senza richiedere un utente assegnato. L'utente finale può accedere al Portale aziendale per iOS per specificarsi come utente primario in un dispositivo iOS/iPadOS registrato senza affinità dispositivo. Per altre informazioni sulla registrazione automatica dei dispositivi, vedere [Registrare automaticamente i dispositivi iOS/iPadOS con Registrazione automatica del dispositivo di Apple](../enrollment/device-enrollment-program-enroll-ios.md).

### <a name="win32-app-installation-notifications-and-the-company-portal---7485945----"></a>Notifiche di installazione dell'app Win32 e Portale aziendale<!-- 7485945  -->
Gli utenti finali potranno decidere se le applicazioni visualizzate nel [portale aziendale Web di Microsoft Intune](https://portal.manage.microsoft.com/) devono essere aperte dall'app Portale aziendale o dal portale aziendale Web. Questa opzione è disponibile solo se l'utente finale ha installato l'app Portale aziendale e avvia un'applicazione del portale aziendale Web all'esterno di un browser.

### <a name="the-company-portal-adds-configuration-manager-application-support---4297660---"></a>Il Portale aziendale aggiunge il supporto delle applicazioni di Configuration Manager<!-- 4297660 -->
Il Portale aziendale supporta ora le applicazioni di Configuration Manager. Questa funzionalità consente agli utenti finali di visualizzare le applicazioni distribuite di Configuration Manager e Intune nel Portale aziendale per i clienti co-gestiti. Questo supporto consente agli amministratori di consolidare le diverse esperienze del portale per gli utenti finali. Per altre informazioni, vedere [Usare l'app Portale aziendale in dispositivi con co-gestione](https://docs.microsoft.com/mem/configmgr/core/get-started/2020/technical-preview-2006#bkmk_portal).

<!-- ***********************************************-->
## <a name="device-configuration"></a>Configurazione del dispositivo

### <a name="set-device-compliance-state-from-third-party-mdm-partners---6361689-----"></a>Impostare lo stato di conformità del dispositivo da partner MDM di terze parti<!-- 6361689   -->
I clienti di Microsoft 365 proprietari di soluzioni MDM di terze parti saranno in grado di applicare criteri di accesso condizionale per le app Microsoft 365 in iOS e Android tramite l'integrazione del servizio Conformità del dispositivo di Microsoft Intune. Il fornitore di MDM di terze parti potrà usare il servizio Conformità del dispositivo di Intune per inviare i dati di conformità del dispositivo a Intune. Intune li valuterà quindi per determinare se il dispositivo è attendibile e impostare gli attributi di accesso condizionale in Azure AD.  Ai clienti verrà richiesto di impostare criteri di accesso condizionale di Azure AD dall'interfaccia di amministrazione di Microsoft Endpoint Manager o dal portale di Azure AD.  


### <a name="new-vpn-settings-for-windows-10-and-newer-devices---6602122----"></a>Nuove impostazioni della VPN per Windows 10 e dispositivi più recenti<!-- 6602122  -->
Quando si crea un profilo VPN usando il tipo di connessione IKEv2 sono disponibili nuove impostazioni che è possibile configurare (**Dispositivi** > **Profili di configurazione** > **Crea profilo** > **Windows 10 e versioni successive** per la piattaforma > **VPN** per il profilo > **VPN di base**):

- **Tunnel del dispositivo**: consente ai dispositivi di connettersi automaticamente alla VPN senza richiedere alcuna interazione con l'utente, compreso l'accesso dell'utente. Questa funzionalità richiede l'abilitazione di **Always On** e l'uso dei **Certificati della macchina** come metodo di autenticazione.
- Impostazioni di Cryptography Suite: configurare gli algoritmi usati per proteggere le associazioni IKE e di sicurezza figlio, che consentono di associare le impostazioni client e server.

Per visualizzare le impostazioni che è possibile configurare, passare a [Impostazioni del dispositivo Windows per aggiungere connessioni VPN con Intune](../configuration/vpn-settings-windows-10.md).

Si applica a:
- Windows 10 e versioni successive

### <a name="new-features-for-managed-home-screen-on-android-enterprise-device-owner-dedicated-devices-cosu---7414175-7133328-7133720-7134873-7135184----"></a>Nuove funzionalità per la schermata iniziale gestita nei dispositivi dedicati del proprietario del dispositivo Android Enterprise (COSU)<!-- 7414175 7133328 7133720 7134873 7135184  -->
Nei dispositivi Android Enterprise gli amministratori potranno usare i profili di configurazione dei dispositivi per personalizzare la schermata iniziale gestita nei dispositivi dedicati usando la modalità tutto schermo per più app (**Dispositivi** > **Profili di configurazione** > **Crea profilo** > **Android Enterprise** per la piattaforma > **Solo proprietario del dispositivo** > **Limitazioni del dispositivo** per il profilo > **Esperienza del dispositivo**).

In particolare, è possibile:

- Personalizzare le icone, modificare l'orientamento dello schermo e visualizzare le notifiche dell'app sulle icone badge <!--7414175-->
- Nascondere il punto di ingresso delle impostazioni gestite <!--7133328-->
- Accedere più facilmente al menu di debug <!--7133720-->
- Creare un elenco di reti Wi-Fi consentite <!-- 7134873-->
- Accedere più facilmente alle informazioni sul dispositivo <!-- 7135184-->

Per altre informazioni, vedere [Impostazioni dei dispositivi Android Enterprise per consentire o limitare l'uso delle funzionalità](../configuration/device-restrictions-android-for-work.md).

Si applica a:

- Dispositivi dedicati del proprietario del dispositivo Android Enterprise (COSU)

<!-- ***********************************************-->
## <a name="device-enrollment"></a>Registrazione del dispositivo

### <a name="corporate-owned-personally-enabled-devices-preview--4442275---"></a>Dispositivi di proprietà dell'azienda abilitati personalmente (anteprima)<!--4442275 -->
Intune supporterà i dispositivi di proprietà dell'azienda Android Enterprise con un profilo di lavoro per le versioni del sistema operativo Android 8 e versioni successive. I dispositivi di proprietà dell'azienda con un profilo di lavoro sono uno degli scenari di gestione aziendale del set di soluzioni Android Enterprise. Questo scenario è per i dispositivi a utente singolo destinati all'uso personale e aziendale. Questo scenario per dispositivi di proprietà dell'azienda abilitati personalmente (COPE) offre:

- containerizzazione dei profili di lavoro e personali
- controllo a livello di dispositivo per gli amministratori
- garanzia per gli utenti finali che i dati e le applicazioni personali rimarranno privati

La prima versione di anteprima pubblica conterrà un subset delle funzionalità che verranno incluse nella versione disponibile a livello generale. Altre funzionalità verranno aggiunte progressivamente. Le funzionalità che saranno disponibili nella prima anteprima includono:

- Registrazione: gli amministratori possono creare più profili di registrazione con token univoci senza scadenza. La registrazione del dispositivo può essere eseguita tramite NFC, immissione di token, codice a matrice, Zero Touch o Knox Mobile Enrollment.
- Configurazione del dispositivo: subset delle impostazioni dei dispositivi completamente gestiti e dedicati esistenti.
- Conformità del dispositivo: criteri di conformità attualmente disponibili per i dispositivi completamente gestiti.
- Azioni del dispositivo: eliminazione del dispositivo (ripristino delle impostazioni predefinite), riavvio del dispositivo e blocco del dispositivo.  
- Gestione delle app: assegnazioni di app, configurazione delle app e funzionalità di creazione di report associate 
- Accesso condizionale



<!-- ***********************************************-->
## <a name="device-management"></a>Gestione dei dispositivi

### <a name="device-compliance-logs-now-in-english--6014904---"></a>Log di conformità del dispositivo ora in inglese<!--6014904 -->
I log IntuneDeviceComplianceOrg hanno solo enumerazioni per ComplianceState, OwnerType e DeviceHealthThreatLevel. In un aggiornamento futuro questi log avranno informazioni in lingua inglese nelle colonne.

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>Supporto degli script di PowerShell per dispositivi BYOD<!-- 1862833  -->
Gli script di PowerShell supporteranno i dispositivi registrati con Azure AD in Intune. Per altre informazioni su PowerShell, vedere [Usare gli script di PowerShell nei dispositivi Windows 10 in Intune](../apps/intune-management-extension.md). Questa funzionalità non supporta i dispositivi che eseguono Windows 10 Home Edition.

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics includerà il log dei dettagli del dispositivo<!--6014987  -->
I log dei dettagli dei dispositivi di Intune saranno disponibili in **Report** > **Log Analytics**. È possibile correlare i dettagli dei dispositivi per creare query personalizzate e cartelle di lavoro di Azure.

### <a name="tenant-attach-device-timeline-in-the-admin-center--7220536-cm7141381---"></a>Collegamento di tenant: sequenza temporale dispositivo nell'interfaccia di amministrazione<!--7220536, CM7141381 -->
Quando Configuration Manager sincronizza un dispositivo con Microsoft Endpoint Manager tramite il collegamento al tenant, è possibile visualizzare una sequenza temporale degli eventi. Questa sequenza temporale mostra le attività precedenti eseguite sul dispositivo che possono risultare utili per la risoluzione dei problemi. Per altre informazioni, vedere [Configuration Manager technical preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_timeline).  

### <a name="tenant-attach-install-an-application-from-the-admin-center---7220536-cm6024389---"></a>Collegamento di tenant: installare un'applicazione dall'interfaccia di amministrazione<!-- 7220536, CM6024389 -->
Sarà possibile avviare l'installazione di un'applicazione in tempo reale per un dispositivo collegato al tenant dall'interfaccia di amministrazione di Microsoft Endpoint Management. Per altre informazioni, vedere [Configuration Manager technical preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_apps).

### <a name="tenant-attach-cmpivot-from-the-admin-center--7220536-cm6024392---"></a>Collegamento di tenant: CMPivot dall'interfaccia di amministrazione<!--7220536, CM6024392 -->
Sarà possibile sfruttare la potenza di [CMPivot](../../configmgr/tenant-attach/cmpivot-overview-attached.md) nell'interfaccia di amministrazione di Microsoft Endpoint Manager. Altri utenti tipo, ad esempio il personale del supporto tecnico, possono avviare query in tempo reale dal cloud su un singolo dispositivo gestito da ConfigMgr e restituire i risultati all'interfaccia di amministrazione. In questo modo è possibile usufruire di tutti i vantaggi tradizionali di CMPivot, che consente agli amministratori IT e ad altri utenti designati di valutare rapidamente lo stato dei dispositivi nel proprio ambiente e di intervenire di conseguenza. Per altre informazioni, vedere [Configuration Manager technical preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_cmpivot). 

### <a name="tenant-attach-run-scripts-from-the-admin-center--7220536-cm6234688---"></a>Collegamento di tenant: eseguire script dall'interfaccia di amministrazione<!--7220536, CM6234688 -->
Sarà possibile sfruttare la potenza della funzionalità locale di Configuration Manager per [l'esecuzione di script](../../configmgr/apps/deploy-use/create-deploy-scripts.md) nell'interfaccia di amministrazione di Microsoft Endpoint Manager. Altri utenti tipo, ad esempio il personale del supporto tecnico, possono eseguire script di PowerShell dal cloud su un singolo dispositivo gestito di Configuration Manager. In questo modo è possibile usufruire di tutti i vantaggi tradizionali degli script di PowerShell che sono già stati definiti e approvati dall'amministratore di Configuration Manager nel nuovo ambiente. Per altre informazioni, vedere [Configuration Manager technical preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_scripts). 

### <a name="new-merge-logic-for-windows-10-devices--179048--"></a>Nuova logica di merge per dispositivi Windows 10<!--179048-->
Attualmente, se un cliente ricrea un'immagine di un dispositivo e lo registra nuovamente, nella console di amministrazione di Microsoft Endpoint Manager verranno visualizzati più record per il dispositivo. È in fase di sviluppo una nuova logica di unione per unire tali record duplicati per i dispositivi Windows 10.

### <a name="updates-to-the-remote-lock-action-for-macos-devices--7032805---"></a>Aggiornamenti dell'azione di blocco remoto per i dispositivi macOS<!--7032805 -->
Gli aggiornamenti all'azione di blocco remoto per i dispositivi macOS includono:
- Il PIN di ripristino verrà visualizzato per 30 giorni prima dell'eliminazione (anziché sette giorni).
- Se un amministratore ha un secondo browser aperto e tenta di attivare di nuovo il comando da una scheda o un browser diverso, Intune consentirà l'esecuzione del comando. Tuttavia, lo stato dei report verrà impostato su Non riuscito anziché generare un nuovo PIN.
- L'amministratore non potrà eseguire un altro comando di blocco remoto se il comando precedente è ancora in sospeso o se il dispositivo non è stato nuovamente verificato.
Queste modifiche sono progettate per impedire la sovrascrittura del PIN corretto dopo più comandi di blocco remoto.

### <a name="deploy-software-updates-to-macos-devices----3194876---"></a>Distribuire gli aggiornamenti software nei dispositivi macOS <!-- 3194876 -->
Sarà possibile distribuire gli aggiornamenti software a gruppi di dispositivi macOS. Questa funzionalità include aggiornamenti critici, firmware, file di configurazione e altri aggiornamenti. Sarà possibile inviare aggiornamenti alla successiva sincronizzazione del dispositivo oppure selezionare una pianificazione settimanale per distribuire gli aggiornamenti entro o al di fuori degli intervalli di tempo impostati. Ciò può risultare utile quando si vuole aggiornare i dispositivi al di fuori delle ore di lavoro standard o quando l'help desk occupa tutto il personale. Si otterrà anche un report dettagliato di tutti i dispositivi macOS a cui sono stati distribuiti gli aggiornamenti. È possibile esaminare il report per ogni singolo dispositivo per visualizzare lo stato di specifici aggiornamenti.

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## <a name="monitor-and-troubleshoot"></a>Monitorare e risolvere i problemi

### <a name="additional-data-warehouse-v10-properties---6125732-----"></a>Proprietà di Data Warehouse v1.0 aggiuntive<!-- 6125732   -->
È possibile accedere alle proprietà aggiuntive usando il data warehouse di Intune v1.0. Le proprietà seguenti vengono ora esposte attraverso l'entità [devices](../developer/reports-ref-devices.md#devices):
- `ethernetMacAddress`: identificatore di rete univoco del dispositivo.
- `office365Version`: versione di Office 365 installata nel dispositivo.

Le proprietà seguenti vengono ora esposte attraverso l'entità [devicePropertyHistories](../developer/reports-ref-devices.md#devicepropertyhistories):
- `physicalMemoryInBytes`: memoria fisica in byte.
- `totalStorageSpaceInBytes`: capacità di archiviazione totale in byte.

Per altre informazioni, vedere [API Data Warehouse di Microsoft Intune](../developer/reports-nav-intune-data-warehouse.md).

### <a name="power-bi-compliance-report-template-v20---636958----"></a>Modello di report di conformità Power BI V2.0<!-- 636958  -->
Gli amministratori potranno aggiornare il modello di report di conformità di Power BI da V1.0 a V2.0. V2.0 includerà una struttura migliorata e modifiche ai calcoli e ai dati esposti come parte del modello. Per informazioni correlate, vedere [Connettersi al data warehouse con Power BI](../developer/reports-proc-get-a-link-powerbi.md).

<!-- ***********************************************-->
## <a name="role-based-access-control"></a>Controllo di accesso in base ai ruoli

### <a name="scope-tag-support-for-customization-policies--6182440---"></a>Supporto dei tag di ambito per i criteri di personalizzazione<!--6182440 -->
Sarà possibile assegnare tag di ambito ai criteri di personalizzazione. A tale scopo, passare all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Amministrazione del tenant**> **Personalizzazione** dove verranno visualizzate le opzioni di configurazione **Tag di ambito**.

### <a name="assign-profile-and-update-profile-permission-changes--7177586---"></a>Modifiche delle autorizzazioni Assegna profilo e Aggiorna profilo<!--7177586 -->
Le autorizzazioni di controllo degli accessi in base al ruolo verranno modificate per Assegna profilo e Aggiorna profilo:
- Assegna profilo: gli amministratori con questa autorizzazione potranno anche assegnare i profili ai token e assegnare un profilo predefinito a un token.
- Aggiorna profilo: gli amministratori con questa autorizzazione potranno aggiornare solo i profili esistenti.

<!-- ***********************************************-->
## <a name="security"></a>Sicurezza

### <a name="app-protection-policy-support-for-symantec-endpoint-security-and-check-point-sandblast----4452423-4731168---"></a>Supporto dei criteri di protezione delle app per Symantec Endpoint Security e Check Point Sandblast<!--  4452423, 4731168 -->

Nell'ottobre 2019 i criteri di protezione delle app di Intune hanno aggiunto la capacità per usare i dati di alcuni dei partner MTD (Microsoft Threat Defense). Verrà aggiunto il supporto per i partner seguenti per usare un criterio di protezione delle app per bloccare o cancellare in modo selettivo i dati aziendali dell'utente in base all'integrità di un dispositivo:

- **Check Point Sandblast** in Android, iOS e iPadOS
- **Symantec Endpoint Security** in Android, iOS e iPadOS

Per informazioni sull'uso dei criteri di protezione delle app con i partner MTD, vedere [Creare criteri di protezione delle app Mobile Threat Defense con Intune](../protect/mtd-app-protection-policy.md).

### <a name="store-the-recovery-key-for-a-macos-device-that-was-encrypted-with-filevault-before-enrolling-with-intune--5239424-----"></a>Archiviare la chiave di ripristino per un dispositivo macOS crittografato con FileVault prima della registrazione con Intune<!--5239424   -->
A breve, gli utenti finali di un dispositivo macOS che non è stato crittografato con i criteri FileVault da Intune o è stato crittografato prima di essere registrato con Intune, non dovranno decrittografare il dispositivo in modo che possa essere crittografato nuovamente da Intune. Al contrario, la crittografia corrente può rimanere attiva e l'utente può accedere al sito Web del portale aziendale dove è possibile scegliere *Archivia la chiave di ripristino* per inviare la propria chiave di ripristino personale per il dispositivo macOS crittografato. Quando si invia una chiave valida, Intune ruota la chiave personale per generare una nuova chiave che rimane disponibile per l'utente nel sito Web del portale aziendale, nel portale aziendale iOS/, nel portale aziendale Android o nell'app Intune. Gli utenti possono quindi accedere a queste posizioni da qualsiasi dispositivo per visualizzare la chiave nel caso in cui vengano bloccati dal dispositivo macOS.

### <a name="hide-the-personal-recovery-key-from-a-device-user-during-macos-filevault-disk-encryption----5475632----"></a>Nascondere la chiave di ripristino personale da un utente del dispositivo durante la crittografia del disco FileVault di macOS<!--  5475632  -->
Verrà aggiunta una nuova impostazione denominata *Nascondi la chiave di ripristino* ai criteri di crittografia del disco di sicurezza dell'endpoint per FileVault (**Sicurezza degli endpoint** > **Crittografia del disco** > **Crea profilo** > **macOS** > **FileVault**). Quando si abilita la nuova impostazione, Intune nasconde la chiave di ripristino personale dell'utente del dispositivo macOS durante la crittografia. Nascondendo la chiave sarà possibile proteggerla poiché gli utenti non potranno annotarla in attesa della crittografia del dispositivo. Se invece è necessario il ripristino, l'utente può sempre usare qualsiasi dispositivo per visualizzare la chiave di ripristino personale tramite il sito Web del Portale aziendale Intune.

### <a name="improved-view-of-security-baseline-details-for-devices---5536846-----"></a>Visualizzazione migliorata dei dettagli della baseline di sicurezza per i dispositivi<!-- 5536846   -->
Stiamo lavorando per migliorare la visualizzazione dei dettagli delle impostazioni della baseline di sicurezza quando si analizzano i dettagli di un dispositivo (**Sicurezza degli endpoint** > **Dispositivi**).  Per ogni baseline di sicurezza assegnata, sarà possibile visualizzare un elenco semplice di dettagli per ogni impostazione che include le categorie di impostazioni, i nomi delle impostazioni e lo stato di ogni impostazione nel dispositivo.

### <a name="manage-source-locations-for-definition-updates-with-endpoint-security-antivirus-policy-for-windows-10-devices---6347801----"></a>Gestire i percorsi di origine per gli aggiornamenti delle definizioni con i criteri antivirus di sicurezza degli endpoint per i dispositivi Windows 10<!-- 6347801  -->  
Verranno aggiunte due nuove impostazioni alla categoria *Aggiornamenti* dei criteri antivirus di sicurezza degli endpoint per i dispositivi Windows 10 che consentono di gestire il modo in cui i dispositivi ottengono le definizioni degli aggiornamenti (**Sicurezza degli endpoint** > ** Antivirus** > **Crea criterio** > **Windows 10 e versioni successive** > **Microsoft Defender Antivirus**).

Con le nuove impostazioni, sarà possibile aggiungere condivisioni file UNC come percorsi di origine dei download per gli aggiornamenti delle definizioni e definire l'ordine in cui vengono contattati i percorsi di origine diversi. Le nuove impostazioni gestiranno i seguenti provider di servizi di configurazione Defender:

- [signatureupdatefilesharessources](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-signatureupdatefilesharessources)
- [signatureupdatefallbackorder](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-signatureupdatefallbackorder)

### <a name="endpoint-detection-and-response-policy-for-onboarding-tenant-attached-devices-to-mdatp-is-moving-out-of-preview---7303816-----"></a>I criteri di rilevamento di endpoint e riposta per l'onboarding dei dispositivi con collegamento di tenant in MDATP non sono più in versione di anteprima<!-- 7303816   -->
Come parte della sicurezza degli endpoint in Intune, il supporto dei criteri di rilevamento di endpoint e riposta (EDR) da usare con i dispositivi gestiti da Configuration Manager non saranno più in versione di anteprima e diventeranno disponibili a livello generale (**Sicurezza degli endpoint** > **Rilevamento di endpoint e risposta** > **Crea criterio** > **Windows 10 e Windows Server**). Quando si configura il [collegamento di tenant per Configuration Manager](../../configmgr/tenant-attach/device-sync-actions.md), è possibile usare i criteri EDR per eseguire l'onboarding dei dispositivi gestiti da Configuration Manager in Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP). 

### <a name="improvements-for-the-security-baselines-node---7433136-----"></a>Miglioramenti del nodo delle baseline di sicurezza<!-- 7433136   -->
Per migliorare l'usabilità del nodo della baseline di sicurezza nell'interfaccia di amministrazione di Microsoft Endpoint Manager, verrà rimossa la scheda *Panoramica* per ogni baseline e verrà aprirà la scheda **Profilo** delle baseline (**Sicurezza degli endpoint** > **Baseline di sicurezza** > *baseline*).

La pagina *Panoramica* per ogni baseline visualizza i grafici e i riquadri che aggregano i risultati dell'ultima versione della baseline distribuita. Queste informazioni vengono duplicate rispetto a quanto visualizzato se si espande una versione per altri dettagli. Dopo aver rimosso la pagina *Panoramica*, i grafici e i dettagli di aggregazione rimarranno disponibili quando si espande direttamente la versione.  

### <a name="firewall-rule-migration-tool-preview---6423187----"></a>Anteprima dello strumento di migrazione delle regole del firewall<!-- 6423187  -->
Come anteprima pubblica, stiamo lavorando a uno strumento basato su PowerShell che eseguirà la migrazione delle regole di Windows Defender Firewall. Quando si installa e si esegue lo strumento, vengono creati automaticamente i criteri di regola del firewall della sicurezza degli endpoint per Intune basati sulla configurazione corrente di un client Windows 10.

### <a name="new-settings-for-the-device-control-profile-in-endpoint-security-attack-surface-reduction-policy--7032084---"></a>Nuove impostazioni per il profilo di controllo del dispositivo nei criteri di riduzione della superficie di attacco per la sicurezza degli endpoint<!--7032084 -->
Verranno aggiunte diverse impostazioni per i dispositivi Windows 10 al profilo di controllo del dispositivo per i criteri di riduzione della superficie di attacco per la sicurezza degli endpoint (**Sicurezza degli endpoint** > **Riduzione della superficie di attacco** > **Crea criterio** > **Windows 10 e versioni successive** > **Controllo del dispositivo**). 

Le nuove impostazioni corrisponderanno a quelle attualmente disponibili nei [profili Limitazioni del dispositivo](../configuration/device-restrictions-windows-10.md) per *Configurazione del dispositivo*. Le impostazioni da aggiungere al profilo *Controllo del dispositivo* devono includere diverse impostazioni Bluetooth.  


<!-- ***********************************************-->
## <a name="notices"></a>Notifiche

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Vedere anche

Per informazioni dettagliate sugli ultimi sviluppi, vedere [Novità di Microsoft Intune](whats-new.md).
