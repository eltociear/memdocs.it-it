---
title: Impostazioni delle funzionalità dei dispositivi macOS in Microsoft Intune - Azure | Microsoft Docs
description: Visualizzare le impostazioni per configurare i dispositivi macOS per AirPrint e personalizzare la finestra di accesso per visualizzare o nascondere pulsanti di alimentazione in Microsoft Intune. Vedere i passaggi per ottenere l'indirizzo IP, il percorso e le impostazioni della porta di un server AirPrint nella rete. Usare queste impostazioni in un profilo di configurazione del dispositivo per configurare le funzionalità dei dispositivi macOS.
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
ms.reviewer: kakyker; annovich
ms.suite: ems
search.appverid: ''
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 79c389767ad3cb796e2cc7b4cd9a35015e17a837
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/25/2020
ms.locfileid: "88819661"
---
# <a name="macos-device-feature-settings-in-intune"></a>Impostazioni relative alle funzionalità dei dispositivi macOS in Intune

Intune include alcune impostazioni predefinite per personalizzare le funzionalità nei dispositivi macOS. Ad esempio, gli amministratori possono aggiungere stampanti AirPrint, scegliere la modalità di accesso degli utenti, configurare i controlli di risparmio energia, usare l'autenticazione Single Sign-On e altro ancora.

Usare queste funzionalità per controllare i dispositivi macOS nella soluzione di gestione di dispositivi mobili (MDM).

L'articolo elenca queste impostazioni e descrive la funzione di ogni impostazione. Vengono inoltre elencati i passaggi per ottenere l'indirizzo IP, il percorso e la porta delle stampanti AirPrint tramite l'app Terminale (emulatore). Per altre informazioni sulle funzionalità del dispositivo, vedere [Aggiungere impostazioni relative alle funzionalità dei dispositivi iOS/iPadOS e macOS](device-features-configure.md).

> [!NOTE]
> L'interfaccia utente potrebbe non corrispondere ai tipi di iscrizione indicati in questo articolo. Le informazioni contenute in questo articolo sono corrette. L'interfaccia utente verrà aggiornata in una versione futura.

## <a name="before-you-begin"></a>Prima di iniziare

[Creare un profilo delle funzionalità del dispositivo macOS](device-features-configure.md).

> [!NOTE]
> Queste impostazioni si applicano a diversi tipi di registrazione, con alcune impostazioni che si applicano a tutte le opzioni di registrazione. Per altre informazioni sui diversi tipi di registrazione, vedere [Registrazione di macOS](../enrollment/macos-enroll.md).

## <a name="airprint"></a>AirPrint

### <a name="settings-apply-to-all-enrollment-types"></a>Le impostazioni si applicano a: Tutti i tipi di registrazione

