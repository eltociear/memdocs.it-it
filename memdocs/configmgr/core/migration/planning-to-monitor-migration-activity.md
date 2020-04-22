---
title: Monitorare la migrazione
titleSuffix: Configuration Manager
description: Informazioni su come usare la console di Configuration Manager per monitorare l'avanzamento e il completamento dei processi di migrazione.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: fc731d3f-edd7-4049-b17b-653d6693a564
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f9d1766a374c7abd8b13f503c3c7a64e35a5ac2c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693399"
---
# <a name="planning-to-monitor-migration-activity-in-configuration-manager"></a>Pianificazione del monitoraggio dell'attività di migrazione in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Con Configuration Manager è possibile monitorare la migrazione nella console di Configuration Manager che si connette alla gerarchia di destinazione. Nell'area di lavoro **Amministrazione** della console di Configuration Manager, è possibile usare il nodo **Migrazione** per monitorare l'avanzamento e il completamento dei processi di migrazione. È possibile visualizzare le informazioni di riepilogo per ciascun processo di migrazione in cui vengono individuati gli oggetti migrati, gli oggetti non ancora migrati e il numero di oggetti esclusi da un processo di migrazione. Verranno inoltre visualizzati dettagli relativi a eventuali problemi di migrazione.  

## <a name="view-migration-progress"></a>Visualizza avanzamento della migrazione  
 Per visualizzare l'avanzamento di un processo di migrazione, eseguire una delle seguenti azioni:  

-   Nell'area di lavoro **Amministrazione** della console di Configuration Manager, espandere il nodo **Processi di migrazione**, selezionare un processo e la scheda **Oggetti nel processo**.  

-   Usare i file di log di Configuration Manager per verificare l'avanzamento della migrazione o per individuare eventuali problemi. Gestione migrazione è il processo di Configuration Manager che tiene traccia delle azioni di migrazione e le registra nel file migmctrl.log nella cartella **\&lt;PercorsoInstallazione\>\\LOGS** del server del sito.  

    > [!NOTE]  
    >  Se un processo di migrazione non riesce, esaminare quanto prima i dettagli nel file migmctrl.log. Le voci del registro migrazione vengono continuamente aggiunte al file e sovrascrivono le informazioni precedenti. Se le voci vengono sovrascritte, potrebbe non essere possibile individuare se eventuali problemi relativi agli oggetti migrati dipendono da problemi di migrazione. L'attività di migrazione viene registrata nel sito principale della gerarchia, indipendentemente dal sito a cui si connette la console di Configuration Manager durante la configurazione della migrazione.  

-   Usare la creazione di report di Configuration Manager. Configuration Manager offre vari report predefiniti per la migrazione che possono essere usati direttamente o modificati per adattarli a specifiche esigenze. Per altre informazioni sui report di Configuration Manager, vedere [Introduzione ai report](../servers/manage/introduction-to-reporting.md).  
