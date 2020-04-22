---
title: Elenchi di controllo per la migrazione
titleSuffix: Configuration Manager
description: Usare gli elenchi di controllo per gli amministratori per facilitare la pianificazione di una strategia di migrazione verso Configuration Manager Current Branch.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 295fdf07-93cc-490c-acdd-ce3ee88cb36f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e406a2b7674815bb3313200ba850baa249f17ebc
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701809"
---
# <a name="administrator-checklists-for-migration-planning-in-configuration-manager"></a>Elenchi di controllo per gli amministratori per la pianificazione della migrazione in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Usare gli elenchi di controllo per gli amministratori seguenti per facilitare la pianificazione di una strategia di migrazione verso Configuration Manager Current Branch.

##  <a name="administrator-checklist-for-migration-planning"></a><a name="Checklist_Migraiton_Planning"></a> Elenco di controllo amministratore per la pianificazione della migrazione  
 Utilizzare il seguente elenco di controllo per la procedura di pianificazione pre-migrazione.  

-   **Valutare l'ambiente corrente:**  

     Identificare i requisiti aziendali esistenti soddisfatti dalla gerarchia di origine e sviluppare piani per continuare a soddisfare tali requisiti nella gerarchia di destinazione.  

-   **Esaminare le funzionalità e le modifiche disponibili con la versione di Configuration Manager in uso e sfruttare tali informazioni per progettare la gerarchia di destinazione:**  

    Per altre informazioni, vedere [Nozioni fondamentali di Configuration Manager](../../core/understand/fundamentals.md) e [Novità](../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md).  


