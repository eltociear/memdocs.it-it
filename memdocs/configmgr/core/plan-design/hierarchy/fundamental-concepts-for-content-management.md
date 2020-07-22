---
title: Concetti di base della gestione dei contenuti
titleSuffix: Configuration Manager
description: È possibile usare gli strumenti e le opzioni di Configuration Manager per gestire il contenuto da distribuire.
ms.date: 07/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c201be2a-692c-4d67-ac95-0a3afa5320fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d8f29ed1e3201da139daeaa1fadca739ff44dc8e
ms.sourcegitcommit: 488db8a6ab272f5d639525d70718145c63d0de8f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/14/2020
ms.locfileid: "86384945"
---
# <a name="fundamental-concepts-for-content-management-in-configuration-manager"></a>Concetti di base per la gestione dei contenuti in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Configuration Manager supporta un solido sistema di strumenti e opzioni per gestire i contenuti software, necessari per tutte le distribuzioni di software, quali applicazioni, pacchetti, aggiornamenti software e distribuzioni del sistema operativo. Configuration Manager archivia il contenuto sia sui server del sito che sui punti di distribuzione. Questo contenuto richiede una grande quantità di larghezza di banda di rete durante il trasferimento tra i percorsi. Per pianificare e usare efficacemente l'infrastruttura di gestione dei contenuti, è opportuno conoscere prima le opzioni e le configurazioni disponibili. Quindi valutare come usarle per adattare al meglio l'ambiente di rete e le esigenze di distribuzione del contenuto.  

