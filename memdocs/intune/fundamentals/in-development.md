---
title: In fase di sviluppo - Microsoft Intune
titleSuffix: ''
description: Funzionalità di Microsoft Intune in fase di sviluppo
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/01/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 90039e9bb75bcf7c266ac033408f87d37e27ef8d
ms.sourcegitcommit: 7a5196d4d9736c5cd52a23155c479523e52a097d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2020
ms.locfileid: "84436755"
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

### <a name="improvements-to-devices-page-of-iosipados-and-macos-company-portals---6055001----"></a>Miglioramenti alla pagina dispositivi dei portali aziendali iOS/iPadOS e macOS<!-- 6055001  -->
Sono stati apportati diversi miglioramenti all'esperienza utente della pagina **Dispositivi** dell'app Portale aziendale per iOS/iPadOS e Mac. È stata rinnovata la pagina **Dispositivi** per ottenere un aspetto più moderno e una migliore organizzazione delle informazioni sul dispositivo. Usando una colonna singola con intestazioni di sezione definite, gli utenti di iOS/iPad e macOS dell'organizzazione potranno controllare facilmente lo stato dei loro dispositivi per assicurarsi che siano protetti e mantengano l'accesso alle risorse dell'organizzazione. Sono stati inoltre aggiunti messaggi più chiari e ulteriori passaggi per la risoluzione dei problemi per gli utenti i cui dispositivi non sono conformi. Per altre informazioni sul Portale aziendale, vedere [Come personalizzare le app Portale aziendale Intune, il sito Web Portale aziendale e l'app Intune](../apps/company-portal-app.md).

### <a name="improvements-to-the-company-portal-for-macos-enrollment-experience---6444452----"></a>Miglioramenti apportati al Portale aziendale per l'esperienza di registrazione di macOS<!-- 6444452  -->
Il Portale aziendale per l'esperienza di registrazione di macOS prevede un processo di registrazione più semplice che si allinea maggiormente al Portale aziendale per l'esperienza di registrazione di iOS. Gli utenti dei dispositivi potranno visualizzare:  
- Un'interfaccia utente più accattivante.  
- Un elenco di controllo per la registrazione migliorato.  
- Istruzioni più chiare su come registrare i dispositivi.  
- Opzioni di risoluzione dei problemi migliorate.  

