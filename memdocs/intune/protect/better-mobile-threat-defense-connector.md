---
title: Connettore Better Mobile Threat Defense con Intune
titleSuffix: Intune on Azure
description: Configurare il connettore Better Mobile Threat Defense con Intune.
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
ms.assetid: ''
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: beb1f8c287e952726c0ba929b49496c16599fe08
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990430"
---
# <a name="better-mobile-threat-defense-connector-with-intune"></a>Connettore Better Mobile Threat Defense con Intune

È possibile controllare l'accesso dei dispositivi mobili alle risorse aziendali usando l'accesso condizionale basato sulla valutazione dei rischi condotta da Better Mobile, una soluzione Mobile Threat Defense (MTD) integrata in Microsoft Intune. La valutazione dei rischi viene eseguita in base ai dati di telemetria raccolti dai dispositivi che eseguono l'app Better Mobile.

È possibile configurare criteri di accesso condizionale in base alla valutazione dei rischi di Better Mobile abilitata tramite i criteri di conformità dei dispositivi di Intune per i dispositivi registrati, che possono essere usati per consentire o impedire ai dispositivi non conformi di accedere alle risorse aziendali a seconda delle minacce rilevate. Per i dispositivi non registrati, è possibile usare i criteri di protezione delle app per applicare un blocco o una cancellazione selettiva in base alle minacce rilevate.

## <a name="how-do-intune-and-better-mobile-help-protect-your-company-resources"></a>In che modo Intune e Better Mobile consentono di proteggere le risorse aziendali?

L'app Better Mobile viene installata ed eseguita nei dispositivi mobili. Questa app consente di acquisire dati di telemetria per il file system, lo stack di rete, il dispositivo e le applicazioni (se disponibili) e di inviarli al servizio cloud Better Mobile per la valutazione del livello di rischio per le minacce per dispositivi mobili.

- **Supporto per i dispositivi registrati** - I criteri di conformità dei dispositivi di Intune includono una regola per Mobile Threat Defense (MTD), che può usare le informazioni di valutazione dei rischi di Better Mobile. Quando la regola per MTD è abilitata, Intune valuta la conformità del dispositivo in base ai criteri abilitati. Se il dispositivo risulta non conforme, l'accesso degli utenti a risorse aziendali come Exchange Online e SharePoint Online viene bloccato. Gli utenti ricevono inoltre istruzioni dall'app Better Mobile installata nei relativi dispositivi per risolvere il problema e ottenere nuovamente l'accesso alle risorse aziendali. Per supportare l'uso di Better Mobile con i dispositivi registrati:
  - [Aggiungere app MTD ai dispositivi](../protect/mtd-apps-ios-app-configuration-policy-add-assign.md)
  - [Creare criteri di conformità dei dispositivi che supportano MTD](../protect/mtd-device-compliance-policy-create.md)
  - [Abilitare il connettore MTD in Intune](../protect/mtd-connector-enable.md)

