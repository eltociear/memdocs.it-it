---
title: Gestire le sequenze di attività
titleSuffix: Configuration Manager
description: Creare, modificare, distribuire, importare ed esportare sequenze di attività per gestirle e automatizzarle nel proprio ambiente.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: a1f099f1-e9b5-4189-88b3-f53e3b4e4add
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 609f5d010018fa23dd4a533b2f1079f07d8c2283
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125066"
---
# <a name="manage-task-sequences-to-automate-tasks"></a>Gestire le sequenze di attività per automatizzare le attività

*Si applica a: Configuration Manager (Current Branch)*

Usare le sequenze di attività per automatizzare i passaggi nell'ambiente di Configuration Manager. Questi passaggi consentono di distribuire un'immagine del sistema operativo in un computer di destinazione, di compilare e acquisire un'immagine del sistema operativo da un set di file di installazione del sistema operativo e di acquisire e ripristinare le informazioni sullo stato utente. Le sequenze di attività si trovano nella console di Configuration Manager. Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi** e selezionare **Sequenze di attività**. Il nodo **Sequenze di attività**, che include le sottocartelle create, viene replicato in tutta la gerarchia di Configuration Manager. Per informazioni sulla pianificazione, vedere [Considerazioni sulla pianificazione per l'automazione delle attività](../plan-design/planning-considerations-for-automating-tasks.md).  

## <a name="create"></a><a name="BKMK_CreateTaskSequence"></a> Creare

Creare sequenze attività usando la Creazione guidata della sequenza di attività. Questa procedura guidata consente di creare i seguenti tipi di sequenze attività:  

- [Sequenza di attività per installare un sistema operativo](create-a-task-sequence-to-install-an-operating-system.md): creare i passaggi per installare un sistema operativo. Include anche le opzioni per eseguire la migrazione dei dati utente, includere gli aggiornamenti software e installare le applicazioni.

- [Sequenza di attività per aggiornare un sistema operativo](create-a-task-sequence-to-upgrade-an-operating-system.md): creare i passaggi per aggiornare un sistema operativo. Include anche le opzioni per includere gli aggiornamenti software e installare le applicazioni.

- [Sequenza di attività per acquisire un sistema operativo](create-a-task-sequence-to-capture-an-operating-system.md): Crea i passaggi per compilare e acquisire un sistema operativo da un computer di riferimento. È possibile includere gli aggiornamenti software e installare le applicazioni nel computer di riferimento prima dell'acquisizione dell'immagine.

- [Sequenza di attività per acquisire e ripristinare lo stato utente](create-a-task-sequence-to-capture-and-restore-user-state.md): aggiungere i passaggi a una sequenza di attività esistente per acquisire e ripristinare i dati dello stato utente.

- [Sequenza di attività personalizzata](create-a-custom-task-sequence.md): Questo tipo non aggiunge alcun passaggio alla sequenza di attività. Dopo aver creato questa sequenza di attività, modificarla e aggiungere i passaggi.

## <a name="edit"></a><a name="BKMK_ModifyTaskSequence"></a> Modifica  

Modificare una sequenza di attività aggiungendo o rimuovendo passaggi, aggiungendo o rimuovendo gruppi oppure modificando l'ordine dei passaggi. Per altre informazioni, vedere [Usare l'editor delle sequenze di attività](../understand/task-sequence-editor.md).

## <a name="reduce-the-size-of-task-sequence-policy"></a><a name="bkmk_policysize"></a>Ridurre le dimensioni dei criteri delle sequenze di attività

<!--6982275-->
Quando le dimensioni dei criteri delle sequenze di attività superano 32 MB, il client non riesce a elaborare i criteri di grandi dimensioni. Il client non riesce quindi a eseguire la distribuzione della sequenza di attività.

La dimensione della sequenza di attività archiviate nel database del sito è minore, ma può comunque causare problemi se troppo grande. Quando il client elabora per intero i criteri di una sequenza di attività, dimensioni superiori a 32 MB possono determinare problemi.

