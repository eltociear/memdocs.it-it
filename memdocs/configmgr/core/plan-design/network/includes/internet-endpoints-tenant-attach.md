---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: include
ms.date: 08/11/2020
ms.openlocfilehash: 27436e7cd782ca910049007d52f37e2d7945f01e
ms.sourcegitcommit: e533cdf8722156a66b1cc46f710def96587345d0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/15/2020
ms.locfileid: "90606515"
---
- `https://aka.ms/configmgrgateway`

- `https://*.manage.microsoft.com` <!--7424742-->

- `https://dc.services.visualstudio.com` <!--7541816-->

Il punto di connessione del servizio crea una connessione in uscita di lunga durata al servizio di notifica ospitato in `https://*.manage.microsoft.com`. Verificare che il proxy usato per il punto di connessione del servizio non applichi troppo rapidamente il timeout delle connessioni in uscita. Il tempo consigliato per le connessioni in uscita a questo endpoint Internet è 3 minuti. <!--7820969-->