---
title: Diagnostica e dati di utilizzo
titleSuffix: Configuration Manager
description: Informazioni sui dati di diagnostica e utilizzo raccolti da Configuration Manager.
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 88ac4e55-d47b-4c94-b9c3-704c6a48b845
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ffa50d2cfb3095eb136128c09b74e9ee6a4eb501
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82904408"
---
# <a name="diagnostics-and-usage-data-for-configuration-manager"></a>Dati di diagnostica e utilizzo per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Configuration Manager raccoglie dati di utilizzo e di diagnostica su se stesso che vengono usati da Microsoft per migliorare l'esperienza, la qualità e la sicurezza di installazione delle versioni future.  

I dati di utilizzo e di diagnostica sono abilitati per ogni gerarchia di Configuration Manager. Essi consistono in query di SQL Server eseguite su base settimanale in ogni sito primario e nel sito di amministrazione centrale. Quando la gerarchia usa un sito di amministrazione centrale, i siti primari figlio replicano i dati in tale sito. Nel sito di livello superiore della gerarchia, il [punto di connessione del servizio](../../servers/deploy/configure/about-the-service-connection-point.md) invia queste informazioni quando verifica la presenza di aggiornamenti. Se il punto di connessione del servizio è in modalità offline, le informazioni vengono trasferite tramite lo [strumento di connessione del servizio](../../servers/manage/use-the-service-connection-tool.md).

> [!NOTE]  
> Configuration Manager raccoglie i dati solo dal database di SQL Server del sito e non direttamente dai client o dai server del sito.  

Per altre informazioni, vedere l'[Informativa sulla privacy Microsoft](https://privacy.microsoft.com/privacystatement).  

> [!div class="nextstepaction"]
> [Come Microsoft usa i dati di diagnostica e di utilizzo](how-diagnostics-and-usage-data-is-used.md)
