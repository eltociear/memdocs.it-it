---
title: Programma di installazione di hotfix
titleSuffix: Configuration Manager
description: Informazioni su quando e come installare gli aggiornamenti usando il programma di installazione degli hotfix per Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f3058277-c597-4dac-86d1-41b6f7e62b36
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a8eed671b723091f2a43350f42ca82d90e0d9da3
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906142"
---
# <a name="use-the-hotfix-installer-to-install-updates-for-configuration-manager"></a>Usare il programma di installazione di hotfix per installare gli aggiornamenti per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Alcuni aggiornamenti per Configuration Manager non sono disponibili dal servizio cloud Microsoft e possono essere ottenuti solo come rilascio fuori programma. Questo si verifica, ad esempio, nel caso di un hotfix a rilascio limitato per la soluzione di un problema specifico.   
Quando è necessario installare un aggiornamento (o hotfix) ricevuto da Microsoft e tale aggiornamento ha un nome file che termina con l'estensione **.exe** (non **update.exe**), usare il programma di installazione di hotfix incluso con il download dell'hotfix per installare l'aggiornamento direttamente nel server del sito di Configuration Manager.  

Se il file dell'hotfix ha estensione **update.exe**, vedere [Usare lo strumento di registrazione dell'aggiornamento per importare hotfix in Configuration Manager](../../../core/servers/manage/use-the-update-registration-tool-to-import-hotfixes.md).  

> [!NOTE]  
> Questo argomento fornisce indicazioni generali su come installare gli hotfix che aggiornano Configuration Manager. Per informazioni dettagliate su uno specifico aggiornamento, consultare l'articolo corrispondente della Knowledge Base (KB) nel Supporto tecnico Microsoft.  

##  <a name="overview-of-hotfixes-for-configuration-manager"></a><a name="bkmk_Overview"></a> Panoramica degli hotfix per Configuration Manager  
Gli hotfix per Configuration Manager sono simili a quelli per altri prodotti Microsoft, ad esempio SQL Server, contengono una singola correzione o un bundle (un rollup di correzioni) e sono descritti in un articolo della Microsoft Knowledge Base.  

Gli aggiornamenti singoli includono un solo aggiornamento mirato per una versione specifica di Configuration Manager.  
I bundle di aggiornamenti comprendono più aggiornamenti per una versione specifica di Configuration Manager.  
Quando un aggiornamento è in bundle, non è possibile installare singoli aggiornamenti da tale bundle.  

Se si pianifica di creare distribuzioni per installare gli aggiornamenti in computer aggiuntivi, è necessario installare il bundle di aggiornamenti in un server del sito di amministrazione centrale o del sito primario.  

Quando si esegue il bundle di aggiornamenti, si verifica quanto segue:  

- I file di aggiornamento per ciascun componente applicabile vengono estratti dal bundle di aggiornamenti.  

- Avvia una procedura guidata che descrive il processo per la configurazione degli aggiornamenti e delle opzioni di distribuzione degli aggiornamenti.  

- Quando si completa la procedura guidata, nel server del sito vengono installati gli aggiornamenti presenti nel bundle che si applicano al server del sito.  

La procedura guidata crea anche distribuzioni che è possibile usare per installare gli aggiornamenti in computer aggiuntivi. Gli aggiornamenti vengono distribuiti agli altri computer utilizzando un metodo di distribuzione supportato, ad esempio un pacchetto di distribuzione software o Microsoft System Center Updates Publisher 2011.  

Quando viene eseguita la procedura guidata, viene creato un file con estensione **.cab** nel server del sito da usare con Updates Publisher 2011. Facoltativamente, è possibile configurare la procedura guidata in modo da creare anche uno o più pacchetti di distribuzione software. È possibile usare queste distribuzioni per installare aggiornamenti sui componenti, come i client o la console di Configuration Manager. È anche possibile installare manualmente gli aggiornamenti nei computer in cui non è in esecuzione il client di Configuration Manager.  

I tre gruppi seguenti in Configuration Manager possono essere aggiornati:  

- Ruoli del server di Configuration Manager, tra cui:  

  - Sito di amministrazione centrale  

  - Sito primario  

  - Sito secondario  

  - Provider SMS remoto  

- Console di Configuration Manager  

- Client di Configuration Manager  

