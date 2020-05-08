---
title: Funzionalità nella Technical Preview 1601
titleSuffix: Configuration Manager
description: Informazioni sulle funzionalità disponibili nella versione Technical Preview 1601 per Configuration Manager.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: aae1cf2f-2c04-4f68-a03a-f4a925433c09
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: ed3f53b6e2e9557def20fc459dfcf4641b0e396d
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905832"
---
# <a name="capabilities-in-technical-preview-1601-for-configuration-manager"></a>Funzionalità della versione Technical Preview 1601 per Configuration Manager

*Si applica a: Configuration Manager (Technical Preview Branch)*

Questo articolo presenta le funzionalità disponibili nella Technical Preview per Configuration Manager versione 1601. È possibile installare questa versione per aggiornare e aggiungere nuove funzionalità al sito di Technical Preview di Configuration Manager.      Prima di installare questa versione Technical Preview, consultare l'argomento introduttivo [Technical Preview per Center Configuration Manager](../../core/get-started/technical-preview.md) per acquisire familiarità con i requisiti generali e con le limitazioni per l'uso di una versione Technical Preview, con le modalità di aggiornamento tra le versioni e con le modalità per offrire commenti e suggerimenti sulle funzionalità di una versione Technical Preview.  

 **Problemi noti di questa versione Technical Preview:**  

-   quando di gestiscono le **Opzioni di aggiornamento client** per alzare il livello di un client di pre-produzione a client di produzione, il testo della casella di controllo indica una versione client zero (0) invece del numero effettivo della build client. La versione corretta del client di pre-produzione è indicata nell'area sopra questa opzione e corrisponde alla versione del client alzato di livello a client di produzione quando si seleziona questa opzione.  

-   Quando si esegue l'aggiornamento alla versione Technical Preview 1601 e si sceglie di testare il client di Configuration Manager in una raccolta di pre-produzione, il pacchetto client per la raccolta non verrà aggiornato. Questo problema riguarda solo la Technical Preview 1601.  

     Per una soluzione alternativa a questo problema, effettuare una delle operazioni seguenti:  

    -   Eseguire lo script SQL seguente nel database del sito primario:  

        ``` SQL
        DECLARE @PilotingPkgID NVARCHAR(8)  

        SELECT @PilotingPkgID = PilotingPackageID FROM ClientDeploymentSettings  

        MERGE INTO PkgServers_G AS T  
        USING (  
            SELECT @PilotingPkgID AS PkgID, NALPath, SiteCode, SiteName, SourceSite, RefreshTrigger, UpdateMask, [Action]  
            FROM PkgServers_G WHERE PkgID IN (SELECT UpgradePackageID FROM ClientDeploymentSettings)  
            ) AS S  
        ON T.PkgID = S.PkgID and T.NALPath = S.NALPath  

        WHEN NOT MATCHED THEN  
            INSERT (PkgID, NALPATH, SiteCode, SiteName, SourceSite, LastRefresh, RefreshTrigger, UpdateMask, [Action])  
            VALUES (S.PkgID, S.NALPath, S.SiteCode, S.SiteName, S.SourceSite, GetUTCDate(), S.RefreshTrigger, S.UpdateMask, S.[Action])  
        ;  

        ```  

    -   Aggiungere un nuovo ruolo del sistema del sito del punto di distribuzione al sito lab. Il nuovo punto di distribuzione aggiornerà la raccolta di pre-produzione con il nuovo pacchetto client.  

**Di seguito sono riportate le nuove funzionalità disponibili con questa versione.**  

##  <a name="improvements-to-microsoft-intune-integration"></a><a name="bkmk_hybrid1"></a> Miglioramenti dell'integrazione di Microsoft Intune  
Nella Technical Preview 1601 è stato aggiunto il supporto delle funzionalità seguenti:  

### <a name="improvements-to-conditional-access"></a>Miglioramenti per l'accesso condizionale  

