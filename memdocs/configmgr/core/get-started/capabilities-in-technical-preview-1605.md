---
title: Funzionalità nella Technical Preview 1605
titleSuffix: Configuration Manager
description: Informazioni sulle funzionalità disponibili nella versione Technical Preview 1605 per Configuration Manager.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2bafd028-1923-4463-9e3e-ee41bc0c437b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: c38230b44f7f18e3f60cb4c88b31a03e10a37d30
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705599"
---
# <a name="capabilities-in-technical-preview-1605-for-configuration-manager"></a>Funzionalità della versione Technical Preview 1605 per Configuration Manager

*Si applica a: Configuration Manager (Technical Preview Branch)*

Questo articolo presenta le funzionalità disponibili nella Technical Preview per Configuration Manager versione 1605. È possibile installare questa versione per aggiornare e aggiungere nuove funzionalità al sito di Technical Preview di Configuration Manager.      Prima di installare questa versione Technical Preview, consultare l'argomento introduttivo [Technical Preview per Center Configuration Manager](../../core/get-started/technical-preview.md) per acquisire familiarità con i requisiti generali e con le limitazioni per l'uso di una versione Technical Preview, con le modalità di aggiornamento tra le versioni e con le modalità per offrire commenti e suggerimenti sulle funzionalità di una versione Technical Preview.  

 **Problemi noti di questa versione Technical Preview:**  

- Con la versione Technical Preview 1605, se si aggiornano le proprietà di un punto di gestione dopo l'installazione, si potrebbe ottenere un errore di console che forza la chiusura della console.  In questo caso è possibile disinstallare il punto di gestione e quindi reinstallarlo utilizzando le impostazioni desiderate. In alternativa è possibile modificare il punto di gestione prima di installare la versione Technical Preview 1605.  

- Quando si usa la funzionalità Windows Store per le aziende con la versione Technical Preview 1604 e quindi si esegue l'aggiornamento a Technical Preview 1605 non è più possibile visualizzare i dati di caricamento. Tutte le altre caratteristiche continuano a funzionare. Se si è eseguito il caricamento con la versione Technical Preview 1604, lo si mantiene dopo l'installazione di Technical Preview 1605 e non è necessario eseguire altre azioni.  

  **Di seguito sono riportate le nuove funzionalità disponibili con questa versione.**  

##  <a name="per-app-vpn-for-windows-10-devices"></a><a name="BKMK_PerAppVPN"></a> VPN per app per dispositivi Windows 10  
 Per i dispositivi Windows 10 gestiti usando Configuration Manager con Intune è possibile aggiungere un elenco di app che aprono automaticamente una connessione VPN configurata dalla console di amministrazione di Configuration Manager. È possibile scegliere di limitare il traffico VPN per tali applicazioni oppure continuare a consentire tutto il traffico tramite la connessione VPN.  

 **Requisiti**:  

-   Configuration Manager con Intune  

-   Un profilo VPN di Windows 10 che è stato distribuito ad almeno un dispositivo  

##  <a name="improvements-to-the-install-software-updates-task-sequence"></a><a name="BKMK_InstallSU"></a> Miglioramenti della sequenza di attività Installa aggiornamenti software  
 Sono stati apportati i seguenti miglioramenti alla sequenza di attività Installa aggiornamenti software:  

-   È disponibile la nuova variabile di sequenza di attività SMSTSSoftwareUpdateScanTimeout che consente di controllare il timeout dell'analisi degli aggiornamenti software durante il passaggio della sequenza di attività Installa aggiornamenti software. Il valore predefinito è 30 minuti.  

-   Sono stati apportati miglioramenti alla registrazione. Il file di registro smsts.log conterrà nuove voci di log che fanno riferimento ad altri file di log che consentono di risolvere i problemi durante il processo di installazione degli aggiornamenti software.  

##  <a name="improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step"></a><a name="BKMK_PrepareConfigMgrClient"></a> Miglioramenti del passaggio della sequenza di attività Prepara client ConfigMgr per l'acquisizione  
 Il passaggio Prepara client ConfigMgr a questo punto rimuove completamente il client di Configuration Manager, invece di rimuovere solo le informazioni sulla chiave. Quando la sequenza di attività distribuisce l'immagine del sistema operativo acquisita, verrà installato ogni volta un nuovo client di Configuration Manager.  

##  <a name="grace-period-for-required-application-deployments"></a><a name="BKMK_Grace"></a> Periodo di tolleranza per le distribuzioni di applicazioni obbligatorie  
 In alcuni casi è possibile concedere agli utenti più tempo per l'installazione di distribuzioni di applicazioni obbligatorie oltre eventuali scadenze configurate. Ad esempio, se un utente finale è appena tornato da una vacanza, potrebbe dover attendere un po' tempo mentre vengono installate le distribuzioni delle applicazioni scadute. Tuttavia potrà comunque installare l'applicazione immediatamente in qualsiasi momento.  

 Per risolvere il problema adesso è possibile definire un **periodo di tolleranza** distribuendo le impostazioni client di Configuration Manager in una raccolta.  

 Per configurare il periodo di tolleranza eseguire le operazioni seguenti:  

