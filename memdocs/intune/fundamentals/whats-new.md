---
title: Novità di Microsoft Intune - Azure | Microsoft Docs
titleSuffix: ''
description: Informazioni sulle novità nel portale di Intune di Azure
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/23/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 791ed23f-bd13-4ef0-a3dd-cd2d7332c5cc
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5d8ff51b8b20c5f6505cb341f666ce043b086b3b
ms.sourcegitcommit: 795e8a6aca41e1a0690b3d0d55ba3862f8a683e7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/24/2020
ms.locfileid: "80220184"
---
# <a name="whats-new-in-microsoft-intune"></a>Novità di Microsoft Intune

Informazioni sulle novità di Microsoft Intune ogni settimana, oltre ad [avvisi importanti](#notices), [versioni precedenti](whats-new-archive.md) e informazioni su [come vengono rilasciati gli aggiornamenti del servizio Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728). 

> [!Note]
> La distribuzione di ogni [aggiornamento mensile](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728), che può impiegare fino a tre giorni, avviene nell'ordine seguente:
>
> - Giorno 1: Asia Pacifico
> - Giorno 2: Europa, Medio Oriente, Africa
> - Giorno 3: America del Nord
> - Giorno 4+: Intune per enti governativi
>
> Alcune funzionalità possono essere implementate in diverse settimane e durante la prima è possibile che non siano disponibili per tutti i clienti.
>
> Per un elenco delle funzionalità che verranno rilasciate prossimamente, vedere la [pagina delle funzionalità in fase di sviluppo](in-development.md).

**Feed RSS**: è possibile ricevere una notifica quando questa pagina viene aggiornata copiando e incollando l'URL seguente nel lettore di feed: `https://docs.microsoft.com/api/search/rss?search=%22What%27s+new+in+microsoft+intune%3F+-+Azure%22&locale=en-us`

<!-- Common categories:  
### App management
### Device configuration
### Device enrollment
### Device management
### Device security
### Intune apps
### Monitor and troubleshoot
### Role-based access control
-->  

<!-- ########################## -->
## <a name="week-of-march-16-2020-2003-service-release"></a>Settimana del 16 marzo 2020 (versione del servizio 2003)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Gestione delle app

#### <a name="macos-and-ios-company-portal-updates---5779439-5780234----"></a>Aggiornamenti del Portale aziendale macOS e iOS<!-- 5779439, 5780234  -->
Il riquadro del profilo del Portale aziendale macOS e iOS è stato aggiornato in modo da includere il pulsante di disconnessione. Sono inoltre stati apportati miglioramenti dell'interfaccia utente nel riquadro del profilo del Portale aziendale macOS. Per altre informazioni sul Portale aziendale, vedere [Come configurare l'app Portale aziendale di Microsoft Intune](../apps/company-portal-app.md).

#### <a name="retarget-web-clips-to-microsoft-edge-on-ios-devices---5455276-----"></a>Ridestinare le clip Web a Microsoft Edge nei dispositivi iOS<!-- 5455276   -->
Le clip Web appena implementate (app Web aggiunte) nei dispositivi iOS, che devono essere aperte in un browser protetto, verranno aperte in Microsoft Edge anziché in Intune Managed Browser. È necessario ridestinare le clip Web preesistenti per assicurarsi che per l'apertura venga usato Microsoft Edge anziché Managed Browser. Per altre informazioni, vedere [Gestire l'accesso Web usando Microsoft Edge con Microsoft Intune](../apps/manage-microsoft-edge.md) e [Aggiungere app Web a Microsoft Intune](../apps/web-app.md).

#### <a name="use-the-intune-diagnostic-tool-with-microsoft-edge-for-android---4735244----"></a>Usare lo strumento di diagnostica di Intune con Microsoft Edge per Android<!-- 4735244  -->
Microsoft Edge per Android è ora integrato con lo strumento di diagnostica di Intune. Analogamente all'esperienza di Microsoft Edge per iOS, l'immissione di "about:intunehelp" nella barra degli URL (la casella dell'indirizzo) di Microsoft Edge nel dispositivo causa l'avvio dello strumento di diagnostica di Intune. Questo strumento genera log dettagliati. Gli utenti possono essere guidati in modo che raccolgano e inviino i log al reparto IT o visualizzino i log MAM per app specifiche.

#### <a name="updates-to-intune-branding-and-customization---5236032----"></a>Aggiornamenti del riquadro Personalizzazione di Intune<!-- 5236032  -->
Il riquadro di Intune denominato "Personalizzazione" è stato aggiornato apportando i miglioramenti seguenti:

- Il nome del riquadro, **Personalizzazione**, resterà invariato.
- Miglioramento dell'organizzazione e della progettazione delle impostazioni.
- Miglioramento del testo delle impostazioni e delle descrizioni comando.

Per trovare queste impostazioni in Intune, passare all'[Interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), selezionare **Amministrazione del tenant** > **Personalizzazione**. Per informazioni sulla personalizzazione esistente, vedere [Come configurare l'app Portale aziendale di Microsoft Intune](../apps/company-portal-app.md).

#### <a name="users-personal-encrypted-recovery-key---6273943----"></a>Chiave di ripristino crittografata personale dell'utente<!-- 6273943  -->
È disponibile una nuova funzionalità di Intune che consente agli utenti di recuperare la chiave di ripristino **FileVault** crittografata personale per i dispositivi Mac usando l'applicazione Portale aziendale per Android o l'applicazione Intune per Android. Sia nell'applicazione Portale aziendale che nell'applicazione Intune è disponibile un collegamento che aprirà un'istanza del browser Chrome per accedere al portale aziendale Web in cui l'utente può visualizzare la chiave di ripristino **FileVault** necessaria per accedere ai dispositivi Mac. Per altre informazioni sulla crittografia, vedere [Usare la crittografia dei dispositivi con Intune](../protect/encrypt-devices.md).

#### <a name="optimized-dedicated-device-enrollment----6114580-wnready---"></a>Ottimizzata la registrazione di dispositivi dedicati <!-- 6114580 wnready -->
È in corso l'ottimizzazione della registrazione per i dispositivi Android Enterprise dedicati ed è più semplice applicare i certificati SCEP associati al Wi-Fi ai dispositivi dedicati registrati prima del 22 novembre 2019. Per le nuove registrazioni, l'app di Intune continuerà a essere installata, ma gli utenti finali non dovranno più eseguire il passaggio per l'**abilitazione dell'agente di Intune** durante la registrazione. La fase verrà eseguita automaticamente in background e i certificati SCEP associati al Wi-Fi possono essere distribuiti e impostati senza interazione da parte dell'utente finale.  

