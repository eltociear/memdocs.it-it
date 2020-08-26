---
title: In fase di sviluppo - Microsoft Intune
titleSuffix: ''
description: Funzionalità di Microsoft Intune in fase di sviluppo
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/06/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0d443cb784c19956f52347a10f4123c622ab82a8
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/25/2020
ms.locfileid: "88820063"
---
# <a name="in-development-for-microsoft-intune"></a>In fase di sviluppo per Microsoft Intune

Per supportare gli utenti nella preparazione e pianificazione, questa pagina illustra gli aggiornamenti e le funzionalità dell'interfaccia utente di Intune che sono in fase di sviluppo ma non ancora rilasciati. Oltre alle informazioni contenute in questa pagina: 

- Se sono previste azioni prima di una modifica, verrà pubblicato un post complementare nel Centro messaggi di Office.
- Quando una funzionalità entra in produzione, sia in versione anteprima sia disponibile a livello generale, la descrizione della funzionalità viene spostata da questa pagina alla [pagina delle novità](whats-new.md).
- Questa pagina e la [pagina delle novità](whats-new.md) vengono aggiornate periodicamente. Consultarla a intervalli regolari per ulteriori aggiornamenti.
- Vedere la [roadmap di Microsoft 365](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS) per informazioni sulle sequenze temporali e i risultati finali strategici.

> [!NOTE]
> Questa pagina riflette le attuali previsioni su funzionalità di Intune che verranno introdotte in una versione futura. Le date e le singole funzionalità potrebbero cambiare. Questa pagina non descrive tutte le funzionalità in fase di sviluppo.

**Feed RSS**: è possibile sapere quando questa pagina viene aggiornata copiando e incollando l'URL seguente nel lettore di feed: `https://docs.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us`

**Questo articolo è stato aggiornato l'ultima volta nella data indicata sotto al titolo precedente**.

<!--
## What's coming to Intune in the Azure portal 
## What's coming to Intune apps
## Notices
-->

<!-- Common categories:  
## App management
## Device configuration
## Device enrollment
## Device management
## Intune apps
## Monitor and troubleshoot
## Role-based access control
## Security

-->
 
<!-- ***********************************************-->
## <a name="app-management"></a>Gestione delle app

