---
title: Valutazione delle raccolte
titleSuffix: Configuration Manager
description: Informazioni sul processo, sui tipi e sui trigger di valutazione raccolta. Informazioni sul grafico e sulla gerarchia di valutazione raccolta.
ms.date: 06/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d17e1188-d277-438f-9236-db9cd213b421
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 15b58b841ca87cf2b5e04c98dfd35c487c941e78
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88693319"
---
# <a name="collection-evaluation-in-configuration-manager"></a>Valutazione raccolta in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Configuration Manager usa la *valutazione raccolta* per aggiornare l'appartenenza alla raccolta, in base alle regole di raccolta definite. L'ambito e la durata della valutazione raccolta variano a seconda della configurazione del sito e della raccolta e del tipo di valutazione. 

È importante comprendere il comportamento della valutazione raccolta in modo da poter prendere decisioni appropriate riguardo alla progettazione della raccolta. Per indicazioni e consigli per la valutazione raccolta, vedere [Procedure consigliate per le raccolte](best-practices-for-collections.md).

## <a name="evaluation-process"></a>Processo di valutazione

Il file [colleval.log](../../../plan-design/hierarchy/log-files.md#BKMK_ServerLogs) registra quando l'analizzatore di raccolte crea, modifica ed elimina le raccolte.

A un livello elevato, ogni singola valutazione raccolta e ogni aggiornamento seguono questi passaggi:

![Processo di aggiornamento della raccolta di alto livello](media/high-level-collection-update-process.png)

1. Eseguire la query di raccolta.
1. Aggiungere tutti i sistemi che sono membri diretti.
1. Valutare tutte le raccolte di tipo *include*.
   
   Se le raccolte include contengono anche regole di query o raccolte di tipo include o exclude, devono essere valutate. Se le stesse raccolte include sono raccolte di limitazione, valutare le eventuali raccolte sottostanti. Dopo aver valutato completamente l'albero, restituire i risultati alla raccolta chiamante.
   
1. Eseguire un `AND` logico tra i risultati restituiti e la raccolta di limitazione.
1. Valutare le raccolte *exclude*.
   
   Se le raccolte exclude contengono anche regole di query o raccolte di tipo include o exclude, devono essere valutate. Se queste raccolte sono raccolte di limitazione, valutare le eventuali raccolte sottostanti. Dopo aver valutato completamente l'albero, restituire i risultati alla raccolta chiamante.
   
1. Confrontare il set di risultati della valutazione dei membri diretti e delle raccolte include con i risultati della valutazione delle raccolte exclude.
1. Scrivere le modifiche nel database ed eseguire gli aggiornamenti.
1. Attivare anche eventuali raccolte dipendenti da aggiornare. Le raccolte dipendenti sono raccolte limitate dalla raccolta corrente o che fanno riferimento alla raccolta corrente usando regole di inclusione o esclusione.

## <a name="collection-evaluation-types-and-triggers"></a>Tipi e trigger di valutazione raccolta

Questi tipi di thread gestiscono la valutazione raccolta a seconda del tipo di valutazione:

- **Primaria** per gli aggiornamenti pianificati delle raccolte
- **Ausiliaria** per aggiornare manualmente le raccolte con raccolte dipendenti
- **Singola** per aggiornare manualmente le raccolte senza raccolte dipendenti
- **Rapida** per aggiornamenti incrementali della raccolta

Nella tabella seguente vengono descritti i trigger di valutazione raccolta e i relativi tipi di valutazione. 

| Trigger | Tipo di valutazione | Descrizione |
|---------|-----------------|-------------|
|Manuale|Singola o ausiliaria|Manual è la valutazione raccolta con la massima priorità. Quando un amministratore richiede una valutazione manuale della raccolta, l'analizzatore di raccolte assegna il successivo thread di valutazione disponibile alla valutazione.|
|Scheduled|Primario|Il processo di valutazione pianificata è identico a quello della valutazione manuale, ad eccezione del fatto che la valutazione è basata sul tempo anziché sugli eventi.|
|Staging|Singola o ausiliaria|Tutte le raccolte dipendono direttamente o indirettamente da **Tutti i sistemi** o **Tutti gli utenti e i gruppi di utenti**. Entrambe le raccolte eseguono una valutazione raccolta completa ogni giorno alle 4:00. Una modifica apportata a una di queste raccolte attiva gli aggiornamenti delle raccolte dipendenti, in base a un [grafico completo delle raccolte](#collection-evaluation-graph).
|Incremental|Rapida|La valutazione incrementale usa un grafico di valutazione raccolta per valutare e aggiornare le raccolte dipendenti se viene modificato un aggiornamento dell'appartenenza alla raccolta incrementale. Configuration Manager monitora e aggiorna gli oggetti delle risorse in tutte le raccolte configurate per gli aggiornamenti incrementali.<br /><br />Se una query di raccolta si basa su informazioni che verranno aggiornate in un secondo momento, ad esempio l'inventario hardware, Configuration Manager si limita ad aggiungere o rimuovere la risorsa dalla raccolta durante l'aggiornamento pianificato della raccolta.|

## <a name="collection-evaluation-graph"></a>Grafico di valutazione raccolta

Un *grafico di valutazione raccolta* esegue il mapping di tutte le raccolte correlate alla raccolta selezionata per la valutazione. La valutazione raccolta include la raccolta di destinazione e tutte le raccolte correlate presenti nel grafico di valutazione raccolta.

Quando viene avviata la valutazione raccolta, Configuration Manager compila un grafico che include tutte le raccolte che potrebbero richiedere la valutazione in seguito alle modifiche apportate alla raccolta di destinazione, a partire dal livello più alto del ciclo. L'analizzatore di raccolte si sposta all'interno del grafico, valutando una ad una tutte le appartenenze alla raccolta. Completata la valutazione della raccolta, l'analizzatore di raccolte rimuove le raccolte di livello inferiore che non sono interessate da questo ciclo dal grafico di valutazione raccolta.

Se una o più raccolte valutate presentano una regola di inclusione o esclusione, l'analizzatore di raccolte aggiunge la raccolta inclusa o esclusa al grafico, insieme alle raccolte limitate dalla raccolta. Se sono state apportate modifiche durante la valutazione delle raccolte di tipo include ed exclude, il grafico continua su quel ramo prima di tornare al ramo principale.

Configuration Manager crea due tipi di grafico di valutazione, *incrementale* o *completo*.

### <a name="incremental-collection-evaluation"></a>Valutazione raccolta incrementale

Quando i dati della tabella cambiano, un trigger SQL inserisce una riga nella tabella **CollectionNotifications**. Quando successivamente viene generata una pianificazione della valutazione raccolta, applica `AND` all'ID della risorsa e alla query di raccolta esistente e attiva gli aggiornamenti per le raccolte abilitate per le raccolte *incrementali*.

La valutazione raccolta incrementale esegue una query per ogni computer. La configurazione del sito predefinita per la valutazione raccolta incrementale è ogni cinque minuti.

Un grafico di valutazione raccolta incrementale esegue il mapping delle raccolte a cui si fa riferimento solo se sono abilitate per la valutazione incrementale. Se una valutazione incrementale è limitata a una raccolta non abilitata per la valutazione incrementale, il grafico valuta la raccolta in base all'appartenenza esistente della raccolta di limitazione. 

Nel diagramma seguente, ad esempio, sono indicate le risorse appena individuate applicabili a tutte le raccolte. Tuttavia, la valutazione raccolta aggiorna solo le raccolte **Tutti i server** e **Tutti i controller di dominio**. L'analizzatore di raccolte non valuta le altre raccolte, perché la raccolta **Tutti i server membri** non è abilitata per la valutazione incrementale.

![Esempio di grafico di valutazione raccolta incrementale](media/incremental-collection-evaluation-graph.png)

### <a name="full-collection-evaluation"></a>Valutazione raccolta completa

Le valutazioni raccolta manuali o pianificate creano un grafico di valutazione raccolta *completo* di tutte le raccolte dipendenti. Il grafico include tutte le raccolte che fanno riferimento alla raccolta che si sta aggiornando e alle raccolte successive. Configuration Manager continua a valutare il grafico finché vengono eseguiti aggiornamenti per le raccolte in fase di elaborazione.

Il diagramma seguente illustra in che modo una richiesta di aggiornamento di una raccolta pianificata o manuale per la raccolta **Tutti i server** genera un grafico completo che include tutte le raccolte applicabili. Il nuovo server DNS e le risorse del controller di dominio rientrano nell'ambito delle query di appartenenza di tutte le raccolte, quindi vengono aggiornate tutte le raccolte.

![Grafico di valutazione raccolta completa - Esempio 1](media/full-collection-evaluation-graph-1.png)

Una valutazione completa non valuta sempre tutte le raccolte. Il grafico di valutazione raccolta continua a valutare le raccolte dipendenti solo se si verifica un aggiornamento all'attuale raccolta di riferimento. Se una raccolta aggiornata in modo incrementale viene aggiornata durante le valutazioni incrementali pianificate, è possibile che le raccolte di riferimento non abilitate per gli aggiornamenti incrementali non vengano aggiornate. Una valutazione completa non aggiorna la raccolta, terminando il grafico di valutazione raccolta ed eventuali valutazioni raccolta di riferimento per quel ciclo. 

Nell'esempio seguente l'installazione di DNS nel server esistente fa diventare il server membro della raccolta **Server DNS**, ma poiché non è disponibile alcun aggiornamento per la relativa raccolta di limitazione **Tutti i server membri**, la valutazione completa non valuta la raccolta **Server DNS**. Il successivo ciclo di valutazione incrementale valuterà la raccolta **Server DNS**, perché si tratta di una raccolta incrementale.

![Grafico di valutazione raccolta completa - Esempio 2](media/full-collection-evaluation-graph-2.png)

## <a name="next-steps"></a>Passaggi successivi
- [Come creare le raccolte](create-collections.md)
- [Procedure consigliate per le raccolte](best-practices-for-collections.md)
- [Collection Evaluation Viewer](../../../support/ceviewer.md)
- Sessione [ConfigMgrDogs Troubleshoot ConfigMgr 2012](https://channel9.msdn.com/Events/TechEd/Australia/2014/DCI411) su TechEd Australia