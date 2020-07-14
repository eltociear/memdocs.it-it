---
title: Riferimento ai file di log
titleSuffix: Configuration Manager
description: Riferimento di tutti i file di log per i componenti client, server e dipendenti di Configuration Manager.
ms.date: 07/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c1ff371e-b0ad-4048-aeda-02a9ff08889e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 296ac8448292b46318921cb952b5b8545a34f1fa
ms.sourcegitcommit: 3806a1850813b7a179d703e002bcc5c7eb1cb621
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/09/2020
ms.locfileid: "86210333"
---
# <a name="log-file-reference"></a>Riferimento ai file di log

*Si applica a: Configuration Manager (Current Branch)*

In Configuration Manager i componenti client e del server del sito registrano le informazioni di processo in singoli file di log. È possibile usare le informazioni contenute nei file di log per risolvere i problemi che potrebbero verificarsi. Per impostazione predefinita, la registrazione dei componenti client e server è abilitata in Configuration Manager.

Per informazioni più generali sui file di log in Configuration Manager, vedere [Informazioni sui file di log](about-log-files.md). L'articolo include informazioni sugli strumenti da usare, sulla configurazione dei log e sulla posizione in cui trovarli.

Nelle sezioni seguenti vengono fornite informazioni dettagliate sui diversi file di log disponibili. Monitorare i log dei client e dei server di Configuration Manager per ottenere maggiori dettagli sulle operazioni e visualizzare le informazioni sugli errori per la risoluzione di eventuali problemi.  

