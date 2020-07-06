---
title: Restrizioni di registrazione dei dispositivi per il framework di configurazione della sicurezza di Android Enterprise
titleSuffix: Microsoft Intune
description: Restrizioni di registrazione dei dispositivi per il framework di configurazione della sicurezza di Android Enterprise.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/24/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: rosssmi
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: d26040c5a009a9c3877abbc25512e317f584f114
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/27/2020
ms.locfileid: "85502975"
---
# <a name="android-enterprise-device-enrollment-restrictions"></a>Restrizioni di registrazione dei dispositivi Android Enterprise

Prima di registrare dispositivi per il [Framework di configurazione della sicurezza di Android Enterprise](), le organizzazioni devono configurare le restrizioni appropriate. Queste restrizioni assicurano che gli utenti possano eseguire la registrazione solo di
- dispositivi approvati;
- un numero specifico di dispositivi;
- dispositivi con piattaforme specifiche;
- dispositivi con sistemi operativi specifici;
- dispositivi di produttori specifici.

Per altre informazioni sulle restrizioni di registrazione dei dispositivi, vedere [Impostare le restrizioni di registrazione](enrollment-restrictions-set.md).

## <a name="work-profile-basic-level-1-security-restrictions"></a>Restrizioni di sicurezza di base (livello 1) del profilo di lavoro

Per la sicurezza di base (livello 1) del profilo di lavoro di Android Enterprise, è necessario implementare le restrizioni seguenti per i dispositivi:

| Tipo | Piattaforma | Version | Dispositivi personali consentiti |
|--------|--------|--------|--------|
| Android Enterprise | Consenti | Android 5.0 e versioni successive.<p>Microsoft consiglia di configurare la versione principale minima di Android in modo che corrisponda alle versioni di Android supportate per le app Microsoft. Gli OEM e i dispositivi che rispettano i requisiti consigliati per Android Enterprise devono supportare la versione corrente con l'aggiornamento di una sola lettera.   Attualmente Android consiglia Android 8.0 e versioni successive per i knowledge worker. Per altre informazioni, vedere [Android Enterprise Recommended requirements](https://www.android.com/enterprise/recommended/requirements/) (Requisiti consigliati di Android Enterprise). | Sì |
| Amministratore dispositivo Android| Blocca | Tutte le versioni | Sì |

## <a name="work-profile-high-level-3-security-restrictions"></a>Restrizioni di sicurezza elevate (livello 3) del profilo di lavoro
Per la sicurezza elevata (livello 3) del profilo di lavoro di Android Enterprise, è necessario implementare le restrizioni seguenti per i dispositivi:

| Tipo | Piattaforma | Version | Dispositivi personali consentiti |
|--------|--------|--------|--------|
| Android Enterprise | Consenti | Android 8.0 e versioni successive | Sì |
| Amministratore dispositivo Android| Blocca | Tutte le versioni | Sì |

## <a name="fully-managed-security-restrictions"></a>Restrizioni di sicurezza completamente gestite
Assicurarsi che l'organizzazione supporti la registrazione dei dispositivi completamente gestita Android Enterprise esaminando le caratteristiche di questa funzionalità. 

## <a name="next-steps"></a>Passaggi successivi

[Impostare criteri di configurazione dell'app](android-app-configuration-policies.md)
