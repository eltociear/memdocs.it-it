---
title: Procedure consigliate per le raccolte
titleSuffix: Configuration Manager
description: Suggerimenti per la configurazione delle raccolte e della valutazione raccolta in Configuration Manager.
ms.date: 06/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 7a2abb79-9ae5-4a25-9e18-5dcf528de3bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3ee640a70eea9f2e8470e852409911d28e542bc2
ms.sourcegitcommit: 1d8bf691780b94a945e94945115d4d1df4242808
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/10/2020
ms.locfileid: "84663375"
---
# <a name="best-practices-for-collections-in-configuration-manager"></a>Procedure consigliate per le raccolte in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Il materiale sussidiario disponibile per la gestione delle raccolte può essere contraddittorio. Per motivi di prestazioni, ad esempio, è necessario limitare il numero di raccolte che vengono aggiornate di frequente. Ma aggiornare spesso le raccolte è utile, poiché la maggior parte delle funzionalità di Configuration Manager dipende dalle raccolte. Valutare con attenzione sia gli effetti sulle prestazioni che i requisiti aziendali quando si progettano e configurano le raccolte e la valutazione della raccolta.

Usare le procedure consigliate seguenti per le raccolte in Configuration Manager.  

## <a name="configure-maintenance-window-for-updates"></a>Configurare la finestra di manutenzione per gli aggiornamenti

È possibile configurare le finestre di manutenzione per le raccolte di dispositivi al fine di limitare il numero di possibili installazioni del software da parte di Configuration Manager su questi dispositivi. Se si configurano dimensioni insufficienti della finestra di manutenzione, il client potrebbe non essere in grado di installare aggiornamenti software critici, rendendo il client vulnerabile ai problemi risolti dall'aggiornamento.

Durante la pianificazione delle finestre di manutenzione tenere presenti le seguenti considerazioni importanti:

- Il tempo di esecuzione massimo per l'aggiornamento software predefinito è di 60 minuti.
- Quando Configuration Manager calcola se è possibile installare un aggiornamento, aggiunge cinque minuti al tempo di esecuzione massimo per un riavvio.
- La durata rimanente di una finestra di manutenzione deve essere superiore al tempo di esecuzione massimo dell'aggiornamento software a cui vanno aggiunti cinque minuti.

## <a name="avoid-frequent-collection-evaluation"></a>Evitare la valutazione frequente delle raccolte

Una valutazione raccolta completa valuta non solo la raccolta di destinazione, ma anche tutte le raccolte limitate dalla raccolta se si verifica un aggiornamento. Inoltre, una raccolta senza pianificazione viene comunque valutata se si aggiorna la relativa raccolta di limitazione. È quindi possibile che alcune raccolte vengano valutate più spesso del previsto.

In un ambiente di Configuration Manager trafficato, è possibile migliorare le prestazioni della valutazione raccolta ridimensionando le pianificazioni per evitare di ripetere le valutazioni. In una struttura ad albero profonda è possibile ridurre la frequenza della valutazione raccolta man mano che le raccolte scendono più a fondo nell'albero, perché le valutazioni raccolta di livello superiore attiveranno anche quelle di livello inferiore.

## <a name="understand-the-collection-evaluation-graph"></a>Informazioni sul grafico di valutazione raccolta

