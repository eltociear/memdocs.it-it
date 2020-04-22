---
title: Cartella CD.Latest
titleSuffix: Configuration Manager
description: Informazioni sul processo che fornisce aggiornamenti per il prodotto dalla console di Configuration Manager.
ms.date: 03/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8db92d67-5d9c-4e9c-80d0-ae6fa0dd4817
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 577bfd865ad3872c386384c3bba95cb009ef83ec
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704049"
---
# <a name="the-cdlatest-folder-for-configuration-manager"></a>Cartella CD.Latest per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Configuration Manager include un processo che fornisce aggiornamenti per il prodotto dalla console di Configuration Manager. Per supportare questo nuovo metodo di aggiornamento di Configuration Manager viene creata una nuova cartella denominata **CD.Latest**. Questa cartella contiene una copia dei file di installazione di Configuration Manager per la versione aggiornata del sito.  

La cartella CD.Latest contiene una cartella denominata **Redist**, contenente i file ridistribuibili scaricati e usati dal programma di installazione. Questi file corrispondono alla versione dei file di Configuration Manager della cartella CD.Latest. Quando si esegue l'installazione da una cartella CD.Latest, è necessario usare i file che corrispondono alla versione del programma di installazione. È possibile impostare il programma di installazione in modo che scarichi i file nuovi e aggiornati da Microsoft oppure che usi i file della cartella Redist inclusa nella cartella CD.Latest.

Il supporto di base non include una cartella **Redist**. Il sito non crea una cartella Redist fino a quando non viene installato un aggiornamento nella console. Nel frattempo, usare la cartella Redist usata durante l'installazione di siti dal supporto di base.  

> [!TIP]  
> Assicurarsi di usare file ridistribuibili aggiornati. Se i file ridistribuibili non sono stati scaricati di recente, pianificarne il download da Microsoft tramite il programma di installazione.   

Negli scenari seguenti viene creata o aggiornata la cartella CD.Latest in un sito di amministrazione centrale o in un server del sito primario:  

- Quando si installa un aggiornamento o un hotfix dalla console di Configuration Manager, il sito crea o aggiorna la cartella nella cartella di installazione di Configuration Manager.  

- Quando si esegue l'attività di backup predefinita di Configuration Manager, il sito crea o aggiorna la cartella nel percorso della cartella di backup specificato.  

- Quando si installa un nuovo sito usando il supporto di base, il sito crea la cartella CD.Latest.


## <a name="supported-scenarios"></a>Scenari supportati

I file di origine della cartella CD.Latest sono supportati per gli scenari seguenti:  

### <a name="backup-and-recovery"></a>Backup e ripristino
Per ripristinare un sito, usare i file di origine da una cartella CD.Latest corrispondente al sito in questione. Quando si esegue un backup del sito usando l'attività di backup del sito predefinita, la cartella CD.Latest viene inclusa come parte del backup.

- Quando si reinstalla un sito come parte di un'operazione di ripristino sito, eseguire l'installazione dalla cartella CD.Latest inclusa nel backup. In questo modo, il sito viene installato usando le versioni dei file che corrispondono al backup del sito e al database del sito.  

    - Se non si ha accesso alla versione corretta della cartella CD.Latest, è possibile ottenere una cartella CD.Latest con le versioni dei file corrette installando un sito in un ambiente lab. Aggiornare quindi tale sito in modo che corrisponda alla versione che si vuole ripristinare.  

    - Se la cartella CD.Latest corretta e il relativo contenuto non sono disponibili, non è possibile ripristinare un sito. In questo caso, è necessario reinstallare il sito.  

- Quando non è disponibile una cartella CD.Latest, ma si ha un sito primario figlio o un sito di amministrazione centrale funzionante è possibile usare tale sito come riferimento per il ripristino.  

### <a name="install-a-child-primary-site"></a>Installare un sito primario figlio
Quando si vuole installare un nuovo sito primario figlio all'interno di un sito di amministrazione centrale in cui sono stati installati uno o più aggiornamenti nella console, usare il programma di installazione e i file di origine della cartella CD.Latest del sito di amministrazione centrale. Questo processo usa i file di origine per l'installazione corrispondenti alla versione del sito di amministrazione centrale. Per altre informazioni, vedere [Usare l'installazione guidata per installare i siti](../deploy/install/use-the-setup-wizard-to-install-sites.md).  

### <a name="expand-a-stand-alone-primary-site"></a>Espandere un sito primario autonomo
Quando si espande un sito primario autonomo installando un nuovo sito di amministrazione centrale, usare il programma di installazione e i file di origine della cartella CD.Latest del sito primario. Questo processo usa i file di origine per l'installazione corrispondenti alla versione del sito primario. Per altre informazioni, vedere [Espandere un sito primario autonomo](../deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand).

### <a name="install-a-secondary-site"></a>Installare un sito secondario
<!-- SCCMDocs-pr issue #3164 -->
Se si vuole installare un nuovo sito secondario all'interno di un sito primario in cui sono stati installati uno o più aggiornamenti nella console, usare i file di origine della cartella CD.Latest del sito primario. 

Per altre informazioni, vedere [Installare un sito secondario](../deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_secondary). 


## <a name="unsupported-scenarios"></a>Scenari non supportati

I file di origine della cartella CD.Latest aggiornati non sono supportati per:  

- Installazione di un nuovo sito per una nuova gerarchia  
- Aggiornamento da un sito di Microsoft System Center 2012 Configuration Manager a Configuration Manager Current Branch
- Installazione dei client di Configuration Manager
- Installazione delle console di Configuration Manager
