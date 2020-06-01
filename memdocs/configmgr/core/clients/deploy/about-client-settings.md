---
title: Impostazioni client
titleSuffix: Configuration Manager
description: Informazioni sulle impostazioni predefinite e personalizzate per il controllo dei comportamenti client
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: f7560876-8084-4570-aeab-7fd44f4ba737
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 127ed43fded6c66bc4395ae4d69a28ae8c9eddd5
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83877510"
---
# <a name="about-client-settings-in-configuration-manager"></a>Informazioni sulle impostazioni client in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

È possibile gestire tutte le impostazioni client nella console di Configuration Manager dal nodo **Impostazioni client** nell'area di lavoro **Amministrazione**. Con Configuration Manager viene specificato un set di impostazioni predefinite. Quando si modificano le impostazioni client predefinite, tali impostazioni vengono applicate a tutti i client nella gerarchia. È anche possibile configurare le impostazioni client personalizzate, che sostituiscono le impostazioni client predefinite quando le si assegnano a raccolte. Per altre informazioni, vedere [Come configurare le impostazioni client](configure-client-settings.md).

Le sezioni seguenti descrivono le impostazioni e le opzioni in modo dettagliato.  


## <a name="background-intelligent-transfer-service-bits"></a>Servizio trasferimento intelligente in background (BITS)  

### <a name="limit-the-maximum-network-bandwidth-for-bits-background-transfers"></a>Limitare la larghezza di banda di rete massima per i trasferimenti in background BITS

Se questa opzione corrisponde a **Sì**, i client usano la limitazione larghezza di banda BITS. Per configurare le altre impostazioni di questo gruppo, è necessario abilitare questa impostazione.

### <a name="throttling-window-start-time"></a>Ora di inizio dell'intervallo di limitazione

Specificare l'ora di inizio locale per l'intervallo di limitazione BITS.  

### <a name="throttling-window-end-time"></a>Ora di fine dell'intervallo di limitazione

Specificare l'ora di fine locale per l'intervallo di limitazione BITS. Se il valore dell'ora di fine è lo stesso dell'**ora di inizio dell'intervallo di limitazione**, la limitazione BITS è sempre abilitata.  

### <a name="maximum-transfer-rate-during-throttling-window-kbps"></a>Velocità massima di trasferimento durante l'intervallo di limitazione (Kbps)

Specificare la velocità massima di trasferimento che i client possono usare durante l'intervallo.  

### <a name="allow-bits-downloads-outside-the-throttling-window"></a>Consentire i download BITS all'esterno dell'intervallo di limitazione

Consente ai client di usare impostazioni BITS separate all'esterno dell'intervallo specificato.  

### <a name="maximum-transfer-rate-outside-the-throttling-window-kbps"></a>Velocità massima di trasferimento all'esterno dell'intervallo di limitazione (Kbps)

Specifica la velocità massima di trasferimento che i client possono usare al di fuori dell'intervallo di limitazione BITS.  



## <a name="client-cache-settings"></a>Impostazioni della cache dei client

### <a name="configure-branchcache"></a>Configura BranchCache

Configura il computer client per [Windows BranchCache](../../plan-design/configs/support-for-windows-features-and-networks.md#bkmk_branchcache
). Per consentire la memorizzazione nella cache BranchCache nel client, impostare **Abilita BranchCache** su **Sì**.

- **Abilita BranchCache**: Abilita BranchCache nei computer client.

- **Dimensioni massime della cache BranchCache (percentuale del disco)** : Percentuale del disco consentita dall'utente per l'uso da parte di BranchCache.

> [!TIP]
> Se si imposta **Configura BranchCache** su **No**, Configuration Manager non configura le impostazioni di BranchCache.
>
> Per disabilitare BranchCache, impostare **Configura BranchCache** su **Sì** e quindi impostare **Abilita BranchCache** su **No**.<!-- 6244852 -->

### <a name="configure-client-cache-size"></a>Configurare la dimensione della cache del client

Nei computer Windows la cache client di Configuration Manager archivia i file temporanei usati per installare applicazioni e programmi. Se questa opzione è impostata su **No**, il valore predefinito è 5.120 MB.

Se si sceglie **Sì**, specificare:

- **Dimensioni massime della cache (MB)**
- **Dimensioni massime della cache (percentuale del disco)** : La cache del client può raggiungere le dimensioni massime consentite in MB o in percentuale del disco, a seconda di quale di questi due valori è inferiore.

### <a name="enable-as-peer-cache-source"></a>Abilitare come origine di peer cache

> [!Note]  
> Nella versione 1902 e nelle versioni precedenti questa impostazione era denominata **Abilita il client di Configuration Manager nell'intero sistema operativo per condividere i contenuti**. Il comportamento dell'impostazione è rimasto il medesimo.

Abilita la [peer cache](../../plan-design/hierarchy/client-peer-cache.md) per i client di Configuration Manager. Scegliere **Sì** e quindi specificare la porta attraverso la quale il client comunica con il computer peer.

- **Porta per la trasmissione di rete iniziale** (impostazione predefinita UDP 8004): Configuration Manager usa questa porta in Windows PE o nella versione completa del sistema operativo Windows. Il motore della sequenza di attività di Windows PE invia il broadcast per ottenere le posizioni del contenuto prima di avviare la sequenza di attività.<!--SCCMDocs issue 910-->

- **Porta per il download di contenuto da peer** (impostazione predefinita TCP 8003): Configuration Manager configura automaticamente le regole di Windows Firewall in modo che questo tipo di traffico sia consentito. Se si usa un firewall diverso, è necessario configurare le regole manualmente.  

    Per altre informazioni, vedere [Porte usate per le connessioni](../../plan-design/hierarchy/ports.md#BKMK_PortsClient-ClientWakeUp).  

### <a name="minimum-duration-before-cached-content-can-be-removed-minutes"></a>Minimum duration before cached content can be removed (minutes) (Durata minima prima della rimozione del contenuto memorizzato nella cache (minuti))

<!--4485509-->
A partire dalla versione 1906, specificare il tempo minimo di mantenimento del contenuto memorizzato nella cache da parte del client di Configuration Manager. Questa impostazione client definisce la quantità minima di tempo che l'agente di Configuration Manager deve attendere prima di poter rimuovere il contenuto dalla cache se è necessario più spazio.

Per impostazione predefinita, questo valore è impostato su 1.440 minuti (24 ore).
Il valore massimo per questa impostazione è 10.080 minuti (1 settimana).

Questa impostazione offre maggiore controllo sulla cache del client in diversi tipi di dispositivi. È possibile ridurre il valore in client che hanno dischi rigidi di piccole dimensioni e che non devono mantenere il contenuto esistente prima di eseguire un'altra distribuzione.


## <a name="client-policy"></a>Criteri client  

### <a name="client-policy-polling-interval-minutes"></a>Intervallo di polling dei criteri client (minuti)

Specifica la frequenza con cui i client di Configuration Manager seguenti scaricano criteri client:

- Computer Windows (ad esempio, desktop, server, portatili)  
- Dispositivi mobili registrati da Configuration Manager  
- Computer Mac  
- Computer con sistema operativo Linux o UNIX  

Per impostazione predefinita, questo valore è di 60 minuti. Riducendo questo valore, i client eseguono con una maggiore frequenza il polling del sito. Se i client sono numerosi, questo comportamento può avere un impatto negativo sulle prestazioni del sito. Le [istruzioni su dimensioni e scala](../../plan-design/configs/size-and-scale-numbers.md) si basano sul valore predefinito. Aumentando questo valore, i client eseguono meno speso il polling del sito. In caso di modifiche apportate ai criteri del client, tra cui nuove distribuzioni, il download e l'elaborazione richiedono più tempo per i client.<!-- SCCMDocs issue 823 -->

### <a name="enable-user-policy-on-clients"></a>Abilitare i criteri utente nei client

Se si imposta questa opzione su **Sì** e si usa l'[individuazione utente](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser), i client ricevono applicazioni e programmi destinati all'utente connesso.  

Se questa impostazione è **No**, gli utenti non ricevono le applicazioni necessarie distribuite dall'amministratore. Gli utenti non ricevono neanche le altre attività di gestione nei criteri utente.  

Questa impostazione si applica agli utenti i cui computer si trovano nella Intranet o su Internet. Se si vuole che i criteri utente siano abilitati anche su Internet, l'impostazione deve corrispondere a **Sì**.  

> [!Note]  
> A partire dalla versione 1906, i client aggiornati usano automaticamente il punto di gestione per le distribuzioni di applicazioni disponibili per gli utenti. Non è possibile installare nuovi ruoli del Catalogo applicazioni.
>
> Se ancora in uso, il Catalogo applicazioni riceve l'elenco del software disponibile per gli utenti dal server del sito. Per questa ragione, questa impostazione non deve essere **Sì** perché gli utenti possano visualizzare e richiedere applicazioni dal Catalogo applicazioni. Se questa impostazione è **No**, gli utenti non possono installare le applicazioni visualizzate nel Catalogo applicazioni.  

### <a name="enable-user-policy-requests-from-internet-clients"></a>Abilitare le richieste dei criteri utente dai client Internet

Impostare questa opzione su **Sì** se si vuole che gli utenti ricevano i criteri utente nei computer basati su Internet. Devono essere rispettati anche i requisiti seguenti:  

- Il client e il sito devono essere configurati per la [gestione client basata su Internet](../manage/plan-internet-based-client-management.md) o per un [gateway di gestione cloud](../manage/cmg/plan-cloud-management-gateway.md).  

- L'impostazione **Abilitare i criteri utente nei client** deve essere **Sì**.  

- Il punto di gestione basato su Internet deve eseguire l'autenticazione dell'utente tramite l'autenticazione di Windows (Kerberos o NTLM). Per altre informazioni, vedere [Considerazioni per le comunicazioni client da Internet o da una foresta non attendibile](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan).  

- Il gateway di gestione cloud autentica correttamente l'utente tramite Azure Active Directory. Per altre informazioni, vedere [Deploy user-available applications on Azure AD-joined devices](../../../apps/deploy-use/deploy-applications.md#deploy-user-available-applications-on-azure-ad-joined-devices) (Distribuire applicazioni disponibili per l'utente in dispositivi aggiunti ad Azure AD).  

