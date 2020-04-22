---
title: Collection Evaluation Viewer
titleSuffix: Configuration Manager
description: Usare Collection Evaluation Viewer per visualizzare e risolvere i problemi del processo di valutazione raccolta in Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: caad2d93-087c-4dc0-a2a7-6a2fd808b4c8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9ab75238e5dd26872847e68863ef603d3ac22671
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707889"
---
# <a name="collection-evaluation-viewer"></a>Collection Evaluation Viewer

*Si applica a: Configuration Manager (Current Branch)*

Collection Evaluation Viewer è uno [strumento di Configuration Manager](tools.md). Usarlo per visualizzare e risolvere i problemi del processo di valutazione raccolta nel server del sito primario.

Questo strumento fornisce le informazioni seguenti:  

- Informazioni sia cronologiche che in tempo reale per le valutazioni raccolta incrementali  

- Stato della coda di valutazione  

- Ora di completamento delle valutazioni raccolta  

- Raccolte attualmente in fase di valutazione  

- Ora prevista di inizio e completamento di una valutazione raccolta  



## <a name="about-collection-evaluation"></a>Informazioni su Collection Evaluation Viewer

Il processo di valutazione raccolta viene eseguito valutando le regole di appartenenza di una raccolta per aggiornarne i membri. Il sito inserisce una raccolta che sta valutando in una di quattro diverse code:  

- **Manual Queue** (Coda manuale): per le raccolte selezionate manualmente da un amministratore per la valutazione dalla console  

- **Nuova coda**: per le nuove raccolte create  

- **Full Queue** (Coda completa): per le raccolte su cui eseguire una valutazione completa  

- **Incremental Queue** (Coda incrementale): per le raccolte con valutazione incrementale  

Esistono quattro thread che vengono eseguiti per valutare le raccolte presenti nelle code precedenti. Ogni coda include una serie di matrici e ogni matrice include le raccolte da valutare. Il thread in esecuzione per la coda seleziona una raccolta dalla matrice ed esegue la valutazione. La lunghezza della coda indica il numero di matrici nella coda.



## <a name="requirements"></a>Requisiti

- Eseguire lo strumento nel server del sito  

- Eseguire lo strumento tramite un utente amministratore con almeno il ruolo **Analista di sola lettura**  

- L'utente deve avere anche l'autorizzazione **Lettura** per il database del sito in SQL



## <a name="usage"></a>Utilizzo

Eseguire **CEViewer.exe**. Il menu principale dello strumento contiene le schede seguenti: 

