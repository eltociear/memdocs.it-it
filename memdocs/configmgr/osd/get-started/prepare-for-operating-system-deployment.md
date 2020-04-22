---
title: Preparare la distribuzione del sistema operativo
titleSuffix: Configuration Manager
description: Informazioni su come preparare le distribuzioni del sistema operativo in Configuration Manager
ms.date: 02/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 8d27e5ac-4f19-4b3d-85c7-fa34eb5d5e7e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bdd8cd61aedb06fe35a4ba268806f64cc18bf85d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708839"
---
# <a name="prepare-for-os-deployment-in-configuration-manager"></a>Preparare la distribuzione del sistema operativo in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Prima di poter distribuire i sistemi operativi è necessario eseguire alcune operazioni in Configuration Manager. Fare riferimento agli articoli seguenti per prepararsi per la distribuzione del sistema operativo:  

-   [Gestire le immagini di avvio](manage-boot-images.md)  

-   [Gestire le immagini del sistema operativo](manage-operating-system-images.md)  

-   [Gestire i pacchetti di aggiornamento del sistema operativo](manage-operating-system-upgrade-packages.md)  

-   [Gestire i driver](manage-drivers.md)  

-   [Gestire lo stato utente](manage-user-state.md)  

-   [Preparare le distribuzioni in computer sconosciuti](prepare-for-unknown-computer-deployments.md)  

-   [Associare gli utenti a un computer di destinazione](associate-users-with-a-destination-computer.md)  



### <a name="os-image-size"></a>Dimensioni delle immagini del sistema operativo  

Le immagini del sistema operativo hanno grandi dimensioni. Ad esempio, l'immagine per Windows 7 ha dimensioni minime di 3 gigabyte (GB). La dimensione dell'immagine e il numero di computer in cui viene distribuito contemporaneamente il sistema operativo influiscono sulle prestazioni di rete e sulla larghezza di banda disponibile. Assicurarsi di testare le prestazioni della rete. I test dell'impatto consentono di misurare meglio il potenziale effetto della distribuzione dell'immagine e il tempo necessario per completare la distribuzione. Le attività di Configuration Manager che influiscono sulle prestazioni di rete includono la distribuzione dell'immagine in un punto di distribuzione, la distribuzione dell'immagine da un sito a un altro e il download dell'immagine nel client.  

Assicurarsi inoltre di pianificare uno spazio di archiviazione su disco sufficiente nei punti di distribuzione che ospitano le immagini del sistema operativo.  

Per altre informazioni, vedere [Considerazioni aggiuntive sulla pianificazione per i punti di distribuzione](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_AdditionalPlanning).


### <a name="client-cache-size"></a>Dimensione della cache del client  

Quando i client di Configuration Manager scaricano i contenuti, usano automaticamente il Servizio trasferimento intelligente in background (BITS), se disponibile. Quando si distribuisce una sequenza di attività per l'installazione di un sistema operativo, è possibile impostare un'opzione di distribuzione che consente ai client di Configuration Manager di scaricare l'immagine completa in una cache locale prima dell'esecuzione della sequenza di attività.  

Quando un client di Configuration Manager deve scaricare un'immagine del sistema operativo, ma non c'è spazio sufficiente nella cache, il client può liberare spazio nella cache. Controlla gli altri pacchetti nella cache per stabilire se eliminando alcuni pacchetti meno recenti sarà possibile di liberare spazio su disco sufficiente per l'immagine. Se l'eliminazione dei pacchetti non libera spazio sufficiente, il client non scarica l'immagine e la distribuzione non riesce. Questo comportamento può verificarsi se nella cache è presente un pacchetto di grandi dimensioni configurato per essere mantenuto. Se l'eliminazione dei pacchetti libera spazio su disco sufficiente nella cache, il client li elimina e quindi scarica l'immagine nella cache.  

Le dimensioni della cache predefinita nei client di Configuration Manager potrebbero essere insufficienti per la maggior parte delle distribuzioni dell'immagine del sistema operativo. Se si intende scaricare l'immagine completa nella cache del client, regolare le dimensioni della cache del client nei computer di destinazione in modo che si adattino alle dimensioni dell'immagine oggetto della distribuzione.  

Per altre informazioni, vedere [Configurare la cache del client](../../core/clients/manage/manage-clients.md#BKMK_ClientCache).  


