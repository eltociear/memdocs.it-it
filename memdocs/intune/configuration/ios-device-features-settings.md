---
title: Impostazioni delle funzionalità dei dispositivi iOS/iPadOS in Microsoft Intune - Azure | Microsoft Docs
description: Visualizzare tutte le impostazioni per configurare i dispositivi iOS/iPadOS per AirPrint, layout della schermata iniziale, notifiche delle app, dispositivi condivisi, Single Sign-On e filtro del contenuto Web in Microsoft Intune. Usare queste impostazioni in un profilo di configurazione del dispositivo per configurare i dispositivi iOS/iPadOS per l'uso di queste funzionalità Apple nell'organizzazione.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/20/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: ''
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 09ccfe079511c90f2ce7ecf6c27d4dfcf1c85327
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/25/2020
ms.locfileid: "88820188"
---
# <a name="ios-and-ipados-device-settings-to-use-common-iosipados-features-in-intune"></a>Impostazioni dei dispositivi iOS e iPadOS per usare le funzionalità iOS/iPadOS comuni in Intune

Intune include alcune impostazioni predefinite per consentire agli utenti di iOS/iPadOS di usare diverse funzionalità Apple nei dispositivi. Ad esempio è possibile controllare le stampanti AirPrint, aggiungere app e cartelle al dock e alle pagine nella schermata iniziale, visualizzare le notifiche delle app, visualizzare i dettagli dei tag degli asset nella schermata di blocco, usare l'autenticazione Single Sign-On e usare l'autenticazione basata su certificati.

Usare queste funzionalità per controllare i dispositivi iOS/iPadOS nella soluzione di gestione di dispositivi mobili (MDM).

L'articolo elenca queste impostazioni e descrive la funzione di ogni impostazione. Per altre informazioni su queste funzionalità, vedere [Aggiungere impostazioni relative alle funzionalità dei dispositivi iOS/iPadOS e macOS](device-features-configure.md).

## <a name="before-you-begin"></a>Prima di iniziare

[Creare un profilo delle funzionalità del dispositivo iOS/iPadOS](device-features-configure.md).

> [!NOTE]
> Queste impostazioni si applicano a diversi tipi di registrazione, con alcune impostazioni che si applicano a tutte le opzioni di registrazione. Per altre informazioni sui diversi tipi di registrazione, vedere [Registrazione di iOS/iPadOS](../enrollment/ios-enroll.md).

## <a name="airprint"></a>AirPrint

### <a name="settings-apply-to-all-enrollment-types"></a>Le impostazioni si applicano a: Tutti i tipi di registrazione

> [!NOTE]
> Assicurarsi di aggiungere tutte le stampanti allo stesso profilo. Apple impedisce a più profili AirPrint di avere come destinazione lo stesso dispositivo.

- **Indirizzo IP**: immettere l'indirizzo IPv4 o IPv6 della stampante. Se si usano i nomi host per identificare le stampanti, è possibile ottenere l'indirizzo IP effettuando il ping della stampante nel terminale. Per informazioni più dettagliate, vedere Ottenere l'indirizzo IP e il percorso (in questo articolo).
- **Percorso**: il percorso è in genere `ipp/print` per le stampanti di rete. Per informazioni più dettagliate, vedere Ottenere l'indirizzo IP e il percorso (in questo articolo).
- **Porta**: immettere la porta di ascolto della destinazione AirPrint. Se si omette questa proprietà, AirPrint usa la porta predefinita. Disponibile in iOS 11.0+ e iPadOS 13.0+.
- **TLS**: **Abilita** protegge le connessioni AirPrint con Transport Layer Security (TLS). Disponibile in iOS 11.0+ e iPadOS 13.0+.

Per aggiungere server AirPrint, è possibile:

- **Aggiungi** aggiunge il server AirPrint all'elenco. È possibile aggiungere molti server AirPrint.
- **Importare** un file con valori delimitati da virgole (CSV) con queste informazioni. In alternativa, scegliere **Esporta** per creare un elenco dei server AirPrint aggiunti.

### <a name="get-server-ip-address-resource-path-and-port"></a>Ottenere indirizzo IP del server, percorso della risorsa e porta

Per aggiungere i server AirPrinter, sono necessari l'indirizzo IP della stampante, il percorso della risorsa e la porta. La procedura seguente mostra come ottenere queste informazioni.

1. In un dispositivo Mac connesso alla stessa rete locale (subnet) delle stampanti AirPrint aprire **Terminale** (da **/Applicazioni/Utilità**).
2. Nel Terminale digitare `ippfind` e premere INVIO.

    Prendere nota delle informazioni della stampante. Ad esempio, potrebbe restituire un valore simile a `ipp://myprinter.local.:631/ipp/port1`. La prima parte è il nome della stampante. L'ultima parte (`ipp/port1`) è il percorso della risorsa.

3. Nel Terminale digitare `ping myprinter.local` e premere INVIO.

   Prendere nota dell'indirizzo IP. Ad esempio, potrebbe restituire un valore simile a `PING myprinter.local (10.50.25.21)`.

