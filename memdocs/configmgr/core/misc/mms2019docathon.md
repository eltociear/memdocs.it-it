---
title: MMS 2019 Docathon
ms.date: 05/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
description: Informazioni e regole per MMS 2019 Docathon
ms.assetid: 8fe2ecfc-f5c1-4fa6-8703-245339400723
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 91430688fd2af93e5d5b5ce7eb0cbc6358388ea4
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/09/2020
ms.locfileid: "89607843"
---
# <a name="mms-2019-docathon"></a>MMS 2019 Docathon

In occasione del Midwest Management Summit (MMS) 2019, il Microsoft Content Team per Configuration Manager e Microsoft Intune ha organizzato un docathon. Se si prevede di frequentare il [laboratorio pratico su docs.microsoft.com](https://sched.co/N6fd) che si terrà lunedì 6 maggio, questa è l'occasione giusta per sviluppare nuovi contributi con il supporto degli autori di Microsoft. Il docathon si terrà per tutta la durata della conferenza ed è aperto alla partecipazione di tutti gli iscritti al summit MMS 2019.

Perché partecipare? Docs.microsoft.com è una piattaforma open source per la documentazione relativa ai prodotti Microsoft, basata su GitHub. Microsoft invita tutti gli utenti a offrire il proprio contributo alla documentazione. Quando un utente offre un proprio contributo, viene riconosciuto dalla piattaforma nell'elenco dei collaboratori per ogni articolo. Questi sono alcuni dei tipi di contributo che possono essere offerti dalla community:

- Refusi
- Precisazioni
- Esempio
- Suggerimenti e indicazioni dal mondo reale
- Revisione del contenuto, per maggiore leggibilità

## <a name="set-up"></a>Configurare

Se non si è ancora configurati come collaboratori, eseguire in anticipo i passaggi seguenti.

### <a name="github-account"></a>Account GitHub

Creare un [account GitHub](https://github.com/join)

- Identificare eventuali affiliazioni nel proprio profilo  

- Abilitare l'autenticazione a due fattori  

#### <a name="additional-considerations"></a>Altre considerazioni

- Verificare i criteri adottati dalla propria società in merito ai contributi open source  

    > [!Note]  
    > Per contributi più ampi, sarà necessario accettare il [Contributor License Agreement (CLA)](https://cla.opensource.microsoft.com/) di Microsoft relativo ai contributi open source. Esaminare in anticipo questo contratto.  

- I contributi forniti a docs.microsoft.com sono validi ai fini della valutazione per il riconoscimento MVP  

- I dipendenti Microsoft devono effettuare alcuni passaggi in più e seguire una procedura leggermente diversa per fornire il proprio contributo  

Per altre informazioni, vedere [Configurazione dell'account GitHub](/contribute/get-started-setup-github) nella Guida per i collaboratori di docs.microsoft.com.

## <a name="scope"></a>Ambito

L'evento interesserà solo i repository GitHub seguenti:

- [IntuneDocs](https://github.com/MicrosoftDocs/IntuneDocs)
- [SCCMDocs](https://github.com/MicrosoftDocs/SCCMdocs)
- [sccm-docs-powershell-ref](https://github.com/MicrosoftDocs/sccm-docs-powershell-ref)

Eventuali modifiche ad altri contenuti di docs.microsoft.com saranno apprezzate e vivamente consigliate, ma non saranno riconosciute ai fini di questo evento.

## <a name="learn-the-process"></a>Informazioni sul processo

Leggere le informazioni su [come segnalare problemi](../understand/use-docs.md#bkmk_docfeedback) e [come contribuire](../understand/use-docs.md#bkmk_contribute). Quasi tutte le modifiche di base possono eseguite attraverso l'esperienza utente del browser per GitHub.  

> [!Note]  
> Se si è interessati al flusso di lavoro più complesso con git e VSCode, vedere [Installare gli strumenti di creazione del contenuto](/contribute/get-started-setup-tools). E/o chiedere aiuto ad Aaron o Erik. Può essere opportuno usare il flusso di lavoro più complesso per le seguenti operazioni:
>
> - Creare un nuovo articolo
> - Aggiungere immagini
> - Eseguire la ricerca e la sostituzione di stringhe, incluse espressioni regolari
> - Apportare modifiche più estese e complesse  

## <a name="determine-your-goals"></a>Definizione degli obiettivi

È consigliabile iniziare a pianificare i propri obiettivi per questo evento. Quali sono gli obiettivi da raggiungere?

- Esaminare i problemi esistenti nei repository di ambito. Determinate etichette, come **good-first-issue** o **help-wanted**, possono offrire un buon punto di partenza. Se si vuole trattare uno di questi problemi, inserire un commento con **#MMS2019Docathon** e aggiungere un tag all'autore (@author), chiedendo di farsi assegnare il problema. In questo modo si [reclama il diritto](https://www.merriam-webster.com/words-at-play/word-origin-dibs) a gestirlo personalmente. Questa operazione può essere eseguita il numero di volte desiderato.  
    Ad esempio, in SCCMDocs, dove Aaron è l'autore degli articoli: `@aczechowski I'm claiming this issue for #MMS2019Docathon`

- Si è conoscenza di un problema relativo a un articolo, ma non è stato ancora inviato feedback. In altre parole, non è presente alcuna informazione nella sezione **Commenti** nella parte inferiore dell'articolo. Segnalare un nuovo problema e quindi usare le istruzioni precedenti per reclamare il diritto a gestirlo.  

    - Aggiungere un esempio di codice, un esempio dal mondo reale o un suggerimento comune.  

    - Evitare correzioni di grammatica o stile, a meno che non se ne sia già parlato con Aaron o Erik.  

    - Il proprio articolo preferito risulta non modificato da oltre 90 giorni, prima del 6 febbraio 2019. È possibile rivederlo e quindi modificare la proprietà dei metadati **ms.date**. In questo caso, il contributo significherà: "Ho rivisto questo articolo ed è ancora tecnicamente corretto, quindi ho aggiornato la data." Segnalare un problema per reclamare il diritto a gestirlo.  

    - Controllare prima il feedback sugli articoli per essere sicuri che non vi siano problemi aperti da un altro utente. Questa azione è indispensabile dal punto di vista tecnico. Se si segue questa procedura e qualcun altro invia prima il proprio feedback, verrà preso in considerazione solo il primo contributo.  

- La sessione di un'ora che si terrà lunedì in pausa pranzo sarà dedicata a definire questi obiettivi. Aaron e Erik saranno a disposizione per domande o problemi.

## <a name="contest-summary"></a>Riepilogo

Il concorso si terrà durante l'intera settimana, dal 6 al 9 maggio. Tutti gli iscritti al summit MMS 2019 possono partecipare. Inviare il proprio contributo entro le ore 15:00 (ora centrale del Pacifico) di giovedì 9 maggio 2019. I premi verranno assegnati giovedì 9 maggio dopo la sessione [ConfigMgr Product Team Q&A](https://sched.co/N6ge). Per vincere è necessario partecipare al summit MMS 2019, ma non necessariamente a tale sessione. Se non si è presenti alla sessione, per ritirare un premio, contattare Aaron prima di venerdì mattina.

> [!Important]  
> Per essere accreditati, è necessario includere l'hashtag **#MMS2019Docathon** in tutti i contributi.

### <a name="award-categories"></a>Categorie dei premi

#### <a name="grand-prize"></a>Premio speciale

- **Il contributo più significativo**: valutato in base ai criteri seguenti, secondo il giudizio di Aaron e Erik. Se si ritiene che il proprio contributo abbia i requisiti per ricevere questo premio, includere un commento nella richiesta pull per convincere la giuria.

    - Vantaggio per la community (50%)
    - Conformità allo stile Microsoft (25%)
    - Markdown corretto (25%)  

Il vincitore del premio speciale riceverà:

- Un pass per [MMS Jazz Edition](https://mmsmoa.com/sessions/jazz-edition.html), per gentile concessione della direzione di MMS, del valore di 1799 USD.
- Un tumbler Yeti Rambler 30 oz personalizzato
- Un supporto portatelefono per auto Popsocket personalizzato (con morsa)

#### <a name="first-place-prizes"></a>Primi premi

I riconoscimenti seguenti vengono calcolati in base al numero di contributi idonei ai repository di ambito. Non è necessario che siano stati uniti o pubblicati. È sufficiente che siano stati inviati come richiesta pull entro la fine della conferenza. Microsoft si riserva il diritto di escludere dal Concorso tutti coloro che risultano compiere atti allo scopo di eludere le regole del sistema. Il vincitore in ogni categoria riceverà un tumbler Yeti Rambler 30 oz personalizzato e un supporto portatelefono per auto Popsocket personalizzato (con morsa). Verrà selezionato un solo vincitore per ogni categoria.

- **Il maggior numero di commit inviati**

- **Il maggior numero di righe modificate**

- **Il maggior numero di articoli modificati**

> [!Note]  
> Non verranno assegnati premi per il maggior numero di problemi segnalati. Il feedback è utile, ma l'obiettivo principale di questo evento è di promuovere l'invio di contributi.

## <a name="resources"></a>Risorse

- [Stile Microsoft](https://aka.ms/MicrosoftStyle)

    - [Avvio rapido](/contribute/style-quick-start)

    - [10 suggerimenti principali di Microsoft sullo stile e il tono](/style-guide/top-10-tips-style-voice)

- [Guida per i collaboratori](/contribute)

- [Come usare Markdown per scrivere articoli di Docs](/contribute/markdown-reference)

## <a name="official-rules"></a>Regolamento ufficiale

Concorso dell'Evento Docathon del Microsoft Cloud + AI Developer Relations Content & Learning MMS 2019 - REGOLAMENTO UFFICIALE

1. SPONSOR

    Il presente Regolamento ufficiale ("Regolamento") disciplina lo svolgimento del Concorso relativo all'Evento Docathon ("Concorso") che si terrà in occasione del Microsoft C+AI DevRel Content MMS 2019. Lo sponsor ("Sponsor") è Microsoft Corporation.

2. DEFINIZIONI

    In questo Regolamento, il termine "Microsoft" fa riferimento allo Sponsor. Il termine "Partecipante" fa riferimento a un partecipante del Concorso. Il termine "Evento" fa riferimento all'evento Docathon MMS 2019 che si tiene a Minneapolis, Stati Uniti. La partecipazione a questo Concorso costituisce l'accettazione piena e incondizionata del Partecipante al presente Regolamento ufficiale.

3. PERIODO DI AMMISSIONE

    Il Concorso si svolgerà durante il normale orario dell'Evento, dal 6 al 9 maggio 2019 ("Periodo di ammissione").

4. REQUISITI DI IDONEITÀ

    Il Concorso è aperto a tutti i partecipanti iscritti all'Evento, che abbiano compiuto almeno 18 anni e che risiedano legalmente in uno dei 50 Stati Uniti d'America, incluso il District of Columbia. I dipendenti e i dirigenti di Microsoft Corporation e delle relative filiali, le persone coinvolte nell'esecuzione o nell'amministrazione di questo Evento promozionale e i relativi familiari (dipendenti, parenti stretti e membri dello stesso nucleo familiare) non sono idonei a partecipare al Concorso. L'idoneità è nulla laddove proibito.

    Per i partecipanti agli eventi di carattere commerciale o fieristico: In caso di partecipazione all'Evento in qualità di dipendente di una società, è esclusiva responsabilità del Partecipante rispettare i criteri di conferimento dei premi stabiliti dal datore di lavoro. Microsoft non potrà essere parte in eventuali controversie o azioni correlate a tale questione. DIPENDENTI PUBBLICI, INCLUSI GLI INSEGNANTI: Microsoft si impegna a rispettare le regole etiche e di condotta degli enti pubblici in merito al conferimento di premi e pertanto i dipendenti pubblici non sono idonei a partecipare a questo Evento promozionale.

5. MODALITÀ DI PARTECIPAZIONE

    Per creare un contributo, inviare modifiche agli articoli nei repository GitHub seguenti: IntuneDocs, SCCMDocs, sccm-docs-powershell-ref. Per altre informazioni sulla modalità di invio, vedere [Come contribuire ai documenti](/sccm/core/understand/use-docs#bkmk_contribute).

    Per inviare un contributo, inviare una richiesta pull su GitHub.

    Non vi sono limitazioni al numero di contributi che è possibile inviare. A ogni singola persona potrà essere assegnato un solo premio per categoria.

    Microsoft non potrà essere ritenuta responsabile di contributi in eccesso, persi, inviati in ritardo, danneggiati o incompleti. In caso di controversia, i contributi saranno considerati come inviati dal titolare autorizzato dell'account GitHub.

6. IDONEITÀ DEI CONTRIBUTI

    Per essere idoneo, un contributo deve soddisfare i requisiti di contenuto/tecnici seguenti:

    - Il contributo deve essere un'opera originale del Partecipante; e
    - Il contributo non deve essere stato selezionato come vincitore in altri concorsi; e
    - Il Partecipante deve avere ottenuto tutte le autorizzazioni, le approvazioni o le licenze necessarie per l'invio del contributo; e
    - Nella misura in cui il contributo richieda l'invio di contenuti realizzati da utenti, quali software, foto, video, brani musicali, grafica, saggi e così via, i Partecipanti garantiscono che il contributo è frutto del loro lavoro originale, che non è stato copiato da altri senza autorizzazione o diritti verificabili e che non viola il diritto alla protezione dei dati personali, i diritti di proprietà intellettuale o altri diritti di qualsiasi altra persona o entità. Il Partecipante può includere marchi, logo ed elementi grafici Microsoft, per i quali Microsoft concede una licenza d'uso limitata ai soli fini dell'invio di un contributo per il presente Concorso; e
    - Il contributo NON può contenere, come determinato da Microsoft a sua esclusiva discrezione, contenuti osceni, offensivi, violenti, diffamatori, denigratori o illegali, che promuovano l'uso di alcol, droghe illegali, tabacco o un particolare programma politico o che trasmettano messaggi con possibili effetti negativi sull'avviamento di Microsoft.

7. USO DEI CONTRIBUTI

    Microsoft non rivendica diritti di proprietà sul contributo inviato dal Partecipante. Tuttavia, inviando un contributo, il Partecipante concede a Microsoft il diritto e la licenza irrevocabili, internazionali e a titolo gratuito per l'uso, la revisione, la valutazione, il test e l'analisi del contributo e di tutto il suo contenuto in relazione al presente Concorso e per l'uso di tale contributo su qualsiasi mezzo, attualmente conosciuto o inventato in seguito, per qualsiasi scopo commerciale o non commerciale, inclusi, a titolo esemplificativo, marketing, vendita o promozione di prodotti o servizi Microsoft, senza ulteriore autorizzazione da parte del Partecipante. Il Partecipante è consapevole del fatto che non riceverà alcun compenso o credito per l'uso del contributo, oltre a quanto descritto nel presente Regolamento ufficiale.

    Partecipando al Concorso, il Partecipante riconosce che Microsoft potrebbe aver sviluppato o commissionato materiali simili o identici al proprio contributo e rinuncia a eventuali rivendicazioni in merito a qualsiasi analogia con esso. Il Partecipante riconosce altresì che Microsoft non imporrà alcun limite agli incarichi operativi dei suoi rappresentanti che hanno avuto accesso al contributo e accetta che l'uso delle informazioni memorizzate da tali rappresentanti nello sviluppo o nella distribuzione di prodotti o servizi non determini una responsabilità per Microsoft ai sensi del presente contratto o della legge sul copyright o sui segreti commerciali.

    Il contributo del Partecipante potrebbe essere pubblicato su un sito Web accessibile pubblicamente. Microsoft non può essere ritenuta responsabile di un eventuale uso non autorizzato del contributo del Partecipante da parte dei visitatori del sito Web. Microsoft non è obbligata a fare uso del contributo del Partecipante per qualsiasi scopo, anche se selezionato come vincitore.

8. SELEZIONE DEI VINCITORI E NOTIFICA

    In attesa di conferma dell'idoneità, i potenziali vincitori dei premi verranno selezionati da Microsoft, dal relativo Agente o da una giuria qualificata fra tutti i contributi idonei pervenuti secondo i criteri seguenti:

    - Premio speciale: Il contributo più significativo, in base ai criteri seguenti:
        - 50% - Vantaggio per la community
        - 25% - Conformità allo stile Microsoft
        - 25% - Markdown corretto
    - I primi premi seguenti, calcolati in base al numero di contributi idonei ai repository di ambito. Non è necessario che siano stati uniti o pubblicati. È sufficiente che siano stati inviati come richiesta pull entro la fine della conferenza. Microsoft si riserva il diritto di escludere dal Concorso tutti coloro che risultano compiere atti allo scopo di eludere le regole del sistema.
        - Il maggior numero di commit inviati
        - Il maggior numero di righe modificate
        - Il maggior numero di articoli modificati

    I vincitori verranno selezionati giovedì 9 maggio 2019 dopo le 15:00 (CT).

    I vincitori verranno informati in occasione dell'Evento e dovranno ritirare il premio prima della chiusura dell'Evento.

    In caso di parità tra contributi idonei, la decisione spetterà a un giudice supplementare in base ai criteri di giudizio descritti in precedenza. Le decisioni dei giudici sono definitive e vincolanti. Se non viene inviato un numero sufficiente di contributi conformi ai requisiti stabiliti, Microsoft selezionerà, a propria discrezione, un numero minore di vincitori rispetto al numero di premi in palio per il Concorso.

    I vincitori verranno informati tramite le informazioni di contatto fornite al momento dell'invio del contributo e potrebbero essere tenuti a compilare moduli per il ritiro del premio e per finalità fiscali ("Moduli"). Se un vincitore selezionato non può essere contattato, non è idoneo, non riesce a ritirare un premio o a restituire un modulo, il vincitore perderà il diritto al premio e verrà selezionato un altro vincitore, purché entro i tempi consentiti. Potranno essere selezionati solo tre vincitori alternativi, dopodiché i premi non ritirati rimarranno non assegnati.  

9. PREMI

    Verranno assegnati i premi seguenti:

    - Un (1) premio speciale. Il pacchetto del premio include gli elementi seguenti:
        - Un pass per [MMS Jazz Edition](https://mmsmoa.com/sessions/jazz-edition.html), concesso della direzione di MMS. Valore commerciale approssimativo: 1799 USD.
        - Un tumbler Yeti Rambler 30 oz. Valore commerciale approssimativo: 35 USD.
        - Un supporto portatelefono per auto Popsocket (con morsa). Valore commerciale approssimativo: 15 USD.

        Il valore commerciale approssimativo totale di questo pacchetto è 1849 USD.

    - Tre (3) primi premi. Il pacchetto del premio include gli elementi seguenti:
        - Un tumbler Yeti Rambler 30 oz. Valore commerciale approssimativo: 35 USD.
        - Un supporto portatelefono per auto Popsocket (con morsa). Valore commerciale approssimativo: 15 USD.

        Il valore commerciale approssimativo totale di questo pacchetto è 50 USD.

    Il valore commerciale approssimativo totale di tutti i premi è 1999 USD.

    Verrà assegnato un (1) solo premio per persona. Non verranno assegnati altri premi oltre a quelli menzionati. Non sarà consentito alcun trasferimento, sostituzione o cessione di premio, fatto salvo il caso in cui Microsoft si riservi il diritto di sostituire un premio con un altro premio di valore uguale o superiore, nel caso in cui il premio offerto non sia disponibile. I premi vengono assegnati "COSÌ COME SONO" con nessuna garanzia di alcun tipo, espressa o implicita, incluse a titolo esemplificativo le garanzie implicite di commerciabilità, adeguatezza per uno scopo specifico e non violazione di diritti di terzi. Ai vincitori potrà essere richiesto di compilare moduli per il ritiro del premio e/o per finalità fiscali ("Moduli") e restituirli entro il termine specificato nella notifica della vincita. Le eventuali imposte applicate al premio sono di esclusiva responsabilità del vincitore, che è invitato a rivolgersi a un consulente indipendente in merito alle implicazioni fiscali legate all'accettazione di un premio. Ritirando un premio, il vincitore accetta che Microsoft possa pubblicarne il contributo, il nome, l'immagine e la città di provenienza, online, su materiale cartaceo o su altri supporti, in relazione al presente Concorso, senza pretendere alcun compenso, salvo nei casi non consentiti dalla legge.

10. PROBABILITÀ DI VINCITA

    Le probabilità di vincita si basano sul numero e sulla qualità dei contributi idonei pervenuti.

11. CONDIZIONI GENERALI ED ESCLUSIONE DI RESPONSABILITÀ

    Nella misura massima consentita dalla legge, partecipando al Concorso, il Partecipante accetta di sollevare e manlevare Microsoft e i rispettivi partner, dipendenti e agenti, nonché società principali, affiliate e consociate, da qualsiasi responsabilità e da qualsiasi lesione, perdita o danno che potrebbe verificarsi in connessione con il presente Concorso o da qualsiasi premio ricevuto.

    Il Concorso sarà disciplinato dalle leggi locali. Le decisioni di Microsoft sono definitive e vincolanti.

    Microsoft si riserva il diritto di annullare, modificare o sospendere il presente Concorso per qualsiasi motivo, inclusi comportamenti scorretti, guasto tecnico, evento catastrofico, conflitto bellico o qualsiasi altro evento imprevisto, dovuto a errore sia tecnico che umano, che comprometta l'integrità del Concorso. Se non sarà possibile ripristinare l'integrità del Concorso, Microsoft potrà selezionare i vincitori tra tutti i contributi idonei pervenuti prima dell'annullamento, della modifica o della sospensione. I trasgressori del Regolamento saranno perseguiti nella misura massima consentita dalla legge e potranno essere esclusi dalla partecipazione a Concorsi Microsoft.

12. ELENCO DEI VINCITORI

    L'elenco dei vincitori sarà pubblicato sul Web all'indirizzo https://aka.ms/mms2019docathon entro 30 giorni dal 9 maggio 2019.

13. PRIVACY

    Microsoft si impegna a tutelare il diritto alla protezione dei dati personali dei Partecipanti. Microsoft usa le informazioni fornite in questo modulo per comunicare al Partecipante importanti informazioni sui propri prodotti, aggiornamenti e miglioramenti e per inviare informazioni su altri prodotti e servizi Microsoft. Microsoft si impegna a non condividere con terze parti le informazioni fornite dal Partecipante senza previa autorizzazione dello stesso, salvo quando ciò sia necessario per completare le transazioni o i servizi richiesti o in base a quanto stabilito dalla legge. Microsoft si impegna a proteggere la riservatezza delle informazioni personali. usando un'ampia gamma di tecnologie e procedure di sicurezza per proteggere le informazioni personali da accesso, uso o divulgazione non autorizzati. Le informazioni personali del Partecipante non verranno mai condivise all'esterno della società senza previa autorizzazione dello stesso, tranne alle condizioni descritte in precedenza.

    Se si ritiene che Microsoft non abbia rispettato la presente informativa, contattare Microsoft inviando un messaggio tramite posta elettronica all'indirizzo privrc@microsoft.com o tramite il servizio postale all'indirizzo Microsoft Privacy Response Center, Microsoft Corporation, One Microsoft Way, Redmond, WA 98052.