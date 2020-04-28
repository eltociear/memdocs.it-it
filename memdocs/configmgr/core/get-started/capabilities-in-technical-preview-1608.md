---
title: Funzionalità nella Technical Preview 1608
titleSuffix: Configuration Manager
description: Informazioni sulle funzionalità disponibili nella versione Technical Preview 1608 per Configuration Manager.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 63e1df5e-637c-4b07-b7ec-95340f43a805
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: fd668760a6b5d1a16cfbb8549063da4f7e8a8b7d
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074181"
---
# <a name="capabilities-in-technical-preview-1608-for-configuration-manager"></a>Funzionalità della versione Technical Preview 1608 per Configuration Manager

*Si applica a: Configuration Manager (Technical Preview Branch)*

Questo articolo presenta le funzionalità disponibili nella Technical Preview per Configuration Manager versione 1608. È possibile installare questa versione per aggiornare e aggiungere nuove funzionalità al sito di Technical Preview di Configuration Manager.      Prima di installare questa versione Technical Preview, consultare l'argomento introduttivo [Technical Preview per Center Configuration Manager](../../core/get-started/technical-preview.md) per acquisire familiarità con i requisiti generali e con le limitazioni per l'uso di una versione Technical Preview, con le modalità di aggiornamento tra le versioni e con le modalità per offrire commenti e suggerimenti sulle funzionalità di una versione Technical Preview.    


**Di seguito sono riportate le nuove funzionalità disponibili con questa versione.**  




##  <a name="improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step"></a>Miglioramenti del passaggio della sequenza di attività Prepara client ConfigMgr per l'acquisizione  
Il passaggio Prepara client ConfigMgr a questo punto rimuove completamente il client di Configuration Manager, invece di rimuovere solo le informazioni sulla chiave. Quando la sequenza di attività distribuisce l'immagine del sistema operativo acquisita, verrà installato ogni volta un nuovo client di Configuration Manager.  


## <a name="improvements-to-software-center"></a>Miglioramenti a Software Center
* Le schede **Applicazioni**, **Aggiornamenti** e **Sistemi operativi** di Software Center consentono di visualizzare il software aggiunto di recente. I numeri nel riquadro di spostamento mostrano i nuovi software contenuti in ogni scheda.
* Gli utenti possono ora richiedere l'approvazione per le applicazioni e quindi visualizzare la cronologia delle richieste nella vista **Dettagli applicazione** di Software Center. Il pulsante **Request** (Richiedi) in **Dettagli applicazione** non reindirizza al Catalogo applicazioni basato sul Web.

## <a name="improvements-to-asset-intelligence"></a>Miglioramenti ad Asset Intelligence
Alle proprietà dei software di inventario è stato aggiunto un campo che consente di impostare una relazione di tipo padre e figlio con un altro software. Nell'elenco Software di inventario è possibile visualizzare il padre di qualsiasi software e anche nascondere tutti i software figlio.

### <a name="configure-a-parent-to-child-relationship"></a>Configurare una relazione padre-figlio
  1. Per impostare un software padre nel nodo Software di inventario, fare clic con il pulsante destro del mouse su un elemento software nell'elenco **Software di inventario** e scegliere **Proprietà**.
  2. Nella finestra di dialogo visualizzata selezionare il software che si desidera impostare come software padre nella selezione iniziale.

### <a name="filter-the-software-display"></a>Filtrare la visualizzazione del software
Dopo aver definito le relazioni padre-figlio, è possibile filtrare la visualizzazione per mostrare solo i software padre o i software che non presentano relazioni definite. In questo modo vengono nascosti tutti i software impostati come figli di un altro software di inventario. A tale scopo, procedere nel seguente modo:
   1. Sulla barra di ricerca, scegliere **Aggiungi criteri**
   2. Selezionare **Software padre**, cambiare il valore dei criteri su **è vuoto** e quindi fare clic su **Cerca**.

Ora vengono visualizzati solo i software padre o i software che non presentano relazioni definite. I software che sono soltanto elementi figlio di un altro titolo non vengono visualizzati.

## <a name="remote-control-keyboard-translation"></a>Traduzione della tastiera di controllo remoto
In passato Configuration Manager trasmetteva la posizione del tasto dal percorso del visualizzatore al percorso del condivisore. In questo modo si riscontravano problemi per le configurazioni della tastiera che differivano dal visualizzatore al condivisore. Ad esempio, se un visualizzatore con tastiera inglese digitava "A", la tastiera francese del condivisore generava una "Q". Il comportamento predefinito è stato modificato in modo che il carattere stesso venga trasmesso dalla tastiera del visualizzatore al condivisore e affinché al condivisore arrivi ciò che il visualizzatore intende digitare.

Il visualizzatore può disattivare questo comportamento se preferisce digitare in base alla disposizione della tastiera del condivisore. Per modificare il comportamento, in **Controllo remoto di Configuration Manager** scegliere **Azione** e poi scegliere **Abilita tastiera e traduzione** per trasmettere la posizione del tasto.

> [!NOTE]
>
> I tasti speciali, ad esempio ~!#@$%, non verranno tradotti correttamente.
