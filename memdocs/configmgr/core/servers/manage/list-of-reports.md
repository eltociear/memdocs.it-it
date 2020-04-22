---
title: Elenco dei report
titleSuffix: Configuration Manager
description: Esaminare l'elenco dei report inclusi in Configuration Manager. I report vengono visualizzati in diverse categorie.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b7332ed3-8003-454b-bb12-1fdf8721425c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 49fe5b5b94b29d93d29108660e2b76db2f87ddf9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694489"
---
# <a name="list-of-reports-in-configuration-manager"></a>Elenco dei report di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Configuration Manager offre molti report predefiniti relativi a molte delle attività di report che si possono eseguire. È anche possibile usare le istruzioni SQL in questi report che consentono di scrivere propri report.   

I report seguenti sono disponibili in Configuration Manager. I report vengono visualizzati in diverse categorie.  



## <a name="administrative-security"></a>Protezione amministrativa  

I sei report seguenti sono elencati nella categoria **Protezione amministrativa**.  

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Registro attività di amministrazione**|Visualizza un record delle modifiche amministrative apportate per utenti amministratori, ruoli di sicurezza, ambiti di protezione e raccolte.|  
|**Assegnazioni di protezione utenti amministratori**|Visualizza gli utenti amministratori, i ruoli di sicurezza associati e gli ambiti di protezione associati a ogni ruolo di sicurezza per ogni utente.|  
|**Oggetti protetti da un unico ambito di protezione**|Visualizza gli oggetti che un amministratore ha assegnato solo all'ambito di protezione specificato. Questo report non visualizza gli oggetti che un amministratore associa a più di un ambito di protezione.|  
|**Protezione per oggetti specifici o multipli di Configuration Manager**|Visualizza gli oggetti a protezione diretta, gli ambiti di protezione associati agli oggetti e quali utenti amministratori dispongono dei diritti per gli oggetti.|  
|**Riepilogo ruoli di sicurezza**|Visualizza i ruoli di sicurezza e gli amministratori di Configuration Manager associati a ogni ruolo.|  
|**Riepilogo ambiti di protezione**|Visualizza gli ambiti di protezione e gli utenti amministratori e i gruppi di sicurezza di Configuration Manager associati a ogni ambito.|  



## <a name="alerts"></a>Avvisi  

I due report seguenti sono elencati nella categoria **Avvisi**.  

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Scorecard avvisi**|Visualizza un riepilogo di tutti gli avvisi posticipati generati tra la data di inizio e la data di fine specificate.|  
|**Avvisi generati più frequentemente**|Visualizza un riepilogo degli avvisi generati più frequentemente dalla data corrente alla data passata specificata per l'area funzionale fornita.|  



## <a name="asset-intelligence"></a>Asset Intelligence  

I 67 report seguenti sono elencati nella categoria **Asset Intelligence**.  

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Hardware 01A - Riepilogo dei computer in una raccolta specifica**|Visualizza un riepilogo di Asset Intelligence dei computer in una raccolta specificata.|  
|**Hardware 03A - Utenti computer primario**|Visualizza gli utenti e il numero di computer in cui sono utenti primari.|  
|**Hardware 03B - Computer per un utente console primario specifico**|Visualizza tutti i computer per cui l'utente specificato è l'utente console primario.|  
|**Hardware 04A - Computer con più utenti (condivisi)**|Visualizza i computer che non hanno un utente primario in quanto nessun utente dispone di una percentuale di tempo di accesso superiore a 66%.|  
|**Hardware 05A - Utenti console in un computer specifico**|Visualizza tutti gli utenti console in un computer specifico.|  
|**Hardware 06A - Computer per cui non è possibile determinare gli utenti console**|Consente agli utenti amministratori di identificare i computer in cui è necessario attivare la registrazione di protezione.|  
|**Hardware 07A - Dispositivi USB per produttore**|Visualizza i dispositivi USB raggruppati in base al produttore.|  
|**Hardware 07B - Dispositivi USB per produttore e descrizione**|Visualizza i dispositivi USB raggruppati in base al produttore e alla descrizione.|  
|**Hardware 07C - Computer con un dispositivo USB specifico**|Visualizza tutti i computer con un dispositivo USB specifico.|  
|**Hardware 07D - Dispositivi USB in un computer specifico**|Visualizza tutti i dispositivi USB in un computer specifico.|  
|**Hardware 08A - Hardware che non è pronto per un aggiornamento software**|Visualizza l'hardware che non soddisfa i requisiti hardware minimi.|  
|**Hardware 09A - Ricerca di computer**|Visualizza un riepilogo dei computer che corrispondono ai filtri in base a parole chiave. I filtri sono: nome del computer, sito di Configuration Manager, dominio, utente console principale, sistema operativo, produttore o modello.|  
|**Hardware 10A - Computer in una raccolta specifica che sono stati modificati durante un intervallo di tempo specifico**|Visualizza un elenco di computer in una raccolta specifica in cui una classe hardware è stata modificata durante un intervallo di tempo specifico.|  
|**Hardware 10B - Modifiche in un computer specifico in un intervallo di tempo specifico**|Visualizza le classi che sono state modificate in un computer specifico in un intervallo di tempo specifico.|  
|**Licenza 01A - Ledger Microsoft Volume License per resoconti delle licenze Microsoft**|Visualizza un inventario dei nomi di tutti i software Microsoft disponibili nel programma Microsoft Volume Licensing.|  
|**Licenza 01B - Elemento ledger Microsoft Volume License per canale di vendita**|Identifica i canali di vendita per il software Microsoft Volume License in inventario.|  
|**Licenza 01C - Computer con specifici oggetti e canali di vendita del Ledger Microsoft Volume License**|Identifica e visualizza i computer che dispongono di un elemento specifico dal Ledger Microsoft Volume License.|  
|**Licenza 01D - Prodotti Ledger Microsoft Volume License in un computer specifico**|Identifica e visualizza tutti gli elementi Ledger Microsoft Volume License in un computer specifico.|  
|**Licenza 02A - Conteggio delle licenze prossime alla scadenza per intervalli di tempo**|Visualizza il numero di licenze prossime alla scadenza per un intervallo di tempo specificato. Le licenze dei prodotti visualizzati sono gestite dal Servizio gestione licenze software.|  
|**Licenza 02B - Computer con licenze prossime alla scadenza**|Visualizza i computer specificati con le licenze prossime alla scadenza.|  
|**Licenza 02C - Informazioni sulla licenza in un computer specifico**|Visualizza i prodotti in un computer specifico che hanno le licenze gestite dal Servizio gestione licenze software.|  
|**Licenza 03A - Conteggio delle licenze per stato della licenza**|Visualizza i prodotti, per stato della licenza, che hanno le licenze gestite dal Servizio gestione licenze software.|  
|**Licenza 03B - Computer con uno stato licenza specifico**|Visualizza i prodotti, con uno stato della licenza specifico, che hanno le licenze gestite dal Servizio gestione licenze software.|  
|**Licenza 04A - Conteggio dei prodotti gestiti dalla gestione licenze software**|Visualizza il conteggio dei prodotti che hanno le licenze gestite dal Servizio gestione licenze software.|  
|**Licenza 04B - Computer con un prodotto specifico gestito dal Servizio gestione licenze software**|Visualizza i computer gestiti dal Servizio gestione licenze software che contengono un prodotto specifico.|  
|**Licenza 05A - Computer che forniscono il Servizio di gestione delle chiavi**|Visualizza i computer che agiscono come Server di gestione delle chiavi.|  
|**Licenza 06A - Numero di processori per prodotti con licenza per processore**|Visualizza il numero di processori nei computer che usano i prodotti Microsoft che supportano la gestione licenze per processore.|  
|**Licenza 06B - Computer con un prodotto specifico che supporta le licenze per processore**|Visualizza un elenco di computer in cui è installato un prodotto Microsoft specifico che supporta la gestione licenze per processore.|  
|**Licenza 14A - Report di riconciliazione di Microsoft Volume Licensing**|Visualizza la riconciliazione sulle licenze software ottenute tramite il contratto Microsoft Volume License e il numero corrente in inventario.|  
|**Licenza 14B - Elenco dell'inventario software Microsoft non trovato in MVLS**|Questo report visualizza i titoli del software Microsoft in uso che non sono stati trovati nel contratto Microsoft Volume License.|  
|**Licenza 15A - Report di riconciliazione licenza generale**|Visualizza la riconciliazione sulle licenze software generali ottenute e il numero corrente in inventario.|  
|**Licenza 15B - Report di riconciliazione licenza generale per computer**|Visualizza i computer in cui è installato il prodotto concesso in licenza con una versione specifica.|  
|**Software 01A - Riepilogo del software installato in una raccolta specifica**|Visualizza un riepilogo del software installato ordinato per numero di istanze trovate nell'inventario.|  
|**Software 02A - Famiglie di prodotti per una raccolta specifica**|Visualizza le famiglie di prodotti e il conteggio del software nella famiglia per una raccolta specifica.|  
|**Software 02B - Categorie di prodotti per una famiglia di prodotti specifica**|Visualizza le categorie di prodotti di una famiglia di prodotti specifica e il conteggio del software della categoria.|  
|**Software 02C - Software in una famiglia e categoria di prodotti specifica**|Visualizza tutto il software presente nella categoria e nella famiglia di prodotti specificate.|  
|**Software 02D - Computer con software specifico installato**|Visualizza tutti i computer con un software specifico installato.|  
|**Software 02E - Software installati in un computer specifico**|Visualizza tutto il software installato in un computer specifico.|  
|**Software 03A - Software senza categoria**|Visualizzare il software categorizzato come sconosciuto o senza categoria.|  
|**Software 04A - Software configurato per l'esecuzione automatica nei computer**|Visualizza un elenco di software configurati per l'esecuzione automatica nei computer.|  
|**Software 04B - Computer con software specifico configurato per l'esecuzione automatica**|Visualizza tutti i computer con software specifico configurato per l'esecuzione automatica.|  
|**Software 04C - Software configurato per l'esecuzione automatica in un computer specifico**|Visualizza il software installato e configurato per l'esecuzione automatica in un computer specifico.|  
|**Software 05A - Oggetti browser helper**|Visualizza gli oggetti browser helper installati nei computer in una raccolta specifica.|  
|**Software 05B - Computer con un oggetto browser helper specifico**|Visualizza tutti i computer con un oggetto browser helper specifico.|  
|**Software 05C - Oggetti browser helper installati in un computer specifico**|Visualizza tutti gli oggetti browser helper installati in un computer specifico.|  
|**Software 06A - Ricerca di software installato**|Questo report offre un riepilogo del software installato. Esegue la ricerca in base ai criteri seguenti: nome del prodotto, editore o versione.|  
|**Software 06B - Software per nome prodotto**|Visualizza un riepilogo del software installato in base a un nome di prodotto specifico.|  
|**Software 07A - Programmi eseguibili usati di recente per numero di computer**|Visualizza i programmi eseguibili usati di recente. Contiene inoltre il numero di computer in cui gli utenti hanno usato il programma. Il controllo software deve essere abilitato per questo sito per poter visualizzare il report.|  
|**Software 07B - Computer che hanno usato di recente un programma eseguibile specifico**|Visualizza i computer nei quali gli utenti hanno usato di recente un programma eseguibile specifico. Questo report richiede l'abilitazione dell'impostazione client relativa alla misurazione del software.|  
|**Software 07C - Programmi eseguibili usati di recente in un computer specifico**|Visualizza i file eseguibili usati di recente in un computer specifico. Questo report richiede l'abilitazione dell'impostazione client relativa alla misurazione del software.|  
|**Software 08A - Programmi eseguibili usati di recente per numero di utenti**|Visualizza i programmi eseguibili usati di recente. Include inoltre il numero di utenti che hanno usato il programma più di recente. Questo report richiede l'abilitazione dell'impostazione client relativa alla misurazione del software.|  
|**Software 08B - Utenti che hanno usato di recente un programma eseguibile specifico**|Visualizza gli utenti che hanno usato più di recente un programma eseguibile specificato. Questo report richiede l'abilitazione dell'impostazione client relativa alla misurazione del software.|  
|**Software 08C - Programmi eseguibili usati di recente da un utente specifico**|Visualizza i programmi eseguibili che l'utente specificato ha usato di recente. Questo report richiede l'abilitazione dell'impostazione client relativa alla misurazione del software.|  
|**Software 09A - Software usato raramente**|Visualizza i titoli software che gli utenti non hanno usato durante un periodo di tempo specifico.|  
|**Software 09B - Computer con software installato usato raramente**|Visualizza i computer con software installato che gli utenti non hanno usato per un periodo di tempo specifico. Il periodo di tempo specifico è basato sul valore specificato nel report "Software 09A - Software usato raramente".|  
|**Software 10A - Titoli software con più etichette personalizzate specifiche definite**|Visualizza i titoli software in base alla corrispondenza di tutti i criteri etichetta personalizzata specificati. È possibile selezionare fino a tre etichette personalizzate per perfezionare la ricerca di titoli software.|  
|**Software 10B - Computer in cui è installato il titolo software con l'etichetta personalizzata specificata**|Visualizza tutti i computer nella raccolta in cui è installato il titolo software con l'etichetta personalizzata specificata.|  
|**Software 11A - Titoli software con un'etichetta personalizzata specifica definita**|Visualizza i titoli software in base alla corrispondenza di almeno uno dei criteri etichetta personalizzata specificati.|  
|**Software 12A - Titoli software senza un'etichetta personalizzata**|Visualizza tutti i titoli software che non hanno un'etichetta personalizzata definita.|  
|**Software 14A - Ricerca di software con tag di identificazione software abilitato**|Visualizza un conteggio dei software installati con un tag di identificazione software abilitato.|  
|**Software 14B - Computer con software specifico installato con tag di identificazione software abilitato**|Visualizza tutti i computer con software installato con un tag di identificazione software abilitato specifico.|  
|**Software 14C - Software istallato con tag di identificazione software abilitato in un computer specifico**|Visualizza tutti i software installati con un tag di identificazione software specifico abilitato in un computer specifico.|  
|**Ciclo di vita 01A - Computer con un prodotto software specifico**|Visualizza un elenco dei computer in cui viene rilevato un prodotto specificato.|
|**Ciclo di vita 02A - Elenco di computer con prodotti scaduti nell'organizzazione**|Visualizza i computer con prodotti scaduti. È possibile filtrare questo report in base al nome del prodotto.|
|**Ciclo di vita 03A - Elenco di prodotti scaduti rilevati nell'organizzazione**|Visualizza i dettagli relativi ai prodotti trovati nell'ambiente con date del ciclo di vita scadute.|
|**Ciclo di vita 04A - Panoramica generale del ciclo di vita del prodotto**|Visualizza un elenco di cicli di vita dei prodotti. Filtrare l'elenco in base al nome del prodotto e ai giorni mancanti alla scadenza.|
|**Ciclo di vita 05A - Dashboard Ciclo di vita del prodotto**|A partire dalla versione 1810, questo report include informazioni simili a quelle del dashboard nella console.|



