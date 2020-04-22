---
title: Creare aggiornamenti
titleSuffix: Configuration Manager
description: Creare e aggregare aggiornamenti software con System Center Updates Publisher
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 46a1a8ac-126c-4ee6-ae09-32dfbdb83368
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b2445158732f5adf21c43d73b13039f9e41610c8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708699"
---
# <a name="create--software-updates-and-update-bundles-with-updates-publisher"></a>Creare aggiornamenti software e aggiornare aggregazioni con Updates Publisher

*Si applica a: System Center Updates Publisher*

Con Updates Publisher è possibile usare la **Creazione guidata aggiornamento** per creare aggiornamenti e la **Creazione guidata aggregazione** per creare aggregazioni di aggiornamenti.

Poiché queste due procedure guidate hanno un flusso di lavoro simile, la procedura per la creazione di un'aggregazione di aggiornamenti fa riferimento a quella per la creazione di aggiornamenti, con solo le differenze rilevanti dettagliate.

## <a name="use-the-create-update-wizard"></a>Usare la Creazione guidata aggiornamento
1. Nella console passare all'**area di lavoro Aggiornamenti** , quindi, nel riquadro **Operazioni preliminari**, scegliere **Aggiorna** dalla scheda **Home** della barra multifunzione. Viene avviata la **Creazione guidata aggiornamento**.

2. Nella pagina **Pacchetto** usare le informazioni seguenti per configurare l'aggiornamento:

   -   Scegliere **Sfoglia** per individuare il pacchetto di aggiornamento che verrà usato come origine del pacchetto. Le origini valide includono file con estensione msi, msp o exe. Updates Publisher richiede l'accesso al file per creare un hash di file. L'hash e il nome file vengono quindi usati nei metadati dell'aggiornamento per l'aggiornamento in fase di creazione.

   -   Specificare il percorso di origine del contenuto per l'aggiornamento. In genere si tratta del percorso da cui il file binario di aggiornamento verrà scaricato durante la pubblicazione in un server WSUS.  Se è selezionata l'opzione **Use a local source to publish software update content** (Usa un'origine locale per pubblicare il contenuto dell'aggiornamento software), non è richiesto il percorso.

       Successivamente, quando l'aggiornamento viene pubblicato in un server WSUS, Updates Publisher scarica i file binari per l'aggiornamento dal percorso di origine indicato.  Se non viene fornito alcun percorso, Update Publisher cerca il file binario di aggiornamento nel [percorso di pubblicazione di origine locale](updates-publisher-options.md#advanced).

   -   Specificare **Binary language** (Linguaggio binario) per l'aggiornamento software.

   -   Specificare **Success return codes** (Codici restituiti per esito positivo) e **Success pending reboot codes** (Codici di avvio in sospeso per esito positivo) per l'aggiornamento. Separare più codici restituiti mediante una virgola. È possibile usare i codici restituiti per determinare quando l'installazione dell'aggiornamento ha avuto esito positivo e quando è stato necessario un riavvio.

       -   Questi valori, che non possono essere modificati, vengono impostati automaticamente dai file e dalle patch di Windows Installer (file con estensione msi e msp).

       -   Per gli aggiornamenti con estensione exe, se non è specificato alcun codice restituito, vengono usati i codici predefiniti definiti dal file con estensione exe.

   -   Specificare gli eventuali argomenti della riga di comando necessari per installare l'aggiornamento software.

       -   Questi valori vengono impostati automaticamente dai file e dalle patch di Windows Installer (file con estensione msi e msp). Per questi tipi di file gli argomenti devono essere specificati come **\[nome\]=\[valore\]** . Inoltre, tutte le opzioni che iniziano con **/** (ad esempio **/qn**) non sono supportate per gli aggiornamenti software con estensione msi o msp.

       -   Per gli aggiornamenti con estensione exe tutti gli argomenti sono validi.

