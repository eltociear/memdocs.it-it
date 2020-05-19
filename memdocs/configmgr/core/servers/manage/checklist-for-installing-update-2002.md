---
title: Elenco di controllo per la versione 2002
titleSuffix: Configuration Manager
description: Informazioni sulle azioni da intraprendere prima di eseguire l'aggiornamento di Configuration Manager alla versione 2002.
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2993032a-1204-4bd8-b5af-17a980bb0649
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 63293c103cf8a19d006bd700cac6c370ba5e7391
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268947"
---
# <a name="checklist-for-installing-update-2002-for-configuration-manager"></a>Elenco di controllo per l'installazione dell'aggiornamento 2002 di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Quando si usa la versione Current Branch di Configuration Manager, è possibile installare l'aggiornamento nella console per la versione 2002 per aggiornare la gerarchia da una versione precedente. <!-- baseline only statement:-->La versione 2002 è disponibile anche come [supporto di base](updates.md#bkmk_Baselines), quindi è possibile usare il supporto di installazione per installare il primo sito di una nuova gerarchia.

Per ottenere l'aggiornamento per la versione 2002, è necessario usare un punto di connessione del servizio nel sito principale della gerarchia. Questo ruolo del sistema del sito può essere in modalità online o offline. Per scaricare l'aggiornamento quando il punto di connessione del servizio è in modalità offline, [usare lo strumento di connessione del servizio](use-the-service-connection-tool.md).<!-- SCCMDocs#1946 -->

Dopo che la gerarchia ha scaricato l'aggiornamento da Microsoft, lo si può trovare nella console. Nell'area di lavoro **Amministrazione** selezionare il nodo **Aggiornamenti e manutenzione**.