## <a name="client-push"></a>Push client  

I quattro report seguenti sono elencati nella la categoria **Push client**.  

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Dettagli stato dell'installazione push client**|Visualizza informazioni sul processo di installazione push client per tutti i siti.|  
|**Dettagli stato dell'installazione push client per un sito specifico**|Visualizza informazioni sul processo di installazione push client per un sito specifico.|  
|**Riepilogo stato dell'installazione push client**|Visualizza un riepilogo dello stato di installazione push client per tutti i siti.|  
|**Riepilogo stato dell'installazione push client per un sito specifico**|Visualizza un riepilogo dello stato di installazione push client per un sito specifico.|  



## <a name="client-status"></a>Stato del client  

I sette report seguenti sono elencati nella categoria **Stato client**.  

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Dettagli correzione client**|Visualizza i dettagli delle azioni di correzione dei client per una raccolta specifica.|  
|**Riepilogo correzione client**|Visualizza un riepilogo delle azioni di correzione dei client per una raccolta specifica.|  
|**Cronologia stato client**|Visualizza una cronologia dello stato client generale nel sito.|  
|**Riepilogo stato client**|Visualizza i risultati del controllo client dei client attivi per una raccolta specificata.|  
|**Tempo di richiesta criterio del client**|Visualizza la percentuale di client che hanno richiesto il criterio almeno una volta negli ultimi 30 giorni. Ogni giorno rappresenta una percentuale dei client totali che hanno richiesto il criterio dal primo giorno in cui erano all'interno del ciclo.|  
|**Client con dettagli controllo client non riuscito**|Visualizza i dettagli sui client che non hanno passato il controllo client per una raccolta specifica.|  
|**Dettagli client inattivi**|Visualizza un elenco dettagliato dei client inattivi per una raccolta specifica.|  



## <a name="company-resource-access"></a>Accesso alle risorse aziendali  

I tre report seguenti sono elencati nella categoria **Accesso alle risorse aziendali**. 

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Cronologia di rilascio dei certificati**|Visualizza la cronologia dei certificati rilasciati dal punto di registrazione certificati a utenti e dispositivi per l'intervallo di date specificato.|  
|**Elenco degli asset per stato di rilascio del certificato**|Visualizza i dispositivi o gli utenti in uno specifico stato di rilascio di certificati a seguito della valutazione di un profilo di certificato specifico.|  
|**Elenco degli asset con certificati prossimi alla scadenza**|Visualizza i dispositivi o gli utenti con certificati che scadono in corrispondenza della data specificata o prima.|  



## <a name="compliance-and-settings-management"></a>Gestione conformità e impostazioni  

I 22 report seguenti sono elencati nella categoria **Gestione conformità e impostazioni**. 

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Cronologia di conformità di una linea di base configurazione**|Visualizza la cronologia delle modifiche in conformità di una linea di base configurazione per l'intervallo di date specificato.|  
|**Cronologia di conformità di un elemento di configurazione**|Visualizza la cronologia delle modifiche in conformità di un elemento di configurazione per l'intervallo di date specificato.|  
|**Dettagli delle regole conformi degli elementi di configurazione in una linea di base configurazione per un asset**|Visualizza informazioni sulle regole valutate come conformi per un elemento di configurazione specifico per un dispositivo o utente specifico.|  
|**Dettagli delle regole in conflitto degli elementi di configurazione in una linea di base configurazione per un asset**|Visualizza informazioni sulle regole in un elemento di configurazione distribuito in conflitto con altre regole. Include le altre regole nello stesso elemento di configurazione distribuito o in un altro elemento.|  
|**Dettagli degli errori degli elementi di configurazione in una linea di base configurazione per un asset**|Visualizza le informazioni sugli errori generati da un elemento di configurazione specifico per un dispositivo o un utente specifico.|  
|**Dettagli delle regole non conformi degli elementi di configurazione in una linea di base configurazione per un asset**|Visualizza le informazioni sulle regole valutate come non conformi per un elemento di configurazione specifico, per un dispositivo o un utente specifico.|  
|**Dettagli delle regole risolte degli elementi di configurazione in una linea di base configurazione per un asset**|Visualizza le informazioni sulle regole risolte da un elemento di configurazione specifico per un dispositivo o un utente specifico.|  
|**Elenco degli asset per stato di conformità per una linea di base configurazione**|Visualizza i dispositivi o gli utenti in uno specifico stato di conformità a seguito della valutazione di una linea di base configurazione specifica.|  
|**Elenco degli asset per stato di conformità per un elemento di configurazione in una linea di base configurazione**|Visualizza i dispositivi o gli utenti in uno specifico stato di conformità a seguito della valutazione di un elemento di configurazione specifico.|  
|**Elenco di app e dispositivi non conformi per un utente specificato**|Visualizza informazioni sugli utenti e sui dispositivi che dispongono di app installate che non sono conformi ai criteri specificati.|  
|**Elenco delle regole in conflitto con una regola specifica per un asset**|Visualizza un elenco di regole in conflitto con una regola specifica per un elemento di configurazione distribuito.|  
|**Elenco degli asset sconosciuti per una linea di base configurazione**|Visualizza un elenco di dispositivi o utenti che non hanno ancora segnalato eventuali dati di conformità per una linea di base di configurazione specifica.|  
|**Elenco degli asset sconosciuti per un elemento di configurazione**|Visualizza un elenco di dispositivi o utenti che non hanno ancora segnalato eventuali dati di conformità per un elemento di configurazione specifico.|  
|**Riepilogo delle regole e degli errori degli elementi di configurazione in una linea di base configurazione per un asset**|Visualizza un riepilogo dello stato di conformità delle regole ed eventuali errori di impostazione per un elemento di configurazione specifico. L'elemento di configurazione deve essere distribuito a un dispositivo o a un utente.|  
|**Riepilogo di conformità per linea di base configurazione**|Visualizza un riepilogo della conformità generale delle linee di base di configurazione distribuite nella gerarchia.|  
|**Riepilogo di conformità per elementi di configurazione per una linea di base configurazione**|Visualizza un riepilogo della conformità degli elementi di configurazione in una linea di base di configurazione.|  
|**Riepilogo di conformità per criteri di configurazione**|Visualizza un riepilogo della conformità dei criteri di configurazione.|  
|**Riepilogo di conformità di una linea di base di configurazione per una raccolta**|Visualizza un riepilogo della conformità generale di una linea di base di configurazione specifica. L'elemento di configurazione deve essere distribuito a una raccolta specifica.|  
|**Riepilogo degli utenti con app non conformi**|Visualizza informazioni sugli utenti che dispongono di app installate che non sono conformi ai criteri specificati.|  
|**Accettazione di termini e condizioni**|Visualizza i termini e le condizioni e indica la versione accettata da ogni utente.|  



## <a name="data-warehouse"></a>Data warehouse  

I sette report seguenti sono elencati nella categoria **Data warehouse**. 

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Distribuzione applicazioni**|Cronologico: Visualizza i dettagli per la distribuzione di applicazioni per un'applicazione e un computer specifici.|
|**Conformità di Endpoint Protection e degli aggiornamenti software**|Cronologico: Visualizza i computer in cui mancano aggiornamenti software.|
|**Inventario hardware generale**|Cronologico: Visualizza tutto l'inventario dell'hardware per un computer specifico.|
|**Inventario software generale**|Cronologico: Visualizza tutto l'inventario del software per un computer specifico.|
|**Panoramica dell'integrità dell'infrastruttura**|Cronologico: Visualizza una panoramica dell'integrità dell'infrastruttura di Configuration Manager.|
|**Elenco del malware rilevato**|Cronologico: Visualizza il malware che è stato rilevato nell'organizzazione.|
|**Riepilogo di distribuzione del software**|Cronologico: Riepilogo della distribuzione del software per un annuncio e un computer specifici.|


## <a name="device-management"></a>Gestione dei dispositivi  

