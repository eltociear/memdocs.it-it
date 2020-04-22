---
title: Technical Preview 1802 | Microsoft Docs
titleSuffix: Configuration Manager
description: Informazioni sulle funzionalità disponibili nella versione Technical Preview 1802 per Configuration Manager.
ms.date: 02/09/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4884a2d3-13ce-44e5-88c4-a66dc7ec6014
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 50e05d07ec3e2612c170157c45f5e64abe3766de
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701329"
---
# <a name="capabilities-in-technical-preview-1802-for-configuration-manager"></a>Funzionalità della versione Technical Preview 1802 per Configuration Manager

*Si applica a: Configuration Manager (Technical Preview Branch)*

Questo articolo presenta le funzionalità disponibili nella Technical Preview per Configuration Manager versione 1802. È possibile installare questa versione per aggiornare e aggiungere nuove funzionalità al sito di Technical Preview di Configuration Manager. 

Vedere [Technical Preview per Configuration Manager](technical-preview.md) prima di installare questa versione della Technical Preview. L'articolo consente di acquisire familiarità con i requisiti e le limitazioni generali per l'uso di una Technical Preview, con l'aggiornamento tra le versioni e con l'invio di commenti e suggerimenti.     


<!--  Known Issues Template   
## Known Issues in this Technical Preview:
-   **Issue Name**. Details
    Workaround details.
-->
## <a name="known-issues-in-this-technical-preview"></a>Problemi noti di questa versione Technical Preview
- **L'aggiornamento a una nuova versione di anteprima ha esito negativo se il server del sito è in modalità passiva**. Se si usa un [server del sito primario in modalità passiva](capabilities-in-technical-preview-1706.md#site-server-role-high-availability), è necessario disinstallare il server del sito in modalità passiva prima dell'aggiornamento a questa nuova versione di anteprima. Sarà possibile reinstallare il server del sito in modalità passiva al termine dell'aggiornamento del sito.

  Per disinstallare il server del sito in modalità passiva:
  1. Nella console di Configuration Manager passare ad **Amministrazione** > **Panoramica** > **Configurazione del sito** > **Server e ruoli del sistema del sito** e quindi selezionare il server del sito in modalità passiva.
  2. Nel riquadro **Ruoli sistema del sito** fare clic con il pulsante destro del mouse sul ruolo **Server del sito** e quindi scegliere **Rimuovi ruolo**.
  3. Fare clic con il pulsante destro del mouse sul server del sito in modalità passiva e quindi scegliere **Elimina**.
  4. Dopo la disinstallazione del server del sito, nel server del sito primario attivo riavviare il servizio **CONFIGURATION_MANAGER_UPDATE**.
  <!--sms 489412-->


</br>

**Di seguito sono riportate le nuove funzionalità disponibili con questa versione.**  


## <a name="transition-endpoint-protection-workload-to-intune-using-co-management"></a>Eseguire la transizione del carico di lavoro di Endpoint Protection a Intune tramite la co-gestione    
<!-- 1357365 -->
In questa versione è ora possibile eseguire la transizione del carico di lavoro di Endpoint Protection da Configuration Manager a Intune dopo aver abilitato la co-gestione. Per eseguire questa transizione, passare alla pagina delle proprietà di co-gestione e spostare la barra del dispositivo di scorrimento da Configuration Manager a **Pilota** o **Tutto**. Per i dettagli, vedere [Co-gestione per dispositivi Windows 10](../../comanage/overview.md).


 
## <a name="configure-windows-delivery-optimization-to-use-configuration-manager-boundary-groups"></a>Configurare Ottimizzazione recapito di Windows per usare i gruppi di limiti di Configuration Manager
<!-- 1324696 -->
I gruppi di limiti di Configuration Manager consentono di definire e regolamentare la distribuzione del contenuto nella rete aziendale e negli uffici remoti. [Ottimizzazione recapito di Windows](/windows/deployment/update/waas-delivery-optimization) è una tecnologia peer-to-peer basata sul cloud per la condivisione di contenuti tra dispositivi Windows 10. A partire da questa versione è possibile configurare Ottimizzazione recapito in modo che usi i gruppi di limiti quando si condividono contenuti tra peer. Una nuova impostazione client applica l'identificatore del gruppo di limiti come identificatore di gruppo di Ottimizzazione recapito sul client. Quando il client comunica con il servizio cloud Ottimizzazione recapito, usa questo identificatore per individuare i peer con il contenuto desiderato. 

### <a name="prerequisites"></a>Prerequisiti
- Ottimizzazione recapito è disponibile solo nei client Windows 10

### <a name="try-it-out"></a>Verifica
 Provare a completare le attività. Quindi inviare **Commenti e suggerimenti** dalla scheda **Home** della barra multifunzione.

1. Nella console di Configuration Manager creare un criterio di impostazioni dispositivo client personalizzate nel nodo **Impostazioni client** dell'area di lavoro **Amministrazione**.
2. Selezionare il nuovo gruppo **Ottimizzazione recapito**.
3. Abilitare l'impostazione **Usare i gruppi di limiti di Configuration Manager per l'ID del gruppo di ottimizzazione recapito**.

Per altre informazioni, vedere l'opzione di modalità di recapito **Gruppo** in [Delivery Optimization options](/windows/deployment/update/waas-delivery-optimization#how-microsoft-uses-delivery-optimization) (Opzioni di Ottimizzazione recapito).



## <a name="windows-10-in-place-upgrade-task-sequence-via-cloud-management-gateway"></a>Sequenza di attività di aggiornamento sul posto di Windows 10 tramite Cloud Management Gateway
<!-- 1357149 -->

Ora la [sequenza di attività di aggiornamento sul posto](../../osd/deploy-use/upgrade-windows-to-the-latest-version.md) di Windows 10 supporta la distribuzione nei client basati su Internet tramite [Cloud Management Gateway](../clients/manage/cmg/plan-cloud-management-gateway.md). Ciò consente agli utenti remoti di eseguire più facilmente l'aggiornamento a Windows 10 senza doversi connettere alla rete aziendale. 

