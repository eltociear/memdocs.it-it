---
title: Gestione client basata su Internet
titleSuffix: Configuration Manager
description: Creare una piano per gestire client basati su Internet in Configuration Manager.
ms.date: 05/16/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 83a7c934-3b11-435d-ba22-cbc274951e83
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 485b27e9781d9c636b8dfe3691fa7f7068a6db92
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696679"
---
# <a name="plan-for-internet-based-client-management-in-configuration-manager"></a>Pianificare la gestione dei client basata su Internet in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

La gestione dei client basata su Internet consente di gestire i client di Configuration Manager quando non sono connessi alla rete aziendale, ma usano una connessione Internet standard. Tale disposizione presenta diversi vantaggi che includono la riduzione dei costi associata alla possibilità di non dover eseguire reti private virtuali (VPN) e di poter distribuire aggiornamenti software in modo tempestivo.  

 Dati i requisiti di protezione più elevati per la gestione di computer client su una rete pubblica, la gestione client basata su Internet richiede che i client e i server del sistema del sito ai quali si collegano usino certificati PKI. Ciò garantisce che le connessioni vengano autenticate da un'autorità indipendente e che i dati provenienti da e diretti a questi sistemi del sito vengano crittografati tramite Secure Sockets Layer (SSL).  

 Usare le sezioni seguenti per la pianificazione della gestione client basata su Internet.  

##  <a name="features-that-are-not-supported-on-the-internet"></a>Funzionalità non supportate su Internet  
 Non tutte le funzionalità di gestione client sono adatte a Internet e, pertanto, non sono supportate quando i client vengono gestiti su Internet. Le funzionalità non supportate per la gestione su Internet in genere si basano su Active Directory Domain Services o non sono adatte a una rete pubblica, come individuazione rete e riattivazione LAN (WOL).  

 Le caratteristiche seguenti non sono supportate quando i client sono gestiti su Internet:  

- Distribuzione di client su Internet, ad esempio la distribuzione client basata su aggiornamento software e push client. Usare invece l'installazione client manuale.  

- Assegnazione automatica del sito.  

- Riattivazione LAN.  

- Distribuzione del sistema operativo. Tuttavia, è possibile distribuire le sequenze attività che non distribuiscono un sistema operativo, come ad esempio sequenze che eseguono script e attività di manutenzione sui client  

- Controllo remoto.  

- Distribuzione software agli utenti a meno che il punto di gestione basato su Internet sia in grado di autenticare l'utente in Active Directory Domain Services tramite l'autenticazione di Windows (Kerberos o NTLM). Questo è possibile quando il punto di gestione basato su Internet considera attendibile la foresta in cui risiede l'account utente.  

  La gestione client basata su Internet, inoltre, non supporta il roaming. Il roaming consente ai client di individuare sempre i punti di distribuzione più vicini per scaricare il contenuto. I client gestiti su Internet comunicano con i sistemi del sito dal relativo sito assegnato quando i sistemi sono configurati per l'utilizzo di un FQDN Internet e i ruoli del sistema del sito consentono connessioni client da Internet. I client selezionano in modo non deterministico uno dei sistemi del sito basati su Internet, indipendentemente dalla posizione fisica o dalla larghezza di banda.  

  Se si dispone di un punto di aggiornamento software configurato per accettare le connessioni a Internet, i client basati su Internet di Configuration Manager eseguono l'analisi sempre rispetto a questo punto per determinare gli aggiornamenti software necessari. Tuttavia, i client su Internet provano a scaricare prima gli aggiornamenti software da Microsoft Update piuttosto che da un punto di distribuzione basato su Internet. Solo in caso di errore, proveranno quindi a scaricare gli aggiornamenti software richiesti da un punto di distribuzione basato su Internet. I client non configurati per la gestione client basata su Internet non provano mai a scaricare gli aggiornamenti software da Microsoft Update, ma usano sempre i punti di distribuzione di Configuration Manager.  
 
