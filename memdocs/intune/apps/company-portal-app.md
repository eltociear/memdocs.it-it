---
title: Come configurare l'app Portale aziendale
titleSuffix: Microsoft Intune
description: Informazioni su come applicare specifiche personalizzazioni aziendali all'app Portale aziendale Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/24/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: dec6f258-ee1b-4824-bf66-29053051a1ae
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 36d26eb7f644731082407e816358b74c515333cb
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79340164"
---
# <a name="how-to-configure-the-microsoft-intune-company-portal-app"></a>Come configurare l'app Portale aziendale di Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Il portale aziendale di Microsoft Intune è il punto in cui gli utenti possono accedere ai dati aziendali ed eseguire attività comuni quali la registrazione dei dispositivi, l'installazione di app e la ricerca delle informazioni di assistenza del reparto IT. Dall'app Portale aziendale l'utente può anche accedere in modo sicuro alle risorse aziendali. L'app Portale aziendale è costituita da diverse pagine, ad esempio Pagina iniziale, App, Dettagli app, Dispositivi e Dettagli dispositivo. Per trovare rapidamente le app all'interno del Portale aziendale, è possibile filtrare le app nella pagina App.

> [!IMPORTANT]
> Per supportare Firebase Cloud Messaging (FCM) di Google, è necessario aggiornare l'app Portale aziendale per Android alla versione più recente.  

> [!Tip]
> Quando si personalizza il portale aziendale, le configurazioni vengono applicate sia al sito Web che alle app Portale aziendale. Si noti che gli utenti devono avere una licenza di Intune assegnata per accedere al sito Web del portale aziendale.

Con la personalizzazione del Portale aziendale si offrirà agli utenti finali un'esperienza familiare e utile. A questo scopo, passare all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), selezionare **Amministrazione del tenant** > **Personalizzazione** e quindi configurare le impostazioni necessarie.

Quando si installa un'applicazione iOS/iPadOS dal Portale aziendale, viene inviata una richiesta. Ciò avviene quando l'app iOS/iPadOS è collegata all'App Store, a un programma Volume Purchase Program (VPP) oppure a un'app line-of-business. La richiesta consente agli utenti di accettare l'azione o consentire la gestione dell'app. Nella richiesta sarà visualizzato il nome della società o, quando il nome della società non è disponibile, sarà visualizzato **Portale aziendale**. 

> [!Note]
> Se si usa Azure per enti pubblici, l'utente finale riceve i log delle app per prendere decisioni in merito alla condivisione quando avvia il processo per visualizzare la Guida per un problema. Se tuttavia non si usa Azure per enti pubblici, il portale aziendale per Windows 10 invierà i log delle app direttamente a Microsoft quando l'utente avvia il processo per visualizzare la Guida per un problema. Inviando i log delle app a Microsoft sarà più semplice risolvere i problemi. 

## <a name="company-information-and-privacy-statement"></a>Informazioni e informativa sulla privacy della società
Il nome dell'azienda viene visualizzato come titolo del portale aziendale. L'informativa sulla privacy viene visualizzata quando un utente fa clic sul relativo collegamento.

| Nome del campo | Lunghezza massima | Altre informazioni |
|---|---|---|
|**Nome società**| 40 | Questo nome viene visualizzato come titolo del portale aziendale e appare come testo nell'intera esperienza utente Intune. |
| **URL dell'informativa sulla privacy** |     79     | È possibile indicare l'informativa sulla privacy della propria azienda che verrà visualizzata quando gli utenti fanno clic sui collegamenti relativi alla privacy dal portale aziendale. Immettere un URL valido nel formato `<https://www.contoso.com>`. |

> [!NOTE]
> In conformità con i criteri Microsoft e Apple, non si vendono per alcun motivo a terze parti i dati raccolti dal servizio.

## <a name="support-information"></a>Informazioni di supporto
Immettere le informazioni di supporto della società, in modo da garantire al dipendente un contatto per le domande relative a Intune.

|Nome del campo|Lunghezza massima|Altre informazioni|
|---|---|---|
|**Nome di contatto** | 40 | Questo nome viene visualizzato nella pagina **Guida e supporto tecnico**. |
|**Numero di telefono** | 20 | Questo numero di contatto viene visualizzato nella pagina **Guida e supporto tecnico** che consente ai dipendenti di contattare l'organizzazione per ottenere supporto. |
|**Indirizzo di posta elettronica**| 40 | Questo indirizzo di contatto viene visualizzato nella pagina **Guida e supporto tecnico**. È necessario immettere un indirizzo di posta elettronica valido nel formato `alias@domainname.com`. |
|**Nome del sito Web**| 40 | Questo è il nome descrittivo visualizzato per l'URL del sito Web del supporto tecnico. Se si specifica l'URL del sito Web senza un nome descrittivo, nella pagina **Guida e supporto tecnico** del Portale aziendale verrà visualizzato Vai al sito Web IT. |
|**URL del sito Web**| 150 | Se si dispone di un sito Web di supporto che si desidera venga usato dagli utenti, è necessario specificare qui l'URL. Il formato dell'URL deve essere `https://www.contoso.com`. Se non si specifica un URL, nella pagina **Guida e supporto tecnico** di Portale aziendale non verranno visualizzate informazioni sul sito Web del supporto tecnico. |
| **Informazioni aggiuntive**| 120 | Vengono visualizzate nella pagina **Guida e supporto tecnico**. |


