---
title: Monitorare la replica di database
titleSuffix: Configuration Manager
description: Informazioni su come monitorare la replica di SQL Server nella gerarchia di Configuration Manager.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 69550b35-bcdb-4b47-bbec-b3c8bc92bb7b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4a9ae791582911f91e5f76b841248ad5085d8170
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83879826"
---
# <a name="monitor-database-replication"></a>Monitorare la replica di database

*Si applica a: Configuration Manager (Current Branch)*

Monitorare i dettagli della replica di database con il nodo **Replica di database** nell'area di lavoro **Monitoraggio** della console di Configuration Manager. È possibile monitorare lo stato dei collegamenti di replica tra siti. Vengono anche visualizzate l'inizializzazione e la replica dei gruppi di replica per il sito a cui ci si connette.  

> [!TIP]  
> Nonostante un nodo **Replica di database** venga visualizzato anche sotto il nodo **Configurazione della gerarchia** nell'area di lavoro **Amministrazione**, da quella posizione non è possibile visualizzare lo stato di replica per i collegamenti di replica di database.  

## <a name="replication-link-status"></a><a name="BKMK_MonitorReplicationLinks"></a> Stato del collegamento di replica  

La replica di database tra siti implica la replica di diversi set di informazioni, denominati *gruppi di replica*. Ogni gruppo di replica invia e riceve dati con priorità diverse. Per impostazione predefinita, non è possibile modificare i dati contenuti in un gruppo di replica e la frequenza di replica.  

Quando un collegamento di replica è attivo e lo stato non è non riuscito o ridotto, tutti i gruppi vengono replicati rapidamente. Se uno o più gruppi non riescono a completare la replica nel periodo di tempo previsto, il collegamento viene visualizzato come *ridotto*. I collegamenti ridotti possono comunque funzionare, ma è consigliabile monitorarli per verificare che ritornino allo stato attivo. Esaminarli per assicurarsi che non si verifichino ulteriori errori di riduzione delle prestazioni o di replica.  

Per ogni collegamento di replica, specificare per quante volte un gruppo può essere replicato in modo non corretto. Dopo questo numero di tentativi, il sito imposta lo stato del collegamento su ridotto o non riuscito. Anche se un solo gruppo non viene replicato correttamente, il sito imposta lo stato del collegamento su ridotto o non riuscito. Questo stato viene impostato perché quell'unico gruppo di replica non riesce a completare la replica nel numero specificato di tentativi. Per altre informazioni, vedere [Soglie di replica di database](../../plan-design/hierarchy/database-replication.md#BKMK_DBRepThresholds).  

Usare le informazioni seguenti per conoscere lo stato dei collegamenti di replica che potrebbero richiedere ulteriori indagini:  

### <a name="link-is-active"></a>Il collegamento è attivo

Non è stato rilevato alcun problema e la comunicazione nel collegamento è corrente.

Mentre un sito padre sta effettuando l'aggiornamento a una nuova versione e si visualizza lo stato del collegamento dal sito figlio, lo stato del collegamento viene visualizzato come attivo. Dopo l'aggiornamento, fino a quando il sito figlio ha la stessa versione del sito padre, lo stato del collegamento risulta attivo se visualizzato dal sito padre. Quando viene visualizzato dal sito figlio, risulta in corso di configurazione.  

### <a name="link-is-degraded"></a>Il collegamento è ridotto

La replica ha funzionato, ma almeno una oggetto o gruppo di replica è in ritardo. Monitorare i collegamenti in questo stato. Rivedere le informazioni da entrambi i siti sul collegamento per indicazioni sul possibile non funzionamento del collegamento.

Un collegamento può anche visualizzare lo stato di ridotto quando il sito che riceve i dati replicati non è in grado di confermare rapidamente i dati al database. Questo comportamento si verifica quando si replicano grandi volumi di dati, ad esempio quando si distribuisce un aggiornamento software in un numero elevato di computer. Il sito padre nel collegamento potrebbe richiedere del tempo per elaborare questo volume di dati replicati. Un ritardo di elaborazione nel sito padre lo porta a impostare lo stato del collegamento su ridotto fino a quando non può elaborare correttamente il backlog di dati.

