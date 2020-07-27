---
title: Impostazioni per il rilevamento di endpoint e risposta per la sicurezza degli endpoint in Intune | Microsoft Docs
description: Impostazioni di criteri per il rilevamento di endpoint e risposta per la sicurezza degli endpoint in Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
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
ms.openlocfilehash: e26719bb9bf322e3e4bf11b39911e98788707629
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2020
ms.locfileid: "86460417"
---
# <a name="endpoint-detection-and-response-policy-settings-for-endpoint-security-in-intune"></a>Impostazioni di criteri per il rilevamento di endpoint e risposta per la sicurezza degli endpoint in Intune

Visualizzare le impostazioni che è possibile configurare nei profili per i [criteri di rilevamento di endpoint e risposta](../protect/endpoint-security-edr-policy.md) nel nodo sicurezza degli endpoint di Intune.

Piattaforme e profili supportati:

- **Windows 10 e versioni successive**: usare questa piattaforma per i criteri distribuiti nei dispositivi gestiti con Intune.
  - Profilo: **Rilevamento di endpoint e risposta (MDM)**

- **Windows 10 e Windows Server**: usare questa piattaforma per i criteri distribuiti nei dispositivi gestiti da Configuration Manager.
  - Profilo: **Rilevamento di endpoint e risposta (ConfigMgr)**

## <a name="endpoint-detection-and-response-mdm"></a>Rilevamento di endpoint e risposta (MDM)

**Rilevamento di endpoint e risposta**:

- **Tipo del pacchetto di configurazione client di Microsoft Defender ATP**

  Caricare un pacchetto di configurazione firmato che verrà usato per l'onboarding del client Microsoft Defender ATP.

  - **Non configurato** (*impostazione predefinita*)
  - **BLOB di onboarding**  
  - **BLOB di offboarding**  

  Se impostato su *BLOB di onboarding*, è possibile configurare le impostazioni seguenti:

  - **BLOB di onboarding di Advanced Threat Protection**  
    Fare clic su **Select onboarding file** (Seleziona file di onboarding) per aprire il riquadro *Select onboarding file* (Seleziona file di onboarding), in cui è possibile specificare un file `.onboarding`.

  Se impostato su *BLOB di offboarding*, è possibile configurare le impostazioni seguenti:
  
  - **BLOB di offboarding di Advanced Threat Protection**  
     Fare clic su **Select offboarding file** (Seleziona file di offboarding) per aprire il riquadro *Select offboarding file* (Seleziona file di offboarding), in cui è possibile specificare un file `.offboarding`.

- **Condivisione di esempi per tutti i file**  

  Restituisce o imposta il parametro di configurazione per la condivisione di esempi di Microsoft Defender Advanced Threat Protection.  
  - **Non configurato**   (*impostazione predefinita*)
  - **Sì**

- **Accelera la frequenza di creazione di report di telemetria**

  - **Non configurato**   (*impostazione predefinita*)
  - **Sì**: consente di aumentare la frequenza di creazione di report di telemetria di Microsoft Defender Advanced Threat Protection.

## <a name="endpoint-detection-and-response-configmgr"></a>Rilevamento di endpoint e risposta (ConfigMgr)

**Rilevamento di endpoint e risposta**:

- **Condivisione di esempi per tutti i file**  

  Restituisce o imposta il parametro di configurazione per la condivisione di esempi di Microsoft Defender Advanced Threat Protection.  
  - **Non configurato**   (*impostazione predefinita*)
  - **Sì**

- **Accelera la frequenza di creazione di report di telemetria**

  - **Non configurato**   (*impostazione predefinita*)
  - **Sì**: consente di aumentare la frequenza di creazione di report di telemetria di Microsoft Defender Advanced Threat Protection.

## <a name="next-steps"></a>Passaggi successivi

[Criteri di sicurezza degli endpoint per EDR](../protect/endpoint-security-edr-policy.md)
