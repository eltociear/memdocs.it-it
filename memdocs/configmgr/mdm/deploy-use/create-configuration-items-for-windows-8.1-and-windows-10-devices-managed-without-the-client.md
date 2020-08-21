---
title: Creare elementi di configurazione per Windows
titleSuffix: Configuration Manager
description: Creare elementi di configurazione per gestire le impostazioni per i computer Windows 10 con la gestione di dispositivi mobili (MDM) locale in Configuration Manager.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 23e1e4dc-623a-4521-ad04-ae9482927097
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 26846066aa713d40fdacfe75810d43cafd1c3f04
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88693676"
---
# <a name="create-configuration-items-for-windows-devices-with-on-premises-mdm-in-configuration-manager"></a>Creare elementi di configurazione per dispositivi Windows con MDM locale in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Usare l'elemento di configurazione Configuration Manager **Windows 8.1 e Windows 10** per gestire le impostazioni per i dispositivi Windows gestiti con la gestione di dispositivi mobili (MDM) locale.

Per informazioni più generali sulle impostazioni di conformità in Configuration Manager, vedere gli articoli seguenti:

- [Introduzione alle impostazioni di conformità](../../compliance/get-started/get-started-with-compliance-settings.md)

- [Pianificare e configurare le impostazioni di conformità](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)

## <a name="create-a-configuration-item"></a>Creare un elemento di configurazione

1. Nella console di Configuration Manager passare all'area di lavoro **asset e conformità** , espandere **impostazioni di conformità**e quindi selezionare il nodo **elementi di configurazione** .

1. Nella scheda **Home** della barra multifunzione selezionare **Crea elemento di configurazione** nel gruppo **Crea**.

1. Nel **Generale** pagina del **Creazione guidata dell'elemento di configurazione**, specificare le seguenti informazioni:

    - **Nome**: nome univoco per identificare questo elemento di configurazione.

    - **Descrizione**: descrizione facoltativa per fornire ulteriori informazioni sul relativo utilizzo.

    - In **impostazioni per i dispositivi gestiti *senza* il client di Configuration Manager**selezionare **Windows 8.1 e Windows 10**.

    - **Categorie**: è possibile creare e assegnare categorie per facilitare la ricerca e il filtraggio degli elementi di configurazione nella console di Configuration Manager.

1. Nella pagina **piattaforme supportate** della procedura guidata selezionare le piattaforme Windows specifiche per valutare questo elemento di configurazione.