Se si imposta questa opzione su **No** o uno o più dei requisiti precedenti non vengono soddisfatti, un computer connesso a Internet riceve solo criteri computer. In questo scenario gli utenti possono comunque visualizzare, richiedere e installare applicazioni da un Catalogo applicazioni basato su Internet. Se questa impostazione corrisponde a **No**, ma l'opzione **Abilitare i criteri utente nei client** è impostata su **Sì**, gli utenti ricevono i criteri client solo quando il computer è connesso alla Intranet.  

> [!NOTE]  
> Per la gestione client basata su Internet, le richieste di approvazione dell'applicazione da parte degli utenti non richiedono criteri utente o l'autenticazione dell'utente. Cloud Management Gateway non supporta le richieste di approvazione dell'applicazione.  

### <a name="enable-user-policy-for-multiple-user-sessions"></a>Abilitare i criteri utente per più sessioni utente

<!--4737447-->

*Si applica alla versione 1910*

Per impostazione predefinita, questa impostazione è disabilitata. Anche se si abilitano i criteri utente, a partire dalla versione 1906 il client li disabilita per impostazione predefinita su qualsiasi dispositivo che consente più sessioni utente attive simultanee. Ad esempio, server terminal o Windows 10 Enterprise multisessione in [Desktop virtuale Windows](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop).

Il client disabilita i criteri utente solo quando rileva questo tipo di dispositivo durante una nuova installazione. Per i client esistenti di questo tipo che vengono aggiornati alla versione 1906 o successiva, viene mantenuto il comportamento precedente. In un dispositivo esistente l'impostazione dei criteri utente viene configurata anche se il dispositivo consente più sessioni utente.

Se è necessario usare criteri utente e si accettano le potenziali conseguenze sulle prestazioni, abilitare questa impostazione client.


## <a name="cloud-services"></a>Servizi cloud

### <a name="allow-access-to-cloud-distribution-point"></a>Consentire accesso al punto di distribuzione cloud

Impostare questa opzione su **Sì** se si vuole che i client possano ottenere contenuto da un punto di distribuzione cloud. Questa impostazione non richiede che il dispositivo sia basato su Internet.

### <a name="automatically-register-new-windows-10-domain-joined-devices-with-azure-active-directory"></a>Registra automaticamente i nuovi dispositivi Windows 10 aggiunti al dominio con Azure Active Directory

Quando si configura Azure Active Directory per il supporto dell'aggiunta ibrida, Configuration Manager configura i dispositivi Windows 10 per questa funzionalità. Per altre informazioni, vedere [How to configure hybrid Azure Active Directory joined devices](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) (Come configurare dispositivi aggiunti ad Azure Active Directory in modo ibrido).

### <a name="enable-clients-to-use-a-cloud-management-gateway"></a>Consenti ai client di usare un gateway di gestione cloud

Per impostazione predefinita, tutti i client connessi a Internet possono usare qualsiasi [Cloud Management Gateway ](../manage/cmg/plan-cloud-management-gateway.md) disponibile. Un esempio in cui questa impostazione viene configurata su **No** è la necessità di definire un ambito per l'utilizzo del servizio, ad esempio un progetto pilota o la riduzione dei costi.



## <a name="compliance-settings"></a>Impostazioni di conformità  

### <a name="enable-compliance-evaluation-on-clients"></a>Abilitare la valutazione di conformità sui client

Impostare questa opzione su **Sì** per configurare le altre impostazioni di questo gruppo.

### <a name="schedule-compliance-evaluation"></a>Valutazione di conformità della pianificazione

Selezionare **Pianificazione** per creare la pianificazione predefinita per le distribuzioni della linea di base di configurazione. Questo valore può essere configurato per ogni linea di base nella finestra di dialogo **Linea di base configurazione distribuzione**.  

### <a name="enable-user-data-and-profiles"></a>Abilitare i dati e profili utente

Scegliere **Sì** se si vogliono distribuire elementi di configurazione [dati e profili utente](../../../compliance/deploy-use/create-user-data-and-profiles-configuration-items.md).



## <a name="computer-agent"></a>Agente computer  

### <a name="user-notifications-for-required-deployments"></a>Notifiche utente per le distribuzioni richieste

