---
title: Raccolta di dati di diagnostica
titleSuffix: Configuration Manager
description: Informazioni sulla modalità di raccolta dei dati di utilizzo e di diagnostica di Configuration Manager da parte di questo strumento.
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: becfa825-b19f-448c-ab82-bb929255e4ae
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ca40891c840e954f2828833c179f01bcbc6e7448
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688469"
---
# <a name="how-configuration-manager-collects-diagnostics-and-usage-data"></a>Come Configuration Manager raccoglie i dati di diagnostica e utilizzo

*Si applica a: Configuration Manager (Current Branch)*

Per raccogliere dati di diagnostica e di utilizzo per Configuration Manager, ogni sito primario esegue query di SQL Server su base settimanale. In una gerarchia a più siti, i dati vengono replicati nel sito di amministrazione centrale.  

Nel sito di livello superiore di una gerarchia, il punto di connessione del servizio invia queste informazioni quando verifica la presenza di aggiornamenti. La modalità del punto di connessione del servizio determina il modo in cui vengono trasferiti i dati:

- **Online**: una volta alla settimana, il punto di connessione del servizio invia automaticamente i dati di diagnostica e utilizzo al servizio cloud.

- **Offline**: i dati di diagnostica e di utilizzo possono essere trasferiti manualmente con lo [strumento di connessione del servizio](../../servers/manage/use-the-service-connection-tool.md).

Per altre informazioni, vedere [Informazioni sul punto di connessione del servizio](../../servers/deploy/configure/about-the-service-connection-point.md).

> [!div class="nextstepaction"]
> [Come visualizzare i dati di diagnostica e di utilizzo](view-diagnostics-and-usage-data.md)