1. Nella pagina **Impostazioni dispositivo** selezionare i gruppi di impostazioni che si desidera configurare. Per ulteriori informazioni sulle impostazioni disponibili, vedere [riferimento alle impostazioni](#bkmk_setref).

    > [!TIP]
    > Se l'impostazione desiderata non è inclusa nell'elenco, selezionare l'opzione per **configurare impostazioni aggiuntive non presenti nei gruppi di impostazioni predefinite**. Questa opzione consente di aggiungere la pagina **Impostazioni aggiuntive** alla procedura guidata.

1. In ogni pagina di impostazioni configurare le impostazioni necessarie. Quando le impostazioni lo supportano, è anche possibile monitorare e **aggiornare le impostazioni non conformi**. Se un dispositivo valuta l'impostazione come non conforme a questo elemento di configurazione, l'impostazione verrà risolta in modo da essere conforme.

    Per ogni gruppo di impostazioni, è anche possibile configurare la gravità segnalata quando l'impostazione non è conforme. Scegliere uno dei valori seguenti per l'opzione **gravità della non conformità per i report** :

    - **Nessuno**: i dispositivi che non soddisfano questa regola di conformità non segnalano una gravità dell'errore per i report di Configuration Manager.

    - **Informazioni**

    - **Warning**

    - **Critico**

    - **Errore critico con evento**: i dispositivi che non soddisfano questa regola di conformità segnalano una gravità dell'errore di tipo **Errore critico** per i report di Configuration Manager. Registra inoltre lo stato non conforme come un evento Windows nel registro eventi dell'applicazione.

1. Nella pagina **applicabilità piattaforma** della procedura guidata, esaminare le impostazioni che non sono compatibili con le piattaforme supportate selezionate. Tornare indietro e rimuovere queste impostazioni, modificare le piattaforme di supporto o continuare.

    > [!IMPORTANT]
    > I dispositivi non valutano la conformità delle impostazioni non supportate.

1. Completare la procedura guidata.

È possibile visualizzare il nuovo elemento di configurazione nel nodo **Elementi di configurazione** dell'area di lavoro **Asset e conformità** .

## <a name="settings-reference"></a><a name="bkmk_setref"></a> Riferimento alle impostazioni  

Le sezioni seguenti illustrano in dettaglio le impostazioni specifiche disponibili in ogni gruppo. Configurare queste impostazioni nella pagina **Impostazioni dispositivo** della creazione **guidata dell'elemento di configurazione** per i dispositivi **Windows 8.1 e Windows 10** gestiti *senza* il client di Configuration Manager.

### <a name="password"></a>Password

Queste impostazioni sono solo per i dispositivi che eseguono Windows 10 e versioni successive.

- **Richiedi impostazioni password nei dispositivi**: richiedere una password nei dispositivi supportati.
- **Lunghezza minima password (caratteri)**: lunghezza minima della password.
- **Scadenza password in giorni**: numero di giorni prima che l'utente debba modificare la password.
- **Numero di password memorizzate**: impedisce il riutilizzo delle password usate in precedenza.
- **Numero di tentativi di accesso non riusciti prima**della cancellazione del dispositivo: se questo numero di tentativi di accesso ha esito negativo, MDM Cancella il dispositivo
- **Tempo di inattività prima del blocco del dispositivo**: specificare la quantità di tempo per cui un dispositivo può rimanere inattivo prima che venga bloccato. Il dispositivo è inattivo quando non è presente alcun input da parte dell'utente.
- **Complessità password**: scegliere se è possibile specificare un PIN numerico, ad esempio `1234` , o se è necessario fornire una password complessa.
  - **Numero di set di caratteri complessi richiesti nella password**: se la complessità della password è **elevata**, selezionare il numero di tipi di caratteri necessari per la password: lettere maiuscole, lettere minuscole, numeri o simboli. Per impostazione predefinita, questo valore è `2`.
- **Invia PIN di ripristino password a Exchange Server**

### <a name="device"></a>Dispositivo

- **Acquisizione schermo**: abilitare questa impostazione per consentire all'utente di acquisire uno screenshot dello schermo del dispositivo. (solo Windows 10)
- **Invio dati di diagnostica**: abilitare questa impostazione per consentire i dati di diagnostica di Windows per l'analisi. (solo Windows 8.1)
- **Consenti l'invio di dati di diagnostica (Windows 10)**: impostare il livello dei dati di diagnostica di Windows per Analytics: Disable, Basic, Enhanced o full. (solo Windows 10)
- **Georilevazione**: abilitare questa impostazione per consentire al dispositivo di usare le informazioni dei servizi di posizione. (solo Windows 10)
- **Copy and paste**: abilitare questa impostazione per usare copia e incolla per trasferire i dati tra le app. (solo Windows 10)
- **Ripristino**delle impostazioni predefinite: abilitare questa impostazione per consentire all'utente di ripristinare le impostazioni iniziali del dispositivo. (solo Windows 10)
- **Bluetooth**: consente o impedisce l'uso della funzionalità Bluetooth del dispositivo.
- **Modalità individuabile Bluetooth**: consente o impedisce l'individuazione del dispositivo da parte di altri dispositivi Bluetooth. (solo Windows 10)
- **Pubblicità Bluetooth**: consente o impedisce l'uso di annunci con Bluetooth. (solo Windows 10)
- **Registrazione vocale**: consente o impedisce l'uso delle funzionalità di registrazione vocale del dispositivo. (solo Windows 10)
- **Cortana**: consente o impedisce l'uso dell'Assistente vocale di Cortana. (solo Windows 10)
- **Notifiche del centro operativo**: abilitare o disabilitare il riquadro delle notifiche in Windows 10. (solo Windows 10)
- **Modifica delle impostazioni dell'area (solo desktop)**: consente o impedisce all'utente di modificare le impostazioni internazionali del dispositivo.
- **Modifica delle impostazioni di risparmio energia e sospensione (solo desktop)**: consente o impedisce all'utente di modificare le impostazioni di risparmio energia e sospensione nel dispositivo.
- **Modifica delle impostazioni della lingua (solo desktop)**: consente o impedisce all'utente di modificare le impostazioni della lingua nel dispositivo.
- **Modifica dell'ora di sistema**: consente o impedisce all'utente di modificare la data e l'ora del dispositivo.
- **Modifica del nome del dispositivo**: consente o impedisce all'utente di modificare il nome del dispositivo.

### <a name="email-management"></a>Gestione della posta elettronica

Queste impostazioni si riferiscono solo ai dispositivi che eseguono Windows 8.1 e Windows 10.  

- **Posta elettronica POP e IMAP**: consente o impedisce le connessioni agli account di posta elettronica che usano gli standard pop e IMAP.
- **Tempo massimo di conservazione della posta elettronica**: per quanto tempo è necessario mantenerlo prima che il server lo elimini.
- **Formati di messaggi consentiti**: specificare se i messaggi di posta elettronica sono **testo normale** o **HTML e testo normale**.
- **Dimensione massima per la posta elettronica di testo normale (scaricata automaticamente)**: impostare la dimensione massima dei messaggi di posta elettronica di testo normale quando vengono scaricati automaticamente.
- **Dimensione massima per la posta elettronica HTML (scaricata automaticamente)**: impostare la dimensione massima dei messaggi di posta elettronica HTML quando vengono scaricati automaticamente.
- **Dimensione massima di un allegato (scaricato automaticamente)**: impostare la dimensione massima degli allegati di posta elettronica scaricati automaticamente.
- **Sincronizzazione del calendario**: consente o impedisce la sincronizzazione dei calendari al dispositivo.
- **Account di posta elettronica personalizzato**: consente o impedisce l'uso di un account di posta elettronica non aziendale sul dispositivo.
- **Rendi l'account Microsoft facoltativo nell'app Windows Mail**: abilitare questa opzione per non richiedere un account Microsoft in Windows Mail.

### <a name="store"></a>Archivio

Queste impostazioni sono solo per i dispositivi che eseguono Windows 10 e versioni successive.

- **Archivio applicazioni**: consentire o impedire l'accesso al Microsoft Store nel dispositivo.
- **Immettere una password per accedere allo Store di applicazioni**: abilitare questa opzione per richiedere agli utenti di immettere una password per accedere all'app Microsoft Store.
- **Acquisti in-app**: consentire o impedire agli utenti di effettuare acquisti in-app.
- **Avvio dell'app originata dallo Store**: Disabilita tutte le app preinstallate nel dispositivo o installate dal Microsoft Store.
- **Aggiorna automaticamente le app dallo Store**: consente o impedisce l'aggiornamento automatico delle app installate dal Microsoft Store.
- **Installare le app nell'unità di sistema**: consentire o impedire al dispositivo di installare le app nell'unità di sistema, che in genere è l' `C:` unità.
- **Installa i dati dell'app nel volume di sistema**: abilitare questa opzione per consentire alle app di archiviare i dati nell'unità di sistema.
- **Usa solo lo store privato**: richiedere agli utenti di scaricare le app dallo Store privato.
- **Gioco DVR**: Disabilita la registrazione e la trasmissione del gioco Windows

### <a name="browser"></a>Browser

Queste impostazioni si riferiscono solo ai dispositivi che eseguono Windows 8.1 e Windows 10.

- **Consenti il Web browser**: consente o impedisce l'uso del Web browser nel dispositivo.
- **Riempimento automatico**: consente o impedisce la modifica delle impostazioni di completamento automatico nel browser.
- **Scripting attivo**: consente o impedisce se il browser può eseguire script, ad esempio gli script ActiveX.
- **Plug-** in: consente o impedisce l'aggiunta di plug-in a Internet Explorer.
- **Blocco popup**: consente o impedisce il blocco popup del browser.
- **Cookie**: consente o impedisce il salvataggio dei cookie nel dispositivo.
- **Avviso di illecito**: consentire o proibire avvisi di potenziali siti Web fraudolenti.

### <a name="internet-explorer"></a>Internet Explorer

Queste impostazioni si riferiscono solo ai dispositivi che eseguono Windows 8.1 e Windows 10.

- **Invia sempre l'intestazione Do Not Track**: consente o impedisce l'invio di informazioni di esplorazione a siti di terze parti.
- **Area di protezione Intranet**: consente o impedisce l'assegnazione di un livello di sicurezza all'area di sicurezza Intranet.
- **Livello di sicurezza per l'area Internet**: impostare il livello di sicurezza per l'area Internet: alta, media-alta o media.
- **Livello di protezione per l'area Intranet**: impostare il livello di sicurezza per l'area Intranet: alta, medio-alta, media, medio-basso o basso.
- **Livello di protezione per l'area siti attendibili**: impostare il livello di sicurezza per l'area siti attendibili: alta, medio-alta, media, medio-bassa o bassa.
- **Livello di protezione per l'area siti con restrizioni**: impostare il livello di sicurezza per l'area siti con restrizioni: alto.
- **Spazi dei nomi per l'area Intranet**: configurare i siti Web da aggiungere o rimuovere dall'area Intranet.
- **Vai al sito Intranet per l'immissione di una singola parola**: Consenti o Impedisci a Internet Explorer di passare automaticamente a un sito Intranet se l'utente immette un nome di sito valido senza un protocollo precedente, ad esempio `https://` .
- **Opzione di menu modalità Enterprise**: consente agli utenti di attivare e disattivare la modalità Enterprise dal menu **strumenti** di Internet Explorer.
  - **Percorso report di registrazione (URL)**: quando è attiva la modalità Enterprise, specificare un URL per registrare i siti Web visitati.
- **Posizione elenco siti modalità Enterprise (URL)**: quando è attiva la modalità Enterprise, specificare l'elenco di siti Web che lo usano.

### <a name="cloud"></a>Cloud

Queste impostazioni si riferiscono solo ai dispositivi che eseguono Windows 8.1 e Windows 10.

- **Sincronizzazione delle impostazioni**: consente o impedisce le impostazioni per la sincronizzazione tra dispositivi.
- **Sincronizzazione delle credenziali**: consente o impedisce le credenziali per la sincronizzazione tra dispositivi.
- **Account Microsoft**: abilitare questa impostazione per consentire l'uso di un account Microsoft nel dispositivo.
- **Sincronizzazione delle impostazioni con connessioni a consumo**: consente o impedisce le impostazioni per la sincronizzazione quando viene misurata la connessione di rete.

### <a name="security"></a>Sicurezza

- **Installazione file non firmati**: consente agli utenti che possono installare un file non firmato. (solo Windows 10)
- **Applicazioni non firmate**: consentire o impedire l'installazione di app non firmate. (solo Windows 10)
- **Messaggistica SMS e MMS**: consentire o proibire protocolli SMS sul dispositivo. (solo Windows 10)
- **Archivi rimovibili**: consente o impedisce l'uso di archivi rimovibili, ad esempio una scheda SD. (solo Windows 10)
- **Fotocamera**: consente o impedisce l'uso della fotocamera del dispositivo. (solo Windows 10)
- **NFC (Near Field Communication)**: consente o impedisce la comunicazione tramite NFC. (solo Windows 10)
- **Modalità antifurto**: consente o impedisce l'uso della modalità AntiTheft di Windows 10. (solo Windows 10)
- **Consenti la connessione USB**: consente o impedisce ad altri dispositivi di connettersi a questo dispositivo tramite una connessione USB. (solo Windows 10)
- **Profilo VPN Windows RT**: effettua il provisioning di un profilo VPN per i dispositivi Windows RT (solo Windows 8.1)

### <a name="peak-synchronization"></a>Sincronizzazione nelle ore di punta

Queste impostazioni sono solo per i dispositivi che eseguono Windows 10 e versioni successive.

- **Specificare l'ora di punta**: impostare l'ora di picco e i giorni della settimana per la sincronizzazione dei dispositivi mobili.
- **Frequenza di sincronizzazione in ore di punta**: configurare la frequenza con cui viene eseguita la sincronizzazione durante le ore di picco.
- **Frequenza di sincronizzazione fuori ore di punta**: configurare la frequenza con cui viene eseguita la sincronizzazione fuori dalle ore di picco.

### <a name="roaming"></a>Roaming

- **Gestione dei dispositivi durante il roaming**: consente o impedisce Configuration Manager la gestione del dispositivo durante il roaming. (solo Windows 10)
- **Download del software durante il roaming**: consente o impedisce il download di applicazioni e software durante il roaming. (solo Windows 10)
- **Download della posta elettronica durante il roaming**: consente o impedisce i download di posta elettronica durante il roaming. (solo Windows 10)
- **Roaming dei dati**: consente o impedisce il roaming tra reti quando si accede ai dati.
- **VPN su rete cellulare**: consente o impedisce al dispositivo di usare una connessione VPN mentre è connessa a una rete cellulare. (solo Windows 10)
- **Roaming VPN su rete cellulare**: consente o impedisce al dispositivo di usare una connessione VPN durante il roaming in una rete cellulare. (solo Windows 10)

### <a name="encryption"></a>Crittografia

- **Crittografia scheda di memoria**: impostare on per richiedere all'utente di crittografare le schede di memoria usate nel dispositivo. (solo Windows 10)
- **Crittografia file nel dispositivo**: impostare on per crittografare i file archiviati nel dispositivo.
- **Richiedi la firma tramite posta elettronica**: l'utente deve firmare digitalmente i messaggi di posta elettronica prima di essere inviati.
  - **Algoritmo di firma**: selezionare l'algoritmo per la firma di messaggi di posta elettronica: default, SHA o MD5
- **Richiedi crittografia posta elettronica**: l'utente deve crittografare i messaggi di posta elettronica prima di essere inviati.
  - **Algoritmo di crittografia**: selezionare l'algoritmo per la crittografia dei messaggi di posta elettronica: default, triple DES, des, RC2 128-bit, RC2 64-bit, RC2 40-bit

### <a name="wireless-communications"></a>Comunicazioni wireless

Queste impostazioni sono solo per i dispositivi che eseguono Windows 10 e versioni successive.

- **Connessione di rete wireless**: consente o impedisce la funzionalità Wi-Fi del dispositivo.
- **Tethering Wi-Fi**: consentire all'utente di usare il dispositivo come hotspot mobile.
- **Offload dei dati al Wi-Fi quando possibile**: consentire al dispositivo di usare la connessione Wi-Fi per quanto possibile.
- **Reporting hotspot Wi-Fi**: consente al dispositivo di inviare informazioni sulle connessioni Wi-Fi per consentire all'utente di individuare le connessioni nelle vicinanze.
- **Configurazione Wi-Fi manuale**: consente all'utente di configurare manualmente le connessioni wireless.

#### <a name="configured-wireless-network-connections"></a>Connessioni di rete wireless configurate

1. Nella pagina **Configura impostazioni di comunicazione wireless del dispositivo mobile** selezionare **Aggiungi**.

1. Nella finestra **Connessione rete wireless** specificare le informazioni seguenti sulla connessione wireless per il provisioning nei dispositivi mobili:

    - **Nome rete (SSID)**: immettere il nome della rete Wi-Fi.
    - **Connessione di rete**: scegliere **Internet** o **lavoro**.
    - **Autenticazione**: scegliere il metodo di autenticazione per la connessione wireless:
        - **Apri**
        - **Condivisa**
        - **WPA**
        - **WPA-PSK**
        - **WPA2**
        - **WPA2-PSK**
    - **Crittografia dei dati**: scegliere il metodo di crittografia usato dalla connessione. I valori disponibili cambiano in base al metodo di **autenticazione** selezionato:
        - **Disabilitato**
        - **WEP**
        - **TKIP**
        - **AES**
    - **Indice chiave**: quando si imposta la **crittografia dei dati** su **WEP**, selezionare un indice chiave da **1** a **4**.
    - **Questa rete si connette a Internet**: specificare le impostazioni proxy per consentire ai dispositivi mobili in una rete wireless di connettersi a Internet.
        - **Impostazioni server proxy**: configurare le impostazioni del **Server** e della **porta** per i proxy **http**, **WAP**e **Sockets** .
    - **Impostazioni 802.1 x**:
        - **Abilitare l'accesso alla rete 802.1 x**: proteggere la connessione specificando un tipo EAP.
        - **Tipo EAP**: scegliere uno dei protocolli di autenticazione seguenti:
            - **PEAP**
            - **Smart card o certificato**

### <a name="certificates"></a>Certificati

Importare i certificati da installare nei dispositivi mobili.

Selezionare **Importa**, quindi specificare i valori seguenti:

- **File di certificato**: individuare e selezionare un file di certificato (**. cer**) da importare.
- **Archivio di destinazione**: scegliere uno o più degli archivi certificati seguenti:
  - **Radice**
  - **CA**
  - **Normal**
  - **Con privilegi**
  - **SPC**
  - **Peer**
- **Ruolo**: se si sceglie l'archivio certificati **SPC** (Software Publisher certificate), scegliere il ruolo da associare al certificato:
  - **Operatore di telefonia mobile**
  - **Responsabile**
  - **Autenticazione utente**
  - **Amministratore IT**
  - **Utente non autenticato**
  - **Server di provisioning attendibile**

### <a name="system-security"></a>Protezione del sistema

- **Controllo account utente**: consente di configurare il comportamento del controllo dell'account utente di Windows nel dispositivo.
- **Firewall di rete**: Richiedi Windows per abilitare il firewall incorporato. (Windows 8.1)
- **Aggiornamenti**: configurare il comportamento degli aggiornamenti software di Windows. (Windows 8.1)
  - **Classificazione minima degli aggiornamenti**: scegliere la classificazione minima degli aggiornamenti da scaricare e installare: **nessuno**, **importante**o **consigliato**.
- **Aggiornamenti (Windows 10)**: configurare il comportamento degli aggiornamenti software di Windows. (solo Windows 10)
  - **Giorno di installazione**: scegliere il giorno pianificato quando il dispositivo installa automaticamente gli aggiornamenti e i riavvii. (solo Windows 10)
  - **Ora di installazione**: scegliere l'ora pianificata in cui il dispositivo installa automaticamente gli aggiornamenti e i riavvii. (solo Windows 10)
- **SmartScreen**: Abilita o Disabilita lo schermo intelligente di Windows.
- **Protezione da virus**: richiedere che Windows disponga di un software antivirus.
- Le **firme di protezione da virus sono**aggiornate: è necessario che i file delle firme antivirus siano aggiornati.
- **Visualizzazione notifiche schermata di blocco**: abilitare o disabilitare le notifiche da visualizzare nella schermata di blocco.
- **Funzionalità di versioni**non definitive: specificare se il dispositivo accetta le impostazioni e le funzionalità di versione non definitiva. (solo Windows 10)
- **Installazione manuale del certificato radice**: abilitare o disabilitare l'utente per installare manualmente un certificato radice, che Abilita l'attendibilità per qualsiasi certificato emesso da tale radice. (solo Windows 10)
- Consenti l'annullamento della **registrazione manuale**: consente o impedisce all'utente di annullare la registrazione del dispositivo dalla gestione dei dispositivi mobili locale con Configuration Manager.

### <a name="windows-server-work-folders"></a>Cartelle di lavoro di Windows Server

Queste impostazioni si riferiscono solo ai dispositivi che eseguono Windows 8.1 e Windows 10.

- **URL cartelle di lavoro**: specificare il percorso di una cartella di lavoro di Windows Server a cui gli utenti possono connettersi dal dispositivo.

### <a name="allowed-and-blocked-apps-list"></a>Elenco delle app consentite e bloccate

Queste impostazioni sono solo per i dispositivi che eseguono Windows Phone, che Configuration Manager MDM locale non supporta. Per altre informazioni, vedere [Che cosa è successo alla MDM ibrida?](../understand/what-happened-to-hybrid.md).

### <a name="windows-10-team"></a>Windows 10 Team

Queste impostazioni sono solo per i dispositivi che eseguono Windows 10 team.

- **Consenti la riattivazione automatica dello schermo quando i sensori rilevano qualcuno nella stanza**: consentire o impedire al dispositivo di riattivarsi automaticamente quando il sensore rileva qualcuno nella chat room.
- **Richiedi PIN per proiezione wireless**: abilitare o disabilitare se è necessario immettere un PIN prima che un altro dispositivo possa connettersi in modalità wireless per la proiezione.
- **Finestra di manutenzione**: abilitare questa impostazione per configurare la finestra quando gli aggiornamenti possono installare e riavviare il dispositivo.
  - **Ora di inizio**: impostare l'ora di inizio per la finestra di manutenzione.
  - **Durata (ore)**: impostare la lunghezza in ore della finestra di manutenzione.
- **Azure Operational Insights**: consentire ad [Azure Operational Insights](https://azure.microsoft.com/resources/videos/azure-operational-insights-overview/) di raccogliere, archiviare e analizzare i dati dei file di log dai dispositivi Windows 10 team.
  - **ID area di lavoro**: immettere un ID di area di lavoro valido
  - **Chiave area di lavoro**: immettere la chiave per l'area di lavoro associata
- **Proiezione wireless Miracast**: consente di proiettare i dispositivi abilitati per Miracast in questo dispositivo Windows 10 team.
  - **Canale Miracast**: selezionare un canale Miracast per proiettare il contenuto.
- **Informazioni sulla riunione visualizzate nella schermata iniziale**: scegliere il tipo di informazioni visualizzate dal dispositivo nel riquadro **riunioni** della schermata **iniziale** :
  - **Mostra solo organizzatore e ora**
  - **Mostra organizzatore, ora e oggetto (l'oggetto è nascosto per le riunioni private)**
- **URL immagine di sfondo Lockscreen**: specificare un URL per visualizzare uno sfondo personalizzato nella schermata **iniziale** di un dispositivo Windows 10 team. Avviare l'URL con `https://` e usare il formato png.

### <a name="windows-information-protection"></a>Windows Information Protection  

Per ulteriori informazioni su come configurare la protezione dei dati aziendali con Configuration Manager, vedere [proteggere i dati aziendali mediante Windows Information Protection (WIP)](/windows/security/information-protection/windows-information-protection/protect-enterprise-data-using-wip).

### <a name="microsoft-edge-legacy"></a>Legacy Microsoft Edge

Queste impostazioni sono solo per i dispositivi che eseguono Windows 10 e versioni successive.  

- **Consenti suggerimenti di ricerca nella barra degli indirizzi**: consente al motore di ricerca di suggerire siti durante la digitazione delle frasi di ricerca.
- **Consenti Do Not Track**: informa i siti Web che non si vuole tenere traccia della visita.
- **Enable SmartScreen**: verificare che i file scaricati non contengano codice dannoso.
- **Consenti popup**: Configura popup del browser.
- **Consenti cookie**: configurare l'uso dei cookie.
- **Consenti riempimento**automatico: consente al browser di riempire automaticamente i moduli con informazioni archiviate, ad esempio nome, indirizzo e telefono.
- **Consenti password manager**: consente al browser di archiviare e gestire le password per i siti Web.
- **Strumenti di sviluppo**: consente o impedisce la funzionalità degli strumenti di sviluppo di Edge.
- **Estensioni**: consentire o proibire estensioni di Edge.
- **InPrivate Browsing**: consente o impedisce InPrivate Browsing, che non archivia cronologia o cookie.
- **Indirizzo IP localhost WebRTC**: consente o impedisce la visualizzazione dell'indirizzo IP localhost del dispositivo quando l'utente effettua chiamate telefoniche tramite il protocollo Web RTC.
- **Blocca l'accesso a about: Flags**: consente o impedisce all'utente di accedere alla `about:flags` pagina, che contiene le impostazioni sperimentali e di sviluppo.
- **Override del prompt SmartScreen per i file**: consente o impedisce all'utente di ignorare gli avvisi del filtro SmartScreen sul download di file potenzialmente dannosi.
- **Override del prompt SmartScreen**: consente o impedisce all'utente di ignorare gli avvisi del filtro SmartScreen relativi a siti Web potenzialmente dannosi.
- **Primo URL di esecuzione**: specificare un sito Web da visualizzare quando un utente apre la rete perimetrale per la prima volta.

### <a name="windows-defender-antivirus"></a>Windows Defender Antivirus

Queste impostazioni sono solo per i dispositivi che eseguono Windows 10 e versioni successive.

- **Consenti il monitoraggio in tempo reale**: Abilita l'analisi in tempo reale per malware, spyware e altro software indesiderato.
- **Consenti il monitoraggio del comportamento**: Defender controlla la presenza di alcuni modelli noti di attività sospette nei dispositivi.
- **Enable Network Inspection System**: il Network Inspection System (NIS) consente di proteggere i dispositivi dagli exploit basati sulla rete. Usa le firme delle vulnerabilità note da Microsoft Endpoint Protection Center per consentire di rilevare e bloccare il traffico dannoso.
- **Analizza tutti i download**: Defender analizza tutti i file scaricati da Internet.
- **Consenti analisi script**: Defender analizza gli script usati in Internet Explorer.
- **Monitora l'attività di file e programmi**: Defender monitora l'attività di file e programmi nei dispositivi.
  - **File monitorati**: scegliere il tipo di file da monitorare: tutti, in ingresso o in uscita.
- **Giorni di rilevamento del malware risolto**: Defender continua a tenere traccia del malware risolto per il numero di giorni specificato. È quindi possibile controllare manualmente i dispositivi precedentemente interessati. Se si imposta il numero di giorni su 0, il malware rimane nella cartella di quarantena e non viene rimosso automaticamente. Il valore massimo è 90.
- **Consenti accesso all'interfaccia utente client**: controlla se nascondere l'interfaccia utente di Defender dagli utenti. Quando si modifica questa impostazione, l'operazione viene applicata alla successiva riavvio del dispositivo.
- **Pianificare un'analisi del sistema**: scegliere un'analisi completa o veloce che viene eseguita regolarmente il giorno e l'ora selezionati:
  - **Giorno pianificato**: scegliere il giorno pianificato quando Defender esegue l'analisi.
  - **Tempo pianificato**: scegliere l'ora pianificata in cui Defender esegue l'analisi.
- **Pianifica un'analisi veloce giornaliera**: scegliere l'ora pianificata quando Defender esegue un'analisi veloce ogni giorno.
- **Limita utilizzo CPU durante un'analisi**: impostare la percentuale del processore che Defender può utilizzare durante l'esecuzione di un'analisi. Immettere un valore compreso tra 1 e 100.
- **Analizza file di archivio**: Defender analizza gli archivi compressi, ad esempio i file con estensione zip o CAB.
- **Analizza messaggi di posta elettronica**: Defender analizza i messaggi di posta elettronica non appena arrivano sul dispositivo.
- **Analizza unità rimovibili**: Defender analizza le unità rimovibili, ad esempio le chiavette USB.
- **Analizza unità mappate**: Defender analizza le unità mappate a condivisioni di rete. Ad esempio, `H:` viene eseguito il mapping all'unità personale di un utente. Se i file nell'unità sono di sola lettura, Defender non può rimuovere il malware rilevato.
- **Analizza i file aperti da cartelle di rete condivise**: Defender analizza i file quando un utente li apre da un percorso di rete condiviso. Ad esempio: `\\server\share\file.doc`. Se il file nella condivisione è di sola lettura, Defender non può rimuovere alcun malware rilevato.
- **Intervallo di aggiornamento della firma**: scegliere l'intervallo di tempo quando Defender verifica la presenza di nuovi file di firma.
- **Consenti la protezione cloud**: Defender usa il cloud Microsoft per ricevere informazioni sull'attività malware e abilitare funzionalità come il blocco a prima visione.
- **Richiedi agli utenti l'invio dei campioni**: scegliere il comportamento per Defender quando i file potrebbero richiedere un'ulteriore analisi. Ad esempio, Defender può inviare automaticamente i file a Microsoft per determinare se sono dannosi.
- **Rilevamento di applicazioni potenzialmente indesiderate**: protegge il dispositivo dal software in esecuzione Classificato da Defender come potenzialmente indesiderato. È possibile proteggersi da queste applicazioni in esecuzione o usare la modalità di controllo per segnalare quando un utente installa un'applicazione potenzialmente indesiderata.
- **Esclusioni di file e cartelle**: aggiungere uno o più file e cartelle all'elenco esclusioni. Ad esempio, `C:\Path` o `%ProgramFiles%\Path\filename.exe`. Defender non include questi file e cartelle nelle analisi in tempo reale o pianificate.
- **Esclusioni**di estensioni di file: aggiungere una o più estensioni di file all'elenco esclusioni. Ad esempio, `java` o `exe`. Defender non include alcun file con queste estensioni nelle analisi in tempo reale o pianificate.
- **Esclusioni dei processi**: aggiungere processi specifici all'elenco esclusioni. Ad esempio: `C:\path\myproc.exe`. Questo tipo di esclusione supporta solo le estensioni seguenti: `exe` , `com` o `scr` . Defender non include questi processi nelle analisi in tempo reale o pianificate.

### <a name="additional-settings"></a>Impostazioni aggiuntive

Nella pagina **Impostazioni dispositivo** della procedura guidata, se si seleziona l'opzione per la **configurazione di impostazioni aggiuntive non presenti nei gruppi**di impostazioni predefinite, utilizzare questa pagina di **Impostazioni aggiuntive** per configurare tali impostazioni. Selezionare **Aggiungi** e quindi scegliere dall'elenco delle impostazioni per dispositivi mobili disponibili. Scegliere **Seleziona** per modificare l'impostazione predefinita o **Crea impostazione** per creare un valore di registro personalizzato o un tipo di impostazione URI OMA.

## <a name="next-steps"></a>Passaggi successivi

[Monitorare le impostazioni di conformità](../../compliance/deploy-use/monitor-compliance-settings.md)