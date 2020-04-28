---
title: Creare applicazioni server Linux e UNIX
titleSuffix: Configuration Manager
description: Questo articolo descrive le considerazioni da tenere presenti quando si creano e distribuiscono applicazioni per i dispositivi Linux e UNIX.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 79cd131a-1a24-4751-87c8-7f275e45d847
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 3f5d0cfb930e6d1b8cf4cd6dfb0eabfa38ddab16
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075779"
---
# <a name="create-linux-and-unix-server-applications-with-configuration-manager"></a>Creare applicazioni server Linux e UNIX con Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

> [!Important]  
> A partire dalla versione 1902, Configuration Manager non supporta i client Linux o UNIX. 
> 
> Per la gestione dei server Linux, è possibile usare la gestione di Microsoft Azure. Le soluzioni di Azure includono un ampio supporto per Linux che nella maggior parte dei casi supera le funzionalità di Configuration Manager, inclusa la gestione end-to-end delle patch per Linux.

Tenere presenti le seguenti considerazioni quando si creano e si distribuiscono applicazioni per computer che eseguono Linux e UNIX.  

## <a name="general-considerations"></a>Considerazioni generali  
 Il client di Configuration Manager per Linux e UNIX supporta le **distribuzioni software che usano pacchetti e programmi**. Non è possibile distribuire le applicazioni di Configuration Manager nei computer che eseguono Linux e UNIX.  

 Ecco alcune delle funzionalità disponibili per le distribuzioni software Linux e UNIX:  

-   Installazione del software per i server Linux e UNIX, include le funzionalità seguenti:  

    -   Nuova distribuzione software  

    -   Aggiornamenti software per i programmi già presenti in un computer  

    -   Patch del sistema operativo  

-   Comandi nativi di Linux e UNIX e script presenti in server Linux e UNIX  

-   Distribuzioni limitate ai sistemi operativi specificati durante la selezione dell'opzione del programma **Solo sulle piattaforme client specificate**

-   Finestre di manutenzione per verificare quando viene installato il software

-   Messaggi di stato della distribuzione per monitorare le distribuzioni  

-   Possibilità per il client di limitare l'uso della rete durante il download del software da un punto di distribuzione  

### <a name="differences-between-deploying-to-linux-and-unix-computers-and-deploying-to-windows-devices"></a>Differenze tra la distribuzione in computer Linux e UNIX e la distribuzione in dispositivi Windows
Di seguito sono illustrate le principali differenze tra la distribuzione di pacchetti e programmi in computer Linux e UNIX e la distribuzione di pacchetti e programmi in dispositivi Windows:  

|Configurazione|Dettagli|  
|-------------------|-------------|  
|Usare solo le configurazioni destinate ai computer. Non usare le configurazioni destinate agli utenti.|Il client di Configuration Manager per Linux e UNIX non supporta le configurazioni destinate agli utenti.|  
|Configurare i programmi per scaricare il software dal punto di distribuzione ed eseguire i programmi dalla cache del client locale.|Il client di Configuration Manager per Linux e UNIX non supporta l'esecuzione di software dal punto di distribuzione. Al contrario, è necessario configurare il software per scaricare il client e quindi eseguire l'installazione.<br /><br /> Per impostazione predefinita, dopo che il client per Linux e UNIX installa il software, tale software viene eliminato dalla cache del client. Tuttavia i pacchetti configurati con l'opzione **Rendi permanente il contenuto nella cache client** non vengono eliminati dal client e rimangono nella cache dopo l'installazione del software.<br /><br /> Il client per Linux e UNIX non supporta le configurazioni per la cache del client e la dimensione massima di tale cache viene limitata solo dallo spazio libero su disco nel computer client.|  
|Configurare l'account di accesso alla rete per l'accesso del punto di distribuzione|I computer Linux e UNIX sono progettati per essere utilizzati come computer del gruppo di lavoro. Per accedere ai pacchetti dal punto di distribuzione nel dominio del server del sito di Configuration Manager, è necessario configurare l'account di accesso alla rete per il sito. È necessario specificare questo account come una proprietà del componente di distribuzione software e configurare l'account prima di distribuire il software.<br /><br /> È possibile configurare più account di accesso alla rete in ogni sito. Il client per Linux e UNIX può utilizzare tutti gli account configurati come account di accesso alla rete.<br /><br /> Per altre informazioni, vedere [Componenti del sito per Configuration Manager](../../core/servers/deploy/configure/site-components.md).|  

 È possibile distribuire pacchetti e programmi nelle raccolte che contengono solo client Linux o UNIX o distribuirli in raccolte che contengono un insieme di tipi di client, ad esempio la **raccolta Tutti i sistemi**. I client non Linux e non UNIX, tuttavia, non installeranno il software o segnaleranno un errore.  

 Quando il client di Configuration Manager per Linux e UNIX riceve ed esegue una distribuzione, genera dei messaggi di stato. È possibile visualizzare i messaggi di stato nella console di Configuration Manager oppure usare i report per monitorare lo stato della distribuzione.  

 Per informazioni su come usare pacchetti e programmi, vedere [Pacchetti e programmi in Configuration Manager](../../apps/deploy-use/packages-and-programs.md).  

