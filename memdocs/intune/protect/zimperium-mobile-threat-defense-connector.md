---
title: Connettore Zimperium MTD con Intune
titleSuffix: Intune on Azure
description: Informazioni sull'integrazione di Intune con Zimperium Mobile Threat Defense per controllare l'accesso dei dispositivi mobili alle risorse aziendali.
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
ms.assetid: 975d8d84-792a-41ad-925a-4a7f1ae4dcaf
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b443f922b31523ec6f27971648ba1ea9c5123867
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989390"
---
# <a name="zimperium-mobile-threat-defense-connector-with-intune"></a>Connettore Zimperium Mobile Threat Defense con Intune

È possibile controllare l'accesso dei dispositivi mobili alle risorse aziendali usando l'accesso condizionale basato sulla valutazione dei rischi condotta da Zimperium, una soluzione Mobile Threat Defense (MTD) integrata in Microsoft Intune. La valutazione dei rischi viene eseguita in base ai dati di telemetria raccolti dai dispositivi che eseguono l'app Zimperium.

È possibile configurare criteri di accesso condizionale basati sulla valutazione dei rischi di Zimperium abilitata con i criteri di conformità dei dispositivi di Intune per i dispositivi registrati, che possono essere usati per consentire o impedire ai dispositivi non conformi di accedere alle risorse aziendali a seconda delle minacce rilevate. Per i dispositivi non registrati, è possibile usare i criteri di protezione delle app per applicare un blocco o una cancellazione selettiva in base alle minacce rilevate.

## <a name="supported-platforms"></a>Piattaforme supportate

- **Android 4.1 e versioni successive**

- **iOS 8 e versioni successive**

## <a name="prerequisites"></a>Prerequisiti

- Azure Active Directory Premium

- Sottoscrizione di Microsoft Intune

