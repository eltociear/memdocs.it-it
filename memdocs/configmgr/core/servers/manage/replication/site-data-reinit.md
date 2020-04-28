---
title: Reinizializzazione dei dati del sito
titleSuffix: Configuration Manager
description: Usare questo diagramma per avviare la risoluzione dei problemi di reinizializzazione della replica SQL per i dati del sito in una gerarchia di Configuration Manager
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 19741d45-2d42-438e-a9f3-15bb365d63ca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6a336bdf323fbb81a16082e9c308577763a7c104
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078592"
---
# <a name="troubleshoot-site-data-reinit"></a>Risolvere i problemi di reinizializzazione dei dati del sito

In una gerarchia multisito Configuration Manager usa la replica SQL per trasferire i dati tra i siti. Per altre informazioni, vedere [Replica di database](../../../plan-design/hierarchy/database-replication.md).

Usare il diagramma seguente per avviare la risoluzione dei problemi di reinizializzazione della replica SQL per i dati del sito in una gerarchia di Configuration Manager:

![Diagramma per la risoluzione dei problemi di reinizializzazione dei dati del sito](media/site-data-reinit.svg)

## <a name="queries"></a>Query

Questo diagramma usa le query seguenti:

### <a name="check-if-site-replication-hasnt-finished-reinit"></a>Controllare se la replica del sito non ha terminato la reinizializzazione

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N`Site'
```

### <a name="get-the-trackingguid--status-from-the-cas"></a>Ottenere il GUID di traccia e lo stato dal sito CAS

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N'Site'
```

### <a name="get-the-trackingguid--status-from-the-primary-site"></a>Ottenere il GUID di traccia e lo stato dal sito primario

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
WHERE RequestTrackingGUID=@trackingGuid
```

### <a name="check-primary-site-isnt-in-maintenance-mode"></a>Controllare che il sito primario non sia in modalità di manutenzione

```sql
SELECT * FROM ServerData
WHERE SiteStatus = 125
AND SiteCode=dbo.fnGetSiteCode()
AND ServerRole=N'Peer'
```

### <a name="check-request-status-for-the-tracking-id"></a>Controllare lo stato della richiesta per l'ID di traccia

```sql
SELECT Status FROM RCM_InitPackageRequest
WHERE RequestTrackingGUID=@trackGuid
```

## <a name="next-steps"></a>Passaggi successivi

- [Reinizializzazione del messaggio mancante](reinit-missing-message.md)
- [Reinizializzazione dei dati globali](global-data-reinit.md)
