---
title: Eseguire il backup di siti
titleSuffix: Configuration Manager
description: Informazioni su come eseguire un backup di siti prima di un evento di errore o di perdita di dati in Configuration Manager.
ms.date: 01/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f7832d83-9ae2-4530-8a77-790e0845e12f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 824eaeb939249e1bcc2ed21d5815a0a72dc54797
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700269"
---
# <a name="back-up-a-configuration-manager-site"></a>Eseguire il backup di un sito di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Preparare gli approcci di backup e ripristino per evitare la perdita di dati. Per i siti di Configuration Manager un approccio di backup e ripristino consente di ripristinare siti e gerarchie più rapidamente e con la minore perdita di dati.  

Le sezioni di questo articolo illustrano come eseguire un backup dei siti. Per ripristinare un sito, vedere [Ripristino per Configuration Manager](recover-sites.md).  

<!--/SCCMdocs/issues/2108-->
>[!WARNING]
> I due metodi di backup supportati per il ripristino dei siti di Configuration Manager sono:
>
> - Un backup corretto dall'attività di manutenzione **Backup server sito**
> - Un backup del database del sito ripristinato manualmente


## <a name="considerations-before-creating-a-backup"></a>Considerazioni prima della creazione di un backup  

-   Se si usa un gruppo di disponibilità SQL Server Always On per ospitare il database del sito: Modificare i piani di backup e ripristino come descritto in [Preparare l'uso di gruppi di disponibilità Always On](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#changes-for-site-backup).  

-   Il ripristino del database del sito può essere eseguito dall'attività di backup di Configuration Manager. Può anche essere usato un backup del database del sito creato con un altro processo.   

     Ad esempio, è possibile ripristinare il database del sito da un backup creato nell'ambito di un piano di manutenzione di Microsoft SQL Server. È possibile anche usare un backup creato usando Data Protection Manager per eseguire un backup del database del sito.  

-   A partire dalla versione 1806, installare un server del sito aggiuntivo in modalità *passiva*. Il server del sito in modalità passiva è in aggiunta al server del sito esistente in modalità *attiva*. Un server del sito in modalità passiva è disponibile per l'uso immediato, quando è necessario. Per altre informazioni, vedere [Disponibilità elevata del server del sito](../deploy/configure/site-server-high-availability.md). Sebbene non elimini la necessità di pianificare ed eseguire le operazioni di backup e ripristino, questo ruolo riduce notevolmente il lavoro richiesto per ripristinare un sito quando è necessario.  
  

####  <a name="using-data-protection-manager-to-back-up-your-site-database"></a>Utilizzo di Data Protection Manager per eseguire il backup del database del sito
È possibile usare Microsoft System Center Data Protection Manager (DPM) per eseguire un backup del database del sito di Configuration Manager.

È necessario creare un nuovo gruppo di protezione dati in DPM per il computer del database del sito. Nella pagina **Seleziona membri del gruppo** della procedura guidata Crea nuovo gruppo protezione dati selezionare il servizio SMS Writer dall'elenco di origine dei dati. Selezionare quindi il database del sito come membro appropriato. Per altre informazioni su DPM, vedere la raccolta della documentazione di [Data Protection Manager](https://docs.microsoft.com/system-center/dpm).  

> [!IMPORTANT]  
>  Configuration Manager non supporta il backup di DPM per un cluster SQL Server che usa un'istanza denominata. Supporta tuttavia il backup di DPM in un cluster di SQL Server che usa l'istanza predefinita di SQL Server.  

Dopo il ripristino del database del sito, seguire i passaggi della procedura di installazione per ripristinare il sito. Per usare il database del sito di cui è stato eseguito un backup con Data Protection Manager, selezionare l'opzione di ripristino **Utilizza un database del sito ripristinato manualmente**.  



## <a name="backup-maintenance-task"></a>Attività di manutenzione di backup
È possibile automatizzare il backup per i siti di Configuration Manager mediante la programmazione dell'attività di manutenzione Backup server sito predefinita. Questa attività include le funzionalità seguenti:

-   Viene eseguita in base a una pianificazione
-   Esegue il backup del database del sito
-   Esegue il backup di chiavi del Registro di sistema specifiche
-   Esegue il backup di cartelle e file specifici
-   Esegue il backup della cartella [CD.Latest](the-cd.latest-folder.md)   

Pianificare l'esecuzione dell'attività di backup del sito predefinita almeno ogni cinque giorni. Il motivo è che Configuration Manager usa un *periodo di conservazione del rilevamento modifiche di SQL Server* di 5 giorni. Per altre informazioni, vedere [Periodo di conservazione del rilevamento modifiche di SQL Server](recover-sites.md#sql-server-change-tracking-retention-period).

Per semplificare il processo di backup, è possibile creare un file **AfterBackup.bat**. Questo script esegue automaticamente le azioni post-backup dopo che l'attività di backup è stata completata correttamente. Il file AfterBackup.bat viene usato di solito per archiviare lo snapshot di backup in un percorso sicuro. È possibile anche usare il file AfterBackup.bat per copiare i file nella cartella di backup e avviare altre attività di backup.  

È possibile eseguire un backup di un sito di amministrazione centrale e di un sito primario. I siti secondari o i server del sistema del sito non prevedono attività di backup.

Quando viene eseguito il servizio di backup di Configuration Manager, vengono seguite le istruzioni definite nel file di controllo del backup: `<ConfigMgrInstallationFolder>\Inboxes\Smsbkup.box\Smsbkup.ctl`. È possibile modificare il file di controllo del backup per modificare il comportamento del servizio di backup.  
> [!NOTE]
> Le modifiche di **Smsbkup.ctl** verranno applicate dopo un riavvio del servizio SMS_SITE_VSS_WRITER nel server del sito.

Le informazioni sullo stato di backup del sito vengono scritte nel file **Smsbkup.log** . Questo file viene creato nella cartella di destinazione specificata nelle proprietà dell'attività di manutenzione Backup server sito.  

#### <a name="to-enable-the-site-backup-maintenance-task"></a>Per attivare l'attività di manutenzione di backup del sito  
1.  Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito** e selezionare **Siti**.  

2.  Selezionare il sito per cui si vuole attivare l'attività di manutenzione di backup del sito.  

3.  Fare clic su **Attività di manutenzione del sito** nella barra multifunzione.  

4.  Selezionare l'attività **Backup server sito** e fare clic su **Modifica**.  

5.  Selezionare l'opzione **Abilita questa attività**. Fare clic su **Imposta percorsi** per specificare la destinazione di backup. Sono disponibili le seguenti opzioni:  

    > [!IMPORTANT]  
    >  Per impedire la manomissione dei file di backup, archiviare i file in una posizione sicura. Il percorso di backup più sicuro è un'unità locale, che consente di impostare le autorizzazioni file NTFS per la cartella. Configuration Manager non esegue la crittografia dei dati di backup archiviati nel percorso di backup.  

    -   **Unità locale nel server del sito per il database e i dati del sito**: specifica che l'attività deve archiviare i file di backup per il sito e il database del sito nel percorso specificato nell'unità disco locale del server del sito. Creare la cartella locale prima dell'esecuzione dell'attività di backup. L'account di sistema locale nel server del sito deve disporre delle autorizzazioni file NTFS di **Scrittura** nella cartella locale per il backup del server del sito. L'account di sistema locale nel computer che esegue SQL Server deve disporre delle autorizzazioni NTFS di **Scrittura** nella cartella per il backup del database del sito.  

    -   **Percorso di rete (nome UNC) per il database e i dati del sito**: specifica che l'attività deve archiviare i file di backup per il sito e il database del sito nel percorso di rete indicato. Creare la condivisione prima dell'esecuzione dell'attività di backup. L'account computer del server del sito deve disporre delle autorizzazioni di condivisione e NTFS di **Scrittura** per la cartella di rete condivisa. Se SQL Server è installato su un altro computer, l'account computer di SQL Server deve avere le stesse autorizzazioni.  

    -   **Unità locali nel server del sito e in SQL Server**: specifica che l'attività deve archiviare i file di backup per il sito nel percorso specificato nell'unità locale del server del sito. L'attività archivia i file di backup per il database del sito nel percorso specificato nell'unità locale del server del database del sito. Creare le cartelle locali prima dell'esecuzione dell'attività di backup. L'account computer del server del sito deve disporre delle autorizzazioni NTFS di **Scrittura** nella cartella creata nel server del sito. L'account computer di SQL Server deve disporre delle autorizzazioni NTFS di **Scrittura** nella cartella creata nel server di database del sito. Questa opzione è disponibile solo quando il database del sito non è installato nel server del sito.  

    > [!NOTE]  
    > L'opzione per selezionare la destinazione di backup è disponibile solo quando si specifica il percorso di rete della destinazione di backup.  
    >  
    > Il nome della cartella o il nome condivisione usato per la destinazione di backup non supporta l'utilizzo di caratteri Unicode.  

6.  Configurare una pianificazione per l'attività di backup del sito. È consigliabile pianificare l'esecuzione del backup in orari non lavorativi. Se è presente una gerarchia, è consigliabile una pianificazione da eseguire almeno due volte a settimana. Se si verifica un problema nel sito, questa pianificazione garantisce la massima conservazione dati.  

    Quando Console di Configuration Manager viene eseguita nello stesso server del sito configurato per il backup, l'attività di backup usa l'ora locale per la pianificazione. Quando si esegue Console di Configuration Manager da un altro computer, l'attività di backup usa l'ora Coordinated Universal Time (UTC) per la pianificazione.  

7.  Scegliere se creare un avviso in caso di errore dell'attività di backup del sito. Se l'opzione è selezionata, Configuration Manager crea un avviso critico per l'errore di backup. È possibile esaminare questi avvisi nel nodo **Avvisi** dell'area di lavoro **Monitoraggio**.  

#### <a name="verify-that-the-backup-site-server-maintenance-task-is-running"></a>Verificare che l'attività di manutenzione Backup server sito sia stata completata correttamente  

-   Esaminare il timestamp nei file della cartella di destinazione del backup creata dall'attività di manutenzione Backup server sito. Verificare che il timestamp sia aggiornato all'orario in cui è stata pianificata l'ultima esecuzione dell'attività.  

-   Passare al nodo **Stato componente** dell'area di lavoro **Monitoraggio**. Esaminare i messaggi di stato relativi a **SMS_SITE_BACKUP**. Quando il backup del sito viene completato correttamente, viene visualizzato l'ID messaggio **5035**. Il messaggio indica che il backup del sito è stato completato senza errori.  

-   Quando si configura l'attività di backup per creare un avviso in caso di errore, cercare gli avvisi di errore di backup nel nodo **Avvisi** dell'area di lavoro **Monitoraggio**.  

-   Aprire Esplora risorse nel server del sito e selezionare `<ConfigMgrInstallationFolder>\Logs`. Verificare la presenza di errori e avvisi nel file **Smsbkup.log**. Quando il backup del sito è stato completato correttamente, il registro indica `Backup completed` con ID messaggio `STATMSG: ID=5035`.  

    > [!TIP]  
    >  In caso di errore dell'attività di manutenzione di backup, riavviare l'attività di backup interrompendo e riavviando il servizio Windows **SMS_SITE_BACKUP**.  



## <a name="archive-the-backup-snapshot"></a>Archiviare lo snapshot di backup  
L'attività di backup crea uno snapshot del backup la prima volta che viene eseguita. È possibile usare questo snapshot per ripristinare il server del sito in caso di errore. Quando l'attività di backup viene eseguita nuovamente in base alla pianificazione, viene creato un nuovo snapshot di backup che sovrascrive lo snapshot precedente. Di conseguenza, il sito dispone di un singolo snapshot di backup e non è possibile recuperare uno snapshot di backup precedente.  

Mantenere più archivi dello snapshot di backup per i seguenti motivi:  

-   I supporti di backup possono presentare problemi, venire smarriti o includere solo un backup parziale. Il ripristino di un sito primario autonomo danneggiato da un vecchio backup è una soluzione migliore rispetto a un ripristino senza backup. Per un server del sito in una gerarchia, il backup deve essere eseguito nel periodo di conservazione del rilevamento modifiche SQL Server oppure il backup non è necessario.  

-   È possibile che un danneggiamento del sito non venga rilevato per diversi cicli di backup. Potrebbe essere necessario usare lo snapshot di un backup precedente il danneggiamento del sito. Questo motivo si applica a un sito primario autonomo e ai siti in una gerarchia in cui il backup rientri nel periodo di conservazione del rilevamento modifiche SQL Server.  

-   Il sito potrebbe non avere uno snapshot di backup, ad esempio se si verifica un problema nell'attività di manutenzione Backup Server sito. Dal momento che l'attività di backup determina la rimozione dello snapshot di backup precedente prima di avviare il backup dei dati correnti, non sarà disponibile uno snapshot di backup valido.  



## <a name="using-the-afterbackupbat-file"></a>Uso del file AfterBackup.bat  
Dopo avere eseguito correttamente il backup del sito, l'attività di backup prova a eseguire automaticamente un script denominato **AfterBackup.bat**. Creare manualmente il file AfterBackup.bat nel server del sito in `<ConfigMgrInstallationFolder>\Inboxes\Smsbkup.box`. Se è già presente nella cartella corretta, il file AfterBackup.bat viene eseguito automaticamente al termine dell'attività di backup.

Il file AfterBackup.bat consente di archiviare lo snapshot di backup al termine di ogni operazione di backup. Può eseguire automaticamente altre attività dopo il backup non incluse nell'attività di manutenzione Backup server sito. Il file AfterBackup.bat integra l'archivio e le operazioni di backup, assicurando che ogni nuovo snapshot di backup sia archiviato.

Se il file AfterBackup.bat non è presente, questo passaggio viene ignorato dall'attività di backup, senza alcun effetto sull'operazione di backup. Per verificare che l'attività di backup abbia eseguito correttamente questo script, passare al nodo **Stato componente** nell'area di lavoro **Monitoraggio** ed esaminare i messaggi di stato relativi a **SMS_SITE_BACKUP**. Quando l'attività avvia correttamente il file di comando AfterBackup.bat, viene visualizzato l'ID messaggio **5040**.  

> [!TIP]  
>  Per archiviare i file di backup del server sito con AfterBackup.bat è necessario usare uno strumento di comando copia nel file batch. Uno di questi strumenti è [Robocopy](https://docs.microsoft.com/windows-server/administration/windows-commands/robocopy) in Windows Server. Ad esempio, creare il file AfterBackup.bat con il seguente comando: `Robocopy E:\ConfigMgr_Backup \\ServerName\ShareName\ConfigMgr_Backup /MIR`  

Sebbene l'uso previsto del file AfterBackup.bat sia l'archiviazione di snapshot di backup, è possibile creare un file AfterBackup.bat che consenta di eseguire attività aggiuntive al termine di ogni operazione di backup.  



##  <a name="supplemental-backup-tasks"></a>Attività di backup supplementari  
L'attività di manutenzione Backup server sito fornisce uno snapshot di backup per i file del server del sito e il database del sito. Quando si definisce una strategia di backup, occorre considerare anche altri elementi di cui non viene eseguito il backup. Per completare la strategia di backup di Configuration Manager usare queste sezioni.  

### <a name="back-up-custom-reports"></a>Eseguire il backup di report personalizzati   
Se si modificano report personalizzati creati o predefiniti in SQL Server Reporting Services, creare un backup per i file di database del server di report. Il backup del server di report deve includere i componenti seguenti:
- File di origine per i report e i modelli
- Chiavi di crittografia
- Estensioni o assembly personalizzati
- File di configurazione
- Viste personalizzate di SQL Server usate nei report personalizzati
- Stored procedure personalizzate  

> [!IMPORTANT]  
>  Quando Configuration Manager viene aggiornato a una versione più recente, i report predefiniti potrebbero essere sovrascritti da nuovi report. Se si modifica un report predefinito, assicurarsi di eseguirne il backup e quindi di ripristinarlo in Reporting Services.  

Per altre informazioni sul backup di report personalizzati in Reporting Services, vedere [Operazioni di backup e ripristino per Reporting Services](https://docs.microsoft.com/sql/reporting-services/install-windows/backup-and-restore-operations-for-reporting-services).  

### <a name="back-up-content-files"></a>Eseguire il backup di file di contenuto  
La raccolta contenuto in Configuration Manager è la posizione in cui vengono archiviati tutti i file di contenuto per tutte le distribuzioni software. La raccolta contenuto si trova sul server del sito e in corrispondenza di ogni punto di distribuzione. L'attività di manutenzione Backup server sito non esegue il backup della libreria contenuto o dei file di origine del pacchetto. Quando si verifica un errore sul server del sito, le informazioni sulla raccolta contenuto vengono ripristinate nel database del sito, ma è necessario ripristinare la raccolta contenuto e i file di origine del pacchetto.  

-   È necessario ripristinare la raccolta contenuto prima di ridistribuire il contenuto nei punti di distribuzione. Quando si avvia la ridistribuzione del contenuto, Configuration Manager copia i file dalla raccolta contenuto sul server del sito nei punti di distribuzione. Per altre informazioni, vedere [Raccolta contenuto](../../plan-design/hierarchy/the-content-library.md).  

-   Prima di aggiornare il contenuto nei punti di distribuzione, è necessario ripristinare i file di origine del pacchetto. Quando si avvia un aggiornamento del contenuto, Configuration Manager copia i file nuovi o modificati dall'origine del pacchetto nella raccolta contenuto. I file vengono quindi copiati nei punti di distribuzione associati. Eseguire la query SQL Server seguente sul database del sito per trovare il percorso di origine del pacchetto per tutti i pacchetti e le applicazioni: `SELECT * FROM v_Package`. È possibile identificare il sito di origine del pacchetto esaminando i primi tre caratteri dell'ID di pacchetto. Ad esempio, se l'ID del pacchetto è CEN00001, il codice del sito per il sito di origine è CEN. I file di origine del pacchetto devono essere ripristinati nella stessa posizione in cui si trovavano prima dell'errore.  

Verificare di avere incluso sia la raccolta contenuto sia i file di origine del pacchetto nel backup del file system per il server del sito.  

### <a name="back-up-custom-software-updates"></a>Eseguire il backup di aggiornamenti software personalizzati  
System Center Updates Publisher è uno strumento autonomo che consente di gestire gli aggiornamenti software personalizzati. Updates Publisher usa un database locale per il relativo repository degli aggiornamenti software. Quando si usa Updates Publisher per gestire gli aggiornamenti software personalizzati, stabilire se è necessario includere il database di Updates Publisher nel piano di backup. Per altre informazioni, vedere [System Center Updates Publisher](../../../sum/tools/updates-publisher.md).  

Per eseguire il backup del database Updates Publisher usare la procedura seguente.  

#### <a name="back-up-the-updates-publisher-database"></a>Eseguire un backup del database di Updates Publisher  

1.  Nel computer su cui è in esecuzione Updates Publisher individuare il file di database di Updates Publisher **Scupdb.sdf** in `%USERPROFILE%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\`. Esiste un file di database diverso per ogni utente che esegue Updates Publisher.  

2.  Copiare il file di database nella destinazione di backup. Ad esempio, se la destinazione di backup è `E:\ConfigMgr_Backup`, è possibile copiare il file di database di Updates Publisher in `E:\ConfigMgr_Backup\SCUP`.  

    > [!TIP]  
    >  In presenza di più file di database su un computer, è consigliabile archiviare il file in una sottocartella che indichi il profilo associato con il file di database. Ad esempio, si potrebbe avere un file di database in `E:\ConfigMgr_Backup\SCUP\User1` e un altro file di database in `E:\ConfigMgr_Backup\SCUP\User2`.  



## <a name="user-state-migration-data"></a>Dati di migrazione sullo stato utente  
È possibile usare le sequenze di attività di Configuration Manager per acquisire e ripristinare i dati dello stato utente in scenari di distribuzione del sistema operativo. Le proprietà del punto di migrazione dello stato elencano le cartelle in cui sono memorizzati i dati dello stato dell'utente. Non è previsto il backup di questi dati nell'ambito dell'attività di manutenzione Backup server sito. Come parte del piano di backup, è necessario eseguire manualmente il backup delle cartelle in cui si è specificato di archiviare i dati di migrazione sullo stato dell'utente.   

### <a name="determine-the-folders-used-to-store-user-state-migration-data"></a>Determinare le cartelle usate per l'archiviazione dei dati di migrazione sullo stato dell'utente  

1.  Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito** e selezionare il nodo **Server e ruoli del sistema del sito**.  

2.  Selezionare il sistema del sito che ospita il ruolo di migrazione stato. Quindi selezionare **Punto di migrazione stato** nel riquadro **Ruoli sistema del sito**.  

3.  Fare clic su **Proprietà** nella barra multifunzione.  

4.  Nella sezione **Dettagli cartella** della scheda **Generale** vengono elencate le cartelle in cui sono archiviati i dati di migrazione sullo stato dell'utente.  



## <a name="about-the-sms-writer-service"></a>Informazioni sul servizio SMS Writer  
SMS Writer è un servizio che interagisce con Servizio Copia Shadow del volume di Windows durante il processo di backup. Per il corretto completamento del backup del sito di Configuration Manager è necessario che SMS Writer sia in esecuzione.  

### <a name="process"></a>Processo  
1. SMS Writer esegue la registrazione al servizio VSS e associa le interfacce e gli eventi. 
2. Quando VSS trasmette gli eventi o invia determinate notifiche a SMS Writer, questo risponde alla notifica ed esegue l'azione appropriata. 
3. SMS Writer legge il file di controllo del backup **smsbkup.ctl** presente in `<ConfigMgrInstallationPath>\inboxes\smsbkup.box` e determina i file e i dati di cui eseguire il backup. 
4. SMS Writer crea i metadati, composti da vari componenti, inclusi dati specifici provenienti dalla chiave e dalle sottochiavi del registro SMS. 
    a. Quando richiesto invia i metadati al Servizio Copia Shadow del volume. 
    b. Il Servizio Copia Shadow del volume invia quindi i metadati all'applicazione richiedente: Gestione backup di Configuration Manager. 
5. Gestione backup seleziona i dati di cui eseguire il backup e li invia a SMS Writer tramite il Servizio Copia Shadow del volume. 
6. SMS Writer esegue i passaggi appropriati per la preparazione del backup. 
7. In seguito, quando il Servizio Copia Shadow del volume è pronto per acquisire lo snapshot: a. Invia un evento b. SMS Writer arresta tutti i servizi di Configuration Manager c. Assicura che le attività di Configuration Manager siano bloccate durante la creazione dello snapshot. 
8. In seguito al completamento dello snapshot, SMS Writer riavvia i servizi e le attività.

Il servizio SMS Writer viene installato automaticamente. Deve essere eseguito quando l'applicazione VSS richiede un backup o un ripristino.  

### <a name="writer-id"></a>ID writer  
L'ID writer per SMS Writer è: **03ba67dd-dc6d-4729-a038-251f7018463b**.  

### <a name="permissions"></a>Autorizzazioni  
Il servizio SMS Writer deve essere eseguito all'interno dell'account di sistema locale.  

### <a name="volume-shadow-copy-service"></a>Servizio Copia Shadow del volume  
VSS è un set di API COM che consente di implementare un framework per l'esecuzione dei backup del volume durante la scrittura delle applicazioni di un sistema nei volumi. VSS offre un'interfaccia coerente che consente il coordinamento tra le applicazioni utente per l'aggiornamento dei dati sul disco (il servizio SMS Writer) e quelle che eseguono il backup delle applicazioni (il servizio Gestione backup). Per altre informazioni, vedere [Servizio Copia Shadow del volume](https://go.microsoft.com/fwlink/p/?LinkId=241968).  



## <a name="next-steps"></a>Passaggi successivi
Dopo aver creato un backup, esercitarsi a [ripristinare il sito](recover-sites.md) con tale backup. Questa esercitazione permette di acquisire familiarità con il processo di ripristino prima di fare affidamento su di esso. Può consentire anche di verificare che il backup sia stato utile allo scopo designato.  
