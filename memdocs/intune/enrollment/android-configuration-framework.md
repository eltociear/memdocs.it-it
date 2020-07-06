---
title: Framework di configurazione della sicurezza di Android Enterprise
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
ms.openlocfilehash: 6f0e4452f5209d569e11a782528582f4d5a76045
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/27/2020
ms.locfileid: "85502978"
---
# <a name="android-enterprise-security-configuration-framework"></a>Framework di configurazione della sicurezza di Android Enterprise

Il framework di configurazione della sicurezza di Android Enterprise include una serie di consigli per la conformità dei dispositivi e le impostazioni dei criteri di configurazione. Questi consigli consentono di adattare la protezione della sicurezza dei dispositivi mobili dell'organizzazione alle esigenze specifiche.

Le organizzazioni che si occupano della sicurezza esaminano i modi per garantire la protezione dei dati aziendali sui dispositivi mobili. Un metodo usato per proteggere i dati è la registrazione dei dispositivi. La registrazione dei dispositivi consente alle organizzazioni di:
- distribuire i criteri di conformità, ad esempio la complessità del PIN, la convalida jailbreak/radice e così via.
- distribuire i criteri di configurazione, ad esempio Wi-Fi, certificati, VPN.
- gestire Il ciclo di vita dell'app.

Per consentire la configurazione di uno scenario di sicurezza completo, Microsoft ha introdotto una nuova tassonomia per le [configurazioni di sicurezza in Windows 10](https://aka.ms/secconframework). Intune usa una tassonomia simile per il framework di configurazione della sicurezza di Android Enterprise. Sono incluse le impostazioni consigliate per la conformità dei dispositivi e le restrizioni dei dispositivi per la sicurezza di base, avanzata ed elevata. Questa tassonomia è descritta negli articoli seguenti:

1. [Metodologia di distribuzione del framework di Android Enterprise](framework-deployment-methodology.md): metodologia consigliata per la distribuzione del framework di configurazione della sicurezza.
2. [Restrizioni di registrazione dei dispositivi Android](device-enrollment-restrictions.md): restrizioni dei dispositivi di pre-registrazione per i dispositivi Android Enterprise.
3. [Impostare i criteri di configurazione delle app per i dispositivi Android Enterprise](android-app-configuration-policies.md): configurare le app nei dispositivi per non consentire gli account personali.
4. [Impostazioni di sicurezza del profilo di lavoro Android](android-work-profile-security-settings.md): impostazioni di configurazione specifiche per la sicurezza di base ed elevata nei dispositivi del profilo di lavoro.
5. [Impostazioni di sicurezza di dispositivi Android Enterprise completamente gestiti](android-fully-managed-security-settings.md): impostazioni di configurazione specifiche per la sicurezza di base, avanzata ed elevata nei dispositivi completamente gestiti.

## <a name="android-enterprise-enrollment-modes"></a>Modalità di registrazione di Android Enterprise

Con Android 5.0, Google ha introdotto Android Enterprise che include due modalità di registrazione. Il framework di configurazione della sicurezza di Android Enterprise offre consigli per entrambe le modalità.
- [Dispositivi completamente gestiti (proprietario del dispositivo)](android-fully-managed-enroll.md): per i dispositivi di proprietà dell'azienda associati a un singolo utente. Questi dispositivi sono destinati esclusivamente a un uso professionale e non personale.
- [Profilo di lavoro (proprietario del dispositivo)](android-work-profile-enroll.md): in genere, per i dispositivi di proprietà personale in cui è richiesto un limite chiaro tra i dati personali e di lavoro. I criteri controllati dal reparto IT assicurano che i dati di lavoro non possano essere trasferiti nel profilo personale.


## <a name="next-steps"></a>Passaggi successivi

[Metodologia di distribuzione del framework di Android Enterprise](framework-deployment-methodology.md)