I 37 report seguenti sono elencati nella categoria **Gestione dispositivi**. 

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Tutti i dispositivi mobili di proprietà dell'azienda**|Visualizza tutti i dispositivi mobili di proprietà dell'azienda.|
|**Tutti i client dispositivo mobile**|Visualizza le informazioni su tutti i client del dispositivo mobile. I dispositivi gestiti dal connettore Exchange Server non sono inclusi.|  
|**Problemi di certificato nei dispositivi mobili gestiti dal client di Configuration Manager per Windows CE e che non sono integri**|Visualizza informazioni dettagliate sui problemi di certificato nei dispositivi mobili gestiti dal client di Configuration Manager per Windows CE.|  
|**Errori di distribuzione client per i dispositivi mobili gestiti dal client di Configuration Manager per Windows CE**|Visualizza informazioni dettagliate sugli errori di distribuzione per i dispositivi mobili gestiti dal client di Configuration Manager per Windows CE.|  
|**Dettagli di stato della distribuzione client per i dispositivi mobili gestiti dal client di Configuration Manager per Windows CE**|Visualizza informazioni sullo stato dei dispositivi mobili gestiti dal client di Configuration Manager per Windows CE.|  
|**Distribuzione client per i dispositivi mobili gestiti dal client di Configuration Manager per Windows CE**|Visualizza informazioni dettagliate sulla distribuzione per i dispositivi mobili gestiti dal client di Configuration Manager per Windows CE.|  
|**Problemi di comunicazione nei dispositivi mobili gestiti dal client di Configuration Manager per Windows CE e che non sono integri**|Il report contiene informazioni dettagliate sui problemi di comunicazione nei dispositivi mobili gestiti dal client di Configuration Manager per Windows CE.|  
|**Stato di conformità del criterio cassetta postale ActiveSync predefinito per i dispositivi mobili gestiti dal connettore Exchange Server**|Visualizza un riepilogo dello stato di conformità al criterio cassetta postale Exchange ActiveSync predefinito per i dispositivi mobili gestiti dal connettore Exchange Server.|  
|**Numero di dispositivi mobili per configurazioni di visualizzazione**|Questo report visualizza il numero di dispositivi mobili per impostazioni di visualizzazione.|  
|**Numero di dispositivi mobili per sistema operativo**|Visualizza il numero di dispositivi mobili per sistema operativo.|  
|**Numero di dispositivi mobili per memoria programma**|Visualizza il numero di dispositivi mobili per memoria programma.|  
|**Numero di dispositivi mobili per configurazioni memoria di archiviazione**|Numero di dispositivi mobili per configurazioni memoria di archiviazione|  
|**Informazioni di stato dettagliate per i dispositivi mobili gestiti dal client di Configuration Manager per Windows CE**|Visualizza informazioni di stato dettagliate per i dispositivi mobili gestiti dal client di Configuration Manager per Windows CE.|  
|**Informazioni di riepilogo dello stato per i dispositivi mobili gestiti dal client di Configuration Manager per Windows CE**|Visualizza informazioni di riepilogo dello stato per i dispositivi mobili gestiti dal client di Configuration Manager per Windows CE.|  
|**Dispositivi mobili inattivi che sono gestiti dal connettore Exchange Server**|Visualizza i dispositivi mobili gestiti dal connettore Exchange Server che non si sono connessi a Exchange Server in un numero di giorni specifico.|  
|**Elenco di dispositivi in base allo stato dell'attestazione dell'integrità**|Visualizza un elenco di dispositivi con attributi segnalati dal servizio di attestazione dell'integrità.|
|**Elenco dei dispositivi registrati a Microsoft Intune per utente**|Visualizza tutti i dispositivi iscritti da un utente con Microsoft Intune.|  
|**Elenco di dispositivi in una categoria di dispositivi specifica**|Visualizza informazioni per tutti i dispositivi all'interno di una categoria di dispositivi specifica.|
|**Problemi del client locale nei dispositivi mobili gestiti dal client di Configuration Manager per Windows CE e che non sono integri**|Il report contiene informazioni dettagliate sui problemi del client locale nei dispositivi mobili gestiti dal client di Configuration Manager per Windows CE.|  
|**Informazioni client dispositivo mobile**|Visualizza informazioni sui dispositivi mobili in cui è installato il client di Configuration Manager. È possibile usare il report per verificare quali dispositivi mobili sono in grado di comunicare con un punto di gestione.|  
|**Dettagli di conformità dei dispositivi mobili per il connettore Exchange Server**|Visualizza i dettagli di conformità dei dispositivi mobili per un criterio cassetta postale predefinito di Exchange ActiveSync configurato usando il connettore Exchange Server.|  
|**Dispositivi mobili per sistema operativo**|Visualizza i dispositivi mobili per sistema operativo.|  
|**Dispositivi mobili jailbroken o dispositivo rooted**|Visualizza i dispositivi mobili jailbroken o un dispositivo rooted.|  
|**Dispositivi mobili non gestiti perché si sono registrati ma non sono riusciti ad assegnare a un sito**|Visualizza i dispositivi mobili che hanno completato la registrazione in Configuration Manager e hanno un certificato, ma non sono riusciti a completare l'assegnazione sito.|  
|**Dispositivi mobili con una quantità specifica di memoria programma libera**|Visualizza tutti i dispositivi mobili con la quantità specificata di memoria programma libera.|  
|**Dispositivi mobili con una quantità specifica di memoria di archiviazione disponibile libera**|Visualizza tutti i dispositivi mobili con la quantità specificata di memoria rimovibile libera.|  
|**Dispositivi mobili con problemi di rinnovo certificato**|Visualizza i dispositivi mobili registrati che non sono riusciti a rinnovare il certificato. Se il certificato non viene rinnovato prima del periodo di scadenza, i dispositivi mobili non saranno gestiti.|  
|**Dispositivi mobili con memoria programma insufficiente (inferiore ai KB disponibili specificati)**|Visualizza i dispositivi mobili per cui la memoria programma è inferiore alla dimensione specificata in KB.|  
|**Dispositivi mobili con memoria di archiviazione rimovibile insufficiente (inferiore ai KB disponibili specificati)**|Visualizza i dispositivi mobili per cui la memoria di archiviazione rimovibile è inferiore alla dimensione specificata in KB.|  
|**Numero di dispositivi registrati a Microsoft Intune per utente**|Visualizza gli utenti abilitati alla sottoscrizione a Microsoft Intune. Visualizza anche il numero totale di dispositivi registrati per ogni utente.|  
|**Richiesta di disattivazione e cancellazione in sospeso per i dispositivi mobili**|Visualizza le richieste di cancellazione in sospeso per i dispositivi mobili.|  
|**Dispositivi mobili registrati e assegnati di recente**|Visualizza i dispositivi mobili che si sono registrati di recente a Configuration Manager e hanno assegnato a un sito.|  
|**Dispositivi mobili cancellati di recente**|Visualizza l'elenco dei dispositivi mobili che sono stati cancellati di recente.|  
|**Riepilogo impostazioni per i dispositivi mobili che sono gestiti dal connettore Exchange Server**|Visualizza il numero di dispositivi mobili che applicano le impostazioni per ogni criterio cassetta postale Exchange ActiveSync predefinito gestito dal connettore Exchange Server.|  
|**Stato dettagliato delle chiavi di sideload di Windows RT**|Visualizza informazioni dettagliate sullo stato per una chiave di sideload di Windows RT specifica.|  
|**Riepilogo delle chiavi di sideload di Windows RT**|Visualizza lo stato delle chiavi di sideload di Windows RT.|  



## <a name="driver-management"></a>Gestione driver  

I 13 report seguenti sono elencati nella categoria **Gestione driver**. 

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Tutti i driver**|Visualizza un elenco di tutti i driver.|  
|**Tutti i driver per una piattaforma specifica**|Visualizza tutti i driver per una piattaforma specifica.|  
|**Tutti i driver in un'immagine di avvio specifica**|Visualizza tutti i driver in un'immagine di avvio specifica.|  
|**Tutti i driver in una categoria specifica**|Visualizza tutti i driver in una categoria specifica.|  
|**Tutti i driver in un pacchetto specifico**|Visualizza tutti i driver in un pacchetto specifico.|  
|**Categorie per un driver specifico**|Visualizza le categorie per un driver specifico.|  
|**Computer in cui non è stato possibile installare i driver per una raccolta specifica**|Visualizza i computer in cui non è stato possibile installare i driver per una raccolta specifica.|  
|**Report che corrisponde al catalogo driver per una raccolta specifica**|Visualizza il report che corrisponde al catalogo driver per una raccolta specifica.|  
|**Report che corrisponde al catalogo driver per un computer specifico**|Visualizza il report che corrisponde al catalogo driver per un computer specifico.|  
|**Report che corrisponde al catalogo driver per un dispositivo specifico in un computer specifico**|Visualizza il report che corrisponde al catalogo driver per un dispositivo specifico in un computer specifico.|  
|**Report che corrisponde al catalogo driver per i computer in una raccolta specifica con un dispositivo specifico**|Visualizza il report che corrisponde al catalogo driver per i computer in una raccolta specifica con un dispositivo specifico.|  
|**Driver che non è stato possibile installare in un computer specifico**|Visualizza i driver che non è stato possibile installare in un computer specifico.|  
|**Piattaforme supportate per un driver specifico**|Visualizza le piattaforme supportate per un driver specifico.|  



## <a name="endpoint-protection"></a>Endpoint Protection  

I sei report seguenti sono elencati nella categoria **Endpoint Protection**. 

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Report attività antimalware**|Visualizza una panoramica dell'attività antimalware.|  
|**Cronologia e stato generale antimalware**|Visualizza la cronologia e lo stato generale antimalware.|  
|**Dettagli malware computer**|Visualizza i dettagli di un computer specifico e l'elenco di malware rilevati.|  
|**Computer infetti**|Visualizza un elenco di computer in cui è stata rilevata una minaccia specifica.|  
|**Principali utenti da minacce**|Visualizza l'elenco degli utenti con il numero maggiore di minacce rilevate.|  
|**Elenco di minacce utente**|Visualizza l'elenco delle minacce rilevate per un account utente specifico.|  



## <a name="hardware---cd-rom"></a>Hardware - CD-ROM  

I quattro report seguenti sono elencati nella categoria **Hardware - CD-ROM**. 

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Informazioni CD-ROM per un computer specifico**|Visualizza le informazioni sulle unità CD-ROM in un computer specifico.|  
|**Computer per un produttore CD-ROM specifico**|Visualizza un elenco di computer che contengono un'unità CD-ROM fatta da un produttore specifico.|  
|**Numero di unità CD-ROM per produttore**|Visualizza il numero di unità CD-ROM in inventario per produttore.|  
|**Cronologia - Cronologia CD-ROM per un computer specifico**|Visualizza le informazioni di inventario per le unità CD-ROM in un computer specifico.|  



## <a name="hardware---disk"></a>Hardware - Disco  

Gli otto report seguenti sono elencati nella categoria **Hardware - Disco**. 

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Computer con una dimensione specifica di disco rigido**|Visualizza un elenco di computer che dispongono di dischi rigidi di una capacità specifica.|  
|**Computer con spazio su disco insufficiente (inferiore alla percentuale disponibile specificata)**|Visualizza un elenco di computer in una raccolta specifica con una quantità di spazio su disco libero inferiore alla percentuale specificata.|  
|**Computer con spazio su disco insufficiente (inferiore ai MB disponibili specificati)**|Visualizza un elenco di computer e dischi in cui lo spazio del disco è insufficiente. La quantità di spazio disponibile da controllare è specificata in MB.|  
|**Conteggio configurazioni disco fisso**|Visualizza il numero di dischi fissi in inventario per capacità disco.|  
|**Informazioni disco per un computer specifico - Dischi logici**|Visualizza le informazioni di riepilogo sui dischi logici in un computer specifico.|  
|**Informazioni disco per un computer specifico - Partizioni**|Visualizza le informazioni di riepilogo sulle partizioni del disco in un computer specifico.|  
|**Informazioni disco per un computer specifico - Dischi fisici**|Visualizza le informazioni di riepilogo sui dischi fisici in un computer specifico.|  
|**Cronologia - Cronologia spazio disco logico per un computer specifico**|Visualizza le informazioni di inventario per le unità disco logico in un computer specifico.|  



