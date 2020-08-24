---
title: Usare il multicast per distribuire Windows in rete
titleSuffix: Configuration Manager
description: È possibile usare il multicast nell'ambiente di Configuration Manager in modo che più computer possano scaricare simultaneamente l'immagine del sistema operativo.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 4cafb7fc-380b-41b1-b83e-045aebfb7131
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9f580467ccb26209ed20666733e30959bbf50128
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124706"
---
# <a name="use-multicast-to-deploy-windows-over-the-network-with-configuration-manager"></a>Usare il multicast per distribuire Windows in rete con Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Il multicast è un metodo di ottimizzazione della rete che è possibile usare quando è probabile che più client scarichino la stessa immagine del sistema operativo contemporaneamente. Quando si usa il multicast, più computer scaricano contemporaneamente l'immagine del sistema operativo, che viene trasmessa in multicast dal punto di distribuzione. Questo comportamento sostituisce il meccanismo in base al quale ogni client scarica una copia dell'immagine dal punto di distribuzione tramite una connessione separata.

Distribuire i sistemi operativi in rete usando il multicast negli scenari di distribuzione del sistema operativo seguenti:

- [Aggiornare un computer esistente con una nuova versione di Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

- [Installare una nuova versione di Windows in un nuovo computer (bare metal)](install-new-windows-version-new-computer-bare-metal.md)

Completare i passaggi in uno di questi scenari di distribuzione del sistema operativo. Usare quindi le sezioni seguenti per supportare il multicast.

## <a name="configure-distribution-points-for-multicast"></a><a name="BKMK_Configure"></a> Configurare i punti di distribuzione per il multicast

Per usare il multicast, configurare almeno un punto di distribuzione. Per altre informazioni, vedere [Installare e configurare i punti di distribuzione](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-multicast).

Per un elenco delle porte necessarie per supportare il multicast, vedere [Porte](../../core/plan-design/hierarchy/ports.md#BKMK_PortsClient-DP2).

## <a name="prepare-an-os-image-for-multicast"></a>Preparare un'immagine del sistema operativo per il multicast

Per supportare il multicast, è necessario configurare l'immagine del sistema operativo. Per altre informazioni, vedere [Preparare l'immagine del sistema operativo per le distribuzioni multicast](../get-started/manage-operating-system-images.md#BKMK_OSImageMulticast).

## <a name="deploy-the-task-sequence"></a><a name="BKMK_Deploy"></a> Distribuire la sequenza di attività

Distribuire il sistema operativo in una raccolta di destinazione. Per altre informazioni, vedere [Deploy a task sequence](deploy-a-task-sequence.md).

## <a name="next-steps"></a>Passaggi successivi

[Esperienze utente per la distribuzione del sistema operativo](../understand/user-experience.md)
