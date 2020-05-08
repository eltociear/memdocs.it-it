---
title: Versioni di SQL Server supportate
titleSuffix: Configuration Manager
description: Requisiti di configurazione e della versione di SQL Server per l'hosting di un database del sito di Configuration Manager.
ms.date: 04/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 35e237b6-9f7b-4189-90e7-8eca92ae7d3d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3c52008089a6d23d5c4efe44f0970bb186eb334a
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82904641"
---
# <a name="supported-sql-server-versions-for-configuration-manager"></a>Versioni di SQL Server supportate per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Ogni sito di Configuration Manager richiede una versione e una configurazione di SQL Server supportate per ospitare il database del sito.  

## <a name="sql-server-instances-and-locations"></a><a name="bkmk_Instances"></a> Istanze e percorsi di SQL Server

### <a name="central-administration-site-and-primary-sites"></a>Sito di amministrazione centrale e siti primari

Il database del sito deve usare un'installazione completa di SQL Server.  

SQL Server può trovarsi:  

- Nel computer del server del sito.  
- In un computer remoto rispetto al server del sito.  

Sono supportate le istanze seguenti:  

- Istanza predefinita o denominata di SQL Server.  
- Configurazioni a più istanze.  
- Cluster SQL Server. Vedere [Usare un cluster SQL Server per ospitare il database del sito](../../servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md).
- Gruppo di disponibilità SQL Server AlwaysOn. Per altre informazioni, vedere [Preparare l'uso di gruppi di disponibilità Always On di SQL Server](../../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

### <a name="secondary-sites"></a>Siti secondari

Il database del sito può usare l'istanza predefinita di un'installazione completa di SQL Server o SQL Server Express.  

È necessario che SQL Server si trovi nel computer del server del sito.  

### <a name="limitations-to-support"></a>Limitazioni al supporto

Le configurazioni seguenti non sono supportate:

- Un cluster SQL Server in una configurazione cluster Bilanciamento carico di rete (NLB)
- Un cluster SQL Server cluster in un Volume condiviso cluster
- La tecnologia di mirroring e la replica peer-to-peer del database di SQL Server

La replica transazionale di SQL Server è supportata solo per la replica di oggetti ai punti di gestione configurati per l'uso delle [repliche di database](../../servers/deploy/configure/database-replicas-for-management-points.md).  

## <a name="supported-versions-of-sql-server"></a><a name="bkmk_SQLVersions"></a> Versioni supportate di SQL Server

In una gerarchia con più siti, diversi siti possono usare versioni diverse di SQL Server per ospitare il database del sito, purché siano vere le condizioni seguenti:

- Configuration Manager supporta le versioni di SQL Server usate.
- Le versioni di SQL Server usate sono supportate da Microsoft.
- SQL Server supporta la replica tra le due versioni di SQL Server. Per altre informazioni, vedere [Compatibilità con le versioni precedenti della replica di SQL Server](https://docs.microsoft.com/sql/relational-databases/replication/replication-backward-compatibility).

Per SQL Server 2016 e versioni precedenti, il supporto per ogni versione di SQL e Service Pack segue i [criteri del ciclo di vita Microsoft](https://aka.ms/sqllifecycle). Il supporto per un Service Pack di SQL Server specifico include gli aggiornamenti cumulativi, a meno che non interrompano la compatibilità con la versione di base del Service Pack. A partire da SQL Server 2017, i Service Pack non verranno rilasciati perché segue un [modello di manutenzione moderno](https://docs.microsoft.com/archive/blogs/sqlreleaseservices/announcing-the-modern-servicing-model-for-sql-server). Il team di SQL Server consiglia l'[installazione proattiva continua degli aggiornamenti cumulativi](https://docs.microsoft.com/archive/blogs/sqlreleaseservices/announcing-updates-to-the-sql-server-incremental-servicing-model-ism) non appena diventano disponibili.

Se non specificato diversamente, le versioni seguenti di SQL Server sono supportate con tutte le versioni attive di Configuration Manager. Se viene aggiunto il supporto per una nuova versione di SQL Server, viene indicata la versione di Configuration Manager che aggiunge tale supporto. Analogamente, se il supporto è deprecato, cercare i dettagli relativi alle versioni di Configuration Manager interessate.

> [!IMPORTANT]  
> Se si usa SQL Server Standard per il database nel sito di amministrazione centrale, si limita il numero totale di client che una gerarchia può supportare. Vedere [Numeri di ridimensionamento e scalabilità](size-and-scale-numbers.md).

### <a name="sql-server-2019-standard-enterprise"></a>SQL Server 2019: Standard, Enterprise

A partire da Configuration Manager versione 1910, è possibile usare questa versione con qualsiasi aggiornamento cumulativo, purché la versione dell'aggiornamento cumulativo sia supportata dal ciclo di vita di SQL.

Questa versione di SQL può essere usata per i siti seguenti:

- sito di amministrazione centrale
- sito primario
- sito secondario

#### <a name="known-issue-with-sql-server-2019"></a>Problema noto con SQL Server 2019

Esiste un problema noto<!--6436234--> con la nuova funzionalità di [inlining delle funzioni definite dall'utente scalari](https://docs.microsoft.com/sql/relational-databases/user-defined-functions/scalar-udf-inlining) in SQL 2019. Per ovviare a questo problema e disabilitare l'inlining delle funzioni definite dall'utente, eseguire lo script seguente nel server SQL 2019:

```sql
ALTER DATABASE SCOPED CONFIGURATION SET TSQL_SCALAR_UDF_INLINING = OFF  
```

Sebbene non sia sempre necessario, potrebbe essere necessario riavviare SQL Server dopo l'esecuzione dello script. Per altre informazioni, vedere [Disabilitazione dell'inlining di funzioni definite dall'utente scalari senza modificare il livello di compatibilità](https://docs.microsoft.com/sql/relational-databases/user-defined-functions/scalar-udf-inlining?view=sql-server-ver15#disabling-scalar-udf-inlining-without-changing-the-compatibility-level).

È possibile disabilitare in modo sicuro questa funzionalità SQL per il server di database del sito perché Configuration Manager non la usa.

Se non si disabilita l'inlining delle funzioni definite dall'utente scalari in SQL 2019, nel server del sito si verificheranno errori casuali durante l'esecuzione di query sul database del sito. Ad esempio, verranno visualizzati gli errori seguenti in **hman.log**:

```hman.log
*** [HY000][0][Microsoft][SQL Server Native Client 11.0]Unspecified error occurred on SQL Server. Connection may have been terminated by the server.
*** select dbo.fnGetSiteMode(dbo.fnGetSiteCode())
*** [HY000][596][Microsoft][SQL Server Native Client 11.0][SQL Server]Cannot continue the execution because the session is in the kill state.
Failed to execute SQL command select dbo.fnGetSiteMode(dbo.fnGetSiteCode())
```

È possibile che vengano visualizzati errori simili in altri log, ad esempio **SmsAdminUI.log**.

SQL Server versione 2019 registra l'errore seguente:

`Microsoft SQL Server reported SQL message 596, severity 21: [HY000][596][Microsoft][SQL Server Native Client 11.0][SQL Server]Cannot continue the execution because the session is in the kill state.`

Verranno visualizzati anche dump di arresto anomalo del sistema (file `.mdump`) da SQL nella relativa directory dei log, che per impostazione predefinita è `C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\Log`.

### <a name="sql-server-2017-standard-enterprise"></a>SQL Server 2017: Standard, Enterprise

È possibile usare questa versione con la [versione 2 dell'aggiornamento cumulativo](https://support.microsoft.com/help/4052574) o versione successiva, purché la versione dell'aggiornamento cumulativo sia supportata dal ciclo di vita di SQL. Questa versione di SQL può essere usata per i siti seguenti:

- sito di amministrazione centrale  
- sito primario  
- sito secondario  
  <!--SMS.498506-->

### <a name="sql-server-2016-standard-enterprise"></a>SQL Server 2016: Standard, Enterprise  
<!--514985-->
È possibile usare questa versione con il Service Pack minimo e l'aggiornamento cumulativo supportato dal ciclo di vita di SQL. Questa versione di SQL può essere usata per i siti seguenti:

- sito di amministrazione centrale  
- sito primario  
- sito secondario  

### <a name="sql-server-2014-standard-enterprise"></a>SQL Server 2014: Standard, Enterprise

È possibile usare questa versione con il Service Pack minimo e l'aggiornamento cumulativo supportato dal ciclo di vita di SQL. Questa versione di SQL può essere usata per i siti seguenti:

- sito di amministrazione centrale  
- sito primario  
- sito secondario

### <a name="sql-server-2012-standard-enterprise"></a>SQL Server 2012: Standard, Enterprise

È possibile usare questa versione con il Service Pack minimo e l'aggiornamento cumulativo supportato dal ciclo di vita di SQL. Questa versione di SQL può essere usata per i siti seguenti:

- sito di amministrazione centrale  
- sito primario  
- sito secondario  

### <a name="sql-server-2017-express"></a>SQL Server 2017 Express

È possibile usare questa versione con la [versione 2 dell'aggiornamento cumulativo](https://support.microsoft.com/help/4052574) o versione successiva, purché la versione dell'aggiornamento cumulativo sia supportata dal ciclo di vita di SQL. Questa versione di SQL può essere usata per i siti seguenti:

- sito secondario
<!--SMS.498506-->

### <a name="sql-server-2016-express"></a>SQL Server 2016 Express

È possibile usare questa versione con il Service Pack minimo e l'aggiornamento cumulativo supportato dal ciclo di vita di SQL. Questa versione di SQL può essere usata per i siti seguenti:

- sito secondario

### <a name="sql-server-2014-express"></a>SQL Server 2014 Express

È possibile usare questa versione con il Service Pack minimo e l'aggiornamento cumulativo supportato dal ciclo di vita di SQL. Questa versione di SQL può essere usata per i siti seguenti:

- sito secondario  

### <a name="sql-server-2012-express"></a>SQL Server 2012 Express

È possibile usare questa versione con il Service Pack minimo e l'aggiornamento cumulativo supportato dal ciclo di vita di SQL. Questa versione di SQL può essere usata per i siti seguenti:

- sito secondario  

## <a name="required-configurations-for-sql-server"></a><a name="bkmk_SQLConfig"></a> Configurazioni necessarie per SQL Server

Le configurazioni seguenti sono necessarie per tutte le installazioni di SQL Server usate per un database del sito, incluso SQL Server Express. Quando Configuration Manager installa SQL Server Express come parte dell'installazione di un sito secondario, crea automaticamente queste configurazioni.  

### <a name="sql-server-architecture-version"></a>Versione dell'architettura di SQL Server

Configuration Manager richiede una versione a 64 bit di SQL Server per ospitare il database del sito.  

### <a name="database-collation"></a>Regole di confronto del database

In ogni sito sia l'istanza di SQL Server usata per il sito che il database del sito devono usare le regole di confronto seguenti: **SQL_Latin1_General_CP1_CI_AS**.  

Configuration Manager supporta due eccezioni a queste regole di confronto per lo standard GB18030 per la Cina. Per altre informazioni, vedere [Supporto internazionale](../hierarchy/international-support.md).  

### <a name="database-compatibility-level"></a>Livello di compatibilità database

Configuration Manager richiede un livello di compatibilità per il database del sito non inferiore alla versione minima di SQL Server supportata per la versione di Configuration Manager. Ad esempio, a partire dalla versione 1702, è necessario avere un [livello di compatibilità del database](https://docs.microsoft.com/sql/relational-databases/databases/view-or-change-the-compatibility-level-of-a-database) maggiore o uguale a 110. <!-- SMS.506266-->

### <a name="sql-server-features"></a>Funzionalità di SQL Server

Solo la funzionalità **Servizi Motore di database** è necessaria per ogni server del sito.  

La replica di database di Configuration Manager non richiede la funzionalità di **replica di SQL Server**. Questa configurazione di SQL Server, tuttavia, è necessaria quando si usano [repliche di database per i punti di gestione](../../servers/deploy/configure/database-replicas-for-management-points.md).  

### <a name="windows-authentication"></a>Autenticazione di Windows

Configuration Manager richiede l' **autenticazione di Windows** per convalidare le connessioni al database.  

### <a name="sql-server-instance"></a>Istanza di SQL Server

Usare un'istanza dedicata di SQL Server per ogni sito. L'istanza può essere un'**istanza denominata** o un'**istanza predefinita**.  

### <a name="sql-server-memory"></a>Memoria di SQL Server

Riservare la memoria per SQL Server usando SQL Server Management Studio. Impostare la **memoria minima per il server** nelle **opzioni per la memoria del server**. Per altre informazioni su come configurare questa impostazione, vedere [Opzioni di configurazione del server Server Memory](https://docs.microsoft.com/sql/database-engine/configure-windows/server-memory-server-configuration-options).  

- **Per un server di database che si installa nello stesso computer del server del sito**: Limitare la memoria per SQL Server al 50-80% della memoria di sistema indirizzabile disponibile.  

- **Per un server di database dedicato e remoto dal computer del server del sito**: Limitare la memoria per SQL Server all'80-90% della memoria di sistema indirizzabile disponibile.  

- **Per una riserva di memoria per il pool di buffer di ogni istanza di SQL Server in uso**:  

  - Per un sito di amministrazione centrale: Impostare un minimo di 8 GB.  
  - Per un sito primario: Impostare un minimo di 8 GB.  
  - Per un sito secondario: Impostare un minimo di 4 GB.  

### <a name="sql-nested-triggers"></a>Trigger annidati SQL

I trigger nidificati SQL devono essere abilitati. Per altre informazioni, vedere [Configurare l'opzione di configurazione del server nested triggers](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-the-nested-triggers-server-configuration-option)

### <a name="sql-server-clr-integration"></a>Integrazione CLR di SQL Server

Il database del sito richiede l'abilitazione di Common Language Runtime (CLR) di SQL Server. Questa opzione viene abilitata automaticamente quando si installa Configuration Manager. Per altre informazioni su CLR, vedere [Introduzione all'integrazione CLR di SQL Server](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/introduction-to-sql-server-clr-integration).  

### <a name="sql-server-service-broker-ssb"></a>SQL Server Service Broker (SSB)

SQL Server Service Broker è necessario sia per la replica tra siti che per un singolo sito primario.

### <a name="trustworthy-setting"></a>Impostazione TRUSTWORTHY

Configuration Manager abilita automaticamente la [proprietà TRUSTWORTHY del database](https://docs.microsoft.com/sql/relational-databases/security/trustworthy-database-property). Questa proprietà è obbligatoria per l'**attivazione di Configuration Manager**.

## <a name="optional-configurations-for-sql-server"></a><a name="bkmk_optional"></a> Configurazioni facoltative per SQL Server

Le configurazioni seguenti sono facoltative per ogni database che usa un'installazione completa di SQL Server.  

### <a name="sql-server-service"></a>Servizio SQL Server

È possibile configurare il servizio SQL Server per l'esecuzione con:  

- Un account *utente di dominio con diritti limitati*:  

  - Questa configurazione è una procedura ottimale e potrebbe essere necessario registrare manualmente il nome dell'entità servizio (SPN) per l'account.  

- L'account **sistema locale** del computer in cui viene eseguito SQL Server:  

  - Usare l'account sistema locale per semplificare il processo di configurazione.  
  - Quando si usa l'account sistema locale, Configuration Manager registra automaticamente il nome SPN per il servizio SQL Server.  
  - L'uso dell'account di sistema locale per il servizio SQL Server non è una procedura consigliata di SQL Server.  

Se il computer che esegue SQL Server non usa il proprio account di sistema locale per eseguire il servizio di SQL Server, configurare il nome dell'entità servizio (SPN) dell'account che esegue il servizio di SQL Server in Active Directory Domain Services. Se viene usato l'account di sistema, il nome dell'entità servizio viene registrato automaticamente.

Per informazioni sui nomi SPN per il database del sito, vedere [Gestire il SPN per il server di database del sito](../../servers/manage/modify-your-infrastructure.md#bkmk_SPN).  

Per informazioni su come modificare l'account usato dal servizio SQL Server, vedere [Gestione configurazione SQL Server - Modificare l'account di avvio del servizio](https://docs.microsoft.com/sql/database-engine/configure-windows/scm-services-change-the-service-startup-account).  

### <a name="sql-server-reporting-services"></a>SQL Server Reporting Services

SQL Server Reporting Services è necessario per l'installazione di un punto di Reporting Services che consente di eseguire report. Configuration Manager supporta per la creazione di report le stesse versioni di SQL Server supportate per il database del sito.

Per altre informazioni, vedere [Prerequisiti per la creazione di report in Configuration Manager](../../servers/manage/prerequisites-for-reporting.md).

> [!IMPORTANT]  
> Dopo aver aggiornato SQL Server da una versione precedente, potrebbe essere visualizzato l'errore seguente: *Report Builder Does Not Exist* (Generatore report non esiste).  
> Per risolvere questo errore è necessario reinstallare il ruolo del sistema del sito del punto di Reporting Services.  

### <a name="data-warehouse-service-point"></a>Punto di servizio del data warehouse

Il data warehouse usa un database separato. È possibile ospitarlo nel server di database del sito o in un'istanza di SQL Server separata. Per altre informazioni, vedere [Punto di servizio del data warehouse per Configuration Manager](../../servers/manage/data-warehouse.md).

### <a name="sql-server-ports"></a>Porte di SQL Server

Per la comunicazione con il motore di database di SQL Server e per la replica tra siti, è possibile usare le configurazioni di porte SQL Server predefinite o specificare porte personalizzate:  

- Le **comunicazioni tra siti** usano SQL Server Service Broker, che per impostazione predefinita usa la porta TCP 4022.  
- Le **comunicazioni all'interno del sito** tra il motore di database SQL Server e i diversi ruoli del sistema del sito di Configuration Manager usano per impostazione predefinita la porta TCP 1433. I ruoli del sistema del sito seguenti comunicano direttamente con il database di SQL Server:  

  - Punto di gestione  
  - Computer del provider SMS  
  - Punto di Reporting Services  
  - Server del sito  

Se un computer che esegue SQL Server ospita un database da più di un sito, ogni database deve usare un'istanza separata di SQL Server e ogni istanza deve essere configurata con un set univoco di porte.  

> [!WARNING]  
> Configuration Manager non supporta porte dinamiche. Poiché per impostazione predefinita le istanze denominate di SQL Server usano le porte dinamiche per le connessioni al motore di database, quando si usa un'istanza denominata è necessario configurare manualmente la porta statica da usare per la comunicazione tra siti.  

Se è disponibile un firewall abilitato nel computer che esegue SQL Server, assicurarsi che sia configurato per consentire le porte usate dalla distribuzione e in tutti i percorsi della rete tra i computer che comunicano con SQL Server.  

Per un esempio di come configurare SQL Server per l'uso di una porta specifica, vedere [Configurare un server per l'attesa su una porta TCP specifica](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port).  

## <a name="upgrade-options-for-sql-server"></a>Opzioni di aggiornamento per SQL Server

Se è necessario aggiornare la versione di SQL Server, usare uno dei metodi seguenti, dal più semplice al più complesso:  

- [Aggiornare SQL Server sul posto](../../servers/manage/upgrade-on-premises-infrastructure.md#to-upgrade-sql-server-on-the-site-database-server) (scelta consigliata)  

- Installare una nuova versione di SQL Server in un nuovo computer e quindi [usare l'opzione di spostamento del database](../../servers/manage/modify-your-infrastructure.md#bkmk_dbconfig) dell'installazione di Configuration Manager in modo che il server del sito punti alla nuova versione di SQL Server  

- Usare le funzionalità di [backup e ripristino](../../servers/manage/backup-and-recovery.md). L'uso delle funzionalità di backup e ripristino per uno scenario di aggiornamento SQL è supportato. È possibile ignorare il requisito di controllo delle versioni SQL quando si rivedono le [Considerazioni prima del recupero di un sito](../../servers/manage/recover-sites.md#considerations-before-recovering-a-site).
