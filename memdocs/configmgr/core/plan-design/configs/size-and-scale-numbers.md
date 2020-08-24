---
title: Ridimensionamento e scalabilità
titleSuffix: Configuration Manager
description: Determinare il numero di ruoli del sistema del sito e di siti necessari per supportare i dispositivi nell'ambiente.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c5a42100-2f60-4952-b495-918025ea6559
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 0d8057d61ebaaa8a545d21b31331faec1c04884e
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126699"
---
# <a name="size-and-scale-numbers-for-configuration-manager"></a>Numeri di ridimensionamento e scalabilità per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Ogni distribuzione di Configuration Manager ha un numero massimo di siti, di ruoli del sistema del sito e di dispositivi che può supportare. Questi numeri variano a seconda della struttura della gerarchia: i tipi e i numeri dei siti che vengono usati e dei ruoli del sistema del sito che vengono distribuiti. Le informazioni in questo articolo consentono di determinare il numero di ruoli del sistema del sito e di siti necessari per supportare i dispositivi che si prevede di gestire.

Per altre informazioni, vedere gli articoli seguenti:

- [Recommended hardware](recommended-hardware.md) (Hardware consigliato)
- [Sistemi operativi supportati per i server del sistema del sito di System Center Configuration Manager](supported-operating-systems-for-site-system-servers.md)  
- [Sistemi operativi supportati per client e dispositivi](supported-operating-systems-for-clients-and-devices.md)
- [Prerequisiti del sito e del sistema del sito](site-and-site-system-prerequisites.md)

I numeri del supporto si basano sull'uso dell'hardware consigliato per Configuration Manager. Si basano anche sulle impostazioni predefinite per tutte le funzionalità di Configuration Manager disponibili. Quando non si utilizza l'hardware consigliato o si adottano impostazioni personalizzate più aggressive, le prestazioni dei sistemi del sito possono peggiorare. I sistemi del sito potrebbero non soddisfare i livelli di supporto. Un esempio di impostazioni client più aggressive è eseguire l'inventario hardware o software più frequentemente di quanto definito dalle impostazioni predefinite, vale a dire una volta ogni sette giorni.

## <a name="site-types"></a><a name="bkmk_SiteSystemScale"></a> Tipi di sito  

### <a name="central-administration-site"></a>Sito di amministrazione centrale  

- Un sito di amministrazione centrale supporta fino a 25 siti primari figlio.  

### <a name="primary-site"></a>Sito primario  

- Ogni sito primario può supportare fino a 250 siti secondari.  

