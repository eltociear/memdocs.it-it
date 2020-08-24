---
title: Come personalizzare le app Portale aziendale Intune, il sito Web Portale aziendale e l'app Intune
titleSuffix: Microsoft Intune
description: Informazioni su come applicare personalizzazioni specifiche dell'azienda alle app Portale aziendale Intune, al sito Web Portale aziendale e all'app Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 08/12/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: dec6f258-ee1b-4824-bf66-29053051a1ae
ms.reviewer: esthermsft
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: a82fbfa9e494828450729e29467580c29a590282
ms.sourcegitcommit: d1bfd5b8481439babc7eae43493f28edaebe647a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/13/2020
ms.locfileid: "88179554"
---
# <a name="how-to-customize-the-intune-company-portal-apps-company-portal-website-and-intune-app"></a>Come personalizzare le app Portale aziendale Intune, il sito Web Portale aziendale e l'app Intune

Le app Portale aziendale, il sito Web Portale aziendale e l'app Intune in Android consentono agli utenti di accedere ai dati aziendali ed eseguire attività comuni. Le attività comuni possono includere la registrazione dei dispositivi, l'installazione di app e la ricerca di informazioni, ad esempio di assistenza dal reparto IT. Inoltre, consentono agli utenti di accedere in modo sicuro alle risorse aziendali. L'esperienza utente finale offre diverse pagine, ad esempio Pagina iniziale, App, Dettagli app, Dispositivi e Dettagli dispositivo. Per trovare rapidamente le app all'interno del Portale aziendale, è possibile filtrare le app nella pagina App.

## <a name="customizing-the-user-experience"></a>Personalizzazione dell'esperienza utente

Con la personalizzazione dell'esperienza utente finale sarà possibile offrire agli utenti finali un'esperienza familiare e utile. A tale scopo, andare all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) e selezionare **Amministrazione tenant** > **Personalizzazione**, dove è possibile modificare i criteri predefiniti o creare fino a 10 criteri di gruppo mirati. Queste impostazioni si applicano alle app Portale aziendale, al sito Web Portale aziendale e all'app Intune in Android.

## <a name="branding"></a>Personalizzazione

La tabella seguente fornisce i dettagli di personalizzazione per l'esperienza utente finale:

| Nome del campo | Altre informazioni |
|---|---|---|
| **Nome organizzazione** | Questo nome viene visualizzato nella messaggistica nell'esperienza utente finale. Può essere impostato anche per la visualizzazione nelle intestazioni usando l'impostazione **Mostra su intestazione**. La lunghezza massima è di 40 caratteri. |
| **Colore** | Scegliere **Standard** per selezionare tra cinque colori standard. Scegliere **Personalizzato** per selezionare un colore specifico in base a un valore in formato esadecimale. |
| **Colore del tema** | Impostare il colore del tema da visualizzare nell'esperienza utente finale. Il colore del testo verrà impostato automaticamente su nero o bianco in modo che sia visibile sul colore del tema selezionato. |
| **Mostra su intestazione** | Specificare se l'intestazione nelle esperienze utente finale deve includere **il logo e il nome dell'organizzazione**, **solo il logo dell'organizzazione** o **solo il nome dell'organizzazione**. Le caselle di anteprima seguenti visualizzano solo i logo, non il nome.  |
| **Carica il logo per lo sfondo con colore del tema** | Caricare il logo che si desidera visualizzare sopra il colore del tema selezionato. Per assicurare un aspetto ottimale, caricare un logo con uno sfondo trasparente. È possibile visualizzare il risultato nella casella di anteprima sotto l'impostazione.<p>Dimensioni massime immagine: 400 x 400 px<br>Dimensioni massime del file:   750 kB<br>Tipo di file: PNG, JPG o JPEG |
| **Carica il logo per lo sfondo bianco o chiaro** | Caricare il logo da visualizzare sopra gli sfondi di colore bianco o chiaro. Per assicurare un aspetto ottimale, caricare un logo con uno sfondo trasparente. È possibile visualizzare il risultato su uno sfondo bianco nella casella di anteprima sotto l'impostazione.<p>Dimensioni massime immagine: 400 x 400 px<br>Dimensioni massime del file: 750 kB<br>Tipo di file: PNG, JPG o JPEG |
| **Carica l'immagine del marchio** | Caricare un'immagine del marchio dell'organizzazione.<p><ul><li>Larghezza immagine consigliata: Maggiore di 1125 px (deve essere almeno 650 px)</li><li>Dimensioni massime immagine: 1,3 MB</li><li>Tipo di file: PNG, JPG o JPEG</li><li>Viene visualizzato nelle posizioni seguenti:</li><ul><li>Portale aziendale iOS/iPadOS: Immagine di sfondo nella pagina del profilo dell'utente.</li><li>Sito Web del portale aziendale:   Immagine di sfondo nella pagina del profilo dell'utente.</li><li>App Intune Android: nel menu e come immagine di sfondo nella pagina del profilo dell'utente.</li></ul></ul> |

