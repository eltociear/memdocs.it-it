---
title: replica di database
titleSuffix: Configuration Manager
description: Informazioni su come la replica di database di Configuration Manager usa SQL Server per trasferire i dati nella gerarchia.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8b495b02-c966-4eb3-92b9-52ebbf5c38ae
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d1a2c8baa349e6499aa483f947d94f7459357be4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703599"
---
# <a name="database-replication"></a>replica di database

*Si applica a: Configuration Manager (Current Branch)*

La replica di database di Configuration Manager usa SQL Server per trasferire i dati. Usa questo metodo per unire le modifiche nel database del sito con le informazioni del database in altri siti della gerarchia.

Considerare i punti seguenti sulla replica di database:

- Tutti i siti condividono le stesse informazioni.  

- Quando si installa un sito in una gerarchia, Configuration Manager definisce automaticamente la replica di database tra il nuovo sito e il sito padre.  

- Al termine dell'installazione del sito, la replica di database viene avviata automaticamente.  

Quando si aggiunge un nuovo sito a una gerarchia, Configuration Manager crea un database generico nel nuovo sito. Il sito padre crea uno snapshot dei dati rilevanti nel database, quindi trasferisce lo snapshot nel nuovo sito usando la [replica basata su file](file-based-replication.md). Il nuovo sito usa poi un programma per la copia bulk di SQL Server (BCP) per caricare le informazioni nella copia locale del database di Configuration Manager. Dopo il caricamento dello snapshot, ogni sito esegue la replica di database con l'altro sito.  

Per replicare i dati tra siti, Configuration Manager usa il proprio servizio di replica database. Il servizio di replica di database usa il rilevamento modifiche di SQL Server per monitorare le modifiche al database del sito locale. Quindi replica le modifiche agli altri siti usando SQL Server Service Broker (SSB). Per impostazione predefinita, questo processo usa la porta TCP 4022.  


## <a name="replication-groups"></a>Gruppi di replica

Configuration Manager riunisce i dati replicati con replica di database in gruppi di replica diversi. Ogni gruppo di replica dispone di una pianificazione di replica fissa separata. Il sito usa questa pianificazione per determinare la frequenza con cui replica le modifiche agli altri siti.  

Ad esempio una modifica alla configurazione dell'amministrazione basata su ruoli viene rapidamente replicata ad altri siti. Questo comportamento assicura che l'altro sito possa applicare rapidamente queste modifiche. Una modifica della configurazione con priorità più bassa, ad esempio una richiesta di installazione di un nuovo sito secondario, viene invece replicata con minore urgenza. La richiesta di un nuovo sito può infatti impiegare alcuni minuti prima che raggiunga il sito primario di destinazione.  


## <a name="settings"></a>Impostazioni

Per la replica di database, è possibile modificare le impostazioni seguenti:  

- **Collegamenti di replica di database**: Consentono di controllare quando la rete viene attraversata da traffico specifico.  

- **Viste distribuite**: Quando un sito di amministrazione centrale (CAS, Central Administration Site) richiede dati del sito selezionati, può accedere ai dati stessi direttamente dal database in un sito primario figlio.  

- **Pianificazioni**: Consentono di specificare quando viene usato un collegamento di replica e quando vengono replicati diversi tipi di dati del sito.  

- **Riepilogo**: Consente di modificare le impostazioni per il riepilogo di dati sul traffico di rete che attraversa i collegamenti di replica. Per impostazione predefinita, il riepilogo avviene ogni 15 minuti. Viene usato nei report per la replica del database.  

- **Soglie di replica del database**: Consentono di definire quando il sito segnala i collegamenti come danneggiati o non riusciti. È anche possibile configurare quando Configuration Manager genera avvisi sui collegamenti di replica con stato danneggiato o non riuscito.  


## <a name="types-of-data"></a>Tipi di dati

