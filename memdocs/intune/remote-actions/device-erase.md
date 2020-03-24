---
title: Cancellare un dispositivo macOS
titleSuffix: Microsoft Intune
description: Informazioni su come cancellare tutti i dati, incluso il sistema operativo, da un dispositivo macOS.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ab396092-907a-44b7-a157-aabee62176a9
ms.reviewer: coferro
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 650ba81c9e92ce03b67e90cf188435b7dc0800fb
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79338214"
---
# <a name="erase-all-data-from-a-macos-device"></a>Cancellare tutti i dati da un dispositivo macOS

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

È possibile cancellare tutti i dati da un dispositivo macOS, incluso il sistema operativo. Il dispositivo verrà rimosso anche dalla gestione di Intune. Nessun avviso verrà visualizzato dall'utente finale.

1. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) scegliere **Dispositivi** > **Tutti i dispositivi** > scegliere il dispositivo che si vuole cancellare.
2. Fare clic su **Altro** > **Cancella** e quindi specificare un numero di 6 cifre per il **PIN di ripristino**. Questo è il PIN che è necessario dare all'utente per poter reinstallare il sistema operativo nel dispositivo. Assicurarsi di prendere nota di questo PIN perché non sarà visibile una volta completata l'azione di cancellazione.
![Screenshot](./media/device-erase/providepin.png)
3. Fare clic su **OK** per cancellare il dispositivo.