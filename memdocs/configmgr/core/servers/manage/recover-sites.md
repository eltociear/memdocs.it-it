---
title: Ripristino del sito
titleSuffix: Configuration Manager
description: Informazioni su come ripristinare i siti in Configuration Manager.
ms.date: 06/02/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 19539f4d-1667-4b4c-99a1-9995f12cf5f7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9e71baef06349a00d49bc7fdc799d078c29939d8
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699518"
---
# <a name="recover-a-configuration-manager-site"></a>Ripristinare un sito di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Eseguire un ripristino del sito di Configuration Manager dopo che si verifica un errore nel sito o una perdita di dati nel database del sito. La riparazione e la risincronizzazione dei dati sono le attività principali del ripristino di un sito e sono necessarie per evitare l'interruzione delle operazioni.

Le sezioni in questo articolo sono utili per il ripristino di un sito di Configuration Manager. Per creare un backup, vedere [Backup di Configuration Manager](backup-and-recovery.md).

## <a name="considerations-before-recovering-a-site"></a>Considerazioni prima del recupero di un sito

> [!Important]  
> Queste informazioni si applicano solo agli scenari di ripristino sito. Se si sta aggiornando l'infrastruttura locale e non ripristinando attivamente un sito in cui si è verificato un errore, esaminare le informazioni negli articoli seguenti:
>
> - [Aggiornare l'infrastruttura locale](upgrade-on-premises-infrastructure.md)
> - [Modificare l'infrastruttura](modify-your-infrastructure.md)

### <a name="prepare-the-server-hardware"></a>Preparare l'hardware del server

<!-- 2841893 -->

Verificare che non siano presenti configurazioni esistenti nel server del sito. Qualsiasi configurazione precedente può causare conflitti durante il processo di ripristino del sito. Per l'hardware del server usare una delle opzioni seguenti:

- Usare un nuovo server che soddisfi i requisiti generali e di ripristino.

- Formattare i dischi e reinstallare il sistema operativo nel server esistente. Assicurarsi che soddisfi i requisiti generali e di ripristino.

- Riusare un server esistente pulito.

Per pulire un server esistente, usare una delle procedure seguenti:

#### <a name="clean-an-existing-server-for-site-server-recovery-only"></a>Pulire un server esistente solo per il ripristino del server del sito

1. Eliminare le chiavi del Registro di sistema SMS: `HKLM\Software\Microsoft\SMS`.
2. Eliminare tutte le voci del Registro di sistema che iniziano con `SMS` da `HKLM\System\CurrentControlSet\Services`. Ad esempio:
    - SMS_DISCOVERY_DATA_MANAGER
    - SMS_EXECUTIVE
    - SMS_INBOX_MONITOR
    - SMS_INVENTORY_DATA_LOADER
    - SMS_LAN_SENDER
    - SMS_MP_FILE_DISPATCH_MANAGER
    - SMS_SCHEDULER
    - SMS_SITE_BACKUP
    - SMS_SITE_COMPONENT_MANAGER
    - SMS_SITE_SQL_BACKUP
    - SMS_SITE_VSS_WRITER
    - SMS_SOFTWARE_METERING_PROCESSOR
    - SMS_STATE_SYSTEM
    - SMS_STATUS_MANAGER
    - SMS_WSUS_SYNC_MANAGER
    - SMSvcHost 3.0.0.0
    - SMSvcHost 4.0.0.0
3. Disinstallare la console di Configuration Manager.
4. Riavviare il server.
5. Verificare che tutte le chiavi del Registro di sistema sopra riportate siano state eliminate.

Il server è ora pronto per la procedura di ripristino di Configuration Manager.

#### <a name="clean-an-existing-server-for-site-database-recovery-only"></a>Pulire un server esistente solo per il ripristino del database del sito

1. Eseguire il backup del database del sito. Eseguire anche il backup di tutti gli altri database di supporto, come WSUS.
2. Assicurarsi di prendere nota del nome del server SQL e del nome dell'istanza.
3. Eliminare manualmente il database del sito da SQL Server.
4. Riavviare SQL Server.

Il server è ora pronto per la procedura di ripristino di Configuration Manager.

#### <a name="clean-an-existing-server-for-full-recovery"></a>Pulire un server esistente per il ripristino completo

1. Eseguire il backup del database del sito. Eseguire anche il backup di tutti gli altri database di supporto, come WSUS.
2. Creare una copia della raccolta contenuto.
3. Eliminare manualmente il database del sito da SQL Server.
4. Disinstallare il sito di Configuration Manager.
5. Eliminare manualmente la cartella di installazione di Configuration Manager e tutte le altre cartelle di Configuration Manager.
6. Riavviare il server.
7. Ripristinare la raccolta contenuto e gli altri database come WSUS.

Il server è ora pronto per la procedura di ripristino di Configuration Manager.

### <a name="use-a-supported-version-and-same-edition-of-sql-server"></a>Usare una versione supportata e la stessa edizione di SQL Server

<!-- SCCMDocs#751 -->

Se possibile, usare la stessa versione di SQL Server. Tuttavia, è possibile ripristinare un database in una versione più recente.

Non modificare l'edizione di SQL Server. Il ripristino di un database del sito dall'edizione Standard all'edizione Enterprise non è supportato.

Altri requisiti di configurazione di SQL Server:

- SQL Server non può essere impostato sulla **modalità utente singolo**.
- Verificare che i file MDF e LDF siano validi. Quando si ripristina un sito, non viene eseguita alcuna verifica dello stato dei file.  

### <a name="sql-server-always-on-availability-groups"></a>Gruppi di disponibilità Always On di SQL Server

Se si usano i gruppi di disponibilità Always On di SQL Server per ospitare il database del sito, modificare i piani di ripristino come descritto in [Prepararsi all'uso di SQL Server Always On](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#changes-for-site-recovery).

### <a name="database-replicas"></a>Repliche di database

Dopo aver ripristinato un database del sito configurato per le repliche di database, riconfigurare ogni replica. Prima di poter usare le repliche di database, ricreare sia le pubblicazioni che le sottoscrizioni.

## <a name="determine-your-recovery-options"></a>Determinare le opzioni di ripristino

Ci sono due aree principali da tenere in considerazione per il ripristino del sito di amministrazione centrale e del server del sito primario di Configuration Manager: il **server del sito** e il **database del sito**.
Le sezioni seguenti consentono di selezionare le opzioni migliori per lo scenario di ripristino.

> [!NOTE]  
> Quando il programma di installazione di Configuration Manager rileva la presenza di un sito sul server, è possibile avviare un ripristino del sito, nonostante le opzioni di ripristino per il server del sito siano limitate. Ad esempio, se si esegue il programma di installazione su un server del sito esistente, scegliendo l'operazione di ripristino è possibile recuperare il server di database del sito, ma l'opzione di ripristino del server del sito è disabilitata.

### <a name="site-server-recovery-options"></a>Opzioni di ripristino del server del sito

Avviare l'installazione di Configuration Manager da una copia della cartella **CD.Latest** creata esternamente alla cartella di installazione di Configuration Manager.  

- Se si esegue il programma di installazione dal menu **Start** sul server del sito, l'opzione **Ripristina un sito** non sarà disponibile.  

- Se sono stati installati aggiornamenti dalla console di Configuration Manager prima di aver eseguito il backup, non è possibile reinstallare il sito usando il programma di installazione dalle posizioni seguenti:

  - Supporti di installazione
  - Percorso di installazione di Configuration Manager

Selezionare quindi l'opzione **Ripristina un sito**. Sono disponibili le seguenti opzioni di ripristino per il server del sito in cui si è verificato un errore:  

#### <a name="recover-the-site-server-using-an-existing-backup"></a>Ripristina il server di sito utilizzando un backup esistente

Usare questa opzione quando si ha un backup di Configuration Manager del server del sito da prima che si verificasse l'errore del sito. Il sito crea questo backup durante l'attività di manutenzione **Backup server sito**. Il sito viene reinstallato e vengono configurate le relative impostazioni in base al sito di cui era stato eseguito il backup.  

#### <a name="reinstall-the-site-server"></a>Reinstallare il server del sito

Usare questa opzione se non si ha un backup del server del sito. Il server del sito viene reinstallato ed è necessario specificare le impostazioni del sito come nella procedura di installazione iniziale.  

- Usare lo stesso codice del sito e nome del database del sito usati durante l'installazione iniziale del sito in cui si è verificato l'errore.  

- È possibile reinstallare il sito in un nuovo computer che esegue una nuova versione del sistema operativo.  

- Il server deve usare lo stesso nome host e lo stesso nome di dominio completo (FQDN) del server del sito originale.

### <a name="site-database-recovery-options"></a>Opzioni di ripristino del database del sito

Quando si esegue il programma di installazione di Configuration Manager, sono disponibili le opzioni di ripristino seguenti per il database del sito:  

#### <a name="recover-the-site-database-using-a-backup-set"></a>Recover the site database using a backup set (Ripristina il database del sito usando un set di backup)

Usare questa opzione quando si ha un backup di Configuration Manager del database del sito da prima che si verificasse l'errore del database. Il sito crea questo backup durante l'attività di manutenzione **Backup server sito**. In una gerarchia, quando si ripristina un sito primario, il processo di ripristino recupera dal sito di amministrazione centrale tutte le modifiche apportate al database del sito dopo l'ultimo backup. Quando si ripristina il sito di amministrazione centrale, il processo di ripristino recupera queste modifiche da un sito primario di riferimento. Quando si ripristina il database del sito per un sito primario autonomo, si perdono le modifiche apportate al sito dopo l'ultimo backup.  

Quando si ripristina il database del sito per un sito in una gerarchia, il comportamento di ripristino è differente per un sito di amministrazione centrale o un sito primario. Il comportamento è diverso anche quando l'ultimo backup è compreso o non compreso nel periodo di conservazione del rilevamento delle modifiche di SQL Server. Per altre informazioni, vedere la sezione [Scenari di ripristino del database del sito](#site-database-recovery-scenarios) in questo articolo.  

> [!NOTE]  
> Se si sceglie di ripristinare il database del sito usando un set di backup, ma il database del sito è già esistente, il ripristino non riesce.  

#### <a name="create-a-new-database-for-this-site"></a>Crea un nuovo database per il sito

Usare questa opzione se non si ha un backup del database del sito. In una gerarchia il processo di ripristino crea un nuovo database del sito. Quando ripristina un sito primario figlio, recupera i dati eseguendo la replica dal sito di amministrazione centrale. Quando ripristina il sito di amministrazione centrale, replica i dati da un sito primario di riferimento. Questa opzione non è disponibile quando si ripristina un sito primario autonomo o un sito di amministrazione centrale che non ha siti primari.  

#### <a name="use-a-site-database-that-has-been-manually-recovered"></a>Usa un database del sito ripristinato manualmente

Usare questa opzione quando è già stato eseguito il ripristino del database del sito di Configuration Manager, ma è necessario completare il processo di ripristino.  

- Configuration Manager può ripristinare il database del sito da uno qualsiasi dei processi seguenti:  

  - L'attività di manutenzione di backup di Configuration Manager  
  - Un backup del database del sito tramite Data Protection Manager (DPM)  
  - Un altro processo di backup  

    Dopo il ripristino del database del sito mediante un metodo esterno a Configuration Manager, eseguire il programma di installazione e selezionare questa opzione per completare il ripristino del database del sito.  

    > [!NOTE]  
    > Quando si usa DPM per il backup del database del sito, usare le procedure DPM per ripristinare il database del sito in una posizione specifica prima di continuare il processo di ripristino in Configuration Manager. Per altre informazioni su DPM, vedere la raccolta della documentazione di [Data Protection Manager](/system-center/dpm).  

- In una gerarchia, quando si recupera il database di un sito primario, il processo di ripristino recupera dal sito di amministrazione centrale tutte le modifiche apportate al database del sito dopo l'ultimo backup. Quando si ripristina il sito di amministrazione centrale, il processo di ripristino recupera queste modifiche da un sito primario di riferimento. Quando si ripristina il database del sito per un sito primario autonomo, si perdono le modifiche apportate al sito dopo l'ultimo backup.  

#### <a name="skip-database-recovery"></a>Ignorare il ripristino del database

Usare questa opzione quando non si è verificata alcuna perdita di dati nel server di database del sito di Configuration Manager. Questa opzione è valida solo quando il database del sito si trova in un computer diverso rispetto al server del sito che si vuole ripristinare.  

### <a name="sql-server-change-tracking-retention-period"></a>Periodo di memorizzazione del rilevamento modifiche di SQL Server

Configuration Manager consente il rilevamento delle modifiche per il database del sito in SQL Server. Il rilevamento delle modifiche consente a Configuration Manager di cercare le informazioni sulle modifiche apportate alle tabelle di database dopo un punto di ripristino precedente. Il periodo di conservazione specifica per quanto tempo verranno conservate le informazioni di rilevamento delle modifiche. Per impostazione predefinita, il database del sito è configurato per un periodo di conservazione di cinque giorni. Quando si ripristina un database del sito, il processo di ripristino viene eseguito in modo diverso a seconda che il backup rientri o meno nel periodo di memorizzazione. Se, ad esempio, nel server SQL si verifica un errore e l'ultimo backup risale a sette giorni fa, il backup non è compreso nel periodo di conservazione.

Per altre informazioni sui meccanismi interni di rilevamento delle modifiche di SQL Server, vedere i post di blog seguenti del team di SQL Server: [Change Tracking Cleanup - part 1](/archive/blogs/sql_server_team/change-tracking-cleanup-part-1) (Pulizia del rilevamento modifiche - parte 1) e [Change Tracking Cleanup - part 2](/archive/blogs/sql_server_team/change-tracking-cleanup-part-2) (Pulizia del rilevamento modifiche - parte 2).

### <a name="reinitialization-of-site-or-global-data"></a>Reinizializzazione dei dati globali o del sito

Il processo per reinizializzare i dati globali o i dati del sito sostituisce i dati esistenti nel database del sito con i dati di un altro database del sito. Quando ad esempio il sito ABC reinizializza i dati dal sito XYZ, vengono eseguiti i seguenti passaggi:

- I dati vengono copiati dal sito XYZ al sito ABC.
- I dati esistenti per il sito XYZ vengono rimossi dal database del sito nel sito ABC.
- I dati copiati dal sito XYZ vengono inseriti nel database del sito per il sito ABC.

#### <a name="example-scenario-1-the-primary-site-reinitializes-the-global-data-from-the-cas"></a>Scenario di esempio 1: il sito primario reinizializza i dati globali dal sito di amministrazione centrale.

Il processo di ripristino rimuove i dati globali esistenti per il sito primario nel database del sito primario e li sostituisce con i dati globali copiati dal sito di amministrazione centrale.

#### <a name="example-scenario-2-the-cas-reinitializes-the-site-data-from-a-primary-site"></a>Scenario di esempio 2: il sito di amministrazione centrale reinizializza i dati del sito da un sito primario

Il processo di ripristino rimuove i dati del sito esistenti per il sito primario nel database del sito di amministrazione centrale. Sostituisce i dati con i dati del sito copiati dal sito primario. I dati del sito per altri siti primari non sono interessati.

### <a name="site-database-recovery-scenarios"></a>Scenari di ripristino del database del sito

Dopo il ripristino di un database del sito da un backup, Configuration Manager prova a ripristinare le modifiche apportate nei dati globali e nei dati del sito dopo l'ultimo backup del database. Configuration Manager avvia le azioni seguenti dopo il ripristino del database del sito dal backup:  

#### <a name="recovered-site-is-a-cas"></a>Il sito ripristinato è un sito di amministrazione centrale

- Backup del database all'interno del periodo di memorizzazione del rilevamento delle modifiche  

  - **Dati globali**: le modifiche apportate ai dati globali in seguito al backup vengono replicate da tutti i siti primari.  

  - **Dati del sito**: le modifiche apportate ai dati del sito in seguito al backup vengono replicate da tutti i siti primari.  

- Backup del database antecedente al periodo di memorizzazione del rilevamento delle modifiche  

  - **Dati globali**: il sito di amministrazione centrale reinizializza i dati globali dal sito primario di riferimento, se specificato. Tutti gli altri siti primari reinizializzano quindi i dati globali dal sito di amministrazione centrale. Se non si specifica un sito di riferimento, tutti i siti primari reinizializzano quindi i dati globali dal sito di amministrazione centrale. Questi dati sono quelli ripristinati dal backup.  

  - **Dati del sito**: il sito di amministrazione centrale reinizializza i dati del sito da ogni sito primario.  

#### <a name="recovered-site-is-a-primary-site"></a>Il sito ripristinato è un sito primario

- Backup del database all'interno del periodo di memorizzazione del rilevamento delle modifiche  

  - **Dati globali**: le modifiche apportate ai dati globali in seguito al backup vengono replicate dal sito di amministrazione centrale.  

  - **Dati del sito**: il sito di amministrazione centrale reinizializza i dati del sito dal sito primario. Le modifiche apportate dopo il backup vanno perse. I client riscrivono la maggior parte dei dati quando inviano le informazioni al sito primario.  

- Backup del database antecedente al periodo di memorizzazione del rilevamento delle modifiche  

  - **Dati globali**: il sito primario reinizializza i dati globali dal sito di amministrazione centrale.  

  - **Dati del sito**: il sito di amministrazione centrale reinizializza i dati del sito dal sito primario. Le modifiche apportate dopo il backup vanno perse. I client riscrivono la maggior parte dei dati quando inviano le informazioni al sito primario.  

## <a name="site-recovery-procedures"></a>Procedure di ripristino del sito

Usare una delle procedure seguenti per ripristinare il server del sito e il database del sito:

### <a name="start-a-site-recovery-in-the-setup-wizard"></a>Avviare un ripristino sito nell'Installazione guidata

1. Copiare la cartella [CD.Latest](the-cd.latest-folder.md) in un percorso esterno alla cartella di installazione di Configuration Manager. Dalla copia della cartella CD.Latest eseguire l'Installazione guidata di Configuration Manager.  

2. Nella pagina **Riquadro attività iniziale** selezionare **Ripristina un sito** e quindi selezionare **Avanti**.  

3. Completare la procedura guidata usando le opzioni appropriate per il ripristino del sito.  

     - Durante il ripristino, il programma di installazione identifica la porta di SQL Server Service Broker (SSB) usata da SQL Server. Se questa impostazione della porta viene modificata durante il ripristino, la replica dei dati non verrà eseguita correttamente al termine del ripristino.  

     - È possibile specificare il percorso originale o uno nuovo da usare per l'installazione di Configuration Manager nell'Installazione guidata.  

### <a name="start-an-unattended-site-recovery"></a>Avviare un ripristino sito automatico

1. Preparare lo script di installazione automatica per le opzioni richieste per il ripristino del sito. Per altre informazioni, vedere [Ripristino automatico dei siti](unattended-recovery.md).  

2. Eseguire il programma di installazione di Configuration Manager con l'opzione della riga di comando `/script`. Si crea, ad esempio, un file di inizializzazione dell'installazione **ConfigMgrUnattend.ini**. Lo si salva nella directory `C:\Temp` del computer in cui si esegue l'installazione. Usare il comando seguente:  

    `setup.exe /script C:\temp\ConfigMgrUnattend.ini`  

> [!NOTE]  
> Dopo aver ripristinato un sito di amministrazione centrale, potrebbe non essere possibile stabilire la replica di alcuni dati del sito da siti figlio. Questi dati includono, tra gli altri, l'inventario hardware, l'inventario software e i messaggi di stato.
>
> Se si verifica questo problema, reinizializzare **ConfigMgrDRSSiteQueue** per la replica di database. Usare **SQL Server Manager** per eseguire la query riportata di seguito nel database del sito per il sito di amministrazione centrale:
>
> ``` SQL
> IF EXISTS (SELECT * FROM sys.service_queues WHERE name = 'ConfigMgrDRSSiteQueue' AND is_receive_enabled = 0)  
>  
> ALTER QUEUE [dbo].[ConfigMgrDRSSiteQueue] WITH STATUS = ON
> ```

## <a name="post-recovery-tasks"></a>Attività post-ripristino

Dopo aver eseguito il ripristino del sito, considerare alcune attività post-ripristino prima di completare il ripristino del sito. Usare le seguenti sezioni per completare il processo di ripristino del sito.

### <a name="reenter-user-account-passwords"></a>Immettere di nuovo le password account utente

Dopo un ripristino del server del sito, immettere nuovamente le password per tutti gli account utente nel sito. Queste password vengono reimpostate durante il ripristino del sito. Gli account vengono elencati nella pagina **Completato** dell'Installazione guidata dopo il completamento del ripristino sito. L'elenco viene salvato anche in `C:\ConfigMgrPostRecoveryActions.html` nel server del sito ripristinato.

#### <a name="reenter-user-account-passwords-after-site-recovery"></a>Immettere nuovamente le password account utente dopo il ripristino del sito

1. Aprire la console di Configuration Manager e connettersi al sito ripristinato.  

2. Andare all'area di lavoro **Amministrazione**, espandere **Sicurezza** e quindi selezionare **Account**.  

3. Per ogni account, seguire questa procedura per immette nuovamente la password:  

     1. Selezionare l'account dall'elenco identificato dopo il ripristino sito.  

     2. Nella barra multifunzione selezionare **Proprietà**.  

     3. Nella scheda **Generale** selezionare **Imposta** e quindi immettere nuovamente la password per l'account.  

     4. Selezionare **Verifica**, scegliere l'origine dati appropriata per l'account utente selezionato e quindi selezionare **Verifica connessione**. Questo passaggio consente di controllare che l'account utente possa connettersi all'origine dati e verifica le credenziali.  

     5. Selezionare **OK** per salvare le modifiche alla password e quindi selezionare **OK** per chiudere la pagina delle proprietà dell'account.  

#### <a name="reenter-pxe-passwords"></a>Immettere nuovamente le password PXE

<!-- SCCMDocs#1683 -->

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione** e selezionare il nodo **Punti di distribuzione**. Tutti i punti di distribuzione locali con **Sì** nella colonna **PXE** supportano PXE ed è possibile che sia necessario immettere nuovamente la password.

1. Selezionare il punto di distribuzione che supporta PXE e selezionare **Proprietà** nella barra multifunzione.

1. Passare alla scheda **PXE**.

1. Se è abilitata l'opzione **Richiedi password quando i computer utilizzano PXE**, immettere e confermare la password.

1. Selezionare **OK** per salvare e chiudere le proprietà.

Ripetere questo processo per qualsiasi altro punto di distribuzione locale che supporta PXE.

#### <a name="reenter-task-sequence-passwords"></a>Immettere nuovamente le password della sequenza di attività

<!-- SCCMDocs#1683 -->

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**, espandere **Sistemi operativi** e selezionare il nodo **Sequenze di attività**.

1. Selezionare una sequenza di attività e quindi selezionare **Modifica** nella barra multifunzione.

1. Per immettere nuovamente le password, vedere i passaggi seguenti:

    - **Applica impostazioni Windows**: se si abilita e si specifica la password dell'amministratore locale, immettere nuovamente e confermare la password.

    - **Applica impostazioni di rete**: per l'account con le autorizzazioni per l'aggiunta al dominio selezionare **Imposta**. Immettere e confermare la password e quindi selezionare **Verifica**.

    - **Acquisisci immagine del sistema operativo**: per l'account usato per accedere alla destinazione selezionare **Imposta**. Immettere e confermare la password e quindi selezionare **Verifica**.

    - **Connetti alla cartella di rete**: per l'account usato per la connessione a una cartella di rete selezionare **Imposta**. Immettere e confermare la password e quindi selezionare **Verifica**.

    - **Attiva BitLocker**: se si usa l'opzione di gestione delle chiavi **TPM e PIN**, immettere nuovamente il PIN.

    - **Aggiunta a dominio o gruppo di lavoro**: per l'account con le autorizzazioni per l'aggiunta al dominio selezionare **Imposta**. Immettere e confermare la password e quindi selezionare **Verifica**.

    - **Esegui riga di comando**: se si usa l'opzione **Esegui questo passaggio come account specificato**, selezionare **Imposta**. Immettere e confermare la password e quindi selezionare **Verifica**.

    - **Esegui script PowerShell**: se si usa l'opzione **Esegui questo passaggio come account specificato**, selezionare **Imposta**. Immettere e confermare la password e quindi selezionare **Verifica**.

Ripetere questo processo per tutte le sequenze di attività.

### <a name="recreate-bootable-media-and-prestaged-media-in-non-pki-environments"></a>Ricreare supporti di avvio e supporti pre-installati in ambienti non PKI

Negli ambienti non PKI, i certificati autofirmati in supporti di avvio e supporti pre-installati si basano sulle chiavi di computer del server in cui è stato creato il supporto. Per questo motivo, se l'hardware viene modificato o il sistema operativo viene reinstallato nell'ambito di un ripristino, è necessario creare nuovamente tutti i supporti di avvio e i supporti pre-installati creati in tale server. Per altre informazioni su come creare supporti di avvio e pre-installati, vedere [Creare supporti di avvio](../../../osd/deploy-use/create-bootable-media.md) e [Creare supporti pre-installati](../../../osd/deploy-use/create-prestaged-media.md).

### <a name="reenter-sideloading-keys"></a>Immettere nuovamente le chiavi di sideload

Dopo un ripristino del server del sito, immettere nuovamente le chiavi di sideload di Windows specificate per il sito. Queste chiavi vengono reimpostate durante il ripristino sito. Dopo aver immesso nuovamente le chiavi di sideload, il sito reimposta il conteggio nella colonna **Attivazioni usate** per le chiavi di sideload di Windows.

Ad esempio, prima dell'errore del sito il conteggio **Attivazioni totali** è pari a **100**. Il numero di chiavi usate dal dispositivo, indicato in **Attivazioni utilizzate**, è pari a **90**. Dopo il ripristino del sito, il valore **Attivazioni totali** visualizza ancora **100**, ma la colonna **Attivazioni usate** visualizza erroneamente **0**. Successivamente all'uso da parte di 10 nuovi dispositivi di una chiave di sideload, non esistono più chiavi di sideload e per l'undicesimo dispositivo non sarà possibile applicare una chiave di sideload.

### <a name="recreate-azure-services"></a>Ricreare i servizi di Azure

<!-- SCCMDocs#1022 -->

In Configuration Manager versione 1806, dopo il ripristino del sito verrà visualizzato l'errore seguente nel file cloudmgr.log:

`Index (zero-based) must be greater than or equal to zero`

Per risolvere questo problema, [Rinnovare la chiave privata](../deploy/configure/azure-services-wizard.md#bkmk_renew) per ogni connessione al tenant di Azure.

### <a name="configure-ssl-for-site-system-roles-that-use-iis"></a>Configurare SSL per i ruoli del sistema del sito che usano IIS

Quando si ripristinano sistemi del sito che eseguono IIS e che erano configurati per HTTPS, riconfigurare IIS per usare il certificato del server Web.

### <a name="reinstall-hotfixes"></a>Reinstallare gli aggiornamenti rapidi

Dopo il ripristino di un sito, è necessario reinstallare gli [aggiornamenti rapidi fuori banda](updates.md#bkmk_outofband) applicati al server del sito. Dopo il ripristino sito, visualizzare l'elenco degli aggiornamenti rapidi installati in precedenza nella pagina **Completato** dell'Installazione guidata. Questo elenco viene salvato anche in `C:\ConfigMgrPostRecoveryActions.html` nel server del sito ripristinato.

### <a name="recover-custom-reports"></a>Recuperare i report personalizzati

Alcuni clienti creano report personalizzati in SQL Server Reporting Services. Quando si verifica un errore in questo componente, recuperare i report da un backup del server di report. Per altre informazioni sul ripristino dei report personalizzati in Reporting Services, vedere [Operazioni di backup e ripristino per Reporting Services](/sql/reporting-services/install-windows/backup-and-restore-operations-for-reporting-services).

### <a name="recover-content-files"></a>Ripristinare i file di contenuto

Il database del sito tiene traccia di dove il server del sito archivia i file di contenuto. I file di contenuto in sé non sono sottoposti a backup o ripristino durante il processo di backup e ripristino. Per eseguire il ripristino completo dei file di contenuto, ripristinare i file di origine del pacchetto e la raccolta contenuto nel percorso originale. Esistono diversi metodi per ripristinare i file di contenuto. Il metodo più semplice consiste nel ripristinare i file da un backup del file system del server del sito.

Se non si ha un backup del file system per i file di origine pacchetto, copiarli o scaricarli manualmente. Questo processo è simile a quando si è creato il pacchetto in origine. Eseguire la query seguente in SQL Server per trovare il percorso di origine del pacchetto per tutti i pacchetti e le applicazioni: `SELECT * FROM v_Package`. Identificare il sito di origine del pacchetto esaminando i primi tre caratteri dell'ID di pacchetto. Ad esempio, se l'ID del pacchetto è CEN00001, il codice del sito per il sito di origine è CEN. I file di origine del pacchetto devono essere ripristinati nella stessa posizione in cui si trovavano prima dell'errore.

Se non si ha un backup del file system che includa la raccolta contenuto, eseguire una delle seguenti opzioni di ripristino:  

- **Importare un file di contenuti in versione di preproduzione**: in una gerarchia di Configuration Manager è possibile creare un file di contenuti in versione di preproduzione con tutti i pacchetti e le applicazioni da un altro percorso. Importare quindi il file di contenuti in versione di preproduzione per ripristinare la raccolta contenuto nel server del sito.  

- **Aggiornare il contenuto**: Configuration Manager copia il contenuto dall'origine del pacchetto alla raccolta contenuto. Per completare correttamente questa azione, è necessario che i file origine pacchetto siano disponibili nel percorso originale. Eseguire questa azione in ogni pacchetto e applicazione.

### <a name="recover-custom-software-updates"></a>Ripristinare gli aggiornamenti software personalizzati

Quando sono stati inclusi i file di database di System Center Updates Publisher nel piano di backup, è possibile ripristinare i database in caso di errore del computer Updates Publisher. Per altre informazioni su System Center Updates Publisher, vedere [System Center Updates Publisher](../../../sum/tools/updates-publisher.md).

#### <a name="restore-the-updates-publisher-database"></a>Ripristinare il database Updates Publisher

1. Reinstallare Updates Publisher nel computer ripristinato.  

2. Copiare il file di database **Scupdb.sdf** dalla destinazione di backup a `%USERPROFILE%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\` nel computer che esegue Updates Publisher.  

3. Quando più utenti eseguono Updates Publisher nel computer, copiare ogni file di database nel percorso del profilo utente appropriato.  

### <a name="user-state-migration-data"></a>Dati di migrazione sullo stato utente

Come parte delle proprietà del punto di migrazione stato, è possibile specificare le cartelle in cui vengono archiviati i dati dello stato utente. Dopo aver ripristinato un punto di migrazione stato, ripristinare manualmente i dati dello stato utente nel server. Ripristinarli nelle stesse cartelle in cui erano archiviati i dati prima dell'errore.

### <a name="regenerate-the-certificates-for-distribution-points"></a>Rigenerare i certificati per i punti di distribuzione

Dopo aver ripristinato un sito, **distmgr.log** potrebbe elencare la voce seguente per uno o più punti di distribuzione: `Failed to decrypt cert PFX data`. Questa voce indica che i dati del certificato del punto di distribuzione non possono essere decrittografati dal sito. Per risolvere questo problema, rigenerare o reimportare il certificato per i punti di distribuzione interessati. Usare il cmdlet[Set-CMDistributionPoint](/powershell/module/configurationmanager/set-cmdistributionpoint) di PowerShell.

### <a name="update-certificates-used-for-cloud-based-distribution-points"></a>Aggiornare i certificati usati per i punti di distribuzione basati sul cloud

Configuration Manager richiede un certificato di gestione di Azure per la comunicazione dal server del sito con i punti di distribuzione basati sul cloud. Dopo un ripristino del sito, aggiornare i certificati per i punti di distribuzione basati sul cloud.

## <a name="recover-a-secondary-site"></a>Ripristinare un sito secondario

Configuration Manager non supporta il backup del database in un sito secondario, ma supporta il ripristino mediante reinstallazione del sito secondario. Il ripristino del sito secondario è necessario quando si verifica un errore del sito secondario di Configuration Manager.

### <a name="requirements"></a>Requisiti

- Il server deve soddisfare tutti i prerequisiti del sito secondario e deve avere i diritti di sicurezza appropriati configurati.  

- Usare lo stesso percorso di installazione usato per il sito in cui si è verificato l'errore.  

- Usare un server con la stessa configurazione del server in cui si è verificato l'errore. Questa configurazione include il nome di dominio completo (FQDN).  

- Il server deve avere la stessa configurazione di SQL Server del sito in cui si è verificato l'errore.  

  - Durante il ripristino di un sito secondario, Configuration Manager non installa SQL Server Express, se questo non è già installato nel computer.  

  - Usare la stessa versione di SQL Server e la stessa istanza di SQL Server usate per il database del sito secondario prima dell'errore.  

### <a name="procedure"></a>Procedura

Usare l'azione **Ripristina sito secondario** dal nodo **Siti** nella console di Configuration Manager. A differenza di altri tipi di siti, il ripristino di un sito secondario non usa un file di backup. Questo processo reinstalla i file del sito secondario nel server in cui si è verificato l'errore. Dopo la reinstallazione del sito, i dati del sito secondario vengono reinizializzati dal sito primario padre.

Durante il processo di ripristino, Configuration Manager verifica se la raccolta contenuto esiste nel server del sito secondario. Controlla anche che il contenuto appropriato sia disponibile. Il sito secondario usa la raccolta contenuto esistente, se questa include il contenuto appropriato. In caso contrario, per ripristinare la raccolta contenuto di un sito secondario, ridistribuire o pre-installare il contenuto nel server.

Quando si ha un punto di distribuzione che non si trova nel server del sito secondario, non è necessario reinstallare il punto di distribuzione durante un ripristino del sito secondario. Dopo il ripristino del sito secondario il sito si sincronizza automaticamente con il punto di distribuzione.

È possibile verificare lo stato del sito secondario usando l'azione **Mostra stato installazione** dal nodo **Siti** nella console di Configuration Manager.