##  <a name="configure-packages-programs-and-deployments-for-linux-and-unix-servers"></a>Configurare pacchetti, programmi e distribuzioni per i server Linux e UNIX  
 È possibile creare e distribuire pacchetti e programmi usando le opzioni predefinite disponibili nella console di Configuration Manager. Il client non richiede configurazioni univoche.  

 Usare le informazioni contenute nelle sezioni seguenti per configurare pacchetti, programmi e distribuzioni.  

### <a name="packages-and-programs"></a>Pacchetti e programmi  
 Per creare un pacchetto e un programma per un server Linux o UNIX, usare la **Creazione guidata pacchetto e programma** dalla console di Configuration Manager. Il client per Linux e UNIX supporta la maggior parte delle impostazioni di pacchetti e programmi. Tuttavia, alcune impostazioni non sono supportate. Quando si crea o si configura un pacchetto e un programma, considerare i punti seguenti:  

-   Includere i tipi di file supportati dai computer di destinazione.  

-   Definire le righe di comando appropriate per l'uso nel computer di destinazione.  

-   Tenere presente che le impostazioni che interagiscono con gli utenti non sono supportate.  

Nella seguente tabella vengono elencate le proprietà non supportate per i pacchetti e programmi:  

|Proprietà pacchetto e programma|Comportamento|Altre informazioni|  
|----------------------------------|--------------|----------------------|  
|Impostazioni di condivisione del pacchetto:<br /><br /> - Tutte le opzioni|Viene generato un errore e l'installazione del software non viene completata|Il client non supporta questa configurazione. Il client deve invece scaricare il software utilizzando HTTP o HTTPS e quindi eseguire la riga di comando dalla cache locale.|  
|Impostazioni di aggiornamento del pacchetto:<br /><br /> - Disconnetti gli utenti dai punti di distribuzione|Le impostazioni vengono ignorate|Il client non supporta questa configurazione.|  
|Impostazioni di distribuzione del sistema operativo:<br /><br /> - Tutte le opzioni|Le impostazioni vengono ignorate|Il client non supporta questa configurazione.|  
|Report:<br /><br /> - Usa le proprietà pacchetto per la corrispondenza MIF di stato<br /><br /> - Usa i campi per la corrispondenza MIF di stato|Le impostazioni vengono ignorate|Il client non supporta l'uso di file MIF di stato.|  
|**Esegui**:<br /><br /> - Tutte le opzioni|Le impostazioni vengono ignorate|Il client esegue sempre i pacchetti senza interfaccia utente.<br /><br /> Il client ignora tutte le opzioni di configurazione per Esegui.|  
|Dopo l'esecuzione:<br /><br />- Configuration Manager riavvia il computer<br /><br /> - Riavvio controlli programma<br /><br /> - Configuration Manager disconnette l'utente|Viene generato un errore e l'installazione del software non viene completata|L'impostazione di riavvio del sistema e le impostazioni specifiche dell'utente non sono supportate.<br /><br /> Quando viene utilizzata un'altra impostazione diversa da **Non è necessaria alcuna operazione** , il client genera un errore e continua l'installazione del software, senza eseguire alcuna operazione.|  
|Requisiti per esecuzione programma:<br /><br /> - Solo se un utente è connesso|Viene generato un errore e l'installazione del software non viene completata|Le impostazioni specifiche dell'utente non sono supportate.<br /><br /> Quando questa opzione è configurata, il client genera un errore e l'installazione del software non viene completata.<br /><br /> Altre opzioni vengono ignorate e l'installazione del software continua.|  
|Modalità esecuzione:<br /><br /> - Esegui con diritti dell'utente|Le impostazioni vengono ignorate|Le impostazioni specifiche dell'utente non sono supportate.<br /><br /> Tuttavia, il client supporta la configurazione per l'esecuzione con diritti amministrativi.<br /><br /> Quando si specifica l'opzione **Esegui con diritti amministrativi** il client di Configuration Manager usa le relative credenziali radice.<br /><br /> Questa impostazione non genera una voce di registro o errore. Al contrario, l'installazione del software non viene completata quando il client genera un errore per la configurazione dei prerequisiti di **Requisiti per esecuzione programma** = **Solo se un utente è connesso**.|  
|Consenti agli utenti di visualizzare e interagire con l'installazione del programma|Le impostazioni vengono ignorate|Le impostazioni specifiche dell'utente non sono supportate.<br /><br /> Questa configurazione viene ignorata e l'installazione del software continua.|  
|Modalità unità:<br /><br /> - Tutte le opzioni|Le impostazioni vengono ignorate|Questa impostazione non è supportata perché il contenuto viene sempre scaricato nel client ed eseguito localmente.|  
|Esegui prima un altro programma|Viene generato un errore e l'installazione del software non viene completata|L'installazione del programma ricorsiva non è supportata.<br /><br /> Quando un programma viene configurato per eseguire prima un altro programma, è impossibile completare l'installazione del software e l'installazione dell'altro programma non viene avviata.|  
|Se il programma è assegnato a un computer:<br /><br /> - Esegui una volta per ogni utente che si connette|Le impostazioni vengono ignorate|Le impostazioni specifiche dell'utente non sono supportate.<br /><br /> Tuttavia, il client supporta la configurazione per l'esecuzione unica per il computer.<br /><br /> Questa impostazione non genera una voce di log o un errore perché sono già stati creati per la configurazione dei prerequisiti di **Requisiti per esecuzione programma** = **Solo se un utente è connesso**.|  
|Elimina notifiche programma|Le impostazioni vengono ignorate|Il client non implementa un'interfaccia utente.<br /><br /> Quando questa configurazione viene selezionata, viene ignorata e l'installazione del software continua.|  
|Disattiva il programma nei computer in cui è distribuito|Le impostazioni vengono ignorate|Questa impostazione non è supportata e non influisce sull'installazione del software.|  
|Consenti l'installazione di questo programma dalla sequenza di attività Installa pacchetto senza che venga distribuito||Il client non supporta le sequenze di attività.<br /><br /> Questa impostazione non è supportata e non influisce sull'installazione del software.|  
|Windows Installer:<br /><br /> - Tutte le opzioni|Le impostazioni vengono ignorate|Il client non supporta impostazioni o file di Windows Installer.|  
|Modalità manutenzione OpsMgr:<br /><br /> - Tutte le opzioni|Le impostazioni vengono ignorate|Il client non supporta questa configurazione.|  

