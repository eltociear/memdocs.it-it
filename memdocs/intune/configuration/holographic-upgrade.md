---
title: Eseguire l'aggiornamento a Windows Holographic for Business
titleSuffix: Microsoft Intune
description: Informazioni su come aggiornare i dispositivi che eseguono Windows Holographic a Windows Holographic for Business
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/22/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: f4e809a888fc2696e54540ee6baa2271d7340579
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "79361055"
---
# <a name="upgrade-devices-running-windows-holographic-to-windows-holographic-for-business"></a>Aggiornare i dispositivi che eseguono Windows Holographic a Windows Holographic for Business

Microsoft Intune include diverse impostazioni utili per la gestione e la protezione dei dispositivi. Questo articolo elenca e descrive le impostazioni per aggiornare i dispositivi Windows Holographic a Windows Holographic for Business. Queste impostazioni vengono create in un profilo di configurazione dell'aggiornamento in Intune di cui viene eseguito il push o la distribuzione nei dispositivi.

Usare queste impostazioni nella propria soluzione di gestione di dispositivi mobili (MDM) per aggiornare i dispositivi Windows Holographic. Per Microsoft HoloLens è possibile acquistare Commercial Suite per ottenere la licenza necessaria per l'aggiornamento. Per altre informazioni, vedere [Sbloccare le funzionalità di Windows Holographic for Business](https://docs.microsoft.com/hololens/hololens1-upgrade-enterprise).

Per altre informazioni su questa funzionalità, vedere [Aggiornare le edizioni di Windows 10 o abilitare la modalità S](edition-upgrade-configure-windows-10.md).

## <a name="before-you-begin"></a>Prima di iniziare

[Creare un profilo di configurazione del dispositivo](edition-upgrade-configure-windows-10.md#create-the-profile).

## <a name="edition-upgrade"></a>Aggiornamento dell'edizione

- **Edizione a cui eseguire l'aggiornamento**: selezionare **Windows 10 Holographic for Business**.
- **File di licenza**: cercare e selezionare il file di licenza XML fornito.

  ![Immettere il nome del file XML che include le informazioni sulla licenza Holographic for Business](./media/holographic-upgrade/Holographic-edition-upgrade.png)
 
## <a name="next-steps"></a>Passaggi successivi

Il profilo è stato creato, ma potrebbe non essere ancora operativo. Assicurarsi di [assegnare il profilo](device-profile-assign.md) e [monitorarne lo stato](device-profile-monitor.md).

È anche possibile creare i profili di aggiornamento dell'edizione per i dispositivi [Windows 10 e versioni successive](edition-upgrade-windows-settings.md).