3. Nella pagina **Informazioni** specificare i dettagli che vengono inclusi al momento della pubblicazione o dell'esportazione dell'aggiornamento. I dettagli includono proprietà localizzate quali il nome (titolo) e la descrizione degli aggiornamenti. Specificare quindi i dettagli più generali, ad esempio la classificazione, il fornitore e il prodotto, e i riferimenti per altre informazioni sull'aggiornamento.

    __Proprietà localizzate:__

   - **Lingua**: selezionare una lingua e quindi specificare un titolo e una descrizione. È quindi possibile selezionare lingue aggiuntive, specificandone una alla volta. Ciascuna lingua supporta i propri titolo e descrizione.

   - **Titolo**: immettere il nome dell'aggiornamento. Questo nome viene visualizzato nell'area di lavoro Aggiornamenti della console di Updates Publisher.

   - **Descrizione**: una breve descrizione dell'aggiornamento. È possibile includere il contenuto installato dall'aggiornamento e specificare il motivo o le situazioni d'uso.

   **Classificazione:** di seguito vengono riportate descrizioni di uso comune per le differenti classificazioni.

   - **Aggiornamento**: aggiornamento di un'applicazione o di un file attualmente installato.

   - **Critico**: aggiornamento rilasciato su vasta scala per un problema specifico e che risolve un bug critico non correlato alla sicurezza.

   - **Feature Pack**: nuove funzionalità del prodotto distribuite al di fuori di una versione del prodotto. In genere sono incluse nella versione successiva del prodotto completo.

   - **Sicurezza**: aggiornamento rilasciato su vasta scala per un problema specifico del prodotto e correlato alla sicurezza.

   - **Aggiornamento cumulativo**: set cumulativo di aggiornamenti rapidi inclusi nello stesso pacchetto per facilitarne la distribuzione. Questi aggiornamenti rapidi possono includere aggiornamenti della sicurezza, aggiornamenti critici, aggiornamenti e così via. Un aggiornamento cumulativo riguarda in genere un'area specifica, ad esempio la sicurezza o una funzionalità del prodotto.

   - **Service Pack**: set cumulativo di aggiornamenti rapidi applicati a un'applicazione. Questi aggiornamenti rapidi possono includere aggiornamenti della sicurezza, aggiornamenti critici, aggiornamenti software e così via.

   - **Strumento**: specifica uno strumento o una funzionalità che consente di completare una o più attività.

   - **Driver**: aggiornamento del software driver.

   **Fornitore**: specificare un fornitore per l'aggiornamento. Per usare i valori di aggiornamenti disponibili nel repository, è possibile usare l'elenco a discesa. Quando si specifica un fornitore, la procedura guidata crea una cartella con lo stesso nome del fornitore sotto **Tutti gli aggiornamenti software** nell'**area di lavoro Aggiornamenti**, se tale cartella non esiste già. Di seguito sono riportati nomi WSUS (Windows Server Update Services) riservati che non è possibile immettere per gli aggiornamenti creati:
   - Microsoft Corporation
   - Microsoft
   - Aggiornamento
   - Aggiornamento software
   - Strumenti
   - Strumento
   - Critico
   - Aggiornamenti critici
   - Sicurezza
   - Aggiornamenti della sicurezza
   - Feature Pack
   - Aggiornamento cumulativo
   - Service Pack
   - Driver
   - Aggiornamento driver
   - Bundle
   - Aggiornamento aggregazione

   **Prodotto**: specificare il tipo di prodotto a cui si applica l'aggiornamento. Per usare i valori di aggiornamenti disponibili nel repository, è possibile usare l'elenco a discesa. I nomi riservati WSUS che non possono essere usati per **Fornitore** non possono essere usati nemmeno per **Prodotto**.

   **More info URL** (URL altre informazioni): specificare l'URL in cui è possibile trovare altre informazioni sull'aggiornamento. Quando si immette l'URL, è necessario usare lettere minuscole per **https** o **http**.

