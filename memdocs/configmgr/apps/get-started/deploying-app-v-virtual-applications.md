---
title: Distribuire applicazioni virtuali App-V
titleSuffix: Configuration Manager
description: Questo articolo descrive le considerazioni da tenere presenti quando si creano e distribuiscono applicazioni virtuali.
ms.date: 03/12/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: ddcad9f2-a542-4079-83ca-007d7cb44995
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: df6f550b21523e365055f6a4cdafadca7603c4bf
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906377"
---
# <a name="deploy-app-v-virtual-applications-with-configuration-manager"></a>Distribuire applicazioni virtuali App-V con Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Quando si usa Configuration Manager per gestire applicazioni virtuali, si ottengono i vantaggi seguenti:  

-   Un'infrastruttura di gestione singola  

-   Funzionalità di scalabilità, distribuzione e di distribuzione del contenuto, come raccolte e affinità utente-dispositivo  

-   Funzionalità avanzate per la gestione delle applicazioni  

-   Distribuzione del sistema operativo, inventario software e hardware, misurazione del software e Asset Intelligence per il supporto delle applicazioni virtuali  

Per altre informazioni su come creare e sequenziare le applicazioni con Microsoft Application Virtualization (App-V), vedere la [documentazione di Application Virtualization 4](https://docs.microsoft.com/microsoft-desktop-optimization-pack/appv-v4/).  

Oltre agli altri requisiti e alle procedure di Configuration Manager per la creazione di un'applicazione, quando si creano e si distribuiscono applicazioni virtuali è necessario tenere presente quanto segue:

-   Per distribuire applicazioni virtuali nei computer, occorre che il client di Configuration Manager e di App-V siano installati sui computer. I dispositivi client possono includere computer desktop e portatili, nonché i client Virtual Desktop Infrastructure (VDI). Il software client di Configuration Manager e quello di App-V collaborano per recapitare, individuare e avviare i pacchetti delle applicazioni virtuali. Il client di Configuration Manager gestisce il recapito dei pacchetti delle applicazioni virtuali al client App-V. Il client App-V esegue l'applicazione virtuale sul client.  

-   Per distribuire un'applicazione virtuale, è necessario innanzitutto creare l'applicazione virtuale usando App-V Application Virtualization Sequencer. Il Sequencer monitora il processo di installazione e configurazione per un'applicazione e registra le informazioni necessarie per eseguire l'applicazione in un ambiente virtuale. È anche possibile usare il Sequencer per impostare i file e le configurazioni applicabili a tutti gli utenti e le configurazioni che possono essere personalizzate degli utenti.  

-   Quando si esegue la sequenziazione di un'applicazione, è necessario salvare il pacchetto in una posizione accessibile da Configuration Manager. È quindi possibile creare una distribuzione dell'applicazione che contiene l'applicazione virtuale.  

-   Configuration Manager non supporta l'uso della funzionalità di cache condivisa di sola lettura di App-V 4.6.  

-   Configuration Manager supporta la funzionalità di archivio dei contenuti condivisi in App-V 5.  

-   Quando si crea un tipo di distribuzione per un'applicazione virtuale, Configuration Manager crea il tipo di distribuzione usando i contenuti del file manifesto dell'applicazione. Si tratta di un file XML che contiene le informazioni sull'applicazione virtuale. Configuration Manager consente anche di creare i requisiti per il tipo di distribuzione in base al contenuto del file con estensione osd di App-V che include le informazioni sui sistemi operativi supportati per l'applicazione virtuale.  

-   Per distribuire applicazioni virtuali in Configuration Manager, nei computer client deve essere installato il client App-V 4.6 SP1 o una versione successiva.  

-   Per poter distribuire applicazioni virtuali, aggiornare il client App-V con l'hotfix più recente. Per altre informazioni, vedere [Elenco corrente delle versioni di file App-V 4.5 e App-V 4.6](https://support.microsoft.com/help/2950945/current-list-of-app-v-4-5-and-app-v-4-6-file-versions).

-   Quando si usano i gruppi di connessione in App-V 5.0, le applicazioni virtuali distribuite possono condividere lo stesso file system e Registro di sistema nei computer client. A differenza delle applicazioni virtuali standard, queste applicazioni possono condividere dati con un'altra. Inoltre, i gruppi di connessione mantengono le impostazioni utente per le applicazioni che contengono. Gli ambienti virtuali App-V in Configuration Manager vengono usati per configurare gruppi di connessione nei computer client. Gli ambienti virtuali vengono creati o modificati nei computer client quando viene installata l'applicazione o quando i client valutano le applicazioni installate. È possibile ordinare queste applicazioni in modo che quando più applicazioni tentano di modificare un valore del Registro di sistema o di file system, la priorità viene assegnata all'applicazione con l'ordine più elevato. Per altre informazioni, vedere [Create App-V virtual environments](../../apps/deploy-use/create-app-v-virtual-environments.md) (Creare ambienti virtuali App-V).  

##  <a name="supported-app-v-versions"></a>Versioni supportate di App-V  
 Configuration Manager supporta le versioni seguenti di App-V:  

-   **App-V 4.6**: per usare le applicazioni virtuali in Configuration Manager, nei computer client deve essere installato il client App-V 4.6 SP1, App-V 4.6 SP2 o App-V 4.6 SP3.  

     Per poter distribuire applicazioni virtuali è necessario aggiornare il client App-V 4.6 con l'hotfix più recente. Per altre informazioni, vedere [Elenco corrente delle versioni di file App-V 4.5 e App-V 4.6](https://support.microsoft.com/help/2950945/current-list-of-app-v-4-5-and-app-v-4-6-file-versions).  

-   **App-V 5, App-V 5.0 SP1, App-V 5.0 SP2, App-V 5.0 SP3 e App-V 5.1**: Per App-V 5.0 SP2, è necessario installare il [pacchetto hotfix 5](https://support.microsoft.com/help/2963211) oppure usare App-V 5.0 SP3.  
-   **App-V 5.2**: questa versione è inclusa in Windows 10 Education (1607 e versioni successive), Windows 10 Enterprise (1607 e versioni successive) e Windows Server 2016.

Per altre informazioni su App-V in Windows 10, vedere gli argomenti seguenti:

- [What's new in App-V](https://docs.microsoft.com/windows/application-management/app-v/appv-about-appv) (Novità di App-V)
- [Getting Started with App-V for Windows 10](https://docs.microsoft.com/windows/application-management/app-v/appv-getting-started) (Introduzione a App-V per Windows 10)
- [Upgrading to App-V for Windows 10 from an existing installation](https://docs.microsoft.com/windows/application-management/app-v/appv-upgrading-to-app-v-for-windows-10-from-an-existing-installation) (Aggiornamento da un'installazione esistente a App-V per Windows 10)

##  <a name="steps-to-manage-app-v-virtual-applications"></a>Passaggi per la gestione di applicazioni virtuali App-V  
 Per gestire le applicazioni virtuali App-V, seguire questi passaggi:  

1.   **Sequenziazione**: la sequenziazione è il processo di conversione di un'applicazione in un'applicazione virtuale usando il Sequencer App-V.

2.   **Crea**: usare la Creazione guidata tipo di distribuzione per importare l'applicazione sequenziata in un tipo di distribuzione di Configuration Manager che sia poi possibile aggiungere a un'applicazione. È inoltre possibile creare ambienti virtuali che consentano la condivisione delle impostazioni da parte di più applicazioni virtuali.

3.   **Distribuzione**: la distribuzione è il processo con cui le applicazioni App-V vengono rese disponibili nei punti di distribuzione di Configuration Manager.

4.   **Distribuisci**: l'implementazione è il processo con cui l'applicazione viene resa disponibile nei computer client. Nell'infrastruttura App-V completa questo processo è noto come pubblicazione e streaming.  

##  <a name="configuration-manager-virtual-application-delivery-methods"></a>Metodi di recapito delle applicazioni virtuali di Configuration Manager  
Configuration Manager supporta due metodi per il recapito di applicazioni virtuali ai client, ovvero recapito in streaming e recapito locale (download ed esecuzione).

Per decidere quale metodo di recapito usare, confrontare il requisito per lo spazio su disco ridotto per il recapito in streaming con la disponibilità garantita delle applicazioni App-V offerta dal recapito locale. L'aumento dello spazio su disco client richiesto per il recapito locale potrebbe essere preferibile al recapito in streaming in modo che gli utenti possano avere l'applicazione sempre a disposizione da qualsiasi posizione.  

###  <a name="streaming-delivery"></a>Recapito in streaming
Quando viene usato per gestire il client App-V, Configuration Manager supporta lo streaming di applicazioni virtuali tramite HTTP o HTTPS da un punto di distribuzione. Lo streaming tramite HTTP o HTTPS è abilitato per impostazione predefinita ed è configurato nella finestra di dialogo delle proprietà del punto di distribuzione. Quando si distribuisce un'applicazione virtuale nei computer client e un utente esegue l'applicazione virtuale, il client di Configuration Manager contatta un punto di gestione per determinare quale punto di distribuzione usare. Viene quindi eseguito lo streaming dell'applicazione dal punto di distribuzione.  

Usare le informazioni nella tabella seguente per decidere se il recapito in streaming è il metodo ottimale per le specifiche esigenze:

|Vantaggi|Svantaggi|  
|----------------|-------------------|  
|Questo metodo usa i protocolli di rete standard per lo streaming del contenuto del pacchetto dai punti di distribuzione.<br /><br /> I collegamenti ai programmi per le applicazioni virtuali richiedono una connessione al punto di distribuzione, in modo che il recapito dell'applicazione virtuale avvenga su richiesta.<br /><br /> Questo metodo funziona per i client con connessioni a banda larga ai punti di distribuzione.<br /><br /> Le applicazioni virtuali aggiornate distribuite in azienda sono disponibili poiché i client ricevono criteri che li informano che la versione corrente è stata sostituita e scaricano solo le modifiche dalla versione precedente.<br /><br /> Le autorizzazioni di accesso vengono definite nel punto di distribuzione per impedire agli utenti di accedere ad applicazioni o pacchetti non autorizzati.|Lo streaming delle applicazioni virtuali non viene eseguito fino a quando l'utente non esegue l'applicazione per la prima volta. In questo scenario, un utente potrebbe ricevere dei collegamenti ai programmi per le applicazioni virtuali e poi scollegarsi dalla rete prima di eseguire le applicazioni virtuali per la prima volta. Se l'utente tenta di eseguire l'applicazione virtuale mentre il client è offline, viene visualizzato un errore e l'utente non potrà eseguire l'applicazione virtualizzata perché un punto di distribuzione di Configuration Manager non è disponibile per lo streaming dell'applicazione. L'applicazione non sarà disponibile fino a quando l'utente non si riconnette alla rete e non esegue l'applicazione.<br /><br /> Per evitarlo, è possibile usare il metodo di recapito locale per il recapito dell'applicazione virtuale ai client oppure abilitare la gestione client basata su Internet per il recapito in streaming.|  

###  <a name="local-delivery-download-and-execute"></a>Recapito locale (download ed esecuzione)  
Il metodo del download e dell'esecuzione è l'approccio più comune quando si usa Configuration Manager, dal momento che questo approccio simula strettamente la modalità di recapito degli altri formati di applicazioni con Configuration Manager. Quando si usa questo metodo di recapito, il client di Configuration Manager scarica per prima cosa l'intero pacchetto dell'applicazione virtuale nella cache del client di Configuration Manager, quindi dà istruzione al client App-V di eseguire lo streaming dell'applicazione dalla cache di Configuration Manager nella cache di App-V. Se si distribuisce un'applicazione virtuale nei computer client e il contenuto non si trova nella cache di App-V, il client App-V esegue lo streaming del contenuto dell'applicazione dalla cache del client di Configuration Manager nella cache App-V ed esegue l'applicazione. Dopo l'esecuzione corretta dell'applicazione, è possibile configurare il client di Configuration Manager per eliminare tutte le versioni precedenti del pacchetto nel ciclo di eliminazione successivo oppure mantenerle nella cache del client di Configuration Manager. Per mantenere il contenuto in locale, è possibile sfruttare i metodi di ottimizzazione per la distribuzione del contenuto dei pacchetti, quali BranchCache e PeerCache.

Usare le informazioni nella tabella seguente per decidere se il recapito locale è il metodo ottimale per le specifiche esigenze:   

|Vantaggi|Svantaggi|  
|----------------|-------------------|  
|La funzionalità del punto di distribuzione standard viene usata per scaricare il pacchetto tramite il Servizio trasferimento intelligente in background (BITS).<br /><br /> Il contenuto del pacchetto dell'applicazione virtuale viene recapitato in locale al client. Questo significa che gli utenti possono eseguirlo quando il computer non è connesso alla rete.<br /><br /> Questo metodo è adatto per le connessioni di rete lente o inaffidabili e per i computer che si connettono solo occasionalmente alla rete.<br /><br /> Configuration Manager usa la compressione differenziale remota (RDC) per inviare ai client solo i byte all'interno dei file che sono stati modificati quando è stato aggiornato il contenuto del pacchetto dell'applicazione virtuale. Il client di Configuration Manager usa la RDC per costruire una nuova versione del pacchetto di un'applicazione virtuale sulla base della versione corrente del pacchetto e di tutte le modifiche inviate al client.<br /><br /> Questo metodo fornisce flessibilità di applicazione per gli utenti mobili o per gli utenti scollegati. Gli amministratori possono scegliere di mantenere il pacchetto nella cache di Configuration Manager dopo il recapito se l'applicazione virtuale è stata distribuita con un'azione di installazione. Il pacchetto nella cache del client di Configuration Manager serve come origine streaming locale e affidabile al client App-V per portare il pacchetto nella propria cache.|Quando l'applicazione virtuale viene mantenuta nella cache di Configuration Manager, nel client è necessaria una quantità di spazio su disco pari fino al doppio delle dimensioni del pacchetto dell'applicazione virtuale.|  

###  <a name="deployment-from-an-image"></a>Distribuzione da un'immagine

È possibile inoltre preinstallare le applicazioni virtuali su un computer e quindi creare un'immagine di tale computer per la distribuzione in altri computer. Se il pacchetto dell'applicazione virtuale è stato creato in un sito differente, tuttavia, la replica delle differenze binarie non verrà usata per scaricare gli aggiornamenti per l'applicazione. Questa opzione può essere utile in un'infrastruttura desktop virtuale quando si desidera che le applicazioni siano immediatamente disponibili invece di scaricarle dopo l'accesso dell'utente.    

##  <a name="migrating-from-an-app-v-infrastructure-to-a-configuration-manager-and-app-v-infrastructure"></a>Migrazione da un'infrastruttura App-V a un'infrastruttura Configuration Manager e App-V  
Usare la tabella seguente per pianificare una migrazione da un'infrastruttura App-V esistente alla gestione di un'applicazione virtuale con Configuration Manager.  

|Passaggio|Altre informazioni|  
|----------|----------------------|  
|Esaminare le applicazioni virtuali correnti per scegliere le applicazioni di cui si intende effettuare la migrazione nell'infrastruttura di Configuration Manager.|Nessuna informazione aggiuntiva.|  
|Valutare gli utenti e i dispositivi in cui verranno distribuite le applicazioni virtuali.|Creare raccolte di Configuration Manager per raggruppare utenti e dispositivi ai quali si vogliono distribuire le applicazioni virtuali. Vedere [Introduzione alle raccolte](../../core/clients/manage/collections/introduction-to-collections.md).|  
|Eseguire la migrazione dei gruppi di connessione di App-V 5 negli ambienti virtuali di Configuration Manager.|Vedere la sezione [Eseguire la migrazione dei gruppi di connessione di App-V 5 negli ambienti virtuali di Configuration Manager](deploying-app-v-virtual-applications.md#migrating-app-v-5-connection-groups-to-configuration-manager-virtual-environments) in questo argomento.|  
|Analizzare e scoprire se una delle applicazioni virtuali esiste come applicazione completa nell'infrastruttura di Configuration Manager.|Per una gestione più semplice, è possibile aggiungere l'applicazione virtuale come nuovo tipo di distribuzione all'applicazione completa esistente. Vedere [Creare applicazioni](../../apps/deploy-use/create-applications.md).|  
|Creare applicazioni per sostituire i pacchetti App-V esistenti.|Vedere [Introduzione alla gestione delle applicazioni](../understand/introduction-to-application-management.md) e [Creare applicazioni](../../apps/deploy-use/create-applications.md).|  
|Configuration Manager comincia a gestire applicazioni virtuali su un client dopo la prima distribuzione di un'applicazione virtuale. Successivamente, tutte le applicazioni App-V nel computer devono essere gestite da Configuration Manager.|Nessuna informazione aggiuntiva.|  
|Distribuire il contenuto nei punti di distribuzione appropriati per consentire il recapito locale delle applicazioni.|Vedere [Gestire il contenuto e l'infrastruttura del contenuto](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).|  
|Distribuire l'applicazione ai client di Configuration Manager.<br /><br /> Se l'applicazione App-V è stata creata con una versione precedente del sequencer che non crea un file XML manifesto, è possibile aprirla e salvarla in una versione più recente del sequencer per creare il file. Questo file è necessario per distribuire le applicazioni virtuali con Configuration Manager.<br /><br /> App-V supporta i pacchetti di applicazioni virtuali creati con SoftGrid 4.1 SP1 o le versioni 4.2 del sequencer.<br /><br /> Se le applicazioni sono state precedentemente installate in locale, è necessario disinstallarle prima di distribuire una versione virtuale dell'applicazione.|Vedere [Come distribuire le applicazioni](../../apps/deploy-use/deploy-applications.md).|  
|Configuration Manager non supporta più l'uso di pacchetti e programmi che contengono applicazioni virtuali. Quando esegue la migrazione da Configuration Manager 2007 a Configuration Manager Current Branch, Configuration Manager converte questi pacchetti in applicazioni.<br /><br /> Gli annunci di Configuration Manager 2007 vengono convertiti nei tipi di distribuzione seguenti:<br /><br /> - Migrazione di pacchetti App-V con nessun annuncio:  un tipo di distribuzione che usa le impostazioni predefinite del tipo di distribuzione.<br /><br /> - Migrazione di pacchetti App-V con un annuncio: un tipo di distribuzione che usa le stesse impostazioni dell'annuncio di <br />                Configuration Manager 2007.<br /><br /> - Migrazione di pacchetti App-V con più annunci: un tipo di distribuzione, per ogni <br />                annuncio di Configuration Manager 2007 che usa le impostazioni per tale annuncio.|Vedere [Pianificare la migrazione degli oggetti a Configuration Manager Current Branch](../../core/migration/planning-for-the-migration-of-objects.md).|  

##  <a name="migrating-app-v-5-connection-groups-to-configuration-manager-virtual-environments"></a>Migrazione di gruppi di connessione App-V 5 in ambienti virtuali di Configuration Manager  
Gli ambienti virtuali App-V in Configuration Manager consentono alle applicazioni virtuali distribuite di condividere lo stesso file system e Registro di sistema nei computer client. Ciò significa che, a differenza delle applicazioni virtuali standard, queste applicazioni possono condividere dati tra loro. Gli ambienti virtuali vengono creati o modificati nei computer client quando viene installata l'applicazione o quando i client valutano le applicazioni installate. Gli ambienti virtuali sono simili ai gruppi di connessione in App-V 5 autonoma.  

Quando si esegue la migrazione dei gruppi di connessione dalla versione autonoma di App-V 5 agli ambienti virtuali di Configuration Manager, è necessario assicurarsi che i gruppi di connessione già esistenti nei computer client vengano gestiti correttamente da Configuration Manager e che venga mantenuto l'ambiente dell'utente all'interno di tali gruppi di connessione.  

Per convertire i gruppi di connessione App-V 5 in ambienti virtuali di Configuration Manager:  

1.  Creare applicazioni di Configuration Manager per tutte le applicazioni esistenti in App-V.  

2.  Distribuire tali applicazioni a utenti o dispositivi con scopo della distribuzione **Richiesto**. Le distribuzioni agli utenti devono essere indirizzate agli stessi utenti che hanno usato l'applicazione in App-V. Le distribuzioni ai computer devono essere indirizzate agli stessi computer che avevano l'applicazione in App-V.  

3.  Dopo aver completato la distribuzione, creare ambienti virtuali corrispondenti ai gruppi di connessione pubblicati nella versione autonoma di App-V. L'ambiente virtuale deve contenere gli stessi pacchetti, in particolare, i tipi di distribuzione di App-V 5, nello stesso ordine.  

Per informazioni su come creare un ambiente virtuale App-V, vedere [How to create App-V virtual environments](../../apps/deploy-use/create-app-v-virtual-environments.md) (Come creare ambienti virtuali App V).  

In alternativa è possibile eliminare tutti i gruppi di connessione dal client App-V prima di iniziare la distribuzione delle applicazioni con Configuration Manager. Le eventuali impostazioni salvate dagli utenti nei gruppi di connessione di App-V andranno però perse.  

##  <a name="dynamic-suite-composition-in-app-v-46"></a>Dynamic Suite Composition in App-V 4.6  
Dynamic Suite Composition è una funzionalità che consente di definire un pacchetto applicazione virtuale con dipendenza da un altro pacchetto applicazione virtuale. Quando l'applicazione viene eseguita, il client App-V ospita il pacchetto primario e quello dipendente nello stesso ambiente virtuale destinato all'applicazione.  

Per usare questa funzionalità con Configuration Manager, è necessario che entrambi i pacchetti siano distribuiti e registrati con il client App-V. Per assicurarsi che il contenuto del pacchetto dipendente sia ospitato localmente nel computer client, configurare la distribuzione dell'applicazione per il recapito locale (download ed esecuzione).  

Per altre informazioni sulla funzionalità Dynamic Suite Composition di App-V, vedere la documentazione di App-V.  

##  <a name="converting-app-v-46-applications-to-app-v-5-applications"></a>Conversione di applicazioni App-V 4.6 in applicazioni App-V 5  
Il formato relativo al pacchetto dell'applicazione è stato modificato tra App-V 4.6 e App-V 5. Le applicazioni sequenziate da App-V 4.6 non sono più supportate. App-V 5 include comunque uno strumento di conversione pacchetti che può essere usato per convertire le applicazioni. Per altre informazioni, vedere [Come convertire un pacchetto creato in una versione precedente di App-V](https://docs.microsoft.com/microsoft-desktop-optimization-pack/appv-v5/how-to-convert-a-package-created-in-a-previous-version-of-app-v).  

Per convertire le applicazioni App-V 4.6 in applicazioni App-V 5, attenersi alla procedura seguente:  

1.  Convertire o ri-sequenziare i pacchetti App-V 4.6 nel formato App-V 5.  

2.  Distribuire il client App-V 5 ai computer della gerarchia.  

3.  Creare nuove applicazioni contenenti tipi di distribuzione per le applicazioni App-V 5 e creare le regole di sostituzione per sostituire le applicazioni App-V 4.6.  

4.  Creare i necessari ambienti virtuali.  

5.  Distribuire le nuove applicazioni App-V 5 ai computer.  

##  <a name="user-and-deployment-configuration-files"></a>File di configurazione dell'utente e della distribuzione  
I file di configurazione dell'utente e della distribuzione contengono impostazioni che controllano il comportamento di un'applicazione. È possibile usare tali file per modificare le impostazioni dell'applicazione senza ri-sequenziarla.  

Una tipica applicazione App-V 5 potrebbe contenere i seguenti file:  

-   Un file di pacchetto applicazione (.appv)  

-   Un file di configurazione dell'utente  

-   Un file di configurazione della distribuzione  

Il file di configurazione dell'utente contiene impostazioni che si applicano solo all'utente connesso. È ad esempio possibile modificare i file di configurazione per modificare le informazioni sul collegamento dell'applicazione da distribuire agli utenti. È anche possibile creare un'applicazione di Configuration Manager con più tipi di distribuzione, ciascuna contenente un file di configurazione dell'utente diverso e regole requisiti tali da assicurarne l'installazione agli utenti desiderati.  

Il file di configurazione della distribuzione contiene le impostazioni relative al computer, come le impostazioni del Registro di sistema. Il file può contenere anche impostazioni utente, che vengono applicate a tutti gli utenti.  

Se si intende distribuire applicazioni virtuali App-V 5 con Configuration Manager, questi tre file dovranno essere presenti nella stessa cartella quando si crea il tipo di distribuzione App-V 5. Se la cartella contiene più file, Configuration Manager userà il più recente.  

Per altre informazioni, vedere [Informazioni sulla configurazione dinamica di App-V 5.0](https://docs.microsoft.com/microsoft-desktop-optimization-pack/appv-v5/about-app-v-50-dynamic-configuration).  

##  <a name="app-v-local-interaction"></a>Interazione locale di App-V  
In determinati scenari di distribuzione, alcune applicazioni vengono installate localmente nei computer client e altre applicazioni vengono distribuite come applicazioni virtuali negli stessi computer client. Per impostazione predefinita, le applicazioni installate localmente non possono vedere o comunicare direttamente con le applicazioni virtualizzate. Questo è il comportamento previsto da App-V per l'isolamento delle applicazioni. L'interazione locale è una funzionalità del client App-V che può essere abilitata per consentire alle applicazioni installate localmente in esecuzione in un computer client di vedere e comunicare con le applicazioni virtualizzate. Configuration Manager e App-V offrono il pieno supporto dell'interazione locale.  

Per altre informazioni sulla funzionalità di interazione locale di App-V, vedere la documentazione di App-V.  

##  <a name="app-v-5-shared-content-store"></a>Archivio contenuti condivisi di App-V 5  
Configuration Manager supporta la funzionalità SCS (Shared Content Store) di App-V 5. Per altre informazioni, vedere la pagina relativa alla [pianificazione per Shared Content Store (SCS) di App-V 5.0](https://docs.microsoft.com/microsoft-desktop-optimization-pack/appv-v5/planning-for-the-app-v-50-sequencer-and-client-deployment#planning-for-the-app-v-50-shared-content-store-scs).  

##  <a name="monitoring-virtual-applications"></a>Monitoraggio di applicazioni virtuali  

### <a name="virtual-application-reports"></a>Report di applicazioni virtuali  
È possibile usare i report seguenti per monitorare App-V nell'ambiente Configuration Manager:  

|Nome report|Descrizione|  
|-----------------|-----------------|  
|Risultati ambiente virtuale App-V|Mostra informazioni su un ambiente virtuale selezionato che si trova in uno stato specificato per una raccolta selezionata (solo App-V 5).|  
|Risultati ambiente virtuale App-V per asset|Mostra informazioni su un ambiente virtuale selezionato per un asset specificato ed eventuali tipi di distribuzione per l'ambiente virtuale selezionato (solo App-V 5).|  
|Stato ambiente virtuale App-V|Mostra informazioni di conformità per un ambiente virtuale selezionato per una raccolta selezionata. La colonna **Permanenza** di questo report mostra gli asset in cui un ambiente virtuale precedentemente configurato non è più applicabile, ma viene conservato per mantenere le impostazioni utente nelle applicazioni eseguite nell'ambiente virtuale (solo App-V 5).|  
|Computer con un'applicazione virtuale specifica|Mostra un riepilogo dei computer che dispongono del collegamento App-V specificato creato da Application Virtualization Management Sequencer (solo App-V 4.6).|  
|Computer con un pacchetto applicazione virtuale specifico|Mostra un elenco dei computer in cui è installato il pacchetto applicazione App-V specificato (solo App-V 4.6).|  
|Conteggio di tutte le istanze dei pacchetti di applicazioni virtuali|Mostra un conteggio di tutti i pacchetti applicazioni App-V rilevati (solo App-V 4.6).|  
|Conteggio di tutte le istanze delle applicazioni virtuali|Mostra un conteggio di tutte le applicazioni App-V rilevate (solo App-V 4.6).|  

### <a name="log-files"></a>File di registro  
Configuration Manager registra le informazioni sulla distribuzione di applicazioni virtuali nei file di log. Per informazioni sui file di log usati dalle applicazioni virtuali e per la gestione di applicazioni di Configuration Manager, vedere [File di log](../../core/plan-design/hierarchy/log-files.md).  

Per Windows 8.1, i log per il client App-V sono disponibili in C:\ProgramData\Microsoft\Application Virtualization Client.  
