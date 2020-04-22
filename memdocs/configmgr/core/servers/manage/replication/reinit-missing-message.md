---
title: Reinizializzazione del messaggio mancante
titleSuffix: Configuration Manager
description: Usare questo diagramma per avviare la risoluzione dei problemi relativi a un messaggio mancante con la reinizializzazione della replica SQL in Configuration Manager
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 39a3001e-2df5-4b36-bd83-4f1d21dda335
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1e640c3dd756d96a58e8b54d6056d2adbb7bb99c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703979"
---
# <a name="reinit-missing-message"></a>Reinizializzazione del messaggio mancante

In una gerarchia multisito Configuration Manager usa la replica SQL per trasferire i dati tra i siti. Per altre informazioni, vedere [Replica di database](../../../plan-design/hierarchy/database-replication.md).

Usare il diagramma seguente per avviare la risoluzione dei problemi relativi a un messaggio mancante con la reinizializzazione della replica SQL:

![Diagramma per risolvere i problemi relativi a un messaggio mancante con la reinizializzazione](media/reinit-missing-message.svg)

## <a name="queries"></a>Query

Questo diagramma usa le query seguenti:

### <a name="check-if-site-replication-hasnt-finished-reinit"></a>Controllare se la replica del sito non ha terminato la reinizializzazione

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
```

### <a name="get-the-trackingguid--status-from-subscriber-site"></a>Ottenere il GUID di traccia e lo stato dal sito del sottoscrittore

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
```

### <a name="get-the-trackingguid--status-from-the-publishing-site"></a>Ottenere il GUID di traccia e lo stato dal sito di pubblicazione

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
WHERE RequestTrackingGUID=@trackingGuid
```

## <a name="remediation-actions"></a>Azioni di correzione

### <a name="version-1902-and-later"></a>Versione 1902 e successive

Per rilevare il problema ed effettuare la reinizializzazione, eseguire [Replication Link Analyzer](../monitor-replication.md#BKMK_RLA).

### <a name="version-1810-and-earlier"></a>Versione 1810 e precedenti

Eseguire la query SQL seguente per ottenere `ReplicationGroupID`:

```sql
SELECT rd.ID AS ReplicationGroupID from ReplicationData rd
INNER JOIN RCM_DrsInitializationTracking it ON rd.ReplicationGroup = it.ReplicationGroup
WHERE it.RequestTrackingGUID=@trackingGuid
```

Usare quindi il metodo `InitializeData` sulla classe WMI `SMS_ReplicationGroup` con i valori seguenti:

- ReplicationGroupID: dalla query SQL precedente
- SiteCode1: sito padre
- SiteCode2: sito figlio

Per altre informazioni, vedere [Metodo InitializeData nella classe SMS_ReplicationGroup](../../../../develop/reference/core/servers/configure/initializedata-method-in-class-sms_replicationgroup.md).

#### <a name="example"></a>Esempio

```PowerShell
Invoke-WmiMethod –Namespace "root\sms\site_CAS" -Class SMS_ReplicationGroup –Name InitializeData -ArgumentList "20", "CAS", "PR1"
```

## <a name="next-steps"></a>Passaggi successivi

- [Reinizializzazione della replica SQL (reinit)](sql-replication-reinit.md)
