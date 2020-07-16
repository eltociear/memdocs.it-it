---
title: Gestire Edge per iOS e Android con Intune
titleSuffix: ''
description: Usare i criteri di protezione e di configurazione delle app di Intune con Microsoft Edge per iOS e Android per garantire che l'accesso ai siti Web aziendali venga sempre eseguito con misure di sicurezza applicate.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 3fb2f050-ec94-42ab-be05-c3d4101148bb
ms.reviewer: ilwu
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4d32c496fc094879943fc15102bbb5061d830092
ms.sourcegitcommit: c7afcc3a2232573091c8f36d295a803595708b6c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84973061"
---
# <a name="manage-web-access-by-using-edge-for-ios-and-android-with-microsoft-intune"></a>Gestire l'accesso Web usando Microsoft Edge per iOS e Android con Microsoft Intune

Edge per iOS e Android è progettato per consentire agli utenti di esplorare il Web e supporta multi-identità. Gli utenti possono aggiungere sia un account aziendale che un account personale per l'esplorazione. Le due identità sono completamente separate, in modo analogo a quanto offerto da altre app per dispositivi mobili Microsoft.

Edge per iOS è supportato in iOS 12.0 e versioni successive. Edge per Android è supportato in Android 5 e versioni successive.

> [!NOTE]
> Edge per iOS e Android non usa le impostazioni che gli utenti definiscono per il browser nativo nei propri dispositivi, perché Edge per iOS e Android non può accedere a tali impostazioni.

Le funzionalità di protezione più complete e più ampie per i dati di Office 365 sono disponibili con l'abbonamento alla suite Enterprise Mobility + Security, che include funzionalità di Microsoft Intune e Azure Active Directory Premium, come l'accesso condizionale. Come minimo, è consigliabile implementare criteri di accesso condizionale che consentono di connettersi a Edge per iOS e Android solo dai dispositivi mobili e criteri di protezione delle app di Intune che garantiscono la protezione dell'esperienza di navigazione.

> [!NOTE]
> Le clip Web (app Web aggiunte) nei dispositivi iOS verranno aperte in Edge per iOS e Android anziché in Intune Managed Browser quando devono essere aperte in un browser protetto. Le clip Web iOS precedenti devono essere ridestinate per assicurarsi che si aprano in Edge per iOS e Android anziché in Managed Browser.

## <a name="apply-conditional-access"></a>Applicare l'accesso condizionale
Le organizzazioni possono usare i criteri di accesso condizionale di Azure AD per assicurarsi che gli utenti possano accedere solo ai contenuti aziendali o dell'istituto di istruzione usando Edge per iOS e Android. A tale scopo, è necessario disporre di criteri di accesso condizionale destinati a tutti i potenziali utenti. Per informazioni dettagliate sulla creazione di questi criteri, vedere [Richiedere i criteri di protezione delle app per l'accesso alle app cloud con accesso condizionale](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access).