### <a name="link-has-failed"></a>Il collegamento non è riuscito

La replica non funziona. È possibile che un collegamento di replica possa essere ripristinato senza ulteriori azioni. Per analizzare e correggere la replica su questo collegamento, usare Replication Link Analyzer (RLA).

Questo stato può anche indicare un problema con la rete fisica tra il sito padre e il sito figlio sul collegamento di replica.


## <a name="monitor-replication-status"></a><a name="BKMK_MonitorReplicationStatus"></a> Monitorare lo stato della replica

Usare il nodo **Replica di database** nell'area di lavoro **Monitoraggio** per visualizzare lo stato del collegamento di una replica. Visualizzare i dettagli sul database in ogni sito del collegamento di replica. È anche possibile visualizzare i dettagli relativi ai gruppi di replica. Per visualizzare questi dettagli, selezionare un collegamento di replica e selezionare la scheda appropriata per lo stato di replica che si vuole visualizzare.

Le sezioni seguenti forniscono informazioni dettagliate sulle diverse schede per lo stato della replica:

### <a name="summary"></a>Riepilogo

Visualizza informazioni generali sulla replica dei dati del sito e dei dati globali tra i due siti di un collegamento.  

Selezionare **Visualizza report per la cronologia dei dati di traffico** per visualizzare un report con i dettagli relativi alla larghezza di banda di rete usata dalla replica nel collegamento.  

### <a name="parent-site"></a>Sito padre

Per il sito padre su un collegamento di replica, visualizzare i dettagli sul database, che includono:  

- Porte del firewall per SQL Server  

- Spazio libero su disco  

- Percorsi dei file del database  

- Certificati  

### <a name="child-site"></a>Sito figlio

Per il sito figlio su un collegamento di replica, visualizzare i dettagli sul database, che includono:  

- Porte del firewall per SQL Server  

- Spazio libero su disco  

- Percorsi dei file del database  

- Certificati  

### <a name="initialization-detail"></a>Dettaglio di inizializzazione

Visualizzare lo stato di inizializzazione per i gruppi che vengono replicati nel collegamento. Queste informazioni consentono di identificare quando l'inizializzazione dei dati di replica è in corso o ha avuto esito negativo.  

Usare queste informazioni per identificare quando un sito potrebbe essere in *modalità di interoperabilità*. La modalità di interoperabilità si verifica quando il sito figlio non esegue la stessa versione di Configuration Manager del sito padre.  

### <a name="replication-detail"></a>Dettaglio di replica

