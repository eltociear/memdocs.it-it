---
title: Downloader di installazione
titleSuffix: Configuration Manager
description: Leggere le informazioni su questa applicazione autonoma progettata per assicurare che l'installazione del sito usi le versioni correnti dei file di installazione principali.
ms.date: 01/22/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bda87fc5-2e4c-4992-98a4-01770365038c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2fa1899f8e7dc14812f9f9ecf889350a153b2d25
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700569"
---
# <a name="setup-downloader-for-configuration-manager"></a>Downloader di installazione per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Prima di eseguire il programma di installazione per installare o aggiornare un sito di Configuration Manager, è possibile usare l'applicazione autonoma downloader di installazione dalla versione di Configuration Manager che si vuole installare per scaricare i file di installazione aggiornati.  

L'uso di file di installazione aggiornati assicura che l'installazione del sito usi le versioni correnti dei file di installazione principali. Panoramica:   
-   Quando si usa il Downloader di installazione per scaricare i file prima di avviare il programma di installazione, specificare la cartella che contiene i file.  
-   L'account usato per eseguire l'installazione del downloader deve avere autorizzazioni di tipo **Controllo completo** per accedere alla cartella del download.  
-   Quando si esegue il programma di installazione per installare o aggiornare un sito, è possibile indirizzarlo per l'uso di questa copia locale dei file scaricati in precedenza. In questo modo, si evita che il programma di installazione debba connettersi a Microsoft quando si avvia l'installazione o l'aggiornamento del sito.  
-   È possibile usare la stessa copia locale dei file di installazione per gli aggiornamenti o le installazioni successive del sito.  

I tipi di file seguenti vengono scaricati dal Downloader di installazione:  
-   File ridistribuibili dei prerequisiti obbligatori  
-   Language Pack  
-   Aggiornamenti più recenti del programma di installazione  

Sono disponibili due opzioni per l'esecuzione del downloader di installazione:
- Eseguire l'applicazione con l'interfaccia utente
- Per le opzioni della riga di comando, eseguire l'applicazione al prompt dei comandi


## <a name="run-setup-downloader-with-the-user-interface"></a><a name="bkmk_ui"></a> Eseguire il Downloader di installazione con l'interfaccia utente  

1.  In un computer con accesso a Internet, aprire Esplora risorse e passare a **&lt;ConfigMgrInstallationMedia\>\SMSSETUP\BIN\X64**.  

2.  Per aprire il downloader di installazione, fare doppio clic su **Setupdl.exe**.   

3. Specificare il percorso della cartella che ospiterà i file di installazione aggiornati e quindi fare clic su **Download**. Il downloader di installazione verifica i file nella cartella di download. E scarica solo i file mancanti o più recenti rispetto ai file esistenti. Il downloader di installazione crea sottocartelle per le lingue scaricate e altre sottocartelle necessarie.  

4.  Per rivedere i risultati del download, aprire il file **ConfigMgrSetup.log** nella directory radice dell'unità C.  

## <a name="run-setup-downloader-from-a-command-prompt"></a><a name="bkmk_cmd"></a> Eseguire il Downloader di installazione da un prompt dei comandi  

1.  In una finestra del prompt dei comandi passare a **&lt;*Supporti di installazione di Configuration Manager*\>\SMSSETUP\BIN\X64**.   

2.  Eseguire **Setupdl.exe** per aprire il downloader di installazione.

    Con **Setupdl.exe** è possibile usare le seguenti opzioni della riga di comando:   

    -   **/VERIFY**: usare questa opzione per verificare i file nella cartella di download, inclusi i file di lingua. Rivedere il file ConfigMgrSetup.log nella directory radice dell'unità C per un elenco di file non aggiornati. Se si usa questa opzione, non verrà scaricato alcun file.  

    -   **/VERIFYLANG**: usare questa opzione per verificare i file di lingua nella cartella di download. Rivedere il file ConfigMgrSetup.log nella directory radice dell'unità C per un elenco di file di lingue non aggiornati.

    -   **/LANG**: usare questa opzione per scaricare solo i file della lingua nella cartella di download.  

    -   **/NOUI**: usare questa opzione per avviare il Downloader di installazione senza visualizzare l'interfaccia utente. Quando si usa questa opzione, è necessario specificare il **percorso di download** come parte della riga di comando al prompt dei comandi.  

    -   **&lt;DownloadPath\>** : è possibile specificare il percorso della cartella di download per avviare automaticamente la verifica o il processo di download. Quando si usa l'opzione **/NOUI**, è necessario specificare il percorso di download. Se non si specifica un percorso di download, sarà necessario specificarlo all'apertura del downloader di installazione. Il downloader di installazione crea la cartella se non esiste già.  

    Comandi di esempio:

    -   **setupdl &lt;PercorsoDownload\>**  

        -   Il downloader di installazione viene avviato, verifica i file nella cartella di download specificata e scarica solo i file mancanti o più recenti rispetto a quelli esistenti.     

    -   **setupdl /VERIFY &lt;PercorsoDownload\>**  

        -   Il Downloader di installazione viene avviato e verifica i file nella cartella di download specificata.  

    -   **setupdl /NOUI &lt;PercorsoDownload\>**  

        -   Il downloader di installazione viene avviato, verifica i file nella cartella di download specificata e scarica solo i file mancanti o più recenti rispetto a quelli esistenti.  

    -   **setupdl /LANG  &lt;PercorsoDownload\>**  

        -   Il downloader di installazione viene avviato, verifica i file della lingua nella cartella di download specificata e scarica solo i file della lingua mancanti o i file più recenti rispetto a quelli esistenti.  

    -   **setupdl /VERIFY**  

        -   Il Downloader di installazione viene avviato e quindi è necessario specificare il percorso alla cartella di download. Dopo aver fatto clic su **Verifica**, il downloader di installazione verifica i file nella cartella di download.  

3.  Per rivedere i risultati del download, aprire il file **ConfigMgrSetup.log** nella directory radice dell'unità C.

## <a name="copy-setup-downloader-files-to-another-computer"></a><a name="bkmk_cp-files"></a> Copiare i file del Downloader di installazione in un altro computer

1. In Esplora risorse passare a una delle posizioni seguenti:

    - **&lt;Supporto di installazione di Configuration Manager>\SMSSETUP\BIN\X64**
    - **&lt;Percorso di installazione di Configuration Manager>\BIN\X64**
    
1. Copiare i file seguenti nella cartella di destinazione in un altro computer:
    
    - **setupdl.exe**
    - **.\\&lt;lingua>\\setupdlres.dll**
      - Questo file si trova nella sottocartella per la lingua di installazione. Ad esempio, l'inglese si trova nella sottocartella `00000409`.

    Ad esempio, le cartelle di destinazione nel dispositivo dovrebbero avere un aspetto simile al seguente:
    - C:\ConfigManInstall\setupdl.exe
    - C:\ConfigManInstall\00000409\setupdlres.dll

1. Avviare il Downloader di installazione dal computer usando l'[interfaccia utente](#bkmk_ui) o il [prompt dei comandi](#bkmk_cmd), descritto nelle sezioni precedenti.