4. Nella pagina **Optional Info** (Informazioni facoltative) è possibile configurare dettagli che forniscono informazioni aggiuntive sull'aggiornamento.

   -   **ID bollettino**: gli ID bollettino vengono in genere, ma non sempre, specificati dai fornitori degli aggiornamenti.

   -   **ID articolo**: se è disponibile l'ID articolo di un aggiornamento software, gli utenti possono usarlo per cercare altre informazioni sull'aggiornamento in questione.

   -   **CVE IDs** (ID CVE): elencare uno o più indicatori CVE (Common Vulnerabilities and Exposures) che offrono informazioni sulla sicurezza per l'aggiornamento o l'aggregazione di aggiornamenti. Quando si elencano più ID CVE, separarli con un punto e virgola, come nell'esempio seguente: *CVE1;CVE2.*

   -   **Support URL** (URL supporto): indicare l'URL in cui sono disponibili informazioni di supporto per l'aggiornamento, se disponibili. Quando si immette l'URL, è necessario usare lettere minuscole per **https** o **http**.

   -   **Gravità**: impostare il livello di gravità per l'aggiornamento.

   -   **Impatto**: per specificare l'impatto è possibile usare le opzioni seguenti:
       -   **Normale**: usare questa opzione per indicare che l'aggiornamento richiede procedure di installazione tipiche.
       -   **Minor** (Secondario): usare questa opzione per indicare che l'aggiornamento richiede procedure di installazione minime.
       -   **Requires exclusive handling** (Richiede gestione esclusiva): usare questa opzione per indicare che l'aggiornamento deve essere installato da solo, separato da altri aggiornamenti.   <br /><br />

   -   **Riavvio del sistema**: usare questa opzione per fornire informazioni sul comportamento del riavvio degli aggiornamenti. Questa impostazione non influisce sul comportamento effettivo dell'installazione dell'aggiornamento.

       -   **Never reboots** (Non riavviare mai): il computer non esegue mai un riavvio del sistema dopo l'installazione dell'aggiornamento software.
       -   **Always requires reboot** (Richiede sempre il riavvio): il computer esegue sempre un riavvio del sistema dopo l'installazione dell'aggiornamento software.
       -   **Can request reboot** (Può richiedere il riavvio): dopo l'installazione dell'aggiornamento software, il computer richiede un riavvio del sistema solo se necessario. L'utente può posticipare il riavvio. Questo è il valore predefinito. <br /><br />

5. Nella pagina **Prerequisito** specificare i prerequisiti che devono essere installati nel computer prima dell'installazione dell'aggiornamento. I prerequisiti possono essere **detectoid** o altri aggiornamenti. I detectoid sono regole di livello elevato, come quella secondo la quale la CPU dei computer deve essere un processore a 64 bit. I detectoid possono anche specificare aggiornamenti che devono essere installati prima dell'aggiornamento.

   -   Per prestazioni ottimali, usare i detectoid ed evitare di creare regole di tipo *installabile* e *installato* che eseguono la stessa azione o lo stesso controllo.

   Usare l'opzione di ricerca **Available software updates and detectoids** (Aggiornamenti software e detectoid disponibili) per trovare aggiornamenti o detectoid specifici. Ad esempio, cercare **CPU** per trovare il detectoid che consente di limitare l'installazione in base alla specifica architettura della CPU.

   È possibile selezionare uno o più elementi alla volta da aggiungere come prerequisito. Durante l'aggiunta di prerequisiti, i detectoid selezionati vengono aggiunti come uno o più gruppi. Un computer viene considerato adatto per l'installazione solo se soddisfa i requisiti di almeno un membro di ciascun gruppo configurato:

   -   Quando si fa clic su **Add Prerequisite** (Aggiungi prerequisito), tutti gli elementi selezionati vengono aggiunti a singoli gruppi separati. Un computer viene considerato adatto per l'aggiornamento solo se soddisfa i prerequisiti del gruppo in questione e quelli di qualsiasi gruppo aggiuntivo configurato.

   -   Quando si fa clic su **Aggiungi gruppo**, tutti gli elementi selezionati vengono aggiunti a un singolo gruppo. Un computer viene considerato adatto per l'aggiornamento solo se soddisfa almeno uno dei prerequisiti del gruppo in questione e quelli di qualsiasi gruppo aggiuntivo configurato.

6. Nella pagina **Sostituzione** specificare gli aggiornamenti che vengono sostituiti dal nuovo aggiornamento. Quando questo aggiornamento viene pubblicato, Configuration Manager contrassegna ogni aggiornamento sostituito come **Scaduto**. I clienti installano quindi questo aggiornamento al posto di quelli sostituiti.

