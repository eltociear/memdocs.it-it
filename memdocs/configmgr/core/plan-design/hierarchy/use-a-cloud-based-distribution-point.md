---
title: Punto di distribuzione cloud
titleSuffix: Configuration Manager
description: Pianificare e progettare la distribuzione del contenuto software tramite Microsoft Azure con i punti di distribuzione cloud in Configuration Manager.
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3cd9c725-6b42-427d-9191-86e67f84e48c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b488e0953648b42baa59dc347b0bc942bac291fe
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692571"
---
# <a name="use-a-cloud-distribution-point-in-configuration-manager"></a>Usare un punto di distribuzione cloud in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

> [!Important]  
> È stata modificata l'implementazione per la condivisione del contenuto da Azure. Usare un gateway di gestione cloud abilitato per il contenuto abilitando l'opzione **Consenti il funzionamento di CMG come punto di distribuzione cloud e per la gestione di contenuti da Archiviazione di Azure**. Per altre informazioni, vedere [Modify a CMG](../../clients/manage/cmg/setup-cloud-management-gateway.md#modify-a-cmg) (Modificare un gateway di gestione cloud).
>
> Non sarà possibile creare un punto di distribuzione cloud tradizionale in futuro. Per altre informazioni, vedere [Funzionalità rimosse e deprecate](../changes/deprecated/removed-and-deprecated-cmfeatures.md).

Un punto di distribuzione cloud è un punto di distribuzione di Configuration Manager ospitato come PaaS (piattaforma distribuita come servizio) in Microsoft Azure. Questo servizio supporta gli scenari seguenti:  

- Fornire contenuto software ai client basati su Internet senza infrastruttura locale aggiuntiva  

- Abilitare il sistema di distribuzione del contenuto per il cloud  

- Ridurre la necessità di punti di distribuzione tradizionali  

Questo articolo fornisce informazioni sul punto di distribuzione cloud, sulla pianificazione del suo utilizzo e sulla progettazione dell'implementazione. Include le sezioni seguenti:

- [Funzionalità e vantaggi](#bkmk_features)
- [Progettazione della topologia](#bkmk_topology)
- [Requirements](#bkmk_requirements)
- [Specifiche](#bkmk_spec)
- [Costi](#bkmk_cost)
- [Prestazioni e scalabilità](#bkmk_perf)
- [Porte e flusso di dati](#bkmk_dataflow)
- [Certificati](#bkmk_certs)
- [Domande frequenti](#bkmk_faq)


## <a name="features-and-benefits"></a><a name="bkmk_features"></a> Funzionalità e vantaggi

### <a name="features"></a>Caratteristiche

Il punto di distribuzione cloud supporta diverse funzionalità che sono offerte anche dai punti di distribuzione locali:  

- I punti di distribuzione cloud sono gestiti singolarmente o come membri di gruppi di punti di distribuzione  

- È possibile usare un punto di distribuzione cloud come percorso di fallback per il contenuto  

- Offre supporto per client basati su Internet e intranet  

### <a name="benefits"></a>Vantaggi

Il punto di distribuzione cloud offre i vantaggi aggiuntivi seguenti:  

- Il sito esegue la crittografia del contenuto prima di inviarlo al punto di distribuzione cloud in Azure.  

- Il servizio cloud può essere ridimensionato manualmente in Azure per adattarlo alle variazioni dei volumi delle richieste di contenuto dai client. Per questa operazione non è necessario installare ed effettuare il provisioning di punti di distribuzione aggiuntivi in Configuration Manager.  

- È supportato il download del contenuto da client configurati per altre tecnologie di gestione di contenuti, come Windows BranchCache e provider di contenuto alternativi.  

- A partire dalla versione 1806 è possibile usare i punti di distribuzione cloud come percorsi di origine per i punti di distribuzione pull.  


## <a name="topology-design"></a><a name="bkmk_topology"></a> Progettazione della topologia

La distribuzione e l'utilizzo del punto di distribuzione cloud includono i componenti seguenti:  

- Un **servizio cloud** in Azure. Il sito distribuisce contenuto a questo servizio, che lo memorizza nell'archiviazione cloud di Azure. Il punto di gestione fornisce ai client questo percorso del contenuto nell'elenco delle origini disponibili, secondo necessità.  

- Un ruolo del sistema del sito del **punto di gestione** risponde alle richieste del client normalmente.  

    - I client locali usano in genere un punto di gestione locale.  

    - I client basati su Internet usano un [gateway di gestione cloud](../../clients/manage/cmg/plan-cloud-management-gateway.md) o un [punto di gestione basato su Internet](../../clients/manage/plan-internet-based-client-management.md).  

- Il punto di distribuzione cloud usa un servizio Web **HTTPS basato sui certificati** per proteggere la comunicazione di rete con i client. I client devono considerare attendibile questo certificato.  

### <a name="azure-resource-manager"></a>Azure Resource Manager

<!--1322209-->
A partire dalla versione 1806, è possibile creare un punto di distribuzione cloud usando una **distribuzione Azure Resource Manager**. [Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) è una piattaforma moderna per la gestione di tutte le risorse di una soluzione come una singola entità detta [gruppo di risorse](/azure/azure-resource-manager/resource-group-overview#resource-groups). Quando si distribuisce un punto di distribuzione cloud con Azure Resource Manager, il sito usa Azure Active Directory (Azure AD) per autenticare e creare le risorse cloud necessarie. Questa distribuzione modernizzata non richiede il certificato di gestione classico di Azure.  

> [!Note]  
> Questa funzionalità non supporta i provider di servizi cloud di Azure. La distribuzione di punti di distribuzione cloud con Azure Resource Manager continua a usare il servizio cloud classico, non supportato dal provider di servizi cloud. Per altre informazioni, vedere [Available Azure services in Azure CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services) (servizi di Azure disponibili in Azure CSP).  

A partire da Configuration Manager versione 1902, Azure Resource Manager è l'unico meccanismo di distribuzione per le nuove istanze del punto di distribuzione cloud. Le distribuzioni esistenti continuano a funzionare normalmente.<!-- 3605704 -->

In Configuration Manager versione 1810 e precedenti la procedura guidata del punto di distribuzione cloud offre ancora l'opzione per una **distribuzione classica del servizio** tramite un certificato di gestione di Azure. Per semplificare la distribuzione e la gestione delle risorse, usare il modello di distribuzione Azure Resource Manager per tutti i nuovi punti di distribuzione cloud. Se possibile, ridistribuire i punti di distribuzione cloud esistenti tramite Resource Manager.

> [!Important]  
> A partire dalla versione 1810, la distribuzione classica del servizio in Azure è deprecata in Configuration Manager. Si tratta dell'ultima versione che supporta la creazione di queste distribuzioni di Azure. Questa funzionalità verrà rimossa in una versione futura di Configuration Manager.<!--SCCMDocs-pr issue #2993-->  

Configuration Manager non esegue la migrazione dei punti di distribuzione cloud classici esistenti nel modello di distribuzione Azure Resource Manager. Creare nuovi punti di distribuzione cloud usando distribuzioni di Azure Resource Manager e quindi rimuovere i punti di distribuzione cloud classici.

### <a name="hierarchy-design"></a>Progettazione della gerarchia

La posizione in cui si crea il punto di distribuzione cloud dipende da quali client dovranno accedere al contenuto. A partire dalla versione 1806, esistono tre tipi di punti di distribuzione cloud:  

- Distribuzione Azure Resource Manager: creare questo tipo in un sito primario o nel sito di amministrazione centrale.  

- Distribuzione classica del servizio: creare questo tipo solo in un sito primario.  

- Anche il gateway di gestione cloud può distribuire contenuti ai client. Questa funzionalità riduce i certificati necessari e i costi delle macchine virtuali di Azure. Per altre informazioni, vedere [Plan for cloud management gateway](../../clients/manage/cmg/plan-cloud-management-gateway.md) (Pianificare il gateway di gestione cloud).<!--1358651-->  

Per determinare se includere punti di distribuzione cloud nei gruppi di limiti, considerare i comportamenti seguenti:  

- I client basati su Internet non si basano sui gruppi di limiti. Usano solo punti di distribuzione con connessione Internet o punti di distribuzione cloud. Se si usano solo punti di distribuzione cloud per fornire servizi a questi tipi di client, non è necessario includerli in gruppi di limiti.  

- Se si desidera che i client nella rete interna usino un punto di distribuzione cloud, questo dovrà essere nello stesso gruppo di limiti dei client. I client danno priorità minima ai punti di distribuzione cloud nel loro elenco delle origini di contenuti, perché il download di contenuti da Azure comporta un costo. Quindi un punto di distribuzione cloud viene in genere usato come origine di fallback per i client basati su Intranet. Se si desidera dare la priorità al cloud, progettare i gruppi di limiti in modo da soddisfare questo requisito aziendale. Per altre informazioni, vedere [Configurare gruppi di limiti](../../servers/deploy/configure/boundary-groups.md).  

Anche se si installano punti di distribuzione cloud in specifiche aree di Azure, i client non tengono conto delle aree di Azure, ma selezionano un punto di distribuzione cloud in modo casuale. Se si installano punti di distribuzione cloud in più aree e un client riceve più punti nell'elenco dei percorsi del contenuto, il client potrebbe non usare un punto di distribuzione cloud della stessa area di Azure.  

### <a name="backup-and-recovery"></a>Backup e ripristino  

Quando si usa un punto di distribuzione cloud nella gerarchia, usare le informazioni seguenti per pianificare il backup e il ripristino:  

- Quando si usa l'attività di manutenzione **Backup server sito**, Configuration Manager include automaticamente le configurazione per il punto di distribuzione cloud.  

- Eseguire il backup e salvare una copia del certificato di autenticazione server. Se si usa la distribuzione classica del servizio in Azure, eseguire il backup e salvare una copia anche del certificato di gestione di Azure. Quando si ripristina il sito primario di Configuration Manager in un server diverso, è necessario reimportare i certificati.  


## <a name="requirements"></a><a name="bkmk_requirements"></a> Requisiti

- È necessaria una **sottoscrizione di Azure** per l'hosting del servizio.  

    - Un **amministratore di Azure** deve partecipare alla creazione iniziale di alcuni componenti, a seconda della progettazione. Questo utente tipo non necessita di autorizzazioni in Configuration Manager.  

- Il server del sito richiede l'**accesso a Internet** per distribuire e gestire il servizio cloud.  

- Quando si usa il metodo di distribuzione **Azure Resource Manager**, integrare Configuration Manager con [Azure AD](../../servers/deploy/configure/azure-services-wizard.md) per **Gestione cloud**. L'*individuazione utenti* di Azure AD non è necessaria.  

- Un **certificato di autenticazione server**. Per ulteriori informazioni, vedere la sezione [Certificati](#bkmk_certs) sottostante.  

    - Per ridurre il livello di complessità, usare un provider di certificati pubblico per il certificato di autenticazione server. In tal caso, è necessario anche un **alias CNAME del DNS** per consentire ai client di risolvere il nome del servizio cloud.  

- In Configuration Manager versione 1810 o precedenti con il metodo di distribuzione classico di Azure è necessario usare un **certificato di gestione di Azure**. Per ulteriori informazioni, vedere la sezione [Certificati](#bkmk_certs) sottostante.  

    > [!TIP]  
    > A partire da Configuration Manager versione 1806, usare il modello di distribuzione **Azure Resource Manager**, che non richiede il certificato di gestione.  
    >
    > Il metodo di distribuzione classica è deprecato a partire dalla versione 1810.  

- Impostare l'opzione del client **Consentire accesso al punto di distribuzione cloud** su **Sì** nel gruppo **Servizi cloud**. Per impostazione predefinita, questo valore è configurato su **No**.  

- I dispositivi client richiedono una **connessione a Internet** e devono usare il protocollo **IPv4**.  


## <a name="specifications"></a><a name="bkmk_spec"></a> Specifiche

- Il punto di distribuzione cloud supporta tutte le versioni di Windows elencate in [Sistemi operativi supportati per client e dispositivi ](../configs/supported-operating-systems-for-clients-and-devices.md).  

- Un amministratore distribuisce i tipi di contenuto software supportati seguenti:  
  - Applicazioni
  - Pacchetti
  - Pacchetti di aggiornamento del sistema operativo
  - Aggiornamenti software di terze parti  

    > [!Important]  
    > - Anche se la console di Configuration Manager non blocca la distribuzione degli aggiornamenti software Microsoft in un punto di distribuzione cloud, si sostengono costi di Azure per archiviare contenuto non usato dai client. I client basati su Internet ottengono sempre i contenuti di aggiornamento software Microsoft dal servizio cloud Microsoft Update. Evitare di distribuire gli aggiornamenti software Microsoft in un punto di distribuzione cloud.
    > - Quando si usa un CMG per l'archiviazione del contenuto, il contenuto per gli aggiornamenti di terze parti non verrà scaricato nei client se è abilitata l'[impostazione client](../../clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available) **Consenti ai client di scaricare contenuto differenziale quando disponibile**. <!--6598587--> 

- A partire dalla versione 1806, è possibile configurare un punto di distribuzione pull per usare un punto di distribuzione cloud come origine. Per altre informazioni, vedere [Informazioni sui punti di distribuzione di origine](use-a-pull-distribution-point.md#about-source-distribution-points).<!--1321554-->  

### <a name="deployment-settings"></a>Impostazioni di distribuzione

- **Scaricare il contenuto localmente quando necessario eseguendo la sequenza di attività**. A partire dalla versione 1910, il motore della sequenza di attività può scaricare pacchetti su richiesta da un servizio CMG abilitato per il contenuto o da un punto di distribuzione cloud. Questa modifica offre ulteriore flessibilità con le distribuzioni di aggiornamento sul posto di Windows 10 ai dispositivi basati su Internet.

- **Scaricare tutto il contenuto in locale prima di avviare la sequenza di attività**. In Configuration Manager versione 1906 e precedenti, altre opzioni come **Scaricare il contenuto localmente quando necessario eseguendo la sequenza di attività** non sono applicabili a questo scenario. Il motore della sequenza di attività non può scaricare il contenuto da un'origine cloud. Il client Gestione configurazione deve scaricare il contenuto dall'origine cloud prima di avviare la sequenza di attività. È comunque possibile usare questa opzione nella versione 1910, se necessario, per soddisfare i requisiti.

- Un punto di distribuzione cloud non supporta le distribuzioni di pacchetti con l'opzione **Esegui programma dal punto di distribuzione**. Usare l'opzione di distribuzione **Scarica il contenuto dal punto di distribuzione ed esegui in locale**.  

### <a name="limitations"></a>Limitazioni  

- Non è possibile usare un punto di distribuzione cloud per distribuzioni abilitate per PXE o per il multicast.  

- Un punto di distribuzione cloud non supporta lo streaming di applicazioni con App-V.  

- Non è possibile [pre-installare il contenuto](manage-network-bandwidth.md#BKMK_PrestagingContent) in un punto di distribuzione cloud. La gestione distribuzione del sito primario che gestisce il punto di distribuzione cloud trasferisce tutto il contenuto.  

- Non è possibile configurare un punto di distribuzione cloud come punto di distribuzione pull.  


## <a name="cost"></a><a name="bkmk_cost"></a> Costi

<!--501018-->
> [!IMPORTANT]  
> Le informazioni sui costi seguenti sono puramente stime. Altre variabili dell'ambiente possono influire sul costo complessivo dell'uso di un punto di distribuzione cloud.  

Configuration Manager include le opzioni seguenti per il controllo dei costi e il monitoraggio dell'accesso ai dati:  

- È possibile controllare e monitorare la quantità dei contenuti archiviati in un servizio cloud. Per altre informazioni, vedere la sezione sul [monitoraggio dei punti di distribuzione cloud](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md#bkmk_monitor).  

- È possibile configurare Configuration Manager in modo che avvisi l'utente quando le soglie per i download del client raggiungono o superano i limiti mensili. Per altre informazioni, vedere la sezione sugli [avvisi di soglia di trasferimento dati](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md#bkmk_alerts).

- Per ridurre il numero di trasferimenti di dati dai punti di distribuzione cloud eseguiti dai client, è possibile usare una delle tecnologie di peer caching seguenti:  
  - Peer cache di Configuration Manager
  - Windows BranchCache
  - Ottimizzazione recapito per Windows 10  

    Per altre informazioni su BranchCache, vedere [Fundamental concepts for content management](fundamental-concepts-for-content-management.md) (Concetti di base per la gestione dei contenuti).  

### <a name="components"></a>Componenti

Un punto di distribuzione cloud usa i componenti di Azure seguenti, che implicano l'addebito di costi all'account della sottoscrizione di Azure:  

> [!Tip]  
> A partire dalla versione 1806, anche il gateway di gestione cloud può distribuire contenuti ai client. Questa funzionalità riduce i costi consolidando le macchine virtuali di Azure. Per altre informazioni, vedere i [costi per il gateway di gestione cloud](../../clients/manage/cmg/plan-cloud-management-gateway.md#cost).  

#### <a name="virtual-machine"></a>Macchina virtuale

- Il punto di distribuzione cloud usa i servizi cloud di Azure come PaaS (piattaforma distribuita come servizio). Questo servizio usa macchine virtuali che comportano costi di calcolo.  

- Ogni servizio del punto di distribuzione cloud usa due macchine virtuali A0 Standard.  

- Vedere il [calcolatore dei prezzi di Azure](https://azure.microsoft.com/pricing/calculator/) per determinare i costi potenziali.

    > [!NOTE]  
    > I costi delle macchine virtuali variano a seconda dell'area.

#### <a name="outbound-data-transfer"></a>Trasferimento dati in uscita

- I flussi di dati verso Azure sono gratuiti (dati in ingresso o caricamento). La distribuzione di contenuti dal sito al punto di distribuzione cloud è un caricamento in Azure.  

- Gli addebiti si basano sul flusso di dati in uscita da Azure (dati in uscita o download). I flussi di dati del punto di distribuzione cloud da Azure sono costituiti dal contenuto software scaricato dai client.  

- Per altre informazioni, vedere la sezione sul [monitoraggio dei punti di distribuzione cloud](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md#bkmk_monitor).  

- Vedere i [dettagli sui prezzi per la larghezza di banda di Azure](https://azure.microsoft.com/pricing/details/bandwidth/) per determinare i costi potenziali. I prezzi del trasferimento dei dati sono diversificati. Un maggior utilizzo comporta un costo minore per gigabyte.  

#### <a name="content-storage"></a>Archivio del contenuto

- I client basati su Internet ricevono i contenuti di aggiornamento del software Microsoft dal servizio cloud Microsoft Update gratuitamente. Evitare di distribuire pacchetti di distribuzione di aggiornamenti software con gli aggiornamenti del software Microsoft a un punto di distribuzione cloud. In caso contrario, si dovranno sostenere costi di archiviazione dati per contenuto mai usato dai client.  

- I punti di distribuzione cloud usano gli archivi BLOB standard seguenti in base al modello di distribuzione:  

    - Una distribuzione di Azure Resource Manager usa l'archiviazione di Azure con ridondanza locale. Questa modifica riduce il costo dell'account di archiviazione. La distribuzione classica non usava le funzionalità aggiuntive di archiviazione con ridondanza geografica. Per altre informazioni, vedere [Archiviazione con ridondanza locale](/azure/storage/common/storage-redundancy-lrs).  

    - Una distribuzione classica con Configuration Manager versione 1810 o precedente usa l'archiviazione con ridondanza geografica di Azure. Per altre informazioni, vedere [Archiviazione con ridondanza geografica](/azure/storage/common/storage-redundancy-grs).  

#### <a name="other-costs"></a>Altri costi

- Ogni servizio cloud ha un indirizzo IP dinamico. Ogni punto di distribuzione cloud distinto usa un nuovo indirizzo IP dinamico. L'aggiunta di macchine virtuali per il servizio cloud non aumenta il numero di indirizzi.  


## <a name="ports-and-data-flow"></a><a name="bkmk_dataflow"></a> Porte e flusso di dati

Vi sono due flussi di dati primari per il punto di distribuzione cloud:  

- Il server del sito si connette ad Azure per configurare il servizio del punto di distribuzione cloud  

- Un client si connette al punto di distribuzione cloud per scaricare contenuti  

### <a name="site-server-to-azure"></a>Da server del sito ad Azure

Non è necessario aprire alcuna porta in ingresso per la rete locale. Il server del sito avvia tutte le comunicazioni con Azure e con il punto di distribuzione cloud per distribuire, aggiornare e gestire il servizio cloud. Il server del sito deve creare connessioni in uscita verso il cloud Microsoft. Ciò equivale a installare il ruolo del sistema del sito del punto di distribuzione in un sito specifico.  

### <a name="client-to-cloud-distribution-point"></a>Da client a punto di distribuzione cloud

Non è necessario aprire alcuna porta in ingresso per la rete locale. I client basati su Internet comunicano direttamente con il servizio di Azure. I client nella rete interna che usano un punto di distribuzione cloud devono connettersi al cloud Microsoft.

Per altre informazioni sulla priorità dei percorsi dei contenuti e sui casi in cui i client basati su intranet usano un punto di distribuzione cloud, vedere [Content source priority](fundamental-concepts-for-content-management.md#content-source-priority) (Priorità delle origini dei contenuti).

Quando un client usa un punto di distribuzione cloud come percorso del contenuto:  

1. Il punto di gestione fornisce al client un token di accesso insieme all'elenco delle origini dei contenuti. Il token è valido per 24 ore e consente al client l'accesso al punto di distribuzione cloud.  

2. Il punto di gestione risponde alla richiesta di percorso del client con il **nome di dominio completo del servizio** del punto di distribuzione cloud. Questa proprietà corrisponde al nome comune del certificato di autenticazione server.  

    Se si usa il proprio nome di dominio, ad esempio WallaceFalls.contoso.com, il client tenta innanzitutto di risolvere questo FQDN. È necessario un alias CNAME nel DNS con connessione internet del proprio dominio per consentire ai client di risolvere il nome del servizio di Azure, ad esempio: WallaceFalls.cloudapp.net.  

3. Il client quindi risolve il nome del servizio di Azure, ad esempio WallaceFalls.cloudapp.net, in un indirizzo IP valido. Questa risposta deve essere gestita dal DNS di Azure.  

4. Il client si connette al punto di distribuzione cloud. Azure bilancia il carico della connessione a una delle istanze di VM. Il client si autentica usando il token di accesso.  

5. Il punto di distribuzione cloud autentica il token di accesso del client e quindi fornisce al client la posizione esatta del contenuto nell'archiviazione di Azure.  

6. Se il client considera attendibile il certificato di autenticazione server del punto di distribuzione cloud, si connette all'archiviazione di Azure per scaricare il contenuto.


## <a name="performance-and-scale"></a><a name="bkmk_perf"></a> Prestazioni e scalabilità

<!--494872-->

Come con qualsiasi progettazione dei punti di distribuzione, prendere in considerazione i fattori seguenti:  

- Numero di connessioni client simultanee
- Dimensioni del contenuto scaricato dai client
- Il tempo disponibile per soddisfare i requisiti aziendali

A seconda della [progettazione della topologia](#bkmk_topology), se i client hanno la scelta tra più punti di distribuzione cloud per un dato contenuto, selezioneranno in modo casuale uno dei servizi cloud. Se si distribuisce un determinato contenuto in un solo punto di distribuzione cloud e un gran numero di client tenta di scaricare questo contenuto allo stesso tempo, questa attività sottopone quel singolo punto di distribuzione cloud a un carico maggiore. Quando si aggiunge un punto di distribuzione cloud, viene incluso anche un servizio di archiviazione di Azure separato. Per altre informazioni sul modo in cui il client comunica con i componenti del punto di distribuzione cloud e scarica il contenuto, vedere [Porte e flusso di dati](#bkmk_dataflow).  

Il punto di distribuzione cloud usa due macchine virtuali di Azure come front-end per l'archiviazione di Azure. Questa distribuzione predefinita soddisfa la maggior parte delle esigenze dei clienti. In alcuni casi estremi, con un numero elevato di connessioni client simultanee (ad esempio, 150.000 client), la capacità di elaborazione delle macchine virtuali di Azure non riesce a gestire le richieste dei client. Non è possibile ridimensionare le macchine virtuali di Azure usate per il punto di distribuzione cloud. Non è possibile configurare il numero di istanze di macchine virtuali per il punto di distribuzione cloud in Configuration Manager. Se necessario, è comunque possibile riconfigurare il servizio cloud nel portale di Azure, aggiungendo manualmente altre istanze di macchine virtuali oppure configurando la scalabilità automatica del servizio.

> [!Important]  
> Quando si aggiorna Configuration Manager, il sito ridistribuisce il servizio cloud. Se si riconfigura manualmente il servizio cloud nel portale di Azure, il numero di istanze viene reimpostato sul valore predefinito di due.  

Il servizio di archiviazione di Azure supporta 500 richieste al secondo per un singolo file. In un test delle prestazioni, un singolo punto di distribuzione cloud ha supportato la distribuzione di un unico file da 100 MB a 50.000 client in 24 ore.<!--512106-->  


## <a name="certificates"></a><a name="bkmk_certs"></a> Certificati  

A seconda della progettazione del punto di distribuzione cloud, sono necessari uno o più certificati digitali.  

### <a name="general-information"></a>Informazioni generali

<!--SCCMDocs issue #779-->
I certificati per i punti di distribuzione cloud supportano le configurazioni seguenti:  

- Lunghezza della chiave 4096 bit

- Certificati versione 3 Per altre informazioni, vedere [Panoramica dei certificati CNG](../network/cng-certificates-overview.md).  

- A partire dalla versione 1802, quando si configura Windows con i criteri seguenti: **Crittografia di sistema: utilizza algoritmi FIPS compatibili per crittografia, hash e firma**  

- A partire dalla versione 1802, supporto per TLS 1.2. Per altre informazioni, vedere [Riferimento tecnico per i controlli crittografici](../security/cryptographic-controls-technical-reference.md#about-ssl-vulnerabilities).  

### <a name="server-authentication-certificate"></a>Certificato di autenticazione server

*Questo certificato è necessario per tutte le distribuzioni di punti di distribuzione cloud.*

Per altre informazioni, vedere [Certificato di autenticazione server del gateway di gestione cloud](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_serverauth) e le sottosezioni seguenti, come necessario:  

- Certificato radice trusted del gateway di gestione cloud per i client
- Certificato di autenticazione server rilasciato da un provider pubblico
- Certificato di autenticazione server rilasciato da un'infrastruttura a chiave pubblica di tipo Enterprise

Il punto di distribuzione cloud usa questo tipo di certificato nello stesso modo del gateway di gestione cloud. Anche i client devono considerare attendibile questo certificato. Per ridurre la complessità, Microsoft consiglia di usare un certificato rilasciato da un provider pubblico.

A meno di non usare un certificato con caratteri jolly, non riusare lo stesso certificato. Ogni istanza del punto di distribuzione cloud e del gateway di gestione cloud richiede un certificato di autenticazione server univoco.

Per altre informazioni sulla creazione di questo certificato da un'infrastruttura PKI, vedere [Distribuire il certificato di servizio per i punti di distribuzione basati su cloud](../network/example-deployment-of-pki-certificates.md#BKMK_clouddp2008_cm2012).  

### <a name="azure-management-certificate"></a>Certificato di gestione di Azure

*Questo certificato è obbligatorio per le distribuzioni di servizi classiche. Non è necessario per le distribuzioni di Azure Resource Manager.*

> [!Important]  
> A partire da Configuration Manager versione 1806, usare il modello di distribuzione **Azure Resource Manager**, che non richiede il certificato di gestione.  
>
> Il metodo di distribuzione classica è deprecato a partire dalla versione 1810.  
>
> A partire da Configuration Manager versione 1902, Azure Resource Manager è l'unico meccanismo di distribuzione per le nuove istanze del punto di distribuzione cloud. Questo certificato non è necessario in Configuration Manager versione 1902 o successive.<!-- 3605704 -->

Se si usa il metodo di distribuzione classico di Azure con Configuration Manager versione 1810 o precedenti, è necessario usare un **certificato di gestione di Azure**. Per altre informazioni, vedere la sezione [Certificato di gestione di Azure](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_azuremgmt) dell'articolo sui certificati per il gateway di gestione cloud. Il server del sito di Configuration Manager usa questo certificato per autenticarsi con Azure per creare e gestire la distribuzione classica.  

Per ridurre la complessità, usare lo stesso certificato di gestione di Azure per tutte le distribuzioni classiche di punti di distribuzione cloud e gateway di gestione cloud, con tutte le sottoscrizioni di Azure e tutti i siti di Configuration Manager.


## <a name="frequently-asked-questions-faq"></a><a name="bkmk_faq"></a> Domande frequenti

### <a name="does-a-client-need-a-certificate-to-download-content-from-a-cloud-distribution-point"></a>Un client necessita di un certificato per scaricare contenuti da un punto di distribuzione cloud?

Non è necessario un certificato di autenticazione client. Il client deve considerare attendibile il certificato di autenticazione server usato dal punto di distribuzione cloud. Se questo certificato è rilasciato da un provider di certificati pubblico, la maggior parte dei dispositivi Windows include già i certificati radice trusted per tali provider. Se è stato emesso un certificato di autenticazione server dall'infrastruttura PKI dell'organizzazione, i clienti devono considerare attendibili le certificazioni dell'intera catena. Questa catena include l'autorità di certificazione radice e tutte le autorità di certificazione intermedie. A seconda della progettazione dell'infrastruttura PKI, questo certificato può introdurre complessità aggiuntive nella distribuzione del punto di distribuzione cloud. Per evitare questa complessità, Microsoft consiglia di usare un provider di certificati pubblici che i client considerano già attendibile.  

### <a name="can-my-on-premises-clients-use-a-cloud-distribution-point"></a>I client locali possono usare un punto di distribuzione cloud?

Sì. Se si desidera che i client nella rete interna usino un punto di distribuzione cloud, questo dovrà essere nello stesso gruppo di limiti dei client. I client danno priorità minima ai punti di distribuzione cloud nel loro elenco delle origini di contenuti, perché il download di contenuti da Azure comporta un costo. Quindi un punto di distribuzione cloud viene in genere usato come origine di fallback per i client basati su Intranet. Se si desidera dare la priorità al cloud, progettare i gruppi di limiti di conseguenza. Per altre informazioni, vedere [Configurare gruppi di limiti](../../servers/deploy/configure/boundary-groups.md).  

### <a name="do-i-need-azure-expressroute"></a>È necessario Microsoft Azure ExpressRoute?

[Microsoft Azure ExpressRoute](/azure/expressroute/expressroute-introduction) consente di estendere la rete locale nel cloud Microsoft. Microsoft Azure ExpressRoute o altre connessioni di rete virtuale simili non sono necessari per il punto di distribuzione cloud di Configuration Manager.  

Se l'organizzazione usa ExpressRoute, isolare la sottoscrizione di Azure per il punto di distribuzione cloud dalla sottoscrizione che usa ExpressRoute. Questa configurazione assicura che il punto di distribuzione cloud non sia connesso accidentalmente in questo modo.  

### <a name="do-i-need-to-maintain-the-azure-virtual-machines"></a>È necessario gestire le macchine virtuali di Azure?

Non è necessaria alcuna manutenzione. La progettazione del punto di distribuzione cloud usa Azure come PaaS (piattaforma come servizio). Tramite la sottoscrizione offerta dall'utente, Configuration Manager crea le macchine virtuali, le risorse di archiviazione e la rete necessari. Azure protegge e aggiorna le macchine virtuali. Queste macchine virtuali non fanno parte dell'ambiente locale, come accade con l'infrastruttura come servizio (IaaS). Il punto di distribuzione cloud è un PaaS che estende l'ambiente di Configuration Manager nel cloud. Per altre informazioni, vedere [Vantaggi di sicurezza di un modello di servizio cloud PaaS](/azure/security/security-paas-deployments#security-advantages-of-a-paas-cloud-service-model).  

### <a name="does-the-cloud-distribution-point-use-azure-cdn"></a>Il punto di distribuzione cloud usa la rete CDN di Azure?

La rete per la distribuzione di contenuti (CDN) di Azure è una soluzione globale per distribuire rapidamente contenuto con larghezza di banda elevata memorizzandolo nella cache di nodi fisici posizionati strategicamente in tutto il mondo. Per ulteriori informazioni, vedere [Definizione di rete per la distribuzione di contenuti](/azure/cdn/cdn-overview).

Il punto di distribuzione cloud di Configuration Manager non supporta attualmente la rete CDN di Azure.


## <a name="next-steps"></a>Passaggi successivi

[Installare punti di distribuzione basati sul cloud](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md)