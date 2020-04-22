---
title: Creare supporti di avvio
titleSuffix: Configuration Manager
description: Usare supporti di avvio in Configuration Manager per installare una nuova versione di Windows o sostituire un computer.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: ead79e64-1b63-4d0d-8bd5-addff8919820
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 44c570fc2844093b190e388727dd3799bcbcdb92
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694899"
---
# <a name="create-bootable-media"></a>Creare supporti di avvio

*Si applica a: Configuration Manager (Current Branch)*

I supporti di avvio in Configuration Manager contengono l'immagine d'avvio, i comandi di preavvio opzionali e i rispettivi file associati e i file di Configuration Manager. Usare i supporti preinstallati per gli scenari di distribuzione del sistema operativo seguenti:  

- [Installare una nuova versione di Windows in un nuovo computer (bare metal)](install-new-windows-version-new-computer-bare-metal.md)  

- [Sostituire un computer esistente e trasferire le impostazioni](replace-an-existing-computer-and-transfer-settings.md)  


## <a name="usage"></a>Utilizzo

Il processo seguente si verifica all'avvio con supporti di avvio:

1. Il computer di destinazione si avvia
1. Si connette alla rete
1. Recupera dal sito il contenuto seguente:
    - Sequenza di attività specificata
    - Immagine del sistema operativo
    - Qualsiasi altro contenuto necessario

Poiché la sequenza di attività non è presente nel supporto, è possibile modificare la sequenza di attività o il contenuto senza dover ricreare il supporto.

I pacchetti nei supporti di avvio non sono crittografati. Per assicurarsi che il contenuto del pacchetto sia protetto da utenti non autorizzati, adottare misure di sicurezza appropriate, ad esempio, aggiungere una password al supporto.

## <a name="prerequisites"></a>Prerequisiti

Prima di creare supporti di avvio usando la Creazione guidata del supporto per la sequenza di attività, assicurarsi che tutte queste condizioni siano soddisfatte.

### <a name="boot-image"></a>Immagine d'avvio

Tenere in considerazione i punti seguenti per l'immagine d'avvio da usare nella sequenza di attività per distribuire il sistema operativo:

- L'architettura dell'immagine d'avvio deve essere appropriata per l'architettura del computer di destinazione. Ad esempio, un computer di destinazione x64 può avviare ed eseguire un'immagine di avvio x86 o x64. Tuttavia, un computer di destinazione x86 può avviare ed eseguire solo un'immagine di avvio x86.
- Assicurarsi che l'immagine d'avvio contenga i driver di archiviazione e di rete necessari per eseguire il provisioning del computer di destinazione.

### <a name="create-a-task-sequence-to-deploy-an-os"></a>Creare una sequenza di attività per distribuire un sistema operativo

Nell'ambito del supporto di avvio, è necessario specificare la sequenza di attività per distribuire il sistema operativo. Per altre informazioni, vedere [Creare una sequenza di attività per installare un sistema operativo](create-a-task-sequence-to-install-an-operating-system.md).

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Distribuire tutto il contenuto associato alla sequenza di attività

Distribuire tutto il contenuto richiesto dalla sequenza di attività in almeno un punto di distribuzione. Tale contenuto include l'immagine d'avvio e altri file di preavvio associati. La procedura guidata raccoglie il contenuto dal punto di distribuzione quando crea il supporto di avvio.

L'account utente usato deve avere almeno diritti di accesso in **lettura** per la raccolta contenuto nel punto di distribuzione. Per altre informazioni, vedere [Distribuire il contenuto](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

### <a name="prepare-the-removable-usb-drive"></a>Preparare l'unità USB rimovibile

Se si usa un'unità USB rimovibile, connetterla al computer in cui si esegue la Creazione guidata del supporto per la sequenza di attività. L'unità USB deve essere rilevabile da Windows come dispositivo rimovibile. La procedura guidata scrive direttamente nell'unità USB durante la creazione del supporto.

### <a name="create-an-output-folder"></a>Creare una cartella di output

Prima di eseguire la Creazione guidata del supporto per la sequenza di attività per creare il supporto per un set di CD o DVD, creare una cartella per i file di output creati dalla procedura guidata. Il supporto creato per un set di CD o DVD viene scritto come file con estensione iso direttamente nella cartella.


## <a name="process"></a>Processo

 > [!NOTE]  
 > Per gli ambienti PKI, dato che la CA radice viene specificata nel sito primario, verificare che il supporto di avvio venga creato nel sito primario. Il sito CAS non contiene informazioni sulla CA radice sufficienti per creare correttamente il supporto di avvio.

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**, espandere **Sistemi operativi** e selezionare il nodo **Sequenze di attività**.  

2. Nella scheda **Home** della barra multifunzione nel gruppo **Crea** selezionare **Crea supporto per sequenza attività**. Questa azione avvia la Creazione guidata del supporto per la sequenza di attività.  

