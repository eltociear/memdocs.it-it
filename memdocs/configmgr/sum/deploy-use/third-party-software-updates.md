---
title: Abilitare gli aggiornamenti di terze parti
titleSuffix: Configuration Manager
description: Abilitare gli aggiornamenti di terze parti in Configuration Manager
ms.date: 04/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 946b0f74-0794-4e8f-a6af-9737d877179b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f430979a2189494e977c501a36f9f039f860ca7a
ms.sourcegitcommit: 568f8f8c19fafdd0f4352d0682f1ca7a4d665d25
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2020
ms.locfileid: "81771434"
---
# <a name="enable-third-party-updates"></a>Abilitare gli aggiornamenti di terze parti 

*Si applica a: Configuration Manager (Current Branch)*

A partire dalla versione 1806, il nodo **Cataloghi di aggiornamenti software di terze parti** nella console di Configuration Manager consente di sottoscrivere i cataloghi di terze parti, pubblicarne gli aggiornamenti nel punto di aggiornamento software e quindi implementare i cataloghi nei client.  <!--1357605, 1352101, 1358714-->

> [!Note]  
> Configuration Manager non abilita questa funzionalità per impostazione predefinita. Prima di usarlo, abilitare la funzionalità facoltativa **Abilita il supporto per gli aggiornamenti di terze parti sui client**. Per altre informazioni, vedere [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options) (Abilitare le funzioni facoltative dagli aggiornamenti).


## <a name="prerequisites"></a>Prerequisiti 
- Spazio su disco sufficiente nel punto di aggiornamento software principale, cartella WSUSContent, per archiviare il contenuto binario di origine per gli aggiornamenti software di terze parti.
    - La quantità di memoria richiesta varia in base al fornitore, ai tipi di aggiornamenti e agli aggiornamenti specifici pubblicati per la distribuzione.
    - Se è necessario spostare la cartella WSUSContent in un'altra unità con maggiore spazio disponibile, vedere il post di blog [How to change the location where WSUS stores updates locally](https://blogs.technet.microsoft.com/sus/2008/05/19/wsus-how-to-change-the-location-where-wsus-stores-updates-locally/) (Come modificare il percorso in cui WSUS archivia aggiornamenti in locale).
- Il servizio di sincronizzazione degli aggiornamenti software di terze parti richiede l'accesso a Internet.
    - Per l'elenco di cataloghi partner, è necessario l'accesso a download.microsoft.com sulla porta HTTPS 443. 
    -  Accesso a Internet per tutti i cataloghi di terze parti e i file di contenuto degli aggiornamenti. Potrebbero essere necessarie altre porte diverse dalla 443.
    - Gli aggiornamenti di terze parti usano le stesse impostazioni proxy del punto di aggiornamento software.


## <a name="additional-requirements-when-the-sup-is-remote-from-the-top-level-site-server"></a>Requisiti aggiuntivi quando il punto di aggiornamento software è remoto rispetto al server del sito principale 

