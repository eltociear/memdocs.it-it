---
title: Technical Preview 1806.2
titleSuffix: Configuration Manager
description: Informazioni sulle nuove funzionalità disponibili in Configuration Manager Technical Preview versione 1806.2.
ms.date: 06/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3af2a69d-30e7-4dce-832d-82b7a1c082f8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: b7643c73d2e9dad00e926bdc3db905016c45860a
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905213"
---
# <a name="capabilities-in-technical-preview-18062-for-configuration-manager"></a>Funzionalità della versione Technical Preview 1806.2 per Configuration Manager

*Si applica a: Configuration Manager (Technical Preview Branch)*

Questo articolo presenta le funzionalità disponibili nella Technical Preview per Configuration Manager, versione 1806.2. È possibile installare questa versione per aggiornare il sito delle anteprime tecniche aggiungendovi nuove funzionalità. 

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

### <a name="clients-dont-automatically-update"></a><a name="ki_sqlncli"></a> I client non vengono aggiornati automaticamente
<!--518760-->
Durante l'aggiornamento alla versione 1806.2, il sito aggiorna anche SQL Native Client e ciò può causare un riavvio in sospeso nel server del sito. Questo ritardo impedisce l'aggiornamento di determinati file, con effetti sull'aggiornamento automatico del client.

#### <a name="workarounds"></a>Soluzioni alternative
Per evitare questo problema, aggiornare manualmente SQL Native Client *prima di aggiornare* Configuration Manager alla versione 1806.2. Per altre informazioni, vedere l'[aggiornamento di manutenzione più recente di SQL Server 2012 Native Client](https://www.microsoft.com/download/details.aspx?id=50402).

Se il sito è già stato aggiornato, l'aggiornamento del client automatico e il push del client non funzioneranno. È necessario aggiornare i client per testare completamente la maggior parte delle nuove funzionalità. Aggiornare manualmente i client Technical Preview usando la procedura seguente:  

1. Individuare i file di origine client nella cartella **CMUClient** della directory di installazione di Configuration Manager nel server del sito. Ad esempio: `C:\Program Files\Configuration Manager\CMUClient`  

2. Copiare l'intera cartella CMUClient nel dispositivo client. Ad esempio: `C:\Temp\CMUClient`  

    Questo percorso può essere una condivisione di rete accessibile dai client.  

3. Eseguire la riga di comando seguente da un prompt dei comandi con privilegi elevati: `C:\Temp\CMUClient\ccmsetup.exe /source:C:\Temp\CMUClient`  

Per l'installazione di un nuovo client nel sito con versione Technical Preview 1806.2 usare lo stesso processo. 

> [!Important]  
> Non usare il parametro della riga di comando `/MP` in questo scenario. Questo parametro è prioritario rispetto a `/source` e fa sì che ccmsetup scarichi il contenuto client dal punto di gestione o dal punto di distribuzione.
> 
> È possibile usare proprietà della riga di comando, come SMSSITECODE o CCMLOGLEVEL, ma non dovrebbe essere necessario per l'aggiornamento di un client esistente. 


### <a name="version-18062-shows-version-1806-in-about-configuration-manager"></a><a name="ki_version"></a> La versione 1806.2 indica la versione 1806 in Informazioni su Configuration Manager
<!--518148-->
Dopo l'aggiornamento alla versione Technical Preview 1806.2, se si apre la finestra **Informazioni su Configuration Manager** dall'angolo superiore sinistro della console, viene ancora visualizzata la **versione 1806**. 

#### <a name="workaround"></a>Soluzione alternativa
Usare la proprietà **Versione sito** per determinare la differenza tra 1806 e 1806.2:

| Versione sito  | Version
|---------|---------|
| 5.0.**8672**.1000 | 1806 |
| 5.0.**8685**.1000 | 1806.2 |
 


</br>

**Di seguito sono riportate le nuove funzionalità disponibili con questa versione.**  


## <a name="improvements-to-phased-deployments"></a><a name="bkmk_pod"></a> Miglioramenti alle distribuzioni in più fasi

