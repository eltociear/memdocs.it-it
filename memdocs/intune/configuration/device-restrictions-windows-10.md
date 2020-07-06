---
title: Impostazioni relative alle restrizioni dei dispositivi per Windows 10 in Microsoft Intune - Azure | Microsoft Docs
description: Visualizzare un elenco di tutte le impostazioni e le relative descrizioni per la creazione di limitazioni per i dispositivi in Windows 10 e versioni successive. Usare queste impostazioni in un profilo di configurazione per controllare screenshot, requisiti per le password, impostazioni della modalità tutto schermo, app nello Store, browser Microsoft Edge, Microsoft Defender, accesso al cloud, menu Start e altro in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/30/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6f4fd580a2e36a1cf7a29766c7a5e325e17fc528
ms.sourcegitcommit: f3f2632df123cccd0e36b2eacaf096a447022b9d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85591069"
---
# <a name="windows-10-and-newer-device-settings-to-allow-or-restrict-features-using-intune"></a>Impostazioni dei dispositivi Windows 10 (e versioni successive) per consentire o limitare l'uso delle funzionalità tramite Intune

Questo articolo descrive le diverse impostazioni che è possibile controllare nei dispositivi Windows 10 e versioni successive. Usare queste impostazioni nella soluzione di gestione di dispositivi mobili (MDM) per abilitare o disabilitare funzionalità, impostare regole per le password, personalizzare la schermata di blocco, usare Microsoft Defender e altro ancora.

Queste impostazioni vengono aggiunte a un profilo di configurazione del dispositivo in Intune e quindi assegnate o distribuite ai dispositivi Windows 10.

> [!Note]
> Non tutte le opzioni sono disponibili in tutte le edizioni di Windows. Per informazioni sulle edizioni supportate, vedere [Policy CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-configuration-service-provider) (Provider di servizi di configurazione dei criteri) (viene aperto un altro sito Web Microsoft).
>  
> La maggior parte delle impostazioni configurabili in un profilo di restrizioni dei dispositivi Windows 10 viene distribuita a livello di dispositivo. I criteri distribuiti a gruppi di utenti sono effettivi sia per l'utente di destinazione sia per gli altri utenti che accedono successivamente al dispositivo e hanno una licenza di Intune.

## <a name="before-you-begin"></a>Prima di iniziare