Tenere presente il funzionamento del grafico di valutazione raccolta, in modo da poter progettare una struttura di raccolta appropriata. Non fare affidamento sulla valutazione raccolta completa per aggiornare sempre tutte le raccolte. Se una raccolta aggiornata in modo incrementale viene aggiornata in base a una pianificazione, è possibile che le raccolte di riferimento non abilitate per gli aggiornamenti incrementali non vengano aggiornate. Poiché probabilmente si sono verificati aggiornamenti durante le valutazioni incrementali, una valutazione completa potrebbe non aggiornare la raccolta, terminando il grafico di valutazione raccolta per quel ciclo. In tal caso, non viene eseguita alcuna valutazione raccolta di riferimento. Per altre informazioni, vedere [Grafico di valutazione raccolta](collection-evaluation.md#collection-evaluation-graph).

## <a name="limit-incremental-updates"></a><a name="bkmk_incremental"></a> Limitare gli aggiornamenti incrementali

L'abilitazione degli aggiornamenti incrementali per molte raccolte può causare ritardi della valutazione. È preferibile limitare il numero di raccolte aggiornate in modo incrementale a 200. Il numero esatto dipende da:

- Il numero totale di raccolte
- La frequenza di aggiunta e modifica delle nuove risorse nella gerarchia
- Il numero di client in una gerarchia
- La complessità delle regole di appartenenza alla raccolta in una gerarchia

Se il ciclo di valutazione incrementale impiega più tempo rispetto alla frequenza di aggiornamento configurata, Configuration Manager elabora in modo costante le valutazioni raccolta e questo potrebbe influire sulle prestazioni del sistema. Ridurre il numero di raccolte aggiornate in modo incrementale o aumentare il tempo tra i cicli di valutazione incrementale.

Dato il potenziale impatto delle raccolte incrementali, è importante avere un criterio o una procedura per la creazione delle raccolte e l'assegnazione delle pianificazioni degli aggiornamenti. Alcuni esempi di considerazioni sui criteri:

- Usare gli aggiornamenti incrementali solo per le raccolte usate per l'ambito di sicurezza, le impostazioni client e le finestre di manutenzione. Questi aggiornamenti delle raccolte influiscono sul comportamento del client e sull'accesso alle risorse.
- Per le applicazioni senza approvazione delle licenze, annunciare le applicazioni alle raccolte esistenti e usare le condizioni globali per limitare la disponibilità.
- Delineare i periodi appropriati per altre raccolte con aggiornamenti completi della raccolta pianificati.

## <a name="avoid-evaluation-of-large-trees-from-the-cas"></a>Evitare la valutazione di alberi di grandi dimensioni dal sito di amministrazione centrale

In un ambiente di Configuration Manager, il sito di amministrazione centrale non valuta l'appartenenza alla raccolta. I siti primari sono gli unici siti che valutano le raccolte. I siti secondari fungono da proxy che usano solo i dati che replicano dal sito primario.

Per richiedere un aggiornamento della raccolta, il sito di amministrazione centrale invia una richiesta a ogni sito primario. I siti primari valutano la raccolta e inviano i risultati al sito di amministrazione centrale. I risultati della valutazione raccolta vengono visualizzati solo dopo che tutte le istruzioni per la valutazione raccolta vengono replicate in tutti i siti, tutti i siti valutano tutte le raccolte e tutti i dati vengono restituiti al sito di amministrazione centrale e consolidati.

Il diagramma seguente illustra il flusso quando il sito di amministrazione centrale richiede un aggiornamento manuale della raccolta:

![Aggiornamento manuale della raccolta da un sito di amministrazione centrale](media/manual-collection-update-from-cas.png)

Un aggiornamento di una raccolta da un sito di amministrazione centrale con più siti primari può richiedere molto tempo. Se una raccolta non viene valutata tempestivamente, è possibile che la richiesta venga ripetuta.

Quando un thread di valutazione raccolta inizia e carica il grafico di valutazione, la valutazione continua finché il grafico di valutazione raccolta non è vuoto. Il thread quindi termina e diventa disponibile per la valutazione successiva. Tuttavia, se un altro ciclo di valutazione raccolta viene accodato mentre il thread sta valutando le raccolte, il thread viene immediatamente riavviato per tentare una valutazione del ciclo "mancante".

Ogni metodo di valutazione viene eseguito nel proprio thread. È possibile che all'interno del thread Configuration Manager tenti di rappresentare graficamente la stessa raccolta più di una volta. Configuration Manager elimina quindi la seconda e le successive richieste.

Per impedire scenari come questi, evitare valutazioni raccolta manuali di alberi di grandi dimensioni, soprattutto quando si lavora dal sito di amministrazione centrale con più siti.

## <a name="consider-collection-depth-and-cross-referencing"></a>Considerare la profondità della raccolta e il riferimento incrociato

Per trovare un equilibrio tra i requisiti aziendali e le prestazioni, è importante comprendere la struttura della raccolta creata e le relative dipendenze rispetto ad altre raccolte. Se si crea una raccolta con regole che fanno riferimento a una o più raccolte che a loro volta fanno riferimento ad altre raccolte, tutte queste raccolte vengono valutate per creare l'appartenenza della raccolta.

Con le regole di raccolta include ed exclude di Configuration Manager, fare riferimento alle raccolte è più facile che scrivere una query WQL personalizzata. Tuttavia, se l'uso delle raccolte di tipo include ed exclude influisce pesantemente sulle prestazioni, è possibile usare il metodo di query WQL:

Include:

`Select * from SMSRSystem where SMSRSystem.ResourceId in (select ResourceID from SMS_CM_RES_COLL_[collection id])`

Exclude:

`Select * from SMSRSystem where SMSRSystem.ResourceId not in (select ResourceID from SMS_CM_RES_COLL_[collection id])`

## <a name="use-ceviewer-to-monitor-collection-evaluation"></a>Usare CEViewer per monitorare la valutazione raccolta

È possibile usare [Collection Evaluation Viewer](https://docs.microsoft.com/mem/configmgr/core/support/ceviewer) (CEViewer) per monitorare il numero di raccolte in fase di valutazione e il tempo di esecuzione dell'aggiornamento di ogni raccolta. CEViewer si trova nella cartella *CD.Latest* del server del sito.

Per eseguire manualmente un controllo simile con SQL, è possibile usare la query seguente:

```sql
SELECT [t2].[CollectionName], [t2].[SiteID], [t2].[value] AS [Seconds], [t2].[LastIncrementalRefreshTime], [t2].[IncrementalMemberChanges] AS [IncChanges], [t2].[LastMemberChangeTime] AS [MemberChangeTime]
FROM (
    SELECT [t0].[CollectionName], [t0].[SiteID], DATEDIFF(Millisecond, [t1].[IncrementalEvaluationStartTime], [t1].[LastIncrementalRefreshTime]) * 0.001 AS [value], [t1].[LastIncrementalRefreshTime], [t1].[IncrementalMemberChanges], [t1].[LastMemberChangeTime], [t1].[IncrementalEvaluationStartTime], v1.[RefreshType]
    FROM [dbo].[Collections_G] AS [t0]
    INNER JOIN [dbo].[Collections_L] AS [t1] ON [t0].[CollectionID] = [t1].[CollectionID]
    inner join v_Collection v1 on [t0].[siteid] = v1.CollectionID
    ) AS [t2]
WHERE ([t2].[IncrementalEvaluationStartTime] IS NOT NULL) AND ([t2].[LastIncrementalRefreshTime] IS NOT NULL) and (refreshtype='4' or refreshtype='6')
ORDER BY [t2].[value] DESC
```


