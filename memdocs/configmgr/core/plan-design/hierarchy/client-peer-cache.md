---
title: Peer cache per i client
titleSuffix: Configuration Manager
description: Usare la peer cache per i client per i percorsi di origine client quando si distribuisce contenuto con Configuration Manager.
ms.date: 09/19/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 86cd5382-8b41-45db-a4f0-16265ae22657
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a1b9afc8c9cde94488908e4cd9737a58547326f9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703669"
---
# <a name="peer-cache-for-configuration-manager-clients"></a>Peer cache per i client di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

<!--1101436-->
Usare la peer cache per gestire la distribuzione di contenuti ai client in posizioni remote. La peer cache è una soluzione integrata di Configuration Manager che consente ai client di condividere i contenuti con altri client direttamente dalla cache locale.   

> [!Note]  
> Nella versione 1906 Configuration Manager abilita questa funzionalità per impostazione predefinita. Nella versione 1902 o precedenti Configuration Manager non abilita questa funzionalità facoltativa per impostazione predefinita. Pertanto sarà necessario abilitarla prima di poterla usare. Per altre informazioni, vedere [Enable optional features from updates](../../servers/manage/install-in-console-updates.md#bkmk_options) (Abilitare le funzioni facoltative dagli aggiornamenti).<!--505213-->  



## <a name="overview"></a>Panoramica

Definizioni:  

- **Client di peer cache**: qualsiasi client di Configuration Manager che scarica contenuto da un peer  

- **Origine di peer cache**: client di Configuration Manager che consente di usare la peer cache e include contenuto da condividere con altri client  

Usare le impostazioni client per consentire ai client di essere origini di peer cache. Non è necessario abilitare i client di peer cache. Quando si consente ai client di essere origini di peer cache, il punto di gestione li include nell'elenco delle origini di percorso del contenuto.<!--510397--> Per altre informazioni su questo processo, vedere [Operazioni](#operations).  

Un'origine di peer cache deve essere un membro del gruppo di limiti corrente del client di peer cache. Il punto di gestione non include le origini di peer cache di un gruppo di limiti vicino nell'elenco di origini di contenuto che fornisce al client, ma include solo i punti di distribuzione di un gruppo di limiti vicino. Per altre informazioni sui gruppi di limiti correnti e adiacenti, vedere [Gruppi di limiti](../../servers/deploy/configure/boundary-groups.md).<!--SCCMDocs issue 685-->  

Il client di Configuration Manager usa la peer cache per distribuire ad altri client qualsiasi tipo di contenuto presente nella cache, ad esempio file di Office 365 e file di installazione rapida.<!--SMS.500850-->  

La peer cache non sostituisce l'uso di altre soluzioni, come Windows BranchCache o Ottimizzazione recapito, ma viene usata insieme ad altre soluzioni. Queste tecnologie offrono maggiori opzioni per estendere le soluzioni tradizionali di distribuzione del contenuto, ad esempio i punti di distribuzione. La peer cache è una soluzione personalizzata che non dipende da BranchCache. Se si non abilita o non si usa BranchCache, la peer cache funziona comunque.  

> [!Note]  
> A partire dalla versione 1802, Windows BranchCache è sempre abilitato nelle distribuzioni. L'impostazione **Consenti ai client di condividere il contenuto con altri client nella stessa subnet** è stata rimossa.<!--SCCMDocs issue 539--> Se il punto di distribuzione lo supporta e se è abilitata nelle impostazioni client, i client usano BranchCache. Per altre informazioni, vedere [Configurare BranchCache](../../clients/deploy/about-client-settings.md#configure-branchcache).<!--SCCMDocs issue 735-->   



## <a name="operations"></a>Operazioni

Per abilitare la peer cache, distribuire le [impostazioni client](#bkmk_settings) in una raccolta. I membri di tale raccolta fungono quindi da origine di peer cache per altri client all'interno dello stesso gruppo di limiti.  

- Un client che agisce come origine contenuto peer invia un elenco di contenuti disponibili memorizzati nella cache al suo punto di gestione tramite messaggi di stato.

   > [!NOTE]
   > Vedere [Messaggi di stato in Configuration Manager](state-messaging-system-center-configuration-manager.md#7200-state_topictype_super_peer_update_cache_map) per l'elenco dei messaggi di stato dell'origine del contenuto peer applicabili, in particolare quelli con ID messaggio di stato 7200, 7201, 7202 e 7203.

- Un altro client nello stesso gruppo di limiti invia una richiesta di percorso del contenuto al punto di gestione. Il server restituisce l'elenco delle possibili origini del contenuto. Questo elenco include tutte le origini di peer cache che includono contenuto e sono online. Include anche i punti di distribuzione e altri percorsi di origine del contenuto in tale gruppo di limiti. Per altre informazioni, vedere [Priorità dell'origine del contenuto](fundamental-concepts-for-content-management.md#content-source-priority).  

- In genere, il client che cerca il contenuto seleziona un'origine dall'elenco specificato. A questo punto il client tenta di ottenere il contenuto.  

A partire dalla versione 1806, sono disponibili impostazioni aggiuntive per i gruppi di limiti per offrire maggiore controllo sulla distribuzione di contenuti nell'ambiente. Per altre informazioni, vedere [Opzioni del gruppo di limiti per download peer](../../servers/deploy/configure/boundary-groups.md#bkmk_bgoptions).<!--1356193-->

> [!NOTE]  
> Se il client esegue il fallback a un gruppo di limiti vicino per il contenuto, il punto di gestione non aggiunge le origini di peer cache del gruppo di limiti vicino all'elenco di possibili percorsi di origine del contenuto.  

Scegliere solo i client più adatti come origini di peer cache. Valutare l'idoneità dei client in base ad attributi come il tipo di chassis, lo spazio su disco e la connettività di rete. Per altre informazioni utili per scegliere i client più adatti da usare per la peer cache, vedere [questo blog scritto da un consulente Microsoft](https://techcommunity.microsoft.com/t5/core-infrastructure-and-security/configuration-manager-peer-cache-custom-reporting-examples/ba-p/570801).


### <a name="limited-access-to-a-peer-cache-source"></a>Accesso limitato a un'origine di peer cache  

Un'origine di peer cache rifiuta le richieste di contenuto quando soddisfa una delle condizioni seguenti nel momento in cui un peer richiede il contenuto:  

- È in modalità di batteria in esaurimento  

- Il carico del processore supera l'80%  

- L'I/O disco ha un valore di *AvgDiskQueueLength* superiore a 10  

- Non vi sono più connessioni disponibili al computer  

> [!Tip]  
> Configurare queste impostazioni usando la classe WMI del server di configurazione client per la funzionalità dell'origine peer (*SMS_WinPEPeerCacheConfig*) in Configuration Manager SDK.  

Quando l'origine di peer cache rifiuta una richiesta di contenuto, il client di peer cache continua a cercare il contenuto dall'elenco di percorsi di origine del contenuto.   



## <a name="requirements"></a>Requisiti

- La peer cache supporta tutte le versioni di Windows indicate come supportate in [Sistemi operativi supportati per client e dispositivi](../configs/supported-operating-systems-for-clients-and-devices.md). I sistemi operativi non Windows non sono supportati come origini di peer cache o client di peer cache.  

- Un'origine di peer cache deve essere un client di Configuration Manager aggiunto a un dominio. Tuttavia, un client non aggiunto a un dominio può ottenere contenuto da un'origine di peer cache aggiunta al dominio.  

- I client possono scaricare il contenuto solo origini di peer cache inclusi nel relativo gruppo di limiti corrente.  

- Non è richiesto alcun [account di accesso alla rete](accounts.md#network-access-account), ad eccezione dei casi seguenti:  

  - Configurare un account di accesso alla rete nel sito quando un client abilitato per la peer cache esegue una sequenza di attività di Software Center e viene riavviato in un'immagine d'avvio. Quando il dispositivo si trova in Windows PE, usa l'account di accesso alla rete per ottenere il contenuto dall'origine di peer cache.  

  - Quando necessario, l'origine di peer cache usa l'account di accesso alla rete per autenticare le richieste di download ricevute dai peer. Per tale scopo, a questo account sono richieste solo le autorizzazioni utente di dominio.  

- Con la versione 1802 e precedenti, l'ultimo invio dell'individuazione heartbeat del client determina il limite corrente di un'origine di peer cache. Un client che si sposta in un gruppo di limiti diverso potrebbe comunque essere un membro del relativo gruppo di limiti precedente ai fini della peer cache. Di conseguenza, a un client può essere offerta un'origine di peer cache che non si trova nel relativo percorso di rete immediato. Non abilitare i client di roaming come origine di peer cache.<!--SCCMDocs issue 641-->  

  > [!Important]  
  > A partire dalla versione 1806, Configuration Manager è più efficiente nel determinare se è stato eseguito il roaming di un'origine peer cache in un'altra posizione. Questo comportamento garantisce che il punto di gestione la offra come origine di contenuto ai client nella nuova posizione e non in quella precedente. Se si usa la funzionalità di peer cache con origini di peer cache in roaming, dopo aver aggiornato il sito alla versione 1806, aggiornare anche tutte le origini di peer cache alla versione più recente del client. Il punto di gestione non include tali origini di peer cache nell'elenco di posizioni del contenuto finché non vengono aggiornate almeno alla versione 1806.<!--SCCMDocs issue 850-->  

- Prima di provare a scaricare il contenuto, il punto di gestione verifica che l'origine di peer cache sia online.<!--sms.498675--> La convalida viene eseguita tramite il "canale veloce" per la notifica client, che usa la porta TCP 10123.<!--511673-->  

> [!Note]  
> Per sfruttare i vantaggi delle nuove funzionalità di Configuration Manager, aggiornare prima di tutto i clienti alla versione più recente. Anche se le nuove funzionalità vengono visualizzate nella console di Configuration Manager quando si esegue l'aggiornamento del sito e della console, lo scenario completo risulta funzionante solo dopo l'aggiornamento alla versione più recente del client.  



## <a name="peer-cache-client-settings"></a><a name="bkmk_settings"></a> Impostazioni del client di peer cache

Per altre informazioni sulle impostazioni del client di peer cache, vedere [Impostazioni della cache del client](../../clients/deploy/about-client-settings.md#client-cache-settings). 

Per altre informazioni sulla configurazione di queste impostazioni, vedere [Come configurare le impostazioni client](../../clients/deploy/configure-client-settings.md).

Nei client con peer cache abilitata che usano Windows Firewall, Configuration Manager configura le porte del firewall specificate nelle impostazioni client.



## <a name="partial-download-support"></a><a name="bkmk_parts"></a> Supporto per download parziale
<!--1357346-->
A partire dalla versione 1806, le origini di peer cache dei client sono in grado di dividere il contenuto in parti, grazie alle quali è possibile ridurre al minimo il trasferimento in rete, riducendo l'utilizzo della rete WAN. Il punto di gestione consente una traccia più dettagliata delle parti del contenuto e tenta di eliminare più download dello stesso contenuto per ogni gruppo di limiti. 


### <a name="example-scenario"></a>Scenario di esempio

Contoso ha un sito primario singolo con due gruppi di limiti: Headquarters (HQ) (Sede centrale) e Branch Office (Succursale). Tra i gruppi di limiti esiste una relazione di fallback di 30 minuti. Il punto di gestione e il punto di distribuzione per il sito si trovano solo all'interno del limite di HQ. La succursale non ha alcun punto di distribuzione locale. Due dei quattro client presso la succursale vengono configurati come origini di peer cache. 

![Diagramma della configurazione di rete descritta per lo scenario di esempio](media/1357346-peer-cache-source-parts.png)

1. L'obiettivo è una distribuzione di contenuto a tutti i quattro client nella succursale. Il contenuto è stato distribuito solo al punto di distribuzione.  

2. Client3 e Client4 non hanno un'origine locale per la distribuzione. Il punto di gestione indica ai client di attendere 30 minuti prima di eseguire il fallback al gruppo di limiti remoto.  

3. Client1 (PCS1) è la prima origine di peer cache ad aggiornare i criteri con il punto di gestione. Poiché questo client è abilitato come origine di peer cache, il punto di gestione indica a questo di avviare immediatamente il download della parte A dal punto di distribuzione.  

4. Quando Client2 (PCS2) contatta il punto di gestione, dato che il download della parte A è già in corso ma non è ancora completato, il punto di gestione indica a Client2 di avviare immediatamente il download della parte B dal punto di distribuzione.  

5. PCS1 completa il download della parte A e informa immediatamente il punto di gestione. Dato che il download della parte B è già in corso ma non è ancora completato, il punto di gestione indica a PCS1 di avviare il download della parte C dal punto di distribuzione.  

6. PCS2 completa il download della parte B e informa immediatamente il punto di gestione. Il punto di gestione istruisce indica a PCS2 di avviare immediatamente il download della parte D dal punto di distribuzione.  

7. PCS1 completa il download della parte C e informa immediatamente il punto di gestione. Il punto di gestione informa PCS1 che non ci sono altre parti da scaricare dal punto di distribuzione remoto e indica a questo client di scaricare la parte B dal peer locale, PCS2.  

8. Questo processo continua finché entrambe le origini di peer cache client non hanno scaricato tutte le parti l'una dall'altra. Il punto di gestione dà la priorità alle parti che devono essere scaricate dal punto di distribuzione remoto prima di indicare alle origini di peer cache di scaricare parti dal peer locale.  

9. Client3 è il primo ad aggiornare i criteri dopo la scadenza del periodo di fallback di 30 minuti. Questo client ora esegue un controllo presso il punto di gestione, che lo informa della presenza di nuove origini locali. Invece di scaricare completamente il contenuto dal punto di distribuzione attraverso la rete WAN, il client lo scarica interamente da una delle origini di peer cache client. I client danno la priorità alle origini peer locali. 

> [!Note]  
> Se il numero di origini di peer cache client è maggiore del numero delle parti del contenuto, il punto di gestione indica alle origini di peer cache aggiuntive di attendere il fallback come un client normale. 


### <a name="configure-partial-download"></a>Configurare il download parziale

1. Configurare [gruppi di limiti](../../servers/deploy/configure/boundary-groups.md) e origini di peer cache normalmente.  

2. Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Configurazione del sito** e selezionare **Siti**. Fare clic su **Impostazioni gerarchia** sulla barra multifunzione.  

3. Nella scheda **Generale** abilitare l'opzione per **configurare le origini di peer cache client per la suddivisione del contenuto in parti**.  

4. Creare una distribuzione richiesta con contenuto.  

   > [!Note]  
   > Questa funzionalità funziona solo se il client scarica il contenuto in background, ad esempio con una distribuzione richiesta. I download su richiesta, ad esempio quando l'utente installa una distribuzione disponibile in Software Center, si comportano come di consueto.  

Per visualizzarli durante la gestione del download del contenuto in parti, esaminare il file **ContentTransferManager.log** nell'origine di peer cache client e il file **MP_Location.log** nel punto di gestione.  



## <a name="guidance-for-cache-management"></a>Indicazioni per la gestione della cache
<!--510645-->
Per condividere il contenuto, la peer cache si basa sulla cache del client di Configuration Manager. Tenere in considerazione i punti seguenti per la gestione della cache del client nell'ambiente:  

- La cache del client di Configuration Manager non è simile alla raccolta contenuto in un punto di distribuzione. Durante la gestione del contenuto distribuito in un punto di distribuzione, il client di Configuration Manager gestisce automaticamente il contenuto presente nella propria cache. Sono disponibili impostazioni e metodi che consentono di controllare il tipo di contenuto presente nella cache di un'origine di peer cache. Per altre informazioni, vedere [Configurare la cache del client per i client di Configuration Manager](../../clients/manage/manage-clients.md#BKMK_ClientCache).  

- Alle origini di peer cache si applicano le impostazioni normali per dimensione della cache e manutenzione. Per altre informazioni, vedere [Configurare la dimensione della cache del client](../../clients/deploy/about-client-settings.md#configure-client-cache-size). Prendere in considerazione le dimensioni del contenuto più esteso, come i pacchetti di aggiornamento del sistema operativo o i file di aggiornamento rapido di Windows 10. Confrontare la necessità di tale contenuto con lo spazio su disco disponibile nelle origini di peer cache.  

- Il client di origine della peer cache aggiorna l'ora dell'ultimo riferimento del contenuto nella cache quando viene scaricato da un peer. Il client usa questo timestamp quando gestisce automaticamente la relativa cache, rimuovendo per primo il contenuto meno recente. Deve quindi attendere prima di rimuovere il contenuto che i client di peer cache scaricano con maggiore frequenza, se non addirittura evitare di rimuoverlo.  

- Se necessario, durante una sequenza di attività di distribuzione del sistema operativo usare la variabile **SMSTSPreserveContent** per mantenere il contenuto della cache del client. Per altre informazioni, vedere [Variabili della sequenza di attività](../../../osd/understand/task-sequence-variables.md#SMSTSPreserveContent).  

- Se necessario, durante la creazione del software seguente, usare l'opzione **Rendi permanente il contenuto nella cache client**:  
  - Applicazioni
  - Pacchetti
  - Immagini dei sistemi operativi
  - Pacchetti di aggiornamento del sistema operativo
  - Immagini d'avvio



## <a name="monitoring"></a>Monitoraggio   

Per capire come viene usata la peer cache, è possibile visualizzare il dashboard **Origini dati del client**. Per altre informazioni, vedere [Dashboard Origini dati del client](../../servers/deploy/configure/monitor-content-you-have-distributed.md#client-data-sources-dashboard).

Usare inoltre i report per visualizzare l'uso della peer cache. Nella console passare all'area di lavoro **Monitoraggio**, espandere **Report** e selezionare il nodo **Report**. Il tipo dei report seguenti è **Distribuzione software - Contenuto**:  

1.  **Rifiuto di contenuto di origine di peer cache**: frequenza con cui le origini di peer cache in un gruppo di limiti rifiutano una richiesta di contenuto.  

    > [!Note]  
    > **Problema noto**<!--486652-->: quando si esegue il drill-down in risultati come *MaxCPULoad* o *MaxDiskIO*, è possibile che venga visualizzato un errore per segnalare che non è possibile trovare il report o i dettagli. Per risolvere questo problema, usare gli altri due report che mostrano direttamente i risultati.  

2. **Peer cache source content rejection by condition** (Rifiuto di contenuto di origine di peer cache - per condizione): visualizza i dettagli relativi al rifiuto per un tipo di rifiuto o un gruppo di limiti specificato. 

    > [!Note]  
    > **Problema noto**<!--486652-->: non è possibile selezionare i parametri disponibili, ma è necessario immetterli manualmente. Immettere i valori relativi al *nome del gruppo di limiti* e al *tipo di rifiuto* indicati nel report **Rifiuto di contenuto di origine di peer cache**. Ad esempio, per *Rejection Type* (Tipo di rifiuto) è possibile immettere *MaxCPULoad* o *MaxDiskIO*.  

3. **Peer cache source content rejection details** (Rifiuto di contenuto di origine di peer cache - dettagli): visualizza le informazioni sul contenuto richiesto dal client al momento del rifiuto.  

    > [!Note]  
    > **Problema noto**<!--486652-->: non è possibile selezionare i parametri disponibili, ma è necessario immetterli manualmente. Immettere il valore per *Rejection Type* (Tipo di rifiuto) come visualizzato nel report **Rifiuto di contenuto di origine di peer cache**. Immettere quindi il valore per *ID risorsa* per l'origine contenuto sulla quale si vogliono più informazioni. 
    > 
    > Per trovare l'ID risorsa dell'origine di contenuto:  
    > 
    > 1. Trovare il nome del computer visualizzato come *Origine di peer cache* nei risultati del report **Rifiuto di contenuto di origine di peer cache per condizione**.  
    > 
    > 2. Passare all'area di lavoro **Asset e conformità**, selezionare il nodo **Dispositivi** e cercare il nome del computer. Usare il valore della colonna ID risorsa.  

