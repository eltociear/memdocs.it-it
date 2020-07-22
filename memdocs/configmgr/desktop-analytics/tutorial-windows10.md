---
title: 'Esercitazione: Distribuire Windows 10'
titleSuffix: Configuration Manager
description: Esercitazione sull'uso di Desktop Analytics e Configuration Manager per distribuire Windows 10 in un gruppo pilota.
ms.date: 06/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: tutorial
ms.assetid: 3e82cd96-0ce0-474a-a597-d65fceadc95a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 15cf7f3621f25a82f0e16d5275369ec93225bbf7
ms.sourcegitcommit: 034226b5a60de49a75c7b54e856814f81c03a112
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/16/2020
ms.locfileid: "86422838"
---
# <a name="tutorial-deploy-windows-10-to-pilot"></a>Esercitazione: Distribuire Windows 10 a un gruppo pilota

Questa esercitazione usa Desktop Analytics e Configuration Manager per distribuire Windows 10 in un gruppo pilota. Viene evidenziata l'integrazione del servizio cloud per offrire informazioni dettagliate per la distribuzione di Windows con il prodotto locale. Usare Desktop Analytics per individuare i dispositivi più adatti da inserire in un gruppo pilota. Quindi usare Configuration Manager per la sincronizzazione con Windows.

In questa esercitazione si apprenderà come:  

> [!div class="checklist"]  
> * Configurare Desktop Analytics nel portale di Azure  
> * Connettere Configuration Manager e configurare le impostazioni del dispositivo  
> * Creare un piano di distribuzione di Desktop Analytics per Windows 10  
> * Usare Configuration Manager per distribuire Windows 10 al gruppo pilota  

Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free) prima di iniziare. Se configurato correttamente, l'uso di Desktop Analytics non comporta costi di Azure.