Questa versione include i miglioramenti seguenti per le [distribuzioni in più fasi](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md):
- [Stato di distribuzione in più fasi](#bkmk_pod-monitor)
- [Distribuzione in più fasi di applicazioni](#bkmk_pod-app)
- [Implementazione graduale durante le distribuzioni in più fasi](#bkmk_pod-throttle)


### <a name="phased-deployment-status"></a><a name="bkmk_pod-monitor"></a> Stato di distribuzione in più fasi
<!--1358577-->
Per le distribuzioni in più fasi è ora disponibile un'esperienza di monitoraggio nativa. Dal nodo **Distribuzioni** nell'area di lavoro **Monitoraggio** selezionare una distribuzione in più fasi e quindi fare clic su **Stato di distribuzione in più fasi** nella barra multifunzione.

![Dashboard dello stato di distribuzione in più fasi che mostra lo stato delle due fasi](media/1358577-phased-deployment-status.png)

Questo dashboard visualizza le informazioni seguenti per ogni fase della distribuzione:  

- **Dispositivi totali**: numero di dispositivi interessati da questa fase.  

- **Status** (Stato): stato corrente della fase. Ogni fase può trovarsi in uno degli stati seguenti:  

    - **La distribuzione è stata creata**: la distribuzione in più fasi ha creato una distribuzione del software nella raccolta per questa fase. Ai client viene assegnato in modo attivo questo software.  

    - **In attesa**: la fase precedente non ha ancora raggiunto i criteri di esito positivo per consentire la continuazione della distribuzione verso questa fase.  

    - **Sospeso**: un amministratore ha sospeso la distribuzione.  

- **Stato**: stati di distribuzione con codifica a colori dai client. Ad esempio: Esito positivo, In corso, Errore, Requisiti non soddisfatti e Sconosciuto. 


#### <a name="known-issue"></a>Problema noto
Il dashboard dello stato di distribuzione in più fasi potrebbe visualizzare più righe per la stessa fase.<!--518510-->


### <a name="phased-deployment-of-applications"></a><a name="bkmk_pod-app"></a> Distribuzione in più fasi di applicazioni
<!--1358147-->
Creare distribuzioni in più fasi per le applicazioni. Le distribuzioni in più fasi consentono di orchestrare un'implementazione coordinata e in sequenza del software basata su criteri e gruppi personalizzabili.

Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software** espandere **Gestione applicazioni** e selezionare **Applicazioni**. Selezionare un'applicazione e quindi fare clic su **Crea una distribuzione in più fasi** nella barra multifunzione. 

Il comportamento di una distribuzione di un'applicazione in più fasi è identico a quello delle sequenze di attività. Per altre informazioni, vedere [Creare distribuzioni in più fasi per una sequenza di attività](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md).

#### <a name="prerequisite"></a>Prerequisito
Distribuire il contenuto per l'applicazione da un punto di distribuzione prima di creare la distribuzione in più fasi.<!--518293-->

#### <a name="known-issue"></a>Problema noto
Non è possibile creare manualmente le fasi per un'applicazione. La procedura guidata crea automaticamente due fasi per le distribuzioni di applicazioni.


### <a name="gradual-rollout-during-phased-deployments"></a><a name="bkmk_pod-throttle"></a> Implementazione graduale durante le distribuzioni in più fasi
<!--1358578-->
Durante una distribuzione in più fasi, l'implementazione di ogni fase può ora essere graduale. Questo comportamento consente di ridurre il rischio di problemi di distribuzione e diminuisce il carico sulla rete causato dalla distribuzione di contenuti ai client. Il sito può rendere gradualmente disponibile il software a seconda della configurazione per ogni fase. Tutti i client in una fase hanno una scadenza definita in base al momento in cui il software viene reso disponibile. L'intervallo di tempo tra l'ora di disponibilità e la scadenza è uguale per tutti i client in una fase. 

Quando si crea una distribuzione in più fasi e si configura manualmente una fase nella pagina **Impostazioni delle fasi** dell'Aggiunta guidata fasi o nella pagina **Impostazioni** della procedura guidata Crea una distribuzione in più fasi, configurare l'opzione: **Rendi gradualmente disponibile il software in questo periodo di tempo (in giorni)** . Il valore predefinito di questa impostazione è **0**, ovvero la distribuzione non è limitata per impostazione predefinita.

> [!Note]  
> Questa opzione è attualmente disponibile solo per le distribuzioni in più fasi delle sequenze di attività.  



## <a name="support-for-new-windows-app-package-formats"></a><a name="bkmk_msix"></a> Supporto per nuovi formati di pacchetti dell'app Windows
<!--1357427-->
Configuration Manager supporta ora la distribuzione dei nuovi formati di pacchetto dell'app (con estensione msix) e bundle dell'app (con estensione msixbundle) di Windows 10. Le build più recenti di [Windows Insider Preview](https://insider.windows.com/) supportano attualmente questi nuovi formati.

Per una panoramica di MSIX, vedere [A closer look at MSIX](https://docs.microsoft.com/archive/blogs/sgern/a-closer-look-at-msix) (MSIX più da vicino).

Per informazioni su come creare una nuova app MSIX, vedere [MSIX support introduced in Insider Build 17682](https://techcommunity.microsoft.com/t5/MSIX-Blog/MSIX-support-introduced-in-Insider-Build-17682/ba-p/202376) (Introduzione del supporto di MSIX nella build di Insider 17682).

### <a name="prerequisites"></a>Prerequisiti
- Un client Windows 10 che esegue almeno Windows Insider Preview build 17682
- Un pacchetto di app Windows nel formato MSIX

### <a name="try-it-out"></a>Verifica
Provare a completare le attività. Inviare quindi [commenti e suggerimenti](capabilities-in-technical-preview-1804.md#bkmk_feedback).

1. [Creare un'applicazione](../../apps/deploy-use/create-applications.md) nella console di Configuration Manager. 
2. Selezionare il **Tipo** di file di installazione dell'applicazione **Pacchetto app Windows (\*.appx, \*.appxbundle, \*.msix, \*.msixbundle)** .
3. [Distribuire l'applicazione](../../apps/deploy-use/deploy-applications.md) al client che esegue la build più recente di Windows Insider Preview.



## <a name="improvement-to-client-push-security"></a><a name="bkmk_client-push"></a> Miglioramento della sicurezza dei push client
<!--1358204-->
Quando si usa il metodo di installazione [push client](../clients/deploy/plan/client-installation-methods.md#client-push-installation) per il client di Configuration Manager, il server del sito crea una connessione remota al client per avviare l'installazione. A partire da questa versione, il sito può richiedere l'autenticazione reciproca Kerberos non consentendo il fallback a NTLM prima di stabilire la connessione. Questo miglioramento consente di proteggere la comunicazione tra il server e il client. 

A seconda dei criteri di sicurezza, l'ambiente può già preferire o richiedere l'autenticazione Kerberos rispetto all'autenticazione NTLM meno recente. Per altre informazioni sulle considerazioni relative alla sicurezza per questi protocolli di autenticazione, vedere l'[impostazione dei criteri di sicurezza di Windows per limitare NTLM](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-security-restrict-ntlm-outgoing-ntlm-traffic-to-remote-servers#security-considerations).


### <a name="prerequisite"></a>Prerequisito

Per usare questa funzionalità, i client devono essere in una foresta di Active Directory trusted. Il protocollo Kerberos in Windows si basa su Active Directory per l'autenticazione reciproca. 


### <a name="try-it-out"></a>Verifica

Provare a completare le attività. Inviare quindi [commenti e suggerimenti](capabilities-in-technical-preview-1804.md#bkmk_feedback).

Quando si aggiorna il sito, viene mantenuto il comportamento esistente. Dopo aver *aperto* le proprietà di installazione push client, il sito abilita automaticamente la verifica di Kerberos. Se necessario, è possibile consentire alla connessione di ricorrere all'uso di una connessione NTLM meno sicura, anche se non è consigliato. 

1. Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Configurazione del sito** e selezionare **Siti**. Selezionare il sito di destinazione. Nella barra multifunzione fare clic su **Impostazioni di installazione client** e selezionare **Installazione push client**.  

2. Per il sito è ora abilitato il controllo di Kerberos per l'installazione push client. Fare clic su **OK** per chiudere la finestra.  

3. Se necessario per l'ambiente, nella finestra Proprietà installazione push client, nella scheda **Generale**, vedere l'opzione **Allow connection fallback to NTLM** (Consenti fallback connessione a NTLM). Questa opzione è disabilitata per impostazione predefinita. 



## <a name="management-insights-for-proactive-maintenance"></a><a name="bkmk_insights"></a> Informazioni dettagliate sulla gestione per la manutenzione proattiva
<!--1352184,et al-->
In questa versione sono disponibili informazioni dettagliate sulla gestione aggiuntive per evidenziare i potenziali problemi di configurazione. Esaminare le regole seguenti nel nuovo gruppo **Manutenzione proattiva**:  

- **Elementi di configurazione inutilizzati**: elementi di configurazione che non fanno parte di una linea di base di configurazione e sono anteriori a 30 giorni.  

- **Immagini d'avvio inutilizzate**: immagini di avvio a cui non viene fatto riferimento per l'avvio PXE o per l'uso di sequenze di attività.  

- **Gruppi di limiti senza sistemi del sito assegnati**: senza sistemi del sito assegnati, i gruppi di limiti possono essere usati solo per l'assegnazione del sito.  

- **Gruppi di limiti senza membri**: i gruppi di limiti non sono applicabili per l'assegnazione del sito o la ricerca di contenuto se non hanno membri.  

- **Punti di distribuzione che non forniscono contenuti ai client**: punti di distribuzione che non hanno reso disponibile contenuto ai client negli ultimi 30 giorni. I dati sono basati sui report dai client della relativa cronologia di download.  

- **Expired updates found** (Trovati aggiornamenti scaduti): gli aggiornamenti scaduti non sono applicabili per la distribuzione.   



## <a name="transition-mobile-apps-workload-for-co-managed-devices"></a><a name="bkmk_comgmt"></a> Transizione del carico di lavoro per le app per dispositivi mobili per dispositivi con co-gestione
<!--1357892-->
È possibile gestire le app per dispositivi mobili con Microsoft Intune continuando al tempo stesso a usare Configuration Manager per distribuire applicazioni desktop di Windows. Per eseguire la transizione del carico di lavoro per le app per dispositivi mobili, andare alla pagina delle proprietà di co-gestione. Spostare il dispositivo di scorrimento da Configuration Manager a Pilota o Tutto. 

Dopo la transizione di questo carico di lavoro, qualsiasi app disponibile distribuita da Intune sarà disponibile nel portale aziendale. Le app distribuite da Configuration Manager sono disponibili in Software Center. 

Per altre informazioni, vedere gli articoli seguenti:  

- [Co-gestione per dispositivi Windows 10](../../comanage/overview.md)  

- [Informazioni sulla gestione delle app in Microsoft Intune](https://docs.microsoft.com/intune/app-management)  



## <a name="boundary-group-options-for-peer-downloads"></a><a name="bkmk_bgoptions"></a> Opzioni del gruppo di limiti per download peer
<!--1356193-->
Sono ora disponibili impostazioni aggiuntive per i gruppi di limiti per offrire maggiore controllo sulla distribuzione di contenuti nell'ambiente. Questa versione aggiunge le opzioni seguenti:  

- **Consenti i download peer in questo gruppo di limiti**: Questa opzione è attivata per impostazione predefinita. Il punto di gestione fornisce ai client un elenco di posizioni del contenuto che include le origini peer. <!--This setting also affects applying Group IDs for Delivery Optimization.518268-->  

    Esistono due scenari comuni in cui potrebbe essere utile disabilitare questa opzione:  

    - In presenza di un gruppo di limiti che include limiti da posizioni geograficamente dislocate, come una VPN. Due client possono essere inclusi nello stesso gruppo di limiti perché sono connessi tramite VPN, ma trovarsi in luoghi molto lontani non appropriati per la condivisione peer del contenuto.  

    - Se si usa un singolo gruppo di limiti di grandi dimensioni per l'assegnazione del sito che non fa riferimento ad alcun punto di distribuzione.  

- **Durante i download peer, usa solo i peer entro la stessa subnet**: Questa impostazione dipende da quella precedente. Se si abilita questa opzione, il punto di gestione include nell'elenco delle posizioni del contenuto solo le origini peer incluse nella stessa subnet del client.

    Scenari comuni per l'abilitazione di questa opzione:

    - La progettazione del gruppo di limiti per la distribuzione del contenuto include un solo gruppo di limiti di grandi dimensioni che si sovrappone ad altri gruppi di limiti più piccoli. Con questa nuova impostazione, l'elenco di origini di contenuto che il punto di gestione fornisce ai client include solo le origini peer dalla stessa subnet.

    - È disponibile un singolo gruppo di limiti di grandi dimensioni per tutti gli uffici remoti. Abilitare questa opzione e i client potranno condividere solo il contenuto all'interno della subnet nell'ufficio remoto, invece di correre i rischi correlati alla condivisione del contenuto tra posizioni diverse.


### <a name="known-issue"></a>Problema noto
Se il client dell'origine peer ha più di un indirizzo IP (IPv4, IPv6 o entrambi), il peer caching non funziona. La nuova opzione **Durante i download peer, usa solo i peer entro la stessa subnet** non ha alcun effetto se l'origine peer ha più di un indirizzo IP.<!--518661-->   



## <a name="third-party-software-updates-support-for-custom-catalogs"></a><a name="bkmk_3pupdate"></a> Supporto per gli aggiornamenti software di terze parti per i cataloghi personalizzati
<!--1358714-->
Questa versione esegue un'ulteriore iterazione sul supporto per gli aggiornamenti software di terze parti in seguito ai [commenti e suggerimenti raccolti con UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8803711-3rd-party-patching-scup-integration-with-sccm-co). [Technical Preview versione 1806](capabilities-in-technical-preview-1806.md#bkmk-3pupdate) ha reso disponibile il supporto per *cataloghi partner*, ovvero cataloghi registrati da fornitori di software. I cataloghi forniti, non registrati con Microsoft, sono denominati *cataloghi personalizzati*. Aggiungere cataloghi personalizzati nella console di Configuration Manager.  


### <a name="prerequisites"></a>Prerequisiti 

- Configurare gli [aggiornamenti software di terze parti](capabilities-in-technical-preview-1806.md#bkmk-3pupdate). Completare la Fase 1: abilitare e configurare la funzionalità.   

- Un catalogo personalizzato con firma digitale contiene aggiornamenti software con firma digitale.  

- Per l'amministratore sono necessarie le autorizzazioni seguenti:  

    - Sito: Creazione, Modifica  


### <a name="try-it-out"></a>Verifica

Provare a completare le attività. Inviare quindi [commenti e suggerimenti](capabilities-in-technical-preview-1804.md#bkmk_feedback).

1. Nella console di Configuration Manager passare all'area di lavoro **Raccolta software**, espandere **Aggiornamenti software** e selezionare il nodo **Cataloghi di aggiornamenti software di terze parti**. Fare clic su **Aggiungi catalogo personalizzato** nella barra multifunzione.  

2. Nella pagina **Generale** specificare i dettagli seguenti:  

    - **URL di download**: un indirizzo HTTPS valido del catalogo personalizzato.  

    - **Editore**: nome dell'organizzazione che pubblica il catalogo.  

    - **Nome**: nome del catalogo da visualizzare nella console di Configuration Manager.  

    - **Descrizione**: una descrizione del catalogo.  

    - **URL supporto tecnico** (facoltativo): indirizzo HTTPS valido di un sito Web per ottenere assistenza con il catalogo.  

    - **Contatto supporto tecnico** (facoltativo): informazioni di contatto per ottenere assistenza con il catalogo.  

3. Completare la procedura guidata. La procedura guidata aggiunge il nuovo catalogo in uno stato senza sottoscrizione.  

4. Sottoscrivere il catalogo personalizzato usando l'azione esistente **Sottoscrivi il catalogo**. Per altre informazioni, vedere [Fase 2: sottoscrivere un catalogo di terze parti e sincronizzare gli aggiornamenti](capabilities-in-technical-preview-1806.md#phase-2-subscribe-to-a-third-party-catalog-and-sync-updates).  

> [!Note]  
> Non è possibile aggiungere cataloghi con lo stesso URL di download e non è possibile modificare le proprietà del catalogo. Se si specificano proprietà non corrette per un catalogo personalizzato, eliminare il catalogo prima di aggiungerlo nuovamente.  


#### <a name="unsubscribe-from-a-catalog"></a>Annullare la sottoscrizione a un catalogo
Per annullare la sottoscrizione da un catalogo, selezionare il catalogo desiderato nell'elenco e fare clic su **Annulla la sottoscrizione al catalogo** nella barra multifunzione. Se si annulla la sottoscrizione da un catalogo, si verificano le azioni e i comportamenti seguenti: 
- Il sito interrompe la sincronizzazione dei nuovi aggiornamenti 
- Il sito blocca i certificati associati per la firma del catalogo e l'aggiornamento del contenuto. 
- Gli aggiornamenti esistenti non vengono rimossi, ma potrebbe non essere possibile pubblicarli o distribuirli.

#### <a name="delete-a-custom-catalog"></a>Eliminare un catalogo personalizzato
Eliminare i cataloghi personalizzati dallo stesso nodo della console. Selezionare un catalogo personalizzato in stato *senza sottoscrizione* e fare clic su **Elimina il catalogo personalizzato**. Se il catalogo è già stato sottoscritto, annullare la sottoscrizione prima di eliminarlo. Non è possibile eliminare i cataloghi dei partner. L'eliminazione di un catalogo personalizzato ne comporta la rimozione dall'elenco dei cataloghi. Questa azione non riguarda gli aggiornamenti software pubblicati nel punto di aggiornamento software.


### <a name="known-issue"></a>Problema noto
L'azione di eliminazione per i cataloghi personalizzati risulta non disponibile, pertanto non è possibile eliminare cataloghi personalizzati dalla console. Per risolvere questo problema, usare lo strumento **wbemtest** nel server del sito. Recuperare l'istanza che si vuole eliminare usando il nome o l'URL di download, ad esempio: `select * from SMS_ISVCatalog where DownloadURL="http://www.contoso.com/catalog.cab"`. Nella finestra dei risultati di query selezionare l'oggetto e fare clic su **Elimina**.<!--518676-->  



## <a name="improvements-to-cloud-management-features"></a><a name="bkmk_cloud"></a> Miglioramenti delle funzionalità di gestione cloud

Questa versione include i miglioramenti seguenti:  

- Le funzionalità seguenti supportano ora l'uso di Azure Stati Uniti Cloud pubblica amministrazione:<!--511980-->  

    - Onboarding del sito per **Gestione del Cloud** tramite [Servizi di Azure](../servers/deploy/configure/azure-services-wizard.md)  

    - Distribuzione di un [gateway di gestione cloud con Azure Resource Manager](../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager)  

    - Distribuzione di un [punto di distribuzione cloud con Azure Resource Manager](capabilities-in-technical-preview-1805.md#cloud-distribution-point-support-for-azure-resource-manager)  

- I clienti usano Windows AutoPilot per il provisioning di Windows 10 nei dispositivi aggiunti ad Azure Active Directory che sono connessi alla rete locale. Per installare o aggiornare il client di Configuration Manager su questi dispositivi, ora non è più necessario un punto di distribuzione cloud o un punto di distribuzione locale con l'opzione **Consenti connessione anonima dei client** configurata. In alternativa, abilitare l'opzione del sito **Use Configuration Manager-generated certificates for HTTP site systems** (Usa certificati generati da Configuration Manager per i sistemi del sito HTTP), che consente a un client aggiunto a un dominio cloud di comunicare con un punto di distribuzione abilitato per HTTP locale. Per altre informazioni, vedere [Comunicazioni client sicure migliorate](https://docs.microsoft.com/sccm/core/get-started/capabilities-in-technical-preview-1805#improved-secure-client-communications).<!--515854-->  



## <a name="new-software-updates-compliance-report"></a><a name="bkmk_report"></a> Nuovo report di conformità degli aggiornamenti software
<!--1357775-->
La visualizzazione dei report per la conformità degli aggiornamenti software include in genere dati dei client che non hanno contattato il sito di recente. Un nuovo report consente di filtrare i risultati di conformità per un gruppo di aggiornamenti software specifico in base ai client "integri". Questo report mostra lo stato di conformità più realistico dei client attivi nell'ambiente in uso. 
 
Per visualizzare il report, passare all'area di lavoro **Monitoraggio**, espandere **Report**, espandere **Report**, espandere **Aggiornamenti software - Conformità A** e selezionare **Conformità 9 - Dati complessivi su integrità e conformità**. Specificare lo stato **Gruppo di aggiornamento**, **Nome raccolta** e **Stato client**.

Il report include le parti seguenti:
- **Clienti integri rispetto a client totali**: questo grafico a barre confronta i client "integri" che hanno comunicato con il sito nel periodo di tempo specificato rispetto al numero totale di client nella raccolta specificata.
- **Panoramica conformità**: grafico a torta che visualizza lo stato di conformità generale per il gruppo di aggiornamenti software specifico nei client attivi nella raccolta specificata.
- **Top 5 Non-Compliant by Article ID** (Primi 5 non conformi in base a ID articolo): questo grafico a barre visualizza i primi cinque aggiornamenti software nel gruppo specificato che non sono conformi nei client attivi nella raccolta specificata.
- La parte inferiore del report è una tabella con altri dettagli, in cui sono elencati gli aggiornamenti software nel gruppo specificato.



## <a name="next-steps"></a>Passaggi successivi
Per informazioni sull'installazione o l'aggiornamento del ramo Technical Preview, vedere [Technical Preview per Configuration Manager](technical-preview.md).    
