---
title: Novità della versione 1906
titleSuffix: Configuration Manager
description: Informazioni dettagliate sulle modifiche e sulle nuove funzionalità introdotte nella versione 1906 di Configuration Manager Current Branch.
ms.date: 10/01/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 97e23075-549c-4e45-ab1e-0671027edacf
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d28d3ed697097b177ef9e2849fbcd6003505594c
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/09/2020
ms.locfileid: "89607796"
---
# <a name="whats-new-in-version-1906-of-configuration-manager-current-branch"></a>Novità della versione 1906 di Configuration Manager Current Branch

*Si applica a: Configuration Manager (Current Branch)*

L'aggiornamento 1906 per Configuration Manager Current Branch è disponibile come aggiornamento nella console. Applicare questo aggiornamento ai siti con la versione 1802 o versioni successive. <!-- baseline only statement:When installing a new site, it's also available as a baseline version.--> Questo articolo offre un riepilogo delle modifiche e delle nuove funzionalità di Configuration Manager versione 1906.  

Esaminare sempre l'elenco di controllo più recente per installare questo aggiornamento. Per altre informazioni, vedere [Elenco di controllo per l'installazione dell'aggiornamento 1906](../../servers/manage/checklist-for-installing-update-1906.md). Dopo aver aggiornato un sito, vedere anche [Elenco di controllo post-aggiornamento](../../servers/manage/checklist-for-installing-update-1906.md#post-update-checklist).

Per sfruttare i vantaggi delle nuove funzionalità di Configuration Manager, dopo l'aggiornamento del sito aggiornare anche i client alla versione più recente. Anche se le nuove funzionalità vengono visualizzate nella console di Configuration Manager quando si esegue l'aggiornamento del sito e della console, lo scenario completo risulta funzionante solo dopo l'aggiornamento alla versione più recente del client.

> [!Tip]  
> Per ricevere una notifica quando questa pagina viene aggiornata, copiare e incollare l'URL seguente nel lettore di feed RSS: `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1906+-+Configuration+Manager%22&locale=en-us`


## <a name="requirement-changes"></a>Modifiche ai requisiti

### <a name="version-1906-client-requires-sha-2-code-signing-support"></a>Il client versione 1906 richiede il supporto della firma del codice SHA-2

<!--SCCMDocs-pr#3404-->
A causa dei punti di debolezza dell'algoritmo SHA-1 e per allinearsi agli standard del settore, Microsoft ora firma i file binari di Configuration Manager solo usando l'algoritmo SHA-2, più sicuro. Per le versioni seguenti del sistema operativo Windows è necessario un aggiornamento per il supporto della firma del codice SHA-2:

- Windows 7 SP1
- Windows Server 2008 R2 SP1
- Windows Server 2008 SP2

