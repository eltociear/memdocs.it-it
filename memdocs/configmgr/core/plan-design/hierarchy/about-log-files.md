---
title: Informazioni sui file di log
titleSuffix: Configuration Manager
description: Usare i file di log per la risoluzione dei problemi con i client di Configuration Manager e i sistemi del sito.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b1751e3c-a60c-4ab7-a943-2595df1eb612
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 588bccc533909f2438dc61d6f25b39c3a582c71b
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83879018"
---
# <a name="about-log-files-in-configuration-manager"></a>Informazioni sui file di log di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

In Configuration Manager i componenti client e del server del sito registrano le informazioni di processo in singoli file di log. È possibile usare le informazioni contenute nei file di log per risolvere i problemi che potrebbero verificarsi. Per impostazione predefinita, la registrazione dei componenti client e server è abilitata in Configuration Manager.

Questo articolo include informazioni generali sui file di log di Configuration Manager. Sono inclusi gli strumenti da usare, la configurazione dei log e la posizione in cui trovarli. Per altre informazioni su file di log specifici, vedere [Riferimento per i file di log](log-files.md).


## <a name="how-it-works"></a><a name="BKMK_AboutLogs"></a> Come funziona

La maggior parte dei processi in Configuration Manager scrive le informazioni operative in un file di log dedicato al processo. Questi file di log sono identificati dall'estensione **.log** o **.lo_** . Configuration Manager scrive in un file con estensione .log fino a quando il file non raggiunge la dimensione massima. Quando il log è pieno, il file .log viene copiato in un file con lo stesso nome ma con estensione .lo_ e il processo o il componente continua a scrivere nel file .log. Quando il file .log raggiunge nuovamente la dimensione massima, il file .lo_ viene sovrascritto e il processo si ripete. Alcuni componenti stabiliscono una cronologia per i file di log aggiungendo un indicatore di data e ora al nome del file di log e mantenendo l'estensione di file log.


## <a name="log-viewer-tools"></a><a name="bkmk_tools"></a> Strumenti visualizzatore log

Tutti i file di log di Configuration Manager sono file di testo normale, pertanto è possibile visualizzarli con qualsiasi lettore di testo, ad esempio con il Blocco note. I log usano una formattazione univoca che viene visualizzata in modo ottimale con uno degli strumenti specializzati seguenti:

