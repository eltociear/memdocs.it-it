---
title: Introduzione agli aggiornamenti software
titleSuffix: Configuration Manager
description: Informazioni di base sugli aggiornamenti software in Configuration Manager.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 10/30/2017
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: e9778b13-c8a3-40eb-8655-34ac8ce9cdaa
ms.openlocfilehash: 3cb8d07c9bcc31353e16f01de9e60857d47d49e4
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700423"
---
# <a name="introduction-to-software-updates-in-configuration-manager"></a>Introduzione agli aggiornamenti software in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Gli aggiornamenti software in Configuration Manager offrono un set di strumenti e risorse che consentono di gestire la complessa attività di monitoraggio e applicazione degli aggiornamenti software ai computer client dell'azienda. Un processo di gestione efficiente degli aggiornamenti software è necessario per mantenere l'efficienza operativa, risolvere i problemi di sicurezza e mantenere la stabilità dell'infrastruttura di rete. Tuttavia, a causa della natura mutevole della tecnologia e della continua comparsa di nuove minacce per la sicurezza, una gestione efficiente degli aggiornamenti software richiede un'attenzione costante e ininterrotta.  

Per uno scenario di esempio in cui viene illustrato come distribuire gli aggiornamenti software nell'ambiente, vedere [Example scenario to deploy security software updates](../deploy-use/example-scenario-deploy-monitor-monthly-security-updates.md) (Scenario di esempio per distribuire aggiornamenti di sicurezza del software).  

##  <a name="software-updates-synchronization"></a><a name="BKMK_Synchronization"></a> Sincronizzazione degli aggiornamenti software  
 La sincronizzazione degli aggiornamenti software in Configuration Manager avviene mediante la connessione a Microsoft Update per recuperare i metadati degli aggiornamenti software. Il sito di livello superiore, un sito di amministrazione centrale o un sito primario autonomo, vengono sincronizzati con Microsoft Update in base a una pianificazione o quando si avvia manualmente la sincronizzazione dalla console di Configuration Manager. Quando Configuration Manager termina la sincronizzazione degli aggiornamenti software nel sito di livello superiore, la sincronizzazione degli aggiornamenti software viene avviata nei siti figlio, se esistenti. Dopo che la sincronizzazione è stata completata in ogni sito primario o secondario, vengono creati criteri a livello di sito che forniscono ai computer client la posizione dei punti di aggiornamento software.  

> [!NOTE]  
>  Per impostazione predefinita, gli aggiornamenti software sono abilitati nelle impostazioni client. Se, tuttavia, si imposta l'impostazione client **Abilitare aggiornamento software nei client** su **No** per disabilitare gli aggiornamenti software in una raccolta o nelle impostazioni predefinite, la posizione dei punti di aggiornamento software non viene inviata ai client associati. Per altre informazioni, vedere le impostazioni del client per gli aggiornamenti software in [About client settings in System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md#software-updates) (Informazioni sulle impostazioni client in System Center Configuration Manager).  

 Dopo aver ricevuto i criteri, il client avvia un'analisi della conformità degli aggiornamenti software e scrive le informazioni in Strumentazione gestione Windows (WMI). Le informazioni sulla conformità vengono quindi inviate al punto di gestione che le invia infine al server del sito. Per altre informazioni sulla valutazione della conformità, vedere la sezione [Software updates compliance assessment](#BKMK_SUMCompliance) in questo argomento.  

 È possibile installare più punti di aggiornamento software in un sito primario. Il primo punto di aggiornamento software installato viene configurato come origine della sincronizzazione. Ciò consente la sincronizzazione da Microsoft Update o da un server WSUS non presente nella gerarchia di Configuration Manager. Gli altri punti di aggiornamento software nel sito usano il primo punto di aggiornamento software come origine della sincronizzazione.  

> [!NOTE]  
>  Al termine del processo di sincronizzazione degli aggiornamenti software nel sito di livello superiore, i metadati degli aggiornamenti software vengono replicati nei siti figlio usando la replica di database. Quando si connette una console di Configuration Manager al sito figlio, in Configuration Manager vengono visualizzati i metadati degli aggiornamenti software. Finché tuttavia non si installa e configura un punto di aggiornamento software nel sito, i client non analizzeranno la conformità degli aggiornamenti software né comunicheranno le informazioni sulla conformità a Configuration Manager e non sarà possibile distribuire correttamente gli aggiornamenti software.  