> [!NOTE]  
> Gli **aggiornamenti per i ruoli del sistema del sito**, inclusi gli aggiornamenti per il database del sito e i punti di distribuzione basati sul cloud, vengono installati come parte dell'aggiornamento per i servizi e i server del sito da Gestione componenti del sito.  
>   
> I punti di distribuzione pull degli aggiornamenti sono tuttavia gestiti da Distribution Manager e non da Gestione componenti del sito.  

Ogni bundle di aggiornamenti per Configuration Manager è un file EXE autoestraente (SFX) che contiene i file necessari per installare l'aggiornamento nei componenti applicabili di Configuration Manager. In genere, il file SFX può contenere i file seguenti:  

|File|Dettagli|  
|----------|-------------|  
|&lt;Versione prodotto\>-QFE-KB&lt;ID articolo KB\>-&lt;piattaforma\>-&lt;lingua\>.exe|Questo è il file di aggiornamento. La riga di comando per questo file è gestita da Updatesetup.exe.<br /><br /> Ad esempio:<br />CM1511RTM-QFE-KB123456-X64-ENU.exe|  
|Updatesetup.exe|Questo wrapper .msi gestisce l'installazione del bundle di aggiornamenti.<br /><br /> Quando si esegue l'aggiornamento, Updatesetup.exe rileva la lingua di visualizzazione del computer in cui viene eseguito. Per impostazione predefinita, l'interfaccia utente per l'aggiornamento è in inglese. Quando la lingua di visualizzazione è supportata, l'interfaccia utente viene visualizzato nella lingua locale del computer.|  
|License_&lt;lingua\>.rtf|Ove applicabile, ogni aggiornamento contiene uno o più file di licenza per le lingue supportate.|  
|&lt;TipoProdotto&Aggiornamento>-&lt;versione prodotto\>-&lt;ID articolo KB\>-&lt;piattaforma\>.msp|Quando l'aggiornamento si applica alla console o ai client di Configuration Manager, il bundle di aggiornamento include file (.msp) separati della patch di Windows Installer.<br /><br /> Ad esempio:<br /><br /> **Aggiornamento della console di Configuration Manager:** ConfigMgr1511-AdminUI-KB1234567-i386.msp<br /><br /> **Aggiornamento client:** ConfigMgr1511-client-KB1234567-i386.msp<br />ConfigMgr1511-client-KB1234567-x64.msp|  

Per impostazione predefinita, il bundle di aggiornamento registra le azioni in un file .log sul server del sito. Il file di log ha lo stesso nome del bundle di aggiornamento e viene scritto nella cartella **%SystemRoot%/Temp** .  

Quando si esegue il pacchetto di aggiornamento, viene estratto un file con lo stesso nome del pacchetto di aggiornamento in una cartella temporanea sul computer, quindi viene eseguito Updatesetup.exe. Updatesetup.exe avvia la procedura guidata di aggiornamento software per Configuration Manager &lt;versione prodotto\>&lt;numero KB\>.  

In base a quanto applicabile per l'ambito dell'aggiornamento, la procedura guidata crea una serie di cartelle nella cartella di installazione di Configuration Manager nel server del sito. La struttura di cartelle è simile alla seguente:   
**\\\\&lt;Nome del server\>\SMS_&lt;Codice sito\>\HotFix\\&lt;Numero KB\>\\&lt;Tipo di aggiornamento\>\\&lt;Piattaforma\>** .  

La tabella seguente fornisce informazioni dettagliate sulle cartelle nella struttura di cartelle:  

|Nome cartella|Altre informazioni|  
|-----------------|----------------------|  
|&lt;Nome del server\>|Questo è il nome del server del sito in cui si esegue il bundle di aggiornamento.|  
|SMS_&lt;Codice sito\>|Questo è il nome della condivisione della cartella di installazione di Configuration Manager.|  
|&lt;Numero KB\>|Questo è il numero ID dell'articolo della Knowledge Base per questo bundle di aggiornamento.|  
|&lt;Tipo di aggiornamento\>|Questi sono i tipi di aggiornamenti per Configuration Manager. La procedura guidata crea una cartella separata per ogni tipo di aggiornamento incluso nel bundle di aggiornamento. I nomi delle cartelle rappresentano i tipi di aggiornamento. Essi includono quanto segue:<br /><br /> **Server**: include gli aggiornamenti ai server del sito, ai server del database del sito e ai computer che eseguono il provider SMS.<br /><br /> **Client**: include gli aggiornamenti del client di Configuration Manager.<br /><br /> **AdminConsole**: include gli aggiornamenti della console di Configuration Manager<br /><br /> Oltre ai tipi di aggiornamento precedenti, la procedura guidata crea una cartella denominata **SCUP**. Questa cartella non rappresenta un tipo di aggiornamento, ma contiene invece il file CAB per Updates Publisher.|  
|&lt;Platform\>|Si tratta di una cartella specifica della piattaforma. Contiene i file di aggiornamento specifici di un tipo di processore.  Queste cartelle includono:<br /><br />- x64<br /><br /> - I386|  

