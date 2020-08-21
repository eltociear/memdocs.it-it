---
title: Technical Preview 1706
titleSuffix: Configuration Manager
description: Informazioni sulle funzionalità disponibili nella versione Technical Preview 1706 per Configuration Manager.
ms.date: 09/15/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ca3b4714-2a16-495e-8a17-1d87991d5556
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 8c3624f9fc903395b36846170ff3552f32db59dd
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692945"
---
# <a name="capabilities-in-technical-preview-1706-for-configuration-manager"></a>Funzionalità della versione Technical Preview 1706 per Configuration Manager

*Si applica a: Configuration Manager (Technical Preview Branch)*

Questo articolo presenta le funzionalità disponibili nella Technical Preview per Configuration Manager, versione 1706. È possibile installare questa versione per aggiornare e aggiungere nuove funzionalità al sito di Technical Preview di Configuration Manager. Prima di installare questa versione Technical Preview, consultare [Technical Preview per Configuration Manager](../../core/get-started/technical-preview.md) per acquisire familiarità con i requisiti generali e con le limitazioni per l'uso di una versione Technical Preview, con le modalità di aggiornamento tra le versioni e con le modalità per offrire commenti e suggerimenti sulle funzionalità di una versione Technical Preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
- **Issue Name**. Details
    Workaround details.
-->
**Problemi noti di questa versione Technical Preview:**

- **Move distribution point** (Sposta punto di distribuzione): le opzioni nella console per spostare un punto di distribuzione tra i siti non possono essere usate con questa versione a causa del limite di Technical Preview a un singolo sito primario.

- **Device compliance settings** (Impostazioni di conformità del dispositivo): potrebbe verificarsi un comportamento contrario quando si usano le due nuove impostazioni di conformità del dispositivo:
  - **Blocca il debug USB nel dispositivo**
  - **Blocca app da origini sconosciute**

    Ad esempio, se gli amministratori impostano **Blocca il debug USB nel dispositivo**  su **true**, tutti i dispositivi per i quali il debug USB non è abilitato sono contrassegnati come non conformi.

**Di seguito sono riportate le nuove funzionalità disponibili con questa versione.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improved-boundary-groups-for-software-update-points"></a>Gruppi di limiti migliorati per i punti di aggiornamento software
<!-- 1324591 -->
Questa versione include dei miglioramenti per il funzionamento dei punti di aggiornamento del software con i gruppi di limiti. Di seguito viene riepilogato il nuovo comportamento di fallback:
- Il fallback per i punti di aggiornamento del software usa attualmente un tempo configurabile per il fallback a gruppi di limiti adiacenti, con un tempo minimo di 120 minuti.

- Indipendentemente dalla configurazione di fallback, un client tenta di raggiungere l'ultimo punto di aggiornamento del software che ha usato per 120 minuti. Dopo l'esito negativo nel raggiungere il server per 120 minuti, il client controlla quindi il proprio pool di punti di aggiornamento del software disponibili, per poterne trovare uno nuovo.

  - Tutti i punti di aggiornamento del software nel gruppo di limiti attuale del client vengono aggiunti immediatamente al pool del client.

  - Poiché un client cerca di usare il proprio server originale per 120 minuti prima di richiederne uno nuovo, non viene contattato nessun server aggiuntivo fino a che non sono trascorse due ore.

  - Se il fallback a un gruppo adiacente è configurato per il valore minimo di 120 minuti, i punti di aggiornamento del software da quel gruppo di limiti adiacente farà parte del pool del client di server disponibili.

- Dopo l'esito negativo nel raggiungere il server originale per due ore, il client passa a un ciclo più breve per contattare un nuovo punto di aggiornamento del software.

  Ciò significa che se un client non riesce a connettersi con un nuovo server, seleziona rapidamente il server successivo dal relativo pool di server disponibili e cerca di contattarne uno nuovo.

  - Questo ciclo continua fino a quando il client si connette a un punto di aggiornamento del software da poter usare.
  - Fino a quando il client non trova un punto di aggiornamento del software, vengono aggiunti dei server aggiuntivi al pool di server disponibili quando si raggiunge l'ora di fallback per ogni gruppo di limiti adiacente.

