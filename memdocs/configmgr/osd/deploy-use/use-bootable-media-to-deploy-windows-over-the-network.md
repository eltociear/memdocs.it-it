---
title: Usare i supporti di avvio per distribuire Windows in rete
titleSuffix: Configuration Manager
description: Le distribuzioni dei supporti di avvio in Configuration Manager consentono di distribuire il sistema operativo all'avvio del computer di destinazione.
ms.date: 06/16/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 999b5409-7e72-48d2-8554-4d44427ce383
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 22a3219cdf0bb09061e57f34e52ca7a061f55a2f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709239"
---
# <a name="use-bootable-media-to-deploy-windows-over-the-network-with-configuration-manager"></a>Usare i supporti di avvio per distribuire Windows in rete con Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

È possibile distribuire il sistema operativo all'avvio del computer di destinazione usando una distribuzione dei supporti di avvio. Il supporto contiene un puntatore alla sequenza di attività, all'immagine del sistema operativo e ad altri contenuti richiesti dalla rete. All'avvio del computer di destinazione, il computer recupera gli elementi a cui fa riferimento il puntatore del mouse. Con il supporto di avvio senza contenuto, è possibile aggiornare la destinazione senza sostituirlo nel supporto.

È possibile distribuire i sistemi operativi in rete usando il multicast negli scenari di distribuzione del sistema operativo seguenti:

-   [Aggiornare un computer esistente con una nuova versione di Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

-   [Installare una nuova versione di Windows in un nuovo computer (bare metal)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Sostituire un computer esistente e trasferire le impostazioni](replace-an-existing-computer-and-transfer-settings.md)  

Completare i passaggi in uno degli scenari di distribuzione del sistema operativo e quindi fare riferimento alle sezioni seguenti per usare i supporti di avvio per distribuire il sistema operativo.  

## <a name="configure-deployment-settings"></a>Configurare le impostazioni di distribuzione  
Quando si usa un supporto di avvio per avviare il processo di distribuzione del sistema operativo, configurare la distribuzione per rendere disponibile il sistema operativo per il supporto. È possibile impostare questa opzione nella pagina **Impostazioni di distribuzione** della Distribuzione guidata del software o nella scheda **Impostazioni di distribuzione** nelle proprietà della distribuzione. Per l'impostazione **Rendi disponibile per** , configurare uno degli elementi seguenti:

-   Client di Configuration Manager, supporti e PXE

-   Solo supporti e PXE

-   Solo supporti e PXE (nascosto)

## <a name="create-the-bootable-media"></a>Creare il supporto di avvio
È possibile specificare se il supporto di avvio è un'unità flash USB o un set di CD/DVD. Il computer in cui vengono avviati i supporti deve consentire l'opzione scelta come unità di avvio. Per altre informazioni, vedere [Creare supporti di avvio](create-bootable-media.md).  

##  <a name="install-the-operating-system-from--bootable-media"></a><a name="BKMK_Deploy"></a> Installare il sistema operativo da supporti di avvio  
Inserire il supporto di avvio in un'unità di avvio del computer e quindi accendere il sistema per installare il sistema operativo.
