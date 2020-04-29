---
title: Creare una sequenza di attività per installare un sistema operativo
titleSuffix: Configuration Manager
description: Usare le sequenze di attività in Configuration Manager per installare automaticamente un'immagine del sistema operativo e altro contenuto in un computer di destinazione.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 217c8a0e-5112-420e-a325-2a6d75326290
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6e1b298856edea3f81cab2e9cd5ab75af49dff51
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707309"
---
# <a name="create-a-task-sequence-to-install-an-os"></a>Creare una sequenza di attività per installare un sistema operativo

*Si applica a: Configuration Manager (Current Branch)*

Usare le sequenze di attività in Configuration Manager per installare automaticamente un'immagine del sistema operativo in un computer di destinazione. Creare una sequenza di attività che faccia riferimento a un'immagine di avvio usata per avviare il computer di destinazione, all'immagine del sistema operativo da installare nel computer di destinazione e qualsiasi altro contenuto aggiuntivo, ad esempio altre applicazioni o aggiornamenti software, che si vuole installare. Distribuire quindi la sequenza di attività in una raccolta che contiene il computer di destinazione.  

## <a name="create-a-task-sequence-to-install-an-os"></a><a name="BKMK_InstallOS"></a> Creare una sequenza di attività per installare un sistema operativo

Esistono più scenari per la distribuzione di un sistema operativo nei computer dell'ambiente. Nella maggior parte dei casi creare una sequenza di attività e selezionare **Installa un pacchetto immagine esistente** nella creazione guidata della sequenza di attività. Questa opzione crea una sequenza di attività che installa il sistema operativo, esegue la migrazione delle impostazioni utente, applica gli aggiornamenti software e installa le applicazioni.

### <a name="prerequisites"></a>Prerequisiti

Prima di creare una sequenza di attività per installare un sistema operativo, devono essere soddisfatti i requisiti seguenti:

#### <a name="required"></a>Richiesto

- Un [immagine d'avvio](../get-started/manage-boot-images.md)  

- Un'[immagine del sistema operativo](../get-started/manage-operating-system-images.md)  

#### <a name="required-if-used"></a>Obbligatorio (se usato)

- Sincronizzare gli [aggiornamenti software](../../sum/get-started/synchronize-software-updates.md)  

- Aggiungere le [applicazioni](../../apps/deploy-use/create-applications.md)  

### <a name="process-to-create-a-task-sequence-that-installs-an-os"></a>Procedura per la creazione di una sequenza di attività che installi un sistema operativo  

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**, espandere **Sistemi operativi** e selezionare il nodo **Sequenze di attività**.  

2. Nella scheda **Home** della barra multifunzione nel gruppo **Crea** selezionare **Crea sequenza di attività**. Questa azione avvia la Creazione guidata della sequenza di attività.  

3. Nella pagina **Crea una nuova sequenza di attività** selezionare **Installa un pacchetto immagine esistente**, quindi selezionare **Avanti**.  

4. Nella pagina **Informazioni sequenza di attività** specificare le impostazioni seguenti:  

    - **Nome sequenza di attività**: Specificare un nome che identifica la sequenza di attività.  

    - **Descrizione**: Specificare una descrizione delle operazioni eseguite dalla sequenza di attività.  

    - **Immagine d'avvio**: Specificare l'immagine di avvio usata dalla sequenza di attività per installare il sistema operativo nel computer di destinazione. L'immagine di avvio contiene una versione di Windows PE, oltre ai driver di dispositivo aggiuntivi necessari. Per altre informazioni, vedere [Manage boot images](../get-started/manage-boot-images.md) (Gestire le immagini d'avvio).  

        > [!IMPORTANT]  
        > L'architettura dell'immagine di avvio deve essere compatibile con l'architettura hardware del computer di destinazione.  

