---
title: Distribuire applicazioni
titleSuffix: Configuration Manager
description: Creare o simulare la distribuzione di un'applicazione a una raccolta di utenti o dispositivi
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a7bbf395a5de98459043609986e51647362e7a0b
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075337"
---
# <a name="deploy-applications-with-configuration-manager"></a>Distribuire applicazioni con Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Creare o simulare la distribuzione di un'applicazione a una raccolta di utenti o dispositivi in Configuration Manager. La distribuzione specifica istruzioni per il client di Configuration Manager su come e quando installare il software.

Prima di distribuire un'applicazione, creare almeno un tipo di distribuzione per l'applicazione. Per altre informazioni, vedere [Create applications](create-applications.md) (Creare le applicazioni).

A partire dalla versione 1906, è possibile creare un gruppo di applicazioni da inviare a un utente o a una raccolta di dispositivi come singola distribuzione. Per altre informazioni, vedere [Creare gruppi di applicazioni](create-app-groups.md).

È anche possibile simulare la distribuzione di un'applicazione. La simulazione verifica l'applicabilità di una distribuzione senza installare o disinstallare l'applicazione. Una distribuzione simulata esegue una valutazione del metodo di rilevamento, dei requisiti e delle dipendenze per un tipo di distribuzione e segnala i risultati nel nodo **Distribuzioni** dell'area di lavoro **Monitoraggio**. Per altre informazioni, vedere [Simulare distribuzioni di applicazioni ](simulate-application-deployments.md).

> [!Note]
> È possibile simulare la distribuzione solo di applicazioni necessarie, ma non di pacchetti o aggiornamenti software.
>
> I dispositivi registrati con MDM non supportano le distribuzioni simulate, l'esperienza utente o le impostazioni di pianificazione.



## <a name="deploy-an-application"></a><a name="bkmk_deploy"></a> Distribuire un'applicazione

1. Nella console di Configuration Manager passare all'area di lavoro **Raccolta software**, espandere **Gestione applicazioni** e selezionare il nodo **Applicazioni** o **Gruppi di applicazioni**.

2. Selezionare un'applicazione o un gruppo di applicazioni nell'elenco da distribuire. Sulla barra multifunzione fare clic su **Distribuisci**.  