Per altre informazioni sulle tre impostazioni seguenti, vedere [Notifiche utente per le distribuzioni richieste](../../../apps/deploy-use/deploy-applications.md#bkmk_notify):

- **Più di 24 ore alla scadenza di distribuzione. Avvisare l'utente ogni (ore)**
- **Meno di 24 ore alla scadenza di distribuzione. Avvisare l'utente ogni (ore)**
- **Meno di 1 ora alla scadenza di distribuzione. Avvisare l'utente ogni (minuti)**

### <a name="default-application-catalog-website-point"></a>Punto per siti Web del Catalogo applicazioni predefinito

> [!Important]  
> L'esperienza utente di Silverlight per il catalogo applicazioni non è supportata a partire dalla versione Current Branch 1806. A partire dalla versione 1906, i client aggiornati usano automaticamente il punto di gestione per le distribuzioni di applicazioni disponibili per gli utenti. Non è inoltre possibile installare nuovi ruoli del Catalogo applicazioni. Il supporto per i ruoli del Catalogo applicazioni termina con la versione 1910.  
>
> Per altre informazioni, vedere gli articoli seguenti:
>
> - [Configurare Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Funzionalità rimosse e deprecate](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Configuration Manager usa questa impostazione per connettere gli utenti al Catalogo applicazioni dal Software Center. Selezionare **Imposta sito** per specificare un server che ospita il punto per siti Web del Catalogo applicazioni. Immettere il nome NetBIOS o l'FQDN e specificare il rilevamento automatico o un URL per distribuzioni personalizzate. Il rilevamento automatico è la scelta migliore nella maggior parte dei casi.

### <a name="add-default-application-catalog-website-to-internet-explorer-trusted-sites-zone"></a>Aggiungere il sito Web del Catalogo applicazioni predefinito all'area siti attendibili di Internet Explorer

> [!Important]  
> L'esperienza utente di Silverlight per il catalogo applicazioni non è supportata a partire dalla versione Current Branch 1806. A partire dalla versione 1906, i client aggiornati usano automaticamente il punto di gestione per le distribuzioni di applicazioni disponibili per gli utenti. Non è inoltre possibile installare nuovi ruoli del Catalogo applicazioni. Il supporto per i ruoli del Catalogo applicazioni termina con la versione 1910.  
>
> Per altre informazioni, vedere gli articoli seguenti:
>
> - [Configurare Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Funzionalità rimosse e deprecate](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Se questa opzione è impostata su **Sì**, il client aggiunge automaticamente l'URL del sito Web del Catalogo applicazioni predefinito corrente all'area siti attendibili di Internet Explorer.  

Questa impostazione garantisce che l'impostazione di Internet Explorer per Modalità protetta non sia abilitata. Se la modalità protetta è abilitata, il client di Configuration Manager potrebbe non essere in grado di installare applicazioni dal Catalogo applicazioni. Per impostazione predefinita, l'area siti attendibili supporta anche l'accesso utente al Catalogo applicazioni che richiede l'autenticazione di Windows.  

Se si lascia questa opzione impostata su **No**, i client di Configuration Manager potrebbero non essere in grado di installare applicazioni dal Catalogo applicazioni. Un metodo alternativo consiste nel configurare queste impostazioni di Internet Explorer in un'altra area per l'URL del Catalogo applicazioni usata dai client.  

### <a name="allow-silverlight-applications-to-run-in-elevated-trust-mode"></a>Consentire l'esecuzione in modalità di attendibilità elevata delle applicazioni Silverlight

> [!Important]  
> Il client non installa automaticamente Silverlight.
>
> A partire dalla versione 1806, l'**esperienza utente di Silverlight** per il ruolo Punto per siti Web del Catalogo applicazioni non è più supportato. Gli utenti devono usare il nuovo Software Center. Per altre informazioni, vedere [Configurare Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex).  

Per consentire agli utenti di usare il Catalogo applicazioni, è necessario impostare questa opzione su **Sì**.  

L'eventuale modifica di questa impostazione ha effetto al successivo caricamento del browser o aggiornamento della finestra del browser attualmente aperta da parte degli utenti.  

Per altre informazioni su questa impostazione, vedere [Certificati per Microsoft Silverlight 5 e modalità di attendibilità elevata richiesta per il Catalogo applicazioni](../../../apps/plan-design/security-and-privacy-for-application-management.md#BKMK_CertificatesSilverlight5).  

### <a name="organization-name-displayed-in-software-center"></a>Nome organizzazione visualizzato in Software Center

Digitare il nome visualizzato dagli utenti in Software Center. Queste informazioni di personalizzazione consentono agli utenti di identificare questa applicazione come origine attendibile. Per altre informazioni sulla priorità di questa impostazione, vedere [Personalizzazione di Software Center](../../../apps/plan-design/plan-for-software-center.md#branding-software-center).  

### <a name="use-new-software-center"></a>Usa il nuovo Software Center

L'impostazione predefinita è **Sì**.

Se si imposta questa opzione su **Sì**, tutti i computer client useranno Software Center. Software Center visualizza il software, gli aggiornamenti software e le sequenze di attività distribuite a utenti o dispositivi.

### <a name="enable-communication-with-health-attestation-service"></a>Abilita le comunicazioni con il servizio di attestazione dell'integrità

Impostare questa opzione su **Sì** se si vuole che i dispositivi Windows 10 possano usare [Attestazione dell'integrità](../../servers/manage/health-attestation.md). Quando si abilita questa impostazione, è disponibile per la configurazione anche l'impostazione seguente.

### <a name="use-on-premises-health-attestation-service"></a>Usare il servizio di attestazione dell'integrità locale

Impostare questa opzione su **Sì** se si vuole che i dispositivi usino un servizio locale. Impostarla su **No** se si vuole che i dispositivi usino un servizio Microsoft basato sul cloud.  

### <a name="install-permissions"></a>Autorizzazioni di installazione

Configurare la modalità di installazione del software, degli aggiornamenti software e delle sequenze di attività da parte degli utenti:  

- **Tutti gli utenti**: utenti con qualsiasi autorizzazione eccetto Guest.  

- **Solo amministratori**: Gli utenti devono essere membri del gruppo Administrators locale.  

- **Solo amministratori e utenti primari**: gli utenti devono far parte del gruppo Administrators locale o devono essere utenti primari del computer.  

- **Nessun utente**: nessun utente che ha eseguito l'accesso a un computer client può installare il software, gli aggiornamenti software e le sequenze di attività. Le distribuzioni obbligatorie per il computer vengono sempre installate alla scadenza. Gli utenti non possono installare il software da Software Center.  

### <a name="suspend-bitlocker-pin-entry-on-restart"></a>Sospendere immissione PIN di BitLocker al riavvio

Se il computer richiede l'immissione PIN di BitLocker, questa opzione ignora tale richiesta quando il computer viene riavviato dopo l'installazione di software.  

- **Sempre**: Configuration Manager sospende temporaneamente BitLocker dopo aver installato il software che richiede un riavvio e aver iniziato un riavvio del computer. Questa impostazione si applica solo se il riavvio del computer viene avviato da Configuration Manager. Questa impostazione non sospende la richiesta di immissione PIN di BitLocker quando l'utente riavvia il computer. La richiesta di immissione PIN di BitLocker viene ripristinata dopo l'avvio di Windows.

- **Mai**: Configuration Manager non sospende BitLocker dopo l'installazione di software che richiede un riavvio. In questo scenario, l'installazione del software non può terminare fintanto che l'utente non immette il PIN per completare il processo di avvio e caricamento standard di Windows.

### <a name="additional-software-manages-the-deployment-of-applications-and-software-updates"></a>Il software aggiuntivo gestisce la distribuzione delle applicazioni e degli aggiornamenti software

Attivare questa opzione solo in presenza di una delle seguenti condizioni:  

- Si usa una soluzione per fornitori che richiede l'abilitazione di questa impostazione.  

- Per gestire le notifiche dell'agente client e l'installazione delle applicazioni e degli aggiornamenti software, si usa il Software Development Kit (SDK) di Configuration Manager.  

> [!WARNING]  
> - Se si sceglie questa opzione quando non è soddisfatta alcuna di queste condizioni, il client non installa gli aggiornamenti software e le applicazioni necessarie. Questa impostazione non impedisce agli utenti di installare il software disponibile da Software Center, incluse le applicazioni, i pacchetti e le sequenze di attività.  
> -  Quando si abilita questa impostazione, le notifiche di tipo avviso popup per il nuovo software o per il software richiesto non vengono generate nei client. <!--6347668-->

### <a name="powershell-execution-policy"></a>Criteri di esecuzione di PowerShell

Configurare la modalità di esecuzione degli script di Windows PowerShell da parte dei client di Configuration Manager. Questi script possono essere usati per il rilevamento negli elementi di configurazione per le impostazioni di conformità. Possono anche essere inviati in una distribuzione come script standard.  

- **Ignora**: il client di Configuration Manager ignora la configurazione di Windows PowerShell nel computer client per consentire l'esecuzione degli script non firmati.  

- **Con restrizioni**: il client di Configuration Manager usa la configurazione di Windows PowerShell corrente nel computer client. Questa configurazione determina se possono essere eseguiti script non firmati.  

- **Tutti firmati**: il client di Configuration Manager esegue gli script solo se sono firmati da un autore attendibile. Questa restrizione si applica in modo indipendente dalla configurazione di PowerShell corrente nel computer client.  

Questa opzione richiede almeno Windows PowerShell versione 2.0. Il valore predefinito è **Tutti firmati**.  

> [!TIP]  
> Se non è possibile eseguire gli script non firmati a causa di questa impostazione client, Configuration Manager segnala questo errore nei modi seguenti:  
>
> - L'area di lavoro **Monitoraggio** nella console visualizza l'ID errore stato distribuzione **0x87D00327** e la descrizione **Script non firmato**.  
> - I report visualizzano il tipo di errore **Errore di individuazione**, quindi visualizzano il codice di errore **0x87D00327** e la descrizione **Script non firmato** oppure il codice di errore **0x87D00320** e la descrizione **L'host script non è stato ancora installato**. Un report di esempio è: **Dettagli degli errori degli elementi di configurazione in una linea di base configurazione per un asset**.  
> - Il file **DcmWmiProvider.log** visualizza il messaggio **Script non firmato (errore: 87D00327; origine: CCM)** .  

### <a name="show-notifications-for-new-deployments"></a>Mostra notifiche per nuove distribuzioni

Scegliere **Sì** per visualizzare una notifica per le distribuzioni disponibili per meno di una settimana. Questo messaggio viene visualizzato a ogni avvio dell'agente client.

### <a name="disable-deadline-randomization"></a>Disabilitare sequenza casuale scadenza

Dopo la scadenza della distribuzione, questa impostazione determina se il client usa un ritardo di attivazione di un massimo di due ore per installare gli aggiornamenti software obbligatori. Per impostazione predefinita, il ritardo di attivazione è disabilitato.  

Per gli scenari relativi all'infrastruttura VDI, questo ritardo consente di distribuire l'elaborazione della CPU e il trasferimento dei dati per un computer host con più macchine virtuali. Anche se non si usa l'infrastruttura VDI, uno scenario in cui gli stessi aggiornamenti vengono installati contemporaneamente in molti client può determinare un incremento dell'utilizzo della CPU nel server del sito con impatto negativo. Questo comportamento può anche rallentare i punti di distribuzione e ridurre in modo significativo la larghezza di banda di rete disponibile.  

Se i client devono installare gli aggiornamenti software obbligatori alla scadenza della distribuzione senza alcun ritardo, configurare questa impostazione su **Sì**.

### <a name="grace-period-for-enforcement-after-deployment-deadline-hours"></a>Periodo di tolleranza per l'imposizione dopo la scadenza della distribuzione (ore)

Se si vuole concedere agli utenti più tempo per l'installazione delle distribuzioni delle applicazioni o degli aggiornamenti software necessari, impostare un valore per questa opzione. Questo periodo di tolleranza tiene conto dei computer rimasti spenti per molto tempo, i cui utenti devono installare molte distribuzioni di applicazioni o aggiornamenti, come nel caso, ad esempio, di un utente che, tornato da una vacanza, deve attendere parecchio tempo mentre il client installa le distribuzioni di applicazioni scadute.

Impostare un periodo di tolleranza compreso tra 0 e 120 ore. Usare questa impostazione in combinazione con la proprietà di distribuzione **Ritardare l'imposizione di questa distribuzione in base alle preferenze dell'utente**. Per altre informazioni, vedere l'argomento relativo alla [distribuzione delle applicazioni](../../../apps/deploy-use/deploy-applications.md#delay-enforcement-with-a-grace-period).


## <a name="computer-restart"></a>Riavvio del computer

Le impostazioni seguenti devono avere una durata più breve della finestra di manutenzione più breve applicata al computer:

- **Visualizzare una notifica temporanea in cui viene indicato l'intervallo di disconnessione dell'utente o di riavvio del computer (minuti)**
- **Visualizzare una finestra di dialogo che l'utente non può chiudere in cui viene indicato l'intervallo per il conto alla rovescia prima della disconnessione dell'utente o del riavvio del computer (minuti)**


Per altre informazioni sulle finestre di manutenzione, vedere [Come usare le finestre di manutenzione](../manage/collections/use-maintenance-windows.md).

- **Specificare la durata del rinvio per le notifiche con conto alla rovescia per il riavvio del computer (minuti)** (a partire dalla versione 1906)<!--3976435-->
  - Il valore predefinito è 240 minuti.
  - Il valore di durata della sospensione deve essere minore del valore di notifica minimo meno il valore della notifica che l'utente non può ignorare.
  - Per altre informazioni, vedere [Notifiche di riavvio dispositivo](device-restart-notifications.md).

**Quando una distribuzione richiede un riavvio, mostra una finestra di dialogo all'utente invece di un avviso popup**<!--3555947-->: A partire dalla versione 1902, la configurazione di questa impostazione su **Sì** rede più invasiva l'esperienza utente. Questa impostazione si applica a tutte le distribuzioni di applicazioni, sequenze di attività e aggiornamenti software. Per altre informazioni, vedere [Pianificare Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_impact).

> [!IMPORTANT]
> In Configuration Manager 1902, in determinate circostanze, la finestra di dialogo non sostituisce le notifiche di tipo avviso popup. Per risolvere questo problema, installare l'[aggiornamento cumulativo per Configuration Manager versione 1902](https://support.microsoft.com/help/4500571/update-rollup-for-configuration-manager-current-branch-1902). <!--4404715-->


## <a name="delivery-optimization"></a>Ottimizzazione recapito 

<!-- 1324696 -->
I gruppi di limiti di Configuration Manager consentono di definire e regolamentare la distribuzione del contenuto nella rete aziendale e negli uffici remoti. [Ottimizzazione recapito di Windows](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization) è una tecnologia peer-to-peer basata sul cloud per la condivisione di contenuti tra dispositivi Windows 10. Configurare Ottimizzazione recapito in modo che usi i gruppi di limiti per la condivisione di contenuti tra peer.

> [!Note]
> - Ottimizzazione recapito è disponibile solo nei client Windows 10.
> - L'accesso a Internet al servizio cloud Ottimizzazione recapito è un requisito per utilizzare le funzionalità peer-to-peer. Per informazioni sugli endpoint Internet necessari, vedere [Domande frequenti per Ottimizzazione recapito](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions).
> - Quando si usa un CMG per l'archiviazione del contenuto, il contenuto per gli aggiornamenti di terze parti non viene scaricato nei client se è abilitata l'[impostazione client](#allow-clients-to-download-delta-content-when-available) **Consenti ai client di scaricare contenuto differenziale quando disponibile**. <!--6598587--> 

### <a name="use-configuration-manager-boundary-groups-for-delivery-optimization-group-id"></a>Use Configuration Manager Boundary Groups for Delivery Optimization Group ID (Usare i gruppi di limiti di Configuration Manager per l'ID del gruppo di Ottimizzazione recapito)

Scegliere **Sì** per applicare l'identificatore del gruppo di limiti come identificatore di gruppo di Ottimizzazione recapito sul client. Quando il client comunica con il servizio cloud Ottimizzazione recapito, usa questo identificatore per individuare i peer con il contenuto desiderato. L'abilitazione di questa impostazione consente inoltre di impostare la modalità di download di Ottimizzazione recapito sull'opzione Gruppo (2) sui client di destinazione.

> [!Note]
> Microsoft consiglia di consentire al client di configurare questa impostazione tramite criteri locali anziché Criteri di gruppo. Ciò consente di impostare l'identificatore del gruppo di limiti come identificatore di gruppo di Ottimizzazione recapito nel client. Per altre informazioni, vedere [Ottimizzazione recapito](../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization).

### <a name="enable-devices-managed-by-configuration-manager-to-use-microsoft-connected-cache-servers-for-content-download"></a>Abilitare i dispositivi gestiti da Configuration Manager in modo che usino i server di Microsoft Connected Cache per il download dei contenuti

<!--3555764-->
Scegliere **Sì** per consentire ai client di scaricare i contenuti da un punto di distribuzione locale abilitato come server di Microsoft Connected Cache. Per altre informazioni, vedere [Microsoft Connected Cache in Configuration Manager](../../plan-design/hierarchy/microsoft-connected-cache.md).


## <a name="endpoint-protection"></a>Endpoint Protection

> [!Tip]
> Oltre alle informazioni seguenti, è possibile trovare altri dettagli sull'uso delle impostazioni client di Endpoint Protection in [Scenario di esempio: Uso di Endpoint Protection per proteggere i computer dal malware](../../../protect/deploy-use/scenarios-endpoint-protection.md).

### <a name="manage-endpoint-protection-client-on-client-computers"></a>Gestire il client Endpoint Protection nei computer client

Scegliere **Sì** se si vogliono gestire i client di Endpoint Protection e di Windows Defender esistenti nei computer della gerarchia.  

Scegliere questa opzione se il client di Endpoint Protection è già installato e si vuole gestirlo con Configuration Manager. Questa installazione separata include un processo con script che usa un'applicazione di Configuration Manager o un pacchetto e un programma. I dispositivi Windows 10 non richiedono l'installazione dell'agente di Endpoint Protection. Per tali dispositivi deve essere comunque abilitata l'opzione **Gestire il client Endpoint Protection nei computer client**. <!--503654-->

### <a name="install-endpoint-protection-client-on-client-computers"></a>Installare il client Endpoint Protection nei computer client

Scegliere **Sì** per installare e abilitare il client di Endpoint Protection nei computer client in cui non è già in esecuzione. I client Windows 10 non richiedono l'installazione dell'agente di Endpoint Protection.  

> [!NOTE]  
> Se il client di Endpoint Protection è già installato e si sceglie **No**, il client non viene disinstallato. Per disinstallare il client di Endpoint Protection, configurare l'impostazione del client **Gestire il client Endpoint Protection nei computer client** su **No**. In seguito distribuire un pacchetto e programma per disinstallare il client di Endpoint Protection.  

### <a name="allow-endpoint-protection-client-installation-and-restarts-outside-maintenance-windows-maintenance-windows-must-be-at-least-30-minutes-long-for-client-installation"></a>Consentire l'installazione del client di Endpoint Protection e i riavvii al di fuori delle finestre di manutenzione. Le finestre di manutenzione devono avere una durata di almeno 30 minuti per l'installazione del client.

Impostare questa opzione su **Sì** per sostituire i comportamenti di installazione tipici con le finestre di manutenzione. Questa impostazione soddisfa i requisiti aziendali relativi alla priorità della manutenzione del sistema per motivi di sicurezza.

### <a name="for-windows-embedded-devices-with-write-filters-commit-endpoint-protection-client-installation-requires-restarts"></a>Per i dispositivi Windows Embedded con filtri di scrittura, eseguire il commit dell'installazione del client di Endpoint Protection (richiede il riavvio)

Selezionare **Sì** per disabilitare il filtro di scrittura nel dispositivo con Windows Embedded e riavviare il dispositivo. Questa azione conferma l'installazione nel dispositivo.  

Se si seleziona **No**, il client viene installato in una sovrimpressione temporanea che viene cancellata al riavvio del dispositivo. In questo scenario, il client di Endpoint Protection viene installato completamente solo quando un'altra installazione conferma le modifiche al dispositivo. Questa configurazione corrisponde all'impostazione predefinita.  

### <a name="suppress-any-required-computer-restarts-after-the-endpoint-protection-client-is-installed"></a>Evitare il riavvio necessario del computer dopo l'installazione del client Endpoint Protection

Scegliere **Sì** per evitare un riavvio del computer dopo l'installazione del client di Endpoint Protection.  

> [!IMPORTANT]  
> Se il client di Endpoint Protection richiede il riavvio del computer e questa impostazione corrisponde a **No**, il computer viene riavviato indipendentemente da qualsiasi finestra di manutenzione configurata.  

### <a name="allowed-period-of-time-users-can-postpone-a-required-restart-to-complete-the-endpoint-protection-installation-hours"></a>Periodo di tempo consentito agli utenti per rimandare un riavvio necessario per completare l'installazione di Endpoint Protection (ore)

Se dopo l'installazione del client di Endpoint Protection è necessario il riavvio, questa impostazione specifica di quante ore gli utenti possono posticipare il riavvio. Questa impostazione richiede che l'opzione **Evitare il riavvio necessario del computer dopo l'installazione del client Endpoint Protection** sia impostata su **No**.  

### <a name="disable-alternate-sources-such-as-microsoft-windows-update-microsoft-windows-server-update-services-or-unc-shares-for-the-initial-definition-update-on-client-computers"></a>Disabilitare le origini alternative, ad esempio Microsoft Windows Update, Microsoft Windows Server Update Services o condivisioni UNC, per l'aggiornamento iniziale delle definizioni nei computer client

Scegliere **Sì** se si vuole che Configuration Manager installi solo l'aggiornamento della definizione iniziale nei computer client. Questa impostazione può essere utile per evitare connessioni di rete non necessarie e ridurre la larghezza di banda della rete durante l'installazione iniziale dell'aggiornamento delle definizioni.  



## <a name="enrollment"></a>Registrazione

### <a name="polling-interval-for-mobile-device-legacy-clients"></a>Intervallo di polling per client precedenti del dispositivo mobile

Selezionare **Imposta intervallo** per specificare per quanto tempo, in minuti o ore, i dispositivi mobili legacy possono eseguire il polling dei criteri. Questi dispositivi includono piattaforme quali Windows CE, Mac OS X e Unix o Linux.

### <a name="polling-interval-for-modern-devices-minutes"></a>Intervallo di polling per i dispositivi moderni (minuti)

Immettere per quanti minuti i dispositivi moderni possono eseguire il polling dei criteri. Questa impostazione è destinata ai dispositivi Windows 10 gestiti tramite la gestione dei dispositivi mobili locale.

### <a name="allow-users-to-enroll-mobile-devices-and-mac-computers"></a>Consenti agli utenti di registrare i dispositivi mobili e i computer Mac

Per consentire la registrazione dei dispositivi legacy basata sugli utenti, impostare questa opzione su **Sì** e quindi configurare l'impostazione seguente:

- **Profilo di registrazione**: Selezionare **Imposta profilo** per creare o selezionare un profilo di registrazione. Per altre informazioni, vedere [Configurare le impostazioni client per la registrazione](deploy-clients-to-macs.md#configure-client-settings).

### <a name="allow-users-to-enroll-modern-devices"></a>Consenti agli utenti di registrare i dispositivi moderni

Per consentire la registrazione dei dispositivi moderni basata sugli utenti, impostare questa opzione su **Sì** e quindi configurare l'impostazione seguente:

- **Profilo di registrazione per dispositivi moderni**: Selezionare **Imposta profilo** per creare o selezionare un profilo di registrazione. Per altre informazioni, vedere [Creare un profilo di registrazione che consenta agli utenti di registrare i dispositivi moderni](../../../mdm/get-started/set-up-device-enrollment-on-premises-mdm.md#bkmk_createProf).



## <a name="hardware-inventory"></a>Inventario hardware  

### <a name="enable-hardware-inventory-on-clients"></a>Attivare l'inventario hardware nei client

L'impostazione predefinita di questa opzione è **Sì**. Per altre informazioni, vedere [Introduzione all'inventario hardware](../manage/inventory/introduction-to-hardware-inventory.md).

### <a name="hardware-inventory-schedule"></a>Pianificazione inventario hardware

Selezionare **Pianificazione** per regolare la frequenza con cui i client devono eseguire il ciclo di inventario hardware. Per impostazione predefinita, il ciclo viene eseguito ogni sette giorni.

### <a name="maximum-random-delay-minutes"></a>Ritardo casuale massimo (minuti)

Specificare per quanti minuti al massimo il client di Configuration Manager può impostare in modo casuale il ciclo di inventario hardware dalla pianificazione definita. Questa impostazione casuale in tutti i client consente di bilanciare il carico dell'elaborazione dell'inventario nel server del sito. È possibile specificare qualsiasi valore compreso tra 0 e 480 minuti. L'impostazione predefinita è 240 minuti (4 ore).

### <a name="maximum-custom-mif-file-size-kb"></a>Dimensioni massime file MIF personalizzate (KB)

Specificare la dimensione massima consentita, in KB, per ogni file MIF (Management Information Format) personalizzato raccolto dal client durante il ciclo di inventario hardware. L'agente di inventario hardware di Configuration Manager non elabora alcun file MIF personalizzato che superi tali dimensioni. È possibile specificare una dimensione compresa tra 1 KB e 5.120 KB. Per impostazione predefinita, il valore è impostato su 250 KB. Questa impostazione non influisce sulle dimensioni del file di dati di inventario hardware normale.  

> [!NOTE]  
> Questa impostazione è disponibile solo nelle impostazioni del client predefinite.  

### <a name="hardware-inventory-classes"></a>Classi di inventario hardware

Selezionare **Imposta classi** per estendere le informazioni hardware raccolte dai client senza modificare manualmente il file sms_def.mof. Per altre informazioni, vedere [Come configurare l'inventario hardware](../manage/inventory/configure-hardware-inventory.md).  

### <a name="collect-mif-files"></a>Raccogli file MIF

Usare questa impostazione per specificare se raccogliere i file MIF dai client di Configuration Manager durante l'inventario hardware.  

Perché un file MIF venga raccolto dall'inventario hardware, deve trovarsi nel percorso corretto nel computer client. Per impostazione predefinita, i file si trovano nei percorsi seguenti:  

- I **file IDMIF** devono trovarsi nella cartella Windows\System32\CCM\Inventory\Idmif.

- I **file NOIDMIF** devono trovarsi nella cartella Windows\System32\CCM\Inventory\Noidmif.

> [!NOTE]  
> Questa impostazione è disponibile solo nelle impostazioni del client predefinite.



## <a name="metered-internet-connections"></a>Connessioni Internet a consumo  

È possibile gestire la modalità con cui i computer Windows 8 e versioni successive usano connessioni Internet a consumo per comunicare con Configuration Manager. I provider Internet talvolta applicano un addebito per il traffico dati in entrata e in uscita quando si usa una connessione Internet a consumo.  

> [!NOTE]  
> L'impostazione client configurata non viene applicata negli scenari seguenti:  
>
> - Se il computer usa una connessione dati in roaming, il client di Gestione configurazione non esegue alcuna operazione che richieda il trasferimento dei dati nei siti di Configuration Manager.  
> - Se le proprietà di connessione di rete di Windows sono configurate come connessioni non a consumo, il client Gestione configurazione si comporta come se la connessione non fosse a consumo e pertanto trasferisce i dati al sito.  

### <a name="client-communication-on-metered-internet-connections"></a>Comunicazione dei client nelle connessioni Internet a consumo

Per questa impostazione scegliere una delle opzioni seguenti:  

- **Consenti**: tutte le comunicazioni client sono consentite tramite la connessione Internet a consumo, a meno che il dispositivo client usi una connessione dati in roaming.  

- **Limite**: sono consentite solo le comunicazioni client seguenti tramite la connessione Internet a consumo:  

    - Recupero dei criteri client  

    - Messaggi di stato del client da inviare al sito  

    - Richieste di installazione software da Software Center  

    - Distribuzioni richieste (quando viene raggiunta la scadenza per l'installazione)  

    Se il client raggiunge il limite di trasferimento dei dati per la connessione Internet a consumo, non prova più a comunicare con i siti di Configuration Manager.  

- **Blocca**: il client di Configuration Manager non prova a comunicare con i siti di Configuration Manager in presenza di una connessione Internet a consumo. Questa opzione corrisponde all'impostazione predefinita.  

> [!IMPORTANT]  
> Il client consente sempre le installazioni software da Software Center, indipendentemente dalle impostazioni della connessione Internet a consumo. Se l'utente richiede un'installazione software quando il dispositivo è in una rete a consumo, Software Center rispetta la finalità dell'utente.<!-- MEMDocs#285 -->


## <a name="power-management"></a>Risparmio energia  

### <a name="allow-power-management-of-devices"></a>Consentire il risparmio energia dei dispositivi

Impostare questa opzione su **Sì** per abilitare il risparmio energia nei client. Per altre informazioni, vedere [Introduzione alle raccolte](../manage/power/introduction-to-power-management.md).

### <a name="allow-users-to-exclude-their-device-from-power-management"></a>Consentire agli utenti di escludere il dispositivo usato dal risparmio energia

Scegliere **Sì** per consentire agli utenti di Software Center di escludere il computer dalle impostazioni di risparmio energia configurate.  

### <a name="allow-network-wake-up"></a>Consenti l'attivazione della rete

Opzione aggiunta nella versione 1810. Se impostata su **Attiva**, configura le impostazioni di risparmio energia nella scheda di rete per consentire alla scheda di rete di riattivare il dispositivo. Se impostata su **Disattiva**, configura le impostazioni di risparmio energia nella scheda di rete per non consentire alla scheda di rete di riattivare il dispositivo.

### <a name="enable-wake-up-proxy"></a>Abilitare il proxy di riattivazione

Specificare **Sì** per integrare l'impostazione Riattivazione LAN del sito quando è configurata per i pacchetti unicast.  

Per altre informazioni sul proxy di riattivazione, vedere [Pianificare la riattivazione dei client](plan/plan-wake-up-clients.md).  

> [!WARNING]  
> Non abilitare il proxy di riattivazione in una rete di produzione senza prima comprenderne il funzionamento e valutarlo in un ambiente di test.  

Configurare quindi le impostazioni aggiuntive seguenti in base alle esigenze:

- **Numero di porta del proxy di riattivazione (UDP)** : Numero di porta usato dai client per inviare pacchetti di riattivazione ai computer in sospensione. Mantenere la porta predefinita 25536 o modificare il numero con un valore a propria scelta.  

- **Numero di porta di riattivazione LAN (UDP)** : mantenere il valore predefinito 9 a meno che non sia stato modificato il numero di porta di riattivazione LAN (UDP) nelle **Proprietà** del sito nella scheda **Porte**.  

    > [!IMPORTANT]  
    > Questo numero deve corrispondere al numero nelle **Proprietà**del sito. Se si modifica questo numero in una posizione, non viene aggiornato automaticamente nell'altra.  

- **Eccezione di Windows Defender Firewall per il proxy di riattivazione**: Il client di Configuration Manager configura automaticamente il numero di porta del proxy di riattivazione nei dispositivi che eseguono Windows Defender Firewall. Selezionare **Configura** per specificare i profili firewall desiderati.  

    Se i client eseguono un firewall diverso, è necessario configurarlo manualmente per consentire il **Numero di porta del proxy di riattivazione (UDP)** .  

- **Prefissi IPv6 se richiesti per DirectAccess o altri dispositivi di rete. Usare una virgola per specificare più voci**: Immettere i prefissi IPv6 necessari per il funzionamento del proxy di riattivazione nella rete in uso.



## <a name="remote-tools"></a>Strumenti remoti  

### <a name="enable-remote-control-on-clients-and-firewall-exception-profiles"></a>Abilitare controllo remoto nei client e Profili delle eccezioni firewall

Selezionare **Configura** per abilitare la funzionalità di controllo remoto di Configuration Manager. Facoltativamente, configurare le impostazioni del firewall per consentire al controllo remoto di funzionare nei computer client.  

Per impostazione predefinita, il controllo remoto è disattivato.  

> [!IMPORTANT]  
> Se le impostazioni del firewall non sono configurate, il controllo remoto potrebbe non funzionare correttamente.  

### <a name="users-can-change-policy-or-notification-settings-in-software-center"></a>Gli utenti possono modificare le impostazioni di criteri o notifiche in Software Center

Scegliere se gli utenti possono modificare le opzioni di controllo remoto da Software Center.  

### <a name="allow-remote-control-of-an-unattended-computer"></a>Consentire il controllo remoto di un computer senza intervento dell'utente

Scegliere se un amministratore può usare il controllo remoto per accedere a un computer client disconnesso o bloccato. Solo un computer connesso e sbloccato può essere controllato da remoto quando questa impostazione è disattivata.  

### <a name="prompt-user-for-remote-control-permission"></a>Richiedere all'utente l'autorizzazione di controllo remoto

Scegliere se il computer client deve visualizzare un messaggio per richiedere l'autorizzazione dell'utente prima di consentire una sessione di controllo remoto.  

### <a name="prompt-user-for-permission-to-transfer-content-from-shared-clipboard"></a>Richiedere all'utente l'autorizzazione per il trasferimento di contenuto dagli Appunti condivisi

Offre agli utenti la possibilità di accettare o rifiutare il trasferimento di file prima di trasferire il contenuto dagli Appunti condivisi in una sessione di controllo remoto. Gli utenti devono concedere l'autorizzazione una sola volta per sessione. Il visualizzatore non può autorizzare se stesso a trasferire il file.

### <a name="grant-remote-control-permission-to-local-administrators-group"></a>Concedere l'autorizzazione di controllo remoto al gruppo Administrators locale

Scegliere se gli amministratori locali del server che avvia la connessione di controllo remoto possono stabilire sessioni di controllo remoto nei computer client.  

### <a name="access-level-allowed"></a>Livello di accesso consentito

Specificare il livello di accesso di controllo remoto da consentire. Scegliere tra le impostazioni seguenti:  

- **Nessun accesso**
- **Solo visualizzazione**
- **Controllo completo**  

### <a name="permitted-viewers-of-remote-control-and-remote-assistance"></a>Visualizzatori autorizzati di controllo remoto e assistenza remota

Selezionare **Imposta** per specificare i nomi degli utenti Windows che possono stabilire sessioni di controllo remoto per i computer client.  

### <a name="show-session-notification-icon-on-taskbar"></a>Mostra icona di notifica sessione nella barra delle applicazioni

Configurare questa impostazione su **Sì** per indicare una sessione di controllo remoto attiva tramite la visualizzazione di un'icona sulla barra delle applicazioni di Windows del client.  

### <a name="show-session-connection-bar"></a>Mostrare barra delle connessioni sessione

Impostare questa opzione su **Sì** per indicare una sessione di controllo remoto attiva tramite la visualizzazione di una barra di connessione della sessione ad alta visibilità nei client.  

### <a name="play-a-sound-on-client"></a>Riprodurre un suono nel client

Selezionare questa opzione per usare un suono per indicare quando una sessione di controllo remoto è attiva in un computer client. Selezionare una delle opzioni seguenti:

- **Nessun suono**
- **Inizio e fine della sessione** (impostazione predefinita)
- **Ripetutamente nel corso della sessione**  

### <a name="manage-unsolicited-remote-assistance-settings"></a>Gestire le impostazioni di assistenza remota non richiesta

Configurare questa impostazione su **Sì** per consentire a Configuration Manager di gestire le sessioni di assistenza remota non richiesta.  

Nelle sessioni di assistenza remota non richiesta la sessione viene avviata senza che l'utente del computer client abbia richiesto assistenza.  

### <a name="manage-solicited-remote-assistance-settings"></a>Gestire le impostazioni di assistenza remota su richiesta

Impostare questa opzione su **Sì** per consentire a Configuration Manager di gestire le sessioni di assistenza remota richiesta.  

Nelle sessioni di assistenza remota su richiesta l'utente nel computer client ha inviato una richiesta di assistenza remota all'amministratore.  

### <a name="level-of-access-for-remote-assistance"></a>Livello di accesso per assistenza remota

Scegliere il livello di accesso da assegnare alle sessioni di assistenza remota avviate nella console di Configuration Manager. Selezionare una delle opzioni seguenti:

- **Nessuno** (impostazione predefinita)
- **Visualizzazione remota**
- **Controllo completo**

> [!NOTE]  
> L'utente nel computer client deve sempre concedere l'autorizzazione per avviare una sessione di assistenza remota.  

### <a name="manage-remote-desktop-settings"></a>Gestire le impostazioni di desktop remoto

Impostare questa opzione su **Sì** per consentire a Configuration Manager di gestire le sessioni Desktop remoto per i computer.  

### <a name="allow-permitted-viewers-to-connect-by-using-remote-desktop-connection"></a>Consentire ai visualizzatori autorizzati di connettersi mediante connessione desktop remoto

Impostare questa opzione su **Sì** per aggiungere gli utenti specificati nell'elenco di visualizzatori autorizzati al gruppo utenti locale di Desktop remoto nei client.  

### <a name="require-network-level-authentication-on-computers-that-run-windows-vista-operating-system-and-later-versions"></a>Richiedere Autenticazione a livello di rete nei computer che eseguono il sistema operativo Windows Vista e versioni successive

Impostare questa opzione su **Sì** per stabilire connessioni Desktop remoto a computer client tramite Autenticazione a livello di rete (NLA). NLA inizialmente richiede meno risorse del computer remoto perché completa l'autenticazione utente prima di stabilire una connessione Desktop remoto. NLA rappresenta una configurazione più sicura. NLA consente di proteggere il computer da utenti malintenzionati o da software dannoso e riduce il rischio di attacchi Denial of Service.  



## <a name="software-center"></a>Software Center

### <a name="select-these-new-settings-to-specify-company-information"></a>Selezionare le nuove impostazioni per specificare le informazioni aziendali

Impostare questa opzione su **Sì** e quindi specificare le impostazioni seguenti per personalizzare Software Center per l'organizzazione:

- **Nome società**: Immettere il nome dell'organizzazione visualizzato dagli utenti in Software Center.  

- **Combinazione colori per il Software Center**: fare clic su **Seleziona il colore** per definire il colore primario usato da Software Center.  

- **Seleziona un logo per il Software Center**: Fare clic su **Sfoglia** per scegliere un'immagine da visualizzare in Software Center. Il logo deve essere un file JPEG, PNG o BMP di 400 x 100 pixel, con una dimensione massima di 750 KB. Il nome del file del logo non deve contenere spazi.  

### <a name="hide-unapproved-applications-in-software-center"></a><a name="bkmk_HideUnapproved"></a> Nascondi le applicazioni non approvate nel Software Center

Quando si abilita questa opzione, le applicazioni disponibili per l'utente che richiedono l'approvazione sono nascoste in Software Center.<!--1355146-->

### <a name="hide-installed-applications-in-software-center"></a><a name="bkmk_HideInstalled"></a> Nascondi le applicazioni installate in Software Center

Quando si abilita questa opzione, le applicazioni che sono già installate non compaiono più nella scheda Applicazioni. L'opzione abilitata è l'impostazione predefinita quando si installa o si esegue l'aggiornamento a Configuration Manager 1802. Le applicazioni installate sono ancora visualizzabili nella scheda Stato installazione. <!--1357592-->

### <a name="hide-application-catalog-link-in-software-center"></a><a name="bkmk_HideAppCat"></a> Nascondi il collegamento al Catalogo applicazioni in Software Center

Specifica la visibilità del collegamento al sito Web del Catalogo applicazioni in Software Center. Quando questa opzione è impostata, gli utenti non possono visualizzare il collegamento al sito Web del Catalogo applicazioni nel nodo Stato dell'installazione di Software Center. <!--1358214-->

> [!Important]  
> L'esperienza utente di Silverlight per il catalogo applicazioni non è supportata a partire dalla versione Current Branch 1806. A partire dalla versione 1906, i client aggiornati usano automaticamente il punto di gestione per le distribuzioni di applicazioni disponibili per gli utenti. Non è inoltre possibile installare nuovi ruoli del Catalogo applicazioni. Il supporto per i ruoli del Catalogo applicazioni termina con la versione 1910.  

### <a name="software-center-tab-visibility"></a>Visibilità delle schede di Software Center

#### <a name="starting-in-version-1906"></a>A partire dalla versione 1906
<!--4063773-->

Scegliere le schede che devono essere visibili in Software Center. Usare il pulsante **Aggiungi** per spostare una scheda in **Visible tabs** (Schede visibili). Usare il pulsante **Rimuovi** per spostarla nell'elenco  **Hidden tabs** (Schede nascoste). Ordinare le schede usando i pulsanti **Sposta su** o **Sposta giù**. 

Schede disponibili:
- **Applicazioni**
- **Aggiornamenti**
- **Sistemi operativi**
- **Stato installazione**
- **Conformità del dispositivo**
- **Opzioni**
- Aggiungere fino a 5 schede personalizzate facendo clic sul pulsante **Aggiungi la scheda**.
  - Specificare il **Nome della scheda** e l'**URL del contenuto** per la scheda personalizzata.
  - Fare clic su **Elimina la scheda** per rimuovere una scheda personalizzata.  

  >[!Important]  
  > - Alcune funzionalità del sito Web potrebbero non funzionare quando viene usato come scheda personalizzata in Software Center. Assicurarsi di testare i risultati prima di eseguire la distribuzione nei client. <!--519659-->
  > - Specificare indirizzi Web solo attendibili o intranet quando si aggiunge una scheda personalizzata.<!--SCCMDocs issue 1575-->

#### <a name="version-1902-and-earlier"></a>Versione 1902 e precedenti

Configurare le impostazioni aggiuntive di questo gruppo su **Sì** per rendere visibili in Software Center le schede seguenti:

- **Applicazioni**
- **Aggiornamenti**
- **Sistemi operativi**
- **Stato installazione**
- **Conformità del dispositivo**
- **Opzioni**
- **Specifica una scheda personalizzata per Software Center** <!--1358132-->
    - **Nome scheda**
    - **URL del contenuto**

    >[!Important]  
    > Alcune funzionalità del sito Web potrebbero non funzionare quando viene usato come scheda personalizzata in Software Center. Assicurarsi di testare i risultati prima di eseguire la distribuzione nei client. <!--519659-->
    >
    > Specificare indirizzi Web solo attendibili o intranet quando si aggiunge una scheda personalizzata.<!--SCCMDocs issue 1575-->

Se ad esempio l'organizzazione non usa criteri di conformità e si vuole nascondere la scheda Conformità del dispositivo in Software Center, impostare **Abilita la scheda Conformità del dispositivo** su **No**.

### <a name="configure-default-views-in-software-center"></a><a name="bkmk_swctr_defaults"></a> Configurazione delle visualizzazioni predefinite in Software Center
<!--3612112-->
*(Funzionalità introdotta nella versione 1902)*

- Impostare **Filtro predefinito dell'applicazione** per tutte le applicazioni (**Tutti**) o solo per le applicazioni richieste (**Richiesto**).  

  - Software Center usa sempre l'impostazione predefinita. Gli utenti possono modificare questo filtro, ma la preferenza non viene salvata da Software Center.  

- Impostare **Visualizzazione predefinita dell'applicazione** su **Visualizzazione affiancata** o **Visualizzazione elenco**. 

  - Se un utente modifica questa configurazione, Software Center salva la preferenza dell'utente per il futuro. 


## <a name="software-deployment"></a>Distribuzione software  

### <a name="schedule-re-evaluation-for-deployments"></a>Pianificare nuova valutazione per le distribuzioni

Configurare una pianificazione che indichi quando Configuration Manager deve eseguire una nuova valutazione delle regole dei requisiti per tutte le distribuzioni. Il valore predefinito è ogni sette giorni.  

> [!IMPORTANT]  
> Questa impostazione è più invasiva per il client locale rispetto al server di rete o al server del sito. Una pianificazione di rivalutazione più aggressiva influisce negativamente sulle prestazioni della rete e dei computer client. Microsoft non consiglia di impostare un valore inferiore a quello predefinito. Se si modifica questo valore, monitorare attentamente le prestazioni.  

Avviare questa azione da un client scegliendo **Ciclo di valutazione distribuzione applicazione** nella scheda**Azioni** del pannello di controllo di **Configuration Manager**.  



## <a name="software-inventory"></a>Inventario software  

### <a name="enable-software-inventory-on-clients"></a>Abilitare inventario software nei client

L'impostazione predefinita di questa opzione è **Sì**. Per altre informazioni, vedere [Introduzione all'inventario software](../manage/inventory/introduction-to-software-inventory.md).

### <a name="schedule-software-inventory-and-file-collection"></a>Pianificare inventario software e raccolta file

Selezionare **Pianificazione** per regolare la frequenza con cui i client devono eseguire il ciclo di inventario software e quello di raccolta file. Per impostazione predefinita, il ciclo viene eseguito ogni sette giorni.

### <a name="inventory-reporting-detail"></a>Dettaglio report inventario

Specificare uno dei livelli di informazioni seguenti dei file per l'inventario:

- **Solo file**
- **Solo prodotto**
- **Dettagli completi** (impostazione predefinita)

### <a name="inventory-these-file-types"></a>Tipi di file da includere nell'inventario

Per specificare i tipi di file per l'inventario, selezionare **Imposta tipi** e quindi configurare le opzioni seguenti:  

> [!NOTE]  
> Se a un computer vengono applicate più impostazioni client personalizzate, l'inventario restituito da ogni impostazione viene unito.  

- Selezionare **Nuovo** per aggiungere un nuovo tipo di file all'inventario. Specificare quindi le informazioni seguenti nella finestra di dialogo **Proprietà file in inventario**:  

    - **Nome**: specificare un nome per il file che si vuole includere nell'inventario. Usare il carattere jolly asterisco (`*`) per rappresentare qualsiasi stringa di testo e un punto interrogativo (`?`) per rappresentare qualsiasi carattere singolo. Ad esempio, se si vogliono includere nell'inventario tutti i file con estensione doc, specificare il nome del file `*.doc`.  

    - **Location** (Percorso): selezionare **Imposta** per aprire la finestra di dialogo **Proprietà percorso**. Configurare l'inventario software per cercare in tutti i dischi rigidi del client il file specificato, un percorso specifico (ad esempio `C:\Folder`) o una variabile specifica (ad esempio `%windir%`). È anche possibile cercare tutte le sottocartelle nel percorso specificato.  

    - **Escludi file crittografati e compressi**: quando si seleziona questa opzione, tutti i file compressi o crittografati non vengono inclusi nell'inventario.  

    - **Escludi file nella cartella Windows**: quando si seleziona questa opzione, tutti i file nella cartella Windows e nelle relative sottocartelle non vengono inclusi nell'inventario.  

    Scegliere **OK** per chiudere la finestra di dialogo **Proprietà file in inventario**. Aggiungere tutti i file che si vogliono includere nell'inventario e quindi scegliere **OK** per chiudere la finestra di dialogo **Configura impostazione client**.  

### <a name="collect-files"></a>Raccogli file

Se si vogliono raccogliere i file dai computer client, selezionare **Imposta file** e quindi configurare le impostazioni seguenti:  

> [!NOTE]  
> Se a un computer vengono applicate più impostazioni client personalizzate, l'inventario restituito da ogni impostazione viene unito.  

- Nella finestra di dialogo **Configura impostazione client** selezionare **Nuovo** per aggiungere un file da raccogliere.  

- Nella finestra di dialogo **Proprietà file recuperato** immettere le informazioni seguenti:  

    - **Nome**: specificare un nome per il file che si vuole raccogliere. Usare il carattere jolly asterisco (`*`) per rappresentare qualsiasi stringa di testo e un punto interrogativo (`?`) per rappresentare qualsiasi carattere singolo.  

    - **Location** (Percorso): selezionare **Imposta** per aprire la finestra di dialogo **Proprietà percorso**. Configurare l'inventario software per cercare in tutti i dischi rigidi del client il file che si vuole raccogliere, un percorso specifico (ad esempio `C:\Folder`) o una variabile specifica (ad esempio `%windir%`). È anche possibile cercare tutte le sottocartelle nel percorso specificato.  

    - **Escludi file crittografati e compressi**: quando si seleziona questa opzione, i file compressi o crittografati non vengono inclusi nell'inventario.  

    - **Interrompere la raccolta file quando le dimensioni totali dei file superano (KB)** : specificare le dimensioni del file, in kilobyte (KB), oltre le quali il client smette di raccogliere i file specificati.  

    > [!NOTE]  
    > Il server del sito raccoglie le cinque versioni più recenti dei file raccolti e le archivia nella directory `<ConfigMgr installation directory>\Inboxes\Sinv.box\Filecol`. Se dopo l'ultimo ciclo di inventario software un file non è stato modificato, non viene raccolto nuovamente.  
    >
    > L'inventario software non raccoglie file di dimensioni superiori a 20 MB.  
    >
    > Il valore **Dimensioni massime per tutti i file raccolti (KB)** nella finestra di dialogo **Configura impostazione client** visualizza le dimensioni massime per tutti i file raccolti. Quando viene raggiunta questa dimensione, la raccolta file viene interrotta. Tutti i file già raccolti vengono mantenuti e inviati al server del sito.  

    > [!IMPORTANT]
    > Se si configura l'inventario software in modo da raccogliere molti file di grandi dimensioni, questa configurazione può influire negativamente sulle prestazioni del server di rete e del sito.  

    Per informazioni su come visualizzare i file raccolti, vedere [Come usare Esplora inventario risorse per visualizzare l'inventario software](../manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

    Scegliere **OK** per chiudere la finestra di dialogo **Proprietà file recuperato**. Aggiungere tutti i file che si vogliono raccogliere e quindi scegliere **OK** per chiudere la finestra di dialogo **Configura impostazione client**.  

### <a name="set-names"></a>Impostare i nomi

L'agente inventario software recupera i nomi del produttore e del prodotto dalle informazioni di intestazione dei file. Questi nomi non sono sempre standardizzati all'interno di queste informazioni. Quando si visualizza l'inventario software in Esplora inventario risorse, possono essere visualizzate versioni diverse dello stesso nome di produttore o di prodotto. Per standardizzare i nomi visualizzati, selezionare **Imposta nomi** e quindi configurare le impostazioni seguenti:  

- **Tipo nome**: L'inventario software raccoglie informazioni su produttori e prodotti. Scegliere se configurare i nomi visualizzati per un **Produttore** o un **Prodotto**.  

- **Nome visualizzato**: specificare il nome visualizzato da usare al posto dei nomi inclusi nell'elenco **Nomi di inventario**. Per specificare un nuovo nome visualizzato, selezionare **Nuovo**.  

- **Nomi di inventario**: per aggiungere un nome di inventario, selezionare **Nuovo**. Questo nome viene sostituito nell'inventario software dal nome scelto nell'elenco **Nome visualizzato**. È possibile aggiungere più nomi da sostituire.  



## <a name="software-metering"></a>Controllo software

### <a name="enable-software-metering-on-clients"></a>Abilitare controllo software nei client

Questa impostazione corrisponde a **Sì** per impostazione predefinita. Per altre informazioni, vedere [Controllo del software](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md#configure-software-metering).

### <a name="schedule-data-collection"></a>Pianifica raccolta dati

Selezionare **Pianificazione** per regolare la frequenza con cui i client devono eseguire il ciclo di misurazione del software. Per impostazione predefinita, il ciclo viene eseguito ogni sette giorni.



## <a name="software-updates"></a>Aggiornamenti software  

### <a name="enable-software-updates-on-clients"></a>Abilitare aggiornamento software nei client

Usare questa impostazione per abilitare gli aggiornamenti software nei client di Configuration Manager. Quando si disabilita questa opzione, Configuration Manager rimuove i criteri di distribuzione esistenti dai client. Quando si riattiva questa impostazione, il client scaricherà il criterio di distribuzione corrente.  

> [!IMPORTANT]  
> Quando si deseleziona questa impostazione, i criteri di conformità basati sugli aggiornamenti software non funzioneranno più.  

### <a name="software-update-scan-schedule"></a>Pianificazione analisi aggiornamento software

Selezionare **Pianificazione** per specificare la frequenza con cui il client avvia un'analisi di valutazione conformità. Questa analisi determina lo stato degli aggiornamenti software nel client (ad esempio, aggiornamento obbligatorio o installato). Per altre informazioni sulla valutazione della conformità, vedere [Valutazione della conformità negli aggiornamenti software](../../../sum/understand/software-updates-introduction.md#BKMK_SUMCompliance).  

Per impostazione predefinita, questa analisi usa una pianificazione semplice da avviare ogni sette giorni. È possibile creare una pianificazione personalizzata. È possibile specificare una data e un'ora di avvio specifiche, usare l'ora UTC o l'ora locale e configurare l'intervallo ricorrente per un giorno specifico della settimana.  

> [!NOTE]  
> Se si specifica un intervallo inferiore a un giorno, Configuration Manager usa automaticamente il valore pari a un giorno come impostazione predefinita.  

> [!WARNING]  
> L'ora di avvio effettiva nei computer client corrisponde all'ora di avvio con l'aggiunta di una quantità di tempo casuale, fino a un massimo di due ore. Questa impostazione casuale impedisce ai computer client di avviare l'analisi e contemporaneamente di connettersi al punto di aggiornamento software attivo.  

### <a name="schedule-deployment-re-evaluation"></a>Pianificare nuova valutazione di distribuzione

Selezionare **Pianificazione** per configurare la frequenza di esecuzione della valutazione degli aggiornamenti software da parte dell'agente client aggiornamenti software per la verifica dello stato di installazione nei computer client di Configuration Manager. Se gli aggiornamenti software installati in precedenza non sono più presenti nei client ma sono ancora necessari, il client li reinstalla.

Regolare la pianificazione in base ai criteri aziendali di conformità degli aggiornamenti software e in base al fatto che gli utenti possano disinstallare o meno gli aggiornamenti software. Ogni ciclo di rivalutazione della distribuzione comporta attività del processore del computer client e della rete. Per impostazione predefinita, questa impostazione usa una pianificazione semplice per avviare la rivalutazione della distribuzione ogni sette giorni.  

> [!NOTE]  
> Se si specifica un intervallo inferiore a un giorno, Configuration Manager usa automaticamente il valore pari a un giorno come impostazione predefinita.  

### <a name="when-any-software-update-deployment-deadline-is-reached-install-all-other-software-update-deployments-with-deadline-coming-within-a-specified-period-of-time"></a>Quando viene raggiunta la scadenza di una distribuzione di aggiornamenti software, installare tutte le altre distribuzioni di aggiornamenti software con scadenza entro un periodo di tempo specificato

Impostare questa opzione su **Sì** per installare tutti gli aggiornamenti software da distribuzioni obbligatorie con scadenze che rientrano in un periodo di tempo specifico. Quando la distribuzione di aggiornamenti software obbligatori raggiunge la scadenza, il client avvia l'installazione degli aggiornamenti software nella distribuzione. Questa impostazione determina se installare aggiornamenti software da altre distribuzioni obbligatorie con una scadenza compresa nel periodo specificato.  

Usare questa impostazione per accelerare l'installazione di aggiornamenti software obbligatori. Questa impostazione potrebbe anche aumentare la sicurezza dei client, ridurre il numero di notifiche inviate all'utente e diminuire i riavvi dei client. Per impostazione predefinita, questa impostazione è impostata su **No**.  

### <a name="period-of-time-for-which-all-pending-deployments-with-deadline-in-this-time-will-also-be-installed"></a>Periodo di tempo entro cui verranno installate anche tutte le distribuzioni in sospeso con scadenza in questo periodo

Usare questa impostazione per specificare il periodo di tempo per l'impostazione precedente. È possibile immettere un valore compreso tra 1 e 23 ore e tra 1 e 365 giorni. Per impostazione predefinita, questa impostazione è configurata su sette giorni.  

### <a name="allow-clients-to-download-delta-content-when-available"></a>Consenti ai client di scaricare contenuto differenziale quando disponibile

*(Funzionalità introdotta nella versione 1902)*

Impostare questa opzione su **Sì** per consentire ai client di usare file di contenuto differenziale. Questa impostazione consente all'agente di Windows Update sul dispositivo di determinare il contenuto necessario e di scaricarlo in modo selettivo. 

- Prima di abilitare questa impostazione client, verificare che la funzionalità Ottimizzazione recapito sia configurata in modo appropriato per l'ambiente in uso. Per altre informazioni, vedere [Ottimizzazione recapito di Windows](../../../sum/deploy-use/optimize-windows-10-update-delivery.md#windows-delivery-optimization) e l'[impostazione client Ottimizzazione recapito](#delivery-optimization).
 - Questa impostazione client sostituisce **Abilita l'installazione di file per l'installazione rapida nei client**. Impostare questa opzione su **Sì** per consentire ai client di usare file di installazione rapida. Per altre informazioni, vedere [Gestire i file di installazione rapida per gli aggiornamenti di Windows 10](../../../sum/deploy-use/manage-express-installation-files-for-windows-10-updates.md).
 - A partire da Configuration Manager versione 1910, se questa opzione è impostata, il download del contenuto differenziale viene usato per tutti i file di installazione di Windows Update, non solo per i file di installazione rapida.
    - Quando si usa un CMG per l'archiviazione del contenuto, il contenuto per gli aggiornamenti di terze parti non viene scaricato nei client se è abilitata l'impostazione client **Consenti ai client di scaricare contenuto differenziale quando disponibile**. <!--6598587--> 


### <a name="port-that-clients-use-to-receive-requests-for-delta-content"></a>Porta usata dai client per ricevere richieste per contenuto differenziale

*(Funzionalità introdotta nella versione 1902)*

Questa impostazione consente di configurare la porta locale per il listener HTTP per il download del contenuto differenziale. Per impostazione predefinita, corrisponde a 8005. Non è necessario aprire questa porta nel firewall client. 

> [!NOTE]
>Questa impostazione client sostituisce **Porta usata per scaricare contenuto per i file per l'installazione rapida**.


### <a name="enable-management-of-the-office-365-client-agent"></a>Abilitare la gestione dell'agente del client Office 365

Impostare questa opzione su **Sì** per consentire la configurazione delle impostazioni di installazione di Office 365. Questa opzione consente anche il download di file dalle reti per la distribuzione di contenuti (CDN) di Office e la distribuzione dei file come applicazione in Configuration Manager. Per altre informazioni, vedere [Gestire gli aggiornamenti di Office 365 ProPlus](../../../sum/deploy-use/manage-office-365-proplus-updates.md).

### <a name="enable-installation-of-software-updates-in-all-deployments-maintenance-window-when-software-update-maintenance-window-is-available"></a><a name="bkmk_SUMMaint"></a> Consenti l'installazione degli aggiornamenti software nella finestra di manutenzione "Tutte le distribuzioni" quando la finestra di manutenzione "Aggiornamento software" è disponibile

A partire dalla versione 1810, quando si imposta questa opzione su **Sì** e per il client è stata definita almeno una finestra di manutenzione "Aggiornamento software", gli aggiornamenti software verranno installati durante una finestra di manutenzione "Tutte le distribuzioni".

Per impostazione predefinita, questa impostazione è impostata su **No**. Questo valore applica il comportamento precedente: se esistono entrambi i tipi, ignorerà la finestra. <!--2839307-->

> [!NOTE]
> Questa impostazione si applica anche alle finestre di manutenzione configurate per l'applicazione a **Sequenze di attività**.<!-- SCCMDocs-pr #4596 -->
>
> Se ha una sola finestra **Tutte le distribuzioni** disponibile, il client installa comunque gli aggiornamenti software o le sequenze di attività nella finestra.

#### <a name="maintenance-window-example"></a>Esempio di finestre di manutenzione

È ad esempio possibile configurare le finestre di manutenzione seguenti:

- **Distribuzione completa**: 02:00 - 04:00
- **Aggiornamenti software**: 04:00 - 06:00

Per impostazione predefinita, il client installa gli aggiornamenti software solo durante la seconda finestra di manutenzione. Ignora la finestra di manutenzione per tutte le distribuzioni in questo scenario. Quando si imposta questa opzione su **Sì**, il client installa gli aggiornamenti software nell'intervallo di tempo compreso tra le 02.00 e le 06.00.


### <a name="specify-thread-priority-for-feature-updates"></a><a name="bkmk_thread-priority"></a> Specificare la priorità del thread per gli aggiornamenti delle funzionalità

<!--3734525-->
A partire da Configuration Manager versione 1902, è possibile modificare la priorità con cui i client Windows 10 versione 1709 o versioni successive installano un aggiornamento di funzionalità tramite [pacchetti di manutenzione di Windows 10](../../../osd/deploy-use/manage-windows-as-a-service.md). Questa impostazione non influisce sulle sequenze di attività di aggiornamento sul posto di Windows 10.

Questa impostazione client include le opzioni seguenti:

- **Non configurato**: Configuration Manager non cambia l'impostazione. Gli amministratori possono pre-installare un proprio file setupconfig.ini. Questo è il valore predefinito.

- **Normale**: Installazione di Windows usa più risorse di sistema ed effettua l'aggiornamento più velocemente. Usa più tempo processore e quindi il tempo totale di installazione è più breve, ma l'interruzione per l'utente è più lunga.  

    - Consente di configurare il file setupconfig.ini nel dispositivo con l'[opzione della riga di comando di installazione di Windows `/Priority Normal`](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options).

- **Bassa**: è possibile continuare a usare il dispositivo durante il download e l'applicazione degli aggiornamenti in background. Il tempo totale di installazione è più lungo, ma l'interruzione per l'utente è più breve. Potrebbe essere necessario aumentare il tempo di esecuzione massimo dell'aggiornamento per evitare un timeout quando si usa questa opzione.  

    - Rimuove l'[opzione della riga di comando di installazione di Windows `/Priority`](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options) dal file setupconfig.ini.


### <a name="enable-third-party-software-updates"></a>Enable third party software updates (Abilita aggiornamenti software di terze parti)

Se questa opzione è impostata su **Sì**, vengono impostati i criteri per **Consenti aggiornamenti firmati da un percorso del servizio di aggiornamento Microsoft nella rete Intranet** e il certificato di firma viene installato nell'archivio degli autori attendibili nel client.

### <a name="enable-dynamic-update-for-feature-updates"></a><a name="bkmk_du"></a>Abilitare l'aggiornamento dinamico per gli aggiornamenti delle funzionalità
<!--4062619-->
A partire da Configuration Manager versione 1906, è possibile configurare l'[aggiornamento dinamico per Windows 10](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/The-benefits-of-Windows-10-Dynamic-Update/ba-p/467847). L'aggiornamento dinamico installa i language pack, le funzionalità su richiesta, i driver e gli aggiornamenti cumulativi durante l'installazione di Windows indicando al client di scaricare questi aggiornamenti da Internet. Quando questa impostazione è impostata su **Sì** o **No**, Configuration Manager modifica il file [setupconfig](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options) usato durante l'installazione dell'aggiornamento delle funzionalità.

- **Non configurato**: il valore predefinito. Non vengono apportate modifiche al file setupconfig.
  - L'aggiornamento dinamico è abilitato per impostazione predefinita in tutte le versioni supportate di Windows 10.
    - Per Windows 10 versioni 1803 e precedenti, l'aggiornamento dinamico ricerca nel server WSUS del dispositivo gli aggiornamenti dinamici approvati. Poiché negli ambienti Configuration Manager gli aggiornamenti dinamici non vengono mai approvati direttamente nel server WSUS, questi dispositivi non li installano.
    - A partire da Windows 10 versione 1809, l'aggiornamento dinamico usa la connessione Internet del dispositivo per ottenere gli aggiornamenti dinamici da Microsoft Update. Questi aggiornamenti dinamici non sono pubblicati per l'uso di WSUS.
- **Sì**: abilita l'aggiornamento dinamico.
- **No**: disabilita l'aggiornamento dinamico.


## <a name="state-messaging"></a>Messaggistica di stato

### <a name="state-message-reporting-cycle-minutes"></a>Ciclo di segnalazione messaggi di stato (minuti)

Specifica la frequenza con cui i client segnalano i messaggi di stato. Per impostazione predefinita, questa impostazione corrisponde a 15 minuti.



## <a name="user-and-device-affinity"></a>Affinità utente-dispositivo  

### <a name="user-device-affinity-usage-threshold-minutes"></a>Soglia di utilizzo di affinità utente dispositivo (minuti)

Specificare il numero di minuti prima della creazione di un mapping di affinità del dispositivo utente da parte di Configuration Manager. Per impostazione predefinita, questo valore è impostato su 2880 minuti (due giorni).

### <a name="user-device-affinity-usage-threshold-days"></a>Soglia di utilizzo di affinità utente dispositivo (giorni)

Specificare il numero di giorni in cui il client misura la soglia di affinità del dispositivo in base all'utilizzo. Per impostazione predefinita, questo valore è impostato su 30 giorni.

> [!NOTE]  
> È ad esempio possibile impostare **Soglia di utilizzo di affinità utente dispositivo (minuti)** su **60** minuti e **Soglia di utilizzo di affinità utente dispositivo (giorni)** su **5** giorni. L'utente deve quindi usare il dispositivo per 60 minuti in un periodo di 5 giorni per creare affinità automatica con il dispositivo.  

### <a name="automatically-configure-user-device-affinity-from-usage-data"></a>Configurare automaticamente l'affinità utente dispositivo dai dati di utilizzo

Scegliere **Sì** per creare automaticamente affinità utente-dispositivo in base alle informazioni sull'utilizzo raccolte da Configuration Manager.  

### <a name="allow-user-to-define-their-primary-devices"></a>Consentire all'utente di definire i dispositivi primari
<!--3485366-->
Se questa opzione è impostata su **Sì**, gli utenti possono identificare i propri dispositivi primari in Software Center. Per altre informazioni, vedere il [Manuale dell'utente di Software Center](../../understand/software-center.md#work-information).

## <a name="windows-analytics"></a>Windows Analytics

> [!Important]  
> Il servizio Windows Analytics è stato ritirato il 31 gennaio 2020. Per altre informazioni, vedere [KB 4521815: Ritiro di Windows Analytics il 31 gennaio 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement).
>
> Desktop Analytics è l'evoluzione di Windows Analytics. Per altre informazioni, vedere [Che cos'è Desktop Analytics](../../../desktop-analytics/overview.md).
