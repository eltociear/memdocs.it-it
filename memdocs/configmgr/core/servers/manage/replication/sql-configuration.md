---
title: Configurazione SQL
titleSuffix: Configuration Manager
description: Usare questo diagramma per avviare la risoluzione dei problemi di configurazione SQL per Configuration Manager
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 95ab8cbd-0807-4422-823a-f5f9314ba623
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b909d992dc16b6e786c62143347ed420d913dbc5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707619"
---
# <a name="sql-configuration"></a>Configurazione SQL

In una gerarchia multisito Configuration Manager usa la replica SQL per trasferire i dati tra i siti. Per altre informazioni, vedere [Replica di database](../../../plan-design/hierarchy/database-replication.md).

Usare il diagramma seguente per avviare la risoluzione dei problemi di configurazione SQL relativa a SQL Service Broker:

![Diagramma per la risoluzione dei problemi di configurazione SQL](media/sql-configuration.svg)

## <a name="queries"></a>Query

Il diagramma include le query e le azioni seguenti:

### <a name="check-if-sql-can-deliver-ssb-messages"></a>Controllare se SQL riesce a recapitare messaggi SSB

```sql
SELECT transmission_status, *
FROM sys.transmission_queue
ORDER BY enqueue_time DESC
```

## <a name="remediation-actions"></a>Azioni di correzione

### <a name="remediate-the-issues-reported-from-transmission_status"></a>Correggere i problemi segnalati da transmission_status

Problemi comuni:

- Configurazione del firewall
- Configurazione di rete
- Certificato SSB non configurato correttamente

### <a name="run-sql-profiler-to-trace-ssb-events"></a>Eseguire SQL Profiler per tracciare gli eventi SSB

Eseguire SQL Profiler nel database del sito primario e del sito CAS per tracciare gli eventi correlati a SQL Service Broker:

- **Controllare il login di Service Broker**
- **Controllare la conversazione di Service Broker**
- Eventi nella categoria **Broker**
