---
title: Avvisi e sistema di stato
titleSuffix: Configuration Manager
description: Configurare gli avvisi e usare il sistema di stato per rimanere aggiornati sullo stato della distribuzione di Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7341cc6e-9e08-41e4-bcc6-6c1ff12e85ca
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c066a61380e09961192bcbe7192e2e945341c97c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704279"
---
# <a name="use-alerts-and-the-status-system-for-configuration-manager"></a>Usare gli avvisi e il sistema di stato per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Configurare gli avvisi e usare il sistema di stato predefinito per rimanere aggiornati sullo stato della distribuzione di Configuration Manager.  


##  <a name="status-system"></a><a name="bkmk_Status"></a> Sistema di stato  
 Tutti i componenti principali del sito generano messaggi di stato che forniscono feedback e suggerimenti sulle operazioni del sito e della gerarchia.    Queste informazioni consentono di restare informati sull'integrità dei vari processi del sito. È possibile ottimizzare il sistema di avvisi per ignorare il disturbo prodotto da problemi noti, aumentando allo stesso tempo la visibilità tempestiva per altri problemi che potrebbero richiedere attenzione.  

 Per impostazione predefinita, il sistema di stato di Configuration Manager funziona senza configurazione usando impostazioni adatte alla maggior parte degli ambienti. Tuttavia, è possibile configurare quanto segue:  

-   **Generatori riepilogo dello stato:** è possibile modificare i generatori riepilogo dello stato in ogni sito per controllare la frequenza dei messaggi di stato che generano una modifica dell'indicatore di stato per i quattro generatori riepilogo seguenti:  

    -   Generatore riepilogo distribuzione applicazione  

    -   Generatore riepilogo statistiche applicazione  

    -   Generatore riepilogo dello stato dei componenti  

    -   Generatore riepilogo dello stato del sistema sito  

-   **Regole di filtro dello stato:** è possibile creare nuove regole di filtro dello stato, modificare la priorità delle regole, abilitare o disabilitare regole ed eliminare le regole inutilizzate presenti in ogni sito.  

    > [!NOTE]  
    >  Le regole di filtro dello stato non supportano l'utilizzo di variabili di ambiente per l'esecuzione di comandi esterni.  

-   **Creazione rapporti di stato:** è possibile configurare la creazione di report per componenti server e client per modificare il modo in cui i messaggi di stato vengono segnalati al sistema di stato di Configuration Manager e specificare dove inviare i messaggi di stato.  

    > [!WARNING]  
    >  Poiché le impostazioni di creazione rapporti predefinite sono adatte alla maggior parte degli ambienti, modificarle con cautela. Quando si aumenta il livello di creazione rapporti di stato scegliendo di includere nel rapporto tutti i dettagli dello stato, è possibile aumentare la quantità dei messaggi di stato da elaborare, che a sua volta aumenta il carico di elaborazione nel sito di Configuration Manager. Se si diminuisce il livello di creazione di rapporti di stato è possibile che venga limitata l'utilità dei generatori di riepilogo dello stato.  

Poiché il sistema di stato mantiene configurazioni separate per ogni sito è necessario modificare ogni singolo sito.  

###  <a name="procedures-for-configuring-the-status-system"></a><a name="bkmk_configstatus"></a> Procedure per la configurazione del sistema di stato  

##### <a name="to-configure-status-summarizers"></a>Per configurare i generatori di riepilogo dello stato  

1.  Nella console di Configuration Manager passare ad **Amministrazione** > **Configurazione del sito** >**Siti**, quindi selezionare il sito per cui configurare il sistema di stato.  

2.  Nella scheda **Home** , nel gruppo **Impostazioni** , fare clic su **Generatori di riepilogo dello stato**.  

3.  Nella finestra di dialogo **Generatori di riepilogo dello stato** selezionare il generatore che si desidera configurare e quindi fare clic su **Modifica** per aprire le proprietà di tale generatore. Se si sta modificando Distribuzione applicazioni o Generatore riepilogo statistiche applicazione, procedere con il passaggio 5. Se si sta modificando il direttamente lo stato del componente, andare al passaggio 6. Se si sta modificando il Generatore riepilogo dello stato del sistema del sito, andare al passaggio 7.  

