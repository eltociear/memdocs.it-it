---
author: aczechowski
ms.author: aaroncz
ms.reviewer: acabello
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/30/2018
ms.openlocfilehash: 431c88b07889f7c80d2723425aaef2245c7f06bc
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268785"
---
Usare le definizioni seguenti per distinguere tra pilota e produzione:  

- **Pilota**: un subset di dispositivi da convalidare prima di procedere alla distribuzione in un set più ampio. Usare Desktop Analytics per contrassegnare i dispositivi come univoci per il set pilota. I dispositivi nel set pilota sono pronti per l'aggiornamento quando non sono presenti asset bloccanti. Un asset bloccante è contrassegnato come *critico* e *non idoneo* per l'aggiornamento.  

- **Production**: tutti gli altri dispositivi registrati in Desktop Analytics che non sono inclusi nel set pilota. I dispositivi di produzione sono pronti per l'aggiornamento quando tutti gli asset sono approvati. Desktop Analytics approva automaticamente tutti gli asset non critici.  
