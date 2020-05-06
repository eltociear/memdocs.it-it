---
title: Gestione client basata su Internet
titleSuffix: Configuration Manager
description: Creare una piano per gestire client basati su Internet in Configuration Manager.
ms.date: 04/29/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 83a7c934-3b11-435d-ba22-cbc274951e83
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f7054c75643c6ffa37decba74f9fe85831728985
ms.sourcegitcommit: b7e5b053dfa260e7383a9744558d50245f2bccdc
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/29/2020
ms.locfileid: "82587224"
---
# <a name="plan-for-internet-based-client-management-in-configuration-manager"></a>Pianificare la gestione dei client basata su Internet in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Usare la gestione client basata su Internet (IBCM) per gestire i client di Configuration Manager quando non sono connessi alla rete interna. Vantaggi dell'uso di IBCM:

- Controllo completo di server e ruoli che offrono il servizio
- Nessuna dipendenza del servizio cloud
- Potrebbe non essere necessaria una rete privata virtuale (VPN)
- Tutti i costi sono associati al servizio locale

A causa dei requisiti di sicurezza più elevati per la gestione dei computer client in una rete pubblica, IBCM richiede l'uso di certificati PKI. Questa configurazione assicura che le connessioni vengano autenticate da un'autorità indipendente. I dati inviati dai client IBCM e dai server del sito vengono crittografati e protetti.  

## <a name="client-communications"></a>Comunicazioni client

I ruoli del sistema del sito seguenti nei siti primari supportano connessioni da client che si trovano in percorsi non attendibili:

> [!NOTE]
> Sebbene IBCM sia incentrato principalmente sullo scenario basato su Internet, gli stessi comportamenti si applicano ai client in una foresta Active Directory non attendibile. I siti secondari non supportano le connessioni client da percorsi non attendibili.

- Punto di registrazione certificati per il modulo criteri di Configuration Manager (NDES)

- Punto di distribuzione

- Punto di distribuzione basato su cloud

- Punto proxy di registrazione

- Punto di stato di fallback

- Punto di gestione

- Punto di aggiornamento software

> [!NOTE]
> Il supporto per i ruoli del Catalogo applicazioni è terminato con la versione 1910. Per altre informazioni, vedere [Rimuovere il catalogo applicazioni](../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat). Per le versioni di Configuration Manager 1906 e precedenti ancora supportate, il punto per siti Web del catalogo applicazioni può accettare connessioni da client basati su Internet.

### <a name="about-internet-facing-site-systems"></a>Informazioni sui sistemi del sito con connessione Internet

Non è necessario che esista l'attendibilità reciproca tra la foresta del client e quella del server del sistema del sito. Quando la foresta che contiene il sistema del sito con connessione Internet considera attendibile la foresta che contiene gli account utente, tuttavia, questa configurazione supporta criteri basati sull'utente per i dispositivi su Internet se si abilita l'impostazione client **Abilitare le richieste dei criteri utente dai client Internet** di **Criteri client**.

Ad esempio, le configurazioni seguenti illustrano quando IBCM supporta criteri utente per i dispositivi su Internet:

- Il punto di gestione basato su Internet si trova nella rete perimetrale. Questa rete include anche un controller di dominio di sola lettura per autenticare l'utente. Un firewall tra le reti perimetrale e interna consente i pacchetti Active Directory.

- L'account utente è incluso nella foresta basata su Intranet. Il punto di gestione basato su Internet è incluso nella foresta basata sul perimetro. La foresta perimetrale considera attendibile la foresta interna. Un firewall tra la rete perimetrale e la rete interna consente i pacchetti di autenticazione.

- L'account utente e il punto di gestione basato su Internet sono entrambi inclusi nella foresta basata su Intranet. Il punto di gestione viene pubblicato su Internet con un server proxy Web.

### <a name="use-a-web-proxy-server"></a>Usare un server proxy Web

È possibile posizionare i sistemi del sito basati su Internet nella Intranet quando vengono pubblicati in Internet con un server proxy Web. Configurare questi sistemi del sito per connessioni client solo da Internet o per connessioni client da Internet e Intranet. Quando si usa un server Web proxy, è possibile configurarlo per il bridging Secure Sockets Layer (SSL) a SSL o il tunneling SSL.

#### <a name="ssl-bridging-to-ssl"></a>Bridging SSL a SSL

Il bridging SSL a SSL è la configurazione consigliata e più sicura, perché usa la terminazione SSL con l'autenticazione. Autentica i computer client con l'autenticazione del computer. I dispositivi mobili registrati da Configuration Manager non supportano il bridging SSL.

