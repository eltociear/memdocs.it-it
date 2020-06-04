---
title: Gestire la crittografia del disco con i criteri di sicurezza degli endpoint in Microsoft Intune | Microsoft Docs
description: Configurare e distribuire criteri per i dispositivi gestiti con i criteri di crittografia del disco per la sicurezza degli endpoint in Microsoft Endpoint Manager.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: b988e4ddeb306c7da290c87e8a32fa0571627257
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431670"
---
# <a name="disk-encryption-policy-for-endpoint-security-in-intune"></a>Criteri di crittografia del disco per la sicurezza degli endpoint in Intune

I profili di crittografia del disco per la sicurezza degli endpoint si concentrano solo sulle impostazioni rilevanti per un metodo di crittografia predefinito dei dispositivi, ad esempio FileVault o BitLocker. Questo focus consente agli amministratori della sicurezza di gestire in modo semplice le impostazioni di crittografia del disco senza dover passare in un host di impostazioni non correlate.

Sebbene sia possibile configurare le stesse impostazioni del dispositivo usando i profili *Endpoint Protection* per la configurazione del dispositivo, i profili di configurazione del dispositivo includono categorie aggiuntive di impostazioni. Queste impostazioni aggiuntive non sono correlate alla crittografia del disco e possono complicare l'attività di configurare solo la crittografia del disco.

I criteri di sicurezza degli endpoint per i criteri di crittografia del disco sono disponibili in *Gestione* nel nodo **Sicurezza degli endpoint** dell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

## <a name="prerequisites-for-disk-encryption-policy"></a>Prerequisiti per i criteri di crittografia del disco

- **macOS**: macOS 10.13 o versioni successive
- **Windows**: Windows 10 o versioni successive

## <a name="disk-encryption-profiles"></a>Profili di crittografia del disco

**Profili macOS**:

- **FileVault**: FileVault fornisce la crittografia completa del disco predefinita per dispositivi macOS.

  Gestire le [impostazioni di FileVault](../protect/endpoint-security-disk-encryption-profile-settings.md#filevault) per macOS.

  Per creare un profilo FileVault, vedere [Usare la crittografia del disco FileVault per macOS](../protect/encrypt-devices-filevault.md).

**Profili di Windows 10**:

- **BitLocker**: Crittografia unità BitLocker è una funzionalità di protezione dei dati che si integra con il sistema operativo e affronta le minacce relative al furto o alla diffusione di dati da computer persi, rubati o ritirati in modo non appropriato

  Gestire le [impostazioni BitLocker](../protect/endpoint-security-disk-encryption-profile-settings.md#bitlocker) per Windows 10.

  Per creare un profilo BitLocker, vedere [Usare la crittografia del disco BitLocker per Windows 10](../protect/encrypt-devices.md).

## <a name="manage-device-encryption"></a>Gestire la crittografia del dispositivo

Dopo aver distribuito i criteri per crittografare un disco del dispositivo, vedere gli articoli seguenti per informazioni sulla gestione della crittografia:

- [Gestire BitLocker](../protect/encrypt-devices.md#manage-bitlocker)
- [Gestire FileVault](../protect/encrypt-devices-filevault.md#manage-filevault)
- [Monitorare la crittografia del dispositivo](../protect/encryption-monitor.md)

## <a name="next-steps"></a>Passaggi successivi

- [Per creare un profilo FileVault](../protect/encrypt-devices-filevault.md#create-an-endpoint-security-policy-for-filevault)
- [Per creare un profilo BitLocker](../protect/encrypt-devices.md#create-an-endpoint-security-policy-for-bitlocker)
