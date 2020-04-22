---
title: Technical Preview 1803
titleSuffix: Configuration Manager
description: Informazioni sulle nuove funzionalità disponibili in Configuration Manager Technical Preview versione 1803.
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 56dc4b07-5aa4-43e2-9be8-d26ae5ff5613
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: bb8224df3ccbb086ca0c83d08f29522cf3289c32
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701949"
---
# <a name="capabilities-in-technical-preview-1803-for-configuration-manager"></a>Funzionalità della versione Technical Preview 1803 per Configuration Manager

*Si applica a: Configuration Manager (Technical Preview Branch)*

Questo articolo presenta le funzionalità disponibili nella Technical Preview per Configuration Manager, versione 1803. È possibile installare questa versione per aggiornare il sito delle anteprime tecniche aggiungendovi nuove funzionalità. 

Prima di installare questo aggiornamento, vedere l'articolo [Technical Preview](technical-preview.md). L'articolo consente di acquisire familiarità con i requisiti e le limitazioni generali per l'uso di una Technical Preview, con l'aggiornamento tra le versioni e con l'invio di commenti e suggerimenti.     


<!--  Known Issues Template   
## Known Issues in this Technical Preview:
-   **Issue Name**. Details
    Workaround details.
-->


</br>

**Di seguito sono riportate le nuove funzionalità disponibili con questa versione.**  



 
## <a name="pull-distribution-points-support-cloud-distribution-points-as-source"></a>I punti di distribuzione pull supportano punti di distribuzione cloud come origine  
<!--1321554-->
Molti clienti usano [punti di distribuzione pull](../plan-design/hierarchy/use-a-pull-distribution-point.md) in uffici remoti o succursali per scaricare contenuto da un punto di distribuzione di origine attraverso la rete WAN. Se gli uffici remoti hanno una connessione Internet più efficiente, oppure se si vuole ridurre il carico sui collegamenti WAN, è ora possibile usare come origine un [punto di distribuzione cloud](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md) in Microsoft Azure. Quando si aggiunge un'origine nella scheda **Punto di distribuzione pull** delle proprietà dei punti di distribuzione, qualsiasi punto di distribuzione cloud nel sito viene elencato come punto di distribuzione disponibile. Il comportamento di entrambi i ruoli del sistema del sito rimane per altri versi invariato. 

### <a name="prerequisites"></a>Prerequisiti
- Per comunicare con Microsoft Azure, il punto di distribuzione pull richiede l'accesso a Internet.
- Il contenuto deve essere distribuito al punto di distribuzione cloud di origine.

