---
title: Novità della versione 1806
titleSuffix: Configuration Manager
description: Informazioni dettagliate sulle modifiche e sulle nuove funzionalità introdotte nella versione 1806 di Configuration Manager (Current Branch).
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0249dbd3-1e85-4d05-a9e5-420fbe44d850
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 295940337f191b791d8c7a86de4003466213df6b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702339"
---
# <a name="whats-new-in-version-1806-of-configuration-manager-current-branch"></a>Novità della versione 1806 di Configuration Manager (Current Branch)

*Si applica a: Configuration Manager (Current Branch)*

L'aggiornamento 1806 per Configuration Manager (Current Branch) è disponibile come aggiornamento nella console. Applicare questo aggiornamento ai siti con la versione 1706, 1710 o 1802. <!-- baseline only statement: When installing a new site, it's also available as a baseline version.-->

Esaminare sempre l'elenco di controllo più recente per installare questo aggiornamento. Per altre informazioni, vedere [Elenco di controllo per l'installazione dell'aggiornamento 1806](../../servers/manage/checklist-for-installing-update-1806.md). Dopo aver aggiornato un sito, vedere anche [Elenco di controllo post-aggiornamento](../../servers/manage/checklist-for-installing-update-1806.md#post-update-checklist).

<!--
> [!Important]  
> This article currently lists all significant features in this version. However, not all sections yet link to updated content with further information on the new features. Keep checking this page regularly for updates. Changes are noted with the ***[Updated]*** tag. This note will be removed when the content is finalized.  
-->

Le sezioni seguenti offrono informazioni dettagliate sulle modifiche e sulle nuove funzionalità della versione 1806 di Configuration Manager (Current Branch).  



## <a name="deprecated-features-and-operating-systems"></a>Funzionalità e sistemi operativi deprecati

Informazioni sulle modifiche apportate al supporto prima dell'implementazione in [Elementi rimossi e deprecati](deprecated/removed-and-deprecated.md).

A partire dal 14 agosto 2018, la funzionalità di gestione ibrida dei dispositivi mobili è deprecata. Per altre informazioni, vedere [Che ne è stato della gestione di dispositivi mobili ibrida?](../../../mdm/understand/what-happened-to-hybrid.md).<!--Intune feature 2683117-->  

<!--
Version 1806 drops support for the following products:
-->



## <a name="site-infrastructure"></a>Infrastruttura del sito

### <a name="cmpivot"></a>CMPivot
<!--1358456-->
Configuration Manager ha sempre fornito un archivio centralizzato di grandi dimensioni per i dati dei dispositivi, usato dai clienti per i report. Il sito in genere raccoglie questi dati su base settimanale. CMPivot è una nuova utilità inclusa nella console che ora consente l'accesso allo stato in tempo reale dei dispositivi nell'ambiente in uso. Esegue immediatamente una query su tutti i dispositivi connessi nella raccolta di destinazione e restituisce i risultati. È quindi possibile filtrare e raggruppare questi dati nello strumento. La disponibilità di dati in tempo reale dai client online consente di rispondere alle domande aziendali, risolvere i problemi e rispondere agli eventi imprevisti di sicurezza in modo più veloce. 

Per altre informazioni, vedere [CMPivot](../../servers/manage/cmpivot.md).  


### <a name="site-server-high-availability"></a>Disponibilità elevata del server del sito
<!--1128774-->
La disponibilità elevata per un ruolo del server del sito primario autonomo è una soluzione basata su Configuration Manager per installare un server del sito aggiuntivo in modalità passiva. Il server del sito in modalità passiva è in aggiunta al server del sito esistente in modalità attiva. Un server del sito in modalità passiva è disponibile per l'uso immediato, quando è necessario. 

Per altre informazioni, vedere gli articoli seguenti: 
- [Disponibilità elevata del server del sito](../../servers/deploy/configure/site-server-high-availability.md) 
- [Diagramma di flusso - Configurare un server del sito in modalità passiva](../../servers/deploy/configure/passive-site-server-flowchart.md)
- [Diagramma di flusso - Alzare di livello il server del sito (con pianificazione)](../../servers/deploy/configure/promote-site-server-flowchart.md)
- [Diagramma di flusso - Alzare di livello il server del sito (senza pianificazione)](../../servers/deploy/configure/promote-site-server-unplanned-flowchart.md)


### <a name="improvements-to-management-insights"></a>Miglioramenti alle informazioni dettagliate sulla gestione
Questa versione include i miglioramenti seguenti alle informazioni dettagliate sulla gestione:  

- Alcune informazioni dettagliate sulla gestione offrono ora la possibilità di eseguire un'azione. Questa azione consiste nel passaggio al nodo associato nella console o alla visualizzazione di una vista filtrata basata su query.<!--1357930-->  

- È disponibile un nuovo gruppo per la manutenzione proattiva con sei nuove regole, che consentono di evidenziare potenziali problemi di configurazione da evitare tramite la manutenzione regolare.<!--1352184-->  

Per altre informazioni, vedere [Informazioni dettagliate sulla gestione](../../servers/manage/management-insights.md).


### <a name="configuration-manager-tools"></a>Strumenti di Configuration Manager
<!--1357145-->
Gli strumenti per server e client di Configuration Manager sono ora inclusi nel server. Sono disponibili nella cartella `CD.Latest\SMSSETUP\Tools` nel server del sito. Non è necessaria un'ulteriore installazione. 

Per altre informazioni, vedere [Strumenti di Configuration Manager](../../support/tools.md).


### <a name="exclude-active-directory-containers-from-discovery"></a>Escludere i contenitori di Active Directory dall'individuazione
<!--1358143-->
Per ridurre il numero di oggetti individuati, escludere specifici contenitori dal metodo di individuazione sistema Active Directory. 

