---
title: Aggiornamento di Windows Autopilot
ms.reviewer: ''
manager: laurawi
description: Aggiornamento di Windows Autopilot
keywords: Autopilot, aggiornamento, Windows 10
ms.prod: w10
ms.mktglfcycl: deploy
ms.sitesec: library
ms.pagetype: deploy
ms.localizationpriority: medium
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: a677dec0d722f0ef17a8c16248a41dea1b0be947
ms.sourcegitcommit: 42882de75c8a984ba35951b1165c424a7e0ba42e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2020
ms.locfileid: "89068121"
---
# <a name="windows-autopilot-update"></a>Aggiornamento di Windows Autopilot

**Si applica a**

- Windows 10, versione 1903

Windows Autopilot Update installa le funzionalità e le correzioni più recenti di Autopilot per i dispositivi Autopilot dell'organizzazione. I dispositivi non vengono spostati nella versione più recente del sistema operativo Windows. Con l'aggiornamento di Autopilot è possibile mantenere la versione corrente del sistema operativo dei dispositivi e sfruttare ancora le nuove funzionalità e correzioni di bug.

Il processo di aggiornamento di Windows Autopilot si verifica dopo il controllo di aggiornamento critico di [Windows Zero Day patch (ZDP)](/windows-hardware/customize/desktop/windows-updates-during-oobe) . Durante il processo di aggiornamento, i dispositivi controllano Windows Update per un nuovo aggiornamento automatico. Se è disponibile un aggiornamento di Autopilot, il dispositivo Scarica e installa l'aggiornamento, quindi riavvia automaticamente. Vedere l'esempio seguente.

 ![Aggiornamento automatico 1](images/update1.png)<br>
 ![Aggiornamento automatico 2](images/update2.png)<br>
 ![Aggiornamento automatico 3](images/update3.png)

Nel diagramma seguente viene illustrata una tipica orchestrazione della distribuzione di Windows Autopilot durante l'esperienza predefinita (OOBE) con il nuovo nodo di aggiornamento di Windows Autopilot.

 ![Flusso di aggiornamento di Autopilot](images/update-flow.png)

## <a name="release-cadence"></a>Frequenza di rilascio

- Quando è disponibile un aggiornamento di Autopilot, viene in genere rilasciato il quarto martedì del mese. È possibile che l'aggiornamento venga rilasciato in una settimana diversa se si verifica un'eccezione.
- Verrà pubblicato anche un articolo della Knowledge base (KB) per documentare le modifiche incluse nell'aggiornamento.

Per un elenco degli aggiornamenti rilasciati, vedere la cronologia degli aggiornamenti di [Autopilot](windows-autopilot-whats-new.md#windows-autopilot-update-history).

## <a name="see-also"></a>Vedere anche

[Windows Update durante la configurazione guidata](/windows-hardware/customize/desktop/windows-updates-during-oobe)<br>
[Novità di Windows Autopilot](windows-autopilot-whats-new.md)<br>