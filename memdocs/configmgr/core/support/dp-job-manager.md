---
title: DP Job Queue Manager
titleSuffix: Configuration Manager
description: Usare DP Job Queue Manager per eseguire la risoluzione dei problemi e la gestione dei processi di distribuzione del contenuto ai punti di distribuzione di Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4b72922a-d11e-4aef-b309-19f5f0716f32
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9f6269d559bbcb192b1189419a8450a860d70058
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694339"
---
# <a name="dp-job-queue-manager"></a>DP Job Queue Manager

*Si applica a: Configuration Manager (Current Branch)*

Distribution Point (DP) Job Queue Manager è uno degli [strumenti di Configuration Manager](tools.md). Usare lo strumento per eseguire la risoluzione dei problemi e la gestione dei processi di distribuzione del contenuto in corso ai punti di distribuzione di Configuration Manager. 

Lo strumento consente di visualizzare l'elenco dei processi presenti nella coda del componente Package Transfer Manager. Mostra inoltre lo stato dei processi: pronto per essere eseguito, in esecuzione o nuovo tentativo in corso. Consente di modificare i processi nella coda, spostare i processi più in alto nell'elenco, annullare un processo o avviarne manualmente l'esecuzione.

Ottiene anche informazioni dal server del sito sul punto di distribuzione in cui è in esecuzione un processo. Lo strumento si connette tramite il provider al server del sito. Non si connette a ogni singolo punto di distribuzione remoto per raccogliere queste informazioni. Poiché attiva azioni e ottiene informazioni tramite il provider, le modifiche dai punti di distribuzione remoti vengono applicate con un ritardo.



## <a name="usage"></a>Utilizzo

Eseguire **DPJobMgr.exe**. Il menu principale dello strumento contiene le schede seguenti: 

