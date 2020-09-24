---
title: Pianificare gli aggiornamenti software
titleSuffix: Configuration Manager
description: La pianificazione dell'infrastruttura del punto di aggiornamento software è essenziale prima di usare gli aggiornamenti software in un ambiente di produzione di Configuration Manager.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 09/16/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: d071b0ec-e070-40a9-b7d4-564b92a5465f
ms.openlocfilehash: c38f3b509ba6104647dd60c8284fde52b5b4995e
ms.sourcegitcommit: 6176a7825d6c663faa318a6818b7764bc70f08fc
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/17/2020
ms.locfileid: "90718825"
---
# <a name="plan-for-software-updates-in-configuration-manager"></a>Pianificare gli aggiornamenti software in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Prima di usare gli aggiornamenti software in un ambiente di produzione di Configuration Manager, è importante eseguire il processo di pianificazione. La definizione di una pianificazione valida per l'infrastruttura del punto di aggiornamento software è fondamentale per un'implementazione corretta di aggiornamenti software. Per informazioni sulla pianificazione della capacità per gli aggiornamenti software, vedere [Numeri di ridimensionamento e scalabilità](../../core/plan-design/configs/size-and-scale-numbers.md#software-update-point).


##  <a name="determine-the-software-update-point-infrastructure"></a><a name="BKMK_SUPInfrastructure"></a> Determinare l'infrastruttura del punto di aggiornamento software  

