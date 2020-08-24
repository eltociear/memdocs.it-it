---
title: Risolvere i problemi di Desktop Analytics
titleSuffix: Configuration Manager
description: Dettagli tecnici che consentono di risolvere i problemi relativi a Desktop Analytics.
ms.date: 08/10/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 63e08f3f-9558-4ed7-9bf3-3a185ddaac5c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: e83e8d5d967b4cd3bbcb817c149cd40284bb5f9c
ms.sourcegitcommit: 66c58078a32af3872d98f7c62af4f8047ee81b50
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/11/2020
ms.locfileid: "88089946"
---
# <a name="troubleshoot-desktop-analytics"></a>Risolvere i problemi di Desktop Analytics

I dettagli illustrati in questo articolo consentono di risolvere i problemi relativi a Desktop Analytics integrato con Configuration Manager.

## <a name="confirm-prerequisites"></a>Confermare i prerequisiti

Molti problemi comuni sono dovuti a prerequisiti mancanti. Per prima cosa confermare le configurazioni seguenti:

- [Prerequisiti](overview.md#prerequisites)  

- [Aggiornamenti dei componenti di Windows](enroll-devices.md#update-devices)  

- [Come abilitare la condivisione dei dati](enable-data-sharing.md), che include gli argomenti seguenti:  

  - Endpoint Internet a cui i client devono connettersi  

  - Autenticazione del server proxy  

  - Livelli dei dati di diagnostica  

## <a name="monitor-connection-health"></a>Monitorare l'integrità della connessione

Usare il dashboard **Integrità connessione** in Configuration Manager per eseguire il drill-down delle categorie in base all'integrità del dispositivo. Nella console di Configuration Manager passare all'area di lavoro **Raccolta software**, espandere il nodo **Manutenzione di Desktop Analytics** e selezionare il dashboard **Integrità connessione**.  

Per altre informazioni, vedere [Monitorare l'integrità della connessione](monitor-connection-health.md).

> [!NOTE]
> La connessione di Configuration Manager a Desktop Analytics si basa sul punto di connessione del servizio. Eventuali modifiche apportate a questo ruolo del sistema del sito possono avere effetto sulla sincronizzazione con il servizio cloud. Per altre informazioni, vedere [Informazioni sul punto di connessione del servizio](../core/servers/deploy/configure/about-the-service-connection-point.md#bkmk_move).

A partire dalla versione 2002, se il server del sito di Configuration Manager non riesce a connettersi agli endpoint necessari per un servizio cloud, genera un messaggio di stato critico con ID 11488. Quando non è in grado di connettersi al servizio, lo stato del componente SMS_SERVICE_CONNECTOR diventa critico. Visualizzare lo stato dettagliato nel nodo [Stato componente](../core/servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus) della console di Configuration Manager.<!-- 5566763 -->

## <a name="log-files"></a>File di registro

Per altre informazioni, vedere [File di log per Desktop Analytics](../core/plan-design/hierarchy/log-files.md#desktop-analytics)

A partire da Configuration Manager versione 1906, usare lo strumento **DesktopAnalyticsLogsCollector.ps1** dalla directory di installazione di Configuration Manager per facilitare la risoluzione dei problemi di Desktop Analytics. Lo strumento esegue alcuni passaggi di base per la risoluzione dei problemi e raccoglie i log di rilievo in un'unica directory di lavoro. Per altre informazioni, vedere [Agente di raccolta dei log](log-collector.md).

### <a name="enable-verbose-logging"></a>Abilita la registrazione dettagliata

1. Nel punto di connessione del servizio passare alla chiave del Registro di sistema seguente: `HKLM\Software\Microsoft\SMS\Tracing\SMS_SERVICE_CONNECTOR`  
2. Impostare il valore **LoggingLevel** su `0`  

## <a name="azure-ad-applications"></a><a name="bkmk_AzureADApps"></a> Applicazioni Azure AD

Desktop Analytics aggiunge le applicazioni seguenti ad Azure AD:

- **Microservizio Configuration Manager**: consente di connettere Configuration Manager con Desktop Analytics. Questa app non presenta requisiti di accesso.  

- **MALogAnalyticsReader**: consente di monitorare l'area di lavoro di Azure Log Analytics per assicurarsi che lo snapshot giornaliero venga copiato correttamente. Per altre informazioni, vedere [Ruolo applicazione MALogAnalyticsReader](#bkmk_MALogAnalyticsReader).  

- **Desktop Analytics**: consente a Configuration Manager il recupero delle informazioni sul piano di distribuzione e dello stato di idoneità dei dispositivi Desktop Analytics.

Se è necessario effettuare il provisioning di queste app dopo aver completato l'installazione, andare al riquadro **Servizi connessi**. Selezionare **Configurare l'accesso a utenti e applicazioni** ed effettuare il provisioning delle app.  

- **App Azure AD per Configuration Manager**. Se è necessario eseguire il provisioning o risolvere i problemi di connessione dopo aver completato l'installazione, vedere [Creare e importare app per Configuration Manager](#create-and-import-app-for-configuration-manager). Questa app richiede le autorizzazioni **Write CM Collection Data** (Scrivi dati raccolta CM) e **Read CM Collection Data** (Leggi dati raccolta CM) nell'API del **servizio Configuration Manager**.  

    > [!NOTE]
    > Desktop Analytics supporta più gerarchie di Configuration Manager che dipendono da un singolo tenant di Azure AD.<!-- 4814075 --> In caso di gerarchie multiple configurate con lo stesso ID commerciale all'interno di un ambiente, usare [app diverse](connect-configmgr.md#bkmk_connect) per ciascuna gerarchia per condividere il tenant di Azure AD e l'istanza di Desktop Analytics.

### <a name="create-and-import-app-for-configuration-manager"></a>Creare e importare app per Configuration Manager

Se non è possibile creare l'app Azure AD per Configuration Manager dalla configurazione guidata dei servizi di Azure o se si vuole riutilizzare un'app esistente, è necessario crearla e importarla manualmente. Dopo aver completato l'[Onboarding iniziale](set-up.md#initial-onboarding) nel portale di Desktop Analytics, seguire questa procedura:

#### <a name="create-app-in-azure-ad"></a>Creare l'app in Azure AD

1. Aprire il [portale di Azure](https://portal.azure.com) come utente con autorizzazioni *amministratore globale*, passare a **Azure Active Directory** e selezionare **Registrazioni app**. Selezionare quindi **Nuova registrazione**.  

2. Nel pannello **Crea** configurare le impostazioni seguenti:  

    - **Nome**: nome univoco che identifica l'app, ad esempio: `Desktop-Analytics-Connection`  

    - **Tipi di account supportati**: **Account solo in questa directory organizzativa (Contoso)**

    - **URI di reindirizzamento (facoltativo)** : **Web**  

    <!--     - **Sign-on URL**: this value isn't used by Configuration Manager, but required by Azure AD. Enter a unique and valid URL, for example: `https://configmgrapp`   -->
  
    Selezionare **Registra**.  

3. Selezionare l'app, annotare l'**ID dell'applicazione (client)** e l'**ID della directory (tenant)** . I valori sono GUID usati per configurare la connessione di Configuration Manager.  

4. Nel menu **Gestisci** selezionare **Certificati e segreti**. Selezionare **Nuovo segreto client**. Immettere una **Descrizione**, specificare una durata di scadenza e quindi selezionare **Aggiungi**. Copiare il **Valore** della chiave usata per configurare la connessione di Configuration Manager.

    > [!Important]  
    > Questa è l'unica opportunità per copiare il valore della chiave. Se non lo si copia adesso, sarà necessario creare un'altra chiave.  
    >
    > Salvare il valore della chiave in una posizione sicura.  

5. Nel menu **Gestisci** selezionare **Autorizzazioni API**.  

    1. Nel pannello **Autorizzazioni API** selezionare **Aggiungi un'autorizzazione**.  

    2. Nel pannello **Richiedi le autorizzazioni dell'API** passare a **API usate dall'organizzazione**.  

    3. Cercare e selezionare l'API del **microservizio Configuration Manager**.  

    4. Selezionare il gruppo **Autorizzazioni applicazione**. Espandere **CmCollectionData** e selezionare entrambe le autorizzazioni seguenti: **Write CM Collection Data** (Scrivi dati raccolta CM) e **Read CM Collection Data** (Leggi dati raccolta CM).  

    5. Selezionare **Aggiungi autorizzazioni**.  

6. Nel pannello **Autorizzazioni API** selezionare **Fornisci il consenso amministratore**. Selezionare **Sì**.  

#### <a name="import-app-in-configuration-manager"></a>Importare le app in Configuration Manager

1. Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Servizi cloud** e selezionare il nodo **Servizi di Azure**. Selezionare **Configura i servizi di Azure** nella barra multifunzione.  

2. Nella pagina **Servizi di Azure** della procedura guidata per i servizi di Azure configurare le impostazioni seguenti:  

    - Specificare un **Nome** per l'oggetto in Configuration Manager.  

    - Specificare un parametro facoltativo **Descrizione** per identificare il servizio.  

    - Selezionare **Desktop Analytics** dall'elenco dei servizi disponibili.  
  
   Selezionare **Avanti**.  

3. Nella pagina **App** selezionare l'**Ambiente di Azure** appropriato. Selezionare quindi **Importa** per l'app Web. Configurare le impostazioni seguenti nella finestra **Importa le app**:  

    - **Nome del tenant di Azure AD**: corrisponde al nome in Configuration Manager  

    - **ID tenant di Azure AD**: **ID directory** copiato da Azure AD  

    - **Client ID** (ID client): **ID applicazione** copiato dall'app Azure AD  

    - **Chiave privata**: **Valore** della chiave copiato dall'app Azure AD  

    - **Scadenza della chiave privata**: la stessa data di scadenza della chiave  

    - **URI ID app**: questa impostazione dovrebbe essere popolata automaticamente con il valore seguente: `https://cmmicrosvc.manage.microsoft.com/`  
  
   Selezionare **Verifica** e quindi **OK** per chiudere la finestra di dialogo Importa le app. Selezionare **Avanti** nella pagina App della Procedura guidata per i servizi di Azure.  

Per continuare il resto della procedura guidata nella pagina **Dati di diagnostica**, vedere [Connettersi al servizio](connect-configmgr.md#bkmk_connect).

#### <a name="troubleshoot-app-in-configuration-manager"></a>Risolvere i problemi delle app in Configuration Manager

Se si incontrano problemi durante la creazione o l'importazione dell'app, controllare prima **SMSAdminUI. log** per l'errore specifico. Verificare quindi le configurazioni seguenti:

- Il tenant è stato registrato correttamente nel servizio Desktop Analytics. Per altre informazioni, vedere [Come configurare Desktop Analytics](set-up.md).

- Tutti gli endpoint necessari sono accessibili. Per altre informazioni, vedere [Endpoint](enable-data-sharing.md#endpoints).

- Verificare che l'utente che accede abbia le autorizzazioni corrette. Per altre informazioni, vedere [Prerequisiti](overview.md#prerequisites).

- Verificare che l'utente possa accedere ad Azure in generale. Questa azione determina se sono presenti problemi generali di autenticazione di Azure AD.

- Controllare i messaggi di stato per il componente **SMS_SERVICE_CONNECTOR** relativo al *ruolo di lavoro Desktop Analytics*.

### <a name="maloganalyticsreader-application-role"></a><a name="bkmk_MALogAnalyticsReader"></a> Ruolo applicazione MALogAnalyticsReader

Quando si configura Desktop Analytics, l'utente concede il consenso per conto dell'organizzazione. Questo consenso consiste nell'assegnare all'applicazione MALogAnalyticsReader il ruolo di Lettore di Log Analytics per l'area di lavoro. Questo ruolo applicazione è richiesto da Desktop Analytics.

In caso di problemi con questo processo durante l'installazione, usare il processo seguente per aggiungere manualmente questa autorizzazione:

1. Andare al [portale di Azure](https://portal.azure.com) e selezionare **Tutte le risorse**. Selezionare l'area di lavoro di tipo **Log Analytics**.  

2. Nel menu dell'area di lavoro selezionare **Controllo di accesso (IAM)** e quindi **Aggiungi**.  

3. Nel pannello **Aggiungi autorizzazioni** configurare le impostazioni seguenti:  

    - **Ruolo**: **Lettore**  

    - **Assegna accesso a**: **Applicazione, gruppo o utente di Azure AD**  

    - **Seleziona**: **MALogAnalyticsReader**  

4. Selezionare **Salva**.

Nel portale viene visualizzata una notifica che informa che è stata aggiunta l'assegnazione di ruolo.

## <a name="data-latency"></a>Latenza dei dati

<!-- 3846531 -->
La prima volta che si configura Desktop Analytics, si registrano nuovi clienti o si configurano nuovi piani di distribuzione, è possibile che i report in Configuration Manager e il portale di Desktop Analytics non visualizzino immediatamente i dati completi. Possono essere necessari 2-3 giorni prima che:

- I dispositivi attivi inviino i dati di diagnostica al servizio Desktop Analytics
- Il servizio elabori i dati
- Il servizio venga sincronizzato con il sito di Configuration Manager

Quando si sincronizzano le raccolte di dispositivi dalla gerarchia di Configuration Manager a Desktop Analytics, potrebbe essere necessaria fino a un'ora prima che le raccolte vengano visualizzate nel portale di Desktop Analytics. Analogamente, quando si crea un piano di distribuzione in Desktop Analytics, può essere necessaria fino a un'ora prima che le nuove raccolte associate al piano di distribuzione vengano visualizzate nella gerarchia di Configuration Manager. I siti primari creano le raccolte e il sito di amministrazione centrale si sincronizza con Desktop Analytics. Configuration Manager può richiedere fino a 24 ore per valutare e aggiornare l'appartenenza alla raccolta. Per velocizzare questo processo, aggiornare manualmente l'appartenenza alla raccolta.<!-- 4984639 -->

> [!Note]
> Per fare in modo che gli aggiornamenti manuali della raccolta rispecchino le modifiche, è necessario prima sincronizzare il componente SMS_SERVICE_CONNECTOR_M365ADeploymentPlanWorker. L'esecuzione di questo processo può richiedere fino a un'ora. Per altre informazioni, vedere **M365ADeploymentPlanWorker.log**.

Nel portale di Desktop Analytics sono disponibili due tipi di dati: **dati dell'amministratore** e **dati di diagnostica**:

- I **dati dell'amministratore** si riferiscono alle modifiche apportate alla configurazione dell'area di lavoro. Ad esempio, quando si modifica la **Decisione di aggiornamento** o l'**Importanza** di una risorsa si stanno cambiando i dati dell'amministratore. Queste modifiche hanno spesso un effetto di associazione, poiché possono modificare lo stato di conformità di un dispositivo con la risorsa in questione installata.

- I **dati di diagnostica** fanno riferimento ai metadati di sistema caricati da dispositivi client in Microsoft. Questi dati vengono inviati a Desktop Analytics. Sono inclusi attributi come l'inventario dei dispositivi e lo stato di sicurezza e aggiornamento delle funzionalità.

Per impostazione predefinita, tutti i dati nel portale di Desktop Analytics vengono aggiornati automaticamente ogni giorno. Questo aggiornamento include le modifiche ai dati di diagnostica per i due giorni precedenti e le eventuali modifiche apportate alla configurazione (dati dell'amministratore). Dovrebbe essere visibile nel portale di Desktop Analytics entro le 08:00 UTC ogni giorno.

Quando si apportano modifiche ai dati dell'amministratore, è possibile attivare un aggiornamento su richiesta dei dati dell'amministratore nell'area di lavoro. Da qualsiasi pagina nel portale di Desktop Analytics, aprire il riquadro a comparsa sull'attualità dei dati:

![Screenshot della scheda del riquadro a comparsa sull'attualità dei dati nel portale di Desktop Analytics](media/data-currency-flyout.png)

Selezionare quindi **Applica modifiche**:

![Screenshot del riquadro a comparsa sull'attualità dei dati esteso nel portale di Desktop Analytics](media/data-currency-flyout-expand.png)

Questo processo richiede in genere da 15 a 60 minuti. I tempi dipendono dalle dimensioni dell'area di lavoro e dall'ambito delle modifiche da elaborare. Quando si richiede un aggiornamento dati su richiesta, non vengono apportate modifiche ai dati di diagnostica.  Per altre informazioni, vedere [Domande frequenti su Desktop Analytics](faq.md#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).

Se non vengono visualizzate modifiche aggiornate entro gli intervalli di tempo indicati in precedenza, attendere altre 24 ore per l'aggiornamento giornaliero successivo. Se vengono visualizzati tempi più lunghi, controllare il dashboard di integrità dei servizi. Se il servizio viene segnalato come integro, contattare il supporto tecnico Microsoft.<!-- 3896921 -->

> [!IMPORTANT]
> L'opzione di Desktop Analytics **Visualizza dati recenti** è deprecata. Questa azione verrà rimossa in una versione futura del servizio Desktop Analytics. Per altre informazioni, vedere [Funzionalità deprecate](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).<!--7080949-->  

## <a name="service-notifications"></a>Notifiche del servizio

<!-- 4982509 -->

Il portale di Desktop Analytics può visualizzare banner di notifica agli amministratori. Queste notifiche consentono a Microsoft di comunicare con l'utente in merito a eventi e problemi importanti. Le sezioni seguenti illustrano in dettaglio le notifiche che è possibile visualizzare.

### <a name="see-whats-new-this-month-in-desktop-analytics"></a>Le novità di questo mese sono disponibili in Desktop Analytics

Questa notifica informativa segnala modifiche apportate al servizio. Per altre informazioni, vedere [Novità di Desktop Analytics](whats-new.md) (`https://aka.ms/danews`).

### <a name="there-are-new-prerequisites-to-continue-using-desktop-analytics-review-the-new-requirements"></a>Sono presenti nuovi prerequisiti. Per continuare a usare Desktop Analytics, esaminare i nuovi requisiti.

Questa notifica informativa segnala modifiche apportate ai prerequisiti. Ad esempio, un nuovo endpoint Internet o un aggiornamento software. Per altre informazioni, vedere [Prerequisiti](overview.md#prerequisites) (`https://aka.ms/daprereqs`).

### <a name="were-investigating-an-issue-that-impacts-desktop-analytics"></a>È in corso la ricerca della causa di un problema relativo a Desktop Analytics

Questa notifica di avviso indica che Microsoft è a conoscenza di un problema con impatto sul servizio Desktop Analytics. Il problema si verifica di solito con la generazione di snapshot. Quando viene visualizzata questa notifica, significa che Microsoft sta esaminando il problema per determinare l'ambito e l'origine dell'effetto. Non è necessario contattare il supporto tecnico Microsoft. Per altre informazioni, vedere [Flusso di dati](privacy.md#data-flow).

### <a name="were-investigating-an-issue-with-data-latency-if-you-enrolled-new-devices-or-changed-any-assets-in-the-last-24-hours-they-may-not-appear-right-away"></a>È in corso la ricerca della causa di un problema relativo alla latenza dei dati. Se sono stati registrati nuovi dispositivi o sono stati modificati asset nelle ultime 24 ore, è possibile che non vengano visualizzati immediatamente.

Questa notifica di avviso indica che Microsoft è a conoscenza di un problema con impatto sul servizio Desktop Analytics. Microsoft monitora costantemente il servizio per verificare che tutti i componenti aggiornino gli snapshot nei tempi corretti. Durante questo monitoraggio, uno di questi componenti non è stato completato come previsto. Quando viene visualizzata questa notifica, significa che Microsoft sta indagando sul problema. Non è necessario contattare il supporto tecnico Microsoft. Per altre informazioni, vedere [Flusso di dati](privacy.md#data-flow).

Se di recente [sono stati registrati dispositivi](enroll-devices.md) o sono stati modificati [asset](about-assets.md), attendere che Microsoft risolva il problema. Non è necessario ripetere alcuna azione.

### <a name="weve-resolved-a-temporary-issue-with-data-latency-daily-refresh-of-portal-data-is-delayed"></a>È stato risolto un problema temporaneo relativo alla latenza dei dati. L'aggiornamento giornaliero dei dati del portale è ritardato.

Questa notifica informa che si è verificato un problema con la latenza dei dati. Il servizio sta ancora elaborando lo snapshot e l'aggiornamento dei dati è ritardato. Per altre informazioni, vedere [Latenza dei dati](#data-latency).

### <a name="weve-resolved-an-issue-with-data-latency-if-you-enrolled-new-devices-or-changed-any-assets-in-the-last-24-hours-they-may-not-appear-right-away"></a>È stato risolto un problema relativo alla latenza dei dati. Se sono stati registrati nuovi dispositivi o sono stati modificati asset nelle ultime 24 ore, è possibile che non vengano visualizzati immediatamente.

Questa notifica informa che Microsoft ha risolto un problema segnalato in precedenza relativo alla latenza dei dati. È possibile che vengano visualizzati dati non aggiornati per lo snapshot del giorno successivo. Se [sono stati registrati dispositivi](enroll-devices.md) o sono state apportate modifiche alla configurazione del dispositivo nelle ultime 24 ore, questi cambiamenti non verranno visualizzati immediatamente nel portale. È possibile continuare a usare Desktop Analytics per categorizzare gli [asset](about-assets.md) e preparare [piani di distribuzione](about-deployment-plans.md). Queste azioni possono usare i dati dello snapshot precedente.

### <a name="weve-resolved-an-issue-with-desktop-analytics-daily-refresh-of-the-portal-data-is-on-track"></a>È stato risolto un problema relativo a Desktop Analytics. L'aggiornamento giornaliero dei dati del portale è puntuale.

Questa notifica informa che Microsoft ha identificato un componente dello snapshot che ha smesso di funzionare durante l'elaborazione. Microsoft ha riavviato il componente, operazione che richiede tempo per l'elaborazione dello snapshot. Microsoft monitora costantemente il servizio per verificare che tutti i componenti aggiornino gli snapshot nei tempi corretti.