### <a name="deploy-software-to-a-linux-or-unix-server"></a>Distribuire il software in un server Linux o UNIX
 Per distribuire il software in un server Linux o UNIX usando un pacchetto e programma, è possibile usare la **Distribuzione guidata del software** dalla console di Configuration Manager. La maggior parte delle impostazioni di distribuzione è supportata dal client per Linux e UNIX. Tuttavia, alcune impostazioni non sono supportate. Quando si distribuisce il software, considerare i punti seguenti:  

- Effettuare il provisioning del pacchetto in almeno un punto di distribuzione associato al gruppo di limiti configurato per la posizione del contenuto.  

- È necessario che il client per Linux e UNIX che riceve questa distribuzione sia in grado di accedere a questo punto di distribuzione dal relativo percorso di rete.  

- Il client per Linux e UNIX scarica il pacchetto dal punto di distribuzione ed esegue il programma nel computer locale.  

- Il client per Linux e UNIX non è in grado di scaricare i pacchetti dalle cartelle condivise. Scarica i pacchetti dai punti di distribuzione abilitati per IIS che supportano HTTP o HTTPS.  

  Nella tabella seguente sono elencate le proprietà per le distribuzioni che non sono supportate:  

|Proprietà di distribuzione|Comportamento|Altre informazioni|  
|-------------------------|--------------|----------------------|  
|Impostazioni di distribuzione - scopo:<br /><br /> - Disponibile<br /><br /> - Richiesto|Le impostazioni vengono ignorate|Le impostazioni specifiche dell'utente non sono supportate.<br /><br /> Tuttavia, il client supporta l'impostazione **Richiesto**, che applica l'ora di installazione pianificata, ma non supporta l'installazione manuale prima di tale ora pianificata.|  
|Invia pacchetti di riattivazione|Le impostazioni vengono ignorate|Il client non supporta questa configurazione.|  
|Pianificazione assegnazione:<br /><br /> - Accesso<br /><br /> - Uscita|Viene generato un errore e l'installazione del software non viene completata|Le impostazioni specifiche dell'utente non sono supportate.<br /><br /> Tuttavia, il client supporta l'impostazione **Appena possibile**.|  
|Impostazioni di notifica:<br /><br /> - Consenti agli utenti di eseguire il programma indipendentemente dalle assegnazioni|Le impostazioni vengono ignorate|Il client non implementa un'interfaccia utente.|  
|Quando viene raggiunto il periodo di assegnazione pianificato, consentire l'esecuzione delle seguenti attività all'esterno della finestra di manutenzione:<br /><br /> - Riavvio del sistema (se necessario per completare l'installazione)|Viene generato un errore|Il client non supporta un riavvio del sistema.|  
|Opzione di distribuzione per reti veloci (LAN):<br /><br /> - Esegui programma dal punto di distribuzione|Viene generato un errore e l'installazione del software non viene completata|Il client non è in grado di eseguire il software dal punto di distribuzione ed è necessario che scarichi il programma prima di poterlo eseguire.|  
|Opzione di distribuzione per l'utilizzo entro i limiti di una rete lenta o non affidabile o l'utilizzo di un percorso di origine di fallback per il contenuto:<br /><br /> - Consenti ai client di condividere il contenuto con altri client nella stessa subnet|Le impostazioni vengono ignorate|Il client non supporta la condivisione del contenuto tra peer.|  

 Per altre informazioni sul percorso del contenuto, vedere [Gestire il contenuto e l'infrastruttura del contenuto per Configuration Manager](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

 Per altre informazioni sulla creazione di una distribuzione, vedere l'argomento relativo alla [distribuzione delle applicazioni](../../apps/deploy-use/deploy-applications.md).  

##  <a name="manage-network-bandwidth-for-software-downloads-from-distribution-points"></a>Gestione della larghezza di banda di rete per i download di software dai punti di distribuzione  
 Il client per Linux e UNIX supporta i controlli della larghezza di banda di rete durante il download di software da un punto di distribuzione.  

 Il client usa le impostazioni BITS (Servizio trasferimento intelligente in background) configurate come impostazioni client in Configuration Manager, ma non implementa il servizio BITS. Al contrario, per limitare l'utilizzo della larghezza di banda di rete, il client controlla la dimensione del blocco della richiesta HTTP e il ritardo tra i blocchi per il download del software.  

 Per configurare un client per l'utilizzo dei controlli della larghezza di banda di rete, vengono configurate le impostazioni client per **Trasferimento intelligente in background** e quindi applicate al computer client. Per usare i controlli della larghezza di banda, il client deve ricevere le impostazioni client per **Trasferimento intelligente in background** con le impostazioni seguenti configurate come **Sì**:  

- **Limitare la larghezza di banda di rete massima per i trasferimenti in background BITS**  

  Il client supporta le seguenti configurazioni per il Trasferimento intelligente in background:  

  -   **Ora di inizio dell'intervallo di limitazione**  

  -   **Ora di fine dell'intervallo di limitazione**  

  -   **Velocità massima di trasferimento durante l'intervallo di limitazione (Kbps)**  

  -   **Velocità massima di trasferimento all'esterno dell'intervallo di limitazione (Kbps)**  

La seguente configurazione per Trasferimento intelligente in background non è supportata e viene ignorata dal client per Linux e UNIX:  

- **Consentire i download BITS all'esterno dell'intervallo di limitazione**  

  Se il download del software nel client da un punto di distribuzione viene interrotto, il client per Linux e UNIX non lo riprende, ma riavvia il download dell'intero pacchetto software.  

##  <a name="configure-operations-for-software-deployments"></a>Configurare le operazioni per le distribuzioni software  
 Come per il client Windows, il client di Configuration Manager per Linux e UNIX individua nuove distribuzioni software quando esegue il polling e verifica la presenza di nuovi criteri. La frequenza con cui il client verifica la presenza di nuovi criteri dipende dalle impostazioni del client. È possibile configurare le finestre di manutenzione in modo che controllino quando si verificano le distribuzioni software.  

 È possibile configurare le distribuzioni software per i server Linux e UNIX utilizzando le proprietà del pacchetto, le proprietà del programma e le proprietà di distribuzione.  

 Quando il client riceve i criteri per una distribuzione, invia un messaggio di stato. Invia messaggi di stato anche quando l'installazione del software viene avviata e quando viene completata oppure non riesce.  

 I programmi per le distribuzioni software vengono eseguiti con le credenziali radice usate per l'esecuzione del client di Configuration Manager per Linux e UNIX. Il codice di uscita del comando per i programmi viene utilizzato per determinare l'esito positivo o negativo. Un codice di uscita pari a 0 (zero) viene considerato come esito positivo. Inoltre, **stdout** (flusso di output standard) e **stderr** (flusso di errore standard) vengono copiati nel file di log quando il livello del registro viene impostato su INFO o TRACE.  

> [!TIP]  
>  Se il software che si desidera distribuire è situato in una condivisione NFS (Network File System) a cui il server Linux o UNIX può accedere, non è necessario utilizzare un punto di distribuzione per scaricare il pacchetto. Al contrario, quando si crea un pacchetto non selezionare la casella di controllo per **Questo pacchetto contiene file di origine**. Quindi, quando si configura il programma, specificare la riga di comando appropriata per accedere direttamente al pacchetto nel punto di montaggio NFS.  
