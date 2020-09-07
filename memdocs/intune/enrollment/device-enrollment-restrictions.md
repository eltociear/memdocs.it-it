---
title: Restrizioni di registrazione dei dispositivi per il framework di configurazione della sicurezza di Android Enterprise
titleSuffix: Microsoft Intune
description: Restrizioni di registrazione dei dispositivi per il framework di configurazione della sicurezza di Android Enterprise.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 07/02/2020
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
ms.openlocfilehash: 618be398d963e0a796ad9be7e8810201fc5e12f5
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88995093"
---
# <a name="android-enterprise-device-enrollment-restrictions"></a>Restrizioni di registrazione dei dispositivi Android Enterprise

Prima di registrare dispositivi per il [Framework di configurazione della sicurezza di Android Enterprise](android-configuration-framework.md), le organizzazioni devono configurare le restrizioni appropriate. Queste restrizioni assicurano che gli utenti possano eseguire la registrazione solo di

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
Per assicurarsi che l'organizzazione supporti la registrazione dei dispositivi completamente gestiti Android Enterprise, vedere [Registrare i dispositivi completamente gestiti](android-fully-managed-enroll.md#enroll-the-fully-managed-devices). 

## <a name="conditional-access-policies"></a>Criteri di accesso condizionale
Le organizzazioni possono usare i criteri di accesso condizionale di Azure AD per assicurarsi che gli utenti possano accedere solo ai contenuti aziendali o dell'istituto di istruzione nei dispositivi Android registrati. A tale scopo, è necessario disporre di criteri di accesso condizionale destinati a tutti i potenziali utenti. Per informazioni dettagliate sulla creazione di questi criteri, vedere [Richiedere dispositivi gestiti per l'accesso alle app cloud con l'accesso condizionale](/azure/active-directory/conditional-access/require-managed-devices). 

Seguire i passaggi descritti in [Scenario: Richiedere la registrazione per i dispositivi iOS e Android](/azure/active-directory/conditional-access/require-managed-devices#scenario-require-device-enrollment-for-ios-and-android-devices), per assicurarsi che solo i dispositivi mobili registrati conformi possano connettersi agli endpoint di Microsoft 365.

## <a name="next-steps"></a>Passaggi successivi

[Impostare criteri di configurazione dell'app](android-app-configuration-policies.md)