4. Usare i valori del percorso della risorsa e dell'indirizzo IP. In questo esempio l'indirizzo IP è `10.50.25.21` e il percorso della risorsa è `/ipp/port1`.

## <a name="home-screen-layout"></a>Layout della schermata iniziale

Questa funzionalità si applica a:

- iOS 9.3 o versione successiva
- iPadOS 13.0 e versioni successive

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Le impostazioni si applicano a: Registrazione automatica dei dispositivi (supervisione)

> [!NOTE]
> Aggiungere un'app solo al dock, a una pagina o a una cartella in una pagina. L'aggiunta della stessa app in tutte le posizioni impedisce che l'app venga visualizzata nei dispositivi e possa visualizzare errori per la creazione dei report.
>
> Ad esempio, se si aggiunge l'app della fotocamera a un dock e a una pagina, l'app della fotocamera non viene visualizzata e la creazione di report potrebbe indicare un errore per il criterio. Per aggiungere l'app della fotocamera al layout della schermata iniziale, scegliere solo il dock o una pagina, non entrambi.

### <a name="dock"></a>Dock

Usare le impostazioni di **Dock** per aggiungere fino a sei elementi o cartelle al dock su schermo. Molti dispositivi supportano un minor numero di elementi. I dispositivi iPhone, ad esempio, supportano al massimo quattro elementi. In questo caso, nei dispositivi verranno visualizzati solo i primi quattro elementi aggiunti.

È possibile aggiungere fino a **sei** elementi (app e cartelle in combinazione) per il dock del dispositivo.

- **Aggiungi**: aggiungere app o cartelle al dock nei dispositivi.
- **Tipo**: aggiungere un'**App** o una **Cartella**:

  - **App**: scegliere questa opzione per aggiungere le app al dock nella schermata. Immettere:

    - **Nome app**: immettere un nome per l'app. Questo nome viene usato per riferimento nell'interfaccia di amministrazione di Microsoft Endpoint Manager. *Non* viene visualizzato nel dispositivo iOS/iPadOS.
    - **ID bundle dell'app**: immettere l'ID bundle dell'app. Per alcuni esempi, vedere [ID di bundle per le app iOS/iPadOS predefinite](bundle-ids-built-in-ios-apps.md).

  - **Cartella**: scegliere questa opzione per aggiungere una cartella al dock nella schermata.

    Le app aggiunte a una pagina in una cartella vengono disposte da sinistra a destra e nello stesso ordine dell'elenco. Se si aggiungono più app di quelle che può contenere una pagina, le app vengono spostate in un'altra pagina.

    - **Nome cartella**: immettere il nome della cartella. Questo nome viene visualizzato nel dispositivo degli utenti.
    - **Elenco di pagine**: selezionare **Aggiungi** per aggiungere una pagina e immettere le proprietà seguenti:

      - **Nome della pagina**: Immettere un nome per la pagina. Questo nome viene usato per riferimento nell'interfaccia di amministrazione di Microsoft Endpoint Manager. *Non* viene visualizzato nel dispositivo iOS/iPadOS.
      - **Nome app**: immettere un nome per l'app. Questo nome viene usato per riferimento nell'interfaccia di amministrazione di Microsoft Endpoint Manager. *Non* viene visualizzato nel dispositivo iOS/iPadOS.
      - **ID bundle dell'app**: immettere l'ID bundle dell'app. Per alcuni esempi, vedere [ID di bundle per le app iOS/iPadOS predefinite](bundle-ids-built-in-ios-apps.md).

      È possibile aggiungere fino a **20** pagine per il dock del dispositivo.

> [!NOTE]
> Quando si usano le impostazioni Layout della schermata iniziale per aggiungere pagine o pagine e app al dock, le icone della schermata iniziale e le pagine sono bloccate. Non possono essere spostate o eliminate. Questo comportamento può essere previsto da iOS/iPadOS e dai criteri MDM di Apple.

#### <a name="example"></a>Esempio

Nell'esempio seguente la schermata del Dock visualizza le app Safari, Mail e Borsa. L'app Mail viene selezionata per visualizzarne le proprietà:

> [!div class="mx-imgBorder"]
> ![Esempio di impostazioni del Dock del layout della schermata iniziale di iOS/iPadOS in Intune](./media/ios-device-features-settings/dock-screen-mail-app.png)

Quando si assegnano i criteri a un iPhone, il dock è simile all'immagine seguente:

> [!div class="mx-imgBorder"]
> ![Esempio di layout del dock iOS/iPadOS su iPhone](./media/ios-device-features-settings/bAgCe8F.png)

### <a name="pages"></a>.NET

Aggiungere le pagine che verranno visualizzate nella schermata iniziale e le app che verranno visualizzate in ogni pagina. Le app aggiunte a una pagina vengono disposte da sinistra a destra, nello stesso ordine dell'elenco. Se si aggiungono più app di quelle che può contenere una pagina, le app vengono spostate in un'altra pagina.

> [!TIP]
> Per riordinare gli elementi di qualsiasi schermata iniziale e qualsiasi elenco di pagine, è possibile trascinarli e rilasciarli.

