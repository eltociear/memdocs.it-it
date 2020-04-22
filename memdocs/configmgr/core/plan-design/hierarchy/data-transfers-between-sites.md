---
title: Trasferimenti di dati tra siti
titleSuffix: Configuration Manager
description: Informazioni su come Configuration Manager sposta i dati tra i siti e come gestire il trasferimento dei dati in rete.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: dc526e8d-fac3-4bb5-b206-03ad29b0ae11
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 6b6d4eab77d0543f9001cef2c1e2b618ba3e4328
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703619"
---
# <a name="data-transfers-between-sites"></a>Trasferimenti di dati tra siti

*Si applica a: Configuration Manager (Current Branch)*

Configuration Manager usa la *replica basata su file* e la *replica di database* per il trasferimento di tipi di informazioni diversi tra i siti. Informazioni su come Configuration Manager sposta i dati tra i siti e come gestire il trasferimento dei dati in rete.  

## <a name="types-of-replication"></a>Tipi di replica

### <a name="file-based-replication"></a><a name="bkmk_fileroute" /> Replica basata su file

Configuration Manager usa la replica basata su file per trasferire i dati basati su file tra i siti all'interno della gerarchia. Questi dati includono le applicazioni e i pacchetti che si vuole distribuire ai punti di distribuzione nei siti figlio. Gestiscono anche record dei dati di individuazione non elaborati che il sito trasferisce al sito padre e quindi elabora.  

Per altre informazioni, vedere [Replica basata su file](file-based-replication.md).

### <a name="database-replication"></a><a name="bkmk_dbrep" /> Replica di database

La replica di database di Configuration Manager usa SQL Server per trasferire i dati. Usa questo metodo per unire le modifiche nel database del sito con le informazioni del database in altri siti della gerarchia.

Per altre informazioni, vedere [Replica di database](database-replication.md).

Per la risoluzione dei problemi di replica SQL. vedere [Risolvere i problemi di replica SQL](../../servers/manage/replication/overview.md).

## <a name="see-also"></a>Vedere anche

[Monitorare la replica](../../servers/manage/monitor-replication.md)
