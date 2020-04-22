---
title: Pianificare la migrazione dei client
titleSuffix: Configuration Manager
description: Informazioni sulle attività di migrazione dei client da una gerarchia di origine a una gerarchia di destinazione di Configuration Manager Current Branch.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2e27b0b7-7bd3-45cd-bc99-9c991606c637
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c0885cab43deacf7e7f487e5c20e171f6475b302
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704559"
---
# <a name="plan-a-client-migration-strategy-in-configuration-manager"></a>Pianificare una strategia di migrazione dei client in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Per eseguire la migrazione dei client dalla gerarchia di origine a una gerarchia di destinazione di Configuration Manager Current Branch, è necessario effettuare due attività. È necessario migrare gli oggetti associati al client e quindi reinstallare o riassegnare i client dalla gerarchia di origine alla gerarchia di destinazione. Migrare innanzitutto gli oggetti in modo che siano disponibili al momento della migrazione dei client. Gli oggetti associati al client vengono migrati mediante processi di migrazione. Per informazioni sulla migrazione degli oggetti associati al client, vedere [Pianificazione di una strategia di processo di migrazione](../../core/migration/planning-a-migration-job-strategy.md).  

 Utilizzare le seguenti sezioni per pianificare la migrazione dei client nella gerarchia di destinazione.  