- **Supporto per i dispositivi non registrati**: Intune può usare i dati di valutazione dei rischi dell'app Better Mobile nei dispositivi non registrati quando si usano i criteri di protezione delle app di Intune. Gli amministratori possono usare questa combinazione per proteggere i dati aziendali all'interno di un'[app protetta da Microsoft Intune](../apps/apps-supported-intune-apps.md), nonché eseguire un blocco o una cancellazione selettiva per i dati aziendali nei dispositivi non registrati. Per supportare l'uso di Better Mobile con dispositivi non registrati:
  - [Aggiungere l'app MTD ai dispositivi non registrati](../protect/mtd-add-apps-unenrolled-devices.md)
  - [Creare criteri di protezione dell'app Mobile Threat Defense](../protect/mtd-app-protection-policy.md)
  - [Abilitare il connettore MTD in Intune per i dispositivi non registrati](../protect/mtd-enable-unenrolled-devices.md)

## <a name="supported-platforms"></a>Piattaforme supportate

- **Android 4.1 e versioni successive**

- **iOS 8.0 e versioni successive**

## <a name="prerequisites"></a>Prerequisiti

- Azure Active Directory Premium

- Sottoscrizione di Microsoft Intune

- Sottoscrizione di Better Mobile Threat Defense

  - Per altre informazioni, vedere il [sito Web Better Mobile](https://www.better.mobi/).

## <a name="sample-scenarios"></a>Scenari di esempio

Ecco alcuni scenari comuni.

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Controllare l'accesso in base alle minacce da parte di app dannose

Se nei dispositivi vengono rilevate app dannose, come malware, è possibile impedire ai dispositivi di eseguire le azioni seguenti fino alla risoluzione della condizione di minaccia:

- Connessione alla posta elettronica aziendale

- Sincronizzazione di file aziendali tramite l'app OneDrive for Work

- Accesso alle app aziendali

Bloccare quando vengono rilevate app dannose:

![Immagine che illustra il rilevamento di app dannose](./media/better-mobile-threat-defense-connector/better-mobile-maliciousapps-blocked.png)

L'accesso viene concesso dopo la correzione:

![App dannose rilevate e accesso consentito](./media/better-mobile-threat-defense-connector/better-mobile-maliciousapps-unblocked.png)

### <a name="control-access-based-on-threat-to-network"></a>Controllare l'accesso in base alle minacce per la rete

Rilevare le minacce per la rete, ad esempio attacchi **Man-in-the-middle** e proteggere l'accesso alle reti Wi-Fi in base al livello di rischio del dispositivo.

Bloccare l'accesso alla rete tramite Wi-Fi:

![Bloccare l'accesso alla rete tramite Wi-Fi](./media/better-mobile-threat-defense-connector/better-mobile-network-wifi-blocked.png)

L'accesso viene concesso dopo la correzione:

![Immagine che illustra la concessione dell'accesso dopo la correzione](./media/better-mobile-threat-defense-connector/better-mobile-network-wifi-unblocked.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Controllare l'accesso a SharePoint Online in base alle minacce alla rete

Rilevare le minacce per la rete, ad esempio attacchi **Man-in-the-middle**, e impedire la sincronizzazione dei file aziendali in base al livello di rischio del dispositivo.

Bloccare SharePoint Online quando vengono rilevate minacce per la rete:

![Bloccare SharePoint Online quando vengono rilevate minacce per la rete](./media/better-mobile-threat-defense-connector/better-mobile-network-spo-blocked.png)

Accesso concesso dopo la risoluzione:

![Accesso concesso dopo la risoluzione per l'esempio di SharePoint](./media/better-mobile-threat-defense-connector/better-mobile-network-spo-unblocked.png)

### <a name="control--access-on-unenrolled-devices-based-on-threats-from-malicious-apps"></a>Controllare l'accesso nei dispositivi non registrati in base alle minacce da parte di app dannose

Quando la soluzione Better Mobile Threat Defense considera un dispositivo infetto: ![I criteri di protezione delle app eseguono il blocco a causa del malware rilevato](./media/better-mobile-threat-defense-connector/better-mobile-app-policy-block.png)

L'accesso viene concesso dopo la correzione:

![L'accesso viene concesso dopo la correzione per i criteri di protezione delle app](./media/better-mobile-threat-defense-connector/better-mobile-app-policy-remediated.png)

## <a name="next-steps"></a>Passaggi successivi

- [Integrare Better Mobile con Intune](better-mobile-mtd-connector-integration.md)

- [Configurare le app di Better Mobile](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [Creare criteri di conformità dei dispositivi Better Mobile](mtd-device-compliance-policy-create.md)

- [Abilitare il connettore Better Mobile MTD](mtd-connector-enable.md)

- [Creare un criterio di protezione delle app MTD](mtd-app-protection-policy.md) 
