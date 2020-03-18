---
title: Gestire i dispositivi con profilo di lavoro Android Enterprise in Microsoft Intune
titleSuffix: ''
description: Microsoft Intune gestisce i dispositivi con profilo di lavoro Android Enterprise per offrire funzionalità di gestione e privacy aggiuntive quando gli utenti usano i dispositivi Android personali per il lavoro.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 01/22/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 2cc3c960-1fdd-47ca-a693-420d47b403de
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: df5cb910d38deaca76ee92246badcebf02a7e4de
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79339605"
---
# <a name="manage-android-work-profile-devices-with-intune"></a>Gestire i dispositivi del profilo di lavoro Android con Intune

Android Enterprise offre un set di opzioni di registrazione che forniscono agli utenti le funzionalità più aggiornate e sicure. La registrazione con il profilo di lavoro Android Enterprise offre un set di funzionalità e servizi per separare le app e i dati personali da quelli aziendali. Vengono fornite inoltre funzionalità di gestione e privacy aggiuntive quando gli utenti usano i dispositivi Android personali per lavoro. 

## <a name="supported-devices"></a>Dispositivi supportati

Le funzionalità di gestione di Android Enterprise si basano su funzionalità che fanno parte dei sistemi operativi Android più recenti. Per i dispositivi che non supportano Android Enterprise, rimangono disponibili le funzionalità di gestione convenzionali di Android. Per altre informazioni, vedere [Android Enterprise requirements](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012) (Requisiti di Android Enterprise).

## <a name="onboarding"></a>Onboarding

Prima di registrare i dispositivi con il profilo di lavoro Android Enterprise, è necessario eseguire alcuni passaggi di onboarding. Questi passaggi stabiliscono una connessione tra il tenant di Intune e il servizio Google Play gestito. Per altre informazioni, vedere [Abilitare la registrazione dei dispositivi con profilo di lavoro Android Enterprise](android-work-profile-enroll.md).

## <a name="work-profile-management"></a>Gestione del profilo di lavoro

Quando si gestisce un dispositivo con profilo di lavoro Android Enterprise usando Intune, non si gestisce l'intero dispositivo. Le funzionalità di gestione hanno effetti solo sul profilo di lavoro creato nel dispositivo durante la registrazione. Qualsiasi app distribuita nel dispositivo con Intune viene installata nel profilo di lavoro. Le icone delle app nel profilo di lavoro si differenziano dalle app personali nel dispositivo. Tutti i dati e le app Android all'esterno della parte dedicata ad Android Enterprise del dispositivo rimangono personali e sotto il controllo dell'utente finale. Gli utenti possono installare qualsiasi app nella parte personale del dispositivo. Gli amministratori possono gestire e monitorare le app e le azioni nell'ambito del profilo di lavoro.

Intune offre una gamma di impostazioni generali predefinite che è possibile configurare nei dispositivi del profilo di lavoro Android. Per altre informazioni, vedere [Android work profile device policy settings](../protect/compliance-policy-create-android-for-work.md) (Impostazioni dei criteri dei dispositivi del profilo di lavoro Android).

## <a name="app-publishing-and-distribution"></a>Distribuzione e pubblicazione di app

Il servizio Google Play gestito è parte integrante della distribuzione e della gestione di app Android Enterprise. Tutte le app distribuite nei dispositivi con profilo di lavoro Android Enterprise provengono dal servizio Google Play gestito. Per gestire e distribuire le app in Play Store, accedere al sito Web Google Play con le credenziali di amministratore della società per la gestione di Google. È possibile approvare le app per la distribuzione di Android Enterprise in modo che vengano visualizzate nei profili di lavoro dei dispositivi. Queste app vengono quindi sincronizzate con la console di Intune e possono essere distribuite e gestite tramite Intune. Le app line-of-business (LOB) sviluppate dall'organizzazione devono essere pubblicate in Google Play gestito usando la console per la pubblicazione di app Android di Google. Le app line-of-business devono essere configurate nella console di pubblicazione di app Android per limitare l'accesso all'organizzazione.

Le app possono essere installate senza interazioni con l'utente e senza richiedere all'utente di consentire l'**installazione da origini sconosciute**. Per cercare e installare app facoltative o disponibili, l'utente può usare lo store Play for Work nel proprio dispositivo. Per altre informazioni, vedere [Assegnare app ai dispositivi con profilo di lavoro Android Enterprise con Intune](../apps/apps-add-android-for-work.md).

## <a name="app-configuration"></a>Configurazione delle app

Android Enterprise offre un'infrastruttura per distribuire i valori di configurazione delle app alle app che li supportano. Specificando i valori di configurazione per le app di lavoro, è possibile assicurarsi che vengano impostate correttamente quando gli utenti le avviano per la prima volta. Per il supporto della configurazione delle app è necessario che gli sviluppatori creino le app Android in modo specifico per supportare valori di configurazione gestiti. Ciò rende possibile usare Intune per specificare e applicare queste impostazioni di configurazione. Per altre informazioni, vedere [Aggiungere criteri di configurazione delle app per i dispositivi Android gestiti](../apps/app-configuration-policies-use-android.md).