Assicurarsi che tutto il contenuto a cui fa riferimento la sequenza di attività di aggiornamento sul posto sia distribuito a un [punto di distribuzione cloud](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md). In caso contrario i dispositivi non potranno eseguire la sequenza di attività.

Per distribuire una sequenza di attività di aggiornamento sul posto usare le impostazioni seguenti:
- **Consenti l'esecuzione della sequenza di attività per il client in Internet** nella scheda Esperienza utente della distribuzione.
- **Scaricare tutto il contenuto localmente prima di avviare la sequenza di attività** nella scheda Punti di distribuzione della distribuzione. Altre opzioni come **Scaricare il contenuto localmente quando necessario eseguendo la sequenza di attività** non sono applicabili a questo scenario. Il motore di esecuzione della sequenza attività non è attualmente in grado di ottenere contenuto da un punto di distribuzione cloud. Il client Gestione configurazione deve scaricare il contenuto dal punto di distribuzione cloud prima di avviare la sequenza di attività.
- (*Facoltativo*) **Pre-download del contenuto per questa sequenza di attività** nella scheda Generale della distribuzione. Per altre informazioni, vedere [Configurare la pre-cache del contenuto](../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md#configure-pre-cache-content).



## <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Miglioramenti alla sequenza di attività di aggiornamento sul posto di Windows 10
<!-- 1357425 -->
Il modello di sequenza di attività predefinita per l'aggiornamento sul posto di Windows 10 include ora gruppi aggiuntivi con azioni consigliate da aggiungere prima e dopo il processo di aggiornamento. Queste azioni sono comuni tra numerosi clienti che stanno aggiornando i propri dispositivi a Windows 10. 

### <a name="new-groups-under-prepare-for-upgrade"></a>Nuovi gruppi in **Preparazione dell'aggiornamento**
- **Verifiche della batteria**: consente di aggiungere passaggi in questo gruppo per verificare se il computer usa la batteria o l'alimentazione tramite cavo. Per eseguire questo controllo serve un'utilità o uno script personalizzato.
- **Verifiche della connessione di rete/via cavo**: consente di aggiungere passaggi in questo gruppo per verificare se il computer è connesso a una rete e non usa una connessione wireless. Per eseguire questo controllo serve un'utilità o uno script personalizzato.
- **Rimuovi le applicazioni non compatibili**: consente di aggiungere passaggi in questo gruppo per rimuovere eventuali applicazioni non compatibili con questa versione di Windows 10. Il metodo per disinstallare un'applicazione varia a seconda dei casi. Se l'applicazione usa Windows Installer, copiare la riga di comando **Disinstalla programma** dalla scheda **Programmi** nelle proprietà del tipo di distribuzione di Windows Installer dell'applicazione. Quindi aggiungere un passaggio **Esegui riga di comando** in questo gruppo con la riga di comando Disinstalla programma. Ad esempio: </br>`msiexec /x {150031D8-1234-4BA8-9F52-D6E5190D1CBA} /q`</br> 
- **Rimuovi i driver non compatibili**: consente di aggiungere passaggi in questo gruppo per rimuovere eventuali driver non compatibili con questa versione di Windows 10.
- **Rimuovi/Sospendi la sicurezza di terze parti**: consente di aggiungere passaggi in questo gruppo per rimuovere o sospendere programmi di sicurezza di terze parti, ad esempio l'antivirus.
   - Se si usa un programma di crittografia dischi di terze parti, fornire il relativo driver di crittografia al programma di Installazione di Windows con l'[opzione della riga di comando](/windows-hardware/manufacture/desktop/windows-setup-command-line-options) **/ReflectDrivers**. Aggiungere un passaggio [Imposta variabile della sequenza di attività](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) alla sequenza di attività in questo gruppo. Impostare la variabile della sequenza di attività su **OSDSetupAdditionalUpgradeOptions**. Impostare il valore su **/ReflectDriver** con il percorso del driver. Questa [variabile di azione della sequenza di attività](../../osd/understand/task-sequence-steps.md#BKMK_UpgradeOS) accoda la riga di comando del programma di installazione di Windows usata dalla sequenza di attività. Per ulteriori indicazioni su questo processo, contattare il fornitore del software in uso.

### <a name="new-groups-under-post-processing"></a>Nuovi gruppi in **Post-elaborazione**
- **Applica driver basati su installazione**: consente di aggiungere passaggi in questo gruppo per installare driver basati su installazione (EXE) dai pacchetti.
- **Installa/Abilita la sicurezza di terze parti**: consente di aggiungere passaggi in questo gruppo per installare o abilitare i programmi di sicurezza di terze parti, ad esempio l'antivirus. 
- **Imposta le app predefinite e le associazioni di Windows**: consente di aggiungere passaggi in questo gruppo per impostare le app predefinite e le associazioni di file di Windows. Preparare prima un computer di riferimento con le associazioni di app desiderate. Quindi eseguire l'esportazione tramite la riga di comando seguente: </br>`dism /online /Export-DefaultAppAssociations:"%UserProfile%\Desktop\DefaultAppAssociations.xml"`</br>Aggiungere il file XML a un pacchetto. Quindi aggiungere un passaggio [Esegui riga di comando](../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) in questo gruppo. Specificare il pacchetto che contiene il file XML, quindi specificare la riga di comando seguente: </br>`dism /online /Import-DefaultAppAssociations:DefaultAppAssocations.xml`</br> Per altre informazioni, vedere [Export or import default application associations](/windows-hardware/manufacture/desktop/export-or-import-default-application-associations) (Esportare o importare associazioni di applicazioni predefinite).
- **Applica personalizzazioni**: consente di aggiungere passaggi in questo gruppo per applicare le personalizzazioni del menu Start, ad esempio l'organizzazione di gruppi di programmi. Per altre informazioni, vedere [Customize the Start screen](/windows-hardware/manufacture/desktop/customize-the-start-screen) (Personalizzare la schermata iniziale).

### <a name="additional-recommendations"></a>Suggerimenti aggiuntivi
- Vedere l'articolo [Risolvere gli errori di aggiornamento di Windows 10](/windows/deployment/upgrade/resolve-windows-10-upgrade-errors) nella documentazione di Windows. Questo articolo include anche informazioni dettagliate sul processo di aggiornamento.
- Nel passaggio predefinito **Verifica conformità** abilitare **Verifica lo spazio minimo disponibile su disco (MB)** . Impostare il valore su almeno **16384** (16 GB) per un pacchetto di aggiornamento del sistema operativo a 32 bit o su **20480** (20 GB) per un pacchetto a 64 bit. 
- Usare la [variabile di sequenza di attività predefinita](../../osd/understand/task-sequence-variables.md) **SMSTSDownloadRetryCount** per riprovare a scaricare i criteri. Per impostazione predefinita, attualmente il client esegue due tentativi; questa variabile è impostata su due (2). Se i client non sono su una connessione di rete aziendale cablata, ulteriori tentativi possono aiutare a ottenere i criteri per tali client. L'uso di questa variabile non ha effetti collaterali negativi, se non un errore ritardato in caso il download dei criteri non riesca.<!-- 501016 --> Aumentare inoltre il valore della variabile **SMSTSDownloadRetryDelay** dai 15 secondi predefiniti.
- Eseguire una valutazione della compatibilità inline. 
   - Aggiungere un secondo passaggio **Aggiorna sistema operativo** nel gruppo **Preparazione dell'aggiornamento**. Assegnargli in nome *Valutazione aggiornamento*. Specificare lo stesso pacchetto di aggiornamento e quindi abilitare l'opzione **Esegui analisi compatibilità Installazione di Windows senza avviare l’aggiornamento**. Abilitare **Continua in caso di errore** nella scheda Opzioni. 
   - Subito dopo questo passaggio *Valutazione aggiornamento* aggiungere un passaggio **Esegui riga di comando**. Specificare la riga di comando seguente:</br> `cmd /c exit %_SMSTSOSUpgradeActionReturnCode%`</br>Nella scheda **Opzioni** aggiungere la condizione seguente: </br>`Task Sequence Variable _SMSTSOSUpgradeActionReturnCode not equals 3247440400` </br>Questo codice restituito è l'equivalente in formato decimale di MOSETUP_E_COMPAT_SCANONLY (0xC1900210), che indica una valutazione della compatibilità riuscita senza problemi. Se il passaggio *Valutazione aggiornamento* riesce e restituisce questo codice, questo passaggio non viene eseguito. Se invece il passaggio di valutazione restituisce qualsiasi altro codice, questo passaggio esegue con errori la sequenza di attività con il codice restituito dall'analisi di compatibilità di Installazione di Windows.
   - Per altre informazioni, vedere [Aggiorna sistema operativo](../../osd/understand/task-sequence-steps.md#BKMK_UpgradeOS).
- Se si vuole modificare il dispositivo da BIOS a UEFI durante questa sequenza di attività, vedere [Conversione da BIOS a UEFI durante un aggiornamento sul posto](../../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md#convert-from-bios-to-uefi-during-an-in-place-upgrade).

Se si hanno altri suggerimenti, selezionare **Feedback** nella scheda **Home** sulla barra multifunzione.



## <a name="improvements-to-pxe-enabled-distribution-points"></a>Miglioramenti ai punti di distribuzione che supportano PXE
<!-- 1357580 -->
Per chiarire il comportamento della [nuova funzionalità PXE](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6) introdotta per la prima volta nella Technical Preview versione 1706, l'opzione **Supporto IPv6** è stata rinominata. Nella scheda **PXE** delle proprietà del punto di distribuzione selezionare **Abilita un risponditore PXE senza i Servizi di distribuzione Windows**. 

Questa opzione abilita un risponditore PXE nel punto di distribuzione, che non richiede Servizi di distribuzione Windows. Se si abilita questa nuova opzione in un punto di distribuzione che supporta già PXE, Configuration Manager sospende l'esecuzione di Servizi di distribuzione Windows. Se si disabilita questa nuova opzione ma si lascia selezionata l'opzione **Abilita supporto PXE per i client**, il punto di distribuzione abilita di nuovo Servizi di distribuzione Windows.

Poiché i Servizi di distribuzione Windows non sono obbligatori, il punto di distribuzione che supporta PXE può essere un sistema operativo client o server, incluso Windows Server Core. Questo nuovo servizio risponditore PXE continua a supportare IPv6 e migliora inoltre la flessibilità dei punti di distribuzione che supportano PXE negli uffici remoti.

> [!NOTE]
> Questo servizio usa la stessa tecnologia di base del [servizio risponditore PXE basato su client](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) disponibile nella Technical Preview versione 1712. Tale funzionalità non richiede l'overhead del ruolo del punto di distribuzione.

### <a name="multicast"></a>Multicast
Per abilitare e configurare il multicast nella scheda **Multicast** delle proprietà del punto di distribuzione, il punto di distribuzione deve usare Servizi di distribuzione Windows. 
- Se si seleziona **Abilita supporto PXE per i client** e **Abilita multicast per inviare contemporaneamente dati a più client**, non è possibile selezionare anche **Abilita un risponditore PXE senza i Servizi di distribuzione Windows**.
- Se si seleziona **Abilita supporto PXE per i client** e **Abilita un risponditore PXE senza i Servizi di distribuzione Windows**, non è possibile selezionare anche **Abilita multicast per inviare contemporaneamente dati a più client**.



## <a name="deployment-templates-for-task-sequences"></a>Modelli di distribuzione per le sequenze di attività
<!-- 1357391 -->
Ora la distribuzione guidata per le sequenze di attività può creare un modello di distribuzione. Il modello di distribuzione può essere salvato e applicato a una sequenza di attività nuova o esistente per creare una distribuzione. 

### <a name="try-it-out"></a>Verifica  
Provare a completare le attività. Quindi inviare **Commenti e suggerimenti** dalla scheda **Home** della barra multifunzione. 

 **Creare un modello di distribuzione per una nuova distribuzione di sequenza di attività** <br/> 
1. Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi** e selezionare **Sequenze di attività**.
2. Fare clic con il pulsante destro del mouse su una sequenza di attività e scegliere **Distribuisci**. 
3. Nella scheda **Generale** è ora presente l'opzione **Seleziona modello di distribuzione**. 
4. Proseguire con la **Distribuzione guidata del software** selezionando le impostazioni di distribuzione della sequenza di attività. 
5. Quando si raggiunge la scheda **Riepilogo** della **Distribuzione guidata del software**, fare clic su **Salva come modello**.
6. Assegnare un nome al modello e selezionare le impostazioni da salvare nel modello. 
7. Fare clic su **Save**. Il modello è ora disponibile per l'uso tramite l'opzione **Seleziona modello di distribuzione**.



## <a name="product-lifecycle-dashboard"></a>Dashboard del ciclo di vita del prodotto
<!--1319632-->
Il nuovo [dashboard del ciclo di vita del prodotto](../clients/manage/asset-intelligence/product-lifecycle-dashboard.md) mostra lo stato del criterio Ciclo di vita del prodotto Microsoft per i prodotti Microsoft installati nei dispositivi gestiti con Configuration Manager. Fornisce informazioni sui prodotti Microsoft in uso nell'ambiente, sullo stato del supporto e sulle date di fine del supporto. È possibile usare il dashboard per conoscere la disponibilità del supporto per ogni prodotto. 

Per accedere al dashboard del ciclo di vita, nella console di Configuration Manager scegliere **Asset e conformità** >**Asset Intelligence** >**Ciclo di vita del prodotto**.



## <a name="improvements-to-reporting"></a>Miglioramenti alla funzione di reporting
<!--1357653-->
In seguito al [feedback degli utenti](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/32434147-new-builtin-reports-about-windows-10-versions-and), è stato aggiunto un nuovo report sui **dettagli relativi alla manutenzione dei pacchetti di Windows 10 per una raccolta specifica**. Questo report mostra le informazioni seguenti relative ai dispositivi Windows 10: ID risorsa, nome NetBIOS, nome del sistema operativo, versione del sistema operativo, build, branch del sistema operativo e stato di manutenzione. Per accedere al report, scegliere **Monitoraggio** >**Report** >**Report** >**Sistemi operativi** >**Windows 10 Servicing details for a specific collection** (Dettagli manutenzione pacchetti di Windows 10 per una raccolta specifica).



## <a name="improvements-to-software-center"></a>Miglioramenti a Software Center
<!--1357592-->
In seguito al [feedback degli utenti](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/13002684-software-center-show-only-available-software-hid), ora le applicazioni installate possono essere nascoste in Software Center. Quando questa opzione è abilitata, le applicazioni che sono già installate non compaiono più nella scheda Applicazioni. 

### <a name="try-it-out"></a>Verifica
Abilitare l'impostazione **Nascondi le applicazioni installate in Software Center** nelle impostazioni client di Software Center. Osservare il comportamento di Software Center quando l'utente finale installa un'applicazione.



## <a name="improvements-to-run-scripts"></a>Miglioramenti alla funzionalità Esegui script
<!--1236459-->
La funzionalità [Esegui script](../../apps/deploy-use/create-deploy-scripts.md) restituisce ora l'output dello script con la formattazione JSON. Questo formato restituisce in modo coerente un output dello script leggibile. È possibile che l'output degli script la cui esecuzione non riesce non venga restituito. 



## <a name="boundary-group-fallback-for-management-points"></a>Fallback del gruppo di limiti per i punti di gestione
<!-- 1324594 -->
A partire da questa versione, è possibile configurare relazioni di fallback per i punti di gestione tra [gruppi di limiti](../servers/deploy/configure/boundary-groups.md). Questo comportamento consente un maggiore controllo per i punti di gestione usati dai client. Nella scheda **Relazioni** delle proprietà del gruppo di limiti è presente una nuova colonna per il punto di gestione. Quando si aggiunge un nuovo gruppo di limiti di fallback, attualmente il tempo di fallback per il punto di gestione è sempre zero (0). Questo comportamento corrisponde all'opzione **Comportamento predefinito** del gruppo di limiti predefinito del sito.

Nelle versioni precedenti si verifica comunemente un problema in presenza di un punto di gestione protetto in una rete protetta. I client nella rete aziendale principale ricevono criteri che includono questo punto di gestione protetto, anche se non possono comunicare con esso attraverso un firewall. Per risolvere il problema, usare l'opzione **Non eseguire mai il fallback** per fare in modo che i client eseguano il fallback solo ai punti di gestione con cui possono comunicare.

Quando si aggiorna il sito a questa versione, Configuration Manager aggiunge tutti i punti di gestione senza connessione Internet nel gruppo di limiti predefinito del sito. Questo comportamento dell'aggiornamento assicura che le versioni client precedenti continuino a comunicare con i punti di gestione. Per sfruttare tutti i vantaggi di questa funzionalità, spostare i punti di gestione nei gruppi di limiti desiderati.

Il comportamento del fallback dei gruppi di limiti dei punti di gestione non cambia durante l'installazione dei client (ccmsetup). Se la riga di comando non specifica il punto di gestione iniziale tramite il parametro /MP, il nuovo client riceve l'elenco completo dei punti di gestione disponibili. Per il processo di avvio iniziale, il client usa il primo punto di gestione a cui può accedere. Una volta registratosi con il sito, il client riceve l'elenco dei punti di gestione correttamente ordinato con questo nuovo comportamento. 

### <a name="prerequisites"></a>Prerequisiti
- Abilitare i [punti di gestione preferiti](../servers/deploy/configure/boundary-groups.md#bkmk_preferred). Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**. Espandere **Configurazione del sito** e selezionare **Siti**. Fare clic su **Impostazioni gerarchia** sulla barra multifunzione. Nella scheda **Generale** abilitare **I client preferiscono usare i punti di gestione specificati nei gruppi di limiti**. 

### <a name="known-issues"></a>Problemi noti
- I processi di distribuzione dei sistemi operativi non sono a conoscenza dei gruppi di limiti.

### <a name="troubleshooting"></a>Risoluzione dei problemi
Nel log **LocationServices.log** sono presenti nuove voci. L'attributo **Locality** identifica uno degli stati seguenti:
- 0: Sconosciuto
- 1: il punto di gestione specificato si trova solo nel gruppo di limiti predefinito del sito per il fallback
- 2: il punto di gestione specificato si trova in un gruppo di limiti remoto o adiacente. Quando il punto di gestione si trova sia in un gruppo di limiti vicino sia in quello predefinito del sito, l'attributo locality è uguale a 2.
- 3: il punto di gestione specificato si trova nel gruppo di limiti locale o corrente. Quando il punto di gestione si trova sia nel gruppo di limiti corrente e in uno vicino o in quello predefinito del sito, l'attributo locality è uguale a 3. Se non si abilita l'impostazione dei punti di gestione preferiti in Impostazioni gerarchia, l'attributo locality è sempre uguale a 3 indipendentemente dal gruppo di limiti in cui si trova il punto di gestione.

I client usano prima i punti di gestione locali (locality 3), quindi quelli remoti (locality 2) e infine eseguono il fallback (locality 1). 

Quando un client riceve cinque errori in dieci minuti e non riesce a comunicare con un punto di gestione nel relativo gruppo di limiti corrente, cerca di contattare un punto di gestione in un gruppo di limiti vicino o in quello predefinito del sito. Se in seguito il punto di gestione nel gruppo di limiti corrente torna online, il client torna al punto di gestione locale al successivo ciclo di aggiornamento. Il ciclo di aggiornamento avviene ogni 24 ore o al riavvio del servizio agente di Configuration Manager.



## <a name="improved-support-for-cng-certificates"></a>Supporto migliorato per i certificati CNG
<!-- 1357314 -->
Configuration Manager (Current Branch) versione 1710 supporta i [certificati CNG (Cryptography: Next Generation)](../plan-design/network/cng-certificates-overview.md). La versione 1710 limita il supporto ai certificati client in diversi scenari. 

A partire da questa versione della Technical Preview, è possibile usare i certificati CNG per i ruoli del server abilitati pe HTTPS seguenti:
- Punto di gestione
- Punto di distribuzione
- Punto di aggiornamento software

L'elenco degli [scenari non supportati](../plan-design/network/cng-certificates-overview.md#unsupported-scenarios) rimane invariato.



## <a name="cloud-management-gateway-support-for-azure-resource-manager"></a>Supporto di Cloud Management Gateway per Azure Resource Manager
<!-- 1324735 -->
Quando si crea un'istanza di [Cloud Management Gateway](../clients/manage/cmg/plan-cloud-management-gateway.md), ora la procedura guidata consente di creare una **distribuzione Azure Resource Manager**. [Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) è una piattaforma moderna per la gestione di tutte le risorse di una soluzione come una singola entità detta [gruppo di risorse](/azure/azure-resource-manager/resource-group-overview#resource-groups). Quando si distribuisce Cloud Management Gateway con Azure Resource Manager, il sito usa Azure Active Directory (Azure AD) per autenticare e creare le risorse cloud necessarie. Questa distribuzione modernizzata non richiede il certificato di gestione classico di Azure.  

La procedura guidata di Cloud Management Gateway offre ancora l'opzione per una **distribuzione classica del servizio** tramite un certificato di gestione di Azure. Per semplificare la distribuzione e la gestione delle risorse, è consigliabile usare il modello di distribuzione Azure Resource Manager per tutte le nuove istanze di Cloud Management Gateway. Se possibile, ridistribuire le istanze di Cloud Management Gateway esistenti tramite Resource Manager.

Configuration Manager non esegue la migrazione delle istanze di Cloud Management Gateway classiche esistenti nel modello di distribuzione Azure Resource Manager. Creare nuove istanze di Cloud Management Gateway usando le distribuzioni Azure Resource Manager e quindi rimuovere le istanze di Cloud Management Gateway classiche. 

> [!IMPORTANT]
> Questa funzionalità non supporta i provider di servizi cloud di Azure. La distribuzione di Cloud Management Gateway con Azure Resource Manager continua infatti a usare il servizio cloud classico, non supportato dal provider di servizi cloud. Per altre informazioni, vedere [Available Azure services in Azure CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services) (servizi di Azure disponibili in Azure CSP).  

### <a name="prerequisites"></a>Prerequisiti
- Integrazione con [Azure AD](../clients/deploy/deploy-clients-cmg-azure.md). L'individuazione utenti di Azure AD non è necessaria.
- Stessi [requisiti di Cloud Management Gateway](../clients/manage/cmg/plan-cloud-management-gateway.md#requirements), ad eccezione del certificato di gestione di Azure.

### <a name="try-it-out"></a>Verifica  
 Provare a completare le attività. Quindi inviare **Commenti e suggerimenti** dalla scheda **Home** della barra multifunzione.

1. Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Servizi cloud** e selezionare **Cloud Management Gateway**. Fare clic su **Crea un gateway di gestione cloud** sulla barra multifunzione. 
2. Nella pagina **Generale** selezionare **Modello di distribuzione Azure Resource Manager**. Fare clic su **Accedi** per eseguire l'autenticazione con un account amministratore della sottoscrizione di Azure. La procedura guidata compila automaticamente i campi rimanenti in base alle informazioni di sottoscrizione di Azure AD archiviate durante il prerequisito di integrazione. Se si hanno più sottoscrizioni, selezionare quella che si vuole usare. Fare clic su **Avanti**.  
3. Nella pagina **Impostazioni** specificare il file del certificato PKI server come di consueto. Questo certificato definisce il nome del servizio Cloud Management Gateway in Azure. Selezionare l'area in **Area** e quindi selezionare **Crea nuovo** o **Usa esistente** per il gruppo di risorse. Immettere il nome del nuovo gruppo di risorse o selezionare un gruppo di risorse esistente nell'elenco a discesa. 
4. Completare la procedura guidata.

> [!NOTE] 
> Per l'app server Azure AD selezionata Azure assegna l'autorizzazione di **collaboratore** per la sottoscrizione. 

Monitorare lo stato della distribuzione del servizio con **cloudmgr.log** nel punto di connessione del servizio.



## <a name="approve-application-requests-for-users-per-device"></a>Approvazione delle richieste di applicazioni degli utenti per dispositivo
<!-- 1357015 -->
A partire da questa versione, quando un utente invia la richiesta per un'applicazione che richiede l'approvazione, il nome del dispositivo specifico fa parte della richiesta. Se l'amministratore approva la richiesta, l'utente può installare l'applicazione solo su quel dispositivo. Per installare l'applicazione in un altro dispositivo dovrà inviare un'altra richiesta. 

> [!NOTE]
> Questa funzionalità è facoltativa. Quando si esegue l'aggiornamento a questa versione, abilitare questa funzionalità nell'Aggiornamento guidato. In alternativa, è possibile abilitarla nella console in un secondo momento. Per altre informazioni, vedere [Enable optional features from updates](../servers/manage/install-in-console-updates.md#bkmk_options) (Abilitare le funzioni facoltative dagli aggiornamenti).

### <a name="prerequisites"></a>Prerequisiti
- Aggiornare il client Gestione configurazione all'ultima versione
- Abilitare l'impostazione client **Usa il nuovo Software Center** nel gruppo [Agente computer](../clients/deploy/about-client-settings.md#computer-agent).

### <a name="try-it-out"></a>Verifica
 Provare a completare le attività. Quindi inviare **Commenti e suggerimenti** dalla scheda **Home** della barra multifunzione.

1. Distribuire un'applicazione come disponibile a una raccolta di utenti.
2. Nella pagina **Impostazioni di distribuzione** abilitare l'opzione: **Un amministratore deve approvare una richiesta per questa applicazione nel dispositivo**.
3. In qualità di utente designato, usare Software Center per inviare una richiesta per l'applicazione. 
4. Nell'area di lavoro **Raccolta software** della console di Configuration Manager visualizzare **Richieste di approvazione** in **Gestione applicazioni**. Nell'elenco è ora presente una colonna **Dispositivo** per ogni richiesta. Quando si intraprende un'azione sulla richiesta, la finestra di dialogo Richiesta di applicazioni include anche il nome del dispositivo da cui l'utente ha inviato la richiesta.



## <a name="use-software-center-to-browse-and-install-user-available-applications-on-azure-ad-joined-devices"></a>Usare Software Center per esplorare e installare le applicazioni disponibili per gli utenti in dispositivi aggiunti ad Azure AD
<!-- 1322613 -->
Se si distribuiscono applicazioni come disponibili agli utenti, questi possono ora esplorarle e installarle tramite Software Center nei dispositivi Azure Active Directory (Azure AD).  

### <a name="prerequisites"></a>Prerequisiti
- Abilitare HTTPS nel punto di gestione
- Integrare il sito con [Azure AD](../clients/deploy/deploy-clients-cmg-azure.md)
- Distribuire un'applicazione come disponibile a una raccolta di utenti
- Distribuire il contenuto dell'applicazione a un [punto di distribuzione cloud](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md)
- Abilitare l'impostazione client **Usa il nuovo Software Center** nel gruppo [Agente computer](../clients/deploy/about-client-settings.md#computer-agent).
- Il client deve essere: 
   - Windows 10
   - Aggiunto ad Azure AD, detto anche aggiunto a un dominio cloud
- Per supportare i client basati su Internet:
    - [Gateway di gestione cloud](../clients/manage/cmg/plan-cloud-management-gateway.md) 
    - Abilitare l'impostazione client: **Abilitare le richieste dei criteri utente dai client Internet** nel gruppo [Criteri client](../clients/deploy/about-client-settings.md#client-policy)
- Per supportare i client nella rete aziendale:
    - Aggiungere il punto di distribuzione cloud a un gruppo di limiti usato dai client
    - I client devono essere in grado di risolvere il nome di dominio completo (FQDN) del punto di gestione abilitato per HTTPS



## <a name="report-on-windows-autopilot-device-information"></a>Report sulle informazioni sui dispositivi di Windows AutoPilot
<!-- 1351442 -->
Windows AutoPilot è una soluzione per l'onboarding e la configurazione di nuovi dispositivi Windows 10 in un modo moderno. Per altre informazioni, vedere una [panoramica di Windows AutoPilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-10-autopilot). Un metodo per registrare i dispositivi esistenti con Windows AutoPilot consiste nel caricare le informazioni sul dispositivo in Microsoft Store per le aziende e per la formazione. Queste informazioni includono il numero di serie del dispositivo, l'identificatore del prodotto Windows e un ID hardware. Usare Configuration Manager per raccogliere e segnalare queste informazioni. 

### <a name="prerequisites"></a>Prerequisiti
- Queste informazioni sul dispositivo si applicano solo ai client su Windows 10 versione 1703 e successive

### <a name="try-it-out"></a>Verifica
 Provare a completare le attività. Quindi inviare **Commenti e suggerimenti** dalla scheda **Home** della barra multifunzione.

1. Nell'area di lavoro **Monitoraggio** della console di Configuration Manager espandere il nodo **Report**, espandere **Report** e selezionare il nodo **Hardware - Generale**.
2. Eseguire il nuovo report **Informazioni sui dispositivi di Windows AutoPilot** e visualizzare i risultati. 
3. Nel visualizzatore report fare clic sull'icona **Esporta** e selezionare l'opzione **CSV (delimitato da virgole)** .
4. Dopo aver salvato il file, caricare i dati in Microsoft Store per le aziende e per la formazione. Per altre informazioni, vedere [Add devices in Microsoft Store for Business and Education](https://docs.microsoft.com/microsoft-store/add-profile-to-devices#add-devices-and-apply-autopilot-deployment-profile) (Aggiungere dispositivi in Microsoft Store per le aziende e per la formazione). 



## <a name="improvements-to-configuration-manager-policies-for-windows-defender-exploit-guard"></a>Miglioramenti ai criteri di Configuration Manager per Windows Defender Exploit Guard
<!-- 1356220 -->
Ulteriori impostazioni dei criteri per i componenti Riduzione della superficie di attacco e Accesso controllato alle cartelle sono state aggiunte in Configuration Manager per [Windows Defender Exploit Guard](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection).

**Nuove impostazioni per Accesso controllato alle cartelle**<br/>
Esistono due opzioni aggiuntive quando si configura l'accesso controllato alle cartelle: **Blocca solo i settori del disco** e **Controlla solo i settori del disco**. Queste due impostazioni consentono di abilitare Accesso controllato alle cartelle solo per i settori di avvio e non abilitano la protezione di cartelle specifiche o delle cartelle protette predefinite. 

**Nuove impostazioni per Riduzione della superficie di attacco**
- Usa la protezione avanzata da ransomware.
- Blocca il furto di credenziali dal sottosistema dell'autorità di protezione locale di Windows. 
- Blocca l'esecuzione dei file eseguibili a meno che non rispettino criteri di prevalenza, di validità o dell'elenco di elementi attendibili. 
- Blocca processi non attendibili e non firmati eseguiti da USB.



## <a name="microsoft-edge-browser-policies"></a>Criteri del browser Microsoft Edge
<!-- 1357310 -->
I clienti che usano il Web browser [Microsoft Edge](https://technet.microsoft.com/microsoft-edge/bb265256) in client Windows 10 ora possono creare un criterio delle impostazioni di conformità di Configuration Manager per configurare diverse impostazioni di Microsoft Edge. Questo criterio include attualmente le impostazioni seguenti:
- **Imposta il browser Microsoft Edge come predefinito**: configura l'impostazione dell'app predefinita di Windows 10 per il Web browser su Microsoft Edge.
- **Consenti l'elenco a discesa della barra degli indirizzi**: richiede Windows 10 versione 1703 o successiva. Per altre informazioni, vedere [Criterio del browser AllowAddressBarDropdown](/windows/client-management/mdm/policy-csp-browser#browser-allowaddressbardropdown).
- **Consenti la sincronizzazione dei Preferiti tra browser Microsoft**: richiede Windows 10 versione 1703 o successiva. Per altre informazioni, vedere [Criterio del browser SyncFavoritesBetweenIEAndMicrosoftEdge](/windows/client-management/mdm/policy-csp-browser#browser-syncfavoritesbetweenieandmicrosoftedge).
- **Consenti la cancellazione dei dati di esplorazione all'uscita**: richiede Windows 10 versione 1703 o successiva. Per altre informazioni, vedere [Criterio del browser ClearBrowsingDataOnExit](/windows/client-management/mdm/policy-csp-browser#browser-clearbrowsingdataonexit).
- **Consenti le intestazioni Do Not Track**: per altre informazioni, vedere [Criterio del browser AllowDoNotTrack](/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack).
- **Consenti riempimento automatico**: per altre informazioni, vedere [Criterio del browser AllowAutofill](/windows/client-management/mdm/policy-csp-browser#browser-allowautofill).
- **Consenti cookie**: per altre informazioni, vedere [Criterio del browser AllowCookies](/windows/client-management/mdm/policy-csp-browser#browser-allowcookies).
- **Consenti blocco popup**: per altre informazioni, vedere [Criterio del browser AllowPopups](/windows/client-management/mdm/policy-csp-browser#browser-allowpopups).
- **Consenti suggerimenti di ricerca nella barra degli indirizzi**: per altre informazioni, vedere [Criterio del browser AllowSearchSuggestionsinAddressBar](/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar).
- **Consenti l'invio di traffico Intranet a Internet Explorer**: per altre informazioni, vedere [Criterio del browser SendIntranetTraffictoInternetExplorer](/windows/client-management/mdm/policy-csp-browser#browser-sendintranettraffictointernetexplorer).
- **Consenti strumento per la gestione delle password**: per altre informazioni, vedere [Criterio del browser AllowPasswordManager](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager).
- **Consenti gli Strumenti di sviluppo**: per altre informazioni, vedere [Criterio del browser AllowDeveloperTools](/windows/client-management/mdm/policy-csp-browser#browser-allowdevelopertools).
- **Consenti le estensioni**: per altre informazioni, vedere [Criterio del browser AllowExtensions](/windows/client-management/mdm/policy-csp-browser#browser-allowextensions).

### <a name="prerequisites"></a>Prerequisiti
- Client Windows 10 aggiunto ad Azure Active Directory. 

### <a name="known-issues"></a>Problemi noti
- I dispositivi aggiunti a domini locali non possono applicare questo criterio in questa versione. Questo problema interessa anche i dispositivi aggiunti a domini Ibridi.

### <a name="try-it-out"></a>Verifica  
 Provare a completare le attività. Quindi inviare **Commenti e suggerimenti** dalla scheda **Home** della barra multifunzione.

**Creare il criterio**
1. Nella console di Configuration Manager passare all'area di lavoro **Asset e conformità**. Espandere **Impostazioni di conformità** e selezionare il nuovo nodo **Profili del browser Microsoft Edge**. Fare clic sull'opzione **Crea un criterio del browser Microsoft Edge** sulla barra multifunzione.
2. Specificare un nome per il criterio nel campo **Nome** e una descrizione facoltativa nel campo **Descrizione**, quindi fare clic su **Avanti**.
3. Nella pagina **Impostazioni** cambiare il valore delle impostazioni da includere nel criterio su **Configurato**, quindi fare clic su **Avanti**.
4. Nella pagina **Piattaforme supportate** selezionare le architetture e le versioni del sistema operativo a cui si applica il criterio, quindi fare clic su **Avanti**. 
5. Completare la procedura guidata.

**Distribuire il criterio**
1. Selezionare il criterio e fare clic sull'opzione **Distribuisci** sulla barra multifunzione.
2. Fare clic su **Sfoglia** per selezionare la raccolta utenti o dispositivi nella quale si vuole distribuire il criterio. 
3. Selezionare le opzioni aggiuntive eventualmente necessarie. Impostare la generazione di avvisi quando il criterio non è conforme. Impostare la pianificazione in base alla quale il client valuta la conformità del dispositivo al criterio.
4. Fare clic su **OK** per creare la distribuzione.

Come avviene con qualsiasi criterio delle impostazioni di conformità, il client monitora e aggiorna le impostazioni sulla pianificazione specificata. [Monitorare e creare report sulla conformità dei dispositivi](../../compliance/deploy-use/monitor-compliance-settings.md) nella console di Configuration Manager.



## <a name="report-for-default-browser-counts"></a>Report sul numero di browser predefiniti
<!-- 1357830 -->
È disponibile un nuovo report che mostra il numero di client con un Web browser specifico come impostazione predefinita di Windows. 

### <a name="known-issues"></a>Problemi noti
- Alla prima apertura del report è indicato solo il numero e non il valore di BrowserProgID. Per risolvere il problema, modificare la query per il report con la sintassi seguente:  
    `select BrowserProgId00 as BrowserProgId, Count(*) as Count`  
    `from DEFAULT_BROWSER_DATA as dbd`  
    `group by BrowserProgId00`

### <a name="try-it-out"></a>Verifica  
 Provare a completare le attività. Quindi inviare **Commenti e suggerimenti** dalla scheda **Home** della barra multifunzione.
1. Nell'area di lavoro **Monitoraggio** della console di **Configuration Manager** espandere il nodo **Report**, espandere **Report** e selezionare **Software - Società e prodotti**.
2. Eseguire il report **Numero di browser predefiniti**.

Usare il riferimento seguente per i valori BrowserProgID più comuni:
- **AppXq0fevzme2pys62n3e0fbqa7peapykr8v**: Microsoft Edge
- **IE.HTTP**: Microsoft Internet Explorer
- **ChromeHTML**: Google Chrome
- **OperaStable**: Opera Software
- **FirefoxURL-308046B0AF4A39CB**: Mozilla Firefox



## <a name="support-for-windows-10-arm64-devices"></a>Supporto per dispositivi ARM64 Windows 10
<!-- 1353704 -->
A partire da questa versione il client Gestione configurazione è supportato nei dispositivi ARM64 Windows 10. Le funzionalità di gestione client esistenti dovrebbero funzionare con questi nuovi dispositivi, ad esempio l'inventario hardware e software, gli aggiornamenti del software e la gestione delle applicazioni. La distribuzione del sistema operativo non è attualmente supportata. 

## <a name="changes-to-phased-deployments"></a>Modifiche alle distribuzioni in più fasi
<!-- 1357405 -->
Le distribuzioni in più fasi automatizzano un'implementazione del software coordinata e in sequenza in più raccolte. In questa versione Technical Preview la distribuzione guidata in più fasi può essere completata per le sequenze di attività nella console di amministrazione e vengono quindi create le distribuzioni. Tuttavia, la seconda fase non viene avviata automaticamente una volta soddisfatti i criteri di superamento della prima fase. La seconda fase può essere avviata manualmente con un'istruzione SQL.   

### <a name="try-it-out"></a>Verifica  
  Provare a completare le attività. Quindi inviare **Commenti e suggerimenti** dalla scheda **Home** della barra multifunzione.
 
**Creare una distribuzione in fasi per una sequenza di attività** </br>
1. Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi** e selezionare **Sequenze di attività**.
2. Fare clic con il pulsante destro del mouse su una sequenza di attività esistente e selezionare **Create Phased Deployment** (Crea distribuzione in fasi). 
3. Nella scheda **Generale** assegnare alla distribuzione in più fasi un nome e una descrizione (facoltativa), quindi selezionare **Crea automaticamente una distribuzione predefinita in due fasi**. 
4. Popolare i campi **Prima raccolta** e **Seconda raccolta**. Selezionare **Avanti**.
5. Nella scheda **Impostazioni** scegliere un'opzione per ogni impostazione di pianificazione. Al termine, selezionare **Avanti**. 
6. Nella scheda **Phases** (Fasi) modificare le fasi se necessario e fare clic su **Avanti**.
7. Confermare le selezioni nella scheda **Riepilogo** e fare clic su **Avanti** per continuare.
8. Una volta soddisfatti i criteri di superamento della prima fase, seguire le istruzioni per avviare la seconda fase con un'istruzione SQL.
 
**Avviare la seconda fase con un'istruzione SQL**
1. Identificare il valore di PhasedDeploymentID per la distribuzione creata con la query SQL seguente:<br/> `Select * from PhasedDeployment`
2. Eseguire l'istruzione seguente per avviare la fase di produzione:<br/> `UPDATE PhasedDeployment SET EvaluatePhasedDeployment = 1, Action = 3 WHERE PhasedDeploymentID = <Phased Deployment ID>`


## <a name="next-steps"></a>Passaggi successivi
Per informazioni sull'installazione o l'aggiornamento del ramo Technical Preview, vedere [Technical Preview per Configuration Manager](technical-preview.md).    
