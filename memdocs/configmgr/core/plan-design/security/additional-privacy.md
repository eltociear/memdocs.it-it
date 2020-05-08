---
title: Informazioni aggiuntive sulla privacy
titleSuffix: Configuration Manager
description: Informazioni su come Microsoft raccoglie e usa i dati da Configuration Manager.
ms.date: 09/04/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1fcc921f-085f-4b0b-9c53-1e0707211076
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f877de32c9915f91d1e2d7f2d90b9b40ab69df11
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906581"
---
# <a name="additional-information-about-privacy-for-configuration-manager"></a>Altre informazioni sulla privacy per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*


## <a name="updates-and-servicing"></a>Aggiornamenti e manutenzione

Configuration Manager usa un modello di aggiornamento che consente di mantenere aggiornato l'ambiente con gli aggiornamenti e le funzionalità più recenti. Questa funzionalità usa un ruolo del sistema del sito chiamato punto di connessione del servizio. Si sceglie il server in cui installare questo ruolo. 

Per altre informazioni sui dati raccolti e su come vengono usati, vedere [Dati di utilizzo](#usage-data).



## <a name="usage-data"></a>Dati di utilizzo

Configuration Manager raccoglie dati di utilizzo e di diagnostica su se stesso, che Microsoft usa per migliorare l'esperienza, la qualità e la sicurezza di installazione delle versioni future.
I dati di utilizzo e di diagnostica sono abilitati per ogni gerarchia di Configuration Manager. Essi consistono in query di SQL Server eseguite su base settimanale in ogni sito primario e nel sito di amministrazione centrale. Quando la gerarchia usa un sito di amministrazione centrale, i dati dai siti primari vengono quindi replicati in tale sito. Nel sito di livello superiore della gerarchia, il punto di connessione del servizio invia queste informazioni quando verifica la presenza di aggiornamenti. Se il punto di connessione del servizio è in modalità offline, le informazioni vengono trasferite tramite lo strumento di connessione del servizio.

Configuration Manager raccoglie i dati solo dal database di SQL Server del sito e non direttamente dai client o dai server del sito.

Gli amministratori possono modificare il livello dei dati raccolti andando alla sezione **Dati di utilizzo** della console di Configuration Manager.

Per altre informazioni sui livelli e sulle impostazioni dei dati di utilizzo, vedere [Dati di diagnostica e di utilizzo](../diagnostics/diagnostics-and-usage-data.md).



## <a name="log-analytics-connector"></a>Connettore Log Analytics

Il connettore Log Analytics sincronizzazione i dati, ad esempio le raccolte, da Configuration Manager al servizio cloud di Azure. L'ID sottoscrizione e la chiave privata di Azure vengono memorizzati nel database di Configuration Manager quando l'amministratore configura la funzionalità. Sia la chiave privata del client di Azure Active Directory che la chiave condivisa dell'area di lavoro di Azure vengono archiviate nel database di Configuration Manager in locale. Tutte le comunicazioni tra Configuration Manager e Azure usano HTTPS. A Microsoft non vengono fornite informazioni aggiuntive sulle raccolte, a parte dati di diagnostica e utilizzo casuali. 

Per altre informazioni sui dati raccolti da Log Analytics, vedere [Sicurezza dei dati di Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-security).



## <a name="asset-intelligence"></a>Asset Intelligence

Asset Intelligence consente agli amministratori di definire, tenere traccia e gestire in modo proattivo la conformità agli standard di configurazione. Il controllo e i report sulla distribuzione e l'utilizzo di applicazioni fisiche e virtuali consentono alle organizzazioni di prendere decisioni aziendali più efficaci relativamente alle licenze software, nonché di garantire la conformità rispetto ai contratti di licenza. Dopo aver raccolto i dati sull'utilizzo dai client di Configuration Manager, è possibile usare diverse funzionalità per visualizzare tali dati, ad esempio le raccolte, le query e i report.

Durante ogni sincronizzazione, viene scaricato un catalogo di software conosciuti dal sito Microsoft. È possibile scegliere di inviare a Microsoft le informazioni relative ai titoli di software senza categoria rilevati nell'organizzazione, al fine di cercarli e aggiungerli al catalogo. Prima di caricare queste informazioni, viene visualizzata una finestra di dialogo in cui sono mostrati i dati che si stanno per caricare. Non è possibile annullare il caricamento dei dati selezionati. Asset Intelligence non invia a Microsoft informazioni su utenti e computer o sull'utilizzo delle licenze.

Una volta caricato un titolo di software, i ricercatori Microsoft identificano, classificano e rendono le informazioni disponibili a tutti gli altri clienti che usano la funzionalità e a tutti gli utenti del catalogo. Tutti i titoli di software caricati diventano pubblici. Le informazioni su una determinata applicazione e la relativa classificazione diventano parte del catalogo e possono essere scaricate dagli altri utenti del catalogo. Prima di configurare la raccolta dei dati di Asset Intelligence e decidere se inviare informazioni a Microsoft, prendere in considerazione i requisiti sulla privacy della propria organizzazione.

Asset Intelligence non è abilitato in Configuration Manager per impostazione predefinita. Il caricamento dei titoli senza categoria non avviene mai automaticamente e il sistema non è progettato per l'automazione di questa attività. È necessario selezionare manualmente e approvare il caricamento di ogni titolo di software.



## <a name="endpoint-protection"></a>Endpoint Protection

Microsoft Cloud Protection Service era precedentemente conosciuto come Microsoft Active Protection Service o MAPS.

I prodotti applicabili sono System Center Endpoint Protection e la funzionalità Endpoint Protection di Configuration Manager (per la gestione di System Center Endpoint Protection e Windows Defender per Windows 10). Questa funzionalità non è implementata né per System Center Endpoint Protection per Linux né per System Center Endpoint Protection per Mac.

La community antimalware Microsoft Cloud Protection Service è una community antimalware online diffusa in tutto il mondo che comprende gli utenti di System Center Endpoint Protection. Se un utente entra a far parte di Microsoft Cloud Protection Service, System Center Endpoint Protection invierà automaticamente informazioni a Microsoft per consentire di individuare il software da analizzare alla ricerca di potenziali minacce e per migliorare l'efficacia di System Center Endpoint Protection. Questa community contribuisce ad arrestare la diffusione di nuove infezioni causate da software dannoso. Se un report di Microsoft Cloud Protection Service include informazioni su malware o software potenzialmente dannoso che il client di Endpoint Protection potrebbe rimuovere, Microsoft Cloud Protection Service esegue il download della firma più recente per risolvere il problema. Microsoft Cloud Protection Service può anche trovare i "falsi positivi" e correggerli. I falsi positivi sono elementi in origine identificati erroneamente come malware. 

Le segnalazioni di Microsoft Cloud Protection Service includono dati relativi a potenziali file di malware, come i nomi dei file, l'hash crittografico, il fornitore, le dimensioni e gli indicatori di data. Microsoft Cloud Protection Service potrebbe inoltre raccogliere gli URL completi per indicare l'origine del file. Questi URL possono occasionalmente includere informazioni personali come termini di ricerca o dati immessi nei moduli. I report possono inoltre includere le azioni che sono state eseguite quando Endpoint Protection ha notificato software indesiderato. I report di Microsoft Cloud Protection Service includono queste informazioni per consentire a Microsoft di valutare l'efficacia di Endpoint Protection nel rilevare e rimuovere il malware e il software potenzialmente indesiderato e per tentare di identificare nuovo malware.

È possibile entrare a far parte di Microsoft Cloud Protection Service se si dispone di un'iscrizione base o avanzata. I report dei membri con iscrizione base includono le informazioni descritte in precedenza. I report dei membri con iscrizione avanzata sono più dettagliati e offrono altre informazioni relative al software rilevato da Endpoint Protection, come la posizione del software, i nomi file, le modalità di funzionamento del software e i suoi effetti sul computer. Tali report e quelli di altri utenti di Endpoint Protection che partecipano a Microsoft Cloud Protection Service aiutano i ricercatori Microsoft a scoprire più rapidamente le nuove minacce. Successivamente vengono create le definizioni dei malware per i programmi che soddisfano i criteri di analisi; le definizioni aggiornate sono messe a disposizione di tutti gli utenti attraverso Microsoft Update.

Per consentire di individuare e correggere alcuni tipi di infezioni malware, il prodotto invia regolarmente a Microsoft Cloud Protection Service informazioni sullo stato di protezione del PC. Queste informazioni includono indicazioni sulle impostazioni di protezione del PC e i file di log che descrivono i driver e altro software che viene caricato all'avvio del PC.

Viene inoltre inviato un numero che identifica in modo univoco il PC. Microsoft Cloud Protection Service può anche raccogliere gli indirizzi IP a cui i potenziali file malware si connettono.

I report Microsoft Cloud Protection Service vengono utilizzati per migliorare il software e i servizi Microsoft. Potrebbero essere usati anche per fini statistici, analitici o a scopo di prova e per generare definizioni. Solo i dipendenti, i collaboratori, i partner e i fornitori di Microsoft che abbiano una necessità commerciale di usare i report vi possono accedere.

Microsoft Cloud Protection Service non raccoglie intenzionalmente informazioni personali. Eventuali informazioni personali raccolte da Microsoft Cloud Protection Service non verranno utilizzate da Microsoft per identificare o contattare l'utente.

Per altre informazioni, vedere [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md).



## <a name="site-hierarchy--geographical-view-with-bing-maps"></a>Gerarchia dei siti: visualizzazione geografica con Bing Maps

Nella console di Configuration Manager andare all'area di lavoro **Monitoraggio**, selezionare il nodo **Gerarchia siti** e passare a **Vista geografica**. Questa vista consente di usare le mappe fornite da Microsoft Bing Maps per visualizzare la topologia dei server fisici di Configuration Manager. Per abilitare questa funzionalità, le informazioni sulla posizione fornite dall'utente vengono inviate dal server al servizio Web di Bing Maps.

Microsoft usa le informazioni per il funzionamento e il miglioramento delle mappe di Microsoft Bing Maps e di altri siti e servizi Microsoft. Per altre informazioni, vedere l'[Informativa sulla privacy Microsoft](https://privacy.microsoft.com/privacystatement).

È possibile scegliere di non usare la visualizzazione geografica per la gerarchia dei siti. La vista Diagramma gerarchia predefinita consente di visualizzare la gerarchia e non usa il servizio Bing Maps.
