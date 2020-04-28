---
title: Uso di macchine virtuali Windows 10 con Microsoft Intune
titleSuffix: ''
description: Linee guida per l'uso di macchine virtuali Windows 10 con Microsoft Intune
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 11/20/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 944b3d98dc59dcae69f72fef5dfdb1793701f67a
ms.sourcegitcommit: 2871a17e43b2625a5850a41a9aff447c8ca44820
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2020
ms.locfileid: "82126180"
---
# <a name="using-windows-10-virtual-machines-with-intune"></a>Uso di macchine virtuali Windows 10 con Intune

Intune supporta la gestione di macchine virtuali che eseguono Windows 10 Enterprise con alcune limitazioni. La gestione di Intune non dipende o interferisce con la gestione di Desktop virtuale Windows della stessa macchina virtuale.

Quando si gestiscono le macchine virtuali Windows 10 con Intune, tenere presente quanto segue:

- Windows 10 Enterprise Multi-Session (Enterprise for Virtual Devices) usato in Desktop virtuale Windows non supporta attualmente la gestione di Intune.

## <a name="enrollment"></a>Registrazione
- Non è consigliabile gestire macchine virtuali su richiesta e host sessione con Intune. È necessario registrare ogni macchina virtuale al momento della creazione. Inoltre, l'eliminazione regolare delle macchine virtuali lascia i record di dispositivo orfani in Intune fino a quando non viene eseguita la [pulizia](../remote-actions/devices-wipe.md#automatically-delete-devices-with-cleanup-rules). 
- I tipi di distribuzione automatica e "White Glove" di Windows Autopilot non sono supportati perché richiedono un Trusted Platform Module (TPM) fisico. 
- La registrazione Configurazione guidata non è supportata nelle macchine virtuali a cui è possibile accedere solo tramite RDP, ad esempio le macchine virtuali ospitate in Azure. Questa restrizione comporta quanto segue:
    - Windows Autopilot e la configurazione guidata commerciale non sono supportati.
    - Le opzioni della pagina relativa allo stato della registrazione per i criteri del contesto del dispositivo non sono supportate.


## <a name="configuration"></a>Configurazione
Intune non supporta alcuna configurazione che usi un modulo TPM (Trusted Platform Module) o la gestione hardware, tra cui:
- [Impostazioni di BitLocker](../configuration/device-profiles.md#endpoint-protection)
- [Impostazioni di Interfaccia di configurazione del firmware del dispositivo](../configuration/device-profiles.md#device-firmware-configuration-interface)

## <a name="reporting"></a>Reporting
Intune rileva automaticamente le macchine virtuali e le segnala come "macchina virtuale" nel campo visualizzato scegliendo **Dispositivi** > **Tutti i dispositivi** > scegliere un dispositivo > **Panoramica** > **Modello**. 

Le macchine virtuali deallocate potrebbero essere incluse nei report di dispositivi non conformi poiché non sono in grado di [archiviare con il servizio Intune](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned).

## <a name="retirement"></a>Ritiro
Se si dispone solo dell'accesso RDP, non usare l'[azione di cancellazione](../remote-actions/devices-wipe.md#wipe). L'azione di cancellazione elimina le impostazioni RDP della macchina virtuale e impedisce ulteriori connessi.