Questa sezione include i seguenti argomenti secondari:    
- [Elenco dei punti di aggiornamento software](#BKMK_SUPList)
- [Passaggio a un nuovo punto di aggiornamento software](#BKMK_SUPSwitching)
- [Passare manualmente i client a un nuovo punto di aggiornamento software](#BKMK_ManuallySwitchSUPs)
- [Punti di aggiornamento software in una foresta non trusted](#BKMK_SUP_CrossForest)
- [Usare un server WSUS esistente come origine di sincronizzazione nel sito principale](#BKMK_WSUSSyncSource)
- [Punto di aggiornamento software in un sito secondario](#BKMK_SUPSecSite)  
- [Pianificare client basati su Internet](#bkmk_internet-clients)  
- [Pianificare i contenuti degli aggiornamenti software](#bkmk_content)  
- [Pianificare gli aggiornamenti di terze parti](#bkmk_thirdparty)  


Il sito di amministrazione centrale e tutti i siti primari figlio devono avere un punto di aggiornamento software. Quando si pianifica l'infrastruttura del punto di aggiornamento software, determinare le dipendenze seguenti:
- La posizione in cui installare il punto di aggiornamento software per il sito  
- Quali siti richiedono un punto di aggiornamento software che accetta la comunicazione da client basati su Internet
- Se è necessario un punto di aggiornamento software in siti secondari  

> [!IMPORTANT]  
>  Per altre informazioni sulle dipendenze interne ed esterne necessarie per gli aggiornamenti software, vedere [Prerequisiti per gli aggiornamenti software](prerequisites-for-software-updates.md).  

È possibile aggiungere più punti di aggiornamento software in un sito primario di Configuration Manager per rendere disponibile la tolleranza di errore. La struttura di failover del punto di aggiornamento software è anche diversa dal modello di pura sequenza casuale usato nella struttura dei punti di gestione. A differenza di questi ultimi, il passaggio a un nuovo punto di aggiornamento software comporta costi in termini di prestazioni di rete e client per la struttura dei punti di gestione. Quando il client passa a un nuovo server WSUS per analizzare gli aggiornamenti software, il risultato è un incremento nella dimensione del catalogo e nelle richieste in termini di prestazioni di rete e lato client associate. Di conseguenza il client mantiene l'affinità con l'ultimo punto di aggiornamento software dal quale ha eseguito correttamente l'analisi.  

Il primo punto di aggiornamento software installato su un sito primario è l'origine di sincronizzazione per tutti gli ulteriori punti di aggiornamento software aggiunti nel sito primario. Dopo aver aggiunto i punti di aggiornamento software e avviato la sincronizzazione, visualizzare lo stato dei punti di aggiornamento software e l'origine di sincronizzazione dal nodo **Stato di sincronizzazione del punto di aggiornamento software** nell'area di lavoro **Monitoraggio**.  

Quando si verifica un errore del punto di aggiornamento software configurato come origine di sincronizzazione per il sito, rimuovere manualmente il ruolo che origina l'errore. Quindi selezionare un nuovo punto di aggiornamento software da usare come origine di sincronizzazione. Per altre informazioni, vedere [Rimuovere un ruolo del sistema del sito](../../core/servers/deploy/install/uninstall-sites-and-hierarchies.md#bkmk_role).  


###  <a name="software-update-point-list"></a><a name="BKMK_SUPList"></a> Elenco dei punti di aggiornamento software  

Configuration Manager offre al client un elenco di punti di aggiornamento software nei seguenti scenari:  

- Un nuovo client riceve i criteri per abilitare gli aggiornamenti software  

- Un client non riesce a contattare il punto di aggiornamento software assegnato e deve passare a un altro punto  

Il client seleziona un punto di aggiornamento software a caso dall'elenco. Assegna la priorità ai punti di aggiornamento software appartenenti alla stessa foresta. Configuration Manager offre ai client un elenco diverso a seconda del tipo di client:  

-   **Client basati su Intranet**: si riceve un elenco di punti di aggiornamento software che è possibile configurare per consentire solo connessioni dalla Intranet oppure un elenco di punti di aggiornamento software che consentono connessioni client Internet e Intranet.  

-   **Client basati su Internet**: si riceve un elenco di punti di aggiornamento software che è possibile configurare per consentire solo connessioni da Internet oppure un elenco di punti di aggiornamento software che consentono connessioni client Internet e Intranet.  


###  <a name="software-update-point-switching"></a><a name="BKMK_SUPSwitching"></a> Passaggio a un nuovo punto di aggiornamento software  

> [!NOTE]  
> I client usano i gruppi di limiti per trovare un nuovo punto di aggiornamento software. Se il loro punto di aggiornamento software corrente non è più accessibile, usano anche i gruppi di limiti per eseguire il fallback e trovare un nuovo punto. Aggiungere singoli punti di aggiornamento software a diversi gruppi di limiti per controllare quali server possono essere trovati da un client. Per altre informazioni, vedere [Punti di aggiornamento software](../../core/servers/deploy/configure/boundary-groups.md#bkmk_sup).  

Se sono presenti più punti di aggiornamento software in un sito e uno di questi registra un errore o non è più disponibile, i client si connettono a un altro punto di aggiornamento software. Con questo nuovo server i client continuano a cercare gli aggiornamenti software più recenti. Quando un client viene inizialmente assegnato a un punto di aggiornamento software, resta assegnato a tale punto, salvo errori durante l'analisi.  

L'analisi degli aggiornamenti software può avere un esito negativo con una serie di diversi codici di errore relativi a nuovi tentativi o mancati tentativi. In caso di analisi non riuscita con un codice di errore di nuovi tentativi, il client avvia un processo di nuovi tentativi di analisi degli aggiornamenti software sul relativo punto. Le condizioni di alto livello che generano tale codice di errore sono spesso attribuibili a un server WSUS non disponibile o temporaneamente sovraccarico. Quando il client non riesce ad analizzare gli aggiornamenti software, adotta il processo seguente:  

1.  Il client esegue l'analisi degli aggiornamenti software:  
    - All'ora pianificata
    - Quando viene eseguito manualmente dal pannello di controllo sul client
    - Quando viene eseguito manualmente dalla console di Configuration Manager tramite un'azione di notifica client
    - Quando viene eseguito da un metodo di Configuration Manager SDK  

2.  Se l'analisi ha esito negativo, il client attende 30 minuti prima di riprovare. Il punto di aggiornamento software usato è lo stesso.  

3.  Il client esegue almeno quattro tentativi a intervalli di 30 minuti. Al quarto tentativo non riuscito, e dopo aver atteso altri due minuti, il client passa al punto di aggiornamento software successivo nel proprio elenco.  

4.  Il client ripete questo processo con il nuovo punto di aggiornamento software. Dopo un'analisi con esito positivo, il client continua a connettersi al nuovo punto di aggiornamento software.  

L'elenco seguente include informazioni aggiuntive utili per i tentativi di connessione a un punto di aggiornamento software e gli scenari di commutazione:  

-   Se un client è disconnesso dall'intranet e non riesce ad analizzare gli aggiornamenti software, non passa a un altro punto di aggiornamento software. Si tratta di un errore previsto, perché il client non è in grado di raggiungere la rete interna o un punto di aggiornamento software che consente le connessioni dall'intranet. Il client di Configuration Manager determina la disponibilità del punto di aggiornamento software intranet.  

-   Se si gestiscono client su Internet e sono stati configurati più punti di aggiornamento software per l'accettazione delle comunicazioni da client su Internet, il processo di commutazione si svolge con la sequenza di nuovi tentativi standard descritta nello scenario precedente.  

-   Se il processo di analisi viene avviato ma il client viene spento prima del completamento dell'analisi, questa situazione non viene considerata come condizione di errore di analisi e non viene inclusa tra i quattro tentativi disponibili.  

Se l'agente di Windows Update invia a Configuration Manager uno dei codici di errore seguenti, il client riprova a stabilire la connessione:  

2149842970, 2147954429, 2149859352, 2149859362, 2149859338, 2149859344, 2147954430, 2147747475, 2149842974, 2149859342, 2149859372, 2149859341, 2149904388, 2149859371, 2149859367, 2149859366, 2149859364, 2149859363, 2149859361, 2149859360, 2149859359, 2149859358, 2149859357, 2149859356, 2149859354, 2149859353, 2149859350, 2149859349, 2149859340, 2149859339, 2149859332, 2149859333, 2149859334, 2149859337, 2149859336, 2149859335

Per conoscere il significato di un codice di errore, convertire il codice di errore decimale in formato esadecimale e cercare il valore esadecimale in un sito, ad esempio [Windows Update Agent - Error Codes Wiki](https://social.technet.microsoft.com/wiki/contents/articles/15260.windows-update-agent-error-codes.aspx) (Agente di Windows Update: wiki codici di errore). Ad esempio il codice di errore decimale 2149842970 corrisponde a 8024001A esadecimale, ovvero WU_E_POLICY_NOT_SET - Un valore dei criteri non è stato impostato.  


###  <a name="manually-switch-clients-to-a-new-software-update-point"></a><a name="BKMK_ManuallySwitchSUPs"></a> Passare manualmente i client a un nuovo punto di aggiornamento software

È possibile commutare i client di Configuration Manager a un nuovo punto di aggiornamento software quando si verificano problemi con il punto di aggiornamento software attivo. Questa modifica avviene solo quando un client riceve più punti di aggiornamento software da un punto di gestione.

> [!IMPORTANT]    
> Quando si passa a un altro dispositivo per usare un nuovo server, i dispositivi trovano il nuovo server tramite fallback. I client passano al nuovo punto di aggiornamento software durante il successivo ciclo di analisi per aggiornamenti software.<!-- SCCMDocs#1537 -->
>
> Prima di avviare questa modifica esaminare le configurazioni dei gruppi di limiti e assicurarsi che i punti di aggiornamento software si trovino nei gruppi di limite appropriati. Per altre informazioni, vedere [Punti di aggiornamento software](../../core/servers/deploy/configure/boundary-groups.md#bkmk_sup).  
>
> La commutazione a un nuovo punto di aggiornamento software genera traffico di rete aggiuntivo. La quantità di traffico dipende dalle impostazioni di configurazione di WSUS, ad esempio le classificazioni e i prodotti sincronizzati o l'uso di un database WSUS condiviso. Se si prevede di commutare più dispositivi, è consigliabile pianificare l'attività durante una finestra di manutenzione. In tal modo si riduce l'impatto sulle prestazioni di rete quando i client effettuano la scansione con il nuovo punto di aggiornamento software.  

#### <a name="process-to-switch-software-update-points"></a>Processo per commutare i punti di aggiornamento software  
Avviare questa modifica in una raccolta di dispositivi. Dopo che l'opzione è stata attivata, all'analisi successiva il client cerca un altro punto di aggiornamento software.  

1.  Nella console di Configuration Manager passare all'area di lavoro **Asset e conformità** e selezionare il nodo **Raccolte dispositivi**.  

2.  Selezionare la raccolta di destinazione. Nel gruppo **Raccolta** della scheda **Home** della barra multifunzione, fare clic su **Notifica client** e quindi su **Passare al punto di aggiornamento software successivo**.  


###  <a name="software-update-points-in-an-untrusted-forest"></a><a name="BKMK_SUP_CrossForest"></a> Punti di aggiornamento software in una foresta non trusted  

È possibile creare uno o più punti di aggiornamento software in un sito per supportare client in una foresta non trusted. Per aggiungere un punto di aggiornamento software in un'altra foresta, prima installare e configurare un server WSUS nella foresta. Avviare quindi la procedura guidata per aggiungere un server del sito di Configuration Manager con il ruolo di sistema del sito del punto di aggiornamento software. Nella procedura guidata, configurare le seguenti impostazioni per connettersi al server WSUS nella foresta non trusted:  

-   Specificare un **account di installazione del sistema del sito** in grado di accedere al server WSUS nella foresta non trusted.  

-   Specificare un **account di connessione al server WSUS** per la connessione a tale server.  

Ad esempio, si dispone di un sito primario nella foresta A con due punti di aggiornamento software (SUP01 e SUP02). Per lo stesso sito primario vi sono anche due punti di aggiornamento software (SUP03 e SUP04) nella foresta B. Quando si verifica la commutazione al punto di aggiornamento software successivo, i client danno la priorità ai server appartenenti alla stessa foresta.  


###  <a name="use-an-existing-wsus-server-as-the-synchronization-source-at-the-top-level-site"></a><a name="BKMK_WSUSSyncSource"></a> Usare un server WSUS esistente come origine di sincronizzazione nel sito principale  

In genere, il sito di livello superiore della gerarchia è configurato per sincronizzare i metadati degli aggiornamenti software con Microsoft Update. Quando i criteri di protezione dell'organizzazione non consentono l'accesso a Internet al sito di livello superiore, configurare l'origine di sincronizzazione per il sito di livello superiore per l'uso di un server WSUS. Questo server WSUS non è incluso nella gerarchia di Configuration Manager dell'organizzazione. Ad esempio è presente un server WSUS in una rete connessa a Internet (rete perimetrale), ma il sito di livello superiore si trova in una rete interna senza accesso a Internet. Configurare il server WSUS nella rete perimetrale come origine di sincronizzazione per i metadati degli aggiornamenti software. Configurare il server WSUS nella rete perimetrale per la sincronizzazione degli aggiornamenti software con gli stessi criteri necessari in Configuration Manager. In caso contrario, il sito di livello superiore potrebbe non essere in grado di sincronizzare gli aggiornamenti software previsti. Quando si installa il punto di aggiornamento software, configurare un account di connessione server WSUS. Questo account deve avere accesso al server WSUS nella rete perimetrale. Verificare anche che il firewall consenta il traffico sulle porte appropriate. Per altre informazioni, vedere le [porte usate dal punto di aggiornamento software per l'origine di sincronizzazione](../../core/plan-design/hierarchy/ports.md#BKMK_PortsSUP-WSUS).  


###  <a name="software-update-point-on-a-secondary-site"></a><a name="BKMK_SUPSecSite"></a> Punto di aggiornamento software in un sito secondario  

Il punto di aggiornamento software è facoltativo in un sito secondario. Installare un solo punto di aggiornamento software in un sito secondario. Quando un punto di aggiornamento software non è installato nel sito secondario, i dispositivi inclusi nei limiti di un sito secondario usano un punto di aggiornamento software nel sito primario assegnato. In genere un punto di aggiornamento software viene installato in un sito secondario in caso di larghezza di banda di rete limitata tra i dispositivi del sito secondario e i punti di aggiornamento software nel sito primario padre. È possibile usare questa configurazione anche quando il punto di aggiornamento software nel sito primario si avvicina al limite di capacità. Dopo l'installazione e la configurazione di un punto di aggiornamento software nel sito secondario, vengono aggiornati criteri a livello di sito per i client e tali client iniziano a usare il nuovo punto di aggiornamento software.  


### <a name="plan-for-internet-based-clients"></a><a name="bkmk_internet-clients"></a> Pianificare client basati su Internet

Se è necessario gestire dispositivi che si spostano fuori dalla rete e su Internet, è possibile sviluppare un piano per la gestione di aggiornamenti software in questi dispositivi. Configuration Manager supporta varie tecnologie per questo scenario. Usare una tecnologia o una combinazione di tecnologie in base alle esigenze, per soddisfare i requisiti dell'organizzazione.

#### <a name="cloud-management-gateway"></a>Gateway di gestione cloud
Creare un gateway di gestione cloud in Microsoft Azure e abilitare almeno un punto di aggiornamento software locale per consentire il traffico dai client basati su Internet. Quando i client effettuano il roaming in Internet, continuano a eseguire l'analisi sui punti di aggiornamento software. Tutti i client basati su Internet ottengono sempre i contenuti dal servizio cloud Microsoft Update. 

Per altre informazioni, vedere [Pianificare per Cloud Management Gateway](../../core/clients/manage/cmg/plan-cloud-management-gateway.md) e [Configurare gruppi di limiti](../../core/servers/deploy/configure/boundary-groups.md#bkmk_sup).  

#### <a name="internet-based-client-management"></a>Gestione client basata su Internet
Inserire un punto di aggiornamento software in una rete con connessione a Internet e abilitarlo per consentire il traffico da client basati su Internet. Quando i client effettuano il roaming in Internet passano su questo punto di aggiornamento software per l'analisi. Tutti i client basati su Internet ottengono sempre i contenuti dal servizio cloud Microsoft Update.

Per altre informazioni sui vantaggi e gli svantaggi della gestione client basata su Internet, vedere [Gestire i client su Internet](../../core/clients/manage/manage-clients-internet.md).

#### <a name="windows-update-for-business"></a>Windows Update for Business
Windows Update for Business consente di tenere sempre aggiornati i dispositivi Windows 10 con miglioramenti e aggiornamenti delle funzionalità. Questi dispositivi si connettono direttamente al servizio cloud Windows Update. Configuration Manager è in grado di distinguere tra i computer Windows 10 che ricevono gli aggiornamenti software da Windows Update for Business e i computer che li ricevono da WSUS.

Per altre informazioni, vedere [Integrazione con Windows Update for Business](../deploy-use/integrate-windows-update-for-business-windows-10.md).


### <a name="plan-software-update-content"></a><a name="bkmk_content"></a> Pianificare il contenuto degli aggiornamenti software

I client devono scaricare i file di contenuto degli aggiornamenti software per installarli. Configuration Manager offre numerose tecnologie per supportare la gestione e il recapito di questo contenuto. In alternativa è possibile configurare distribuzioni di aggiornamenti software per consentire o richiedere ai client di ottenere il contenuto direttamente dal servizio cloud Microsoft Update.

#### <a name="download-and-distribute-content"></a>Scaricare e distribuire il contenuto 
Per impostazione predefinita, il processo di gestione degli aggiornamenti software in Configuration Manager usa le funzionalità di gestione del contenuto incorporate. Queste funzionalità includono la raccolta contenuto, un archivio a istanza singola centralizzato, e la struttura distribuita del ruolo del sistema del sito del punto di distribuzione. Queste funzionalità vengono usate per scaricare e inoltrare i pacchetti di distribuzione di aggiornamenti software. 

Per altre informazioni, vedere [Scaricare gli aggiornamenti software](../deploy-use/download-software-updates.md).

#### <a name="manage-express-installation-files-for-windows-10"></a>Gestire i file di installazione rapida per Windows 10
Configuration Manager supporta l'uso di file di installazione rapida per gli aggiornamenti di Windows 10. I file di aggiornamento rapido e le tecnologie di supporto, ad esempio l'ottimizzazione recapito, possono aiutare a ridurre l'impatto sulle prestazioni della rete del download di file di contenuto di grandi dimensioni nei client. 

Per altre informazioni, vedere [FAQs to optimize Windows 10 update delivery](../deploy-use/optimize-windows-10-update-delivery.md) (FAQ per ottimizzare il recapito degli aggiornamenti di Windows 10).

#### <a name="clients-download-content-from-the-internet"></a>I client scaricano il contenuto da Internet
Quando si distribuiscono aggiornamenti software ai client, configurare la distribuzione in modo che i client scarichino il contenuto dal servizio cloud di Microsoft Update. Quando i client non sono in grado di scaricare il contenuto da un'altra origine di contenuto, possono comunque scaricare il contenuto da Internet. 

A partire dalla versione 1806 non è necessario creare un pacchetto di distribuzione quando si distribuiscono gli aggiornamenti software. Quando si seleziona l'opzione **Nessun pacchetto di distribuzione**, i client possono comunque scaricare contenuto dalle origini locali, se disponibili, ma in genere lo scaricano dal servizio Microsoft Update.<!--1357933-->

I client basati su Internet scaricano sempre il contenuto dal servizio cloud Microsoft Update. Evitare di distribuire pacchetti di distribuzione di aggiornamenti software a un punto di distribuzione cloud. L'archiviazione nel punto di distribuzione cloud comporta dei costi, ma i client non scaricano i pacchetti. 


### <a name="plan-for-third-party-updates"></a><a name="bkmk_thirdparty"></a> Pianificare gli aggiornamenti di terze parti
Configuration Manager è integrato con WSUS, che supporta in modo nativo gli aggiornamenti software pubblicati da Microsoft. La maggior parte dei clienti usa altre applicazioni di terze parti che a loro volta richiedono aggiornamenti. Per l'aggiornamento costante delle applicazioni di terze parti è possibile considerare varie opzioni.

#### <a name="supersede-applications-to-update"></a>Sostituire applicazioni le applicazioni da aggiornare
Usare una relazione di sostituzione con la funzionalità di gestione applicazioni in Configuration Manager per aggiornare o sostituire le applicazioni esistenti. Quando si sostituisce un'applicazione, specificare un nuovo tipo di distribuzione che andrà a sostituire il tipo di distribuzione dell'applicazione sostituita. Decidere anche se aggiornare o disinstallare l'applicazione sostituita prima di installare l'applicazione sostitutiva.

Per altre informazioni, vedere [Rivedere e sostituire le applicazioni](../../apps/deploy-use/revise-and-supersede-applications.md).

#### <a name="third-party-software-updates"></a>Aggiornamenti software di terze parti
A partire dalla versione 1806 usare il nodo **Cataloghi di aggiornamenti software di terze parti** nella console di Configuration Manager per sottoscrivere i cataloghi di terze parti, pubblicarne gli aggiornamenti nel punto di aggiornamento software e quindi implementare i cataloghi nei client.<!--1352101-->

Per altre informazioni, vedere [Aggiornamenti software di terze parti](../deploy-use/third-party-software-updates.md).

#### <a name="system-center-updates-publisher"></a>System Center Updates Publisher
System Center Updates Publisher (SCUP) è uno strumento autonomo che consente ai provider di software indipendenti o agli sviluppatori di applicazioni line-of-business di gestire aggiornamenti personalizzati. Tali aggiornamenti includono gli aggiornamenti con dipendenze, ad esempio i driver o le aggregazioni di aggiornamenti.

Per altre informazioni, vedere [System Center Updates Publisher](../tools/updates-publisher.md).



##  <a name="plan-for-software-update-point-installation"></a><a name="BKMK_SUPInstallation"></a> Pianificare l'installazione del punto di aggiornamento software  

Questa sezione include i seguenti argomenti secondari:  
- [Requisiti per il punto di aggiornamento software](#BKMK_SUPSystemRequirements)
- [Pianificare l'installazione di WSUS](#BKMK_PlanningForWSUS)
- [Configurare i firewall](#BKMK_ConfigureFirewalls)  


Questa sezione include informazioni sulle procedure per pianificare e preparare l'installazione del punto di aggiornamento software. Prima di creare un ruolo del sistema del sito per il punto di aggiornamento software in Configuration Manager, è necessario considerare diversi requisiti. I requisiti specifici variano a seconda dell'infrastruttura di Configuration Manager. Quando si configura il punto di aggiornamento software per le comunicazioni tramite HTTPS, è particolarmente importante esaminare questa sezione. Per funzionare correttamente, i server abilitati per HTTPS richiedono passaggi aggiuntivi.  

###  <a name="requirements-for-the-software-update-point"></a><a name="BKMK_SUPSystemRequirements"></a> Requisiti per il punto di aggiornamento software  

Installare il ruolo del punto di aggiornamento software in un sistema del sito conforme ai requisiti minimi per WSUS e alle configurazioni supportate per i sistemi del sito di Configuration Manager.  

-   Per altre informazioni sui requisiti minimi per il ruolo del server WSUS in Windows Server, vedere [Rivedere le considerazioni e i requisiti di sistema](/windows-server/administration/windows-server-update-services/plan/plan-your-wsus-deployment#11-review-considerations-and-system-requirements).  

-   Per altre informazioni sulle configurazioni supportate per i sistemi del sito di Configuration Manager, vedere [Prerequisiti del sito e di sistema del sito](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  


###  <a name="plan-for-wsus-installation"></a><a name="BKMK_PlanningForWSUS"></a> Pianificare l'installazione di WSUS  

Installare su tutti i server del sistema del sito una versione supportata di WSUS, configurata per il ruolo punto di aggiornamento software. Quando non si installa un punto di aggiornamento software nel server del sito, installare la console di amministrazione WSUS nel server del sito. Questo componente consente al server del sito di comunicare con WSUS in esecuzione nel punto di aggiornamento software.  

Quando si usa WSUS in Windows Server 2012 o versioni successive, configurare autorizzazioni aggiuntive per consentire al componente **WSUS Configuration Manager** in Configuration Manager di connettersi a WSUS. Questo componente esegue controlli di integrità periodici. Scegliere una delle seguenti opzioni per configurare l'autorizzazione richiesta:  

-   Aggiungere l'account **SYSTEM** per il gruppo **WSUS Administrators**  

-   Aggiungere l'account **NT AUTHORITY\SYSTEM** come utente per il database WSUS (SUSDB). Configurare come minimo l'appartenenza al ruolo del database webService.  
  
Per altre informazioni sull'installazione di WSUS in Windows Server, vedere [Installare il ruolo server WSUS](/windows-server/administration/windows-server-update-services/deploy/1-install-the-wsus-server-role).  

In caso di installazione di più di un punto di aggiornamento software in un sito primario, utilizzare lo stesso database WSUS per ciascun punto di aggiornamento software nella stessa foresta Active Directory. La condivisione dello stesso database migliora le prestazioni quando i client passano a un nuovo punto di aggiornamento software. Per altre informazioni, vedere [Usare un database WSUS condiviso per punti di aggiornamento software](software-updates-best-practices.md#bkmk_shared-susdb).  

#### <a name="configuring-the-wsus-content-directory-path"></a>Configurazione del percorso della directory del contenuto WSUS

Quando si installa WSUS è necessario specificare un percorso per la directory del contenuto. La directory del contenuto WSUS viene usata principalmente per archiviare i file delle condizioni di licenza software Microsoft richiesti dai client durante l'analisi. La directory del contenuto WSUS non dovrebbe sovrapporsi alla directory di origine del contenuto per i pacchetti di distribuzione software di Configuration Manager. In caso di sovrapposizione della directory del contenuto WSUS e dell'origine dei pacchetti di Configuration Manager, verranno rimossi file non corretti dalla directory del contenuto WSUS.

####  <a name="configure-wsus-to-use-a-custom-website"></a><a name="BKMK_CustomWebSite"></a> Configurare WSUS per l'uso di un sito Web personalizzato  
Quando si installa WSUS, è possibile utilizzare il sito Web predefinito IIS esistente o creare un sito Web di WSUS personalizzato. Creare un sito Web personalizzato per WSUS, in modo che IIS ospiti i servizi WSUS in un sito Web virtuale dedicato. In caso contrario condividerà il sito Web usato dagli altri sistemi del sito o dalle altre applicazioni Configuration Manager. Questa configurazione è particolarmente importante quando si installa il ruolo del punto di aggiornamento software sul server del sito. Quando si esegue WSUS in Windows Server 2012 o versioni successive, per impostazione predefinita WSUS viene configurato con l'uso della porta 8530 per HTTP e della porta 8531 per HTTPS. Specificare queste porte al momento della creazione del punto di aggiornamento software in un sito.  


####  <a name="use-an-existing-wsus-infrastructure"></a><a name="BKMK_WSUSInfrastructure"></a> Uso di un'infrastruttura WSUS esistente  
Selezionare un server WSUS che era attivo nell'ambiente prima dell'installazione di Configuration Manager come punto di aggiornamento software. Quando il punto di aggiornamento software è configurato, specificare le impostazioni di sincronizzazione. Configuration Manager si connette al server WSUS eseguito nel punto di aggiornamento software e lo configura con le stesse impostazioni. 

Prima di configurare il server come punto di aggiornamento software, confrontare la configurazione di prodotti e classificazioni con le impostazioni di Configuration Manager. Se il server WSUS esistente è stato sincronizzato prima di configurarlo come punto di aggiornamento software e gli elenchi di prodotti e classificazioni sono diversi, il server sincronizza i metadati degli aggiornamenti software indipendentemente dalle impostazioni configurate. Questo comportamento produce metadati degli aggiornamenti software imprevisti nel database del sito. 

Lo stesso comportamento viene registrato in caso di aggiunta di prodotti o classificazioni direttamente nella console di amministrazione di WSUS e di successivo avvio immediato di una sincronizzazione. Per impostazione predefinita, Configuration Manager si connette ogni ora a WSUS e reimposta qualsiasi impostazione modificata al di fuori di Configuration Manager. Gli aggiornamenti software non conformi ai prodotti e alle classificazioni specificati nelle impostazioni di sincronizzazione vengono impostati come scaduti. Quindi vengono rimossi dal database del sito.  

Quando un server WSUS è configurato come punto di aggiornamento software, non è più possibile usarlo come server WSUS autonomo. Se è necessario un server WSUS autonomo separato non gestito da Configuration Manager, configurarlo in un altro server.  

####  <a name="configure-wsus-as-a-replica-server"></a><a name="BKMK_WSUSAsReplica"></a> Configurare WSUS come server di replica  
Quando si aggiunge il ruolo punto di aggiornamento software in un server del sito primario, non è possibile usare un server WSUS configurato come una replica. Se il server WSUS viene configurato come server di replica, Configuration Manager non riesce a configurarlo e non è possibile completare la sincronizzazione di WSUS. Il primo punto di aggiornamento software installato in un sito primario è il punto predefinito. I punti di aggiornamento software aggiuntivi nel sito sono configurati come repliche del punto di aggiornamento software predefinito.  

####  <a name="decide-whether-to-configure-wsus-to-use-ssl"></a><a name="BKMK_WSUSandSSL"></a> Decidere se configurare WSUS per l'uso di SSL  

È vivamente consigliabile usare il protocollo SSL per proteggere il punto di aggiornamento software. WSUS utilizza SSL per l'autenticazione tra computer client e server WSUS downstream e il server WSUS. WSUS utilizza inoltre SSL per crittografare i metadati dell'aggiornamento software. Se si sceglie di proteggere WSUS con SSL, preparare il server WSUS prima di installare il punto di aggiornamento software.

Quando si installa e si configura il punto di aggiornamento software, selezionare l'impostazione **Abilita le comunicazioni SSL per il server WSUS**. In caso contrario, Configuration Manager configura WSUS in modo che non usi SSL. Quando si abilita SSL in un punto di aggiornamento software, configurare anche tutti i punti di aggiornamento software nei siti figlio per l'uso di SSL. Per altre informazioni, vedere l'esercitazione [Configurare un punto di aggiornamento software per l'uso di TLS/SSL con un certificato PKI](../get-started/software-update-point-ssl.md).

###  <a name="configure-firewalls"></a><a name="BKMK_ConfigureFirewalls"></a> Configurare i firewall  

Il punto di aggiornamento software in un sito di amministrazione centrale di Configuration Manager comunica con WSUS nel punto di aggiornamento software. WSUS comunica con l'origine di sincronizzazione per sincronizzare i metadati degli aggiornamenti software. I punti di aggiornamento software in un sito figlio comunicano con il punto di aggiornamento software nel sito padre. Quando è presente più di un punto di aggiornamento software in un sito primario, i punti di aggiornamento software aggiuntivi comunicano con il punto di aggiornamento software predefinito. Il ruolo predefinito corrisponde al primo punto di aggiornamento software installato nel sito.  

Può essere necessario configurare il firewall in modo da consentire il traffico HTTP o HTTPS usato da WSUS negli scenari seguenti: 
- Tra il punto di aggiornamento software e Internet
- Tra un punto di aggiornamento software e la relativa origine di sincronizzazione upstream
- Tra punti di aggiornamento software aggiuntivi  

La connessione a Microsoft Update viene sempre configurata per utilizzare la porta 80 per HTTP e la porta 443 per HTTPS. Usare una porta personalizzata per la connessione da WSUS sul punto di aggiornamento software in un sito figlio a WSUS sul punto di aggiornamento software nel sito padre. Quando i criteri di sicurezza non consentono la connessione, usare il metodo di sincronizzazione esportazione e importazione. Per altre informazioni, vedere la sezione [Origine di sincronizzazione](#BKMK_SyncSource) in questo articolo. Per altre informazioni sulle porte usate da WSUS, vedere [Come determinare le impostazioni di porta usate da WSUS in Configuration Manager](../get-started/install-a-software-update-point.md#wsus-settings).  


#### <a name="restrict-access-to-specific-domains"></a>Limitare l'accesso a domini specifici  

Se l'organizzazione limita le comunicazioni della rete con Internet tramite un firewall o un dispositivo proxy, è necessario consentire al punto di aggiornamento software attivo di accedere agli endpoint Internet. WSUS e Aggiornamenti automatici possono quindi comunicare con il servizio cloud Microsoft Update.

Per altre informazioni, vedere i [requisiti di accesso Internet](../../core/plan-design/network/internet-endpoints.md#bkmk_sum).


##  <a name="plan-for-synchronization-settings"></a><a name="BKMK_SyncSettings"></a> Pianificare le impostazioni di sincronizzazione  

Questa sezione include i seguenti argomenti secondari:  
- [Origine di sincronizzazione](#BKMK_SyncSource)
- [Pianificazione della sincronizzazione](#BKMK_SyncSchedule)
- [Classificazioni degli aggiornamenti](#BKMK_UpdateClassifications)
- [Prodotti](#BKMK_UpdateProducts)
- [Regole di sostituzione](#BKMK_SupersedenceRules)
- [Lingue](#BKMK_UpdateLanguages)  
- [Tempo di esecuzione massimo](#bkmk_maxruntime)


La sincronizzazione degli aggiornamenti software in Configuration Manager scarica i metadati degli aggiornamenti software in base ai criteri configurati. Il sito di livello superiore nella gerarchia sincronizza gli aggiornamenti software da Microsoft Update. È possibile scegliere di configurare il punto di aggiornamento software nel sito principale per la sincronizzazione con un server WSUS esistente, non nella gerarchia di Configuration Manager. I siti primari figlio sincronizzano i metadati degli aggiornamenti software dal punto di aggiornamento software nel sito di amministrazione centrale. Prima di installare e configurare un punto di aggiornamento software, utilizzare questa sezione per pianificare le impostazioni di sincronizzazione.  


###  <a name="synchronization-source"></a><a name="BKMK_SyncSource"></a> Origine di sincronizzazione  

Le impostazioni dell'origine di sincronizzazione per il punto di aggiornamento software specificano il percorso in cui il punto di aggiornamento software recupera i metadati degli aggiornamenti software. Le impostazioni specificano anche se il processo di sincronizzazione crea eventi di reporting WSUS.  

-   **Origine di sincronizzazione**: per impostazione predefinita, il punto di aggiornamento software nel sito di livello superiore configura l'origine di sincronizzazione per Microsoft Update. È possibile sincronizzare il sito principale con un server WSUS esistente. Il punto di aggiornamento software in un sito primario figlio configura l'origine di sincronizzazione come il punto di aggiornamento software nel sito di amministrazione centrale.  

    -  Il primo punto di aggiornamento software installato in un sito primario, ovvero il punto predefinito, si sincronizza con il sito di amministrazione centrale. I punti di aggiornamento software aggiuntivi nel sito primario si sincronizzano con il punto di aggiornamento software predefinito nel sito primario.  

    - Quando un punto di aggiornamento software è disconnesso da Microsoft Update o dal server aggiornamenti upstream, impostare l'origine di sincronizzazione in modo che non esegua la sincronizzazione con un'origine di sincronizzazione configurata. Configurarla invece per l'uso della funzione di esportazione e importazione dello strumento **WSUSUtil** per la sincronizzazione degli aggiornamenti software. Per altre informazioni, vedere [Sincronizzare gli aggiornamenti software da un punto di aggiornamento software disconnesso](../get-started/synchronize-software-updates-disconnected.md).  

-   **Eventi di reporting WSUS:** l'agente di Windows Update nei computer client è in grado di creare messaggi di eventi per il reporting WSUS. Questi eventi non vengono usati da Configuration Manager. Di conseguenza l'opzione **Non creare eventi di reporting WSUS** è selezionata per impostazione predefinita. Quando questi eventi non vengono creati, il client deve connettersi al server WSUS solo durante la valutazione dell'aggiornamento software e le analisi di conformità. Se questi eventi sono necessari per il reporting al di fuori di Configuration Manager, è necessario modificare questa impostazione in modo da creare gli eventi di reporting WSUS.  


###  <a name="synchronization-schedule"></a><a name="BKMK_SyncSchedule"></a> Pianificazione della sincronizzazione  

Configurare la pianificazione della sincronizzazione solo nel punto di aggiornamento software del sito principale della gerarchia di Configuration Manager. Quando si configura la pianificazione della sincronizzazione, il punto di aggiornamento software si sincronizza con l'origine di sincronizzazione alla data e all'ora specificata. La pianificazione personalizzata consente di sincronizzare gli aggiornamenti software per l'ottimizzazione dell'ambiente. Prendere in considerazione le esigenze di prestazioni del server WSUS, del server del sito e della rete. Un orario di esempio possono essere le 2:00 una volta alla settimana. In alternativa, avviare manualmente la sincronizzazione nel sito principale usando l'azione **Sincronizzazione degli aggiornamenti software** dal nodo **Tutti gli aggiornamenti software** o **Gruppi di aggiornamenti software** nella console di Configuration Manager.  

> [!TIP]  
>  Pianificare la sincronizzazione degli aggiornamenti software da eseguire usando un orario appropriato per l'ambiente. Un tipico scenario è quello che prevede di impostare la pianificazione della sincronizzazione poco dopo il normale rilascio di aggiornamenti software Microsoft, il secondo martedì di ogni mese. In genere questa giornata è definita *Patch Tuesday*. Se si usa Configuration Manager per recapitare aggiornamenti delle definizioni e del motore di Endpoint Protection e Windows Defender, è consigliabile impostare la pianificazione della sincronizzazione per l'esecuzione giornaliera.  

Dopo il completamento della sincronizzazione del punto di aggiornamento software, questo invia una richiesta di sincronizzazione ai siti figlio. Se sono disponibili punti di aggiornamento software aggiuntivi in un sito primario, il sito invia la richiesta di sincronizzazione a ogni punto di aggiornamento software. Questo processo viene ripetuto in ogni sito nella gerarchia.  


###  <a name="update-classifications"></a><a name="BKMK_UpdateClassifications"></a> Classificazioni degli aggiornamenti  

Ogni aggiornamento software viene definito in base a una classificazione di aggiornamento che consente di organizzare i diversi tipi di aggiornamenti. Durante il processo di sincronizzazione il sito sincronizza i metadati per le classificazioni selezionate. 

Configuration Manager supporta la sincronizzazione delle classificazioni aggiornamenti seguenti:  

-   **Aggiornamenti critici**: aggiornamento rilasciato su vasta scala per un problema specifico, per un bug critico, non correlato alla sicurezza.  

-   **Aggiornamenti delle definizioni**: aggiornamento per virus o altri file di definizione.  

-   **Feature Pack**: nuove funzionalità del prodotto distribuite al di fuori di una versione del prodotto. In genere sono incluse nella versione successiva del prodotto completo.  

-   **Aggiornamenti della sicurezza**: aggiornamento rilasciato su vasta scala per un problema specifico del prodotto e correlato alla sicurezza.  

-   **Service Pack**: set cumulativo di hotfix applicati a un sistema operativo o a un'applicazione. Questi aggiornamenti rapidi includono aggiornamenti della sicurezza, aggiornamenti critici e aggiornamenti software.  

-   **Strumenti**: utilità o funzionalità che consentono di completare una o più attività.  

-   **Aggiornamenti cumulativi**: set cumulativo di hotfix inclusi nello stesso pacchetto per facilitarne la distribuzione. Questi aggiornamenti rapidi includono aggiornamenti della sicurezza, aggiornamenti critici e aggiornamenti software. Un aggiornamento cumulativo è relativo in genere a un'area specifica, ad esempio la sicurezza o un componente del prodotto.  

-   **Aggiornamenti**: aggiornamento di un'applicazione o di un file attualmente installato.  

-   **Aggiornamenti delle funzionalità**: aggiornamento delle funzionalità a una nuova versione di Windows 10.  

Configurare le impostazioni delle classificazioni aggiornamento solo nel sito di livello superiore. Tali impostazioni non vengono configurate nel punto di aggiornamento software dei siti figlio, poiché i metadati degli aggiornamenti software vengono replicati dal sito di livello superiore. Quando si selezionano le classificazioni di aggiornamento, tenere presente che quante più classificazioni vengono selezionate tanto maggiore sarà il tempo richiesto per la sincronizzazione dei metadati degli aggiornamenti software.  

> [!WARNING]  
>  Prima di sincronizzare per la prima volta è consigliabile deselezionare tutte le classificazioni. Dopo la sincronizzazione iniziale selezionare le classificazioni desiderate, quindi eseguire nuovamente la sincronizzazione.  


###  <a name="products"></a><a name="BKMK_UpdateProducts"></a> Prodotti  

I metadati per ogni aggiornamento software definiscono uno o più prodotti ai quali è applicabile l'aggiornamento. Un prodotto è un'edizione specifica di un sistema operativo o di un'applicazione. Un esempio di prodotto è Microsoft Windows 10. Una famiglia di prodotti è il sistema operativo o l'applicazione di base da cui derivano i singoli prodotti. Un esempio di famiglia di prodotti è Microsoft Windows, alla quale appartengono Windows 10 e Windows Server 2016. Selezionare una famiglia di prodotti o singoli prodotti all'interno di una famiglia di prodotti.  

Se gli aggiornamenti software sono applicabili a più prodotti e almeno uno dei prodotti è selezionato per la sincronizzazione, tutti i prodotti vengono visualizzati nella console di Configuration Manager, anche se alcuni non sono stati selezionati. Si supponga ad esempio di selezionare solo il prodotto Windows Server 2012. Se un aggiornamento software si applica a Windows Server 2012 e Windows Server 2012 Datacenter Edition, entrambi i prodotti sono inclusi nel database del sito.  

Configurare le impostazioni del prodotto solo nel sito di livello superiore. Tali impostazioni non vengono configurate nel punto di aggiornamento software per i siti figlio poiché i metadati degli aggiornamenti software vengono replicati dal sito di livello superiore. Maggiore è il numero di prodotti selezionati, maggiore è il tempo necessario per sincronizzare i metadati degli aggiornamenti software.  

> [!IMPORTANT]  
>  Configuration Manager archivia un elenco di prodotti e famiglie di prodotti che è possibile scegliere quando si installa per la prima volta il punto di aggiornamento software. I prodotti e le famiglie di prodotti rilasciate dopo il rilascio di Configuration Manager potrebbero non essere disponibili per la selezione finché non si completa la sincronizzazione. Il processo di sincronizzazione aggiorna l'elenco dei prodotti e delle famiglie di prodotti disponibili e selezionabili. Deselezionare tutti i prodotti prima di sincronizzare gli aggiornamenti software per la prima volta. Dopo la sincronizzazione iniziale selezionare i prodotti desiderati, quindi eseguire nuovamente la sincronizzazione.  


###  <a name="supersedence-rules"></a><a name="BKMK_SupersedenceRules"></a> Regole di sostituzione  

In genere, un aggiornamento software che sostituisce un altro aggiornamento software consente di effettuare una o più delle seguenti azioni:  

-   Migliora o aggiorna la correzione fornita da uno o più aggiornamenti rilasciati in precedenza.  

-   Migliora l'efficienza del pacchetto dei file di aggiornamento sostituito, che viene installato sui client se l'aggiornamento viene approvato per l'installazione. Ad esempio, l'aggiornamento sostituito potrebbe contenere file che non sono più rilevanti per l'aggiornamento o per i sistemi operativi supportati dal nuovo aggiornamento. Questi file non sono inclusi nel pacchetto di file sostitutivo dell'aggiornamento.  

-   Aggiorna versioni più recenti di un prodotto. In altre parole, aggiorna le versioni che non sono più applicabili alle versioni o configurazioni di un prodotto precedenti. Gli aggiornamenti possono anche sostituire altri aggiornamenti, se sono state apportate modifiche per espandere il supporto della lingua. Ad esempio, una revisione recente di un aggiornamento prodotto per Microsoft 365 Apps potrebbe rimuovere il supporto per un sistema operativo precedente, ma potrebbe aggiungere supporto aggiuntivo per nuove lingue al rilascio di aggiornamento iniziale.  

Nelle proprietà del punto di aggiornamento software specificare che gli aggiornamenti software sostituiti scadono immediatamente. Questa impostazione ne impedisce l'inclusione nelle nuove distribuzioni. L'impostazione contrassegna anche le distribuzioni esistenti per indicare che contengono uno o più aggiornamenti software scaduti. In alternativa, specificare un periodo di tempo trascorso il quale gli aggiornamenti software sostituiti scadono. Questa azione consente di continuare a distribuirli. 

Prendere in considerazione i seguenti scenari in cui potrebbe essere necessario distribuire un aggiornamento software sostituito:  

-   Un aggiornamento software sostitutivo supporta solo le versioni più recenti di un sistema operativo. Alcuni computer client eseguono versioni precedenti del sistema operativo.  

-   Un aggiornamento software sostitutivo ha un'applicabilità più limitata dell'aggiornamento software sostituito. Questo potrebbe renderlo inappropriato per alcuni client.  

-   Un aggiornamento software sostitutivo potrebbe non essere stato approvato per la distribuzione nell'ambiente di produzione.  

    > [!NOTE]  
    > - Prima di Configuration Manager versione 1806, quando Configuration Manager imposta un aggiornamento software sostituito su **Scaduto**, non imposta l'aggiornamento su **Rifiutato** in WSUS. I client continuano a eseguire l'analisi dell'aggiornamento scaduto finché l'aggiornamento non viene rifiutato manualmente o tramite uno script personalizzato.  Dopo Configuration Manager versione 1806, Configuration Manager rifiuterà anche gli aggiornamenti sostituiti in WSUS. Per altre informazioni sull'attività di pulizia di WSUS, vedere [Manutenzione degli aggiornamenti software](../deploy-use/software-updates-maintenance.md).
    > - A partire dalla versione 1810 è possibile specificare il comportamento delle regole di sostituzione per gli **aggiornamenti delle funzionalità** separatamente dagli **aggiornamenti non delle funzionalità**.

###  <a name="languages"></a><a name="BKMK_UpdateLanguages"></a> Lingue  

Le impostazioni della lingua per il punto di aggiornamento software consentono di configurare: 
- Le lingue per cui i dettagli di riepilogo (metadati degli aggiornamenti software) vengono sincronizzati per gli aggiornamenti software  
- Le lingue dei file di aggiornamento software che vengono scaricate per gli aggiornamenti software  

#### <a name="software-update-file"></a>File di aggiornamento software  
Configurare le lingue per l'impostazione **File di aggiornamento software** nelle proprietà del punto di aggiornamento software. Questa impostazione include le lingue predefinite che sono disponibili quando si scaricano aggiornamenti software in un sito. Modificare le lingue selezionate per impostazione predefinita ogni volta che gli aggiornamenti software vengono scaricati o distribuiti. Durante il processo di download, i file di aggiornamento software per le lingue configurate vengono scaricati nel percorso di origine del pacchetto di distribuzione, se i file di aggiornamento software sono disponibili nella lingua selezionata. Quindi vengono copiati nella raccolta contenuto sul server del sito. Successivamente vengono distribuiti ai punti di distribuzione configurati per il pacchetto.  

Configurare le impostazioni della lingua dei file di aggiornamento software con le lingue usate più di frequente nell'ambiente. Ad esempio i client del sito usano prevalentemente inglese e giapponese per Windows o le applicazioni. Nel sito vengono usate anche altre lingue. Quando si scarica o distribuisce l'aggiornamento software, selezionare solo inglese e giapponese nella colonna **File di aggiornamento software**. Questa operazione consente di usare le impostazioni predefinite nella pagina **Selezione lingua** della distribuzione e di scaricare le procedure guidate. Impedisce anche il download di file di aggiornamento non necessari. Configurare questa impostazione in ogni punto di aggiornamento software della gerarchia di Configuration Manager.  



#### <a name="summary-details"></a>Dettagli di riepilogo  
Durante il processo di sincronizzazione, le informazioni dei dettagli di riepilogo (metadati degli aggiornamenti software) vengono aggiornate per gli aggiornamenti software nelle lingue specificate. I metadati restituiscono informazioni sull'aggiornamento software, ad esempio:
- Name
- Descrizione
- Prodotti supportati dall'aggiornamento
- Classificazione aggiornamento
- ID articolo
- URL di download
- Regole di applicabilità

Configurare le impostazioni dei dettagli di riepilogo solo nel sito di livello superiore. I dettagli di riepilogo non vengono configurati nel punto di aggiornamento software nei siti figlio, poiché i metadati degli aggiornamenti software vengono replicati dal sito di amministrazione centrale usando la replica basata su file. Quando si selezionano le lingue dei dettagli di riepilogo, selezionare solo le lingue necessarie per l'ambiente. Più lingue vengono selezionate, maggiore è il tempo necessario per sincronizzare i metadati degli aggiornamenti software. Configuration Manager consente di visualizzare i metadati degli aggiornamenti software nelle impostazioni locali del sistema operativo in cui viene eseguita la console di Configuration Manager. Se le proprietà localizzate per gli aggiornamenti software non sono disponibili per le impostazioni locali del sistema operativo, le informazioni degli aggiornamenti software vengono visualizzate in inglese.  

> [!IMPORTANT]  
>  Selezionare tutte le lingue necessarie per i dettagli di riepilogo. Quando il punto di aggiornamento software nel sito di livello superiore viene sincronizzato con l'origine di sincronizzazione, le lingue dei dettagli di riepilogo selezionate determinano i metadati degli aggiornamenti software recuperati. Se si modificano le lingue dei dettagli di riepilogo dopo che la sincronizzazione è stata eseguita almeno una volta, i metadati degli aggiornamenti software vengono recuperati solo per aggiornamenti software nuovi o modificati. Gli aggiornamenti software che sono già stati sincronizzati non vengono aggiornati con i nuovi metadati per le lingue modificate, a meno che non sia presente una modifica all'aggiornamento software nell'origine di sincronizzazione.


###  <a name="maximum-run-time"></a><a name="bkmk_maxruntime"></a> Tempo di esecuzione massimo
<!--3734426-->
*(Funzionalità introdotta nella versione 1906)*

A partire dalla versione 1906, è possibile specificare il tempo di esecuzione massimo per completare l'installazione di un aggiornamento software. Il tempo di esecuzione massimo può essere specificato per le operazioni seguenti:

- **Tempo di esecuzione massimo per gli aggiornamenti di funzionalità Windows (minuti)**
  - **Aggiornamenti delle funzionalità**: un aggiornamento che è in una di queste tre classificazioni:
    - Aggiornamenti
    - Aggiornamenti cumulativi
    - Service Pack

- **Tempo di esecuzione massimo per gli aggiornamenti di Office 365 e gli aggiornamenti non delle funzionalità per Windows (minuti)**
  - **Aggiornamenti non di funzionalità**: un aggiornamento che non è un aggiornamento della funzionalità e il cui prodotto è elencato come uno dei seguenti:
    - Windows 10 (tutte le versioni)
    - Windows Server 2012
    - R2 per Windows Server 2012
    - Windows Server 2016
    - Windows Server 2019
    - Office 365

- Queste impostazioni cambiano solo il tempo di esecuzione massimo per i nuovi aggiornamenti sincronizzati da Microsoft Update. Non cambiano il tempo di esecuzione per gli aggiornamenti di funzionalità o non di funzionalità già esistenti.
- Tutti gli altri prodotti e classificazioni non sono configurabili con questa impostazione. Se è necessario modificare il tempo di esecuzione massimo di uno di questi aggiornamenti, [configurare le impostazioni di aggiornamento software](../get-started/manage-settings-for-software-updates.md#BKMK_SoftwareUpdatesSettings)

> [!NOTE]
> Nella versione 1906 il tempo di esecuzione massimo non è disponibile quando si installa il punto di aggiornamento software principale. Al termine dell'installazione, modificare il tempo di esecuzione massimo nel punto di aggiornamento software principale.

##  <a name="plan-for-a-software-updates-maintenance-window"></a><a name="BKMK_MaintenanceWindow"></a> Piano per una finestra di manutenzione di aggiornamenti software  

Aggiungere una finestra di manutenzione dedicata per l'installazione di aggiornamenti software. Questa azione consente di configurare una finestra di manutenzione generale e una finestra di manutenzione diversa per gli aggiornamenti software. Quando si configura sia una finestra di manutenzione generale sia una finestra di manutenzione degli aggiornamenti software, i client installano aggiornamenti software solo nella finestra di manutenzione degli aggiornamenti software. 

A partire da Configuration Manager versione 1810 è possibile modificare questo comportamento e consentire l'installazione degli aggiornamenti software durante una finestra di manutenzione generale. Per altre informazioni su questa impostazione client, vedere [Impostazioni client degli aggiornamenti software](../../core/clients/deploy/about-client-settings.md#bkmk_SUMMaint).

Per altre informazioni sulle finestre di manutenzione, vedere [Come usare le finestre di manutenzione](../../core/clients/manage/collections/use-maintenance-windows.md).  


##  <a name="restart-options-for-windows-10-clients-after-software-update-installation"></a><a name="BKMK_RestartOptions"></a> Opzioni di riavvio per i client Windows 10 dopo l'installazione degli aggiornamenti software

Quando un aggiornamento software che richiede il riavvio viene distribuito e installato tramite Configuration Manager, il client pianifica un riavvio in sospeso e visualizza una finestra di dialogo di riavvio.

Quando è presente un riavvio in sospeso per un aggiornamento software di Configuration Manager, tra le opzioni di risparmio energia di Windows nei computer Windows 10 sono disponibili **Aggiorna e riavvia** e **Aggiorna e arresta**. Dopo che una di queste opzioni è stata usata e il computer è stato riavviato, la finestra di dialogo di riavvio non viene visualizzata. In alcuni casi, il sistema operativo può rimuovere le opzioni di riavvio in sospeso. Ciò può verificarsi se è abilitata la funzionalità Avvio rapido di Windows 10. Per altre informazioni, vedere [Gli aggiornamenti potrebbero non essere installati con Avvio rapido in Windows 10](https://support.microsoft.com/help/4011287/windows-updates-not-install-with-fast-startup).

## <a name="evaluate-software-updates-after-a-servicing-stack-update"></a><a name="bkmk_ssu"></a> Valutare gli aggiornamenti software dopo un aggiornamento dello stack di manutenzione
<!--4639943-->
A partire dalla versione 2002, Configuration Manager rileva se un aggiornamento dello stack di manutenzione fa parte di un'installazione per più aggiornamenti. Quando viene rilevato un aggiornamento dello stack di manutenzione, questo viene installato per primo. Dopo aver installato l’aggiornamento dello stack di manutenzione, viene eseguito un ciclo di valutazione degli aggiornamenti software per installare gli aggiornamenti rimanenti. Questa modifica consente l'installazione di un aggiornamento cumulativo dipendente dopo l'aggiornamento dello stack di manutenzione. Non è necessario riavviare il dispositivo tra le installazioni e non è necessario creare una finestra di manutenzione aggiuntiva. Gli aggiornamenti dello stack di manutenzione vengono installati per primi solo per le installazioni non avviate dall'utente. Ad esempio, se un utente avvia un'installazione per più aggiornamenti da Software Center, è possibile che l'aggiornamento dello stack di manutenzione non venga installato per prima. L'installazione di SSUs non è disponibile per i sistemi operativi Windows Server quando si usa la versione 2002 di Configuration Manager. <!--7813007-->Questa funzionalità è stata aggiunta nella versione 2006 di Configuration Manager per i sistemi operativi Windows Server.



## <a name="next-steps"></a>Passaggi successivi
Quando si pianificano gli aggiornamenti software, vedere [Preparare la gestione degli aggiornamenti software](../get-started/prepare-for-software-updates-management.md).  

Per altre informazioni sulla gestione di Windows come servizio, vedere [Nozioni di base su Configuration Manager come servizio e Windows distribuito come servizio](../../core/understand/configuration-manager-and-windows-as-service.md).