##  <a name="how-to-install-updates"></a><a name="bkmk_Install"></a> Come installare gli aggiornamenti  
Per installare gli aggiornamenti, è prima necessario installare il bundle di aggiornamento in un server del sito. Quando si installa un bundle di aggiornamenti, viene avviata una procedura guidata di installazione dell'aggiornamento. Questa procedura:  

- Estrae i file di aggiornamento  

- Consente di configurare le distribuzioni  

- Installa gli aggiornamenti applicabili nei componenti del server del computer locale  

Dopo aver installato il bundle di aggiornamento in un server del sito, è possibile aggiornare i componenti aggiuntivi per Configuration Manager. La tabella seguente descrive le azioni di aggiornamento per i vari componenti:  

|Componente|Istruzioni|  
|---------------|------------------|  
|Server del sito|Distribuire gli aggiornamenti in un server del sito remoto quando si sceglie di non installare il bundle di aggiornamenti direttamente sul tale server del sito remoto.|  
|Database del sito|Per i server del sito remoti, distribuire gli aggiornamenti del server che includono un aggiornamento al database del sito se non si installa il bundle di aggiornamento su tale server del sito remoto.|  
|Console di Configuration Manager|Dopo l'installazione iniziale della console di Configuration Manager, è possibile installare aggiornamenti per la console di Configuration Manager in ogni computer in cui è in esecuzione la console. Non è possibile modificare il file di installazione della console di Configuration Manager per applicare gli aggiornamenti durante l'installazione iniziale della console.|  
|Provider SMS remoto|Installare gli aggiornamenti per ciascuna istanza del provider SMS che viene eseguita su un computer diverso dal server del sito dove è stato installato il bundle di aggiornamento.|  
|Client di Configuration Manager|Dopo l'installazione iniziale del client di Configuration Manager, è possibile installare aggiornamenti per il client di Configuration Manager in ogni computer in cui è in esecuzione il client.|  

> [!NOTE]  
> È possibile distribuire aggiornamenti solo ai computer in cui è in esecuzione il client di Configuration Manager.  

Se si reinstalla un client, la console di Configuration Manager o il provider SMS, è necessario reinstallare anche gli aggiornamenti per questi componenti.  

Usare le informazioni delle sezioni che seguono per installare gli aggiornamenti in ognuno dei componenti per Configuration Manager.  

###  <a name="update-servers"></a><a name="bkmk_servers"></a> Aggiornare i server  
Gli aggiornamenti per server possono includere gli aggiornamenti per i **siti**, per il **site database**e per i computer che eseguono un'istanza del **provider SMS**:  

####  <a name="update-a-site"></a><a name="bkmk_site"></a> Aggiornare un sito  
Per aggiornare un sito di Configuration Manager, è possibile installare il bundle di aggiornamento direttamente in un server del sito oppure distribuire gli aggiornamenti in un server del sito dopo aver installato il bundle di aggiornamento in un sito diverso.  

Quando si installa un aggiornamento su un server del sito, il processo di installazione dell'aggiornamento gestisce azioni aggiuntive richieste per applicare l'aggiornamento, come ad esempio i ruoli del sistema del sito che stanno effettuando l'aggiornamento. L'eccezione è il database del sito. La sezione seguente contiene informazioni su come aggiornare il database del sito.  

####  <a name="update-a-site-database"></a><a name="bkmk_database"></a> Aggiornare un database del sito  
Per aggiornare il database del sito, il processo di installazione esegue un file denominato **update.sql** sul database del sito. È possibile configurare il processo di aggiornamento per aggiornare automaticamente il database del sito oppure aggiornare manualmente il database del sito in un secondo momento.  

**Aggiornamento automatico del database del sito**  

Quando si installa il bundle di aggiornamento su un server del sito, è possibile scegliere di aggiornare automaticamente il database del sito quando viene installato l'aggiornamento del server. Tale decisione si applica solo al server del sito in cui si installa il bundle di aggiornamenti e non si applica alle distribuzioni create per installare gli aggiornamenti su server del sito remoti.  

