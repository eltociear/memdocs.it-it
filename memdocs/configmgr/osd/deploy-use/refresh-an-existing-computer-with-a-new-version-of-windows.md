---
title: Aggiornare il sistema operativo di un computer esistente
titleSuffix: Configuration Manager
description: È possibile usare vari metodi in Configuration Manager per eseguire partizioni e formattare un computer esistente e installare un nuovo sistema operativo nel computer.
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b189a346-8c0d-4870-a876-0719fbb0ab04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9582d6840e1f750d53504da4e8e7f6bf54f44965
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708409"
---
# <a name="refresh-an-existing-computer-with-a-new-version-of-windows"></a>Aggiornare un computer esistente con una nuova versione di Windows

*Si applica a: Configuration Manager (Current Branch)*

Usare Configuration Manager per eseguire partizioni e formattare un computer esistente e quindi installare un nuovo sistema operativo. Questo processo viene talvolta chiamato *ricreazione dell'immagine* o *cancellazione e caricamento*. Per questo scenario, scegliere tra i numerosi e diversi metodi di distribuzione disponibili, ad esempio PXE, supporti di avvio o Software Center. È anche possibile usare un punto di migrazione stato per archiviare le impostazioni e quindi ripristinarle nel nuovo sistema operativo.

Per scegliere lo scenario di distribuzione del sistema operativo corretto, vedere [Scenari di distribuzione di sistemi operativi aziendali](scenarios-to-deploy-enterprise-operating-systems.md).  

## <a name="plan"></a><a name="BKMK_Plan"></a> Pianificazione  

### <a name="plan-for-and-implement-infrastructure-requirements"></a>Pianificare e implementare i requisiti di infrastruttura

Per poter distribuire un sistema operativo è necessario stabilire diversi requisiti di infrastruttura. Alcuni di questi requisiti includono Windows ADK, l'Utilità di migrazione stato utente (USMT) e i Servizi di distribuzione Windows (WDS). Per altre informazioni, vedere [Requisiti dell'infrastruttura per la distribuzione del sistema operativo](../plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

### <a name="install-a-state-migration-point"></a>Installare un punto di migrazione stato

Se si vogliono acquisire le impostazioni da un computer esistente e quindi di ripristinarle nel nuovo sistema operativo, considerare la possibilità di usare un punto di migrazione stato. Per altre informazioni, vedere [Punto di migrazione dello stato](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints).  

## <a name="configure"></a><a name="BKMK_Configure"></a> Configura  

### <a name="prepare-a-boot-image"></a>Preparare un'immagine d'avvio

Le immagini d'avvio consentono di avviare un computer in un ambiente Windows PE. Windows PE è un sistema operativo di base con servizi e componenti limitati. Da Windows PE Configuration Manager può installare un sistema operativo Windows completo nel computer.

Per altre informazioni, vedere gli articoli seguenti:

- [Gestire le immagini di avvio](../get-started/manage-boot-images.md)

- [Personalizzare le immagini di avvio](../get-started/customize-boot-images.md)

- [Distribuire il contenuto](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)

### <a name="prepare-an-os-image"></a>Preparare un'immagine del sistema operativo

L'immagine del sistema operativo contiene i file necessari per installare il sistema operativo nel computer di destinazione.

Per altre informazioni, vedere gli articoli seguenti:

- [Gestire le immagini del sistema operativo](../get-started/manage-operating-system-images.md)

- [Distribuire il contenuto](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)

### <a name="create-a-task-sequence-to-deploy-an-os"></a>Creare una sequenza di attività per distribuire un sistema operativo

Usare una sequenza di attività per automatizzare l'installazione del sistema operativo. A seconda del metodo di distribuzione scelto, potrebbero essere necessarie considerazioni aggiuntive per la sequenza di attività.

Per altre informazioni, vedere gli articoli seguenti:

- [Creare una sequenza di attività per installare un sistema operativo](create-a-task-sequence-to-install-an-operating-system.md)

- [Gestire lo stato utente](../get-started/manage-user-state.md)

## <a name="deploy"></a><a name="BKMK_Deploy"></a> Distribuisci

- Per distribuire il sistema operativo, usare uno dei metodi di distribuzione seguenti:  

  - [Usare PXE per distribuire Windows in rete](use-pxe-to-deploy-windows-over-the-network.md)  

  - [Usare il multicast per distribuire Windows in rete](use-multicast-to-deploy-windows-over-the-network.md)  

  - [Creare un'immagine per un OEM presso un produttore computer o un deposito locale](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

  - [Use stand-alone media to deploy Windows without using the network](use-stand-alone-media-to-deploy-windows-without-using-the-network.md) (Usare i supporti autonomi per distribuire Windows senza usare la rete)  

  - [Usare i supporti di avvio per distribuire Windows in rete](use-bootable-media-to-deploy-windows-over-the-network.md)  

  - [Use Software Center to deploy Windows over the network](use-software-center-to-deploy-windows-over-the-network.md) (Usare Software Center per distribuire Windows tramite la rete)  

## <a name="monitor"></a>Monitoraggio  

Per altre informazioni, vedere [Monitorare le distribuzioni del sistema operativo](monitor-operating-system-deployments.md).  

> [!Note]
> Quando si ricrea l'immagine di un dispositivo UEFI, Windows Boot Manager crea una nuova voce nel caricatore di avvio. Questo comportamento è più evidente quando si ricrea ripetutamente l'immagine di un dispositivo, ad esempio in un ambiente di test o in un lab per studenti. Questo in genere non influisce sulle prestazioni o sull'utilizzo del dispositivo. Se l'elenco diventa troppo grande, è possibile che in alcuni dispositivi hardware specifici si verifichino problemi funzionali. Ad esempio, non viene eseguito l'avvio in un'unità USB esterna oppure non è possibile selezionare la voce di avvio corrente dall'elenco. Usare il comando Windows **bcdedit** per cancellare le voci di avvio inutilizzate. Per altre informazioni, vedere [BCDEdit/deletevalue](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--deletevalue).<!-- 2841926 -->
