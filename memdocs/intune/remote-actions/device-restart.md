---
title: Riavviare i dispositivi con Microsoft Intune - Azure | Microsoft Docs
description: È possibile riavviare i dispositivi Windows e iOS/iPadOS con Microsoft Intune nel portale di Azure usando l'azione remota Riavvia.
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
ms.assetid: c707e0c4-391a-4bad-9dfd-9a7799c48dd5
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 45317cc9c43f4f25f0adc043ce784a7b3dc4b9fd
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2020
ms.locfileid: "86461777"
---
# <a name="remotely-restart-devices-with-intune"></a>Riavviare i dispositivi in remoto con Intune


[!INCLUDE [azure_portal](../includes/azure_portal.md)]

L'azione del dispositivo **Riavvia** causa il riavvio del dispositivo scelto (entro 5 minuti). Il proprietario del dispositivo non viene avvisato automaticamente del riavvio e può perdere il proprio lavoro.

## <a name="supported-platforms"></a>Piattaforme supportate

- Windows: funzionalità supportata in Windows 8.1 e versioni successive
- Windows Phone: funzionalità supportata in Windows Phone 8.1 e versioni successive
- Dispositivi Android Enterprise dedicati - Supportati in Android 7.0 e versioni successive
- Dispositivi Android Enterprise completamente gestiti - Supportati in Android 6.0 e versioni successive
- Dispositivi Android Enterprise di proprietà aziendale con profilo di lavoro - Supportati in Android 8.0 e versioni successive
- iOS/iPadOS: supportata

    > [!Note]  
    > Per eseguire questo comando sono necessari un dispositivo supervisionato e il diritto di accesso **Device Lock** (Blocco dispositivo). Il dispositivo viene riavviato immediatamente. I dispositivi iOS/iPadOS bloccati con passcode non vengono di nuovo aggiunti a una rete Wi-Fi dopo il riavvio. Dopo il riavvio il dispositivo potrebbe non essere in grado di comunicare con il server.
- macOS: funzionalità non supportata
- Dispositivi Android e del profilo di lavoro Android: funzionalità non supportata

## <a name="restart-a-device"></a>Riavviare un dispositivo

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Selezionare **Dispositivi** > **Tutti i dispositivi**.
4. Selezionare un dispositivo nell'elenco dei dispositivi gestiti > **Riavvia** > **Sì**.

## <a name="next-steps"></a>Passaggi successivi

- Per visualizzare lo stato dell'azione del dispositivo **Riavvia**, selezionare **Dispositivi** > **Azioni del dispositivo**.