> [!NOTE]  
> Quando si sceglie di aggiornare automaticamente il database del sito, il processo aggiorna un database indipendentemente dal fatto che sia posizionato sul server del sito o su un computer remoto.  

> [!IMPORTANT]  
> Prima di aggiornare il database del sito, creare un backup del database del sito. Non è possibile disinstallare un aggiornamento nel database del sito. Per informazioni su come creare un backup per Configuration Manager, vedere [Eseguire il backup e il ripristino per Configuration Manager](backup-and-recovery.md).  

**Aggiornamento manuale del database del sito**  

Se si sceglie di non aggiornare automaticamente il database del sito quando si installa il bundle di aggiornamento sul server del sito, l'aggiornamento del server non modifica il database sul server del sito in cui è in esecuzione il bundle di aggiornamento. Le distribuzioni che usano il pacchetto creato per la distribuzione software o installato, tuttavia, aggiornano sempre il database del sito.  

> [!WARNING]  
> Quando l'aggiornamento include gli aggiornamenti al server del sito e al database del sito, l'aggiornamento non è funzionale finché non è stato completato sia per il server del sito che per il database del sito. Il sito rimane in uno stato non supportato fino a che l'aggiornamento non viene applicato al database del sito.  

**Per aggiornare manualmente un database del sito:**  

1.  Arrestare il servizio SMS_SITE_COMPONENT_MANAGER nel server del sito e quindi arrestare il servizio SMS_EXECUTIVE.  

2.  Chiudere la console di Configuration Manager.  

3.  Eseguire lo script di aggiornamento denominato **update.sql** nel database di tale sito. Per informazioni su come eseguire uno script per aggiornare un database di SQL Server, vedere la documentazione per la versione di SQL Server utilizzata per il server del database del sito.  

4.  Riavviare i servizi arrestati nei passaggi precedenti.  

5.  Quando si installa il bundle di aggiornamento, **update.sql** viene estratto nel seguente percorso sul server del sito:  **\\\\&lt;Nome server\>\SMS_&lt;Codice sito\>\Hotfix\\&lt;Numero KB\>\update.sql**  

####  <a name="update-a-computer-that-runs-the-sms-provider"></a><a name="bkmk_provider"></a> Aggiornare un computer che esegue il provider SMS  
Dopo aver installato un pacchetto di aggiornamento che include aggiornamenti per il provider SMS è necessario distribuire l'aggiornamento in ogni computer che esegue il provider SMS. L'unica eccezione è costituita dall'istanza del provider SMS installata in precedenza nel server del sito in cui si installa il bundle di aggiornamenti. L'istanza locale del provider SMS nel server del sito viene aggiornata quando si installa il bundle di aggiornamenti.  

Se si rimuove e quindi si reinstalla il provider SMS in un computer, sarà necessario reinstallare l'aggiornamento per il provider SMS in tale computer.  

###  <a name="update-clients"></a><a name="BKMK_clients"></a> Aggiornare i client  
Quando si installa un aggiornamento che include aggiornamenti per il client di Configuration Manager è possibile scegliere se aggiornare automaticamente i client con l'installazione dell'aggiornamento oppure aggiornarli manualmente in un secondo momento. Per altre informazioni sull'aggiornamento automatico dei client, vedere [Come aggiornare i client per i computer Windows](../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

È possibile distribuire gli aggiornamenti con Updates Publisher o un pacchetto di distribuzione software oppure è possibile scegliere di installare manualmente l'aggiornamento in ogni client. Per altre informazioni su come usare le distribuzioni per installare gli aggiornamenti, vedere la sezione [Distribuire gli aggiornamenti per Configuration Manager](#BKMK_Deploy) in questo argomento.  

> [!IMPORTANT]  
> Quando si installano gli aggiornamenti per i client e il pacchetto di aggiornamento include aggiornamenti per i server, assicurarsi di installare anche gli aggiornamenti server nel sito primario a cui sono assegnati i client.  

Per installare manualmente l'aggiornamento software, è necessario eseguire **Msiexec.exe** e fare riferimento al file con estensione MSP specifico della piattaforma in ogni client di Configuration Manager.  

Ad esempio, è possibile utilizzare la seguente riga di comando per un aggiornamento client. Questa riga di comando esegue MSIEXEC nel computer client e fa riferimento al file MSP estratto dal pacchetto di aggiornamento nel server del sito: **msiexec.exe /p \\\\&lt;NomeServer\>\SMS_&lt;CodiceSito\>\Hotfix\\&lt;Numero KB\>\Client\\&lt;Piattaforma\>\\&lt;msp\> /L\*v &lt;filelog\>REINSTALLMODE=mous REINSTALL=ALL**  