## <a name="company-identity-branding-customization"></a>Personalizzazione del branding dell'identità aziendale
È possibile personalizzare il portale aziendale con logo, nome dell'azienda, colore del tema e sfondo.

### <a name="theme-color-and-logo-in-the-company-portal"></a>Colore del tema e logo nel portale aziendale
È possibile applicare un colore del tema al portale aziendale. Selezionare un colore standard o immettere un codice esadecimale a sei cifre corrispondente a un colore personalizzato.

|Nome del campo|Altre informazioni|
|---|---|
|**Select a standard color or enter a six-digit hex code** (Selezionare un colore standard o immettere un codice esadecimale a sei cifre)| Scegliere **Standard** per selezionare visivamente un colore. Scegliere **Personalizzato** per selezionare un colore specifico in base a un valore in formato esadecimale.|
|**Choose theme color** (Scegliere il colore del tema)| Selezionare un colore del tema da applicare al portale aziendale. È possibile scegliere un colore standard o immettere un codice esadecimale specifico. |
|**Display** (Schermo)| Specificare se visualizzare il **logo e il nome della società**, **solo il logo della società** o solo il **nome della società**. |
|**Upload your company logo** (Carica il logo della società)|È possibile caricare il logo della società da visualizzare nel portale aziendale. Si noti che il colore del testo viene selezionato automaticamente per offrire il massimo livello di contrasto. Per assicurare un aspetto ottimale, caricare un logo con uno sfondo trasparente.<p><ul><li>Dimensioni massime dell'immagine: 400x400 px</li><li>Dimensioni massime del file: 750 kB</li><li>Tipo di file: PNG, JPG o JPEG</li></ul>|

Dopo aver caricato il logo, l'area di anteprima visualizza il logo con il colore del tema. Se si sceglie di visualizzare il nome della società, il nome verrà visualizzato in nero o in bianco nel portale aziendale in modo da offrire il massimo livello di contrasto in base al colore del tema. L'area di anteprima nella schermata non visualizzerà il nome della società. 

### <a name="logo-to-use-on-white-or-light-backgrounds"></a>Logo da usare su sfondi bianchi o chiari
Scegliere un logo adatto a sfondi bianchi o chiari.

|Nome del campo|Altre informazioni|
|---|---|
|**Upload your logo** (Carica il logo)| Questa opzione è disponibile se si è scelto di visualizzare il logo della società. Per assicurare un aspetto ottimale, caricare un logo con uno sfondo trasparente.<p><ul><li>Dimensioni massime dell'immagine: 400x400 px</li><li>Dimensioni massime del file: 750 kB</li><li>Tipo di file: PNG, JPG o JPEG</li></ul>|

### <a name="brand-image-for-company-portal"></a>Immagine del marchio per il portale aziendale

Visualizzare un'immagine del marchio che rifletta il marchio della società. Dopo aver salvato le modifiche è possibile scegliere **Visualizzare l'anteprima delle impostazioni nel portale Web di Intune** nella parte superiore del riquadro per verificare come vengono visualizzate le configurazioni. Si noti che l'immagine del marchio può essere visualizzata in anteprima solo in un dispositivo iOS/iPadOS e non nel portale Web di Intune. 

|Nome del campo|Altre informazioni|
|---|---|
|**Upload your brand image** (Caricare immagine del marchio)| Questa opzione consente di visualizzare un'immagine del marchio. Nell'app Portale aziendale iOS/iPadOS viene visualizzata come immagine di sfondo nella pagina del profilo dell'utente.<p><ul><li>Larghezza dell'immagine consigliata: Maggiore di 1125px (deve essere almeno 650 px)</li><li>Dimensioni massime dell'immagine: 1,3 MB</li><li>Tipo di file: PNG, JPG o JPEG</li></ul>|

L'immagine del marchio può migliorare la fiducia dell'utente nel portale aziendale presentando un forte senso di marchio della società. Di seguito sono riportati alcuni suggerimenti che è possibile prendere in considerazione per l'acquisizione, la scelta e l'ottimizzazione dell'immagine per il portale aziendale. 