> [!TIP]  
> Per ulteriori informazioni sul processo di distribuzione del contenuto e per informazioni sulla diagnosi e la risoluzione dei problemi di distribuzione del contenuto generale, vedere [Comprensione e risoluzione dei problemi di distribuzione del contenuto in Configuration Manager](https://support.microsoft.com/help/4000401/content-distribution-in-mcm).

Le sezioni seguenti includono i concetti di base per la gestione dei contenuti. Se per un concetto sono necessarie informazioni aggiuntive o più complete, vengono forniti collegamenti a tali informazioni.


## <a name="accounts-used-for-content-management"></a>Account usati per la gestione dei contenuti

Con la gestione dei contenuti è possibile usare gli account seguenti:  

### <a name="network-access-account"></a>Account di accesso alla rete

Usato dai client per connettersi a un punto di distribuzione e accedere al contenuto. Per impostazione predefinita, l'account computer viene usato per primo.  

Questo account viene usato anche dai punti di distribuzione pull per scaricare contenuto da un punto di distribuzione di origine in una foresta remota.  

A partire dalla versione 1806, in alcuni scenari non è più necessario un account di accesso alla rete. È possibile abilitare il sito per l'uso di HTTP migliorato con l'autenticazione di Azure Active Directory.<!--1358228-->

Per altre informazioni, vedere [Account di accesso alla rete](accounts.md#network-access-account).

### <a name="package-access-account"></a>Account di accesso al pacchetto

Per impostazione predefinita, Configuration Manager concede l'accesso ai contenuti in un punto di distribuzione agli account di accesso generici Utenti e Amministratori. È tuttavia possibile configurare autorizzazioni aggiuntive per limitare l'accesso.

Per altre informazioni, vedere [Account di accesso al pacchetto](accounts.md#package-access-account).


## <a name="bandwidth-throttling-and-scheduling"></a>Limitazione e pianificazione della larghezza di banda della rete

Le opzioni di limitazione e pianificazione della larghezza di banda della rete consentono di controllare la distribuzione del contenuto da un server del sito ai punti di distribuzione. Queste funzionalità sono simili, ma non direttamente correlate, ai controlli della larghezza di banda per la replica da sito a sito basata su file.  

Per altre informazioni, vedere [Gestire la larghezza di banda di rete](manage-network-bandwidth.md).


## <a name="binary-differential-replication"></a>Replica differenziale binaria

Configuration Manager usa la replica differenziale binaria per aggiornare il contenuto distribuito in precedenza ad altri siti o a punti di distribuzione remoti. Per supportare la riduzione dell'uso della larghezza di banda da parte della replica differenziale binaria, installare la funzionalità **Compressione differenziale remota** nei punti di distribuzione. Per altre informazioni, vedere i [prerequisiti per i punti di distribuzione](../configs/site-and-site-system-prerequisites.md#bkmk_2012dppreq).

La replica differenziale binaria riduce al minimo la larghezza di banda di rete usata per inviare aggiornamenti per il contenuto distribuito. Invia nuovamente solo il contenuto nuovo o modificato anziché inviare l'intero set di file di origine del contenuto ogni volta che si modificano tali file.  

Quando si usa la replica differenziale binaria, Configuration Manager consente di identificare le modifiche apportate ai file di origine per ogni set di contenuti distribuiti in precedenza.  

- Quando i file nel contenuto di origine cambiano, il sito crea una nuova versione incrementale dei contenuti, quindi replica solo i file modificati nei siti di destinazione e i punti di distribuzione. Un file è considerato modificato se viene rinominato, spostato o se il contenuto del file cambia. Ad esempio, se si sostituisce un singolo file del driver con un pacchetto di driver che è stato in precedenza distribuito in diversi siti, vengono replicati solo i file dei driver modificati.  

- Configuration Manager supporta fino a cinque versioni incrementali del set di contenuti prima di inviare nuovamente l'intero set di contenuti. Dopo il quinto aggiornamento, la successiva modifica del set di contenuto fa sì che il sito crei una nuova versione del set di contenuto. Configuration Manager distribuisce quindi la nuova versione del set di contenuti per sostituire il set precedente e qualsiasi sua versione incrementale. Dopo che il nuovo set di contenuti è stato distribuito, le modifiche incrementali successive ai file di origine vengono nuovamente replicate dalla replica differenziale binaria.  

La replica differenziale binaria è supportata tra ogni sito padre e figlio in una gerarchia. La replica differenziale binaria è supportata all'interno di un sito tra il server del sito e i suoi normali punti di distribuzione. I punti di distribuzione pull e i punti di distribuzione cloud non supportano però la replica differenziale binaria per trasferire i contenuti. I punti di distribuzione pull supportano i delta a livello di file e il trasferimento dei nuovi file, ma non i blocchi all'interno di un file.

Le applicazioni usano sempre la replica differenziale binaria. La replica differenziale binaria è facoltativa per i pacchetti e non è abilitata per impostazione predefinita. Per usare la replica differenziale binaria per i pacchetti, abilitare questa funzionalità per ogni pacchetto. Selezionare l'opzione **Abilita replica differenziale binaria** quando si crea o si modifica un pacchetto.


### <a name="bdr-or-delta-replication"></a>Replica differenziale binaria o replica differenziale

<!-- SCCMDocs#1209 -->
Gli elenchi seguenti riepilogano le differenze tra la *replica differenziale binaria* e la *replica differenziale*.

#### <a name="summary-of-binary-differential-replication"></a>Riepilogo della replica differenziale binaria

- Termine di Configuration Manager per la **compressione differenziale remota** di Windows
- Differenze a livello di *blocco*
- Sempre abilitata per le app
- Facoltativa nei pacchetti legacy
- Se un file è già presente nel punto di distribuzione e viene apportata una modifica, il sito usa la replica differenziale binaria per replicare la modifica a livello di blocco anziché l'intero file. Questo comportamento si verifica solo quando si abilita l'oggetto per l'utilizzo della replica differenziale binaria.<!-- SCCMDocs#2026 -->

#### <a name="summary-of-delta-replication"></a>Riepilogo della replica differenziale

- Differenze a livello di *file*
- Attiva per impostazione predefinita, non configurabile
- Quando viene modificato un pacchetto, il sito ricerca le modifiche ai singoli file anziché all'intero pacchetto.
    - Se un file viene modificato, usare la replica differenziale binaria
    - Se è presente un nuovo file, copiare il nuovo file


## <a name="peer-caching-technologies"></a>Tecnologie di peer caching

<!-- SCCMDocs#1044 -->

Configuration Manager supporta diverse opzioni per la gestione del contenuto tra dispositivi peer nella stessa rete:

- [BranchCache](#branchcache)
- [Ottimizzazione recapito](#delivery-optimization)
- [Peer cache di Configuration Manager](#peer-cache)

Usare la tabella seguente per confrontare le funzionalità principali di queste tecnologie:

| Funzionalità  | Peer&nbsp;cache  | Ottimizzazione&nbsp;recapito  | BranchCache  |
|---------|---------|---------|---------|
| Tra subnet | Sì | Sì | No |
| Limitazione larghezza di banda | Sì (BITS) | Sì (nativa) | Sì (BITS) |
| Contenuto parziale | Sì | Sì | Sì |
| Controllo delle dimensioni della cache su disco | Sì | Sì | Sì |
| Individuazione origine peer | Manuale (impostazione client) | Automatico | Automatico |
| Individuazione peer | Tramite il punto di gestione con gruppi di limiti | Servizio cloud ottimizzazione recapito | Trasmissione |
| Reporting | Dashboard origini dati del client | Dashboard origini dati del client | Dashboard origini dati del client |
| Controllo dell'utilizzo WAN | Gruppi di limiti | GroupID ottimizzazione recapito | Solo subnet |
| Contenuto supportato | Tutto il contenuto di ConfigMgr | Aggiornamenti di Windows, driver, app dello Store | Tutto il contenuto di ConfigMgr |
| Controllo dei criteri | Impostazioni agente client | Impostazioni agente client (parziali) | Impostazioni agente client |

### <a name="recommendations"></a>Indicazioni

- Gestione moderna: Se si usano già strumenti moderni, ad esempio Intune, implementare l'ottimizzazione recapito

- Configuration Manager e co-gestione: Usare una combinazione di peer cache e ottimizzazione recapito. Usare la peer cache con i punti di distribuzione locali e usare l'ottimizzazione recapito per gli scenari cloud.

- BranchCache esistente implementato: Usare tutte e tre le tecnologie in parallelo. Usare la peer cache e l'ottimizzazione recapito per scenari non supportati da BranchCache.


## <a name="branchcache"></a>BranchCache

[BranchCache](https://docs.microsoft.com/windows-server/networking/branchcache/branchcache) è una tecnologia di Windows. I client che supportano BranchCache e hanno scaricato una distribuzione configurata per BranchCache agiscono da origine di contenuto per altri client abilitati per BranchCache.  

Ad esempio, è necessario un punto di distribuzione che esegue Windows Server 2012 o versione successiva ed è configurato come server BranchCache. Quando il primo client abilitato per BranchCache richiede un contenuto da questo server, il client scarica tale contenuto e lo memorizza nella cache.  

- Il client può quindi rendere disponibile il contenuto per altri client abilitati per BranchCache nella stessa subnet, che a sua volta memorizza il contenuto nella cache.  
- Altri client nella stessa subnet non devono scaricare contenuto dal punto di distribuzione.  
- Il contenuto viene distribuito tra più client per trasferimenti futuri.  

Per altre informazioni, vedere [Supporto per Windows BranchCache](../configs/support-for-windows-features-and-networks.md#bkmk_branchcache).

## <a name="delivery-optimization"></a>Ottimizzazione recapito

<!-- 1324696 -->
I gruppi di limiti di Configuration Manager consentono di definire e regolamentare la distribuzione del contenuto nella rete aziendale e negli uffici remoti. [Ottimizzazione recapito di Windows](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization) è una tecnologia peer-to-peer basata sul cloud per la condivisione di contenuti tra dispositivi Windows 10. Configurare Ottimizzazione recapito in modo che usi i gruppi di limiti per la condivisione di contenuti tra peer. Le impostazioni del client applicano l'identificatore del gruppo di limiti come identificatore di gruppo di Ottimizzazione recapito sul client. Quando comunica con il servizio cloud Ottimizzazione recapito, il client usa questo identificatore per individuare i peer con il contenuto. Per altre informazioni, vedere impostazioni client per [ottimizzazione recapito](../../clients/deploy/about-client-settings.md#delivery-optimization).

Ottimizzazione recapito è la tecnologia consigliata per ottimizzare il recapito degli aggiornamenti di Windows 10 dei file di installazione rapida per gli aggiornamenti qualitativi di Windows 10. A partire da Configuration Manager versione 1910, l'accesso Internet al servizio cloud Ottimizzazione recapito è un requisito per utilizzare le funzionalità peer-to-peer. Per informazioni sugli endpoint Internet necessari, vedere [Domande frequenti per Ottimizzazione recapito](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions). L'ottimizzazione può essere usata per tutti gli aggiornamenti di Windows. Per altre informazioni, vedere [Ottimizzare il recapito degli aggiornamenti di Windows 10](../../../sum/deploy-use/optimize-windows-10-update-delivery.md).


## <a name="microsoft-connected-cache"></a>Microsoft Connected Cache

<!--3555764-->
a partire dalla versione 1906, è possibile installare un server di Microsoft Connected Cache nei punti di distribuzione. Memorizzando nella cache questo contenuto in locale, i client possono trarre vantaggio dalla funzionalità di Ottimizzazione recapito, tuttavia è possibile contribuire a proteggere i collegamenti WAN.

> [!NOTE]
> A partire dalla versione 1910, questa funzionalità è denominata **Microsoft Connected Cache**. In precedenza era nota come Cache in rete di Ottimizzazione recapito.

Questo server di cache agisce come una cache trasparente su richiesta per il contenuto scaricato da Ottimizzazione recapito. Usare le impostazioni client per assicurarsi che il server sia disponibile soltanto ai membri del gruppo di limiti di Configuration Manager locale.

Questa cache è separata dal contenuto del punto di distribuzione di Configuration Manager. Se si sceglie la stessa unità come ruolo del punto di distribuzione, il contenuto viene archiviato separatamente.

Per altre informazioni, vedere [Microsoft Connected Cache in Configuration Manager](microsoft-connected-cache.md).


## <a name="peer-cache"></a>Peer cache

La peer cache client consente di gestire la distribuzione di contenuti ai client in posizioni remote. La peer cache è una soluzione integrata di Configuration Manager che consente ai client di condividere i contenuti con altri client direttamente dalla cache locale.

Distribuire prima di tutto in una raccolta le impostazioni client che abilitano la peer cache. I membri di tale raccolta possono fungere da origine del contenuto peer per altri client all'interno dello stesso gruppo di limiti.

A partire dalla versione 1806, le origini delle peer cache dei client sono in grado di dividere il contenuto in parti, grazie alle quali è possibile ridurre al minimo il trasferimento in rete, riducendo l'utilizzo della rete WAN. Il punto di gestione consente una traccia più dettagliata delle parti del contenuto e tenta di eliminare più download dello stesso contenuto per ogni gruppo di limiti.<!--1357346-->

Per altre informazioni, vedere [Peer cache per i client di Configuration Manager](client-peer-cache.md).


## <a name="windows-pe-peer-cache"></a>Peer cache di Windows PE

Quando si distribuisce un nuovo sistema operativo con Configuration Manager, i computer che eseguono la sequenza di attività possono usare la peer cache Windows PE. Scaricano contenuto da un'origine peer cache anziché da un punto di distribuzione. Questo comportamento contribuisce a ridurre al minimo il traffico WAN negli scenari con le filiali, in cui non esiste un punto di distribuzione locale.

Per altre informazioni, vedere [Peer cache di Windows PE](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md).


## <a name="windows-ledbat"></a>Windows LEDBAT

<!--1358112-->
Windows LEDBAT (Low Extra Delay Background Transport) è una funzionalità di controllo della congestione della rete di Windows Server che consente di gestire i trasferimenti di rete in background. Per i punti di distribuzione in esecuzione in versioni supportate di Windows Server, abilitare un'opzione che consente di regolare il traffico di rete. In questo modo i client usano la larghezza di banda di rete solo quando è disponibile.

Per altre informazioni di carattere generale su Windows LEDBAT, vedere il post di blog [New transport advancements](https://techcommunity.microsoft.com/t5/Networking-Blog/Announcing-Transport-Features-and-Performance-Advancements-in/ba-p/339726) (Nuovi miglioramenti per il trasporto).

Per altre informazioni su come usare Windows LEDBAT con i punti di distribuzione di Configuration Manager, vedere l'impostazione **Regola la velocità del download per usare la larghezza di banda di rete inutilizzata (Windows LEDBAT)** descritta nella sezione relativa alla [configurazione delle impostazioni generali di un punto di distribuzione](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-general).


## <a name="client-locations"></a>Posizioni dei client

Di seguito sono elencate le posizioni da cui i client accedono al contenuto:  

- **Intranet** (locale):  

    - I punti di distribuzione possono usare HTTP o HTTPS.  

    - Usare i punti di distribuzione cloud solo come opzione di fallback, se non sono disponibili punti di distribuzione locali.  

- **Internet**:  

    - richiede che i punti di distribuzione con connessione Internet accettino HTTPS.  

    - Può usare un punto di distribuzione cloud o Cloud Management Gateway (CMG).  

        A partire dalla versione 1806, un CMG può anche trasferire contenuti ai client. Questa funzionalità riduce i certificati necessari e i costi delle macchine virtuali di Azure. Per altre informazioni, vedere [Modify a CMG](../../clients/manage/cmg/setup-cloud-management-gateway.md) (Modificare un gateway di gestione cloud).

- **Gruppo di lavoro**:  

    - I punti di distribuzione devono accettare HTTPS.  

    - Può usare un punto di distribuzione cloud o Cloud Management Gateway.  


## <a name="content-source-priority"></a>Priorità dell'origine del contenuto

Quando un client ha bisogno di contenuto, invia una richiesta di percorso del contenuto al punto di gestione. Il punto di gestione restituisce un elenco di percorsi del contenuto validi per il contenuto richiesto. Questo elenco varia a seconda dello scenario specifico, delle tecnologie in uso, della struttura del sito, dei gruppi di limiti e delle impostazioni di distribuzione. Quando viene eseguita una sequenza di attività, ad esempio, il client completo di Configuration Manager non è sempre in esecuzione e il comportamento può quindi variare.<!-- SCCMDocs#1960 -->

L'elenco seguente contiene tutti i possibili percorsi di origine del contenuto utilizzabili da un client Configuration Manager, in ordine di priorità:  

1. Il punto di distribuzione presente nello stesso computer del client
2. Un'origine peer nella stessa subnet di rete
3. Un punto di distribuzione nella stessa subnet di rete
4. Un'origine peer nello stesso gruppo di limiti
5. Un punto di distribuzione nel gruppo di limiti corrente
6. Un punto di distribuzione in un gruppo di limiti vicino configurato per il fallback
7. Un punto di distribuzione nel gruppo di limiti predefinito del sito
8. Il servizio cloud di Windows Update
9. Un punto di distribuzione con connessione Internet
10. Un punto di distribuzione cloud in Azure

> [!Note]  
> <!-- SCCMDocs#1607 -->L'ottimizzazione recapito non è applicabile a queste priorità di origine. Questo elenco indica il modo in cui il client di Configuration Manager trova il contenuto. L'agente di Windows Update scarica il contenuto per l'ottimizzazione recapito. Se l'agente di Windows Update non riesce a trovare il contenuto, il client di Configuration Manager usa questo elenco per cercarlo.

## <a name="content-library"></a>Raccolta contenuto

La raccolta contenuto è l'archivio a istanza singola del contenuto in Configuration Manager. Questa raccolta consente di ridurre la dimensione complessiva del contenuto distribuito.  

- Altre informazioni sulla [raccolta contenuto](the-content-library.md).
- Usare lo [strumento per la pulizia della raccolta contenuto](content-library-cleanup-tool.md) per rimuovere il contenuto non più associato a un'applicazione.  


## <a name="distribution-points"></a>Punti di distribuzione

Configuration Manager usa i punti di distribuzione per memorizzare i file necessari per l'esecuzione del software nei computer client. I client devono avere accesso ad almeno un punto di distribuzione da cui scaricare i file relativi al contenuto da distribuire.  

Il punto di distribuzione di base (non specializzato) è noto come punto di distribuzione standard. Esistono due principali varianti nel punto di distribuzione standard:  

- **Punto di distribuzione pull**: variante di un punto di distribuzione in cui il punto di distribuzione ottiene il contenuto da un altro punto di distribuzione (punto di distribuzione di origine). Questo processo è simile al modo in cui i client scaricano contenuto dai punti di distribuzione. I punti di distribuzione pull possono risultare utili per evitare i colli di bottiglia della larghezza di banda di rete che si verificano quando il server del sito deve distribuire direttamente il contenuto a ogni punto di distribuzione. [Usare un punto di distribuzione pull](use-a-pull-distribution-point.md).

- **Punto di distribuzione cloud**: variante di un punto di distribuzione installata in Microsoft Azure. [Informazioni sull'uso di un punto di distribuzione cloud](use-a-cloud-based-distribution-point.md).  

I punti di distribuzione standard supportano una gamma di configurazioni e funzionalità:  

- Per controllare il trasferimento, usare controlli come le **pianificazioni** o la **limitazione della larghezza di banda**.  

- È anche possibile usare altre opzioni, tra cui il **contenuto pre-installazione** e i **punti di distribuzione pull** per ridurre al minimo e controllare il consumo della rete.  

- **BranchCache**, **peer cache** e **Ottimizzazione recapito** sono tecnologie peer-to-peer per ridurre la larghezza di banda di rete usata quando si distribuisce il contenuto.  

- Esistono diverse configurazioni per le distribuzioni del sistema operativo, quali **[PXE](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)** e **[Multicast](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_DPMulticast)**  

- Opzioni per **dispositivi mobili**  
  
I punti di distribuzione pull e cloud supportano molte di queste configurazioni, ma presentano limitazioni specifiche per ogni variante del punto di distribuzione.  


## <a name="distribution-point-groups"></a>Gruppi di punti di distribuzione

I gruppi di punti di distribuzione sono raggruppamenti logici di punti di distribuzione che possono semplificare la distribuzione del contenuto.  

Per altre informazioni, vedere [Gestire i gruppi di punti di distribuzione](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage).


## <a name="distribution-point-priority"></a>Priorità dei punti di distribuzione

Il valore di priorità del punto di distribuzione è basato sul tempo impiegato per trasferire le distribuzioni precedenti al punto di distribuzione.  

- Questo valore è automatico. È impostato su ogni punto di distribuzione per consentire a Configuration Manager di trasferire più rapidamente il contenuto a più punti di distribuzione.  

- Quando si distribuisce contenuto a più punti di distribuzione contemporaneamente o a un gruppo di punti di distribuzione, il sito invia prima di tutto il contenuto al server con la priorità più alta. Quindi, invia lo stesso contenuto a un punto di distribuzione con una priorità più bassa.  

- La priorità di un punto di distribuzione non sostituisce la priorità di distribuzione dei pacchetti. La priorità del pacchetto rimane il fattore decisivo di quando il sito invia contenuto diverso.  

Ad esempio, si consideri un pacchetto con una priorità pacchetto alta. Tale pacchetto viene distribuito a un server con una priorità dei punti di distribuzione bassa. Questo pacchetto a priorità alta viene trasferito sempre prima di un pacchetto con una priorità più bassa. La priorità del pacchetto si applica anche se il sito distribuisce pacchetti di priorità inferiore ai server con priorità del punto di distribuzione più alta.

La priorità alta del pacchetto garantisce che il contenuto venga distribuito da Configuration Manager ai punti di distribuzione prima dell'invio di eventuali pacchetti con una priorità più bassa.  

> [!NOTE]  
> I punti di distribuzione pull usano anche un concetto di priorità per ordinare la sequenza dei punti di distribuzione di origine.  
>
> - La priorità dei punti di distribuzione per trasferimenti di contenuto al server è diversa dalla priorità usata dai punti di distribuzione pull. I punti di distribuzione pull usano la loro priorità quando cercano il contenuto da un punto di distribuzione di origine.  
> - Per altre informazioni, vedere [Usare un punto di distribuzione pull](use-a-pull-distribution-point.md).  


## <a name="fallback"></a>Fallback

Sono stati modificati alcuni aspetti in Configuration Manager Current Branch relativi al modo in cui i client individuano un punto di distribuzione con contenuto, fallback compreso.

I client che non riescono a individuare il contenuto da un punto di distribuzione associato al gruppo limite corrente eseguono il fallback per usare i percorsi di origine del contenuto associati a gruppi di limiti adiacenti. Per essere usato per il fallback, un gruppo di limiti adiacente deve avere una relazione definita con il gruppo di limiti corrente del client. Questa relazione include un tempo configurato che deve trascorrere prima che un client che non riesce a individuare contenuto localmente possa includere nella ricerca origini di contenuto dal gruppo di limiti adiacente.

I concetti di punti di distribuzione preferiti non sono più usati e le impostazioni per **Consenti percorso origine di fallback per il contenuto** non sono più disponibili o applicate.

Per altre informazioni, vedere [Gruppi di limiti](../../servers/deploy/configure/boundary-groups.md).


## <a name="network-bandwidth"></a>Larghezza di banda di rete

Per gestire la quantità di larghezza di banda di rete usata per la distribuzione del contenuto, è possibile usare le opzioni seguenti:  

- **Contenuto pre-installazione**: trasferimento del contenuto a un punto di distribuzione senza distribuire il contenuto nella rete.  

- **Pianificazione e limitazione della larghezza di banda della rete**: configurazioni che consentono di controllare la modalità e le tempistiche di distribuzione del contenuto ai punti di distribuzione.  

Per altre informazioni, vedere [Gestire la larghezza di banda di rete](manage-network-bandwidth.md).


## <a name="network-connection-speed-to-content-source"></a>Velocità di connessione di rete nell'origine del contenuto

Sono stati modificati alcuni aspetti in Configuration Manager Current Branch relativi al modo in cui i client individuano un punto di distribuzione con contenuto. Queste modifiche comprendono la velocità di rete verso un'origine di contenuto.

Le velocità di connessione di rete che definiscono un punto di distribuzione come **Veloce** o **Lento** non vengono più usate. Al contrario, ogni sistema del sito associato a un gruppo di limiti viene trattato allo stesso modo.

Per altre informazioni, vedere [Gruppi di limiti](../../servers/deploy/configure/boundary-groups.md).


## <a name="on-demand-content-distribution"></a>Distribuzione di contenuto su richiesta

La distribuzione del contenuto su richiesta è un'opzione per singole distribuzioni di applicazioni e pacchetti. Questa opzione consente la distribuzione del contenuto su richiesta ai server preferiti.  

- Per abilitare questa impostazione per una distribuzione, abilitare: **Distribuisci il contenuto del pacchetto nei punti di distribuzione preferiti**.  

- Quando si abilita questa opzione per una distribuzione e un client richiede contenuto non disponibile in uno qualsiasi dei punti di distribuzione preferiti del client, Configuration Manager distribuisce automaticamente tale contenuto ai punti di distribuzione preferiti del client.  

- In questo modo viene attivata la distribuzione automatica del contenuto ai punti di distribuzione preferiti del client da parte di Configuration Manager e il client può ottenere tale contenuto da altri punti di distribuzione prima che i punti di distribuzione preferiti per il client ricevano la distribuzione. In questo caso, il contenuto sarà presente nel punto di distribuzione per l'uso da parte del client successivo che cerca quella specifica distribuzione.  

Per altre informazioni, vedere [Gruppi di limiti](../../servers/deploy/configure/boundary-groups.md).


## <a name="package-transfer-manager"></a>Package Transfer Manager

Componente del server del sito che trasferisce il contenuto ai punti di distribuzione in altri computer.  

Per altre informazioni, vedere [Package Transfer Manager](package-transfer-manager.md).  


## <a name="prestage-content"></a>Pre-installare il contenuto

La pre-installazione del contenuto è un processo di trasferimento del contenuto a un punto di distribuzione senza distribuire il contenuto nella rete.  

Per altre informazioni, vedere [Gestire la larghezza di banda di rete](manage-network-bandwidth.md).
