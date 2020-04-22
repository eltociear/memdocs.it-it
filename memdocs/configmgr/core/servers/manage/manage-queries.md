---
title: Gestire le query
titleSuffix: Configuration Manager
description: Informazioni su come gestire le query. Include una tabella di riferimento dettagliata.
ms.date: 04/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e562e2a0-8df8-4952-952f-e8c38461c612
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 37050a3a96b732df3f56269592e049077008ab2b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694469"
---
# <a name="how-to-manage-queries-in-configuration-manager"></a>Come gestire le query in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Questo articolo è utile per gestire le query in Configuration Manager.  

 Per informazioni su come creare query, vedere [Come creare query in Configuration Manager](../../../core/servers/manage/create-queries.md).  

## <a name="manage-queries"></a>Gestire le query
 Nell'area di lavoro **Monitoraggio** selezionare **Query**, selezionare la query da gestire e quindi selezionare un'attività di gestione.  

 Nella tabella seguente vengono fornite informazioni sulle attività di gestione.  

|Attività di gestione|Dettagli| 
|---------------------|-------------|
|**Esegui**|Esegue la query selezionata e visualizza i risultati nella console di Configuration Manager.|
|**Installa client**|Apre la **procedura guidata di installazione client** che consente di installare il client di Configuration Manager nei computer restituiti dalla query selezionata.<br /><br /> Questa opzione non è disponibile per le query che restituiscono dispositivi mobili, utenti o gruppi di utenti. <br /><br /> Per altre informazioni su come installare i client di Configuration Manager usando push client, vedere [Come distribuire i client nei computer Windows](../../clients/deploy/deploy-clients-to-windows-computers.md).| 
|**Export**|Apre l'**Esportazione guidata oggetti**. Questa procedura guidata consente di esportare la query in un file MOF (Managed Object Format) che è quindi possibile importare in un altro sito.
|**Sposta**|Apre la finestra di dialogo **Sposta elementi selezionati**. Questa finestra di dialogo consente di spostare la query selezionata in una cartella creata in precedenza nel nodo **Query**.|

## <a name="next-steps"></a>Passaggi successivi 
 [Creare query](../../../core/servers/manage/create-queries.md)
