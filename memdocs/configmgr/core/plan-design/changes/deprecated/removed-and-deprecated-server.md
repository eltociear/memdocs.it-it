---
title: Elementi deprecati per i server del sito
titleSuffix: Configuration Manager
description: Informazioni su prodotti e sistemi operativi che Configuration Manager non supporta più per i server del sito.
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d53ac075-438b-41da-ab85-42f33982da0c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2b6f9dfae2eaa4e7fac4cc9b059b608de3c1386a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702569"
---
# <a name="removed-and-deprecated-for-configuration-manager-site-servers"></a>Elementi rimossi e deprecati per i server del sito di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Questo articolo descrive i prodotti e i sistemi operativi rimossi dal supporto per i server del sito di Configuration Manager o che verranno rimossi in un aggiornamento futuro (deprecati). Anticipa informazioni sulle future modifiche che potrebbero influire sull'uso di Configuration Manager.  

Queste informazioni possono cambiare in futuro. Potrebbero non includere tutte le funzionalità, i prodotti o i sistemi operativi deprecati.  

## <a name="server-os"></a>Sistema operativo server  

|Sistemi operativi|Primo annuncio riguardo agli elementi deprecati|Supporto rimosso|
|-|-|-|
|Windows Server 2008 R2 con SP1|10 luglio 2015| Versione 1702|
|Windows Server 2008 con SP2|10 luglio 2015|Versione 1511|

## <a name="sql-server"></a>SQL Server

|Versioni di SQL Server|Primo annuncio riguardo agli elementi deprecati|Supporto rimosso|
|-|-|-|
|SQL Server 2008 R2|10 luglio 2015|Versione 1702|
|SQL Server 2008|10 luglio 2015|Versione 1511|

Se è necessario aggiornare la versione di SQL Server, è consigliabile usare i metodi seguenti, dal più semplice al più complesso:

1. [Aggiornare SQL Server sul posto](../../../servers/manage/upgrade-on-premises-infrastructure.md#BKMK_SupConfigUpgradeDBSrv) (scelta consigliata).  

2. Installare una nuova versione di SQL Server in un nuovo computer. Quindi per fare in modo che il server del sito punti alla nuova versione di SQL server, [usare l'opzione di spostamento del database](../../../servers/manage/modify-your-infrastructure.md#bkmk_dbconfig) delle impostazioni di Configuration Manager.  

3. Usare le funzionalità di [backup e ripristino](../../../servers/manage/backup-and-recovery.md).  

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni, vedere gli articoli seguenti:

- [Elementi rimossi e deprecati](removed-and-deprecated.md)  

- [Ciclo di vita del supporto Microsoft](https://support.microsoft.com/lifecycle)  

- [Supporto per le versioni Current Branch di System Center Configuration Manager](../../../servers/manage/current-branch-versions-supported.md)  
