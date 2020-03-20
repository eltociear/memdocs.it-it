---
title: Connettore Lookout MTD con Microsoft Intune
titleSuffix: Microsoft Intune
description: Informazioni sull'integrazione di Intune con Lookout Mobile Threat Defense (MTD) per controllare l'accesso dei dispositivi mobili alle risorse aziendali.
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
ms.assetid: 3a730a5d-2a90-42b0-aa28-aadfc7a18788
ms.reviewer: davera
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1b3927f09bb74f9058b19dad7f2f3b72f21a0d43
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79351929"
---
# <a name="lookout-mobile-endpoint-security-connector-with-intune"></a>Connettore Lookout Mobile Endpoint Security con Intune

È possibile controllare l'accesso dai dispositivi mobili alle risorse aziendali in base alla valutazione dei rischi condotta da Lookout, una soluzione di protezione dalle minacce per dispositivi mobili integrata in Microsoft Intune. La valutazione dei rischi viene effettuata in base ai dati di telemetria raccolti dai dispositivi dal servizio Lookout, che includono:

- Vulnerabilità del sistema operativo
- Installazione di app dannose
- Profili di rete dannosi

È possibile configurare criteri di accesso condizionale basati sulla valutazione dei rischi di Lookout abilitata con i criteri di conformità di Intune per i dispositivi registrati, che possono essere usati per consentire o impedire ai dispositivi non conformi di accedere alle risorse aziendali a seconda delle minacce rilevate. Per i dispositivi non registrati, è possibile usare i criteri di protezione delle app per applicare un blocco o una cancellazione selettiva in base alle minacce rilevate.

## <a name="how-do-intune-and-lookout-mobile-endpoint-security-help-protect-company-resources"></a>In che modo Intune e Lookout Mobile Endpoint Security possono proteggere le risorse aziendali?

L'app per dispositivi mobili di Lookout, **Lookout for Work**, viene installata ed eseguita nei dispositivi mobili. Questa app consente di acquisire dati di telemetria per il file system, lo stack di rete, il dispositivo e le applicazioni (se disponibili) e di inviarli al servizio cloud Lookout per la valutazione del livello di rischio per le minacce per dispositivi mobili. È possibile modificare le classificazioni del livello di rischio per le minacce nella console di Lookout in base alle proprie esigenze.

- **Supporto per i dispositivi registrati**: i criteri di conformità dei dispositivi di Intune includono una regola per Mobile Threat Defense (MTD), che può usare le informazioni di valutazione dei rischi di Lookout for Work. Quando la regola per MTD è abilitata, Intune valuta la conformità del dispositivo in base ai criteri abilitati. Se il dispositivo risulta non conforme, l'accesso degli utenti a risorse aziendali come Exchange Online e SharePoint Online viene bloccato. Gli utenti ricevono inoltre istruzioni dall'app Lookout for Work installata nei relativi dispositivi per risolvere il problema e ottenere nuovamente l'accesso alle risorse aziendali. Per supportare l'uso di Lookout for Work con i dispositivi registrati:
  - [Aggiungere app MTD ai dispositivi](../protect/mtd-apps-ios-app-configuration-policy-add-assign.md)
  - [Creare criteri di conformità dei dispositivi che supportano MTD](../protect/mtd-device-compliance-policy-create.md)
  - [Abilitare il connettore MTD in Intune](../protect/mtd-connector-enable.md)