Con la terminazione SSL nel proxy, i pacchetti da Internet vengono controllati prima di inoltrarli alla rete interna. Il proxy autentica la connessione dal client, la termina, quindi apre una nuova connessione autenticata ai sistemi del sito basati su Internet. Quando i client di Configuration Manager usano un proxy, il client contiene in modo sicuro la relativa identità (GUID) nel payload del pacchetto. Il punto di gestione non considera il proxy come client. Configuration Manager non supporta il bridging da HTTP a HTTPS o da HTTPS a HTTP.

> [!NOTE]
> Configuration Manager non supporta l'impostazione di configurazioni di bridge SSL di terze parti. Ad esempio, Citrix Netscaler o F5 BIG-IP. Collaborare con il fornitore del dispositivo per configurarlo per l'uso con Configuration Manager.

#### <a name="tunneling"></a>Tunneling

Se il server Web proxy non è in grado di supportare i requisiti per il bridging SSL, Configuration Manager supporta anche il tunneling SSL. È anche possibile usare il tunneling SSL per supportare i dispositivi mobili registrati con Configuration Manager. Si tratta di un'opzione meno sicura perché il proxy inoltra i pacchetti SSL da Internet ai sistemi del sito senza terminazione SSL. Il proxy non controlla i pacchetti per individuare contenuti dannosi. Quando si usa il tunneling SSL, non sono previsti requisiti di certificato per il server Web proxy.

## <a name="plan-for-internet-based-clients"></a>Pianificare client basati su Internet

Decidere se configurare i client basati su Internet per la gestione sia nella Intranet che in Internet oppure solo per la gestione client basata su Internet. Questa opzione di gestione può essere configurata solo durante l'installazione del client. Per modificarla in un secondo momento, reinstallare il client.

> [!NOTE]
> Se si configura un punto di gestione per supportare i client basati su Internet, i client che si connettono a questo punto di gestione potranno usare Internet dopo aver aggiornato l'elenco di punti di gestione disponibili.
>
> Non si dovrà limitare la configurazione esclusivamente alla gestione client basata su Internet. È possibile usarla anche per la rete Intranet.

I client configurati solo per la gestione basata su Internet comunicano esclusivamente con i sistemi del sito configurati per le connessioni client da Internet. Usare questa configurazione negli scenari seguenti:

- Per i computer che sicuramente non si connetteranno mai alla Intranet. Ad esempio, i computer POS in posizioni remote.
- Per limitare la comunicazione client solo a HTTPS. Ad esempio, per supportare il firewall e i criteri di sicurezza limitati.
- Quando si installano sistemi del sito basati su Internet in una rete perimetrale e si vogliono gestire questi server come client di Configuration Manager.

> [!NOTE]
> Quando si vogliono gestire client di un gruppo di lavoro su Internet, installarli con una configurazione limitata a Internet.
>
> Quando si configura un dispositivo mobile per l'uso di un punto di gestione basato su Internet, questo viene configurato automaticamente come solo Internet.

È possibile configurare altri client per la gestione client Internet e Intranet. Quando rilevano il cambio di rete, passano automaticamente dalla gestione IBCM a quella basata sulla Intranet. Se sono in grado di trovare e connettersi a un punto di gestione che supporta le connessioni client sulla Intranet, questi client vengono gestiti come client Intranet. I client Intranet dispongono di funzionalità complete di Configuration Manager. Se non riescono a trovare o a connettersi a un punto di gestione che supporta le connessioni client sulla Intranet, i client tentano di connettersi a un punto di gestione basato su Internet. Se questa azione riesce, questi client vengono quindi gestiti dai sistemi del sito basati su Internet nel sito assegnato.

Il vantaggio del cambio automatico è che i client possono usare tutte le funzionalità quando si connettono alla Intranet e ricevono funzionalità di gestione essenziali quando si trovano su Internet. Il download del contenuto che inizia su Internet può riprendere facilmente sulla Intranet e viceversa.

## <a name="prerequisites"></a>Prerequisiti

La gestione IBCM in Configuration Manager ha le dipendenze seguenti:

- I client richiedono una connessione a Internet. Configuration Manager usa la connessione Internet esistente del dispositivo. I dispositivi mobili devono avere una connessione Internet diretta. I computer client completi possono usare una connessione Internet diretta oppure connettersi tramite un server Web proxy.

