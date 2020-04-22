---
title: CMTrace
titleSuffix: Configuration Manager
description: Informazioni su come usare lo strumento CMTrace per visualizzare i file di log per Configuration Manager.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6a4a3290-5228-4871-918a-554aa1c20834
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8c9c42dcd1e6a6a4ca064953f0513157f5ebb228
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707899"
---
# <a name="cmtrace"></a>CMTrace

*Si applica a: Configuration Manager (Current Branch)*

CMTrace è uno [strumento di Configuration Manager](tools.md). Consente di visualizzare e monitorare i file, inclusi i tipi seguenti:  

- File di log in formato Configuration Manager o Client Component Manager (CCM)  

- File di testo normale ASCII o Unicode, ad esempio log di Windows Installer  

Lo strumento consente di analizzare i file di log tramite evidenziazione, filtri e ricerca di errori.

A partire dalla versione 1806, lo strumento per la visualizzazione di log CMTrace viene installato automaticamente insieme al client Configuration Manager. Viene aggiunto alla directory di installazione del client, che per impostazione predefinita è `%WinDir%\CCM\CMTrace.exe`.<!--1357971-->

> [!Note]  
> CMTrace non viene registrato automaticamente in Windows per l'apertura dei file con estensione log. Per altre informazioni, vedere [Associazioni di file](#file-associations).  

A partire dalla versione 1906 **OneTrace** è un nuovo visualizzatore log del Supporto tecnico. Funziona in modo analogo a CMTrace, con miglioramenti. Per altre informazioni, vedere [Supporto tecnico OneTrace](support-center-onetrace.md).

## <a name="usage"></a>Utilizzo

Eseguire **CMTrace.exe**. La prima volta che si esegue lo strumento, viene visualizzato un prompt per l'associazione del file. Per altre informazioni, vedere [Associazioni di file](#file-associations).

La maggior parte delle azioni in CMTrace viene eseguita dai menu seguenti:

