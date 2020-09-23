---
title: In fase di sviluppo - Microsoft Intune
titleSuffix: ''
description: Funzionalità di Microsoft Intune in fase di sviluppo
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/28/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: b1f261d8d61fc2c4273ae8f137a43bb6c607430d
ms.sourcegitcommit: fdd6d3c4b906e895ebec2856ebc38b0656296d2c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/22/2020
ms.locfileid: "91002699"
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


<!-- ***********************************************-->
## <a name="device-configuration"></a>Configurazione del dispositivo

### <a name="create-pkcs-certificate-profiles-for-android-enterprise-fully-managed-devices-cobo---4839686---"></a>Creare nuovi profili dei certificati PKCS per dispositivi Android Enterprise completamente gestiti (COBO)<!-- 4839686 -->
È possibile creare profili dei certificati PKCS per distribuire certificati ai proprietari di dispositivi Android Enterprise e a dispositivi con profilo di lavoro (**Dispositivi** > **Profili di configurazione**  > **Crea profilo** > **Android Enterprise > Solo proprietario del dispositivo** oppure **Android Enterprise > Solo profilo di lavoro** per la piattaforma > **PKCS** per il profilo).

A breve sarà possibile creare nuovi profili dei certificati PKCS per dispositivi Android Enterprise completamente gestiti. Il connettore di certificati PFX di Intune è obbligatorio. Se non si usa SCEP e si usa solo PKCS, è possibile rimuovere il connettore NDES dopo aver installato il nuovo connettore PFX. Il nuovo connettore PFX importa i file PFX e distribuisce i certificati PKCS a tutte le piattaforme.

Per altre informazioni sui certificati PKCS, vedere [Configurare e usare i certificati PKCS con Intune](../protect/certficates-pfx-configure.md).

Si applica a:
- Android Enterprise completamente gestito (COBO)

### <a name="use-netmotion-as-a-vpn-connection-type-for-android-enterprise-work-profile-devices---7764263---"></a>Usare NetMotion come tipo di connessione VPN per i dispositivi con profilo di lavoro Android Enterprise<!-- 7764263 -->
Quando si crea un profilo VPN, NetMotion è disponibile come tipo di connessione VPN (**Dispositivi** > **Configurazione dispositivo** > **Crea profilo** > **Profilo di lavoro Android Enterprise** per la piattaforma > **VPN** per il profilo > **NetMotion** per il tipo di connessione).

Per altre informazioni sui profili VPN in Intune, vedere [Creare profili VPN per la connessione ai server VPN](../configuration/vpn-settings-configure.md).

Si applica a:
- Profilo di lavoro di Android Enterprise

### <a name="changes-for-password-settings-in-device-restriction-profiles-for-android-device-administrator---7662279----"></a>Modifiche per le impostazioni della password nei profili di restrizione dei dispositivi per l'amministratore di dispositivi Android<!-- 7662279  --> 
Sono state introdotte alcune modifiche per le impostazioni della password per i criteri di *restrizione del dispositivo* e di *conformità* per l'*amministratore di dispositivi Android*. (**Dispositivi** > **Profili di configurazione** > **Crea profilo** > **Restrizioni del dispositivo** e **Dispositivi** > **Criteri di conformità** > **Crea criterio**) Queste modifiche consentono a Intune di integrare le modifiche in Android versione 10 e successive, per garantire che le impostazioni per le password continuino a essere applicate ai dispositivi come previsto.
 
Le modifiche includono:
- Rimozione dell'opzione di primo livello per **Password**.  
- Le impostazioni verranno riorganizzate in sezioni in base ai dispositivi a cui si applicano.
- L'impostazione **Lunghezza minima password** verrà disabilitata per l'uso, a meno che l'impostazione **Tipo password** non sia configurata su un valore a cui si applica la lunghezza della password.
- Altri aggiornamenti per le etichette e il testo di esempio.

Queste modifiche si applicano all'interfaccia utente per le impostazioni e non influiscono sui profili esistenti. 

<!-- ***********************************************-->
## <a name="device-enrollment"></a>Registrazione del dispositivo

### <a name="ending-support-for-ios-11--7327321---"></a>Termine del supporto per iOS 11<!--7327321 -->
Dopo il rilascio di iOS 14, la registrazione di Intune e l'app Portale aziendale supporteranno iOS versione 12 e successive. Le versioni precedenti non saranno supportate ma continueranno a ricevere i criteri.

