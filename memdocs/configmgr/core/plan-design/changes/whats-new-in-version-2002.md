---
title: Novità della versione 2002
titleSuffix: Configuration Manager
description: Informazioni dettagliate sulle modifiche e sulle nuove funzionalità introdotte nella versione 2002 di Configuration Manager Current Branch.
ms.date: 06/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: de718cdc-d0a9-47e2-9c99-8fa2cb25b5f8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 58819d764f69ab7e1cc928e14189e01470deb73b
ms.sourcegitcommit: f3f2632df123cccd0e36b2eacaf096a447022b9d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85590440"
---
# <a name="whats-new-in-version-2002-of-configuration-manager-current-branch"></a>Novità della versione 2002 di Configuration Manager Current Branch

*Si applica a: Configuration Manager (Current Branch)*

L'aggiornamento 2002 per Configuration Manager Current Branch è disponibile come aggiornamento nella console. Applicare questo aggiornamento ai siti con la versione 1810 o successiva. <!-- baseline only statement:-->Quando si installa un nuovo sito, è disponibile anche come versione di base. Questo articolo offre un riepilogo delle modifiche e delle nuove funzionalità di Configuration Manager versione 2002.

Esaminare sempre l'elenco di controllo più recente per installare questo aggiornamento. Per altre informazioni, vedere [Elenco di controllo per l'installazione dell'aggiornamento 2002](../../servers/manage/checklist-for-installing-update-2002.md). Dopo aver aggiornato un sito, vedere anche [Elenco di controllo post-aggiornamento](../../servers/manage/checklist-for-installing-update-2002.md#post-update-checklist).

Per sfruttare i vantaggi delle nuove funzionalità di Configuration Manager, dopo l'aggiornamento del sito aggiornare anche i client alla versione più recente. Anche se le nuove funzionalità vengono visualizzate nella console di Configuration Manager quando si esegue l'aggiornamento del sito e della console, lo scenario completo risulta funzionante solo dopo l'aggiornamento alla versione più recente del client.

> [!TIP]
> Per ricevere una notifica quando questa pagina viene aggiornata, copiare e incollare l'URL seguente nel lettore di feed RSS: `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+2002+-+Configuration+Manager%22&locale=en-us`

## <a name="microsoft-endpoint-manager-tenant-attach"></a><a name="bkmk_tenant"></a> Collegamento del tenant di Microsoft Endpoint Manager

### <a name="device-sync-and-device-actions"></a><a name="bkmk_attach"></a> Sincronizzazione e azioni dei dispositivi
<!--3555758-->
Microsoft Endpoint Manager è una soluzione integrata per la gestione di tutti i dispositivi. Microsoft ha riunito Configuration Manager e Intune in un'unica console denominata **Interfaccia di amministrazione di Microsoft Endpoint Manager**. A partire da questa versione è possibile caricare dispositivi Configuration Manager nel servizio cloud ed effettuare azioni dal pannello **Dispositivi**  dell'interfaccia di amministrazione.

Per altre informazioni, vedere [Collegamento del tenant di Microsoft Endpoint Manager](../../../tenant-attach/device-sync-actions.md).

## <a name="site-infrastructure"></a><a name="bkmk_infra"></a> Infrastruttura del sito

### <a name="remove-a-central-administration-site"></a>Rimuovere un sito di amministrazione centrale
<!-- 3607277 -->

Se la gerarchia è costituita da un sito di amministrazione centrale e da un singolo sito primario figlio, è ora possibile rimuovere il sito di amministrazione centrale. Questa azione semplifica l'infrastruttura di Configuration Manager riducendola a un singolo sito primario autonomo. Elimina le complessità della replica da sito a sito e concentra le attività di gestione al singolo sito primario.

Per altre informazioni, vedere [Rimuovere il sito di amministrazione centrale](../../servers/deploy/install/remove-central-administration-site.md).

### <a name="new-management-insight-rules"></a>Nuove regole delle informazioni dettagliate sulla gestione

Questa versione include le regole di analisi della gestione seguenti:

- Nove regole nel gruppo **Valutazione di Configuration Manager** cortesia di Microsoft Premier Field Engineering. Queste regole sono un esempio dei molti altri controlli forniti da Microsoft Premier nell'hub Servizi.<!-- 3607758 -->

  - La configurazione di Individuazione gruppo di protezione Active Directory prevede un'esecuzione troppo frequente
  - La configurazione di Individuazione sistema Active Directory prevede un'esecuzione troppo frequente
  - La configurazione di Individuazione utente Active Directory prevede un'esecuzione troppo frequente
  - Raccolte limitate a Tutti i sistemi o Tutti gli utenti
  - L'opzione Individuazione heartbeat è disabilitata
  - Query su raccolte a esecuzione prolungata abilitate per gli aggiornamenti incrementali
  - Riduci il numero di applicazioni e pacchetti nei punti di distribuzione
  - Problemi di installazione dei siti secondari
  - Aggiorna tutti i siti alla stessa versione

