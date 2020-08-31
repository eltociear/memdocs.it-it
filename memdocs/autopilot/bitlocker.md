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
ms.openlocfilehash: f72410d0570e1b9ebbc324f26a288100e744f422
ms.sourcegitcommit: 41e6e6b7f5c2a87aaf7f23d90d0f175dd63c0579
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2020
ms.locfileid: "89056990"
---
# <a name="setting-the-bitlocker-encryption-algorithm-for-autopilot-devices"></a>Impostazione dell'algoritmo di crittografia BitLocker per i dispositivi Autopilot

**Si applica a**

-  Windows 10

Con Windows Autopilot è possibile configurare le impostazioni di crittografia di BitLocker per l'applicazione prima che venga avviata la crittografia automatica. Questa configurazione garantisce che l'algoritmo di crittografia predefinito non venga applicato automaticamente. Prima che venga avviata la crittografia automatica di BitLocker, è inoltre possibile applicare altri criteri di BitLocker. 

L'algoritmo di crittografia BitLocker viene utilizzato quando BitLocker viene abilitato per la prima volta. L'algoritmo imposta il livello di attendibilità per la crittografia completa del volume. Gli algoritmi di crittografia disponibili sono: AES-CBC 128 bit, AES-CBC 256-bit, XTS-AES 128-bit o XTS-AES 256-bit Encryption. Il valore predefinito è la crittografia XTS-AES a 128 bit. Per informazioni sugli algoritmi di crittografia consigliati da usare, vedere [BITLOCKER CSP](/windows/client-management/mdm/bitlocker-csp) .

Per assicurarsi che l'algoritmo di crittografia BitLocker desiderato sia impostato prima che venga eseguita la crittografia automatica per i dispositivi Autopilot:

1. Configurare le [impostazioni del metodo di crittografia](/intune/endpoint-protection-windows-10#windows-encryption) nel profilo di Endpoint Protection Windows 10 sull'algoritmo di crittografia desiderato. 
2. [Assegnare i criteri](/intune/device-profile-assign) al gruppo di dispositivi Autopilot. Il criterio di crittografia deve essere assegnato ai **dispositivi** del gruppo, non agli utenti.
3. Abilitare la pagina relativa [allo stato di registrazione](enrollment-status.md) di Autopilot (ESP) per questi dispositivi. Se ESP non è abilitato, il criterio non verrà applicato prima dell'avvio della crittografia.

Di seguito è riportato un esempio di Microsoft Intune impostazioni di crittografia di Windows.

![Impostazioni di crittografia di BitLocker](images/bitlocker-encryption.png)

Un dispositivo crittografato automaticamente dovrà essere decrittografato prima di modificare l'algoritmo di crittografia.

Le impostazioni sono disponibili in **Configurazione dispositivo**  >  **profili**  >  **Crea profilo**  >  **piattaforma** = Windows 10 e versioni successive, tipo di profilo = Endpoint Protection > **configurare**  >  **Windows Encryption**  >  **le impostazioni di base di BitLocker**di crittografia Windows, configurare i metodi di crittografia = Abilita.

Si consiglia inoltre di impostare **Windows Encryption**  >  **le impostazioni di Windows**per crittografia Windows  >  **Encrypt** = require.

## <a name="requirements"></a>Requisiti

Windows 10, versione 1809 o successiva.

## <a name="next-steps"></a>Passaggi successivi

[Panoramica di BitLocker](/windows/security/information-protection/bitlocker/bitlocker-overview)