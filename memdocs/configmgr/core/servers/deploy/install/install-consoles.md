---
title: Installare la console
titleSuffix: Configuration Manager
description: Installare la console di Configuration Manager per la connessione a un sito di amministrazione centrale o a un sito primario.
ms.date: 04/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d39c201f-d364-4e7b-bde4-faa76d747f33
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f5fda03090f7ec69eb78b20385dfc009bac88f40
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700799"
---
# <a name="install-the-configuration-manager-console"></a>Installare la console di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Gli amministratori usano la console di Configuration Manager per gestire l'ambiente di Configuration Manager. Ogni console di Configuration Manager può connettersi a un sito di amministrazione centrale o a un sito primario. Non è possibile connettere una console di Configuration Manager a un sito secondario.

La console di Configuration Manager viene sempre installata nel server del sito per il sito di amministrazione centrale o un sito primario. Per installare la console in un momento diverso rispetto all'installazione del server del sito, eseguire il programma di installazione autonomo.  



## <a name="prerequisites"></a>Prerequisiti

- Avere i diritti di **Amministratore** locale nel computer in cui verrà installata la console.  

- Si dispone di autorizzazioni di **lettura** per il percorso dei file di installazione della console di Configuration Manager.  



## <a name="source-paths"></a>Percorsi di origine

Decidere quale percorso di origine usare:  

- Cartella ConsoleSetup nel server del sito: `<Configuration Manager site server installation path>\Tools\ConsoleSetup`  

    Quando si installa un server del sito, i file di installazione della console e i Language Pack supportati per il sito vengono copiati nella sottocartella **Tools\ConsoleSetup**. Facoltativamente, è possibile copiare la cartella **ConsoleSetup** in un percorso alternativo per avviare l'installazione. Quando si aggiorna il sito, la versione locale viene sempre mantenuta aggiornata.  

- Supporto di installazione di Configuration Manager: `<Configuration Manager installation media>\SMSSETUP\BIN\I386`  

    Quando si installa la console di Configuration Manager dai supporti di installazione viene sempre installata la versione in lingua inglese. Questo comportamento si verifica anche se il server del sito supporta diverse lingue o il sistema operativo del computer di destinazione è impostato su una lingua diversa.  

Quando possibile, avviare il programma di installazione della console dalla cartella **ConsoleSetup** piuttosto che dal supporto di origine.

> [!Important]  
> Non installare la console usando i file di origine **CD.Latest**. Questo scenario non è supportato e potrebbe causare problemi con l'installazione della console. Per altre informazioni, vedere [Cartella CD.Latest](../../manage/the-cd.latest-folder.md#unsupported-scenarios).<!-- SCCMDocs issue 1359 -->  

Se si crea un pacchetto per l'installazione della console in altri computer, assicurarsi che il pacchetto includa i file seguenti:<!--3612513-->

- ConsoleSetup.exe
- AdminConsole.msi
- ConfigMgr.AC_Extension.i386.cab (a partire dalla versione 1902)
- ConfigMgr.AC_Extension.amd64.cab (a partire dalla versione 1902)



## <a name="use-the-setup-wizard"></a>Usare l'installazione guidata  

1. Passare al percorso di origine e aprire **ConsoleSetup.exe**.  

    > [!IMPORTANT]  
    > Installare sempre la console tramite **ConsoleSetup.exe**. Anche se è possibile installare la console di Configuration Manager eseguendo AdminConsole.msi, con questo metodo non viene eseguita la verifica delle dipendenze o dei prerequisiti. L'installazione potrebbe non essere completata correttamente.  

2. Nella procedura guidata selezionare **Avanti**.  

3. Nella pagina **Server del sito** immettere il nome di dominio completo (FQDN) del server del sito al quale si connette la console di Configuration Manager.  

4. Nella pagina **Cartella di installazione** immettere la cartella di installazione per la console di Configuration Manager. Il percorso della cartella non può includere spazi finali o caratteri Unicode.  

