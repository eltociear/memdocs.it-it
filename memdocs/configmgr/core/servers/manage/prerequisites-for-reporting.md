---
title: Prerequisiti per la creazione di report
titleSuffix: Configuration Manager
description: Individuare le diverse dipendenze che influiscono sull'uso della creazione di report in Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9cc508a5-5023-4833-b776-ae9a6971138f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e08833a5ef560a0f958fe68b4ade0d4717dffc73
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703519"
---
# <a name="prerequisites-for-reporting-in-configuration-manager"></a>Prerequisiti per la creazione di report in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

La creazione di report in Configuration Manager ha le dipendenze seguenti:

- SQL Server Reporting Services
- Punto di Reporting Services
- Server di report di Power BI (facoltativo, a partire dalla versione 2002)

## <a name="sql-server-reporting-services"></a>SQL Server Reporting Services

Prima di poter usare la creazione di report in Configuration Manager è necessario installare e configurare SQL Server Reporting Services.

Per altre informazioni sulla pianificazione e la distribuzione di Reporting Services, vedere [Installare SQL Server Reporting Services](https://docs.microsoft.com/sql/reporting-services/install-windows/install-reporting-services).

Installare il database di Reporting Services nell'istanza predefinita o in un'istanza denominata di un'installazione di SQL Server a 64 bit. Collocare l'istanza di SQL Server in un percorso condiviso con il server del sistema del sito oppure configurarla in un computer remoto.

Configuration Manager supporta per la creazione di report le stesse versioni di SQL Server supportate per il database del sito. Per altre informazioni, vedere [Versioni di SQL Server supportate](../../plan-design/configs/support-for-sql-server-versions.md#bkmk_SQLVersions).

## <a name="reporting-services-point"></a>Punto di Reporting Services

Prima di poter usare la creazione di report in Configuration Manager, occorre configurare il ruolo di sistema del sito del punto di Reporting Services.

Per altre informazioni, vedere [Prerequisiti del sito e del sistema del sito](../../plan-design/configs/site-and-site-system-prerequisites.md#bkmk_2012RSpoint).

## <a name="power-bi-report-server"></a>Server di report di Power BI

A partire dalla versione 2002, è possibile integrare la creazione di report con il server di report di Power BI. Per altre informazioni, inclusi i prerequisiti, vedere [Integrare il server di report di Power BI](powerbi-report-server.md).

## <a name="next-steps"></a>Passaggi successivi

[Configurare la creazione di report](configuring-reporting.md)