- [Connessione](#bkmk_connect): consente di stabilire la connessione iniziale al server del sito primario  

- [Informazioni generali](#bkmk_overview): riepiloga tutti i processi in esecuzione in tutti i punti di distribuzione in una singola vista  

- [Informazioni punto di distribuzione](#bkmk_dp-info): consente di eseguire la selezione multipla dei punti di distribuzione per tenerne traccia e gestire un singolo processo di interesse  

- [Gestione processi](#bkmk_manage-jobs): Elenca tutti i processi e i relativi stati in un'unica visualizzazione semplice. Modificare o spostare i processi più in alto nell'elenco, annullare o avviare manualmente un processo.  


### <a name="connect-tab"></a><a name="bkmk_connect"></a> Scheda Connetti

Usare questa scheda per stabilire la connessione iniziale al server del sito primario. Usa le credenziali dell'utente attualmente connesso. Non è possibile connettersi al sito di amministrazione centrale o ai siti secondari. Per la connessione è necessario il ruolo di sicurezza **amministratore completo**.

Al termine una notifica nella parte inferiore dello strumento conferma la corretta esecuzione della connessione al server del sito. 


### <a name="overview-tab"></a><a name="bkmk_overview"></a> Scheda Informazioni generali

Riepiloga tutti i processi in tutti i punti di distribuzione. Vedere le colonne seguenti:  

- **Punto di distribuzione**: elenca i nomi dei punti di distribuzione  

- **Processi in esecuzione**: indica il numero di processi simultanei in esecuzione in un punto di distribuzione specifico.  

    > [!Tip]  
    > Un'impostazione del sito determina il numero di distribuzioni software simultanee. Modificare questa impostazione in Proprietà componente distribuzione software.  

- **Totale processi**: indica il numero di tutti i processi che hanno come destinazione un punto di distribuzione specifico. Sono inclusi i processi in esecuzione, in attesa di esecuzione o di cui si sta eseguendo un nuovo tentativo.  

- **Total Retries** (Totale tentativi): indica il numero di volte per cui viene tentata l'esecuzione dei processi in un punto di distribuzione specifico. Un numero più alto può indicare un problema generale relativo allo specifico punto di distribuzione.  


> [!Tip]  
> - Per ordinare ciascuna colonna in questa scheda, fare clic sul nome della colonna.  
> 
> - Aggiornare manualmente le informazioni in questa scheda facendo clic su **Aggiorna**.  
> 
> - Aggiornare automaticamente le informazioni in questa scheda facendo clic su **Start Auto Refresh** (Avvia aggiornamento automatico) e impostando l'intervallo di aggiornamento automatico. L'intervallo di aggiornamento predefinito è due minuti.  


### <a name="distribution-point-info-tab"></a><a name="bkmk_dp-info"></a> Scheda Informazioni punto di distribuzione

Elenca tutti i punti di distribuzione sotto il sito connesso. Nel riquadro a sinistra sono elencati tutti i punti di distribuzione. Fare clic su **Seleziona tutto** o **Deseleziona tutto** in base alle necessità oppure eseguire la selezione multipla di punti di distribuzione specifici in questo elenco. Nel riquadro a destra sono elencati i processi relativi ai punti di distribuzione selezionati.

Sono presenti otto colonne:  

- **Icona stato**: le icone di stato sono tre:  

    - **Pronto**: indica che sono stati completati tutti i passaggi di verifica per un processo specifico. Il processo è pronto per essere aggiunto ai processi simultanei in esecuzione. I processi in questo stato sono in genere in una fase di attesa. Rimangono in attesa che vengano completati i processi in esecuzione prima di riservarsi uno spazio.  

    - **In esecuzione**: indica che un processo specifico è attualmente in esecuzione in un punto di distribuzione. Per i processi ad esecuzione prolungata (pacchetti di grandi dimensioni), in genere un valore indica il tempo dallo stato di avanzamento (%) fino al completamento. Mostra questa percentuale nella colonna **Indicatore di stato** in questa visualizzazione. Per i pacchetti di piccole dimensioni, la colonna **Indicatore di stato** potrebbe non contenere alcun valore. Il processo potrebbe essere già stato completato prima di ricevere lo stato dal punto di distribuzione remoto.  

    - **Riprova**: indica che un determinato processo ha avuto esito negativo ed è in corso un nuovo tentativo di esecuzione. Il nuovo tentativo viene eseguito dopo l'intervallo tentativi. Questo intervallo è configurabile e impostato su 30 minuti per impostazione predefinita.  

- **Software**: nome del pacchetto che ha come destinazione un punto di distribuzione specifico  

- **ID pacchetto**: ID del pacchetto che ha come destinazione un punto di distribuzione specifico  

- **Dimensioni**: dimensioni del pacchetto espresse in KB  

- **Stato**: percentuale di completamento del processo. Per altre informazioni, vedere la descrizione dell'icona di stato **In esecuzione**.  

- **Start/Restart Time** (Orario avvio/riavvio): per un processo in esecuzione, si tratta dell'orario di avvio (in verde). Per un nuovo tentativo questo valore è l'ora in cui verrà eseguito un nuovo tentativo per il processo.  

- **Tentativi**: numero di tentativi di esecuzione del pacchetto.  

- **Nome punto di distribuzione**: nome di dominio completo (FQDN) del punto di distribuzione  

> [!Tip]  
> - Per ordinare ciascuna colonna in questa scheda, fare clic sul nome della colonna.  
> 
> - Aggiornare manualmente le informazioni in questa scheda facendo clic su **Aggiorna**.  
> 
> - Aggiornare automaticamente le informazioni in questa scheda facendo clic su **Start Auto Refresh** (Avvia aggiornamento automatico) e impostando l'intervallo di aggiornamento automatico. L'intervallo di aggiornamento predefinito è due minuti.  
> 
> - Se è necessario modificare uno specifico processo, fare clic con il pulsante destro del mouse sul processo in questa visualizzazione e selezionare **Gestisci processo**. Questa azione apre la scheda [Gestione processi](#bkmk_manage-jobs).  


### <a name="manage-jobs-tab"></a><a name="bkmk_manage-jobs"></a> Scheda Gestione processi

Elenca tutti i processi e i relativi stati in un'unica visualizzazione semplice. Contiene le stesse otto colonne presenti nella scheda [Informazioni punto di distribuzione](#bkmk_dp-info). In questa visualizzazione fare clic con il pulsante destro del mouse sui processi per le azioni seguenti:  

- **Esegui**: avvia un processo che si trova in uno stato diverso da quello di esecuzione  

- **Sposta all'inizio**: sposta uno o più processi all'inizio della coda. Questa azione può comportare l'esecuzione immediata dei processi. Un processo con priorità più bassa può essere sospeso eseguendo questa azione.  

- **Sposta su**: sposta un processo specifico una riga più in alto. L'esecuzione di un processo con priorità più bassa può essere sospesa eseguendo questa azione.  

- **Sposta giù**: sposta un processo specifico una riga più in basso.  

- **Sposta alla fine**: sposta uno o più processi alla fine della coda.  

    > [!Tip]  
    > Per spostare i processi nell'elenco eseguire un'operazione di trascinamento della selezione.  

- **Annulla**: tenta di annullare uno o più processi.  

    > [!Note]  
    > Non è possibile annullare i lavori prossimi all'ora di completamento finale. Se il server del sito è anche un punto di distribuzione, non è possibile annullare i processi nel server del sito.  



## <a name="see-also"></a>Vedere anche

- [Concetti di base sulla gestione dei contenuti](../plan-design/hierarchy/fundamental-concepts-for-content-management.md)
- [Package Transfer Manager](../plan-design/hierarchy/package-transfer-manager.md)