Per altre informazioni, vedere [Configurare l'individuazione sistema Active Directory](../../servers/deploy/configure/configure-discovery-methods.md#bkmk_config-adsd).



## <a name="content-management"></a>Gestione dei contenuti

### <a name="configure-a-remote-content-library-for-the-site-server"></a>Configurare una raccolta contenuto remota per il server del sito
<!--1357525-->
Per configurare la disponibilità elevata del server del sito o per liberare spazio sul disco rigido nei server di amministrazione centrale o del sito primario, spostare la libreria del contenuto in un'altra posizione di archiviazione. Spostare la raccolta contenuto in un'altra unità sul server del sito, su un server distinto o su dischi a tolleranza d'errore in una rete di archiviazione (SAN). 

Per altre informazioni, vedere gli articoli seguenti: 
- [Raccolta contenuto](../hierarchy/the-content-library.md)
- [Diagramma di flusso - Gestire la raccolta contenuto](../hierarchy/manage-content-library-flowchart.md)


### <a name="cloud-distribution-point-support-for-azure-resource-manager"></a>Supporto del punto di distribuzione cloud per Azure Resource Manager
<!--1322209-->
Quando si crea un punto di distribuzione cloud, la procedura guidata consente ora di creare una **distribuzione di Azure Resource Manager**. Azure Resource Manager è una piattaforma moderna per la gestione di tutte le risorse di una soluzione come una singola entità denominata gruppo di risorse. Quando si distribuisce un punto di distribuzione cloud con Azure Resource Manager, il sito usa Azure Active Directory per autenticare e creare le risorse cloud necessarie. Questa distribuzione modernizzata non richiede il certificato di gestione classico di Azure. 

Anche la documentazione della funzionalità per il punto di distribuzione cloud è stata revisionata e migliorata. Per altre informazioni, vedere gli articoli seguenti:
- [Usare un punto di distribuzione cloud](../hierarchy/use-a-cloud-based-distribution-point.md)   
- [Installare un punto di distribuzione cloud](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md)  


### <a name="pull-distribution-points-support-cloud-distribution-points-as-source"></a>I punti di distribuzione pull supportano punti di distribuzione cloud come origine  
<!--1321554-->
Molti clienti usano punti di distribuzione pull in uffici remoti o succursali per scaricare contenuto da un punto di distribuzione di origine attraverso la rete WAN. Se gli uffici remoti hanno una connessione Internet più efficiente oppure se si vuole ridurre il carico sui collegamenti WAN, è ora possibile usare come origine un punto di distribuzione cloud in Microsoft Azure. Quando si aggiunge un'origine nella scheda **Punto di distribuzione pull** delle proprietà dei punti di distribuzione, qualsiasi punto di distribuzione cloud nel sito viene elencato come punto di distribuzione disponibile. Il comportamento di entrambi i ruoli del sistema del sito rimane per altri versi invariato. 

Per altre informazioni, vedere [Usare punti di distribuzione pull](../hierarchy/use-a-pull-distribution-point.md).


### <a name="enable-distribution-points-to-use-network-congestion-control"></a>Abilitare punti di distribuzione per l'uso del controllo di congestione della rete
<!--1358112-->
La funzionalità LEDBAT (Low Extra Delay Background Transport) di Windows Server consente di gestire i trasferimenti di rete in background. Per i punti di distribuzione in esecuzione in versioni supportate di Windows Server, abilitare un'opzione che consente di regolare il traffico di rete. I client usano la larghezza di banda di rete solo quando è disponibile. 

Per altre informazioni, vedere [LEDBAT Windows](../hierarchy/fundamental-concepts-for-content-management.md#windows-ledbat).


### <a name="partial-download-support-in-client-peer-cache-to-reduce-wan-utilization"></a>Riduzione dell'utilizzo della rete WAN tramite supporto parziale del download nella peer cache del client
<!--1357346-->
Le origini delle peer cache dei client sono ora in grado di dividere il contenuto in parti, grazie alle quali è possibile ridurre al minimo il trasferimento in rete, riducendo l'utilizzo della rete WAN. Il punto di gestione consente una traccia più dettagliata delle parti del contenuto e tenta di eliminare più download dello stesso contenuto per ogni gruppo di limiti. 

Per altre informazioni, vedere [Supporto per download parziale](../hierarchy/client-peer-cache.md#bkmk_parts). 


### <a name="boundary-group-options-for-peer-downloads"></a>Opzioni del gruppo di limiti per download peer
<!--1356193-->
Sono ora disponibili impostazioni aggiuntive per i gruppi di limiti per offrire maggiore controllo sulla distribuzione di contenuti nell'ambiente. Questa versione aggiunge le opzioni seguenti:  

- **Consenti i download peer in questo gruppo di limiti**: Il punto di gestione fornisce ai client un elenco di posizioni del contenuto che include le origini peer. Questa impostazione influisce anche sull'applicazione di ID di gruppo per l'ottimizzazione recapito.  

- **Durante i download peer, usa solo i peer entro la stessa subnet**: Il punto di gestione include nell'elenco delle posizioni del contenuto solo le origini peer incluse nella stessa subnet del client.  

Per altre informazioni, vedere [Opzioni del gruppo di limiti per download peer](../../servers/deploy/configure/boundary-groups.md#bkmk_bgoptions).


### <a name="improvement-to-peer-cache-source-location-status"></a>Miglioramento dello stato della posizione di origine di peer cache
<!--SCCMDocs issue 850-->
Configuration Manager è più efficiente nel determinare se è stato eseguito il roaming di un'origine peer cache in un'altra posizione. Questo comportamento garantisce che il punto di gestione la offra come origine di contenuto ai client nella nuova posizione e non in quella precedente. Se si usa la funzionalità di peer cache con origini di peer cache in roaming, dopo aver aggiornato il sito alla versione 1806, aggiornare anche tutte le origini di peer cache alla versione più recente del client. Il punto di gestione non include tali origini di peer cache nell'elenco di posizioni del contenuto finché non vengono aggiornate almeno alla versione 1806.

Per altre informazioni, vedere i [requisiti per la peer cache](../hierarchy/client-peer-cache.md#requirements).



<!-- ## Migration  -->



## <a name="client-management"></a>Gestione dei client

### <a name="improvement-to-client-push-security"></a>Miglioramento alla sicurezza dei push client
<!--1358204-->
Quando si usa il metodo di installazione push client per il client di Configuration Manager, il sito richiede ora l'autenticazione reciproca Kerberos. Questo miglioramento consente di proteggere la comunicazione tra il server e il client. 

Per altre informazioni , vedere [Come installare i client con l'installazione push client](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).


### <a name="enhanced-http-site-system"></a><a name="bkmk_ehttp"></a>Sistema del sito HTTP migliorato
<!--1356889,1358228-->
L'uso delle comunicazioni HTTPS è consigliato per tutti i percorsi di comunicazione di Configuration Manager, ma può essere difficile per alcuni clienti a causa del sovraccarico di gestione dei certificati PKI.

Questa versione include miglioramenti per le modalità di comunicazione dei client con i sistemi del sito. Nella scheda **Comunicazione computer client** delle proprietà del sito selezionare l'opzione per **HTTPS o HTTP** e quindi abilitare la nuova opzione **Usa i certificati generati da Configuration Manager per sistemi del sito HTTP**. Si tratta di una [funzionalità di versione non definitiva](../../servers/manage/pre-release-features.md).

Per altre informazioni, vedere [HTTP migliorato](../hierarchy/enhanced-http.md).


### <a name="azure-ad-device-identity"></a>Identità del dispositivo di Azure AD 
<!--1358460-->
Un dispositivo [aggiunto ad Azure AD](/azure/active-directory/devices/concept-azure-ad-join) o un [dispositivo di Azure AD ibrido](/azure/active-directory/devices/concept-azure-ad-join-hybrid) senza un utente di Azure AD connesso può comunicare in modo sicuro con il relativo sito assegnato. L'identità del dispositivo basata sul cloud è ora sufficiente per l'autenticazione con CMG e il punto di gestione.  

Per altre informazioni, vedere [HTTP migliorato](../hierarchy/enhanced-http.md).


### <a name="cmtrace-installed-with-client"></a>Installazione di CMTrace con il client
<!--1357971-->
Lo strumento per la visualizzazione di log CMTrace viene ora installato automaticamente insieme al client di Configuration Manager. Viene aggiunto alla directory di installazione del client, che per impostazione predefinita è `%WinDir%\ccm\cmtrace.exe`. 

Per altre informazioni, vedere [CMTrace](../../support/cmtrace.md).


### <a name="cloud-management-dashboard"></a>Dashboard di gestione del cloud
<!--1358461-->
Il nuovo dashboard Gestione cloud fornisce una visualizzazione centralizzata per l'utilizzo di Cloud Management Gateway. Dopo l'onboarding del sito con Azure AD, nel dashboard vengono visualizzati anche dati sugli utenti e i dispositivi del cloud.   

Questa funzionalità include anche l'**analizzatore della connessione CMG** per verifiche in tempo reale a supporto della risoluzione dei problemi. L'utilità inclusa nella console controlla lo stato corrente del servizio e il canale di comunicazione dal punto di connessione CMG a tutti i punti di gestione che consentono il traffico CMG. 

Per altre informazioni, vedere le sezioni seguenti nell'articolo relativo al [monitoraggio di CMG](../../clients/manage/cmg/monitor-clients-cloud-management-gateway.md):  
- [Dashboard di gestione del cloud](../../clients/manage/cmg/monitor-clients-cloud-management-gateway.md#cloud-management-dashboard)  
- [Analizzatore della connessione](../../clients/manage/cmg/monitor-clients-cloud-management-gateway.md#connection-analyzer)  


### <a name="improvements-to-cloud-management-gateway"></a>Miglioramenti al gateway di gestione cloud

La versione 1806 include i miglioramenti seguenti a Cloud Management Gateway (CMG):

#### <a name="simplified-client-bootstrap-command-line"></a>Riga di comando semplificata per bootstrap client
<!--1358215-->
Quando si installa il client di Configuration Manager su Internet usando un CMG, ora è richiesto un numero inferiore di proprietà della riga di comando. Questo miglioramento riduce la dimensione della riga di comando usata in Microsoft Intune durante la preparazione per la co-gestione. 

Per altre informazioni, vedere [How to prepare internet-based devices for co-management](../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client) (Come preparare i dispositivi basati su Internet per la co-gestione).

#### <a name="download-content-from-a-cmg"></a>Scaricare il contenuto da un CMG
<!--1358651-->
In precedenza, era necessario distribuire un punto di distribuzione cloud e un gateway CMG come ruoli separati. Ora in questa versione un CMG può anche trasferire il contenuto ai client. Questa funzionalità riduce i certificati necessari e i costi delle macchine virtuali di Azure. 

Per altre informazioni, vedere [Modify a CMG](../../clients/manage/cmg/setup-cloud-management-gateway.md#modify-a-cmg) (Modificare un gateway di gestione cloud).

#### <a name="trusted-root-certificate-isnt-required-with-azure-ad"></a>Non è necessario un certificato radice trusted con Azure AD
<!--503899-->
Quando si crea un gateway CMG, non è più necessario specificare un [certificato radice trusted](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_cmgroot) nella pagina Impostazioni. Questo certificato non è obbligatorio se si usa Azure Active Directory (Azure AD) per l'autenticazione client, ma veniva richiesto nella procedura guidata. Se si usano certificati di autenticazione client PKI, è comunque necessario aggiungere un certificato radice trusted al CMG.



## <a name="co-management"></a>Co-gestione

### <a name="sync-mdm-policy-from-microsoft-intune-for-a-co-managed-device"></a>Sincronizzare i criteri MDM da Microsoft Intune per un dispositivo con co-gestione
<!--1357377-->
Quando si passa a un carico di lavoro con co-gestione, i dispositivi con co-gestione sincronizzano automaticamente i criteri MDM da Microsoft Intune. La sincronizzazione si verifica anche quando si avvia l'azione **Scarica criteri computer** dalle notifiche client nella console di Configuration Manager. 

Per altre informazioni, vedere [Come passare i carichi di lavoro di Configuration Manager a Intune](../../../comanage/how-to-switch-workloads.md).


### <a name="transition-new-workloads-to-intune-using-co-management"></a>Transizione di nuovi carichi di lavoro a Intune usando la co-gestione
È ora possibile eseguire la transizione dei carichi di lavoro seguenti da Configuration Manager a Intune dopo aver abilitato la co-gestione:  

- **Configurazione del dispositivo**<!--1357903-->: questo carico di lavoro consente di usare Intune per distribuire criteri MDM, pur continuando a usare Configuration Manager per la distribuzione delle applicazioni.  

- **Office 365**<!--1357841-->: i dispositivi non installano le distribuzioni di Office 365 da Configuration Manager.  

- **App per dispositivi mobili**<!--1357892-->: qualsiasi app disponibile distribuita da Intune sarà disponibile nel portale aziendale. Le app distribuite da Configuration Manager sono disponibili in Software Center. Si tratta di una [funzionalità di versione non definitiva](../../servers/manage/pre-release-features.md).  

Per eseguire la transizione dei carichi di lavoro, passare alla pagina delle proprietà di co-gestione e spostare il dispositivo di scorrimento dei carichi di lavoro da Configuration Manager a **Pilota** o a **Tutte**. 

Per altre informazioni, vedere [Co-gestione per dispositivi Windows 10](../../../comanage/overview.md).


### <a name="support-for-multiple-hierarchies-to-one-intune-tenant"></a>Supporto per più gerarchie in un tenant di Intune
<!--1357944-->
Alcuni clienti hanno diverse gerarchie di Configuration Manager che intendono consolidare in futuro in un singolo tenant per Azure Active Directory e Microsoft Intune. La co-gestione ora supporta la connessione di più ambienti di Configuration Manager allo stesso tenant di Intune.

Per altre informazioni, vedere i [prerequisiti per la co-gestione](../../../comanage/overview.md#prerequisites).
 


## <a name="compliance-settings"></a>Impostazioni di conformità

### <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge"></a>Configurare le impostazioni di Windows Defender SmartScreen per Microsoft Edge
<!--1353701-->
I criteri delle impostazioni di conformità del browser Microsoft Edge aggiungono le tre impostazioni seguenti per Windows Defender SmartScreen: 
- Consenti SmartScreen
- Gli utenti possono eseguire l'override del prompt di SmartScreen per i siti
- Gli utenti possono eseguire l'override del prompt di SmartScreen per i file

Per altre informazioni, vedere [Configurare le impostazioni di Microsoft Edge](../../../compliance/deploy-use/browser-profiles.md).


### <a name="scap-extensions"></a>Estensioni SCAP
<!--1357552-->
Convertire il contenuto del protocollo SCAP (Security Content Automation Protocol) in baseline di impostazioni di conformità e generare rapporti SCAP tramite un'estensione della console. Questa funzione include anche un nuovo dashboard per la visualizzazione della conformità dei client e della conformità alla regola XCCDF. 





## <a name="application-management"></a>Gestione delle applicazioni

### <a name="phased-deployment-of-applications"></a>Distribuzione in più fasi di applicazioni
<!--1358147-->
Creare una distribuzione in più fasi per un'applicazione. Le distribuzioni in più fasi consentono di orchestrare un'implementazione coordinata e in sequenza del software basata su criteri e gruppi personalizzabili. È possibile, ad esempio, distribuire l'applicazione in una raccolta pilota e quindi continuare automaticamente l'implementazione in base ai criteri per l'esito positivo. 

Per altre informazioni, vedere gli articoli seguenti:  

- [Creare una distribuzione in più fasi](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  

- [Gestire e monitorare le distribuzioni in più fasi](../../../osd/deploy-use/manage-monitor-phased-deployments.md?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  


### <a name="provision-windows-app-packages-for-all-users-on-a-device"></a>Effettuare il provisioning dei pacchetti di app Windows per tutti gli utenti in un dispositivo
<!--1358310-->
Eseguire il provisioning di un'applicazione con un pacchetto di app Windows per tutti gli utenti nel dispositivo. Un esempio comune di questo scenario è il provisioning di un'app da Microsoft Store per le aziende e la formazione, ad esempio Minecraft: Education Edition, in tutti i dispositivi usati dagli studenti di una scuola. In precedenza, Configuration Manager supportava solo l'installazione di queste applicazioni per ogni utente. Dopo aver eseguito l'accesso a un nuovo dispositivo, uno studente dovrebbe attendere prima di poter accedere a un'app. Ora quando viene eseguito il provisioning dell'app nel dispositivo per tutti gli utenti, tutti possono essere produttivi più rapidamente. 

Per altre informazioni, vedere [Creare applicazioni Windows](../../../apps/get-started/creating-windows-applications.md#bkmk_provision).


### <a name="office-customization-tool-integration-with-the-office-365-installer"></a>Integrazione dello Strumento di personalizzazione di Office con il Programma di installazione di Office 365
<!--1358149-->
Lo Strumento di personalizzazione di Office è ora integrato con il Programma di installazione di Office 365 nella console di Configuration Manager. Quando si crea una distribuzione per Office 365, configurare dinamicamente le impostazioni di gestibilità di Office più recenti. Lo Strumento di personalizzazione di Office viene aggiornato quando vengono rilasciate nuove build di Office 365. Questa integrazione consente di usufruire delle nuove impostazioni di gestibilità di Office 365 non appena sono disponibili. 

Per altre informazioni, vedere [Distribuire app di Office 365](../../../sum/deploy-use/manage-office-365-proplus-updates.md#deploy-office-365-apps).


### <a name="support-for-new-windows-app-package-formats"></a>Supporto per nuovi formati di pacchetti di app Windows
<!--1357427-->
Configuration Manager supporta ora la distribuzione dei nuovi formati di pacchetto dell'app (con estensione msix) e bundle dell'app (con estensione msixbundle) di Windows 10. 

Per altre informazioni, vedere [Creare applicazioni Windows](../../../apps/get-started/creating-windows-applications.md#bkmk_msix).


### <a name="uninstall-application-on-approval-revocation"></a>Disinstallare l'applicazione in caso di revoca dell'approvazione
<!--1357891-->
Quando si revoca l'approvazione per un'applicazione, il comportamento è stato modificato. Ora, quando si nega la richiesta per l'applicazione, il client disinstalla l'applicazione dal dispositivo dell'utente. Questo comportamento richiede l'abilitazione della [funzionalità facoltativa](https://docs.microsoft.com/sccm/core/servers/manage/install-in-console-updates#bkmk_options) **Approva le richieste dell'applicazione per gli utenti per ogni dispositivo**. 

Per altre informazioni, vedere l'argomento relativo alla [distribuzione delle applicazioni](../../../apps/deploy-use/deploy-applications.md#bkmk_approval).


### <a name="package-conversion-manager"></a>Package Conversion Manager 
<!--1357861-->
Package Conversion Manager è ora uno strumento integrato che consente di convertire i pacchetti legacy in applicazioni di Configuration Manager Current Branch. È quindi possibile usare le funzionalità di applicazioni come dipendenze, regole dei requisiti e affinità utente-dispositivo.

Per altre informazioni, vedere [Package Conversion Manager](../../../apps/pcm/package-conversion-manager.md).



## <a name="os-deployment"></a>Distribuzione del sistema operativo

### <a name="improvements-to-phased-deployments"></a>Miglioramenti alle distribuzioni in più fasi

Questa versione include i miglioramenti seguenti alle distribuzioni in più fasi:  

#### <a name="create-a-phased-deployment-with-manually-configured-phases"></a>Creare una distribuzione in più fasi con fasi configurate manualmente
<!--1358148-->
Per una sequenza di attività, configurare ora manualmente le fasi quando si crea una distribuzione in più fasi. Aggiungere fino a 10 fasi aggiuntive dalla scheda **Fasi** della procedura guidata Crea una distribuzione in più fasi. È comunque possibile creare automaticamente una distribuzione in due fasi predefinita. 

Per altre informazioni, vedere [Creare una distribuzione in più fasi con fasi configurate manualmente](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md#bkmk_manual).

#### <a name="phased-deployment-status"></a>Stato della distribuzione in più fasi
<!--1358577-->
Per le distribuzioni in più fasi è ora disponibile un'esperienza di monitoraggio nativa. Dal nodo **Distribuzioni** nell'area di lavoro **Monitoraggio** selezionare una distribuzione in più fasi e quindi fare clic su **Stato di distribuzione in più fasi** nella barra multifunzione. 

Per altre informazioni, vedere questo articolo: [Gestire e monitorare le distribuzioni in più fasi](../../../osd/deploy-use/manage-monitor-phased-deployments.md).  

#### <a name="gradual-rollout-during-phased-deployments"></a>Implementazione graduale durante le distribuzioni in più fasi
<!--1358578-->
Durante una distribuzione in più fasi, l'implementazione di ogni fase può ora essere graduale. Questo comportamento consente di ridurre il rischio di problemi di distribuzione e diminuisce il carico sulla rete causato dalla distribuzione di contenuti ai client. Il sito può rendere gradualmente disponibile il software a seconda della configurazione per ogni fase. Tutti i client in una fase hanno una scadenza definita in base al momento in cui il software viene reso disponibile. L'intervallo di tempo tra l'ora di disponibilità e la scadenza è uguale per tutti i client in una fase. 

Per altre informazioni, vedere [Impostazioni delle fasi](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md#bkmk_settings).  


### <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Miglioramenti alla sequenza di attività di aggiornamento sul posto di Windows 10
<!--1358500-->
Il modello di sequenza di attività predefinita per l'aggiornamento sul posto di Windows 10 include ora un altro nuovo gruppo con azioni consigliate da aggiungere in caso di esito negativo del processo di aggiornamento. Queste azioni facilitano la risoluzione dei problemi. Uno di questi strumenti è [SetupDiag](https://docs.microsoft.com/windows/deployment/upgrade/setupdiag) di Windows. È uno strumento di diagnostica autonomo per ottenere i dettagli sui motivi per cui un aggiornamento a Windows 10 non è riuscito. 

Per altre informazioni, vedere [Creare una sequenza di attività per aggiornare un sistema operativo](../../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md#recommended-task-sequence-steps-on-failure).


### <a name="improvements-to-pxe-enabled-distribution-points"></a>Miglioramenti ai punti di distribuzione che supportano PXE
<!--1357580-->
Nella scheda **PXE** delle proprietà del punto di distribuzione selezionare **Abilita un risponditore PXE senza i Servizi di distribuzione Windows**. Questa nuova opzione abilita un risponditore PXE nel punto di distribuzione, che non richiede Servizi di distribuzione Windows (WDS). Poiché i Servizi di distribuzione Windows non sono necessari, il punto di distribuzione che supporta PXE può essere un sistema operativo client o server, incluso Windows Server Core. Questo nuovo servizio risponditore PXE supporta IPv6 e migliora la flessibilità dei punti di distribuzione che supportano PXE negli uffici remoti. 

Per altre informazioni, vedere [Abilitare un risponditore PXE senza i Servizi di distribuzione Windows](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).


### <a name="network-access-account-not-required-for-some-scenarios"></a>Account di accesso alla rete non necessario per alcuni scenari
<!--1358278,1358279-->
La funzione [Sistema del sito HTTP migliorato](#bkmk_ehttp) rimuove anche alcune dipendenze nell'account di accesso alla rete. Quando si abilita la nuova opzione del sito che consente di **usare i certificati generati da Configuration Manager per i sistemi di sito HTTP**, gli scenari seguenti non richiedono un account di accesso alla rete per scaricare il contenuto da un punto di distribuzione:  

- Sequenze di attività in esecuzione da supporti di avvio o PXE
- Sequenze di attività in esecuzione da Software Center  

Queste sequenze di attività possono essere per la distribuzione del sistema operativo o personalizzate. Sono supportate anche per i computer del gruppo di lavoro.

Per altre informazioni, vedere [Sequenze di attività e account di accesso alla rete](../../../osd/plan-design/planning-considerations-for-automating-tasks.md#BKMK_TSNetworkAccessAccount).


### <a name="other-improvements-to-os-deployment"></a>Altri miglioramenti alla distribuzione del sistema operativo

#### <a name="mask-sensitive-data-stored-in-task-sequence-variables"></a>Mascherare i dati sensibili archiviati nelle variabili della sequenza di attività
 <!--1358330-->
 nel passaggio **Imposta variabile della sequenza di attività** selezionare la nuova opzione **Non visualizzare questo valore**, 

 Per altre informazioni, vedere [Imposta variabile della sequenza di attività](../../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable). 

#### <a name="mask-program-name-during-run-command-step-of-a-task-sequence"></a>Mascherare il nome programma durante il passaggio Esegui riga di comando di una sequenza di attività
 <!--1358493-->
 Per impedire la visualizzazione o la registrazione di dati potenzialmente sensibili, configurare la variabile della sequenza di attività **OSDDoNotLogCommand**.  

 Per altre informazioni, vedere [Variabili della sequenza di attività](../../../osd/understand/task-sequence-variables.md#OSDDoNotLogCommand). 

#### <a name="task-sequence-variable-for-dism-parameters-when-installing-drivers"></a>Variabile della sequenza di attività per i parametri DISM durante l'installazione di driver
 <!--516679/2840016-->
 Per specificare parametri della riga di comando aggiuntivi per DISM, usare la nuova variabile della sequenza di attività **OSDInstallDriversAdditionalOptions**. 

 Per altre informazioni, vedere [Variabili della sequenza di attività](../../../osd/understand/task-sequence-variables.md#OSDInstallDriversAdditionalOptions). 

#### <a name="option-to-use-full-disk-encryption"></a>Opzione per usare la crittografia del disco completo
 <!--SCCMDocs-pr issue 2671-->
 I passaggi **Attiva BitLocker** e **BitLocker pre-provisioning** includono ora entrambi un'opzione **Usa la crittografia del disco completo**. Per impostazione predefinita, questi passaggi eseguono la crittografia dello spazio usato sull'unità. Questo comportamento predefinito è consigliato perché è più veloce ed efficiente. 

 Per altre informazioni, vedere [Attivare BitLocker](../../../osd/understand/task-sequence-steps.md#BKMK_EnableBitLocker) ed [Eseguire il pre-provisioning di BitLocker](../../../osd/understand/task-sequence-steps.md#BKMK_PreProvisionBitLocker). 

#### <a name="client-provisioning-mode-isnt-enabled-with-windows-10-upgrade-compatibility-scan"></a>La modalità di provisioning client non è abilitata con l'analisi di compatibilità dell'aggiornamento di Windows 10
 <!--SCCMDocs-pr issue 2812-->
 Ora, quando si abilita l'opzione **Esegui analisi di compatibilità di Installazione di Windows senza avviare l'aggiornamento**, il passaggio della sequenza di attività **Aggiorna sistema operativo** non imposta il client di Configuration Manager in modalità di provisioning.

 Per altre informazioni, vedere [Aggiorna sistema operativo](../../../osd/understand/task-sequence-steps.md#BKMK_UpgradeOS).

#### <a name="revised-documentation-for-task-sequence-variables"></a>Documentazione rivista per le variabili della sequenza di attività
Sono ora disponibili due nuovi articoli con informazioni sulle variabili della sequenza di attività:  

- [How to use task sequence variables](../../../osd/understand/using-task-sequence-variables.md) (Come usare le variabili della sequenza di attività) è un nuovo articolo che descrive i diversi tipi di variabili, i metodi per impostare le variabili e come accedervi.  

- [Task sequence variables](../../../osd/understand/task-sequence-variables.md) (Variabili della sequenza di attività) è un articolo con informazioni di riferimento per tutte le variabili della sequenza di attività. Questo articolo combina gli articoli precedenti in cui le variabili predefinite erano separate dalle variabili di azione. 



## <a name="software-center"></a>Software Center

> [!Important]  
> Per sfruttare i vantaggi delle nuove funzionalità di Configuration Manager, aggiornare prima di tutto i clienti alla versione più recente. Anche se le nuove funzionalità vengono visualizzate nella console di Configuration Manager quando si esegue l'aggiornamento del sito e della console, lo scenario completo risulta funzionante solo dopo l'aggiornamento alla versione più recente del client.


### <a name="software-center-infrastructure-improvements"></a>Miglioramenti all'infrastruttura di Software Center
<!--1358309-->
I ruoli del catalogo applicazioni non sono più necessari per visualizzare le applicazioni disponibili per gli utenti in Software Center. Questa modifica consente di ridurre l'infrastruttura server necessaria per distribuire le applicazioni agli utenti. Software Center ora si affida al punto di gestione per ottenere queste informazioni e questo consente una migliore scalabilità degli ambienti di grandi dimensioni, che vengono assegnati a [gruppi di limiti](../../servers/deploy/configure/boundary-groups.md#management-points).

Per altre informazioni, vedere [Configurare Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)  

> [!Note]  
> Il ruolo Punto per siti Web e il ruolo Punto per servizi Web del Catalogo applicazioni non sono più *necessari* nella versione 1806, ma sono ancora *supportati*. 
> 
> L'**esperienza utente di Silverlight** per il ruolo Punto per siti Web del Catalogo applicazioni non è più supportato. Per altre informazioni, vedere [Funzionalità rimosse e deprecate](deprecated/removed-and-deprecated-cmfeatures.md).  


### <a name="specify-the-visibility-of-the-application-catalog-website-link-in-software-center"></a>Specifica la visibilità del collegamento al sito Web del Catalogo applicazioni in Software Center
<!--1358214-->
Usare le impostazioni client per controllare se il collegamento **Aprire il sito Web del Catalogo applicazioni** viene visualizzato nel nodo **Stato installazione** di Software Center.  

Per altre informazioni, vedere [Impostazioni client di Software Center](../../clients/deploy/about-client-settings.md#software-center).

> [!Note]  
> L'**esperienza utente di Silverlight** per il ruolo Punto per siti Web del Catalogo applicazioni non è più supportato. Per altre informazioni, vedere [Funzionalità rimosse e deprecate](deprecated/removed-and-deprecated-cmfeatures.md).  


### <a name="custom-tab-for-webpage-in-software-center"></a>Scheda personalizzata per pagine Web in Software Center
<!--1358132-->
Usare le impostazioni client per creare una scheda personalizzata per aprire una pagina Web in Software Center. Questa funzionalità consente di visualizzare il contenuto per gli utenti finali in modo coerente e affidabile. L'elenco seguente include alcuni esempi:  

- Contatta IT: informazioni su come contattare il reparto IT dell'organizzazione  

- Centro assistenza IT: azioni self-service per l'IT, ad esempio la ricerca nella Knowledge Base o l'apertura di un ticket di supporto.  

- Documentazione per l'utente finale: articoli per gli utenti dell'organizzazione su diversi argomenti IT, ad esempio l'uso delle applicazioni o l'aggiornamento a Windows 10.  

Per altre informazioni, vedere [Impostazioni client di Software Center](../../clients/deploy/about-client-settings.md#software-center) e [Manuale dell'utente di Software Center](../../understand/software-center.md).


### <a name="maintenance-windows-in-software-center"></a>Finestre di manutenzione in Software Center
<!--1358131-->
Software Center ora visualizza la finestra di manutenzione pianificata successiva. Nella scheda Stato installazione cambiare la visualizzazione da Tutto a Upcoming (Prossima). Visualizza l'intervallo di tempo e l'elenco delle distribuzioni pianificate. L'elenco è vuoto se non ci sono finestre di manutenzione future. 

Per altre informazioni, vedere [Come usare le finestre di manutenzione](../../clients/manage/collections/use-maintenance-windows.md) e [Manuale dell'utente di Software Center](../../understand/software-center.md).



## <a name="software-updates"></a>Aggiornamenti software

### <a name="third-party-software-updates"></a>Aggiornamenti software di terze parti
<!--1357605, 1352101, 1358714-->
Gli aggiornamenti software di terze parti consentono di sottoscrivere i cataloghi partner nella console di Configuration Manager e di pubblicare gli aggiornamenti in WSUS. È quindi possibile distribuire questi aggiornamenti usando il processo di gestione degli aggiornamenti software esistente. 

Per altre informazioni, vedere [Abilitare gli aggiornamenti di terze parti](../../../sum/deploy-use/third-party-software-updates.md).


### <a name="deploy-software-updates-without-content"></a>Distribuire aggiornamenti software senza contenuto
<!--1357933-->
Distribuire gli aggiornamenti software ai dispositivi senza prima scaricare e distribuire il contenuto nei punti di distribuzione. Questa funzionalità è utile quando si lavora con il contenuto di aggiornamenti di dimensioni molto grandi o si vuole che i client ricevano sempre il contenuto dal servizio cloud Microsoft Update. I client in questo scenario possono anche scaricare il contenuto da peer in cui è già presente il contenuto necessario. Il client Gestione configurazione continua a gestire il download del contenuto, quindi è in grado di usare la funzionalità peer cache di Configuration Manager o altre tecnologie, ad esempio Ottimizzazione recapito. Questa funzionalità supporta qualsiasi tipo di aggiornamento supportato dalla gestione degli aggiornamenti software di Configuration Manager, tra cui gli aggiornamenti di Windows e Office. 

Per altre informazioni, vedere l'opzione **Nessun pacchetto di distribuzione** quando si esegue la [distribuzione manuale degli aggiornamenti software](../../../sum/deploy-use/manually-deploy-software-updates.md) o la [distribuzione automatica degli aggiornamenti software](../../../sum/deploy-use/automatically-deploy-software-updates.md).


### <a name="filter-automatic-deployment-rules-by-software-update-architecture"></a>Filtrare le regole di distribuzione automatica in base all'architettura di aggiornamento software
 <!--1322266-->
È ora possibile filtrare le regole di distribuzione automatica in modo da escludere architetture come Itanium e ARM64. Nella pagina **Aggiornamenti software** della Creazione guidata delle regole di distribuzione automatica è ora disponibile il filtro di proprietà **Architettura**. 

Per altre informazioni, vedere [Distribuire automaticamente gli aggiornamenti software](../../../sum/deploy-use/automatically-deploy-software-updates.md).


### <a name="improved-wsus-maintenance"></a>Manutenzione WSUS migliorata 
<!--1357898-->
La pulizia guidata WSUS rifiuta ora gli aggiornamenti scaduti in base alle regole di sostituzione definite nelle proprietà del componente del punto di aggiornamento software. 

Per altre informazioni, vedere [Manutenzione degli aggiornamenti software](../../../sum/deploy-use/software-updates-maintenance.md).



## <a name="reporting"></a>Reporting

### <a name="new-software-updates-compliance-report"></a>Nuovo report di conformità degli aggiornamenti software
<!--1357775-->
La visualizzazione dei report per la conformità degli aggiornamenti software include in genere dati dei client che non hanno contattato il sito di recente. Un nuovo report **Conformità 9 - Dati complessivi su integrità e conformità** consente di filtrare i risultati di conformità per un gruppo di aggiornamenti software specifico in base ai client "integri". Questo report mostra lo stato di conformità più realistico dei client attivi nell'ambiente in uso. 

Per altre informazioni, vedere [Report degli aggiornamenti software](../../../sum/deploy-use/monitor-software-updates.md#BKMK_SUReports).



## <a name="inventory"></a>Argomento

### <a name="improvement-to-hardware-inventory-for-large-integer-values"></a><a name="bkmk_bigint"></a> Miglioramento all'inventario hardware per valori interi di grandi dimensioni
<!--1357880-->
L'inventario hardware aveva in precedenza un limite per numeri interi maggiori di 4.294.967.296 (2^32). Questo limite può essere raggiunto per attributi come le dimensioni delle unità disco rigido in byte. Il punto di gestione non elaborava valori interi oltre questo limite e quindi nessun valore veniva archiviato nel database. In questa versione, il limite è stato aumentato a 18.446.744.073.709.551.616 (2^64). 

Per altre informazioni, vedere [Utilizzo di valori interi di grandi dimensioni](../../clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md#bkmk_bigint).


### <a name="hardware-inventory-default-unit-revision"></a>Revisione dell'unità predefinita di inventario hardware
<!--514442-->
In [Configuration Manager versione 1710](whats-new-in-version-1710.md#site-infrastructure) l'unità predefinita usata in molte visualizzazioni Rapporti è passata da megabyte (MB) a gigabyte (GB). A causa dei [miglioramenti all'inventario hardware per i valori interi di grandi dimensioni](#bkmk_bigint) e in base alle opinioni dei clienti, l'unità predefinita ora è di nuovo MB.



<!-- ## Mobile device management -->



<!-- ## Protect devices-->




## <a name="configuration-manager-console"></a>Console di Configuration Manager

### <a name="product-lifecycle-dashboard"></a>Dashboard del ciclo di vita del prodotto
<!--1319632-->
Il dashboard del ciclo di vita del prodotto mostra lo stato del criterio Ciclo di vita del prodotto Microsoft per i prodotti Microsoft installati nei dispositivi gestiti con Configuration Manager. Fornisce anche informazioni sui prodotti Microsoft in uso nell'ambiente, sullo stato del supporto e sulle date di fine del supporto. Usare il dashboard per conoscere la disponibilità del supporto per ogni prodotto. Queste informazioni consentono anche di pianificare l'aggiornamento dei prodotti Microsoft in uso prima del raggiungimento della fine del supporto.   

Per altre informazioni, vedere [Dashboard del ciclo di vita del prodotto](../../clients/manage/asset-intelligence/product-lifecycle-dashboard.md).


### <a name="copy-asset-details-from-monitoring-views"></a>Copiare i dettagli degli asset dalle viste di monitoraggio
<!--1357856-->
Le seguenti aree dell'area di lavoro **Monitoraggio** supportano ora la copia del testo:  

- Nel nodo **Distribuzioni** selezionare una distribuzione e fare clic su **Visualizza stato**. Nel riquadro **Dettagli asset** della visualizzazione Stato distribuzione selezionare uno o più dispositivi.  

- Espandere il nodo **Stato distribuzione** e selezionare **Stato contenuto**. Selezionare un componente software, quindi scegliere **Visualizza stato**. Selezionare uno o più punti di distribuzione nel riquadro **Dettagli asset** della visualizzazione Stato contenuto. 

Fare clic con il pulsante destro del mouse sull'asset e selezionare **Copia**. Questa azione copia le risorse selezionate come elenco delimitato da virgole che include i dettagli completi. I tasti di scelta rapida **CTRL** + **C** funzionano anche in queste visualizzazioni. 

Per altre informazioni, vedere [Miglioramenti della console nella versione 1806](../../servers/manage/admin-console.md#copy-details-in-monitoring-views).


### <a name="improvements-to-the-surface-dashboard"></a>Miglioramenti al dashboard di Surface
<!--1358654-->
Questa versione include i miglioramenti seguenti al dashboard di Surface:  

- Il dashboard di Surface ora visualizza un elenco di dispositivi pertinenti quando vengono selezionate sezioni specifiche del grafico.  

   - Facendo clic sul riquadro **Percentuale di dispositivi Surface** viene aperto un elenco di dispositivi Surface.  

   - Facendo clic su una barra nel riquadro **Prime cinque versioni di firmware** viene aperto un elenco di dispositivi Surface con quella versione di firmware specifica.  

- Quando si visualizzano questi elenchi di dispositivi dal dashboard di Surface, fare clic con il pulsante destro del mouse su un dispositivo per eseguire azioni comuni.  

Per altre informazioni, vedere [Dashboard dei dispositivi Surface](../../clients/manage/surface-device-dashboard.md).


### <a name="view-the-currently-signed-on-user-for-a-device"></a>Visualizzare l'utente attualmente connesso per un dispositivo
<!--1358202-->
Per impostazione predefinita il nodo **Dispositivi** dell'area di lavoro **Asset e conformità** visualizza ora una colonna per **Utente attualmente connesso**. Viene visualizzata anche per qualsiasi elenco di dispositivi specifici della raccolta. Questo valore è aggiornato quanto lo [stato del client](../../clients/manage/monitor-clients.md#bkmk_indStatus). Quando l'utente esegue l'accesso, il client cancella questo valore. Se nessun utente è connesso, il valore è vuoto. 

Per altre informazioni, vedere [Miglioramenti della console nella versione 1806](../../servers/manage/admin-console.md#view-users-for-a-device).


### <a name="submit-feedback-from-the-configuration-manager-console"></a>Inviare commenti e suggerimenti dalla console di Configuration Manager  
<!--1357542-->

Commenti e suggerimenti Ora è possibile comunicare direttamente al team di Configuration Manager le proprie esperienze. Inviare commenti e suggerimenti dalla console di Configuration Manager è molto semplice. Siamo interessati a ogni tipo di feedback: apprezzamenti, problemi e suggerimenti. Nella console di Configuration Manager fare clic sul pulsante Smile nell'angolo superiore destro sopra la barra multifunzione. Questi commenti e suggerimenti vengono inviati direttamente al team del prodotto Microsoft per Configuration Manager. Anche se l'uso dell'Hub di Feedback di Windows 10 è ancora supportato, è consigliabile usare il meccanismo per l'invio di feedback disponibile nella console.  

Per altre informazioni, vedere [Miglioramenti della console nella versione 1806](../../servers/manage/admin-console.md#send-feedback) e [Commenti e suggerimenti sul prodotto](../../understand/find-help.md#BKMK_1806Feedback).



## <a name="other-updates"></a>Altri aggiornamenti

A parte le nuove funzionalità, questa versione include anche ulteriori modifiche, ad esempio correzioni di bug. Per altre informazioni, vedere [Riepilogo delle modifiche in Configuration Manager Current Branch, versione 1806](https://support.microsoft.com/help/4459701).

Per altre informazioni sulle modifiche apportate ai cmdlet di Windows PowerShell per Configuration Manager, vedere le [note sulla versione di PowerShell 1806](https://docs.microsoft.com/powershell/sccm/1806_release_notes?view=sccm-ps).

L'aggiornamento cumulativo seguente (4462978) è disponibile nella console a partire dal 24 ottobre 2018: [Aggiornamento cumulativo per Configuration Manager Current Branch, versione 1806](https://support.microsoft.com/help/4462978).


### <a name="hotfixes"></a>Hotfix

Gli hotfix aggiuntivi seguenti sono disponibili per la risoluzione di problemi specifici:

| ID | Titolo | Date | Nella console |
|---------|---------|---------|---------|
| [4346645](https://support.microsoft.com/help/4346645) | Aggiornamento per Configuration Manager versione 1806, primo gruppo | 31 agosto 2018 | Sì |
| [4465865](https://support.microsoft.com/help/4465865) | Gli aggiornamenti software non vengono scaricati nell'ambiente Configuration Manager se WSUS è disconnesso<br><br>Questo aggiornamento è incluso anche nell'aggiornamento cumulativo (4462978) | 1º ottobre 2018 | Sì |
| [4471892](https://support.microsoft.com/help/4471892) | Il risponditore PXE non funziona nelle subnet in Configuration Manager 1806 | 23 novembre 2018 | No |
| [4487960](https://support.microsoft.com/help/4487960) | Il certificato del connettore Microsoft Intune non viene rinnovato in Configuration Manager | 18 gennaio 2019 | Sì |


## <a name="next-steps"></a>Passaggi successivi

Quando si è pronti per installare la versione, vedere [Installazione degli aggiornamenti per Configuration Manager](../../servers/manage/updates.md) ed [Elenco di controllo per l'installazione dell'aggiornamento 1806](../../servers/manage/checklist-for-installing-update-1806.md).

> [!TIP]  
> Per installare un nuovo sito, usare una versione base di Configuration Manager.  
>
> Sono disponibili altre informazioni su:    
> - [Installing new sites](../../servers/deploy/install/installing-sites.md) (Installare nuovi siti)  
> - [Baseline and update versions](../../servers/manage/updates.md#bkmk_Baselines) (Versioni di base e di aggiornamento)

Per problemi noti e importanti, vedere [Note sulla versione](../../servers/deploy/install/release-notes.md).

Dopo aver aggiornato un sito, vedere anche [Elenco di controllo post-aggiornamento](../../servers/manage/checklist-for-installing-update-1806.md#post-update-checklist).