## <a name="hardware---general"></a>Hardware - Generale  

I cinque report seguenti sono elencati nella categoria **Hardware - Generale**.

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Informazioni computer per un computer specifico**|Visualizza le informazioni di riepilogo per un computer specifico.|  
|**Computer in un gruppo di lavoro o dominio specifico**|Visualizza un elenco di computer in un gruppo di lavoro o dominio specifico.|  
|**Classi inventario assegnate a una raccolta specifica**|Visualizza le classi inventario assegnate a una raccolta specifica.|  
|**Classi inventario abilitate in un computer specifico**|Visualizza le classi inventario abilitate in un computer specifico.|  
|**Informazioni sui dispositivi di Windows AutoPilot**|Visualizza le informazioni sul dispositivo client necessarie per la registrazione a Windows AutoPilot.|



## <a name="hardware---memory"></a>Hardware - Memoria  

I cinque report seguenti sono elencati nella categoria **Hardware - Memoria**.

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Computer in cui la memoria fisica è cambiata**|Visualizza un elenco di computer in cui la quantità di RAM è cambiata dall'ultimo ciclo di inventario.|  
|**Computer con una quantità specifica di memoria**|Visualizza un elenco di computer che dispongono di una quantità specifica di RAM (memoria fisica totale arrotondata in MB).|  
|**Computer con memoria insufficiente (inferiore o uguale ai MB specificati)**|Visualizza un elenco di computer con memoria insufficiente. La quantità di memoria da controllare è specificata in MB.|  
|**Conteggio configurazioni memoria**|Visualizza il numero di computer in inventario per quantità di RAM.|  
|**Informazioni memoria per un computer specifico**|Visualizza le informazioni di riepilogo sulla memoria in un computer specifico.|  



## <a name="hardware---modem"></a>Hardware - Modem  

I tre report seguenti sono elencati nella categoria **Hardware - Modem**.

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Computer per un produttore modem specifico**|Visualizza un elenco di computer che dispongono di un modem fatto da un produttore specifico.|  
|**Conteggio di modem per produttore**|Visualizza il numero di modem in inventario per ogni produttore.|  
|**Informazioni modem per un computer specifico**|Visualizza le informazioni di riepilogo sul modem in un computer specifico.|  



## <a name="hardware---network-adapter"></a>Hardware - Scheda di rete  

I tre report seguenti sono elencati nella categoria **Hardware - Scheda di rete**.

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Computer con una scheda di rete specifica**|Visualizza un elenco di computer che dispongono di una scheda di rete specifica.|  
|**Conteggio schede di rete per tipo**|Visualizza il numero di schede di rete di ogni tipo in inventario.|  
|**Informazioni scheda di rete per un computer specifico**|Visualizza informazioni sulle schede di rete installate in un computer specifico.|  



## <a name="hardware---processor"></a>Hardware - Processore  

I cinque report seguenti sono elencati nella categoria **Hardware - Processore**.

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Computer per una velocità di processore specifica**|Visualizza un elenco di computer che dispongono di un processore di una velocità specifica.|  
|**Computer con processori veloci (velocità superiore o uguale alla velocità di clock specificata)**|Visualizza un elenco di computer che dispongono di processori con una velocità più veloce rispetto a quella specificata.|  
|**Computer con processori lenti (velocità inferiore o uguale alla velocità di clock specificata)**|Visualizza un elenco di computer che dispongono di un processore che esegue a una velocità uguale o superiore alla velocità di clock specificata.|  
|**Conteggio velocità processore**|Visualizza il numero di computer in inventario per velocità del processore.|  
|**Informazioni processore per un computer specifico**|Visualizza informazioni sui processori installati in un computer specifico.|  



## <a name="hardware---scsi"></a>Hardware - SCSI  

I cinque report seguenti sono elencati nella categoria **Hardware - SCSI**.

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Computer con un tipo di scheda SCSI specifica**|Visualizza un elenco di computer che dispongono di una scheda SCSI specifica.|  
|**Conteggio tipi di scheda SCSI**|Visualizza il numero di schede SCSI in inventario per tipo di scheda.|  
|**Informazioni scheda SCSI per un computer specifico**|Visualizza informazioni sulle schede SCSI installate in un computer specifico.|  



## <a name="hardware---security"></a>Hardware - Sicurezza

Il report seguente è elencato nella categoria **Hardware - Sicurezza**.

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Dettagli degli stati del firmware nei dispositivi**|Visualizza i dettagli degli stati di UEFI, SecureBoot e TPM. **Nota**: questo report non è incluso nella versione 1810.<!--SCCMDocs issue #1189-->|  



## <a name="hardware---sound-card"></a>Hardware - Scheda audio  

I tre report seguenti sono elencati nella categoria **Hardware - SCSI**.

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Computer con una scheda audio specifica**|Visualizza un elenco di computer che dispongono di una scheda audio specifica.|  
|**Conteggio schede audio**|Visualizza il numero di computer in inventario per ogni tipo di scheda audio.|  
|**Informazioni scheda audio per un computer specifico**|Visualizza le informazioni di riepilogo sulla scheda audio in un computer specifico.|  



## <a name="hardware---video-card"></a>Hardware - Scheda video  

I tre report seguenti sono elencati nella categoria **Hardware - Scheda video**.

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Computer con una scheda video specifica**|Visualizza un elenco di computer che dispongono di una scheda video specifica.|  
|**Conteggio schede video per tipo**|Visualizza un elenco di tutte le schede video installate nei computer. Indica inoltre il numero di ogni tipo di scheda video.|  
|**Informazioni scheda video per un computer specifico**|Visualizza informazioni di riepilogo sulle schede video installate in un computer specifico.|  



## <a name="migration"></a>Migrazione  

I cinque report seguenti sono elencati nella categoria **Migrazione**.

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Client nell'elenco di esclusione**|Visualizza i client che sono esclusi dalla migrazione.|  
|**Dipendenza da una raccolta di Configuration Manager**|Visualizza gli oggetti che dipendono da una raccolta della gerarchia di origine.|  
|**Proprietà processo migrazione**|Questo report mostra i contenuti del processo di migrazione specifico.|  
|**Processi di migrazione**|Questo report mostra l'elenco dei processi di migrazione.|  
|**Oggetti non migrati**|Visualizza un elenco degli oggetti che non sono stati migrati durante l'ultimo tentativo.|  



## <a name="network"></a>Rete  

I sei report seguenti sono elencati nella categoria **Rete**.

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Conteggio indirizzi IP per subnet**|Visualizza il numero di indirizzi IP in inventario per ogni subnet IP.|  
|**IP - Tutte le subnet per subnet mask**|Visualizza un elenco di subnet IP e subnet mask.|  
|**IP - Computer in una subnet specifica**|Visualizza un elenco di computer e informazioni IP per una subnet IP specifica.|  
|**IP - Informazioni per un computer specifico**|Visualizza le informazioni di riepilogo sull'IP in un computer specifico.|  
|**IP - Informazioni per un indirizzo IP specifico**|Visualizza le informazioni di riepilogo su un indirizzo IP specifico.|  
|**MAC - Computer per un indirizzo MAC specifico**|Visualizza il nome del computer e l'indirizzo IP dei computer con l'indirizzo MAC specificato.|  



## <a name="operating-system"></a>Sistema operativo  

I 10 report seguenti sono elencati nella categoria **Sistema operativo**.

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Cronologia versione del sistema operativo del computer**|Visualizza la cronologia di inventario per sistema operativo in un computer specifico.|  
|**Computer con un sistema operativo specifico**|Visualizza i computer con un sistema operativo specifico.|  
|**Computer con un sistema operativo e un Service Pack specifici**|Visualizza i computer con un sistema operativo e un Service Pack specifici.|  
|**Conteggio versioni sistema operativo**|Visualizza il numero di computer in inventario per sistema operativo.|  
|**Conteggio di sistemi operativi e Service Pack**|Visualizza il numero di computer in inventario per sistema operativo e combinazioni di Service Pack.|  
|**Servizi - Computer che eseguono un servizio specifico**|Visualizza un elenco di computer che eseguono un servizio specifico.|  
|**Servizi - Computer che eseguono Server di Accesso remoto**|Visualizza un elenco di computer che eseguono Server di Accesso remoto.|  
|**Servizi - Informazioni sui servizi per un computer specifico**|Visualizza le informazioni di riepilogo sui servizi in un computer specifico.|  
|**Dettagli della manutenzione di Windows 10 per una raccolta specifica**|Visualizza informazioni generali sulla manutenzione di Windows 10 per una raccolta specifica.|
|**Computer Windows Server**|Visualizza un elenco di computer che eseguono sistemi operativi Windows Server.|  


## <a name="power-management"></a>Risparmio energia  

I 18 report seguenti sono elencati nella categoria **Risparmio energia**.

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Risparmio energia - Attività computer**|Visualizza un grafico che illustra l'attività di monitor, computer e utente per una raccolta specifica in un periodo di tempo specificato.|  
|**Risparmio energia - attività computer per computer**|Visualizza un grafico che illustra l'attività di monitor, computer e utente per un computer specifico in una data specificata.|  
|**Risparmio energia - Dettagli attività computer**|Visualizza un elenco di capacità sospese e attive di computer in una raccolta specificata per una data e ora specificate.|  
|**Risparmio energia - Dettagli computer**|Visualizza informazioni dettagliate su capacità di risparmio di energia, impostazioni del risparmio di energia e combinazioni per il risparmio di energia applicate a un computer specificato.|  
|**Risparmio energia - Computer che non segnalano dettagli**|Visualizza un elenco di computer che non riportano attività per il risparmio di energia per una data e ora specificate.|  
|**Risparmio energia - Computer esclusi**|Visualizza un elenco di computer esclusi dalla combinazione per il risparmio di energia.|  
|**Risparmio energia - Computer con più combinazioni per il risparmio di energia**|Visualizza un elenco di computer con più impostazioni per il risparmio di energia in conflitto.|  
|**Risparmio energia - Consumo energia**|Visualizza il consumo totale di energia mensile (in kWh) per una raccolta specificata in un periodo di tempo specificato.|  
|**Risparmio energia - Consumo energia per giorno**|Visualizza il consumo totale di energia (in kWh) per una raccolta specificata negli ultimi 31 giorni.|  
|**Risparmio energia - Costo energia**|Visualizza il costo totale del consumo di energia mensile per una raccolta specificata in un periodo di tempo specificato.|  
|**Risparmio energia - Costo energia per giorno**|Visualizza il costo totale del consumo di energia per una raccolta specificata nei precedenti 31 giorni.|  
|**Risparmio energia - Impatto ambientale**|Visualizza un grafico con le emissioni di anidride carbonica (CO2) generate da una raccolta specificata nel corso di un periodo di tempo specificato.|  
|**Risparmio energia - Impatto ambientale per giorno**|Visualizza un grafico con le emissioni di CO2 generate da una raccolta specificata nel corso dei precedenti 31 giorni.|  
|**Risparmio energia - Dettagli errore sospensione del computer**|Visualizza informazioni dettagliate sui computer che non sono stati sospesi o messi in stato di ibernazione nel periodo di tempo specificato.|  
|**Risparmio energia - Report errore sospensione**|Visualizza un elenco di cause comuni che hanno impedito ai computer di essere sospesi o messi in stato di ibernazione. Indica inoltre il numero di computer interessati da ogni causa per un periodo di tempo specificato.|  
|**Risparmio energia - Funzionalità alimentazione**|Visualizza le capacità di gestione energia dei computer nella raccolta specificata.|  
|**Risparmio energia - Impostazioni risparmio energia**|Visualizza un elenco aggregato di impostazioni per il risparmio di energia usate dai computer in una raccolta specificata.|  
|**Risparmio energia - Dettagli impostazioni risparmio energia**|Usato per visualizzare altre informazioni sui computer che sono stati specificati nel report **Risparmio energia - Impostazioni risparmio energia**.|  



