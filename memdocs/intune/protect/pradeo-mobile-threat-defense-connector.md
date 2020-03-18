---
title: Connettore Mobile Threat Defense Pradeo con Intune
titleSuffix: Intune on Azure
description: Informazioni su come integrare Intune con il connettore Pradeo Mobile Threat Defense per controllare l'accesso dei dispositivi mobili alle risorse aziendali.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/09/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: cde4d389-1770-4226-85a3-a2f3b3fb92a3
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: a23155c31586992c82781998bb664bf2ce6a0889
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79339176"
---
# <a name="pradeo-mobile-threat-defense-connector-with-intune"></a>Connettore Mobile Threat Defense Pradeo con Intune

È possibile controllare l'accesso dei dispositivi mobili alle risorse aziendali usando l'accesso condizionale basato sulla valutazione dei rischi condotta da Pradeo, una soluzione Mobile Threat Defense (MTD) integrata in Microsoft Intune. La valutazione dei rischi viene eseguita in base ai dati di telemetria raccolti dai dispositivi che eseguono l'app Pradeo.

È possibile configurare criteri di accesso condizionale in base alla valutazione dei rischi di Pradeo abilitata tramite i criteri di conformità dei dispositivi di Intune, che possono essere usati per consentire o impedire ai dispositivi non conformi di accedere alle risorse aziendali a seconda delle minacce rilevate.

> [!NOTE]
> Questo fornitore di Mobile Threat Defense non è supportato per i dispositivi non registrati.

## <a name="supported-platforms"></a>Piattaforme supportate

- **Android 4.0.3 e versioni successive**

- **iOS 7 e versioni successive**

## <a name="prerequisites"></a>Prerequisiti

- Azure Active Directory Premium

- Sottoscrizione di Microsoft Intune

- Sottoscrizione di Pradeo Security Mobile Threat Defense

  - Per altre informazioni, vedere il [sito Web Pradeo](https://www.pradeo.com/en-US/mobile-threat-protection).

## <a name="how-do-intune-and-pradeo-help-protect-your-company-resources"></a>In che modo Intune e Pradeo consentono di proteggere le risorse aziendali?

L'app Pradeo per Android e iOS/iPadOS acquisisce i dati di telemetria, se disponibili, relativi al file system, allo stack di rete, al dispositivo e alle applicazioni e li invia al servizio cloud Pradeo per la valutazione del livello di rischio delle minacce per dispositivi mobili.

I criteri di conformità dei dispositivi di Intune includono una regola per Pradeo Mobile Threat Defense, basata sulla valutazione dei rischi eseguita da Pradeo. Quando questa regola è abilitata, Intune valuta la conformità del dispositivo in base ai criteri abilitati. Se il dispositivo risulta non conforme, l'accesso degli utenti a risorse aziendali come Exchange Online e SharePoint Online viene bloccato. Gli utenti ricevono inoltre istruzioni dall'app Pradeo installata nei relativi dispositivi per risolvere il problema e ottenere nuovamente l'accesso alle risorse aziendali.

## <a name="sample-scenarios"></a>Scenari di esempio

Ecco alcuni scenari comuni.

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Controllare l'accesso in base alle minacce da parte di app dannose

Se nei dispositivi vengono rilevate app dannose, come malware, è possibile impedire ai dispositivi di eseguire le azioni seguenti fino alla risoluzione della condizione di minaccia:

- Connessione alla posta elettronica aziendale

- Sincronizzazione di file aziendali tramite l'app OneDrive for Work

- Accesso alle app aziendali

*Bloccare quando vengono rilevate app dannose:*

![Immagine concettuale del rilevamento di app dannose](./media/pradeo-mobile-threat-defense-connector/pradeo-maliciousapps-blocked.png)

*Accesso concesso dopo la correzione:*

![App dannose rilevate e accesso consentito](./media/pradeo-mobile-threat-defense-connector/pradeo-maliciousapps-unblocked.png)

### <a name="control-access-based-on-threat-to-network"></a>Controllare l'accesso in base alle minacce per la rete

Rilevare le minacce per la rete, ad esempio attacchi **Man-in-the-middle** e proteggere l'accesso alle reti Wi-Fi in base al livello di rischio del dispositivo.

*Bloccare l'accesso alla rete tramite Wi-Fi:*

![Bloccare l'accesso alla rete tramite Wi-Fi](./media/pradeo-mobile-threat-defense-connector/pradeo-network-wifi-blocked.png)

*Accesso concesso dopo la correzione:*

![Immagine concettuale dell'accesso concesso dopo la correzione](./media/pradeo-mobile-threat-defense-connector/pradeo-network-wifi-unblocked.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Controllare l'accesso a SharePoint Online in base alle minacce alla rete

Rilevare le minacce per la rete, ad esempio attacchi **Man-in-the-middle**, e impedire la sincronizzazione dei file aziendali in base al livello di rischio del dispositivo.

*Bloccare SharePoint Online quando vengono rilevate minacce per la rete:*

![Bloccare SharePoint Online quando vengono rilevate minacce per la rete](./media/pradeo-mobile-threat-defense-connector/pradeo-network-spo-blocked.png)

*Accesso concesso dopo la correzione:*

![Immagine concettuale dell'accesso concesso dopo la correzione per l'esempio di SharePoint](./media/pradeo-mobile-threat-defense-connector/pradeo-network-spo-unblocked.png)

<!-- 
### Control access on unenrolled devices based on threats from malicious apps

When the Pradeo Mobile Threat Defense solution considers a device to be infected:

![App protection policy blocks due to detected malware](./media/pradeo-mobile-threat-defense-connector/pradeo-app-policy-block.png)

Access is granted on remediation:

![Access is granted on remediation for App protection policy](./media/pradeo-mobile-threat-defense-connector/pradeo-app-policy-remediated.png)
-->

## <a name="next-steps"></a>Passaggi successivi

- [Integrare Pradeo con Intune](pradeo-mtd-connector-integration.md)

- [Configurare app Pradeo](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [Creare criteri di conformità per dispositivi Pradeo](mtd-device-compliance-policy-create.md)

- [Abilitare il connettore MTD Pradeo](mtd-connector-enable.md)
