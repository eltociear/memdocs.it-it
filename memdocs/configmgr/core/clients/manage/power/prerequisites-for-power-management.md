---
title: Prerequisiti per il risparmio energia
titleSuffix: Configuration Manager
description: Informazioni sui prerequisiti per il risparmio energia in Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 9c062f13-3c1f-4621-9cae-de0e322aa03f
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: a816d333d96dba6cb1c38f6499ccac78e2db8a3c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696519"
---
# <a name="prerequisites-for-power-management-in-configuration-manager"></a>Prerequisiti per il risparmio energia in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Il risparmio energia in Configuration Manager ha dipendenze esterne e dipendenze nel prodotto.  

## <a name="dependencies-external-to-configuration-manager"></a>Dipendenze esterne a Configuration Manager  
 La tabella seguente elenca le dipendenze esterne a Configuration Manager per il risparmio energia.  

|Dipendenza|Altre informazioni|  
|----------------|----------------------|  
|I computer client devono essere in grado di supportare gli stati necessari relativi al risparmio energia|Per usare tutte le funzionalità di risparmio energia, i computer client devono essere in grado di supportare le azioni sospensione, ibernazione, riattivazione dallo stato di sospensione e riattivazione dallo stato di ibernazione. È possibile usare il report **Funzionalità alimentazione** per determinare se i computer supportano queste azioni. Per altre informazioni, vedere [Report Funzionalità alimentazione](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md#BKMK_Capabilites) nell'argomento [Come monitorare e pianificare il risparmio energia](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).|  

## <a name="configuration-manager-dependencies"></a>Dipendenze di Configuration Manager  
 La tabella seguente elenca le dipendenze interne di Configuration Manager per il risparmio energia.  

|Dipendenza|Altre informazioni|  
|----------------|----------------------|  
|Il risparmio energia deve essere abilitato prima di poter creare e monitorare le combinazioni per il risparmio di energia.|Per informazioni su come abilitare e configurare il risparmio energia, vedere [Configurazione del risparmio energia](../../../../core/clients/manage/power/configuring-power-management.md).|  
|Punto di Reporting Services|Prima di poter visualizzare i report di risparmio energia, è necessario configurare un punto di Reporting Services. Per altre informazioni, vedere [Introduzione ai report](../../../servers/manage/introduction-to-reporting.md).|  