## <a name="replication-traffic"></a>Traffico di replica  

I 10 report seguenti sono elencati nella categoria **Traffico di replica**.

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Traffico di replica dati globali per collegamento (grafico a linee)**|Visualizza il traffico di replica dei dati globali totale in un collegamento specificato per un numero di giorni specificato.|  
|**Traffico di replica dati globali per collegamento (grafico a torta)**|Visualizza il traffico di replica dei dati globali totale in un collegamento specificato per un numero di giorni specificato.|  
|**Traffico di replica della gerarchia per collegamento**|Visualizza il traffico di replica totale per ciascun collegamento della gerarchia per il numero di giorni specificato.|  
|**Traffico dei primi dieci gruppi di replica della gerarchia (grafico a torta)**|Visualizza il traffico di replica per i primi 10 gruppi di replica di tutta la gerarchia identificata per collegamento.|  
|**Traffico di replica del collegamento**|Visualizza il traffico di replica totale per tutti i dati per il numero di giorni specificato.|  
|**Traffico del gruppo di replica per collegamento**|Visualizza il traffico di rete del gruppo di replica su un collegamento di replica di database specifico per il numero di giorni specificato.|  
|**Traffico di replica dati del sito per collegamento (grafico a linee)**|Visualizza il traffico di replica dei dati del sito totale in un collegamento specificato per un numero di giorni specificato.|  
|**Traffico di replica dati del sito per collegamento (grafico a torta)**|Visualizza il traffico di replica dei dati del sito totale in un collegamento specificato per un numero di giorni specificato.|  
|**Traffico di replica totale della gerarchia (grafico a linee)**|Visualizza la replica dati del sito e dei dati globali aggregati della gerarchia per ciascuna direzione di ogni collegamento per il numero di giorni specificato.|  
|**Traffico di replica totale della gerarchia (grafico a torta)**|Visualizza la replica dati del sito e dei dati globali aggregati della gerarchia per ciascuna direzione di ogni collegamento per il numero di giorni specificato.|  



## <a name="site---client-information"></a>Sito - Informazioni client  

I 19 report seguenti sono elencati nella categoria **Sito - Informazioni client**.

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Report dettagliato sullo stato di assegnazione client**|Visualizza informazioni dettagliate sullo stato di assegnazione client.|  
|**Dettagli errore di assegnazione client**|Visualizza informazioni dettagliate sugli errori di assegnazione client.|  
|**Dettagli stato di assegnazione client**|Visualizza informazioni generali sullo stato di assegnazione client.|  
|**Dettagli assegnazione client completata**|Visualizza informazioni dettagliate sui client assegnati.|  
|**Report errore di distribuzione client**|Visualizza informazioni dettagliate per i client in cui non è stato possibile eseguire la distribuzione.|  
|**Dettagli stato di distribuzione client**|Visualizza informazioni di riepilogo per lo stato delle installazioni client.|  
|**Report distribuzione client completata**|Visualizza informazioni dettagliate per i client distribuiti.|  
|**Client non idonei per la comunicazione HTTPS**|Visualizza informazioni dettagliate su ogni client che esegue lo strumento per la preparazione della comunicazione HTTPS e che segnala di non essere in grado di comunicare tramite HTTPS.|  
|**Computer assegnati ma non installati per un sito particolare**|Visualizza un elenco di computer assegnati a un sito specifico, ma che non riportano al sito.|  
|**Computer con una specifica versione del client di Configuration Manager**|Visualizza un elenco di computer che eseguono una versione specifica del software client di Configuration Manager.|  
|**Conteggio di client e protocolli usati per la comunicazione**|Visualizza un riepilogo dei metodi di comunicazione usati dai client (HTTP o HTTPS).|  
|**Conteggio di client assegnati e installati per ogni sito**|Visualizza il numero di computer assegnati e installati per ogni sito. I client con un percorso di rete associato a più siti sono contati solo come installati se riportano a un sito.|  
|**Conteggio dei client idonei per la comunicazione HTTPS**|Visualizza informazioni dettagliate su ogni client che esegue lo strumento per la preparazione della comunicazione HTTPS e che segnala di essere o non essere in grado di comunicare tramite HTTPS.|  
|**Conteggio di client per ogni sito**|Visualizza il numero di client di Configuration Manager installati per codice sito.|  
|**Conteggio dei client di Configuration Manager per versioni client**|Visualizza il numero di computer individuati dalla versione client di Configuration Manager.|  
|**Dettagli problema riportati al punto di stato di fallback per una raccolta specifica**|Visualizza informazioni dettagliate sui problemi segnalati dai client in una raccolta specifica. È necessario assegnare a questi client un punto di stato di fallback.|  
|**Dettagli problema riportati al punto di stato di fallback per un sito specifico**|Visualizza informazioni dettagliate sui problemi segnalati dai client in un sito specifico. È necessario assegnare a questi client un punto di stato di fallback.|  
|**Riepilogo dei problemi riportati al punto di stato di fallback**|Visualizza informazioni su tutti i problemi segnalati dai client. È necessario assegnare a questi client un punto di stato di fallback.|  
|**Riepilogo dei problemi riportati al punto di stato di fallback per una raccolta specifica**|Visualizza informazioni di riepilogo sui problemi segnalati dai client in una raccolta specifica. È necessario assegnare a questi client un punto di stato di fallback.|  



## <a name="site---discovery-and-inventory-information"></a>Sito - Informazioni individuazione e inventario  

I 10 report seguenti sono elencati nella categoria **Sito - Informazioni individuazione e inventario**.

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Client che non hanno riportato di recente (in un numero specifico di giorni)**|Visualizza un elenco dei client che non hanno riportato dati di individuazione, inventario hardware o inventario software in un numero specifico di giorni.|  
|**Computer individuati per un sito specifico**|Visualizza un elenco di tutti i computer individuati dal sito specificato. Indica inoltre la data dell'individuazione più recente.|  
|**Computer individuati recentemente per metodo di individuazione**|Visualizza un elenco dei computer individuati dal sito entro il numero di giorni specificato. Elenca anche gli agenti che li hanno individuati. Se un computer è stato individuato da più agenti, è possibile che venga visualizzato più di una volta nell'elenco.|  
|**Client non individuati di recente (in un numero specifico di giorni)**|Visualizza un elenco dei computer che il sito ha individuato non di recente. Indica anche il numero di giorni trascorsi da quando il sito ha individuato il computer.|  
|**Computer non entrati in inventario di recente (in un numero specifico di giorni)**|Visualizza un elenco dei computer che il sito non ha inserito nell'inventario di recente. Indica anche l'ultima volta che il sito ha incluso il computer in inventario.|  
|**Computer che potrebbero condividere lo stesso identificatore univoco di Configuration Manager**|Visualizza un elenco di computer che hanno modificato il nome. Una modifica nel nome può significare che un computer condivide un identificatore univoco di Configuration Manager con un altro computer.|  
|**Computer con indirizzi MAC duplicati**|Visualizza computer che condividono l'indirizzo MAC.|  
|**Conteggio dei computer nei domini o gruppi di lavoro della risorsa**|Visualizza il numero di computer in ogni dominio o gruppo di lavoro della risorsa.|  
|**Informazioni individuazione per un computer specifico**|Visualizza un elenco di agenti e siti che hanno individuato un computer specifico.|  
|**Date inventario per un computer specifico**|Visualizza la data e l'ora in cui è stato eseguito per l'ultima volta l'inventario in un computer specifico.|  



## <a name="site---general"></a>Sito - Generale  

I tre report seguenti sono elencati nella categoria **Sito - Generale**.

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Computer in un sito specifico**|Visualizza un elenco di computer client in un sito specifico.|  
|**Stato sito per la gerarchia**|Visualizza un elenco dei siti nella gerarchia con informazioni versione sito e stato sito.|  
|**Stato dell'aggiornamento di Configuration Manager all'interno della gerarchia**|Visualizza informazioni sugli aggiornamenti del sito di Configuration Manager per la gerarchia.|  



## <a name="site---server-information"></a>Sito - Informazioni server  

Il report seguente è elencato nella categoria **Sito - Informazioni server**.

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Ruoli sistema sito e server sistema sito per un sito specifico**|Visualizza un elenco di server di sistema del sito e i relativi ruoli del sistema del sito per un sito specifico.|  



## <a name="software---companies-and-products"></a>Software - Società e prodotti  

I 15 report seguenti sono elencati nella categoria **Software - Società e prodotti**.

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Tutti i prodotti in inventario per una società software specifica**|Visualizza un elenco di prodotti software in inventario e versioni prodotte da una società software specifica.|  
|**Tutte le società software**|Visualizza un elenco di tutte le società in inventario che producono software.|  
|**Tutte le app di Windows**|Visualizza un riepilogo delle app di Windows installate. La ricerca usa i criteri seguenti: nome dell'applicazione, architettura o editore.|  
|**Computer con un prodotto specifico**|Visualizza un elenco dei computer in cui è in inventario un prodotto specifico e le versioni del prodotto.|  
|**Computer con nome e versione prodotto specifici**|Visualizza un elenco dei computer in cui è in inventario una versione specifica di un prodotto.|  
|**Computer con software specifico registrato in Installazione applicazioni**|Visualizza un riepilogo di tutti i computer con software specifico registrato in Installazione applicazioni oppure in Programmi e funzionalità.|  
|**Conteggio dei prodotti e delle versioni in inventario**|Visualizza un elenco di prodotti e versioni software in inventario e il numero di computer su cui sono installati.|  
|**Conteggio dei prodotti e delle versioni in inventario per un prodotto specifico**|Visualizza un elenco delle versioni in inventario di un prodotto specifico e il numero di computer su cui sono installate.|  
|**Conteggio di tutte le istanze software registrate con Installazione applicazioni**|Visualizza un riepilogo di tutte le istanze software installate e registrate in Installazione applicazioni oppure in Programmi e funzionalità nei computer all'interno di una raccolta specifica.|  
|**Conteggio delle istanze software registrate in Installazione applicazioni**|Visualizza un conteggio delle istanze per pacchetti software specifici installati e registrati in Installazione applicazioni oppure in Programmi e funzionalità.|  
|**Numero di browser predefiniti**|Visualizza il numero di client con un Web browser specifico come impostazione predefinita di Windows. <br>Usare il riferimento seguente per i valori BrowserProgID più comuni:<br> - AppXq0fevzme2pys62n3e0fbqa7peapykr8v: Microsoft Edge<br> - IE.HTTP: Microsoft Internet Explorer<br> - ChromeHTML: Google Chrome<br> - OperaStable: Opera Software<br> - FirefoxURL-308046B0AF4A39CB: Mozilla Firefox<br> - Sconosciuto: il sistema operativo del client non supporta la query, la query non è stata eseguita o un utente non si è connesso|
|**Installazioni delle app di Windows specificate**|Questo report elenca tutti i computer con un'app di Windows specificata.|  
|**Prodotto in un computer specifico**|Visualizza un elenco di prodotti software in inventario e dei relativi produttori in un computer specifico.|  
|**Software registrato in Installazione applicazioni in un computer specifico**|Visualizza un riepilogo del software installato in un computer specifico registrato in Installazione applicazioni oppure in Programmi e funzionalità.|  
|**App di Windows installate per l'utente specificato**|Visualizza tutte le app di Windows installate per l'utente specificato|  



