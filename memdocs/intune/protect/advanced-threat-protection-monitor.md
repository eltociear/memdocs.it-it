---
title: Monitorare l'integrazione di Microsoft Defender Advanced Threat Protection (ATP) in Microsoft Intune - Azure | Microsoft Docs
description: Monitorare Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) con Intune, incluso lo stato di conformità del dispositivo e di onboarding.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/23/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: cedb255a575d4b6ea04dd684b5592748e63397c8
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/28/2020
ms.locfileid: "87264537"
---
# <a name="monitor-device-status-when-you-integrate-microsoft-defender-atp-with-intune"></a>Monitorare lo stato del dispositivo quando si integra Microsoft Defender ATP con Intune

Quando si integrano Microsoft Intune e Microsoft Defender Advanced Threat Protection (ATP), è possibile visualizzare le informazioni sulla conformità dei dispositivi e sull'onboarding nell'interfaccia di amministrazione di Microsoft Endpoint Manager.

## <a name="monitor-device-compliance"></a>Monitorare la conformità dei dispositivi

Monitorare lo stato dei dispositivi in cui sono applicati i criteri di conformità di Microsoft Defender ATP.

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selezionare **Dispositivi** > **Monitoraggio** > **Conformità dei criteri**.

3. Trovare il proprio criterio di Microsoft Defender ATP nell'elenco e verificare quali dispositivi sono conformi o non conformi.

È anche possibile usare il report *operativo* per i dispositivi non conformi dallo stesso percorso:

- Selezionare **Dispositivi** > **Monitoraggio** > **Dispositivi non conformi**.

Per altre informazioni sui report, vedere [Report di Intune](../fundamentals/reports.md).

## <a name="view-onboarding-status"></a>Visualizzare lo stato di onboarding

Per visualizzare lo stato di onboarding dei dispositivi gestiti da Intune, accedere a **Sicurezza degli endpoint** > **Microsoft Defender ATP**. Da questa pagina è anche possibile creare un profilo di configurazione dei dispositivi per eseguire l'onboarding di altri dispositivi in Microsoft Defender ATP.

## <a name="next-steps"></a>Passaggi successivi

[Applicare la conformità per Microsoft Defender ATP con l'accesso condizionale in Intune](../protect/advanced-threat-protection.md)
