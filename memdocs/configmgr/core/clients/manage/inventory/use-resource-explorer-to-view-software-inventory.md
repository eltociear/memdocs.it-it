---
title: Visualizzare l'inventario software con Esplora inventario risorse
titleSuffix: Configuration Manager
description: Usare Esplora risorse per visualizzare l'inventario software in Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4b7aa5f6-5ebd-49be-b7f3-4206caadc187
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 08905a72b6af6e9eae4d2cef9f4732ef692dc134
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690069"
---
# <a name="how-to-use-resource-explorer-to-view-software-inventory-in-configuration-manager"></a>Come usare Esplora risorse per visualizzare l'inventario software in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

È possibile usare Esplora inventario risorse in Configuration Manager per visualizzare informazioni relative all'inventario software raccolto dai computer nella gerarchia.  

> [!NOTE]  
>  Esplora inventario risorse non visualizzerà dati di inventario fino al completamento dell'esecuzione di un ciclo di inventario software nel client.  

 Esplora inventario risorse fornisce le informazioni di inventario software seguenti:  

-   **Software**:  

    -   **File raccolti**: file raccolti durante l'inventario software.  

    -   **Dettagli file**: file di cui è stato eseguito l'inventario durante l'inventario software, che non sono associati a uno specifico prodotto o il produttore.  

    -   **Ultima analisi software**: data e ora dell'ultimo inventario software e dell'ultima raccolta dei file per il computer client.  

    -   **Dettagli prodotto**: prodotti software inclusi nell'inventario software, raggruppati in base al produttore.  

## <a name="to-run-resource-explorer-from-the-configuration-manager-console"></a>Per eseguire Esplora inventario risorse dalla console di Configuration Manager  

1.  Nella console di Configuration Manager scegliere **Asset e conformità**.

2.  Nell'area di lavoro **Asset e conformità** scegliere **Dispositivi** oppure aprire eventuali raccolte che visualizzano dispositivi.  

3.  Scegliere il computer che contiene l'inventario da visualizzare e quindi nel gruppo **Dispositivi** della scheda **Home** scegliere **Avvia** > **Esplora inventario risorse**.

4.  È possibile fare clic con il pulsante destro del mouse su qualsiasi elemento nel riquadro di destra della finestra Esplora inventario risorse e quindi scegliere **Proprietà** per visualizzare le informazioni di inventario raccolte in un formato più leggibile.  
 
## <a name="view-and-manage-collected-diagnostic-files"></a><a name="bkmk_diag"> </a> Visualizzare e gestire i file di diagnostica raccolti

A partire da Configuration Manager versione 2002, usare Esplora inventario risorse per visualizzare e gestire i file raccolti quando si usa la notifica client per [raccogliere i log del client](../client-notification.md#client-diagnostics). 

1. Dal nodo **Dispositivi** fare clic con il pulsante destro del mouse sul dispositivo per il quale si vogliono visualizzare i log.
1. Scegliere **Avvia** e quindi **Esplora inventario risorse**.
1. In **Esplora inventario risorse** fare clic su **File di diagnostica**.
1. Nell'elenco **File di diagnostica** è possibile visualizzare la data di raccolta dei file. Il formato del nome dei log del client è `Support_<guid>.zip`.
1. Fare clic con il pulsante destro del mouse sul file ZIP e scegliere una delle opzioni seguenti:
    - **Apri il Supporto tecnico**: avvia il [Supporto tecnico](../../../support/support-center.md).
    - **Copia**: copia le informazioni sulle righe da Esplora inventario risorse.
    - **Visualizza file**: apre la cartella in cui si trova il file ZIP con Esplora file.
    - **Salva**: apre una finestra di dialogo Salva file per il file selezionato.
    - **Esporta**: salva le colonne di Esplora inventario risorse visualizzate in **File di diagnostica**.
    - **Aggiornare**: aggiorna l'elenco dei file.
    - **Proprietà**: restituisce le proprietà del file selezionato. 

[![Esaminare e salvare i log del client da Esplora inventario risorse](./../media/4226618-view-collected-client-logs.png)](./../media/4226618-view-collected-client-logs.png#lightbox)

## <a name="next-steps"></a>Passaggi successivi

[Usare Support Center](../../../support/support-center.md) per visualizzare i file di diagnostica raccolti.