- **Destinazioni di AirPrint**: **Aggiungere** una o più stampanti AirPrint che gli utenti possono usare dai dispositivi. Specificare anche:
  - **Porta** (iOS 11.0+, iPadOS 13.0+): immettere la porta di ascolto della destinazione AirPrint. Se si omette questa proprietà, AirPrint usa la porta predefinita.
  - **Indirizzo IP**: immettere l'indirizzo IPv4 o IPv6 della stampante. Immettere ad esempio `10.0.0.1`. Se si usano i nomi host per identificare le stampanti, è possibile ottenere l'indirizzo IP effettuando il ping della stampante nell'app Terminale. Per informazioni più dettagliate, vedere [Ottenere l'indirizzo IP e il percorso](#get-the-ip-address-and-path) (in questo articolo).
  - **Percorso**: immettere il percorso della stampante. il percorso è in genere `ipp/print` per le stampanti di rete. Per informazioni più dettagliate, vedere [Ottenere l'indirizzo IP e il percorso](#get-the-ip-address-and-path) (in questo articolo).
  - **TLS** (iOS 11.0+, iPadOS 13.0+): Le opzioni disponibili sono:
    - **No** (impostazione predefinita): Transport Layer Security (TLS) non viene applicato quando ci si connette alle stampanti AirPrint.
    - **Sì**: protegge le connessioni AirPrint con Transport Layer Security (TLS).

- **Importare** un file delimitato da virgole (CSV) che include un elenco delle stampanti AirPrint. Dopo aver aggiunto le stampanti AirPrint in Intune, è anche possibile **esportare** questo elenco.

### <a name="get-the-ip-address-and-path"></a>Ottenere l'indirizzo IP e il percorso

Per aggiungere i server AirPrinter, sono necessari l'indirizzo IP della stampante, il percorso della risorsa e la porta. La procedura seguente mostra come ottenere queste informazioni.

1. In un dispositivo Mac connesso alla stessa rete locale (subnet) delle stampanti AirPrint aprire **Terminale** (da **/Applicazioni/Utilità**).
2. Nell'app Terminale digitare `ippfind` e premere INVIO.

    Prendere nota delle informazioni della stampante. Ad esempio, potrebbe restituire un valore simile a `ipp://myprinter.local.:631/ipp/port1`. La prima parte è il nome della stampante. L'ultima parte (`ipp/port1`) è il percorso della risorsa.

3. Nel Terminale digitare `ping myprinter.local` e premere INVIO.

   Prendere nota dell'indirizzo IP. Ad esempio, potrebbe restituire un valore simile a `PING myprinter.local (10.50.25.21)`.

4. Usare i valori del percorso della risorsa e dell'indirizzo IP. In questo esempio l'indirizzo IP è `10.50.25.21` e il percorso della risorsa è `/ipp/port1`.

## <a name="associated-domains"></a>Domini associati

Con Intune, è possibile:

- Aggiungere molte associazioni da app a dominio.
- Associare molti domini alla stessa app.

Questa funzionalità si applica a:

- macOS 10.15 e versioni successive

### <a name="settings-apply-to-user-approved-device-enrollment-and-automated-device-enrollment"></a>Le impostazioni si applicano a: Registrazione dei dispositivi approvata dall'utente e registrazione automatica dei dispositivi

- **Domini associati**: **Aggiungere** un'associazione tra il dominio e un'app. Questa funzionalità condivide le credenziali di accesso tra un'app Contoso e un sito Web Contoso. Specificare anche:

  - **ID app**: immettere l'identificatore dell'app da associare a un sito Web. L'identificatore dell'app include l'ID team e un ID bundle: `TeamID.BundleID`.

    L'ID team è una stringa alfanumerica (lettere e numeri) di 10 caratteri generata da Apple per gli sviluppatori di app, ad esempio `ABCDE12345`. [Locate your Team ID](https://help.apple.com/developer-account/#/dev55c3c710c) (Individuare l'ID team) (apre il sito Web di Apple) include ulteriori informazioni.

    L'ID bundle identifica in modo univoco l'app ed è in genere formattato in notazione del nome di dominio inverso. Ad esempio, l'ID bundle di Finder è `com.apple.finder`. Per trovare l'ID bundle, usare AppleScript nel terminale:

    `osascript -e 'id of app "ExampleApp"'`

  - **Dominio**: immettere il dominio del sito Web da associare a un'app. Il dominio include un tipo di servizio e un nome host completo, ad esempio `webcredentials:www.contoso.com`.

    È possibile cercare tutti i sottodomini di un dominio associato immettendo `*.` (un carattere jolly asterisco e un punto) prima dell'inizio del dominio. Il punto è obbligatorio. I domini esatti hanno una priorità più alta rispetto ai domini con caratteri jolly. Di conseguenza, i modelli dei domini padre vengono individuati *se* non viene trovata una corrispondenza nel sottodominio completo.

    Il tipo di servizio può essere:

    - **authsrv**: Estensione dell'app Single Sign-On
    - **applink**: collegamento universale
    - **webcredentials**: riempimento automatico delle password

> [!TIP]
> Per risolvere i problemi, nel dispositivo macOS aprire **Preferenze di sistema** > **Profili**. Verificare che il profilo creato sia presente nell'elenco profili del dispositivo. Se il profilo è incluso, assicurarsi che la **configurazione dei domini associati** si trovi nel profilo e includa i domini e l'ID app corretti.

## <a name="content-caching"></a>Memorizzazione del contenuto nella cache

La memorizzazione del contenuto nella cache salva una copia locale del contenuto. Queste informazioni possono essere recuperate da altri dispositivi Apple senza connessione a Internet. Questa operazione di memorizzazione nella cache accelera i download salvando gli aggiornamenti software, le app, le foto e altro contenuto al primo download. Dato che le app vengono scaricate una sola volta e condivise con altri dispositivi, gli istituti di istruzione e le organizzazioni con molti dispositivi risparmiano larghezza di banda.

> [!NOTE]
> Usare un solo profilo per queste impostazioni. Se si assegnano più profili con queste impostazioni, si verificherà un errore.
>
> Per altre informazioni sul monitoraggio della memorizzazione del contenuto nella cache, vedere [Visualizzare i log e le statistiche della cache dei contenuti](https://support.apple.com/guide/mac-help/view-content-caching-logs-statistics-mac-mchl0d8533cd/10.15/mac/10.15) (apre il sito Web di Apple).

Questa funzionalità si applica a:

- macOS 10.13.4 e versioni successive

### <a name="settings-apply-to-all-enrollment-types"></a>Le impostazioni si applicano a: Tutti i tipi di registrazione

Per altre informazioni su queste impostazioni, vedere [Impostazioni del payload "Cache dei contenuti"](https://support.apple.com/guide/mdm/content-caching-mdm163612d39/1/web/1) (apre il sito Web di Apple).

**Abilita la memorizzazione di contenuti nella cache**: **Sì** attiva la memorizzazione del contenuto nella cache e gli utenti non possono disabilitarla. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe disattivarla.

- **Tipo di contenuto da memorizzare nella cache**: Le opzioni disponibili sono:
  - **Tutto il contenuto**: memorizza nella cache il contenuto di iCloud e il contenuto condiviso.
  - **Solo contenuti utente**: memorizza nella cache il contenuto di iCloud dell'utente, incluse foto e documenti.
  - **Solo contenuti condivisi**: memorizza nella cache le app e gli aggiornamenti software.

- **Dimensioni massime della cache**: immettere la quantità massima di spazio su disco (in byte) usata per memorizzare il contenuto nella cache. Quando il campo è vuoto (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe impostare questo valore su zero (`0`) byte, corrispondente a spazio su disco illimitato per la cache.

  Assicurarsi di non superare lo spazio disponibile nei dispositivi. Per altre informazioni sulla capacità di archiviazione del dispositivo, vedere [Indicazione della capacità di archiviazione in iOS e macOS](https://support.apple.com/HT201402) (apre il sito Web di Apple).

- **Percorso cache**: immettere il percorso in cui archiviare il contenuto memorizzato nella cache. Il percorso predefinito è `/Library/Application Support/Apple/AssetCache/Data`. Si consiglia di non modificare questo percorso.

  Se si modifica questa impostazione, il contenuto memorizzato nella cache non viene spostato nella nuova posizione. Per spostarlo automaticamente, è necessario che gli utenti modifichino il percorso nel dispositivo (**Preferenze di Sistema** > **Condivisione** > **Cache dei contenuti**).

- **Porta**: Immettere il numero di porta TCP (da 0 a 65535) nei dispositivi in modo che la cache accetti le richieste di download e caricamento. Immettere zero (`0`) (impostazione predefinita) per usare qualsiasi porta disponibile.
- **Blocca la condivisione della connessione Internet e del contenuto memorizzato nella cache**: noto anche come memorizzazione nella cache con tethering. **Sì** impedisce la condivisione della connessione Internet e impedisce la condivisione del contenuto memorizzato nella cache con dispositivi iOS/iPadOS connessi tramite USB al Mac. Gli utenti non possono abilitare questa funzionalità. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.

- **Abilita la condivisione della connessione Internet**: noto anche come memorizzazione nella cache con tethering. **Sì** consente la condivisione della connessione Internet e consente la condivisione del contenuto memorizzato nella cache con i dispositivi iOS/iPadOS connessi tramite USB al Mac. Gli utenti non possono disabilitare questa funzionalità. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe disattivarla.

  Questa funzionalità si applica a:

  - macOS 10.15.4 e versioni successive

- **Consenti alla cache di registrare i dettagli del client**: **Sì** registra l'indirizzo IP e il numero di porta dei dispositivi che richiedono il contenuto. Per risolvere i problemi relativi ai dispositivi, questo file di log può essere utile. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe non registrare queste informazioni.

- **Mantieni sempre il contenuto dalla cache, anche quando il sistema necessita di spazio su disco per altre app**: **Sì** mantiene il contenuto della cache e verifica che non vengano eliminati elementi, anche quando lo spazio su disco è insufficiente. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe eliminare automaticamente il contenuto dalla cache quando è necessario spazio di archiviazione per altre app.

  Questa funzionalità si applica a:

  - macOS 10.15 e versioni successive

- **Mostra gli avvisi sullo stato**: con l'impostazione **Sì** gli avvisi vengono visualizzati come notifiche di sistema. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe non visualizzare questi avvisi come notifiche di sistema.

  Questa funzionalità si applica a:

  - macOS 10.15 e versioni successive

- **Impedisci la sospensione del dispositivo quando la memorizzazione nella cache è attivata**: **Sì** impedisce al computer di passare in sospensione quando la memorizzazione nella cache è attiva. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire la sospensione del dispositivo.

  Questa funzionalità si applica a:

  - macOS 10.15 e versioni successive

- **Dispositivi da memorizzare nella cache**: scegliere i dispositivi che possono memorizzare il contenuto nella cache. Le opzioni disponibili sono:
  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione. 
  - **Dispositivi che usano la stessa rete locale**: la cache del contenuto offre il contenuto ai dispositivi nella stessa rete locale immediata. Nessun contenuto viene offerto ai dispositivi su altre reti, inclusi i dispositivi raggiungibili dalla cache del contenuto.
  - **Dispositivi che usano lo stesso indirizzo IP pubblico**: la cache del contenuto offre il contenuto ai dispositivi che usano lo stesso indirizzo IP pubblico. Nessun contenuto viene offerto ai dispositivi su altre reti, inclusi i dispositivi raggiungibili dalla cache del contenuto.
  - **Dispositivi che usano reti locali personalizzate**: la cache del contenuto fornisce il contenuto ai dispositivi negli intervalli IP immessi.
    - **Intervalli di ascolto client**: immettere l'intervallo di indirizzi IP che può ricevere la cache del contenuto.
  - **Dispositivi che usano reti locali personalizzate con fallback**: la cache del contenuto fornisce il contenuto ai dispositivi negli intervalli di ascolto, negli intervalli di ascolto peer e negli indirizzi IP padre.
    - **Intervalli di ascolto client**: immettere l'intervallo di indirizzi IP che può ricevere la cache del contenuto.

- **Indirizzi IP pubblici personalizzati**: immettere un intervallo di indirizzi IP pubblici. I server cloud usano questo intervallo per abbinare i dispositivi client alle cache.

- **Condividi contenuti con altre cache**: quando la rete ha più di una cache di contenuto, le cache di contenuto in altri dispositivi diventano automaticamente peer. Questi dispositivi possono consultare e condividere il software memorizzato nella cache. 

  Quando un elemento richiesto non è disponibile in una cache del contenuto, viene cercato nei relativi peer. Se l'elemento è disponibile, viene scaricato dalla cache del contenuto nel dispositivo peer. Se non è ancora disponibile, la cache del contenuto scarica l'elemento da:

  - Un indirizzo IP padre, se ne è stato configurato uno
  
    OPPURE,
    
  - Da Apple tramite Internet

  Quando è disponibile più di una cache di contenuto, i dispositivi selezionano automaticamente la cache di contenuto corretta. 

  Le opzioni disponibili sono:

  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione.
  - **Cache di contenuti che usano la stessa rete locale**: la cache di contenuto è in peer solo con altre cache di contenuto nella stessa rete locale immediata.
  - **Cache di contenuti con lo stesso indirizzo IP pubblico**: la cache di contenuto è in peer solo con altre cache di contenuto sullo stesso indirizzo IP pubblico.
  - **Memorizzazioni di contenuti nella cache che usano reti locali personalizzate**: la cache di contenuto è in peer solo con altre cache di contenuto nell'intervallo di ascolto degli indirizzi IP immesso:

    - **Intervalli di ascolto peer**: immettere gli indirizzi IP iniziale finale IPv4 o IPv6 per l'intervallo. La cache di contenuto risponde solo alle richieste di cache peer dalle cache di contenuto negli intervalli di indirizzi IP immessi.
    - **Intervalli di filtro peer**: immettere gli indirizzi IP iniziale finale IPv4 o IPv6 per l'intervallo. La cache del contenuto filtra l'elenco di peer usando gli intervalli di indirizzi IP immessi.

- **Indirizzi IP padre**: immettere l'indirizzo IP locale di un'altra cache di contenuto da aggiungere come cache padre. La cache carica e scarica il contenuto in queste cache, anziché caricare o scaricare direttamente con Apple. Aggiungere solo un indirizzo IP padre una volta.
- **Criterio di selezione padre**: quando sono presenti molte cache padre, selezionare il modo in cui viene scelto l'indirizzo IP padre. Le opzioni disponibili sono:
  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione.
  - **Round robin**: usare gli indirizzi IP padre in ordine. Questa opzione è ideale per gli scenari di bilanciamento del carico.
  - **Primo disponibile**: usare sempre il primo indirizzo IP disponibile nell'elenco.
  - **Hash**: crea un valore hash per la parte del percorso dell'URL richiesto. Questa opzione assicura che lo stesso indirizzo IP padre venga sempre usato per lo stesso URL.
  - **Casuale**: usare in modo casuale un indirizzo IP nell'elenco. Questa opzione è ideale per gli scenari di bilanciamento del carico.
  - **Temporaneo disponibile**: usare sempre il primo indirizzo IP nell'elenco. Se non è disponibile, usare il secondo indirizzo IP nell'elenco. Continuare a usare il secondo indirizzo IP fino a quando non è disponibile e così via.

## <a name="login-items"></a>Elementi di accesso

### <a name="settings-apply-to-all-enrollment-types"></a>Le impostazioni si applicano a: Tutti i tipi di registrazione

- **Aggiungere le cartelle, le app e i file personalizzati che verranno aperti all'avvio**: selezionare **Aggiungi** per aggiungere il percorso di un file, una cartella, un'app personalizzata o un'app di sistema da aprire quando gli utenti accedono ai loro dispositivi. Specificare anche:

  - **Percorso dell'elemento**: Immettere il percorso del file, della cartella o dell'app. Le app di sistema o le app compilate o personalizzate per l'organizzazione si trovano in genere nella cartella `Applications`, con un percorso simile a `/Applications/AppName.app`.

    È possibile aggiungere molti file, cartelle e app. Ad esempio, immettere:  
  
    - `/Applications/Calculator.app`
    - `/Applications`
    - `/Applications/Microsoft Office/root/Office16/winword.exe`
    - `/Users/UserName/music/itunes.app`
  
    Quando si aggiunge un'app, una cartella o un file, assicurarsi di immettere il percorso corretto. Non tutti gli elementi si trovano nella cartella `Applications`. Se gli utenti spostano un elemento da una posizione a un'altra, il percorso viene modificato. Questo elemento spostato non verrà aperto quando l'utente accede.

  - **Nascondi**: scegliere di mostrare o nascondere l'app. Le opzioni disponibili sono:
    - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe mostrare gli elementi nell'elenco degli elementi di accesso Utenti e gruppi con l'opzione Nascondi deselezionata.
    - **Sì**: nasconde l'app nell'elenco degli elementi di accesso Utenti e gruppi.

## <a name="login-window"></a>Finestra di accesso

### <a name="settings-apply-to-all-enrollment-types"></a>Le impostazioni si applicano a: Tutti i tipi di registrazione

- **Mostra informazioni aggiuntive sulla barra dei menu**: quando viene selezionata l'area del tempo nella barra dei menu, **Sì** mostra il nome host e la versione di macOS. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe non visualizzare queste informazioni nella barra dei menu.
- **Banner**: immettere un messaggio che viene visualizzato nella schermata di accesso dei dispositivi. Ad esempio, immettere le informazioni sull'organizzazione, un messaggio di benvenuto, le informazioni perse e trovate e così via.
- **Rendi obbligatori i campi di testo nome utente e password**: scegliere la modalità di accesso degli utenti ai dispositivi. **Sì** richiede agli utenti di immettere un nome utente e una password. Quando questa opzione è impostata su **Non configurato**, Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo può richiedere agli utenti di selezionare il proprio nome utente da un elenco e quindi digitare la password.

  Specificare anche:

  - **Nascondi gli utenti locali**: **Sì** non mostra gli account utente locali nell'elenco degli utenti, che può includere gli account standard e amministratore. Vengono visualizzati solo gli account utente di rete e del sistema. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe visualizzare gli account utente locali nell'elenco degli utenti.
  - **Nascondi gli account per dispositivi mobili**: **Sì** non mostra gli account per dispositivi mobili nell'elenco degli utenti. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe visualizzare gli account di dispositivi mobili nell'elenco degli utenti. Alcuni account per dispositivi mobili possono essere visualizzati come utenti della rete.
  - **Mostra gli utenti di rete**: selezionare **Sì** per elencare gli utenti di rete nell'elenco degli utenti. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe non visualizzare gli account utente di rete nell'elenco degli utenti.
  - **Nascondi gli amministratori del computer**: **Sì** non mostra gli account utente amministratori nell'elenco degli utenti. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe visualizzare gli account utente amministratori nell'elenco degli utenti.
  - **Mostra gli altri utenti**: selezionare **Sì** per elencare **Altri...** utenti nell'elenco degli utenti. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe non visualizzare gli altri account utente nell'elenco degli utenti.

- **Nascondi il pulsante Arresta**: **Sì** non mostra il pulsante di arresto nella schermata di accesso. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe visualizzare il pulsante Arresta.
- **Nascondi il pulsante Riavvia**: **Sì** non mostra il pulsante di riavvio nella schermata di accesso. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe visualizzare il pulsante Riavvia.
- **Nascondi il pulsante Sospendi**: **Sì** non mostra il pulsante di sospensione nella schermata di accesso. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe visualizzare il pulsante Sospendi.
- **Disabilita l'accesso utente dalla console**: **Sì** nasconde la riga di comando macOS usata per accedere. Per gli utenti tipici, impostare su **Sì**. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti esperti di accedere usando la riga di comando di macOS. Per passare alla modalità console, gli utenti immettono `>console` nel campo Nome utente e devono autenticarsi nella finestra della console.
- **Disabilita Arresta quando è stato eseguito l'accesso**: **Sì** impedisce agli utenti di selezionare l'opzione **Arresta** dopo aver effettuato l'accesso. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di selezionare la voce di menu **Arresta** nei dispositivi.
- **Disabilita Riavvia quando è stato eseguito l'accesso**: **Sì** impedisce agli utenti di selezionare l'opzione **Riavvia** dopo aver effettuato l'accesso. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di selezionare la voce di menu **Riavvia** nei dispositivi.
- **Disabilita Spegni quando è stato eseguito l'accesso**: **Sì** impedisce agli utenti di selezionare l'opzione **Spegni** dopo aver effettuato l'accesso. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di selezionare la voce di menu **Spegni** nei dispositivi.
- **Disabilita Disconnetti quando è stato eseguito l'accesso** (macOS 10.13 e versioni successive): **Sì** impedisce agli utenti di selezionare l'opzione **Disconnetti** dopo aver effettuato l'accesso. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di selezionare la voce di menu **Disconnetti** nei dispositivi.
- **Disabilita Schermata di blocco quando è stato eseguito l'accesso** (macOS 10.13 e versioni successive): **Sì** impedisce agli utenti di selezionare l'opzione **Schermata di blocco** dopo aver effettuato l'accesso. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di selezionare la voce di menu **Schermata di blocco** nei dispositivi.

## <a name="single-sign-on-app-extension"></a>Estensione dell'app Single Sign-On

Questa funzionalità si applica a:

- macOS 10.15 e versioni successive

### <a name="settings-apply-to-user-approved-device-enrollment-and-automated-device-enrollment"></a>Le impostazioni si applicano a: Registrazione dei dispositivi approvata dall'utente e registrazione automatica dei dispositivi

- **Tipo di estensione dell'app per accesso Single Sign-On**: scegliere il tipo di estensione dell'app per l'accesso Single Sign-On. Le opzioni disponibili sono:

  - **Non configurata**: non vengono usate le estensioni dell'app. Per disabilitare un'estensione dell'app, impostare il tipo di estensione dell'app per l'accesso Single Sign-On su **Non configurato**.
  - **Microsoft Azure AD**: Usa il plug-in Microsoft Enterprise Single Sign-On, che è un'estensione dell'app per accesso Single Sign-On di tipo reindirizzamento. Questo plug-in offre l'accesso SSO per gli account Active Directory in tutte le applicazioni macOS che supportano la funzionalità [Enterprise Single Sign-On di Apple](https://developer.apple.com/documentation/authenticationservices). Usare questo tipo di estensione dell'app SSO per abilitare l'accesso Single Sign-On per le app Microsoft, le app dell'organizzazione e i siti Web che eseguono l'autenticazione con Azure AD.

    Il plug-in per l'accesso Single Sign-On funge da broker di autenticazione avanzato e offre miglioramenti della sicurezza e dell'esperienza utente.

    > [!IMPORTANT]
    > Per ottenere l'accesso SSO con il tipo di estensione dell'app per accesso Single Sign-On di Microsoft Azure AD, installare prima l'app Portale aziendale macOS nei dispositivi. L'app Portale aziendale distribuisce il plug-in Microsoft Enterprise Single Sign-On ai dispositivi. Le impostazioni dell'estensione dell'app per accesso Single Sign-On di MDM attivano il plug-in. Dopo aver installato l'app Portale aziendale e il profilo dell'estensione dell'app per accesso Single Sign-On nei dispositivi, gli utenti possono accedere con le loro credenziali e creare una sessione nei loro dispositivi. Questa sessione viene usata tra diverse applicazioni senza richiedere agli utenti di eseguire di nuovo l'autenticazione.
    >
    > Per altre informazioni sull'app Portale aziendale, vedere [Cosa succede se si installa l'app Portale aziendale e si registra il dispositivo macOS in Intune](../user-help/what-happens-if-you-install-the-Company-Portal-app-and-enroll-your-device-in-intune-macos.md). [Scaricare](https://go.microsoft.com/fwlink/?linkid=853070) l'app Portale aziendale.

  - **Reindirizzamento**: usare un'estensione dell'app di reindirizzamento generica e personalizzabile per usare Single Sign-On con i flussi di autenticazione moderni. Assicurarsi di conoscere l'estensione e l'ID team per l'estensione dell'app dell'organizzazione.
  - **Credenziali**: usare un'estensione dell'app per le credenziali personalizzabile e generica per usare Single Sign-On con i flussi di autenticazione challenge-and-response (richiesta e risposta). Assicurarsi di conoscere l'ID estensione e l'ID team dell'estensione dell'app per l'accesso Single Sign-On dell'organizzazione.  
  - **Kerberos**: usare l'estensione Kerberos predefinita di Apple, inclusa in macOS Catalina 10.15 e versioni successive. Questa opzione è una versione specifica di Kerberos dell'estensione dell'app **Credenziali**.

  > [!TIP]
  > Con i tipi **Reindirizzamento** e **Credenziali** è possibile aggiungere i propri valori di configurazione per passare l'estensione. Se si usa il tipo **Credenziali**, può essere utile usare le impostazioni di configurazione predefinite di Apple nel tipo **Kerberos**.

- **ID estensione** (reindirizzamento e credenziali): immettere l'identificatore dell'aggregazione che identifica l'estensione dell'app per l'accesso Single Sign-On, ad esempio `com.apple.ssoexample`.
- **ID team** (reindirizzamento e credenziali): immettere l'identificatore del team dell'estensione dell'app per l'accesso Single Sign-On. Un identificatore del team è una stringa alfanumerica (numeri e lettere) di 10 caratteri generata da Apple, ad esempio `ABCDE12345`. 

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

- **Utilizzo di Keychain** (solo Kerberos): scegliere **Blocca** per impedire il salvataggio e l'archiviazione delle password in Keychain. Se l'impostazione è bloccata, non viene richiesto agli utenti di salvare la password e gli utenti devono immettere nuovamente la password quando il ticket Kerberos scade. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire il salvataggio e l'archiviazione delle password in Keychain. Agli utenti non viene richiesto di immettere nuovamente la password quando il ticket scade.
- **Face ID, Touch ID o passcode** (solo Kerberos): **Richiedi** impone agli utenti di immettere Face ID, Touch ID o passcode del dispositivo quando sono necessarie le credenziali per aggiornare il ticket Kerberos. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe non richiedere agli utenti di usare la biometria o il passcode del dispositivo per aggiornare il ticket Kerberos. Se l'impostazione **Utilizzo di Keychain** è bloccata, non è applicabile.
- **Area di autenticazione predefinita** (solo Kerberos): scegliere **Abilita** per impostare il valore **Area di autenticazione** immesso come area di autenticazione predefinita. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe non impostare un'area di autenticazione predefinita.

  > [!TIP]
  > - **Abilitare** questa impostazione se si stanno configurando più estensioni dell'app per l'accesso Single Sign-On Kerberos nell'organizzazione.
  > - **Abilitare** questa impostazione se si usano più aree di autenticazione. Imposta il valore **Area di autenticazione** immesso come area di autenticazione predefinita.
  > - Se si ha una sola area di autenticazione, lasciare l'impostazione **Non configurato** (impostazione predefinita).

- **Individuazione automatica** (solo Kerberos): quando questa opzione è impostata su **Blocca**, l'estensione Kerberos non usa automaticamente LDAP e DNS per determinare il rispettivo nome del sito di Active Directory. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire all'estensione di individuare automaticamente il nome del sito Active Directory.
- **Modifiche della password** (solo Kerberos): **Blocca** impedisce agli utenti di modificare le password usate per accedere ai domini immessi. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire le modifiche della password.  
- **Sincronizzazione password** (solo Kerberos): scegliere **Abilita** per sincronizzare le password locali degli utenti per Azure AD. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe disabilitare la sincronizzazione delle password in Azure AD. Usare questa impostazione come alternativa o backup per l'accesso Single Sign-On. Questa impostazione non funziona se gli utenti hanno eseguito l'accesso con un account per dispositivi mobili Apple.
- **Complessità della password di Windows Server Active Directory** (solo Kerberos): scegliere **Richiedi** per forzare le password degli utenti a soddisfare i requisiti di complessità delle password di Active Directory. Per altre informazioni, vedere [Le password devono essere conformi ai requisiti di complessità](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements). Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe non richiedere agli utenti di rispettare i requisiti delle password di Active Directory.
- **Lunghezza minima password** (solo Kerberos): immettere il numero minimo di caratteri che possono costituire le password degli utenti. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe non applicare una lunghezza minima della password agli utenti.
- **Limite di riutilizzo password** (solo Kerberos): immettere il numero di nuove password, da 1 a 24, che vengono usate prima che una password precedente possa essere usata nuovamente nel dominio. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe non imporre un limite di riutilizzo delle password.
- **Validità minima della password** (solo Kerberos): immettere il numero di giorni per cui viene usata una password nel dominio prima che gli utenti possano modificarla. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe non imporre una validità minima delle password prima che possano essere modificate.
- **Notifica della scadenza della password** (solo Kerberos): immettere il numero di giorni prima della scadenza di una password per cui gli utenti riceveranno una notifica della scadenza della password. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe usare `15` giorni.
- **Scadenza password** (solo Kerberos): immettere il numero di giorni che devono trascorrere prima che la password del dispositivo debba essere cambiata. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe non prevedere la scadenza delle password.
- **URL di modifica della password** (solo Kerberos): immettere l'URL che viene visualizzato quando gli utenti avviano una modifica della password Kerberos.
- **Nome entità** (solo Kerberos): immettere il nome utente dell'entità Kerberos. Non è necessario includere il nome dell'area di autenticazione. Ad esempio, in `user@contoso.com` `user` è il nome dell'entità e `contoso.com` è il nome dell'area di autenticazione.

  > [!TIP]
  > - È anche possibile usare le variabili nel nome dell'entità immettendo parentesi graffe `{{ }}`. Ad esempio, per visualizzare il nome utente, immettere `Username: {{username}}`. 
  > - Prestare tuttavia attenzione alla sostituzione delle variabili poiché le variabili non vengono convalidate nell'interfaccia utente e fanno distinzione tra maiuscole e minuscole. Assicurarsi di immettere le informazioni corrette.
  
- **Codice del sito di Active Directory** (solo Kerberos): immettere il nome del sito Active Directory che deve essere usato dall'estensione Kerberos. Potrebbe non essere necessario modificare questo valore poiché l'estensione Kerberos potrebbe trovare automaticamente il codice del sito Active Directory.
- **Nome cache** (solo Kerberos): immettere il nome GSS (Generic Security Services) della cache Kerberos. Probabilmente non è necessario impostare questo valore.  
- **Messaggio relativo ai requisiti per le password** (solo Kerberos): immettere una versione in formato testo dei requisiti per le password dell'organizzazione visualizzati agli utenti. Il messaggio viene visualizzato se non sono richiesti i requisiti di complessità delle password di Active Directory o non si specifica la lunghezza minima della password.  
- **Abilita la modalità dispositivo condiviso** (solo Microsoft Azure AD): selezionare **Sì** se si distribuisce il plug-in Microsoft Enterprise Single Sign-On ai dispositivi macOS configurati per la funzionalità della modalità dispositivo condiviso di Azure AD. I dispositivi in modalità condivisa consentono a molti utenti di effettuare l'accesso e la disconnessione a livello globale dalle applicazioni che supportano Modalità dispositivo condiviso. Quando questa opzione è impostata su **Non configurato**, Intune non modifica o aggiorna questa impostazione. 

  Se è impostata su **Sì**, tutti gli account utente esistenti vengono cancellati dai dispositivi. Per evitare la perdita di dati o per impedire il ripristino delle impostazioni predefinite, assicurarsi di capire gli effetti di questa impostazione sui dispositivi.

  Per altre informazioni sulla modalità dispositivo condiviso, vedere [Panoramica della modalità dispositivo condiviso](https://docs.microsoft.com/azure/active-directory/develop/msal-shared-devices).

- **ID bundle dell'app** (Microsoft Azure AD, Kerberos): **aggiungere** gli identificatori delle aggregazioni di app che devono usare l'accesso Single Sign-On nei dispositivi. A queste app viene concesso l'accesso al ticket di concessione ticket Kerberos e al ticket di autenticazione. Anche le app autenticano gli utenti per i servizi a cui sono autorizzati ad accedere.
- **Mapping dell'area di autenticazione dei domini** (solo Kerberos): **aggiungere** i suffissi DNS di dominio che devono essere mappati all'area di autenticazione. Usare questa impostazione quando i nomi DNS degli host non corrispondono al nome dell'area di autenticazione. Probabilmente non è necessario creare questo mapping da dominio ad area di autenticazione personalizzato.
- **Certificato PKINIT** (solo Kerberos): **selezionare** il certificato PKINIT (Public Key Cryptography for Initial Authentication) che può essere usato per l'autenticazione Kerberos. È possibile scegliere tra i certificati [PKCS](../protect/certficates-pfx-configure.md) o [SCEP](../protect/certificates-scep-configure.md) aggiunti in Intune. Per altre informazioni sui certificati, vedere [Usare i certificati per l'autenticazione in Microsoft Intune](../protect/certificates-configure.md).

## <a name="next-steps"></a>Passaggi successivi

[Assegnare il profilo](device-profile-assign.md) e [monitorarne lo stato](device-profile-monitor.md).

È anche possibile configurare le funzionalità del dispositivo in [iOS/iPadOS](ios-device-features-settings.md).
