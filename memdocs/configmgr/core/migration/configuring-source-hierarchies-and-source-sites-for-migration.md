---
title: Gerarchie di origine della migrazione
titleSuffix: Configuration Manager
description: Configurare una gerarchia di origine e i siti di origine per eseguire la migrazione dei dati all'ambiente di Configuration Manager Current Branch.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ccce7cb5-e18f-4337-8adf-2018edca3c00
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c2e8e2ba57867b3c2a0929cfd670629296fdb9c9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701779"
---
# <a name="configure-source-hierarchies-and-source-sites-for-migration-to-configuration-manager-current-branch"></a>Configurare gerarchie di origine e siti di origine per la migrazione a Configuration Manager Current Branch

*Si applica a: Configuration Manager (Current Branch)*

Per abilitare la migrazione dei dati nell'ambiente di Configuration Manager Current Branch, è necessario configurare una gerarchia di origine di Configuration Manager supportata e uno o più siti di origine nella stessa gerarchia che contengono i dati da migrare.  

> [!NOTE]  
>  Le operazioni di migrazione vengono eseguite nel sito di livello superiore della gerarchia di destinazione. Se la migrazione viene configurata durante l'uso di una console di Configuration Manager connessa a un sito figlio primario, è necessario attendere che la configurazione venga replicata nel sito di amministrazione centrale, che venga avviata e che lo stato venga replicato di nuovo nel sito primario a cui l'utente è connesso.  

 Usare le informazioni e le procedure riportate nelle sezioni seguenti per specificare la gerarchia di origine e aggiungere siti di origine aggiuntivi. Dopo aver completato queste procedure, è possibile creare i processi di migrazione e iniziare a migrare i dati dalla gerarchia di origine alla gerarchia di destinazione.  

