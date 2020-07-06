---
title: Novità di Microsoft Intune - Azure | Microsoft Docs
titleSuffix: ''
description: Informazioni sulle novità nel portale di Intune di Azure
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/25/2020
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
ms.openlocfilehash: 89703c8aec11517417f9459391c431b9db75456c
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/27/2020
ms.locfileid: "85502290"
---
# <a name="whats-new-in-microsoft-intune"></a>Novità di Microsoft Intune

Per informazioni sulle novità di Microsoft Intune ogni settimana, vedere l'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431). oltre ad [avvisi importanti](#notices), [versioni precedenti](whats-new-archive.md) e informazioni su [come vengono rilasciati gli aggiornamenti del servizio Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728). 

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
### Scripts


<!-- ########################## -->

## <a name="week-of-june-22-2020"></a>Settimana del 22 giugno 2020

### <a name="app-management"></a>Gestione delle app

#### <a name="newly-available-protected-apps-for-intune---7248952---"></a>Nuove app protette disponibili per Intune<!-- 7248952 -->
Sono ora disponibili le app protette seguenti:
- BlueJeans Video Conferencing
- Cisco Jabber for Intune
- Tableau Mobile for Intune
- ZERO for Intune

Per altre informazioni, vedere [App protette di Microsoft Intune](../apps/apps-supported-intune-apps.md).

### <a name="monitor-and-troubleshoot"></a>Monitorare e risolvere i problemi

#### <a name="use-endpoint-analytics-to-improve-user-productivity-and-reduce-it-support-costs---5653063---"></a>Usare Analisi degli endpoint per migliorare la produttività degli utenti e ridurre i costi di supporto IT<!-- 5653063 --> 
Questa funzionalità verrà implementata la settimana prossima. La funzionalità Analisi degli endpoint mira a migliorare la produttività dell'utente e a ridurre i costi del supporto IT mettendo a disposizione informazioni approfondite nell'esperienza utente. Tali informazioni consentono al reparto IT di ottimizzare l'esperienza utente con il supporto proattivo e di rilevare eventuali regressioni valutando l'impatto delle modifiche apportate alla configurazione sull'esperienza utente. Per altre informazioni, vedere [Analisi degli endpoint (anteprima)](https://aka.ms/uea).