### <a name="synchronization-on-the-top-level-site"></a>Sincronizzazione nel sito principale  
 Il processo di sincronizzazione degli aggiornamenti software nel sito di livello superiore recupera da Microsoft Update i metadati degli aggiornamenti software che soddisfano i criteri specificati in Proprietà del componente del punto di aggiornamento software. È possibile configurare i criteri solo nel sito di livello superiore.  

> [!NOTE]  
>  Come origine della sincronizzazione è possibile specificare un server WSUS esistente non presente nella gerarchia di Configuration Manager, anziché Microsoft Update.  

 Nell'elenco seguente vengono descritti i passaggi fondamentali per il processo di sincronizzazione nel sito di livello superiore:  

1.  Viene avviata la sincronizzazione degli aggiornamenti software.  

2.  Gestione sincronizzazione WSUS invia a WSUS in esecuzione sul punto di aggiornamento software una richiesta di avvio della sincronizzazione con Microsoft Update.  

3.  I metadati degli aggiornamenti software vengono sincronizzati da Microsoft Update e le modifiche vengono inserite o aggiornate nel database WSUS.  

4.  Quando WSUS ha terminato la sincronizzazione, Gestione sincronizzazione WSUS sincronizza i metadati degli aggiornamenti software dal database WSUS al database di Configuration Manager e le modifiche successive all'ultima sincronizzazione vengono inserite o aggiornate nel database del sito. I metadati degli aggiornamenti software vengono archiviati nel database del sito come elemento di configurazione.  

5.  Gli elementi di configurazione degli aggiornamenti software vengono inviati ai siti figli usando la replica di database.  

6.  Al termine della sincronizzazione, Gestione sincronizzazione WSUS crea il messaggio di stato 6702.  

7.  Gestione sincronizzazione WSUS invia una richiesta di sincronizzazione a tutti i siti figlio.  

8.  Gestione sincronizzazione WSUS invia una richiesta alla volta per WSUS in esecuzione su altri punti di aggiornamento software nel sito. I server WSUS negli altri punti di aggiornamento software vengono configurati come repliche di WSUS in esecuzione sul punto di aggiornamento software predefinito nel sito.  

### <a name="synchronization-on-child-primary-and-secondary-sites"></a>Sincronizzazione in siti figlio primari e secondari  
 Durante il processo di sincronizzazione degli aggiornamenti software nel sito di livello superiore, gli elementi di configurazione degli aggiornamenti software vengono replicati nei siti figlio usando la replica di database. Al termine del processo, il sito di livello superiore invia una richiesta di sincronizzazione al sito figlio e il sito figlio avvia la sincronizzazione WSUS. L'elenco seguente include i passaggi fondamentali per il processo di sincronizzazione in un sito primario figlio o in un sito secondario:  

1.  Gestione sincronizzazione WSUS riceve una richiesta di sincronizzazione dal sito di livello superiore.  

2.  Viene avviata la sincronizzazione degli aggiornamenti software.  

3.  Gestione sincronizzazione WSUS effettua una richiesta di avvio della sincronizzazione a WSUS in esecuzione sul punto di aggiornamento software.  

4.  WSUS in esecuzione sul punto di aggiornamento software nel sito figlio sincronizza i metadati degli aggiornamenti software da WSUS in esecuzione sul punto di aggiornamento software nel sito padre.  

5.  Al termine della sincronizzazione, Gestione sincronizzazione WSUS crea il messaggio di stato 6702.  

6.  Da un sito primario Gestione sincronizzazione WSUS invia una richiesta di sincronizzazione ai siti secondari figlio. Il sito secondario avvia la sincronizzazione degli aggiornamenti software con il sito primario padre. Il sito secondario viene configurato come replica di WSUS in esecuzione sul sito padre.  

7.  Gestione sincronizzazione WSUS invia una richiesta alla volta per WSUS in esecuzione su altri punti di aggiornamento software nel sito. I server WSUS negli altri punti di aggiornamento software vengono configurati come repliche di WSUS in esecuzione sul punto di aggiornamento software predefinito nel sito.  