-   **Determinare il modello di protezione amministrativa da usare per l'amministrazione basata sui ruoli:**  

    Per altre informazioni, vedere [Nozioni fondamentali di amministrazione basata su ruoli per Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

-   **Valutare la rete e la topologia di Active Directory:** Esaminare la struttura del dominio e la topologia di rete esistenti e valutarne l'effetto sulle attività di migrazione e progettazione della gerarchia.  

-   **Finalizzare la struttura della gerarchia di destinazione:**  

    Stabilire la posizione di un sito di amministrazione centrale, dei siti principali, dei siti secondari e delle opzioni di distribuzione del contenuto.  

-   **Mappare la gerarchia ai computer che verranno usati per i siti e i server dei siti nella gerarchia di destinazione:**  

    Identificare i computer che verranno usati dai siti e dai server dei sistemi dei siti nella gerarchia di destinazione e quindi verificare che questi dispongano di capacità sufficiente per soddisfare i requisiti di funzionamento esistenti e futuri.  

-   **Pianificare la strategia di migrazione degli oggetti:**  

    Pianificare l'uso dei processi di migrazione disponibili per eseguire la migrazione di oggetti diversi, tra cui limiti del sito, raccolte, annunci e distribuzioni. Per altre informazioni, vedere [Tipi di processi di migrazione](../../core/migration/planning-a-migration-job-strategy.md#Types_of_Migration) in [Pianificazione di una strategia di processo di migrazione](../../core/migration/planning-a-migration-job-strategy.md)  

    Configuration Manager esegue la migrazione solo degli oggetti selezionati. Tutti gli oggetti di cui non viene eseguita la migrazione e che sono necessari nella gerarchia di destinazione devono essere ricreati nella gerarchia di destinazione.  

    Gli oggetti di cui è possibile eseguire la migrazione vengono visualizzati durante la configurazione del processi di migrazione.  

-   **Pianificare la strategia di migrazione del client:**  

    Pianificare la migrazione di client utilizzando un approccio controllato che limita i requisiti di elaborazione del server e di larghezza di banda quando si esegue la migrazione dei client nella gerarchia di destinazione. Per altre informazioni sulla pianificazione di una strategia di migrazione dei client, vedere [Pianificazione di una strategia di migrazione client](../../core/migration/planning-a-client-migration-strategy.md).  

-   **Pianificare i dati di inventario e di conformità:**  

    Configuration Manager non supporta la migrazione dell'inventario hardware o software o dei dati di conformità della gestione configurazione desiderata per i client o gli aggiornamenti software.  

    Dopo aver eseguito la migrazione nel nuovo sito nella gerarchia di destinazione e aver ricevuto il criterio per tali configurazioni, il client invia le informazioni al sito assegnato. Questa azione consente di popolare il database del sito di destinazione con i dati di conformità e l'inventario corrente.  

-   **Pianificare il completamento della migrazione dalla gerarchia di origine:**  

    Decidere quando verrà eseguita la migrazione degli oggetti e dei client. Al termine della migrazione è possibile pianificare la rimozione delle autorizzazioni per i server del sito nella gerarchia di origine.  

##  <a name="administrator-checklist-for-hierarchy-migration"></a><a name="Checklist_Hierarchy_for_migration"></a> Elenco di controllo amministratore per la migrazione di una gerarchia  
Prima di iniziare la migrazione utilizzare il seguente elenco di controllo per la pianificazione di una gerarchia di destinazione.  

-   **Identificare i computer da usare nella gerarchia di destinazione:**  

    Configuration Manager non supporta l'aggiornamento sul posto dall'infrastruttura di Configuration Manager 2007. Si usa invece la migrazione per spostare i dati da Configuration Manager 2007 a Configuration Manager Current Branch. Per questa operazione è necessario usare una distribuzione side-by-side e installare Configuration Manager nei nuovi computer.  

    Analogamente, quando si esegue la migrazione da un'altra gerarchia di Configuration Manager, è necessario installare una nuova gerarchia di destinazione che sia una distribuzione side-by-side nella gerarchia di origine.  

-   **Creare una gerarchia di destinazione:**  

    Per preparare la migrazione, installare e configurare una gerarchia di destinazione di Configuration Manager che includa un sito primario. Ad esempio:  

    -   Installare un sito di amministrazione centrale e almeno un sito primario figlio.  

    -   Installare un sito primario autonomo se non si prevede di utilizzare un sito di amministrazione centrale.  

-   **Per eseguire la migrazione di informazioni relative agli aggiornamenti software, configurare un punto di aggiornamento software nella gerarchia di destinazione e sincronizzare gli aggiornamenti software:**  

    È necessario configurare e sincronizzare gli aggiornamenti software nella gerarchia di destinazione prima di eseguire la migrazione delle informazioni sugli aggiornamenti software dalla gerarchia di origine.  


-   **Installare e configurare ruoli del sistema del sito aggiuntivi nella gerarchia di destinazione:**  

    Configurare i ruoli del sistema del sito e i sistemi del sito aggiuntivi necessari.  

-   **Controllare la funzionalità operativa nella gerarchia di destinazione:**  

    Verificare quanto segue:  

    -   Se la gerarchia di destinazione include più siti, confermare il funzionamento della replica di database tra i siti. La replica del database non è applicabile a siti primari autonomi.  

    -   Controllare che tutti i ruoli del sistema del sito installati siano operativi.  

    -   Controllare che i client di Configuration Manager installati nella gerarchia di destinazione siano in grado di comunicare correttamente con il relativo sito assegnato.  


##  <a name="administrator-checklist-for-migration"></a><a name="Checklisit_Migration"></a> Elenco di controllo amministratore per la migrazione  
Utilizzare il seguente elenco di controllo per la migrazione dei dati dalla gerarchia di origine alla gerarchia di destinazione.  

-   **Abilitare la migrazione nella gerarchia di destinazione:**  

    Configurare una gerarchia di origine specificando il sito di livello superiore della gerarchia di origine. Per altre informazioni sulla specificazione del sito di origine, vedere [Pianificazione di una strategia per la gerarchia di origine](../../core/migration/planning-a-source-hierarchy-strategy.md).  

-   **Quando la gerarchia di origine esegue Configuration Manager 2007 SP2, selezionare e configurare ulteriori siti nella gerarchia di origine:**  

    Per ogni sito aggiuntivo nella gerarchia di origine di Configuration Manager 2007 SP2 da cui si desidera raccogliere i dati è necessario configurare le credenziali per la raccolta dei dati. Dopo aver configurato ciascun sito di origine, il processo di raccolta dei dati inizia immediatamente e prosegue per tutto il periodo di migrazione fino a quando non si interrompe la raccolta dati per tale sito. Con la raccolta dei dati è possibile eseguire la migrazione dalla gerarchia di origine degli oggetti che risultano aggiornati o aggiunti dopo un processo precedente di raccolta dei dati.

    > [!NOTE]  
    >  Quando una gerarchia di origine esegue System Center 2012 Configuration Manager o versione successiva, non è necessario configurare siti di origine aggiuntivi.  

-   **Configurare la condivisione dei punti di distribuzione:**  

    È possibile condividere i punti di distribuzione tra due gerarchie per rendere disponibile il contenuto relativo agli oggetti migrati per i client presenti nella gerarchia di destinazione. Ciò garantisce che lo stesso contenuto rimanga disponibile per i client in entrambe le gerarchie e che sia possibile conservare tale contenuto fino all'interruzione della raccolta dei dati e alla fine della migrazione.  

    Per informazioni sui punti di distribuzione condivisi, vedere [Condividere punti di distribuzione tra gerarchie di origine e destinazione](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration) in [Pianificare una strategia di migrazione per la distribuzione del contenuto](../../core/migration/planning-a-content-deployment-migration-strategy.md).  

-   **Creare ed eseguire i processi di migrazione per la migrazione di oggetti associati ai client nella gerarchia di origine:**  

    Creare i processi di migrazione per la migrazione di oggetti tra le gerarchie. Le configurazioni necessarie per ogni processo di migrazione possono variare a seconda dei dati che vengono migrati dal processo.  

    Ad esempio, quando si esegue la migrazione di contenuto, indipendentemente dal processo di migrazione che si sceglie di utilizzare, è necessario assegnare un sito nella gerarchia di destinazione come responsabile della gestione di tale contenuto. Il sito assegnato potrà accedere al percorso originale del file di origine per tale contenuto ed è responsabile per la distribuzione del contenuto ai punti di distribuzione presenti nella gerarchia di destinazione.  

    Per altre informazioni, vedere [Creare e modificare i processi di migrazione per Configuration Manager](../../core/migration/operations-for-migration.md#Create_Edit_migration_Jobs) in [Operazioni per la migrazione a Configuration Manager Current Branch](../../core/migration/operations-for-migration.md).  

-   **Eseguire la migrazione dei client nella gerarchia di destinazione:**  

    Il processo di migrazione dei client dipende dallo scenario di migrazione:  

    -   Quando si esegue la migrazione di client che dispongono di una versione di client diversa da quella della gerarchia di destinazione, è necessario aggiornare il software client. L'aggiornamento richiede la rimozione del client di Configuration Manager corrente e quindi l'installazione della nuova versione del client corrispondente al sito di destinazione.  

    -   Quando si esegue la migrazione di client che dispongono di una versione di client corrispondente a quella della gerarchia di destinazione, non è necessario eseguire l'aggiornamento o la reinstallazione del client. Il client viene riassegnato a un sito primario nella gerarchia di destinazione.  

    Quando si esegue la migrazione di un client nella gerarchia di destinazione, il client viene associato ai relativi dati, precedentemente migrati in tale gerarchia di destinazione.  

    Per altre informazioni, vedere [Pianificazione di una strategia di migrazione client](../../core/migration/planning-a-client-migration-strategy.md).  

-   **Aggiornare o riassegnare i punti di distribuzione condivisi:**  

    Quando non è più necessario supportare i client nella gerarchia di origine, è possibile aggiornare i punti di distribuzione condivisi da un sito di origine di Configuration Manager 2007 o riassegnare i punti di distribuzione condivisi da un sito di origine di System Center 2012 Configuration Manager o Configuration Manager Current Branch. Quando si aggiorna o si riassegna un punto di distribuzione, il ruolo del sistema del sito viene trasferito in un sito primario presente nella gerarchia di destinazione e il punto di distribuzione viene rimosso dal sito di origine nella gerarchia di origine. Quando si aggiorna o si riassegna un punto di distribuzione condiviso, il contenuto rimane nel computer del punto di distribuzione e non è necessario ridistribuirlo nei nuovi punti di distribuzione presenti nella gerarchia di destinazione.  

    È inoltre possibile aggiornare un punto di distribuzione di Configuration Manager 2007 con percorso condiviso in un server del sito secondario. Tale operazione comporta la rimozione del sito secondario e la presenza di un solo punto di distribuzione nella gerarchia di destinazione.  

    Per informazioni sui punti di distribuzione condivisi, vedere [Condividere punti di distribuzione tra gerarchie di origine e destinazione](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration) in [Pianificare una strategia di migrazione per la distribuzione del contenuto](../../core/migration/planning-a-content-deployment-migration-strategy.md).  

-   **Completare la migrazione:**  

    Dopo aver eseguito la migrazione dei dati e dei client da tutti i siti presenti nella gerarchia di origine e dopo aver aggiornato i punti di distribuzione applicabili, è possibile terminare la migrazione. Per terminare la migrazione, è necessario interrompere la raccolta dei dati per ogni sito di origine nella gerarchia di origine. È quindi possibile eliminare le informazioni di migrazione non necessarie e rimuovere le autorizzazioni per l'infrastruttura della gerarchia di origine. Per altre informazioni, vedere [Pianificazione del completamento della migrazione](../../core/migration/planning-to-complete-migration.md).  