- [CMTrace](#cmtrace)
- [OneTrace](#onetrace)
- [Visualizzatore log del Supporto tecnico](#support-center-log-viewer)

### <a name="cmtrace"></a>CMTrace

Per visualizzare i log usare lo strumento visualizzatore log **CMTrace** di Configuration Manager. È disponibile nella cartella `\SMSSetup\Tools` del supporto di origine di Configuration Manager. Lo strumento CMTrace viene aggiunto a tutte le immagini di avvio aggiunte alla Raccolta software. Lo strumento per la visualizzazione di log di CMTrace viene ora installato automaticamente insieme al client di Configuration Manager.<!--1357971--> Per altre informazioni, vedere [CMTrace](../../support/cmtrace.md).

### <a name="onetrace"></a>OneTrace

A partire dalla versione 1906 **OneTrace** è un nuovo visualizzatore log del Supporto tecnico. Funziona in modo analogo a CMTrace, con miglioramenti. Per altre informazioni, vedere [Supporto tecnico OneTrace](../../support/support-center-onetrace.md).

### <a name="support-center-log-viewer"></a>Visualizzatore log del Supporto tecnico

Il **Supporto tecnico** include un visualizzatore log aggiornato. Questo strumento sostituisce CMTrace e include un'interfaccia personalizzabile, con il supporto per schede e finestre ancorabili. Offre un livello di presentazione veloce e può caricare file di log di grandi dimensioni in pochi secondi. Per altre informazioni, vedere [Riferimento del visualizzatore log del Supporto tecnico](../../support/support-center-ui-reference.md#bkmk_log-viewer).

> [!Note]  
> Support Center e OneTrace usano Windows Presentation Foundation (WPF). Questo componente non è disponibile in Windows PE. Continuare a usare CMTrace nelle immagini d'avvio con le distribuzioni di sequenze di attività.


## <a name="configure-logging-options"></a><a name="bkmk_logoptions"></a> Configurare le opzioni di registrazione

È possibile modificare la configurazione dei file di log, ad esempio il livello di dettaglio, le dimensioni e la cronologia. Sono disponibili diversi modi per modificare queste impostazioni:

- [Durante l'installazione client](#bkmk_logoptions-clientprop)
- [Tramite Configuration Manager Service Manager](#bkmk_logoptions-sm)
- [Tramite il Registro di sistema di Windows](#bkmk_logoptions-registry)
- [Nella console di Configuration Manager](#bkmk_logoptions-console)

### <a name="configure-logging-options-during-client-installation"></a><a name="bkmk_logoptions-clientprop"></a> Configurare le opzioni di registrazione durante l'installazione client

È possibile impostare la configurazione dei file di log del client durante l'installazione. Usare le proprietà seguenti:

- CCMENABLELOGGING
- CCMDEBUGLOGGING
- CCMLOGLEVEL
- CCMLOGMAXHISTORY
- CCMLOGMAXSIZE

Per altre informazioni, vedere [Informazioni sulle proprietà di installazione del client in System Center Configuration Manager](../../clients/deploy/about-client-installation-properties.md#clientMsiProps).

### <a name="configure-logging-options-by-using-configuration-manager-service-manager"></a><a name="bkmk_logoptions-sm"></a> Configurare le opzioni di registrazione usando Configuration Manager Service Manager

È possibile modificare la posizione in cui Configuration Manager archivia i file di log e le relative dimensioni.  

Per modificare le dimensioni, il nome e il percorso dei file di log o per fare in modo che più componenti scrivano in un unico file di log, eseguire i passaggi seguenti:  

#### <a name="modify-logging-for-a-component"></a>Modificare la registrazione per un componente  

1. Nella console di Configuration Manager passare all'area di lavoro **Monitoraggio**, espandere **Stato del sistema** e selezionare il nodo **Stato del sito** o **Stato componente**.  

2. Nella barra multifunzione selezionare **Start** e quindi scegliere **Configuration Manager Service Manager**.  

3. All'apertura di Configuration Manager Service Manager, connettersi al sito da gestire. Se non viene visualizzato il sito che si vuole gestire, selezionare **Sito**, quindi selezionare **Connetti** e immettere il nome del server del sito corretto.  

4. Espandere il sito e passare a **Componenti** o **Server** in base alla posizione dei componenti da gestire.  

5. Nel riquadro a destra selezionare uno o più componenti.  

6. Scegliere **Registrazione** dal menu **Componente**.  

7. Nella finestra di dialogo **Registrazione componente di Configuration Manager** completare le opzioni di configurazione disponibili per la selezione effettuata.  

8. Selezionare **OK** per salvare la configurazione.  

### <a name="configure-logging-options-by-using-the-windows-registry"></a><a name="bkmk_logoptions-registry"></a> Configurare le opzioni di registrazione usando il registro di sistema di Windows

<!-- SCCMDocs#992 -->
Usare il registro di sistema di Windows nei server o nei client per modificare le opzioni di registrazione seguenti:

- Livello di dettaglio
- Numero massimo di voci della cronologia salvate
- Dimensioni massime

Durante la risoluzione di un problema, è possibile abilitare la registrazione dettagliata in modo che Configuration Manager scriva dettagli aggiuntivi nei file di log.

> [!Warning]
> Una configurazione errata di queste impostazioni può causare la registrazione di grandi quantità di informazioni o di nessuna informazione da parte di Configuration Manager. Questi dati possono essere utili per la risoluzione dei problemi, ma è consigliabile fare attenzione quando si modificano questi valori nei siti di produzione. In primo luogo testare sempre queste modifiche in un ambiente lab. La proprietà può dare origine a un volume eccessivo di registrazioni e quindi rendere difficile l'individuazione delle informazioni desiderate nei file di log.

Dopo avere apportato le modifiche a queste impostazioni del registro di sistema, riavviare il componente:

- Se si modificano le impostazioni client, riavviare il servizio **Host agenti di SMS** (CCMExec).
- Se si modificano le impostazioni del server, riavviare il servizio **SMS Executive**.

Le impostazioni del registro di sistema variano a seconda del componente:

- [Client e punto di gestione](#bkmk_reg-client)
- [Server del sito](#bkmk_reg-site)
- [Ruolo del sistema del sito](#bkmk_reg-role)
- [Console di Configuration Manager](#bkmk_reg-console)

#### <a name="client-and-management-point-logging-options"></a><a name="bkmk_reg-client"></a> Opzioni di registrazione del client e del punto di gestione

Per configurare le opzioni di registrazione per tutti i componenti in un sistema di sito client o punto di gestione, configurare i seguenti valori di **REG_DWORD** sotto la seguente chiave del Registro di sistema di Windows:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Logging\@Global`

|Name  |Valori  |Descrizione  |
|---------|---------|---------|
|LogLevel|`0`: Dettagliato<br>`1`: Predefinito<br>`2`: Avvisi ed errori<br>`3`: Solo errori|Livello di dettagli da scrivere nei file di log.|
|LogMaxHistory|Qualsiasi numero intero maggiore o uguale a zero, ad esempio:<br>`0`: Nessuna cronologia<br>`1`: Predefinito|Quando un file di log raggiunge la dimensione massima, il client lo rinomina come file di backup e crea un nuovo file di log. Specificare il numero di versioni precedenti da mantenere.|
|LogMaxSize|Qualsiasi numero intero maggiore o uguale a 10.000, ad esempio:<br>250000|La dimensione massima del file di log in byte. Quando un log raggiunge la dimensione specificata, il client lo rinomina come file di cronologia e crea un nuovo file. Il valore predefinito è 250.000 byte.|

> [!Note]  
> Non modificare altri valori che potrebbero esistere in questa chiave del Registro di sistema.

Per il debug avanzato è anche possibile aggiungere questo valore **REG_SZ** sotto la seguente chiave del registro di sistema di Windows:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Logging\DebugLogging`

|Name  |Valori  |Descrizione  |
|---------|---------|---------|
|Abilitato | `True`: abilita log di debug<br>`False`: disabilita log di debug |Abilita la registrazione di debug per la risoluzione dei problemi.|

Con questa impostazione il client registra le informazioni di basso livello per la risoluzione dei problemi. Evitare di usare questa impostazione nei siti di produzione. La proprietà può dare origine a un volume eccessivo di registrazioni e quindi rendere difficile l'individuazione delle informazioni desiderate nei file di log. Assicurarsi di disattivare questa impostazione dopo aver risolto il problema.

#### <a name="site-server-logging-options"></a><a name="bkmk_reg-site"></a> Opzioni di registrazione del server del sito

È possibile configurare le impostazioni globalmente o per un componente specifico nel server del sito Configuration Manager.

Configurare questi valori nella seguente chiave del Registro di sistema di Windows:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\Tracing`

|Name  |Valori  |Tipo  |Descrizione
|---------|---------|---------|---------|
|SqlEnabled| `1`: abilita la traccia SQL<br> `0`: disabilita la traccia SQL |REG_DWORD|Aggiungere la registrazione della traccia SQL a tutti i log del server del sito.|
|ArchiveEnabled| `1`: abilita gli archivi log<br> `0`: disabilita gli archivi log | REG_DWORD |Archiviare i log del server del sito in una posizione separata per la conservazione cronologica.|
|ArchivePath| Un percorso di cartella valido, ad esempio `C:\Logs\Archive` | REG_SZ |Percorso per l'archiviazione dei log del server del sito.|

Abilitare la traccia SQL solo a scopo di risoluzione dei problemi. Evitare di usarla nei siti di produzione. La proprietà può dare origine a un volume eccessivo di registrazioni e quindi rendere difficile l'individuazione delle informazioni desiderate nei file di log. Assicurarsi di disattivare questa impostazione dopo aver risolto il problema.

> [!Note]  
> Non modificare altri valori che potrebbero esistere in questa chiave del Registro di sistema.

Per configurare le opzioni di registrazione per un componente server specifico, configurare i seguenti valori di **REG_DWORD** sotto la seguente chiave del Registro di sistema di Windows:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\Tracing\<ComponentName>`

|Name  |Valori  |Descrizione  |
|---------|---------|---------|
|LoggingLevel|`0`: Dettagliato<br>`1`: Predefinito<br>`2`: Avvisi ed errori<br>`3`: Solo errori|Livello di dettagli da scrivere nei file di log.|
|LogMaxHistory|Qualsiasi numero intero maggiore o uguale a zero, ad esempio:<br>`0`: Nessuna cronologia<br>`1`: Predefinito|Quando un file di log raggiunge la dimensione massima, il server lo rinomina come file di backup e crea un nuovo file di log. Specificare il numero di versioni precedenti da mantenere.|
|MaxFileSize|Qualsiasi numero intero maggiore o uguale a 10.000, ad esempio:<br>250000|La dimensione massima del file di log in byte. Quando un log raggiunge la dimensione specificata, il client lo rinomina come file di cronologia e crea un nuovo file. Il valore predefinito è 250.000 byte.|
|DebugLogging| `1`: abilita log di debug<br>`0`: disabilita log di debug |Abilita la registrazione di debug per la risoluzione dei problemi.|

Con l'impostazione DebugLogging il server registra le informazioni di basso livello per la risoluzione dei problemi. Evitare di usare questa impostazione nei siti di produzione. La proprietà può dare origine a un volume eccessivo di registrazioni e quindi rendere difficile l'individuazione delle informazioni desiderate nei file di log. Assicurarsi di disattivare questa impostazione dopo aver risolto il problema.

> [!Note]  
> Non modificare altri valori che potrebbero esistere in questa chiave del Registro di sistema.

#### <a name="site-system-role-logging-options"></a><a name="bkmk_reg-role"></a> Opzioni di registrazione dei ruoli del sistema del sito

È possibile configurare le impostazioni globalmente o per un componente specifico in un sistema del sito che ospita un ruolo del server Configuration Manager.

Per configurare le opzioni di registrazione per un componente server specifico, configurare i seguenti valori di **REG_DWORD** sotto la seguente chiave del Registro di sistema di Windows:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\<ComponentName>\Logging`

Ad esempio per il ruolo punto di distribuzione:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP\Logging`

|Name  |Valori  |Descrizione  |
|---------|---------|---------|
|LogLevel|`0`: Dettagliato<br>`1`: Predefinito<br>`2`: Avvisi ed errori<br>`3`: Solo errori|Livello di dettagli da scrivere nei file di log.|
|LogMaxHistory|Qualsiasi numero intero maggiore o uguale a zero, ad esempio:<br>`0`: Nessuna cronologia<br>`1`: Predefinito|Quando un file di log raggiunge la dimensione massima, il server lo rinomina come file di backup e crea un nuovo file di log. Specificare il numero di versioni precedenti da mantenere.|
|LogMaxSize|Qualsiasi numero intero maggiore o uguale a 10.000, ad esempio:<br>250000|La dimensione massima del file di log in byte. Quando un log raggiunge la dimensione specificata, il server lo rinomina come file di cronologia e crea un nuovo file. Il valore predefinito è 250.000 byte.|

> [!Note]  
> Non modificare altri valori che potrebbero esistere in questa chiave del Registro di sistema.

#### <a name="configuration-manager-console-logging-options"></a><a name="bkmk_reg-console"></a> Opzioni di registrazione della console di Configuration Manager

Per modificare il livello di dettaglio di AdminUI.log per la console di Configuration Manager seguire questa procedura:

1. Aprire il file di configurazione della console **Microsoft.ConfigurationManagement.exe.config** in un editor XML come il Blocco note. Il file di configurazione predefinito si trova nel percorso seguente: `C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\bin\Microsoft.ConfigurationManagement.exe.config`

    > [!IMPORTANT]
    > A partire dalla versione 1910, questo percorso è stato modificato in modo da usare la cartella `Microsoft Endpoint Manager`. Assicurarsi di non usare una versione precedente del file che potrebbe esistere in un'altra cartella.

1. Nell'elemento **system.diagnostics** > **sources** > **source** modificare l'attributo **switchValue** da `Error` a `Verbose`. Ad esempio:

    Riga originale: `<source name="SmsAdminUISnapIn" switchValue="Error">` Nuovo: `<source name="SmsAdminUISnapIn" switchValue="Verbose" >`

1. Salvare il file e riavviare la console.

### <a name="configure-logging-options-in-the-configuration-manager-console"></a><a name="bkmk_logoptions-console"></a> Configurare le opzioni di registrazione nella console di Configuration Manager

<!-- 4433455 -->

A partire dalla versione 1910, abilitare o disabilitare la registrazione dettagliata in un client o una raccolta dalla console:

1. Nella console di Configuration Manager passare all'area di lavoro **Asset e conformità**, selezionare il nodo **Dispositivi** e scegliere un dispositivo di destinazione.

1. Nella scheda **Home** della barra multifunzione, nel gruppo **Dispositivo**, selezionare **Diagnostica client**. Scegliere una delle azioni disponibili.

Per altre informazioni, vedere [Diagnostica client](../../clients/manage/client-notification.md#client-diagnostics).

## <a name="locating-log-files"></a><a name="BKMK_LogLocation"></a> Come trovare i file di log

Configuration Manager e i componenti dipendenti archiviano i file di log in diverse posizioni. Queste posizioni dipendono dal processo che crea il file di log e dalla configurazione dell'ambiente.

Di seguito sono riportati i percorsi predefiniti. Se le directory di installazione sono state personalizzate nell'ambiente in uso, i percorsi reali possono variare.

- Client: `C:\Windows\CCM\logs`
- Server: `C:\Program Files\Microsoft Configuration Manager\Logs`
- Punto di gestione: `C:\SMS_CCM\Logs`
- Console di Configuration Manager: `C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\AdminUILog`
- IIS: `C:\inetpub\logs\logfiles\w3svc1`

### <a name="task-sequence-log-locations"></a>Percorsi del log della sequenza di attività

Il percorso del file di log della sequenza di attività **smsts.log** varia a seconda della fase della sequenza di attività:

- In Windows PE si trova prima del passaggio [Formato e disco partizione](../../../osd/understand/task-sequence-steps.md#BKMK_FormatandPartitionDisk): `X:\Windows\temp\smstslog\smsts.log` (X è l'unità RAM Windows PE)
- In Windows PE si trova dopo il passaggio **Formato e disco partizione**: `X:\smstslog\smsts.log`, quindi copiato in `C:\_SMSTaskSequence\Logs\smstslog\smsts.log` quando l'unità è pronta
- Nel nuovo sistema operativo si trova Windows prima dell'installazione del client: `C:\_SMSTaskSequence\Logs\smstslog\smsts.log`
- In Windows si trova dopo l'installazione del client: `C:\Windows\CCM\Logs\smstslog\smsts.log`
- In Windows si trova al termine della sequenza di attività: `C:\Windows\CCM\Logs\smsts.log`

> [!Tip]  
> La variabile di sola lettura della sequenza di attività [_SMSTSLogPath](../../../osd/understand/task-sequence-variables.md#SMSTSLogPath) contiene sempre il percorso del file di log corrente.


## <a name="see-also"></a>Vedere anche

- [Riferimento per i file di log](log-files.md)

- [Supporto tecnico OneTrace](../../support/support-center-onetrace.md)

- [Visualizzatore file di log del Supporto tecnico](../../support/support-center.md#support-center-log-file-viewer)

- [CMTrace](../../support/cmtrace.md)