-   [Specificare una gerarchia di origine per la migrazione](#BKBM_ConfigSrcHierarchy)  

-   [Individuare siti di origine aggiuntivi della gerarchia di origine](#BKBM_ConfigSrcSites)  

##  <a name="specify-a-source-hierarchy-for-migration"></a><a name="BKBM_ConfigSrcHierarchy"></a> Specificare una gerarchia di origine per la migrazione  
 Per migrare i dati nella gerarchia di destinazione, è necessario specificare una gerarchia di origine supportata contenente i dati da migrare. Per impostazione predefinita, il sito di livello superiore di tale gerarchia diventa un sito di origine della gerarchia di origine. Se si esegue la migrazione da una gerarchia di Configuration Manager 2007, è quindi possibile configurare siti di origine aggiuntivi per la migrazione dopo avere raccolto i dati dal sito di origine iniziale. Se si esegue la migrazione da una gerarchia di System Center 2012 Configuration Manager o di Configuration Manager Current Branch, non è necessario configurare i siti di origine aggiuntivi per la migrazione dei dati dalla gerarchia di origine. Questo è possibile perché le versioni di Configuration Manager usano un database condiviso disponibile nel sito principale della gerarchia di origine. Il database condiviso include tutte le informazioni che è possibile migrare.  

 Usare le procedure seguenti per specificare una gerarchia di origine per la migrazione e per individuare siti di origine aggiuntivi in una gerarchia di Configuration Manager 2007.  

 Eseguire questa procedura con una console di Configuration Manager connessa alla gerarchia di destinazione:  

### <a name="to-configure-a-source-hierarchy"></a>Per configurare una gerarchia di origine   

1. Nella console di Configuration Manager fare clic su **Amministrazione**.  

2. Nell'area di lavoro **Amministrazione** espandere **Migrazione**, quindi fare clic su **Gerarchia di origine**.  

3. Nella scheda **Home** , nel gruppo **Migrazione** , fare clic su **Specifica gerarchia di origine**.  

4. Nella finestra di dialogo **Specifica gerarchia di origine** , per **Gerarchia di origine**, selezionare **Nuova gerarchia di origine**.  

5. Per **Server di sito di Configuration Manager di livello superiore** immettere il nome o l'indirizzo IP del sito principale di una gerarchia di origine supportata.  

6. Specificare gli account di accesso del sito di origine che dispongono delle seguenti autorizzazioni:  

   - Account del sito di origine: autorizzazione di **lettura** per il provider SMS per il sito di livello superiore specificato nella gerarchia di origine. Per la condivisione e gli aggiornamenti dei punti di distribuzione sono necessarie le autorizzazioni **Modifica** ed **Eliminazione** per il sito nella gerarchia di origine.

   - Account del database del sito di origine: autorizzazioni di **lettura** ed **esecuzione** per il database di SQL Server per il sito di livello superiore specificato nella gerarchia di origine.  

     Se viene specificato l'uso dell'account computer, Configuration Manager usa l'account computer del sito principale della gerarchia di destinazione. Per questa opzione, verificare che l'account appartenga al gruppo di protezione **Distributed COM Users** nel dominio in cui si trova il sito di livello superiore della gerarchia di origine.  

7. Per condividere i punti di distribuzione tra le gerarchie di origine e di destinazione, selezionare la casella di controllo **Abilita la condivisione dei punti di distribuzione per il server del sito di origine** . Se non si abilita la condivisione dei punti di distribuzione in questo momento, è possibile farlo modificando le credenziali del sito di origine dopo che la raccolta dei dati è terminata.  

8. Fare clic su **OK** per salvare la configurazione. Verrà visualizzata la finestra di dialogo **Stato raccolta dati** e la raccolta dei dati inizierà automaticamente.  

9. Al termine della raccolta dei dati, fare clic su **Chiudi** per chiudere la finestra di dialogo **Stato raccolta dati** e completare la configurazione.  

##  <a name="identify-additional-source-sites-of-the-source-hierarchy"></a><a name="BKBM_ConfigSrcSites"></a> Individuare siti di origine aggiuntivi della gerarchia di origine  
 Quando viene configurata una gerarchia di origine supportata, il sito di livello superiore di tale gerarchia viene configurato automaticamente come sito di origine e i dati vengono automaticamente raccolti dal sito. L'azione successiva dipende dalla versione di Configuration Manager eseguita dalla gerarchia di origine:  

-   Per una gerarchia di origine di Configuration Manager 2007, è possibile avviare la migrazione da tale sito di origine iniziale oppure configurare altri siti di origine dalla gerarchia di origine al termine della raccolta dei dati per il sito di origine iniziale. Per migrare i dati disponibili solo da un sito figlio, configurare siti di origine aggiuntivi per una gerarchia di Configuration Manager 2007. Ad esempio, potrebbero essere configurati siti di origine aggiuntivi per raccogliere dati sui contenuti che si vuole migrare quando sono stati creati in un sito figlio nella gerarchia di origine e non sono disponibili nel sito di livello superiore per la gerarchia di origine.  

-   Per una gerarchia di origine di System Center 2012 Configuration Manager o Configuration Manager Current Branch, non è necessario selezionare siti di origine aggiuntivi. Questo è possibile perché le versioni di Configuration Manager usano un database condiviso disponibile nel sito principale della gerarchia di origine. Il database condiviso include tutte le informazioni che è possibile migrare da tutti i siti di tale gerarchia di origine. Ciò rende i dati di cui è possibile eseguire la migrazione disponibili nel sito di livello superiore della gerarchia di origine.  

Quando si configurano siti di origine aggiuntivi per una gerarchia di origine di Configuration Manager 2007, è necessario configurare i siti di origine aggiuntivi provenienti dalla gerarchia di origine procedendo dall'alto verso il basso. Prima di configurare uno dei siti figlio come sito di origine, è necessario configurare un sito padre come sito di origine.  

Usare la procedura seguente per configurare siti di origine aggiuntivi per le gerarchie di origine di Configuration Manager 2007:  

### <a name="to-identify-additional-source-sites-in-the-source-hierarchy"></a>Per individuare siti di origine aggiuntivi nella gerarchia di origine 

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** espandere **Migrazione**, quindi fare clic su **Gerarchia di origine**.  

3.  Scegliere il sito che si vuole configurare come sito di origine.  

4.  Nella scheda **Home** , nel gruppo **Sito di origine** , fare clic su **Configura**.  

5.  Nella finestra di dialogo **Credenziali del sito di origine** , per gli account di accesso al sito di origine, specificare gli account che dispongono delle seguenti autorizzazioni:  

    -   Account del sito di origine: autorizzazione di **lettura** per il provider SMS per il sito di livello superiore specificato nella gerarchia di origine. Per la condivisione e gli aggiornamenti dei punti di distribuzione sono necessarie le autorizzazioni **Modifica** ed **Eliminazione** per il sito nella gerarchia di origine.  

    -   Account del database del sito di origine: autorizzazioni di **lettura** ed **esecuzione** per il database di SQL Server per il sito di livello superiore specificato nella gerarchia di origine.  

    Se viene specificato l'uso dell'account computer, Configuration Manager usa l'account computer del sito principale della gerarchia di destinazione. Per questa opzione, verificare che l'account appartenga al gruppo di protezione **Distributed COM Users** nel dominio in cui si trova il sito di livello superiore della gerarchia di origine.  

6.  Per condividere i punti di distribuzione tra le gerarchie di origine e di destinazione, selezionare la casella di controllo **Abilita la condivisione dei punti di distribuzione per il server del sito di origine** . Se non si abilita la condivisione dei punti di distribuzione in questo momento, è possibile farlo modificando le credenziali per il sito di origine dopo che la raccolta dei dati è terminata.  

7. Fare clic su **OK** per salvare la configurazione. Verrà visualizzata la finestra di dialogo **Stato raccolta dati** e la raccolta dei dati inizierà automaticamente.  

8.  Al termine della raccolta dei dati, fare clic su **Chiudi** per completare la configurazione.  