1. Nella pagina **Agente computer** delle impostazioni del client configurare la nuova proprietà **Periodo di tolleranza per l'imposizione dopo la scadenza della distribuzione (ore)** con un valore compreso tra **1** e **120** ore.  

2. In una nuova distribuzione dell'applicazione o nelle proprietà di una distribuzione esistente, nella pagina **Pianificazione** selezionare la casella di controllo **Ritardare l'imposizione di questa distribuzione in base alle preferenze dell'utente**, fino al periodo di tolleranza definito nelle impostazioni client.  

    Tutte le distribuzioni con questa casella di controllo selezionata e che sono destinate a dispositivi in cui è stata distribuita anche l'impostazione del client avranno il periodo di tolleranza.  

   In questa versione il periodo di tolleranza configurato non è utilizzato dai dispositivi client. Se si configura un periodo di tolleranza e si seleziona la casella di controllo, l'applicazione verrà installata nella prima finestra non aziendale che l'utente ha configurato dopo la scadenza.  

   Opzioni simili sono state aggiunte alla procedura guidata di distribuzione degli aggiornamenti software, alla procedura guidata di creazione delle regole di distribuzione automatica e alle pagine delle proprietà. Tuttavia non sono attualmente implementate in questa versione Technical Preview.  

##  <a name="new-experience-for-remote-device-actions"></a><a name="BKMK_Remote"></a> Nuova esperienza per le azioni dei dispositivi remoti  
 È stata migliorata l'esperienza di esecuzione di azioni dei dispositivi remoti dalla console di Configuration Manager.  
Azioni comuni come **Ritira/cancella dati**, **Reimpostazione passcode**, **Blocco remoto** e **Bypass del blocco attivazione** sono adesso disponibili nel menu **Azioni remote dispositivo** accessibile dall'area di lavoro **Asset e conformità**.  

 ![Nuova schermata Azioni remote dispositivo](media/New-Remote-Device-Actions.png)  

 È possibile trovare lo stato per ognuna di queste operazioni nelle seguenti posizioni:  

- Nel riquadro dei dettagli quando si seleziona un dispositivo dal nodo **Dispositivi**.  

- Nella pagina **Proprietà** per un dispositivo.  

- Nella pagina principale del nodo **Dispositivi** (non tutte le colonne potrebbero essere visibili per impostazione predefinita).  