## <a name="software---files"></a>Software - File  

I cinque report seguenti sono elencati nella categoria **Software - File**.

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Tutti i file in inventario per un prodotto specifico**|Visualizza un riepilogo dei file in inventario che sono associati a un prodotto software specifico.|  
|**Tutti i file in inventario in un computer specifico**|Visualizza un riepilogo di tutti i file in inventario in un computer specifico.|  
|**Confrontare l'inventario software in due computer**|Visualizza le differenze tra gli inventari software segnalati per due computer specifici.|  
|**Computer con un file specifico**|Visualizza un elenco di computer che hanno raccolto l'inventario software per un nome file specifico. Se un computer contiene più copie del file, è possibile che venga visualizzato più di una volta nell'elenco.|  
|**Conteggio dei computer con un nome file specifico**|Visualizza il numero dei computer che hanno raccolto l'inventario software per un file specifico.|  



## <a name="software-distribution---application-monitoring"></a>Distribuzione software - Monitoraggio applicazione  

I 10 report seguenti sono elencati nella categoria **Distribuzione software - Monitoraggio applicazione**.

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Tutte le distribuzioni applicazione (avanzate)**|Visualizza informazioni di riepilogo dettagliate per tutte le distribuzioni dell'applicazione.|  
|**Tutte le distribuzioni applicazione (base)**|Visualizza informazioni di riepilogo per tutte le distribuzioni dell'applicazione.|  
|**Conformità applicazione**|Visualizza le informazioni di conformità per l'applicazione specificata all'interno della raccolta specificata.|  
|**Distribuzioni applicazione per asset**|Visualizza le applicazioni distribuite in un dispositivo o utente specificato.|  
|**Errori infrastruttura applicazione**|Visualizza gli errori di infrastruttura dell'applicazione. Questi errori includono problemi di infrastruttura interna o errori derivanti da regole di requisiti non valide.|  
|**Stato dettagliato uso applicazione**|Visualizza i dettagli di uso per le applicazioni installate.|  
|**Stato riepilogo uso applicazione**|Visualizza un riepilogo sull'uso per le applicazioni installate.|  
|**Distribuzioni sequenza attività contenenti l'applicazione**|Visualizza le distribuzioni della sequenza di attività che installano un'applicazione specifica.|  


## <a name="software-distribution---collections"></a>Distribuzione software - Raccolte  

I tre report seguenti sono elencati nella categoria **Distribuzione software - Raccolte**.

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Tutte le raccolte**|Visualizza tutte le raccolte nella gerarchia.|  
|**Tutte le risorse in una raccolta specifica**|Visualizza tutte le risorse in una raccolta specifica.|  
|**Finestre di manutenzione disponibili a un client specificato**|Visualizza tutte le finestre di manutenzione applicabili al client specificato.|  



## <a name="software-distribution---content"></a>Distribuzione software - Contenuto  

I 16 report seguenti sono elencati nella categoria **Distribuzione software - Contenuto**.

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Tutte le distribuzioni contenuto attive**|Visualizza tutti i punti di distribuzione in cui si sta installando o rimuovendo contenuto.|  
|**Tutto il contenuto**|Visualizza tutte le applicazioni e i pacchetti in un sito.|  
|**Tutto il contenuto in un punto di distribuzione specifico**|Visualizza tutto il contenuto attualmente installato in un punto di distribuzione specifico.|  
|**Tutti i punti di distribuzione**|Visualizza le informazioni sui punti di distribuzione per ogni sito.|  
|**Tutti i messaggi di stato per un pacchetto specifico in un punto di distribuzione specifico**|Visualizza tutti i messaggi di stato per un pacchetto specifico in un punto di distribuzione specifico.|  
|**Stato di distribuzione del contenuto applicazione**|Visualizza le informazioni sullo stato di distribuzione per il contenuto applicazione.|  
|**Applicazioni destinate a un gruppo di punti di distribuzione**|Visualizza le informazioni sul contenuto applicazione che è stato distribuito un gruppo di punti di distribuzione specifico.|  
|**Applicazioni non sincronizzate in un gruppo di punti di distribuzione specifico**|Visualizza le applicazioni per cui i file di contenuto associati non sono stati aggiornati con la versione più recente in un gruppo di punti di distribuzione specifico.|  
|**Gruppo di punti di distribuzione**|Visualizza le informazioni su un gruppo di punti di distribuzione specifico.|  
|**Riepilogo di uso dei punti di distribuzione**|Visualizza il riepilogo di uso dei punti di distribuzione per ogni punto di distribuzione.|  
|**Stato di distribuzione del pacchetto specificato**|Visualizza lo stato di distribuzione per il contenuto di un pacchetto specifico in ogni punto di distribuzione.|  
|**Pacchetti destinati a un gruppo di punti di distribuzione**|Visualizza le informazioni sui pacchetti destinati a un gruppo di punti di distribuzione specifico.|  
|**Pacchetti non sincronizzati in un gruppo di punti di distribuzione specifico**|Visualizza i pacchetti per cui i file di contenuto associati non sono stati aggiornati con la versione più recente in un gruppo di punti di distribuzione specifico.|  
|**Rifiuto di contenuto di origine di peer cache**|Visualizza il numero di rifiuti delle origini di peer cache per gruppo di limiti.|
|**Rifiuto di contenuto di origine di peer cache per condizione**|Visualizza le origini di peer cache che hanno rifiutato di distribuire il contenuto in base a una condizione.|
|**Dettagli del rifiuto di contenuto di origine di peer cache**|Visualizza il nome del contenuto rifiutato da un'origine peer.|



## <a name="software-distribution---package-and-program-deployment"></a>Distribuzione software - Distribuzione programma e pacchetto 

I cinque report seguenti sono elencati nella categoria **Distribuzione software - Distribuzione programma e pacchetto**.

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Tutte le distribuzioni per un pacchetto e programma specifico**|Visualizza le informazioni su tutte le distribuzioni di un pacchetto e programma specifico.|  
|**Distribuzioni di pacchetto e programma**|Visualizza tutte le distribuzioni di pacchetto e programma nel sito.|  
|**Tutte le distribuzioni di pacchetti e programmi in una collezione specifica**|Visualizza tutte le distribuzioni di pacchetti e programmi in una collezione specifica.|  
|**Tutte le distribuzioni di pacchetti e programmi in un computer specifico**|Visualizza tutte le distribuzioni di pacchetti e programmi applicabili a un computer specifico.|  
|**Tutte le distribuzioni di pacchetti e programmi a un utente specifico**|Visualizza tutte le distribuzioni di pacchetti e programmi a un utente specifico.|  



## <a name="software-distribution---package-and-program-deployment-status"></a>Distribuzione software - Stato distribuzione programma e pacchetto  

I cinque report seguenti sono elencati nella categoria **Distribuzione software - Stato distribuzione programma e pacchetto**.

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Tutte le distribuzioni di pacchetti e programmi della risorsa di sistema con stato**|Visualizza tutte le distribuzioni di pacchetti e programmi per il sito con uno stato del riepilogo di ogni distribuzione.|  
|**Tutte le risorse di sistema per una distribuzione pacchetto e programma specifica in uno stato specifico**|Visualizza un elenco di risorse in uno stato specifico per una distribuzione del pacchetto e programma specifica.|  
|**Grafico - Stato di completamento distribuzione programma e pacchetto oraria**|Visualizza la percentuale di computer in cui il pacchetto è stato installato. L'elenco è organizzato per ogni ora da quando un amministratore crea la distribuzione di pacchetto e programma. Si può usare per tenere traccia del tempo medio per una distribuzione pacchetto e programma.|  
|**Stato della distribuzione di pacchetto e programma per un client e una distribuzione specifici**|Visualizza i messaggi di stato segnalati per un computer e una distribuzione di pacchetto e programma specifici.|  
|**Stato di una distribuzione pacchetto e programma specifica**|Visualizza il riepilogo dello stato della distribuzione di un pacchetto e programma specifica.|  



## <a name="software-metering"></a>Controllo del software  

I 13 report seguenti sono elencati nella categoria **Controllo software**.

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Tutte le regole di controllo software applicate al sito**|Visualizza un elenco di tutte le regole di controllo software applicate al sito.|  
|**Computer che hanno installato un programma di controllo ma non hanno eseguito il programma da una data specificata**|Visualizza tutti i computer con l'applicazione a consumo specificata, ma in cui nessun utente ha eseguito il programma dalla data specificata.|  
|**Computer che hanno eseguito un programma di controllo software specifico**|Visualizza un elenco di computer che hanno eseguito programmi corrispondenti alla regola di controllo software specificata entro il mese e l'anno specificati.|  
|**Uso simultaneo per tutti i programmi di controllo software**|Visualizza il numero massimo di utenti che hanno eseguito simultaneamente ogni programma software a consumo durante il mese e l'anno specificati.|  
|**Analisi della tendenza di uso simultaneo di un programma di controllo software specifico**|Visualizza il numero massimo di utenti che hanno eseguito simultaneamente il programma software a consumo durante ciascun mese dell'anno passato.|  
|**Installare la base per tutti i programmi di controllo software**|Visualizza il numero di computer che hanno programmi software a consumo installati come indicato dall'inventario software. Questo report richiede la raccolta dell'inventario software da parte del computer.|  
|**Stato di riepilogo del controllo software**|Visualizza l'ora in cui sono stati elaborati i dati di controllo riepilogati più di recente nel server del sito. I report di misurazione del software riflettono solo i dati di misurazione elaborati prima di queste date.|  
|**Riepilogo di uso dell'ora del giorno per un programma di controllo software specifico**|Visualizza il numero medio di usi di un particolare programma negli ultimi 90 giorni, suddivisi per ora e giorno.|  
|**Uso totale per tutti i programmi di controllo software**|Visualizza il numero di utenti che hanno eseguito programmi entro il mese e l'anno specificati e che corrispondono a ogni regola di misurazione del software. Queste regole si applicano al software installato in locale o all'uso di Servizi terminal.|  
|**Uso totale per tutti i programmi di controllo software in Windows Terminal Server**|Visualizza il numero di utenti che hanno eseguito programmi corrispondenti a ogni regola di controllo software tramite Servizi terminal entro il mese e l'anno specificati.|  
|**Analisi della tendenza di uso totale per un programma di controllo software specifico**|Visualizza il numero di utenti che hanno eseguito programmi durante ogni mese per l'ultimo anno e che corrispondono alla regola di misurazione del software specificata. Queste regole si applicano al software installato in locale o all'uso di Servizi terminal.|  
|**Analisi della tendenza di uso totale per un programma di controllo software specifico in Windows Terminal Server**|Visualizza il numero di utenti che hanno eseguito programmi durante ogni mese per l'ultimo anno e che corrispondono alla regola di misurazione del software specificata. Queste regole sono per l'uso di Servizi terminal.|  
|**Utenti che hanno eseguito un programma di controllo software specifico**|Visualizza un elenco di utenti che hanno eseguito programmi entro il mese e l'anno specificati e che corrispondono alla regola di misurazione del software specificata.|  



## <a name="software-updates---a-compliance"></a>Aggiornamenti software - Conformità A  

