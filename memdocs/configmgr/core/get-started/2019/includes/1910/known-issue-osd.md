---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 10/17/2019
ms.openlocfilehash: 668db6aa10fbee0a078eef04f0560973e5ed9454
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697849"
---
### <a name="task-sequences-arent-available-to-pxe-or-media"></a><a name="ki_osd"></a> Le sequenze di attività non sono disponibili per PXE o supporti

<!--5578298-->
Se si distribuisce una sequenza di attività per PXE o supporti (USB o DVD), il client non riceve i criteri. Il messaggio seguente si trova in **smsts.log**:

`There are no task sequences available to this computer.`

#### <a name="workaround"></a>Soluzione alternativa

Avviare la sequenza di attività da Software Center.