Per altre informazioni sul Portale aziendale, vedere [Come personalizzare le app Portale aziendale Intune, il sito Web Portale aziendale e l'app Intune](../apps/company-portal-app.md).

### <a name="use-autonomous-single-app-mode-settings-to-configure-the-ios-company-portal-to-be-a-sign-insign-out-app---7055619----"></a>Usare le impostazioni della Modalità applicazione singola autonoma per configurare il Portale aziendale iOS come app di accesso/disconnessione<!-- 7055619  -->
Sarà possibile configurare il Portale aziendale iOS per usare la Modalità applicazione singola autonoma (ASAM). È possibile usare le impostazioni di ASAM nella console di Microsoft Endpoint Manager per configurare il Portale aziendale iOS per entrare e uscire dalla modalità app singola quando si esegue la disconnessione e l'accesso. Quando il Portale aziendale è in Modalità applicazione singola autonoma gli utenti non sono in grado di usare altre app o il pulsante Home sul dispositivo fino a quando non eseguono l'accesso al Portale aziendale. Quando si esegue la disconnessione, il Portale aziendale torna alla modalità app singola. 

Per configurare il Portale aziendale in modo che sia in Modalità applicazione singola autonoma in Microsoft Endpoint Manager, selezionare **Dispositivi** > **Profili di configurazione** > **Crea profilo**. Selezionare **iOS/iPadOS** come piattaforma e selezionare **Restrizioni dei dispositivi** come profilo. Nella scheda **Impostazioni di configurazione**, selezionare **Modalità applicazione singola autonoma**. Impostare il **Nome dell'app** su `Company Portal` e impostare l'**ID bundle dell'app** su `com.app.CompanyPortal`. Per altre informazioni, vedere [Modalità applicazione singola autonoma](../configuration/device-restrictions-ios.md#autonomous-single-app-mode-asam) e [Modalità applicazione singola](https://support.apple.com/guide/mdm/single-app-mode-mdm80a981/1/web/1).

<!-- ***********************************************-->
## <a name="device-configuration"></a>Configurazione del dispositivo

### <a name="set-device-compliance-state-from-third-party-mdm-partners---6361689-----"></a>Impostare lo stato di conformità del dispositivo da partner MDM di terze parti<!-- 6361689   -->
Sarà presto possibile consentire l'impostazione dello stato di conformità dei dispositivi iOS o Android gestiti da partner di gestione di dispositivi mobili (MDM) di terze parti in Azure Active Directory (Azure AD).

Quando Intune è configurato per la conformità con i partner, i dati di conformità per i dispositivi gestiti dal partner MDM di terze parti vengono inviati a Intune per la valutazione della conformità. I risultati vengono quindi trasmessi ad Azure AD, dove vengono usati i dati di conformità per applicare i criteri di accesso condizionale per tali dispositivi.

Il supporto comprenderà presto i partner seguenti:
- VMware WorkspaceONE (noto precedentemente come AirWatch)

Per abilitare un partner per la conformità dei dispositivi, usare un nuovo nodo nell'interfaccia di amministrazione di Microsoft Endpoint Manager: **Amministrazione del tenant** > **Connettori e token** > **Gestione della conformità dei partner** dove occorre selezionare **Aggiungi un partner per la conformità**.

### <a name="add-a-link-to-your-company-portal-support-website-to-emails-for-noncompliance---7225498------"></a>Aggiungere un collegamento al sito Web di assistenza del portale aziendale per i messaggi di posta elettronica per la non conformità<!-- 7225498    -->
È stata aggiunta una nuova impostazione al modello di notifica tramite posta elettronica che aggiungerà il collegamento al sito Web del portale aziendale per le notifiche di posta elettronica inviate agli utenti di dispositivi non conformi. (**Sicurezza degli endpoint** > **Conformità del dispositivo** > **Notifiche** > **Crea la notifica**).  Gli utenti che ricevono un messaggio di posta elettronica a causa di un dispositivo non conforme possono usare il collegamento per aprire un sito Web per ottenere altre informazioni sul motivo per cui il dispositivo non è conforme.

### <a name="new-filevault-setting-for-macos-endpoint-protection-device-configuration-policy---5459801-----"></a>Nuova impostazione FileVault per i criteri di configurazione del dispositivo Endpoint Protection per macOS<!-- 5459801   -->
È in corso l'aggiunta di una nuova impostazione alla categoria FileVault nel modello di [Endpoint Protection per macOS](../protect/endpoint-protection-macos.md): Nascondi la chiave di ripristino (**Dispositivi** > **Profili di configurazione** > **Crea profilo**, selezionare **macOS** per *Piattaforma* e quindi **Endpoint Protection** per *Tipo di profilo*). Questa impostazione nasconde la chiave personale all'utente finale durante la crittografia FileVault 2. Un utente di un dispositivo può visualizzare la chiave di ripristino personale in qualsiasi momento dall'app Portale aziendale di iOS o dal sito Web del portale aziendale per il dispositivo macOS crittografato. Per visualizzare la chiave di ripristino personale, può passare ai dettagli del dispositivo e fare clic su *Ottieni la chiave di ripristino*.

Questa impostazione non sarà disponibile nei criteri creati in precedenza. Per configurare questa impostazione e poterla usare, sarà necessario ricreare i criteri di FileVault. 

### <a name="configure-content-caching-on-macos-devices---7106872---"></a>Configurare la memorizzazione del contenuto nella cache nei dispositivi macOS<!-- 7106872 -->
Nei dispositivi macOS è possibile creare un profilo di configurazione che configura la memorizzazione del contenuto nella cache (**Dispositivi** > **Profili di configurazione** > **Crea profilo** > **macOS** per la piattaforma > **Funzionalità del dispositivo** per il profilo). Usare queste impostazioni per eliminare la cache, consentire la memorizzazione nella cache condivisa, impostare un limite della cache sul disco e altro ancora.

Per altre informazioni sulla memorizzazione del contenuto nella cache, vedere [ContentCaching](https://developer.apple.com/documentation/devicemanagement/contentcaching) (viene aperto il sito Web di Apple).

Per visualizzare le impostazioni che è possibile configurare, passare alle [impostazioni delle funzionalità dei dispositivi macOS in Intune](../configuration/macos-device-features-settings.md).

Si applica a:
- macOS

### <a name="new-vpn-settings-for-windows-10-and-newer-devices---6602122----"></a>Nuove impostazioni della VPN per Windows 10 e dispositivi più recenti<!-- 6602122  -->
Quando si crea un profilo VPN usando il tipo di connessione IKEv2 sono disponibili nuove impostazioni che è possibile configurare (**Dispositivi** > **Profili di configurazione** > **Crea profilo** > **Windows 10 e versioni successive** per la piattaforma > **VPN** per il profilo > **VPN di base**):

- **Tunnel del dispositivo**: consente ai dispositivi di connettersi automaticamente alla VPN senza richiedere alcuna interazione con l'utente, compreso l'accesso dell'utente. Questa funzionalità richiede l'abilitazione di **Always On** e l'uso dei **Certificati della macchina** come metodo di autenticazione.
- Impostazioni di Cryptography Suite: configurare gli algoritmi usati per proteggere le associazioni IKE e di sicurezza figlio, che consentono di associare le impostazioni client e server.

Per visualizzare le impostazioni che è possibile configurare, passare a [Impostazioni del dispositivo Windows per aggiungere connessioni VPN con Intune](../configuration/vpn-settings-windows-10.md).

Si applica a:
- Windows 10 e versioni successive

### <a name="block-shared-ipad-temporary-sessions-on-shared-ipad-devices---6613794---"></a>Bloccare le sessioni temporanee di iPad condiviso sui dispositivi iPad condivisi<!-- 6613794 -->
In Intune è disponibile una nuova impostazione **Block Shared iPad temporary sessions** (Blocca le sessioni temporanee di Ipad condiviso) che blocca le sessioni temporanee nei dispositivi iPad condivisi (**Dispositivi** > **Profili di configurazione** > **Crea profilo** > **iOS/iPadOS** per piattaforma > **Restrizioni dei dispositivi** per tipo di profilo> **iPad condiviso**). Se abilitata, gli utenti finali non possono usare l'account Guest, ma devono accedere al dispositivo con l'ID Apple e la password gestiti. 

Per altre informazioni sulle impostazioni configurabili, vedere [Impostazioni dei dispositivi iOS e iPadOS per consentire o limitare l'uso delle funzionalità](../configuration/device-restrictions-ios.md).

Si applica a:
- Dispositivi iPad condivisi che eseguono iOS/iPadOS 13.4 e versioni successive

### <a name="use-microsoft-launcher-as-the-default-launcher-for-fully-managed-android-enterprise-devices---4927976----"></a>Usare Microsoft Launcher come utilità di avvio predefinita per i dispositivi Android Enterprise completamente gestiti<!-- 4927976  -->
Nei dispositivi per i proprietari di dispositivi Android Enterprise è possibile impostare Microsoft Launcher come utilità di avvio predefinito per i dispositivi completamente gestiti (**Dispositivi** > **Profili di configurazione** > **Crea profilo** > **Android Enterprise** per la piattaforma > **Proprietario dispositivo** > **Restrizioni dei dispositivi** per il profilo > **Esperienza del dispositivo**). Per configurare tutte le altre impostazioni dell'utilità di avvio Microsoft, usare i criteri di configurazione dell'app. 

Sono inoltre disponibili altri aggiornamenti dell'interfaccia utente, tra cui i **Dispositivi dedicati**, rinominati **Esperienza del dispositivo**.

Per visualizzare tutte le impostazioni configurabili, vedere [Impostazioni dei dispositivi Android Enterprise per consentire o limitare funzionalità tramite Intune](../configuration/device-restrictions-android-for-work.md). 

Si applica a:
- Proprietario del dispositivo Android Enterprise completamente gestito

### <a name="add-new-schema-settings-and-search-for-existing-schema-settings-using-oemconfig-on-android-enterprise---6394386----"></a>Aggiungere nuove impostazioni dello schema e cercare le impostazioni esistenti usando OEMConfig in Android Enterprise<!-- 6394386  -->
In Intune è possibile usare OEMConfig per gestire le impostazioni dei dispositivi Android Enterprise (**Dispositivi** > **Profili di configurazione** > **Crea profilo** > **Android Enterprise** per la piattaforma > **OEMConfig** per il profilo). Quando si usa **Progettazione configurazione**, vengono visualizzate le proprietà nello schema dell'app. A questo punto, nella finestra di **Progettazione configurazione** è possibile:
- aggiungere nuove impostazioni allo schema dell'app;
- cercare le impostazioni nuove ed esistenti nello schema dell'app.

Per altre informazioni sui profili OEMConfig in Intune, vedere [Usare e gestire i dispositivi Android Enterprise con OEMConfig in Microsoft Intune](../configuration/android-oem-configuration-overview.md).

Si applica a:
- Android Enterprise

<!-- ***********************************************-->
## <a name="device-enrollment"></a>Registrazione del dispositivo

### <a name="automated-device-enrollment-sync-errors---6988214---"></a>Errori di sincronizzazione nella registrazione automatica dei dispositivi<!-- 6988214 -->
Verranno restituiti nuovi errori per i dispositivi iOS/iPadOS e macOS, tra cui:
- caratteri non validi nel numero di telefono o se il campo è vuoto; 
- nome di configurazione non valido o vuoto per il profilo; 
- valore del cursore non valido/scaduto o cursore non trovato;
- token rifiutato o scaduto; 
- campo relativo al reparto vuoto o troppo lungo; 
- non è stato trovato il profilo da Apple ed è necessario crearne uno nuovo; 
- verrà aggiunto un conteggio dei dispositivi Apple Business Manager rimossi alla pagina di panoramica in cui viene visualizzato lo stato dei dispositivi.

### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344---"></a>I dispositivi BYOD (Bring Your Own Device) possono usare la VPN per la distribuzione<!--5015344 -->
Il nuovo profilo di Autopilot **Ignora il controllo della connettività al dominio** consente di distribuire dispositivi aggiunti ad Azure AD ibrido senza accedere alla rete aziendale usando il proprio client VPN Win32 di terze parti. Per visualizzare il nuovo interruttore, passare all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Dispositivi**  > **Windows** > **Registrazione Windows** > **Profili di distribuzione** > **Crea profilo** > **Configurazione guidata**.

### <a name="shared-ipads-for-business--6367326---"></a>IPad condivisi per le aziende<!--6367326 -->
Sarà possibile usare Intune e Apple Business Manager per configurare in modo semplice e sicuro l'iPad condiviso, in modo che più dipendenti possano condividere i dispositivi. [iPad condiviso](https://developer.apple.com/education/shared-ipad/) di Apple offre un'esperienza personalizzata per più utenti, pur proteggendo i dati dei singoli utenti. Tramite un ID Apple gestito gli utenti possono accedere alle loro app, ai dati e alle impostazioni personali dopo aver eseguito l'accesso a qualsiasi iPad condiviso nell'organizzazione. iPad condiviso funziona con le identità federate.

Per visualizzare questa funzionalità passare all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Dispositivi** > **iOS** > **Registrazione di iOS** > **Token del programma di registrazione** > scegliere un token > **Profili** > **Crea profilo** > **iOS**. Nella pagina **Impostazioni di gestione** selezionare **Registra senza affinità utente**. Verrà visualizzata l'opzione **iPad condiviso**.

**Si applica a:** macOS 13.4 e versioni successive. In questa versione è stato aggiunto il supporto per le sessioni temporanee con iPad condiviso, in modo che gli utenti possano accedere a un dispositivo senza un ID Apple gestito. Al momento della disconnessione, il dispositivo cancella tutti i dati dell'utente e torna a essere immediatamente pronto per l'uso, eliminando la necessità di una cancellazione del dispositivo stesso. 

<!-- ***********************************************-->
## <a name="device-management"></a>Gestione dei dispositivi

### <a name="change-primary-user-on-co-managed-devices--7319183---"></a>Modificare l'utente primario nei dispositivi con co-gestione<!--7319183 -->
Sarà possibile modificare l'utente primario di un dispositivo per i dispositivi Windows co-gestiti. Per altre informazioni su come trovarlo e modificarlo, vedere [Trovare l'utente primario di un dispositivo Intune](../remote-actions/find-primary-user.md).

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>Supporto degli script di PowerShell per dispositivi BYOD<!-- 1862833  -->
Gli script di PowerShell supporteranno i dispositivi registrati con Azure AD in Intune. Per altre informazioni su PowerShell, vedere [Usare gli script di PowerShell nei dispositivi Windows 10 in Intune](../apps/intune-management-extension.md). Questa funzionalità non supporta i dispositivi che eseguono Windows 10 Home Edition.

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics includerà il log dei dettagli del dispositivo<!--6014987  -->
I log dei dettagli dei dispositivi di Intune saranno disponibili in **Report** > **Log Analytics**. È possibile correlare i dettagli dei dispositivi per creare query personalizzate e cartelle di lavoro di Azure.

### <a name="setting-the-intune-primary-user-also-sets-the-azure-ad-owner-property--7319227---"></a>L'impostazione dell'utente primario di Intune imposta anche la proprietà Owner di Azure AD<!--7319227 -->
Questa funzionalità, presto disponibile, imposta automaticamente la proprietà Owner nei dispositivi appena registrati Azure AD ibrido aggiunti nello stesso momento in cui è impostato l'utente primario di Intune. Per altre informazioni sull'utente primario, vedere [Trovare l'utente primario di un dispositivo Intune](../remote-actions/find-primary-user.md).

Si tratta di una modifica al processo di registrazione che si applica solo ai dispositivi appena registrati. Per i dispositivi aggiunti ad Azure AD ibrido esistenti, è necessario aggiornare manualmente la proprietà Owner di Azure AD. A tale scopo è possibile usare la [funzionalità Modifica l'utente primario](../remote-actions/find-primary-user.md#change-a-devices-primary-user) o [uno script](https://github.com/microsoftgraph/powershell-intune-samples/tree/master/ManagedDevices).

Quando i dispositivi Windows 10 diventano dispositivi ibridi aggiunti ad Azure Active Directory, il primo utente del dispositivo diventa l'utente primario in Endpoint Manager.  Attualmente, l'utente non è impostato sull'oggetto dispositivo Azure AD corrispondente. Questo causa un'incoerenza quando si confronta la proprietà *Owner* da un portale di Azure AD con la proprietà *utente primario* nell'interfaccia di amministrazione di Microsoft Endpoint Manager. La proprietà Owner di Azure AD viene usata per proteggere l'accesso alle chiavi di ripristino di BitLocker. La proprietà non viene popolata nei dispositivi aggiunti ad Azure AD ibrido. Questa limitazione impedisce la configurazione self-service del ripristino di BitLocker da Azure AD. La funzionalità presto disponibile risolve tale limitazione.

### <a name="tenant-attach-device-timeline-in-the-admin-center--7220536-cm7141381---"></a>Collegamento di tenant: sequenza temporale dispositivo nell'interfaccia di amministrazione<!--7220536, CM7141381 -->
Quando Configuration Manager sincronizza un dispositivo con Microsoft Endpoint Manager tramite il collegamento al tenant, è possibile visualizzare una sequenza temporale degli eventi. Questa sequenza temporale mostra le attività precedenti eseguite sul dispositivo che possono risultare utili per la risoluzione dei problemi. Per altre informazioni, vedere [Configuration Manager technical preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_timeline).  

### <a name="tenant-attach-install-an-application-from-the-admin-center---7220536-cm6024389---"></a>Collegamento di tenant: installare un'applicazione dall'interfaccia di amministrazione<!-- 7220536, CM6024389 -->
Sarà possibile avviare l'installazione di un'applicazione in tempo reale per un dispositivo collegato al tenant dall'interfaccia di amministrazione di Microsoft Endpoint Management. Per altre informazioni, vedere [Configuration Manager technical preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_apps).

### <a name="tenant-attach-cmpivot-from-the-admin-center--7220536-cm6024392---"></a>Collegamento di tenant: CMPivot dall'interfaccia di amministrazione<!--7220536, CM6024392 -->
Sarà possibile sfruttare la potenza di [CMPivot](../../configmgr/tenant-attach/cmpivot-overview-attached.md) nell'interfaccia di amministrazione di Microsoft Endpoint Manager. Altri utenti tipo, ad esempio il personale del supporto tecnico, possono avviare query in tempo reale dal cloud su un singolo dispositivo gestito da ConfigMgr e restituire i risultati all'interfaccia di amministrazione. In questo modo è possibile usufruire di tutti i vantaggi tradizionali di CMPivot, che consente agli amministratori IT e ad altri utenti designati di valutare rapidamente lo stato dei dispositivi nel proprio ambiente e di intervenire di conseguenza. Per altre informazioni, vedere [Configuration Manager technical preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_cmpivot). 

### <a name="tenant-attach-run-scripts-from-the-admin-center--7220536-cm6234688---"></a>Collegamento di tenant: eseguire script dall'interfaccia di amministrazione<!--7220536, CM6234688 -->
Sarà possibile sfruttare la potenza della funzionalità locale di Configuration Manager per [l'esecuzione di script](../../configmgr/apps/deploy-use/create-deploy-scripts.md) nell'interfaccia di amministrazione di Microsoft Endpoint Manager. Altri utenti tipo, ad esempio il personale del supporto tecnico, possono eseguire script di PowerShell dal cloud su un singolo dispositivo gestito di Configuration Manager. In questo modo è possibile usufruire di tutti i vantaggi tradizionali degli script di PowerShell che sono già stati definiti e approvati dall'amministratore di Configuration Manager nel nuovo ambiente. Per altre informazioni, vedere [Configuration Manager technical preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_scripts). 

### <a name="new-merge-logic-for-windows-10-devices--179048--"></a>Nuova logica di merge per dispositivi Windows 10<!--179048-->
Attualmente, se un cliente ricrea un'immagine di un dispositivo e lo registra nuovamente, nella console di amministrazione di Microsoft Endpoint Manager verranno visualizzati più record per il dispositivo. È in fase di sviluppo una nuova logica di unione per unire tali record duplicati per i dispositivi Windows 10.

### <a name="remote-lock-pin-availability-for-macos-devices--7281557--"></a>Disponibilità del PIN di blocco remoto per i dispositivi macOS<!--7281557-->
La disponibilità dei pin di blocco remoto per i dispositivi macOS sarà aumentata da 7 a 30 giorni.

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## <a name="monitor-and-troubleshoot"></a>Monitorare e risolvere i problemi

### <a name="power-bi-compliance-report-template-v20---636958----"></a>Modello di report di conformità Power BI V2.0<!-- 636958  -->
Gli amministratori potranno aggiornare il modello di report di conformità di Power BI da V1.0 a V2.0. V2.0 includerà una struttura migliorata e aggiornamenti ai calcoli e ai dati esposti come parte del modello. Per informazioni correlate, vedere [Connettersi al data warehouse con Power BI](../developer/reports-proc-get-a-link-powerbi.md).

<!-- ***********************************************-->
<!--
## Role-based access control
-->

<!-- ***********************************************-->
<!--## Security-->


<!-- ***********************************************-->
## <a name="notices"></a>Notifiche

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Vedere anche

Per informazioni dettagliate sugli ultimi sviluppi, vedere [Novità di Microsoft Intune](whats-new.md).
