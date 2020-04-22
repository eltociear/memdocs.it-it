---
title: Strumento di connessione del servizio
titleSuffix: Configuration Manager
description: Lo strumento consente di connettersi al servizio cloud di Configuration Manager per caricare manualmente le informazioni sull'utilizzo.
ms.date: 09/06/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6e4964c5-43cb-4372-9a89-b62ae6a4775c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e535653e0f31e186a6bdbde8da77750f2afdfdb0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690299"
---
# <a name="use-the-service-connection-tool-for-configuration-manager"></a>Usare lo strumento di connessione del servizio per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Usare lo **strumento di connessione del servizio** quando il punto di connessione del servizio è in modalità offline oppure quando i server del sistema del sito di Configuration Manager non sono connessi a Internet. Lo strumento consente di mantenere il sito aggiornato con gli aggiornamenti più recenti di Configuration Manager.  

Quando viene eseguito, lo strumento si connette manualmente al servizio cloud di Configuration Manager per caricare le informazioni di utilizzo per la gerarchia e per scaricare gli aggiornamenti. Il caricamento dei dati di utilizzo è necessario per abilitare il servizio cloud in modo che fornisca gli aggiornamenti corretti per la distribuzione.  

## <a name="prerequisites-for-using-the-service-connection-tool"></a>Prerequisiti per l'uso dello strumento di connessione del servizio
Di seguito sono elencati i prerequisiti e i problemi noti.

**Prerequisiti:**

- È installato un punto di connessione del servizio, impostato su **Offline, connessione su richiesta**.  

- Lo strumento deve essere eseguito da un prompt dei comandi.  

- Ogni computer in cui viene eseguito lo strumento, ossia il computer del punto di connessione del servizio e il computer connesso a Internet, deve avere un sistema a 64 bit (x64) e avere installato quanto segue:  

  - File x86 e x64 di **Visual C++ Redistributable** .   Per impostazione predefinita, Configuration Manager installa la versione x64 nel computer che ospita il punto di connessione del servizio.  

    Per scaricare una copia dei file di Visual C++, visitare [Visual C++ Redistributable Packages per Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=40784) nell'Area download Microsoft.  

  - .NET Framework 4.5.2 o versioni successive.  

- L'account usato per eseguire lo strumento deve avere:
  - Le autorizzazioni di**amministratore locale** nel computer che ospita il punto di connessione del servizio (dove viene eseguito lo strumento).
  - Le autorizzazioni di**lettura** per il database del sito.  



- È necessaria un'unità USB con spazio libero sufficiente per l'archiviazione dei file e degli aggiornamenti oppure un altro metodo di trasferimento dei file tra il computer del punto di connessione del servizio e il computer con accesso a Internet. Questo scenario presuppone che i computer del sito e i computer gestiti non abbiano una connessione diretta a Internet.  



## <a name="use-the-service-connection-tool"></a>Usare lo strumento di connessione del servizio  

 Lo strumento di connessione del servizio (**serviceconnectiontool.exe**) è disponibile nel supporto di installazione di Configuration Manager nella cartella **%path%\smssetup\tools\ServiceConnectionTool**. Usare sempre lo strumento di connessione del servizio che corrisponde alla versione di Configuration Manager in uso.


 In questa procedura gli esempi della riga di comando usano i nomi file e i percorsi di cartelle seguenti (non è necessario usare questi percorsi e nomi file, si possono usare anche alternative più adatte al proprio ambiente e alle proprie preferenze):  

- Percorso a una chiave USB dove vengono archiviati i dati per il trasferimento tra server:  **D:\USB\\**  

- Nome del file CAB che contiene i dati esportati dal sito: **UsageData.cab**  

- Nome della cartella vuota in cui verranno archiviati gli aggiornamenti scaricati per Configuration Manager per il trasferimento tra server: **UpdatePacks**  

Nel computer che ospita il punto di connessione del servizio:  

- Aprire un prompt dei comandi con privilegi amministrativi, quindi passare alla directory nel percorso che contiene **serviceconnectiontool.exe**.  

  Per impostazione predefinita, questo strumento è disponibile nel supporto di installazione di Configuration Manager nella cartella **%path%\smssetup\tools\ServiceConnectionTool**. Per il funzionamento dello strumento di connessione del servizio, tutti i file devono essere nella stessa cartella.  