A partire dal 2006 è possibile usare le [informazioni dettagliate sulla gestione](../../core/servers/manage/management-insights.md#operating-system-deployment) per controllare che le dimensioni dei criteri della sequenza di attività sui clienti non superino i 32 MB.

Per ridurre le dimensioni complessive dei criteri di distribuzione di una sequenza di attività, eseguire le azioni seguenti:

- Separare i segmenti funzionali in sequenze di attività figlio e usare il passaggio [Esegui la sequenza di attività](../understand/task-sequence-steps.md#child-task-sequence). Le dimensioni dei criteri di ogni sequenza di attività hanno un limite di 32 MB.

    > [!NOTE]
    > La riduzione del numero totale di passaggi e gruppi in una sequenza di attività ha un effetto minimo sulle dimensioni dei criteri. Ogni passaggio corrisponde a circa 2 KB nei criteri. Lo spostamento di gruppi di passaggi in una sequenza di attività figlio ha un impatto più consistente.

- Ridurre il numero di aggiornamenti software nelle distribuzioni alla stessa raccolta della sequenza di attività.

- Anziché immettere uno script nel passaggio [Esegui script PowerShell](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript), farvi riferimento tramite un pacchetto.

- È previsto un limite di 8 KB per le dimensioni dell'ambiente della sequenza di attività durante l'esecuzione. Rivedere l'utilizzo delle variabili della sequenza di attività personalizzate, che possono anch'esse contribuire alle dimensioni dei criteri.

- Come ultima risorsa, suddividere una sequenza di attività dinamica complessa in sequenze di attività separate con distribuzioni distinte in raccolte diverse.

## <a name="software-center-properties"></a><a name="bkmk_prop-general"></a> Proprietà di Software Center

Attenersi alla procedura seguente per configurare i dettagli per la sequenza di attività visualizzata in Software Center. Tali dettagli sono solo a scopo informativo.  

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**, espandere **Sistemi operativi** e selezionare **Sequenze di attività**.  

2. Selezionare la sequenza di attività da modificare e selezionare **Proprietà**.  

3. Nella scheda **Generale** sono disponibili le impostazioni seguenti per Software Center:  

    - **Riavvio necessario**: consente all'utente di sapere se è necessario un riavvio durante l'installazione.  

    - **Dimensioni del download (MB)** : specifica quanti megabyte vengono visualizzati in Software Center per la sequenza di attività.  

    - **Tempo di esecuzione stimato (minuti)** : specifica il tempo di esecuzione stimato in minuti che viene visualizzato in Software Center per la sequenza di attività.  

## <a name="advanced-settings"></a><a name="bkmk_prop-advanced"></a> Impostazioni avanzate

Usare la procedura seguente per configurare il comportamento della sequenza di attività nel client di Configuration Manager.  

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**, espandere **Sistemi operativi** e selezionare **Sequenze di attività**.  

2. Selezionare la sequenza di attività da modificare e selezionare **Proprietà**.  

3. Nella scheda **Avanzate** sono disponibili le impostazioni seguenti:  

    - **Esegui prima un altro programma**: selezionare questa opzione per eseguire un programma in un altro pacchetto, prima di eseguire la sequenza di attività. Per impostazione predefinita, questa casella di controllo è deselezionata. Non è necessario distribuire separatamente il programma che deve essere eseguito per primo.  

        > [!IMPORTANT]
        > Questa impostazione si applica solo alle sequenze di attività che vengono eseguite nel sistema operativo completo. Se si avvia la sequenza di attività usando PXE o il supporto di avvio, Configuration Manager ignora questa impostazione.  

        - **Pacchetto**: cercare il pacchetto contenente il programma da eseguire prima di questa sequenza di attività.  

        - **Programma**: selezionare il programma da eseguire prima di questa sequenza di attività.  

        > [!NOTE]  
        > Se l'esecuzione su in client del programma selezionato non riesce, la sequenza di attività non viene eseguita. Se l'esecuzione del programma selezionato avviene correttamente, il programma non viene eseguito nuovamente, anche se la sequenza di attività viene rieseguita nello stesso client.  

    - **Elimina notifiche della sequenza di attività**: Selezionare questa opzione per nascondere l'avviso popup **È disponibile nuovo software**. Viene ancora visualizzata l'icona **Nuovo software** di Software Center nell'area di notifica. Questa opzione è disabilitata per impostazione predefinita.  

    - **Disattiva questa sequenza di attività nei computer in cui è distribuita**: se si seleziona questa opzione, Configuration Manager disabilita temporaneamente tutte le distribuzioni che contengono questa sequenza di attività. La sequenza di attività viene anche rimossa dall'elenco di distribuzioni disponibili per l'esecuzione. La sequenza di attività viene eseguita solo dopo averla abilitata. Questa opzione è disabilitata per impostazione predefinita.  

    - **Tempo di esecuzione massimo consentito**: specifica il tempo massimo, in minuti, previsto per l'esecuzione della sequenza di attività nel computer di destinazione. Usare un numero intero uguale o maggiore di zero. Per impostazione predefinita, questo valore è impostato su 120 minuti.  

        > [!IMPORTANT]  
        > Se si usano finestre di manutenzione per la raccolta in cui si distribuisce la sequenza di attività, è possibile che si verifichi un conflitto se il **tempo di esecuzione massimo consentito** è superiore alla finestra di manutenzione pianificata. Se si imposta il tempo di esecuzione massimo su **0**, la sequenza di attività viene avviata durante la finestra di manutenzione. L'esecuzione continua fino al completamento oppure ha esisto negativo dopo la chiusura della finestra di manutenzione. Pertanto le sequenze di attività con un tempo massimo di esecuzione impostato su **0** potrebbero essere eseguite dopo il termine delle relative finestre di manutenzione. Se il tempo di esecuzione massimo viene impostato su un periodo specifico, diverso da zero, con durata superiore a quella di tutte le finestre di manutenzione disponibili, la sequenza di attività non viene eseguita. Per altre informazioni, vedere [Come usare le finestre di manutenzione](../../core/clients/manage/collections/use-maintenance-windows.md).  

        Se si imposta il valore su **0**, Configuration Manager valuta il tempo di esecuzione massimo consentito in **12** ore (720 minuti) per il controllo dello stato. Tuttavia, la sequenza di attività viene avviata a condizione che la durata del conto alla rovescia non superi il valore specificato per la finestra di manutenzione.  

        > [!NOTE]
        > Quando raggiunge il tempo massimo di esecuzione, se non si consente agli utenti di interagire con una distribuzione richiesta, Configuration Manager interrompe la sequenza di attività. Se la sequenza di attività non viene arrestata, Configuration Manager arresta il monitoraggio dopo il raggiungimento del tempo di esecuzione massimo consentito.

    - **Utilizza un'immagine d'avvio**: usare l'immagine d'avvio selezionata quando viene eseguita la sequenza di attività. Selezionare **Sfoglia** per selezionare un'altra immagine d'avvio. Deselezionare questa opzione per disabilitare l'uso dell'immagine d'avvio selezionata quando viene eseguita la sequenza di attività.  

    - **Questa sequenza di attività può essere eseguita in qualsiasi piattaforma**: se questa opzione è selezionata, quando viene eseguita la sequenza di attività Configuration Manager non verifica il tipo di piattaforma del computer di destinazione. Questa opzione è selezionata per impostazione predefinita.  

    - **Questa sequenza di attività può essere eseguita solo in piattaforme specifiche**: L'opzione specifica i processori, le versioni dei sistemi operativi e i Service Pack per i quali può essere eseguita la sequenza di attività. Se questa opzione è selezionata, selezionare almeno una piattaforma dall'elenco. Per impostazione predefinita non è selezionata alcuna piattaforma. Configuration Manager usa queste informazioni quando valuta quali computer di destinazione di una raccolta ricevono la sequenza di attività distribuita.  

        > [!NOTE]  
        > Quando si esegue una sequenza di attività dal supporto di avvio o da PXE, Configuration Manager ignora questa opzione. La sequenza di attività viene eseguita come se l'opzione **Questo programma può essere eseguito in qualsiasi piattaforma** fosse selezionata.  

## <a name="high-impact-settings"></a>Impostazioni ad alto impatto

Configurare una sequenza di attività come "ad alto impatto" e personalizzare i messaggi ricevuti dagli utenti quando eseguono la sequenza.

> [!WARNING]
> Se si usano distribuzioni PXE e si configura l'hardware dei dispositivi con la scheda di rete come primo dispositivo di avvio, questi dispositivi possono avviare automaticamente una sequenza di attività di distribuzione del sistema operativo senza l'intervento dell'utente. Questa configurazione non viene gestita dalla procedura di verifica della distribuzione. Se da un lato questa configurazione può semplificare il processo e ridurre l'interazione dell'utente, dall'altro aumenta il rischio di ricreazione accidentale dell'immagine del dispositivo.

### <a name="set-a-task-sequence-as-a-high-impact-task-sequence"></a>Impostare una sequenza di attività come una sequenza di attività a impatto elevato

Attenersi alla procedura seguente per impostare una sequenza di attività a impatto elevato.

> [!NOTE]  
> Qualsiasi sequenza di attività che soddisfi determinate condizioni viene definita automaticamente come a impatto elevato. Per altre informazioni, vedere [Impostazioni per gestire distribuzioni ad alto rischio](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**, espandere **Sistemi operativi** e selezionare **Sequenze di attività**.  

2. Selezionare la sequenza di attività da modificare e selezionare **Proprietà**.  

3. Nella scheda **Notifica utente** selezionare **Questa è una sequenza di attività a impatto elevato**.  

### <a name="create-a-custom-notification-for-high-risk-deployments"></a>Creare una notifica personalizzata per le distribuzioni ad alto rischio

Usare la procedura seguente per creare una notifica personalizzata per le distribuzioni ad alto impatto.

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**, espandere **Sistemi operativi** e selezionare **Sequenze di attività**.  

2. Selezionare la sequenza di attività da modificare e selezionare **Proprietà**.  

3. Nella scheda **Notifica utente** selezionare **Usa il testo personalizzato**.  

    > [!NOTE]
    > È possibile impostare il testo della notifica utente solo quando si seleziona l'opzione **Questa è una sequenza di attività a impatto elevato**.  

4. Configurare le seguenti impostazioni:  

    > [!Note]  
    > Ogni casella di testo ha un limite massimo di 255 caratteri.  

    - **Testo dell'intestazione della notifica all'utente**: specifica il testo blu che viene visualizzato nella notifica utente di Software Center. Ad esempio, nella notifica utente predefinita questa sezione contiene il testo "Confermare l'aggiornamento del sistema operativo in questo computer".  

    - **Testo del messaggio di notifica all'utente**: sono presenti tre caselle di testo che specificano il corpo della notifica personalizzata. Tutte le caselle di testo richiedono l'aggiunta di testo.  

        - Prima casella di testo: specifica il corpo principale del testo, in genere contenente le istruzioni per l'utente. Ad esempio, nella notifica utente predefinita questa sezione contiene il testo "L'aggiornamento del sistema operativo potrebbe durare a lungo e richiedere più riavvii del computer".  

        - Seconda casella di testo: specifica il testo in grassetto nel corpo principale del testo. Ad esempio, nella notifica utente predefinita questa sezione contiene il testo "Questo aggiornamento sul posto installa il nuovo sistema operativo ed esegue automaticamente la migrazione di app, dati e impostazioni".  

        - Terza casella di testo: specifica l'ultima riga di testo in grassetto. Ad esempio, nella notifica all'utente predefinita questa sezione contiene un testo simile a "Fare clic su Installa per iniziare, altrimenti fare clic su Annulla".  

#### <a name="example"></a>Esempio

Si supponga di configurare la notifica personalizzata seguente nelle proprietà.

![Scheda Notifica utente personalizzata delle proprietà della sequenza di attività](../media/user-notification.png)

Viene visualizzato il messaggio di notifica seguente quando l'utente finale apre il programma di installazione da Software Center.

![Notifica di sequenza di attività personalizzata per l'utente finale da Software Center](../media/user-notification-enduser.png)

## <a name="performance-improvements-for-power-plans"></a><a name="bkmk_perf"></a> Miglioramenti delle prestazioni per le combinazioni per il risparmio di energia

<!--3555926-->

A partire dalla versione 1910, è ora possibile eseguire una sequenza di attività con la combinazione per il risparmio di energia per prestazioni elevate. Questa opzione migliora la velocità complessiva della sequenza di attività. Configura Windows in modo da usare la combinazione per il risparmio di energia per prestazioni elevate predefinita, che offre prestazioni massime a scapito di un consumo di energia superiore. Questa opzione è abilitata per impostazione predefinita per le nuove sequenze di attività.

Nella maggior parte degli scenari, all'avvio la sequenza di attività registra la combinazione per il risparmio di energia attualmente abilitata. Imposta quindi come combinazione per il risparmio di energia attiva la combinazione **Prestazioni elevate** predefinita di Windows. Se la sequenza di attività riavvia il computer, questo processo viene ripetuto. Alla fine della sequenza di attività, la combinazione per il risparmio di energia viene reimpostata sul valore archiviato. Questa funzionalità è disponibile sia in Windows che in Windows PE, ma non ha alcun effetto sulle macchine virtuali.

- Se la sequenza di attività viene avviata in Windows PE, la sequenza di attività non registra la combinazione per il risparmio di energia attualmente abilitata per un successivo riutilizzo

- Una sequenza di attività di distribuzione del sistema operativo che ricrea l'immagine del computer (cancellazione e caricamento) non mantiene l'impostazione della combinazione per il risparmio di energia del sistema operativo precedente. Alla fine della sequenza di attività, viene ripristinata la combinazione per il risparmio di energia predefinita **Bilanciata**.

> [!Important]
> Per sfruttare i vantaggi di questa nuova funzionalità di Configuration Manager, dopo l'aggiornamento del sito aggiornare i client alla versione più recente. Aggiornare anche le immagini d'avvio per includere i componenti client più recenti. Anche se le nuove funzionalità vengono visualizzate nella console di Configuration Manager quando si esegue l'aggiornamento del sito e della console, lo scenario completo risulta funzionante solo dopo l'aggiornamento alla versione più recente del client.

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**. Espandere **Sistemi operativi** e selezionare il nodo **Sequenze di attività**.

1. Creare o scegliere una sequenza di attività esistente e quindi selezionare **Proprietà**.

1. Passare alla scheda **Prestazioni**.

1. Abilitare l'opzione **Run as high performance power plan** (Esegui come combinazione per il risparmio di energia per prestazioni elevate).

> [!Warning]
> Prestare attenzione con questa impostazione su hardware a prestazioni ridotte. L'esecuzione di operazioni di sistema intensive per un lungo periodo di tempo può rappresentare un carico eccessivo per hardware di fascia bassa. Rivolgersi al produttore dell'hardware per indicazioni specifiche.

### <a name="known-issue"></a>Problema noto

<!-- 5554928 -->

In genere, quando si modificano le impostazioni nelle proprietà della sequenza di attività, vengono aggiornate tutte le distribuzioni esistenti. La modifica di questa impostazione delle prestazioni nelle proprietà della sequenza di attività non influisce sulle distribuzioni esistenti della sequenza di attività. Per abilitare o disabilitare questa impostazione per prestazioni elevate, creare una nuova distribuzione della sequenza di attività.
<!-- MEMDocs#437, SCCMDocs#2107 -->

## <a name="distribute-referenced-content"></a><a name="BKMK_DistributeTS"></a> Distribuire il contenuto di riferimento  

Prima che i client eseguano una sequenza di attività che fa riferimento al contenuto, distribuire tale contenuto ai punti di distribuzione. In qualsiasi momento, è possibile selezionare la sequenza di attività e distribuire il relativo contenuto per creare un nuovo elenco di pacchetti di riferimento per la distribuzione. Se si apportano modifiche alla sequenza di attività con contenuto aggiornato, ridistribuire il contenuto prima che diventi disponibile per i client. Usare la seguente procedura per distribuire il contenuto a cui fa riferimento una sequenza di attività.  

### <a name="process-to-distribute-referenced-content-to-distribution-points"></a>Processo per la distribuzione di contenuto di riferimento ai punti di distribuzione  

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**, espandere **Sistemi operativi** e quindi selezionare il nodo **Sequenze di attività**.  

2. Nell'elenco **Sequenza di attività** selezionare la sequenza di attività da distribuire.  

3. Nella scheda **Home** della barra multifunzione selezionare **Distribuisci contenuto** nel gruppo **Distribuzione**. Questa azione avvia la Distribuzione guidata contenuto.  

4. Nella pagina **Generale** verificare che sia stata selezionata la sequenza di attività corretta per la distribuzione.  

5. Nella pagina **Contenuto** verificare il contenuto da distribuire, ad esempio l'immagine d'avvio a cui fa riferimento la sequenza di attività.  

6. Nella pagina **Destinazione del contenuto** specificare le raccolte, il punto di distribuzione o il gruppo di punti di distribuzione in cui si vuole distribuire i contenuti della sequenza di attività.  

    > [!IMPORTANT]  
    > Se la sequenza di attività selezionata fa riferimento a contenuto già distribuito in un punto di distribuzione specifico, la procedura guidata non elenca tale punto di distribuzione.  

7. Completare la procedura guidata.  

È anche possibile pre-installare il contenuto a cui viene fatto riferimento nella sequenza di attività. Configuration Manager crea un file di contenuto pre-installato e compresso, contenente i file, le relative dipendenze e i metadati associati per il contenuto selezionato. Si importa quindi manualmente il contenuto in un server del sito, in un sito secondario o in un punto di distribuzione. Per altre informazioni su come pre-installare i file di contenuto, vedere [Prestage content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage) (Pre-installare il contenuto).  

## <a name="deploy"></a><a name="BKMK_DeployTS"></a> Distribuisci  

Per altre informazioni, vedere [Deploy a task sequence](deploy-a-task-sequence.md).

## <a name="export-and-import"></a><a name="BKMK_ExportImport"></a> Esportazione e importazione  

Esportare e importare sequenze di attività con o senza i relativi oggetti. Questo contenuto di riferimento include gli oggetti seguenti:  

- Immagini dei sistemi operativi  
- Immagini d'avvio  
- Pacchetti come il pacchetto di installazione client  
- Pacchetti driver  
- Applicazioni con dipendenze  

Considerare i punti seguenti quando si esportano e importano sequenze di attività:  

- Configuration Manager non esporta le password nella sequenza di attività. Se si esporta e importa una sequenza di attività che contiene password, modificare la sequenza di attività importata per immettere nuovamente le password. Esaminare i passaggi seguenti che possono includere una password:  

  - [Aggiunta a dominio o gruppo di lavoro](../understand/task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)  
  - [Connessione a una cartella di rete](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)  
  - [Esegui riga di comando](../understand/task-sequence-steps.md#BKMK_RunCommandLine)  

- Quando si esporta una sequenza di attività con il passaggio **Imposta variabili dinamiche**, Configuration Manager non esporta i valori per le variabili configurate con l'impostazione **Valore segreto**. Immettere nuovamente i valori per tali variabili dopo aver importato la sequenza di attività.  

- Quando si hanno più siti primari, importare sequenze di attività nel sito di amministrazione centrale.  

### <a name="process-to-export-task-sequences"></a>Processo di esportazione delle sequenze di attività  

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**, espandere **Sistemi operativi** e quindi selezionare il nodo **Sequenze di attività**.  

2. Nell'elenco **Sequenza di attività** , selezionare le sequenze attività che si desidera esportare. Se si seleziona più di una sequenza di attività, vengono memorizzate tutte in un file di esportazione.  

3. Nella scheda **Home** della barra multifunzione selezionare **Esporta** nel gruppo **Sequenza di attività**. Questa azione avvia l'Esportazione guidata della sequenza di attività.  

4. Nella pagina **Generale** specificare le impostazioni seguenti:  

    - **File**: Specificare il percorso e il nome del file di esportazione. Se si immette direttamente il nome del file, assicurarsi di includere l'estensione .zip nel nome del file. Se si seleziona il file di esportazione, la procedura guidata aggiunge automaticamente questa estensione del nome del file.  

    - Per non esportare le dipendenze della sequenza di attività, deselezionare l'opzione **Esporta tutte le dipendenze della sequenza di attività**. Per impostazione predefinita, la procedura guidata esegue la scansione di tutti gli oggetti correlati e li esporta con la sequenza di attività. Tali dipendenze includono tutti i tipi di applicazione.  

    - Per non copiare il contenuto dall'origine del pacchetto al percorso di esportazione, deselezionare l'opzione **Esporta tutti i contenuti per le sequenze di attività selezionate e le dipendenze**. Se si seleziona questa opzione, l'Importazione guidata della sequenza di attività usa il percorso di importazione come nuovo percorso di origine del pacchetto.  

    - **Commenti amministratore**: Aggiungere una descrizione della sequenza di attività da esportare.  

5. Completare la procedura guidata.  

La procedura guidata crea i seguenti file di output:  

- Se non si esporta contenuto: un file ZIP.  

- Se si esporta contenuto: un file compresso e una cartella denominata *export*_files, in cui *export* è il nome del file compresso che contiene il contenuto esportato.  

Se si include del contenuto quando si esporta una sequenza di attività, assicurarsi di copiare il file con estensione zip e la cartella *export*_files, altrimenti l'importazione non avrà esito positivo.  

### <a name="process-to-import-task-sequences"></a>Processo di importazione delle sequenze di attività  

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**, espandere **Sistemi operativi** e quindi selezionare il nodo **Sequenze di attività**.  

2. Nella scheda **Home** della barra multifunzione selezionare **Importa sequenza di attività** nel gruppo **Crea**. Questa azione avvia l'Importazione guidata della sequenza di attività.  

3. Nella pagina **Generale** della barra multifunzione specificare il file ZIP esportato.  

4. Nella pagina **Contenuto file** , selezionare l'azione richiesta per ogni oggetto da importare. In questa pagina vengono visualizzati tutti gli oggetti individuati da Configuration Manager per l'importazione.  

    - Se l'oggetto non è mai stata importato, selezionare **Crea nuovo**.  

    - Se l'oggetto è stato importato in precedenza, selezionare una delle seguenti azioni:  

        - **Ignora duplicato** (impostazione predefinita): questa azione non importa l'oggetto. Al contrario, la procedura guidata collega l'oggetto esistente alla sequenza di attività.  

        - **Sovrascrivi**: Questa azione sovrascrive l'oggetto esistente con l'oggetto importato. Per le applicazioni, è possibile aggiungere una revisione per aggiornare l'applicazione esistente o creare una nuova applicazione.  

5. Completare la procedura guidata.  

Dopo aver importato la sequenza di attività, modificarla per specificare le password che erano presenti nella sequenza di attività originale. Per motivi di sicurezza, le password non vengono esportate.  

## <a name="return-to-previous-page-on-failure"></a>Tornare alla pagina precedente in caso di errore

Quando si esegue una sequenza di attività e si verifica un errore, è possibile tornare a una pagina precedente della creazione guidata della sequenza di attività. Nelle versioni precedenti di Configuration Manager se si verificava un errore era necessario riavviare la sequenza di attività. Usare il pulsante **Precedente** negli scenari seguenti:

- Quando un computer viene avviato in Windows PE, potrebbe essere visualizzata la finestra di dialogo di avvio della sequenza di attività prima che la sequenza stessa sia disponibile. Se in questo scenario si seleziona Avanti, viene visualizzata la pagina finale della sequenza di attività che informa l'utente che non sono disponibili sequenze di attività. È ora possibile selezionare **Precedente** per ripetere la ricerca di sequenze di attività. È possibile ripetere questo processo finché la sequenza di attività non è disponibile.  

- Quando si esegue una sequenza di attività ma i pacchetti di contenuto dipendenti non sono ancora disponibili nei punti di distribuzione, la sequenza di attività ha esito negativo. Distribuire il contenuto mancante non ancora distribuito. In alternativa, attendere che il contenuto sia disponibile nei punti di distribuzione. Quindi selezionare **Precedente** per fare in modo che la sequenza di attività cerchi nuovamente il contenuto.

## <a name="collection-and-device-variables"></a><a name="BKMK_CreateTSVariables"></a> Variabili di raccolta e dispositivo

È possibile definire variabili della sequenza di attività personalizzate per computer e insiemi. Le variabili definite per un computer vengono definite variabili della sequenza di attività con ambito computer. Le variabili definite per una raccolta vengono definite variabili della sequenza di attività con ambito raccolta. Per altre informazioni, vedere [Variabili di raccolta e dispositivo](../understand/using-task-sequence-variables.md#bkmk_set-coll-var).

## <a name="additional-actions"></a><a name="BKMK_AdditionalActionsTS"></a> Azioni aggiuntive  

È possibile gestire le sequenze di attività usando le azioni aggiuntive disponibili quando si seleziona la sequenza di attività.  

### <a name="edit"></a>Modifica

Per altre informazioni, vedere [Usare l'editor delle sequenze di attività](../understand/task-sequence-editor.md#bkmk_edit).

### <a name="enable"></a>Abilitare

Attiva la sequenza di attività in modo che i client possano eseguirla. Dopo l'attivazione non è necessario ridistribuire una sequenza di attività.  

### <a name="disable"></a>Disabilitato

Disattiva la sequenza di attività in modo che non possa essere eseguita nei computer. Le sequenze attività disattivate possono essere distribuite ai computer, ma questi non le eseguono finché non vengono attivate.  

### <a name="export"></a>Export

Per altre informazioni, vedere [Esportare e importare sequenze di attività](#BKMK_ExportImport).

### <a name="copy"></a>Copia

Crea una copia della sequenza di attività selezionata. Questa azione è utile quando si crea una nuova sequenza di attività basata su una sequenza di attività esistente.

Quando si copia una sequenza di attività in una cartella, la copia viene elencata in tale cartella fino all'aggiornamento del nodo sequenza di attività. Dopo l'aggiornamento, la copia viene visualizzata nella cartella principale.  

### <a name="refresh"></a>Aggiorna

Aggiorna i dettagli per la sequenza di attività selezionata.

### <a name="delete"></a>Elimina

Elimina la sequenza di attività selezionata.

### <a name="create-phased-deployment"></a>Crea una distribuzione in più fasi

Per altre informazioni, vedere [Creare distribuzioni in più fasi](create-phased-deployment-for-task-sequence.md).

### <a name="deploy"></a>Distribuisci

Per altre informazioni, vedere [Deploy a task sequence](deploy-a-task-sequence.md).

### <a name="distribute-content"></a>Distribuisci contenuto

Avvia la Distribuzione guidata contenuto per inviare il contenuto di riferimento ai punti di distribuzione.

### <a name="create-prestaged-content-file"></a>Crea file di contenuto pre-installazione

Avvia la Creazione guidata file di contenuto pre-installazione per pre-installare il contenuto della sequenza di attività. Per informazioni su come creare un file di contenuto pre-installato, vedere [Prestage content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage) (Pre-installare il contenuto).

### <a name="move"></a>Sposta

Sposta la sequenza di attività selezionata in un'altra cartella nel nodo **Sequenze di attività**.

### <a name="set-security-scopes"></a>Imposta ambiti di protezione

Selezionare gli ambiti di protezione per la sequenza di attività selezionata. Per altre informazioni, vedere [Ambiti di protezione](../../core/understand/fundamentals-of-role-based-administration.md#bkmk_PlanScope).

### <a name="properties"></a>Proprietà

Per altre informazioni, vedere [Configurare le proprietà di Software Center](#bkmk_prop-general) e [Configurare impostazioni della sequenza di attività avanzate](#bkmk_prop-advanced).

### <a name="view"></a>Visualizza

<!--3633146-->
A partire dalla versione 1902, l'azione **Visualizza** è il valore predefinito per le sequenze di attività. Questa azione consente di vedere i passaggi della sequenza di attività senza bloccarla per la modifica. Per altre informazioni, vedere [Usare l'editor delle sequenze di attività](../understand/task-sequence-editor.md#bkmk_view).

## <a name="see-also"></a>Vedere anche

- [Scenari di distribuzione di sistemi operativi aziendali](scenarios-to-deploy-enterprise-operating-systems.md)

- [Usare l'editor delle sequenze di attività](../understand/task-sequence-editor.md)

- [Distribuire una sequenza di attività](deploy-a-task-sequence.md)

- [Passaggi della sequenza di attività](../understand/task-sequence-steps.md)

- [Variabili di raccolta e dispositivo](../understand/using-task-sequence-variables.md#bkmk_set-coll-var)

- [Creare distribuzioni in più fasi](create-phased-deployment-for-task-sequence.md)