> [!NOTE]
> Quando si installa un'applicazione iOS/iPadOS dal Portale aziendale, viene inviata una richiesta. Ciò avviene quando l'app iOS/iPadOS è collegata all'App Store, a un programma Volume Purchase Program (VPP) oppure a un'app line-of-business. La richiesta consente agli utenti di accettare l'azione o consentire la gestione dell'app. Nella richiesta sarà visualizzato il nome della società o, quando il nome della società non è disponibile, sarà visualizzato **Portale aziendale**.

### <a name="brand-image-best-practices"></a>Procedure consigliate per l'immagine del marchio

L'immagine del marchio può migliorare la fiducia dell'utente presentando un forte senso di marchio dell'organizzazione. Di seguito sono riportati alcuni suggerimenti che è possibile prendere in considerazione per l'acquisizione, la scelta e l'ottimizzazione dell'immagine per le diverse posizioni di visualizzazione.

- Rivolgersi al reparto marketing o pubblicità. È possibile che il reparto abbia già a disposizione un set di immagini del marchio approvate. Il reparto può anche aiutare l'utente ad adattare le immagini alle esigenze specifiche.
- Prendere in considerazione sia la composizione verticale che quella orizzontale. L'immagine deve avere uno sfondo sufficiente che circonda il punto focale. L'immagine può essere ritagliata in diversi modi in base alle dimensioni del dispositivo, all'orientamento e alla piattaforma.
- Evitare di usare un'immagine generica. L'immagine deve riflettere il marchio dell'organizzazione ed essere familiare agli utenti. Se non è disponibile alcuna immagine, è preferibile non usare un'immagine generica che non ha alcun significato per l'utente.
- Rimuovere i metadati non necessari. Il file di immagine può includere i metadati, ad esempio il profilo della fotocamera, la posizione geografica, il titolo, il sottotitolo e così via. Usare uno strumento di ottimizzazione delle immagini per rimuovere queste informazioni per mantenere la qualità e rispettare il limite di dimensione del file.

### <a name="brand-image-examples"></a>Esempi di immagini di marchio

L'immagine seguente mostra un esempio di immagine del marchio in un iPhone:

<img alt="Screenshot of example iPhone branding image" src="./media/company-portal-app/company-portal-app-01.png" width="250">

L'immagine seguente mostra un esempio dell'immagine del marchio nell'app Intune per Android:

<img alt="Screenshot of example #1 for Intune app for Android branding image" src="./media/company-portal-app/company-portal-app-02.png" width="250">

<img alt="Screenshot of example #2 for Intune app for Android branding image" src="./media/company-portal-app/company-portal-app-03.png" width="250">

## <a name="support-information"></a>Informazioni di supporto

Immettere le informazioni sul supporto dell'organizzazione per consentire ai dipendenti di porre domande. Le informazioni sul supporto vengono visualizzate nelle pagine **Supporto**, **Guida e supporto** e **Supporto tecnico** nell'esperienza utente finale.

