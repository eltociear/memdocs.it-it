---
title: Gestire le impostazioni antivirus con i criteri di sicurezza degli endpoint in Microsoft Intune | Microsoft Docs
description: Configurare e distribuire criteri e usare report per i dispositivi gestiti con i criteri antivirus di sicurezza degli endpoint in Microsoft Endpoint Manager.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/24/2020
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
ms.openlocfilehash: 2460a132711fb19d12f33bbada23756fc2344cca
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/31/2020
ms.locfileid: "89194247"
---
# <a name="antivirus-policy-for-endpoint-security-in-intune"></a>Criteri antivirus per la sicurezza degli endpoint in Intune

I criteri antivirus di sicurezza degli endpoint in Intune possono aiutare gli amministratori della sicurezza a concentrarsi sulla gestione del gruppo specifico di impostazioni antivirus per i dispositivi gestiti. Per usare i criteri antivirus, integrare Intune con Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) come soluzione Mobile Threat Defense.

I criteri antivirus includono diversi profili. Ogni profilo contiene solo le impostazioni rilevanti per l'antivirus Microsoft Defender ATP per macOS, Windows 10 o per l'esperienza utente dell'app Sicurezza di Windows nei dispositivi Windows 10.

I criteri antivirus sono disponibili in **Gestione** nel nodo Sicurezza degli endpoint dell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

I criteri antivirus includono le stesse impostazioni disponibili nei profili *Endpoint Protection* o *Limitazioni del dispositivo* per i criteri [Configurazione dispositivo](../configuration/device-profile-create.md) e sono simili alle impostazioni dei criteri [Conformità del dispositivo](../protect/device-compliance-get-started.md). Tuttavia questi tipi di criteri includono altre categorie di impostazioni non correlate all'antivirus. Le impostazioni aggiuntive possono complicare l'attività di configurazione dell'antivirus. Inoltre le impostazioni disponibili nei criteri antivirus per macOS non sono disponibili tramite gli altri tipi di criteri. Il profilo Antivirus per macOS elimina la necessità di configurare le impostazioni usando file `.plist`.

## <a name="prerequisites-for-antivirus-policy"></a>Prerequisiti per i criteri Antivirus

**Generale**:

- **macOS**
  - Qualsiasi versione supportata di macOS
  - Perché Intune gestisca le impostazioni antivirus di Intune in un dispositivo, è necessario che nel dispositivo sia installato Microsoft Defender ATP. Vedere [Microsoft Defender ATP per macOS](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) (nella documentazione di Microsoft Defender ATP)

- **Windows 10 e versioni successive**
  - Non sono necessari altri prerequisiti.

**Supporto per i client di Configuration Manager** (*anteprima*)

*Questo scenario è disponibile in anteprima e richiede l'uso di Configuration Manager (Current Branch) versione 2006 o successiva*.
<!--*This scenario is in preview and requires use of Configuration Manager Technical Preview version 2007 or later*.-->

- **Configurare il collegamento al tenant per i dispositivi di Configuration Manager**: per supportare la distribuzione dei criteri antivirus nei dispositivi gestiti da Configuration Manager, configurare il *collegamento al tenant*. A questo scopo, è necessario configurare le raccolte di dispositivi di Configuration Manager in modo da supportare i criteri di sicurezza degli endpoint di Intune.

  Per configurare il collegamento al tenant, vedere [Configurare il collegamento al tenant per supportare i criteri di Endpoint Protection](../protect/tenant-attach-intune.md).

## <a name="antivirus-profiles"></a>Profili antivirus

### <a name="devices-managed-by-intune"></a>Dispositivi gestiti da Intune

Per i dispositivi gestiti con Intune sono supportati i profili seguenti:

**macOS**:

- Piattaforma: **macOS**

  - Profilo: **Antivirus** - Gestire le [impostazioni dei criteri antivirus](../protect/antivirus-microsoft-defender-settings-macos.md) per macOS.

    Quando si usa [Microsoft Defender ATP per Mac](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) è possibile configurare e distribuire le impostazioni antivirus nei dispositivi macOS gestiti tramite Intune, anziché configurare tali impostazioni usando i file `.plist`.

