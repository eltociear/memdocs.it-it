---
title: Anteprima di Analisi degli endpoint
titleSuffix: Configuration Manager
description: Istruzioni per l'anteprima di Analisi degli endpoint.
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 00537b90-f6d2-45e9-a9a1-6b3ada466a16
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: 6f481fa54a8018137a4b45bc62f6fde9c1f1165b
ms.sourcegitcommit: 7b224e138c0618e978be59832b3486f3745abacc
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/13/2020
ms.locfileid: "83381580"
---
# <a name="endpoint-analytics-preview"></a><a name="bkmk_uea"></a> Anteprima di Analisi degli endpoint

> [!Note]  
> Queste informazioni fanno riferimento a una funzionalità di anteprima che può essere modificata sostanzialmente prima del rilascio della versione commerciale. Microsoft non offre alcuna garanzia, espressa o implicita, relativamente alle informazioni fornite in questo articolo. 
>
> Per altre informazioni sulle modifiche apportate ad Analisi degli endpoint, vedere [Novità di Analisi degli endpoint](whats-new-endpoint-analytics.md). 
>
>Per partecipare all'anteprima privata di Analisi degli endpoint, immettere i dettagli [in questo modulo](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR9-ZzmlTlbJMh03eDDHtO81UOERLUkMzNFZKSlBaNFNFUVhFSlE0MzNYMS4u). I tenant verranno distribuiti in anteprima come opportunità per le espansioni dell'anteprima.


## <a name="endpoint-analytics-overview"></a>Panoramica di Analisi degli endpoint

Non è insolito per gli utenti finali riscontrare tempi di avvio lunghi o interruzioni di altro tipo. Le interruzioni possono essere dovute a una combinazione dei seguenti fattori:

- Hardware legacy
- Configurazioni software non ottimizzate per l'esperienza dell'utente finale
- Problemi causati da aggiornamenti e modifiche della configurazione

Questi problemi e altri problemi relativi all'esperienza dell'utente finale persistono perché l'IT non ha molta visibilità nell'esperienza dell'utente finale. In genere, l'unica visibilità su questi problemi proviene da un canale di supporto lento e costoso che in genere non offre informazioni chiare su ciò che deve essere ottimizzato. Non è solo il supporto IT a sopportare il peso di questi problemi. Anche il tempo che gli information worker dedicano alla gestione dei problemi è costoso. Le prestazioni, l'affidabilità e i problemi di supporto che riducono la produttività degli utenti possono avere un impatto notevole anche sul bilancio di un'azienda.

La funzionalità **Analisi degli endpoint** mira a migliorare la produttività dell'utente e a ridurre i costi del supporto IT mettendo a disposizione informazioni approfondite nell'esperienza utente. Tali informazioni consentono al reparto IT di ottimizzare l'esperienza utente con il supporto proattivo e di rilevare eventuali regressioni valutando l'impatto delle modifiche apportate alla configurazione sull'esperienza utente.

Questa versione iniziale si concentra su tre elementi:

