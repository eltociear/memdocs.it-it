---
title: Acquisire e ripristinare lo stato utente
titleSuffix: Configuration Manager
description: Usare le sequenze di attività di Configuration Manager per acquisire e ripristinare i dati dello stato utente in scenari di distribuzione del sistema operativo.
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: d566d85c-bf7a-40e7-8239-57640a1db5f4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 93a39ba21b9e7d6cacfe59f763756aeef3736d52
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707349"
---
# <a name="create-a-task-sequence-to-capture-and-restore-user-state-in-configuration-manager"></a>Creare una sequenza di attività per acquisire e ripristinare lo stato utente in Configuration Manager

 *Si applica a: Configuration Manager (Current Branch)*

 Usare le sequenze di attività di Configuration Manager per acquisire e ripristinare i dati dello stato utente in scenari di distribuzione del sistema operativo. In questi scenari, si vuole mantenere lo stato utente del sistema operativo corrente. A seconda del tipo di sequenza di attività che si crea, è possibile aggiungervi automaticamente i passaggi di acquisizione e ripristino. In altri scenari potrebbe essere necessario aggiungere manualmente i passaggi di acquisizione e ripristino alla sequenza di attività. Questo articolo descrive i passaggi che è necessario aggiungere a una sequenza di attività esistente per acquisire e ripristinare i dati dello stato utente.  



## <a name="task-sequence-steps"></a>Passaggi della sequenza di attività  

Per acquisire e ripristinare lo stato utente, aggiungere i passaggi seguenti alla sequenza di attività:  

