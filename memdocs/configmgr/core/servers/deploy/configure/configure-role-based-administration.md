---
title: Configurare l'amministrazione basata su ruoli
titleSuffix: Configuration Manager
ms.date: 11/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 57413dd3-b2f8-4a5f-b27f-8464d357caff
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 14258c3e7e2cfe5423b97064a26fdf5616d6b0a4
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078618"
---
# <a name="configure-role-based-administration-for-configuration-manager"></a>Configurare l'amministrazione basata su ruoli per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

In Configuration Manager l'amministrazione basata su ruoli combina ruoli di sicurezza, ambiti di protezione e raccolte assegnate per definire l'ambito amministrativo per ogni utente amministratore. L'ambito amministrativo comprende gli oggetti che possono essere visualizzati da un utente amministratore nella console di Configuration Manager, nonché le attività relative a tali oggetti eseguibili dall'utente amministratore. Le configurazioni dell'amministrazione basata su ruoli vengono applicate a tutti i siti della gerarchia.  

 Se non si ha ancora familiarità con i concetti dell'amministrazione basata su ruoli, vedere [Nozioni fondamentali di amministrazione basata su ruoli](../../../understand/fundamentals-of-role-based-administration.md).  

 Le informazioni contenute nelle seguenti procedure consentono di creare e configurare l'amministrazione basata su ruoli e le relative impostazioni di sicurezza:  