**Windows 10**:

- Piattaforma: **Profili di Windows 10**

  - Profilo: **Microsoft Defender Antivirus** - Gestire le [impostazioni dei criteri antivirus](../protect/antivirus-microsoft-defender-settings-windows.md) per Windows 10.

    Defender Antivirus è il componente di protezione di nuova generazione di Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP). La protezione di nuova generazione raggruppa tecnologie come Machine Learning e l'infrastruttura cloud per proteggere i dispositivi nell'organizzazione aziendale.

    Il profilo *Microsoft Defender Antivirus* è un'istanza separata delle impostazioni antivirus disponibili nel profilo *Limitazioni del dispositivo* per i criteri Configurazione dispositivo.
  
    Diversamente dalle impostazioni antivirus in un *profilo Limitazioni del dispositivo*, è possibile usare queste impostazioni nei dispositivi con co-gestione. Per usare queste impostazioni, il [dispositivo di scorrimento del carico di lavoro di co-gestione](/configmgr/comanage/how-to-switch-workloads) per Endpoint Protection deve essere impostato su Intune.

  - Profilo: **Esclusioni di Microsoft Defender Antivirus**: gestire le impostazioni dei criteri solo per le [esclusioni dell'antivirus](../protect/antivirus-microsoft-defender-settings-windows.md#microsoft-defender-antivirus-exclusions).
  
    Con questi criteri è possibile gestire le impostazioni per i seguenti provider di servizi di configurazione (CSP) di Microsoft Defender Antivirus che definiscono le esclusioni dell'antivirus:

    - Defender/ExcludedPaths
    - Defender/ExcludedExtensions
    - Defender/ExcludedProcesses

    Questi provider di servizi di configurazione per le esclusioni dell'antivirus sono anche gestiti da criteri di *Microsoft Defender Antivirus*, che includono impostazioni identiche per le esclusioni. Le impostazioni di entrambi i tipi di criteri (*antivirus* ed *esclusioni dell'antivirus*) sono soggette all'[unione dei criteri](#policy-merge-for-settings) e creano un superset di esclusioni  per i dispositivi e gli utenti applicabili.

  - Profilo: **Esperienza Sicurezza di Windows**: gestire le [impostazioni dell'app Sicurezza di Windows](../protect/antivirus-security-experience-windows-settings.md) che gli utenti finali possono visualizzare in Microsoft Defender Security Center e le notifiche ricevute dagli utenti.

    L'app Sicurezza di Windows viene usata da numerose funzionalità di sicurezza di Windows per notifiche sull'integrità e sulla sicurezza del computer. Le notifiche delle app per la sicurezza includono firewall, prodotti antivirus, Windows Defender SmartScreen e altri.

### <a name="devices-managed-by-configuration-manager-in-preview"></a>Dispositivi gestiti da Configuration Manager *(in anteprima)*

[!INCLUDE [Profiles for Configuration Manager tenant attached devices](includes/configmgr-antivirus-profiles.md)]

## <a name="policy-merge-for-settings"></a>Unione dei criteri per le impostazioni

Alcune impostazioni dei criteri antivirus supportano l'*unione dei criteri*. L'unione dei criteri consente di evitare conflitti quando più criteri si applicano agli stessi dispositivi e configurano la stessa impostazione. Intune valuta le impostazioni supportate dall'unione dei criteri per ogni utente o dispositivo, acquisite da tutti i criteri applicabili. Tali impostazioni vengono quindi unite in un singolo superset di criteri.

Si creano ad esempio tre criteri antivirus distinti che definiscono esclusioni di percorso di file antivirus differenti. Alla fine, tutti e tre i criteri vengono assegnati allo stesso utente. Poiché il CSP per le esclusioni di percorsi di file di Microsoft Defender supporta l'unione dei criteri, Intune valuta e combina le esclusioni di file derivanti da tutti i criteri applicabili per l'utente. Le esclusioni vengono aggiunte a un superset e il singolo elenco di esclusioni viene distribuito al dispositivo degli utenti.

Se l'unione dei criteri non è supportata per un'impostazione, può verificarsi un conflitto. In caso di conflitti, l'utente o il dispositivo non riceve criteri per l'impostazione. Ad esempio, l'unione dei criteri non supporta il CSP per impedire l'installazione di ID dispositivo corrispondenti (*PreventInstallationOfMatchingDeviceIDs*). Le configurazioni per questo CSP non vengono unite e vengono elaborate separatamente.

Quando vengono elaborati separatamente, i conflitti dei criteri vengono risolti come segue:

1. Si applica il criterio più sicuro.
2. Se due criteri sono ugualmente sicuri, si applica l'ultimo criterio modificato.
3. Se l'ultimo criterio modificato non è in grado di risolvere il conflitto, al dispositivo non vengono distribuiti criteri.

### <a name="settings-and-csps-that-support-policy-merge"></a>Impostazioni e CSP che supportano l'unione dei criteri

Le impostazioni seguenti supportano l'unione dei criteri:

[Criteri di Microsoft Defender Antivirus](../protect/antivirus-microsoft-defender-settings-windows.md)

- **Defender - Processi da escludere** - CSP: [Defender/ExcludedProcesses](/windows/client-management/mdm/policy-csp-defender#defender-excludedprocesses)
- **Estensioni di file da escludere dalle analisi e dalla protezione in tempo reale** - CSP: [Defender/ExcludedExtensions](/windows/client-management/mdm/policy-csp-defender#defender-excludedextensions)
- **Defender - File e cartelle da escludere** - CSP: [Defender/ExcludedPaths](/windows/client-management/mdm/policy-csp-defender#defender-excludedpaths)

## <a name="antivirus-policy-reports"></a>Report sui criteri antivirus

I report sui criteri antivirus visualizzano dettagli sullo stato dei criteri antivirus di sicurezza degli endpoint e sullo stato del dispositivo. Questi report sono disponibili nel nodo Sicurezza degli endpoint dell'interfaccia di amministrazione di Microsoft Endpoint Manager.

Per visualizzare i report, nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) passare a Sicurezza degli endpoint e selezionare **Antivirus**. Se si seleziona Antivirus viene visualizzata la pagina Riepilogo. Altri report e visualizzazioni di stato sono disponibili come pagine aggiuntive.

### <a name="summary"></a>Riepilogo

Nella pagina **Riepilogo** è possibile [creare nuovi criteri](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy) e visualizzare un elenco dei criteri creati in precedenza. L'elenco include i dettagli di alto livello del profilo incluso in quei criteri (Tipo di criteri) e indica se i criteri sono assegnati.

![Pagina di riepilogo dei criteri antivirus](./media/endpoint-security-antivirus-policy/antivirus-summary.png)

Quando si selezionano criteri nell'elenco, viene aperta la *pagina di panoramica* per l'istanza dei criteri e vengono visualizzate altre informazioni. Quando si seleziona un riquadro in questa visualizzazione, Intune visualizza altri dettagli per il profilo, se disponibili.

![Pagina di panoramica dei criteri antivirus](./media/endpoint-security-antivirus-policy/policy-overview.png)

### <a name="windows-10-unhealthy-endpoints"></a>Endpoint non integri di Windows 10

Nella pagina degli **endpoint non integri di Windows 10** è possibile visualizzare informazioni sullo stato dell'antivirus nei dispositivi Windows 10 gestiti da MDM. Queste informazioni vengono restituite da Windows Defender Antivirus in esecuzione sul dispositivo come *Stato dell'agente delle minacce*.

In questa vista vengono visualizzati solo i dispositivi con problemi rilevati. Questa vista non visualizza i dettagli dei dispositivi identificati come puliti.

![Pagina dei criteri antivirus relativa a endpoint non integri](./media/endpoint-security-antivirus-policy/antivirus-unhealthy-endpoints.png)

## <a name="next-steps"></a>Passaggi successivi

[Configurare i criteri di sicurezza degli endpoint](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)