È possibile aggiungere fino a **40** pagine in un dispositivo.

- **Elenco di pagine**: selezionare **Aggiungi** per aggiungere una pagina e immettere le proprietà seguenti:

  - **Nome della pagina**: Immettere un nome per la pagina. Questo nome viene usato per riferimento nell'interfaccia di amministrazione di Microsoft Endpoint Manager e *non* viene visualizzato nel dispositivo iOS/iPadOS.

  È possibile aggiungere fino a **60** elementi (app e cartelle in combinazione) in un dispositivo.

  - **Aggiungi**: aggiungere app o cartelle a una pagina nei dispositivi.

    - **Tipo**: aggiungere un'**App** o una **Cartella**:

      - **App**: scegliere questa opzione per aggiungere le app a una pagina nella schermata. Specificare anche:

        - **Nome app**: immettere un nome per l'app. Questo nome viene usato per riferimento nell'interfaccia di amministrazione di Microsoft Endpoint Manager. *Non* viene visualizzato nel dispositivo iOS/iPadOS.
        - **ID bundle dell'app**: immettere l'ID bundle dell'app. Per alcuni esempi, vedere [ID di bundle per le app iOS/iPadOS predefinite](bundle-ids-built-in-ios-apps.md).

      - **Cartella**: scegliere questa opzione per aggiungere una cartella al dock nella schermata.

        Le app aggiunte a una pagina in una cartella vengono disposte da sinistra a destra e nello stesso ordine dell'elenco. Se si aggiungono più app di quelle che può contenere una pagina, le app vengono spostate in un'altra pagina.

        - **Nome cartella**: immettere un nome per la cartella. Questo nome viene visualizzato agli utenti nei dispositivi.
        - **Aggiungi**: consente di aggiungere pagine alla cartella. Immettere anche le proprietà seguenti:

          - **Nome della pagina**: Immettere un nome per la pagina. Questo nome viene usato per riferimento nell'interfaccia di amministrazione di Microsoft Endpoint Manager. *Non* viene visualizzato nel dispositivo iOS/iPadOS.
          - **Nome app**: immettere un nome per l'app. Questo nome viene usato per riferimento nell'interfaccia di amministrazione di Microsoft Endpoint Manager. *Non* viene visualizzato nel dispositivo iOS/iPadOS.
          - **ID bundle dell'app**: immettere l'ID bundle dell'app. Per alcuni esempi, vedere [ID di bundle per le app iOS/iPadOS predefinite](bundle-ids-built-in-ios-apps.md).

#### <a name="example"></a>Esempio

Nell'esempio seguente viene aggiunta una nuova pagina denominata **Contoso**. La pagina visualizza le app Trova amici e Impostazioni:

> [!div class="mx-imgBorder"]
> ![Impostazioni della nuova pagina di layout della schermata iniziale di iOS/iPadOS ed esempio in Intune](./media/ios-device-features-settings/page-find-friends-settings-apps.png)

L'app Impostazioni viene selezionata per visualizzarne le proprietà:

