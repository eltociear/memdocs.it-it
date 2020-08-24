---
title: Usare i supporti di avvio per distribuire Windows in rete
titleSuffix: Configuration Manager
description: Le distribuzioni dei supporti di avvio in Configuration Manager consentono di distribuire il sistema operativo all'avvio del computer di destinazione.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 999b5409-7e72-48d2-8554-4d44427ce383
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: db28c89e88ba08f92618c6d5fde1d1516b74afe4
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124757"
---
# <a name="use-bootable-media-to-deploy-windows-over-the-network-with-configuration-manager"></a>Usare i supporti di avvio per distribuire Windows in rete con Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

I supporti di avvio includono solo l'immagine di avvio e un puntatore alla sequenza di attività. Scaricano l'immagine del sistema operativo e altro contenuto a cui viene fatto riferimento dalla rete. Poiché i supporti di avvio non includono molto contenuto, è possibile aggiornare la sequenza di attività e gran parte del contenuto senza dover sostituire tali supporti.

Distribuire i sistemi operativi in rete con i supporti di avvio negli scenari seguenti:

- [Aggiornare un computer esistente con una nuova versione di Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

- [Installare una nuova versione di Windows in un nuovo computer (bare metal)](install-new-windows-version-new-computer-bare-metal.md)

- [Sostituire un computer esistente e trasferire le impostazioni](replace-an-existing-computer-and-transfer-settings.md)

Completare i passaggi in uno degli scenari di distribuzione dei sistemi operativi e quindi fare riferimento alle sezioni seguenti per usare i supporti di avvio per la distribuzione del sistema operativo.

## <a name="configure-deployment-settings"></a>Configurare le impostazioni di distribuzione

Quando si usano i supporti di avvio per avviare il processo di distribuzione dei sistemi operativi, configurare la distribuzione della sequenza di attività per rendere disponibile il sistema operativo per il supporto. Impostare questa opzione nella pagina **Impostazioni di distribuzione** della distribuzione. Per l'impostazione **Rendi disponibile per**, selezionare una delle opzioni seguenti:

- Client di Configuration Manager, supporti e PXE

- Solo supporti e PXE

- Solo supporti e PXE (nascosto)

Per altre informazioni, vedere [Deploy a task sequence](deploy-a-task-sequence.md).

## <a name="create-the-bootable-media"></a>Creare il supporto di avvio

Quando si crea un supporto di avvio, specificare se si tratta di un'unità flash USB o un set CD/DVD. Il computer in cui vengono avviati i supporti deve consentire l'opzione scelta come unità di avvio. Per altre informazioni, vedere [Creare supporti di avvio](create-bootable-media.md).

## <a name="install-the-os-from-bootable-media"></a><a name="BKMK_Deploy"></a> Installare il sistema operativo da un supporto di avvio

Per installare il sistema operativo, inserire il supporto di avvio e quindi accendere il computer.

## <a name="support-for-cloud-based-content"></a>Supporto per contenuto basato sul cloud

<!--6209223-->

A partire dalla versione 2006, il supporto di avvio può scaricare contenuto basato sul cloud. Ad esempio, può essere necessario inviare una chiave USB a un utente in un ufficio remoto per ricreare l'immagine del dispositivo. O si immagini un ufficio che ha un server PXE locale, ma si vuole che i dispositivi diano il più possibile la priorità ai servizi cloud. Anziché appesantire la rete WAN per scaricare contenuti di distribuzione del sistema operativo di grandi dimensioni, i supporti di avvio e le distribuzioni PXE possono ora ottenere contenuti da origini basate sul cloud, come ad esempio un gateway di gestione cloud (CMG) abilitato per la condivisione del contenuto.

> [!NOTE]
> Il dispositivo necessita tuttavia di una connessione Intranet al punto di gestione.

Durante l'esecuzione della sequenza di attività, il contenuto viene scaricato dalle origini basate sul cloud. Esaminare il file **smsts.log** nel client.

### <a name="prerequisites"></a>Prerequisiti

- Abilitare l'impostazione client seguente nel gruppo **Servizi cloud**: **Consentire accesso al punto di distribuzione cloud**. Assicurarsi che l'impostazione client sia distribuita nei client di destinazione. Per altre informazioni, vedere [Informazioni sulle impostazioni client - Servizi cloud](../../core/clients/deploy/about-client-settings.md#cloud-services).

- Per il gruppo di limiti in cui si trova il client:

  - Associare i sistemi CMG abilitati per il contenuto o del sito del punto di distribuzione cloud. Per altre informazioni, vedere [Configurare un gruppo di limiti](../../core/servers/deploy/configure/boundary-group-procedures.md#bkmk_config).

  - Abilitare l'opzione seguente: **Preferisci le origini basate sul cloud rispetto alle origini locali**. Per altre informazioni, vedere [Opzioni del gruppo di limiti per download peer](../../core/servers/deploy/configure/boundary-groups.md#bkmk_bgoptions).

- Distribuire il contenuto cui si fa riferimento nella sequenza di attività al servizio CMG abilitato per il contenuto o a un punto di distribuzione cloud.

## <a name="next-steps"></a>Passaggi successivi

[Esperienze utente per la distribuzione del sistema operativo](../understand/user-experience.md#task-sequence-wizard)
