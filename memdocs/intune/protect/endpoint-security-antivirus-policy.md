---
title: Gestire le impostazioni antivirus con i criteri di sicurezza degli endpoint in Microsoft Intune | Microsoft Docs
description: Configurare e distribuire criteri e usare report per i dispositivi gestiti con i criteri antivirus di sicurezza degli endpoint in Microsoft Endpoint Manager.
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
ms.openlocfilehash: 2f3a378cdb3b5e24371edb2fd6dc240962f80342
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431904"
---
# <a name="antivirus-policy-for-endpoint-security-in-intune"></a>Criteri antivirus per la sicurezza degli endpoint in Intune

I criteri antivirus per la sicurezza degli endpoint in Intune possono aiutare gli amministratori della sicurezza a concentrarsi sulla gestione del gruppo specifico di impostazioni antivirus per i dispositivi gestiti. Per usare i criteri antivirus, integrare Intune con Microsoft Defender Advanced Threat Protection (Defender ATP) come soluzione Mobile Threat Defense.

I criteri antivirus includono diversi profili. Ogni profilo contiene solo le impostazioni rilevanti per l'antivirus Defender ATP per macOS, Windows 10 o per l'esperienza utente dell'app Sicurezza di Windows nei dispositivi Windows 10.

I criteri antivirus sono disponibili in **Gestione** nel nodo Sicurezza degli endpoint dell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

I criteri antivirus includono le stesse impostazioni disponibili nei profili *Endpoint Protection* o *Restrizioni per i dispositivi* per i criteri [Configurazione dispositivo](../configuration/device-profile-create.md) e sono simili alle impostazioni dei criteri [Conformità del dispositivo](../protect/device-compliance-get-started.md). Tuttavia questi tipi di criteri includono altre categorie di impostazioni non correlate all'antivirus. Le impostazioni aggiuntive possono complicare l'attività di configurazione dell'antivirus. Inoltre le impostazioni disponibili nei criteri antivirus per macOS non sono disponibili tramite gli altri tipi di criteri. Il profilo Antivirus per macOS elimina la necessità di configurare le impostazioni usando file `.plist`.

## <a name="prerequisites-for-antivirus-policy"></a>Prerequisiti per i criteri Antivirus

- **macOS**
  - Qualsiasi versione supportata di macOS
  - Perché Intune gestisca le impostazioni antivirus di Intune in un dispositivo, è necessario che nel dispositivo sia installato Defender ATP. Vedere [Defender ATP per macOS](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) (nella documentazione di Defender ATP)

- **Windows 10 e versioni successive**
  - Perché Intune gestisca le impostazioni antivirus di Intune in un dispositivo, è necessario che nel dispositivo sia installato Defender ATP. Vedere [Microsoft Defender ATP per Windows](../protect/advanced-threat-protection.md) nella documentazione di Intune.
  - L'app Sicurezza di Windows è installata in tutti i dispositivi che eseguono Windows 10 e non sono richiesti altri prerequisiti.

## <a name="antivirus-profiles"></a>Profili antivirus

**Profili macOS**:

- **Antivirus** - Gestire le [impostazioni dei criteri antivirus](../protect/antivirus-microsoft-defender-settings-macos.md) per macOS.

  Quando si usa [Microsoft Defender ATP per Mac](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) è possibile configurare e distribuire le impostazioni antivirus nei dispositivi macOS gestiti tramite Intune, anziché configurare tali impostazioni usando i file `.plist`.

**Profili di Windows 10**:

- **Microsoft Defender Antivirus** - Gestire le [impostazioni dei criteri antivirus](../protect/antivirus-microsoft-defender-settings-windows.md) per Windows 10.

  Defender Antivirus è il componente di protezione di nuova generazione di Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP). La protezione di nuova generazione combina apprendimento automatico, analisi dei Big data, ricerca approfondita sulla resistenza alle minacce e infrastruttura cloud per proteggere i dispositivi nell'organizzazione aziendale.

  Il profilo *Microsoft Defender Antivirus* è un'istanza separata delle impostazioni antivirus disponibili nel profilo *Limitazioni del dispositivo* per i criteri Configurazione dispositivo.
  
  Diversamente dalle impostazioni antivirus in un *profilo Limitazioni del dispositivo*, è possibile usare queste impostazioni nei dispositivi con co-gestione. Per usare queste impostazioni, il [dispositivo di scorrimento del carico di lavoro di co-gestione](https://docs.microsoft.com/configmgr/comanage/how-to-switch-workloads) per Endpoint Protection deve essere impostato su Intune.

- **Esperienza Sicurezza di Windows**: gestire le [impostazioni dell'app Sicurezza di Windows](../protect/antivirus-security-experience-windows-settings.md) che gli utenti finali possono visualizzare in Microsoft Defender Security Center e le notifiche ricevute dagli utenti. L'app Sicurezza di Windows viene usata da numerose funzionalità di sicurezza di Windows per notifiche sull'integrità e sulla sicurezza del computer. Le notifiche delle app per la sicurezza includono firewall, prodotti antivirus, Windows Defender SmartScreen e altri.

## <a name="antivirus-policy-reports"></a>Report sui criteri antivirus

I report sui criteri antivirus visualizzano dettagli sullo stato dei criteri antivirus di sicurezza degli endpoint e sullo stato del dispositivo. Questi report sono disponibili nel nodo Sicurezza degli endpoint dell'interfaccia di amministrazione di Microsoft Endpoint Manager.

Per visualizzare i report, nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) passare a Sicurezza degli endpoint e selezionare **Antivirus**. Se si seleziona Antivirus viene visualizzata la pagina Riepilogo. Altri report e visualizzazioni di stato sono disponibili come pagine aggiuntive.

### <a name="summary"></a>Riepilogo

Nella pagina **Riepilogo** è possibile [creare nuovi criteri](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy) e visualizzare un elenco dei criteri creati in precedenza. L'elenco include i dettagli di alto livello del profilo incluso in quei criteri (Tipo di criteri) e indica se i criteri sono assegnati.

![Pagina di panoramica dei criteri antivirus](./media/endpoint-security-antivirus-policy/antivirus-summary.png)

Quando si selezionano criteri nell'elenco, viene aperta la *pagina di panoramica* per l'istanza dei criteri e vengono visualizzate altre informazioni. Quando si seleziona un riquadro da questa visualizzazione, Intune visualizza altri dettagli per il profilo, se disponibili.

![Pagina di panoramica dei criteri antivirus](./media/endpoint-security-antivirus-policy/policy-overview.png)

### <a name="windows-10-unhealthy-endpoints"></a>Endpoint non integri di Windows 10

Nella pagina degli **endpoint non integri di Windows 10** è possibile visualizzare informazioni sullo stato dell'antivirus nei dispositivi Windows 10 gestiti da MDM. Queste informazioni vengono restituite da Windows Defender Antivirus in esecuzione sul dispositivo come *Stato dell'agente delle minacce*.

In questa vista vengono visualizzati solo i dispositivi con problemi rilevati. Questa vista non visualizza i dettagli dei dispositivi identificati come puliti.

![Pagina di panoramica dei criteri antivirus](./media/endpoint-security-antivirus-policy/antivirus-unhealthy-endpoints.png)

## <a name="next-steps"></a>Passaggi successivi

[Configurare i criteri di sicurezza degli endpoint](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