##  <a name="software-updates-compliance-assessment"></a><a name="BKMK_SUMCompliance"></a> Software updates compliance assessment  
 Prima di distribuire gli aggiornamenti software nei computer client in Configuration Manager, avviare un'analisi della conformità degli aggiornamenti software nei computer client. Per ogni aggiornamento software, viene creato un messaggio di stato contenente lo stato di conformità per l'aggiornamento. I messaggi di stato vengono inviati in blocco al punto di gestione e quindi al server del sito, dove lo stato di conformità viene inserito nel database del sito. Lo stato di conformità per gli aggiornamenti software viene visualizzato nella console di Configuration Manager. È possibile distribuire e installare gli aggiornamenti software nei computer che richiedono gli aggiornamenti. Nelle sezioni seguenti vengono fornite informazioni sugli stati di conformità e viene descritto il processo di analisi della conformità degli aggiornamenti software.  

### <a name="software-updates-compliance-states"></a>Stati di conformità degli aggiornamenti software  
 Di seguito viene elencato e descritto ogni stato di conformità visualizzato nella console di Configuration Manager per gli aggiornamenti software.  

-   **Richiesto**  

     Specifica che l'aggiornamento software è applicabile e richiesto nel computer client. Una delle seguenti condizioni può essere vera quando lo stato dell'aggiornamento software è **Richiesto**:  

    -   L'aggiornamento software non è stato distribuito nel computer client.  

    -   L'aggiornamento software è stato installato nel computer client. Tuttavia, il messaggio di stato più recente non è stato ancora inserito nel database sul server del sito. Il computer client analizza nuovamente l'aggiornamento dopo l'installazione. Potrebbero trascorrere fino a due minuti prima che il client invii lo stato aggiornato al punto di gestione che quindi inoltra lo stato aggiornato al server del sito.  

    -   L'aggiornamento software è stato installato nel computer client. Tuttavia, l'installazione dell'aggiornamento software richiede un riavvio del computer prima che venga completato l'aggiornamento.  

    -   L'aggiornamento software è stato distribuito nel computer client, ma non è ancora stato installato.  

-   **Non richiesto**  

     Specifica che l'aggiornamento software non è applicabile nel computer client. Pertanto, l'aggiornamento software non è richiesto.  

-   **Installato**  

     Specifica che l'aggiornamento software è applicabile nel computer client e che è già installato nel computer client.  

-   **Sconosciuto**  

     Specifica che il server del sito non ha ricevuto un messaggio di stato dal computer client, in genere per uno dei motivi seguenti:  

    -   La conformità degli aggiornamenti software non è stata analizzata correttamente nel computer client.  

    -   L'analisi è stata completata nel computer client. Tuttavia, il messaggio di stato non è ancora stato elaborato sul server del sito, probabilmente a causa di un backlog del messaggio di stato.  

    -   L'analisi è stata completata nel computer client, ma il messaggio di stato non è stato ricevuto dal sito figlio.  

    -   L'analisi è stata completata nel computer client, ma il file del messaggio di stato è stato danneggiato e non può essere elaborato.  

### <a name="scan-for-software-updates-compliance-process"></a>Analisi del processo di conformità degli aggiornamenti software  
 Quando il punto di aggiornamento software viene installato e sincronizzato, vengono creati criteri del computer a livello di sito che informano i computer client che gli aggiornamenti software di Configuration Manager sono stati abilitati per il sito. Quando un client riceve i criteri del computer, viene programmata un'analisi di valutazione della conformità con avvio casuale entro due ore. Quando l'analisi viene avviata, un processo di Agente client aggiornamenti software cancella la cronologia dell'analisi, invia una richiesta per trovare il server WSUS da usare per l'analisi e aggiorna i Criteri di gruppo locali con il percorso del server WSUS.  

> [!NOTE]  
>  I client basati su Internet devono connettersi al server WSUS usando SSL.  

 Una richiesta di analisi viene passata all'agente di Windows Update (WUA). L'agente WUA si connette quindi al percorso del server WSUS elencato nei criteri locali, recupera i metadati degli aggiornamenti software sincronizzati nel server WSUS e analizza il computer client alla ricerca di aggiornamenti. Un processo di Agente client aggiornamenti software rileva che la verifica della conformità è stata completata e crea messaggi di stato per ciascun aggiornamento software il cui stato di conformità è stato modificato dall'ultima analisi. I messaggi di stato vengono inviati in blocco al punto di gestione ogni 15 minuti. Il punto di gestione inoltra quindi i messaggi di stato al server del sito, dove vengono inseriti all'interno del relativo database.  

 Dopo l'analisi iniziale per la conformità degli aggiornamenti software, l'analisi viene avviata in base a una pianificazione configurata. Tuttavia, se il client ha analizzato la conformità degli aggiornamenti software nell'intervallo di tempo indicato dal valore Durata (TTL), utilizzerà i metadati degli aggiornamenti software memorizzati in locale. Quando l'ultima analisi non rientra nell'intervallo TTL, il client deve connettersi a WSUS in esecuzione sul punto di aggiornamento software e aggiornare i metadati degli aggiornamenti software nel client.  

 L'analisi per la conformità degli aggiornamenti software, inclusa la relativa pianificazione, può iniziare nei modi seguenti:  