5. Nella pagina **Installa Windows** specificare le impostazioni seguenti:  

    - **Pacchetto immagine**: Specificare il pacchetto che contiene l'immagine del sistema operativo da installare. Per altre informazioni, vedere [Gestire le immagini del sistema operativo](../get-started/manage-operating-system-images.md).  

    - **Immagine**: Se il pacchetto immagine del sistema operativo contiene più immagini, specificare l'indice dell'immagine del sistema operativo da installare.  

    - **Creare partizioni e formattare il computer di destinazione prima di installare il sistema operativo**: Specificare se la sequenza di attività deve eseguire una partizione e una formattazione del computer di destinazione prima di installare il sistema operativo.  

    - **Codice Product Key**: Specificare il codice Product Key di Windows, se necessario. È possibile specificare i codici Product Key per contratti multilicenza codificati e i codici Product Key standard. Se si usa un codice Product Key non codificato, ogni gruppo di cinque caratteri deve essere separato da un trattino (`-`). Ad esempio: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*  

    - **Modalità di gestione licenze del server**: specificare che la licenza del server è **Per postazione**, **Per server** o che non è specificata alcuna licenza. Se la licenza del server è **Per server**, specificare anche il numero massimo di connessioni al server.  

    - Specificare come gestire l'account amministratore per il nuovo sistema operativo:  

        - **Genera in modo casuale la password dell'account amministratore locale e disattiva l'account su tutte le piattaforme supportate (consigliato)** : Windows disabilita l'account amministratore locale dopo che la sequenza di attività distribuisce l'immagine del sistema operativo.  

        - **Attiva l'account e specifica la password dell'amministratore locale**: Windows usa la stessa password per l'account amministratore locale in tutti i computer in cui la sequenza di attività distribuisce il sistema operativo.  

6. Nella pagina **Configura rete** specificare le impostazioni seguenti:  

    - **Aggiunta a un gruppo di lavoro**: Aggiunge il computer di destinazione a un gruppo di lavoro.  

    - **Aggiunta a un dominio**: Aggiunge il computer di destinazione a un dominio. In **Dominio**specificare il nome del dominio.  

        > [!IMPORTANT]  
        > È possibile cercare i domini nella foresta locale, ma è necessario specificare il nome di dominio per una foresta remota.  

        È anche possibile specificare un'unità organizzativa nel campo **Unità organizzativa di dominio**. Questa impostazione è facoltativa e specifica il nome distinto LDAP X.500 dell'unità organizzativa. Se non esiste già, Windows crea l'account computer in questa unità organizzativa.  

    - **Account**: Nome utente e password per l'account con le autorizzazioni per l'aggiunta al dominio specificato. Ad esempio: *dominio\utente* o *%variabile%* .  

        > [!IMPORTANT]  
        > Se si prevede di migrare le impostazioni del dominio o le impostazioni del gruppo di lavoro, immettere le credenziali di dominio appropriate.  

7. Nella pagina **Installa Configuration Manager** specificare il pacchetto client di Configuration Manager da installare nel computer di destinazione. Si possono includere anche eventuali proprietà di installazione.  

8. Nella pagina **Migrazione stato** specificare le informazioni seguenti:  

    - **Acquisisci impostazioni utente**: La sequenza di attività acquisisce lo stato utente. Per altre informazioni su come acquisire e ripristinare lo stato utente, vedere [Gestire lo stato utente](../get-started/manage-user-state.md).  

    - **Acquisisci impostazioni di rete**: Specificare se la sequenza di attività acquisisce le impostazioni di rete dal computer di destinazione. Acquisisce l'appartenenza del dominio o del gruppo di lavoro e le impostazioni della scheda di rete.  

    - **Acquisisci impostazioni di Microsoft Windows**: La sequenza di attività acquisisce le impostazioni di Windows dal computer di destinazione prima di installare l'immagine del sistema operativo. Acquisisce il nome del computer, il nome dell'utente registrato e dell'organizzazione e le impostazioni di fuso orario.  

9. Nella pagina **Includi aggiornamenti** specificare se installare gli aggiornamenti software necessari, tutti gli aggiornamenti software o nessun aggiornamento software. Se si sceglie di installare gli aggiornamenti software, Configuration Manager installa solo quelli assegnati alle raccolte di cui il computer di destinazione è membro.  

10. Nella pagina **Installa applicazioni** specificare le applicazioni da installare nel computer di destinazione. Se si specificano più applicazioni, è possibile specificare che la sequenza di attività continui anche se l'installazione di un'applicazione specifica non riesce.  

11. Completare la procedura guidata.  

Ora è possibile distribuire la sequenza di attività in una raccolta di computer. Per altre informazioni, vedere [Deploy a task sequence](deploy-a-task-sequence.md).


## <a name="pre-cache-content"></a>Pre-cache del contenuto

<!--4224642-->
A partire dalla versione 1906 è possibile abilitare questo tipo di sequenza di attività per la pre-cache del contenuto. La funzionalità pre-cache per le distribuzioni di sequenze di attività disponibili consente ai client di scaricare il contenuto pertinente prima che un utente installi la sequenza di attività.  

