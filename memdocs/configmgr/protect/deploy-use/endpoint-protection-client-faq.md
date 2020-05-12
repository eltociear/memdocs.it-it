---
title: Domande frequenti relative al client Endpoint Protection
titleSuffix: Configuration Manager
description: Risposte alle domande frequenti su Windows Defender e su Endpoint Protection.
ms.date: 12/09/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e3aaa9d2-a40e-42b1-ad75-5a115351729e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3b206c1556c2e9550ade5c2322acd65ad2b19412
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906839"
---
# <a name="endpoint-protection-client-frequently-asked-questions"></a>Domande frequenti relative al client Endpoint Protection

*Si applica a: Configuration Manager (Current Branch)*


Queste domande frequenti sono destinate a utenti di computer il cui amministratore IT ha distribuito Windows Defender o Endpoint Protection nel computer gestito. Il contenuto illustrato di seguito potrebbe non essere applicabile ad altri software antimalware. Microsoft System Center Endpoint Protection gestisce Windows Defender su Windows 10. Può anche distribuire e gestire il client di Endpoint Protection in computer precedenti Windows 10. Anche se in questo articolo viene descritto Windows Defender, le informazioni si applicano anche a Endpoint Protection.  

-   [Perché è necessario avere un software antivirus e antispyware?](#why-do-i-need-antivirus-and-antispyware-software)  
-   [Come stabilire se il computer è infettato da software dannoso?](#how-can-i-tell-if-my-computer-is-infected-with-malicious-software)
-   [Come si fa a trovare la versione di Windows Defender?](#how-can-i-find-the-version-of-windows-defender)
-   [Cosa è necessario fare se Windows Defender o Endpoint Protection rileva software dannoso nel computer?](#what-should-i-do-if-windows-defender-or-endpoint-protection-detects-malicious-software-on-my-computer)  
-   [Che cos'è un virus?](#what-is-a-virus)  
-   [Che cos'è uno spyware?](#what-is-spyware)  
-   [Qual è la differenza tra virus, spyware e altro software potenzialmente dannoso?](#whats-the-difference-between-viruses-spyware-and-other-potentially-harmful-software)  
-   [Da dove provengono virus, spyware e altro software potenzialmente indesiderato?](#where-do-viruses-spyware-and-other-potentially-unwanted-software-come-from)  
-   [È possibile ricevere software dannoso senza esserne a conoscenza?](#can-i-get-malicious-software-without-knowing-it)  
-   [Perché è importante leggere i contratti di licenza prima di installare software?](#why-is-it-important-to-review-license-agreements-before-installing-software)  
-   [Qual è la differenza tra Endpoint Protection e Windows Defender?](#whats-the-difference-between-endpoint-protection-and-windows-defender)  
-   [Perché Windows Defender non rileva i cookie?](#why-doesnt-windows-defender-detect-cookies)  
-   [Come è possibile evitare il malware?](#how-can-i-prevent-malware)  
-   [Cosa sono le definizioni di virus e spyware?](#what-are-virus-and-spyware-definitions)  
-   [Come mantenere aggiornate le definizioni di virus e spyware?](#how-do-i-keep-virus-and-spyware-definitions-up-to-date)  
-   [Come si rimuovono o si ripristinano gli elementi messi in quarantena da Windows Defender o Endpoint Protection?](#how-do-i-remove-or-restore-items-quarantined-by-windows-defender-or-endpoint-protection)  
-   [Cos'è la protezione in tempo reale?](#what-is-real-time-protection)  
-   [Come si capisce che Windows Defender o Endpoint Protection è in esecuzione nel computer?](#how-do-i-know-that-windows-defender-or-endpoint-protection-is-running-on-my-computer)
-   [Come si configurano gli avvisi di Windows Defender o Endpoint Protection?](#how-to-set-up-windows-defender-or-endpoint-protection-alerts)  

##  <a name="why-do-i-need-antivirus-and-antispyware-software"></a>Perché è necessario un software antivirus e antispyware?  

 È fondamentale verificare che nel computer sia in esecuzione un programma software che protegga da software dannoso. Il software dannoso, che include virus, spyware o altro software potenzialmente indesiderato, può autoinstallarsi nel computer in qualsiasi momento mentre si è connessi a Internet. Può inoltre infettare il computer quando si installa un programma da un CD, un DVD o un altro supporto rimovibile. Il software dannoso può inoltre essere programmato affinché venga eseguito in momenti imprevisti e non quando viene installato.  

 Windows Defender o Endpoint Protection mettono a disposizione tre modi per impedire al software dannoso di infettare il computer:  

-   **Uso della protezione in tempo reale**: la protezione in tempo reale consente a Windows Defender di monitorare costantemente il computer e di avvertire l'utente quando il software dannoso, inclusi virus, spyware o altro software potenzialmente indesiderato, tenta l'installazione o l'esecuzione nel computer. Windows Defender sospende quindi il software e consente di seguire il suggerimento proposto relativo al software o di eseguire un'azione alternativa.

-   **Opzioni di analisi**: è possibile usare Windows Defender per eseguire un'analisi al fine di rilevare potenziali minacce, come ad esempio virus, spyware e altro software dannoso, che potrebbero compromettere la sicurezza del computer. È inoltre possibile pianificare le analisi periodicamente e rimuovere il software dannoso rilevato durante un'analisi.  

-   **Community di Microsoft Active Protection Service**: la community online di Microsoft Active Protection Service consente di verificare il comportamento di altri utenti nei riguardi del software non ancora classificato in relazione ai potenziali rischi. Queste informazioni possono essere utili per decidere se consentire l'installazione di un programma software nel computer. Le proprie scelte verranno quindi aggiunte alle classificazioni della community per fornire agli altri membri un orientamento importante ai fini delle decisioni.  

##  <a name="how-can-i-tell-if-my-computer-is-infected-with-malicious-software"></a>Come stabilire se il computer è infettato da software dannoso  

 Nel computer potrebbe essere presente una qualche forma di software dannoso, tra cui virus, spyware o altro software potenzialmente indesiderato, se:  

-   Si notano barre degli strumenti, collegamenti o Preferiti nuovi non aggiunti intenzionalmente al Web browser.  

-   La pagina iniziale, il puntatore del mouse o il programma di ricerca cambia in modo imprevisto.  

-   Si digita l'indirizzo di un sito specifico, ad esempio un motore di ricerca, ma si passa a un sito Web diverso senza preavviso.  

-   Vengono eliminati automaticamente file dal computer.  

-   Il computer viene usato per attaccare altri computer.  

-   Vengono visualizzati annunci pubblicitari popup, anche se non si è connessi a Internet.  

-   Il computer diventa improvvisamente più lento del solito. Non tutti i problemi di prestazioni del computer sono causati da software dannoso, ma il software dannoso, in particolare lo spyware, può influire in modo significativo.  

Potrebbe essere presente software dannoso nel computer anche senza alcun sintomo. Questo tipo di software può raccogliere informazioni sull'utente e sul computer all'insaputa dell'utente e senza il suo consenso. Per proteggere la privacy di utenti e computer, è consigliabile eseguire sempre Windows Defender o Endpoint Protection.  

## <a name="how-can-i-find-the-version-of-windows-defender"></a>Come si fa a trovare la versione di Windows Defender?
 Per visualizzare la versione di Windows Defender in esecuzione nel computer, aprire Windows Defender (fare clic su **Start** e cercare **Windows Defender**), fare clic su **Impostazioni**, scorrere fino alla fine delle impostazioni di Windows Defender per trovare **Informazioni sulla versione**.

##  <a name="what-should-i-do-if-windows-defender-or-endpoint-protection-detects-malicious-software-on-my-computer"></a>Cosa è necessario fare se Windows Defender o Endpoint Protection rileva software dannoso nel computer?  

 Se Windows Defender rileva software dannoso o potenziamene indesiderato nel computer, sia quando viene eseguito il monitoraggio del computer con la protezione in tempo reale che dopo l'esecuzione di un'analisi, avvisa l'utente dell'elemento rilevato visualizzando un messaggio di notifica nell'angolo in basso a destra dello schermo.  

 Il messaggio di notifica contiene il pulsante **Pulisci computer** e il collegamento **Mostra dettagli** che consente di visualizzare ulteriori informazioni sull'elemento rilevato. Fare clic sul collegamento **Mostra dettagli** per aprire la finestra **Dettagli minaccia potenziale** per ottenere altre informazioni sull'elemento rilevato. È quindi possibile scegliere l'azione da applicare all'elemento o fare clic su **Pulisci computer**. Per determinare più facilmente l'azione da applicare all'elemento rilevato, è possibile usare come guida il livello di attenzione assegnato da Windows Defender all'elemento. Per altre informazioni, vedere Informazioni sui livelli di avviso.  

 I livelli di avviso consentono di scegliere come rispondere ai virus, spyware e ad altri software potenzialmente indesiderati. Anche se Windows Defender in genere consiglia di rimuovere tutti i virus e gli spyware, non tutto il software contrassegnato è dannoso o indesiderato. Le informazioni seguenti sono utili per definire l'azione da intraprendere nel caso in cui Windows Defender rilevi la presenza di software potenzialmente indesiderato nel computer.  

 In base al livello di attenzione è possibile scegliere una delle azioni seguenti da applicare all'elemento rilevato:  

- **Rimuovi**: questa azione consente di eliminare permanentemente il software dal computer.  

- **Quarantena**: questa azione consente di mettere in quarantena il software in modo da impedirne l'esecuzione. Quando Windows Defender mette il software in quarantena, lo sposta in una posizione diversa del computer impedendone l'esecuzione finché l'utente non sceglie se ripristinarlo o rimuoverlo dal computer.  

- **Consenti**: questa azione aggiunge il software all'elenco dei software consentiti di Windows Defender e ne consente l'esecuzione nel computer. Windows Defender non avviserà più l'utente dei rischi posti dal software per la privacy o la sicurezza del computer.  

  Se si sceglie **Consenti** per un elemento, ad esempio un programma software, Windows Defender non avviserà più l'utente dei rischi posti dal software per la privacy dell'utente o la sicurezza del computer. Inserire pertanto un software nell'elenco degli elementi consentiti solo se si considera attendibile il software e il relativo autore.  

### <a name="how-to-remove-potentially-harmful-software"></a>Come rimuovere software potenzialmente dannoso

Per rimuovere facilmente e velocemente tutti gli elementi indesiderati o potenzialmente dannosi rilevati da Windows Defender, usare l'opzione **Pulisci computer** .  

1.  Fare clic su **Pulisci computer**nel messaggio visualizzato nell'area di notifica dopo che Windows Defender ha rilevato minacce potenziali.  

2.  Windows Defender rimuove tutte le minacce potenziali e avvisa l'utente al termine dell'operazione.  

3.  Per ulteriori informazioni sulle minacce rilevate, fare clic sulla scheda **Cronologia** , quindi selezionare **Tutti gli elementi rilevati**.  

4.  Se non vengono visualizzati tutti gli elementi rilevati, fare clic su **Visualizza dettagli**. Se viene richiesta una password di amministratore o una conferma, digitare la password o confermare l'azione.

> [!NOTE]  
>  Durante la pulizia del computer, laddove possibile, Windows Defender rimuove solo la parte infetta di un file e non tutto il file.  

##  <a name="what-is-a-virus"></a>Che cos'è un virus?  
 I virus sono programmi software deliberatamente progettati per interferire con le attività del computer, per registrare, danneggiare o eliminare dati o per infettare altri computer su Internet. I virus causano spesso rallentamenti e altri problemi nel processo.  

##  <a name="what-is-spyware"></a>Che cos'è uno spyware?  
 Lo spyware è software che può autoinstallarsi o essere eseguito automaticamente nel computer senza ottenere il consenso dell'utente oppure fornire segnalazioni o misure di controllo adeguate. I computer infettati da spyware potrebbero non presentare alcun sintomo, ma molti programmi dannosi o indesiderati possono influire sul funzionamento del computer. Ad esempio, i programmi spyware possono monitorare il comportamento online o raccogliere informazioni personali dell'utente (comprese le informazioni che consentono di identificare l'utente o altre informazioni riservate), modificare le impostazioni del computer o causarne il rallentamento.  

##  <a name="whats-the-difference-between-viruses-spyware-and-other-potentially-harmful-software"></a>Qual è la differenza tra virus, spyware e altro software potenzialmente dannoso?  
 Sia virus che spyware vengono installati nel computer a insaputa dell'utente ed entrambi sono potenzialmente intrusivi e distruttivi. Sono anche in grado di acquisire informazioni nel computer e danneggiare o eliminare tali informazioni. Entrambi possono influire negativamente sulle prestazioni del computer.  

 Le differenze principali tra virus e spyware è il comportamento nel computer. I virus, come per gli organismi viventi, hanno lo scopo di infettare un computer, replicarsi e quindi diffondersi nel maggior numero di computer possibile. Lo spyware, invece, può essere paragonato a una talpa: il suo scopo è intrufolarsi nel computer e rimanerci il più a lungo possibile, inviando informazioni importanti sul computer a un'origine esterna.  

##  <a name="where-do-viruses-spyware-and-other-potentially-unwanted-software-come-from"></a>Da dove provengono virus, spyware e altro software potenzialmente indesiderato?  
 Il software indesiderato, come i virus, può essere installato da siti Web o da programmi scaricati o installati tramite CD, DVD, dischi rigidi esterni o dispositivi. Lo spyware viene in genere installato tramite software gratuito, ad esempio strumenti di condivisione file, screen saver o barre degli strumenti di ricerca.  

##  <a name="can-i-get-malicious-software-without-knowing-it"></a>È possibile ricevere software dannoso senza esserne a conoscenza?  
 Sì, alcuni software dannosi possono essere installati da un sito Web tramite uno script o un programma incorporato in una pagina Web. Alcuni malware richiedono l'intervento dell'utente per l'installazione. Questo software usa popup Web o software gratuito che richiede di accettare un file scaricabile. Tuttavia, se si mantiene aggiornato Microsoft Windows® e non si riducono le impostazioni di sicurezza, è possibile ridurre al minimo il rischio di infezioni.  

##  <a name="why-is-it-important-to-review-license-agreements-before-installing-software"></a>Perché è importante leggere i contratti di licenza prima di installare software?  
 Quando si visitano siti Web, non accettare automaticamente di scaricare qualsiasi cosa offerta dal sito. Se si scarica software gratuito, come programmi per la condivisione di file o screen saver, leggere attentamente il contratto di licenza. Controllare se sono presenti clausole che indicano che è obbligatorio accettare annunci pubblicitari e popup dell'azienda o che il software invierà determinate informazioni all'autore del software.  

##  <a name="whats-the-difference-between-endpoint-protection-and-windows-defender"></a>Qual è la differenza tra Endpoint Protection e Windows Defender?  
 Endpoint Protection è un software antimalware, ovvero è progettato per rilevare e proteggere il computer da un'ampia gamma di software dannoso, tra cui virus, spyware e altro software potenzialmente indesiderato. Windows Defender, installato automaticamente con il sistema operativo Windows, è un software progettato per il rilevamento e la rimozione di spyware.  

##  <a name="why-doesnt-windows-defender-detect-cookies"></a>Perché Windows Defender non rileva i cookie?  
 I cookie sono piccoli file di testo inseriti dai siti Web nel computer per archiviare informazioni relative all'utente e alle sue preferenze. I siti Web usano i cookie per offrire un'esperienza personalizzata e raccogliere informazioni sull'uso del sito Web. Windows Defender non rileva i cookie perché non li considera un rischio per la privacy degli utenti o per la sicurezza del computer. La maggior parte dei browser Internet consente di bloccare i cookie.  

##  <a name="how-can-i-prevent-malware"></a>Come è possibile evitare il malware?  
 Due delle principali preoccupazioni per gli utenti dei computer sono oggi virus e spyware. In entrambi i casi, anche se possono rappresentare un problema, è possibile difendersi abbastanza facilmente con un minimo di pianificazione:  

-   Mantenere aggiornato il software del computer e ricordarsi di installare tutte le patch. Ricordarsi di aggiornare regolarmente il sistema operativo.  

-   Assicurarsi che il software antivirus e antispyware, Windows Defender, usi gli aggiornamenti più recenti dalle potenziali minacce (vedere Come mantenere aggiornate le definizioni di virus e spyware). Assicurarsi inoltre di usare sempre la versione più recente di Windows Defender.  

-   Scaricare aggiornamenti solo da fonti attendibili. Per i sistemi operativi Windows usare sempre il [catalogo Microsoft Update](https://catalog.update.microsoft.com).  Per altri prodotti software usare sempre i siti Web ufficiali della società o dell'utente che li produce.

-   Se si riceve un messaggio di posta elettronica con un allegato e non si è certi dell'origine, è opportuno eliminarlo immediatamente. Non scaricare applicazioni o file eseguibili da origini sconosciute e prestare attenzione nello scambio di file con altri utenti.  

-   Installare e usare un firewall. Si consiglia di abilitare Windows Firewall.  

##  <a name="what-are-virus-and-spyware-definitions"></a>Informazioni sulle definizioni di virus e spyware  
 Quando si usa Windows Defender o Endpoint Protection, è importante disporre di definizioni di virus e spyware aggiornate. Le definizioni sono file che operano come un'enciclopedia delle potenziali minacce software aggiornata costantemente. Windows Defender o Endpoint Protection usano le definizioni per stabilire se il software rilevato è un virus, spyware o altro software potenzialmente indesiderato, quindi per avvisare in caso di rischi potenziali. Per mantenere aggiornate le definizioni, Windows Defender o Endpoint Protection è integrato con Microsoft Update per installare automaticamente le nuove definizioni non appena vengono rilasciate. È anche possibile impostare Windows Defender o Endpoint Protection per controllare online se sono disponibili definizioni aggiornate prima dell'analisi.  

##  <a name="how-do-i-keep-virus-and-spyware-definitions-up-to-date"></a>Come mantenere aggiornate le definizioni di virus e spyware  
 Le definizioni di virus e spyware sono file che operano come un'enciclopedia del software dannoso noto, tra cui virus, spyware e altro software potenzialmente indesiderato. Dato che viene continuamente sviluppato nuovo malware, Windows Defender o Endpoint Protection si basa su definizioni aggiornate per determinare se il software che sta tentando di installare, eseguire o modificare le impostazioni del computer è un virus, spyware o altro software potenzialmente indesiderato.  

### <a name="to-automatically-check-for-new-definitions-before-scheduled-scans-recommended"></a>Per verificare automaticamente la disponibilità di nuove definizioni prima delle analisi pianificate (operazione consigliata)  

1.  Aprire Windows Defender o il client Endpoint Protection facendo clic sull'icona nell'area di notifica o avviandolo dal menu **Start** .  

2.  Fare clic su **Impostazioni**e quindi su **Analisi pianificata**.  

3.  Assicurarsi che la casella di controllo **Verifica la disponibilità di definizioni di virus e spyware più recenti prima di eseguire l'analisi pianificata** sia selezionata e quindi fare clic su **Salva modifiche**. Se viene richiesta una password di amministratore o una conferma, digitare la password o confermare l'azione.  

### <a name="to-check-for-new-definitions-manually"></a>Per verificare manualmente la disponibilità di nuove definizioni

 Windows Defender o Endpoint Protection aggiorna automaticamente le definizioni di virus e spyware nel computer. Se le definizioni non sono state aggiornate per più di sette giorni, ad esempio se il computer è rimasto spento per una settimana, Windows Defender o Endpoint Protection segnaleranno che le definizioni non sono aggiornate.  

1.  Aprire Windows Defender o il client Endpoint Protection facendo clic sull'icona nell'area di notifica o avviandolo dal menu **Start** .  

2.  Per verificare manualmente la disponibilità di nuove definizioni, fare clic sulla scheda **Aggiorna** e quindi su **Aggiorna definizioni**.  

##  <a name="how-do-i-remove-or-restore-items-quarantined-by-windows-defender-or-endpoint-protection"></a>Come si rimuovono o si ripristinano gli elementi messi in quarantena da Windows Defender o Endpoint Protection?  

 Quando Windows Defender o Endpoint Protection mette il software in quarantena, lo sposta in una posizione diversa del computer impedendone l'esecuzione finché l'utente non sceglie se ripristinarlo o rimuoverlo dal computer.  

 Se nei passaggi di questa procedura viene richiesta una password di amministratore o una conferma, digitare la password o fornire la conferma.  

###  <a name="to-remove-or-restore-items-quarantined-by-windows-defender-or-endpoint-protection"></a>Per rimuovere o ripristinare gli elementi messi in quarantena da Windows Defender o Endpoint Protection


1.  Fare clic sulla scheda **Cronologia** , selezionare **Elementi in quarantena**e quindi selezionare l'opzione **Elementi in quarantena** .  

2.  Fare clic su **Visualizza dettagli** per visualizzare tutti gli elementi.  

3.  Esaminare tutti gli elementi, quindi fare clic su **Rimuovi** o **Ripristina**per ognuno di essi. Se si desidera rimuovere tutti gli elementi in quarantena dal computer, fare clic su **Rimuovi tutto**.  

##  <a name="what-is-real-time-protection"></a>Cos'è la protezione in tempo reale?  

 La protezione in tempo reale consente a Windows Defender monitorare costantemente il computer e segnalare la presenza di potenziali minacce, quali virus e spyware che tentano l'installazione o l'esecuzione nel computer. Dato che questa funzionalità è un elemento importante del modo in cui Windows Defender protegge il computer, assicurarsi che la protezione in tempo reale sia sempre attivata. Se la protezione in tempo reale viene disattivata, Windows Defender lo segnala e imposta lo stato del computer su **A rischio**.  

 Se la protezione in tempo reale rileva una minaccia o una potenziale minaccia, Windows Defender visualizza una notifica. È quindi possibile scegliere una delle opzioni seguenti:  

- Fare clic su **Pulisci computer** per rimuovere l'elemento rilevato. Windows Defender rimuoverà automaticamente l'elemento dal computer.  

- Fare clic sul collegamento **Mostra** dettagli per visualizzare la finestra Dettagli rischi potenziali e quindi scegliere l'azione da applicare all'elemento rilevato.  

  È possibile scegliere il software e le impostazioni che si vuole monitorare con Windows Defender, ma è consigliabile attivare la protezione in tempo reale e abilitare tutte le opzioni di protezione in tempo reale. La tabella seguente illustra le opzioni disponibili.  

|||  
|-|-|  
|**Opzione di protezione in tempo reale**|**Scopo**|  
|Analizza tutti i download|Questa opzione consente di monitorare i file e i programmi scaricati, inclusi i file scaricati automaticamente tramite Windows Internet Explorer e Microsoft Outlook® Express, ad esempio i controlli ActiveX® e i programmi di installazione software. Questi file possono essere scaricati, installati o eseguiti dal browser stesso. Software dannoso, tra cui virus, spyware e altro software potenzialmente indesiderato, può essere incluso in questi file e installato all'insaputa dell'utente.<br /><br /> Con l'opzione di protezione in tempo reale, Windows Defender mantiene costantemente monitorato il computer e controlla l'eventuale presenza di file o programmi dannosi che potrebbero essere stati scaricati. Questa funzionalità di monitoraggio significa che Windows Defender non deve rallentare l'esperienza di esplorazione o per la posta elettronica richiedendo un controllo di tutti i file o programmi da scaricare.|  
|Monitoraggio dell'attività di file e programmi nel computer|Questa opzione consente di monitorare i file e programmi in esecuzione nel computer e quindi genera avvisi per le eventuali azioni eseguite da tali file e programmi e le azioni eseguite su di essi. Si tratta di un aspetto importante, perché il software dannoso può sfruttare le vulnerabilità nei programmi installati per eseguire software dannoso o indesiderato all'insaputa dell'utente. Ad esempio, un programma spyware può attivarsi automaticamente in background all'avvio di un programma usato di frequente. Windows Defender mantiene monitorati i programmi e genera avvisi se rileva attività sospette.|  
|Abilita monitoraggio del comportamento|Questa opzione consente di monitorare raccolte di comportamenti per individuare modelli sospetti che potrebbero non essere rilevati dai metodi di rilevamento antivirus tradizionali.|  
|Abilita Network Inspection System|Questa opzione consente di proteggere il computer dagli exploit zero-day delle vulnerabilità note, riducendo il periodo di tempo tra l'individuazione di una vulnerabilità e l'applicazione di un aggiornamento.|  

### <a name="to-turn-off-real-time-protection"></a>Per disattivare la protezione in tempo reale  

1.  Fare clic su **Impostazioni**, quindi su **Protezione in tempo reale**.  

2.  Deselezionare le opzioni di protezione in tempo reale da disattivare e quindi fare clic su **Salva modifiche**. Se viene richiesta una password di amministratore o una conferma, digitare la password o confermare l'azione.  

##  <a name="how-do-i-know-that-windows-defender-or-endpoint-protection-is-running-on-my-computer"></a>Come si capisce che Windows Defender o Endpoint Protection è in esecuzione nel computer?  

 Dopo aver installato Windows Defender nel computer, è possibile chiudere la finestra principale e lasciare che Windows Defender venga eseguito in background. Windows Defender rimarrà in esecuzione nel computer, monitorandolo e proteggendolo dalle minacce.  

 Si noterà naturalmente l'esecuzione di Windows Defender ogni volta che viene visualizzata una notifica nell'area di notifica. Queste notifiche avvisano l'utente delle minacce potenziali rilevate da Windows Defender.  

 Verranno anche visualizzate notifiche di avviso di tipo diverso, ad esempio nel caso in cui per qualche motivo è stata disattivata la protezione in tempo reale o non è stato eseguito l'aggiornamento delle definizioni di virus e spyware per alcuni giorni oppure se sono disponibili aggiornamenti del programma. Windows Defender visualizza brevemente una notifica anche per segnalare che è in corso l'analisi del computer.  

> [!TIP]
> 
> Se l'icona di Windows Defender non viene visualizzata, fare clic sulla freccia nell'area di notifica per visualizzare le icone nascoste, compresa l'icona di Windows Defender.  


 Il colore dell'icona dipende dallo stato corrente del computer:  

-   Verde indica che lo stato del computer è "protetto".  

-   Giallo indica che lo stato del computer è "potenzialmente non protetto".  

-   Rosso indica che lo stato del computer è "a rischio".  

##  <a name="how-to-set-up-windows-defender-or-endpoint-protection-alerts"></a>Come si configurano gli avvisi di Windows Defender o Endpoint Protection?  
 Quando Windows Defender è in esecuzione nel computer, l'utente viene avvisato automaticamente se vengono rilevati virus, spyware o altro software potenzialmente indesiderato. È inoltre possibile impostare Windows Defender in modo da essere avvisati se viene eseguito software non ancora analizzato ed è possibile scegliere di essere avvisati qualora il software apporti modifiche al computer.  

### <a name="to-set-up-alerts"></a>Per configurare gli avvisi  

1.  Fare clic su **Impostazioni**, quindi su **Protezione in tempo reale**.  

2.  Accertarsi che sia selezionata la casella di controllo **Attiva protezione in tempo reale (opzione consigliata)** .  

3.  Selezionare le caselle di controllo accanto alle opzioni della protezione in tempo reale che si desidera eseguire, quindi fare clic su **Salva modifiche**. Se viene richiesta una password di amministratore o una conferma, digitare la password o confermare l'azione.  

### <a name="see-also"></a>Vedere anche  
 [Troubleshooting Windows Defender or Endpoint Protection client](troubleshoot-endpoint-client.md) (Risoluzione dei problemi di Windows Defender o del client di Endpoint Protection)   

 [Guida del client di Endpoint Protection](endpoint-protection-client-help.md)
