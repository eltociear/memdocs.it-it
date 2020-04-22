---
title: Supporto internazionale
titleSuffix: Configuration Manager
description: Configurare Configuration Manager per la conformità a requisiti internazionali specifici.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 46dd9cb2-a812-4b6a-a747-b840f92fef8b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 05e90466ec3ee9529e4eb770839347ad7ac94447
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704599"
---
# <a name="international-support-in-configuration-manager"></a>Supporto internazionale in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Le sezioni seguenti illustrano i dettagli tecnici che consentono di garantire la conformità di Configuration Manager a requisiti internazionali specifici.  

## <a name="gb18030-requirements"></a>Requisiti GB18030  
 Configuration Manager soddisfa gli standard definiti in GB18030. È quindi possibile usare Configuration Manager in Cina. Una distribuzione di Configuration Manager deve disporre delle seguenti configurazioni per soddisfare i requisiti GB18030:  

-   Ogni computer del server di sito e ogni computer SQL Server in uso con Configuration Manager deve usare un sistema operativo in cinese.  

-   Ogni database del sito e ogni istanza di SQL Server nella gerarchia deve utilizzare le stesse regole di confronto e deve essere una delle seguenti opzioni:  

    -   Chinese_Simplified_Pinyin_100_CI_AI  

    -   Chinese_Simplified_Stroke_Order_100_CI_AI  

    > [!NOTE]  
    >  Queste regole di confronto di database rappresentano un'eccezione ai requisiti indicati in [Supporto per le versioni di SQL Server per Configuration Manager](../../../core/plan-design/configs/support-for-sql-server-versions.md).  

-   Il file denominato **GB18030.SMS** deve trovarsi nella cartella radice del volume di avvio di ogni computer server del sito presente nella gerarchia. Questo file non contiene dati e può essere un file di testo vuoto denominato in modo da soddisfare questo requisito.  