- Rivolgersi al reparto marketing o pubblicità. È possibile che il reparto abbia già a disposizione un set di immagini del marchio approvate. Il reparto può anche aiutare l'utente ad adattare le immagini alle esigenze specifiche. 

- Prendere in considerazione sia la composizione verticale che quella orizzontale. L'immagine deve avere uno sfondo sufficiente che circonda il punto focale. L'immagine può essere ritagliata in diversi modi in base alle dimensioni del dispositivo, all'orientamento e alla piattaforma. 

- Evitare di usare un'immagine generica. L'immagine deve riflettere il marchio della società ed essere familiare agli utenti. Se non è disponibile alcuna immagine, è preferibile non usare un'immagine generica che non ha alcun significato per l'utente. 

- Rimuovere i metadati non necessari. Il file di immagine può includere i metadati, ad esempio il profilo della fotocamera, la posizione geografica, il titolo, il sottotitolo e così via. Usare uno strumento di ottimizzazione delle immagini per rimuovere queste informazioni per mantenere la qualità e rispettare il limite di dimensione del file. 

Dopo l'aggiunta o la modifica di un'immagine del marchio in Intune, l'utente finale potrebbe non vedere la modifica nei dispositivi iOS/iPadOS fino a quando il portale aziendale non riconosce la modifica all'avvio e viene quindi riavviato per visualizzare l'immagine del marchio. 

### <a name="brand-image-examples"></a>Esempi di immagini di marchio

L'immagine seguente mostra un esempio di immagine del marchio per iPad:

![Screenshot dell'immagine del marchio per iPad di esempio](./media/company-portal-app/company-portal-app-03.png)

L'immagine seguente mostra un esempio di immagine del marchio iPhone:

![Screenshot dell'immagine del marchio per iPhone di esempio](./media/company-portal-app/company-portal-app-02.png)

## <a name="privacy-statement-customization"></a>Personalizzazione dell'informativa sulla privacy

È possibile personalizzare l'informativa sulla privacy visualizzata per l'organizzazione nei dispositivi iOS/iPadOS gestiti. Questo messaggio elenca gli elementi che l'organizzazione non può visualizzare o eseguire nei dispositivi iOS/iPadOS gestiti.

In **Personalizzazione del Portale aziendale** > **Messaggio sulla gestione dei dispositivi e sulla privacy**, è possibile:

- Accettare **Predefinito** per usare l'elenco come illustrato, oppure
- Scegliere **Personalizzato** per personalizzare gli elementi che l'organizzazione non può visualizzare o eseguire nei dispositivi iOS/iPadOS gestiti. È possibile usare [Markdown](https://daringfireball.net/projects/markdown/) per aggiungere punti elenco, grassetto, corsivo e collegamenti.

## <a name="company-portal-derived-credentials-for-ios-devices"></a>Credenziali derivate del portale aziendale per i dispositivi iOS

Intune supporta la verifica dell'identità personale (PIV, Personal Identity Verification) e le credenziali derivate CAC (Common Access Card) in collaborazione con i provider di credenziali DISA Purebred, Entrust Datacard e Intercede. Gli utenti finali eseguiranno ulteriori passaggi dopo la registrazione del dispositivo iOS/iPadOS per verificarne l'identità nell'applicazione Portale aziendale. Le credenziali derivate verranno abilitate per gli utenti impostando prima di tutto un provider di credenziali per il tenant, quindi specificando come destinazione un profilo che usa credenziali derivate per utenti o dispositivi.

> [!NOTE]
> L'utente visualizzerà le istruzioni sulle credenziali derivate in base al collegamento specificato tramite Intune.

Per altre informazioni sulle credenziali derivate per i dispositivi iOS/iPadOS, vedere [Usare le credenziali derivate in Microsoft Intune](../protect/derived-credentials.md).

## <a name="dark-mode-for-ios-company-portal"></a>Modalità scura per il portale aziendale iOS

La modalità scura è disponibile per il portale aziendale iOS. Gli utenti possono scaricare le app aziendali, gestire i propri dispositivi e ottenere supporto tecnico nella combinazione di colori scelta in base alle impostazioni del dispositivo. Il portale aziendale iOS adatterà automaticamente le impostazioni del dispositivo dell'utente finale per la modalità scura o chiara.

## <a name="windows-company-portal-keyboard-shortcuts"></a>Tasti di scelta rapida per il portale aziendale di Windows

Gli utenti finali possono usare tasti di scelta rapida per eseguire azioni di spostamento, sulle app e sui dispositivi nel portale aziendale di Windows.

I tasti di scelta rapida seguenti sono disponibili nell'app Portale aziendale di Windows.

| Area | Descrizione | Tasti di scelta rapida |
|:------------------:|:--------------:|:-----------------:|
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

![Screenshot dei tasti di scelta rapida disponibili nell'app Portale aziendale di Windows](./media/company-portal-app/company-portal-app-01.png)

## <a name="user-self-service-device-actions-from-the-company-portal"></a>Azioni self-service che l'utente può eseguire nel dispositivo dal Portale aziendale

Gli utenti possono eseguire azioni nei dispositivi locali o remoti tramite l'app Portale aziendale o il sito Web. Le azioni che un utente può eseguire variano in base alla configurazione e alla piattaforma del dispositivo. In tutti i casi, le azioni sui dispositivi remoti possono essere eseguite solo dall'utente primario del dispositivo.
- **Ritiro**: rimuove il dispositivo dalla Gestione di Intune. Nell'app Portale aziendale e nel sito Web questa azione viene visualizzata come **Rimuovi**.
- **Cancellazione**: questa azione avvia la reimpostazione del dispositivo. Nel sito Web del Portale aziendale viene visualizzato come **Ripristina** o **Ripristino delle impostazioni predefinite** nell'app Portale aziendale per iOS.
- **Ridenominazione**: questa azione modifica il nome del dispositivo che l'utente può visualizzare nel Portale aziendale. Non modifica il nome del dispositivo locale, ma solo l'elenco nel Portale aziendale.
- **Sincronizzazione**: questa azione avvia la sincronizzazione del dispositivo con il servizio Intune. Viene visualizzato come **Verifica stato** nel Portale aziendale.
- **Blocco remoto**: blocca il dispositivo e richiede un PIN per poterlo sbloccare.
- **Reimpostazione passcode**: questa azione reimposta il passcode del dispositivo. Nei dispositivi iOS/iPadOS il passcode verrà rimosso e l'utente finale dovrà immettere un nuovo codice nelle impostazioni. Nei dispositivi Android supportati Intune genera un nuovo passcode che viene temporaneamente visualizzato nel Portale aziendale.
- **Recupero chiave**: questa azione recupera una chiave di ripristino personale per i dispositivi macOS crittografati dal sito Web del Portale aziendale. 

### <a name="self-service-actions"></a>Azioni self-service

Alcune piattaforme e configurazioni non consentono azioni self-service nel dispositivo. La tabella seguente contiene altri dettagli sulle azioni self-service:

|  | Windows 10<sup>(3)</sup> | iOS/iPadOS<sup>(3)</sup> | MacOS<sup>(3)</sup> | Android<sup>(3)</sup> |
|----------------------|--------------------------|-------------------|-----------------------------------|-------------------------|
| Ritiro | Disponibile<sup>(1)</sup> | Disponibile | Disponibile | Disponibile<sup>(7)</sup> |
| Cancellazione | Disponibile | Disponibile<sup>(5)</sup> | N/D | Disponibile<sup>(7)</sup> |
| Ridenominazione<sup>(4)</sup> | Disponibile | Disponibile | Disponibile | Disponibile |
| Sincronizza | Disponibile | Disponibile | Disponibile | Disponibile |
| Blocco remoto | Solo per Windows Phone | Disponibile | Disponibile | Disponibile |
| Reimpostazione passcode | Solo per Windows Phone | Disponibile<sup>(8)</sup> | N/D | Disponibile<sup>(6)</sup> |
| Recupero chiavi | N/D | N/D | Disponibile<sup>(2)</sup> | N/D |

<sup>(1)</sup> Il **ritiro** è sempre bloccato nei dispositivi Windows aggiunti ad Azure AD.<br>
<sup>(2)</sup> Il **recupero chiavi** per MacOS è disponibile solo tramite il portale Web.<br>
<sup>(3) </sup> tutte le azioni remote sono disabilitate se si usa la registrazione di un manager di registrazione dispositivi.<br>
<sup>(4)</sup> La **ridenominazione** modifica solo il nome del dispositivo nell'app Portale aziendale o nel portale Web, non nel dispositivo.<br>
<sup>(5)</sup> La **cancellazione** non è disponibile nei dispositivi iOS registrati dall'utente.<br>
<sup>(6)</sup> La **reimpostazione del passcode** non è supportata in alcune configurazioni di Android e Android Enterprise. Per altre informazioni, vedere [Reimpostare o rimuovere il passcode di un dispositivo in Intune](../remote-actions/device-passcode-reset.md).<br>
<sup>(7)</sup> Il **ritiro** e la **cancellazione** non sono disponibili in scenari di proprietari di dispositivi Android Enterprise (COPE, COBO, COSU).<br> 
<sup>(8)</sup> La **reimpostazione del passcode** non è supportata nei dispositivi iOS registrati dall'utente.

## <a name="next-steps"></a>Passaggi successivi

- [Aggiungere manualmente l'app Portale aziendale di Windows 10 usando Microsoft Intune](company-portal-app.md)