- Quando l'aggiornamento risulta **Disponibile**, è pronto per l'installazione. Prima di installare la versione 2002, leggere le informazioni seguenti sull'[installazione dell'aggiornamento 2002](#about-installing-update-2002) e l'[elenco di controllo](#checklist) delle configurazioni da eseguire prima dell'avvio dell'aggiornamento.

- Se l'aggiornamento risulta come **Download** e non cambia, esaminare eventuali errori in **hman.log** e in **dmpdownloader.log**.

  - Il file dmpdownloader.log può indicare che il processo dmpdownloader è in attesa di un intervallo prima di cercare gli aggiornamenti. Per riavviare il download dei file di ridistribuzione dell'aggiornamento, riavviare il servizio **SMS_Executive** nel server del sito.

  - Un altro problema di download comune si verifica quando le impostazioni del server proxy impediscono il download da `silverlight.dlservice.microsoft.com`, `download.microsoft.com` e `go.microsoft.com`.

Per altre informazioni sull'installazione degli aggiornamenti, vedere [Aggiornamenti e manutenzione nella console](updates.md#bkmk_inconsole).

Per altre informazioni sulle versioni Current Branch, vedere [Versioni di base e di aggiornamento](updates.md#bkmk_Baselines).

## <a name="about-installing-update-2002"></a>Informazioni sull'installazione dell'aggiornamento 2002

### <a name="sites"></a>Siti

L'aggiornamento 2002 deve essere installato nel sito principale della gerarchia. Avviare l'installazione dal sito di amministrazione centrale (CAS) o dal sito primario autonomo. Dopo l'installazione dell'aggiornamento nel sito di livello più alto, l'aggiornamento nei siti figlio viene eseguito nel modo seguente:

- I siti primari figlio installano automaticamente l'aggiornamento al termine dell'installazione dell'aggiornamento nel sito di amministrazione centrale. È possibile usare gli intervalli di servizio per controllare quando eseguire l'installazione dell'aggiornamento in un sito. Per altre informazioni, vedere [Intervalli di servizio per i server del sito](service-windows.md).

- Dopo che il sito primario padre ha completato l'installazione dell'aggiornamento, aggiornare manualmente ogni sito secondario dalla console di Configuration Manager. L'aggiornamento automatico dei server dei siti secondari non è supportato.

### <a name="site-system-roles"></a>Ruoli del sistema del sito

Quando un server del sito installa l'aggiornamento, aggiorna automaticamente tutti i ruoli del sistema del sito. Questi ruoli sono nel server del sito o installati in server remoti. Prima di installare l'aggiornamento, verificare quindi che ogni server del sistema del sito soddisfi i prerequisiti correnti per la nuova versione di aggiornamento.

### <a name="configuration-manager-consoles"></a>Console di Configuration Manager

La prima volta che si usa una console di Configuration Manager dopo l'aggiornamento, viene richiesto di aggiornare tale console. È anche possibile eseguire l'installazione di Configuration Manager nel computer che ospita la console e scegliere l'opzione per aggiornare la console. Installare l'aggiornamento nella console appena possibile. Per altre informazioni, vedere [Installare la console di Configuration Manager](../deploy/install/install-consoles.md).

> [!IMPORTANT]  
> Quando si installa un aggiornamento nel sito di amministrazione centrale, tenere presenti le limitazioni e i ritardi seguenti che si verificano finché tutti i siti primari figlio non hanno completato l'installazione dell'aggiornamento:
>
> - Gli **aggiornamenti client** non vengono avviati. Sono inclusi gli aggiornamenti automatici dei client e quelli dei client pre-produzione. Inoltre non è possibile promuovere i client di pre-produzione nell'ambiente di produzione finché l'ultimo sito non ha completato l'installazione dell'aggiornamento. Al termine dell'installazione dell'aggiornamento nell'ultimo sito, gli aggiornamenti client vengono avviati in base alle scelte di configurazione.
> - Le **nuove funzionalità** abilitate con l'aggiornamento non sono disponibili. Questo comportamento consente di evitare che la replica dei dati del sito di amministrazione centrale relativi a una funzionalità venga inviata a un sito in cui non è ancora installato il supporto per tale funzionalità. La funzionalità specificata è disponibile per l'uso dopo che l'aggiornamento è stato installato in tutti i siti primari.
> - I **collegamenti di replica** tra il sito di amministrazione centrale e i siti primari figlio non risultano aggiornati. Questa condizione è segnalata dallo stato di installazione dell'aggiornamento impostato come *Completato con avviso* per Monitoraggio dell'inizializzazione della replica. Nell'area di lavoro **Monitoraggio** della console, questo stato viene visualizzato come *Configurazione collegamento in corso*.

### <a name="early-update-ring"></a>Anello di aggiornamento anticipato

<!-- SCCMDocs#1397 -->

A partire dall'11 maggio 2020 la versione 2002 è disponibile per l'installazione a livello globale da parte di tutti i clienti. Se in precedenza è stato scelto l'anello di aggiornamento anticipato, controllare la presenza di un aggiornamento a questa versione Current Branch.

<!--
At this time, version 2002 is released for the early update ring. To install this update, you need to opt-in. The following PowerShell script adds your hierarchy or standalone primary site to the early update ring for version 2002:

[Version 2002 opt-in script](https://go.microsoft.com/fwlink/?linkid=2099733) <!-- This fwlink points to the script package on the Download Center, don't change the link here! Make any changes to the fwlink target -->

<!--
Microsoft digitally signs the script, and bundles it inside a signed self-extracting executable.

> [!Note]  
> The version 2002 update is only applicable to sites running version 1810 or later.

To opt-in to the early update ring:

1. Open Windows PowerShell and **Run as administrator**
1. Run the **EnableEarlyUpdateRing2002.ps1** script, using the following syntax:

    `EnableEarlyUpdateRing2002.ps1 <SiteServer_Name> | SiteServer_IP>`

    Where `SiteServer` refers to the central administration site or standalone primary site server. For example, `EnableEarlyUpdateRing2002.ps1 cmprimary01`

1. Check for updates. For more information, see [Get available updates](install-in-console-updates.md#get-available-updates).

The version 2002 update should now be available in the console.

> [!Important]  
> This script only adds your site to the early update ring for version 2002. It's not a permanent change.
 -->

## <a name="checklist"></a>Elenco di controllo

### <a name="all-sites-run-a-supported-version-of-configuration-manager"></a>Tutti i siti eseguono una versione supportata di Configuration Manager

Per poter avviare l'installazione dell'aggiornamento alla versione 2002, ogni server del sito nella gerarchia deve eseguire la stessa versione di Configuration Manager. Per eseguire l'aggiornamento alla versione 2002, è necessario usare la versione 1810 o successiva.

### <a name="review-the-status-of-your-product-licensing"></a>Esaminare lo stato della licenza del prodotto

È necessario avere un contratto Software Assurance (SA) attivo o diritti di sottoscrizione equivalenti per installare questo aggiornamento. Quando aggiorna il sito, nella pagina **Licenze** è disponibile l'opzione per la conferma della **data di scadenza di Software Assurance**.

Questo valore è facoltativo. È possibile specificarlo come utile promemoria della data di scadenza della licenza. Questa data è visibile quando si installano gli aggiornamenti futuri. Questo valore potrebbe essere stato specificato in precedenza durante la configurazione o l'installazione di un aggiornamento. È anche possibile specificare questo valore nella console di Configuration Manager. Nell'area di lavoro **Amministrazione** espandere **Configurazione del sito** e selezionare **Siti**. Selezionare **Impostazioni gerarchia** sulla barra multifunzione e passare alla scheda **Licenze**.

Per altre informazioni, vedere [Licenze e rami](../../understand/learn-more-editions.md).

### <a name="review-microsoft-net-versions"></a>Esaminare le versioni di Microsoft .NET

Quando un sito installa questo aggiornamento, se il requisito minimo di .NET Framework 4.5 non è installato, Configuration Manager installa automaticamente .NET Framework 4.5.2. Quando questo prerequisito non è già installato, il sito lo installa in ogni server che ospita uno dei ruoli del sistema del sito seguenti:

- Punto di gestione
- punto di connessione del servizio
- Punto proxy di registrazione
- Punto di registrazione

Questa installazione consente di impostare il server del sistema del sito in uno stato di riavvio in sospeso e segnala gli errori al visualizzatore di stato dei componenti di Configuration Manager. È anche possibile che le applicazioni .NET sul server presentino errori casuali fino a quando il server non viene riavviato.

Per altre informazioni, vedere  [Prerequisiti del sito e del sistema del sito](../../plan-design/configs/site-and-site-system-prerequisites.md).

### <a name="review-the-version-of-the-windows-adk-for-windows-10"></a>Esaminare la versione di Windows ADK per Windows 10

La versione di Windows 10 Assessment and Deployment Kit (ADK) deve essere supportata per Configuration Manager versione 2002. Per altre informazioni sulle versioni supportate di Windows ADK, vedere [Windows 10 ADK](../../plan-design/configs/support-for-windows-10.md#windows-10-adk). Se è necessario aggiornare Windows ADK, eseguire questa operazione prima di iniziare l'aggiornamento di Configuration Manager. Questo ordine assicura che le immagini d'avvio predefinite vengano aggiornate automaticamente alla versione più recente di Windows PE. Aggiornare manualmente eventuali immagini di avvio personalizzate dopo l'aggiornamento del sito.

Se si aggiorna il sito prima di aggiornare Windows ADK, vedere [Aggiornare i punti di distribuzione con l'immagine di avvio](../../../osd/get-started/manage-boot-images.md#update-distribution-points-with-the-boot-image).

### <a name="review-sql-server-native-client-version"></a>Verificare la versione di SQL Server Native Client

Installare una versione minima di SQL Server 2012 Native Client che include il supporto per TLS 1.2. Per altre informazioni, vedere [Elenco dei controlli dei prerequisiti](../deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).

### <a name="review-the-site-and-hierarchy-status-for-unresolved-issues"></a>Esaminare lo stato del sito e della gerarchia per verificare la presenza di problemi non risolti

Un aggiornamento del sito può avere esito negativo a causa di problemi operativi esistenti. Prima di aggiornare un sito, risolvere tutti i problemi operativi per i sistemi seguenti:  

- Server del sito  
- Server di database del sito  
- Ruoli del sistema del sito remoto su altri server

Per altre informazioni, vedere  [Usare gli avvisi e il sistema di stato](use-alerts-and-the-status-system.md).

### <a name="review-file-and-data-replication-between-sites"></a>Esaminare la replica di file e dati tra siti

Verificare che la replica di file e database tra siti sia funzionante e aggiornata. Eventuali ritardi o backlog in uno dei due ambiti possono compromettere l'aggiornamento.

#### <a name="database-replication"></a>replica di database

Per la [replica di database](../../plan-design/hierarchy/database-replication.md), per risolvere i problemi prima di avviare l'aggiornamento, usare **Replication Link Analyzer** (RLA). Per altre informazioni, vedere [Monitorare la replica di database](monitor-replication.md).

Usare RLA per rispondere alle domande seguenti:

- La replica per gruppo è in uno stato valido?
- Eventuali collegamenti sono ridotti?
- Sono presenti errori?

Se è presente un backlog, attendere il completamento della cancellazione. Se il backlog è di grandi dimensioni, ad esempio milioni di record, il collegamento è in uno stato non valido. Prima di aggiornare il sito, risolvere il problema di replica. Se è necessaria ulteriore assistenza, contattare il supporto tecnico Microsoft.<!-- 2838129 -->

#### <a name="file-based-replication"></a>replica basata su file

Per la [replica basata su file](../../plan-design/hierarchy/file-based-replication.md), controllare tutte le cartelle di posta in arrivo per verificare la presenza di un backlog sia nei siti di origine che in quelli di destinazione. Se sono presenti molti processi di replica bloccati o in sospeso, attendere che vengano cancellati.<!-- SCCMDocs#1792 -->

- Nel sito di origine esaminare **sender.log**.
- Nel sito di destinazione esaminare **despooler.log**.

### <a name="install-all-applicable-critical-windows-updates"></a>Installare tutti gli aggiornamenti di Windows critici applicabili

Prima di installare un aggiornamento per Configuration Manager, installare gli aggiornamenti critici del sistema operativo per ogni sistema del sito applicabile. Questi server includono il server del sito, il server di database del sito e i ruoli del sistema del sito remoto. Se un aggiornamento installato richiede un riavvio, riavviare i server interessati prima di iniziare l'aggiornamento.

### <a name="disable-database-replicas-for-management-points-at-primary-sites"></a>Disabilitare le repliche di database per i punti di gestione nei siti primari

Configuration Manager non può aggiornare un sito primario per il quale esista una replica del database per i punti di gestione abilitati. Prima di installare un aggiornamento per Configuration Manager, disabilitare la replica di database.

Per altre informazioni, vedere [Repliche di database per i punti di gestione](../deploy/configure/database-replicas-for-management-points.md).

### <a name="set-sql-server-alwayson-availability-groups-to-manual-failover"></a>Impostare i gruppi di disponibilità di SQL Server Always On per eseguire il failover manuale

Se si usa un gruppo di disponibilità, prima di iniziare l'installazione dell'aggiornamento verificare che il gruppo di disponibilità sia impostato sul failover manuale. Dopo l'aggiornamento del sito, è possibile ripristinare la modalità di failover automatico. Per altre informazioni, vedere  [Server AlwaysOn per database del sito](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

### <a name="disable-site-maintenance-tasks-at-each-site"></a>Disabilitare le attività di manutenzione del sito in ogni sito

Prima di installare l'aggiornamento , disabilitare le eventuali attività di manutenzione che potrebbero essere eseguite mentre è in corso il processo di aggiornamento. Ad esempio, tra gli altri:

- Backup server sito
- Elimina operazioni client obsolete
- Elimina dati di individuazione obsoleti

Quando un'attività di manutenzione del database del sito viene eseguita durante l'installazione dell'aggiornamento, quest'ultima potrebbe avere esito negativo. Prima di disabilitare un'attività, registrarne la pianificazione per poter ripristinare la sua configurazione dopo l'installazione dell'aggiornamento.

Per altre informazioni, vedere  [Attività di manutenzione](maintenance-tasks.md)  e [Informazioni di riferimento per le attività di manutenzione](reference-for-maintenance-tasks.md).

### <a name="temporarily-stop-any-antivirus-software"></a>Arrestare temporaneamente i software antivirus

Prima di aggiornare un sito, arrestare il software antivirus sui server Configuration Manager. L'aggiornamento infatti potrebbe non riuscire perché il software antivirus può bloccare alcuni file che devono essere aggiornati. <!--SMS.503481-->

### <a name="create-a-backup-of-the-site-database"></a>Creare un backup del database del sito

Prima di aggiornare un sito, eseguire il backup del database del sito nel sito di amministrazione centrale e nei siti primari. Questo backup assicura di avere un backup corretto da usare per il ripristino di emergenza.

Per altre informazioni, vedere  [Backup e ripristino](backup-and-recovery.md).

### <a name="back-up-customized-files"></a>Eseguire il backup di file personalizzati

Se l'utente o un prodotto di terze parti personalizza un file di configurazione di Configuration Manager, salvare una copia delle personalizzazioni.

Ad esempio, aggiungere le voci personalizzate al file **osdinjection.xml** nella cartella `bin\X64` della directory di installazione di Configuration Manager. Dopo l'aggiornamento di Configuration Manager, queste personalizzazioni non vengono mantenute. È necessario riapplicare le personalizzazioni.

### <a name="plan-for-client-piloting"></a>Pianificare la distribuzione pilota del client

Quando si installa un aggiornamento del sito che aggiorna anche il client, testare il nuovo aggiornamento client in pre-produzione prima di aggiornare tutti i client di produzione. Per usare questa opzione, configurare il sito in modo da supportare gli aggiornamenti automatici di pre-produzione prima di iniziare l'installazione dell'aggiornamento.

Per altre informazioni, vedere  [Aggiornare i client](../../clients/manage/upgrade/upgrade-clients.md)  e [Come testare gli aggiornamenti client in una raccolta di pre-produzione](../../clients/manage/upgrade/test-client-upgrades.md).

### <a name="plan-to-use-service-windows"></a>Iniziare a usare gli intervalli di servizio

Per definire un periodo durante il quale possono essere installati gli aggiornamenti a un server del sito, usare gli intervalli di servizio, che permettono di controllare quando i siti nella gerarchia installano l'aggiornamento. Per altre informazioni, vedere  [Intervalli di servizio per i server del sito](service-windows.md).

### <a name="review-supported-extensions"></a>Verificare le estensioni supportate

<!--SCCMdocs#587-->
Se si estende Configuration Manager con altri prodotti Microsoft o di partner Microsoft, verificare che la versione 2002 sia supportata da tali prodotti. Rivolgersi al fornitore del prodotto per verificare questa informazione. Ad esempio, vedere le [note sulla versione](../../../mdt/release-notes.md) di Microsoft Deployment Toolkit.

### <a name="remove-intune-subscription-hybrid-mdm"></a>Rimuovere la sottoscrizione di Intune (MDM ibrida)

<!-- SCCMDocs-pr#4253 -->
L'offerta di servizio MDM ibrido è stata ritirata a partire dal 1° settembre 2019. Se il sito di Configuration Manager dispone di una sottoscrizione Microsoft Intune, è necessario rimuoverlo. Per altre informazioni, vedere [Rimuovere la soluzione MDM ibrida](../../../mdm/understand/what-happened-to-hybrid.md#remove-hybrid-mdm).

### <a name="run-the-setup-prerequisite-checker"></a>Eseguire il controllo dei prerequisiti di installazione

Quando l'aggiornamento risulta **Disponibile** nella console, è possibile eseguire il controllo dei prerequisiti prima di procedere all'installazione. Quando si installa l'aggiornamento nel sito, il controllo dei prerequisiti viene eseguito nuovamente.

Per eseguire il controllo dei prerequisiti dalla console, passare all'area di lavoro **Amministrazione** e selezionare **Aggiornamenti e manutenzione**. Selezionare il pacchetto di aggiornamento **Configuration Manager 2002** e selezionare **Esegui controllo prerequisiti** sulla barra multifunzione.

Per altre informazioni, vedere la sezione per **eseguire il controllo dei prerequisiti prima di installare un aggiornamento** in [Prima di installare un aggiornamento nella console](install-in-console-updates.md#bkmk_beforeinstall).

> [!IMPORTANT]  
> Quando viene eseguito il controllo dei prerequisiti, vengono aggiornati alcuni file di origine del prodotto usati per le attività di manutenzione del sito. Di conseguenza, dopo aver eseguito il controllo dei prerequisiti, ma prima di installare l'aggiornamento, se si deve svolgere un'attività di manutenzione del sito, eseguire  **Setupwfe.exe** (il programma di installazione di Configuration Manager) dalla cartella CD.Latest nel server del sito.

### <a name="update-sites"></a>Aggiornare i siti

A questo punto è possibile avviare l'installazione dell'aggiornamento per la gerarchia. Per altre informazioni sull'installazione dell'aggiornamento, vedere [Installare gli aggiornamenti nella console](install-in-console-updates.md#bkmk_install).

È possibile pianificare l'installazione dell'aggiornamento al di fuori delle normali ore lavorative. Determinare quando il processo avrà l'impatto minimo sulle operazioni aziendali. Con l'installazione dell'aggiornamento e le relative azioni, vengono reinstallati i componenti del sito e i ruoli del sistema del sito.

Per altre informazioni, vedere  [Aggiornamenti per Configuration Manager](updates.md).

## <a name="post-update-checklist"></a>Elenco di controllo post-aggiornamento

Dopo gli aggiornamenti del sito, usare l'elenco di controllo seguente per completare le configurazioni e le attività comuni.

### <a name="confirm-version-and-restart-if-necessary"></a>Confermare la versione e il riavvio (se necessario)

Verificare che per ogni server del sito e ogni ruolo del sistema del sito sia stato eseguito l'aggiornamento alla versione 2002. Nella console aggiungere la colonna **Versione** ai nodi **Siti** e **Punti di distribuzione** nell'area di lavoro **Amministrazione**. Se necessario, un ruolo del sistema del sito viene reinstallato automaticamente per l'aggiornamento alla nuova versione.

Provare a riavviare i sistemi del sito remoti che non vengono aggiornati subito. Esaminare l'infrastruttura dei siti e verificare che sia stato correttamente completato il riavvio dei server del sito e dei server del sistema del sito remoti applicabili. In genere, i server del sito vengono riavviati solo quando Configuration Manager installa .NET come prerequisito per un ruolo del sistema del sito.

### <a name="confirm-site-to-site-replication-is-active"></a>Verificare che la replica da sito a sito sia attiva

Nella console di Configuration Manager passare alle posizioni seguenti per visualizzare lo stato e assicurarsi che la replica sia attiva:  

- Area di lavoro **Monitoraggio**, nodo **Gerarchia siti**  

- Area di lavoro **Monitoraggio**, nodo **Replica di database**  

Per altre informazioni, vedere gli articoli seguenti:  

- [Monitorare l'infrastruttura della gerarchia e di replica](monitor-hierarchy.md)
- [Informazioni su Replication Link Analyzer](monitor-replication.md#BKMK_RLA)  

### <a name="update-configuration-manager-consoles"></a>Aggiornare le console di Configuration Manager

Aggiornare tutte le console remote di Configuration Manager alla stessa versione. Viene richiesto di aggiornare la console nei casi seguenti:  

- Si apre la console.  

- Si passa a un nuovo nodo nella console.  

### <a name="reconfigure-database-replicas-for-management-points"></a>Riconfigurare le repliche di database per i punti di gestione

Dopo aver aggiornato un sito primario, riconfigurare la replica di database per i punti di gestione disinstallati prima dell'aggiornamento del sito. Per altre informazioni, vedere [Repliche di database per i punti di gestione](../deploy/configure/database-replicas-for-management-points.md).  

### <a name="reconfigure-sql-server-alwayson-availability-groups"></a>Riconfigurare i gruppi di disponibilità SQL Server AlwaysOn

Se si usa un gruppo di disponibilità, reimpostare la configurazione di failover su automatico. Per altre informazioni, vedere [Server AlwaysOn per database del sito](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).<!-- SCCMDocs #1366 -->

### <a name="reconfigure-any-disabled-maintenance-tasks"></a>Riconfigurare le attività di manutenzione disabilitate

Se si sono disabilitate le [attività di manutenzione](maintenance-tasks.md) del database in un sito prima dell'installazione dell'aggiornamento, riconfigurare tali attività. Usare le stesse impostazioni presenti prima dell'aggiornamento.  

### <a name="update-clients"></a>Aggiornare i client

Aggiornare i client in base al piano creato, in particolare se è stata configurata la distribuzione client pilota prima di installare l'aggiornamento. Per altre informazioni, vedere [Come aggiornare i client per i computer Windows in System Center Configuration Manager](../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

### <a name="third-party-extensions"></a>Estensioni di terze parti

Se si usano estensioni di Configuration Manager, eseguire l'aggiornamento alla versione più recente per supportare Configuration Manager versione 2002.

### <a name="update-custom-boot-images-and-media"></a>Aggiornare le immagini di avvio e i supporti personalizzati

<!--SCCMDocs issue 775-->

Usare l'azione **Aggiorna punti di distribuzione** per qualsiasi immagine di avvio usata, sia che si tratti di un'immagine di avvio predefinita o personalizzata. Questa azione assicura che i client possano usare la versione più recente. Anche se non è disponibile una nuova versione di Windows ADK, i componenti client di Configuration Manager possono cambiare con un aggiornamento. Se non si aggiornano le immagini di avvio e i supporti, le distribuzioni della sequenza attività potrebbero non riuscire nei dispositivi.

Quando si aggiorna il sito, Configuration Manager aggiorna automaticamente le immagini di avvio *predefinite*. Non distribuisce automaticamente il contenuto aggiornato ai punti di distribuzione. Usare l'azione **Aggiorna punti di distribuzione** sulle immagini di avvio specifiche quando si è pronti per distribuire il contenuto in rete.

Aggiornare manualmente eventuali immagini di avvio *personalizzate* dopo l'aggiornamento del sito. Questa azione aggiorna l'immagine di avvio con i componenti client più recenti, se necessario, la ricarica facoltativamente con la versione corrente di Windows PE e ridistribuisce il contenuto ai punti di distribuzione.

Per altre informazioni, vedere [Aggiornare il contenuto nei punti di distribuzione](../../../osd/get-started/manage-boot-images.md#update-distribution-points-with-the-boot-image).
