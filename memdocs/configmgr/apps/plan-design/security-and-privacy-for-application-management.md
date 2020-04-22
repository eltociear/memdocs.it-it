---
title: Sicurezza e privacy per le app
titleSuffix: Configuration Manager
description: Indicazioni e consigli per la sicurezza e la privacy nella gestione delle applicazioni in Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 4d26deed-3b16-4116-b640-f618f2c20f5a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7f7085b7ee6f0f723c9bcf9d10cb85b03f990a44
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689069"
---
# <a name="security-and-privacy-for-application-management-in-configuration-manager"></a>Sicurezza e privacy per la gestione delle applicazioni in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

## <a name="security-guidance-for-application-management"></a>Indicazioni sulla sicurezza per la gestione delle applicazioni  

### <a name="use-the-software-center-without-the-application-catalog"></a>Usare Software Center senza il Catalogo applicazioni

<!--1358309-->

L'esperienza utente di Silverlight per il catalogo applicazioni non è supportata a partire dalla versione Current Branch 1806. Questa configurazione consente di ridurre l'infrastruttura server necessaria per distribuire le applicazioni agli utenti.

A partire dalla versione 1906, i client aggiornati usano automaticamente il punto di gestione per le distribuzioni di applicazioni disponibili per gli utenti. Non è inoltre possibile installare nuovi ruoli del Catalogo applicazioni. Il supporto per i ruoli del Catalogo applicazioni termina con la versione 1910. Riducendo l'infrastruttura server si riduce anche la superficie di attacco.

Per offrire un'esperienza dell'applicazione coerente e sicura per i client basati su Internet, usare Azure Active Directory e il gateway di gestione cloud.

