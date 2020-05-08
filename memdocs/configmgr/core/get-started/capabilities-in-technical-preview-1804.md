---
title: Technical Preview 1804
titleSuffix: Configuration Manager
description: Informazioni sulle nuove funzionalità disponibili in Configuration Manager Technical Preview versione 1804.
ms.date: 05/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8af43618-ec60-4c3e-a007-12399d1335b9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: b709d6ec0c0cda188502c314d945a70e8de71288
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905242"
---
# <a name="capabilities-in-technical-preview-1804-for-configuration-manager"></a>Funzionalità della versione Technical Preview 1804 per Configuration Manager

*Si applica a: Configuration Manager (Technical Preview Branch)*

Questo articolo presenta le funzionalità disponibili nella Technical Preview per Configuration Manager, versione 1804. È possibile installare questa versione per aggiornare il sito delle anteprime tecniche aggiungendovi nuove funzionalità. 

Prima di installare questo aggiornamento, vedere l'articolo [Technical Preview](technical-preview.md). L'articolo consente di acquisire familiarità con i requisiti e le limitazioni generali per l'uso di una Technical Preview, con l'aggiornamento tra le versioni e con l'invio di commenti e suggerimenti.     


<!--  Known Issues Template   -->
## <a name="known-issues-in-this-technical-preview"></a>Problemi noti di questa versione Technical Preview

### <a name="setup-link-to-download-updates-not-working"></a><a name="bkmk_ki-prereqs"></a> Il collegamento di installazione per scaricare gli aggiornamenti non funziona
<!--514334-->
Se si esegue l'installazione dal supporto, la pagina iniziale include il collegamento **Get the latest Configuration Manager updates** (Ottieni gli ultimi aggiornamenti di Configuration Manager) che non funziona in questa versione. Questo collegamento consente di scaricare i file necessari per l'installazione.

#### <a name="workaround"></a>Soluzione alternativa
Per scaricare i file necessari per l'installazione, eseguire l'installazione guidata. Nella pagina Download prerequisiti usare l'opzione **Scarica file richiesti**. 


### <a name="the-application-catalog-web-service-point-cant-be-https-enabled"></a><a name="bkmk_appcathttps"></a> Il punto per servizi Web del Catalogo applicazioni non può essere abilitato per HTTPS
<!--512637-->
Se il punto per servizi Web del Catalogo applicazioni è abilitato per HTTPS:

- Le applicazioni distribuite come disponibili per gli utenti non sono visualizzate in Software Center  

- In awebsctl.log viene registrato l'errore seguente:  

     `Call to HttpSendRequestSync failed for port 443 with status code 500, text: Internal Server Error`

#### <a name="workaround"></a>Soluzione alternativa
Riconfigurare il punto per servizi Web del Catalogo applicazioni per la comunicazione tramite connessioni HTTP.  




</br>

**Di seguito sono riportate le nuove funzionalità disponibili con questa versione.**  


## <a name="configure-a-remote-content-library-for-the-site-server"></a>Configurare una raccolta contenuto remota per il server del sito  
<!--1357525-->
Per liberare spazio sul disco rigido nel server del sito primario, spostare la relativa [raccolta contenuto](../plan-design/hierarchy/the-content-library.md) in un'altra posizione di archiviazione. È possibile spostare la raccolta contenuto in un'altra unità sul server del sito, un server distinto o dischi a tolleranza di errore in una rete di archiviazione (SAN). È consigliabile una SAN perché fornisce uno spazio di archiviazione elastico, che può aumentare o ridursi nel tempo per soddisfare i requisiti del contenuto. 

