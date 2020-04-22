---
title: Riferimento tecnico per i controlli crittografici
titleSuffix: Configuration Manager
description: Questo argomento illustra come la firma e la crittografia consentono di impedire agli autori di attacchi la lettura dei dati in Configuration Manager.
ms.date: 12/08/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: df289c284774a4e0bb3a379853f31f8d6f5bd44d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704169"
---
# <a name="cryptographic-controls-technical-reference"></a>Riferimento tecnico per i controlli crittografici

*Si applica a: Configuration Manager (Current Branch)*

Configuration Manager usa la firma e la crittografia per proteggere la gestione dei dispositivi nella gerarchia di Configuration Manager. Con la firma, se i dati sono stati modificati in transito vengono scartati. La crittografia consente di impedire a un utente malintenzionato di leggere i dati usando uno strumento di analisi dei protocolli di rete.  

 L'algoritmo hash primario usato da Configuration Manager per la firma è SHA-256. Quando due siti di Configuration Manager comunicano tra loro, firmano le comunicazioni con SHA-256. L'algoritmo di crittografia primario implementato in Configuration Manager è 3DES. Questo algoritmo viene usato per archiviare dati nel database di Configuration Manager e per la comunicazione HTTP del client. Quando si usa la comunicazione client in HTTPS, è possibile configurare l'infrastruttura a chiave pubblica (PKI) per usare i certificati RSA con gli algoritmi hash e le lunghezze di chiave massimi documentati in [Requisiti dei certificati PKI](../network/pki-certificate-requirements.md).  

 Per la maggior parte delle operazioni crittografiche per i sistemi operativi basati su Windows, Configuration Manager usa gli algoritmi SHA-2, 3DES e AES, RSA dalla libreria CryptoAPI rsaenh.dll di Windows.  

