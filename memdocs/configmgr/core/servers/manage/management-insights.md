---
title: Informazioni dettagliate sulla gestione
titleSuffix: Configuration Manager
description: Informazioni sulla funzionalità Informazioni dettagliate sulla gestione disponibile nella console di Configuration Manager.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a79f83be-884c-48e6-94d6-ed0a68c22e2f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: de3c75982e19e6183260a2a5f99f65b9c785d27f
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700515"
---
# <a name="management-insights-in-configuration-manager"></a>Informazioni dettagliate sulla gestione in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

La funzionalità Informazioni dettagliate sulla gestione in Configuration Manager offre indicazioni utili sullo stato corrente dell'ambiente. Le informazioni si basano sull'analisi dei dati presenti nel database del sito. Le informazioni dettagliate aiutano a capire meglio l'ambiente e a intervenire di conseguenza. <!--1353967-->

## <a name="review-management-insights"></a>Esaminare le informazioni dettagliate sulla gestione

Per visualizzare le informazioni dettagliate, l'account deve disporre dell'autorizzazione di **lettura** per l'oggetto **sito**.

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Informazioni dettagliate sulla gestione** e selezionare **Tutte le informazioni dettagliate**.

    > [!NOTE]
    > Quando si seleziona il nodo **Informazioni dettagliate sulla gestione** viene visualizzato il [Dashboard di informazioni dettagliate sulla gestione](#bkmk_insights).

1. Aprire il nome del gruppo di informazioni dettagliate sulla gestione che si vuole esaminare.

1. Nella barra multifunzione selezionare **Mostra le informazioni dettagliate**.

È possibile esaminare le quattro schede seguenti:

- **Tutte le regole**: fornisce l'elenco completo delle informazioni dettagliate per il gruppo scelto.

- **Completa**:  elenca i dati per cui non è necessaria alcuna azione.

- **In corso**: mostra i dati in cui alcuni, ma non tutti i prerequisiti sono soddisfatti.

- **Azione richiesta**: elenca i dati per cui è necessario intervenire. Scegliere **Altri dettagli** per visualizzare elementi specifici in cui è necessaria un'azione.

Nel riquadro **Prerequisiti** sono elencati gli elementi obbligatori per eseguire i dati selezionati.

Ad esempio, lo screenshot seguente illustra un esempio della scheda **Tutte le regole** per il gruppo **Servizi cloud**:

:::image type="content" source="media/management-insights-all-cloud-rules.png" alt-text="Informazioni dettagliate sulla gestione: tutte le regole e i prerequisiti per il gruppo Servizi cloud":::

Per visualizzare i dettagli, selezionare un'informazione dettagliata e quindi selezionare **Altri dettagli**.

## <a name="operations"></a>Operazioni

Il sito rivaluta l'applicabilità delle informazioni dettagliate sulla gestione a una pianificazione settimanale. Per rivalutare manualmente un'informazione dettagliata, selezionarla con il pulsante destro del mouse e selezionare **Valuta di nuovo**.

Il file di log per le informazioni dettagliate sulla gestione è **SMS_DataEngine.log** ed è disponibile nel server del sito.

<!--1357930-->
Alcune informazioni dettagliate consentono di intervenire. Selezionare un'informazione dettagliata, selezionare **Altri dettagli** e quindi, se disponibile, selezionare **Intervieni**. A seconda dell'informazione dettagliata, questa azione presenta uno dei comportamenti seguenti:

- Passare direttamente nella console al nodo in cui è possibile eseguire ulteriori azioni. Ad esempio, se le informazioni dettagliate sulla gestione consigliano di modificare un'impostazione client, l'opzione per eseguire un'azione consente di passare al nodo **Impostazioni client**. Eseguire quindi ulteriori azioni modificando l'impostazione predefinita o un oggetto impostazioni client personalizzato.

- Passare a una visualizzazione filtrata in base a una query. Ad esempio, eseguire l'azione per un'informazione dettagliata delle raccolte vuote mostra semplicemente queste raccolte nell'elenco delle raccolte. Eseguire quindi eseguire ulteriori azioni, ad esempio eliminare una raccolta o modificarne le regole di appartenenza.

## <a name="management-insights-dashboard"></a><a name="bkmk_insights"></a> Dashboard delle informazioni dettagliate sulla gestione

<!--1357979-->

Selezionare il nodo **Informazioni dettagliate sulla gestione** per visualizzare un dashboard grafico. Questo dashboard visualizza una panoramica degli stati delle informazioni dettagliate che rende più semplice visualizzare lo stato di avanzamento.

Usare i filtri seguenti nella parte superiore del dashboard per ottimizzare la visualizzazione:

- Mostra completate
- Facoltativo
- Consigliato
- Critico

Il dashboard include i riquadri seguenti:  

- **Indice informazioni dettagliate sulla gestione**: registra l'avanzamento generale delle informazioni dettagliate sulla gestione. L'indice è una media ponderata. Le informazioni dettagliate critiche hanno maggior valore. Questo indice assegna il minor peso alle informazioni dettagliate facoltative.

- **Gruppi di informazioni dettagliate sulla gestione**: mostra la percentuale di informazioni dettagliate di ogni gruppo che soddisfa i filtri. Selezionare un gruppo per eseguire il drill-down nelle informazioni dettagliate specifiche del gruppo.

- **Priorità delle informazioni dettagliate sulla gestione**: mostra la percentuale di informazioni dettagliate in base alla priorità che soddisfa i filtri.

- **10 regole principali per informazioni dettagliate applicabili**: tabella delle informazioni dettagliate con priorità e stato. Usare il campo **Filtro** nella parte superiore della tabella per la corrispondenza con stringhe in una qualsiasi delle colonne disponibili. Il dashboard consente di ordinare la tabella nell'ordine seguente:

  - Stato: Azione necessaria, Completato, Sconosciuto  
  - Priorità: Critico, Consigliato, Facoltativo  
  - Ultima modifica: le date meno recenti sono visualizzate all'inizio  

:::image type="content" source="media/1357979-management-insights-dashboard.png" alt-text="Screenshot del dashboard delle informazioni dettagliate sulla gestione" lightbox="media/1357979-management-insights-dashboard.png":::

## <a name="groups-and-insights"></a>Gruppi e informazioni dettagliate

Le informazioni dettagliate sono organizzate nei gruppi di informazioni dettagliate sulla gestione seguenti:

- [Applicazioni](#applications)
- [Servizi cloud](#cloud-services)
- [raccolte](#collections)
- [Valutazione di Configuration Manager](#configuration-manager-assessment)
- [Ottimizzazione dei ruoli di lavoro remoti](#optimize-for-remote-workers)
- [Manutenzione proattiva](#proactive-maintenance)
- [Security](#security)
- [Gestione semplificata](#simplified-management)
- [Software Center](#software-center)
- [Aggiornamenti software](#software-updates)
- [Windows 10](#windows-10)

> [!NOTE]
> È possibile che il sito non visualizzi tutti i gruppi e le informazioni dettagliate seguenti. Alcune informazioni dettagliate non vengono visualizzate quando il sito è già stato configurato per la raccomandazione.

### <a name="applications"></a>Applicazioni

Informazioni dettagliate per la gestione delle applicazioni.

- **Applicazioni senza distribuzioni o riferimenti**: elenca le applicazioni dell'ambiente senza riferimenti o distribuzioni attive. I riferimenti includono dipendenze, sequenze di attività e ambienti virtuali. Questa informazione dettagliata consente di individuare ed eliminare le applicazioni non usate per semplificare l'elenco di applicazioni visualizzato nella console. Per altre informazioni, vedere l'argomento relativo alla [distribuzione delle applicazioni](../../../apps/deploy-use/deploy-applications.md).<!-- B585E3FF-585F-4CE9-AE2C-648A7CA2F143 -->

### <a name="cloud-services"></a>Servizi cloud

Facilita l'integrazione con molti servizi cloud per una gestione moderna dei dispositivi.

- **Valuta l'idoneità per la co-gestione**: consente di comprendere i passaggi necessari per abilitare la co-gestione. Questa informazione dettagliata include alcuni prerequisiti. Per altre informazioni, vedere la [panoramica sulla co-gestione](../../../comanage/overview.md).<!-- D99F094A-A965-402F-AFE5-EE00CCAF0A12 -->

- **Dispositivi non caricati in Azure AD**: a partire dalla versione 2002, questa informazione dettagliata elenca i dispositivi non caricati dal sito in Azure Active Directory (Azure AD) perché non è stato configurato per HTTPS.<!--6268489--> Configurare [HTTP avanzato](../../plan-design/hierarchy/enhanced-http.md) o abilitare almeno un punto di gestione per HTTPS. Se il sito è già stato configurato per la comunicazione HTTPS, questa informazione dettagliata non viene visualizzata.<!-- 609F03D4-D9B4-4D0D-A67F-9E365F6C0DD0 -->

- **Abilita Cloud Management Gateway**: Cloud Management Gateway consente di gestire i client di Configuration Manager in Internet in modo semplice. Distribuendo Cloud Management Gateway come servizio cloud in Microsoft Azure, è possibile continuare a gestire e trasferire contenuto ai client che effettuano il roaming in Internet. Con Cloud Management Gateway non è necessaria un'infrastruttura locale aggiuntiva esposta a Internet. Per altre informazioni, vedere [Pianificare il gateway di gestione cloud](../../clients/manage/cmg/plan-cloud-management-gateway.md).<!-- 451B9B3A-D86A-4EF1-ACC3-FE6A207886BA -->

- **Consenti dispositivi ibridi aggiunti ad Azure Active Directory**: i dispositivi aggiunti ad Azure AD consentono agli utenti di accedere con le credenziali del dominio e garantire che i dispositivi soddisfino gli standard di sicurezza e conformità dell'organizzazione. Per altre informazioni, vedere [Considerazioni di progettazione dell'identità ibrida di Azure Active Directory](/azure/active-directory/hybrid/plan-hybrid-identity-design-considerations-overview).<!-- 6DC6B149-8B48-45E9-B189-F1E12A62D994 -->

- **Siti senza configurazione HTTPS appropriata**: a partire dalla versione 2002, questa informazione dettagliata elenca i siti nella gerarchia che non sono configurati correttamente per HTTPS. Questa configurazione impedisce al sito di [sincronizzare i risultati di appartenenza alla raccolta con i gruppi di Azure AD](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync). Di conseguenza, è possibile che AD Sync non carichi tutti i dispositivi. La gestione di questi client potrebbe non funzionare correttamente.<!--6268489--> Configurare [HTTP avanzato](../../plan-design/hierarchy/enhanced-http.md) o abilitare almeno un punto di gestione per HTTPS. Se il sito è già stato configurato per la comunicazione HTTPS, questa informazione dettagliata non viene visualizzata.<!-- 73884047-3395-430E-B971-F853806D4349 -->

- **Aggiorna i client alla versione più recente di Windows 10**: Windows 10, versione 1709 o versioni successive, migliora e modernizza l'esperienza di elaborazione degli utenti. Per altre informazioni, vedere [Articoli principali sull'adozione di Windows as a Service](../../understand/configuration-manager-and-windows-as-service.md#key-articles-about-adopting-windows-as-a-service).<!-- FD2C7B93-E5C6-4DCB-89AF-9EFCFCD01524 -->

### <a name="collections"></a>Raccolte

Informazioni dettagliate che consentono di semplificare la gestione tramite la pulizia e la riconfigurazione delle raccolte.

- **Raccolte vuote**: un elenco delle raccolte dell'ambiente che non hanno membri. Per altre informazioni, vedere [Come gestire le raccolte](../../clients/manage/collections/manage-collections.md).<!-- 4266054A-695D-4BCA-8000-27BD32F7C006 -->

<!--3555752-->
- **Raccolte senza regole di query e senza membri diretti**: per semplificare l'elenco di raccolte nella gerarchia, eliminare queste raccolte.<!-- 3C234964-B3F3-49EE-AA13-048CD2021924 -->

- **Raccolte con la stessa ora di inizio di rivalutazione**: queste raccolte hanno la stessa ora di rivalutazione di altre raccolte. Modificare l'ora di rivalutazione in modo da evitare conflitti.<!-- A85B79A6-BA81-404F-8DA4-DD7C87582CCD -->

- **Raccolte con tempo di query di oltre cinque minuti**: rivedere le regole di query per queste raccolte. Prendere in considerazione di modificarle o eliminarle.<!-- 6AF42536-BDF4-4535-87C1-535AE1B813DA -->

- Le informazioni dettagliate seguenti includono configurazioni che possono causare un carico non necessario del sito. Rivedere queste raccolte e quindi eliminarle oppure disabilitare la valutazione delle regole della raccolta:

  - **Raccolte senza regole di query e con gli aggiornamenti incrementali abilitati**<!-- 6A4845AB-6D2C-4F2A-B7AB-EC77C81FD571 -->

  - **Raccolte senza regole di query e abilitate per qualsiasi pianificazione**<!-- 219B9C45-BD02-4E7E-A29D-B66094366200 -->

  - **Raccolte senza regole di query e con pianificazione della valutazione completa selezionata**<!-- 8A401207-5A7C-4200-A1DB-990A197458FA -->

### <a name="configuration-manager-assessment"></a>Valutazione di Configuration Manager

<!--3607758-->

A partire dalla versione 2002, questo gruppo è gentilmente fornito da gentilmente fornite da Microsoft Premier Field Engineering. Queste informazioni dettagliate sono un esempio dei molti altri controlli forniti da Microsoft Premier nell'[hub Servizi](/services-hub/health/getting_started_with_on_demand_assessments).

- **La configurazione di Individuazione gruppo di protezione Active Directory prevede un'esecuzione troppo frequente**: Non è in genere necessario configurare Individuazione gruppo di protezione Active Directory con una ricorrenza superiore a ogni tre ore. Una configurazione più frequente può avere un impatto negativo sulle prestazioni di Active Directory, della rete e di Configuration Manager. Abilitare la sincronizzazione incrementale invece di usare una pianificazione della sincronizzazione completa. Per altre informazioni, vedere [Individuazione gruppo Active Directory](../deploy/configure/about-discovery-methods.md#bkmk_aboutGroup).<!-- 4E739B65-AEC9-4B1D-8B36-AC6AC4A72022 -->

- **La configurazione di Individuazione sistema Active Directory prevede un'esecuzione troppo frequente**: non è in genere necessario configurare Individuazione sistema Active Directory con una ricorrenza superiore a ogni tre ore. Una configurazione più frequente può avere un impatto negativo sulle prestazioni di Active Directory, della rete e di Configuration Manager. Abilitare la sincronizzazione incrementale invece di usare una pianificazione della sincronizzazione completa. Per altre informazioni, vedere [Individuazione sistema Active Directory](../deploy/configure/about-discovery-methods.md#bkmk_aboutSystem).<!-- 353CAFBC-AC90-4FD3-B3CF-51D6D9FB376C -->

- **La configurazione di Individuazione utente Active Directory prevede un'esecuzione troppo frequente**: Non è in genere necessario configurare Individuazione utente Active Directory con una ricorrenza superiore a ogni tre ore. Una configurazione più frequente può avere un impatto negativo sulle prestazioni di Active Directory, della rete e di Configuration Manager. Abilitare la sincronizzazione incrementale invece di usare una pianificazione della sincronizzazione completa. Per altre informazioni, vedere [Individuazione utente Active Directory](../deploy/configure/about-discovery-methods.md#bkmk_aboutUser).<!-- 2E742924-7319-4013-B1E1-97DE7EB16B74 -->

- **Raccolte limitate a Tutti i sistemi o Tutti gli utenti**: consente di esaminare eventuali raccolte che usano le raccolte **Tutti i sistemi** o **Tutti gli utenti** come raccolta di delimitazione. Configuration Manager aggiorna l'appartenenza di queste raccolte predefinite con dati dai metodi di individuazione di Active Directory. È possibile che questi dati non siano informazioni valide per i client di Configuration Manager.<!-- 2382F0C9-A36D-4079-AB37-E3D8EE47E8D4 -->

- **L'opzione Individuazione heartbeat è disabilitata**: per l'individuazione heartbeat è necessario installare il client di Configuration Manager nei dispositivi. Si tratta dell'unico metodo di individuazione avviato dai client. Tutti gli altri metodi vengono applicati nei server del sito. L'individuazione heartbeat è essenziale per mantenere aggiornato lo stato di attività dei client. Garantisce che il sito non renda inavvertitamente obsoleti i record di risorse dal database del sito. Per altre informazioni, vedere [Individuazione heartbeat](../deploy/configure/about-discovery-methods.md#bkmk_aboutHeartbeat).<!-- A3089798-DF4E-490A-AF78-4AF474B214CF -->

- **Query su raccolte a esecuzione prolungata abilitate per gli aggiornamenti incrementali**: le raccolte con durata dell'ultimo aggiornamento incrementale superiore a 30 secondi usano risorse del server del sito e del database che potrebbero potenzialmente influire sulle prestazioni complessive di Configuration Manager. Per altre informazioni, vedere [Procedure consigliate per le raccolte](../../clients/manage/collections/best-practices-for-collections.md).<!-- 21F14C0E-008B-47F3-B1E2-19CF79DC97B4 -->

- **Riduci il numero di applicazioni e pacchetti nei punti di distribuzione**: Microsoft supporta ufficialmente un totale combinato di massimo 10.000 pacchetti e applicazioni per un punto di distribuzione. Il superamento di questo totale può causare problemi operativi. Per altre informazioni, vedere [Numeri di ridimensionamento e scalabilità - punto di distribuzione](../../plan-design/configs/size-and-scale-numbers.md#distribution-point).<!-- FFE6906E-932E-4927-8EE0-BA25C37943CB -->

- **Problemi di installazione dei siti secondari**: lo stato di installazione di alcuni siti secondari è **In sospeso** o **Errore**. Questi stati indicano che l'installazione è stata avviata ma non è stata completata. Fino al completamento dell'installazione dei siti secondari, è possibile che i client non comunichino correttamente con il sito primario. Controllare l'area di lavoro **Monitoraggio** e ritentare l'installazione. Per altre informazioni, vedere [Ripetere l'installazione di un aggiornamento non riuscito](install-in-console-updates.md#bkmk_retry) .<!-- ED3F5BDD-2F02-44A4-87F4-BB2C1032D4DE -->

- **Aggiorna tutti i siti alla stessa versione**: usare la stessa versione di Configuration Manager in una gerarchia. Questa configurazione garantisce che tutti i siti offrano le stesse funzionalità. I siti di versioni diverse nella stessa gerarchia introducono scenari di interoperabilità. Nelle versioni successive di Configuration Manager sono incluse nuove funzionalità e vengono risolti problemi noti. Per altre informazioni, vedere [Interoperabilità tra versioni diverse](../../plan-design/hierarchy/interoperability-between-different-versions.md).<!-- 88C630A5-6D6B-4DDB-95D7-78E12107970D -->

Per altre informazioni su queste informazioni dettagliate, vedere [Procedure di correzione per i programmi consigliati sulla gestione di Configuration Manager](/services-hub/health/remediation-steps-configmgr).

> [!TIP]
> I clienti di Microsoft Unified o Microsoft Premier possono accedere all'[hub Servizi](https://serviceshub.microsoft.com/assessments/) per ulteriori valutazioni su richiesta.
>
> Per altre informazioni sui servizi Microsoft, vedere le [soluzioni di supporto tecnico](https://www.microsoft.com/enterprise/services/support).

### <a name="operating-system-deployment"></a>Distribuzione del sistema operativo

<!--6982275-->

A partire dalla versione 2006, le informazioni dettagliate sulla gestione seguenti consentono di gestire le dimensioni dei criteri delle sequenze di attività. Quando le dimensioni dei criteri delle sequenze di attività superano 32 MB, il client non riesce a elaborare i criteri di grandi dimensioni. Il client non riesce quindi a eseguire la distribuzione della sequenza di attività.

- **Dimensioni elevate delle sequenze di attività possono contribuire al superamento delle dimensioni massime dei criteri**: se si distribuiscono queste sequenze di attività, i client potrebbero non essere in grado di elaborare gli oggetti criteri di grandi dimensioni. Ridurre le dimensioni dei criteri delle sequenze di attività per evitare potenziali problemi di elaborazione dei criteri.<!-- D9A15248-832E-4780-8151-ACD1B9E53FE1 -->

- **Le dimensioni totali dei criteri per le sequenze di attività superano il limite dei criteri**: i client non sono in grado di elaborare i criteri per queste sequenze di attività a causa delle dimensioni eccessive. Ridurre le dimensioni dei criteri delle sequenze di attività per consentire l'esecuzione della distribuzione nei client.<!-- 6568F6A3-D1D8-4E63-940B-FE44F8349802 -->

Per altre informazioni, vedere [Ridurre le dimensioni dei criteri delle sequenze di attività](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#bkmk_policysize).

Nella versione 2006, le informazioni dettagliate seguenti sono state spostate in questo gruppo dal gruppo **Manutenzione proattiva**:

- **Immagini d'avvio inutilizzate**: immagini di avvio a cui non viene fatto riferimento per l'avvio PXE o per l'uso di sequenze di attività. Per altre informazioni, vedere [Manage boot images](../../../osd/get-started/manage-boot-images.md) (Gestire le immagini d'avvio).<!-- 4C1FBA51-AD56-4CA8-8326-066F65D24F0E -->

### <a name="optimize-for-remote-workers"></a>Ottimizzazione dei ruoli di lavoro remoti

<!--6982226-->

A partire dalla versione 2006, le informazioni dettagliate seguenti consentono di creare esperienze migliori per i ruoli di lavoro remoti e di ridurre il carico sull'infrastruttura:

- **Configurare i client connessi alla VPN per preferire le origini del contenuto basate sul cloud**: per ridurre il traffico sulla VPN, abilitare l'opzione del gruppo di limiti **Preferisci le origini basate sul cloud rispetto alle origini locali**. Questa opzione consente ai client di scaricare il contenuto da Internet anziché i punti di distribuzione attraverso la VPN. Per altre informazioni vedere [Opzioni del gruppo di limiti](../deploy/configure/boundary-groups.md#bkmk_bgoptions4).<!-- 1BFD7A7A-077C-4E8A-9EAA-4559E41D400A -->

- **Definire gruppi di limiti VPN**: creare un limite VPN e associarlo a un gruppo di limiti. Associare i sistemi del sito specifici della VPN al gruppo e configurare le impostazioni per l'ambiente. Queste informazioni consentono di individuare almeno un gruppo di limiti con almeno un limite VPN. Dalle proprietà di queste informazioni selezionare **Verificare le azioni** per passare al nodo **Gruppi di limiti**. Per altre informazioni, vedere [Tipo di limite VPN](../deploy/configure/boundaries.md#vpn).<!-- E44BF0CC-0ADA-4B00-A4DF-4005256DF73E -->

- **Disabilitare la condivisione del contenuto peer-to-peer per i client connessi alla VPN**: per impedire il traffico peer-to-peer superfluo che probabilmente non avvantaggia i client remoti, disabilitare l'opzione del gruppo di limiti **Consenti i download peer in questo gruppo di limiti**. Per altre informazioni vedere [Opzioni del gruppo di limiti](../deploy/configure/boundary-groups.md#bkmk_bgoptions1).<!-- 60404B23-96A9-4EE2-B8D6-1F226C2F2F5A -->

### <a name="proactive-maintenance"></a>Manutenzione proattiva

<!--1352184-->
Le informazioni dettagliate in questo gruppo evidenziano potenziali problemi di configurazione che possono essere evitati tramite la manutenzione degli oggetti di Configuration Manager.

- **Gruppi di limiti senza sistemi del sito assegnati**: senza sistemi del sito assegnati, i gruppi di limiti possono essere usati solo per l'assegnazione del sito. Per altre informazioni, vedere [Configurare gruppi di limiti](../deploy/configure/boundary-groups.md).<!-- 01E5A4BC-0E31-494E-A553-2B32C410FA5B -->

- **Gruppi di limiti senza membri**: i gruppi di limiti non sono applicabili per l'assegnazione del sito o la ricerca di contenuto se non hanno membri. Per altre informazioni, vedere [Configurare gruppi di limiti](../deploy/configure/boundary-groups.md).<!-- 4f0d37b1-f979-4ba3-b15b-7fe3c915f239 -->

- **Punti di distribuzione che non forniscono contenuti ai client**: punti di distribuzione che non hanno reso disponibile contenuto ai client negli ultimi 30 giorni. I dati sono basati sui report dai client della relativa cronologia di download. Per altre informazioni, vedere [Installare e configurare i punti di distribuzione](../deploy/configure/install-and-configure-distribution-points.md).<!-- 9A115092-F8D4-4AB7-B846-C09143B9B9B0 -->

- **Abilita la pulizia WSUS**: verifica che sia stata abilitata l'opzione per eseguire la pulizia WSUS sulle proprietà del componente del punto di aggiornamento software. Questa opzione consente di migliorare le prestazioni di WSUS. Per altre informazioni, vedere [Manutenzione degli aggiornamenti software](../../../sum/deploy-use/software-updates-maintenance.md).<!-- D43080F1-FE98-4F24-94ED-FEB1C2DDEF50 -->

- **Elementi di configurazione inutilizzati**: elementi di configurazione che non fanno parte di una linea di base di configurazione e sono anteriori a 30 giorni. Per altre informazioni, vedere [Creare configurazioni di base](../../../compliance/deploy-use/create-configuration-baselines.md).<!-- 0597907B-17D4-4EA5-92E4-CCE692E1468D -->

- **Aggiorna le origini di peer cache alla versione più recente del client di Configuration Manager**:<!--1358008--> identificare i client che fungono da origine di peer cache, ma non sono stati aggiornati da una versione del client precedente alla 1806. I client precedenti alla versione 1806 non possono essere usati come origine di peer cache per i client che eseguono la versione 1806 o versioni successive. Selezionare **Intervieni** per aprire una visualizzazione del dispositivo che mostra l'elenco dei client.<!-- B51C6733-F9FF-46BC-8F5E-624F2CBED719 -->

> [!TIP]
> Nella versione 2006, le informazioni dettagliate per **Immagini d'avvio inutilizzate** sono state spostate nel nuovo gruppo [Distribuzione del sistema operativo](#operating-system-deployment).

### <a name="security"></a>Sicurezza

Informazioni dettagliate per il miglioramento dell'infrastruttura e dei dispositivi.

- **Fallback NTLM abilitato**:<!--4572953--> a partire dalla versione 1906, questa informazione dettagliata rileva se è stato abilitato il metodo di fallback dell'autenticazione NTLM meno sicuro per il sito. Quando si usa il metodo di installazione push client per il client Configuration Manager, il sito può richiedere l'autenticazione reciproca Kerberos. Questo miglioramento consente di proteggere la comunicazione tra il server e il client. Per altre informazioni , vedere [Come installare i client con l'installazione push client](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).<!-- C16C6826-8209-47A9-BA71-14A8C83E4C35 -->

- **Versioni client dell'antimalware non supportate**: più del 10% dei cliente esegue versioni di System Center Endpoint Protection che non sono più supportate. Per altre informazioni, vedere [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md).<!-- ACD63321-CF15-4CDD-B1A3-69005887C633 -->

### <a name="simplified-management"></a>Gestione semplificata

Informazioni dettagliate utili per semplificare la gestione quotidiana dell'ambiente.

- **Connettere il sito al cloud Microsoft per gli aggiornamenti di Configuration Manager**: questa informazione dettagliata assicura che il punto di connessione del servizio Configuration Manager sia stato connesso al cloud Microsoft negli ultimi sette giorni. Questa connessione consente di scaricare il contenuto per gli aggiornamenti regolari. Vedere DMPDownloader.log e hman.log. Per altre informazioni, vedere i [requisiti di accesso Internet](../../plan-design/network/internet-endpoints.md#bkmk_scp-updates).<!-- AC662C91-54DF-4B43-B09A-B19D2766144B -->

- **Versioni client non CB**: elenca tutti i client le cui versioni non corrispondono a una build Current Branch (CB). Per altre informazioni, vedere [Aggiornare i client](../../clients/manage/upgrade/upgrade-clients.md).<!-- 450090EA-DF71-428C-AB49-6DEBB85A004C -->

- **Aggiorna i client a una versione di Windows 10 supportata**:<!--3897268--> questa informazione dettagliata segnala i client che eseguono una versione di Windows 10 che non è più supportata. Include anche i client con una versione di Windows 10 che sta per raggiungere la fine del servizio (tre mesi).<!-- 560669D6-1756-4814-9505-C54BDB4930D0 -->

### <a name="software-center"></a>Software Center

Informazioni dettagliate per la gestione di Software Center.

- **Indirizza gli utenti a Software Center invece che al Catalogo applicazioni**: controlla se gli utenti hanno installato o richiesto applicazioni dal Catalogo applicazioni negli ultimi 14 giorni. La funzionalità principale del Catalogo applicazioni è ora inclusa in Software Center. Il supporto per i ruoli del Catalogo applicazioni termina con la versione 1910. Per altre informazioni, vedere [Funzionalità deprecate](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md#deprecated-features).<!-- DB9E65CF-C59C-4B76-B6A0-ADB95D809246 -->

- **Usa la nuova versione di Software Center**: La versione precedente di Software Center non è più supportata. Configurare i client per l'uso del nuovo Software Center abilitando l'impostazione client **Usa il nuovo Software Center** nel gruppo **Agente computer**. Per altre informazioni, vedere [About client settings](../../clients/deploy/about-client-settings.md#use-new-software-center) (Informazioni sulle impostazioni client).<!-- A9BCA10D-834F-4F39-89F5-CDCCE8F80C56 -->

### <a name="software-updates"></a>Aggiornamenti software

- **Le impostazioni client non sono configurate per consentire ai client di scaricare contenuto differenziale**: Alcuni aggiornamenti software sincronizzati nell'ambiente includono contenuto differenziale. Abilitare l'impostazione del client **Consenti ai client di scaricare contenuto differenziale quando disponibile**. Se non si abilita questa impostazione, quando si distribuiscono questi aggiornamenti, il client scaricherà inutilmente più contenuto del necessario. Per altre informazioni, vedere [Impostazioni del client - Aggiornamenti software](../../clients/deploy/about-client-settings.md#software-updates).<!-- 3E2E9E10-1CDC-47E3-BFC9-3A46AB7FE1BD -->

- **Abilitare la categoria di prodotti per gli aggiornamenti software 'Windows 10 versione 1903 e versioni successive'** : È presente una nuova categoria di prodotti per gli aggiornamenti software per Windows 10 versione 1903 e versioni successive. Se si sincronizzano gli aggiornamenti di Windows 10 e si hanno client Windows 10 versione 1903 o versioni successive, selezionare la categoria di prodotti **Windows 10 versione 1903 e versioni successive** nelle proprietà del componente del punto di aggiornamento software. Per altre informazioni, vedere [Configurare le classificazioni e i prodotti per la sincronizzazione](../../../sum/get-started/configure-classifications-and-products.md).<!-- 16B1152D-6511-4DC7-824E-539B2597F9B0 -->

### <a name="windows-10"></a>Windows 10

Informazioni dettagliate correlate alla distribuzione e alla manutenzione di Windows 10. Il gruppo di informazioni dettagliate sulla gestione di Windows 10 è disponibile solo quando in più della metà dei client è in esecuzione Windows 7, Windows 8 o Windows 8.1.

- **Configurare i dati di diagnostica di Windows e la chiave ID commerciale**: per usare i dati da Desktop Analytics, configurare i dispositivi con una chiave ID commerciale e abilitare la raccolta dei dati di diagnostica. Impostare i dispositivi Windows 10 sul livello **Avanzata (con limitazioni)** o superiore. Per altre informazioni, vedere [Abilitare la condivisione dei dati per Desktop Analytics](../../../desktop-analytics/enable-data-sharing.md).<!-- B224393F-B255-4C80-A1D1-1014BE1DC7D4 -->