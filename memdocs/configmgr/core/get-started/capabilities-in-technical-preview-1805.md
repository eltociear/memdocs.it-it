---
title: Technical Preview 1805
titleSuffix: Configuration Manager
description: Informazioni sulle nuove funzionalità disponibili in Configuration Manager Technical Preview versione 1805.
ms.date: 05/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7996b3eb-5259-483b-af40-adae2943d123
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 88234bb3117850bc3280242671ae459308a5262e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696029"
---
# <a name="capabilities-in-technical-preview-1805-for-configuration-manager"></a>Funzionalità della versione Technical Preview 1805 per Configuration Manager

*Si applica a: Configuration Manager (Technical Preview Branch)*

Questo articolo presenta le funzionalità disponibili nella Technical Preview per Configuration Manager, versione 1805. È possibile installare questa versione per aggiornare il sito delle anteprime tecniche aggiungendovi nuove funzionalità. 

Prima di installare questo aggiornamento, vedere l'articolo [Technical Preview](technical-preview.md). L'articolo consente di acquisire familiarità con i requisiti e le limitazioni generali per l'uso di una Technical Preview, con l'aggiornamento tra le versioni e con l'invio di commenti e suggerimenti.     


<!--  Known Issues Template
## Known Issues in this Technical Preview

### <a name="bkmk_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->



</br>

**Di seguito sono riportate le nuove funzionalità disponibili con questa versione.**  



## <a name="create-a-phased-deployment-with-manually-configured-phases-for-a-task-sequence"></a>Creare una distribuzione in più fasi con fasi configurate manualmente per una sequenza di attività
<!--1358148-->
È ora possibile [creare una distribuzione in più fasi](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md) con fasi configurate manualmente per una sequenza di attività. È possibile aggiungere fino a 10 fasi aggiuntive dalla scheda **Fasi** della procedura guidata Crea una distribuzione in più fasi. 