-   **Pianificazione analisi aggiornamenti software**: l'analisi per la conformità degli aggiornamenti software inizia in base alla pianificazione configurata nelle impostazioni di Agente client aggiornamenti software. Per altre informazioni sulla configurazione delle impostazioni client degli aggiornamenti software, vedere le impostazioni client degli aggiornamenti software in [About client settings in System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md#software-updates) (Informazioni sulle impostazioni client in System Center Configuration Manager).  

-   **Azione Proprietà di Configuration Manager**: l'utente può avviare l'azione **Ciclo di analisi per aggiornamenti software** o **Ciclo di valutazione distribuzione aggiornamenti software** nella scheda **Azione** della finestra di dialogo **Proprietà di Configuration Manager** nel computer client.  

-   **Pianificazione della rivalutazione della distribuzione**: la valutazione della distribuzione e l'analisi per la conformità degli aggiornamenti software iniziano in base alla pianificazione della rivalutazione della distribuzione configurata nelle impostazioni di Agente client aggiornamenti software. Per altre informazioni sulla configurazione delle impostazioni client degli aggiornamenti software, vedere le impostazioni client degli aggiornamenti software in [About client settings in System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md#software-updates) (Informazioni sulle impostazioni client in System Center Configuration Manager).  

-   **Prima di scaricare i file di aggiornamento**: quando un computer client riceve un criterio di assegnazione per una nuova distribuzione richiesta, l'Agente client aggiornamenti software scarica i file di aggiornamento software nella cache del client locale. Prima di scaricare i file di aggiornamento software, l'agente client avvia un'analisi per verificare che l'aggiornamento software sia ancora necessario.  

-   **Prima dell'installazione dell'aggiornamento software**: prima dell'installazione dell'aggiornamento software, l'Agente client aggiornamenti software avvia un'analisi per verificare che gli aggiornamenti software siano ancora necessari.  

-   **Dopo l'installazione dell'aggiornamento software**: dopo il completamento dell'installazione dell'aggiornamento software, l'Agente client aggiornamenti software avvia un'analisi per verificare che gli aggiornamenti software non siano più necessari e crea un nuovo messaggio di stato che indica che l'aggiornamento software è installato. Quando l'installazione è terminata, ma è necessario un riavvio, il messaggio di stato indica che il computer client è in attesa di un riavvio.  

-   **Dopo il riavvio del sistema**: quando un computer client è in attesa di un riavvio del sistema per completare l'installazione dell'aggiornamento software, l'Agente client aggiornamenti software avvia un'analisi dopo il riavvio per verificare che l'aggiornamento software non sia più richiesto e crea un messaggio di stato che indica che l'aggiornamento software è installato.  

#### <a name="time-to-live-value"></a>Valore di durata  
 I metadati degli aggiornamenti software richiesti per l'analisi della conformità degli aggiornamenti software vengono memorizzati nel computer client locale e, per impostazione predefinita, sono rilevanti per un massimo di 24 ore. Questo valore è noto come Durata (TTL).  

#### <a name="scan-for-software-updates-compliance-types"></a>Analisi dei tipi di conformità degli aggiornamenti software  
 I client analizzano la conformità degli aggiornamenti software usando un'analisi online o offline e un'analisi forzata o non forzata, in base al modo in cui l'analisi per la conformità degli aggiornamenti software viene avviata. Di seguito vengono descritti i metodi di avvio dell'analisi online e offline e viene specificato se l'analisi è forzata o non forzata.  

-   **Pianificazione analisi aggiornamento software** (analisi online non forzata)  

     Nella pianificazione analisi configurata, il client si connette a WSUS in esecuzione sul punto di aggiornamento software per recuperare i metadati degli aggiornamenti software solo quando l'ultima analisi non rientra nell'intervallo TTL.  

