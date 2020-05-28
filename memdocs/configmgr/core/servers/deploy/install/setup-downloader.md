---
title: Strumento downloader di installazione
titleSuffix: Configuration Manager
description: Usare lo strumento autonomo per scaricare le versioni correnti dei file di installazione fondamentali per l'installazione.
ms.date: 05/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bda87fc5-2e4c-4992-98a4-01770365038c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2da8aed5cfe4a478010165445094f1fce4627d9a
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83428842"
---
# <a name="setup-downloader-for-configuration-manager"></a>Downloader di installazione per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Prima di eseguire il programma di installazione di Configuration Manager per installare o aggiornare un sito, è possibile usare lo strumento autonomo downloader di installazione per scaricare i file di installazione aggiornati. Eseguire lo strumento dalla versione di Configuration Manager che si vuole installare. Usare file di installazione aggiornati per assicurarsi che l'installazione del sito usi le versioni correnti dei file di installazione principali.

Quando si usa il downloader di installazione, si specifica una cartella in cui inserire i file. L'account usato per eseguire lo strumento deve avere autorizzazioni di tipo **Controllo completo** per la cartella di download. Quando si esegue il programma di installazione per installare o aggiornare un sito, è possibile specificare questa copia locale dei file scaricati in precedenza. Questo comportamento evita che il programma di installazione si connetta a Microsoft quando si avvia l'installazione o l'aggiornamento del sito. È possibile usare la stessa copia locale dei file di installazione per altri aggiornamenti o installazioni della stessa versione.

Lo strumento downloader di installazione scarica i tipi di file seguenti:

- File ridistribuibili dei prerequisiti obbligatori
- Language Pack
- Aggiornamenti più recenti dei prodotti per l'installazione

Per eseguire il downloader di installazione sono disponibili due opzioni:

- Eseguire l'applicazione con l'interfaccia utente
- Eseguire l'applicazione al prompt dei comandi per opzioni della riga di comando aggiuntive

Se l'organizzazione limita le comunicazioni della rete con Internet tramite un firewall o un dispositivo proxy, è necessario consentire allo strumento di accedere agli endpoint Internet. Il dispositivo in cui verrà eseguito lo strumento richiede l'accesso a Internet così come il punto di connessione del servizio. Per altre informazioni, vedere i [requisiti di accesso Internet](../../../plan-design/network/internet-endpoints.md#bkmk_scp).<!-- SCCMDocs#677 -->

## <a name="run-setup-downloader-with-the-user-interface"></a><a name="bkmk_ui"></a> Eseguire il downloader di installazione con l'interfaccia utente

1. In un computer dotato di accesso a Internet, passare al supporto di installazione per la versione di Configuration Manager che si vuole installare.

1. Nella sottocartella **SMSSETUP\BIN\X64** eseguire **Setupdl. exe**.

1. Specificare il percorso della cartella in cui archiviare i file di installazione aggiornati e quindi selezionare **Download**. Il downloader di installazione verifica i file presenti nella cartella di download. E scarica solo i file mancanti o più recenti rispetto ai file esistenti. Crea sottocartelle per le lingue scaricate e altri componenti necessari.

1. Per esaminare i risultati del download, vedere **C:\ConfigMgrSetup.log**.

## <a name="run-setup-downloader-from-a-command-prompt"></a><a name="bkmk_cmd"></a> Eseguire il downloader di installazione al prompt dei comandi

1. Aprire il prompt dei comandi e passare al supporto di installazione per la versione di Configuration Manager che si vuole installare.

1. Passare alla sottocartella **SMSSETUP\BIN\X64** ed eseguire **Setupdl. exe** con le opzioni necessarie.

1. Per esaminare i risultati del download, vedere **C:\ConfigMgrSetup.log**.

### <a name="command-line-options"></a>Opzioni della riga di comando

Con **Setupdl.exe** è possibile usare le seguenti opzioni della riga di comando:

- **/VERIFY**: verifica i file nella cartella di download, inclusi i file di lingua. Per l'elenco dei file obsoleti, vedere **C:\ConfigMgrSetup.log**. Quando si usa questa opzione, non viene scaricato alcun file.

- **/VERIFYLANG**: verifica solo i file di lingua nella cartella di download. Per l'elenco dei file di lingua obsoleti, vedere **C:\ConfigMgrSetup.log**.

- **/LANG**: scarica solo i file di lingua nella cartella di download.

- **/NOUI**: avvia il downloader di installazione senza l'interfaccia utente. Quando si usa questa opzione, è necessario indicare il **percorso di download**.

- **Percorso di download**: per avviare automaticamente il processo di verifica o di download, specificare il percorso della cartella di download. Quando si usa l'opzione **/NOUI**, è necessario indicare il percorso di download. Se non si specifica un percorso di download, il downloader di installazione richiede di specificarlo. Se la cartella non esiste, il downloader di installazione la crea.

### <a name="example-commands"></a>Comandi di esempio

#### <a name="example-1"></a>Esempio 1

Il downloader di installazione verifica i file nella cartella di download specificata e quindi scarica i file.

`setupdl.exe C:\Download`

#### <a name="example-2"></a>Esempio 2

Il downloader di installazione verifica solo i file nella cartella di download specificata.

`setupdl.exe /VERIFY C:\Download`

#### <a name="example-3"></a>Esempio 3:

Il downloader di installazione verifica i file nella cartella di download specificata e quindi scarica i file. Lo strumento non visualizza alcuna interfaccia utente.

`setupdl.exe /NOUI C:\Download`

#### <a name="example-4"></a>Esempio 4

Il downloader di installazione verifica i file di lingua nella cartella di download specificata e quindi scarica solo i file di lingua.

`setupdl.exe /LANG C:\Download`

## <a name="copy-setup-downloader-files-to-another-computer"></a><a name="bkmk_cp-files"></a> Copiare i file del downloader di installazione in un altro computer

1. In Esplora risorse passare a una delle posizioni seguenti:

    - **&lt;Supporto di installazione di Configuration Manager>\SMSSETUP\BIN\X64**

    - **&lt;Percorso di installazione di Configuration Manager>\BIN\X64**

1. Copiare i file seguenti nella cartella di destinazione in un altro computer:

    - **setupdl.exe**

    - **.\\&lt;lingua>\\setupdlres.dll**

        > [!NOTE]
        > Questo file si trova nella sottocartella per la lingua di installazione. Ad esempio, l'inglese si trova nella sottocartella `00000409`.

    Le cartelle di destinazione nel dispositivo dovrebbero avere un aspetto simile all'esempio seguente:

    - `C:\ConfigManInstall\setupdl.exe`

    - `C:\ConfigManInstall\00000409\setupdlres.dll`

1. Eseguire il downloader di installazione dal computer di destinazione. Usare l'[interfaccia utente](#bkmk_ui) o il [prompt dei comandi](#bkmk_cmd).
