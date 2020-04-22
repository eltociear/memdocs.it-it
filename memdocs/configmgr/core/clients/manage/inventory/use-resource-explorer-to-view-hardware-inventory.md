---
title: Come usare Esplora inventario risorse
titleSuffix: Configuration Manager
description: Usare Esplora inventario risorse per visualizzare l'inventario hardware in Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 375912f5-436d-4315-bdbe-d77afee6c9f3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: daa673169825638474fea05156fd837acbf0ba98
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690099"
---
# <a name="how-to-use-resource-explorer-to-view-hardware-inventory-in-configuration-manager"></a>Come usare Esplora inventario risorse per visualizzare l'inventario hardware in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Usare Esplora inventario risorse in Configuration Manager per visualizzare le informazioni relative all'inventario hardware. Il sito raccoglie le informazioni dai client nella gerarchia.  

> [!Tip]  
>  Esplora inventario risorse non visualizzerà alcun inventario dati fino a quando non viene eseguito un ciclo di inventario hardware nel client a cui ci si connette.  



## <a name="overview"></a>Panoramica

Esplora inventario risorse contiene le sezioni seguenti relative all'inventario hardware:  

- **Hardware**: illustra l'inventario hardware più recente raccolto dal dispositivo client specificato.  

    - Il nodo **Stato workstation** mostra l'ora e la data dell'ultimo inventario hardware dal dispositivo.  

- **Cronologia hardware**: contiene una cronologia degli elementi inclusi nell'inventario che sono stati modificati dall'ultima esecuzione del ciclo dell'inventario hardware.  

    - Espandere un elemento per visualizzare un nodo **Corrente** e uno o più nodi con la data cronologica. Confrontare le informazioni nel nodo corrente con uno dei nodi cronologici per individuare gli elementi modificati.  

> [!NOTE]  
> Per impostazione predefinita, Configuration Manager elimina i dati di inventario hardware che sono rimasti inattivi per 90 giorni. Regolare il numero di giorni nell'attività di manutenzione del sito **Elimina cronologia inventario obsoleta**. Per ulteriori informazioni, vedere [Attività di manutenzione](../../../servers/manage/maintenance-tasks.md).  



## <a name="how-to-open-resource-explorer"></a><a name="bkmk_open"></a> Come aprire Esplora inventario risorse   

1.  Nella console di Configuration Manager passare all'area di lavoro **Asset e conformità** e selezionare il nodo **Dispositivi**. In alternativa, selezionare una raccolta nel nodo **Raccolte dispositivi**.  

2.  Selezionare un dispositivo. Nella scheda **Home** e nel gruppo **Dispositivi** della barra multifunzione, fare clic su **Avvia** e quindi selezionare **Esplora inventario risorse**.   

> [!Tip]  
> In Esplora inventario risorse fare clic con il pulsante destro del mouse su un elemento nel riquadro dei risultati a destra per visualizzare altre azioni. Scegliere **Proprietà** per visualizzare l'elemento in un formato diverso.  



## <a name="use-of-large-integer-values"></a><a name="bkmk_bigint"></a> Utilizzo di valori interi di grandi dimensioni
<!--1357880-->
Nelle versioni di Configuration Manager 1802 e precedenti, l'inventario hardware prevede un limite per i valori interi maggiori di 4.294.967.296 (2^32). Questo limite può essere raggiunto per attributi come le dimensioni delle unità disco rigido in byte. Il punto di gestione non elabora valori interi oltre questo limite, quindi nessun valore viene archiviato nel database. 

A partire dalla versione 1806, il limite è stato aumentato a 18.446.744.073.709.551.616 (2^64). 

Per una proprietà con un valore che non cambia, ad esempio le dimensioni totali del disco, il valore potrebbe non essere immediatamente visibile dopo l'aggiornamento del sito. La maggior parte dell'inventario hardware è un report delta. Il client invia solo valori che cambiano. Per risolvere questo problema, aggiungere un'altra proprietà alla stessa classe. Con questa azione, il client aggiorna tutte le proprietà nella classe modificata. 



## <a name="see-also"></a>Vedere anche

Per informazioni su come visualizzare l'inventario hardware dai client che eseguono Linux e UNIX, vedere [Come monitorare i client per i server Linux e UNIX](../monitor-clients-for-linux-and-unix-servers.md).  

Esplora inventario risorse mostra anche l'inventario software. Per altre informazioni, vedere [Come usare Esplora inventario risorse per visualizzare l'inventario software](use-resource-explorer-to-view-software-inventory.md).
