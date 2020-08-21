---
title: Pianificare la sicurezza
titleSuffix: Configuration Manager
description: Procedure consigliate e altre informazioni sulla sicurezza in Configuration Manager.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2a216814-ca8c-4d2e-bcef-dc00966a3c9f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0cdb14d282cbfa93655d6678b12b5f0837a225aa
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699280"
---
# <a name="plan-for-security-in-configuration-manager"></a>Pianificare la sicurezza in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Questo articolo descrive i concetti da tenere in considerazione durante la pianificazione della sicurezza nell'implementazione di Configuration Manager. Include le sezioni seguenti:  

- [Pianificare i certificati (autofirmati e PKI)](#BKMK_PlanningForCertificates)  
  - [Certificati CNG (Cryptography: Next Generation)](#bkmk_plan-cng)  
  - [HTTP avanzato](#bkmk_plan-ehttp)  
  - [Certificati per CMG e CDP](#bkmk_plan-cmgcdp)  
  - [Certificato di firma del server del sito (autofirmato)](#bkmk_plansitesign)  
  - [Revoca di certificati PKI](#BKMK_PlanningForCRLs)  
  - [Certificati radice trusted PKI e autorità di certificazione](#BKMK_PlanningForRootCAs)  
  - [Selezione del certificato client PKI](#BKMK_PlanningForClientCertificateSelection)  
  - [Strategia di transizione per certificati PKI e gestione client basata su Internet](#BKMK_PlanningForPKITransition)  

- [Pianificare la chiave radice attendibile](#BKMK_PlanningForRTK)  

- [Pianificare firma e crittografia](#BKMK_PlanningForSigningEncryption)  

- [Pianificare l'amministrazione basata su ruoli](#BKMK_PlanningForRBA)  

- [Pianificare Azure Active Directory](#bkmk_planazuread)  

- [Pianificare l'autenticazione del provider SMS](#bkmk_auth)



##  <a name="plan-for-certificates-self-signed-and-pki"></a><a name="BKMK_PlanningForCertificates"></a> Pianificare certificati (autofirmati e PKI)  

Configuration Manager usa una combinazione di certificati autofirmati e certificati di infrastruttura a chiave pubblica (PKI).  

Usare i certificati PKI quando possibile. Per altre informazioni, vedere [requisiti dei certificati PKI](../network/pki-certificate-requirements.md). Quando Configuration Manager richiede i certificati PKI durante la registrazione di dispositivi mobili, è necessario usare Active Directory Domain Services e un'autorità di certificazione globale (enterprise). Tutti gli altri certificati PKI possono essere distribuiti e gestiti indipendentemente da Configuration Manager. 

I certificati PKI sono obbligatori quando i computer client si connettono a sistemi del sito basati su internet. Anche alcuni scenari con gateway di gestione cloud e punto di distribuzione cloud richiedono l'uso di certificati PKI. Per altre informazioni, vedere [Gestire i client su Internet](../../clients/manage/manage-clients-internet.md).

Quando si usa una PKI, è possibile usare anche IPsec per proteggere la comunicazione da server a server tra sistemi in un sito, tra siti e per altri trasferimenti dati tra computer. L'implementazione di IPsec è indipendente da Configuration Manager.  

Quando i certificati PKI non sono disponibili, Configuration Manager genera automaticamente certificati autofirmati. Alcuni certificati in Configuration Manager sono sempre autofirmati. Nella maggior parte dei casi, Configuration Manager gestisce automaticamente i certificati autofirmati e non sono necessarie azioni aggiuntive. Un esempio è il certificato di firma del server del sito. Questo certificato è sempre autofirmato. Garantisce che i criteri che i client scaricano dal punto di gestione siano stati inviati dal server del sito e non siano stati manomessi.  


### <a name="cryptography-next-generation-cng-certificates"></a><a name="bkmk_plan-cng"></a> Certificati CNG (Cryptography: Next Generation)  

Configuration Manager supporta i certificati CNG (Cryptography: Next Generation). I client di Configuration Manager possono usare certificati di autenticazione client con chiave privata nel provider di archiviazione chiavi (KSP) CNG. Con il supporto per i provider di archiviazione chiavi, i client di Configuration Manager supportano chiavi private basate sull'hardware, ad esempio TPM KSP per i certificati di autenticazione client PKI. Per altre informazioni, vedere [Panoramica dei certificati CNG](../network/cng-certificates-overview.md).


### <a name="enhanced-http"></a><a name="bkmk_plan-ehttp"></a> HTTP avanzato  

L'uso di comunicazioni HTTPS è consigliato per tutti i percorsi di comunicazione di Configuration Manager, ma risulta difficile per alcuni clienti a causa del sovraccarico di lavoro derivante dalla gestione dei certificati PKI. L'introduzione dell'integrazione di Azure Active Directory (Azure AD) riduce alcuni ma non tutti i requisiti per i certificati. A partire dalla versione 1806 si può consentire al sito di usare la funzionalità **HTTP avanzato**. Questa configurazione supporta HTTPS nei sistemi del sito tramite una combinazione di certificati autofirmati e Azure AD. Non sono necessari certificati PKI. Per altre informazioni, vedere [Enhanced HTTP](../hierarchy/enhanced-http.md) (HTTP avanzato).  


### <a name="certificates-for-cmg-and-cdp"></a><a name="bkmk_plan-cmgcdp"></a> Certificati per CMG e CDP

La gestione dei client in Internet tramite il gateway di gestione cloud (CMG) e il punto di distribuzione cloud (CDP) richiede l'uso di certificati. Il numero e il tipo di certificati variano a seconda degli scenari specifici. Per altre informazioni, vedere gli articoli seguenti:
- [Certificati per il gateway di gestione cloud](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md)  
- [Certificati per il punto di distribuzione cloud](../hierarchy/use-a-cloud-based-distribution-point.md#bkmk_certs)  


### <a name="plan-for-the-site-server-signing-certificate-self-signed"></a><a name="bkmk_plansitesign"></a> Pianificare il certificato di firma del server del sito (autofirmato)  

I client possono ottenere in modo sicuro una copia del certificato di firma del server del sito da Active Directory Domain Services e dall'installazione push client. Se i client non riescono a ottenere una copia del certificato tramite uno di questi meccanismi, installarlo durante l'installazione del client. Questo processo è particolarmente importante se la prima comunicazione del client con il sito avviene in un punto di gestione basato su Internet. Dal momento che questo server è connesso a una rete non attendibile, esso risulta più vulnerabile agli attacchi. Se non si adotta questa misura aggiuntiva, i client scaricano automaticamente una copia del certificato di firma del server del sito dal punto di gestione.  

I client non riescono a ottenere in modo sicuro una copia del certificato del server del sito negli scenari seguenti:  

- Il client non viene installato tramite installazione push client e:  

  - Lo schema di Active Directory non è stato esteso a Configuration Manager.  

  - Il sito del client non è stato pubblicato in Active Directory Domain Services.  

  - Il client deriva da un gruppo di lavoro o una foresta non trusted.  

- È in uso la gestione client basata su Internet e il client viene installato quando è in Internet.  

#### <a name="to-install-clients-with-a-copy-of-the-site-server-signing-certificate"></a>Per installare i client con una copia del certificato di firma del server del sito  

1.  Individuare il certificato di firma del server del sito nel server del sito primario. Il certificato si trova nell'archivio certificati **SMS** di Windows. Il Nome soggetto è **Server del sito** e il nome descrittivo è **Certificato di firma del server del sito**.  

2.  Esportare il certificato senza la chiave privata, archiviare il file in modo sicuro e accedervi solo da un canale protetto.  

3.  Installare il client usando la proprietà client.msi seguente: `SMSSIGNCERT=<full path and file name>`  


###  <a name="plan-for-pki-certificate-revocation"></a><a name="BKMK_PlanningForCRLs"></a> Pianificare revoche di certificati PKI  

Quando si usano i certificati PKI con Configuration Manager, pianificare l'uso di un elenco di revoche di certificati (CRL). I dispositivi usano l'elenco di revoche di certificati per verificare il certificato presente nel computer che si connette. L'elenco di revoche di certificati è un file creato e firmato da un'autorità di certificazione. Contiene un elenco di certificati rilasciati dall'autorità di certificazione, ma revocati. Quando un amministratore revoca i certificati, la relativa identificazione personale viene aggiunta all'elenco di revoche di certificati. Ad esempio, in caso di sospetta o accertata compromissione di un certificato rilasciato.

> [!IMPORTANT]  
> Poiché il percorso dell'elenco di revoche di certificati viene aggiunto al certificato al momento del rilascio da parte di un'autorità di certificazione, assicurarsi di pianificare l'uso di questo elenco prima di distribuire qualsiasi certificato PKI usato da Configuration Manager.  

IIS verifica sempre la presenza dei certificati client nell'elenco di revoche di certificati e questa configurazione non può essere modificata in Configuration Manager. Per impostazione predefinita, i client Configuration Manager cercano sempre i sistemi del sito nell'elenco CRL. Disabilitare questa impostazione specificando una proprietà del sito e una proprietà CCMSetup.  

I computer che usano il controllo della revoca del certificato, ma non riescono a individuare l'elenco di revoche di certificati, si comportano come se tutti i certificati nella catena di certificazione fossero revocati. Questo comportamento è dovuto al fatto che questi computer non possono verificare se i certificati sono inclusi nell'elenco di revoche di certificati. In questo scenario, non è possibile stabilire alcuna connessione che richieda certificati e includa il controllo dell'elenco di revoche di certificati. Quando si verifica l'accessibilità dell'elenco di revoche di certificati passando al relativo percorso HTTP, è importante notare che il client di Configuration Manager viene eseguito come sistema locale. Pertanto, il test di accessibilità dell'elenco di revoche di certificati con un Web browser in esecuzione nel contesto utente può avere esito positivo, ma l'account del computer può essere bloccato durante il tentativo di stabilire una connessione HTTP allo stesso URL dell'elenco di revoche di certificati a causa di una soluzione di filtro Web interna. In una situazione di questo tipo può essere necessario includere l'URL dell'elenco di revoche di certificati nell'elenco elementi consentiti delle soluzioni di filtro Web.

Il controllo dell'elenco di revoche di certificati ogni volta che viene usato un certificato offre maggiore protezione dall'uso di un certificato che è stato revocato, anche se introduce un ritardo nella connessione e un'elaborazione aggiuntiva nel client. L'organizzazione può richiedere questo controllo di sicurezza aggiuntivo per i client in Internet o in una rete non attendibile.  

Consultare gli amministratori PKI prima di decidere se i client di Configuration Manager devono controllare l'elenco di revoche di certificati. Quindi valutare la possibilità di tenere questa opzione abilitata in Configuration Manager quando vengono soddisfatte entrambe le condizioni seguenti:  

- L'infrastruttura PKI supporta un elenco di revoche di certificati che è pubblicato in una posizione in cui tutti i client di Configuration Manager possono individuarlo. Questi client possono includere dispositivi in Internet e in foreste non attendibili.  

- Il requisito relativo al controllo dell'elenco di revoche di certificati per ogni connessione a un sistema del sito configurata per l'uso di un certificato PKI è più importante rispetto ai requisiti seguenti:  
  - Connessioni più veloci  
  - Elaborazione efficiente nel client  
  - Rischio che i client non possano connettersi ai server se non è possibile individuare l'elenco di revoche di certificati  


###  <a name="plan-for-the-pki-trusted-root-certificates-and-the-certificate-issuers-list"></a><a name="BKMK_PlanningForRootCAs"></a> Pianificare certificati radice trusted PKI e l'elenco di autorità di certificazione  

Se i sistemi del sito IIS usano certificati client PKI per l'autenticazione dei client su HTTP o per l'autenticazione e la crittografia dei client su HTTPS, potrebbe essere necessario importare i certificati CA radice come proprietà del sito. Ecco i due scenari:  

- I sistemi operativi sono distribuiti tramite Configuration Manager e i punti di gestione accettano solo connessioni client HTTPS.  

- Si usano certificati client PKI non concatenati a un certificato radice considerato attendibile dai punti di gestione.  

  > [!NOTE]  
  > Quando i certificati client PKI vengono rilasciati dalla stessa gerarchia di CA che rilascia i certificati del server usati per i punti di gestione, non è necessario specificare questo certificato CA radice. Tuttavia, se si usano più gerarchie di CA e non si è certi che queste si considerino reciprocamente attendibili, importare la CA radice per la gerarchia di CA dei client.  

Se è necessario importare certificati CA radice per Configuration Manager, esportarli dalla CA emittente o dal computer client. Se si esporta il certificato dalla CA emittente che corrisponde anche alla CA radice, assicurarsi di non esportare la chiave privata. Archiviare il file del certificato esportato in una posizione sicura per impedire eventuali manomissioni. Al momento della configurazione del sito sarà necessario l'accesso al file. In caso di accesso dalla rete, accertarsi che la comunicazione sia protetta da eventuali manomissioni usando IPsec.  

Se un certificato CA radice importato viene rinnovato, è necessario importare il certificato rinnovato.  

Questi certificati CA radice importati e il certificato CA radice di ogni punto di gestione creano l'elenco di autorità emittenti di certificati usato dai computer di Configuration Manager nei modi seguenti:  

- Quando i client si connettono a un punto di gestione, quest'ultimo verifica che il certificato client sia concatenato a un certificato radice attendibile incluso nell'elenco di autorità emittenti di certificati del sito. Se non lo è, il certificato viene rifiutato e la connessione PKI non riesce.  

- In presenza di un elenco di autorità emittenti di certificati, i client selezionano un certificato PKI concatenato a un certificato radice trusted presente nell'elenco. In assenza di una corrispondenza, il client non seleziona un certificato PKI. Per altre informazioni, vedere [Pianificare la selezione del certificato client PKI](#BKMK_PlanningForClientCertificateSelection).  


###  <a name="plan-for-pki-client-certificate-selection"></a><a name="BKMK_PlanningForClientCertificateSelection"></a> Pianificare la selezione del certificato client PKI  

Se i sistemi del sito IIS usano certificati client PKI per l'autenticazione dei client su HTTP o per l'autenticazione e la crittografia dei client su HTTPS, pianificare la modalità con cui i client Windows selezionano il certificato da usare per Configuration Manager.  

> [!NOTE]  
> Alcuni dispositivi non supportano un metodo di selezione del certificato, ma selezionano automaticamente il primo certificato che soddisfa i requisiti. Ad esempio, i client su computer Mac e dispositivi mobili non supportano un metodo di selezione del certificato.  

In molti casi, la configurazione e il comportamento predefiniti sono sufficienti. Il client Configuration Manager su computer Windows filtra più certificati usando questi criteri nell'ordine indicato:  

1.  L'elenco di autorità emittenti di certificati: il certificato si concatena a una CA radice considerata attendibile dal punto di gestione.  

2.  Il certificato si trova nell'archivio certificati predefinito **Personale**.  

3.  Il certificato è valido, non revocato e non è scaduto. La convalida verifica anche che la chiave privata sia accessibile.  

4.  Il certificato ha funzionalità di autenticazione client.

5.  Il nome del soggetto del certificato contiene il nome del computer locale come sottostringa.  

6.  Il certificato ha il periodo di validità più lungo.  

Configurare i client per l'uso dell'elenco di autorità di certificazione usando i meccanismi seguenti:  

- Pubblicarlo con le informazioni del sito di Configuration Manager in Active Directory Domain Services.  

- Installare i client tramite installazione push client.  

- I client lo scaricano dal punto di gestione dopo essere stati correttamente assegnati al rispettivo sito.  

- Specificarlo durante l'installazione del client come proprietà client.msi CCMSetup di CCMCERTISSUERS.  

I client che al momento dell'installazione iniziale sono privi dell'elenco di autorità di certificazione e che non sono ancora assegnati al sito, saltano questo controllo. Quando i client hanno l'elenco di autorità di certificazione e non hanno un certificato PKI concatenato a un certificato radice trusted nell'elenco di autorità di certificazione, la selezione del certificato non riesce. I client non proseguono con gli altri criteri di selezione del certificato.  

Nella maggior parte dei casi, il client Configuration Manager identifica correttamente un certificato PKI univoco e appropriato. Tuttavia, in assenza di questo comportamento, anziché selezionare il certificato sulla base della funzionalità di autenticazione client, è possibile configurare due metodi di selezione alternativi:  

- Una corrispondenza di stringa parziale nel nome soggetto del certificato client. Questo metodo è una corrispondenza senza distinzione tra maiuscole e minuscole. È appropriato se si usa il nome di dominio completo (FQDN) di un computer nel campo del soggetto e si vuole che la selezione del certificato si basi sul suffisso del dominio, ad esempio **contoso.com**. È tuttavia possibile usare questo metodo di selezione per identificare qualsiasi stringa di caratteri sequenziali nel nome soggetto del certificato che lo differenzi da altri certificati presenti nell'archivio certificati del client.  

  > [!NOTE]
  > Non è consentito usare la corrispondenza di stringa parziale con il nome alternativo del soggetto (SAN) come impostazione del sito. Anche se è possibile specificare una corrispondenza di stringa parziale per il SAN usando CCMSetup, essa verrà sovrascritta dalle proprietà del sito negli scenari seguenti:  
  > 
  > - I client recuperano le informazioni del sito pubblicate in Active Directory Domain Services.  
  >   - I client vengono installati tramite installazione push client.  
  > 
  >   Usare una corrispondenza di stringa parziale nel SAN solo quando si installano i client manualmente e quando questi non recuperano le informazioni del sito da Active Directory Domain Services. Queste condizioni si applicano, ad esempio, ai client solo Internet.  

- Una corrispondenza nei valori di attributo del nome soggetto del certificato client o nei valori di attributo del nome alternativo del soggetto (SAN). Questo metodo è una corrispondenza con distinzione tra maiuscole e minuscole. È appropriato se si usa un nome distinto X500 o identificatori di oggetto (OID) equivalenti in conformità con RFC 3280 e si vuole che la selezione del certificato si basi sui valori di attributo. È possibile specificare solo gli attributi e i rispettivi valori richiesti per identificare o convalidare in modo univoco il certificato e differenziarlo dagli altri certificati nel relativo archivio.  

Nella tabella seguente vengono illustrati i valori attributo che Configuration Manager supporta per i criteri di selezione del certificato client.  

|Attributo OID|Attributo del nome distinto|Definizione di attributo|  
|-------------------|----------------------------------|--------------------------|  
|0.9.2342.19200300.100.1.25|DC|Componente del dominio|  
|1.2.840.113549.1.9.1|E o E-mail|Indirizzo di posta elettronica|  
|2.5.4.3|CN|Nome comune|  
|2.5.4.4|SN|Nome oggetto|  
|2.5.4.5|SERIALNUMBER|Numero di serie|  
|2.5.4.6|C|Codice paese|  
|2.5.4.7|L|Località|  
|2.5.4.8|S o ST|Nome di provincia o stato|  
|2.5.4.9|STREET|Indirizzo|  
|2.5.4.10|O|Nome organizzazione|  
|2.5.4.11|OU|Unità organizzativa|  
|2.5.4.12|T o Title|Titolo|  
|2.5.4.42|G o GN o GivenName|Nome specificato|  
|2.5.4.43|I o Initials|Iniziali|  
|2.5.29.17|(nessun valore)|Nome alternativo soggetto| 

  > [!NOTE]
  > Se si configura uno dei metodi di selezione dei certificati alternativi sopra indicati, non è necessario che il nome del soggetto del certificato contenga il nome del computer locale.

Se viene individuato più di un certificato appropriato dopo aver applicato i criteri di selezione, è possibile ignorare la configurazione predefinita che prevede la selezione del certificato con il periodo di validità più lungo specificando che nessun certificato è selezionato. In questo scenario, il client non riuscirà a comunicare con i sistemi del sito IIS con un certificato PKI. Il client invia un messaggio di errore al suo punto di stato di fallback assegnato per avvisare circa l'esito negativo della selezione del certificato e consentire la modifica o il perfezionamento dei criteri di selezione del certificato. Il comportamento del client varia a seconda se la connessione non riuscita era su HTTPS o HTTP:  

- Se la connessione non riuscita era su HTTPS: il client prova connettersi su HTTP e usa il certificato autofirmato.  

- Se la connessione non riuscita era su HTTP: il client prova a connettersi di nuovo su HTTP usando il certificato client autofirmato.  

Per identificare un certificato client PKI univoco, è anche possibile specificare un archivio personalizzato diverso dall'archivio predefinito **Personale** in **Computer**. È tuttavia necessario creare questo archivio indipendentemente da Configuration Manager, nonché essere in grado di distribuire i certificati a questo archivio personalizzato e rinnovarli prima della scadenza del periodo di validità.  

Per altre informazioni, vedere [Configurare le impostazioni per i certificati PKI client](configure-security.md#BKMK_ConfigureClientPKI).  


###  <a name="plan-a-transition-strategy-for-pki-certificates-and-internet-based-client-management"></a><a name="BKMK_PlanningForPKITransition"></a> Pianificare una strategia di transizione per certificati PKI e gestione client basata su Internet  

Le opzioni di configurazione flessibile in Configuration Manager consentono di eseguire una transizione graduale dei client e del sito all'uso dei certificati PKI per garantire la sicurezza degli endpoint dei client. I certificati PKI offrono maggiore sicurezza e consentono di gestire i client Internet.  

Dato il numero di opzioni e scelte di configurazione in Configuration Manager, le modalità di transizione di un sito all'uso di connessioni HTTPS da parte di tutti i client sono molteplici. Tuttavia, è possibile attenersi alla seguente procedura come guida:  

1. Installare il sito di Configuration Manager e configurarlo in modo che i sistemi del sito accettino le connessioni client su HTTPS e HTTP.  

2. Configurare la scheda **Comunicazione computer client** nelle proprietà del sito in modo che **Impostazioni sistema del sito** sia **HTTP o HTTPS**, quindi selezionare **Usa certificato client PKI (funzionalità di autenticazione client) quando disponibile**.  Per altre informazioni, vedere [Configurare le impostazioni per i certificati PKI client](configure-security.md#BKMK_ConfigureClientPKI).  

    > [!Note]
    > A partire dalla versione 1906, questa scheda è denominata **Communication Security** (Sicurezza comunicazione).<!-- SCCMDocs#1645 -->  

3. Eseguire il progetto pilota di un'implementazione PKI per i certificati client. Per una distribuzione di esempio, vedere [Distribuire il certificato client per computer Windows](../network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012).  

4. Installare i client usando il metodo di installazione push client. Per altre informazioni, vedere [Come installare i client di Configuration Manager usando push client](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).  

5. Monitorare lo stato e la distribuzione dei client usando i report e le informazioni nella console di Configuration Manager.  

6. Tenere traccia del numero di client che usano un certificato client PKI visualizzando la colonna **Certificato client** nell'area di lavoro **Asset e conformità** , nodo **Dispositivi** .  

    È anche possibile distribuire lo strumento di valutazione della conformità HTTPS di Configuration Manager (**cmHttpsReadiness.exe**) ai computer. Usare quindi i report per vedere quanti computer possono usare un certificato PKI client con Configuration Manager.  

   > [!NOTE]
   >  All'installazione del client di Configuration Manager, lo strumento **CMHttpsReadiness.exe** viene installato nella cartella `%windir%\CCM`. Quando si esegue lo strumento, le opzioni della riga di comando disponibili sono le seguenti:  
   > 
   > - `/Store:<name>`: questa opzione equivale alla proprietà client.msi **CCMCERTSTORE**  
   > - `/Issuers:<list>`: questa opzione equivale alla proprietà client.msi **CCMCERTISSUERS**    
   > - `/Criteria:<criteria>`: questa opzione equivale alla proprietà client.msi **CCMCERTSEL**    
   > - `/SelectFirstCert`: questa opzione equivale alla proprietà client.msi **CCMFIRSTCERT**    
   > 
   >   Per altre informazioni, vedere [Proprietà di installazione client](../../clients/deploy/about-client-installation-properties.md).  

7. Dopo avere appurato che un numero sufficiente di client stia usando correttamente il rispettivo certificato PKI client per l'autenticazione su HTTP, seguire questa procedura:  

   1.  Distribuire un certificato server Web PKI a un server membro che esegue un punto di gestione aggiuntivo per il sito e configurare il certificato in IIS. Per altre informazioni, vedere [Distribuire il certificato del server Web per sistemi del sito che eseguono IIS](../network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012).  

   2.  Installare il ruolo del punto di gestione su questo server e configurare l'opzione **Connessioni client** nelle proprietà del punto di gestione per **HTTPS**.  

8. Monitorare e verificare che i client che dispongono di un certificato PKI utilizzino il nuovo punto di gestione tramite HTTPS. Per verificare si può usare la registrazione IIS o i contatori delle prestazioni.  

9. Riconfigurare altri ruoli del sistema del sito per l'utilizzo di connessioni client HTTPS. Se si vuole gestire i client in Internet, verificare che i sistemi del sito abbiano un nome di dominio completo Internet. Configurare singoli punti di gestione e punti di distribuzione per accettare le connessioni client da Internet.  

    > [!IMPORTANT]  
    > Prima di configurare i ruoli del sistema del sito per accettare connessioni da Internet, vedere le informazioni e i prerequisiti di pianificazione per la gestione client basata su Internet. Per altre informazioni, vedere [Comunicazioni tra gli endpoint](../hierarchy/communications-between-endpoints.md).  

10. Estendere l'implementazione dei certificati PKI a client e sistemi del sito che eseguono IIS. Configurare i ruoli del sistema del sito per le connessioni client HTTPS e le connessioni Internet, in base alle esigenze.  

11. Per la massima protezione: Quando si è certi che tutti i client stanno usando un certificato client PKI per l'autenticazione e la crittografia, modificare le proprietà del sito per l'utilizzo esclusivo di HTTPS.  

    Questo piano introduce prima i certificati PKI solo per l'autenticazione su HTTP e successivamente per l'autenticazione e la crittografia su HTTPS. Adottando questo piano per introdurre gradualmente questi certificati si riduce il rischio di avere client non gestiti e si beneficerà della massima sicurezza supportata da Configuration Manager.  

##  <a name="plan-for-the-trusted-root-key"></a><a name="BKMK_PlanningForRTK"></a> Pianificare la chiave radice attendibile  

La chiave radice attendibile di Configuration Manager offre un meccanismo che consente ai client di Configuration Manager di verificare che i sistemi del sito appartengano alla propria gerarchia. Ogni server del sito genera una chiave di scambio per comunicare con altri siti. La chiave di scambio dal sito di livello superiore nella gerarchia viene chiamata chiave radice attendibile.  

La funzione della chiave radice attendibile in Configuration Manager è simile a quella di un certificato radice in un'infrastruttura a chiave pubblica. Tutto ciò che è firmato dalla chiave privata della chiave radice attendibile è considerato attendibile nei livelli inferiori della gerarchia. I client archiviano una copia della chiave radice attendibile del sito nello spazio dei nomi WMI **root\ccm\locationservices**. 

Ad esempio, il sito rilascia un certificato al punto di gestione firmandolo con la chiave privata della chiave radice attendibile. Il sito condivide con i client la chiave pubblica della chiave radice attendibile. I client possono quindi distinguere i punti di gestione che sono nella propria gerarchia da quelli che non lo sono.   

I client recuperano automaticamente la copia pubblica della chiave radice attendibile tramite due meccanismi:  

- Estendere lo schema di Active Directory per Configuration Manager e pubblicare il sito in Active Directory Domain Services. I client recuperano quindi le informazioni del sito da un server di catalogo globale. Per altre informazioni, vedere [Preparare Active Directory per la pubblicazione di siti](../network/extend-the-active-directory-schema.md).  

- Installare i client tramite il metodo di installazione push client. Per altre informazioni, vedere [Installazione push client](../../clients/deploy/plan/client-installation-methods.md#client-push-installation).  

Se i client non sono in grado di recuperare la chiave radice attendibile tramite uno di questi meccanismi, considereranno attendibile la chiave radice attendibile fornita dal primo punto di gestione con cui è stata stabilita una connessione. In questo scenario, un client potrebbe essere erroneamente indirizzato al punto di gestione di un utente malintenzionato in cui riceverebbe criteri dal punto di gestione non autorizzato. Questa azione richiede un utente malintenzionato esperto. Questo attacco è limitato al breve periodo di tempo che trascorre prima che il client recuperi la chiave radice attendibile da un punto di gestione valido. Per ridurre il rischio di un errato indirizzamento dei client a un punto di gestione non autorizzato, effettuare il pre-provisioning dei client con la chiave radice attendibile.  

Seguire le procedure seguenti per eseguire il pre-provisioning e verificare la chiave radice attendibile per un client di Configuration Manager:  

- [Effettuare il pre-provisioning di un client con la chiave radice attendibile usando un file](#bkmk_trk-provision-file)  

- [Effettuare il pre-provisioning di un client con la chiave radice attendibile senza usare un file](#bkmk_trk-provision-nofile)  

- [Verificare la chiave radice attendibile in un client](#bkmk_trk-verify)  

- [Rimuovere o sostituire la chiave radice attendibile](#bkmk_trk-reset)  

  > [!NOTE]  
  > Se i client riescono a ottenere la chiave radice attendibile da Active Directory Domain Services o tramite push client, il pre-provisioning non è necessario. 
  > 
  > Quando i client usano la comunicazione HTTPS ai punti di gestione, il pre-provisioning della chiave radice attendibile non è necessario. Questi client stabiliscono relazioni di trust tramite i certificati PKI.  


### <a name="pre-provision-a-client-with-the-trusted-root-key-by-using-a-file"></a><a name="bkmk_trk-provision-file"></a> Effettuare il pre-provisioning di un client con la chiave radice attendibile usando un file  

1.  Nel server del sito aprire il file seguente in un editor di testo: `<Configuration Manager install directory>\bin\mobileclient.tcf`  

2.  Individuare la voce **SMSPublicRootKey=** . Copiare la chiave da questa riga e chiudere il file senza apportare modifiche.  

3.  Creare un nuovo file di testo e incollare le informazioni della chiave copiate dal file mobileclient.tcf.  

4.  Salvare il file in un percorso accessibile a tutti i computer, ma che sia protetto da eventuali manomissioni.  

5.  Installare il client usando qualsiasi metodo di installazione che accetti le proprietà client.msi. Specificare la proprietà seguente: `SMSROOTKEYPATH=<full path and file name>`  

    > [!IMPORTANT]  
    > Quando si specifica la chiave radice attendibile durante l'installazione del client specificare anche il codice del sito. Usare la proprietà client.msi seguente: `SMSSITECODE=<site code>`   


### <a name="pre-provision-a-client-with-the-trusted-root-key-without-using-a-file"></a><a name="bkmk_trk-provision-nofile"></a> Effettuare il pre-provisioning di un client con la chiave radice attendibile senza usare un file  

1.  Nel server del sito aprire il file seguente in un editor di testo: `<Configuration Manager install directory>\bin\mobileclient.tcf`  

2.  Individuare la voce **SMSPublicRootKey=** . Copiare la chiave da questa riga e chiudere il file senza apportare modifiche.  

3.  Installare il client usando qualsiasi metodo di installazione che accetti le proprietà client.msi. Specificare la proprietà client.msi seguente: `SMSPublicRootKey=<key>` in cui `<key>` è la stringa copiata da mobileclient.tcf.  

    > [!IMPORTANT]  
    >  Quando si specifica la chiave radice attendibile durante l'installazione del client specificare anche il codice del sito. Usare la proprietà client.msi seguente: `SMSSITECODE=<site code>`   


### <a name="verify-the-trusted-root-key-on-a-client"></a><a name="bkmk_trk-verify"></a> Verificare la chiave radice attendibile in un client  

1. Aprire la console di Windows PowerShell come amministratore.  

2. Eseguire il comando seguente:  

    ``` PowerShell
    (Get-WmiObject -Namespace root\ccm\locationservices -Class TrustedRootKey).TrustedRootKey
    ```

La stringa restituita è la chiave radice attendibile. Verificare che corrisponda al valore **SMSPublicRootKey** presente nel file mobileclient.tcf nel server del sito.  


### <a name="remove-or-replace-the-trusted-root-key"></a><a name="bkmk_trk-reset"></a> Rimuovere o sostituire la chiave radice attendibile  

Rimuovere la chiave radice attendibile da un client usando la proprietà client.msi **RESETKEYINFORMATION = TRUE**. 

Per sostituire la chiave radice attendibile reinstallare il client insieme alla nuova chiave radice attendibile. Usare ad esempio il push client oppure specificare la proprietà client.msi **SMSPublicRootKey**.  

Per altre informazioni su queste proprietà di installazione, vedere [Informazioni sui parametri e le proprietà di installazione del client](../../clients/deploy/about-client-installation-properties.md).



##  <a name="plan-for-signing-and-encryption"></a><a name="BKMK_PlanningForSigningEncryption"></a> Pianificare firma e crittografia  
 
Quando si usano i certificati PKI per tutte le comunicazioni client, non è necessario pianificare la firma e la crittografia per proteggere la comunicazione dei dati dei client. Se si configura qualsiasi sistema del sito che esegue IIS per consentire le connessioni client HTTP, decidere la modalità di protezione della comunicazione client per il sito.  

Per proteggere i dati che i client inviano ai punti di gestione, è possibile rendere obbligatoria la firma dei dati da parte dei client. È anche possibile richiedere l'algoritmo SHA-256 per la firma. Questa configurazione è più sicura, ma rendere obbligatorio l'uso di SHA-256 solo se è supportato da tutti i client. Molti sistemi operativi supportano questo algoritmo in modo nativo, ma i sistemi operativi precedenti potrebbe richiedere un aggiornamento o un hotfix. 

Mentre la firma contribuisce a proteggere i dati da eventuali manomissioni, la crittografia contribuisce a proteggere i dati dalla diffusione di informazioni. È possibile attivare la crittografia 3DES per i dati di inventario e i messaggi di stato che i client inviano ai punti di gestione presenti nel sito. Per supportare questa opzione non è necessario installare aggiornamenti nei client. La crittografia e la decrittografia comportano un utilizzo aggiuntivo della CPU per client e punti di gestione.  

Per altre informazioni su come configurare le impostazioni per la firma e la crittografia, vedere [Configurare la firma e la crittografia](configure-security.md#BKMK_ConfigureSigningEncryption).  



##  <a name="plan-for-role-based-administration"></a><a name="BKMK_PlanningForRBA"></a> Pianificare l'amministrazione basata su ruoli  

Per altre informazioni, vedere [Nozioni fondamentali sull'amministrazione basata su ruoli](../../understand/fundamentals-of-role-based-administration.md).  



## <a name="plan-for-azure-active-directory"></a><a name="bkmk_planazuread"></a> Pianificare Azure Active Directory

Configuration Manager si integra con Azure Active Directory (Azure AD) per consentire al sito e ai client di usare l'autenticazione moderna. L'onboarding del sito in Azure AD supporta gli scenari di Configuration Manager seguenti:

**Client**  

- [Gestire i client in Internet tramite il gateway di gestione cloud](../../clients/manage/cmg/plan-cloud-management-gateway.md#scenarios)  

- [Gestire i dispositivi aggiunti a un dominio cloud](../../clients/deploy/deploy-clients-cmg-azure.md)  

- [Co-gestione](../../../comanage/overview.md)  

- [Distribuire applicazioni disponibili per l'utente](../../../apps/deploy-use/deploy-applications.md#deploy-user-available-applications)

- [App online di Microsoft Store per le aziende](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)  

- Ridurre i requisiti di infrastruttura. Usare ad esempio [Software Center tramite il punto di gestione](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex) anziché il Catalogo applicazioni  

- [Gestire App di Microsoft 365 per grandi imprese](../../../sum/deploy-use/manage-office-365-proplus-updates.md)  


**Server**  

- [Desktop Analytics](../../../desktop-analytics/overview.md)  

- [Azure Log Analytics](/azure/azure-monitor/platform/collect-sccm)  

- [Hub della community](../../get-started/capabilities-in-technical-preview-1807.md#bkmk_hub)  

- [Punto di distribuzione cloud](../hierarchy/use-a-cloud-based-distribution-point.md)  

- [Individuazione utente](../../servers/deploy/configure/configure-discovery-methods.md#azureaadisc)  


Per altre informazioni sulla connessione del sito ad Azure AD, vedere [Configurare i servizi di Azure](../../servers/deploy/configure/azure-services-wizard.md).


Per altre informazioni su Azure AD, vedere la [documentazione di Azure Active Directory](/azure/active-directory/).



## <a name="plan-for-sms-provider-authentication"></a><a name="bkmk_auth"></a> Pianificare l'autenticazione del provider SMS
<!--1357013--> 

A partire dalla versione 1810, è possibile specificare il livello di autenticazione minimo per gli amministratori per l'accesso ai siti di Configuration Manager. Questa funzionalità impone agli amministratori di accedere a Windows con il livello richiesto. Si applica a tutti i componenti che accedono al provider SMS. Ad esempio, la console di Configuration Manager, i metodi dell'SDK e i cmdlet di Windows PowerShell. 

Questa configurazione è un'impostazione a livello di gerarchia. Prima di modificare questa impostazione, assicurarsi che tutti gli amministratori di Configuration Manager possano accedere a Windows con il livello di autenticazione richiesto. 

Sono disponibili i livelli seguenti:

- **Autenticazione di Windows**: richiede l'autenticazione con le credenziali del dominio di Active Directory.   

- **Autenticazione del certificato**: richiede l'autenticazione con un certificato valido emesso da un'autorità di certificazione PKI attendibile.  

- **Autenticazione di Windows Hello for Business**: richiede l'autenticazione a due fattori avanzata associata a un dispositivo e l'uso di dati biometrici o di un PIN.  

Per altre informazioni, vedere [Piano per il provider SMS](../hierarchy/plan-for-the-sms-provider.md#bkmk_auth). 



## <a name="see-also"></a>Vedere anche
- [Sicurezza e privacy per i client di Configuration Manager](../../clients/deploy/plan/security-and-privacy-for-clients.md)  

- [Configurare la sicurezza](configure-security.md)  

- [Comunicazioni tra gli endpoint](../hierarchy/communications-between-endpoints.md)  

- [Riferimento tecnico per i controlli crittografici](cryptographic-controls-technical-reference.md)  

- [Requisiti dei certificati PKI](../network/pki-certificate-requirements.md)