---
title: Strategia per la gerarchia di origine
titleSuffix: Configuration Manager
description: Configurare una gerarchia di origine e raccogliere i dati da un sito di origine prima di configurare un processo di migrazione di Configuration Manager.
ms.date: 01/3/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4800a800-66c8-4c35-aebe-e413a23790c1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 28960753da06058ef181f94a5d11d9f2327ebf56
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702859"
---
# <a name="plan-a-source-hierarchy-strategy-in-configuration-manager"></a>Pianificare una strategia per la gerarchia di origine in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Prima di configurare un processo di migrazione nell'ambiente di Configuration Manager, è necessario configurare una gerarchia di origine e raccogliere i dati da almeno un sito di origine di tale gerarchia. Usare le sezioni seguenti per pianificare la configurazione delle gerarchie di origine, configurare i siti di origine e determinare come Configuration Manager raccoglie le informazioni dai siti di origine nella gerarchia di origine. 

##  <a name="source-hierarchies"></a><a name="BKMK_Source_Hierarchies"></a> Gerarchie di origine  
Una gerarchia di origine è una gerarchia di Configuration Manager che contiene i dati di cui si vuole eseguire la migrazione. Quando si configura la migrazione e si specifica una gerarchia di origine, specificare il sito di livello superiore della gerarchia di origine. Tale sito viene anche denominato sito di origine. Anche i siti aggiuntivi da cui è possibile migrare dati dalla gerarchia di origine vengono denominati siti di origine.  

-   Quando si configura un processo di migrazione per la migrazione dei dati da una gerarchia di origine di Configuration Manager 2007, tale processo viene configurato per eseguire la migrazione dei dati da uno o più siti di origine specifici nella gerarchia di origine.  

-   Quando si configura un processo per la migrazione dei dati da una gerarchia di origine che esegue System Center 2012 Configuration Manager o versione successiva, è sufficiente specificare solo il sito principale.  

È possibile configurare una sola gerarchia di origine alla volta.  

-   Se si configura una nuova gerarchia di origine, quest'ultima diventa automaticamente la gerarchia di origine corrente sostituendo la gerarchia di origine precedente.  

-   Quando si configura una gerarchia di origine, è necessario specificare il sito principale della gerarchia di origine e specificare le credenziali per Configuration Manager da usare per connettersi al provider SMS e al database del sito di origine.  

-   Configuration Manager usa queste credenziali per eseguire una raccolta dati per recuperare le informazioni sugli oggetti e sui punti di distribuzione dal sito di origine.  

-   Come parte del processo di raccolta dati, vengono individuati i siti figlio presenti nella gerarchia di origine.  

-   Se la gerarchia di origine è una gerarchia di Configuration Manager 2007, è possibile configurare tali siti aggiuntivi come siti di origine, con credenziali diverse per ogni sito di origine.  

Anche se è possibile configurare più gerarchie di origine, la migrazione è attiva per una sola gerarchia di origine alla volta.  

-   Se si configura una gerarchia di origine aggiuntiva prima di completare la migrazione dalla gerarchia di origine corrente, Configuration Manager annulla tutti i processi di migrazione attivi e posticipa tutti i processi di migrazione pianificati per la gerarchia di origine corrente.  

-   La gerarchia di origine appena configurata diventa quindi la gerarchia di origine corrente e la gerarchia originale viene disattivata.  

-   È quindi possibile configurare le credenziali di connessione, i siti di origine aggiuntivi e i processi di migrazione per la nuova gerarchia di origine.  

Se si ripristina una gerarchia di origine inattiva e non si è usato **Pulisci dati migrazione**, è possibile visualizzare i processi di migrazione configurati prima per tale gerarchia di origine. Tuttavia, prima di poter proseguire con la migrazione da tale gerarchia, è necessario riconfigurare le credenziali per la connessione ai siti di origine applicabili nella gerarchia e quindi pianificare nuovamente eventuali processi di migrazione non completati.  

> [!CAUTION]  
>  Se la migrazione di dati viene eseguita da più di una gerarchia di origine, è necessario che ogni gerarchia di origine aggiuntiva contenga un insieme univoco di codici del sito.  
> Le gerarchie di origine e destinazione richiedono anche set di codici del sito diversi.

