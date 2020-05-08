---
title: Nuova versione 1802
titleSuffix: Configuration Manager
description: Informazioni dettagliate sulle modifiche e sulle nuove funzionalità introdotte nella versione 1802 di Configuration Manager.
ms.date: 10/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5bd637b1-d7a1-411b-877a-c7aae9741173
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: e7bc30c4350d96654a0f6a6ae548d63c2928e791
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82904663"
---
# <a name="whats-new-in-version-1802-of-configuration-manager"></a>Novità della versione 1802 di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

L'aggiornamento 1802 per Configuration Manager current branch è disponibile come aggiornamento nella console. Applicare questo aggiornamento ai siti con la versione 1702, 1706 o 1710. <!-- baseline only statement: -->Quando si installa un nuovo sito, è disponibile anche come versione di base.

A parte le nuove funzionalità, questa versione include anche ulteriori modifiche, ad esempio correzioni di bug. Per altre informazioni, vedere [Riepilogo delle modifiche in Configuration Manager Current Branch, versione 1802](https://support.microsoft.com/help/4101375).

Sono ora disponibili anche i seguenti aggiornamenti aggiuntivi per questa versione:
- [Aggiornamento cumulativo per Configuration Manager Current Branch, versione 1802](https://support.microsoft.com/help/4163547)

> [!TIP]  
> Per installare un nuovo sito, è necessario usare una versione base di Configuration Manager.  
>
> Sono disponibili altre informazioni su:    
> - [Installing new sites](../../servers/deploy/install/installing-sites.md) (Installare nuovi siti)  
> - [Installing updates at sites](../../servers/manage/updates.md) (Installare aggiornamenti nei siti)  
> - [Baseline and update versions](../../servers/manage/updates.md#bkmk_Baselines) (Versioni di base e di aggiornamento)

Le sezioni seguenti offrono informazioni dettagliate sulle modifiche e sulle nuove funzionalità della versione 1802 di Configuration Manager.  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](deprecated/removed-and-deprecated.md).

Version 1802 drops support for the following products:
-->


## <a name="site-infrastructure"></a>Infrastruttura del sito

### <a name="reassign-distribution-point"></a>Riassegnare un punto di distribuzione
<!-- 1306937 -->
Molti clienti hanno infrastrutture di Configuration Manager di grandi dimensioni e stanno diminuendo i siti primari o secondari per semplificare il proprio ambiente. Per distribuire il contenuto ai client gestiti, questi clienti devono comunque mantenere i punti di distribuzione nelle succursali. Questi punti di distribuzione spesso includono più terabyte di contenuto. La distribuzione di questo contenuto ai server remoti è dispendiosa in termini di tempo e larghezza di banda di rete. Questa funzionalità consente di riassegnare un punto di distribuzione a un altro sito primario senza ridistribuire il contenuto. Questa azione aggiorna l'assegnazione del sistema del sito mantenendo tutto il contenuto nel server. Per altre informazioni, vedere [Reassign a distribution point](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_reassign) (Riassegnare un punto di distribuzione).

### <a name="configure-windows-delivery-optimization-to-use-configuration-manager-boundary-groups"></a>Configurare Ottimizzazione recapito di Windows per usare i gruppi di limiti di Configuration Manager
<!-- 1324696 -->
I gruppi di limiti di Configuration Manager consentono di definire e regolamentare la distribuzione del contenuto nella rete aziendale e negli uffici remoti. [Ottimizzazione recapito di Windows](/windows/deployment/update/waas-delivery-optimization) è una tecnologia peer-to-peer basata sul cloud per la condivisione di contenuti tra dispositivi Windows 10. A partire da questa versione è possibile configurare Ottimizzazione recapito in modo che usi i gruppi di limiti quando si condividono contenuti tra peer. Una nuova impostazione client applica l'identificatore del gruppo di limiti come identificatore di gruppo di Ottimizzazione recapito sul client. Quando il client comunica con il servizio cloud Ottimizzazione recapito, usa questo identificatore per individuare i peer con il contenuto desiderato. Per altre informazioni su BranchCache, vedere [Fundamental concepts for content management](../hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization) (Concetti di base per la gestione dei contenuti).

### <a name="support-for-windows-10-arm64-devices"></a>Supporto per dispositivi ARM64 Windows 10
<!-- 1353704 -->
A partire da questa versione il client Gestione configurazione è supportato nei dispositivi ARM64 Windows 10. Le funzionalità di gestione client esistenti dovrebbero funzionare con questi nuovi dispositivi, ad esempio l'inventario hardware e software, gli aggiornamenti del software e la gestione delle applicazioni. La distribuzione del sistema operativo non è attualmente supportata. 

### <a name="improved-support-for-cng-certificates"></a>Supporto migliorato per i certificati CNG
<!-- 1357314 -->
Configuration Manager (Current Branch) versione 1710 supporta i [certificati CNG (Cryptography: Next Generation)](../network/cng-certificates-overview.md). La versione 1710 limita il supporto ai certificati client in diversi scenari. 

A partire da questa versione, è possibile usare i certificati CNG per i ruoli del server abilitati per HTTPS seguenti:
- Punto di gestione
- Punto di distribuzione
- Punto di aggiornamento software
- Punto di migrazione stato  


### <a name="boundary-group-fallback-for-management-points"></a>Fallback del gruppo di limiti per i punti di gestione
<!-- 1324594 -->
È possibile configurare relazioni di fallback per i punti di gestione tra [gruppi di limiti](../../servers/deploy/configure/boundary-groups.md). Questo comportamento consente un maggiore controllo per i punti di gestione usati dai client. Per altre informazioni, vedere [Configurare gruppi di limiti](../../servers/deploy/configure/boundary-groups.md#management-points).


### <a name="cloud-distribution-point-site-affinity"></a>Affinità del sito del punto di distribuzione cloud
<!--503719-->
Questa funzionalità è utile per i clienti con una gerarchia multisito dislocata in più aree geografiche che usano punti di distribuzione cloud. Quando un client basato su Internet cerca il contenuto, l'elenco dei punti di distribuzione cloud ricevuto dal client in precedenza non era ordinato in alcun modo. Questo comportamento può determinare la ricezione di contenuto proveniente da punti di distribuzione cloud geograficamente distanti dai client basati su Internet. Il download di contenuto da un server distante è in genere più lento rispetto a quello da un server più vicino.
 
Con l'affinità del sito del punto di distribuzione cloud, un client basato su Internet riceve un elenco ordinato. L'elenco dà la priorità ai punti di distribuzione cloud del sito assegnato al client. Questo comportamento consente all'amministratore di mantenere le finalità di progettazione per i download del contenuto dalle risorse del sito.
 

## <a name="management-insights"></a>Informazioni dettagliate sulla gestione
<!-- 1353967 -->
La funzionalità Informazioni dettagliate sulla gestione in Configuration Manager offre indicazioni utili sullo stato corrente dell'ambiente. Le informazioni si basano sull'analisi dei dati presenti nel database del sito. Le informazioni dettagliate aiutano a capire meglio l'ambiente e a intervenire di conseguenza. Per i dettagli, vedere [Informazioni dettagliate sulla gestione](../../servers/manage/management-insights.md)

In Configuration Manager 1802 sono disponibili le informazioni dettagliate seguenti:
- Applicazioni:
    - Applicazioni senza distribuzioni
- Servizi cloud: <!--1356412-->
    - Valutare la preparazione alla co-gestione 
    - Abilitare i dispositivi per l'aggiunta ad Azure Active Directory ibrido
    - Modernizzare l'infrastruttura di identità e accesso
    -  Aggiornare i client a Windows 10, versione 1709 o successiva 
- Raccolte:
    - Raccolte vuote
- Gestione semplificata:  <!--1355148-->
    - Versioni client obsolete  
- Software Center: 
    - Indirizzare gli utenti a Software Center anziché al Catalogo applicazioni  
    - Usare la nuova versione di Software Center 
- Windows 10: <!--1357421-->
    - Configurare la telemetria di Windows e la chiave ID commerciale 
    - Connettere Configuration Manager a Preparazione aggiornamenti 
   
<!-- ## Migration  -->



## <a name="client-management"></a>Gestione dei client

### <a name="cloud-management-gateway-support-for-azure-resource-manager"></a>Supporto di Cloud Management Gateway per Azure Resource Manager
<!-- 1324735 -->
Quando si crea un'istanza di [Cloud Management Gateway](../../clients/manage/cmg/plan-cloud-management-gateway.md), ora la procedura guidata consente di creare una **distribuzione Azure Resource Manager**. [Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) è una piattaforma moderna per la gestione di tutte le risorse di una soluzione come una singola entità detta [gruppo di risorse](/azure/azure-resource-manager/resource-group-overview#resource-groups). Quando si distribuisce Cloud Management Gateway con Azure Resource Manager, il sito usa Azure Active Directory (Azure AD) per autenticare e creare le risorse cloud necessarie. Questa distribuzione modernizzata non richiede il certificato di gestione classico di Azure. Per altre informazioni, vedere [Progettazione della topologia CMG](../../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager).

> [!IMPORTANT]
> Questa funzionalità non supporta i provider di servizi cloud di Azure. La distribuzione del gateway di gestione cloud con Azure Resource Manager continua infatti a usare il servizio cloud classico, non supportato dal provider di servizi cloud. Per altre informazioni, vedere [Available Azure services in Azure CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services) (Servizi di Azure disponibili in Azure CSP).  

### <a name="improvements-to-cloud-management-gateway"></a>Miglioramenti al gateway di gestione cloud  

- A partire da questa versione, il **gateway di gestione cloud** non è più una funzionalità non definitiva.  

- La documentazione della funzionalità è stata rivista e migliorata. Per altre informazioni, vedere gli articoli seguenti:
    - [Pianificare il gateway di gestione cloud](../../clients/manage/cmg/plan-cloud-management-gateway.md)
    - [Numeri di ridimensionamento e scalabilità del gateway di gestione cloud](../configs/size-and-scale-numbers.md#bkmk_cmg)
    - [Sicurezza e privacy per il gateway di gestione del cloud](../../clients/manage/cmg/security-and-privacy-for-cloud-management-gateway.md)
    - [Domande frequenti sul gateway di gestione cloud](../../clients/manage/cmg/cloud-management-gateway-faq.md)
    - [Certificati per il gateway di gestione del cloud](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md)
    - [Configurare il gateway di gestione cloud](../../clients/manage/cmg/setup-cloud-management-gateway.md)  


### <a name="configure-hardware-inventory-to-collect-strings-larger-than-255-characters"></a>Configurare l'inventario hardware per raccogliere le stringhe maggiori di 255 caratteri
<!-- 1357389 -->
Per le proprietà dell'inventario hardware è possibile configurare la lunghezza delle stringhe su un valore maggiore di 255 caratteri. Questa modifica si applica solo alle nuove classi aggiunte e alle proprietà dell'inventario hardware diverse dalle chiavi. Per informazioni dettagliate, vedere l'articolo [Estendere l'inventario hardware](../../clients/manage/inventory/extend-hardware-inventory.md#bkmk_GreaterThan255). 

 ### <a name="deprecation-announcement-for-linux-and-unix-client-support"></a>Annuncio di supporto deprecato per i client Linux e Unix
 <!--510139-->
Microsoft intende deprecare il supporto per i client Linux e UNIX in Configuration Manager entro circa un anno, in modo da non includerli nella versione 1902 all'inizio del 2019. La versione 1810 di Configuration Manager, in programma per la fine del 2018, sarà l'ultima versione a includere i client Linux e UNIX che saranno supportati per l'intero ciclo di vita di Configuration Manager 1810. Dopo Configuration Manager 1810, i clienti dovranno prendere in considerazione la gestione di Microsoft Azure per gestire i server Linux. Le soluzioni di Azure includono un ampio supporto per Linux che nella maggior parte dei casi supera le funzionalità di Configuration Manager, inclusa la gestione end-to-end delle patch per Linux.

### <a name="surface-device-dashboard"></a>Dashboard dei dispositivi Surface
<!--1355788-->
Il dashboard dei dispositivi Surface visualizza informazioni sui dispositivi Surface rilevati nell'ambiente. Nella console passare a **Monitoraggio** > **Surface Devices** (Dispositivi Surface). È possibile visualizzare:
- Percentuale di dispositivi Surface
- Percentuale di modelli Surface
- Prime cinque versioni di firmware

Per informazioni dettagliate, vedere l'articolo [Dashboard dei dispositivi Surface](../../clients/manage/surface-device-dashboard.md).

### <a name="change-in-the-configuration-manager-client-install"></a>Modifica dell'installazione del client di Configuration Manager
<!--1356195-->
A partire da questa versione, Silverlight non viene più installato automaticamente nei dispositivi client. Per altre informazioni, vedere [Prerequisiti per la distribuzione dei client nei computer Windows](../../clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md#bkmk_ExternalDependencies)

## <a name="co-management"></a>Co-gestione

### <a name="transition-endpoint-protection-workload-to-intune-using-co-management"></a>Eseguire la transizione del carico di lavoro di Endpoint Protection a Intune tramite la co-gestione
<!-- 1357365 -->
 Dopo aver abilitato la co-gestione, è possibile eseguire la transizione del carico di lavoro di Endpoint Protection a Intune. Per eseguire questa transizione, passare alla pagina delle proprietà di co-gestione e spostare la barra del dispositivo di scorrimento da Configuration Manager a **Pilota** o **Tutto**. Per informazioni dettagliate sui carichi di lavoro, vedere [Co-management workloads](../../../comanage/workloads.md) (Carichi di lavoro di co-gestione). Per altre informazioni sulla co-gestione, vedere [Co-gestione per dispositivi Windows 10](../../../comanage/overview.md).
 
### <a name="co-management-dashboard-in-configuration-manager"></a>Dashboard di co-gestione in Configuration Manager
<!--1356648-->
A partire da questa versione, è possibile visualizzare un dashboard con informazioni sulla co-gestione. Il dashboard consente di esaminare i computer co-gestiti presenti nell'ambiente. I grafici consentono di identificare i dispositivi che potrebbero richiedere attenzione. Per informazioni dettagliate, vedere l'articolo [Dashboard di co-gestione](../../../comanage/how-to-monitor.md#co-management-dashboard). 


## <a name="compliance-settings"></a>Impostazioni di conformità

### <a name="microsoft-edge-browser-policies"></a>Criteri del browser Microsoft Edge
<!-- 1357310 -->
I clienti che usano il Web browser [Microsoft Edge](https://www.microsoft.com/itpro/microsoft-edge) in client Windows 10 possono creare un criterio delle impostazioni di conformità di Configuration Manager per configurare diverse impostazioni di Microsoft Edge. Per altre informazioni, vedere [Creare il profilo del browser Microsoft Edge](../../../compliance/deploy-use/browser-profiles.md). 



## <a name="application-management"></a>Gestione delle applicazioni

### <a name="allow-user-interaction-when-installing-an-application"></a>Consentire l'interazione utente durante l'installazione di un'applicazione
<!-- 1356976 -->
È possibile consentire a un utente finale di interagire con l'installazione di un'applicazione durante l'esecuzione della sequenza di attività. Ad esempio, è possibile eseguire un processo di installazione che chiede all'utente finale diverse opzioni. Nei programmi di installazione di alcune applicazioni non è possibile disattivare i prompt utente o il processo di installazione può richiedere valori di configurazione specifici noti solo all'utente. Questa funzionalità consente di gestire questi scenari di installazione. Per altre informazioni, vedere [Specificare le opzioni dell'esperienza utente per il tipo di distribuzione](../../../apps/deploy-use/create-applications.md#bkmk_dt-ux).

### <a name="do-not-automatically-upgrade-superseded-applications"></a>Non vengono aggiornate automaticamente le applicazioni sostituite
<!-- 1351266 -->
È possibile configurare la distribuzione di un'applicazione in modo che non aggiorni automaticamente le versioni sostituite. Ora quando si crea la distribuzione, nella pagina **Impostazioni di distribuzione** della **Distribuzione guidata del software**, per lo scopo di installazione **Disponibile** è possibile abilitare o disabilitare l'opzione **Aggiorna automaticamente tutte le versioni sostituite di questa applicazione**. Per altre informazioni, vedere [Specificare le impostazioni di distribuzione](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-settings).

### <a name="approve-application-requests-for-users-per-device"></a>Approvazione delle richieste di applicazioni degli utenti per dispositivo
<!-- 1357015 -->
A partire da questa versione, quando un utente invia la richiesta per un'applicazione che richiede l'approvazione, il nome del dispositivo specifico fa parte della richiesta. Se l'amministratore approva la richiesta, l'utente può installare l'applicazione solo su quel dispositivo. Per installare l'applicazione in un altro dispositivo dovrà inviare un'altra richiesta. Per altre informazioni, vedere [Specificare le impostazioni di distribuzione](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-settings).

 > [!Note]  
 > Si tratta di una funzionalità facoltativa. Per altre informazioni, vedere [Enable optional features from updates](../../servers/manage/install-in-console-updates.md#bkmk_options) (Abilitare le funzioni facoltative dagli aggiornamenti).  


### <a name="run-scripts-improvements"></a>Miglioramenti alla funzionalità Esegui script 
<!-- 1236459 -->
 A partire da questa versione, **Esegui script** non è più una funzionalità non definitiva. L'output dello script ora viene restituito con la formattazione JSON. Per altre informazioni, vedere [Creare ed eseguire script di PowerShell dalla console di Configuration Manager](../../../apps/deploy-use/create-deploy-scripts.md).


## <a name="operating-system-deployment"></a>Distribuzione del sistema operativo

### <a name="windows-10-in-place-upgrade-task-sequence-via-cloud-management-gateway"></a>Sequenza di attività di aggiornamento sul posto di Windows 10 tramite Cloud Management Gateway
<!-- 1357149 -->
Ora la [sequenza di attività di aggiornamento sul posto](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md) di Windows 10 supporta la distribuzione nei client basati su Internet tramite [Cloud Management Gateway](../../clients/manage/cmg/plan-cloud-management-gateway.md). Ciò consente agli utenti remoti di eseguire più facilmente l'aggiornamento a Windows 10 senza doversi connettere alla rete aziendale. Per altre informazioni, vedere [Deploy a task sequence](../../../osd/deploy-use/deploy-a-task-sequence.md).

### <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Miglioramenti alla sequenza di attività di aggiornamento sul posto di Windows 10
<!-- 1357425 -->
Il modello di sequenza di attività predefinita per l'aggiornamento sul posto di Windows 10 include ora gruppi aggiuntivi con azioni consigliate da aggiungere prima e dopo il processo di aggiornamento. Queste azioni sono comuni tra numerosi clienti che stanno aggiornando i propri dispositivi a Windows 10. Per altre informazioni, vedere [Creare una sequenza di attività per aggiornare un sistema operativo](../../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md#recommended-task-sequence-steps-to-prepare-for-upgrade).

### <a name="improvements-to-operating-system-deployment"></a>Miglioramenti alla distribuzione del sistema operativo
Questa versione include i miglioramenti seguenti alla distribuzione del sistema operativo:
- In Windows PE quando si avvia cmtrace.exe non viene più richiesto di scegliere se rendere questo programma lo strumento di visualizzazione predefinito per i file di log. <!-- SMS 500897 -->
- Aggiungere immagini d'avvio al passaggio [Scarica contenuto pacchetto](../../../osd/understand/task-sequence-steps.md#BKMK_DownloadPackageContent) della sequenza di attività.
- Miglioramenti del passaggio [Esegui la sequenza di attività](../../../osd/understand/task-sequence-steps.md#child-task-sequence): <!-- 1261338 -->   
  - Supporto per tutti gli scenari di distribuzione del sistema operativo da Software Center, PXE e dai supporti.
  - Miglioramenti apportati alle operazioni della console, come copia, importazione, esportazione e generazione di avvisi durante l'eliminazione di oggetti.
  - Supporto per la [Creazione guidata file di contenuto pre-installazione](../hierarchy/manage-network-bandwidth.md#BKMK_PrestagingContent).
  - Integrazione con la verifica della distribuzione. Per altre informazioni, vedere [Distribuzioni di sequenze di attività ad alto rischio](../../../osd/deploy-use/deploy-a-task-sequence.md). 
  - Il passaggio Esegui la sequenza di attività può ora essere usato a più livelli di sequenze di attività e non solo in un'unica relazione padre/figlio. Poiché le relazioni a più livelli aggiungono complessità, usarle con attenzione. Queste relazioni vengono comunque controllate per individuare i riferimenti circolari.

### <a name="deployment-templates-for-task-sequences"></a>Modelli di distribuzione per le sequenze di attività
<!-- 1357391 -->
Ora la [distribuzione guidata per le sequenze di attività](../../../osd/deploy-use/deploy-a-task-sequence.md) può creare un modello di distribuzione. Il modello di distribuzione può essere salvato e applicato a una sequenza di attività nuova o esistente per creare una distribuzione. 

### <a name="phased-deployments-for-task-sequences"></a>Distribuzioni in più fasi per le sequenze di attività
<!--1356837-->
 Le distribuzioni in più fasi sono una [funzionalità di versione non definitiva](../../servers/manage/pre-release-features.md). Le distribuzioni in più fasi automatizzano un'implementazione coordinata e in sequenza di una sequenza di attività in più raccolte. È possibile [creare distribuzioni in più fasi](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md) con l'impostazione predefinita di due fasi oppure configurare manualmente più fasi. La distribuzione in più fasi delle sequenze di attività non supporta l'installazione di PXE o di supporti.




## <a name="software-center"></a>Software Center

### <a name="install-multiple-applications-in-software-center"></a>Installare più applicazioni nel Software Center
<!-- 1357126 -->
Se un utente finale o un tecnico desktop deve installare più applicazioni in un dispositivo, il Software Center ora supporta l'installazione di più applicazioni selezionate. Questo comportamento consente all'utente di essere più efficiente senza dover aspettare che termini un'installazione prima di avviare quella successiva. Per altre informazioni, vedere [Installare più applicazioni](../../understand/software-center.md#install-multiple-applications) nel nuovo Manuale dell'utente di Software Center.

### <a name="use-software-center-to-browse-and-install-user-available-applications-on-azure-ad-joined-devices"></a>Usare Software Center per esplorare e installare le applicazioni disponibili per gli utenti in dispositivi aggiunti ad Azure AD
<!-- 1322613 -->
Se si distribuiscono applicazioni come disponibili agli utenti, questi possono ora esplorarle e installarle tramite Software Center nei dispositivi Azure Active Directory (Azure AD). Per altre informazioni, vedere [Deploy user-available applications on Azure AD-joined devices](../../../apps/deploy-use/deploy-applications.md#deploy-user-available-applications-on-azure-ad-joined-devices) (Distribuire applicazioni disponibili per l'utente in dispositivi aggiunti ad Azure AD).

### <a name="hide-installed-applications-in-software-center"></a>Nascondi le applicazioni installate in Software Center
<!--1357592-->
Le applicazioni installate possono ora essere nascoste in Software Center. Quando questa opzione è abilitata nelle impostazioni del client, le applicazioni già installate non vengono più visualizzate nella scheda Applicazioni. L'opzione abilitata è l'impostazione predefinita quando si installa o si esegue l'aggiornamento a Configuration Manager 1802.  Le applicazioni installate sono ancora visualizzabili nella scheda Stato installazione. [Nascondi le applicazioni installate in Software Center](../../clients/deploy/about-client-settings.md#bkmk_HideInstalled) include altri dettagli.   

### <a name="hide-unapproved-applications-in-software-center"></a>Nascondi le applicazioni non approvate nel Software Center
 <!--1355146-->
Quando questa impostazione del client è abilitata, le applicazioni disponibili per l'utente che richiedono l'approvazione sono nascoste in Software Center.  [Nascondi le applicazioni non approvate nel Software Center](../../clients/deploy/about-client-settings.md#bkmk_HideUnapproved) include altri dettagli.  

### <a name="software-center-shows-user-additional-compliance-information"></a>Software Center offre all'utente informazioni di conformità aggiuntive
<!-- 1235616 -->
 Quando si usa lo stato di Attestazione dell'integrità del dispositivo come regola dei criteri di conformità per l'accesso condizionale alle risorse aziendali, Software Center ora visualizza per l'utente l'impostazione di Attestazione dell'integrità del dispositivo che non è conforme.


 ## <a name="software-updates"></a>Aggiornamenti software 

### <a name="schedule-automatic-deployment-rule-evaluation-to-be-offset-from-a-base-day"></a>Pianificare la valutazione di una regola di distribuzione automatica con un offset da un giorno di base. 
<!--1357133-->
È possibile pianificare la valutazione delle regole di distribuzione automatica con un offset da un giorno di base. Se, ad esempio, Patch Tuesday (martedì) per l'utente cade effettivamente di mercoledì, è possibile impostare la pianificazione della valutazione per il secondo martedì del mese con un offset di un giorno. Per informazioni dettagliate, vedere [Distribuire automaticamente gli aggiornamenti software](../../../sum/deploy-use/automatically-deploy-software-updates.md#BKMK_CreateAutomaticDeploymentRule). 



## <a name="reporting"></a>Reporting

### <a name="report-for-default-browser-counts"></a>Report sul numero di browser predefiniti
<!-- 1357830 -->
È disponibile un nuovo report che mostra il numero di client con un Web browser specifico come impostazione predefinita di Windows. Vedere il report **Numero di browser predefiniti** nel gruppo di report **Software - Società e prodotti**. Per altre informazioni, vedere [Elenco dei report](../../servers/manage/list-of-reports.md#software---companies-and-products).

### <a name="report-on-windows-autopilot-device-information"></a>Report sulle informazioni sui dispositivi Windows Autopilot
<!-- 1351442 -->
Windows Autopilot è una soluzione per l'onboarding e la configurazione di nuovi dispositivi Windows 10 in un modo moderno. Per altre informazioni, vedere [Panoramica di Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-10-autopilot). Un metodo per registrare i dispositivi esistenti con Windows Autopilot consiste nel caricare le informazioni sul dispositivo in Microsoft Store per le aziende e per la formazione. Queste informazioni includono il numero di serie del dispositivo, l'identificatore del prodotto Windows e un ID hardware. Usare Configuration Manager per raccogliere e segnalare queste informazioni con il nuovo report **Informazioni sui dispositivi di Windows Autopilot** nel nodo dei report **Hardware - Generale**. Per altre informazioni, vedere [How to prepare internet-based devices for co-management](../../../comanage/how-to-prepare-Win10.md#windows-autopilot) (Come preparare i dispositivi basati su Internet per la co-gestione).

### <a name="report-on-windows-10-servicing-details-for-a-specific-collection"></a>Report sui dettagli della manutenzione di Windows 10 per una raccolta specifica
<!--1357653-->
Il report **Dettagli della manutenzione di Windows 10 per una raccolta specifica** visualizza informazioni generali sulla manutenzione di Windows 10 per una raccolta specifica. Questo report mostra le informazioni seguenti relative ai dispositivi Windows 10: ID risorsa, nome NetBIOS, nome del sistema operativo, versione del sistema operativo, build, branch del sistema operativo e stato di manutenzione. Per altre informazioni, vedere [Elenco dei report](../../servers/manage/list-of-reports.md#operating-system).



<!-- ## Inventory  -->



<!-- ## Mobile device management -->



 ## <a name="protect-devices"></a>Proteggere i dispositivi

### <a name="improvements-to-configuration-manager-policies-for-windows-defender-exploit-guard"></a>Miglioramenti ai criteri di Configuration Manager per Windows Defender Exploit Guard
<!-- 1356220 -->
Ulteriori impostazioni dei criteri per i componenti [Riduzione della superficie di attacco](../../../protect/deploy-use/create-deploy-exploit-guard-policy.md#bkmk_ASR) e [Accesso controllato alle cartelle](../../../protect/deploy-use/create-deploy-exploit-guard-policy.md#bkmk_CFA) sono state aggiunte in Configuration Manager per [Windows Defender Exploit Guard](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-attack-surface-reduction).

### <a name="new-host-interaction-settings-for-windows-defender-application-guard"></a>Nuove impostazioni per l'interazione con l'host per Windows Defender Application Guard
<!-- 1356256 -->
Per i dispositivi Windows 10 versione 1709 e successive sono disponibili due nuove impostazioni per l'interazione con l'host per [Windows Defender Application Guard](../../../protect/deploy-use/create-deploy-application-guard-policy.md#bkmk_HIS): 
- È possibile concedere ai siti Web l'accesso all'unità di elaborazione grafica virtuale dell'host. 
- È possibile salvare in modo permanente nell'host i file scaricati all'interno del contenitore. 




## <a name="configuration-manager-console"></a>Console di Configuration Manager

### <a name="improvements-to-the-configuration-manager-console"></a>Miglioramenti della console di Configuration Manager 
Questa versione include i miglioramenti seguenti alla console di Configuration Manager.
- Gli elenchi di dispositivi in Asset e conformità, Dispositivi, ora visualizzano l'utente primario per impostazione predefinita. Questa colonna viene visualizzata solo nel nodo Dispositivi. L'ultimo utente connesso può inoltre essere aggiunto come colonna facoltativa.<!-- 1357280 --> Abilitare le impostazioni del client [Affinità dispositivi e utenti](../../clients/deploy/about-client-settings.md#user-and-device-affinity) per il sito per associare un utente primario a un dispositivo.
- Se una raccolta è membro di un'altra raccolta e viene rinominata, il nuovo nome viene aggiornato nelle regole di appartenenza.<!--1357282--> 
- Quando si usa il controllo remoto in un client con più monitor con ridimensionamenti DPI diversi, il cursore del mouse ora esegue correttamente il mapping. <!--433170-->
- Il [dashboard di Gestione client di Office 365](../../../sum/deploy-use/office-365-dashboard.md) visualizza un elenco di dispositivi rilevanti quando vengono selezionate le sezioni del grafico. <!--1357281 --> 



## <a name="next-steps"></a>Passaggi successivi
Quando si è pronti per installare questa versione, vedere [Aggiornamenti per System Center Configuration Manager](../../servers/manage/updates.md).
