---
title: Creare una sequenza di attività personalizzata
titleSuffix: Configuration Manager
description: Modificare una sequenza di attività personalizzata in Configuration Manager per aggiungere passaggi alla sequenza di attività.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: b9800a66-7541-47ca-8276-da8ef6cb6d1b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f390c3857ad5a277002839c4c14ab1307d9ab281
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125577"
---
# <a name="create-a-custom-task-sequence-with-configuration-manager"></a>Creare una sequenza di attività personalizzata con Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Quando si crea una sequenza di attività personalizzata in Configuration Manager, la sequenza di attività non contiene passaggi. Dopo averla creata, modificarla e aggiungere i passaggi della sequenza di attività necessari.  

## <a name="create-a-custom-task-sequence"></a><a name="BKMK_CustomTS"></a> Creare una sequenza di attività personalizzata

Seguire questa procedura per creare una sequenza di attività personalizzata:

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**, espandere **Sistemi operativi** e quindi selezionare il nodo **Sequenze di attività**.  

1. Nella scheda **Home** della barra multifunzione nel gruppo **Crea** selezionare **Crea sequenza di attività**. Questa azione avvia la Creazione guidata della sequenza di attività.  

1. Nella pagina **Crea una nuova sequenza di attività** selezionare **Crea una nuova sequenza di attività personalizzata**.  

1. Nella pagina **informazioni sequenza di attività** specificare:

    - Un nome per la sequenza di attività
    - Una descrizione della sequenza di attività
    - Un'immagine di avvio facoltativa per la sequenza di attività da usare

Dopo aver completato la Creazione guidata sequenza di attività, Configuration Manager aggiunge la sequenza di attività personalizzata al nodo **Sequenze di attività**. È ora possibile modificare questa sequenza di attività per aggiungere passaggi della sequenza di attività.  

## <a name="see-also"></a>Vedere anche

Per un elenco dei passaggi della sequenza di attività disponibili, vedere [Passaggi della sequenza di attività](../understand/task-sequence-steps.md).  

Per altre informazioni su come modificare una sequenza di attività, vedere [Usare l'editor delle sequenze di attività](../understand/task-sequence-editor.md).  

Le sequenze di attività vengono usate principalmente per automatizzare le attività di distribuzione del sistema operativo, ma è possibile creare una sequenza di attività personalizzata per automatizzare tipi di attività diversi. Per altre informazioni, vedere [Creare una sequenza di attività per distribuzioni non di sistema operativo](create-a-task-sequence-for-non-operating-system-deployments.md).

A partire dalla versione 2002, è possibile installare applicazioni complesse usando le sequenze di attività con il modello di applicazione. Aggiungere un tipo di distribuzione a un'app che è una sequenza di attività per installare o disinstallare l'app. Per altre informazioni, vedere [Creare applicazioni Windows](../../apps/get-started/creating-windows-applications.md#bkmk_tsdt).<!-- 3555953 -->

## <a name="next-steps"></a>Passaggi successivi

[Distribuire la sequenza di attività](deploy-a-task-sequence.md)
