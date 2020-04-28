---
title: Nuova versione 1610
titleSuffix: Configuration Manager
description: Informazioni dettagliate sulle modifiche e sulle nuove funzionalità introdotte nella versione 1610 di Configuration Manager.
ms.date: 11/23/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f7eb0803-3f8f-4ab6-825a-99ac11f5ba7d
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: d154dc0ba681a37ebb2155bfa1bcdb6d8734965f
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073960"
---
# <a name="what39s-new-in-version-1610-of-configuration-manager"></a>Novità della versione 1610 di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

L'aggiornamento 1610 per Configuration Manager Current Branch è disponibile come aggiornamento nella console per siti precedentemente installati che eseguono la versione 1511, 1602 o 1606.


> [!TIP]  
> Per installare un nuovo sito, è necessario usare una versione base di Configuration Manager.  
>
> Sono disponibili altre informazioni su:    
> - [Installing new sites](https://technet.microsoft.com/library/mt590197.aspx) (Installare nuovi siti)  
> - [Installing updates at sites](https://technet.microsoft.com/library/mt607046.aspx) (Installare aggiornamenti nei siti)  
> - [Baseline and update versions](../../servers/manage/updates.md#bkmk_Baselines) (Versioni di base e di aggiornamento)

Le sezioni seguenti illustrano in dettaglio le modifiche e le nuove funzionalità introdotte nella versione 1610 di Configuration Manager.  


## <a name="in-console-monitoring-of-update-installation-status"></a>Monitoraggio dello stato di installazione dell'aggiornamento nella console  
A partire dalla versione 1610, quando si installa un pacchetto di aggiornamento e si esegue il monitoraggio dell'installazione nella console, viene attivata una nuova fase: la **post-installazione**. Questa fase include lo stato di attività quali il riavvio dei servizi principali e l'inizializzazione del monitoraggio delle repliche. Questa fase è disponibile nella console solo dopo l'aggiornamento del sito alla versione 1610. Per altre informazioni sullo stato di installazione dell'aggiornamento, vedere [Installare gli aggiornamenti nella console](../../servers/manage/install-in-console-updates.md#bkmk_install).


## <a name="exclude-clients-from-automatic-upgrade"></a>Impedire l'aggiornamento automatico dei client
È possibile escludere i client Windows dall'aggiornamento con nuove versioni del software client. Per eseguire questa operazione includere i computer client in una raccolta per la quale è specificata l'esclusione dall'aggiornamento. I client presenti nella raccolta esclusa ignorano le richieste di aggiornamento del software client.  Per altre informazioni, vedere [Escludere i client Windows dagli aggiornamenti](../../clients/manage/upgrade/exclude-clients-windows.md).


## <a name="improvements-for-boundary-groups"></a>Miglioramenti ai gruppi limite
La versione 1610 introduce importanti modifiche ai gruppi di limiti e al loro funzionamento con i punti di distribuzione. Queste modifiche possono semplificare la progettazione dell'infrastruttura del contenuto, offrendo maggiore controllo su come e quando i client eseguono il fallback per la ricerca di punti di distribuzione aggiuntivi come percorsi di origine del contenuto. Sono inclusi i punti di distribuzione in locale e su cloud.
Questi miglioramenti sostituiscono concetti e comportamenti correnti, come la configurazione della velocità o della lentezza dei punti di distribuzione. Il nuovo modello assicura maggiore facilità di configurazione e gestione. Queste modifiche costituiscono anche un presupposto per modifiche future che miglioreranno altri ruoli del sistema del sito associati ai gruppi di limiti.

Durante l'aggiornamento alla versione 1610 le configurazioni dei gruppi di limiti correnti vengono convertite per adattarle al nuovo modello, per evitare che le modifiche alterino le configurazioni di distribuzione del contenuto.

Per altre informazioni, vedere [Gruppi di limiti](../../servers/deploy/configure/boundary-groups.md).


## <a name="peer-cache-for-content-distribution-to-clients"></a>Peer cache per la distribuzione del contenuto ai client
A partire dalla versione 1610, la **peer cache** client consente di gestire la distribuzione di contenuti ai client in posizioni remote. La peer cache è una soluzione di Configuration Manager integrata che consente ai client di condividere i contenuti con altri client direttamente dalla cache locale.

Dopo aver distribuito le impostazioni client che abilitano la peer cache per una raccolta, i membri di tale raccolta possono fungere da origine di contenuto peer per altri client nello stesso gruppo di limiti.

È anche possibile usare il nuovo dashboard **Origini dati del client** per informazioni sull'uso di origini di contenuto peer cache nell'ambiente.

> [!TIP]  
> Con la versione 1610, la peer cache e il dashboard Origini dati del client sono funzionalità di versioni non definitive. Per abilitarle, vedere [Usare le funzionalità di versioni non definitive degli aggiornamenti](../../servers/manage/install-in-console-updates.md#bkmk_prerelease).

Per altre informazioni, vedere [Peer cache per i client di Configuration Manager](../hierarchy/client-peer-cache.md) e [Dashboard Origini dati del client](../../servers/deploy/configure/monitor-content-you-have-distributed.md#client-data-sources-dashboard).


## <a name="migrate-multiple-shared-distribution-points-at-the-same-time"></a>Eseguire la migrazione simultanea di più punti di distribuzione condivisi
È ora possibile usare l'opzione **Riassegna punto di distribuzione** in modo che Configuration Manager elabori in parallelo la riassegnazione simultanea di un massimo di 50 punti di distribuzione condivisi. Prima di questa versione, i punti di distribuzione riassegnati venivano elaborati uno alla volta. Per altre informazioni, vedere, [Eseguire la migrazione simultanea di più punti di distribuzione condivisi](../../migration/planning-a-content-deployment-migration-strategy.md#migrate-multiple-shared-distribution-points-at-the-same-time).

## <a name="cloud-management-gateway-for-managing-internet-based-clients"></a>Gateway di gestione cloud per la gestione di client su Internet

Il gateway di gestione cloud consente di gestire i client di Configuration Manager su Internet in modo semplice. Il servizio gateway di gestione cloud, che viene distribuito in Microsoft Azure e richiede una sottoscrizione di Azure, si connette all'infrastruttura locale di Configuration Manager usando un nuovo ruolo, denominato punto di connessione del gateway di gestione cloud. Dopo che il servizio è stato completamente distribuito e configurato, i client possono comunicare con i ruoli di sistema del sito di Configuration Manager e i punti di distribuzione cloud, indipendentemente dal fatto che siano connessi sulla rete privata interna o su Internet. Per altre informazioni e per confrontare il gateway di gestione cloud con la gestione client su Internet, vedere [Manage clients on the Internet](../../clients/manage/manage-clients-internet.md) (Gestire i client su Internet).

## <a name="improvements-to-the-windows-10-edition-upgrade-policy"></a>Miglioramenti al criterio di aggiornamento edizione di Windows 10
In questa versione sono stati apportati i miglioramenti seguenti a questo tipo di criteri:

- È ora possibile usare i criteri di aggiornamento edizione con PC Windows 10 che eseguono il client di Configuration Manager, oltre che con PC Windows 10 registrati con Microsoft Intune.
- È possibile eseguire l'aggiornamento da Windows 10 Professional a una qualsiasi delle piattaforme nella procedura guidata compatibili con l'hardware in uso.

## <a name="manage-hardware-identifiers"></a>Gestire gli ID hardware
Ora è possibile specificare un elenco di ID hardware che dovranno essere ignorati da Configuration Manager ai fini dell'avvio PXE e della registrazione di client. Questa possibilità contribuisce a risolvere due problemi comuni:

1. Molti dispositivi, ad esempio Surface Pro 3, non sono dotati di una porta Ethernet incorporata. In genere viene usato un adattatore da USB a Ethernet per stabilire una connessione cablata per la distribuzione del sistema operativo. Tuttavia, per motivi di costi e usabilità generale, si tratta spesso di adattatori condivisi. Poiché per identificare il dispositivo viene usato l'indirizzo MAC dell'adattatore, risulta problematico riusare l'adattatore senza interventi aggiuntivi dell'amministratore tra le diverse distribuzioni. In Configuration Manager 1610 è ora possibile escludere l'indirizzo MAC dell'adattatore in modo da poterlo riusare facilmente in questo scenario.
2. L'ID SMBIOS dovrebbe essere un identificatore hardware univoco, ma alcuni dispositivi hardware speciali sono realizzati con ID duplicati. È possibile che questo problema non sia comune come lo scenario dell'adattatore da USB a Ethernet sopra descritto, ma è possibile risolverlo usando l'elenco degli ID hardware esclusi.

Per informazioni dettagliate, vedere [Manage duplicate hardware identifiers](../../clients/manage/manage-clients.md#manage-duplicate-hardware-identifiers) (Gestire gli identificatori hardware duplicati).

## <a name="enhancements-to-windows-store-for-business-integration-with-configuration-manager"></a>Miglioramenti all'integrazione di Windows Store per le aziende con Configuration Manager
Modifiche in questa versione:
- In precedenza, era possibile distribuire solo app gratuite da Windows Store per le aziende. Configuration Manager ora supporta anche la distribuzione di app con licenza online a pagamento (solo per dispositivi registrati con Intune).
- Ora è possibile avviare una sincronizzazione immediata tra Windows Store per le aziende e Configuration Manager.
- È ora possibile modificare la chiave privata del client ottenuta da Azure Active Directory.
- È possibile eliminare una sottoscrizione a Windows Store.

Per informazioni dettagliate, vedere [Gestire le app da Windows Store per le aziende con Configuration Manager](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).


## <a name="policy-sync-for-intune-enrolled-devices"></a>Sincronizzazione criteri per i dispositivi registrati in Intune
È ora possibile richiedere una sincronizzazione dei criteri per un dispositivo registrato in Intune dalla console di Configuration Manager, senza dover richiedere la sincronizzazione dall'app Portale aziendale sul dispositivo stesso. Le informazioni sullo stato della richiesta di sincronizzazione sono disponibili nelle visualizzazioni del dispositivo come nuova colonna, denominata **Remote Sync State** (Stato sincronizzazione remota). Queste informazioni sono disponibili anche nella sezione Dati di individuazione della finestra di dialogo **Proprietà** di ogni dispositivo.


## <a name="use-compliance-settings-to-configure-windows-defender-settings"></a>Usare le impostazioni di conformità per configurare le impostazioni di Windows Defender
È ora possibile configurare le impostazioni del client di Windows Defender nei computer Windows 10 registrati in Intune usando gli elementi di configurazione nella console di Configuration Manager.
Per informazioni dettagliate, vedere la sezione **Windows Defender** in [Creare elementi di configurazione per dispositivi Windows 8.1 e Windows 10 gestiti senza il client Configuration Manager](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).



## <a name="general-improvements-to-software-center"></a>Miglioramenti generali a Software Center
- Gli utenti possono ora richiedere app da Software Center, oltre che dal Catalogo applicazioni.
- Miglioramenti per segnalare agli utenti il software nuovo e importante.

## <a name="new-columns-in-device-collection-views"></a>Nuove colonne nelle visualizzazioni raccolta dispositivi
Ora è possibile visualizzare le colonne **IMEI** e **Numero di serie** (per i dispositivi iOS) nelle visualizzazioni raccolta dispositivi.

## <a name="customizable-branding-for-software-center-dialogs"></a>Personalizzazione delle finestre di dialogo di Software Center
In Configuration Manager versione 1602 è stata introdotta la personalizzazione per Software Center. Nella versione 1610 la personalizzazione viene ora estesa a tutte le finestre di dialogo associate, in modo da offrire agli utenti di Software Center un'esperienza più uniforme.

In Software Center la personalizzazione viene applicata secondo le regole seguenti:

- Se il ruolo del server del sito punto per siti Web del Catalogo applicazioni non è installato, Software Center visualizza il nome dell'organizzazione specificato nell'impostazione **Nome organizzazione visualizzato in Software Center** del client **Agente computer**. Per istruzioni, vedere [Come configurare le impostazioni client](../../clients/deploy/configure-client-settings.md).

- Se il ruolo del server del sito punto per siti Web del Catalogo applicazioni è installato, Software Center visualizza il nome dell'organizzazione e il colore specificati nelle proprietà del ruolo del server del sito punto per siti Web del Catalogo applicazioni. Per altre informazioni, vedere [Configuration options for Application Catalog website point](../../servers/deploy/configure/configuration-options-for-site-system-roles.md#BKMK_ApplicationCatalog_Website) (Opzioni di configurazione per il punto per siti Web del Catalogo applicazioni).

- Se una sottoscrizione di Microsoft Intune è configurata e connessa all'ambiente Configuration Manager, Software Center visualizza il nome dell'organizzazione, il colore e il logo aziendale specificati nelle proprietà della sottoscrizione di Intune.


## <a name="enforcement-grace-period-for-required-application-and-software-update-deployments"></a>Periodo di tolleranza per l'imposizione delle distribuzioni di applicazioni e aggiornamenti software obbligatorie
In alcuni casi, è possibile concedere agli utenti più tempo per l'installazione di distribuzioni di applicazioni o aggiornamenti del software obbligatori, anche oltre eventuali scadenze impostate. Questo accorgimento potrebbe essere opportuno, ad esempio, quando un computer è stato disattivato per un lungo periodo di tempo ed è necessario installare un numero elevato di distribuzioni di applicazioni o aggiornamenti. Ad esempio, se un utente finale è appena tornato da una vacanza, potrebbe dover attendere un po' tempo mentre vengono installate le distribuzioni delle applicazioni scadute. Per risolvere il problema ora è possibile definire un periodo di tolleranza di imposizione distribuendo le impostazioni del client di Configuration Manager a una raccolta. 

Per configurare il periodo di tolleranza eseguire le operazioni seguenti:
1. Nella pagina **Agente computer** delle impostazioni del client configurare la nuova proprietà **Periodo di tolleranza per l'imposizione dopo la scadenza della distribuzione (ore)** con un valore compreso tra **1** e **120** ore.
2. In una nuova distribuzione richiesta dell'applicazione o nelle proprietà di una distribuzione esistente, nella pagina **Pianificazione** selezionare la casella di controllo **Ritardare l'imposizione di questa distribuzione in base alle preferenze dell'utente, fino al periodo di tolleranza massimo definito nelle impostazioni del client**. Tutte le distribuzioni con questa casella di controllo selezionata e destinate a dispositivi in cui è stata distribuita anche l'impostazione del client useranno il periodo di tolleranza per l'imposizione.

Se si configura un periodo di tolleranza di imposizione e si seleziona la casella di controllo, quando si raggiunge la scadenza dell'installazione dell'applicazione, essa verrà installata nella prima finestra non aziendale che l'utente ha configurato fino al periodo di grazia. Tuttavia l'utente può comunque aprire Software Center e installare l'applicazione in qualsiasi momento. Una volta scaduto il periodo di tolleranza, le distribuzioni scadute torneranno al normale comportamento. Opzioni simili sono state aggiunte alla procedura guidata di distribuzione degli aggiornamenti software, alla procedura guidata di creazione delle regole di distribuzione automatica e alle pagine delle proprietà.



## <a name="improved-functionality-in-dialog-boxes-about-required-software"></a>Funzionalità migliorate nelle finestre di dialogo relative al software necessario
Quando si riceve il software necessario, dall'impostazione **Posponi e ricorda tra:** è possibile selezionare un'opzione dall'elenco di valori a discesa seguente: 
- **In seguito**. Specifica che le notifiche vengono pianificate in base alle impostazioni di notifica configurate nell'agente client.
- **Orario fisso**. Specifica che viene pianificata una nuova visualizzazione della notifica dopo l'ora selezionata, ad esempio entro 30 minuti.

![Pagina dell'agente computer nelle impostazioni dell'agente client](media/client-notification-settings.png)

Il tempo di posticipo massimo è basato sui valori di notifica configurati nelle impostazioni dell'agente client. Ad esempio, se l'impostazione nella pagina dell'agente computer **Più di 24 ore alla scadenza di distribuzione. Avvisare l'utente ogni (ore)** è configurata per 10 ore e alla scadenza mancano più di 24 ore, l'utente visualizzerà un set di opzioni di posticipo, ma mai superiori a 10 ore. Con l'avvicinarsi della scadenza saranno disponibili meno opzioni, in accordo con le impostazioni dell'agente client pertinente per ogni componente della cronologia di distribuzione.

Per una distribuzione ad alto rischio, ad esempio una sequenza di attività che distribuisce un sistema operativo, l'esperienza di notifica dell'utente è ora più invasiva. Ogni volta che l'utente viene informato della necessità di manutenzione critica del software, invece di una notifica temporanea sulla barra delle applicazioni, nel computer dell'utente viene visualizzata una finestra di dialogo simile alla seguente:

![Finestra di dialogo del software richiesto](media/client-toast-notification.png)


Per altre informazioni:
- [Impostazioni per gestire le distribuzioni ad alto rischio](../../servers/manage/settings-to-manage-high-risk-deployments.md)
- [Come configurare le impostazioni client](../../clients/deploy/configure-client-settings.md)

## <a name="software-updates-dashboard"></a>Dashboard Aggiornamenti software
Usare il nuovo dashboard Aggiornamenti software per visualizzare lo stato di conformità corrente dei dispositivi dell'organizzazione e analizzare rapidamente i dati per vedere quali dispositivi sono a rischio. Per visualizzare il dashboard, scegliere **Monitoraggio** > **Panoramica** > **Sicurezza** > **Software Updates Dashboard** (Dashboard Aggiornamenti software).

Per informazioni dettagliate, vedere [Monitorare gli aggiornamenti software](../../../sum/deploy-use/monitor-software-updates.md).


## <a name="improvements-to-the-application-request-process"></a>Miglioramenti al processo di richiesta dell'applicazione
Dopo avere approvato un'applicazione per l'installazione, è possibile scegliere di negare la richiesta facendo clic su **Nega** nella console di Configuration Manager. In precedenza questo pulsante era disabilitato dopo l'approvazione.

Questa azione non comporta la disinstallazione dell'applicazione dal dispositivo. Tuttavia, impedisce agli utenti di installare nuove copie dell'applicazione da Software Center.

## <a name="filter-by-content-size-in-automatic-deployment-rules"></a>Filtrare per dimensioni del contenuto nelle regole di distribuzione automatica
È ora possibile filtrare le dimensioni del contenuto per gli aggiornamenti software nelle regole di distribuzione automatica. Ad esempio, per scaricare solo gli aggiornamenti software inferiori a 2 MB, è possibile impostare il filtro **Dimensioni contenuto (KB)** su **< 2048**. Questo filtro impedisce che vengano scaricati in automatico gli aggiornamenti software di grandi dimensioni, al fine di migliorare il supporto della manutenzione Windows semplificata di livello inferiore quando la larghezza di banda è limitata. Per informazioni dettagliate, vedere:
- [Configuration Manager and Simplified Windows Servicing on Down Level Operating Systems](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/) (Configuration Manager e manutenzione Windows semplificata su sistemi operativi di versioni precedenti)
- [Distribuire automaticamente gli aggiornamenti software](../../../sum/deploy-use/automatically-deploy-software-updates.md)

Per configurare il campo **Dimensioni contenuto (KB)** , eseguire una delle operazioni seguenti:
- Quando si crea una regola di distribuzione automatica, nella Creazione regola di distribuzione automatica passare alla pagina **Aggiornamenti software**.
- Nelle proprietà di una regola di distribuzione automatica esistente passare alla scheda **Aggiornamenti software**.

## <a name="office-365-client-management-dashboard"></a>Dashboard di Gestione client di Office 365
Il dashboard di gestione client di Office 365 è ora disponibile nella console di Configuration Manager. Per visualizzare il dashboard, passare a **Raccolta software** > **Panoramica** > **Gestione client di Office 365**.

Nel dashboard vengono visualizzati i grafici per:

- Numero di client di Office 365
- Versioni dei client di Office 365
- Lingue dei client di Office 365
- Canali dei client di Office 365     

Per informazioni dettagliate, vedere [Gestire gli aggiornamenti di Office 365 ProPlus](../../../sum/deploy-use/manage-office-365-proplus-updates.md).

## <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>Passaggi della sequenza di attività per la gestione della conversione da BIOS a UEFI
È ora possibile personalizzare una sequenza di attività di distribuzione del sistema operativo con una nuova variabile, TSUEFIDrive, in modo che il passaggio **Riavvia computer** prepari una partizione FAT32 sul disco rigido per la transizione a UEFI. La procedura seguente fornisce un esempio sulle modalità di creazione dei passaggi della sequenza di attività per preparare il disco rigido alla conversione da BIOS a UEFI. Per informazioni dettagliate, vedere [Passaggi della sequenza di attività per la gestione della conversione da BIOS a UEFI](../../../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md).

##  <a name="improvements-to-the-task-sequence-step-prepare-configmgr-client-for-capture"></a>Miglioramenti al passaggio della sequenza di attività: Prepare ConfigMgr Client for Capture  
Il passaggio Prepara client ConfigMgr a questo punto rimuove completamente il client di Configuration Manager, invece di rimuovere solo le informazioni sulla chiave. Quando la sequenza di attività distribuisce l'immagine del sistema operativo acquisita, verrà installato ogni volta un nuovo client di Configuration Manager. Per informazioni dettagliate, vedere [Passaggi della sequenza di attività](../../../osd/understand/task-sequence-steps.md#BKMK_PrepareConfigMgrClientforCapture).



## <a name="intune-compliance-policy-charts"></a>Grafici dei criteri di conformità di Intune
È ora possibile ottenere una panoramica della conformità generale dei dispositivi e dei motivi principali della non conformità grazie a nuovi grafici, disponibili nell'area di lavoro **Monitoraggio** della console di Configuration Manager. È possibile fare clic su una sezione del grafico per eseguire il drill-down in un elenco dei dispositivi della categoria corrispondente. Per informazioni dettagliate, vedere [Monitorare i criteri di conformità](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).


## <a name="lookout-integration-for-hybrid-implementations-to-protect-ios-and-android-devices"></a>Integrazione di Lookout nelle implementazioni ibride per la protezione di dispositivi iOS e Android
Microsoft si integra con la soluzione di protezione dalle minacce Lookout per proteggere i dispositivi mobili iOS e Android tramite il rilevamento di malware, app rischiose e altre minacce nei dispositivi. La soluzione Lookout consente di determinare il livello di minaccia, che è configurabile. È possibile creare una regola dei criteri di conformità in Configuration Manager per determinare la conformità del dispositivo in base alla valutazione dei rischi di Lookout. Tramite criteri di accesso condizionale, è possibile consentire o bloccare l'accesso alle risorse aziendali in base allo stato di conformità del dispositivo.

Agli utenti dei dispositivi iOS non conformi verrà richiesto di effettuare la registrazione. Verrà inoltre richiesto di installare l'applicazione Lookout for Work, di attivare l'app e di correggere le minacce segnalate da Lookout for Work per poter accedere ai dati aziendali.


## <a name="new-compliance-settings-for-configuration-items"></a>Nuove impostazioni di conformità per gli elementi di configurazione
Sono disponibili molte nuove impostazioni che è possibile usare negli elementi di configurazione relativi a diverse piattaforme per dispositivi. Si tratta di impostazioni che in precedenza esistevano nella configurazione autonoma di Microsoft Intune, rese ora disponibili per Intune con Configuration Manager.
Per informazioni dettagliate, vedere [Elementi di configurazione per dispositivi gestiti senza il client Configuration Manager](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).

### <a name="new-settings-for-android-devices"></a>Nuove impostazioni per i dispositivi Android
#### <a name="password-settings"></a>Impostazioni della password
- **Ricorda cronologia password**
- **Consenti sblocco delle impronte digitali**

#### <a name="security-settings"></a>Impostazioni di sicurezza
- **Richiedi crittografia sulle schede di memoria**
- **Consenti acquisizione schermo**
- **Consenti invio dati di diagnostica**

#### <a name="browser-settings"></a>Impostazioni del browser
- **Consenti browser Web**
- **Consenti riempimento automatico**
- **Consenti blocco popup**
- **Consenti cookie**
- **Consenti scripting**

#### <a name="app-settings"></a>Impostazioni delle app
- **Consenti archivio Google Play**

#### <a name="device-capability-settings"></a>Impostazioni relative alle funzionalità dei dispositivi
- **Consenti archivi rimovibili**
- **Consenti tethering Wi-Fi**
- **Consenti georilevazione**
- **Consenti NFC**
- **Consenti Bluetooth**
- **Consenti roaming vocale**
- **Consenti dati in roaming**
- **Consenti messaggi SMS/MMS**
- **Consenti assistente vocale**
- **Consenti composizione vocale**
- **Consenti copia e incolla**

### <a name="new-settings-for-ios-devices"></a>Nuove impostazioni per i dispositivi iOS
#### <a name="password-settings"></a>Impostazioni della password
- **Numero di caratteri complessi richiesti nella password**
- **Consenti password semplici**
- **Minuti di inattività prima che venga richiesta la password**
- **Ricorda cronologia password**

### <a name="new-settings-for-mac-os-x-devices"></a>Nuove impostazioni per i dispositivi Mac OS X
#### <a name="password-settings"></a>Impostazioni della password
- **Numero di caratteri complessi richiesti nella password**
- **Consenti password semplici**
- **Ricorda cronologia password**
- **Minuti di inattività prima dell'attivazione dello screen saver**

### <a name="new-settings-for-windows-10-desktop-and-mobile-devices"></a>Nuove impostazioni per i dispositivi Windows 10 Desktop e mobili
#### <a name="password-settings"></a>Impostazioni della password
- **Numero minimo di set di caratteri**
- **Ricorda cronologia password**
- **Richiedi una password quando il dispositivo torna attivo dopo uno stato di inattività**

#### <a name="security-settings"></a>Impostazioni di sicurezza
- **Richiedi crittografia sui dispositivi mobili**
- **Consenti l'annullamento della registrazione manuale**

#### <a name="device-capability-settings"></a>Impostazioni relative alle funzionalità dei dispositivi
- **Consenti VPN su rete cellulare**
- **Consenti roaming VPN su rete cellulare**
- **Consenti ripristino del telefono**
- **Consenti connessione USB**
- **Consenti Cortana**
- **Consenti notifiche del Centro operativo**

### <a name="new-settings-for-windows-10-team-devices"></a>Nuove impostazioni per i dispositivi Windows 10 Team
#### <a name="device-settings"></a>Impostazioni del dispositivo
- **Abilita Azure Operational Insights**
- **Abilita proiezione wireless Miracast**
- **Scegli le informazioni sulla riunione visualizzate nella schermata iniziale**
- **URL dell'immagine di sfondo per la schermata di blocco**

### <a name="new-settings-for-windows-81-devices"></a>Nuove impostazioni per i dispositivi Windows 8.1
#### <a name="applicability-settings"></a>Impostazioni di applicabilità
- **Applica tutte le configurazioni a Windows 10**

#### <a name="password-settings"></a>Impostazioni della password
- **Tipo di password richiesto**
- **Numero minimo di set di caratteri**
- **Lunghezza minima password**
- **Numero di errori di accesso ripetuti consentiti prima della cancellazione del dispositivo**
- **Minuti di inattività prima dello spegnimento dello schermo**
- **Scadenza password (giorni)**
- **Ricorda cronologia password**
- **Impedisci riutilizzo delle password precedenti**
- **Consenti password grafica e PIN**

#### <a name="browser-settings"></a>Impostazioni del browser
- **Consenti rilevamento automatico della rete Intranet**

### <a name="new-settings-for-windows-phone-81-devices"></a>Nuove impostazioni per i dispositivi Windows Phone 8.1
#### <a name="applicability-settings"></a>Impostazioni di applicabilità
- **Applica tutte le configurazioni a Windows 10**

#### <a name="password-settings"></a>Impostazioni della password
- **Numero minimo di set di caratteri**
- **Consenti password semplici**
- **Ricorda cronologia password**

#### <a name="device-capability-settings"></a>Impostazioni relative alle funzionalità dei dispositivi
- **Consenti connessione automatica agli hotspot Wi-Fi gratuiti**