[Creare un profilo di restrizioni dei dispositivi Windows 10](device-restrictions-configure.md#create-the-profile).

## <a name="app-store"></a>App Store

Queste impostazioni usano il [provider di servizi di configurazione dei criteri relativi ad ApplicationManagement](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement), che elenca anche le edizioni di Windows supportate.

- **App Store (solo dispositivi mobili)** : **Blocca** impedisce agli utenti di accedere all'App Store nei dispositivi mobili. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di accedere all'App Store.
- **Aggiorna automaticamente le app dallo Store**: **Blocca** impedisce l'installazione automatica degli aggiornamenti da Microsoft Store. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'aggiornamento automatico delle app installate da Microsoft Store.

  [ApplicationManagement/AllowAppStoreAutoUpdate CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowappstoreautoupdate)

- **Installazione di app attendibile**: scegliere se è possibile installare app non Microsoft Store, operazione nota anche come sideload. Il termine sideload indica l'installazione e poi l'esecuzione e il test di un'app non certificata da Microsoft Store. Ad esempio, un'app interna usata solo dall'azienda. Le opzioni disponibili sono:
  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione.
  - **Blocca**: impedisce il sideload. Non è possibile installare app non Microsoft Store.
  - **Consenti**: consente il sideload. È possibile installare app non Microsoft Store.

- **Sblocco dallo sviluppatore**: consente agli utenti di modificare le impostazioni per gli sviluppatori Windows, ad esempio consentire il sideload delle app. Le opzioni disponibili sono:
  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione.
  - **Blocca**: impedisce la modalità sviluppatore e il sideload delle app.
  - **Consenti**: consente la modalità sviluppatore e il sideload delle app.

  In [Abilitare il dispositivo per lo sviluppo](https://docs.microsoft.com/windows/uwp/get-started/enable-your-device-for-development) sono disponibili altre informazioni su questa funzionalità.
  
  [ApplicationManagement/AllowAllTrustedApps CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowalltrustedapps)

- **Dati app utente condivisi**: scegliere **Consenti** per condividere i dati dell'applicazione tra utenti diversi dello stesso dispositivo e con altre istanze dell'app. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe impedire la condivisione dei dati con altri utenti e altre istanze della stessa app.

  [ApplicationManagement/AllowSharedUserAppData CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowshareduserappdata)

- **Usa solo lo Store privato**: **Consenti** consente solo il download delle app da uno Store privato e non dallo Store pubblico, incluso un catalogo al dettaglio. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire il download delle app da uno Store privato e da uno Store pubblico.

  [ApplicationManagement/RequirePrivateStoreOnly CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-requireprivatestoreonly)

- **Avvio di app originate dallo Store**: **Blocca** disabilita tutte le app preinstallate nel dispositivo o scaricate da Microsoft Store. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'apertura di queste app.

  [ApplicationManagement/DisableStoreOriginatedApps CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-disablestoreoriginatedapps)

- **Installa i dati dell'app nel volume di sistema**: **Blocca** impedisce alle app di archiviare dati nel volume di sistema del dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire alle app di archiviare i dati nel volume del disco di sistema.

  [ApplicationManagement/RestrictAppDataToSystemVolume CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-restrictappdatatosystemvolume)

- **Installa le app nell'unità di sistema**: **Blocca** impedisce l'installazione delle app nell'unità di sistema nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'installazione delle app nell'unità di sistema.

  [ApplicationManagement/RestrictAppToSystemVolume CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-restrictapptosystemvolume)

- **Game DVR (solo desktop)** : **Blocca** disabilita la registrazione e la trasmissione di giochi di Windows. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire la registrazione e la trasmissione di giochi.

  [ApplicationManagement/AllowGameDVR CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowgamedvr)

- **App solo dallo Store**: questa impostazione determina l'esperienza utente quando gli utenti installano app da posizioni diverse da Microsoft Store. Non impedisce l'installazione di contenuto da dispositivi USB, condivisioni di rete o altre origini non Internet. Usare un browser attendibile per assicurarsi che queste protezioni funzionino come previsto.

  Le opzioni disponibili sono:

  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di installare app da posizioni diverse da Microsoft Store, incluse le app definite in altre impostazioni di criteri.  
  - **Ovunque**: disattiva i consigli per le app e consente agli utenti di installare le app da qualsiasi percorso.  
  - **Solo Store**: La finalità è impedire che i contenuti dannosi influiscano sui dispositivi degli utenti durante il download del contenuto eseguibile da Internet. Quando gli utenti tentano di installare app da Internet, l'installazione è bloccata. Gli utenti visualizzano un messaggio che consiglia di scaricare le app dal Microsoft Store.
  - **Consigli**: quando si installa un'app dal Web che è disponibile in Microsoft Store, gli utenti visualizzano un messaggio che consiglia il download dallo Store.  
  - **Preferenza allo Store**: avvisa gli utenti quando installano app da posizioni diverse da Microsoft Store.

  [Provider di servizi di configurazione SmartScreen/EnableAppInstallControl](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-smartscreen#smartscreen-enableappinstallcontrol)

- **Controllo utente sulle installazioni**: **Blocca** impedisce agli utenti di modificare le opzioni di installazione generalmente riservate agli amministratori di sistema, ad esempio l'immissione della directory per installare i file. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, Windows Installer potrebbe impedire agli utenti di modificare queste opzioni di installazione. Alcune delle funzionalità di sicurezza di Windows Installer vengono ignorate.

  [ApplicationManagement/MSIAllowUserControlOverInstall CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-msiallowusercontroloverinstall)

- **Installazione di app con privilegi elevati**: **Blocca** indica a Windows Installer di usare le autorizzazioni elevate per installare qualsiasi programma nel sistema. Questi privilegi vengono estesi a tutti i programmi. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema potrebbe applicare le autorizzazioni dell'utente corrente quando installa programmi non offerti o distribuiti da un amministratore di sistema.

  [ApplicationManagement/MSIAlwaysInstallWithElevatedPrivileges CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-msialwaysinstallwithelevatedprivileges)

- **App di avvio**: immettere un elenco di app da aprire dopo l'accesso di un utente al dispositivo. Assicurarsi di usare un elenco delimitato da punto e virgola di nomi della famiglia di pacchetti (PFN) di applicazioni Windows. Per il corretto funzionamento di questo criterio, il manifesto nelle app Windows deve usare un'attività di avvio.

  [ApplicationManagement/LaunchAppAfterLogOn CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-launchappafterlogon)

## <a name="cellular-and-connectivity"></a>Rete cellulare e connettività

Queste impostazioni usano i provider di servizi di configurazione per i [criteri di connettività](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-connectivity) e i [criteri Wi-Fi](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-wifi), che elencano anche le edizioni di Windows supportate.

- **Canale per rete dati**: scegliere se gli utenti possono usare i dati, ad esempio esplorare il Web, quando sono connessi a una rete cellulare. Le opzioni disponibili sono:
  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione. Gli utenti possono disattivarla.
  - **Blocca**: non consente il canale per rete dati. Questa opzione non può essere attivata dagli utenti.
  - **Consenti (non modificabile)** : consente il canale per rete dati. Questa opzione non può essere disattivata dagli utenti.

- **Dati in roaming**: **Blocca** impedisce il roaming della rete dati nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, quando si accede ai dati il roaming tra reti è consentito.
- **VPN nella rete cellulare**: **Blocca** impedisce al dispositivo di accedere a connessioni VPN quando è connesso a una rete cellulare. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire alla rete VPN di usare qualsiasi connessione, inclusa la rete cellulare.
- **Roaming VPN nella rete cellulare**: **Blocca** impedisce al dispositivo di accedere alle connessioni VPN durante il roaming in una rete cellulare. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire le connessioni VPN durante il roaming.
- **Servizio dispositivi connessi**: **Blocca** disabilita il componente CDP (Connected Devices Platform). Il componente CDP (Connected Devices Platform) consente l'individuazione e la connessione ad altri dispositivi (tramite Bluetooth/LAN o il cloud) per supportare l'avvio di app remote, la messaggistica remota, le sessioni di app remote e altre esperienze che coinvolgono più dispositivi. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire il servizio dei dispositivi connessi, che abilita l'individuazione e la connessione ad altri dispositivi Bluetooth.
- **NFC**: **Blocca** impedisce le funzionalità NFC (Near Field Communication). Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di abilitare e configurare le funzionalità NFC nel dispositivo.
- **Wi-Fi**: **Blocca** impedisce agli utenti di abilitare, configurare e usare le connessioni Wi-Fi nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire le connessioni Wi-Fi.
- **Connetti automaticamente a hotspot Wi-Fi**: **Blocca** impedisce ai dispositivi di connettersi automaticamente agli hotspot Wi-Fi. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire ai dispositivi di connettersi automaticamente agli hotspot Wi-Fi gratuiti e accettare automaticamente termini e condizioni per la connessione.
- **Configurazione Wi-Fi manuale**: **Blocca** impedisce ai dispositivi di connettersi a una rete Wi-Fi all'esterno delle reti installate in server MDM. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di aggiungere e configurare SSID di rete per connessioni Wi-Fi personali.
- **Intervallo di analisi Wi-Fi**: immettere la frequenza con cui i dispositivi ricercano le reti Wi-Fi. Immettere un valore compreso tra 1 (ricerca più frequente) e 500 (ricerca meno frequente). Il valore predefinito è `0` (zero).

### <a name="bluetooth"></a>Bluetooth

Queste impostazioni usano il [provider di servizi di configurazione per i criteri Bluetooth](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth), che elenca anche le edizioni di Windows supportate.

- **Bluetooth**: **Blocca** impedisce agli utenti di abilitare Bluetooth. L'impostazione **Non configurata** (predefinita) consente Bluetooth nel dispositivo.
- **Individuabilità di Bluetooth**: **Blocca** impedisce che il dispositivo sia individuabile da altri dispositivi Bluetooth. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire ad altri dispositivi Bluetooth, ad esempio le cuffie, di individuare il dispositivo.

  [Bluetooth/AllowDiscoverableMode CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowdiscoverablemode)

- **Pre-associazione Bluetooth**: **Blocca** impedisce a dispositivi Bluetooth specifici l'associazione automatica a un dispositivo host. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'associazione automatica al dispositivo host.

  [Bluetooth/AllowPrepairing CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowprepairing)

- **Annunci con Bluetooth**: **Blocca** impedisce al dispositivo di inviare annunci Bluetooth. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire al dispositivo di inviare annunci Bluetooth.

  [Bluetooth/AllowAdvertising CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowadvertising)

- **Connessioni di prossimità Bluetooth**: **Blocca** impedisce a un utente del dispositivo di usare Associazione rapida e altri scenari basati sulla prossimità. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire al dispositivo di inviare annunci Bluetooth.

  [CSP Bluetooth/AllowPromptedProximalConnections](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowpromptedproximalconnections)

- **Servizi Bluetooth consentiti**: **Aggiungi** consente di aggiungere un elenco di servizi e profili Bluetooth consentiti in forma di stringhe esadecimali, ad esempio `{782AFCFC-7CAA-436C-8BF0-78CD0FFBD4AF}`.

  In [ServicesAllowedList usage guide](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#servicesallowedlist-usage-guide) (Guida all'utilizzo di ServicesAllowedList) sono disponibili altre informazioni sull'elenco di servizi.

  [Bluetooth/ServicesAllowedList CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-servicesallowedlist)

## <a name="cloud-and-storage"></a>Cloud e risorse di archiviazione

Queste impostazioni usano il [provider di servizi di configurazione per i criteri relativi agli account](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-accounts), che elenca anche le edizioni di Windows supportate.

> [!IMPORTANT]
> Il blocco o la disabilitazione di queste impostazioni dell'account Microsoft può influire sugli scenari di registrazione che richiedono l'accesso ad Azure AD da parte degli utenti. Ad esempio, si usa la modalità [White Glove per Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/white-glove). In genere, gli utenti visualizzano una finestra di accesso di Azure AD. Quando queste impostazioni sono impostate su **Blocca** o **Disabilita**, è possibile che l'opzione di accesso ad Azure AD non venga visualizzata. Viene invece richiesto agli utenti di accettare il contratto di licenza e creare un account locale e questo potrebbe non essere il risultato sperato.

- **Account Microsoft**: **Blocca** impedisce agli utenti di associare un account Microsoft al dispositivo. **Blocca** potrebbe anche influire su alcuni scenari di registrazione che si basano sugli utenti per completare il processo di registrazione. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'aggiunta e l'uso di un account Microsoft.
- **Account non Microsoft**: **Blocca** impedisce agli utenti di aggiungere account non Microsoft tramite l'interfaccia utente. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di aggiungere account di posta elettronica che non sono associati a un account Microsoft.
- **Sincronizzazione delle impostazioni per l'account Microsoft**: **Blocca** impedisce che le impostazioni del dispositivo e delle app associate con un account Microsoft vengano sincronizzate fra i dispositivi. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire questa sincronizzazione.
- **Assistente per l'accesso all'account Microsoft**: Questo servizio del sistema operativo consente agli utenti di accedere al proprio account Microsoft. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di avviare e arrestare il servizio **Assistente per l'accesso all'account Microsoft** (wlidsvc).
  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di avviare e arrestare il servizio **Assistente per l'accesso all'account Microsoft** (wlidsvc).
  - **Disabilitato**: imposta il servizio Assistente per l'accesso di Microsoft (wlidsvc) su Disabilitato e impedisce agli utenti finali di avviarlo manualmente.

      **Disabilita** potrebbe anche influire su alcuni scenari di registrazione che si basano sugli utenti per completare la registrazione. Ad esempio, si usa la modalità [White Glove per Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/white-glove). In genere, gli utenti visualizzano una finestra di accesso di Azure AD. Quando è impostata su **Disabilita**, l'opzione di accesso Azure AD potrebbe non essere visualizzata. Viene invece richiesto agli utenti di accettare il contratto di licenza e creare un account locale e questo potrebbe non essere il risultato sperato.

## <a name="cloud-printer"></a>Stampante cloud

Queste impostazioni usano il [provider di servizi di configurazione per i criteri EnterpriseCloudPrint](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-enterprisecloudprint), che elenca anche le edizioni di Windows supportate.

- **URL di individuazione stampanti**: immettere l'URL per l'individuazione delle stampanti nel cloud. Immettere ad esempio `https://cloudprinterdiscovery.contoso.com`.
- **URL dell'autorità per l'accesso alle stampanti**: immettere l'URL dell'endpoint di autenticazione per l'acquisizione di token OAuth. Immettere ad esempio `https://azuretenant.contoso.com/adfs`.
- **GUID dell'app client nativa di Azure**: immettere l'identificatore univoco globale (GUID) dell'applicazione client autorizzata a ottenere token OAuth da OAuthAuthority. Immettere ad esempio `E1CF1107-FF90-4228-93BF-26052DD2C714`.
- **URI della risorsa del servizio di stampa**: immettere l'URI della risorsa OAuth per il servizio di stampa configurato nel portale di Azure. Immettere ad esempio `http://MicrosoftEnterpriseCloudPrint/CloudPrint`.
- **Numero massimo di stampanti da sottoporre a query**: immettere il numero massimo di stampanti da sottoporre a query. Il valore predefinito è `20`.
- **URI della risorsa del servizio di individuazione**: immettere l'URI della risorsa OAuth per il servizio di individuazione delle stampanti configurato nel portale di Azure. Immettere ad esempio `http://MopriaDiscoveryService/CloudPrint`.

> [!TIP]
> Dopo aver configurato [Hybrid Cloud Print di Windows Server](https://docs.microsoft.com/windows-server/administration/hybrid-cloud-print/hybrid-cloud-print-overview), è possibile configurare queste impostazioni e quindi eseguire la distribuzione ai dispositivi Windows.

## <a name="control-panel-and-settings"></a>Pannello di controllo e impostazioni

- **App Impostazioni**: **Blocca** impedisce agli utenti di accedere all'app Impostazioni di Windows. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di aprire l'app Impostazioni nel dispositivo.
  - **Sistema**: **Blocca** impedisce l'accesso all'area Sistema dell'app Impostazioni. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.
    - **Modifica delle impostazioni di risparmio energia e sospensione** (solo desktop): **Blocca** impedisce agli utenti di modificare le impostazioni di risparmio energia e sospensione del dispositivo. L'impostazione **Non configurata** (predefinita) consente agli utenti di modificare le impostazioni di risparmio energia e sospensione.
  - **Dispositivi**: **Blocca** impedisce l'accesso all'area Dispositivi dell'app Impostazioni nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.
  - **Rete e Internet**: **Blocca** impedisce l'accesso all'area Rete e Internet dell'app Impostazioni nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.
  - **Personalizzazione**: **Blocca** impedisce l'accesso all'area Personalizzazione dell'app Impostazioni nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.
  - **App**: **Blocca** impedisce l'accesso all'area App dell'app Impostazioni nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.
  - **Account**: **Blocca** impedisce l'accesso all'area Account dell'app Impostazioni nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.
  - **Ora e lingua**: **Blocca** impedisce l'accesso all'area Data/ora e lingua dell'app Impostazioni nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.
    - **Modifica dell'ora di sistema**: **Blocca** impedisce agli utenti di modificare le impostazioni di data e ora nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Gli utenti possono modificare queste impostazioni.
    - **Modifica delle impostazioni dell'area** (solo desktop): **Blocca** impedisce agli utenti di modificare le impostazioni dell'area del dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Gli utenti possono modificare queste impostazioni.
    - **Modifiche alle impostazioni della lingua (solo desktop)** : **Blocca** impedisce agli utenti di modificare le impostazioni della lingua del dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Gli utenti possono modificare queste impostazioni.

      [Provider di servizi di configurazione per i criteri relativi alle impostazioni](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-settings)

  - **Modalità di gioco**: **Blocca** impedisce l'accesso all'area Giochi dell'app Impostazioni nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.
  - **Accessibilità**: **Blocca** impedisce l'accesso all'area Accessibilità dell'app Impostazioni nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.
  - **Privacy**: **Blocca** impedisce l'accesso all'area Privacy dell'app Impostazioni nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.
  - **Aggiornamento e sicurezza**: **Blocca** impedisce l'accesso all'area Aggiornamento e sicurezza dell'app Impostazioni nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.

## <a name="display"></a>Schermo

Queste impostazioni usano il [provider di servizi di configurazione per i criteri relativi allo schermo](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-display), che elenca anche le edizioni di Windows supportate.

Il ridimensionamento DPI del programma GDI consente alle applicazioni non sensibili ai valori DPI di diventare sensibili ai valori DPI per monitor.

- **Attiva il ridimensionamento del programma GDI per le app**: **Aggiungi** consente di aggiungere le app legacy per cui attivare il ridimensionamento DPI del programma GDI. Ad esempio, immettere `filename.exe` o `%ProgramFiles%\Path\Filename.exe`.

  Il ridimensionamento DPI del programma GDI è attivato per tutte le applicazioni legacy nell'elenco.

- **Disattiva il ridimensionamento del programma GDI per le app**: **Aggiungi** consente di aggiungere le app legacy per cui disattivare il ridimensionamento DPI del programma GDI. Ad esempio, immettere `filename.exe` o `%ProgramFiles%\Path\Filename.exe`.

  Il ridimensionamento DPI del programma GDI è disattivato per tutte le applicazioni legacy nell'elenco.

È anche possibile **importare** un file CSV con l'elenco delle app.

## <a name="general"></a>Generale

Queste impostazioni usano il [provider di servizi di configurazione per i criteri relativi all'esperienza](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience), che elenca anche le edizioni di Windows supportate. 

- **Acquisizione di schermata** (solo dispositivi mobili): **Blocca** impedisce agli utenti di ottenere screenshot nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.
- **Copia e incolla (solo dispositivi mobili)** : **Blocca** impedisce agli utenti di eseguire operazioni Copia e Incolla tra app nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.
- **Annullamento manuale della registrazione**: **Blocca** impedisce agli utenti di eliminare l'account aziendale usando il pannello di controllo dell'area di lavoro nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.

  Questa impostazione dei criteri non è applicabile se il computer è stato aggiunto ad Azure AD e la registrazione automatica è abilitata.

- **Installazione manuale del certificato radice** (solo per dispositivi mobili): **Blocca** impedisce agli utenti di installare manualmente i certificati radice e i certificati CAP intermedi. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.
- **Fotocamera**: **Blocca** impedisce agli utenti di usare la fotocamera nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'accesso alla fotocamera del dispositivo.

  Intune gestisce solo l'accesso alla fotocamera del dispositivo. Non ha accesso alle immagini o ai video.

  [Provider di servizi di configurazione della fotocamera](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-camera)

- **Sincronizzazione dei file di OneDrive**: **Blocca** impedisce agli utenti di sincronizzare file in OneDrive dal dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.

  [System/DisableOneDriveFileSync CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-system#system-disableonedrivefilesync)

- **Archivi rimovibili**: **Blocca** impedisce agli utenti di usare dispositivi di archiviazione esterni, come schede SD, con il dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.
- **Georilevazione**: **Blocca** impedisce agli utenti di attivare servizi di georilevazione nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.

  [System/AllowLocation CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-system#system-allowlocation)

- **Internet condiviso**: **Blocca** impedisce la condivisione della connessione Internet nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.
- **Ripristino delle impostazioni predefinite del telefono**: **Blocca** impedisce agli utenti di cancellare o ripristinare le impostazioni predefinite del dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.
- **Connessione USB**: **Blocca** impedisce l'accesso ai dispositivi di archiviazione esterni tramite una connessione USB nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. I dispositivi di ricarica USB non sono interessati da questa impostazione.

  [Connectivity/AllowUSBConnection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-connectivity#connectivity-allowusbconnection)

- **Modalità antifurto** (solo per dispositivi mobili): **Blocca** impedisce agli utenti di selezionare le preferenze della modalità antifurto nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.
- **Cortana**: **Blocca** disabilita l'assistente vocale Cortana nel dispositivo. Quando Cortana è disattivata, gli utenti possono comunque eseguire una ricerca per trovare elementi nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire Cortana.

  [Experience/AllowCortana CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowcortana)

- **Registrazione vocale** (solo per dispositivi mobili): **Blocca** impedisce agli utenti di usare il registratore vocale nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire la registrazione vocale per le app.
- **Modifica del nome dispositivo** (solo dispositivi mobili): **Blocca** impedisce agli utenti di modificare il nome del dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.
- **Aggiungi pacchetti di provisioning**: **Blocca** impedisce all'agente di configurazione di runtime di installare pacchetti di provisioning nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.
- **Rimuovi i pacchetti di provisioning**: **Blocca** impedisce all'agente di configurazione di runtime di rimuovere pacchetti di provisioning dal dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.
- **Individuazione dei dispositivi**: **Blocca** impedisce l'individuazione di un dispositivo da parte di altri dispositivi. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.

  [Experience/AllowDeviceDiscovery](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowdevicediscovery)

- **Cambio modalità per l'attività** (solo dispositivi mobili): **Blocca** impedisce il cambio di modalità per l'attività nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.
- **Finestra di dialogo di errore per la scheda SIM** (solo dispositivi mobili): **Blocca** impedisce la visualizzazione di messaggi di errore nel dispositivo se non viene rilevata alcuna scheda SIM. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe visualizzare messaggi di errore.
- **Area Ink**: scegliere se e come l'utente accede all'area Ink. Le opzioni disponibili sono:
  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe attivare l'area Ink, che gli utenti sono autorizzati a usare sopra la schermata di blocco.
  - **Disabilitato nella schermata di blocco**: l'area Ink è abilitata e la funzionalità è attivata. Tuttavia, gli utenti non possono accedervi sopra la schermata di blocco.
  - **Disabilitato**: l'accesso all'area Ink è disabilitato. La funzionalità è disattivata.

  [Provider di servizi di configurazione dei criteri relativi a WindowsInkWorkspace](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-windowsinkworkspace)

- **Reimpostazione di Autopilot**: scegliere **Consenti** in modo che gli utenti con diritti amministrativi possano eliminare tutti i dati utente e tutte le impostazioni utente tramite **CTRL+tasto WINDOWS+R** nella schermata di blocco del dispositivo. Il dispositivo viene automaticamente riconfigurato e registrato di nuovo nella gestione. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe bloccare questa funzionalità.
- **Richiedi agli utenti di connettersi alla rete durante la configurazione del dispositivo**: scegliere **Rendi obbligatorio** in modo che il dispositivo si connetta a una rete prima di passare oltre la pagina Rete durante la configurazione di Windows. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di andare oltre la pagina Rete anche se non sono connessi a una rete.

  L'impostazione diventa effettiva alla successiva cancellazione o reimpostazione del dispositivo. Come per qualsiasi altra configurazione di Intune, è necessario che il dispositivo sia registrato e gestito da Intune al fine di ricevere le impostazioni di configurazione. Ma dopo che è stato registrato e che riceve i criteri, la reimpostazione del dispositivo determina l'applicazione dell'impostazione durante l'installazione di Windows successiva.

  [Provider di servizi di configurazione TenantLockdown](https://docs.microsoft.com/windows/client-management/mdm/tenantlockdown-csp)

- **Accesso diretto alla memoria**: **Blocca** consente di impedire l'accesso diretto alla memoria (Direct Memory Access, DMA) per tutte le porte downstream PCI collegabili a un sistema acceso finché un utente non accede a Windows. **Abilitato** (impostazione predefinita) consente l'accesso diretto alla memoria, anche quando un utente non è connesso.

  [CSP DataProtection/AllowDirectMemoryAccess](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-dataprotection#dataprotection-allowdirectmemoryaccess)

- **End processes from Task Manager** (Termina processi da Gestione attività): questa impostazione determina se gli utenti non amministratori possono usare Gestione attività per terminare le attività. **Blocca** impedisce agli utenti standard (non amministratori) di usare Gestione attività per terminare un processo o un'attività nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti standard di terminare un processo o un'attività usando Gestione attività.

  [TaskManager/AllowEndTask CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-taskmanager#taskmanager-allowendtask)

## <a name="locked-screen-experience"></a>Esperienza della schermata bloccata

- **Notifiche del centro notifiche (solo per dispositivi mobili)** : **Blocca** impedisce la visualizzazione delle notifiche del centro notifiche nella schermata di blocco del dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di scegliere quali app mostrano le notifiche nella schermata di blocco.

  [Provider di servizi di configurazione AboveLock/AllowActionCenterNotifications](https://msdn.microsoft.com/ie/dn904962(v=vs.94)#AboveLock_AllowActionCenterNotifications)

- **URL dell'immagine della schermata bloccata (solo desktop)** : immettere l'URL di un'immagine in formato JPG, JPEG o PNG da usare come sfondo della schermata di blocco di Windows. Immettere ad esempio `https://contoso.com/image.png`. Questa impostazione blocca l'immagine e non può essere modificata in un secondo momento.

  [Provider di servizi di configurazione Personalization/LockScreenImageUrl](https://docs.microsoft.com/windows/client-management/mdm/personalization-csp)

- **Timeout dello schermo configurabile dall'utente (solo dispositivi mobili)** : **Consenti** consente agli utenti di configurare il timeout dello schermo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe non concedere agli utenti questa opzione.

  [Provider di servizi di configurazione DeviceLock/AllowScreenTimeoutWhileLockedUserConfig](https://msdn.microsoft.com/ie/dn904962(v=vs.94)#DeviceLock_AllowScreenTimeoutWhileLockedUserConfig)

- **Cortana nella schermata di blocco** (solo desktop): **Blocca** impedisce agli utenti di interagire con Cortana quando il dispositivo si trova nella schermata di blocco. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'interazione con Cortana.

  [Provider di servizi di configurazione AboveLock/AllowCortanaAboveLock](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-abovelock#abovelock-allowcortanaabovelock)

- **Notifiche di tipo avviso popup nella schermata di blocco**: **Blocca** impedisce la visualizzazione delle notifiche di tipo avviso popup nella schermata di blocco del dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire queste notifiche.

  [Provider di servizi di configurazione AboveLock/AllowToasts](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-abovelock#abovelock-allowtoasts)

- **Timeout dello schermo (solo dispositivi mobili)** : impostare il tempo di attesa, in secondi, dal blocco dello schermo alla disattivazione dello schermo. I valori supportati sono compresi tra 11 e 1800. Ad esempio, immettere `300` per impostare il timeout di 5 minuti.

  [Provider di servizi di configurazione DeviceLock/ScreenTimeoutWhileLocked](https://msdn.microsoft.com/ie/dn904962(v=vs.94)#DeviceLock_ScreenTimeoutWhileLocked)

## <a name="messaging"></a>Messaggistica

Queste impostazioni usano il [provider di servizi di configurazione per i criteri relativi alla messaggistica](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-messaging), che elenca anche le edizioni di Windows supportate.

- **Sincronizzazione di messaggi (solo dispositivi mobili)** : **Blocca** disabilita il backup o il ripristino degli SMS e la sincronizzazione di messaggi tra i dispositivi Windows. La disabilitazione consente di evitare l'archiviazione delle informazioni in server fuori dal controllo dell'organizzazione. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di modificare queste impostazioni e di sincronizzare i messaggi.
- **MMS (solo dispositivi mobili)** : **Blocca** disabilita la funzionalità di invio e ricezione di MMS nel dispositivo. Le aziende possono usare questi criteri per disabilitare gli MMS nei dispositivi come parte dei requisiti di controllo o di gestione. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'invio e la ricezione di MMS.
- **RCS (solo dispositivi mobili)** : **Blocca** disabilita la funzionalità di invio e ricezione di RCS (Rich Communication Services) nel dispositivo. Le aziende possono usare questi criteri per disabilitare RCS nei dispositivi come parte dei requisiti di controllo o di gestione. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'invio e la ricezione di RCS.

## <a name="microsoft-edge-browser"></a>Browser Microsoft Edge

Queste impostazioni usano il [provider di servizi di configurazione per i criteri relativi al browser](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser), che elenca anche le edizioni di Windows supportate.

> [!NOTE]
> L'uso dei criteri del provider di servizi di configurazione per i criteri relativi al browser si applica a Microsoft Edge versione 45 e versioni precedenti. Per Microsoft Edge Enterprise versione 77 e successive, vedere [Configurare le impostazioni dei criteri di Microsoft Edge con Microsoft Intune](/DeployEdge/configure-edge-with-intune).

### <a name="use-microsoft-edge-kiosk-mode"></a>Usa la modalità tutto schermo di Microsoft Edge

Le impostazioni disponibili variano a seconda delle scelte effettuate. Le opzioni disponibili sono:

- **No** (impostazione predefinita): Microsoft Edge non viene eseguito in modalità tutto schermo. È possibile modificare e configurare tutte le impostazioni di Microsoft Edge.
- **Insegna digitale o schermo interattivo (app singola in modalità tutto schermo)** : filtra le impostazioni di Microsoft Edge applicabili alla modalità tutto schermo di Microsoft Edge Insegna digitale o schermo interattivo per l'uso solo in app singole in modalità tutto schermo Windows 10. Scegliere questa impostazione per aprire un URL a tutto schermo e visualizzare solo il contenuto di quel sito Web. [Set up digital signs](https://docs.microsoft.com/windows/configuration/setup-digital-signage) (Configurare insegne digitali) offre altre informazioni su questa funzionalità.
- **Esplorazione pubblica InPrivate (app singola in modalità tutto schermo)** : filtra le impostazioni di Microsoft Edge applicabili alla modalità tutto schermo di Microsoft Edge Esplorazione pubblica InPrivate per l'uso in app singole in modalità tutto schermo Windows 10. Esegue una versione a schede multiple di Microsoft Edge.
- **Modalità normale (più app in modalità tutto schermo)** : filtra le impostazioni di Microsoft Edge applicabili alla modalità tutto schermo di Microsoft Edge normale. Esegue una versione completa di Microsoft Edge con tutte le funzionalità di esplorazione.
- **Esplorazione pubblica (più app in modalità tutto schermo)** : filtra le impostazioni di Microsoft Edge applicabili all'esplorazione pubblica in più app in modalità tutto schermo Windows 10.  Esegue una versione a schede multiple di Microsoft Edge InPrivate.

> [!TIP]
> Per altre informazioni su queste opzioni, vedere [Microsoft Edge kiosk mode configuration types](https://docs.microsoft.com/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-configuration-types) (Tipi di configurazione della modalità tutto schermo di Microsoft Edge).

Questo profilo di restrizioni per i dispositivi è direttamente correlato al profilo in modalità tutto schermo creato usando le [impostazioni della modalità tutto schermo di Windows](kiosk-settings-windows.md). Per concludere:

1. Creare il profilo con le [impostazioni della modalità tutto schermo di Windows](kiosk-settings-windows.md) per eseguire il dispositivo in modalità tutto schermo. Selezionare Microsoft Edge come applicazione e impostare la modalità tutto schermo di Microsoft Edge nel profilo in modalità tutto schermo.
2. Creare il profilo di restrizioni per i dispositivi descritto in questo articolo e configurare funzionalità e impostazioni specifiche consentite in Microsoft Edge. Assicurarsi di scegliere lo stesso tipo di modalità tutto schermo di Microsoft Edge di quello selezionato nel profilo in modalità tutto schermo ([impostazioni della modalità tutto schermo di Windows](kiosk-settings-windows.md)). 

    [Supported kiosk mode settings](https://docs.microsoft.com/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-policies-for-kiosk-mode) (Impostazioni supportate per la modalità tutto schermo) è un'ottima risorsa.

> [!IMPORTANT] 
> Assicurarsi di assegnare questo profilo di Microsoft Edge agli stessi dispositivi del profilo in modalità tutto schermo ([impostazioni della modalità tutto schermo di Windows](kiosk-settings-windows.md)).

[CSP ConfigureKioskMode](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-configurekioskmode)

### <a name="start-experience"></a>Esperienza di avvio

- **Avvia Microsoft Edge con**: consente di scegliere quali pagine si devono aprire all'avvio di Microsoft Edge. Le opzioni disponibili sono:
  - **Pagine iniziali personalizzate**: immettere le pagine iniziali, ad esempio `http://www.contoso.com`. Microsoft Edge carica le pagine iniziali immesse.
  - **Pagina Nuova scheda**: Microsoft Edge carica qualsiasi pagina immessa per l'impostazione **URL di Nuova scheda**.
  - **Pagina dell'ultima sessione**: Microsoft Edge carica la pagina dell'ultima sessione.
  - **Pagine iniziali nelle impostazioni dell'app locale**: Microsoft Edge viene avviato con la pagina iniziale predefinita definita dal sistema operativo.

- **Consenti all'utente di modificare le pagine iniziali**: **Sì** (impostazione predefinita) consente all'utente di cambiare le pagine iniziali. Gli amministratori possono usare `EdgeHomepageUrls` per immettere le pagine iniziali che gli utenti visualizzano per impostazione predefinita all'apertura di Microsoft Edge. **No** impedisce agli utenti di modificare le pagine iniziali.
- **Consenti il contenuto Web nella pagina Nuova scheda**: se impostato su **Sì** (impostazione predefinita), Microsoft Edge apre l'URL immesso per l'impostazione **URL di Nuova scheda**. Se l'impostazione **URL di nuova scheda** è vuota, Microsoft Edge apre la pagina della nuova scheda indicata nelle impostazioni di Microsoft Edge. Modificabile dagli utenti. Se impostato su **No**, Microsoft Edge apre una nuova scheda con una pagina vuota. Gli utenti non possono modificare questa impostazione.
- **URL di Nuova scheda**: immettere l'URL da aprire nella pagina Nuova scheda. Ad esempio, immettere `https://www.bing.com` o `https://www.contoso.com`.

- **Pulsante Pagina iniziale**: scegliere cosa deve accadere quando si seleziona il pulsante Pagina iniziale. Le opzioni disponibili sono:
  - **Pagine iniziali**: viene aperta la pagina scelta per l'impostazione **Avvia Microsoft Edge con**.
  - **Pagina Nuova scheda**: apre l'URL immesso per l'impostazione **URL di Nuova scheda**.
  - **URL del pulsante Pagina iniziale**: immettere l'URL da aprire. Ad esempio, immettere `https://www.bing.com` o `https://www.contoso.com`.
  - **Nascondi il pulsante Pagina iniziale**: nasconde il pulsante Pagina iniziale
- **Consenti agli utenti di modificare il pulsante Pagina iniziale**: **Sì** consente agli utenti di cambiare il pulsante Pagina iniziale. Le modifiche dell'utente sostituiscono eventuali impostazioni dell'amministratore per il pulsante Pagina iniziale. **No** (impostazione predefinita) impedisce agli utenti di modificare la configurazione del pulsante Pagina iniziale impostata dall'amministratore.
- **Mostra la pagina del completamento dell'installazione (solo dispositivi mobili)** : **Sì** (impostazione predefinita) mostra la prima pagina di introduzione all'uso in Microsoft Edge. **No** impedisce la visualizzazione della pagina introduttiva quando si esegue Microsoft Edge per la prima volta. Questa funzionalità consente alle aziende, ad esempio le organizzazioni registrate in configurazioni a zero emissioni, di bloccare questa pagina.
- **Posizione dell'elenco di URL per il completamento dell'installazione** (solo Windows 10 Mobile): immettere l'URL che punta al file XML contenente i primi URL della pagina di esecuzione. Immettere ad esempio `https://www.contoso.com/sites.xml`.

- **Aggiorna il browser dopo il tempo di inattività**: immettere il numero di minuti di inattività trascorsi i quali il browser viene aggiornato, da 0 a 1440 minuti. L'impostazione predefinita è `5` minuti. Se impostata su `0` (zero), il browser non viene aggiornato dopo essere stato inattivo.

  Questa impostazione è disponibile solo in modalità [Esplorazione pubblica InPrivate (app singola in modalità tutto schermo)](#use-microsoft-edge-kiosk-mode).

- **Consenti popup** (solo desktop): **Sì** (impostazione predefinita) consente i popup nel Web browser. **No** non consente le finestre popup nel browser.
- **Invia traffico Intranet a Internet Explorer**(solo desktop): **Sì** consente agli utenti di aprire siti Web della Intranet in Internet Explorer invece che in Microsoft Edge. Questa impostazione è disponibile per compatibilità con le versioni precedenti. **No** (impostazione predefinita) consente agli utenti di usare Microsoft Edge.
- **Posizione dell'elenco di siti con modalità Enterprise** (solo desktop): immettere l'URL che punta al file XML contenente un elenco di siti Web aperti in modalità Enterprise. Gli utenti non possono modificare questo elenco. Immettere ad esempio `https://www.contoso.com/sites.xml`.
- **Messaggio all'apertura di siti in Internet Explorer**: usare questa impostazione per configurare Microsoft Edge per visualizzare una notifica prima dell'apertura di un sito in Internet Explorer 11. Le opzioni disponibili sono:
  - **Non visualizzare questo messaggio**: viene usato il comportamento predefinito del sistema operativo, che potrebbe non prevedere la visualizzazione di un messaggio.
  - **Mostra un messaggio relativo all'apertura del sito in Internet Explorer 11**: imposta la visualizzazione del messaggio all'apertura di siti in Internet Explorer. I siti vengono aperti in Internet Explorer. 
  - **Mostra il messaggio con l'opzione per l'apertura di siti in Microsoft Edge**: mostra il messaggio all'apertura dei siti in Microsoft Edge. Il messaggio include un collegamento **Continua in Microsoft Edge** in modo che gli utenti possano scegliere Microsoft Edge invece di Internet Explorer.

  > [!IMPORTANT]
  > Questa impostazione richiede di usare l'impostazione **Posizione dell'elenco di siti con modalità Enterprise**, l'impostazione **Invia traffico Intranet a Internet Explorer** o entrambe.

- **Consenti l'elenco di compatibilità Microsoft**: **Sì** (impostazione predefinita) consente l'uso di un elenco di compatibilità Microsoft. **No** impedisce l'uso dell'elenco di compatibilità Microsoft in Microsoft Edge. Questo elenco fornito da Microsoft aiuta Microsoft Edge a visualizzare in modo appropriato i siti con problemi di compatibilità noti.
- **Precarica le pagine iniziali e la pagina Nuova scheda**: **Sì** (impostazione predefinita) usa il comportamento predefinito del sistema operativo, che potrebbe prevedere il precaricamento di queste pagine. Il precaricamento riduce al minimo il tempo necessario per avviare Microsoft Edge e caricare nuove schede. **No** impedisce a Microsoft Edge di precaricare le pagine iniziali e la pagina Nuova scheda.
- **Preavvia le pagine iniziali e la pagina Nuova scheda**: **Sì** (impostazione predefinita) usa il comportamento predefinito del sistema operativo, che potrebbe prevedere il preavvio di queste pagine. Il preavvio contribuisce a migliorare le prestazioni di Microsoft Edge e riduce al minimo il tempo necessario per avviare Microsoft Edge. **No** impedisce a Microsoft Edge di preavviare le pagine iniziali e la pagina Nuova scheda.

### <a name="favorites-and-search"></a>Preferiti e ricerca

- **Mostra la barra Preferiti**: scegliere cosa accade alla barra Preferiti in qualsiasi pagina di Microsoft Edge. Le opzioni disponibili sono:
  - **Nelle pagine iniziali e della nuova scheda**: mostra la barra Preferiti all'avvio di Microsoft Edge e in tutte le nuove schede. Gli utenti possono modificare questa impostazione.
  - **In tutte le pagine**: mostra la barra Preferiti in tutte le pagine. Gli utenti non possono modificare questa impostazione.
  - **Nascosto**: nasconde la barra Preferiti in tutte le pagine. Gli utenti non possono modificare questa impostazione.
- **Consenti modifiche ai preferiti**: con l'impostazione **Sì** (predefinita) viene usata l'impostazione predefinita del sistema operativo, che consente agli utenti di modificare l'elenco. **No** impedisce agli utenti di eseguire operazioni di aggiunta, importazione, ordinamento o modifica dell'elenco Preferiti.
  - **Elenco Preferiti**: consente di aggiungere un elenco di URL al file dei Preferiti. Ad esempio: aggiungere `http://contoso.com/favorites.html`.
- **Sincronizza i Preferiti tra i browser Microsoft** (solo desktop): **Sì** impone la sincronizzazione dei Preferiti tra Internet Explorer e Microsoft Edge. Le aggiunte, le eliminazioni, le modifiche e le variazioni dell'ordine dei Preferiti vengono condivise tra i browser.  Con l'impostazione **No** (predefinita) viene usata l'impostazione predefinita del sistema operativo, che può consentire agli utenti di scegliere di sincronizzare i Preferiti tra i browser.
- **Motore di ricerca predefinito**: scegliere il motore di ricerca predefinito nel dispositivo. Gli utenti possono modificare questo valore in qualsiasi momento. Le opzioni disponibili sono:
  - Motore di ricerca nelle impostazioni client di Microsoft Edge
  - Bing
  - Google
  - Yahoo
  - Valore personalizzato: in **URL XML OpenSearch** immettere un URL HTTPS con il file XML che include come minimo il nome breve e l'URL per il motore di ricerca. Immettere ad esempio `https://www.contoso.com/opensearch.xml`.
- **Mostra i suggerimenti per la ricerca**: **Sì** (impostazione predefinita) consente al motore di ricerca di suggerire siti durante la digitazione delle frasi di ricerca nella barra degli indirizzi. **No** impedisce questa funzionalità.
- **Consenti modifiche al motore di ricerca**: **Sì** (impostazione predefinita) consente agli utenti di aggiungere nuovi motori di ricerca o di cambiare quello predefinito in Microsoft Edge. Scegliere **No** per impedire agli utenti di personalizzare il motore di ricerca.

  Questa impostazione è disponibile solo in [Modalità normale (più app in modalità tutto schermo)](#use-microsoft-edge-kiosk-mode).

### <a name="privacy-and-security"></a>Privacy e sicurezza

- **Consenti InPrivate Browsing**: **Sì** (impostazione predefinita) consente InPrivate Browsing in Microsoft Edge. Dopo la chiusura di tutte le schede InPrivate, Microsoft Edge elimina i dati di esplorazione dal dispositivo. **No** impedisce agli utenti di aprire sessioni InPrivate Browsing.
- **Salva la cronologia esplorazioni**: **Sì** (impostazione predefinita) consente di salvare la cronologia esplorazioni in Microsoft Edge. **No** impedisce di salvare la cronologia esplorazioni.
- **Cancella i dati di esplorazione all'uscita** (solo desktop): **Sì** cancella la cronologia e i dati di esplorazione quando gli utenti escono da Microsoft Edge. **No** (impostazione predefinita) usa il valore predefinito del sistema operativo, che potrebbe memorizzare nella cache i dati di esplorazione.
- **Sincronizza le impostazioni del browser tra i dispositivi di un utente**: scegliere la modalità di sincronizzazione delle impostazioni del browser tra i dispositivi. Le opzioni disponibili sono:
  - **Consenti**: consente la sincronizzazione delle impostazioni del browser Microsoft Edge tra i dispositivi dell'utente.
  - **Blocca e consenti l'override dell'utente**: blocca la sincronizzazione delle impostazioni del browser Microsoft Edge tra i dispositivi dell'utente. Gli utenti possono modificare questa impostazione.
  - **Blocca**: blocca la sincronizzazione delle impostazioni del browser Microsoft Edge tra i dispositivi degli utenti. Gli utenti non possono sostituire questa impostazione.

Quando l'opzione "Blocca e consenti l'override dell'utente" è selezionata, un utente può eseguire l'override della designazione dell'amministratore.

- **Consenti strumento per la gestione delle password**: **Sì** (impostazione predefinita) consente a Microsoft Edge di usare automaticamente lo strumento di gestione delle password, che consente agli utenti di salvare e gestire le password nel dispositivo. **No** impedisce l'uso dello strumento di gestione delle password in Microsoft Edge.
- **Cookie**: scegliere la modalità di gestione dei cookie nel Web browser. Le opzioni disponibili sono:
  - **Consenti**: i cookie vengono archiviati nel dispositivo.
  - **Blocca tutti i cookie**: i cookie non vengono archiviati nel dispositivo.
  - **Blocca solo i cookie di terze parti**: i cookie di partner o terze parti non vengono archiviati nel dispositivo.
- **Consenti il riempimento automatico nei moduli**: **Sì** (impostazione predefinita) consente agli utenti di modificare le impostazioni di completamento automatico nel browser e riempire automaticamente i campi del modulo. **No** disabilita la funzionalità di riempimento automatico in Microsoft Edge.
- **Invia intestazioni DNT (Do Not Track)** : **Sì** invia intestazioni DNT (Do Not Track) ai siti Web che richiedono informazioni di traccia (scelta consigliata). **No** (impostazione predefinita) non invia intestazioni che consentono ai siti Web di tenere traccia dell'utente. Gli utenti possono configurare questa impostazione.
- **Mostra l'indirizzo IP localhost WebRTC**: **Sì** (impostazione predefinita) consente la visualizzazione dell'indirizzo IP localhost degli utenti quando eseguono telefonate con questo protocollo. **No** impedisce la visualizzazione dell'indirizzo IP localhost degli utenti. 
- **Consenti la raccolta di dati dei riquadri animati**: **Sì** (impostazione predefinita) consente a Microsoft Edge di raccogliere informazioni dai riquadri animati aggiunti al menu Start. **No** impedisce la raccolta di queste informazioni, che possono fornire agli utenti un'esperienza limitata.
- **L'utente può eseguire l'override degli errori del certificato**: **Sì** (impostazione predefinita) consente agli utenti di accedere ai siti Web con errori SSL/TLS (Secure Socket Layer/Transport Layer Security). **No** (scelta consigliata per una maggiore sicurezza) impedisce agli utenti di accedere ai siti Web con errori SSL o TLS.

### <a name="additional"></a>Altro

- **Consenti il browser Microsoft Edge** (solo dispositivi mobili): **Sì** (impostazione predefinita) consente l'uso del Web browser Microsoft Edge nel dispositivo mobile. **No** impedisce l'uso di Microsoft Edge nei dispositivi. Se si sceglie **No**, le altre singole impostazioni si applicano solo al desktop.
- **Consenti l'elenco a discesa per la barra degli indirizzi**: **Sì** (impostazione predefinita) consente a Microsoft Edge di visualizzare l'elenco a discesa per la barra degli indirizzi con un elenco di suggerimenti. **No** impedisce a Microsoft Edge di visualizzare un elenco di suggerimenti in un elenco a discesa durante la digitazione. L'impostazione **No** consente di:
  - Ridurre al minimo l'uso della larghezza di banda tra Microsoft Edge e i servizi Microsoft.
  - Disabilitare **Mostra suggerimenti per la ricerca e i siti durante la digitazione** in Microsoft Edge > Impostazioni.
- **Consenti la modalità schermo intero**: **Sì** (impostazione predefinita) consente a Microsoft Edge di usare la modalità schermo intero, che mostra solo il contenuto Web e nasconde l'interfaccia utente di Microsoft Edge. **No** impedisce la modalità schermo intero in Microsoft Edge.
- **Consenti la pagina dei flag Informazioni su**: **Sì** (predefinita) viene usata l'impostazione predefinita del sistema operativo, che potrebbe consentire l'accesso alla pagina `about:flags`. La pagina `about:flags` consente agli utenti di modificare le impostazioni per gli sviluppatori e abilitare le funzionalità sperimentali. **No** impedisce agli utenti di accedere alla pagina `about:flags` in Microsoft Edge.
- **Consenti gli Strumenti di sviluppo**: **Sì** (impostazione predefinita) consente agli utenti di usare gli strumenti di sviluppo F12 per compilare ed eseguire il debug delle pagine Web per impostazione predefinita. **No** impedisce agli utenti di usare gli strumenti di sviluppo F12.
- **Consenti JavaScript**: **Sì** (impostazione predefinita) consente di eseguire script, ad esempio JavaScript, nel browser Microsoft Edge. **No** impedisce l'esecuzione di script Java del browser.
- **L'utente può installare estensioni**: **Sì** (impostazione predefinita) consente agli utenti di installare le estensioni di Microsoft Edge nei dispositivi. **No** impedisce l'installazione.
- **Consenti il sideload delle estensioni per sviluppatori**: con l'impostazione **Sì** (predefinita) viene usata l'impostazione predefinita del sistema operativo, che potrebbe consentire il sideload. Il sideload installa ed esegue estensioni non verificate. **No** impedisce il sideload in Microsoft Edge con la funzionalità **Carica estensioni**. Non impedisce il sideload delle estensioni in altri modi, ad esempio con PowerShell.
- **Estensioni obbligatorie**: scegliere le estensioni che non possono essere disattivate dagli utenti in Microsoft Edge. Immettere i nomi delle famiglie di pacchetti e selezionare **Aggiungi**. In [Trovare un nome di famiglia di pacchetti (PFN) per una rete VPN per app](https://docs.microsoft.com/configmgr/protect/deploy-use/find-a-pfn-for-per-app-vpn) sono disponibili alcune linee guida.

  È anche possibile **importare** un file CSV che include i nomi delle famiglie di pacchetti. In alternativa, **esportare** i nomi delle famiglie di pacchetti immessi.

## <a name="network-proxy"></a>Proxy di rete

Queste impostazioni usano il [provider di servizi di configurazione per i criteri relativi a NetworkProxy](https://docs.microsoft.com/windows/client-management/mdm/networkproxy-csp), che elenca anche le edizioni di Windows supportate.

- **Rileva automaticamente impostazioni proxy**: **Blocca** impedisce ai dispositivi di rilevare automaticamente uno script di configurazione automatica del proxy (PAC). Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe abilitare questa funzionalità e i dispositivi potrebbero tentare di trovare il percorso di uno script PAC.
- **Usa lo script proxy**: scegliere **Consenti** per immettere un percorso per lo script PAC per configurare il server proxy. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe non consentire di immettere l'URL di uno script PAC.
  - **URL dell'indirizzo dello script di installazione**: immettere l'URL di uno script PAC che si vuole usare per configurare il server proxy.
- **Usa il server proxy manuale**: scegliere **Consenti** per immettere manualmente il nome o l'indirizzo IP e il numero di porta TCP di un server proxy. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe non consentire di immettere manualmente i dettagli di un server proxy.
  - **Indirizzo**: immettere il nome o l'indirizzo IP del server proxy.
  - **Numero porta**: immettere il numero di porta del server proxy.
  - **Eccezione del proxy**: immettere gli URL che non devono usare il server proxy. Per separare ogni elemento, usare un punto e virgola (`;`).
  - **Ignora il server proxy per l'indirizzo locale**: **Consenti** non usa il server proxy per gli indirizzi Intranet locali. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe usare un server proxy per gli indirizzi locali della rete Intranet.

## <a name="password"></a>Password

Queste impostazioni usano il [provider di servizi di configurazione per i criteri relativi a DeviceLock](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock), che elenca anche le edizioni di Windows supportate.

- **Password**: **Rendi obbligatorio** richiede agli utenti di immettere una password per accedere al dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'accesso ai dispositivi senza password. Si applica solo agli account locali. Le password dell'account di dominio restano configurate da Active Directory (AD) e Azure AD.

  [DeviceLock/DevicePasswordEnabled CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-devicepasswordenabled)

  - **Tipo di password richiesto**: scegliere il tipo di password. Le opzioni disponibili sono:
    - **Non configurata**: Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire alla password di includere numeri e lettere.
    - **Alfanumerica**: la password deve essere composta da una combinazione di lettere e numeri.
    - **Numerica**: la password deve essere composta solo da numeri.

    [CSP DeviceLock/AlphanumericDevicePasswordRequired](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-alphanumericdevicepasswordrequired)

  - **Lunghezza minima password**: immettere il numero minimo di caratteri necessari, da 4 a 16. Ad esempio, immettere `6` per richiedere una lunghezza della password di minimo sei caratteri. Per impostazione predefinita, il sistema operativo potrebbe impostare il valore su `4`.
  
    [DeviceLock/MinDevicePasswordLength CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-mindevicepasswordlength)
  
    > [!IMPORTANT]
    > La modifica dei requisiti per la password in un desktop di Windows interessa gli utenti al successivo accesso, ossia quando i dispositivi passano dallo stato inattivo allo stato attivo. Agli utenti con password che soddisfano i requisiti viene comunque chiesto di cambiare la password.

  - **Numero di errori di accesso prima della cancellazione dei dati del dispositivo**: immettere il numero di password non corrette consentite prima che il dispositivo venga cancellato, fino a 11. Il numero valido immesso dipende dall'edizione. In [Provider di servizi di configurazione DeviceLock/MaxDevicePasswordFailedAttempts](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-maxdevicepasswordfailedattempts) sono elencati i valori supportati. `0` (zero) potrebbe disabilitare la funzionalità di cancellazione del dispositivo.

    Questa impostazione ha inoltre un impatto diverso a seconda dell'edizione. Per informazioni dettagliate su questa impostazione, vedere il [provider di servizi di configurazione DeviceLock/MaxDevicePasswordFailedAttempts](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-maxdevicepasswordfailedattempts).

  - **Numero massimo di minuti di inattività fino al blocco dello schermo**: immettere il periodo di tempo per cui un dispositivo deve rimanere inattivo prima che lo schermo venga bloccato. Ad esempio, immettere `5` per bloccare i dispositivi dopo 5 minuti di inattività. Quando questa opzione è impostata su **Non configurato**, Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe impostare il valore su `0` (zero), cioè timeout nullo.

    [DeviceLock/MaxInactivityTimeDeviceLock CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-maxinactivitytimedevicelock)

  - **Scadenza password (giorni)** : immettere il periodo di tempo in giorni dopo il quale è necessario modificare la password del dispositivo, da 1 a 365. Ad esempio, immettere `90` per impostare la scadenza della password dopo 90 giorni. Quando il valore è vuoto, Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe impostare il valore su `0` (zero), cioè scadenza nulla.

    [DeviceLock/DevicePasswordExpiration CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-devicepasswordexpiration)

  - **Impedisci riutilizzo delle password precedenti**: immettere il numero di password usate in precedenza che non è possibile usare, da 1 a 24. Ad esempio, immettere `5` in modo che gli utenti non possano definire una nuova password uguale alla password corrente o a una qualsiasi delle quattro precedenti. Quando il valore è vuoto, Intune non modifica o aggiorna questa impostazione.

    [DeviceLock/DevicePasswordHistory CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-devicepasswordhistory)

  - **Richiedi la password quando il dispositivo torna attivo dopo uno stato di inattività** (Mobile e Holographic): **Rendi obbligatorio** richiede agli utenti di immettere una password per sbloccare il dispositivo dopo l'inattività. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe non richiedere un PIN o una password dopo l'inattività.

    [DeviceLock/AllowIdleReturnWithoutPassword CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-allowidlereturnwithoutpassword)

  - **Password semplici**: **Blocca** impedisce agli utenti di creare password semplici, ad esempio `1234` o `1111`. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di creare password semplici. Questa impostazione impedisce anche l'uso di password grafiche.

    [DeviceLock/AllowSimpleDevicePassword CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-allowsimpledevicepassword)

- **Crittografia automatica durante l'aggiunta ad AAD**: **Blocca** impedisce la crittografia automatica BitLocker dei dispositivi quando i dispositivi vengono preparati per il primo uso e sono aggiunti ad Azure AD. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe abilitare la crittografia.

  Altre informazioni sulla [crittografia BitLocker per dispositivi](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-device-encryption-overview-windows-10#bitlocker-device-encryption).

  [CSP Security/PreventAutomaticDeviceEncryptionForAzureADJoinedDevices](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-security#security-preventautomaticdeviceencryptionforazureadjoineddevices)

- **Criteri FIPS (Federal Information Processing Standard)** : con **Consenti** vengono usati i criteri FIPS (Federal Information Processing Standard), ovvero uno standard del governo degli Stati Uniti per crittografia, hash e firma. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe non consentire FIPS.

  [CSP Cryptography/AllowFipsAlgorithmPolicy](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-cryptography#cryptography-allowfipsalgorithmpolicy)

- **Autenticazione del dispositivo Windows Hello**: **Consenti** permette agli utenti di usare un dispositivo complementare Windows Hello, ad esempio un telefono, un bracciale per il fitness o un dispositivo IoT per accedere a un computer Windows 10. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe impedire ai dispositivi complementari Windows Hello di eseguire l'autenticazione.

  [CSP Authentication/AllowSecondaryAuthenticationDevice](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-authentication#authentication-allowsecondaryauthenticationdevice)

- **Dominio preferito del tenant di Azure AD**: immettere un nome di dominio esistente nell'organizzazione Azure AD. Gli utenti di questo dominio non dovranno digitare il nome di dominio all'accesso. Immettere ad esempio `contoso.com`. Gli utenti inclusi nel dominio `contoso.com` possono accedere usando il proprio nome utente, ad esempio `abby` invece di `abby@contoso.com`.

  [CSP Authentication/PreferredAadTenantDomainName](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-authentication#authentication-preferredaadtenantdomainname)

## <a name="per-app-privacy-exceptions"></a>Eccezioni alla privacy per app

Consente di **aggiungere** app che devono avere un comportamento di privacy diverso da quello definito in "Privacy predefinita".

- **Nome pacchetto**: nome della famiglia di pacchetti dell'app.
- **Nome app**: nome dell'app.

### <a name="exceptions"></a>Eccezioni

- **Informazioni sull'account**: consente di definire se questa app può accedere a nome utente, immagine e altre informazioni del contatto.
- **App in background**: consente di definire se l'app può essere eseguita in background.
- **Calendario**: consente di definire se l'app può accedere al calendario.
- **Registro chiamate**: consente di definire se l'app può accedere al registro delle chiamate personale.
- **Fotocamera**: consente di definire se l'app può accedere alla fotocamera.
- **Contatti**: consente di definire se l'app può accedere ai contatti.
- **Posta elettronica**: consente di definire se l'app può accedere alla posta elettronica e inviare messaggi.
- **Location** (Percorso): consente di definire se l'app può accedere alle informazioni sulla posizione.
- **Messaggistica**: consente di definire se l'app può leggere o inviare SMS o MMS.
- **Microfono**: consente di definire se l'app può usare il microfono.
- **Movimento**: consente di definire se l'app può accedere alle informazioni sul movimento dei dispositivi.
- **Notifiche**: consente di definire se l'app può accedere alle notifiche.
- **Telefono**: consente di definire se l'app può accedere al telefono.
- **Radio**: alcune app usano le radio nel dispositivo, ad esempio Bluetooth, per inviare e ricevere i dati e devono attivare o disattivare queste radio. Specificare se l'app può controllare queste radio.
- **Attività**: consente di definire se l'app può accedere alle attività personali.
- **Dispositivi attendibili**: specificare se l'app può usare dispositivi attendibili, I dispositivi attendibili sono hardware già connesso o hardware incluso nel dispositivo. Ad esempio, usare TV, proiettori e così via come dispositivi attendibili.
- **Commenti e diagnostica**: consente di definire se l'app può accedere alle informazioni di diagnostica.
- **Sincronizza con i dispositivi**: specificare se l'app può condividere e sincronizzare automaticamente le informazioni con dispositivi wireless non associati in modo esplicito al dispositivo.

## <a name="personalization"></a>Personalization

Queste impostazioni usano il [provider di servizi di configurazione per i criteri relativi alla personalizzazione](https://docs.microsoft.com/windows/client-management/mdm/personalization-csp), che elenca anche le edizioni di Windows supportate.

- **URL dell'immagine di sfondo del desktop (solo desktop)** : immettere l'URL per un'immagine in formato JPG, JPEG o PNG che si vuole usare come sfondo del desktop di Windows. Gli utenti non possono modificare l'immagine. Immettere ad esempio `https://contoso.com/logo.png`.

  Quando il campo è vuoto, Intune non modifica o aggiorna questa impostazione.

## <a name="printer"></a>Stampante

- **Stampanti**: aggiungere stampanti usando i rispettivi nomi host di rete (nome DNS). Il sistema operativo cerca e installa i driver della stampante corrispondenti per ogni stampante del dispositivo. Se non viene inserito un valore, Intune non modifica o aggiorna questa impostazione.

  [Education/PrinterNames CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-education#education-printernames)

- **Stampante predefinita**: immettere il nome host di rete (nome DNS) di una stampante installata da usare come stampante predefinita. Se non viene inserito un valore, Intune non modifica o aggiorna questa impostazione.

  [Education/DefaultPrinterName CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-education#education-defaultprintername)

- **Aggiungere nuove stampanti**: **Blocca** impedisce agli utenti di aggiungere nuove stampanti. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire di aggiungere nuove stampanti.

  [Education/PreventAddingNewPrinters CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-education#education-preventaddingnewprinters)

## <a name="privacy"></a>Privacy

Queste impostazioni usano il [provider di servizi di configurazione per i criteri relativi alla privacy](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-privacy), che elenca anche le edizioni di Windows supportate.

- **Esperienza relativa alla privacy**: **Blocca** impedisce l'apertura dell'esperienza relativa alla privacy quando gli utenti effettuano l'accesso e per utenti nuovi e aggiornati. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.

  [Privacy/DisablePrivacyExperience](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-privacy#privacy-disableprivacyexperience)

- **Personalizzazione dell'input**: **Blocca** impedisce l'uso della voce per la dettatura e per comunicare con Cortana e altre app che usano il riconoscimento vocale basato sul cloud Microsoft. La funzionalità è disabilitata e gli utenti non possono abilitare il riconoscimento vocale online usando le impostazioni. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di scegliere. Se si consentono questi servizi, Microsoft potrebbe raccogliere dati vocali per migliorare il servizio.

  [Privacy/AllowInputPersonalization CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-privacy#privacy-allowinputpersonalization)

- **Accettazione automatica delle richieste di associazione e di consenso utente sulla privacy**: con **Consenti** Windows può accettare automaticamente messaggi di associazione e consenso sulla privacy durante l'esecuzione di app. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe impedire di accettare automaticamente.

  [Privacy/AllowAutoAcceptPairingAndPrivacyConsentPrompts CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-privacy#privacy-allowautoacceptpairingandprivacyconsentprompts)

- **Pubblica le attività utente**: **Blocca** impedisce alle app e al sistema operativo di pubblicare le attività utente. Inoltre, impedisce la condivisione delle esperienze e l'individuazione delle risorse usate di recente nel feed attività. Le attività utente rilevano lo stato delle attività di un utente in un'app o nel sistema operativo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe abilitare questa funzionalità in modo che le app possano pubblicare le attività utente.

  [Privacy/PublishUserActivities CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-privacy#privacy-publishuseractivities)

- **Solo attività locali**: **Blocca** consente di bloccare le esperienze condivise o l'individuazione di risorse usate di recente nello strumento per il cambio modalità per l'attività e così via solo in base all'attività locale. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.

È possibile configurare le informazioni accessibili per tutte le app nel dispositivo. Definire anche le eccezioni per le singole app tramite **Eccezioni alla privacy per app**.

### <a name="exceptions"></a>Eccezioni

- **Informazioni sull'account**: consente di definire se questa app può accedere a nome utente, immagine e altre informazioni del contatto.
- **App in background**: consente di definire se l'app può essere eseguita in background.
- **Calendario**: consente di definire se l'app può accedere al calendario.
- **Registro chiamate**: consente di definire se l'app può accedere al registro delle chiamate personale.
- **Fotocamera**: consente di definire se l'app può accedere alla fotocamera.
- **Contatti**: consente di definire se l'app può accedere ai contatti.
- **Posta elettronica**: consente di definire se l'app può accedere alla posta elettronica e inviare messaggi.
- **Location** (Percorso): consente di definire se l'app può accedere alle informazioni sulla posizione.
- **Messaggistica**: consente di definire se l'app può leggere o inviare SMS o MMS.
- **Microfono**: consente di definire se l'app può usare il microfono.
- **Movimento**: consente di definire se l'app può accedere alle informazioni sul movimento dei dispositivi.
- **Notifiche**: consente di definire se l'app può accedere alle notifiche.
- **Telefono**: consente di definire se l'app può accedere al telefono.
- **Radio**: alcune app usano le radio nel dispositivo, ad esempio Bluetooth, per inviare e ricevere i dati e devono attivare o disattivare queste radio. Specificare se l'app può controllare queste radio.
- **Attività**: consente di definire se l'app può accedere alle attività personali.
- **Dispositivi attendibili**: specificare se l'app può usare dispositivi attendibili, I dispositivi attendibili sono hardware già connesso o hardware incluso nel dispositivo. Ad esempio, usare TV, proiettori e così via come dispositivi attendibili.
- **Commenti e diagnostica**: specificare se l'app può accedere alle informazioni di diagnostica.
- **Sincronizza con i dispositivi** - Specificare se l'app può condividere e sincronizzare automaticamente le informazioni con dispositivi wireless non associati in modo esplicito a questo PC, tablet o telefono.

## <a name="projection"></a>Proiezione

Queste impostazioni usano il [provider di servizi di configurazione per i criteri relativi a WirelessDisplay](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-wirelessdisplay), che elenca anche le edizioni di Windows supportate.

- **Input degli utenti da ricevitori di schermo wireless**: **Blocca** impedisce l'input degli utenti da ricevitori di schermo wireless. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire a uno schermo wireless di inviare l'input da tastiera, mouse, penna e tocco al dispositivo di origine.

  [WirelessDisplay/AllowUserInputFromWirelessDisplayReceiver CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-wirelessdisplay#wirelessdisplay-allowuserinputfromwirelessdisplayreceiver)

- **Proiezione per questo computer**: **Blocca** impedisce ad altri dispositivi di trovare il dispositivo per la proiezione e impedisce la proiezione in altri dispositivi. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire ai dispositivi di essere individuabili e può consentire la proiezione nel dispositivo al di sopra della schermata di blocco.

  [WirelessDisplay/AllowProjectionFromPC CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-wirelessdisplay#wirelessdisplay-allowprojectionfrompc)

- **Richiedi il PIN per l'associazione**: **Rendi obbligatorio** richiede sempre un PIN per la connessione a un dispositivo di proiezione. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe non richiedere un PIN per associare il dispositivo.

  [WirelessDisplay/RequirePinForPairing CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-wirelessdisplay#wirelessdisplay-requirepinforpairing)

## <a name="reporting-and-telemetry"></a>Reporting e telemetria

- **Condividi i dati di utilizzo**: scegliere il livello di dati di diagnostica inviati. Le opzioni disponibili sono:
  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione. nessuna impostazione viene imposta. Gli utenti scelgono il livello inviato. Per impostazione predefinita, il sistema operativo potrebbe non condividere i dati.
  - **Sicurezza**: le informazioni necessarie per mantenere più sicuro Windows, inclusi i dati sulle impostazioni del componente Esperienze utente connesse e telemetria, Strumento di rimozione malware e Microsoft Defender
  - **Base**: informazioni di base sul dispositivo, inclusi dati relativi a qualità, compatibilità delle app, utilizzo delle app e i dati dal livello Sicurezza
  - **Avanzato**: informazioni dettagliate aggiuntive, ad esempio come vengono usati Windows, Windows Server, System Center e le app, le relative prestazioni, dati avanzati sull'affidabilità e i dati dei livelli Base e Sicurezza
  - **Completa**: tutti i dati necessari per identificare e contribuire alla risoluzione dei problemi, oltre ai dati dal livello Sicurezza, Base e Avanzato.

  [Provider di servizi di configurazione System/AllowTelemetry](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-system#system-allowtelemetry)

- **Invia i dati di esplorazione di Microsoft Edge a Microsoft 365 Analytics**: per usare questa funzionalità, impostare l'opzione **Condividi i dati di utilizzo** su **Avanzato** o **Completo**. Questa funzionalità consente di controllare quali dati Microsoft Edge invia a Microsoft 365 Analytics per i dispositivi aziendali con un ID commerciale configurato. Le opzioni disponibili sono:
  - **Non configurata**: Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe non raccogliere o inviare i dati della cronologia esplorazioni.
  - **Invia solo dati Intranet**: consente all'amministratore di inviare la cronologia dei dati Intranet.
  - **Invia solo dati Internet**: consente all'amministratore di inviare la cronologia dei dati Internet.
  - **Invia dati Intranet e Internet**: consente all'amministratore di inviare la cronologia dei dati Intranet e Internet.

  [Provider di servizi di configurazione Browser/ConfigureTelemetryForMicrosoft365Analytics](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-configuretelemetryformicrosoft365analytics)

- **Server proxy di telemetria**: immettere il nome di dominio completo (FQDN) o l'indirizzo IP di un server proxy per l'inoltro delle richieste del servizio Esperienze utente connesse e telemetria tramite una connessione Secure Sockets Layer (SSL). Il formato di questa impostazione è *server*:*porta*. In caso di errore del proxy denominato oppure se non viene immesso alcun proxy, i dati di Esperienze utente connesse e telemetria non vengono inviati. Essi rimangono sul dispositivo locale.

  Se non viene inserito un valore, Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo può inviare i dati di Esperienze utente connesse e telemetria a Microsoft usando la configurazione proxy predefinita.

  Formati di esempio:

  ```
  IPv4: 192.246.246.106:100
  IPv6: [2001:4898:4010:4013:95c1:a8b2:953c:c633]:100
  FQDN: www.contoso.com:345
  ```

  [Provider di servizi di configurazione System/TelemetryProxy](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-system#system-telemetryproxy)

## <a name="search"></a>Cerca

Queste impostazioni usano il [provider di servizi di configurazione per i criteri relativi alla ricerca](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search), che elenca anche le edizioni di Windows supportate.

- **Ricerca sicura (solo dispositivi mobili)** : controlla come Cortana filtra il contenuto per adulti nei risultati della ricerca. Le opzioni disponibili sono:
  - **Definita dall'utente**: Intune non modifica o aggiorna questa impostazione. nessuna impostazione viene imposta. Gli utenti scelgono le proprie impostazioni.
  - **Restrittivo**: filtro massimo del contenuto per adulti
  - **Moderato**: filtro moderato del contenuto per adulti. I risultati di ricerca validi non vengono filtrati.
- **Visualizza i risultati Web nella ricerca**: **Blocca** impedisce agli utenti di usare Windows Search per eseguire ricerche in Internet e i risultati Web non vengono visualizzati in Search. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di eseguire ricerche nel Web e i risultati vengono visualizzati nel dispositivo.
- **Segni diacritici**: **Blocca** impedisce che i segni diacritici vengano visualizzati in Windows Search. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe mostrare i segni diacritici.

  [Search/AllowUsingDiacritics CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search#search-allowusingdiacritics)

- **Rilevamento lingua automatico**: **Blocca** impedisce a Windows Search di rilevare automaticamente la lingua durante l'indicizzazione di contenuti o proprietà. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire questa funzionalità.

  [Search/AlwaysUseAutoLangDetection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search#search-alwaysuseautolangdetection)

- **Cerca percorso**: **Blocca** impedisce a Windows Search di usare il percorso. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire questa funzionalità.

  [Search/AllowSearchToUseLocation CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search#search-allowsearchtouselocation)

- **Backoff dell'indicizzatore**: **Blocca** disabilita la funzionalità di ricerca del backoff dell'indicizzatore. L'indicizzazione continua alla massima velocità, anche se l'attività del sistema è elevata. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe usare la logica backoff per limitare l'attività di indicizzazione quando l'attività del sistema è elevata.

  [Search/DisableBackoff CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search#search-disablebackoff)

- **Indicizzazione delle unità rimovibili**: **Blocca** impedisce di aggiungere le posizioni nelle unità rimovibili alle librerie e ne impedisce l'indicizzazione. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire questa funzionalità.

  [Search/DisableRemovableDriveIndexing CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search#search-disableremovabledriveindexing)

- **Indicizzazione con spazio su disco insufficiente**: **Abilita** consente l'indicizzazione automatica, anche quando lo spazio su disco è ridotto. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe disattivare l'indicizzazione automatica quando lo spazio su disco rigido è di 600 MB o inferiore. Se i dispositivi dell'organizzazione hanno spazio su disco rigido limitato, impostarlo su **Non configurato**.

  [Search/PreventIndexingLowDiskSpaceMB CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search#search-preventindexinglowdiskspacemb)

- **Query remote**: **Abilita** consente le query remote dell'indice del dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe impedire agli utenti di eseguire query remote dell'indice del dispositivo.

  [Search/PreventRemoteQueries CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search#search-preventremotequeries)

## <a name="start"></a>Avvia

Queste impostazioni usano il [provider di servizi di configurazione per i criteri relativi al menu Start](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start), che elenca anche le edizioni di Windows supportate.  

- **Layout del menu Start**: Caricare un file XML che include le personalizzazioni, tra cui l'ordine in cui sono elencate le app e altro ancora. Il file XML sostituisce il layout di avvio predefinito. Gli utenti non possono modificare il layout del menu Start immesso.

  Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.

  [Start/StartLayout CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-startlayout)

- **Aggiungi i siti Web ai riquadri nel menu Start**: consente di importare immagini da Microsoft Edge. Queste immagini vengono mostrate come collegamenti nel menu Start di Windows per i dispositivi desktop. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.

  [Start/ImportEdgeAssets CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-importedgeassets)

- **Rimuovi le app dalla barra della applicazioni**: **Blocca** impedisce agli utenti di sbloccare app dalla barra delle applicazioni. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di rimuovere le app dalla barra delle applicazioni.

  [Start/NoPinningToTaskbar CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-nopinningtotaskbar)

- **Cambio rapido utente**: **Blocca** impedisce il cambio utente tra utenti connessi simultaneamente senza che eseguano la disconnessione. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe mostrare il comando **Cambia utente** nel riquadro utente.

  [Start/HideSwitchAccount CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hideswitchaccount)

- **App più usate**: **Blocca** nasconde le app più usate nel menu Start. Questa opzione disabilita anche l'alternanza corrispondente nell'app Impostazioni. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe mostrare le app più usate.

  [Start/HideFrequentlyUsedApps CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hidefrequentlyusedapps)

- **App aggiunte di recente**: **Blocca** nasconde le app aggiunte di recente al menu Start. Questa opzione disabilita anche l'alternanza corrispondente nell'app Impostazioni. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe mostrare le app aggiunte di recente al menu Start.

  [Start/HideRecentlyAddedApps CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hiderecentlyaddedapps)

- **Modalità della schermata Start**: scegliere le dimensioni della schermata Start. Le opzioni disponibili sono:
  - **Definita dall'utente**: Intune non modifica o aggiorna questa impostazione. nessuna impostazione viene imposta. Gli utenti possono impostare le dimensioni.
  - **Schermo intero**: impone le dimensioni a schermo intero per il menu Start.
  - **Non a schermo intero**: impone le dimensioni non a schermo intero per il menu Start.

  [Start/ForceStartSize CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-forcestartsize)

- **Elementi aperti di recente nelle jump list**: **Blocca** nasconde le jump list recenti nel menu Start e nella barra delle applicazioni. Questa opzione disabilita anche l'alternanza corrispondente nell'app Impostazioni. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe mostrare gli elementi aperti di recente nelle jump list.

  [Start/HideRecentJumplists CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hiderecentjumplists)

- **Elenco di app**: scegliere come visualizzare tutti gli elenchi di app. Le opzioni disponibili sono:
  - **Definita dall'utente**: Intune non modifica o aggiorna questa impostazione. nessuna impostazione viene imposta. Gli utenti scelgono come viene visualizzato l'elenco delle app.
  - **Comprimi**: nasconde l'elenco con tutte le app.
  - **Comprimi e disabilita l'app Impostazioni**: nasconde l'elenco con tutte le app e disabilita **Mostra l'elenco delle app nel menu Start** nell'app Impostazioni.
  - **Rimuovi e disabilita l'app Impostazioni**: nasconde l'elenco con tutte le app, rimuove il pulsante per visualizzare tutte le app e disabilita l'opzione **Mostra l'elenco di app nel menu Start** nell'app Impostazioni.

  [Start/HideAppList CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hideapplist)

- **Pulsante di alimentazione**: **Blocca** nasconde il pulsante di alimentazione nel menu Start. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe mostrare il pulsante di alimentazione.

  [Start/HidePowerButton CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hidepowerbutton)

- **Riquadro utente**: **Blocca** nasconde il riquadro utente nel menu Start. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe mostrare il riquadro utente. Configurare le seguenti impostazioni:
  - **Blocco**: **Blocca** nasconde l'opzione **Blocca** nel riquadro utente nel menu Start.  Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe mostrare l'opzione **Blocca**.
  - **Disconnetti**: **Blocca** nasconde l'opzione **Disconnetti** nel riquadro utente nel menu Start. Con l'impostazione **Non configurata** (predefinita) viene visualizzata l'opzione **Disconnetti**.

  [Start/HideUserTile CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hideusertile)

- **Arresta**: **Blocca** nasconde le opzioni **Aggiorna e arresta** e **Arresta** nel pulsante di alimentazione nel menu Start. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.

  [Start/HideShutDown CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hideshutdown)

- **Sospendi**: **Blocca** nasconde l'opzione **Sospendi** nel pulsante di alimentazione nel menu Start. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.

  [Start/HideSleep CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hidesleep)

- **Iberna**: **Blocca** nasconde l'opzione **Iberna** nel pulsante di alimentazione nel menu Start. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.

  [Start/HideHibernate CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hidehibernate)

- **Cambia account**: **Blocca** nasconde l'opzione **Cambia account** nel riquadro utente nel menu Start. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.

  [Start/HideSwitchAccount CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hideswitchaccount)

- **Opzioni per il riavvio**:  **Blocca** nasconde le opzioni **Aggiorna e riavvia** e **Riavvia** nel pulsante di alimentazione nel menu Start. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.

  [Start/HideRestart CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hiderestart)

- **Documenti nel menu Start**: nasconde o mostra la cartella Documenti nel menu Start di Windows. Le opzioni disponibili sono:
  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione. nessuna impostazione viene imposta. Gli utenti possono scegliere di mostrare o nascondere il collegamento.
  - **Nascondi**: il collegamento viene nascosto e l'impostazione viene disabilitata nell'app Impostazioni.
  - **Mostra**: il collegamento viene mostrato e l'impostazione viene disabilitata nell'app Impostazioni.

  [Start/AllowPinnedFolderDocuments CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderdocuments)

- **Download nel menu Start**: nasconde o mostra la cartella Download nel menu Start di Windows. Le opzioni disponibili sono:
  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione. nessuna impostazione viene imposta. Gli utenti possono scegliere di mostrare o nascondere il collegamento.
  - **Nascondi**: il collegamento viene nascosto e l'impostazione viene disabilitata nell'app Impostazioni.
  - **Mostra**: il collegamento viene mostrato e l'impostazione viene disabilitata nell'app Impostazioni.

  [Start/AllowPinnedFolderDownloads CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderdownloads)

- **Esplora file nel menu Start**: nasconde o mostra Esplora file nel menu Start di Windows. Le opzioni disponibili sono:
  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione. nessuna impostazione viene imposta. Gli utenti possono scegliere di mostrare o nascondere il collegamento.
  - **Nascondi**: il collegamento viene nascosto e l'impostazione viene disabilitata nell'app Impostazioni.
  - **Mostra**: il collegamento viene mostrato e l'impostazione viene disabilitata nell'app Impostazioni.

  [Start/AllowPinnedFolderFileExplorer CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderfileexplorer)

- **HomeGroup nel menu Start**: nasconde o mostra il collegamento Gruppo Home nel menu Start di Windows. Le opzioni disponibili sono:
  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione. nessuna impostazione viene imposta. Gli utenti possono scegliere di mostrare o nascondere il collegamento.
  - **Nascondi**: il collegamento viene nascosto e l'impostazione viene disabilitata nell'app Impostazioni.
  - **Mostra**: il collegamento viene mostrato e l'impostazione viene disabilitata nell'app Impostazioni.

  [Start/AllowPinnedFolderHomeGroup CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderhomegroup)

- **Musica nel menu Start**: nasconde o mostra la cartella Musica nel menu Start di Windows. Le opzioni disponibili sono:
  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione. nessuna impostazione viene imposta. Gli utenti possono scegliere di mostrare o nascondere il collegamento.
  - **Nascondi**: il collegamento viene nascosto e l'impostazione viene disabilitata nell'app Impostazioni.
  - **Mostra**: il collegamento viene mostrato e l'impostazione viene disabilitata nell'app Impostazioni.

  [Start/AllowPinnedFolderMusic CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfoldermusic)

- **Rete nel menu Start**: nasconde o mostra Rete nel menu Start di Windows. Le opzioni disponibili sono:
  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione. nessuna impostazione viene imposta. Gli utenti possono scegliere di mostrare o nascondere il collegamento.
  - **Nascondi**: il collegamento viene nascosto e l'impostazione viene disabilitata nell'app Impostazioni.
  - **Mostra**: il collegamento viene mostrato e l'impostazione viene disabilitata nell'app Impostazioni.

  [Start/AllowPinnedFolderNetwork CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfoldernetwork)

- **Cartella Personale nel menu Start**: nasconde o mostra la cartella Personale nel menu Start di Windows. Le opzioni disponibili sono:
  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione. nessuna impostazione viene imposta. Gli utenti possono scegliere di mostrare o nascondere il collegamento.
  - **Nascondi**: il collegamento viene nascosto e l'impostazione viene disabilitata nell'app Impostazioni.
  - **Mostra**: il collegamento viene mostrato e l'impostazione viene disabilitata nell'app Impostazioni.

  [Start/AllowPinnedFolderPersonalFolder CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderpersonalfolder)

- **Immagini nel menu Start**: nasconde o mostra la cartella delle immagini nel menu Start di Windows. Le opzioni disponibili sono:
  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione. nessuna impostazione viene imposta. Gli utenti possono scegliere di mostrare o nascondere il collegamento.
  - **Nascondi**: il collegamento viene nascosto e l'impostazione viene disabilitata nell'app Impostazioni.
  - **Mostra**: il collegamento viene mostrato e l'impostazione viene disabilitata nell'app Impostazioni.

  [Start/AllowPinnedFolderPictures CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderpictures)

- **Impostazioni nel menu Start**: nasconde o mostra il collegamento Impostazioni nel menu Start di Windows. Le opzioni disponibili sono:
  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione. nessuna impostazione viene imposta. Gli utenti possono scegliere di mostrare o nascondere il collegamento.
  - **Nascondi**: il collegamento viene nascosto e l'impostazione viene disabilitata nell'app Impostazioni.
  - **Mostra**: il collegamento viene mostrato e l'impostazione viene disabilitata nell'app Impostazioni.

  [Start/AllowPinnedFolderSettings CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfoldersettings)

- **Video nel menu Start**: nasconde o mostra la cartella dei video nel menu Start di Windows. Le opzioni disponibili sono:
  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione. nessuna impostazione viene imposta. Gli utenti possono scegliere di mostrare o nascondere il collegamento.
  - **Nascondi**: il collegamento viene nascosto e l'impostazione viene disabilitata nell'app Impostazioni.
  - **Mostra**: il collegamento viene mostrato e l'impostazione viene disabilitata nell'app Impostazioni.

  [Start/AllowPinnedFolderVideos CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfoldervideos)

## <a name="microsoft-defender-smartscreen"></a>Microsoft Defender SmartScreen

- **SmartScreen per Microsoft Edge**: **Rendi obbligatorio** attiva Microsoft Defender SmartScreen e impedisce agli utenti di disattivarlo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo può attivare SmartScreen e consentire agli utenti di attivarlo e disattivarlo.

  Microsoft Edge usa Microsoft Defender SmartScreen (attivato) per proteggere gli utenti da potenziali tentativi di phishing e software dannoso.

  [Provider di servizi di configurazione Browser/AllowSmartScreen](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)

- **Accesso a siti dannosi**: **Blocca** impedisce agli utenti di ignorare gli avvisi del filtro SmartScreen di Microsoft Defender e impedisce loro di passare al sito. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di ignorare gli avvisi e di passare al sito.

  [Provider di servizi di configurazione Browser/PreventSmartScreenPromptOverride](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)

- **Download di file non verificati**: **Blocca** impedisce agli utenti di ignorare gli avvisi del filtro SmartScreen di Microsoft Defender nonché di scaricare file non verificati. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di ignorare gli avvisi e continuare a scaricare i file non verificati.

  [Provider di servizi di configurazione Browser/PreventSmartScreenPromptOverrideForFiles](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)

## <a name="windows-spotlight"></a>Contenuti in evidenza di Windows

Queste impostazioni usano il [provider di servizi di configurazione per i criteri relativi all'esperienza](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience), che elenca anche le edizioni di Windows supportate.

- **Windows Spotlight**: **Blocca** disattiva Contenuti in evidenza di Windows nella schermata di blocco, Suggerimenti di Windows, le funzionalità per gli utenti consumer Microsoft e altre funzionalità correlate. Se l'obiettivo è ridurre al minimo il traffico di rete dai dispositivi, selezionare **Sì**. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire le funzionalità di Windows Spotlight e potrebbe essere controllato dagli utenti.

  [Experience/AllowWindowsSpotlight CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsspotlight)

  Quando l'opzione è impostata su **Non configurato**, è anche possibile consentire o bloccare le impostazioni seguenti:

  - **Windows Spotlight nella schermata di blocco**: **Blocca** impedisce a Windows Spotlight di visualizzare informazioni nella schermata di blocco del dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe mostrare le informazioni di Windows Spotlight nella schermata di blocco.

    [Experience/ConfigureWindowsSpotlightOnLockScreen CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-configurewindowsspotlightonlockscreen)

  - **Suggerimenti di terze parti in Windows Spotlight**: **Blocca** impedisce a Windows Spotlight di suggerire contenuto non pubblicato da Microsoft. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire i suggerimenti di app e contenuti dei partner e mostrare app consigliate nel menu Start e suggerimenti di Windows.

    [Experience/AllowThirdPartySuggestionsInWindowsSpotlight CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowthirdpartysuggestionsinwindowsspotlight)

  - **Funzionalità consumer**: **Blocca** disattiva le esperienze solitamente riservate ai consumer, ad esempio i suggerimenti del menu Start, le notifiche sull'appartenenza, l'installazione di app post-OOBE e i riquadri di reindirizzamento. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.

    [Experience/AllowWindowsConsumerFeatures CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsconsumerfeatures)

  - **Suggerimenti di Windows**: **Blocca** disabilita i suggerimenti di Windows popup. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire la visualizzazione dei suggerimenti di Windows.

    [Experience/AllowWindowsTips CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowwindowstips)

  - **Centro notifiche di Windows Spotlight**: **Blocca** impedisce la visualizzazione di notifiche per Windows Spotlight nel centro notifiche. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe mostrare notifiche nel centro notifiche che suggeriscono app o funzionalità che permettono agli utenti di migliorare la produttività in Windows.

    [Experience/AllowWindowsSpotlightOnActionCenter CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsspotlightonactioncenter)

  - **Personalizzazione di Windows Spotlight**: **Blocca** impedisce a Windows di usare i dati di diagnostica per fornire esperienze personalizzate agli utenti. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire a Microsoft di usare dati di diagnostica per fornire consigli, suggerimenti e offerte personalizzati per adattare Windows alle esigenze dell'utente.

    [Experience/AllowTailoredExperiencesWithDiagnosticData CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowtailoredexperienceswithdiagnosticdata)

  - **Esperienza di Configurazione e personalizzazione di Windows**: **Blocca** consente di disattivare la funzionalità dell'esperienza di Configurazione e personalizzazione di Windows per Windows Spotlight. L'esperienza di Configurazione e personalizzazione di Windows non verrà visualizzata in presenza di aggiornamenti e modifiche per Windows e le relative app. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'esperienza di Configurazione e personalizzazione di Windows che mostra agli utenti informazioni su funzionalità nuove o aggiornate.

    [Experience/AllowWindowsSpotlightWindowsWelcomeExperience CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsspotlightwindowswelcomeexperience)

## <a name="microsoft-defender-antivirus"></a>Microsoft Defender Antivirus

Queste impostazioni usano il [provider di servizi di configurazione per i criteri relativi a Defender](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender), che elenca anche le edizioni di Windows supportate.

- **Monitoraggio in tempo reale**: **Abilita** attiva l'analisi in tempo reale di malware, spyware e altro software indesiderato. Questa opzione non può essere disattivata dagli utenti. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo attiva questa funzionalità e consente agli utenti di modificarla.

  Se questa impostazione viene abilitata e quindi impostata nuovamente su **Non configurato**, Intune lascia l'impostazione nello stato configurato in precedenza.

  Intune non disattiva questa funzionalità. Per disabilitarla, usare un URI personalizzato.

  [Provider di servizi di configurazione Defender/AllowRealtimeMonitoring](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring)

- **Monitoraggio del comportamento**: **Abilita** attiva il monitoraggio del comportamento e controlla la presenza di modelli noti di attività sospette nei dispositivi. Gli utenti non possono disattivare il monitoraggio del comportamento. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe attivare il monitoraggio del comportamento e consentire agli utenti di modificare l'impostazione.

  Se l'impostazione viene abilitata e quindi impostata nuovamente su **Non configurato**, Intune lascia l'impostazione nello stato configurato in precedenza.

  Intune non disattiva questa funzionalità. Per disabilitarla, usare un URI personalizzato.

  [Provider di servizi di configurazione Defender/AllowBehaviorMonitoring](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowbehaviormonitoring)

- **Network Inspection System (NIS)** : consente di proteggere i dispositivi da exploit basati sulla rete. Usa le firme delle vulnerabilità note da Microsoft Endpoint Protection Center per consentire di rilevare e bloccare il traffico dannoso.

  - **Abilita**: attiva la protezione di rete e il blocco della rete. Questa opzione non può essere disattivata dagli utenti. Quando questa funzionalità è abilitata, agli utenti viene impedito di connettersi a vulnerabilità note.

  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo attiva NIS e consente agli utenti di modificare l'impostazione.

  Se l'impostazione viene abilitata e quindi impostata nuovamente su **Non configurato**, Intune lascia l'impostazione nello stato configurato in precedenza.

  Intune non disattiva questa funzionalità. Per disabilitarla, usare un URI personalizzato.

  [Provider di servizi di configurazione Defender/EnableNetworkProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection)

- **Analizza tutti i download**: **Abilita** attiva questa impostazione e Defender analizza tutti i file scaricati da Internet. Gli utenti non possono disattivare questa impostazione. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe attivare questa impostazione e consentire agli utenti di modificarla.

  Se l'impostazione viene abilitata e quindi impostata nuovamente su **Non configurato**, Intune lascia l'impostazione nello stato configurato in precedenza.

  Intune non disattiva questa funzionalità. Per disabilitarla, usare un URI personalizzato.

  [Provider di servizi di configurazione Defender/AllowIOAVProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowioavprotection)

- **Analizza gli script caricati nei Web browser Microsoft**: **Abilita** consente a Defender di analizzare gli script usati in Internet Explorer. Gli utenti non possono disattivare questa impostazione. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe attivare questa impostazione e consentire agli utenti di modificarla.

  Se l'impostazione viene abilitata e quindi impostata nuovamente su **Non configurato**, Intune lascia l'impostazione nello stato configurato in precedenza.

  Intune non disattiva questa funzionalità. Per disabilitarla, usare un URI personalizzato.

  [Provider di servizi di configurazione Defender/AllowScriptScanning](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowscriptscanning)

- **Accesso dell'utente finale a Defender**: **Blocca** nasconde l'interfaccia utente di Microsoft Defender agli utenti. Vengono anche eliminate tutte le notifiche di Microsoft Defender. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe concedere l'accesso utente all'interfaccia utente di Microsoft Defender e consentire agli utenti di modificare l'impostazione.

  Se l'impostazione viene bloccata e quindi impostata nuovamente su **Non configurato**, Intune lascia l'impostazione nello stato configurato in precedenza.

  Intune non disattiva questa funzionalità. Per disabilitarla, usare un URI personalizzato.

  Quando questa impostazione viene modificata, le modifiche diventano effettive a partire dal successivo riavvio del dispositivo.

  [Provider di servizi di configurazione Defender/AllowUserUIAccess](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowuseruiaccess)

- **Intervallo di aggiornamento dell'intelligence sulla sicurezza (in ore)** : immettere l'intervallo con il quale Defender controllerà se è disponibile una nuova intelligence sulla sicurezza, da 0 a 24. Le opzioni disponibili sono:

  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione. L'impostazione predefinita del sistema operativo prevede la verifica della disponibilità degli aggiornamenti ogni 8 ore.
  - **Non controllare**: Defender non controlla se sono disponibili nuovi aggiornamenti dell'intelligence sulla sicurezza.
  - **1-24**: `1` controlla ogni ora `2` controlla ogni due ore, `24` controlla una volta al giorno e così via.
  
  [Provider di servizi di configurazione Defender/SignatureUpdateInterval](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-signatureupdateinterval)
  
- **Monitora l'attività di file e programmi**: Consente a Defender di monitorare l'attività di file e programmi nei dispositivi. Le opzioni disponibili sono:

  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione. L'impostazione predefinita del sistema operativo potrebbe monitorare tutti i file.
  - **Il monitoraggio è disabilitato**
  - **Monitora tutti i file**
  - **Monitora solo i file in ingresso**
  - **Monitora solo i file in uscita**

  [Provider di servizi di configurazione Defender/RealTimeScanDirection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-realtimescandirection)

- **Giorni di attesa prima dell'eliminazione di malware in quarantena**: continua a monitorare il malware risolto per il numero di giorni immesso, in modo che sia possibile controllare manualmente i dispositivi colpiti in precedenza. 

  Se questa impostazione non viene configurata o viene impostata su `0` giorni, il malware rimane nella cartella di quarantena e non viene rimosso automaticamente. Con l'impostazione `90` gli elementi in quarantena vengono archiviati per 90 giorni nel sistema e quindi rimossi.

  [Provider di servizi di configurazione Defender/DaysToRetainCleanedMalware](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-daystoretaincleanedmalware)

- **Limite di utilizzo della CPU durante un'analisi**: consente di limitare la quantità di CPU che le analisi possono usare (da `0` a `100`%). Per impostazione predefinita, il sistema operativo potrebbe impostare il valore su 50%.
- **Analizza file di archivio**: **Abilita** attiva Defender in modo da analizzare i file di archivio, ad esempio file ZIP o CAB. Gli utenti non possono disattivare questa impostazione. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe attivare questa analisi e consentire agli utenti di modificarla.

  Se l'impostazione viene abilitata e quindi impostata nuovamente su **Non configurato**, Intune lascia l'impostazione nello stato configurato in precedenza.

  Intune non disattiva questa funzionalità. Per disabilitarla, usare un URI personalizzato.

  [Provider di servizi di configurazione Defender/AllowArchiveScanning](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowarchivescanning)

- **Analizza i messaggi di posta in arrivo**: **Abilita** consente a Defender di analizzare i messaggi di posta elettronica non appena arrivano nei dispositivi. Quando questa opzione è abilitata, il motore analizza la cassetta postale e i file di posta elettronica per esaminare il corpo dei messaggi e gli allegati. È possibile analizzare i formati .pst (Outlook), .dbx, .mbx, MIME (Outlook Express) e BinHex (Mac).

  Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo disattiva questa analisi e consente agli utenti di modificare l'impostazione.

  Se l'impostazione viene abilitata e quindi impostata nuovamente su **Non configurato**, Intune lascia l'impostazione nello stato configurato in precedenza.

  Intune non disattiva questa funzionalità. Per disabilitarla, usare un URI personalizzato.

  [Provider di servizi di configurazione Defender/AllowEmailScanning](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowemailscanning)

- **Analizza le unità rimovibili durante un'analisi completa**: **Abilita** attiva le analisi delle unità rimovibili da parte di Defender durante un'analisi completa. Gli utenti non possono disattivare questa impostazione. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire a Defender di analizzare le unità rimovibili come le chiavette USB e consentire agli utenti di modificare questa impostazione.

  Se l'impostazione viene abilitata e quindi impostata nuovamente su **Non configurato**, Intune lascia l'impostazione nello stato configurato in precedenza.

  Durante un'analisi veloce, le unità rimovibili possono comunque essere analizzate.

  Intune non disattiva questa funzionalità. Per disabilitarla, usare un URI personalizzato.

  [Provider di servizi di configurazione Defender/AllowFullScanRemovableDriveScanning](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanremovabledrivescanning)

- **Analizza le unità di rete mappate durante un'analisi completa**: con **Abilita** Defender analizza i file nelle unità di rete mappate. Se i file nell'unità sono di sola lettura, Defender non può rimuovere il malware rilevato in tali file. Gli utenti non possono disattivare questa impostazione.

  Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo attiva questa funzionalità e consente agli utenti di modificarla.

  Se l'impostazione viene abilitata e quindi impostata nuovamente su **Non configurato**, Intune lascia l'impostazione nello stato configurato in precedenza. 

  Durante un'analisi veloce, le unità di rete mappate possono comunque essere analizzate.

  Intune non disattiva questa funzionalità. Per disabilitarla, usare un URI personalizzato.

  [Provider di servizi di configurazione Defender/AllowFullScanOnMappedNetworkDrives](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanonmappednetworkdrives)

- **Analizza file aperti da cartelle di rete**: **Abilita** consente a Defender di analizzare i file aperti da cartelle di rete o unità di rete condivise, ad esempio i file a cui si accede da un percorso UNC. Gli utenti non possono disattivare questa impostazione. Se i file nell'unità sono di sola lettura, Defender non può rimuovere il malware rilevato in tali file.

  Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo analizza i file aperti da cartelle di rete e consente agli utenti di modificare l'impostazione.

  Se l'impostazione viene abilitata e quindi impostata nuovamente su **Non configurato**, Intune lascia l'impostazione nello stato configurato in precedenza.

  Intune non disattiva questa funzionalità. Per disabilitarla, usare un URI personalizzato.

  [Provider di servizi di configurazione Defender/AllowScanningNetworkFiles](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowscanningnetworkfiles)

- **Consenti protezione cloud**: **Abilita** attiva Microsoft Active Protection Service per ricevere informazioni sull'attività del malware dai dispositivi gestiti. Gli utenti non possono modificare questa impostazione. 

  Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo consente a Microsoft Active Protection Service di ricevere informazioni e consente agli utenti di modificare questa impostazione.

  Se l'impostazione viene abilitata e quindi impostata nuovamente su **Non configurato**, Intune lascia l'impostazione nello stato configurato in precedenza.

  Intune non disattiva questa funzionalità. Per disabilitarla, usare un URI personalizzato.

  [Provider di servizi di configurazione Defender/AllowCloudProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

- **Richiedi conferma all'utente prima dell'invio di campioni**: determina se i file potenzialmente dannosi che potrebbero richiedere ulteriore analisi devono essere inviati automaticamente a Microsoft. Le opzioni disponibili sono:

  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione. L'impostazione predefinita del sistema operativo prevede l'invio automatico di campioni sicuri.
  - **Chiedi sempre conferma**
  - **Richiedi conferma prima di inviare dati personali**
  - **Non inviare mai dati**
  - **Invia tutti i dati senza chiedere conferma**: i dati vengono inviati automaticamente.

  [Provider di servizi di configurazione Defender/SubmitSamplesConsent](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-submitsamplesconsent)

- **Ora di esecuzione di un'analisi veloce giornaliera**: scegliere l'ora per eseguire un'analisi veloce giornaliera. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe eseguire questa analisi alle 02:00.

  Per una maggiore personalizzazione, configurare l'impostazione **Tipo di analisi di sistema da eseguire**.

  [CSP Defender/ScheduleQuickScanTime](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-schedulequickscantime)

- **Tipo di analisi di sistema da eseguire**: consente di pianificare un'analisi di sistema, inclusi il livello di analisi e il giorno e l'ora in cui eseguire l'analisi. Le opzioni disponibili sono:
  - **Non configurata**: Intune non modifica o aggiorna questa impostazione. nessuna impostazione viene imposta. Gli utenti possono eseguire manualmente le analisi nei dispositivi in base alle proprie esigenze.
  - **Disabilita**: disabilita qualsiasi analisi di sistema nei dispositivi. Scegliere questa opzione se si usa una soluzione antivirus partner che analizza i dispositivi.
  - **Analisi veloce**: esamina i percorsi comuni in cui potrebbe essere presente malware registrato, ad esempio chiavi del Registro di sistema e cartelle di avvio di Windows note.
    - **Giorno pianificato**: scegliere il giorno in cui eseguire l'analisi.
    - **Ora pianificata**: scegliere l'ora in cui eseguire l'analisi.
  - **Analisi completa**: esamina i percorsi comuni in cui potrebbe essere presente malware registrato e analizza anche ogni file e cartella presente nel dispositivo.
    - **Giorno pianificato**: scegliere il giorno in cui eseguire l'analisi.
    - **Ora pianificata**: scegliere l'ora in cui eseguire l'analisi.

  > [!TIP]
  > Questa impostazione potrebbe essere in conflitto con l'impostazione **Ora di esecuzione di un'analisi veloce giornaliera**. Alcuni consigli:  
  >
  > - Se si vuole pianificare un'analisi veloce giornaliera e un'analisi completa settimanale, effettuare le operazioni seguenti:
  >   1. Configurare l'impostazione **Ora di esecuzione di un'analisi veloce giornaliera**.
  >   2. Configurare **Tipo di analisi di sistema da eseguire** impostando un'analisi completa.
  > 
  > - Se si vuole solo un'analisi veloce giornaliera (nessuna analisi completa), usare una delle due impostazioni seguenti: **Ora di esecuzione di un'analisi veloce giornaliera** o **Tipo di analisi di sistema da eseguire**. Ad esempio, per eseguire un'analisi veloce ogni martedì alle 6, configurare l'impostazione **Tipo di analisi di sistema da eseguire**.
  > 
  > - Non configurare l'impostazione **Ora di esecuzione di un'analisi veloce giornaliera** contemporaneamente a **Tipo di analisi di sistema da eseguire** impostato su **Analisi veloce**. Queste impostazioni possono essere in conflitto e l'analisi potrebbe non essere eseguita.

  [CSP Defender/ScanParameter](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-scanparameter)  
  [CSP Defender/ScheduleScanDay](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-schedulescanday)  
  [CSP Defender/ScheduleScanTime](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-schedulescantime)

- **Rileva applicazioni potenzialmente indesiderate**: Questa funzionalità identifica e impedisce il download e l'installazione nella rete di applicazioni potenzialmente indesiderate (PUA). Queste applicazioni non sono considerate virus, malware o altri tipi di minacce. Tuttavia, possono eseguire azioni sugli endpoint e influire sulle prestazioni o sull'utilizzo. Scegliere il livello di protezione quando Windows rileva le PUA. Le opzioni disponibili sono:

  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, Microsoft Defender potrebbe disabilitare questa funzionalità.
  - **Off**: Protezione PUA disattivata.
  - **Abilita**: Microsoft Defender rileva le PUA e gli elementi rilevati vengono bloccati. Questi elementi compaiono nella cronologia insieme alle altre minacce.
  - **Controllo**: Microsoft Defender rileva le PUA ma non esegue alcuna azione. È possibile esaminare le informazioni sulle applicazioni per le quali Microsoft Defender interverrebbe. Ad esempio, cercare gli eventi creati da Microsoft Defender nel Visualizzatore eventi.

  Per altre informazioni sulle app potenzialmente indesiderate, vedere [Rilevare e bloccare le applicazioni potenzialmente indesiderate](https://docs.microsoft.com/windows/threat-protection/windows-defender-antivirus/detect-block-potentially-unwanted-apps-windows-defender-antivirus).

  [Provider di servizi di configurazione Defender/PUAProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-puaprotection)

- **Invia il consenso per i campioni**: attualmente questa impostazione non ha alcun effetto. Non usare questa impostazione. Potrebbe essere rimossa in una delle prossime versioni.

- **Protezione sempre attiva**: **Blocca** impedisce l'analisi dei file aperti o scaricati. Questa opzione non può essere attivata dagli utenti. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe abilitare questa funzionalità e consentire agli utenti di modificarla.

  Se l'impostazione viene bloccata e quindi impostata nuovamente su **Non configurato**, Intune lascia l'impostazione nello stato configurato in precedenza del sistema operativo.

  Intune non attiva questa funzionalità. Per abilitarla, usare un URI personalizzato.

  [CSP Defender/AllowOnAccessProtection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowonaccessprotection)

- **Azioni per le minacce malware rilevate**: selezionare **Abilita** per scegliere le azioni che Defender deve eseguire a seconda del livello di minaccia rilevato: basso, moderato, alto o grave. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire a Microsoft Defender di scegliere l'opzione migliore.

  Quando l'opzione è impostata su **Abilita**, selezionare l'azione:
  
  - **Pulisci**
  - **Quarantena**
  - **Rimuovi**
  - **Consentito**
  - **Definito dall'utente**
  - **Bloccato**

  Se l'azione non è possibile, Microsoft Defender sceglie l'opzione migliore per assicurare che la minaccia venga corretta.

  [Provider di servizi di configurazione Defender/ThreatSeverityDefaultAction](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-threatseveritydefaultaction)

### <a name="microsoft-defender-antivirus-exclusions"></a>Esclusioni di Antivirus Microsoft Defender

È possibile escludere determinati file dalle analisi di Microsoft Defender Antivirus modificando gli elenchi di esclusione. **In genere non è necessario applicare esclusioni**. Microsoft Defender Antivirus include una serie di esclusioni automatiche basate su comportamenti noti del sistema operativo e file di gestione tipici, ad esempio quelli usati nella gestione aziendale, nella gestione dei database e in altri scenari e situazioni aziendali.

> [!WARNING]
> **La definizione di esclusioni riduce la protezione offerta da Microsoft Defender Antivirus**. Valutare sempre i rischi associati all'implementazione di esclusioni. Verificare di escludere solo i file non dannosi.

- **File e cartelle da escludere dalle analisi e dalla protezione in tempo reale**: Aggiunge uno o più file e cartelle come **C:\Percorso** o **%ProgramFiles%\Percorso\nomefile.exe** all'elenco di esclusione. Questi file e cartelle non sono inclusi in alcuna scansione in tempo reale o pianificata.
- **Estensioni di file da escludere dalle analisi e dalla protezione in tempo reale**: Aggiungere uno o più estensioni di file come **jpg** o **txt** all'elenco delle esclusioni. I file con queste estensioni non vengono inclusi nelle analisi in tempo reale o pianificate.
- **Processi da escludere dalle analisi e dalla protezione in tempo reale**: Aggiungere uno o più processi del tipo **.exe**, **.com** o **.scr** all'elenco delle esclusioni. Questi processi non vengono inclusi nelle analisi in tempo reale o nelle analisi pianificate.

## <a name="power-settings"></a>Impostazioni di risparmio energia

Queste impostazioni usano il [provider di servizi di configurazione per i criteri di risparmio di energia](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power), che elenca anche le edizioni di Windows supportate.

### <a name="battery"></a>Batteria

- **Livello di batteria per l'attivazione del risparmio energia**: quando il dispositivo usa l'alimentazione a batteria, immettere il livello di carica della batteria per attivare il risparmio energia (da 0 a 100). Immettere un valore percentuale che indica il livello di carica della batteria. Ad esempio, quando è impostato su `80`, il risparmio di energia si attiva quando la batteria ha una carica disponibile uguale o inferiore all'80%.

  Se non viene inserito un valore, Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe impostare il valore su 70%.

  [Provider di servizi di configurazione Power/EnergySaverBatteryThresholdOnBattery](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-energysaverbatterythresholdonbattery)

- **Chiusura coperchio (solo computer portatili)** : quando il dispositivo usa l'alimentazione a batteria, scegliere cosa accade quando si chiude il coperchio. Le opzioni disponibili sono:

  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di controllare questa impostazione.
  - **Nessuna azione**: il dispositivo rimane acceso e continua a usare l'alimentazione a batteria.
  - **Sospendi**: il dispositivo passa alla modalità sospensione e usa una carica della batteria minima. Il computer è ancora acceso e le app e i file aperti vengono archiviati nella memoria ad accesso casuale (RAM).
  - **Iberna**: il dispositivo passa alla modalità ibernazione. Le app e i file aperti vengono archiviati nel disco rigido e il dispositivo si spegne.
  - **Arresta**: il dispositivo viene arrestato. Le app e i file aperti vengono chiusi senza essere salvati.

  [Provider di servizi di configurazione Power/SelectLidCloseActionOnBattery](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-selectlidcloseactiononbattery)

- **Pulsante di alimentazione**: quando il dispositivo usa l'alimentazione a batteria, scegliere cosa accade quando si seleziona il pulsante di alimentazione. Le opzioni disponibili sono:

  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di controllare questa impostazione.
  - **Nessuna azione**: il dispositivo rimane acceso e continua a usare l'alimentazione a batteria.
  - **Sospendi**: il dispositivo passa alla modalità sospensione e usa una carica della batteria minima. Il computer è ancora acceso e le app e i file aperti vengono archiviati nella memoria ad accesso casuale (RAM).
  - **Iberna**: il dispositivo passa alla modalità ibernazione. Le app e i file aperti vengono archiviati nel disco rigido e il dispositivo si spegne.
  - **Arresta**: il dispositivo viene arrestato. Le app e i file aperti vengono chiusi senza essere salvati.

  [Provider di servizi di configurazione Power/SelectPowerButtonActionOnBattery](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-selectpowerbuttonactiononbattery)

- **Pulsante Sospendi**: quando il dispositivo usa l'alimentazione a batteria, scegliere cosa accade quando si seleziona il pulsante Sospendi. Le opzioni disponibili sono:

  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di controllare questa impostazione.
  - **Nessuna azione**: il dispositivo rimane acceso e continua a usare l'alimentazione a batteria.
  - **Sospendi**: il dispositivo passa alla modalità sospensione e usa una carica della batteria minima. Il computer è ancora acceso e le app e i file aperti vengono archiviati nella memoria ad accesso casuale (RAM).
  - **Iberna**: il dispositivo passa alla modalità ibernazione. Le app e i file aperti vengono archiviati nel disco rigido e il dispositivo si spegne.
  - **Arresta**: il dispositivo viene arrestato. Le app e i file aperti vengono chiusi senza essere salvati.

  [Provider di servizi di configurazione Power/SelectSleepButtonActionOnBattery](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-selectsleepbuttonactiononbattery)

- **Sospensione ibrida**: quando il dispositivo usa l'alimentazione a batteria, scegliere di abilitare o disabilitare la modalità di sospensione ibrida.

  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di controllare questa impostazione.
  - **Abilita**: i dispositivi possono passare alla modalità sospensione ibrida. Le app e i file aperti vengono archiviati nella memoria ad accesso casuale (RAM) e sul disco rigido. Viene usata una carica della batteria minima.
  - **Disabilita**: impedisce ai dispositivi di passare alla modalità di sospensione ibrida.

  [Provider di servizi di configurazione Power/TurnOffHybridSleepOnBattery](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-turnoffhybridsleeponbattery)

### <a name="pluggedin"></a>Alimentazione da rete elettrica

- **Livello di batteria per l'attivazione del risparmio energia**: quando il dispositivo è alimentato da rete elettrica, immettere il livello di carica della batteria per attivare il risparmio energia (da 0 a 100). Immettere un valore percentuale che indica il livello di carica della batteria. Ad esempio, quando è impostato su `80`, il risparmio di energia si attiva quando la batteria ha una carica disponibile uguale o inferiore all'80%.

  Se non viene inserito un valore, Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe impostare il valore su 70%.

  [Provider di servizi di configurazione Power/EnergySaverBatteryThresholdPluggedIn](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-energysaverbatterythresholdpluggedin)

- **Chiusura coperchio (solo computer portatili)** : quando il dispositivo è alimentato da rete elettrica, scegliere cosa accade quando si chiude il coperchio. Le opzioni disponibili sono:

  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione.
  - **Nessuna azione**: il dispositivo rimane acceso.
  - **Sospendi**: il dispositivo passa alla modalità sospensione. Il computer è ancora acceso e le app e i file aperti vengono archiviati nella memoria ad accesso casuale (RAM).
  - **Iberna**: il dispositivo passa alla modalità ibernazione. Le app e i file aperti vengono archiviati nel disco rigido e il dispositivo si spegne.
  - **Arresta**: il dispositivo viene arrestato. Le app e i file aperti vengono chiusi senza essere salvati.
  
    [Provider di servizi di configurazione Power/SelectLidCloseActionPluggedIn](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-selectlidcloseactionpluggedin)
  
- **Pulsante di alimentazione**: quando il dispositivo è alimentato da rete elettrica, scegliere cosa accade quando si seleziona il pulsante di alimentazione. Le opzioni disponibili sono:

  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione.
  - **Nessuna azione**: il dispositivo rimane acceso.
  - **Sospendi**: il dispositivo passa alla modalità sospensione. Il computer è ancora acceso e le app e i file aperti vengono archiviati nella memoria ad accesso casuale (RAM).
  - **Iberna**: il dispositivo passa alla modalità ibernazione. Le app e i file aperti vengono archiviati nel disco rigido e il dispositivo si spegne.
  - **Arresta**: il dispositivo viene arrestato. Le app e i file aperti vengono chiusi senza essere salvati.

  [Provider di servizi di configurazione Power/SelectPowerButtonActionPluggedIn](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-selectpowerbuttonactionpluggedin)

- **Pulsante Sospendi**: quando il dispositivo è alimentato da rete elettrica, scegliere cosa accade quando si seleziona il pulsante Sospendi. Le opzioni disponibili sono:

  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione.
  - **Nessuna azione**: il dispositivo rimane acceso.
  - **Sospendi**: il dispositivo passa alla modalità sospensione. Il computer è ancora acceso e le app e i file aperti vengono archiviati nella memoria ad accesso casuale (RAM).
  - **Iberna**: il dispositivo passa alla modalità ibernazione. Le app e i file aperti vengono archiviati nel disco rigido e il dispositivo si spegne.
  - **Arresta**: il dispositivo viene arrestato. Le app e i file aperti vengono chiusi senza essere salvati.

  [Provider di servizi di configurazione Power/SelectSleepButtonActionPluggedIn](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-selectsleepbuttonactionpluggedin)

- **Sospensione ibrida**: quando il dispositivo è collegato alla rete elettrica, scegliere di abilitare o disabilitare la modalità di sospensione ibrida.

  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di controllare questa impostazione.
  - **Abilita**: i dispositivi possono passare alla modalità sospensione ibrida. Le app e i file aperti vengono archiviati nella memoria ad accesso casuale (RAM) e sul disco rigido.
  - **Disabilita**: impedisce ai dispositivi di passare alla modalità di sospensione ibrida.

  [Provider di servizi di configurazione Power/TurnOffHybridSleepPluggedIn](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-turnoffhybridsleeppluggedin)

## <a name="next-steps"></a>Passaggi successivi

Per altri dettagli tecnici su ogni impostazione e sulle edizioni di Windows supportate, vedere [Windows 10 Policy CSP Reference](https://docs.microsoft.com/windows/client-management/mdm/policy-configuration-service-provider) (Informazioni di riferimento sul provider di servizi di configurazione Policy di Windows 10)

[Assegnare il profilo](device-profile-assign.md) e [monitorarne lo stato](device-profile-monitor.md).
