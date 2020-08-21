---
title: Informazioni di riferimento sull'interfaccia utente del Supporto tecnico
titleSuffix: Configuration Manager
description: Informazioni su come usare gli strumenti del Supporto tecnico.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 41cdebfe-b595-40aa-a385-32e0746255ed
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 79d483f95c12c1da1e34ca556836a1f42bbffbef
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699450"
---
# <a name="support-center-user-interface-reference"></a>Informazioni di riferimento sull'interfaccia utente del Supporto tecnico

*Si applica a: Configuration Manager (Current Branch)*

Questo articolo è un testo di riferimento che descrive le interfacce utente degli strumenti del Supporto tecnico:
- Support Center
- Visualizzatore log del Supporto tecnico
- Visualizzatore del Supporto tecnico



## <a name="support-center-reference"></a>Informazioni di riferimento sul Supporto tecnico

Questa sezione descrive l'interfaccia utente dello strumento **Supporto tecnico**. 
- [Menu Window](#bkmk_support-window) (Finestra)  
- [Scheda Home](#bkmk_support-home)  
- [Scheda Client](#bkmk_support-client)  
- [Scheda Policy](#bkmk_support-policy) (Criteri)  
- [Scheda Content](#bkmk_support-content) (Contenuto)  
- [Scheda Inventory](#bkmk_support-inventory) (Inventario)  
- [Scheda Troubleshooting](#bkmk_support-troubleshoot) (Risoluzione dei problemi)  
- [Scheda Logs](#bkmk_support-logs) (Log)  


### <a name="window-menu"></a><a name="bkmk_support-window"></a> Menu Window (Finestra)

Nell'angolo superiore sinistro della finestra del Supporto tecnico aprire questo menu selezionando la freccia nella casella blu.

#### <a name="local-machine-connection"></a>Local Machine Connection
Il Supporto tecnico raccoglie i file di log ed esegue la risoluzione dei problemi sul client che esegue lo strumento.

#### <a name="remote-connection"></a>Remote Connection
Consente di stabilire una connessione remota con un altro client di Configuration Manager. Dopo la connessione, il Supporto tecnico raccoglie i file di log ed esegue la risoluzione dei problemi sul client a cui è connesso.

#### <a name="about"></a>Informazioni su
Visualizza informazioni sul Supporto tecnico.

#### <a name="options"></a>Options
Nella finestra di dialogo **Options** è possibile:
- Ridurre il movimento degli elementi dell'interfaccia utente animati  
- Cambiare il percorso di salvataggio predefinito per i file di bundle di dati  
- Cambiare il percorso dei file temporanei    
- Reimpostare gli avvisi. Eventuali messaggi di avviso eliminati in precedenza vengono visualizzati nuovamente quando vengono attivati.  
- Reimpostare il percorso predefinito dei file temporanei, `%UserProfile%\AppData\Local\Microsoft\ConfigMgrSupportCenter`

#### <a name="exit"></a>Exit
Chiude il Supporto tecnico.



### <a name="home-tab"></a><a name="bkmk_support-home"></a> Scheda Home

#### <a name="collect-selected-data"></a>Collect Selected Data (Raccogli dati selezionati)
Il Supporto tecnico raccoglie informazioni dal client di Configuration Manager. Per impostazione predefinita, vengono raccolti i tipi seguenti:
- File di registro
- Client configuration collector
- Sistema operativo

Per raccogliere altri tipi di informazioni, selezionare la casella di controllo accanto al nome del tipo.

Selezionare l'elenco a discesa nella parte inferiore del pulsante **Collect selected data** (Raccogli dati selezionati) sulla barra multifunzione e selezionare **Collect all data** (Raccogli tutti i dati). Questa azione consente di raccogliere il set completo dei dati dello stato del client.

Mentre il Supporto tecnico sta raccogliendo i dati, selezionare **Cancel collection** (Annulla raccolta) per interrompere l'operazione.

#### <a name="data-types"></a>Tipi di dati
Se si seleziona la casella di controllo relativa a un'opzione, quando si seleziona di nuovo **Collect selected data** (Raccogli dati selezionati) il Supporto tecnico raccoglie i dati del tipo corrispondente. Sono disponibili i tipi seguenti:  

- **File di log**: file di log del client, inclusi i log di installazione  

- **Policy** (Criteri): raccolta dei criteri del client  

- **Certificati**: informazioni sulle chiavi pubbliche per i certificati client. Support Center non raccoglie chiavi private per i certificati.  

- **Client configuration collector** (Agente di raccolta configurazione client): informazioni sul client di Configuration Manager. Questo tipo di dati non può essere disabilitato.  

- **Client registry** (Registro di sistema client): raccoglie informazioni di configurazione del client dal Registro di sistema. Support Center raccoglie solo le informazioni del Registro di sistema relative a Configuration Manager.  

- **Client WMI** (WMI client): informazioni di configurazione del client da WMI. Support Center non raccoglie criteri client.  

- **Troubleshooting** (Risoluzione dei problemi): dati in tempo reale di risoluzione dei problemi che agevolano la diagnosi dei problemi più comuni dei client con Active Directory, punti di gestione, reti, assegnazioni di criteri e registrazione.  

    > [!NOTE]  
    > Questo tipo di dati non è supportato quando si stabilisce una connessione remota a un altro client.  

- **Debug dumps** (Dump del debug): esegue il dump del debug del client e dei processi correlati. I dump del debug possono essere di grandi dimensioni. Abilitare questa opzione solo durante la risoluzione dei problemi di prestazioni del client.  

    > [!WARNING]  
    > Raccogliendo i dump del debug i bundle di dati possono diventare molto grandi, arrivando in alcuni casi a diverse centinaia di MB.  
    >  
    > I dump del debug possono contenere informazioni riservate, ad esempio password, segreti di crittografia o dati utente. I dump del debug devono essere raccolti solo dietro indicazione del personale del supporto tecnico Microsoft. I bundle di dati che contengono dump del debug devono essere gestiti con attenzione per garantirne la protezione da accessi non autorizzati.  
    >  
    > Questo tipo di dati non è supportato quando si stabilisce una connessione remota a un altro client.  

- **Sistema operativo**: raccoglie informazioni di configurazione sul computer locale. Questi dati includono informazioni sull'installazione di Windows, sulle schede di rete e sulla configurazione dei servizi di sistema. Questo tipo di dati non può essere disabilitato.  



### <a name="client-tab"></a><a name="bkmk_support-client"></a> Scheda Client

#### <a name="load-or-refresh"></a>Load o Refresh
Il Supporto tecnico carica o aggiorna i dettagli per il client di Configuration Manager.

#### <a name="control-client-agent-service"></a>Control client agent service
Eseguire una delle azioni seguenti nel servizio agente client di Configuration Manager (ccmexec) del client connesso:  

- **Restart client** (Riavvia client)  

    > [!IMPORTANT]  
    > Se il servizio agente client non viene riavviato correttamente, il client non può essere gestito da Configuration Manager finché il servizio non viene riavviato.  

- **Start client** (Avvia client)  

- **Stop client** (Arresta client)  

    > [!IMPORTANT]  
    > Il client non può essere gestito da Configuration Manager finché il servizio non viene riavviato.  

#### <a name="properties"></a>Proprietà
Quando si caricano i dettagli del client, il Supporto tecnico visualizza le proprietà seguenti:  

- **Client ID** (ID client): identificatore univoco usato da Configuration Manager per identificare il client  

- **Hardware ID** (ID hardware): identificatore univoco usato da Configuration Manager per identificare l'hardware del client  

- **Approved** (Approvato): indica se il client è stato approvato in Configuration Manager  

- **Registration State** (Stato della registrazione): indica se il client è registrato con Configuration Manager  

- **Internet-facing** (Con connessione Internet): indica se il client è connesso a Internet  

- **Version** (Versione): numero di versione del client di Configuration Manager installato  

- **Site Code** (Codice del sito): codice del sito primario a cui è assegnato il client  

- **Assigned MP** (Punto di gestione assegnato): nome di dominio completo (FQDN) del punto di gestione attualmente assegnato al client  

- **Resident MP** (Punto di gestione residente): FQDN del punto di gestione residente  

- **Proxy MP** (Punto di gestione proxy): nome host o FQDN del punto di gestione proxy (se presente)  

- **Proxy Site Code** (Codice del sito proxy): Codice del sito per il sito secondario (se presente)  

- **Proxy State** (Stato proxy): stato del punto di gestione proxy del client di Configuration Manager, ad esempio, **Active** (Attivo) o **Pending** (In sospeso).  



### <a name="policy-tab"></a><a name="bkmk_support-policy"></a> Scheda Policy (Criteri)

Usare le azioni in questa scheda anziché lo strumento [PolicySpy](policy-spy.md) precedente.

#### <a name="load-policy"></a>Load Policy (Carica criteri)
Questa opzione varia a seconda della visualizzazione:

- **Load Actual policy** (Carica criteri effettivi): selezionare **Actual** (Effettivi) nel gruppo View (Visualizza) e quindi selezionare questa opzione nel gruppo Policy (Criteri). Il Supporto tecnico carica i criteri client attualmente selezionati.  

- **Load Requested policy** (Carica criteri richiesti): selezionare **Requested** (Richiesti) nel gruppo View (Visualizza) e quindi selezionare questa opzione nel gruppo Policy (Criteri). Il Supporto tecnico carica i criteri client richiesti per il client.  

- **Load Default policy** (Carica criteri predefiniti): selezionare **Default** (Predefiniti) nel gruppo View (Visualizza) e quindi selezionare questa opzione nel gruppo Policy (Criteri). Il Supporto tecnico carica i criteri predefiniti per questo client.  

Selezionare l'elenco a discesa nella parte inferiore di questo pulsante per visualizzare opzioni aggiuntive:

- **Load or Refresh all** (Carica o aggiorna tutto): carica o aggiorna i criteri effettivi, richiesti e predefiniti nello stesso tempo.  

#### <a name="actual-view"></a>Visualizzazione Actual (Effettivi)
Apre la visualizzazione dei criteri effettivi

#### <a name="requested-view"></a>Visualizzazione Requested (Richiesti)
Apre la visualizzazione dei criteri richiesti

#### <a name="default-view"></a>Visualizzazione Default (Predefiniti)
Apre la visualizzazione dei criteri predefinita. I dispositivi ottengono questi criteri quando si installa il client di Configuration Manager.

#### <a name="request-and-evaluate-policy"></a>Request and evaluate policy (Richiedi e valuta criteri)
Il Supporto tecnico richiede i criteri client al punto di gestione e quindi li valuta nel client.

Selezionare l'elenco a discesa nella parte inferiore di questo pulsante per visualizzare opzioni aggiuntive:  

- **Request policy** (Richiedi criteri): il Supporto tecnico richiede i criteri client al punto di gestione.  

- **Evaluate policy** (Valuta criteri): il Supporto tecnico valuta i criteri client nel client.  

- **Reset policy to default** (Reimposta impostazioni predefinite criteri): il Supporto tecnico indica al client di Configuration Manager di riapplicare i criteri predefiniti e rimuove tutti i criteri computer e utente presenti nel client.  

#### <a name="listen-for-policy-events"></a>Listen for policy events
Il Supporto tecnico rimane in ascolto degli eventi dei criteri. Selezionare di nuovo questa opzione per disabilitare l'ascolto degli eventi dei criteri. Per visualizzare **Policy events** (Eventi criteri), selezionare la freccia nella parte inferiore di questa scheda. 

#### <a name="clear-events"></a>Clear Events (Cancella eventi)
Il Supporto tecnico cancella tutti gli eventi dei criteri.



### <a name="content-tab"></a><a name="bkmk_support-content"></a> Scheda Content (Contenuto)

Visualizza il contenuto del client, incluso il contenuto memorizzato nella cache e consente il monitoraggio dello stato delle distribuzioni di aggiornamenti software e di applicazioni. 

#### <a name="load-or-refresh"></a>Load o Refresh
*Si applica alle visualizzazioni Content (Contenuto) e Cache*

Il Supporto tecnico carica o aggiorna l'elenco del contenuto presente in quel momento nel client.

#### <a name="invoke-trigger"></a>Invoke trigger (Chiama trigger)
Le voci seguenti di questo menu richiedono un'azione del client relativa al contenuto:  

- **Location services** (Servizi di posizione)  

    - **Refresh content locations** (Aggiorna posizioni contenuti): aggiorna i punti di distribuzione usati da tutti i download di contenuto attivi.  

    - **Refresh management points** (Aggiorna punti di gestione): aggiorna l'elenco interno di punti di gestione usati dal client.  

    - **Time out content requests** (Timeout richieste contenuto): se una richiesta di posizione di contenuto è in esecuzione da troppo tempo, questa azione la interrompe.  

- **Application deployment evaluation** (Valutazione distribuzione applicazioni): avvia un'attività che valuta le applicazioni distribuite.  

- **Software updates deployment evaluation** (Valutazione distribuzione aggiornamenti software): avvia un'attività che valuta gli aggiornamenti del software distribuiti.  

- **Software updates source scan** (Analisi origine aggiornamenti software): avvia un'attività che analizza i percorsi di origine degli aggiornamenti.  

- **Windows Installer source list update** (Aggiornamento elenco origine Windows Installer): avvia un'attività che aggiorna il percorso di origine per le installazioni di Windows Installer (MSI).  

#### <a name="content-view"></a>Visualizzazione di contenuto
Visualizza le applicazioni, i pacchetti e gli aggiornamenti caricati nel client. Se si seleziona un'applicazione, un pacchetto o un aggiornamento, vengono visualizzate informazioni dettagliate sul contenuto. Per alcune applicazioni, è anche possibile eseguire le azioni seguenti:  

- **Aggiornare**: aggiorna la visualizzazione dei dettagli  

- **Verify or Download** (Verifica o scarica): consente di verificare se un'applicazione è disponibile per il download  

- **Install** (Installa): installa l'applicazione  

- **Uninstall** (Disinstalla): Disinstallare l'applicazione  

#### <a name="cache-view"></a>Visualizzazione Cache
Visualizza la configurazione della cache del client e i dettagli sul contenuto della cache. Quando si connette il Supporto tecnico a un client locale, è anche possibile eseguire le azioni seguenti:  

- Per cambiare il percorso della cache, selezionare **Change** (Modifica) accanto al campo **Cache location** (Percorso cache).  

- Per regolare le dimensioni della cache, selezionare **Change** (Modifica) accanto al campo **Cache size** (Dimensioni cache).  

- Per cancellare la cache del client, selezionare **Clear** (Cancella) accanto al campo **Cache in use** (Cache in uso).  

Questa visualizzazione illustra le proprietà seguenti:  

- **Location** (Percorso): percorso di ogni cartella della cache. Selezionare il collegamento per aprire la cartella in Esplora risorse.   
- **Content ID** (ID contenuto)  
- **Cache ID** (ID cache)  
- **Size**  
- **Last Referenced** (Ultimo riferimento): questa proprietà corrisponde alla data in cui il client ha letto o scritto questo elemento nella cache.  

#### <a name="monitoring-view"></a>Visualizzazione Monitoring (Monitoraggio)
Selezionare **Monitoring** (Monitoraggio) per visualizzare lo stato attivo delle distribuzioni di aggiornamenti software e di applicazioni. La visualizzazione mostra i messaggi di stato generati dai messaggi WMI degli eventi di aggiornamento software e applicazioni.

Per ogni evento, questa visualizzazione illustra le proprietà seguenti:  

- **Time** (Ora): ora in cui il client ha generato l'evento  
- **Topic type** (Tipo di argomento): il tipo del messaggio di stato  
- **Topic ID** (ID argomento): ID del messaggio di stato, usato per eseguire il mapping agli eventi nei file di log  
- **Topic ID type** (Tipo ID argomento): sottotipo del messaggio di stato  
- **State ID** (ID stato): risultati dell'azione monitorata  
- **Details** (Dettagli) e **Event data** (Dati evento): altre informazioni nei messaggi di stato illustrati nella visualizzazione. I dettagli sullo stato possono anche essere vuoti.  



### <a name="inventory-tab"></a><a name="bkmk_support-inventory"></a> Scheda Inventory (Inventario)

#### <a name="load-or-refresh"></a>Load o Refresh
Il Supporto tecnico carica o aggiorna l'inventario del client per la visualizzazione attualmente selezionata.

#### <a name="invoke-trigger"></a>Invoke trigger (Chiama trigger)

> [!Note]  
> Per le attività diverse da **Software metering report cycle**:  
> - Se si richiede l'attività quando è già in esecuzione un'altra attività di inventario, il client accoda la nuova attività e la esegue dopo il completamento dell'attività corrente e delle altre attività in coda.  
> - È possibile tenere traccia dello stato dell'attività in **InventoryAgent.log**.  

Le voci seguenti di questo menu richiedono un'azione del client correlata all'inventario:  

- **Discovery data collection cycle (heartbeat)** (Ciclo raccolta dati di individuazione (heartbeat)): attiva l'attività client usata per la raccolta delle informazioni di individuazione dei dispositivi  

- **File collection cycle** (Ciclo raccolta file): attiva l'attività client usata per la raccolta dei file locali  

- **Hardware inventory cycle** (Ciclo inventario hardware): attiva l'attività client usata per la raccolta dei dati di inventario hardware  

- **IDMIF collection cycle** (Ciclo raccolta IDMIF): attiva l'attività client usata per la raccolta dei dati IDMIF  

- **Software inventory cycle** (Ciclo inventario software): attiva l'attività client usata per la raccolta dei dati di inventario software  

- **Software metering report cycle** (Ciclo report misurazione del software): attiva l'attività client usata per creare un report di controllo del software e inviarlo al punto di gestione. È possibile tenere traccia dello stato dell'attività in **SWMTRReportGen.log**.

- **Send unsent state messages in queue** (Invia messaggi di stato non inviati in coda): attiva l'attività client per scaricare la coda dei messaggi di stato.

- **Advanced**  
    - **Hardware inventory cycle (full resynchronization)** (Ciclo inventario hardware (risincronizzazione completa))  
    - **Software inventory cycle (full resynchronization)** (Ciclo inventario software (risincronizzazione completa))  


#### <a name="views"></a>Visualizzazioni
Se non è abilitata una funzionalità, la visualizzazione non visualizza alcun dato. 

- **Status** (Stato): visualizza i set di dati di inventario raccolti dal client  

- **DDR**: informazioni sui dati di individuazione client raccolti dal client  

- **HINV**: informazioni sui dati di inventario hardware raccolti dal client  

- **SINV**: informazioni sui dati di inventario software raccolti dal client  

- **File collection** (Raccolta file): informazioni sui file raccolti dal client  

- **IDMIF**: informazioni sui dati IDMIF e NOIDMIF raccolti dal client  

- **Metering** (Misurazione): informazioni sui dati di misurazione del software raccolti dal client  



### <a name="troubleshooting-tab"></a><a name="bkmk_support-troubleshoot"></a> Scheda Troubleshooting (Risoluzione dei problemi)

Consente di risolvere alcuni dei problemi più comuni relativi ai client di Configuration Manager:  
- Problemi con Active Directory  
- Rete di Windows  
- Configuration Manager   
    - Punti di gestione  
    - Assegnazione di criteri  
    - Registrazione  


> [!NOTE]  
> Questa scheda non è disponibile quando ci si connette a un client di Configuration Manager remoto.


#### <a name="start"></a>Avvia
Avvia la risoluzione dei problemi del client

- **Active Directory**: esegue una query in Active Directory per recuperare le informazioni pubblicate nel sito di Configuration Manager  
- **MPCERTIFICATE**: Ottiene i certificati del punto di gestione  
- **MPLIST**: Ottiene un elenco dei punti di gestione  
- **MPKEYINFORMATION**: ottiene le informazioni delle chiavi di crittografia del punto di gestione  
- **Rete**: Consente di risolvere i problemi di rete  
- **Policy Assignments** (Assegnazioni criteri): Recupera le assegnazioni di criteri  
- **Registration** (Registrazione): verifica che il client sia registrato con il sito  

#### <a name="view-selected-log"></a>View selected log
Dopo aver selezionato una riga nella scheda Troubleshooting (Risoluzione dei problemi), selezionare questa azione per visualizzare il file di log.

#### <a name="keep-previous-results"></a>Keep previous results
Se si esegue la risoluzione dei problemi del client e quindi si vuole tentare nuovamente questa operazione, scegliere questa opzione per conservare i risultati del primo tentativo. In caso contrario, il Supporto tecnico sovrascrive i file di log della risoluzione dei problemi precedente.



### <a name="logs-tab"></a><a name="bkmk_support-logs"></a> Scheda Logs (Log)

Questa sezione contiene un elenco degli elementi disponibili nella scheda **Logs** (Log) dello strumento Supporto tecnico. 

Questa scheda è quasi identica allo strumento **Visualizzatore log**. Lo strumento **Visualizzatore log** non include le funzionalità **Configure client logging** (Configura registrazione client) e **Log groups** (Gruppi di log) descritte in questa sezione. La sezione [Informazioni di riferimento sul Visualizzatore log del Supporto tecnico](#bkmk_log-viewer) illustra in dettaglio le altre opzioni disponibili in questa scheda.

#### <a name="configure-client-logging"></a>Configure Client Logging

Impostare le opzioni seguenti: 
- **Client log level** (Livello registrazione client): livello di dettaglio e dimensioni del file di log  
- **Maximum file count** (Numero massimo di file): consente più file di log di un tipo specifico  
- **Maximum file size** (Dimensioni massime del file): dimensioni in byte di un file di log specifico prima che il client crei un nuovo log  

> [!NOTE]  
> Se si imposta un valore troppo basso per queste impostazioni, il client potrebbe non registrare informazioni utili. Se si imposta un valore troppo alto, i log del client possono utilizzare una quantità eccessiva di spazio di archiviazione.  

#### <a name="log-groups"></a>Log groups

Anziché selezionare manualmente i file di log usando il pulsante **Open logs** (Apri log), usare questo elenco a discesa per aprire tutti i file di log associati alle aree di funzionalità seguenti: 
- **Gestione della configurazione desiderata**
- **Inventario**
- **Distribuzione del software**
- **Aggiornamenti software**
- **Gestione delle applicazioni**
- **Criteri**
- **Registrazione client**
- **Distribuzione del sistema operativo**


## <a name="support-center-log-viewer-reference"></a><a name="bkmk_log-viewer"></a> Informazioni di riferimento sul Visualizzatore log del Supporto tecnico

Questa sezione descrive l'interfaccia utente dello strumento **Visualizzatore log del Supporto tecnico**. 

- [Menu Window](#bkmk_log-window) (Finestra)  
- [Scheda Home](#bkmk_log-home)  

Lo strumento **Visualizzatore log** è quasi identico alla scheda **Logs** (Log) del **Supporto tecnico**. Lo strumento **Visualizzatore log** non include le opzioni **Configure client logging** (Configura registrazione client) e **Log groups** (Gruppi di log).


### <a name="window-menu"></a><a name="bkmk_log-window"></a> Menu Window (Finestra)

Nell'angolo superiore sinistro della finestra del Visualizzatore log del Supporto tecnico aprire questo menu selezionando la freccia nella casella blu.

#### <a name="open-logs"></a>Open logs
Passare al percorso dei file di log da aprire. 

#### <a name="options"></a>Options
Nella finestra di dialogo **Options** è possibile:
- Ridurre il movimento degli elementi dell'interfaccia utente animati  
- Registrare il Visualizzatore log come app predefinita per i file di log con le estensioni log e lo_  
- Reimpostare gli avvisi. Eventuali messaggi di avviso eliminati in precedenza vengono visualizzati nuovamente quando vengono attivati.  

#### <a name="about"></a>Informazioni su
Visualizza informazioni sul Visualizzatore log del Supporto tecnico

#### <a name="close"></a>Chiudi
Chiude il Visualizzatore log del Supporto tecnico


### <a name="home-tab"></a><a name="bkmk_log-home"></a> Scheda Home

#### <a name="open-logs"></a>Open logs 
Il Supporto tecnico chiede di selezionare uno o più file di log da aprire.

Selezionare l'elenco a discesa nella parte inferiore del pulsante **Open logs** (Apri log) sulla barra multifunzione e selezionare una delle opzioni aggiuntive seguenti: 
- **Open logs in current view** (Apri i log nella visualizzazione corrente): consente di aprire i file di log selezionati nella visualizzazione corrente  
- **Open logs in new window** (Apri i log in una nuova finestra): consente di aprire i file di log selezionati in una nuova finestra del **Visualizzatore log**  

#### <a name="close-and-clear-logs"></a>Close and clear logs
Chiude tutti i file di log aperti e cancella le voci di file di log visualizzate nella finestra. Il Supporto tecnico non visualizzerà queste voci in futuro.

Selezionare l'elenco a discesa nella parte inferiore del pulsante **Close and clear logs** (Chiudi e cancella log) sulla barra multifunzione e selezionare una delle opzioni aggiuntive seguenti: 
- **Clear all entries** (Cancella tutte le voci): Cancella le voci di file di log visualizzate nella finestra. Il Supporto tecnico non visualizzerà queste voci in futuro.  
- **Close all logs** (Chiudi tutti i log): Chiude tutti i file di log aperti  

#### <a name="find"></a>Trova
Apre la finestra di dialogo**Find** (Trova). Immettere la stringa da cercare. Per evitare corrispondenze di stringhe brevi in altre stringhe, è possibile scegliere di cercare solo parole intere. È anche possibile cercare stringhe con distinzione tra maiuscole e minuscole.

#### <a name="find-next"></a>Trova successivo
Dopo aver trovato una corrispondenza per la stringa cercata, questa opzione consente di passare alla corrispondenza successiva.

#### <a name="find-previous"></a>Trova precedente
Dopo aver trovato due o più corrispondenze per la stringa cercata, questa opzione consente di passare alla corrispondenza precedente.

#### <a name="options"></a>Options

- **Live updating** (Aggiornamento in tempo reale): consente di monitorare le modifiche a un file di log attualmente aperto. Questa caratteristica non funziona quando sono aperti più file di log. Questa opzione è attivata per impostazione predefinita.  

- **Auto-scroll** (Scorrimento automatico): se è stata selezionata anche l'opzione **Live updating** (Aggiornamento in tempo reale), questa opzione abilita lo scorrimento automatico della visualizzazione del log in modo da mostrare le nuove voci. Questa caratteristica non funziona quando sono aperti più file di log. Questa opzione è attivata per impostazione predefinita.  

- **Show details** (Mostra dettagli): quando si seleziona un messaggio di un file di log, nella parte inferiore della scheda **Logs** (Log) vengono visualizzati i dettagli del messaggio. Questa opzione è attivata per impostazione predefinita.  

- **Quick filter** (Filtro rapido): consente di filtrare i messaggi dei file di log in tutti i file di log aperti per trovare una stringa specifica. È possibile filtrare in base al testo del log, al nome del componente e all'ID thread. Per trovare messaggi di log simili, è anche possibile fare clic con il pulsante destro del mouse su un messaggio di log e quindi selezionare **Quick Filter** (Filtro rapido) per il testo del log.  

- **Wrap log text** (Testo log a capo): consente di adattare all'interno di una colonna messaggi lunghi e su più righe. Questo comportamento rende più facile la lettura di tali messaggi. Questa opzione è attivata per impostazione predefinita.  

- **Raw log entry display** (Visualizzazione voci di registro non elaborate): consente di visualizzare righe di log non elaborate.  

- **Advanced filters** (Filtri avanzati): apre la finestra di dialogo **Advanced filters** (Filtri avanzati). Per altre informazioni, vedere [Filtri avanzati dei file di log](#bkmk_adv-filters).  

- **Error code links** (Collegamenti codici errore): i codici di errore nel testo dei log vengono evidenziati e resi selezionabili tramite clic. Questa opzione è attivata per impostazione predefinita.  

#### <a name="error-lookup"></a>Error lookup
Immettere un codice di errore per cercarlo nei file di log attualmente aperti. Usare i formati di codice di errore seguenti:
- **Intero a 32 bit (con segno)** : ad esempio, `-2147024891`  
- **Intero a 32 bit (senza segno)** : ad esempio, `2147942405`  
- **Esadecimale a 32 bit**: ad esempio, `0x80070005`  

#### <a name="decode-certificate"></a>Decode certificate
Nella finestra di dialogo **Decode certificate** (Decodifica certificato), incollare il valore del certificato serializzato per qualsiasi certificato presente nel client. Trovare questo valore nel Registro di sistema, nei file di log o in WMI. Selezionare **Process** (Elabora) per visualizzare informazioni generali e dettagli sul certificato. Queste informazioni includono il percorso di certificazione. Selezionare **Export** (Esporta) per esportare il certificato come file con estensione **cer**.



## <a name="advanced-log-file-filters"></a><a name="bkmk_adv-filters"></a> Filtri avanzati dei file di log

I filtri avanzati dei file di log consentono di includere, escludere o evidenziare stringhe specifiche. Queste stringhe possono trovarsi in un file di log o in un gruppo di file di log quando si esaminano voci di file di log. Quando si crea un filtro è possibile usare ricerche con caratteri jolly. È possibile salvare una combinazione di filtri utile come *set di filtri*. 

I filtri avanzati dei file di log prevalgono sui filtri rapidi. È possibile usarli entrambi contemporaneamente, ma i filtri rapidi si applicano solo ai dati di log visualizzati. I filtri avanzati determinano i dati visualizzati inizialmente prima che vengano applicati eventuali filtri rapidi.

Nella finestra di dialogo Advanced filters (Filtri avanzati) è possibile creare set di filtri complessi, che consentono di cercare stringhe all'interno di molti componenti di file di log, ovvero messaggi, thread, livelli di registrazione e componenti. Un set di filtri contiene più istruzioni di filtro per includere, escludere o evidenziare messaggi di file di log. Un filtro definisce una colonna dei file di log all'interno della quale cercare, un operatore e un valore. Il valore può contenere espressioni regolari, ad esempio il *carattere jolly*`*`.


### <a name="add-a-filter"></a>Aggiungere un filtro

1. Nella finestra del **Visualizzatore log** o nella scheda **Logs** (Log) del Supporto tecnico selezionare **Advanced filters** (Filtri avanzati).  

2. Nella finestra di dialogo Advanced filters (Filtri avanzati) selezionare **Add** (Aggiungi). Selezionare quindi una delle opzioni seguenti per agire sulle voci di log che soddisfano i criteri del filtro:  
    - **Include** (Includi)  
    - **Exclude** (Escludi)  
    - **Highlight** (Evidenzia)  

3. Nella finestra di dialogo **Advanced filter configuration** (Configurazione filtri avanzata) scegliere una colonna e un operatore:  

    - **Column** (Colonna): scegliere la colonna in cui cercare le stringhe che corrispondono al filtro:  

         - **Log Text** (Testo log): consente di cercare all'interno del testo di un file di log  

         - **Log severity** (Gravità log): cerca i log con un livello di gravità specifico. Impostare questi livelli di gravità nel campo **Value** (Valore).  

         - **Component** (Componente): cerca un componente specifico in base al nome  

         - **Thread ID** (ID thread): cerca messaggi di log con un ID thread specifico  

         - **Source file** (File di origine): cerca messaggi di log all'interno di un file di log specifico  

    - **Operator** (Operatore): scegliere un operatore per il filtro  

4. Immettere un valore per il filtro nel campo **Value** (Valore). Se il valore contiene espressioni regolari, selezionare **Enable regular expression matching** (Abilita corrispondenza espressioni regolari).  


### <a name="manage-filter-sets"></a>Gestire i set di filtri

- Per modificare un filtro, selezionare il filtro e quindi selezionare **Edit** (Modifica).  

- Per eliminare un filtro, selezionare il filtro e quindi selezionare **Delete** (Elimina).  

- Per cancellare tutti i filtri, selezionare **Clear** (Cancella).  

- Per salvare il set di filtri corrente, selezionare **Save filters** (Salva filtri) e quindi salvare il set di filtri come file con estensione **filterset**.  

- Per caricare un set di filtri salvato, selezionare **Load filters** (Carica filtri) e quindi passare a un file con estensione **filterset** salvato in precedenza.  



## <a name="support-center-viewer-reference"></a><a name="bkmk_viewer"></a> Informazioni di riferimento sul Visualizzatore del Supporto tecnico

Questa sezione descrive l'interfaccia utente dello strumento Configuration Manager **Support Center Viewer** . Le schede disponibili variano in base al contenuto del bundle di risoluzione dei problemi. Il [menu Window](#bkmk_viewer-window) (Finestra) e la [scheda Home](#bkmk_viewer-home) sono visualizzati per impostazione predefinita.
- [Menu Window](#bkmk_viewer-window) (Finestra)
- [Scheda Home](#bkmk_viewer-home)
- [Scheda Configuration](#bkmk_viewer-config) (Configurazione)
- [Scheda Logs](#bkmk_viewer-logs) (Log)
- [Scheda Debug dumps](#bkmk_viewer-debug) (Dump del debug)
- [Scheda WMI](#bkmk_viewer-wmi)
- [Scheda Registry](#bkmk_viewer-registry) (Registro di sistema)
- [Scheda Policy](#bkmk_viewer-policy) (Criteri)
- [Scheda Certificates](#bkmk_viewer-certs) (Certificati)
- [Scheda Troubleshooting](#bkmk_viewer-troubleshoot) (Risoluzione dei problemi)


### <a name="window-menu"></a><a name="bkmk_viewer-window"></a> Menu Window (Finestra)

Nell'angolo superiore sinistro della finestra del Visualizzatore del Supporto tecnico aprire questo menu selezionando la freccia nella casella blu.

#### <a name="open-bundle"></a>Open bundle (Apri bundle)
Passare al percorso di un bundle di dati creato dal Supporto tecnico.

#### <a name="about"></a>Informazioni su
Visualizza informazioni sul Visualizzatore del Supporto tecnico.

#### <a name="options"></a>Options
Nella finestra di dialogo **Options** è possibile:
- Ridurre il movimento degli elementi dell'interfaccia utente animati  
- Cambiare il percorso dei file temporanei    
- Reimpostare gli avvisi. Eventuali messaggi di avviso eliminati in precedenza vengono visualizzati nuovamente quando vengono attivati.  
- Reimpostare il percorso predefinito dei file temporanei, `%UserProfile%\AppData\Local\Microsoft\ConfigMgrSupportCenterViewer`  


#### <a name="exit"></a>Exit
Esce da Support Center Viewer


### <a name="home-tab"></a><a name="bkmk_viewer-home"></a> Scheda Home

#### <a name="open-bundle"></a>Open bundle (Apri bundle)
Passare al percorso di un bundle di dati creato dal Supporto tecnico.

#### <a name="open-log-file"></a>Open log file (Apri file di log)
Selezionare uno o più file di log da aprire.

#### <a name="decode-certificate"></a>Decode certificate
Nella finestra di dialogo **Decode certificate** (Decodifica certificato), incollare il valore del certificato serializzato per qualsiasi certificato presente nel client. Trovare questo valore nel Registro di sistema, nei file di log o in WMI. Selezionare **Process** (Elabora) per visualizzare informazioni generali e dettagli sul certificato. Queste informazioni includono il percorso di certificazione. Selezionare **Export** (Esporta) per esportare il certificato come file con estensione **cer**.


### <a name="configuration-tab"></a><a name="bkmk_viewer-config"></a> Scheda Configuration (Configurazione)

La scheda **Configuration** dello strumento Support Center Viewer fornisce le visualizzazioni seguenti usando dati provenienti dai provider WMI:

#### <a name="client"></a>Client
Questa visualizzazione illustra le stesse informazioni presenti nella scheda **Client** del Supporto tecnico.

#### <a name="operating-system"></a>Sistema operativo
Dettagli del sistema operativo client. Usa la classe [Win32_OperatingSystem](/windows/desktop/CIMWin32Prov/win32-operatingsystem).

#### <a name="computer"></a>Computer
Dettagli del computer client. Usa la classe [Win32_OperatingSystem](/windows/desktop/CIMWin32Prov/win32-operatingsystem).

#### <a name="services"></a>Servizi
Dettagli dei servizi in esecuzione nel computer client. Usa la classe [Win32_Service](/windows/desktop/CIMWin32Prov/win32-service).

#### <a name="network-adapters"></a>Schede di rete
Dettagli delle schede di rete installate nel computer client. Usa la classe [Win32_NetworkAdapterConfiguration](/windows/desktop/CIMWin32Prov/win32-networkadapterconfiguration).


### <a name="logs-tab"></a><a name="bkmk_viewer-logs"></a> Scheda Logs (Log)

La scheda **Logs** mostra un elenco dei file di log inclusi nel bundle. Ogni riga di questa scheda visualizza il percorso, il nome e le dimensioni del file di log. 

#### <a name="open"></a>Open
Dopo aver selezionato un file di log, selezionare questo pulsante per aprire il **Visualizzatore log**. Offre un subset delle funzionalità già esaminate per la scheda Logs (Log) del Supporto tecnico.

#### <a name="decode-certificate"></a>Decode certificate
Nella finestra di dialogo **Decode certificate** (Decodifica certificato), incollare il valore del certificato serializzato per qualsiasi certificato presente nel client. Trovare questo valore nel Registro di sistema, nei file di log o in WMI. Selezionare **Process** (Elabora) per visualizzare informazioni generali e dettagli sul certificato. Queste informazioni includono il percorso di certificazione. Selezionare **Export** (Esporta) per esportare il certificato come file con estensione **cer**.


### <a name="debug-dumps-tab"></a><a name="bkmk_viewer-debug"></a> Scheda Debug Dumps (Dump del debug)

Ogni riga di questa scheda fornisce dettagli sui file di dump del debug disponibili per l'esportazione. Usare questa scheda per esportare i file di dump del debug (con estensione dmp) per un'ulteriore analisi con uno strumento di debug, ad esempio WinDbg. 

> [!WARNING]  
> I dump del debug possono contenere informazioni riservate, ad esempio password, segreti di crittografia o dati utente. Raccogliere dump del debug solo dietro indicazione del personale del supporto tecnico Microsoft. I bundle di dati che contengono dump del debug devono essere gestiti con attenzione per garantirne la protezione da accessi non autorizzati.  

#### <a name="export"></a>Export
Consente di salvare una copia del file di dump del debug selezionato.


### <a name="wmi-tab"></a><a name="bkmk_viewer-wmi"></a> Scheda WMI

Questa scheda visualizza il set di dati WMI del client di Configuration Manager incluso nel bundle di dati. 

#### <a name="find"></a>Trova
Apre la finestra di dialogo Find (Trova), che include le funzionalità seguenti:  

- **Find what** (Trova): immettere la stringa da cercare nel set di dati WMI. I caratteri jolly sono supportati.  

- **Look at** (Cerca): scegliere se cercare nel set di dati WMI un **nome di classe o istanza**, una **proprietà** o un **valore** corrispondente.  

- **Match whole string only** (Solo stringa intera): per impostazione predefinita, vengono cercate le stringhe che contengono la stringa cercata. Selezionare questa casella di controllo per cercare solo le stringhe che corrispondono esattamente alla stringa inserita.  

#### <a name="find-next"></a>Trova successivo
Apre l'istanza successiva della stringa inserita nella finestra di dialogo di ricerca all'interno del set di dati WMI.

#### <a name="decode-certificate"></a>Decode certificate
Nella finestra di dialogo **Decode certificate** (Decodifica certificato), incollare il valore del certificato serializzato per qualsiasi certificato presente nel client. Trovare questo valore nel Registro di sistema, nei file di log o in WMI. Selezionare **Process** (Elabora) per visualizzare informazioni generali e dettagli sul certificato. Queste informazioni includono il percorso di certificazione. Selezionare **Export** (Esporta) per esportare il certificato come file con estensione **cer**.


### <a name="registry-tab"></a><a name="bkmk_viewer-registry"></a> Scheda Registry (Registro di sistema)

Usare la scheda **Registry** (Registro di sistema) per visualizzare i dati del Registro di sistema inclusi nel bundle di dati e per esportarli per un'ulteriore analisi.

#### <a name="export"></a>Export
Consente di salvare una copia della chiave del Registro di sistema e delle sottochiavi selezionate in un file del Registro di sistema (con estensione reg).

#### <a name="find"></a>Trova
Apre la finestra di dialogo Find (Trova), che include le funzionalità seguenti:  

- **Find what** (Trova): immettere la stringa da cercare nel set di dati WMI. I caratteri jolly sono supportati.  

- **Look at** (Cerca): scegliere se cercare nel set di dati WMI un **nome di classe o istanza**, una **proprietà** o un **valore** corrispondente.  

- **Match whole string only** (Solo stringa intera): per impostazione predefinita, vengono cercate le stringhe che contengono la stringa cercata. Selezionare questa casella di controllo per cercare solo le stringhe che corrispondono esattamente alla stringa inserita.  

#### <a name="find-next"></a>Trova successivo
Apre l'istanza successiva della stringa inserita nella finestra di dialogo di ricerca all'interno del set di dati WMI.

#### <a name="decode-certificate"></a>Decode certificate
Nella finestra di dialogo **Decode certificate** (Decodifica certificato), incollare il valore del certificato serializzato per qualsiasi certificato presente nel client. Trovare questo valore nel Registro di sistema, nei file di log o in WMI. Selezionare **Process** (Elabora) per visualizzare informazioni generali e dettagli sul certificato. Queste informazioni includono il percorso di certificazione. Selezionare **Export** (Esporta) per esportare il certificato come file con estensione **cer**.


### <a name="policy-tab"></a><a name="bkmk_viewer-policy"></a> Scheda Policy (Criteri)

La scheda **Policy** consente di visualizzare i dati sui criteri inclusi nel bundle di dati. 

#### <a name="find"></a>Trova
Apre la finestra di dialogo Find (Trova), che include le funzionalità seguenti:  

- **Find what** (Trova): immettere la stringa da cercare nel set di dati WMI. I caratteri jolly sono supportati.  

- **Look at** (Cerca): scegliere se cercare nel set di dati WMI un **nome di classe o istanza**, una **proprietà** o un **valore** corrispondente.  

- **Match whole string only** (Solo stringa intera): per impostazione predefinita, vengono cercate le stringhe che contengono la stringa cercata. Selezionare questa casella di controllo per cercare solo le stringhe che corrispondono esattamente alla stringa inserita.  

#### <a name="find-next"></a>Trova successivo
Apre l'istanza successiva della stringa inserita nella finestra di dialogo di ricerca all'interno del set di dati WMI.

#### <a name="decode-certificate"></a>Decode certificate
Nella finestra di dialogo **Decode certificate** (Decodifica certificato), incollare il valore del certificato serializzato per qualsiasi certificato presente nel client. Trovare questo valore nel Registro di sistema, nei file di log o in WMI. Selezionare **Process** (Elabora) per visualizzare informazioni generali e dettagli sul certificato. Queste informazioni includono il percorso di certificazione. Selezionare **Export** (Esporta) per esportare il certificato come file con estensione **cer**.


### <a name="certificates-tab"></a><a name="bkmk_viewer-certs"></a> Scheda Certificates (Certificati)

La scheda **Certificates** consente di visualizzare i certificati inclusi nel bundle di dati e di esportarli.

#### <a name="view-certificate"></a>View certificate (Visualizza certificato)
Visualizza informazioni sul certificato selezionato.

#### <a name="export"></a>Export
Apre la finestra di dialogo **Save as** (Salva con nome) per il salvataggio di una copia del certificato selezionato.


### <a name="troubleshooting-tab"></a><a name="bkmk_viewer-troubleshoot"></a> Scheda Troubleshooting (Risoluzione dei problemi)

Usare la scheda **Troubleshooting** (Risoluzione dei problemi) per visualizzare file di log creati con la scheda Troubleshooting (Risoluzione dei problemi) del Supporto tecnico.

#### <a name="view-log"></a>View log
Dopo aver selezionato una riga nella scheda **Troubleshooting** (Risoluzione dei problemi), selezionare questa opzione per visualizzare il file di log con il Visualizzatore log.