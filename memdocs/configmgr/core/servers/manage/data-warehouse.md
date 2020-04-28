---
title: Data warehouse
titleSuffix: Configuration Manager
description: Punto di servizio e database del data warehouse per Configuration Manager
ms.date: 05/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: aaf43e69-68b4-469a-ad58-9b66deb29057
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: abe6b05d24955959e1d08defc2c5054c4499d756
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075592"
---
#  <a name="the-data-warehouse-service-point-for-configuration-manager"></a>Punto di servizio del data warehouse per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

<!--1277922-->
Usare il punto di servizio del data warehouse per archiviare e creare report di dati cronologici a lungo termine per la distribuzione di Configuration Manager.

> [!Note]  
> Nella versione 1910 Configuration Manager abilita questa funzionalità per impostazione predefinita. Nella versione 1906 o nelle versioni precedenti Configuration Manager non abilita questa funzionalità facoltativa per impostazione predefinita. Pertanto sarà necessario abilitarla prima di poterla usare. Per altre informazioni, vedere [Enable optional features from updates](install-in-console-updates.md#bkmk_options) (Abilitare le funzioni facoltative dagli aggiornamenti).<!--505213-->  


Il data warehouse supporta fino a 2 TB di dati, con timestamp per il rilevamento delle modifiche. Il data warehouse archivia i dati sincronizzando i dati automaticamente dal database del sito di Configuration Manager al database del data warehouse. Queste informazioni diventano quindi accessibili dal punto di Reporting Services. I dati sincronizzati nel database del data warehouse vengono mantenuti per tre anni. Periodicamente, un'attività predefinita rimuove i dati che hanno superato i tre anni.

Tra i dati sincronizzati sono inclusi i dati seguenti dai gruppi di dati globali e del sito:
- Integrità dell'infrastruttura
- Sicurezza
- Conformità
- Malware   
- Distribuzioni software
- Dettagli relativi all'inventario. La cronologia dell'inventario, tuttavia, non è sincronizzata.

Quando viene installato, il ruolo del sistema del sito installa e configura il database del data warehouse. Vengono inoltre installati alcuni report che semplificano le attività di ricerca dei dati e di creazione dei report.

A partire dalla versione 1810, è possibile sincronizzare un maggior numero di tabelle dal database del sito al data warehouse. Questa modifica consente di creare più report in base ai requisiti aziendali.<!--1358870--> 



## <a name="prerequisites"></a>Prerequisiti

- Il ruolo del sistema del sito del data warehouse è supportato solo dal sito di livello superiore della gerarchia, ad esempio un sito di amministrazione centrale o un sito primario autonomo.  

- Il computer in cui si installa il ruolo del sistema del sito richiede .NET Framework 4.5.2 o versioni successive.  

- Concedere ad **Account punto di Reporting Services** l'autorizzazione **db_datareader** per il database del data warehouse.  

- Per sincronizzare i dati con il database del data warehouse, Configuration Manager usa l'account del computer del ruolo del sistema del sito. L'account richiede le autorizzazioni seguenti:  

    - **Amministratore** nel computer che ospita il database del data warehouse.  

    - Autorizzazione **DB_Creator** nel database del data warehouse.  

    - **DB_owner** o **DB_reader** con autorizzazioni di **esecuzione** nel database del sito di primo livello.  

- Il database del data warehouse richiede l'uso di SQL Server 2012 o versione successiva, edizione Standard, Enterprise o Datacenter. La versione di SQL Server per il data warehouse non deve necessariamente essere la stessa del server di database del sito.<!--SCCMDocs issue 662-->  

- Il database warehouse supporta le configurazioni di SQL Server seguenti:  

    - Un'istanza predefinita o denominata  

    - Gruppo di disponibilità Always On di SQL Server  

    - Cluster di failover di SQL Server  

- Se si usano [viste distribuite](../../plan-design/hierarchy/database-replication.md#bkmk_distviews), il punto di servizio del data warehouse deve essere installato nello stesso server che ospita il database del sito di amministrazione centrale.  

Per altre informazioni sulle licenze di SQL Server, vedere [Domande frequenti su prodotto e licenze](../../understand/product-and-licensing-faq.md). <!-- sms500967 -->

Le dimensioni del database del data warehouse devono essere le stesse del database del sito. Sebbene il data warehouse abbia all'inizio dimensioni minori, le dimensioni aumenteranno nel corso del tempo. <!--SCCMDocs issue 756-->



## <a name="install"></a>Installazione

Ogni gerarchia supporta un'unica istanza di questo ruolo, in qualsiasi sistema del sito di livello superiore. L'istanza di SQL Server che ospita il database del data warehouse può essere locale nel ruolo del sistema del sito o remota. Il data warehouse funziona con il punto di Reporting Services installato nello stesso sito. Non è necessario installare i due ruoli del sistema del sito nello stesso server.   

Per installare il ruolo, usare l'**Aggiunta guidata ruoli del sistema del sito** o la **Creazione guidata server del sistema sito**. Per altre informazioni, vedere [Installare i ruoli del sistema del sito](../deploy/configure/install-site-system-roles.md). Nella pagina **Selezione ruolo del sistema** della procedura guidata selezionare il ruolo**Punto di servizio del data warehouse**. 

Quando si installa il ruolo, Configuration Manager crea il database del data warehouse nell'istanza di SQL Server specificata dall'utente. Se si specifica il nome di un database esistente, Configuration Manager non crea un nuovo database. Usa invece quello specificato. Questo processo è analogo allo [spostamento del database del data warehouse in un nuovo server SQL Server](#move-the-database).


### <a name="configure-properties"></a>Configurare le proprietà

#### <a name="general-page"></a>Pagina generale

- **Nome di dominio completo di SQL**: specificare il nome di dominio completo (FQDN, Full Qualified Domain Name) del server che ospita il database del punto di servizio del data warehouse.  

- **Nome istanza di SQL Server, se applicabile**: se non si usa un'istanza predefinita di SQL Server, specificare l'istanza denominata.  

- **Nome database**: Specificare il nome del database del data warehouse. Configuration Manager crea il database del data warehouse con questo nome. Se si specifica un nome di database già esistente nell'istanza di SQL Server, Configuration Manager usa il database corrispondente.  

- **Porta di SQL Server usata per la connessione**: specificare il numero di porta TCP/IP usata dall'istanza di SQL Server che ospita il database del data warehouse. Il servizio di sincronizzazione del data warehouse usa questa porta per la connessione al database del data warehouse. Per impostazione predefinita, viene usata la porta di SQL Server **1433** per la comunicazione.  

- **Account del punto di servizio del data warehouse**: a partire dalla versione 1802, impostare il **nome utente** usato da SQL Server Reporting Services per la connessione al database del data warehouse.  


#### <a name="synchronization-schedule-page"></a>Pagina Pianificazione della sincronizzazione
*Si applica alla versione 1806 e precedenti*

- **Ora di inizio**: Specificare l'ora in cui si vuole avviare la sincronizzazione del data warehouse.  

- **Criterio ricorrenza**

    - **Ogni giorno**: specificare che la sincronizzazione viene eseguita ogni giorno.  

    - **Ogni settimana**: specificare un solo giorno alla settimana e la ricorrenza settimanale per la sincronizzazione.


#### <a name="synchronization-settings-page"></a>Pagina Impostazioni di sincronizzazione
*Si applica alla versione 1810 e successive*

- **Impostazione personalizzata della sincronizzazione dei dati**: scegliere l'opzione **Selezionare le tabelle**. Nella finestra Tabelle di database selezionare i nomi delle tabelle da sincronizzare con il database del data warehouse. Usare il filtro per eseguire la ricerca in base al nome o selezionare l'elenco a discesa per scegliere gruppi specifici. Al termine, selezionare **OK** per salvare.  

    > [!Note]  
    > Non è possibile rimuovere le tabelle che il ruolo seleziona per impostazione predefinita.  

- **Ora di inizio**: Specificare l'ora in cui si vuole avviare la sincronizzazione del data warehouse.  

- **Criterio ricorrenza**

    - **Ogni giorno**: specificare che la sincronizzazione viene eseguita ogni giorno.  

    - **Ogni settimana**: specificare un solo giorno alla settimana e la ricorrenza settimanale per la sincronizzazione.



## <a name="reporting"></a>Reporting

Dopo aver installato un punto di servizio del data warehouse, diversi report diventano disponibili nel punto di Reporting Services per il sito. Se si installa il punto di servizio del data warehouse prima di installare un punto di Reporting Services, i report vengono aggiunti automaticamente quando in seguito si installa il punto di Reporting Services.

> [!WARNING]  
> A partire dalla versione 1802, il punto del data warehouse supporta credenziali alternative.<!--507334--> Se è stato eseguito l'aggiornamento da una versione precedente di Configuration Manager, è necessario specificare le credenziali usate da SQL Server Reporting Services per connettersi al database del data warehouse. I report del data warehouse non vengono aperti fino a quando non vengono aggiunte le credenziali. 
> 
> Per specificare un account, impostare il **Nome utente** per l'account del punto di servizio del data warehouse nelle proprietà del ruolo. Per altre informazioni, vedere [Configurare le proprietà](#configure-properties). 

Il ruolo del sistema del sito del data warehouse include i report seguenti nella categoria **Data warehouse**:  

- **Application Deployment - Historical** (Distribuzione applicazioni - Cronologia): Visualizza i dettagli per la distribuzione di applicazioni per un'applicazione e un computer specifici.  

- **Conformità di Endpoint Protection e degli aggiornamenti software - cronologia**: Visualizza i computer in cui mancano aggiornamenti software.  

- **General Hardware Inventory - Historical** (Inventario generale hardware - Cronologia): Visualizza tutto l'inventario dell'hardware per un computer specifico.  

- **General Software Inventory - Historical** (Inventario generale software - Cronologia): Visualizza tutto l'inventario del software per un computer specifico.  

- **Infrastructure Health Overview - Historical** (Panoramica integrità infrastruttura - Cronologia): Visualizza una panoramica dell'integrità dell'infrastruttura di Configuration Manager.  

- **List of Malware Detected - Historical** (Elenco di malware rilevato - Cronologia): Visualizza il malware che è stato rilevato nell'organizzazione.  

- **Software Distribution Summary - Historical** (Riepilogo distribuzione software - Cronologia): Riepilogo della distribuzione del software per un annuncio e un computer specifici.  



## <a name="site-expansion"></a>Espansione del sito

Prima di installare un sito di amministrazione centrale per espandere un sito primario autonomo esistente, disinstallare il ruolo del punto di servizio del data warehouse. Dopo aver installato il sito di amministrazione centrale, è possibile installare il ruolo del sistema del sito nel sito di amministrazione centrale.  

A differenza di uno spostamento del database del data warehouse, questa modifica comporta la perdita dei dati cronologici sincronizzati in precedenza nel sito primario. Le operazioni di backup del database dal sito primario e di ripristino nel sito di amministrazione centrale non sono supportate.



## <a name="move-the-database"></a>Spostare il database

Per spostare il database del data warehouse in un nuovo SQL Server, procedere come segue:  

1. Usare SQL Server Management Studio per eseguire il backup del database del data warehouse. Ripristinare quindi il database in SQL Server nel nuovo computer che ospita il data warehouse.  

    > [!NOTE]  
    > Dopo aver ripristinato il database nel nuovo server, assicurarsi che le autorizzazioni di accesso al database per il nuovo database del data warehouse siano le stesse del data warehouse originale.  

2. Usare la console di Configuration Manager per rimuovere il ruolo del punto di servizio del data warehouse dal server corrente.  

3. Reinstallare il punto di servizio del data warehouse. Specificare il nome della nuova istanza di SQL Server e dell'istanza che ospita il database del data warehouse ripristinato.  

4. Dopo l'installazione del ruolo del sistema del sito, lo spostamento è completato.  



## <a name="troubleshooting"></a>Risoluzione dei problemi 

### <a name="log-files"></a>File di registro 

Usare i log seguenti per analizzare i problemi dell'installazione del punto di servizio del data warehouse o della sincronizzazione dei dati:

- **DWSSMSI.log** e **DWSSSetup.log**: questi log consentono di analizzare gli errori che si verificano durante l'installazione del punto di servizio del data warehouse.  

- **Microsoft.ConfigMgrDataWarehouse.log**: questo log consente di analizzare la sincronizzazione dei dati tra il database del sito e il database del data warehouse.  


### <a name="set-up-failure"></a>Errore di installazione 

Quando il ruolo del punto di servizio del data warehouse è il primo ruolo installato in un server remoto, l'installazione non viene eseguita per il data warehouse.  

#### <a name="workaround"></a>Soluzione alternativa 
Verificare che il computer in cui si installa il punto di servizio del data warehouse ospiti già almeno un altro ruolo.  


### <a name="synchronization-failed-to-populate-schema-objects"></a>La sincronizzazione non ha popolato gli oggetti dello schema 

La sincronizzazione non viene eseguita e viene visualizzato il messaggio seguente in **Microsoft.ConfigMgrDataWarehouse.log**: `failed to populate schema objects`

#### <a name="workaround"></a>Soluzione alternativa 
Verificare che l'account del computer del ruolo del sistema del sito sia **db_owner** nel database del data warehouse.


### <a name="reports-fail-to-open"></a>Non è possibile aprire i report

Non è possibile aprire i report del data warehouse quando il database del data warehouse e il punto di Reporting Services si trovano in sistemi del sito diversi.  

#### <a name="workaround"></a>Soluzione alternativa
Concedere ad **Account punto di Reporting Services** l'autorizzazione **db_datareader** per il database del data warehouse.


### <a name="error-opening-reports"></a>Errore durante l'apertura dei report

Quando si apre un report del data warehouse, viene restituito l'errore seguente:

``` Output
An error has occurred during report processing. (rsProcessingAborted)
Cannot create a connection to data source 'AutoGen__39B693BB_524B_47DF_9FDB_9000C3118E82_'. (rsErrorOpeningConnection)
A connection was successfully established with the server, but then an error occurred during the pre-login handshake. (provider: SSL Provider, error: 0 - The certificate chain was issued by an authority that is not trusted.)
```

#### <a name="workaround"></a>Soluzione alternativa 
Per configurare i certificati eseguire questa procedura:

1. Nel computer che ospita il database del data warehouse:  

    1. Aprire IIS, selezionare **Certificati del server** e quindi fare clic con il pulsante destro del mouse su **Crea certificato autofirmato**. Quindi specificare il "nome descrittivo" del certificato come **Certificato di identificazione SQL Server del data warehouse**. Selezionare l'archivio certificati come **Personale**.  

    2. Aprire **Gestione configurazione SQL Server**. In **Configurazione di rete SQL Server** fare clic con il pulsante destro del mouse per selezionare **Proprietà** in **Protocolli per MSSQLSERVER**. Passare alla scheda **Certificato**, selezionare **Certificato di identificazione SQL Server del data warehouse** come certificato e salvare le modifiche.  

    3. In **Gestione configurazione SQL Server**, in **Servizi di SQL Server** riavviare il **servizio SQL Server**. Se nel server che ospita il database del data warehouse è installato anche SQL Reporting Services, riavviare anche i servizi **Reporting Services**.  

    4. Aprire Microsoft Management Console (MMC) e aggiungere lo snap-in **Certificati**. Selezionare l'**Account del computer** del computer locale. Espandere la cartella **Personale** e selezionare **Certificati**. Esportare il **Certificato di identificazione SQL Server del data warehouse** come file **Binario codificato DER x.509 (.CER)** .  

2. Nel computer che ospita SQL Server Reporting Services aprire MMC e aggiungere lo snap-in **Certificati**. Selezionare **Account del computer**. Nella cartella **Autorità di certificazione principale attendibili** importare **Certificato di identificazione SQL Server del data warehouse**.  



## <a name="data-flow"></a>Flusso di dati   

![Diagramma che illustra il flusso di dati logico tra i componenti del sito per il data warehouse](./media/datawarehouse.png)

#### <a name="data-storage-and-synchronization"></a>Sincronizzazione e archiviazione dei dati

| Passaggio   | Dettagli  |
|--------|----------|  
| **1**  | Il server del sito trasferisce e archivia i dati nel database del sito. |  
| **2**  | In base alla pianificazione e alla configurazione, il punto di servizio del data warehouse recupera dati dal database del sito. |  
| **3**  | Il punto di servizio del data warehouse trasferisce e archivia una copia dei dati sincronizzati nel database del data warehouse. |  


#### <a name="reporting"></a>Reporting

| Passaggio   | Dettagli  |
|--------|----------|  
| **A**  | Un utente richiede i dati usando i report predefiniti. Questa richiesta viene passata al punto di Reporting Services tramite SQL Server Reporting Services. |  
| **B**  | La maggior parte dei report sono usati per informazioni correnti e queste richieste vengono eseguite tramite il database del sito. |  
| **C**  | Se un report richiede dati cronologici tramite un report con *Categoria* corrispondente a **Data warehouse**, la richiesta viene eseguita tramite il database del data warehouse. |  