Gli otto report seguenti sono elencati nella categoria **Aggiornamenti software - Conformità A**.

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Conformità 1 - Conformità generale**|Visualizza i dati di conformità generale di un gruppo di aggiornamento software.|  
|**Conformità 2 - Aggiornamento software specifico**|Visualizza i dati di conformità per un aggiornamento software specifico.|  
|**Conformità 3 - Gruppo di aggiornamenti (per aggiornamento)**|Visualizza i dati di conformità degli aggiornamenti software definiti in un gruppo di aggiornamento software.|  
|**Conformità 4 - Anno e mese degli aggiornamenti per fornitore**|Visualizza i dati di conformità per gli aggiornamenti software rilasciati da un fornitore durante un mese e un anno specificati.|  
|**Conformità 5 - Computer specifico**|Questo report restituisce i dati di conformità dell'aggiornamento software per un computer specifico. Per limitare la quantità di informazioni restituite, è possibile specificare la classificazione dell'aggiornamento software e del fornitore.|  
|**Conformità 6 - Stati specifici di aggiornamento software (secondario)**|Visualizza il numero e la percentuale di computer in ogni stato di conformità per l'aggiornamento software specificato.|  
|**Conformità 7 - Computer in uno stato di conformità specifico per un gruppo di aggiornamenti (secondario)**|Visualizza tutti i computer in una raccolta che hanno uno stato di conformità generale specificato rispetto a un gruppo di aggiornamento software.|  
|**Conformità 8 - Computer in uno stato di conformità specifico per un aggiornamento (secondario)**|Visualizza tutti i computer in una raccolta che hanno uno stato di conformità specificato per un aggiornamento software.|  
|**Conformità 9 - Dati complessivi su integrità e conformità**|Visualizza i dati complessivi relativi all'integrità e alla conformità per un gruppo di aggiornamento software. (a partire dalla versione 1806)| 


## <a name="software-updates---b-deployment-management"></a>Aggiornamenti software - Gestione distribuzione B  

Gli otto report seguenti sono elencati nella categoria **Aggiornamenti software - Gestione distribuzione B**.

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Gestione 1 - Distribuzioni di un gruppo di aggiornamenti**|Visualizza tutte le distribuzioni che includono tutti gli aggiornamenti software definiti in un gruppo di aggiornamento software specifico.|  
|**Gestione 2 - Aggiornamenti richiesti ma non distribuiti**|Visualizza tutti gli aggiornamenti software di uno specifico fornitore che i client hanno rilevato come obbligatori, ma che l'amministratore non ha distribuito a una raccolta specifica.|  
|**Gestione 3 - Aggiornamenti in una distribuzione**|Visualizza gli aggiornamenti software che sono contenuti in una distribuzione specifica.|  
|**Gestione 4 - Distribuzioni associate a una raccolta**|Visualizza tutte le distribuzioni di aggiornamenti software destinate a una raccolta specifica.|  
|**Gestione 5 - Distribuzioni associate a un computer**|Visualizza tutte le distribuzioni di aggiornamenti software distribuite in un computer specifico.|  
|**Gestione 6 - Distribuzioni che contengono un aggiornamento specifico**|Visualizza tutte le distribuzioni che includono un aggiornamento software specifico e la raccolta di destinazione associata per la distribuzione.|  
|**Gestione 7 - Aggiornamenti in una distribuzione senza contenuto**|Visualizza gli aggiornamenti software in una distribuzione specifica per i quali non è stato recuperato tutto il contenuto associato. Questo stato impedisce ai client di installare l'aggiornamento e alla distribuzione di raggiungere il 100% di conformità.|  
|**Gestione 8 - Computer senza contenuto (secondario)**|Visualizza tutti i computer che necessitano dell'aggiornamento software specificato, ma il contenuto associato non è ancora stato distribuito a un punto di distribuzione.|  



## <a name="software-updates---c-deployment-states"></a>Aggiornamenti software - Stati distribuzione C  

I sei report seguenti sono elencati nella categoria **Aggiornamenti software - Stati distribuzione C**.

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Stati 1 - Stati di imposizione per una distribuzione**|Visualizza gli stati di imposizione di una distribuzione di aggiornamento software specificata che in genere è la seconda fase della valutazione di una distribuzione.|  
|**Stati 2 - Stati di valutazione per una distribuzione**|Visualizza lo stato di valutazione di una distribuzione di aggiornamento software specificata che in genere è la prima fase della valutazione di una distribuzione.|  
|**Stati 3 - Stati per una distribuzione e un computer**|Visualizza gli stati per tutti gli aggiornamenti software nella distribuzione specificata per un computer specifico.|  
|**Stati 4 - Computer in uno stato specifico per una distribuzione (secondario)**|Visualizza tutti i computer in uno stato specifico per una distribuzione di aggiornamento software.|  
|**Stati 5 - Stati per un aggiornamento in una distribuzione (secondario)**|Visualizza un riepilogo degli stati per un aggiornamento software specifico indicato da una distribuzione specifica.|  
|**Stati 6 - Computer in uno stato di imposizione specifico per un aggiornamento (secondario)**|Visualizza tutti i computer in uno stato di applicazione specifico per un aggiornamento software specifico.|  



## <a name="software-updates---d-scan"></a>Aggiornamenti software - Analisi D  

I quattro report seguenti sono elencati nella categoria **Aggiornamenti software - Analisi D**.

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Analisi 1 - Ultimi stati di analisi per raccolta**|Specifica una raccolta per la quale visualizzare il numero di computer in ogni stato di analisi di conformità. I client restituiscono lo stato durante l'ultima analisi di conformità.|  
|**Analisi 2 - Ultimi stati di analisi per sito**|Specifica un sito per il quale visualizzare il numero di computer in ogni stato di analisi di conformità. I client restituiscono lo stato durante l'ultima analisi di conformità.|  
|**Analisi 3 - Client di una raccolta che inviano uno stato specifico (secondario)**|Visualizza tutti i computer per una raccolta specifica e uno stato di analisi di conformità specifico nel corso dell'ultima analisi di conformità.|  
|**Analisi 4 - Client di un sito che inviano uno stato specifico (secondario)**|Specifica un sito per il quale visualizzare tutti i computer con uno stato di analisi di conformità specifico. I client di restituiscono lo stato durante l'ultima analisi di conformità.|  



## <a name="software-updates---e-troubleshooting"></a>Aggiornamenti software - Risoluzione dei problemi E  

I quattro report seguenti sono elencati nella categoria **Aggiornamenti software - Risoluzione dei problemi E**.

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Risoluzione dei problemi 1 - Errori di analisi**|Visualizza gli errori di analisi nel sito e il numero di computer in cui si verifica ogni errore.|  
|**Risoluzione dei problemi 2 - Errori di distribuzione**|Visualizza gli errori di distribuzione nel sito e un conteggio dei computer in cui si stanno verificando gli errori.|  
|**Risoluzione dei problemi 3 - Computer in cui si verificano errori di scansione specifici (secondario)**|Visualizza l'elenco dei computer in cui non è possibile eseguire l'analisi a causa di un errore specifico.|  
|**Risoluzione dei problemi 4 - Computer in cui si verificano errori di distribuzione specifici (secondario)**|Visualizzare l'elenco dei computer in cui non è possibile eseguire la distribuzione dell'aggiornamento a causa di un errore specifico.|  



## <a name="state-migration"></a>Migrazione stato  

I tre report seguenti sono elencati nella categoria **Migrazione stato**.

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Informazioni di migrazione dello stato per un computer di origine specifico**|Visualizza le informazioni di migrazione dello stato per un computer specifico.|  
|**Informazioni di migrazione stato per un punto di migrazione dello stato specifico**|Visualizza le informazioni di migrazione stato per un punto di migrazione dello stato specifico.|  
|**Punti di migrazione stato per un sito specifico**|Visualizza i punti di migrazione stato per un sito specifico.|  



## <a name="status-messages"></a>Messaggi di stato  

I 12 report seguenti sono elencati nella categoria **Messaggi di stato**.

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Tutti i messaggi per un ID messaggio specifico**|Visualizza un elenco di messaggi di stato con un ID messaggio specifico.|  
|**Client che hanno inviato errori nelle ultime 12 ore per un sito specifico**|Visualizza un elenco di computer e componenti che hanno inviato errori nelle ultime 12 ore e il numero di errori restituiti.|  
|**Messaggi componente per le ultime 12 ore**|Visualizza un elenco di messaggi componente per le ultime 12 ore per un codice sito, computer e componente specifico.|  
|**Messaggi componente per l'ultima ora**|Visualizza un elenco di messaggi di stato creati nell'ultima ora da un componente specifico in un computer specifico in un sito specifico.|  
|**Conteggio messaggi componente nell'ultima ora per un computer specifico**|Visualizza il numero di messaggi di stato per componente e gravità riportata nell'ultima ora in un singolo sito specificato.|  
|**Conteggio errori nelle ultime 12 ore**|Visualizza il numero di messaggi di stato di errore componente server nelle ultime 12 ore.|  
|**Errori irreversibili (per componente)**|Visualizza un elenco di computer che hanno riportato errori irreversibili per componente.|  
|**Errori irreversibili (per nome computer)**|Visualizza un elenco di computer che hanno riportato errori irreversibili per nome computer.|  
|**Ultimi 1.000 messaggi per un computer specifico (errori e avvisi)**|Visualizza un riepilogo degli ultimi 1.000 messaggi di stato errore e avviso componente per un computer specifico.|  
|**Ultimi 1.000 messaggi per un computer specifico (errori avvisi e informazioni)**|Visualizza un riepilogo degli ultimi 1.000 messaggi di stato errore, avviso e informativi sul componente per un computer specifico.|  
|**Ultimi 1.000 messaggi per un computer specifico (errori)**|Visualizza un riepilogo degli ultimi 1.000 messaggi di stato errore componente server per un computer specifico.|  
|**Ultimi 1.000 messaggi per un componente server specifico**|Visualizza un riepilogo dei 1.000 messaggi di stato più recenti per un componente server specifico.|  



## <a name="status-messages---audit"></a>Messaggi di stato - Controllo  

I tre report seguenti sono elencati nella categoria **Messaggi di stato - Controllo**.

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Tutti i messaggi di controllo per un utente specifico**|Visualizza un riepilogo di tutti i messaggi di stato di controllo per un utente specifico. I messaggi di controllo descrivono le azioni eseguite nella console di Configuration Manager che aggiungono, modificano o eliminano oggetti in Configuration Manager.|  
|**Controllo remoto - Tutti i computer sotto controllo remoto da un utente specifico**|Visualizza un riepilogo dei messaggi di stato che indicano il controllo remoto dei computer client per utente specificato.|  
|**Controllo remoto - Tutte le informazioni sul controllo remoto**|Visualizza un riepilogo dei messaggi di stato correlati al controllo remoto dei computer client.|  



## <a name="task-sequence---deployment-status"></a>Sequenza attività - Stato distribuzione  