1. Seguire [Scenario 2: le app del browser richiedono app approvate con i criteri di protezione delle app](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access#scenario-2-browser-apps-require-approved-apps-with-app-protection-policies), che consente l'uso di Edge per iOS e Android, ma impedisce ad altri Web browser di connettersi agli endpoint Office 365.

   >[!NOTE]
   > Questi criteri garantiscono che gli utenti di dispositivi mobili possano accedere a tutti gli endpoint di Office 365 da Edge per iOS e Android. Questi criteri impediscono inoltre agli utenti di usare InPrivate per accedere agli endpoint di Office 365.

Con l'accesso condizionale, è anche possibile fare riferimento a siti locali esposti a utenti esterni tramite il [proxy di applicazione AD Azure](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started).

## <a name="create-intune-app-protection-policies"></a>Creare criteri di protezione delle app di Intune

I criteri di protezione delle app definiscono quali app sono consentite e le azioni che queste possono eseguire con i dati dell'organizzazione. Le scelte disponibili sull'APP consentono alle organizzazioni di adattare la protezione alle loro esigenze specifiche. Per alcuni utenti potrebbe non essere semplice individuare le impostazioni dei criteri necessarie per implementare uno scenario completo. Per aiutare le organizzazioni a dare la priorità alla protezione avanzata degli endpoint di client mobili, Microsoft ha introdotto la tassonomia per il framework di protezione dei dati dell'APP per la gestione di dispositivi mobili iOS e Android.

Il framework di protezione dei dati dell'APP è organizzato in tre livelli di configurazione distinti, ognuno dei quali si basa sul livello precedente:

- **Protezione di base dei dati aziendali** (livello 1) garantisce che le app siano protette con un PIN e crittografate ed esegue operazioni di cancellazione selettiva. Per i dispositivi Android questo livello convalida l'attestazione dei dispositivi Android. Si tratta di una configurazione a livello di voce che offre un controllo simile di protezione dei dati nei criteri della cassetta postale di Exchange Online e introduce l'IT e la popolazione di utente nell'APP.
- **Protezione avanzata dei dati aziendali** (livello 2) introduce i meccanismi di protezione della perdita dei dati aziendali dell'APP e i requisiti minimi del sistema operativo. Questa configurazione è applicabile alla maggior parte degli utenti di dispositivi mobili che accedono ai dati aziendali o dell'istituto di istruzione.
- **Protezione elevata dei dati aziendali** (livello 3) introduce meccanismi avanzati per la protezione dei dati, configurazione del PIN avanzata e Mobile Threat Defense dell'APP. Questa configurazione è utile per gli utenti che accedono a dati ad alto rischio.

Per visualizzare le raccomandazioni specifiche per ogni livello di configurazione e le app minime che devono essere protette, consultare il [Framework di protezione dei dati con criteri di protezione delle app](app-protection-framework.md).

Indipendentemente dal fatto che il dispositivo sia registrato in una soluzione di gestione unificata degli endpoint (UEM), è necessario creare un criterio di protezione delle app di Intune per le app iOS e Android, seguendo la procedura descritta in [Come creare e assegnare criteri di protezione delle app](app-protection-policies.md). Questi criteri, come minimo, devono soddisfare le condizioni seguenti:

1. Sono incluse tutte le app Microsoft 365 per dispositivi mobili, ad esempio Microsoft Edge, Outlook, OneDrive, Office o Teams, in modo da garantire che gli utenti possano accedere e modificare i dati aziendali o dell'istituto di istruzione in qualsiasi app Microsoft in modo sicuro.

2. Sono assegnati a tutti gli utenti. Ciò garantisce che tutti gli utenti siano protetti, indipendentemente dal fatto che usino Edge per iOS o Android.

3. Determinare il livello di framework che soddisfa i requisiti. La maggior parte delle organizzazioni deve implementare le impostazioni definite in **Protezione avanzata dei dati aziendali** (livello 2), in quanto consente di controllare i requisiti di protezione e accesso ai dati.

Per altre informazioni sulle impostazione disponibili, vedere gli articoli [Impostazioni dei criteri di protezione delle app di Android](app-protection-policy-settings-android.md) e [Impostazioni dei criteri di protezione delle app per iOS](app-protection-policy-settings-ios.md).

> [!IMPORTANT]
> Per applicare i criteri di protezione delle app di Intune alle app nei dispositivi Android che non sono registrati in Intune, l'utente deve anche installare il Portale aziendale Intune. Per altre informazioni, consultare l'articolo [Aspettative relative alla gestione dell'app per Android con criteri di protezione delle app](../fundamentals/end-user-mam-apps-android.md).

## <a name="single-sign-on-to-azure-ad-connected-web-apps-in-policy-protected-browsers"></a>Accesso Single Sign-On alle app Web connesse ad Azure AD in browser protetti da criteri

Edge per iOS e Android può usare l'accesso Single Sign-On (SSO) per tutte le app Web (SaaS e locali) connesse ad Azure AD. L'accesso SSO consente agli utenti di accedere alle app Web connesse ad Azure AD tramite Edge per iOS e Android senza dover immettere nuovamente le proprie credenziali.

Per usare l'accesso SSO, è necessario che il dispositivo sia registrato tramite l'app Microsoft Authenticator per i dispositivi iOS oppure nel Portale aziendale Intune in Android. Quando gli utenti hanno a disposizione una di queste configurazioni, viene loro richiesto di registrare il dispositivo quando accedono a un'app Web connessa ad Azure AD in un browser protetto da criteri (ciò vale solo se il dispositivo non è ancora registrato). Dopo la registrazione del dispositivo con l'account utente gestito da Intune, per l'account viene abilitato l'accesso SSO per le app Web connesse ad Azure AD.

> [!NOTE]
> La registrazione del dispositivo è una semplice procedura di accesso al servizio Azure AD. Non richiede la registrazione del dispositivo completa e non implica la concessione di privilegi aggiuntivi al personale IT per il dispositivo.

## <a name="utilize-app-configuration-to-manage-the-browsing-experience"></a>Usare la configurazione delle app per gestire l'esperienza di navigazione

Edge per iOS e Android supporta le impostazioni dell'app che consentono agli amministratori della gestione unificata degli endpoint, ad esempio Microsoft Endpoint Manager, di personalizzare il comportamento dell'app.

La configurazione dell'app può essere eseguita tramite il canale di gestione di dispositivi mobili (MDM) del sistema operativo sui dispositivi registrati (canale [Configurazione delle app gestite](https://developer.apple.com/library/content/samplecode/sc2279/Introduction/Intro.html) per iOS o [Android nel canale Enterprise](https://developer.android.com/work/managed-configurations) per Android) o tramite il canale Criteri di protezione delle app (APP) di Intune. Edge per iOS e Android supporta gli scenari di configurazione seguenti:

- Ammettere solo account aziendali o di un istituto di istruzione
- Impostazioni generali di configurazione delle app
- Impostazioni di protezione dati

> [!IMPORTANT]
> Per gli scenari di configurazione che richiedono la registrazione del dispositivo in Android, i dispositivi devono essere registrati in Android Enterprise e Edge per Android deve essere distribuito tramite la versione gestita di Google Play Store. Per altre informazioni, vedere gli articoli [Configurare la registrazione dei dispositivi con profilo di lavoro Android Enterprise](../enrollment/android-work-profile-enroll.md) e [Criteri di configurazione delle app per Microsoft Intune](app-configuration-policies-use-android.md).

Ogni scenario di configurazione evidenzia i propri requisiti specifici. Ad esempio, se lo scenario di configurazione richiede la registrazione del dispositivo e quindi funziona con qualsiasi provider UEM o richiede criteri di Protezione app di Intune.

> [!NOTE]
> Con Microsoft Endpoint Manager, la configurazione dell'app eseguita tramite il canale MDM del sistema operativo è indicata come Criteri di configurazione delle app (ACP) per **dispositivi gestiti**; la configurazione dell'app eseguita tramite il canale Criteri di protezione delle app è denominata Criteri di configurazione delle app per**app gestite**.

## <a name="only-allow-work-or-school-accounts"></a>Ammettere solo account aziendali o di un istituto di istruzione

Il rispetto dei criteri di conformità e sicurezza dei dati dei clienti principali e altamente regolamentati è un elemento fondamentale del valore di Microsoft 365. Alcune società hanno la necessità di acquisire tutte le informazioni sulle comunicazioni all'interno dell'ambiente aziendale, nonché di assicurarsi che i dispositivi vengano usati solo per le comunicazioni aziendali. Per supportare questi requisiti, è possibile configurare Edge per iOS e Android nei dispositivi registrati in modo da consentire il provisioning di un singolo account aziendale sull'app.

Per altre informazioni sulla configurazione delle impostazioni della modalità degli account dell'organizzazione consentiti, vedere:

- [Impostazione Android](app-configuration-policies-use-android.md#allow-only-configured-organization-accounts-in-multi-identity-apps)
- [Impostazione iOS](app-configuration-policies-use-ios.md#allow-only-configured-organization-accounts-in-multi-identity-apps)

Questo scenario di configurazione funziona solo con i dispositivi registrati. Tuttavia, sono supportati tutti i provider UEM. Se non si usa Microsoft Endpoint Manager, è necessario consultare la documentazione di UEM per informazioni su come implementare queste chiavi di configurazione.

## <a name="general-app-configuration-scenarios"></a>Scenari generali di configurazione delle app

Edge per iOS e Android offre agli amministratori la possibilità di personalizzare la configurazione predefinita per diverse impostazioni in-app. Questa funzionalità è attualmente disponibile solo quando Edge per iOS e Android dispone di un Criterio di protezione app di Intune applicato all'account aziendale o dell'Istituto di istruzione che ha eseguito l'accesso all'app.

> [!IMPORTANT]
> Edge per Android non supporta le impostazioni di Chromium disponibili nella versione gestita di Google Play.

Edge supporta le impostazioni seguenti per la configurazione:

- Esperienze d'uso della Pagina Nuova scheda
- Esperienze d'uso dei Segnalibri
- Esperienze di Comportamento app
- Esperienze in modalità tutto schermo

Queste impostazioni possono essere implementate nell'app indipendentemente dallo stato di registrazione del dispositivo.

### <a name="new-tab-page-experiences"></a>Esperienze d'uso della Pagina Nuova scheda

Edge per iOS e Android offre alle organizzazioni diverse opzioni per adeguare l'esperienza Pagina nuova scheda.

#### <a name="organization-logo-and-brand-color"></a>Logo e colore del marchio dell'organizzazione

Queste impostazioni consentono di personalizzare la pagina Nuova scheda su Edge per iOS e Android per visualizzare il logo e il colore del marchio dell'organizzazione come sfondo della pagina.

Per caricare il logo e il colore dell'organizzazione, seguire prima di tutto questa procedura:
1. Nel portale di [Microsoft Endpoint Manager](https://endpoint.microsoft.com) andare su **Amministrazione del tenant** -> **Personalizzazione** -> **Personalizzazione dell'identità aziendale**.
2. Per impostare il logo del marchio, accanto a **Mostra in intestazione**, scegliere "solo il logo della società". Sono consigliati logo con sfondo trasparente.
3. Per impostare il colore di sfondo del marchio, scegliere **Colore del tema**. Edge per iOS e Android applica una sfumatura più chiara del colore nella pagina Nuova scheda, che garantisce una maggiore leggibilità della pagina.

Usare quindi le coppie chiave/valore seguenti per eseguire il pull degli elementi aziendali personalizzati in Edge per iOS e Android:

|    Chiave    |    Valore    |
|--------------------------------------------------------------------|------------|
|    com.microsoft.intune.mam.managedbrowser.NewTabPage.BrandLogo    |    **true** mostra il logo dell'organizzazione<br>**false** (impostazione predefinita) non esporrà un logo    |
|    com.microsoft.intune.mam.managedbrowser.NewTabPage.BrandColor    |    **true** mostra il colore del marchio dell'organizzazione<br>**false** (impostazione predefinita) non esporrà un colore    |

#### <a name="homepage-shortcut"></a>Collegamento alla home page

Questa impostazione consente di configurare un collegamento alla home page per Edge per iOS e Android. Il collegamento alla home page configurato verrà visualizzato come prima icona sotto la barra di ricerca quando l'utente apre una nuova scheda in Edge per iOS e Android. L'utente non può modificare o eliminare questo collegamento nel contesto gestito. Nel collegamento alla home page viene visualizzato il nome dell'organizzazione per poterlo distinguere. 

|    Chiave    |    Valore    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.homepage   |    Specificare un URL valido. Come misura di sicurezza, gli URL non corretti vengono bloccati.<br>ad esempio `https://www.bing.com`     |

#### <a name="multiple-top-site-shortcuts"></a>Collegamenti a più siti principali

Analogamente alla configurazione di un collegamento alla home page, è possibile configurare più collegamenti ai siti principali nelle nuove schede in Edge per iOS e Android. L'utente non può modificare o eliminare questi collegamenti in un contesto gestito. Nota: è possibile configurare un totale di 8 collegamenti, incluso un collegamento alla home page. Se si è configurato un collegamento alla home page, questo sostituirà il primo sito principale configurato. 

|    Chiave    |    Valore    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.managedTopSites   |    Specificare il set di valori e URL. Ogni collegamento a un sito principale è costituito da un titolo e un URL. Separare titolo e URL con il carattere `|`.<br>ad esempio `GitHub|https://github.com/||LinkedIn|https://www.linkedin.com`    |

#### <a name="industry-news"></a>Notizie del settore

È possibile configurare la nuova esperienza d'uso della Pagina Nuova scheda in Microsoft Edge per iOS e Android per visualizzare le notizie sul settore rilevanti per l'organizzazione. Quando si abilita questa funzionalità, Microsoft Edge per iOS e Android usa il nome di dominio dell'organizzazione per aggregare notizie dal Web in merito all'organizzazione, al settore dell'organizzazione e ai concorrenti, in modo che gli utenti possano trovare le notizie esterne pertinenti dalle pagine Nuova scheda centralizzate in Microsoft Edge per iOS e Android. La funzione Notizie del settore è disattivata per impostazione predefinita. 

|    Chiave    |    Valore    |
|------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.NewTabPage.IndustryNews    |    **true** mostra le Notizie del settore nella pagina della nuova scheda<br>**false** (impostazione predefinita) nasconde le notizie del settore nella pagina della nuova scheda    |

### <a name="bookmark-experiences"></a>Esperienze d'uso dei Segnalibri

Microsoft Edge per iOS e Android offre alle organizzazioni diverse opzioni per gestire i segnalibri.

#### <a name="managed-bookmarks"></a>Segnalibri gestiti

Per semplificare l'accesso, è possibile configurare segnalibri da mettere a disposizione degli utenti quando usano Microsoft Edge per iOS e Android.

- I segnalibri vengono visualizzati solo nell'account aziendale o dell'Istituto di istruzione e non sono esposti agli account personali.
- I segnalibri non possono essere eliminati o modificati dagli utenti.
- I segnalibri vengono visualizzati nella parte superiore dell'elenco. Eventuali segnalibri creati dagli utenti vengono visualizzati sotto questi segnalibri.
- Se è stato abilitato il reindirizzamento di Application Proxy, è possibile aggiungere le app Web di Application Proxy usando il relativo URL interno o esterno.
- Quando si aggiungono gli URL all'elenco, farli precedere dal prefisso **http://** o **https://** .
- I segnalibri vengono creati in una cartella con il nome dell'organizzazione definito in Azure Active Directory.

|    Chiave    |    Valore    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.bookmarks    |    Il valore per questa configurazione è un elenco di segnalibri. Ogni segnalibro è costituito da titolo e URL. Separare titolo e URL con il carattere `|`.<br> ad esempio `Microsoft Bing|https://www.bing.com`<p>Per configurare più segnalibri, separare ogni coppia con il doppio carattere `||`.<br>Ad esempio:<br>`Microsoft Bing|https://www.bing.com||Contoso|https://www.contoso.com`    |

#### <a name="my-apps-bookmark"></a>Segnalibro in App personali

Per impostazione predefinita, il segnalibro è configurato in App personali all'interno della cartella dell'organizzazione in Microsoft Edge per iOS e Android.

|    Chiave    |    Valore    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.MyApps    |    **true** (impostazione predefinita) mostra App personali nei segnalibri di Microsoft Edge per iOS e Android<br>**false** nasconde le App personali in Microsoft Edge per iOS e Android    |

### <a name="app-behavior-experiences"></a>Esperienze di Comportamento app

Microsoft Edge per iOS e Android offre alle organizzazioni diverse opzioni per gestire il comportamento dell'app.

#### <a name="default-protocol-handler"></a>Gestore di protocollo predefinito

Per impostazione predefinita, Microsoft Edge per iOS e Android usa il gestore di protocollo HTTPS se l'utente non specifica il protocollo nell'URL. In genera questa è considerata una procedura consigliata, ma può essere disattivata.

|    Chiave    |    Valore    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.defaultHTTPS     |     **ture** (impostazione predefinita) il gestore di protocollo predefinito è HTTPS<br>**false** il gestore di protocollo predefinito è HTTPS     |

#### <a name="disable-data-sharing-for-personalization"></a>Disabilitare la condivisione dei dati per la personalizzazione

Per impostazione predefinita, Microsoft Edge per iOS e Android richiede agli utenti la raccolta dei dati di utilizzo e la condivisione della cronologia di navigazione per personalizzare l'esperienza di navigazione. Le organizzazioni possono disabilitare la condivisione dei dati evitando che questa richiesta venga visualizzata dagli utenti finali.

|    Chiave    |    Valore    |
|----------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.disableShareUsageData    |     **true** disabilita la visualizzazione della richiesta agli utenti finali<br>**false** (impostazione predefinita) agli utenti viene richiesto di condividere i dati di utilizzo    |
|     com.microsoft.intune.mam.managedbrowser.disableShareBrowsingHistory    |     **true** disabilita la visualizzazione della richiesta agli utenti finali<br>**false** (impostazione predefinita) agli utenti viene richiesto di condividere i dati di navigazione     |

#### <a name="disable-specific-features"></a>Disabilitare funzionalità specifiche

Microsoft Edge per iOS e Android consente alle organizzazioni di disabilitare funzionalità abilitate per impostazione predefinita. Per disabilitare queste funzionalità, configurare le impostazioni seguenti:

|    Chiave    |    Valore    |
|-----------------------|-----------------------|
|    com.microsoft.intune.mam.managedbrowser.disabledFeatures    |    **password** disabilita le richieste che consentono di salvare le password per l'utente finale<br>**inprivate** disabilita InPrivate Browsing<p>Per disabilitare più funzionalità, separare i valori con `|`. Ad esempio, `inprivate|password`disabilita InPrivate e l'archiviazione password.     |

> [!NOTE]
> Microsoft Edge per Android non supporta la disabilitazione del gestore password.

#### <a name="disable-extensions"></a>Disabilita le estensioni

È possibile disabilitare il framework delle estensioni in Microsoft Edge per Android per impedire agli utenti di installare qualsiasi estensione app. Per eseguire questa operazione, configurare l'impostazione seguente:

|    Chiave    |    Valore    |
|-----------|-------------|
|    com.microsoft.intune.mam.managedbrowser.disableExtensionFramework    |    **true** disabilita il framework delle estensioni<br>**false** (impostazione predefinita) abilita il framework delle estensioni    |

### <a name="kiosk-mode-experiences-on-android-devices"></a>Esperienza in modalità tutto schermo su dispositivi Android

Microsoft Edge per Android può essere abilitato come app in modalità tutto schermo con le impostazioni seguenti:

|    Chiave    |    Valore    |
|-----------|-------------|
|    com.microsoft.intune.mam.managedbrowser.enableKioskMode    |    **true** abilita la modalità tutto schermo per Microsoft Edge per Android<br>**false** (impostazione predefinita) disabilita la modalità tutto schermo    |
|    com.microsoft.intune.mam.managedbrowser.showAddressBarInKioskMode    |    **true** visualizza la barra degli indirizzi in modalità tutto schermo<br> **false** (impostazione predefinita) nasconde la barra degli indirizzi in modalità tutto schermo    |
|    com.microsoft.intune.mam.managedbrowser.showBottomBarInKioskMode    |    **true** visualizza la barra delle azioni inferiore in modalità tutto schermo<br> **false** (impostazione predefinita) nasconde la barra inferiore in modalità tutto schermo    |

## <a name="data-protection-app-configuration-scenarios"></a>Scenari di configurazione dell'app per la protezione dei dati

Microsoft Edge per iOS e Android supporta i criteri di configurazione delle app per le seguenti impostazioni di protezione dati quando l'app viene gestita da Microsoft Endpoint Manager con criteri di protezione delle app di Intune applicati all'account aziendale o dell'istituto di istruzione che ha eseguito l'accesso all'app:

- Gestire la sincronizzazione degli account
- Gestire siti Web con restrizioni
- Gestire configurazioni proxy
- Gestire i siti di Single Sign-On NTLM

Queste impostazioni possono essere implementate nell'app indipendentemente dallo stato di registrazione del dispositivo.

### <a name="manage-account-synchronization"></a>Gestire la sincronizzazione degli account

Per impostazione predefinita, la sincronizzazione di Microsoft Edge consente agli utenti di accedere ai dati di navigazione su tutti i dispositivi connessi. I dati supportati dalla sincronizzazione includono:

- Preferiti
- Password
- Indirizzi e altro (immissione del modulo di riempimento automatico)

La funzionalità di sincronizzazione è abilitata tramite il consenso dell'utente e gli utenti possono attivare o disattivare la sincronizzazione per ogni tipo di dati elencato sopra. Per altre informazioni, vedere l'articolo [Sincronizzazione di Microsoft Edge](https://docs.microsoft.com/DeployEdge/microsoft-edge-enterprise-sync).

Le organizzazioni possono disabilitare la sincronizzazione di Microsoft Edge per iOS e Android. 

|Chiave  |Valore  |
|---------|---------|
|com.microsoft.intune.mam.managedbrowser.account.syncDisabled     |**true** (impostazione predefinita) consente la sincronizzazione di Microsoft Edge<br>**false** disabilita la sincronizzazione di Microsoft Edge          |

### <a name="manage-restricted-web-sites"></a>Gestire siti Web con restrizioni

Le organizzazioni possono definire i siti a cui gli utenti possono accedere con un account aziendale o dell'Istituto di istruzione in Microsoft Edge per iOS e Android. Se si usa un elenco di siti consentiti, gli utenti possono accedere solo ai siti inseriti in modo esplicito nell'elenco. Se si usa un elenco di siti bloccati, gli utenti possono accedere a tutti i siti esclusi quelli esplicitamente bloccati. Imporre solo un elenco di siti consentiti o uno di siti bloccati e non entrambi. Se vengono applicati entrambi, viene rispettato solo l'elenco dei siti consentiti.

L'organizzazione definisce inoltre cosa accade quando un utente tenta di passare a un sito Web con restrizioni. Per impostazione predefinita, le transizioni sono consentite. Se l'organizzazione lo consente, i siti Web con restrizioni possono essere aperti sull'account personale, in modalità InPrivate dell'account Azure AD o se il sito è completamente bloccato. Per altre informazioni sui vari scenari supportati, vedere l'articolo [Transizioni di siti Web con restrizioni in Microsoft Edge per dispositivi mobili](https://techcommunity.microsoft.com/t5/intune-customer-success/restricted-website-transitions-in-microsoft-edge-mobile/ba-p/1381333). Consentendo l'esperienza di transizione, gli utenti dell'organizzazione rimangono protetti, mantenendo al contempo le risorse aziendali al sicuro.

> [!NOTE]
> Microsoft Edge per iOS e Android può bloccare l'accesso ai siti solo quando vi si accede direttamente. Non blocca l'accesso quando gli utenti usano servizi intermedi (ad esempio, un servizio di traduzione) per accedere al sito.

Usare le coppie chiave/valore seguenti per configurare un elenco di siti consentiti o bloccati per Microsoft Edge per iOS e Android. 

|Chiave  |Valore  |
|---------|---------|
|com.microsoft.intune.mam.managedbrowser.AllowListURLs     |Il valore corrispondente per la chiave è un elenco di URL. Immettere tutti gli URL da consentire come singolo valore, separandoli tramite un carattere di barra verticale`|`.<p>**Esempi:**<br>`URL1|URL2|URL3`<br>`http://.contoso.com/|https://.bing.com/|https://expenses.contoso.com`         |
|com.microsoft.intune.mam.managedbrowser.BlockListURLs     |Il valore corrispondente per la chiave è un elenco di URL. Immettere tutti gli URL da bloccare come singolo valore, separandoli tramite un carattere di barra verticale`|`.<br>**Esempi:**<br>`URL1|URL2|URL3`<br>`http://.contoso.com/|https://.bing.com/|https://expenses.contoso.com`         |
|com.microsoft.intune.mam.managedbrowser.AllowTransitionOnBlock     |**true** (impostazione predefinita) consente a Microsoft Edge per iOS e Android di eseguire la transizione dei siti con restrizioni. Quando gli account personali non sono disabilitati, agli utenti viene richiesto di passare al contesto personale per aprire il sito con restrizioni o aggiungere un account personale. Se com.microsoft.intune.mam.managedbrowser.openInPrivateIfBlocked è impostato su true, gli utenti possono aprire il sito con restrizioni con InPrivate.<p>**false** impedisce la transizione degli utenti di Microsoft Edge per iOS e Android. Per gli utenti viene semplicemente visualizzato un messaggio che informa che il sito a cui stanno tentando di accedere è bloccato.         |
|com.microsoft.intune.mam.managedbrowser.openInPrivateIfBlocked     |**true** consente l'apertura di siti con restrizioni in modalità InPrivate dell'account Azure AD. Se l'account Azure AD è l'unico account configurato in Microsoft Edge per iOS e Android, il sito con restrizioni viene aperto automaticamente in modalità InPrivate. Se l'utente ha configurato un account personale, gli viene richiesto di scegliere tra aprire InPrivate o passare all'account personale.<p> **false** (impostazione predefinita) richiede che il sito con restrizioni venga aperto nell'account personale dell'utente. Se gli account personali sono disabilitati, il sito viene bloccato.<p>Per rendere effettiva questa impostazione, è necessario che com.microsoft.intune.mam.managedbrowser.AllowTransitionOnBlock sia impostato su true.          |
|com.microsoft.intune.mam.managedbrowser.durationOfOpenInPrivateSnackBar     | Immettere il numero di secondi per cui gli utenti visualizzeranno il collegamento "notifica snackbar" aperta con la modalità InPrivate. L'organizzazione richiede l'uso della modalità InPrivate per questo contenuto". Per impostazione predefinita, la notifica snackbar viene visualizzata per 7 secondi.

I siti seguenti sono sempre consentiti indipendentemente dalle impostazioni dell'elenco di consentiti o bloccati:
- `https://*.microsoft.com/*`
- `http://*.microsoft.com/*`
- `https://microsoft.com/*`
- `http://microsoft.com/*`
- `https://*.windowsazure.com/*`
- `https://*.microsoftonline.com/*`
- `https://*.microsoftonline-p.com/*`

#### <a name="url-formats-for-allowed-and-blocked-site-list"></a>Formati di URL per gli elenchi dei siti consentiti e bloccati 

È possibile usare diversi formati di URL per creare gli elenchi dei siti consentiti e bloccati. I modelli che è possibile usare sono descritti in dettaglio nella tabella seguente.

- Quando si aggiungono gli URL all'elenco, farli precedere dal prefisso **http://** o **https://** .
- È possibile usare il carattere jolly (\*) secondo le regole nell'elenco di modelli consentiti seguente.
- Un carattere jolly può corrispondere solamente a un componente intero del nome host (separato da punti) o a parti intere del percorso (separate da barre). Ad esempio, `http://*contoso.com`**non** è supportato.
- È possibile specificare numeri di porta nell'indirizzo. Se non si specifica un numero di porta, i valori usati sono:
  - Porta 80 per http
  - Porta 443 per https
- L'uso di caratteri jolly per il numero di porta **non** è supportato. Ad esempio, `http://www.contoso.com:*` e `http://www.contoso.com:*/` non sono supportati. 

    |    URL    |    Dettagli    |    Corrispondenze    |    Non corrisponde    |
    |-------------------------------------------|--------------------------------------------------------|-------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
    |    `http://www.contoso.com`    |    Corrisponde a una singola pagina    |    `www.contoso.com`    |    `host.contoso.com`<br>`www.contoso.com/images`<br>`contoso.com/`    |
    |    `http://contoso.com`    |    Corrisponde a una singola pagina    |    `contoso.com/`    |    `host.contoso.com`<br>`www.contoso.com/images`<br>`www.contoso.com`    |
    |    `http://www.contoso.com/*;`   |    Cerca una corrispondenza con tutti gli URL che iniziano con `www.contoso.com`    |    `www.contoso.com`<br>`www.contoso.com/images`<br>`www.contoso.com/videos/tvshows`    |    `host.contoso.com`<br>`host.contoso.com/images`    |
    |    `http://*.contoso.com/*`    |    Corrisponde a tutti i sottodomini in `contoso.com`    |    `developer.contoso.com/resources`<br>`news.contoso.com/images`<br>`news.contoso.com/videos`    |    `contoso.host.com`
    |    `http://*contoso.com/*`    |    Corrisponde a tutti i sottodomini che terminano con `contoso.com/`    |    `http://news-contoso.com`<br>`http://news-contoso.com.com/daily`    |    `http://news-contoso.host.com`    |
    `http://www.contoso.com/images`    |    Corrisponde a una singola cartella    |    `www.contoso.com/images`    |    `www.contoso.com/images/dogs`    |
    |    `http://www.contoso.com:80`    |    Corrisponde a una singola pagina, tramite un numero di porta    |    `http://www.contoso.com:80`    |         |
    |    `https://www.contoso.com`    |    Corrisponde a una singola pagina protetta    |    `https://www.contoso.com`    |    `http://www.contoso.com`    |
    |    `http://www.contoso.com/images/*`    |    Corrisponde a una singola cartella e a tutte le sottocartelle    |    `www.contoso.com/images/dogs`<br>`www.contoso.com/images/cats`    |    `www.contoso.com/videos`    |
  
- Di seguito sono riportati esempi di alcuni input che non è possibile specificare:
  - `*.com`
  - `*.contoso/*`
  - `www.contoso.com/*images`
  - `www.contoso.com/*images*pigs`
  - `www.contoso.com/page*`
  - Indirizzi IP
  - `https://*`
  - `http://*`
  - `https://*contoso.com`
  - `http://www.contoso.com:*`
  - `http://www.contoso.com: /*`

### <a name="manage-proxy-configuration"></a>Gestire configurazioni proxy

È possibile usare Microsoft Edge per iOS e Android e [Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started) in combinazione per consentire agli utenti l'accesso ai siti Intranet con i dispositivi mobili. Ad esempio: 

- Un utente sta usando l'app per dispositivi mobili Outlook, protetta da Intune. L'utente fa clic su un collegamento a un sito Intranet in un messaggio di posta elettronica e Microsoft Edge per iOS e Android riconosce che tale sito Intranet è stato esposto all'utente tramite Application Proxy. L'utente viene automaticamente indirizzato tramite Application Proxy, per autenticarsi con l'autenticazione a più fattori applicabile e con l'accesso condizionale prima di accedere al sito Intranet. L'utente può così accedere ai siti interni anche da dispositivi mobili e il collegamento in Outlook funziona come previsto.
- Un utente apre Edge per iOS e Android sul dispositivo iOS o Android. Se Edge per iOS e Android è protetto con Intune e Application Proxy è abilitato, l'utente può passare a un sito Intranet usando l'URL interno che è abituato a usare. Edge per iOS e Android riconosce che tale sito Intranet è stato esposto all'utente tramite Application Proxy. L'utente viene automaticamente indirizzato tramite Application Proxy, per eseguire l'autenticazione prima di raggiungere il sito Intranet. 

Prima di iniziare:

- Configurare le applicazioni interne tramite Azure AD Application Proxy.
  - Per configurare il proxy di applicazione e pubblicare le applicazioni, vedere la [documentazione del programma di installazione](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy).
- [Criteri di protezione delle app di Intune](app-protection-policy.md) devono essere assegnati all'app Edge per iOS e Android.
- Le app Microsoft devono avere un criterio di protezione delle app con l'impostazione di trasferimento dei dati **Limita il trasferimento di contenuto Web con altre app** impostata su **Microsoft Edge**.

> [!NOTE]
> Possono essere necessarie fino a 24 ore perché l'aggiornamento dei dati di reindirizzamento di Application Proxy sia visibile in Edge per iOS e Android.

Per abilitare il proxy di applicazione in Edge per iOS usare la coppia chiave/valore seguente:

|    Chiave    |    Valore    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.AppProxyRedirection    |    **true** abilita gli scenari di reindirizzamento di Azure AD Application Proxy<br>**false** (impostazione predefinita) impedisce scenari Azure AD App Proxy    |

> [!NOTE]
> Edge per Android non usa questa chiave. Edge per Android usa invece automaticamente la configurazione Azure AD Application Proxy, purché siano applicati criteri di protezione delle app sull'account Azure AD di accesso.

Per altre informazioni su come è possibile usare Edge per iOS e Android e Azure AD Application Proxy in combinazione per un accesso semplice e protetto alle app Web locali, vedere l'articolo [Meglio insieme: Intune and Azure Active Directory team up to improve user access](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/better-together-intune-and-azure-active-directory-team-up-to/ba-p/250254) (Meglio insieme: Intune e Azure Active Directory insieme per migliorare l'accesso utente). Questo blog post fa riferimento a Intune Managed Browser, ma il contenuto si applica anche a Edge per iOS e Android.

### <a name="manage-ntlm-single-sign-on-sites"></a>Gestire i siti di Single Sign-On NTLM

È possibile che le organizzazioni richiedano agli utenti di eseguire l'autenticazione con NTLM per accedere ai siti Web Intranet. Per impostazione predefinita, agli utenti viene richiesto di immettere le credenziali ogni volta che accedono a un sito Web che richiede l'autenticazione NTLM perché la memorizzazione nella cache delle credenziali NTLM è disabilitata. 

Le organizzazioni possono abilitare la memorizzazione nella cache delle credenziali NTLM per determinati siti Web. Per questi siti, dopo l'immissione delle credenziali da parte dell'utente e l'autenticazione corretta, le credenziali vengono memorizzate nella cache per 30 giorni per impostazione predefinita.


|Chiave  |Valore  |
|---------|---------|
|com.microsoft.intune.mam.managedbrowser.NTLMSSOURLs     |Il valore corrispondente per la chiave è un elenco di URL. Immettere tutti gli URL da consentire come singolo valore, separandoli tramite un carattere di barra verticale`|`.<p>**Esempi:**<br>`URL1|URL2`<br>`http://app.contoso.com/|https://expenses.contoso.com`<p>Per altre informazioni sui tipi di formati di URL supportati, vedere l'articolo [Formati di URL per gli elenchi dei siti consentiti e bloccati](#url-formats-for-allowed-and-blocked-site-list).         |
|com.microsoft.intune.mam.managedbrowser.durationOfNTLMSSO     |Numero di ore per la memorizzazione delle credenziali nella cache. Il valore predefinito è 720 ore         |

## <a name="deploy-app-configuration-scenarios-with-microsoft-endpoint-manager"></a>Implementare scenari di configurazione delle app con Microsoft Endpoint Manager

Se si usa Microsoft Endpoint Manager come provider di gestione delle app per dispositivi mobili, la procedura seguente consente di creare criteri di configurazione delle app per le app gestite. Dopo aver creato la configurazione, è possibile assegnare le impostazioni a gruppi di utenti.

1. Accedere a [Microsoft Endpoint Manager](https://endpoint.microsoft.com).

2. Selezionare **App** e quindi selezionare **Criteri di configurazione delle app**.

3. Nel pannello **Criteri di configurazione delle app** scegliere **Aggiungi** e selezionare **App gestite**.

4. Nel pannello sezione**Nozioni di base** immettere **Nome** e **Descrizione** facoltativa per le impostazioni di configurazione dell'app.

5. Per le **app pubbliche** scegliere **Seleziona app pubbliche**e quindi nel pannello **app di destinazione** scegliere **Edge per iOS e Android** selezionando entrambe le app della piattaforma iOS e Android. Fare clic su **Seleziona** per salvare le app pubbliche selezionate.

6. Fare clic su **Avanti** per completare le impostazioni di base dei criteri di configurazione dell'app.

7. Nella sezione **Impostazioni** espandere le impostazioni di configurazione di **Edge**.

8. Se si vogliono gestire le impostazioni di protezione dati, configurare le impostazioni desiderate di conseguenza:

    - Per il **reindirizzamento del proxy di applicazione**, scegliere tra le opzioni disponibili: **Abilita**, **Disabilita** (impostazione predefinita).

    - Per l'**URL di collegamento alla homepage**, specificare un URL valido che includa il prefisso *http://* o *https://* . Come misura di sicurezza, gli URL non corretti vengono bloccati.

    - Per i **Segnalibri gestiti**, specificare il titolo e un URL valido che includa il prefisso *http://* o *https://* .

    - For gli **URL consentiti**, specificare un URL valido (sono consentiti solo questi URL e nessun altro sito è accessibile). Per altre informazioni sui tipi di formati di URL supportati, vedere l'articolo [Formati di URL per gli elenchi dei siti consentiti e bloccati](#url-formats-for-allowed-and-blocked-site-list).

    - Per gli **URL bloccati**, specificare un URL valido (solo questi URL sono bloccati). Per altre informazioni sui tipi di formati di URL supportati, vedere l'articolo [Formati di URL per gli elenchi dei siti consentiti e bloccati](#url-formats-for-allowed-and-blocked-site-list).

    - Per **Reindirizza i siti con restrizioni al contesto personale**, scegliere tra le opzioni disponibili: **Abilita** (impostazione predefinita), **Disabilita**.

    > [!NOTE]
    > Se la politica definisce sia URL consentiti che URL bloccati, viene rispettato solo l'elenco consentito.

9. Se si desiderano impostazioni di configurazione dell'app aggiuntive non esposte nel criterio precedente, espandere il nodo **Impostazioni di configurazione generali** e immettere le coppie chiave-valore adeguate.

10. Dopo aver configurato le impostazioni, scegliere **Avanti**.

11. Nella sezione **Assegnazioni** scegliere **Selezionare i gruppi da includere**. Selezionare il gruppo di Azure AD a cui si vogliono assegnare i criteri di configurazione dell'app e quindi scegliere **Seleziona**.

12. Al termine delle assegnazioni, scegliere **Avanti**.

13. Nella schermata **Creare criteri di configurazione dell'app Consultare + Creare** consultare le impostazioni configurate e scegliere **Crea**.

I nuovi criteri di configurazione creati verranno visualizzi nel riquadro **Configurazione dell'app**.

## <a name="use-edge-for-ios-and-android-to-access-managed-app-logs"></a>Usare Edge per iOS e Android per accedere ai log delle app gestite

Gli utenti che hanno installato Edge per iOS e Android nel dispositivo iOS o Android possono visualizzare lo stato di gestione di tutte le app pubblicate Microsoft. Possono inviare log per la risoluzione dei problemi relativi alle app iOS o Android gestite seguendo questa procedura:

1. Aprire Edge per iOS e Android sul tuo dispositivo.
2. Digitare `about:intunehelp` nella casella dell'indirizzo.
3. Edge per iOS e Android avvia la modalità di risoluzione dei problemi.

Per un elenco delle impostazioni archiviate nei log delle app, vedere [Esaminare i log di protezione delle app nel Managed Browser](app-protection-policy-settings-log.md).

Per informazioni su come visualizzare i log nei dispositivi Android, vedere [Inviare i log al supporto tecnico dell'azienda tramite posta elettronica](https://docs.microsoft.com/mem/intune/user-help/send-logs-to-your-it-admin-by-email-android).

## <a name="next-steps"></a>Passaggi successivi

- [Che cosa sono i criteri di protezione delle app?](app-protection-policy.md) 
- [Criteri di configurazione delle app per Microsoft Intune](app-configuration-policies-overview.md)