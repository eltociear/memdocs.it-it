---
title: Configurare i servizi di Azure
titleSuffix: Configuration Manager
description: Connettere l'ambiente di Configuration Manager con i servizi di Azure per la gestione del cloud, Microsoft Store per le aziende e Log Analytics.
ms.date: 06/10/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a26a653e-17aa-43eb-ab36-0e36c7d29f49
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 6ca5307de5c7df54c3cf7924bc91b0175b1bfa39
ms.sourcegitcommit: 2f1963ae208568effeb3a82995ebded7b410b3d4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/11/2020
ms.locfileid: "84715323"
---
# <a name="configure-azure-services-for-use-with-configuration-manager"></a>Configurare i servizi di Azure da usare con Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Usare la **Procedura guidata per i servizi di Azure** per semplificare il processo di configurazione dei servizi di Azure usati con Configuration Manager. Questa procedura guidata offre un'esperienza di configurazione comune usando le registrazioni di app Web di Azure Active Directory (Azure AD). Queste app specificano dettagli di sottoscrizione e configurazione e autenticano le comunicazioni con Azure AD. L'app evita di dover immettere le stesse informazioni ogni volta che si configura un nuovo componente o servizio di Configuration Manager con Azure.

## <a name="available-services"></a>Servizi disponibili

Configurare i seguenti servizi di Azure tramite questa procedura guidata:  