###  <a name="update-configuration-manager-consoles"></a><a name="BKMK_console"></a> Aggiornare le console di Configuration Manager  
Per aggiornare una console di Configuration Manager, al termine dell'installazione della console è necessario installare l'aggiornamento nel computer che esegue la console.  

> [!IMPORTANT]  
> Quando si installano gli aggiornamenti per la console di Configuration Manager e il pacchetto di aggiornamento include aggiornamenti per i server, assicurarsi di installare anche gli aggiornamenti server nel sito che si usa con la console di Configuration Manager.  

Se il computer che si aggiorna esegue il client di Configuration Manager:  

- È possibile usare una distribuzione per installare l'aggiornamento. Per altre informazioni su come usare le distribuzioni per installare gli aggiornamenti, vedere la sezione [Distribuire gli aggiornamenti per Configuration Manager](#BKMK_Deploy) in questo argomento.  

- Se si è connessi direttamente al computer client, è possibile eseguire l'installazione in modo interattivo.  

- È possibile installare manualmente l'aggiornamento in ogni computer. Per installare manualmente l'aggiornamento della console di Configuration Manager, in ogni computer che esegue la console di Configuration Manager è possibile eseguire Msiexec.exe e fare riferimento al file MSP di aggiornamento della console di Configuration Manager.  

Ad esempio, è possibile usare la riga di comando seguente per aggiornare una console di Configuration Manager. Questa riga di comando esegue MSIEXEC nel computer e fa riferimento al file MSP estratto dal pacchetto di aggiornamento nel server del sito: **msiexec.exe /p \\\\&lt;NomeServer\>\SMS_&lt;CodiceSito\>\Hotfix\\&lt;Numero KB\>\AdminConsole\\&lt;Piattaforma\>\\&lt;msp\> /L\*v &lt;filelog\>REINSTALLMODE=mous REINSTALL=ALL**  

##  <a name="deploy-updates-for-configuration-manager"></a><a name="BKMK_Deploy"></a> Distribuire gli aggiornamenti per Configuration Manager  
Dopo aver installato il bundle di aggiornamenti in un server del sito, è possibile distribuire gli aggiornamenti in altri computer usando uno dei tre metodi seguenti.  

###  <a name="use-updates-publisher-2011-to-install-updates"></a><a name="BKMK_DeploySCUP"></a> Usare Updates Publisher 2011 per installare gli aggiornamenti  
Quando si installa il bundle di aggiornamenti in un server del sito, la procedura guidata di installazione crea un file di catalogo per Updates Publisher che è possibile usare per distribuire gli aggiornamenti nei computer applicabili. La procedura guidata crea sempre questo catalogo, anche quando si seleziona l'opzione **Use package and program to deploy this update**.  

Il catalogo per Updates Publisher, **SCUPCatalog.cab**, è disponibile nel percorso seguente del computer in cui viene eseguito il pacchetto di aggiornamento: **\\\\&lt;NomeServer\>\SMS_&lt;CodiceSito\>\Hotfix\\&lt;Numero KB\>\SCUP\SCUPCatalog.cab**  

> [!IMPORTANT]  
> Poiché viene creato utilizzando i percorsi specifici per il server del sito in cui viene installato il pacchetto di aggiornamento, il file SCUPCatalog.cab non può essere utilizzato in altri server del sito.  

