---
title: Console di Configuration Manager
titleSuffix: Configuration Manager
description: Informazioni sull'esplorazione tramite la console di Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 463ce307-59dd-4abd-87b8-42ca9db178d7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f6bcd0bc06721fbd6ea3ce1226867db522bb2560
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700339"
---
# <a name="how-to-use-the-configuration-manager-console"></a>Come usare la console di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Gli amministratori usano la console di Configuration Manager per gestire l'ambiente di Configuration Manager. Questo articolo illustra le nozioni di base dell'esplorazione della console.  

## <a name="open-the-console"></a><a name="bkmk_open"></a> Aprire la console

La console di Configuration Manager viene sempre installata nel server del sito. È anche possibile installarla in altri computer. Per altre informazioni, vedere [Installare la console di Configuration Manager](../deploy/install/install-consoles.md).

Il metodo più semplice per aprire la console in un computer Windows 10 consiste nel premere **Start** e iniziare a digitare `Configuration Manager console`. Può non essere necessario digitare l'intera stringa per consentire a Windows di trovare la migliore corrispondenza.

Se si scorre il menu Start, cercare l'icona **Console di Configuration Manager** nel gruppo **Microsoft Endpoint Manager**.

![Icone del menu Start di Microsoft Endpoint Manager](media/microsoft-endpoint-manager-start-menu.png)

> [!NOTE]
> Nella versione 1910 il percorso del menu Start è stato modificato. Nella versione 1906 e precedenti, il nome della cartella è **System Center**. Quando si aggiorna Configuration Manager alla versione 1910 o successiva, assicurarsi di aggiornare la documentazione gestita internamente in modo da includere questo nuovo percorso.

## <a name="connect-to-a-site-server"></a>Connettersi a un server del sito

La console si connette al server di sito di amministrazione centrale o ai server del sito primario. Non è possibile connettere una console di Configuration Manager a un sito secondario. Durante l'installazione, è stato specificato il nome di dominio completo (FQDN) del server del sito a cui si connette la console.

Per connettersi a un server del sito diverso, eseguire questa procedura:

1. Selezionare la freccia nella parte superiore della [barra multifunzione](#ribbon) e scegliere **Connetti a un nuovo sito**.  

    ![Connettere la console a un nuovo sito](media/connect-to-a-new-site.png)  

2. Digitare il nome di dominio completo del server del sito. Se precedentemente ci si è connessi al server del sito, selezionare il server dall'elenco a discesa.  

    ![Nella finestra Connessione al sito immettere il nome di dominio completo del server del sito](media/site-server-fqdn.png)  

3. Selezionare **Connetti**.  

A partire dalla versione 1810, è possibile specificare il livello di autenticazione minimo per gli amministratori per l'accesso ai siti di Configuration Manager. Questa funzionalità impone agli amministratori di accedere a Windows con il livello richiesto. Per altre informazioni, vedere [Piano per il provider SMS](../../plan-design/hierarchy/plan-for-the-sms-provider.md#bkmk_auth). <!--1357013-->  

## <a name="navigation"></a>Spostamento

Alcune aree della console potrebbero non essere visibili a seconda del ruolo di sicurezza assegnato. Per altre informazioni sui ruoli, vedere [Nozioni fondamentali sull'amministrazione basata su ruoli](../../understand/fundamentals-of-role-based-administration.md).

### <a name="workspaces"></a>Aree di lavoro

La console di Configuration Manager ha quattro **aree di lavoro**:  

- **Asset e conformità**  

- **Raccolta software**  

- **Monitoraggio**  

- **Amministrazione**  

![Aree di lavoro di Configuration Manager con menu di scelta rapida](media/configuration-manager-workspaces.png)  

Riordinare i pulsanti delle aree di lavoro selezionando la freccia giù e scegliendo **Opzioni riquadro di spostamento**. Selezionare un elemento e fare clic su **Sposta su** o **Sposta giù**. Selezionare **Reimposta** per ripristinare l'ordine predefinito dei pulsanti.  

![Finestra Opzioni riquadro di spostamento per riordinare le aree di lavoro](media/navigation-pane-options.png)  

Ridurre a icona il pulsante di un'area di lavoro selezionando **Mostra meno pulsanti**. Prima viene ridotta a icona l'ultima area di lavoro dell'elenco. Selezionare un pulsante ridotto a icona e scegliere **Mostra più pulsanti** per ripristinare le dimensioni originali del pulsante.

![Aree di lavoro ridotte a icona nella console di Configuration Manager](media/workspace-buttons.png)  

### <a name="nodes"></a>Nodi

Le aree di lavoro sono una raccolta di **nodi**. Un esempio di nodo è il nodo **Gruppi di aggiornamenti software** nell'area di lavoro **Raccolta software**.

All'interno del nodo, è possibile selezionare la freccia per ridurre il riquadro di spostamento.  

![Nodo di esempio e freccia di riduzione evidenziata](media/software-update-groups-node.png)  

Usare la **barra di spostamento** per muoversi nella console quando si riduce a icona il riquadro di spostamento.  

![Riquadro di spostamento ridotto a icona di Configuration Manager](media/minimized-navigation-pane.png)  

Nella console i nodi in alcuni casi sono organizzati in cartelle. Quando si seleziona la cartella, in genere si visualizza un **indice di spostamento** o una **dashboard**.  

![Indice di spostamento degli aggiornamenti software per Configuration Manager](media/software-updates-navigation-index.png)  

### <a name="ribbon"></a>Barra multifunzione

La barra multifunzione è nella parte superiore della console di Configuration Manager. La barra multifunzione può avere più di una scheda e può essere ridotta a icona con la freccia sulla destra. I pulsanti sulla barra multifunzione sono diversi a seconda del nodo. La maggior parte dei pulsanti della barra multifunzione è disponibile anche nei menu di scelta rapida.  

![Barra multifunzione di esempio, evidenziazione di più schede e freccia di riduzione](media/ribbon.png)

### <a name="details-pane"></a>Riquadro dei dettagli

È possibile ottenere informazioni aggiuntive sugli elementi esaminando il riquadro dei dettagli. Il riquadro dei dettagli può avere una o più schede. Le schede variano a seconda del nodo.  

![Riquadro dei dettagli di esempio di Configuration Manager](media/details-pane.png)

### <a name="columns"></a>Colonne

È possibile aggiungere, rimuovere, riordinare e ridimensionare le colonne. Queste azioni consentono di visualizzare i dati che si preferisce. Le colonne disponibili variano a seconda del nodo. Per aggiungere o rimuovere una colonna dalla visualizzazione, fare clic con il pulsante destro del mouse sull'intestazione di una colonna esistente e selezionare un elemento. Riordinare le colonne trascinando l'intestazione di colonna nella posizione desiderata.  

![Aggiungere colonne in Configuration Manager](media/add-columns.png)  

Nella parte inferiore del menu di scelta rapida della colonna è possibile ordinare o raggruppare in base a una colonna. È anche possibile ordinare in base a una colonna selezionandone l'intestazione.  

![Raggruppare per colonna in Configuration Manager](media/column-group-by.png)  

## <a name="reclaim-lock-for-editing-objects"></a><a name="bkmk_sedo"></a> Richiamare il blocco per la modifica delle sequenze di attività

<!--4786915-->

Se la console di Configuration Manager non risponde, può essere bloccata la possibilità di apportare ulteriori modifiche fino al termine del blocco, dopo 30 minuti. Questo blocco fa parte del sistema di Configuration Manager SEDO (modifica serializzata di Distributed Objects). Per altre informazioni, vedere [Configuration Manager SEDO](../../../develop/core/understand/sedo.md).

A partire da [Current Branch versione 1906](../../plan-design/changes/whats-new-in-version-1906.md#reclaim-sedo-lock-for-task-sequences), è possibile cancellare il blocco su una sequenza di attività. A partire dalla versione 1910, è possibile cancellare il blocco su qualsiasi oggetto nella console di Configuration Manager.

Questa azione si applica solo al proprio account utente che ha il blocco e allo stesso dispositivo da cui il sito ha concesso il blocco. Quando si tenta di accedere a un oggetto bloccato, è ora possibile **rimuovere le modifiche** e continuare a modificare l'oggetto. Queste modifiche andrebbero perse comunque al termine del blocco.

## <a name="view-recently-connected-consoles"></a><a name="bkmk_viewconnected"></a> Visualizzare le console connesse di recente

<!--3699367-->
A partire dalla versione 1902, è possibile visualizzare le connessioni più recenti per la console di Configuration Manager. La visualizzazione include le connessioni attive e quelle stabilite di recente. Nell'elenco si vedrà sempre la connessione corrente alla console e si vedranno solo le connessioni dalla console di Configuration Manager. Non sarà possibile vedere le connessioni PowerShell o altre connessioni al provider SMS basate su SDK. Il sito rimuove dall'elenco le istanze anteriori a 30 giorni.

### <a name="prerequisites-to-view-connected-consoles"></a><a name="bkmk_connections-prereq"></a> Prerequisiti per visualizzare le console connesse

- Account con autorizzazione di **lettura** per l'oggetto **SMS_Site**

- Configurare l'API REST del servizio di amministrazione. Per altre informazioni, vedere [Che cos'è il servizio di amministrazione](../../../develop/adminservice/overview.md).

### <a name="view-connected-consoles"></a>Visualizzare le console connesse

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**.  

2. Espandere **Sicurezza** e selezionare il nodo **Connessioni di console**.  

3. Visualizzare le connessioni recenti, con le proprietà seguenti:  

    - Nome utente
    - Nome computer
    - Codice del sito connesso
    - Versione della console
    - Ora dell'ultima connessione: l'ultima volta che l'utente ha *aperto* la console
    - A partire dalla versione 1910, la colonna **Ultimo heartbeat della console** ha sostituito la colonna **Ora dell'ultima connessione**. <!--4923997-->
       - Una console aperta in primo piano invia un heartbeat ogni 10 minuti.

![Visualizzare le connessioni della console di Configuration Manager](media/console-connections.png)

## <a name="start-microsoft-teams-chat-from-console-connections"></a><a name="bkmk_message"></a> Avviare la chat di Microsoft Teams da connessioni della console
<!--4923997-->
*(Funzionalità introdotta nella versione 1910)*

A partire dalla versione 1910, è possibile inviare messaggi agli altri amministratori di Configuration Manager dal nodo **Connessioni di console** usando Microsoft Teams. Quando si sceglie **Avvia la chat di Microsoft Teams** per avviare una chat con un amministratore, viene avviato Microsoft Teams e viene aperta una chat con l'utente.

### <a name="prerequisites"></a>Prerequisiti

- Per avviare una chat con un amministratore, è necessario che l'account con cui si vuole chattare sia stato individuato con [Azure AD o l'individuazione dell'utente AD](../deploy/configure/about-discovery-methods.md#bkmk_aboutUser).
- Nel dispositivo da cui viene eseguita la console deve essere installato Microsoft Teams.
nota
- Tutti i [prerequisiti per visualizzare le console connesse](#bkmk_connections-prereq)

### <a name="start-microsoft-teams-chat"></a>Avviare la chat di Microsoft Teams

1. Passare ad **Amministrazione** > **Sicurezza** > **Connessioni di console**.
1. Fare clic con il pulsante destro del mouse sulla connessione di console di un utente e selezionare **Avvia la chat di Microsoft Teams**.
    - Se il nome dell'entità utente non viene trovato per l'amministratore selezionato, l'opzione **Avvia la chat di Microsoft Teams** è disattivata.
    - Viene visualizzato un messaggio di errore, incluso un collegamento per il download, se Microsoft Teams non è installato nel dispositivo da cui viene eseguita la console.
    - Se Microsoft Teams è installato nel dispositivo da cui viene eseguita la console, verrà aperta una chat con l'utente.

### <a name="known-issues"></a>Problemi noti

Il messaggio di errore che informa che Microsoft Teams non è installato non verrà visualizzato se la chiave del Registro di sistema seguente non esiste:

Computer\HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall

Per risolvere il problema, creare manualmente la chiave del Registro di sistema.

## <a name="configuration-manager-console-notifications"></a><a name="bkmk_notify"></a> Notifiche della console di Configuration Manager

<!--3556016, fka 1318035-->
A partire da Configuration Manager versione 1902, la console visualizza una notifica per gli eventi seguenti:

- Quando è disponibile un aggiornamento per Configuration Manager
- Quando nell'ambiente si verificano eventi di manutenzione e relativi al ciclo di vita

Queste notifiche sono visualizzate in una barra nella parte superiore della finestra della console sotto la barra multifunzione. Sostituiscono l'esperienza precedente che avvisava della disponibilità di aggiornamenti di Configuration Manager. Queste notifiche nella console visualizzano comunque informazioni critiche, ma non interferiscono con l'interazione tra utente e console. Le notifiche critiche non possono essere ignorate. Tutte le notifiche della console sono visualizzate in una nuova area di notifica della barra del titolo.

![Barra delle notifiche e flag nella console](./media/1318035-notify-eval-version-expired.png)

### <a name="configure-a-site-to-show-non-critical-notifications"></a>Configurare un sito per la visualizzazione delle notifiche non critiche

È possibile configurare ogni sito per la visualizzazione delle notifiche non critiche nelle proprietà del sito.

1. Nell'area di lavoro **Amministrazione** espandere **Configurazione sito** e quindi selezionare il nodo **Siti**.
1. Selezionare il sito che si vuole configurare per le notifiche non critiche.
1. Nella barra multifunzione selezionare **Proprietà**.
1. Nella scheda **Avvisi** selezionare l'opzione **Abilita le notifiche della console per modifiche non critiche all'integrità del sito**.
   - Se si abilita questa impostazione, tutti gli utenti vedranno le notifiche di livello critico, gli avvisi e le informazioni. Questa opzione è attivata per impostazione predefinita.  
   - Se si disabilita questa impostazione, gli utenti della console vedranno solo le notifiche di livello critico.  

La maggior parte delle notifiche della console sono relative alla sessione. La console valuta le query quando vengono avviate dall'utente. Per visualizzare le modifiche nelle notifiche, riavviare la console. Se un utente chiude una notifica critica, questa verrà inviata nuovamente al riavvio della console, purché sia ancora applicabile.

Le notifiche seguenti vengono rivalutate ogni cinque minuti:

- Il sito si trova in modalità di manutenzione  
- Il sito si trova in modalità di ripristino  
- Il sito si trova in modalità di aggiornamento  

Le notifiche seguono le autorizzazioni dell'amministrazione basata sui ruoli. Ad esempio, se un utente non dispone delle autorizzazioni per visualizzare gli aggiornamenti di Configuration Manager, l'utente non vedrà tali notifiche.

Alcune notifiche sono associate a un'azione. Ad esempio, se la versione della console non corrisponde alla versione del sito, selezionare **Install the new console version** (Installare la nuova versione della console). Questa azione avvia il programma di installazione della console.

Le notifiche seguenti sono applicabili in prevalenza al ramo Technical Preview:  

- La versione di valutazione ha una scadenza entro 30 giorni (Avviso): la data di scadenza della versione di valutazione è entro 30 giorni dalla data corrente  
- La versione di valutazione è scaduta (Errore critico): la data corrente è oltre la data di scadenza della versione di valutazione  
- Mancata corrispondenza con la versione della console (Errore critico): la versione della console non corrisponde alla versione del sito  
- Aggiornamento del sito disponibile (Avviso): è disponibile un nuovo pacchetto di aggiornamento  

Per altre informazioni e istruzioni per la risoluzione dei problemi, vedere il file **SmsAdminUI.log** nel computer della console. Per impostazione predefinita, questo file si trova nel percorso seguente: `C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\AdminUILog\SmsAdminUI.log`.


## <a name="in-console-documentation-dashboard"></a><a name="bkmk_doc-dashboard"></a> Dashboard della documentazione nella console

<!--3556019 FKA 1357546-->
A partire da Configuration Manager versione 1902, è disponibile il nodo **Documentazione** nella nuova area di lavoro **Community**. Questo nodo contiene informazioni aggiornate sulla documentazione di Configuration Manager e gli articoli del supporto tecnico. Include le sezioni seguenti:  

### <a name="product-documentation-library"></a>Libreria della documentazione del prodotto

- **Consigliato**: un elenco curato manualmente di articoli importanti.
- **Di tendenza**: gli articoli più visualizzati nell'ultimo mese.
- **Aggiornato di recente**: gli articoli rivisti nell'ultimo mese.

### <a name="support-articles"></a>Articoli del supporto tecnico

- **Articoli sulla risoluzione dei problemi**: procedure dettagliate guidate per la risoluzione dei problemi relativi a funzionalità e componenti di Configuration Manager.
- **Articoli del supporto tecnico nuovi e aggiornati**: articoli nuovi o aggiornati negli ultimi due mesi.

### <a name="troubleshooting-connection-errors"></a>Risoluzione dei problemi relativi agli errori di connessione
Il nodo **Documentazione** non ha configurazioni proxy esplicite. Usa qualsiasi proxy definito dal sistema operativo nell'applet del pannello di controllo **Opzioni Internet**. Per riprovare dopo un errore di connessione, aggiornare il nodo **Documentazione**.


## <a name="command-line-options"></a>Opzioni della riga di comando

La console di Configuration Manager include le seguenti opzioni della riga di comando:

|Opzione|Descrizione|  
|------------|-----------------|  
|`/sms:debugview=1`|Una DebugView viene inserita in tutte le ResultViews che specificano una visualizzazione. DebugView mostra le proprietà non elaborate (nomi e valori).|  
|`/sms:NamespaceView=1`|Mostra la visualizzazione dello spazio dei nomi nella console.|  
|`/sms:ResetSettings`|La console ignora la connessione permanente dell'utente e gli stati della visualizzazione. Le dimensioni della finestra non vengono reimpostate.|  
|`/sms:IgnoreExtensions`|Disabilita tutte le estensioni di Configuration Manager.|  
|`/sms:NoRestore`|La console ignora lo spostamento del nodo permanente precedente.|  


## <a name="tips"></a>Suggerimenti

### <a name="general"></a>Generale

#### <a name="improvements-to-console-search"></a><a name="bkmk_search"></a> Miglioramenti alla ricerca nella console
<!--4640570-->
*(Funzionalità introdotta nella versione 1910)*

- È possibile usare l'opzione di ricerca **Tutte le sottocartelle** dai nodi **Pacchetti driver** e **Query**.<!--2841181,5424892--> A partire dalla versione 2002, si può usare questa opzione anche dai nodi **Elementi di configurazione** e **Linee di base di configurazione**.<!--5891241-->

- Quando una ricerca restituisce più di 1000 risultati, è possibile selezionare il pulsante **OK** sulla barra di notifica per visualizzare altri risultati.<!--4640570-->

    ![Screenshot della barra di notifica per un numero eccessivo di risultati della ricerca](./media/4640570-search-too-many-results.png)

    > [!TIP]
    > Il limite predefinito per i risultati della ricerca è 1000. È possibile modificare questo valore predefinito. Nella console di Configuration Manager passare alla scheda **Ricerca** della barra multifunzione. Nel gruppo **Opzioni** selezionare **Impostazioni di ricerca**. Modificare il valore di **Risultati della ricerca**. Un numero maggiore di risultati della ricerca potrebbe richiedere più tempo per la visualizzazione.
    >
    > Per impostazione predefinita, il limite massimo superiore è 100.000. Per modificare questo limite, impostare il valore DWORD **QueryResultCountMaximum** nella chiave del Registro di sistema seguente:
    >
    > `HKEY_CURRENT_USER\Software\Microsoft\ConfigMgr10\AdminUI`
    >
    > L'impostazione nella console corrisponde al valore **QueryResultCountLimit** nella stessa chiave. Un amministratore può configurare questi valori nell'hive HKLM per tutti gli utenti del dispositivo. Il valore HKCU sostituisce l'impostazione HKLM.

#### <a name="role-based-administration-for-folders"></a>Amministrazione basata sui ruoli per le cartelle
<!--3600867-->
*(Funzionalità introdotta nella versione 1906)*

È possibile impostare gli ambiti di protezione nelle cartelle. Se si ha accesso a un oggetto nella cartella ma non si ha accesso alla cartella, non sarà possibile visualizzare l'oggetto. Analogamente, se si ha accesso a una cartella ma non a un oggetto all'interno della cartella, non sarà possibile visualizzare l'oggetto. Fare clic con il pulsante destro del mouse su una cartella, scegliere **Imposta ambiti di protezione** e quindi scegliere gli ambiti di protezione da applicare.

#### <a name="views-sort-by-integer-values"></a>L'ordinamento nelle viste si basa sui valori interi

*(Funzionalità introdotta nella versione 1902)*

Sono state migliorate le modalità di ordinamento dei dati nelle varie visualizzazioni. Nel nodo **Distribuzioni** dell'area di lavoro **Monitoraggio**, ad esempio, l'ordinamento nelle colonne seguenti si basa ora sui numeri invece che sui valori delle stringhe:  

- Numero errori
- Numero in corso
- Numero altri
- Numero riusciti
- Numero sconosciuti  

#### <a name="move-the-warning-for-a-large-number-of-results"></a>Spostare l'avviso per un numero elevato di risultati

*(Funzionalità introdotta nella versione 1902)*

Quando si seleziona un nodo della console che restituisce più di 1.000 risultati, Configuration Manager visualizza l'avviso seguente:

> Configuration Manager ha restituito un numero elevato di risultati. È possibile limitare i risultati con la ricerca oppure fare clic qui per visualizzare un massimo di 100000 risultati.

È ora presente uno spazio vuoto aggiuntivo tra questo avviso e il campo di ricerca. Questo spostamento impedisce di selezionare inavvertitamente l'avviso per visualizzare altri risultati.

#### <a name="send-feedback"></a>Inviare un feedback

*(Funzionalità introdotta nella versione 1806)*
<!--1357542-->

Inviare commenti e suggerimenti dalla console.  

- **Invia smile**: inviare commenti e suggerimenti su ciò che si è apprezzato  

- **Invia faccia imbronciata**: inviare commenti e suggerimenti su ciò che non si è apprezzato  

- **Invia un suggerimento**: consente di accedere a UserVoice per condividere la propria opinione  

Per altre informazioni, vedere [Commenti e suggerimenti sul prodotto](../../understand/find-help.md#BKMK_1806Feedback).


### <a name="assets-and-compliance-workspace"></a>Area di lavoro Asset e conformità

#### <a name="real-time-actions-from-device-lists"></a>Azioni in tempo reale dagli elenchi di dispositivi
<!--4616810-->
*(Funzionalità introdotta nella versione 1906)*

Esistono diversi modi per visualizzare un elenco di dispositivi nel nodo **Dispositivi** dell'area di lavoro **Asset e conformità**.

- Nell'area di lavoro **Asset e conformità** selezionare il nodo **Raccolte dispositivi**. Selezionare una raccolta di dispositivi e scegliere l'azione che consente di **visualizzare i membri**. Questa azione apre un sottonodo del nodo **Dispositivi** con un elenco di dispositivi per la raccolta.  

  - Quando si seleziona il sottonodo della raccolta, è ora possibile avviare **CMPivot** dal gruppo Raccolta della barra multifunzione.  

- Nell'area di lavoro **Monitoraggio** selezionare il nodo **Distribuzioni**. Selezionare una distribuzione e scegliere l'azione di **visualizzazione dello stato** nella barra multifunzione. Nel riquadro dello stato della distribuzione fare doppio clic sugli asset totali per eseguire il drill-through in un elenco di dispositivi.  

  - Quando si seleziona un dispositivo in questo elenco, è ora possibile avviare **CMPivot** ed **eseguire script** dal gruppo Dispositivi della barra multifunzione.  


#### <a name="collections-tab-in-devices-node"></a>Scheda Raccolte nel nodo Dispositivi
<!--4616810-->
*(Funzionalità introdotta nella versione 1906)*

Nell'area di lavoro **Asset e conformità** passare al nodo **Dispositivi** e selezionare un dispositivo. Nel riquadro dei dettagli passare alla nuova scheda **Raccolte**. Questa scheda contiene le raccolte che includono questo dispositivo. 

> [!Note]  
> - La scheda non è attualmente disponibile da un sottonodo dispositivi del nodo **Raccolte di dispositivi**. Ad esempio, quando si seleziona l'opzione che consente di **visualizzare i membri** per una raccolta.
> - Questa scheda potrebbe non essere popolata come previsto per alcuni utenti. Per visualizzare l'elenco completo delle raccolte a cui appartiene un dispositivo, è necessario avere il ruolo di sicurezza **Amministratore completo**. Si tratta di un problema noto. <!--5107309--> <!--5107309-->


#### <a name="add-smbios-guid-column-to-device-and-device-collection-nodes"></a>Aggiungi la colonna GUID SMBIOS ai nodi Dispositivo e Raccolta di dispositivi

*(Funzionalità introdotta nella versione 1906)*

<!--4526580-->
Nei nodi **Dispositivo** e **Raccolte di dispositivi** è ora possibile aggiungere una nuova colonna per **GUID SMBIOS**. Questo valore corrisponde alla proprietà **GUID BIOS** della classe Risorsa di sistema. Si tratta di un identificatore univoco dell'hardware del dispositivo.

#### <a name="search-device-views-using-mac-address"></a>Eseguire la ricerca nelle visualizzazioni dispositivi tramite indirizzi MAC

<!--3600878-->
*(Funzionalità introdotta nella versione 1902)*

È possibile cercare un indirizzo MAC in una visualizzazione dispositivi della console di Configuration Manager. Questa proprietà è utile per gli amministratori della distribuzione di sistemi operativi durante la risoluzione dei problemi delle distribuzioni basate su Pre-Boot eXecution Environment. Quando si visualizza un elenco di dispositivi, aggiungere la colonna **Indirizzo MAC** alla visualizzazione. Usare il campo di ricerca per aggiungere i criteri di ricerca **Indirizzo MAC**.

#### <a name="view-users-for-a-device"></a>Visualizzare gli utenti per un dispositivo

A partire dalla versione 1806, le colonne seguenti sono disponibili nel nodo **Dispositivi**:  

- **Utente/i primario** <!--1357280-->  

- **Utente attualmente connesso** <!--1358202-->  

    > [!NOTE]  
    > La visualizzazione dell'utente attualmente connesso richiede l'[individuazione dell'utente](../deploy/configure/configure-discovery-methods.md#bkmk_config-adud) e l'[affinità utente-dispositivo](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

Per altre informazioni su come visualizzare una colonna non predefinita, vedere [Colonne](#columns).

#### <a name="improvement-to-device-search-performance"></a>Miglioramento delle prestazioni di ricerca dei dispositivi

<!-- 3614690 -->
A partire dalla versione 1806, quando si esegue la ricerca in una raccolta di dispositivi, non viene eseguita la ricerca della parola chiave in tutte le proprietà degli oggetti. Quando non si specifica cosa cercare, la ricerca viene eseguita nelle quattro proprietà seguenti:

- Name
- Utente/i primario/i
- Utente attualmente connesso
- Nome utente ultimo accesso

Questo comportamento migliora significativamente il tempo necessario per le ricerche in base al nome, in particolare in un ambiente di grandi dimensioni. Le ricerche personalizzate in base a criteri specifici non sono interessate da questa modifica.


### <a name="software-library-workspace"></a>Area di lavoro Raccolta software

#### <a name="order-by-program-name-in-task-sequence"></a>Ordinare in base al nome del programma nella sequenza di attività
<!--4616810-->
*(Funzionalità introdotta nella versione 1906)*

Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi** e selezionare il nodo **Sequenze di attività**. Modificare una sequenza di attività e selezionare o aggiungere il passaggio [Installa pacchetto](../../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage). Se un pacchetto include più di un programma, l'elenco a discesa ora visualizza i programmi in ordine alfabetico.

#### <a name="task-sequences-tab-in-applications-node"></a>Scheda Sequenze di attività nel nodo Applicazioni
<!--4616810-->
*(Funzionalità introdotta nella versione 1906)*

Nell'area di lavoro **Raccolta software** espandere **Gestione applicazioni**, passare al nodo **Applicazioni** e selezionare un'applicazione. Nel riquadro dei dettagli passare alla nuova scheda **Sequenze di attività**. Questa scheda contiene le sequenze di attività che fanno riferimento a questa applicazione.

#### <a name="drill-through-required-updates"></a>Drill-through degli aggiornamenti obbligatori
<!--4224414-->
*(Funzionalità introdotta nella versione 1906)*

1. Nella console di Configuration Manager selezionare una delle seguenti posizioni:

   - **Raccolta software** > **Aggiornamenti software** > **Tutti gli aggiornamenti software**
   - **Raccolta software** > **Manutenzione pacchetti di Windows 10** > **Tutti gli aggiornamenti di Windows 10**
   - **Raccolta software** > **Gestione client di Office 365** > **Aggiornamenti di Office 365**

1. Selezionare tutti gli aggiornamenti richiesti da almeno un dispositivo.
1. Esaminare la scheda **Riepilogo** e individuare il grafico a torta in **Statistiche**.
1. Selezionare il collegamento ipertestuale **View Required** (Visualizza richiesto) accanto al grafico a torta per eseguire il drill-down nell'elenco dei dispositivi.
1. Questa azione consente di visualizzare un nodo temporaneo in **Dispositivi** dove è possibile visualizzare i dispositivi che richiedono l'aggiornamento. È anche possibile eseguire azioni per il nodo, come creare una nuova raccolta dall'elenco.


#### <a name="maximize-the-browse-registry-window"></a>Ingrandire la finestra Sfoglia Registro di sistema

<!--3594151 includes all MMS 1902 console changes-->
*(Funzionalità introdotta nella versione 1902)*

1. Nell'area di lavoro **Raccolta software** espandere **Gestione applicazioni** e quindi selezionare il nodo **Applicazioni**.
1. Selezionare un'applicazione con tipo di distribuzione basato su un metodo di rilevamento, ad esempio un metodo di rilevamento di Windows Installer.
1. Nel riquadro dei dettagli passare alla scheda **Tipi di distribuzione**.
1. Aprire le proprietà di un tipo di distribuzione e passare alla scheda **Metodo di rilevamento**. Selezionare **Aggiungi clausola**.
1. Impostare **Tipo di impostazione** su **Registro** e selezionare **Sfoglia** per aprire la finestra **Sfoglia Registro di sistema**. È ora possibile ingrandire questa finestra.  

#### <a name="edit-a-task-sequence-by-default"></a>Modificare una sequenza di attività per impostazione predefinita

*(Funzionalità introdotta nella versione 1902)*

Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi** e selezionare il nodo **Sequenze di attività**. **Modifica** è ora l'azione predefinita quando si apre una sequenza di attività. In precedenza l'azione predefinita era **Proprietà**.  

#### <a name="go-to-the-collection-from-an-application-deployment"></a>Passare alla raccolta dalla distribuzione di un'applicazione

*(Funzionalità introdotta nella versione 1902)*

1. Nell'area di lavoro **Raccolta software** espandere **Gestione applicazioni** e quindi selezionare il nodo **Applicazioni**.
1. Selezionare un'applicazione. Nel riquadro dei dettagli passare alla scheda **Distribuzioni**.
1. Selezionare una distribuzione e quindi scegliere la nuova opzione **Raccolta** nella barra multifunzione della scheda Distribuzione. Questa azione cambia la visualizzazione sostituendola con la raccolta di destinazione della distribuzione.
   - Questa azione è disponibile anche dal menu di scelta rapida che viene aperto facendo clic con il pulsante destro del mouse sulla distribuzione in questa visualizzazione.


### <a name="monitoring-workspace"></a>Area di lavoro di monitoraggio

#### <a name="correct-names-for-client-operations"></a>Nomi corretti per le operazioni client
<!--4616810-->
*(Funzionalità introdotta nella versione 1906)*

Nell'area di lavoro **Monitoraggio** espandere **Operazioni client**. L'operazione di **passaggio al punto di aggiornamento software successivo** è ora denominata in modo corretto.

#### <a name="show-collection-name-for-scripts"></a>Visualizzare il nome della raccolta per gli script
<!--4616810-->
*(Funzionalità introdotta nella versione 1906)*

Nell'area di lavoro **Monitoraggio** selezionare il nodo **Stato script**, che ora indica il **nome della raccolta** oltre all'ID.

#### <a name="remove-content-from-monitoring-status"></a>Rimuovere il contenuto dal monitoraggio dello stato

*(Funzionalità introdotta nella versione 1902)*

1. Nell'area di lavoro **Monitoraggio**, espandere **Stato distribuzione** e selezionare **Stato contenuto**.
1. Selezionare un elemento nell'elenco e scegliere l'opzione **Visualizza stato** nella barra multifunzione.
1. Nel riquadro Dettagli asset fare clic con il pulsante destro del mouse su un punto di distribuzione e scegliere la nuova opzione **Rimuovi**. Questa azione rimuove il contenuto dal punto di distribuzione selezionato.

#### <a name="copy-details-in-monitoring-views"></a>Copiare i dettagli nelle viste monitoraggio

*(Funzionalità introdotta nella versione 1806)*
<!--1357856-->
Copiare le informazioni dal riquadro **Dettagli asset** per i nodi di monitoraggio seguenti:  

- **Stato distribuzione contenuto**  

- **Stato distribuzione**  

![Vista Stato distribuzione, copiare i dettagli degli asset](media/1810-deployment-status.PNG)

### <a name="administration-workspace"></a>Area di lavoro Amministrazione

<!--4223683-->
A partire dalla versione 1906, è possibile abilitare alcuni nodi nel nodo **Protezione** per usare il servizio di amministrazione. Questa modifica consente alla console di comunicare con il provider SMS tramite HTTPS anziché tramite WMI. Per altre informazioni, vedere l'articolo sulla [configurazione del servizio di amministrazione](../../../develop/adminservice/set-up.md#bkmk_console).

## <a name="next-steps"></a>Passaggi successivi

[Funzionalità di accesso facilitato](../../understand/accessibility-features.md)

[Editor delle sequenze di attività](../../../osd/understand/task-sequence-editor.md#bkmk_conditions)
