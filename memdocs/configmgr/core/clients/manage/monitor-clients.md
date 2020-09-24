---
title: Monitorare i client
titleSuffix: Configuration Manager
description: Informazioni su come monitorare i client in Configuration Manager
ms.date: 09/15/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2c8f57cf-1968-48de-87fb-4897432ed6e0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8094db944a1430311f0c3bb8c94bc7043b12c5ae
ms.sourcegitcommit: cba06c182646cb6dceef304b35230bf728d5133e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/15/2020
ms.locfileid: "90574618"
---
# <a name="how-to-monitor-clients-in-configuration-manager"></a>Come monitorare i client in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Dopo aver installato il client Configuration Manager nei dispositivi Windows nel proprio sito, monitorarne l'integrità e l'attività nella console di Configuration Manager.  


## <a name="about-client-status"></a><a name="bkmk_about"></a> Informazioni sullo stato del client

Configuration Manager offre i seguenti tipi di informazioni come stato del client:  

- **Stato online del client**: il sito considera un dispositivo **online** se è connesso al relativo punto di gestione assegnato. Per indicare che è online, il client invia i messaggi di tipo ping al punto di gestione. Se il punto di gestione non riceve alcun messaggio per cinque minuti, il sito considera il client **offline**.  

- **Attività client**: il sito considera il client **attivo** se ha comunicato con Configuration Manager negli ultimi sette giorni. Il sito considera il client **inattivo** se non ha eseguito le azioni seguenti per sette giorni:  

    - Richiesta di aggiornamento dei criteri  
    - Invio di un messaggio di tipo heartbeat  
    - Invio dell'inventario hardware  