-   **Ciclo di analisi per aggiornamenti software** o **Ciclo di valutazione distribuzione aggiornamenti software** (analisi online forzata)  

     Il computer client si connette sempre a WSUS in esecuzione sul punto di aggiornamento software per recuperare i metadati degli aggiornamenti software prima che il computer client analizzi la conformità degli aggiornamenti software. Al termine dell'analisi, il contatore TTL viene reimpostato. Ad esempio, se il valore TTL è 24 ore, dopo che un utente avvia un'analisi per la conformità degli aggiornamenti software, tale valore viene reimpostato su 24 ore.  

-   **Pianificazione della rivalutazione della distribuzione** (analisi online non forzata)  

     Nella pianificazione della rivalutazione della distribuzione configurata, il client si connette a WSUS in esecuzione sul punto di aggiornamento software per recuperare i metadati degli aggiornamenti software solo quando l'ultima analisi non rientra nell'intervallo TTL.  

-   **Prima di scaricare i file di aggiornamento** (analisi online non forzata)  

     Prima che il client possa scaricare i file di aggiornamento nelle distribuzioni richieste, si connette a WSUS in esecuzione sul punto di aggiornamento software per recuperare i metadati degli aggiornamenti software solo quando l'ultima analisi non rientra nell'intervallo TTL.  

-   **Prima dell'installazione dell'aggiornamento software** (analisi online non forzata)  

     Prima che il client installi gli aggiornamenti software nelle distribuzioni richieste, si connette a WSUS in esecuzione sul punto di aggiornamento software per recuperare i metadati degli aggiornamenti software solo quando l'ultima analisi non rientra nell'intervallo TTL.  

-   **Dopo l'installazione dell'aggiornamento software** (analisi offline forzata)  

     Dopo aver installato un aggiornamento software, l'Agente client aggiornamenti software avvia un'analisi usando i metadati locali. Il client non si connette mai a WSUS in esecuzione sul punto di aggiornamento software per recuperare i metadati degli aggiornamenti software.  

-   **Dopo il riavvio del sistema** (analisi offline forzata)  

     Dopo aver installato un aggiornamento software e riavviato il computer, l'Agente client aggiornamenti software avvia un'analisi usando i metadati locali. Il client non si connette mai a WSUS in esecuzione sul punto di aggiornamento software per recuperare i metadati degli aggiornamenti software.  

##  <a name="software-update-deployment-packages"></a><a name="BKMK_DeploymentPackages"></a> Pacchetti di distribuzione degli aggiornamenti software  
 Un pacchetto di distribuzione degli aggiornamenti software rappresenta il mezzo usato per scaricare tali aggiornamenti in una cartella di rete condivisa nonché copiare i file di origine aggiornamento software nella raccolta contenuto nei server del sito e nei punti di distribuzione definiti nella distribuzione. Usando il Download guidato degli aggiornamenti, è possibile scaricare gli aggiornamenti software e aggiungerli ai pacchetti di distribuzione prima di distribuirli. La procedura guidata consente di effettuare il provisioning degli aggiornamenti software nei punti di distribuzione e di verificare che questa parte del processo di distribuzione sia eseguita correttamente prima di distribuire gli aggiornamenti software nei client.  

 Quando vengono distribuiti gli aggiornamenti software scaricati tramite la Distribuzione guidata degli aggiornamenti software, la distribuzione usa automaticamente il pacchetto di distribuzione contenente gli aggiornamenti software. Quando vengono distribuiti aggiornamenti software che non sono stati scaricati, è necessario specificare un pacchetto di distribuzione nuovo o esistente nella Distribuzione guidata degli aggiornamenti software e gli aggiornamenti software vengono scaricati al termine della procedura.  

> [!IMPORTANT]  
>  È necessario creare manualmente la cartella di rete condivisa per i file di origine del pacchetto di distribuzione prima di specificarla nella procedura guidata. Ogni pacchetto di distribuzione deve usare una cartella di rete condivisa diversa.  