4.  Dopo aver aperto la pagina delle proprietà per il generatore riepilogo distribuzione applicazione o statistiche applicazione, utilizzare la seguente procedura:  

    1.  Nella scheda **Generale** della pagina delle proprietà del generatore di riepilogo configurare gli intervallo di riepilogo, quindi fare clic su **OK** per chiudere la pagina delle proprietà.  

    2.  Fare clic su **OK** per chiudere la finestra di dialogo **Generatori riepilogo dello stato** e completare la procedura.  

5.  Dopo l'apertura delle pagine delle proprietà per il generatore di riepilogo dello stato del componente utilizzare la seguente procedura:  

    1.  Nella scheda **Generale** della pagina delle proprietà dei generatori di riepilogo configurare i valori del periodo di soglia e di replica.  

    2.  Nella scheda **Soglie** selezionare il **Tipo messaggio** che si desidera configurare, quindi fare clic sul nome di un componente nell'elenco **Soglie** .  

    3.  Nella finestra di dialogo **Proprietà soglia di stato** modificare i valori di soglia critico o avviso e quindi fare clic su **OK**.  

    4.  Ripetere i passaggi 6.b e 6.c in base alle necessità e dopo averli completati fare clic su **OK** per chiudere le proprietà del generatore di riepilogo.  

    5.  Fare clic su **OK** per chiudere la finestra di dialogo **Generatori riepilogo dello stato** e completare la procedura.  

6.  Dopo l'apertura delle pagine delle proprietà per il generatore di riepilogo dello stato del sistema sito utilizzare la seguente procedura:  

    1.  Nella scheda **Generale** della pagina delle proprietà dei generatori di riepilogo configurare i valori di pianificazione e replica.  

    2.  Nella scheda **Soglie** specificare i valori per le **Soglie predefinite** per configurare le soglie predefinite per la visualizzazione dello stato critico e di avviso.  

    3.  Per modificare i valori per **Oggetti archiviazione**specifici, specificare l'oggetto dall'elenco **Soglie specifiche** , quindi fare clic sul pulsante **Proprietà** per effettuare l'accesso e modificare la soglia critica e la soglia di avviso degli oggetti di archiviazione. Fare clic su **OK** per chiudere le proprietà degli oggetti di archiviazione.  

    4.  Per creare un nuovo oggetto di archiviazione, fare clic sul pulsante **Crea oggetto** e specificare i valori degli oggetti di archiviazione. Fare clic su **OK** per chiudere le proprietà degli oggetti di archiviazione.  

    5.  Per eliminare un oggetto di archiviazione, selezionare l'oggetto e quindi fare clic sul pulsante **Elimina** .  

    6.  Ripetere i passaggi da 7.b a 7.e se necessario. Al termine fare clic su **OK** per chiudere le proprietà del generatore di riepilogo.  

    7.  Fare clic su **OK** per chiudere la finestra di dialogo **Generatori riepilogo dello stato** e completare la procedura.  

##### <a name="to-create-a-status-filter-rule"></a>Per creare una regola di filtro dello stato  

1.  Nella console di Configuration Manager passare ad **Amministrazione** > **Configurazione del sito** >**Siti**, quindi selezionare il sito dove verrà configurato il sistema di stato.  

2.  Nella scheda **Home** , nel gruppo **Impostazioni** , fare clic su **Regole di filtro dello stato**. Verrà visualizzata la finestra di dialogo **Regole di filtro dello stato** .  

3.  Scegliere **Crea**.  

4.  Nella **Creazione guidata regola di filtro dello stato**nella pagina **Generale** specificare un nome per la nuova regola di filtro dello stato e per i criteri corrispondenti ai messaggi per la regola, quindi fare clic su **Avanti**.  

5.  Nella pagina **Azioni** specificare le azioni da eseguire quando un messaggio di stato corrisponde alla regola di filtro e quindi fare clic su **Avanti**.  

6.  Nella pagina **Riepilogo** esaminare i dettagli relativi alla nuova regola, quindi completare la procedura guidata.  

    > [!NOTE]  
    >  Configuration Manager richiede solo che la nuova regola di filtro dello stato abbia un nome. Se viene creata la regola ma non vengono specificati i criteri per l'elaborazione dei messaggi di stato, la regola di filtro dello stato non avrà alcun effetto. Questo comportamento consente di creare e organizzare le regole prima di configurare i criteri di filtro dello stato per ogni regola.  

##### <a name="to-modify-or-delete-a-status-filter-rule"></a>Per modificare o eliminare una regola di filtro dello stato  

