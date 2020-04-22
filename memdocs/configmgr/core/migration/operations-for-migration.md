---
title: Operazioni di migrazione
titleSuffix: Configuration Manager
description: Creare ed eseguire processi per la migrazione di dati e client a Configuration Manager Current Branch.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c28e3492-851a-40fc-ba13-67ebc2d8b41a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a93269fc50c7bb39cd47f10e448d30742fc8ab22
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704569"
---
# <a name="operations-for-migrating-to-configuration-manager-current-branch"></a>Operazioni per la migrazione a Configuration Manager Current Branch

*Si applica a: Configuration Manager (Current Branch)*

Per la migrazione in Configuration Manager, è possibile eseguire la migrazione di dati e client dopo aver raccolto correttamente i dati da un sito di origine in una gerarchia di origine supportata. Usare le informazioni nelle sezioni seguenti per creare ed eseguire i processi di migrazione per la migrazione di dati, client e quindi completare il processo di migrazione.  

-   [Creare e modificare i processi di migrazione](#Create_Edit_migration_Jobs)  

-   [Eseguire i processi di migrazione](#Run_Migration_Jobs)  

-   [Aggiornare o riassegnare un punto di distribuzione condiviso](#BKMK_ProcUpgrdSS)  

-   [Monitorare l'attività di migrazione nell'area di lavoro Migrazione](#Monitor_MIgration)  

-   [Eseguire la migrazione dei client](#BKMK_MigrateClients)  

-   [Completare la migrazione](#Complete_Migration)  

##  <a name="create-and-edit-migration-jobs"></a><a name="Create_Edit_migration_Jobs"></a> Creare e modificare i processi di migrazione  
 Usare le procedure seguenti per creare processi di migrazione dei dati, modificare l'elenco di esclusione per i processi di migrazione basati su raccolte, configurare i punti di distribuzione condivisi e modificare le pianificazioni dei processi di migrazione.  

> [!NOTE]  
>  La procedura seguente per la creazione di un processo di migrazione, che esegue la migrazione per raccolte, è applicabile solo alle gerarchie di origine che eseguono una versione supportata di Configuration Manager 2007. Il tipo di processo di migrazione basato su raccolte non è disponibile quando si esegue la migrazione da una gerarchia di origine di System Center 2012 Configuration Manager o Configuration Manager Current Branch.  

#### <a name="create-a-migration-job-to-migrate-by-collections"></a>Creare un processo di migrazione per eseguire la migrazione per raccolte  

1.  Nella console di Configuration Manager scegliere **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** espandere **Migrazione**e quindi scegliere **Processi di migrazione**.  

3.  Nella scheda **Home**, nel gruppo **Crea**, scegliere **Crea processo di migrazione**.  

4.  Nella pagina **Generale** della Creazione guidata del processo di migrazione configurare gli elementi seguenti e quindi scegliere **OK**:  

    -   Specificare un nome per il processo di migrazione.  

    -   Nell'elenco a discesa **Tipo di processo** selezionare **Migrazione raccolta**.  

5.  Nella pagina **Seleziona raccolte** configurare gli elementi seguenti e quindi fare clic su **Avanti**:  

    -   Selezionare le raccolte da migrare.  

    -   Per migrare solo le raccolte e non gli oggetti associati a tali raccolte, deselezionare **Esegui la migrazione degli oggetti associati alle raccolte specificate** . Se si deseleziona questa opzione, in questo processo non verrà eseguita la migrazione di alcun oggetto associato ed è possibile ignorare i passaggi 6 e 7.  

6.  Nella pagina **Seleziona oggetti** deselezionare tutti i tipi di oggetto oppure specifici oggetti disponibili di cui non si vuole eseguire la migrazione. Per impostazione predefinita, vengono selezionati tutti gli oggetti disponibili e tutti i tipi di oggetto associati. Scegliere **Avanti**.  

7.  Nella pagina **Proprietà contenuto** assegnare la proprietà del contenuto da ciascun sito di origine elencato a un sito nella gerarchia di destinazione e quindi scegliere **Avanti**.  

8.  Nella pagina **Ambito di protezione** selezionare uno o più ambiti di protezione dell'amministrazione basata su ruoli da assegnare agli oggetti di cui eseguire la migrazione in questo processo e quindi scegliere **Avanti**.  

9. Nella pagina **Limitazione della raccolta** configurare una raccolta dalla gerarchia di destinazione per limitare l'ambito di ogni raccolta elencata e quindi scegliere **Avanti**. In assenza di raccolte elencate scegliere **Avanti**.  

10. Nella pagina **Sostituzione dei codici del sito** assegnare un codice del sito dalla gerarchia di destinazione per sostituire il codice del sito di Configuration Manager 2007 per ogni raccolta elencata e quindi scegliere **Avanti**. In assenza di raccolte elencate scegliere **Avanti**.  

11. Nella pagina **Riesamina informazioni** scegliere **Salva nel file** per salvare le informazioni per poterle visualizzare in seguito. Quando si è pronti per continuare scegliere **Avanti**.  

12. Nella pagina **Impostazioni** configurare il momento in cui eseguire il processo di migrazione ed eventuali impostazioni aggiuntive necessarie per questo processo di migrazione, quindi scegliere **Avanti**.  

13. Confermare le impostazioni e completare la procedura guidata.  

#### <a name="create-a-migration-job-to-migrate-by-objects"></a>Creare un processo di migrazione per eseguire la migrazione per oggetti  

1.  Nella console di Configuration Manager scegliere **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** espandere **Migrazione**e quindi scegliere **Processi di migrazione**.  

3.  Nella scheda **Home**, nel gruppo **Crea**, scegliere **Crea processo di migrazione**.  

4.  Nella pagina **Generale** della Creazione guidata del processo di migrazione configurare gli elementi seguenti e quindi scegliere **Avanti**:  

    -   Specificare un nome per il processo di migrazione.  

    -   Nell'elenco a discesa **Tipo di processo** selezionare **Migrazione oggetti**.  

5.  Nella pagina **Seleziona oggetti** selezionare i tipi di oggetto da migrare. Per impostazione predefinita, vengono selezionati tutti gli oggetti disponibili per ogni tipo di oggetto selezionato.  

6.  Nella pagina **Proprietà contenuto** assegnare la proprietà del contenuto da ciascun sito di origine elencato a un sito nella gerarchia di destinazione e quindi scegliere **Avanti**. Se non è elencato alcuna sito di origine scegliere **Avanti**.  

7.  Nella pagina **Ambito di protezione** selezionare uno o più ambiti di protezione dell'amministrazione basata su ruoli da assegnare agli oggetti in questo processo di migrazione e quindi scegliere **Avanti**.  

8.  Nella pagina **Riesamina informazioni** scegliere **Salva nel file** per salvare le informazioni per poterle visualizzare in seguito. Quando si è pronti per continuare scegliere **Avanti**.  

9. Nella pagina **Impostazioni** configurare il momento in cui eseguire la migrazione ed eventuali impostazioni aggiuntive necessarie per questo processo di migrazione. Scegliere quindi **Avanti**.  

10. Confermare le impostazioni e completare la procedura guidata.  

#### <a name="create-a-migration-job-to-migrate-changed-objects"></a>Creare un processo di migrazione per eseguire la migrazione di oggetti modificati  

1.  Nella console di Configuration Manager scegliere **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** espandere **Migrazione**e quindi scegliere **Processi di migrazione**.  

3.  Nella scheda **Home**, nel gruppo **Crea**, scegliere **Crea processo di migrazione**.  

4.  Nella pagina **Generale** della Creazione guidata del processo di migrazione configurare gli elementi seguenti e quindi scegliere **Avanti**:  

    -   Specificare un nome per il processo di migrazione.  

    -   Nell'elenco a discesa **Tipo di processo** selezionare **Oggetti modificati dopo la migrazione**.  

5.  Nella pagina **Seleziona oggetti** selezionare i tipi di oggetto da migrare. Per impostazione predefinita, vengono selezionati tutti gli oggetti disponibili per ogni tipo di oggetto selezionato.  

6.  Nella pagina **Proprietà contenuto** assegnare la proprietà del contenuto da ciascun sito di origine elencato a un sito nella gerarchia di destinazione e quindi scegliere **Avanti**. Se non è elencato alcuna sito di origine scegliere **Avanti**.  

7.  Nella pagina **Ambito di protezione** selezionare uno o più ambiti di protezione dell'amministrazione basata su ruoli da assegnare agli oggetti in questo processo di migrazione e quindi scegliere **Avanti**.  

8.  Nella pagina **Riesamina informazioni** scegliere **Salva nel file** per salvare le informazioni per poterle visualizzare in seguito. Quando si è pronti per continuare scegliere **Avanti**.  

9. Nella pagina **Impostazioni** configurare il momento in cui eseguire il processo di migrazione ed eventuali impostazioni aggiuntive necessarie per questo processo di migrazione. Diversamente dagli altri tipi di processi di migrazione, questo processo deve sovrascrivere gli oggetti migrati in precedenza nel database di Configuration Manager. Scegliere **Avanti**.  

10. Confermare le impostazioni e quindi completare la procedura guidata.  

###  <a name="modify-the-exclusion-list-for-migration"></a><a name="BKMK_Modify_Exclusion_List"></a> Modificare l'elenco di esclusione per la migrazione  

1.  Nella console di Configuration Manager scegliere **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** scegliere **Migrazione** per ottenere l'accesso all'elenco di esclusione. È possibile accedere all'elenco di esclusione anche dal nodo **Gerarchia di origine** o **Processi di migrazione** .  

3.  Nella scheda **Home**, nel gruppo **Migrazione**, scegliere **Modifica elenco di esclusione**.  

4.  Nella finestra di dialogo **Modifica elenco di esclusione** selezionare l'oggetto escluso che si vuole rimuovere dall'elenco di esclusione e quindi scegliere **Rimuovi**.  

5.  Scegliere **OK** per salvare le modifiche e completare la modifica. Per annullare le modifiche correnti e ripristinare tutti gli oggetti rimossi, scegliere **Annulla** e quindi **No**. In questo modo verrà annullata la rimozione degli oggetti e la finestra di dialogo **Modifica elenco di esclusione** verrà chiusa.  

#### <a name="share-distribution-points-from-the-source-hierarchy"></a>Condividere i punti di distribuzione dalla gerarchia di origine  

1.  Nella console di Configuration Manager scegliere **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** espandere **Migrazione**, scegliere **Gerarchia di origine** e quindi selezionare il sito di origine da configurare.  

3.  Nella scheda **Home**, nel gruppo **Sito di origine**, scegliere **Configura**.  

4.  Nella finestra di dialogo **Credenziali del sito di origine** selezionare **Abilita la condivisione dei punti di distribuzione per il server del sito di origine** e quindi scegliere **OK**.  

5.  Al termine della raccolta dati, scegliere **Chiudi**.  

#### <a name="change-the-schedule-of-a-migration-job"></a>Modificare la pianificazione di un processo di migrazione  

1.  Nella console di Configuration Manager scegliere **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** espandere **Migrazione**e quindi scegliere **Processi di migrazione**.  

3.  Scegliere il processo di migrazione da modificare. Nella scheda **Home**, nel gruppo **Proprietà**, fare clic su **Proprietà**.  

4.  Nelle proprietà del processo di migrazione selezionare la scheda **Impostazioni**, modificare il tempo di esecuzione per il processo di migrazione e quindi scegliere **OK**.  

##  <a name="run-migration-jobs"></a><a name="Run_Migration_Jobs"></a> Eseguire i processi di migrazione  
 Utilizzare la seguente procedura per eseguire un processo di migrazione non ancora avviato.  


1.  Nella console di Configuration Manager scegliere **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** espandere **Migrazione**e quindi scegliere **Processi di migrazione**.  

3.  Scegliere il processo di migrazione da eseguire. Nella scheda **Home**, nel gruppo **Processo di migrazione**, scegliere **Avvia**.  

4.  Scegliere **Sì** per avviare il processo di migrazione.  

##  <a name="upgrade-or-reassign-a-shared-distribution-point"></a><a name="BKMK_ProcUpgrdSS"></a> Aggiornare o riassegnare un punto di distribuzione condiviso  
 È possibile aggiornare un punto di distribuzione supportato condiviso da un sito di origine di Configuration Manager 2007 oppure riassegnare un punto di distribuzione supportato condiviso da un sito di origine di Configuration Manager in modo che diventi un punto di distribuzione nella gerarchia di destinazione.  

> [!IMPORTANT]  
>  Prima di aggiornare un punto di distribuzione secondario di Configuration Manager 2007, è necessario disinstallare il software client di Configuration Manager 2007 dal computer del punto di distribuzione secondario. Se il software client di Configuration Manager 2007 viene installato durante il tentativo di aggiornamento del punto di distribuzione, l'aggiornamento ha esito negativo e il contenuto precedentemente distribuito a un punto di distribuzione secondario viene rimosso dal computer.  

> [!CAUTION]  
>  Quando si aggiorna o si riassegna un punto di distribuzione condiviso, il computer di sistema del sito e il ruolo di sistema del sito del punto di distribuzione vengono rimossi dal sito di origine e aggiunti come punto di distribuzione al sito nella gerarchia di destinazione selezionata.  

#### <a name="upgrade-or-reassign-a-shared-distribution-point"></a>Aggiornare o riassegnare un punto di distribuzione condiviso  

1.  Nella console di Configuration Manager scegliere **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** espandere **Migrazione** e quindi scegliere **Gerarchia di origine**.  

3.  Selezionare il sito proprietario del punto di distribuzione da aggiornare, scegliere la scheda **Punti di distribuzione condivisi** e selezionare il punto di distribuzione appropriato da aggiornare o riassegnare.  

4.  Nella scheda **Punto di distribuzione**, nel gruppo **Punto di distribuzione**, scegliere **Riassegna**.  

5.  Specificare le impostazioni in Riassegnazione guidata punti di distribuzione condivisi come per l'installazione di un nuovo punto di distribuzione per la gerarchia di destinazione, con le seguenti aggiunte:  

    -   Nella pagina **Conversione del contenuto** controllare le indicazioni relative allo spazio richiesto per convertire il contenuto esistente. Nella pagina **Impostazioni unità** della procedura guidata verificare quindi che nell'unità del computer del punto di distribuzione selezionata sia disponibile la quantità di spazio libero su disco necessaria.  

6.  Confermare le impostazioni e quindi completare la procedura guidata.  

##  <a name="monitor-migration-activity-in-the-migration-workspace"></a><a name="Monitor_MIgration"></a> Monitorare l'attività di migrazione nell'area di lavoro Migrazione  
 Usare la console di Configuration Manager per monitorare la migrazione.  

1.  Nella console di Configuration Manager scegliere **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** espandere **Migrazione**e quindi scegliere **Processi di migrazione**.  

3.  Scegliere il processo di migrazione da monitorare.  

4.  Visualizzare i dettagli e lo stato relativi al processo di migrazione selezionato nelle schede **Riepilogo** e **Oggetti nel processo**.  

##  <a name="migrate-clients"></a><a name="BKMK_MigrateClients"></a> Eseguire la migrazione dei client  
 Dopo aver eseguito la migrazione dei dati per i client da una gerarchia all'altra, ma prima di completare tale operazione, pianificare la migrazione dei client nella gerarchia di destinazione. La migrazione di client da una gerarchia all'altra comporta la disinstallazione del software client di Configuration Manager dai computer assegnati alla gerarchia di origine e l'installazione del software client di Configuration Manager dalla gerarchia di destinazione. Quando si installa il client dalla gerarchia di destinazione si assegna anche il client a un sito primario in tale gerarchia. Per altre informazioni sulla migrazione dei client, vedere [Pianificazione di una strategia di migrazione client](../../core/migration/planning-a-client-migration-strategy.md).  

##  <a name="finish-migration"></a><a name="Complete_Migration"></a> Completare la migrazione  
 Usare questa procedura per completare la migrazione dalla gerarchia di origine.  

1.  Nella console di Configuration Manager scegliere **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** espandere **Migrazione** e quindi scegliere **Gerarchia di origine**.  

3.  Per una gerarchia di origine di Configuration Manager 2007, selezionare un sito di origine nel livello inferiore della gerarchia di origine. Per una gerarchia di origine di System Center 2012 Configuration Manager o Configuration Manager Current Branch, selezionare il sito di origine disponibile.  

4.  Nella scheda **Home**, nel gruppo **Pulisci**, scegliere **Interrompi raccolta dati**.  

5.  Scegliere **Sì** per confermare l'azione.  

6.  Per una gerarchia di origine di Configuration Manager 2007, ripetere i passaggi 3, 4 e 5 prima di passare al passaggio successivo. Eseguire questi passaggi in ogni sito della gerarchia, dal livello inferiore a quello superiore. Per una gerarchia di origine di System Center 2012 Configuration Manager o Configuration Manager Current Branch, continuare con il passaggio successivo.  

7.  Nella scheda **Home**, nel gruppo **Pulisci**, scegliere **Pulisci dati migrazione**.  

8.  Nella finestra di dialogo **Pulisci dati migrazione** selezionare il codice e il server del sito del sito principale della gerarchia di origine nell'elenco a discesa **Gerarchia di origine** e quindi scegliere **OK**.  

9. Scegliere **Sì** per completare il processo di migrazione per la gerarchia di origine.  