> [!IMPORTANT]  
>  L'account computer del provider SMS e l'utente amministratore che scarica effettivamente gli aggiornamenti software richiedono entrambi le autorizzazioni di **Scrittura** nell'origine del pacchetto. Limitare l'accesso all'origine del pacchetto consente di ridurre il rischio di manomissioni da parte di utenti malintenzionati dei file di origine degli aggiornamenti software nell'origine del pacchetto.  

 Quando viene creato un nuovo pacchetto di distribuzione, la versione del contenuto è impostata su 1 prima che venga scaricato qualsiasi aggiornamento software. Quando i file di aggiornamento software vengono scaricati usando il pacchetto, la versione del contenuto viene aumentata a 2. Pertanto, tutti i nuovi pacchetti di distribuzione iniziano con una versione del contenuto pari a 2. Ogni volta che il contenuto viene modificato in un pacchetto di distribuzione, la versione del contenuto viene incrementata di 1. Per altre informazioni su BranchCache, vedere [Fundamental concepts for content management](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md) (Concetti di base per la gestione dei contenuti).  

 I client installano gli aggiornamenti software in una distribuzione tramite un punto di distribuzione con aggiornamenti software disponibili, indipendentemente dal pacchetto di distribuzione. Anche se un pacchetto di distribuzione viene eliminato per una distribuzione attiva, i client sono ancora in grado di installare gli aggiornamenti software nella distribuzione finché ciascun aggiornamento non è stato scaricato in almeno un altro pacchetto di distribuzione ed è disponibile in un punto di distribuzione accessibile dal client. Quando l'ultimo pacchetto di distribuzione contenente un aggiornamento software viene eliminato, i computer client non sono in grado di recuperare l'aggiornamento software finché non viene scaricato nuovamente in un pacchetto di distribuzione. Gli aggiornamenti software vengono visualizzati con una freccia rossa nella console di Configuration Manager quando i file di aggiornamento non si trovano in alcun pacchetto di distribuzione. Le distribuzioni vengono visualizzate con una doppia freccia rossa se contengono aggiornamenti in questa condizione.  

##  <a name="software-update-deployment-workflows"></a><a name="BKMK_DeploymentWorkflows"></a> Flussi di lavoro di distribuzione degli aggiornamenti software  
 Esistono due scenari principali per la distribuzione di aggiornamenti software nell'ambiente, la distribuzione manuale e la distribuzione automatica. In genere, si effettuerà la distribuzione manuale degli aggiornamenti software per creare una linea di base per i computer client, quindi si gestiranno gli aggiornamenti software nei client usando la distribuzione automatica. Le sezioni seguenti forniscono un riepilogo del flusso di lavoro per la distribuzione manuale e automatica degli aggiornamenti software.  

###  <a name="manual-deployment-of-software-updates"></a><a name="BKMK_ManualDeployment"></a> Distribuzione manuale degli aggiornamenti software  
 La distribuzione manuale degli aggiornamenti software consiste nel processo di selezione di aggiornamenti software nella console di Configuration Manager e di avvio manuale del processo di distribuzione. In genere si utilizzerà questo metodo di distribuzione per mantenere aggiornati i computer client con gli aggiornamenti software richiesti prima di creare regole di distribuzione automatica che gestiranno le distribuzioni degli aggiornamenti software in corso a cadenza mensile e per distribuire i requisiti di aggiornamento software fuori banda. Il seguente elenco descrive il flusso di lavoro generale per la distribuzione manuale degli aggiornamenti software:  

1.  Filtrare gli aggiornamenti software che usano requisiti specifici. Ad esempio, è possibile fornire criteri per il recupero di tutti gli aggiornamenti software critici o della sicurezza necessari su più di 50 computer client.  

2.  Creare un gruppo di aggiornamenti software che contenga gli aggiornamenti software.  

3.  Scaricare il contenuto per gli aggiornamenti software nel gruppo di aggiornamenti software.  

4.  Distribuire manualmente il gruppo di aggiornamenti software.  

###  <a name="automatic-deployment-of-software-updates"></a><a name="BKMK_AutomaticDeployment"></a> Distribuzione automatica degli aggiornamenti software  
 La distribuzione automatica degli aggiornamenti software viene configurata con una regola di distribuzione automatica. Questo metodo di distribuzione viene in genere usato per gli aggiornamenti software mensili (comunemente noti come Patch martedì) e per la gestione degli aggiornamenti delle definizioni. Quando si esegue la regola, gli aggiornamenti software vengono rimossi dal gruppo di aggiornamenti software (se si usa un gruppo esistente), gli aggiornamenti software che soddisfano un criterio specificato (ad esempio, tutti gli aggiornamenti software della sicurezza rilasciati la settimana precedente) vengono aggiunti a un gruppo di aggiornamenti software, i file di contenuto per gli aggiornamenti software vengono scaricati e copiati nei punti di distribuzione e gli aggiornamenti software vengono distribuiti nei computer client nella raccolta di destinazione. Il seguente elenco descrive il flusso di lavoro generale per la distribuzione automatica degli aggiornamenti software:  

