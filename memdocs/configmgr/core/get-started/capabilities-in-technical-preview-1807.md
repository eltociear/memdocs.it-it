---
title: Technical Preview 1807
titleSuffix: Configuration Manager
description: Informazioni sulle nuove funzionalità disponibili in Configuration Manager Technical Preview versione 1807.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bcde47a7-433e-4944-964b-539b17d15d64
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: ace27e9035af6696e455382a32365be0e3824d65
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905207"
---
# <a name="capabilities-in-configuration-manager-technical-preview-version-1807"></a>Funzionalità in Configuration Manager Technical Preview versione 1807 

*Si applica a: Configuration Manager (Technical Preview Branch)*

Questo articolo presenta le funzionalità disponibili nella Technical Preview per Configuration Manager, versione 1807. Installare questa versione per aggiornare il sito delle anteprime tecniche aggiungendovi nuove funzionalità. 

Prima di installare questo aggiornamento, vedere l'articolo [Technical Preview](technical-preview.md). L'articolo consente di acquisire familiarità con i requisiti e le limitazioni generali per l'uso di una Technical Preview, con l'aggiornamento tra le versioni e con l'invio di commenti e suggerimenti.     


<!--  Known Issues Template
## Known issues 

### <a name="ki_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->



## <a name="known-issues"></a>Problemi noti 

### <a name="issues-with-office-365-software-updates"></a><a name="ki_o365"></a> Problemi con gli aggiornamenti software di Office 365
<!--521365-->
Se si gestiscono gli aggiornamenti di Office 365 con le versioni Technical Preview 1806 e 1806.2, l'installazione nei client potrebbe non riuscire. 

#### <a name="workaround"></a>Soluzione alternativa
- Eliminare i pacchetti di distribuzione esistenti e i gruppi di aggiornamenti software per Office 365.  

- A partire dal 31 luglio 2018, sincronizzare gli aggiornamenti software di Office 365 e distribuire solo gli aggiornamenti più recenti.  



</br>

**Le sezioni seguenti descrivono le nuove funzionalità da provare in questa versione:**  


## <a name="community-hub"></a><a name="bkmk_hub"></a> Hub della community
<!--1357766-->

L'Hub della community è una posizione centralizzata per la condivisione di oggetti utili di Configuration Manager con altri utenti. Vedere la nuova area di lavoro **Community** nella console di Configuration Manager e selezionare il nodo **Hub**. Usare l'Hub della community per scaricare i seguenti tipi di oggetti di Configuration Manager: 
- Script
- Elementi di configurazione

![Console di Configuration Manager, area di lavoro Community, nodo Hub](media/1357766-hub.png)

Per visualizzare altri dettagli su un elemento disponibile, fare clic nell'hub. Dalla pagina dei dettagli fare clic su **Scarica** per acquisire l'elemento. Quando lo si scarica dall'hub, l'elemento viene aggiunto automaticamente al sito. 

![Console di Configuration Manager, area di lavoro Community, nodo Hub, pagina dei dettagli](media/1357766-hub-details.png)

L'area di lavoro **Community** include anche i nodi seguenti:

