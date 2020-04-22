---
title: Client Spy
titleSuffix: Configuration Manager
description: Usare Client Spy per risolvere i problemi relativi a distribuzione software, inventario e misurazione del software nei client Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 60575413-44fe-43bb-bcfb-39ec5ed5055b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 43c3d0f25cf9a71bf07189315ee5f11eba47de1d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707909"
---
# <a name="client-spy"></a>Client Spy

*Si applica a: Configuration Manager (Current Branch)*

Client Spy è uno [strumento di Configuration Manager](tools.md). È uno strumento per la risoluzione dei problemi relativi a distribuzione software, inventario e misurazione del software nei client Configuration Manager. 

La maggior parte delle informazioni recuperate dallo strumento è relativa alle distribuzioni software:
- Tutte le distribuzioni software correnti 
- Cronologia delle distribuzioni software
- Configurazione della cache del client
- Elementi memorizzati nella cache
- Distribuzioni necessarie in sospeso
- Distribuzioni disponibili  

Visualizza anche le informazioni seguenti sull'inventario
- Data dell'ultimo ciclo di inventario
- Data dell'ultimo report
- Versione principale e secondaria dell'inventario software
- Raccolta file
- Inventario hardware
- Raccolta IDMIF
- Record dei dati di individuazione (DDR) 

Vengono visualizzate anche le regole di misurazione del software. 

> [!Note]   
> Per migliorare le prestazioni, lo strumento raccoglie informazioni per ogni scheda solo quando la si seleziona. Analogamente, quando si fa clic su **Aggiorna**, aggiorna solo le informazioni della scheda attualmente visualizzata.



## <a name="usage"></a>Utilizzo


### <a name="tools-menu"></a>Menu Strumenti

Nel menu **Strumenti** sono disponibili le azioni seguenti:  

#### <a name="connect"></a>Connessione
Recuperare informazioni da un computer diverso.  

- Per impostazione predefinita, lo strumento visualizza le informazioni dal computer corrente. 

- Connettersi usando il nome computer remoto, il nome utente e la password per l'account. Lo strumento stabilisce una connessione alla condivisione IPC$ nel computer remoto. Elimina la connessione quando lo strumento viene chiuso o ci si connette a un altro computer.  

- Per ottenere le informazioni, è necessario un account con credenziali sufficienti.  

- Se non si specificano nome utente e password, Client Spy usa il contesto di protezione dell'utente attualmente connesso per provare a stabilire la connessione.  

- Quando ci si connette a un computer remoto, tutte le schede visualizzate mostrano informazioni dal computer remoto.