- **Supporto per i dispositivi non registrati**: Intune può usare i dati di valutazione dei rischi dell'app Lookout for Work nei dispositivi non registrati quando si usano i criteri di protezione delle app di Intune. Gli amministratori possono usare questa combinazione per proteggere i dati aziendali all'interno di un'[app protetta da Microsoft Intune](../apps/apps-supported-intune-apps.md), nonché eseguire un blocco o una cancellazione selettiva per i dati aziendali nei dispositivi non registrati. Per supportare l'uso di Lookout for Work con dispositivi non registrati:
  - [Aggiungere l'app MTD ai dispositivi non registrati](../protect/mtd-add-apps-unenrolled-devices.md)
  - [Creare criteri di protezione dell'app Mobile Threat Defense](../protect/mtd-app-protection-policy.md)
  - [Abilitare il connettore MTD in Intune per i dispositivi non registrati](../protect/mtd-enable-unenrolled-devices.md)

## <a name="supported-platforms"></a>Piattaforme supportate

Lookout supporta le piattaforme seguenti per i dispositivi registrati in Intune:

- **Android 4.1 e versioni successive**  
- **iOS 8 e versioni successive**  

Per altre informazioni sulle piattaforme e le lingue supportate, visitare il [sito Web di Lookout](https://personal.support.lookout.com/hc/articles/114094140253).  

## <a name="prerequisites"></a>Prerequisiti

- Sottoscrizione aziendale a Lookout Mobile EndPoint Security  
- Sottoscrizione di Microsoft Intune
- Azure Active Directory Premium
- Enterprise Mobility + Security (EMS) E3 o E5, con licenze assegnate agli utenti.  

Per altre informazioni, vedere [Lookout Mobile Endpoint Security](https://www.lookout.com/products/mobile-endpoint-security)

## <a name="sample-scenarios"></a>Scenari di esempio

Ecco gli scenari comuni per l'uso di Lookout Mobile Endpoint Security con Intune.

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Controllare l'accesso in base alle minacce da parte di app dannose

Se nei dispositivi vengono rilevate app dannose, come malware, è possibile impedire ai dispositivi di eseguire le operazioni seguenti fino alla risoluzione della condizione di minaccia:

- Connessione alla posta elettronica aziendale
- Sincronizzazione di file aziendali tramite l'app OneDrive for Work
- Accesso alle app aziendali

*Bloccare quando vengono rilevate app dannose:*

> [!div class="mx-imgBorder"]
> ![Immagine concettuale dei criteri che bloccano l'accesso a causa di app dannose](./media/lookout-mobile-threat-defense-connector/malicious-apps-blocked.png)

*Accesso concesso dopo la correzione:*

> [!div class="mx-imgBorder"]
> ![Immagine concettuale in cui l'accesso viene concesso ai dispositivi dopo la correzione](./media/lookout-mobile-threat-defense-connector/malicious-apps-unblocked.png)

### <a name="control-access-based-on-threat-to-network"></a>Controllare l'accesso in base alle minacce per la rete

Rilevare le minacce per la rete, ad esempio attacchi man-in-the-middle e proteggere l'accesso a reti Wi-Fi in base al livello di rischio del dispositivo.

*Bloccare l'accesso alla rete tramite Wi-Fi:*

> [!div class="mx-imgBorder"]
> ![Immagine che illustra il blocco dell'accesso alla rete Wi-Fi in base alle minacce per la rete](./media/lookout-mobile-threat-defense-connector/network-wifi-blocked.png)

*Accesso concesso dopo la correzione:*

> [!div class="mx-imgBorder"]
> ![Immagine concettuale dell'accesso condizionale che consente l'accesso dopo la correzione](./media/lookout-mobile-threat-defense-connector/network-wifi-unblocked.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Controllare l'accesso a SharePoint Online in base alle minacce alla rete

Rilevare le minacce alla rete, ad esempio attacchi di tipo man-in-the-middle, e impedire la sincronizzazione dei file aziendali in base al rischio per il dispositivo.

*Bloccare SharePoint Online quando vengono rilevate minacce per la rete:*

> [!div class="mx-imgBorder"]
> ![Immagine concettuale del blocco dell'accesso a SharePoint Online](./media/lookout-mobile-threat-defense-connector/network-spo-blocked.png)

*Accesso concesso dopo la correzione:*

> [!div class="mx-imgBorder"]
> ![Immagine concettuale della concessione dell'accesso dopo la risoluzione della condizione di minaccia per la rete](./media/lookout-mobile-threat-defense-connector/network-spo-unblocked.png)

### <a name="control-access-on-unenrolled-devices-based-on-threats-from-malicious-apps"></a>Controllare l'accesso nei dispositivi non registrati in base alle minacce da parte di app dannose

Quando la soluzione Lookout Mobile Threat Defense considera un dispositivo infetto:
> [!div class="mx-imgBorder"]
> ![I criteri di protezione delle app eseguono il blocco a causa del malware rilevato](./media/lookout-mobile-threat-defense-connector/lookout-app-policy-block.png)

L'accesso viene concesso dopo la correzione:

> [!div class="mx-imgBorder"]
> ![L'accesso viene concesso dopo la correzione per i criteri di protezione delle app](./media/lookout-mobile-threat-defense-connector/lookout-app-policy-remediated.png)

## <a name="next-steps"></a>Passaggi successivi

Ecco i passaggi principali da seguire per implementare questa soluzione:

- [Configurare l'integrazione di Lookout](lookout-mtd-connector-integration.md)
- [Abilitare Mobile Endpoint Security in Intune](mtd-connector-enable.md)
- [Aggiungere e assegnare l'app Lookout for Work](mtd-apps-ios-app-configuration-policy-add-assign.md)
- [Configurare i criteri di conformità dei dispositivi di Lookout](mtd-device-compliance-policy-create.md)
- [Creare un criterio di protezione delle app MTD](mtd-app-protection-policy.md)