---
title: Guida di riferimento tecnico per la risoluzione dei problemi di distribuzione delle applicazioni
titleSuffix: Configuration Manager
description: Riferimento tecnico per la risoluzione dei problemi di distribuzione delle applicazioni in Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: a4eb09c8-e570-4369-9adb-ded9c8ad3400
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5b3513131b73ac2b63cf18f31b1e39e15ee97420
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688869"
---
# <a name="technical-reference-for-application-deployment-in-configuration-manager"></a>Riferimento tecnico per la distribuzione delle applicazioni in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

In questo articolo si apprenderà come funzionano le distribuzioni dell'applicazione.

## <a name="before-you-begin"></a>Operazioni preliminari

Per risolvere i problemi relativi alle distribuzioni dell'applicazione, sono disponibili più elementi che possono essere utili per esaminare i registri del client. Questi elementi includono:

- ID CI applicazione
- ID applicazione univoco
- ID univoco del tipo di distribuzione
- ID univoco della distribuzione dell'applicazione (noto anche come ID assegnazione univoco)
- Scopo della distribuzione dell'applicazione
- ID contenuto univoco
- ID e nome raccolta
- Tipo di raccolta

Per semplificare la risoluzione dei problemi, è possibile eseguire una query SQL simile alla seguente nel database di Configuration Manager per ottenere le informazioni elencate in precedenza.

```sql
SELECT APP.CI_ID [App CI ID], APP.CI_UniqueID [App Unique ID], APP.DisplayName [App Name],
DT.CI_UniqueID [DT Unique ID], DT.ContentId [DT Content ID],
CIA.Assignment_UniqueID [Assignment ID], CIA.CollectionID, CIA.CollectionName,
CASE CIA.OfferTypeID WHEN 0 THEN 'Required' WHEN 2 THEN 'Available' WHEN 3 THEN 'Simulate' ELSE 'Unknown' END AS [Deployment Purpose],
CASE C.CollectionType WHEN 1 THEN 'User Collection' WHEN 2 THEN 'Device Collection' ELSE 'Unknown' END AS [Collection Type],
DT.Technology, DT.DisplayName [DT Name]
FROM fn_ListApplicationCIs(1033) APP
JOIN fn_ListDeploymentTypeCIs(1033) DT ON DT.AppModelName = APP.ModelName AND DT.IsLatest = 1
LEFT JOIN v_CIAssignmentToCI CIACI ON CIACI.CI_ID = APP.CI_ID
LEFT JOIN v_CIAssignment CIA ON CIACI.AssignmentID = CIA.AssignmentID
LEFT JOIN v_Collection C ON C.CollectionID = CIA.CollectionID
WHERE APP.IsLatest = 1 AND APP.DisplayName = 'Application Name' -- Replace Application Name
```

> [!IMPORTANT]
> Quando si esegue la query, è **necessario** usare il nome dell'applicazione elencato nella scheda Informazioni generali in Proprietà dell'applicazione anziché usare il nome dell'applicazione localizzata elencato nella scheda Software Center in Proprietà dell'applicazione.

## <a name="next-steps"></a>Passaggi successivi

- [Criteri di distribuzione delle applicazioni](deployment-policy-technical-reference.md)