Gli 11 report seguenti sono elencati nella categoria **Sequenza attività - Stato distribuzione**.

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Tutte le risorse di sistema per una distribuzione sequenza attività in uno stato specifico**|Visualizza un elenco dei computer di destinazione per la distribuzione sequenza attività specificata in uno stato di distribuzione specificato.|  
|**Tutte le risorse di sistema per una distribuzione sequenza attività che si trova in uno stato specifico ed è disponibile ai computer sconosciuti**|Visualizza un elenco dei computer di destinazione per la distribuzione sequenza attività specificata che si trova nello stato di distribuzione specificato.|  
|**Conteggio delle risorse di sistema che hanno delle distribuzioni sequenza attività assegnate ma non ancora eseguite**|Visualizza il numero di computer che hanno accettato le sequenze attività, ma la sequenza di attività non è stata eseguita.|  
|**Cronologia di una distribuzione sequenza attività in un computer**|Visualizza lo stato di ogni passaggio della distribuzione sequenza attività specificata nel computer di destinazione specificato. Se non viene restituito alcun record, la sequenza attività non è stata avviata nel computer.|  
|**Elenco di computer che hanno superato una durata specifica per eseguire una distribuzione sequenza attività**|Visualizza l'elenco dei computer di destinazione che hanno superato la durata specificata per eseguire una sequenza attività.|  
|**Tempo di esecuzione per una distribuzione sequenza attività specifica in un computer di destinazione specifico**|Visualizza il tempo totale necessario per completare una sequenza attività specificata in un computer di destinazione specificato.|  
|**Tempo di esecuzione per ogni passaggio della distribuzione sequenza attività in un computer di destinazione specifico**|Visualizza il tempo necessario per completare ogni passaggio della distribuzione sequenza attività specificata nel computer di destinazione specificato.|  
|**Stato di una distribuzione sequenza attività specifica per un computer specifico**|Visualizza il riepilogo dello stato di una distribuzione sequenza attività specificata in un computer specificato.|  
|**Stato di una distribuzione della sequenza attività in un computer di destinazione sconosciuto**|Visualizza lo stato della distribuzione sequenza attività specificata nel computer di destinazione sconosciuto specificato.|  
|**Riepilogo di stato di una distribuzione sequenza attività specifica**|Visualizza un riepilogo dello stato di tutte le risorse che sono state usate come destinazione da una distribuzione.|  
|**Riepilogo di stato di una distribuzione sequenza attività specifica disponibile ai computer sconosciuti**|Visualizza il riepilogo dello stato di tutte le risorse di destinazione della distribuzione specificata che è disponibile per una raccolta contenente computer sconosciuti.|  



## <a name="task-sequence---deployments"></a>Sequenza attività - Distribuzioni  

Gli 11 report seguenti sono elencati nella categoria **Sequenza attività - Distribuzioni**.

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Tutte le risorse di sistema attualmente in un gruppo o fase specifici di una distribuzione sequenza attività specificata**|Visualizza un elenco di computer che sono attualmente in esecuzione in una fase o in un gruppo specifici di una distribuzione sequenza attività specificata.|  
|**Tutte le risorse di sistema in cui una distribuzione di sequenza attività ha riportato errori in un gruppo o in una fase specifici**|Visualizza un elenco di computer che hanno riportato errori in una fase o in un gruppo specifici della distribuzione sequenza attività specificata.|  
|**Tutte le distribuzioni di sequenza attività**|Visualizza i dettagli di tutte le distribuzioni sequenza attività inizializzate dal sito corrente.|  
|**Tutte le distribuzioni di sequenza attività disponibili nei computer sconosciuti**|Visualizza i dettagli di tutte le distribuzioni di sequenza di attività avviate dal sito e distribuite alle raccolte che contengono computer sconosciuti.|  
|**Numero di errori in ogni fase o gruppo di una sequenza attività specifica**|Visualizza il numero di errori in ogni fase o gruppo della sequenza attività specifica.|  
|**Numero di errori in ogni fase o gruppo di una distribuzione sequenza attività specifica**|Visualizza il numero di errori in ogni fase o gruppo della distribuzione sequenza attività specifica.|  
|**Stato di distribuzione di tutte le distribuzioni sequenza attività**|Visualizza lo stato generale di tutte le distribuzioni sequenza attività.|  
|**Stato di una sequenza attività in esecuzione**|Visualizza lo stato della sequenza attività specificata.|  
|**Stato di una distribuzione della sequenza attività in esecuzione**|Visualizza le informazioni di riepilogo per la distribuzione della sequenza attività specificata.|  
|**Stato di tutte le distribuzioni per una sequenza attività specifica**|Visualizza lo stato di tutte le distribuzioni per la sequenza attività specificata.|  
|**Report di riepilogo per una distribuzione sequenza attività**|Visualizza le informazioni di riepilogo per la distribuzione della sequenza attività specificata.|  



## <a name="task-sequence---progress"></a>Sequenza attività - Progresso  

I cinque report seguenti sono elencati nella categoria **Sequenza attività - Progresso**.

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Grafico - Avanzamento settimanale di una sequenza attività**|Visualizza l'avanzamento settimanale di una sequenza attività iniziando dal giorno della prima distribuzione.|  
|**Stato di una sequenza attività**|Visualizza lo stato della sequenza attività specificata.|  
|**Avanzamento di tutte le sequenze attività**|Visualizza un riepilogo dello stato di tutte le sequenze attività.|  
|**Avanzamento delle sequenze attività per le distribuzioni del sistema operativo**|Visualizza l'avanzamento di tutte le sequenze attività che distribuiscono sistemi operativi.|  
|**Stato di tutti i computer sconosciuti**|Visualizza un elenco dei computer che erano sconosciuti nel momento in cui hanno eseguito una distribuzione di sequenza di attività e indica se ora sono computer noti.|  



## <a name="task-sequences---references"></a>Sequenza attività - Riferimenti  

Il report seguente è elencato nella categoria **Sequenza attività - Riferimenti**.

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Contenuto a cui fa riferimento una sequenza attività specifica**|Visualizza il contenuto a cui fa riferimento una sequenza attività specifica.|  



<!--
## Upgrade Assessment  
The following 11 reports are listed under the **Upgrade Assessment** category.

|Report name|Description|  
|-----------------|-----------------|  
|**Application status for a specific computer**|Displays the compatibility of applications that are installed on a computer for a specified operating system.|  
|**Application status for computers in a specific collection**|Displays the overall status for computers in a collection to let you assess them for upgrade to a specified operating system based on the applications on each computer. Use this report to determine which computers have compatible applications before you deploy an operating system.|  
|**Application status summary**|Displays a summary of the application status for a specified operating system. Use this report to determine application compatibility before you deploy an operating system.|  
|**Computers with a specific application installed**|Displays computers with a specified application installed.|  
|**Computers with a specific hardware device**|Displays computers that have a specific hardware device.|  
|**Hardware device status for a specific computer**|Displays the compatibility status of hardware devices for a specified operating system that are found on a specified computer.|  
|**Hardware device status for computers in a specific collection**|Displays the overall status for hardware devices for a specified operating system for computers in a specified collection. Use this report to determine hardware compatibility before you deploy an operating system.|  
|**Hardware device status summary**|Displays a summary of hardware device status for a specified operating system. You can use this report to determine hardware device compatibility before you deploy an operating system.|  
|**Operating system hardware requirements**|Displays the minimum and recommended hardware criteria for operating systems.|  
|**Operating system requirement status for computers in a specific collection**|Displays the status of operating system requirements for the specified operating system for computers in a specified collection. Use this report to determine if a computer meets the specified operating system requirements for CPU processor speed, memory size, and hard disk space.|  
|**Upgrade assessment summary**|Displays the upgrade assessment summary. You can use this report to assess the overall status for upgrade compatibility.|  
-->



## <a name="user---device-affinity"></a>Utente - Affinità dispositivo  

I due report seguenti sono elencati nella categoria **Utente - Affinità dispositivo**.

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Associazioni affinità-utente dispositivo in sospeso per raccolta**|Questo report mostra tutte le assegnazioni affinità utente dispositivo basate sui dati di uso per i membri di una raccolta.|  
|**Associazioni affinità-utente dispositivo per raccolta**|Visualizza tutte le associazioni dispositivo utente per la raccolta specificata e raggruppa i risultati per tipo di raccolta, ad esempio utente o dispositivo.|  



## <a name="user-data-and-profiles-health"></a>Integrità profili e dati utente  

I quattro report seguenti sono elencati nella categoria **Integrità profili e dati utente**.

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Rapporto di stato di indirizzamento cartelle - Dettagli**|Visualizza i dettagli dello stato di integrità del reindirizzamento cartelle per ognuna delle cartelle reindirizzate per un utente specifico.|  
|**Rapporto di stato di profili utente mobili - Dettagli**|Visualizza i dettagli dello stato di integrità del profilo utente mobile per un utente specifico.|  
|**Rapporto di stato di profili e dati utente - Dettagli**|Visualizza i dettagli di errore o avviso del reindirizzamento cartelle o dei profili utente mobile. Questo report è la destinazione dei dettagli dal report di riepilogo.|  
|**Rapporto di stato di profili e dati utente - Riepilogo**|Visualizza il riepilogo degli stati di integrità per il reindirizzamento cartelle e i profili utente mobili.|  



## <a name="users"></a>Utenti  

I tre report seguenti sono elencati nella categoria **Utenti**.

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Computer per un nome utente specifico**|Visualizza l'elenco dei computer usati da un utente specifico.|  
|**Conteggio utenti per dominio**|Visualizza il numero di utenti in ciascun dominio.|  
|**Utenti in un dominio specifico**|Visualizza un elenco di utenti e relativi computer in un dominio specifico.|  



## <a name="virtual-applications"></a>Applicazioni virtuali  

I sette report seguenti sono elencati nella categoria **Applicazioni virtuali**.

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Risultati ambiente virtuale App-V**|Visualizza le informazioni su un ambiente virtuale specifico che si trova in uno stato specifico per una raccolta specifica.|  
|**Risultati ambiente virtuale App-V per asset**|Visualizza informazioni su un ambiente virtuale specifico per un asset specifico. Indica inoltre i tipi di distribuzione per l'ambiente virtuale specifico.|  
|**Stato ambiente virtuale App-V**|Visualizza informazioni di conformità per un ambiente virtuale specifico per una raccolta specifica.|  
|**Computer con un'applicazione virtuale specifica**|Visualizza il riepilogo dei computer che dispongono del collegamento applicazione App-V creato usando Application Virtualization Management Sequencer.|  
|**Computer con un pacchetto applicazione virtuale specifico**|Visualizza il riepilogo dei computer con il pacchetto dell'applicazione App-V specificato.|  
|**Conteggio di tutte le istanze delle applicazioni virtuali**|Visualizza il conteggio dei pacchetti applicazione App-V rilevati.|  
|**Conteggio di tutte le istanze delle applicazioni virtuali**|Visualizza il conteggio delle applicazioni App-V rilevate.|  



## <a name="vulnerability-assessment"></a>Valutazione della vulnerabilità

Il report seguente è elencato nella categoria **Valutazione della vulnerabilità**.

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Report generale sulla valutazione della vulnerabilità**|Identifica le vulnerabilità correlate all'amministrazione, alla sicurezza e alla conformità di un computer specifico.|  



## <a name="wake-on-lan"></a>Riattivazione LAN  

I sette report seguenti sono elencati nella categoria **Riattivazione LAN**.

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Tutti i computer usati come destinazione per l'attività riattivazione LAN**|Specifica il tipo di distribuzione per visualizzare un elenco di computer di destinazione dell'attività riattivazione LAN.|  
|**Tutti gli oggetti che hanno delle attività di riattivazione in sospeso**|Visualizza gli oggetti che sono pianificati per la riattivazione.|  
|**Tutti i siti che sono abilitati per la riattivazione LAN**|Visualizza un elenco di tutti i siti nella gerarchia che sono abilitati per la riattivazione LAN.|  
|**Errori ricevuti durante l'invio dei pacchetti di riattivazione per un periodo definito**|Visualizza gli errori ricevuti durante l'invio dei pacchetti di riattivazione ai computer per un periodo definito.|  
|**Cronologia dell'attività di riattivazione LAN**|Visualizza una cronologia delle attività di riattivazione eseguite dopo un determinato periodo.|  
|**Dettagli dello stato della distribuzione del proxy di riattivazione**|Visualizza informazioni sullo stato della distribuzione del proxy di riattivazione per ciascun dispositivo di una raccolta specifica.|  
|**Riepilogo dello stato della distribuzione del proxy di riattivazione**|Visualizza un riepilogo dello stato della distribuzione del proxy di riattivazione di una raccolta specificata.|  
