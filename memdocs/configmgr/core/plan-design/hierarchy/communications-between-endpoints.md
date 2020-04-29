---
title: Comunicazioni tra gli endpoint
titleSuffix: Configuration Manager
description: Informazioni sulle modalità di comunicazione tra i componenti e i sistemi del sito di Configuration Manager in una rete.
ms.date: 10/25/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 68fe0e7e-351e-4222-853a-877475adb589
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bf22bbf8b0660f598f65cf73d0035e6223a52d1d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703649"
---
# <a name="communications-between-endpoints-in-configuration-manager"></a>Comunicazioni tra gli endpoint in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Questo articolo illustra le modalità di comunicazione tra i componenti e i sistemi del sito di Configuration Manager in una rete. Include le sezioni seguenti:  

- [Comunicazioni tra sistemi del sito in un sito](#Planning_Intra-site_Com)  
    - [Dal server del sito al punto di distribuzione](#bkmk_site2dp)  

- [Comunicazioni da client a sistemi e servizi del sito](#Planning_Client_to_Site_System)  
    - [Comunicazioni tra client e punti di gestione](#bkmk_client2mp)  
    - [Comunicazioni tra client e punti di distribuzione](#bkmk_client2dp)  
    - [Considerazioni per le comunicazioni client da Internet o da una foresta non attendibile](#BKMK_clientspan)  
    - [Informazioni sui sistemi del sito con connessione Internet](#bkmk_internetfacing)  

- [Comunicazioni tra foreste Active Directory](#Plan_Com_X-Forest)  
    - [Supportare i computer di dominio in una foresta considerata non attendibile dalla foresta del server del sito](#bkmk_noforesttrust)  
    - [Supportare i computer in un gruppo di lavoro](#bkmk_workgroup)  
    - [Scenari di supporto di un sito o una gerarchia che si estende su più domini e foreste](#bkmk_span)  



##  <a name="communications-between-site-systems-in-a-site"></a><a name="Planning_Intra-site_Com"></a> Comunicazioni tra sistemi del sito in un sito  

 Quando i sistemi o componenti del sito di Configuration Manager comunicano in rete con altri sistemi del sito o componenti nel sito, usano uno dei protocolli seguenti, a seconda della configurazione del sito:  

-   Server Message Block (SMB)  

-   HTTP  

-   HTTPS  

Con l'eccezione della comunicazione dal server del sito a un punto di distribuzione, le comunicazioni tra server in un sito possono verificarsi in qualsiasi momento. Queste comunicazioni non usano meccanismi per controllare la larghezza di banda di rete. Poiché non è possibile controllare la comunicazione tra sistemi del sito, assicurarsi di installare i server del sistema del sito in posizioni che dispongono di reti veloci e ben connesse.  


### <a name="site-server-to-distribution-point"></a><a name="bkmk_site2dp"></a> Dal server del sito al punto di distribuzione 

Per gestire il trasferimento di contenuto dal server del sito ai punti di distribuzione, adottare le strategie seguenti:  

-   Configurare il punto di distribuzione per il controllo della larghezza di banda di rete e la pianificazione. Questi controlli sono simili alle configurazioni usate dagli indirizzi intrasito. Usare questa configurazione invece di installare un altro sito di Configuration Manager quando il trasferimento di contenuti su percorsi di rete remoti è il problema principale a livello di uso della larghezza di banda.  

-   È possibile installare un punto di distribuzione come punto di distribuzione pre-installato. Un punto di distribuzione pre-installato consente di usare contenuto che viene messo manualmente sul server del punto di distribuzione e rimuove il requisito di trasferire i file di contenuto sulla rete.  

Per altre informazioni, vedere [Gestire la larghezza di banda di rete per la gestione dei contenuti](manage-network-bandwidth.md).



##  <a name="communications-from-clients-to-site-systems-and-services"></a><a name="Planning_Client_to_Site_System"></a> Comunicazioni da client a sistemi e servizi del sito  

I client avviano le comunicazioni con i ruoli del sistema del sito, Active Directory Domain Services e servizi online. Per abilitare queste comunicazioni, i firewall devono consentire il traffico di rete tra i client e gli endpoint delle comunicazioni. Per altre informazioni sulle porte e i protocolli usati dai client per la comunicazione con questi endpoint, vedere [Porte usate in Configuration Manager](ports.md).  

Per poter comunicare con un ruolo del sistema del sito, il client usa la posizione del servizio per individuare un ruolo che supporta il protocollo del client (HTTP o HTTPS). Per impostazione predefinita, i client usano il metodo più sicuro a loro disposizione. Per altre informazioni, vedere [Informazioni su come i client trovano i servizi e le risorse del sito](understand-how-clients-find-site-resources-and-services.md).  

Per utilizzare HTTPS, configurare una delle opzioni seguenti:  

- Usare un'infrastruttura a chiave pubblica (PKI) e installare i certificati PKI sui client e sui server. Per informazioni su come usare i certificati, vedere [Requisiti dei certificati PKI per Configuration Manager](../network/pki-certificate-requirements.md).  

- A partire dalla versione 1806, configurare il sito con l'opzione **Usa i certificati generati da Configuration Manager per sistemi del sito HTTP**. Per altre informazioni, vedere [HTTP migliorato](enhanced-http.md).  

Quando si distribuisce un ruolo del sistema del sito che usa Internet Information Services (IIS) e supporta le comunicazioni dai client, è necessario specificare se i client si connettono al sistema del sito tramite HTTP o HTTPS. Se si usa HTTP, è necessario considerare anche le opzioni di firma e crittografia. Per altre informazioni, vedere [Pianificazione di firma e crittografia](../security/plan-for-security.md#BKMK_PlanningForSigningEncryption).  


### <a name="client-to-management-point-communication"></a><a name="bkmk_client2mp"></a> Comunicazioni tra client e punti di gestione

La comunicazione tra un client e un punto di gestione avviene in due fasi: autenticazione (trasporto) e autorizzazione (messaggio). Questo processo varia a seconda dei fattori seguenti: 
- Configurazione del sito: Solo HTTPS, consente HTTP o HTTPS o consente HTTP o HTTPS con il protocollo HTTP avanzato abilitato
- Configurazione del punto di gestione: HTTPS o HTTP
- Identità del dispositivo per gli scenari incentrati sui dispositivi
- Identità dell'utente per gli scenari incentrati sugli utenti

Usare la tabella seguente per comprendere il funzionamento del processo:  

| Tipo di punto di gestione  | Autenticazione client  | Autorizzazione client<br>Identità del dispositivo  | Autorizzazione client<br>Identità utente  |
|----------|---------|---------|---------|
| HTTP     | Anonima<br>Con la modalità HTTP avanzato, il sito verifica il token *user* (utente) o *device* (dispositivo) di Azure AD. | Richiesta della posizione: Anonima<br>Pacchetto client: Anonima<br>Registrazione con uno dei metodi seguenti per dimostrare l'identità del dispositivo:<br> - Anonima (approvazione manuale)<br> - Autenticazione integrata Windows<br> - Token *device* di Azure AD (HTTP avanzato)<br>Dopo la registrazione il client usa la firma del messaggio per dimostrare l'identità del dispositivo | Per gli scenari incentrati sull'utente, registrazione con uno dei metodi seguenti per dimostrare l'identità dell'utente:<br> - Autenticazione integrata Windows<br> - Token *user* di Azure AD (HTTP avanzato) |
| HTTPS    | Mediante uno dei metodi seguenti:<br> - Certificato PKI<br> - Autenticazione integrata Windows<br> - Token *user* o *device* di Azure AD | Richiesta della posizione: Anonima<br>Pacchetto client: Anonima<br>Registrazione con uno dei metodi seguenti per dimostrare l'identità del dispositivo:<br> - Anonima (approvazione manuale)<br> - Autenticazione integrata Windows<br> - Certificato PKI<br> - Token *user* o *device* di Azure AD<br>Dopo la registrazione il client usa la firma del messaggio per dimostrare l'identità del dispositivo | Per gli scenari incentrati sull'utente, registrazione con uno dei metodi seguenti per dimostrare l'identità dell'utente:<br> - Autenticazione integrata Windows<br> - Token *user* di Azure AD |

> [!Tip]  
> Per altre informazioni sulla configurazione del punto di gestione per i diversi tipi di identità del dispositivo e con il Cloud Management Gateway, vedere [Abilitare i punti di gestione per HTTPS](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_mphttps).  


### <a name="client-to-distribution-point-communication"></a><a name="bkmk_client2dp"></a> Comunicazioni tra client e punti di distribuzione

Quando un client comunica con un punto di distribuzione, deve solo eseguire l'autenticazione prima di scaricare il contenuto. Usare la tabella seguente per comprendere il funzionamento del processo:


| Tipo punto di distribuzione  | Autenticazione client  |
|----------|---------|
| HTTP     | - Anonima, se consentita<br>- Autenticazione integrata Windows con account del computer o account di accesso alla rete<br> - Token di accesso al contenuto (HTTP avanzato) |
| HTTPS    | - Certificato PKI<br> - Autenticazione integrata Windows con account del computer o account di accesso alla rete<br> - Token di accesso al contenuto |


###  <a name="considerations-for-client-communications-from-the-internet-or-an-untrusted-forest"></a><a name="BKMK_clientspan"></a> Considerazioni per le comunicazioni client da Internet o da una foresta non attendibile  

I seguenti ruoli del sistema del sito installati nei siti primari supportano connessioni da client che si trovano in percorsi non attendibili, come Internet o una foresta non attendibile. I siti secondari non supportano le connessioni client da percorsi non attendibili. 

-   Punto per siti Web del catalogo applicazioni  

-   Modulo criteri di Configuration Manager (NDES) 

-   Punto di distribuzione   

-   Punto di distribuzione basato sul cloud (richiede HTTPS)

-   Punto proxy di registrazione  

-   Punto di stato di fallback  

-   Punto di gestione  

-   Punto di aggiornamento software  

-   Gateway di gestione cloud (richiede HTTPS)


### <a name="about-internet-facing-site-systems"></a><a name="bkmk_internetfacing"></a> Informazioni sui sistemi del sito con connessione a Internet

> [!Note]  
> La sezione seguente riguarda gli scenari di gestione di client basata su Internet. Non è applicabile agli scenari di gateway di gestione cloud. Per altre informazioni, vedere [Gestire i client su Internet](../../clients/manage/manage-clients-internet.md).  

Non è necessario che esista l'attendibilità reciproca tra la foresta del client e quella del server del sistema del sito. Quando la foresta che contiene il sistema del sito con connessione Internet considera attendibile la foresta che contiene gli account utente, tuttavia, questa configurazione supporta criteri basati sull'utente per i dispositivi su Internet se si abilita l'impostazione client **Abilitare le richieste dei criteri utente dai client Internet** di **Criteri client**.  

Ad esempio, le configurazioni seguenti illustrano quando la gestione client basata su Internet supporta criteri utente per i dispositivi su Internet:  

-   Il punto di gestione basato su Internet si trova nella rete perimetrale in cui risiede un controller di dominio di sola lettura per autenticare l'utente e un firewall consente il passaggio dei pacchetti di Active Directory.  

-   L'account utente si trova nella Foresta A (intranet) e il punto di gestione basato su Internet si trova nella Foresta B (la rete perimetrale). La Foresta B considera attendibile la Foresta A e un firewall consente i pacchetti di autenticazione.  

-   L'account utente e il punto di gestione basato su Internet si trovano nella Foresta A (intranet). Il punto di gestione viene pubblicato su Internet usando un server Web proxy, ad esempio Forefront Threat Management Gateway.  

> [!NOTE]  
>  Se l'autenticazione Kerberos ha esito negativo, sarà automaticamente tentata l'autenticazione NTLM.  

Come visualizzato nell'esempio precedente, è possibile posizionare i sistemi del sito basati su Internet nell'intranet quando vengono pubblicati su Internet usando un server Web proxy. Questi sistemi del sito possono essere configurati per connessioni client solo da Internet o per connessioni client da Internet e dall'intranet. Quando si usa un server Web proxy, è possibile configurarlo per il bridging Secure Sockets Layer (SSL) a SSL (più sicuro) o tunneling SSL, come segue:  

-   **Bridging SSL a SSL:**    
    La configurazione consigliata quando si usano server Web proxy per la gestione client basata su Internet è il bridging da SSL a SSL, che usa la terminazione SSL con l'autenticazione. I computer client devono essere autenticati usando l'autenticazione computer e i client legacy di dispositivi mobili vengono autenticati usando l'autenticazione utente. I dispositivi mobili che vengono registrati da Configuration Manager non supportano il bridging SSL.  

     Il vantaggio della terminazione SSL sul server Web proxy è che i pacchetti provenienti da Internet sono sottoposti a verifica prima di essere inoltrati alla rete interna. Il server Web proxy autentica la connessione dal client, la termina, quindi apre una nuova connessione autenticata ai sistemi del sito basati su Internet. Quando i client di Configuration Manager usano un server Web proxy, l'identità client (GUID client) viene inclusa in modo protetto nel payload dei pacchetti, in modo che il punto di gestione non consideri il server Web proxy come il client. Il bridging da HTTP a HTTPS o da HTTPS a HTTP non è supportato in Configuration Manager.  

-   **Tunneling**:   
    Se il server Web proxy non supporta i requisiti per il bridging SSL o se si vuole configurare il supporto Internet per i dispositivi mobili registrati da Configuration Manager, è supportato anche il tunneling SSL. Si tratta di un'opzione meno sicura, perché i pacchetti SSL provenienti da Internet vengono inoltrati ai sistemi del sito senza terminazione SSL e pertanto non possono essere verificati per l'eventuale presenza di contenuto dannoso. Quando si usa il tunneling SSL, non sono previsti requisiti di certificato per il server Web proxy.  



##  <a name="communications-across-active-directory-forests"></a><a name="Plan_Com_X-Forest"></a> Comunicazioni tra foreste Active Directory  

Configuration Manager supporta siti e gerarchie che si estendono su foreste Active Directory. Supporta anche computer del dominio che non si trovano nella stessa foresta Active Directory del server del sito e computer che appartengono a gruppi di lavoro.  


### <a name="support-domain-computers-in-a-forest-thats-not-trusted-by-your-site-servers-forest"></a><a name="bkmk_noforesttrust"></a> Supportare i computer di dominio in una foresta considerata non attendibile dalla foresta del server del sito 

-   Installare i ruoli del sistema del sito in tale foresta non trusted, con la possibilità di pubblicare le informazioni sul sito in tale foresta di Active Directory  

-   Gestire questi computer come computer di un gruppo di lavoro  

Quando si installano i server del sistema del sito in una foresta Active Directory non trusted, la comunicazione tra client e server eseguita dai client della foresta viene mantenuta all'interno di tale foresta e Configuration Manager può autenticare il computer con Kerberos. Quando vengono pubblicate le informazioni del sito sulla foresta del client, i client possono recuperare le informazioni del sito, come ad esempio un elenco di punti di gestione disponibili, dalla relativa foresta Active Directory invece di scaricarle dal punto di gestione assegnato.  

> [!NOTE]  
>  Se si vuole gestire i dispositivi su Internet, è possibile installare ruoli del sistema del sito basati su Internet nella rete perimetrale quando i server del sistema del sito si trovano nella foresta Active Directory. In questo scenario non è richiesto un trust bidirezionale tra la rete perimetrale e la foresta del server del sito.  


### <a name="support-computers-in-a-workgroup"></a><a name="bkmk_workgroup"></a> Supportare i computer in un gruppo di lavoro  

-   Approvare manualmente i computer del gruppo di lavoro quando questi usano connessioni client HTTP ai ruoli del sistema del sito. Configuration Manager non può autenticare questi computer usando Kerberos.  

-   Configurare i client dei gruppi di lavoro per l'uso dell'Account di accesso alla rete in modo che questi computer possano recuperare il contenuto dai punti di distribuzione.  

-   Fornire ai client del gruppo di lavoro un meccanismo alternativo per trovare i punti di gestione. Usare la pubblicazione DNS, WINS oppure assegnare direttamente un punto di gestione. Questi client non possono recuperare le informazioni del sito da Active Directory Domain Services.  

Per altre informazioni, vedere gli articoli seguenti:  

-   [Gestire i record in conflitto](../../clients/manage/manage-clients.md#BKMK_ConflictingRecords)  

-   [Account di accesso alla rete](fundamental-concepts-for-content-management.md#accounts-used-for-content-management)  

-   [Come installare i client di Configuration Manager sui computer del gruppo di lavoro](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientWorkgroup)  


###  <a name="scenarios-to-support-a-site-or-hierarchy-that-spans-multiple-domains-and-forests"></a><a name="bkmk_span"></a> Scenari di supporto di un sito o una gerarchia che si estende su più domini e foreste  

#### <a name="scenario-1-communication-between-sites-in-a-hierarchy-that-spans-forests"></a>Scenario 1: Comunicazione tra siti in una gerarchia che si estende su più foreste  
Questo scenario richiede un trust tra foreste bidirezionale che supporti l'autenticazione Kerberos.  Se non è presente un trust tra foreste bidirezionale che supporta l'autenticazione Kerberos, Configuration Manager non supporterà il sito figlio nella foresta remota.  

Configuration Manager supporta l'installazione di un sito figlio in una foresta remota che dispone del trust bidirezionale richiesto con la foresta del sito padre. Ad esempio, è possibile inserire un sito secondario in una foresta diversa da quella del sito primario padre a condizione che sia presente il trust necessario.  

> [!NOTE]  
>  Un sito figlio può essere un sito primario (dove il sito di amministrazione centrale è il sito padre) o un sito secondario.  

La comunicazione tra siti in Configuration Manager usa la replica di database e i trasferimenti basati su file. Quando si installa un sito, è necessario specificare un account da usare per l'installazione del sito nel server designato. Inoltre, questo account stabilisce e mantiene la comunicazione tra siti. Dopo che il sito è stato installato correttamente e i trasferimenti basati su file e la replica di database sono stati avviati, non sarà necessario eseguire altre configurazioni per la comunicazione con il sito.  

In presenza di un trust tra foreste bidirezionale, Configuration Manager non richiede altri passaggi di configurazione.  

Per impostazione predefinita, quando si installa un nuovo sito figlio Configuration Manager configura gli elementi seguenti:  

-   Una route di replica basata su file tra siti per ogni sito che usa l'account computer del server del sito. Configuration Manager aggiunge l'account computer di ciascun computer al gruppo **SMS_SiteToSiteConnection_&lt;sitecode\>** nel computer di destinazione.  

-   Replica di database tra i server SQL in ogni sito.  

Vengono impostate anche le configurazioni seguenti:  

-   I firewall e i dispositivi di rete interessati devono consentire i pacchetti di rete richiesti da Configuration Manager.  

-   La risoluzione dei nomi deve funzionare tra le foreste.  

-   Per installare un sito o un ruolo del sistema del sito, è necessario specificare un account con autorizzazioni di amministratore locale sul computer specificato.  

#### <a name="scenario-2-communication-in-a-site-that-spans-forests"></a>Scenario 2: Comunicazione in un sito che si estende su più foreste  
Questo scenario non richiede un trust tra foreste bidirezionale.  

I siti primari supportano l'installazione dei ruoli del sistema del sito su computer in foreste remote.  

-   Il punto per servizi Web del Catalogo applicazioni è l'unica eccezione.  È supportato solo nella stessa foresta del server del sito.  

-   Quando un ruolo del sistema del sito accetta connessioni da Internet, la procedura ottimale di protezione prevede l'installazione dei ruoli del sistema del sito in una posizione in cui i limiti della foresta garantiscono la protezione per il server del sito, ad esempio in una rete perimetrale.  

Per installare un ruolo del sistema del sito in un computer in una foresta non trusted:  

- Specificare un **account di installazione del sistema del sito**, che il sito usa per installare il ruolo del sistema del sito. L'account deve disporre delle credenziali di amministratore locale per la connessione. Installare quindi i ruoli del sistema del sito nel computer specificato.  

- Selezionare l'opzione del sistema del sito **Richiedi al server del sito di avviare le connessioni al sistema del sito**. Questa impostazione richiede al server del sito di stabilire connessioni al server del sistema del sito per il trasferimento di dati. Questa configurazione evita che il computer nella posizione non attendibile avvii un contatto con il server del sito all'interno della rete attendibile. Queste connessioni usano l' **account di installazione del sistema del sito**.  

Per usare un ruolo del sistema del sito installato in una foresta non attendibile, i firewall devono consentire il traffico di rete anche quando il server del sito avvia il trasferimento dei dati.  

Inoltre, i seguenti ruoli del sistema del sito richiedono l'accesso diretto al database del sito. È quindi necessario che i firewall consentano il traffico applicabile dalla foresta non trusted a SQL Server dei siti:  

-   Punto di sincronizzazione di Asset Intelligence  

-   Punto di Endpoint Protection  

-   Punto di registrazione  

-   Punto di gestione  

-   Punto di Reporting Services  

-   Punto di migrazione stato  

Per altre informazioni, vedere [Porte usate in Configuration Manager](ports.md).  

Può essere necessario configurare l'accesso del punto di registrazione e del punto di gestione al database del sito.

-   Per impostazione predefinita, quando si installano questi ruoli, Configuration Manager configura l'account computer del nuovo server del sistema del sito come account di connessione per il ruolo del sistema del sito. Quindi aggiunge l'account al ruolo del database SQL Server appropriato.  

-   Quando si installano questi ruoli del sistema del sito in un dominio non attendibile, configurare l'account di connessione del ruolo del sistema del sito in modo da abilitarlo alla ricezione delle informazioni dal database.  

Se si configura un account utente di dominio come account di connessione per questi ruoli del sistema del sito, assicurarsi che l'account utente di dominio abbia l'accesso appropriato al database di SQL Server in quel sito:  

-   Punto di gestione: **account connessione di database punto di gestione**  

-   Punto di registrazione: **account di connessione al punto di registrazione**  

Considerare le seguenti informazioni aggiuntive per la pianificazione di ruoli del sistema del sito in altre foreste:  

-   Se si esegue Windows Firewall, configurare i profili firewall applicabili per consentire il passaggio delle comunicazioni tra il server di database del sito e i computer installati con i ruoli del sistema del sito remoto.   

-   Quando il punto di gestione basato su Internet considera attendibile la foresta che contiene gli account utente, vengono supportati i criteri utente. In caso contrario, sono supportati solo i criteri computer.  

#### <a name="scenario-3-communication-between-clients-and-site-system-roles-when-the-clients-arent-in-the-same-active-directory-forest-as-their-site-server"></a>Scenario 3: Comunicazione tra client e ruoli del sistema del sito quando i client non si trovano nella stessa foresta Active Directory del relativo server del sito  
Configuration Manager supporta i seguenti scenari per i client che non si trovano nella stessa foresta del relativo server del sito:  

-   È presente un trust tra foreste bidirezionale tra la foresta del client e la foresta del server del sito.  

-   Il server del ruolo del sistema del sito si trova nella stessa foresta del client.  

-   Il client si trova in un computer di dominio che non dispone di un trust tra foreste bidirezionale con il server del sito e i ruoli del sistema del sito non sono installati nella foresta del client.  

-   Il client si trova in un computer del gruppo di lavoro.  

I client in un computer aggiunto a un dominio possono usare Active Directory Domain Services per la posizione del servizio quando il relativo sito è pubblicato nella foresta Active Directory.  

Per pubblicare le informazioni di un sito in un'altra foresta Active Directory:  

-   Specificare la foresta, quindi abilitare la pubblicazione in tale foresta nel nodo **Foreste Active Directory** dell'area di lavoro **Amministrazione** .  

-   Configurare ogni sito per la pubblicazione dei relativi dati in Servizi di dominio Active Directory. Questa configurazione consente ai client di tale foresta di recuperare le informazioni del sito e trovare punti di gestione. Per i client che non possono usare Active Directory Domain Services per la posizione del servizio è possibile usare DNS, WINS o il punto di gestione client assegnato.  


####  <a name="scenario-4-put-the-exchange-server-connector-in-a-remote-forest"></a><a name="bkmk_xchange"></a> Scenario 4: Inserire il connettore Exchange Server in una foresta remota  

Per il supporto di questo scenario, assicurarsi che la risoluzione dei nomi funzioni correttamente tra le foreste. Ad esempio, configurare gli inoltri DNS. Quando si configura il connettore Exchange Server, specificare il FQDN intranet di Exchange Server. Per altre informazioni, vedere [Gestire i dispositivi mobili con Configuration Manager ed Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  



## <a name="see-also"></a>Vedere anche

- [Pianificare la sicurezza](../security/plan-for-security.md)  

- [Sicurezza e privacy per i client di Configuration Manager](../../clients/deploy/plan/security-and-privacy-for-clients.md)  