Per altre informazioni, vedere la sezione [Punti di aggiornamento software](../servers/deploy/configure/boundary-groups.md#bkmk_sup) nell'argomento Gruppi di limiti e relazioni per il Current Branch.


## <a name="site-server-role-high-availability"></a>Disponibilità elevata per il ruolo del server del sito
<!-- 1128774 -->
La disponibilità elevata per il ruolo del server del sito è una soluzione di base di Configuration Manager per installare un server del sito primario aggiuntivo in modalità *Passivo*. Il server del sito in modalità Passivo è un'aggiunta al server del sito primario esistente in modalità *Attivo*. Un server del sito in modalità Passivo è disponibile per l'uso immediato, quando necessario.

Un server del sito primario in modalità Passivo:
- Usa lo stesso database del sito usato dal server del sito attivo.
- Riceve una copia della raccolta del contenuto dei server del sito attivi, che viene quindi mantenuta sincronizzata.
- Non scrive dati nel database del sito fino a quando si trova in modalità Passivo.
- Non supporta l'installazione o la rimozione di ruoli del sistema del sito facoltativi, fino a quando si trova in modalità Passivo.

Per far sì che il server del sito in modalità Passivo diventi il server del sito in modalità attiva, alzare manualmente di livello. In questo modo si otterrà un server del sito attivo dal server del sito passivo. I ruoli del sistema del sito che sono disponibili nel server in modalità Attivo originale rimangono disponibili fin a quando tale computer è accessibile. Solo il ruolo del server del sito viene commutato tra modalità Attivo e Passivo.

Per installare un server del sito in modalità Passivo, usare **Creazione guidata server del sistema sito** per configurare un nuovo server del sito con un tipo di **Server del sito primario** e una modalità di **Passivo**. La procedura guidata esegue quindi l'installazione di Configuration Manager nel server specificato per installare il nuovo server del sito in modalità Passivo. Al completamento dell'installazione, il server del sito in modalità Attivo mantiene il server del sito in modalità Passivo e la sua raccolta contenuto sincronizzata con le modifiche o le configurazioni apportate al server del sito attivo.

### <a name="prerequisites-and-limitations"></a>Prerequisiti e limiti
- Ciascun sito primario supporta un singolo server del sito in modalità Passivo.

- Il server del sito in modalità Passivo può essere locale o basato su cloud in Azure.

- I server del sito in modalità Passivo e in modalità Attivo devono essere nello stesso dominio.

- I server del sito in modalità Passivo e in modalità Attivo devono usare lo stesso database del sito, che deve essere remoto rispetto ai computer di ogni server del sito.

    - SQL Server che ospita il database può usare un'istanza predefinita, un'istanza denominata, un cluster di SQL Server o un gruppo di disponibilità Always on.

    - Il server del sito in modalità Passivo è configurato per usare lo stesso database del server del sito in modalità Attivo. Tuttavia, il server del sito in modalità Passivo non usa tale database finché non viene poi promosso alla modalità Attivo.

- Il computer che eseguirà il server del sito in modalità Passivo:

    - Deve soddisfare i [prerequisiti per l'installazione di un sito primario](/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#primary-sites-and-the-central-administration-site).

    - Esegue l'installazione usando file di origine che corrispondono alla versione del server del sito in modalità Attivo.

    - Non può avere un ruolo del sistema del sito da qualsiasi sito prima di installare il sito in modalità Passivo.

- I computer del server del sito in modalità Attivo e Passivo possono eseguire diversi sistemi operativi o versioni di service pack, a condizione che entrambe restino supportate dalla versione di Configuration Manager dell'utente.

- La promozione del server del sito verso la modalità Attivo è manuale. Non si verifica failover automatico.

- I ruoli del sistema del sito possono essere installati solo sul server del sito che è in modalità Attivo.

    - Un server del sito in modalità Attivo supporta tutti i ruoli del sistema del sito. Non è possibile installare i ruoli del sistema del sito nel server quando è in modalità Passivo.

    - I ruoli del sistema del sito che usano un database, ad esempio il punto di reporting, devono avere il database in un server che sia remoto rispetto ai server del sito in modalità Attivo e Passivo.

    - SMS_Provider non viene installato nel server del sito in modalità Passivo. Poiché è necessario connettersi a un SMS_Provider per far sì che il sito innalzi manualmente il livello del server dalla modalità Passivo a quella Attivo, è consigliabile [installare almeno un'istanza aggiuntiva del provider](../plan-design/hierarchy/plan-for-the-sms-provider.md) su un computer aggiuntivo.

**Problema noto**:   
Con questa versione, lo **Stato** per le condizioni seguenti viene visualizzato nella console come valori numerici anziché come testo leggibile:
- 131071 - Installazione del server del sito non riuscita
- 720895 - Disinstallazione del ruolo del server del sito non riuscita
- 851967 - Failover non riuscito

### <a name="add-a-site-server-in-passive-mode"></a>Aggiungere un server del sito in modalità Passivo
1. Nella console passare ad **Amministrazione** > **Configurazione del sito** > **Siti** e avviare l'[Aggiunta guidata ruoli del sistema del sito](../servers/deploy/configure/install-site-system-roles.md). È possibile usare anche la **Creazione guidata server del sistema sito**.

2. Nella pagina **Generale** specificare il server che ospiterà il server del sito in modalità Passivo. Il server specificato non può ospitare eventuali ruoli del sistema del sito prima di installare un server del sito in modalità Passivo.

3. Nella pagina **Selezione ruolo del sistema** selezionare solo **Primary site server in passive mode** (Server del sito primario in modalità Passivo).

4. Per completare la procedura guidata, è necessario fornire le informazioni seguenti che vengono usate per eseguire la configurazione e installare il ruolo del server del sito nel server specificato:
    - Scegliere di copiare i file di installazione dal server del sito attivo al nuovo server del sito in modalità Passivo o specificare un percorso a una posizione che includa il contenuto della cartella del server del sito attivo **CD.Latest**.

    - Specificare lo stesso server del database del sito e il nome del database come usati dal server del sito in modalità Attivo.

5. Configuration Manager installa quindi il server del sito in modalità Passivo nel server specificato.

Per lo stato di installazione dettagliato, passare ad **Amministrazione** > **Configurazione sito** > **Siti**.
- Lo stato del server per il server del sito in modalità Passivo viene visualizzato come **Installazione**.

- Selezionare il server e quindi fare clic su **Mostra stato** per aprire lo **Site Server Installation Status** (Stato installazione del server del sito) per informazioni più dettagliate.



### <a name="promote-the-passive-mode-site-server-to-active-mode"></a>Alzare il livello del server in modalità Passivo passandolo in modalità Attivo
Se si desidera modificare il server del sito dalla modalità Passivo alla modalità Attivo, l'operazione viene eseguita dal riquadro **Nodi** **Amministrazione** > **Configurazione sito** > **Siti**. Finché si può accedere a un'istanza di SMS_Provider, è possibile accedere al sito per apportare questa modifica.
1. Nel riquadro **Nodi** della console di Configuration Manager selezionare il server del sito in modalità Passivo e quindi dalla barra multifunzione scegliere **Alza di livello su attivo**.

2. Il semplice **Stato** per il server che si sta alzando di livello viene visualizzato nel riquadro **Nodi** come **Innalzamento di livello**.

3. Al termine dell'innalzamento di livello, la colonna **Stato** mostra la scritta **OK** per il nuovo server del sito in modalità *Attivo* e per il nuovo server del sito in modalità *Passivo*.

4. In **Amministrazione** > **Configurazione sito** > **Siti** il nome del server del sito primario mostra ora il nome del nuovo server del sito in modalità *Attivo*.
Per informazioni dettagliate sullo stato, passare a **Monitoraggio** > **Site Server Status** (Stato server del sito).
    - La colonna **Modalità** identifica quale server è *Attivo* o *Passivo*.

    - Durante l'innalzamento di livello di un server dalla modalità Passivo alla modalità Attivo, selezionare il server del sito che si sta innalzando di livello in modalità Attivo e quindi scegliere **Mostra stato** dalla barra multifunzione. Viene visualizzata la finestra**Site Server Promotion Status** (Stato innalzamento di livello server del sito) che mostra altri dettagli relativi al processo.

Quando un server del sito in modalità Attivo passa alla modalità Passivo, solo il ruolo del sistema del sito è reso passivo. Tutti gli altri ruoli del sistema del sito che vengono installati su quel computer restano attivi e accessibili ai client.


### <a name="daily-monitoring"></a>Monitoraggio giornaliero
Quando si dispone di un sito primario in modalità Passivo, è possibile monitorarlo giornalmente per garantire che rimanga sincronizzato con il server del sito in modalità Attivo e pronto per l'uso. A tale scopo, passare a **Monitoraggio** > **Site Server Status** (Stato server del sito). In questa posizione è possibile visualizzare il server del sito in modalità Passivo e in modalità Attivo.

La scheda **Riepilogo**:
- La colonna **Modalità** identifica quale server è Attivo o Passivo.
- La colonna **Stato** riporta **OK** quando il server in modalità Passivo è sincronizzato con il server in modalità Attivo.
- Per visualizzare altri dettagli sullo stato di sincronizzazione del contenuto, fare clic su **Mostra stato** dallo Content Sync State (Stato di sincronizzazione del contenuto). Viene visualizzata la scheda Content Library (Raccolta contenuto) in cui è possibile provare a risolvere i problemi di sincronizzazione del contenuto.

La scheda **Content Library** (Raccolta contenuto):
- Visualizzare lo **Stato** per il contenuto che sincronizza dal server del sito Attivo al server del sito in modalità Passivo.
- È possibile selezionare il contenuto con uno stato di **Non riuscito** e quindi scegliere **Sync selected items** (Sincronizza elementi selezionati) dalla barra multifunzione. Questa azione tenta di sincronizzare nuovamente il contenuto dall'origine del contenuto al server del sito in modalità passiva. Durante il recupero, lo Stato è visualizzato come **In corso** e dopo la sincronizzazione viene visualizzato come **Operazione riuscita**.

### <a name="try-it-out"></a>Verifica
Provare a completare le attività seguenti e quindi inviare **Feedback** dalla scheda **Home** della barra multifunzione per comunicarci come è andata:
- È possibile installare un sito primario nella modalità Passivo.
- È possibile usare la console per alzare di livello il server del sito in modalità Passivo per rendere il server del sito modalità Attivo e confermare la modifica dello stato di entrambi i server del sito.


## <a name="include-trust-for-specific-files-and-folders-in-a-device-guard-policy"></a>Includere attendibilità per file e cartelle specifici in un criterio di Device Guard
<!-- 1324676 -->
In questa versione sono state aggiunte altre funzionalità alla gestione dei criteri di [Device Guard](../../protect/deploy-use/use-device-guard-with-configuration-manager.md)

Ora è possibile aggiungere facoltativamente attendibilità per file e cartelle specifici in un criterio di Device Guard. Ciò consente di:

1. Risolvere i problemi relativi ai comportamenti del programma di installazione gestito
2. Rendere attendibili le app line-of-business che non possono essere distribuite con Configuration Manager
3. Rendere attendibili le app incluse in un'immagine di distribuzione del sistema operativo.

### <a name="try-it-out"></a>Verifica

1. Durante la creazione di un criterio di Device Guard, nella scheda Inclusioni della procedura guidata per la creazione di criteri di Device Guard fare clic su **Aggiungi**.
2. Nella finestra di dialogo **Aggiungi file o cartella attendibile** specificare le informazioni sul file o sulla cartella che si desidera considerare attendibile. È possibile specificare un percorso di file o cartella locale oppure connettersi a un dispositivo remoto per cui si dispone dell'autorizzazione per connettersi e specificare un percorso di file o cartella nel dispositivo.
3. Completare la procedura guidata.


## <a name="hide-task-sequence-progress"></a>Nascondere l'avanzamento della sequenza di attività
<!-- 1354291 -->
In questa versione è possibile controllare quando stato sequenza di attività viene visualizzato agli utenti finali tramite una nuova variabile. Nella sequenza di attività usare il passaggio **Imposta variabile della sequenza attività** per impostare il valore per la variabile **TSDisableProgressUI** per nascondere o visualizzare lo stato della sequenza di attività. È possibile usare più volte il passaggio Imposta variabile della sequenza di attività in una sequenza di attività per modificare il valore della variabile. Ciò consente di visualizzare o nascondere l'avanzamento dello stato della sequenza di attività in varie sezioni della sequenza di attività.

#### <a name="to-hide-task-sequence-progress"></a>Per nascondere l'avanzamento della sequenza di attività
Nell'editor di sequenze di attività usare il passaggio [Imposta variabile della sequenza di attività](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) per impostare il valore della variabile **TSDisableProgressUI** su **True** per nascondere lo stato della sequenza di attività.

#### <a name="to-display-task-sequence-progress"></a>Per visualizzare l'avanzamento della sequenza di attività
Nell'editor di sequenze di attività usare il passaggio [Imposta variabile della sequenza di attività](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) per impostare il valore della variabile **TSDisableProgressUI** su **False** per visualizzare lo stato della sequenza di attività.

## <a name="specify-a-different-content-location-for-install-content-and-uninstall-content"></a>Specificare un percorso del contenuto diverso per il contenuto di installazione e il contenuto di disinstallazione
<!-- 1097546 -->
Oggi, in Configuration Manager specificare il percorso di installazione che contiene i file di installazione per un'app. Quando si specifica un percorso di installazione, questo viene usato anche come percorso di disinstallazione per il contenuto dell'applicazione.
In base ai commenti, quando si desidera disinstallare un'applicazione distribuita e il contenuto dell'app non è presente nel computer client, il client scaricherà nuovamente tutti i file di installazione dell'app prima che l'applicazione venga disinstallata.
Per risolvere questo problema, è ora possibile specificare sia il percorso del contenuto di installazione che il percorso del contenuto di disinstallazione facoltativo. In aggiunta, è possibile scegliere di non specificare il percorso del contenuto di disinstallazione.

### <a name="try-it-out"></a>Procedura

1. Nelle proprietà del tipo di distribuzione di un'applicazione fare clic sulla scheda **Contenuto**.
2. Configurare il **percorso del contenuto di installazione** come di consueto.
3. Per **Impostazioni del contenuto di disinstallazione**, scegliere una delle opzioni seguenti:
   - **Uguale al contenuto di installazione**: lo stesso percorso del contenuto sarà usato indipendentemente dal fatto che si stia installando o disinstallando l'applicazione.
   - **Nessun contenuto di disinstallazione**: scegliere questa opzione se non si desidera fornire un percorso del contenuto di disinstallazione per l'applicazione.
   - **Diversa dal contenuto di installazione**: scegliere questa opzione se si desidera specificare un percorso del contenuto di disinstallazione diverso dal percorso del contenuto di installazione.
5. Se si seleziona **Diversa dal contenuto di installazione**, selezionare o immettere il percorso del contenuto dell'applicazione che verrà usato per disinstallare l'applicazione.
6. Fare clic su **OK** per chiudere la finestra di dialogo delle proprietà del tipo di distribuzione.


## <a name="accessibility-improvements"></a>Miglioramenti all'accessibilità  
<!--1253000 -->
Questa versione di anteprima introduce diversi miglioramenti alle [funzionalità di accessibilità](../understand/accessibility-features.md) nella console di Configuration Manager. Sono inclusi:     

**Nuovi tasti di scelta rapida per spostarsi all'interno della console:**
- CTRL + M - Imposta il focus nel riquadro principale (centrale).
- CTRL + T - Imposta il focus sul nodo principale nel riquadro di spostamento. Se il focus era già in questo riquadro, viene impostato sull'ultimo nodo visitato.
- CTRL + I - Imposta il focus sulla barra di navigazione, sotto la barra multifunzione.
- CTRL + L - Imposta il focus sul campo **Ricerca**, se disponibile.
- CTRL + D - Imposta il focus sul riquadro dei dettagli, se disponibile.
- ALT - Sposta il focus dentro e fuori la barra multifunzione.

**Miglioramenti generali:**
- Navigazione migliorata nel riquadro di spostamento quando si digitano le lettere del nome di un nodo.
- La navigazione tramite tastiera nella vista principale e nella barra multifunzione è ora circolare.
- La navigazione tramite tastiera nel riquadro dei dettagli è ora circolare. Per tornare al riquadro o all'oggetto precedente, è possibile usare Ctrl + D e poi MAIUSC + TAB.
- Dopo l'aggiornamento di una vista dell'area di lavoro, il focus è impostato nel riquadro principale dell'area di lavoro.
- Risolto un problema per abilitare i lettori dello schermo per annunciare i nomi degli elementi dell'elenco.
- Nomi accessibili aggiunti per più controlli nella pagina che consente ai lettori dello schermo di annunciare informazioni importanti.


## <a name="changes-to-the-azure-services-wizard-to-support-upgrade-readiness"></a>Modifiche alla procedura guidata dei servizi di Azure per il supporto della Preparazione aggiornamenti
<!-- 1353331 -->
A partire da questa versione, usare la procedura guidata per i servizi di Azure per configurare una connessione da Configuration Manager a Preparazione aggiornamenti. L'uso della procedura guidata semplifica la configurazione del connettore tramite una procedura guidata comune per i servizi di Azure correlati.   

Anche se il metodo per configurare la connessione è stato modificato, i prerequisiti per la connessione e le modalità d'uso di Preparazione aggiornamenti restano invariati.   

### <a name="prerequisites-for-upgrade-readiness"></a>Prerequisiti per Preparazione aggiornamenti
I prerequisiti per la connessione a Preparazione aggiornamenti sono identici a quelli dettagliati per Configuration Manager Current Branch. Ne riportiamo un pratico riepilogo:  

**Prerequisiti**
- Per l'aggiunta della connessione, è necessario che nell'ambiente di Configuration Manager sia stato configurato un [punto di connessione del servizio](../servers/deploy/configure/about-the-service-connection-point.md) in [modalità online](../servers/deploy/configure/about-the-service-connection-point.md#bkmk_modes). Quando si aggiunge la connessione all'ambiente, viene installato anche Microsoft Monitoring Agent nel computer che esegue questo ruolo del sistema del sito.
- Registrare Configuration Manager come strumento di gestione "Applicazione Web e/o API Web" e ottenere l'[ID client della registrazione](/azure/active-directory/develop/quickstart-register-app).
- Creare una chiave client per lo strumento di gestione registrato in Azure Active Directory.
- Nel portale di Azure fornire all'app Web registrata l'autorizzazione per accedere a OMS.

> [!IMPORTANT]       
> Quando si configura l'autorizzazione per accedere a OMS, assicurarsi di scegliere il ruolo **Collaboratore** e di assegnare a tale ruolo le autorizzazioni per il gruppo di risorse dell'app registrata.

Dopo aver configurato i prerequisiti, si è pronti a usare la procedura guidata per creare la connessione.

### <a name="use-the-azure-services-wizard-to-configure-upgrade-readiness"></a>Usare la procedura guidata dei servizi di Azure per configurare Preparazione aggiornamenti
1. Nella console passare ad **Amministrazione** > **Panoramica** > **Servizi cloud** > **Servizi di Azure** e quindi scegliere **Configura i servizi di Azure** dalla scheda **Home** della barra multifunzione per avviare la **Procedura guidata per i servizi di Azure**.

2. Nella pagina **Servizi di Azure** selezionare **Connettore Upgrade Readiness** e quindi fare clic su **Avanti**.

3. Nella pagina **App** specificare l'**ambiente Azure** (technical preview supporta solo cloud pubblici). Quindi, fare clic su **Importa** per aprire la finestra **Importa le app**.

4. Nella finestra **Importa le app** specificare i dettagli per un'app Web già esistente in Azure AD.
    - Specificare un nome descrittivo per Nome del tenant di Azure AD. Quindi, specificare l'ID Tenant, il nome dell'applicazione, l'ID Client, la chiave privata per l'app Web di Azure e l'URI ID dell'app.
    - Fare clic su **Verifica** e, se ha esito positivo, fare clic su **OK** per continuare.

5.  Nella pagina **Configurazione** specificare la sottoscrizione, il gruppo di risorse e l'area di lavoro di Windows Analytics che si desidera usare con questa connessione a Preparazione aggiornamenti.  

6. Fare clic su **Avanti** per visualizzare la pagina **Riepilogo** e quindi completare la procedura guidata per creare la connessione.


## <a name="new-client-settings-for-cloud-services"></a>Nuove impostazioni client per i servizi cloud
<!-- 1319883 -->

In questa versione sono state aggiunte due nuove impostazioni client a Configuration Manager. Queste sono disponibili nella sezione **Servizi Cloud**.  Queste impostazioni offrono le funzionalità seguenti:

- Controllare quali client di Configuration Manager possono accedere a un gateway di gestione del cloud configurato.
- Registrare automaticamente i client di Configuration Manager appartenenti a un dominio di Windows 10 con Azure Active Directory.

Le nuove impostazioni consentono di eseguire le funzionalità descritte in [Configuration Manager 1705 Technical Preview](capabilities-in-technical-preview-1705.md#new-capabilities-for-azure-ad-and-cloud-management) (Technical Preview 1705 di Configuration Manager).

### <a name="before-you-start"></a>Prima di iniziare

È necessario aver installato e configurato Azure AD Connect tra Active Directory locale e il tenant di Azure AD.

Se si rimuove la connessione, non viene annullata la registrazione dei dispositivi, ma non è possibile registrarne di nuovi.

### <a name="try-it-out"></a>Verifica

1. Configurare la sezione seguente di impostazioni client (in Servizi cloud) tramite le informazioni contenute in [Come configurare le impostazioni client in System Center Configuration Manager](../clients/deploy/configure-client-settings.md).
   - **Registra automaticamente i nuovi dispositivi Windows 10 aggiunti al dominio con Azure Active Directory** impostato su **Sì** (impostazione predefinita) o **No**.
   - **Consenti ai client di usare un gateway di gestione cloud** impostato su **Sì** (impostazione predefinita) o **No**.
2. Distribuire le impostazioni client per la raccolta necessaria di dispositivi.

Per verificare che il dispositivo sia stato aggiunto ad Azure AD, eseguire il comando **dsregcmd.exe /status** in una finestra del prompt dei comandi. Il campo **AzureAdjoined** nei risultati visualizza **Sì** se il dispositivo è stato aggiunto ad Azure AD.

## <a name="create-and-run-powershell-scripts-from-the-configuration-manager-console"></a>Creare ed eseguire gli script di PowerShell dalla console di Configuration Manager
<!-- 1236459 -->

In Configuration Manager, è possibile distribuire script ai dispositivi client tramite pacchetti e programmi. In questa versione technical preview sono stati aggiunte nuove funzionalità che consentono di intraprendere le azioni seguenti:

- Importare gli script di PowerShell in Configuration Manager
- Modificare gli script dalla console di Configuration Manager (solo per script non firmati)
- Contrassegnare gli script come Approvato o Rifiutato per migliorare la sicurezza
- Eseguire gli script nelle raccolte di PC client Windows e nei PC Windows gestiti in locale. Gli script non vengono distribuiti ma eseguiti quasi in tempo reale sui dispositivi client.
- Esaminare i risultati restituiti dallo script nella console di Configuration Manager.


### <a name="prerequisites"></a>Prerequisiti

Per usare gli script, l'utente deve essere membro del ruolo di sicurezza appropriato di Configuration Manager.

- **Per importare e creare script**: l'account deve avere autorizzazioni di **creazione** per **script SMS** nel ruolo di sicurezza **Amministratore completo**.
- **Per approvare o rifiutare script**: l'account deve avere autorizzazioni di **approvazione** per **script SMS** nel ruolo di sicurezza **Amministratore completo**.
- **Per eseguire script**: l'account deve disporre delle autorizzazioni **Run Script** per **script SMS** nel ruolo di sicurezza **Gestione impostazioni di conformità**.

Per altre informazioni sui ruoli di sicurezza di Configuration Manager, vedere [Nozioni fondamentali di amministrazione basata su ruoli per System Center Configuration Manager](../understand/fundamentals-of-role-based-administration.md).

Per impostazione predefinita, gli utenti non possono approvare uno script da loro stessi creato. Poiché gli script sono versatili e possono essere distribuiti su più dispositivi, è stato introdotto un nuovo concetto per offrire la possibilità di separare i ruoli tra la persona che crea lo script e la persona che approva lo script. In questo modo viene garantito un livello aggiuntivo di protezione dall'esecuzione di uno script senza supervisione. È possibile disattivare questa approvazione secondaria, per semplificare il test, in particolare durante la versione Technical Preview.

Per consentire agli utenti di approvare i propri script:

1. Nella console di Configuration Manager fare clic su **Amministrazione**.
2. Nell'area di lavoro **Amministrazione** , espandere **Configurazione sito**, quindi fare clic su **Siti**.
3. Nell'elenco dei siti selezionare il sito e quindi scegliere la scheda **Home** nel gruppo **Siti** e fare clic su **Impostazioni gerarchia**.
4. Nella scheda **Generale** della finestra di dialogo **Proprietà delle impostazioni di gerarchia** deselezionare la casella di controllo **Do not allow script authors to approve their own scripts** (Non consentire agli autori di script di approvare i propri script).


### <a name="try-it-out"></a>Verifica

#### <a name="import-and-edit-a-script"></a>Importare e modificare uno script

1. Nella console di Configuration Manager fare clic su **Raccolta software**.
2. Nell'area di lavoro **Raccolta software** fare clic su **Script**.
3. Nella scheda **Home** nel gruppo **Crea** fare clic su **Crea gruppo**.
4. Nella pagina **Script** della procedura guidata **Crea script** configurare quanto segue:
   - In **Nome script** inserire il nome dello script. Sebbene sia possibile creare più script con lo stesso nome, ciò renderà più difficile individuare lo script necessario per la console di Configuration Manager.
   - **Lingua script**: attualmente sono supportati solo script di **PowerShell**.
   - **Importa**: importare uno script di PowerShell nella console. Lo script viene visualizzato nel campo **Script**.
   - **Elimina**: rimuove lo script corrente dal campo **Script**.
   - **Script**: visualizza lo script attualmente importato. È possibile modificare lo script in questo campo in base alle esigenze.
5. Completare la procedura guidata. Il nuovo script viene visualizzato nell'elenco **Script** con stato **In attesa di approvazione** . Prima di poter eseguire questo script nei dispositivi client, è necessario approvarlo.


#### <a name="approve-or-deny-a-script"></a>Approvare o rifiutare uno script



Prima di eseguire uno script, deve essere approvato. Per approvare uno script:

1. Nella console di Configuration Manager fare clic su **Raccolta software**.
2. Nell'area di lavoro **Raccolta software** fare clic su **Script**.
3. Nell'elenco **Script** scegliere lo script che si desidera approvare o rifiutare e quindi scegliere la scheda **Home** nel gruppo **Script**, quindi fare clic su **Approve/Deny** (Approva/Rifiuta).
4. Nella finestra di dialogo **Approve or deny script** (Approvare o rifiutare script) scegliere di **approvare** o **rifiutare** lo script e, facoltativamente, immettere un commento sulla scelta. Se si rifiuta uno script, questo non può essere eseguito sui dispositivi client.
5. Completare la procedura guidata. Nell'elenco **Script** la colonna **Stato dell'approvazione** cambia a seconda dell'azione eseguita.

#### <a name="run-a-script"></a>Esegui uno script

Dopo aver approvato uno script, questo può essere eseguito su una raccolta a scelta.

1. Nella console di Configuration Manager fare clic su **Asset e conformità**.
2. Nell'area di lavoro **Asset e conformità** fare clic su **Raccolte dispositivi**.
3. Nell'elenco **Raccolte dispositivi** fare clic sulla raccolta di dispositivi in cui si desidera eseguire lo script.
3. Nella scheda **Home** nel gruppo **Tutti i sistemi** fare clic su **Esegui script**.
4. Nella pagina **Script** della procedura guidata **Esegui Script** scegliere uno script dall'elenco. Vengono visualizzati solo gli script approvati. Fare clic su **Avanti** e completare la procedura guidata.

#### <a name="monitor-a-script"></a>Monitorare uno script

Dopo aver eseguito uno script sui dispositivi client, è possibile usare questa procedura per monitorare la riuscita dell'operazione.

1. Nella console di Configuration Manager fare clic su **Monitoraggio**.
2. Nell'area di lavoro **Monitoraggio** fare clic su **Script Results** (Risultati script).
3. Nell'elenco **Risultati script** vengono mostrati i risultati per ogni script eseguito sui dispositivi client. Il codice di uscita dello script **0** in genere indica che lo script è stato eseguito correttamente.

## <a name="pxe-network-boot-support-for-ipv6"></a>Supporto dell'avvio della rete PXE per IPv6
<!-- 1269793 -->
È ora possibile abilitare il supporto dell'avvio della rete PXE per IPv6 per avviare una distribuzione del sistema operativo della sequenza di attività. Quando si usa questa impostazione, i punti di distribuzione abilitati per PXE supporteranno sia IPv4 che IPv6. Questa opzione non richiede WDS e interromperà WDS, se presente.

#### <a name="to-enable-pxe-boot-support-for-ipv6"></a>Per abilitare il supporto dell'avvio della rete PXE per IPv6
Usare la procedura seguente per abilitare l'opzione per il supporto IPv6 per PXE.

1. Nella console di Configuration Manager andare ad **Amministrazione** > **Panoramica** > **Punti di distribuzione** e fare clic su **Proprietà** per i punti di distribuzione abilitati per PXE.
2. Nella scheda **PXE** selezionare **Support IPv6** (Supporto IPv6) per abilitare il supporto IPv6 per PXE.

## <a name="manage-microsoft-surface-driver-updates"></a>Gestire gli aggiornamenti dei driver di Microsoft Surface
<!-- 1098490 -->
È ora possibile usare Configuration Manager per gestire gli aggiornamenti dei driver di Microsoft Surface.

### <a name="prerequisites"></a>Prerequisiti
Tutti i punti di aggiornamento software devono eseguire Windows Server 2016.

### <a name="try-it-out"></a>Verifica
Provare a completare le attività seguenti e quindi inviare **Feedback** dalla scheda **Home** della barra multifunzione per comunicarci come è andata:
1. Abilitare la sincronizzazione per i driver di Microsoft Surface. Usare la procedura in [Configurare le classificazioni e i prodotti per la sincronizzazione](../../sum/get-started/configure-classifications-and-products.md) e selezionare **Includi i driver di Microsoft Surface e gli aggiornamenti del firmware** nella scheda **Classificazioni** per abilitare i driver di Surface.
2. [Sincronizzare i driver di Microsoft Surface](../../sum/get-started/synchronize-software-updates.md).
3. [Distribuire i driver di Microsoft Surface sincronizzati](../../sum/deploy-use/deploy-software-updates.md)

## <a name="configure-windows-update-for-business-deferral-policies"></a>Configurare i criteri di rinvio di Windows Update for Business
<!-- 1290890 -->
È ora possibile configurare i criteri di rinvio dei dispositivi per gli aggiornamenti delle funzionalità di Windows 10 o gli aggiornamenti di qualità di Windows 10 gestiti direttamente da Windows Update for Business. È possibile gestire i criteri di rinvio nel nuovo nodo **Criteri di Windows Update for Business** in **Libreria Software** > **Manutenzione pacchetti di Windows 10**.

### <a name="prerequisites"></a>Prerequisiti
I dispositivi di Windows 10 gestiti da Windows Update for Business devono disporre di connettività a Internet.

#### <a name="to-create-a-windows-update-for-business-deferral-policy"></a>Per creare i criteri di rinvio di Windows Update for Business
1. In **Libreria Software** > **Manutenzione pacchetti di Windows 10** > **Criteri di Windows Update for Business**
2. Nella scheda **Home**, nel gruppo **Crea**, selezionare **Crea un criterio di Windows Update for Business** per aprire la procedura guidata Creazione guidata di un criterio di Windows Update for Business.
3. Nella pagina **Generale** specificare un nome e una descrizione per il criterio.
4. Nella pagina **Criteri di differimento** configurare se si desidera differire o sospendere gli aggiornamenti delle funzionalità.    
    Gli aggiornamenti delle funzionalità sono generalmente nuove funzionalità per Windows. Dopo aver configurato l'impostazione **Livello di conformità con Branch**, è possibile definire se e per quanto tempo si desidera rinviare la ricezione di aggiornamenti delle funzionalità in base alla disponibilità da Microsoft.
    - **Livello di conformità con Branch**: impostare il branch per il quale il dispositivo riceverà gli aggiornamenti di Windows (Current Branch o Current Branch for Business).
    - **Periodo di differimento (giorni)** :  specificare il numero di giorni per cui verranno posticipati gli aggiornamenti delle funzionalità. È possibile posticipare la ricezione di questi aggiornamenti delle funzionalità per un periodo di 180 giorni dopo il rilascio.
    - **Sospendi gli aggiornamenti delle funzionalità a partire da**: scegliere se sospendere la ricezione da parte dei dispositivi degli aggiornamenti delle funzionalità per un periodo massimo di 60 giorni a partire dal momento in cui si sospendono gli aggiornamenti. Una volta trascorso il numero massimo di giorni, la sospensione della funzionalità scadrà automaticamente e il dispositivo analizzerà Windows Updates per gli aggiornamenti applicabili. Dopo questa analisi, è possibile sospendere nuovamente gli aggiornamenti. È possibile riprendere gli aggiornamenti delle funzionalità deselezionando la casella di controllo.   
5. Scegliere se rinviare o sospendere gli aggiornamenti di qualità.     
    Gli aggiornamenti di qualità sono in genere correzioni e miglioramenti alle funzionalità esistenti di Windows e vengono generalmente pubblicati il primo martedì di ogni mese, sebbene possano essere rilasciati in qualsiasi momento da Microsoft. È possibile definire se e per quanto tempo si desidera rinviare la ricezione degli aggiornamenti di qualità dopo la loro disponibilità.
    - **Periodo di differimento (giorni)** : specificare il numero di giorni per cui verranno posticipati gli aggiornamenti delle funzionalità. È possibile posticipare la ricezione di questi aggiornamenti delle funzionalità per un periodo di 180 giorni dopo il rilascio.
    - **Sospendi gli aggiornamenti qualitativi a partire da**: scegliere se sospendere la ricezione da parte dei dispositivi degli aggiornamenti qualitativi per un periodo massimo di 35 giorni a partire dal momento in cui si sospendono gli aggiornamenti. Una volta trascorso il numero massimo di giorni, la sospensione della funzionalità scadrà automaticamente e il dispositivo analizzerà Windows Updates per gli aggiornamenti applicabili. Dopo questa analisi, è possibile sospendere nuovamente gli aggiornamenti. È possibile riprendere gli aggiornamenti di qualità deselezionando la casella di controllo.
6. Selezionare **Installa gli aggiornamenti per altri prodotti Microsoft** per abilitare l'impostazione dei criteri di gruppo che rendono le impostazioni di rinvio applicabili a Microsoft Update, oltre agli aggiornamenti di Windows.
7. Selezionare **Include drivers with Windows Update** (Includi i driver con Windows Update) per aggiornare automaticamente i driver da Windows Update. Se si deseleziona questa impostazione, gli aggiornamenti dei driver non vengono scaricati da Windows Update.
8. Completare la procedura guidata per creare i nuovi criteri di rinvio.

#### <a name="to-deploy-a-windows-update-for-business-deferral-policy"></a>Per distribuire i criteri di rinvio di Windows Update for Business
1. In **Libreria Software** > **Manutenzione pacchetti di Windows 10** > **Criteri di Windows Update for Business**
2. Nella scheda **Home**, nel gruppo **Distribuzione** selezionare **Distribuisci il criterio di Windows Update for Business**.
3. Configurare le seguenti impostazioni:
    - **Criteri di configurazione da distribuire**: selezionare il criterio di Windows Update per le aziende che si vuole distribuire.
    - **Raccolta**: fare clic su **Sfoglia** per selezionare la raccolta in cui si vogliono distribuire i criteri.
    - **Monitora e aggiorna le regole non conformi, se supportato**: selezionare per correggere automaticamente tutte le regole non conformi per Strumentazione gestione Windows (WMI), il Registro di sistema, gli script e tutte le impostazioni per i dispositivi mobili registrati da Configuration Manager.
    - **Consenti monitoraggio e aggiornamento fuori dalla finestra di manutenzione**: se è stata configurata una finestra di manutenzione per la raccolta in cui si distribuiscono i criteri, abilitare questa opzione per consentire alle impostazioni di conformità di monitorare e aggiornare il valore fuori dalla finestra di manutenzione. Per altre informazioni sulle finestre di manutenzione, vedere [Come usare le finestre di manutenzione](../clients/manage/collections/use-maintenance-windows.md).
    - **Genera un avviso**: configura un avviso che viene generato se la conformità della linea di base di configurazione è inferiore a una percentuale specificata in base a una data e un orario specifici. È inoltre possibile specificare se si desidera che un avviso venga inviato a System Center Operations Manager.
    - **Ritardo casuale (ore)** : specifica una finestra di ritardo per evitare un'elaborazione eccessiva nel servizio Registrazione dispositivi di rete. Il valore predefinito è 64 ore.
    - **Pianificazione**: specifica la pianificazione per la valutazione della conformità in base alla quale il profilo distribuito viene valutato nei computer client. Può trattarsi di una pianificazione semplice o personalizzata. Il profilo viene valutato dai computer client quando l'utente effettua l'accesso.
4.  Completare la procedura guidata per distribuire il profilo.



## <a name="support-for-entrust-certification-authorities"></a>Supporto per le autorità di certificazione Entrust
<!-- 1350740 -->
Configuration Manager supporta ora l'autorità di certificazione Entrust; ciò consente la consegna del certifica PFX nei dispositivi registrati in Microsoft Intune.

Quando si aggiunge un ruolo di punto di registrazione certificato in Configuration Manager, è possibile configurare Entrust come autorità di certificazione. Quando si aggiunge un nuovo profilo di certificato che emette i certificati PFX, è possibile selezionare l'autorità di certificazione Microsoft o Entrust.

**Problema noto**: nella Technical Preview 1706 i certificati PFX non vengono emessi per le autorità di certificazione di Microsoft. Ciò non influenza i certificati PFX importati o i profili SCEP.


## <a name="cisco-ipsec-support-for-ios-vpn-profiles"></a>Supporto Cisco (IPSec) per i profili VPN iOS
<!-- 1321367 -->

È possibile creare un profilo VPN iOS con Cisco (IPSec) come tipo di connessione. Per altre informazioni, vedere [Creare profili VPN](../../protect/deploy-use/create-vpn-profiles.md#create-a-vpn-profile).


## <a name="new-windows-configuration-item-settings"></a>Nuove impostazioni degli elementi di configurazione di Windows
<!-- 1354715 -->

In questa versione sono state aggiunte le seguenti nuove impostazioni che è possibile usare negli elementi di configurazione di Windows:

### <a name="password"></a>Password

- **Crittografia dispositivo**

### <a name="device"></a>Dispositivo

- **Modifica delle impostazioni dell'area (solo desktop)**
- **Modifica delle impostazioni di risparmio energia e sospensione**
- **Modifiche alle impostazioni della lingua**
- **Modifica dell'ora di sistema**
- **Modifica del nome dispositivo**

### <a name="store"></a>Archivio

- **Aggiorna automaticamente le app dallo Store**
- **Usa solo lo Store privato**
- **Avvio di app originate dallo Store**

### <a name="microsoft-edge"></a>Microsoft Edge

- **Blocca l'accesso ai flag Informazioni su**
- **Override del prompt SmartScreen**
- **Override del prompt SmartScreen per i file**
- **Indirizzo IP localhost WebRtc**
- **Motore di ricerca predefinito**
- **URL XML OpenSearch**
- **Homepages (desktop only)** (Home page (solo desktop))

Per altre informazioni sulle impostazioni di conformità, vedere [Garantire la conformità dei dispositivi con System Center Configuration Manager](../../compliance/understand/ensure-device-compliance.md).


## <a name="new-device-compliance-policy-rules"></a>Nuove regole per i criteri di conformità dei dispositivi

* **Tipo di password richiesto**. Specificare se gli utenti devono creare una password alfanumerica o una password numerica. Per le password alfanumeriche, si specifica anche il numero minimo di set di caratteri che la password deve contenere. I quattro set di caratteri sono: lettere minuscole, lettere maiuscole, simboli e numeri.

  **Supportato in:**
  * Windows Phone 8+
  * Windows 8.1+
  * iOS 6+
<br></br>
* **Blocca il debug USB nel dispositivo**. Non è necessario configurare questa impostazione poiché l'esecuzione del debug dell'USB è già stata disabilitata in Android per i dispositivi di lavoro.

  **Supportato in:**
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
<br></br>
* **Blocca app da origini sconosciute**. Obbligare i dispositivi a impedire l'installazione di app da origini sconosciute. Non è necessario configurare questa impostazione poiché Android per i dispositivi di lavoro limita sempre l'installazione da origini sconosciute.

  **Supportato in:**
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
<br></br>
* **Rendi obbligatoria l'analisi delle minacce nelle app**. Questa impostazione specifica che la funzionalità dell'app di verifica è abilitata nel dispositivo.

  **Supportato in:**
  * Android da 4.2 a 4.4
  * Samsung KNOX Standard 4.0+


## <a name="new-mobile-application-management-policy-settings"></a>Nuove impostazioni dei criteri di gestione delle applicazioni mobili
A partire da questa versione, è possibile usare tre nuove impostazioni di criteri di gestione delle applicazioni per dispositivi mobili (MAM):

- **Blocca acquisizione schermo (solo per dispositivi Android):** Specifica che le funzionalità di acquisizione schermo del dispositivo vengono bloccate quando si usa questa app.

- **Disabilita la sincronizzazione dei contatti:** impedisce all'app di salvare i dati nell'app dei contatti nativa del dispositivo.

- **Disabilita stampa:** impedisce all'app di stampare dati aziendali o dell'istituto di istruzione.

## <a name="android-and-ios-enrollment-restrictions"></a>Restrizioni di registrazione di Android e iOS
<!-- 1290826 -->
A partire da questa versione, gli amministratori possono ora specificare che gli utenti non possono registrare dispositivi Android o iOS personali nel proprio ambiente ibrido. Ciò consente di limitare i dispositivi registrati ai dispositivi pre-dichiarati, di proprietà dell'azienda o ai dispositivi iOS registrati solo con il Device Enrollment Program.

### <a name="try-it-out"></a>Procedura
1. Nell'area di lavoro **Amministrazione** della console di Configuration Manager andare a **Servizi cloud** > **Sottoscrizioni a Microsoft Intune**.
2. Nel gruppo **Sottoscrizione** della scheda **Home** scegliere **Configura piattaforme** e quindi selezionare **Android** o **iOS**.
3. Selezionare **Consenti la registrazione a Intune solo ai dispositivi di proprietà dell'azienda, inclusi i dispositivi predichiarati e i dispositivi con registrazione DEP**.

## <a name="android-for-work-application-management-policy-for-copy-paste"></a>Criteri per la gestione dell'applicazione Android for Work per il copia e incolla
Sono state aggiornate le descrizioni delle impostazioni per Android per gli elementi di configurazione del lavoro per **Consenti la condivisione dei dati tra i profili di lavoro e personali**.

|Prima della Technical Preview 1706 | Nuovo nome dell'opzione | Comportamento|
|-|-|-|
|Impedire qualsiasi condivisione tra i limiti| Restrizioni di condivisione predefinite| Dall'ambito di lavoro a quello personale: predefinito (dovrà essere bloccato in tutte le versioni) <br>Dall'ambito personale a quello di lavoro: predefinito (consentito in 6.x+, bloccato in 5.x)|
|Nessuna restrizione| Le app nel profilo personale possono gestire richieste di condivisione dal profilo di lavoro| Dall'ambito di lavoro a quello personale: Consentito  <br>Dall'ambito personale a quello di lavoro: Consentito|
|Le app nel profilo di lavoro possono gestire richieste di condivisione dal profilo personale |Le app nel profilo di lavoro possono gestire richieste di condivisione dal profilo personale |Dall'ambito di lavoro a quello personale: Predefinito<br>Dall'ambito personale a quello di lavoro: Consentito<br>(utile solamente su 5.x dove l'opzione dall'ambito personale a quello di lavoro è bloccata)|

Nessuna di queste opzioni impedisce direttamente il comportamento di copia e incolla. È stata aggiunta un'impostazione personalizzata al servizio e all'app del Portale aziendale in 1704 che può essere configurata per evitare di copiare e incollare. L'impostazione è configurabile tramite un URI personalizzato.

- URI OMA:  ./Vendor/MSFT/WorkProfile/DisallowCrossProfileCopyPaste
- Tipo valore: Boolean

Impostando DisallowCrossProfileCopyPaste su true si impedisce il comportamento di copia e incolla tra Android for Work personale e i profili di lavoro.

### <a name="try-it-out"></a>Procedura
1. Nella console di Configuration Manager, selezionare **Asset e conformità** > **Panoramica** > **Impostazioni di conformità** > **Elementi di configurazione**.
2. Scegliere **Crea** per creare un nuovo elemento di configurazione e specificare **Nome** e **Android for Work**.
3. Nei gruppi di impostazione del dispositivo da configurare selezionare **Profilo di lavoro** e scegliere **Avanti**.
4. Selezionare un valore per **Consenti la condivisione dei dati tra i profili di lavoro e personali** e completare la procedura guidata.

## <a name="device-health-attestation-assessment-for-compliance-policies-for-conditional-access"></a>Valutazione dell'attestazione dell'integrità dei dispositivi per i criteri di conformità per l'accesso condizionale
<!-- 1097546 -->
A partire da questa versione è possibile usare lo stato dell'attestazione dell'integrità del dispositivo come regola dei criteri di conformità per l'accesso condizionale alle risorse aziendali.

### <a name="try-it-out"></a>Procedura
Selezionare una regola di attestazione dell'integrità dei dispositivi come parte di una valutazione dei criteri di conformità.