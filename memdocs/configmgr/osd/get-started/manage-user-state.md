---
title: Gestire lo stato utente
titleSuffix: Configuration Manager
description: Configuration Manager usa l'Utilità di migrazione stato utente per acquisire e ripristinare i dati sullo stato utente negli scenari di distribuzione del sistema operativo.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: d8d5c345-1e91-410b-b8a9-0170dcfa846e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0a720c68fc705187dedb6ff04fc3898a8b0b21c8
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124364"
---
# <a name="manage-user-state-in-configuration-manager"></a>Gestire lo stato utente in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

È possibile usare le sequenze attività di Configuration Manager per acquisire e ripristinare i dati sullo stato utente in scenari di distribuzione del sistema operativo in cui si desidera mantenere lo stato utente del sistema operativo corrente. Ad esempio:  

- Distribuzioni in cui si vuole acquisire lo stato utente da un computer per ripristinarlo in un altro computer.  

- Distribuzioni di aggiornamenti in cui si desidera acquisire e ripristinare lo stato utente sullo stesso computer.  

Configuration Manager usa l'Utilità di migrazione stato utente (USMT) 10.0 per gestire la migrazione dei dati sullo stato utente da un computer di origine a un computer di destinazione al termine dell'installazione del sistema operativo. Per altre informazioni sugli scenari comuni di migrazione per USMT 10.0 vedere  [Scenari di migrazione comuni](https://docs.microsoft.com/windows/deployment/usmt/usmt-common-migration-scenarios).

Vedere le sezioni seguenti per informazioni sull'acquisizione e sul ripristino dei dati utente.

## <a name="store-user-state-data"></a><a name="BKMK_StoringUserData"></a> Archiviare i dati dello stato utente

 Quando si acquisisce lo stato utente, è possibile archiviare i dati corrispondenti nel computer di destinazione o in un punto di migrazione stato. Per archiviare lo stato utente in un punto di migrazione stato utente, è necessario usare un server di sistema del sito di Configuration Manager che ospita il ruolo di sistema del sito del punto di migrazione stato. Per archiviare lo stato utente nel computer di destinazione, è necessario configurare la sequenza attività in modo da archiviare i dati localmente utilizzando i collegamenti.

> [!NOTE]
> I collegamenti utilizzati per archiviare lo stato utente localmente vengono definiti collegamenti reali. I collegamenti reali sono una funzionalità di USMT 10.0 che cerca nel computer i file e le impostazioni utente e quindi crea una directory di collegamenti reali a questi file. I collegamenti reali vengono quindi utilizzati per ripristinare i dati utente dopo la distribuzione del nuovo sistema operativo.

> [!IMPORTANT]
> Non è possibile utilizzare un punto di migrazione stato e utilizzare i collegamenti reali per archiviare i dati dello stato utente nello stesso momento.

Quando vengono acquisite le informazioni sullo stato utente, le informazioni possono essere memorizzate in uno dei modi seguenti:  

- È possibile memorizzare i dati di stato utente in remoto configurando un punto di migrazione stato. La sequenza di attività di **acquisizione** invia i dati al punto di migrazione stato. Dopo aver distribuito il sistema operativo, la sequenza di attività di **ripristino** recupera i dati e ripristina lo stato utente nel computer di destinazione.  

- È possibile memorizzare i dati dello stato utente in una posizione specifica in locale. In questo scenario la sequenza di attività di **acquisizione** copia i dati utente in una posizione specifica nel computer di destinazione. Dopo aver distribuito il sistema operativo, la sequenza di attività di **ripristino** recupera i dati e ripristina lo stato utente da tale posizione.  

- È possibile specificare i collegamenti reali che possono essere usati per ripristinare i dati utente e la relativa posizione originale. In questo scenario i dati dello stato utente rimangono sull'unità quando viene rimosso il sistema operativo precedente. Dopo aver distribuito il sistema operativo, la sequenza di attività di **ripristino** usa quindi i collegamenti reali per ripristinare i dati dello stato utente nella posizione originale.  

### <a name="store-user-data-on-a-state-migration-point"></a><a name="BKMK_UserDataSMP"></a> Archiviare i dati utente in un punto di migrazione stato

 Per archiviare i dati dello stato utente in un punto di migrazione stato, è necessario procedere come segue:  

1. [Configure a state migration point](#BKMK_StateMigrationPoint) per archiviare i dati dello stato utente.  

1. [Create a computer association](#BKMK_ComputerAssociation) tra il computer di origine e il computer di destinazione. Prima di acquisire lo stato utente nel computer di origine, è necessario creare questa associazione.  

1. [Creare una sequenza di attività per acquisire e ripristinare lo stato utente](../deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md). In particolare, è necessario aggiungere i passaggi della sequenza di attività seguenti per acquisire dati utente da un computer, archiviarli in un punto di migrazione stato e ripristinarli in un computer:  

    - [Richiedi archiviazione stati](../understand/task-sequence-steps.md#BKMK_RequestStateStore) per richiedere l'accesso a un punto di migrazione stato durante l'acquisizione dello stato da un computer o il ripristino dello stato in un computer.  

    - [Acquisisci stato utente](../understand/task-sequence-steps.md#BKMK_CaptureUserState) per acquisire e archiviare i dati sullo stato utente nel punto di migrazione stato.  

    - [Ripristina stato utente](../understand/task-sequence-steps.md#BKMK_RestoreUserState) per ripristinare lo stato utente nel computer di destinazione recuperando i dati da un punto di migrazione stato utente.  

    - [Rilascia archiviazione stati](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore) per notificare il completamento dell'azione di ripristino o acquisizione al punto di migrazione stato.  

### <a name="store-user-data-locally"></a><a name="BKMK_UserDataDestination"></a> Archiviare localmente i dati utente

 Per archiviare i dati dello stato utente localmente, è necessario procedere come segue:  

- [Creare una sequenza di attività per acquisire e ripristinare lo stato utente](../deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md). In particolare, è necessario aggiungere i passaggi della sequenza di attività seguenti per acquisire i dati utente da un computer e ripristinarli in un computer usando collegamenti reali.

  - [Acquisisci stato utente](../understand/task-sequence-steps.md#BKMK_CaptureUserState) per acquisire e archiviare i dati sullo stato utente in una cartella locale usando collegamenti reali.  

  - [Ripristina stato utente](../understand/task-sequence-steps.md#BKMK_RestoreUserState) per ripristinare lo stato utente nel computer di destinazione recuperando i dati tramite collegamenti reali.  

    > [!NOTE]
    > I dati dello stato utente a cui fanno riferimento i collegamenti reali rimangono nel computer dopo che la sequenza attività ha rimosso il sistema operativo precedente. Si tratta dei dati utilizzati per ripristinare lo stato utente quando viene distribuito il nuovo sistema operativo.  

## <a name="configure-a-state-migration-point"></a><a name="BKMK_StateMigrationPoint"></a> Configure a state migration point

Il punto di migrazione stato archivia i dati sullo stato dell'utente acquisiti in un computer e quindi ripristinati in un altro computer. Tuttavia, quando si acquisiscono le impostazioni utente per una distribuzione del sistema operativo nello stesso computer, ad esempio una distribuzione in cui il sistema operativo viene aggiornato nel computer di destinazione, è possibile archiviare i dati nello stesso computer con collegamenti reali oppure in un punto di migrazione stato. Per alcune distribuzioni di computer, quando viene creata l'archiviazione stati, Configuration Manager crea automaticamente un'associazione tra l'archiviazione stati e il computer di destinazione. Per configurare un punto di migrazione stato per archiviare i dati dello stato utente, è possibile utilizzare i metodi seguenti:  

- Utilizzare la **Creazione guidata server del sistema sito** per creare un nuovo server di sistema del sito per il punto di migrazione stato.  

- Utilizzare l' **Aggiunta guidata ruoli del sistema del sito** per aggiungere un punto di migrazione stato a un server esistente.  

  Quando si utilizzano queste procedure guidate, viene richiesto di fornire le informazioni seguenti per il punto di migrazione stato:  

- Cartelle in cui archiviare i dati dello stato utente.  

- Numero massimo di client che possono archiviare i dati nel punto di migrazione stato.  

- Spazio minimo disponibile per il punto di migrazione stato in cui archiviare i dati sullo stato utente.  

- Criteri di eliminazione per il ruolo. È possibile specificare che i dati dello stato utente vengano eliminati immediatamente dopo il ripristino in un computer o dopo un numero specifico di giorni dopo il ripristino dei dati utente in un computer.  

- Se il punto di migrazione stato deve rispondere solo alle richieste di ripristino dei dati dello stato utente. Quando si abilita questa opzione, non è possibile utilizzare il punto di migrazione stato per archiviare dati dello stato utente.  

  Per altre informazioni sul punto di migrazione stato e sui passaggi per configurarlo, vedere [Punto di migrazione stato](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints).  

## <a name="create-a-computer-association"></a><a name="BKMK_ComputerAssociation"></a> Create a computer association

Creare un'associazione computer per definire una relazione tra un computer di origine e un computer di destinazione quando si installa un sistema operativo su hardware nuovo e si vogliono acquisire e ripristinare le impostazioni dei dati utente. Il computer di origine è un computer esistente gestito da Configuration Manager. Quando si distribuisce il nuovo sistema operativo nel computer di destinazione, il computer di origine contiene lo stato utente di cui viene eseguita la migrazione al computer di destinazione.  

> [!NOTE]  
> Non è supportata la creazione di un'associazione computer tra computer che si trovano in un sito padre di Configuration Manager e computer in un sito figlio. Le associazioni computer sono specifiche del sito e non vengono replicate.  

### <a name="to-create-a-computer-association"></a>Per creare un'associazione computer

1. Nella console di Configuration Manager fare clic su **Asset e conformità**.  

1. Nell'area di lavoro **Asset e conformità** fare clic su **Migrazione stato utente**.  

1. Nel gruppo **Crea** della scheda **Home** fare clic su **Crea associazione di computer**.  

1. Nella scheda **Associazione computer** della finestra di dialogo **Proprietà associazione computer** specificare il computer di origine di cui è necessario acquisire lo stato utente e il computer di destinazione in cui ripristinare i dati dello stato utente.  

1. Nella scheda **Account utente** specificare gli account utente di cui eseguire la migrazione nel computer di destinazione. Specificare una delle impostazioni seguenti:  

    - **Acquisisci e ripristina tutti gli account utente**: questa impostazione consente di acquisire e ripristinare tutti gli account utente. Utilizzare questa impostazione per creare più associazioni con lo stesso computer di origine.  

    - **Acquisisci tutti gli account utente e ripristina gli account specificati**: questa impostazione consente di acquisire tutti gli account utente nel computer di origine e di ripristinare solo gli account specificati nel computer di destinazione. Inoltre, è possibile utilizzare questa impostazione quando si desidera creare più associazioni con lo stesso computer di origine.  

    - **Acquisisci e ripristina gli account utente specificati**: questa impostazione consente di acquisire e ripristinare solo gli account specificati. Quando si seleziona questa impostazione, non è possibile creare più associazioni con lo stesso computer di origine.  

## <a name="restore-user-state-data-when-an-operating-system-deployment-fails"></a><a name="BKMK_MigrationFails"></a> Ripristinare i dati dello stato utente in caso di errore di distribuzione del sistema operativo

Se la distribuzione del sistema operativo non riesce, usare la funzionalità USMT 10.0 LoadState per recuperare i dati dello stato utente acquisito durante il processo di distribuzione. Sono inclusi i dati memorizzati su un punto di migrazione dello stato o i dati salvati localmente sul computer di destinazione. Per ulteriori informazioni su questa caratteristica di USMT, vedere [Sintassi di LoadState](https://docs.microsoft.com/windows/deployment/usmt/usmt-loadstate-syntax).
