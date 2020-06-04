---
title: Eseguire l'aggiornamento a Windows Holographic for Business in Microsoft Intune - Azure | Microsoft Docs
description: Eseguire l'aggiornamento a Windows 10 Holographic for Business usando un profilo di configurazione del dispositivo in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: d561d2682cf90d5d7075640c260d8f21c8b891b1
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556116"
---
# <a name="upgrade-devices-running-windows-holographic-to-windows-holographic-for-business"></a>Aggiornare i dispositivi che eseguono Windows Holographic a Windows Holographic for Business

Microsoft Intune include diverse impostazioni utili per la gestione e la protezione dei dispositivi. Questo articolo elenca e descrive le impostazioni per aggiornare i dispositivi Windows Holographic a Windows Holographic for Business.

Usare queste impostazioni nella propria soluzione di gestione di dispositivi mobili (MDM) per aggiornare i dispositivi Windows Holographic. Per Microsoft HoloLens è possibile acquistare Commercial Suite per ottenere la licenza necessaria per l'aggiornamento. Per altre informazioni, vedere [Sbloccare le funzionalità di Windows Holographic for Business](https://docs.microsoft.com/hololens/hololens1-upgrade-enterprise).

Come amministratore di Intune, è possibile creare e assegnare queste impostazioni ai dispositivi.

Per altre informazioni su questa funzionalità, vedere [Aggiornare le edizioni di Windows 10 o abilitare la modalità S](edition-upgrade-configure-windows-10.md).

## <a name="before-you-begin"></a>Prima di iniziare

[Creare un profilo di configurazione del dispositivo per l'aggiornamento e il cambio modalità dell'edizione di Windows 10](edition-upgrade-configure-windows-10.md#create-the-profile).

Quando si crea un profilo di configurazione del dispositivo per l'aggiornamento e il cambio modalità dell'edizione di Windows 10, sono disponibili altre impostazioni rispetto a quelle elencate in questo articolo. I dispositivi Windows Holographic for Business supportano le impostazioni indicate in questo articolo.

## <a name="edition-upgrade"></a>Aggiornamento dell'edizione

- **Edizione a cui eseguire l'aggiornamento**: Selezionare **Windows 10 Holographic for Business**.
- **File di licenza**: Cercare e selezionare il file di licenza XML fornito.

  :::image type="content" source="./media/holographic-upgrade/Holographic-edition-upgrade.png" alt-text="In Intune immettere il nome del file XML che include le informazioni sulla licenza Holographic for Business.":::

## <a name="next-steps"></a>Passaggi successivi

[Assegnare il profilo](device-profile-assign.md) e [monitorarne lo stato](device-profile-monitor.md).

È anche possibile creare i profili di aggiornamento dell'edizione per i dispositivi [Windows 10 e versioni successive](edition-upgrade-windows-settings.md).
