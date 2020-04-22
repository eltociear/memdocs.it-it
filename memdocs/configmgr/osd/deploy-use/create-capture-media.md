---
title: Creare supporti di acquisizione
titleSuffix: Configuration Manager
description: Usare supporto di acquisizione in Configuration Manager per acquisire un'immagine del sistema operativo da un computer di riferimento.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: article
ms.assetid: 10eb8958-3848-49d7-95c0-16119b624580
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fbbec355356a74d61f263fe2b16d44c0cd15ba80
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690769"
---
# <a name="create-capture-media"></a>Creare supporti di acquisizione

*Si applica a: Configuration Manager (Current Branch)*

Il supporto di acquisizione in Configuration Manager consente di acquisire un'immagine del sistema operativo da un computer di riferimento. Contiene l'immagine d'avvio che avvia il computer di riferimento e la sequenza di attività che acquisisce l'immagine del sistema operativo. Usare i supporti di acquisizione per lo scenario per [Creare una sequenza di attività per acquisire un sistema operativo](create-a-task-sequence-to-capture-an-operating-system.md).  


## <a name="prerequisites"></a>Prerequisiti

Prima di creare supporti di acquisizione usando la Creazione guidata del supporto per la sequenza di attività, assicurarsi che tutte queste condizioni siano soddisfatte.

### <a name="boot-image"></a>Immagine d'avvio

Tenere in considerazione i punti seguenti per l'immagine d'avvio da usare nella sequenza di attività per distribuire il sistema operativo:

- L'architettura dell'immagine d'avvio deve essere appropriata per l'architettura del computer di destinazione. Ad esempio, un computer di destinazione x64 può avviare ed eseguire un'immagine di avvio x86 o x64. Tuttavia, un computer di destinazione x86 può avviare ed eseguire solo un'immagine di avvio x86.
- Assicurarsi che l'immagine d'avvio contenga i driver di archiviazione e di rete necessari per eseguire il provisioning del computer di destinazione.

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Distribuire tutto il contenuto associato alla sequenza di attività

Distribuire tutto il contenuto richiesto dalla sequenza di attività in almeno un punto di distribuzione. Tale contenuto include l'immagine d'avvio, l'immagine del sistema operativo e altri file associati. La procedura guidata raccoglie il contenuto dal punto di distribuzione quando crea il supporto di acquisizione.

L'account utente usato deve avere almeno diritti di accesso in **lettura** per la raccolta contenuto nel punto di distribuzione. Per altre informazioni, vedere [Distribuire il contenuto](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

### <a name="prepare-the-removable-usb-drive"></a>Preparare l'unità USB rimovibile

Se si usa un'unità USB rimovibile, connetterla al computer in cui si esegue la Creazione guidata del supporto per la sequenza di attività. L'unità USB deve essere rilevabile da Windows come dispositivo rimovibile. La procedura guidata scrive direttamente nell'unità USB durante la creazione del supporto.

### <a name="create-an-output-folder"></a>Creare una cartella di output

Prima di eseguire la Creazione guidata del supporto per la sequenza di attività per creare il supporto per un set di CD o DVD, creare una cartella per i file di output creati dalla procedura guidata. Il supporto creato per un set di CD o DVD viene scritto come file con estensione iso direttamente nella cartella.


## <a name="process"></a>Processo

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**, espandere **Sistemi operativi** e selezionare il nodo **Sequenze di attività**.  

2. Nella scheda **Home** della barra multifunzione nel gruppo **Crea** selezionare **Crea supporto per sequenza attività**. Questa azione avvia la Creazione guidata del supporto per la sequenza di attività.  

3. Nella pagina **Seleziona tipo di supporto** selezionare **Acquisisci supporto**.  

4. Nella pagina **Tipo di supporto** specificare se il supporto è **un'unità USB rimovibile** o un **set di CD/DVD**. Configurare quindi le opzioni seguenti:  

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

5. Nella pagina **Immagine d'avvio** specificare le opzioni seguenti:  

    > [!IMPORTANT]  
    > L'architettura dell'immagine d'avvio distribuita deve essere appropriata per l'architettura del computer di destinazione. Ad esempio, un computer di destinazione x64 può avviare ed eseguire un'immagine di avvio x86 o x64. Tuttavia, un computer di destinazione x86 può avviare ed eseguire solo un'immagine di avvio x86.  

    - **Immagine d'avvio**: selezionare l'immagine di avvio per avviare il computer di destinazione.  

    - **Punto di distribuzione**: selezionare il punto di distribuzione che ospita l'immagine d'avvio. La procedura guidata consente di recuperare l'immagine di avvio dal punto di distribuzione e di scriverla sul supporto.  

        > [!NOTE]  
        > L'account utente usato deve avere almeno autorizzazioni di **lettura** per la raccolta contenuto nel punto di distribuzione.  

6. Completare la procedura guidata.  


## <a name="next-steps"></a>Passaggi successivi

[Creare una sequenza di attività per acquisire un sistema operativo](create-a-task-sequence-to-capture-an-operating-system.md)