5. Nella pagina **Analisi utilizzo software** selezionare se partecipare all'Analisi utilizzo software.  

    > [!Note]  
    > A partire da Configuration Manager versione 1802, la funzionalità Analisi utilizzo software è stata rimossa dal prodotto.

6. Nella pagina **Pronto per l'installazione** selezionare **Installa**.  



## <a name="install-from-a-command-prompt"></a>Installazione da un prompt dei comandi  

> [!TIP]  
> Quando si installa la console di Configuration Manager da un prompt dei comandi viene sempre installata la versione in lingua inglese. Questo comportamento si verifica anche se il sistema operativo del computer di destinazione è impostato su una lingua diversa. Per installare la console di Configuration Manager in una lingua diversa dall'inglese [usare l'installazione guidata](#use-the-setup-wizard).  


### <a name="consolesetupexe-command-line-options"></a>Opzioni della riga di comando di ConsoleSetup.exe

#### <a name="q"></a>/q

Installa la console di Configuration Manager in modalità automatica. Le opzioni **EnableSQM**, **TargetDir**e **DefaultSiteServerName** sono obbligatorie solo quando si usa questa opzione.

#### <a name="uninstall"></a>/uninstall

Disinstalla la console di Configuration Manager. Specificare per prima questa opzione quando viene usata con l'opzione **/q**.

#### <a name="langpackdir"></a>LangPackDir

Specifica il percorso alla cartella che contiene i file di lingua. È possibile usare il **Downloader di installazione** per scaricare i file di lingua. Se non si usa questa opzione, il programma di installazione cerca la cartella della lingua nella cartella corrente. Se la cartella della lingua non viene trovata, il programma di installazione prosegue con l'installazione della sola versione in lingua inglese. Per altre informazioni, vedere [Setup Downloader](setup-downloader.md) (Downloader di installazione).

#### <a name="targetdir"></a>TargetDir

Specifica la cartella di installazione per installare la console di Configuration Manager. Questa opzione è obbligatoria solo quando si usa l'opzione **/q** .

#### <a name="enablesqm"></a>EnableSQM

Specifica se partecipare all'Analisi utilizzo software (CEIP). Usare un valore di **1** per partecipare all'Analisi utilizzo software e un valore di **0** per non partecipare a tale analisi. Questa opzione è obbligatoria solo quando si usa l'opzione **/q** .

> [!Important]  
> A partire da Configuration Manager versione 1802, la funzionalità Analisi utilizzo software è stata rimossa dal prodotto. Se si usa il parametro, l'installazione non riuscirà.

#### <a name="defaultsiteservername"></a>DefaultSiteServerName

Specifica l'FQDN del server del sito a cui si connette la console all'apertura. Questa opzione è obbligatoria solo quando si usa l'opzione **/q** .


### <a name="examples"></a>Esempi

> [!Important]  
> Per le versioni 1802 e successive non includere il parametro **EnableSQM**

#### <a name="silent-install"></a>Installazione invisibile all'utente

`ConsoleSetup.exe /q TargetDir="%ProgramFiles%\ConfigMgr Console" DefaultSiteServerName=MyServer.Contoso.com`

#### <a name="silent-install-with-language-packs"></a>Installazione invisibile all'utente con i Language Pack

`ConsoleSetup.exe /q TargetDir="C:\Program Files\ConfigMgr Console" DefaultSiteServerName=MyServer.Contoso.com LangPackDir=C:\Downloads\ConfigMgr`  

#### <a name="silent-uninstall"></a>Disinstallazione invisibile all'utente

`ConsoleSetup.exe /uninstall /q`  



## <a name="see-also"></a>Vedere anche

Gli amministratori possono visualizzare gli oggetti nella console in base alle autorizzazioni assegnate al proprio account utente. Per altre informazioni, vedere [Nozioni fondamentali sull'amministrazione basata su ruoli](../../../understand/fundamentals-of-role-based-administration.md).

Per altre informazioni sui concetti fondamentali relativi allo spostamento nella console di Configuration Manager, vedere [Uso della console](../../manage/admin-console.md).