Per altre informazioni, vedere [Prerequisiti per i client Windows](../../clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md#bkmk_sha2).


## <a name="site-infrastructure"></a><a name="bkmk_infra"></a> Infrastruttura del sito

### <a name="site-server-maintenance-task-improvements"></a>Miglioramenti alle attività di manutenzione del server del sito

<!--3555894-->
Le attività di manutenzione del server del sito possono ora essere visualizzate e modificate dalla scheda corrispondente nella visualizzazione dettagli di un server del sito. La nuova scheda **Maintenance Tasks** (Attività di manutenzione) offre le informazioni seguenti:

- Abilitazione dell'attività
- Pianificazione dell'attività
- Ultima ora di inizio
- Ora dell'ultimo completamento
- Completamento dell'attività

![Nuova scheda per le attività di manutenzione nella visualizzazione dettagli di un server del sito](./media/3555894-maintenance-tasks.png)

Per ulteriori informazioni, vedere [Attività di manutenzione](../../servers/manage/maintenance-tasks.md#bkmk_MTs1906).

### <a name="configuration-manager-update-database-upgrade-monitoring"></a>Monitoraggio dell'aggiornamento del database di Configuration Manager

<!--4200581-->
Durante l'applicazione di un aggiornamento di Configuration Manager, è ora possibile visualizzare lo stato dell'attività **Aggiorna database di ConfigMgr** nella finestra dello stato dell'installazione.

- Se l'aggiornamento del database è bloccato, viene visualizzato l'avviso **In corso, Richiesta attenzione**.
   - cmupdate.log registrerà il nome del programma e l'ID sessione SQL che blocca l'aggiornamento del database.
- Quando l'aggiornamento del database non sarà più bloccato, lo stato verrà reimpostato su **In corso** o **Completato**.
   - Quando l'aggiornamento del database è bloccato, viene effettuato un controllo ogni 5 minuti per verificare se è ancora bloccato.

   ![Monitoraggio dell'aggiornamento del database durante l'installazione](./media/4200581-database-upgrade-monitoring.png)

Per altre informazioni, vedere [Installare gli aggiornamenti nella console](../../servers/manage/install-in-console-updates.md#3-monitor-the-progress-of-updates-as-they-install).

### <a name="management-insights-rule-for-ntlm-fallback"></a>Regola delle informazioni dettagliate sulla gestione per il fallback di NTLM

<!--4572953-->
Le informazioni dettagliate sulla gestione includono una nuova regola che rileva se per il sito è stato abilitato il metodo di fallback dell'autenticazione NTLM, meno sicuro: **Fallback NTLM abilitato**.

Per altre informazioni, vedere [Informazioni dettagliate sulla gestione](../../servers/manage/management-insights.md#security).

### <a name="improvements-to-support-for-sql-always-on"></a>Miglioramenti al supporto per SQL Always On

- Aggiunta di un nuovo membro di replica sincrona dalla configurazione<!--3127336-->: è ora possibile aggiungere un nuovo nodo di replica secondaria a un gruppo di disponibilità SQL Always On esistente. Invece di un processo manuale, usare la configurazione di Configuration Manager per apportare questa modifica. Per altre informazioni, vedere [Configurare gruppi di disponibilità AlwaysOn di SQL Server](../../servers/deploy/configure/configure-aoag.md#bkmk_sync).

- Failover su più subnet<!-- SCCMDocs-pr#3734 -->: è ora possibile abilitare la [parola chiave della stringa di connessione MultiSubnetFailover](/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server#MultiSubnetFailover) in SQL Server. È anche necessario configurare manualmente il server del sito. Per altre informazioni, vedere il prerequisito relativo al [failover su più subnet](../../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#multi-subnet-failover).

- Supporto per le viste distribuite<!-- SCCMDocs-pr#3792 -->: Il database del sito può essere ospitato in un gruppo di disponibilità Always On di SQL Server ed è possibile abilitare i collegamenti della replica di database per l'uso di [viste distribuite](../hierarchy/data-transfers-between-sites.md#bkmk_dbrep).

    > [!Note]  
    > Questa modifica non si applica ai cluster SQL Server.

- Site Recovery può ricreare il database in un gruppo SQL Always On. Questo processo funziona con il seeding sia manuale che automatico.<!-- SCCMDocs-pr#3846 -->

- Nuovi controlli dei prerequisiti:<!-- SCCMDocs-pr#3899 -->  

    - Tutte le repliche dei gruppi di disponibilità SQL devono avere la stessa modalità seeding
    - Le repliche dei gruppi di disponibilità di SQL devono essere integre

## <a name="cloud-attached-management"></a><a name="bkmk_cloud"></a> Gestione collegata al cloud

### <a name="azure-active-directory-user-group-discovery"></a>Individuazione dei gruppi utenti in Azure Active Directory

<!--3611956-->

È ora possibile individuare i gruppi utenti e i membri dei gruppi in Azure Active Directory (Azure AD). Gli utenti trovati nei gruppi di Azure AD che non sono stati individuati in precedenza dal sito vengono aggiunti come risorse utente in Configuration Manager. Quando il gruppo è un gruppo di sicurezza viene creato un record di risorsa gruppo utenti. Si tratta di una [funzionalità di versione non definitiva](../../servers/manage/pre-release-features.md) e deve essere abilitata.

Per altre informazioni, vedere [Configurare i metodi di individuazione](../../servers/deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco).

### <a name="synchronize-collection-membership-results-to-azure-active-directory-groups"></a>Sincronizzare i risultati di appartenenza alla raccolta con i gruppi di Azure Active Directory

<!--3607475-->

È ora possibile abilitare la sincronizzazione delle appartenenze alle raccolte con un gruppo di Azure Active Directory (Azure AD). Questa sincronizzazione è una funzionalità di versione non definitiva. Per abilitarla, vedere [Funzionalità di versioni non definitive in System Center Configuration Manager](../../servers/manage/pre-release-features.md).

La sincronizzazione consente di usare le regole di raggruppamento locali esistenti nel cloud creando appartenenze ai gruppi di Azure AD in base ai risultati delle appartenenze alle raccolte. Solo i dispositivi con un record Azure Active Directory vengono riportati nel gruppo di Azure AD. Sono supportati sia i dispositivi aggiunti ad Azure AD ibrido che quelli aggiunti ad Azure Active Directory.

Per altre informazioni, vedere [Creare raccolte](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync).


## <a name="desktop-analytics"></a><a name="bkmk_da"></a> Desktop Analytics

### <a name="readiness-insights-for-desktop-apps"></a>Informazioni dettagliate sull'idoneità per le app desktop

<!-- 4021225 -->

È ora possibile ottenere informazioni più dettagliate per le applicazioni desktop, incluse le applicazioni line-of-business. Il toolkit App Health Analyzer precedente è ora integrato con il client di Configuration Manager. Questa integrazione semplifica la distribuzione e la gestione delle informazioni dettagliate sull'idoneità delle app nel portale di Desktop Analytics.

Per altre informazioni, vedere [Valutazione della compatibilità in Desktop Analytics](../../../desktop-analytics/compat-assessment.md#advanced-insights).


### <a name="dalogscollector-tool"></a>Strumento DALogsCollector

<!--4622989-->
Usare lo strumento DesktopAnalyticsLogsCollector.ps1 dalla directory di installazione di Configuration Manager per facilitare la risoluzione dei problemi di Desktop Analytics. Lo strumento esegue alcuni passaggi di base per la risoluzione dei problemi e raccoglie i log di rilievo in un'unica directory di lavoro.

Per altre informazioni, vedere [Agente di raccolta dei log](../../../desktop-analytics/log-collector.md).


## <a name="real-time-management"></a><a name="bkmk_real"></a> Gestione in tempo reale

### <a name="add-joins-additional-operators-and-aggregators-in-cmpivot"></a>Aggiungere join, operatori aggiuntivi e aggregatori in CMPivot

<!--4054074-->

Per CMPivot sono ora disponibili operatori aritmetici aggiuntivi, aggregatori e la possibilità di aggiungere join di query, ad esempio l'uso congiunto di Registry e File.

Per altre informazioni, vedere [CMPivot](../../servers/manage/cmpivot-changes.md#bkmk_cmpivot1906).

### <a name="cmpivot-standalone"></a>Modalità autonoma per CMPivot

<!--3555890, 4619340, 4692885 -->

È ora possibile usare CMPivot come app autonoma. La versione autonoma di CMPivot è una **funzionalità di versione non definitiva** ed è disponibile solo in inglese. Eseguire CMPivot all'esterno della console di Configuration Manager per visualizzare in tempo reale lo stato dei dispositivi presenti nell'ambiente. Questa modifica consente di usare CMPivot in un dispositivo senza aver prima installato la console.

È possibile condividere le funzionalità di CMPivot con altri utenti tipo, ad esempio operatori di help desk o amministratori della sicurezza, che non hanno la console installata nel proprio computer. Queste altre persone possono usare CMPivot per eseguire query su Configuration Manager insieme agli altri strumenti che usano solitamente. Condividendo questi dati di gestione completi, è possibile collaborare per risolvere proattivamente i problemi aziendali che riguardano più ruoli.

Per altre informazioni, vedere [CMPivot](../../servers/manage/cmpivot.md#bkmk_standalone) e [Funzionalità di versioni non definitive](../../servers/manage/pre-release-features.md#bkmk_table).

### <a name="added-permissions-to-the-security-administrator-role"></a>Autorizzazioni aggiunte al ruolo Amministratore della protezione

<!--4683130-->

Al ruolo [**Amministratore della protezione**](../../understand/fundamentals-of-role-based-administration.md#bkmk_Planroles) predefinito di Configuration Manager sono state aggiunte le autorizzazioni seguenti:

- Read on SMS Script (Lettura per script SMS)
- Run CMPivot on Collection (Esecuzione di CMPivot su raccolta)
- Read on Inventory Report (Lettura su report inventario)

Per altre informazioni, vedere [CMPivot](../../servers/manage/cmpivot-changes.md#bkmk_cmpivot_secadmin1906).


## <a name="content-management"></a><a name="bkmk_content"></a> Gestione dei contenuti

### <a name="delivery-optimization-download-data-in-client-data-sources-dashboard"></a>Dati di download di Ottimizzazione recapito nel dashboard Origini dati del client

<!--3555759-->
Il dashboard Origini dati del client ora include i dati di [Ottimizzazione recapito](../hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization). Il dashboard consente di comprendere da dove ricevono il contenuto i client nell'ambiente.

Per altre informazioni, vedere [Dashboard Origini dati del client](../../servers/deploy/configure/monitor-content-you-have-distributed.md#client-data-sources-dashboard).

### <a name="use-your-distribution-point-as-an-in-network-cache-server-for-delivery-optimization"></a>Usa il punto di distribuzione come server di cache in rete per Ottimizzazione recapito

<!--3555764-->
È ora possibile installare il server di cache in rete di Ottimizzazione recapito nei punti di distribuzione. Memorizzando nella cache questo contenuto in locale, i client possono trarre vantaggio dalla funzionalità di Ottimizzazione recapito, tuttavia è possibile contribuire a proteggere i collegamenti WAN.

Questo server di cache agisce come una cache trasparente su richiesta per il contenuto scaricato da Ottimizzazione recapito. Usare le impostazioni client per assicurarsi che il server sia disponibile soltanto ai membri del gruppo di limiti di Configuration Manager locale.

Per altre informazioni, vedere [Cache in rete di Ottimizzazione recapito in Configuration Manager](../hierarchy/microsoft-connected-cache.md).


## <a name="client-management"></a><a name="bkmk_client"></a> Gestione dei client

### <a name="support-for-windows-virtual-desktop"></a>Supporto per Desktop virtuale Windows

<!--3556025-->
[Desktop virtuale Windows](/azure/virtual-desktop/) è una funzionalità di anteprima di Microsoft Azure e Microsoft 365. È ora possibile usare Configuration Manager per gestire questi dispositivi virtuali che eseguono Windows in Azure.

Analogamente a un server terminal, questi dispositivi virtuali consentono l'esecuzione di più sessioni utente attive simultanee. Per migliorare le prestazioni dei client, Configuration Manager disabilita ora i criteri utente su tutti i dispositivi che consentono l'esecuzione di più sessioni utente. Anche se si abilitano i criteri utente, il client li disabilita per impostazione predefinita in questi dispositivi che includono Desktop virtuale Windows e i server terminal.

Per altre informazioni, vedere [Versioni dei sistemi operativi supportate per client e dispositivi](../configs/supported-operating-systems-for-clients-and-devices.md#windows-computers).

### <a name="support-center-onetrace-preview"></a>Supporto tecnico OneTrace (anteprima)

<!--3555962-->
OneTrace è un nuovo visualizzatore log con Support Center. Funziona in modo analogo a CMTrace, con i miglioramenti seguenti:

- Una visualizzazione a schede
- Finestre ancorabili
- Funzionalità di ricerca migliorate
- Possibilità di abilitare i filtri senza uscire dalla visualizzazione del log
- Hint della barra di scorrimento per identificare rapidamente i cluster di errori
- Apertura veloce del log per i file di grandi dimensioni

![Screenshot del visualizzatore log OneTrace](./media/3555962-onetrace.png)

Per altre informazioni, vedere [Supporto tecnico OneTrace](../../support/support-center-onetrace.md).

### <a name="configure-client-cache-minimum-retention-period"></a>Configurare il periodo di conservazione minimo della cache del client

<!--4485509-->
È ora possibile specificare il tempo minimo che il client di Configuration Manager ha per mantenere il contenuto memorizzato nella cache. Questa impostazione client definisce la quantità minima di tempo che l'agente di Configuration Manager deve attendere prima di poter rimuovere il contenuto dalla cache se è necessario più spazio. Nel gruppo **Impostazioni della cache del client** delle impostazioni del client configurare l'impostazione seguente: **Minimum duration before cached content can be removed (minutes)** (Durata minima prima che il contenuto nella cache possa essere rimosso (minuti)).

> [!Note]  
> Nello stesso gruppo delle impostazioni del client l'impostazione esistente **Abilita il client di Configuration Manager nell'intero sistema operativo per condividere i contenuti** è stata rinominata in **Enable as peer cache source** (Abilita come origine di peer cache). Il comportamento dell'impostazione è il medesimo.  

Per altre informazioni vedere [Impostazioni della cache dei client](../../clients/deploy/about-client-settings.md#client-cache-settings).


## <a name="co-management"></a><a name="bkmk_comgmt"></a> Co-gestione

### <a name="improvements-to-co-management-auto-enrollment"></a>Miglioramenti alla registrazione automatica di co-gestione

- Un nuovo dispositivo co-gestito viene ora registrato automaticamente nel servizio Microsoft Intune in base al token di *dispositivo* di Azure Active Directory (Azure AD). Non è necessario attendere che un utente esegua l'accesso al dispositivo per avviare la registrazione automatica. Questa modifica consente di ridurre il numero di dispositivi con lo [stato di registrazione](../../../comanage/how-to-monitor.md#co-management-enrollment-status) *Accesso utente in sospeso*.<!-- 4454491 -->

- Per i clienti che hanno già dispositivi registrati nella co-gestione, i nuovi dispositivi vengono ora registrati non appena soddisfano i prerequisiti, ad esempio non appena il dispositivo è stato aggiunto ad Azure AD e il client di Configuration Manager è stato installato.<!--4321130-->

Per altre informazioni, vedere [Abilitare la co-gestione](../../../comanage/how-to-enable.md).

### <a name="multiple-pilot-groups-for-co-management-workloads"></a>Più gruppi pilota per i carichi di lavoro con co-gestione

<!--3555750-->
È ora possibile configurare raccolte pilota diverse per ognuno dei carichi di lavoro con co-gestione. L'uso di raccolte pilota diverse consente di adottare un approccio più granulare durante il trasferimento dei carichi di lavoro.

- Nella scheda **Enablement** (Abilitazione) è ora possibile specificare una raccolta **Intune Auto Enrollment** (Registrazione automatica Intune).
    - La raccolta **Intune Auto Enrollment** (Registrazione automatica Intune) deve contenere tutti i client di cui si vuole eseguire l'onboarding nella co-gestione. Si tratta essenzialmente di un soprainsieme di tutte le altre raccolte di gestione temporanea.

- Nella scheda **Gestione temporanea** anziché usare un'unica raccolta pilota per tutti i carichi di lavoro, è ora possibile scegliere una singola raccolta per ogni carico di lavoro.

    ![La scheda Gestione temporanea per la co-gestione consente di scegliere una raccolta per ogni carico di lavoro](./media/3555750-co-management-staging-tab.png)

Queste opzioni sono disponibili anche quando si abilita la co-gestione per la prima volta.

Per altre informazioni, vedere [Abilitare la co-gestione](../../../comanage/how-to-enable.md).

### <a name="co-management-support-for-government-cloud"></a>Supporto della co-gestione per il cloud per enti pubblici

<!--4075452-->
I clienti costituiti da enti pubblici degli Stati Uniti possono ora usare la co-gestione con il cloud di Azure per enti pubblici degli Stati Uniti (portal.azure.us). Per altre informazioni, vedere [Abilitare la co-gestione](../../../comanage/how-to-enable.md).


## <a name="application-management"></a><a name="bkmk_app"></a> Gestione delle applicazioni

### <a name="filter-applications-deployed-to-devices"></a>Filtrare le applicazioni distribuite nei dispositivi

<!--4451056-->
Le categorie utente per le distribuzioni di applicazioni destinate a dispositivi vengono ora visualizzate come filtri in Software Center. Specificare una **categoria utente** per un'applicazione nella pagina **Software Center** delle proprietà. Quindi aprire l'app in Software Center ed esaminare i filtri disponibili.

Per altre informazioni, vedere [Specificare manualmente le informazioni sull'applicazione](../../../apps/deploy-use/create-applications.md#bkmk_manual-app).

### <a name="application-groups"></a>Gruppi di applicazioni

<!--3555907-->
Creare un gruppo di applicazioni che è possibile inviare a un utente o a una raccolta di dispositivi come singola distribuzione. I metadati specificati in relazione al gruppo di app sono visualizzati in Software Center come una singola entità. È possibile ordinare le app del gruppo in modo che il client le installi in un ordine specifico.

Si tratta di una funzionalità di versione non definitiva. Per abilitarla, vedere [Funzionalità di versioni non definitive in System Center Configuration Manager](../../servers/manage/pre-release-features.md).

Per altre informazioni, vedere [Creare gruppi di applicazioni](../../../apps/deploy-use/create-app-groups.md).

### <a name="retry-the-install-of-pre-approved-applications"></a>Ripetere l'installazione delle applicazioni pre-approvate

<!--4336307-->
È ora possibile ritentare l'installazione di un'app che è stata precedentemente approvata per un utente o un dispositivo. L'opzione di approvazione è destinata solo alle distribuzioni disponibili. Se l'utente disinstalla l'app o se il processo di installazione iniziale non riesce, Configuration Manager non rivaluta lo stato dell'app e la reinstalla. Questa funzionalità consente a un tecnico del supporto di ritentare rapidamente l'installazione dell'app per un utente che richiede assistenza.

Per altre informazioni, vedere [Approvare le applicazioni](../../../apps/deploy-use/app-approval.md).

### <a name="install-an-application-for-a-device"></a>Installare un'applicazione per un dispositivo

<!--4402180-->
Nella console di Configuration Manager è ora possibile installare le applicazioni per un dispositivo in tempo reale. Questa funzionalità consente di ridurre la necessità di raccolte separate per ogni applicazione.

Per altre informazioni, vedere [Installare applicazioni per un dispositivo](../../../apps/deploy-use/install-app-for-device.md).

### <a name="improvements-to-app-approvals"></a>Miglioramenti delle approvazioni di app

<!--4224910-->
Questa versione include i miglioramenti seguenti alle approvazioni delle app:

- Se si approva una richiesta di app nella console e poi la si rifiuta, ora è possibile approvarla nuovamente. L'app viene reinstallata nel client dopo l'approvazione.  

- Nell'area di lavoro **Raccolta software** della console di Configuration Manager, in **Gestione applicazioni**, il nodo **Richieste di approvazione** è stato rinominato in **Richieste applicazione**.<!-- SCCMDocs-pr#4028 -->

- Esiste un nuovo metodo WMI, **DeleteInstance**, per rimuovere una richiesta di approvazione di app. Questa azione non disinstalla l'app nel dispositivo. Se non è già installata, l'utente non può installare l'app da Software Center.

- Chiamare l'API **CreateApprovedRequest** per creare una richiesta preapprovata per un'app in un dispositivo. Per impedire l'installazione automatica dell'app nel client, impostare il parametro **AutoInstall** su `FALSE`. L'utente visualizza l'app in Software Center, ma non viene automaticamente installata.

Per altre informazioni, vedere [Approvare le applicazioni](../../../apps/deploy-use/app-approval.md).


## <a name="os-deployment"></a><a name="bkmk_osd"></a> Distribuzione del sistema operativo

### <a name="task-sequence-debugger"></a>Debugger di sequenze di attività

<!--3612274-->
Il debugger di sequenze di attività è un nuovo strumento per la risoluzione dei problemi. Si distribuisce una sequenza di attività in modalità di debug a una raccolta di un dispositivo. Consente di esaminare la sequenza di attività in modo controllato per facilitare la risoluzione dei problemi e l'analisi.

![Screenshot del debugger di sequenze di attività](./media/3612274-tsdebug.png)

Si tratta di una funzionalità di versione non definitiva. Per abilitarla, vedere [Funzionalità di versioni non definitive in System Center Configuration Manager](../../servers/manage/pre-release-features.md).

Per altre informazioni, vedere [Eseguire il debug di una sequenza di attività](../../../osd/deploy-use/debug-task-sequence.md).

### <a name="clear-app-content-from-client-cache-during-task-sequence"></a>Cancellare il contenuto dell'app dalla cache del client durante la sequenza di attività

<!--4485675-->
Nel passaggio **Installa applicazione** della sequenza di attività è ora possibile eliminare il contenuto dell'app dalla cache del client dopo l'esecuzione del passaggio stesso.

Per altre informazioni, vedere [Passaggi della sequenza di attività](../../../osd/understand/task-sequence-steps.md#BKMK_InstallApplication).

> [!Important]  
> Aggiornare il client di destinazione con la versione più recente per supportare questa nuova funzionalità.

### <a name="reclaim-sedo-lock-for-task-sequences"></a>Riscatta il blocco SEDO per le sequenze di attività

<!--3699337-->
Se la console di Configuration Manager non risponde, può essere bloccata la possibilità di apportare ulteriori modifiche a una sequenza di attività. Quando si tenta di accedere a una sequenza di attività bloccata, è ora possibile **rimuovere le modifiche** e continuare a modificare l'oggetto.

Per altre informazioni, vedere [Usare l'editor delle sequenze di attività](../../../osd/understand/task-sequence-editor.md#bkmk_sedo).

### <a name="pre-cache-driver-packages-and-os-images"></a>Pre-cache per pacchetti di driver e immagini del sistema operativo

<!--4224642-->
La pre-cache della sequenza di attività include ora tipi di contenuto aggiuntivi. La pre-cache del contenuto in precedenza si applicava solo ai pacchetti di aggiornamento del sistema operativo. È ora possibile usarla per ridurre il consumo di larghezza di banda di:

- Immagini dei sistemi operativi
- Pacchetti driver
- Pacchetti

Per altre informazioni, vedere [Configurare la pre-cache del contenuto](../../../osd/deploy-use/configure-precache-content.md).

### <a name="improvements-to-os-deployment"></a>Miglioramenti della distribuzione del sistema operativo

Questa versione include i miglioramenti seguenti alla distribuzione del sistema operativo:

- Usare i due cmdlet di PowerShell seguenti per creare e modificare il passaggio [Esegui la sequenza di attività](../../../osd/understand/task-sequence-steps.md#child-task-sequence):<!--2839943-->

    - **New-CMTSStepRunTaskSequence**

    - **Set-CMTSStepRunTaskSequence**

- È ora più semplice modificare le variabili quando si esegue una sequenza di attività. Dopo la selezione di una sequenza di attività nella finestra Creazione guidata sequenza di attività, la pagina per la modifica delle variabili della sequenza di attività include un pulsante **Modifica**.<!-- 4668846 --> Per altre informazioni, vedere [How to use task sequence variables](../../../osd/understand/using-task-sequence-variables.md#bkmk_set-tswiz) (Come usare le variabili della sequenza di attività).

- Il passaggio della sequenza di attività **Disattiva BitLocker** ha un nuovo contatore di riavvii. Usare questa opzione per specificare il numero di riavvii per mantenere BitLocker disabilitato. Questa modifica consente di semplificare la sequenza di attività. È possibile usare un unico passaggio anziché aggiungere più istanze di questo. <!--4512937--> Per altre informazioni, vedere [Disabilitare BitLocker](../../../osd/understand/task-sequence-steps.md#BKMK_DisableBitLocker).

- Usare la nuova variabile della sequenza di attività **SMSTSRebootDelayNext** con la variabile [SMSTSRebootDelay](../../../osd/understand/task-sequence-variables.md#SMSTSRebootDelay) esistente. Se si vuole che i riavvii successivi si verifichino con un timeout diverso rispetto al primo, impostare questa nuova variabile su un valore diverso in secondi. <!--4447680--> Per altre informazioni, vedere [SMSTSRebootDelayNext](../../../osd/understand/task-sequence-variables.md#SMSTSRebootDelayNext).

- La sequenza di attività imposta una nuova variabile di sola lettura, **_SMSTSLastContentDownloadLocation**. Questa variabile contiene l'ultimo percorso in cui la sequenza di attività ha scaricato o provato a scaricare contenuto. Esaminare questa variabile anziché analizzare i log del client.<!-- 2840337 -->

- Quando si crea un supporto per sequenza di attività, Configuration Manager non aggiunge un file autorun.inf. Questo file è generalmente bloccato da prodotti antimalware. È ancora possibile includere il file se necessario per lo scenario.<!-- 4090666 -->

### <a name="improvements-to-pxe"></a>Miglioramenti a PXE

L'opzione 82 durante l'handshake DHCP PXE è ora supportata con il risponditore PXE senza WDS. L'opzione 82 non è supportata con WDS.


## <a name="software-center"></a><a name="bkmk_userxp"></a> Software Center

### <a name="improvements-to-software-center-tab-customizations"></a>Miglioramenti delle personalizzazioni delle schede di Software Center

<!--4063773-->
È ora possibile aggiungere fino a cinque schede personalizzate in Software Center. È anche possibile modificare l'ordine in cui queste schede vengono visualizzate in Software Center.

Per altre informazioni, vedere [Impostazioni client di Software Center](../../clients/deploy/about-client-settings.md#software-center).

### <a name="software-center-infrastructure-improvements"></a>Miglioramenti all'infrastruttura di Software Center

<!--3555950-->

Questa versione include i seguenti miglioramenti apportati all'infrastruttura di Software Center:

- Software Center comunica ora con un punto di gestione per le app destinate agli utenti, se disponibili. Non usa più il catalogo applicazioni. Grazie a questa modifica, è più facile rimuovere il catalogo applicazioni dal sito.

- In precedenza, Software Center selezionava il primo punto di gestione nell'elenco di server disponibili. A partire da questa versione, usa lo stesso punto di gestione del client. Questa modifica consente a Software Center di usare lo stesso punto di gestione del client dal sito primario assegnato.

> [!Important]  
> Questi miglioramenti iterativi di Software Center e il punto di gestione sono concepiti per il ritiro dei ruoli del catalogo applicazioni.
>
> - L'esperienza utente di Silverlight non è supportata a partire dalla versione Current Branch 1806.
> - A partire dalla versione 1906, i client aggiornati usano automaticamente il punto di gestione per le distribuzioni di applicazioni disponibili per gli utenti. Non è inoltre possibile installare nuovi ruoli del Catalogo applicazioni.
> - Il supporto per i ruoli del Catalogo applicazioni termina con la versione 1910.  

Per altre informazioni, vedere [Rimuovere il catalogo applicazioni](../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat) e [Pianificare per Software Center](../../../apps/plan-design/plan-for-software-center.md).

### <a name="redesigned-notification-for-newly-available-software"></a>Notifica riprogettata per il nuovo software disponibile

<!--3555904-->
La notifica **È disponibile nuovo software** verrà visualizzata una sola volta per ogni utente per una determinata applicazione e revisione. L'utente non visualizzerà più la notifica a ogni accesso, ma visualizzerà un'altra notifica solo se l'applicazione è stata modificata o ridistribuita.

Per altre informazioni, vedere [Create and deploy an application](../../../apps/get-started/create-and-deploy-an-application.md#end-user-experience) (Creare e distribuire un'applicazione).

### <a name="more-frequent-countdown-notifications-for-restarts"></a>Notifiche del conto alla rovescia più frequenti per i riavvii

<!--3976435-->

Gli utenti finali ora riceveranno un promemoria più frequentemente per un riavvio in sospeso tramite notifiche intermittenti del conto alla rovescia. È possibile definire l'intervallo per le notifiche intermittenti in **Impostazioni client** nella pagina **Riavvio del computer**. Modificare il valore di **Specificare la durata del rinvio per le notifiche con conto alla rovescia per il riavvio del computer (minuti)** per configurare la frequenza con cui un utente riceve il promemoria di un riavvio in sospeso fino a quando non si verifica la notifica finale del conto alla rovescia.

In più, il valore massimo di **Visualizzare una notifica temporanea in cui viene indicato l'intervallo di disconnessione dell'utente o di riavvio del computer (minuti)** è stato aumentato da 1440 minuti (24 ore) a 20160 minuti (due settimane).

Per altre informazioni, vedere [Notifiche di riavvio dispositivo](../../clients/deploy/device-restart-notifications.md) e [Informazioni sulle impostazioni client](../../clients/deploy/about-client-settings.md#computer-restart).

### <a name="direct-link-to-custom-tabs-in-software-center"></a>Collegamento diretto a schede personalizzate in Software Center

<!--4655176-->

È ora possibile offrire agli utenti un collegamento diretto a una [scheda personalizzata](../../clients/deploy/about-client-settings.md#software-center-tab-visibility) in Software Center.

Usare il formato URL seguente per aprire Software Center con una scheda specifica:

`softwarecenter:page=CustomTab1`

La stringa `CustomTab1` è la prima scheda personalizzata nell'ordine.

Ad esempio, digitare l'URL seguente nella finestra **Esegui** di Windows.

È anche possibile usare questa sintassi per aprire le schede predefinite in Software Center:

|Riga di comando  |Scheda  |
|---------|---------|
|`AvailableSoftware`|Applicazioni|
|`Updates`|Aggiornamenti|
|`OSD`|Sistemi operativi|
|`InstallationStatus`|Stato installazione|
|`Compliance`|Conformità del dispositivo|
|`Options`|Options|

Per altre informazioni, vedere [Visibilità delle schede di Software Center](../../clients/deploy/about-client-settings.md#software-center-tab-visibility).

## <a name="software-updates"></a><a name="bkmk_sum"></a> Aggiornamenti software

### <a name="additional-options-for-wsus-maintenance"></a>Opzioni aggiuntive per la manutenzione di WSUS

<!--4110109-->
Sono ora disponibili attività di manutenzione di WSUS aggiuntive che possono essere eseguite da Configuration Manager per mantenere l'integrità dei punti di aggiornamento software. La manutenzione di WSUS avviene dopo ogni sincronizzazione. Oltre a rifiutare gli aggiornamenti scaduti in WSUS, Configuration Manager ora può:

- Rimuovere gli aggiornamenti obsoleti dal database di WSUS.
- Aggiungere indici non cluster al database di WSUS per migliorare le prestazioni di pulizia di WSUS.

Per altre informazioni, vedere [Manutenzione degli aggiornamenti software](../../../sum/deploy-use/software-updates-maintenance.md#wsus-cleanup-starting-in-version-1906).

### <a name="configure-the-default-maximum-run-time-for-software-updates"></a>Configurare il tempo di esecuzione massimo predefinito per gli aggiornamenti software

<!--3734426-->

Ora è possibile specificare il tempo di esecuzione massimo per completare l'installazione di un aggiornamento software. È possibile specificare gli elementi seguenti nella scheda **Tempo di esecuzione massimo** nel punto di aggiornamento software:

- **Tempo di esecuzione massimo per gli aggiornamenti di funzionalità Windows (minuti)**
- **Tempo di esecuzione massimo per gli aggiornamenti di Office 365 e gli aggiornamenti non delle funzionalità per Windows (minuti)**

Per altre informazioni, vedere [Pianificare gli aggiornamenti software](../../../sum/plan-design/plan-for-software-updates.md#bkmk_maxruntime).

### <a name="configure-dynamic-update-during-feature-updates"></a>Configurare l'aggiornamento dinamico durante gli aggiornamenti delle funzionalità

<!--4062619-->

Usare una nuova impostazione client per configurare l'[aggiornamento dinamico](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/The-benefits-of-Windows-10-Dynamic-Update/ba-p/467847) durante l'installazione degli aggiornamenti delle funzionalità di Windows 10. L'aggiornamento dinamico installa i language pack, le funzionalità su richiesta, i driver e gli aggiornamenti cumulativi durante l'installazione di Windows indicando al client di scaricare questi aggiornamenti da Internet.

Per altre informazioni, vedere [Impostazioni client dell'aggiornamento software](../../clients/deploy/about-client-settings.md#software-updates) e [Gestire Windows come servizio](../../../osd/deploy-use/manage-windows-as-a-service.md).

### <a name="new-windows-10-version-1903-and-later-product-category"></a>Nuova categoria di prodotti per Windows 10 versione 1903 e successive

<!--4682946-->

**Windows 10 versione 1903 e successive** è stato aggiunto a Microsoft Update come prodotto a sé stante, anziché all'interno del prodotto **Windows 10** come le versioni precedenti. A causa di questa modifica è necessario eseguire una serie di passaggi manuali per assicurarsi che i client visualizzino questi aggiornamenti. Si è cercato di ridurre il numero di passaggi manuali che è necessario eseguire per il nuovo prodotto.

Quando si esegue l'aggiornamento a Configuration Manager versione 1906 e il prodotto **Windows 10** è selezionato per la sincronizzazione, vengono eseguite automaticamente le azioni seguenti:

- Il prodotto **Windows 10 versione 1903 e successive** viene aggiunto per la sincronizzazione.
- Le regole di distribuzione automatica che contengono il prodotto **Windows 10** vengono aggiornate in modo da includere **Windows 10 versione 1903 e successive**.
- I piani di manutenzione vengono aggiornati in modo da includere il prodotto **Windows 10 versione 1903 e successive**.

Per altre informazioni, vedere [Configurare le classificazioni e i prodotti per la sincronizzazione](../../../sum/get-started/configure-classifications-and-products.md), [Piani di manutenzione](../../../osd/deploy-use/manage-windows-as-a-service.md#servicing-plan-workflow) e [Regole di distribuzione automatica](../../../sum/deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process).

### <a name="drill-through-required-updates"></a>Drill-through degli aggiornamenti obbligatori

<!--4224414-->
È ora possibile esaminare nel dettaglio le statistiche di conformità per individuare i dispositivi che richiedono un aggiornamento software specifico. Per visualizzare l'elenco dei dispositivi, è necessaria l'autorizzazione per visualizzare gli aggiornamenti e le raccolte a cui appartengano i dispositivi. Per eseguire il drill-down nell'elenco dei dispositivi, selezionare il collegamento ipertestuale **Visualizza gli elementi necessari** accanto al grafico a torta nella scheda **Riepilogo** relativa a un aggiornamento. Se si fa clic sul collegamento ipertestuale, si passa a un nodo temporaneo in **Dispositivi** dove è possibile visualizzare i dispositivi che richiedono l'aggiornamento.

Il collegamento ipertestuale  **Visualizza gli elementi necessari** è disponibile nei percorsi seguenti:

   - **Raccolta software** > **Aggiornamenti software** > **Tutti gli aggiornamenti software**
   - **Raccolta software** > **Manutenzione pacchetti di Windows 10** > **Tutti gli aggiornamenti di Windows 10**
   - **Raccolta software** > **Gestione client di Office 365** > **Aggiornamenti di Office 365**

Per altre informazioni, vedere [Monitorare gli aggiornamenti software](../../../sum/deploy-use/monitor-software-updates.md#drill-through-required-updates), [Gestire Windows come servizio](../../../osd/deploy-use/manage-windows-as-a-service.md#drill-through-required-updates) e [Gestire gli aggiornamenti di App di Microsoft 365](../../../sum/deploy-use/manage-office-365-proplus-updates.md).


## <a name="office-management"></a><a name="bkmk_o365"></a> Gestione di Office

### <a name="office-365-proplus-upgrade-readiness-dashboard"></a>Dashboard Preparazione aggiornamenti per Office 365 ProPlus

<!--4021125-->

Per individuare i dispositivi pronti per l'aggiornamento a Microsoft 365 Apps for enterprise, è disponibile un nuovo dashboard di conformità. Include il riquadro **Preparazione aggiornamenti di Office 365 ProPlus** rilasciato in Configuration Manager Current Branch versione 1902. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**, espandere **Gestione client di Office 365** e selezionare il nodo **Preparazione aggiornamenti di Office 365 ProPlus**.

Per altre informazioni sul dashboard, sui prerequisiti e sull'uso di questi dati, vedere [Integrazione per l'idoneità per Office 365 ProPlus](../../../sum/deploy-use/office-365-dashboard.md#bkmk_readiness-dash).


## <a name="protection"></a><a name="bkmk_protect"></a> Protezione

### <a name="windows-defender-application-guard-file-trust-criteria"></a>Criteri di attendibilità file di Windows Defender Application Guard

<!--3555858-->

Una nuova impostazione dei criteri consente agli utenti di considerare attendibili i file che si aprono normalmente in Windows Defender Application Guard (WDAG). Dopo l'esecuzione con esito positivo, i file vengono aperti nel dispositivo host anziché in WDAG.

Per altre informazioni, vedere [Creare e distribuire criteri di Windows Defender Application Guard](../../../protect/deploy-use/create-deploy-application-guard-policy.md#bkmk_FM).


## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a> Console di Configuration Manager

### <a name="role-based-access-for-folders"></a>Accesso basato sui ruoli per le cartelle

<!--3600867-->

È ora possibile impostare ambiti di protezione per le cartelle. Se si ha accesso a un oggetto nella cartella ma non si ha accesso alla cartella, non sarà possibile visualizzare l'oggetto. Analogamente, se si ha accesso a una cartella ma non a un oggetto all'interno della cartella, non sarà possibile visualizzare l'oggetto. Fare clic con il pulsante destro del mouse su una cartella, scegliere **Imposta ambiti di protezione** e quindi scegliere gli ambiti di protezione da applicare.

Per altre informazioni, vedere [Suggerimenti sulla console di Configuration Manager ](../../servers/manage/admin-console-tips.md) e [Configurare l'amministrazione basata su ruoli](../../servers/deploy/configure/configure-role-based-administration.md#bkmk_config-folder).

### <a name="add-smbios-guid-column-to-device-and-device-collection-nodes"></a>Aggiungi la colonna GUID SMBIOS ai nodi Dispositivo e Raccolta di dispositivi

<!--4526580-->
Nei nodi **Dispositivi** e **Raccolte di dispositivi** è ora possibile aggiungere una nuova colonna per il **GUID SMBIOS**. Questo valore corrisponde alla proprietà **GUID BIOS** della classe Risorsa di sistema. Si tratta di un identificatore univoco dell'hardware del dispositivo.

### <a name="administration-service-support-for-security-nodes"></a>Supporto del servizio di amministrazione per i nodi di sicurezza

<!--4223683-->
È ora possibile abilitare alcuni nodi della console di Configuration Manager per l'uso del servizio di amministrazione. Questa modifica consente alla console di comunicare con il provider SMS tramite HTTPS anziché tramite WMI.

Per altre informazioni, vedere [Servizio di amministrazione](../hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service).

> [!Note]
> A partire dalla versione 1906, la scheda **Comunicazione computer client** nelle proprietà del sito viene chiamata **Communication Security** (Sicurezza della comunicazione).<!-- SCCMDocs#1645 -->  

### <a name="collections-tab-in-devices-node"></a>Scheda Raccolte nel nodo Dispositivi

<!--4616810-->
Nell'area di lavoro **Asset e conformità** passare al nodo **Dispositivi** e selezionare un dispositivo. Nel riquadro dei dettagli passare alla nuova scheda **Raccolte**. Questa scheda contiene le raccolte che includono questo dispositivo.

> [!Note]  
> - La scheda non è attualmente disponibile da un sottonodo dispositivi del nodo **Raccolte di dispositivi**. Ad esempio, quando si seleziona l'opzione che consente di **visualizzare i membri** per una raccolta.
> - Questa scheda potrebbe non essere popolata come previsto per alcuni utenti. Per visualizzare l'elenco completo delle raccolte a cui appartiene un dispositivo, è necessario avere il ruolo di sicurezza **Amministratore completo**. Si tratta di un problema noto. <!--5107309-->

### <a name="task-sequences-tab-in-applications-node"></a>Scheda Sequenze di attività nel nodo Applicazioni

<!--4616810-->
Nell'area di lavoro **Raccolta software** espandere **Gestione applicazioni**, passare al nodo **Applicazioni** e selezionare un'applicazione. Nel riquadro dei dettagli passare alla nuova scheda **Sequenze di attività**. Questa scheda contiene le sequenze di attività che fanno riferimento a questa applicazione.

### <a name="show-collection-name-for-scripts"></a>Visualizzare il nome della raccolta per gli script

<!--4616810-->
Nell'area di lavoro **Monitoraggio** selezionare il nodo **Stato script**, che ora indica il **nome della raccolta** oltre all'ID.

### <a name="real-time-actions-from-device-lists"></a>Azioni in tempo reale dagli elenchi di dispositivi

<!--4616810-->
Esistono diversi modi per visualizzare un elenco di dispositivi nel nodo **Dispositivi** dell'area di lavoro **Asset e conformità**.

- Nell'area di lavoro **Asset e conformità** selezionare il nodo **Raccolte dispositivi**. Selezionare una raccolta di dispositivi e scegliere l'azione che consente di **visualizzare i membri**. Questa azione apre un sottonodo del nodo **Dispositivi** con un elenco di dispositivi per la raccolta.  

  - Quando si seleziona il sottonodo della raccolta, è ora possibile avviare **CMPivot** dal gruppo Raccolta della barra multifunzione.  

- Nell'area di lavoro **Monitoraggio** selezionare il nodo **Distribuzioni**. Selezionare una distribuzione e scegliere l'azione di **visualizzazione dello stato** nella barra multifunzione. Nel riquadro dello stato della distribuzione fare doppio clic sugli asset totali per eseguire il drill-through in un elenco di dispositivi.  

  - Quando si seleziona un dispositivo in questo elenco, è ora possibile avviare **CMPivot** ed **eseguire script** dal gruppo Dispositivi della barra multifunzione.  

### <a name="order-by-program-name-in-task-sequence"></a>Ordinare in base al nome del programma nella sequenza di attività

<!--4616810-->
Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi** e selezionare il nodo **Sequenze di attività**. Modificare una sequenza di attività e selezionare o aggiungere il passaggio [Installa pacchetto](../../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage). Se un pacchetto include più di un programma, l'elenco a discesa ora visualizza i programmi in ordine alfabetico.

### <a name="correct-names-for-client-operations"></a>Nomi corretti per le operazioni client

<!--4616810-->
Nell'area di lavoro **Monitoraggio** espandere **Operazioni client**. L'operazione di **passaggio al punto di aggiornamento software successivo** è ora denominata in modo corretto.


## <a name="deprecated-features-and-operating-systems"></a><a name="bkmk_deprecated"></a> Funzionalità e sistemi operativi deprecati

Per conoscere le modifiche relative al supporto prima che siano implementate, vedere [Elementi rimossi e deprecati](deprecated/removed-and-deprecated.md).

Nella versione 1906 è stato eliminato il supporto delle funzionalità seguenti:  

- Non è possibile installare nuovi ruoli del Catalogo applicazioni. I client aggiornati usano automaticamente il punto di gestione per le distribuzioni di applicazioni disponibili per gli utenti. Per altre informazioni, vedere [Pianificare Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex).

Nella versione 1906 vengono impostati come deprecati i prodotti seguenti:  

- Windows CE 7.0
- Windows 10 Mobile
- Windows 10 Mobile Enterprise


## <a name="other-updates"></a>Altri aggiornamenti

A partire da questa versione, le funzionalità seguenti non sono più in versione non definitiva:

- [Servizio di amministrazione del provider SMS](../hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service)
- [Gestione di Controllo di applicazioni di Windows Defender](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md)

A parte le nuove funzionalità, questa versione include anche ulteriori modifiche, ad esempio correzioni di bug. Per altre informazioni, vedere [Riepilogo delle modifiche in Configuration Manager Current Branch, versione 1906](https://support.microsoft.com/help/4514258).

Per altre informazioni sulle modifiche apportate ai cmdlet di Windows PowerShell per Configuration Manager, vedere le [note sulla versione 1906 di PowerShell](/powershell/sccm/1906-release-notes).

L'aggiornamento cumulativo seguente (4517869) è disponibile nella console a partire dal 1° ottobre 2019: [Aggiornamento cumulativo per Configuration Manager Current Branch, versione 1906](https://support.microsoft.com/help/4517869).

<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune connector certificate does not renew in Configuration Manager | 18 January 2019 | Yes |

> [!Note]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](../../servers/manage/updates.md#bkmk_supersede).
-->


## <a name="next-steps"></a>Passaggi successivi

<!--At this time, version 1906 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-1906.md#early-update-ring). -->
A partire dal 16 agosto 2019, la versione 1906 è disponibile per l'installazione a livello globale da parte di tutti i clienti.

Al momento di installare questa versione, vedere [Installazione degli aggiornamenti per Configuration Manager](../../servers/manage/updates.md) ed [Elenco di controllo per l'installazione dell'aggiornamento 1906](../../servers/manage/checklist-for-installing-update-1906.md).

> [!TIP]  
> Per installare un nuovo sito, usare una versione base di Configuration Manager.  
>
> Sono disponibili altre informazioni su:
>
> - [Installing new sites](../../servers/deploy/install/installing-sites.md) (Installare nuovi siti)  
> - [Baseline and update versions](../../servers/manage/updates.md#bkmk_Baselines) (Versioni di base e di aggiornamento)  

Per problemi noti e importanti, vedere [Note sulla versione](../../servers/deploy/install/release-notes.md).

Dopo aver aggiornato un sito, vedere anche [Elenco di controllo post-aggiornamento](../../servers/manage/checklist-for-installing-update-1906.md#post-update-checklist).