- Sottoscrizione di Zimperium Mobile Threat Defense

  - Per altre informazioni, vedere il [sito Web di Zimperium](https://www.zimperium.com/zips-mobile-ips).

## <a name="how-do-intune-and-zimperium-help-protect-your-company-resources"></a>In che modo Intune e Zimperium consentono di proteggere le risorse aziendali?

L'app Zimperium per Android e iOS/iPadOS acquisisce i dati di telemetria, se disponibili, relativi al file system, allo stack di rete, al dispositivo e alle applicazioni e li invia al servizio cloud Zimperium per la valutazione del livello di rischio delle minacce per dispositivi mobili.

- **Supporto per i dispositivi registrati**: i criteri di conformità dei dispositivi di Intune includono una regola per Mobile Threat Defense (MTD), che può usare le informazioni di valutazione dei rischi di Zimperium. Quando la regola per MTD è abilitata, Intune valuta la conformità del dispositivo in base ai criteri abilitati. Se il dispositivo risulta non conforme, l'accesso degli utenti a risorse aziendali come Exchange Online e SharePoint Online viene bloccato. Gli utenti ricevono inoltre istruzioni dall'app Zimperium installata nei relativi dispositivi per risolvere il problema e ottenere nuovamente l'accesso alle risorse aziendali. Per supportare l'uso di Zimperium con i dispositivi registrati:
  - [Aggiungere app MTD ai dispositivi](../protect/mtd-apps-ios-app-configuration-policy-add-assign.md)
  - [Creare criteri di conformità dei dispositivi che supportano MTD](../protect/mtd-device-compliance-policy-create.md)
  - [Abilitare il connettore MTD in Intune](../protect/mtd-connector-enable.md)

- **Supporto per i dispositivi non registrati**: Intune può usare i dati di valutazione dei rischi dell'app Zimperium nei dispositivi non registrati quando si usano i criteri di protezione delle app di Intune. Gli amministratori possono usare questa combinazione per proteggere i dati aziendali all'interno di un'[app protetta da Microsoft Intune](../apps/apps-supported-intune-apps.md), nonché eseguire un blocco o una cancellazione selettiva per i dati aziendali nei dispositivi non registrati. Per supportare l'uso di Zimperium con dispositivi non registrati:
  - [Aggiungere l'app MTD ai dispositivi non registrati](../protect/mtd-add-apps-unenrolled-devices.md)
  - [Creare criteri di protezione dell'app Mobile Threat Defense](../protect/mtd-app-protection-policy.md)
  - [Abilitare il connettore MTD in Intune per i dispositivi non registrati](../protect/mtd-enable-unenrolled-devices.md)
  
## <a name="sample-scenarios"></a>Scenari di esempio

Di seguito sono riportati alcuni scenari in cui Zimperium viene integrato in Intune:

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Controllare l'accesso in base alle minacce da parte di app dannose

Se nei dispositivi vengono rilevate app dannose, come malware, è possibile bloccare i dispositivi finché la condizione di minaccia non viene risolta:

- Connessione alla posta elettronica aziendale

- Sincronizzazione di file aziendali tramite l'app OneDrive for Work

- Accesso alle app aziendali

*Bloccare quando vengono rilevate app dannose:*

> [!div class="mx-imgBorder"]
> ![Immagine concettuale del rilevamento di app dannose](./media/zimperium-mobile-threat-defense-connector/Maliciousapps-blocked-zimperium.png)

*Accesso concesso dopo la correzione:*

> [!div class="mx-imgBorder"]
> ![Immagine concettuale dell'accesso concesso dopo la correzione](./media/zimperium-mobile-threat-defense-connector/maliciousapps-unblocked-zimperium.png)

### <a name="control-access-based-on-threat-to-network"></a>Controllare l'accesso in base alle minacce alla rete

Rilevare minacce nella rete, come attacchi di tipo **Man-in-the-middle**, e proteggere l'accesso alle reti Wi-Fi in base al livello di rischio del dispositivo.

*Bloccare l'accesso alla rete tramite Wi-Fi:*

> [!div class="mx-imgBorder"]
> ![Bloccare l'accesso alla rete tramite Wi-Fi](./media/zimperium-mobile-threat-defense-connector/network-wifi-blocked-zimperium.png)

*Accesso concesso dopo la correzione:*

> [!div class="mx-imgBorder"]
> ![Accesso concesso dopo la correzione](./media/zimperium-mobile-threat-defense-connector/network-wifi-unblocked-zimperium.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Controllare l'accesso a SharePoint Online in base alle minacce alla rete

Rilevare minacce nella rete, come attacchi di tipo **Man-in-the-middle**, e impedire la sincronizzazione dei file aziendali in base al livello di rischio del dispositivo.

*Bloccare SharePoint Online quando vengono rilevate minacce per la rete:*

> [!div class="mx-imgBorder"]
> ![Bloccare SharePoint Online quando vengono rilevate minacce per la rete](./media/zimperium-mobile-threat-defense-connector/network-spo-blocked-zimperium.png)

*Accesso concesso dopo la correzione:*

> [!div class="mx-imgBorder"]
> ![Accesso concesso dopo la risoluzione per l'esempio di SharePoint](./media/zimperium-mobile-threat-defense-connector/network-spo-unblocked-zimperium.png)

### <a name="control-access-on-unenrolled-devices-based-on-threats-from-malicious-apps"></a>Controllare l'accesso nei dispositivi non registrati in base alle minacce da parte di app dannose

Quando la soluzione Zimperium Mobile Threat Defense considera un dispositivo infetto:

> [!div class="mx-imgBorder"]
> ![I criteri di protezione delle app eseguono il blocco a causa del malware rilevato](./media/zimperium-mobile-threat-defense-connector/zimperium-mobile-app-policy-block.png)

L'accesso viene concesso dopo la correzione:

> [!div class="mx-imgBorder"]
> ![L'accesso viene concesso dopo la correzione per i criteri di protezione delle app](./media/zimperium-mobile-threat-defense-connector/zimperium-mobile-app-policy-remediated.png)

## <a name="next-steps"></a>Passaggi successivi

- [Integrare Zimperium con Intune](zimperium-mtd-connector-integration.md)

- [Configurare le app di Zimperium](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [Creare criteri di conformità dei dispositivi di Zimperium](mtd-device-compliance-policy-create.md)

- [Abilitare il connettore Zimperium MTD](mtd-connector-enable.md)

- [Creare un criterio di protezione delle app MTD](../protect/mtd-app-protection-policy.md)
