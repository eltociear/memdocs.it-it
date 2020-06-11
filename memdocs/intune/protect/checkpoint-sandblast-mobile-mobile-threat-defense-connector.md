---
title: Configurare il connettore Check Point SandBlast MTD con Intune
titleSuffix: Microsoft Intune
description: Informazioni sull'integrazione di Intune con Check Point SandBlast Mobile Threat Defense per controllare l'accesso dei dispositivi mobili alle risorse aziendali.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 706a4228-9bdf-41e0-b8d1-64c923dd2d2b
ms.reviewer: davidra
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: a0645c771b304bfb4930f5cd365b9291366499b1
ms.sourcegitcommit: 42a4a4454e56fa681f0ad39f5e585492dfbad286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/03/2020
ms.locfileid: "84330917"
---
# <a name="check-point-sandblast-mobile-threat-defense-connector-with-intune"></a>Connettore Check Point SandBlast Mobile Threat Defense con Intune

È possibile controllare l'accesso dei dispositivi mobili alle risorse aziendali usando l'accesso condizionale in base alla valutazione dei rischi condotta da Check Point SandBlast Mobile, una soluzione di Mobile Threat Defense integrata in Microsoft Intune. La valutazione dei rischi viene eseguita in base ai dati di telemetria raccolti dai dispositivi che eseguono l'app Check Point SandBlast Mobile.

È possibile configurare criteri di accesso condizionale in base alla valutazione dei rischi di Check Point SandBlast Mobile abilitata tramite i criteri di conformità dei dispositivi di Intune, che possono essere usati per consentire o impedire ai dispositivi non conformi di accedere alle risorse aziendali a seconda delle minacce rilevate.

> [!NOTE]
> Questo fornitore di Mobile Threat Defense non è supportato per i dispositivi non registrati.

## <a name="supported-platforms"></a>Piattaforme supportate

- **Android 4.1 e versioni successive**

- **iOS 8 e versioni successive**

## <a name="pre-requisites"></a>Prerequisiti

- Azure Active Directory Premium

- Sottoscrizione di Microsoft Intune

- Sottoscrizione di Check Point SandBlast Mobile Threat Defense
  - Vedere il [sito Web di CheckPoint SandBlast](https://www.checkpoint.com/) per altre informazioni.

## <a name="how-do-intune-and-check-point-sandblast-mobile-help-protect-your-company-resources"></a>In che modo Intune e Check Point SandBlast Mobile consentono di proteggere le risorse aziendali?

L'app Check Point SandBlast Mobile per Android e iOS/iPadOS acquisisce, se disponibili, i dati di telemetria relativi al file system, allo stack di rete, al dispositivo e alle applicazioni e li invia al servizio cloud Check Point SandBlast per la valutazione del livello di rischio delle minacce per dispositivi mobili.

I criteri di conformità dei dispositivi di Intune includono una regola per Check Point SandBlast Mobile Threat Defense, basata sulla valutazione dei rischi eseguita da Check Point SandBlast. Quando questa regola è abilitata, Intune valuta la conformità del dispositivo in base ai criteri abilitati. Se il dispositivo risulta non conforme, l'accesso degli utenti a risorse aziendali come Exchange Online e SharePoint Online viene bloccato. Gli utenti ricevono inoltre istruzioni dall'app Check Point SandBlast Mobile installata nei relativi dispositivi per risolvere il problema e ottenere nuovamente l'accesso alle risorse aziendali.

Ecco alcuni scenari comuni:

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Controllare l'accesso in base alle minacce da parte di app dannose

Se nei dispositivi vengono rilevate app dannose, come malware, è possibile bloccare i dispositivi finché la condizione di minaccia non viene risolta:

- Connessione alla posta elettronica aziendale

- Sincronizzazione di file aziendali tramite l'app OneDrive for Work

- Accesso alle app aziendali

*Bloccare quando vengono rilevate app dannose:*

> [!div class="mx-imgBorder"]
> ![Blocco di Check Point MTD quando vengono rilevate app dannose](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-2.PNG)

*Accesso concesso dopo la correzione:*

> [!div class="mx-imgBorder"]
> ![Accesso a Check Point MTD concesso](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-3.PNG)

### <a name="control-access-based-on-threat-to-network"></a>Controllare l'accesso in base alle minacce per la rete

Rilevare minacce nella rete, come attacchi di tipo **Man-in-the-middle**, e proteggere l'accesso alle reti Wi-Fi in base al livello di rischio del dispositivo.

*Bloccare l'accesso alla rete tramite Wi-Fi:*

> [!div class="mx-imgBorder"]
> ![Blocco dell'accesso alla rete Check Point MTD tramite Wi-Fi](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-4.PNG)

*Accesso concesso dopo la correzione:*

> [!div class="mx-imgBorder"]
> ![Accesso alla rete Wi-Fi Check Point MTD concesso](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-5.PNG)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Controllare l'accesso a SharePoint Online in base alle minacce alla rete

Rilevare minacce nella rete, come attacchi di tipo **Man-in-the-middle**, e impedire la sincronizzazione dei file aziendali in base al livello di rischio del dispositivo.

*Bloccare SharePoint Online quando vengono rilevate minacce per la rete:*

> [!div class="mx-imgBorder"]
> ![Blocco di Check Point MTD dell'accesso a SharePoint Online](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-6.PNG)

*Accesso concesso dopo la correzione:*

> [!div class="mx-imgBorder"]
> ![Accesso di Check Point MTD a SharePoint Online concesso](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-7.PNG)

<!-- ### Control access on unenrolled devices based on threats from malicious apps

When the Check Point Sandblast Mobile Threat Defense solution considers a device to be infected:
> [!div class="mx-imgBorder"]
> ![App protection policy blocks due to detected malware](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/sandblast-app-policy-block.png)

Access is granted on remediation:

> [!div class="mx-imgBorder"]
> ![Access is granted on remediation for App protection policy](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/sandblast-app-policy-remediated.png)
-->

## <a name="next-steps"></a>Passaggi successivi

- [Integrare Check Point SandBlast con Intune](checkpoint-sandblast-mobile-mtd-connector-integration.md)

- [Configurare l'app Check Point SandBlast Mobile](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [Creare criteri di conformità per dispositivi CheckPoint SandBlast Mobile](mtd-device-compliance-policy-create.md)

- [Abilitare il connettore CheckPoint SandBlast Mobile MTD](mtd-connector-enable.md)