- Per configurare il sito per l'aggiunta di comunicazioni HTTPS sicure, sono presenti due regole aggiuntive nel gruppo **Servizi cloud**:<!-- 6268489 -->

  - Siti senza configurazione HTTPS appropriata
  - Dispositivi non caricati in Azure AD

Per altre informazioni, vedere [Informazioni dettagliate sulla gestione](../../servers/manage/management-insights.md).

### <a name="improvements-to-administration-service"></a>Miglioramenti al servizio di amministrazione

<!-- 5728365 -->

Il servizio di amministrazione è un'API REST per il provider SMS. In precedenza era necessario implementare una delle dipendenze seguenti:

- Abilitare HTTP migliorato per l'intero sito
- Associare manualmente un certificato basato su PKI a IIS nel server che ospita il ruolo Provider SMS

A partire da questa versione, il servizio di amministrazione usa automaticamente il certificato autofirmato del sito. Questa modifica contribuisce a semplificare l'uso del servizio di amministrazione. Il sito genera sempre questo certificato. L'impostazione del sito HTTP migliorato **Usa i certificati generati da Configuration Manager per sistemi del sito HTTP** controlla solo se i sistemi del sito lo usano o meno. Il servizio di amministrazione ignora ora questa impostazione del sito, perché usa sempre il certificato del sito anche se nessun altro sistema del sito usa HTTP migliorato. È comunque possibile usare un certificato di autenticazione server basato su PKI.

Per altre informazioni, vedere i nuovi articoli seguenti:

- [Che cos'è il servizio di amministrazione](../../../develop/adminservice/overview.md)
- [Come configurare il servizio di amministrazione](../../../develop/adminservice/set-up.md)

### <a name="proxy-support-for-azure-active-directory-discovery-and-group-sync"></a>Supporto proxy per l'individuazione e la sincronizzazione dei gruppi di Azure Active Directory

<!-- 5913817 -->

Le impostazioni proxy del sistema del sito, inclusa l'autenticazione, vengono ora usate da:

- Individuazione degli utenti di Azure Active Directory (Azure AD)
- Individuazione dei gruppi di utenti di Azure AD
- Sincronizzazione dei risultati di appartenenza alla raccolta con i gruppi di Azure Active Directory

Per altre informazioni, vedere [Supporto dei server proxy](../network/proxy-server-support.md#bkmk_other).

## <a name="cloud-attached-management"></a><a name="bkmk_cloud"></a> Gestione collegata al cloud

### <a name="critical-status-message-shows-server-connection-errors-to-required-endpoints"></a>Messaggio di stato critico che mostra gli errori di connessione del server agli endpoint necessari

<!-- 5566763 -->

Se il server del sito di Configuration Manager non riesce a connettersi agli endpoint necessari per un servizio cloud, genera un messaggio di stato critico con ID 11488. Quando il server del sito non è in grado di connettersi al servizio, lo stato del componente SMS_SERVICE_CONNECTOR diventa critico. Visualizzare lo stato dettagliato nel nodo Stato componente della console di Configuration Manager.

### <a name="token-based-authentication-for-cloud-management-gateway"></a>Autenticazione basata su token per Cloud Management Gateway

<!-- 5686290 -->

Cloud Management Gateway (CMG) supporta molti tipi di client, ma anche con HTTP avanzato, questi client richiedono un certificato di autenticazione client. Può essere complicato gestire il provisioning di questo requisito del certificato nei client basati su Internet che non si connettono spesso alla rete interna, non possono essere aggiunti ad Azure Active Directory (Azure AD) e non hanno un metodo per installare un certificato emesso da PKI.

Configuration Manager estende il supporto dei dispositivi con i metodi seguenti:

- Registrazione nella rete interna per un token univoco
- Creare un token di registrazione in blocco per i dispositivi basati su Internet

Per altre informazioni, vedere [Autenticazione basata su token per CMG](../../clients/deploy/deploy-clients-cmg-token.md).

### <a name="microsoft-endpoint-configuration-manager-cloud-features"></a>Funzionalità cloud di Microsoft Endpoint Configuration Manager

<!--5834830-->

Quando sono disponibili nuove funzionalità basate sul cloud nell'interfaccia di amministrazione di Microsoft Endpoint Manager o in altri servizi cloud collegati per l'installazione locale di Configuration Manager, è possibile ora acconsentire esplicitamente a queste nuove funzionalità nella console di Configuration Manager. Per altre informazioni sull'abilitazione delle funzionalità nella console di Configuration Manager, vedere [Abilitare le funzionalità facoltative degli aggiornamenti](../../servers/manage/install-in-console-updates.md#bkmk_options).

## <a name="desktop-analytics"></a><a name="bkmk_da"></a> Desktop Analytics

Per altre informazioni sulle modifiche mensili al servizio cloud Desktop Analytics, vedere [Novità di Desktop Analytics](../../../desktop-analytics/whats-new.md).

### <a name="connection-health-dashboard-shows-client-connection-issues"></a>Il dashboard Integrità connessione mostra i problemi di connessione client

Per monitorare l'integrità della connettività dei client, usare il dashboard Integrità connessione di Desktop Analytics in Configuration Manager. Consente ora di identificare più facilmente i problemi di configurazione del proxy client in due aree:

- **Controlli della connettività degli endpoint**: se i client non riescono a raggiungere un endpoint richiesto, viene visualizzato un avviso di configurazione nel dashboard. Eseguire il drill-down per visualizzare gli endpoint a cui i client non possono connettersi a causa di problemi di configurazione del proxy.<!-- 4963230 -->

- **Stato della connettività**: se i client usano un server proxy per accedere al servizio cloud Desktop Analytics, Configuration Manager visualizza ora i problemi di autenticazione del proxy dai client. Eseguire il drill-down per visualizzare i client che non possono eseguire la registrazione a causa dell'autenticazione del proxy.<!-- 4963383 -->

Per altre informazioni, vedere [Monitorare l'integrità della connessione](../../../desktop-analytics/monitor-connection-health.md).

## <a name="real-time-management"></a><a name="bkmk_real"></a> Gestione in tempo reale

### <a name="improvements-to-cmpivot"></a>Miglioramenti di CMPivot

<!-- 5870934 -->

È stata semplificata l'esplorazione delle entità CMPivot. È ora possibile cercare entità CMPivot. Sono state inoltre aggiunte nuove icone per distinguere facilmente le entità e i tipi di oggetto entità.

Per altre informazioni, vedere [CMPivot](../../servers/manage/cmpivot.md#bkmk_2002).

## <a name="content-management"></a><a name="bkmk_content"></a> Gestione dei contenuti

### <a name="exclude-certain-subnets-for-peer-content-download"></a>Escludere determinate subnet per il download del contenuto peer

<!-- 3555777 -->

I gruppi di limiti includono l'opzione seguente per i download peer: **Durante i download peer, usa solo i peer entro la stessa subnet**. Se si abilita questa opzione, l'elenco delle posizioni del contenuto dal punto di gestione include solo le origini peer nella stessa subnet e nello stesso gruppo di limiti del client. A seconda della configurazione della rete, è ora possibile escludere determinate subnet per l'individuazione delle corrispondenze. Ad esempio, si vuole includere un limite ma escludere una subnet VPN specifica.

Per altre informazioni vedere [Opzioni del gruppo di limiti](../../servers/deploy/configure/boundary-groups.md#bkmk_bgoptions).

### <a name="proxy-support-for-microsoft-connected-cache"></a>Supporto del proxy per Microsoft Connected Cache

<!-- 5856396 -->

Se l'ambiente usa un server proxy non autenticato per l'accesso a Internet, ora quando si abilita un punto di distribuzione di Configuration Manager per Microsoft Connected Cache, può comunicare tramite il proxy. Per altre informazioni, vedere [Microsoft Connected Cache](../hierarchy/microsoft-connected-cache.md).

## <a name="client-management"></a><a name="bkmk_client"></a> Gestione dei client

### <a name="client-log-collection"></a>Raccolta dei log del client

<!-- 4226618 -->

È ora possibile attivare un dispositivo client per il caricamento dei rispettivi log del client nel server del sito mediante l'invio di un'azione di notifica client dalla console di Configuration Manager.

Per altre informazioni, vedere [Notifiche client](../../clients/manage/client-notification.md#client-diagnostics).

### <a name="wake-up-a-device-from-the-central-administration-site"></a>Riattivare un dispositivo dal sito di amministrazione centrale

<!-- 6030715 -->

Dal sito di amministrazione centrale, nel nodo Dispositivi o Raccolte di dispositivi, è ora possibile usare l'azione di notifica client per riattivare i dispositivi. Questa azione era disponibile in precedenza solo da un sito primario.

Per altre informazioni, vedere [Come configurare la riattivazione LAN](../../clients/deploy/configure-wake-on-lan.md#bkmk_wol-1810).

### <a name="improvements-to-support-for-arm64-devices"></a>Miglioramenti al supporto per dispositivi ARM64

<!--5954175-->

La piattaforma **Tutti i dispositivi Windows 10 (ARM64)** è disponibile nell'elenco delle versioni dei sistemi operativi supportate per gli oggetti con regole di requisiti o elenchi di applicabilità.

> [!NOTE]
> Se in precedenza era stata selezionata la piattaforma **Windows 10** di primo livello, con questa azione sono state selezionate automaticamente entrambe le piattaforme **Tutti i dispositivi Windows 10 (64 bit)** e **Tutti i dispositivi Windows 10 (32 bit)** . Questa nuova piattaforma non viene selezionata automaticamente. Se si vuole aggiungere **Tutti i dispositivi Windows 10 (ARM64)** , selezionarla manualmente nell'elenco.

Per altre informazioni sul supporto di Configuration Manager per dispositivi ARM64, vedere [Windows 10 in ARM64](../configs/support-for-windows-10.md#bkmk_arm64).

### <a name="track-configuration-item-remediations"></a>Tenere traccia delle correzioni per gli elementi di configurazione
<!--4261411-->
È ora possibile usare l'opzione **Track remediation history when supported** (Tieni traccia della cronologia delle correzioni quando supportato) per le regole di conformità degli elementi di configurazione. Quando questa opzione è abilitata, qualsiasi correzione eseguita sul client per l'elemento di configurazione genera un messaggio di stato. La cronologia viene archiviata nel database di Configuration Manager.

Per altre informazioni su questa impostazione, vedere [Come creare elementi di configurazione personalizzati per computer desktop e server Windows gestiti con il client di Configuration Manager](../../../compliance/deploy-use/create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-client.md#bkmk_track).

<!-- ## <a name="bkmk_comgmt"></a> Co-management -->

## <a name="application-management"></a><a name="bkmk_app"></a> Gestione delle applicazioni

### <a name="microsoft-edge-management-dashboard"></a>Dashboard Gestione di Microsoft Edge

<!-- 3871913 -->

Il dashboard Gestione di Microsoft Edge fornisce informazioni dettagliate sull'uso di Microsoft Edge e di altri browser. In questo dashboard è possibile:

- Vedere in quanti dispositivi è installato Microsoft Edge
- Vedere quanti client hanno versioni diverse di Microsoft Edge installate
- Ottenere una panoramica dei browser installati nei vari dispositivi
- Visualizzazione del browser preferito per dispositivo

Dall'area di lavoro Raccolta software fare clic su Gestione di Microsoft Edge per visualizzare il dashboard. Modificare la raccolta per i dati del grafo facendo clic Sfoglia e scegliendo un'altra raccolta. Per impostazione predefinita, l'elenco a discesa include le cinque raccolte più grandi. Quando si seleziona una raccolta che non è presente nell'elenco, la raccolta appena selezionata occupa la posizione più in basso nell'elenco a discesa.

Per altre informazioni, vedere [Gestione di Microsoft Edge](../../../apps/deploy-use/deploy-edge.md#bkmk_edge-dash).

### <a name="improvements-to-microsoft-edge-management"></a>Miglioramenti alla gestione di Microsoft Edge

<!-- 4561024 -->

È ora possibile creare un'applicazione Microsoft Edge configurandola in modo da ricevere aggiornamenti automatici anziché avere gli aggiornamenti automatici disabilitati. Questa modifica consente di scegliere di gestire gli aggiornamenti per Microsoft Edge con Configuration Manager o consentire l'aggiornamento automatico di Microsoft Edge. Quando si crea l'applicazione, selezionare Allow Microsoft Edge to automatically update the version of the client on the end user's device (Consenti a Microsoft Edge di aggiornare automaticamente la versione del client nel dispositivo dell'utente finale) nella pagina Impostazioni di Microsoft Edge.

Per altre informazioni, vedere [Gestione di Microsoft Edge](../../../apps/deploy-use/deploy-edge.md#bkmk_autoupdate).

### <a name="task-sequence-as-an-app-model-deployment-type"></a>Sequenza di attività come tipo di distribuzione del modello di app

<!-- 3555953 -->

È ora possibile installare applicazioni complesse usando le sequenze di attività con il modello di applicazione. Aggiungere un tipo di distribuzione a un'app che è una sequenza di attività per installare o disinstallare l'app. Questa funzionalità offre questi comportamenti:

- Visualizzare la sequenza di attività dell'app con un'icona in Software Center. Un'icona rende più semplice per gli utenti individuare e identificare la sequenza di attività dell'app.

- Definire metadati aggiuntivi per la sequenza di attività dell'app, incluse le informazioni localizzate

Per altre informazioni, vedere [Creare applicazioni Windows](../../../apps/get-started/creating-windows-applications.md#bkmk_tsdt).

## <a name="os-deployment"></a><a name="bkmk_osd"></a> Distribuzione del sistema operativo

### <a name="bootstrap-a-task-sequence-immediately-after-client-registration"></a>Avviare una sequenza di attività immediatamente dopo la registrazione del client

<!-- 5526972 -->

Quando si installa e si registra un nuovo client di Configuration Manager e si distribuisce anche una sequenza di attività, è difficile determinare il momento in cui verrà eseguita la sequenza di attività dopo la registrazione. Questa versione introduce una nuova proprietà di installazione client che è possibile usare per avviare una sequenza di attività in un client dopo che è stato registrato correttamente nel sito.

Per altri dettagli, vedere [Informazioni sulle proprietà di installazione client - PROVISIONTS](../../clients/deploy/about-client-installation-properties.md#provisionts).

### <a name="improvements-to-check-readiness-task-sequence-step"></a>Miglioramenti al passaggio della sequenza di attività Verifica conformità

<!-- 6005561 -->

È ora possibile verificare più proprietà del dispositivo nel passaggio della sequenza di attività **Verifica conformità**. Usare questo passaggio in una sequenza di attività per verificare che il computer di destinazione soddisfi le condizioni dei prerequisiti.

- Architettura del sistema operativo corrente
- Versione minima del sistema operativo
- Versione massima del sistema operativo
- Versione minima del client
- Lingua del sistema operativo corrente
- Alimentazione da rete elettrica collegata
- La scheda di rete è connessa e non è wireless

Per altre informazioni, vedere [Passaggi della sequenza di attività - Verifica conformità](../../../osd/understand/task-sequence-steps.md#BKMK_CheckReadiness).

### <a name="improvements-to-task-sequence-progress"></a>Miglioramenti per lo stato delle sequenze di attività

<!-- 5932692 -->

La finestra di stato della sequenza di attività include ora i miglioramenti seguenti:

- È possibile abilitarla per visualizzare il numero del passaggio corrente, il numero totale di passaggi e la percentuale di completamento
- Ingrandimento della finestra per offrire più spazio per mostrare meglio il nome dell'organizzazione su un'unica riga

Per altre informazioni, vedere [Esperienze utente per la distribuzione del sistema operativo](../../../osd/understand/user-experience.md#task-sequence-progress).

### <a name="improvements-to-os-deployment"></a>Miglioramenti della distribuzione del sistema operativo

Questa versione include i miglioramenti seguenti alla distribuzione del sistema operativo:

- L'ambiente della sequenza di attività include una nuova variabile di sola lettura, `_TSSecureBoot`.<!--5842295--> Usare questa variabile per determinare lo stato dell'avvio protetto in un dispositivo abilitato per UEFI. Per altre informazioni, vedere [_TSSecureBoot](../../../osd/understand/task-sequence-variables.md#TSSecureBoot).

- Impostare le variabili della sequenza di attività per configurare il contesto utente per i passaggi **Esegui riga di comando** ed **Esegui script PowerShell**.<!-- 5573175 --> Per altre informazioni, vedere [SMSTSRunCommandLineAsUser](../../../osd/understand/task-sequence-variables.md#SMSTSRunCommandLineAsUser) e [SMSTSRunPowerShellAsUser](../../../osd/understand/task-sequence-variables.md#SMSTSRunPowerShellAsUser).

- Nel passaggio **Esegui script PowerShell** è ora possibile impostare la proprietà **Parametri** su una variabile.<!-- 5690481 --> Per altre informazioni, vedere [Eseguire script di PowerShell](../../../osd/understand/task-sequence-steps.md#BKMK_RunPowerShellScript).

- Il risponditore PXE di Configuration Manager invia ora i messaggi di stato al server del sito. Questa modifica semplifica la risoluzione dei problemi relativi alle distribuzioni del sistema operativo che usano questo servizio.<!-- 5568051 -->

<!-- ## <a name="bkmk_userxp"></a> Software Center -->

## <a name="software-updates"></a><a name="bkmk_sum"></a> Aggiornamenti software

### <a name="orchestration-groups"></a>Gruppi di orchestrazione

<!-- 3098816 -->

Per controllare meglio la distribuzione degli aggiornamenti software nei dispositivi, è possibile creare un gruppo di orchestrazione. Molti amministratori del server devono gestire attentamente gli aggiornamenti per carichi di lavoro specifici e automatizzare i comportamenti tra loro.

Un gruppo di orchestrazione consente di aggiornare i dispositivi in base a una percentuale, un numero specifico o un ordine esplicito. È anche possibile eseguire uno script PowerShell prima e dopo che i dispositivi eseguono la distribuzione degli aggiornamenti.

Tutti i client di Configuration Manager, non solo i server, possono essere membri di un gruppo di orchestrazione. Le regole del gruppo di orchestrazione vengono applicate ai dispositivi per tutte le distribuzioni di aggiornamenti software in qualsiasi raccolta contenente un membro del gruppo di orchestrazione. Altri comportamenti di distribuzione rimangono validi, ad esempio le finestre di manutenzione e le pianificazioni della distribuzione.

Per altre informazioni, vedere [Gruppi di orchestrazione](../../../sum/deploy-use/orchestration-groups.md).

### <a name="evaluate-software-updates-after-a-servicing-stack-update"></a>Valutare gli aggiornamenti software dopo un aggiornamento dello stack di manutenzione

<!-- 4639943 -->

Configuration Manager ora rileva se un aggiornamento dello stack di manutenzione fa parte di un'installazione per più aggiornamenti. Quando viene rilevato un aggiornamento dello stack di manutenzione, questo viene installato per primo. Dopo aver installato l’aggiornamento dello stack di manutenzione, viene eseguito un ciclo di valutazione degli aggiornamenti software per installare gli aggiornamenti rimanenti. Questa modifica consente l'installazione di un aggiornamento cumulativo dipendente dopo l'aggiornamento dello stack di manutenzione. Non è necessario riavviare il dispositivo tra le installazioni e non è necessario creare una finestra di manutenzione aggiuntiva. Gli aggiornamenti dello stack di manutenzione vengono installati per primi solo per le installazioni non avviate dall'utente. Ad esempio, se un utente avvia un'installazione per più aggiornamenti da Software Center, è possibile che l'aggiornamento dello stack di manutenzione non venga installato per prima.

Per altre informazioni, vedere [Pianificare gli aggiornamenti software](../../../sum/plan-design/plan-for-software-updates.md#bkmk_ssu).

### <a name="office-365-updates-for-disconnected-software-update-points"></a>Aggiornamenti di Office 365 per punti di aggiornamento software disconnessi

<!-- 4065163 -->

È possibile usare un nuovo strumento per importare gli aggiornamenti di Office 365 da un server WSUS connesso a Internet in un ambiente di Configuration Manager disconnesso. In passato, quando si esportavano e importavano i metadati per il software aggiornato in ambienti disconnessi, non era possibile distribuire gli aggiornamenti di Office 365. Gli aggiornamenti di Office 365 richiedono metadati aggiuntivi scaricati da un'API di Office e dalla rete CDN di Office, operazione impossibile per gli ambienti disconnessi.

Per altre informazioni, vedere [Sincronizzare gli aggiornamenti di Office 365 da un punto di aggiornamento software disconnesso](../../../sum/get-started/synchronize-office-updates-disconnected.md).

<!-- ## <a name="bkmk_o365"></a> Office management -->

## <a name="protection"></a><a name="bkmk_protect"></a> Protezione

### <a name="expand-microsoft-defender-advanced-threat-protection-atp-onboarding"></a>Espansione dell'onboarding di Microsoft Defender Advanced Threat Protection (ATP)
 
<!-- 5229962 -->
Configuration Manager ha espanso il supporto per l'onboarding di dispositivi in Microsoft Defender ATP. Per altre informazioni, vedere [Microsoft Defender Advanced Threat Protection](../../../protect/deploy-use/defender-advanced-threat-protection.md).

### <a name="onboard-configuration-manager-clients-to-microsoft-defender-atp-via-the-microsoft-endpoint-manager-admin-center"></a><a name="bkmk_atp"></a> Eseguire l'onboarding di client di Configuration Manager in Microsoft Defender ATP tramite l'interfaccia di amministrazione di Microsoft Endpoint Manager
<!--5691658-->
È ora possibile distribuire i criteri di onboarding di Microsoft Defender ATP Endpoint Detection and Response (EDR) nei client gestiti di Configuration Manager. Questi client non richiedono Azure AD o la registrazione MDM e il criterio è destinato alle raccolte di ConfigMgr anziché ai gruppi di Azure AD.

Questa funzionalità consente ai clienti di gestire sia la soluzione MDM di Intune che l'onboarding EDR/ATP del client di Configuration Manager da una singola esperienza di gestione, l'interfaccia di amministrazione di Microsoft Endpoint Manager. Per altre informazioni, vedere i [criteri di rilevamento di endpoint e risposta per la sicurezza degli endpoint in Intune](../../../../intune/protect/endpoint-security-edr-policy.md).

> [!Important]
> Per questa funzionalità è necessario che il rollup di hotfix [KB4563473](https://support.microsoft.com/help/4563473) sia installato nell'ambiente in uso.

### <a name="improvements-to-bitlocker-management"></a>Miglioramenti alla gestione di BitLocker

- I criteri di gestione di BitLocker ora includono impostazioni aggiuntive, tra cui i criteri per le unità fisse e rimovibili.<!-- 5925683 --> Per altre informazioni, vedere [Informazioni di riferimento sulle impostazioni di BitLocker](../../../protect/tech-ref/bitlocker/settings.md).

- In Configuration Manager Current Branch versione 1910, per integrare il servizio di ripristino di BitLocker in Configuration Manager era necessario abilitare un punto di gestione per HTTPS. La connessione HTTPS, infatti, è necessaria per crittografare le chiavi di ripristino attraverso la rete dal client Configuration Manager al punto di gestione. La procedura di configurazione del punto di gestione e di tutti i client per HTTPS, tuttavia, può risultare per molti clienti troppo complessa.

    A partire da questa versione, il requisito HTTPS è valido solo per il sito Web IIS che ospita il servizio di ripristino, non per l'intero ruolo del punto di gestione. Con questa modifica vengono comunque soddisfatti i requisiti del certificato e crittografate le chiavi di ripristino in transito.<!-- 5925660 --> Per altre informazioni, vedere [Crittografare i dati di ripristino](../../../protect/deploy-use/bitlocker/encrypt-recovery-data.md).

## <a name="reporting"></a><a name="bkmk_report"></a> Creazione di report

### <a name="integrate-with-power-bi-report-server"></a>Integrare il server di report di Power BI

<!-- 3721603 -->

È ora possibile integrare il server di report di Power BI con la creazione di report di Configuration Manager. Questa integrazione offre una visualizzazione moderna e prestazioni migliori. Aggiunge il supporto della console per report di Power BI simili a quelli già esistenti con SQL Server Reporting Services.

Per altre informazioni, vedere [Integrare il server di report di Power BI](../../servers/manage/powerbi-report-server.md).

## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a> Console di Configuration Manager

### <a name="show-boundary-groups-for-devices"></a>Visualizzare i gruppi di limiti per i dispositivi

<!--6521835-->

Per semplificare la risoluzione dei problemi relativi ai comportamenti dei dispositivi con i gruppi di limiti, è ora possibile visualizzare i gruppi di limiti per dispositivi specifici. Nel nodo **Dispositivi** o quando si visualizzano i membri di una **Raccolta di dispositivi**, aggiungere la nuova colonna **Gruppi di limiti** alla visualizzazione elenco.

Per altre informazioni, vedere [Gruppi di limiti](../../servers/deploy/configure/boundary-groups.md#bkmk_show-boundary).

### <a name="send-a-smile-improvements"></a>Miglioramenti per Invia smile

<!-- 5891852 -->

Quando si invia uno smile o si invia una faccia imbronciata, viene creato un messaggio di stato quando vengono inviati i commenti e i suggerimenti. Questo miglioramento consente di registrare le informazioni seguenti:

- Quando sono stati inviati commenti e suggerimenti
- Chi ha inviato i commenti e suggerimenti
- L'ID dei commenti e suggerimenti
- Se l'invio di commenti e suggerimenti ha avuto esito positivo o negativo

Un messaggio di stato con ID 53900 indica un invio con esito positivo e l'ID 53901 corrisponde a un invio non riuscito.

Per altre informazioni, vedere la sezione su [commenti e suggerimenti per i prodotti](../../understand/find-help.md#BKMK_1806Feedback).

### <a name="search-all-subfolders-for-configuration-items-and-configuration-baselines"></a>Ricerca di Tutte le sottocartelle per Elementi di configurazione e Linee di base di configurazione

<!--5891241-->

In linea con i miglioramenti apportati nelle versioni precedenti, è possibile usare l'opzione di ricerca **Tutte le sottocartelle** dai nodi **Elementi di configurazione** e **Linee di base di configurazione**.

### <a name="community-hub"></a>Hub della community

<!--3555935, 3555936-->

_Introdotto per la prima volta nel giugno del 2020_

La community di amministratori IT ha sviluppato un patrimonio di conoscenze nel corso degli anni. Per offrire la possibilità di condividere le esperienze, evitando di reinventare da zero elementi come script e report, abbiamo creato l'**Hub della community** di Configuration Manager. Sfruttando il lavoro degli altri, è possibile risparmiare diverse ore di lavoro. L'hub della community incentiva la creatività offrendo la possibilità di condividere reciprocamente con gli altri i risultati del proprio lavoro. GitHub include già processi e strumenti a livello di settore destinati alla condivisione. Ora tramite l'hub della community questi strumenti potranno essere usati direttamente nella console di Configuration Manager come basi per lo sviluppo di questa nuova community.

Per altre informazioni, vedere [Hub della community e GitHub](../../servers/manage/community-hub.md).

## <a name="tools"></a><a name="bkmk_tools"></a> Strumenti

### <a name="onetrace-log-groups"></a>Gruppi di log di OneTrace

<!-- 5559993 -->

OneTrace supporta ora gruppi di log personalizzabili, in modo analogo alla funzionalità in Supporto Center. I gruppi di log consentono di aprire tutti i file di log per un singolo scenario. OneTrace include attualmente gruppi per gli scenari seguenti:

- Gestione delle applicazioni
- Impostazioni di conformità (definite anche gestione configurazione desiderata)
- Aggiornamenti software

Per altre informazioni, vedere [Supporto tecnico OneTrace](../../support/support-center-onetrace.md).

### <a name="improvements-to-extend-and-migrate-on-premises-site-to-microsoft-azure"></a><a name="bkmk_extend"></a>Miglioramenti per estendere ed eseguire la migrazione di un sito locale in Microsoft Azure
<!--5665775, 6307931-->
Lo strumento per estendere ed eseguire la migrazione di un sito locale in Microsoft Azure supporta ora il provisioning di più ruoli del sistema del sito in una singola macchina virtuale di Azure. È possibile aggiungere ruoli del sistema del sito dopo il completamento della distribuzione iniziale della macchina virtuale di Azure.

Per altre informazioni, vedere [Estendere ed eseguire la migrazione di un sito locale in Microsoft Azure](../../support/azure-migration-tool.md#bkmk_add_role).

## <a name="other-updates"></a>Altri aggiornamenti

A partire da questa versione, le funzionalità seguenti non sono più in [versione non definitiva](../../servers/manage/pre-release-features.md):

- [Individuazione dei gruppi utenti in Azure Active Directory](../../servers/deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco)<!--3611956-->
- [Sincronizzare i risultati di appartenenza alla raccolta con Azure Active Directory](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync)<!--3607475-->
- [Modalità autonoma per CMPivot](../../servers/manage/cmpivot.md#bkmk_standalone)<!--3555890/4692885-->
- [App client per dispositivi con co-gestione](../../../comanage/workloads.md#client-apps) (precedentemente note come *App per dispositivi mobili per dispositivi con co-gestione*)<!-- 1357892/3600959 -->

Per altre informazioni sulle modifiche apportate ai cmdlet di Windows PowerShell per Configuration Manager, vedere le [note sulla versione 2002 di PowerShell](https://docs.microsoft.com/powershell/sccm/2002-release-notes?view=sccm-ps).

Per altre informazioni sulle modifiche all'API REST del servizio di amministrazione, vedere le [note sulla versione del servizio di amministrazione](../../../develop/adminservice/release-notes.md#bkmk_2002).

A parte le nuove funzionalità, questa versione include anche ulteriori modifiche, ad esempio correzioni di bug. Per altre informazioni, vedere [Riepilogo delle modifiche in Configuration Manager Current Branch, versione 2002](https://support.microsoft.com/help/4556203).

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

<!-- At this time, version 2002 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-2002.md#early-update-ring). -->

A partire dall'11 maggio 2020 la versione 2002 è disponibile per l'installazione a livello globale da parte di tutti i clienti.

Al momento di installare questa versione, vedere [Installazione degli aggiornamenti per Configuration Manager](../../servers/manage/updates.md) ed [Elenco di controllo per l'installazione dell'aggiornamento 2002](../../servers/manage/checklist-for-installing-update-2002.md).

> [!TIP]
> Per installare un nuovo sito, usare una versione base di Configuration Manager.
>
> Sono disponibili altre informazioni su:
>
> - [Installing new sites](../../servers/deploy/install/installing-sites.md) (Installare nuovi siti)
> - [Baseline and update versions](../../servers/manage/updates.md#bkmk_Baselines) (Versioni di base e di aggiornamento)

Per problemi noti e importanti, vedere [Note sulla versione](../../servers/deploy/install/release-notes.md).

Dopo aver aggiornato un sito, vedere anche [Elenco di controllo post-aggiornamento](../../servers/manage/checklist-for-installing-update-2002.md#post-update-checklist).