> [!Tip]  
> Il client di Configuration Manager determina automaticamente se si trova sull'intranet o su Internet. Se il client riesce a contattare un controller di dominio o un punto di gestione locale, imposta il proprio tipo di connessione su Ora intranet. In caso contrario, passa a Ora Internet e il client usa i punti di gestione, i punti di aggiornamento software e i punti di distribuzione assegnati al proprio sito per la comunicazione.

##  <a name="considerations-for-client-communications-from-the-internet-or-untrusted-forest"></a>Considerazioni per le comunicazioni client da Internet o da una foresta untrusted  
 I seguenti ruoli del sistema del sito installati nei siti primari supportano connessioni da client che si trovano in percorsi non attendibili, come Internet o una foresta untrusted (i siti secondari non supportano le connessioni client da percorsi non attendibili):  

- Punto per siti Web del Catalogo applicazioni  

    > [!Important]  
    > Il supporto per i ruoli del Catalogo applicazioni termina con la versione 1910. Per altre informazioni, vedere [Rimuovere il catalogo applicazioni](../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

- Modulo criteri di Configuration Manager  

- Punto di distribuzione (HTTPS è richiesto dai punti di distribuzione basati sul cloud)  

- Punto proxy di registrazione  

- Punto di stato di fallback  

- Punto di gestione  

- Punto di aggiornamento software  

  **Informazioni sui sistemi del sito con connessione internet:**    
  Sebbene non sia richiesto un trust tra la foresta di un client e quella di un server del sistema del sito, quando la foresta che contiene il sistema del sito con connessione Internet considera attendibile la foresta che contiene gli account utente, questa configurazione supporta criteri basati sull'utente per i dispositivi su Internet se si abilita l'impostazione client **Abilitare le richieste dei criteri utente dai client Internet** di **Criteri client**.  

  Ad esempio, le configurazioni seguenti illustrano quando la gestione client basata su Internet supporta criteri utente per i dispositivi su Internet:  

- Il punto di gestione basato su Internet si trova nella rete perimetrale in cui risiede un controller di dominio di sola lettura per autenticare l'utente e un firewall consente il passaggio dei pacchetti di Active Directory.  

- L'account utente si trova nella Foresta A (intranet) e il punto di gestione basato su Internet si trova nella Foresta B (la rete perimetrale). La Foresta B considera attendibile la Foresta A e un firewall consente i pacchetti di autenticazione.  

- L'account utente e il punto di gestione basato su Internet si trovano nella Foresta A (intranet). Il punto di gestione viene pubblicato su Internet usando un server Web proxy, ad esempio Forefront Threat Management Gateway.  

> [!NOTE]  
>  Se l'autenticazione Kerberos ha esito negativo, sarà automaticamente tentata l'autenticazione NTLM.  

 Come mostrato nell'esempio precedente, è possibile posizionare i sistemi del sito basati su Internet nella Intranet quando vengono pubblicati su Internet usando un server Web proxy, come ISA Server e Forefront Threat Management Gateway. Questi sistemi del sito possono essere configurati per connessioni client solo da Internet o per connessioni client da Internet e Intranet. Quando si usa un server Web proxy, è possibile configurarlo per il bridging Secure Sockets Layer (SSL) a SSL (più sicuro) o tunneling SSL:  

-   **Bridging SSL a SSL:**    
    La configurazione consigliata quando si usano server Web proxy per la gestione client basata su Internet è il bridging da SSL a SSL, che usa la terminazione SSL con l'autenticazione. I computer client devono essere autenticati usando l'autenticazione computer e i client legacy di dispositivi mobili vengono autenticati usando l'autenticazione utente. I dispositivi mobili che vengono registrati da Configuration Manager non supportano il bridging SSL.  

     Il vantaggio della terminazione SSL sul server Web proxy è che i pacchetti provenienti da Internet sono soggetti alla verifica prima di essere inoltrati alla rete interna. Il server Web proxy autentica la connessione dal client, la termina, quindi apre una nuova connessione autenticata ai sistemi del sito basati su Internet. Quando i client di Configuration Manager usano un server Web proxy, l'identità client (GUID client) viene contenuta in modo protetto all'interno del payload dei pacchetti in modo che il punto di gestione non consideri il server Web proxy come il client. Il bridging HTTP a HTTPS o HTTPS a HTTP non è supportato in Configuration Manager.  
     
    > [!Note]  
    > Configuration Manager non supporta l'impostazione di configurazioni di bridge SSL di terze parti. Ad esempio, Citrix Netscaler o F5 BIG-IP. Collaborare con il fornitore del dispositivo per configurarlo per l'uso con Configuration Manager.  

-   **Tunneling**:   
    Se il server Web proxy non può supportare i requisiti per il bridging SSL o se si vuole configurare il supporto Internet per i dispositivi mobili registrati da Configuration Manager, è supportato il tunneling SSL. Si tratta di un'opzione meno sicura perché i pacchetti SSL provenienti da Internet vengono inoltrati ai sistemi del sito senza terminazione SSL e, pertanto, non possono essere verificati per l'eventuale presenza di contenuto dannoso. Quando si usa il tunneling SSL, non sono previsti requisiti di certificato per il server Web proxy.  

##  <a name="planning-for-internet-based-clients"></a>Pianificazione dei client basati su Internet  
 È necessario decidere se i computer client che saranno gestiti su Internet debbano essere configurati per la gestione sulla Intranet e su Internet o solo per la gestione client basata su Internet. L'opzione di gestione client può essere configurata solo durante l'installazione di un computer client. Se si cambia idea, sarà necessario reinstallare il client.  

> [!NOTE]  
>  Se si configura un punto di gestione con Internet, i client che si connettono al punto di gestione potranno usare Internet dopo aver aggiornato l'elenco di punti di gestione disponibili.  

> [!TIP]  
>  Non si dovrà limitare la configurazione esclusivamente alla gestione client basata su Internet in modo da poterla usare anche sulla Intranet.  

 I client configurati solo per la gestione basata su Internet comunicano esclusivamente con i sistemi del sito configurati per le connessioni client da Internet. Questa configurazione sarebbe ideale per i computer che non vengono mai connessi alla intranet aziendale, ad esempio computer POS in sedi remote. Potrebbe anche essere appropriata se si vuole limitare la comunicazione client solo a HTTPS (ad esempio per supportare firewall e criteri di sicurezza limitati), se si installano sistemi del sito basati su Internet in una rete perimetrale e se si vuole gestire tali server usando il client di Configuration Manager.  

 Quando si desidera gestire client di un gruppo di lavoro su Internet, è necessario installarli con una configurazione limitata a Internet.  

> [!NOTE]  
>  I client dei dispositivi mobili vengono configurati automaticamente solo per Internet quando sono configurati per l'utilizzo di un punto di gestione basato su Internet.  

 È possibile configurare altri computer client per la gestione client Internet e Intranet. Possono passare automaticamente dalla gestione client basata su Internet a quella basata sulla Intranet e viceversa quando rilevano una modifica della rete. Se questi client possono rilevare e connettersi a un punto di gestione configurato per le connessioni client sull'intranet, vengono gestiti come client intranet con piene funzionalità di gestione di Configuration Manager. Se i client non sono in grado di rilevare o di connettersi a un punto di gestione configurato per le connessioni client sulla Intranet, cercano di connettersi a un punto di gestione basato su Internet e, se vi riescono, vengono gestiti come sistemi del sito basati su Internet nel rispettivo sito assegnato.  

 Il vantaggio di un passaggio automatico tra la gestione client basata su Internet e una gestione client basata sull'intranet è che i computer client possono usare automaticamente tutte le funzionalità di Configuration Manager quando si connettono alla Intranet e continuano a essere gestiti per le funzioni di gestione essenziali quando sono connessi a Internet. Inoltre, un download iniziato su Internet può riprendere senza problemi sulla Intranet e viceversa.  

##  <a name="prerequisites-for-internet-based-client-management"></a>Prerequisiti per la gestione client basata su Internet  
 La gestione client basata su Internet in Configuration Manager presenta le dipendenze esterne seguenti:  

- I client che verranno gestiti su Internet devono disporre di una connessione a Internet.  

   Configuration Manager usa connessioni esistenti del Provider di servizi Internet (ISP) a Internet, che possono essere di natura permanente o temporanea. I dispositivi mobili client devono disporre di una connessione diretta a Internet, mentre i computer client possono usufruire di una connessione Internet diretta oppure di una connessione tramite server Web proxy.  

- I sistemi del sito che supportano la gestione client basata su Internet devono disporre della connettività a Internet e devono trovarsi in un dominio Active Directory.  

   I sistemi del sito basati su Internet non richiedono una relazione di trust con la foresta Active Directory del server del sito. Tuttavia, quando il punto di gestione basato su Internet è in grado di autenticare l'utente usando l'autenticazione di Windows, sono supportati criteri utente. Se l'autenticazione di Windows ha esito negativo, sono supportati solo i criteri computer.  

  > [!NOTE]
  >  Per supportare i criteri utente è inoltre necessario impostare **True** per le due impostazioni client **Criteri client** :  
  > 
  > - **Abilitare il polling dei criteri utente sui client**  
  >   -   **Abilitare le richieste dei criteri utente dai client Internet**  

   Un punto per siti Web del Catalogo applicazioni basato su Internet richiede inoltre l'autenticazione di Windows per autenticare gli utenti quando il relativo computer si trova su Internet. Questo requisito è indipendente dai criteri utente.  

- È necessario disporre di un'infrastruttura a chiave pubblica (PKI) di supporto che possa distribuire e gestire i certificati richiesti dai client e gestiti su Internet e sui server del sistema del sito basati su Internet.  

   Per altre informazioni sui certificati PKI, vedere [Requisiti dei certificati PKI per Configuration Manager](../../plan-design/network/pki-certificate-requirements.md).  

- Il nome di dominio completo (FQDN) Internet dei sistemi del sito che supportano la gestione client basata su Internet deve essere registrato come voce host sui server DNS pubblici.  

- I firewall o server proxy devono consentire la comunicazione client associata ai sistemi del sito basati su Internet.  

   Requisiti di comunicazione client:  

  - Supporto HTTP 1.1  

  - Autorizzazione al tipo di contenuto HTTP di allegati MIME multiparte (multiparte/misto e applicazione/flusso di ottetti)  

  - Autorizzazione ai seguenti verbi per il punto di gestione basato su Internet:  

    -   HEAD  

    -   CCM_POST  

    -   BITS_POST  

    -   GET  

    -   PROPFIND  

  - Autorizzazione ai seguenti verbi per il punto di distribuzione basato su Internet:  

    -   HEAD  

    -   GET  

    -   PROPFIND  

  - Autorizzazione ai seguenti verbi per il punto di stato di fallback basato su Internet:  

    -   POST  

  - Autorizzazione ai seguenti verbi per il punto per siti Web del Catalogo applicazioni basato su Internet:  

    -   POST  

    -   GET  

  - Autorizzazione alle seguenti intestazioni HTTP per il punto di gestione basato su Internet:  

    -   Intervallo:  

    -   CCMClientID:  

    -   CCMClientIDSignature:  

    -   CCMClientTimestamp:  

    -   CCMClientTimestampsSignature:  

  - Autorizzazione alla seguente intestazione HTTP per il punto di distribuzione basato su Internet:  

    -   Intervallo:  

    Per informazioni sulla configurazione richiesta per supportare tali requisiti, consultare la documentazione sul server proxy o firewall.  

    Per i requisiti di comunicazione simili richiesti quando si usa il punto di aggiornamento software per le connessioni client da Internet, vedere la documentazione per Windows Server Update Services (WSUS). Ad esempio, per WSUS su Windows Server 2003, vedere [Appendice D: Impostazioni di protezione](https://go.microsoft.com/fwlink/p/?LinkId=143368), l'appendice della distribuzione per le impostazioni di protezione.
