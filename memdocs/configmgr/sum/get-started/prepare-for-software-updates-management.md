---
title: Preparare la gestione degli aggiornamenti software
titleSuffix: Configuration Manager
description: Per preparare la gestione degli aggiornamenti, completare queste attività per visualizzare i dati di valutazione di conformità nella console di Configuration Manager.
ms.date: 10/06/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 01907900-e28b-4cd7-9479-42906416707b
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: ab22fdcacf7574884f7cfd21859cb4b1aeb8e23f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81699499"
---
# <a name="prepare-for-software-updates-management"></a>Preparare la gestione degli aggiornamenti software

*Si applica a: Configuration Manager (Current Branch)*

Prima che i dati di valutazione della conformità dell'aggiornamento software siano visualizzati nella console di Configuration Manager e prima di poter distribuire gli aggiornamenti software nei computer client, è necessario completare i passaggi seguenti.

## <a name="step-1-install-a-software-update-point"></a>Passaggio 1: Installare un punto di aggiornamento software  
Il punto di aggiornamento software è necessario nel sito di amministrazione centrale e nei siti primari autonomi per abilitare la valutazione della conformità degli aggiornamenti software e per distribuire gli aggiornamenti software ai client. Il punto di aggiornamento software è facoltativo nei siti secondari. Per informazioni dettagliate, vedere[Installare un punto di aggiornamento software](install-a-software-update-point.md)  

## <a name="step-2-synchronize-software-updates"></a>Passaggio 2: Sincronizzare gli aggiornamenti software
La sincronizzazione degli aggiornamenti software è il processo di recupero dei metadati degli aggiornamenti software che soddisfano i criteri configurati. Gli aggiornamenti software non vengono visualizzati nella console di Configuration Manager finché non verranno sincronizzati. Per informazioni dettagliate, vedere [Sincronizzare gli aggiornamenti software](synchronize-software-updates.md).   

## <a name="step-3-configure-classifications-and-products-to-synchronize"></a>Passaggio 3: configurare le classificazioni e i prodotti per la sincronizzazione
Eseguire questa configurazione nel sito di amministrazione centrale o nel sito primario autonomo. Dopo aver sincronizzato gli aggiornamenti software per la prima volta, Configuration Manager recupera un elenco aggiornato di classificazioni e prodotti. A questo punto, è possibile eseguire selezioni dalle nuove opzioni delle proprietà del componente punto di aggiornamento software. Dopo aver configurato le nuove classificazioni e i prodotti, ripetere il passaggio 2 per avviare la sincronizzazione degli aggiornamenti software per recuperare i metadati degli aggiornamenti software per i nuovi criteri. Per informazioni dettagliate, vedere [Configurare le classificazioni e i prodotti per la sincronizzazione](configure-classifications-and-products.md).

## <a name="step-4-manage-settings-for-software-updates"></a>Passaggio 4: Gestire le impostazioni per gli aggiornamenti software
Dopo aver sincronizzato gli aggiornamenti software, verificare le impostazioni client di Configuration Manager, le configurazioni dei criteri di gruppo e le impostazioni degli aggiornamenti software prima di distribuirle. Per informazioni dettagliate, vedere [Gestire le impostazioni per gli aggiornamenti software](manage-settings-for-software-updates.md).
