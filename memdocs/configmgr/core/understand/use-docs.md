---
title: Come usare la documentazione
titleSuffix: Configuration Manager
description: Suggerimenti sull'uso della di documentazione tecnica di Configuration Manager.
ms.date: 04/20/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b3d755bd-0870-4f1f-a56d-bfd3c7b492b9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d694f9985e6d1e5118f2620e5cbd556de249788a
ms.sourcegitcommit: 568f8f8c19fafdd0f4352d0682f1ca7a4d665d25
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2020
ms.locfileid: "81771323"
---
# <a name="how-to-use-the-configuration-manager-docs"></a>Uso della documentazione di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Questo articolo fornisce risorse e suggerimenti per l'uso della raccolta di documentazione per Configuration Manager.

- Come eseguire la ricerca
- Invio di segnalazioni di bug, miglioramenti, domande e nuove idee per la documentazione
- Come ricevere notifiche relative alle modifiche
- Come contribuire alla documentazione

Per informazioni generali sul prodotto, vedere l'argomento sulla [consultazione della Guida](find-help.md).

## <a name="search"></a><a name="bkmk_searchtips"></a> Ricerca

Per trovare le informazioni necessarie, usare i seguenti suggerimenti per la ricerca:

- Quando si usa il motore di ricerca preferito per individuare il contenuto per Configuration Manager, includere `ConfigMgr` con le parole chiave della ricerca.

  - Cercare i risultati in `docs.microsoft.com/configmgr` per il branch corrente di Configuration Manager. I risultati di `docs.microsoft.com/previous-versions` sono per le versioni precedenti del prodotto.

  - Per concentrare ulteriormente i risultati della ricerca sulla raccolta di contenuto corrente, includere `site:docs.microsoft.com` per definire l'ambito del motore di ricerca.

- Usare termini di ricerca che corrispondano alla terminologia nell'interfaccia utente e nella documentazione online. Evitare termini non ufficiali o abbreviazioni che possono trovarsi nei contenuti della community. Ad esempio, cercare:

  - "punto di gestione" anziché di "PG"
  - "tipo di distribuzione" anziché "TD"
  - "aggiornamenti software" anziché "AS"

- Per cercare all'interno dell'articolo corrente, usare la funzionalità di **ricerca** del browser. Con i Web browser più recenti, premere **CTRL**+**F** e quindi immettere i termini di ricerca.

- Ogni articolo in `docs.microsoft.com` include i campi seguenti per agevolare la ricerca del contenuto:

  - **Cerca** nell'angolo superiore destro. Per cercare in tutti gli articoli immettere i termini in questo campo. Gli articoli nella raccolta di Configuration Manager includono automaticamente l'ambito `ConfigMgr` per eseguire la ricerca solo in questa raccolta di documentazione.

  - **Filtra per titolo** sopra il sommario a sinistra. Per eseguire una ricerca nel sommario corrente, immettere i termini in questo campo. Il campo consente di individuare le corrispondenze solo con termini che appaiono nei titoli degli articoli per il nodo corrente. Ad esempio, **Infrastruttura di base** (`docs.microsoft.com/configmgr/core`) o **Gestione applicazioni** (`docs.microsoft.com/configmgr/apps`).