- I sistemi del sito che supportano IBCM richiedono una connessione Internet e devono essere inclusi in un dominio Active Directory. I sistemi del sito basati su Internet non richiedono una relazione di trust con la foresta di Active Directory del server del sito. Tuttavia, quando il punto di gestione basato su Internet è in grado di autenticare l'utente usando l'autenticazione di Windows, supporta i criteri utente. Se l'autenticazione di Windows ha esito negativo, supporta solo i criteri del dispositivo.

    > [!NOTE]
    > Per supportare i criteri utente, abilitare anche le impostazioni client seguenti nel gruppo **Criteri client**:
    >
    > - **Abilitare il polling dei criteri utente sui client**
    > - **Abilitare le richieste dei criteri utente dai client Internet**  

- Infrastruttura a chiave pubblica (PKI) per la distribuzione e la gestione dei certificati richiesti per i client basati su Internet e i server del sistema del sito. Per altre informazioni, vedere [requisiti dei certificati PKI](../../plan-design/network/pki-certificate-requirements.md).

- Registrare le voci host DNS pubblico per i nomi di dominio completi (FQDN) Internet dei sistemi del sito che supportano IBCM.

### <a name="client-communication-requirements"></a>Requisiti di comunicazione client

I firewall o server proxy coinvolti devono consentire la comunicazione client per i sistemi del sito basati su Internet:

- Supporto HTTP 1.1  

- Autorizzazione al tipo di contenuto HTTP di allegati MIME multiparte (multiparte/misto e applicazione/flusso di ottetti)  

#### <a name="verbs"></a>Verbi

Consentire i verbi seguenti per i ruoli del server del sistema del sito basati su Internet:

| Ruolo | Verbi |
|------|-------|
| Punto di gestione | - HEAD<br>- CCM_POST<br>- BITS_POST<br>- GET<br>- PROPFIND |
| Punto di distribuzione | - HEAD<br>- GET<br>- PROPFIND |
| Punto di stato di fallback | POST |
| Punto per siti Web del catalogo applicazioni | -POST<br>-GET |

#### <a name="http-headers"></a>Intestazioni HTTP

Consentire le intestazioni HTTP seguenti per i ruoli del server del sistema del sito basati su Internet:

| Ruolo | Intestazioni HTTP |
|------|--------------|
| Punto di gestione | - Range:<br>- CCMClientID:<br>- CCMClientIDSignature:<br>- CCMClientTimestamp:<br>- CCMClientTimestampsSignature: |
| Punto di distribuzione | Intervallo: |

Per i requisiti di comunicazione simili richiesti quando si usa il punto di aggiornamento software per le connessioni client da Internet, vedere la documentazione per Windows Server Update Services (WSUS).

## <a name="unsupported-features"></a>Funzionalità non supportate

Non tutte le funzionalità di gestione client sono appropriate per Internet. Configuration Manager non supporta alcune funzionalità per i client su Internet. Queste funzionalità non supportate si basano in genere su Active Directory Domain Services o non sono appropriate per una rete pubblica.

Le funzionalità seguenti non sono supportate quando si gestiscono i client su Internet con IBCM:

- Distribuzione di client su Internet, ad esempio la distribuzione client basata su aggiornamento software e push client. Usare l'installazione client manuale.

- Assegnazione automatica al sito

- Riattivazione LAN

- Distribuzione del sistema operativo. Tuttavia, è possibile distribuire sequenze di attività che non distribuiscono un sistema operativo.

- Controllo remoto

- Distribuzione di software agli utenti. Questa funzionalità si basa sul Catalogo applicazioni, che è deprecato.

- Roaming dei client. Il roaming consente ai client di individuare sempre i punti di distribuzione più vicini per scaricare il contenuto. I client selezionano in modo non deterministico uno dei sistemi del sito basati su Internet, indipendentemente dalla larghezza di banda o dalla posizione fisica.

Quando si configura un punto di aggiornamento software per accettare le connessioni da Internet, i client basati su Internet eseguono sempre l'analisi rispetto a questo punto per determinare gli aggiornamenti software necessari. Quando questi client sono connessi a Internet, provano prima a scaricare gli aggiornamenti software da Microsoft Update, piuttosto che da un punto di distribuzione basato su Internet. In caso di errore, provano quindi a scaricare gli aggiornamenti software richiesti da un punto di distribuzione basato su Internet.

> [!TIP]
> Il client di Configuration Manager determina automaticamente se si trova sull'intranet o su Internet. Se il client riesce a contattare un controller di dominio o un punto di gestione locale, imposta il proprio tipo di connessione su "Ora *Intranet*". In caso contrario, passa a "Ora *Internet*" e comunica con i sistemi del sito assegnati al relativo sito.