Per altre informazioni, vedere [Configurare la pre-cache del contenuto](configure-precache-content.md).


## <a name="example-task-sequence"></a><a name="BKMK_InstallExistingOSImageTSExample"></a> Sequenza di attività di esempio

Usare la tabella seguente come guida durante la creazione di una sequenza di attività per la distribuzione di un sistema operativo con un'immagine esistente. La tabella è utile per decidere la sequenza generale per i passaggi della sequenza di attività e come organizzare e strutturare i passaggi della sequenza di attività in gruppi logici. La sequenza di attività creata può variare rispetto a questo esempio e contenere più o meno passaggi e gruppi.  

> [!NOTE]  
> Usare la Creazione guidata della sequenza di attività per creare questa sequenza di attività.  
>
> Quando si usa la Creazione guidata della sequenza di attività per creare questa nuova sequenza di attività, alcuni nomi dei passaggi differiscono da quelli per l'aggiunta manuale dei passaggi a una sequenza esistente.

|Gruppo o passaggio di sequenza di attività|Descrizione|  
|---------------------------------|-----------------|  
|Acquisisci file e impostazioni - **(Nuovo gruppo di sequenze di attività)**|Creare un gruppo di sequenze di attività. Un gruppo di sequenze di attività consente di mantenere assieme i passaggi delle sequenze di attività per una migliore organizzazione e un maggiore controllo degli errori.<br /><br /> Questo gruppo contiene i passaggi necessari per l'acquisizione di file e impostazioni dal sistema operativo del computer di riferimento.|  
|Acquisisci impostazioni Windows|Usare questo passaggio della sequenza di attività per identificare le impostazioni di Microsoft Windows per l'acquisizione dal computer di riferimento. È possibile acquisire il nome del computer, utente e informazioni sull'organizzazione e le impostazioni di fuso orario.|  
|Acquisisci impostazioni di rete|Usare questo passaggio della sequenza di attività per acquisire le impostazioni di rete dal computer di riferimento. È possibile acquisire l'appartenenza al gruppo di lavoro o dominio del computer di riferimento e impostazione delle informazioni relative alla scheda di rete.|  
|Acquisisci file utente e impostazioni - **(Nuovo sottogruppo di sequenze di attività)**|Creare un gruppo di sequenze di attività all'interno di un gruppo di sequenze di attività. Questo sottogruppo contiene i passaggi necessari per acquisire dati sullo stato utente. Analogamente al gruppo iniziale aggiunto, questo sottogruppo tiene uniti i passaggi delle sequenze di attività per una migliore organizzazione e un maggiore controllo degli errori.|  
|Archiviazione dello stato utente richiesta|Usare questo passaggio della sequenza di attività per richiedere l'accesso a un punto di migrazione stato in cui sono archiviati i dati dello stato utente. È possibile configurare questo passaggio della sequenza di attività per acquisire o ripristinare le informazioni sullo stato utente.|  
|Acquisisci file utente e impostazioni|Usare questo passaggio della sequenza di attività per usare l'Utilità di migrazione stato utente per acquisire lo stato utente e le impostazioni dal computer di riferimento che riceve la sequenza di attività associata a questo passaggio. È possibile acquisire le opzioni standard o configurare le opzioni da acquisire.|  
|Rilascia archiviazione stato utente|Utilizzare questo passaggio della sequenza attività per notificare lo stato punto di migrazione che l'azione di ripristino o acquisizione è stata completata.|  
|Installa il sistema operativo - **(Nuovo gruppo di sequenze di attività)**|Creare un altro sottogruppo di sequenze di attività. Questo sottogruppo contiene i passaggi necessari per installare e configurare l'ambiente Windows PE.|  
|Riavvia in Windows PE|Utilizzare questo passaggio della sequenza attività per specificare le opzioni di riavvio del computer di destinazione che riceve questa sequenza di attività. Questo passaggio viene visualizzato un messaggio all'utente che indica che il computer verrà riavviato affinché possa continuare l'installazione.<br /><br /> Questo passaggio usa la variabile della sequenza di attività **_SMSTSInWinPE** di sola lettura. Se il valore associato è uguale a **false** il passaggio della sequenza attività continua.|  
|Partizione disco 0|Questo passaggio della sequenza attività specifica le azioni necessarie per formattare il disco rigido nel computer di destinazione. Il numero di disco predefinito è **0**.<br /><br /> Questo passaggio usa la variabile della sequenza di attività **_SMSTSClientCache** di sola lettura. Questo passaggio viene eseguito se la cache del client di Configuration Manager non esiste.|  
|Applica sistema operativo|Utilizzare questo passaggio della sequenza attività per installare l'immagine del sistema operativo nel computer di destinazione. Questo passaggio elimina innanzitutto tutti i file nel volume, ad eccezione dei file di controllo specifici di Configuration Manager. Applica quindi tutte le immagini del volume contenute nel file WIM al volume del disco sequenziale corrispondente nel computer di destinazione. È possibile specificare un **sysprep** file di risposte e inoltre configurare la partizione del disco viene utilizzata per l'installazione.|  
|Applica impostazioni Windows|Usare questo passaggio della sequenza di attività per configurare le informazioni di configurazione delle impostazioni di Windows per il computer di destinazione. Le impostazioni di Windows applicabili sono le informazioni sull'utente e sull'organizzazione, le informazioni sul prodotto o sul codice di licenza, il fuso orario e la password dell'amministratore locale.|  
|Applica impostazioni di rete|Usare questo passaggio della sequenza di attività per specificare le informazioni di configurazione per la rete o il gruppo di lavoro per il computer di destinazione. È inoltre possibile specificare se il computer utilizza un server DHCP oppure è possibile assegnare staticamente le informazioni sull'indirizzo IP.|  
|Applica driver dispositivo|Utilizzare questo passaggio della sequenza attività per installare i driver come parte della distribuzione del sistema operativo. È possibile consentire a Installazione di Windows di cercare tutte le categorie di driver esistenti selezionando **Considera i driver di tutte le categorie** oppure limitare le categorie in cui Installazione di Windows esegue la ricerca selezionando **Limita la corrispondenza dei driver in modo da considerare solo i driver delle categorie selezionate**.<br /><br /> Questo passaggio usa la variabile della sequenza di attività **_SMSTSMediaType** di sola lettura. Questo passaggio della sequenza di attività viene eseguito solo se il valore della variabile è diverso da **FullMedia**.|  
|Applica pacchetto di driver|Utilizzare questo passaggio della sequenza attività per rendere disponibili per l'utilizzo tutti i driver di dispositivo in un pacchetto driver dal programma di installazione di Windows.|  
|Installa sistema operativo - **(Nuovo gruppo di sequenze di attività)**|Creare un altro sottogruppo di sequenze di attività. Questo sottogruppo contiene i passaggi necessari per configurare il sistema operativo installato.|  
|Imposta Windows e ConfigMgr|Usare questo passaggio della sequenza di attività per installare il software client di Configuration Manager. Configuration Manager installa e registra il GUID del client di Configuration Manager. È possibile assegnare i parametri di installazione necessari nella finestra **Proprietà di installazione** .|  
|Installa aggiornamenti|Usare questo passaggio della sequenza di attività per specificare in che modo gli aggiornamenti software vengono installati nel computer di destinazione. Il computer di destinazione viene valutato alla ricerca di aggiornamenti software applicabili solo in corrispondenza con l'esecuzione di questo passaggio della sequenza di attività, quando il computer di destinazione viene valutato alla ricerca di aggiornamenti software applicabili in modo simile agli altri client gestiti da Configuration Manager.<br /><br /> Questo passaggio usa la variabile della sequenza di attività **_SMSTSMediaType** di sola lettura. Questo passaggio della sequenza di attività viene eseguito solo se il valore della variabile è diverso da **FullMedia**.|  
|Ripristina file utente e impostazioni - **(Nuovo gruppo di sequenze di attività)**|Creare un altro sottogruppo di sequenze di attività. Questo sottogruppo contiene i passaggi necessari per ripristinare i file utente e le impostazioni.|  
|Archiviazione dello stato utente richiesta|Utilizzare questo passaggio della sequenza attività per richiedere l'accesso a un punto di migrazione stato archiviazione i dati dello stato utente.|  
|Ripristina file utente e impostazioni|Usare questo passaggio della sequenza di attività per eseguire l'Utilità di migrazione stato utente e ripristinare lo stato utente e le impostazioni in un computer di destinazione.|  
|Rilascia archiviazione stato utente|Usare questo passaggio della sequenza di attività per segnalare al punto di migrazione stato che i dati dello stato utente non sono più necessari.|  
