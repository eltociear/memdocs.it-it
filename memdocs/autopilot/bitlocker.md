---
title: Impostazione dell'algoritmo di crittografia BitLocker per i dispositivi Autopilot
ms.reviewer: ''
manager: laurawi
description: Microsoft Intune offre un set completo di opzioni di configurazione per la gestione di BitLocker nei dispositivi Windows 10.
keywords: Autopilot, BitLocker, crittografia, 256 bit, Windows 10
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
ms.openlocfilehash: 137001d443ba9d5d8e4a8532000a976778e7f818
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/04/2020
ms.locfileid: "87756715"
---
# <a name="setting-the-bitlocker-encryption-algorithm-for-autopilot-devices"></a>Impostazione dell'algoritmo di crittografia BitLocker per i dispositivi Autopilot

**Si applica a**

-   Windows 10

Con Windows Autopilot è possibile configurare le impostazioni di crittografia di BitLocker da applicare prima dell'avvio della crittografia automatica. In questo modo si garantisce che l'algoritmo di crittografia predefinito non venga applicato automaticamente quando questa non è l'impostazione desiderata. Prima che venga avviata la crittografia automatica di BitLocker, è inoltre possibile recapitare altri criteri di BitLocker che devono essere applicati prima della crittografia. 

L'algoritmo di crittografia BitLocker viene utilizzato quando BitLocker viene abilitato per la prima volta e imposta il livello di attendibilità in cui deve essere eseguita la crittografia completa del volume. Gli algoritmi di crittografia disponibili sono: AES-CBC 128 bit, AES-CBC 256-bit, XTS-AES 128-bit o XTS-AES 256-bit Encryption. Il valore predefinito è la crittografia XTS-AES a 128 bit. Per informazioni sugli algoritmi di crittografia consigliati da usare, vedere [BITLOCKER CSP](https://docs.microsoft.com/windows/client-management/mdm/bitlocker-csp) .

Per assicurarsi che l'algoritmo di crittografia BitLocker desiderato sia impostato prima che venga eseguita la crittografia automatica per i dispositivi Autopilot:

1. Configurare le [impostazioni del metodo di crittografia](https://docs.microsoft.com/intune/endpoint-protection-windows-10#windows-encryption) nel profilo di Endpoint Protection Windows 10 sull'algoritmo di crittografia desiderato. 
2. [Assegnare i criteri](https://docs.microsoft.com/intune/device-profile-assign) al gruppo di dispositivi Autopilot. 
    - **Importante**: i criteri di crittografia devono essere assegnati ai **dispositivi** del gruppo, non agli utenti.
3. Abilitare la pagina relativa [allo stato di registrazione](enrollment-status.md) di Autopilot (ESP) per questi dispositivi. 
    - **Importante**: se ESP non è abilitato, il criterio non verrà applicato prima dell'avvio della crittografia.

Di seguito è riportato un esempio di Microsoft Intune impostazioni di crittografia di Windows.

   ![Impostazioni di crittografia di BitLocker](images/bitlocker-encryption.png)

**Nota**: è necessario decrittografare un dispositivo crittografato automaticamente prima di modificare l'algoritmo di crittografia.

Le impostazioni sono disponibili in configurazione dispositivo-profili >-> Crea profilo-> Platform = Windows 10 e versioni successive, tipo di profilo = Endpoint Protection-> Configure-> crittografia Windows-> impostazioni di base di BitLocker, configurare i metodi di crittografia = Abilita.

**Nota**: è inoltre consigliabile impostare la crittografia windows-> impostazioni di windows-> Encrypt = **Require**.

## <a name="requirements"></a>Requisiti

Windows 10, versione 1809 o successiva.

## <a name="see-also"></a>Vedere anche

[Panoramica di BitLocker](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-overview)
