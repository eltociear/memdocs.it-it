---
title: Risolvere i problemi di replica SQL
titleSuffix: Configuration Manager
description: Usare questi diagrammi per semplificare la comprensione e la risoluzione dei problemi di replica SQL tra siti di Configuration Manager
ms.date: 02/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 71d7430e-c5aa-485b-8dc0-c80fd8f29f17
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 202a3360b5e04d66ada0d3b47ddd4638c2197167
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703989"
---
# <a name="troubleshoot-sql-replication"></a>Risolvere i problemi di replica SQL

In una gerarchia multisito Configuration Manager usa la replica SQL per trasferire i dati tra i siti. Per altre informazioni, vedere [Replica di database](../../../plan-design/hierarchy/database-replication.md).

Per comprendere meglio e risolvere i problemi di replica SQL, usare questi diagrammi.

- [Replica SQL](sql-replication.md)
- [Configurazione SQL](sql-configuration.md)
- [Prestazioni SQL](sql-performance.md)
- [Reinizializzazione della replica SQL (reinit)](sql-replication-reinit.md)
- [Reinizializzazione dei dati globali](global-data-reinit.md)
- [Reinizializzazione dei dati del sito](site-data-reinit.md)
- [Reinizializzazione del messaggio mancante](reinit-missing-message.md)

Questi diagrammi per la risoluzione dei problemi sono interconnessi. Usare il diagramma seguente per comprenderne le relazioni:

![Diagramma di panoramica del processo di risoluzione dei problemi di replica SQL](media/overview.png)

<!-- PNG used instead of SVG because of weird blankspace in the SVG. The SVG file exists in the same location. -->

Per altre informazioni, vedere la serie seguente di blog del supporto tecnico Microsoft:

- [ConfigMgr DRS Synchronization Internals](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-drs-synchronization-internals/ba-p/1154317) (Elementi interni della sincronizzazione di ConfigMgr DRS)
- [ConfigMgr 2012 Data Replication Service (DRS) Unleashed](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-data-replication-service-drs-unleashed/ba-p/339916) (ConfigMgr 2012 Data Replication Service (DRS) al massimo)
- [ConfigMgr 2012 DRS – Troubleshooting FAQs](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-drs-troubleshooting-faqs/ba-p/339934) (ConfigMgr 2012 DRS - Domande frequenti sulla risoluzione dei problemi)
- [ConfigMgr 2012 DRS Initialization Internals](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-drs-initialization-internals/ba-p/339948) (Elementi interni dell'inizializzazione di ConfigMgr 2012 DRS)
- [ConfigMgr 2012: DRS and SQL service broker certificate issues](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-drs-and-sql-service-broker-certificate-issues/ba-p/339910) (ConfigMgr 2012: DRS e problemi dei certificati SQL Service Broker)