Questa raccolta contenuto remota è un nuovo prerequisito per la [disponibilità elevata dei ruoli del server del sito](capabilities-in-technical-preview-1706.md#site-server-role-high-availability). 

> [!Note]  
> Questa azione sposta solo la raccolta contenuto nel server del sito. Non influisce sulla posizione della raccolta contenuto nei punti di distribuzione. 

### <a name="prerequisites"></a>Prerequisiti  
- L'account computer del server del sito deve disporre di autorizzazioni di **lettura** e **scrittura** per il percorso di rete in cui deve essere spostata la raccolta contenuto. Non sono installati componenti nel sistema remoto. 

### <a name="try-it-out"></a>Verifica
 Provare a completare le attività. Inviare quindi [commenti e suggerimenti](#bkmk_feedback).

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**. Espandere **Configurazione del sito** e selezionare **Siti**. Nella scheda **Riepilogo** nella parte inferiore del riquadro dei dettagli è visibile una nuova colonna **Raccolta contenuto**.  

2. Fare clic su **Gestisci la raccolta contenuto** sulla barra multifunzione.  

3. Selezionare **On a network share** (In una condivisione di rete) e immettere un percorso di rete valido. Questo percorso è la posizione in cui il sito sposta la raccolta contenuto. Fare clic su **OK**.  

4. Si noti la proprietà **Stato** nella colonna Raccolta contenuto nel riquadro dei dettagli. Viene aggiornata per mostrare lo stato di avanzamento del sito durante lo spostamento della raccolta contenuto. Quando lo spostamento è in corso, viene visualizzata la percentuale di completamento. Se è presente uno stato di errore, viene visualizzato l'errore. Gli errori tipici comprendono `access denied` o `disk full`. Al termine, viene visualizzato `OK`. Per informazioni dettagliate, vedere **distmgr.log**. Per altre informazioni, vedere [Log del server del sito e del server di sistema del sito](../plan-design/hierarchy/log-files.md#BKMK_SiteSiteServerLog).  

Se è necessario spostare nuovamente la raccolta contenuto nel server del sito, ripetere questo processo, ma selezionare l'opzione **Local to the site server** (Locale nel server del sito).  

> [!Tip]  
> Per spostare il contenuto in un'altra unità nel server del sito, usare lo **strumento per il trasferimento di raccolte di contenuto**. Per altre informazioni, vedere [Configuration Manager Toolkit](#configuration-manager-toolkit).  



## <a name="submit-feedback-from-the-configuration-manager-console"></a><a name="bkmk_feedback"></a> Inviare commenti e suggerimenti dalla console di Configuration Manager  
<!--1357542-->

Commenti e suggerimenti Ora è possibile comunicare direttamente al team di Configuration Manager le proprie esperienze. Inviare commenti e suggerimenti dalla console di Configuration Manager è molto semplice. Siamo interessati a ogni tipo di feedback: apprezzamenti, problemi e suggerimenti.  

### <a name="try-it-out"></a>Verifica
 Provare a completare le attività. Inviare quindi **commenti e suggerimenti**.  

1. Nella console di Configuration Manager fare clic sul pulsante Smile nell'angolo superiore destro sopra la barra multifunzione.  

2. Nell'elenco a discesa selezionare una delle opzioni disponibili:  

   - **Invia smile**: questa opzione consente di esprimere apprezzamento per un particolare elemento. Per questa opzione, immettere i dettagli relativi al feedback, quindi includere uno screenshot e l'indirizzo di posta elettronica (facoltativo).  

   - **Invia faccia imbronciata**: si è verificato un problema nella console o un determinato elemento non ha funzionato come previsto. Per questa opzione, immettere i dettagli del potenziale problema del prodotto, quindi includere uno screenshot, l'indirizzo di posta elettronica e i dati di diagnostica (facoltativo).  

   - **Invia un suggerimento**: questa opzione consente di proporre un'idea per modificare e migliorare Configuration Manager. Verrà aperto il sito [UserVoice](https://configurationmanager.uservoice.com) nel Web browser.  

Questi commenti e suggerimenti vengono inviati direttamente al team del prodotto Microsoft per Configuration Manager. Anche se l'uso dell'Hub di Feedback di Windows 10 è ancora supportato, è consigliabile usare il meccanismo per l'invio di feedback disponibile nella console.  

Le seguenti informazioni anonime vengono sempre incluse con il feedback per il contesto:  

- Versione e lingua della console di Configuration Manager  

- Versione del sito di Configuration Manager  

- ID supporto, noto anche come ID gerarchia  

- Versione e lingua del sistema operativo per il sistema in cui è in esecuzione la console  

- Posizione esatta nella console da cui è stato fatto clic sullo smile  

Questi dati sono coerenti con la raccolta dei dati di utilizzo e di diagnostica. Per altre informazioni, vedere [Diagnostica e dati di utilizzo](../plan-design/diagnostics/diagnostics-and-usage-data.md).

### <a name="known-issues"></a>Problemi noti

Se si tenta di inviare feedback da un dispositivo che non è in grado di accedere a Internet, è possibile che l'applicazione venga chiusa in modo imprevisto. Per inviare uno smile o una faccia imbronciata, assicurarsi che il dispositivo sia in grado di accedere a petrol.office.microsoft.com.



## <a name="support-center"></a>Support Center
<!--1357489-->

Usare Support Center per la risoluzione dei problemi dei client, la visualizzazione dei log in tempo reale o l'acquisizione dello stato di un computer client di Configuration Manager per l'analisi successiva. Support Center è un singolo strumento che consolida numerosi strumenti di risoluzione dei problemi per gli amministratori. Nella Technical Preview sono disponibili le anteprime della versione più recente di Support Center, con correzioni di bug e miglioramenti, e del nuovo visualizzatore di log. Il programma di installazione di Support Center è disponibile nel server del sito, nella cartella **cd.latest\SMSSETUP\Tools\SupportCenter**.


### <a name="new-support-center-features"></a>Nuove funzionalità di Support Center  

- Un nuovo visualizzatore di log, OneTrace. Funziona in modo simile a CMTrace e include miglioramenti come una visualizzazione a schede e finestre ancorabili.  

- Una nuova funzionalità dell'agente di raccolta dati raccoglie i log di diagnostica da un client Configuration Manager locale o remoto. Fornisce funzionalità di diagnostica in tempo reale dell'inventario (sostituisce Client Spy), dei criteri (sostituisce Policy Spy) e della cache del client.  



## <a name="configuration-manager-toolkit"></a>Configuration Manager Toolkit
<!--1357145-->

Gli strumenti server e client di Configuration Manager ora sono inclusi con la versione Technical Preview. Sono disponibili nella cartella **cd.latest\SMSSETUP\Tools** nel server del sito. Non è necessaria un'ulteriore installazione.

#### <a name="server-tools"></a>Strumenti server  

- **DP Job Manager**: consente di risolvere i problemi dei processi di distribuzione del contenuto ai punti di distribuzione  

- **Collection Evaluation Viewer**: consente di visualizzare informazioni dettagliate sulla valutazione della raccolta  

- **Content Library Explorer**: consente di visualizzare il contenuto dell'archivio a istanza singola della raccolta contenuto  

- **Content Library Transfer**: trasferisce la raccolta contenuto tra diverse unità  

- **Content Ownership Tool**: modifica la proprietà dei pacchetti orfani. Questi pacchetti sono presenti nel sito senza un server del sito proprietario.  

- **Role-based Administration and Auditing Tool**: consente agli amministratori di controllare la configurazione dei ruoli  

#### <a name="client-tools"></a>Strumenti client

- **CMTrace**: consente di visualizzare i log  

- **Deployment Monitoring Tool**: consente di risolvere i problemi di applicazioni, aggiornamenti e distribuzioni delle linee di base  

- **Policy Spy**: consente di visualizzare le assegnazioni dei criteri  

- **Power Viewer Tool**: consente di visualizzare lo stato della funzionalità di risparmio energia  

- **Send Schedule Tool**: consente di attivare pianificazioni e valutazioni delle linee di base DCM  

> [!Important]  
> [Support Center](#support-center) è consigliato per la maggior parte casi d'uso, perché include le stesse funzionalità o funzionalità migliorate per gli strumenti seguenti:  
> - Client Spy
> - CMTrace<sup>1</sup> 
> - Deployment Monitoring Tool
> - Policy Spy
> - Send Schedule Tool
> 
> <sup>1</sup> CMTrace non dipende da .NET o Windows Presentation Foundation (WPF), pertanto viene ancora usato nelle immagini di avvio Windows PE.

### <a name="known-issues"></a>Problemi noti
Alcuni strumenti per client e server possono chiudersi in modo imprevisto all'avvio. Questo problema è dovuto a un file mancante nei supporti. Per ovviare a questo problema, copiare il file **Microsoft.Diagnostics.Tracing.EventSource.dll** dalla directory AdminConsole\bin in entrambe le directory SMSSETUP\Tools\ClientTools e ServerTools. La versione di questo file deve essere la stessa di quella usata dalla console di Configuration Manager. Altre versioni potrebbero non funzionare. <!--513977-->



## <a name="uninstall-application-on-approval-revocation"></a>Disinstallare l'applicazione in caso di revoca dell'approvazione
<!--1357891-->

Quando si revoca l'approvazione per un'applicazione, il comportamento è stato modificato. Ora, quando si nega la richiesta per l'applicazione, il client disinstalla l'applicazione dal dispositivo dell'utente. 

### <a name="prerequisites"></a>Prerequisiti
- Abilitare la funzionalità **Approvazione delle richieste di applicazioni degli utenti per dispositivo**.

### <a name="try-it-out"></a>Verifica
 Provare a completare le attività. Inviare quindi [commenti e suggerimenti](#bkmk_feedback).

1. Nella console di Configuration Manager distribuire a un utente un'applicazione che richiede l'approvazione. Nella scheda **Impostazioni di distribuzione** della distribuzione abilitare l'opzione **Un amministratore deve approvare una richiesta per questa applicazione nel dispositivo**.  

2. Nel client di Configuration Manager in Software Center l'utente richiede l'approvazione per installare l'applicazione.  

3. Nella console di Configuration Manager approvare la richiesta per l'installazione dell'applicazione nel dispositivo da parte dell'utente. Le richieste di approvazione dell'applicazione vengono visualizzate nell'area di lavoro **Raccolta software**, in **Gestione applicazioni**, nel nodo **Richieste di approvazione**.  

4. Nel client in Software Center l'utente installa l'applicazione.  

5. Nella console di Configuration Manager negare la richiesta per l'installazione dell'applicazione nel dispositivo da parte dell'utente.  

### <a name="known-issues"></a>Problemi noti
- Dopo che l'utente ha installato l'applicazione nel client, aggiornare i criteri utente. In Software Center passare alla scheda **Opzioni**, espandere **Manutenzione computer** e fare clic su **Criteri sincronizzazione**.<!--480609-->  

- Il punto per servizi Web del Catalogo applicazioni deve essere HTTP. Per altre informazioni, vedere [Problemi noti di questa versione Technical Preview](#bkmk_appcathttps).<!--512637-->  



## <a name="exclude-active-directory-containers-from-discovery"></a>Escludere i contenitori di Active Directory dall'individuazione
<!--1358143-->
Per ridurre il numero degli oggetti individuati, ora è possibile escludere specifici contenitori da Individuazione sistema Active Directory. Questa funzionalità è il risultato dei [commenti e suggerimenti raccolti tramite UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8414520-exclude-virtual-cluster-and-ou-from-discovery).

### <a name="try-it-out"></a>Verifica
 Provare a completare le attività. Inviare quindi [commenti e suggerimenti](#bkmk_feedback).

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**. Espandere **Configurazione della gerarchia** e selezionare **Metodi di individuazione**. Selezionare **Individuazione sistema Active Directory** e fare clic su **Proprietà** nella barra multifunzione.  

2. Fare clic sull'icona Nuovo per specificare un nuovo contenitore di Active Directory.   

3. Nella finestra di dialogo Contenitore Active Directory selezionare o immettere il **percorso** nella sezione Posizione per avviare l'individuazione.  

4. Nella sezione Opzioni di ricerca abilitare l'opzione **Esegui ricerca ricorsiva nei contenitori figlio di Active Directory**. Fare quindi clic su **Aggiungi** per selezionare i sottocontenitori da escludere da questa individuazione.  

5. Nella finestra di dialogo Seleziona nuovo contenitore selezionare un contenitore figlio da escludere. Fare clic su **OK** per chiudere la finestra di dialogo Seleziona nuovo contenitore.  

6. Fare clic su **OK** per chiudere la finestra di dialogo Contenitore Active Directory.  

7. Nella finestra Individuazione sistema Active Directory - Proprietà controllare il percorso del contenitore Active Directory in cui ha inizio il rilevamento. La colonna **Ricorsivo** indica **Sì** e anche la nuova colonna **Con esclusioni** indica **Sì**. Fare clic su **OK** per chiudere la finestra Individuazione sistema Active Directory - Proprietà.  



## <a name="specify-the-visibility-of-the-application-catalog-website-link-in-software-center"></a>Specificare la visibilità del collegamento del sito Web del Catalogo applicazioni in Software Center
<!--1358214-->

Ora è possibile controllare se il collegamento **Aprire il sito Web del Catalogo applicazioni** viene visualizzato nel nodo **Stato installazione** di Software Center.  

> [!Note]  
> Il supporto per l'esperienza utente del sito Web Catalogo applicazioni terminerà con il primo aggiornamento rilasciato dopo il 1° giugno 2018. Per altre informazioni, vedere [Funzionalità rimosse e deprecate](../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).  

### <a name="try-it-out"></a>Verifica
 Provare a completare le attività. Inviare quindi [commenti e suggerimenti](#bkmk_feedback).

1. Nella console di Configuration Manager creare un criterio di impostazioni dispositivo client personalizzate nel nodo **Impostazioni client** dell'area di lavoro **Amministrazione**.  

2. Selezionare il gruppo **Software Center**.  

3. Per **Impostazioni del Software Center** fare clic su **Personalizza**.  

4. Abilitare l'opzione **Hide the Application Catalog web site link in Software Center** (Nascondi il collegamento del sito Web del Catalogo applicazioni in Software Center).   

Per altre informazioni sulle impostazioni client, vedere [Configurare le impostazioni client](../clients/deploy/configure-client-settings.md).




## <a name="filter-automatic-deployment-rules-by-software-update-architecture"></a>Filtrare le regole di distribuzione automatica in base all'architettura di aggiornamento software
 <!--1322266-->
Ora è possibile filtrare le regole di distribuzione automatica in modo da escludere architetture come Itanium e ARM64.

### <a name="try-it-out"></a>Verifica
Provare a completare le attività. Inviare quindi [commenti e suggerimenti](#bkmk_feedback).

1. Nella console di Configuration Manager passare all'area di lavoro **Raccolta software**. Espandere **Aggiornamenti software** e selezionare **Regole di distribuzione automatica**. Sulla barra multifunzione selezionare **Crea regola di distribuzione automatica**.  

2. Immettere le impostazioni appropriate per la scheda **Generale** e la scheda **Impostazioni di distribuzione**.  

3. Nella scheda **Aggiornamenti software** selezionare **Architettura**, quindi fare clic su **elementi da trovare** in **Criteri di ricerca**.  

4. Selezionare le architetture da includere nella regola di distribuzione automatica.  

5. Fare clic su **Avanti** e procedere con la creazione della regola di distribuzione automatica.  

> [!IMPORTANT]  
> Tenere presente che esistono applicazioni e componenti a 32 bit (x86) che vengono eseguiti in sistemi a 64 bit (x64). A meno che non si sia certi che x86 non è necessario, abilitare questa funzionalità anche quando si sceglie x64.  

### <a name="known-issues"></a>Problemi noti
Dopo aver aggiunto i criteri relativi all'architettura, nella pagina delle proprietà delle regole di distribuzione automatica viene visualizzato **Titolo** nei criteri di ricerca. La regola di distribuzione automatica funziona comunque come previsto e seleziona gli aggiornamenti software corretti. Attualmente, tuttavia, non è possibile includere entrambi i criteri **Architettura** e **Titolo**. <!--512634,512632-->



## <a name="improvements-to-os-deployment"></a>Miglioramenti della distribuzione del sistema operativo
Sono stati apportati i miglioramenti seguenti alla distribuzione del sistema operativo a seguito dei commenti e suggerimenti di UserVoice.  

- [Maschera i dati sensibili archiviati nelle variabili della sequenza di attività](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15282795-secret-task-sequence-variable-value-exposed): nel passaggio [Imposta variabile della sequenza di attività](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) selezionare la nuova opzione **Non visualizzare questo valore**, ad esempio quando si specifica una password.<!--1358330--> Quando si abilita questa opzione, si applicano i comportamenti seguenti:
  - Il valore della variabile non viene visualizzato in smsts.log.
  - La console di Configuration Manager e il provider SMS gestiscono questo valore come gli altri segreti, ad esempio le password.
  - Il valore non è incluso quando si esporta la sequenza di attività.
  - L'editor della sequenza di attività non legge questo valore quando si modifica il passaggio. Digitare di nuovo l'intero valore per apportare modifiche.

  > [!Important]  
  > Le variabili e i relativi valori vengono salvati con la sequenza di attività in formato XML e offuscati nel database. Quando il client richiede un criterio della sequenza di attività dal punto di gestione, il criterio viene crittografato in transito e durante l'archiviazione sul client. Tuttavia, tutti i valori delle variabili sono in testo normale nell'ambiente della sequenza di attività in memoria in fase di esecuzione nel client. Se la sequenza di attività include un passaggio per l'output del valore della variabile, questo output è in testo normale. Questo comportamento richiede un'azione esplicita da parte dell'amministratore per includere tale passaggio nella sequenza di attività. 


- [Maschera 'nome programma' durante il passaggio 'Esegui riga di comando' di una sequenza di attività](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15282795-secret-task-sequence-variable-value-exposed): per impedire la visualizzazione o la registrazione di dati potenzialmente sensibili, impostare la variabile **OSDDoNotLogCommand** della sequenza di attività su `TRUE`. Questa variabile maschera il nome del programma in smsts.log durante il passaggio [Esegui riga di comando](../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) della sequenza di attività. <!--1358493-->  



## <a name="improvements-to-the-configuration-manager-console"></a>Miglioramenti della console di Configuration Manager
- Le informazioni sull'utente primario sono ora visibili durante la visualizzazione dei membri di una raccolta in **Asset e conformità**, **Raccolte di dispositivi**.<!--510252-->  



## <a name="next-steps"></a>Passaggi successivi
Per informazioni sull'installazione o l'aggiornamento del ramo Technical Preview, vedere [Technical Preview per Configuration Manager](technical-preview.md).    