-   [Pianificare la migrazione dei client nella gerarchia di destinazione](#Planning_for_Client_Agent_Migration)  

-   [Pianificare la gestione dei dati conservati nei client durante la migrazione](#Planning_for_Client_Data_Migration)  

-   [Pianificare i dati di inventario e di conformità durante la migrazione](#Planning_for_Inventory_data_migration)  

##  <a name="plan-to-migrate-clients-to-the-destination-hierarchy"></a><a name="Planning_for_Client_Agent_Migration"></a> Pianificare la migrazione dei client nella gerarchia di destinazione  
 Quando si esegue la migrazione dei client da una gerarchia di origine, il software client nel computer client viene aggiornato in base alla versione prodotto della gerarchia di destinazione.  

-   **Gerarchia di origine con Configuration Manager 2007:** quando si esegue la migrazione dei client da una gerarchia di origine che esegue una versione supportata di Configuration Manager, il software client esegue l'aggiornamento alla versione client per la gerarchia di destinazione.  

-   **System Center 2012 Configuration Manager o gerarchia di origine successiva:** quando si esegue la migrazione dei client tra gerarchie della stessa versione prodotto, il software client non esegue modifiche o aggiornamenti. Il client esegue invece la riassegnazione dalla gerarchia di origine a un sito della gerarchia di destinazione.  

    > [!NOTE]  
    >  Quando la versione prodotto di una gerarchia non è supportata per la migrazione alla gerarchia di destinazione, aggiornare a una versione prodotto compatibile tutti i siti e i client nella gerarchia di origine. Dopo che la gerarchia di origine è stata aggiornata alla versione prodotto supportata, è possibile eseguire la migrazione tra le gerarchie. Per altre informazioni, vedere [Versioni di Configuration Manager supportate per la migrazione](../../core/migration/prerequisites-for-migration.md#BKMK_SupportedMigrationVersions) in [Prerequisiti per la migrazione](../../core/migration/prerequisites-for-migration.md).  

Per pianificare la migrazione client, utilizzare le seguenti informazioni:  

-   Per aggiornare o riassegnare i client da un sito di origine a un sito di destinazione, utilizzare qualsiasi metodo di distribuzione client supportato per la distribuzione dei client nella gerarchia di destinazione. I metodi di distribuzione client tipici includono l'installazione push client, la distribuzione software, i criteri di gruppo e l'installazione client basata su aggiornamento software. Per altre informazioni, vedere [Metodi di installazione client](../../core/clients/deploy/plan/client-installation-methods.md).  

-   Verificare che il dispositivo che esegue il software client nella gerarchia di origine soddisfi i requisiti hardware minimi ed esegua un sistema operativo supportato dalla versione di Configuration Manager nella gerarchia di destinazione.  

-   Prima della migrazione di un client, eseguire un processo di migrazione delle informazioni che il client userà nella gerarchia di destinazione.  

-   I client che vengono aggiornati mantengono la cronologia di esecuzione per le distribuzioni. In questo modo si evitano riesecuzioni non necessarie delle distribuzioni nella gerarchia di destinazione.  

    -   Per i client di Configuration Manager 2007, viene mantenuta la cronologia di esecuzione degli annunci.  

    -   Per i client System Center 2012 Configuration Manager o Configuration Manager Current Branch viene mantenuta la cronologia di esecuzione delle distribuzioni.  

-   È possibile migrare i client da siti della gerarchia di origine nell'ordine desiderato. È tuttavia consigliabile optare per una migrazione a più fasi di quantità limitate di client, invece che per un'unica migrazione di ampie quantità di client. Una migrazione a più fasi consente di ridurre i requisiti di larghezza di banda di rete e l'elaborazione del server quando i nuovi client aggiornati inviano tutti i dati di conformità e di inventario iniziali al sito assegnato.  

-   Quando si esegue la migrazione dei client Configuration Manager 2007, il software client esistente viene disinstallato dal computer client e viene installato il software client nuovo.  

-   Configuration Manager non può eseguire la migrazione di un client Configuration Manager 2007 in cui è installato il client App-V, se la versione del client App-V non è 4.6 SP1 o successiva.  

È possibile monitorare il processo di migrazione client nel nodo **Migrazione** dell'area di lavoro **Amministrazione** nella console di Configuration Manager.  

Dopo la migrazione del client nella gerarchia di destinazione, non è più possibile gestire il dispositivo usando la gerarchia di origine ed è necessario valutare la rimozione del client dalla gerarchia di origine. Benché non si tratti di un requisito relativo alla migrazione tra gerarchie, questo consente di impedire il rilevamento di un client migrato in un report della gerarchia di origine o un conteggio errato delle risorse tra le due gerarchie durante la migrazione. Quando ad esempio un client migrato rimane nel database del sito di origine, è possibile eseguire un report degli aggiornamenti software che rileva erroneamente il computer come risorsa non gestita, sebbene il computer sia ora gestito dalla gerarchia di destinazione.  

##  <a name="plan-to-handle-data-maintained-on-clients-during-migration"></a><a name="Planning_for_Client_Data_Migration"></a> Pianificare la gestione dei dati conservati nei client durante la migrazione  
Quando si esegue la migrazione di un client dalla gerarchia di origine alle gerarchia di destinazione, alcune informazioni vengono conservate nel dispositivo, mentre altre informazioni non sono più disponibili nel dispositivo dopo la migrazione.  

Le seguenti informazioni vengono conservate nel dispositivo client:  

-   Identificatore univoco (GUID), che associa un client alle relative informazioni nel database di Configuration Manager.  

-   La cronologia degli annunci o delle distribuzioni, che impedisce ai client di rieseguire inutilmente gli annunci o le distribuzioni nella gerarchia di destinazione.  

Le seguenti informazioni non vengono conservate nel dispositivo client:  

-   I file nella cache del client. Se il client richiede tali file per l'installazione del software, li scarica nuovamente dalla gerarchia di destinazione.  

-   Le informazioni della gerarchia di origine relative a tutti gli annunci o le distribuzioni non ancora eseguite. Se si desidera che il client esegua gli annunci o le distribuzioni dopo la migrazione, è necessario rieseguire la distribuzione al client nella gerarchia di destinazione.  

-   Le informazioni relative all'inventario. Il client reinvia queste informazioni al sito assegnato nella gerarchia di destinazione al termine della migrazione del client e della generazione dei nuovi dati del client.  

-   Dati di conformità. Il client reinvia queste informazioni al sito assegnato nella gerarchia di destinazione al termine della migrazione del client e della generazione dei nuovi dati del client.  

Quando un client esegue la migrazione, le informazioni archiviate nel Registro di sistema del client di Configuration Manager e il percorso del file non vengono mantenuti. Dopo la migrazione, è necessario applicare nuovamente tali impostazioni. Le impostazioni tipiche includono:  

-   Combinazioni risparmio energia  

-   Impostazioni di registrazione  

-   Impostazioni del criterio locale  

Inoltre, potrebbe essere necessario reinstallare alcune applicazioni.  

##  <a name="plan-for--inventory-and-compliance-data-during-migration"></a><a name="Planning_for_Inventory_data_migration"></a> Pianificare i dati di inventario e di conformità durante la migrazione  
I dati di inventario e di conformità del client non vengono salvati quando si esegue la migrazione di un client nella gerarchia di destinazione. Queste informazioni vengono invece ricreate nella gerarchia di destinazione quando un client invia le proprie informazioni al sito assegnato. Per ridurre i requisiti di larghezza di banda di rete e l'elaborazione del server, valutare una migrazione a più fasi di quantità limitate di client, anziché un'unica migrazione di ampie quantità di client.  

 Non è inoltre possibile eseguire la migrazione di personalizzazioni per l'inventario hardware da una gerarchia di origine. È necessario introdurre tali personalizzazioni nella gerarchia di destinazione indipendentemente dalla migrazione. Per altre informazioni su come estendere l'inventario hardware, vedere [Come configurare l'inventario hardware](../../core/clients/manage/inventory/configure-hardware-inventory.md).  
