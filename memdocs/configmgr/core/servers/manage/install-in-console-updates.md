---
title: Aggiornamenti nella console
titleSuffix: Configuration Manager
description: Installare gli aggiornamenti in Configuration Manager dal cloud Microsoft
ms.date: 06/02/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c14a3607-253b-41fb-8381-ae2d534a9022
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a0d7f36c921f782c0baad740d8e643f54cee0309
ms.sourcegitcommit: 5e339c07001e911cf75ef922e6c66a7efdeab6f1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/10/2020
ms.locfileid: "84637670"
---
# <a name="install-in-console-updates-for-configuration-manager"></a>Installare gli aggiornamenti nella console per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Configuration Manager si sincronizza con il servizio cloud Microsoft per ottenere aggiornamenti. Installare quindi tali aggiornamenti dalla console di Configuration Manager.

## <a name="get-available-updates"></a>Ottenere gli aggiornamenti disponibili

Il sito scarica solo gli aggiornamenti che si applicano all'infrastruttura e alla versione in uso. Questa sincronizzazione può essere automatica o manuale a seconda di come si configura il punto di connessione del servizio per la gerarchia:

- In **modalità online**il punto di connessione si connette automaticamente al servizio cloud Microsoft e scarica gli aggiornamenti applicabili.  

    Per impostazione predefinita, Configuration Manager verifica la disponibilità di nuovi aggiornamenti ogni 24 ore. Verificare manualmente la disponibilità di aggiornamenti nella console di Configuration Manager. Passare all'area di lavoro **Amministrazione**, selezionare il nodo **Aggiornamenti e manutenzione** e scegliere **Controlla la disponibilità di aggiornamenti** sulla barra multifunzione.  

- In **modalità offline**, il punto di connessione del servizio non si connette al servizio cloud Microsoft. Per scaricare e quindi importare gli aggiornamenti disponibili, [usare lo strumento di connessione del servizio](use-the-service-connection-tool.md).  

