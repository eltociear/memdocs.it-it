---
title: Usare Sophos Mobile con Intune
titleSuffix: Intune on Azure
description: Come usare la soluzione Sophos Mobile con Microsoft Intune per controllare l'accesso dei dispositivi mobili alle risorse aziendali.
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
ms.assetid: ''
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 285f323f55d41edab5ccd450deb0244b6fbda874
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "79526445"
---
# <a name="sophos-mobile-threat-defense-connector-with-intune"></a>Connettore Sophos Mobile Threat Defense con Intune
È possibile controllare l'accesso dei dispositivi mobili alle risorse aziendali usando l'accesso condizionale basato sulla valutazione dei rischi condotta da Sophos Mobile, una soluzione MTD (Mobile Threat Defense) integrata in Microsoft Intune. La valutazione dei rischi viene eseguita in base ai dati di telemetria raccolti dai dispositivi che eseguono l'app Sophos Mobile.
È possibile configurare criteri di accesso condizionale in base alla valutazione dei rischi di Sophos Mobile abilitata tramite i criteri di conformità dei dispositivi di Intune, che possono essere usati per consentire o impedire ai dispositivi non conformi di accedere alle risorse aziendali a seconda delle minacce rilevate.

> [!NOTE]
> Questo fornitore di Mobile Threat Defense non è supportato per i dispositivi non registrati.

## <a name="supported-platforms"></a>Piattaforme supportate

- Android 5.0 e versioni successive
- iOS 11.0 e versioni successive

## <a name="prerequisites"></a>Prerequisiti

- Azure Active Directory Premium
- Sottoscrizione di Microsoft Intune
- Sottoscrizione di Sophos Mobile Threat Defense

Per altre informazioni, vedere il [sito Web Sophos](https://www.sophos.com/products/mobile-control.aspx).

## <a name="how-do-intune-and-sophos-mobile-help-protect-your-company-resources"></a>In che modo Intune e Sophos Mobile consentono di proteggere le risorse aziendali?

L'app Sophos Mobile per Android e iOS/iPadOS acquisisce i dati di telemetria, se disponibili, relativi al file system, allo stack di rete, al dispositivo e alle applicazioni e li invia al servizio cloud Sophos Mobile per la valutazione del livello di rischio delle minacce per dispositivi mobili.

I criteri di conformità dei dispositivi di Intune includono una regola per Mobile Threat Defense, basata sulla valutazione dei rischi eseguita da Sophos Mobile. Quando questa regola è abilitata, Intune valuta la conformità del dispositivo in base ai criteri abilitati. Se il dispositivo risulta non conforme, l'accesso degli utenti a risorse aziendali come Exchange Online e SharePoint Online viene bloccato. Gli utenti ricevono inoltre istruzioni dall'app Sophos Mobile installata nei relativi dispositivi per risolvere il problema e ottenere nuovamente l'accesso alle risorse aziendali.  

## <a name="sample-scenarios"></a>Scenari di esempio

Ecco alcuni scenari comuni.

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Controllare l'accesso in base alle minacce da parte di app dannose

Se nei dispositivi vengono rilevate app dannose, come malware, è possibile impedire ai dispositivi di eseguire le azioni seguenti fino alla risoluzione della condizione di minaccia:

- Connessione alla posta elettronica aziendale
- Sincronizzazione di file aziendali tramite l'app OneDrive for Work
- Accesso alle app aziendali

*Bloccare quando vengono rilevate app dannose*:

![Immagine concettuale del rilevamento di app dannose](./media/sophos-mtd-connector/sophos-malicious-apps-blocked.png)  

*Accesso concesso dopo la correzione*:  
![Immagine concettuale dell'accesso concesso dopo la correzione](./media/sophos-mtd-connector/sophos-malicious-apps-unblocked.png)

### <a name="control-access-based-on-threat-to-network"></a>Controllare l'accesso in base alle minacce alla rete

Rilevare le minacce per la rete, ad esempio attacchi Man-in-the-middle, e proteggere l'accesso alle reti Wi-Fi in base al livello di rischio del dispositivo.  

*Bloccare l'accesso alla rete tramite Wi-Fi*:  
![Bloccare l'accesso alla rete tramite Wi-Fi](./media/sophos-mtd-connector/sophos-network-wifi-blocked.png)

*Accesso concesso dopo la correzione*:   
![Accesso concesso dopo la correzione](./media/sophos-mtd-connector/sophos-network-wifi-unblocked.png)  

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Controllare l'accesso a SharePoint Online in base alle minacce alla rete

Rilevare le minacce per la rete, ad esempio attacchi Man-in-the-middle, e impedire la sincronizzazione dei file aziendali in base al livello di rischio del dispositivo.  

*Bloccare SharePoint Online quando vengono rilevate minacce per la rete*:

![Bloccare SharePoint Online quando vengono rilevate minacce per la rete](./media/sophos-mtd-connector/sophos-network-spo-blocked.png)  

*Accesso concesso dopo la correzione*:

![Accesso concesso dopo la risoluzione per l'esempio di SharePoint](./media/sophos-mtd-connector/sophos-network-spo-unblocked.png)  

<!-- 
### Control access on unenrolled devices based on threats from malicious apps

When the Sophos Mobile Threat Defense solution considers a device to be infected:

![App protection policy blocks due to detected malware](./media/sophos-mtd-connector/sophos-mobile-app-policy-block.png)

Access is granted on remediation:

![Access is granted on remediation for App protection policy](./media/sophos-mtd-connector/sophos-mobile-app-policy-remediated.png)
-->

## <a name="next-steps"></a>Passaggi successivi

- [Integrare Sophos Mobile con Intune](sophos-mtd-connector-integration.md)
- [Configurare le app Sophos](mtd-apps-ios-app-configuration-policy-add-assign.md)
- [Creare criteri di conformità dei dispositivi Sophos](mtd-device-compliance-policy-create.md)
- [Abilitare il connettore Sophos MTD](mtd-connector-enable.md)