- **Documentazione**: visualizza la [libreria della documentazione](https://docs.microsoft.com/sccm/) di Configuration Manager  

- **Commenti e suggerimenti**: visualizza il [sito UserVoice](https://configurationmanager.uservoice.com/) di Configuration Manager  


### <a name="prerequisites"></a>Prerequisiti

- Usare la console di Configuration Manager in un sistema operativo client.  

    - In alternativa, ma non consigliato: in un sistema operativo server disabilitare [ Protezione avanzata di Internet Explorer](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd883248(v=ws.10)).

- Il computer con la console deve avere accesso a Internet e la connettività ai siti seguenti:  
    - `https://aka.ms`  
    - `https://comfigmgr-hub.azurewebsites.net`  
    - `https://configmgronline.visualstudio.com`  


### <a name="known-issue"></a>Problema noto

Il contributo di elementi nell'hub non è attualmente disponibile in questa versione. 



## <a name="specify-the-drive-for-offline-os-image-servicing"></a><a name="bkmk_osd"></a> Specificare l'unità per la manutenzione di immagini del sistema operativo offline  
<!--1358924-->

In base ai [commenti e suggerimenti do UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/33506009-gui-option-for-offline-os-image-servicing-drive), è ora possibile specificare l'unità usata da Configuration Manager durante la manutenzione offline delle immagini del sistema operativo. Questo processo può utilizzare una grande quantità di spazio su disco con i file temporanei, pertanto questa opzione offre la flessibilità di selezionare l'unità da usare. 


### <a name="try-it-out"></a>Verifica

Provare a completare le attività. Inviare quindi [commenti e suggerimenti](capabilities-in-technical-preview-1804.md#bkmk_feedback) con le proprie opinioni sulla funzionalità.

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito** e selezionare **Siti**. Fare clic su **Configura componenti del sito** nella barra multifunzione e selezionare **Punto di aggiornamento software**.  

2. Passare alla scheda **Installazione offline** e specificare l'opzione **A local drive to be used by offline servicing of images** (Unità locale usata dalla manutenzione offline delle immagini).  

L'impostazione predefinita di questa opzione è **Automatic** (Automatica). Con questo valore, Configuration Manager seleziona l'unità in cui è installato. 

Durante l'installazione offline, Configuration Manager archivia i file temporanei nella cartella `<drive>:\ConfigMgr_OfflineImageServicing` e monta anche le immagini del sistema operativo in questa cartella. 

Vedere il file di log **OfflineServicingMgr.log**. 



## <a name="co-managed-device-sync-activity-from-intune"></a><a name="bkmk_comgmt"></a> Attività di sincronizzazione dei dispositivi con co-gestione con Intune
<!--1358565-->

Consente di indicare nella console di Configuration Manager se un dispositivo con co-gestione è attivo con Microsoft Intune. Questo stato si basa sui dati provenienti dal [data warehouse di Intune](https://docs.microsoft.com/intune/reports-nav-create-intune-reports). Il dashboard **Stato client** nella console di Configuration Manager mostra i **Clienti inattivi che usano Intune**. Questa nuova categoria è destinata ai dispositivi con co-gestione inattivi con Configuration Manager, ma sincronizzati con il servizio di Intune nell'ultima settimana.


### <a name="try-it-out"></a>Verifica

Provare a completare le attività. Inviare quindi [commenti e suggerimenti](capabilities-in-technical-preview-1804.md#bkmk_feedback) con le proprie opinioni sulla funzionalità.

Se il sito è già stato configurato per la co-gestione: 

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Servizi cloud** e selezionare il nodo **Co-gestione**. Fare clic su **Proprietà** nella barra multifunzione.  

2. Passare alla scheda **Creazione report**. Fare clic su **Accedi** ed eseguire l'autenticazione. Quindi fare clic su **Aggiorna** per abilitare le autorizzazioni di lettura per il data warehouse di Intune.  

3. Dopo la sincronizzazioni del sito con Intune, passare all'area di lavoro **Monitoraggio** e selezionare il nodo **Stato client**. Nella sezione **Stato client generale** vedere la riga per **Clienti inattivi che usano Intune**.  

Per altre informazioni sulla co-gestione, vedere [Co-gestione per dispositivi Windows 10](../../comanage/overview.md).



## <a name="repair-applications"></a><a name="bkmk_app-repair"></a> Ripristinare le applicazioni
<!--1357866-->

In risposta ai [commenti e suggerimenti di UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8365071-force-reinstall-of-application), è ora possibile specificare una riga di comando di ripristino per i tipi di distribuzione Windows Installer e Programma di installazione dello script. 


### <a name="try-it-out"></a>Verifica

Provare a completare le attività. Inviare quindi [commenti e suggerimenti](capabilities-in-technical-preview-1804.md#bkmk_feedback) con le proprie opinioni sulla funzionalità.

1. Nella console di Configuration Manager aprire le proprietà di un tipo di distribuzione Windows Installer o Programma di installazione dello script.  

2. Passare alla scheda **Programmi**. Specificare il comando **Ripristino programma**.  

3. Distribuire l'app. Nella scheda **Impostazioni di distribuzione** della distribuzione abilitare l'opzione **Consenti agli utenti finali di provare a ripristinare questa applicazione**.  


### <a name="known-issue"></a>Problema noto

Il nuovo pulsante **Ripristina** in Software Center, che consente agli utenti di ripristinare l'app, non è visibile in questa versione.  



## <a name="approve-application-requests-via-email"></a><a name="bkmk_email-approve"></a> Approvare le richieste dell'applicazione tramite posta elettronica
<!--1321550-->

È possibile configurare le notifiche tramite posta elettronica per le richieste di approvazione dell'applicazione. Quando un utente richiede un'applicazione, si riceve un messaggio di posta elettronica. Fare clic sui collegamenti nel messaggio di posta elettronica per approvare o rifiutare la richiesta, senza che sia necessario usare la console di Configuration Manager.


### <a name="prerequisites"></a>Prerequisiti

#### <a name="to-send-email-notifications"></a>Per inviare notifiche tramite posta elettronica
- Abilitare la [funzionalità facoltativa](../servers/manage/install-in-console-updates.md#bkmk_options) **Approva le richieste dell'applicazione per gli utenti per ogni dispositivo**.  

- Configurare la [notifica tramite posta elettronica per gli avvisi](../servers/manage/use-alerts-and-the-status-system.md#to-configure-email-notification-for-alerts).  

#### <a name="to-approve-or-deny-requests-from-email"></a>Per approvare o rifiutare le richieste dal messaggio di posta elettronica
Se non si configurano questi prerequisiti, il sito invia notifica tramite posta elettronica per le richieste dell'applicazione senza collegamenti per approvare o rifiutare la richiesta.  

- Nelle proprietà del sito selezionare **Abilita l'endpoint REST per tutti i ruoli del provider in questo sito e consenti il traffico di Cloud Management Gateway di Configuration Manager**. Per altre informazioni, vedere [Accesso ai dati di endpoint OData](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access).  

    - Riavviare il servizio SMS_EXEC dopo aver abilitato l'endpoint REST

- [Gateway di gestione cloud](../clients/manage/cmg/plan-cloud-management-gateway.md)  

- Eseguire l'onboarding del sito in [servizi di Azure](../servers/deploy/configure/azure-services-wizard.md) per la **gestione del cloud**  

    - Abilitare [Individuazione utente Azure AD](../servers/deploy/configure/configure-discovery-methods.md#azureaadisc)  

    - Configurare manualmente le impostazioni seguenti per questa app nativa in Azure AD:  

        - **URI di reindirizzamento**: `https://<CMG FQDN>/CCM_Proxy_ServerAuth/ImplicitAuth`. Usare il nome di dominio completo (FQDN) del servizio Cloud Management Gateway (CMG), ad esempio, GraniteFalls.Contoso.com.   

        - **Manifesto**: impostare **oauth2AllowImplicitFlow** su true: `"oauth2AllowImplicitFlow": true,`  


### <a name="try-it-out"></a>Verifica

Provare a completare le attività. Inviare quindi [commenti e suggerimenti](capabilities-in-technical-preview-1804.md#bkmk_feedback) con le proprie opinioni sulla funzionalità.

1. Nella console di Configuration Manager distribuire un'applicazione come disponibile a una raccolta di utenti. Nella pagina **Impostazioni di distribuzione** abilitarla per l'approvazione. Immettere quindi un *singolo* indirizzo di posta elettronica per ricevere le notifiche.  

     > [!Note]  
     > Chiunque riceva il messaggio di posta elettronica nell'organizzazione di Azure AD può approvare la richiesta. Non inoltrare il messaggio di posta elettronica ad altri utenti a meno che non si voglia che intervengano.  

2. Come utente, richiedere l'applicazione in Software Center.  

3. Si riceve una notifica tramite posta elettronica simile all'esempio seguente:  

![Notifica tramite posta elettronica di esempio per l'approvazione dell'applicazione](media/1321550-email.png)

> [!Note]  
> Il collegamento per approvare o rifiutare è monouso. Ad esempio, se si configura un alias di gruppo per ricevere le notifiche e un utente approva la richiesta, un altro utente del gruppo non potrà rifiutarla.  



## <a name="improvement-to-script-output"></a><a name="bkmk_script"></a> Miglioramento dell'output degli script
<!--1236459-->

È ora possibile visualizzare l'output degli script dettagliato in formato JSON non elaborato o strutturato. Questo tipo di formattazione rende più facile leggere e analizzare l'output. Se lo script restituisce testo in formato JSON valido, è possibile visualizzare l'output dettagliato come **Output JSON** oppure **Output non elaborato**. In caso contrario, l'unica opzione è **Output dello script**. 

#### <a name="example-script-output-is-valid-json"></a>Esempio: output dello script in formato JSON valido
Comando: `$PSVersionTable.PSVersion`  

``` Output
Major  Minor  Build  Revision
-----  -----  -----  --------
5      1      16299  551
```

#### <a name="example-script-output-isnt-valid-json"></a>Esempio: output dello script non in formato JSON valido
Comando: `Write-Output (Get-WmiObject -Class Win32_OperatingSystem).Caption`  

``` Output
Microsoft Windows 10 Enterprise
```


### <a name="try-it-out"></a>Verifica

Provare a completare le attività. Inviare quindi [commenti e suggerimenti](capabilities-in-technical-preview-1804.md#bkmk_feedback) con le proprie opinioni sulla funzionalità.

1. Nella console di Configuration Manager passare all'area di lavoro **Asset e conformità** e selezionare il nodo **Raccolte dispositivi**. Fare clic con il pulsante destro del mouse su una raccolta e scegliere **Esegui script**. Per altre informazioni sulla creazione e l'esecuzione di script, vedere [Creare ed eseguire script di PowerShell dalla console di Configuration Manager](../../apps/deploy-use/create-deploy-scripts.md).  

2. Eseguire uno script sulla raccolta di destinazione.  

3. Nella pagina **Monitoraggio dello stato dello script** della procedura guidata Esegui script selezionare la scheda **Riepilogo** nella parte inferiore. Selezionare **Output dello script** e **Tabella dati** nei due elenchi a discesa in alto. Fare quindi doppio clic sulla riga dei risultati per aprire la finestra di dialogo **Detailed Output** (Output dettagliato).  

4. Nella pagina **Monitoraggio dello stato dello script** della procedura guidata Esegui script selezionare la scheda **Dettagli esecuzione** nella parte inferiore. Fare doppio clic sulla riga dei risultati per aprire la finestra di dialogo Detailed Output (Output dettagliato) per tale dispositivo.  



## <a name="improvement-to-third-party-software-updates"></a><a name="bkmk_3pupdate"></a> Miglioramento degli aggiornamenti software di terze parti
<!--1358714-->

È ora possibile modificare le proprietà di cataloghi personalizzati.

Per altre informazioni, vedere [Supporto per gli aggiornamenti software di terze parti per i cataloghi personalizzati](capabilities-in-technical-preview-1806-2.md#bkmk_3pupdate).



## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sull'installazione o l'aggiornamento del ramo Technical Preview, vedere [Technical Preview](technical-preview.md).    

Per altre informazioni sui diversi rami di Configuration Manager, vedere [Scelta del ramo di Configuration Manager da usare](../understand/which-branch-should-i-use.md)