| Nome del campo | Lunghezza massima | Altre informazioni |
|------------------------|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Nome contatto | 40 | Questo è il nome della persona che gli utenti potranno raggiungere quando contatteranno il supporto tecnico. |
| Numero di telefono | 20 | Questo numero consente agli utenti di contattare il supporto tecnico. |
| Indirizzo di posta elettronica | 40 | Questo indirizzo e-mail è l'indirizzo a cui gli utenti inviano messaggi di posta elettronica per richiedere il supporto. È necessario immettere un indirizzo di posta elettronica valido nel formato `alias@domainname.com`. |
| Nome sito Web | 40 | Questo è il nome descrittivo visualizzato in alcune posizioni per l'URL del sito Web del supporto tecnico. Se si specifica un URL del sito Web di supporto e nessun nome descrittivo, viene visualizzato l'URL nelle esperienze utente finale.  |
| URL del sito Web | 150 | Sito Web di supporto che deve essere usato dagli utenti. Il formato dell'URL deve essere `https://www.contoso.com`.  |
| Informazioni aggiuntive | 120 | Inserire quindi eventuali messaggi aggiuntivi relativi al supporto per gli utenti. |

## <a name="configuration"></a>Configurazione

È possibile configurare l'esperienza del Portale aziendale specificatamente per la registrazione, la privacy, le notifiche, le origini app e le azioni self-service.

### <a name="enrollment"></a>Registrazione

La tabella seguente offre altri dettagli di configurazione:

