---
title: Configurare i gruppi di disponibilità
titleSuffix: Configuration Manager
description: Configurare e gestire i gruppi di disponibilità Always On di SQL Server con Configuration Manager
ms.date: 09/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7e4ec207-bb49-401f-af1b-dd705ecb465d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2e85b36d0caeb6ceb99f56220e271774dc0db0f6
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699246"
---
# <a name="configure-sql-server-always-on-availability-groups-for-configuration-manager"></a>Configurare gruppi di disponibilità Always On di SQL Server con Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Le informazioni contenute in questo articolo consentono di configurare e gestire i gruppi di disponibilità usati con Configuration Manager.

Prima di iniziare:  

- Acquisire familiarità con le informazioni contenute in [Prepararsi a usare i gruppi di disponibilità Always On di SQL Server con Configuration Manager](sql-server-alwayson-for-a-highly-available-site-database.md).
- Acquisire familiarità con la documentazione di SQL Server relativa all'uso dei gruppi di disponibilità e alle procedure correlate. Tali informazioni sono necessarie per completare gli scenari seguenti.


## <a name="create-and-configure-an-availability-group"></a><a name="bkmk_create"></a> Creare e configurare un gruppo di disponibilità

Adottare la procedura seguente per creare un gruppo di disponibilità e quindi spostare una copia del database del sito nel gruppo di disponibilità creato.

1. Usare il comando seguente per arrestare il sito di Configuration Manager:

    `preinst.exe /stopsite`

    Per altre informazioni, vedere [Strumento di manutenzione gerarchia](../../manage/hierarchy-maintenance-tool-preinst.exe.md).

2. Modificare il modello di backup per il database del sito da **SIMPLE** a **FULL**:

    ```sql
    ALTER DATABASE [CM_xxx] SET RECOVERY FULL;
    ```

    I gruppi di disponibilità supportano solo il modello di backup FULL. Per altre informazioni, vedere [Visualizzare o modificare il modello di recupero di un database](/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server).

3. Usare SQL Server per creare un backup completo del database del sito. Scegliere una delle seguenti opzioni:

    - **Sarà membro del gruppo di disponibilità**: se si usa questo server come membro di replica primaria iniziale del gruppo di disponibilità, non è necessario ripristinare una copia del database del sito in questo server o in un altro presente nel gruppo. Il database è già incluso nella replica primaria. SQL Server replica il database nelle repliche secondarie durante un passaggio successivo.  

    - **Non sarà membro del gruppo di disponibilità**: Ripristinare una copia del database del sito nel server che ospiterà la replica primaria del gruppo.

    Per altre informazioni, vedere gli articoli seguenti nella documentazione di SQL Server:

    - [Creare un backup completo del database](/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server)
    - [Ripristinare un backup del database tramite SSMS](/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)

    > [!NOTE]  
    > Se si prevede di passare da un gruppo di disponibilità a una versione autonoma in una replica esistente, rimuovere prima il database dal gruppo di disponibilità.

4. Nel server che ospiterà la replica primaria iniziale del gruppo usare la [Creazione guidata gruppo di disponibilità](/sql/database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio) per creare il gruppo di disponibilità. Nella procedura guidata:

    - Nella pagina **Seleziona database** selezionare il database per il sito di Configuration Manager.  

    - Nella pagina **Specifica repliche** configurare:

        - **Repliche**: specificare i server che ospiteranno le repliche secondarie.

        - **Listener**: specificare il **Nome DNS del listener** come nome DNS completo, ad esempio `<listener_server>.fabrikam.com`. Quando si configura Configuration Manager per l'uso del database nel gruppo di disponibilità, verrà usato questo nome.

    - Nella pagina **Seleziona sincronizzazione dati iniziale** selezionare **Completa**. Dopo avere creato il gruppo di disponibilità, la procedura guidata esegue il backup del database primario e del log delle transazioni, quindi li ripristina in ogni server che ospita una replica secondaria.

        > [!Note]  
        > Se non si usa questo passaggio, ripristinare una copia del database del sito in ogni server che ospita una replica secondaria. Quindi aggiungere manualmente il database al gruppo.