### <a name="ending-support-for-macos-1012--7327326---"></a>Termine del supporto per macOS 10.12<!--7327326 -->
Dopo il rilascio di macOS 11, la registrazione di Intune e l'app Portale aziendale supporteranno macOS versione 10.13 e successive. Le versioni precedenti non saranno supportate.


<!-- ***********************************************-->
## <a name="device-management"></a>Gestione dei dispositivi

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>Supporto degli script di PowerShell per dispositivi BYOD<!-- 1862833  -->
Gli script di PowerShell supporteranno i dispositivi registrati con Azure AD in Intune. Per altre informazioni su PowerShell, vedere [Usare gli script di PowerShell nei dispositivi Windows 10 in Intune](../apps/intune-management-extension.md). Questa funzionalità non supporta i dispositivi che eseguono Windows 10 Home Edition.

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics includerà il log dei dettagli del dispositivo<!--6014987  -->
I log dei dettagli dei dispositivi di Intune saranno disponibili in **Report** > **Log Analytics**. È possibile correlare i dettagli dei dispositivi per creare query personalizzate e cartelle di lavoro di Azure.

### <a name="tenant-attach-run-scripts-from-the-admin-center--7220536-cm6234688---"></a>Collegamento di tenant: eseguire script dall'interfaccia di amministrazione<!--7220536, CM6234688 -->
Sarà possibile sfruttare la potenza della funzionalità locale di Configuration Manager per [l'esecuzione di script](../../configmgr/apps/deploy-use/create-deploy-scripts.md) nell'interfaccia di amministrazione di Microsoft Endpoint Manager. Altri utenti tipo, ad esempio il personale del supporto tecnico, possono eseguire script di PowerShell dal cloud su un singolo dispositivo gestito di Configuration Manager. In questo modo è possibile usufruire di tutti i vantaggi tradizionali degli script di PowerShell che sono già stati definiti e approvati dall'amministratore di Configuration Manager nel nuovo ambiente. Per altre informazioni, vedere [Configuration Manager technical preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_scripts). 

### <a name="deploy-software-updates-to-macos-devices----3194876---"></a>Distribuire gli aggiornamenti software nei dispositivi macOS <!-- 3194876 -->
Sarà possibile distribuire gli aggiornamenti software a gruppi di dispositivi macOS. Questa funzionalità include aggiornamenti critici, firmware, file di configurazione e altri aggiornamenti. Sarà possibile inviare aggiornamenti alla successiva sincronizzazione del dispositivo oppure selezionare una pianificazione settimanale per distribuire gli aggiornamenti entro o al di fuori degli intervalli di tempo impostati. Ciò può risultare utile quando si vuole aggiornare i dispositivi al di fuori delle ore di lavoro standard o quando l'help desk occupa tutto il personale. Si otterrà anche un report dettagliato di tutti i dispositivi macOS a cui sono stati distribuiti gli aggiornamenti. È possibile esaminare il report per ogni singolo dispositivo per visualizzare lo stato di specifici aggiornamenti.

<!-- ***********************************************-->
## <a name="intune-apps"></a>App di Intune

### <a name="unified-delivery-of-azure-ad-enterprise-and-office-online-applications-in-the-windows-company-portal---1817861----"></a>Distribuzione unificata di applicazioni Azure AD Enterprise e Office Online nel Portale aziendale di Windows<!-- 1817861  -->
Nella versione 2006 è stata annunciata la [distribuzione unificata di applicazioni Azure AD Enterprise e Office Online nel Portale aziendale](../fundamentals/whats-new.md). Questa funzionalità sarà supportata nell'app Portale aziendale di Windows. Nel riquadro **Personalizzazione** di Intune sarà possibile selezionare **Nascondi** o **Mostra** sia per le**applicazioni aziendali di Azure AD** che per le **applicazioni di Office Online** nel Portale aziendale di Windows. Ogni utente visualizzerà l'intero catalogo applicazioni dal servizio Microsoft scelto. Per impostazione predefinita, ogni origine di app aggiuntiva verrà impostata su **Nascondi**. Per trovare questa impostazione di configurazione, nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) selezionare **Amministrazione del tenant** > **Personalizzazione**. Per informazioni correlate, vedere [Come personalizzare le app Portale aziendale Intune, il sito Web Portale aziendale e l'app Intune](../apps/company-portal-app.md).
 

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
