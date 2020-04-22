---
title: Dashboard dei dispositivi Surface
titleSuffix: Configuration Manager
description: Esaminare le informazioni relative ai dispositivi Surface tramite il dashboard.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 7397fc17-3ae8-4525-8386-aea8a9cffa06
ms.openlocfilehash: 08baf595199bdda121f897d507de97cb7e93e620
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696349"
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
     ![Elenco dei dispositivi per un modello di dispositivo Surface](media/Surface-Firmware-Hover.PNG)


## <a name="more-information"></a>Altre informazioni

Per altre informazioni sui dispositivi Surface, vedere:
- Il sito Web [Surface]( https://go.microsoft.com/fwlink/?linkid=861998).

Per altre informazioni sulla distribuzione degli aggiornamenti del firmware di Surface in Configuration Manager, vedere:
- [Come gestire gli aggiornamenti dei driver di Surface in Configuration Manager]( https://support.microsoft.com/help/4098906).