> [!div class="mx-imgBorder"]
> ![Esempio delle proprietà dell'app Impostazioni per il layout della schermata iniziale di iOS/iPadOS in Intune](./media/ios-device-features-settings/page-settings-app-properties.png)

Quando si assegnano i criteri a un iPhone, la pagina è simile all'immagine seguente:

> [!div class="mx-imgBorder"]
> ![Dispositivo iOS/iPadOS con schermata iniziale modificata in Intune](./media/ios-device-features-settings/Bd37PHa.png)

## <a name="app-notifications"></a>Notifiche delle app

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Le impostazioni si applicano a: Registrazione automatica dei dispositivi (supervisione)

- **Aggiungi**: consente di aggiungere notifiche per le app:

  > [!div class="mx-imgBorder"]
  > ![Aggiungere la notifica dell'app nel profilo iOS/iPadOS in Intune](./media/ios-device-features-settings/ios-ipados-app-notifications.png)

  - **ID bundle dell'app**: immettere l'**ID bundle dell'app** che si vuole aggiungere. Per alcuni esempi, vedere [ID di bundle per le app iOS/iPadOS predefinite](bundle-ids-built-in-ios-apps.md).
  - **Nome app**: immettere il nome dell'app che si vuole aggiungere. Questo nome viene usato per riferimento nell'interfaccia di amministrazione di Microsoft Endpoint Manager. *Non* verrà visualizzato nei dispositivi.
  - **Autore**: immettere l'autore dell'app da aggiungere. Questo nome viene usato per riferimento nell'interfaccia di amministrazione di Microsoft Endpoint Manager. *Non* verrà visualizzato nei dispositivi.
  - **Notifiche**: selezionare **Abilita** o **Disabilita** per l'invio di notifiche ai dispositivi da parte dell'app.
    - **Mostra nel centro notifiche**: **Abilita** consente all'app di visualizzare notifiche nel centro notifiche del dispositivo. **Disabilita** impedisce all'app di visualizzare notifiche nel centro notifiche.
    - **Mostra nella schermata di blocco**: **Abilita** mostra le notifiche dell'app nella schermata di blocco del dispositivo. **Disabilita** impedisce all'app di visualizzare notifiche nella schermata di blocco.
    - **Tipo di avviso**: scegliere come visualizzare la notifica quando i dispositivi vengono sbloccati. Le opzioni disponibili sono:
      - **Nessuno**: non vengono visualizzate notifiche.
      - **Banner**: viene brevemente viene visualizzato un banner con la notifica.
      - **Modale**: la notifica viene visualizzata e gli utenti devono chiuderla manualmente prima di continuare a usare il dispositivo.
    - **Badge sull'icona dell'app**: selezionare **Abilita** per aggiungere un badge all'icona dell'app. Il badge indica che l'app ha inviato una notifica.
    - **Suoni**: selezionare **Abilita** per riprodurre un suono quando viene recapitata una notifica.

## <a name="lock-screen-message"></a>Messaggio della schermata di blocco

Questa funzionalità si applica a:

- iOS 9.3 e versioni successive
- iPadOS 13.0 e versioni successive

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Le impostazioni si applicano a: Registrazione automatica dei dispositivi (supervisione)

- **Informazioni sui tag asset**: immettere informazioni sul tag asset del dispositivo. Ad esempio, immettere `Owned by Contoso Corp` o `Serial Number: {{serialnumber}}`.

  Il testo immesso viene visualizzato nella finestra di accesso e nella schermata di blocco nei dispositivi.

- **Nota a piè di pagina della schermata di blocco**: immettere una nota utile per la restituzione dei dispositivi in caso di furto o smarrimento. È possibile immettere qualsiasi testo. Ad esempio, `If found, call Contoso at ...`.

  Per aggiungere informazioni specifiche del dispositivo in questi campi è anche possibile usare token di dispositivo. Ad esempio, per visualizzare il numero di serie, immettere `Serial Number: {{serialnumber}}` o `Device ID: {{DEVICEID}}`. Nella schermata di blocco il testo è simile a `Serial Number 123456789ABC`. Quando si immettono le variabili, assicurarsi di usare le parentesi graffe `{{ }}`. I [token di configurazione delle app](../apps/app-configuration-policies-use-ios.md#tokens-used-in-the-property-list) includono un elenco delle variabili che è possibile usare. È anche possibile usare `DEVICENAME` o qualsiasi altro valore specifico del dispositivo.

  > [!NOTE]
  > Le variabili non vengono convalidate nell'interfaccia utente e fanno distinzione tra maiuscole e minuscole. Di conseguenza possono essere visualizzati dei profili salvati con input non corretto. Ad esempio, se si immette `{{DeviceID}}` invece di `{{deviceid}}` o '{{DEVICEID}}', viene visualizzata la stringa letterale anziché l'ID univoco del dispositivo. Assicurarsi di immettere le informazioni corrette. Sono supportate tutte le variabili in minuscolo o maiuscolo sono supportate, ma non una combinazione delle due. 

## <a name="single-sign-on"></a>Single Sign-On

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Le impostazioni si applicano a: Registrazione del dispositivo, Registrazione automatica dei dispositivi (con supervisione)

- **Area di autenticazione**: immettere la parte del dominio dell'URL. Immettere ad esempio `contoso.com`.
- **Nome dell'entità di sicurezza Kerberos**: Intune cerca questo attributo per ogni utente in Azure AD Intune popola quindi il campo corrispondente (ad esempio UPN) prima di generare il file XML da installare nei dispositivi. Le opzioni disponibili sono:

  - **Non configurata**: Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo richiederà agli utenti un nome di entità di sicurezza Kerberos quando il profilo viene distribuito nei dispositivi. Per installare i profili SSO, è necessario un nome di entità di sicurezza per gli MDM.
  - **Nome entità utente**: Il nome di accesso UPN viene analizzato nel modo seguente:

    > [!div class="mx-imgBorder"]
    > ![Attributo SSO di nome utente iOS/iPadOS in Intune](./media/ios-device-features-settings/User-name-attribute.png)

    È anche possibile sovrascrivere l'area di autenticazione con il testo immesso nella casella di testo **Area di autenticazione**.

    Contoso, ad esempio, ha più aree, tra cui Europa, Asia e America del Nord. Contoso vuole che gli utenti in Asia usino SSO e l'app richiede l'UPN nel formato `username@asia.contoso.com`. Quando si seleziona **Nome entità utente**, l'area di autenticazione per ogni utente viene recuperata da Azure AD e corrisponde a `contoso.com`. Per gli utenti in Asia, selezionare quindi **Nome entità utente** e immettere `asia.contoso.com`. L'UPN dell'utente diventa `username@asia.contoso.com` invece di `username@contoso.com`.

  - **ID dispositivo Intune**: Intune seleziona automaticamente l'ID dispositivo di Intune.

    Per impostazione predefinita, le app devono usare solo l'ID del dispositivo. Se l'app usa l'area di autenticazione e l'ID del dispositivo, tuttavia, è possibile digitare l'area di autenticazione nella casella di testo **Area di autenticazione**.

    > [!NOTE]
    > Per impostazione predefinita, mantenere vuoto il campo dell'area di autenticazione se si usa l'ID del dispositivo.

  - **ID dispositivo di Azure AD**
  - **Nome account SAM**: Intune popola il nome dell'account di Gestione account di protezione (SAM) locale.


- **App**: **Aggiungi** consente di aggiungere app nei dispositivi degli utenti che potranno usare l'accesso Single Sign-On.

  La matrice `AppIdentifierMatches` deve includere stringhe corrispondenti agli ID dei bundle dell'app. Queste stringhe possono essere corrispondenze esatte, ad esempio `com.contoso.myapp`. In alternativa, immettere una corrispondenza di prefisso per l'ID del bundle usando il carattere jolly \*. Il carattere jolly deve essere visualizzato dopo un punto (.) e può comparire una sola volta alla fine della stringa, ad esempio `com.contoso.*`. Quando si include un carattere jolly, viene concesso all'account l'accesso a qualsiasi app il cui ID di bundle inizia con il prefisso.

  Usare **Nome app** per immettere un nome descrittivo per facilitare l'identificazione dell'ID bundle.

- **Prefissi URL**: **aggiungere** tutti gli URL all'interno dell'organizzazione che richiedono l'autenticazione Single Sign-On per gli utenti.

  Quando un utente si connette a uno di questi siti, ad esempio, il dispositivo iOS/iPadOS usa le credenziali Single Sign-On. Gli utenti non devono immettere credenziali aggiuntive. Se è abilitata l'autenticazione a più fattori, gli utenti devono immettere la seconda autenticazione.

  > [!NOTE]
  > Questi URL devono essere nomi di dominio completi formattati in modo appropriato. Apple richiede che siano nel formato `http://<yourURL.domain>`.

  I criteri di corrispondenza per gli URL devono iniziare con `http://` o `https://`. Viene eseguito un confronto di stringhe semplice e quindi il prefisso URL `http://www.contoso.com/` non corrisponde a `http://www.contoso.com:80/`. Con iOS 10.0+ e iPadOS 13.0+ è possibile immettere tutti i valori corrispondenti usando un solo carattere jolly \*. Ad esempio, `http://*.contoso.com/` corrisponde sia a `http://store.contoso.com/` che a `http://www.contoso.com`.

  I criteri `http://.com` e `https://.com` corrispondono rispettivamente a tutti gli URL HTTP e HTTPS.

- **Certificato di rinnovo**: Se si usano i certificati per l'autenticazione (non le password), selezionare il certificato SCEP o PFX esistente come certificato di autenticazione. In genere, questo certificato è lo stesso distribuito agli utenti per altri profili, ad esempio VPN, Wi-Fi o posta elettronica.

## <a name="web-content-filter"></a>Filtro contenuto Web

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Le impostazioni si applicano a: Registrazione automatica dei dispositivi (supervisione)

- **Tipo di filtro**: scegliere se consentire specifici siti Web. Le opzioni disponibili sono:

  - **Configurare gli URL**: usare il filtro Web predefinito di Apple che cerca termini per adulti, incluso un linguaggio volgare e sessualmente esplicito. Questa funzionalità valuta ogni pagina Web quando viene caricata e identifica e blocca i contenuti non appropriati. È anche possibile aggiungere gli URL che si preferisce non vengano controllati dal filtro oppure bloccare URL specifici, indipendentemente dalle impostazioni di filtro di Apple.

    - **URL autorizzati**: **aggiungere** gli URL che si vuole consentire. Questi URL ignorano il filtro Web di Apple.

        > [!NOTE]
        > Gli URL immessi sono quelli che non devono essere valutati dal filtro Web di Apple. Questi URL non sono un elenco di siti Web consentiti. Per creare un elenco di siti Web consentiti, impostare **Tipo filtro** su **Solo siti Web specifici**.

    - **URL bloccati**: **aggiungere** gli URL di cui si vuole impedire l'apertura, indipendentemente dalle impostazioni del filtro Web di Apple.

  - **Solo siti Web specifici** (solo per il Web browser Safari): questi URL vengono aggiunti ai segnalibri del browser Safari. Viene consentito agli utenti di visitare **solo** questi siti e non è possibile aprire altri siti. Usare questa opzione solo se si conosce l'elenco esatto degli URL a cui gli utenti possono accedere.

    - **URL**: immettere l'URL del sito Web che si vuole consentire. Immettere ad esempio `https://www.contoso.com`.
    - **Percorso del segnalibro**: questa impostazione è stata modificata da Apple. Tutti i segnalibri vengono inseriti nella cartella **Siti approvati**. I segnalibri non vengono inseriti nel percorso del segnalibro specificato.
    - **Titolo**: immettere un titolo descrittivo per il segnalibro.

    Se non si immettono URL, gli utenti possono accedere solo ai siti Web `microsoft.com`, `microsoft.net` e `apple.com`. Questi URL sono automaticamente consentiti da Intune.

## <a name="single-sign-on-app-extension"></a>Estensione dell'app Single Sign-On

Questa funzionalità si applica a:

- iOS 13.0 e versioni successive
- iPadOS 13.0 e versioni successive

### <a name="settings-apply-to-all-enrollment-types"></a>Le impostazioni si applicano a: Tutti i tipi di registrazione

- **Tipo di estensione dell'app per accesso Single Sign-On**: scegliere il tipo di estensione dell'app per l'accesso Single Sign-On. Le opzioni disponibili sono:

  - **Non configurata**: Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo non usa le estensioni dell'app. Per disabilitare un'estensione dell'app, è possibile impostare il tipo di estensione dell'app per l'accesso Single Sign-On su **Non configurato**.
  - **Microsoft Azure AD**: Usa il plug-in Microsoft Enterprise Single Sign-On, che è un'estensione dell'app per accesso Single Sign-On di tipo reindirizzamento. Questo plug-in offre l'accesso SSO per gli account Active Directory in tutte le applicazioni che supportano la funzionalità [Enterprise Single Sign-On di Apple](https://developer.apple.com/documentation/authenticationservices). Usare questo tipo di estensione dell'app SSO per abilitare l'accesso Single Sign-On per le app Microsoft, le app dell'organizzazione e i siti Web che eseguono l'autenticazione con Azure AD.

    Il plug-in per l'accesso Single Sign-On funge da broker di autenticazione avanzato e offre miglioramenti della sicurezza e dell'esperienza utente. Tutte le app che usavano l'app Microsoft Authenticator per l'autenticazione continuano a ottenere l'accesso Single Sign-On con il [plug-in Microsoft Enterprise Single Sign-On per i dispositivi Apple](https://docs.microsoft.com/azure/active-directory/develop/apple-sso-plugin).

    > [!IMPORTANT]
    > Per ottenere l'accesso SSO con il tipo di estensione dell'app SSO di Microsoft Azure AD, installare prima l'app Microsoft Authenticator iOS/iPadOS nei dispositivi. L'app Authenticator recapita il plug-in Microsoft Enterprise Single Sign-On ai dispositivi e le impostazioni dell'estensione dell'app SSO MDM attivano il plug-in. Quando Authenticator e il profilo dell'estensione dell'app SSO sono installati nei dispositivi, gli utenti devono immettere le credenziali per accedere e creare una sessione nei propri dispositivi. La sessione viene quindi usata su diverse applicazioni senza richiedere agli utenti di eseguire di nuovo l'autenticazione. Per altre informazioni su Authenticator, vedere l'articolo sull'[app Microsoft Authenticator](https://docs.microsoft.com/azure/active-directory/user-help/user-help-auth-app-overview).

  - **Reindirizzamento**: usare un'estensione dell'app di reindirizzamento generica e personalizzabile per usare Single Sign-On con i flussi di autenticazione moderni. Assicurarsi di conoscere l'ID estensione dell'app dell'organizzazione.
  - **Credenziali**: usare un'estensione dell'app per le credenziali personalizzabile e generica per usare Single Sign-On con i flussi di autenticazione challenge-and-response (richiesta e risposta). Assicurarsi di conoscere l'ID estensione dell'app dell'organizzazione.
  - **Kerberos**: usare l'estensione Kerberos predefinita di Apple, inclusa in iOS 13.0+ e iPadOS 13.0+. Questa opzione è una versione specifica di Kerberos dell'estensione dell'app **Credenziali**.

  > [!TIP]
  > Con i tipi **Reindirizzamento** e **Credenziali** è possibile aggiungere i propri valori di configurazione per passare l'estensione. Se si usa **Credenziali**, provare a usare le impostazioni di configurazione predefinite fornite da Apple nel tipo **Kerberos**.

- **Modalità dispositivo condiviso** (solo Microsoft Azure AD): Scegliere **Abilita** se si sta distribuendo il plug-in Microsoft Enterprise Single Sign-On in dispositivi iOS/iPadOS configurati per la funzionalità Modalità dispositivo condiviso di Azure AD. I dispositivi in modalità condivisa consentono a molti utenti di effettuare l'accesso e la disconnessione a livello globale dalle applicazioni che supportano Modalità dispositivo condiviso. Quando questa opzione è impostata su **Non configurato**, Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, i dispositivi iOS/iPadOS non sono destinati alla condivisione tra più utenti.

  Per altre informazioni sulla funzionalità Modalità dispositivo condiviso e su come abilitarla, vedere la [panoramica di Modalità dispositivo condiviso](https://docs.microsoft.com/azure/active-directory/develop/msal-shared-devices) e le informazioni sull'uso di [Modalità dispositivo condiviso per i dispositivi iOS](https://docs.microsoft.com/azure/active-directory/develop/msal-ios-shared-devices).  

  Questa funzionalità si applica a:
  
  - iOS/iPadOS 13.5 e versioni successive

- **ID estensione** (reindirizzamento e credenziali): immettere l'identificatore dell'aggregazione che identifica l'estensione dell'app per l'accesso Single Sign-On, ad esempio `com.apple.extensiblesso`.

- **ID team** (reindirizzamento e credenziali): immettere l'identificatore del team dell'estensione dell'app per l'accesso Single Sign-On. Un identificatore del team è una stringa alfanumerica (numeri e lettere) di 10 caratteri generata da Apple, ad esempio `ABCDE12345`. L'ID team non è obbligatorio.

  [Locate your Team ID](https://help.apple.com/developer-account/#/dev55c3c710c) (Individuare l'ID del team) (apre il sito Web di Apple) include ulteriori informazioni.

- **Area autenticazione** (credenziali e Kerberos): immettere il nome dell'area di autenticazione. Il nome dell'area di autenticazione deve essere in lettere maiuscole, ad esempio `CONTOSO.COM`. In genere, il nome dell'area di autenticazione corrisponde al nome di dominio DNS, ma in lettere maiuscole.

- **Domini** (credenziali e Kerberos): immettere il nome di dominio o il nome host dei siti che possono eseguire l'autenticazione tramite SSO. Ad esempio, se il sito Web è `mysite.contoso.com`, `mysite` è il nome host e `contoso.com` è il nome di dominio. Quando gli utenti si connettono a uno di questi siti, l'estensione dell'app gestisce la richiesta di autenticazione. Questa autenticazione consente agli utenti di usare Face ID, Touch ID o il pincode/passcode Apple per accedere.

  - Tutti i domini nei profili di Intune dell'estensione dell'app Single Sign-On devono essere univoci. Non è possibile ripetere un dominio in un profilo di estensione dell'app di accesso, anche se si usano tipi diversi di estensioni dell'app per l'accesso Single Sign-On.
  - Questi domini non fanno distinzione tra maiuscole e minuscole.

- **URL** (solo reindirizzamento): immettere i prefissi URL dei provider di identità per cui l'estensione dell'app di reindirizzamento usa l'accesso Single Sign-On. Quando gli utenti vengono reindirizzati a questi URL, l'estensione dell'app per l'accesso Single Sign-On interviene e richiede l'accesso Single Sign-On.

  - Tutti gli URL nei profili di estensione dell'app per l'accesso Single Sign-On di Intune devono essere univoci. Non è possibile ripetere un dominio in un profilo di estensione dell'app per l'accesso Single Sign-On, anche se si usano tipi diversi di estensioni dell'app per l'accesso Single Sign-On.
  - Gli URL devono iniziare con `http://` o `https://`.

- **Configurazione aggiuntiva** (Microsoft Azure AD, reindirizzamento e credenziali): immettere i dati aggiuntivi specifici dell'estensione da passare all'estensione dell'app per l'accesso SSO:
  - **Chiave**: immettere il nome dell'elemento che si vuole aggiungere, ad esempio `user name`.
  - **Tipo**: immettere il tipo di dati. Le opzioni disponibili sono:

    - Stringa
    - Booleano: in **Valore di configurazione** immettere `True` o `False`.
    - Integer: in **Valore di configurazione** immettere un numero.

  - **Valore**: immettere i dati.

  - **Aggiungi**: selezionare questa impostazione per aggiungere le chiavi di configurazione.

- **Utilizzo di Keychain** (solo Kerberos): **Blocca** impedisce il salvataggio e l'archiviazione delle password in Keychain. Se l'impostazione è bloccata, non viene richiesto agli utenti di salvare la password e gli utenti devono immettere nuovamente la password quando il ticket Kerberos scade. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire il salvataggio e l'archiviazione delle password in Keychain. Agli utenti non viene richiesto di immettere nuovamente la password quando il ticket scade.
- **Face ID, Touch ID o passcode** (solo Kerberos): **Richiedi** impone agli utenti di immettere Face ID, Touch ID o passcode del dispositivo quando sono necessarie le credenziali per aggiornare il ticket Kerberos. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe non richiedere agli utenti di usare la biometria o il passcode del dispositivo per aggiornare il ticket Kerberos. Se l'impostazione **Utilizzo di Keychain** è bloccata, non è applicabile.
- **Area di autenticazione predefinita** (solo Kerberos): **Abilita** imposta il valore **Area di autenticazione** immesso come area di autenticazione predefinita. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe non impostare un'area di autenticazione predefinita.

  > [!TIP]
  > - **Abilitare** questa impostazione se si stanno configurando più estensioni dell'app per l'accesso Single Sign-On Kerberos nell'organizzazione.
  > - **Abilitare** questa impostazione se si usano più aree di autenticazione. Imposta il valore **Area di autenticazione** immesso come area di autenticazione predefinita.
  > - Se si ha una sola area di autenticazione, lasciare l'impostazione **Non configurato** (impostazione predefinita).

- **Nome entità** (solo Kerberos): immettere il nome utente dell'entità Kerberos. Non è necessario includere il nome dell'area di autenticazione. Ad esempio, in `user@contoso.com` `user` è il nome dell'entità e `contoso.com` è il nome dell'area di autenticazione.

  > [!TIP]
  > - È anche possibile usare le variabili nel nome dell'entità immettendo parentesi graffe `{{ }}`. Ad esempio, per visualizzare il nome utente, immettere `Username: {{username}}`. 
  > - Prestare tuttavia attenzione alla sostituzione delle variabili poiché le variabili non vengono convalidate nell'interfaccia utente e fanno distinzione tra maiuscole e minuscole. Assicurarsi di immettere le informazioni corrette.

- **Codice del sito di Active Directory** (solo Kerberos): immettere il nome del sito Active Directory che deve essere usato dall'estensione Kerberos. Potrebbe non essere necessario modificare questo valore poiché l'estensione Kerberos potrebbe trovare automaticamente il codice del sito Active Directory.
- **Nome cache** (solo Kerberos): immettere il nome GSS (Generic Security Services) della cache Kerberos. Probabilmente non è necessario impostare questo valore.
- **ID bundle dell'app** (Microsoft Azure AD, Kerberos): immettere gli ID bundle delle app aggiuntive che dovranno accedere con Single Sign-On tramite un'estensione nei dispositivi.

  Se si usa il tipo di estensione dell'app per accesso Single Sign-On di Microsoft Azure AD, queste app usano il plug-in Microsoft Enterprise Single Sign-On per autenticare l'utente senza che sia necessario l'accesso. Gli ID bundle dell'app immessi sono autorizzati a usare l'estensione dell'app per accesso Single Sign-On di Microsoft Azure AD se non usano librerie Microsoft, ad esempio Microsoft Authentication Library (MSAL). L'esperienza per queste app potrebbe non essere uniforme rispetto alle librerie Microsoft. Le app precedenti che usano l'autenticazione MSAL o le app che non usano le librerie Microsoft più recenti devono essere aggiunte a questo elenco per funzionare correttamente con l'estensione dell'app per accesso Single Sign-On di Microsoft Azure.  

  Se si usa il tipo di estensione dell'app per accesso Single Sign-On di Kerberos, queste app hanno accesso al Ticket Granting Ticket Kerberos, il ticket di autenticazione, ed eseguono l'autenticazione degli utenti per i servizi a cui sono autorizzati ad accedere.

- **Mapping dell'area di autenticazione dei domini** (solo Kerberos): **aggiungere** i suffissi DNS di dominio che devono essere mappati all'area di autenticazione. Usare questa impostazione quando i nomi DNS degli host non corrispondono al nome dell'area di autenticazione. Probabilmente non è necessario creare questo mapping da dominio ad area di autenticazione personalizzato.
- **Certificato PKINIT** (solo Kerberos): **selezionare** il certificato PKINIT (Public Key Cryptography for Initial Authentication) che può essere usato per l'autenticazione Kerberos. È possibile scegliere tra i certificati [PKCS](../protect/certficates-pfx-configure.md) o [SCEP](../protect/certificates-scep-configure.md) aggiunti in Intune. Per altre informazioni sui certificati, vedere [Usare i certificati per l'autenticazione in Microsoft Intune](../protect/certificates-configure.md).

## <a name="wallpaper"></a>Wallpaper

Può verificarsi un comportamento imprevisto quando un profilo senza immagine viene assegnato a dispositivi con un'immagine esistente. Ad esempio, si crea un profilo senza un'immagine. Il profilo viene assegnato a dispositivi che dispongono già di un'immagine. In questo scenario è possibile che l'immagine assuma il valore predefinito del dispositivo o che l'immagine originale rimanga nel dispositivo. Questo comportamento è controllato e limitato dalla piattaforma MDM di Apple.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Le impostazioni si applicano a: Registrazione automatica dei dispositivi (supervisione)

- **Posizione di visualizzazione dello sfondo**: scegliere una posizione nei dispositivi per visualizzare l'immagine. Le opzioni disponibili sono:
  - **Non configurata**: Intune non modifica o aggiorna questa impostazione. Un'immagine personalizzata non viene aggiunta ai dispositivi. Per impostazione predefinita, il sistema operativo potrebbe impostare la propria immagine.
  - **Schermata di blocco**: aggiunge l'immagine alla schermata di blocco.
  - **Home screen** (Schermata iniziale): aggiunge l'immagine alla schermata iniziale.
  - **Schermata di blocco e schermata iniziale**: usa la stessa immagine nella schermata di blocco e nella schermata iniziale.
- **Immagine di sfondo**: caricare un'immagine PNG, JPG o JPEG esistente che si vuole usare. Assicurarsi che le dimensioni del file siano inferiori a 750 KB. È anche possibile **rimuovere** un'immagine aggiunta.

> [!TIP]
> Per visualizzare immagini diverse nella schermata di blocco e nella schermata iniziale, creare un profilo con l'immagine della schermata di blocco. Creare un altro profilo con l'immagine della schermata iniziale. Assegnare entrambi i profili ai gruppi di utenti o dispositivi iOS/iPadOS.

## <a name="next-steps"></a>Passaggi successivi

[Assegnare il profilo](device-profile-assign.md) e [monitorarne lo stato](device-profile-monitor.md).

È anche possibile creare profili di funzionalità dei dispositivi per i dispositivi [macOS](macos-device-features-settings.md).