Visualizzare lo stato della replica per ogni gruppo che viene replicato nel collegamento. Usare queste informazioni per identificare i problemi o i ritardi della replica di dati specifici. Possono contribuire a determinare le soglie di replica di database appropriate per questo collegamento. Per altre informazioni, vedere [Soglie di replica di database](../../plan-design/hierarchy/database-replication.md#BKMK_DBRepThresholds).  

> [!TIP]  
> I gruppi di replica per i dati del sito vengono inviati solo dal sito figlio al sito padre. I gruppi di replica per i dati globali vengono replicati in entrambe le direzioni.  


## <a name="replication-link-analyzer"></a><a name="BKMK_RLA"></a> Replication Link Analyzer

Configuration Manager include **Replication Link Analyzer** (RLA) che consente di analizzare e risolvere i problemi di replica. Usare RLA per correggere gli errori del collegamento quando la replica ha esito negativo. È utile anche quando la replica smette di funzionare, ma il sito non l'ha ancora segnalata come non riuscita.

Usare RLA per risolvere i problemi di replica tra i computer seguenti della gerarchia:  

- Tra un server del sito e il server di database del sito  

- Tra un server di database del sito e un altro server di database del sito, nota anche come replica tra siti  

> [!Note]  
> La direzione dell'errore di replica non è rilevante.

Eseguire Replication Link Analyzer nella console di Configuration Manager o al prompt dei comandi:  

- Per l'esecuzione nella console di Configuration Manager: passare all'area di lavoro **Monitoraggio** e selezionare il nodo **Replica di database**. Selezionare il collegamento di replica che si vuole analizzare e quindi nella barra multifunzione selezionare **Replication Link Analyzer**.  

- Per l'esecuzione al prompt dei comandi, digitare il comando seguente: `%ProgramFiles(x86)%\Microsoft Endpoint Manager\AdminConsole\bin\Microsoft.ConfigurationManager.ReplicationLinkAnalyzer.Wizard.exe <source site server FQDN> <destination site server FQDN>`  

    > [!IMPORTANT]
    > A partire dalla versione 1910, questo percorso è stato modificato in modo da usare la cartella `Microsoft Endpoint Manager`. Assicurarsi di non usare una versione precedente del file che potrebbe esistere in un'altra cartella.

Quando si esegue Replication Link Analyzer, vengono rilevati eventuali problemi mediante una serie di controlli e regole diagnostiche. I problemi identificati dallo strumento vengono visualizzati. Quando sono presenti istruzioni per risolvere un problema, vengono visualizzate. Se RLA può risolvere automaticamente un problema, lo segnala all'utente.

Al completamento dell'esecuzione di Replication Link Analyzer, i risultati vengono salvati nel report seguente basato su XML e in un file di log sul desktop dell'utente che esegue lo strumento:  

- ReplicationAnalysis.xml  

- ReplicationLinkAnalysis.log  

RLA arresta i servizi seguenti durante la risoluzione di alcuni problemi e li riavvia al termine della correzione:  

- SMS_SITE_COMPONENT_MANAGER  

- SMS_EXECUTIVE  

Se RLA non riesce a completare la correzione, riavviare questi servizi nel server del sito, se necessario.  

RLA registra tutte le azioni di analisi e correzione per fornire dettagli aggiuntivi che non vengono visualizzati nella procedura guidata.  

### <a name="rla-prerequisites"></a>Prerequisiti di RLA

L'account usato per eseguire RLA deve avere le autorizzazioni seguenti:

- Diritti di amministratore locale su ogni computer coinvolto nel collegamento di replica.

- Diritti di amministratore di sistema per ogni database di SQL Server coinvolto nel collegamento di replica.  

> [!Note]  
> L'account non richiede un ruolo di sicurezza di amministrazione basata su ruoli di Configuration Manager specifico. Un utente amministratore con accesso al nodo **Replica di database** può eseguire lo strumento nella console di Configuration Manager. Un amministratore di sistema con diritti sufficienti per ogni computer può eseguire lo strumento al prompt dei comandi.  

### <a name="rla-known-issue"></a>Problema noto di RLA

RLA genera errori di certificato di SQL Server Service Broker (SSB) per i siti primari aggiornati da System Center 2012 Configuration Manager. Questo problema è dovuto alle modifiche apportate ai nomi dei certificati in Configuration Manager Current Branch. È possibile ignorare questi errori.  


## <a name="monitoring-database-replication"></a><a name="BKMK_ProcsforMonitoringReplication"></a> Monitoraggio della replica di database  

### <a name="monitor-high-level-site-to-site-database-replication-status"></a>Monitorare a livello generale lo stato della replica di database da sito a sito

1. Nella console di Configuration Manager passare all'area di lavoro **Monitoraggio**.  

2. Selezionare il nodo **Gerarchia siti** per aprire la vista **Diagramma gerarchia**.  

3. Posizionare il puntatore del mouse sulla riga tra i due siti. Visualizzare lo stato della replica dei dati globali e del sito per questi siti.  

### <a name="monitor-the-status-of-a-replication-link"></a>Monitorare lo stato di un collegamento di replica

1. Nella console di Configuration Manager passare all'area di lavoro **Monitoraggio**.  

2. Selezionare il nodo **Replica di database** e quindi selezionare il collegamento di replica da monitorare. Selezionare infine la scheda appropriata per visualizzare diversi dettagli relativi allo stato della replica per il collegamento.  