- In caso di problemi durante la ricerca, [inviare un feedback](#bkmk_docfeedback). Quando si segnala il problema specificare il motore di ricerca in uso, le parole chiave che si è tentato di usare e l'articolo di destinazione. Questo feedback consente a Microsoft di ottimizzare il contenuto per migliorare la ricerca.

> [!TIP]
> A partire da Configuration Manager versione 1902, è disponibile il nodo **Documentazione** nella nuova area di lavoro **Community** della console di Configuration Manager. Questo nodo contiene informazioni aggiornate sulla documentazione di Configuration Manager e gli articoli del supporto tecnico. Per altre informazioni, vedere [Uso della console di Configuration Manager](../servers/manage/admin-console.md#bkmk_doc-dashboard).

## <a name="feedback"></a><a name="bkmk_docfeedback"></a> Commenti e suggerimenti

Selezionare il collegamento **Commenti e suggerimenti** in alto a destra nell'articolo per passare alla sezione corrispondente in fondo. Questa sezione è integrata con il sistema dei problemi di GitHub. Per altre informazioni sull'integrazione con Problemi di GitHub, vedere il [post di blog sulla piattaforma di documentazione](https://docs.microsoft.com/teamblog/a-new-feedback-system-is-coming-to-docs).

Per condividere commenti e suggerimenti sul prodotto Configuration Manager, selezionare **Commenti e suggerimenti sul prodotto**. Per altre informazioni, vedere la sezione su [commenti e suggerimenti per i prodotti](find-help.md#product-feedback).

Un [account GitHub](https://github.com/join) è un prerequisito per l'invio di un feedback sulla documentazione. Dopo aver effettuato l'accesso, viene richiesta un'autorizzazione per l'organizzazione MicrosoftDocs. Quando si seleziona **Commenti sul contenuto** immettere un titolo e un commento e quindi scegliere **Invia commenti**. Con questa azione si aggiunge un nuovo problema relativo all'articolo di destinazione al [repository SCCMdocs](https://github.com/MicrosoftDocs/SCCMdocs/issues).

Questa integrazione consente anche di visualizzare eventuali problemi chiusi o aperti esistenti per l'articolo di destinazione. Se esistono altri problemi, esaminarli prima di inviare un nuovo problema. Se si trova un problema correlato, selezionare l'icona del viso per aggiungere una reazione o espanderla per aggiungere un commento.

#### <a name="types-of-feedback"></a>Tipi di feedback

Usare Problemi di GitHub per inviare i seguenti tipi di commenti e suggerimenti:

- Bug della documentazione: il contenuto non è aggiornato, è poco chiaro, confuso o incompleto.
- Miglioramento della documentazione: suggerimenti per migliorare l'articolo.
- Domanda sulla documentazione: è necessario reperire documentazione esistente.
- Idea per la documentazione: suggerimenti per un nuovo articolo. Usare questo metodo anziché UserVoice per i suggerimenti sulla documentazione.
- Apprezzamenti: commenti positivi su un articolo utile o informativo.
- Localizzazione: commenti e suggerimenti sulla traduzione del contenuto.
- Ottimizzazione del motore di ricerca (SEO): commenti e suggerimenti sui problemi che si verificano durante la ricerca di contenuto. Includere il motore di ricerca, le parole chiave e l'articolo di destinazione nei commenti.

Se si crea un problema per argomenti non correlati alla documentazione, Microsoft lo chiuderà. Ad esempio:

- [Commenti e suggerimenti sul prodotto](find-help.md#product-feedback)
- [Domande sul prodotto](https://social.technet.microsoft.com/Forums/en-US/home?category=ConfigMgrCB)
- [Richieste di supporto](https://aka.ms/cmcbsupport)

Per condividere commenti e suggerimenti sulla piattaforma docs.microsoft.com, vedere la sezione relativa al [feedback sulla documentazione](https://aka.ms/sitefeedback). La piattaforma include tutti i componenti di wrapping, ad esempio l'intestazione, il sommario e il menu a destra. Include anche indicazioni sull'esecuzione del rendering degli articoli nel browser, ad esempio il tipo di carattere, le finestre di avviso e gli ancoraggi delle pagine.

## <a name="notifications"></a><a name="bkmk_notifications"></a> Notifiche

Per ricevere notifiche quando viene modificato il contenuto nella libreria della documentazione, procedere come segue:

1. Usare la [ricerca nella documentazione](https://docs.microsoft.com/search/index?scope=ConfigMgr) per trovare un articolo o una serie di articoli. Ad esempio:

    - Cercare un singolo articolo in base al titolo, ad esempio ["File di log per la risoluzione dei problemi - Configuration Manager"](https://docs.microsoft.com/search/index?search=%22Log+files+for+troubleshooting+-+Configuration+Manager%22&scope=ConfigMgr)

    - Cercare qualsiasi articolo relativo a [SQL](https://docs.microsoft.com/search/index?search=SQL&scope=ConfigMgr)

2. Nell'angolo superiore destro selezionare il collegamento **RSS**.

3. Usare questo feed in qualsiasi applicazione RSS per ricevere notifiche quando viene apportata una modifica a uno dei risultati della ricerca.

> [!TIP]
> È anche possibile **consultare** il [repository SCCMdocs](https://github.com/MicrosoftDocs/SCCMdocs) su GitHub. Questo metodo genera molte notifiche. Non include inoltre le modifiche presenti in un repository privato usato da Microsoft.

## <a name="contribute"></a><a name="bkmk_contribute"></a> Collaborazione

La libreria di documentazione di Configuration Manager, analogamente alla maggior parte del contenuto su docs.microsoft.com, è open source su GitHub. Questa raccolta accetta e incoraggia i contributi della community. Per altre informazioni su come iniziare, vedere la [guida per i collaboratori](https://docs.microsoft.com/contribute). L'unico prerequisito consiste nel creare un [account GitHub](https://github.com/join).

### <a name="basic-steps-to-contribute-to-sccmdocs"></a>Procedura di base per contribuire a SCCMdocs

1. Nell'articolo di destinazione selezionare **Modifica**. Questa azione apre il file di origine in GitHub.

2. Per modificare il file di origine, selezionare l'icona a forma di matita.

3. Apportare le modifiche nel markdown. Per altre informazioni, vedere [How to use Markdown for writing Docs](https://docs.microsoft.com/contribute/markdown-reference) (Come usare il markdown per scrivere documenti).

4. Nella sezione di modifica del file immettere un commento di commit pubblico che descriva *cosa* è stato modificato. Selezionare quindi **Propose file change** (Proponi modifica file).

5. Scorrere verso il basso e verificare le modifiche apportate. Selezionare **Create pull request** (Crea richiesta pull) per aprire il modulo. Indicare *perché* è stata apportata la modifica. Assegnare un tag all'autore dell'articolo e richiedere la sua revisione. Selezionare **Create pull request** (Crea richiesta pull).

### <a name="what-to-contribute"></a>In che modo si contribuisce

Se si vuole contribuire, ma non si sa dove iniziare, vedere i suggerimenti seguenti:

- Cercare nell'elenco dei problemi le etichette assegnate alla community:

  - [good-first-issue](https://github.com/MicrosoftDocs/sccmdocs/issues?q=is:open+is:issue+label:good-first-issue)
  - [help-wanted](https://github.com/MicrosoftDocs/sccmdocs/issues?q=is:open+is:issue+label:help-wanted)  

    Gli autori di Microsoft assegnano queste etichette ai problemi per cui più facilmente si riceveranno contributi della community.

- Esaminare un articolo per verificarne l'accuratezza. Aggiornare quindi i metadati **ms.date** usando il formato `mm/dd/yyyy`. Questo contributo consente di mantenere aggiornato il contenuto.

- Aggiungere precisazioni, esempi o indicazioni in base alla propria esperienza. Questo contributo usa le risorse della community per condividere le informazioni.

- Correggere le traduzioni in una lingua diversa dall'inglese. Questo contributo migliora l'usabilità del contenuto localizzato.

> [!NOTE]
> Chi non è un dipendente di Microsoft deve firmare un contratto di licenza per contributi per inviare contributi consistenti. GitHub richiede automaticamente di firmare questo contratto quando un contributo raggiunge la soglia.

### <a name="tips"></a>Suggerimenti

Quando si contribuisce alla documentazione di Configuration Manager, seguire queste linee guida generali:

- Invece di inviare richieste pull di grandi dimensioni, [segnalare un problema](#bkmk_docfeedback) e avviare una discussione. Si eviterà così di perdere tempo e sarà possibile stabilire come procedere.

- Leggere la [guida di stile Microsoft](https://aka.ms/MicrosoftStyle). Tenere presenti i [10 suggerimenti principali di Microsoft sullo stile e il tono](https://docs.microsoft.com/style-guide/top-10-tips-style-voice).

- Basare il proprio lavoro sul [modello di richiesta pull](https://github.com/MicrosoftDocs/SCCMdocs/blob/master/PULL_REQUEST_TEMPLATE.md).

- Seguire il [flusso di lavoro di GitHub](https://guides.github.com/introduction/flow/).

- Creare spesso blog e tweet (o quanto si ritiene idoneo) sui propri contributi.

Questo elenco è stato tratto dalla [guida ai contributi su .NET](https://github.com/dotnet/docs/blob/master/CONTRIBUTING.md#dos-and-donts).

## <a name="consolidation-of-documentation-for-microsoft-endpoint-manager"></a>Consolidamento della documentazione per Microsoft Endpoint Manager

Per supportare meglio gli scenari combinati per Intune e Configuration Manager, le librerie di documentazione sono state consolidate nel [sito di Microsoft Endpoint Manager](https://docs.microsoft.com/mem). La documentazione di Intune è ora disponibile all'indirizzo [docs.microsoft.com/mem/intune](https://docs.microsoft.com/mem/intune) e la documentazione di Configuration Manager è ora all'indirizzo [docs.microsoft.com/mem/configmgr](https://docs.microsoft.com/mem/configmgr). Se viene usato un URL precedente, l'URL verrà reindirizzato automaticamente. Non è quindi necessario apportare alcuna modifica per poter leggere questi contenuti.

Tuttavia, se si inviano commenti o si contribuisce alla stesura degli articoli, saranno necessarie alcune modifiche:

- I problemi di GitHub esistenti rimangono nel repository originale: [IntuneDocs](https://github.com/MicrosoftDocs/IntuneDocs/issues) o [SCCMDocs](https://github.com/MicrosoftDocs/SCCMDocs/issues).

  - Questi problemi, pertanto, non verranno visualizzati come problemi aperti o chiusi nella sezione dei commenti dell'articolo correlato.

  - Continueremo a lavorare per cercare di risolvere questi problemi.

  - In alcuni casi, potremmo decidere di chiudere un problema che riteniamo di non poter risolvere.

  - Se si riscontra un problema nel repository esistente e si vuole segnalarlo, inserire un commento nell'articolo spostato nel [repository MEMDocs](https://github.com/MicrosoftDocs/MEMDocs).

- Quando si inserisce un commento o si modifica un articolo, il problema o la richiesta pull viene inserita nel repository MEMDocs.