> [!Note]  
> Questa funzionalità comporta l'addebito alla sottoscrizione di Azure per l'archiviazione dei dati e il traffico di rete in uscita. Per altre informazioni, vedere [Costo dell'uso della distribuzione basata sul cloud](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_cost).



## <a name="partial-download-support-in-client-peer-cache-to-reduce-wan-utilization"></a>Riduzione dell'utilizzo della rete WAN tramite supporto parziale del download nella peer cache del client
<!--1357346-->
Le origini delle peer cache dei client sono ora in grado di dividere il contenuto in parti, grazie alle quali è possibile ridurre al minimo il trasferimento in rete, riducendo l'utilizzo della rete WAN. Il punto di gestione consente una traccia più dettagliata delle parti del contenuto e tenta di eliminare più download dello stesso contenuto per ogni gruppo di limiti. 

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


### <a name="try-it-out"></a>Verifica
 Provare a completare le attività. Quindi inviare **Commenti e suggerimenti** dalla scheda **Home** della barra multifunzione.

1. Impostare [gruppi di limiti](../servers/deploy/configure/boundary-groups.md) e [origini di peer cache](../plan-design/hierarchy/client-peer-cache.md) normalmente.
2. Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Configurazione del sito** e selezionare **Siti**. Fare clic su **Impostazioni gerarchia** sulla barra multifunzione. 
3. Nella scheda **Generale** abilitare l'opzione per **configurare le origini di peer cache client per la suddivisione del contenuto in parti**. 
4. Creare una distribuzione richiesta con contenuto.  

   > [!Note]  
   > Questa funzionalità funziona solo se il client scarica il contenuto in background, ad esempio con una distribuzione richiesta. I download su richiesta, ad esempio quando l'utente installa una distribuzione disponibile in Software Center, si comportano come di consueto.  

1. Per visualizzarli durante la gestione del download del contenuto in parti, esaminare il file **ContentTransferManager.log** nell'origine di peer cache client e il file **MP_Location.log** nel punto di gestione.  
 



## <a name="maintenance-windows-in-software-center"></a>Finestre di manutenzione in Software Center
<!--1358131-->
Software Center ora visualizza la finestra di manutenzione pianificata successiva. Nella scheda Stato installazione cambiare la visualizzazione da Tutto a Upcoming (Prossima). Visualizza l'intervallo di tempo e l'elenco delle distribuzioni pianificate. L'elenco è vuoto se non ci sono finestre di manutenzione future. 

![Software Center con l'elenco delle distribuzioni future nella scheda Stato installazione](media/1358131-software-center-maintenance-windows.png)


## <a name="custom-tab-for-webpage-in-software-center"></a>Scheda personalizzata per pagine Web in Software Center
<!--1358132-->
È ora possibile creare una scheda personalizzata per aprire una pagina Web in Software Center. Questa funzionalità consente di visualizzare il contenuto per gli utenti finali in modo coerente e affidabile. L'elenco seguente include alcuni esempi:
- Contatta IT: informazioni su come contattare il reparto IT dell'organizzazione
- Centro assistenza IT: azioni self-service per l'IT, ad esempio la ricerca nella Knowledge Base o l'apertura di un ticket di supporto.
- Documentazione per l'utente finale: articoli per gli utenti dell'organizzazione su diversi argomenti IT, ad esempio l'uso delle applicazioni o l'aggiornamento a Windows 10.


### <a name="try-it-out"></a>Verifica
 Provare a completare le attività. Quindi inviare **Commenti e suggerimenti** dalla scheda **Home** della barra multifunzione.

1. Nel nodo **Impostazioni client** dell'area di lavoro **Amministrazione** della console di Configuration Manager aprire i criteri **Impostazioni client predefinite**.
2. Selezionare il gruppo **Software Center**.
3. Per **Impostazioni del Software Center** fare clic su **Personalizza**.
4. Passare alla scheda **Schede**.
5. Abilitare l'opzione per **specificare una scheda personalizzata per Software Center**.
    1. Immettere un nome nel campo di testo **Nome scheda**. Questo è il nome visualizzato per l'utente in Software Center.
    2. Immettere un URL valido nel campo di testo **URL del contenuto**. Questo URL costituisce il contenuto visualizzato da Software Center quando gli utenti fanno clic su questa scheda.

> [!Tip]  
> Per il rendering della pagina Web, Software Center usa componenti di Internet Explorer.

## <a name="enable-third-party-software-update-support-on-clients"></a>Abilitare il supporto dell'aggiornamento software di terze parti nei client

È ora possibile abilitare la configurazione dei client Configuration Manager per gli aggiornamenti software di terze parti. Quando si **abilitano gli aggiornamenti software di terze parti** per le proprietà del componente del punto di aggiornamento software, quest'ultimo scaricherà il certificato di firma usato da WSUS per gli aggiornamenti di terze parti. <!--1357605-->

Se si seleziona **Enable third party software updates** (Abilita aggiornamenti software di terze parti) nelle impostazioni client, avviene quanto segue: 
- Nel client vengono impostati i criteri 'Consenti aggiornamenti firmati da un percorso del servizio di aggiornamento Microsoft nella rete Intranet' 
- Il certificato di firma viene installato nell'archivio autori attendibili nel client. 

### <a name="try-it-out"></a>Verifica
 Provare a completare le attività. Quindi inviare **Commenti e suggerimenti** dalla scheda **Home** della barra multifunzione.

1. Nel sito di livello più alto nella gerarchia di Configuration Manager passare al nodo **Amministrazione**, espandere **Configurazione del sito** e quindi **Siti**.
2. Fare clic sul server del sito di livello più alto e selezionare **Configura componenti del sito** e quindi **Punto di aggiornamento software**.
3. Fare clic su **Third Party Updates** (Aggiornamenti di terze parti) e selezionare **Enable third party software updates** (Abilita aggiornamenti software di terze parti).
4. Aprire **Impostazioni client** e passare alle impostazioni per **Aggiornamenti software**.
5. Assicurarsi che l'opzione **Enable third party software updates** sia impostata su **Sì**.

## <a name="enable-copypaste-of-asset-details-from-monitoring-views"></a>Abilitare le operazioni di copia e incolla dei dettagli degli asset da visualizzazioni di monitoraggio
A seguito di [commenti e suggerimenti forniti in UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/20234866-allow-us-to-copy-information-out-of-the-asset-det), è ora possibile abilitare la funzionalità copia/incolla nel riquadro Dettagli asset nelle visualizzazioni di monitoraggio dello stato della distribuzione e dell'implementazione.  <!--1357552-->

## <a name="scap-extensions"></a>Estensioni SCAP
La versione non definitiva delle estensioni SCAP è disponibile nella cartella Cd.latest in SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi. Questa versione non definitiva delle estensioni SCAP può essere installata in qualsiasi versione attualmente supportata di Configuration Manager Current Branch e LTSB 1606.



## <a name="next-steps"></a>Passaggi successivi
Per informazioni sull'installazione o l'aggiornamento del ramo Technical Preview, vedere [Technical Preview per Configuration Manager](technical-preview.md).    
