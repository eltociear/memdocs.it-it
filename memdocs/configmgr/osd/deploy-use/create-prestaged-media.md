---
title: Creare supporti pre-installati
titleSuffix: Configuration Manager
description: Usare supporti pre-installati in Configuration Manager per semplificare la distribuzione di Windows in diversi scenari.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: ff6e7267-302a-4563-815e-cdc0d1a4b60f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 82bb02d8154939b4b0e0ee89bcc6637e9393acff
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125220"
---
# <a name="create-prestaged-media"></a>Creare supporti pre-installati

*Si applica a: Configuration Manager (Current Branch)*

I supporti pre-installati in Configuration Manager sono un file WIM che può essere installato in un computer bare metal dal produttore o nel centro di gestione temporanea non connesso all'ambiente di Configuration Manager. I supporti pre-installati contengono l'immagine d'avvio usata per avviare il computer di destinazione e l'immagine del sistema operativo applicata al computer di destinazione. È anche possibile specificare applicazioni, pacchetti e pacchetti driver da includere come parte del supporto pre-installato. La sequenza di attività che distribuisce il sistema operativo non è inclusa nel supporto. Il supporto pre-installato viene applicato al disco rigido di un nuovo computer prima che il computer venga inviato all'utente finale.

Usare i supporti pre-installati per gli scenari di distribuzione del sistema operativo seguenti:  

