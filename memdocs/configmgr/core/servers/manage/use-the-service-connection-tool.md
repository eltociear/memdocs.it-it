---
title: Strumento di connessione del servizio
titleSuffix: Configuration Manager
description: Lo strumento consente di connettersi al servizio cloud di Configuration Manager per caricare manualmente le informazioni sull'utilizzo.
ms.date: 07/02/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6e4964c5-43cb-4372-9a89-b62ae6a4775c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 48aa08f3318aaa4629691bfb30b60580cd3e25f0
ms.sourcegitcommit: 03d2331876ad61d0a6bb1efca3aa655b88f73119
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/03/2020
ms.locfileid: "85946845"
---
# <a name="use-the-service-connection-tool-for-configuration-manager"></a>Usare lo strumento di connessione del servizio per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Usare lo **strumento di connessione del servizio** quando il punto di connessione del servizio è in modalità offline. È possibile usarlo anche quando i server del sistema del sito Configuration Manager non sono connessi a Internet. Lo strumento consente di mantenere il sito aggiornato con gli aggiornamenti più recenti di Configuration Manager.

Quando viene eseguito, lo strumento si connette al servizio cloud Configuration Manager, carica le informazioni di utilizzo per la gerarchia e scarica gli aggiornamenti. Il caricamento dei dati di utilizzo è necessario per abilitare il servizio cloud, in modo che offra gli aggiornamenti corretti per l'ambiente in uso.

## <a name="prerequisites"></a>Prerequisiti

- Il sito ha un punto di connessione del servizio e viene configurato con l'impostazione **Offline, connessione su richiesta**.

- Eseguire lo strumento al prompt dei comandi come amministratore. Non è disponibile un'interfaccia utente.

- Lo strumento deve essere eseguito dal punto di connessione del servizio e da un computer in grado di connettersi a Internet. Ognuno di questi computer deve avere un sistema operativo x64 e i componenti seguenti:

  - File x86 e x64 di **Visual C++ Redistributable** . Per impostazione predefinita, Configuration Manager installa la versione x64 nel computer che ospita il punto di connessione del servizio. Per scaricare questo componente, vedere [Visual C++ Redistributable Package per Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=40784).

  - **.NET Framework 4.5.2** o versioni successive

- L'account usato per eseguire lo strumento deve avere le autorizzazioni seguenti:

  - **Amministratore locale** nel computer che ospita il punto di connessione del servizio

  - Autorizzazioni di **lettura** per il database del sito

- È necessario un metodo per trasferire i file tra il computer con accesso a Internet e il punto di connessione del servizio. Ad esempio, un'unità USB con spazio libero sufficiente per l'archiviazione dei file e degli aggiornamenti.

## <a name="overview"></a>Panoramica

1. **Preparazione**: eseguire lo strumento nel punto di connessione del servizio. Lo strumento inserisce i dati di utilizzo in un file con estensione cab nel percorso specificato. Copiare il file di dati nel computer con connessione a Internet.

2. **Connessione**: eseguire lo strumento nel computer con connessione a Internet. Lo strumento carica i dati di utilizzo e quindi scarica gli aggiornamenti di Configuration Manager. Copiare gli aggiornamenti scaricati nel punto di connessione del servizio.

    È possibile caricare più file di dati contemporaneamente, ognuno da una gerarchia diversa. È anche possibile specificare un server proxy e un utente per il server proxy.

3. **Importazione**: eseguire lo strumento nel punto di connessione del servizio. Lo strumento importa gli aggiornamenti e li aggiunge al sito. È quindi possibile visualizzare e [installare gli aggiornamenti](install-in-console-updates.md) nella console di Configuration Manager.

### <a name="upload-multiple-data-files"></a>Caricare più file di dati

- Inserire tutti i file di dati esportati da gerarchie separate nella stessa cartella. Assegnare un nome univoco a ogni file. Se necessario, è possibile rinominare manualmente i file.

- Quando si esegue lo strumento per caricare i dati in Microsoft, specificare la cartella che contiene i file di dati.

- Quando si esegue lo strumento per importare i dati, vengono importati solo i dati per la gerarchia corrente.

### <a name="specify-a-proxy-server"></a>Specificare un server proxy