5. Controllare la configurazione in ogni replica:

    1. Verificare che l'account computer del server del sito sia un membro del gruppo **Administrators** locale in tutti i computer membri del gruppo di disponibilità.  

    2. Eseguire lo [script di verifica](sql-server-alwayson-for-a-highly-available-site-database.md#prerequisites) per assicurarsi che il database del sito in ogni replica sia configurato correttamente.

    3. Se è necessario impostare le configurazioni nelle repliche secondarie, prima di continuare, eseguire il failover manuale della replica primaria nella replica secondaria. È possibile configurare solo il database di una replica primaria. Per altre informazioni, vedere [Eseguire un failover manuale pianificato di un gruppo di disponibilità](/sql/database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server) nella documentazione di SQL Server.

6. Quando tutte le repliche soddisfano i requisiti, il gruppo di disponibilità è pronto per essere usato con Configuration Manager.


## <a name="configure-a-site-to-use-the-availability-group"></a><a name="bkmk_configure"></a> Configurare un sito per l'uso del gruppo di disponibilità

Dopo aver [creato e configurato il gruppo di disponibilità](#bkmk_create), usare la funzione di manutenzione del sito di Configuration Manager per configurare il sito affinché usi il database ospitato dal gruppo di disponibilità.

L'installazione di un nuovo sito con il proprio database in un gruppo di disponibilità non è supportata. Se, ad esempio, si usano i supporti di base, installare il sito usando una singola istanza di SQL Server. Dopo aver completato l'installazione, spostare il database del sito nel gruppo di disponibilità.

1. Eseguire il **programma di installazione di Configuration Manager**`\BIN\X64\setup.exe` dalla cartella di installazione del sito di Configuration Manager.

2. Nella pagina **Riquadro attività iniziale** selezionare **Esegui una manutenzione del sito o reimposta il sito** e quindi scegliere **Avanti**.

3. Selezionare **Modifica la configurazione di SQL Server** e quindi scegliere **Avanti**.

4. Riconfigurare le impostazioni seguenti per il database del sito:

    - **Nome SQL Server**: immettere il nome virtuale per il *listener* del gruppo di disponibilità. Il listener è stato configurato al momento della creazione del gruppo di disponibilità. Il nome virtuale deve essere un nome DNS completo, ad esempio `<Listener_Server>.fabrikam.com`.  

    - **Istanza**: per specificare l'istanza predefinita per il *listener* del gruppo di disponibilità, questo valore deve essere vuoto. Se il database del sito corrente viene eseguito in un'istanza denominata, cancellare l'istanza denominata corrente.

    - **Database**: non modificare il nome visualizzato. Questo nome è il database del sito corrente.

5. Dopo aver specificato le informazioni per il nuovo percorso del database, completare l'installazione con il processo e le configurazioni normali.


## <a name="synchronous-replica-members"></a><a name="bkmk_sync"></a> Membri di replica sincrona  

Se il database del sito è ospitato in un gruppo di disponibilità, usare le procedure seguenti per aggiungere o rimuovere membri di replica sincrona. Per altre informazioni sul tipo e sul numero di repliche supportate, vedere [Configurazioni dei gruppi di disponibilità](sql-server-alwayson-for-a-highly-available-site-database.md#availability-group-configurations).

### <a name="add-a-new-synchronous-replica-member"></a><a name="bkmk_sync-add"></a> Aggiungere un nuovo membro di replica sincrona

<!--3127336-->
A partire dalla versione 1906, eseguire l'installazione di Configuration Manager per aggiungere un nuovo membro di replica sincrona.

1. Aggiungere una replica secondaria usando le procedure di SQL Server.

    1. [Aggiungere una replica secondaria a un gruppo di disponibilità Always On](/sql/database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server).

    1. Controllare lo stato in SQL Management Studio. Attendere che il gruppo di disponibilità torni allo stato di integrità completa.

1. Eseguire l'installazione di Configuration Manager e selezionare l'opzione per modificare il sito.

1. Specificare il nome del listener del gruppo di disponibilità come nome del database. Se il listener usa una porta di rete non standard, specificare anche quella. In questo modo l'installazione verificherà che ogni nodo sia configurato in modo appropriato. Viene anche avviato un processo di ripristino del database.

L'installazione di Configuration Manager usa l'operazione di spostamento del database SQL e verifica che i nodi siano configurati correttamente.

Per altre informazioni sull'esecuzione manuale di questo processo nella versione 1902 o precedenti, vedere [ConfigMgr 1702: Adding a new node (Secondary Replica) to an existing SQL AO AG](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-1702-adding-a-new-node-secondary-replica-to-an/ba-p/339960) (ConfigMgr 1702: Aggiungere un nuovo nodo (replica secondaria) a un gruppo di disponibilità SQL AlwaysOn esistente).

### <a name="remove-a-replica-member"></a>Rimuovere un membro di replica

A partire dalla versione 1906 è possibile usare l'installazione di Configuration Manager per rimuovere un membro di replica. Usare lo stesso processo descritto in [Aggiungere un nuovo membro di replica sincrona](#bkmk_sync-add).

Per altre informazioni sull'esecuzione manuale di questo processo nella versione 1902 o precedenti, vedere [Rimuovere una replica secondaria da un gruppo di disponibilità](/sql/database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server).  


## <a name="asynchronous-replicas"></a><a name="bkmk_async"></a> Repliche asincrone

Nel gruppo di disponibilità usato con Configuration Manager è possibile usare una replica asincrona. Non è necessario eseguire gli script di configurazione richiesti per configurare una replica sincrona perché la replica asincrona non è supportata per il database del sito.

### <a name="configure-an-asynchronous-commit-replica"></a>Configurare una replica con commit asincrono

Per altre informazioni, vedere [Aggiungere una replica secondaria a un gruppo di disponibilità](/sql/database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server).

### <a name="use-the-asynchronous-replica-to-recover-your-site"></a>Usare la replica asincrona per il ripristino del sito

Usare la replica asincrona per il ripristino del database del sito.

1. Arrestare il sito primario attivo per impedire altre operazioni di scrittura nel database del sito. A questo scopo, usare lo [strumento di manutenzione gerarchia](../../manage/hierarchy-maintenance-tool-preinst.exe.md): `preinst.exe /stopsite`

1. Dopo aver arrestato il sito, usare la replica asincrona anziché un [database ripristinato manualmente](../../manage/recover-sites.md#use-a-site-database-that-has-been-manually-recovered).


## <a name="stop-using-an-availability-group"></a><a name="bkmk_stop"></a> Interrompere l'uso di un gruppo di disponibilità

Usare la procedura seguente se non si vuole più ospitare il database del sito in un gruppo di disponibilità. Con questo processo, il database del sito viene riportato in una istanza singola di SQL Server.

1. Usare il comando seguente per arrestare il sito di Configuration Manager: `preinst.exe /stopsite`. Per altre informazioni, vedere [Strumento di manutenzione gerarchia](../../manage/hierarchy-maintenance-tool-preinst.exe.md).

2. Usare SQL Server per creare un backup completo del database del sito dalla replica primaria. Per altre informazioni, vedere [Creare un backup completo del database](/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server).

3. Usare SQL Server per ripristinare il backup del database del sito nel server che ospiterà il database del sito. Per altre informazioni, vedere [Ripristinare un backup del database tramite SSMS](/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms).

    > [!Note]  
    > Se il server di replica primaria del gruppo di disponibilità ospiterà l'istanza singola del database del sito, ignorare questo passaggio.

4. Nel server che ospiterà il database del sito, modificare il modello di backup per il database del sito da **FULL** a **SIMPLE**. Per altre informazioni, vedere [Visualizzare o modificare il modello di recupero di un database](/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server).

5. Eseguire il **programma di installazione di Configuration Manager**`\BIN\X64\setup.exe` dalla cartella di installazione del sito di Configuration Manager.

6. Nella pagina **Riquadro attività iniziale** selezionare **Esegui una manutenzione del sito o reimposta il sito** e quindi scegliere **Avanti**.  

7. Selezionare **Modifica la configurazione di SQL Server** e quindi scegliere **Avanti**.  

8. Riconfigurare le impostazioni seguenti per il database del sito:

    - **Nome server SQL:** immettere il nome del server che ora ospita il database del sito.

    - **Istanza**: specificare l'istanza denominata che ospita il database del sito. Se il database si trova nell'istanza predefinita, lasciare vuoto questo campo.

    - **Database**: non modificare il nome visualizzato. Questo nome è il database del sito corrente.

9. Dopo aver specificato le informazioni per il nuovo percorso del database, completare l'installazione con il processo e le configurazioni normali. Al termine dell'installazione, il sito viene riavviato e inizia a usare il nuovo percorso del database.

10. Per pulire i server che erano membri del gruppo di disponibilità, seguire le indicazioni riportate in [Rimuovere un gruppo di disponibilità](/sql/database-engine/availability-groups/windows/remove-an-availability-group-sql-server).