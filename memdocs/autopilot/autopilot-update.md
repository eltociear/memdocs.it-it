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
ms.openlocfilehash: 34db88c53cdd7db46c126f15bb60a7fd2941a627
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/04/2020
ms.locfileid: "87757374"
---
# <a name="windows-autopilot-update"></a>Aggiornamento di Windows Autopilot

**Si applica a**

-   Windows 10, versione 1903

Aggiornamento di Windows Autopilot consente di ottenere le funzionalità di Autopilot più recenti e correzioni di problemi critici senza dover passare alla versione più recente del sistema operativo Windows. Con l'aggiornamento di Autopilot, le organizzazioni possono mantenere la versione corrente del sistema operativo e trarre vantaggio dalle nuove funzionalità e correzioni di bug di Autopilot.
 
Durante il processo di distribuzione di Autopilot, l'aggiornamento di Windows Autopilot è stato aggiunto come nuovo nodo dopo il controllo di aggiornamento critico di [Windows Zero Day patch (ZDP)](https://docs.microsoft.com/windows-hardware/customize/desktop/windows-updates-during-oobe) . Durante il processo di aggiornamento, i dispositivi di Windows Autopilot raggiungono Windows Update per verificare la presenza di un nuovo aggiornamento automatico.  Se è disponibile un aggiornamento automatico, il dispositivo scaricherà e installerà l'aggiornamento, quindi verrà riavviato automaticamente. Vedere l'esempio seguente.

   ![Aggiornamento automatico 1](images/update1.png)<br>
   ![Aggiornamento automatico 2](images/update2.png)<br>
   ![Aggiornamento automatico 3](images/update3.png)

Nel diagramma seguente viene illustrata una tipica orchestrazione della distribuzione di Windows Autopilot durante l'esperienza predefinita (OOBE) con il nuovo nodo di aggiornamento di Windows Autopilot.

   ![Flusso di aggiornamento di Autopilot](images/update-flow.png)

## <a name="release-cadence"></a>Frequenza di rilascio

- Quando è disponibile un aggiornamento di Autopilot, viene in genere rilasciato il 4 martedì del mese. È possibile che l'aggiornamento venga rilasciato in una settimana diversa se si verifica un'eccezione.
- Verrà pubblicato anche un articolo della Knowledge base (KB) per documentare le modifiche incluse nell'aggiornamento.

Per un elenco degli aggiornamenti rilasciati, vedere la cronologia degli aggiornamenti di [Autopilot](windows-autopilot-whats-new.md#windows-autopilot-update-history).

## <a name="see-also"></a>Vedere anche

[Windows Update durante la configurazione guidata](https://docs.microsoft.com/windows-hardware/customize/desktop/windows-updates-during-oobe)<br>
[Novità di Windows Autopilot](windows-autopilot-whats-new.md)<br>