> [!Note]  
> Quando si visualizzano le proprietà di una distribuzione esistente, le sezioni seguenti corrispondono alle schede della finestra delle proprietà della distribuzione:  
>
> - [Generalee](#bkmk_deploy-general)
> - [Contenuto](#bkmk_deploy-content)
> - [Impostazioni distribuzione](#bkmk_deploy-settings)
> - [Pianificazione](#bkmk_deploy-sched)
> - [Esperienza utente](#bkmk_deploy-ux)
> - [Avvisi](#bkmk_deploy-alerts)


### <a name="deployment-general-information"></a><a name="bkmk_deploy-general"></a> Informazioni della scheda **Generale** della distribuzione

Nella pagina **Generale** della Distribuzione guidata del software specificare le seguenti informazioni:  

- **Software**: visualizza l'applicazione da distribuire. Fare clic su **Sfoglia** per selezionare un'altra applicazione.  

- **Raccolta**: Fare clic su **Sfoglia** per selezionare la raccolta in cui distribuire l'applicazione.  

- **Utilizza gruppi di punti di distribuzione predefiniti associati a questa raccolta**: archivia il contenuto dell'applicazione nel gruppo di punti di distribuzione predefinito della raccolta. Se la raccolta selezionata non è stata associata a un gruppo di punti di distribuzione, l'opzione è disattivata.  

- **Distribuisci automaticamente contenuto per dipendenze**: se uno dei tipi di distribuzione dell'applicazione ha dipendenze, il sito invia anche il contenuto dell'applicazione dipendente ai punti di distribuzione.  

    >[!Note]  
    > Se l'applicazione dipendente viene aggiornata dopo la distribuzione dell'applicazione primaria, il sito non distribuisce automaticamente il nuovo contenuto per la dipendenza.  

- **Commenti (facoltativo)** : Facoltativamente, immettere una descrizione per la distribuzione.  


### <a name="deployment-content-options"></a><a name="bkmk_deploy-content"></a> Opzioni del **Contenuto** per la distribuzione

Nella pagina **Contenuto** fare clic su **Aggiungi** per distribuire il contenuto per questa applicazione a un punto di distribuzione o a un gruppo di punti di distribuzione.

Se è stata selezionata l'opzione **Utilizza gruppi di punti di distribuzione predefiniti associati a questa raccolta** nella pagina Generale, questa opzione viene popolata automaticamente. Solo un membro del ruolo di sicurezza **Amministratore applicazione** può modificarlo.

Se il contenuto dell'applicazione è già distribuito, viene visualizzato qui.


### <a name="deployment-settings"></a><a name="bkmk_deploy-settings"></a> **Impostazioni di distribuzione**

Nella pagina **Impostazioni distribuzione** specificare le informazioni seguenti:  

- **Azione**: usare l'elenco a discesa per indicare se la distribuzione deve **installare** o **disinstallare** l'applicazione.  

    > [!NOTE]  
    > Se si crea una distribuzione per **installare** un'app e un'altra distribuzione per **disinstallare** la stessa app nello stesso dispositivo, la distribuzione di **installazione**  avrà la priorità.  

    Non è possibile modificare l'azione di una distribuzione dopo averla creata.  

- **Scopo**: dall'elenco a discesa scegliere una delle seguenti opzioni:  

  - **Disponibile**: l'utente visualizza l'applicazione in Software Center. Può eseguire l'installazione su richiesta.  

  - **Richiesto**: il client installa automaticamente l'app in base alla pianificazione configurata. Se l'applicazione non è nascosta, un utente può verificarne lo stato di distribuzione. Gli utenti possono anche usare Software Center per installare l'applicazione prima della scadenza.  

    > [!NOTE]  
    > Quando si imposta l'azione di distribuzione su **Disinstalla**, lo scopo della distribuzione viene impostato automaticamente su **Richiesto**. Non è possibile modificare questo comportamento.  

- **Consenti agli utenti finali di provare a ripristinare questa applicazione**: a partire dalla versione 1810, se l'applicazione è stata creata con una riga di comando di ripristino, abilitare questa opzione. In Software Center è disponibile per gli utenti l'opzione **Ripristina** per ripristinare l'applicazione.<!--1357866-->  

- **Pre-distribuisci il software nel dispositivo primario dell'utente**: se la distribuzione è destinata a un utente, selezionare questa opzione per distribuire l'applicazione nel dispositivo primario dell'utente. Questa impostazione non richiede all'utente di accedere prima che venga eseguita la distribuzione. Non selezionare questa opzione se l'utente deve interagire con l'installazione. Questa opzione è disponibile solo quando la distribuzione è impostata su **Richiesto**.  

- **Invia pacchetti di riattivazione**: se la distribuzione è impostata su **Richiesto**, Configuration Manager invia un pacchetto di riattivazione ai computer prima che il client esegua la distribuzione. Il pacchetto attiva i computer nel momento in cui scade l'installazione. Prima di usare questa opzione, i computer e le reti devono essere configurati per la riattivazione LAN. Per altre informazioni, vedere [Pianificare la riattivazione dei client](../../core/clients/deploy/plan/plan-wake-up-clients.md).  

- **Consente a tutti i client che usano una connessione di rete a consumo di scaricare il contenuto una volta raggiunta la scadenza dell'installazione. Se si abilita questa opzione, potrebbe essere addebitato un costo aggiuntivo**: Questa opzione è disponibile solo per distribuzioni con scopo **Richiesto**.  

- **Aggiorna automaticamente tutte le versioni sostituite di questa applicazione**: il client aggiorna tutte le versioni sostituite dell'applicazione usando l'applicazione sostitutiva.

    > [!Note]  
    > Questa opzione funziona indipendentemente dall'approvazione dell'amministratore. Se un amministratore ha già approvato la versione sostituita, non sarà necessario approvare anche la versione sostitutiva. L'approvazione è necessaria solo per le nuove richieste, non per gli aggiornamenti sostitutivi.<!--515824-->  
    >
    > Per lo scopo di installazione **Disponibile** è possibile abilitare o disabilitare questa opzione. <!--1351266-->


#### <a name="approval-settings"></a><a name="bkmk_approval"></a> Impostazioni di approvazione

Il comportamento di approvazione applicazione dipende dall'abilitazione o meno della funzionalità facoltativa consigliata **Approva le richieste dell'applicazione per gli utenti per ogni dispositivo**.

- **Un amministratore deve approvare una richiesta per questa applicazione nel dispositivo**: Se si attiva la funzionalità facoltativa, l'amministratore deve approvare qualsiasi richiesta utente per l'applicazione prima che l'utente possa installarla nel dispositivo desiderato. Se l'amministratore approva la richiesta, l'utente può installare l'applicazione solo su quel dispositivo. Per installare l'applicazione in un altro dispositivo dovrà inviare un'altra richiesta. Questa opzione è disattivata quando lo scopo della distribuzione è **Richiesto** o quando si distribuisce l'applicazione un una raccolta di dispositivi.

- **Richiedi l'approvazione dell'amministratore se gli utenti richiedono questa applicazione**: se non si attiva la funzionalità facoltativa, l'amministratore deve approvare qualsiasi richiesta utente per l'applicazione prima che l'utente possa installarla. Questa opzione è disattivata quando lo scopo della distribuzione è **Richiesto** o quando si distribuisce l'applicazione un una raccolta di dispositivi.  

Per altre informazioni, vedere [Approvare le applicazioni](app-approval.md).


#### <a name="deployment-properties-deployment-settings"></a>**Impostazioni distribuzione** delle proprietà della distribuzione

Quando si visualizzano le proprietà di una distribuzione, l'opzione seguente viene visualizzata nella scheda **Impostazioni distribuzione**, se è supportata dal tipo di tecnologia di distribuzione:

**Chiudi automaticamente eventuali file eseguibili in esecuzione specificati nella scheda Comportamento di installazione della finestra di dialogo relativa alle proprietà del tipo di distribuzione**. Per altre informazioni, vedere [Controllare l'esecuzione di file eseguibili prima di installare un'applicazione](#bkmk_exe-check).



### <a name="deployment-scheduling-settings"></a><a name="bkmk_deploy-sched"></a> Impostazioni di **Pianificazione** della distribuzione

Nella pagina **Pianificazione** configurare il momento in cui l'applicazione deve essere distribuita o resa disponibile per i dispositivi client.

Per impostazione predefinita, Configuration Manager rende i criteri di distribuzione immediatamente disponibili ai client. Se si vuole creare la distribuzione, ma non renderla disponibile ai client fino a una data successiva, configurare l'opzione **Pianifica disponibilità applicazione**. Selezionare quindi la data e l'ora, specificando anche se viene usata l'ora UTC o il fuso orario del client.

Se la distribuzione è di tipo **Richiesto**, specificare anche la **Scadenza installazione**. Per impostazione predefinita, la scadenza è Appena possibile.

Ad esempio, è necessario distribuire una nuova applicazione line-of-business. Tutti gli utenti devono eseguire l'installazione entro una determinata ora, ma si vuole offrire agli utenti la possibilità di acconsentire esplicitamente in anticipo. È anche necessario assicurarsi che il sito abbia distribuito il contenuto in tutti i punti di distribuzione. È possibile pianificare l'applicazione in modo che sia disponibile tra cinque giorni da oggi. Questa pianificazione offre il tempo necessario per distribuire il contenuto e confermarne lo stato. È quindi possibile impostare la scadenza dell'installazione a un mese da oggi. Gli utenti potranno visualizzare l'applicazione in Software Center quando sarà disponibile tra cinque giorni. Se non eseguono alcuna azione, il client installerà automaticamente l'applicazione in corrispondenza della scadenza dell'installazione.

Se l'applicazione distribuita sostituisce un'altra applicazione, è possibile impostare la scadenza dell'installazione in corrispondenza del momento in cui gli utenti ricevono la nuova applicazione. Per aggiornare gli utenti con l'applicazione sostituita, impostare la **Scadenza installazione**.


#### <a name="delay-enforcement-with-a-grace-period"></a>Posticipare l'imposizione con un periodo di tolleranza

È possibile che si voglia concedere agli utenti più tempo per installare le applicazioni necessarie, *oltre* a eventuali scadenze configurate. Questo comportamento è in genere necessario quando un computer è stato disattivato per molto tempo ed è necessario installare molte applicazioni, come nel caso, ad esempio, di un utente che, tornato da una vacanza, deve attendere parecchio tempo mentre il client installa le distribuzioni scadute. Per contribuire alla risoluzione di questo problema, definire un periodo di tolleranza per l'imposizione.

- Configurare prima di tutto il periodo di tolleranza con la proprietà **Periodo di tolleranza per l'imposizione dopo la scadenza della distribuzione (ore)** nelle impostazioni del client. Per altre informazioni, vedere il gruppo [Agente computer](../../core/clients/deploy/about-client-settings.md#computer-agent). Specificare un valore compreso tra **1** e **120** ore.  

- Nella pagina **Pianificazione** di una distribuzione richiesta dell'applicazione abilitare l'opzione **Ritardare l'imposizione di questa distribuzione in base alle preferenze dell'utente, fino al periodo di tolleranza massimo definito nelle impostazioni del client**. Tale periodo di tolleranza si applica a tutte le distribuzioni con questa opzione abilitata e destinate a dispositivi in cui è stata distribuita anche l'impostazione del client.

Dopo la scadenza il client installa l'applicazione nella prima finestra non lavorativa, configurata dall'utente, fino al termine del periodo di tolleranza. Tuttavia l'utente può comunque aprire Software Center e installare l'applicazione in qualsiasi momento. Una volta scaduto il periodo di tolleranza, le distribuzioni scadute torneranno al normale comportamento.

![Diagramma della sequenza temporale del periodo di tolleranza](media/grace-period.svg)

<!-- SCCMDocs issue #1599 -->

> [!Note]  
> Nella maggior parte dei casi, questa funzionalità risolve lo scenario in cui il dispositivo è spento mentre l'utente è fuori sede. Tecnicamente, il periodo di tolleranza inizia quando il client ottiene i criteri dopo la scadenza della distribuzione. Lo stesso comportamento si verifica se si arresta il servizio client Configuration Manager (CcmExec) e quindi lo si riavvia in un secondo momento dopo la scadenza della distribuzione.

### <a name="deployment-user-experience-settings"></a><a name="bkmk_deploy-ux"></a> Impostazioni dell'**Esperienza utente** della distribuzione

Nella pagina **Esperienza utente** specificare le informazioni sulle modalità di interazione degli utenti con l'installazione dell'applicazione.

- **Notifiche utente**: specificare se visualizzare la notifica in Software Center nell'orario disponibile configurato. Questa impostazione consente di stabilire anche se inviare notifiche agli utenti nei computer client. Per le distribuzioni disponibili non è possibile selezionare l'opzione **Nascondi in Software Center e nascondi tutte le notifiche**.  

    - **Quando sono necessarie modifiche al software, mostra una finestra di dialogo all'utente invece di un avviso popup**<!--3555947-->: a partire dalla versione 1902, selezionare questa opzione per modificare l'esperienza utente rendendola più invasiva. Si applica solo alle distribuzioni richieste. Per altre informazioni, vedere [Pianificare Software Center](../plan-design/plan-for-software-center.md#bkmk_impact).

- **Installazione software** e **Riavvio sistema**: configurare queste impostazioni solo per le distribuzioni obbligatorie. Consentono di specificare i comportamenti relativi al raggiungimento della scadenza da parte della distribuzione all'esterno di qualsiasi finestra di manutenzione definita. Per altre informazioni sulle finestre di manutenzione, vedere [Come usare le finestre di manutenzione](../../core/clients/manage/collections/use-maintenance-windows.md).  

- **Gestione filtri di scrittura per dispositivi con Windows Embedded**: questa impostazione controlla il comportamento di installazione nei dispositivi con Windows Embedded in cui è abilitato un filtro di scrittura. Scegliere l'opzione per eseguire il commit delle modifiche alla scadenza dell'installazione o durante una finestra di manutenzione. Quando si seleziona questa opzione, è necessario un riavvio e la modifica viene salvata in modo permanente nel dispositivo. In caso contrario, l'applicazione viene installata nell'overlay temporaneo e il commit viene eseguito successivamente.  

    - Quando si distribuisce un aggiornamento software in un dispositivo con Windows Embedded, verificare che il dispositivo appartenga a una raccolta che ha una finestra di manutenzione configurata. Per altre informazioni sulle finestre di manutenzione e sui dispositivi con Windows Embedded, vedere [Creare applicazioni Windows Embedded con System Center Configuration Manager](../get-started/creating-windows-embedded-applications.md).  


### <a name="deployment-alerts"></a><a name="bkmk_deploy-alerts"></a>**Avvisi** della distribuzione

Nella pagina **Avvisi** configurare la modalità di generazione di avvisi per questa distribuzione da parte di Configuration Manager. Se si usa anche System Center Operations Manager, configurare i rispettivi avvisi. È possibile configurare solo alcuni avvisi per le distribuzioni obbligatorie. 


## <a name="create-a-phased-deployment"></a><a name="bkmk_phased"></a> Creare una distribuzione in più fasi

<!--1358147-->
A partire dalla versione 1806, è possibile creare una distribuzione in più fasi per un'applicazione. Le distribuzioni in più fasi consentono di orchestrare un'implementazione coordinata e in sequenza del software basata su criteri e gruppi personalizzabili. È possibile, ad esempio, distribuire l'applicazione in una raccolta pilota e quindi continuare automaticamente l'implementazione in base ai criteri per l'esito positivo.

Per altre informazioni, vedere gli articoli seguenti:  

- [Creare una distribuzione in più fasi](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  

- [Gestire e monitorare le distribuzioni in più fasi](../../osd/deploy-use/manage-monitor-phased-deployments.md?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  



## <a name="delete-a-deployment"></a><a name="bkmk_delete"></a> Eliminare una distribuzione

1. Nella console di Configuration Manager passare all'area di lavoro **Raccolta software**, espandere **Gestione applicazioni** e selezionare il nodo **Applicazioni** o **Gruppi di applicazioni**.  

2. Selezionare l'applicazione o il gruppo di applicazioni che include la distribuzione da eliminare.  

3. Passare alla scheda **Distribuzioni** del riquadro dei dettagli e selezionare la distribuzione.  

4. Sulla barra multifunzione fare clic su **Elimina** nella scheda **Distribuzione** e nel gruppo **Distribuzione**.  

Quando si elimina la distribuzione di un'applicazione, tutte le istanze dell'applicazione già installate dai client non vengono rimosse. Per rimuovere queste applicazioni, distribuire l'applicazione nei computer con **Disinstalla**. Se si elimina la distribuzione di un'applicazione o si rimuove una risorsa dalla raccolta in cui si vuole eseguire la distribuzione, l'applicazione non è più visibile in Software Center.



## <a name="user-notifications-for-required-deployments"></a><a name="bkmk_notify"></a> Notifiche utente per le distribuzioni richieste

Quando gli utenti ricevono software obbligatorio e selezionano l'impostazione **Posponi e ricorda tra**, possono scegliere una delle opzioni seguenti:  

- **In seguito**: specifica che le notifiche vengono programmate in base alle impostazioni di notifica configurate nelle impostazioni del client.  

- **Orario fisso**: specifica che la notifica venga pianificata per una nuova visualizzazione dopo l'ora selezionata. Ad esempio, se si seleziona un periodo di 30 minuti, la notifica viene visualizzata di nuovo dopo 30 minuti.  

![Gruppo Agente computer nelle impostazioni client predefinite](media/ComputerAgentSettings.png)

Il tempo di posticipo massimo è sempre basato sui valori di notifica configurati nelle impostazioni del client su ogni orario presente lungo la cronologia di distribuzione. Ad esempio:  

- Viene configurata l'impostazione **Più di 24 ore alla scadenza di distribuzione. Avvisare l'utente ogni (ore)** nella pagina **Agente computer** per 10 ore.  

- Il client visualizza la finestra di dialogo di notifica più di 24 ore prima della scadenza di distribuzione.  

- La finestra di dialogo visualizza opzioni di posposizione fino a 10 ore ma mai superiori.  

- Quando la scadenza di distribuzione di avvicina, nella finestra di dialogo vengono visualizzate meno opzioni. Tali opzioni sono coerenti con le impostazioni del client pertinenti per ogni componente della scadenza di distribuzione.  

Per una distribuzione ad alto rischio, ad esempio una sequenza di attività che distribuisce un sistema operativo, l'esperienza di notifica dell'utente è più invasiva. Anziché una notifica temporanea sulla barra delle applicazioni, viene visualizzata una finestra di dialogo simile alla seguente ogni volta che è necessaria una manutenzione critica del software:

![Finestra di dialogo software che notifica la necessità di una manutenzione critica del software](media/client-toast-notification.png)



## <a name="check-for-running-executable-files"></a><a name="bkmk_exe-check"></a> Verificare se sono in esecuzione file eseguibili

Configurare una distribuzione in modo da verificare se alcuni file eseguibili sono in esecuzione sul client. Usare questa opzione per controllare se sono presenti processi che potrebbero interrompere l'installazione dell'applicazione. Se uno di questi file eseguibili è in esecuzione nel client, l'installazione del tipo di distribuzione si blocca. L'utente deve chiudere il file eseguibile in esecuzione prima che il client installi il tipo di distribuzione. Per le distribuzioni con scopo Richiesto, il client può chiudere automaticamente il file eseguibile in esecuzione.

1. Aprire la finestra di dialogo **Proprietà** per il tipo di distribuzione.  

2. Passare alla scheda **Comportamento di installazione** e fare clic su **Aggiungi**.  

3. Nella finestra di dialogo **Aggiungi un file eseguibile** immettere il nome del file eseguibile di destinazione. Facoltativamente, immettere un nome descrittivo per l'applicazione in modo da identificarla più facilmente nell'elenco.  

4. Fare clic su **OK** e quindi su **OK** per chiudere la finestra delle proprietà del tipo di distribuzione.  

5. Quando si distribuisce l'applicazione, selezionare l'opzione **Chiudi automaticamente eventuali file eseguibili in esecuzione specificati nella scheda Comportamento di installazione della finestra di dialogo relativa alle proprietà del tipo di distribuzione**. Questa opzione è disponibile nella scheda **Impostazioni distribuzione** delle proprietà della distribuzione.  

> [!Note]
> Se si configura un'applicazione per verificare l'esecuzione dei file eseguibili e la si include nel passaggio [Installa applicazione](../../osd/understand/task-sequence-steps.md#BKMK_InstallApplication) della sequenza di attività, la sequenza di attività non riuscirà a installarla. Se non si configura questo passaggio della sequenza di attività in modo da continuare in caso di errore, l'intera sequenza di attività non riuscirà.

### <a name="client-behaviors-and-user-notifications"></a>Comportamenti dei client e notifiche utente

Dopo che i client ricevono la distribuzione, si applica il comportamento seguente:  

- Se l'applicazione è stata distribuita come **Disponibile** e un utente prova a installarla, il client chiede all'utente di chiudere tutti i file eseguibili in esecuzione specificati prima di procedere con l'installazione.  

- Se l'applicazione è stata distribuita con scopo **Richiesto** ed è stata specificata l'opzione **Chiudi automaticamente eventuali file eseguibili in esecuzione specificati nella scheda Comportamento di installazione della finestra di dialogo relativa alle proprietà del tipo di distribuzione**, il client mostrerà una notifica per segnalare all'utente che i file eseguibili specificati vengono chiusi automaticamente al raggiungimento della scadenza dell'installazione dell'applicazione.  

    - È possibile pianificare queste finestre di dialogo nel gruppo **Agente computer** delle impostazioni del client. Per altre informazioni, vedere [Agente computer](../../core/clients/deploy/about-client-settings.md#computer-agent).  

    - Se non si vuole che l'utente visualizzi questi messaggi, selezionare l'opzione **Nascondi in Software Center e nascondi tutte le notifiche** nella scheda **Esperienza utente** delle proprietà della distribuzione. Per altre informazioni, vedere [Impostazioni dell'esperienza utente per la distribuzione](#bkmk_deploy-ux).  

- Se l'applicazione è stata distribuita come **Richiesta** e non è stata specificata l'opzione **Chiudi automaticamente eventuali file eseguibili in esecuzione specificati nella scheda Comportamento di installazione della finestra di dialogo relativa alle proprietà del tipo di distribuzione**, l'installazione dell'applicazione ha esito negativo se sono in esecuzione una o più applicazioni tra quelle specificate.  



## <a name="deploy-user-available-applications-on-azure-ad-joined-devices"></a>Distribuire applicazioni disponibili per l'utente in dispositivi aggiunti ad Azure AD

<!-- 1322613 -->
Se si distribuiscono applicazioni come disponibili agli utenti, questi possono esplorarle e installarle tramite Software Center nei dispositivi Azure Active Directory (Azure AD).  

### <a name="prerequisites"></a>Prerequisiti

- Abilitare HTTPS nel punto di gestione  

- Integrare il sito con [Azure AD](../../core/servers/deploy/configure/azure-services-wizard.md) per la **Gestione cloud**  

    - Configurare [l'individuazione utenti di Azure AD](../../core/servers/deploy/configure/configure-discovery-methods.md#azureaadisc)  

- Distribuire un'applicazione come disponibile a una raccolta di utenti da Azure AD  

- Distribuire il contenuto dell'applicazione a un [punto di distribuzione cloud](../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md)  

- Abilitare l'impostazione client **Usa il nuovo Software Center** nel gruppo [Agente computer](../../core/clients/deploy/about-client-settings.md#computer-agent).  

- Il sistema operativo del client deve essere Windows 10 e il client deve essere aggiunto ad Azure AD, solo al dominio cloud o ibrido aggiunto ad Azure AD.  

- Per supportare i client basati su Internet:  

    - [Gateway di gestione cloud](../../core/clients/manage/cmg/plan-cloud-management-gateway.md)  

    - Abilitare l'impostazione client: **Abilitare le richieste dei criteri utente dai client Internet** nel gruppo [Criteri client](../../core/clients/deploy/about-client-settings.md#client-policy)  

- Per supportare i client su Intranet:  

    - Aggiungere il punto di distribuzione cloud a un gruppo di limiti usato dai client  

    - I client devono risolvere il nome di dominio completo (FQDN) del punto di gestione abilitato per HTTPS  



## <a name="next-steps"></a>Passaggi successivi

- [Monitorare le applicazioni](monitor-applications-from-the-console.md)
- [Risolvere i problemi relativi alla distribuzione di applicazioni](troubleshoot-application-deployment.md)
- [Attività di gestione per le applicazioni](management-tasks-applications.md)
- [Manuale dell'utente di Software Center](../../core/understand/software-center.md)