1. Creare una regola di distribuzione automatica che specifica le impostazioni di distribuzione, tra cui:  

   -   Raccolta di destinazione  

   -   Decidere se abilitare la distribuzione o il report sulla conformità degli aggiornamenti software per i computer client nella raccolta di destinazione  

   -   Criteri degli aggiornamenti software  

   -   Pianificazioni di valutazione e distribuzione  

   -   Esperienza utente  

   -   Proprietà di download  

2. Gli aggiornamenti software vengono aggiunti a un gruppo di aggiornamenti software.  

3. Il gruppo di aggiornamenti software viene distribuito ai computer client nella raccolta di destinazione, se specificato.  

   È necessario determinare la strategia di distribuzione da usare nel proprio ambiente. Ad esempio, è possibile creare la regola di distribuzione automatica e trovare una raccolta di destinazione dei client di prova. Dopo aver verificato che gli aggiornamenti software siano installati nel gruppo di prova, è possibile aggiungere una nuova distribuzione alla regola o modificare la raccolta nella distribuzione esistente in una raccolta di destinazione che include un set di client più ampio. Gli oggetti di aggiornamento software creati dalle regole di distribuzione automatica sono interattivi.  

- Gli aggiornamenti software distribuiti usando una regola di distribuzione automatica vengono distribuiti automaticamente nei nuovi client aggiunti alla raccolta di destinazione.  

- I nuovi aggiornamenti software aggiunti a un gruppo di aggiornamenti software vengono distribuiti automaticamente ai client nella raccolta di destinazione.  

- È possibile abilitare o disabilitare le distribuzioni in qualsiasi momento per la regola di distribuzione automatica.  

  Dopo aver creato una regola di distribuzione automatica, è possibile aggiungere altre distribuzioni alla regola. Ciò consente di gestire la complessità della distribuzione di aggiornamenti diversi a raccolte differenti. Ogni nuova distribuzione include l'intera gamma dell'esperienza di monitoraggio di funzionalità e distribuzione. Ogni nuova distribuzione aggiunta:  

- Utilizza lo stesso gruppo e lo stesso pacchetto di aggiornamento creato alla prima esecuzione di ADR  

- Può specificare una raccolta diversa  

- Supporta proprietà di distribuzione univoca tra cui:  

  -   Ora attivazione  

  -   Scadenza  

  -   Mostra o nascondi l'esperienza dell'utente finale  

  -   Avvisi separati per questa distribuzione  

##  <a name="software-update-deployment-process"></a><a name="BKMK_DeploymentProcess"></a> Processo di distribuzione degli aggiornamenti software  
 Dopo aver distribuito gli aggiornamenti software oppure quando viene eseguita una regola di distribuzione automatica e vengono distribuiti gli aggiornamenti software, viene aggiunto un criterio di assegnazione distribuzione ai criteri del computer per il sito. Gli aggiornamenti software vengono scaricati dal percorso download, Internet o dalla cartella di rete condivisa nell'origine del pacchetto. Gli aggiornamenti software vengono copiati dall'origine del pacchetto nella raccolta contenuto nel server del sito, quindi nella raccolta contenuto nel punto di distribuzione.  

 Quando un computer client nella raccolta di destinazione per la distribuzione riceve dei criteri del computer, l'Agente client aggiornamenti software avvia un'analisi di valutazione. L'agente client scarica il contenuto per gli aggiornamenti software richiesti da un punto di distribuzione nella cache del client locale in base all'impostazione **Tempo disponibile software** per la distribuzione e quindi gli aggiornamenti software sono disponibili per l'installazione. Gli aggiornamenti software nelle distribuzioni facoltative (distribuzioni che non hanno una scadenza dell'installazione) non vengono scaricati fino a quando un utente non avvia manualmente l'installazione.  

 Una volta trascorsa la scadenza configurata, l'Agente client aggiornamenti software esegue un'analisi per verificare che gli aggiornamenti software siano ancora necessari. Quindi controlla la cache locale sul computer client per verificare che i file di origine degli aggiornamenti software siano ancora disponibili. Infine, il client installa gli aggiornamenti software. Se il contenuto è stato eliminato dalla cache client per far spazio a un'altra distribuzione, il client scarica nuovamente gli aggiornamenti software dal punto di distribuzione nella cache client. Gli aggiornamenti software vengono sempre scaricati nella cache del client, indipendentemente dalla dimensione massima della cache client configurata. Al termine dell'installazione, l'agente client verifica che gli aggiornamenti software non siano più necessari e invia un messaggio di stato al punto di gestione per indicare che gli aggiornamenti software sono ora installati sul client.  

