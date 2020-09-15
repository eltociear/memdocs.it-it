---
title: Dashboard dei dispositivi Surface
titleSuffix: Configuration Manager
description: Esaminare le informazioni relative ai dispositivi Surface tramite il dashboard.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 06/09/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 7397fc17-3ae8-4525-8386-aea8a9cffa06
ms.openlocfilehash: cbea7d7e126b120145533b7cf19822b54b3cb701
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/09/2020
ms.locfileid: "89607966"
---
# <a name="surface-device-dashboard-in-configuration-manager"></a>Dashboard dei dispositivi Surface in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

A partire dalla versione 1802, il dashboard dei dispositivi Surface visualizza informazioni a colpo d'occhio sui dispositivi Surface rilevati nell'ambiente in uso. <!--1355788-->

## <a name="open-the-surface-device-dashboard"></a>Aprire il dashboard dei dispositivi Surface

Per aprire il dashboard dei dispositivi Surface, procedere come segue: 

1. Aprire la console di Configuration Manager. 
2. Fare clic sul nodo **Monitoraggio**. 
3. Per caricare il dashboard, fare clic su **Dispositivi Surface**.

**Dashboard dei dispositivi Surface**
![Dashboard dei dispositivi Surface](media/Surface-device-dashboard.PNG)



## <a name="reviewing-information-in-the-surface-device-dashboard"></a>Esaminare le informazioni nel dashboard dei dispositivi Surface

Il dashboard dei dispositivi Surface visualizza tre grafici per l'ambiente in uso. 

- **Percentuale di dispositivi Surface**: visualizza la percentuale di dispositivi Surface presenti in tutto l'ambiente.

    ![Grafico Percentuale di dispositivi Surface](media/Percent-Surface-Devices.PNG)
- **Modelli di dispositivi Surface**: visualizza il numero di dispositivi per modello di Surface. 
  - Se si passa il mouse su una sezione del grafico, viene visualizzata la percentuale dei dispositivi Surface del modello selezionato. 

       ![Grafico dei modelli di dispositivi Surface](media/Surface-Models-Hover.PNG)
  - Se si fa clic su una sezione del grafico si passa all'elenco dei dispositivi per il modello corrispondente. 
      ![Elenco dei dispositivi per un modello di dispositivo Surface](media/Surface-Model-Device-List.PNG)

- **Prime cinque versioni di firmware**: visualizza un grafico con i primi cinque modelli di firmware nell'ambiente in uso. 
  - Se si passa il mouse su una sezione del grafico, viene visualizzato il numero dei dispositivi Surface con la versione del firmware selezionata. A partire da Configuration Manager versione 1806, quando si fa clic sulla sezione di un grafico, viene visualizzato un elenco di dispositivi pertinenti. <!--1358654-->
     ![Descrizione comando del firmware di Surface](media/Surface-Firmware-Hover.PNG)


## <a name="more-information"></a>Altre informazioni

Per altre informazioni sui dispositivi Surface, vedere il sito Web [Surface](https://www.microsoft.com/surface).

Per altre informazioni sulla distribuzione degli aggiornamenti del firmware Surface in Configuration Manager, vedere [Gestire i driver di Surface con Configuration Manager](../../../sum/deploy-use/surface-drivers.md).




