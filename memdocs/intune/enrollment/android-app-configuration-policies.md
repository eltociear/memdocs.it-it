---
title: Criteri di configurazione della sicurezza di Android Enterprise
titleSuffix: Microsoft Intune
description: Informazioni sulle restrizioni e le impostazioni consigliate per la sicurezza di base ed elevata dei dispositivi Android Enterprise.
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
ms.openlocfilehash: 3735a37d4572454968638d29ab2646d6fda943ad
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/04/2020
ms.locfileid: "87546587"
---
# <a name="android-enterprise-security-configuration-framework-app-configuration-policies"></a>Criteri di configurazione delle app del framework di configurazione della sicurezza di Android Enterprise

Come parte del [framework di configurazione della sicurezza di Android Enterprise](android-configuration-framework.md), è necessario impostare correttamente i criteri di configurazione delle app per i dispositivi Android Enterprise.

I dispositivi del profilo di lavoro Android Enterprise sono progettati per isolare i dati di lavoro e personali l'uno dall'altro. I dispositivi completamente gestiti Android Enterprise sono progettati solo per i dati aziendali o dell'Istituto di istruzione. Per questa ragione, le app Microsoft distribuite in questi dispositivi devono essere configurate in modo da non consentire gli account personali.

## <a name="disallow-personal-accounts-for-microsoft-apps-on-android-enterprise-devices"></a>Non consentire gli account personali per le app Microsoft nei dispositivi Android Enterprise

1. Aggiungere le app a Google Play gestito. Per altre informazioni, vedere [Aggiungere app di Google Play gestite a dispositivi Android Enterprise con Intune](../apps/apps-add-android-for-work.md).
2. Creare criteri per ogni app di Google Play gestito come descritto in [Aggiungere criteri di configurazione delle app per i dispositivi Android gestiti]().
3. Creare la chiave singola seguente in ogni criterio:

    | Chiave | Valori |
    | --- | --- |
    | com.microsoft.intune.mam.AllowedAccountUPNs | Uno o più valori; UPN delimitati.<br>Solo gli account consentiti sono gli account utente gestiti definiti da questa chiave.<br>Per i dispositivi registrati in Intune, è possibile usare il token {{userprincipalname}} per rappresentare l'account utente registrato. |


## <a name="next-steps"></a>Passaggi successivi
Applicare le [impostazioni di sicurezza del profilo di lavoro Android Enterprise](android-work-profile-security-settings.md) o le [impostazioni di sicurezza completamente gestite di Android Enterprise](android-fully-managed-security-settings.md).