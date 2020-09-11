---
title: SQL Server Always On
titleSuffix: Configuration Manager
description: Pianificare l'uso di un gruppo di disponibilità Always On di SQL Server con Configuration Manager
ms.date: 07/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 58d52fdc-bd18-494d-9f3b-ccfc13ea3d35
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5e9c911929dd5a99c6b63beed9c6b221e69e9b25
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/09/2020
ms.locfileid: "89607552"
---
# <a name="prepare-to-use-sql-server-always-on-availability-groups-with-configuration-manager"></a>Preparare l'uso di gruppi di disponibilità Always On di SQL Server con Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Usare questo articolo per preparare Configuration Manager per l'uso di gruppi di disponibilità Always On di SQL Server. Questa funzionalità fornisce una soluzione di disponibilità elevata e ripristino di emergenza per il database del sito.  

Configuration Manager supporta l'uso di gruppi di disponibilità:

- nei siti primari e nel sito di amministrazione centrale;
- in locale o in Microsoft Azure.

Quando si usano i gruppi di disponibilità in Microsoft Azure, è possibile aumentare ulteriormente la disponibilità del database del sito con i *set di disponibilità di Azure*. Per altre informazioni sui set di disponibilità di Azure, vedere [Gestione della disponibilità delle macchine virtuali](/azure/virtual-machines/windows/manage-availability).

> [!Important]
> Prima di continuare, acquisire familiarità con la configurazione di SQL Server e dei gruppi di disponibilità di SQL Server. Le informazioni seguenti fanno riferimento alla libreria della documentazione e alle procedure relative a SQL Server.


## <a name="supported-scenarios"></a>Scenari supportati

Di seguito sono riportati gli scenari supportati per l'uso di gruppi di disponibilità con Configuration Manager. Per altre informazioni e procedure per ogni scenario, vedere [Configurare i gruppi di disponibilità per Configuration Manager](configure-aoag.md).