Se il computer con connessione a Internet richiede un server proxy, lo strumento supporta una configurazione proxy di base. Usare i parametri facoltativi **-proxyserveruri** e **-proxyusername**. Per altre informazioni, vedere [Parametri della riga di comando](#bkmk_cmd).

### <a name="specify-the-type-of-updates-to-download"></a>Specificare il tipo di aggiornamenti da scaricare

Lo strumento supporta opzioni per controllare quali file vengono scaricati. Per impostazione predefinita, lo strumento consente di scaricare solo l'aggiornamento più recente disponibile adeguato alla versione del sito. Non scarica gli hotfix.

Per modificare questo comportamento, usare uno dei parametri seguenti per impostare i file scaricati.

- **-downloadall**: scaricare tutti gli aggiornamenti, inclusi gli aggiornamenti e gli hotfix, indipendentemente dalla versione del sito.
- **-downloadhotfix**: scaricare tutti gli hotfix, indipendentemente dalla versione del sito.
- **-downloadsiteversion**: scaricare gli aggiornamenti e gli hotfix con versione successiva a quella del sito.

    > [!IMPORTANT]
    > A causa di un problema noto in Configuration Manager versione 2002, il comportamento predefinito non funziona come previsto. Usare il parametro **-downloadsiteversion** per scaricare gli aggiornamenti necessari per la versione 2002.<!-- 7594517 -->

Per altre informazioni, vedere [Parametri della riga di comando](#bkmk_cmd).

> [!TIP]
> Lo strumento determina la versione del sito dal file di dati. Per verificare la versione, cercare nel file con estensione cab il file di testo con il nome corrispondente alla versione del sito.

## <a name="use-the-tool"></a>Usare lo strumento  

Lo strumento di connessione del servizio si trova nel supporto di installazione di Configuration Manager, nel percorso seguente: `SMSSETUP\TOOLS\ServiceConnectionTool\ServiceConnectionTool.exe`. Usare sempre lo strumento di connessione del servizio che corrisponde alla versione di Configuration Manager in uso. Per il funzionamento dello strumento di connessione del servizio, tutti questi file devono trovarsi nella stessa cartella.

Copiare la cartella **ServiceConnectionTool** e tutto il suo contenuto nel computer con connessione a Internet.

In questa procedura gli esempi della riga di comando usano i nomi file e i percorsi delle cartelle seguenti. Non è necessario usare questi percorsi e nomi file. È possibile usare alternative adatte all'ambiente e alle preferenze in uso.

- Percorso dei file di origine del supporto di installazione di Configuration Manager nel punto di connessione del servizio: `C:\Source`

- Percorso di un'unità USB in cui archiviare i dati da trasferire tra i computer: `D:\USB\`

- Nome del file di dati esportato dal sito: `UsageData.cab`

- Nome della cartella vuota in cui lo strumento archivia gli aggiornamenti scaricati per Configuration Manager: `UpdatePacks`

### <a name="prepare"></a>Preparazione

1. Nel computer che ospita il punto di connessione del servizio aprire un prompt dei comandi come amministratore e passare alla directory in cui si trova lo strumento. Ad esempio:

    `cd C:\Source\SMSSETUP\TOOLS\ServiceConnectionTool\`

1. Eseguire il comando seguente per preparare il file di dati:

    `ServiceConnectionTool.exe -prepare -usagedatadest D:\USB\UsageData.cab`

    > [!NOTE]
    > Se si prevede di caricare file di dati da più gerarchie nello stesso momento, assegnare un nome univoco a ogni file di dati. Se necessario, è possibile rinominare i file in un secondo momento.

    I dati nel file si basano sul livello dei dati di diagnostica e di utilizzo configurato per il sito. Per altre informazioni, vedere [Panoramica dei dati di diagnostica e di utilizzo](../../plan-design/diagnostics/diagnostics-and-usage-data.md). È possibile usare lo strumento per esportare i dati in un file con estensione csv per visualizzarne il contenuto. Per altre informazioni, vedere [-export](#-export).

1. Quando lo strumento completa l'esportazione dei dati di utilizzo, copiare il file di dati in un computer che dispone di accesso a Internet.

### <a name="connect"></a>Connessione

1. Nel computer con accesso a Internet aprire un prompt dei comandi come amministratore e passare alla directory in cui si trova lo strumento. Questo percorso è una copia dell'intera cartella **ServiceConnectionTool**. Ad esempio:

    `cd D:\USB\ServiceConnectionTool\`

1. Eseguire il comando seguente per caricare il file di dati e scaricare gli aggiornamenti di Configuration Manager:

    `ServiceConnectionTool.exe -connect -usagedatasrc D:\USB -updatepackdest D:\USB\UpdatePacks`

    Per altri esempi, vedere [Parametri della riga di comando](#bkmk_cmd).

    > [!NOTE]  
    > Quando si esegue questa riga di comando è possibile che venga visualizzato l'errore seguente:
    >
    > **Eccezione non gestita: System.UnauthorizedAccessException: Accesso al percorso 'C:\ Users\br\AppData\Local\Temp\extractmanifestcab\95F8A562.sql' negato.**
    >
    > È possibile ignorare questo errore. Chiudere la finestra dell'errore per continuare.

1. Quando lo strumento completa il download degli aggiornamenti, copiare gli aggiornamenti nel punto di connessione del servizio.

### <a name="import"></a>Importazione

1. Nel computer che ospita il punto di connessione del servizio aprire un prompt dei comandi come amministratore e passare alla directory in cui si trova lo strumento. Ad esempio:

    `cd C:\Source\SMSSETUP\TOOLS\ServiceConnectionTool\`

1. Immettere il seguente comando per importare gli aggiornamenti:

    `ServiceConnectionTool.exe -import -updatepacksrc D:\USB\UpdatePacks`

1. Al termine dell'importazione, chiudere il prompt dei comandi. Vengono importati solo gli aggiornamenti per la gerarchia applicabile.

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione** e selezionare il nodo **Aggiornamenti e manutenzione**. Gli aggiornamenti importati sono ora disponibili per l'installazione. Per altre informazioni, vedere [Installare gli aggiornamenti nella console](install-in-console-updates.md).

## <a name="log-files"></a>File di registro

- **ServiceConnectionTool.log**: ogni volta che viene eseguito, lo strumento di connessione del servizio scrive in questo file di log. Il percorso del file di log è sempre lo stesso dello strumento. Questo file di log include semplici dettagli sull'uso dello strumento in base ai parametri usati. Ogni volta che si esegue lo strumento, qualsiasi file di log esistente viene sostituito.

- **ConfigMgrSetup.log**: durante la fase [Connessione](#connect) lo strumento scrive in questo file di log nella radice dell'unità di sistema. Questo file di log include informazioni più dettagliate. Ad esempio indica quali file vengono scaricati dallo strumento e se i controlli hash hanno esito positivo.

## <a name="command-line-parameters"></a><a name="bkmk_cmd"></a> Parametri della riga di comando

Questa sezione elenca in ordine alfabetico tutti i parametri disponibili per lo strumento di connessione del servizio.

### <a name="-connect"></a>-connect

Usare durante la fase [Connessione](#connect) sul computer con accesso a Internet. Si connette al servizio cloud Configuration Manager per caricare il file di dati e scaricare gli aggiornamenti.

Richiede i seguenti parametri:

- **-usagedatasrc**: percorso del file di dati da caricare
- **-updatepackdest**: percorso degli aggiornamenti scaricati

È anche possibile usare i seguenti parametri facoltativi:

- **-proxyserveruri**: nome di dominio completo (FQDN) del server proxy
- **-proxyusername**: nome utente per il server proxy
- **-downloadall**: scaricare tutti gli elementi, inclusi aggiornamenti e hotfix, indipendentemente dalla versione del sito.
- **-downloadhotfix**: vengono scaricati tutti gli hotfix, indipendentemente dalla versione del sito.
- **-downloadsiteversion**: vengono scaricati gli aggiornamenti e gli hotfix con versione successiva a quella del sito.

#### <a name="example-of-connect-without-a-proxy-server"></a>Esempio di connessione senza un server proxy

`ServiceConnectionTool.exe -connect -usagedatasrc D:\USB\ -updatepackdest D:\USB\UpdatePacks`

#### <a name="example-of-connect-with-a-proxy-server"></a>Esempio di connessione con un server proxy

`ServiceConnectionTool.exe -connect -usagedatasrc D:\USB\Usagedata.cab -updatepackdest D:\USB\UpdatePacks -proxyserveruri itproxy.contoso.com -proxyusername jqpublic`

#### <a name="example-of-connect-to-download-only-site-version-applicable-updates"></a>Esempio di connessione per scaricare solo gli aggiornamenti della versione del sito applicabili

`ServiceConnectionTool.exe -connect -downloadsiteversion -usagedatasrc D:\USB -updatepackdest D:\USB\UpdatePacks`

### <a name="-dest"></a>-dest

Parametro obbligatorio con il parametro **-export** per specificare il percorso e il nome del file con estensione csv da esportare. Per altre informazioni, vedere [-export](#-export).

### <a name="-downloadall"></a>-downloadall

Parametro facoltativo con il parametro **-connect** che consente di scaricare tutti gli elementi, inclusi gli aggiornamenti e gli hotfix, indipendentemente dalla versione del sito. Per altre informazioni, vedere [-connect](#connect).

### <a name="-downloadhotfix"></a>-downloadhotfix

Parametro facoltativo con il parametro **-connect** che consente di scaricare solo tutti gli hotfix, indipendentemente dalla versione del sito. Per altre informazioni, vedere [-connect](#-connect).

### <a name="-downloadsiteversion"></a>-downloadsiteversion

Parametro facoltativo con il parametro **-connect** che consente scaricare solo gli aggiornamenti e gli hotfix con versione successiva a quella del sito. Per altre informazioni, vedere [-connect](#-connect).

### <a name="-export"></a>-export

Usare durante la fase [Preparazione](#prepare) per esportare i dati di utilizzo in un file con estensione csv. Eseguire come amministratore nel punto di connessione del servizio. Questa azione consente di esaminare il contenuto dei dati di utilizzo prima di caricarli in Microsoft. Richiede il parametro **-dest** per specificare il percorso del file con estensione csv.

#### <a name="example-of-export"></a>Esempio di export

`-export -dest D:\USB\usagedata.csv`

### <a name="-import"></a>-import

Usare durante la fase [Importazione](#import) nel punto di connessione del servizio per importare gli aggiornamenti al sito. Per specificare il percorso degli aggiornamenti scaricati è necessario il parametro **-updatepacksrc**.

#### <a name="example-of-import"></a>Esempio di import

`ServiceConnectionTool.exe -import -updatepacksrc D:\USB\UpdatePacks`

### <a name="-prepare"></a>-prepare

Usare durante la fase [Preparazione](#prepare) nel punto di connessione del servizio per esportare i dati di utilizzo dal sito. Per specificare il percorso del file di dati esportato è necessario il parametro **-usagedatadest**.

#### <a name="example-of-prepare"></a>Esempio di prepare

`ServiceConnectionTool.exe -prepare -usagedatadest D:\USB\UsageData.cab`

### <a name="-proxyserveruri"></a>-proxyserveruri

Parametro facoltativo con il parametro **-connect** che specifica il nome di dominio completo del server proxy. Per altre informazioni, vedere [-connect](#-connect).

### <a name="-proxyusername"></a>-proxyusername

Parametro facoltativo con il parametro **-connect** che specifica il nome utente da autenticare con il server proxy. Per altre informazioni, vedere [-connect](#-connect).

### <a name="-updatepackdest"></a>-updatepackdest

Parametro obbligatorio con il parametro **-connect** che specifica il percorso per gli aggiornamenti scaricati. Per altre informazioni, vedere [-connect](#-connect).

### <a name="-updatepacksrc"></a>-updatepacksrc

Parametro obbligatorio con il parametro **-import** che specifica il percorso per gli aggiornamenti scaricati. Per altre informazioni, vedere [-import](#-import).

### <a name="-usagedatadest"></a>-usagedatadest

Parametro obbligatorio con il parametro **-prepare** che specifica il percorso e il nome del file di dati esportato. Per altre informazioni, vedere [-prepare](#-prepare).

## <a name="next-steps"></a>Passaggi successivi

[Installare gli aggiornamenti nella console](install-in-console-updates.md)

[Come visualizzare i dati di diagnostica e di utilizzo](../../plan-design/diagnostics/view-diagnostics-and-usage-data.md)
