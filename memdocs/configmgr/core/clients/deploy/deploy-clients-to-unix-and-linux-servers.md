---
title: Distribuire client UNIX/Linux
titleSuffix: Configuration Manager
description: Di seguito viene descritto come distribuire i client in un server UNIX o Linux in Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 15a4e323-9f42-4fea-bb14-f2b905d1f77c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4375867e70cb7f2989b78572c7fc8e005f95be73
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694039"
---
# <a name="how-to-deploy-clients-to-unix-and-linux-servers-in-configuration-manager"></a>Come distribuire i client in server UNIX e Linux in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

> [!Important]  
> A partire dalla versione 1902, Configuration Manager non supporta i client Linux o UNIX. 
> 
> Per la gestione dei server Linux, è possibile usare la gestione di Microsoft Azure. Le soluzioni di Azure includono un ampio supporto per Linux che nella maggior parte dei casi supera le funzionalità di Configuration Manager, inclusa la gestione end-to-end delle patch per Linux.


Prima di poter gestire un server Linux o UNIX con Configuration Manager, è necessario installare il client di Configuration Manager per Linux e UNIX in ogni server Linux o UNIX. L'installazione del client può essere eseguita manualmente in ogni computer o con uno script della shell che installa il client in modalità remota. Configuration Manager non supporta l'uso dell'installazione push client per i server Linux o UNIX. Facoltativamente è possibile configurare un Runbook per System Center Orchestrator per automatizzare l'installazione del client nel server Linux o UNIX.  

 Indipendentemente dal metodo di installazione usato, la gestione del processo di installazione richiede uno script denominato **install** . Questo script viene incluso quando si scarica il Client per Linux e UNIX.  

 Lo script di installazione per il client di Configuration Manager per Linux e UNIX supporta le proprietà della riga di comando. Alcune proprietà della riga di comando sono obbligatorie, mentre altre sono facoltative. Ad esempio, quando si installa il client, è necessario specificare un punto di gestione dal sito utilizzato dal server Linux o UNIX per il contatto iniziale con il sito. Per l'elenco completo delle proprietà della riga di comando, vedere [Proprietà della riga di comando per l'installazione del client nei server Linux e UNIX](#BKMK_CmdLineInstallLnUClient).  

 Dopo aver installato il client, specificare le impostazioni client nella console di Configuration Manager per configurare l'agente client in modo analogo ai client basati su Windows. Per altre informazioni, vedere  [Impostazioni client per server Linux e UNIX](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ClientSettingsforLnU).  

##  <a name="about-client-installation-packages-and-the-universal-agent"></a><a name="BKMK_AboutInstallPackages"></a> Informazioni sui pacchetti di installazione client e sull'agente universale  
 Per installare il client per Linux e UNIX in una piattaforma specifica, è necessario usare il pacchetto di installazione client applicabile al computer in cui si installa il client. I pacchetti di installazione client applicabili sono inclusi in ogni download del client eseguito dall' [Area download Microsoft](https://go.microsoft.com/fwlink/?LinkID=525184). Oltre ai pacchetti di installazione client, il download del client include lo script di **install** che gestisce l'installazione del client in ogni computer.  

 Quando si installa un client, è possibile usare lo stesso processo e le stesse proprietà della riga di comando indipendentemente dal pacchetto di installazione client usato.  

 Per informazioni su sistemi operativi, piattaforme e pacchetti di installazione client supportati per ogni versione del client di Configuration Manager per Linux e UNIX, vedere [Linux and UNIX servers](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#linux-and-unix-servers) (Server Linux e UNIX).  

##  <a name="install-the-client-on-linux-and-unix-servers"></a><a name="BKMK_InstallLnUClient"></a> Installare il client nei server Linux e UNIX  
 Per installare il client per Linux e UNIX, si esegue uno script in ogni computer Linux o UNIX. Lo script è denominato **install** e supporta le proprietà della riga di comando che modificano il comportamento di installazione e fanno riferimento al pacchetto di installazione client. Il pacchetto di installazione client e script di installazione deve trovarsi sul client. Il pacchetto di installazione client contiene i file del client di Configuration Manager per una specifica piattaforma e sistema operativo Linux o UNIX.
Ogni pacchetto di installazione client contiene tutti i file necessari per completare l'installazione del client e, a differenza dei computer basati su Windows, non scarica file aggiuntivi da un punto di gestione o un altro percorso di origine.  

 Dopo aver installato il client di Configuration Manager per Linux e UNIX, non è necessario riavviare il computer. Non appena viene completata l'installazione del software, il client è operativo. Se si riavvia il computer, il client di Configuration Manager viene riavviato automaticamente.  

 Il client installato viene eseguito con le credenziali radice. Per raccogliere l'inventario hardware ed eseguire le distribuzioni software sono necessarie le credenziali radice.  

 Usare il formato di comando seguente:  

 `./install -mp <computer> -sitecode <sitecode> <property #1> <property #2> <client installation package>`  

-   `install` è il nome del file di script che installa il client per Linux e UNIX. Questo file viene fornito con il software client.  

-   `-mp <computer>` specifica il punto di gestione iniziale usato dal client. Esempio: `smsmp.contoso.com`  

-   `-sitecode <site code>` specifica il codice del sito a cui è assegnato il client. Esempio: `S01`  

-   `<property #1> <property #2>` specifica le proprietà della riga di comando da usare con lo script di installazione.  

    > [!NOTE]  
    >  Per altre informazioni, vedere [Proprietà della riga di comando per l'installazione del client nei server Linux e UNIX](#BKMK_CmdLineInstallLnUClient).  

-   **Pacchetto installazione client** è il nome del pacchetto TAR di installazione client per il sistema operativo del computer, la versione e l'architettura della CPU. Il file. tar installazione del client deve essere specificato per ultimo. Esempio: `ccm-Universal-x64.<build>.tar`  

###  <a name="to-install-the-configuration-manager-client-on-linux-and-unix-servers"></a><a name="BKMK_ToInstallLnUClinent"></a> Per installare il client di Configuration Manager nei server Linux e UNIX  

1.  In un computer Windows [scaricare il file client appropriato per il server Linux o UNIX](https://go.microsoft.com/fwlink/?LinkID=525184) che si vuole gestire.  

2.  Eseguire il file autoestraente EXE nel computer Windows per estrarre lo script di installazione e il file TAR di installazione del client.  

3.  Copiare lo script di **installazione** e il file TAR in una cartella sul server che si vuole gestire.  

4.  Nel server UNIX o Linux eseguire il comando seguente per abilitare l'esecuzione dello script come programma: `chmod +x install`  

    > [!IMPORTANT]  
    >  Per installare il client, è necessario utilizzare le credenziali radice.  

5.  Eseguire quindi il comando seguente per installare il client di Configuration Manager: `./install -mp <hostname> -sitecode <code> ccm-Universal-x64.<build>.tar`  

     Quando si immette questo comando, utilizzare le proprietà della riga di comando aggiuntive che necessarie. Per l'elenco delle proprietà della riga di comando, vedere [Proprietà della riga di comando per l'installazione del client nei server Linux e UNIX](#BKMK_CmdLineInstallLnUClient)  

6.  Dopo l'esecuzione dello script, convalidare l'installazione esaminando il file **/var/opt/microsoft/scxcm.log** . È anche possibile verificare che il client sia installato e in comunicazione con il sito visualizzando i dettagli per il client nel nodo **Dispositivi** dell'area di lavoro **Asset e conformità** della console di Configuration Manager.  

###  <a name="command-line-properties-for-installing-the-client-on-linux-and-unix-servers"></a><a name="BKMK_CmdLineInstallLnUClient"></a> Proprietà della riga di comando per l'installazione del client nei server Linux e UNIX  
 Per modificare il comportamento dello script di installazione sono disponibili le proprietà seguenti:  

> [!NOTE]  
>  Usare la proprietà `-h` per visualizzare l'elenco delle proprietà supportate.  

-   `-mp <server FQDN>`  

     Obbligatorio. Specifica il nome di dominio completo del server del punto di gestione che il client usa come punto di contatto iniziale.  

    > [!IMPORTANT]  
    >  Questa proprietà non specifica il punto di gestione a cui viene assegnato il client dopo l'installazione.  

    > [!NOTE]  
    >  Quando si usa la proprietà `-mp` per specificare un punto di gestione configurato per accettare solo connessioni client HTTPS, è necessario usare anche la proprietà `-UsePKICert`.  

-   `-sitecode <sitecode>`  

     Obbligatorio. Specifica il sito primario di Configuration Manager al quale assegnare il client di Configuration Manager. Esempio: `-sitecode S01`  

-   `-fsp <server_FQDN>`  

     Facoltativo. Specifica nome di dominio completo, i server del punto di stato di fallback che il client utilizza per inviare messaggi di stato. Per altre informazioni, vedere [Stabilire se è necessario un punto di stato di fallback](plan/determine-the-site-system-roles-for-clients.md#fallback-status-point).  

-   `-dir <directory>`  

     Facoltativo. Specifica un percorso alternativo per installare i file del client di Configuration Manager. Per impostazione predefinita, il client viene installato nel percorso seguente: `/opt/microsoft`  

-   `-nostart`  

     Facoltativo. Impedisce l'avvio automatico del servizio client di Configuration Manager, **ccmexec.bin**, al termine dell'installazione del client.  

     Dopo aver installato il client, è necessario avviare manualmente il servizio client.  

     Per impostazione predefinita, il servizio client viene avviata dopo il completamento dell'installazione del client e ogni volta che il computer viene riavviato.  

-   `-clean`  

     Facoltativo. Specifica la rimozione di tutti i file del client e i dati da un client installato in precedenza per Linux e UNIX, prima che inizi la nuova installazione. Questa operazione consente di rimuovere l'archivio certificati e il database del client.  

-   `-keepdb`  

     Facoltativo. Specifica che il database del client locale viene mantenuto e riutilizzato quando si reinstalla un client. Per impostazione predefinita, quando si reinstalla un client viene eliminato il database.  

-   `-UsePKICert <parameter>`  

     Facoltativo. Specifica il percorso e il nome completo per un certificato x. 509 PKI nel formato Public Key Certificate Standard (PKCS #12). Questo certificato viene utilizzato per l'autenticazione client. Se non è stato specificato un certificato durante l'installazione e si vuole aggiungere o modificare un certificato, usare l'utilità **certutil** . Per altre informazioni, vedere [Come gestire i certificati sul client per Linux e UNIX](../manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ManageLinuxCerts).  

     Quando si usa `-UsePKICert`, è necessario specificare anche la password associata al file PKCS#12 tramite il parametro della riga di comando `-certpw`.  

     Se non si usa questa proprietà per specificare un certificato PKI, il client usa un certificato autofirmato e tutte le comunicazioni ai sistemi del sito avvengono tramite HTTP.  

     Se si specifica un certificato non valido nella riga di comando di installazione del client, non vengono restituiti errori La convalida del certificato avviene dopo l'installazione del client. All'avvio del client, i certificati vengono convalidati con il punto di gestione. In caso di errore nella convalida di un certificato, viene visualizzato il messaggio seguente in **scxcm.log**: **Failed validate the certificate for Management Point** (Convalida non riuscita del certificato per il punto di gestione). Il percorso predefinito del file di log è:  **/var/opt/microsoft/scxcm.log**.  

     > [!NOTE]  
     > È necessario specificare questa proprietà quando si installa un client e usare la proprietà `-mp` per specificare un punto di gestione configurato per accettare solo connessioni client HTTPS.  

     Esempio: `-UsePKICert <full path and filename> -certpw <password>`  

-   `-certpw <parameter>`  

     Facoltativo. Specifica la password associata al file PKCS#12 specificato tramite la proprietà `-UsePKICert`.  

     Esempio: `-UsePKICert <full path and filename> -certpw <password>`  

-   `-NoCRLCheck`  

     Facoltativo. Specifica che un client non deve controllare l'elenco di revoche di certificati quando comunica tramite HTTPS usando un certificato PKI. Quando questa opzione non è specificata, il client controlla l'elenco di revoche di certificati prima di stabilire una connessione HTTPS usando i certificati PKI. Per ulteriori informazioni sul controllo CRL client, vedere pianificazione di revoche di certificati PKI.  

     Esempio: `-UsePKICert <full path and filename> -certpw <password> -NoCRLCheck`  

-   `-rootkeypath <file location>`  

     Facoltativo. Specifica il percorso e il nome completo per la chiave radice attendibile di Configuration Manager. La chiave radice attendibile di Configuration Manager offre un meccanismo usato dai client Linux e UNIX per verificare di essere connessi a un sistema del sito che appartiene alla gerarchia corretta.  

     Se non si specifica la chiave radice attendibile nella riga di comando, il client considererà attendibile il primo punto di gestione con cui comunica e recupererà automaticamente la chiave radice attendibile da tale punto di gestione.  

     Per altre informazioni, vedere  [Planning for the Trusted Root Key](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

     Esempio: `-rootkeypath <full path and filename>`  

-   `-httpport <port>`  

     Facoltativo. Specifica la porta configurato nei punti di gestione utilizzato dal client durante la comunicazione ai punti di gestione su HTTP. Se la porta non è specificata, viene usato il valore predefinito 80.  

     Esempio: `-httpport 80`  

-   `-httpsport <port>`  

     Facoltativo. Specifica la porta configurato nei punti di gestione utilizzato dal client durante la comunicazione ai punti di gestione tramite HTTPS. Se la porta non è specificata, viene usato il valore predefinito 443.  

     Esempio: `-UsePKICert <full path and certificate name> -httpsport 443`  

-   `-ignoreSHA256validation`  

     Facoltativo. Specifica che l'installazione del client ignora la convalida di SHA-256. Usare questa opzione quando si installa il client in sistemi operativi che non sono stati rilasciati con una versione di OpenSSL che supporta SHA-256. Per altre informazioni, vedere [Informazioni sui sistemi operativi Linux e UNIX che non supportano SHA-256](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_NoSHA-256).  

-   `-signcertpath <file location>`  

     Facoltativo. Specifica il percorso completo e **. cer** nome file del certificato autofirmato esportato nel server del sito. Se non sono disponibili certificati PKI, il server del sito di Configuration Manager genera automaticamente certificati autofirmati.  

     Questi certificati vengono utilizzati per convalidare che i criteri client scaricati dal punto di gestione sono stati inviati dal sito di destinazione. Se non è stato specificato un certificato autofirmato durante l'installazione o si vuole modificare il certificato, usare l'utilità **certutil** . Per altre informazioni, vedere [Come gestire i certificati sul client per Linux e UNIX](../manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ManageLinuxCerts).  

     Il certificato può essere recuperato dall'archivio certificati **SMS** e ha il nome oggetto **Server del sito** e il nome descrittivo **Certificato di firma del server del sito**.  

     Se questa opzione non viene specificata durante l'installazione, i client Linux e UNIX considerano attendibile il primo punto di gestione con cui comunicano. I client recuperano automaticamente il certificato di firma da tale punto di gestione.  

     Esempio: `-signcertpath <full path and file name>`  

-   `-rootcerts`  

     Facoltativo. Specifica certificati PKI aggiuntivi da importare che non fanno parte di una gerarchia di autorità di certificazione dei punti gestione. Se si specificano più certificati nella riga di comando, dovranno essere delimitati da virgole.  

     Usare questa opzione se si usano certificati client PKI non concatenati a un certificato CA radice considerato attendibile dai punti di gestione dei siti. I punti di gestione rifiuteranno il client se il certificato client non è concatenato a un certificato radice attendibile nell'elenco di autorità di certificazione del sito.  

     Se non si usa questa opzione, il client Linux e UNIX verificherà la gerarchia di trust usando solo il certificato nell'opzione `-UsePKICert`.  

     Esempio: `-rootcerts <full path and file name>,<full path and file name>`  

###  <a name="uninstalling-the-client-from-linux-and-unix-servers"></a><a name="BKMK_UninstallLnUClient"></a> Disinstallazione del client da server Linux e UNIX  
 Per disinstallare il client di Configuration Manager per Linux e UNIX, usare l'utilità di disinstallazione, **uninstall**. Per impostazione predefinita, questo file si trova nel **/rifiutare/microsoft/configmgr/bin/** cartella nel computer client. Questo comando di disinstallazione non supporta alcun parametro della riga di comando e rimuove tutti i file correlati al software client dal server.  

 Per disinstallare il client, utilizzare la seguente riga di comando: **/opt/microsoft/configmgr/bin/uninstall**  

 Non è necessario riavviare il computer dopo la disinstallazione del client di Configuration Manager per Linux e UNIX.  

##  <a name="configure-request-ports-for-the-client-for-linux-and-unix"></a><a name="BKMK_ConfigLnUClientCommuincations"></a> Configurare le porte richieste per il Client per Linux e UNIX  
 Come per i client basati su Windows, anche il client di Configuration Manager per Linux e UNIX usa HTTP e HTTPS per comunicare con i sistemi del sito di Configuration Manager. Le porte che il client di Configuration Manager usa per comunicare vengono definite porte di richiesta.  

 Quando si installa il client di Configuration Manager per Linux e UNIX, è possibile modificare le porte di richiesta predefinite del client specificando le proprietà di installazione **-httpport** e **-httpsport**. Quando non si specificano la proprietà di installazione e un valore personalizzato, il client usa i valori predefiniti. I valori predefiniti sono **80** per il traffico HTTP e **443** per il traffico HTTPS.  

 Dopo aver installato il client, non è possibile modificare la configurazione delle porte di richiesta. Per modificare la configurazione della porta è invece necessario reinstallare il client e specificare la nuova configurazione della porta. Quando si reinstalla il client per modificare i numeri delle porte di richiesta, eseguire il comando **install** in modo analogo all'installazione di un nuovo client, ma usare la proprietà della riga di comando aggiuntiva **-keepdb**. Questa opzione indica che l'installazione deve mantenere i file e il database client, inclusi l'archivio certificati e il GUID del client.  

 Per altre informazioni sui numeri di porta di comunicazione client, vedere [Come configurare porte di comunicazione client](../../../core/clients/deploy/configure-client-communication-ports.md).  

##  <a name="configure-the-client-for-linux-and-unix-to-locate-management-points"></a><a name="BKMK_ConfigClientMP"></a> Configurare il Client per Linux e UNIX individuare i punti di gestione  
 Quando si installa il client di Configuration Manager per Linux e UNIX, è necessario specificare un punto di gestione da usare come punto iniziale del contatto.  

 Il client di Configuration Manager per Linux e UNIX contatta il punto di gestione nel momento in cui viene installato il client. Se il client non riesce a contattare il punto di gestione, il software client continuerà a provare fino a quando non riesce.  

 Per altre informazioni sulle modalità con cui i client individuano i punti di gestione, vedere [Individuazione dei punti di gestione](assign-clients-to-a-site.md#locating-management-points).