- [Creare un gruppo di disponibilità per l'uso con Configuration Manager](configure-aoag.md#bkmk_create)  
- [Configurare un sito per l'uso del gruppo di disponibilità](configure-aoag.md#bkmk_configure)  
- [Aggiungere e rimuovere i membri di una replica sincrona da un gruppo di disponibilità che ospita un database del sito](configure-aoag.md#bkmk_sync)  
- [Configurare o ripristinare un sito da una replica con commit asincrono](configure-aoag.md#bkmk_async)  
- [Spostare un database del sito da un gruppo di disponibilità a un'istanza predefinita o denominata di SQL Server autonomo](configure-aoag.md#bkmk_stop)  


## <a name="prerequisites"></a>Prerequisiti

I prerequisiti seguenti si applicano a tutti gli scenari. Se a uno scenario si applicano prerequisiti aggiuntivi, i dettagli verranno forniti con lo scenario specifico.

### <a name="configuration-manager-accounts-and-permissions"></a>Account e autorizzazioni di Configuration Manager

#### <a name="installation-account"></a>Account di installazione

L'account usato per eseguire il programma di installazione di Configuration Manager deve:

- Essere membro del gruppo **Administrators** locale in ogni computer membro del gruppo di disponibilità.
- Essere **amministratore di sistema** in ogni istanza di SQL Server che ospita il database del sito.

#### <a name="site-server-to-replica-member-access"></a>Server del sito per l'accesso ai membri di replica

L'account computer del server del sito deve essere un membro del gruppo **Administrators** locale in tutti i computer membri del gruppo di disponibilità.

### <a name="sql-server"></a>SQL Server

#### <a name="version"></a>Version

Ogni replica nel gruppo di disponibilità deve eseguire una versione di SQL Server supportata dalla versione in uso di Configuration Manager. Se supportati da SQL Server, nodi diversi di un gruppo di disponibilità possono eseguire versioni diverse di SQL Server. Per altre informazioni, vedere [Versioni di SQL Server supportate per Configuration Manager](../../../plan-design/configs/support-for-sql-server-versions.md).<!--SCCMDocs issue 656-->

#### <a name="edition"></a>Edizione

Usare un'edizione *Enterprise* di SQL Server.

#### <a name="account"></a>Account

Ogni istanza di SQL Server può essere eseguita con un account utente di dominio (**account del servizio**) o con un account non di dominio. Ogni replica in un gruppo può avere una configurazione diversa.

- Usare un account con autorizzazioni minime. Per altre informazioni, vedere [Considerazioni sulla sicurezza per un'installazione di SQL Server](/sql/sql-server/install/security-considerations-for-a-sql-server-installation).  

- Per altre informazioni sulla configurazione degli account del servizio e delle autorizzazioni per SQL Server, vedere [Configurare account di servizio e autorizzazioni di Windows](/sql/database-engine/configure-windows/configure-windows-service-accounts-and-permissions).  

- Per usare un account non di dominio, sono necessari certificati. Per altre informazioni, vedere [Utilizzare certificati per un endpoint del mirroring del database (Transact-SQL)](/sql/database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql).  

- Per altre informazioni vedere [Creare un endpoint del mirroring del database per i gruppi di disponibilità Always On](/sql/database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell).  


### <a name="database"></a>Database

#### <a name="configure-the-database-on-a-new-replica"></a>Configurare il database su una nuova replica

Configurare il database di ogni replica con le impostazioni seguenti:  

- Abilitare **Integrazione CLR**:

    ``` SQL
    sp_configure 'show advanced options', 1;  
    GO  
    RECONFIGURE;  
    GO  
    sp_configure 'clr enabled', 1;  
    GO  
    RECONFIGURE;  
    GO
    ```

    Per altre informazioni, vedere [Integrazione CLR](/sql/relational-databases/clr-integration/clr-integration-enabling).  

- Impostare **Max text repl size** su `2147483647`:  

    ``` SQL
    EXECUTE sp_configure 'max text repl size (B)', 2147483647
    ```

- Impostare il proprietario del database su *Account amministratore di sistema*. Non è necessario abilitare questo account.

- **Attivare** l'impostazione **TRUSTWORTHY**:

    ``` SQL
    ALTER DATABASE [CM_xxx] SET TRUSTWORTHY ON;
    ```

    Per altre informazioni, vedere [Proprietà di database TRUSTWORTHY](/sql/relational-databases/security/trustworthy-database-property).

- Abilitare **Service Broker**:  

    ``` SQL
    ALTER DATABASE [CM_xxx] SET ENABLE_BROKER
    ```

    > [!Note]  
    > Non è possibile abilitare l'opzione Service Broker per un database che fa già parte di un gruppo di disponibilità. È necessario abilitare questa opzione prima di aggiungere il database al gruppo di disponibilità.<!-- SCCMDocs#1432 -->

- Configurare la priorità di Service Broker:

    ``` SQL
    ALTER DATABASE [CM_xxx] SET HONOR_BROKER_PRIORITY ON;
    ALTER DATABASE [CM_xxx] SET ENABLE_BROKER WITH ROLLBACK IMMEDIATE

    ```

Creare queste configurazioni solo su una replica primaria. Per configurare una replica secondaria, effettuare prima il failover dalla replica primaria a quella secondaria. Questa azione trasforma la replica secondaria nella nuova replica primaria.

#### <a name="database-verification-script"></a>Script di verifica del database

Eseguire lo script SQL seguente per verificare le configurazioni di database per le repliche primaria e secondaria. Prima di risolvere un problema su una replica secondaria, è necessario trasformare tale replica secondaria in replica primaria.

``` SQL
    SET NOCOUNT ON

    DECLARE @dbname NVARCHAR(128)

    SELECT @dbname = sd.name FROM sys.sysdatabases sd WHERE sd.dbid = DB_ID()

    IF (@dbname = N'master' OR @dbname = N'model' OR @dbname = N'msdb' OR @dbname = N'tempdb' OR @dbname = N'distribution' ) BEGIN
    RAISERROR(N'ERROR: Script is targeting a system database.  It should be targeting the DB you created instead.', 0, 1)
    GOTO Branch_Exit;
    END ELSE
    PRINT N'INFO: Targeted database is ' + @dbname + N'.'

    PRINT N'INFO: Running verifications....'

    IF NOT EXISTS (SELECT * FROM sys.configurations c WHERE c.name = 'clr enabled' AND c.value_in_use = 1)
    PRINT N'ERROR: CLR is not enabled!'
    ELSE
    PRINT N'PASS: CLR is enabled.'

    DECLARE @repltable TABLE (
    name nvarchar(max),
    minimum int,
    maximum int,
    config_value int,
    run_value int )

    INSERT INTO @repltable
    EXEC sp_configure 'max text repl size (B)'

    IF NOT EXISTS(SELECT * from @repltable where config_value = 2147483647 and run_value = 2147483647 )
    PRINT N'ERROR: Max text repl size is not correct!'
    ELSE
    PRINT N'PASS: Max text repl size is correct.'

    IF NOT EXISTS (SELECT db.owner_sid FROM sys.databases db WHERE db.database_id = DB_ID() AND db.owner_sid = 0x01)
    PRINT N'ERROR: Database owner is not sa account!'
    ELSE
    PRINT N'PASS: Database owner is sa account.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_trustworthy_on = 1 )
    PRINT N'ERROR: Trustworthy bit is not on!'
    ELSE
    PRINT N'PASS: Trustworthy bit is on.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_broker_enabled = 1 )
    PRINT N'ERROR: Service broker is not enabled!'
    ELSE
    PRINT N'PASS: Service broker is enabled.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_honor_broker_priority_on = 1 )
    PRINT N'ERROR: Service broker priority is not set!'
    ELSE
    PRINT N'PASS: Service broker priority is set.'

    PRINT N'Done!'

    Branch_Exit:
```


### <a name="availability-group-configurations"></a>Configurazioni dei gruppi di disponibilità

#### <a name="replica-members"></a>Membri di replica

- Il gruppo di disponibilità deve avere una sola replica primaria.  

- In un gruppo di disponibilità usare lo stesso numero e lo stesso tipo di repliche supportati dalla versione di SQL Server in uso.

- Per ripristinare la replica sincrona, è possibile usare la replica con commit asincrono. Per altre informazioni, vedere [Opzioni di ripristino del database del sito](../../manage/recover-sites.md#site-database-recovery-options).  

    > [!Warning]  
    > Configuration Manager non supporta il *failover* per l'uso della replica con commit asincrono come database del sito. Per altre informazioni, vedere [Failover e modalità di failover (gruppi di disponibilità AlwaysOn)](/sql/database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups).  

Configuration Manager non convalida lo stato della replica con commit asincrono per verificare che sia aggiornato. L'uso di una replica con commit asincrono come database del sito può mettere a rischio l'integrità del sito e dei dati. Una replica di questo tipo potrebbe non essere sincronizzata. Per altre informazioni, vedere [Panoramica di Gruppi di disponibilità AlwaysOn (SQL Server)](/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server).

Ogni membro di replica deve avere la configurazione seguente:

- Deve usare l'*istanza predefinita* o un'*istanza denominata*  

- L'opzione **Connessioni nel ruolo primario** deve essere impostata su **Consenti tutte le connessioni**  

- L'opzione **Secondario leggibile** deve essere impostata su **Sì**  

- **Failover manuale** deve essere abilitato

    > [!Note]
    > Nella versione 1902 e precedenti è necessario configurare tutti i gruppi di disponibilità in SQL Server per il failover manuale. Questa configurazione è necessaria anche se non ospita il database del sito.
    >
    > A partire dalla versione 1906 Configuration Manager supporta l'uso di repliche sincrone del gruppo di disponibilità se è stata scelta l'impostazione **Failover automatico**. Impostare **Failover manuale** quando:
    >
    > - Si esegue il programma di installazione di Configuration Manager per specificare l'uso del database del sito nel gruppo di disponibilità.  
    > - Si installa un qualsiasi aggiornamento di Configuration Manager (non solo gli aggiornamenti che si applicano al database del sito).  

- Tutti i membri devono usare la stessa [modalità di seeding](/sql/database-engine/availability-groups/windows/automatic-seeding-secondary-replicas).<!-- SCCMDocs-pr#3899 --> Il programma di installazione di Configuration Manager include un controllo dei prerequisiti per verificare questa configurazione quando si crea un database usando l'installazione o il ripristino.

    > [!Note]  
    > Quando il programma di installazione crea il database e si configura il seeding **automatico**, il gruppo di disponibilità deve avere le autorizzazioni necessarie per creare il database. Questo requisito si applica sia a un nuovo database che a un nuovo ripristino. Per altre informazioni, vedere l'articolo sul [seeding automatico per la replica secondaria](/sql/database-engine/availability-groups/windows/automatic-seeding-secondary-replicas#security).<!-- SCCMDocs-pr#3900 -->

#### <a name="replica-member-location"></a>Percorso dei membri della replica

Tutte le repliche in un gruppo di disponibilità devono essere ospitate in locale o in Microsoft Azure. Non sono supportati gruppi che includono un membro locale e un membro in Azure.

> [!NOTE]
> Se per SQL Server si usa una macchina virtuale di Azure, abilitare **Floating IP**. Per altre informazioni, vedere [Configurare un servizio di bilanciamento del carico per un gruppo di disponibilità SQL Server Always On in macchine virtuali di Azure](/azure/azure-sql/virtual-machines/windows/availability-group-load-balancer-portal-configure).<!-- SCCMDocs#1928 -->

Il programma di installazione di Configuration Manager deve connettersi a ogni replica. Quando si imposta un gruppo di disponibilità in Azure e il gruppo si trova dietro un bilanciamento del carico interno o esterno, aprire le seguenti porte predefinite:

- Mapper di endpoint RPC: **TCP 135**

- SQL Server Service Broker: **TCP 4022**  

- SQL su TCP: **TCP 1433**

Al termine dell'installazione, le porte seguenti devono rimanere aperte per Configuration Manager e Replication Link Analyzer.<!-- MEMDocs#375 -->

È possibile usare porte personalizzate per queste configurazioni. Usare le stesse porte personalizzate usate dall'endpoint e in tutte le repliche nel gruppo di disponibilità.

Per la replica SQL dei dati tra i siti, creare una regola di bilanciamento del carico per ogni porta nel servizio di bilanciamento del carico di Azure. Per altre informazioni, vedere [Configurare le porte a disponibilità elevata per un bilanciamento del carico interno](/azure/load-balancer/load-balancer-configure-ha-ports).<!-- MEMDocs#252 -->

#### <a name="listener"></a>Listener

Il gruppo di disponibilità deve avere almeno un *listener del gruppo di disponibilità*. Il nome virtuale di questo listener viene usato quando si configura Configuration Manager per usare il database del sito nel gruppo di disponibilità. Anche se un gruppo di disponibilità può contenere più listener, Configuration Manager può usarne solo uno. Per altre informazioni, vedere [Creare o configurare un listener del gruppo di disponibilità (SQL Server)](/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server).

#### <a name="file-paths"></a>Percorsi di file

Quando si esegue il programma di installazione di Configuration Manager per configurare un sito per l'uso del database in un gruppo di disponibilità, ogni server di replica secondaria deve avere un percorso di file di SQL Server identico a quello dei file di database del sito nella replica primaria corrente. Se non esiste un percorso identico, non sarà possibile aggiungere l'istanza per il gruppo di disponibilità come nuovo percorso del database del sito.  

L'account del servizio di SQL Server locale deve avere l'autorizzazione **Controllo completo** per questa cartella.

I server di replica secondaria richiedono questo percorso file solo durante l'installazione di Configuration Manager per specificare l'istanza di database nel gruppo di disponibilità. Una volta completata la configurazione del database del sito nel gruppo di disponibilità, è possibile eliminare il percorso inutilizzato dai server di replica secondari.

Prendere ad esempio in considerazione i seguenti scenari:

- Si crea un gruppo di disponibilità che usa tre server SQL.  

- Il server di replica primaria è una nuova installazione di SQL Server 2014. Per impostazione predefinita, archivia i file MDF e LDF del database in `C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA`.  

- Entrambi i server di replica secondaria sono stati aggiornati a SQL Server 2014 dalle versioni precedenti. Con l'aggiornamento, questi server mantengono il percorso originale per archiviare i file di database: `C:\Program Files\Microsoft SQL Server\MSSQL10.MSSQLSERVER\MSSQL\DATA`.  

- Prima di spostare il database del sito in questo gruppo di disponibilità, in ogni server di replica secondaria creare il percorso di file seguente: `C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA`. Questo percorso è un duplicato del percorso usato nella replica primaria, anche se le repliche secondarie non lo useranno.  

- È quindi possibile concedere all'account del servizio SQL Server in ogni replica secondaria l'accesso con controllo completo al percorso di file appena creato nel server.  

- È ora possibile eseguire correttamente l'installazione di Configuration Manager per configurare il sito in modo che usi il database del sito nel gruppo di disponibilità.  

#### <a name="multi-subnet-failover"></a>Failover su più subnet

<!-- SCCMDocs-pr#3734 -->
A partire dalla versione 1906, è possibile abilitare la [parola chiave della stringa di connessione MultiSubnetFailover](/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server#MultiSubnetFailover) in SQL Server. È anche necessario aggiungere manualmente i valori seguenti al Registro di sistema di Windows nel server del sito:

``` Registry
HKLM:\SOFTWARE\Microsoft\SMS\Identification
HKLM:\SOFTWARE\Microsoft\SMS\SQL Server

MSF Enabled : 1 (DWORD)
```

> [!Warning]  
> L'uso della [disponibilità elevata del server del sito](site-server-high-availability.md) e di SQL Server Always On con il failover su più subnet non offre le funzionalità complete del failover automatico per le situazioni di ripristino di emergenza.

Se è necessario creare un gruppo di disponibilità con un membro in una posizione remota, assegnare la priorità in base alla latenza di rete più bassa. Una latenza di rete elevata può causare errori di replica.<!-- SCCMDocs#1381 -->


## <a name="limitations-and-known-issues"></a>Limitazioni e problemi noti

Le limitazioni seguenti si applicano a tutti gli scenari.

### <a name="unsupported-sql-server-options-and-configurations"></a>Opzioni e configurazioni di SQL Server non supportate

- **Gruppi di disponibilità di base**: introdotti con SQL Server 2016 Standard Edition, i gruppi di disponibilità di base non supportano l'accesso in lettura alle repliche secondarie, requisito essenziale per l'uso con Configuration Manager. Per altre informazioni, vedere [Gruppi di disponibilità di base (gruppi di disponibilità AlwaysOn)](/sql/database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups).  

- **Istanza del cluster di failover**: le istanze del cluster di failover non sono supportate per una replica usata con Configuration Manager. Per altre informazioni, vedere [Istanze del cluster di failover AlwaysOn (SQL Server)](/sql/sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server).  

- **MultiSubnetFailover**: Nella versione 1902 e nelle versioni precedenti l'uso di un gruppo di disponibilità con Configuration Manager in una configurazione con più subnet non è supportato. Non è possibile usare nemmeno la stringa di connessione tramite parola chiave [MultiSubnetFailover](/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server#MultiSubnetFailover).

    Per supportare questa configurazione, aggiornare Configuration Manager alla versione 1906 o a versioni successive. Per altre informazioni, vedere il prerequisito relativo al [failover su più subnet](sql-server-alwayson-for-a-highly-available-site-database.md#multi-subnet-failover).

### <a name="sql-servers-that-host-additional-availability-groups"></a>Istanze di SQL Server che ospitano gruppi di disponibilità aggiuntivi

<!--SCCMDocs issue 649-->
Quando SQL Server ospita uno o più gruppi di disponibilità oltre a quello usato per Configuration Manager, al momento dell'esecuzione del programma di installazione di Configuration Manager sono necessarie impostazioni specifiche. Queste impostazioni sono necessarie anche per installare un aggiornamento per Configuration Manager. Ogni replica in ogni gruppo di disponibilità deve avere le configurazioni seguenti:

- Failover manuale  
- Connessioni di sola lettura consentite  

> [!Note]
> Nella versione 1902 e precedenti è necessario configurare tutti i gruppi di disponibilità in SQL Server per il failover manuale. Questa configurazione è necessaria anche se non ospita il database del sito.
>
> A partire dalla versione 1906 Configuration Manager supporta l'uso di repliche sincrone del gruppo di disponibilità se è stata scelta l'impostazione **Failover automatico**. Impostare **Failover manuale** quando:
>
> - Si esegue il programma di installazione di Configuration Manager per specificare l'uso del database del sito nel gruppo di disponibilità.  
> - Si installa un qualsiasi aggiornamento di Configuration Manager (non solo gli aggiornamenti che si applicano al database del sito).  

### <a name="unsupported-database-use"></a>Uso di database non supportati

#### <a name="configuration-manager-supports-only-the-site-database-in-an-availability-group"></a>Configuration Manager supporta solo il database del sito in un gruppo di disponibilità

i database seguenti non sono supportati da Configuration Manager in un gruppo di disponibilità Always On di SQL Server:  

- Database di report  
- Database WSUS  

#### <a name="pre-existing-database"></a>Database preesistente

non è possibile usare un nuovo database creato nella replica. Quando si configura un gruppo di disponibilità, ripristinare una copia di un database di Configuration Manager esistente nella replica primaria.  

#### <a name="distributed-views"></a>Viste distribuite

<!-- SCCMDocs-pr#3792 -->
Nella versione 1902 e versioni precedenti, se si ospita il database del sito in un gruppo di disponibilità SQL Server Always On, non è possibile abilitare le [viste distribuite](../../../plan-design/hierarchy/data-transfers-between-sites.md#bkmk_dbrep) per la replica di database. Per supportare questa configurazione, eseguire l'aggiornamento alla versione 1906 o a versioni successive.


### <a name="setup-errors-in-configmgrsetuplog"></a>Errori di configurazione in ConfigMgrSetup.log

Quando si esegue il programma di installazione di Configuration Manager per spostare un database del sito in un gruppo di disponibilità, il programma tenta di elaborare i ruoli del database nelle repliche secondarie del gruppo di disponibilità. Il file **ConfigMgrSetup.log** mostra l'errore seguente:  

`ERROR: SQL Server error: [25000][3906][Microsoft][SQL Server Native Client 11.0][SQL Server]Failed to update database "CM_AAA" because the database is read-only. Configuration Manager Setup 1/21/2016 4:54:59 PM 7344 (0x1CB0)`  

Ignorare questi errori.

### <a name="site-expansion"></a>Espansione del sito

<!--SCCMDocs issue 568-->
Se si configura il database del sito per un sito primario autonomo in modo che usi SQL Always On, non è possibile espandere il sito per includere un sito di amministrazione centrale. Se si cerca di eseguire questo processo, l'esito è negativo. Per espandere il sito, rimuovere temporaneamente il database del sito primario dal gruppo di disponibilità.

Quando si aggiunge un sito secondario, non è necessario apportare alcuna modifica alla configurazione.


## <a name="changes-for-site-backup"></a>Modifiche per il backup del sito

### <a name="backup-database-files"></a>Eseguire il backup dei file di database
  
Quando un database del sito usa un gruppo di disponibilità, eseguire l'attività di manutenzione predefinita **Backup server sito** per eseguire il backup di impostazioni e file comuni di Configuration Manager. Non usare i file MDF o LDF creati dal backup. Eseguire invece backup diretti di questi file del sito usando SQL Server.

### <a name="transaction-log"></a>Log delle transazioni  

Impostare il modello di recupero del database del sito su **Completo**. Questa configurazione è un requisito necessario per usare Configuration Manager in un gruppo di disponibilità. Pianificare il monitoraggio e la gestione delle dimensioni del log delle transazioni del database del sito. Nel modello di recupero Completo le transazioni non vengono finalizzate fino a quando non viene eseguito un backup completo del database o del log delle transazioni. Per altre informazioni, vedere [Backup e ripristino di database SQL Server](/sql/relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases).


## <a name="changes-for-site-recovery"></a>Modifiche per il ripristino del sito

Se almeno uno dei nodi del gruppo di disponibilità continua a funzionare, usare l'opzione di ripristino del sito **Ignora ripristino database (utilizzare questa opzione se non si sono verificati errori nel database del sito)** .

A partire dalla versione 1906, con il ripristino del sito è possibile ricreare il database in un gruppo SQL Always On. Questo processo funziona con il seeding sia manuale che automatico.<!-- SCCMDocs-pr#3846 -->

Nella versione 1902 e nelle versioni precedenti se tutti i nodi di un gruppo di disponibilità sono andati perduti, prima di poter ripristinare il sito è necessario ricreare il gruppo di disponibilità. Configuration Manager non è in grado di ricompilare o ripristinare il nodo di disponibilità. Ricreare il gruppo, ripristinare il backup e riconfigurare SQL. Quindi usare l'opzione di ripristino sito **Ignora ripristino database (utilizzare questa opzione se non si sono verificati errori nel database del sito)** .

Per altre informazioni, vedere [Backup e ripristino](../../manage/backup-and-recovery.md).


## <a name="changes-for-reporting"></a>Modifiche per la creazione di report

### <a name="install-the-reporting-service-point"></a>Installare il punto di Reporting Services

Il punto di Reporting Services non supporta l'uso del nome virtuale del listener del gruppo di disponibilità, né l'hosting del relativo database in un gruppo di disponibilità Always On di SQL Server.  

- Per impostazione predefinita, l'installazione del punto di Reporting Services imposta il **nome del server del database del sito** sul nome virtuale specificato come listener. Modificare questa impostazione per specificare un nome computer e l'istanza di una replica nel gruppo di disponibilità.  

- Per eseguire l'offload della creazione di report e aumentare la disponibilità quando un nodo di replica è offline, prendere in considerazione l'installazione di altri punti di Reporting Services in ogni nodo di replica. Quindi configurare ogni punto di Reporting Services in modo che usi il proprio nome computer. Quando si installa un punto di Reporting Services in ogni replica del gruppo di disponibilità, il reporting può sempre connettersi a un server del punto di reporting attivo.  

### <a name="switch-the-reporting-services-point-used-by-the-console"></a>Cambiare il punto di Reporting Services usato dalla console

1. Nella console di Configuration Manager passare all'area di lavoro **Monitoraggio**, espandere **Report** e selezionare il nodo **Report**.

1. Nella barra multifunzione selezionare **Opzioni rapporti**.  

1. Nella finestra di dialogo Opzioni rapporti selezionare il punto di Reporting Services da usare.  


## <a name="next-steps"></a>Passaggi successivi

Questo articolo descrive i prerequisiti, le limitazioni e le modifiche alle attività comuni richiesti da Configuration Manager quando si usano i gruppi di disponibilità. Per le procedure di installazione e configurazione del sito per l'uso dei gruppi di disponibilità, vedere [Configurare gruppi di disponibilità](configure-aoag.md).