| Nome del campo | Lunghezza massima | Altre informazioni |
|------------------------------------------------------|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Registrazione del dispositivo | N/D | Specificare se e in che modo è consigliabile richiedere agli utenti di registrarsi nella gestione dei dispositivi mobili. Per altre informazioni vedere le [opzioni delle impostazioni per la Registrazione dei dispositivi](../apps/company-portal-app.md#device-enrollment-setting-options). |

#### <a name="device-enrollment-setting-options"></a>Opzioni di impostazione della registrazione dei dispositivi

> [!NOTE]
> Per il supporto per l'impostazione della registrazione dei dispositivi è necessario che gli utenti finali dispongano delle versioni del Portale aziendale seguenti:
> - Portale aziendale in iOS/iPadOS: versione 4.4 o successiva
> - Portale aziendale in Android: versione 5.0.4715.0 o successiva 

> [!IMPORTANT]
> Le impostazioni seguenti non si applicano ai dispositivi iOS/iPadOS configurati per la registrazione con la [Registrazione automatica dei dispositivi](../enrollment/device-enrollment-program-enroll-ios.md). Indipendentemente dal modo in cui queste impostazioni sono configurate, i dispositivi iOS/iPadOS configurati per la Registrazione automatica dei dispositivi verranno registrati durante il flusso predefinito e agli utenti verrà richiesto di eseguire l'accesso all'avvio del Portale aziendale.
> 
> Le impostazioni seguenti si applicano ai dispositivi Android configurati con [Registrazione per dispositivi mobili Samsung KNOX](../enrollment/android-samsung-knox-mobile-enroll.md). Se un dispositivo è stato configurato per Registrazione per dispositivi mobili Samsung KNOX e la registrazione del dispositivo è impostata su Non disponibile, il dispositivo non sarà in grado di registrarsi durante il flusso predefinito.

|    Opzioni di registrazione dei dispositivi    |    Descrizione    |    Richieste di elenco di controllo    |    Notifica    |    Stato dei dettagli del dispositivo    |    Stato dei dettagli dell'app (per app che richiedono la registrazione)    |
|-----------------------------------|-------------------------------------------------------------------------------------------------------------------------|-------------------------|--------------------|-----------------------------|--------------------------------------------------------------------|
|    Disponibile, con richieste di conferma    |    Esperienza predefinita con richieste di registrazione in tutte le posizioni possibili.    |    Sì    |    Sì    |    sì    |    sì    |
|    Disponibile, senza richieste di conferma    |    L'utente può eseguire la registrazione tramite lo stato nei dettagli del dispositivo per il dispositivo corrente o dalle app che richiedono la registrazione.    |    No    |    No    |    Sì    |    Sì    |
|    Non disponibile    |    Gli utenti non possono eseguire la registrazione.    |    No    |    No    |    No    |    No    |

### <a name="privacy"></a>Privacy

La tabella seguente offre dettagli di configurazione specifici per la privacy:

| Nome del campo | Lunghezza massima | Altre informazioni |
|------------------------------------------------------|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| URL dell'informativa sulla privacy | 79 | Impostare l'informativa sulla privacy dell'organizzazione in modo che venga visualizzata quando gli utenti fanno clic sui collegamenti per la privacy. Immettere un URL valido nel formato `https://www.contoso.com`. |
| Messaggio sulla privacy nel Portale aziendale per iOS/iPadOS | 520 | Mantenere il messaggio **predefinito** o definirne uno **personalizzato** per elencare gli elementi che l'organizzazione può o non è in grado di visualizzare nei dispositivi iOS/iPadOS gestiti. È possibile usare il markdown per aggiungere punti elenco, grassetto, corsivo e collegamenti. Gli utenti visualizzeranno anche un elenco di elementi che possono essere visualizzati ed eseguiti dall'organizzazione, ma tale elenco viene generato automaticamente da Intune e non è personalizzabile. |

### <a name="device-ownership-notification"></a>Notifica relativa alla proprietà del dispositivo

La tabella seguente offre dettagli di configurazione specifici per le notifiche:

| Nome del campo | Lunghezza massima | Altre informazioni |
|------------------------------------------------------|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Inviare una notifica push agli utenti quando il tipo di proprietà del dispositivo cambia da personale ad aziendale (solo Android e iOS/iPadOS)​ | N/D | Inviare una notifica push agli utenti del portale aziendale sia Android che iOS quando il tipo di proprietà del dispositivo cambia da personale ad aziendale. Per impostazione predefinita, questa notifica push è disattivata. Quando la proprietà del dispositivo è impostata su aziendale, Intune ha un accesso più ampio al dispositivo, che include l'inventario completo delle app, la rotazione delle chiavi FileVault, il recupero dei numeri di telefono e alcune azioni remote selezionate. Per altre informazioni, vedere [Modificare la proprietà del dispositivo](../enrollment/corporate-identifiers-add.md#change-device-ownership).  |

### <a name="app-sources"></a>Origini app

È possibile scegliere le origini app aggiuntive che verranno visualizzate sul Portale aziendale. La tabella seguente offre dettagli di configurazione specifici per le origini app:

| Nome del campo | Lunghezza massima | Altre informazioni |
|------------------------------------------------------|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Applicazioni aziendali Azure AD | N/D | Selezionare **Nascondi** oppure **Mostra** per visualizzare le **applicazioni aziendali Azure AD** nel Portale aziendale per ogni utente finale. Per altre informazioni vedere [Opzioni di impostazione dell'origine app](../apps/company-portal-app.md#app-source-setting-options). |
| Applicazioni di Office Online | N/D | Selezionare **Nascondi** oppure **Mostra** per visualizzare le **applicazioni di Office Online** nel Portale aziendale per ogni utente finale. Per altre informazioni vedere [Opzioni di impostazione dell'origine app](../apps/company-portal-app.md#app-source-setting-options). |

#### <a name="app-source-setting-options"></a>Opzioni di impostazione dell'origine app

> [!NOTE]
> Il sito Web del Portale aziendale supporterà inizialmente la visualizzazione delle app da altri servizi Microsoft.

È possibile nascondere o mostrare le **applicazioni aziendali Azure AD** e le **applicazioni di Office Online** nel Portale aziendale per ogni utente finale. L'opzione **Mostra** farà in modo che il Portale aziendale visualizzi l'intero catalogo applicazioni dal servizio o dai servizi Microsoft selezionati e assegnati all'utente. Le **applicazioni aziendali Azure AD** vengono registrate e assegnate tramite il [portale di Azure](https://portal.azure.com). Le **applicazioni Office Online** vengono assegnate usando i controlli di licenza disponibili nell'[Interfaccia di amministrazione di M365](https://admin.microsoft.com). Per trovare questa impostazione di configurazione, nel [centro di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) selezionare **Amministrazione del tenant** > **Personalizzazione**. Per impostazione predefinita, ogni origine di app aggiuntiva verrà impostata su **Nascondi**. 

### <a name="customizing-user-self-service-actions-for-the-company-portal"></a>Personalizzazione delle azioni self-service che l'utente può eseguire sul Portale aziendale

È possibile personalizzare le azioni self-service del dispositivo disponibili che vengono visualizzate dagli utenti finali nell'app e nel sito Web Portale aziendale. Per contribuire a evitare le azioni non previste nel dispositivo, sarà possibile configurare le impostazioni per l'app Portale aziendale selezionando **Amministrazione del tenant** > **Personalizzazione**. 

Sono disponibili le azioni seguenti:
- Nascondi il pulsante **Rimuovi** nei dispositivi Windows aziendali.
- Nascondi il pulsante **Ripristina** nei dispositivi Windows aziendali.
- Nascondi il pulsante **Rimuovi** nei dispositivi iOS/iPadOS aziendali.
- Nascondi il pulsante **Ripristina** nei dispositivi iOS/iPadOS aziendali.

> [!NOTE]
> Queste azioni possono essere usate per limitare le azioni del dispositivo nell'app e nel sito Web Portale aziendale e non implementano criteri di restrizione dei dispositivi. Per impedire agli utenti di eseguire il ripristino delle impostazioni di fabbrica o la rimozione di MDM dalle impostazioni, è necessario configurare i criteri di restrizione dei dispositivi. 

## <a name="opening-web-company-portal-applications"></a>Apertura di applicazioni Portale aziendale Web
Per le applicazioni Web Portale aziendale, se l'utente finale ha installato l'applicazione Portale aziendale, per gli utenti finali verrà visualizzata una finestra di dialogo in cui viene chiesto come vogliono aprire l'applicazione all'esterno del browser. Se l'app non si trova nel percorso di Portale aziendale, per il sito Web Portale aziendale verrà aperta la home page. Se l'app si trova nel percorso, il Portale aziendale aprirà l'app specifica. 

Quando si seleziona il Portale aziendale, l'utente viene indirizzato alla pagina corrispondente nell'applicazione quando il percorso URI è uno dei seguenti:

- `/apps` -Il Portale aziendale Web apre la pagina App in cui sono elencate tutte le app.
- `/apps/[appID]` -Il Portale aziendale Web apre la pagina Dettagli dell'app corrispondente.
- *Il percorso URI è diverso o imprevisto* - Verrà visualizzata la home page di Portale aziendale Web.

Se l'utente non ha l'app Portale aziendale, l'utente verrà indirizzato al Portale aziendale Web.

## <a name="company-portal-derived-credentials-for-iosipados-devices"></a>Credenziali derivate del portale aziendale per i dispositivi iOS/iPadOS

Intune supporta la verifica dell'identità personale (PIV, Personal Identity Verification) e le credenziali derivate CAC (Common Access Card) in collaborazione con i provider di credenziali DISA Purebred, Entrust Datacard e Intercede. Gli utenti finali eseguiranno ulteriori passaggi dopo la registrazione del dispositivo iOS/iPadOS per verificarne l'identità nell'applicazione Portale aziendale. Le credenziali derivate verranno abilitate per gli utenti impostando prima di tutto un provider di credenziali per il tenant, quindi specificando come destinazione un profilo che usa credenziali derivate per utenti o dispositivi.

> [!NOTE]
> L'utente visualizzerà le istruzioni sulle credenziali derivate in base al collegamento specificato tramite Intune.

Per altre informazioni sulle credenziali derivate per i dispositivi iOS/iPadOS, vedere [Usare le credenziali derivate in Microsoft Intune](../protect/derived-credentials.md).

## <a name="dark-mode-for-the-company-portal"></a>Modalità scura per il Portale aziendale

La modalità scura è disponibile per il Portale aziendale iOS/iPadOS, macOS e Windows. Gli utenti possono scaricare le app, gestire i propri dispositivi e ottenere supporto tecnico nella combinazione di colori scelta in base alle impostazioni del dispositivo. Il Portale aziendale iOS/iPadOS, macOS e Windows adatterà automaticamente le impostazioni del dispositivo dell'utente finale per la modalità scura o chiara.

## <a name="windows-company-portal-keyboard-shortcuts"></a>Tasti di scelta rapida per il portale aziendale di Windows

Gli utenti finali possono usare tasti di scelta rapida per eseguire azioni di spostamento, sulle app e sui dispositivi nel portale aziendale di Windows.

I tasti di scelta rapida seguenti sono disponibili nell'app Portale aziendale di Windows.

| Area | Descrizione | Tasti di scelta rapida |
|--------------------|----------------|-------------------|
| Menu di spostamento | Spostamento | ALT+M |
|  | Home | ALT+H |
|  | Tutte le app | ALT+A |
|  | App installate | ALT+I |
|  | Inviare un feedback | ALT+F |
|  | Profilo personale | ALT+U |
|  | Impostazioni | ALT+T |
| Home - Riquadro dispositivo | Rinomina | F2 |
|  | Remove | CTRL+D o CANC |
|  | Verifica l'accesso | CTRL+M o F9 |
| Dettagli dispositivo | Rinomina | F2 |
|  | Remove | CTRL+D o CANC |
|  | Verifica l'accesso | CTRL+M o F9 |
| Dettagli dell'app | Installazione | CTRL+I |
| Dispositivi | Disponibile | CTRL+D |

Gli utenti finali potranno anche visualizzare i tasti di scelta rapida disponibili nell'app Portale aziendale di Windows.

![Screenshot dei tasti di scelta rapida disponibili nell'app Portale aziendale di Windows](./media/company-portal-app/company-portal-app-04.png)

## <a name="user-self-service-device-actions-from-the-company-portal"></a>Azioni self-service che l'utente può eseguire nel dispositivo dal Portale aziendale

Gli utenti possono eseguire azioni nei dispositivi locali o remoti tramite l'app Portale aziendale, il sito Web dell'app Portale aziendale o l'app Intune in Android. Le azioni che un utente può eseguire variano in base alla configurazione e alla piattaforma del dispositivo. In tutti i casi, le azioni sui dispositivi remoti possono essere eseguite solo dall'utente primario del dispositivo.  

Tra le azioni self-service disponibili per i dispositivi sono incluse le seguenti:

- **Ritiro**: rimuove il dispositivo dalla Gestione di Intune. Nell'app Portale aziendale e nel sito Web questa azione viene visualizzata come **Rimuovi**.
- **Cancellazione**: questa azione avvia la reimpostazione del dispositivo. Nel sito Web del Portale aziendale viene visualizzato come **Ripristina** o **Ripristino delle impostazioni predefinite** nell'app Portale aziendale per iOS/iPadOS.
- **Ridenominazione**: questa azione modifica il nome del dispositivo che l'utente può visualizzare nel Portale aziendale. Non modifica il nome del dispositivo locale, ma solo l'elenco nel Portale aziendale.
- **Sincronizzazione**: questa azione avvia la sincronizzazione del dispositivo con il servizio Intune. Viene visualizzato come **Verifica stato** nel Portale aziendale.
- **Blocco remoto**: blocca il dispositivo e richiede un PIN per poterlo sbloccare.
- **Reimpostazione passcode**: questa azione reimposta il passcode del dispositivo. Nei dispositivi iOS/iPadOS il passcode verrà rimosso e l'utente finale dovrà immettere un nuovo codice nelle impostazioni. Nei dispositivi Android supportati Intune genera un nuovo passcode che viene temporaneamente visualizzato nel Portale aziendale.
- **Recupero chiave**: questa azione recupera una chiave di ripristino personale per i dispositivi macOS crittografati dal sito Web del Portale aziendale. 

Per personalizzare le azioni self-service disponibili per gli utenti vedere [Personalizzazione delle azioni self-service degli utenti per il Portale aziendale](../apps/company-portal-app.md#customizing-user-self-service-actions-for-the-company-portal).

### <a name="self-service-actions"></a>Azioni self-service

Alcune piattaforme e configurazioni non consentono azioni self-service nel dispositivo. La tabella seguente contiene altri dettagli sulle azioni self-service:

| Action | Windows 10<sup>(3)</sup> | iOS/iPadOS<sup>(3)</sup> | macOS<sup>(3)</sup> | Android<sup>(3)</sup> |
|----------------------|--------------------------|-------------------|-----------------------------------|-------------------------|
| Ritiro | Disponibile<sup>(1)</sup> | Disponibile<sup>(9)</sup> | Disponibile | Disponibile<sup>(7)</sup> |
| Cancellazione | Disponibile | Disponibile<sup>(5)</sup><sup>(9)</sup> | N/D | Disponibile<sup>(7)</sup> |
| Ridenominazione<sup>(4)</sup> | Disponibile | Disponibile | Disponibile | Disponibile |
| Sincronizza | Disponibile | Disponibile | Disponibile | Disponibile |
| Recupero chiavi | ND | ND | Disponibile<sup>(2)</sup> | N/D |

<sup>(1)</sup> Il **ritiro** è sempre bloccato nei dispositivi Windows aggiunti ad Azure AD.<br>
<sup>(2)</sup> Il **recupero chiavi** per macOS è disponibile solo tramite il portale Web.<br>
<sup>(3) </sup> tutte le azioni remote sono disabilitate se si usa la registrazione di un manager di registrazione dispositivi.<br>
<sup>(4)</sup> La **ridenominazione** modifica solo il nome del dispositivo nell'app Portale aziendale o nel portale Web, non nel dispositivo.<br>
<sup>(5)</sup> La **cancellazione** non è disponibile nei dispositivi iOS/iPadOS registrati dall'utente.<br>
<sup>(6)</sup> La **reimpostazione del passcode** non è supportata in alcune configurazioni di Android e Android Enterprise. Per altre informazioni, vedere [Reimpostare o rimuovere il passcode di un dispositivo in Intune](../remote-actions/device-passcode-reset.md).<br>
<sup>(7)</sup> Il **ritiro** e la **cancellazione** non sono disponibili in scenari di proprietari di dispositivi Android Enterprise (COPE, COBO, COSU).<br>
<sup>(8)</sup> La **reimpostazione del passcode** non è supportata nei dispositivi iOS/iPadOS registrati dall'utente.<br>
<sup>(9)</sup>Tutti i dispositivi di Registrazione automatica dei dispositivi iOS/iPads (noti in precedenza come DEP) presentano le opzioni **ritiro** e **cancellazione** disabilitate.

### <a name="app-logs"></a>Log dell'app

Se si usa Azure per enti pubblici, l'utente finale riceve i log delle app per prendere decisioni in merito alla condivisione quando avvia il processo per visualizzare la Guida per un problema. Se tuttavia non si usa Azure per enti pubblici, il portale aziendale invierà i log delle app direttamente a Microsoft quando l'utente avvia il processo per visualizzare la Guida per un problema. Inviando i log delle app a Microsoft sarà più semplice risolvere i problemi.

> [!NOTE]
> In conformità con i criteri Microsoft e Apple, i dati raccolti dal servizio non vengono venduti per alcun motivo a terze parti.

## <a name="next-steps"></a>Passaggi successivi

- [Configurare il logo dell'organizzazione e il colore del marchio per le pagine Nuova scheda in Microsoft Edge per iOS e Android](manage-microsoft-edge.md#organization-logo-and-brand-color)
- [Aggiungere app](apps-add.md)
