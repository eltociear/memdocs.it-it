---
title: Aggiornare installazioni di valutazione
titleSuffix: Configuration Manager
description: Informazioni su come eseguire l'aggiornamento di un'installazione di valutazione a installazione completa di Configuration Manager.
ms.date: 02/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9a32f5a3-9917-434f-9811-106170f404be
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a8a42b2538ff1baaceb6895d371081ac2a444c5f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700459"
---
# <a name="upgrade-an-evaluation-installation-of-configuration-manager-to-a-full-installation"></a>Aggiornare un'installazione di valutazione di Configuration Manager a un'installazione completa

*Si applica a: Configuration Manager (Current Branch)*

Se Configuration Manager è stato installato come versione di valutazione, dopo 180 giorni la console di Configuration Manager passerà alla modalità di sola lettura fino a quando il prodotto non sarà attivato nella pagina **Manutenzione sito** del programma di installazione. In qualsiasi momento prima o dopo il periodo di 180 giorni, è possibile eseguire l'aggiornamento di un'installazione di valutazione a un'installazione completa.  

> [!NOTE]  
>  Quando si connette una console di Configuration Manager a un'installazione di valutazione di Configuration Manager, sulla barra del titolo della console viene visualizzato il numero di giorni restanti prima della scadenza dell'installazione di valutazione. Il numero di giorni non viene aggiornato automaticamente, ma solo quando si stabilisce una nuova connessione a un sito.  

 È possibile aggiornare i siti seguenti che eseguono un'installazione di valutazione:  

-   Sito di amministrazione centrale  
-   Sito primario  

Poiché i siti secondari non sono trattati come installazioni di valutazione, non è necessario modificare un sito secondario dopo l'aggiornamento del sito padre primario a un'installazione completa.  

Prerequisiti per l'aggiornamento di una versione di valutazione a una versione con licenza:  

-   È necessario avere un prodotto valido da usare durante l'aggiornamento.  
-   L'account deve avere i diritti di **amministratore** sul computer in cui è installato il sito.  

### <a name="to-upgrade-an-evaluation-version-of-configuration-manager-to-a-licensed-version"></a>Per aggiornare una versione di valutazione di Configuration Manager a una versione con licenza  

1.  Nel server del sito eseguire il programma di installazione di Configuration Manager **Setup.exe** dalla cartella di installazione di Configuration Manager ( **%path%\BIN\X64**). È necessario copiare il programma di installazione che si trova nel server del sito nella cartella Configuration Manager perché le opzioni di manutenzione del sito non sono disponibili quando si esegue il programma di installazione dal supporto di installazione.  
2.  Nella pagina **Prima di iniziare** scegliere **Avanti**.  
3.  Nella pagina **Riquadro attività iniziale** selezionare **Esegui una manutenzione del sito o reimposta il sito** e quindi scegliere **Avanti**.  
4.  Nella pagina **Manutenzione sito** selezionare **Aggiornare la versione di valutazione a una versione con licenza**, immettere un codice Product Key valido e quindi scegliere **Avanti**.  
5.  Nella pagina **Condizioni di licenza software Microsoft** leggere e accettare le condizioni di licenza e scegliere **Avanti**.  
6.  Nella pagina **Configurazione** scegliere **Chiudi** per completare la procedura guidata.  

    > [!NOTE]  
    >  È possibile che la barra del titolo di una console di Configuration Manager che rimane connessa al sito aggiornato indichi che nel sito è ancora attiva la versione di valutazione finché non si riconnette la console al sito.  