Quando si esegue il comando seguente, lo strumento prepara un file CAB che contiene informazioni sull'utilizzo e lo copia in una posizione specificata. I dati nel file CAB si basano sul livello dei dati di diagnostica e di utilizzo che il sito è configurato per raccogliere. Vedere [Dati di diagnostica e utilizzo per Configuration Manager](../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md).  Eseguire questo comando per creare il file CAB:  

- **serviceconnectiontool.exe -prepare -usagedatadest D:\USB\UsageData.cab**  

È anche necessario copiare la cartella ServiceConnectionTool con tutto il contenuto nell'unità USB o renderla comunque disponibile nel computer da usare per i passaggi 3 e 4.  

### <a name="overview"></a>Panoramica
#### <a name="there-are-three-primary-steps-to-using-the-service-connection-tool"></a>I passaggi principali per l'uso dello strumento di connessione del servizio sono tre  

1.  **Preparazione**:  questo passaggio viene eseguito nel computer che ospita il punto di connessione del servizio. Quando si esegue lo strumento, i dati di utilizzo vengono inseriti in un file CAB e archiviati in un'unità USB o in una posizione di trasferimento alternativa specificata.  

2.  **Connessione**: per questo passaggio lo strumento viene eseguito in un computer remoto che si connette a Internet in modo da poter caricare i dati di utilizzo e poi scaricare gli aggiornamenti.  

3.  **Importazione**: questo passaggio viene eseguito nel computer che ospita il punto di connessione del servizio. Quando si esegue lo strumento, gli aggiornamenti scaricati vengono importati e aggiunti al sito in modo da poter visualizzare e quindi installare gli aggiornamenti dalla console di Configuration Manager.  

A partire dalla versione 1606, mentre si è connessi a Microsoft è possibile caricare più file con estensione cab contemporaneamente, ognuno da una gerarchia diversa, e specificare un server proxy e un utente per il server proxy.   