Configuration Manager classifica i dati che replica come *dati globali* o come *dati del sito*. Quando si verifica la replica di database, il sito trasferisce le modifiche ai dati globali e ai dati del sito attraverso il collegamento di replica di database. I dati globali vengono replicati a un sito padre o a un sito figlio. I dati del sito vengono replicati solo a un sito padre. Esiste un terzo tipo di dati, i *dati locali*, che non viene replicato ad altri siti. I dati locali sono informazioni non richieste da altri siti.  

### <a name="global-data"></a>Dati globali

I dati globali sono oggetti creati dall'amministratore e replicati in tutti i siti in tutta la gerarchia. I siti secondari ricevono solo un subset di dati globali, come dati proxy globali. I dati globali vengono creati nel sito CAS e nei siti primari. Includono i dati seguenti:

- Distribuzioni software
- Aggiornamenti software
- Definizioni di raccolta
- Ambiti di protezione dell'amministrazione basata su ruoli

### <a name="site-data"></a>Dati del sito

I dati del sito sono informazioni operative create dai siti primari di Configuration Manager e dai rispettivi client assegnati. I dati del sito vengono replicati nel sito di amministrazione centrale, ma non in altri siti primari. I dati del sito possono essere visualizzati solo nel sito di amministrazione centrale e nel sito primario da cui hanno origine. È possibile modificare i dati del sito solo nel sito primario in cui sono stati creati. Includono i dati seguenti:

- Inventario hardware
- Messaggi di stato
- Avvisi
- Risultati di raccolte basate su query

Tutti i dati del sito vengono replicati nel sito di amministrazione centrale. Il sito CAS esegue l'amministrazione e la creazione di report per l'intera gerarchia.  


## <a name="database-replication-links"></a><a name="bkmk_Dblinks"></a> Collegamenti di replica di database

Quando si installa un nuovo sito in una gerarchia, Configuration Manager crea automaticamente un collegamento di replica di database tra il sito padre e il nuovo sito. Crea un unico collegamento per collegare i due siti.  

Per controllare il trasferimento dei dati nel collegamento della replica, modificare le impostazioni di ogni collegamento. Ogni collegamento di replica supporta configurazioni separate. Ogni collegamento della replica di database include i controlli seguenti:  

- Arresto della replica di dati del sito selezionati da un sito primario al sito CAS. Questa azione fa in modo che il sito CAS acceda a questi dati direttamente dal database del sito primario.  

- Pianificazione dei dati del sito selezionati per il trasferimento da un sito primario figlio al sito CAS.

- Definizione delle impostazioni che determinano quando un collegamento di replica di database è danneggiato o non è riuscito.

- La possibilità di specificare in quali casi generare avvisi per un collegamento di replica non riuscito.

- Specificare la frequenza con cui Configuration Manager riepiloga i dati sul traffico di replica che usa il collegamento di replica. Usa questi dati nei report.

Per configurare un collegamento di replica di database, nella console di Configuration Manager passare all'area di lavoro **Monitoraggio**. Selezionare il nodo **Replica di database** e modificare le proprietà del collegamento. Questo nodo è presente anche nell'area di lavoro **Amministrazione**, sotto il nodo **Configurazione della gerarchia**. Modificare un collegamento di replica dal relativo sito padre o sito figlio.  

> [!TIP]  
> È possibile modificare i collegamenti di replica di database dal nodo **Replica di database** in qualsiasi area di lavoro. Tuttavia quando si usa il nodo **Replica di database** nell'area di lavoro **Monitoraggio**, è anche possibile visualizzare lo stato della replica di database. Il nodo consente anche di accedere allo strumento [Replication Link Analyzer](../../servers/manage/monitor-replication.md#BKMK_RLA). Usare questo strumento per analizzare i problemi relativi alla replica di database.  