- **Gestione cloud**: questo servizio consente al sito e ai client di eseguire l'autenticazione usando Azure AD. Questa autenticazione abilita altri scenari, ad esempio:  

  - [Installare e assegnare client di Configuration Manager in dispositivi Windows 10 usando Azure AD per l'autenticazione](../../../clients/deploy/deploy-clients-cmg-azure.md)  

  - [Configurare l'individuazione utente di Azure AD](configure-discovery-methods.md#azureaadisc)  

  - [Configurare l'individuazione dei gruppi utenti di Azure AD](configure-discovery-methods.md#bkmk_azuregroupdisco)

  - Supporto di alcuni [scenari di Cloud Management Gateway](../../../clients/manage/cmg/plan-cloud-management-gateway.md#scenarios)  

  - [Notifiche tramite posta elettronica di approvazione delle app](../../../../apps/deploy-use/app-approval.md#bkmk_email-approve)

- **Connettore Log Analytics**: [Connettersi ad Azure Log Analytics](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm). Sincronizza i dati della raccolta a Log Analytics.  

    > [!Note]  
    > Questo articolo si riferisce al *connettore Log Analytics*, che era in precedenza denominato *OMS Connector*. Non esistono differenze funzionali. Per altre informazioni, vedere [Gestione di Azure - Monitoraggio](https://docs.microsoft.com/azure/azure-monitor/terminology#log-analytics).  

- **Microsoft Store per le aziende**: connettersi a [Microsoft Store per le aziende](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md). Consente di ottenere da Microsoft Store le app distribuibili con Configuration Manager.  

### <a name="service-details"></a>Dettagli dei servizi

La tabella seguente elenca informazioni dettagliate sui singoli servizi.  

- **Tenant**: numero di istanze del servizio che è possibile configurare. Ogni istanza deve essere un tenant di Azure AD distinto.  

- **Cloud**: tutti i servizi supportano il cloud globale di Azure, ma non tutti i servizi supportano i cloud privati, ad esempio il cloud Azure Governo degli Stati Uniti.  

- **App Web**: indica se il servizio usa un'app Azure AD di tipo *App Web/API*, detta anche app server in Configuration Manager.  

- **App nativa**: indica se il servizio usa un'app Azure AD di tipo *Nativo*, detta anche app client in Configuration Manager.  

- **Azioni**: indica se è possibile importare o creare queste app nella procedura guidata per i servizi di Azure di Configuration Manager.  

|Servizio  |Tenant  |Cloud  |App Web  |App nativa  |Azioni  |
|---------|---------|---------|---------|---------|---------|
|Gestione cloud con<br>individuazione di Azure AD | Più elementi | Pubblico, Privato | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | Importa, Crea |
|Connettore Log Analytics | Uno | Pubblico, Privato | ![Supportato](media/green_check.png) | ![Non supportato](media/Red_X.png) | Importa |
|Microsoft Store per<br>Business | Uno | Pubblico | ![Supportato](media/green_check.png) | ![Non supportato](media/Red_X.png) | Importa, Crea |

### <a name="about-azure-ad-apps"></a>Informazioni sulle app di Azure AD

I diversi servizi di Azure richiedono configurazioni distinte, implementabili nel portale di Azure. Le app di ogni servizio possono richiedere autorizzazioni di accesso specifiche alle risorse di Azure.  

È possibile usare una singola app per più servizi. In Configuration Manager e Azure AD è presente un solo oggetto da gestire. Quando la chiave di sicurezza dell'app scade, è sufficiente aggiornare una sola chiave.

Quando si creano servizi di Azure aggiuntivi nella procedura guidata, Configuration Manager è progettato per riutilizzare le informazioni comuni tra i servizi. Questo comportamento evita di dover specificare le stesse informazioni più volte.

Per altre informazioni sulle autorizzazioni delle app necessarie e sulle configurazioni per ogni servizio, vedere l'articolo di Configuration Manager corrispondente in [Servizi disponibili](#available-services).

Per altre informazioni sulle app di Azure, vedere gli articoli seguenti:

- [Autenticazione e autorizzazione nel servizio app di Azure](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview)
- [Panoramica di App Web](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview)
- [Basics of Registering an Application in Azure AD](/azure/active-directory/develop/authentication-scenarios) (Nozioni di base per la registrazione di un'applicazione in Azure AD)  
- [Registrare l'applicazione nel tenant di Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration)

## <a name="before-you-begin"></a>Prima di iniziare

Dopo aver scelto il servizio al quale connettersi, fare riferimento alla tabella in [Dettagli servizio](#service-details). Questa tabella specifica informazioni necessarie per completare la procedura guidata del servizio di Azure. In primo luogo valutare le alternative con l'amministratore di Azure AD. Decidere quali delle azioni seguenti eseguire:

- Creare manualmente le app in anticipo nel portale di Azure. Quindi importare i dettagli delle app in Configuration Manager.  

- Usare Configuration Manager per creare le app direttamente in Azure AD. Per raccogliere i dati necessari da Azure AD, esaminare le informazioni delle altre sezioni di questo articolo.  

Alcuni servizi richiedono che le app di Azure AD dispongano di autorizzazioni specifiche. Esaminare le informazioni per ogni servizio per determinare le autorizzazioni necessarie. Ad esempio, prima di poter importare un'app Web è necessario che un amministratore di Azure crei l'app nel [portale di Azure](https://portal.azure.com).

Quando si configura il connettore Log Analytics, concedere alla nuova app Web registrata l'autorizzazione *Collaboratore* per il gruppo di risorse che contiene l'area di lavoro appropriata. Questa autorizzazione consente a Configuration Manager di accedere all'area di lavoro. Durante l'assegnazione dell'autorizzazione cercare il nome della registrazione dell'app nell'area **Aggiungi utenti** del portale di Azure. Questo processo è analogo a quello che [aggiunge a Configuration Manager le autorizzazioni per Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#grant-configuration-manager-with-permissions-to-log-analytics). Queste autorizzazioni devono essere assegnate da un amministratore prima dell'importazione dell'app in Configuration Manager.

## <a name="start-the-azure-services-wizard"></a>Avviare la procedura guidata per i servizi di Azure

1. Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Servizi cloud** e selezionare il nodo **Servizi di Azure**.  

2. Nella scheda **Home** della barra multifunzione nel gruppo **Servizi di Azure** selezionare **Configura i servizi di Azure**.  

3. Nella pagina **Servizi di Azure** della procedura guidata per i servizi di Azure:  

    1. Specificare un **Nome** per l'oggetto in Configuration Manager.  

    2. Specificare un parametro facoltativo **Descrizione** per identificare il servizio.  

    3. Selezionare il servizio di Azure che si vuole connettere con Configuration Manager.  

4. Selezionare **Avanti** per passare alla pagina [Proprietà dell'app](#azure-app-properties) della procedura guidata per i servizi di Azure.  

## <a name="azure-app-properties"></a>Proprietà dell'app di Azure

Nella pagina **App** della procedura guidata per i servizi di Azure selezionare l'**ambiente Azure** dall'elenco. Per informazioni sull'ambiente attualmente disponibile per il servizio, vedere la tabella [Dettagli servizio](#service-details).

Il resto della pagina App varia in base al servizio specifico. Per informazioni sul tipo di app usata dal servizio e sull'azione che è possibile usare, vedere la tabella in [Dettagli servizio](#service-details).

- Se l'app supporta sia l'azione di importazione che quella di creazione, selezionare **Sfoglia**. Viene visualizzata la [finestra di dialogo App server](#server-app-dialog) o la [finestra di dialogo App client](#client-app-dialog).  

- Se l'app supporta solo l'azione di importazione, selezionare **Importa**. Viene visualizzata la [finestra di dialogo Importa le app (server)](#import-apps-dialog-server) o la finestra di dialogo [Importa le app (client)](#import-apps-dialog-client).

Dopo aver specificato le app in questa pagina, selezionare **Avanti** per aprire la pagina [Configurazione o Individuazione](#configuration-or-discovery) della procedura guidata per i servizi di Azure.

### <a name="web-app"></a>App Web

Questa app Azure AD di tipo *App Web/API* è detta anche app server in Configuration Manager.

#### <a name="server-app-dialog"></a>Finestra di dialogo App server

Quando si seleziona **Sfoglia** per **App Web** nella pagina App della procedura guidata per i servizi di Azure, viene visualizzata la finestra di dialogo App server. La finestra visualizza un elenco con le proprietà seguenti per le app web esistenti:

- Nome descrittivo del tenant
- Nome descrittivo dell'app
- Tipo di servizio

Nella finestra di dialogo App server è possibile eseguire tre operazioni:

- Per riusare un'app Web esistente, selezionarla nell'elenco.
- Selezionare **Importa** per aprire la [finestra di dialogo Importa le app](#import-apps-dialog-server).
- Selezionare **Crea** per aprire la [finestra di dialogo Crea un'applicazione server](#create-server-application-dialog).

Dopo aver selezionato, importato o creato un'app Web, selezionare **OK** per chiudere la finestra di dialogo App server. Questa azione torna a visualizzare la [pagina App](#azure-app-properties) della procedura guidata per i servizi di Azure.

#### <a name="import-apps-dialog-server"></a>Finestra di dialogo Importa le app (server)

Quando si seleziona **Importa** nella finestra di dialogo App server o nella pagina App della procedura guidata per i servizi di Azure, viene visualizzata la finestra di dialogo Importa le app. Questa pagina consente di immettere informazioni su un'app Web di Azure AD che è già stata creata nel portale di Azure. Consente anche di importare i metadati relativi a questa app Web in Configuration Manager. Specificare le informazioni seguenti:

- **Nome del tenant di Azure AD**: nome del tenant di Azure AD.
- **ID tenant di Azure AD**: GUID del tenant di Azure AD.
- **Nome applicazione**: nome descrittivo per l'app, il nome visualizzato nella registrazione app.
- **Client ID** (ID client): il valore **ID applicazione (client)** della registrazione app. Il formato è un GUID standard.
- **Chiave privata**: copiare la chiave privata quando si registra l'app in Azure AD.
- **Scadenza della chiave privata**: selezionare una data futura nel calendario.
- **URI ID app**: questo valore deve essere univoco nel tenant di Azure AD. È incluso nel token di accesso usato dal client Configuration Manager per richiedere l'accesso al servizio. Il valore è l'**URI ID applicazione** della voce di registrazione app nel portale di Azure AD. Il formato è simile a `https://ConfigMgrService`.

Dopo aver immesso le informazioni, selezionare **Verifica**. Quindi selezionare **OK** per chiudere la finestra di dialogo Importa le app. Questa azione torna a visualizzare la [pagina App](#azure-app-properties) della procedura guidata per i servizi di Azure o la [finestra di dialogo App server](#server-app-dialog).

> [!TIP]
> Quando si registra l'app in Azure AD, potrebbe essere necessario specificare manualmente l'**URI di reindirizzamento** seguente: `ms-appx-web://Microsoft.AAD.BrokerPlugin/<ClientID>`. Specificare il GUID dell'ID client dell'app, ad esempio `ms-appx-web://Microsoft.AAD.BrokerPlugin/a26a653e-17aa-43eb-ab36-0e36c7d29f49`.<!-- SCCMDocs#1135 -->

#### <a name="create-server-application-dialog"></a>Finestra di dialogo Crea un'applicazione server

Quando si seleziona **Crea** nella finestra di dialogo App server viene visualizzata la finestra di dialogo Crea un'applicazione server. Questa pagina automatizza la creazione di un'app Web in Azure AD. Specificare le informazioni seguenti:

- **Nome applicazione**: nome descrittivo per l'app.
- **URL della home page**: questo valore non viene usato da Configuration Manager, ma è richiesto da Azure AD. Per impostazione predefinita, questo valore è impostato su `https://ConfigMgrService`.  
- **URI ID app**: questo valore deve essere univoco nel tenant di Azure AD. È incluso nel token di accesso usato dal client Configuration Manager per richiedere l'accesso al servizio. Per impostazione predefinita, questo valore è impostato su `https://ConfigMgrService`.  
- **Periodo di validità della chiave privata**: scegliere **1 anno** o **2 anni** dall'elenco a discesa. Il valore predefinito è 1 anno.

Selezionare **Accedi** per eseguire l'autenticazione in Azure come utente amministratore. Queste credenziali non vengono memorizzate in Configuration Manager. Questo utente tipo non richiede autorizzazioni in Configuration Manager e non deve necessariamente essere lo stesso account che esegue la procedura guidata per i servizi di Azure. Dopo l'autenticazione in Azure, nella pagina viene visualizzato il **Nome del tenant di Azure AD** come riferimento.

Selezionare **OK** per creare l'app Web in Azure AD e chiudere la finestra di dialogo Crea un'applicazione server. Questa azione torna a visualizzare la [finestra di dialogo App server](#server-app-dialog).

> [!NOTE]
> Se sono stati definiti criteri di accesso condizionale di Azure AD applicabili a **tutte le app cloud**, è necessario escludere l'applicazione server creata da questi criteri. Per altre informazioni su come escludere app specifiche, vedere la [documentazione sull'accesso condizionale di Azure AD](https://docs.microsoft.com/azure/active-directory/conditional-access/).

### <a name="native-client-app"></a>App client nativa

Questa app Azure AD di tipo *Nativo* è detta anche app client in Configuration Manager.

#### <a name="client-app-dialog"></a>Finestra di dialogo App client

Quando si seleziona **Sfoglia** per **App client nativa** nella pagina App della procedura guidata per i servizi di Azure, viene visualizzata la finestra di dialogo App client. La finestra visualizza un elenco con le proprietà seguenti per le app native esistenti:

- Nome descrittivo del tenant
- Nome descrittivo dell'app
- Tipo di servizio

Nella finestra di dialogo App client è possibile eseguire tre operazioni:

- Per riusare un'app nativa esistente, selezionarla nell'elenco. 
- Selezionare **Importa** per aprire la [finestra di dialogo Importa le app](#import-apps-dialog-client).
- Selezionare **Crea** per aprire la [finestra di dialogo Crea un'applicazione client](#create-client-application-dialog).

Dopo aver selezionato, importato o creato un'app nativa, scegliere **OK** per chiudere la finestra di dialogo App client. Questa azione torna a visualizzare la [pagina App](#azure-app-properties) della procedura guidata per i servizi di Azure.

#### <a name="import-apps-dialog-client"></a>Finestra di dialogo Importa le app (client)

Quando si seleziona **Importa** nella finestra di dialogo App client viene visualizzata la finestra di dialogo Importa le app. Questa pagina consente di immettere informazioni su un'app nativa di Azure AD che è già stata creata nel portale di Azure. Consente anche di importare i metadati relativi all'app nativa in Configuration Manager. Specificare le informazioni seguenti:

- **Nome applicazione**: nome descrittivo per l'app.
- **Client ID** (ID client): il valore **ID applicazione (client)** della registrazione app. Il formato è un GUID standard.

Dopo aver immesso le informazioni, selezionare **Verifica**. Quindi selezionare **OK** per chiudere la finestra di dialogo Importa le app. Questa azione torna a visualizzare la [finestra di dialogo App client](#client-app-dialog).

#### <a name="create-client-application-dialog"></a>Finestra di dialogo Crea un'applicazione client

Quando si seleziona **Crea** nella finestra di dialogo App client viene visualizzata la finestra di dialogo Crea un'applicazione client. Questa pagina automatizza la creazione di un'app nativa in Azure AD. Specificare le informazioni seguenti:

- **Nome applicazione**: nome descrittivo per l'app.
- **URL di risposta**: questo valore non viene usato da Configuration Manager, ma è richiesto da Azure AD. Per impostazione predefinita, questo valore è impostato su `https://ConfigMgrService`.

Selezionare **Accedi** per eseguire l'autenticazione in Azure come utente amministratore. Queste credenziali non vengono memorizzate in Configuration Manager. Questo utente tipo non richiede autorizzazioni in Configuration Manager e non deve necessariamente essere lo stesso account che esegue la procedura guidata per i servizi di Azure. Dopo l'autenticazione in Azure, nella pagina viene visualizzato il **Nome del tenant di Azure AD** come riferimento.

Selezionare **OK** per creare l'app nativa in Azure AD e chiudere la finestra di dialogo Crea un'applicazione client. Questa azione torna a visualizzare la [finestra di dialogo App client](#client-app-dialog).

## <a name="configuration-or-discovery"></a>Configurazione o Individuazione

Dopo aver specificato l'app Web e l'app nativa nella pagina App, la procedura guidata per i servizi di Azure visualizza una pagina **Configurazione** o una pagina **Individuazione**, a seconda del servizio a cui ci si connette. I dettagli di questa pagina variano a seconda del servizio. Per altre informazioni, vedere uno degli articoli seguenti:  

- Servizio **Gestione cloud**, pagina **Individuazione**: [Configurare l'individuazione utente di Azure AD](configure-discovery-methods.md#azureaadisc)  

- Servizio **Connettore Log Analytics**, pagina **Configurazione**: [Configurare la connessione a Log Analytics](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm)  

- Servizio **Microsoft Store per le aziende**, pagina **Configurazioni**: [Configurare la sincronizzazione di Microsoft Store per le aziende](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md#bkmk_config)  

Infine completare la procedura guidata per i servizi di Azure con le pagine Riepilogo, Stato e Completamento. La configurazione di un servizio di Azure in Configuration Manager è completata. Ripetere questo processo per configurare altri servizi di Azure.

## <a name="renew-secret-key"></a><a name="bkmk_renew"></a> Rinnovare la chiave privata

### <a name="renew-key-for-created-app"></a>Rinnovare la chiave per un'app creata

1. Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Servizi cloud** e selezionare il nodo **Tenant di Azure Active Directory**.

1. Nel riquadro Dettagli selezionare il tenant di Azure AD per l'app.

1. Nella barra multifunzione selezionare **Rinnova la chiave privata**. Immettere le credenziali del proprietario dell'app o di un amministratore di Azure AD.

### <a name="renew-key-for-imported-app"></a>Rinnovare la chiave per un'app importata

Se l'app Azure è stata importata in Configuration Manager, usare il portale di Azure per il rinnovo. Prendere nota della nuova chiave privata e della data di scadenza. Aggiungere queste informazioni nella procedura guidata **Rinnova la chiave privata**.  

> [!NOTE]
> Salvare la chiave privata prima di chiudere la pagina **Chiave** delle proprietà dell'applicazione di Azure. Queste informazioni vengono rimosse quando si chiude la pagina.

## <a name="view-the-configuration-of-an-azure-service"></a>Visualizzare la configurazione di un servizio di Azure

È possibile visualizzare le proprietà di un servizio di Azure configurato per l'uso. Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Servizi cloud** e selezionare **Servizi di Azure**. Selezionare il servizio che si vuole visualizzare o modificare e selezionare **Proprietà**.

Se si seleziona un servizio e quindi si sceglie **Elimina** nella barra multifunzione, viene eliminata la connessione in Configuration Manager. L'app in Azure AD non viene eliminata. Chiedere all'amministratore di Azure di eliminare l'app quando non è più necessaria. In alternativa eseguire la procedura guidata per i servizi di Azure per importare l'app.<!--483440-->

## <a name="cloud-management-data-flow"></a>Flusso di dati per la gestione cloud

Il diagramma seguente è un flusso di dati concettuale per l'interazione tra Configuration Manager, Azure AD e i servizi cloud connessi. Questo esempio specifico usa il servizio **Gestione cloud**, che include un client Windows 10 e app sia server che client. I flussi per altri servizi sono simili.

![Diagramma di flusso di dati per Configuration Manager con Azure AD e gestione cloud](media/aad-auth.png)

1. L'amministratore di Configuration Manager importa o crea le app client e server in Azure AD.  

2. Viene eseguito il metodo di individuazione utenti di Azure AD Configuration Manager. Il sito usa il token dell'app server di Azure AD per il rilevamento di oggetti utente in Microsoft Graph.  

3. Il sito archivia dati sugli oggetti utente. Per altre informazioni, vedere [Individuazione utente Azure AD](about-discovery-methods.md#azureaddisc).  

4. Il client Configuration Manager richiede il token utente di Azure AD. Il client esegue l'attestazione mediante l'ID applicazione dell'app client di Azure AD, con l'app server come gruppo di destinatari. Per altre informazioni, vedere [Claims in Azure AD Security Tokens](/azure/active-directory/develop/authentication-scenarios#security-tokens) (Attestazioni nei token di sicurezza di Azure AD).  

5. Il client esegue l'autenticazione nel sito presentando il token di Azure AD al gateway di gestione cloud e al punto di gestione locale abilitato per HTTPS.  

Per informazioni più dettagliate, vedere [Flusso di lavoro di autenticazione di Azure AD](../../../clients/manage/azure-ccmsetup.md).
