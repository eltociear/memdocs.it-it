---
title: Novità della versione 2006
titleSuffix: Configuration Manager
description: Informazioni dettagliate sulle modifiche e sulle nuove funzionalità introdotte nella versione 2006 di Configuration Manager Current Branch.
ms.date: 09/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4b071746-61e1-404b-8053-60978de028a7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7e67773c359291db3c537ac0ed8fe6ce6fbcfc1f
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/09/2020
ms.locfileid: "89607648"
---
# <a name="whats-new-in-version-2006-of-configuration-manager-current-branch"></a>Novità della versione 2006 di Configuration Manager Current Branch

*Si applica a: Configuration Manager (Current Branch)*

L'aggiornamento 2006 per Configuration Manager Current Branch è disponibile come aggiornamento nella console. Applicare questo aggiornamento ai siti con la versione 1810 o successiva. <!-- baseline only statement:When installing a new site, it's also available as a baseline version. -->Questo articolo offre un riepilogo delle modifiche e delle nuove funzionalità di Configuration Manager versione 2006.

Esaminare sempre l'elenco di controllo più recente per installare questo aggiornamento. Per altre informazioni, vedere [Elenco di controllo per l'installazione dell'aggiornamento 2006](../../servers/manage/checklist-for-installing-update-2006.md). Dopo aver aggiornato un sito, vedere anche [Elenco di controllo post-aggiornamento](../../servers/manage/checklist-for-installing-update-2006.md#post-update-checklist).

Per sfruttare i vantaggi delle nuove funzionalità di Configuration Manager, dopo l'aggiornamento del sito aggiornare anche i client alla versione più recente. Anche se le nuove funzionalità vengono visualizzate nella console di Configuration Manager quando si esegue l'aggiornamento del sito e della console, lo scenario completo risulta funzionante solo dopo l'aggiornamento alla versione più recente del client.

> [!TIP]
> Per ricevere una notifica quando questa pagina viene aggiornata, copiare e incollare l'URL seguente nel lettore di feed RSS: `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+2006+-+Configuration+Manager%22&locale=en-us`

## <a name="microsoft-endpoint-manager-tenant-attach"></a><a name="bkmk_tenant"></a> Collegamento del tenant di Microsoft Endpoint Manager