Desktop Analytics usa un'*area di lavoro Log Analytics* nella sottoscrizione di Azure. Un'area di lavoro è sostanzialmente un contenitore che include informazioni sull'account e semplici informazioni di configurazione per l'account. Per altre informazioni, vedere [Gestire le aree di lavoro](https://docs.microsoft.com/azure/log-analytics/log-analytics-manage-access?toc=/azure/azure-monitor/toc.json).



## <a name="prerequisites"></a>Prerequisiti

Prima di iniziare questa esercitazione, verificare di avere i prerequisiti seguenti:  

- Una sottoscrizione di Azure attiva con autorizzazioni [**Amministratore globale**](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#company-administrator-permissions)  

    Per altre informazioni, vedere [Prerequisiti di Desktop Analytics](overview.md#prerequisites).

- Configuration Manager versione 1902 con aggiornamento cumulativo (4500571) o versione successiva con ruolo **Amministratore completo**  

- Supporto di installazione per l'ultima versione di Windows 10

- Almeno un dispositivo Windows 10 con le configurazioni seguenti:  

    - Windows 10 versione 1709 o successiva, ma inferiore alla versione del supporto di installazione che si prevede di usare

    - Aggiornamento qualitativo cumulativo più recente di Windows 10  

    - Client Configuration Manager versione 1902 con aggiornamento cumulativo (4500571) o versione successiva  

- Approvazione aziendale per configurare il livello dei dati di diagnostica di Windows su **Avanzata (con limitazioni)** nei dispositivi pilota  

    Per altre informazioni, vedere [Privacy di Desktop Analytics](privacy.md).

- Connettività di rete dal dispositivo agli endpoint Internet seguenti:

    - `https://v10c.events.data.microsoft.com`  
    - `https://settings-win.data.microsoft.com`  
    - `http://adl.windows.com`  
    - `https://watson.telemetry.microsoft.com`  
    - `https://umwatsonc.events.data.microsoft.com`  
    - `https://ceuswatcab01.blob.core.windows.net`  
    - `https://ceuswatcab02.blob.core.windows.net`  
    - `https://eaus2watcab01.blob.core.windows.net`  
    - `https://eaus2watcab02.blob.core.windows.net`  
    - `https://weus2watcab01.blob.core.windows.net`  
    - `https://weus2watcab02.blob.core.windows.net`  
    - `https://kmwatsonc.events.data.microsoft.com`  
    - `https://oca.telemetry.microsoft.com`  
    - `https://login.live.com`  
    - `https://graph.windows.net` (solo nel ruolo del server di Configuration Manager)
    - `https://*.manage.microsoft.com` (solo nel ruolo del server di Configuration Manager)

    Per altre informazioni, vedere [Come abilitare la condivisione dei dati per Desktop Analytics](enable-data-sharing.md#endpoints).  

> [!Important]  
> Questi prerequisiti sono ai fini di questa esercitazione. Per altre informazioni sui prerequisiti generali per Desktop Analytics con Configuration Manager, vedere [Prerequisiti](overview.md#prerequisites).  



## <a name="set-up-desktop-analytics"></a>Configurare Desktop Analytics

Usare questa procedura per accedere a Desktop Analytics e configurarlo nella sottoscrizione. Si tratta di un processo che viene eseguito una sola volta per configurare Desktop Analytics per l'organizzazione.  

1. Aprire il [portale di Desktop Analytics](https://aka.ms/desktopanalytics) in Gestione dei dispositivi per Microsoft 365 come utente con le autorizzazioni **Amministratore globale**. Selezionare **Inizio**.  

2. Nella pagina **Accetta il contratto di servizio** esaminare il contratto di servizio e selezionare **Accetta**.  

3. Nella pagina **Confermare l'abbonamento** l'elenco delle licenze valide obbligatorie è per le funzionalità di integrità dei dispositivi Windows di Desktop Analytics. Selezionare **Avanti** per continuare.  

4. Nella pagina **Concedere l'accesso a utenti**:

    - **Consentire a Desktop Analytics di gestire i ruoli della directory per conto dell'utente**: Desktop Analytics assegna automaticamente ai **Proprietari dell'area di lavoro** il ruolo **Amministratore di Desktop Analytics**. Se ai gruppi è già assegnato un **Amministratore globale**, non vengono apportate modifiche.  

        Se non si seleziona questa opzione, Desktop Analytics aggiunge comunque gli utenti come membri del gruppo di sicurezza. Un **Amministratore globale** deve assegnare manualmente il ruolo **Amministratore di Desktop Analytics** per gli utenti.  

        Per altre informazioni sull'assegnazione delle autorizzazioni del ruolo di amministratore in Azure Active Directory e sulle autorizzazioni assegnate agli **Amministratori di Desktop Analytics**, vedere [Autorizzazioni del ruolo Amministratore in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles).  

    - Desktop Analytics preconfigura il gruppo di sicurezza **Proprietari dell'area di lavoro** in Azure Active Directory per creare e gestire aree di lavoro e piani di distribuzione. 

        Per aggiungere un utente al gruppo, digitarne il nome o l'indirizzo di posta elettronica nella sezione **Immettere il nome o l'indirizzo di posta elettronica**. Al termine, selezionare **Avanti**.

5. Nella pagina **Configura la tua area di lavoro**:  

    > [!Note]  
    > Per completare questo passaggio, l'utente deve avere le autorizzazioni **Proprietario dell'area di lavoro** e l'accesso aggiuntivo alla sottoscrizione di Azure e al gruppo di risorse. Per altre informazioni, vedere i [prerequisiti](overview.md#prerequisites).  

    - Selezionare la sottoscrizione di Azure.  

    - Per usare un'area di lavoro esistente per Desktop Analytics, selezionarla e continuare con il passaggio successivo.  

    - Per creare un'area di lavoro per Desktop Analytics, selezionare **Aggiungi area di lavoro**.  

        1. Immettere un **Nome dell'area di lavoro**.  

        2. Selezionare l'elenco a discesa per **selezionare il nome della sottoscrizione di Azure per l'area di lavoro** e scegliere la sottoscrizione di Azure per l'area di lavoro.  

        3. Per il gruppo di risorse, scegliere **Crea nuovo** o **Usa esistente**.  

        4. Selezionare l'**Area** dall'elenco, quindi selezionare **Aggiungi**.  

6. Selezionare un'area di lavoro nuova o esistente, quindi selezionare **Set as Desktop Analytics workspace** (Imposta come area di lavoro di Desktop Analytics).  Quindi selezionare **Continua** nella finestra di dialogo **Conferma e concedi l'accesso**.  

7. Nella nuova scheda del browser selezionare un account da usare per l'accesso. Selezionare l'opzione **Acconsenti per conto dell'organizzazione** e selezionare **Accetta**.  


    > [!Note]  
    > Questo consenso assegna all'applicazione MALogAnalyticsReader il ruolo Lettore di Log Analytics per l'area di lavoro. Questo ruolo applicazione è richiesto da Desktop Analytics. Per altre informazioni, vedere [Ruolo applicazione MALogAnalyticsReader](troubleshooting.md#bkmk_MALogAnalyticsReader).  

8. Tornare alla pagina **Configura la tua area di lavoro** e selezionare **Avanti**.  

9. Nella pagina **Last steps** (Ultimi passaggi) selezionare **Vai a Desktop Analytics**. Nel portale di Azure viene visualizzata la pagina **Home page** di Desktop Analytics.  



## <a name="connect-configuration-manager"></a>Connettere Configuration Manager

Usare questa procedura per aggiornare Configuration Manager, connettersi a Desktop Analytics e configurare le impostazioni del dispositivo. Questa procedura è un processo singolo per l'associazione della gerarchia al servizio cloud.  

### <a name="update-configuration-manager"></a>Aggiornare Configuration Manager

Installare l'aggiornamento cumulativo versione 1902 (4500571) di Configuration Manager per supportare l'integrazione con Desktop Analytics. Per altre informazioni su questo aggiornamento, vedere [Aggiornamento cumulativo per Configuration Manager Current Branch, versione 1902](https://support.microsoft.com/help/4500571).

1. Aggiornare il sito con l'aggiornamento cumulativo per la versione 1902. Per altre informazioni, vedere [Installare gli aggiornamenti nella console](../core/servers/manage/install-in-console-updates.md).  

2. Aggiornare i client. Per semplificare questo processo, è consigliabile usare l'aggiornamento automatico. Per altre informazioni, vedere [Aggiornare i client](../core/clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade).  


### <a name="connect-to-the-service"></a>Connettersi al servizio

1. Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Servizi cloud** e selezionare il nodo **Servizi di Azure**. Selezionare **Configura i servizi di Azure** nella barra multifunzione.  

2. Nella pagina **Servizi di Azure** della Procedura guidata per i servizi di Azure configurare le impostazioni seguenti:  

    - Specificare un **Nome** per l'oggetto in Configuration Manager  

    - Specificare una **Descrizione** facoltativa per identificare il servizio  

    - Selezionare **Desktop Analytics** dall'elenco dei servizi disponibili  
  
   Selezionare **Avanti**.  

3. Nella pagina **App** selezionare l'**Ambiente di Azure** appropriato. Quindi selezionare **Sfoglia** per l'app Web.

4. Selezionare **Crea** per aggiungere con facilità un'app Azure AD per la connessione a Desktop Analytics.

5. Configurare le impostazioni seguenti nella finestra **Crea un'applicazione server**:  

    - **Nome applicazione**: nome descrittivo per l'app in Azure AD.

    - **URL della home page**: questo valore non viene usato da Configuration Manager, ma è richiesto da Azure AD. Per impostazione predefinita, questo valore è impostato su `https://ConfigMgrService`.  

    - **URI ID app**: questo valore deve essere univoco nel tenant di Azure AD. È incluso nel token di accesso usato dal client Configuration Manager per richiedere l'accesso al servizio. Per impostazione predefinita, questo valore è impostato su `https://ConfigMgrService`.  

    - **Periodo di validità della chiave privata**: scegliere **1 anno** o **2 anni** dall'elenco a discesa. Il valore predefinito è 1 anno.  

    Selezionare **Accedi**. Dopo l'autenticazione in Azure, nella pagina viene visualizzato il **Nome del tenant di Azure AD** come riferimento.

    > [!Note]  
    > Completare questo passaggio come **Amministratore globale**. Queste credenziali non vengono memorizzate in Configuration Manager. Questo utente tipo non richiede autorizzazioni in Configuration Manager e non deve necessariamente essere lo stesso account che esegue la procedura guidata per i servizi di Azure.  

    Selezionare **OK** per creare l'app Web in Azure AD e chiudere la finestra di dialogo Crea un'applicazione server. Nella finestra di dialogo App server selezionare **OK**. Selezionare **Avanti** nella pagina App della Procedura guidata per i servizi di Azure.  

6. Nella pagina **Dati di diagnostica** configurare le impostazioni seguenti:  

    - **ID commerciale**: questo valore deve essere popolato automaticamente con l'ID dell'organizzazione  

    - **Livello dei dati di diagnostica di Windows 10**: selezionare almeno **Avanzata (con limitazioni)**  

    - **Consenti il nome del dispositivo nei dati di diagnostica**: selezionare **Abilita**  
  
   Selezionare **Avanti**. La pagina **Funzionalità disponibile** mostra la funzionalità Desktop Analytics disponibile con le impostazioni dei dati di diagnostica della pagina precedente. Selezionare **Avanti**.  

7. Nella pagina **Raccolte** configurare le impostazioni seguenti:  

    - **Nome visualizzato**: Il portale di Desktop Analytics visualizza questa connessione a Configuration Manager usando questo nome. Usare il nome per distinguere le diverse gerarchie. Ad esempio, *lab di test* o *produzione*.  

    - **Raccolta di destinazione**: Questa raccolta include tutti i dispositivi che Configuration Manager configura con l'ID commerciale e le impostazioni dei dati di diagnostica. Si tratta del set completo di dispositivi che Configuration Manager connette al servizio Desktop Analytics.  

    - **I dispositivi nella raccolta di destinazione usano un proxy autenticato dall'utente per le comunicazioni in uscita**: Per impostazione predefinita, questo valore è **No**. Se necessario nell'ambiente in uso, impostare su **Sì**.  

    - **Selezionare raccolte specifiche da sincronizzare con Desktop Analytics**: Selezionare **Aggiungi** per includere altre raccolte. Queste raccolte sono disponibili nel portale di Desktop Analytics per il raggruppamento con i piani di distribuzione. Assicurarsi di includere le raccolte pilota e di esclusioni pilota.  

        Queste raccolte continuano a essere sincronizzate quando viene modificata l'appartenenza. Il piano di distribuzione, ad esempio, usa una raccolta con una regola di appartenenza di Windows 7. Quando i dispositivi eseguono l'aggiornamento a Windows 10 e Configuration Manager valuta l'appartenenza alla raccolta, i dispositivi escono dalla raccolta e dal piano di distribuzione.  

8. Completare la procedura guidata.  

Configuration Manager crea criteri di impostazioni per configurare i dispositivi nella raccolta di destinazione. Questi criteri includono le impostazioni dei dati di diagnostica per abilitare i dispositivi all'invio di dati a Microsoft. Per impostazione predefinita, i client aggiornano i criteri ogni ora. Dopo aver ricevuto le nuove impostazioni, può essere necessario attendere diverse ore prima che i dati siano disponibili in Desktop Analytics.

> [!Note]  
> Per altre informazioni su queste impostazioni, vedere [Impostazioni di Windows](enroll-devices.md#windows-settings).  

Monitorare la configurazione dei dispositivi per Desktop Analytics. Nella console di Configuration Manager passare all'area di lavoro **Raccolta software**, espandere il nodo **Manutenzione di Desktop Analytics** e selezionare il dashboard **Integrità connessione**.  

Configuration Manager sincronizza le raccolte entro 60 minuti dalla creazione della connessione. Nel portale di Desktop Analytics passare a **Pilota globale** e visualizzare le raccolte di dispositivi di Configuration Manager. Possono essere necessari due o tre giorni per visualizzare i dati completi nel resto del portale. Per altre informazioni, vedere [Latenza dei dati](troubleshooting.md#data-latency).

## <a name="create-a-desktop-analytics-deployment-plan"></a>Creare un piano di distribuzione di Desktop Analytics

Usare questa procedura per creare un piano di distribuzione in Desktop Analytics.

1. Aprire il [portale di Desktop Analytics](https://aka.ms/desktopanalytics). Usare credenziali con almeno le autorizzazioni **Collaboratori dell'area di lavoro**.  

2. Selezionare **Piani di distribuzione** nel gruppo Gestisci.  

3. Nel riquadro **Piani di distribuzione** selezionare **Crea**.  

4. Nella riquadro **Crea piano di distribuzione** configurare le impostazioni seguenti:  

    - **Nome**: Nome univoco per il piano di distribuzione, ad esempio `Windows 10 pilot`  

    - **Prodotti e versioni**: scegliere la versione di Windows 10 da distribuire. Microsoft consiglia di creare piani di distribuzione che usano la versione più recente.

    - **Gruppi di dispositivi**: Selezionare uno o più gruppi dalla scheda Configuration Manager e quindi selezionare **Imposta come gruppi di destinazione**. Questi gruppi sono raccolte sincronizzate da Configuration Manager.  

    - **Regole di idoneità**: queste regole consentono di individuare i dispositivi idonei per l'aggiornamento. Selezionare **Sistema operativo Windows** e configurare le impostazioni seguenti:  

        - **Il mio computer scarica automaticamente i driver da Windows Update**: L'impostazione predefinita è **No**, consigliata quando si esegue la distribuzione con Configuration Manager.  

        - **Definire una soglia di numero di installazioni basso per le proprie app**: L'impostazione predefinita è `2%`. Le app al di sotto di questa soglia vengono impostate automaticamente su *Numero di installazioni basso*. Desktop Analytics non convalida questi componenti aggiuntivi durante il progetto pilota.  

            Se un'app viene installata in una percentuale di computer superiore a questa soglia, il piano di distribuzione contrassegna l'app come *importanti*. È quindi possibile deciderne l'importanza da testare durante la fase pilota.  

    - **Data di completamento**: scegliere la data entro cui Windows deve essere completamente distribuito in tutti i dispositivi di destinazione.  

5. Selezionare **Crea**. Il nuovo piano viene visualizzato nell'elenco dei piani di distribuzione durante l'elaborazione. Per velocizzare l'elaborazione, richiedere un aggiornamento dati su richiesta. Per altre informazioni, vedere [Domande frequenti su Desktop Analytics](faq.md#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).

6. Aprire il piano di distribuzione selezionandone il nome.  

7. Nel menu del piano di distribuzione nel gruppo **Preparazione** selezionare **Identificazione dell'importanza**.  

    1. Nella scheda **App** selezionare l'opzione per visualizzare solo le risorse **Non riviste**.  

    2. Selezionare ogni app, quindi selezionare **Modifica**. È possibile selezionare più app da modificare contemporaneamente.  

    3. Scegliere un livello di importanza dall'elenco **Importanza**. Se si vuole che l'app venga convalidata da Desktop Analytics durante il progetto pilota, selezionare **Critica** o **Importante**. Non viene eseguita la convalida delle app contrassegnate come **Non importante**. Quando si assegnano i livelli di importanza, valutare la [compatibilità](compat-assessment.md) e altre informazioni dettagliate sui piani.  

        Quando si assegnano i livelli di importanza è anche possibile scegliere la decisione di aggiornamento.  

    4. Al termine, selezionare **Salva**.  

8. Nel menu del piano di distribuzione nel gruppo **Preparazione** selezionare **Identifica gruppo pilota**.  

    1. Esaminare i dispositivi consigliati per il progetto pilota.  

    2. Selezionare ogni dispositivo e scegliere **Aggiungi al gruppo pilota**. Se non si è d'accordo con quanto consigliato, selezionare **Sostituisci**.  

        Per altre informazioni sulle raccomandazioni di Desktop Analytics, selezionare l'icona Informazioni nell'angolo superiore destro del riquadro **Identifica gruppo pilota**.



## <a name="deploy-windows-10-in-configuration-manager"></a>Distribuire Windows 10 in Configuration Manager

Usare questa procedura per distribuire Windows 10 in Configuration Manager al gruppo pilota.

- Se non è già presente, [creare un pacchetto di aggiornamento del sistema operativo per Windows 10](#bkmk_create-package)  

- Se non è già presente, [creare una sequenza di attività di aggiornamento del sistema operativo per Windows 10](#bkmk_create-ts)  

- [Distribuire la sequenza di attività](#bkmk_deploy-ts) usando il piano di distribuzione di Desktop Analytics  

- [Installare la sequenza di attività](#bkmk_install-ts) da Software Center in un dispositivo di destinazione  

<!-- 
- [Monitor](#bkmk_monitor-ts) status in Configuration Manager  
 -->

### <a name="create-an-os-upgrade-package-for-windows-10"></a><a name="bkmk_create-package"></a> Creare un pacchetto di aggiornamento del sistema operativo per Windows 10

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**, espandere **Sistemi operativi** e selezionare il nodo **Pacchetti di aggiornamento del sistema operativo**.  

2. Nella scheda **Home** della barra multifunzione, nel gruppo **Crea** selezionare **Aggiungi pacchetto di aggiornamento del sistema operativo**. Questa azione avvia l'Aggiunta guidata del pacchetto di aggiornamento del sistema operativo.  

3. Nella pagina **Origine dati** specificare il **Percorso** di rete dei file di origine dell'installazione del pacchetto di aggiornamento del sistema operativo. Ad esempio, `\\server\share\path`  

    > [!NOTE]  
    > I file di origine dell'installazione contengono Setup.exe e altri file e cartelle per installare il sistema operativo.  

4. Nella pagina **Generale** specificare un **Nome** univoco per il pacchetto di aggiornamento del sistema operativo.  

5. Completare l'Aggiunta guidata del pacchetto di aggiornamento del sistema operativo.  

#### <a name="distribute-content"></a>Distribuire il contenuto

Quindi distribuire il pacchetto di aggiornamento del sistema operativo ai punti di distribuzione.  

1. Selezionare il pacchetto di aggiornamento del sistema operativo nell'elenco. Nella scheda **Home** della barra multifunzione selezionare **Distribuisci contenuto** nel gruppo **Distribuzione**. Viene visualizzata la Distribuzione guidata contenuto.  

2. Nella pagina **Generale** verificare che il contenuto elencato sia quello da distribuire, quindi selezionare **Avanti**.  

3. Nella pagina **Destinazione contenuto** scegliere **Aggiungi**, quindi **Punto di distribuzione**. Selezionare un punto di distribuzione esistente e quindi fare clic su **OK**. Dopo aver aggiunto le destinazioni del contenuto, selezionare **Avanti**.  

4. Completare la Distribuzione guidata contenuto.  


### <a name="create-an-os-upgrade-task-sequence-for-windows-10"></a><a name="bkmk_create-ts"></a> Creare una sequenza di attività di aggiornamento del sistema operativo per Windows 10

1. Nella console di Configuration Manager passare all'area di lavoro **Raccolta software**, espandere **Sistemi operativi** e quindi selezionare **Sequenze di attività**.  

2. Nella scheda **Home** della barra multifunzione nel gruppo **Crea** selezionare **Crea sequenza di attività**.  

3. Nella pagina **Crea una nuova sequenza di attività** della Creazione guidata della sequenza di attività selezionare **Aggiorna sistema operativo dal pacchetto di aggiornamento** e quindi selezionare **Avanti**.  

4. Nella pagina **Informazioni sequenza di attività** specificare un **Nome sequenza di attività** che identifichi la sequenza di attività.  

5. Nella pagina **Aggiorna il sistema operativo Windows** specificare le impostazioni seguenti e quindi selezionare **Avanti**:  

    - **Pacchetto di aggiornamento**: specificare il pacchetto di aggiornamento che contiene i file di origine per l'aggiornamento del sistema operativo.  

    - **Indice dell'edizione**: se nel pacchetto sono disponibili più indici dell'edizione del sistema operativo, selezionare l'indice dell'edizione desiderato. Per impostazione predefinita, la procedura guidata seleziona il primo indice.  

    - **Codice Product Key**: specificare il codice Product Key Windows per il sistema operativo da installare. Specificare i codici Product Key per contratti multilicenza codificati o i codici Product Key standard. Se si usa un codice Product Key standard, separare ogni gruppo di cinque caratteri con un trattino (-). Ad esempio: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*. Se l'aggiornamento è per un'edizione per contratti multilicenza, il codice Product Key potrebbe non essere obbligatorio.  

        > [!Note]  
        > Questo codice Product Key può essere un codice ad attivazione multipla (MAK) o un codice generico di contratti multilicenza (GVLK). Un codice GVLK è anche definito codice di configurazione client del servizio di gestione delle chiavi (KMS). Per altre informazioni, vedere [Pianificare l'attivazione dei contratti multilicenza](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client). Per un elenco di codici di configurazione client KMS, vedere l'[Appendice A](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys) della Guida di attivazione di Windows Server.

6. Nella pagina **Includi aggiornamenti** selezionare **Avanti** per non installare alcun aggiornamento software.  

7. Nella pagina **Installa applicazioni** selezionare **Avanti** per non installare alcuna applicazione.

8. Completare la Creazione guidata della sequenza di attività.  


### <a name="deploy-the-task-sequence-using-the-desktop-analytics-deployment-plan"></a><a name="bkmk_deploy-ts"></a> Distribuire la sequenza di attività usando il piano di distribuzione di Desktop Analytics

1. Nella console di Configuration Manager passare a **Raccolta software**, espandere **Manutenzione di Desktop Analytics** e selezionare il nodo **Piani di distribuzione**.  

2. Selezionare il piano di distribuzione pilota di Windows 10 e quindi selezionare **Dettagli del piano di distribuzione** nella barra multifunzione.  

3. Nel riquadro **Stato della distribuzione pilota** scegliere **Sequenza di attività** dall'elenco a discesa e quindi selezionare **Distribuisci**.  

4. Nella pagina **Generale** della Distribuzione guidata del software selezionare **Sfoglia** accanto al campo **Software**. Selezionare la sequenza di attività di aggiornamento sul posto di Windows 10 e selezionare **Avanti**.  

    > [!Note]  
    > Con l'integrazione di Desktop Analytics, Configuration Manager crea automaticamente raccolte pilota e di produzione per il piano di distribuzione. Prima di poterle usare, può essere necessario attendere che venga eseguita la sincronizzazione di queste raccolte. Per altre informazioni, vedere [Risolvere i problemi - Latenza dei dati](troubleshooting.md#data-latency).<!-- 4984639 -->
    >
    > Questa raccolta è riservata ai dispositivi del piano di distribuzione di Desktop Analytics. Le modifiche manuali a questa raccolta non sono supportate.<!-- 3866460, SCCMDocs-pr 3544 -->  

5. Nella pagina **Contenuto** selezionare **Aggiungi**, quindi **Punto di distribuzione**. Selezionare un punto di distribuzione disponibile per ospitare il contenuto di installazione e scegliere **OK**. Selezionare quindi **Avanti**.  

6. Nella pagina **Impostazioni di distribuzione** selezionare **Avanti** per accettare le impostazioni predefinite. (Un'installazione disponibile).  

7. Nella pagina **Pianificazione** selezionare **Avanti** per accettare le impostazioni predefinite. (Disponibile appena possibile).  

8. Nella pagina **Esperienza utente** selezionare **Avanti** per accettare le impostazioni predefinite. (Visualizzare in Software Center e mostrare solo le notifiche per il ravvio del computer).  

9. Nella pagina **Avvisi** selezionare **Avanti** per accettare le impostazioni predefinite.  

10. Completare la procedura guidata.  


### <a name="install-the-task-sequence-from-software-center"></a><a name="bkmk_install-ts"></a> Installare la sequenza di attività da Software Center

1. Accedere a un dispositivo che è membro del piano di distribuzione pilota.  

2. Aprire **Software Center** e installare il sistema operativo disponibile per Windows 10.  


<!--
### <a name="bkmk_monitor-app"></a> Monitor status in Configuration Manager
-->


## <a name="next-steps"></a>Passaggi successivi

Passare all'articolo successivo per altre informazioni sui piani di distribuzione di Desktop Analytics.
> [!div class="nextstepaction"]  
> [Piani di distribuzione](about-deployment-plans.md)