- Il numero di siti secondari per il sito primario si basa su connessioni WAN (Wide Area Network) continuamente connesse e affidabili. Per i percorsi contenenti meno di 500 client, considerare un punto di distribuzione anziché un sito secondario.  

  Per informazioni sul numero di client e di dispositivi che un sito primario può supportare, vedere la sezione [Numero di client per siti e gerarchie](#bkmk_clientnumbers).  

### <a name="secondary-site"></a>Sito secondario  

- I siti secondari non supportano siti figlio.  

## <a name="site-system-roles"></a><a name="bkmk_roles"></a> Site system roles

### <a name="application-catalog-web-service-point"></a>Punto per servizi Web del catalogo applicazioni  

> [!Important]
> L'esperienza utente di Silverlight per il Catalogo applicazioni non è supportata a partire dalla versione Current Branch 1806. A partire dalla versione 1906, i client aggiornati usano automaticamente il punto di gestione per le distribuzioni di applicazioni disponibili per gli utenti. Non è inoltre possibile installare nuovi ruoli del Catalogo applicazioni. Il supporto per i ruoli del Catalogo applicazioni termina con la versione 1910.  
>
> Per altre informazioni, vedere gli articoli seguenti:
>
> - [Configurare Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Funzionalità rimosse e deprecate](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

- È possibile installare più istanze del punto di servizio Web Catalogo applicazioni nei siti primari.  

### <a name="application-catalog-website-point"></a>Punto per siti Web del catalogo applicazioni  

> [!Important]
> L'esperienza utente di Silverlight per il catalogo applicazioni non è supportata a partire dalla versione Current Branch 1806. A partire dalla versione 1906, i client aggiornati usano automaticamente il punto di gestione per le distribuzioni di applicazioni disponibili per gli utenti. Non è inoltre possibile installare nuovi ruoli del Catalogo applicazioni. Il supporto per i ruoli del Catalogo applicazioni termina con la versione 1910.  
>
> Per altre informazioni, vedere gli articoli seguenti:
>
> - [Configurare Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Funzionalità rimosse e deprecate](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

- È possibile installare più istanze del punto di sito Web Catalogo applicazioni nei siti primari.  

### <a name="cloud-management-gateway"></a><a name="bkmk_cmg"></a>Gateway di gestione cloud

- È possibile installare più istanze del gateway di gestione cloud nei siti primari o del sito di amministrazione centrale.  

    > [!Tip]  
    > Nella gerarchia, creare il gateway di gestione cloud nel sito di amministrazione centrale.  

  - Un gateway di gestione cloud supporta da 1 a 16 istanze di macchina virtuale nel servizio cloud di Azure.  

  - Ogni istanza di macchina virtuale del gateway di gestione cloud supporta 6.000 connessioni client simultanee. Quando il gateway di gestione cloud ha un carico elevato a causa di un numero di client maggiore di quello supportato, le richieste continuano a essere gestite ma potrebbero verificarsi ritardi.  

Per altre informazioni, vedere [Prestazioni e scalabilità](../../clients/manage/cmg/plan-cloud-management-gateway.md#performance-and-scale) del gateway di gestione cloud

### <a name="cloud-management-gateway-connection-point"></a>Punto di connessione del gateway di gestione cloud

- È possibile installare più istanze del punto di connessione del gateway di gestione cloud nei siti primari.  

- Un punto di connessione del gateway di gestione cloud può supportare un gateway con fino a quattro istanze di macchine virtuali. Se il gateway di gestione cloud ha di più di quattro istanze di macchine virtuali, aggiungere un secondo punto di connessione per il bilanciamento del carico. Un gateway di gestione cloud con 16 istanze di macchine virtuali deve essere collegato a quattro punti di connessione gateway di gestione cloud.

Per altre informazioni, vedere [Prestazioni e scalabilità](../../clients/manage/cmg/plan-cloud-management-gateway.md#performance-and-scale) del gateway di gestione cloud

> [!NOTE]
> Quando si considerano i requisiti hardware per il punto di connessione di CMG, vedere [Hardware consigliato per i server del sistema del sito remoti](recommended-hardware.md#bkmk_RemoteSiteSystem).<!-- SCCMDocs#2276 -->

### <a name="distribution-point"></a>Punto di distribuzione  

- Punti di distribuzione per sito:  

  - Ogni sito primario e secondario supporta fino a 250 punti di distribuzione.  

  - Ogni sito primario e secondario supporta fino a 2000 punti di distribuzione aggiuntivi configurati come punti di distribuzione pull. **Ad esempio**, un singolo sito primario supporta 2250 punti di distribuzione quando 2000 di questi punti di distribuzione sono configurati come punti di distribuzione pull.  

  - Ogni punto di distribuzione supporta connessioni da massimo 4.000 client.  

  - Un punto di distribuzione pull funziona come client durante l'accesso al contenuto da un punto di distribuzione di origine.  

- Ogni sito primario e secondario supporta un totale combinato di massimo 5.000 punti di distribuzione. Tale totale include tutti i punti di distribuzione nel sito primario e tutti i punti di distribuzione che appartengono ai siti secondari figlio del sito primario.  

- Ogni punto di distribuzione supporta un totale combinato di massimo 10.000 pacchetti e applicazioni.  

> [!WARNING]  
> Il numero effettivo di client che un punto di distribuzione può supportare dipende dalla velocità della rete e dalla configurazione hardware del server.  
>
> Analogamente, il numero di punti di distribuzione pull che un punto di distribuzione di origine può supportare dipende dalla velocità della rete e dalla configurazione hardware del punto di distribuzione di origine. Ma questo numero dipende anche dalla quantità di contenuto che è stato distribuito. Questo accade perché, a differenza dei client che in genere accedono al contenuto in momenti diversi durante una distribuzione, tutti i punti di distribuzione pull richiedono contenuto nello stesso momento. I punti di distribuzione pull possono richiedere tutto il contenuto disponibile senza limitarsi al contenuto che è applicabile ad essi. Quando un punto di distribuzione di origine presenta un carico di elaborazione elevato, si possono verificare ritardi imprevisti nella distribuzione del contenuto ai punti di distribuzione di destinazione.  

### <a name="fallback-status-point"></a>Punto di stato di fallback  

- Ogni punto di stato di fallback è in grado di supportare fino a 100.000 client.  

### <a name="management-point"></a>Punto di gestione  

- Ogni sito primario supporta fino a 15 punti di gestione.  

    > [!TIP]  
    > Non installare punti di gestione in server che usano un collegamento lento dal server del sito primario o dal server di database del sito.  

- Ciascun sito secondario supporta un unico punto di gestione che deve essere installato nel server del sito secondario.  

Per informazioni sul numero di client e dispositivi che un punto di gestione può supportare, vedere la sezione [Punti di gestione](#bkmk_mp).  

> [!NOTE]
> Se si abilita il punto di gestione per il supporto di un [gateway di gestione cloud](../../clients/manage/cmg/plan-cloud-management-gateway.md), il punto di gestione esegue normalmente le richieste client basate su Internet. Le linee guida per il ridimensionamento di un punto di gestione sono le stesse per i punti che gestiscono sia richieste client basate su Intenet che locali.

### <a name="software-update-point"></a>Punto di aggiornamento software  

Usare come baseline i seguenti elementi consigliati. Questa baseline consente di determinare le informazioni relative alla pianificazione della capacità degli aggiornamenti software appropriate per la propria organizzazione. I requisiti di capacità effettivi potrebbero differire dagli elementi consigliati in questo articolo in base ai seguenti criteri:

- L'ambiente di rete specifico
- L'hardware usato per ospitare il sistema del sito del punto di aggiornamento software
- Il numero di client gestiti
- Gli altri ruoli del sistema del sito installati nel server  

> [!NOTE]
> Se si abilita il punto di aggiornamento software per il supporto di un [gateway di gestione cloud](../../clients/manage/cmg/plan-cloud-management-gateway.md), il punto di gestione esegue normalmente le richieste client basate su Internet. Le linee guida per il ridimensionamento di un punto di aggiornamento software sono le stesse per i punti che gestiscono sia richieste client basate su Intenet che locali.

#### <a name="capacity-planning-for-the-software-update-point"></a><a name="BKMK_SUMCapacity"></a> Pianificazione della capacità per il punto di aggiornamento software  

Il numero di client supportati dipende dalla versione di Windows Server Update Services (WSUS) in esecuzione nel punto di aggiornamento software. Dipende anche dal fatto che il ruolo del sistema del sito del punto di aggiornamento software coesista o meno con un altro ruolo del sistema del sito:  

- Il punto di aggiornamento software è in grado di supportare fino a 25.000 client quando WSUS è in esecuzione nel server del punto di aggiornamento software e il punto coesiste con un altro ruolo del sistema del sito.  

- Il punto di aggiornamento software può supportare fino a 150.000 client quando un server remoto soddisfa i requisiti di WSUS, WSUS viene usato con Configuration Manager e si configurano le impostazioni seguenti:

  Pool di applicazioni IIS:

  - Aumentare la lunghezza della coda WsusPool a 2000
  - Aumentare il limite di memoria privata WsusPool di 4 volte oppure impostarlo su 0 (illimitato). Se ad esempio il limite predefinito è 1.843.200 kB, aumentarlo a 7.372.800. Per altre informazioni su questo problema, vedere questo [post del blog del team di supporto di Configuration Manager](https://www.phoenixtekk.com/configmgr-2012-support-tip-wsus-sync-fails-with-http-503-errors/).  

    Per altre informazioni sui requisiti hardware per il punto di aggiornamento software, vedere [Recommended hardware for site systems](recommended-hardware.md#bkmk_ScaleSieSystems) (Hardware consigliato per i sistemi del sito).  

#### <a name="capacity-planning-for-software-updates-objects"></a><a name="bkmk_sum-capacity-obj"></a> Pianificazione della capacità per gli oggetti degli aggiornamenti software  

Usare le seguenti informazioni sulla capacità per la pianificazione degli oggetti degli aggiornamenti software:  

- **Limite di 1000 aggiornamenti software in una distribuzione**: è necessario limitare il numero di aggiornamenti software a 1000 per ogni distribuzione degli aggiornamenti software. Quando si crea una regola di distribuzione automatica (ADR), specificare un criterio che limiti il numero di aggiornamenti software. La regola di distribuzione automatica ha esito negativo quando i criteri specificati restituiscono più di 1000 aggiornamenti software. Controllare lo stato della regola di distribuzione automatica dal nodo **Regole di distribuzione automatica** nella console di Configuration Manager. Durante la distribuzione manuale degli aggiornamenti software, non selezionare più di 1000 aggiornamenti per la distribuzione.  

  È anche necessario limitare il numero di aggiornamenti software a 1000 in una linea di base di configurazione. Per altre informazioni, vedere [Creare configurazioni di base](../../../compliance/deploy-use/create-configuration-baselines.md).

- **Limite di 580 ambiti di protezione per le regole di distribuzione automatica** -<!--ado 4962928-->
Limitare il numero di ambiti di protezione nelle regole di distribuzione automatica a un valore inferiore a 580. Quando si crea una regola di distribuzione automatica, vengono aggiunti automaticamente gli ambiti di protezione che vi hanno accesso. Se sono presenti più di 580 ambiti di protezione impostati, la regola di distribuzione automatica non viene eseguita e viene registrato un errore in ruleengine.log.

### <a name="sms-provider"></a>Provider SMS

<!-- SCCMDocs#1958 -->

Ogni istanza del provider SMS supporta connessioni simultanee da più richieste. Gli unici limiti su queste connessioni sono il numero di connessioni server disponibili per Windows e le risorse disponibili sul server per rispondere alle richieste di connessione.

Per altre informazioni, vedere [Piano per il provider SMS](../hierarchy/plan-for-the-sms-provider.md).

Il servizio di amministrazione è un'API REST su ogni istanza del provider SMS. Supporta fino a 5.000 richieste al secondo e 200 richieste per ogni indirizzo IP del client.

## <a name="client-numbers-for-sites-and-hierarchies"></a><a name="bkmk_clientnumbers"></a> Numero di client per siti e gerarchie

Usare le informazioni seguenti per determinare quanti e quali tipi di client è possibile supportare in un sito o in una gerarchia.  

### <a name="hierarchy-with-a-central-administration-site"></a><a name="bkmk_cas"></a> Gerarchia con un sito di amministrazione centrale

Un sito di amministrazione centrale supporta un numero totale di dispositivi che comprende fino al numero di dispositivi elencati per i tre gruppi seguenti:  

- 700.000 desktop Windows. Vedere anche il supporto per i [dispositivi Windows Embedded](#embedded).

- 25.000 dispositivi che eseguono Mac e Windows CE 7.0  

- 100.000 dispositivi gestiti con software di gestione di dispositivi mobili (MDM) locale

Ad esempio, in una gerarchia è possibile supportare 700.000 desktop, fino a 25.000 dispositivi Mac e Windows CE 7.0 e fino a 100.000 dispositivi gestiti con software MDM locale. Questa gerarchia supporta un totale di 825.000 dispositivi.

> [!IMPORTANT]  
> In una gerarchia in cui il sito di amministrazione centrale usa un'edizione Standard di SQL Server, la gerarchia supporta un massimo di 50.000 desktop e dispositivi. Per supportare più di 50.000 desktop e dispositivi è necessario usare un'edizione Enterprise di SQL Server. Questo requisito si applica solo a un sito di amministrazione centrale. Non si applica a un sito primario autonomo o un sito primario figlio. L'edizione di SQL Server in uso per un sito primario non limita la sua capacità di supportare il numero dichiarato di client.

L'edizione di SQL Server in uso in un sito primario autonomo non limita la capacità di tale sito di supportare fino al numero dichiarato di client.  

### <a name="child-primary-site"></a><a name="bkmk_chipri"></a> Sito primario figlio

Ogni sito primario figlio in una gerarchia con un sito di amministrazione centrale supporta il numero di client seguente:  

- Un totale di 150.000 client e dispositivi che non sono limitati a un gruppo o tipo specifico, a condizione di non superare il numero supportato per la gerarchia. Vedere anche il supporto per i [dispositivi integrati](#embedded).

Ad esempio, un sito primario supporta 25.000 dispositivi Mac e Windows CE 7.0. Tale numero è il limite per la gerarchia. Questo sito primario può quindi supportare 125.000 computer desktop aggiuntivi. raggiungendo un numero totale di dispositivi supportati per il sito figlio primario di 150.000.

### <a name="stand-alone-primary-site"></a><a name="bkmk_pri"></a> Sito primario autonomo

Un sito primario autonomo supporta il numero seguente di dispositivi:  

- Un totale di 175.000 client e dispositivi, senza superare:  

  - 150.000 desktop (computer che eseguono Windows, Linux e UNIX). Vedere anche il supporto per i [dispositivi integrati](#embedded).

  - 25.000 dispositivi che eseguono Mac e Windows CE 7.0

  - 50.000 dispositivi gestiti con software MDM locale  

Ad esempio, un sito primario autonomo che supporta 150.000 desktop e 10.000 dispositivi Mac può supportare solo altri 15.000 dispositivi mobili gestiti con software MDM locale.

### <a name="primary-sites-and-windows-embedded-devices"></a><a name="embedded"></a> Siti primari e dispositivi con Windows Embedded

I siti primari supportano i dispositivi con Windows Embedded in cui sono abilitati i filtri di scrittura basati su file (FBWF). Se nei dispositivi integrati non sono abilitati filtri di scrittura, un sito primario può supportare un numero di dispositivi integrati non superiore al numero di dispositivi consentito per il sito. Quando nei dispositivi incorporati è abilitato FBWF o Unified Write Filters (UWF), un sito primario può supportare un massimo di 10.000 dispositivi Windows Embedded. Questi dispositivi devono essere configurati con le eccezioni elencate nella nota importante disponibile in [Pianificazione della distribuzione del client in dispositivi con Windows Embedded](../../clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md). Un sito primario supporta solo 3.000 dispositivi con Windows Embedded in cui è abilitato EWF e che non sono configurati per le eccezioni.

### <a name="secondary-sites"></a><a name="bkmk_sec"></a> Siti secondari

I siti secondari supportano il numero di dispositivi seguente:  

- 15.000 desktop (computer che eseguono Windows, Linux e UNIX)  

### <a name="management-points"></a><a name="bkmk_mp"></a> Punti di gestione

Ogni punto di gestione può supportare il numero di dispositivi seguente:  

- Un totale di 25.000 client e dispositivi, senza superare:  

  - 25.000 desktop (computer che eseguono Windows, Linux e UNIX)  

  - Uno dei gruppi seguenti (non entrambi):  

    - 10.000 dispositivi gestiti con software MDM locale  

    - 10.000 dispositivi che eseguono client Mac e Windows CE 7.0