#### <a name="to-upload-multiple-cab-files"></a>Per caricare più file con estensione cab
- Inserire i singoli file con estensione cab da esportare da gerarchie diverse nella stessa cartella. Il nome di ogni file deve essere univoco ed è possibile rinominarli manualmente se necessario.
- Quando si esegue il comando per caricare i dati in Microsoft, specificare la cartella che contiene i file con estensione cab. (Prima dell'aggiornamento 1606, era possibile caricare i dati da una sola gerarchia alla volta e lo strumento richiedeva di specificare il nome del file con estensione cab nella cartella).
- Quando in seguito si esegue l'attività di importazione nel punto di connessione del servizio di una gerarchia, lo strumento importerà automaticamente solo i dati della gerarchia specifica.  

#### <a name="to-specify-a-proxy-server"></a>Per specificare un server proxy
È possibile usare i parametri facoltativi seguenti per specificare un server proxy (ulteriori informazioni sull'uso di questi parametri sono disponibili nella sezione Opzioni della riga di comando in questo argomento):
- **-proxyserveruri [FQDN_of_proxy_server]**  Usare questo parametro per specificare il server proxy da usare per la connessione.
- **-proxyusername [username]**  Usare questo parametro quando è necessario specificare un utente per il server proxy.

#### <a name="specify-the-type-of-updates-to-download"></a>Specificare il tipo di aggiornamenti da scaricare
A partire dalla versione 1706, è stato modificato il comportamento di download di strumenti predefinito e lo strumento supporta le opzioni per controllare i file da scaricare.
- Per impostazione predefinita, lo strumento consente di scaricare solo l'aggiornamento più recente disponibile adeguato alla versione del sito. Non scarica gli aggiornamenti rapidi.

Per modificare questo comportamento, utilizzare uno dei parametri seguenti per impostare i file che vengono scaricati. 

> [!NOTE]
> La versione del sito è determinata dai dati nel file CAB che viene caricata quando viene eseguito lo strumento.
>
> È possibile verificare la versione cercando il file *SiteVersion*.txt all'interno del file CAB.

- **-downloadall** Questa opzione consente di scaricare tutti gli elementi, inclusi aggiornamenti e aggiornamenti rapidi, indipendentemente dalla versione del sito.
- **-downloadhotfix** Questa opzione consente di scaricare tutti gli aggiornamenti rapidi indipendentemente dalla versione del sito.
- **-downloadsiteversion** Questa opzione consente di scaricare aggiornamenti e aggiornamenti rapidi con una versione più recente rispetto alla versione del sito.

Riga di comando di esempio che utilizza *- downloadsiteversion*:
- **serviceconnectiontool.exe -connect  *-downloadsiteversion* -usagedatasrc D:\USB -updatepackdest D:\USB\UpdatePacks**




### <a name="to-use-the-service-connection-tool"></a>Per usare lo strumento di connessione del servizio  

1. Nel computer che ospita il punto di connessione del servizio:  

   - Aprire un prompt dei comandi con privilegi amministrativi, quindi passare alla directory nel percorso che contiene **serviceconnectiontool.exe**.   

2. Eseguire il comando seguente per fare in modo che lo strumento prepari un file con estensione cab contenente informazioni sull'utilizzo e lo copi nel percorso specificato:  

   - **serviceconnectiontool.exe -prepare -usagedatadest D:\USB\UsageData.cab**  

   Se si caricano file con estensione cab da più gerarchie contemporaneamente, è necessario che ogni file nella cartella abbia un nome univoco. È possibile rinominare manualmente i file aggiunti nella cartella.

   Per visualizzare le informazioni sull'utilizzo raccolte per essere caricate nel servizio cloud di Configuration Manager, eseguire il comando seguente per esportare gli stessi dati come file con estensione csv che può essere visualizzato usando un'applicazione come Excel:  

   - **serviceconnectiontool.exe -export -dest D:\USB\UsageData.csv**  

3. Una volta completata la procedura di preparazione, spostare l'unità USB (o trasferire i dati esportati con un altro metodo) in un computer con l'accesso a Internet.  

4. Nel computer con l'accesso a Internet aprire un prompt dei comandi con privilegi amministrativi, quindi passare alla directory nel percorso che contiene una copia dello strumento  **serviceconnectiontool.exe** e gli altri file provenienti dalla cartella specificata.  

5. Eseguire questo comando per avviare il caricamento delle informazioni di utilizzo e il download degli aggiornamenti per Configuration Manager:  

   - **serviceconnectiontool.exe -connect -usagedatasrc D:\USB -updatepackdest D:\USB\UpdatePacks**

   Per altri esempi di questa riga di comando, vedere la sezione [Opzioni della riga di comando](../../../core/servers/manage/use-the-service-connection-tool.md#bkmk_cmd) più avanti in questo argomento.

   > [!NOTE]  
   >  Quando si esegue la riga di comando per connettersi al servizio cloud di Configuration Manager, potrebbe verificarsi un errore simile al seguente:  
   >   
   > - Eccezione non gestita: System.UnauthorizedAccessException:  
   >   
   >      L'accesso al percorso 'C:\  
   >     Users\br\AppData\Local\Temp\extractmanifestcab\95F8A562.sql' è negato.  
   >   
   > Questo errore può essere ignorato senza conseguenze ed è possibile chiudere la finestra di errore e continuare.  

6. Dopo aver scaricato gli aggiornamenti per Configuration Manager, spostare l'unità USB (o trasferire i dati esportati con un altro metodo) nel computer che ospita il punto di connessione del servizio.  

7. Nel computer che ospita il punto di connessione del servizio aprire un prompt dei comandi con privilegi amministrativi, passare alla directory nel percorso che contiene **serviceconnectiontool.exe**, quindi eseguire il comando seguente:  

   - **serviceconnectiontool.exe -import -updatepacksrc D:\USB\UpdatePacks**  

8. Al termine dell'importazione, è possibile chiudere il prompt dei comandi. Vengono importati solo gli aggiornamenti per la gerarchia applicabile.  

9. Aprire la console di Configuration Manager e passare ad **Amministrazione** > **Aggiornamenti e manutenzione**. Gli aggiornamenti importati sono ora pronti per l'installazione. Nelle versioni precedenti la 1702, Aggiornamenti e manutenzione si trova in **Amministrazione** > **Servizi cloud**.

   Per informazioni sull'installazione degli aggiornamenti, vedere [Installare gli aggiornamenti nella console per Configuration Manager](../../../core/servers/manage/install-in-console-updates.md).  

## <a name="log-files"></a><a name="bkmk_cmd"></a> File di log

**ServiceConnectionTool.log**

Ogni volta che si esegue lo strumento di connessione del servizio, verrà generato un file di log denominato **ServiceConnectionTool.log** nello stesso percorso dello strumento.  Questo file di log fornirà semplici dettagli sull'esecuzione dello strumento in base ai comandi usati.  Un file di log esistente verrà sostituito ogni volta che si esegue lo strumento.

**ConfigMgrSetup.log**

Quando si usa lo strumento per la connessione e il download degli aggiornamenti, verrà generato un file di log nella radice dell'unità di sistema denominato **ConfigMgrSetup.log**.  Questo file di log fornirà informazioni più dettagliate, ad esempio quali file vengono scaricati, estratti e se i controlli dell'hash hanno esito positivo.

## <a name="command-line-options"></a><a name="bkmk_cmd"></a> Opzioni della riga di comando  
Per visualizzare le informazioni della Guida per lo strumento del punto di connessione del servizio, aprire il prompt dei comandi nella cartella che contiene lo strumento ed eseguire il comando:  **serviceconnectiontool.exe**.  


|Opzioni della riga di comando|Dettagli|  
|---------------------------|-------------|  
|**-prepare -usagedatadest [unità:][percorso][nomefile.cab]**|Questo comando archivia i dati di utilizzo correnti in un file CAB.<br /><br /> Eseguire questo comando come **amministratore locale** nel server che ospita il punto di connessione del servizio.<br /><br /> Esempio:   **-prepare -usagedatadest D:\USB\Usagedata.cab**|    
|**-connect -usagedatasrc [unità:][percorso] -updatepackdest [unità:][percorso] -proxyserveruri [nome FQDN del server proxy] -proxyusername [nome utente]** <br /> <br /> Se si usa una versione di Configuration Manager precedente alla 1606, è necessario specificare il nome del file con estensione cab e non è possibile usare le opzioni per un server proxy.  I parametri di comando supportati sono: <br /> **-connect -usagedatasrc [unità:][percorso][nome file] -updatepackdest [unità:][percorso]** |Questo comando si connette al servizio cloud di Configuration Manager per caricare i file con estensione cab dei dati di utilizzo dal percorso specificato e per scaricare i pacchetti di aggiornamento disponibili e il contenuto della console. Le opzioni per i server proxy sono facoltative.<br /><br /> Eseguire questo comando come **amministratore locale** in un computer con connessione a Internet.<br /><br /> Esempio per la connessione senza server proxy: **-connect -usagedatasrc D:\USB\ -updatepackdest D:\USB\UpdatePacks** <br /><br /> Esempio per la connessione con server proxy: **-connect -usagedatasrc D:\USB\Usagedata.cab -updatepackdest D:\USB\UpdatePacks -proxyserveruri itgproxy.redmond.corp.microsoft.com -proxyusername Meg** <br /><br /> Se si usa una versione precedente alla 1606, è necessario specificare un nome per il file con estensione cab e non è possibile specificare un server proxy. Usare la riga di comando di esempio seguente: **-connect -usagedatasrc D:\USB\Usagedata.cab -updatepackdest D:\USB\UpdatePacks**|      
|**-import -updatepacksrc [unità:][percorso]**|Questo comando importa i pacchetti di aggiornamento e il contenuto della console scaricati in precedenza nella console di Configuration Manager.<br /><br /> Eseguire questo comando come **amministratore locale** nel server che ospita il punto di connessione del servizio.<br /><br /> Esempio:  **-import -updatepacksrc D:\USB\UpdatePacks**|  
|**-export -dest [unità:][percorso][nomefile.csv]**|Questo comando esporta i dati di utilizzo in un file CSV che può essere visualizzato successivamente.<br /><br /> Eseguire questo comando come **amministratore locale** nel server che ospita il punto di connessione del servizio.<br /><br /> Esempio: **-export -dest D:\USB\usagedata.csv**|  
