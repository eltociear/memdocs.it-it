---
title: Entità IntuneManagementExtension
titleSuffix: Microsoft Intune
description: Argomento di riferimento per l'entità della categoria IntuneManagementExtension della raccolta di entità nell'API Data Warehouse di Intune.
keywords: Data warehouse di Intune
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/03/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 73DF3B90-6D52-4EF6-AFFD-1873A18C7421
ms.reviewer: dariusz
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: f8152eb12779376e1885d0a2b2898cd602aa825d
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79359768"
---
# <a name="reference-for-intune-management-extensions"></a>Informazioni di riferimento per le estensioni di gestione di Intune

La categoria **intuneManagementExtensions** contiene le entità per i dispositivi mobili che tengono traccia di informazioni come:

- Versioni di IntuneManagementExtension
- Stato di installazione di IntuneManagementExtension

## <a name="intunemanagementextensionversions"></a>intuneManagementExtensionVersions

L'entità **intuneManagementExtensionVersion** elenca tutte le versioni usate da intuneManagementExtensionVersion.

| Proprietà  | Descrizione | Esempio |
|---------|------------|--------|
| extensionVersionKey |Identificatore univoco della versione di intuneManagementExtensionVersion. | 1 |
| extensionVersion |Numero della versione a 4 cifre. |1.0.2.0 |

## <a name="intunemanagementextensionhealthstates"></a>intuneManagementExtensionHealthStates

**intuneManagementExtensionHealthState** elenca tutti i possibili stati di integrità di intuneManagementExtensions.

| Proprietà  | Descrizione | Esempio |
|---------|------------|--------|
| extensionStateKey |Identificatore univoco dello stato di integrità. | 2 |
| extensionState |Stato di integrità di IntuneManagementExtension. | Healthy |

## <a name="intunemanagementextensions"></a>intuneManagementExtensions

**intuneManagementExtension** elenca l'integrità di IntuneManagementExtensions per ogni dispositivo Windows 10 al giorno.
I dati mantenuti sono quelli relativi agli ultimi 60 giorni. 


|      Proprietà       |                         Descrizione                         | Esempio |
|---------------------|-------------------------------------------------------------|---------|
|       dateKey       |               Identificatore univoco della data.                |   123   |
|      tenantKey      |              Identificatore univoco del tenant.               |   456   |
|      deviceKey      |              Identificatore univoco del dispositivo.               |   789   |
| extensionVersionKey | Identificatore univoco della versione di intuneManagementExtension. |    1    |
|  extensionStateKey  |             Identificatore univoco dello stato di integrità.              |    2    |
