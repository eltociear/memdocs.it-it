---
title: Technical Preview 1806
titleSuffix: Configuration Manager
description: Informazioni sulle nuove funzionalità disponibili in Configuration Manager Technical Preview versione 1806.
ms.date: 06/06/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 52d64ef0-8c0d-42c3-857e-07d7ec776f29
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 44fcea129b6f45c292bcdd6b83004131ce2d4e96
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694424"
---
# <a name="capabilities-in-technical-preview-1806-for-configuration-manager"></a>Funzionalità della versione Technical Preview 1806 per Configuration Manager

*Si applica a: Configuration Manager (Technical Preview Branch)*

Questo articolo presenta le funzionalità disponibili nella Technical Preview per Configuration Manager, versione 1806. È possibile installare questa versione per aggiornare il sito delle anteprime tecniche aggiungendovi nuove funzionalità. 

Prima di installare questo aggiornamento, vedere l'articolo [Technical Preview](technical-preview.md). L'articolo consente di acquisire familiarità con i requisiti e le limitazioni generali per l'uso di una Technical Preview, con l'aggiornamento tra le versioni e con l'invio di commenti e suggerimenti.     


<!--  Known Issues Template
## Known Issues in this Technical Preview

### <a name="ki_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->
## <a name="known-issues-in-this-technical-preview"></a>Problemi noti di questa versione Technical Preview

### <a name="site-fails-to-upgrade-with-remote-content-library"></a><a name="ki_contentlib"></a> Impossibile aggiornare il sito con una raccolta contenuto remota
<!--514642-->
Il sito non esegue l'aggiornamento con gli errori seguenti in **cmupdate.log**:  

``` Log
Failed to find any valid drives  
GetContentLibraryParameters failed; 0x80070057  
ERROR: Failed to process configuration manager update.  
```  

Questo problema si verifica in questa versione quando la raccolta contenuto si trova in una posizione remota.

#### <a name="workaround"></a>Soluzione alternativa
Spostare la raccolta contenuto in un'unità locale nel server del sito. Per altre informazioni, vedere [Configurare una raccolta contenuto remota per il server del sito](capabilities-in-technical-preview-1804.md#configure-a-remote-content-library-for-the-site-server). 



</br>

**Di seguito sono riportate le nuove funzionalità disponibili con questa versione.**  



## <a name="third-party-software-updates"></a><a name="bkmk-3pupdate"></a> Aggiornamenti di software di terze parti
<!--1352101-->
Questa versione esegue un'ulteriore iterazione sul supporto per gli aggiornamenti software di terze parti in seguito ai [commenti e suggerimenti raccolti con UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8803711-3rd-party-patching-scup-integration-with-sccm-co). Non è più necessario usare System Center Updates Publisher (SCUP) per alcuni scenari comuni. Il nuovo nodo **Cataloghi di aggiornamenti software di terze parti** nella console di Configuration Manager consente di sottoscrivere i cataloghi di terze parti, pubblicarne gli aggiornamenti nel punto di aggiornamento software e quindi implementare i cataloghi nei client. 

I seguenti cataloghi di aggiornamento software di terze parti sono disponibili in questa versione:

 | Pubblicazione | Nome catalogo |
 |--------|---------------------|
 | HP | Catalogo degli aggiornamenti client di HP |

SCUP continua a supportare altri cataloghi e scenari. L'elenco dei cataloghi nel nodo Cataloghi di aggiornamento software di terze parti della console di Configuration Manager è dinamico e viene aggiornato non appena sono disponibili e supportati altri cataloghi.