- **Controllo client**: stato della valutazione periodica eseguita sul dispositivo dal client Configuration Manager. La valutazione controlla il dispositivo e può correggere alcuni problemi rilevati. Per altre informazioni, vedere [Controlli dell'integrità dei client](#BKMK_ClientHealth).  

     Nei dispositivi che eseguono Windows 7 il controllo dei client viene eseguito come un'attività pianificata. Nelle versioni dei sistemi operativi successivi il controllo dei client viene eseguito automaticamente durante la manutenzione di Windows.  

     È possibile configurare la correzione in modo che venga eseguita su dispositivi specifici, ad esempio un server di rilevanza critica per l'azienda. Per valutare altri elementi, usare le impostazioni di conformità di Configuration Manager per monitorare altre configurazioni. Per altre informazioni sulle impostazioni di conformità, vedere [Pianificare e configurare le impostazioni di conformità](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md).  

- **Rimozione delle autorizzazioni eseguita**: il sito ha contrassegnato il record del dispositivo per l'eliminazione. Questo comportamento può verificarsi quando una nuova registrazione per lo stesso dispositivo lo assegna allo stesso sito primario di una gerarchia o a uno diverso. Il sito elimina questi dispositivi alla successiva esecuzione dell'attività di manutenzione del sito **Elimina dati di individuazione obsoleti**.<!-- SCCMDocs issue #1418 -->  

- **Obsoleto**: il sito ha individuato un nuovo record di dispositivo con lo stesso ID hardware, quindi contrassegna il record precedente come obsoleto. Nei report i record obsoleti dello stesso dispositivo non vengono conteggiati più volte. È tuttavia possibile assegnare criteri ai dispositivi obsoleti. Se il sito non riceve un heartbeat per un record obsoleto dopo 90 giorni di inattività, rimuove il dispositivo obsoleto quando esegue l'attività di manutenzione del sito **Elimina dati di individuazione client obsoleti**.


## <a name="monitor-individual-clients"></a><a name="bkmk_indStatus"></a> Monitorare i singoli client

1. Nella console di Configuration Manager passare all'area di lavoro **Asset e conformità**. Selezionare il nodo **Dispositivi** o scegliere una raccolta in **Raccolte dispositivi**.  

    Le icone all'inizio di ogni riga indicano lo stato online del dispositivo:  

    | Icona | Descrizione |
    | ---- | ----------- |  
    |![icona di stato online per i client](../../../core/clients/manage/media/online-status-icon.png)|Il dispositivo è online|  
    |![icona di stato offline per i client](../../../core/clients/manage/media/offline-status-icon.png)|Il dispositivo è offline|  
    |![icona di stato sconosciuto per i client](../../../core/clients/manage/media/unknown-status-icon.png)|Lo stato online è sconosciuto|  
    |![client non installato](../../../core/clients/manage/media/client-not-installed.png)|Il client non è installato nel dispositivo|  

2. Per ottenere uno stato online più dettagliato, aggiungere le informazioni sullo stato online del client alla visualizzazione del dispositivo. Fare clic con il pulsante destro del mouse sull'intestazione di colonna e scegliere i campi dello stato online da aggiungere:

    - **Stato online del dispositivo**: indica se il client è attualmente online o offline. Questo stato corrisponde alle informazioni fornite dalle icone.  

    - **Ora dell'ultimo stato online**: indica quando lo stato online del client è diventato online  

    - **Ora dell'ultimo stato offline** indica quando lo stato è diventato offline  

3. Selezionare un singolo client nel riquadro dell'elenco per visualizzare altre informazioni di stato nel riquadro dei dettagli. Queste informazioni includono l'attività del client e lo stato del controllo del client.  


## <a name="client-health-dashboard"></a><a name="bkmk_health"></a> Dashboard di integrità del client

<!--3599209-->
La distribuzione di aggiornamenti software e altre app per proteggere l'ambiente raggiunge solo i client integri. I client di Configuration Manager non integri hanno effetti negativi sulla conformità complessiva. Determinare lo stato del client può essere difficile e molto dipende dalla base di partenza, ovvero dal numero totale di dispositivi nell'ambito di gestione. Ad esempio, se si rilevano tutti i sistemi di Active Directory, anche se alcuni record provengono da computer ritirati, il processo aumenta la base di partenza.

Configuration Manager offre un dashboard con informazioni sull'integrità dei client nell'ambiente. Il dashboard consente di visualizzare l'integrità dei client, l'integrità dello scenario e gli errori più comuni. È possibile filtrare la visualizzazione per diversi attributi per visualizzare i potenziali problemi per versione del sistema operativo e client.

Nella console di Configuration Manager passare all'area di lavoro **Monitoraggio**. Espandere **Stato client** e selezionare il nodo **Dashboard sull'integrità del client**.

:::image type="content" source="media/3599209-client-health-dashboard.png" alt-text="Screenshot del dashboard sull'integrità del client" lightbox="media/3599209-client-health-dashboard.png":::

> [!Tip]  
> Nessuna modifica per ccmeval.  

Per impostazione predefinita, il dashboard sull'integrità del client mostra i client online e i client attivi negli ultimi tre giorni. Pertanto, in questo dashboard potrebbero essere visualizzati valori diversi rispetto ad altre fonti cronologiche di dati sull'integrità del client. Ad esempio, altri nodi in **Stato client** o i report nella categoria di stato client.

### <a name="filters"></a>Filtri

Nella parte superiore del dashboard è presente un set di filtri per modificare i dati visualizzati.

- **Integrità del client per i client nelle raccolte seguenti**: per impostazione predefinita, i dispositivi nel dashboard vengono visualizzati nella raccolta **Tutti i sistemi**. Selezionare una raccolta di dispositivi per limitare l'ambito della visualizzazione a un sottoinsieme di dispositivi in una raccolta specifica.  

- **Client attivi nel numero di giorni recenti indicato**: per impostazione predefinita, nel dashboard vengono visualizzati i client attivi negli ultimi tre giorni.  

- **Includi l'integrità del client per i client offline**: per impostazione predefinita, nel dashboard vengono visualizzati solo i client online. Questo stato deriva dal canale di notifica client che aggiorna lo stato del client ogni cinque minuti. Per altre informazioni, vedere [Informazioni sullo stato del client](monitor-clients.md#bkmk_about).  

- **Mostra i dettagli solo dei client non integri**: consente di limitare la visualizzazione solo ai dispositivi che segnalano un errore di integrità del client.  

    > [!Tip]  
    > Usare questo filtro con i riquadri della versione del client e del sistema operativo. Per altre informazioni, vedere [Riquadri versione](#version-tiles).

### <a name="overall-client-health"></a>Integrità complessiva del client

Questo riquadro illustra l'integrità complessiva dei client nella gerarchia.

Un client di Configuration Manager integro presenta le proprietà seguenti:

- Online  
- Invia attivamente dati  
- Esegue tutti i controlli di valutazione dell'integrità del client  

Per altre informazioni, vedere [Informazioni sullo stato del client](monitor-clients.md#bkmk_about).

Un client integro comunica correttamente con il sito. Segnala tutti i dati in base alle pianificazioni definite nelle impostazioni del client.

Selezionare un segmento del grafico per eseguire il drill-down a un elenco di dispositivi.

### <a name="version-tiles"></a>Riquadri di versione

Sono presenti due riquadri che illustrano lo stato del client in base alla versione del client di Configuration Manager e alla versione del sistema operativo. Questi riquadri sono utili quando si apportano modifiche ai filtri, ad esempio a **Failure only** (Solo errore). Consentono di stabilire se un problema ricorre in modo costante in una versione specifica. Usare queste informazioni per prendere in considerazione eventuali aggiornamenti.

Selezionare un segmento dei grafici per eseguire il drill-down a un elenco di dispositivi.

### <a name="scenario-health"></a>Integrità dello scenario

Questo grafico a barre illustra l'integrità complessiva degli scenari principali seguenti:

- Criteri client
- Individuazione heartbeat
- Inventario hardware
- Inventario software
- Messaggi di stato

Usare i selettori per evidenziare scenari specifici nel grafico.

Le due barre seguenti vengono sempre visualizzate:

- **Combinati (tutti)** : la combinazione di tutti gli scenari (AND)  
- **Combinati (qualsiasi)** : almeno uno degli scenari (OR)

> [!Tip]  
> L'integrità di uno scenario non viene misurato dalla configurazione delle impostazioni del client. Questi valori possono variare in base al set di criteri risultante per ogni dispositivo. Usare la procedura seguente per modificare i periodi di valutazione per l'integrità degli scenari:
>
> - Nella console di Configuration Manager passare all'area di lavoro **Monitoraggio** e selezionare il nodo **Stato client**.  
> - Nella barra multifunzione selezionare **Impostazioni stato client**.  
>
> Per impostazione predefinita, se un client non invia i dati specifici dello scenario entro **7 giorni**, Configuration Manager lo considera non integro per lo scenario.

### <a name="top-10-client-health-failures"></a>10 errori principali di Integrità del client

Questo grafico elenca gli errori più comuni nell'ambiente in uso. Questi errori provengono da Windows o da Configuration Manager.

<!-- The following list includes some of the more common failures overall:

#### Failure 1 title
Failure 1 description

Solution for failure 1 -->


## <a name="monitor-the-status-of-all-clients"></a><a name="bkmk_allStatus"></a> Monitorare lo stato di tutti i client

1. Nella console di Configuration Manager passare all'area di lavoro **Monitoraggio** e selezionare il nodo **Stato client**. Esaminare le statistiche generali per l'attività client e i controlli client nell'intero sito. Modificare l'ambito delle informazioni scegliendo una raccolta diversa.  

2. Per eseguire il drill-down delle statistiche segnalate, scegliere il nome delle informazioni segnalate. Ad esempio, **Client attivi che hanno superato il controllo o con nessun risultato**. Esaminare quindi le informazioni sui singoli client.  

3. Selezionare **Attività client** per visualizzare grafici che illustrano l'attività del client nel sito di Configuration Manager.  

4. Selezionare **Controllo client** per visualizzare grafici che illustrano lo stato dei controlli client nel sito di Configuration Manager.  

    Configurare avvisi per ricevere una notifica quando i risultati dei controlli client o l'attività client scende al di sotto di una percentuale specificata. Il sito può generare un avviso anche quando la correzione non riesce su una percentuale di client specificata. Per altre informazioni, vedere [Come configurare lo stato del client](../deploy/configure-client-status.md).  


## <a name="client-health-checks"></a><a name="BKMK_ClientHealth"></a> Controlli di integrità dei client

Il controllo dei client esegue i controlli e le correzioni seguenti:  

|Controllo client|Azione di correzione|Ulteriori informazioni|  
|------------------|------------------------|----------------------|  
|Verificare che il controllo client sia stato eseguito di recente|Esecuzione del controllo client|Verifica che il controllo client sia eseguito almeno una volta negli ultimi tre giorni.|  
|Verificare che siano installati i prerequisiti client|Installazione dei prerequisiti client|Verifica che siano installati i prerequisiti client. Legge il file ccmsetup.xml nella cartella di installazione client per individuare i prerequisiti.|  
|Verifica di integrità del repository WMI|Reinstallare il client di Configuration Manager|Verifica che le voci client di Configuration Manager siano presenti in WMI.|  
|Verificare che sia in esecuzione il servizio client|Avvio del servizio client (host agenti di SMS)|Nessuna informazione aggiuntiva|  
|Verifica del sink di evento WMI.|Riavvio del servizio client|Verificare se il relativo sink di evento WMI di Configuration Manager è stato perso|  
|Verificare che sia presente il servizio Strumentazione gestione Windows (WMI)|Nessuna correzione|Nessuna informazione aggiuntiva|  
|Verificare che il client sia stato installato correttamente|Reinstallazione del client|Nessuna informazione aggiuntiva|  
|Verificare che il tipo di avvio del servizio antimalware sia automatico|Reimpostare il tipo di avvio del servizio su automatico|Nessuna informazione aggiuntiva|  
|Verificare che sia in esecuzione il servizio antimalware|Avvio del servizio antimalware|Nessuna informazione aggiuntiva|  
|Verificare che il tipo di avvio del servizio Windows Update sia automatico o manuale|Reimpostare il tipo di avvio del servizio su automatico|Nessuna informazione aggiuntiva|  
|Verificare che il tipo di avvio del servizio client (host agenti SMS) sia automatico|Reimpostare il tipo di avvio del servizio su automatico|Nessuna informazione aggiuntiva|  
|Verificare che sia in esecuzione il servizio Strumentazione gestione Windows (WMI).|Avvio del servizio Strumentazione gestione Windows|Nessuna informazione aggiuntiva|  
|Verificare che il database Microsoft SQL CE sia integro|Reinstallare il client di Configuration Manager|Nessuna informazione aggiuntiva|  
|Verifica di integrità di Microsoft Policy Platform WMI|Ripristinare Microsoft Policy Platform|Nessuna informazione aggiuntiva|  
|Verificare che il servizio Microsoft Policy Platform esista|Ripristinare Microsoft Policy Platform|Nessuna informazione aggiuntiva|  
|Verificare che il tipo di avvio del servizio Microsoft Policy Platform sia manuale|Reimpostare il tipo di avvio del servizio su manuale|Nessuna informazione aggiuntiva|  
|Verificare che sia presente il Servizio trasferimento intelligente in background|Nessuna correzione|Nessuna informazione aggiuntiva|  
|Verificare che il tipo di avvio del Servizio trasferimento intelligente in background sia automatico o manuale|Reimpostare il tipo di avvio del servizio su automatico|Nessuna informazione aggiuntiva|  
|Verificare che il tipo di avvio del servizio controllo di rete sia manuale|Reimpostare il tipo di avvio del servizio su manuale se installato|Nessuna informazione aggiuntiva|  
|Verificare che il tipo di avvio del servizio Strumentazione gestione Windows (WMI) sia automatico|Reimpostare il tipo di avvio del servizio su automatico|Nessuna informazione aggiuntiva|  
|Verificare che il tipo di avvio del servizio Windows Update nei dispositivi Windows 8 sia automatico o manuale|Reimpostare il tipo di avvio del servizio su manuale|Nessuna informazione aggiuntiva|  
|Verificare che esista il servizio client (Host agenti di SMS).|Nessuna correzione|Nessuna informazione aggiuntiva|  
|Verificare che il tipo di avvio del servizio Controllo remoto di Configuration Manager sia automatico o manuale|Reimpostare il tipo di avvio del servizio su automatico|Nessuna informazione aggiuntiva|  
|Verificare che il servizio Controllo remoto di Configuration Manager sia in esecuzione|Avviare il servizio di controllo remoto|Nessuna informazione aggiuntiva|  
|Verificare che sia in esecuzione il servizio proxy di riattivazione (Proxy di riattivazione di Configuration Manager)|Avviare il servizio Proxy di riattivazione di Configuration Manager|Questa verifica del client viene eseguita solo se l'impostazione **Risparmio energia**: **Abilitare il proxy di riattivazione** del client è impostata su **Sì** nei sistemi operativi client supportati.|  
|Verificare che il tipo di avvio del servizio proxy di riattivazione (Proxy di riattivazione di Configuration Manager) sia automatico|Reimpostare il tipo di avvio del servizio Proxy di riattivazione di Configuration Manager su automatico|Questa verifica del client viene eseguita solo se l'impostazione **Risparmio energia**: **Abilitare il proxy di riattivazione** del client è impostata su **Sì** nei sistemi operativi client supportati.|  


<!-- 
5/31/2019 ACz: need to confirm if these checks are still applicable
|WMI repository read and write test|Reset the WMI repository and reinstall the Configuration Manager client|Remediation of this client check is only performed on devices that run Windows Server 2003, Windows XP (64-bit) or earlier versions.|  
|Verify that the client WMI provider is healthy|Restart the Windows Management Instrumentation service|Remediation of this client check is only performed on devices that run Windows Server 2003, Windows XP (64-bit) or earlier.|  
 -->


## <a name="client-deployment-log-files"></a>File di log distribuzione client

Per altre informazioni sui file di log usati dalle operazioni di distribuzione e gestione client, vedere [File di log](../../plan-design/hierarchy/log-files.md#BKMK_ClientLogs).