Per altre informazioni, vedere [Configurare Software Center](plan-for-software-center.md#bkmk_userex).

### <a name="use-https-with-the-application-catalog"></a>Usare HTTPS con il Catalogo applicazioni

> [!Important]  
> Il supporto per i ruoli del Catalogo applicazioni termina con la versione 1910. Per altre informazioni, vedere [Rimuovere il catalogo applicazioni](plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

Configurare il punto per siti Web del Catalogo applicazioni e il punto per servizi Web del Catalogo applicazioni per accettare le connessioni HTTPS. Con questa configurazione, il server viene autenticato agli utenti. I dati trasmessi sono protetti da manomissioni e visualizzazioni.

Impedire attacchi di ingegneria sociale istruendo gli utenti a connettersi esclusivamente a siti Web attendibili. Informare gli utenti sui pericoli dei siti Web dannosi.

Quando non si usa HTTPS, non usare le opzioni di configurazione della personalizzazione. Queste impostazioni mostrano il nome dell'organizzazione nel Catalogo applicazioni come identificazione.  


### <a name="use-role-separation"></a>Usare la separazione dei ruoli

> [!Important]  
> Il supporto per i ruoli del Catalogo applicazioni termina con la versione 1910. Per altre informazioni, vedere [Rimuovere il catalogo applicazioni](plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

Installare il punto per siti Web del Catalogo applicazioni e il punto per servizi Web del Catalogo applicazioni in server separati. Se il punto per siti Web è compromesso, viene separato dal punto per servizi Web. In questo modo si proteggono i client e l'infrastruttura. Questa configurazione è particolarmente importante se il punto per siti Web accetta connessioni client da Internet, rendendo così il server più vulnerabile agli attacchi.  

### <a name="close-browser-windows"></a>Chiudere le finestre del browser

> [!Important]  
> Il supporto per i ruoli del Catalogo applicazioni termina con la versione 1910. Per altre informazioni, vedere [Rimuovere il catalogo applicazioni](plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

Istruire gli utenti a chiudere la finestra del browser dopo aver usato il Catalogo applicazioni. Se gli utenti navigano in un sito Web esterno nella stessa finestra del browser usata per il Catalogo applicazioni, il browser continua a usare le impostazioni di sicurezza adatte per i siti attendibili nell'Intranet.  

### <a name="centrally-specify-user-device-affinity"></a>Specificare a livello centrale l'affinità utente-dispositivo

Specificare manualmente l'affinità utente-dispositivo invece di consentire agli utenti di identificare il dispositivo primario. Non abilitare la configurazione basata sull'utilizzo.

Non considerare autorevoli le informazioni raccolte dagli utenti o dal dispositivo. Se si distribuisce il software usando un'affinità utente-dispositivo non specificata da un utente amministratore attendibile, il software potrebbe essere installato in computer e per utenti che non sono autorizzati a riceverlo.  

### <a name="dont-run-deployments-from-distribution-points"></a>Non eseguire distribuzioni dai punti di distribuzione

Configurare sempre le distribuzioni per scaricare il contenuto dai punti di distribuzione, anziché eseguirlo dai punti di distribuzione. Quando si configurano le distribuzioni per scaricare il contenuto da un punto di distribuzione ed eseguirlo in locale, il client di Configuration Manager verifica l'hash del pacchetto dopo aver scaricato il contenuto. Il client scarta il pacchetto se l'hash non corrisponde all'hash nei criteri.

Se si configura la distribuzione per l'esecuzione direttamente da un punto di distribuzione, il client di Configuration Manager non verifica l'hash pacchetto, il che significa che il client di Configuration Manager può installare software che è stato manomesso.

Se è necessario eseguire le distribuzioni direttamente da punti di distribuzione, usare autorizzazioni NTFS per i pacchetti nei punti di distribuzione. Usare anche IPsec (Internet Protocol Security) per proteggere il canale tra il client e i punti di distribuzione e tra i punti di distribuzione e il server del sito.

### <a name="dont-let-users-interact-with-elevated-processes"></a><a name="bkmk_interact"></a> Non consentire agli utenti di interagire con processi con privilegi elevati
  
Se si abilitano le opzioni **Esegui con diritti amministrativi** o **Installa per sistema**, non consentire agli utenti di interagire con tali applicazioni. Quando si configura un'applicazione, è possibile impostare l'opzione **Consenti agli utenti di visualizzare e interagire con l'installazione del programma**. Questa impostazione consente agli utenti di rispondere a qualsiasi richiesta necessaria nell'interfaccia utente. Se anche l'applicazione è configurata con **Esegui con diritti amministrativi** o, a partire dalla versione1802, con **Installa per sistema**, un utente malintenzionato nel computer in cui è in esecuzione il programma potrebbe usare l'interfaccia utente per riassegnare i privilegi nel computer client.

Usare programmi che usano Windows Installer per l'installazione e privilegi elevati per utente per le distribuzioni software che richiedono credenziali amministrative. Il programma di installazione deve essere eseguito nel contesto di un utente che non ha credenziali amministrative. I privilegi elevati per utente di Windows Installer rappresentano il modo più sicuro per distribuire applicazioni con questo requisito.

### <a name="restrict-whether-users-can-install-software-interactively"></a>Limitare gli utenti che possono installare software in modo interattivo

Configurare l'impostazione client **Autorizzazioni di installazione** nel gruppo **Agente computer**. Questa impostazione limita i tipi di utenti che possono installare software in Software Center.

Ad esempio, creare un impostazione client personalizzata con **Autorizzazioni di installazione** impostato su **Solo amministratori**. Applicare questa impostazione client a un raccolta di server. Questa configurazione impedisce agli utenti senza autorizzazioni amministrative di installare software in tali server.  

### <a name="for-mobile-devices-deploy-only-applications-that-are-signed"></a>Per i dispositivi mobili, distribuire solo le applicazioni firmate.

Distribuire applicazioni per dispositivi mobili solo se il relativo codice è firmato da un'autorità di certificazione (CA) considerata attendibile dal dispositivo mobile.

Ad esempio:

- Un'applicazione di un fornitore, firmata da un'autorità di certificazione nota, come VeriSign.  

- Un'applicazione interna che viene firmata in modo indipendente da Configuration Manager usando l'autorità di certificazione interna.  

- Un'applicazione interna firmata con Configuration Manager quando si crea il tipo di applicazione e si usa un certificato di firma.

### <a name="secure-the-location-of-the-mobile-device-application-signing-certificate"></a>Proteggere il percorso del certificato di firma dell'applicazione per dispositivi mobili

Se si firmano applicazioni per dispositivi mobili usando la **Creazione guidata applicazione** in Configuration Manager, proteggere il percorso del file del certificato di firma e il canale di comunicazione. Per proteggersi dall'elevazione dei privilegi e dagli attacchi man-in-the-middle, archiviare il file del certificato di firma in una cartella protetta

e usare IPsec tra i computer seguenti:

- Computer che esegue la console di Configuration Manager
- Computer in cui è archiviato il file del certificato di firma
- Computer in cui sono archiviati i file di origine dell'applicazione

In alternativa, firmare l'applicazione indipendentemente da Configuration Manager e prima di eseguire la **Creazione guidata applicazione**.

### <a name="implement-access-controls"></a>Implementare i controlli di accesso

Per proteggere i computer di riferimento, implementare i controlli di accesso. Quando si configura il metodo di rilevamento in un tipo di distribuzione selezionando un computer di riferimento, assicurarsi che il computer non sia compromesso.

### <a name="restrict-and-monitor-administrative-users"></a>Limitare e monitorare gli utenti amministratori

Limitare e monitorare gli utenti amministratori a cui vengono concessi i ruoli di sicurezza basata sui ruoli per la gestione delle applicazioni:

- **Amministratore applicazione**
- **Autore applicazione**
- **Gestione distribuzione applicazioni**

Anche quando si configura l'amministrazione basata su ruoli, gli utenti amministratori che creano e distribuiscono le applicazioni potrebbero disporre di più autorizzazioni del previsto. Ad esempio, gli utenti amministratori che creano o modificano un'applicazione possono selezionare applicazioni dipendenti non incluse nel loro ambito di protezione.

### <a name="configure-app-v-apps-in-virtual-environments-with-the-same-trust-level"></a>Configurare app App-V in ambienti virtuali con lo stesso livello di attendibilità

Durante la configurazione di ambienti virtuali Microsoft Application Virtualization (App-V), selezionare le applicazioni con lo stesso livello di attendibilità nell'ambiente virtuale. Poiché le applicazioni in un ambiente virtuale App-V possono condividere risorse, come gli Appunti, configurare l'ambiente virtuale in modo che le applicazioni selezionate abbiano lo stesso livello di attendibilità.

Per altre informazioni, vedere [Create App-V virtual environments](../deploy-use/create-app-v-virtual-environments.md) (Creare ambienti virtuali App-V).

### <a name="make-sure-macos-apps-are-from-a-trustworthy-source"></a>Verificare che le app macOS provengano da un'origine attendibile

Se si distribuiscono applicazioni per dispositivi macOS, accertarsi che i file di origine provengano da una fonte attendibile. Lo strumento CMAppUtil non convalida la firma del pacchetto di origine. Verificare che il pacchetto provenga da un'origine considerata attendibile. Lo strumento CMAppUtil non consente di rilevare eventuali manomissioni dei file.

### <a name="secure-the-cmmac-file-for-macos-apps"></a>Proteggere il file con estensione cmmac per le app macOS

Se si distribuiscono applicazioni per computer macOS, proteggere il percorso del file con estensione **cmmac**. Lo strumento CMAppUtil genera questo file e quindi lo si importa in Configuration Manager. Questo file non viene firmato o convalidato.

Proteggere il canale di comunicazione quando si importa questo file in Configuration Manager. Per evitare che questo file venga manomesso, archiviarlo in una cartella protetta. e usare IPsec tra i computer seguenti:

- Computer che esegue la console di Configuration Manager  
- Computer in cui è archiviato il file **CMMAC**  

### <a name="use-https-for-web-applications"></a>Usare HTTPS per le applicazioni Web

Se si configura un tipo di distribuzione delle applicazioni Web, usare HTTPS per proteggere la connessione. Se si distribuisce un'applicazione Web usando un collegamento HTTP anziché un collegamento HTTPS, il dispositivo potrebbe essere reindirizzato a un server non autorizzato. I dati trasferiti tra il dispositivo e il server potrebbero essere manomessi.


## <a name="security-issues-for-application-management"></a>Problemi di protezione per la gestione delle applicazioni  

- Utenti con diritti limitati possono copiare file dalla cache del client sul computer client.  

     Gli utenti possono leggere la cache del client, ma non possono scrivere al suo interno. Con le autorizzazioni di lettura, un utente può copiare i file di installazione applicazione da un computer a un altro.  

- Gli utenti con diritti limitati possono modificare i file che registrano la cronologia della distribuzione software nel computer client.  

     Dato che le informazioni sulla cronologia applicazioni non sono protette, un utente può modificare i file che indicano se un'applicazione è installata.  

- I pacchetti App-V non sono firmati.  

     I pacchetti App-V in Configuration Manager non supportano la firma. Le firme digitali verificano che il contenuto provenga da una fonte attendibile e non sia stato alterato durante la trasmissione. Non è possibile ovviare a questo problema di sicurezza. Seguire la procedura consigliata per la sicurezza per scaricare il contenuto da una fonte attendibile e da un percorso sicuro.  

- Le applicazioni App-V pubblicate possono essere installate da tutti gli utenti sul computer.  

     Quando un'applicazione App-V viene pubblicata in un computer, tutti gli utenti che accedono a tale computer possono installare l'applicazione. Non è possibile limitare gli utenti che possono installare l'applicazione dopo la pubblicazione.  


## <a name="certificates-for-microsoft-silverlight-5-and-elevated-trust-mode-required-for-the-application-catalog"></a><a name="BKMK_CertificatesSilverlight5"></a> Certificati per Microsoft Silverlight 5 e modalità di attendibilità elevata richiesta per il Catalogo applicazioni  

> [!Important]  
> Il supporto per i ruoli del Catalogo applicazioni termina con la versione 1910. Per altre informazioni, vedere [Rimuovere il catalogo applicazioni](plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

I client di Configuration Manager versione 1710 e precedenti richiedono Microsoft Silverlight 5 che deve essere eseguito in modalità di attendibilità elevata perché gli utenti installino il software dal Catalogo applicazioni. Per impostazione predefinita, le applicazioni Silverlight vengono eseguite in modalità di attendibilità parziale per evitare l'accesso ai dati utente. Se non è già installato, Configuration Manager installa automaticamente Microsoft Silverlight 5 nei client. Per impostazione predefinita, Configuration Manager imposta su **Sì** l'impostazione client **Consentire alle applicazioni di Silverlight di essere eseguite in modalità attendibilità elevata**. Questa impostazione consente alle applicazioni Silverlight firmate e attendibili di richiedere la modalità attendibilità elevata.  

Quando si installa il ruolo del sistema del sito del punto per siti Web del Catalogo applicazioni, il client installa anche un certificato di firma Microsoft nell'archivio certificati del computer Autori attendibili in ogni computer client di Configuration Manager. Le applicazioni Silverlight firmate da questo certificato vengono eseguite nella modalità attendibilità elevata che i computer richiedono per installare software dal Catalogo applicazioni. Configuration Manager gestisce automaticamente questo certificato di firma. Per aumentare la continuità del servizio, non eliminare manualmente né spostare questo certificato di firma Microsoft.  

> [!WARNING]  
> Se abilitata, l'impostazione client **Consentire alle applicazioni di Silverlight di essere eseguite in modalità attendibilità elevata** consente l'esecuzione in modalità attendibilità elevata per tutte le applicazioni Silverlight firmate da certificati nell'archivio certificati Autori attendibili nell'archivio computer o nell'archivio utente. L'impostazione client non può abilitare la modalità di attendibilità elevata specificamente per il Catalogo applicazioni di Configuration Manager o per l'archivio certificati Autori attendibili nell'archivio computer. Se un malware aggiunge un certificato non autorizzato nell'archivio Autori attendibili, anche il malware che usa l'applicazione Silverlight può essere eseguito in modalità di attendibilità elevata.  

Se si configura l'impostazione client **Consentire l'esecuzione in modalità di attendibilità elevata delle applicazioni Silverlight** su **No**, i client non rimuovono il certificato di firma di Microsoft.  

Per altre informazioni sulle applicazioni attendibili in Silverlight, vedere [Trusted Applications (Applicazioni attendibili)](https://docs.microsoft.com/previous-versions/windows/silverlight/dotnet-windows-silverlight/ee721083\(v=vs.95\)).  


## <a name="privacy-information-for-application-management"></a>Informazioni sulla privacy per la gestione delle applicazioni  

La gestione delle applicazioni consente l'esecuzione di qualsiasi applicazione, programma o script in qualsiasi client della gerarchia. Configuration Manager non controlla i tipi di applicazioni, programmi o script eseguiti né il tipo di informazioni trasmesse. Durante il processo di distribuzione delle applicazioni, Configuration Manager può trasmettere informazioni che identificano gli account di accesso e del dispositivo tra i client e i server.  

Configuration Manager conserva le informazioni sullo stato relative al processo di distribuzione del software. Le informazioni sullo stato di distribuzione del software non vengono crittografate durante la trasmissione, a meno che il client non comunichi tramite HTTPS. Le informazioni sullo stato non vengono memorizzate in forma crittografata nel database.  

L'uso delle funzionalità di installazione delle applicazioni di Configuration Manager per installare in remoto, in modo interattivo o automatico il software nei client può essere soggetto alle condizioni di licenza software per tali software, distinte dalle Condizioni di licenza software per Configuration Manager. Rivedere sempre e accettare le Condizioni di licenza software prima di distribuire il software usando Configuration Manager.  

Configuration Manager raccoglie dati di utilizzo e di diagnostica sulle applicazioni, che vengono usati da Microsoft per migliorare le versioni future. Per altre informazioni, vedere [Diagnostica e dati di utilizzo](../../core/plan-design/diagnostics/diagnostics-and-usage-data.md).

La distribuzione delle applicazioni non avviene per impostazione predefinita e richiede diversi passaggi di configurazione.  

Le funzionalità seguenti consentono di distribuire il software in modo efficiente:

- L'**affinità utente-dispositivo** esegue il mapping di un utente ai dispositivi. Un amministratore di Configuration Manager distribuisce il software a un utente. Il client installa automaticamente il software in uno o più computer che l'utente usa più di frequente.  

- **Software Center** viene automaticamente installato in un dispositivo quando si installa il client di Configuration Manager. Gli utenti modificano le impostazioni e selezionano e installano il software da Software Center.  

- Il **Catalogo applicazioni** è un sito Web che consente agli utenti di richiedere software da installare.  

    > [!Important]  
    > Il supporto per i ruoli del Catalogo applicazioni termina con la versione 1910. Per altre informazioni, vedere [Rimuovere il catalogo applicazioni](plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

### <a name="user-device-affinity-privacy-information"></a><a name="bkmk_privacy-uda"></a>Informazioni sulla privacy relative all'affinità utente-dispositivo

- È possibile che Configuration Manager trasmetta informazioni tra i client e i sistemi del sito del punto di gestione, che identificano il computer e l'account di accesso, nonché dati di utilizzo aggregati relativi agli account di accesso.  

- Le informazioni trasmesse tra il client e il server non vengono crittografate, a meno che il punto di gestione sia configurato in modo da richiedere che i client comunichino tramite HTTPS.  

- Le informazioni sul computer e sull'uso dell'account di accesso, usate per eseguire il mapping di un utente a un dispositivo, vengono archiviate nei computer client, inviate ai punti di gestione e quindi archiviate nel database di Configuration Manager. Le informazioni precedenti vengono eliminate dal database per impostazione predefinita dopo 90 giorni. È possibile configurare il comportamento di eliminazione impostando l'attività di manutenzione del sito **Elimina dati di affinità utente dispositivo obsoleti** .  

- Configuration Manager conserva informazioni sullo stato relative all'affinità utente dispositivo. Le informazioni sullo stato non vengono crittografate durante la trasmissione, a meno che i client non siano configurati in modo da comunicare con i punti di gestione tramite HTTPS. Le informazioni sullo stato non vengono memorizzate in forma crittografata nel database.  

- Le informazioni sul computer e sull'utilizzo dell'account di accesso, usate per stabilire l'affinità utente-dispositivo, sono sempre abilitate. Gli utenti e gli utenti amministrativi possono fornire informazioni sull'affinità utente-dispositivo.  

### <a name="software-center-privacy-information"></a><a name="bkmk_privacy-userex"></a>Informazioni sulla privacy relative a Software Center

- Software Center consente all'amministratore di Configuration Manager di pubblicare tutte le applicazioni, i programmi o gli script che gli utenti dovranno eseguire. Configuration Manager non ha alcun controllo sui tipi di programmi o script che vengono pubblicati nel catalogo, né sul tipo di informazioni trasmesse.  

- È possibile che Configuration Manager trasmetta informazioni tra i client e il punto di gestione. Queste informazioni potrebbero consentire l'identificazione di computer e account di accesso. Le informazioni trasmesse tra il client e i server non vengono crittografate, a meno che il punto di gestione non venga configurato per richiedere la connessione dei client tramite HTTPS.  

- Le informazioni relative alla richiesta di approvazione applicazione vengono memorizzate nel database di Configuration Manager. Le richieste annullate o respinte vengono eliminate per impostazione predefinita dopo 30 giorni, insieme alle relative voci di cronologia delle richieste. È possibile configurare il comportamento di eliminazione impostando l'attività di manutenzione del sito **Elimina dati richiesta applicazione obsoleti** . Le richieste di approvazione di applicazioni con stato approvato e in attesa non vengono mai eliminate.  

- Software Center viene automaticamente installato quando si installa il client di Configuration Manager in un dispositivo.  

### <a name="application-catalog-privacy-information"></a>Informazioni sulla privacy relative al Catalogo applicazioni

> [!Important]  
> Il supporto per i ruoli del Catalogo applicazioni termina con la versione 1910. Per altre informazioni, vedere [Rimuovere il catalogo applicazioni](plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

- Il Catalogo applicazioni non viene installato per impostazione predefinita. Questa installazione richiede diversi passaggi di configurazione.  

- Il Catalogo applicazioni consente all'amministratore di Configuration Manager di pubblicare tutte le applicazioni, i programmi o gli script che gli utenti dovranno eseguire. Configuration Manager non ha alcun controllo sui tipi di programmi o script che vengono pubblicati nel catalogo, né sul tipo di informazioni trasmesse.  

- Configuration Manager potrebbe trasmettere informazioni tra i client e i ruoli del sistema del sito del Catalogo applicazioni. Queste informazioni potrebbero consentire l'identificazione di computer e account di accesso. Le informazioni trasmesse tra il client e i server non vengono crittografate, a meno che tali ruoli del sistema non siano configurati in modo da richiedere che i client si connettano tramite HTTPS.  