> [!IMPORTANT]  
>  In [Informazioni sulle vulnerabilità di SSL](#about-ssl-vulnerabilities)sono disponibili informazioni sulle modifiche consigliate in risposta alle vulnerabilità di SSL.  

##  <a name="cryptographic-controls-for-configuration-manager-operations"></a>Controlli crittografici per le operazioni di Configuration Manager  
 Le informazioni in Configuration Manager possono essere firmate e crittografate, indipendentemente dal fatto che si usino i certificati PKI con Configuration Manager.  

### <a name="policy-signing-and-encryption"></a>Firma e crittografia di criteri  
 Le assegnazioni di criteri client vengono firmate dal certificato di firma del server del sito autofirmato per evitare i rischi di sicurezza di un punto di gestione compromesso che invia criteri manomessi. Questo è importante se si sta usando la gestione client basata su Internet, perché questo ambiente richiede un punto di gestione esposto alla comunicazione Internet.  

 I criteri vengono crittografati con 3DES quando contengono dati sensibili. I criteri che contengono dati sensibili vengono inviati solo ai client autorizzati. I criteri che non dispongono di dati sensibili non vengono crittografati.  

 Quando il criterio viene archiviato nei client, viene crittografato usando l'API di protezione dati (DPAPI).  

### <a name="policy-hashing"></a>Hash criteri  
 Quando i client di Configuration Manager richiedono criteri, per prima cosa ricevono un'assegnazione di criteri in modo da sapere quali criteri verranno applicati, quindi richiedono solo quei corpi di criteri. Ogni assegnazione di criteri contiene l'hash calcolato per il corpo di criteri corrispondente. Il client recupera i corpi di criteri applicabili, quindi calcola l'hash di tale corpo. Se l'hash nel corpo di criteri scaricato non corrisponde all'hash nell'assegnazione di criteri, il client rimuove il corpo di criteri.  

 L'algoritmo hash per i criteri è SHA-1 e SHA-256.  

### <a name="content-hashing"></a>Hash contenuto  

Il servizio di Gestione distribuzione nel server del sito genera un hash per i file di contenuto per tutti i pacchetti. Il provider di criteri include l'hash nei criteri di distribuzione software. Quando il client di Configuration Manager scarica il contenuto, il client rigenera l'hash a livello locale e lo confronta con quello specificato nei criteri. Se gli hash corrispondono, il contenuto non è stato alterato e il client lo installa. Se un singolo byte del contenuto è stato modificato, gli hash non corrispondono e il software non verrà installato. Questo controllo consente di verificare che sia installato il software corretto poiché il contenuto effettivo viene confrontato con i criteri.  

L'algoritmo hash predefinito per il contenuto è SHA-256.

Non tutti i dispositivi sono in grado di supportare l'hash contenuto. Le eccezioni includono:  

- Client Windows quando trasmettono contenuto App-V.  

- Client Windows Phone, anche se questi client verificano la firma di un'applicazione firmata da una fonte attendibile.  

- Client Windows RT, anche se questi client verificano la firma di un'applicazione firmata da una fonte attendibile e usano anche la convalida del nome completo del pacchetto.  

- Client eseguiti su versioni di Linux e UNIX che non supportano SHA-256. Per altre informazioni, vedere [Pianificazione della distribuzione client per computer Linux e UNIX](../../clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md).  

### <a name="inventory-signing-and-encryption"></a>Firma e crittografia dell'inventario  
 L'inventario che i client inviano ai punti di gestione viene sempre firmato dai dispositivi, indipendentemente dalla comunicazioni con i punti di gestione in HTTP o HTTPS. Se usano HTTP, è possibile crittografare questi dati, il che è consigliabile.  

### <a name="state-migration-encryption"></a>Crittografia della migrazione stato  
 I dati memorizzati nei punti di migrazione stato per la distribuzione del sistema operativo vengono sempre crittografati dall'Utilità di migrazione stato utente (USMT) usando 3DES.  

### <a name="encryption-for-multicast-packages-to-deploy-operating-systems"></a>Crittografia per pacchetti multicast per la distribuzione di sistemi operativi  
 Per ogni pacchetto di distribuzione di sistemi operativi, è possibile abilitare la crittografia quando il pacchetto viene trasferito nei computer usando multicast. La crittografia usa Advanced Encryption Standard (AES). Se si abilita la crittografia, non è necessaria alcuna configurazione aggiuntiva del certificato. Il punto di distribuzione abilitato per multicast genera automaticamente chiavi simmetriche per crittografare il pacchetto. Ogni pacchetto ha una chiave di crittografia diversa. La chiave viene memorizzata nel punto di distribuzione abilitato per multicast usando le API Windows standard. Quando il client si collega alla sessione multicast, lo scambio di chiave avviene su un canale crittografato con il certificato di autenticazione client emesso da PKI (quando il client usa HTTPS) oppure il certificato autofirmato (quando il client usa HTTP). Il client memorizza la chiave solo per la durata della sessione multicast.  

### <a name="encryption-for-media-to-deploy-operating-systems"></a>Crittografia per i supporti per la distribuzione di sistemi operativi  
 Quando si usano supporti per distribuire sistemi operativi e si specifica una password per proteggere i supporti, le variabili di ambiente sono crittografate usando Advanced Encryption Standard (AES). Gli altri dati presenti sul supporto, inclusi i pacchetti e il contenuto per le applicazioni, non vengono crittografati.  

### <a name="encryption-for-content-that-is-hosted-on-cloud-based-distribution-points"></a>Crittografia per il contenuto ospitato nei punti di distribuzione basati su cloud  
 A partire da System Center 2012 Configuration Manager SP1, quando si usano punti di distribuzione basati su cloud, il contenuto caricato su questi punti di distribuzione viene crittografato usando Advanced Encryption Standard (AES) con una chiave di dimensioni 256 bit. Quando si aggiorna, il contenuto viene nuovamente crittografato. Quando i client scaricano il contenuto, esso viene crittografato e protetto tramite la connessione HTTPS.  

### <a name="signing-in-software-updates"></a>Firma negli aggiornamenti software  
 Tutti gli aggiornamenti software devono essere firmati da un autore attendibile per la protezione contro eventuali manomissioni. Nei computer client, l'agente di Windows Update (WUA) esegue la scansione degli aggiornamenti dal catalogo, ma non installerà l'aggiornamento se non riesce a individuare il certificato digitale nell'archivio Autori attendibili nel computer locale. Se il certificato autofirmato è stato usato per la pubblicazione del catalogo degli aggiornamenti, come Autori WSUS autofirmato, il certificato deve trovarsi anche nell'archivio certificati dell'autorità di certificazione radice attendibile nel computer locale affinché venga verificata la validità del certificato stesso. L'agente di Windows Update (WUA) controlla anche se l'impostazione **Criteri di gruppo Consenti contenuto firmato dal percorso del servizio di aggiornamento Microsoft nella rete Intranet** è abilitata nel computer locale. È necessario abilitare questa impostazione dei criteri per l'agente di Windows Update affinché venga eseguita la scansione degli aggiornamenti che sono stati creati e pubblicati con Updates Publisher.  

 Quando gli aggiornamenti software vengono pubblicati in System Center Updates Publisher, un certificato digitale firma gli aggiornamenti software quando vengono pubblicati su un server di aggiornamento. È possibile specificare un certificato PKI o configurare Updates Publisher per generare un certificato autofirmato per firmare l'aggiornamento software.  

### <a name="signed-configuration-data-for-compliance-settings"></a>Dati di configurazione firmati per le impostazioni di conformità  
 Quando si importano dati di configurazione, Configuration Manager verifica la firma digitale del file. Se i file non sono stati firmati o il controllo della verifica della firma digitale non riesce, all'utente verrà notificato e richiesto se continuare con l'importazione. Continuare a importare i dati di configurazione solo se si considerano attendibili l'autore e l'integrità dei file.  

### <a name="encryption-and-hashing-for-client-notification"></a>Crittografia e hash per la notifica client  
 Se si usa la notifica client, tutte le comunicazioni usano TLS e la crittografia più elevata che il server e i sistemi operativi client possano negoziare. Ad esempio, un computer client con Windows 7 e un punto di gestione con Windows Server 2008 R2 possono supportare la crittografia AES a 128 bit, mentre un computer client con Vista sullo stesso punto di gestione negozierà una crittografia 3DES. La stessa negoziazione si verifica per l'hash dei pacchetti che vengono trasferiti durante la notifica client che usa SHA-1 o SHA-2.  

##  <a name="certificates-used-by-configuration-manager"></a>Certificati usati da Configuration Manager  
 Per un elenco dei certificati di infrastruttura a chiave pubblica (PKI) che possono essere usati da Configuration Manager, i requisiti o le limitazioni speciali e le modalità d'uso dei certificati, vedere [Requisiti dei certificati PKI](../network/pki-certificate-requirements.md). Questo elenco include gli algoritmi hash e le lunghezze di chiave supportati. La maggior parte dei certificati supporta la lunghezza di chiave SHA-256 e a 2.048 bit.  

> [!NOTE]  
>  Tutti i certificati che Configuration Manager usa devono contenere solo caratteri a byte singolo nel nome oggetto o nel nome alternativo oggetto.  

 I certificati PKI sono necessari per gli scenari seguenti:  

- Quando si gestiscono client di Configuration Manager su Internet.  

- Quando si gestiscono client di Configuration Manager su dispositivi mobili.  

- Quando si gestiscono computer Mac.  

- Quando si usano punti di distribuzione basati su cloud.  

  Per la maggior parte delle altre comunicazioni di Configuration Manager che richiedono certificati per l'autenticazione, la firma o la crittografia, Configuration Manager usa automaticamente i certificati PKI se sono disponibili. Se non sono disponibili, Configuration Manager genera certificati autofirmati.  

  Configuration Manager non usa i certificati PKI quando gestisce dispositivi mobili con il connettore Exchange Server.  

### <a name="mobile-device-management-and-pki-certificates"></a>Gestione dei dispositivi mobili e certificati PKI  
 Se il dispositivo mobile non è stato bloccato dall'operatore mobile, è possibile usare Configuration Manager o Microsoft Intune per richiedere e installare un certificato client. Questo certificato assicura l'autenticazione reciproca tra il client sul dispositivo mobile e i sistemi del sito di Configuration Manager o i servizi di Microsoft Intune. Se il dispositivo mobile è bloccato, non è possibile usare Configuration Manager o Microsoft Intune per la distribuzione dei certificati.  

 Se si abilita l'inventario hardware per i dispositivi mobili, Configuration Manager o Microsoft Intune archivia anche i certificati installati sul dispositivo mobile.   

### <a name="operating-system-deployment-and-pki-certificates"></a>Distribuzione del sistema operativo e dei certificati PKI  
 Quando si usa Configuration Manager per distribuire sistemi operativi e un punto di gestione richiede connessioni client HTTPS, anche il computer client deve usare un certificato per comunicare con il punto di gestione, anche se si trova in una fase transitoria come un avvio da supporto per sequenza di attività o in un punto di distribuzione abilitato PXE. Per supportare questo scenario, è necessario creare un certificato di autenticazione client PKI ed esportarlo con la chiave privata, quindi importarlo nelle proprietà del server del sito oltre ad aggiungere il certificato CA principale attendibile del punto di gestione.  

 Quando si crea un supporto di avvio, è necessario importare il certificato di autenticazione client. Configurare una password su un supporto di avvio per proteggere la chiave privata e altri dati sensibili configurati nella sequenza di attività. Ogni computer che si avvia dal supporto di avvio presenta lo stesso certificato al punto di gestione, come richiesto per le funzioni client quali la richiesta di criteri client.  

 Se si usa l'avvio PXE, è necessario importare il certificato di autenticazione client nel punto di distribuzione abilitato PXE e viene usato lo stesso certificato per ogni client che si avvia da quel punto di distribuzione abilitato PXE. Come procedura di sicurezza consigliata, è necessario richiedere agli utenti che collegano i computer a un servizio PXE di fornire una password per proteggere la chiave privata e altri dati sensibili nelle sequenze attività.  

 Se uno dei due certificati di autenticazione client è compromesso, bloccare i certificati nel nodo **Certificati** dell'area di lavoro **Amministrazione** , nodo **Sicurezza** . Per gestire questi certificati, è necessario disporre del diritto **Gestisci il certificato di distribuzione del sistema operativo** .  

 Dopo che la distribuzione del sistema operativo e l'installazione di Configuration Manager sono state completate, il client richiederà il certificato di autenticazione client PKI per la comunicazione client HTTPS.  

### <a name="isv-proxy-solutions-and-pki-certificates"></a>Soluzioni proxy ISV e certificati PKI  
 I fornitori di software indipendenti (ISV) possono creare applicazioni per l'estensione di Configuration Manager. Ad esempio, un ISV può creare estensioni per il supporto di piattaforme client non Windows quali Macintosh o UNIX. Tuttavia, se i sistemi del sito richiedono connessioni client HTTPS, anche questi client devono usare i certificati PKI per comunicare con il sito. Configuration Manager offre la possibilità di assegnare un certificato al proxy ISV che consente le comunicazioni tra i client proxy ISV e il punto di gestione. Se si usano le estensioni che richiedono certificati proxy ISV, consultare la documentazione del prodotto in questione. Per altre informazioni sulla creazione di certificati proxy ISV, vedere il kit per sviluppatori (SDK) di Configuration Manager.  

 Se il certificato ISV è compromesso, bloccarlo nel nodo **Certificati** dell'area di lavoro **Amministrazione** , nodo **Sicurezza** .  

### <a name="asset-intelligence-and-certificates"></a>Certificati e Asset Intelligence  
 Configuration Manager viene installato con un certificato X.509 usato dal punto di sincronizzazione di Asset Intelligence per connettersi a Microsoft. Configuration Manager usa questo certificato per richiedere un certificato di autenticazione client dal servizio certificati Microsoft. Il certificato di autenticazione client viene installato sul server del sistema sito del punto di sincronizzazione di Asset Intelligence e usato per l'autenticazione del server verso Microsoft. Configuration Manager usa il certificato di autenticazione client per scaricare il catalogo di Asset Intelligence e caricare i titoli software.  

 La lunghezza della chiave del certificato è 1.024 bit.  

### <a name="cloud-based-distribution-points-and-certificates"></a>Certificati e punti di distribuzione basati su cloud  
 A partire da System Center 2012 Configuration Manager SP1, i punti di distribuzione basati su cloud richiedono un certificato di gestione (autofirmato o PKI) che viene caricato in Microsoft Azure. Questo certificato di gestione richiede funzionalità di autenticazione server e una lunghezza della chiave del certificato di 2.048 bit. Inoltre, è necessario configurare un certificato di servizio per ciascun punto di distribuzione basato su cloud, che non può essere autofirmato ma che deve disporre di funzionalità di autenticazione server e una lunghezza minima della chiave del certificato di 2.048 bit.  

> [!NOTE]  
>  Il certificato di gestione autofirmato è esclusivamente a scopo di test e non è destinato all'uso nelle reti di produzione.  

 I client non richiedono un certificato PKI per l'utilizzo di punti di distribuzione basati su cloud; l'autenticazione tra i client e il punto gestione viene eseguita con un certificato autofirmato o un certificato PKI client. Il punto di gestione invia quindi un token di accesso di Configuration Manager al client, che a sua volta lo presenta al punto di distribuzione basato su cloud. Il token è valido per 8 ore.  

### <a name="the-microsoft-intune-connector-and-certificates"></a>Certificati e connettore Microsoft Intune  
 Quando Microsoft Intune registra dispositivi mobili, è possibile gestire tali dispositivi in Configuration Manager creando un connettore Microsoft Intune. Il connettore usa un certificato PKI con funzionalità di autenticazione client per autenticare Configuration Manager in Microsoft Intune e per trasferire tutte le informazioni tra di essi usando SSL. La chiave del certificato ha una dimensione di 2.048 bit e usa l'algoritmo hash SHA-1.  

 Quando si installa il connettore sul server del sito viene creato e archiviato un certificato di firma per chiavi di trasferimento locali, viene creato e archiviato un certificato di crittografia nel punto di registrazione del certificato per crittografare la richiesta di verifica Simple Certificate Enrollment Protocol (SCEP). La chiave di questi certificati ha una dimensione di 2048 bit e questi usano l'algoritmo hash SHA-1.  

 Quando Intune registra i dispositivi mobili, viene installato un certificato PKI nel dispositivo mobile. Il certificato dispone di funzionalità di autenticazione client e usa una chiave di 2.048 bit e l'algoritmo hash SHA-1.  

 Questi certificati PKI vengono richiesti, generati e installati automaticamente da Microsoft Intune.  

### <a name="crl-checking-for-pki-certificates"></a>Controllo CRL per i certificati PKI  
 Un elenco di revoche di certificati (CRL) PKI aumenta il carico di elaborazione e amministrativo ma garantisce maggiore sicurezza. Tuttavia, se il controllo CRL è abilitato ma il CRL non è accessibile, la connessione PKI ha esito negativo. Per altre informazioni, vedere [Sicurezza e privacy per Configuration Manager](security-and-privacy.md).  

 Per impostazione predefinita, il controllo dell'elenco di revoche di certificati (CRL) è abilitato in IIS, pertanto se si sta usando un CRL con la distribuzione PKI, non è necessario eseguire ulteriori configurazioni nella maggior parte dei sistemi del sito di Configuration Manager che eseguono IIS. L'eccezione riguarda gli aggiornamenti software, che richiedono un passaggio manuale per l'abilitazione del controllo CRL per verificare le firme sui file di aggiornamento software.  

 Per impostazione predefinita, il controllo CRL è abilitato per i computer client che usano connessioni client HTTPS. Non è possibile disabilitare il controllo CRL per i client su computer Mac in Configuration Manager SP1 o versioni successive.  

 Il controllo CRL non è supportato in Configuration Manager per le connessioni seguenti:  

-   Connessioni tra server.  

-   Dispositivi mobili registrati da Configuration Manager.  

-   Dispositivi mobili registrati da Microsoft Intune.  

##  <a name="cryptographic-controls-for-server-communication"></a>Controlli crittografici per la comunicazione tra server  
 Configuration Manager usa i seguenti controlli crittografici per la comunicazione tra server.  

### <a name="server-communication-within-a-site"></a>Comunicazione tra server all'interno di un sito  
 Ogni server del sistema del sito usa un certificato per trasferire i dati ad altri sistemi del sito nello stesso sito di Configuration Manager. Anche alcuni ruoli del sistema del sito usano certificati per l'autenticazione. Ad esempio, se si installa il punto proxy di registrazione su un server e il punto di registrazione su un altro server, questi possono autenticarsi a vicenda usando questo certificato di identità. Quando Configuration Manager usa un certificato per questa comunicazione, se è disponibile un certificato PKI con funzionalità di autenticazione server, lo usa automaticamente. In caso contrario, Configuration Manager genera un certificato autofirmato. Questo certificato autofirmato dispone di funzionalità di autenticazione server, usa SHA-256 e ha una lunghezza chiave di 2.048 bit. Configuration Manager copia il certificato nell'archivio Persone attendibili in altri server del sistema del sito per i quali potrebbe essere necessario verificare l'attendibilità del sistema del sito. I sistemi del sito possono quindi verificare la reciproca attendibilità tramite questi certificati e PeerTrust.  

 Oltre a questo certificato per ogni server del sistema del sito, Configuration Manager genera un certificato autofirmato per la maggior parte dei ruoli del sistema del sito. In presenza di più di un'istanza del ruolo del sistema del sito nello stesso sito, viene condiviso lo stesso certificato. Ad esempio, potrebbero essere presenti più punti di gestione o più punti di registrazione nello stesso sito. Inoltre, il certificato autofirmato usa SHA-256 e ha una lunghezza della chiave di 2.048 bit. Viene inoltre copiato nell'archivio Persone attendibili sui server del sistema del sito che potrebbero doverne verificare l'attendibilità. I seguenti ruoli del sistema del sito generano questo certificato:  

- Punto per servizi Web del Catalogo applicazioni  

- Punto per siti Web del Catalogo applicazioni  

- Punto di sincronizzazione di Asset Intelligence  

- Punto di registrazione certificati  

- Punto di Endpoint Protection  

- Punto di registrazione  

- Punto di stato di fallback  

- Punto di gestione  

- Punto di distribuzione abilitato per multicast  

- Punto di Reporting Services  

- Punto di aggiornamento software  

- Punto di migrazione stato  

- Connettore Microsoft Intune  

Questi certificati vengono gestiti automaticamente da Configuration Manager e generati automaticamente secondo necessità.  

Configuration Manager usa anche un certificato di autenticazione client per inviare messaggi di stato dal punto di distribuzione al punto di gestione. Quando il punto di gestione è configurato solo per connessioni client HTTPS, è necessario usare un certificato PKI. Se il punto di gestione accetta connessioni HTTP, è possibile usare un certificato PKI oppure selezionare l'opzione per l'uso di un certificato autofirmato con funzionalità di autenticazione client, che usi SHA-256 e con una lunghezza della chiave di 2.048 bit.  

### <a name="server-communication-between-sites"></a>Comunicazione server tra siti  
 Configuration Manager trasferisce i dati tra siti usando la replica di database e la replica basata su file. Per altre informazioni, vedere [Comunicazioni tra gli endpoint](../hierarchy/communications-between-endpoints.md).  

 Configuration Manager configura automaticamente la replica di database tra siti e usa i certificati PKI con funzionalità di autenticazione server, se disponibili. In caso contrario, Configuration Manager crea dei certificati autofirmati per l'autenticazione server. In entrambi i casi, l'autenticazione tra siti viene stabilita usando i certificati nell'archivio Persone attendibili che usa PeerTrust. Questo archivio certificati viene usato per garantire che solo i computer SQL Server usati dalla gerarchia di Configuration Manager partecipino alla replica tra siti. Mentre i siti primari e il sito di amministrazione centrale possono replicare le modifiche alla configurazione in tutti i siti della gerarchia, i siti secondari possono replicare tali modifiche solo nel proprio sito padre.  

 I server del sito stabiliscono la comunicazione tra siti usando uno scambio di chiavi protetto automatico. Il server del sito di origine genera un hash che viene firmato con la chiave privata. Il server del sito di destinazione controlla la firma usando la chiave pubblica e confronta l'hash con un valore generato localmente. Se corrispondono, il sito di destinazione accetta i dati replicati. Se i valori non corrispondono, Configuration Manager rifiuta i dati di replica.  

 La replica di database in Configuration Manager usa SQL Server Service Broker per trasferire i dati tra siti con i seguenti meccanismi:  

- Connessione tra SQL Server: usa le credenziali Windows per l'autenticazione server e certificati autofirmati con 1.024 bit per firmare e crittografare i dati tramite Advanced Encryption Standard (AES). Se disponibili, saranno usati certificati PKI con funzionalità di autenticazione server. Il certificato deve trovarsi nell'archivio personale per l'archivio certificati del computer.  

- SQL Service Broker: usa certificati autofirmati con 2.048 bit per l'autenticazione e per firmare e crittografare i dati tramite Advanced Encryption Standard (AES). Il certificato deve trovarsi nel database master di un computer SQL Server.  

  La replica basata su file usa il protocollo Server Message Block (SMB) e SHA-256 per firmare questi dati che non sono crittografati ma non contengono alcun dato sensibile. Per crittografare questi dati, è possibile usare lo standard IPsec, che deve essere implementato indipendentemente da Configuration Manager.  

##  <a name="cryptographic-controls-for-clients-that-use-https-communication-to-site-systems"></a>Controlli crittografici per i client che usano la comunicazione HTTPS con i sistemi del sito  
 Quando i ruoli del sistema del sito accettano connessioni client, è possibile configurarli in modo da accettare connessioni HTTPS e HTTP o solo connessioni HTTPS. I ruoli del sistema del sito che accettano connessioni da Internet accettano solo connessioni client tramite HTTPS.  

 Le connessioni client tramite HTTPS offrono un livello di protezione più elevato mediante l'integrazione con un'infrastruttura a chiave pubblica (PKI) per proteggere la comunicazione tra client e server. Tuttavia, se la configurazione delle connessioni client HTTPS viene eseguita senza una completa comprensione della pianificazione, distribuzione e delle operazioni di PKI, sussisterà un determinato livello di vulnerabilità. Ad esempio, se la CA principale non viene protetta, degli utenti non autorizzati potrebbero compromettere l'attendibilità dell'intera infrastruttura PKI. L'assenza di una distribuzione e gestione dei certificati PKI tramite processi controllati e protetti potrebbe dar luogo a client non gestiti impossibilitati a ricevere pacchetti o aggiornamenti software critici.  

> [!IMPORTANT]  
>  I certificati PKI usati per la comunicazione client proteggono la comunicazione solo tra il client e alcuni sistemi del sito. Non proteggono il canale di comunicazione tra il server del sito e i sistemi del sito o tra i server del sito.  

### <a name="communication-that-is-unencrypted-when-clients-use-https-communication"></a>Comunicazione non crittografata quando i client usano la comunicazione HTTPS  
 Quando i client comunicano con i sistemi del sito usando HTTPS, le comunicazioni sono in genere crittografate tramite SSL. Tuttavia, nelle situazioni seguenti, i client comunicano con i sistemi del sito senza usare la crittografia:  

- I client non riescono a stabilire una connessione HTTPS sulla intranet e tentano di usare HTTP quando i sistemi del sito consentono tale configurazione  

- Comunicazione con i seguenti ruoli del sistema del sito:  

  -   Il client invia messaggi di stato al punto di stato di fallback  

  -   Il client invia richieste PXE al punto di distribuzione abilitato PXE  

  -   Il client invia dati di notifica a un punto di gestione  

  I punti di Reporting Services sono configurati per usare HTTP o HTTPS in modo indipendente dalla modalità di comunicazione client.  

##  <a name="cryptographic-controls-for-clients-chat-use-http-communication-to-site-systems"></a>Controlli crittografici per i client che usano la comunicazione HTTPS con i sistemi del sito  
 Per la comunicazione HTTP con i ruoli del sistema del sito i client possono usare i certificati PKI per l'autenticazione client oppure dei certificati autofirmati generati da Configuration Manager. Quando Configuration Manager genera certificati autofirmati, questi hanno un identificatore oggetto personalizzato per la firma e la crittografia e vengono usati per identificare il client in modo univoco. Per tutti i sistemi operativi supportati, ad eccezione di Windows Server 2003, questi certificati autofirmati usano SHA-256 e la loro chiave ha una lunghezza di 2048 bit. Per Windows Server 2003, SHA1 viene usato con una lunghezza della chiave pari a 1024 bit.  

### <a name="operating-system-deployment-and-self-signed-certificates"></a>Distribuzione del sistema operativo e certificati autofirmati  
 Quando si usa Configuration Manager per distribuire sistemi operativi con certificati autofirmati, anche il computer client deve usare un certificato per comunicare con il punto di gestione, anche se si trova in una fase transitoria come un avvio da supporto per sequenza di attività o in un punto di distribuzione abilitato PXE. Per supportare questo scenario per le connessioni client HTTP, Configuration Manager genera certificati autofirmati con un identificatore oggetto personalizzato per la firma e la crittografia e vengono usati questi certificati per identificare il client in modo univoco. Per tutti i sistemi operativi supportati, ad eccezione di Windows Server 2003, questi certificati autofirmati usano SHA-256 e la loro chiave ha una lunghezza di 2048 bit. Per Windows Server 2003, SHA1 viene usato con una lunghezza della chiave pari a 1024 bit. Per evitare che utenti non autorizzati possano usare dei certificati autofirmati compromessi per impersonare client attendibili, bloccare i certificati nel nodo **Certificati** dell'area di lavoro **Amministrazione** , nodo **Sicurezza** .  

### <a name="client-and-server-authentication"></a>Autenticazione server e client  
 Quando si connettono con HTTP i client autenticano i punti di gestione usando Servizi di dominio Active Directory o la chiave radice attendibile di Configuration Manager. I client non autenticano altri ruoli del sistema del sito, ad esempio punto di migrazione stato o punti di aggiornamento software.  

 Quando un punto di gestione autentica per la prima volta un client usando il certificato client autofirmato, questo meccanismo fornisce un livello minimo di protezione poiché qualsiasi computer può generare un certificato autofirmato. In questo scenario il processo di identificazione del client deve essere aumentato mediante l'approvazione. Solo i computer attendibili devono essere approvati, automaticamente da Configuration Manager o manualmente da un utente amministratore. Per altre informazioni, vedere la sezione relativa all'approvazione in [Comunicazioni tra gli endpoint](../hierarchy/communications-between-endpoints.md).  

## <a name="about-ssl-vulnerabilities"></a>Informazioni sulle vulnerabilità di SSL
Per migliorare la sicurezza dei client e server di Configuration Manager, eseguire le operazioni seguenti:

- Abilitare TLS 1.2

  Per abilitare TLS 1.2 per Configuration Manager, vedere [Come abilitare TLS 1.2 per Configuration Manager](enable-tls-1-2.md).
- Disabilitare SSL 3.0, TLS 1.0 e TLS 1.1 
- Riordinare i pacchetti di crittografia relativi a TLS 

Per altre informazioni, vedere [Come limitare l'utilizzo di determinati algoritmi e protocolli crittografici in Schannel.dll](https://support.microsoft.com/en-us/kb/245030/) e [Prioritizing Schannel Cipher Suites](https://msdn.microsoft.com/library/windows/desktop/bb870930.aspx) (Definizione delle priorità dei pacchetti di crittografia in Schannel). Queste procedure non influiscono sulle funzionalità di Configuration Manager.

