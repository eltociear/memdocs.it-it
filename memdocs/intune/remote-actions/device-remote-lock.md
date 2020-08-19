---
title: Bloccare i dispositivi con Microsoft Intune - Azure | Microsoft Docs
description: Usare l'azione Blocco remoto in Microsoft Intune per bloccare un dispositivo protetto da PIN o password.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 3b67f285-229d-4a0f-ae34-0402a20b4518
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4e558c885098b8b396ca0e6304bd18ef36e3c28b
ms.sourcegitcommit: cb12dd341792c0379bebe9fd5f844600638c668a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/15/2020
ms.locfileid: "88252238"
---
# <a name="remotely-lock-devices-with-intune"></a>Bloccare in remoto i dispositivi con Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

L'azione del dispositivo **Blocco remoto** consente di bloccare il dispositivo. Per sbloccarlo, il proprietario del dispositivo immette il passcode. È possibile bloccare in remoto i dispositivi per i quali è impostato un PIN o una password. I dispositivi senza PIN o password non possono essere bloccati in remoto.

## <a name="supported-platforms"></a>Piattaforme supportate

Il **Blocco remoto** è supportato nelle piattaforme seguenti:

- Android
- Dispositivi in modalità tutto schermo di Android Enterprise
- Dispositivi con profilo di lavoro Android Enterprise
- Dispositivi completamente gestiti Android Enterprise
- Dispositivi Android Enterprise di proprietà aziendale con profilo di lavoro
- iOS
- macOS

La funzionalità **Blocco remoto** non è supportata in:
- Windows 10 Desktop

> [!NOTE]
> Per i dispositivi macOS, impostare un PIN di ripristino di 6 cifre. Quando il dispositivo è bloccato, nella **Panoramica** del dispositivo viene visualizzato il PIN finché non viene inviata un'altra azione del dispositivo. Assicurarsi di prendere nota del PIN poiché sarà disponibile solo per 30 giorni dopo l'invio del comando di blocco remoto. Dopo i 30 giorni, il PIN non sarà più disponibile per Intune. Verrà inoltre visualizzato uno stato di errore nei report se si avvia nuovamente questo comando per lo stesso dispositivo, mentre il PIN originale non è stato usato per sbloccare correttamente il dispositivo. È necessario inviare questo comando una sola volta, annotare il PIN e fino a quando non lo si usa per accedere correttamente al dispositivo macOS, non tentare di inviare di nuovo questo comando allo stesso dispositivo.


## <a name="remote-lock-a-device"></a>Blocco remoto un dispositivo

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Selezionare **Dispositivi** > **Tutti i dispositivi**.
4. Nell'elenco dei dispositivi selezionare un dispositivo e quindi l'azione **Blocco remoto**.

## <a name="next-steps"></a>Passaggi successivi

- Per visualizzare lo stato di questa azione, selezionare **Microsoft Intune** > **Dispositivi** > **Azioni del dispositivo**. 
- Per altre azioni utili per la gestione dei dispositivi, vedere [Azioni disponibili](device-management.md).