1.  Nella console di Configuration Manager passare ad **Amministrazione** > **Configurazione del sito** >**Siti**, quindi selezionare il sito dove verrà configurato il sistema di stato.  

2.  Nella scheda **Home** , nel gruppo **Impostazioni** , fare clic su **Regole di filtro dello stato**.  

3.  nella finestra di dialogo **Regole di filtro dello stato** selezionare la regola che si desidera modificare, quindi eseguire una delle seguenti azioni:  

    -   Fare clic su **Aumenta priorità** o **Diminuisci priorità** per modificare l'ordine di elaborazione della regola di filtro dello stato. Selezionare quindi un'altra azione o passare al punto 8 della procedura per completare l'attività.  

    -   Fare clic su **Disattiva** o **Attiva** per modificare lo stato della regola. Dopo aver modificato lo stato della regola selezionare un'altra azione o passare al punto 8 della procedura per completare l'attività.  

    -   Fare clic su **Elimina** se si desidera eliminare la regola di filtro dello stato dal sito, quindi scegliere **Sì** per confermare l'azione. Dopo aver eliminato una regola selezionare un'altra azione o passare al punto 8 della procedura per completare l'attività.  

    -   Fare clic su **Modifica** se si desidera modificare i criteri per la regola del messaggio di stato, quindi passare al punto 5 di questa procedura.  

4.  Nella scheda **Generale** della finestra di dialogo delle proprietà della regola di filtro dello stato modificare la regola e i criteri corrispondenti ai messaggi.  

5.  Nella scheda **Azioni** modificare le azioni da eseguire quando un messaggio di stato corrisponde alla regola di filtro.  

6.  Fare clic su **OK** per salvare le modifiche.  

7.  Fare clic su **OK** per chiudere la finestra di dialogo **Regole di filtro dello stato** .  

##### <a name="to-configure-status-reporting"></a>Per configurare la creazione di rapporti di stato  

1.  Nella console di Configuration Manager passare ad **Amministrazione** > **Configurazione del sito** > **Siti**, quindi selezionare il sito dove si prevede di configurare il sistema di stato.  

2.  Nella scheda **Home** , nel gruppo **Impostazioni** , fare clic su **Configura componenti sito**, quindi selezionare **Creazione rapporti di stato**.  

3.  Nella finestra di dialogo **Proprietà componente per la creazione rapporti di stato** specificare i messaggi di stato dei componenti client e server che si desidera segnalare o registrare:  

    1.  Configurare un **Rapporto** per inviare messaggi di stato al sistema dei messaggi di stato di Configuration Manager.  

    2.  Configurare il **Registro** per scrivere il tipo e la gravità dei messaggi di stato nel registro eventi di Windows.  

4.  Fare clic su **OK**.  

###  <a name="monitor-the-status-system-of-configuration-manager"></a><a name="BKMK_MonitorSystemStatus"></a> Configurare il sistema di stato di Configuration Manager  
 Lo **stato del sistema** in Configuration Manager offre una panoramica delle operazioni generali dei siti e delle operazioni del server del sito della gerarchia. Consente di rilevare problemi operativi per i componenti o i server di sistema del sito, nonché di esaminare dettagli specifici per diverse operazioni di Configuration Manager. È possibile monitorare lo stato del sistema dal nodo **Stato del sistema** dell'area di lavoro **Monitoraggio** nella console di Configuration Manager.  

 La maggior parte dei componenti e dei ruoli del sistema del sito di Configuration Manager generano messaggi di stato. I dettagli relativi ai messaggi di stato vengono registrati nel log operativo di ciascun componente e vengono inviati al database del sito, in cui vengono riepilogati e presentati in un rollup generale sull'integrità di ciascun sistema del sito o componente. I rollup dei messaggi di stato forniscono informazioni dettagliate su avvisi e operazioni regolari, nonché dettagli sugli errori. È possibile configurare le soglie di avvio di avvisi o errori e mettere a punto il sistema affinché le informazioni di rollup ignorino i problemi noti non rilevanti per l'utente e segnalino i problemi effettivi nei server o le operazioni del componente che è consigliabile esaminare.  

 Lo stato del sistema viene replicato in altri siti in una gerarchia come dati del sito e non come dati globali. Di conseguenza è possibile visualizzare esclusivamente lo stato del sito a cui si connette la console di Configuration Manager e di tutti i siti figlio del sito. È consigliabile quindi valutare di connettere la console di Configuration Manager al sito di livello superiore della gerarchia per visualizzare lo stato del sistema.  

 Utilizzare la seguente tabella per identificare le varie visualizzazioni dello stato del sistema e capire quando utilizzarle.  