- [File di log del client](#BKMK_ClientLogs)  

  - [Operazioni client](#BKMK_ClientOpLogs)  

  - [Installazione client](#BKMK_ClientInstallLog)  

  - [Client per Linux e UNIX](#BKMK_LogFilesforLnU)  

  - [Client per computer Mac](#BKMK_LogfilesforMac)  

- [File di log del server](#BKMK_ServerLogs)  

  - [Server del sito e sistemi del sito](#BKMK_SiteSiteServerLog)  

  - [Installazione del server del sito](#BKMK_SiteInstallLog)

  - [Punto di servizio del data warehouse](#BKMK_DataWarehouse)

  - [Punto di stato di fallback](#BKMK_FSPLog)  

  - [Punto di gestione](#BKMK_MPLog)  

  - [Punto di connessione del servizio](#BKMK_WITLog)  

  - [Punto di aggiornamento software](#BKMK_SUPLog)  

- [File di log per funzionalità](#BKMK_FunctionLogs)  

  - [Gestione delle applicazioni](#BKMK_AppManageLog)  

  - [Asset Intelligence](#BKMK_AILog)  

  - [Backup e ripristino](#BKMK_BnRLog)  

  - [Registrazione certificato](#BKMK_CertificateEnrollment)

  - [Notifica client](#BKMK_BGB)

  - [Gateway di gestione cloud](#cloud-management-gateway)

  - [Impostazioni di conformità e accesso alle risorse aziendali](#BKMK_CompSettingsLog)  

  - [Console di Configuration Manager](#BKMK_ConsoleLog)  

  - [Gestione dei contenuti](#BKMK_ContentLog)  

  - [Desktop Analytics](#desktop-analytics)

  - [Individuazione](#BKMK_DiscoveryLog)  

  - [Analisi degli endpoint](#bkmk_analytics)
  
  - [Endpoint Protection](#BKMK_EPLog)  

  - [Estensioni](#BKMK_Extensions)  

  - [Inventario](#BKMK_InventoryLog)  

  - [Migrazione](#BKMK_MigrationLog)  

  - [Dispositivi mobili](#BKMK_MDMLog)  

  - [Distribuzione del sistema operativo](#BKMK_OSDLog)  

  - [Risparmio energia](#BKMK_PowerMgmtLog)  

  - [Controllo remoto](#BKMK_RCLog)  

  - [Creazione di report](#BKMK_ReportLog)  

  - [Amministrazione basata su ruoli](#BKMK_RBALog)  

  - [Controllo del software](#BKMK_MeteringLog)  

  - [Aggiornamenti software](#BKMK_SU_NAPLog)  

  - [Riattivazione LAN](#BKMK_WOLLog)  

  - [Manutenzione di Windows 10](#BKMK_WindowsServicingLog)

  - [Agente di Windows Update](#BKMK_WULog)  

  - [Server WSUS](#BKMK_WSUSLog)  

## <a name="client-log-files"></a><a name="BKMK_ClientLogs"></a> File di log del client

Nelle sezioni seguenti vengono elencati i file di log relativi alle operazioni client e all'installazione del client.  

### <a name="client-operations"></a><a name="BKMK_ClientOpLogs"></a> Operazioni client

Nella tabella seguente sono elencati i file di log individuati nel client di Configuration Manager.  

|Nome registro|Descrizione|  
|--------------|-----------------|  
|ADALOperationProvider.log|Informazioni sulle richieste di token di autenticazione client con Azure Active Directory (Azure AD) Authentication Library (ADAL).|
|BitLockerManagementHandler.log|Registra informazioni sui criteri di gestione di BitLocker.|
|CAS.log|Servizio di accesso ai contenuti. Gestisce la cache dei pacchetti locali sul client.|  
|Ccm32BitLauncher.log|Registra le azioni per l'avvio delle applicazioni sul client contrassegnate per *l'esecuzione a 32 bit*.|  
|CcmEval.log|Registra le attività di valutazione dello stato del client di Configuration Manager oltre a informazioni dettagliate per i componenti richiesti dal client di Configuration Manager.|  
|CcmEvalTask.log|Registra le attività di valutazione dello stato del client di Configuration Manager avviate dall'attività pianificata di valutazione.|  
|CcmExec.log|Registra le attività del client e del servizio host agenti di SMS. Questo file di log include anche informazioni sull'abilitazione e la disabilitazione del proxy di riattivazione.|  
|CcmMessaging.log|Registra le attività relative alle comunicazioni tra il client e i punti di gestione.|  
|CCMNotificationAgent.log|Registra le attività relative alle operazioni di notifica client.|  
|Ccmperf.log|Registra le attività di manutenzione e acquisizione dati correlate ai contatori delle prestazioni dei client.|  
|CcmRestart.log|Registra l'attività di riavvio del servizio client.|  
|CCMSDKProvider.log|Registra le attività per le interfacce dell'SDK client.|  
|ccmsqlce.log|Registra le attività per SQL Compact Edition usate dal client. Questo log viene in genere usato solo quando si abilita la registrazione di debug o in presenza di un problema con il componente. L'attività di integrità del client (ccmeval) in genere corregge autonomamente i problemi relativi a questo componente.|
|CertificateMaintenance.log|Gestisce i certificati per Servizi di dominio Active Directory e i punti di gestione.|  
|CIDownloader.log|Registra informazioni dettagliate sui download di definizioni di elementi di configurazione.|  
|CITaskMgr.log|Registra le attività per ogni applicazione e tipo di distribuzione, ad esempio download di contenuti e azioni di installazione o disinstallazione.|  
|ClientAuth.log|Registra l'attività di firma e autenticazione per il client.|  
|ClientIDManagerStartup.log|Crea e gestisce il GUID del client e identifica le attività durante l'assegnazione e la registrazione del client.|  
|ClientLocation.log|Registra le attività relative all'assegnazione del sito client.|  
|CMHttpsReadiness.log|Registra i risultati dell'esecuzione dello strumento per la preparazione della comunicazione HTTPS di Configuration Manager. Questo strumento consente di verificare se nei computer è presente un certificato di infrastruttura a chiave pubblica (PKI) per l'autenticazione client utilizzabile con Configuration Manager.|  
|CmRcService.log|Registra le informazioni per il servizio di controllo remoto.|  
|CoManagementHandler.log|Usare per risolvere i problemi di co-gestione nel client.|
|ContentTransferManager.log|Pianifica il Servizio trasferimento intelligente in background (BITS) o Server Message Block (SMB) per il download o per l'accesso ai pacchetti.|  
|DataTransferService.log|Registra tutte le comunicazioni BITS per l'accesso ai criteri o ai pacchetti.|  
|DeltaDownload.log|Registra le informazioni sul download di aggiornamenti rapidi e aggiornamenti scaricati con Ottimizzazione recapito.|  
|Diagnostics.log|Registra lo stato delle azioni di diagnostica del client.|
|EndpointProtectionAgent|Registra le informazioni sull'installazione del client di System Center Endpoint Protection e sull'applicazione di criteri antimalware in tale client.|  
|execmgr.log|Registra informazioni dettagliate sui pacchetti e sulle sequenze attività in esecuzione nel client.|  
|ExpressionSolver.log|Registra informazioni dettagliate sui metodi di rilevamento avanzati che vengono usati quando si attiva la registrazione debug o dettagliata.|  
|ExternalEventAgent.log|Registra la cronologia di rilevamento malware di Endpoint Protection e gli eventi relativi allo stato del client.|  
|FileBITS.log|Registra tutte le attività di accesso al pacchetto SMB.|  
|FileSystemFile.log|Registra l'attività del provider Strumentazione gestione Windows (WMI) per l'inventario software e la raccolta file.|  
|FSPStateMessage.log|Registra l'attività per i messaggi di stato inviati dal client al punto di stato di fallback.|  
|InternetProxy.log|Registra l'attività d'uso e configurazione proxy di rete per il client.|  
|InventoryAgent.log|Registra le attività di inventario hardware, inventario software e individuazione heartbeat sul client.|  
|LocationCache.log|Registra l'attività per l'uso e la gestione della cache per l'individuazione per il client.|  
|LocationServices.log|Registra l'attività del client per l'individuazione di punti di gestione, punti di aggiornamento software e punti di distribuzione.|  
|M365AHandler.log|Informazioni sui criteri relativi alle impostazioni di Desktop Analytics|
|MaintenanceCoordinator.log|Registra l'attività per le attività di manutenzione generale per il client.|  
|Mifprovider.log|Registra l'attività del provider WMI per i file MIF (Management Information Format).|  
|mtrmgr.log|Esegue il monitoraggio di tutti i processi di controllo software.|  
|PolicyAgent.log|Registra le richieste di criteri effettuate usando il servizio di trasferimento dei dati.|  
|PolicyAgentProvider.log|Registra le modifiche apportate ai criteri.|  
|PolicyEvaluator.log|Registra informazioni dettagliate sulla valutazione dei criteri nei computer client, inclusi quelli derivanti dagli aggiornamenti software.|  
|PolicyPlatformClient.log|Registra il processo di monitoraggio, aggiornamento e conformità per tutti i provider disponibili in \Program Files\Microsoft Policy Platform, fatta eccezione per il provider di file.|  
|PolicySdk.log|Registra le attività per le interfacce dell'SDK per il sistema dei criteri.|  
|Pwrmgmt.log|Registra le informazioni sull'attivazione o la disattivazione e la configurazione delle impostazioni client proxy di riattivazione.|  
|PwrProvider.log|Registra le attività del provider risparmio energia (PWRInvProvider) ospitato nel servizio WMI. In tutte le versioni supportate di Windows il provider enumera le impostazioni correnti sui computer durante l'inventario hardware e applica le impostazioni della combinazione per il risparmio di energia.|  
|SCClient_&lt;*dominio*\>@&lt;*nomeutente*\>_1.log|Registra l'attività in Software Center per l'utente specificato nel computer client.|  
|SCClient_&lt;*dominio*\>@&lt;*nomeutente*\>_2.log|Registra l'attività cronologica in Software Center per l'utente specificato nel computer client.|  
|Scheduler.log|Registra le attività delle attività pianificate per tutte le operazioni client.|  
|SCNotify_&lt;*dominio*\>@&lt;*nomeutente*\>_1.log|Registra l'attività per la notifica degli utenti riguardo al software per l'utente specificato.|  
|SCNotify_&lt;*dominio*\>@&lt;*nomeutente*\>_1-&lt;*data_ora*>.log|Registra le informazioni cronologiche per la notifica degli utenti riguardo al software per l'utente specificato.|
|SensorWmiProvider.log|Registra l'attività del provider WMI per il sensore di analisi degli endpoint.|
|SensorEndpoint.log|Registra l'esecuzione dei criteri di analisi degli endpoint e il caricamento dei dati client nel server del sito.|
|SensorManagedProvider.log|Registra la raccolta e l'elaborazione di eventi e informazioni per l'analisi degli endpoint.|
|setuppolicyevaluator.log|Registra la configurazione e la creazione dei criteri dell'inventario in WMI.|  
|SleepAgent_&lt;*dominio*\>@SYSTEM_0.log|File di log principale per il proxy di riattivazione.|  
|smscliui.log|Registra l'uso del client di Configuration Manager nel Pannello di controllo.|  
|SrcUpdateMgr.log|Registra l'attività per le applicazioni di Windows Installer installate che vengono aggiornate con i percorsi di origine per i punti di distribuzione correnti.|  
|StatusAgent.log|Registra i messaggi di stato creati dai componenti client.|  
|SWMTRReportGen.log|Genera un report dei dati d'uso raccolto dall'agente di controllo. Tali dati vengono registrati in Mtrmgr.log.|  
|UserAffinity.log|Registra informazioni dettagliate relative all'affinità utente dispositivo.|  
|VirtualApp.log|Registra informazioni specifiche per la valutazione dei tipi di distribuzione di Application Virtualization (App-V).|  
|Wedmtrace.log|Registra le operazioni relative ai filtri di scrittura sui client Windows Embedded.|  
|wakeprxy-install.log|Registra le informazioni di installazione quando i client ricevono l'opzione di impostazione client per attivare il proxy di riattivazione.|  
|wakeprxy-uninstall.log|Registra le informazioni sulla disinstallazione del proxy di riattivazione quando i client ricevono l'opzione di impostazione client per disattivare il proxy di riattivazione, se è stato precedentemente attivato.|  

### <a name="client-installation"></a><a name="BKMK_ClientInstallLog"></a> Installazione client

Nella tabella seguente sono elencati i file di log contenenti informazioni correlate all'installazione del client di Configuration Manager.  

|Nome registro|Descrizione|  
|--------------|-----------------|  
|ccmsetup.log|Registra le attività svolte da ccmsetup.exe per l'installazione, l'aggiornamento e la rimozione dei client. Può essere usato per la risoluzione dei problemi di installazione dei client.|  
|ccmsetup-ccmeval.log|Registra le attività svolte da ccmsetup.exe per lo stato del client e il monitoraggio e l'aggiornamento.|  
|CcmRepair.log|Registra le attività di ripristino dell'agente client.|  
|client.msi.log|Registra le attività di installazione eseguite da client.msi. Può essere usato per la risoluzione dei problemi di installazione o rimozione dei client.|  

### <a name="client-for-linux-and-unix"></a><a name="BKMK_LogFilesforLnU"></a> Client per Linux e UNIX

> [!Important]  
> A partire dalla versione 1902, Configuration Manager non supporta i client Linux o UNIX.
>
> Per la gestione dei server Linux, è possibile usare la gestione di Microsoft Azure. Le soluzioni di Azure includono un ampio supporto per Linux che nella maggior parte dei casi supera le funzionalità di Configuration Manager, inclusa la gestione end-to-end delle patch per Linux.

Il client di Configuration Manager per Linux e UNIX registra le informazioni nei file di log seguenti:  

> [!TIP]
> Usare CMTrace per visualizzare i file di log per i client Linux e UNIX.

|Nome registro|Dettagli|
|-------------------|-----------------------------------------------------------------|
|Scxcm.log| File di log per il servizio principale del client di Configuration Manager per Linux e UNIX (ccmexec.bin). Questo file di log contiene informazioni sull'installazione e le operazioni in corso di ccmexec.bin. Per impostazione predefinita, questo file di log è disponibile in **/var/opt/microsoft/scxcm.log**. Per cambiare il percorso del file di log, modificare **/opt/microsoft/configmgr/etc/scxcm.conf** e apportare le modifiche desiderate nel campo **PATH** . Non è necessario riavviare il servizio o il computer client per rendere effettive le modifiche. È possibile impostare il livello di registrazione scegliendo tra quattro diverse impostazioni. |
| Scxcmprovider.log |File di log per il servizio CIM del client di Configuration Manager per Linux e UNIX (omiserver.bin). Questo file di log contiene informazioni sulle operazioni in corso di nwserver.bin. Questo log si trova in `/var/opt/microsoft/configmgr/scxcmprovider.log`. Per cambiare il percorso del file di log, modificare **/opt/microsoft/omi/etc/scxcmprovider.conf** e apportare le modifiche desiderate nel campo **PATH** . Non è necessario riavviare il servizio o il computer client per rendere effettive le modifiche. È possibile impostare il livello di registrazione scegliendo fra tre impostazioni.|

Entrambi i file di log supportano diversi livelli di registrazione:  

- **scxcm.log**. Per impostare il livello di registrazione, modificare **/opt/microsoft/configmgr/etc/scxcm.conf** e sostituire ogni istanza del tag **MODULE** con il livello di registrazione desiderato:  

  - ERRORE: indica i problemi che richiedono attenzione  

  - AVVISO: indica i possibili problemi per le operazioni client  

  - INFORMAZIONI: registrazione dettagliata aggiuntiva, che indica lo stato di vari eventi nel client  

  - TRACCIA: registrazione dettagliata che viene generalmente usata per diagnosticare i problemi  

- **scxcmprovider.log**. Per impostare il livello di registrazione, modificare **/opt/microsoft/omi/etc/scxcmprovider.conf** e sostituire ogni istanza del tag **MODULE** con il livello di registrazione desiderato:  

  - ERRORE: indica i problemi che richiedono attenzione  

  - AVVISO: indica i possibili problemi per le operazioni client

  - INFORMAZIONI: registrazione dettagliata aggiuntiva, che indica lo stato di vari eventi nel client  

In condizioni operative normali, usare il livello di registrazione ERROR. Questo livello di registrazione crea il file di log più piccolo. Quando il livello di registrazione aumenta da ERROR a WARNING, INFO e infine a TRACE, viene creato un file di log più grande, poiché nel file viene scritta una quantità maggiore di dati.  

#### <a name="manage-log-files-for-the-linux-and-unix-client"></a><a name="BKMK_ManageLinuxLogs"></a> Gestire i file di log per i client Linux e UNIX

Il client per Linux e UNIX non limita la dimensione massima dei file di log. Il client non copia inoltre automaticamente il contenuto dei propri file con estensione log in un altro file, ad esempio un file con estensione lo_. Se si vuole controllare la dimensione massima dei file di log, implementare un processo per gestire i file di log indipendente dal client di Configuration Manager per Linux e UNIX.  

Ad esempio, è possibile usare il comando standard per Linux e UNIX **logrotate** per gestire la dimensione e la rotazione di file log dei client. Il client di Configuration Manager per Linux e UNIX dispone di un'interfaccia che consente a **logrotate** di segnalare al client il completamento della rotazione del log, in modo che il client possa riprendere la registrazione nel file di log.  

Per informazioni su **logrotate**, vedere la documentazione per le distribuzioni di Linux e UNIX in uso.  

### <a name="client-for-mac-computers"></a><a name="BKMK_LogfilesforMac"></a> Client per computer Mac

Il client di Configuration Manager per computer Mac registra le informazioni nei file di log seguenti nel computer Mac:  

|Nome registro|Dettagli|Percorso|
|--------------|-------------|-------------|
|CCMClient-&lt;*data_ora*>.log|Registra le attività correlate alle operazioni del client Mac, inclusi gestione delle applicazioni, inventario e registrazione degli errori.| `/Library/Application Support/Microsoft/CCM/Logs`|  
|CCMAgent-&lt;*data_ora*>.log|Registra le informazioni relative alle operazioni dei client, incluse le operazioni di accesso e disconnessione dell'utente, nonché l'attività del computer Mac.| `~/Library/Logs`|  
|CCMNotifications-&lt;*data_ora*>.log|Registra le attività correlate alle notifiche di Configuration Manager visualizzate nel computer Mac.| `~/Library/Logs`|  
|CCMPrefPane-&lt;*data_ora*>.log|Registra le attività correlate alla finestra di dialogo per le preferenze di Configuration Manager nel computer Mac, che include lo stato generale e la registrazione degli errori.| `~/Library/Logs`|  

Il file **SMS_DM.log** nel server di sistema del sito registra anche le comunicazioni tra i computer Mac e il punto di gestione configurato per i dispositivi mobili e i computer Mac.  

## <a name="server-log-files"></a><a name="BKMK_ServerLogs"></a> File di log del server

Nelle sezioni seguenti sono elencati i file di log disponibili nel server del sito o correlati a specifici ruoli del sistema del sito.  

### <a name="site-server-and-site-systems"></a><a name="BKMK_SiteSiteServerLog"></a> Server del sito e sistemi del sito

Nella tabella seguente sono elencati i file di log disponibili nel server del sito e nei server di sistema del sito di Configuration Manager.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|adctrl.log|Registra le attività di elaborazione delle registrazioni.|Server del sito|  
|ADForestDisc.log|Registra le azioni di individuazione foresta Active Directory.|Server del sito|  
|adminservice.log|Registra le azioni per l'API REST del servizio di amministrazione del provider SMS|Computer con il provider SMS|
|ADService.log|Registra i dettagli relativi alla creazione di account e ai gruppi di sicurezza in Active Directory.|Server del sito|  
|adsgdis.log|Registra le azioni di individuazione gruppo Active Directory.|Server del sito|  
|adsysdis.log|Registra le azioni di individuazione sistema Active Directory.|Server del sito|  
|adusrdis.log|Registra le azioni di individuazione utente Active Directory.|Server del sito|  
|BusinessAppProcessWorker.log|Registra l'elaborazione per le app di Microsoft Store per le aziende.|Server del sito|
|ccm.log|Registra le attività per l'installazione push client.|Server del sito|  
|CertMgr.log|Registra le attività relative ai certificati per le comunicazioni all'interno del sito.|Server del sistema del sito|  
|chmgr.log|Registra le attività della gestione dell'integrità client.|Server del sito|  
|Cidm.log|Registra le modifiche apportate alle impostazioni del client da Client Install Data Manager (CIDM).|Server del sito|  
|CollectionAADGroupSyncWorker.log | A partire dalla versione 2002, file di log per la sincronizzazione dei risultati di appartenenza alla raccolta con Azure Active Directory. Nella versione 1910 e nelle versioni precedenti la registrazione per questa funzionalità era combinata nel file SMS_AZUREAD_DISCOVERY_AGENT.log. | Server del sito|
|colleval.log|Registra dettagli sul momento in cui le raccolte vengono create, modificate ed eliminate dall'analizzatore di raccolte.|Server del sito|  
|compmon.log|Registra lo stato dei thread di componenti monitorati per il server del sito.|Server del sistema del sito|  
|compsumm.log|Registra le attività del Generatore riepilogo dello stato del componente.|Server del sito|  
|ComRegSetup.log|Registra l'installazione iniziale dei risultati di registrazione COM per un server del sito.|Server del sistema del sito|  
|dataldr.log|Registra le informazioni sull'elaborazione dei file MIF e dell'inventario hardware nel database di Configuration Manager.|Server del sito|  
|ddm.log|Registra le attività di Gestione individuazione dati.|Server del sito|  
|despool.log|Registra i trasferimenti delle comunicazioni in arrivo tra siti.|Server del sito|  
|distmgr.log|Registra informazioni dettagliate su creazione del pacchetto, compressione, replica differenziale e aggiornamenti delle informazioni. Può anche includere altre attività dal componente Distribution Manager. Ad esempio, l'installazione di un punto di distribuzione, i tentativi di connessione e l'installazione dei componenti. Per altre informazioni su altre funzionalità che usano questo log, vedere [Punto di connessione del servizio](#BKMK_WITLog) e [Distribuzione del sistema operativo](#BKMK_OSDLog).|Server del sito|  
|EPCtrlMgr.log|Registra le informazioni sulla sincronizzazione di informazioni relative a minacce di tipo malware dal server del ruolo del sistema del sito di Endpoint Protection con il database di Configuration Manager.|Server del sito|  
|EPMgr.log|Registra lo stato del ruolo del sistema del sito di Endpoint Protection.|Server del sistema del sito|  
|EPSetup.log|Fornisce informazioni sull'installazione del ruolo del sistema del sito di Endpoint Protection.|Server del sistema del sito|  
|EnrollSrv.log|Registra le attività relative al processo del servizio di registrazione.|Server del sistema del sito|  
|EnrollWeb.log|Registra le attività relative al processo del sito Web di registrazione.|Server del sistema del sito|  
|fspmgr.log|Registra le attività del ruolo del sistema del sito punto di stato di fallback.|Server del sistema del sito|  
|hman.log|Registra le informazioni sulle modifiche di configurazione del sito e sulla pubblicazione delle informazioni del sito in Servizi di dominio Active Directory.|Server del sito|  
|Inboxast.log|Registra i file che vengono spostati dal punto di gestione alla cartella INBOXES corrispondente nel server del sito.|Server del sito|  
|inboxmgr.log|Registra le attività di trasferimento file tra cartelle Posta in arrivo.|Server del sito|  
|inboxmon.log|Registra l'elaborazione dei file di Posta in arrivo e degli aggiornamenti del contatore delle prestazioni.|Server del sito|  
|invproc.log|Registra l'inoltro dei file MIF da un sito secondario al sito padre corrispondente.|Server del sito|  
|migmctrl.log|Registra informazioni per le azioni di migrazione riguardanti processi di migrazione, punti di distribuzione condivisi e aggiornamenti dei punti di distribuzione.|Sito principale della gerarchia di Configuration Manager e ogni sito primario figlio. In una gerarchia che include più siti primari, usare il file di log creato nel sito di amministrazione centrale.|  
|mpcontrol.log|Registra la registrazione del punto di gestione con WINS (Windows Internet Name Service). Registra la disponibilità del punto di gestione ogni 10 minuti.|Server del sistema del sito|  
|mpfdm.log|Registra le azioni del componente del punto di gestione che sposta i file client nella cartella INBOXES corrispondente nel server del sito.|Server del sistema del sito|  
|mpMSI.log|Registra informazioni dettagliate sull'installazione del punto di gestione.|Server del sito|  
|MPSetup.log|Registra il processo wrapper di installazione del punto di gestione.|Server del sito|  
|netdisc.log|Registra le azioni di individuazione della rete.|Server del sito|  
|NotiCtrl.log|Notifiche di richiesta dell'applicazione.|Server del sito|  
|ntsvrdis.log|Registra l'attività di individuazione dei server di sistema del sito.|Server del sito|  
|Objreplmgr|Registra l'elaborazione delle notifiche di modifica di oggetti per la replica.|Server del sito|  
|offermgr.log|Registra gli aggiornamenti degli annunci.|Server del sito|  
|offersum.log|Registra il riepilogo dei messaggi di stato di distribuzione.|Server del sito|  
|OfflineServicingMgr.log|Registra le attività di applicazione degli aggiornamenti ai file di immagine del sistema operativo.|Server del sito|  
|outboxmon.log|Registra l'elaborazione dei file di Posta in uscita e degli aggiornamenti del contatore delle prestazioni.|Server del sito|  
|PerfSetup.log|Registra i risultati dell'installazione di contatori delle prestazioni.|Server del sistema del sito|  
|PkgXferMgr.log|Registra le azioni del componente SMS_Executive, responsabile per l'invio di contenuto da un sito primario a un punto di distribuzione remoto.|Server del sito|  
|policypv.log|Registra gli aggiornamenti ai criteri del client per riflettere le modifiche apportate alle impostazioni o alle distribuzioni del client.|Server del sito primario|  
|rcmctrl.log|Registra le attività di replica database tra siti nella gerarchia.|Server del sito|  
|replmgr.log|Registra la replica di file tra i componenti server del sito e il componente di utilità di pianificazione.|Server del sito|  
|ResourceExplorer.log|Registra errori, avvisi e informazioni sull'esecuzione di Esplora inventario risorse.|Computer che esegue la console di Configuration Manager|  
|RESTPROVIDERSetup.log|Installazione dell'API REST del servizio di amministrazione del provider SMS|Computer con il provider SMS|
|ruleengine.log|Registra le informazioni dettagliate sulle regole di distribuzione automatica per l'identificazione, il download di contenuto e la creazione di gruppi di aggiornamento software e distribuzione.|Server del sito|  
|schedule.log|Registra informazioni dettagliate su processi e replica di file da sito a sito.|Server del sito|  
|sender.log|Registra i file trasferiti tra siti mediante la replica basata su file.|Server del sito|  
|sinvproc.log|Registra le informazioni sull'elaborazione dei dati di inventario del software nel database del sito.|Server del sito|  
|sitecomp.log|Registra informazioni dettagliate sulla manutenzione dei componenti sito installati in tutti i server di sistema del sito nel sito specifico.|Server del sito|  
|sitectrl.log|Registra le modifiche alle impostazioni del sito apportate agli oggetti di controllo sito nel database.|Server del sito|  
|sitestat.log|Registra il processo di monitoraggio di disponibilità e spazio su disco di tutti i sistemi del sito.|Server del sito|
|SMS_AZUREAD_DISCOVERY_AGENT.log| File di log per l'individuazione di utenti e gruppi di utenti di Azure Active Directory (Azure AD). Nella versione 1910 e versioni precedenti era inclusa anche la sincronizzazione dei risultati dell'appartenenza alla raccolta in Azure AD.| Server del sito|
|SMS_BUSINESS_APP_PROCESS_MANAGER.log|File di log per il componente che sincronizza le app da Microsoft Store per le aziende.|Server del sito|
|SMS_ISVUPDATES_SYNCAGENT.log| File di log per la sincronizzazione degli aggiornamenti software di terze parti.| Punto di aggiornamento software di livello superiore nella gerarchia di Configuration Manager.|
|SMS_OrchestrationGroup.log| File di log per i gruppi di orchestrazione|Server del sito|
|SMS_PhasedDeployment.log| File di log per distribuzioni in più fasi|Sito principale della gerarchia di Configuration Manager|
|SMS_REST_PROVIDER.log|Stato di integrità del servizio per l'API REST del servizio di amministrazione del provider SMS, incluse informazioni sui certificati|Computer con il provider SMS|
|SmsAdminUI.log|Registra l'attività della console di Configuration Manager.|Computer che esegue la console di Configuration Manager|  
|SMSAWEBSVCSetup.log|Registra le attività di installazione dei servizi Web del Catalogo applicazioni.|Server del sistema del sito|  
|smsbkup.log|Registra il risultato del processo di backup del sito.|Server del sito|  
|smsdbmon.log|Registra le modifiche apportate al database.|Server del sito|  
|SMSENROLLSRVSetup.log|Registra le attività di installazione dei servizi Web di registrazione.|Server del sistema del sito|  
|SMSENROLLWEBSetup.log|Registra le attività di installazione del sito Web di registrazione.|Server del sistema del sito|  
|smsexec.log|Registra l'elaborazione di tutti i thread di componenti del server del sito.|Server del sito o sistema di server del sito|  
|SMSFSPSetup.log|Registra i messaggi generati dall'installazione di un punto di stato di fallback.|Server del sistema del sito|  
|SMSPORTALWEBSetup.log|Registra le attività di installazione del sito Web del Catalogo applicazioni.|Server del sistema del sito|  
|SMSProv.log|Registra gli accessi del provider WMI al database del sito.|Computer con il provider SMS|  
|srsrpMSI.log|Registra i risultati dettagliati del processo di installazione del punto di reporting dall'output MSI.|Server del sistema del sito|  
|srsrpsetup.log|Registra i risultati del processo di installazione del punto di reporting.|Server del sistema del sito|  
|statesys.log|Registra l'elaborazione dei messaggi di sistema di stato.|Server del sito|  
|statmgr.log|Registra la scrittura di tutti i messaggi di stato nel database.|Server del sito|  
|swmproc.log|Registra l'elaborazione di file e impostazioni di controllo.|Server del sito|
|UXAnalyticsUploadWorker.log|Registra il caricamento dei dati nel servizio per l'analisi degli endpoint.|Server del sito|   

### <a name="site-server-installation"></a><a name="BKMK_SiteInstallLog"></a> Installazione del server del sito

Nella tabella seguente sono elencati i file di log contenenti informazioni relative all'installazione del sito.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|ConfigMgrPrereq.log|Registra le attività di valutazione e installazione dei componenti dei prerequisiti.|Server del sito|  
|ConfigMgrSetup.log|Registra l'output dettagliato dell'installazione del server del sito.|Server del sito|  
|ConfigMgrSetupWizard.log|Registra le informazioni relative all'attività nell'Installazione guidata.|Server del sito|  
|SMS_BOOTSTRAP.log|Registra le informazioni sullo stato di avanzamento dell'avvio del processo di installazione del sito secondario. I dettagli del processo di configurazione effettivo sono contenuti in ConfigMgrSetup.log.|Server del sito|  
|smstsvc.log|Registra le informazioni sull'installazione, sull'uso e sulla rimozione di un servizio Windows. Windows usa questo servizio per testare la connettività di rete e le autorizzazioni tra i server. Usa l'account computer del server che crea la connessione.|Server del sito e del server di sistema del sito|  

### <a name="data-warehouse-service-point"></a><a name="BKMK_DataWarehouse"></a> Punto di servizio del data warehouse

Nella tabella seguente sono elencati i file di log contenenti informazioni correlate al punto di servizio del data warehouse.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|DWSSMSI.log|Registra i messaggi generati dall'installazione di un punto di servizio del data warehouse.|Server del sistema del sito|  
|DWSSSetup.log|Registra i messaggi generati dall'installazione di un punto di servizio del data warehouse.|Server del sistema del sito|  
|Microsoft.ConfigMgrDataWarehouse.log|Registra le informazioni sulla sincronizzazione dei dati tra il database del sito e il database del data warehouse.|Server del sistema del sito|  

### <a name="fallback-status-point"></a><a name="BKMK_FSPLog"></a> Punto di stato di fallback

Nella tabella seguente sono elencati i file di log contenenti informazioni correlate al punto di stato di fallback.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|FspIsapi|Registra le comunicazioni verso il punto di stato di fallback da client legacy di dispositivi mobili e da computer client.|Server del sistema del sito|  
|fspMSI.log|Registra i messaggi generati dall'installazione di un punto di stato di fallback.|Server del sistema del sito|  
|fspmgr.log|Registra le attività del ruolo del sistema del sito punto di stato di fallback.|Server del sistema del sito|  

### <a name="management-point"></a><a name="BKMK_MPLog"></a> Punto di gestione

Nella tabella seguente sono elencati i file di log contenenti informazioni correlate al punto di gestione.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|CcmIsapi.log|Registra l'attività di messaggistica client sull'endpoint.|Server del sistema del sito|
|CCM_STS.log|Registra le attività per i token di autenticazione, dai token di Azure Active Directory o dai token client emessi dal sito.|Server del sistema del sito|
|ClientAuth.log|Registra l'attività di firma e autenticazione.|Server del sistema del sito|
|MP_CliReg.log|Registra l'attività di registrazione del client elaborata dal punto di gestione.|Server del sistema del sito|  
|MP_Ddr.log|Registra la conversione di record XML.ddr dai client e quindi li copia nel server del sito.|Server del sistema del sito|  
|MP_Framework.log|Registra le attività del punto di gestione principale e dei componenti del framework client.|Server del sistema del sito|  
|MP_GetAuth.log|Registra le attività di autorizzazione del client.|Server del sistema del sito|  
|MP_GetPolicy.log|Registra le attività di richiesta di criteri dai computer client.|Server del sistema del sito|  
|MP_Hinv.log|Registra informazioni dettagliate sulla conversione di record di inventario hardware XML dai client e sulla copia di tali file nel server del sito.|Server del sistema del sito|  
|MP_Location.log|Registra le attività di richiesta per il percorso e di risposta dai client.|Server del sistema del sito|  
|MP_OOBMgr.log|Registra le attività del punto di gestione correlate alla ricezione di un OTP da un client.|Server del sistema del sito|  
|MP_Policy.log|Registra la comunicazione dei criteri.|Server del sistema del sito|  
|MP_RegistrationManager.log|Registra le attività correlate alla registrazione del client, ad esempio la convalida di certificati, CRL e token.|Server del sistema del sito|
|MP_Relay.log|Registra il trasferimento di file che vengono raccolti dal client.|Server del sistema del sito|  
|MP_Retry.log|Registra i processi di nuovi tentativi di inventario hardware.|Server del sistema del sito|  
|MP_Sinv.log|Registra informazioni dettagliate sulla conversione di record di inventario software XML dai client e sulla copia di tali file nel server del sito.|Server del sistema del sito|  
|MP_SinvCollFile.log|Registra informazioni dettagliate sulla raccolta di file.|Server del sistema del sito|  
|MP_Status.log|Registra informazioni dettagliate sulla conversione di file di messaggi di stato XML.svf dai client e sulla copia di tali file nel server del sito.|Server del sistema del sito|
|mpcontrol.log|Registra la registrazione del punto di gestione con WINS. Registra la disponibilità del punto di gestione ogni 10 minuti.|Server del sito|  
|mpfdm.log|Registra le azioni del componente del punto di gestione che sposta i file client nella cartella INBOXES corrispondente nel server del sito.|Server del sistema del sito|  
|mpMSI.log|Registra informazioni dettagliate sull'installazione del punto di gestione.|Server del sito|  
|MPSetup.log|Registra il processo wrapper di installazione del punto di gestione.|Server del sito|  
|UserService.log|Registra le richieste degli utenti da Software Center per il recupero e/o l'installazione di applicazioni disponibili per gli utenti dal server.|Server del sistema del sito|

### <a name="service-connection-point"></a><a name="BKMK_WITLog"></a> Punto di connessione del servizio

La tabella seguente elenca i file di log contenenti informazioni correlate al punto di connessione del servizio.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|CertMgr.log|Registra informazioni sul certificato e sull'account proxy.|Server del sito|  
|CollEval.log|Registra dettagli sul momento in cui le raccolte vengono create, modificate ed eliminate dall'analizzatore di raccolte.|Sito primario e sito di amministrazione centrale|  
|Cloudusersync.log|Registra l'attivazione della licenza per gli utenti.|Computer con il punto di connessione del servizio|  
|Dataldr.log|Registra informazioni sull'elaborazione dei file MIF.|Server del sito|  
|ddm.log|Registra le attività di Gestione individuazione dati.|Server del sito|  
|distmgr.log|Registra informazioni dettagliate sulle richieste di distribuzione del contenuto.|Server del sito principale|  
|Dmpdownloader.log|Registra informazioni dettagliate sui download da Microsoft Intune.|Computer con il punto di connessione del servizio|  
|Dmpuploader.log|Registra informazioni dettagliate sul caricamento delle modifiche del database in Microsoft Intune.|Computer con il punto di connessione del servizio|  
|hman.log|Registra informazioni sull'inoltro dei messaggi.|Server del sito|  
|MSfBSyncWorker.log|Registra informazioni sulle comunicazioni con Microsoft Store per le aziende.|Computer con il punto di connessione del servizio|
|objreplmgr.log|Registra l'elaborazione di criteri e assegnazione.|Server del sito primario|  
|PolicyPV.log|Registra la generazione di tutti i criteri.|Server del sito|  
|outgoingcontentmanager.log|Registra il contenuto caricato in Microsoft Intune.|Computer con il punto di connessione del servizio|  
|ServiceConnectionTool.log|Registra informazioni dettagliate sull'uso dello [strumento di connessione del servizio](../../servers/manage/use-the-service-connection-tool.md) in base al parametro usato. Ogni volta che si esegue lo strumento, qualsiasi file di log esistente viene sostituito.|Stesso percorso dello strumento|
|Sitecomp.log|Registra informazioni dettagliate sull'installazione del punto di connessione del servizio.|Server del sito|  
|SmsAdminUI.log|Registra l'attività della console di Configuration Manager.|Computer che esegue la console di Configuration Manager|  
|SMS_CLOUDCONNECTION.log|Registra informazioni sui servizi cloud.|Computer con il punto di connessione del servizio|
|Smsprov.log|Registra le attività del provider SMS. Le attività della console di Configuration Manager usano il provider SMS.|Computer con il provider SMS|  
|SrvBoot.log|Registra informazioni dettagliate sul servizio di installazione del punto di connessione del servizio.|Computer con il punto di connessione del servizio|  
|Statesys.log|Registra l'elaborazione dei messaggi di gestione dei dispositivi mobili.|Sito primario e sito di amministrazione centrale|  

### <a name="software-update-point"></a><a name="BKMK_SUPLog"></a> Punto di aggiornamento software

Nella tabella seguente sono elencati i file di log contenenti informazioni correlate al punto di aggiornamento software.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|objreplmgr.log|Registra informazioni dettagliate sulla replica di file di notifica di aggiornamenti software da un sito padre ai siti figlio.|Server del sito|  
|PatchDownloader.log|Registra informazioni dettagliate sul processo di download degli aggiornamenti software dall'origine degli aggiornamenti alla destinazione del download sul server del sito.|Quando si scaricano manualmente gli aggiornamenti, questo file è presente nella directory `%temp%` del computer in cui si usa la console. Per le regole di distribuzione automatica, se il client di Configuration Manager è installato nel server del sito, questo file si trova nel server del sito in `%windir%\CCM\Logs`.|  
|ruleengine.log|Registra le informazioni dettagliate sulle regole di distribuzione automatica per l'identificazione, il download di contenuto e la creazione di gruppi di aggiornamento software e distribuzione.|Server del sito|
|SMS_ISVUPDATES_SYNCAGENT.log| File di log per la sincronizzazione degli aggiornamenti software di terze parti.| Punto di aggiornamento software di livello superiore nella gerarchia di Configuration Manager.|
|SUPSetup.log|Registra informazioni dettagliate sull'installazione del punto di aggiornamento software. Al termine dell'installazione del punto di aggiornamento software, **Installation was successful** viene scritto nel file di log.|Server del sistema del sito|  
|WCM.log|Registra informazioni dettagliate sulla configurazione del punto di aggiornamento software e sulle connessioni al server WSUS per categorie di aggiornamento, classificazioni e lingue sottoscritte.|Server del sito che si connette al server WSUS|  
|WSUSCtrl.log|Registra informazioni dettagliate su configurazione, connettività al database e integrità del server WSUS per il sito.|Server del sistema del sito|  
|wsyncmgr.log|Registra informazioni dettagliate sul processo di sincronizzazione degli aggiornamenti software.|Server del sistema del sito|  
|WUSSyncXML.log|Registra informazioni dettagliate sullo strumento di inventario per il processo di sincronizzazione di Microsoft Update.|Computer client configurato come host di sincronizzazione per lo strumento di inventario per Microsoft Update|  


## <a name="log-files-by-functionality"></a><a name="BKMK_FunctionLogs"></a> File di log per funzionalità

Nelle sezioni seguenti sono elencati i file di log correlati alle funzioni di Configuration Manager.  

### <a name="application-management"></a><a name="BKMK_AppManageLog"></a> Gestione delle applicazioni

Nella tabella seguente sono elencati i file di log contenenti informazioni correlate alla gestione delle applicazioni.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|AppIntentEval.log|Registra informazioni dettagliate sullo stato corrente e previsto delle applicazioni, sulla relativa applicabilità, sulla soddisfazione dei requisiti, sui tipi di distribuzione e sulle dipendenze.|Client|  
|AppDiscovery.log|Registra informazioni dettagliate sull'individuazione o sul rilevamento di applicazioni nei computer client.|Client|  
|AppEnforce.log|Registra informazioni dettagliate sulle azioni di imposizione (installazione e disinstallazione) eseguite per applicazioni sul client.|Client|  
|AppGroupHandler.log|A partire dalla versione 1906, informazioni relative al rilevamento e all'imposizione per i gruppi di applicazioni|Client|
|awebsctl.log|Registra le attività di monitoraggio per il ruolo del sistema del sito punto per servizi Web del Catalogo applicazioni.|Server del sistema del sito|  
|awebsvcMSI.log|Registra informazioni di installazione dettagliate per il ruolo del sistema del sito punto per servizi Web del Catalogo applicazioni.|Server del sistema del sito|  
|BusinessAppProcessWorker.log|Registra l'elaborazione per le app di Microsoft Store per le aziende.|Server del sito|
|Ccmsdkprovider.log|Registra le attività di SDK di gestione applicazioni.|Client|  
|colleval.log|Registra dettagli sul momento in cui le raccolte vengono create, modificate ed eliminate dall'analizzatore di raccolte.|Server del sistema del sito|  
|ConfigMgrSoftwareCatalog.log|Registra l'attività del Catalogo applicazioni, che include l'utilizzo di Silverlight.|Client|  
|MSfBSyncWorker.log|Registra informazioni sulle comunicazioni con Microsoft Store per le aziende.|Computer con il punto di connessione del servizio|
|NotiCtrl.log|Notifiche di richiesta dell'applicazione.|Server del sito|  
|portlctl.log|Registra le attività di monitoraggio per il ruolo del sistema del sito punto per siti Web del Catalogo applicazioni.|Server del sistema del sito|  
|portlwebMSI.log|Registra l'attività di installazione MSI per il ruolo del sito Web del Catalogo applicazioni.|Server del sistema del sito|  
|PrestageContent.log|Registra informazioni dettagliate sull'uso dello strumento ExtractContent.exe in un punto di distribuzione pre-installazione remoto. Questo strumento consente di estrarre contenuto che è stato esportato in un file.|Server del sistema del sito|  
|ServicePortalWebService.log|Registra le attività di installazione dei servizi Web del Catalogo applicazioni.|Server del sistema del sito|  
|ServicePortalWebSite.log|Registra le attività del sito Web del Catalogo applicazioni.|Server del sistema del sito|  
|SettingsAgent.log|Imposizione di applicazioni specifiche, registra l'orchestrazione della valutazione del gruppo di applicazioni e i dettagli dei criteri di co-gestione.|Client|
|SMS_BUSINESS_APP_PROCESS_MANAGER.log|File di log per il componente che sincronizza le app da Microsoft Store per le aziende.|Server del sito|
|SMS_CLOUDCONNECTION.log|Registra informazioni sui servizi cloud.|Computer con il punto di connessione del servizio|
|SMSdpmon.log|Registra informazioni dettagliate sulle attività pianificate di monitoraggio dell'integrità del punto di distribuzione configurate su un punto di distribuzione.|Server del sito|  
|SoftwareCatalogUpdateEndpoint.log|Registra le attività per la gestione di URL per il Catalogo di applicazioni indicato in Software Center.|Client|  
|SoftwareCenterSystemTasks.log|Registra le attività correlate alla convalida dei componenti dei prerequisiti di Software Center.|Client|  
|TSDTHandler.log|Per il tipo di distribuzione della sequenza di attività. Registra il processo dall'imposizione dell'app (installazione o disinstallazione) all'avvio della sequenza di attività. Usare con AppEnforce.log e smsts.log.|Client|<!-- MEMDocs#336 -->

#### <a name="packages-and-programs"></a>Pacchetti e programmi

La tabella seguente elenca i file di log contenenti informazioni correlate alla distribuzione di pacchetti e programmi.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|colleval.log|Registra dettagli sul momento in cui le raccolte vengono create, modificate ed eliminate dall'analizzatore di raccolte.|Server del sito|  
|execmgr.log|Registra informazioni dettagliate sui pacchetti e sulle sequenze attività in esecuzione.|Client|  

### <a name="asset-intelligence"></a><a name="BKMK_AILog"></a> Asset Intelligence

Nella tabella seguente sono elencati i file di log contenenti informazioni correlate ad Asset Intelligence.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|AssetAdvisor.log|Registra le attività delle operazioni di inventario di Asset Intelligence.|Client|  
|aikbmgr.log|Registra informazioni dettagliate sull'elaborazione di file XML da Posta in arrivo per l'aggiornamento del catalogo di Asset Intelligence.|Server del sito|  
|AIUpdateSvc.log|Registra l'interazione del punto di sincronizzazione di Asset Intelligence con il servizio cloud.|Server del sistema del sito|  
|AIUSMSI.log|Registra informazioni dettagliate sull'installazione del ruolo del sistema del sito punto di sincronizzazione di Asset Intelligence.|Server del sistema del sito|  
|AIUSSetup.log|Registra informazioni dettagliate sull'installazione del ruolo del sistema del sito punto di sincronizzazione di Asset Intelligence.|Server del sistema del sito|  
|ManagedProvider.log|Registra informazioni dettagliate sull'individuazione di software con tag di identificazione software associato. Registra inoltre le attività correlate all'inventario hardware.|Server del sistema del sito|  
|MVLSImport.log|Registra informazioni dettagliate sull'elaborazione di file di licenza importati.|Server del sistema del sito|  

### <a name="backup-and-recovery"></a><a name="BKMK_BnRLog"></a> Backup e ripristino

Nella tabella seguente sono elencati i file di log contenenti informazioni correlate ad azioni di backup e ripristino, incluse le reimpostazioni di siti e le modifiche apportate al provider SMS.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|ConfigMgrSetup.log|Registra informazioni sulle attività di impostazione e ripristino quando Configuration Manager ripristina un sito dal backup.|Server del sito|  
|Smsbkup.log|Registra informazioni dettagliate sulle attività di backup del sito.|Server del sito|  
|smssqlbkup.log|Registra l'output proveniente dal processo di backup del database del sito quando SQL Server è installato in un server che non è il server del sito.|Server di database del sito|  
|Smswriter.log|Registra informazioni sullo stato del writer VSS di Configuration Manager usato dal processo di backup.|Server del sito|  

### <a name="certificate-enrollment"></a><a name="BKMK_CertificateEnrollment"></a> Registrazione certificato

Nella tabella seguente sono elencati i file di log di Configuration Manager contenenti informazioni correlate alla registrazione dei certificati. Registrazione certificato usa il punto di registrazione certificati e il modulo criteri di Configuration Manager nel server che esegue il servizio Registrazione dispositivi di rete (NDES).  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|Crp.log|Registra le attività di registrazione.|Punto di registrazione certificati|  
|Crpctrl.log|Registra l'integrità operativa del punto di registrazione certificati.|Punto di registrazione certificati|  
|Crpsetup.log|Registra le informazioni sull'installazione e la configurazione del punto di registrazione certificati.|Punto di registrazione certificati|  
|Crpmsi.log|Registra le informazioni sull'installazione e la configurazione del punto di registrazione certificati.|Punto di registrazione certificati|  
|NDESPlugin.log|Registra le attività di richiesta di verifica e registrazione dei certificati.|Modulo criteri di Configuration Manager e servizio Registrazione dispositivi di rete|  

Oltre ai file di log di Configuration Manager, esaminare i registri applicazione di Windows in Visualizzatore eventi nel server che esegue il servizio Registrazione dispositivi di rete e nel server che ospita il punto di registrazione certificati. Ad esempio, cercare i messaggi provenienti dall'origine **ServizioRegistrazioneDispositiviDiRete** .

È inoltre possibile usare i seguenti file di log:  

- File di log di IIS per il servizio Registrazione dispositivi di rete: **%SYSTEMDRIVE%\inetpub\logs\LogFiles\W3SVC1**  

- File di log di IIS per il punto di registrazione certificati: **%SYSTEMDRIVE%\inetpub\logs\LogFiles\W3SVC1**  

- File di log criteri di registrazione dispositivi di rete: **mscep.log**  

    > [!NOTE]  
    > Questo file si trova nella cartella per il profilo dell'account NDES, ad esempio, in C:\Utenti\SCEPSvc. Per altre informazioni su come abilitare la registrazione NDES, vedere la sezione [Enable Logging](https://social.technet.microsoft.com/wiki/contents/articles/9063.active-directory-certificate-services-ad-cs-network-device-enrollment-service-ndes.aspx#Enable_Logging) (Abilitare la registrazione) del wiki dedicato a NDES.  

### <a name="client-notification"></a><a name="BKMK_BGB"></a> Notifica client

Nella tabella seguente sono elencati i file di log contenenti informazioni relative alla notifica client.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|bgbmgr.log|Registra informazioni dettagliate sulle attività del server del sito relative ad attività di notifica client e all'elaborazione di file online e file di stato delle attività.|Server del sito|  
|BGBServer.log|Registra le attività del server di notifica, ad esempio le comunicazioni client-server e il push delle attività ai client. Registra inoltre informazioni sulla generazione di file di stato attività e online da inviare al server del sito.|Punto di gestione|  
|BgbSetup.log|Registra le attività del processo wrapper di installazione del server di notifica durante l'installazione e la disinstallazione.|Punto di gestione|  
|bgbisapiMSI.log|Registra informazioni dettagliate sull'installazione e sulla disinstallazione del server di notifica.|Punto di gestione|  
|BgbHttpProxy.log|Registra le attività del proxy HTTP di notifica durante l'inoltro dei messaggi dei client tramite HTTP verso e dal server di notifica.|Client|  
|CcmNotificationAgent.log|Registra le attività dell'agente di notifica, ad esempio le comunicazioni tra client e server e le informazioni sulle attività ricevute e inviate ad altri agenti client.|Client|  

### <a name="cloud-management-gateway"></a>Gateway di gestione cloud

Nella tabella seguente sono elencati i file di log contenenti informazioni correlate al gateway di gestione cloud.

|Nome registro|Descrizione|Computer con file di log|
|--------------|-----------------|----------------------------|  
|CloudMgr.log|Registra informazioni dettagliate sulla distribuzione del servizio gateway di gestione cloud, lo stato del servizio in corso e i dati d'uso associati al servizio. Per configurare il livello di registrazione, modificare il valore **Livello di registrazione** nella chiave del Registro di sistema seguente: `HKLM\SOFTWARE\ Microsoft\SMS\COMPONENTS\ SMS_CLOUD_ SERVICES_MANAGER`|La cartella *installdir* del server del sito primario o di CAS.|
|CMGSetup.log <sup>[Nota 1](#bkmk_note1)</sup>|Registra informazioni dettagliate sulla seconda fase della distribuzione di Cloud Management Gateway (distribuzione locale in Azure). Per configurare il livello di registrazione, usare l'impostazione **Livello di traccia** (**Informazioni** per impostazione predefinita, **Dettagliato**, **Errore**) nella scheda di **configurazione dei servizi cloud nel portale di Azure**.|Cartella **%approot%\logs** sul server di Azure o cartella SMS/Logs nel server del sistema del sito|
|CMGService.log <sup>[Nota 1](#bkmk_note1)</sup>|Registra informazioni dettagliate sul componente di base del servizio Cloud Management Gateway in Azure. Per configurare il livello di registrazione, usare l'impostazione **Livello di traccia** (**Informazioni** per impostazione predefinita, **Dettagliato**, **Errore**) nella scheda di **configurazione dei servizi cloud nel portale di Azure**.|Cartella **%approot%\logs** sul server di Azure o cartella SMS/Logs nel server del sistema del sito|
|SMS_Cloud_ProxyConnector.log|Registra informazioni dettagliate sull'impostazione di connessioni tra il servizio gateway di gestione cloud e il punto di connessione al gateway di gestione cloud.|Server del sistema del sito|
|CMGContentService.log <sup>[Nota 1](#bkmk_note1)</sup>|<!--SCCMDocs-pr issue #2822-->Quando si abilita un CMG perché trasferisca contenuto dall'archiviazione di Azure, questo log registra i dettagli di tale servizio.|Cartella **%approot%\logs** sul server di Azure o cartella SMS/Logs nel server del sistema del sito|

- Per la risoluzione dei problemi relativi alle distribuzioni, usare **CloudMgr.log** e **CMGSetup.log**
- Per la risoluzione dei problemi relativi all'integrità del servizio, usare **CMGService.log** e **SMS_Cloud_ProxyConnector.log**.
- Per la risoluzione dei problemi relativi al traffico client, usare **CMGHttpHandler.log**, **CMGService.log** e **SMS_Cloud_ProxyConnector.log**.

#### <a name="note-1-logs-synchronized-from-azure"></a><a name="bkmk_note1"></a> Nota 1: Log sincronizzati da Azure

Si tratta di file di log locali di Configuration Manager che il componente di gestione del servizio cloud sincronizza dall'archiviazione di Azure ogni cinque minuti. Il gateway di gestione cloud effettua il push dei log ad Archiviazione di Azure ogni cinque minuti. Il ritardo massimo è quindi di 10 minuti. Le opzioni di tipo Dettagliato hanno effetto sia sui log locali che su quelli remoti. I nomi dei file includono il nome del servizio e l'identificatore dell'istanza del ruolo. Ad esempio, CMG -*ServiceName*-*RoleInstanceID*-CMGSetup.log

### <a name="compliance-settings-and-company-resource-access"></a><a name="BKMK_CompSettingsLog"></a> Impostazioni di conformità e accesso alle risorse aziendali

Nella tabella seguente sono elencati i file di registro contenenti informazioni relative alle impostazioni di conformità e all'accesso alle risorse aziendali.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|CIAgent.log|Registra informazioni dettagliate sul processo di monitoraggio e aggiornamento e conformità per impostazioni di conformità, aggiornamenti software e gestione applicazioni.|Client|  
|CITaskManager.log|Registra le informazioni sulla pianificazione della attività degli elementi di configurazione.|Client|  
|DCMAgent.log|Registra le informazioni di alto livello su valutazione, segnalazione dei conflitti e monitoraggio e aggiornamento di applicazioni ed elementi di configurazione.|Client|  
|DCMReporting.log|Registra le informazioni relative al reporting dei risultati della piattaforma criteri in messaggi di stato per gli elementi di configurazione.|Client|  
|DcmWmiProvider.log|Registra le informazioni sulla lettura dei synclet degli elementi di configurazione da WMI.|Client|  

### <a name="configuration-manager-console"></a><a name="BKMK_ConsoleLog"></a> Console di Configuration Manager

Nella tabella seguente sono elencati i file di log contenenti informazioni correlate alla console di Configuration Manager.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|ConfigMgrAdminUISetup.log|Registra l'installazione della console di Configuration Manager.|Computer che esegue la console di Configuration Manager|  
|SmsAdminUI.log|Registra informazioni sul funzionamento della console di Configuration Manager.|Computer che esegue la console di Configuration Manager|  
|Smsprov.log|Registra le attività del provider SMS. Le attività della console di Configuration Manager usano il provider SMS.|Server del sito o sistema di server del sito|  

### <a name="content-management"></a><a name="BKMK_ContentLog"></a> Gestione dei contenuti

Nella tabella seguente sono elencati i file di log contenenti informazioni correlate alla gestione dei contenuti.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|CloudDP-&lt;guid\>.log|Registra informazioni dettagliate per un punto di distribuzione specifico basato sul cloud, incluse le informazioni sull'archivio e l'accesso ai contenuti.|Server del sistema del sito|  
|CloudMgr.log|Registra informazioni dettagliate sul provisioning dei contenuti, raccogliendo statistiche sull'archiviazione e la larghezza di banda e azioni avviate dall'amministratore per interrompere o avviare il servizio cloud che esegue un punto di distribuzione basato su cloud.|Server del sistema del sito|  
|DataTransferService.log|Registra tutte le comunicazioni BITS per l'accesso ai criteri o ai pacchetti. Questo registro viene usato anche per la gestione dei contenuti per i punti di distribuzione pull.|Computer configurato come punto di distribuzione pull|  
|PullDP.log|Registra informazioni dettagliate sul contenuto che il punto di distribuzione pull trasferisce dai punti di distribuzione di origine.|Computer configurato come punto di distribuzione pull|  
|PrestageContent.log|Registra informazioni dettagliate sull'uso dello strumento ExtractContent.exe in un punto di distribuzione pre-installazione remoto. Questo strumento consente di estrarre contenuto che è stato esportato in un file.|Ruolo del sistema del sito|  
|SMSdpmon.log|Registra informazioni dettagliate sulle attività pianificate di monitoraggio dell'integrità del punto di distribuzione configurate su un punto di distribuzione.|Ruolo del sistema del sito|  
|smsdpprov.log|Registra informazioni dettagliate sull'estrazione di file compressi ricevuti da un sito primario. Questo registro viene generato dal provider WMI del punto di distribuzione remoto.|Computer di punto di distribuzione che non condivide il percorso con il server del sito|  
|smsdpusage.log|Registra informazioni dettagliate su smsdpusage.exe che viene eseguito e raccoglie i dati per il report di riepilogo di utilizzo dei punti di distribuzione.|Ruolo del sistema del sito|  

### <a name="desktop-analytics"></a>Desktop Analytics

Usare i file di log seguenti per risolvere i problemi relativi a Desktop Analytics integrato con Configuration Manager.

I file di log nel punto di connessione del servizio si trovano nella directory seguente: `%ProgramFiles%\Configuration Manager\Logs\M365A`.
I file di log nel client di Configuration Manager si trovano nella directory seguente: `%WinDir%\CCM\logs`.

| Registro | Descrizione |Computer con file di log|
|---------|---------|---------|
| M365ADeploymentPlanWorker.log | Informazioni sulla sincronizzazione del piano di distribuzione dal servizio cloud Desktop Analytics a un'istanza locale di Configuration Manager |punto di connessione del servizio|
| M365ADeviceHealthWorker.log | Informazioni sul caricamento dell'Integrità dispositivi da Configuration Manager al cloud Microsoft |punto di connessione del servizio|
| M365AHandler.log | Informazioni sui criteri relativi alle impostazioni di Desktop Analytics |Client|
| M365AUploadWorker.log | Informazioni sul caricamento di raccolte e dispositivi da Configuration Manager al cloud Microsoft |punto di connessione del servizio|
| SmsAdminUI.log | Informazioni sulle attività della console di Configuration Manager, come la configurazione dei servizi cloud di Azure  |punto di connessione del servizio|

### <a name="discovery"></a><a name="BKMK_DiscoveryLog"></a> Individuazione

Nella tabella seguente sono elencati i file di log contenenti informazioni relative all'individuazione.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|adsgdis.log|Registra le azioni di Individuazione gruppo di protezione Active Directory.|Server del sito|  
|adsysdis.log|Registra le azioni di individuazione sistema Active Directory.|Server del sito|  
|adusrdis.log|Registra le azioni di individuazione utente Active Directory.|Server del sito|  
|ADForestDisc.Log|Registra le azioni di individuazione foresta Active Directory.|Server del sito|  
|ddm.log|Registra le attività di Gestione individuazione dati.|Server del sito|  
|InventoryAgent.log|Registra le attività di inventario hardware, inventario software e individuazione heartbeat sul client.|Client|  
|netdisc.log|Registra le azioni di individuazione della rete.|Server del sito|  

### <a name="endpoint-analytics"></a><a name="bkmk_analytics"></a> Analisi degli endpoint

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|UXAnalyticsUploadWorker.log|Registra il caricamento dei dati nel servizio per l'analisi degli endpoint.|Server del sito|  
|SensorWmiProvider.log|Registra l'attività del provider WMI per il sensore di analisi degli endpoint.|Client|  
|SensorEndpoint.log|Registra l'esecuzione dei criteri di analisi degli endpoint e il caricamento dei dati client nel server del sito.|Client|
|SensorManagedProvider.log|Registra la raccolta e l'elaborazione di eventi e informazioni per l'analisi degli endpoint.|Client|

### <a name="endpoint-protection"></a><a name="BKMK_EPLog"></a> Endpoint Protection

Nella tabella seguente sono elencati i file di log contenenti informazioni correlate a Endpoint Protection.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|EndpointProtectionAgent.log|Registra informazioni dettagliate sull'installazione del client di Endpoint Protection e sull'applicazione di criteri antimalware in tale client.|Client|  
|EPCtrlMgr.log|Registra informazioni dettagliate sulla sincronizzazione di informazioni relative a minacce di tipo malware dal server del ruolo di Endpoint Protection con il database di Configuration Manager.|Server del sistema del sito|  
|EPMgr.log|Esegue il monitoraggio dello stato del ruolo del sistema del sito di Endpoint Protection.|Server del sistema del sito|  
|EPSetup.log|Fornisce informazioni sull'installazione del ruolo del sistema del sito di Endpoint Protection.|Server del sistema del sito|  

### <a name="extensions"></a><a name="BKMK_Extensions"></a> Estensioni

Nella tabella seguente sono elencati i file di log contenenti informazioni correlate alle estensioni.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|AdminUI.ExtensionInstaller.log|Registra informazioni sul download di estensioni da Microsoft e sull'installazione e la disinstallazione di tutte le estensioni.|Computer che esegue la console di Configuration Manager|  
|FeatureExtensionInstaller.log|Registra informazioni sull'installazione e sulla rimozione di singole estensioni quando vengono abilitate o disabilitate nella console di Configuration Manager.|Computer che esegue la console di Configuration Manager|  
|SmsAdminUI.log|Registra l'attività della console di Configuration Manager.|Computer che esegue la console di Configuration Manager|  

### <a name="inventory"></a><a name="BKMK_InventoryLog"></a> Inventario

Nella tabella seguente sono elencati i file di log contenenti informazioni correlate all'elaborazione dei dati di inventario.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|dataldr.log|Registra le informazioni sull'elaborazione dei file MIF e dell'inventario hardware nel database di Configuration Manager.|Server del sito|  
|invproc.log|Registra l'inoltro dei file MIF da un sito secondario al sito padre corrispondente.|Server del sito secondario|  
|sinvproc.log|Registra le informazioni sull'elaborazione dei dati di inventario del software nel database del sito.|Server del sito|  

### <a name="metering"></a><a name="BKMK_MeteringLog"></a> Metering

Nella tabella seguente sono elencati i file di log contenenti informazioni correlate al controllo software.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|mtrmgr.log|Esegue il monitoraggio di tutti i processi di controllo software.|Client|  
|SWMTRReportGen.log|Genera un report dei dati d'uso raccolto dall'agente di controllo. Tali dati vengono registrati in Mtrmgr.log.|Client|
|swmproc.log|Registra l'elaborazione di file e impostazioni di controllo.|Server del sito|

### <a name="migration"></a><a name="BKMK_MigrationLog"></a> Migrazione

Nella tabella seguente sono elencati i file di log contenenti informazioni correlate alla migrazione.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|migmctrl.log|Registra informazioni sulle azioni di migrazione riguardanti processi di migrazione, punti di distribuzione condivisi e aggiornamenti dei punti di distribuzione.|Sito principale della gerarchia di Configuration Manager e ogni sito primario figlio. In una gerarchia che include più siti primari, usare il file di log creato nel sito di amministrazione centrale.|  

### <a name="mobile-devices"></a><a name="BKMK_MDMLog"></a> Dispositivi mobili

Nelle sezioni seguenti vengono elencati i file di log contenenti informazioni correlate alla gestione dei dispositivi mobili.  

#### <a name="enrollment"></a><a name="BKMK_EnrollmentLog"></a> Registrazione

Nella tabella seguente sono elencati i registri che contengono informazioni correlate alla registrazione dei dispositivi mobili.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|DMPRP.log|Registra le comunicazione tra i punti di gestione abilitati per dispositivi mobili e gli endpoint dei punti di gestione.|Server del sistema del sito|  
|dmpmsi.log|Registra i dati di Windows Installer per la configurazione di un punto di gestione abilitato per i dispositivi mobili.|Server del sistema del sito|  
|DMPSetup.log|Registra la configurazione del punto di gestione quando è abilitato per i dispositivi mobili.|Server del sistema del sito|  
|enrollsrvMSI.log|Registra i dati di Windows Installer per la configurazione di un punto di registrazione.|Server del sistema del sito|  
|enrollmentweb.log|Registra le comunicazioni tra dispositivi mobili e il punto di registrazione.|Server del sistema del sito|  
|enrollwebMSI.log|Registra i dati di Windows Installer per la configurazione di un punto proxy di registrazione.|Server del sistema del sito|  
|enrollmentservice.log|Registra le comunicazioni tra un punto proxy di registrazione e un punto di registrazione.|Server del sistema del sito|  
|SMS_DM.log|Registra le comunicazioni tra dispositivi mobili, computer Mac e il punto di gestione abilitato per dispositivi mobili e computer Mac.|Server del sistema del sito|  

#### <a name="exchange-server-connector"></a><a name="BKMK_ExchSrvLog"></a> Connettore Exchange Server

I log seguenti contengono informazioni relative al connettore Exchange Server.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|easdisc.log|Registra le attività e lo stato del connettore Exchange Server.|Server del sito|  

#### <a name="mobile-device-legacy"></a><a name="BKMK_MDLegLog"></a> Dispositivo mobile legacy

Nella tabella seguente sono elencati i registri che contengono informazioni correlate al client di dispositivi mobili legacy.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|DmCertEnroll.log|Registra informazioni dettagliate sui dati di registrazione del certificato nei client dei dispositivi mobili legacy.|Client|  
|DMCertResp.htm|Registra la risposta HTML ricevuta dal server del certificato quando il programma legacy di registrazione client del dispositivo mobile richiede un certificato PKI.|Client|  
|DmClientHealth.log|Registra i GUID di tutti i client legacy dei dispositivi mobili che comunicano con il punto di gestione abilitato per i dispositivi mobili.|Server del sistema del sito|  
|DmClientRegistration.log|Registra le richieste di registrazione e le relative risposte ricevute e trasmesse dai client legacy dei dispositivi mobili.|Server del sistema del sito|  
|DmClientSetup.log|Registra i dati di installazione dei client legacy dei dispositivi mobili.|Client|  
|DmClientXfer.log|Registra i dati di trasferimento dei client legacy dei dispositivi mobili e delle distribuzioni di ActiveSync.|Client|  
|DmCommonInstaller.log|Registra l'installazione dei file di trasferimento per la configurazione dei file di trasferimento dei client legacy dei dispositivi mobili.|Client|  
|DmInstaller.log|Registra l'esito della chiamata da DMInstaller a DmClientSetup e l'esito dell'esecuzione di DmClientSetup per i client legacy dei dispositivi mobili.|Client|  
|DmpDatastore.log|Registra tutte le connessioni al database del sito e le query eseguite dal punto di gestione abilitato per i dispositivi mobili.|Server del sistema del sito|  
|DmpDiscovery.log|Registra tutti i dati di individuazione ricevuti dai client legacy dei dispositivi mobili nel punto di gestione abilitato per i dispositivi mobili.|Server del sistema del sito|  
|DmpHardware.log|Registra i dati di individuazione hardware ricevuti dai client legacy dei dispositivi mobili nel punto di gestione abilitato per i dispositivi mobili.|Server del sistema del sito|  
|DmpIsapi.log|Registra la comunicazione tra i client legacy dei dispositivi mobili e un punto di gestione abilitato per i dispositivi mobili.|Server del sistema del sito|  
|dmpmsi.log|Registra i dati di Windows Installer per la configurazione di un punto di gestione abilitato per i dispositivi mobili.|Server del sistema del sito|  
|DMPSetup.log|Registra la configurazione del punto di gestione quando è abilitato per i dispositivi mobili.|Server del sistema del sito|  
|DmpSoftware.log|Registra i dati di distribuzione software ricevuti dai client legacy dei dispositivi mobili in un punto di gestione abilitato per i dispositivi mobili.|Server del sistema del sito|  
|DmpStatus.log|Registra i dati dei messaggi di stato ricevuti dai client legacy dei dispositivi mobili in un punto di gestione abilitato per i dispositivi mobili.|Server del sistema del sito|  
|DmSvc.log|Registra la comunicazione tra i client legacy dei dispositivi mobili e un punto di gestione abilitato per i dispositivi mobili.|Client|  
|FspIsapi.log|Registra le comunicazioni verso il punto di stato di fallback da client legacy di dispositivi mobili e da computer client.|Server del sistema del sito|  

### <a name="os-deployment"></a><a name="BKMK_OSDLog"></a> Distribuzione del sistema operativo

Nella tabella seguente sono elencati i file di log contenenti informazioni relative alla distribuzione del sistema operativo.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|CAS.log|Registra informazioni dettagliate quando vengono rilevati punti di distribuzione per il contenuto a cui si fa riferimento.|Client|  
|ccmsetup.log|Registra le attività svolte da ccmsetup per l'installazione, l'aggiornamento e la rimozione dei client. Può essere usato per la risoluzione dei problemi di installazione dei client.|Client|  
|CreateTSMedia.log|Registra informazioni dettagliate sulla creazione del supporto per la sequenza di attività.|Computer che esegue la console di Configuration Manager|  
|Dism.log|Registra azioni di installazione driver o di applicazione aggiornamenti per la manutenzione offline.|Server del sistema del sito|  
|distmgr.log|Registra informazioni dettagliate sulla configurazione per l'attivazione di un punto di distribuzione per PXE (Pre-Boot eXecution Environment).|Server del sistema del sito|  
|DriverCatalog.log|Registra informazioni dettagliate sui driver di dispositivo importati nel catalogo dei driver.|Server del sistema del sito|  
|mcsisapi.log|Registra informazioni sul trasferimento dei pacchetti multicast e le risposte alle richieste dei client.|Server del sistema del sito|  
|mcsexec.log|Registra le azioni relative a controllo di integrità, spazio dei nomi, creazione delle sessioni e controllo certificati.|Server del sistema del sito|  
|mcsmgr.log|Registra le modifiche alla configurazione, alla modalità di sicurezza e alla disponibilità.|Server del sistema del sito|  
|mcsprv.log|Registra l'interazione tra il provider multicast e i Servizi di distribuzione Windows (WDS).|Server del sistema del sito|  
|MCSSetup.log|Registra informazioni dettagliate sull'installazione del ruolo server multicast.|Server del sistema del sito|  
|MCSMSI.log|Registra informazioni dettagliate sull'installazione del ruolo server multicast.|Server del sistema del sito|  
|Mcsperf.log|Registra informazioni dettagliate sull'aggiornamento dei contatori delle prestazioni multicast.|Server del sistema del sito|  
|MP_ClientIDManager.log|Registra le risposte del punto di gestione alle richieste dell'ID client originate dalle sequenze di attività a partire da PXE o dal supporto di avvio.|Server del sistema del sito|  
|MP_DriverManager.log|Registra le risposte del punto di gestione alle richieste dell'operazione sequenza di attività Applica automaticamente i driver.|Server del sistema del sito|  
|OfflineServicingMgr.log|Registra informazioni dettagliate sulle pianificazioni della manutenzione offline e sulle azioni di applicazione aggiornamenti sui file di formato Windows Imaging (WIM) del sistema operativo.|Server del sistema del sito|  
|Setupact.log|Registra informazioni dettagliate sui registri di Windows Sysprep e di installazione. Per altre informazioni, vedere [File di log](https://docs.microsoft.com/windows/deployment/upgrade/log-files).|Client|  
|Setupapi.log|Registra informazioni dettagliate sui registri di Windows Sysprep e di installazione.|Client|  
|Setuperr.log|Registra informazioni dettagliate sui registri di Windows Sysprep e di installazione.|Client|  
|smpisapi.log|Registra informazioni dettagliate sulle azioni di acquisizione e ripristino dello stato del client, nonché informazioni sulle soglie.|Client|  
|Smpmgr.log|Registra informazioni dettagliate sui risultati dei controlli di integrità del punto di migrazione stato e delle modifiche della configurazione.|Server del sistema del sito|  
|smpmsi.log|Registra informazioni dettagliate di installazione e configurazione relative al punto di migrazione stato.|Server del sistema del sito|  
|smpperf.log|Registra gli aggiornamenti del contatore delle prestazioni del punto di migrazione stato.|Server del sistema del sito|  
|smspxe.log|Registra informazioni dettagliate sulle risposte ai client avviati tramite PXE e sull'espansione delle immagini di avvio e dei file di avvio.|Server del sistema del sito|  
|smssmpsetup.log|Registra informazioni dettagliate di installazione e configurazione relative al punto di migrazione stato.|Server del sistema del sito|
| SMS_PhasedDeployment.log| File di log per distribuzioni in più fasi|Sito principale della gerarchia di Configuration Manager|
|Smsts.log|Registra le attività delle sequenze attività.|Client|  
|TSAgent.log|Registra l'esito delle dipendenze delle sequenze di attività prima di avviare una sequenza di attività.|Client|  
|TaskSequenceProvider.log|Registra informazioni dettagliate sull'importazione, l'esportazione o la modifica delle sequenze attività.|Server del sistema del sito|  
|loadstate.log|Registra informazioni dettagliate sull'Utilità di migrazione stato utente (USMT) e il ripristino dei dati sullo stato dell'utente.|Client|  
|scanstate.log|Registra informazioni dettagliate sull'Utilità di migrazione stato utente (USMT) e l'acquisizione dei dati sullo stato dell'utente.|Client|  

### <a name="power-management"></a><a name="BKMK_PowerMgmtLog"></a> Risparmio energia

Nella tabella seguente sono elencati i file di log contenenti informazioni correlate al risparmio energia.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|Pwrmgmt.log|Registra informazioni dettagliate sulle attività di risparmio energia sul computer client, che includono il monitoraggio e l'applicazione delle impostazioni da parte dell'agente client di Risparmio energia.|Client|  

### <a name="remote-control"></a><a name="BKMK_RCLog"></a> Controllo remoto

Nella tabella seguente sono elencati i file di log contenenti informazioni correlate al controllo remoto.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|CMRcViewer.log|Registra informazioni dettagliate sull'attività del visualizzatore controllo remoto.|Nel computer che esegue il visualizzatore controllo remoto, nella cartella %temp%.|  

### <a name="reporting"></a><a name="BKMK_ReportLog"></a> Creazione di report

Nella tabella seguente sono elencati i file di log di Configuration Manager contenenti informazioni correlate al reporting.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|srsrp.log|Registra informazioni sulle attività e lo stato del punto di Reporting Services.|Server del sistema del sito|  
|srsrpMSI.log|Registra informazioni dettagliate sui risultati del processo di installazione del punto di Reporting Services dall'output MSI.|Server del sistema del sito|  
|srsrpsetup.log|Registra i risultati del processo di installazione del punto di Reporting Services.|Server del sistema del sito|  

### <a name="role-based-administration"></a><a name="BKMK_RBALog"></a> Amministrazione basata su ruoli

Nella tabella seguente sono elencati i file di log contenenti informazioni correlate alla gestione dell'amministrazione basata su ruoli.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|hman.log|Registra informazioni sulle modifiche della configurazione del sito e sulla pubblicazione delle informazioni del sito in Servizi di dominio Active Directory.|Server del sito|  
|SMSProv.log|Registra gli accessi del provider WMI al database del sito.|Computer con il provider SMS|  

### <a name="software-metering"></a><a name="BKMK_MeteringLog"></a> Misurazione del software

La tabella seguente elenca i file di log contenenti informazioni relative alla misurazione del software.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|mtrmgr.log|Esegue il monitoraggio di tutti i processi di controllo software.|Server del sito|  

### <a name="software-updates"></a><a name="BKMK_SU_NAPLog"></a> Aggiornamenti software

La tabella seguente elenca i file di log contenenti informazioni correlate agli aggiornamenti software.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|AlternateHandler.log|Registra informazioni dettagliate quando il client chiama l'interfaccia COM A portata di clic di Office per scaricare e installare gli aggiornamenti del client App di Microsoft 365 per grandi imprese. È simile all'uso di WuaHandler quando questo chiama l'API Agente di Windows Update per scaricare e installare gli aggiornamenti di Windows.<!-- SCCMDocs#888 -->|Client|
|ccmperf.log|Registra le attività di manutenzione e acquisizione dati correlate ai contatori delle prestazioni dei client.|Client|
|DeltaDownload.log|Registra le informazioni sul download di aggiornamenti rapidi e aggiornamenti scaricati con Ottimizzazione recapito.|Client|  
|PatchDownloader.log|Registra informazioni dettagliate sul processo di download degli aggiornamenti software dall'origine degli aggiornamenti alla destinazione del download sul server del sito.|Se si scaricano gli aggiornamenti manualmente, questo file di log si trova nella directory %temp% dell'utente che esegue la console nel computer in cui questa è in esecuzione. Per le regole di distribuzione automatica, questo file di log si trova nel server del sito in %windir%\CCM\Logs, se il client ConfigMgr è installato nel server del sito.|  
|PolicyEvaluator.log|Registra informazioni dettagliate sulla valutazione dei criteri nei computer client, inclusi quelli derivanti dagli aggiornamenti software.|Client|  
|RebootCoordinator.log|Registra informazioni dettagliate sul coordinamento dei riavvii del sistema nei computer client dopo le installazioni degli aggiornamenti software.|Client|  
|ScanAgent.log|Registra informazioni dettagliate sulle richieste di ricerca di aggiornamenti software, sulla posizione di WSUS e sulle azioni correlate.|Client|  
|SdmAgent.log|Registra informazioni dettagliate sul monitoraggio di aggiornamenti e conformità. Il file di log degli aggiornamenti software, Updateshandler.log, fornisce comunque informazioni più dettagliate sull'installazione degli aggiornamenti software necessari per la conformità. Questo file di log viene condiviso con le impostazioni di conformità.|Client|  
|ServiceWindowManager.log|Registra informazioni dettagliate sulla valutazione delle finestre di manutenzione.|Client|
|SMS_ISVUPDATES_SYNCAGENT.log| File di log per la sincronizzazione degli aggiornamenti software di terze parti.| Punto di aggiornamento software di livello superiore nella gerarchia di Configuration Manager.|
|SMS_OrchestrationGroup.log| File di log per i gruppi di orchestrazione|Server del sito|
|SmsWusHandler.log|Registra informazioni dettagliate sul processo di analisi per lo strumento di inventario per Microsoft Updates.|Client|  
|StateMessage.log|Registra informazioni dettagliate sui messaggi di stato dell'aggiornamento software creati e inviati al punto di gestione.|Client|  
|SUPSetup.log|Registra informazioni dettagliate sull'installazione del punto di aggiornamento software. Al termine dell'installazione del punto di aggiornamento software, **Installation was successful** viene scritto nel file di log.|Server del sistema del sito|  
|UpdatesDeployment.log|Registra informazioni dettagliate sulle distribuzioni nel client, comprese l'attivazione, la valutazione e l'applicazione degli aggiornamenti software. La registrazione dettagliata visualizza informazioni aggiuntive sull'interazione con l'interfaccia utente del client.|Client|  
|UpdatesHandler.log|Registra informazioni dettagliate sull'analisi della conformità degli aggiornamenti software e sul download e l'installazione di aggiornamenti software nel client.|Client|  
|UpdatesStore.log|Registra informazioni dettagliate sullo stato di conformità degli aggiornamenti software ottenuto durante il ciclo di analisi della conformità.|Client|  
|WCM.log|Registra informazioni dettagliate sulle configurazioni del punto di aggiornamento software e sulle connessioni al server WSUS per categorie di aggiornamento, classificazioni e lingue sottoscritte.|Server del sito|  
|WSUSCtrl.log|Registra informazioni dettagliate su configurazione, connettività al database e integrità del server WSUS per il sito.|Server del sistema del sito|  
|wsyncmgr.log|Registra informazioni dettagliate sul processo di sincronizzazione degli aggiornamenti software.|Server del sito|  
|WUAHandler.log|Registra informazioni dettagliate sull'agente di Windows Update nel client durante la ricerca di aggiornamenti software.|Client|  

### <a name="wake-on-lan"></a><a name="BKMK_WOLLog"></a> Riattivazione LAN

Nella tabella seguente sono elencati i file di log contenenti informazioni relative all'uso della riattivazione LAN.  

> [!NOTE]  
> Quando si integra la riattivazione LAN usando il proxy di riattivazione, questa attività viene registrata nel client. Ad esempio, vedere CcmExec.log e SleepAgent_<*dominio*\>@SYSTEM_0.log nella sezione [Operazioni client](#BKMK_ClientOpLogs) di questo articolo.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|wolcmgr.log|Registra informazioni dettagliate sui client ai quali è necessario inviare pacchetti di riattivazione, sul numero di pacchetti di riattivazione inviati e sul numero di pacchetti di riattivazione inviati nuovamente.|Server del sito|  
|wolmgr.log|Registra informazioni dettagliate sulle procedure di riattivazione, ad esempio sul momento in cui riattivare distribuzioni configurate per la riattivazione LAN.|Server del sito|  

### <a name="windows-10-servicing"></a><a name="BKMK_WindowsServicingLog"></a> Manutenzione di Windows 10

Nella tabella seguente sono elencati i file di log contenenti informazioni correlate alla manutenzione di Windows 10.  
Per la manutenzione vengono usati la stessa infrastruttura e lo stesso processo degli aggiornamenti software. Per altri log applicabili allo scenario di manutenzione, vedere [Aggiornamenti software](#BKMK_SU_NAPLog).

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|CBS.log|Registra gli errori di manutenzione correlati alle modifiche per Aggiornamenti di Windows o ruoli e funzionalità.|Client|
|DISM.log|Registra tutte le azioni usando Gestione e manutenzione immagini distribuzione. Se necessario, DISM.log punterà a CBS.log per altri dettagli.|Client|
|setupact.log|File di log primario per la maggior parte degli errori che si verificano durante il processo di installazione di Windows. Il file di log è disponibile nella cartella %windir%\$Windows.~BT\sources\panther.|Client|

Per altre informazioni, vedere [Online Servicing-Related Log Files](https://docs.microsoft.com/windows-hardware/manufacture/desktop/deployment-troubleshooting-and-log-files#online-servicing-related-log-files) (File di log correlati alla manutenzione online).

### <a name="windows-update-agent"></a><a name="BKMK_WULog"></a> Agente di Windows Update

Nella tabella seguente sono elencati i file di log contenenti informazioni correlate all'agente di Windows Update.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|WindowsUpdate.log|Registra informazioni dettagliate che indicano il momento in cui l'agente di Windows Update si connette al server WSUS e recupera gli aggiornamenti software per la valutazione della conformità, nonché se vi sono aggiornamenti per i componenti dell'agente.|Client|  

Per altre informazioni, vedere [File di log di Windows Update](https://docs.microsoft.com/windows/deployment/update/windows-update-logs).

### <a name="wsus-server"></a><a name="BKMK_WSUSLog"></a> Server WSUS

Nella tabella seguente sono elencati i file di log contenenti informazioni correlate al server WSUS.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|Change.log|Registra informazioni dettagliate sulle informazioni modificate del database del server WSUS.|Server WSUS|  
|SoftwareDistribution.log|Registra informazioni dettagliate sugli aggiornamenti software sincronizzati dall'origine aggiornamenti configurata con il database del server WSUS.|Server WSUS|  

Questi file di log si trovano nella cartella `%ProgramFiles%\Update Services\LogFiles`.

## <a name="see-also"></a>Vedere anche

- [Informazioni sui file di log](about-log-files.md)

- [Supporto tecnico OneTrace](../../support/support-center-onetrace.md)

- [Visualizzatore file di log del Supporto tecnico](../../support/support-center.md#support-center-log-file-viewer)

- [CMTrace](../../support/cmtrace.md)