> [!NOTE]  
> Se necessario, importare le correzioni fuori programma nella console. A tal fine, usare lo [strumento di registrazione dell'aggiornamento](use-the-update-registration-tool-to-import-hotfixes.md). Le correzioni fuori programma completano gli aggiornamenti ottenuti quando si esegue la sincronizzazione con il servizio cloud Microsoft.  

Al termine della sincronizzazione degli aggiornamenti, visualizzarli nella console di Configuration Manager. Passare all'area di lavoro **Amministrazione** e selezionare il nodo **Aggiornamenti e manutenzione**.  

- Gli aggiornamenti non installati vengono visualizzati con l'indicazione **Disponibile**.  

- Gli aggiornamenti installati vengono visualizzati con l'indicazione **Installato**. Viene visualizzato solo l'aggiornamento installato più di recente. Per visualizzare gli aggiornamenti installati in precedenza, selezionare **Cronologia** sulla barra multifunzione.  

Prima di configurare il punto di connessione del servizio, esaminare e pianificare i relativi usi aggiuntivi. Gli usi riportati di seguito possono influire sulla modalità di configurazione di questo ruolo del sistema del sito:  

- Il sito usa il punto di connessione del servizio per caricare le informazioni di utilizzo relative al sito. Queste informazioni consentono al servizio cloud di Microsoft di identificare gli aggiornamenti disponibili per la versione corrente dell'infrastruttura. Per altre informazioni, vedere [Diagnostica e dati di utilizzo](../../plan-design/diagnostics/diagnostics-and-usage-data.md).  

Per comprendere meglio ciò che accade quando vengono scaricati gli aggiornamenti, vedere i diagrammi di flusso seguenti:  

- [Diagramma di flusso - scaricare gli aggiornamenti](download-updates-flowchart.md)  

- [Diagramma di flusso - replica di aggiornamento](update-replication-flowchart.md)  

## <a name="assign-permissions-to-view-and-manage-updates-and-features"></a>Assegnare le autorizzazioni per la visualizzazione e la gestione di aggiornamenti e funzionalità

Perché un utente possa visualizzare gli aggiornamenti nella console è necessario che disponga di un ruolo di protezione di amministrazione basato su ruoli che includa una classe di protezione denominata **Pacchetti di aggiornamento**. Questa classe consente l'accesso per visualizzare e gestire gli aggiornamenti nella console di Configuration Manager.

### <a name="about-the-update-packages-class"></a>Informazioni sulla classe Pacchetti di aggiornamento

Per impostazione predefinita, la classe **Pacchetti di aggiornamento** (SMS_CM_Updatepackages) fa parte dei seguenti ruoli di sicurezza predefiniti con le autorizzazioni elencate:  

- **Amministratore completo** con autorizzazioni **Modifica** e **Lettura** :  

  - Un utente con questo ruolo di sicurezza e l'accesso all'ambito di protezione **Tutto** può visualizzare e installare gli aggiornamenti. L'utente può anche abilitare le funzionalità durante l'installazione e abilitare singole funzionalità dopo l'aggiornamento del sito.  

  - Un utente con questo ruolo di sicurezza e l'accesso all'ambito di protezione **Predefinito** può visualizzare e installare gli aggiornamenti. L'utente può anche abilitare le funzionalità durante l'installazione e visualizzarle dopo l'aggiornamento del sito. Non può tuttavia abilitare le funzionalità dopo l'aggiornamento del sito.  

- **Analista di sola lettura** con autorizzazioni **Lettura** :  

  - Un utente con questo ruolo di sicurezza e l'accesso all'ambito **Predefinito** può visualizzare gli aggiornamenti ma non installarli. L'utente può anche visualizzare le funzionalità dopo l'aggiornamento del sito, ma non può abilitarle.  

### <a name="permissions-required-for-updates-and-servicing"></a>Autorizzazioni richieste per gli aggiornamenti e la manutenzione

- Usare un account a cui è assegnato un ruolo di sicurezza che include la classe **Pacchetti di aggiornamento** con entrambe le autorizzazioni **Modifica** e **Lettura**.  

- Assegnare l'account all'ambito **Predefinito**.  

### <a name="permissions-to-only-view-updates"></a>Autorizzazioni per la sola visualizzazione degli aggiornamenti

- Usare un account a cui è assegnato un ruolo di sicurezza che include la classe **Pacchetti di aggiornamento** con la sola autorizzazione **Lettura**.  

- Assegnare l'account all'ambito **Predefinito**.  

### <a name="permissions-required-to-enable-features-after-the-site-updates"></a>Autorizzazioni necessarie per abilitare le funzionalità dopo l'aggiornamento del sito

- Usare un account a cui è assegnato un ruolo di sicurezza che include la classe **Pacchetti di aggiornamento** con entrambe le autorizzazioni **Modifica** e **Lettura**.  

- Assegnare l'account all'ambito **Tutto**.  

## <a name="before-you-install-an-in-console-update"></a><a name="bkmk_beforeinstall"></a> Prima di installare un aggiornamento nella console  

Esaminare i passaggi seguenti prima di installare un aggiornamento dalla console di Configuration Manager.  

### <a name="step-1-review-the-update-checklist"></a><a name="bkmk_step1"></a> Passaggio 1: Esaminare l'elenco di controllo dell'aggiornamento  

Esaminare l'elenco di controllo dell'aggiornamento valido per le azioni da eseguire prima di iniziare l'aggiornamento:

- [Elenco di controllo per l'installazione dell'aggiornamento 2002](checklist-for-installing-update-2002.md)

- [Elenco di controllo per l'installazione dell'aggiornamento 1910](checklist-for-installing-update-1910.md)  

- [Elenco di controllo per l'installazione dell'aggiornamento 1906](checklist-for-installing-update-1906.md)  

- [Elenco di controllo per l'installazione dell'aggiornamento 1902](checklist-for-installing-update-1902.md)

### <a name="step-2-run-the-prerequisite-checker-before-installing-an-update"></a><a name="bkmk_step2"></a> Passaggio 2: Eseguire il controllo dei prerequisiti prima di installare un aggiornamento  

Prima di installare un aggiornamento, si consiglia di eseguire il controllo dei prerequisiti per l'aggiornamento. Se si esegue il prerequisito prima di installare un aggiornamento:  

- Il sito replica i file di aggiornamento in altri siti prima dell'installazione dell'aggiornamento.  

- Quando si sceglie di installare l'aggiornamento, il controllo dei prerequisiti viene eseguito di nuovo automaticamente.  

> [!NOTE]  
> Quando si avvia un controllo dei prerequisiti e quindi si visualizza lo stato, la fase **Installazione** risulta attiva. Il sito, tuttavia, non sta effettivamente installando l'aggiornamento. Per eseguire il controllo dei prerequisiti, il processo di aggiornamento estrae il pacchetto dalla raccolta contenuto e quindi lo inserisce in una cartella di gestione temporanea in cui può accedere ai controlli dei prerequisiti correnti. Quando si installa un aggiornamento, viene eseguito questo stesso processo. Questo comportamento è il motivo per cui la fase Installazione viene visualizzata come **In corso**. Solo il passaggio *Estrai aggiornamento* viene visualizzato nella categoria Installazione.  

Successivamente, quando si installa l'aggiornamento, è possibile configurarlo in modo che ignori gli avvisi del controllo dei prerequisiti.  

#### <a name="to-run-the-prerequisite-checker-before-installing-an-update"></a>Per eseguire il controllo dei prerequisiti prima di installare un aggiornamento  

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione** e selezionare il nodo **Aggiornamenti e manutenzione**.  

2. Selezionare il pacchetto di aggiornamento per cui si vuole eseguire il controllo dei prerequisiti.  

3. Selezionare **Esegui controllo prerequisiti** sulla barra multifunzione.  

    Quando si esegue il controllo dei prerequisiti, il contenuto dell'aggiornamento viene replicato nei siti figlio. Visualizzare **distmgr.log** nel server del sito per verificare che la replica del contenuto venga eseguita correttamente.  

4. Per visualizzare i risultati del controllo dei prerequisiti:  

    1. Nella console di Configuration Manager passare all'area di lavoro **Monitoraggio**.  

    2. Selezionare il nodo **Stato di aggiornamenti e manutenzione** e cercare lo stato dei prerequisiti.  

    3. Per altre informazioni, visualizzare **ConfigMgrPrereq.log** nel server del sito.  

## <a name="install-in-console-updates"></a><a name="bkmk_install"></a> Installare gli aggiornamenti nella console  

Quando si è pronti per installare gli aggiornamenti dalla console di Configuration Manager, iniziare con il sito principale della gerarchia. Questo è il sito di amministrazione centrale o un sito primario autonomo.  

Installare l'aggiornamento fuori dal normale orario di ufficio per ogni sito per ridurre l'impatto sulle attività aziendali. L'installazione dell'aggiornamento può includere azioni come la reinstallazione dei componenti e dei ruoli del sistema del sito.  

- I siti primari figlio avviano automaticamente l'aggiornamento al termine della relativa installazione nel sito di amministrazione centrale. Questo processo è predefinito e consigliato. Per controllare quando verranno installati gli aggiornamenti in un sito primario, usare gli [intervalli di servizio per i server del sito](service-windows.md).  

- Al termine dell'aggiornamento del sito primario padre, aggiornare manualmente i siti secondari dalla console di Configuration Manager. L'aggiornamento automatico dei server dei siti secondari non è supportato.  

- Quando si usa una console di Configuration Manager dopo l'aggiornamento del sito, verrà richiesto di aggiornare la console.  

- Dopo che il server del sito ha completato correttamente l'installazione di un aggiornamento, aggiorna automaticamente tutti i ruoli del sistema del sito applicabili. La reinstallazione e la disconnessione per l'aggiornamento, tuttavia, non vengono eseguite contemporaneamente in tutti i punti di distribuzione. Il server del sito usa le impostazioni di distribuzione del contenuto del sito stesso per distribuire l'aggiornamento a un subset di punti di distribuzione alla volta. Ne consegue che solo alcuni punti di distribuzione saranno offline per consentire l'installazione dell'aggiornamento. I punti di distribuzione in cui non è stato avviato l'aggiornamento o in cui è stato completato restano online e possono continuare a fornire contenuto ai client.

### <a name="overview-of-in-console-update-installation"></a><a name="bkmk_overview"></a> Panoramica dell'installazione degli aggiornamenti nella console  

#### <a name="1-when-the-update-installation-starts"></a>1. Quando viene avviata l'installazione dell'aggiornamento

Viene visualizzato l'Aggiornamento guidato con un elenco delle aree del prodotto a cui si applica l'aggiornamento.  

- Nella pagina **Generale** della procedura guidata configurare **Avvisi relativi ai prerequisiti** in base alle esigenze:  

  - Gli errori relativi ai prerequisiti arrestano sempre l'installazione dell'aggiornamento. Correggere gli errori prima di ritentare l'installazione dell'aggiornamento. Per altre informazioni, vedere [Ripetere l'installazione di un aggiornamento non riuscito](#bkmk_retry) .  

  - Gli avvisi relativi ai prerequisiti possono anche arrestare l'installazione dell'aggiornamento. Risolvere gli avvisi prima di ritentare l'installazione dell'aggiornamento. Per altre informazioni, vedere [Ripetere l'installazione di un aggiornamento non riuscito](#bkmk_retry) .  

  - **Ignorare eventuali avvisi del controllo dei prerequisiti e installare questo aggiornamento anche in caso di requisiti mancanti**: impostare una condizione affinché l'installazione dell'aggiornamento ignori gli avvisi relativi ai prerequisiti. Questa opzione consente all'installazione dell'aggiornamento di continuare. Se non si seleziona questa opzione, l'installazione dell'aggiornamento si interrompe se viene generato un avviso nel processo. Non usare questa opzione a meno che il controllo dei prerequisiti non sia stato eseguito in precedenza e non siano già stati corretti gli avvisi relativi ai prerequisiti per un sito.  

    Nelle aree di lavoro **Amministrazione** e **Monitoraggio**, il nodo Aggiornamenti e manutenzione include un pulsante denominato **Ignora avvisi dei prerequisiti** sulla barra multifunzione. Questo pulsante diventa disponibile quando non viene completata l'installazione di un pacchetto di aggiornamento a causa di avvisi del controllo dei prerequisiti. Ad esempio, dall'Aggiornamento guidato si installa un aggiornamento senza usare l'opzione per ignorare gli avvisi dei prerequisiti. L'installazione dell'aggiornamento si interrompe con uno stato di avviso dei prerequisiti ma senza errori. Successivamente, selezionare **Ignora avvisi dei prerequisiti** sulla barra multifunzione. questa azione attiva la continuazione automatica dell'installazione dell'aggiornamento e gli avvisi relativi ai prerequisiti vengono ignorati. Quando si usa questa opzione l'installazione dell'aggiornamento continua automaticamente dopo alcuni minuti.  

- Se un aggiornamento si applica al client di Configuration Manager, scegliere di testare l'aggiornamento con un set limitato di client. Per altre informazioni, vedere [Come testare gli aggiornamenti client in una raccolta di pre-produzione](../../clients/manage/upgrade/test-client-upgrades.md).  

#### <a name="2-during-the-update-installation"></a>2. Durante l'installazione dell'aggiornamento

Nell'ambito dell'installazione dell'aggiornamento, Configuration Manager esegue queste azioni:  

- Reinstalla tutti i componenti interessati, ad esempio i ruoli del sistema del sito o la console di Configuration Manager.  

- Gestisce gli aggiornamenti dei client in base alle selezioni effettuate per la distribuzione pilota del client e per gli [aggiornamenti automatici del client](../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate).  

- Nell'ambito dell'aggiornamento non è in genere necessario riavviare i server del sistema del sito. Se un ruolo usa .NET e il pacchetto aggiorna tale componente prerequisito, il sistema del sito potrebbe essere riavviato.  

> [!TIP]  
> Quando si installano aggiornamenti di Configuration Manager, il sito aggiorna anche la cartella CD.Latest. Per altre informazioni, vedere [Cartella CD.Latest](the-cd.latest-folder.md).  

#### <a name="3-monitor-the-progress-of-updates-as-they-install"></a>3. Monitorare lo stato di avanzamento degli aggiornamenti durante l'installazione

Per monitorare lo stato di avanzamento, eseguire questi passaggi:  

- Nella console di Configuration Manager passare all'area di lavoro **Amministrazione** e selezionare il nodo **Aggiornamenti e manutenzione**. Questo nodo mostra lo stato di installazione di tutti i pacchetti di aggiornamento.  

- Nella console di Configuration Manager passare all'area di lavoro **Monitoraggio** e selezionare il nodo **Stato di aggiornamenti e manutenzione**. Questo nodo mostra lo stato di installazione solo del pacchetto di aggiornamento corrente che il sito sta installando.  

    L'installazione dell'aggiornamento è divisa in diverse fasi per facilitare il monitoraggio. Per ognuna delle fase seguenti, i dettagli aggiuntivi riportati nello stato di installazione includono il file di log da visualizzare per altre informazioni.  

  - **Download**: questa fase si applica solo al sito principale con il punto di connessione del servizio.

  - **Replica**

  - **Controllo dei prerequisiti**

  - **Installazione**

  - **Post-installazione**: per altre informazioni, vedere [Attività post-installazione](#post-installation-tasks).  

- Visualizzare il file **CMUpdate.log** disponibile in `<ConfigMgr_Installation_Directory>\Logs` nel server del sito.  

>[!NOTE]
> A partire dalla versione 1906 è possibile visualizzare lo stato dell'attività **Aggiorna database di ConfigMgr** durante la fase di **installazione**.
>
> - Se l'aggiornamento del database è bloccato, viene visualizzato l'avviso **In corso, Richiesta attenzione**.
>   - cmupdate.log registrerà il nome del programma e l'ID sessione SQL che blocca l'aggiornamento del database.
> - Quando l'aggiornamento del database non sarà più bloccato, lo stato verrà reimpostato su **In corso** o **Completato**.
>   - Quando l'aggiornamento del database è bloccato, viene effettuato un controllo ogni 5 minuti per verificare se è ancora bloccato.

#### <a name="4-when-the-update-installation-completes"></a>4. Quando viene completata l'installazione dell'aggiornamento

Quando viene completata l'installazione dell'aggiornamento del primo sito:  

- I siti primari figlio installano automaticamente l'aggiornamento. Non è richiesta alcuna azione ulteriore.  

- Aggiornare manualmente i siti secondari dalla console di Configuration Manager. Per altre informazioni, vedere [Per avviare l'installazione dell'aggiornamento in un sito secondario](#bkmk_secondary).  

- Finché tutti i siti della gerarchia non vengono aggiornati alla nuova versione, la gerarchia funziona in modalità mista. Per altre informazioni, vedere [Interoperabilità tra versioni diverse](../../plan-design/hierarchy/interoperability-between-different-versions.md).  

#### <a name="5-update-configuration-manager-consoles"></a>5. Aggiornare le console di Configuration Manager

Dopo l'aggiornamento di un sito di amministrazione centrale o di un sito primario, è necessario aggiornare anche tutte le console di Configuration Manager che si connettono al sito. Viene richiesto di aggiornare una console:  

- Quando si apre la console  

- Quando si passa a un nuovo nodo in una console aperta  

Aggiornare la console subito dopo l'aggiornamento del sito.  

Dopo aver completato l'aggiornamento della console, verificare che le versioni della console e del sito siano corrette. Nella console passare a **Informazioni su Configuration Manager** nell'angolo in alto a sinistra.  

> [!Note]  
> La versione della console è leggermente diversa da quella del sito. La versione secondaria della console corrisponde alla versione finale di Configuration Manager. Ad esempio, in Configuration Manager versione 1802 la versione iniziale del sito è 5.0.8634.1000 e la versione iniziale della console è 5.**1802**.1082.1700. Con i futuri hotfix è possibile che i numeri di build (1082) e revisione (1700) cambino.

### <a name="to-start-the-update-installation-at-the-top-level-site"></a><a name="bkmk_toptier"></a> Per avviare l'installazione dell'aggiornamento nel sito principale  

Nel sito principale della gerarchia passare all'area di lavoro **Amministrazione** nella console di Configuration Manager e selezionare il nodo **Aggiornamenti e manutenzione**. Selezionare un aggiornamento con lo stato **Disponibile** e quindi scegliere **Installa pacchetto di aggiornamento** sulla barra multifunzione.  

### <a name="to-start-the-update-installation-at-a-secondary-site"></a><a name="bkmk_secondary"></a> Per avviare l'installazione dell'aggiornamento in un sito secondario  

Dopo l'aggiornamento del sito primario padre di un sito secondario, aggiornare il sito secondario dalla console di Configuration Manager. A tale scopo, usare l' **aggiornamento guidato per i siti secondari**.  

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito** e selezionare **Siti**. Selezionare il sito secondario da aggiornare e quindi scegliere **Aggiorna** sulla barra multifunzione.  

2. Selezionare **Sì** per avviare l'aggiornamento del sito secondario.  

Per monitorare l'installazione dell'aggiornamento in un sito secondario, selezionare il sito secondario e scegliere **Mostra stato installazione** sulla barra multifunzione. Aggiungere anche la colonna **Versione** al nodo Siti per poter visualizzare la versione di ogni sito secondario.  

In alcuni casi, lo stato nella console non viene aggiornato o indica che l'aggiornamento non è riuscito. Al termine dell'aggiornamento di un sito secondario, usare l'opzione **Riprova installazione**. Questa opzione non reinstalla l'aggiornamento in un sito secondario in cui è stato installato correttamente, ma forza l'aggiornamento dello stato nella console.

### <a name="post-installation-tasks"></a>Operazioni successive all'installazione

Quando un sito installa un aggiornamento, diverse attività non possono essere avviate finché non viene completata l'installazione dell'aggiornamento nel server del sito. L'elenco include le attività successive all'installazione fondamentali per le operazioni sul sito e sulla gerarchia. Dato che sono fondamentali, vengono monitorate attivamente. Le attività aggiuntive che non vengono monitorate direttamente includono la reinstallazione dei ruoli del sistema del sito. Per visualizzare lo stato delle attività successive all'installazione fondamentali, selezionare l'attività **Dopo l'installazione** durante il monitoraggio dell'installazione dell'aggiornamento di un sito.

Non tutte le attività vengono completate immediatamente. Alcune non vengono avviate fino a quando l'installazione dell'aggiornamento non viene completata in ogni sito. Le nuove funzionalità previste potrebbero risultare ritardate fino al completamento di queste attività. L'attivazione delle nuove funzionalità viene avviata solo al termine dell'installazione dell'aggiornamento in tutti i siti e queste funzionalità potrebbero quindi non essere visibili per qualche tempo.

Le attività di post-installazione includono:

- **Installazione del servizio SMS_EXECUTIVE**

  - Servizio critico eseguito nel server del sito.
  - La reinstallazione di questo servizio viene completata rapidamente.

- **Installazione del componente SMS_DATABASE_NOTIFICATION_MONITOR**

  - Thread del componenti critico del sito del servizio SMS_EXECUTIVE.
  - La reinstallazione di questo servizio viene completata rapidamente.

- **Installazione del componente SMS_HIERARCHY_MANAGER**

  - Componente critico del sito eseguito nel server del sito.
  - Responsabile della reinstallazione dei ruoli nei server del sistema del sito. Lo stato della reinstallazione dei singoli ruoli del sistema del sito non viene visualizzato.
  - La reinstallazione di questo servizio viene completata rapidamente.

    > [!Note]
    > Alcuni ruoli del sito di Configuration Manager condividono il framework client. Ad esempio, il punto di gestione e il punto di distribuzione pull. Quando questi ruoli vengono aggiornati, viene aggiornata contemporaneamente la versione client in questi server. Per altre informazioni, vedere [Come aggiornare i client](../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md).

- **Installazione del componente SMS_REPLICATION_CONFIGURATION_MONITOR**

  - Componente critico del sito eseguito nel server del sito.
  - La reinstallazione di questo servizio viene completata rapidamente.

- **Installazione del componente SMS_POLICY_PROVIDER**

  - Componente critico del sito eseguito solo nei siti primari.
  - La reinstallazione di questo servizio viene completata rapidamente.

- **Monitoraggio dell'inizializzazione della replica**

  - Questa attività viene visualizzata solo nel sito di amministrazione centrale e nei siti primari figlio.
  - Dipende da SMS_REPLICATION_CONFIGURATION_MONITOR.
  - Viene completata rapidamente.

- **Aggiornamento del pacchetto di pre-produzione client di Configuration Manager**

  - Questa attività viene visualizzata anche quando l'uso della pre-produzione client, anche detta distribuzione pilota del client, non è abilitato.
  - Viene avviata solo al termine dell'installazione dell'aggiornamento in tutti i siti della gerarchia.

- **Aggiornamento della cartella Client nel server del sito**

  - Questa attività non viene visualizzata se si usa il client in pre-produzione.  
  - Viene completata rapidamente.

- **Aggiornamento del pacchetto client di Configuration Manager**

  - Questa attività non viene visualizzata se si usa il client in pre-produzione.  
  - Termina solo quando tutti i siti hanno installato l'aggiornamento.  

- **Attivazione delle funzionalità**

  - Questa attività viene visualizzata solo nel sito di livello superiore della gerarchia.
  - Viene avviata solo al termine dell'installazione dell'aggiornamento in tutti i siti della gerarchia.
  - Non vengono visualizzate le singole funzionalità.

## <a name="retry-installation-of-a-failed-update"></a><a name="bkmk_retry"></a> Ripetere l'installazione di un aggiornamento non riuscito  

Quando l'installazione di un aggiornamento non riesce, esaminare i commenti nella console per individuare le possibili soluzioni per gli errori e gli avvisi. Per altri dettagli, visualizzare **ConfigMgrPrereq.log** nel server del sito. Prima di riprovare l'installazione di un aggiornamento, è necessario correggere gli errori ed è consigliabile correggere anche gli avvisi.  

> [!TIP]  
> In caso di problemi durante il download o la replica di un aggiornamento, usare lo [strumento di reimpostazione dell'aggiornamento](update-reset-tool.md).  

Quando si è pronti per ripetere l'installazione di un aggiornamento, selezionare l'aggiornamento non riuscito e quindi scegliere un'opzione applicabile. Il nuovo tentativo di installazione dell'aggiornamento varia a seconda del nodo da cui viene riprovato e dal tipo di tentativo usato.  

### <a name="retry-installation-for-the-hierarchy"></a>Riprovare l'installazione per la gerarchia

Ripetere l'installazione di un aggiornamento per l'intera gerarchia quando l'aggiornamento è in uno degli stati seguenti:  

- Controlli dei prerequisiti superati con uno o più avvisi e opzione per ignorare gli avvisi di controllo dei prerequisiti non impostata nell'Aggiornamento guidato. Il valore di **Ignora avviso prerequisito** per l'aggiornamento nel nodo **Aggiornamenti e manutenzione** è **No**.

- Il prerequisito non è riuscito

- L'installazione non è riuscita  

- La replica del contenuto nel sito non è riuscita

Passare all'area di lavoro **Amministrazione** e selezionare il nodo **Aggiornamenti e manutenzione**. Selezionare l'aggiornamento e quindi scegliere una delle opzioni seguenti.  

- **Riprova**: quando si **riprova** da **Aggiornamenti e manutenzione**, viene avviata nuovamente l'installazione dell'aggiornamento e vengono automaticamente ignorati gli avvisi relativi ai prerequisiti. Se la replica del contenuto per l'aggiornamento in precedenza non è riuscita, viene ripetuta.  

- **Ignora avvisi dei prerequisiti**: se l'installazione dell'aggiornamento si interrompe a causa di un avviso, è quindi possibile scegliere **Ignora avvisi dei prerequisiti**. Questa azione consente di continuare l'installazione dell'aggiornamento dopo alcuni minuti, usando l'opzione per ignorare gli avvisi relativi ai prerequisiti.

### <a name="retry-installation-for-the-site"></a>Riprovare l'installazione per il sito

Ripetere l'installazione di un aggiornamento in un sito specifico quando l'aggiornamento è in uno degli stati seguenti:  

- Controlli dei prerequisiti superati con uno o più avvisi e opzione per ignorare gli avvisi di controllo dei prerequisiti non impostata nell'Aggiornamento guidato. Il valore di **Ignora avviso prerequisito** per l'aggiornamento nel nodo Aggiornamenti e manutenzione è **No**.  

- Il prerequisito non è riuscito

- L'installazione non è riuscita

Passare all'area di lavoro **Monitoraggio** e selezionare il nodo **Site Servicing Status** (Stato di manutenzione sito). Selezionare l'aggiornamento e quindi scegliere una delle opzioni seguenti.  

- **Riprova**: quando si **riprova** da **Site Servicing Status** (Stato di manutenzione sito), l'installazione dell'aggiornamento viene avviata nuovamente sono nel sito specifico. A differenza di quanto accade eseguendo **Riprova** dal nodo **Aggiornamenti e manutenzione**, questo nuovo tentativo non ignora gli avvisi relativi ai prerequisiti.  

- **Ignora avvisi dei prerequisiti**: se l'installazione dell'aggiornamento si interrompe a causa di un avviso, è quindi possibile selezionare **Ignora avvisi dei prerequisiti**. Questa azione consente di continuare l'installazione dell'aggiornamento dopo alcuni minuti, usando l'opzione per ignorare gli avvisi relativi ai prerequisiti.  

## <a name="after-a-site-installs-an-update"></a><a name="bkmk_after"></a> Dopo l'installazione di un aggiornamento in un sito  

Dopo l'aggiornamento del sito, esaminare l'elenco di controllo post-aggiornamento per la versione applicabile:  

- [Elenco di controllo post-aggiornamento per la versione 2002](checklist-for-installing-update-2002.md#post-update-checklist)

- [Elenco di controllo post-aggiornamento per la versione 1910](checklist-for-installing-update-1910.md#post-update-checklist)  

- [Elenco di controllo post-aggiornamento per la versione 1906](checklist-for-installing-update-1906.md#post-update-checklist)  

- [Elenco di controllo post-aggiornamento per la versione 1902](checklist-for-installing-update-1902.md#post-update-checklist)  

## <a name="enable-optional-features-from-updates"></a><a name="bkmk_options"></a> Abilitare le funzionalità facoltative degli aggiornamenti  

Quando un aggiornamento include una o più funzionalità facoltative, è possibile abilitare queste funzionalità nella gerarchia. Abilitare le funzionalità durante l'installazione dell'aggiornamento oppure tornare nella console in un secondo momento per abilitare le funzionalità facoltative.

Per visualizzare le funzionalità disponibili e il relativo stato, nella console passare all'area di lavoro **Amministrazione**, espandere **Aggiornamenti e manutenzione** e selezionare il nodo **Funzionalità**.

Quando una funzionalità non è facoltativa, viene installata automaticamente e non compare nel nodo **Funzionalità**.  

> [!Important]  
> In una gerarchia a più siti abilitare le funzionalità facoltative o di versioni non definitive solo dal sito di amministrazione centrale. Questo comportamento assicura che non ci siano conflitti all'interno della gerarchia. <!--507197-->  

Quando si abilita una nuova funzionalità o una funzionalità non definitiva, gestione gerarchie (HMAN) di Configuration Manager deve elaborare la modifica prima che tale funzionalità diventi disponibile. L'elaborazione della modifica è spesso immediata. A seconda del ciclo di elaborazione HMAN, il completamento può richiedere fino a 30 minuti. Dopo l'elaborazione della modifica, per poter usare la funzionalità riavviare prima la console.

A partire dalla versione 2002,<!--5834830--> quando sono disponibili nuove funzionalità basate sul cloud nell'interfaccia di amministrazione di Microsoft Endpoint Manager o in altri servizi cloud collegati per l'installazione locale di Configuration Manager, è possibile ora acconsentire esplicitamente a queste nuove funzionalità nella console di Configuration Manager.

### <a name="list-of-optional-features"></a>Elenco delle funzionalità facoltative

Le funzionalità seguenti sono facoltative nella versione più recente di Configuration Manager:<!--505213-->  

<!--Note to include in target articles

> [!Note]  
> Configuration Manager doesn't enable this optional feature by default. You must enable this feature before using it. For more information, see [Enable optional features from updates](install-in-console-updates.md#bkmk_options).  

-->

- [Hub della community](community-hub.md)<!--3555935, C098DA03-C33C-4E15-B337-6C0FEEB3CB8A-->
- [Gestione di BitLocker](../../../protect/plan-design/bitlocker-management.md) <!-- 3601034,6DD56E46-C3EC-4E38-A16F-E98644BB6434 -->
- [Sincronizzare i risultati di appartenenza alla raccolta con Azure Active Directory](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync) <!--3607475,C2127144-C8DE-49F6-9CB3-D4F5B59F9515-->
- [Individuazione dei gruppi utenti in Azure Active Directory](../deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco) <!--3611956,023715E7-BFBA-4E9E-A80F-B5B626464ADD-->
- [Gruppi di applicazioni](../../../apps/deploy-use/create-app-groups.md) <!--3555907,EE16A1D8-EF1B-4094-845F-AC107E7C621D-->
- [Debugger di sequenze di attività](../../../osd/deploy-use/debug-task-sequence.md) <!--3612274,C3F37661-69E4-4D53-A39C-5D02F97E0E71-->
- [Package Conversion Manager](../../../apps/pcm/package-conversion-manager.md) <!--1357861,4E0C09AF-7FC1-4412-A8BB-166D9BCD0093-->
- [App client per dispositivi con co-gestione](../../../comanage/workloads.md#client-apps) (precedentemente note come *App per dispositivi mobili per dispositivi con co-gestione*) <!--1357892,CC3AE625-BF72-49B1-8AB1-AF0DCF2D6F4C-->
- [Aggiornamenti software di terze parti ](../../../sum/deploy-use/third-party-software-updates.md)<!--1357605,1352101,1358714;B5E192AE-C81F-4348-9EF9-07A3C0FBE597-->
- [Approva le richieste dell'applicazione per gli utenti per ogni dispositivo](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-settings) <!--1357015,4BA987C9-08FC-48E2-BFFE-C9DCF35B496A-->  
- [Crea ed esegui script](../../../apps/deploy-use/create-deploy-scripts.md) <!--1236459,566F8720-F415-4E10-9A51-CDE682BA2B2E-->
- [Aggiornamenti driver di Surface](../../../sum/get-started/configure-classifications-and-products.md) <!--1098490,82AD973A-7CDF-4B67-A665-72875D6E099A-->
- [Gateway di gestione cloud](../../clients/manage/cmg/plan-cloud-management-gateway.md) <!--1101764,DD043119-789C-4158-AC79-725E999F385A-->
- [Creazione di PFX](../../../protect/deploy-use/introduction-to-certificate-profiles.md) <!--1321368,CED76B79-929C-4C45-981F-B9BCA6D38A17-->
- [Connettore di Azure Log Analytics](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm) <!--1258052,73A7EC4D-EF22-4EA4-82A9-419C2A8CFC4D-->
- [Criteri di Windows Defender Exploit Guard](../../../protect/deploy-use/create-deploy-exploit-guard-policy.md) <!--1355468,8491D4C8-8484-46B8-BCD6-17DC2CADBAEB-->
- [VPN per Windows 10](../../../protect/deploy-use/vpn-profiles.md) <!--1283610,EDBEBA3D-3A4D-4465-84D9-D71EB811E7F6-->
- [Manutenzione di una raccolta compatibile con cluster (gruppi di server)](../../../sum/deploy-use/service-a-server-group.md) <!--1081776,290B66D8-C735-4895-B59A-DD732D84A697-->
- [Windows Hello for Business](../../../protect/deploy-use/windows-hello-for-business-settings.md) (noto in precedenza come *Passport for Work*) <!--1245704,8BCA2642-3719-4862-A355-9D39C979E1B4-->

> [!Tip]  
> Per altre informazioni sulle funzionalità che richiedono il consenso per l'abilitazione, vedere [Funzionalità di versioni non definitive](pre-release-features.md).  
>
> Per altre informazioni sulle funzionalità disponibili solo nel ramo Technical Preview, vedere [Technical Preview](../../get-started/technical-preview.md).

## <a name="use-pre-release-features-from-updates"></a><a name="bkmk_prerelease"></a> Usare le funzionalità di versioni non definitive degli aggiornamenti

La versione Current Branch include le funzionalità di versioni non definitive a scopo di test preliminare in un ambiente di produzione. Per altre informazioni, vedere [Funzionalità di versioni non definitive](pre-release-features.md).

## <a name="frequently-asked-questions"></a><a name="bkmk_faq"></a> Domande frequenti

### <a name="why-dont-i-see-certain-updates-in-my-console"></a>Perché alcuni aggiornamenti non vengono visualizzati nella console?

Se dopo una sincronizzazione riuscita con il servizio cloud Microsoft non si riesce a trovare uno specifico aggiornamento nella console, questo comportamento potrebbe essere causato da uno dei motivi seguenti:  

- L'aggiornamento richiede una configurazione non usata nell'infrastruttura oppure la versione corrente del prodotto non soddisfa un prerequisito per la ricezione dell'aggiornamento.  

    Se si ritiene che siano presenti le configurazioni e i prerequisiti necessari per un aggiornamento mancante, verificare che il punto di connessione del servizio sia in modalità online. Usare quindi l'opzione **Controlla aggiornamenti** nel nodo **Aggiornamenti e manutenzione** per forzare un controllo. Se il punto di connessione del servizio è in modalità offline, usare lo strumento di connessione del servizio per eseguire manualmente la sincronizzazione con il servizio cloud.  

- L'account non ha le autorizzazioni corrette di amministrazione basata su ruoli per visualizzare gli aggiornamenti nella console di Configuration Manager. Per altre informazioni, vedere la sezione relativa alle [autorizzazioni per la gestione degli aggiornamenti](#assign-permissions-to-view-and-manage-updates-and-features).  