Al termine della procedura guidata è possibile importare il catalogo in Updates Publisher e usare gli aggiornamenti software di Configuration Manager per distribuire gli aggiornamenti. Per altre informazioni su Updates Publisher, vedere [Updates Publisher 2011](https://docs.microsoft.com/previous-versions/system-center/updates-publisher-2011/hh134742(v=technet.10)).  

Usare la procedura seguente per importare il file SCUPCatalog.cab in Updates Publisher e pubblicare gli aggiornamenti.  

##### <a name="to-import-the-updates-to-updates-publisher-2011"></a>Per importare gli aggiornamenti in Updates Publisher 2011  

1.  Avviare la console di Updates Publisher e fare clic su **Import**.  

2.  Nella pagina **Import Type** della procedura guidata Import Software Updates Catalog Wizard selezionare **Specify the path to the catalog to import**, quindi specificare il file SCUPCatalog.cab.  

3.  Fare clic su **Next**, quindi fare clic di nuovo su **Next** .  

4.  Nella finestra di dialogo **Security Warning - Catalog Validation** fare clic su **Accept**. Al termine, chiudere la procedura guidata.  

5.  Nella console di Updates Publisher selezionare l'aggiornamento da distribuire e quindi fare clic su **Publish**.  

6.  Nella pagina **Publish Options** della procedura guidata Publish Software Updates Wizard selezionare **Full Content**e quindi fare clic su **Next**.  

7.  Completare la procedura guidata per pubblicare gli aggiornamenti.  

###  <a name="use-software-deployment-to-install-updates"></a><a name="BKMK_DeploySWDist"></a> Usare la distribuzione software per installare gli aggiornamenti  
Quando si installa il bundle di aggiornamenti nel server del sito di un sito primario o di un sito di amministrazione centrale, è possibile configurare la procedura guidata di installazione per creare pacchetti di aggiornamento per la distribuzione software. È quindi possibile distribuire ogni pacchetto in una raccolta di computer che si desidera aggiornare.  

Per creare un pacchetto di distribuzione software, nella pagina **Configure Software Update Deployment** della procedura guidata selezionare la casella di controllo relativa a ogni tipo di pacchetto di aggiornamento che si desidera aggiornare. I tipi disponibili possono includere server, console di Configuration Manager e client. Viene creato un pacchetto separato per ogni tipo di aggiornamento selezionato.  

> [!NOTE]  
> Il pacchetto per i server contiene aggiornamenti per i seguenti componenti:  
>   
> - Server del sito  
> - Provider SMS  
> - Database del sito  

Quindi, nella pagina **Configure Software Update Deployment Method** della procedura guidata selezionare l'opzione **I will use software distribution**. Questa selezione imposta la procedura guidata in modo da creare i pacchetti di distribuzione software.  

Al termine della procedura guidata, è possibile visualizzare i pacchetti creati nella console di Configuration Manager nel nodo **Pacchetti** nell'area di lavoro **Raccolta software**. È quindi possibile usare il processo standard per distribuire i pacchetti software nei client di Configuration Manager. Quando viene eseguito un pacchetto in un client, gli aggiornamenti dei componenti applicabili di Configuration Manager vengono installati nel computer client.  

Per informazioni su come distribuire i pacchetti ai client di Configuration Manager, vedere [Pacchetti e programmi](../../../apps/deploy-use/packages-and-programs.md).  

###  <a name="create-collections-for-deploying-updates-to-configuration-manager"></a><a name="BKMK_DeployCollections"></a> Creare raccolte per la distribuzione degli aggiornamenti in Configuration Manager  
È possibile distribuire aggiornamenti specifici nei client applicabili. Le informazioni seguenti consentono di creare raccolte di dispositivi per i vari componenti per Configuration Manager.  

|Componente di Configuration Manager|Istruzioni|  
|----------------------------------------|------------------|  
|Server del sito di amministrazione centrale|Creare una query di appartenenza diretta e aggiungere il computer del server del sito di amministrazione centrale.|  
|Tutti i server del sito primario|Creare una query di appartenenza diretta e aggiungere ogni computer del server del sito primario.|  
|Tutti i server del sito secondario|Creare una query di appartenenza diretta e aggiungere ogni computer del server del sito secondario.|  
|Tutti i client x86|Creare una raccolta con i seguenti criteri di query:<br /><br /> **Select \* from SMS_R_System inner join SMS_G_System_SYSTEM on SMS_G_System_SYSTEM.ResourceID = SMS_R_System.ResourceId where SMS_G_System_SYSTEM.SystemType = "X86-based PC"**|  
|Tutti i client x64|Creare una raccolta con i seguenti criteri di query:<br /><br /> **Select \* from SMS_R_System inner join SMS_G_System_SYSTEM on SMS_G_System_SYSTEM.ResourceID = SMS_R_System.ResourceId where SMS_G_System_SYSTEM.SystemType = "X64-based PC"**|  
|Tutti i computer che eseguono la console di Configuration Manager|Creare una query di appartenenza diretta e aggiungere ogni computer.|  
|Computer remoti che eseguono un'istanza del provider SMS|Creare una query di appartenenza diretta e aggiungere ogni computer.|  

> [!NOTE]  
> Per aggiornare un database del sito, è necessario distribuire l'aggiornamento nel server del sito per tale sito.  

Per informazioni su come creare le raccolte, vedere [Come creare raccolte](../../../core/clients/manage/collections/create-collections.md).  