Per altre informazioni su come configurare i collegamenti di replica, vedere [Controlli di replica di database del sito](#BKMK_DBRepControls). Per altre informazioni sul monitoraggio della replica, vedere [Monitorare la replica del database](../../servers/manage/monitor-replication.md).  


## <a name="distributed-views"></a><a name="bkmk_distviews"></a> Viste distribuite  

Tramite le viste distribuite, quando si esegue una richiesta di dati del sito selezionati al sito CAS si accede direttamente al database nel sito primario figlio. Questo accesso diretto elimina la necessità di replicare i dati dal sito primario al sito CAS. Poiché ogni collegamento di replica è indipendente dagli altri, è possibile usare le viste distribuite nei collegamenti di replica selezionati. Non è possibile usare viste distribuite tra un sito primario e un sito secondario.  

Le viste distribuite offrono i seguenti vantaggi:  

- Ridurre il carico CPU per l'elaborazione le modifiche del database nel sito di amministrazione centrale (CAS) e nei siti primari

- Ridurre la quantità di dati trasferiti attraverso la rete al sito CAS

- Migliorare le prestazioni dell'istanza di SQL Server che ospita il database CAS

- Ridurre lo spazio su disco usato dal database CAS

È consigliabile usare le viste distribuite quando un sito primario si trova vicino al sito CAS sulla rete e i due siti sono sempre attivi e sempre connessi. Le viste distribuite sostituiscono la replica dei dati selezionati tra i siti con connessioni dirette tra i server SQL in ogni sito. Il CAS esegue una connessione diretta ogni volta che vengono richiesti questi dati.

Il sito richiede i dati della vista distribuiti negli scenari di esempio seguenti:

- Quando si eseguono report o query
- Quando si visualizzano informazioni in Esplora inventario risorse
- Valutazione della raccolta per le raccolte che includono regole basate sui dati del sito

Per impostazione predefinita, le viste distribuite sono disabilitate per ogni collegamento di replica. Quando si attivano le viste distribuite si selezionano i dati del sito che non verranno replicati nel CAS su tale collegamento. Il sito CAS accede a questi dati direttamente dal database del sito primario figlio che condivide il collegamento. È possibile configurare i seguenti tipi di dati del sito per le viste distribuite:  

- **Dati di inventario hardware** dei client
- **Dati di controllo e inventario software** dei client
- **Messaggi di stato** dei client, del sito primario e di tutti i siti secondari

Quando si visualizzano i dati nella console di Configuration Manager o nei report, le viste distribuite non sono visibili a livello operativo. Quando si richiedono dati abilitati per le viste distribuite, il server di database del sito CAS accede direttamente al database del sito primario figlio per recuperare le informazioni.

Ad esempio, si usa una console di Configuration Manager connessa al sito CAS. Si richiedono informazioni sull'inventario hardware a due siti primari: ABC e XYZ. L'inventario hardware è stato abilitato solo per le viste distribuite nel sito ABC. Il sito CAS recupera le informazioni sull'inventario per i client XYZ dal proprio database. Il sito CAS recupera le informazioni sull'inventario per i client ABC direttamente dal database nel sito ABC. Queste informazioni vengono visualizzate nella console di Configuration Manager o in un report senza identificazione dell'origine.  

Se il tipo di dati di un collegamento di replica è abilitato per le viste distribuite, il sito primario figlio non replica tali dati al sito CAS. Quando si disattivano le viste distribuite per un tipo di dati, il sito primario figlio riprende la normale replica dei dati al sito CAS. Prima che questi dati diventino disponibili nel sito CAS, i gruppi di replica per questi dati devono essere reinizializzati tra il sito primario e il sito CAS. Dopo aver disinstallato un sito primario abilitato per le viste distribuite, il sito di amministrazione centrale deve completare la reinizializzazione dei suoi dati perché i dati che erano abilitati alle viste distribuite siano accessibili al suo interno.  

> [!IMPORTANT]  
> Quando si usano le viste distribuite in un qualsiasi collegamento di replica nella gerarchia del sito, disabilitare le viste distribuite per tutti i collegamenti di replica prima di disinstallare un sito primario. Per altre informazioni, vedere [Disinstallare un sito primario che usa viste distribuite](../../servers/deploy/install/uninstall-sites-and-hierarchies.md#bkmk_distviews).  

### <a name="prerequisites-and-limitations-for-distributed-views"></a>Prerequisiti e limitazioni per le viste distribuite  

- Usare le viste distribuite solo nei collegamenti di replica tra il sito CAS e un sito primario.

- Il sito CAS deve usare l'edizione Enterprise di SQL Server. Il sito primario non presenta questo requisito.

- Il sito CAS può avere una sola istanza del provider SMS. Installare tale istanza nel server di database del sito. Questa configurazione supporta l'autenticazione Kerberos. Il server SQL nel sito CAS richiede che Kerberos acceda al server SQL nel sito primario figlio. Non esistono limitazioni nel provider SMS nel sito primario figlio.

- È possibile installare un solo punto di Reporting Services nel sito CAS. Installare SQL Server Reporting Services nel server di database del sito. Questa configurazione supporta l'autenticazione Kerberos. Il server SQL nel sito CAS richiede che Kerberos acceda al server SQL nel sito primario figlio.

- Non è possibile ospitare il database del sito in un [cluster di SQL Server](../../servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md).

- Nella versione 1902 e versioni precedenti non è possibile ospitare il database del sito in un [gruppo di disponibilità SQL Server Always On](../../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md). Per supportare questa configurazione, eseguire l'aggiornamento alla versione 1906 o a versioni successive.<!-- SCCMDocs-pr#3792 -->

- L'account computer del server di database CAS richiede autorizzazioni di **lettura** per il database del sito primario.

> [!IMPORTANT]  
> Le viste distribuite e le [pianificazioni](#BKMK_schedules) del momento in cui poter replicare i dati sono configurazioni per un collegamento di replica del database che si escludono a vicenda.  


## <a name="schedule-transfers-of-site-data"></a><a name="BKMK_schedules"></a> Pianificare i trasferimenti dei dati del sito

Per facilitare il controllo della larghezza di banda di rete usata per replicare i dati del sito da un sito primario figlio al sito CAS corrispondente, pianificare quando viene usato un collegamento di replica, quindi specificare quando vengono replicati i diversi tipi di dati del sito. È possibile controllare quando il sito primario replica i messaggi di stato, l'inventario e i dati di controllo. I collegamenti di replica del database dei siti secondari non supportano le pianificazioni per i dati del sito. Non è possibile pianificare il trasferimento di dati globali.  

Quando si configura una pianificazione del collegamento di replica del database, è possibile limitare il trasferimento dei dati del sito selezionati dal sito primario al sito CAS. È anche possibile configurare orari diversi per replicare tipi diversi di dati del sito.  

> [!IMPORTANT]  
> Le [viste distribuite](#bkmk_distviews) e le pianificazioni per quando possono essere replicati i dati sono configurazioni che si escludono a vicenda per un collegamento di replica del database.  


## <a name="summarization-of-traffic"></a><a name="BKMK_SummarizeDBReplication"></a> Esecuzione del riepilogo del traffico  

Ogni sito riepiloga periodicamente i dati sul traffico di rete che attraversa i collegamenti di replica di database del sito. Il sito usa i dati riepilogati nei report per la replica di database. Entrambi i siti su un collegamento di replica riepilogano il traffico di rete che attraversa il collegamento di replica. Il server di database del sito riepiloga i dati. Dopo il riepilogo dei dati, queste informazioni vengono replicate in altri siti come dati globali.  

Per impostazione predefinita, il riepilogo avviene ogni 15 minuti. Per modificare la frequenza di riepilogo per il traffico di rete, modificare il valore in **Intervallo riepilogo** nelle proprietà del collegamento di replica del database. La frequenza di riepilogo riguarda le informazioni visualizzate nei report sulla replica di database. È possibile scegliere un intervallo compreso tra 5 e 60 minuti. Quando si aumenta la frequenza di riepilogo, è possibile aumentare il carico di elaborazione su SQL Server in ogni sito sul collegamento di replica.  

## <a name="database-replication-thresholds"></a><a name="BKMK_DBRepThresholds"></a> Soglie di replica del database

Le soglie di replica del database definiscono quando Configuration Manager restituisce uno stato di un collegamento di replica del database ridotto o non riuscito. Per impostazione predefinita, un collegamento assume lo stato *ridotto* quando un gruppo di replica non completa la replica dopo 12 tentativi consecutivi. Il collegamento assume lo stato *non riuscito* quando un gruppo di replica non esegue la replica dopo 24 tentativi consecutivi.  

È possibile specificare valori personalizzati per lo stato ridotto o non riuscito. Se si modificano questi valori, è possibile monitorare con maggior precisione l'integrità della replica di database tra i collegamenti.  

Uno o più gruppi di replica possono non riuscire a eseguire la replica, mentre altri gruppi di replica continuano a replicare correttamente. Pianificare la verifica dello stato della replica di un collegamento quando questo segnala per la prima volta uno stato ridotto.

Provare a modificare i valori dei tentativi per lo stato ridotto o non riuscito del collegamento nelle situazioni seguenti:

- Si verificano ritardi ricorrenti per specifici gruppi di replica e il ritardo non è un problema

- Il collegamento di rete tra siti ha una larghezza di banda disponibile bassa

Aumentando il numero di tentativi prima che il sito imposti il collegamento su ridotto o non riuscito, è possibile eliminare gli avvisi non necessari per problemi noti. Questa azione consente di tenere traccia più accuratamente dello stato del collegamento.  

Per conoscere la frequenza con cui viene eseguita la replica di tale gruppo, è necessario considerare anche l'intervallo di sincronizzazione della replica per ogni gruppo di replica. Per visualizzare l'**intervallo di sincronizzazione** per i gruppi di replica, passare all'area di lavoro **Monitoraggio** nella console di Configuration Manager. Nel nodo **Replica di database** selezionare la scheda **Dettaglio di replica** di un collegamento di replica.  

Per altre informazioni sul monitoraggio della replica di database, inclusa la visualizzazione dello stato della replica, vedere [Monitorare la replica di database](../../servers/manage/monitor-replication.md).  


## <a name="site-database-replication-controls"></a><a name="BKMK_DBRepControls"></a> Controlli di replica di database del sito  

Per controllare la larghezza di banda di rete usata per la replica di database, modificare le impostazioni per ogni database del sito. Le impostazioni si applicano solo al database del sito in cui vengono configurate. Il sito usa sempre queste impostazioni per replicare i dati a un altro sito tramite replica di database.  

È possibile modificare i controlli di replica seguenti per ogni database del sito:  

- Porta SSB  

- Tempo di attesa prima che venga reinizializzata la copia del database del sito a seguito di tentativi di replica non riusciti  

- Comprimere i dati replicati da un sito. Un sito comprime i dati solo per il trasferimento tra siti e non per l'archiviazione nel database del sito su ogni sito.  

Per modificare le impostazioni dei controlli di replica per un database del sito, modificare le proprietà del database del sito nella console di Configuration Manager dal nodo **Replica di database**. È possibile visualizzare questo nodo sotto il nodo **Configurazione della gerarchia** nell'area di lavoro **Amministrazione** e anche in **Area di lavoro di monitoraggio**. Per modificare le proprietà del database del sito, selezionare il collegamento di replica tra i siti e aprire **Proprietà database principale** oppure **Proprietà database secondario**.  

> [!TIP]  
> È possibile configurare i controlli di replica del database dal nodo **Replica di database** in qualsiasi area di lavoro. Tuttavia, quando si usa il nodo **Replica di database** nell'area di lavoro **Monitoraggio**, è possibile anche visualizzare lo stato della replica del database per un collegamento di replica e accedere allo strumento Replication Link Analyzer che consente all'utente di esaminare eventuali problemi di replica.  


## <a name="see-also"></a>Vedere anche

[Monitorare la replica](../../servers/manage/monitor-replication.md)

[Risolvere i problemi di replica SQL](../../servers/manage/replication/overview.md)