1. Quando il punto di aggiornamento software è remoto, è necessario abilitarvi SSL. Ciò richiede un certificato di autenticazione server generato da un'autorità di certificazione interna o un provider pubblico.
    - [Configurare SSL in WSUS](/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#25-secure-wsus-with-the-secure-sockets-layer-protocol)
        - Quando si configura SSL in WSUS, tenere presente che alcuni dei servizi Web e delle directory virtuali sono sempre HTTP e non HTTPS. 
        - Configuration Manager scarica il contenuto di terze parti per gli aggiornamenti software dalla directory del contenuto WSUS tramite HTTP.   
    - [Configurare SSL nel punto di aggiornamento software](../get-started/install-a-software-update-point.md#configure-ssl-communications-to-wsus)

2. Quando si imposta la configurazione del certificato di firma WSUS degli aggiornamenti di terze parti su **Configuration Manager gestisce il certificato** nelle proprietà del componente del punto di aggiornamento software, sono necessarie le seguenti configurazioni per consentire la creazione del certificato di firma WSUS autofirmato: 
   - Il Registro di sistema remoto deve essere abilitato nel server del punto di aggiornamento software.
   -  L'**account di connessione al server WSUS** deve avere le autorizzazioni del Registro di sistema per il server del punto di aggiornamento software/WSUS. 


3. Creare la chiave del Registro di sistema seguente nel server del sito di Configuration Manager: 
    - `HKLM\Software\Microsoft\Update Services\Server\Setup`, creare un nuovo valore DWORD denominato **EnableSelfSignedCertificates** con il valore `1`. 

4. Per consentire l'installazione del certificato di firma WSUS autofirmato negli archivi di autori attendibili e radici attendibili sul server del punto di aggiornamento software remoto:
   - L'**account di connessione al server WSUS** deve avere autorizzazioni di amministrazione remota per il server del punto di aggiornamento software.

     Se questo elemento non è possibile, esportare il certificato dall'archivio WSUS del computer locale agli archivi di autori attendibili e radici attendibili. 

> [!NOTE] 
>L'**account di connessione al server WSUS** può essere identificato visualizzando la scheda **Impostazioni proxy e account** nelle proprietà del ruolo del sistema del sito del punto di aggiornamento software. Se non viene specificato un account, viene usato l'account computer del server del sito.

## <a name="enable-third-party-updates-on-the-sup"></a>Abilitare gli aggiornamenti di terze parti nel punto di aggiornamento software
Se si abilita questa opzione, è possibile sottoscrivere i cataloghi di aggiornamenti di terze parti nella console di Configuration Manager. È quindi possibile pubblicare gli aggiornamenti in WSUS e distribuirli nei client. Le operazioni descritte di seguito devono essere eseguite una volta per ogni gerarchia per abilitare e configurare la funzionalità per l'uso. Potrebbe essere necessario eseguire nuovamente i passaggi nel caso in cui si dovesse sostituire il server WSUS principale. 

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**. Espandere **Configurazione del sito** e selezionare il nodo **Siti**.
2. Selezionare il sito al primo livello della gerarchia. Fare clic su **Configura componenti del sito** nella barra multifunzione e selezionare **Punto di aggiornamento software**.
3. Passare alla scheda **Aggiornamenti di terze parti**. Selezionare l'opzione **Abilita gli aggiornamenti software di terze parti**.

    ![Screenshot delle proprietà del punto di aggiornamento software degli aggiornamenti di terze parti](media/third-party-sup-properties.PNG)


## <a name="configure-the-wsus-signing-certificate"></a>Configurare il certificato di firma WSUS
Sarà necessario decidere se gestire automaticamente il certificato di firma WSUS di terze parti con Configuration Manager usando un certificato autofirmato oppure se configurare manualmente il certificato. 

### <a name="automatically-manage-the-wsus-signing-certificate"></a>Gestire automaticamente il certificato di firma WSUS
Se non è necessario usare i certificati PKI, è possibile scegliere di gestire automaticamente i certificati di firma per gli aggiornamenti di terze parti. La gestione dei certificati WSUS viene eseguita durante il ciclo di sincronizzazione e viene registrata in `wsyncmgr.log`. 

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**. Espandere **Configurazione del sito** e selezionare il nodo **Siti**.
2. Selezionare il sito al primo livello della gerarchia. Fare clic su **Configura componenti del sito** nella barra multifunzione e selezionare **Punto di aggiornamento software**.
3. Passare alla scheda **Aggiornamenti di terze parti**. Selezionare l'opzione **Configuration Manager gestisce il certificato**. 
4. Un nuovo certificato di tipo **Firma WSUS di terze parti** viene creato nel nodo **Certificati** in  **Protezione** nell'area di lavoro **Amministrazione**.  

### <a name="manually-manage-the-wsus-signing-certificate"></a>Gestire manualmente il certificato di firma WSUS
Se è necessario configurare manualmente il certificato, ad esempio per usare un certificato PKI, sarà necessario usare [System Center Updates Publisher](../tools/updates-publisher-options.md#update-server) o un altro strumento.  

1. Configurare il certificato di firma usando [System Center Updates Publisher](../tools/updates-publisher-options.md#update-server).
2. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**. Espandere **Configurazione del sito** e selezionare il nodo **Siti**.
3. Selezionare il sito al primo livello della gerarchia. Fare clic su **Configura componenti del sito** nella barra multifunzione e selezionare **Punto di aggiornamento software**.
4. Passare alla scheda **Aggiornamenti di terze parti**. Selezionare l'opzione **Gestisci manualmente il certificato**.


## <a name="enable-third-party-updates-on-the-clients"></a>Abilitare gli aggiornamenti di terze parti nei client
Abilitare gli aggiornamenti di terze parti sui client nelle impostazioni client. L'impostazione configura i criteri dell'agente di Windows Update per [Consenti aggiornamenti firmati da un percorso del servizio di aggiornamento Microsoft nella rete Intranet](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/deploy/4-configure-group-policy-settings-for-automatic-updates#allow-signed-updates-from-an-intranet-microsoft-update-service-location). Questa impostazione client installa anche il certificato di firma WSUS nell'archivio di autori attendibili nel client. La registrazione della gestione del certificato è visibile in `updatesdeployment.log` sui client.  Eseguire questi passaggi per ogni impostazione client personalizzata da usare per gli aggiornamenti di terze parti. Per altre informazioni, vedere l'articolo [Informazioni sulle impostazioni client](../../core/clients/deploy/about-client-settings.md#enable-third-party-software-updates).

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione** e selezionare il nodo **Impostazioni client**.
2. Selezionare un'impostazione client personalizzata esistente o crearne una nuova. 
3. Selezionare la scheda **Aggiornamenti software** a sinistra. Se questa scheda non è presente, verificare che la casella **Aggiornamenti software** sia abilitata.
4. Impostare **Abilita gli aggiornamenti software di terze parti** su **Sì**. 


## <a name="add-a-custom-catalog"></a>Aggiungere un catalogo personalizzato
I *cataloghi partner* sono cataloghi di fornitori di software le cui informazioni sono già registrate con Microsoft. È possibile sottoscrivere i cataloghi partner senza dover specificare informazioni aggiuntive. I cataloghi aggiunti sono chiamati *cataloghi personalizzati*. È possibile aggiungere un catalogo personalizzato da un fornitore di aggiornamenti di terze parti a Configuration Manager. I cataloghi personalizzati devono usare https e gli aggiornamenti devono essere firmati digitalmente. 

1. Passare all'area di lavoro **Software Updates Library** (Raccolta aggiornamenti software), espandere **Aggiornamenti software** e selezionare il nodo **Cataloghi di aggiornamenti software di terze parti**. 
   
     ![Screenshot del nodo degli aggiornamenti di terze parti](media/third-party-updates-node.PNG)
2. Fare clic su **Aggiungi catalogo personalizzato** nella barra multifunzione. 

     ![Aggiungi un catalogo personalizzato per gli aggiornamenti di terze parti](media/third-party-updates-custom-catalog.png)
1. Nella pagina **Generale** specificare gli elementi seguenti: 
    - **URL di download**: un indirizzo HTTPS valido del catalogo personalizzato.
    - **Editore**: nome dell'organizzazione che pubblica il catalogo. 
    - **Nome**: nome del catalogo da visualizzare nella console di Configuration Manager. 
    - **Descrizione**: una descrizione del catalogo. 
    - **URL supporto tecnico** (facoltativo): indirizzo HTTPS valido di un sito Web per ottenere assistenza con il catalogo. 
    - **Contatto supporto tecnico** (facoltativo): informazioni di contatto per ottenere assistenza con il catalogo. 
2. Fare clic su **Avanti** per esaminare il riepilogo del catalogo e continuare per completare gli **Aggiornamenti software guidati di terze parti per i cataloghi personalizzati**.


## <a name="subscribe-to-a-third-party-catalog-and-sync-updates"></a>Sottoscrivere un catalogo di terze parti e sincronizzare gli aggiornamenti
Quando si sottoscrive un catalogo di terze parti nella console di Configuration Manager, i metadati per ogni aggiornamento nel catalogo vengono sincronizzate nei server WSUS per i punti di aggiornamento software. La sincronizzazione dei metadati consente ai client di determinare se uno qualsiasi degli aggiornamenti è applicabile. Seguire questa procedura per ogni catalogo di terze parti per cui si vuole effettuare la sottoscrizione:  

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**. Espandere **Aggiornamenti software** e selezionare il nodo **Cataloghi di aggiornamenti software di terze parti**.  
2. Selezionare il catalogo per cui eseguire la sottoscrizione e fare clic su **Sottoscrivi il catalogo** nella barra multifunzione. 
    ![Aggiungi un catalogo personalizzato per gli aggiornamenti di terze parti](media/third-party-updates-subscribe.png)
3. Rivedere e approvare il certificato del catalogo.  
   > [!NOTE]
   > 
   > Quando si sottoscrive un catalogo di aggiornamenti software di terze parti, il certificato rivisto e approvato nella procedura guidata viene aggiunto al sito. Questo certificato è di tipo **Catalogo di aggiornamenti software di terze parti**. È possibile gestirlo dal nodo **Certificati** in **Protezione** nell'area di lavoro **Amministrazione**.  
4. Completare la procedura guidata. Dopo la sottoscrizione iniziale, in pochi minuti viene avviato il download del catalogo. 
    - Il catalogo viene sincronizzato automaticamente ogni 7 giorni.
    - Fare clic su **Sincronizza ora** nella barra multifunzione per forzare una sincronizzazione.
5. Dopo aver scaricato il catalogo, i metadati del prodotto devono essere sincronizzati dal database WSUS nel database di Configuration Manager. [Avviare manualmente la sincronizzazione degli aggiornamenti software](../get-started/synchronize-software-updates.md#manually-start-software-updates-synchronization) per sincronizzare le informazioni sul prodotto.
6. Dopo la sincronizzazione delle informazioni sul prodotto, [configurare il punto di aggiornamento software per sincronizzare il prodotto desiderato](../get-started/configure-classifications-and-products.md#to-configure-classifications-and-products-to-synchronize) in Configuration Manager.  
7. [Avviare manualmente la sincronizzazione degli aggiornamenti software](../get-started/synchronize-software-updates.md#manually-start-software-updates-synchronization) per sincronizzare gli aggiornamenti del nuovo prodotto in Configuration Manager.  
8. Al termine della sincronizzazione, è possibile visualizzare gli aggiornamenti di terze parti nel nodo **Tutti gli aggiornamenti**. Questi aggiornamenti vengono pubblicati come aggiornamenti **solo metadati** finché non si sceglie di pubblicarli. 
     - L'icona con la freccia blu rappresenta un aggiornamento software solo di metadati. ![Icona per gli aggiornamenti software solo metadati](media/MetadataOnly.png)


## <a name="publish-and-deploy-third-party-software-updates"></a>Pubblicare e distribuire gli aggiornamenti software di terze parti 
Quando gli aggiornamenti di terze parti sono nel nodo **Tutti gli aggiornamenti**, è possibile scegliere gli aggiornamenti da pubblicare per la distribuzione. Quando si pubblica un aggiornamento, i file binari vengono scaricati dal fornitore e inseriti nella directory WSUSContent sul punto di aggiornamento software principale. 

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**. Espandere **Aggiornamenti software** e selezionare il nodo **Tutti gli aggiornamenti software**.
2. Fare clic su **Aggiungi criteri** per filtrare l'elenco degli aggiornamenti. Aggiungere ad esempio **Fornitore** per **HP** per visualizzare tutti gli aggiornamenti di HP.  
3. Selezionare gli aggiornamenti richiesti dall'organizzazione. Fare clic su **Pubblica il contenuto degli aggiornamenti software di terze parti**.
    - Questa azione scarica file binari di aggiornamento del fornitore, quindi li archivia nella cartella WSUSContent nel punto di aggiornamento software principale. 
4. [Avviare manualmente la sincronizzazione degli aggiornamenti software](../get-started/synchronize-software-updates.md#manually-start-software-updates-synchronization) per cambiare lo stato degli aggiornamenti pubblicati da solo metadati ad aggiornamenti distribuibili con contenuto. 
    >[!NOTE]
    >Quando si pubblicano contenuti degli aggiornamenti software di terze parti tutti i certificati usati per firmare i contenuti vengono aggiunti al sito. Questi certificati sono di tipo **Contenuto degli aggiornamenti software di terze parti**. È possibile gestirli dal nodo **Certificati** in **Protezione** nell'area di lavoro **Amministrazione**.  

5. Esaminare lo stato in SMS_ISVUPDATES_SYNCAGENT.log. Il log si trova nel punto di aggiornamento software principale nella cartella dei log di sistema del sito.
6. Distribuire gli aggiornamenti usando il processo [Distribuisci aggiornamenti software](../deploy-use/deploy-software-updates.md). 
7. Nella pagina **Download Locations** (Percorsi download) della **Distribuzione guidata degli aggiornamenti software** selezionare l'opzione predefinita **Scarica aggiornamenti software da Internet**. In questo scenario il contenuto è già pubblicato nel punto di aggiornamento software, che viene usato per scaricare il contenuto per il pacchetto di distribuzione.
8. Per poter visualizzare i risultati di conformità, i client dovranno eseguire un'analisi e valutare gli aggiornamenti.  È possibile attivare manualmente questo ciclo dal pannello di controllo di Configuration Manager in un client eseguendo l'azione **Ciclo di analisi per aggiornamenti software**.


## <a name="improvements-for-third-party-updates-starting-in-1910"></a><a name="bkmk_1910"></a> Miglioramenti per gli aggiornamenti di terze parti a partire da 1910
<!--4469002-->
Sono ora disponibili controlli più granulari sulla sincronizzazione dei cataloghi di aggiornamenti di terze parti. A partire da Configuration Manager versione 1910, è possibile configurare la pianificazione della sincronizzazione per ogni catalogo in modo indipendente. Quando si usano cataloghi che includono aggiornamenti suddivisi per categorie, è possibile configurare la sincronizzazione in modo da includere solo determinate categorie di aggiornamenti per evitare di sincronizzare l'intero catalogo. Con i cataloghi suddivisi per categorie, quando si è certi che si distribuirà una categoria, è possibile configurarla per il download e la pubblicazione automatici in WSUS.

### <a name="set-the-schedule-for-a-catalog-in-a-new-catalog-subscription"></a>Impostare la pianificazione per un catalogo in una nuova sottoscrizione del catalogo

1. Passare all'area di lavoro **Raccolta software**, espandere **Aggiornamenti software** e quindi selezionare il nodo **Cataloghi di aggiornamenti software di terze parti**.
1. Selezionare il catalogo per cui eseguire la sottoscrizione e fare clic su **Sottoscrivi il catalogo** nella barra multifunzione.
1. Scegliere le opzioni disponibili nella pagina **Pianificazione** per eseguire l'override della pianificazione predefinita della sincronizzazione:
   - **Pianificazione semplice**:  scegliere l'intervallo di ore, giorni o mesi.
   - **Pianificazione personalizzata**: impostare una pianificazione complessa.

### <a name="update-the-schedule-per-catalog"></a>Aggiornare la pianificazione per catalogo

1. Passare all'area di lavoro **Raccolta software**, espandere **Aggiornamenti software** e quindi selezionare il nodo **Cataloghi di aggiornamenti software di terze parti**.
1. Fare clic con il pulsante destro del mouse sul catalogo e scegliere **Proprietà**.
1. Scegliere le opzioni nella scheda Pianificazione: 
   - **Pianificazione semplice**:  scegliere l'intervallo di ore, giorni o mesi.
   - **Pianificazione personalizzata**: impostare una pianificazione complessa.

### <a name="new-subscription-to-a-third-party-v3-catalog"></a>Nuova sottoscrizione a un catalogo v3 di terze parti

> [!IMPORTANT]
> Questa opzione è disponibile solo per i cataloghi di aggiornamenti di terze parti v3, che supportano le categorie per gli aggiornamenti. Queste opzioni sono disabilitate per i cataloghi non pubblicati nel nuovo formato v3.


1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**. Espandere **Aggiornamenti software** e selezionare il nodo **Cataloghi di aggiornamenti software di terze parti**.
1. Selezionare il catalogo per cui eseguire la sottoscrizione e fare clic su **Sottoscrivi il catalogo** nella barra multifunzione.
1. Scegliere le opzioni nella pagina **Seleziona categorie**:

   - **Synchronize all update categories** (Sincronizza tutte le categorie di aggiornamento) (impostazione predefinita)
       - Sincronizza tutti gli aggiornamenti nel catalogo di aggiornamenti di terze parti in Configuration Manager.
   -  **Select categories for synchronization** (Seleziona categorie per la sincronizzazione)
       - Scegliere le categorie e le categorie figlio da sincronizzare in Configuration Manager.

      ![Selezionare le categorie di aggiornamenti per la sincronizzazione in Configuration Manager](./media/4469002-select-categories-for-sync.png)
1. Scegliere se si vuole **eseguire un'installazione di appoggio del contenuto degli aggiornamenti** per il catalogo. Quando si esegue un'installazione di appoggio del contenuto, tutti gli aggiornamenti delle categorie selezionate vengono scaricati automaticamente nel punto di aggiornamento software di livello superiore. Non è quindi necessario assicurarsi che siano già stati scaricati prima della distribuzione. È consigliabile eseguire un'installazione di appoggio del contenuto automaticamente solo per gli aggiornamenti di cui è probabile che si eseguirà la distribuzione, per evitare un uso eccessivo della larghezza di banda e delle risorse di archiviazione.

   - **Do not stage content, synchronize for scanning only (recommended)** (Non eseguire un'installazione di appoggio, sincronizza solo per l'analisi (scelta consigliata))
     - Non scaricare alcun contenuto degli aggiornamenti per il catalogo di terze parti
   - **Stage the content for selected categories automatically** (Esegui installazione di appoggio automaticamente per le categorie selezionate)
     - Scegliere le categorie di aggiornamenti per le quali scaricare il contenuto automaticamente.
     - Il contenuto degli aggiornamenti delle categorie selezionate verrà scaricato nella directory del contenuto WSUS del punto di aggiornamento software di livello superiore.
      ![Selezionare le categorie di aggiornamenti per l'installazione di appoggio del contenuto](./media/4469002-stage-content.png)
1. Impostare la **pianificazione** per la sincronizzazione del catalogo, quindi completare la procedura guidata.

 

### <a name="edit-an-existing-subscription"></a>Modificare una sottoscrizione esistente

> [!IMPORTANT]
> Questa opzione è disponibile solo per i cataloghi di aggiornamenti di terze parti v3, che supportano le categorie per gli aggiornamenti. Queste opzioni sono disabilitate per i cataloghi non pubblicati nel nuovo formato v3.

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**. Espandere **Aggiornamenti software** e selezionare il nodo **Cataloghi di aggiornamenti software di terze parti**.
1. Fare clic con il pulsante destro del mouse sul catalogo e scegliere **Proprietà**.
1. Scegliere le opzioni nella scheda **Seleziona categorie**.
   - **Synchronize all update categories** (Sincronizza tutte le categorie di aggiornamento) (impostazione predefinita)
       - Sincronizza tutti gli aggiornamenti nel catalogo di aggiornamenti di terze parti in Configuration Manager.
   -  **Select categories for synchronization** (Seleziona categorie per la sincronizzazione)
       - Scegliere le categorie e le categorie figlio da sincronizzare in Configuration Manager.
1. Scegliere le opzioni per la scheda **Stage update content** (Esegui installazione di appoggio per il contenuto degli aggiornamenti).
   - **Do not stage content, synchronize for scanning only (recommended)** (Non eseguire un'installazione di appoggio, sincronizza solo per l'analisi (scelta consigliata))
     - Non scaricare alcun contenuto degli aggiornamenti per il catalogo di terze parti
   - **Stage the content for selected categories automatically** (Esegui installazione di appoggio automaticamente per le categorie selezionate)
     - Scegliere le categorie di aggiornamenti per le quali scaricare il contenuto automaticamente.
     - Il contenuto degli aggiornamenti delle categorie selezionate verrà scaricato nella directory del contenuto WSUS del punto di aggiornamento software di livello superiore. 

## <a name="monitoring-progress-of-third-party-software-updates"></a>Monitoraggio dello stato degli aggiornamenti software di terze parti 

La sincronizzazione degli aggiornamenti software di terze parti viene gestita dal componente SMS_ISVUPDATES_SYNCAGENT nel punto di aggiornamento software principale. È possibile visualizzare i messaggi di stato da questo componente o vedere lo stato più in dettaglio in SMS_ISVUPDATES_SYNCAGENT.log. Questo log si trova nel punto di aggiornamento software principale nella cartella dei log di sistema del sito. Per impostazione predefinita, questo percorso è C:\Programmi\Microsoft Configuration Manager\Logs. Per altre informazioni sul monitoraggio della gestione generale degli aggiornamenti software, vedere [Monitorare gli aggiornamenti software](../deploy-use/monitor-software-updates.md) 

## <a name="known-issues"></a>Problemi noti

- Il computer in cui è in esecuzione la console viene usato per scaricare gli aggiornamenti da WSUS e aggiungerli al pacchetto di aggiornamenti. Il certificato di firma WSUS deve essere considerato attendibile nel computer console. In caso contrario, potrebbero verificarsi problemi con il controllo della firma durante il download degli aggiornamenti di terze parti. 
- Il servizio di sincronizzazione degli aggiornamenti software di terze parti non è in grado di pubblicare contenuto negli aggiornamenti di soli metadati aggiunti a WSUS usando un'altra applicazione o un altro strumento o script, ad esempio SCUP. L'azione **Pubblica il contenuto degli aggiornamenti software di terze parti** avrà esito negativo per questi aggiornamenti. Se è necessario distribuire aggiornamenti di terze parti che questa funzionalità non supporta ancora, usare per intero il processo esistente per distribuire tali aggiornamenti.  
-  Configuration Manager include una nuova versione per il formato di file CAB di catalogo. La nuova versione include i certificati per i file binari del fornitore. Questi certificati vengono aggiunti al nodo **Certificati** sotto **Sicurezza** nell'area di lavoro **Amministrazione** dopo aver approvato e considerato attendibile il catalogo.  
     - È comunque possibile usare la versione del file CAB del catalogo precedente, purché l'URL di download sia https e gli aggiornamenti siano firmati. Il contenuto non verrà pubblicato perché i certificati per i file binari non sono nel file CAB e sono già approvati. Per risolvere il problema, trovare il certificato nel nodo **Certificati**, sbloccarlo e quindi pubblicare di nuovo l'aggiornamento. Se si devono pubblicare più aggiornamenti firmati con certificati diversi, sarà necessario sbloccare ogni certificato usato.
     - Per altre informazioni, vedere i messaggi di stato 11523 e 11524 nella tabella dei messaggi di stato seguente.
-  Quando il servizio di sincronizzazione degli aggiornamenti software di terze parti nel punto di aggiornamento software di livello superiore richiede un server proxy per l'accesso a Internet, i controlli della firma digitale potrebbero non riuscire. Per risolvere questo problema, configurare le impostazioni proxy WinHTTP nel sistema del sito. Per altre informazioni, vedere [Netsh commands for WinHTTP](https://go.microsoft.com/fwlink/p/?linkid=199086) (Comandi Netsh per WinHTTP).
- Quando si usa Cloud Management Gateway per l'archiviazione del contenuto, il contenuto per gli aggiornamenti di terze parti non viene scaricato nei client se è abilitata l'[impostazione client](../../core/clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available) **Consenti ai client di scaricare contenuto differenziale quando disponibile**. <!--6598587-->

## <a name="status-messages"></a>Messaggi di stato

| MessageID       | Gravità           | Descrizione | Possibile causa| Possibile soluzione
| ------------- |-------------| -----|----|----|
| 11516     | Errore |Non è stato possibile pubblicare contenuti per l'aggiornamento "ID aggiornamento" perché i contenuti non sono firmati.  È possibile pubblicare solo contenuti con firme valide.  |Configuration Manager non consente di pubblicare aggiornamenti senza firma.| Pubblicare l'aggiornamento in un altro modo. </br></br>Verificare se è disponibile un aggiornamento firmato dal fornitore.|
| 11523  | Avviso |  Il catalogo "X" non include certificati di firma del contenuto. È possibile che i tentativi di pubblicazione di contenuti di aggiornamento per gli aggiornamenti da questo catalogo abbiano esito negativo fino all'aggiunta e all'approvazione dei certificati di firma del contenuto. | Questo messaggio può essere visualizzato quando si importa un catalogo che usa una versione precedente del formato di file CAB.|Contattare il provider del catalogo per ottenere un catalogo aggiornato che includa certificati di firma del contenuto. </br> </br> I certificati per i file binari non sono inclusi nel file CAB, quindi il contenuto non verrà pubblicato. Per risolvere il problema, trovare il certificato nel nodo **Certificati**, sbloccarlo e quindi pubblicare di nuovo l'aggiornamento. Se si devono pubblicare più aggiornamenti firmati con certificati diversi, sarà necessario sbloccare ogni certificato usato.|
| 11524| Errore  | Non è stato possibile pubblicare l'aggiornamento "ID" a causa di metadati mancanti per l'aggiornamento. | L'aggiornamento potrebbe essere stato sincronizzato con WSUS al di fuori di Configuration Manager.| Sincronizzare l'aggiornamento con Configuration Manager prima di provare a pubblicare contenuti.  </br> </br>Se è stato usato uno strumento esterno per pubblicare l'aggiornamento come **Solo metadati**, usare lo stesso strumento per pubblicare i contenuti dell'aggiornamento.|



## <a name="working-with-third-party-updates-video"></a>Video Working with third-party updates (Uso di aggiornamenti di terze parti)
<iframe width="560" height="315" src="https://www.youtube.com/embed/ai8rLCLtuTI?rel=0" frameborder="0" allowfullscreen></iframe>



## <a name="next-step"></a>Passaggio successivo
> [!div class="nextstepaction"]
> [Distribuire gli aggiornamenti software](./deploy-software-updates.md)