3. Nella pagina **Seleziona tipo di supporto** specificare le opzioni seguenti:  

    - Selezionare **Supporto di avvio**.  

    - Se si vuole solo consentire la distribuzione del sistema operativo senza richiedere input da parte dell'utente, è possibile selezionare **Consenti distribuzione automatica del sistema operativo**.  

        > [!IMPORTANT]  
        > Quando si seleziona questa opzione, all'utente non vengono richieste informazioni sulla configurazione di rete o su sequenze di attività facoltative. Se si configurano i supporti per la protezione con password, all'utente viene richiesta una password.  

4. Nella pagina **Gestione del supporto** specificare una delle opzioni seguenti:  

    - **Supporto dinamico**: consente a un punto di gestione di reindirizzare il supporto a un altro punto di gestione, in base al percorso del client nei limiti del sito.  

    - **Supporto basato su sito**: Il supporto contatta solo il punto di gestione specificato.  

5. Nella pagina **Tipo di supporto** specificare se il supporto è **un'unità USB rimovibile** o un **set di CD/DVD**. Configurare quindi le opzioni seguenti:  

    > [!IMPORTANT]  
    > Il supporto usa il file system FAT32. Non è possibile creare supporti in un'unità USB il cui contenuto include un file di oltre 4 GB.  

    - Se si seleziona **Unità USB rimovibile**, è necessario selezionare l'unità in cui archiviare il contenuto.  

        - **Formatta unità USB rimovibile (FAT32) e consenti l'avvio**: per impostazione predefinita, consente a Configuration Manager di preparare l’unità USB. Molti dispositivi UEFI più recenti richiedono una partizione FAT32 di avvio. Questo formato tuttavia limita anche le dimensioni dei file e la capacità complessiva dell'unità. Se l'unità rimovibile è già stata formattata e configurata, disabilitare questa opzione.

    - Se si seleziona l'opzione **CD/DVD impostato**, specificare la capacità del supporto (**Dimensione supporto**) e il nome e il percorso dei file di output (**File supporto**). La procedura guidata scrive i file di output in questa posizione. ad esempio `\\servername\folder\outputfile.iso`  

        Se la capacità del supporto non è sufficiente per archiviare l'intero contenuto, vengono creati più file. È quindi necessario archiviare il contenuto in più CD o DVD. Quando sono necessari più supporti, Configuration Manager aggiunge un numero di sequenza al nome di ogni file di output creato.  

        > [!IMPORTANT]  
        > Se si seleziona un'immagine iso esistente, la Creazione guidata del supporto per la sequenza di attività elimina l'immagine dall'unità o dalla condivisione non appena si passa alla pagina successiva della procedura guidata. L'immagine esistente viene eliminata, anche se si annulla la procedura guidata.  

    - **Cartella di gestione temporanea**<!--1359388-->: il processo di creazione del supporto può richiedere molto spazio temporaneo sul disco. Per impostazione predefinita questo percorso è simile al seguente: `%UserProfile%\AppData\Local\Temp`. A partire dalla versione 1902, per offrire maggiore flessibilità dal punto di vista del percorso di archiviazione dei file temporanei, modificare questo valore con un'altra unità e un altro percorso.  

    - **Etichetta supporto**<!--1359388-->: a partire dalla versione 1902, è possibile aggiungere un'etichetta al supporto della sequenza di attività. Questa etichetta consente di identificare più facilmente il supporto creato. Il valore predefinito è `Configuration Manager`. Questo campo di testo viene visualizzato nelle posizioni seguenti:  

        - Se si monta un file ISO, Windows visualizza questa etichetta come nome dell'unità montata  

        - Se si formatta un'unità USB, vengono utilizzati i primi 11 caratteri dell'etichetta come nome  

        - Configuration Manager scrive un file di testo denominato `MediaLabel.txt` nella radice del supporto. Per impostazione predefinita, il file include un'unica riga di testo: `label=Configuration Manager`. Se si personalizza l'etichetta del supporto, verrà utilizzata l'etichetta personalizzata anziché il valore predefinito.  

    - **Includi il file autorun.inf sul supporto**<!-- 4090666 -->: a partire dalla versione 1906, Configuration Manager non aggiunge il file autorun.inf per impostazione predefinita. Questo file è generalmente bloccato da prodotti antimalware. Per altre informazioni sulla funzionalità di esecuzione automatica di Windows, vedere [Creating an AutoRun-enabled CD-ROM Application](https://docs.microsoft.com/windows/desktop/shell/autoplay) (Creazione di un'applicazione CD-ROM abilitata per l'esecuzione automatica). Se il file è ancora richiesto dallo scenario, selezionare questa opzione per includerlo.  

6. Nella pagina **Sicurezza** specificare le opzioni seguenti:  

    - **Abilita supporto per computer sconosciuti**: consente al supporto di distribuire un sistema operativo a un computer non gestito da Configuration Manager. Non sono presenti record di questi computer nel database di Configuration Manager. Per altre informazioni, vedere [Operazioni preliminari alle distribuzioni in computer sconosciuti](../get-started/prepare-for-unknown-computer-deployments.md).  

    - **Proteggi supporto con password**: immettere una password complessa per proteggere il supporto dall'accesso non autorizzato. Quando si specifica una password, l'utente deve immettere la password per usare il supporto di avvio.  

        > [!IMPORTANT]  
        > Come procedura consigliata di sicurezza, assegnare sempre una password per proteggere il supporto di avvio.  

    - Per le comunicazioni HTTP, selezionare **Crea certificato del supporto autofirmato**. Specificare quindi la data di inizio e di scadenza del certificato.  
    
      > [!NOTE]  
      > Se si seleziona questa opzione, i punti di gestione HTTPS non saranno disponibili per la selezione nella pagina **Immagine d'avvio** della procedura guidata.

    - Per le comunicazioni HTTPS, selezionare **Importa certificato PKI**. Specificare quindi il certificato da importare e la relativa password.  

        Per altre informazioni su questo certificato client usato dalle immagini d'avvio, vedere [Requisiti dei certificati PKI](../../core/plan-design/network/pki-certificate-requirements.md).  

    - **Affinità utente dispositivo**: per supportare la gestione basata sugli utenti in Configuration Manager, specificare come si vuole che il supporto associ gli utenti al computer di destinazione. Per altre informazioni su come la distribuzione del sistema operativo supporti l'affinità utente-dispositivo, vedere [Associare gli utenti a un computer di destinazione](../get-started/associate-users-with-a-destination-computer.md).  

        - **Consenti affinità utente dispositivo con approvazione automatica**: Il supporto associa automaticamente gli utenti al computer di destinazione. Questa funzionalità si basa sulle azioni della sequenza di attività che distribuisce il sistema operativo. In questo scenario la sequenza di attività crea una relazione tra gli utenti specificati e il computer di destinazione quando distribuisce il sistema operativo nel computer di destinazione.  

        - **Consenti approvazione amministratore in sospeso per affinità utente dispositivo**: Il supporto associa gli utenti al computer di destinazione dopo la concessione dell'approvazione. Questa funzionalità si basa sull'ambito della sequenza di attività che distribuisce il sistema operativo. In questo scenario la sequenza di attività crea una relazione tra gli utenti specificati e il computer di destinazione, ma attende l'approvazione di un utente amministratore prima di distribuire il sistema operativo.  

        - **Non consentire affinità utente dispositivo**: il supporto non associa gli utenti al computer di destinazione. In questo scenario la sequenza di attività non associa gli utenti al computer di destinazione quando distribuisce il sistema operativo.  

7. Nella pagina **Immagine d'avvio** specificare le opzioni seguenti:  

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

8. Nella pagina **Personalizzazione** specificare le opzioni seguenti:  

    - Aggiungere eventuali variabili usate dalla sequenza di attività.  

    - **Attiva comando di preavvio**: Specificare i comandi preavvio da eseguire prima dell'esecuzione della sequenza di attività. I comandi di preavvio sono costituiti da uno script o da un eseguibile che può interagire con l'utente in Windows PE prima che venga eseguita la sequenza di attività. Per altre informazioni vedere [Comandi di preavvio del supporto per sequenza attività](../understand/prestart-commands-for-task-sequence-media.md).  

        > [!TIP]  
        > Durante la creazione del supporto, tale sequenza scrive l'ID del pacchetto e la riga di comando di preavvio, incluso il valore per eventuali variabili della sequenza di attività, nel file **CreateTSMedia.log** nel computer che esegue la console di Configuration Manager. È possibile rivedere questo file di registro per verificare il valore per le variabili della sequenza di attività.  

        Se il comando di preavvio richiede contenuto, selezionare l'opzione **Includi file per il comando di preavvio**.  

9. Completare la procedura guidata.  


## <a name="alternate-method"></a>Metodo alternativo

È possibile creare supporti di avvio in un'unità USB rimovibile quando l'unità non è connessa al computer che esegue la console di Configuration Manager.

1. [Creare il supporto di avvio della sequenza di attività](#process). Nella pagina **Tipo di supporto** selezionare **CD/DVD impostato**. La procedura guidata scrive i file di output nella posizione specificata. Ad esempio: `\\servername\folder\outputfile.iso`.  

2. Preparare l'unità USB rimovibile. L'unità deve essere formattata, vuota e di avvio.

3. Montare l'immagine ISO dal percorso di condivisione e trasferire i file dall'immagine ISO all'unità USB.


## <a name="next-steps"></a>Passaggi successivi

[Usare i supporti di avvio per distribuire Windows in rete](use-bootable-media-to-deploy-windows-over-the-network.md)  