#### <a name="proactively-remediate-end-user-device-issues-using-script-packages---5933328---"></a>Correggere in modo proattivo i problemi dei dispositivi degli utenti finali usando i pacchetti di script<!-- 5933328 -->
È possibile creare ed eseguire pacchetti di script nei dispositivi degli utenti finali per individuare e risolvere in modo proattivo i principali problemi di supporto dell'organizzazione. La distribuzione di pacchetti di script consentirà di ridurre le chiamate al supporto. È possibile scegliere di creare un pacchetto di script personalizzato o distribuire uno dei pacchetti di script scritti e usati nell'ambiente per ridurre i ticket di supporto. Intune consente di visualizzare lo stato dei pacchetti di script distribuiti e di monitorare i risultati del rilevamento e della correzione. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) selezionare **Report** > **Endpoint Analytics** > **Correzioni proattive**. Per altre informazioni, vedere [Correzioni proattive](https://aka.ms/uea_prs).

### <a name="device-security"></a>Sicurezza del dispositivo

#### <a name="use-microsoft-defender-atp-in-compliance-policies-for-android---4425686----"></a>Usare Microsoft Defender ATP in criteri di conformità per Android<!-- 4425686  -->

È ora possibile usare Intune per [eseguire l'onboarding dei dispositivi Android in Microsoft Defender Advanced Threat Protection](../protect/advanced-threat-protection.md#onboard-android-devices) (Microsoft Defender ATP). Dopo l'onboarding dei dispositivi registrati, i criteri di conformità per Android possono usare i segnali di *livello di minaccia* da Microsoft Defender ATP. Si tratta degli stessi segnali che si potevano usare in precedenza per i dispositivi Windows 10.

#### <a name="configure-defender-atp-web-protection-for-android-devices---6185563-wnready---"></a>Configurare la protezione Web di Defender ATP per dispositivi Android<!-- 6185563 WNReady -->

Quando si usa Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) per i dispositivi Android, è possibile [configurare la protezione Web di Microsoft Defender ATP](../protect/advanced-threat-protection.md#configure-web-protection-on-devices-that-run-android) per disabilitare la funzionalità di analisi del phishing o impedire l'uso della VPN per l'analisi.

A seconda della modalità di registrazione del dispositivo Android in Intune, sono disponibili le opzioni seguenti:

- Amministratore di dispositivi Android - Usare impostazioni OMA-URI personalizzate per disabilitare la funzionalità di protezione Web o disabilitare solo l'uso delle reti VPN durante le analisi.
- Profilo di lavoro Android Enterprise - Usare un profilo di configurazione dell'app e la finestra di progettazione della configurazione per disabilitare tutte le funzionalità di protezione Web.

## <a name="week-of-june-15-2020--2006-service-release"></a>Settimana del 15 giugno 2020 (versione del servizio 2006)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Gestione delle app  

#### <a name="telecommunications-data-transfer-protection-for-managed-apps---6884491----"></a>Protezione del trasferimento dei dati di telecomunicazione per le app gestite<!-- 6884491  -->
Quando viene rilevato un numero di telefono con collegamento ipertestuale in un'app protetta, Intune verificherà se è stato applicato un criterio di protezione che consente il trasferimento del numero a un'app dialer. È possibile scegliere come gestire questo tipo di trasferimento del contenuto quando viene avviato da un'app gestita da criteri. Quando si crea un criterio di protezione delle app in Microsoft Endpoint Manager, selezionare un'opzione di app gestita da **Invia i dati dell'organizzazione ad altre app** e quindi selezionare un'opzione da **Trasferisci i dati delle telecomunicazioni a**. Per altre informazioni su questa impostazione di protezione dei dati, vedere [Impostazioni dei criteri di protezione delle app di Android in Microsoft Intune](../apps/app-protection-policy-settings-android.md) e [Impostazioni dei criteri di protezione delle app iOS](../apps/app-protection-policy-settings-ios.md). 

#### <a name="unified-delivery-of-azure-ad-enterprise-and-office-online-applications-in-the-company-portal---7414033----"></a>Distribuzione unificata di applicazioni Azure AD Enterprise e Office Online nel Portale aziendale<!-- 7414033  -->
Nel riquadro **Personalizzazione** di Intune è possibile selezionare **Nascondi** o **Mostra** sia per le**applicazioni aziendali di Azure AD** che per le **applicazioni Office Online** nel Portale aziendale. Ogni utente visualizzerà l'intero catalogo applicazioni dal servizio Microsoft scelto. Per impostazione predefinita, ogni origine di app aggiuntiva verrà impostata su **Nascondi**. Questa funzionalità verrà applicata inizialmente nel sito Web Portale aziendale, e successivamente verrà supportata nell'app Portale aziendale per Windows. Per trovare questa impostazione di configurazione, nel [centro di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) selezionare **Amministrazione del tenant** > **Personalizzazione**. Per informazioni correlate, vedere [Come personalizzare le app Portale aziendale Intune, il sito Web Portale aziendale e l'app Intune](../apps/company-portal-app.md).

#### <a name="improvements-to-the-company-portal-for-macos-enrollment-experience---6444452----"></a>Miglioramenti apportati al Portale aziendale per l'esperienza di registrazione di macOS<!-- 6444452  -->
Il Portale aziendale per l'esperienza di registrazione di macOS prevede un processo di registrazione più semplice che si allinea maggiormente al Portale aziendale per l'esperienza di registrazione di iOS. Gli utenti dei dispositivi potranno visualizzare:  
- Un'interfaccia utente più accattivante.  
- Un elenco di controllo per la registrazione migliorato.  
- Istruzioni più chiare su come registrare i dispositivi.  
- Opzioni di risoluzione dei problemi migliorate.  

Per altre informazioni sul Portale aziendale, vedere [Come personalizzare le app Portale aziendale Intune, il sito Web Portale aziendale e l'app Intune](../apps/company-portal-app.md).

#### <a name="improvements-to-devices-page-of-iosipados-and-macos-company-portals---6055001---"></a>Miglioramenti alla pagina dispositivi dei portali aziendali iOS/iPadOS e macOS<!-- 6055001 -->
Sono state apportate modifiche alla pagina **Dispositivi** di Portale aziendale per migliorare l'esperienza dell'app per gli utenti di iOS/iPadOS e Mac. Oltre a creare un aspetto più moderno, i dettagli del dispositivo sono stati riorganizzati in una singola colonna con intestazioni di sezione definite, in modo che sia più facile per gli utenti visualizzare lo stato del dispositivo. Sono stati anche aggiunti messaggi più chiari e ulteriori passaggi per la risoluzione dei problemi per gli utenti i cui dispositivi non sono conformi. Per altre informazioni su Portale aziendale, vedere [Come personalizzare le app Portale aziendale Intune, il sito Web Portale aziendale e l'app Intune](../apps/company-portal-app.md). Per sincronizzare manualmente un dispositivo, vedere [Sincronizzare manualmente il dispositivo iOS](../user-help/sync-your-device-manually-ios.md).  

#### <a name="cloud-setting-for-iosipados-company-portal-app---7071303----"></a>Impostazione del cloud per l'app Portale aziendale per iOS/iPadOS<!-- 7071303  -->
Una nuova impostazione **Cloud** per l'app Portale aziendale per iOS/iPadOS consente agli utenti di reindirizzare l'autenticazione verso il cloud appropriato per l'organizzazione. Per impostazione predefinita è configurata l'opzione **Automatico**, che indirizza l'autenticazione verso il cloud rilevato automaticamente dal dispositivo dell'utente. Se l'autenticazione per l'organizzazione deve essere reindirizzata a un cloud diverso da quello rilevato automaticamente (ad esempio pubblico o per enti pubblici), gli utenti possono selezionare manualmente il cloud appropriato selezionando l'app **Impostazioni** > **Portale aziendale** > **Cloud**. Gli utenti devono modificare l'impostazione **Cloud** da **Automatico** solo se accedono da un altro dispositivo e il cloud appropriato non viene rilevato automaticamente dal dispositivo. 

#### <a name="duplicate-apple-vpp-tokens---7101606----"></a>Token VPP Apple duplicati<!-- 7101606  -->
I token VPP Apple con **Posizione del token** identica vengono ora contrassegnati come **Duplicati** e possono essere sincronizzati nuovamente dopo la rimozione del token duplicato. È comunque possibile assegnare e revocare le licenze per i token contrassegnati come duplicati. Tuttavia, le licenze per le nuove app e i libri acquistati potrebbero non essere rispecchiate quando un token viene contrassegnato come duplicato. Per trovare i token VPP di Apple per il tenant, dall'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), selezionare **Amministrazione tenant** > **Connettori e token** > **Token VPP Apple**. Per altre informazioni sui token VPP, vedere [Procedura per la gestione delle app iOS e macOS acquistate tramite Volume Purchase Program di Apple con Microsoft Intune](../apps/vpp-apps-ios.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Configurazione del dispositivo

#### <a name="add-multiple-root-certificates-for-eap-tls-authentication-in-wi-fi-profiles-on-macos-devices---2077871----"></a>Aggiungere più certificati radice per l'autenticazione EAP-TLS nei profili Wi-Fi nei dispositivi macOS<!-- 2077871  -->

Nei dispositivi macOS è possibile creare un profilo Wi-Fi e selezionare il tipo di autenticazione EAP (Extensible Authentication Protocol) (**Dispositivi** > **Profili di configurazione** > **Crea profilo** > **macOS** per la piattaforma > **Wi-Fi** per il profilo > **Tipo Wi-Fi** impostato su Enterprise).

Quando si imposta **Tipo EAP** sull'autenticazione **EAP-TLS**, **EAP-TTLS**o **PEAP**, è possibile aggiungere più certificati radice. In precedenza era possibile aggiungere un solo certificato radice.

Per altre informazioni sulle impostazioni che è possibile configurare, vedere [Aggiungere le impostazioni Wi-Fi per dispositivi macOS in Microsoft Intune](../configuration/wi-fi-settings-macos.md).

Si applica a:
- macOS

#### <a name="use-pkcs-certificates-with-wi-fi-profiles-on-windows-10-and-newer-devices---3246388-----"></a>Usare i certificati PKCS con profili Wi-Fi in Windows 10 e dispositivi più recenti<!-- 3246388   -->
È possibile autenticare i profili Wi-Fi di Windows con certificati SCEP (**Configurazione del dispositivo** > **Profili** > **Crea profilo** > **Windows 10 e versioni successive** per la piattaforma > **Wi-Fi** per il tipo di profilo > **Enterprise** > **Tipo EAP**). È ora possibile usare i certificati PKCS con i profili Wi-Fi di Windows. Questa funzionalità consente agli utenti di autenticare i profili Wi-Fi usando profili certificato PKCS nuovi o esistenti nel tenant. 

Per altre informazioni sulle impostazioni Wi-Fi che è possibile configurare, vedere [Aggiungere le impostazioni Wi-Fi per dispositivi Windows 10 e versioni successive in Intune](../configuration/wi-fi-settings-windows.md).

Si applica a:
- Windows 10 e versioni successive

#### <a name="wired-network-device-configuration-profiles-for-macos-devices---3508686----"></a>Profili di configurazione della rete cablata per i dispositivi macOS<!-- 3508686  -->
È disponibile un nuovo profilo di configurazione dei dispositivi macOS che configura le reti cablate (**Dispositivi** > **Profili di configurazione > **Crea profilo** > **macOS** per la piattaforma > **Rete cablata** per il profilo). Usare questa funzionalità per creare profili 802.1x per gestire le reti cablate e distribuire tali reti nei dispositivi macOS.

Per altre informazioni su questa funzionalità, vedere [Reti cablate nei dispositivi macOS](../configuration/wired-networks-configure.md).

Si applica a:
- macOS

#### <a name="use-microsoft-launcher-as-the-default-launcher-for-fully-managed-android-enterprise-devices---4927976-----"></a>Usare Microsoft Launcher come utilità di avvio predefinita per i dispositivi Android Enterprise completamente gestiti<!-- 4927976   -->
Nei dispositivi per i proprietari di dispositivi Android Enterprise è possibile impostare Microsoft Launcher come utilità di avvio predefinito per i dispositivi completamente gestiti (**Dispositivi** > **Profili di configurazione** > **Crea profilo** > **Android Enterprise** per la piattaforma > **Proprietario dispositivo** > **Restrizioni dei dispositivi** per il profilo > **Esperienza del dispositivo**). Per configurare tutte le altre impostazioni dell'utilità di avvio Microsoft, usare i [criteri di configurazione dell'app](../apps/configure-microsoft-launcher.md). 

Sono inoltre disponibili altri aggiornamenti dell'interfaccia utente, tra cui i **Dispositivi dedicati**, rinominati **Esperienza del dispositivo**.

Per visualizzare tutte le impostazioni configurabili, vedere [Impostazioni dei dispositivi Android Enterprise per consentire o limitare funzionalità tramite Intune](../configuration/device-restrictions-android-for-work.md). 

Si applica a:
- Proprietario del dispositivo Android Enterprise completamente gestito

#### <a name="use-autonomous-single-app-mode-settings-to-configure-the-ios-company-portal-app-to-be-a-sign-insign-out-app---7055619-----"></a>Usare le impostazioni della Modalità applicazione singola autonoma per configurare l'app Portale aziendale iOS come app di accesso/disconnessione<!-- 7055619   -->
Nei dispositivi iOS/iPadOS è possibile configurare le app per l'esecuzione in Modalità applicazione singola autonoma. L'app Portale aziendale supporta ora la Modalità applicazione singola autonoma e può essere configurata come app di accesso/disconnessione. In questa modalità, gli utenti devono accedere all'app Portale aziendale per usare altre app e il pulsante della schermata Home del dispositivo. Quando si disconnettono dall'app Portale aziendale, il dispositivo torna alla modalità app singola e blocca l'app Portale aziendale.

Per configurare l'app Portale aziendale per la Modalità applicazione singola autonoma, passare a **Dispositivi** > **Profili di configurazione** > **Crea profilo** > **iOS/iPadOS** per la piattaforma > **Restrizioni del dispositivo** per il profilo > **Modalità applicazione singola autonoma**.

Per altre informazioni, vedere [Modalità applicazione singola autonoma](../configuration/device-restrictions-ios.md#autonomous-single-app-mode-asam) e [Modalità applicazione singola](https://support.apple.com/guide/mdm/single-app-mode-mdm80a981/1/web/1) (si apre il sito Web di Apple).

Si applica a:
- iOS/iPadOS

#### <a name="configure-content-caching-on-macos-devices---7106872-----"></a>Configurare la memorizzazione del contenuto nella cache nei dispositivi macOS<!-- 7106872   -->
Nei dispositivi macOS è possibile creare un profilo di configurazione che configura la memorizzazione del contenuto nella cache (**Dispositivi** > **Profili di configurazione** > **Crea profilo** > **macOS** per la piattaforma > **Funzionalità del dispositivo** per il profilo). Usare queste impostazioni per eliminare la cache, consentire la memorizzazione nella cache condivisa, impostare un limite della cache sul disco e altro ancora.

Per altre informazioni sulla memorizzazione del contenuto nella cache, vedere [ContentCaching](https://developer.apple.com/documentation/devicemanagement/contentcaching) (viene aperto il sito Web di Apple).

Per visualizzare le impostazioni che è possibile configurare, passare alle [impostazioni delle funzionalità dei dispositivi macOS in Intune](../configuration/macos-device-features-settings.md).

Si applica a:
- macOS

#### <a name="add-new-schema-settings-and-search-for-existing-schema-settings-using-oemconfig-on-android-enterprise---6394386-----"></a>Aggiungere nuove impostazioni dello schema e cercare le impostazioni esistenti usando OEMConfig in Android Enterprise<!-- 6394386   -->
In Intune è possibile usare OEMConfig per gestire le impostazioni dei dispositivi Android Enterprise (**Dispositivi** > **Profili di configurazione** > **Crea profilo** > **Android Enterprise** per la piattaforma > **OEMConfig** per il profilo). Quando si usa **Progettazione configurazione**, vengono visualizzate le proprietà nello schema dell'app. A questo punto, nella finestra di **Progettazione configurazione** è possibile:

- aggiungere nuove impostazioni allo schema dell'app;
- cercare le impostazioni nuove ed esistenti nello schema dell'app.

Per altre informazioni sui profili OEMConfig in Intune, vedere [Usare e gestire i dispositivi Android Enterprise con OEMConfig in Microsoft Intune](../configuration/android-oem-configuration-overview.md).

Si applica a:
- Android Enterprise

#### <a name="block-shared-ipad-temporary-sessions-on-shared-ipad-devices---6613794----"></a>Bloccare le sessioni temporanee di iPad condiviso sui dispositivi iPad condivisi<!-- 6613794  -->
In Intune è disponibile una nuova impostazione **Block Shared iPad temporary sessions** (Blocca le sessioni temporanee di Ipad condiviso) che blocca le sessioni temporanee nei dispositivi iPad condivisi (**Dispositivi** > **Profili di configurazione** > **Crea profilo** > **iOS/iPadOS** per piattaforma > **Restrizioni dei dispositivi** per tipo di profilo> **iPad condiviso**). Se abilitata, gli utenti finali non possono usare l'account Guest, ma devono accedere al dispositivo con l'ID Apple e la password gestiti. 

Per altre informazioni, vedere [Impostazioni dei dispositivi iOS e iPadOS per consentire o limitare l'uso delle funzionalità](../configuration/device-restrictions-ios.md).

Si applica a:
- Dispositivi iPad condivisi che eseguono iOS/iPadOS 13.4 e versioni successive

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Registrazione del dispositivo

#### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344----"></a>I dispositivi BYOD (Bring Your Own Device) possono usare la VPN per la distribuzione<!--5015344  -->
Il nuovo profilo di Autopilot **Ignora il controllo della connettività al dominio** consente di distribuire dispositivi aggiunti ad Azure AD ibrido senza accedere alla rete aziendale usando il proprio client VPN Win32 di terze parti. Per visualizzare il nuovo interruttore, passare all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Dispositivi**  > **Windows** > **Registrazione Windows** > **Profili di distribuzione** > **Crea profilo** > **Configurazione guidata**.

#### <a name="enrollment-status-page-profiles-can-be-set-to-device-groups--3952138---"></a>I profili della pagina relativa allo stato della registrazione possono essere impostati sui gruppi di dispositivi<!--3952138 -->
In precedenza, i profili della pagina relativa allo stato della registrazione potevano essere assegnati solo a gruppi di utenti. È ora possibile impostarli anche su gruppi di dispositivi di destinazione. Per altre informazioni, vedere [Configurare una pagina relativa allo stato della registrazione](../enrollment/windows-enrollment-status.md).

#### <a name="automated-device-enrollment-sync-errors---6988214---"></a>Errori di sincronizzazione nella registrazione automatica dei dispositivi<!-- 6988214 -->
Verranno restituiti nuovi errori per i dispositivi iOS/iPadOS e macOS, tra cui:
- caratteri non validi nel numero di telefono o se il campo è vuoto; 
- nome di configurazione non valido o vuoto per il profilo; 
- valore del cursore non valido/scaduto o cursore non trovato;
- token rifiutato o scaduto; 
- campo relativo al reparto vuoto o troppo lungo; 
- non è stato trovato il profilo da Apple ed è necessario crearne uno nuovo; 
- verrà aggiunto un conteggio dei dispositivi Apple Business Manager rimossi alla pagina di panoramica in cui viene visualizzato lo stato dei dispositivi.

#### <a name="shared-ipads-for-business--6367326-----"></a>IPad condivisi per le aziende<!--6367326   -->
È possibile usare Intune e Apple Business Manager per configurare in modo semplice e sicuro iPad condiviso, in modo che più dipendenti possano condividere i dispositivi. [iPad condiviso](https://developer.apple.com/education/shared-ipad/) di Apple offre un'esperienza personalizzata per più utenti, pur proteggendo i dati dei singoli utenti. Tramite un ID Apple gestito gli utenti possono accedere alle loro app, ai dati e alle impostazioni personali dopo aver eseguito l'accesso a qualsiasi iPad condiviso nell'organizzazione. iPad condiviso funziona con le identità federate.

Per visualizzare questa funzionalità passare all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Dispositivi** > **iOS** > **Registrazione di iOS** > **Token del programma di registrazione** > scegliere un token** > **Profili** > **Crea profilo** > **iOS**. Nella pagina **Impostazioni di gestione** selezionare **Registra senza affinità utente**. Verrà visualizzata l'opzione **iPad condiviso**.

Richiede: iPadOS 13.4 e versioni successive. In questa versione è stato aggiunto il supporto per le sessioni temporanee con iPad condiviso, in modo che gli utenti possano accedere a un dispositivo senza un ID Apple gestito. Al momento della disconnessione, il dispositivo cancella tutti i dati dell'utente e torna a essere immediatamente pronto per l'uso, eliminando la necessità di una cancellazione del dispositivo stesso. 

#### <a name="updated-user-interface-for-apples-automated-device-enrollment--7430322---"></a>Interfaccia utente aggiornata per Registrazione automatica dei dispositivi di Apple<!--7430322 -->
L'interfaccia utente è stata aggiornata per sostituire Device Enrollment Program di Apple con Registrazione automatica dei dispositivi per riflettere la terminologia Apple.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Gestione dei dispositivi

#### <a name="device-remote-lock-pin-available-for-macos--7281557-----"></a>PIN di blocco remoto del dispositivo disponibile per macOS<!--7281557   -->
La disponibilità dei PIN di blocco remoto per i dispositivi macOS è stata aumentata da 7 a 30 giorni.

#### <a name="change-primary-user-on-co-managed-devices--7319183----"></a>Modificare l'utente primario nei dispositivi con co-gestione<!--7319183  -->
È possibile modificare l'utente primario di un dispositivo per i dispositivi Windows con co-gestione. Per altre informazioni su come trovarlo e modificarlo, vedere [Trovare l'utente primario di un dispositivo Intune](../remote-actions/find-primary-user.md). Questa funzionalità verrà distribuita gradualmente nelle prossime settimane.

#### <a name="setting-the-intune-primary-user-also-sets-the-azure-ad-owner-property--7319227---"></a>L'impostazione dell'utente primario di Intune imposta anche la proprietà Owner di Azure AD<!--7319227 -->
Questa nuova funzionalità imposta automaticamente la proprietà Owner nei nuovi dispositivi registrati aggiunti ad Azure AD ibrido nello stesso momento in cui viene impostato l'utente primario di Intune. Per altre informazioni sull'utente primario, vedere [Trovare l'utente primario di un dispositivo Intune](../remote-actions/find-primary-user.md).

Si tratta di una modifica al processo di registrazione che si applica solo ai dispositivi appena registrati. Per i dispositivi aggiunti ad Azure AD ibrido esistenti, è necessario aggiornare manualmente la proprietà Owner di Azure AD. A tale scopo è possibile usare la [funzionalità Modifica l'utente primario](../remote-actions/find-primary-user.md#change-a-devices-primary-user) o [uno script](https://github.com/microsoftgraph/powershell-intune-samples/tree/master/ManagedDevices).

Quando i dispositivi Windows 10 diventano dispositivi ibridi aggiunti ad Azure Active Directory, il primo utente del dispositivo diventa l'utente primario in Endpoint Manager.  Attualmente, l'utente non è impostato sull'oggetto dispositivo Azure AD corrispondente. Questo causa un'incoerenza quando si confronta la proprietà *Owner* da un portale di Azure AD con la proprietà *utente primario* nell'interfaccia di amministrazione di Microsoft Endpoint Manager. La proprietà Owner di Azure AD viene usata per proteggere l'accesso alle chiavi di ripristino di BitLocker. La proprietà non viene popolata nei dispositivi aggiunti ad Azure AD ibrido. Questa limitazione impedisce la configurazione self-service del ripristino di BitLocker da Azure AD. La funzionalità presto disponibile risolve tale limitazione.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Sicurezza del dispositivo

#### <a name="hide-the-recovery-key-from-users-during-filevault-2-encryption-for-macos-devices---5459801----"></a>Nascondere la chiave di ripristino dagli utenti durante la crittografia FileVault 2 per i dispositivi macOS<!-- 5459801  -->
È stata aggiunta una nuova impostazione alla categoria *FileVault* nel modello di [Endpoint Protection per macOS](../protect/endpoint-protection-macos.md#filevault): **Nascondi la chiave di ripristino**. Questa impostazione nasconde la chiave personale all'utente finale durante la crittografia FileVault 2. 

Per visualizzare la chiave di ripristino personale di un dispositivo macOS crittografato, l'utente del dispositivo può accedere a uno dei percorsi seguenti e fare clic su *Ottieni la chiave di ripristino* per il dispositivo macOS: 

- App Portale aziendale iOS/iPadOS
- App Intune
- Sito Web del portale aziendale
- App Portale aziendale Android

#### <a name="support-for-smime-signing-and-encryption-certificates-with-outlook-on-android-fully-managed--5896415-----"></a>Supporto per la firma S/MIME e per i certificati di crittografia con Outlook in Android completamente gestito<!--5896415   -->
È ora possibile usare i certificati per la firma S/MIME e la crittografia con Outlook nei dispositivi che eseguono Android Enterprise completamente gestito.

Questa operazione espande il supporto aggiunto il mese scorso per altre versioni di Android (supporto per i certificati di firma e crittografia S/MIME con Outlook in Android). È possibile effettuare il provisioning dei certificati usando i profili certificato SCEP e PKCS importati.

Per altre informazioni su questo supporto, vedere [Etichette di riservatezza e protezione in Outlook per iOS e Android](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/sensitive-labeling-and-protection-outlook-for-ios-android) nella documentazione di Exchange.

#### <a name="add-a-link-to-your-company-portal-support-website-to-emails-for-noncompliance---7225498------"></a>Aggiungere un collegamento al sito Web di assistenza del portale aziendale per i messaggi di posta elettronica per la non conformità<!-- 7225498    -->
Quando si [configura un modello di messaggio di notifica](../protect/actions-for-noncompliance.md#create-a-notification-message-template) per l'invio di notifiche tramite posta elettronica per la mancata conformità, usare la nuova impostazione **Collegamento del sito Web del Portale aziendale** per includere automaticamente un collegamento al sito Web di Portale aziendale. Se questa opzione è impostata su *Abilita*, gli utenti con dispositivi non conformi che ricevono messaggi di posta elettronica basati su questo modello possono usare il collegamento per aprire un sito Web per accedere ad altre informazioni sul motivo per cui il dispositivo non è conforme. 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="licensing"></a>Licenza

#### <a name="admins-no-longer-require-an-intune-license-to-access-microsoft-endpoint-manager-admin-console--1335430---"></a>Gli amministratori non necessitano più di una licenza di Intune per accedere alla console di amministrazione di Microsoft Endpoint Manager.<!--1335430 -->
È ora possibile impostare un interruttore a livello di tenant che rimuove il requisito di licenza di Intune per gli amministratori per accedere alla console di amministrazione di Microsoft Endpoint Manager ed eseguire query sull'API Graph. Una volta rimosso il requisito di licenza, non sarà mai possibile ripristinarlo. 



<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="scripts"></a>Script 

#### <a name="availability-of-shell-scripts-on-macos-devices---7134839----"></a>Disponibilità di script della shell nei dispositivi macOS<!-- 7134839  -->
Gli script della shell per i dispositivi macOS sono ora disponibili per i clienti del cloud per enti pubblici e Cina. Per altre informazioni sugli script della shell, vedere [Usare script della shell nei dispositivi macOS in Intune](../apps/macos-shell-scripts.md).



<!-- ########################## -->
## <a name="week-of-june-8-2020"></a>Settimana del 8 giugno 2020   

### <a name="app-management"></a>Gestione delle app  

#### <a name="updates-to-informational-screen-in-company-portal-for-iosipados---7032452---"></a>Aggiornamenti della schermata informativa in Portale aziendale per iOS/iPadOS <!--7032452 -->
È stata aggiornata una schermata informativa in Portale aziendale per iOS/iPadOS per illustrare meglio ciò che un amministratore può vedere e fare sui dispositivi. Questi chiarimenti riguardano solo i dispositivi di proprietà dell'azienda. Solo il testo è stato aggiornato. Non sono state apportate modifiche effettive a ciò che l'amministratore può vedere o fare nei dispositivi degli utenti. Per visualizzare le schermate aggiornate, vedere [Aggiornamenti dell'interfaccia utente per le applicazioni degli utenti finali di Intune](./whats-new-app-ui.md).

#### <a name="updated-android-app-conditional-launch-end-user-experience---5736084---"></a>Aggiornamento dell'esperienza utente finale di avvio condizionale dell'app Android<!-- 5736084 -->
La versione 2006 dell'app Portale aziendale Android include modifiche che si basano su aggiornamenti dalla versione 2005. Nella versione 2005 è stato implementato un aggiornamento in cui gli utenti finali dei dispositivi Android che ricevono un avviso, un blocco o una cancellazione da un criterio di protezione delle app visualizzano un messaggio a tutta pagina che descrive il motivo dell'avviso, del blocco o della cancellazione e i passaggi per correggere i problemi. Nella versione 2006, gli utenti che usano l'app Android per la prima volta a cui è assegnato un criterio di protezione delle app dovranno eseguire in modo guidato un flusso per correggere i problemi che causano il blocco dell'accesso all'app. 

<!-- ########################## -->
## <a name="week-of-may-25-2020"></a>Settimana del 25 maggio 2020

### <a name="app-management"></a>Gestione delle app

#### <a name="windows-32-bit-x86-apps-on-arm64-devices---5477661---"></a>App Windows a 32 bit (x86) in dispositivi ARM64<!-- 5477661 -->
Le app Windows a 32 bit (x86) distribuite come disponibili nei dispositivi ARM64 verranno ora visualizzate nel Portale aziendale. Per altre informazioni sulle app Windows a 32 bit, vedere [Gestione di app Win32](../apps/apps-win32-app-management.md).

#### <a name="windows-company-portal-app-icon---7114635---"></a>Icona dell'app Portale aziendale Windows<!-- 7114635 -->
L'icona per l'app Portale aziendale Windows è stata aggiornata. Per altre informazioni sul Portale aziendale, vedere [Come personalizzare le app Portale aziendale Intune, il sito Web Portale aziendale e l'app Intune](../apps/company-portal-app.md).


<!-- ########################## -->
## <a name="week-of-may-18-2020"></a>Settimana del 18 maggio 2020

### <a name="app-management"></a>Gestione delle app  

#### <a name="update-to-icons-in-company-portal-app-for-iosipados-and-macos--6057697---"></a>Aggiornamento delle icone nell'app Portale aziendale per iOS/iPadOS e macOS<!--6057697 -->
Le icone di Portale aziendale sono state aggiornate per creare un aspetto più moderno, supportato sui dispositivi a schermo doppio e allineato al sistema di progettazione Microsoft Fluent. Per visualizzare le icone aggiornate, vedere [Aggiornamenti dell'interfaccia utente per le applicazioni degli utenti finali di Intune](./whats-new-app-ui.md). 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Sicurezza del dispositivo

#### <a name="use-endpoint-detection-and-response-policy-to-onboard-devices-to-defender-atp---7130165----"></a>Usare i criteri di rilevamento e risposta degli endpoint per eseguire l'onboarding dei dispositivi in Defender ATP<!-- 7130165  -->

Usare i criteri di [sicurezza degli endpoint per il rilevamento e la risposta dell'endpoint](../protect/endpoint-security-edr-policy.md) (EDR) per eseguire l'onboarding e la configurazione dei dispositivi per la distribuzione di Microsoft Defender Advanced Threat Protection (Defender ATP). EDR supporta i criteri per i dispositivi Windows gestiti da Intune (MDM) e un criterio separato per i dispositivi Windows gestiti da Configuration Manager. 

Per usare i criteri per i dispositivi di Configuration Manager, è necessario [configurare Configuration Manager per supportare i criteri EDR](../protect/endpoint-security-edr-policy.md#set-up-configuration-manager-to-support-edr-policy). La configurazione include:

- La configurazione di Gestione configurazione per il *collegamento di tenant*.
- L'installazione di un aggiornamento nella console per Configuration Manager per abilitare il supporto per i criteri di EDR. Questo aggiornamento si applica solo alle gerarchie che hanno abilitato il *collegamento di tenant*.
- Sincronizzare le raccolte di dispositivi dalla gerarchia all'interfaccia di amministrazione di Microsoft Endpoint Manager.


<!-- ########################## -->
## <a name="week-of-may-11-2020-2005-service-release"></a>Settimana dell'11 maggio 2020 (versione del servizio 2005)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Gestione delle app

#### <a name="customize-self-service-device-actions-in-the-company-portal--4393379---"></a>Personalizzare le azioni self-service nel Portale aziendale<!--4393379 -->
È possibile personalizzare le azioni del dispositivo self-service disponibili che vengono visualizzate dagli utenti finali nell'app e nel sito Web Portale aziendale. Per contribuire a evitare le azioni non previste nel dispositivo, è possibile configurare queste impostazioni per l'app Portale aziendale selezionando **Amministrazione del tenant** > **Personalizzazione**. Sono disponibili le azioni seguenti:
- Nascondi il pulsante **Rimuovi** nei dispositivi Windows aziendali.
- Nascondi il pulsante **Ripristina** nei dispositivi Windows aziendali.
- Nascondi il pulsante **Ripristina** nei dispositivi iOS aziendali.
- Nascondi il pulsante **Rimuovi** nei dispositivi iOS aziendali.
Per altre informazioni, vedere [Azioni self-service che l'utente può eseguire nel dispositivo dal Portale aziendale](../apps/company-portal-app.md#user-self-service-device-actions-from-the-company-portal).

#### <a name="auto-update-vpp-available-apps---3640511----"></a>Aggiornamento automatico delle app disponibili per VPP<!-- 3640511  -->
Le app che vengono pubblicate come disponibili per il Volume Purchase Program (VPP) di Apple verranno aggiornate automaticamente quando **Aggiornamenti automatici delle app** è abilitata per il token VPP. In precedenza, le app disponibili per VPP non erano aggiornate automaticamente. Gli utenti finali dovevano accedere al Portale aziendale e reinstallare l'app quando risultava disponibile una versione aggiornata. Le app obbligatorie continuano a supportare gli aggiornamenti automatici.




#### <a name="android-company-portal-user-experience---5736084----"></a>Esperienza utente per il Portale aziendale Android<!-- 5736084  -->
Nella versione 2005 del Portale aziendale Android gli utenti finali di dispositivi Android che ricevono un avviso, un blocco o una cancellazione da un criterio di protezione delle app visualizzeranno una nuova esperienza utente. Al posto dell'esperienza corrente con finestra di dialogo corrente, gli utenti finali visualizzeranno un messaggio a tutta pagina che include il motivo dell'avviso, blocco o cancellazione e i passaggi per risolvere il problema. Per altre informazioni, vedere [Esperienza di protezione delle app per dispositivi Android](../apps/app-protection-policy.md#app-protection-experience-for-android-devices) e [Impostazioni dei criteri di protezione delle app di Android in Microsoft Intune](../apps/app-protection-policy-settings-android.md).

#### <a name="support-for-multiple-accounts-in-company-portal-for-macos---5779449----"></a>Supporto di più account nel Portale aziendale per macOS<!-- 5779449  -->
Il Portale aziendale nei dispositivi macOS ora memorizza nella cache gli account utente, semplificando l'accesso. Non è più necessario che gli utenti eseguano l'accesso al Portale aziendale ogni volta che avviano l'applicazione. Se nella cache sono memorizzati più account, il Portale aziendale visualizzerà anche un selettore di account, in modo che gli utenti non debbano immettere il nome utente. 

#### <a name="newly-available-protected-apps---7060934-----"></a>Nuove app protette disponibili<!-- 7060934   -->
Sono ora disponibili le app protette seguenti:
- Board Papers
- Breezy per Intune
- Hearsay Relate per Intune
- ISEC7 Mobile Exchange Delegate per Intune
- Lexmark per Intune
- Meetio Enterprise
- Microsoft Whiteboard
- Now® Mobile - Intune
- Qlik Sense Mobile 
- ServiceNow® Agent - Intune
- Onboarding® ServiceNow - Intune
- Smartcrypt per Intune
- Tact per Intune
- Zero - Client di posta elettronica per avvocati

Per altre informazioni, vedere [App protette di Microsoft Intune](../apps/apps-supported-intune-apps.md).

#### <a name="search-the-intune-docs-from-the-company-portal---1736480-----"></a>Ricerca nella documentazione di Intune dal Portale aziendale<!-- 1736480   -->
Ora è possibile eseguire ricerche nella documentazione di Intune direttamente dall'app Portale aziendale per macOS. Nella barra dei menu selezionare **Guida** > **Cerca** e immettere le parole chiave della ricerca per trovare rapidamente risposte alle domande.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Configurazione del dispositivo

#### <a name="improvements-to-oemconfig-support-for-zebra-technologies-devices---4184154---"></a>Miglioramenti al supporto di OEMConfig per i dispositivi Zebra Technologies<!-- 4184154 -->
Intune supporta tutte le funzionalità offerte da Zebra OEMConfig. I clienti che gestiscono dispositivi Zebra Technologies con Android Enterprise e OEMConfig possono distribuire più profili OEMConfig in un unico dispositivo. I clienti possono anche visualizzare report avanzati sullo stato dei profili Zebra OEMConfig.

Per altre informazioni, vedere [Distribuire più profili OEMConfig nei dispositivi Zebra in Microsoft Intune](../configuration/oemconfig-zebra-android-devices.md).

Non sono state apportate modifiche al comportamento di OEMConfig per altri OEM.

Si applica a:
- Android Enterprise
- Dispositivi Zebra Technologies che supportano OEMConfig. Contattare Zebra per ricevere dettagli specifici sul supporto.

#### <a name="configure-system-extensions-on-macos-devices---6255624---"></a>Configurare le estensioni del sistema nei dispositivi macOS<!-- 6255624 -->
Nei dispositivi macOS è possibile creare un profilo di estensioni del kernel per configurare impostazioni a livello del kernel (**Dispositivi** > **Profili di configurazione** > **macOS** per la piattaforma > **Estensioni del kernel** per il profilo). Apple prevede di impostare come deprecate le estensioni del kernel e di sostituirle con estensioni del sistema in una versione futura.

Le estensioni del sistema vengono eseguite nello spazio dell'utente e non hanno accesso al kernel. L'obiettivo è aumentare la protezione e garantire un maggior controllo a livello dell'utente finale, limitando nel contempo gli attacchi a livello del kernel. Sia le estensioni del kernel sia le estensioni del sistema consentono agli utenti di installare estensioni delle app che incrementano la capacità nativa del sistema operativo.

In Intune è possibile configurare le estensioni del kernel e le estensioni del sistema (**Dispositivi** > **Profili di configurazione** > **macOS** per la piattaforma > **Estensioni del sistema** per il profilo). Le estensioni del kernel sono valide per la versione 10.13.2 e versioni successive. Le estensioni del sistema sono valide per la versione 10.15 e versioni successive. Da macOS 10.15 a macOS 10.15.4, le estensioni del kernel e le estensioni del sistema possono essere eseguite simultaneamente. 

Per informazioni sulle estensioni nei dispositivi macOS, vedere [Aggiungere le estensioni macOS](../configuration/kernel-extensions-overview-macos.md).

Si applica a:
- macOS 10.15 e versioni successive

#### <a name="configure-app-and-process-privacy-preferences-on-macos-devices---2934232-----"></a>Configurare le preferenze per la privacy di app e processi nei dispositivi macOS<!-- 2934232   --> 
Nella versione di macOS Catalina 10.15 Apple ha aggiunto nuovi miglioramenti alla sicurezza e alla privacy. Per impostazione predefinita, le applicazioni e i processi non riescono ad accedere a dati specifici senza il consenso utente. Se gli utenti non danno il consenso, le applicazioni e i processi potrebbero non funzionare. In Intune verrà aggiunto il supporto per le impostazioni che permettono agli amministratori IT di accettare o rifiutare il consenso per l'accesso ai dati per conto degli utenti finali nei dispositivi che eseguono macOS 10.14 e versioni successive. Queste impostazioni garantiscono che le applicazioni e i processi continuino a funzionare correttamente e riducono il numero di richieste. 

Per altre informazioni sulle impostazioni che è possibile gestire, vedere [Preferenze per la privacy di macOS](../configuration/device-restrictions-macos.md#privacy-preferences).

Si applica a:
- macOS 10.14 e versioni successive

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Registrazione del dispositivo

#### <a name="enrollment-restrictions-support-scope-tags--4209550----"></a>Le restrizioni di registrazione supporta i tag di ambito<!--4209550  -->
È ora possibile assegnare tag di ambito alle restrizioni di registrazione. A tale scopo accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Dispositivi** > **Restrizioni registrazione** > **Crea restrizione**. Creare uno dei due tipi di restrizione. Verrà visualizzata la pagina **Tag di ambito**. Per altre informazioni, vedere [Impostare le restrizioni di registrazione](../enrollment/enrollment-restrictions-set.md).

#### <a name="autopilot-support-for-hololens-2-devices--6305220----"></a>Supporto dei dispositivi Hololens 2 in Autopilot<!--6305220  -->
Windows Autopilot ora supporta i dispositivi Hololens 2. Per altre informazioni sull'uso di Autopilot per Hololens, vedere [Windows Autopilot per HoloLens 2](https://docs.microsoft.com/hololens/hololens2-autopilot).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Gestione dei dispositivi

#### <a name="use-sync-remote-action-in-bulk-for-ios--6440956--idmiss--"></a>Usare l'azione remota di sincronizzazione in blocco per iOS<!--6440956  idmiss-->
È ora possibile usare l'azione remota di sincronizzazione su un massimo di 100 dispositivi iOS alla volta. Per visualizzare la nuova caratteristica, passare a [Interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Dispositivi** > **Tutti i dispositivi** > **Azioni in blocco del dispositivo**. 

#### <a name="automated-device-sync-interval-down-to-12-hours--3077535----"></a>Intervallo di sincronizzazione automatica dei dispositivi ridotto a 12 ore<!--3077535  -->
Per la Registrazione automatica dei dispositivi di Apple, l'intervallo di sincronizzazione automatica dei dispositivi tra Intune e Apple Business Manager sarà ridotto da 24 a 12 ore. Per altre informazioni sulla sincronizzazione, vedere [Sincronizzare i dispositivi gestiti](../enrollment/device-enrollment-program-enroll-ios.md#sync-managed-devices).


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Sicurezza del dispositivo

#### <a name="derived-credentials-support-for-disa-purebred-on-android-devices---6939073-------"></a>Supporto di credenziali derivate per DISA Purebred nei dispositivi Android<!-- 6939073     -->
È ora possibile usare *DISA Purebred* come provider di [credenziali derivate](../protect/derived-credentials.md) nei dispositivi Android Enterprise completamente gestiti. Il supporto per il recupero di una credenziale derivata per DISA Purebred è incluso. Sarà possibile usare una credenziale derivata per l'autenticazione di app, Wi-Fi, VPN o la firma S/MIME e/o la crittografia, se supportata dalle app. 

#### <a name="send-push-notifications-as-an-action-for-noncompliance----1733150-----"></a>Inviare notifiche push come azione per la mancata conformità <!-- 1733150   -->
È ora possibile configurare un'[azione per mancata conformità](../protect/actions-for-noncompliance.md#available-actions-for-noncompliance) che invia una notifica push a un utente quando il dispositivo dell'utente non soddisfa le condizioni dei criteri di conformità. La nuova azione corrisponde a **Inviare una notifica push all'utente finale**ed è supportata nei dispositivi Android e iOS.

Quando gli utenti selezionano la notifica push nel dispositivo, viene visualizzata l'app Portale aziendale o Intune che mostra i dettagli del motivo della mancata conformità.

#### <a name="endpoint-security-content-and-new-features---5720009-5892558-7130145-5653324-7140602----"></a>Contenuto della sicurezza degli endpoint e nuove caratteristiche<!-- 5720009 5892558, 7130145, 5653324, 7140602  -->

La documentazione relativa a [Sicurezza degli endpoint](../protect/endpoint-security.md) di Intune è ora disponibile. Nel nodo Sicurezza degli endpoint dell'interfaccia di amministrazione di Microsoft Endpoint Manager è possibile:

- Creare e distribuire criteri di sicurezza mirati per i dispositivi gestiti
- Configurare l'integrazione con Microsoft Defender Advanced Threat Protection, inoltre gestire le attività di sicurezza consente a correggere i rischi per i dispositivi a rischio identificati dal team ATP
- Gestire le baseline di sicurezza
- Monitorare i criteri di conformità e di accesso condizionale del dispositivo
- Visualizzare lo stato di conformità per tutti i dispositivi sia da Intune che da Configuration Manager quando Configuration Manager è configurato per la connessione client.

Oltre alla disponibilità del contenuto, di seguito sono riportate le novità per la sicurezza degli endpoint di questo mese:

- I [**criteri di sicurezza degli endpoint**](../protect/endpoint-security-policy.md) **non sono visibili in**  ***anteprima*** e sono ora pronti per l'uso in ambienti di produzione, come *disponibili a livello generale*, con due eccezioni:

  - In una nuova *anteprima pubblica*, è possibile usare il profilo [**Regole di Microsoft Defender Firewall**](../protect/endpoint-security-firewall-policy.md#firewall-profiles) per i criteri del firewall di Windows 10. Con ogni istanza del profilo è possibile configurare fino a 150 regole del firewall per completare i profili di Microsoft Defender Firewall. 
  - I criteri di sicurezza per la protezione account restano in anteprima. 

- È ora possibile [**creare un duplicato dei criteri di sicurezza degli endpoint**](../protect/endpoint-security-policy.md#duplicate-a-policy). I duplicati mantengono la configurazione delle impostazioni dei criteri originali, ma ottengono un nuovo nome. Quindi, la nuova istanza dei criteri non include le assegnazioni ai gruppi fino a quando non si modifica la nuova istanza del criterio per aggiungerle. È possibile duplicare i criteri seguenti:
  - Antivirus
  - Crittografia del disco
  - Firewall
  - Rilevamento di endpoint e risposta
  - Riduzione della superficie di attacco
  - Protezione account

- È ora possibile [**creare un duplicato della baseline di sicurezza**](../protect/security-baselines.md#duplicate-a-security-baseline). I duplicati mantengono la configurazione delle impostazioni dei criteri originali, ma ottengono un nuovo nome. Quindi, la nuova istanza della baseline non include le assegnazioni ai gruppi fino a quando non si modifica la nuova istanza del criterio per aggiungerle.

- È disponibile un nuovo report per i criteri antivirus di degli endpoint di sicurezza: [**Endpoint non integri di Windows 10**](../protect/endpoint-security-antivirus-policy.md#windows-10-unhealthy-endpoints). Questo report è una nuova pagina che è possibile selezionare quando si visualizzano i criteri antivirus per la protezione degli endpoint. Il report visualizza lo stato antivirus dei dispositivi Windows 10 gestiti da MDM.  

#### <a name="support-for-smime-signing-and-encryption-certificates-with-outlook-on-android---7207474----"></a>Supporto per la firma S/MIME e per i certificati di crittografia con Outlook in Android<!-- 7207474  -->
È ora possibile usare i certificati per la firma S/MIME e la crittografia con Outlook in Android. Grazie a questo supporto è possibile effettuare il provisioning dei certificati usando i profili certificato SCEP, PKCS e PKCS importati. Sono supportate le piattaforme Android seguenti:

- Profilo di lavoro di Android Enterprise
- Amministratore di dispositivi Android

Il supporto esteso per i dispositivi Android Enterprise completamente gestiti sarà presto disponibile.

Per altre informazioni su questo supporto, vedere [Etichette di riservatezza e protezione in Outlook per iOS e Android](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/sensitive-labeling-and-protection-outlook-for-ios-android) nella documentazione di Exchange.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Monitorare e risolvere i problemi

#### <a name="device-reports-ui-update---6269408---"></a>Aggiornamento dell'interfaccia utente dei report del dispositivo<!-- 6269408 -->
Nel riquadro Panoramica sui report sono ora disponibili le schede **Riepilogo** e **Report**. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), selezionare **Report**, quindi selezionare la scheda **Report** per visualizzare i tipi di report disponibili. Per informazioni correlate, vedere [Report di Intune](../fundamentals/reports.md).


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="scripting"></a>Scripting

#### <a name="macos-script-support---6376978----"></a>Supporto degli script per macOS<!-- 6376978  -->
Il supporto degli script per macOS è ora disponibile a livello generale. Abbiamo aggiunto anche il supporto per gli script assegnati all'utente e per i dispositivi macOS registrati con Registrazione automatica del dispositivo di Apple (in precedenza Device Enrollment Program). Per altre informazioni, vedere [Usare gli script della shell nei dispositivi macOS in Intune](../apps/macos-shell-scripts.md).


<!-- ########################## -->
## <a name="week-of-may-4-2020"></a>Settimana del 4 maggio 2020  

### <a name="company-portal-for-android-guides-users-to-get-apps-after-work-profile-enrollment----6103999---"></a>Il Portale aziendale per Android consente agli utenti di ottenere le app dopo la registrazione del profilo di lavoro <!-- 6103999 -->
Sono state migliorate le linee guida all'interno del Portale aziendale, in modo da facilitare la ricerca e l'installazione di app per gli utenti. Dopo aver eseguito la registrazione nella gestione del profilo di lavoro, gli utenti visualizzeranno un messaggio che spiega come trovare le app suggerite nella versione con badge di Google Play. L'ultimo passaggio in [Registrare il dispositivo con il profilo Android](../user-help/enroll-device-android-work-profile.md) è stato aggiornato in modo da visualizzare il nuovo messaggio. Gli utenti visualizzeranno anche un nuovo collegamento **Scarica app** nel menu di spostamento del Portale aziendale sul lato sinistro. Per dare più spazio a queste esperienze nuove e migliorate, la scheda **APP** è stata rimossa. Per visualizzare le schermate aggiornate, vedere [Aggiornamenti dell'interfaccia utente per le applicazioni degli utenti finali di Intune](./whats-new-app-ui.md). 

<!-- ########################## -->
## <a name="week-of-april-20-2020"></a>Settimana del 20 aprile 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Gestione dei dispositivi

#### <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions---6317104-cm3555758----"></a>Connessione del tenant di Microsoft Endpoint Manager: sincronizzazione e azioni dei dispositivi<!-- 6317104, CM3555758  -->
Microsoft Endpoint Manager ha riunito Configuration Manager e Intune in un'unica console. A partire da Configuration Manager versione 2002, è possibile caricare i dispositivi Configuration Manager nel servizio cloud ed eseguire le azioni necessarie dall'interfaccia di amministrazione. Per altre informazioni, vedere [Collegamento del tenant di Microsoft Endpoint Manager: sincronizzazione e azioni dei dispositivi](../../configmgr/tenant-attach/device-sync-actions.md). 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Gestione delle app

#### <a name="microsoft-office-365-proplus-rename---6368143---"></a>Nuovo nome per Microsoft Office 365 ProPlus<!-- 6368143 -->
È in corso la modifica del nome di Microsoft Office 365 ProPlus in **App di Microsoft 365 per grandi imprese**. Per altre informazioni, vedere [Modifica del nome di Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change). Nella nostra documentazione si parlerà generalmente di App di Microsoft 365. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) è possibile trovare la suite di app selezionando **App** > **Windows** > **Aggiungi**. Per informazioni sull'aggiunta di app, vedere [Aggiungere app in Microsoft Intune](../apps/apps-add.md).

<!-- ########################## -->
## <a name="week-of-april-13-2020-2004-service-release"></a>Settimana del 13 aprile 2020 (versione del servizio 2004)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Gestione delle app

#### <a name="manage-smime-settings-for-outlook-on-android-enterprise-devices---6517085-----"></a>Gestire le impostazioni S/MIME per Outlook in dispositivi Android Enterprise<!-- 6517085   -->
È possibile usare criteri di configurazione delle app per gestire l'impostazione S/MIME per Outlook nei dispositivi che eseguono Android Enterprise. È anche possibile scegliere se consentire o meno agli utenti del dispositivo di abilitare o disabilitare S/MIME nelle impostazioni di Outlook. Per usare criteri di configurazione delle app per Android, nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) passare ad **App** > **Criteri di configurazione dell'app**  > **Aggiungi** > **Dispositivi gestiti**. Per altre informazioni sulla configurazione delle impostazioni per Outlook, vedere [Impostazioni di configurazione di Microsoft Outlook](../apps/app-configuration-policies-outlook.md).

#### <a name="pre-release-testing-for-managed-google-play-apps---2681933----"></a>Test della versione preliminare per le app gestite di Google Play<!-- 2681933  -->
Le organizzazioni che usano [percorsi di test chiusi di Google Play per i test di versioni non definitive dell'app](https://support.google.com/googleplay/android-developer/answer/3131213) possono gestire questi percorsi con Intune. È possibile assegnare in modo selettivo app pubblicate nei percorsi di pre-produzione di Google Play ai gruppi pilota per eseguire i test. In Intune è anche possibile verificare se per un'app è stato pubblicato un percorso di test di compilazione di pre-produzione, oltre a poter assegnare tale percorso a gruppi di utenti o di dispositivi di AAD. Questa funzionalità è disponibile per tutti gli scenari di Android Enterprise attualmente supportati (profilo di lavoro, completamente gestito e dedicato). Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) è possibile aggiungere un'app Google Play gestita selezionando **App** > **Android** > **Aggiungi**. Per altre informazioni, vedere [Uso di tracce di test chiuse di Google Play gestito](../apps/apps-add-android-for-work.md#working-with-managed-google-play-closed-testing-tracks).

#### <a name="microsoft-teams-is-now-included-in-the-office-365-suite-for-macos---5903936----"></a>Microsoft Teams è ora incluso nella famiglia di prodotti Office 365 per macOS<!-- 5903936  -->
Gli utenti a cui viene assegnato Microsoft Office per macOS in Microsoft Endpoint Manager riceveranno ora Microsoft Teams oltre alle app Microsoft Office esistenti (Word, Excel, PowerPoint, Outlook e OneNote). Intune rileverà i dispositivi Mac esistenti nei quali sono installate altre app Office per macOS e tenterà di installare Microsoft Teams in occasione della successiva sincronizzazione del dispositivo con Intune. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) è possibile trovare **Famiglia di prodotti Office 365** per macOS selezionando **App** > **macOS** > **Aggiungi**. Per altre informazioni, vedere [Assegnare Office 365 a dispositivi macOS con Microsoft Intune](../apps/apps-add-office365-macos.md).

#### <a name="update-to-android-app-configuration-policies---6113334----"></a>Aggiornamento dei criteri di configurazione delle app Android<!-- 6113334  -->
I criteri di configurazione delle app Android sono stati aggiornati per consentire agli amministratori di selezionare il tipo di registrazione del dispositivo prima di creare un profilo di configurazione dell'app. È in corso l'aggiunta della funzionalità per tenere conto dei profili certificato basati sul tipo di registrazione (Profilo di lavoro o Proprietario del dispositivo).  Questo aggiornamento contiene le informazioni seguenti:

1. Se si crea un nuovo profilo e si seleziona il tipo di registrazione del dispositivo Profilo di lavoro e il profilo di Proprietario del dispositivo, non sarà possibile associare un profilo del certificato ai criteri di configurazione dell'app.
2. Se viene creato un nuovo profilo ed è selezionato il tipo Solo profilo di lavoro, è possibile usare i criteri di certificato del profilo di lavoro creati con la configurazione del dispositivo.
3. Se viene creato un nuovo profilo e si seleziona il tipo Solo proprietario del dispositivo, è possibile usare i criteri di certificato del proprietario del dispositivo creati con la configurazione del dispositivo. 

> [!IMPORTANT]
> Per impostazione predefinita, i criteri esistenti creati prima del rilascio di questa funzionalità (versione di aprile 2020 - 2004) che non hanno profili certificato associati useranno il tipo di registrazione del dispositivo Profilo di lavoro e profilo di Proprietario del dispositivo. Per impostazione predefinita, poi, i criteri esistenti creati prima del rilascio di questa funzionalità con profili certificato associati useranno il tipo Solo profilo di lavoro.

Verranno aggiunti anche i profili di configurazione di posta elettronica Gmail e Nine che funzioneranno per entrambi i tipi di registrazione Profilo di lavoro e Proprietario del dispositivo, incluso l'uso di profili certificato per entrambi i tipi di configurazione di posta elettronica.  Eventuali criteri per Gmail o Nine creati nell'ambito della configurazione del dispositivo per i profili di lavoro continueranno a essere applicati al dispositivo e non è necessario spostarli nei criteri di configurazione delle app.

Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) è possibile trovare i criteri di configurazione delle app selezionando **App** > **Criteri di configurazione dell'app**. Per altre informazioni sui criteri di configurazione delle app, vedere [Criteri di configurazione delle app per Microsoft Intune](../apps/app-configuration-policies-overview.md).

#### <a name="push-notification-when-device-ownership-type-is-changed---5575875---"></a>Notifica push quando cambia il tipo di proprietà del dispositivo<!-- 5575875 -->
È possibile configurare una notifica push da inviare agli utenti del portale aziendale sia Android che iOS quando il tipo di proprietà del dispositivo cambia da Personale ad Aziendale come servizio di cortesia per la privacy. Questa notifica push è disattivata per impostazione predefinita. L'impostazione è disponibile in Microsoft Endpoint Manager selezionando **Amministrazione tenant** > **Personalizzazione**. Per altre informazioni sull'impatto della proprietà dei dispositivi sugli utenti finali, vedere [Modificare la proprietà del dispositivo](../enrollment/corporate-identifiers-add.md#change-device-ownership).

#### <a name="group-targeting-support-for-customization-pane---4722837----"></a>Supporto dell'assegnazione di gruppi nel riquadro Personalizzazione<!-- 4722837  -->
È possibile assegnare le impostazioni a gruppi di utenti nel riquadro **Personalizzazione**. Per trovare queste impostazioni in Intune, passare all'[Interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), selezionare **Amministrazione del tenant** > **Personalizzazione**. Per altre informazioni sulla personalizzazione, vedere [Come personalizzare le app Portale aziendale Intune, il sito Web Portale aziendale e l'app Intune](../apps/company-portal-app.md).


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Configurazione del dispositivo

#### <a name="multiple-evaluate-each-connection-attempt-on-demand-vpn-rules-supported-on-ios-ipados-and-macos---6424615----"></a>Più regole VPN su richiesta "Valuta ogni tentativo di connessione" supportate in iOS, iPadOS e macOS<!-- 6424615  -->
L'esperienza utente di Intune consente più regole VPN su richiesta nello stesso profilo VPN con l'azione **Valuta ogni tentativo di connessione** (**Dispositivi** > **Profili di configurazione** > **Crea profilo** > **iOS/iPadOS** o **macOS** per piattaforma > **VPN** per profilo > **VPN automatico** > **Su richiesta**).

Viene rispettata solo la prima regola dell'elenco. Questo comportamento è stato corretto e Intune valuta tutte le regole dell'elenco. Ogni regola viene valutata nell'ordine in cui viene visualizzata nell'elenco di regole su richiesta.

> [!NOTE]
> Se si hanno profili VPN esistenti che usano queste regole VPN su richiesta, la correzione viene applicata alla successiva modifica del profilo VPN. Eseguire, ad esempio, una modifica secondaria, come la modifica del nome della connessione, e quindi salvare il profilo.
>
> Se per l'autenticazione si usano certificati SCEP, questa modifica causa la riemissione dei certificati per il profilo VPN.

Si applica a:
- iOS/iPadOS
- macOS

Per altre informazioni sui profili VPN, vedere [Creare profili VPN](../configuration/vpn-settings-configure.md).

#### <a name="additional-options-in-sso-and-sso-app-extension-profiles-on-iosipados-devices---6504155-----"></a>Opzioni aggiuntive nei profili SSO e di estensione dell'app per l'accesso SSO nei dispositivi iOS/iPadOS<!-- 6504155   -->

Nei dispositivi iOS/iPadOS è possibile:
- Nei profili SSO (**Dispositivi** > **Profili di configurazione** > **Crea profilo** > **iOS/iPadOS** per la piattaforma > **Funzionalità del dispositivo** per il profilo > **Single Sign-On**), impostare il nome dell'entità Kerberos sul nome dell'account di gestione degli account di sicurezza (SAM) nei profili SSO. 
- Nei profili di estensione dell'app per l'accesso SSO (**Dispositivi** > **Profili di configurazione** > **Crea profilo** > **iOS/iPadOS** per la piattaforma > **Funzionalità del dispositivo** per il profilo > **Estensione dell'app per l'accesso Single Sign-On**), configurare l'estensione Microsoft Azure AD iOS/iPadOS con meno clic usando un nuovo tipo di estensione dell'app per l'accesso Single Sign-On. È possibile abilitare l'estensione Azure AD per i dispositivi in modalità condivisa e inviare dati specifici dell'estensione a quest'ultima.

Si applica a:
- iOS/iPadOS 13.0+

Per altre informazioni sull'uso di Single Sign-On nei dispositivi iOS/iPadOS, vedere [Panoramica dell'estensione dell'app Single Sign-On](../configuration/device-features-configure.md#single-sign-on-app-extension) ed [Elenco delle impostazioni di Single Sign-On](../configuration/ios-device-features-settings.md#single-sign-on-app-extension).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Registrazione del dispositivo

#### <a name="delete-apple-automated-device-enrollment-token-when-default-profile-is-present--6393220---"></a>Eliminare il token di registrazione automatica dei dispositivi Apple quando è presente un profilo predefinito<!--6393220 -->
In precedenza non era possibile eliminare un profilo predefinito, quindi non era possibile eliminare il token di Registrazione automatica dei dispositivi associati a tale profilo. È ora possibile eliminare il token quando:
- al token non è assegnato alcun dispositivo
- è presente un profilo predefinito A tale scopo, eliminare il profilo predefinito e quindi eliminare il token associato.
Per altre informazioni, vedere [Eliminare un token di Registrazione automatica dei dispositivi da Intune](../enrollment/device-enrollment-program-enroll-ios.md#delete-an-ade-token-from-intune).

#### <a name="scaled-up-support-for-apple-automated-device-enrollment-and-apple-configurator-2-devices-profiles-and-tokens--3542402---"></a>Aumento del supporto per Registrazione automatica dei dispositivi Apple e per i dispositivi, i profili e i token di Apple Configurator 2<!--3542402 -->
Per venire incontro ai reparti e alle organizzazioni IT distribuiti, Intune supporta ora fino a 1000 profili di registrazione per token, 2000 token di Registrazione automatica dei dispositivi (precedentemente nota come Device Enrollment Program) per account di Intune e 75.000 dispositivi per token. Non esiste un limite specifico di dispositivi per profilo di registrazione, al di sotto del numero massimo di dispositivi per token.

Intune supporta ora fino a 1000 profili Apple Configurator 2.

Per altre informazioni, vedere [Volume supportato](../enrollment/device-enrollment-program-enroll-ios.md#supported-volume).

#### <a name="all-devices-page-column-entry-changes--6967616---"></a>Modifiche alle voci di una colonna della pagina Tutti i dispositivi<!--6967616 -->
Nella pagina **Tutti i dispositivi** le voci della colonna **Gestito da** sono state modificate:
- Viene ora visualizzata la voce *Intune* anziché *MDM*
- Viene ora visualizzata la voce *Con co-gestione* anziché *MDM/Agente di ConfigMgr*

I valori di esportazione rimangono invariati.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Gestione dei dispositivi

#### <a name="trusted-platform-manager-tpm-version-information-now-on-device-hardware-page--6224914-idmiss---"></a>Informazioni sulla versione di TPM (Trusted Platform Manager) ora nella pagina Hardware del dispositivo<!--6224914 idmiss -->
È ora possibile visualizzare il numero di versione di TPM nella pagina Hardware del dispositivo ([Interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Dispositivi** > scegliere un dispositivo > **Hardware** > cercare in **Chassis**).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Monitorare e risolvere i problemi

#### <a name="collect-logs-to-better-troubleshoot-scripts-assigned-to-macos-devices---6359853----"></a>Raccogliere i log per risolvere in modo più efficiente i problemi degli script assegnati ai dispositivi macOS<!-- 6359853  -->
È ora possibile raccogliere i log per rendere più efficiente la risoluzione dei problemi degli script assegnati ai dispositivi macOS. È possibile raccogliere log fino a 60 MB (compressi) o 25 file, a seconda di quale condizione si verifica per prima. Per altre informazioni, vedere [Risolvere i problemi dei criteri di script della shell macOS tramite la raccolta dei log](../apps/macos-shell-scripts.md#troubleshoot-macos-shell-script-policies-using-log-collection).
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="security"></a>Sicurezza

#### <a name="derived-credentials-to-provision-android-enterprise-fully-managed-devices-with-certificates--4839592------"></a>Credenziali derivate per il provisioning di certificati ai dispositivi Android Enterprise completamente gestiti<!--4839592    -->
Intune supporta ora l'uso di [credenziali derivate](../protect/derived-credentials.md) come metodo di autenticazione per i dispositivi Android. Le credenziali derivate sono un'implementazione dello standard NIST (National Institute of Standards and Technology) 800-157 per la distribuzione dei certificati nei dispositivi. Il supporto per Android espande il supporto per i dispositivi che eseguono iOS/iPadOS.

Le credenziali derivate si basano sull'uso della verifica dell'identità personale (PIV) o di una scheda (CAC, Common Access Card), ad esempio una smart card. Per ottenere le credenziali derivate per il dispositivo mobile, gli utenti partono dall'app Microsoft Intune e seguono un flusso di lavoro di registrazione specifico per il provider usato. È comune a tutti i provider la necessità di usare una smart card in un computer per l'autenticazione presso il provider delle credenziali derivate. Il provider rilascia quindi al dispositivo un certificato derivato dalla smart card dell'utente.

È possibile usare le credenziali derivate come metodo di autenticazione per i profili di configurazione dei dispositivi per VPN e Wi-Fi. È anche possibile usarle per l'autenticazione delle app e per la firma e la crittografia S/MIME per le applicazioni che le supportano.

Intune ora supporta con Android i provider di credenziali derivate seguenti:
- Entrust Datacard
- Intercede

Un terzo provider, DISA Purebred, sarà disponibile per Android in una versione futura.

#### <a name="microsoft-edge-security-baseline-is-now-generally-available--6586139---"></a>La baseline di sicurezza di Microsoft Edge è ora disponibile a livello generale<!--6586139 -->

È ora disponibile una nuova versione della [baseline di sicurezza di Microsoft Edge](../protect/security-baselines.md#available-security-baselines), che è stata rilasciata come disponibile a livello generale (GA). La baseline di Edge precedente era in anteprima.  La nuova versione della baseline è di aprile 2020 (versione di Edge 80 e successive). 

Con il rilascio di questa nuova baseline, non sarà più possibile creare profili basati sulle versioni della baseline precedenti, ma sarà possibile continuare a usare i profili creati con tali versioni. È anche possibile scegliere di [aggiornare i profili esistenti per l'uso della versione più recente della baseline](../protect/security-baselines.md#change-the-baseline-version-for-a-profile). 

<!-- ########################## -->
## <a name="week-of-april-6-2020"></a>Settimana del 6 aprile 2020

#### <a name="new-shell-script-settings-for-macos-devices---6884363---"></a>Nuove impostazioni degli script della shell per i dispositivi macOS<!-- 6884363 -->
Quando si configurano script della shell per i dispositivi macOS, ora è possibile configurare le nuove impostazioni seguenti: 
- Nascondi le notifiche degli script nei dispositivi
- Frequenza dello script
- Numero massimo di nuovi tentativi in caso di errore dello script

Per altre informazioni, vedere [Usare gli script della shell nei dispositivi macOS in Intune](../apps/macos-shell-scripts.md).

<!-- ########################## -->
## <a name="week-of-march-30-2020"></a>Settimana del 30 marzo 2020

### <a name="new-url-for-the-microsoft-endpoint-manager-admin-center---3704810---"></a>Nuovo URL per l'interfaccia di amministrazione di Microsoft Endpoint Manager<!-- 3704810 -->
In linea con l'annuncio di Microsoft Endpoint Manager in occasione di Ignite l'anno scorso, l'URL per l'interfaccia di amministrazione di Microsoft Endpoint Manager (in precedenza Gestione dispositivi Microsoft 365) è stato modificato in [https://endpoint.microsoft.com](https://endpoint.microsoft.com). L'URL del centro di amministrazione precedente ([https://devicemanagement.microsoft.com](https://devicemanagement.microsoft.com)) continuerà a funzionare, ma è consigliabile iniziare ad accedere all'interfaccia di amministrazione di Microsoft Endpoint Manager usando il nuovo URL.

Per altre informazioni, vedere [Semplificare le attività IT usando l'interfaccia di amministrazione di Microsoft Endpoint Manager](what-is-device-management.md#simplify-it-tasks-using-the-device-management-admin-center).  


### <a name="app-management"></a>Gestione delle app  

#### <a name="company-portal-for-ios-supports-landscape-mode--6048329----"></a>Il portale aziendale per iOS supporta la modalità orizzontale<!--6048329  -->   
Gli utenti possono registrare dispositivi, trovare app e ottenere supporto IT usando l'orientamento dello schermo preferito. L'app rileverà automaticamente l'orientamento adattandosi allo schermo in modalità verticale o orizzontale, a meno che gli utenti non blocchino lo schermo in modalità verticale.  

#### <a name="script-support-for-macos-devices-public-preview---4280361----"></a>Supporto degli script per i dispositivi macOS (anteprima pubblica)<!-- 4280361  -->
È possibile aggiungere e distribuire script nei dispositivi macOS. Questo supporto consente di configurare i dispositivi macOS oltre le normali possibilità usando le funzionalità MDM native nei dispositivi macOS. Per altre informazioni, vedere [Usare gli script della shell nei dispositivi macOS in Intune](../apps/macos-shell-scripts.md).

<!-- ########################## -->
## <a name="week-of-march-24-2020"></a>Settimana del 24 marzo 2020

### <a name="improved-user-interface-experience-when-creating-device-restrictions-profiles-on-android-and-android-enterprise-devices---5841361---"></a>Esperienza migliorata dell'interfaccia utente per la creazione dei profili di limitazioni dei dispositivi in dispositivi Android e Android Enterprise<!-- 5841361 -->
L'esperienza per la creazione di un profilo per i dispositivi Android e Android Enterprise nell'interfaccia di amministrazione di Endpoint Manager è stata aggiornata. Questa modifica ha effetto sui profili di configurazione dei dispositivi seguenti (**Dispositivi** > **Profili di configurazione** > **Crea profilo** > **Amministratore di dispositivi Android** o **Android Enterprise** per la piattaforma):

- Limitazioni dei dispositivi: Amministratore dispositivo Android
- Limitazioni dei dispositivi: Proprietario del dispositivo Android Enterprise
- Limitazioni dei dispositivi: Profilo di lavoro di Android Enterprise

Per altre informazioni sulle restrizioni dei dispositivi che è possibile configurare, vedere [Amministratore di dispositivi Android](../configuration/device-restrictions-android.md) e [Android Enterprise](../configuration/device-restrictions-android-for-work.md).

### <a name="improved-user-interface-experience-when-creating-configuration-profiles-on-iosipados-and-macos-devices---5569002-5568997---"></a>Esperienza migliorata dell'interfaccia utente per la creazione dei profili di configurazione nei dispositivi iOS/iPadOS e macOS<!-- 5569002 5568997 -->
L'esperienza per la creazione di un profilo per i dispositivi iOS o macOS nell'interfaccia di amministrazione di Endpoint Manager è stata aggiornata. Questa modifica ha effetto sui profili di configurazione dei dispositivi elencati di seguito (**Dispositivi** > **Profili di configurazione** > **Crea profilo** > **iOS/iPadOS** o **macOS** per la piattaforma):

- Personalizzata: iOS/iPadOS, macOS
- Funzionalità del dispositivo: iOS/iPadOS, macOS
- Limitazioni del dispositivo: iOS/iPadOS, macOS
- Endpoint Protection: macOS
- Estensioni: macOS
- File delle preferenze: macOS

### <a name="hide-from-user-configuration-setting-in-device-features-on-macos-devices---6524869---"></a>Impostazione Nascondi dalla configurazione utente nelle funzionalità del dispositivo per i dispositivi macOS<!-- 6524869 -->

Quando si crea un profilo di configurazione delle funzionalità del dispositivo nei dispositivi macOS, è disponibile una nuova impostazione **Nascondi dalla configurazione utente** (**Dispositivi** > **Profili di configurazione** > **Crea profilo** > **macOS** per la piattaforma > **Funzionalità del dispositivo** per il profilo >**Elementi di accesso**).

Questa funzionalità imposta il segno di spunta Nascondi di un'app nell'elenco delle app degli elementi di accesso **Utenti e gruppi** nei dispositivi macOS. I profili esistenti mostrano questa impostazione all'interno dell'elenco come non configurata. Per configurare questa impostazione, gli amministratori possono aggiornare i profili esistenti.

Con l'impostazione **Nascondi** la casella di controllo Nascondi viene selezionata per l'app e gli utenti non possono modificarla. Inoltre, l'app viene nascosta dagli utenti dopo l'accesso ai dispositivi.

> [!div class="mx-imgBorder"]
> ![Nascondere le app nei dispositivi macOS dopo che gli utenti hanno eseguito l'accesso al dispositivo in Microsoft Intune ed Endpoint Manager](./media/whats-new/macos-hide-checkmark-users-groups-login-items-apps-list.png)

Per altre informazioni sull'impostazione che è possibile configurare, vedere [Impostazioni delle funzionalità dei dispositivi macOS](../configuration/macos-device-features-settings.md).

Questa funzionalità si applica a:

- macOS

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

#### <a name="optimized-dedicated-device-enrollment----6114580----"></a>Ottimizzata la registrazione di dispositivi dedicati <!-- 6114580  -->
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
È possibile specificare nella configurazione se la registrazione dei dispositivi nel Portale aziendale sui dispositivi Android e iOS è disponibile con prompt, disponibile senza prompt o non disponibile per gli utenti. Per trovare queste impostazioni in Intune, passare all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) e selezionare **Amministrazione del tenant** > **Personalizzazione** > **Modifica** > **Registrazione del dispositivo**.  

Per il supporto per l'impostazione della registrazione dei dispositivi è necessario che gli utenti finali dispongano delle versioni del Portale aziendale seguenti:
-    Portale aziendale in iOS: versione 4.4 o successiva
-    Portale aziendale in Android: versione 5.0.4715.0 o successiva

Per altre informazioni sulla personalizzazione del Portale aziendale esistente, vedere [Come configurare l'app Portale aziendale di Microsoft Intune](../apps/company-portal-app.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Gestione dei dispositivi

#### <a name="new-android-report-on-android-devices-overview-page---5435435-----"></a>Nuovo report Android nella pagina di panoramica dei dispositivi Android<!-- 5435435   -->
È stato aggiunto un report alla console di amministrazione di Microsoft Endpoint Manager nella pagina di panoramica dei dispositivi Android che visualizza il numero di dispositivi Android registrati in ogni soluzione di gestione dei dispositivi. Questo grafico (corrispondente al grafico già presente nella console di Azure) mostra il numero di dispositivi registrati con profilo di lavoro, completamente gestiti, dedicati e con registrazione di tipo amministratore di dispositivi. Per visualizzare il report, scegliere **Dispositivi** > **Android** > **Panoramica**.

#### <a name="guide-users-from-android-device-administrator-management-to-work-profile-management--5857738-----"></a>Guidare gli utenti dalla gestione degli amministratori dei dispositivi Android alla gestione del profilo di lavoro<!--5857738   -->
È in corso il rilascio di una nuova impostazione di conformità per la piattaforma degli amministratori dei dispositivi Android. Questa impostazione consente di rendere un dispositivo non conforme se gestito con l'amministratore del dispositivo.

In questi dispositivi non conformi gli utenti visualizzeranno il messaggio **Passa alla configurazione della gestione dei nuovi dispositivi** nella pagina **Aggiorna impostazioni del dispositivo**. Toccando il pulsante **Risolvi**, verranno visualizzate indicazioni dettagliate su:

1. Annullamento della registrazione nella gestione degli amministratori dei dispositivi
2. Registrazione nella gestione del profilo di lavoro
3. Risoluzione dei problemi di conformità 
 
Google sta riducendo il supporto per l'amministratore di dispositivi nelle nuove versioni di Android con l'obiettivo di passare a una gestione dei dispositivi moderna, più ricca e sicura con Android Enterprise.  Intune può offrire supporto completo per i dispositivi Android gestiti dall'amministratore di dispositivi che eseguono Android 10 e versioni successive solo fino al secondo trimestre del 2020. I dispositivi gestiti dall'amministratore di dispositivi (tranne i dispositivi Samsung) che eseguono Android 10 o versione successiva in seguito non potranno più essere gestiti interamente. In particolare, i dispositivi interessati non riceveranno nuovi requisiti per le password.

Per altre informazioni su questa impostazione, vedere [Aggiornare i dispositivi Android da amministratore di dispositivi alla gestione del profilo di lavoro](../enrollment/android-move-device-admin-work-profile.md). 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Monitorare e risolvere i problemi

#### <a name="the-data-warehouse-now-provides-the-mac-address---6123680----"></a>Il data warehouse ora indica l'indirizzo MAC<!-- 6123680  -->
Il data warehouse di Intune specifica l'indirizzo MAC come nuova proprietà (`EthernetMacAddress`) nell'entità `device` per consentire agli amministratori di eseguire la correlazione tra l'utente e l'indirizzo MAC dell'host. Questa proprietà consente di raggiungere utenti specifici e risolvere i problemi relativi agli eventi imprevisti che si verificano nella rete. Gli amministratori possono usare questa proprietà anche nei [report di Power BI](../developer/reports-proc-get-a-link-powerbi.md) per compilare report più completi. Per altre informazioni, vedere l'entità [dispositivo](../developer/intune-data-warehouse-collections.md#devices) del data warehouse di Intune.

#### <a name="additional-data-warehouse-device-inventory-properties---6125732----"></a>Proprietà aggiuntive per l'inventario dei dispositivi tramite data warehouse<!-- 6125732  -->
Si può accedere alle proprietà aggiuntive per l'inventario dei dispositivi dal data warehouse di Intune. Le proprietà seguenti sono ora esposte attraverso la raccolta dei [dispositivi](../developer/reports-ref-devices.md#devices):
- `ethernetMacAddress`: identificatore di rete univoco del dispositivo.
- `model`: modello del dispositivo.
- `office365Version`: versione di Office 365 installata nel dispositivo.
- `windowsOsEdition`: versione del sistema operativo.

Le proprietà seguenti sono ora esposte attraverso la raccolta beta [devicePropertyHistory](../developer/reports-ref-devices.md#devicepropertyhistories):
- `physicalMemoryInBytes`: memoria fisica in byte.
- `totalStorageSpaceInBytes`: capacità di archiviazione totale in byte.

Per altre informazioni, vedere [API Data Warehouse di Microsoft Intune](../developer/reports-nav-intune-data-warehouse.md).

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

### <a name="app-management"></a>Gestione delle app  
####  <a name="improved-sign-in-experience-in-company-portal-for-android"></a>Esperienza di accesso aggiornata nel Portale aziendale per Android    
Il layout di diverse schermate di accesso nell'app Portale aziendale per Android è stato aggiornato per rendere l'esperienza più moderna, semplice e ordinata per gli utenti. Per informazioni sui miglioramenti, vedere [Novità dell'interfaccia utente dell'app](https://docs.microsoft.com/mem/intune/fundamentals/whats-new-app-ui).

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
L'esperienza utente per l'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Amministrazione del tenant** > **Ruoli** è stata migliorata per essere più semplice e intuitiva. La nuova esperienza fornisce le stesse impostazioni e gli stessi dettagli attualmente presenti, ma consentirà di visualizzare e definire i ruoli tramite un processo simile a una procedura guidata.

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

## <a name="whats-new-archive"></a>Archivio delle novità
Per i mesi precedenti, vedere [Novità di Microsoft Intune - Mesi precedenti](whats-new-archive.md).

## <a name="notices"></a>Notifiche

[!INCLUDE [Intune notices](../includes/intune-notices.md)]


