---
title: Usare le azioni in blocco del dispositivo nel dispositivo Microsoft Intune.
titleSuffix: ''
description: Usare le azioni in blocco del dispositivo remote.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 3/12/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5f33198e71fd4250ee93207e571bc535abd1c95f
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "80325379"
---
# <a name="use-bulk-device-actions"></a>Usare le azioni in blocco del dispositivo

È possibile usare le azioni in blocco del dispositivo per le azioni remote seguenti:
- [Reimpostazione di Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot-reset#reset-devices-with-remote-windows-autopilot-reset)
- [Notifiche personalizzate](custom-notifications.md#send-a-custom-notification-to-a-single-device)
- [Elimina](devices-wipe.md#delete-devices-from-the-intune-portal)
- [Rinomina](device-rename.md)
- [Riavvia](device-restart.md)
- [Sincronizza](device-sync.md)
- [Cancellazione](devices-wipe.md#wipe)

## <a name="use-a-bulk-device-action"></a>Usare un'azione in blocco del dispositivo

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Scegliere **Dispositivi** > **Tutti i dispositivi** > **Azioni in blocco del dispositivo**.
![Azioni in blocco del dispositivo](./media/bulk-device-actions/bulk-device-actions.png)
3. Nella pagina **Azione in blocco del dispositivo** selezionare un **sistema operativo** e **Azione del dispositivo**. Per alcune azioni del dispositivo sono disponibili altre opzioni o campi da popolare. Scegliere **Avanti**.
4. Nella pagina **Dispositivi** selezionare da 1 a 100 dispositivi > **Avanti**.
5. Nella pagina **Rivedi e crea** selezionare **Crea**.

## <a name="next-steps"></a>Passaggi successivi
[Panoramica della gestione dei dispositivi.](device-management.md)
