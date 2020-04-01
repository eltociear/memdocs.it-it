---
title: Connettore Symantec con Microsoft Intune
titleSuffix: Microsoft Intune
description: Informazioni sull'integrazione di Intune con Symantec Endpoint Protection Mobile per controllare l'accesso dei dispositivi mobili alle risorse aziendali.
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
ms.assetid: df4ce3f6-a093-432c-ab86-7a83865e389e
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d6f8f3cf9ced5b613323093ed2baafcf65667997
ms.sourcegitcommit: fe7484e86ec8a109fa5f54fe9cceef8aac94bd9f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/26/2020
ms.locfileid: "80275085"
---
# <a name="symantec-endpoint-protection-mobile-connector"></a>Connettore Symantec Endpoint Protection Mobile

È possibile controllare l'accesso dei dispositivi mobili alle risorse aziendali usando l'accesso condizionale in base alla valutazione dei rischi condotta da Symantec Endpoint Protection Mobile (SEP Mobile), una soluzione di Mobile Threat Defense integrata in Microsoft Intune. La valutazione dei rischi viene effettuata in base ai dati di telemetria raccolti dai dispositivi che eseguono SEP Mobile, inclusi i seguenti:

- Difesa fisica

- Difesa della rete

- Difesa delle applicazioni

- Difesa delle vulnerabilità

È possibile abilitare la valutazione dei rischi di SEP Mobile tramite i criteri di conformità dei dispositivi di Intune e quindi usare i criteri di accesso condizionale per consentire o impedire l'accesso dei dispositivi non conformi alle risorse aziendali a seconda delle minacce rilevate.

> [!NOTE]
> Questo fornitore di Mobile Threat Defense non è supportato per i dispositivi non registrati.

## <a name="supported-platforms"></a>Piattaforme supportate

- **Android 4.1 e versioni successive**

- **iOS 8 e versioni successive**

## <a name="pre-requisites"></a>Prerequisiti

- Azure Active Directory Premium

- Sottoscrizione di Microsoft Intune

- Sottoscrizione di Symantec Endpoint Protection Mobile

Per altre informazioni, visitare il [sito Web di Symantec](https://help.symantec.com/cs/sep_mobile/SEPMOBILE/v131237277_v127904070/Integrating-Microsoft-Intune-with-Endpoint-Protection-Mobile?locale=EN_US).

## <a name="how-do-intune-and-sep-mobile-help-protect-your-company-resources"></a>In che modo Intune e SEP Mobile consentono di proteggere le risorse aziendali?

L'app SEP Mobile per Android o iOS/iPadOS acquisisce, se disponibili, i dati di telemetria relativi al file system, allo stack di rete, al dispositivo e alle applicazioni e li invia al servizio cloud SEP Mobile per la valutazione del livello di rischio delle minacce per dispositivi mobili.

I criteri di conformità dei dispositivi di Intune includono una regola per SEP Mobile, basata sulla valutazione dei rischi eseguita da SEP Mobile. Quando questa regola è abilitata, Intune valuta la conformità del dispositivo in base ai criteri abilitati.

Se il dispositivo risulta non conforme, l'accesso a risorse come Exchange Online e SharePoint Online viene bloccato. Gli utenti di dispositivi bloccati riceveranno istruzioni dall'app SEP Mobile per dispositivi mobili per risolvere il problema e ottenere nuovamente l'accesso alle risorse aziendali.

Intune supporta due modalità di integrazione con SEP Mobile:

- **Installazione di base**, una modalità di sola lettura che consente la visibilità di SEP Mobile per i dispositivi in Intune.

- **Integrazione completa**, una modalità che consente a SEP Mobile di segnalare a Intune i dettagli relativi ai rischi dei dispositivi e agli eventi imprevisti per la sicurezza.

## <a name="sample-scenarios"></a>Scenari di esempio

Ecco alcuni scenari comuni:

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Controllare l'accesso in base alle minacce da parte di app dannose

Se nei dispositivi vengono rilevate app dannose, come malware, è possibile bloccare i dispositivi finché la condizione di minaccia non viene risolta:

- Connessione alla posta elettronica aziendale

- Sincronizzazione di file aziendali tramite l'app OneDrive for Work

- Accesso alle app aziendali

*Bloccare quando vengono rilevate app dannose:*

![Immagine concettuale del rilevamento di app dannose](./media/skycure-mobile-threat-defense-connector/symantec-arch-1.png)

*Accesso concesso dopo la correzione:*

![Immagine dell'accesso concesso in caso di correzione dopo il rilevamento di app dannose](./media/skycure-mobile-threat-defense-connector/symantec-arch-2.png)

### <a name="control-access-based-on-threat-to-network"></a>Controllare l'accesso in base alle minacce per la rete

Rilevare minacce nella rete, come attacchi di tipo **Man-in-the-middle**, e proteggere l'accesso alle reti Wi-Fi in base al livello di rischio del dispositivo.

*Bloccare l'accesso alla rete tramite Wi-Fi:*

![Bloccare l'accesso alla rete tramite Wi-Fi](./media/skycure-mobile-threat-defense-connector/symantec-arch-3.png)

*Accesso concesso dopo la correzione:*

![Accesso concesso dopo la risoluzione](./media/skycure-mobile-threat-defense-connector/symantec-arch-4.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Controllare l'accesso a SharePoint Online in base alle minacce alla rete

Rilevare minacce nella rete, come attacchi di tipo **Man-in-the-middle**, e impedire la sincronizzazione dei file aziendali in base al livello di rischio del dispositivo.

*Bloccare SharePoint Online quando vengono rilevate minacce per la rete:*

![Bloccare SharePoint Online quando vengono rilevate minacce per la rete](./media/skycure-mobile-threat-defense-connector/symantec-arch-5.png)

*Accesso concesso dopo la correzione:*

![Accesso concesso dopo la risoluzione per l'esempio di SharePoint](./media/skycure-mobile-threat-defense-connector/symantec-arch-6.png)

<!-- 
### Control access on unenrolled devices based on threats from malicious apps

When the Symantec Endpoint Protection Mobile Threat Defense solution considers a device to be infected:
![App protection policy blocks due to detected malware](./media/skycure-mobile-threat-defense-connector/symantec-app-policy-block.png)

Access is granted on remediation:

![Access is granted on remediation for App protection policy](./media/skycure-mobile-threat-defense-connector/symantec-app-policy-remediated.png)
-->

## <a name="next-steps"></a>Passaggi successivi

Questi sono i passaggi da completare per integrare Intune con SEP Mobile:

- [Configurare l'integrazione di SEP Mobile con Intune](skycure-mtd-connector-integration.md)

- [Aggiungere e assegnare app SEP Mobile, Microsoft Authenticator e criteri di configurazione delle app iOS/iPadOS](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [Creare criteri di conformità dei dispositivi SEP Mobile con Intune](mtd-device-compliance-policy-create.md)

- [Abilitare SEP Mobile MTD in Intune](mtd-connector-enable.md)