- [Connessione](#bkmk_connect): stabilisce la connessione iniziale al server del sito primario e a SQL Server  

- [Full Evaluation](#bkmk_full-eval) (Valutazione completa): elenca le informazioni dettagliate su tutte le valutazioni complete precedenti   

- [Incremental evaluation](#bkmk_incremental-eval) (Valutazione incrementale): elenca le informazioni dettagliate su tutte le valutazioni incrementali precedenti  

- [All Queues](#bkmk_all-q) (Tutte le code): riepiloga le valutazioni raccolta correnti per tutte e quattro le code  

- [Manual Queue](#bkmk_manual-q) (Coda manuale): elenca le informazioni dettagliate sulla valutazione raccolta corrente nella coda manuale  

- [Nuova coda](#bkmk_new-q): elenca le informazioni dettagliate sulla valutazione raccolta corrente nella nuova coda  

- [Full Queue](#bkmk_full-q) (Coda completa): elenca le informazioni dettagliate sulla valutazione raccolta corrente nella coda completa  

- [Incremental Queue](#bkmk_incremental-q) (Coda incrementale): elenca le informazioni dettagliate sulla valutazione raccolta corrente nella coda incrementale  


### <a name="connect-tab"></a><a name="bkmk_connect"></a> Scheda Connetti

Questa scheda consente di stabilire la connessione iniziale al server del sito primario. Lo strumento stabilisce anche una connessione al server SQL che ospita il database del sito.

Le connessioni sia al server del sito primario che ai server SQL usano le credenziali dell'utente connesso corrente. Non sono supportate le connessioni al sito di amministrazione centrale o a un sito secondario. Nessun processo di valutazione raccolta viene eseguito in tali siti.

Dopo che lo strumento ha stabilito una connessione, nella parte inferiore di Collection Evaluation Viewer viene visualizzata una notifica, che conferma la connessione dello strumento a SQL server. 


### <a name="full-evaluation-tab"></a><a name="bkmk_full-eval"></a> Scheda Full Evaluation (Valutazione completa)

Mostra informazioni dettagliate sulle valutazioni raccolta complete precedenti. Sono presenti otto colonne:  

- **Nome raccolta**: nome della raccolta  

- **ID sito**: ID del sito della raccolta   

- **Tempo di esecuzione**: durata, in secondi, dell'ultima esecuzione della valutazione raccolta  

- **Last Evaluation Completion Time** (Ora completamento ultima valutazione): ora in cui è stata completata l'ultima valutazione raccolta  

- **Next Evaluation Time** (Ora valutazione successiva): ora di inizio della valutazione completa successiva  

- **Member Changes** (Modifiche ai membri): modifiche apportate ai membri nell'ultima valutazione raccolta. Queste modifiche sono in positivo (membri aggiunti) o in negativo (membri rimossi).  

- **Last Member Change Time** (Ora ultima modifica membri): ora in cui è stata apportata la modifica più recente all'appartenenza nella valutazione raccolta  

- **Percentuale**: percentuale del periodo di valutazione per questa raccolta rispetto al periodo di valutazione totale (tutte le raccolte)  


### <a name="incremental-evaluation-tab"></a><a name="bkmk_incremental-eval"></a> Scheda Incremental evaluation (Valutazione incrementale)

Mostra informazioni dettagliate sulle valutazioni raccolta incrementali precedenti. Sono presenti sette colonne:  

- **Nome raccolta**: nome della raccolta  

- **ID sito**: ID del sito della raccolta   

- **Tempo di esecuzione**: durata, in secondi, dell'ultima esecuzione della valutazione raccolta  

- **Last Evaluation Completion Time** (Ora completamento ultima valutazione): ora in cui è stata completata l'ultima valutazione raccolta  

- **Member Changes** (Modifiche ai membri): modifiche apportate ai membri nell'ultima valutazione raccolta. Queste modifiche sono in positivo (membri aggiunti) o in negativo (membri rimossi).  

- **Last Member Change Time** (Ora ultima modifica membri): ora in cui è stata apportata la modifica più recente all'appartenenza nella valutazione raccolta  

- **Percentuale**: percentuale del periodo di valutazione per questa raccolta rispetto al periodo di valutazione totale (tutte le raccolte)  


### <a name="all-queues-tab"></a><a name="bkmk_all-q"></a> Scheda All Queues (Tutte le code)

Riepiloga le valutazioni raccolta in tempo reale per tutte e quattro le code. Sono presenti sei sezioni:  

- **Riepilogo**: elenca il numero totale di raccolte e la lunghezza delle code per tutte le raccolte in tutte e quattro le code  

- **Running Evaluation** (Valutazione in esecuzione): indica la raccolta di cui è attualmente in corso l'esecuzione in ogni coda e da quanto è in esecuzione  

- **Manual Update** (Aggiornamento manuale): illustra un breve riepilogo delle raccolte da valutare, l'ora di completamento prevista e l'ordine della valutazione nella coda manuale  

- **Nuova raccolta**: illustra un breve riepilogo delle raccolte da valutare, l'ora di completamento prevista e l'ordine della valutazione nella coda della nuova raccolta  

- **Full Evaluation** (Valutazione completa): illustra un breve riepilogo delle raccolte da valutare, l'ora di completamento prevista e l'ordine della valutazione nella coda della valutazione completa  

- **Incremental evaluation** (Valutazione incrementale): illustra un breve riepilogo delle raccolte da valutare, l'ora di completamento prevista e l'ordine della valutazione nella coda della valutazione incrementale  


### <a name="manual-queue-tab"></a><a name="bkmk_manual-q"></a> Scheda Manual Queue (Coda manuale)

Mostra le informazioni sulla valutazione raccolta manuale attualmente in fase di valutazione. L'ordine nell'elenco è quello in cui verrà valutata la raccolta. Sono presenti quattro colonne:  

- **Nome raccolta**: nome della raccolta  

- **ID sito**: ID del sito della raccolta   

- **Tempo previsto di completamento**: ora di fine prevista per la valutazione  

- **Estimated Run Time** (Tempo di esecuzione stimato): durata prevista della valutazione nel formato giorni:ore:minuti:secondi  


### <a name="new-queue-tab"></a><a name="bkmk_new-q"></a> Scheda Nuova coda

Mostra le informazioni in tempo reale sulla nuova valutazione raccolta in fase di valutazione. L'ordine nell'elenco è quello in cui verrà valutata la raccolta. Sono presenti quattro colonne:  

- **Nome raccolta**: nome della raccolta  

- **ID sito**: ID del sito della raccolta   

- **Tempo previsto di completamento**: ora di fine prevista per la valutazione  

- **Estimated Run Time** (Tempo di esecuzione stimato): durata prevista della valutazione nel formato giorni:ore:minuti:secondi  


### <a name="full-queue-tab"></a><a name="bkmk_full-q"></a> Scheda Full Queue (Coda completa)

Mostra le informazioni sulla valutazione raccolta completa attualmente in fase di valutazione. L'ordine nell'elenco è quello in cui verrà valutata la raccolta. Sono presenti quattro colonne:  

- **Nome raccolta**: nome della raccolta  

- **ID sito**: ID del sito della raccolta   

- **Tempo previsto di completamento**: ora di fine prevista per la valutazione  

- **Estimated Run Time** (Tempo di esecuzione stimato): durata prevista della valutazione nel formato giorni:ore:minuti:secondi  


### <a name="incremental-queue-tab"></a><a name="bkmk_incremental-q"></a> Scheda Incremental Queue (Coda incrementale)

Mostra le informazioni sulla valutazione raccolta incrementale attualmente in fase di valutazione. L'ordine nell'elenco è quello in cui verrà valutata la raccolta. Sono presenti quattro colonne:  

- **Nome raccolta**: nome della raccolta  

- **ID sito**: ID del sito della raccolta   

- **Tempo previsto di completamento**: ora di fine prevista per la valutazione  

- **Estimated Run Time** (Tempo di esecuzione stimato): durata prevista della valutazione nel formato giorni:ore:minuti:secondi  