##  <a name="windows-store-for-business-apps"></a><a name="BKMK_WSFB"></a> Windows Store per le app aziendali  
 In [Windows Store per le aziende](https://www.microsoft.com/business-store) è possibile trovare e acquistare app per l'organizzazione, singolarmente o con Volume Purchase Program. Connettendo lo Store a Configuration Manager, è possibile gestire le app acquistate con Volume Purchase Program dalla console di Configuration Manager, ad esempio:  

- È possibile sincronizzare l'elenco di app acquistate con Configuration Manager  

- Le app sincronizzate vengono visualizzate nella console di Configuration Manager e possono essere distribuite come qualsiasi altra app  

- Ogni 24 ore Configuration Manager scarica informazioni sulle licenze delle app dall'archivio ed è possibile esaminarle nella console di Configuration Manager  

  Nella versione Technical Preview 1604 è possibile sincronizzare e visualizzare le app da Windows Store per l'azienda nella console di Configuration Manager. In questa versione è stata aggiunta la possibilità di creare e distribuire applicazioni di Configuration Manager da app dello store sincronizzate.  

### <a name="set-up-windows-store-for-business-synchronization"></a>Configurare la sincronizzazione di Windows Store per le aziende  

1.  In Azure Active Directory registrare Configuration Manager come strumento di gestione "Applicazione Web e/o API Web". Si riceverà un ID client che sarà necessario in seguito.  

    1.  Nel nodo Active Directory di [https://manage.windowsazure.com](https://manage.windowsazure.com) selezionare Azure Active Directory e quindi fare clic su **Applicazioni** > **Aggiungi**.  

    2.  Fare clic su **Aggiungi un'applicazione che l'organizzazione sta sviluppando**.  

    3.  Immettere un nome per l'applicazione, selezionare **Applicazione Web** e/o **API Web** e quindi fare clic sulla freccia **Avanti**.  

    4.  Immettere lo stesso URL per **URL accesso** e **URI ID app**. L'URL può essere di qualsiasi tipo e non è necessario che venga risolto in un indirizzo reale. Ad esempio, è possibile immettere **https://&lt;dominioutente>/sccm**.  

    5.  Completare la procedura guidata.  

2.  In Azure Active Directory creare una chiave client per lo strumento di gestione registrato.  

    1.  Evidenziare l'applicazione appena creata e fare clic su **Configura**.  

    2.  In **Chiavi** selezionare una durata nell'elenco e fare clic su **Salva**. Verrà creata una nuova chiave client. Non uscire dalla pagina fino a quando non è stato completato il caricamento di Windows Store per le aziende in Configuration Manager.  

3.  In Windows Store per le aziende configurare Configuration Manager come strumento di gestione dello Store.  

    1.  Aprire [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/managementtools) ed eseguire l'accesso, se richiesto.  

    2.  Accettare le condizioni per l'utilizzo, se necessario.  

    3.  In **Management Tools** fare clic su **Add a management tool**.  

    4.  In **Search for the tool by name** digitare il nome dell'applicazione creata in precedenza in AAD e quindi fare clic su **Add**.  

    5.  Fare clic su **Activate** accanto all'applicazione appena importata.  

    6.  Nella procedura guidata **Show Offline-Licensed app** fare clic su **Yes** se si vuole consentire l'acquisto di applicazioni con licenza offline.  

4.  Acquistare almeno un'app da Windows Store per le aziende.  

5.  Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Servizi cloud** e quindi fare clic su **Windows Store per le aziende.**  

6.  Nel gruppo **Crea** della scheda **Home** fare clic su **Aggiungere un account di Windows Store per le aziende**.  

7.  Aggiungere l'ID tenant, l'ID client e la chiave client da Azure Active Directory, quindi completare la procedura guidata.  

8.  Al termine verrà visualizzato l'account configurato nell'elenco degli **account di Windows Store per le aziende** nella console di Configuration Manager.  

### <a name="try-it-out"></a>Verifica  
 Provare a completare l'operazione seguente e inviare le informazioni sul funzionamento della procedura utilizzando il modulo di feedback disponibile alla pagina del [programma dei commenti e suggerimenti di Configuration Manager](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) sul sito Microsoft Connect:  

 Creare e distribuire un'applicazione di Configuration Manager da un archivio di Windows per app aziendali con licenza offline.  

1. Nell'area di lavoro **Raccolta software** della console di Configuration Manager espandere **Gestione delle applicazioni** e fare clic su **Informazioni di licenza per le app dello Store**.  

2. Scegliere l'app che si vuole distribuire quindi nella scheda **Home** nel gruppo **Crea** fare clic su **Crea applicazione**.  

   Viene creata un'applicazione di Configuration Manager contenente l'archivio di Windows per l'applicazione aziendale. È quindi possibile distribuire e monitorare l'applicazione come qualsiasi altra applicazione di Configuration Manager.  

> [!IMPORTANT]  
>  Quando si crea un'applicazione di Configuration Manager con un solo tipo di distribuzione da un'app con licenza offline, è possibile distribuirla a dispositivi che sono gestiti da MDM e anche gestirla con il client di Configuration Manager. Se si tenta di distribuire un'app con più tipi di distribuzione l'installazione non riuscirà.  
>   
>  Attualmente non è possibile distribuire le applicazioni con licenza online con Configuration Manager.  

##  <a name="general-improvements-for-volume-purchased-apps"></a><a name="BKMK_VPP2"></a> Miglioramenti generali per le app acquistate con Volume Purchase Program  

-   In questa versione le app acquistate con Volume Purchase Program dall'archivio di Windows per l'azienda e iOS App Store sono state consolidate nella stessa visualizzazione **Informazioni di licenza per le app dello Store**.  

-   Per le app iOS acquistate con Volume Purchase Program la scheda Volume Purchase Program di Apple è stata rimossa dalla finestra di dialogo **Browser pacchetto app per iOS** nella Creazione guidata applicazione. Per creare un'app iOS acquistata con Volume Purchase Program eseguire questi passaggi:  

    1.  1.  Nell'area di lavoro **Raccolta software** della console di Configuration Manager espandere **Gestione delle applicazioni** e fare clic su **Informazioni di licenza per le app dello Store**.  

    2.  2.  Scegliere l'app che si vuole distribuire quindi nella scheda **Home** nel gruppo **Crea** fare clic su **Crea applicazione**.  

-   Il percorso che si usa per ottenere e caricare un token VPP di Apple per le app acquistate con Volume Purchase Program nella console di Configuration Manager è stato modificato. Ora è possibile farlo nell'area di lavoro **Amministrazione** sotto il nodo **Servizi cloud** > **Token di Volume Purchase Program di Apple**.  

##  <a name="enterprise-data-protection-edp"></a><a name="BKMK_VPP"></a> Enterprise Data Protection (EDP)  
 È possibile creare elementi di configurazione che consentono di distribuire i criteri di protezione dei dati aziendali (Enterprise Data Protection o EDP), ad esempio consentono di scegliere le app protette, il livello di protezione EDP e come trovare i dati aziendali in rete. Per altre informazioni su EDP, vedere gli argomenti seguenti:  

- [Proteggere i dati aziendali con Windows Information Protection (WIP)](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/protect-enterprise-data-using-wip)
- [Creare e distribuire un criterio di Windows Information Protection (WIP) con Configuration Manager](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr)


##  <a name="end-users-can-install-apps-from-the-company-portal"></a><a name="BKMK_End"></a> Gli utenti finali possono installare le app dal portale aziendale  
 MDM locale è stato introdotto nella versione 1511 di Configuration Manager. Nelle versioni precedenti era possibile distribuire applicazioni per dispositivi Windows 10 gestiti da MDM che avevano installazione **Richiesta** come scopo di distribuzione per dispositivi locali gestiti da MDM.  

 In questa versione è possibile distribuire applicazioni con lo scopo di distribuzione **Disponibile** a utenti di computer Windows 10 locali gestiti da MDM e gli utenti possono installare queste applicazioni autonomamente dal portale aziendale.
In questa versione Technical Preview se il portale aziendale rimane aperto per più di 15 minuti all'utente finale verrà visualizzato un messaggio di errore. Per risolvere il problema riavviare il portale aziendale.  

### <a name="before-you-start"></a>Prima di iniziare  

#### <a name="server-prerequisites"></a>Prerequisiti del server  

-   .NET 4.5 o versioni successive (richiede il riavvio)  

-   PowerShell 3.0 per lo script di configurazione (richiede il riavvio)  

#### <a name="client-prerequisites"></a>Prerequisiti client  

-   Windows 10 Desktop 1511 (build del sistema operativo 10586.218) o versione successiva  

#### <a name="general-prerequisites"></a>Prerequisiti generali  

-   Accertarsi di avere completato la [preparazione per Gestione dispositivi mobili locali](https://technet.microsoft.com/library/mt613153.aspx) e di aver [registrato i dispositivi](https://technet.microsoft.com/library/mt627870.aspx).  

-   Per la migliore esperienza di installazione delle applicazioni quando si usa il portale aziendale, assicurarsi che Configuration Manager disponga di una connessione attiva a Microsoft Intune.  

-   Se si sceglie l'opzione di registrazione in blocco, configurare l'affinità del dispositivo utente per il dispositivo registrato prima di provare questo scenario.  

### <a name="configuration-steps"></a>Procedura di configurazione  

#### <a name="install-the-application-catalog-roles-and-enable-mobile-device-management-support"></a>Installare i ruoli Catalogo applicazioni e abilitare il supporto di Gestione di dispositivi mobili  

1.  Aggiungere i ruoli Servizio Web e Sito Web del Catalogo applicazioni  

    1.  Selezionare **Modalità HTTPS** e l'opzione **Consenti ai dispositivi mobili di usare questo punto per servizi Web del Catalogo applicazioni**.  

    2.  Limitazioni note della versione Technical Preview:  

        -   È necessario disinstallare eventuali ruoli Catalogo applicazioni esistenti prima di selezionare l'opzione per consentire ai dispositivi mobili di connettersi.  

        -   Assicurarsi che esista un solo set di ruoli Catalogo applicazioni e che i ruoli si trovino nello stesso sistema del sito insieme ai ruoli Punto di registrazione e Punto proxy di registrazione.  

2.  Verificare che i componenti seguenti siano operativi dal nodo Stato componente nella console di Configuration Manager:  

    -   **SMS_AWEBSVC_CONTROL_MANAGER**  

    -   **SMS_DMAPPSVC_CONTROL_MANAGER**  

    -   **SMS_DMCONTENTSVC_CONTROL_MANAGER**  

    -   **SMS_PORTALWEB_CONTROL_MANAGER**  

### <a name="configure-boundaries"></a>Configurare i limiti  
 Configurare i limiti necessari per i punti di distribuzione solo intranet.  

> [!NOTE]  
>  In questo momento per la gestione dei dispositivi mobili sono supportati solo i limiti dell'intervallo IPv4.  

### <a name="deploy-the-company-portal-application-and-configuration"></a>Distribuire l'applicazione del portale aziendale e la configurazione  

1. Per preparare la distribuzione del portale aziendale e la configurazione, usare lo script di configurazione incluso nella versione Technical Preview:  

   1. Aprire un prompt di comando di PowerShell con privilegi elevati.  

   2. Eseguire **set-executionPolicy RemoteSigned**  

   3. Dalla cartella **&lt;directory di installazione SCCM\>\cd.latest\SMSSETUP\TOOLS\MDM** eseguire **.\ConfigurationScript.ps1**  

      Lo script di configurazione esegue le operazioni seguenti:  

   4. Crea un'applicazione di Configuration Manager con il tipo di distribuzione pacchetto app Windows tramite **CompanyPortalOnPremisesMDM.appx** nella stessa cartella.  

   5. Crea un elemento di configurazione e la linea di base di configurazione che configura il portale aziendale.  

   6. Consente di distribuire sia la linea di base di configurazione sia l'applicazione e aggiunge l'applicazione a tutti i punti di distribuzione.  

   > [!NOTE]
   >  Se i ruoli Catalogo applicazioni non si trovano nella stessa posizione del sito primario, eseguire le operazioni seguenti:  
   > 
   > - Nell'area di lavoro **Asset e conformità** individuare l'elemento di configurazione **OnPremMDM Portal Configuration CI - server urls** (CI configurazione portale OnPremMDM - URL del server)  
   >   -   Modificare il valore **Regole di conformità** nel nome di dominio completo del sistema del sito in cui si trovano i ruoli Catalogo applicazioni.  

2. Dopo aver distribuito l'applicazione del portale aziendale e la relativa configurazione, verificare che la linea di base dell'applicazione e della configurazione siano compatibili per il dispositivo specificato utilizzando la sezione **Distribuzioni** della console di Configuration Manager. Il portale aziendale verrà visualizzato come **Portale aziendale (Technical Preview)** nel menu Start sul dispositivo.  

### <a name="try-it-out"></a>Verifica  
 Provare a completare le operazioni seguenti e inviare le informazioni sul funzionamento della procedura utilizzando il modulo di feedback disponibile alla pagina del [programma dei commenti e suggerimenti di Configuration Manager](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) sul sito Microsoft Connect:  

1.  Distribuire varie applicazioni con tipi di distribuzione supportati a una raccolta di utenti con scopo di distribuzione **Disponibile**. In questa versione Technical Preview le applicazioni che richiedono l'approvazione dell'amministratore non sono supportate e non saranno visualizzate nel portale aziendale.  

2.  Gli utenti possono quindi cercare e installare le app dal portale aziendale.  

     Dopo l'apertura del portale aziendale, viene visualizzata una finestra di dialogo di autenticazione denominata **Configuration Manager**. Specificare le credenziali Active Directory dell'utente (nella forma user@domain o dominio\utente) per accedere.  

##  <a name="new-tabs-for-updates-and-operating-systems-in-software-center"></a><a name="BKMK_SW1"></a> Nuove schede per gli aggiornamenti e i sistemi operativi in Software Center  
 In questa versione sono state apportate le seguenti modifiche per migliorare il layout dell'applicazione Software Center:  

-   La scheda **Applicazioni** è stata suddivisa in tre schede separate: **Aggiornamenti**, **Sistemi operativi** (disponibili in precedenza nell'elenco **Filtri**) e **Applicazioni**.  

##  <a name="service-a--server-group"></a><a name="BKMK_ServerGroups"></a> Eseguire la manutenzione di un gruppo di server  
 La versione Technical Preview 1511 per Configuration Manager includeva la possibilità di creare una raccolta in cui tutti i dispositivi della raccolta formavano un gruppo di server. Quindi si poteva configurare le impostazioni del gruppo di server da usare per la distribuzione di aggiornamenti software al gruppo di server, controllare la percentuale di computer che venivano aggiornati in qualsiasi momento e configurare gli script di PowerShell di pre-distribuzione e post-distribuzione per eseguire azioni personalizzate.  

 La versione Technical Preview 1605 per Configuration Manager aggiunge la possibilità di aggiornare i computer del gruppo di server in un ordine specifico definito dall'utente, aggiunge il monitoraggio avanzato per visualizzare lo stato per i computer del gruppo di server e offre la possibilità di cancellare i blocchi di distribuzione, che si rivela utile quando i client non sono riusciti a installare gli aggiornamenti software e impediscono ad altri client di installare i loro aggiornamenti software.  

### <a name="try-it-out"></a>Verifica  
 Provare a completare le operazioni seguenti e inviare le informazioni sul funzionamento della procedura utilizzando il modulo di feedback disponibile alla pagina del [programma dei commenti e suggerimenti di Configuration Manager](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) sul sito Microsoft Connect:  

-   È possibile creare una raccolta che rappresenta un gruppo di server. Per questo test, è possibile configurare le regole di appartenenza alla raccolta in modo che nella raccolta siano presenti 2 macchine.   

-   È possibile specificare che i computer del gruppo di server installano gli aggiornamenti software in un ordine specifico in base alle impostazioni del gruppo di server per la raccolta. Utilizzare gli script di esempio nella procedura per specificare gli script di pre-distribuzione e post-distribuzione.  

-   È possibile distribuire un aggiornamento software a questa raccolta. Esaminare i file start.txt ed end.txt (creati dagli script di esempio) in C:\temp e verificare l'ora di inizio e fine per la distribuzione nei computer del gruppo di server. Esaminare il file UpdatesDeployment.log per ulteriori informazioni.  

#### <a name="to-create-a-collection-for-a-server-group"></a>Per creare una raccolta per un gruppo di server  

1.  [Creare una raccolta di dispositivi](https://technet.microsoft.com/library/gg712295.aspx) che contenga i computer del gruppo di server.  

2.  Nell'area di lavoro **Asset e conformità** fare clic su **Raccolte di dispositivi**, quindi fare clic con il pulsante destro del mouse sulla raccolta che contiene i computer del gruppo di server e scegliere **Proprietà**.  

3.  Nella scheda **Generale** selezionare **Tutti i dispositivi fanno parte dello stesso gruppo di server**, quindi fare clic su **Impostazioni**.  

4.  Nella pagina **Impostazioni gruppo di server** specificare una delle impostazioni seguenti:  

    -   **Consentire a una percentuale di computer di essere aggiornati contemporaneamente**: specifica che viene aggiornata solo una determinata percentuale di client alla volta. Se, ad esempio, l'insieme ha 10 client e la raccolta viene configurata per aggiornare il 30% dei client allo stesso tempo, solo 3 client installeranno gli aggiornamenti software in qualsiasi momento.  

    -   **Consentire a un numero di computer di essere aggiornati contemporaneamente**: specifica che viene aggiornato solo un determinato numero di client alla volta.  

    -   **Specifica la sequenza di manutenzione**: specifica che i client nella raccolta saranno aggiornati uno alla volta nella sequenza che viene configurata. Un client installerà gli aggiornamenti software solo dopo che il client che lo precede nell'elenco avrà completato l'installazione degli aggiornamenti.  

5.  Specificare se usare uno script di pre-distribuzione (svuotamento del nodo) o di post-distribuzione (ripresa del nodo).  

    > [!TIP]  
    >  Di seguito sono riportati alcuni esempi che è possibile usare nei test degli script di pre-distribuzione e post-distribuzione, con cui viene scritta l'ora corrente in un file di testo:  
    >   
    >  **Pre-distribuzione**  
    >   
    >  `#Start`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\start.txt`  
    >   
    >  **Post-distribuzione**  
    >   
    >  `#End`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\end.txt`  

#### <a name="to-deploy-software-updates-to-the-server-group-and-monitor-status"></a>Per distribuire gli aggiornamenti software nel gruppo di server e monitorare lo stato  

1.  [Distribuire gli aggiornamenti software](https://technet.microsoft.com/library/gg712304.aspx) nella raccolta del gruppo di server.  

2.  [Monitorare la distribuzione degli aggiornamenti software](https://technet.microsoft.com/library/gg712304.aspx). Oltre alle viste di monitoraggio standard per la distribuzione degli aggiornamenti software, una nuova descrizione dello stato viene visualizzata quando un client è in attesa del proprio turno per installare gli aggiornamenti software. Per il nuovo stato compare **In attesa di blocco**.  

#### <a name="to-clear-the-deployment-locks-for-computers-in-a-server-group"></a>Per cancellare i blocchi di distribuzione per i computer di un gruppo di server  

1.  Nell'area di lavoro **Asset e conformità** fare clic su **Raccolte di dispositivi** e quindi fare clic sulla raccolta per cancellare i blocchi.  

2.  Sulla scheda **Home**, nel gruppo **Distribuzione**, fare clic su **Cancellare i blocchi di distribuzione del gruppo di server**. Quando i client non sono riusciti a installare gli aggiornamenti software e impediscono ad altri client di installare i loro, i blocchi di distribuzione possono essere cancellati manualmente.  

##  <a name="support-for-microsoft-defender-advanced-threat-protection-service"></a><a name="BKMK_ATP"></a> Supporto del servizio Microsoft Defender Advanced Threat Protection  
 Microsoft Defender Advanced Threat Protection (ATP) è un servizio che consente alle aziende di rilevare, analizzare e rispondere agli attacchi avanzati sulle reti. Microsoft Defender ATP era noto in precedenza come Windows Defender ATP. Altre informazioni su [Microsoft Defender ATP](https://blogs.windows.com/windowsexperience/2016/03/01/announcing-windows-defender-advanced-threat-protection). Configuration Manager può essere d'aiuto per caricare e monitorare dispositivi client Windows 10 Anniversary Edition gestiti.  

### <a name="try-it-now"></a>Prova subito!  
 Provare a completare le operazioni seguenti e inviare le informazioni sul funzionamento della procedura utilizzando il modulo di feedback disponibile alla pagina del [programma dei commenti e suggerimenti di Configuration Manager](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) sul sito Microsoft Connect:  

- Caricare dispositivi sul servizio online Microsoft Defender Advanced Threat Protection (ATP)  

- Monitorare la distribuzione di Microsoft Defender ATP in dispositivi gestiti  

  **Prerequisiti**  

- Sottoscrizione al servizio online Microsoft Defender Advanced Threat Protection  

- Client che eseguono Windows 10 Anniversary Edition (build 14328 e versioni successive)  

- Creare un file di configurazione per il caricamento di client  

  ##### <a name="how-to-create-an-onboarding-configuration-file"></a>Come creare un file di configurazione per il caricamento  

  1.  Accedere al servizio online Microsoft Defender ATP  

  2.  Fare clic sulla voce di menu **Client On-boarding** (Caricamento client)  

  3.  Selezionare **Configuration Manager** e fare clic su **Scarica pacchetto**.  

  4.  Scaricare il file di archivio compresso (zip) ed estrarre il contenuto.  


##### <a name="onboard-devices-for-microsoft-defender-atp"></a>Caricare dispositivi per Microsoft Defender ATP  

1. Nella console di Configuration Manager passare ad **Asset e conformità** > **Panoramica** > **Protezione endpoint** > **Criteri di Windows Defender ATP** e fare clic su **Creare criteri di Windows Defender ATP**. Viene visualizzata la Creazione guidata criteri di Microsoft Defender ATP.  

2. Digitare il **nome** e la **descrizione** per il criterio di Microsoft Defender ATP e selezionare **Onboarding** (Caricamento). Scegliere Avanti.  

3. Usare **Sfoglia** per cercare il file di configurazione fornito dal tenant del servizio cloud Microsoft Defender ATP dell'organizzazione. Fare clic su **Avanti**.  

4. Specificare i file campione che vengono raccolti e condivisi dai dispositivi gestiti per l'analisi.  

   - **Nessuno**: nessun file campione viene raccolto per l'analisi  

   - **File eseguibili portabili**: file come programmi (.exe), librerie di collegamento dinamico (.dll), file di caratteri e simili, che possono essere sfruttati in attacchi informatici, vengono raccolti e condivisi per l'analisi  

     Fare clic su **Avanti**.  

5. Esaminare le informazioni di riepilogo e completare la procedura guidata.  

6. È ora possibile distribuire i criteri di Microsoft Defender ATP nei computer client gestiti facendo clic su **Distribuisci**.  

##### <a name="monitor-microsoft-defender-atp"></a>Monitorare Microsoft Defender ATP  

1.  Nella console di Configuration Manager passare a **Monitoraggio** > **Panoramica** > **Sicurezza** e quindi fare clic su **Windows Defender ATP**.  

2.  Esaminare il dashboard di Microsoft Defender Advanced Threat Protection.  

    -   **Windows Defender Agent Deployment Status** (Stato distribuzione agente Windows Defender): il numero e la percentuale di computer client gestiti idonei con criteri Microsoft Defender ATP attivi caricati  

    -   **Integrità dell'agente di Windows Defender ATP**: percentuale di computer client che inviano informazioni sullo stato per i relativi agenti di Microsoft Defender ATP  

        -   **Integro**: funziona correttamente  

        -   **Inattivo**: nessun dato inviato al servizio durante il periodo di tempo  

        -   **Stato agente**: il servizio di sistema per l'agente in Windows non è in esecuzione  

        -   **Non caricato**: i criteri sono stati applicati ma l'agente non ha segnalato il caricamento dei criteri  

##  <a name="on-premises-device-health-attestation"></a><a name="BKMK_DHA"></a> Attestazione dell'integrità del dispositivo locale  
 L'attestazione dell'integrità per i dispositivi Windows 10 può ora essere configurata per comunicare usando l'infrastruttura locale. Gli amministratori possono specificare se la creazione di report avviene tramite risorse cloud o locali. Se è selezionata l'opzione locale per la creazione di report di attestazione dell'integrità, è possibile specificare un URL per il servizio. In questo modo i PC client senza accesso a Internet possono abilitare e gestire i dispositivi usando l'attestazione dell'integrità.  

### <a name="enable-health-attestation-for-on-premises-devices"></a>Abilitare l'attestazione dell'integrità per i dispositivi locali  
 Nella versione 1605 sono stati corretti alcuni bug individuati nella Technical Preview 1604.  Per provare, configurare il servizio di attestazione dell'integrità locale usando le impostazioni agente client.  

1.  Nella console di Configuration Manager passare ad **Amministrazione** > **Panoramica** > **Impostazioni client**e quindi impostare **Usare il servizio di attestazione dell'integrità locale** su **Sì**.  

2.  Specificare l' **URL del servizio di attestazione dell'integrità locale**e quindi fare clic su **OK**.  

##  <a name="new-restart-options-for-windows-10-clients-after-software-update-installation"></a><a name="BKMK_RestartOptions"></a> Nuove opzioni di riavvio per i client Windows 10 dopo l'installazione degli aggiornamenti software  
 Quando un aggiornamento software che richiede il riavvio viene distribuito tramite Configuration Manager e viene installato in un computer, viene pianificato un riavvio in sospeso e viene visualizzata una finestra di dialogo di riavvio. Attualmente, per Windows 8 e versioni successive, se si arresta o si riavvia il computer tramite le opzioni di risparmio energia di Windows anziché dalla finestra di dialogo di riavvio, la finestra di dialogo di riavvio viene ancora visualizzata dopo il riavvio del computer e sarà necessario riavviare di nuovo il computer in corrispondenza della scadenza configurata. Nella versione Technical Preview, quando c'è un riavvio in sospeso per un aggiornamento software di Configuration Manager, tra le opzioni di risparmio energia di Windows nei computer Windows 10 sono disponibili **Aggiorna e riavvia**e **Aggiorna e arresta**. Dopo che una di queste opzioni è stata usata e il computer è stato riavviato, la finestra di dialogo di riavvio non verrà visualizzata.  

##  <a name="pre-declare-corporate-owned-devices-with-imei-or-ios-serial-number"></a><a name="BKMK_IMEI"></a> Pre-dichiarare i dispositivi di proprietà dell'azienda con numero di serie IMEI o iOS  
 È ora possibile identificare i dispositivi di proprietà dell'azienda importando i relativi codici IMEI (International station Mobile Equipment Identity). È possibile caricare un file con valori separati da virgola (CSV) contenente i codici IMEI o immettere manualmente le informazioni relative ai dispositivi.  È possibile importare i numeri di serie anche per i dispositivi iOS.  Le informazioni importate imposteranno la proprietà dei dispositivi registrati come "Aziendale".  È tuttavia necessaria una licenza di Intune per ogni utente che accede al servizio.  

### <a name="try-it-out"></a>Verifica  
 Provare a completare le operazioni seguenti e inviare le informazioni sul funzionamento della procedura utilizzando il modulo di feedback disponibile alla pagina del [programma dei commenti e suggerimenti di Configuration Manager](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) sul sito Microsoft Connect:  

-   Importare un set di numeri IMEI in un file .csv. Ogni riga può contenere il numero IMEI seguito da un campo di dettagli.  

-   Importare manualmente i numeri IMEI dalla console di Configuration Manager.  

-   Importare un set di numeri di serie iOS in un file .csv. Anche in questo caso, ogni riga contiene un numero seguito dai dettagli per il dispositivo.  

##### <a name="pre-declare-corporate-owned-devices-with-imei-or-ios-serial-number"></a>Predichiarazione dei dispositivi di proprietà dell'azienda con numero di serie IMEI o iOS  

1. Nella console di Configuration Manager passare ad **Asset e conformità** > **Panoramica** > **Tutti i dispositivi di proprietà dell'azienda** > **Dispositivi predichiarati** e fare clic su **Crea dispositivi predichiarati**. Verrà avviata la procedura guidata relativa ai dispositivi predichiarati.  

2. Specificare il modo in cui si vogliono aggiungere le informazioni sul dispositivo:  

   -   **Caricare un file .csv contenente numeri IMEI e dettagli**: per caricare un elenco di numeri, vedere il passaggio 3.  

   -   **Aggiungere manualmente i dettagli e i numeri IMEI**: per inserire manualmente le informazioni, digitare il numero IMEI o il numero di serie iOS e i dettagli per i dispositivi e quindi procedere al passaggio 4.  

3. Per i file caricati, individuare il file .csv contenente le informazioni per predichiarare i dispositivi aziendali. Il file deve avere il formato seguente, esclusa la prima riga, specificata a scopo informativo:  

   |**IMEI #**|**Numero di serie iOS**|**OS**|**Informazioni dettagliate**|
   |---|---|---|---|
   |123456789012345||WINDOWS|Dispositivo Windows di proprietà dell'azienda|
   |123456789012|A0BCD0EFGH0J|IOS|Dispositivi iOS di proprietà dell'azienda|
   |123456789012346||ANDROID|Dispositivo Android di proprietà dell'azienda|

    **Colonne:**  

   - Colonna 1: numero IMEI. Un numero IMEI o un numero di serie iOS è obbligatorio per ogni riga  

   - Colonna 2: numero di serie iOS. Solo i numeri di serie iOS possono essere predichiarati. Usare il numero IMEI per le altre piattaforme di dispositivi  

   - Colonna 3: sistema operativo del dispositivo (con distinzione tra maiuscole e minuscole):  

     -   IOS: tutti i dispositivi iOS  

     -   WINDOWS: include Windows Phone, Windows 10 per dispositivi mobili e PC Windows  

     -   ANDROID: tutti i dispositivi Android  

   - Colonna 4: dettagli. Informazioni aggiuntive sul dispositivo che vengono visualizzate nella console di Configuration Manager  

     Fare clic su **Avanti**.  

4. Esaminare i risultati dell'importazione del file. Per i numeri IMEI o i numeri di serie importati in precedenza, i dettagli saranno aggiornati con nuovi dettagli.  Fare clic su **Avanti** per continuare o **Indietro** per mantenere aggiornati i dettagli e completare la procedura guidata.  