7. Nella pagina **Applicabilità** usare l'**Editor delle regole** per definire un set di regole che determina se un dispositivo necessita dell'aggiornamento. Questa pagina è simile alla pagina **Installato**, che la segue.

   Per aggiungere una nuova regola, fare clic su ![Nuova regola](media/newrule.png). Verrà visualizzata la pagina Applicability Rule (Regola di applicabilità) in cui è possibile configurare le regole.

   I tipi di regole che è possibile creare includono i seguenti:

   -   **File**: usare questa regola per indicare che, per poter eseguire l'aggiornamento, nel dispositivo deve essere presente un file con proprietà che soddisfano uno o più dei criteri specificati.

   -   **Registro di sistema**: usare questo tipo per specificare i dettagli del Registro di sistema che devono essere presenti per consentire l'installazione dell'aggiornamento nel dispositivo.

   -   **Sistema**: questa regola usa i dettagli relativi al sistema per determinare l'applicabilità. È possibile scegliere tra la definizione di una versione di Windows, un linguaggio di Windows o l'architettura del processore. In alternativa, è possibile specificare una query WMI per identificare il sistema operativo dei dispositivi.

   -   **Windows Installer**: usare questa regola per determinare l'applicabilità in base a una patch installata Windows Installer o con estensione msi. È anche possibile determinare se funzionalità o componenti specifici vengono installati come parte del requisito.

       > [!IMPORTANT]  
       > Nel dispositivi gestiti, l'agente di Windows Update non è in grado di rilevare i pacchetti del programma di installazione di Windows installati per utente. Quando si usa questo tipo di regola, configurare regole di applicabilità aggiuntive, come le versioni del file o i valori della chiave del Registro di sistema, in modo che il pacchetto Windows Installer possa essere rilevato correttamente sia in base a un criterio "per utente" che in base a un criterio "per sistema".

   -   **Saved rule** (Regola salvata): questa regola consente di trovare e usare regole *create nell'area di lavoro delle regole*.

       Dopo aver creato una regola, è possibile usare le altre icone per modificare la regola e, se sono presenti più regole, per definire relazioni tra di esse.

   Dopo aver creato e aggiunto le regole, fare clic su **OK** nella finestra di dialogo **Create Rule Set** (Crea set di regole) per salvare il set. È quindi possibile usare l'opzione **Nuova** per creare una regola e aggiungerla al set.

   Quando è necessario aggiungere più regole o set di regole, è possibile usare gli operatori logici nell' **Editor delle regole** per determinare le condizioni tra le regole e il relativo ordine di elaborazione.

8. Nella pagina **Installato** usare l'**Editor delle regole** per definire un set di regole che determinano se in un dispositivo è già stato installato l'aggiornamento che si sta configurando. Questa pagina è simile alla pagina **Applicabilità**, che la precede.

   Questa pagina della procedura guidata supporta regole di configurazione con le stesse opzioni e gli stessi criteri della pagina **Applicabilità**.

   Al termine della procedura guidata, il nuovo aggiornamento viene aggiunto a un nodo nell'**area di lavoro Aggiornamenti** identificato dal nome del **Fornitore** e dal nome del **Prodotto** utilizzati per l'aggiornamento.

## <a name="use-the-create-bundle-wizard"></a>Usare la Creazione guidata aggregazione
Poiché questa procedura guidata usa lo stesso flusso di lavoro della [Creazione guidata aggiornamento](#use-the-create-update-wizard), usare tale flusso di lavoro, ma notare la differenza seguente per le aggregazioni:

1.  Per avviare la procedura guidata, nella console passare all'**area di lavoro Aggiornamenti** e quindi selezionare **Aggregazione** dalla scheda **Home** della barra multifunzione.

2.  A differenza di quanto si verifica nella Creazione guidata aggiornamento, quando si crea un'aggregazione non è presente una pagina Pacchetto.

3.  Nella pagina **Informazioni** specificare i dettagli sull'aggregazione di aggiornamenti che vengono inclusi al momento della pubblicazione o dell'esportazione dell'aggiornamento.

4.  Nella pagina **Optional Info** (Informazioni facoltative) è possibile configurare dettagli che forniscono informazioni aggiuntive sul raggruppamento di aggiornamenti. Si tratta delle stesse opzioni disponibili per la creazione di un aggiornamento. Le opzioni relative a Riavvio del sistema, tuttavia, non sono disponibili e non si applicano alle aggregazioni.

5.  Nella pagina **Prerequisito** specificare i prerequisiti che devono essere installati nel computer prima dell'installazione dell'aggregazione. Si tratta delle stesse regole descritte per gli aggiornamenti individuali.

6.  Nella pagina **Sostituzione** specificare gli aggiornamenti che vengono sostituiti dalla nuova aggregazione di aggiornamenti. Si tratta delle stesse regole descritte per gli aggiornamenti individuali.

7.  Nella pagina **Membri**  selezionare gli aggiornamenti da aggiungere all'aggregazione di aggiornamenti. Sono disponibili solo gli aggiornamenti creati o importati in Updates Publisher.

Al termine della procedura guidata, la nuova aggregazione di aggiornamenti viene aggiunta a un nodo nell'**area di lavoro Aggiornamenti** identificato dal nome del **Fornitore** usato per l'aggregazione di aggiornamenti.
