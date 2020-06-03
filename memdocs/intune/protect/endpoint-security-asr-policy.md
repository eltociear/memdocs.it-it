---
title: Gestire le impostazioni di riduzione della superficie di attacco con i criteri di sicurezza degli endpoint in Microsoft Intune | Microsoft Docs
description: Configurare e distribuire i criteri per i dispositivi gestiti con le impostazioni di criteri per la riduzione della superficie di attacco nella sicurezza degli endpoint in Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 20c8cc73e8037c0f394547b64d562cf75271240c
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431449"
---
# <a name="attack-surface-reduction-policy-for-endpoint-security-in-intune"></a>Criteri di riduzione della superficie di attacco nella sicurezza degli endpoint in Intune

Quando l'antivirus Defender viene usato nei dispositivi Windows 10, è possibile usare i criteri di sicurezza degli endpoint per la riduzione della superficie di attacco di Intune per gestire le impostazioni per i dispositivi.

I criteri di riduzione della superficie di attacco consentono di ridurre le superfici di attacco, ovvero gli spazi in cui l'organizzazione può essere vulnerabile a minacce e attacchi informatici. Per altre informazioni, vedere [Panoramica della riduzione della superficie di attacco]( https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/overview-attack-surface-reduction) nella documentazione di Windows Threat Protection.

I criteri di sicurezza degli endpoint per la riduzione della superficie di attacco sono disponibili in *Gestione* nel nodo **Sicurezza degli endpoint** dell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431). Ogni *profilo* per la riduzione della superficie di attacco gestisce le impostazioni per un'area specifica di un dispositivo Windows 10.

Visualizzare le [impostazioni per i profili di riduzione della superficie di attacco](../protect/endpoint-security-asr-profile-settings.md).

## <a name="prerequisites-for-attack-surface-reduction-profiles"></a>Prerequisiti per i profili di riduzione della superficie di attacco

- Windows 10 o versioni successive
- L'antivirus Defender deve essere l'antivirus principale del dispositivo

## <a name="attack-surface-reduction-profiles"></a>Profili di riduzione della superficie di attacco

**Profili di Windows 10**:

- **Isolamento di app e browser** - Consente di gestire impostazioni per Windows Defender Application Guard (Application Guard) nel contesto di Defender ATP. Application Guard consente di evitare attacchi obsoleti e recenti e può isolare i siti definiti dall'organizzazione come non attendibili e definire i siti, le risorse cloud e le reti interne ritenute attendibili.

  Per altre informazioni, vedere [Application Guard](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/wd-app-guard-overview) nella documentazione di Microsoft Defender ATP.

- **Protezione Web** - Le impostazioni gestibili per la protezione Web in Microsoft Defender ATP configurano la protezione di rete per proteggere i computer dalle minacce Web. Grazie all'integrazione con Microsoft Edge e con i browser di terze parti più diffusi come Chrome e Firefox, Protezione Web blocca le minacce Web senza un proxy Web e può proteggere i computer in sede o fuori sede. Protezione Web impedisce l'accesso a:
  - Siti di phishing
  - Vettori di malware
  - Siti exploit
  - Siti non attendibili o con bassa reputazione
  - Siti bloccati dall'utente nell'elenco di indicatori personalizzato.

  Per altre informazioni, vedere [Protezione Web](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/web-protection-overview) nella documentazione di Microsoft Defender ATP.

- **Controllo applicazione** - Le impostazioni di Controllo applicazione consentono di ridurre le minacce per la sicurezza, limitando le applicazioni che gli utenti possono eseguire e il codice eseguito nel nucleo (kernel) del sistema. È possibile gestire impostazioni che possono bloccare script non firmati e MSI e limitare Windows PowerShell in modo che venga eseguito in modalità di linguaggio vincolato.

  Per altre informazioni, vedere [Controllo applicazione](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control) nella documentazione di Microsoft Defender ATP.

- **Regole per la riduzione della superficie di attacco** -Configurare le impostazioni per le regole di riduzione della superficie di attacco che rilevano comportamenti usati in genere da malware e app per infettare i computer, tra cui:
  - File eseguibili e script usati nelle app di Office o nella posta elettronica Web che provano a scaricare o a eseguire file
  - Script offuscati o sospetti per altri motivi
  - Comportamenti che le app non avviano normalmente durante le attività quotidiane comuni. La riduzione della superficie di attacco significa offrire agli utenti malintenzionati meno opportunità di eseguire attacchi.

  Per altre informazioni, vedere [Regole per la riduzione della superficie di attacco](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction) nella documentazione di Microsoft Defender ATP.

- **Controllo del dispositivo** - Le impostazioni per il controllo del dispositivo consentono di configurare i dispositivi con un approccio a più livelli per la protezione dei supporti rimovibili. Microsoft Defender ATP offre diverse funzionalità di monitoraggio e controllo, che consentono di evitare che le minacce presenti in periferiche non autorizzate compromettano i dispositivi in uso.

  Per altre informazioni, vedere [Come controllare i dispositivi USB e altri elementi multimediali rimovibili con Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/device-control/control-usb-devices-using-intune) nella documentazione di Microsoft Defender ATP.

- **Protezione dagli exploit** - Le impostazioni di protezione dagli exploit possono contribuire alla protezione dal malware che usa gli exploit per infettare i dispositivi ed espandersi. La protezione dagli exploit è costituita da una serie di mitigazioni che è possibile applicare al sistema operativo o a singole app.

  Per altre informazioni, vedere [Abilitare la protezione dagli exploit](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/enable-exploit-protection) nella documentazione di Microsoft Defender ATP.

## <a name="next-steps"></a>Passaggi successivi

[Configurare i criteri di sicurezza degli endpoint](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