- [Richiedi archiviazione stati](../understand/task-sequence-steps.md#BKMK_RequestStateStore): questo passaggio è necessario se si archivia lo stato utente nel punto di migrazione stato.  

- [Acquisisci stato utente](../understand/task-sequence-steps.md#BKMK_CaptureUserState): questo passaggio consente di acquisire i dati dello stato utente. Archivia quindi i dati nel punto di migrazione stato o nel disco locale usando collegamenti reali.  

- [Ripristina stato utente](../understand/task-sequence-steps.md#BKMK_RestoreUserState): Questo passaggio consente di ripristinare i dati dello stato utente nel computer di destinazione. Consente di recuperare i dati da un punto di migrazione stato utente o nel disco locale nel caso di collegamenti reali.  

- [Rilascia archiviazione stati](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore): questo passaggio è necessario se si archivia lo stato utente nel punto di migrazione stato. Questo passaggio consente di rimuovere i dati dal punto di migrazione stato.  


 Usare le procedure seguenti per aggiungere i passaggi della sequenza di attività necessari per acquisire e ripristinare lo stato utente. Per altre informazioni sulla creazione di una sequenza di attività, vedere [Gestire le sequenze di attività per automatizzare le attività](manage-task-sequences-to-automate-tasks.md).  



## <a name="capture-the-user-state"></a>Acquisire lo stato utente  

 Per aggiungere i passaggi della sequenza di attività per acquisire lo stato utente, seguire questa procedura:

1.  Nell'elenco **Sequenza attività** selezionare una sequenza attività, quindi fare clic su **Modifica**.  

2.  Se si usa un punto di migrazione stato per archiviare lo stato utente, aggiungere il passaggio **Richiedi archiviazione stati** alla sequenza di attività. In **Editor della sequenza di attività** fare clic su **Aggiungi**. Scegliere **Stato utente** e quindi fare clic su **Richiedi archiviazione stati**. Configurare le proprietà e le opzioni per questo passaggio, quindi fare clic su **Applica**. Per altre informazioni sulle impostazioni disponibili, vedere [Richiedi archiviazione stati](../understand/task-sequence-steps.md#BKMK_RequestStateStore).  

3.  Aggiungere il passaggio **Acquisisci stato utente** alla sequenza attività. In **Editor della sequenza di attività** fare clic su **Aggiungi**. Scegliere **Stato utente** e quindi fare clic su **Acquisisci stato utente**. Configurare le proprietà e le opzioni per questo passaggio, quindi fare clic su **Applica**. Per altre informazioni sulle impostazioni disponibili, vedere [Acquisisci stato utente](../understand/task-sequence-steps.md#BKMK_CaptureUserState).  

    > [!IMPORTANT]  
    >  Quando si aggiunge questo passaggio alla sequenza di attività, impostare anche la variabile della sequenza di attività **OSDStateStorePath** per specificare dove archiviare i dati dello stato utente. Se si archivia lo stato utente localmente, non specificare una cartella radice perché potrebbe verificarsi un errore nella sequenza di attività. Quando si archiviano i dati utente localmente, utilizzare sempre una cartella o una sottocartella. Per altre informazioni su questa variabile, vedere [Variabili della sequenza di attività](../understand/task-sequence-variables.md#OSDStateStorePath).  

4.  Se si usa un punto di migrazione stato, aggiungere il passaggio **Rilascia archiviazione stati** alla sequenza di attività. In **Editor della sequenza di attività** fare clic su **Aggiungi**. Scegliere **Stato utente** e quindi fare clic su **Rilascia archiviazione stati**. Configurare le proprietà e le opzioni per questo passaggio, quindi fare clic su **Applica**. Per altre informazioni sulle impostazioni disponibili, vedere [Rilascia archiviazione stati](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore).  

    > [!IMPORTANT]  
    >  È necessario che l'azione della sequenza attività eseguita prima del passaggio **Rilascia archiviazione stati** abbia esito positivo prima dell'avvio del passaggio **Rilascia archiviazione stati**.  


 Distribuire questa sequenza attività per acquisire lo stato utente in un computer di destinazione. Per altre informazioni su come distribuire sequenze di attività, vedere [Distribuire una sequenza di attività](deploy-a-task-sequence.md).  



## <a name="restore-the-user-state"></a>Ripristinare lo stato utente  

 Per aggiungere i passaggi della sequenza di attività per ripristinare lo stato utente, seguire questa procedura:

1. Nell'elenco **Sequenza attività** selezionare una sequenza attività, quindi fare clic su **Modifica**.  

2. Aggiungere il passaggio **Ripristina stato utente** alla sequenza attività. In **Editor della sequenza di attività** fare clic su **Aggiungi**. Scegliere **Stato utente** e quindi fare clic su **Ripristina stato utente**. Questo passaggio stabilisce una connessione al punto di migrazione dello stato, se necessario. Configurare le proprietà e le opzioni per questo passaggio, quindi fare clic su **Applica**. Per altre informazioni sulle impostazioni disponibili, vedere [Ripristina stato utente](../understand/task-sequence-steps.md#BKMK_RestoreUserState).  

   > [!Important]  
   >  Quando si usa il passaggio [Acquisisci stato utente](../understand/task-sequence-steps.md#BKMK_CaptureUserState) con l'opzione **Acquisisci tutti i profili utente utilizzando le opzioni standard** selezionata, è necessario selezionare l'impostazione **Ripristina profili utente del computer locale** nel passaggio **Ripristina stato utente**. In caso contrario, la sequenza di attività avrà esito negativo.  

   > [!Note]  
   > Se lo stato utente viene archiviato tramite collegamenti reali locali e il ripristino ha esito negativo, è possibile eliminare manualmente i collegamenti reali creati per l'archiviazione dei dati. La sequenza di attività può eseguire lo strumento USMTUtils per automatizzare questa azione con un passaggio [Esegui riga di comando](../understand/task-sequence-steps.md#BKMK_RunCommandLine). Se si usa USMTUtils per eliminare il collegamento reale, aggiungere un passaggio [Riavvia computer](../understand/task-sequence-steps.md#BKMK_RestartComputer) dopo l'esecuzione di USMTUtils.  

3. Se si usa un punto di migrazione stato per archiviare lo stato utente, aggiungere il passaggio **Rilascia archiviazione stati** alla sequenza di attività. In **Editor della sequenza di attività** fare clic su **Aggiungi**. Scegliere **Stato utente** e quindi fare clic su **Rilascia archiviazione stati**. Configurare le proprietà e le opzioni per questo passaggio, quindi fare clic su **Applica**. Per altre informazioni sulle impostazioni disponibili, vedere [Rilascia archiviazione stati](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore).  

   > [!IMPORTANT]  
   >  È necessario che l'azione della sequenza attività eseguita prima del passaggio **Rilascia archiviazione stati** abbia esito positivo prima dell'avvio del passaggio **Rilascia archiviazione stati**.  


 Distribuire questa sequenza attività per ripristinare lo stato utente in un computer di destinazione. Per informazioni sulla distribuzione di sequenze di attività, vedere [Distribuire una sequenza di attività](deploy-a-task-sequence.md).  



## <a name="next-steps"></a>Passaggi successivi

[Monitorare la distribuzione della sequenza di attività](monitor-operating-system-deployments.md#BKMK_TSDeployStatus)