|Nodo|Altre informazioni|  
|----------|----------------------|  
|Stato del sito|Utilizzare questo nodo per visualizzare un rollup dello stato di ciascun sistema del sito e verificare l'integrità di ciascun server di sistema del sito. L'integrità del sistema del sito è determinata dalle soglie configurate per ciascun sito in **Generatore riepilogo dello stato del sistema sito**.<br /><br /> È possibile visualizzare messaggi di stato per ciascun sistema del sito, impostare le soglie per i messaggi di stato e gestire il funzionamento dei componenti nei sistemi del sito utilizzando **Configuration Manager Service Manager**.|  
|Stato componente|Usare questo nodo per visualizzare un rollup dello stato di ciascun componente di Configuration Manager e verificare l'integrità operativa del componente. L'integrità del componente è determinata dalle soglie configurate per ciascun sito in **Generatore riepilogo dello stato del componente**.<br /><br /> È possibile visualizzare messaggi di stato per ciascun componente, impostare le soglie per i messaggi di stato e gestire il funzionamento dei componenti utilizzando **Configuration Manager Service Manager**.|  
|Record in conflitto|Utilizzare questo nodo per visualizzare i messaggi di stato relativi ai client che potrebbero avere record in conflitto.<br /><br /> Configuration Manager usa l'ID hardware per tentare di identificare i client che potrebbero essere dei duplicati e avvertire l'utente dei record in conflitto. In caso di reinstallazione di un computer, ad esempio, l'ID hardware rimarrebbe lo stesso, mentre il GUID usato da Configuration Manager potrebbe cambiare.|  
|Query messaggi di stato|Utilizzare questo nodo per eseguire query nei messaggi di stato per eventi specifici e relativi dettagli. È possibile utilizzare le query messaggi di stato per individuare i messaggi di stato relativi a eventi specifici.<br /><br /> Spesso è possibile usare le query messaggi di stato per individuare il momento in cui uno specifico componente, operazione o oggetto di Configuration Manager è stato modificato, nonché l'account utilizzato per eseguire la modifica. È ad esempio possibile eseguire la query incorporata per **Raccolte create, modificate o eliminate** al fine di individuare il momento in cui una specifica raccolta è stata creata, nonché l'account utente utilizzato per creare la raccolta.|  

####  <a name="manage-site-status-and-component-status"></a><a name="bkmk_managestatus"></a> Gestire lo stato del sito e lo stato componente  
 Per gestire lo stato del sito e lo stato componente, utilizzare le seguenti informazioni:  