Per altre informazioni sulla configurazione di una gerarchia di origine, vedere [Configurazione di gerarchie di origine e siti di origine per la migrazione in Configuration Manager Current Branch](../../core/migration/configuring-source-hierarchies-and-source-sites-for-migration.md).  

##  <a name="source-sites"></a><a name="BKMK_Source_Sites"></a> Siti di origine  
 I siti di origine sono i siti nella gerarchia di origine che contengono i dati da migrare. Il sito di livello superiore della gerarchia di origine è sempre il primo sito di origine. Quando la migrazione raccoglie i dati dal primo sito di origine di una nuova gerarchia di origine, individua le informazioni sui siti aggiuntivi presenti in tale gerarchia.  

 Al termine della raccolta dati per il sito di origine iniziale, le azioni da intraprendere in seguito dipendono dalla versione del prodotto della gerarchia di origine.  

### <a name="source-sites-that-run-configuration-manager-2007-sp2"></a>Siti di origine che eseguono Configuration Manager 2007 SP2  
 Dopo aver raccolto i dati dal sito di origine iniziale della gerarchia di Configuration Manager 2007 SP2, non è necessario configurare i siti di origine aggiuntivi prima di creare i processi di migrazione. Prima di poter eseguire la migrazione dei dati dai siti aggiuntivi, è necessario configurare i siti aggiuntivi come siti di origine e Configuration Manager deve completare la raccolta dati da tali siti.  

 Per raccogliere dati da siti aggiuntivi, configurare singolarmente ogni sito come sito di origine. Per eseguire questa operazione è necessario specificare le credenziali per Configuration Manager per la connessione al database del sito e al provider SMS di ogni sito di origine. Dopo aver configurato le credenziali per un sito di origine, viene avviato il processo di raccolta dati per tale sito.  

 Quando si configurano i siti di origine aggiuntivi in una gerarchia di origine di Configuration Manager 2007 SP2, è necessario configurare i siti di origine dall'alto verso il basso, ovvero configurare per ultimi i siti di livello inferiore. È possibile configurare i siti di origine in un ramo della gerarchia in qualsiasi momento, ma è necessario configurare un sito come sito di origine prima di configurare eventuali siti figlio come siti di origine.  

> [!NOTE]  
>  Solo i siti primari in una gerarchia di Configuration Manager 2007 SP2 sono supportati per la migrazione.  

### <a name="source-sites-that-run-system-center-2012-configuration-manager-or-later"></a>Siti di origine che eseguono System Center 2012 Configuration Manager o versioni successive  
 Dopo aver raccolto i dati dal sito di origine iniziale della gerarchia di System Center 2012 Configuration Manager o versione successiva, non è necessario configurare siti di origine aggiuntivi in tale gerarchia di origine. Questo è possibile perché, a differenza di Configuration Manager 2007, le versioni di Configuration Manager usano un database condiviso che consente di identificare ed eseguire la migrazione di tutti gli oggetti disponibili dal sito di origine iniziale.  

 Quando si configurano gli account di accesso per la raccolta dati, potrebbe essere necessario garantire l'accesso **Account del provider SMS del sito di origine** per più computer nella gerarchia di origine. Potrebbe essere necessario, ad esempio, quando il sito di origine supporta più istanze del provider SMS, ognuna in un computer diverso. Quando la raccolta dati viene avviata, il sito di livello superiore della gerarchia di origine viene contattato dal sito di livello superiore della gerarchia di destinazione per individuare i percorsi del provider SMS per tale sito. Viene individuata solo la prima istanza del provider SMS. Se il processo di raccolta dati non riesce ad accedere al provider SMS nel percorso individuato, il processo non verrà completato e non tenterà di connettersi a computer aggiuntivi che eseguono un'istanza del provider SMS per tale sito.  