### <a name="try-it-out"></a>Verifica
Seguire le istruzioni per creare una distribuzione in più fasi in cui configurare manualmente tutte le fasi. Inviare quindi [commenti e suggerimenti](capabilities-in-technical-preview-1804.md#bkmk_feedback). 

1. Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi** e selezionare **Sequenze di attività**.  

2. Fare clic con il pulsante destro del mouse su una sequenza di attività esistente e selezionare **Create Phased Deployment** (Crea distribuzione in fasi).  

3. Nella scheda **Generale** assegnare alla distribuzione in più fasi un nome e una descrizione (facoltativa) e quindi selezionare **Configura manualmente tutte le fasi**.  

4. Nella scheda **Fasi** fare clic su **Aggiungi**.  

5. Specificare un **Nome** per la fase e quindi individuare la **Raccolta di fasi** di destinazione.  

6. Nella scheda **Impostazioni delle fasi** scegliere un'opzione per ogni impostazione di pianificazione e selezionare **Avanti** al termine.  

    - Criteri per l'esito positivo della fase precedente (questa opzione è disabilitata per la prima fase).
        - **Percentuale di esiti positivi della distribuzione**: specificare la percentuale di dispositivi che devono completare la distribuzione per i criteri per l'esito positivo della fase precedente.  

    - Condizioni per l'inizio di questa fase della distribuzione dopo l'esito positivo della fase precedente  
        - **Inizia automaticamente questa fase dopo un periodo di differimento (in giorni)** : scegliere il numero di giorni di attesa prima di iniziare la fase successiva dopo l'esito positivo della fase precedente. 
        - **Avvia manualmente questa fase della distribuzione**: non avviare questa fase automaticamente dopo l'esito positivo della fase precedente.  

    - Dopo avere incluso un dispositivo, installare il software
        - **Appena possibile**: imposta come scadenza per l'installazione nel dispositivo il momento in cui il dispositivo viene incluso.
        - **Ora della scadenza (rispetto all'ora in cui il dispositivo viene incluso)** : imposta la scadenza per l'installazione un determinato numero di giorni dopo l'inclusione del dispositivo.  
     
7. Completare la procedura guidata Impostazioni delle fasi.

8. Nella scheda **Fasi** della procedura guidata Crea una distribuzione in più fasi è ora possibile aggiungere, rimuovere, riordinare o modificare le fasi per questa distribuzione.  

9. Completare la procedura guidata Crea una distribuzione in più fasi.  



## <a name="cloud-distribution-point-support-for-azure-resource-manager"></a>Supporto del punto di distribuzione cloud per Azure Resource Manager
<!--1322209-->
Quando si crea un'istanza del [punto di distribuzione cloud](../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md), la procedura guidata consente ora di creare una **distribuzione Azure Resource Manager**. [Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) è una piattaforma moderna per la gestione di tutte le risorse di una soluzione come una singola entità detta [gruppo di risorse](/azure/azure-resource-manager/resource-group-overview#resource-groups). Quando si distribuisce un punto di distribuzione cloud con Azure Resource Manager, il sito usa Azure Active Directory (Azure AD) per autenticare e creare le risorse cloud necessarie. Questa distribuzione modernizzata non richiede il certificato di gestione classico di Azure.  

La procedura guidata per il punto di distribuzione cloud offre ancora l'opzione per una **distribuzione classica del servizio** tramite un certificato di gestione di Azure. Per semplificare la distribuzione e la gestione delle risorse, è consigliabile usare il modello di distribuzione Azure Resource Manager per tutti i nuovi punti di distribuzione cloud. Se possibile, ridistribuire i punti di distribuzione cloud esistenti tramite Resource Manager.

Configuration Manager non esegue la migrazione dei punti di distribuzione cloud classici esistenti nel modello di distribuzione Azure Resource Manager. Creare nuovi punti di distribuzione cloud usando distribuzioni di Azure Resource Manager e quindi rimuovere i punti di distribuzione cloud classici. 

> [!IMPORTANT]  
> Questa funzionalità non supporta i provider di servizi cloud di Azure. La distribuzione di punti di distribuzione cloud con Azure Resource Manager continua a usare il servizio cloud classico, non supportato dal provider di servizi cloud. Per altre informazioni, vedere [Available Azure services in Azure CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services) (servizi di Azure disponibili in Azure CSP).  


### <a name="prerequisites"></a>Prerequisiti  
- Integrazione con [Azure AD](../clients/deploy/deploy-clients-cmg-azure.md). L'individuazione utenti di Azure AD non è necessaria.  

- Stessi [requisiti di un punto di distribuzione cloud](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_requirements), ad eccezione del certificato di gestione di Azure.  


### <a name="try-it-out"></a>Verifica  
 Provare a completare le attività. Inviare quindi [commenti e suggerimenti](capabilities-in-technical-preview-1804.md#bkmk_feedback).

1. Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Servizi cloud** e selezionare **Punti di distribuzione del cloud**. Fare clic su **Crea punto di distribuzione cloud** sulla barra multifunzione.   

2. Nella pagina **Generale** selezionare **Modello di distribuzione Azure Resource Manager**. Fare clic su **Accedi** per eseguire l'autenticazione con un account amministratore della sottoscrizione di Azure. La procedura guidata compila automaticamente i campi rimanenti in base alle informazioni di sottoscrizione di Azure AD archiviate durante il prerequisito di integrazione. Se si hanno più sottoscrizioni, selezionare quella che si vuole usare. Fare clic su **Avanti**.  

3. Nella pagina **Impostazioni** specificare il **file del certificato** PKI server come di consueto. Questo certificato definisce il **nome di dominio completo del servizio** del punto di distribuzione cloud usato da Azure. Selezionare l'area in **Area** e quindi selezionare **Crea nuovo** o **Usa esistente** per il gruppo di risorse. Immettere il nome del nuovo gruppo di risorse o selezionare un gruppo di risorse esistente nell'elenco a discesa.  

4. Completare la procedura guidata.  

> [!NOTE]  
> Per l'app server Azure AD selezionata Azure assegna l'autorizzazione di **collaboratore** per la sottoscrizione.  

Monitorare lo stato della distribuzione del servizio con **cloudmgr.log** nel punto di connessione del servizio.



## <a name="take-actions-based-on-management-insights"></a>Intraprendere azioni in base alle informazioni dettagliate sulla gestione
<!--1357930-->
Alcune [informazioni dettagliate sulla gestione](../servers/manage/management-insights.md) offrono ora la possibilità di eseguire un'azione. A seconda della regola, questa azione presenta uno dei comportamenti seguenti:  

- Passare direttamente nella console al nodo in cui è possibile eseguire ulteriori azioni. Ad esempio, se le informazioni dettagliate sulla gestione consigliano di modificare un'impostazione client, l'opzione per eseguire un'azione consente di passare al nodo Impostazioni client. È possibile eseguire ulteriori azioni modificando l'impostazione predefinita o un oggetto impostazioni client personalizzato.  

- Passare a una visualizzazione filtrata in base a una query. Ad esempio, eseguire l'azione per la regola delle raccolte vuote mostra semplicemente queste raccolte nell'elenco delle raccolte. Qui è possibile eseguire ulteriori azioni, ad esempio eliminare una raccolta o modificarne le regole di appartenenza.  

Le regole per le informazioni dettagliate sulla gestione seguenti includono azioni in questa versione:
- Sicurezza
    - Versioni client dell'antimalware non supportate
- Software Center
    - Usare la nuova versione di Software Center
- Applicazioni
    - Applicazioni senza distribuzioni
- Gestione semplificata
    - Versioni client non CB
- Raccolte
    - Raccolte vuote 
- Servizi cloud
    - Aggiorna i client alla versione più recente di Windows 10



## <a name="transition-device-configuration-workload-to-intune-using-co-management"></a>Transizione del carico di lavoro di configurazione dei dispositivi a Intune usando la co-gestione
<!--1357903-->

È ora possibile eseguire la transizione del carico di lavoro di configurazione dei dispositivi da Configuration Manager a Intune dopo aver abilitato la co-gestione. La transizione di questo carico di lavoro consente di usare Intune per distribuire criteri MDM, pur continuando a usare Configuration Manager per la distribuzione delle applicazioni. 

Per eseguire la transizione di questo carico di lavoro, passare alla pagina delle proprietà di co-gestione e spostare la barra del dispositivo di scorrimento da Configuration Manager su **Pilota** o **Tutte**. Per altre informazioni, vedere [Co-gestione per dispositivi Windows 10](../../comanage/overview.md).

> [!Note]  
> Con lo spostamento di questo carico di lavoro vengono spostati anche i carichi di lavoro **Accesso alla risorsa** e **Endpoint Protection**, che sono un subset del carico di lavoro di configurazione dei dispositivi.

Dopo la transizione di questo carico di lavoro, è comunque possibile continuare a distribuire le impostazioni da Configuration Manager ai dispositivi con co-gestione, anche se Intune è l'autorità di configurazione del dispositivo. Questa eccezione può essere usata per configurare le impostazioni richieste dall'organizzazione, ma non ancora disponibili in Intune. Specificare questa eccezione in una linea di base di configurazione di Configuration Manager. Abilitare l'opzione per **applicare sempre la linea di base anche per i client con co-gestione** quando si crea la linea di base o nella scheda **Generale** delle proprietà di una linea di base esistente. 



## <a name="enable-distribution-points-to-use-network-congestion-control"></a>Abilitare punti di distribuzione per l'uso del controllo di congestione della rete
<!--1358112-->

La funzionalità LEDBAT (Low Extra Delay Background Transport) di Windows Server consente di gestire i trasferimenti di rete in background. Per i punti di distribuzione in esecuzione in versioni supportate di Windows Server, è possibile abilitare un'opzione che consente di regolare il traffico di rete. I client usano la larghezza di banda di rete solo quando è disponibile. 

Per altre informazioni su Windows LEDBAT, vedere il post di blog [New transport advancements](https://blogs.technet.microsoft.com/networking/2016/07/18/announcing-new-transport-advancements-in-the-anniversary-update-for-windows-10-and-windows-server-2016/) (Nuovi miglioramenti per il trasporto).


### <a name="prerequisites"></a>Prerequisiti
- Un punto di distribuzione in Windows Server, versione 1709.  

- Non è presente alcun prerequisito client.<!--SCCMDocs issue 699-->  


### <a name="try-it-out"></a>Verifica
 Provare a completare le attività. Inviare quindi [commenti e suggerimenti](capabilities-in-technical-preview-1804.md#bkmk_feedback).

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**. Selezionare il nodo **Punti di distribuzione**. Selezionare il punto di distribuzione di destinazione e fare clic su **Proprietà** sulla barra multifunzione.  

2. Nella scheda **Generale** abilitare l'opzione **Regola la velocità del download per usare la larghezza di banda di rete inutilizzata (Windows LEDBAT)** .  



## <a name="cloud-management-dashboard"></a>Dashboard di gestione del cloud
<!--1358461-->
Il nuovo **dashboard di gestione del cloud** offre una visualizzazione centralizzata per l'utilizzo di Cloud Management Gateway (CMG). Dopo l'onboarding del sito con Azure AD, nel dashboard vengono visualizzati anche dati sugli utenti e i dispositivi del cloud.  

Lo screenshot seguente illustra una parte del dashboard di gestione del cloud che mostra due dei riquadri disponibili:  
![Riquadri del dashboard di gestione del cloud: traffico CMG e Client online correnti](media/1358461-cmg-dashboard.png)

Questa funzionalità include anche l'**analizzatore della connessione CMG** per verifiche in tempo reale a supporto della risoluzione dei problemi. L'utilità inclusa nella console controlla lo stato corrente del servizio e il canale di comunicazione dal punto di connessione CMG a tutti i punti di gestione che consentono il traffico CMG.


### <a name="prerequisites"></a>Prerequisiti
- Un [gateway di gestione cloud](../clients/manage/cmg/plan-cloud-management-gateway.md) attivo usato dai client basati su Internet.  

- Onboarding del sito in [servizi di Azure](../servers/deploy/configure/azure-services-wizard.md) per la gestione del cloud.  


### <a name="try-it-out"></a>Verifica
Provare a completare le attività. Inviare quindi [commenti e suggerimenti](capabilities-in-technical-preview-1804.md#bkmk_feedback).

#### <a name="cloud-management-dashboard"></a>Dashboard di gestione del cloud

Nella console di Configuration Manager passare all'area di lavoro **Monitoraggio**. Selezionare il nodo **Gestione cloud** e visualizzare i riquadri del dashboard.  

#### <a name="cmg-connection-analyzer"></a>Analizzatore della connessione CMG

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**. Espandere **Servizi cloud** e selezionare **Gateway di gestione cloud**.  

2. Selezionare l'istanza di CMG di destinazione e quindi selezionare **Analizzatore della connessione** sulla barra multifunzione.  

3. Nella finestra dell'analizzatore della connessione CMG selezionare una delle opzioni seguenti per l'autenticazione nel servizio:  

     1. **Utente di Azure AD**: usare questa opzione per simulare la comunicazione di un'identità utente basata sul cloud connessa a un dispositivo Windows 10 aggiunto ad Azure AD. Fare clic su **Accedi** per immettere le credenziali per questo account utente di Azure AD in modo sicuro.  

     2. **Certificato client**: usare questa opzione per simulare la comunicazione di un client di Configuration Manager con un [certificato di autenticazione client](../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_clientauth).  

4. Fare clic su **Avvia** per avviare l'analisi. I risultati vengono visualizzati nella finestra dell'analizzatore. Selezionare una voce per visualizzare ulteriori dettagli nel campo Descrizione.  



## <a name="cmpivot"></a>CMPivot
<!--1358456-->
Configuration Manager ha sempre fornito un archivio centralizzato di grandi dimensioni per i dati dei dispositivi, usato dai clienti per i report. Tuttavia, la validità di questi dati è limitata all'ultima raccolta dai client. 

CMPivot è una nuova utilità inclusa nella console che consente l'accesso allo stato in tempo reale dei dispositivi nell'ambiente in uso. Esegue immediatamente una query su tutti i dispositivi connessi nella raccolta di destinazione e restituisce i risultati. È quindi possibile filtrare e raggruppare questi dati nello strumento. La disponibilità di dati in tempo reale dai client online consente di rispondere alle domande aziendali, risolvere i problemi e rispondere agli eventi imprevisti di sicurezza in modo più veloce.

Ad esempio, perla [mitigazione delle vulnerabilità del canale laterale di esecuzione speculativa](https://techcommunity.microsoft.com/t5/configuration-manager-blog/additional-guidance-to-mitigate-speculative-execution-side/ba-p/274974), uno dei requisiti prevede l'aggiornamento del BIOS di sistema. È possibile usare CMPivot per eseguire rapidamente query sulle informazioni del BIOS di sistema e individuare i client non conformi. 

In questo screenshot, CMPivot visualizza due versioni del BIOS separate con un dispositivo ognuna. È possibile usare questa query di esempio per provare CMPivot:  
`Registry('hklm:\\Hardware\\Description\\System\\BIOS') | where (Property == 'BIOSVersion') | summarize dcount( Device ) by Value`  

![Finestra CMPivot con una query di esempio per BIOSVersion](media/1358456-cmpivot-biosversion.png)

È possibile fare clic sul conteggio dei dispositivi per eseguire il drill-down e visualizzare i dispositivi specifici. Quando si visualizzano i dispositivi in CMPivot, è possibile fare clic con il pulsante destro del mouse su un dispositivo e scegliere le [azioni di notifica client](../clients/manage/manage-clients.md#BKMK_ManagingClients_DevicesNode) seguenti:
- Esegui script
- Controllo remoto
- Esplora inventario risorse

Facendo clic con il pulsante destro del mouse su un dispositivo specifico, è anche possibile trasformare tramite Pivot la visualizzazione del dispositivo specifico in base a uno degli attributi seguenti:
- Comandi di avvio automatico
- Prodotti installati
- Processes
- Servizi
- Utenti
- Connessioni attive
- Aggiornamenti mancanti

### <a name="prerequisites"></a>Prerequisiti
- I client di destinazione devono essere aggiornati alla versione più recente.  

- L'amministratore di Configuration Manager deve avere le autorizzazioni per l'esecuzione di script. Per altre informazioni, vedere [Creare ruoli di sicurezza per gli script](../../apps/deploy-use/create-deploy-scripts.md#bkmk_ScriptRoles).  

### <a name="try-it-out"></a>Verifica
Provare a completare le attività. Inviare quindi [commenti e suggerimenti](capabilities-in-technical-preview-1804.md#bkmk_feedback).

1. Nella console di Configuration Manager passare all'area di lavoro **Asset e conformità** e selezionare **Raccolte dispositivi**. Selezionare una raccolta di destinazione e fare clic su **Avvia CMPivot** sulla barra multifunzione per avviare lo strumento.  

2. L'interfaccia fornisce ulteriori informazioni sull'uso dello strumento. 
     - È possibile immettere manualmente le stringhe di query nella parte superiore oppure fare clic sui collegamenti nella documentazione in linea.
     - Fare clic su una delle **Entità** per aggiungerla alla stringa di query. 
     - I collegamenti per **Operatori tabella**, **Funzioni di aggregazione** e **Funzioni scalari** consentono di aprire la documentazione di riferimento del linguaggio nel Web browser. CMPivot usa lo stesso linguaggio di query di [Azure Log Analytics](https://docs.microsoft.com/azure/kusto/query/).



## <a name="improved-secure-client-communications"></a>Comunicazioni client sicure migliorate
<!--1356889,1358228,1358460-->
L'uso delle comunicazioni HTTPS è consigliato per tutti i percorsi di comunicazione di Configuration Manager, ma può essere difficile per alcuni clienti a causa del sovraccarico di gestione dei certificati PKI. L'introduzione dell'integrazione di Azure Active Directory (Azure AD) riduce alcuni ma non tutti i requisiti per i certificati. 

Questa versione include miglioramenti per le modalità di comunicazione dei client con i sistemi del sito. Questi miglioramenti hanno due obiettivi principali:  

- Proteggere le comunicazioni client senza dover usare certificati di autenticazione server PKI.  

- I client possono accedere in modo sicuro al contenuto dai punti di distribuzione senza la necessità di un account di accesso alla rete.  

> [!Note]  
> I certificati PKI rimangono un'opzione valida per i clienti che vogliono usarli.  


### <a name="scenarios"></a><a name="bkmk_token"></a> Scenari
Gli scenari seguenti traggono vantaggio da questi miglioramenti:  

#### <a name="scenario-1-client-to-management-point"></a><a name="bkmk_token1"></a> Scenario 1: Da client a punto di gestione
<!--1356889-->
I [dispositivi aggiunti ad Azure AD](/azure/active-directory/devices/concept-azure-ad-join) possono comunicare tramite un Cloud Management Gateway (CMG) con un punto di gestione configurato per HTTP. Il server del sito genera un certificato per il punto di gestione in modo che possa comunicare tramite un canale sicuro.   

> [!Note]  
> Questo comportamento è cambiato rispetto a Configuration Manager Current Branch versione 1802, che richiede un punto di gestione abilitato per HTTPS per questo scenario. Per altre informazioni, vedere [Abilitare i punti di gestione per HTTPS](../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_mphttps).  

#### <a name="scenario-2-client-to-distribution-point"></a><a name="bkmk_token2"></a> Scenario 2: Da client a punto di distribuzione
<!--1358228-->
Un gruppo di lavoro o un client aggiunto ad Azure AD può scaricare contenuto tramite un canale sicuro da un punto di distribuzione configurato per HTTP.   

#### <a name="scenario-3-azure-ad-device-identity"></a><a name="bkmk_token3"></a> Scenario 3: Identità del dispositivo di Azure AD 
<!--1358460-->
Un dispositivo aggiunto ad Azure AD o un [dispositivo di Azure AD ibrido](/azure/active-directory/devices/concept-azure-ad-join-hybrid) senza un utente di Azure AD connesso può comunicare in modo sicuro con il relativo sito assegnato. L'identità del dispositivo basata sul cloud è ora sufficiente per l'autenticazione con CMG e il punto di gestione.  


### <a name="prerequisites"></a>Prerequisiti  

- Un punto di gestione configurato per connessioni client HTTP. Impostare questa opzione nella scheda **Generale** delle proprietà del ruolo del sistema del sito.  

- Un punto di distribuzione configurato per connessioni client HTTP. Impostare questa opzione nella scheda **Generale** delle proprietà del ruolo del sistema del sito. Non abilitare l'opzione **Consenti connessione anonima dei client**.  

- Un Cloud Management Gateway.  

- Eseguire l'onboarding del sito in Azure AD per la gestione del cloud.  

    - Se questo prerequisito per il sito è già soddisfatto, è necessario aggiornare l'applicazione Azure AD. Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Servizi cloud** e selezionare **Tenant di Azure Active Directory**. Selezionare il tenant di Azure AD, selezionare l'applicazione Web nel riquadro **Applicazioni** e quindi fare clic su **Aggiornare le impostazioni dell'applicazione** sulla barra multifunzione.  

- Un client che esegue Windows 10 versione 1803 e aggiunto ad Azure AD. (Questo requisito è tecnicamente solo per lo [Scenario 3](#bkmk_token3).) 


### <a name="try-it-out"></a>Verifica
Provare a completare le attività. Inviare quindi [commenti e suggerimenti](capabilities-in-technical-preview-1804.md#bkmk_feedback).

1. Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Configurazione del sito** e selezionare **Siti**. Selezionare il sito e fare clic su **Proprietà** sulla barra multifunzione.  

2. Passare alla scheda **Comunicazione computer client**. Selezionare l'opzione **HTTPS o HTTP** e quindi abilitare la nuova opzione **Use Configuration Manager-generated certificates for HTTP site systems** (Usa certificati generati da Configuration Manager per i sistemi del sito HTTP).  

Vedere l'[elenco di scenari](#bkmk_token) precedenti per la convalida.

> [!Tip]
> In questa versione, il punto di gestione può richiedere fino a 30 minuti per la ricezione e la configurazione del nuovo certificato dal sito.

È possibile visualizzare questi certificati nella console di Configuration Manager. Nell'area di lavoro **Amministrazione** espandere **Sicurezza** e selezionare il nodo **Certificati**. Cercare il certificato radice **Emissione SMS**, nonché i certificati di ruolo del server del sito emessi dalla radice di emissione SMS.


### <a name="known-issues"></a>Problemi noti
- Non è possibile visualizzare in Software Center alcuna applicazione assegnata come disponibile.  

- Per gli scenari di distribuzione del sistema operativo è ancora necessario l'account di accesso alla rete.  

- Se si abilita e disabilita l'opzione **Use Configuration Manager-generated certificates for HTTP site systems** (Usa certificati generati da Configuration Manager per i sistemi del sito HTTP) ripetutamente e velocemente, è possibile che il certificato non venga associato in modo corretto ai ruoli del sistema del sito. Nessun certificato emesso dal certificato "Emissione SMS" viene associato a un sito Web in Windows Server Internet Information Services (IIS). Per risolvere questo problema, eliminare tutti i certificati emessi da "Emissione SMS" dall'archivio certificati **SMS** in Windows e quindi riavviare il servizio smsexec.



## <a name="improvements-for-enabling-third-party-software-update-support"></a>Miglioramenti all'abilitazione del supporto degli aggiornamenti software di terze parti
<!--1357605-->
Grazie ai commenti e suggerimenti dei clienti in UserVoice in merito al [supporto di aggiornamenti software di terze parti](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8803711-3rd-party-patching-scup-integration-with-sccm-co), questa versione migliora ulteriormente l'integrazione con System Center Updates Publisher (SCUP). In Configuration Manager Technical Preview [versione 1803](capabilities-in-technical-preview-1803.md#enable-third-party-software-update-support-on-clients) è stata aggiunta la possibilità di leggere il certificato da WSUS per gli aggiornamenti di terze parti e quindi distribuire tale certificato ai client. È però ancora necessario usare lo strumento SCUP per creare e gestire il certificato per la firma degli aggiornamenti software di terze parti.

In questa versione, è possibile abilitare il sito di Configuration Manager per la configurazione automatica del certificato. Il sito comunica con WSUS per generare un certificato a questo scopo. Configuration Manager continua quindi a distribuire tale certificato ai client. Questa iterazione elimina la necessità di usare lo strumento SCUP per creare e gestire il certificato. 

Per altre informazioni sull'uso generale dello strumento SCUP, vedere [System Center Updates Publisher](../../sum/tools/updates-publisher.md).

### <a name="prerequisites"></a>Prerequisiti
- Abilitare e distribuire l'impostazione client **Abilita gli aggiornamenti software di terze parti** nel gruppo **Aggiornamenti software**.
- Se WSUS è in un server separato dal punto di aggiornamento software, è necessario eseguire una delle operazioni seguenti nel server WSUS remoto:
    - Abilitare il servizio Registro di sistema remoto in Windows  
    Oppure
    - Nella chiave del Registro di sistema `HKLM\Software\Microsoft\Update Services\Server\Setup` creare un nuovo valore DWORD denominato **EnableSelfSignedCertificates** con il valore `1`. 

### <a name="try-it-out"></a>Verifica
Provare a completare le attività. Inviare quindi [commenti e suggerimenti](capabilities-in-technical-preview-1804.md#bkmk_feedback).

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**. Espandere **Configurazione del sito** e selezionare **Siti**. Selezionare il sito di livello superiore, fare clic su **Configura componenti del sito** sulla barra multifunzione e selezionare **Punto di aggiornamento software**.  

2. Passare alla scheda **Aggiornamenti di terze parti**. Selezionare l'opzione **Abilita gli aggiornamenti software di terze parti** e quindi selezionare l'opzione **Configuration Manager automatically manages the certificate** (Certificato gestito automaticamente da Configuration Manager).

3. Continuare con il resto del flusso di lavoro SCUP tipico per l'importazione di un catalogo di aggiornamenti software di terze parti e quindi distribuire gli aggiornamenti ai client.



## <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Miglioramenti alla sequenza di attività di aggiornamento sul posto di Windows 10
<!--1358500-->

Il modello di sequenza di attività predefinita per l'aggiornamento sul posto di Windows 10 include ora un altro nuovo gruppo con azioni consigliate da aggiungere in caso di esito negativo del processo di aggiornamento. Queste azioni facilitano la risoluzione dei problemi.

### <a name="new-groups-under-run-actions-on-failure"></a>Nuovi gruppi in **Esegui azioni in caso di errore**
- **Raccogli registri**: per raccogliere i log dal client, aggiungere passaggi in questo gruppo. 
    - Una pratica comune prevede la copia dei file di log in una condivisione di rete. Per stabilire questa connessione, usare il passaggio [Connetti alla cartella di rete](../../osd/understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder). 
    - Per eseguire l'operazione di copia, usare un'utilità o uno script personalizzato con il passaggio [Esegui riga di comando](../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) oppure [Esegui script PowerShell](../../osd/understand/task-sequence-steps.md#BKMK_RunPowerShellScript).
    - I file da raccogliere potrebbero includere i log seguenti:  
         `%_SMSTSLogPath%\*.log`   
         `%SystemDrive%\$Windows.~BT\Sources\Panther\setupact.log`  
    - Per altre informazioni su setupact.log e altri log di Installazione di Windows, vedere [Windows Setup Log files](/windows/deployment/upgrade/log-files) (File di log di Installazione di Windows).
    - Per altre informazioni sui log client di Configuration Manager, vedere [Log client di Configuration Manager](../plan-design/hierarchy/log-files.md#BKMK_ClientLogs).
    - Per altre informazioni su_SMSTSLogPath e altre variabili utili, vedere [Variabili predefinite della sequenza di attività](../../osd/understand/task-sequence-variables.md).

- **Esegui gli strumenti di diagnostica**: per eseguire strumenti di diagnostica aggiuntivi, aggiungere passaggi in questo gruppo. Questi strumenti devono essere automatizzati per la raccolta di informazioni aggiuntive dal sistema il prima possibile dopo l'errore.
    - Uno di questi strumenti è [SetupDiag](/windows/deployment/upgrade/setupdiag) di Windows. È uno strumento di diagnostica autonomo che è possibile usare per ottenere i dettagli sui motivi per cui un aggiornamento a Windows 10 non è riuscito.
         - In Configuration Manager [creare un pacchetto](../../apps/deploy-use/packages-and-programs.md#create-a-package-and-program) per lo strumento.
         - Aggiungere un passaggio [Esegui riga di comando](../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) a questo gruppo della sequenza di attività. Usare l'opzione **Pacchetto** per fare riferimento allo strumento. La stringa seguente è un esempio di **Riga di comando**:  
             `SetupDiag.exe /Output:"%_SMSTSLogPath%\SetupDiagResults.log" /Mode:Online`



## <a name="cmtrace-installed-with-client"></a>Installazione di CMTrace con il client
<!--1357971-->

Lo strumento per la visualizzazione di log CMTrace viene ora installato automaticamente insieme al client di Configuration Manager. Viene aggiunto alla directory di installazione del client, che per impostazione predefinita è `%WinDir%\ccm\cmtrace.exe`.

> [!Note]  
> CMTrace *non* viene registrato automaticamente in Windows per l'apertura dei file con estensione log.



## <a name="improvement-to-the-configuration-manager-console"></a>Miglioramento della console di Configuration Manager
<!--1358202-->
È stato introdotto il miglioramento seguente per la console di Configuration Manager:

- Gli elenchi di dispositivi in Asset e conformità, Dispositivi, ora visualizzano l'utente attualmente connesso per impostazione predefinita. Questo valore è aggiornato quanto lo [stato del client](../clients/manage/monitor-clients.md#bkmk_indStatus). Il valore viene cancellato quando l'utente si disconnette. Se nessun utente è connesso, il valore è vuoto. 

### <a name="known-issues"></a>Problemi noti
Il valore dell'utente attualmente connesso è vuoto nel nodo Dispositivi o quando si visualizza un elenco di dispositivi nel nodo Raccolte dispositivi. Per risolvere questo problema, scaricare questo [script SQL](https://gallery.technet.microsoft.com/ConfigMgr-1805-BgbUpdateLiv-306ff46c). Eseguire sp_BgbUpdateLiveData.sql nel server di database del sito e quindi riavviare i servizi smsexec e sms_notification_server nel punto di gestione.<!--514471-->



## <a name="improvements-to-console-feedback"></a>Miglioramenti alla funzione della console relativa a commenti e suggerimenti
<!--1357542-->
Questa versione include i miglioramenti seguenti per il nuovo meccanismo per l'invio di [commenti e suggerimenti](capabilities-in-technical-preview-1804.md#bkmk_feedback)nella console di Configuration Manager:  

- La finestra di dialogo per l'invio di commenti e suggerimenti memorizza ora le impostazioni precedenti, ad esempio le opzioni selezionate e l'indirizzo di posta elettronica.  

- È ora supportato l'invio di commenti e suggerimenti offline. È possibile salvare i commenti e i suggerimenti dalla console e quindi caricarli per Microsoft da un sistema connesso a internet. Usare il nuovo strumento per il caricamento dei commenti e suggerimenti offline disponibile in `cd.latest\SMSSETUP\Tools\UploadOfflineFeedback\UploadOfflineFeedback.exe`. Per visualizzare le opzioni della riga di comando disponibili e obbligatorie, eseguire lo strumento con l'opzione `--help`. Il sistema connesso deve avere accesso a **petrol.office.microsoft.com**.

### <a name="known-issues"></a>Problemi noti
Quando si usa **Invia smile** oppure **Invia faccia imbronciata** dalla console in un computer con connettività Internet, può essere restituito il messaggio seguente: "Si è verificato un errore durante l'invio dei commenti e suggerimenti." Se si fa clic su **Altri dettagli** viene visualizzato il testo seguente: `{"Message":""}`. Questo errore è dovuto a un problema noto con la risposta dal sistema di commenti e suggerimenti di back-end. È possibile ignorare l'errore. Microsoft ha ricevuto comunque i commenti e suggerimenti. (Se nei dettagli viene visualizzato un messaggio diverso, usare l'opzione per l'invio di commenti e suggerimenti offline per riprovare a inviarli in un secondo momento.)



## <a name="improvements-to-pxe-enabled-distribution-points"></a>Miglioramenti ai punti di distribuzione che supportano PXE
<!--1357580-->

Questa versione include i miglioramenti aggiuntivi seguenti quando si usa l'opzione [**Abilita un risponditore PXE senza i Servizi di distribuzione Windows**](capabilities-in-technical-preview-1802.md#improvements-to-pxe-enabled-distribution-points) in un punto di distribuzione:  

- Le regole di Windows Firewall vengono create automaticamente nel punto di distribuzione quando si abilita questa opzione  
- Miglioramenti per la registrazione dei componenti



## <a name="improvement-to-hardware-inventory-for-large-integer-values"></a>Miglioramento dell'inventario hardware per valori interi di grandi dimensioni
<!--1357880-->
L'inventario hardware ha attualmente un limite per numeri interi maggiori di 4.294.967.296 (2^32). Questo limite può essere raggiunto per attributi come le dimensioni delle unità disco rigido in byte. Il punto di gestione non elabora valori interi oltre questo limite, pertanto nessun valore viene archiviato nel database. In questa versione, il limite è stato aumentato a 18.446.744.073.709.551.616 (2^64). 

Per una proprietà con un valore che non cambia, ad esempio le dimensioni totali del disco, il valore potrebbe non essere immediatamente visibile dopo l'aggiornamento del sito. La maggior parte dell'inventario hardware è un report delta. Il client invia solo valori che cambiano. Per risolvere questo problema, aggiungere un'altra proprietà alla stessa classe. Con questa azione, il client aggiorna tutte le proprietà nella classe modificata. 



## <a name="improvement-to-wsus-maintenance"></a>Miglioramento della manutenzione di WSUS
<!--1357898-->

La pulizia guidata WSUS ora rifiuta gli aggiornamenti scaduti o sostituiti in base alle regole di sostituzione. Queste regole sono definite nelle proprietà del componente del punto di aggiornamento software.

### <a name="try-it-out"></a>Verifica
Provare a completare le attività. Inviare quindi [commenti e suggerimenti](capabilities-in-technical-preview-1804.md#bkmk_feedback).

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**. Espandere **Configurazione del sito** e selezionare **Siti**. Selezionare il sito di livello superiore, fare clic su **Configura componenti del sito** sulla barra multifunzione e selezionare **Punto di aggiornamento software**.  

2. Passare alla scheda **Regole di sostituzione**. Abilitare l'opzione **Eseguire pulizia guidata WSUS**. Specificare il comportamento di sostituzione desiderato.  

3. Esaminare il file Wsyncmgr.log.



## <a name="improvement-to-support-for-cng-certificates"></a>Miglioramento del supporto per i certificati CNG
<!--1357314-->
In questa versione, è possibile usare i [certificati CNG](../plan-design/network/cng-certificates-overview.md) per i ruoli del server abilitati per HTTPS aggiuntivi seguenti:  
- Punto di registrazione certificati, incluso il server del servizio Registrazione dispositivi di rete con il modulo di criteri di Configuration Manager



## <a name="next-steps"></a>Passaggi successivi
Per informazioni sull'installazione o l'aggiornamento del ramo Technical Preview, vedere [Technical Preview per Configuration Manager](technical-preview.md).    