#### <a name="software-distribution"></a>Distribuzione del software
Visualizza le schede [Distribuzione software](#software-distribution) e nasconde le altre schede. Per impostazione predefinita, Client Spy visualizza le schede Distribuzione software.

#### <a name="inventory"></a>Argomento
Visualizza la scheda Inventario e nasconde le altre schede.

#### <a name="software-metering"></a>Controllo software
Visualizza la scheda Controllo del software e nasconde le altre schede.

#### <a name="save-current-tab-to-file"></a>Save current tab to file (Salva scheda corrente in un file)
Salva le informazioni della scheda attualmente visualizzata in un file di testo specificato. 

#### <a name="save-all-tabs-to-file"></a>Save all tabs to file (Salva tutte le schede in un file)
Salva le informazioni di tutte le schede in un file di testo specificato. Salva solo le informazioni che possono essere visualizzare dall'account.



## <a name="software-distribution-tab"></a>Scheda Distribuzione software

Configurare le impostazioni nelle quattro schede seguenti:
- [Software Distribution Execution Requests](#bkmk_exec-requests) (Richieste di esecuzione della distribuzione software)
- [Software Distribution History](#bkmk_history) (Cronologia delle distribuzioni software)
- [Software Distribution Cache Information](#bkmk_cache-info) (Informazioni sulla cache di distribuzione software)
- [Software Distribution Pending Executions](#bkmk_pending-exec) (Esecuzioni in sospeso di distribuzione software)


### <a name="software-distribution-execution-requests"></a><a name="bkmk_exec-requests"></a> Software Distribution Execution Requests (Richieste di esecuzione della distribuzione software)

Questa scheda visualizza tutte le distribuzioni esistenti, incluse le distribuzioni indirizzate a dispositivi e a utenti.

Ogni elemento dell'albero nella scheda Software Distribution Execution Requests (Richieste di esecuzione della distribuzione software) contiene i quattro attributi seguenti:
- ID annuncio. Questo valore potrebbe essere vuoto, se si tratta di una distribuzione disponibile. 
- ID del pacchetto 
- Nome programma 
- Utente. Potrebbe essere il SID dell'utente designato o il SID dell'utente che ha avviato la richiesta. Se entrambe sono richieste di sistema, l'utente visualizzato è il sistema. 

Per ogni richiesta eseguita, visualizza anche le informazioni seguenti in una struttura a sottoalbero:
- Nome programma 
- ID del pacchetto 
- Nome pacchetto 
- Request Creation Time 
- Stato 
- Running State, se State è Running 
- Execution Context (User o Admin) 
- History State (Success, Failure o NotRun) 
- LastRunTime (Never, se il programma non è stato eseguito prima) 
- RetryCount, se State è WaitingRetry 
- ContentAccess (Retry Count, se State è WaitingRetry) 
- FailureCode, se State è WaitingRetry 
- FailureReason, se State è WaitingRetry 

Se per la richiesta è necessario un contenuto, lo stato è WaitingContent. La scheda Software Distribution Cache Information (Informazioni sulla cache di distribuzione software) visualizza i dettagli di questa richiesta di distribuzione.

Se la richiesta eseguita è una richiesta di download, visualizza anche il numero di byte scaricati.

> [!Note]   
> Usa icone diverse a seconda dello stato di una richiesta eseguita.


### <a name="software-distribution-history"></a><a name="bkmk_history"></a> Software Distribution History (Cronologia delle distribuzioni software)

Questa scheda contiene informazioni su tutti i programmi eseguiti in precedenza. Queste informazioni vengono archiviate nel Registro di sistema.

I rami principali di questo albero sono le diverse cronologie utente, tra cui quella di sistema. Visualizza un sottoalbero contenente l'elenco di pacchetti da cui i programmi sono stati eseguiti per ogni utente. 

L'ID del pacchetto e il nome del pacchetto per ogni sottoalbero di pacchetti visualizzano un elenco dei programmi eseguiti. Per ognuno visualizza gli attributi seguenti: 
- Nome programma
- Run state (Stato dell'esecuzione)
- Last run time (Data e ora ultima esecuzione)
- Failure code (Codice di errore)
- Failure reason (Motivo dell'errore)  

Il codice errore e il motivo dell'errore sono vuoti quando un programma è stato eseguito correttamente.


### <a name="software-distribution-cache-information"></a><a name="bkmk_cache-info"></a> Software Distribution Cache Information (Informazioni sulla cache di distribuzione software)

#### <a name="cache-config"></a>Cache Config (Configurazione cache)
Contiene informazioni sulla cache del client Configuration Manager. Queste informazioni includono il percorso della cache, le dimensioni della cache e se è attualmente in uso. 

#### <a name="cached-items"></a>Cached Items (Elementi memorizzati nella cache)
Contiene un sottoalbero di tutti gli elementi attualmente nella cache. Ogni elemento dell'albero include le informazioni seguenti su ogni elemento: 
- La posizione dell'elemento (cartella) nella cache
- Stato corrente
- ID del pacchetto
- Nome pacchetto
- Versione pacchetto
- Dimensione pacchetto
- Conteggio riferimenti correnti
- Ultima ora di riferimento (UTC)  

#### <a name="downloading-items"></a>Downloading Items (Elementi di download)
Si tratta degli elementi che il client sta attualmente scaricando. Per ognuno sono indicate le stesse informazioni visualizzate per gli elementi nella cache e il numero di kilobyte scaricati. 


### <a name="software-distribution-pending-executions"></a><a name="bkmk_pending-exec"></a> Software Distribution Pending Executions (Esecuzioni in sospeso di distribuzione software)

Questa scheda contiene informazioni che illustrano in dettaglio le distribuzioni necessarie passate e future e un elenco delle distribuzioni disponibili.

Ogni ramo dell'albero corrisponde a un account utente con le distribuzioni disponibili, incluse quelle di sistema.

Per ogni utente, un sottoalbero contiene i tre elementi seguenti:  

#### <a name="mandatory-advertisements-with-future-executions"></a>Mandatory Advertisements With Future Executions (Annunci obbligatori con esecuzioni future)
Si tratta di annunci obbligatori per cui rimangono ancora programmi da eseguire. Possono essere annunci con pianificazioni ricorrenti, monouso o multiple. Per ognuno sono visualizzati l'ID dell'annuncio, l'ora di esecuzione successiva e la pianificazione in base a cui viene eseguito l'annuncio. 

#### <a name="optional-advertisements"></a>Optional Advertisements (Annunci facoltativi)
Visualizza un elenco di tutti gli annunci pubblicati. Per ognuno visualizza anche dettagli quali nome del pacchetto, nome del programma e ID dell'annuncio. 

#### <a name="past-mandatory-advertisements-with-no-future-scheduled-executions"></a>Past Mandatory Advertisements With No Future Scheduled Executions (Annunci passati obbligatori senza esecuzioni future pianificate)
Si tratta di un elenco di annunci esistenti nel client che non hanno programmi futuri pianificati da eseguire. Vengono visualizzati l'ID dell'annuncio, il nome del pacchetto e il nome del programma. Viene visualizzato un elemento del sottoalbero per tutti gli annunci facoltativi.

> [!Note]  
> Le informazioni sul nome del pacchetto sono disponibili solo per i pacchetti a cui sono associati criteri annunciati nel computer visualizzato. Per i pacchetti a cui non sono più associati criteri disponibili viene visualizzato il messaggio "Package Name No Longer Available" (Nome pacchetto non più disponibile).  



## <a name="inventory-tab"></a>Scheda Inventory

Le informazioni sull'inventario sono contenute in una sola scheda. L'albero principale contiene i cinque elementi seguenti:  

- **Inventario software**: contiene la data in cui è stato avviato l'ultimo ciclo, la data dell'ultimo report e le versioni principale e secondaria dell'ultimo report.  

- **File collection** (Raccolta file): contiene la data in cui è stato avviato l'ultimo ciclo, la data dell'ultimo report e le versioni principale e secondaria dell'ultimo report.  

- **Inventario hardware**: contiene la data in cui è stato avviato l'ultimo ciclo, la data dell'ultimo report e le versioni principale e secondaria dell'ultimo report.  

- **IDMIF Collection** (Raccolta IDMF): contiene la data in cui è stato avviato l'ultimo ciclo, la data dell'ultimo report e le versioni principale e secondaria dell'ultimo report.  

- **DDR**: contiene la data in cui è stato avviato l'ultimo ciclo, la data dell'ultimo report e le versioni principale e secondaria dell'ultimo report. Le informazioni DDR vengono visualizzate anche in un sottoalbero.



## <a name="software-metering-tab"></a>Scheda Controllo del software

Questa scheda visualizza le informazioni come sottoalbero e include tutte le regole di misurazione del software. Visualizza ogni regola come nodo, identificato dal nome file e dall'ID della regola. Espandere ogni nodo nell'albero e visualizzare le informazioni seguenti:
- Nome file di Explorer 
- Nome file originale
- ID regola
- Versione file
- Language