### <a name="update-to-device-icons-in-company-portal-and-intune-apps-on-android---6057023----"></a>Aggiornamento alle icone del dispositivo nel Portale aziendale e nelle app di Intune in Android<!-- 6057023  -->
Viene eseguito un aggiornamento delle icone del dispositivo nel Portale aziendale e nelle app di Intune nei dispositivi Android per creare un aspetto più moderno e in linea con Microsoft Fluent Design System. Per informazioni correlate, vedere [Aggiornamento delle icone nell'app Portale aziendale per iOS/iPadOS e macOS](../fundamentals/whats-new-app-ui.md#update-to-icons-in-company-portal-app-for-iosipados-and-macos-). 

### <a name="ios-company-portal-will-support-apples-automated-device-enrollment-without-user-affinity---7282707----"></a>Il Portale aziendale per iOS supporterà la registrazione automatica dei dispositivi di Apple senza affinità utente<!-- 7282707  --> 
Il Portale aziendale per iOS sarà supportato nei dispositivi registrati con la registrazione automatica dei dispositivi di Apple senza richiedere un utente assegnato. L'utente finale può accedere al Portale aziendale per iOS per specificarsi come utente primario in un dispositivo iOS/iPadOS registrato senza affinità dispositivo. Per altre informazioni sulla registrazione automatica dei dispositivi, vedere [Registrare automaticamente i dispositivi iOS/iPadOS con Registrazione automatica del dispositivo di Apple](../enrollment/device-enrollment-program-enroll-ios.md).

### <a name="the-windows-company-portal-adds-configuration-manager-application-support---4297660---"></a>Il Portale aziendale Windows aggiunge il supporto delle applicazioni di Configuration Manager<!-- 4297660 -->
Il Portale aziendale Windows supporta ora le applicazioni di Configuration Manager. Questa funzionalità consente agli utenti finali di visualizzare le applicazioni distribuite di Configuration Manager e Intune nel Portale aziendale Windows per i clienti con co-gestione. Questo supporto consente agli amministratori di consolidare le diverse esperienze del portale per gli utenti finali. Per altre informazioni, vedere [Usare l'app Portale aziendale in dispositivi con co-gestione](https://docs.microsoft.com/mem/configmgr/core/get-started/2020/technical-preview-2006#bkmk_portal).

<!-- ***********************************************-->
## <a name="device-configuration"></a>Configurazione del dispositivo

### <a name="create-pkcs-certificate-profiles-for-android-enterprise-fully-managed-devices-cobo---4839686---"></a>Creare nuovi profili dei certificati PKCS per dispositivi Android Enterprise completamente gestiti (COBO)<!-- 4839686 -->
È possibile creare profili dei certificati PKCS per distribuire certificati ai proprietari di dispositivi Android Enterprise e a dispositivi con profilo di lavoro (**Dispositivi** > **Profili di configurazione**  > **Crea profilo** > **Android Enterprise > Solo proprietario del dispositivo** oppure **Android Enterprise > Solo profilo di lavoro** per la piattaforma > **PKCS** per il profilo).

A breve sarà possibile creare nuovi profili dei certificati PKCS per dispositivi Android Enterprise completamente gestiti. Il connettore di certificati PFX di Intune è obbligatorio. Se non si usa SCEP e si usa solo PKCS, è possibile rimuovere il connettore NDES dopo aver installato il nuovo connettore PFX. Il nuovo connettore PFX importa i file PFX e distribuisce i certificati PKCS a tutte le piattaforme.

Per altre informazioni sui certificati PKCS, vedere [Configurare e usare i certificati PKCS con Intune](../protect/certficates-pfx-configure.md).

Si applica a:
- Android Enterprise completamente gestito (COBO)

<!-- ***********************************************-->
<!-- ## Device enrollment-->




<!-- ***********************************************-->
## <a name="device-management"></a>Gestione dei dispositivi

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>Supporto degli script di PowerShell per dispositivi BYOD<!-- 1862833  -->
Gli script di PowerShell supporteranno i dispositivi registrati con Azure AD in Intune. Per altre informazioni su PowerShell, vedere [Usare gli script di PowerShell nei dispositivi Windows 10 in Intune](../apps/intune-management-extension.md). Questa funzionalità non supporta i dispositivi che eseguono Windows 10 Home Edition.

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics includerà il log dei dettagli del dispositivo<!--6014987  -->
I log dei dettagli dei dispositivi di Intune saranno disponibili in **Report** > **Log Analytics**. È possibile correlare i dettagli dei dispositivi per creare query personalizzate e cartelle di lavoro di Azure.

### <a name="tenant-attach-device-timeline-in-the-admin-center--7220536-cm7141381---"></a>Collegamento di tenant: sequenza temporale dispositivo nell'interfaccia di amministrazione<!--7220536, CM7141381 -->
Quando Configuration Manager sincronizza un dispositivo con Microsoft Endpoint Manager tramite il collegamento al tenant, è possibile visualizzare una sequenza temporale degli eventi. Questa sequenza temporale mostra le attività precedenti eseguite sul dispositivo che possono risultare utili per la risoluzione dei problemi. Per altre informazioni, vedere [Configuration Manager technical preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_timeline).  

### <a name="tenant-attach-install-an-application-from-the-admin-center---7220536-cm6024389---"></a>Collegamento di tenant: installare un'applicazione dall'interfaccia di amministrazione<!-- 7220536, CM6024389 -->
Sarà possibile avviare l'installazione di un'applicazione in tempo reale per un dispositivo collegato al tenant dall'interfaccia di amministrazione di Microsoft Endpoint Management. Per altre informazioni, vedere [Configuration Manager technical preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_apps).

### <a name="tenant-attach-cmpivot-from-the-admin-center--7220536-cm6024392---"></a>Collegamento di tenant: CMPivot dall'interfaccia di amministrazione<!--7220536, CM6024392 -->
Sarà possibile sfruttare la potenza di [CMPivot](../../configmgr/tenant-attach/cmpivot-overview-attached.md) nell'interfaccia di amministrazione di Microsoft Endpoint Manager. Altri utenti tipo, ad esempio il personale del supporto tecnico, possono avviare query in tempo reale dal cloud su un singolo dispositivo gestito da ConfigMgr e restituire i risultati all'interfaccia di amministrazione. In questo modo è possibile usufruire di tutti i vantaggi tradizionali di CMPivot, che consente agli amministratori IT e ad altri utenti designati di valutare rapidamente lo stato dei dispositivi nel proprio ambiente e di intervenire di conseguenza. Per altre informazioni, vedere [Configuration Manager technical preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_cmpivot). 

### <a name="tenant-attach-run-scripts-from-the-admin-center--7220536-cm6234688---"></a>Collegamento di tenant: eseguire script dall'interfaccia di amministrazione<!--7220536, CM6234688 -->
Sarà possibile sfruttare la potenza della funzionalità locale di Configuration Manager per [l'esecuzione di script](../../configmgr/apps/deploy-use/create-deploy-scripts.md) nell'interfaccia di amministrazione di Microsoft Endpoint Manager. Altri utenti tipo, ad esempio il personale del supporto tecnico, possono eseguire script di PowerShell dal cloud su un singolo dispositivo gestito di Configuration Manager. In questo modo è possibile usufruire di tutti i vantaggi tradizionali degli script di PowerShell che sono già stati definiti e approvati dall'amministratore di Configuration Manager nel nuovo ambiente. Per altre informazioni, vedere [Configuration Manager technical preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_scripts). 

### <a name="deploy-software-updates-to-macos-devices----3194876---"></a>Distribuire gli aggiornamenti software nei dispositivi macOS <!-- 3194876 -->
Sarà possibile distribuire gli aggiornamenti software a gruppi di dispositivi macOS. Questa funzionalità include aggiornamenti critici, firmware, file di configurazione e altri aggiornamenti. Sarà possibile inviare aggiornamenti alla successiva sincronizzazione del dispositivo oppure selezionare una pianificazione settimanale per distribuire gli aggiornamenti entro o al di fuori degli intervalli di tempo impostati. Ciò può risultare utile quando si vuole aggiornare i dispositivi al di fuori delle ore di lavoro standard o quando l'help desk occupa tutto il personale. Si otterrà anche un report dettagliato di tutti i dispositivi macOS a cui sono stati distribuiti gli aggiornamenti. È possibile esaminare il report per ogni singolo dispositivo per visualizzare lo stato di specifici aggiornamenti.

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## <a name="monitor-and-troubleshoot"></a>Monitorare e risolvere i problemi

### <a name="power-bi-compliance-report-template-v20---636958----"></a>Modello di report di conformità Power BI V2.0<!-- 636958  -->
Gli amministratori potranno aggiornare il modello di report di conformità di Power BI da V1.0 a V2.0. V2.0 includerà una struttura migliorata e modifiche ai calcoli e ai dati esposti come parte del modello. Per informazioni correlate, vedere [Connettersi al data warehouse con Power BI](../developer/reports-proc-get-a-link-powerbi.md).

<!-- ***********************************************-->
<!--
## Role-based access control
-->

<!-- ***********************************************-->
## <a name="security"></a>Sicurezza

### <a name="app-protection-policy-support-for-symantec-endpoint-security-and-check-point-sandblast----4452423-4731168---"></a>Supporto dei criteri di protezione delle app per Symantec Endpoint Security e Check Point Sandblast<!--  4452423, 4731168 -->

Nell'ottobre 2019 i criteri di protezione delle app di Intune hanno aggiunto la capacità per usare i dati di alcuni dei partner MTD (Microsoft Threat Defense). Verrà aggiunto il supporto per i partner seguenti per usare un criterio di protezione delle app per bloccare o cancellare in modo selettivo i dati aziendali dell'utente in base all'integrità di un dispositivo:

- **Check Point Sandblast** in Android, iOS e iPadOS
- **Symantec Endpoint Security** in Android, iOS e iPadOS

Per informazioni sull'uso dei criteri di protezione delle app con i partner MTD, vedere [Creare criteri di protezione delle app Mobile Threat Defense con Intune](../protect/mtd-app-protection-policy.md).

### <a name="microsoft-defender-atp-creates-endpoint-manager-security-task-with-vulnerability-details---5568193----"></a>Microsoft Defender ATP crea un'attività di sicurezza di Endpoint Manager con i dettagli sulle vulnerabilità<!-- 5568193  -->
Lo strumento di gestione delle minacce e delle vulnerabilità in Microsoft Defender ATP rileva le impostazioni di sicurezza che non sono configurate correttamente nei dispositivi. Gli amministratori usano queste informazioni per aggiornare i dispositivi vulnerabili.

A breve Microsoft Defender ATP potrà generare un'attività di sicurezza di Endpoint Manager (**Endpoint Manager** > **Sicurezza degli endpoint** > **Attività di sicurezza**) con i dettagli sulle vulnerabilità e visualizzare i dispositivi interessati. Gli amministratori IT possono accettare l'attività di sicurezza e distribuire la configurazione richiesta. 

Per altre informazioni sulle attività di sicurezza, vedere [Usare Intune per risolvere le vulnerabilità identificate da Microsoft Defender ATP](../protect/atp-manage-vulnerabilities.md).


<!-- ***********************************************-->
## <a name="notices"></a>Notifiche

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Vedere anche

Per informazioni dettagliate sugli ultimi sviluppi, vedere [Novità di Microsoft Intune](whats-new.md).