### <a name="device-timeline-in-the-admin-center"></a><a name="bkmk_timeline"></a> Sequenza temporale dispositivo nell'interfaccia di amministrazione
<!--7220536, CM7141381-->
Quando Configuration Manager sincronizza un dispositivo con Microsoft Endpoint Manager tramite il collegamento al tenant, è possibile visualizzare una sequenza temporale degli eventi. Questa sequenza temporale mostra le attività precedenti eseguite sul dispositivo che possono risultare utili per la risoluzione dei problemi. Per altre informazioni, vedere [Sequenza temporale dispositivo nell'interfaccia di amministrazione](../../../tenant-attach/timeline.md).

### <a name="resource-explorer-in-the-admin-center"></a><a name="bkmk_hinv"></a> Esplora inventario risorse nell'interfaccia di amministrazione
<!--6479284-->
Dall'interfaccia di amministrazione di Microsoft Endpoint Management è possibile visualizzare l'inventario hardware per i dispositivi Configuration Manager caricati usando Esplora inventario risorse. Per altre informazioni, vedere [Collegamento di tenant: Esplora inventario risorse nell'interfaccia di amministrazione](../../../tenant-attach/resource-explorer.md).

### <a name="cmpivot-from-the-admin-center"></a><a name="bkmk_cmpivot"></a> CMPivot dall'interfaccia di amministrazione
<!--6024392-->
La potenza di CMPivot ora disponibile nell'interfaccia di amministrazione di Microsoft Endpoint Manager. Altri utenti tipo, ad esempio il personale del supporto tecnico, possono avviare query in tempo reale dal cloud su un singolo dispositivo gestito da ConfigMgr e restituire i risultati all'interfaccia di amministrazione. In questo modo è possibile usufruire di tutti i vantaggi tradizionali di CMPivot, che consente agli amministratori IT e ad altri utenti designati di valutare rapidamente lo stato dei dispositivi nel proprio ambiente e di intervenire di conseguenza.

Per altre informazioni su CMPivot dall'interfaccia di amministrazione, vedere [Prerequisiti di CMPivot](../../../tenant-attach/cmpivot-start.md), [Panoramica di CMPivot](../../../tenant-attach/cmpivot-overview-attached.md) e [Script di esempio CMPivot](../../../tenant-attach/cmpivot-samples-attached.md).

### <a name="tenant-attach-microsoft-defender-antivirus-policies-in-the-microsoft-endpoint-manager-admin-center"></a><a name="bkmk_atp"></a> Collegamento di tenant: Criteri di Microsoft Defender Antivirus nell'interfaccia di amministrazione di Microsoft Endpoint Manager
<!--4812909-->
È ora possibile creare i criteri per Microsoft Defender Antivirus nella console di Microsoft Endpoint Manager e distribuirli in raccolte di Configuration Manager. Per altre informazioni, tra cui istruzioni dettagliate e impostazioni disponibili, vedere gli articoli seguenti:
- [Collegamento di tenant: Eseguire l'onboarding di client di Configuration Manager in Microsoft Defender ATP tramite l'interfaccia di amministrazione (anteprima)](../../../tenant-attach/atp-onboard.md)
- [Collegamento di tenant: Distribuire i criteri antivirus di sicurezza degli endpoint dall'interfaccia di amministrazione (anteprima)](../../../tenant-attach/deploy-antivirus-policy.md)
- [Impostazioni per i criteri di Microsoft Defender Antivirus per i dispositivi collegati ai tenant in Microsoft Intune](../../../../intune/protect/antivirus-microsoft-defender-settings-windows-tenant-attach.md?toc=/mem/configmgr/tenant-attach/toc.json&bc=/mem/configmgr/tenant-attach/breadcrumb/toc.json).

### <a name="install-applications-from-the-admin-center"></a>Installare applicazioni dall'interfaccia di amministrazione
<!--7518897, 6024389-->
È possibile avviare l'installazione di un'applicazione in tempo reale per un dispositivo collegato al tenant dall'interfaccia di amministrazione di Microsoft Endpoint Manager. A partire dalla versione 2006 di Configuration Manager, l'elenco di applicazioni disponibili per il dispositivo include anche le applicazioni distribuite all'utente attualmente connesso al dispositivo. Per altre informazioni, vedere [Collegamento di tenant: installare un'applicazione dall'interfaccia di amministrazione](../../../tenant-attach/applications.md).  

### <a name="import-previously-created-azure-ad-application-during-tenant-attach-onboarding"></a> Importare un'applicazione di Azure AD creata in precedenza durante l'onboarding del collegamento al tenant
<!--6479246-->
Durante un nuovo onboarding, un amministratore può specificare un'applicazione creata in precedenza durante l'onboarding nel collegamento al tenant. Per altre informazioni, vedere [Collegamento del tenant di Microsoft Endpoint Manager: sincronizzazione e azioni dei dispositivi](../../../tenant-attach/device-sync-actions.md#bkmk_aad_app).

## <a name="endpoint-analytics"></a><a name="bkmk_ea"></a> Analisi degli endpoint

### <a name="endpoint-analytics-data-collection-enabled-by-default"></a>Raccolta dati di Analisi degli endpoint abilitata per impostazione predefinita
<!--7065447, 7741111-->
L'impostazione client **Abilita raccolta dati di Analisi degli endpoint** è ora abilitata per impostazione predefinita. Questa impostazione consente agli endpoint gestiti di inviare dati, ad esempio informazioni dettagliate sulle prestazioni di avvio, al server del sito di Configuration Manager. Questa modifica ha effetto solo sulla raccolta di dati locali. I dati di Analisi degli endpoint non vengono caricati nell'interfaccia di amministrazione di Microsoft Endpoint Manager fino a quando non si [abilita il caricamento dei dati in Configuration Manager](../../../../analytics/enroll-configmgr.md#bkmk_cm_upload). Il nuovo valore predefinito si applica alle impostazioni client predefinite e alle impostazioni client personalizzate create dopo l'aggiornamento alla versione 2006.

- Se si sta eseguendo l'aggiornamento dalla versione 2002 alla versione 2006, vengono conservati i valori delle impostazioni client personalizzate esistenti. Il valore predefinito di **Abilita raccolta dati di Analisi degli endpoint** in Configuration Manager versione 2002 è **No**.
- Se si esegue l'aggiornamento alla versione 2006 da Configuration Manager versione 1910 o precedenti, le impostazioni client personalizzate preesistenti che contengono il gruppo di impostazioni **Agente computer** ereditano il nuovo valore predefinito **Sì** per **Abilita raccolta dati di Analisi degli endpoint**.

Per altre informazioni, vedere [Configure Endpoint analytics data collection in Configuration Manager](../../../../analytics/enroll-configmgr.md#bkmk_cm_upload) (Configurare la raccolta dati di Analisi degli endpoint in Configuration Manager).

## <a name="site-infrastructure"></a><a name="bkmk_infra"></a> Infrastruttura del sito

### <a name="vpn-boundary-type"></a> Tipo di limite per le VPN

<!--7020519-->

Per semplificare la gestione dei client remoti, è ora possibile creare un nuovo tipo di limite per le VPN. In precedenza era necessario creare limiti per i client VPN in base all'indirizzo IP o alla subnet. Questa configurazione può essere complessa o non fattibile a causa della configurazione della subnet o della progettazione della VPN.

Ora quando un client invia una richiesta di posizione, include informazioni aggiuntive sulla propria configurazione di rete. In base a queste informazioni, il server determina se il client si trova su una VPN.

Per altre informazioni, vedere [Definire limiti](../../servers/deploy/configure/boundaries.md).

### <a name="management-insights-to-optimize-for-remote-workers"></a>Informazioni dettagliate sulla gestione per l'ottimizzazione dei ruoli di lavoro remoti

<!--6982226-->

Questa versione aggiunge un nuovo gruppo di informazioni dettagliate sulla gestione, **Ottimizzazione dei ruoli di lavoro remoti**. Queste informazioni dettagliate consentono di creare esperienze migliori per i ruoli di lavoro remoti e di ridurre il carico sull'infrastruttura. Le informazioni dettagliate in questa versione riguardano principalmente la VPN:

- **Definire gruppi di limiti VPN**
- **Configurare i client connessi alla VPN per preferire le origini del contenuto basate sul cloud**
- **Disabilitare la condivisione del contenuto peer-to-peer per i client connessi alla VPN**

Per altre informazioni, vedere [Informazioni dettagliate sulla gestione](../../servers/manage/management-insights.md).

### <a name="improved-support-for-windows-virtual-desktop"></a> Miglioramenti al supporto per Desktop virtuale Windows

<!--6527576-->

La piattaforma **Windows 10 Enterprise multisessione** è ora disponibile nell'elenco delle versioni del sistema operativo supportate negli oggetti con regole dei requisiti o elenchi di applicabilità.

Per altre informazioni sul supporto di Configuration Manager per Desktop virtuale Windows, vedere [Versioni dei sistemi operativi supportate per client e dispositivi](../configs/supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop).

### <a name="intranet-clients-can-use-a-cmg-software-update-point"></a>I client Intranet possono usare un punto di aggiornamento software CMG
<!--7102873-->
I client Intranet possono ora accedere a un punto di aggiornamento software di CMG quando viene assegnato a un gruppo di limiti. Per altre informazioni, vedere [Configurare gruppi di limiti](../../servers/deploy/configure/boundary-groups.md#bkmk_cmg-sup).

## <a name="cloud-attached-management"></a><a name="bkmk_cloud"></a> Gestione collegata al cloud

### <a name="use-the-company-portal-app-on-co-managed-devices"></a> Usare l'app Portale aziendale in dispositivi con co-gestione

<!--CMADO-3601237,INADO-4297660-->

Il Portale aziendale è ora l'esperienza di portale delle app multipiattaforma per Microsoft Endpoint Manager. Configurando i dispositivi co-gestiti in modo da usare anche il Portale aziendale, è possibile offrire un'esperienza utente coerente su tutti i dispositivi.

Per altre informazioni, vedere [Usare l'app Portale aziendale in dispositivi con co-gestione](../../../comanage/company-portal.md).

### <a name="use-microsoft-azure-china-21vianet-for-co-management"></a>Usare Microsoft Azure China (21Vianet) per la co-gestione
<!--7133238-->
È ora possibile selezionare il cloud di Azure Cina come ambiente Azure quando si abilita la co-gestione. Per altre informazioni, vedere [Come abilitare la co-gestione](../../../comanage/how-to-enable.md).

### <a name="notification-for-azure-ad-app-secret-key-expiration"></a>Notifica di scadenza della chiave privata dell'app Azure AD

<!--6386392-->

Se si configurano i servizi di Azure per il collegamento al cloud del sito, la console di Configuration Manager ora visualizza le notifiche per le circostanze seguenti:

- Una o più chiavi private dell'app Azure AD sono prossime alla scadenza
- Una o più chiavi private dell'app Azure AD sono scadute

Per altre informazioni, vedere [Rinnovare la chiave privata](../../servers/deploy/configure/azure-services-wizard.md#bkmk_renew).

### <a name="desktop-analytics"></a>Desktop Analytics

Per altre informazioni sulle modifiche mensili al servizio cloud Desktop Analytics, vedere [Novità di Desktop Analytics](../../../desktop-analytics/whats-new.md).

#### <a name="change-to-diagnostic-data-labels"></a>Modifiche alle etichette dei dati di diagnostica

<!-- 7363467 -->

Per un migliore allineamento con i requisiti di Desktop Analytics per i dati di diagnostica Windows, queste impostazioni hanno nuove etichette:

| Versione 2006 e successive | Versione 2002 e precedenti |
|---------|---------|
| Obbligatorio | Basic |
| Facoltativo (limitato) | Avanzata (con limitazioni) |
| N/D | Avanzato |
| Facoltativo | Full |

Se in precedenza sono stati configurati dispositivi al livello **Avanzato**, quando si esegue l'aggiornamento alla versione 2006 verranno ripristinati al livello **Facoltativo (limitato)** . Invieranno quindi meno dati a Microsoft. Questa modifica non dovrebbe avere alcun effetto sui dati visualizzati in Desktop Analytics.

Per altre informazioni, vedere [Abilitare la condivisione dei dati per Desktop Analytics](../../../desktop-analytics/enable-data-sharing.md).

## <a name="real-time-management"></a><a name="bkmk_real"></a> Gestione in tempo reale

### <a name="improvements-to-cmpivot"></a>Miglioramenti di CMPivot
<!--6518631-->
In CMPivot sono stati apportati i miglioramenti seguenti:

- È stata eseguita la convergenza di CMPivot autonomo e CMPivot dalla console
- È possibile eseguire CMPivot da un singolo dispositivo o da più dispositivi senza dover selezionare o creare una raccolta
- Dai risultati della query di CMPivot è possibile selezionare un singolo dispositivo o più dispositivi, quindi avviare un'istanza di CMPivot separata riferita alla selezione.

Per altre informazioni, vedere [CMPivot a partire dalla versione 2006](../../servers/manage/cmpivot-changes.md#bkmk_2006).

## <a name="client-management"></a><a name="bkmk_client"></a> Gestione dei client

### <a name="install-and-upgrade-the-client-on-a-metered-connection"></a> Installare e aggiornare il client in una connessione a consumo

<!--6976145-->

In precedenza, se il dispositivo era connesso a una rete a consumo, non venivano installati nuovi client. I client esistenti venivano aggiornati solo se erano state consentite tutte le comunicazioni client. In questo modo i dispositivi che spesso eseguono il roaming in una rete a consumo, non verrebbero gestiti o lo sarebbero in una versione del client precedente. A partire da questa versione, è possibile installare e aggiornare il client quando l'impostazione client **Comunicazione dei client nelle connessioni Internet a consumo** è impostata su **Consenti** o **Limita**. Con questa impostazione, è possibile consentire al client di rimanere aggiornato, ma gestire comunque la comunicazione client in una rete a consumo.

Per definire il comportamento per una nuova installazione del client, è disponibile un nuovo parametro ccmsetup **/AllowMetered**. Quando si consente la comunicazione client in una rete a consumo per ccmsetup, il contenuto viene scaricato e registrato nel sito e vengono scaricati i criteri iniziali. Qualsiasi altra comunicazione client segue la configurazione dell'impostazione client da tali criteri.

Per altre informazioni, vedere gli articoli seguenti:

- [Informazioni sulle impostazioni client](../../clients/deploy/about-client-settings.md#client-communication-on-metered-internet-connections)
- [Informazioni sui parametri e le proprietà di installazione dei client](../../clients/deploy/about-client-installation-properties.md#allowmetered)

### <a name="improvements-to-managing-device-restarts"></a>Miglioramenti alla gestione dei riavvii dei dispositivi

<!--3601213-->

Configuration Manager offre molte opzioni per gestire le notifiche di riavvio e il riavvio del dispositivo. È ora possibile configurare le impostazioni di un client per impedire il riavvio automatico dei dispositivi quando richiesto da una distribuzione. Questa impostazione offre un maggiore controllo in situazioni univoche. Per impostazione predefinita, l'impostazione client **Configuration Manager può forzare il riavvio di un dispositivo** è abilitata, quindi Configuration Manager può forzare il riavvio dei dispositivi. Questa impostazione si applica a distribuzioni di applicazioni, aggiornamenti software e pacchetti che richiedono un riavvio.

Per altre informazioni, vedere [Notifiche di riavvio del dispositivo](../../clients/deploy/device-restart-notifications.md).

## <a name="application-management"></a><a name="bkmk_app"></a> Gestione delle applicazioni

### <a name="improvements-to-available-apps-via-cmg"></a>Miglioramenti alle app disponibili tramite CMG

<!--6935376-->
Questa versione corregge un problema relativo all'autenticazione di Software Center e Azure Active Directory (Azure AD). Per un client rilevato nella Intranet ma che comunica tramite Cloud Management Gateway, in precedenza Software Center avrebbe usato l'autenticazione di Windows. Il tentativo di ottenere l'elenco delle app disponibili per l'utente avrebbe avuto esito negativo. Ora viene usata l'identità di Azure Active Directory (Azure AD) per i dispositivi aggiunti ad Azure AD. Questi dispositivi possono essere aggiunti al cloud o ad AD ibrido.

Per altre informazioni, vedere [Distribuire app disponibili per l'utente](../../../apps/deploy-use/deploy-applications.md#deploy-user-available-applications).

### <a name="microsoft-365-apps-for-enterprise"></a>Microsoft 365 Apps for enterprise
<!--6298093-->
Il 21 aprile 2020 Microsoft Office 365 ProPlus è stato rinominato in Microsoft 365 Apps for enterprise. A partire dalla versione 2006, sono state apportate le modifiche seguenti:

- La console di Configuration Manager è stata aggiornata per l'uso del nuovo nome.
  - Questa modifica include anche i nomi dei canali di aggiornamento per Microsoft 365 Apps.
- Nella console è stato aggiunto un banner di notifica per avvisare se una o più regole di distribuzione automatica fanno riferimento a nomi di canali obsoleti nei criteri **Title** per gli aggiornamenti di Microsoft 365 Apps.

Per altre informazioni, vedere [Nomi dei canali di Microsoft 365 Apps](../../../sum/deploy-use/manage-office-365-proplus-updates.md#bkmk_channel) e [Dashboard di conformità di Microsoft 365 Apps](../../../sum/deploy-use/office-365-dashboard.md#bkmk_readiness-dash).

## <a name="os-deployment"></a><a name="bkmk_osd"></a> Distribuzione del sistema operativo

### <a name="task-sequence-media-support-for-cloud-based-content"></a> Supporto per la sequenza di attività per i contenuti basati su cloud

<!--6209223-->

Il supporto per la sequenza di attività ora può scaricare i contenuti basati su cloud. Ad esempio, può essere necessario inviare una chiave USB a un utente in un ufficio remoto per ricreare l'immagine del dispositivo. O si immagini un ufficio che ha un server PXE locale, ma si vuole che i dispositivi diano il più possibile la priorità ai servizi cloud. Anziché appesantire la rete WAN per scaricare contenuti di distribuzione del sistema operativo di grandi dimensioni, i supporti di avvio e le distribuzioni PXE possono ora ottenere contenuti da origini basate sul cloud, come ad esempio un gateway di gestione cloud (CMG) abilitato per la condivisione del contenuto.

> [!NOTE]
> Il dispositivo necessita tuttavia di una connessione Intranet al punto di gestione.

Per altre informazioni, vedere [Usare supporti di avvio per distribuire Windows in rete](../../../osd/deploy-use/use-bootable-media-to-deploy-windows-over-the-network.md#support-for-cloud-based-content).

### <a name="improvements-to-task-sequences-via-cmg"></a> Miglioramenti alle sequenze di attività tramite CMG

Questa versione include i miglioramenti seguenti per la distribuzione di sequenze di attività nei dispositivi che comunicano tramite Cloud Management Gateway (CMG):

- Supporto della distribuzione del sistema operativo<!--6997525-->: Con una sequenza di attività che usa un'immagine di avvio per distribuire un sistema operativo, è possibile distribuirlo in un dispositivo che comunica tramite CMG. È necessario che l'utente avvii la sequenza di attività da Software Center. Per altre informazioni, vedere [Pianificare CMG - Specifiche](../../clients/manage/cmg/plan-cloud-management-gateway.md#specifications).

- Questa versione corregge i due [problemi noti](../../servers/deploy/install/release-notes.md#task-sequences-cant-run-over-cmg) da Configuration Manager Current Branch versione 2002.<!-- 6983320 --> È ora possibile eseguire una sequenza di attività in un dispositivo che comunica tramite CMG nelle circostanze seguenti:

  - Un dispositivo del gruppo di lavoro registrato con un [token di registrazione in blocco](../../clients/deploy/deploy-clients-cmg-token.md)

  - Si configura il sito per [HTTP migliorato](../hierarchy/enhanced-http.md) e il punto di gestione è HTTP

### <a name="improvements-to-bitlocker-task-sequence-steps"></a>Miglioramenti dei passaggi della sequenza di attività di BitLocker

<!--6995601-->

È ora possibile specificare la modalità di crittografia del disco nei passaggi delle sequenze di attività **Attiva BitLocker** e **Pre-provisioning di BitLocker**. Per impostazione predefinita, nei passaggi si usa ancora il metodo di crittografia predefinito per la versione del sistema operativo.

Il passaggio **Attiva BitLocker** include ora anche l'impostazione **Ignora questo passaggio per computer senza TPM o con TPM non abilitato**. Quando si abilita questa impostazione, il passaggio registra un errore in un dispositivo senza un TPM o un TPM che non viene inizializzato e la sequenza di attività continua. Questa impostazione rende più semplice la gestione del comportamento della sequenza di attività nei dispositivi che non supportano completamente BitLocker.

Per altre informazioni, vedere [Passaggi della sequenza di attività](../../../osd/understand/task-sequence-steps.md).

### <a name="management-insight-rules-for-os-deployment"></a>Regole di dati analitici per la gestione per la distribuzione del sistema operativo

<!--6982275-->

Quando le dimensioni dei criteri delle sequenze di attività superano 32 MB, il client non riesce a elaborare i criteri di grandi dimensioni. Il client non riesce quindi a eseguire la distribuzione della sequenza di attività. Per consentire di gestire le dimensioni dei criteri delle sequenze di attività, questa versione include le informazioni dettagliate sulla gestione seguenti:

- **Dimensioni elevate delle sequenze di attività possono contribuire al superamento delle dimensioni massime dei criteri**

- **Le dimensioni totali dei criteri per le sequenze di attività superano il limite dei criteri**

> [!TIP]
> Queste regole si trovano in un nuovo gruppo per la **distribuzione del sistema operativo** . Anche la regola esistente per le **immagini d'avvio inutilizzate** si trova ora in questo gruppo.

Per altre informazioni, vedere [Informazioni dettagliate sulla gestione](../../servers/manage/management-insights.md#operating-system-deployment).

### <a name="improvements-to-os-deployment"></a>Miglioramenti della distribuzione del sistema operativo

Questa versione include i miglioramenti aggiuntivi seguenti per la distribuzione del sistema operativo:

- Usare una variabile della sequenza di attività per specificare la destinazione del passaggio [Formato e disco partizione](../../../osd/understand/task-sequence-steps.md#BKMK_FormatandPartitionDisk). Questa nuova opzione supporta sequenze di attività più complesse con comportamenti dinamici. Uno script personalizzato, ad esempio, può rilevare il disco e impostare la variabile in base al tipo di hardware. È quindi possibile usare più istanze di questo passaggio per configurare tipi di hardware e partizioni diversi.<!--6610288-->

- Il passaggio [Verifica conformità](../../../osd/understand/task-sequence-steps.md#BKMK_CheckReadiness) ora include un controllo per determinare se il dispositivo usa UEFI. Include anche una nuova variabile della sequenza di attività di sola lettura, **_TS_CRUEFI**.<!--6452769-->

- Se si abilita la [finestra di stato della sequenza di attività](../../../osd/understand/user-experience.md#task-sequence-progress) per visualizzare informazioni più dettagliate sullo stato di avanzamento, ora non vengono conteggiati i passaggi abilitati in un gruppo disabilitato. Questa modifica consente di rendere più precisa la stima dello stato di avanzamento.<!--6448412-->

- In precedenza, durante una sequenza di attività per aggiornare un dispositivo a Windows 10, durante una delle fasi finali della configurazione di Windows veniva visualizzata una finestra del prompt dei comandi. La finestra si basava sulla configurazione guidata di Windows e gli utenti potevano usarla per interrompere il processo di aggiornamento. Ora gli script SetupCompleteTemplate.cmd e SetupRollbackTemplate.cmd di Configuration Manager includono una modifica per nascondere questa finestra del prompt dei comandi.<!--2837795-->

- Alcuni clienti creano interfacce personalizzate della sequenza di attività usando il metodo **IProgressUI::ShowMessage**, ma questo metodo non restituisce un valore per la risposta dell'utente. Questa versione aggiunge il metodo [IProgressUI::ShowMessageEx](../../../develop/reference/core/clients/client-classes/iprogressui--showmessageex-method.md). Questo nuovo metodo è simile al metodo esistente, ma include anche una nuova variabile di risultato Integer, **pResult**.<!--6448458-->

## <a name="protection"></a>Protezione

### <a name="cmg-support-for-endpoint-protection-policies"></a>Supporto di CMG per i criteri di protezione endpoint

<!--4773948-->

Mentre Cloud Management Gateway (CMG) supportava i criteri Endpoint Protection, i dispositivi richiedevano l'accesso a controller di dominio locali. A partire da questa versione, i client che comunicano tramite CMG possono applicare immediatamente i criteri Endpoint Protection senza una connessione attiva ad Active Directory.

Per altre informazioni, vedere [Supporto di CMG per le funzionalità di Configuration Manager](../../clients/manage/cmg/plan-cloud-management-gateway.md#support-for-configuration-manager-features).

### <a name="bitlocker-management-support-for-hierarchies"></a>Supporto per la gestione di BitLocker per le gerarchie

<!-- 5925693 -->

È ora possibile installare il portale self-service di BitLocker e il sito Web di amministrazione e monitoraggio nel sito di amministrazione centrale.

Per altre informazioni, vedere [Configurare i portali di BitLocker](../../../protect/deploy-use/bitlocker/setup-websites.md).

## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a> Console di Configuration Manager

### <a name="community-hub-and-github"></a>Hub della community e GitHub
<!--3555935, 3555936, deep link included 4224406-->

*(Introdotto per la prima volta nel giugno del 2020)*

La community di amministratori IT ha sviluppato un patrimonio di conoscenze nel corso degli anni. Per offrire la possibilità di condividere le esperienze, evitando di reinventare da zero elementi come script e report, abbiamo creato l'**Hub della community** di Configuration Manager. Sfruttando il lavoro degli altri, è possibile risparmiare diverse ore di lavoro. L'hub della community incentiva la creatività offrendo la possibilità di condividere reciprocamente con gli altri i risultati del proprio lavoro. GitHub include già processi e strumenti a livello di settore destinati alla condivisione. Ora tramite l'hub della community questi strumenti potranno essere usati direttamente nella console di Configuration Manager come basi per lo sviluppo di questa nuova community. Per la versione iniziale, il contenuto reso disponibile nell'hub della community verrà caricato solo da Microsoft. 

Per altre informazioni, vedere [Hub della community e GitHub](../../servers/manage/community-hub.md).

### <a name="direct-links-to-community-hub-items"></a><a name="bkmk_deeplink"></a> Collegamenti diretti agli elementi dell'hub della community
<!--4224406-->
È possibile esplorare facilmente e fare riferimento a elementi nel nodo dell'hub della community della console di Configuration Manager con un collegamento diretto. Per altre informazioni, vedere [Collegamenti diretti agli elementi dell'hub della community](../../servers/manage/community-hub.md#bkmk_deeplink).

### <a name="notifications-from-microsoft"></a>Notifiche da Microsoft
<!--3953121-->
Ora è possibile scegliere di ricevere notifiche da Microsoft nella console di Configuration Manager. Queste notifiche consentono di ricevere informazioni sulle funzionalità nuove o aggiornate, sulle modifiche apportate a Configuration Manager e ai servizi collegati e sui problemi che richiedono azioni di correzione.

Per altre informazioni, vedere [Configurare un sito per ricevere messaggi da Microsoft](../../servers/manage/admin-console-notifications.md#bkmk_msft).

### <a name="power-bi-sample-reports"></a>Report di esempio di Power BI
<!--5679791-->

*(Introdotto per la prima volta nel giugno del 2020)*

Quando si integrano il server di report di Power BI con la creazione di report di Configuration Manager, risultano disponibili report di Power BI di esempio. Scaricare e installare i report di esempio seguenti:

- Stato di conformità degli aggiornamenti software
- Stato di distribuzione degli aggiornamenti software

Per altre informazioni, vedere [Installare report di esempio di Power BI](../../servers/manage/powerbi-sample-reports.md).

<!-- Unused sections in this release:
## Reporting
## <a name="bkmk_userxp"></a> User experience
## <a name="bkmk_sum"></a> Software updates
## Office management
## <a name="bkmk_content"></a> Content management
## <a name="bkmk_comgmt"></a> Co-management
-->

## <a name="deprecated-operating-systems"></a><a name="bkmk_deprecated"></a> Sistemi operativi deprecati

Per conoscere le modifiche relative al supporto prima che siano implementate, vedere [Elementi rimossi e deprecati](deprecated/removed-and-deprecated.md).

Come annunciato per la prima volta nella versione 1906, la versione 2006 elimina il supporto per le versioni del sistema operativo client seguenti:  

- Windows CE 7.0
- Windows 10 Mobile
- Windows 10 Mobile Enterprise

## <a name="other-updates"></a>Altri aggiornamenti

<!--
Starting with this version, the following features are no longer [pre-release](../../servers/manage/pre-release-features.md):

### Azure Active Directory user group discovery](../../servers/deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco)<!--3611956
-->

Per altre informazioni sulle modifiche apportate ai cmdlet di Windows PowerShell per Configuration Manager, vedere le [note sulla versione 2006 di PowerShell](/powershell/sccm/2006-release-notes).

Per altre informazioni sulle modifiche all'API REST del servizio di amministrazione, vedere le [note sulla versione del servizio di amministrazione](../../../develop/adminservice/release-notes.md#bkmk_2006).

A parte le nuove funzionalità, questa versione include anche ulteriori modifiche, ad esempio correzioni di bug. Per altre informazioni, vedere [Riepilogo delle modifiche in Configuration Manager Current Branch, versione 2006](https://support.microsoft.com/help/4578830).

<!--
The following update rollup (4517869) is available in the console starting on October 1, 2019: [Update rollup for Configuration Manager current branch, version 1906](https://support.microsoft.com/help/4517869).

-->

<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune connector certificate does not renew in Configuration Manager | 18 January 2019 | Yes |

> [!NOTE]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](../../servers/manage/updates.md#bkmk_supersede).
-->

## <a name="next-steps"></a>Passaggi successivi

<!-- At this time, version 2006 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-2006.md#early-update-ring). -->

A partire dal 31 agosto 2020, la versione 2006 è disponibile per l'installazione a livello globale da parte di tutti i clienti.

Al momento di installare questa versione, vedere [Installazione degli aggiornamenti per Configuration Manager](../../servers/manage/updates.md) ed [Elenco di controllo per l'installazione dell'aggiornamento 2006](../../servers/manage/checklist-for-installing-update-2006.md).

> [!TIP]
> Per installare un nuovo sito, usare una versione base di Configuration Manager.
>
> Sono disponibili altre informazioni su:
>
> - [Installing new sites](../../servers/deploy/install/installing-sites.md) (Installare nuovi siti)
> - [Baseline and update versions](../../servers/manage/updates.md#bkmk_Baselines) (Versioni di base e di aggiornamento)

Per problemi noti e importanti, vedere [Note sulla versione](../../servers/deploy/install/release-notes.md).

Dopo aver aggiornato un sito, vedere anche [Elenco di controllo post-aggiornamento](../../servers/manage/checklist-for-installing-update-2006.md#post-update-checklist).