- [**Software consigliato**](#bkmk_uea_rs): Suggerimenti per offrire la migliore esperienza utente
- [**Script di correzione proattiva**](#bkmk_uea_prs): Risolvere i problemi di supporto comuni prima che gli utenti finali li riscontrino
- [**Prestazioni di avvio**](#bkmk_uea_bp): Consentire all'IT di guidare rapidamente gli utenti dall'accensione alla produttività, senza lunghi ritardi nelle procedure di avvio e accesso

Questa versione è solo l'inizio. Verranno implementate rapidamente nuove informazioni per le altre esperienze utente principali subito dopo la versione iniziale. Per altre informazioni sulle modifiche apportate ad Analisi degli endpoint, vedere [Novità di Analisi degli endpoint](whats-new-endpoint-analytics.md).

## <a name="getting-started"></a><a name="bkmk_uea_prereq"></a> Guida introduttiva

Per iniziare a usare Analisi degli endpoint, verificare i prerequisiti e quindi iniziare a raccogliere i dati. 

### <a name="technical-prerequisites"></a>Prerequisiti tecnici

Per questa versione di anteprima è possibile registrare i dispositivi tramite Configuration Manager o Microsoft Intune. 

Per la registrazione dei dispositivi tramite Intune, questa anteprima richiede:
- Dispositivi registrati in Intune che eseguono Windows 10
- Le informazioni dettagliate sulle prestazioni di avvio sono disponibili solo per i dispositivi che eseguono la versione 1903 o successive di Windows 10 Enterprise (le edizioni Home e Pro non sono attualmente supportate) e i dispositivi devono essere aggiunti ad Azure AD o ad Azure AD ibrido. I computer aggiunti all'area di lavoro non sono attualmente supportati.
- Connettività di rete dai dispositivi al cloud pubblico Microsoft. Per altre informazioni, vedere [Endpoint](#bkmk_uea_endpoints).
- Il [ruolo di amministratore del servizio Intune](https://docs.microsoft.com/intune/fundamentals/role-based-access-control) è necessario per [iniziare a raccogliere i dati](#bkmk_uea_start).
   - Facendo clic su **Avvia**, l'utente accetta e conferma che i dati dei clienti possono essere archiviati al di fuori del percorso selezionato durante il provisioning del tenant di Microsoft Intune.
   - Dopo aver fatto clic su **Avvia** per la raccolta dei dati, altri ruoli di sola lettura possono visualizzare i dati.

Per la registrazione dei dispositivi tramite Configuration Manager, questa anteprima richiede:
- Configuration Manager versione 2002 o successiva
- Client aggiornati alla versione 2002 o successiva
- [Collegamento dei tenant di Microsoft Endpoint Manager](https://docs.microsoft.com/mem/configmgr/tenant-attach/device-sync-actions) abilitato con una posizione del tenant di Azure in America del Nord o in Europa (a breve verrà eseguita l'espansione ad altre aree)

Sia che si esegua la registrazione dei dispositivi tramite Intune o Configuration Manager, lo [**script di correzione proattiva**](#bkmk_uea_prs) ha i requisiti seguenti:
- È necessario che i dispositivi siano aggiunti ad Azure AD o ad Azure AD ibrido e soddisfino una delle condizioni seguenti:
- Un dispositivo Windows 10 Enterprise, Professional o Education gestito da Intune
- Un dispositivo [con co-gestione](../../comanage/overview.md) che esegue Windows 10 Enterprise, versione 1607 o successiva con il [carico di lavoro delle app client](../../comanage/workloads.md#client-apps) impostato su Intune.
- Un dispositivo [con co-gestione](../../comanage/overview.md) che esegue Windows 10 Enterprise, versione 1903 o successiva con il [carico di lavoro delle app client](../../comanage/workloads.md#client-apps) impostato su Configuration Manager.

### <a name="licensing-prerequisites"></a>Prerequisiti per le licenze

La funzionalità Analisi degli endpoint è inclusa nei piani seguenti: 

- [Enterprise Mobility + Security E3](https://www.microsoftvolumelicensing.com/ProductResults.aspx?doc=Product%20Terms,OST&fid=51) o superiore
- [Microsoft 365 Enterprise E3](https://www.microsoft.com/en-us/microsoft-365/enterprise?rtc=1) o superiore.

Per le correzioni proattive è richiesta anche una delle licenze seguenti per i dispositivi gestiti:
- Windows 10 Enterprise E3 o E5 (incluso in Microsoft 365 F3, E3 o E5)
- Windows 10 Education A3 o A5 (incluso in Microsoft 365 A3 o A5)
- Accesso a Desktop virtuale Windows E3 o E5

### <a name="permissions"></a>Autorizzazioni

#### <a name="endpoint-analytics-permissions"></a>Autorizzazioni di Analisi degli endpoint

Per Analisi degli endpoint vengono usate le autorizzazioni seguenti:
- **Lettura** nella categoria **Configurazioni dispositivi**.
- **Lettura** nella categoria **Organizzazione**. <!--temporary for pp-->
- Autorizzazioni appropriate al ruolo dell'utente nella categoria **Analisi degli endpoint**.

Un utente di sola lettura richiederà solo l'autorizzazione **Lettura** sia nella categoria **Configurazioni dispositivi** sia nella categoria **Analisi degli endpoint**. Un amministratore di Intune richiede in genere tutte le autorizzazioni.

#### <a name="proactive-remediations-permissions"></a>Autorizzazioni Correzioni proattive

Per Correzioni proattive l'utente deve avere le autorizzazioni appropriate per il ruolo nella categoria **Configurazioni dispositivi**.  Le autorizzazioni nella categoria **Analisi degli endpoint** non sono necessarie se l'utente usa solo Correzioni proattive.

## <a name="start-gathering-data"></a><a name="bkmk_uea_start"></a> Iniziare a raccogliere i dati
- Se si stanno registrando solo i dispositivi gestiti di Intune, passare alla sezione [Eseguire l'onboarding nel portale di Analisi degli endpoint](#bkmk_uea_onboard).

- Se si stanno registrando i dispositivi gestiti da Configuration Manager, eseguire i passaggi seguenti:
   - [Abilitare la raccolta dati di Analisi degli endpoint in Configuration Manager](#bkmk_uea_cm_enroll)
   - [Abilitare il caricamento dei dati in Configuration Manager](#bkmk_uea_cm_upload)
   - [Eseguire l'onboarding nel portale di Analisi degli endpoint](#bkmk_uea_onboard)  

### <a name="enroll-devices-managed-by-configuration-manager"></a><a name="bkmk_uea_cm_enroll"></a> Registrare i dispositivi gestiti da Configuration Manager
<!--6051638, 5924760-->
Prima di registrare i dispositivi di Configuration Manager verificare i [prerequisiti](#bkmk_uea_prereq), inclusa l'abilitazione dell'[associazione del tenant Microsoft Endpoint Manager](https://docs.microsoft.com/mem/configmgr/tenant-attach/device-sync-actions). Se si stanno registrando solo i dispositivi gestiti di Intune, passare alla sezione [Eseguire l'onboarding nel portale di Analisi degli endpoint](#bkmk_uea_onboard).

#### <a name="enable-endpoint-analytics-data-collection-in-configuration-manager"></a><a name="bkmk_uea_cm_enable"></a> Abilitare la raccolta dati di Analisi degli endpoint in Configuration Manager

1. Nella console di Configuration Manager passare a **Amministrazione** > **Impostazioni client** > **Impostazioni client predefinite**.
1. Fare clic con il pulsante destro del mouse e selezionare **Proprietà**, quindi selezionare le impostazioni **Agente computer**.
1. Impostare **Enable Endpoint analytics data collection** (Abilita raccolta dati di Analisi degli endpoint) su **Sì**.
   > [!Important] 
   > Se si ha un'impostazione dell'agente client personalizzata esistente che è stata distribuita nei dispositivi, sarà necessario aggiornare l'opzione **Enable Endpoint analytics data collection** (Abilita raccolta dati di Analisi degli endpoint) nell'impostazione personalizzata, quindi ridistribuirla nei computer in modo che abbia effetto.

#### <a name="enable-data-upload-in-configuration-manager"></a><a name="bkmk_uea_cm_upload"></a> Abilitare il caricamento dei dati in Configuration Manager

1. Nella console di Configuration Manager accedere a **Amministrazione** > **Servizi cloud** > **Co-gestione**.
1. Selezionare **CoMgmtSettingsProd** e fare clic su **Proprietà**.
1. Nella scheda **Configure upload** (Configura caricamento) selezionare l'opzione **Abilita Analisi degli endpoint per dispositivi caricati in Microsoft Endpoint Manager**.

   :::image type="content" source="media/6051638-configure-upload-configmgr.png" alt-text="Abilita Analisi degli endpoint per dispositivi caricati in Microsoft Endpoint Manager" lightbox="media/6051638-configure-upload-configmgr.png":::

### <a name="onboard-in-the-endpoint-analytics-portal"></a><a name="bkmk_uea_onboard"></a> Eseguire l'onboarding nel portale di Analisi degli endpoint
L'onboarding dal portale di Analisi degli endpoint è necessario sia per i dispositivi gestiti da Configuration Manager sia per quelli gestiti da Intune.

1. Passare a `https://endpoint.microsoft.com/#blade/Microsoft_Intune_Enrollment/UXAnalyticsMenu`
1. Fare clic su **Avvia**. Verrà assegnato automaticamente un profilo di configurazione per raccogliere i dati sulle prestazioni di avvio da tutti i dispositivi idonei. È possibile [modificare i dispositivi assegnati](#bkmk_uea_profile) in un secondo momento. Il popolamento dei dati sulle prestazioni di avvio nei dispositivi registrati in Intune dopo il riavvio può richiedere fino a 24 ore.
   - Per altre informazioni sui problemi comuni, vedere [Risoluzione dei problemi relativi alle prestazioni di avvio dei dispositivi registrati](#bkmk_uea_enrollment_tshooter).

## <a name="overview-page"></a>Pagina di panoramica

Quando i dati sono pronti, si noteranno alcune informazioni nella pagina di **panoramica**, illustrata più in dettaglio di seguito:

- Il **punteggio dell'esperienza utente** è una media ponderata 50/50 del **software consigliato** e dei **punteggi delle prestazioni di avvio**. Il set di punteggi parziali verrà ampliato nel tempo.

- È possibile confrontare il punteggio corrente con altri punteggi impostando una linea di base.
  - Come descritto nella sezione relativa alla [linea di base](#bkmk_uea_baselines), esiste una linea di base predefinita per *Mediana commerciale* per vedere come si esegue il confronto con un'azienda tipica. È possibile creare nuove linee di base facendo riferimento alle metriche correnti, in modo da tenere traccia dello stato di avanzamento o visualizzare le regressioni nel tempo.
   - Gli indicatori della linea di base sono visualizzati per il punteggio complessivo e i punteggi parziali. Se uno dei punteggi regredisce oltre la soglia configurabile rispetto alla linea di base selezionata, il punteggio viene visualizzato in rosso e il punteggio di primo livello viene contrassegnato come elemento che richiede attenzione.
  - Lo stato **dati insufficienti** significa che non si ha a disposizione un numero sufficiente di dispositivi per ottenere un punteggio significativo. Attualmente sono necessari almeno cinque dispositivi.

- I **filtri** consentiranno di visualizzare il punteggio in un sottogruppo di dispositivi o utenti. Tuttavia, la funzionalità di filtro non è abilitata in questa versione di anteprima.

- Per migliorare il punteggio, consultare l'elenco di **informazioni dettagliate e raccomandazioni**, ordinate in base alla priorità. L'elenco è filtrato in base al contesto del sottonodo quando si passa a **Procedure consigliate** o **Software consigliato**.

[![Pagina Panoramica di Analisi degli endpoint](media/overview-page.png)](media/overview-page.png#lightbox)

## <a name="recommended-software"></a><a name="bkmk_uea_rs"></a> Software consigliato

> [!Important]  
> Analisi degli endpoint calcola il **Punteggio di adozione del software** per tutti i dispositivi gestiti da Intune, indipendentemente dal fatto che siano stati registrati o meno in Analisi degli endpoint.

Alcuni software sono noti per migliorare l'esperienza dell'utente finale, indipendentemente dalle metriche di integrità di livello inferiore. Windows 10, ad esempio, ha un punteggio Net Promoter molto più elevato rispetto a Windows 7. Il punteggio di **adozione del software** è un numero compreso tra 0 e 100 che rappresenta una media ponderata della percentuale di dispositivi in cui sono stati distribuiti diversi software consigliati. La ponderazione corrente è superiore per Windows rispetto alle altre metriche poiché gli utenti interagiscono con essi più di frequente. Le metriche sono descritte di seguito: 

[![Pagina Software consigliato di Analisi degli endpoint](media/recommended-software.png)](media/recommended-software.png#lightbox)

### <a name="windows-10"></a><a name="bkmk_uea_win10"></a> Windows 10

Windows 10 offre un'esperienza utente migliore rispetto alle versioni precedenti di Windows. Per altre informazioni, vedere il [white paper TEI](https://vc2prod.blob.core.windows.net/vc-resources/TEIStudies/TEI%20of%20Windows%2010.pdf).

Questa metrica misura la percentuale di dispositivi in Windows 10 rispetto a una versione precedente di Windows.

L'azione di correzione consigliata per il passaggio dei dispositivi dalle versioni precedenti di Windows è creare un piano di distribuzione usando [Desktop Analytics](../../desktop-analytics/overview.md).

### <a name="autopilot"></a><a name="bkmk_uea_ap"></a> Autopilot

Microsoft Autopilot offre un'esperienza di provisioning iniziale dei PC Windows 10 più semplice rispetto all'esperienza nativa; presenta infatti un numero di schermate inferiore nella configurazione guidata e fornisce le impostazioni predefinite per assicurarsi che venga correttamente eseguito il provisioning dei dispositivi dei dipendenti sia dalla factory che in fase di reimpostazione.

Questa metrica misura la percentuale di dispositivi Windows 10 registrati per Autopilot.

L'azione di correzione consigliata è registrare i dispositivi esistenti in Autopilot usando [Microsoft Intune](https://docs.microsoft.com/intune/enrollment-autopilot).

### <a name="azure-active-directory"></a><a name="bkmk_uea_aad"></a> Azure Active Directory

Azure Active Directory (Azure AD) offre agli utenti numerosi vantaggi di produttività, tra cui l'accesso Single Sign-On a livello di dispositivo per app e servizi, l'accesso a Windows Hello, il ripristino self-service della chiave BitLocker e il roaming dei dati aziendali.

Questa metrica misura la percentuale di dispositivi registrati in Azure AD.

I dispositivi gestiti in Microsoft Intune sono già registrati in Azure AD. L'azione di correzione consigliata per i dispositivi gestiti da Configuration Manager è [registrarli in Azure AD](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains) o [co-gestirli](../../comanage/overview.md). La co-gestione dei dispositivi migliora anche il punteggio della gestione cloud.

### <a name="cloud-management"></a><a name="bkmk_uea_intune"></a> Gestione cloud

Microsoft Intune offre agli utenti diversi vantaggi per la produttività, tra cui l'abilitazione dell'accesso alle risorse aziendali anche quando si trovano fuori dalla rete aziendale, oltre ad eliminare la necessità di usare Criteri di gruppo, evitando così un sovraccarico di prestazioni e garantendo una migliore esperienza dell'utente finale. Questa metrica misura la percentuale di PC registrati in Microsoft Intune. Informazioni su come [Microsoft sta abilitando questa funzionalità per i propri dipendenti](https://www.microsoft.com/en-us/itshowcase/managing-windows-10-devices-with-microsoft-intune).

L'azione di correzione consigliata per i dispositivi gestiti da Configuration Manager non ancora registrati in Intune è [co-gestirli](../../comanage/overview.md).

### <a name="no-commercial-median"></a><a name="bkmk_uea_np"></a> Nessuna mediana commerciale

La linea di base predefinita **Mediana commerciale** attualmente non ha metriche per i punteggi parziali indicati nelle sezioni precedenti.

## <a name="startup-performance"></a><a name="bkmk_uea_bp"></a> Prestazioni di avvio

> [!NOTE]
> Se non vengono visualizzati dati sulle prestazioni di avvio da tutti i dispositivi, vedere [Risoluzione dei problemi relativi alle prestazioni di avvio dei dispositivi registrati](#bkmk_uea_enrollment_tshooter).

Il punteggio delle prestazioni di avvio consente all'IT di guidare rapidamente gli utenti dall'accensione alla produttività, senza lunghi ritardi nelle procedure di avvio e accesso. Il **punteggio di avvio** è un numero compreso tra 0 e 100. Questo punteggio è una media ponderata del **punteggio di avvio** e del punteggio di **accesso**, che vengono calcolati come segue:

- **Punteggio di avvio**: Basato sul tempo che trascorre tra l'accensione e l'accesso. Si prende in considerazione l'ultimo tempo di avvio di ogni dispositivo, esclusa la fase di aggiornamento, quindi si assegna un punteggio tra 0 (scarso) e 100 (eccezionale). Su questi punteggi viene calcolata una media per ottenere un punteggio complessivo dell'avvio del tenant.
- **Punteggio di accesso**: in base al tempo che trascorre da quando vengono immesse le credenziali fino a quando l'utente non riesce ad accedere a un desktop reattivo (a indicare che il rendering del desktop è stato eseguito e l'utilizzo della CPU è sceso al di sotto del 50% per almeno 2 secondi). Si prende in considerazione l'ultimo tempo di accesso per ogni dispositivo, esclusi i primi accessi o gli accessi eseguiti subito dopo l'aggiornamento di una funzionalità, quindi si assegna un punteggio compreso tra 0 (scarso) e 100 (eccezionale). Su questi punteggi viene calcolata una media per ottenere un punteggio complessivo dell'avvio del tenant.

[![Pagina Prestazioni di avvio di Analisi degli endpoint](media/startup-performance.png)](media/startup-performance.png#lightbox)

### <a name="insights"></a>Informazioni dettagliate

La pagina **Prestazioni di avvio** contiene anche un elenco di **informazioni dettagliate e raccomandazioni**, ordinate in base alla priorità, descritte nelle sezioni seguenti:

#### <a name="hard-disk-drives"></a><a name="bkmk_uea_hdd"></a> Unità disco rigido

Le prestazioni di avvio offrono informazioni dettagliate sul numero di dispositivi in cui l'unità di avvio è un disco rigido. Le unità disco rigido per l'avvio in genere richiedono tempi da tre a quattro volte più lunghi rispetto alle unità SSD. È anche previsto un miglioramento delle prestazioni di avvio se si passa alle unità SSD.

Fare clic per visualizzare l'elenco dei dispositivi con unità disco rigido. L'azione consigliata è aggiornare questi dispositivi alle unità SSD.

#### <a name="group-policy"></a><a name="bkmk_uea_gp"></a> Criteri di gruppo

Le prestazioni di avvio offrono informazioni dettagliate sul numero di dispositivi che presentano ritardi nell'avvio e nell'accesso a causa di Criteri di gruppo. Fare clic per visualizzare i dispositivi. La visualizzazione è ordinata in base al tempo di Criteri di gruppo, quindi è possibile vedere quali sono i dispositivi interessati per ulteriori procedure di risoluzione dei problemi.

Se si fa clic su un dispositivo specifico, è possibile visualizzarne la cronologia degli avvii e degli accessi. La cronologia consente di determinare se il problema è una regressione e quando potrebbe essersi verificato.

Sebbene esistano molti articoli su come ottimizzare le prestazioni di Criteri di gruppo, è possibile scegliere di eseguire la migrazione alla gestione cloud. La migrazione alla gestione cloud consente di usare le [linee di base di sicurezza di Intune](https://docs.microsoft.com/intune/protect/security-baselines) e lo strumento di analisi dei criteri presto disponibile.

#### <a name="slow-boot-and-sign-in-times"></a><a name="bkmk_uea_sb"></a> Tempi di avvio e accesso lenti

Le prestazioni di avvio offrono informazioni dettagliate sul numero di dispositivi con tempi di avvio o accesso lenti. Un punteggio di avvio o di accesso pari a "0" significa lento. Fare clic per visualizzare i dispositivi. I dispositivi sono ordinati rispettivamente in base al tempo di avvio core o al tempo di accesso di base, quindi è possibile visualizzare i dispositivi interessati per ulteriori procedure di risoluzione dei problemi.

Se si fa clic su un dispositivo specifico, è possibile visualizzarne la cronologia degli avvii e degli accessi. La cronologia consente di determinare se il problema era una regressione e quando potrebbe essersi verificato.

### <a name="reporting-tabs"></a>Schede per la creazione di report

La pagina **Prestazioni di avvio** include schede per la creazione di report che forniscono supporto per le informazioni dettagliate, tra cui:
1. **Prestazioni del modello**. Questa scheda consente di visualizzare le prestazioni di avvio e di accesso in base al modello di dispositivo, utili per identificare se i problemi di prestazioni riguardano solo modelli specifici.
1. **Prestazioni del dispositivo**. Questa scheda fornisce le metriche di avvio e di accesso per tutti i dispositivi. È possibile ordinare i dati in base a una metrica specifica, come il tempo di accesso a un GP, per vedere quali dispositivi hanno i punteggi peggiori per la metrica e facilitare la risoluzione dei problemi. È anche possibile cercare un dispositivo in base al nome. Se si fa clic su un dispositivo, è possibile visualizzarne la cronologia di avvio e accesso, che consente di identificare se è presente una regressione recente
1. **Processi di avvio**. In questa scheda (se visibile, perché è stata distribuita solo ad alcuni utenti dato che questa funzionalità è ancora in corso di sviluppo) saranno indicati i processi che incidono sulla fase di accesso "tempo per risposta del desktop" (ovvero mantenere l'utilizzo della CPU superiore al 50% dopo il rendering del desktop).

## <a name="proactive-remediations"></a><a name="bkmk_uea_prs"></a> Correzioni proattive

Le correzioni proattive sono pacchetti di script che consentono di rilevare e risolvere problemi di supporto comuni in un dispositivo prima che l'utente si renda conto che si è verificato un problema. Queste correzioni consentono di ridurre le chiamate al supporto tecnico. È possibile creare un pacchetto di script personalizzato o distribuire uno dei pacchetti di script scritti e usati nell'ambiente per ridurre i ticket di supporto.

Ogni pacchetto di script è costituito da uno script di rilevamento, uno script di correzione e metadati. Con Intune sarà possibile distribuire questi pacchetti di script e visualizzare i report sulla loro efficacia. Microsoft sta sviluppando attivamente nuovi pacchetti di script e invita gli utenti a condividere le proprie esperienze. Rivolgersi al proprio contatto per l'anteprima di Analisi degli endpoint per condividere commenti e suggerimenti sui pacchetti di script.

### <a name="get-the-detection-and-remediation-scripts"></a><a name="bkmk_uea_prs_ps1"></a> Ricevere gli script di rilevamento e correzione

1. Copiare gli script riportati in fondo a questo articolo nella sezione [Script di PowerShell](#bkmk_uea_ps_scripts).
    - I file di script i cui nomi iniziano con `det` sono script di rilevamento. Gli script di correzione iniziano con `rem`.
    - Per informazioni sui singoli script, vedere [Descrizioni degli script](#bkmk_uea_scripts).
1. Salvare ogni script usando il nome specificato. Il nome è anche indicato nei commenti all'inizio di ogni script.
    - È possibile usare un altro nome di script, ma non corrisponderà al nome indicato nella sezione [Descrizioni degli script](#bkmk_uea_scripts).


### <a name="deploying-and-monitoring-scripts"></a><a name="bkmk_uea_prs_deploy"></a> Distribuzione e monitoraggio di script
Il servizio **Microsoft Intune Management Extension** ottiene gli script da Intune e li esegue. Gli script vengono rieseguiti ogni 24 ore. Per distribuire e monitorare gli script, seguire questa procedura:

1. Passare al nodo **Correzioni proattive** nella console.
1. Fare clic sul pulsante **Crea un pacchetto di script** per creare un pacchetto di script.
     [![Pagina Correzioni proattive di Analisi degli endpoint. Selezionare il collegamento Crea.](media/proactive-remediations-create.png)](media/proactive-remediations-create.png#lightbox)
1. Nel passaggio delle **nozioni di base** assegnare al pacchetto di script un **nome** e, facoltativamente, una **descrizione**. Il campo del **server di pubblicazione** può essere modificato, ma per impostazione predefinita contiene il nome del tenant. Non è possibile modificare la **versione**. 
1. Nel passaggio delle **impostazioni** copiare il testo dagli script scaricati nei campi **Script di rilevamento** e **Script di monitoraggio e aggiornamento**. 
   - È necessario che lo script di rilevamento e lo script di correzione corrispondenti siano nello stesso pacchetto. Ad esempio, lo script di rilevamento `Detect_stale_Group_Policies.ps1` corrisponde allo script di correzione `Remediate_stale_GroupPolicies.ps1`.
       [![Pagina delle impostazioni di script per Correzioni proattive di Analisi degli endpoint.](media/proactive-remediations-script-settings.png)](media/proactive-remediations-script-settings.png#lightbox)
1. Completare le opzioni nella pagina **Impostazioni** con le seguenti configurazioni consigliate:
   - **Esegui lo script con le credenziali dell'utente connesso**: Configurazione che dipende dallo script. Per altre informazioni, vedere la sezione [Descrizioni degli script](#bkmk_uea_scripts).
   - **Imponi il controllo della firma degli script**: No
   - **Esegui lo script in PowerShell a 64 bit**: No
1. Fare clic su **Avanti** quindi assegnare i **tag di ambito** necessari.
1. Nel passaggio delle **assegnazioni** selezionare i gruppi di dispositivi in cui verrà distribuito il pacchetto di script.
1. Completare il passaggio di **verifica e creazione** per la distribuzione.
1. In **Reporting** > **Analisi degli endpoint - Correzioni proattive** è possibile visualizzare una panoramica dello stato del rilevamento e delle correzioni.
       [![Report in Correzioni proattive di Analisi degli endpoint, pagina di panoramica.](media/proactive-remediations-report-overview.png)](media/proactive-remediations-report-overview.png#lightbox)
1. Fare clic su **Stato dispositivo** per ottenere i dettagli sullo stato per ogni dispositivo della distribuzione.
       [![Stato dispositivo in Correzioni proattive di Analisi degli endpoint.](media/proactive-remediations-device-status.png)](media/proactive-remediations-device-status.png#lightbox)


## <a name="endpoint-analytics-settings"></a><a name="bkmk_uea_set"></a> Impostazioni di Analisi degli endpoint

Dalla pagina delle impostazioni è possibile selezionare **Generale** o **Linea di base**. Di seguito sono descritte entrambe le impostazioni.

### <a name="general"></a><a name="bkmk_uea_gen"></a> Generale

La pagina **Generale** in **Impostazioni** consente di verificare se è stata abilitata la raccolta dei dati sulle prestazioni di avvio di Intune. Per impostazione predefinita, viene abilitata automaticamente per tutti i dispositivi quando si fa clic su **Avvia** per abilitare l'analisi dell'esperienza utente. È possibile scegliere di passare al nodo Criteri di raccolta dati di Intune per modificare il set di dispositivi per cui vengono raccolti i record di avvio e di accesso.


#### <a name="intune-data-collection-policy"></a><a name="bkmk_uea_profile"></a> Criteri di raccolta dati di Intune

Per assegnare questa impostazione a un subset di dispositivi, [creare un profilo](/intune/configuration/device-profile-create#create-the-profile) con le informazioni seguenti: 

  - **Nome**: immettere un nome descrittivo per il profilo, ad esempio **Criteri di raccolta dati di Intune**
   
  - **Descrizione**: Immettere una descrizione del profilo. Questa impostazione è facoltativa ma consigliata.
    
  - **Piattaforma**: selezionare **Windows 10 e versioni successive**
   
  - **Tipo di profilo**: selezionare **Monitoraggio dello stato di Windows**
   
  - Configurare le **impostazioni**:
   
       - **Monitoraggio dello stato di integrità**: selezionare **Abilita** per raccogliere informazioni sugli eventi dai dispositivi Windows 10
    
    - **Ambito**: Selezionare **Prestazioni di avvio** 

  - Usare i [tag di ambito](/intune/configuration/device-profile-create#scope-tags) e le [regole di applicabilità](/intune/configuration/device-profile-create#applicability-rules) per filtrare il profilo in base a gruppi IT o dispositivi specifici in un gruppo che soddisfano criteri specifici.

> [!NOTE]
> È disponibile un segnaposto per le istruzioni per la configurazione del connettore dati di Configuration Manager. Questa funzionalità, tuttavia, non è stata implementata in questa anteprima privata iniziale.

  [![Pagina delle impostazioni generali di Analisi degli endpoint](media/settings-general.png)](media/settings-general.png#lightbox)

### <a name="baseline-management"></a><a name="bkmk_uea_baselines"></a> Gestione della linea di base

È possibile confrontare i punteggi totali e parziali correnti con altri punteggi impostando una linea di base.

1. È disponibile una linea di base predefinita per **Mediana commerciale**, che consente di confrontare i punteggi con un'azienda tipo.
1. È possibile creare nuove linee di base facendo riferimento alle metriche correnti per tenere traccia dello stato di avanzamento o visualizzare le regressioni nel tempo. Fare clic sul pulsante **Crea nuovo** e assegnare un nome alla nuova linea di base. Si consiglia di usare un nome che includa la data, poiché è più semplice effettuare una selezione dall'elenco a discesa nelle pagine dei report.
1. È previsto un limite di 100 linee di base per ogni tenant. È possibile eliminare le linee di base obsolete che non sono più necessarie.
1. Le metriche correnti verranno contrassegnate in rosso e visualizzate come regressione se scendono sotto la linea di base corrente nei report. Poiché è perfettamente normale una variazione delle metriche da un giorno all'altro, è possibile impostare una soglia di regressione, che per impostazione predefinita è 10%. Con questa soglia, le metriche vengono contrassegnate come regressione solo se la regressione è superiore al 10%.

   [![Pagina delle impostazioni della linea di base di Analisi degli endpoint](media/settings-baseline.png)](media/settings-baseline.png#lightbox)

## <a name="troubleshooting"></a><a name="bkmk_uea_tshoot"></a> Risoluzione dei problemi

Le sezioni seguenti possono essere usate per facilitare la risoluzione dei problemi che possono verificarsi.

### <a name="troubleshooting-startup-performance-device-enrollment"></a><a name="bkmk_uea_enrollment_tshooter"></a> Risoluzione dei problemi relativi alle prestazioni di avvio dei dispositivi registrati

Se la pagina di panoramica mostra un punteggio delle prestazioni di avvio pari a zero, accompagnato da un banner che indica che è in attesa di dati, o se la scheda delle prestazioni del dispositivo delle prestazioni di avvio mostra un numero inferiore di dispositivi rispetto a quanto previsto, è possibile adottare alcune misure per risolvere il problema.

Per prima cosa, di seguito è riportato un breve riepilogo delle limitazioni per la raccolta dei dati sulle prestazioni di avvio:
1. I dispositivi devono eseguire Windows 10 versione 1903 o successive.
2. I dispositivi devono essere aggiunti ad Azure AD. Attualmente non sono supportati i dispositivi aggiunti all'area di lavoro, anche se si sta esaminando attivamente la possibilità di aggiungere questa funzionalità a Windows.
3. I dispositivi devono disporre di Windows 10 Enterprise Edition. Windows 10 Home e Professional non sono attualmente supportati, sebbene si stia esaminando attivamente la fattibilità dell'aggiunta di questa funzionalità a Windows.

Si noti che questi problemi non si applicano ai dati provenienti dal prossimo connettore di Configuration Manager, che sarà in grado di raccogliere i dati da qualsiasi PC client di Configuration Manager, indipendentemente dalla configurazione di versione, edizione o directory.

In secondo luogo, di seguito è riportato un elenco di controllo rapido da usare per la risoluzione dei problemi:
1. Verificare che il profilo di monitoraggio dell'integrità di Windows sia destinato a tutti i dispositivi per i quali si vogliono recuperare i dati sulle prestazioni. È possibile trovare un collegamento a questo profilo nella pagina delle impostazioni di Analisi degli endpoint oppure passare a tale profilo come si farebbe per qualsiasi altro profilo di Intune. Esaminare la scheda dell'assegnazione per assicurarsi che sia assegnato al set di dispositivi previsto. 
1. Controllare quali dispositivi sono stati configurati correttamente per la raccolta dei dati. È anche possibile visualizzare queste informazioni nella pagina di panoramica del profilo.  
   - Esiste un problema noto a causa del quale i clienti possono visualizzare errori di assegnazione del profilo, per cui i dispositivi interessati mostrano il codice di errore `-2016281112 (Remediation failed)`. Sono in corso indagini per risolvere questo problema.
1. I dispositivi configurati correttamente per la raccolta dei dati devono essere riavviati dopo l'abilitazione della raccolta dei dati ed è poi necessario attendere fino a 24 ore prima che il dispositivo venga visualizzato nella scheda delle prestazioni dei dispositivi.
1. Se il dispositivo è stato configurato correttamente per la raccolta dei dati, è stato poi riavviato e dopo 24 ore non viene ancora visualizzato, è possibile che il dispositivo non riesca a raggiungere gli endpoint di raccolta. Questo problema può verificarsi se l'azienda usa un server proxy e se gli endpoint non sono stati abilitati nel proxy. Per altre informazioni, vedere [Risoluzione dei problemi relativi agli endpoint](#bkmk_uea_endpoints).


### <a name="endpoints"></a><a name="bkmk_uea_endpoints"></a> Endpoint

Per registrare i dispositivi per Analisi degli endpoint, è necessario inviare i dati funzionali richiesti a Microsoft. Se l'ambiente usa un server proxy, usare queste informazioni per configurare il proxy.

Per abilitare la condivisione dei dati funzionali, configurare il server proxy in modo che consenta gli endpoint seguenti:

> [!Important]  
> Per la privacy e l'integrità dei dati, Windows verifica la presenza di un certificato SSL Microsoft (associazione del certificato) durante la comunicazione con gli endpoint di condivisione dei dati funzionali richiesti. L'intercettazione e l'ispezione SSL non sono possibili. Per usare Analisi degli endpoint, escludere questi endpoint dall'ispezione SSL.<!-- BUG 4647542 -->

| Endpoint  | Funzione  |
|-----------|-----------|
| `https://*.events.data.microsoft.com` | Usato per inviare i [dati funzionali richiesti](#bkmk_uea_datacollection) all'endpoint di raccolta dati di Intune. |
| `https://graph.windows.net` | Usato per recuperare automaticamente le impostazioni quando si connette la gerarchia ad Analisi degli endpoint (per il ruolo del server di Configuration Manager). Per altre informazioni, vedere [Configurare il proxy per un server del sistema del sito](../plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |
| `https://*.manage.microsoft.com` | Usato per sincronizzare la raccolta di dispositivi e i dispositivi con Analisi degli endpoint (solo per il ruolo del server di Configuration Manager). Per altre informazioni, vedere [Configurare il proxy per un server del sistema del sito](../plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |


### <a name="proxy-server-authentication"></a>Autenticazione del server proxy

Se l'organizzazione usa l'autenticazione del server proxy per l'accesso a Internet, verificare che non blocchi i dati a causa dell'autenticazione. Se il proxy non consente ai dispositivi di inviare questi dati, non verranno visualizzati in Desktop Analytics.

#### <a name="bypass-recommended"></a>Ignorare (scelta consigliata)

Configurare i server proxy in modo che non richiedano l'autenticazione proxy per il traffico verso gli endpoint di condivisione dei dati. Questa opzione è la soluzione più completa. Può essere usata per tutte le versioni di Windows 10.  

#### <a name="user-proxy-authentication"></a>Autenticazione proxy dell'utente

Configurare i dispositivi per l'uso del contesto dell'utente connesso per l'autenticazione proxy. Questo metodo richiede le configurazioni seguenti:

- Dispositivi con aggiornamento qualitativo corrente per una versione supportata di Windows

- Configurare il proxy a livello di utente (proxy WinINET) in **Impostazioni proxy** nel gruppo Rete e Internet delle Impostazioni di Windows. È anche possibile usare il pannello di controllo Opzioni Internet legacy.

- Verificare che gli utenti abbiano l'autorizzazione proxy per raggiungere gli endpoint di condivisione dei dati. Poiché questa opzione richiede che i dispositivi abbiano utenti console con autorizzazioni proxy, non è possibile usare questo metodo con dispositivi senza intestazioni.

> [!IMPORTANT]
> L'approccio di autenticazione proxy dell'utente non è compatibile con l'uso di Microsoft Defender Advanced Threat Protection. Questo comportamento è dovuto al fatto che questa autenticazione si basa sulla chiave del Registro di sistema **DisableEnterpriseAuthProxy** impostata su `0`, mentre Microsoft Defender ATP richiede che sia impostata su `1`. Per altre informazioni, vedere [Configurare le impostazioni del proxy del computer e della connettività Internet in Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/configure-proxy-internet-windows-defender-advanced-threat-protection).

#### <a name="device-proxy-authentication"></a>Autenticazione proxy del dispositivo

Questo approccio supporta gli scenari seguenti:

- Dispositivi senza intestazioni, in cui nessun utente esegue l'accesso o gli utenti del dispositivo non hanno accesso a Internet

- Proxy autenticati che non usano l'autenticazione integrata di Windows

- Se si usa anche Microsoft Defender Advanced Threat Protection

Questo approccio è il più complesso poiché richiede le configurazioni seguenti:

- Assicurarsi che i dispositivi possano raggiungere il server proxy tramite WinHTTP nel contesto del sistema locale. Usare una delle opzioni seguenti per configurare questo comportamento:

  - `netsh winhttp set proxy` sulla riga di comando

  - Protocollo WPAD (Web Proxy Auto-Discovery)

  - Proxy trasparente

  - Configurare il proxy WinINET a livello di dispositivo usando la seguente impostazione dei criteri di gruppo: **Specificare le impostazioni proxy per computer (anziché per utente)** (ProxySettingsPerUser = `1`)

  - Connessione indirizzata o che usa NAT (Network Address Translation)

- Configurare i server proxy per consentire agli account del computer in Active Directory di accedere agli endpoint dei dati. Questa configurazione richiede che i server proxy supportino l'Autenticazione integrata di Windows.  


## <a name="frequently-asked-questions"></a><a name="bkmk_uea_faq"></a> Domande frequenti

### <a name="will-my-endpoint-analytics-data-migrate-if-i-move-my-intune-tenant-to-a-different-tenant-location"></a>Se si sposta il tenant di Intune in una posizione del tenant diversa, i dati di Analisi degli endpoint verranno sottoposti a migrazione?

Se si esegue la migrazione del tenant di Intune in una posizione diversa, tutti i dati presenti nella soluzione Analisi degli endpoint al momento della migrazione andranno perduti. Poiché gli endpoint creano report in modo continuativo in Analisi degli endpoint, tutti gli eventi che si verificano dopo la migrazione vengono caricati automaticamente nella nuova posizione del tenant e i report iniziano a essere ripopolati, a condizione che i dispositivi rimangano registrati correttamente. 

### <a name="why-are-the-scripts-exiting-with-a-code-of-1"></a>Perché gli script si chiudono con codice 1?

Gli script si chiudono con codice 1 per segnalare a Intune che è necessaria una correzione. In questo caso, la chiusura di uno script di rilevamento con 1 indica che è vero che è necessaria la correzione. Molti pacchetti di script eseguiti esclusivamente in CM possono risultare conformi, ma si chiudono con codice 1. Per questi script, la chiusura con codice 1 non indica un problema grave, ma è opportuno verificare se la correzione nel dispositivo viene eseguita.

### <a name="why-did-the-update-stale-group-policies-script-return-with-error-0x87d00321"></a>Perché lo script di aggiornamento dei criteri di gruppo non aggiornati restituisce un errore 0x87D00321?

0x87D00321 è un errore di timeout esecuzione dello script. Questo errore si verifica in genere con i computer connessi in remoto. Una possibile mitigazione potrebbe essere effettuare la distribuzione solo in una raccolta dinamica di computer con connettività di rete interna.

## <a name="script-descriptions"></a><a name="bkmk_uea_scripts"></a> Descrizioni degli script

In questa tabella sono riportati i nomi degli script, le descrizioni, i rilevamenti, le correzioni e gli elementi configurabili. I file di script i cui nomi iniziano con `Detect` sono script di rilevamento. Gli script di correzione iniziano con `Remediate`. Questi script possono essere copiati dalla sezione successiva di questo articolo.

|Nome script|Descrizione|
|---|---|
|**Update stale Group Policies** (Aggiorna criteri di gruppo non aggiornati) </br>`Detect_stale_Group_Policies.ps1` </br> `Remediate_stale_GroupPolicies.ps1`| Rileva se l'ultimo aggiornamento dei criteri di gruppo è precedente a `7 days`.  </br>Personalizzare la soglia di 7 giorni modificando il valore per `$numDays` nello script di rilevamento. </br></br>Le correzioni vengono applicate eseguendo `gpupdate /target:computer /force` e `gpupdate /target:user /force`  </br> </br>Può aiutare a ridurre le chiamate al supporto tecnico relative alla connettività di rete quando i certificati e le configurazioni vengono recapitati con Criteri di gruppo. </br> </br> **Esegui lo script con le credenziali dell'utente connesso**: Sì|
|**Restart Office Click-to-Run service** (Riavvia il servizio A portata di clic di Office) </br> `Detect_Click_To_Run_Service_State.ps1` </br> `Remediate_Click_To_Run_Service_State.ps1`| Rileva se il servizio A portata di clic è impostato per l'avvio automatico e se il servizio viene arrestato. </br> </br> Le correzioni vengono applicate impostando il servizio per l'avvio automatico e avviando il servizio se viene arrestato. </br></br> Consente di risolvere i problemi per cui App di Microsoft 365 per grandi imprese - Win32 non viene avviato perché il servizio A portata di clic viene arrestato. </br> </br> **Esegui lo script con le credenziali dell'utente connesso**: No|
|**Check network certificates** (Verifica certificati di rete) </br>`Detect_Expired_Issuer_Certificates.ps1` </br>`Remediate_Expired_Issuer_Certificates.ps1`|Rileva i certificati emessi da un'autorità di certificazione scaduti o prossimi alla scadenza nell'archivio personale del computer o dell'utente. </br> Per specificare l'autorità di certificazione, modificare il valore per `$strMatch` nello script di rilevamento. Specificare 0 per `$expiringDays` per trovare i certificati scaduti o specificare un altro numero di giorni per trovare i certificati prossimi alla scadenza.  </br></br>Le correzioni vengono applicate generando una notifica di tipo avviso popup per l'utente. </br> Specificare i valori `$Title` e `$msgText` con il titolo e il testo del messaggio che verrà visualizzato dagli utenti. </br> </br> Notifica agli utenti i certificati scaduti che potrebbero dover essere rinnovati. </br> </br> **Esegui lo script con le credenziali dell'utente connesso**: No|
|**Clear stale certificates** (Cancella certificati non aggiornati) </br>`Detect_Expired_User_Certificates.ps1` </br> `Remediate_Expired_User_Certificates.ps1`| Rileva i certificati scaduti emessi da un'autorità di certificazione nell'archivio personale dell'utente corrente. </br> Per specificare l'autorità di certificazione, modificare il valore per `$certCN` nello script di rilevamento. </br> </br> Per applicare la correzione, rileva nell'archivio personale dell'utente corrente i certificati scaduti emessi da un'autorità di certificazione. </br> Per specificare l'autorità di certificazione, modificare il valore per `$certCN` nello script di correzione. </br> </br> Rileva ed elimina i certificati scaduti emessi da un'autorità di certificazione nell'archivio personale dell'utente corrente. </br> </br> **Esegui lo script con le credenziali dell'utente connesso**: Sì|

## <a name="powershell-scripts"></a><a name="bkmk_uea_ps_scripts"></a> Script di PowerShell

### <a name="detect_stale_group_policiesps1"></a>Detect_stale_Group_Policies.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Detect_stale_Group_Policies.ps1
# Description:     Detect if Group Policy has been updated within number of days
# Notes:           Remediate if "Match", $numDays default value of 7, change as appropriate
#
#=============================================================================================================================

# Define Variables
$numDays = 7

try {
    $gpResult = gpresult /R | Select-String -pattern "Last time Group Policy was applied:" | Select-Object -last 1

    if ($gpResult){
    [int]$lastGPUpdateDays = (New-TimeSpan -Start $lastGPUpdateDate -End (Get-Date)).Days
        if ($lastGPUpdateDays -gt $numDays){
            #We want within last $numDays so we get "Match"
            Write-Host "Match"
            exit 1
        }
        else {
            #Script succeeds but > $numDays since last update so remediate
            #Exit 1 for Intune and "Match" for ConfigMan
            Write-Host "No_Match"
            exit 0
        }
    }
}
catch {
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="remediate_stale_grouppoliciesps1"></a>Remediate_stale_GroupPolicies.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Remediate_stale_GroupPolicies.ps1
# Description:     This script triggers Group Policy update
# Notes:           No variable substitution needed
#
#=============================================================================================================================

try{
    $compGP = gpupdate /target:computer /force | out-string
    $userGP = gpupdate /target:user /force | out-string
    exit 0
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="detect_click_to_run_service_stateps1"></a>Detect_Click_To_Run_Service_State.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Detect_Click_To_Run_Service_State.ps1
# Description:     Detect if Office 16 installed and if "Click to Run Service" is running.
# Notes:           No variable substitution should be necessary
#
#=============================================================================================================================

# Define Variables
$curSvcStat,$svcCTRSvc,$errMsg = "","",""

# Main script
If (-not (Test-Path -Path 'hklm:\Software\Microsoft\Office\16.0')){
    Return "Office 16.0 (or greater) not present on this machine"
    exit 0   
} 

Try{        
    $svcCTRSvc = Get-Service "ClickToRunSvc"
    $curSvcStat = $svcCTRSvc.Status
}

Catch{    
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}

If ($curSvcStat -eq "Running"){
    Write-Output $curSvcStat
    exit 0                        
}
Else{
    If($curSvcStat -eq "Stopped"){
    Write-Output $curSvcStat
    exit 1     
    }
}
Else{
    Write-Error "Error: " + $errMsg
    exit 1
}
```

### <a name="remediate_click_to_run_service_stateps1"></a>Remediate_Click_To_Run_Service_State.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Remediate_Click_To_Run_Service_State.ps1
# Description:     Start the "Click to Run Service" and change its startup type to Automatic
#       Notes:     No variable substitution needed
#
#=============================================================================================================================

# Define Variables
$svcCur = "ClickToRunSvc"
$curSvcStat,$svcCTRSvc,$errMsg = "","",""
$ctr = 0

# Main script
# Make sure nothing has changed since detection, the service exists and is stopped
Try{        
    $svcCTRSvc = Get-Service "ClickToRunSvc"
    $curSvcStat = $svcCTRSvc.Status
    }

Catch{    
    $errMsg = $_.Exception.Message
    }
        
# If the service got started between detection and now (nested if) then return
# If the service got uninstalled or corrupted between detection and now (else) then return the "Error: " + the error
If ($curSvcStat -ne "Stopped"){
    If ($curSvcStat -eq "Running"){
        return
    }
    Else{
        return "Error: " + $errMsg
    }
}

# Service should be there and stopped, change the startup type and start
Try{        
    Set-Service $svcCur -StartupType Automatic
    Start-Service $svcCur
    $svcCTRSvc = Get-Service $svcCur
    $curSvcStat = $svcCTRSvc.Status
        While ($curSvcStat.Equals("Stopped")){
            Start-Sleep -Seconds 5
            ctr++
            if(ctr == 12){
                Return "Service could not be started after 60 seconds"
                break
            }
        }
    }

Catch{    
    $errMsg = $_.Exception.Message
    Return $errMsg
    }

Return $curSvcStat
```

### <a name="detect_expired_issuer_certificatesps1"></a>Detect_Expired_Issuer_Certificates.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Detect_Expired_Issuer_Certificates.ps1
# Description:     Detect expired certificates issued by "CN=<your CA here>" in either Machine
#                  or User certificate store
# Notes:           Change the value of the variable $strMatch from "CN=<your CA here>" to "CN=..."
#                  For testing purposes the value of the variable $expiringDays can be changed to a positive integer
#                  Don't change the $results variable
#
#=============================================================================================================================

# Define Variables
$results = @()
$expiringDays = 0
$strMatch = "CN=<your CA here>"

try
{
    $results = @(Get-ChildItem -Path Cert:\LocalMachine\My -Recurse -ExpiringInDays $expiringDays | where {$_.Issuer -match $strMatch})
    $results += @(Get-ChildItem -Path Cert:\CurrentUser\My -Recurse -ExpiringInDays $expiringDays | where {$_.Issuer -match $strMatch}) 
    if (($results -ne $null)){
        #Below necessary for Intune as of 10/2019 will only remediate Exit Code 1
        Write-Host "Match"
        Return $results.count
        exit 1
    }
    else{
        #No matching certificates, do not remediate
        Write-Host "No_Match"        
        exit 0
    }   
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="remediate_expired_issuer_certificatesps1"></a>Remediate_Expired_Issuer_Certificates.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Remediate_Expired_Issuer_Certificates.ps1
# Description:     Raise a Toast Notification if expired certificates issued by "CN=..."
#                  to user or machine on the machine where detection script found them. No remediation action besides
#                  the Toast is taken.
# Notes:           Change the values of the variables $Title and $msgText
#
#=============================================================================================================================

## Raise toast to have user contact whoever is specified in the $msgText

# Define Variables
$delExpCert = 0
$Title = "Title"
$msgText = "message"

# Main script
[Windows.UI.Notifications.ToastNotificationManager, Windows.UI.Notifications, ContentType = WindowsRuntime] | Out-Null
[Windows.UI.Notifications.ToastNotification, Windows.UI.Notifications, ContentType = WindowsRuntime] | Out-Null
[Windows.Data.Xml.Dom.XmlDocument, Windows.Data.Xml.Dom.XmlDocument, ContentType = WindowsRuntime] | Out-Null

$APP_ID = '{1AC14E77-02E7-4E5D-B744-2EB1AE5198B7}\WindowsPowerShell\v1.0\powershell.exe'

$template = @"
<toast>
    <visual>
        <binding template="ToastText02">
            <text id="1">$Title</text>
            <text id="2">$msgText</text>
        </binding>
    </visual>
</toast>
"@

$xml = New-Object Windows.Data.Xml.Dom.XmlDocument
$xml.LoadXml($template)
$toast = New-Object Windows.UI.Notifications.ToastNotification $xml
[Windows.UI.Notifications.ToastNotificationManager]::CreateToastNotifier($APP_ID).Show($toast)
```

### <a name="detect_expired_user_certificatesps1"></a>Detect_Expired_User_Certificates.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Detect_Expired_User_Certificates.ps1
# Description:     Detect expired certificates issued by "CN=<your CA here>" to User
# Notes:           Change the value of the variable $certCN from "CN=<your CA here>" to "CN=...".
#                  Don't change $results
#
#=============================================================================================================================

# Define Variables
$results = 0
$certCN = "CN=<your CA here>"

try
{   
    $results = Get-ChildItem -Path Cert:\CurrentUser\My -Recurse -ExpiringInDays 0 | where {$_.Issuer -eq($certCN)}
    if (($results -ne $null)){
        #Below necessary for Intune as of 10/2019 will only remediate Exit Code 1
        Write-Host "Match"
        Return $results.count
        exit 1
    }
    else{
        Write-Host "No_Match"
        exit 0
    }    
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="remediate_expired_user_certificatesps1"></a>Remediate_Expired_User_Certificates.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Remediate_Expired_User_Certificates.ps1
# Description:     Remove expired certificates issued by "CN=<your CA here>" to User
# Notes:           Change the value of the variable $certCN from "CN=<your CA here>" to "CN=..."
#
#=============================================================================================================================

# Define Variables
$certCN = "CN=<your CA here>"

try
{
    Get-ChildItem -Path cert:\CurrentUser -Recurse -ExpiringInDays 0 | where {$_.Issuer -eq($certCN)} | Remove-Item
    exit 0
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

## <a name="endpoint-analytics-data-privacy"></a><a name="bkmk_uea_privacy"></a> Privacy dei dati di Analisi degli endpoint

### <a name="data-flow"></a>Flusso di dati

La figura seguente illustra il flusso dei dati funzionali richiesti dai singoli dispositivi attraverso i servizi dati e l'archiviazione temporanea fino al tenant. I dati passano attraverso le pipeline aziendali esistenti senza affidarsi ai dati di diagnostica di Windows.

[![Diagramma del flusso di dati dell'esperienza utente](media/dataflow.png)](media/dataflow.png#lightbox)

1. Configurare i criteri di **raccolta dati di Intune** per i dispositivi registrati. Per impostazione predefinita, questi criteri vengono assegnati a "Tutti i dispositivi" quando si **avvia** Analisi degli endpoint. Tuttavia, è possibile [modificare l'assegnazione](#bkmk_uea_set) in qualsiasi momento per un subset di dispositivi o nessun dispositivo.

2. I dispositivi inviano i dati funzionali richiesti.

    - Per i dispositivi Intune con i criteri assegnati, i dati vengono inviati dall'estensione di gestione di Intune. Per altre informazioni, vedere [Requisiti](#bkmk_uea_prereq).
    - Per i dispositivi gestiti da Configuration Manager, i dati possono essere propagati a Microsoft Endpoint Management anche attraverso il connettore ConfigMgr. Il connettore ConfigMgr è collegato al cloud. Richiede solo la connessione a un tenant di Intune, non l'attivazione della co-gestione.

> [!Note]  
> I dati necessari per calcolare il punteggio di avvio per un dispositivo vengono generati in fase di avvio. A seconda delle impostazioni di risparmio energia e del comportamento dell'utente, potrebbero trascorrere settimane dopo l'assegnazione corretta dei criteri a un dispositivo prima che venga visualizzato il punteggio di avvio nella console di amministrazione.  

3. Il servizio di gestione degli endpoint Microsoft elabora i dati per ogni dispositivo e pubblica i risultati per i singoli dispositivi e per le aggregazioni organizzative nella console di amministrazione usando le API di MS Graph.

La latenza media end-to-end è di circa 12 ore ed è vincolata dal tempo necessario per l'elaborazione giornaliera. Tutte le altre parti del flusso di dati sono quasi in tempo reale.

### <a name="data-collection"></a><a name="bkmk_uea_datacollection"></a>Raccolta dati

Attualmente, la funzionalità di base di Analisi degli endpoint raccoglie le informazioni associate ai record delle prestazioni di avvio appartenenti alle categorie [identified](https://docs.microsoft.com/mem/intune/protect/privacy-data-collect#identified-data) e [pseudonymized](https://docs.microsoft.com/mem/intune/protect/privacy-data-collect#pseudonymized-data). Con l'aggiunta di altre funzionalità nel tempo, i dati raccolti varieranno in base alle esigenze. I punti dati principali attualmente raccolti:

#### <a name="identified-data"></a>Dati identificati

- Informazioni sull'inventario hardware
  - **make:** produttore del dispositivo
  - **model:** modello del dispositivo
  - **deviceClass:** classificazione del dispositivo. Ad esempio, Desktop, Server o Mobile.
  - **Country:** impostazione dell'area del dispositivo
- Inventario delle applicazioni, ad esempio
  - **name:** Windows
  - **ver:** versione del sistema operativo corrente.
  
#### <a name="pseudonymized-data"></a>Dati pseudonimizzati

- Dati di diagnostica, sulle prestazioni e sull'utilizzo associati a un utente e/o a un dispositivo
  - **logOnId**
  - **bootId:** ID di avvio del sistema
  - **coreBootTimeInMilliseconds:** tempo per l'avvio core
  - **totalBootTimeInMilliseconds:** tempo di avvio totale
  - **updateTimeInMilliseconds:** tempo per il completamento degli aggiornamenti del sistema operativo
  - **gpLogonDurationInMilliseconds**: tempo per l'elaborazione dei Criteri di gruppo
  - **desktopShownDurationInMilliseconds:** tempo per il caricamento del desktop (explorer.exe)
  - **desktopUsableDurationInMilliseconds:** tempo per rendere utilizzabile il desktop (explorer.exe)
  - **topProcesses:** elenco dei processi caricati durante l'avvio con il nome, con le statistiche di utilizzo della CPU e i dettagli dell'app (nome, editore, versione). Ad esempio *{\"ProcessName\":\"svchost\",\"CpuUsage\":43,\"ProcessFullPath\":\"C:\\\\Windows\\\\System32\\\\svchost.exe\",\"ProductName\":\"Microsoft&reg; Windows&reg; Operating System\",\"Publisher\":\"Microsoft Corporation\",\"ProductVersion\":\"10.0.18362.1\"}*
- I dati dei dispositivi non associati a un dispositivo o utente (se questi dati sono associati a un dispositivo o un utente, Intune li considera dati identificati)
  - **ID:** ID dispositivo univoco usato da Windows Update
  - **localId:** ID univoco definito localmente per il dispositivo. Questo non è il nome del dispositivo leggibile. Probabilmente uguale al valore archiviato in HKLM\Software\Microsoft\SQMClient\MachineId.
  - **aaddeviceid:** ID dispositivo di Azure Active Directory
  - **orgId:** GUID univoco che rappresenta il tenant di Microsoft O365
  
> [!Important]  
> I criteri di gestione dei dati sono descritti nell'[informativa sulla privacy di Microsoft Intune](https://docs.microsoft.com/legal/intune/microsoft-intune-privacy-statement). I dati dei clienti vengono usati solo per fornire i servizi per i quali si è iscritti. Come descritto durante il processo di onboarding, i punteggi da tutte le organizzazioni registrate vengono anonimizzati e aggregati per mantenere aggiornate le baseline.


### <a name="resources"></a>Risorse

Per altre informazioni sugli aspetti correlati alla privacy, vedere gli articoli seguenti:

- [Informativa sulla privacy di Windows Intune](https://docs.microsoft.com/legal/intune/microsoft-intune-privacy-statement)
- [Windows 10 e conformità in materia di privacy](https://docs.microsoft.com/windows/privacy/windows-10-and-privacy-compliance)
- [Condizioni di licenza e documentazione](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31)  
- [Sicurezza e privacy nei data center di Microsoft Azure](https://azure.microsoft.com/global-infrastructure/)  
- [Fidati del tuo cloud](https://azure.microsoft.com/overview/trusted-cloud/)  
- [Centro protezione](https://www.microsoft.com/trustcenter)  