-   **Supporto dell'accesso condizionale per i PC gestiti da Configuration Manager**  

     È ora possibile impostare criteri di accesso condizionale per i PC gestiti da Configuration Manager, che richiedono che i PC siano conformi ai criteri di conformità per accedere ai servizi Exchange Online e SharePoint Online.  Con questa nuova funzionalità, è anche possibile registrare i PC in Azure AD tramite i criteri di conformità, oltre a monitorare la registrazione in Azure AD e generare report corrispondenti.  

    > [!NOTE]  
    >  L'accesso condizionale non è ancora supportato in Windows 10.  

    L'elenco seguente include i prerequisiti per usare questa funzionalità:  

    -   Sottoscrizione di Azure Active Directory Premium e ADFS Sync.  

    -   Sottoscrizione di Microsoft Intune. La sottoscrizione di Microsoft Intune deve essere configurata nella console di Configuration Manager.  

    -   [Prerequisiti per la registrazione automatica in Azure AD](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1).  

    Per usare l'opzione, è necessario creare un criterio di conformità in Configuration Manager con le regole specifiche descritte di seguito e impostare un criterio di accesso condizionale nella console di Intune.  Inoltre, per assicurarsi che l'accesso sia consentito solo ai PC conformi, è necessario impostare il requisito PC Windows per l'opzione **I dispositivi devono essere conformi**. Di seguito sono descritte le regole dei criteri di conformità applicabili ai PC gestiti da Configuration Manager.  

    -   **Richiedi la registrazione in Azure Active Directory:** questa regola controlla se il dispositivo dell'utente è stato aggiunto all'area di lavoro in Azure AD e in caso contrario il dispositivo viene registrato automaticamente in Azure AD. La registrazione automatica è supportata solo in Windows 8.1. Per i PC con Windows 7, distribuire un file MSI per eseguire la registrazione automatica. Per altre informazioni, vedere [qui](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1).  

    -   **Tutti gli aggiornamenti richiesti installati con una scadenza precedente a un determinato numero di giorni:** questa regola controlla se il dispositivo dell'utente ha tutti gli aggiornamenti necessari (specificati nella regola **Richiedi aggiornamenti automatici**) entro la scadenza e il periodo di tolleranza specificati dall'utente e installa automaticamente eventuali aggiornamenti necessari in sospeso.  

    -   **Richiedi crittografia unità BitLocker:** questo è un controllo per verificare se l'unità principale (ad esempio, C:\\) nel dispositivo è crittografata con BitLocker. Se la crittografia Bitlocker non è attivata nel dispositivo primario, l'accesso alla posta elettronica e ai servizi di SharePoint è bloccato.  

    -   **Richiedi antimalware:** questo è un controllo per verificare se il software antimalware (System Center Endpoint Protection o solo Windows Defender) è abilitato e in esecuzione.  
         Se non è abilitato, l'accesso alla posta elettronica e ai servizi di SharePoint è bloccato.  

    Gli utenti finali bloccati a causa di non conformità visualizzeranno le informazioni di conformità in Software Center e verrà avviata una nuova valutazione dei criteri dopo la risoluzione dei problemi di conformità.  