- [Creare ruoli di sicurezza personalizzati](#BKMK_CreateSecRole)  
- [Configurare i ruoli di sicurezza](#BKMK_ConfigSecRole)  
- [Configurare gli ambiti di protezione per un oggetto](#BKMK_ConfigSecScope)  
- [Configurare le raccolte per la gestione della sicurezza](#BKMK_ConfigColl)  
- [Creare un nuovo utente amministratore](#BKMK_Create_AdminUser)  
- [Modificare l'ambito amministrativo di un utente amministratore](#BKMK_ModAdminUser)  

## <a name="create-custom-security-roles"></a><a name="BKMK_CreateSecRole"></a> Creare ruoli di sicurezza personalizzati

 Configuration Manager fornisce diversi ruoli di sicurezza predefiniti. Se sono necessari ruoli di sicurezza aggiuntivi, è possibile creare un ruolo di sicurezza personalizzato creando una copia di un ruolo di sicurezza esistente e, in seguito, modificando tale copia. È possibile creare un ruolo di sicurezza personalizzato per concedere agli utenti amministratori le autorizzazioni di sicurezza necessarie non incluse in un ruolo di sicurezza attualmente assegnato. Utilizzando un ruolo di sicurezza personalizzato, è possibile concedere soltanto le autorizzazioni richieste, evitando di assegnare un ruolo di sicurezza che conceda più autorizzazioni del necessario.  

 Utilizzare la seguente procedura per creare un nuovo ruolo di sicurezza utilizzando un ruolo di sicurezza esistente come modello.  

### <a name="to-create-custom-security-roles"></a>Per creare ruoli di sicurezza personalizzati

1. Nella console di Configuration Manager passare ad **Amministrazione**.  

2. Nell'area di lavoro **Amministrazione** espandere **Sicurezza** e quindi scegliere **Ruoli di protezione**.  

   Per creare il nuovo ruolo di sicurezza, utilizzare uno dei seguenti processi:  

    - Per creare un nuovo ruolo di sicurezza personalizzato, eseguire le seguenti azioni:  

      1. Selezionare un ruolo di sicurezza esistente da utilizzare come origine per il nuovo ruolo di sicurezza.
      2. Nel gruppo **Ruolo di protezione** della scheda **Home** scegliere **Copia**. Viene creata una copia del ruolo di sicurezza di origine.  
      3. Nella procedura guidata Copia ruolo di protezione, specificare un **Nome** per il nuovo ruolo di sicurezza personalizzato.  
      4. In **Assegnazioni operazioni di protezione**, espandere ciascun nodo **Operazioni di protezione** per visualizzare le azioni disponibili.  
      5. Per modificare l'impostazione per un'operazione di protezione, scegliere la freccia in giù nella colonna **Valore** e scegliere **Sì** o **No**.

            > [!CAUTION]  
            > Quando viene configurato un ruolo di sicurezza personalizzato, assicurarsi di non concedere autorizzazioni non richieste dagli utenti amministratori associati al nuovo ruolo di sicurezza. Il valore **Modifica** per l'operazione di protezione **Ruoli di protezione**, ad esempio, concede agli utenti amministratori l'autorizzazione per la modifica di qualsiasi ruolo di sicurezza accessibile, anche se tali utenti non sono associati a quello specifico ruolo di sicurezza.  

      6. Dopo la configurazione delle autorizzazioni, scegliere **OK** per salvare il nuovo ruolo di sicurezza.  

    - Per importare un ruolo di sicurezza esportato da un altra gerarchia di Configuration Manager, eseguire le azioni seguenti:  

        1. Nel gruppo **Crea** della scheda **Home** scegliere **Importa ruolo di protezione**.  
        2. Specificare il file XML contenente la configurazione del ruolo di sicurezza da importare. Scegliere **Apri** per completare la procedura e salvare il ruolo di sicurezza.  

            > [!NOTE]  
            > Dopo l'importazione di un ruolo di sicurezza, è possibile modificare le proprietà del ruolo di sicurezza per modificare le autorizzazioni oggetto associate al ruolo di sicurezza.  

## <a name="configure-security-roles"></a><a name="BKMK_ConfigSecRole"></a> Configurare i ruoli di sicurezza

 I gruppi di autorizzazioni di sicurezza definiti per un ruolo di sicurezza vengono chiamati assegnazioni delle operazioni di protezione. Le assegnazioni delle operazioni di protezione rappresentano una combinazione di tipi di oggetti e azioni disponibili per ciascun tipo di oggetto. È possibile modificare le operazioni di protezione disponibili per qualsiasi ruolo di sicurezza personalizzato, mentre non è possibile modificare i ruoli di sicurezza predefiniti forniti da Configuration Manager.  

 Utilizzare la seguente procedura per modificare le operazioni di protezione per un ruolo di sicurezza.  

### <a name="to-modify-security-roles"></a>Per modificare i ruoli di sicurezza

1. Nella console di Configuration Manager scegliere **Amministrazione**.  
2. Nell'area di lavoro **Amministrazione** espandere **Sicurezza** e quindi scegliere **Ruoli di protezione**.  
3. Selezionare il ruolo di sicurezza personalizzato che si desidera modificare.  
4. Nella scheda **Home**, nel gruppo **Proprietà**, fare clic su **Proprietà**.  
5. Scegliere la scheda **Autorizzazioni**.  
6. In **Assegnazioni operazioni di protezione**, espandere ciascun nodo **Operazioni di protezione** per visualizzare le azioni disponibili.  
7. Per modificare l'impostazione per un'operazione di protezione, scegliere la freccia in giù nella colonna **Valore** e quindi scegliere **Sì** o **No**.  

    > [!CAUTION]  
    > Quando viene configurato un ruolo di sicurezza personalizzato, assicurarsi di non concedere autorizzazioni non richieste dagli utenti amministratori associati al nuovo ruolo di sicurezza. Il valore **Modifica** per l'operazione di protezione **Ruoli di protezione**, ad esempio, concede agli utenti amministratori l'autorizzazione per la modifica di qualsiasi ruolo di sicurezza accessibile, anche se tali utenti non sono associati a quello specifico ruolo di sicurezza.  

8. Al termine della configurazione delle assegnazioni delle operazioni di protezione, scegliere **OK** per salvare il nuovo ruolo di sicurezza.  

##  <a name="configure-security-scopes-for-an-object"></a><a name="BKMK_ConfigSecScope"></a> Configurare gli ambiti di protezione per un oggetto
 L'associazione di un ambito di protezione per un oggetto si gestisce dall'oggetto e non dall'ambito di protezione. Le uniche configurazioni dirette supportate dagli ambiti di protezione sono le modifiche apportate al nome e alla descrizione. Per modificare il nome e la descrizione di un ambito di protezione durante la visualizzazione delle proprietà dell'ambito di protezione, è necessario disporre dell'autorizzazione **Modifica** per l'oggetto a protezione diretta **Ambiti di protezione** .  

 Quando si crea un nuovo oggetto in Configuration Manager, viene associato a ogni ambito di sicurezza che è associato ai ruoli di sicurezza dell'account usato per creare l'oggetto. Questo comportamento si verifica quando i ruoli di sicurezza forniscono l'autorizzazione **Crea** oppure l'autorizzazione **Imposta ambito di protezione**. È possibile modificare gli ambiti di sicurezza per l'oggetto dopo averlo creato.  

 Si supponga ad esempio che all'utente venga assegnato un ruolo di sicurezza che concede l'autorizzazione per creare un nuovo gruppo di limiti. Quando si crea un nuovo gruppo di limiti, non esiste nessuna opzione a cui è possibile assegnare ambiti di protezione specifici. Gli ambiti di protezione disponibili relativamente ai ruoli di sicurezza a cui è associato l'utente vengono invece assegnati automaticamente al nuovo gruppo di limiti. Dopo aver salvato il nuovo gruppo di limiti, è possibile modificare gli ambiti di protezione associati al nuovo gruppo di limiti.  

 Usare la procedura seguente per configurare gli ambiti di protezione assegnati a un oggetto.  

### <a name="to-configure-security-scopes-for-an-object"></a><a name="bkmk_config-sec-scope"></a> Per configurare gli ambiti di protezione per un oggetto  

1. Nella console di Configuration Manager selezionare un oggetto che supporta l'assegnazione a un ambito di protezione.  
2. Nel gruppo **Classificazione** della scheda **Home** scegliere **Imposta ambiti di protezione**.
3. Nella finestra di dialogo **Imposta ambiti di protezione** selezionare o deselezionare gli ambiti di protezione a cui è associato l'oggetto. Ogni oggetto che supporta gli ambiti di protezione deve essere assegnato almeno a un ambito di protezione.  
4. Scegliere **OK** per salvare gli ambiti di protezione assegnati.  

    > [!NOTE]  
    > Quando viene creato un nuovo oggetto, è possibile assegnare l'oggetto a più ambiti di protezione. Per modificare il numero di ambiti di protezione associati all'oggetto, è necessario modificare l'assegnazione dopo la creazione dell'oggetto.

### <a name="to-configure-security-scopes-for-a-folder-starting-in-version-1906"></a><a name="bkmk_config-folder"></a> Per configurare gli ambiti di protezione per una cartella (a partire dalla versione 1906)
<!--3600867-->

1. Nella console di Configuration Manager selezionare una cartella.  
1. Nella scheda **Cartella** nella barra multifunzione scegliere **Imposta ambiti di protezione**.
   - È anche possibile fare clic con il pulsante destro del mouse sulla cartella e scegliere **Cartella** > **Imposta ambiti di protezione**.
1. Nella finestra di dialogo **Imposta ambiti di protezione** selezionare o deselezionare gli ambiti di protezione per la cartella. È necessario assegnare almeno un ambito di protezione a ogni cartella. A tutte le cartelle è assegnato l'ambito di protezione **Predefinito** fino a quando non viene modificato.
1. Scegliere **OK** per salvare gli ambiti di protezione assegnati.  

    > [!IMPORTANT]  
    > - I ruoli di sicurezza esistenti otterranno automaticamente le autorizzazioni **Classe della cartella** aggiunte durante l'installazione di Configuration Manager versione 1906. È necessario aggiungere le autorizzazioni **Classe della cartella** per tutti i nuovi ruoli di sicurezza e verificare che i ruoli esistenti abbiano le autorizzazioni appropriate per l'ambiente.
    > 
    > - Un elemento è ricercabile in una cartella al di fuori dell'ambito di sicurezza di un utente se quest'ultimo condivide un ambito di sicurezza con la persona che ha creato l'oggetto. <!--5602690-->

## <a name="configure-collections-to-manage-security"></a><a name="BKMK_ConfigColl"></a> Configurare le raccolte per la gestione della sicurezza

 Non esistono procedure per la configurazione delle raccolte per l'amministrazione basata su ruoli. Le raccolte non hanno una configurazione dell'amministrazione basata su ruoli. Vengono invece assegnate a un utente amministratore durante la configurazione dell'utente amministratore. Le operazioni di protezione della raccolta abilitate nei ruoli di sicurezza assegnati degli utenti determinano le autorizzazioni di un utente amministratore per le raccolte e le risorse delle raccolte (membri delle raccolte).  

 Quando un utente amministratore dispone delle autorizzazioni per una raccolta, dispone anche delle autorizzazioni per le raccolte limitate alla raccolta specifica. Ad esempio, l'organizzazione usa una raccolta denominata All Desktops. È inoltre disponibile una raccolta denominata All North America Desktops, limitata alla raccolta All Desktops. Se un utente amministratore dispone delle autorizzazioni per All Desktops, avrà le stesse autorizzazioni anche per la raccolta All North America Desktops.

 Inoltre, un utente amministratore non può usare l'autorizzazione **Elimina** o **Modifica** in una raccolta che gli è stata assegnata direttamente. Può invece usare queste autorizzazioni sulle raccolte limitate alla raccolta specifica. Nell'esempio precedente, l'utente amministratore può eliminare o modificare la raccolta All North America Desktops, ma non può eliminare o modificare la raccolta All Desktops.  

## <a name="create-a-new-administrative-user"></a><a name="BKMK_Create_AdminUser"></a> Creare un nuovo utente amministratore

 Per consentire l'accesso a individui o membri di un gruppo di sicurezza per gestire Configuration Manager, creare un utente amministratore in Configuration Manager e specificare l'account Windows Utente o Gruppo utenti. È necessario assegnare a ogni utente amministratore in Configuration Manager almeno un ruolo di sicurezza e un ambito di protezione. È inoltre possibile assegnare delle raccolte per limitare l'ambito amministrativo dell'utente amministratore.  

 Utilizzare le seguenti procedure per creare nuovi utenti amministratori.  

### <a name="to-create-a-new-administrative-user"></a>Per creare un nuovo utente amministratore  

1. Nella console di Configuration Manager scegliere **Amministrazione**.  
2. Nell'area di lavoro **Amministrazione** espandere **Sicurezza** e quindi scegliere **Utenti amministratori**.  
3. Nel gruppo **Crea** della scheda **Home** scegliere **Aggiungi utente o gruppo**.  
4. Scegliere **Sfoglia** e quindi selezionare l'account utente o il gruppo da usare per il nuovo utente amministratore.  

    > [!NOTE]  
    > Per l'amministrazione basata su console, è possibile specificare solo utenti di dominio o gruppi di sicurezza come utente amministratore.

5. In **Ruoli di protezione assegnati** scegliere **Aggiungi** per aprire un elenco dei ruoli di sicurezza disponibili, selezionare la casella relativa a uno o più ruoli e quindi scegliere **OK**.  

6. Scegliere una delle due opzioni seguenti per definire il comportamento degli oggetti a protezione diretta per il nuovo utente:  

    - **Tutte le istanze degli oggetti collegati ai ruoli di protezione assegnati**: questa opzione associa l'utente amministratore all'ambito di protezione **Tutto** e alle raccolte **Tutti i sistemi** e **Tutti gli utenti e i gruppi utente**. I ruoli di sicurezza assegnati all'utente definiscono l'accesso agli oggetti. I nuovi oggetti creati dall'utente amministratore vengono assegnati all'ambito di protezione **Predefinito** .  

    - **Solo le istanze di oggetti assegnati alle raccolte o agli ambiti di protezione specificati**: per impostazione predefinita questa opzione associa l'utente amministratore all'ambito di protezione **Predefinito** e alle raccolte **Tutti i sistemi** e **Tutti gli utenti e i gruppi utente**. Tuttavia, le raccolte e gli ambiti di protezione effettivi sono limitati a quelli associati all'account utilizzato per creare il nuovo utente amministratore. Questa opzione supporta l'aggiunta o la rimozione di raccolte e ambiti di protezione per personalizzare l'ambito amministrativo dell'utente amministratore.  

    > [!IMPORTANT]  
    > Le opzioni precedenti associano ogni raccolta e ambito di protezione assegnati a ogni ruolo di sicurezza assegnato all'utente amministratore. È possibile usare una terza opzione, **Associa ruoli di protezione assegnati a raccolte e ambiti di protezione specifici**, per associare singoli ruoli di sicurezza a raccolte e ambiti di protezione specifici. Questa terza opzione è disponibile dopo aver creato il nuovo utente amministratore, quando si modifica l'utente amministratore.  

7. A seconda dell'opzione selezionata nel passaggio 6, eseguire le seguenti operazioni:  

    - Se si seleziona **Tutte le istanze degli oggetti collegati ai ruoli di protezione assegnati**, scegliere **OK** per completare questa procedura.  

    - Se si seleziona **Solo le istanze di oggetti assegnati alle raccolte o agli ambiti di protezione specificati**, è possibile scegliere **Aggiungi** per selezionare raccolte e ambiti di protezione aggiuntivi. In alternativa, selezionare uno o più oggetti nell'elenco e quindi scegliere **Rimuovi** per rimuoverli. Scegliere **OK** per completare questa procedura.  

## <a name="modify-the-administrative-scope-of-an-administrative-user"></a><a name="BKMK_ModAdminUser"></a> Modificare l'ambito amministrativo di un utente amministratore

 È possibile modificare l'ambito amministrativo di un utente amministratore aggiungendo o rimuovendo raccolte, ruoli di sicurezza e ambiti di protezione associati all'utente. È necessario associare a ogni utente amministratore almeno un ruolo di sicurezza e un ambito di protezione. Potrebbe essere necessario assegnare una o più raccolte all'ambito amministrativo dell'utente. La maggior parte dei ruoli di sicurezza interagisce con le raccolte e non funziona correttamente senza una raccolta assegnata.  

 Quando si modifica un utente amministratore, è possibile modificare il comportamento di associazione degli oggetti a protezione diretta ai ruoli di sicurezza assegnati. Di seguito, i tre comportamenti che è possibile selezionare:  

- **Tutte le istanze degli oggetti collegati ai ruoli di protezione assegnati**: questa opzione associa l'utente amministratore all'ambito **Tutto** e alle raccolte **Tutti i sistemi** e **Tutti gli utenti e i gruppi utente**. I ruoli di sicurezza assegnati all'utente definiscono l'accesso agli oggetti.  

- **Solo le istanze di oggetti assegnati alle raccolte o agli ambiti di protezione specificati**: questa opzione associa l'utente amministratore agli stessi ambiti di protezione e alle stesse raccolte associate all'account usato per configurare l'utente amministratore. Questa opzione supporta l'aggiunta o la rimozione di raccolte e ruoli di sicurezza per personalizzare l'ambito amministrativo dell'utente amministratore.  

- **Associa ruoli di protezione assegnati a raccolte e ambiti di protezione specifici**: questa opzione consente di creare associazioni specifiche tra raccolte, ruoli di sicurezza e ambiti di protezione specifici per l'utente.  

    > [!NOTE]  
    > Questa opzione è disponibile solo quando si modificano le proprietà di un utente amministratore.  

La configurazione corrente per il comportamento degli oggetti a protezione diretta modifica il processo utilizzato per assegnare i ruoli di sicurezza aggiuntivi. Utilizzare le seguenti procedure basate sulle diverse opzioni per gli oggetti a protezione diretta per gestire un utente amministratore.  

Usare la procedura seguente per visualizzare e gestire la configurazione per gli oggetti a protezione diretta per un utente amministratore.  

### <a name="to-view-and-manage-the-securable-object-behavior-for-an-administrative-user"></a>Per visualizzare e gestire il comportamento degli oggetti a protezione diretta per un utente amministratore  

1. Nella console di Configuration Manager scegliere **Amministrazione**.  
2. Nell'area di lavoro **Amministrazione** espandere **Sicurezza** e quindi scegliere **Utenti amministratori**.  
3. Selezionare l'utente amministratore che si desidera modificare.  
4. Nella scheda **Home**, nel gruppo **Proprietà**, fare clic su **Proprietà**.  
5. Scegliere la scheda **Ambiti di protezione** per visualizzare la configurazione corrente per gli oggetti a protezione diretta per questo utente amministratore.  
6. Per modificare il comportamento degli oggetti a protezione diretta, selezionare una nuova opzione per il comportamento di tali oggetti. Dopo aver modificato questa configurazione, vedere la procedura appropriata per altre informazioni sulla configurazione di raccolte, ambiti di protezione e ruoli di sicurezza per l'utente amministratore.  
7. Scegliere **OK** per completare la procedura.  

Usare la procedura seguente per modificare un utente amministratore con il comportamento degli oggetti a protezione diretta impostato su **Tutte le istanze degli oggetti collegati ai ruoli di protezione assegnati**.  

### <a name="for-option-all-instances-of-the-objects-that-are-related-to-the-assigned-security-roles"></a>Per l'opzione: Tutte le istanze degli oggetti collegati ai ruoli di protezione assegnati  

1. Nella console di Configuration Manager scegliere **Amministrazione**.  
2. Nell'area di lavoro **Amministrazione** espandere **Sicurezza** e quindi scegliere **Utenti amministratori**.  
3. Selezionare l'utente amministratore che si desidera modificare.  
4. Nella scheda **Home**, nel gruppo **Proprietà**, fare clic su **Proprietà**.  
5. Scegliere la scheda **Ambiti di protezione** per assicurarsi che l'utente amministratore sia configurato per **Tutte le istanze degli oggetti collegati ai ruoli di protezione assegnati**.  
6. Per modificare i ruoli di sicurezza assegnati, scegliere la scheda **Ruoli di protezione**.  

    - Per assegnare ruoli di sicurezza aggiuntivi all'utente amministratore, scegliere **Aggiungi**, selezionare la casella relativa a ogni ruolo di sicurezza aggiuntivo da assegnare e quindi scegliere **OK**.  
    - Per rimuovere i ruoli di sicurezza, selezionare uno o più ruoli di sicurezza nell'elenco e quindi scegliere **Rimuovi**.

7. Per modificare il comportamento degli oggetti a protezione diretta, scegliere la scheda **Ambiti di protezione** e scegliere una nuova opzione per il comportamento di tali oggetti. Dopo aver modificato questa configurazione, vedere la procedura appropriata per altre informazioni sulla configurazione di raccolte, ambiti di protezione e ruoli di sicurezza per l'utente amministratore.  

    > [!NOTE]  
    > Quando il comportamento degli oggetti a protezione diretta viene impostato su **Tutte le istanze degli oggetti collegati ai ruoli di protezione assegnati**, non è possibile aggiungere o rimuovere raccolte e ambiti di protezione specifici.  

8. Scegliere **OK** per completare questa procedura.  

Usare la procedura seguente per modificare un utente amministratore con il comportamento degli oggetti a protezione diretta impostato su **Solo le istanze di oggetti assegnati alle raccolte o agli ambiti di protezione specificati**.  

### <a name="for-option-only-the-instances-of-objects-that-are-assigned-to-the-specified-security-scopes-and-collections"></a>Per l'opzione: Solo le istanze di oggetti assegnati alle raccolte o agli ambiti di protezione specificati  

1. Nella console di Configuration Manager scegliere **Amministrazione**.  
2. Nell'area di lavoro **Amministrazione** espandere **Sicurezza** e quindi scegliere **Utenti amministratori**.  
3. Selezionare l'utente amministratore che si desidera modificare.  
4. Nella scheda **Home**, nel gruppo **Proprietà**, fare clic su **Proprietà**.  
5. Scegliere la scheda **Ambiti di protezione** per assicurarsi che l'utente sia configurato per **Solo le istanze di oggetti assegnati alle raccolte o agli ambiti di protezione specificati**.  
6. Per modificare i ruoli di sicurezza assegnati, scegliere la scheda **Ruoli di protezione**.  

    - Per assegnare ruoli di sicurezza aggiuntivi all'utente, scegliere **Aggiungi**, selezionare la casella relativa a ogni ruolo di sicurezza aggiuntivo da assegnare e quindi scegliere **OK**.  
    - Per rimuovere i ruoli di sicurezza, selezionare uno o più ruoli di sicurezza nell'elenco e quindi scegliere **Rimuovi**.  
7. Per modificare le raccolte e gli ambiti di protezione associati ai ruoli di sicurezza, scegliere la scheda **Ambiti di protezione**.  

    - Per associare nuovi ambiti di protezione o raccolte ai ruoli di sicurezza assegnati all'utente amministratore, scegliere **Aggiungi** e selezionare una delle quattro opzioni. Se si seleziona **Ambito di protezione** o **Raccolta**, selezionare la casella relativa a uno o più oggetti per completare la selezione e quindi scegliere **OK**.  
    - Per rimuovere un ambito di protezione o una raccolta, selezionare l'oggetto e quindi scegliere **Rimuovi**.

8. Scegliere **OK** per completare questa procedura.  

Usare la procedura seguente per modificare un utente amministratore con il comportamento degli oggetti a protezione diretta impostato su **Associa ruoli di protezione assegnati a raccolte e ambiti di protezione specifici**.  

### <a name="for-option-associate-assigned-security-roles-with-specific-security-scopes-and-collections"></a>Per l'opzione: Associa ruoli di protezione assegnati a raccolte e ambiti di protezione specifici  

1. Nella console di Configuration Manager scegliere **Amministrazione**.  
2. Nell'area di lavoro **Amministrazione** espandere **Sicurezza** e quindi scegliere **Utenti amministratori**.  
3. Selezionare l'utente amministratore che si desidera modificare.  
4. Nella scheda **Home**, nel gruppo **Proprietà**, fare clic su **Proprietà**.  
5. Scegliere la scheda **Ambiti di protezione** per assicurarsi che l'utente amministratore sia configurato per **Associa ruoli di protezione assegnati a raccolte e ambiti di protezione specifici**.  
6. Per modificare i ruoli di sicurezza assegnati, scegliere la scheda **Ruoli di protezione**.  

    - Per assegnare ruoli di sicurezza aggiuntivi all'utente amministratore, scegliere **Aggiungi**. Nella finestra di dialogo **Aggiungi ruolo di protezione** selezionare uno o più ruoli di sicurezza disponibili, scegliere **Aggiungi** e selezionare un tipo di oggetto da associare ai ruoli di sicurezza selezionati. Se si seleziona **Ambito di protezione** o **Raccolta**, selezionare la casella relativa a uno o più oggetti per completare la selezione e quindi scegliere **OK**.  

        > [!NOTE]  
        > È necessario configurare almeno un ambito di protezione prima di assegnare i ruoli di sicurezza selezionati all'utente amministratore. Quando si selezionano più ruoli di sicurezza, tutte le raccolte e gli ambiti di protezione configurati vengono associati a ogni ruolo di sicurezza selezionato.  

    - Per rimuovere i ruoli di sicurezza, selezionare uno o più ruoli di sicurezza nell'elenco e quindi scegliere **Rimuovi**.  

7. Per modificare le raccolte e gli ambiti di protezione associati a un ruolo di sicurezza specifico, scegliere la scheda **Ambiti di protezione**, selezionare il ruolo di sicurezza e quindi scegliere **Modifica**.  

    - Per associare nuovi oggetti a questo ruolo di sicurezza, scegliere **Aggiungi** e quindi selezionare il tipo di oggetto da associare ai ruoli selezionati. Se si seleziona **Ambito di protezione** o **Raccolta**, selezionare la casella relativa a uno o più oggetti per completare la selezione e quindi scegliere **OK**.  

        > [!NOTE]  
        > È necessario configurare almeno un ambito di protezione.  

    - Per rimuovere una raccolta o un ambito di protezione associato al ruolo di sicurezza, selezionare l'oggetto e quindi scegliere **Rimuovi**.  

    - Dopo aver completato la modifica degli oggetti associati, scegliere **OK**.  

8. Scegliere **OK** per completare questa procedura.  

    > [!CAUTION]  
    > Quando un ruolo di sicurezza concede agli utenti amministratori l'autorizzazione per la distribuzione di raccolte, questi utenti possono distribuire oggetti da ogni ambito di protezione per cui dispongono dell'autorizzazione di **lettura** , anche se tale ambito è associato a un ruolo diverso.  

## <a name="next-steps"></a>Passaggi successivi

[Account usati in Configuration Manager](../../../plan-design/hierarchy/accounts.md)