-   Per configurare le soglie per il sistema di stato, vedere [Procedure per la configurazione del sistema di stato](#bkmk_configstatus).  

-   Per gestire singoli componenti in Configuration Manager, usare **Configuration Manager Service Manager**.  

####  <a name="view-status-messages"></a><a name="bkmk_view"></a> Visualizzare i messaggi di stato  
 È possibile visualizzare i messaggi di stato per i singoli componenti e server di sistema del sito.  

 Per visualizzare i messaggi di stato nella console di Configuration Manager, selezionare un componente o un server di sistema del sito specifico e fare clic su **Mostra messaggi**. Per la visualizzazione dei messaggi, è possibile scegliere di visualizzare tipi di messaggi specifici o messaggi relativi a un periodo di tempo specifico, nonché filtrare i risultati n base ai dettagli dei messaggi di stato.  

##  <a name="alerts"></a><a name="bkmk_Alerts"></a> Avvisi  
 Gli avvisi di Configuration Manager vengono generati da alcune operazioni quando si verifica una condizione specifica.  

- In genere, gli avvisi vengono generati quando si verifica un errore che è necessario risolvere  

- Gli avvisi potrebbero essere generati per informare l'utente dell'esistenza di una condizione, per poter continuare a monitorare la situazione  

- Alcuni avvisi vengono configurati, ad esempio gli avvisi per lo stato di Endpoint Protection e del client, mentre altri avvisi vengono configurati automaticamente  

- È possibile configurare le sottoscrizioni agli avvisi che possono quindi inviare informazioni dettagliate via e-mail, aumentando la consapevolezza di problemi chiave  

  Usare la tabella seguente per trovare informazioni su come configurare gli avvisi e le sottoscrizioni di avvisi in Configuration Manager:  


|Action|Altre informazioni|  
|------------|----------------------|  
|Configurare gli avvisi di Endpoint Protection per una raccolta|Vedere **Come configurare gli avvisi per Endpoint Protection in Configuration Manager** in [Configurazione di Endpoint Protection](../../../protect/deploy-use/endpoint-protection-configure.md)|  
|Configurare gli avvisi di stato del client per una raccolta|Vedere [Come configurare lo stato del client](../../../core/clients/deploy/configure-client-status.md).|  
|Gestire gli avvisi di Configuration Manager|Vedere la sezione [Management tasks for alerts](#BKMK_Manage) in questo argomento.|  
|Configurare le sottoscrizioni e-mail agli avvisi|Vedere la sezione [Management tasks for alerts](#BKMK_Manage) in questo argomento.|  
|Avvisi di monitoraggio|Vedere la sezione [Avvisi di monitoraggio](#BKMK_MonitorAlerts)|  

###  <a name="management-tasks-for-alerts"></a><a name="BKMK_Manage"></a> Management tasks for alerts  

##### <a name="to-manage-general-alerts"></a>Per gestire gli avvisi generali  

1. Nella console di Configuration Manager passare a **Monitoraggio** > **Avvisi**, quindi selezionare un'attività di gestione.  

   Per altre informazioni sulle attività di gestione che potrebbero richiedere alcune informazioni prima della relativa selezione, usare la seguente tabella.  

|Attività di gestione|Dettagli|  
    |---------------------|-------------|  
    |**Configurare un**|Apre la finestra di dialogo *&lt;nome avviso*\>**Proprietà**, dove è possibile modificare il nome, la gravità e le soglie per l'avviso selezionato. Se si modifica il livello di gravità dell'avviso, questa configurazione influisce sulla modalità di visualizzazione degli avvisi nella console di Configuration Manager.|  
    |**Modifica commento**|Immettere un commento per gli avvisi selezionati. Questi commenti vengono visualizzati con l'avviso nella console di Configuration Manager.|  
    |**Rimanda**|Sospende il monitoraggio dell'avviso fino al raggiungimento della data specificata. In tale data lo stato dell'avviso viene aggiornato.<br /><br /> È possibile rimandare un avviso solo quando è abilitato.|  
    |**Crea sottoscrizione**|Apre la finestra di dialogo **Nuova sottoscrizione** dove è possibile creare una sottoscrizione e-mail all'avviso selezionato.|  

<!--##### To configure Endpoint Protection alerts for a collection  

1.  pending  -->

##### <a name="to-configure-client-status-alerts-for-a-collection"></a>Per configurare gli avvisi di stato del client per una raccolta  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità** >   **Raccolte dispositivi**.  

2.  Nell'elenco **Raccolte siti** selezionare la raccolta per cui si desiderano configurare gli avvisi e quindi nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

    > [!NOTE]  
    >  Non è possibile configurare avvisi per raccolte di utenti.  

3.  Nella scheda **Avvisi** della finestra di dialogo *&lt;Nome raccolta*\>**Proprietà** fare clic su **Aggiungi**.  

    > [!NOTE]  
    >  La scheda **Avvisi** viene visualizzata solo se il ruolo di sicurezza a cui si è associati dispone delle autorizzazioni per gli avvisi.  

4.  Nella finestra di dialogo **Aggiungi avvisi nuova raccolta** scegliere gli avvisi che si desidera generare quando le soglie di stato del client scendono sotto un valore specifico e quindi fare clic su **OK**.  

5.  Nell'elenco **Condizioni** della scheda **Avvisi** selezionare ogni avviso dello stato del client, quindi specificare le seguenti informazioni.  

    -   **Nome avviso**: accettare il nome predefinito o immettere un nuovo nome per l'avviso.  

    -   **Gravità avviso**: nell'elenco a discesa scegliere il livello di gravità che verrà visualizzato nella console di Configuration Manager.  

    -   **Genera avviso**: specificare la percentuale di soglia per l'avviso.  

6.  Fare clic su **OK** per chiudere la finestra di dialogo *&lt;Nome raccolta*\>**Proprietà**.  

##### <a name="to-configure-email-notification-for-alerts"></a>Per configurare la notifica degli avvisi e-mail  

1.  Nella console di Configuration Manager passare a **Monitoraggio** > **Avvisi** > **Sottoscrizioni**.  

2.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Configura notifica posta elettronica**.  

3.  Nella finestra di dialogo **Proprietà del componente di notifica e-mail** specificare le informazioni seguenti:  

    -   **Abilita notifiche e-mail per avvisi**: selezionare questa casella di controllo per abilitare in Configuration Manager l'uso di un server SMTP per inviare avvisi di posta elettronica.  

    -   **FQDN o indirizzo IP del server SMTP per inviare avvisi e-mail**: immettere il nome di dominio completo (FQDN) o l'indirizzo IP e la porta SMTP per il server e-mail che si vuole usare per questi avvisi.  

    -   **Account di connessione al server SMTP**: specificare il metodo di autenticazione per Configuration Manager da usare per connettere il server di posta elettronica.  

    -   **Indirizzo mittente per avvisi e-mail**: specificare l'indirizzo e-mail da cui vengono inviati gli avvisi e-mail.  

    -   **Verifica server SMTP**: invia un messaggio e-mail di verifica all'indirizzo e-mail specificato in **Indirizzo mittente per avvisi e-mail**.  

4.  Fare clic su **OK** per salvare le impostazioni e chiudere la finestra di dialogo **Proprietà del componente di notifica e-mail** .  

##### <a name="to-subscribe-to-email-alerts"></a>Per sottoscrivere gli avvisi e-mail  

1.  Nella console di Configuration Manager passare a **Monitoraggio** > **Avvisi**.  

2.  Selezionare un avviso e quindi fare clic su **Crea sottoscrizione** nel gruppo **Sottoscrizione** della scheda **Home**.  

3.  Nella finestra di dialogo **Nuova sottoscrizione** specificare le informazioni seguenti:  

    -   **Nome**: immettere un nome per identificare la sottoscrizione e-mail. È possibile usare fino a 255 caratteri.  

    -   **Indirizzo di posta elettronica**: immettere gli indirizzi e-mail a cui si vuole inviare l'avviso. È possibile separare più indirizzi e-mail con un punto e virgola.  

    -   **Lingua e-mail**: nell'elenco specificare la lingua per l'e-mail.  

4.  Fare clic su **OK** per chiudere la finestra di dialogo **Nuova sottoscrizione** e creare la sottoscrizione e-mail.  

    > [!NOTE]  
    >  È possibile eliminare e modificare le sottoscrizioni nell'area di lavoro **Monitoraggio** quando si espande il nodo **Avvisi** e quindi fare clic sul nodo **Sottoscrizioni** .  

###  <a name="monitor-alerts"></a><a name="BKMK_MonitorAlerts"></a> Avvisi di monitoraggio  
 È possibile visualizzare gli avvisi nel nodo **Avvisi** dell'area di lavoro **Monitoraggio** . Gli avvisi hanno uno degli stati di avviso seguenti:  

- **Mai attivato**: la condizione dell'avviso non è stata soddisfatta.  

- **Attivo**: la condizione dell'avviso è stata soddisfatta.  

- **Annullato**: la condizione di un avviso attivo non viene più soddisfatta. Questo stato indica che la condizione che ha generato l'avviso è stata risolta.  

- **Rimandato**: un utente amministratore ha configurato Configuration Manager per valutare lo stato dell'avviso in un secondo momento.  

- **Disabilitato**: l'avviso è stato disabilitato da un utente amministratore. Quando un avviso ha questo stato, Configuration Manager non aggiorna l'avviso nemmeno in caso di modifica dello stato.  

  Quando Configuration Manager genera un avviso è possibile eseguire una delle seguenti azioni:  

- Risolvere la condizione che ha generato l'avviso, ad esempio un problema di rete o un problema di configurazione. Quando Configuration Manager rileva che il problema non esiste più, lo stato dell'avviso viene modificato in **Annulla**.  

- Se l'avviso è un problema noto, è possibile rimandare l'avviso per un determinato periodo di tempo. In quel momento Configuration Manager aggiorna l'avviso allo stato corrente.  

   È possibile rimandare un avviso solo quando è attivo.  

- È possibile modificare il **Commento** di un avviso in modo che gli altri utenti amministratori vedano che l'utente è al corrente dell'avviso. Nel commento è ad esempio possibile individuare le modalità di risoluzione della condizione, fornire informazioni sullo stato corrente della condizione o spiegare perché l'avviso è stato rimandato.  