##  <a name="data-gathering"></a><a name="BKMK_Data_Gathering"></a> Raccolta dati  
 Subito dopo aver specificato una gerarchia di origine, aver configurato le credenziali per ogni sito di origine aggiuntivo in una gerarchia di origine oppure aver condiviso i punti di distribuzione per un sito di origine, Configuration Manager avvia la raccolta dati dal sito di origine.  

 Il processo di raccolta dati quindi viene ripetuto in una pianificazione semplice per mantenere la sincronizzazione con eventuali modifiche apportate ai dati nel sito di origine. Per impostazione predefinita, il processo viene ripetuto ogni quattro ore. È possibile modificare la pianificazione di questo ciclo modificando le **Proprietà** del sito di origine. Il processo di raccolta dati iniziale deve esaminare tutti gli oggetti nel database di Configuration Manager e il completamento di questa operazione potrebbe richiedere diverso tempo. I processi di raccolta dati successivi individuano solo le modifiche apportate ai dati e richiedono meno tempo.  

 Per raccogliere i dati, il sito di livello superiore nella gerarchia di destinazione si connette al provider SMS e al database del sito del sito di origine per recuperare un elenco di oggetti e punti di distribuzione. Queste connessioni utilizzano gli account di accesso del sito di origine. Per informazioni sulle configurazioni necessarie per la raccolta dati, vedere [Prerequisiti per la migrazione](../../core/migration/prerequisites-for-migration.md).  

 È possibile avviare e interrompere il processo di raccolta dati usando **Raccogli dati adesso**e **Interrompi raccolta dati** nella console di Configuration Manager.  

 Dopo aver usato **Interrompi raccolta dati** per un sito di origine per qualsiasi motivo, è necessario riconfigurare le credenziali per il sito prima di poter raccogliere nuovamente i dati da tale sito. Finché il sito di origine non viene riconfigurato, Configuration Manager non è in grado di individuare nuovi oggetti o modifiche agli oggetti migrati in precedenza in quel sito.  

> [!NOTE]  
>  Prima di espandere un sito primario autonomo in una gerarchia con un sito di amministrazione centrale, è necessario interrompere la raccolta di tutti i dati. È possibile riconfigurare la raccolta dati al termine dell'espansione del sito.  

### <a name="gather-data-now"></a>Raccogliere i dati adesso  
 Dopo aver eseguito il processo di raccolta dati iniziale per un sito, questo processo viene ripetuto per individuare gli oggetti aggiornati dall'ultimo ciclo di raccolta dati. È anche possibile eseguire l'azione **Raccogli dati adesso** nella console di Configuration Manager per avviare subito il processo e reimpostare l'ora di inizio del ciclo successivo.  

 Al termine del processo di raccolta dati per un sito di origine, è possibile condividere i punti di distribuzione dal sito di origine e configurare i processi di migrazione per eseguire la migrazione dei dati dal sito. La raccolta dati è un processo ripetuto per la migrazione e continua finché non viene modificata la gerarchia di origine oppure si usa **Interrompi raccolta dati** per terminare il processo di raccolta dati per tale sito.  

### <a name="stop-gathering-data"></a>Interrompi raccolta dati  
 È possibile eseguire **Interrompi raccolta dati** per terminare il processo di raccolta dati per un sito di origine quando non si vuole più che Configuration Manager individui oggetti nuovi o modificati da tale sito. Questa azione impedisce a Configuration Manager di offrire ai client nella gerarchia di destinazione punti di distribuzione condivisi dall'origine come percorsi contenuto per il contenuto migrato.  

 Per interrompere la raccolta dati da ogni sito di origine, è necessario eseguire **Interrompi raccolta dati** nei siti di origine di livello inferiore, quindi ripetere il processo in ogni sito padre. L'interruzione della raccolta dati nel sito principale della gerarchia di origine deve rappresentare l'ultimo passaggio. È necessario interrompere la raccolta dati in ogni sito figlio prima di eseguire questa azione in un sito padre. In genere, si interrompe la raccolta dati solo quando si è pronti a completare il processo di migrazione.  

 Dopo aver interrotto la raccolta dati per un sito di origine, le informazioni raccolte in precedenza sugli oggetti e le raccolte da tale sito rimangono disponibili per l'uso durante la configurazione di nuovi processi di migrazione. Tuttavia, non vengono visualizzati nuovi oggetti o raccolte né le modifiche apportate agli oggetti esistenti. Se si riconfigura il sito di origine e si avvia nuovamente la raccolta dati, verranno visualizzate le informazioni e lo stato relativi agli oggetti migrati in precedenza.  