### <a name="required-system-restart"></a>Riavvio del sistema richiesto  
 Per impostazione predefinita, viene avviato un riavvio del sistema se richiesto per il completamento dell'installazione di aggiornamenti software da una distribuzione richiesta in un computer client. Per gli aggiornamenti software installati prima della scadenza, il riavvio automatico del sistema viene posticipato fino a tale data, a meno che non si verifichi prima per qualche altro motivo. Il riavvio del sistema può essere inibito per server e workstation. Queste impostazioni sono configurate nella pagina **Esperienza utente** della Distribuzione guidata degli aggiornamenti software o Creazione guidata della regola degli aggiornamenti automatici.  

### <a name="deployment-reevaluation-cycle"></a>Ciclo di rivalutazione della distribuzione  
 Per impostazione predefinita, i computer client avviano un ciclo di rivalutazione della distribuzione ogni 7 giorni. Durante tale ciclo, il computer client analizza di aggiornamenti software precedentemente distribuiti e installati. Se degli aggiornamenti software risultano mancanti, vengono reinstallati dalla cache locale. Se un aggiornamento software non è più disponibile nella cache locale, viene scaricato da un punto di distribuzione e quindi installato. È possibile configurare la pianificazione di rivalutazione nella pagina **Aggiornamenti software** nelle impostazioni client per il sito.  

##  <a name="support-for-windows-embedded-devices-that-use-write-filters"></a><a name="BKMK_EmbeddedDevices"></a> Supporto per dispositivi con Windows Embedded che usano filtri di scrittura  
 Quando si distribuiscono aggiornamenti software a dispositivi con Windows Embedded abilitati ai filtri di scrittura, è possibile specificare se disabilitare il filtro sul dispositivo durante la distribuzione, riavviando il dispositivo al termine di tale operazione. Se il filtro di scrittura non è disabilitato, il software viene distribuito in una sovrapposizione temporanea e non sarà più installato al riavvio del dispositivo, a meno che un'altra distribuzione forzi le modifiche per renderle permanenti.  

> [!NOTE]  
>  Quando si distribuisce un aggiornamento software in un dispositivo con Windows Embedded, verificare che il dispositivo appartenga a una raccolta che dispone di una finestra di manutenzione configurata. Ciò consente di decidere quando abilitare o disabilitare il filtro di scrittura nonché quando riavviare il dispositivo.  

 L'impostazione dell'esperienza utente che consente di controllare il comportamento del filtro di scrittura è una casella di controllo denominata **Invia modifiche alla scadenza o in una finestra di manutenzione (riavvio necessario)** .  

 Per altre informazioni sul modo in cui Configuration Manager gestisce dispositivi Windows Embedded che usano filtri di scrittura, vedere [Planning for client deployment to Windows Embedded devices in System Center Configuration Manager](../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md) (Pianificazione della distribuzione di client in dispositivi Windows Embedded in System Center Configuration Manager).  

##  <a name="extend-software-updates-in-configuration-manager"></a><a name="BKMK_ExtendSoftwareUpdates"></a> Estendere gli aggiornamenti software in Configuration Manager  
 Usare System Center Updates Publisher per gestire gli aggiornamenti software che non sono disponibili da Microsoft Update. Dopo aver pubblicato gli aggiornamenti software nel server di aggiornamento e averli sincronizzati in Configuration Manager, è possibile distribuire gli aggiornamenti software nei client di Configuration Manager. Per altre informazioni su System Center Updates Publisher, vedere [Updates Publisher 2011](/previous-versions/system-center/updates-publisher-2011/hh134742(v=technet.10)).  

## <a name="next-steps"></a>Passaggi successivi
[Plan for software updates](../plan-design/plan-for-software-updates.md) (Pianificare gli aggiornamenti del software)