### <a name="prerequisites"></a>Prerequisiti
- Configurare la gestione degli aggiornamenti software, con un punto di aggiornamento software abilitato per HTTPS. Per altre informazioni, vedere [Prerequisiti per aggiornamenti software](../../sum/get-started/prepare-for-software-updates-management.md).  
  - Il punto di aggiornamento software deve essere nel server del sito per questa funzionalità in questa versione. <!--515810--> 

    > [!Tip]  
    > Il punto di aggiornamento software richiede HTTPS perché è un requisito per le API WSUS usate per gestire i certificati di firma. Non è necessario che anche i client siano abilitati per HTTPS. Per altre informazioni sull'abilitazione di HTTPS in WSUS, vedere gli articoli seguenti per ulteriore assistenza:  
    > - [Secure WSUS with the Secure Sockets Layer Protocol](/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#25-secure-wsus-with-the-secure-sockets-layer-protocol) (Proteggere WSUS con il protocollo Secure Sockets Layer) 
    > - [Post di blog sul supporto di WSUS](/archive/blogs/sus/how-to-create-an-internet-facing-wsus-server-that-uses-different-internal-and-external-names)

- Spazio su disco sufficiente nel punto di aggiornamento software, cartella WSUSContent, per archiviare il contenuto binario di origine per gli aggiornamenti software di terze parti. La quantità di memoria richiesta varia in base al fornitore, ai tipi di aggiornamenti e agli aggiornamenti specifici pubblicati per la distribuzione. Se è necessario spostare la cartella WSUSContent in un'altra unità con maggiore spazio disponibile, vedere il post di blog del team di supporto tecnico di WSUS relativo alla [modifica del percorso in cui WSUS archivia aggiornamenti in locale](/archive/blogs/sus/wsus-how-to-change-the-location-where-wsus-stores-updates-locally).  

- Abilitare e distribuire l'impostazione client [Abilita gli aggiornamenti software di terze parti](../clients/deploy/about-client-settings.md#enable-third-party-software-updates) nel gruppo **Aggiornamenti software**.  

- Il server del sito richiede l'accesso Internet a download.microsoft.com attraverso la porta HTTPS 443. Il servizio di sincronizzazione degli aggiornamenti software di terze parti attualmente viene eseguito nel server del sito. Questo servizio aggiorna l'elenco dei cataloghi di terze parti disponibili, scarica i cataloghi quando si effettua la sottoscrizione e scarica gli aggiornamenti quando vengono pubblicati. Configurare le impostazioni proxy Internet, se necessario, nella scheda **Proxy** delle proprietà del ruolo del sistema del sito del computer server del sito.  


### <a name="try-it-out"></a>Verifica
 Provare a completare le attività. Inviare quindi [commenti e suggerimenti](capabilities-in-technical-preview-1804.md#bkmk_feedback).


#### <a name="phase-1-enable-and-set-up-the-feature"></a>Fase 1: Abilitare e configurare la funzionalità
Eseguire le operazioni descritte di seguito *una volta per ogni gerarchia* per abilitare e configurare la funzionalità per l'uso:  

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**. Espandere **Configurazione del sito** e selezionare il nodo **Siti**.  

2. Selezionare il sito al primo livello della gerarchia. Fare clic su **Configura componenti del sito** nella barra multifunzione e selezionare **Punto di aggiornamento software**.  

3. Passare alla scheda **Aggiornamenti di terze parti**. Selezionare l'opzione che consente di **abilitare gli aggiornamenti software di terze parti**. Per altre informazioni sulle opzioni di certificato, vedere [Miglioramenti all'abilitazione del supporto degli aggiornamenti software di terze parti](capabilities-in-technical-preview-1805.md#improvements-for-enabling-third-party-software-update-support).  

   > [!Note]  
   > Se si usa l'opzione predefinita per Configuration Manager per gestire questo certificato, un nuovo certificato di tipo **Firma WSUS di terze parti** creato nel nodo **Certificati** in  **Protezione** nell'area di lavoro **Amministrazione**.  


#### <a name="phase-2-subscribe-to-a-third-party-catalog-and-sync-updates"></a>Fase 2: Sottoscrivere un catalogo di terze parti e sincronizzare gli aggiornamenti
Eseguire la procedura seguente per *ogni catalogo di terze parti* per cui si vuole effettuare la sottoscrizione:  

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**. Espandere **Aggiornamenti software** e selezionare il nodo **Cataloghi di aggiornamenti software di terze parti**.  

2. Selezionare il catalogo per cui eseguire la sottoscrizione e fare clic su **Sottoscrivi il catalogo** nella barra multifunzione.   

3. Rivedere e approvare il certificato del catalogo.  

   > [!Note]  
   > Quando si sottoscrive un catalogo di aggiornamenti software di terze parti, il certificato rivisto e approvato nella procedura guidata viene aggiunto al sito. Questo certificato è di tipo **Catalogo di aggiornamenti software di terze parti**. È possibile gestirlo dal nodo **Certificati** in **Protezione** nell'area di lavoro **Amministrazione**.  

4. Completare la procedura guidata.  

   > [!Tip]  
   > Dopo la sottoscrizione iniziale, viene immediatamente avviato il download del catalogo. Il catalogo viene quindi risincronizzato ogni 24 ore in questa versione. Se si preferisce non attendere il download automatico del catalogo, fare clic su **Sincronizza ora** nella barra multifunzione.  
   > 
   > Eseguito il download del catalogo, i metadati del prodotto devono essere sincronizzati con il punto di aggiornamento software. Per altre informazioni su questo processo nonché sulle modalità di avvio manuale, vedere [Sincronizzare gli aggiornamenti software](../../sum/get-started/synchronize-software-updates.md). A questo punto, è possibile visualizzare gli aggiornamenti di terze parti nel nodo **Tutti gli aggiornamenti**. 

5. Quindi, configurare il punto di aggiornamento software **Prodotti** per il catalogo di terze parti sottoscritto. Per altre informazioni, vedere [Configurare le classificazioni e i prodotti per la sincronizzazione](../../sum/get-started/configure-classifications-and-products.md). Dopo la modifica di criteri di prodotto, deve verificarsi nuovamente la sincronizzazione degli aggiornamenti software.

Per poter visualizzare i risultati di conformità dei client, è necessario analizzare e valutare gli aggiornamenti. È possibile attivare manualmente questo ciclo dal pannello di controllo di Configuration Manager in un client eseguendo l'azione **Ciclo di analisi per aggiornamenti software**. Per altre informazioni sul processo, vedere l'[introduzione agli aggiornamenti software](../../sum/understand/software-updates-introduction.md).


#### <a name="phase-3-deploy-third-party-software-updates"></a>Fase 3: Distribuire gli aggiornamenti software di terze parti
Eseguire la procedura riportata di seguito per *tutti gli aggiornamenti software di terze parti* da distribuire ai client:  

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**. Espandere **Aggiornamenti software** e selezionare il nodo **Tutti gli aggiornamenti software**.  

   > [!Tip]  
   > Fare clic su **Aggiungi criteri** per filtrare l'elenco degli aggiornamenti. Ad esempio, aggiungere **Fornitore** per **Adobe Systems, Inc.** per visualizzare tutti gli aggiornamenti di Adobe.  

2. Selezionare gli aggiornamenti richiesti dai client. Fare clic su **Pubblica il contenuto degli aggiornamenti software di terze parti** ed esaminare lo stato di avanzamento in SMS_ISVUPDATES_SYNCAGENT.log. Questa azione scarica file binari di aggiornamento del fornitore e li archivia nella cartella WSUSContent nel punto di aggiornamento software. Modifica inoltre lo stato dell'aggiornamento da solo metadati a con contenuto e distribuibile.  

   > [!Note]  
   > Quando si pubblicano contenuti degli aggiornamenti software di terze parti tutti i certificati usati per firmare i contenuti vengono aggiunti al sito. Questi certificati sono di tipo **Contenuto degli aggiornamenti software di terze parti**. È possibile gestirli dal nodo **Certificati** in **Protezione** nell'area di lavoro **Amministrazione**.  

3. Distribuire gli aggiornamenti usando il processo di gestione degli aggiornamenti software esistente. Per altre informazioni, vedere [Distribuire gli aggiornamenti software](../../sum/deploy-use/deploy-software-updates.md). Nella pagina dei **percorsi per il download** della distribuzione guidata degli aggiornamenti software selezionare l'opzione predefinita per **scaricare gli aggiornamenti software da Internet**. In questo scenario il contenuto è già pubblicato nel punto di aggiornamento software, che viene usato per scaricare il contenuto per il pacchetto di distribuzione.


### <a name="monitoring-progress-of-third-party-software-updates"></a>Monitoraggio dello stato degli aggiornamenti software di terze parti
La sincronizzazione degli aggiornamenti software di terze parti viene gestita dal componente SMS_ISVUPDATES_SYNCAGENT nel server del sito. È possibile visualizzare i messaggi di stato da questo componente o vedere lo stato più in dettaglio in SMS_ISVUPDATES_SYNCAGENT.log. Questo log si trova nel server del sito, nella sottocartella **Log** della directory di installazione del sito. Per impostazione predefinita, il percorso è `C:\Program Files\Microsoft Configuration Manager\Logs`. Per altre informazioni sul monitoraggio della gestione generale degli aggiornamenti software, vedere [Monitorare gli aggiornamenti software](../../sum/deploy-use/monitor-software-updates.md).


### <a name="known-issues"></a>Problemi noti
- Il servizio di sincronizzazione degli aggiornamenti software di terze parti non supporta il punto di aggiornamento software configurato per l'uso di un **account di connessione al server WSUS**. Se questo account è configurato nella scheda **Impostazioni proxy e account** della pagina Proprietà del punto di aggiornamento software, verrà visualizzato il seguente errore in SMS_ISVUPDATES_SYNCAGENT.log:  
`WSUS access account appears to be configured, it is not yet supported for third party updates sync.`  
Per altre informazioni su questo account, vedere [Account di connessione al punto di aggiornamento software](../plan-design/hierarchy/accounts.md#software-update-point-connection-account).<!--515492-->  

- Non combinare l'uso di altri strumenti, ad esempio SCUP, con questa nuova funzionalità integrata per gli aggiornamenti software di terze parti. Il servizio di sincronizzazione degli aggiornamenti software di terze parti non è in grado di pubblicare contenuto negli aggiornamenti di soli metadati aggiunti a WSUS usando un'altra applicazione o un altro strumento o script, ad esempio SCUP. L'azione **Pubblica il contenuto degli aggiornamenti software di terze parti** avrà esito negativo per questi aggiornamenti. Se è necessario distribuire aggiornamenti di terze parti che questa funzionalità non supporta ancora, usare per intero il processo esistente per distribuire tali aggiornamenti.<!--515497-->  



## <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge"></a>Configurare le impostazioni di Windows Defender SmartScreen per Microsoft Edge
<!--1353701-->
In questa versione vengono aggiunte tre impostazioni per [Windows Defender SmartScreen](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-smartscreen/microsoft-defender-smartscreen-overview) ai [criteri delle impostazioni di conformità del browser Microsoft Edge](../../compliance/deploy-use/browser-profiles.md). I criteri ora includono le seguenti impostazioni aggiuntive nella pagina **Impostazioni di SmartScreen**:
- **Consenti SmartScreen**: specifica se Windows Defender SmartScreen è consentito. Per altre informazioni, vedere il [criterio di browser AllowSmartScreen](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen).
- **Gli utenti possono eseguire l'override del prompt di SmartScreen per i siti**: specifica se gli utenti possono eseguire l'override degli avvisi del filtro Windows Defender SmartScreen su siti Web potenzialmente dannosi. Per altre informazioni, vedere il [criterio di browser PreventSmartScreenPromptOverride](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride).
- **Gli utenti possono eseguire l'override del prompt di SmartScreen per i file**: specifica se gli utenti possono eseguire l'override degli avvisi del filtro Windows Defender SmartScreen sul download di file non verificati. Per altre informazioni, vedere il [criterio di browser PreventSmartScreenPromptOverrideForFiles](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles).



## <a name="sync-mdm-policy-from-microsoft-intune-for-a-co-managed-device"></a>Sincronizzare i criteri MDM da Microsoft Intune per un dispositivo con co-gestione
<!--1357377-->
A partire da questa versione, quando si [passa a un altro carico di lavoro co-gestione](../../comanage/how-to-switch-workloads.md), i dispositivi in co-gestione sincronizzano automaticamente i criteri di gestione dei dati master di Microsoft Intune. La sincronizzazione si verifica anche quando si avvia l'azione **Scarica criteri computer** dalle notifiche client nella console di Configuration Manager. Per altre informazioni, vedere [Avviare il recupero dei criteri client usando la notifica client](../clients/manage/manage-clients.md#BKMK_PolicyRetrieval).



## <a name="transition-office-365-workload-to-intune-using-co-management"></a>Eseguire la transizione del carico di lavoro di Office 365 a Intune usando la co-gestione
<!--1357841-->
È ora possibile eseguire la transizione del carico di lavoro di Office 365 da Configuration Manager a Intune dopo aver abilitato la co-gestione. Per eseguire la transizione di questo carico di lavoro, passare alla pagina delle proprietà di co-gestione e spostare la barra del dispositivo di scorrimento da Configuration Manager su Pilota o Tutte. Per altre informazioni, vedere [Co-gestione per dispositivi Windows 10](../../comanage/overview.md).

È inoltre disponibile una nuova condizione globale che determina se **le applicazioni di Office 365 sono gestite da Intune nel dispositivo**. Questa condizione viene aggiunta per impostazione predefinita come requisito alle nuove applicazioni di Office 365. Durante la transizione di questo carico di lavoro, i client in co-gestione non soddisfano il requisito relativo all'applicazione, quindi non installano Office 365 distribuito da Configuration Manager.

### <a name="known-issue"></a>Problema noto
- Questa transizione del carico di lavoro attualmente si applica solo alle distribuzioni di Office 365. Configuration Manager continua a gestire gli aggiornamenti di Office 365.<!--510876--> Per altre informazioni, tra cui una possibile soluzione alternativa, vedere la nota sulla versione 1802 di Configuration Manager [La modifica dell'impostazione client di Office 365 non è applicabile](../servers/deploy/install/release-notes.md).



## <a name="package-conversion-manager"></a>Package Conversion Manager 
<!--1357861-->
Package Conversion Manager è ora uno strumento integrato che consente di convertire i pacchetti di Configuration Manager 2007 legacy in applicazioni di Configuration Manager Current Branch. È quindi possibile usare le funzionalità di applicazioni come dipendenze, regole dei requisiti e affinità utente-dispositivo.

### <a name="try-it-out"></a>Verifica
 Provare a completare le attività. Inviare quindi [commenti e suggerimenti](capabilities-in-technical-preview-1804.md#bkmk_feedback).

> [!Important]  
> Se è già installata una versione precedente di Package Conversion Manager, disinstallarla prima di aggiornare il sito. La nuova versione integrata non richiede l'installazione, ma possono verificarsi conflitti con le versioni esistenti.  

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**. Espandere **Gestione applicazioni** e selezionare **Pacchetti**.  
2. Selezionare un pacchetto. Le tre opzioni seguenti sono disponibili nel gruppo di **conversione dei pacchetti** della barra multifunzione:  
     - **Analizza pacchetto**: avviare il processo di conversione analizzando il pacchetto.
     - **Converti pacchetto**: alcuni pacchetti possono essere facilmente convertiti in applicazioni con questa azione.
     - **Correggi e converti**: alcuni pacchetti richiedono la risoluzione dei problemi prima della conversione in applicazioni.  


3. Passare all'area di lavoro **Monitoraggio** e selezionare lo **stato di conversione del pacchetto**. Questo nuovo dashboard visualizza lo stato complessivo dell'analisi e della conversione dei pacchetti nel sito. Una nuova attività in background sintetizza automaticamente i dati di analisi.  

   > [!Tip]  
   > Package Conversion Manager non richiede la pianificazione dell'analisi dei pacchetti. Questa azione è ora gestita dall'attività di riepilogo integrata.  

![Schermata del dashboard di stato di conversione del pacchetto](media/1357861-pcm-dashboard.png)



## <a name="deploy-software-updates-without-content"></a>Distribuire aggiornamenti software senza contenuto
<!--1357933-->
È ora possibile distribuire gli aggiornamenti software ai dispositivi senza prima scaricare e distribuire il contenuto degli aggiornamenti software nei punti di distribuzione. Questa funzionalità è utile quando si lavora con il contenuto di aggiornamenti di dimensioni molto grandi o si vuole che i client ricevano sempre il contenuto dal servizio cloud Microsoft Update. I client in questo scenario possono anche scaricare il contenuto da peer in cui è già presente il contenuto necessario. Il client Gestione configurazione continua a gestire il download del contenuto, quindi è in grado di usare la funzionalità peer cache di Configuration Manager o altre tecnologie, ad esempio Ottimizzazione recapito. Questa funzionalità supporta qualsiasi tipo di aggiornamento supportato dalla gestione degli aggiornamenti software di Configuration Manager, tra cui gli aggiornamenti di Windows e Office. 

### <a name="try-it-out"></a>Verifica
 Provare a completare le attività. Inviare quindi [commenti e suggerimenti](capabilities-in-technical-preview-1804.md#bkmk_feedback).

1. Avviare una normale distribuzione degli aggiornamenti software. Per altre informazioni, vedere [Distribuire gli aggiornamenti software](../../sum/deploy-use/deploy-software-updates.md).
2. Nella pagina **Pacchetto di distribuzione** della Distribuzione guidata degli aggiornamenti software selezionare la nuova opzione per non usare **alcun pacchetto di distribuzione**.

### <a name="known-issues"></a>Problemi noti
- L'icona relativa a un aggiornamento distribuito con questa impostazione viene erroneamente visualizzata con una X rossa come se l'aggiornamento non fosse valido. Per altre informazioni, vedere [Icone usate per gli aggiornamenti software](../../sum/understand/software-updates-icons.md). <!--515556-->  
- Questa impostazione è integrata solo con la Distribuzione guidata degli aggiornamenti software. Non è attualmente disponibile con le regole di distribuzione automatica. <!--515558-->  



## <a name="office-customization-tool-integration-with-the-office-365-installer"></a>Integrazione dello Strumento di personalizzazione di Office con il Programma di installazione di Office 365
<!--1358149-->
Lo Strumento di personalizzazione di Office è ora integrato con il Programma di installazione di Office 365 nella console di Configuration Manager. Quando si crea una distribuzione per Office 365, è ora possibile configurare dinamicamente le impostazioni di gestibilità di Office più recenti. Lo Strumento di personalizzazione di Office viene aggiornato nello stesso momento in cui vengono rilasciate nuove build di Office 365. È ora possibile usufruire delle nuove impostazioni di gestibilità di Office 365 non appena sono disponibili. 

### <a name="prerequisites"></a>Prerequisiti
- Il computer che esegue la console di Configuration Manager deve avere accesso a Internet via HTTPS attraverso la porta 443. L'installazione guidata del client di Office 365 usa un'API di Web browser standard di Windows per aprire https://config.office.com. Se si usa un proxy Internet, l'utente deve essere in grado di accedere a questo URL.

### <a name="try-it-out"></a>Verifica
 Provare a completare le attività. Inviare quindi [commenti e suggerimenti](capabilities-in-technical-preview-1804.md#bkmk_feedback).

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software** e selezionare il nodo **Gestione client di Office 365**.
2. Fare clic sul riquadro **Programma di installazione di Office 365** nel dashboard per avviare l'installazione guidata del client di Office 365. Per altre informazioni, vedere [Distribuire app di Office 365](../../sum/deploy-use/manage-office-365-proplus-updates.md).
3. Nella pagina delle **impostazioni di Office** passare alla **pagina Web di Office**. Usare lo Strumento di personalizzazione di Office online per specificare le impostazioni per questa distribuzione. 
4. Al termine, fare clic su **Invia** in alto a destra. Completare l'installazione guidata del client di Office 365.



## <a name="improvements-to-cloud-management-gateway"></a>Miglioramenti al gateway di gestione cloud
Questa versione include i miglioramenti seguenti al gateway di gestione cloud (CMG, Cloud Management Gateway):

### <a name="simplified-client-bootstrap-command-line"></a>Riga di comando semplificata per bootstrap client
<!--1358215-->
Quando si installa il client Gestione configurazione su Internet usando un CMG, ora sono richieste meno proprietà della riga di comando. Per altre informazioni su un esempio di questo scenario, vedere la [riga di comando per l'installazione del client Gestione configurazione](../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client) durante la preparazione per la co-gestione. 

Le seguenti proprietà della riga di comando sono richieste in tutti gli scenari:
- CCMHOSTNAME  
- SMSSITECODE  

Le seguenti proprietà sono richieste quando si usa Azure AD per l'autenticazione client anziché i certificati di autenticazione client basati su infrastruttura a chiave pubblica:
- AADCLIENTAPPID  
- AADRESOURCEURI  

La seguente proprietà è obbligatoria se il client effettua il roaming alla rete intranet:
- SMSMP  

L'esempio seguente include tutte le proprietà indicate sopra:   
`ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com`

Per altre informazioni, vedere [Informazioni sulle proprietà di installazione del client in System Center Configuration Manager](../clients/deploy/about-client-installation-properties.md).

### <a name="download-content-from-a-cmg"></a>Scaricare il contenuto da un CMG
<!--1358651-->
In precedenza, era necessario distribuire un punto di distribuzione cloud e un gateway CMG come ruoli separati. Ora in questa versione un CMG può anche trasferire contenuti ai client. Questa funzionalità riduce i certificati necessari e i costi delle macchine virtuali di Azure. Per abilitare questa funzionalità, abilitare la nuova opzione che **consente a CMG di funzionare come punto di distribuzione cloud e rendere disponibili i contenuti di Archiviazione di Azure** nella scheda **Impostazioni** delle proprietà del CMG. 

### <a name="trusted-root-certificate-isnt-required-with-azure-ad"></a>Non è necessario un certificato radice trusted con Azure AD
<!--503899-->
Quando si crea un gateway CMG, non è più necessario specificare un [certificato radice trusted](../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_cmgroot) nella pagina Impostazioni. Questo certificato non è obbligatorio se si usa Azure Active Directory (Azure AD) per l'autenticazione client, ma veniva richiesto nella procedura guidata.

> [!Important]  
> Se si usano certificati di autenticazione client PKI, è comunque necessario aggiungere un certificato radice trusted al CMG.



## <a name="improvements-to-secure-client-communications"></a>Miglioramento delle comunicazioni client sicure
<!--1358278,1358279-->
Questa versione continua a perfezionare il [miglioramento delle comunicazioni client sicure](capabilities-in-technical-preview-1805.md#improved-secure-client-communications) rimuovendo altre dipendenze nell'account di accesso alla rete. Quando si abilita la nuova opzione del sito che consente di **usare i certificati generati da Configuration Manager per i sistemi di sito HTTP**, gli scenari seguenti non richiedono un account di accesso alla rete per scaricare il contenuto da un punto di distribuzione:  

- Sequenze di attività in esecuzione da supporti di avvio o PXE
- Sequenze di attività in esecuzione da Software Center  

Queste sequenze di attività possono essere per la distribuzione del sistema operativo o personalizzate. Sono anche supportate per i computer del gruppo di lavoro.



## <a name="software-center-infrastructure-improvements"></a>Miglioramenti all'infrastruttura di Software Center
<!--1358309-->
I ruoli del catalogo applicazioni non sono più necessari per visualizzare le applicazioni disponibili per gli utenti in Software Center. Questa modifica consente di ridurre l'infrastruttura server necessaria per distribuire le applicazioni agli utenti. Software Center ora si affida al punto di gestione per ottenere queste informazioni e questo consente una migliore scalabilità degli ambienti di grandi dimensioni, che vengono assegnati a [gruppi di limiti](../servers/deploy/configure/boundary-groups.md#management-points).

### <a name="try-it-out"></a>Verifica
 Provare a completare le attività. Inviare quindi [commenti e suggerimenti](capabilities-in-technical-preview-1804.md#bkmk_feedback).

1. Rimuovere tutti i ruoli del catalogo applicazioni dal sito. Questi ruoli includono il punto per servizi Web del Catalogo applicazioni e il punto per siti Web del Catalogo applicazioni.
2. Distribuire un'applicazione come disponibile a una raccolta di utenti.
3. Usare Software Center come utente di destinazione per individuare, richiedere e installare l'applicazione.

### <a name="known-issue"></a>Problema noto
- Se si usa un client aggiunto ad Azure Active Directory con questa funzionalità, non configurare il sito in modo da **usare i certificati generati da Configuration Manager per i sistemi di sito HTTP**. Al momento esiste un conflitto con questa funzionalità.<!--515846--> Per altre informazioni su questa impostazione, vedere [Comunicazioni client sicure migliorate](capabilities-in-technical-preview-1805.md#improved-secure-client-communications).



## <a name="provision-windows-app-packages-for-all-users-on-a-device"></a>Effettuare il provisioning dei pacchetti di app Windows per tutti gli utenti in un dispositivo
<!--1358310-->
È ora possibile eseguire il provisioning di un'applicazione con un pacchetto di app di Windows per tutti gli utenti nel dispositivo. Un esempio comune di questo scenario è il provisioning di un'app da Microsoft Store per le aziende e la formazione, ad esempio Minecraft: Education Edition, in tutti i dispositivi usati dagli studenti di una scuola. In precedenza, Configuration Manager supportava solo l'installazione di queste applicazioni per ogni utente. Dopo aver eseguito l'accesso a un nuovo dispositivo, uno studente dovrebbe attendere prima di poter accedere a un'app. Ora quando viene eseguito il provisioning dell'app nel dispositivo per tutti gli utenti, tutti possono essere produttivi più rapidamente.

> [!Important]  
> Prestare attenzione con l'installazione, il provisioning e l'aggiornamento di versioni diverse dello stesso pacchetto di app di Windows in un dispositivo, poiché possono causare risultati imprevisti. Questo comportamento può verificarsi quando si usa Configuration Manager per eseguire il provisioning dell'app, ma dopo si consente agli utenti di aggiornare l'app dal Microsoft Store. Per altre informazioni, vedere le istruzioni del passaggio successivo quando si [gestiscono le app dal Microsoft Store per le aziende](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md#next-steps).  

Quando si esegue il provisioning di un'app con licenza offline Configuration Manager non consente a Windows di aggiornarla automaticamente dal Microsoft Store.  

### <a name="try-it-out"></a>Verifica
 Provare a completare le attività. Inviare quindi [commenti e suggerimenti](capabilities-in-technical-preview-1804.md#bkmk_feedback).

1. Creare una nuova applicazione. Questa app deve far parte di un pacchetto app Windows o essere un'app con licenza offline, sincronizzata dal Microsoft Store per aziende e formazione.  

2. Nella pagina **Informazioni generali** della Creazione guidata applicazione abilitare l'opzione che consente di **eseguire il provisioning dell'applicazione per tutti gli utenti nel dispositivo**.  

   > [!Tip]  
   > Se si modifica un'applicazione esistente, questa impostazione è abilitata nella scheda **Esperienza utente** delle proprietà dell'applicazione.  

3. Distribuire l'applicazione a una raccolta di dispositivi.  

4. Accedere a un dispositivo di destinazione con diversi account utente e avviare l'applicazione.  

> [!Note]  
> Se è necessario disinstallare un'applicazione con provisioning dai dispositivi a cui gli utenti hanno già eseguito l'accesso, è necessario creare due distribuzioni di disinstallazione. Scegliere come destinazione della prima distribuzione di disinstallazione una raccolta di dispositivi che contenga i dispositivi. Scegliere come destinazione della seconda distribuzione di disinstallazione una raccolta di utenti che contenga gli utenti che hanno eseguito l'accesso ai dispositivi con l'applicazione con provisioning. Quando si disinstalla un'app con provisioning in un dispositivo, Windows attualmente non disinstalla l'app anche per gli utenti. 



## <a name="improvements-to-the-surface-dashboard"></a>Miglioramenti al dashboard di Surface
<!--1358654-->
Questa versione include i miglioramenti seguenti al [dashboard di Surface](../clients/manage/surface-device-dashboard.md):
- Il dashboard di Surface ora visualizza un elenco di dispositivi pertinenti quando vengono selezionate le sezioni del grafico.
   - Facendo clic sul riquadro **Percentuale di dispositivi Surface** viene aperto un elenco di dispositivi Surface.
   - Facendo clic su una barra nel riquadro **Prime cinque versioni di firmware** viene aperto un elenco di dispositivi Surface con quella versione di firmware specifica.
- Quando si visualizzano questi elenchi di dispositivi dal dashboard di Surface, è possibile fare clic con il pulsante destro del mouse su un dispositivo ed eseguire azioni comuni.



## <a name="hardware-inventory-default-unit-revision"></a>Revisione dell'unità predefinita di inventario hardware
<!--514442-->
In [Configuration Manager versione 1710](../plan-design/changes/whats-new-in-version-1710.md#site-infrastructure) l'unità predefinita usata in molte visualizzazioni Rapporti è passata da megabyte (MB) a gigabyte (GB). A causa dei [miglioramenti all'inventario hardware per i valori interi di grandi dimensioni](capabilities-in-technical-preview-1805.md#improvement-to-hardware-inventory-for-large-integer-values) e in base alle opinioni dei clienti, l'unità predefinita ora è di nuovo MB.



## <a name="next-steps"></a>Passaggi successivi
Per informazioni sull'installazione o l'aggiornamento del ramo Technical Preview, vedere [Technical Preview per Configuration Manager](technical-preview.md).