---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/30/2018
ms.openlocfilehash: 1b4fb4fb087639d1b3c3075339ce890a9c1dbbca
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708219"
---
Usare le definizioni seguenti per distinguere tra pilota e produzione:  

- **Pilota**: un subset di dispositivi da convalidare prima di procedere alla distribuzione in un set più ampio. Usare Desktop Analytics per contrassegnare i dispositivi come univoci per il set pilota. I dispositivi nel set pilota sono pronti per l'aggiornamento quando non sono presenti asset bloccanti. Un asset bloccante è contrassegnato come *critico* e *non idoneo* per l'aggiornamento.  

- **Production**: tutti gli altri dispositivi registrati in Desktop Analytics che non sono inclusi nel set pilota. I dispositivi di produzione sono pronti per l'aggiornamento quando tutti gli asset sono approvati. Desktop Analytics approva automaticamente tutti gli asset non critici.  

