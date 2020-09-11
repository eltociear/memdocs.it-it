---
title: Approvare le applicazioni
titleSuffix: Configuration Manager
description: Informazioni sulle impostazioni e i comportamenti per l'approvazione delle applicazioni in Configuration Manager.
ms.date: 05/04/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 20493c86-6454-4b35-8f22-0d049b68b8bb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 659dd91c4b6bbeba6e2e93d3318683a4006aa5ff
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/09/2020
ms.locfileid: "89606588"
---
# <a name="approve-applications-in-configuration-manager"></a>Approvare le applicazioni in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Quando si [distribuiscono applicazioni](deploy-applications.md) in Configuration Manager, è possibile richiedere l'approvazione prima dell'installazione. Gli utenti richiedono l'applicazione in Software Center e quindi la richiesta viene esaminata nella console di Configuration Manager. La richiesta può essere approvata o rifiutata.

## <a name="approval-settings"></a><a name="bkmk_approval"></a> Impostazioni di approvazione

Il comportamento di approvazione delle applicazioni dipende dall'abilitazione o meno dell'[esperienza di approvazione di app facoltativa](#bkmk_opt) consigliata. Nella pagina **Impostazioni di distribuzione** dell'applicazione di distribuzione viene visualizzata una delle seguenti impostazioni di approvazione:  

### <a name="an-administrator-must-approve-a-request-for-this-application-on-the-device"></a><a name="bkmk_opt"></a> Un amministratore deve approvare una richiesta per questa applicazione nel dispositivo

> [!Note]  
> Configuration Manager non abilita questa funzionalità per impostazione predefinita. Prima di usarlo, abilitare la funzionalità facoltativa **Approva le richieste dell'applicazione per gli utenti per ogni dispositivo**. Per altre informazioni, vedere [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options) (Abilitare le funzioni facoltative dagli aggiornamenti).
>
> Se non si abilita questa funzionalità, viene visualizzata l'[esperienza precedente](#bkmk_prior).  

L'amministratore deve approvare qualsiasi richiesta utente per l'applicazione prima che l'utente possa installarla nel dispositivo desiderato. Se l'amministratore approva la richiesta, l'utente può installare l'applicazione solo su quel dispositivo. Per installare l'applicazione in un altro dispositivo dovrà inviare un'altra richiesta. Questa opzione è disattivata quando lo scopo della distribuzione è **Richiesto** o quando si distribuisce l'applicazione un una raccolta di dispositivi. <!--1357015-->  

> [!Note]  
> Per sfruttare i vantaggi delle nuove funzionalità di Configuration Manager, aggiornare prima di tutto i clienti alla versione più recente. Anche se le nuove funzionalità vengono visualizzate nella console di Configuration Manager quando si esegue l'aggiornamento del sito e della console, lo scenario completo risulta funzionante solo dopo l'aggiornamento alla versione più recente del client.<!--SCCMDocs issue 646-->  

Visualizzare **Richieste di applicazioni** in **Gestione applicazioni** nell'area di lavoro **Raccolta software** della console di Configuration Manager. Nella versione 1902 e nelle versioni precedenti questo nodo viene chiamato **Richieste di approvazione**. Nell'elenco è ora presente una colonna **Dispositivo** per ogni richiesta. Quando si intraprende un'azione sulla richiesta, la finestra di dialogo Richiesta di applicazioni include anche il nome del dispositivo da cui l'utente ha inviato la richiesta.

Se una richiesta non viene approvata entro 30 giorni, viene rimossa. La reinstallazione del client potrebbe annullare eventuali richieste di approvazione in sospeso.  

Quando si richiede l'approvazione per una distribuzione in una raccolta di dispositivi, l'app non viene visualizzata in Software Center. Se si richiede l'approvazione per una distribuzione in una raccolta di utenti, l'app viene visualizzata in Software Center. È comunque possibile nasconderlo dagli utenti con l'impostazione client **Nascondi le applicazioni non approvate nel Software Center**. Per altre informazioni, vedere [Impostazioni client di Software Center](../../core/clients/deploy/about-client-settings.md#software-center).

Dopo avere approvato un'applicazione per l'installazione, è possibile scegliere di negare la richiesta facendo clic su **Nega** nella console di Configuration Manager. Se gli utenti non hanno ancora installato l'applicazione, questa azione impedisce loro l'installazione di nuove copie dell'applicazione da Software Center. Se in precedenza è già stata approvata e installata un'applicazione, quando si imposta **Nega** nella richiesta per l'applicazione il client disinstalla l'applicazione dal dispositivo dell'utente.<!--1357891-->

A partire dalla versione 1906, se si approva una richiesta di app nella console e poi la si rifiuta, è ora possibile approvarla nuovamente. L'app viene reinstallata nel client dopo l'approvazione.  <!-- 4224910 -->

Automatizzare il processo di approvazione con il cmdlet di PowerShell [Approve-CMApprovalRequest](/powershell/module/configurationmanager/approve-cmapprovalrequest). A partire dalla versione 1902 questo cmdlet include il parametro **InstallActionBehavior**. Usare questo parametro per specificare se installare l'applicazione immediatamente o fuori dall'orario di ufficio.<!-- SCCMDocs-pr issue #3418 -->

A partire dalla versione 1906, è possibile visualizzare le distribuzioni che richiedono l'approvazione. Selezionare un'app nel nodo **Applicazioni**. Nel riquadro dei dettagli passare alla scheda **Distribuzioni**. Per impostazione predefinita viene visualizzata una nuova colonna **Richiede approvazione**.

#### <a name="retry-the-install-of-pre-approved-applications"></a><a name="bkmk_retry"></a> Ripetere l'installazione delle applicazioni pre-approvate

<!--4336307-->
A partire dalla versione 1906, è possibile ritentare l'installazione di un'app precedentemente approvata per un utente o un dispositivo. L'opzione di approvazione è destinata solo alle distribuzioni disponibili. Se l'utente disinstalla l'app o se il processo di installazione iniziale non riesce, Configuration Manager non rivaluta lo stato dell'app e la reinstalla. Questa funzionalità consente a un tecnico del supporto di ritentare rapidamente l'installazione dell'app per un utente che richiede assistenza.

1. Aprire la console di Configuration Manager come utente che dispone dell'autorizzazione **Approva** per l'oggetto applicazione. Ad esempio, i ruoli predefiniti **Amministratore applicazione** e **Autore applicazione** hanno questa autorizzazione.

1. Distribuire un'app che richiede l'approvazione e approvarla.

    > [!Tip]  
    > In alternativa, [installare un'applicazione per un dispositivo](install-app-for-device.md). Crea una richiesta approvata per l'app nel dispositivo.  

Se l'applicazione non viene installata correttamente oppure l'utente disinstalla l'app, usare la procedura seguente per riprovare:

1. Nella console di Configuration Manager passare all'area di lavoro **Raccolta software**, espandere **Gestione applicazioni** e selezionare il nodo **Richieste di applicazioni**. Nella versione 1902 e nelle versioni precedenti questo nodo viene chiamato **Richieste di approvazione**.

1. Selezionare l'app approvata in precedenza. Nel gruppo Richiesta di approvazione della barra multifunzione selezionare **Riprova l'installazione**.

#### <a name="other-app-approval-resources"></a>Altre risorse di approvazione di app

- [Miglioramenti dell'approvazione applicazione in ConfigMgr 1810](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/Application-approval-improvements-in-ConfigMgr-1810/ba-p/303534)
- [Aggiornamenti al processo di approvazione applicazione in Configuration Manager](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/Updates-to-the-application-approval-process-in-Configuration/ba-p/275048)

### <a name="require-administrator-approval-if-users-request-this-application"></a><a name="bkmk_prior"></a> Richiedi l'approvazione dell'amministratore se gli utenti richiedono questa applicazione

> [!Note]  
> Questa esperienza è valida se non si abilita l'[esperienza di approvazione di app facoltativa](#bkmk_opt) consigliata.

L'amministratore deve approvare qualsiasi richiesta utente per l'applicazione prima che l'utente possa installarla. Questa opzione è disattivata quando lo scopo della distribuzione è **Richiesto** o quando si distribuisce l'applicazione un una raccolta di dispositivi.  

Le richieste di approvazione dell'applicazione vengono visualizzate nel nodo **Richieste di applicazioni** in **Gestione applicazioni** nell'area di lavoro **Raccolta software**. Nella versione 1902 e nelle versioni precedenti questo nodo viene chiamato **Richieste di approvazione**. Se una richiesta non viene approvata entro 30 giorni, viene rimossa. La reinstallazione del client potrebbe annullare eventuali richieste di approvazione in sospeso.  

Dopo avere approvato un'applicazione per l'installazione, è possibile scegliere di negare la richiesta facendo clic su **Nega** nella console di Configuration Manager. Questa azione non provoca la disinstallazione dell'applicazione dai dispositivi da parte del client. Impedisce agli utenti di installare nuove copie dell'applicazione da Software Center.  

## <a name="email-notifications"></a><a name="bkmk_email-approve"></a> Notifiche tramite posta elettronica

<!--1321550-->

È possibile configurare notifiche tramite posta elettronica per le richieste di approvazione dell'applicazione. Quando un utente richiede un'applicazione, si riceve un messaggio di posta elettronica. Fare clic sui collegamenti nel messaggio di posta elettronica per approvare o rifiutare la richiesta, senza che sia necessario usare la console di Configuration Manager.

È possibile definire gli indirizzi di posta elettronica degli utenti che possono approvare o rifiutare la richiesta durante la creazione di una nuova distribuzione per l'applicazione. Se è necessario modificare l'elenco degli indirizzi di posta elettronica in un secondo momento, passare all'area di lavoro **Monitoraggio**, espandere **Avvisi** e selezionare il nodo **Sottoscrizioni**. Selezionare **Proprietà** da una delle sottoscrizioni **Approva l'applicazione tramite posta elettronica** correlate alla distribuzione dell'applicazione.

Se sono presenti più avvisi, è possibile determinare a quale distribuzione si riferisce ognuno di questi. Aprire le proprietà dell'avviso e visualizzare l'elenco di **Avvisi selezionati** nella scheda Generale. La distribuzione viene abilitata come avviso per questa sottoscrizione.

Gli utenti possono aggiungere un commento alla richiesta da Software Center. Questo commento viene visualizzato nella richiesta dell'applicazione nella console di Configuration Manager. A partire dalla versione 1902 questo commento viene visualizzato anche nel messaggio di posta elettronica. Includere questo commento nel messaggio di posta elettronica consente ai responsabili dell'approvazione di decidere più facilmente se approvare o rifiutare la richiesta.<!--3594063-->

### <a name="prerequisites"></a>Prerequisiti

#### <a name="to-send-email-notifications-and-take-action-on-internal-network"></a>Per inviare notifiche tramite posta elettronica e intraprendere un'azione nella rete interna

Con questi prerequisiti, i destinatari ricevono una notifica della richiesta tramite posta elettronica. Se sono collegati alla rete interna, possono anche approvare o negare la richiesta direttamente dal messaggio di posta elettronica.

- Abilitare la [funzionalità facoltativa](../../core/servers/manage/install-in-console-updates.md#bkmk_options) **Approva le richieste dell'applicazione per gli utenti per ogni dispositivo**.  

- Configurare la [notifica tramite posta elettronica per gli avvisi](../../core/servers/manage/use-alerts-and-the-status-system.md#to-configure-email-notification-for-alerts).  

    > [!NOTE]
    > L'utente amministratore che distribuisce l'applicazione deve avere l'autorizzazione per creare un avviso e una sottoscrizione. Se l'utente non ha queste autorizzazioni, viene visualizzato un errore alla fine della **Distribuzione guidata del software**: "Non si dispone dei privilegi di protezione per eseguire questa operazione."<!-- 2810283 -->

- Consentire al provider SMS sul sito primario di usare un certificato.<!--SCCMDocs-pr issue 3135--> Usare una delle seguenti opzioni:  

  - (Consigliata) Abilitare [HTTP avanzato](../../core/plan-design/hierarchy/enhanced-http.md) per il sito primario.

    > [!Note]  
    > Quando il sito primario crea un certificato per il provider SMS, il certificato non verrà considerato attendibile dal Web browser nel client. In base alle impostazioni di sicurezza, quando si risponde a una richiesta dell'applicazione, potrebbe essere visualizzato un avviso di sicurezza.  

  - Associare manualmente un certificato basato su PKI alla porta 443 in IIS sul server che ospita il ruolo Provider SMS nel sito primario.

> [!NOTE]
> Se si hanno più siti primari figlio in una gerarchia, configurare questi prerequisiti per ogni sito primario in cui si vuole abilitare questa funzionalità. I collegamenti nella notifica tramite posta elettronica sono relativi al servizio di amministrazione nel sito primario.<!-- 7108472 -->

#### <a name="to-take-action-from-internet"></a>Intraprendere un'azione da Internet

Con questi prerequisiti aggiuntivi facoltativi, i destinatari possono approvare o rifiutare la richiesta ovunque sia disponibile l'accesso a Internet.

- Abilitare il servizio di amministrazione del Provider SMS tramite Cloud Management Gateway. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito** e selezionare il nodo **Server e ruoli del sistema del sito**. Selezionare il server con il ruolo Provider SMS. Nel riquadro dei dettagli selezionare il ruolo **Provider SMS** e scegliere **Proprietà** nella barra multifunzione della scheda Ruolo del sito. Selezionare l'opzione **Consenti il traffico di Configuration Manager Cloud Management Gateway per il servizio di amministrazione**.  

- Provider SMS richiede **.NET 4.5.2** o versioni successive.  

- Configurare un [gateway di gestione cloud](../../core/clients/manage/cmg/plan-cloud-management-gateway.md).

- Eseguire l'onboarding del sito nei [servizi Azure](../../core/servers/deploy/configure/azure-services-wizard.md) per la **gestione cloud**.

- Abilitare l'[individuazione utenti di Azure AD](../../core/servers/deploy/configure/configure-discovery-methods.md#azureaadisc).

- Configurare manualmente le impostazioni di Azure AD:  

    1. Passare al [portale di Azure](https://portal.azure.com) come utente con autorizzazioni di *amministratore globale*. Passare ad **Azure Active Directory** e selezionare **Registrazioni app**.  

    1. Selezionare l'applicazione creata per l'integrazione **Gestione cloud** di Configuration Manager.  

    1. Nel menu **Gestisci** selezionare **Autorizzazione**.  

        1. Nella sezione **URI di reindirizzamento** incollare il percorso seguente: `https://<CMG FQDN>/CCM_Proxy_ServerAuth/ImplicitAuth`  

        1. Sostituire `<CMG FQDN>` con il nome di dominio completo (FQDN) del servizio Cloud Management Gateway (CMG). Ad esempio, GraniteFalls.Contoso.com.  

        1. Selezionare **Salva**.  

    1. Nel menu **Gestisci** selezionare **Manifesto**.  

        1. Nel riquadro Modifica manifesto individuare la proprietà **oauth2AllowImplicitFlow**.  

        1. Impostarne il valore su **true**. L'intera riga dovrebbe assomigliare, ad esempio, alla riga seguente: `"oauth2AllowImplicitFlow": true,`  

        1. Selezionare **Salva**.  

### <a name="configure-email-approval"></a>Configurare l'approvazione tramite posta elettronica

1. Nella console di Configuration Manager [distribuire un'applicazione](deploy-applications.md) come disponibile a una raccolta di utenti. Nella pagina **Impostazioni di distribuzione** abilitarla per l'approvazione. Immettere quindi uno o più indirizzi di posta elettronica per ricevere le notifiche. Se vi sono più indirizzi di posta elettronica, separarli con un punto e virgola (`;`).  

     > [!Note]  
     > Chiunque riceva il messaggio di posta elettronica nell'organizzazione di Azure AD può approvare la richiesta. Non inoltrare il messaggio di posta elettronica ad altri utenti a meno che non si voglia che intervengano.  

2. Come utente, richiedere l'applicazione in Software Center.  

3. Si riceve una notifica tramite posta elettronica entro cinque minuti. Il contenuto del messaggio di posta elettronica è simile al seguente:  

![Notifica tramite posta elettronica di esempio per l'approvazione dell'applicazione](media/1321550-email.png)

> [!Note]  
> Il collegamento per approvare o rifiutare è monouso. Ad esempio, se si configura un alias di gruppo per ricevere le notifiche e un utente approva la richiesta, un altro utente del gruppo non potrà rifiutarla.  

Rivedere il file **NotiCtrl.log** nel server del sito per la risoluzione dei problemi.

## <a name="maintenance"></a>Manutenzione

Configuration Manager memorizza le informazioni relative alla richiesta di approvazione per l'applicazione nel database del sito. La cronologia delle richieste annullate o rifiutate viene eliminata dal sito dopo 30 giorni. È possibile configurare il comportamento di eliminazione con l'**attività di manutenzione del sito** [Elimina dati richiesta applicazione obsoleti](../../core/servers/manage/maintenance-tasks.md). Il sito non elimina mai le richieste applicazione approvate o in attesa.