## <a name="email-configuration"></a>Configurazione della posta elettronica

Android Enterprise non offre un'app di posta elettronica predefinita o un oggetto profilo di posta elettronica nativo simile a quelli offerti da iOS/iPadOS. Le configurazioni per la posta elettronica possono essere invece impostate tramite l'applicazione di impostazioni di configurazione delle app alle app di posta elettronica che le supportano. Gmail e Nine Work sono due app client Exchange ActiveSync (EAS) disponibili in Play Store che supportano l'uso della configurazione delle app Android Enterprise.

Intune offre modelli di configurazione per le app Gmail e Nine Work gestite come app di lavoro. Altre app di posta elettronica che supportano i profili di configurazione delle app possono essere configurate con i criteri di configurazione delle app per dispositivi mobili.

Se si usa l'accesso condizionale di Exchange ActiveSync per un dispositivo con profilo di lavoro Android Enterprise, può essere utile usare l'app di posta elettronica Gmail o Nine Work. Sono anche supportate l'app Microsoft Outlook per Android e qualsiasi altra app di posta elettronica che usa l'autenticazione moderna tramite ADAL. Per altre informazioni, vedere [Come configurare le impostazioni di posta elettronica in Microsoft Intune](../configuration/email-settings-configure.md).

## <a name="app-protection-policies"></a>Criteri di protezione delle app

I criteri di protezione delle app applicati sono completamente supportati nel profilo di lavoro e nel profilo personale. È possibile pubblicare app line-of-business nella console di pubblicazione di app Android all'indirizzo https://play.google.com/apps/publish. Questa console include un'opzione per impostare le app come private per l'organizzazione. Per altre informazioni, vedere [Aggiungere criteri di conformità per dispositivi con profilo di lavoro Android Enterprise in Intune](../protect/compliance-policy-create-android-for-work.md). Per informazioni generali sui criteri di protezione delle app, vedere [Che cosa sono i criteri di protezione delle app](../apps/app-protection-policy.md)

## <a name="vpn-profiles"></a>Profili VPN

Il supporto VPN è simile ai profili VPN Android. Per la gestione di Android Enterprise sono disponibili gli stessi provider di VPN e le stesse opzioni di configurazione di base, con due differenze:

- **VPN con ambito profilo di lavoro**: le connessioni VPN si limitano alle app distribuite nel profilo di lavoro. Solo le app gestite da Android Enterprise possono usare la connessione VPN. Le app personali nel dispositivo non possono usare una connessione VPN gestita. Per altre informazioni, vedere [Impostazioni VPN per Android Enterprise](../configuration/vpn-settings-android-enterprise.md).

- **VPN specifica dell'app**: la VPN specifica dell'app può essere configurata in Intune se il provider VPN supporta:
  - la configurazione per la VPN specifica dell'app
  - la possibilità di configurare una VPN per ogni app tramite il profilo di configurazione delle app di Android Enterprise.
  Per altre informazioni, vedere [Usare un profilo personalizzato di Microsoft Intune per creare un profilo VPN per ogni app per dispositivi Android](../configuration/android-pulse-secure-per-app-vpn.md).

## <a name="certificate-profiles"></a>Profili certificato

Le stesse opzioni di configurazione del profilo certificato disponibili per la gestione Android sono disponibili nei dispositivi con profilo di lavoro Android Enterprise. Android Enterprise fornisce API per la gestione avanzata dei certificati. Le funzionalità di gestione avanzata dei certificati consentono di:

- Assicurarsi che la distribuzione dei certificati sia invisibile all'utente.
- Assicurarsi che i certificati distribuiti vengano rimossi quando un dispositivo viene ritirato da Intune e il profilo di lavoro viene rimosso.
- Offrire comunicazioni migliori per informare gli utenti che il certificato è stato distribuito e configurato dal proprio reparto IT tramite il servizio di gestione.

Per altre informazioni, vedere [Configurare un profilo certificato per i dispositivi in Microsoft Intune](../protect/certificates-configure.md).

## <a name="wi-fi-profiles"></a>Profili Wi-Fi

I profili Wi-Fi gestiti da Android Enterprise vengono rimossi quando il dispositivo viene ritirato da Intune e il profilo di lavoro viene eliminato. Per altre informazioni, vedere [Come configurare le impostazioni Wi-Fi in Microsoft Intune](../configuration/wi-fi-settings-configure.md).

## <a name="next-steps"></a>Passaggi successivi
- [Registrare dispositivi Android](android-enroll.md)
- [Assegnare app ai dispositivi con profilo di lavoro Android Enterprise con Intune](../apps/apps-add-android-for-work.md)
