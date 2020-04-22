---
title: Informazioni dettagliate sulla gestione
titleSuffix: Configuration Manager
description: Informazioni sulla funzionalità Informazioni dettagliate sulla gestione disponibile nella console di Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a79f83be-884c-48e6-94d6-ed0a68c22e2f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e9aae1da48deabd0cc339cd25055827caf07354b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694449"
---
# <a name="management-insights-in-configuration-manager"></a>Informazioni dettagliate sulla gestione in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

La funzionalità Informazioni dettagliate sulla gestione in Configuration Manager offre indicazioni utili sullo stato corrente dell'ambiente. Le informazioni si basano sull'analisi dei dati presenti nel database del sito. Le informazioni dettagliate aiutano a capire meglio l'ambiente e a intervenire di conseguenza. <!--1353967-->

## <a name="review-management-insights"></a>Esaminare le informazioni dettagliate sulla gestione

Per visualizzare le regole, l'account deve disporre dell'autorizzazione di **lettura** per l'oggetto **sito**.

1. Aprire la console di Configuration Manager.  

2. Nell'area di lavoro **Amministrazione** espandere **Informazioni dettagliate sulla gestione** e selezionare **Tutte le informazioni dettagliate**.  

    > [!Note]  
    > Quando si seleziona il nodo **Informazioni dettagliate sulla gestione** viene visualizzato il [Dashboard di informazioni dettagliate sulla gestione](#bkmk_insights).  

3. Aprire il nome del gruppo di informazioni dettagliate sulla gestione che si vuole esaminare. Selezionare **Mostra le informazioni dettagliate** nella barra multifunzione.  

È possibile esaminare le quattro schede seguenti:

- **Tutte le regole**: offre l'elenco completo delle regole per il gruppo di informazioni dettagliate di gestione scelto.  

- **Completa**:  elenca le regole in cui non è necessaria alcuna azione.  

- **In corso**: mostra le regole in cui alcuni, ma non tutti i prerequisiti sono soddisfatti.  

- **Azione richiesta**: sono elencate le regole che richiedono le azioni adottate. Scegliere **Altri dettagli** per recuperare elementi specifici in cui è necessaria un'azione.  

Nel riquadro **Prerequisiti** sono elencati gli elementi obbligatori per eseguire la regola.

### <a name="all-rules-and-prerequisites-for-the-cloud-services-group"></a>Tutte le regole e i prerequisiti per il gruppo di servizi cloud

![Informazioni dettagliate sulla gestione- Tutte le regole e i prerequisiti per il gruppo di servizi cloud](./media/Management-insights-all-cloud-rules.png)

Selezionare una regola e quindi selezionare **Altri dettagli** per visualizzarne i dettagli.

## <a name="operations"></a>Operazioni

Le regole delle informazioni dettagliate sulla gestione rivalutano la loro applicabilità a una pianificazione settimanale. Per valutare nuovamente una regola su richiesta, fare clic con il pulsante destro del mouse sulla regola e selezionare **Valuta di nuovo**.

Il file di log per le regole di Informazioni dettagliate sulla gestione è **SMS_DataEngine.log** ed è disponibile nel server del sito.

<!--1357930-->
Alcune regole consentono di intervenire. Selezionare una regola, selezionare **Altri dettagli** e quindi, se disponibile, selezionare **Intervieni**.

A seconda della regola, questa azione presenta uno dei comportamenti seguenti:  

- Passare direttamente nella console al nodo in cui è possibile eseguire ulteriori azioni. Ad esempio, se le informazioni dettagliate sulla gestione consigliano di modificare un'impostazione client, l'opzione per eseguire un'azione consente di passare al nodo Impostazioni client. Eseguire quindi ulteriori azioni modificando l'impostazione predefinita o un oggetto impostazioni client personalizzato.  

- Passare a una visualizzazione filtrata in base a una query. Ad esempio, eseguire l'azione per la regola delle raccolte vuote mostra semplicemente queste raccolte nell'elenco delle raccolte. Eseguire quindi eseguire ulteriori azioni, ad esempio eliminare una raccolta o modificarne le regole di appartenenza.  

## <a name="management-insights-dashboard"></a><a name="bkmk_insights"></a> Dashboard delle informazioni dettagliate sulla gestione

<!--1357979-->

Il nodo **Informazioni dettagliate sulla gestione** include un dashboard grafico. Questo dashboard visualizza una panoramica degli stati delle regole che rende più semplice visualizzare lo stato di avanzamento.

Usare i filtri seguenti nella parte superiore del dashboard per ottimizzare la visualizzazione:

- Mostra completate
- Facoltativo
- Consigliato
- Critico

Il dashboard include i riquadri seguenti:  

- **Indice informazioni dettagliate sulla gestione**: registra l'avanzamento generale delle regole delle informazioni dettagliate sulla gestione. L'indice è una media ponderata. Le regole critiche hanno maggior valore. Questo indice assegna il minor peso alle regole facoltative.  

- **Gruppi di informazioni dettagliate sulla gestione**: mostra la percentuale di regole di ogni gruppo che soddisfa i filtri. Selezionare un gruppo per eseguire il drill-down nelle regole specifiche del gruppo.  

- **Priorità delle informazioni dettagliate sulla gestione**: mostra la percentuale di regole in base alla priorità che soddisfa i filtri.  

- **Tutte le informazioni dettagliate sulla gestione**: tabella delle informazioni dettagliate con priorità e stato. Usare il campo **Filtro** nella parte superiore della tabella per la corrispondenza con stringhe in una qualsiasi delle colonne disponibili. Il dashboard consente di ordinare la tabella nell'ordine seguente:

  - Stato: Azione necessaria, Completato, Sconosciuto  
  - Priorità: Critico, Consigliato, Facoltativo  
  - Ultima modifica: le date meno recenti sono visualizzate all'inizio  

![Screenshot del dashboard delle informazioni dettagliate sulla gestione](media/1357979-management-insights-dashboard.png)

## <a name="groups-and-rules"></a>Gruppi e regole

Le regole sono organizzate nei seguenti gruppi di informazioni dettagliate sulla gestione:

- [Applicazioni](#applications)
- [Servizi cloud](#cloud-services)
- [raccolte](#collections)
- [Valutazione di Configuration Manager](#configuration-manager-assessment)
- [Manutenzione proattiva](#proactive-maintenance)
- [Security](#security)
- [Gestione semplificata](#simplified-management)
- [Software Center](#software-center)
- [Windows 10](#windows-10)

### <a name="applications"></a>Applicazioni

Informazioni dettagliate per la gestione delle applicazioni.

- **Applicazioni senza distribuzioni**: elenca le applicazioni dell'ambiente senza distribuzioni attive. Questa regola aiuta a individuare ed eliminare le applicazioni non usate per semplificare l'elenco di applicazioni visualizzato nella console. Per altre informazioni, vedere l'argomento relativo alla [distribuzione delle applicazioni](../../../apps/deploy-use/deploy-applications.md).  

### <a name="cloud-services"></a>Servizi cloud

Facilita l'integrazione con molti servizi cloud per una gestione moderna dei dispositivi.

- **Valuta l'idoneità per la co-gestione**: consente di comprendere i passaggi necessari per abilitare la co-gestione. Questa regola ha dei prerequisiti. Per altre informazioni, vedere la [panoramica sulla co-gestione](../../../comanage/overview.md).  

- **Dispositivi non caricati in Azure AD**: a partire dalla versione 2002, questa regola elenca i dispositivi che non vengono caricati in Azure AD perché il sito non è configurato correttamente per HTTPS.<!--6268489--> Configurare [HTTP avanzato](../../plan-design/hierarchy/enhanced-http.md) o abilitare almeno un punto di gestione per HTTPS. Se il sito è già stato configurato per la comunicazione HTTPS, questa regola non viene visualizzata.

- **Configura i servizi di Azure per l'uso con Configuration Manager**: questa regola consente di eseguire l'onboarding di Configuration Manager in Azure AD, in modo che i client possano usare Azure AD per eseguire l'autenticazione nel sito. Per altre informazioni, vedere [Configurare i servizi di Azure](../deploy/configure/azure-services-wizard.md).  

- **Consenti dispositivi ibridi aggiunti ad Azure Active Directory**: i dispositivi aggiunti ad Azure AD consentono agli utenti di accedere con le credenziali del dominio garantendo al contempo che i dispositivi soddisfino gli standard di sicurezza e conformità dell'organizzazione. Per altre informazioni, vedere [Considerazioni di progettazione dell'identità ibrida di Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-overview).  

- **Siti senza configurazione HTTPS appropriata**: a partire dalla versione 2002, questa regola elenca i siti nella gerarchia che non sono configurati correttamente per HTTPS. Questa configurazione impedisce al sito di [sincronizzare i risultati di appartenenza alla raccolta con i gruppi di Azure Active Directory (Azure AD)](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync). Di conseguenza, è possibile che AD Sync non carichi tutti i dispositivi. La gestione di questi client potrebbe non funzionare correttamente.<!--6268489--> Configurare [HTTP avanzato](../../plan-design/hierarchy/enhanced-http.md) o abilitare almeno un punto di gestione per HTTPS. Se il sito è già stato configurato per la comunicazione HTTPS, questa regola non viene visualizzata.

- **Aggiorna i client alla versione più recente di Windows 10**: Windows 10, versione 1709 o versioni successive, migliora e modernizza l'esperienza di elaborazione degli utenti. Per altre informazioni, vedere [Articoli principali sull'adozione di Windows as a Service](../../understand/configuration-manager-and-windows-as-service.md#key-articles-about-adopting-windows-as-a-service).  

### <a name="collections"></a>Raccolte

Informazioni dettagliate che consentono di semplificare la gestione tramite la pulizia e la riconfigurazione delle raccolte.

- **Raccolte vuote**: un elenco delle raccolte dell'ambiente che non hanno membri. Per altre informazioni, vedere [Come gestire le raccolte](../../clients/manage/collections/manage-collections.md).  

A partire dalla versione 1902, sono disponibili nuove regole con raccomandazioni per la gestione delle raccolte.<!--3555752--> Usare queste informazioni dettagliate per semplificare la gestione e migliorare le prestazioni:

- **Raccolte senza regole di query e senza membri diretti**: per semplificare l'elenco di raccolte nella gerarchia, eliminare queste raccolte.  

- **Raccolte con la stessa ora di inizio di rivalutazione**: queste raccolte hanno la stessa ora di rivalutazione di altre raccolte. Modificare l'ora di rivalutazione in modo da evitare conflitti.  

- **Raccolte con tempo di query di oltre due secondi**: rivedere le regole di query per queste raccolte. Prendere in considerazione di modificarle o eliminarle.

- Le regole seguenti includono alcune configurazioni che possono causare un carico non necessario del sito. Rivedere queste raccolte e quindi eliminarle oppure disabilitare la valutazione delle regole:  

  - **Raccolte senza regole di query e con gli aggiornamenti incrementali abilitati**  

  - **Raccolte senza regole di query e abilitate per la valutazione pianificata o incrementale**  

  - **Raccolte senza regole di query e con pianificazione della valutazione completa selezionata**  

### <a name="configuration-manager-assessment"></a>Valutazione di Configuration Manager

<!--3607758-->

A partire dalla versione 2002, questo gruppo è gentilmente fornito da gentilmente fornite da Microsoft Premier Field Engineering. Queste regole sono un esempio dei molti altri controlli forniti da Microsoft Premier nell'[hub Servizi](https://docs.microsoft.com/services-hub/health/getting_started_with_on_demand_assessments).

- **La configurazione di Individuazione gruppo di protezione Active Directory prevede un'esecuzione troppo frequente**: Non è in genere necessario configurare Individuazione gruppo di protezione Active Directory con una ricorrenza superiore a ogni tre ore. Una configurazione più frequente può avere un impatto negativo sulle prestazioni di Active Directory, della rete e di Configuration Manager. Abilitare la sincronizzazione incrementale invece di usare una pianificazione della sincronizzazione completa. Per altre informazioni, vedere [Individuazione gruppo Active Directory](../deploy/configure/about-discovery-methods.md#bkmk_aboutGroup).

- **La configurazione di Individuazione sistema Active Directory prevede un'esecuzione troppo frequente**: non è in genere necessario configurare Individuazione sistema Active Directory con una ricorrenza superiore a ogni tre ore. Una configurazione più frequente può avere un impatto negativo sulle prestazioni di Active Directory, della rete e di Configuration Manager. Abilitare la sincronizzazione incrementale invece di usare una pianificazione della sincronizzazione completa. Per altre informazioni, vedere [Individuazione sistema Active Directory](../deploy/configure/about-discovery-methods.md#bkmk_aboutSystem).

- **La configurazione di Individuazione utente Active Directory prevede un'esecuzione troppo frequente**: Non è in genere necessario configurare Individuazione utente Active Directory con una ricorrenza superiore a ogni tre ore. Una configurazione più frequente può avere un impatto negativo sulle prestazioni di Active Directory, della rete e di Configuration Manager. Abilitare la sincronizzazione incrementale invece di usare una pianificazione della sincronizzazione completa. Per altre informazioni, vedere [Individuazione utente Active Directory](../deploy/configure/about-discovery-methods.md#bkmk_aboutUser).

- **Raccolte limitate a Tutti i sistemi o Tutti gli utenti**: consente di esaminare eventuali raccolte che usano le raccolte **Tutti i sistemi** o **Tutti gli utenti** come raccolta di delimitazione. Configuration Manager aggiorna l'appartenenza di queste raccolte predefinite con dati dai metodi di individuazione di Active Directory. È possibile che questi dati non siano informazioni valide per i client di Configuration Manager.

- **L'opzione Individuazione heartbeat è disabilitata**: per l'individuazione heartbeat è necessario installare il client di Configuration Manager nei dispositivi. Si tratta dell'unico metodo di individuazione avviato dai client. Tutti gli altri metodi vengono applicati nei server del sito. L'individuazione heartbeat è essenziale per mantenere aggiornato lo stato di attività dei client. Garantisce che il sito non renda inavvertitamente obsoleti i record di risorse dal database del sito. Per altre informazioni, vedere [Individuazione heartbeat](../deploy/configure/about-discovery-methods.md#bkmk_aboutHeartbeat).

- **Query su raccolte a esecuzione prolungata abilitate per gli aggiornamenti incrementali**: le raccolte con durata dell'ultimo aggiornamento incrementale superiore a 30 secondi usano risorse del server del sito e del database che potrebbero potenzialmente influire sulle prestazioni complessive di Configuration Manager. Per altre informazioni, vedere [Procedure consigliate per le raccolte](../../clients/manage/collections/best-practices-for-collections.md).

- **Riduci il numero di applicazioni e pacchetti nei punti di distribuzione**: Microsoft supporta ufficialmente un totale combinato di massimo 10.000 pacchetti e applicazioni per un punto di distribuzione. Il superamento di questo totale può causare problemi operativi. Per altre informazioni, vedere [Numeri di ridimensionamento e scalabilità - punto di distribuzione](../../plan-design/configs/size-and-scale-numbers.md#distribution-point).

- **Problemi di installazione dei siti secondari**: lo stato di installazione di alcuni siti secondari è **In sospeso** o **Errore**. Questi stati indicano che l'installazione è stata avviata ma non è stata completata. Fino al completamento dell'installazione dei siti secondari, è possibile che i client non comunichino correttamente con il sito primario. Controllare l'area di lavoro **Monitoraggio** e ritentare l'installazione. Per altre informazioni, vedere [Ripetere l'installazione di un aggiornamento non riuscito](install-in-console-updates.md#bkmk_retry) .

- **Aggiorna tutti i siti alla stessa versione**: usare la stessa versione di Configuration Manager in una gerarchia. Questa configurazione garantisce che tutti i siti offrano le stesse funzionalità. I siti di versioni diverse nella stessa gerarchia introducono scenari di interoperabilità. Nelle versioni successive di Configuration Manager sono incluse nuove funzionalità e vengono risolti problemi noti. Per altre informazioni, vedere [Interoperabilità tra versioni diverse](../../plan-design/hierarchy/interoperability-between-different-versions.md).

Per altre informazioni su queste regole, vedere [Procedure di correzione per ConfigMgr Management Insights](https://docs.microsoft.com/services-hub/health/remediation-steps-configmgr).

> [!TIP]
> I clienti di Microsoft Unified o Microsoft Premier possono accedere all'[hub Servizi](https://serviceshub.microsoft.com/assessments/) per ulteriori valutazioni su richiesta.
>
> Per altre informazioni sui servizi Microsoft, vedere le [soluzioni di supporto tecnico](https://www.microsoft.com/enterprise/services/support).

### <a name="proactive-maintenance"></a>Manutenzione proattiva

<!--1352184-->
Le regole in questo gruppo evidenziano potenziali problemi di configurazione che possono essere evitati tramite la manutenzione degli oggetti di Configuration Manager.

- **Gruppi di limiti senza sistemi del sito assegnati**: senza sistemi del sito assegnati, i gruppi di limiti possono essere usati solo per l'assegnazione del sito. Per altre informazioni, vedere [Configurare gruppi di limiti](../deploy/configure/boundary-groups.md).  

- **Gruppi di limiti senza membri**: i gruppi di limiti non sono applicabili per l'assegnazione del sito o la ricerca di contenuto se non hanno membri. Per altre informazioni, vedere [Configurare gruppi di limiti](../deploy/configure/boundary-groups.md).  

- **Punti di distribuzione che non forniscono contenuti ai client**: punti di distribuzione che non hanno reso disponibile contenuto ai client negli ultimi 30 giorni. I dati sono basati sui report dai client della relativa cronologia di download. Per altre informazioni, vedere [Installare e configurare i punti di distribuzione](../deploy/configure/install-and-configure-distribution-points.md).  

- **Abilita la pulizia WSUS**: verifica che sia stata abilitata l'opzione per eseguire la pulizia WSUS sulle proprietà del componente del punto di aggiornamento software. Questa opzione consente di migliorare le prestazioni di WSUS. Per altre informazioni, vedere [Manutenzione degli aggiornamenti software](../../../sum/deploy-use/software-updates-maintenance.md).  

- **Immagini d'avvio inutilizzate**: immagini di avvio a cui non viene fatto riferimento per l'avvio PXE o per l'uso di sequenze di attività. Per altre informazioni, vedere [Manage boot images](../../../osd/get-started/manage-boot-images.md) (Gestire le immagini d'avvio).  

- **Elementi di configurazione inutilizzati**: elementi di configurazione che non fanno parte di una linea di base di configurazione e sono anteriori a 30 giorni. Per altre informazioni, vedere [Creare configurazioni di base](../../../compliance/deploy-use/create-configuration-baselines.md).  

- **Aggiorna le origini di peer cache alla versione più recente del client di Configuration Manager**: identificare i client che fungono da origine di peer cache, ma non sono stati aggiornati da una versione del client precedente alla 1806. I client precedenti alla versione 1806 non possono essere usati come origine di peer cache per i client che eseguono la versione 1806 o versioni successive. Selezionare **Intervieni** per aprire una visualizzazione del dispositivo che mostra l'elenco dei client.<!--1358008-->  

### <a name="security"></a>Sicurezza

Informazioni dettagliate per il miglioramento dell'infrastruttura e dei dispositivi.

- **Fallback NTLM abilitato**:<!--4572953--> a partire dalla versione 1906, questa regola rileva se è stato abilitato il metodo di fallback dell'autenticazione NTLM meno sicuro per il sito. Quando si usa il metodo di installazione push client per il client Configuration Manager, il sito può richiedere l'autenticazione reciproca Kerberos. Questo miglioramento consente di proteggere la comunicazione tra il server e il client. Per altre informazioni , vedere [Come installare i client con l'installazione push client](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).

- **Versioni client dell'antimalware non supportate**: più del 10% dei cliente esegue versioni di System Center Endpoint Protection che non sono più supportate. Per altre informazioni, vedere [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md).  

### <a name="simplified-management"></a>Gestione semplificata

Informazioni dettagliate utili per semplificare la gestione quotidiana dell'ambiente.

- **Connettere il sito al cloud Microsoft per gli aggiornamenti di Configuration Manager**: Questa regola assicura che il punto di connessione del servizio Configuration Manager sia stato connesso al cloud Microsoft negli ultimi sette giorni. Questa connessione consente di scaricare il contenuto per gli aggiornamenti regolari. Vedere DMPDownloader.log e hman.log. Per altre informazioni, vedere i [requisiti di accesso Internet](../../plan-design/network/internet-endpoints.md#bkmk_scp-updates).

- **Versioni client non CB**: elenca tutti i client le cui versioni non corrispondono a una build Current Branch (CB). Per altre informazioni, vedere [Aggiornare i client](../../clients/manage/upgrade/upgrade-clients.md).  

- **Aggiorna i client a una versione di Windows 10 supportata**: A partire dalla versione 1902, questa regola segnala i client che eseguono una versione di Windows 10 che non è più supportata. Include anche i client con una versione di Windows 10 che sta per raggiungere la fine del servizio (tre mesi).<!--3897268-->  

### <a name="software-center"></a>Software Center

Informazioni dettagliate per la gestione di Software Center.

- **Indirizza gli utenti a Software Center invece che al Catalogo applicazioni**: controlla se gli utenti hanno installato o richiesto applicazioni dal Catalogo applicazioni negli ultimi 14 giorni. La funzionalità principale del Catalogo applicazioni è ora inclusa in Software Center. Il supporto per i ruoli del Catalogo applicazioni termina con la versione 1910. Per altre informazioni, vedere [Funzionalità deprecate](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md#deprecated-features).  

- **Usa la nuova versione di Software Center**: La versione precedente di Software Center non è più supportata. Configurare i client per l'uso del nuovo Software Center abilitando l'impostazione client **Usa il nuovo Software Center** nel gruppo **Agente computer**. Per altre informazioni, vedere [About client settings](../../clients/deploy/about-client-settings.md#use-new-software-center) (Informazioni sulle impostazioni client).  

### <a name="software-updates"></a>Aggiornamenti software

- **Le impostazioni client non sono configurate per consentire ai client di scaricare contenuto differenziale**: Alcuni aggiornamenti software sincronizzati nell'ambiente includono contenuto differenziale. Abilitare l'impostazione del client **Consenti ai client di scaricare contenuto differenziale quando disponibile**. Se non si abilita questa impostazione, quando si distribuiscono questi aggiornamenti, il client scaricherà inutilmente più contenuto del necessario. Per altre informazioni, vedere [Impostazioni del client - Aggiornamenti software](../../clients/deploy/about-client-settings.md#software-updates).

- **Abilitare la categoria di prodotti per gli aggiornamenti software 'Windows 10 versione 1903 e versioni successive'** : È presente una nuova categoria di prodotti per gli aggiornamenti software per Windows 10 versione 1903 e versioni successive. Se si sincronizzano gli aggiornamenti di Windows 10 e si hanno client Windows 10 versione 1903 o versioni successive, selezionare la categoria di prodotti **Windows 10 versione 1903 e versioni successive** nelle proprietà del componente del punto di aggiornamento software. Per altre informazioni, vedere [Configurare le classificazioni e i prodotti per la sincronizzazione](../../../sum/get-started/configure-classifications-and-products.md).

### <a name="windows-10"></a>Windows 10

Informazioni dettagliate correlate alla distribuzione e alla manutenzione di Windows 10. Il gruppo di informazioni dettagliate sulla gestione di Windows 10 è disponibile solo quando in più della metà dei client è in esecuzione Windows 7, Windows 8 o Windows 8.1.

- **Configurare i dati di diagnostica di Windows e la chiave ID commerciale**: per usare i dati da Desktop Analytics, configurare i dispositivi con una chiave ID commerciale e abilitare la raccolta dei dati di diagnostica. Impostare i dispositivi Windows 10 sul livello **Avanzata (con limitazioni)** o superiore. Per altre informazioni, vedere [Abilitare la condivisione dei dati per Desktop Analytics](../../../desktop-analytics/enable-data-sharing.md).

#### <a name="windows-10-management-insights-rules"></a>Regole di Informazioni dettagliate sulla gestione di Windows 10

![Informazioni dettagliate sulla gestione - Regole per Windows 10](./media/Windows-10-insights-group.png)