-   **Accesso condizionale con il servizio di attestazione dell'integrità** È ora possibile limitare l'accesso alla posta elettronica e ai servizi di Office 365 in base all'integrità dei dispositivi, come segnalato dal servizio di attestazione dell'integrità.  Inoltre, i dispositivi gestiti da Intune sono inclusi nei report sull'integrità del dispositivo.  

    È stata aggiunta una nuova regola di conformità alla console di Configuration Manager che consente di specificare se l'accesso deve essere consentito o negato ai dispositivi in base al loro stato di integrità.  Per creare questa regola, aprire la **Creazione guidata criteri di conformità** e aggiungere una nuova regola.  Selezionare la condizione **Segnalato come integro dal servizio di attestazione dell'integrità** e impostare il valore su **True**.  Questo garantirà che solo i dispositivi segnalati come integri avranno accesso alle risorse aziendali. Per informazioni dettagliate sul servizio di attestazione dell'integrità e su come viene segnalata l'integrità dei dispositivi in Intune, vedere [Device Health Attestation](capabilities-in-technical-preview-1512.md#bkmk_devicehealth) (Attestazione dell'integrità dei dispositivi).  

-   **Nuove impostazioni dei criteri di conformità:** le nuove impostazioni dei criteri di conformità consentono di migliorare la sicurezza e la protezione nei dispositivi usati per accedere alla posta elettronica aziendale e ai servizi di SharePoint:  

    -   **Richiedi aggiornamenti automatici:** è possibile richiedere ai dispositivi con Windows 8.1 o versione successiva di consentire l'installazione automatica degli aggiornamenti e anche di specificare la classe degli aggiornamenti installati.  È possibile scegliere di installare solo gli aggiornamenti contrassegnati come importanti o tutti gli aggiornamenti consigliati.  

         Per creare una regola per gli aggiornamenti automatici, aprire la **Creazione guidata criteri di conformità** e aggiungere una nuova regola.  Selezionare **Classificazione minima aggiornamenti richiesti** come condizione e impostare l'opzione su uno dei valori disponibili: **Nessuno**, **Consigliati** e **Importanti**.  

        -   **Nessuno:** gli aggiornamenti non vengono installati automaticamente.  

        -   **Consigliati:** vengono installati tutti gli aggiornamenti consigliati  

        -   **Importanti:** vengono installati solo gli aggiornamenti classificati come importanti.  

    -   **Richiedi una password per sbloccare i dispositivi mobili:** quando questa opzione è impostata su **Sì**, gli utenti finali devono immettere una password per poter accedere al dispositivo.  

         Per creare una regola per la password con cui sbloccare i dispositivi mobili, aprire la **Creazione guidata criteri di conformità** e aggiungere una nuova regola. Selezionare **Richiedi una password per sbloccare un dispositivo inattivo** come condizione e impostare il valore su **True**.  

    -   **Minuti di inattività prima che venga richiesta la password:**  Specifica il tempo di inattività prima che l'utente debba immettere nuovamente la password.  

         Per creare questa regola, aprire la **Creazione guidata criteri di conformità** e aggiungere una nuova regola. Selezionare **Minuti di inattività prima che venga richiesta la password** come condizione e impostare l'opzione su uno dei valori disponibili: 1 minuto, 5 minuti, 15 minuti, 30 minuti, 1 ora.  

-   **Sostituzione regola predefinita - Consenti sempre ai dispositivi registrati in Intune e conformi di accedere a Exchange locale:**  

     Quando si seleziona questa opzione, i dispositivi registrati in Intune e conformi ai criteri di conformità possono accedere a Exchange locale. Questa regola sostituisce la regola predefinita, ossia anche se si definisce per la regola predefinita l'impostazione per la quarantena o il blocco dell'accesso, i dispositivi registrati e conformi potranno accedere a Exchange locale.  
     Usare questa impostazione quando si vuole che i dispositivi registrati e conformi abbiano sempre accesso alla posta elettronica tramite Exchange locale.  

     Questa impostazione è supportata nelle piattaforme seguenti:  Windows Phone 8 e versioni successive, iOS 6 e versioni successive. Android 4.0 e versioni successive, Samsung KNOX Standard 4.0 e versioni successive.  

     Per usare questa opzione, vedere la pagina **Generale** della **Configurazione guidata dei criteri di accesso condizionale** per Exchange locale.  

##  <a name="client-online-status"></a><a name="bkmk_clientStatus"></a> Stato online del client  
A partire dalla versione Technical Preview 1601, è possibile appurare rapidamente se un client è online o offline nella console di Configuration Manager. Grazie alle icone e alle colonne aggiornate negli elenchi di dispositivi della console, è possibile valutare lo stato dei client nell'ambiente in uso per identificare aree problematiche e altri problemi che richiedono attenzione.  

Un client è online se è attualmente connesso a un ruolo del sistema del sito del punto di gestione di Configuration Manager. Fino a quando il punto di gestione riceve messaggi di tipo ping dal client, il relativo stato è online. Se il punto di gestione non riceve un messaggio per circa 5 minuti, lo stato del client passa a offline.  

### <a name="icons-for-client-status"></a>Icone per lo stato del client  

|||  
|-|-|  
|![icona di stato online per i client](media/online-status-icon.png)|Il client è online.|  
|![icona di stato offline per i client](media/offline-status-icon.png)|Il client è offline.|  
|![icona di stato sconosciuto per i client](media/unknown-status-icon.png)|Lo stato del client è sconosciuto.|  

### <a name="prerequisites"></a>Prerequisiti  
 Non ci sono prerequisiti per lo stato online del client. È possibile iniziare a usarlo subito dopo aver installato Configuration Manager Technical Preview 1601.  

### <a name="limitations"></a>Limitazioni  
 Lo stato online del client è disponibile solo per i computer Windows con il client di Configuration Manager installato. Lo stato online del client non è supportato per i computer Mac, Linux o UNIX o per i dispositivi gestiti con Gestione dispositivi mobili locali.  

### <a name="to-view-client-online-status"></a>Per visualizzare lo stato online del client  

1. Nella console di Configuration Manager fare clic su **Asset e conformità > Panoramica > Dispositivi**.  

2. Fare clic con il pulsante destro del mouse nell'intestazione di colonna e quindi fare clic su uno dei campi dello stato online del client per aggiungerlo alla visualizzazione del dispositivo. I campi sono  

   -   **Stato online dispositivo** indica se il client è attualmente online o offline.  

   -   **Ora ultimo stato online** indica quando lo stato online del client è cambiato da offline a online.  

   -   **Ora ultimo stato offline** indica quando lo stato è cambiato da online a offline.  

   Per visualizzare le modifiche più recenti allo stato del client, aggiornare la console.  

##  <a name="improvements-to-application-management"></a><a name="bkmk_appmgmt1601"></a> Miglioramenti per la gestione delle applicazioni  
 Nella Technical Preview 1601 è stato aggiunto il supporto delle funzionalità seguenti:  

### <a name="manage-volume-purchased-apps-for-ios-devices"></a>Gestione delle app acquistate tramite Volume Purchase Program per dispositivi iOS  
 Alcuni App Store consentono di acquistare più licenze per un'app da eseguire nell'azienda. In questo modo, è possibile ridurre il sovraccarico amministrativo associato al monitoraggio di più copie delle app acquistate.  

 Configuration Manager consente ora di gestire le app acquistate con tale programma tramite l'importazione delle informazioni di licenza dall'App Store e la verifica del numero di licenze utilizzate.  


### <a name="ios---app-configuration-for-applicationsbr-hybrid"></a>iOS - Configurazione delle applicazioni<br />Strategia ibrida  
 Alcune applicazioni iOS supportano impostazioni di pre-configurazione, come il server o il database a cui deve connettersi l'applicazione. Configuration Manager supporta ora la distribuzione di criteri di configurazione dell'app nel dispositivo che consentono all'utente di usare immediatamente l'app senza dover conoscere queste informazioni. Gli sviluppatori devono abilitare questa funzionalità nelle proprie app.  

 Un numero limitato di app rilasciate pubblicamente supporta attualmente le impostazioni di pre-configurazione. È anche possibile che siano disponibili app line-of-business sviluppate internamente che supportano queste impostazioni.  

#### <a name="prerequisites-for-this-scenario"></a>Prerequisiti per questo scenario  

-   È necessario aver aggiunto una sottoscrizione di Microsoft Intune a Configuration Manager.  

-   È necessario aver aggiunto un certificato APN Apple valido alla sottoscrizione di Intune.  

-   È necessario avere distribuito un'applicazione iOS che supporta la configurazione dell'applicazione.  

#### <a name="try-it-out"></a>Verifica  
 Una volta soddisfatti i prerequisiti sopra indicati, è necessario creare un'applicazione Configuration Manager che usa un tipo di distribuzione iOS. L'app usata deve supportare la configurazione dell'applicazione. Fare riferimento alla documentazione del fornitore dell'applicazione per informazioni su quali elementi specifici (coppie nome/valore) è possibile configurare.  

 Associare quindi i criteri di configurazione dell'app al tipo di distribuzione iOS durante la distribuzione di app. È anche possibile distribuire i criteri dal nodo **Criteri di configurazione dell'app**, selezionando un'app e una raccolta esistente come destinazione.  

 Prova a completare le attività seguenti, quindi usa le informazioni relative a commenti e suggerimenti nella parte superiore di questo argomento per comunicare i risultati:  

-   Se è disponibile un'app iOS che supporta la configurazione dell'app, consultare la documentazione del fornitore dell'app per trovare le coppie nome/valore che è necessario specificare per configurare l'applicazione.  

-   Avviare la procedura guidata **Crea criteri di configurazione app**. Nella pagina **Criteri iOS** della procedura guidata provare ad aggiungere le coppie nome/valore riportate nella documentazione del fornitore dell'app oppure importare un file XML contenente i valori richiesti.  

-   Nella **Distribuzione guidata del software**, nella pagina **Criteri di configurazione dell'app**, associare i criteri di configurazione dell'app creati a un tipo di distribuzione compatibile dall'applicazione.  

##  <a name="improvements-to-compliance-settings"></a><a name="bkmk_compliance1601"></a> Miglioramenti per le impostazioni di conformità  
 Nella Technical Preview 1601 è stato aggiunto il supporto delle funzionalità seguenti:  

### <a name="microsoft-edge-browser-settings"></a>Impostazioni del browser Microsoft Edge  
 Sono state aggiunte nuove impostazioni per il browser Microsoft Edge all'elemento di configurazione **Windows 8.1 e Windows 10** (le impostazioni si applicano solo ai dispositivi Windows 10).  

 Per visualizzare le nuove impostazioni, scegliere **Microsoft Edge** nella pagina **Impostazioni dispositivo** dell'elemento di configurazione della **Creazione guidata dell'elemento di configurazione**.  

 Per altre informazioni, vedere [Come creare elementi di configurazione per dispositivi Windows 8.1 e Windows 10 gestiti senza il client Configuration Manager](../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  

### <a name="compliance-settings-for-windows-10-team-devices"></a>Impostazioni di conformità per i dispositivi Windows 10 Team  
 Usare le nuove impostazioni di conformità per configurare i dispositivi che eseguono Windows 10 Team, ad esempio dispositivi Surface Hub.  

 Per visualizzare le nuove impostazioni, scegliere **Windows 10 Team** nella pagina **Impostazioni dispositivo** dell'elemento di configurazione della **Creazione guidata dell'elemento di configurazione**.  

 Per altre informazioni, vedere [Come creare elementi di configurazione per dispositivi Windows 8.1 e Windows 10 gestiti senza il client Configuration Manager](../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  

### <a name="android---kiosk-mode-for-samsung-knox-standardbr-hybrid"></a>Android - Modalità tutto schermo per Samsung KNOX Standard<br />Strategia ibrida  
 La modalità tutto schermo consente di bloccare un dispositivo per consentire solo l'uso di alcune funzionalità. Ad esempio, è possibile consentire a un dispositivo di eseguire solo un'app gestita specificata o disabilitare i pulsanti del volume in un dispositivo. Queste impostazioni potrebbero essere usate per un modello demo di un dispositivo o per un dispositivo dedicato all'esecuzione di una sola funzione, ad esempio un dispositivo POS. Queste impostazioni non sono disponibili per i dispositivi Samsung KNOX Standard nell'elemento di configurazione **Windows 8.1 e Windows 10** (le impostazioni si applicano solo ai dispositivi Windows 10).  

 Per visualizzare le nuove impostazioni, scegliere **Modalità tutto schermo - Samsung KNOX** nella pagina **Impostazioni dispositivo** dell'elemento di configurazione della **Creazione guidata dell'elemento di configurazione**.  

 Per altre informazioni, vedere [Come creare elementi di configurazione per dispositivi Windows 8.1 e Windows 10 gestiti senza il client Configuration Manager](../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  