- [Creare un'immagine per un OEM presso un produttore computer o un deposito locale](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

- [Installare una nuova versione di Windows in un nuovo computer (bare metal)](install-new-windows-version-new-computer-bare-metal.md)  

- [Distribuire Windows to Go](deploy-windows-to-go.md)  


## <a name="usage"></a>Utilizzo

Quando il computer viene avviato per la prima volta dopo aver applicato i supporti pre-installati, il computer viene avviato in Windows PE. Si connette a un punto di gestione per individuare la sequenza di attività che completa il processo di distribuzione del sistema operativo. Quando si distribuisce una sequenza di attività che usa supporti pre-installati, il client cerca prima di tutto contenuto valido nella cache della sequenza di attività locale. Se il contenuto non viene trovato o è stato rivisto, il client scarica il contenuto da un punto di distribuzione o da un peer.  


## <a name="prerequisites"></a>Prerequisiti

Prima di creare supporti pre-installati usando la Creazione guidata del supporto per la sequenza di attività, assicurarsi che tutte le condizioni siano soddisfatte.

### <a name="boot-image"></a>Immagine d'avvio

Tenere in considerazione i punti seguenti per l'immagine d'avvio da usare nella sequenza di attività per distribuire il sistema operativo:

- L'architettura dell'immagine d'avvio deve essere appropriata per l'architettura del computer di destinazione. Ad esempio, un computer di destinazione x64 può avviare ed eseguire un'immagine di avvio x86 o x64. Tuttavia, un computer di destinazione x86 può avviare ed eseguire solo un'immagine di avvio x86.
- Assicurarsi che l'immagine d'avvio contenga i driver di archiviazione e di rete necessari per eseguire il provisioning del computer di destinazione.

### <a name="create-a-task-sequence-to-deploy-an-os"></a>Creare una sequenza di attività per distribuire un sistema operativo

Nell'ambito dei supporti pre-installati, è necessario specificare la sequenza di attività per distribuire il sistema operativo. Per altre informazioni, vedere [Creare una sequenza di attività per installare un sistema operativo](create-a-task-sequence-to-install-an-operating-system.md).

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Distribuire tutto il contenuto associato alla sequenza di attività

Distribuire tutto il contenuto richiesto dalla sequenza di attività in almeno un punto di distribuzione. Tale contenuto include l'immagine d'avvio, l'immagine del sistema operativo e altri file associati. La procedura guidata raccoglie il contenuto dal punto di distribuzione quando crea i supporti pre-installati.

L'account utente usato deve avere almeno diritti di accesso in **lettura** per la raccolta contenuto nel punto di distribuzione. Per altre informazioni, vedere [Distribuire il contenuto](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

### <a name="hard-drive-on-the-destination-computer"></a>Disco rigido nel computer di destinazione

È necessario eseguire la formattazione del disco rigido del computer di destinazione prima che i supporti pre-installati venga applicati. Se il disco rigido non è formattato quando vengono applicati i supporti, la sequenza di attività che distribuisce il sistema operativo non potrà avviare il computer di destinazione.

> [!NOTE]  
> La Creazione guidata del supporto per la sequenza di attività imposta la seguente condizione variabile di sequenza di attività nel supporto: **_SMSTSMediaType = OEMMedia**. È possibile usare questa stessa condizione nella sequenza di attività.  


## <a name="process"></a>Processo

 > [!NOTE]  
 > Per gli ambienti PKI, dato che la CA radice viene specificata nel sito primario, verificare che il supporto pre-installato venga creato nel sito primario. Il sito CAS non contiene le informazioni sulla CA radice sufficienti per creare correttamente il supporto pre-installato.

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**, espandere **Sistemi operativi** e selezionare il nodo **Sequenze di attività**.  

2. Nella scheda **Home** della barra multifunzione nel gruppo **Crea** selezionare **Crea supporto per sequenza attività**. Questa azione avvia la Creazione guidata del supporto per la sequenza di attività.  

3. Nella pagina **Seleziona tipo di supporto** specificare le opzioni seguenti:  

    - Selezionare **Supporti preinstallati**.  

    - Se si vuole solo consentire la distribuzione del sistema operativo senza richiedere input da parte dell'utente, è possibile selezionare **Consenti distribuzione automatica del sistema operativo**.  

        > [!IMPORTANT]  
        > Quando si seleziona questa opzione, all'utente non vengono richieste informazioni sulla configurazione di rete o su sequenze di attività facoltative. Se si configurano i supporti per la protezione con password, all'utente viene richiesta una password.  

4. Nella pagina **Gestione del supporto** specificare una delle opzioni seguenti:  

    - **Supporto dinamico**: consente a un punto di gestione di reindirizzare il supporto a un altro punto di gestione, in base al percorso del client nei limiti del sito.  

    - **Supporto basato su sito**: Il supporto contatta solo il punto di gestione specificato.  

5. Nella pagina **Proprietà del supporto** specificare le informazioni seguenti:  

    - **Creato da**: specificare chi ha creato il supporto.  

    - **Versione**: specificare il numero di versione del supporto.  

    - **Commento**: specificare una descrizione univoca dello scopo per cui viene usato il supporto.  

    - **File supporto**: specificare il nome e il percorso dei file di output. La procedura guidata scrive i file di output in questa posizione. ad esempio `\\servername\folder\outputfile.wim`  

    - **Cartella di gestione temporanea**<!--1359388-->: il processo di creazione del supporto può richiedere molto spazio temporaneo sul disco. Per impostazione predefinita questo percorso è simile al seguente: `%UserProfile%\AppData\Local\Temp`. A partire dalla versione 1902, per offrire maggiore flessibilità dal punto di vista del percorso di archiviazione dei file temporanei, modificare questo valore con un'altra unità e un altro percorso.  

6. Nella pagina **Sicurezza** specificare le opzioni seguenti:  

    - **Abilita supporto per computer sconosciuti**: consente al supporto di distribuire un sistema operativo a un computer non gestito da Configuration Manager. Non sono presenti record di questi computer nel database di Configuration Manager. Per altre informazioni, vedere [Operazioni preliminari alle distribuzioni in computer sconosciuti](../get-started/prepare-for-unknown-computer-deployments.md).  

    - **Proteggi supporto con password**: immettere una password complessa per proteggere il supporto dall'accesso non autorizzato. Quando si specifica una password l'utente deve immettere la password per usare il supporto pre-installato.  

        > [!IMPORTANT]  
        > Come procedura consigliata di sicurezza, assegnare sempre una password per proteggere il supporto pre-installato.  
 
    - Per le comunicazioni HTTP, selezionare **Crea certificato del supporto autofirmato**. Specificare quindi la data di inizio e di scadenza del certificato.  
    
        > [!NOTE] 
        > Se si seleziona questa opzione, i punti di gestione HTTPS non saranno disponibili per la selezione nella pagina **Immagine d'avvio** della procedura guidata.

    - Per le comunicazioni HTTPS, selezionare **Importa certificato PKI**. Specificare quindi il certificato da importare e la relativa password.  

        Per altre informazioni su questo certificato client usato dalle immagini d'avvio, vedere [Requisiti dei certificati PKI](../../core/plan-design/network/pki-certificate-requirements.md).  

    - **Affinità utente dispositivo**: per supportare la gestione basata sugli utenti in Configuration Manager, specificare come si vuole che il supporto associ gli utenti al computer di destinazione. Per altre informazioni su come la distribuzione del sistema operativo supporti l'affinità utente-dispositivo, vedere [Associare gli utenti a un computer di destinazione](../get-started/associate-users-with-a-destination-computer.md).  

        - **Consenti affinità utente dispositivo con approvazione automatica**: Il supporto associa automaticamente gli utenti al computer di destinazione. Questa funzionalità si basa sulle azioni della sequenza di attività che distribuisce il sistema operativo. In questo scenario la sequenza di attività crea una relazione tra gli utenti specificati e il computer di destinazione quando distribuisce il sistema operativo nel computer di destinazione.  

        - **Consenti approvazione amministratore in sospeso per affinità utente dispositivo**: Il supporto associa gli utenti al computer di destinazione dopo la concessione dell'approvazione. Questa funzionalità si basa sull'ambito della sequenza di attività che distribuisce il sistema operativo. In questo scenario la sequenza di attività crea una relazione tra gli utenti specificati e il computer di destinazione, ma attende l'approvazione di un utente amministratore prima di distribuire il sistema operativo.  

        - **Non consentire affinità utente dispositivo**: il supporto non associa gli utenti al computer di destinazione. In questo scenario la sequenza di attività non associa gli utenti al computer di destinazione quando distribuisce il sistema operativo.  

7. Nella pagina **Sequenza di attività** specificare la sequenza di attività che viene eseguita nel computer di destinazione. Verificare l'elenco di contenuti a cui si fa riferimento nella sequenza di attività.  

    - **Rileva le dipendenze dell'applicazione associata e aggiungile a questo contenuto multimediale**: aggiungere anche contenuto al supporto per le dipendenze dell'applicazione.  

        > [!TIP]  
        > Se le dipendenze dell'applicazione previste non vengono visualizzate, deselezionare e selezionare nuovamente questa opzione per aggiornare l'elenco.  

8. Nella pagina **Immagine d'avvio** specificare le opzioni seguenti:  

    > [!IMPORTANT]  
    > L'architettura dell'immagine d'avvio distribuita deve essere appropriata per l'architettura del computer di destinazione. Ad esempio, un computer di destinazione x64 può avviare ed eseguire un'immagine di avvio x86 o x64. Tuttavia, un computer di destinazione x86 può avviare ed eseguire solo un'immagine di avvio x86.  

    - **Immagine d'avvio**: selezionare l'immagine di avvio per avviare il computer di destinazione.  

    - **Punto di distribuzione**: selezionare il punto di distribuzione che ospita l'immagine d'avvio. La procedura guidata consente di recuperare l'immagine di avvio dal punto di distribuzione e di scriverla sul supporto.  

        > [!NOTE]  
        > L'account utente usato deve avere almeno autorizzazioni di **lettura** per la raccolta contenuto nel punto di distribuzione.  

    - **Punto di gestione**: solo per *supporto basato su sito*, selezionare un punto di gestione da un sito primario.  

    - **Punti di gestione associati**: solo per *supporti dinamici*, selezionare i punti di gestione del sito primario da usare e l'ordine di priorità per la comunicazione iniziale.  

        > [!NOTE]  
        > I punti di gestione abilitati per HTTPS verranno visualizzati solo quando viene specificato un certificato PKI nella pagina **Sicurezza** della procedura guidata.  

9. Nella pagina **Generale** specificare le opzioni seguenti:  

    - **Pacchetto immagine**: Specificare il sistema operativo da usare. Per altre informazioni, vedere [Gestire le immagini del sistema operativo](../get-started/manage-operating-system-images.md).  

    - **Indice immagine**: specificare l'indice dell'immagine da distribuire se il pacchetto contiene più immagini del sistema operativo.  

    - **Punto di distribuzione**: specificare il punto di distribuzione che ospita il pacchetto dell'immagine del sistema operativo. La procedura guidata recupera l'immagine del sistema operativo dal punto di distribuzione e la scrive sul supporto.  

10. Nella pagina **Selezione applicazione** selezionare altre applicazioni da aggiungere al file del supporto pre-installato.  

11. Nella pagina **Selezione pacchetto** selezionare altri pacchetti da aggiungere al file del supporto pre-installato.  

12. Nella pagina **Selezione il pacchetto driver** selezionare altri pacchetti driver da aggiungere al file del supporto pre-installato.  

13. Nella pagina **Punti di distribuzione** selezionare uno o più punti di distribuzione da cui recuperare il contenuto.  

    Configuration Manager visualizza solo i punti di distribuzione che includono il contenuto. Per continuare, distribuire tutto il contenuto associato alla sequenza di attività in almeno un punto di distribuzione. Dopo avere distribuito il contenuto, aggiornare l'elenco di punti di distribuzione. Rimuovere i punti di distribuzione già selezionati in questa pagina, andare alla pagina precedente e quindi di nuovo alla pagina **Punti di distribuzione**. In alternativa, riavviare la procedura guidata. Per altre informazioni, vedere [Distribuire il contenuto a cui fa riferimento una sequenza di attività](manage-task-sequences-to-automate-tasks.md#BKMK_DistributeTS) e [Gestire il contenuto e l'infrastruttura del contenuto](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

14. Nella pagina **Personalizzazione** specificare le opzioni seguenti:  

    - Aggiungere eventuali variabili usate dalla sequenza di attività.  

    - **Attiva comando di preavvio**: Specificare i comandi preavvio da eseguire prima dell'esecuzione della sequenza di attività. I comandi di preavvio sono costituiti da uno script o da un eseguibile che può interagire con l'utente in Windows PE prima che venga eseguita la sequenza di attività. Per altre informazioni vedere [Comandi di preavvio del supporto per sequenza attività](../understand/prestart-commands-for-task-sequence-media.md).  

        > [!TIP]  
        > Durante la creazione del supporto, tale sequenza scrive l'ID del pacchetto e la riga di comando di preavvio, incluso il valore per eventuali variabili della sequenza di attività, nel file **CreateTSMedia.log** nel computer che esegue la console di Configuration Manager. È possibile rivedere questo file di registro per verificare il valore per le variabili della sequenza di attività.  

        Se il comando di preavvio richiede contenuto, selezionare l'opzione **Includi file per il comando di preavvio**.  

15. Completare la procedura guidata.  


## <a name="next-steps"></a>Passaggi successivi

[Creare un'immagine per un OEM presso un produttore computer o un deposito locale](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)