- [File](#file-menu)
- [Strumenti](#tools-menu)

### <a name="file-menu"></a>Menu File

Nel menu **File** sono disponibili le azioni seguenti:  

- [Apri](#open)
- [Open on Server](#open-on-server) (Apri nel server)
- [Stampa](#print)
- [Preferenze](#preferences)

Il menu File elenca anche gli otto file più recenti. Per riaprire rapidamente uno di questi log, selezionarlo dal menu File.

#### <a name="open"></a>Open

Visualizza la finestra di dialogo Apri per cercare un file di log.

Filtrare la vista per cercare i tipi di file seguenti:

- File di log (\*.log)  
- File di log obsoleti (\*.lo_)
- Tutti i file (\*.\*)

Per impostazione predefinita, le due opzioni seguenti non sono selezionate:  

- **Ignore existing lines** (Ignora righe esistenti): se questa opzione è selezionata, CMTrace ignora i contenuti esistenti del file di log selezionato e visualizza solo le nuove righe quando vengono aggiunte. Usare questa opzione per monitorare solo le nuove azioni quando non è necessaria la cronologia completa del file di log.  

- **Merge selected files** (Unisci file selezionati): se si abilita questa opzione e si selezionano più file di log, CMTrace unisce i log selezionati nella visualizzazione. Li visualizza come se fossero un unico file di log. Il log unito viene aggiornato allo stesso modo e supporta tutte le altre funzionalità di CMTrace come se fosse un unico file di log.  

#### <a name="open-on-server"></a>Open on Server (Apri nel server)

Esplorare la cartella dei log di Configuration Manager in un computer di sistema del sito con la finestra di dialogo Sfoglia. È anche possibile cercare un computer remoto in rete.

Quando si seleziona un computer remoto da esplorare, CMTrace cerca la condivisione di Configuration Manager. Se non riesce a trovare una condivisione con i file di log di Configuration Manager, viene visualizzato un messaggio di errore.  

Per connettersi direttamente a un computer noto senza esplorazione, usare l'azione [Apri](#open), quindi immettere un nome del server e una condivisione usando il formato UNC.

#### <a name="print"></a>Stampa

Visualizzare la finestra di dialogo Stampa di Windows standard. Questa azione invia il file di log corrente a una stampante. Formatta l'output in base alle impostazioni della scheda Stampa delle preferenze di CMTrace.

#### <a name="preferences"></a>Preferenze

Configurare le impostazioni per CMTrace. Sono disponibili le seguenti opzioni:  

- Scheda**Generale**  

    - **Update Interval** (Intervallo di aggiornamento): controlla la frequenza con la quale CMTrace controlla la presenza di modifiche nei file di log e carica le nuove righe. Per impostazione predefinita, questo valore è impostato su 500 millisecondi.  

    - **Highlight (Evidenziazione)** : imposta il colore usato da CMTrace per evidenziare le righe dei log scelte. Per impostazione predefinita, questo colore è il giallo di base (rosso: 255, verde: 255, blu: 0).  

    - **Columns** (Colonne): consente di configurare le colonne visibili nella visualizzazione dei log e l'ordine in cui vengono visualizzate. Per impostazione predefinita, visualizza Log Text, Component, Date/Time e Thread.  

- Scheda **Stampa**  

    - **Columns** (Colonne): consente di configurare le colonne usate nella stampa dei file di log e l'ordine in cui vengono visualizzate. Per impostazione predefinita, le colonne vengono stampate così come sono visualizzate.  

    - **Orientation** (Orientamento): consente di impostare l'orientamento di stampa predefinito per la stampa dei file di log. Eseguire l'override di questa impostazione nella finestra di dialogo Stampa. Per impostazione predefinita, usa l'orientamento verticale.  

- Scheda **Avanzate**  

    - **Refresh Interval** (Intervallo di aggiornamento): forza CMTrace ad aggiornare la visualizzazione dei log in base a un intervallo specificato durante il caricamento di un numero elevato di righe. Per impostazione predefinita, questa opzione è disabilitata con un valore pari a zero.  

        > [!Note]  
        > In generale non modificare l'**intervallo di aggiornamento**. Può aumentare notevolmente la quantità di tempo necessaria per aprire i file di log di grandi dimensioni.

### <a name="tools-menu"></a>Menu Strumenti

Nel menu **Strumenti** sono disponibili le azioni seguenti:

- [Trova](#find)
- [Trova successivo](#find-next)
- [Copia negli Appunti](#copy-to-clipboard)
- [Highlight](#highlight) (Evidenzia)
- [Filtro](#filter)
- [Error lookup](#error-lookup) (Ricerca errori)
- [Sospendi](#pause)
- [Show/Hide Details](#showhide-details) (Mostra/Nascondi dettagli)
- [Show/Hide Info Pane](#showhide-info-pane) (Mostra/Nascondi riquadro informazioni)

#### <a name="find"></a>Trova

Cercare nel file di log aperto una stringa di testo specificata.  

#### <a name="find-next"></a>Trova successivo

Trova la stringa corrispondente successiva, specificata in precedenza nella finestra di dialogo Trova.  

#### <a name="copy-to-clipboard"></a>Copia negli Appunti

Copia le righe selezionate come testo normale negli Appunti di Windows. Se si stanno esaminando file di log di Configuration Manager e CCM, copia le colonne nello stesso ordine della vista. Separa ogni colonna con un carattere di tabulazione. Usare questa azione quando si copiano i log in messaggi di posta elettronica o in altri documenti.  

#### <a name="highlight"></a>Highlight (Evidenzia)

Immettere una stringa usata da CMTrace per cercare il testo di ogni voce di log. Viene quindi evidenziato ogni testo del log che corrisponde alla stringa immessa.  

- L'evidenziazione usa il colore specificato nelle preferenze.  

- Per disattivare l'evidenziazione, cancellare la stringa da questo campo.  

- Se si immette un numero decimale o esadecimale, CMTrace prova ad associare il valore alla colonna Thread. Usare questo comportamento per evidenziare l'elaborazione di un singolo thread, senza filtrare gli altri thread che potrebbero interagire con esso.  

- Per confrontare le stringhe in base alle lettere maiuscole e minuscole, abilitare l'opzione **Maiuscole/minuscole**.  

#### <a name="filter"></a>Filtro

Visualizzare o nascondere le righe del log in base ai criteri specificati. Applicare i filtri a qualsiasi delle quattro colonne indipendentemente dal fatto che siano visibili. Queste impostazioni si applicano a ogni file di log aperto.

Esempi:
<!--SCCMDocs issue #603-->

- Filtrare **smsts.log** in base al testo delle voci contenente "the action" o "the group".
- Filtrare **InventoryAgent.log** in base al testo delle voci contenente "destination".

#### <a name="error-lookup"></a>Error lookup (Ricerca errori)

Digitare o incollare un codice errore in formato decimale o esadecimale per visualizzare una descrizione. Alcune origini di errore possibili sono: Windows, WMI o Winhttp.

#### <a name="pause"></a>Sospendi

Sospendere o riavviare il monitoraggio dei log. I casi d'uso seguenti sono alcuni dei possibili motivi per usare questa azione:  

- Quando CMTrace visualizza troppo velocemente le informazioni dei file di log  

- Quando si sospende il monitoraggio dei log, le informazioni visualizzate da CMTrace non vanno perse se viene eseguito il rollover del file corrente in un nuovo log  

- Quando si vuole evitare che CMTrace visualizzi nuovi dati mentre si esamina il file di log  

#### <a name="showhide-details"></a>Show/Hide Details (Mostra/Nascondi dettagli)

Mostrare o nascondere tutte le colonne diverse da quella del testo del log. Espande anche la colonna del testo del log su tutta la larghezza della finestra. Usare questa azione quando si visualizzano i log in un computer con una risoluzione di visualizzazione non sufficiente. Visualizza altre informazioni del testo del log.  

> [!Note]  
> Quando si visualizzano i file di testo normale, CMTrace nasconde automaticamente i dettagli perché sono sempre vuoti.  

#### <a name="showhide-info-pane"></a>Show/Hide Info Pane (Mostra/Nascondi riquadro informazioni)

Visualizza o nasconde il riquadro delle informazioni. Usare questa azione quando si visualizzano i log in un computer con una risoluzione di visualizzazione non sufficiente. Visualizza altri dettagli di registrazione.  


## <a name="log-pane"></a>Riquadro Log

Il riquadro Log è nella parte superiore della finestra CMTrace. Visualizza le righe dei file di log.

Quando si seleziona una riga, questa viene temporaneamente evidenziata usando la combinazione colori per la selezione di Windows.

Le righe evidenziate corrispondono ai criteri definiti con l'opzione **Highlight** (Evidenzia) nel menu **Strumenti**. L'evidenziazione usa il colore specificato in **Preferenze**.

CMTrace visualizza le righe con errori con uno sfondo rosso e il colore del testo giallo. Nei log in formato CCM le voci dei log hanno un valore di tipo esplicito che indica la voce come errore. Per gli altri formati di log, CMTrace effettua in ogni voce una ricerca con distinzione tra maiuscole e minuscole delle stringhe di testo corrispondenti a "error".

Visualizza le righe con avvisi con uno sfondo giallo. Nei log in formato CCM le voci dei log hanno un valore di tipo esplicito che indica la voce come avviso. Per gli altri formati di log, CMTrace effettua in ogni voce una ricerca con distinzione tra maiuscole e minuscole delle stringhe di testo corrispondenti a "warn".


## <a name="info-pane"></a>Riquadro delle informazioni

Il riquadro delle informazioni è nella parte inferiore della finestra CMTrace. Include le funzionalità seguenti:

- Dettagli sulla voce di log attualmente selezionata  

- Una casella di testo che visualizza il testo del log  

- Visualizza i ritorni a capo in modo che sia più facile leggere il testo formattato  

- È più facile leggere le voci lunghe che non sono completamente visibili nel riquadro Log  

Mostrare o nascondere il riquadro delle informazioni con l'opzione **Show/Hide Info Pane** (Mostra/Nascondi riquadro informazioni) nel menu **Tools**. Se il riquadro delle informazioni occupa più di metà della finestra del log, CMTrace lo nasconde automaticamente.

### <a name="progress-bar"></a>Indicatore di stato

Quando si apre un file di log per la prima volta, CMTrace sostituisce il riquadro delle informazioni con un indicatore di stato. Questo stato indica la quantità di contenuti del file esistente già caricata. Lo stato raggiunge il 100%, CMTrace rimuove l'indicatore di stato e lo sostituisce con il riquadro delle informazioni. Quando si caricano file di grandi dimensioni, questo comportamento offre un'indicazione di quanto tempo potrebbe essere necessario per il caricamento.

### <a name="status-bar"></a>Barra di stato

Per i file di log in formato Configuration Manager e in formato CCM, la barra di stato visualizza il tempo trascorso per le voci del log selezionate. Se si seleziona una singola voce, lo strumento visualizza il tempo trascorso della prima voce di log alla voce selezionata. Se si selezionano più voci, calcola il tempo trascorso dalla prima voce selezionata all'ultima. CMTrace formatta queste informazioni nel modo seguente:

`Elapsed time is <hours>h <minutes>m <seconds>s <milliseconds>ms (<seconds+milliseconds> seconds)`


## <a name="windows-shell-integration"></a>Integrazione della shell di Windows

CMTrace supporta le [associazioni di file](#file-associations) e il [trascinamento della selezione](#drag-and-drop).

### <a name="file-associations"></a>Associazioni di file

CMTrace può associarsi a estensioni di file log e lo_. Quando il programma viene avviato, controlla il Registro di sistema per determinare se è già associato a queste estensioni di file. Se CMTrace non è già associato a nessuna estensione di file, viene chiesto di associare le estensioni di file a CMTrace. Se si seleziona **Non visualizzare più questo messaggio**, CMTrace ignora questo controllo quando viene eseguito su questo computer.

### <a name="drag-and-drop"></a>Trascinamento della selezione

CMTrace supporta la funzionalità di trascinamento della selezione di base. Trascinare un file di log da Esplora risorse a CMTrace per aprirlo.


## <a name="other-tips"></a>Altri suggerimenti

### <a name="last-directory-registry-key"></a>Chiave del Registro di sistema Last Directory

<!--511280-->
Per impostazione predefinita, CMTrace salva l'ultimo percorso di log aperto. Questo comportamento è utile nel server del sito, perché l'impostazione predefinita è ogni volta il percorso log.

La prima volta che lo si avvia in un client, l'impostazione predefinita è la directory di lavoro corrente. Questa posizione può essere il percorso in cui si è salvato CMTrace o un percorso come `%userprofile%\Desktop`.

Il valore **Last Directory** nella chiave del Registro di sistema `HKEY_CURRENT_USER\Software\Microsoft\Trace32` controlla questa posizione predefinita. Se si imposta questo valore su `%windir%\CCM\Logs` nei client, CMTrace apre i file nel percorso log dei client la prima volta che lo si avvia.


## <a name="see-also"></a>Vedere anche

- [File di log](../plan-design/hierarchy/log-files.md)

- [Visualizzatore file di log del Supporto tecnico](support-center.md#support-center-log-file-viewer)

- [Supporto tecnico OneTrace](support-center-onetrace.md)