Queste modifiche verranno implementate in fasi nel mese di marzo durante le distribuzioni back-end del servizio Intune. Tutti i tenant avranno questo nuovo comportamento entro la fine di marzo. Per le informazioni correlate, vedere [Supporto per i certificati SCEP nei dispositivi Android Enterprise dedicati](https://techcommunity.microsoft.com/t5/intune-customer-success/support-for-scep-certificates-in-android-enterprise-dedicated/ba-p/928147).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Configurazione del dispositivo

#### <a name="new-user-experience-when-creating-administrative-templates-on-windows-devices--5096036---"></a>Nuova esperienza utente durante la creazione di modelli amministrativi nei dispositivi Windows<!--5096036 -->
In base ai suggerimenti dei clienti e al passaggio alla nuova esperienza di Azure a schermo intero, l'esperienza del profilo Modelli amministrativi è stata ricompilata con una visualizzazione cartelle. Non sono state apportate modifiche a impostazioni o profili esistenti. Quindi, i profili esistenti rimarranno invariati e potranno essere usati nella nuova visualizzazione. È comunque possibile esplorare tutte le opzioni disponibili selezionando **Tutte le impostazioni** e usando la ricerca. La visualizzazione struttura ad albero è suddivisa in base alle configurazioni computer e utente. Le impostazioni di Windows, Office ed Edge si trovano nelle cartelle associate.  

Si applica a:
- Windows 10 e versioni successive

#### <a name="vpn-profiles-with-ikev2-vpn-connections-can-use-always-on-with-iosipados-devices---1947932-----"></a>I profili VPN con connessioni VPN IKEv2 possono usare Always On con i dispositivi iOS/iPadOS<!-- 1947932   -->
Nei dispositivi iOS/iPadOS è possibile creare un profilo VPN che usa una connessione IKEv2 (**Dispositivi** > **Profili di configurazione** > **Crea profilo** > **iOS/iPadOS** per la piattaforma > **VPN** per il tipo di profilo). Ora è possibile configurare Always On con IKEv2. Quando sono configurati, i profili VPN IKEv2 si connettono automaticamente e rimangono connessi (o si riconnettono rapidamente) alla rete VPN. Rimangono connessi anche quando si passa da una rete a un'altra o si riavviano i dispositivi.

In iOS/iPadOS la VPN Always On è limitata ai profili IKEv2.

Per visualizzare le impostazioni IKEv2 che è possibile configurare, vedere [Aggiungere impostazioni VPN in dispositivi iOS in Microsoft Intune](../configuration/vpn-settings-ios.md#ikev2-settings).

Si applica a:
- iOS/iPadOS

#### <a name="delete-bundles-and-bundle-arrays-in-oemconfig-device-configuration-profiles-on-android-enterprise-devices---5550355-----"></a>Eliminare aggregazioni e matrici di aggregazioni nei profili di configurazione dei dispositivi OEMConfig sui dispositivi Android Enterprise<!-- 5550355   -->
Nei dispositivi Android Enterprise creare e aggiornare i profili OEMConfig (**Dispositivi** > **Profili di configurazione** > **Crea profilo** > **Android Enterprise** per la piattaforma > **OEMConfig** per il tipo di profilo). Gli ora possono eliminare aggregazioni e matrici di aggregazioni usando **Progettazione configurazione** in Intune.

Per altre informazioni sui profili OEMConfig, vedere [Usare e gestire i dispositivi Android Enterprise con OEMConfig in Microsoft Intune](../configuration/android-oem-configuration-overview.md).

Si applica a:
- Android Enterprise

#### <a name="configure-the-iosipados-microsoft-azure-ad-sso-app-extension---5672534-----"></a>Configurare l'estensione dell'app SSO di Microsoft Azure AD per iOS/iPadOS<!-- 5672534   -->
Il team di Microsoft Azure AD ha creato un'estensione di app SSO (Single Sign-On) di reindirizzamento per consentire agli utenti di iOS/iPadOS 13.0 e versioni successive di accedere ad app e siti Web Microsoft con un unico accesso. Tutte le app che in precedenza avevano l'autenticazione tramite broker con l'app Microsoft Authenticator continueranno a ottenere l'accesso Single Sign-On con la nuova estensione SSO. Grazie alla disponibilità dell'estensione dell'app per l'accesso Single Sign-On di Azure AD, è possibile configurare l'estensione SSO con il tipo di estensione di reindirizzamento dell'app per l'accesso Single Sign-On (**Dispositivi** > **Profili di configurazione** > **Crea profilo** > **iOS/iPadOS** per la piattaforma > **Funzionalità del dispositivo** per il tipo di profilo > **Estensione dell'app per l'accesso Single Sign-on**).

Si applica a:
- iOS 13.0 e versioni successive
- iPadOS 13.0 e versioni successive

Per altre informazioni sulle estensioni dell'app per l'accesso Single Sign-On per iOS, vedere [Estensione dell'app per l'accesso Single Sign-On](../configuration/device-features-configure.md#single-sign-on-app-extension).

#### <a name="enterprise-app-trust-settings-modification-setting-is-removed-from-iosipados-device-restriction-profiles---6225131-----"></a>L'impostazione Modifica delle impostazioni di attendibilità delle app aziendali viene rimossa dai profili di limitazione dei dispositivi iOS/iPadOS<!-- 6225131   -->
Nei dispositivi iOS/iPadOS creare un profilo di limitazioni del dispositivo (**Dispositivi** > **Profili di configurazione** > **Crea profilo** > **iOS/iPadOS** per la piattaforma > **Limitazioni del dispositivo** per il tipo di profilo). L'impostazione **Modifica delle impostazioni di attendibilità delle app aziendali** viene rimossa da Apple e viene rimossa da Intune. Se usata in un profilo, attualmente questa impostazione non ha alcun impatto e viene rimossa dai profili esistenti. Questa impostazione viene rimossa anche dalle creazioni di report in Intune.

Si applica a:
- iOS/iPadOS

Per visualizzare le impostazioni che è possibile limitare, vedere [Impostazioni dei dispositivi iOS e iPadOS per consentire o limitare funzionalità](../configuration/device-restrictions-ios.md).

#### <a name="troubleshooting-pending-mam-policy-notification-changed-to-informational-icon--6348954---"></a>Risoluzione dei problemi: Notifica dei criteri MAM in sospeso modificata in icona informativa<!--6348954 -->
L'icona di notifica per i criteri MAM in sospeso nel pannello di risoluzione dei problemi è stata sostituita da un'icona informativa.

####  <a name="ui-update-when-configuring-compliance-policy---3961639------"></a>Aggiornamento dell'interfaccia utente durante la configurazione dei criteri di conformità<!-- 3961639    -->
È stata aggiornata l'interfaccia utente per la [creazione dei criteri di conformità](../protect/create-compliance-policy.md#create-the-policy) in Microsoft Endpoint Manager (**Dispositivi** > **Criteri di conformità** > **Criteri** > **Crea criterio**). Viene visualizzata una nuova esperienza utente con le stesse impostazioni e gli stessi dettagli usati in precedenza. La nuova esperienza segue un processo di tipo procedura guidata per creare i criteri di conformità e include una pagina in cui è possibile aggiungere *Assegnazioni* per i criteri e una pagina *Rivedi e crea* in cui è possibile esaminare la configurazione prima di creare i criteri.

#### <a name="retire-noncompliant-devices---1827291---------"></a>Ritirare i dispositivi non conformi<!-- 1827291       -->
È stata aggiunta una nuova azione per i dispositivi non conformi che è possibile aggiungere a qualsiasi criterio e consente di [ritirare il dispositivo non conforme](../protect/actions-for-noncompliance.md#add-actions-for-noncompliance).  La nuova azione, **Ritira il dispositivo non conforme**, comporta la rimozione di tutti i dati aziendali dal dispositivo e la rimozione di quest'ultimo dalla gestione di Intune.  Questa azione viene eseguita quando viene raggiunto il valore configurato in giorni e a quel punto il dispositivo diventa idoneo per essere ritirato. Il valore minimo è 30 giorni.  Sarà necessaria l'approvazione esplicita dell'amministratore IT per ritirare i dispositivi usando la sezione *Disattiva i dispositivi non conformi*, in cui gli amministratori possono ritirare tutti i dispositivi idonei.

#### <a name="support-for-wpa-and-wpa2-in-ios-enterprise-wi-fi-profiles--6215273-----"></a>Supporto per WPA e WPA2 nei profili Wi-Fi enterprise per iOS<!--6215273   -->
[I profili Wi-Fi aziendali per iOS](../configuration/wi-fi-settings-ios.md#enterprise-profiles) supportano ora il campo *Tipo di sicurezza*. Per *Tipo di sicurezza*, è possibile selezionare **WPA Enterprise** o **WPA/WPA2 Enterprise**, quindi specificare una selezione per il *tipo EAP*,  (**Dispositivi** > **Profili di configurazione** > **Crea profilo** e selezionare **iOS/iPados** per *Piattaforma*, quindi **Wi-Fi** per *Profilo*). 

Le nuove opzioni aziendali sono simili a quelle disponibili per un profilo Wi-Fi di base per iOS.

#### <a name="new-user-experience-for-certificate-email-vpn-and-wi-fi-vpn-profiles---5615208-----"></a>Nuova esperienza utente per i profili VPN di certificato, posta elettronica, VPN e Wi-Fi<!-- 5615208   -->
È stata aggiornata l'[esperienza utente](../configuration/device-profile-create.md) nell'interfaccia di amministrazione di Endpoint Management (**Dispositivi** > **Profili di configurazione** > **Crea profilo**) per la creazione e la modifica dei tipi di profili seguenti. La nuova esperienza presenta le stesse impostazioni di prima, ma usa un'esperienza di tipo procedura guidata che richiede meno azioni di scorrimento orizzontale. Non è necessario modificare le configurazioni esistenti con la nuova esperienza.

- Credenziale derivata
- Posta elettronica
- Certificato PKCS
- Certificato importato PKCS
- Certificato SCEP
- Certificato attendibile
- Connessione
- Wi-Fi

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Registrazione del dispositivo

#### <a name="configure-if-enrollment-is-available-in-company-portal-for-android-and-ios---4260128----"></a>Stabilire se la registrazione è disponibile nel Portale aziendale per Android e iOS<!-- 4260128  -->
È possibile specificare nella configurazione se la registrazione dei dispositivi nel Portale aziendale sui dispositivi Android e iOS è disponibile con prompt, disponibile senza prompt o non disponibile per gli utenti. Per trovare queste impostazioni in Intune, passare all'[Interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) e selezionare **Amministrazione del tenant** > **Personalizzazione** > **Modifica** > **Registrazione del dispositivo**.  

Il supporto per l'impostazione di registrazione del dispositivo richiede che gli utenti finali abbiano le seguenti versioni del Portale aziendale:
-    Portale aziendale in iOS: versione 4.4 o successiva
-    Portale aziendale in Android: versione 5.0.4715.0 o successiva

Per altre informazioni sulla personalizzazione del Portale aziendale esistente, vedere [Come configurare l'app Portale aziendale di Microsoft Intune](../apps/company-portal-app.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Gestione dei dispositivi

#### <a name="new-android-report-on-android-devices-overview-page---5435435-----"></a>Nuovo report Android nella pagina di panoramica dei dispositivi Android<!-- 5435435   -->
È stato aggiunto un report alla console di amministrazione di Microsoft Endpoint Manager nella pagina di panoramica dei dispositivi Android che visualizza il numero di dispositivi Android registrati in ogni soluzione di gestione dei dispositivi. Questo grafico (corrispondente al grafico già presente nella console di Azure) mostra il numero di dispositivi registrati con profilo di lavoro, completamente gestiti, dedicati e con registrazione di tipo amministratore di dispositivi. Per visualizzare il report, scegliere **Dispositivi** > **Android** > **Panoramica**.

#### <a name="guide-users-from-android-device-administrator-management-to-work-profile-management--5857738-idready-wnready-wnstaged--"></a>Guidare gli utenti dalla gestione degli amministratori dei dispositivi Android alla gestione del profilo di lavoro<!--5857738 idready wnready wnstaged-->
È in corso il rilascio di una nuova impostazione di conformità per la piattaforma degli amministratori dei dispositivi Android. Questa impostazione consente di rendere un dispositivo non conforme se gestito con l'amministratore del dispositivo.

In questi dispositivi non conformi gli utenti visualizzeranno il messaggio **Passa alla configurazione della gestione dei nuovi dispositivi** nella pagina **Aggiorna impostazioni del dispositivo**. Toccando il pulsante **Risolvi**, verranno visualizzate indicazioni dettagliate su:

1. Annullamento della registrazione nella gestione degli amministratori dei dispositivi
2. Registrazione nella gestione del profilo di lavoro
3. Risoluzione dei problemi di conformità 
 
Google sta riducendo il supporto per l'amministratore di dispositivi nelle nuove versioni di Android con l'obiettivo di passare a una gestione dei dispositivi moderna, più ricca e sicura con Android Enterprise.  Intune può offrire supporto completo per i dispositivi Android gestiti dall'amministratore di dispositivi che eseguono Android 10 e versioni successive solo fino al secondo trimestre del 2020. I dispositivi gestiti dall'amministratore di dispositivi (tranne i dispositivi Samsung) che eseguono Android 10 o versione successiva in seguito non potranno più essere gestiti interamente. In particolare, i dispositivi interessati non riceveranno nuovi requisiti per le password. Per altre informazioni, vedere questo [avviso](#decreasing-support-for-android-device-administrator).

Per altre informazioni su questa impostazione, vedere [Aggiornare i dispositivi Android da amministratore di dispositivi alla gestione del profilo di lavoro](../enrollment/android-move-device-admin-work-profile.md). 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Monitorare e risolvere i problemi

#### <a name="the-data-warehouse-now-provides-the-mac-address---6123680----"></a>Il data warehouse ora indica l'indirizzo MAC<!-- 6123680  -->
Il data warehouse di Intune specifica l'indirizzo MAC come nuova proprietà (`EthernetMacAddress`) nell'entità `device` per consentire agli amministratori di eseguire la correlazione tra l'utente e l'indirizzo MAC dell'host. Questa proprietà consente di raggiungere utenti specifici e risolvere i problemi relativi agli eventi imprevisti che si verificano nella rete. Gli amministratori possono usare questa proprietà anche nei [report di Power BI](../developer/reports-proc-get-a-link-powerbi.md) per compilare report più completi. Per altre informazioni, vedere l'entità [dispositivo](../developer/intune-data-warehouse-collections.md#devices) del data warehouse di Intune.

#### <a name="additional-data-warehouse-device-inventory-properties---6125732----"></a>Proprietà aggiuntive per l'inventario dei dispositivi tramite data warehouse<!-- 6125732  -->
Si può accedere alle proprietà aggiuntive per l'inventario dei dispositivi dal data warehouse di Intune. Le proprietà seguenti vengono ora esposte attraverso la raccolta dei [dispositivi](../developer/intune-data-warehouse-collections.md#devices):
- "Model": modello del dispositivo.
- "Office365Version": versione di Office 365 installata nel dispositivo.
- "PhysicalMemoryInBytes": memoria fisica in byte.
- `TotalStorageSpaceInBytes`: capacità di archiviazione totale in byte.

Per altre informazioni, vedere [API data warehouse di Microsoft Intune](../developer/reports-nav-intune-data-warehouse.md) e l'entità [dispositivo](../developer/intune-data-warehouse-collections.md#devices) del data warehouse di Intune.

#### <a name="help-and-support-workflow-update-to-support-additional-services---5654170-----"></a>Guida e supporto per l'aggiornamento del flusso di lavoro per supportare servizi aggiuntivi<!-- 5654170   -->
La pagina Guida e supporto dell'interfaccia di amministrazione di Microsoft Endpoint Manager è stata aggiornata e ora offre la possibilità di [scegliere il tipo di gestione da usare](../fundamentals/get-support.md#options-to-access-help-and-support). Con questa modifica sarà possibile scegliere tra i tipi di gestione seguenti:

- Configuration Manager (include Desktop Analytics)
- Intune
- Co-gestione

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="security"></a>Sicurezza

#### <a name="use-a-preview-of-security-administrator-focused-policies-as-part-of-endpoint-security--6131401----"></a>Usare un'anteprima dei criteri specifici per l'amministratore della sicurezza come parte di Endpoint Security<!--6131401  -->
Come anteprima pubblica, sono stati aggiunti diversi nuovi gruppi di criteri nel nodo Endpoint Security dell'interfaccia di amministrazione di Microsoft Endpoint Management. Gli amministratori della sicurezza possono usare questi nuovi criteri per concentrarsi su aspetti specifici della sicurezza dei dispositivi e gestire gruppi distinti di impostazioni correlate senza il sovraccarico del corpo completo dei criteri di configurazione del dispositivo.

Fatta eccezione per i nuovi *criteri antivirus per Microsoft Defender Antivirus* (vedere di seguito), le impostazioni in ognuno dei nuovi profili e criteri di anteprima sono le stesse che già configurate con i [profili di configurazione dei dispositivi](../configuration/device-profile-create.md).

Di seguito sono riportati i nuovi tipi di criteri disponibili nell'anteprima, con i relativi tipi di profilo:

- **Antivirus (anteprima)** :
  - macOS:
    - **Antivirus**: gestire le [impostazioni dei criteri antivirus](../protect/antivirus-microsoft-defender-settings-macos.md) per macOS per gestire [Microsoft Defender ATP per Mac](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac).

  - Windows 10 e versioni successive:
    - **Microsoft Defender Antivirus**: gestire le [impostazioni dei criteri antivirus](../protect/antivirus-microsoft-defender-settings-windows.md) per la protezione del cloud, le esclusioni dell'antivirus, la correzione, le opzioni di analisi e altro ancora.

      Il profilo Antivirus per *Microsoft Defender Antivirus* è un'eccezione che introduce una nuova istanza di impostazioni rilevate come parte di un profilo di restrizione dei dispositivi. Queste nuove impostazioni di Antivirus:

        - Sono le stesse impostazioni rilevate nelle restrizioni dei dispositivi, ma supportano una terza opzione per la configurazione che non è disponibile se configurata come restrizione dei dispositivi.
        - Si applicano ai dispositivi co-gestiti con Configuration Manager, quando il [dispositivo di scorrimento dei carichi di lavoro di co-gestione](https://docs.microsoft.com/configmgr/comanage/how-to-switch-workloads) per Endpoint Protection è impostato su Intune.

     Pianificare l'uso del nuovo profilo *Antivirus* > *Microsoft Defender Antivirus* anziché configurarle usando un profilo di restrizione dei dispositivi.

  - **Esperienza di Sicurezza di Windows**: gestire le impostazioni di sicurezza di Windows che gli utenti finali possono visualizzare in Microsoft Defender Security Center e le notifiche ricevute dagli utenti. Queste impostazioni sono invariate rispetto a quelle disponibili come profilo Endpoint Protection di configurazione del dispositivo.

- **Crittografia dischi (anteprima)** :
  - macOS:
    - **FileVault**
  - Windows 10 e versioni successive:
    - **BitLocker**
- **Firewall (anteprima)** :
  - macOS:
    - **Firewall macOS**
  - Windows 10 e versioni successive:
    - **Microsoft Defender Firewall**
- **Rilevamento di endpoint e risposta (anteprima)** :
  - Windows 10 e versioni successive: -**Windows 10 Intune**
- **Regole per la riduzione della superficie di attacco (anteprima)** :
  - Windows 10 e versioni successive:
    - **Isolamento di app e browser**
    - **Protezione Web**
    - **Controllo applicazione**
    - **Regole per la riduzione della superficie di attacco**
    - **Controllo del dispositivo**
    - **Protezione dagli exploit**
- **Protezione account (anteprima)** :
  - Windows 10 e versioni successive:
    - **Protezione account**

<!-- ########################## -->
## <a name="week-of-march-9-2020"></a>Settimana del 9 marzo 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Gestione delle app

#### <a name="configure-delivery-optimization-agent-when-downloading-win32-app-content---5410945---"></a>Configurare l'agente di ottimizzazione recapito durante il download del contenuto dell'app Win32<!-- 5410945 -->

È possibile configurare l'agente di ottimizzazione recapito per scaricare il contenuto dell'app Win32 in background o in primo piano in base all'assegnazione. Per le app Win32 esistenti, il contenuto continuerà a essere scaricato in background. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) selezionare **App** > **Tutte le app** > *selezionare l'app Win32* > **Proprietà**. Selezionare l'opzione **Modifica** accanto ad **Assegnazioni**.  Modificare l'assegnazione selezionando **Includi** nell'area **Modalità** della sezione **Richiesto**.  La nuova impostazione sarà visibile nella sezione **Impostazioni app**. Per altre informazioni sull'ottimizzazione recapito, vedere [Gestione delle app Win32 - Ottimizzazione recapito](../apps/apps-win32-app-management.md#delivery-optimization).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Gestione dei dispositivi

#### <a name="change-primary-user-for-windows-devices---3794742-----"></a>Modificare l'utente primario per i dispositivi Windows<!-- 3794742   -->
È possibile modificare l'utente primario per i dispositivi Windows ibridi e aggiunti ad Azure AD. A tale scopo, passare a **Intune** > **Dispositivi** > **Tutti i dispositivi** > scegliere un dispositivo **Proprietà** > **Utente primario**. Per altre informazioni, vedere [Modificare l'utente primario di un dispositivo](../remote-actions/find-primary-user.md#change-a-devices-primary-user).

Per questa attività è stata creata anche una nuova autorizzazione di Controllo degli accessi in base al ruolo (dispositivi gestiti/impostazione utente primario). L'autorizzazione è stata aggiunta a ruoli predefiniti quali: Operatore helpdesk, Amministratore di istituto di istruzione ed Endpoint Security Manager.

Questa funzionalità verrà distribuita ai clienti di tutto il mondo in versione di anteprima. Sarà probabilmente disponibile entro poche settimane.


<!-- ########################## -->
## <a name="week-of-march-2-2020"></a>Settimana del 2 marzo 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Gestione dei dispositivi

#### <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions---6317104-cm3555758--"></a>Connessione del tenant di Microsoft Endpoint Manager: sincronizzazione e azioni dei dispositivi<!-- 6317104, CM3555758-->
Microsoft Endpoint Manager ha riunito Configuration Manager e Intune in un'unica console. A partire dalla versione 2002.2 di Configuration Manager Technical Preview, è possibile caricare i dispositivi Configuration Manager nel servizio cloud ed eseguire le azioni necessarie dall'interfaccia di amministrazione. Per altre informazioni, vedere [Funzionalità in Configuration Manager Technical Preview versione 2002.2](https://docs.microsoft.com/configmgr/core/get-started/2020/technical-preview-2002-2#bkmk_attach).

Prima di installare questo aggiornamento, vedere l'articolo su [Configuration Manager Technical Preview](https://docs.microsoft.com/configmgr/core/get-started/technical-preview). L'articolo consente di acquisire familiarità con i requisiti e le limitazioni generali per l'uso di una Technical Preview, con l'aggiornamento tra le versioni e con l'invio di commenti e suggerimenti.

#### <a name="bulk-remote-actions--4576882--"></a>Azioni remote in blocco<!--4576882-->
È ora possibile eseguire i comandi in blocco per le azioni remote seguenti: riavvio, ridenominazione, reimpostazione di Autopilot, cancellazione ed eliminazione. Per visualizzare le nuove azioni in blocco, passare a [Interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Dispositivi** > **Tutti i dispositivi** > **Azioni in blocco**.

#### <a name="all-devices-list-improved-search-sort-and-filter--6179023--"></a>Funzionalità di ricerca, ordinamento e filtro migliorate per l'elenco Tutti i dispositivi<!--6179023-->
Per l'elenco Tutti i dispositivi sono state migliorate le funzionalità di ricerca, ordinamento, filtro e ottimizzazione delle prestazioni. Per altre informazioni, vedere [questo suggerimento per il supporto](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-changes-in-all-devices-list-and-reporting-in-intune/ba-p/1220946).

<!-- ########################## -->
## <a name="week-of-february-24-2020"></a>Settimana del 24 febbraio 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Gestione delle app

#### <a name="macos-company-portal-user-experience-improvements---5568987---"></a>Miglioramenti dell'esperienza utente per Portale aziendale macOS<!-- 5568987 -->
Sono stati apportati miglioramenti all'esperienza di registrazione dei dispositivi macOS e all'app Portale aziendale per Mac. Verranno apportati i miglioramenti seguenti:
- Una migliore esperienza di Microsoft **AutoUpdate** durante la registrazione che garantirà agli utenti di disporre della versione più recente dell'app Portale aziendale.
- Un passaggio di controllo della conformità migliorato durante la registrazione.
- Supporto per la copia degli ID di evento imprevisto, in modo che gli utenti possano inviare più velocemente errori dai propri dispositivi al team di supporto tecnico aziendale.

Per altre informazioni sulla registrazione e sull'app Portale aziendale per Mac, vedere [Registrare il dispositivo macOS usando l'app Portale aziendale](../user-help/enroll-your-device-in-intune-macos-cp.md).

#### <a name="app-protection-policies-for-better-mobile-now-supports-ios-and-ipados---6224512----"></a>I criteri di protezione delle app per Better Mobile ora supportano iOS e iPadOS<!-- 6224512  -->

A ottobre del 2019, nei criteri di protezione delle app di Intune è stata aggiunta la capacità per usare i dati dei partner di Microsoft Threat Defense. Con questo aggiornamento, è ora possibile usare un criterio di protezione delle app per bloccare o cancellare in modo selettivo i dati aziendali degli utenti in base all'integrità di un dispositivo usando Better Mobile in iOS e iPadOS.  Per altre informazioni, vedere [Creare criteri di protezione delle app Mobile Threat Defense con Intune](../protect/mtd-app-protection-policy.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Gestione dei dispositivi

#### <a name="exports-from-the-all-devices-list--now-in-zipped-csv-format--6343117--"></a>Esportazioni dall'elenco Tutti i dispositivi ora in formato CSV compresso<!--6343117-->
Le esportazioni dalla pagina **Dispositivi** > **Tutti i dispositivi** sono ora in formato CSV compresso.


<!-- ########################## -->
## <a name="week-of-february-17-2020-2002-service-release"></a>Settimana del 17 febbraio 2020 (versione del servizio 2002)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Gestione delle app

#### <a name="microsoft-defender-advanced-threat-protection-atp-app-for-macos---5424618---"></a>App Microsoft Defender Advanced Threat Protection (ATP) per macOS<!-- 5424618 -->
Intune fornisce un modo semplice per distribuire l'app Microsoft Defender Advanced Threat Protection (ATP) per macOS nei dispositivi Mac gestiti. Per altre informazioni, vedere [Aggiungere Microsoft Defender ATP ai dispositivi macOS usando Microsoft Intune](../apps/apps-advanced-threat-protection-macos.md) e [Microsoft Defender Advanced Threat Protection per Mac](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac).  

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Configurazione del dispositivo

#### <a name="enable-network-access-control-nac-with-cisco-anyconnect-vpn-on-ios-devices---4860111----"></a>Abilitare il controllo di accesso alla rete (NAC) con la VPN Cisco AnyConnect nei dispositivi iOS<!-- 4860111  -->
Nei dispositivi iOS è possibile creare un profilo VPN e usare tipi di connessione diversi, tra cui Cisco AnyConnect (**Configurazione del dispositivo** > **Profili** > **Crea profilo** > **iOS** per la piattaforma > **VPN** per il tipo di profilo > **Cisco AnyConnect** per il tipo di connessione).

È possibile abilitare il controllo di accesso alla rete (NAC) con Cisco AnyConnect. Per usare questa funzionalità:

1. In [Cisco Identity Services Engine Administrator Guide](https://www.cisco.com/c/en/us/td/docs/security/ise/2-1/admin_guide/b_ise_admin_guide_21/b_ise_admin_guide_20_chapter_01000.html) seguire la procedura per la **configurazione di Microsoft Intune come server MDM** per configurare Cisco Identity Services Engine (ISE) in Azure.
2. Nel profilo di configurazione del dispositivo di Intune selezionare l'impostazione **Abilita il controllo accesso alla rete**.

Per vedere tutte le impostazioni VPN disponibili, passare a [Configurare le impostazioni VPN nei dispositivi iOS](../configuration/vpn-settings-ios.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Registrazione del dispositivo

#### <a name="serial-number-on-the-apple-mdm-push-certificate-page--5947765----"></a>Numero di serie nella pagina Certificato push MDM Apple<!--5947765  -->
Nella pagina Certificato push MDM Apple ora viene visualizzato il numero di serie. Il numero di serie è necessario per ottenere nuovamente l'accesso al certificato per le notifiche push MDM Apple in caso di impossibilità di accedere all'ID Apple usato per creare il certificato. Per visualizzare il numero di serie, passare a **Dispositivi** > **iOS** > **Registrazione iOS** > **Certificato push MDM Apple**.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Gestione dei dispositivi

#### <a name="new-update-schedule-options-for-pushing-os-updates-to-enrolled-iosipados-devices--5879689----"></a>Nuove opzioni di pianificazione degli aggiornamenti per il push degli aggiornamenti del sistema operativo nei dispositivi iOS/iPadOS registrati<!--5879689  -->
Quando si pianificano gli aggiornamenti del sistema operativo per i dispositivi iOS/iPadOS, è possibile scegliere tra le opzioni seguenti. Questa opzione si applica ai dispositivi che hanno usato i tipi di registrazione Apple Business Manager o Apple School Manager.
- Aggiorna alla sincronizzazione successiva
- Aggiorna durante l'orario pianificato
- Aggiorna in orari diversi da quello pianificato

Per le ultime due opzioni, è possibile creare più finestre temporali.

Per visualizzare le nuove opzioni, passare a MEM > **Dispositivi** > **iOS** > **Criteri di aggiornamento per iOS/iPadOS** > **Crea profilo**.

#### <a name="choose-which-iosipados-updates-to-push-to-enrolled-devices--5879689----"></a>Scegliere gli aggiornamenti di iOS/iPadOS di cui eseguire il push nei dispositivi registrati<!--5879689  -->
È possibile scegliere un aggiornamento specifico di iOS/iPadOS (ad eccezione dell'aggiornamento più recente) per eseguire il push nei dispositivi registrati tramite Apple Business Manager o Apple School Manager. Per i dispositivi di questo tipo devono essere impostati criteri di configurazione del dispositivo per ritardare la visibilità degli aggiornamenti software per un determinato numero di giorni. Per visualizzare questa funzionalità, passare a MEM > **Dispositivi** > **iOS** > **Criteri di aggiornamento per iOS/iPadOS** > **Crea profilo**.



<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Sicurezza del dispositivo

#### <a name="improved-intune-reporting-experience---3791418-----"></a>Ottimizzazione dell'esperienza di creazione di report di Intune<!-- 3791418   -->
Intune offre ora un'esperienza ottimizzata per la creazione dei report, inclusi i nuovi tipi, una migliore organizzazione dei report, visualizzazioni più mirate, funzionalità avanzate per i report, nonché dati più coerenti e tempestivi. L'esperienza di creazione di report passerà dalla versione di anteprima pubblica alla versione disponibile a livello generale. Inoltre, la versione disponibile a livello generale fornirà supporto per la localizzazione, correzioni di bug, miglioramenti della progettazione e dati di conformità dei dispositivi aggregati nei riquadri nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

I nuovi tipi di report sono incentrati sulle informazioni seguenti:

- **Operativo**: contiene record aggiornati concentrati sugli stati negativi dell'integrità. 
- **Organizzativo**: offre un riepilogo più ampio dello stato generale.
- **Cronologico**: offre modelli e tendenze nell'arco di un determinato periodo di tempo.
- **Specialistico**: consente di usare i dati non elaborati per creare i propri report personalizzati.

Il primo set di nuovi report è incentrato sulla conformità del dispositivo. Per altre informazioni, vedere il [post di blog sul framework di reporting di Microsoft Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/New-Reporting-Framework-Coming-to-Intune/ba-p/1009553) e [Report di Intune](reports.md).

#### <a name="consolidated-the-location-of-security-baselines-in-the-ui---6177074-----"></a>Posizione consolidata per le baseline di sicurezza nell'interfaccia utente<!-- 6177074   -->
I percorsi per trovare le [baseline di sicurezza](../protect/security-baselines.md) nell'interfaccia di amministrazione di Microsoft Endpoint Manager sono stati consolidati rimuovendo le *baseline di sicurezza* da diverse posizioni dell'interfaccia utente. Per trovare le baseline di sicurezza, è ora possibile usare il percorso seguente:  **Sicurezza degli endpoint** > **Baseline di sicurezza**.

#### <a name="expanded-support-for-imported-pkcs-certificates---6044197----"></a>Supporto espanso per i certificati PKCS importati<!-- 6044197  -->
È stato esteso il supporto per l'uso di [certificati PKCS importati](../protect/certificates-imported-pfx-configure.md#supported-platforms) in modo da supportare anche *dispositivi Android Enterprise completamente gestiti*. L'importazione di certificati PFX viene in genere usata per gli scenari di crittografia S/MIME, in cui i certificati di crittografia di un utente sono necessari su tutti i dispositivi, in modo che la posta elettronica possa essere decrittografata.

Le piattaforme seguenti supportano l'importazione di certificati PFX:

- Android - Amministratore di dispositivi
- Android Enterprise - Completamente gestito
- Android Enterprise - Profilo di lavoro
- iOS
- Mac
- Windows 10

#### <a name="view-the-endpoint-security-configuration-for-devices---6206460----"></a>Visualizzare la configurazione della sicurezza degli endpoint per i dispositivi<!-- 6206460  -->
Il nome dell'opzione nell'interfaccia di amministrazione di Microsoft Endpoint Manager è stato aggiornato, per visualizzare le [configurazioni della sicurezza degli endpoint applicabili a un dispositivo specifico](../protect/security-baselines-monitor.md#view-endpoint-security-configurations-per-device). Questa opzione è stata rinominata **Configurazione della sicurezza degli endpoint** perché mostra le baseline di sicurezza applicabili e i criteri aggiuntivi creati al di fuori delle baseline di sicurezza. In precedenza, questa opzione era denominata *Baseline di sicurezza*.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>Controllo di accesso in base ai ruoli

#### <a name="intune-roles-user-interface-changes-coming--5801612-----"></a>Modifiche all'interfaccia utente dei ruoli di Intune presto disponibili<!--5801612   -->
L'esperienza utente per [Interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Amministrazione del tenant** > **Ruoli** è stata migliorata per essere più semplice e intuitiva. La nuova esperienza fornisce le stesse impostazioni e gli stessi dettagli attualmente presenti, ma consentirà di visualizzare e definire i ruoli tramite un processo simile a una procedura guidata.

<!-- ########################## -->
## <a name="week-of-february-17-2020"></a>Settimana del 17 febbraio 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Gestione delle app

#### <a name="microsofts-new-office-app---5859926---"></a>Nuova app Office di Microsoft<!-- 5859926 -->
La nuova app Office di Microsoft è ora disponibile a livello generale per il download e l'uso. L'app Office è un'esperienza consolidata in cui gli utenti possono lavorare in Word, Excel e PowerPoint con un'unica app. È possibile fare riferimento all'app con criteri di protezione delle app per assicurarsi che i dati a cui si accede siano protetti.

Per altre informazioni, vedere [Come abilitare i criteri di protezione delle app di Intune con l'app di anteprima per dispositivi mobili Office](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-how-to-enable-intune-app-protection-policies-with/ba-p/1045493).

<!-- ########################## -->

## <a name="week-of-february-10-2020"></a>Settimana del 10 febbraio 2020

### <a name="windows-7-ends-extended-support--3042987---"></a>Fine del supporto esteso di Windows 7<!--3042987 -->
Windows 7 ha raggiunto la fine del supporto esteso il 14 gennaio 2020. Contemporaneamente, è stato deprecato il supporto di Intune per i dispositivi che eseguono Windows 7. L'assistenza tecnica e gli aggiornamenti automatici che consentono di proteggere il PC non sono più disponibili. È consigliabile eseguire l'aggiornamento a Windows 10. Per altre informazioni, vedere il [post del blog relativo al piano di modifica](https://aka.ms/Windows7_Intune).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Gestione delle app

#### <a name="microsoft-edge-version-77-and-later-on-windows-10-devices---5843584---"></a>Microsoft Edge versione 77 e versioni successive nei dispositivi Windows 10<!-- 5843584 -->
Intune supporta ora la disinstallazione di Microsoft Edge versione 77 e successive nei dispositivi Windows 10. Per altre informazioni, vedere [Aggiungere Microsoft Edge per Windows 10 a Microsoft Intune](../apps/apps-windows-edge.md).

#### <a name="screen-removed-from-company-portal-android-work-profile-enrollment--6103987---"></a>Schermata rimossa da Portale aziendale, registrazione del profilo di lavoro Android<!--6103987 -->
La schermata **Passaggi successivi** è stata rimossa dal flusso di registrazione del profilo di lavoro Android in Portale aziendale per semplificare l'esperienza utente. Passare a [Eseguire la registrazione con il profilo di lavoro Android](../user-help/enroll-device-android-work-profile.md) per visualizzare il flusso di registrazione del profilo di lavoro Android aggiornato.  

#### <a name="company-portal-app-improved-performance---6178652---"></a>Miglioramento delle prestazioni dell'app Portale aziendale<!-- 6178652 -->
L'app Portale aziendale è stata aggiornata per supportare prestazioni migliorate per i dispositivi che usano processori ARM64, ad esempio Surface Pro X. In precedenza l'app Portale aziendale funzionava in modalità ARM32 emulata. Nella versione 10.4.7080.0 e successive l'app Portale aziendale è ora compilata in modo nativo per ARM64. Per altre informazioni sull'app Portale aziendale, vedere [Come configurare l'app Portale aziendale di Microsoft Intune](../apps/company-portal-app.md).

<!-- ########################## -->
## <a name="week-of-january-27-2020"></a>Settimana del 27 gennaio 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Gestione delle app

#### <a name="intune-support-for-additional-microsoft-edge-version-77-deployment-channel-for-macos---5983950----"></a>Supporto di Intune per il canale di distribuzione aggiuntivo Microsoft Edge versione 77 per macOS<!-- 5983950  -->
Microsoft Intune ora supporta il canale di distribuzione aggiuntivo **Stabile** per l'app Microsoft Edge per macOS. Il canale **Stabile** è il canale consigliato per la distribuzione su larga scala di Microsoft Edge negli ambienti aziendali. Viene aggiornato ogni sei settimane e ogni versione include miglioramenti derivanti dal canale **Beta**. Oltre ai canali **Stabile** e **Beta**, Intune supporta il canale **Dev**. L'anteprima pubblica offre i canali Stabile e Dev per Microsoft Edge 77 e versioni successive per macOS. Per impostazione predefinita, gli aggiornamenti automatici del browser sono attivati. Per altre informazioni, vedere [Aggiungere Microsoft Edge ai dispositivi macOS usando Microsoft Intune](../apps/apps-edge-macos.md).

#### <a name="retirement-of-intune-managed-browser--5728447---"></a>Ritiro di Intune Managed Browser<!--5728447 -->
Intune Managed Browser verrà ritirato. Usare Microsoft Edge per un'esperienza protetta del browser di Intune. Per altre informazioni, vedere la voce "[Azione: Usare Microsoft Edge per l'esperienza protetta del browser di Intune](whats-new.md#take-action-use-microsoft-edge-for-your-protected-intune-browser-experience)" nella sezione [Notifiche](whats-new.md#notices) più avanti nell'articolo.

<!-- ########################## -->
## <a name="week-of-january-20-2020-2001-service-release"></a>Settimana del 20 gennaio 2020 (versione del servizio 2001)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Gestione delle app

#### <a name="user-experience-change-when-adding-apps-to-intune---4705829-----"></a>Modifica dell'esperienza utente durante l'aggiunta di app a Intune<!-- 4705829   -->
Quando si aggiungono app a Intune, viene visualizzata una nuova esperienza utente. La nuova esperienza rende disponibili le stesse impostazioni e gli stessi dettagli di prima, ma per aggiungere un'app a Intune ora è necessario eseguire un processo simile a una procedura guidata. Questa nuova esperienza mette a disposizione anche una pagina di revisione prima dell'aggiunta dell'app. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) selezionare **App** > **Tutte le app** > **Aggiungi**. Per altre informazioni, vedere [Aggiungere app a Microsoft Intune](../apps/apps-add.md).

#### <a name="require-win32-apps-to-restart----5622282-----"></a>Richiedere il riavvio delle app Win32 <!-- 5622282   -->
È possibile richiedere che un'app Win32 venga riavviata dopo il completamento dell'installazione. È anche possibile scegliere la quantità di tempo, ovvero il periodo di tolleranza, prima che il riavvio venga eseguito.

#### <a name="user-experience-change-when-configuring-apps-in-intune---4207990-----"></a>Modifica dell'esperienza utente durante la configurazione delle app in Intune<!-- 4207990   -->
Verrà visualizzata una nuova esperienza utente durante la creazione di criteri di configurazione delle app in Intune. La nuova esperienza rende disponibili le stesse impostazioni e gli stessi dettagli di prima, ma per aggiungere criteri a Intune ora è necessario eseguire un processo simile a una procedura guidata. Dall'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) selezionare **App** > **Criteri di configurazione dell'app** > **Aggiungi**. Per altre informazioni, vedere [Criteri di configurazione delle app per Microsoft Intune](../apps/app-configuration-policies-overview.md). 

#### <a name="intune-support-for-additional-microsoft-edge-for-windows-10-deployment-channel---5861774---"></a>Supporto di Intune per il canale di distribuzione aggiuntivo Microsoft Edge per Windows 10<!-- 5861774 -->
Microsoft Intune ora supporta il canale di distribuzione aggiuntivo **Stabile** per Microsoft Edge 77 e versioni successive per le app Windows 10. Il canale **Stabile** è il canale consigliato per la distribuzione su larga scala di Microsoft Edge per Windows 10 negli ambienti aziendali. Viene aggiornato ogni sei settimane e ogni versione include miglioramenti derivanti dal canale **Beta**. Oltre ai canali **Stabile** e **Beta**, Intune supporta il canale **Dev**. Per altre informazioni, vedere [Microsoft Edge per Windows 10 - Configurare le impostazioni dell'app](../apps/apps-windows-edge.md#configure-app-settings).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Configurazione del dispositivo

#### <a name="improved-user-interface-experience-when-configuring-exchange-activesync-on-premises-connector-ui---5695492-----"></a>Esperienza dell'interfaccia utente migliorata quando si configura l'interfaccia utente del connettore locale di Exchange ActiveSync<!-- 5695492   -->
L'esperienza dell'interfaccia utente per la [configurazione del connettore locale di Exchange ActiveSync](../protect/exchange-connector-install.md) è stata migliorata. L'esperienza aggiornata usa un unico riquadro per configurare, modificare e riepilogare i dettagli dei connettori locali.

#### <a name="add-automatic-proxy-settings-to-wi-fi-profiles-for-android-enterprise-work-profiles---4490822-----"></a>Aggiungere le impostazioni proxy automatiche ai profili Wi-Fi per i profili di lavoro Android Enterprise<!-- 4490822   -->
Nei dispositivi con profilo di lavoro Android Enterprise è possibile creare profili Wi-Fi. Quando si sceglie il tipo di Wi-Fi Enterprise, è anche possibile immettere il tipo EAP (Extensible Authentication Protocol) usato nella rete Wi-Fi.

A questo punto, quando si sceglie il tipo Enterprise, è anche possibile immettere le impostazioni automatiche del proxy, incluso un URL del server proxy, come ad esempio `proxy.contoso.com`.

Per visualizzare le impostazioni del Wi-Fi correnti che è possibile configurare, vedere [Aggiungere le impostazioni Wi-Fi per i dispositivi che eseguono Android Enterprise e Android in modalità tutto schermo in Microsoft Intune](../configuration/wi-fi-settings-android-enterprise.md#work-profile-only).

Si applica a:
- Profilo di lavoro di Android Enterprise

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Registrazione del dispositivo

#### <a name="block-android-enrollments-by-device-manufacturer--5197392----"></a>Bloccare le registrazioni di dispositivi Android per produttore di dispositivi<!--5197392  -->
È possibile bloccare la registrazione dei dispositivi in base al produttore. Questa funzionalità si applica ai dispositivi con profilo di lavoro amministratore di dispositivi Android e Android Enterprise. Per visualizzare le limitazioni della registrazione, accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Dispositivi** > **Restrizioni registrazione**.

#### <a name="improvements-to-the-iosipados-create-enrollment-type-profile-ui---6055005---"></a>Miglioramenti all'interfaccia utente Crea il profilo del tipo di registrazione per iOS/iPadOS<!-- 6055005 -->
Per la registrazione utente iOS/iPadOS la pagina **Crea il profilo del tipo di registrazione** **Impostazioni** è stata semplificata per migliorare il processo di scelta di **Tipo di registrazione** mantenendo la stessa funzionalità. Per visualizzare la nuova interfaccia utente, passare all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Dispositivi** > **iOS** > **Registrazione iOS** > **Tipi di registrazione** > **Crea profilo** > **Impostazioni**. Per altre informazioni, vedere [Creare un profilo di registrazione utente in Intune](../enrollment/ios-user-enrollment.md#create-a-user-enrollment-profile-in-intune).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Gestione dei dispositivi

#### <a name="new-information-in-device-details---4471759-5604099----"></a>Nuove informazioni nei dettagli del dispositivo<!-- 4471759 5604099  -->
Le informazioni seguenti sono ora presenti nella pagina **Panoramica** per i dispositivi:
- Capacità di memoria (quantità di memoria fisica nel dispositivo)
- Capacità di archiviazione (quantità di risorsa di archiviazione fisica nel dispositivo) 
- Architettura della CPU

#### <a name="ios-bypass-activation-lock-remote-action-renamed-to-disable-activation-lock---5904591----"></a>Azione remota Bypass del blocco attivazione di iOS rinominata Disabilita il blocco attivazione <!--5904591  -->
L'azione remota **Bypass del blocco attivazione** è stata rinominata **Disabilita il blocco attivazione**. Per altre informazioni, vedere [Disabilitare il blocco attivazione di iOS in Intune](../remote-actions/device-activation-lock-disable.md).

#### <a name="windows-10-feature-update-deployment-support-for-autopilot-devices---5948137-----"></a>Supporto per la distribuzione degli aggiornamenti delle funzionalità di Windows 10 per i dispositivi Autopilot<!-- 5948137   -->
Intune supporta ora i dispositivi registrati con Autopilot usando le [distribuzioni di aggiornamenti delle funzionalità di Windows 10](../protect/windows-update-for-business-configure.md#windows-10-feature-updates).

I criteri di aggiornamento delle funzionalità di Windows 10 non possono essere applicati durante la configurazione guidata di Autopilot e verranno applicati solo alla prima analisi di Windows Update dopo il completamento del provisioning di un dispositivo, che richiede in genere un giorno.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Monitorare e risolvere i problemi

#### <a name="windows-autopilot-deployment-reports-preview----3856172-----"></a>Report di distribuzione di Windows Autopilot (anteprima) <!-- 3856172   -->
Un nuovo report presenta informazioni dettagliate su ogni dispositivo distribuito tramite Windows Autopilot. Per altre informazioni, vedere [Report di distribuzione Autopilot](../enrollment/enrollment-autopilot.md#autopilot-deployments-report).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>Controllo di accesso in base ai ruoli

#### <a name="new-intune-built-in-role-endpoint-security-manager--4253397-----"></a>Nuovo ruolo predefinito Endpoint Security Manager in Intune<!--4253397   -->
È disponibile un nuovo ruolo predefinito di Intune, ovvero Endpoint Security Manager. Questo nuovo ruolo offre agli amministratori l'accesso completo al nodo Endpoint Manager in Intune e l'accesso in sola lettura ad altre aree. Il ruolo è un'espansione del ruolo "amministratore della sicurezza" in Azure AD. Se al momento l'unico ruolo disponibile è Amministratori globali, non sono necessarie modifiche. Se si usano i ruoli e si vuole disporre della granularità offerta da Endpoint Security Manager, assegnare questo ruolo quando diventa disponibile. Per altre informazioni sui ruoli predefiniti, vedere [Controllo degli accessi in base al ruolo](role-based-access-control.md).

<!-- ########################## -->
## <a name="week-of-january-6-2020"></a>Settimana del 6 gennaio 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Gestione delle app

#### <a name="smime-support-for-microsoft-outlook-for-ios---2669398---"></a>Supporto S/MIME per Microsoft Outlook per iOS<!-- 2669398 -->
Intune supporta l'emissione di certificati di firma e crittografia S/MIME che possono essere usati con Outlook per iOS nei dispositivi iOS. Per altre informazioni, vedere [Etichette di riservatezza e protezione in Outlook per iOS e Android](https://aka.ms/omsmime).

#### <a name="cache-win32-app-content-using-microsoft-connected-cache-server---6030314---"></a>Memorizzare nella cache il contenuto dell'app Win32 usando il server Microsoft Connected Cache<!-- 6030314 -->
È possibile installare un server Microsoft Connected Cache nei punti di distribuzione di Configuration Manager per memorizzare nella cache il contenuto dell'app Win32 di Intune. Per altre informazioni, vedere [Microsoft Connected Cache in Configuration Manager - Supporto per le app Win32 di Intune](https://docs.microsoft.com/configmgr/core/plan-design/hierarchy/microsoft-connected-cache#bkmk_intune).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>Controllo di accesso in base ai ruoli

#### <a name="windows-10-administrative-templates-admx-profiles-now-support-scope-tags---5137390---"></a>I profili dei modelli amministrativi (ADMX) di Windows 10 ora supportano i tag di ambito <!--5137390 -->
Ora è possibile assegnare tag di ambito ai profili dei modelli amministrativi (ADMX). Per fare ciò passare a **Intune** > **Dispositivi** > **Profili di configurazione** > scegliere un profilo dei modelli amministrativi nell'elenco > **Proprietà** > **Tag di ambito**. Per altre informazioni sui tag di ambito, vedere [Assegnare i tag di ambito ad altri oggetti](../fundamentals/scope-tags.md#assign-scope-tags-to-other-objects).

<!-- ########################## -->
## <a name="week-of-december-30-2019"></a>Settimana del 30 dicembre 2019

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Gestione delle app

#### <a name="retrieve-personal-recovery-key-from-mem-encrypted-macos-devices---4851745---"></a>Recuperare la chiave di ripristino personale dai dispositivi macOS crittografati MEM<!-- 4851745 -->
Gli utenti finali possono recuperare la propria chiave di ripristino personale (chiave di FileVault) usando l'app Portale aziendale iOS. Il dispositivo con la chiave di ripristino personale deve essere registrato in Intune e crittografato con FileVault in Intune. Usando l'app Portale aziendale iOS, un utente finale può recuperare la chiave di ripristino personale nel dispositivo macOS crittografato facendo clic su **Ottieni la chiave di ripristino**. La chiave di ripristino può essere recuperata anche da Intune selezionando **Dispositivi** > *il dispositivo macOS crittografato e registrato* > **Ottieni la chiave di ripristino**. Per altre informazioni su FileVault, vedere [Crittografia FileVault per macOS](../protect/encrypt-devices.md#filevault-encryption-for-macos).

#### <a name="ios-and-ipados-user-licensed-vpp-apps---5619268---"></a>App VPP con licenza utente iOS e iPadOS<!-- 5619268 -->
Per i dispositivi iOS e iPadOS registrati dall'utente, agli utenti finali non verranno più presentate le nuove applicazioni VPP con licenza dispositivo distribuite come disponibili. Gli utenti finali continueranno tuttavia a visualizzare tutte le app VPP con licenza utente all'interno del Portale aziendale. Per altre informazioni sulle app VPP, vedere [Procedura per la gestione delle app iOS e macOS acquistate tramite Volume Purchase Program di Apple con Microsoft Intune](../apps/vpp-apps-ios.md).

<!-- ########################## -->
## <a name="week-of-december-23-2019"></a>Settimana del 23 dicembre 2019

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Gestione delle app

#### <a name="notice---windows-10-1703-rs2-will-be-moving-out-of-support----5026679---"></a>Avviso: scadenza del supporto per Windows 10 1703 (RS2) <!-- 5026679 -->
A partire dal 9 ottobre 2018, non è più previsto il supporto della piattaforma Microsoft per le edizioni Home, Pro e Pro for Workstations di Windows 10 1703 (RS2). Per le edizioni Enterprise ed Education di Windows 10, il supporto della piattaforma per Windows 10 1703 (RS2) è scaduto l'8 ottobre 2019. A partire dal 26 dicembre 2019, la versione minima dell'applicazione Portale aziendale Windows verrà aggiornata a Windows 10 1709 (RS3). I computer che eseguono versioni precedenti alla 1709 non riceveranno più le versioni aggiornate per l'applicazione dal Microsoft Store. Questa modifica è stata già comunicata ai clienti che gestiscono le versioni precedenti di Windows 10 attraverso il centro messaggi. Per altre informazioni, vedere [Date importanti nel ciclo di vita di Windows](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet).

<!-- ########################## -->

## <a name="week-of-december-16-2019"></a>Settimana del 16 dicembre 2019

### <a name="device-configuration"></a>Configurazione del dispositivo

#### <a name="updates-to-administrative-templates-for-windows-10-devices----5941568---"></a>Aggiornamenti di Modelli amministrativi per i dispositivi Windows 10 <!-- 5941568 -->

È possibile usare i modelli ADMX in Microsoft Intune per controllare e gestire le impostazioni per Microsoft Edge, Office e Windows. In Modelli amministrativi di Intune sono ha effettuati i seguenti aggiornamenti delle impostazioni dei criteri:

- Aggiunto il supporto per Microsoft Edge versioni 78 e 79.
- Include i file ADMX dell'11 novembre 2019 nei [file dei modelli amministrativi (ADMX/ADML) e in Strumento di personalizzazione di Office per Office 365 ProPlus, Office 2019 e Office 2016](https://www.microsoft.com/download/details.aspx?id=49030).

Per altre informazioni sui modelli ADMX di Intune, vedere [Usare i modelli di Windows 10 per configurare le impostazioni di criteri di gruppo in Microsoft Intune](../configuration/administrative-templates-windows.md).

Si applica a:

- Windows 10 e versioni successive

## <a name="week-of-december-9-2019-1912-service-release"></a>Settimana del 9 novembre 2019 (versione del servizio 1912)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Gestione delle app

#### <a name="migrating-to-microsoft-edge-for-managed-browsing-scenarios---5173762---"></a>Migrazione a Microsoft Edge per gli scenari di esplorazione gestita<!-- 5173762 -->
Con l'approssimarsi del ritiro di Intune Managed Browser, sono state apportate modifiche ai criteri di protezione delle app per semplificare i passaggi necessari per spostare gli utenti in Edge. Sono state aggiornate le opzioni per l'impostazione dei criteri di protezione delle app **Limita il trasferimento di contenuto Web con altre app**, ovvero una delle seguenti:

- Qualsiasi app
- Intune Managed Browser
- Microsoft Edge
- Browser non gestito 

Quando si seleziona **Microsoft Edge**, gli utenti finali visualizzeranno un messaggio di accesso condizionale che informa che per gli scenari di esplorazione gestita è richiesto Microsoft Edge. Verrà richiesto di scaricare e accedere a Microsoft Edge con i propri account AAD, se non lo hanno già fatto.  Questa operazione equivale ad aver impostato su **true** l'impostazione di configurazione delle app `com.microsoft.intune.useEdge` per le app abilitate per MAM. Per i criteri di protezione delle app esistenti che usavano l'impostazione **Browser gestiti da criteri** sarà ora selezionato **Intune Managed Browser** e non sarà visibile alcuna modifica nel comportamento. Questo significa che gli utenti vedranno il messaggio che richiede l'uso di Microsoft Edge se l'impostazione di configurazione dell'app **useEdge** è stata impostata su **True**. Microsoft invita tutti i clienti che sfruttano gli scenari di esplorazione gestita ad aggiornare i criteri di protezione delle app con **Limita il trasferimento di contenuto Web con altre app** per assicurarsi che gli utenti visualizzino le linee guida appropriate per la transizione a Microsoft Edge, indipendentemente dall'app da cui vengono avviati i collegamenti. 

#### <a name="configure-app-notification-content-for-organization-accounts---2576686----"></a>Configurare il contenuto delle notifiche dell'app per gli account dell'organizzazione<!-- 2576686  -->
I criteri di protezione delle app di Intune nei dispositivi Android e iOS consentono di controllare il contenuto delle notifiche dell'app per gli account dell'organizzazione. È possibile selezionare un'opzione (Consenti, Blocca i dati dell'organizzazione o Bloccato) per specificare la modalità di visualizzazione delle notifiche per gli account dell'organizzazione per l'app selezionata. Questa funzionalità richiede il supporto delle applicazioni e può non essere disponibile per tutte le applicazioni abilitate per i criteri di protezione delle app. Outlook per iOS versione 4.15.0 (o successive) e Outlook per Android 4.83.0 (o versione successiva) supporteranno questa impostazione. L'impostazione è disponibile nella console, ma la funzionalità inizierà a essere applicata dopo il 16 dicembre 2019. Per altre informazioni, vedere [Che cosa sono i criteri di protezione delle app?](../apps/app-protection-policy.md).

#### <a name="microsoft-app-icons-update--4677605----"></a>Aggiornamento delle icone delle app Microsoft<!--4677605  -->
Le icone usate per le app Microsoft nel riquadro di destinazione app per i criteri di protezione delle app e i criteri di configurazione delle app sono state aggiornate.

#### <a name="require-use-of-approved-keyboards-on-android--4761794----"></a>Richiedere l'uso di tastiere approvate in Android<!--4761794  -->
Come parte di un criterio di protezione delle app, è possibile specificare l'impostazione [**Tastiere approvate**](../apps/app-protection-policy-settings-android.md#data-protection) per gestire le tastiere Android che possono essere usate con le app Android gestite. Quando un utente apre l'app gestita e non usa ancora una tastiera approvata per l'app, riceve un messaggio che richiede di passare a una delle tastiere approvate già installate nel dispositivo. Se necessario, viene visualizzato un collegamento per scaricare dal Google Play Store una tastiera approvata che l'utente potrà installare e configurare. L'utente può modificare i campi di testo in un'app gestita solo se la tastiera attiva non è una delle tastiere approvate.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Configurazione del dispositivo

#### <a name="updated-single-sign-on-experience-for-apps-and-websites-on-your-ios-ipados-and-macos-devices---4999578----"></a>Aggiornamento dell'esperienza Single Sign-On per app e siti Web nei dispositivi iOS, iPadOS e macOS<!-- 4999578  -->
Intune ha aggiunto altre impostazioni di Single Sign-On (SSO) per i dispositivi iOS, iPadOS e macOS. È ora possibile configurare le estensioni delle app per l'accesso SSO con reindirizzamento scritte dall'organizzazione o dal provider di identità. Usare queste impostazioni per configurare un'esperienza Single Sign-On senza problemi per le app e i siti Web che usano i metodi di autenticazione moderni, ad esempio OAuth e SAML2. 

Queste nuove impostazioni ampliano le impostazioni precedenti per le estensioni delle app per l'accesso SSO e l'estensione Kerberos incorporata di Apple (**Dispositivi** > **Configurazione del dispositivo** > **Profili** > **Crea profilo** > **iOS/iPadOS** o **macOS** per il tipo di piattaforma > **Funzionalità del dispositivo** per il tipo di profilo). 

Per visualizzare l'intera gamma di impostazioni delle estensioni delle app per l'accesso SSO che è possibile configurare, andare a [SSO in iOS](../configuration/ios-device-features-settings.md#single-sign-on-app-extension) e [SSO in macOS](../configuration/macos-device-features-settings.md#single-sign-on-app-extension).

Si applica a:

- iOS/iPadOS
- macOS

#### <a name="we-have-updated-two-device-restriction-settings-for-ios-and-ipados-devices-to-correct-their-behavior---5701352------"></a>Aggiornate due impostazioni relative alle restrizioni per i dispositivi iOS e iPadOS per correggerne il comportamento<!-- 5701352    -->
Per i dispositivi iOS, è possibile creare profili di restrizione del dispositivo che **consentono gli aggiornamenti PKI in modalità wireless** e **bloccano la modalità USB con restrizioni** (**Dispositivi** > **Configurazione del dispositivo**  > **Profili** > **Crea profilo** > **iOS/iPadOS** per la piattaforma > **Limitazioni del dispositivo** per il tipo di profilo). Prima di questa versione, le impostazioni e le descrizioni dell'interfaccia utente per le impostazioni seguenti non erano esatte e ora sono state corrette. A partire da questa versione, il comportamento delle impostazioni è il seguente:

**Blocca gli aggiornamenti PKI in modalità wireless**: **Blocca** impedisce agli utenti di ricevere gli aggiornamenti software a meno che il dispositivo non sia connesso a un computer. **Non configurato** (impostazione predefinita): consente a un dispositivo di ricevere gli aggiornamenti software senza essere connesso a un computer.
- In precedenza, questa impostazione poteva essere configurata come segue: **Consenti**, per consentire agli utenti di ricevere gli aggiornamenti software senza connettere i propri dispositivi a un computer.
**Consenti gli accessori USB durante il blocco del dispositivo**: Selezionando **Consenti** gli accessori USB sono autorizzati a scambiare dati con un dispositivo che è rimasto bloccato per più di un'ora. **Non configurato** (impostazione predefinita): la modalità con restrizioni USB non viene aggiornata nel dispositivo e agli accessori USB verrà impedito di trasferire i dati dal dispositivo se rimane bloccato per più di un'ora.
- In precedenza, questa impostazione poteva essere configurata come segue: **Blocca**, per disabilitare la modalità USB con restrizioni nei dispositivi con supervisione.

Per altre informazioni sulle impostazioni configurabili, vedere [Impostazioni dei dispositivi iOS e iPadOS per consentire o limitare l'uso delle funzionalità tramite Intune](../configuration/device-restrictions-ios.md).

Questa funzionalità si applica a:

- iOS/iPadOS

#### <a name="wired-network-device-configuration-profiles-for-macos-devices---3508686----"></a>Profili di configurazione della rete cablata per i dispositivi macOS<!-- 3508686  -->
   > [!NOTE]
   > Questa funzionalità è stata posticipata, ma verrà presto rilasciata.

#### <a name="block-users-from-configuring-certificate-credentials-in-the-managed-keystore-on-android-enterprise-device-owner-devices---3311998---"></a>Impedisce agli utenti di configurare le credenziali del certificato nell'archivio chiavi gestito nei dispositivi Android Enterprise con proprietario del dispositivo<!-- 3311998 -->
Nei dispositivi Android Enterprise con proprietario del dispositivo è possibile configurare una nuova impostazione che impedisce agli utenti di configurare le proprie credenziali del certificato nell'archivio chiavi gestito (**Configurazione del dispositivo** > **Profili** > **Crea profilo** > **Android Enterprise** per la piattaforma > **Solo proprietario del dispositivo > Limitazioni del dispositivo** per il tipo di profilo > **Utenti e account**).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Gestione dei dispositivi

#### <a name="protected-wipe-action-now-available--51150000---"></a>Azione di cancellazione protetta ora disponibile<!--51150000 -->
Ora si ha la possibilità di usare l'azione Cancella dispositivo per eseguire una cancellazione protetta dei dati da un dispositivo. Le cancellazioni protette sono identiche a quelle standard, tranne per il fatto che non possono essere eluse spegnendo il dispositivo. Una cancellazione dei dati protetta continuerà a provare a reimpostare il dispositivo fino a quando non riesce. In alcune configurazioni questa azione può impedire il riavvio del dispositivo. Per altre informazioni, vedere [Ritirare o cancellare i dispositivi](../remote-actions/devices-wipe.md).

#### <a name="device-ethernet-mac-address-added-to-devices-overview-page--5562275---"></a>Indirizzo MAC Ethernet del dispositivo aggiunto alla pagina Panoramica del dispositivo<!--5562275 -->
È ora possibile visualizzare l'indirizzo MAC Ethernet del dispositivo nella relativa pagina dei dettagli (**Dispositivi** > **Tutti i dispositivi** > scegliere un dispositivo > **Panoramica**.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Sicurezza del dispositivo

#### <a name="improved-experience-on-a-shared-device-when-device-based-conditional-access-policies-are-enabled---1734096----"></a>Ottimizzata l'esperienza in un dispositivo condiviso quando sono abilitati i criteri di accesso condizionale basato su dispositivi<!-- 1734096  -->
È stata migliorata l'esperienza in un dispositivo condiviso con più utenti a cui sono applicati criteri di accesso condizionale basato su dispositivi controllando la valutazione di conformità più recente per l'utente quando si applicano i criteri. Per altre informazioni, vedere gli articoli sui seguenti argomenti:
- [Panoramica di Azure per l'accesso condizionale](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)
- [Panoramica della conformità dei dispositivi in Intune](../protect/device-compliance-get-started.md)

#### <a name="use-pkcs-certificate-profiles-to-provision-devices-with-certificates---2317124-2317130-2317139-2340517-2340528-2340529----"></a>Usare i profili certificato PKCS per eseguire il provisioning dei dispositivi con certificati<!-- 2317124, 2317130, 2317139, 2340517, 2340528, 2340529  -->
È ora possibile usare i profili certificato PKCS per emettere certificati per i *dispositivi* che eseguono Android for Work, iOS/iPadOS e Windows, se associati a profili come quelli per Wi-Fi e VPN. In precedenza queste tre piattaforme supportavano solo certificati basati sull'utente, con il supporto basato sul dispositivo limitato a macOS.

> [!NOTE]
> I profili di certificato PKCS non sono supportati con i profili Wi-Fi. Usare invece i profili certificato SCEP quando si usa un [tipo EAP](../configuration/wi-fi-settings-windows.md#enterprise-profile).

Per usare un certificato basato sul dispositivo, durante la [creazione di un profilo certificato PKCS](../protect/certficates-pfx-configure.md#create-a-pkcs-certificate-profile) per le piattaforme supportate, selezionare **Impostazioni**. Sarà possibile visualizzare l'impostazione per il **tipo di certificato**, che supporta le opzioni per il dispositivo o l'utente.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Monitorare e risolvere i problemi

#### <a name="centralized-audit-logs--5603185-5697164---"></a>Log di controllo centralizzati<!--5603185, 5697164 -->
Con la nuova gestione centralizzata dei log di controllo ora è possibile riunire i log di controllo di tutte le categorie in un'unica pagina. È possibile filtrare i log per ottenere i dati che si stanno cercando. Per visualizzare i log di controllo, passare ad **Amministrazione del tenant** > **Log di controllo**. 

#### <a name="scope-tag-information-included-in-audit-log-activity-details--5763534---"></a>Informazioni sui tag di ambito incluse nei dettagli attività del log di controllo<!--5763534 -->
I dettagli attività del log di controllo ora includono informazioni sui tag di ambito (per gli oggetti Intune che supportano i tag di ambito). Per altre informazioni sui log di controllo, vedere [Usare i log di controllo per tenere traccia degli eventi e monitorarli](monitor-audit-logs.md).

<!-- ########################## -->
## <a name="week-of-december-2-2019"></a>Settimana del 2 dicembre 2019

#### <a name="new-microsoft-endpoint-configuration-manager-co-management-licensing--5027281--"></a>Nuove licenze di co-gestione di Microsoft Endpoint Configuration Manager<!--5027281-->
I clienti di Configuration Manager con Software Assurance possono ottenere i diritti di co-gestione di Intune per PC Windows 10 senza dover acquistare una licenza di Intune aggiuntiva per la co-gestione. I clienti non devono più assegnare singole licenze Intune/EMS ai propri utenti finali per la co-gestione di Windows 10.
- I dispositivi gestiti da Configuration Manager e registrati per la co-gestione hanno quasi gli stessi diritti di un PC con gestione MDM autonoma di Intune. Tuttavia, dopo la reimpostazione non è possibile eseguire di nuovo il provisioning tramite Autopilot.
- I dispositivi Windows 10 registrati in Intune con altri mezzi richiedono licenze di Intune complete.
- Per i dispositivi in altre piattaforme sono ancora richieste licenze di Intune complete.

Per altre informazioni, vedere [Condizioni di licenza](https://www.microsoft.com/en-us/Licensing/product-licensing/products).

<!-- ########################## -->
## <a name="week-of-november-18-2019-1911-service-release"></a>Settimana del 18 novembre 2019 (versione di servizio 1911)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Gestione delle app

#### <a name="ui-update-when-selectively-wiping-app-data---4102028---"></a>Aggiornamento dell'interfaccia utente quando si cancellano selettivamente i dati delle app<!-- 4102028 -->
L'interfaccia utente per la cancellazione selettiva dei dati delle app in Intune è stata aggiornata. Le modifiche dell'interfaccia utente includono:
- Un'esperienza semplificata con un formato di tipo procedura guidata condensata in un unico riquadro.
- Aggiornamento del flusso di creazione per includere le assegnazioni.
- Una pagina di riepilogo di tutti gli elementi impostati durante la visualizzazione delle proprietà, prima della creazione di un nuovo criterio o quando si modifica una proprietà. Al momento della modifica delle proprietà, inoltre, il riepilogo visualizzerà solo un elenco di elementi all'interno della categoria di proprietà in corso di modifica.

Per altre informazioni, vedere [Come cancellare solo i dati aziendali dalle app gestite da Intune](../apps/apps-selective-wipe.md).

#### <a name="ios-and-ipados-third-party-keyboard-support---4922950---"></a>Supporto per le tastiere di terze parti per iOS e iPadOS<!-- 4922950 -->
Nel marzo 2019 è stata annunciata la rimozione del supporto per l'impostazione dei criteri di protezione delle app iOS "Tastiere di terze parti". La funzionalità è di nuovo disponibile in Intune con supporto sia per iOS che per iPadOS. Per abilitare questa impostazione, visitare la scheda **Protezione dati** di un criterio di protezione nuovo o esistente per le app iOS/iPadOS e trovare l'impostazione **Tastiere di terze parti** in **Trasferimento di dati**.

Il comportamento di questa impostazione dei criteri è leggermente diverso rispetto all'implementazione precedente. Nelle app con più identità che usano l'SDK versione 12.0.16 e successive, soggette a criteri di protezione delle app con questa impostazione configurata su **Blocco**, gli utenti finali non saranno in grado di scegliere le tastiere di terze parti sia nell'organizzazione che negli account personali. Le app che usano le versioni 12.0.12 e precedenti dell'SDK continueranno a presentare il comportamento illustrato nel post di blog relativo ai [problemi dovuti all'assenza del blocco delle tastiere di terze parti in iOS per gli account personali](https://aka.ms/3rdparty_iOS_Intune).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Configurazione del dispositivo

#### <a name="target-macos-user-groups-to-require-jamf-management---4061739----"></a>Definire come destinazione gruppi di utenti macOS per richiedere la gestione Jamf<!-- 4061739  --> 
È possibile definire come destinazione gruppi di utenti specifici i cui [dispositivi macOS verranno gestiti da Jamf](../protect/conditional-access-integrate-jamf.md). La definizione della destinazione consente di applicare l'integrazione di conformità Jamf a un subset di dispositivi macOS mentre altri dispositivi sono gestiti da Intune. Se si sta già usando l'integrazione Jamf, per impostazione predefinita tutti gli utenti verranno definiti come destinazione per l'integrazione.

#### <a name="new-exchange-activesync-settings-when-creating-an-email-device-configuration-profile-on-ios-devices---4892824-----"></a>Nuove impostazioni di Exchange ActiveSync durante la creazione di un profilo di configurazione del dispositivo di posta elettronica nei dispositivi iOS<!-- 4892824   --> 
Nei dispositivi iOS/iPadOS è possibile configurare la connettività di posta elettronica in un profilo di configurazione del dispositivo (**Configurazione del dispositivo** > **Profili** > **Crea profilo** > **iOS/iPadOS** per la piattaforma > **Posta elettronica** per il tipo di profilo). 

Sono disponibili nuove impostazioni di Exchange ActiveSync, tra cui:
- **Dati di Exchange da sincronizzare**: Scegliere i servizi di Exchange da sincronizzare (o di cui bloccare la sincronizzazione) per calendario, contatti, promemoria, note e posta elettronica.
- **Consenti agli utenti di modificare le impostazioni di sincronizzazione**: Consentire, o impedire, agli utenti di modificare le impostazioni di sincronizzazione per questi servizi nei propri dispositivi.  

Per altre informazioni su queste impostazioni, vedere le [impostazioni del profilo di posta elettronica per i dispositivi iOS in Intune](../configuration/email-settings-ios.md). 

Si applica a:

- iOS 13.0 e versioni successive
- iPadOS 13.0 e versioni successive

#### <a name="prevent-users-from-adding-personal-google-accounts-to-android-enterprise-fully-managed-and-dedicated-devices---5353228-----"></a>Impedire agli utenti di aggiungere account Google personali a dispositivi Android Enterprise completamente gestiti e dedicati<!-- 5353228   -->
Nei dispositivi Android Enterprise completamente gestiti e dedicati è disponibile una nuova impostazione che impedisce agli utenti di creare account Google personali (**Configurazione del dispositivo** > **Profili** > **Crea profilo** > **Android Enterprise** per la piattaforma > **Solo proprietario del dispositivo > Limitazioni del dispositivo** per il tipo di profilo > **impostazioni Utenti e account** > **Account Google personale**).

Per visualizzare tutte le impostazioni configurabili, vedere [Impostazioni dei dispositivi Android Enterprise per consentire o limitare funzionalità tramite Intune](../configuration/device-restrictions-android-for-work.md).

Si applica a:

- Dispositivi completamente gestiti Android Enterprise
- Dispositivi dedicati Android Enterprise

#### <a name="server-side-logging-for-siri-commands-setting-is-removed-in-iosipados-device-restrictions-profile----5468501-----"></a>La registrazione lato server per l'impostazione dei comandi Siri viene rimossa nel profilo Limitazioni del dispositivo iOS/iPadOS <!-- 5468501   -->
Nei dispositivi iOS e iPadOS l'impostazione della **registrazione lato server per i comandi Siri** viene rimossa dalla console di amministrazione di Microsoft Endpoint Manager (**Configurazione del dispositivo** > **Profili** > **Crea profilo** > **iOS/iPadOS** per la piattaforma > **Limitazioni del dispositivo** per il tipo di profilo > **App predefinite**). 

Questa impostazione non ha alcun effetto sui dispositivi. Per rimuovere l'impostazione dai profili esistenti, aprire il profilo, apportare le modifiche e quindi salvare il profilo. Il profilo viene aggiornato e l'impostazione viene eliminata dai dispositivi.

Per visualizzare tutte le impostazioni configurabili, vedere [Impostazioni dei dispositivi iOS e iPadOS per consentire o limitare l'uso delle funzionalità tramite Intune](../configuration/device-restrictions-ios.md).

Si applica a:

- iOS/iPadOS

#### <a name="windows-10-feature-updates-public-preview---2384877---"></a>Aggiornamenti delle funzionalità di Windows 10 (anteprima pubblica)<!-- 2384877 -->
È ora possibile distribuire gli [aggiornamenti delle funzionalità di Windows 10](../protect/windows-update-for-business-configure.md#windows-10-feature-updates) ai dispositivi Windows 10. Gli aggiornamenti delle funzionalità di Windows 10 sono nuovi criteri di aggiornamento software che impostano la versione di Windows 10 che si vuole venga installata e mantenuta nei dispositivi. È possibile usare questo nuovo tipo di criteri insieme agli anelli di aggiornamento di Windows 10 esistenti.

I dispositivi che ricevono i criteri di aggiornamento delle funzionalità di Windows 10 installeranno la versione specificata di Windows e rimarranno con tale versione fino a quando i criteri non verranno modificati o rimossi. I dispositivi che eseguono una versione successiva di Windows rimangono alla versione corrente. I dispositivi che mantengono una versione specifica di Windows possono comunque installare gli aggiornamenti di qualità e sicurezza per tale versione dagli anelli di aggiornamento di Windows 10.

Questo nuovo tipo di criteri viene implementato nei tenant a partire da questa settimana. Se questi criteri non sono ancora disponibili per il proprio tenant, lo saranno presto.

#### <a name="add-and-change-key-information-in-plist-files-for-macos-applications---4736278---"></a>Aggiungere e modificare le informazioni fondamentali nei file PLIST per le applicazioni macOS<!-- 4736278 -->
Nei dispositivi macOS è ora possibile creare un profilo di configurazione del dispositivo che carica un file di elenco di proprietà (PLIST) associato a un'app o al dispositivo (**Dispositivi** > **Profili di configurazione** > **Crea profilo** > **macOS** per la piattaforma > **File delle preferenze** per il tipo di profilo).

Solo alcune app supportano le preferenze gestite e queste app potrebbero non consentire la gestione di tutte le impostazioni. Assicurarsi di caricare un file di elenco di proprietà che configuri le impostazioni dei canali del dispositivo e non le impostazioni dei canali degli utenti.

Per altre informazioni su questa funzionalità, vedere [Aggiungere un file elenco di proprietà ai dispositivi macOS usando Microsoft Intune](../configuration/preference-file-settings-macos.md).

Si applica a:

- Dispositivi macOS che eseguono la versione 10.7 e successive

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Gestione dei dispositivi

#### <a name="edit-device-name-value-for-autopilot-devices---2640074---"></a>Modificare il valore del nome dispositivo per i dispositivi Autopilot<!-- 2640074 -->
È possibile modificare il valore Nome dispositivo per i dispositivi Autopilot aggiunti ad Azure AD.  Per altre informazioni, vedere la sezione sulla [modifica degli attributi dei dispositivi Autopilot](../enrollment/enrollment-autopilot.md#edit-autopilot-device-attributes).

#### <a name="edit-group-tag-value-for-autopilot-devices---4816775-----"></a>Modificare il valore del tag di gruppo per i dispositivi Autopilot<!-- 4816775   -->
È possibile modificare il valore Tag di gruppo per i dispositivi Autopilot. Per altre informazioni, vedere la sezione sulla [modifica degli attributi dei dispositivi Autopilot](../enrollment/enrollment-autopilot.md#edit-autopilot-device-attributes).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Monitorare e risolvere i problemi

#### <a name="updated-support-experience---5012398---"></a>Esperienza di supporto tecnico aggiornata<!-- 5012398 -->

A partire da ora, viene implementata nei tenant un'esperienza nella console aggiornata e semplificata per [accedere a Guida e supporto tecnico per Intune](get-support.md). Se questo tipo di esperienza non è ancora disponibile per il proprio tenant, lo sarà presto.

Sono stati migliorati la ricerca e il feedback nella console per i problemi comuni nonché il flusso di lavoro usato per contattare il supporto tecnico. Quando si apre una richiesta di assistenza, vengono visualizzate stime in tempo reale dei tempi previsti per la risposta via telefono o posta elettronica e i clienti Premier e Unified Support hanno la possibilità di indicare la gravità del problema per ricevere più rapidamente assistenza.

#### <a name="improved-intune-reporting-experience-public-preview----3791418---"></a>Ottimizzazione dell'esperienza di creazione di report di Intune (anteprima pubblica) <!-- 3791418 -->
Intune offre ora un'esperienza ottimizzata per la creazione dei report, inclusi i nuovi tipi, una migliore organizzazione dei report, visualizzazioni più mirate, funzionalità avanzate per i report, nonché dati più coerenti e tempestivi. I nuovi tipi di report sono incentrati sugli elementi seguenti:

- **Operativo**: contiene record aggiornati concentrati sugli stati negativi dell'integrità. 
- **Organizzativo**: offre un riepilogo più ampio dello stato generale.
- **Cronologico**: offre modelli e tendenze nell'arco di un determinato periodo di tempo.
- **Specialistico**: consente di usare i dati non elaborati per creare i propri report personalizzati.

Il primo set di nuovi report è incentrato sulla conformità del dispositivo. Per altre informazioni, vedere il [post di blog sul framework di reporting di Microsoft Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/New-Reporting-Framework-Coming-to-Intune/ba-p/1009553) e [Report di Intune](reports.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>Controllo di accesso in base ai ruoli

#### <a name="duplicate-custom-or-built-in-roles----1081938-----"></a>Duplicare ruoli personalizzati o predefiniti <!-- 1081938   -->
È ora possibile copiare i ruoli predefiniti e personalizzati. Per altre informazioni, vedere l'articolo relativo alla [copia di un ruolo](../fundamentals/create-custom-role.md#copy-a-role).

#### <a name="new-permissions-for-school-administrator-role----5621805----"></a>Nuove autorizzazioni per il ruolo di amministratore di istituto di istruzione <!-- 5621805  -->  
Sono state aggiunte due nuove autorizzazioni, **Assegnare il profilo** e **Dispositivo sincronizzato**, al ruolo di amministratore di istituto di istruzione > **Autorizzazioni** > **Programmi di registrazione**. L'autorizzazione del profilo di sincronizzazione consente agli amministratori dei gruppi di sincronizzare i dispositivi di Windows Autopilot. L'autorizzazione Assegnare il profilo consente di eliminare i profili di registrazione Apple avviati dall'utente. Consente inoltre di gestire le assegnazioni dei dispositivi Autopilot e le assegnazioni dei profili di distribuzione Autopilot. Per un elenco di tutte le autorizzazioni per l'amministratore del gruppo o dell'istituto di istruzione, vedere [Assegnare amministratori ai gruppi](https://docs.microsoft.com/intune-education/group-admin-delegate).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="security"></a>Sicurezza

#### <a name="bitlocker-key-rotation---2564951----"></a>Rotazione delle chiavi BitLocker<!-- 2564951  -->
È possibile usare un'azione del dispositivo Intune per [ruotare le chiavi di ripristino di BitLocker](../protect/encrypt-devices.md#rotate-bitlocker-recovery-keys) in modalità remota per i dispositivi gestiti che eseguono Windows versione 1909 o successiva. Per essere idonei alla rotazione delle chiavi di ripristino, i dispositivi devono essere configurati in modo da supportare tale rotazione.  

#### <a name="updates-to-dedicated-device-enrollment-to-support-scep-device-certificate-deployment----5198878----"></a>Aggiornamenti alla registrazione di dispositivi dedicati per supportare la distribuzione del certificato dispositivo SCEP <!-- 5198878  -->
Intune ora supporta la distribuzione del certificato dispositivo SCEP ai dispositivi Android Enterprise dedicati per l'accesso basato su certificati ai profili Wi-Fi. Per il corretto funzionamento della distribuzione, è necessario che l'app Microsoft Intune sia presente nel dispositivo. Di conseguenza, l'esperienza di registrazione per i dispositivi Android Enterprise dedicati è stata aggiornata. Le nuove registrazioni iniziano ancora allo stesso modo (con QR, NFC, Zero Touch o identificatore del dispositivo) ma ora hanno un passaggio che richiede agli utenti di installare l'app di Intune. I dispositivi esistenti inizieranno progressivamente a installare automaticamente l'app.

#### <a name="intune-audit-logs-for-business-to-business-collaboration--5670211---"></a>Log di controllo di Intune per la collaborazione business-to-business<!--5670211 -->
La collaborazione business-to-business (B2B) consente di condividere in modo sicuro le applicazioni e i servizi dell'azienda con gli utenti guest di qualsiasi altra organizzazione, mantenendo al tempo stesso il controllo sui propri dati aziendali. Intune ora supporta i log di controllo per gli utenti guest B2B. Ad esempio, quando gli utenti guest apportano modifiche, Intune sarà in grado di acquisire i dati usando i log di controllo. Per altre informazioni, vedere [Che cos'è l'accesso utente guest in Azure Active Directory B2B?](https://docs.microsoft.com/azure/active-directory/b2b/what-is-b2b)

<!-- ########################## -->
## <a name="week-of-november-11-2019"></a>Settimana del 11 novembre 2019  

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Gestione delle app  

#### <a name="improved-macos-enrollment-experience-in-company-portal----5074349----"></a>Esperienza di registrazione macOS migliorata in Portale aziendale <!-- 5074349  -->  
Il Portale aziendale per l'esperienza di registrazione di macOS prevede un processo di registrazione più semplice che si allinea maggiormente al Portale aziendale per l'esperienza di registrazione di iOS. Gli utenti dei dispositivi ora possono visualizzare:  

- Un'interfaccia utente più accattivante.  
- Un elenco di controllo per la registrazione migliorato.  
- Istruzioni più chiare su come registrare i dispositivi.  
- Opzioni di risoluzione dei problemi migliorate.  

#### <a name="web-apps-launched-from-the-windows-company-portal-app---5030972---"></a>App Web avviate dall'app Windows Portale aziendale<!-- 5030972 -->
Gli utenti finali possono ora avviare app Web direttamente dall'app Windows Portale aziendale. Gli utenti finali possono selezionare l'app Web e quindi scegliere l'opzione **Apri nel browser**. L'URL Web pubblicato viene aperto direttamente in un Web browser. Questa funzionalità verrà implementata nel corso della prossima settimana. Per altre informazioni sull'aggiunta di app Web, vedere [Aggiungere app Web in Microsoft Intune](../apps/web-app.md).  

#### <a name="new-assignment-type-column-in-company-portal-for-windows-10----5459950----"></a>Nuova colonna Tipo di assegnazione in Portale aziendale per Windows 10 <!-- 5459950  -->
La colonna Portale aziendale > **App installate** > **Tipo di assegnazione** è stata rinominata **Richiesta dall'organizzazione**.  In tale colonna verrà visualizzato **Sì** o **No** per indicare se un'app è obbligatoria o facoltativa per l'organizzazione. Queste modifiche sono state apportate perché gli utenti dei dispositivi erano confusi in merito al concetto di app disponibili. Per altre informazioni sull'installazione di app nel Portale aziendale, vedere [Installare e condividere app nel dispositivo](../user-help/install-apps-cpapp-windows.md). Per altre informazioni sulla configurazione dell'app Portale aziendale per gli utenti, vedere [Come configurare l'app Portale aziendale di Microsoft Intune](../apps/company-portal-app.md).  

<!-- ########################## -->
## <a name="week-of-november-4-2019"></a>Settimana del 4 novembre 2019

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Sicurezza del dispositivo

#### <a name="security-baselines-are-supported-on-microsoft-azure-government---4062552---"></a>Le baseline di sicurezza sono supportate in Microsoft Azure per enti pubblici<!-- 4062552 -->

Le istanze di Intune ospitate in *Microsoft Azure per enti pubblici* ora possono usare le [baseline di sicurezza](../protect/security-baselines.md) per la protezione degli utenti e dei dispositivi.

## <a name="whats-new-archive"></a>Archivio delle novità
Per i mesi precedenti, vedere [Novità di Microsoft Intune - Mesi precedenti](whats-new-archive.md).

## <a name="notices"></a>Notifiche

[!INCLUDE [Intune notices](../includes/intune-notices.md)]


