---
title: Usare Asset Intelligence
titleSuffix: Configuration Manager
description: Eseguire attività comuni con Asset Intelligence in Configuration Manager.
ms.date: 08/30/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e8159bd9-5c2b-4d25-82f9-78fcfd732ba9
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1e272e8e71ceaa15c712cb3a53d9db835747d327
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695069"
---
# <a name="how-to-use-asset-intelligence-in-configuration-manager"></a>Come usare Asset Intelligence in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Questo argomento contiene informazioni che consentono di gestire le attività tipiche di Asset Intelligence nella gerarchia di Configuration Manager:  

##  <a name="view-asset-intelligence-information"></a><a name="BKMK_ViewInformation"></a> Visualizzare le informazioni di Asset Intelligence  
 È possibile visualizzare le informazioni di Asset Intelligence nella home page e nei report di **Asset Intelligence** .  

###  <a name="asset-intelligence-home-page"></a><a name="BKMK_AssetIntelligenceHomePage"></a> Home page di Asset Intelligence  
 La home page di **Asset Intelligence** visualizza un dashboard di riepilogo delle informazioni del catalogo di Asset Intelligence. Nella home page è possibile visualizzare informazioni sulla sincronizzazione del catalogo e sullo stato del software di inventario. La home page di **Asset Intelligence** è divisa nelle sezioni seguenti:  

- **Sincronizzazione catalogo**: presenta informazioni sullo stato di abilitazione di Asset Intelligence, sullo stato corrente del punto di sincronizzazione di Asset Intelligence, sulla pianificazione della sincronizzazione, sul fatto che il resoconto delle licenze cliente sia stato o meno importato, sulla data dell'ultimo aggiornamento dello stato e sull'ora per il successivo aggiornamento pianificato, nonché sul numero di modifiche apportate dopo l'installazione del sistema del sito del punto di sincronizzazione di Asset Intelligence.  

  > [!NOTE]  
  >  La sezione relativa alla sincronizzazione del catalogo di Asset Intelligence nella home page di **Asset Intelligence** viene visualizzata solo se è stato installato un ruolo del sistema del sito del punto di sincronizzazione di Asset Intelligence.  

- **Stato software di inventario**: indica il conteggio e la percentuale dei programmi software, delle categorie software e delle famiglie software di inventario identificati da Microsoft, identificati da un utente amministratore, con identificazione online in sospeso o non identificati e non in sospeso. Le informazioni visualizzate in formato di tabella mostrano i conteggi, mentre le informazioni visualizzate nel grafico mostrano le percentuali.  

  Attenersi alla procedura seguente per visualizzare le informazioni di Asset Intelligence nella home page di **Asset Intelligence** .  

##### <a name="to-view-asset-intelligence-information-on-the-asset-intelligence-home-page"></a>Per visualizzare le informazioni di Asset Intelligence nella home page di Asset Intelligence  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità**.  

2.  Nell'area di lavoro **Asset e conformità** fare clic su **Asset Intelligence**. Verranno visualizzati i report di Asset Intelligence.  

###  <a name="asset-intelligence-reports"></a><a name="BKMK_AssetIntelligenceReports"></a> Report di Asset Intelligence  
 Sono disponibili oltre 60 report di Asset Intelligence che mostrano le informazioni raccolte da Asset Intelligence. Molti di questi report sono collegati a report più specifici in cui è possibile eseguire una query per informazioni generali e il drill-down per informazioni più dettagliate. I report di Asset Intelligence si trovano nella console di Configuration Manager, nell'area di lavoro **Monitoraggio** del nodo **Report**. I report forniscono informazioni su hardware, gestione delle licenze e software. Per altre informazioni sui report in Configuration Manager, vedere [Introduzione ai report](../../../servers/manage/introduction-to-reporting.md).  

> [!NOTE]  
>  La precisione delle informazioni su licenze e quantità dei titoli software installati visualizzate nei report di Asset Intelligence può variare rispetto al numero effettivo di titoli software installati o licenze in uso nell'ambiente a causa delle complesse dipendenze e limitazioni associate all'esecuzione dell'inventario delle informazioni sulle licenze per i titoli software installati in ambienti aziendali. I report di Asset Intelligence non devono essere usati come unica fonte per determinare la conformità delle licenze software acquistate.  

 Attenersi alla procedura seguente per visualizzare le informazioni di Asset Intelligence usando i report di Asset Intelligence.  

##### <a name="to-view-collected-asset-intelligence-information-by-using-asset-intelligence-reports"></a>Per visualizzare le informazioni di Asset Intelligence raccolte usando i report di Asset Intelligence  

1.  Nella console di Configuration Manager fare clic su **Monitoraggio**.  

2.  Nell'area di lavoro **Monitoraggio** espandere **Report**, espandere **Report**e fare clic su **Asset Intelligence**. Verranno visualizzati i report di Asset Intelligence.  

    > [!WARNING]  
    >  Se nel nodo **Report** non c'è alcuna cartella di report, verificare di aver configurato la creazione di report. Per altre informazioni, vedere [Configurazione della creazione di report](../../../../core/servers/manage/configuring-reporting.md).  

3.  Selezionare il report di Asset Intelligence che si vuole eseguire e quindi nel gruppo **Gruppo Report** della scheda **Home** fare clic su **Esegui**.  

##  <a name="synchronize-the-asset-intelligence-catalog"></a><a name="BKMK_SynchronizeTheCatalog"></a> Sincronizzare il catalogo di Asset Intelligence  
 È possibile sincronizzare il catalogo di Asset Intelligence locale con System Center Online per recuperare la categorizzazione più recente dei titoli software. Quando si richiede manualmente la sincronizzazione del catalogo con System Center Online, potrebbero essere necessari 15 minuti o più per completare il processo di sincronizzazione con System Center Online. Configuration Manager aggiorna l'impostazione **Ultimo aggiornamento** nella home page di **Asset Intelligence** con l'ora attuale in cui la sincronizzazione è stata completata correttamente.  

> [!NOTE]  
>  È prima necessario installare un ruolo del sistema del sito del punto di sincronizzazione di Asset Intelligence usando le procedure. Per informazioni sull'installazione di un punto di sincronizzazione di Asset Intelligence, vedere [Configurazione di Asset Intelligence](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

 Attenersi alla procedura seguente per creare una pianificazione della sincronizzazione per il catalogo di Asset Intelligence.  

#### <a name="to-create-a-synchronization-schedule-for-the-asset-intelligence-catalog"></a>Per creare una pianificazione della sincronizzazione per il catalogo di Asset Intelligence  

1. Nella console di Configuration Manager fare clic su **Asset e conformità**.  

2. Nell'area di lavoro **Asset e conformità** fare clic su **Asset Intelligence**.  

3. Nel gruppo **Crea** della scheda **Home** fare clic su **Sincronizza**e quindi su **Pianifica sincronizzazione**.  

4. Nella finestra di dialogo **Pianificazione punto di sincronizzazione di Asset Intelligence** selezionare **Abilita sincronizzazione su una pianificazione**e quindi configurare una pianificazione semplice o personalizzata.  

5. Fare clic su **OK** per salvare le modifiche.  

   > [!NOTE]  
   >  Per informazioni sulla pianificazione della sincronizzazione, inclusa la sincronizzazione pianificata successiva, vedere il nodo **Asset Intelligence** nell'area di lavoro **Asset e conformità** nel sito principale della gerarchia.  

   Attenersi alla procedura seguente per sincronizzare manualmente il catalogo di Asset Intelligence.  

> [!WARNING]  
>  System Center Online accetta solo una richiesta di sincronizzazione manuale in un periodo di 12 ore.  

###  <a name="to-manually-synchronize-the-asset-intelligence-catalog"></a><a name="BKMK_ManuallySynchronizeCatalog"></a> Per sincronizzare manualmente il catalogo di Asset Intelligence  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità**.  

2.  Nell'area di lavoro **Asset e conformità** fare clic su **Asset Intelligence**.  

3.  Nel gruppo **Crea** della scheda **Home** fare clic su **Sincronizza**, quindi su **Sincronizza catalogo di Asset Intelligence**e infine su **OK**.  

##  <a name="customize-the-asset-intelligence-catalog"></a><a name="BKMK_CustomizeCatalog"></a> Personalizzare il catalogo di Asset Intelligence  
 Le informazioni di categorizzazione del catalogo di Asset Intelligence ricevute da System Center Online vengono archiviate nel database del sito con autorizzazioni di sola lettura e non possono essere modificate o eliminate. Tuttavia, è possibile creare, modificare ed eliminare categorie software, famiglie software, etichette software e informazioni del catalogo sui requisiti hardware personalizzate. È quindi possibile usare dati di categorizzazione personalizzati invece delle informazioni fornite da System Center Online per le informazioni sui titoli software esistenti o definite dall'utente. Quando si modificano o si aggiungono informazioni di categorizzazione, le informazioni del catalogo vengono considerate definite dall'utente. Le informazioni di categorizzazione definite dall'utente vengono archiviate in tabelle di database diverse rispetto alle informazioni del catalogo convalidate.  

###  <a name="software-categories"></a><a name="BKMK_SoftwareCategories"></a> Categorie software  
 Le categorie software di Asset Intelligence vengono usate per categorizzare in modo generale i titoli software di inventario e anche come raggruppamenti generali di famiglie software più specifiche. Un esempio di categoria software potrebbe essere "aziende del settore energetico" e una famiglia software all'interno di tale categoria software potrebbe essere "petrolio e gas" o "energia idroelettrica". Molte categorie software sono predefinite nel catalogo di Asset Intelligence ed è possibile creare altre categorie definite dall'utente per definire ulteriormente il software di inventario. Lo stato di convalida di tutte le categorie software predefinite è sempre **Convalidato**, mentre per le informazioni sulle categorie software personalizzate aggiunte al catalogo di Asset Intelligence lo stato è **Definito da utente**.  

 Attenersi alla procedura seguente per creare una categoria software definita dall'utente.  

##### <a name="to-create-a-user-defined-software-category"></a>Per creare una categoria software definita dall'utente  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità**.  

2.  Nell'area di lavoro **Asset e conformità** fare clic su **Asset Intelligence**e quindi su **Catalogo**.  

3.  Nel gruppo **Crea** della scheda **Home** fare clic su **Crea categoria software**.  

4.  Nella pagina **Generale** immettere un nome e una descrizione facoltativa per la nuova categoria software.  

    > [!NOTE]  
    >  Lo stato di convalida di tutte le nuove categorie software personalizzate è sempre impostato su **Definito da utente**.  

     Fare clic su **Avanti**.  

5.  Nella pagina **Riepilogo** verificare le impostazioni e quindi fare clic su **Avanti**.  

6.  Nella pagina **Completamento** fare clic su **Chiudi** per uscire dalla procedura guidata.  

###  <a name="software-families"></a><a name="BKMK_SoftwareFamilies"></a> Famiglie software  
 Le famiglie software di Asset Intelligence vengono usate per definire ulteriormente i titoli software di inventario all'interno delle categorie software. Un esempio di categoria software potrebbe essere "aziende del settore energetico" e una famiglia software all'interno di tale categoria software potrebbe essere "petrolio e gas" o "energia idroelettrica". Molte famiglie software sono predefinite nel catalogo di Asset Intelligence ed è possibile creare altre famiglie definite dall'utente per definire il software di inventario. Lo stato di convalida di tutte le famiglie software predefinite è sempre **Convalidato**, mentre per le informazioni sulle famiglie software personalizzate aggiunte al catalogo di Asset Intelligence lo stato è **Definito da utente**.  

 Attenersi alla procedura seguente per creare una famiglia software definita dall'utente.  

##### <a name="to-create-a-user-defined-software-family"></a>Per creare una famiglia software definita dall'utente  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità**.  

2.  Nell'area di lavoro **Asset e conformità** fare clic su **Asset Intelligence**e quindi su **Catalogo**.  

3.  Nel gruppo **Crea** della scheda **Home** fare clic su **Crea famiglia software**.  

4.  Nella pagina **Generale** immettere un nome e una descrizione facoltativa per la nuova famiglia software.  

    > [!NOTE]  
    >  Lo stato di convalida di tutte le nuove famiglie software personalizzate è sempre impostato su **Definito da utente**.  

5.  Nella pagina **Riepilogo** verificare le impostazioni e quindi fare clic su **Avanti**.  

6.  Nella pagina **Completamento** fare clic su **Chiudi** per uscire dalla procedura guidata.  

###  <a name="software-labels"></a><a name="BKMK_SoftwareLabels"></a> Etichette software  
 Le etichette di Asset Intelligence software personalizzati consentono di creare filtri che è possibile utilizzare per raggruppare i titoli di software e visualizzarli utilizzando i report di Asset Intelligence. Ad esempio, è possibile creare un'etichetta software denominata shareware, associarla a diverse applicazioni e quindi eseguire un report che mostra tutti i titoli con l'etichetta software shareware. Lo stato di convalida è **Definito da utente** per tutte le etichette software personalizzate aggiunte al catalogo di Asset Intelligence.  

 Attenersi alla procedura seguente per creare un'etichetta personalizzata definita dall'utente.  

##### <a name="to-create-a-user-defined-software-label"></a>Per creare un'etichetta software definita dall'utente  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità**.  

2.  Nell'area di lavoro **Asset e conformità** fare clic su **Asset Intelligence**e quindi su **Catalogo**.  

3.  Nel gruppo **Crea** della scheda **Home** fare clic su **Crea etichetta software**.  

4.  Nella pagina **Generale** immettere un nome e una descrizione facoltativa per la nuova famiglia software.  

    > [!NOTE]  
    >  Lo stato di convalida di tutte le nuove etichette software personalizzate è sempre impostato su **Definito da utente**.  

5.  Nella pagina **Riepilogo** verificare le impostazioni e quindi fare clic su **Avanti**.  

6.  Nella pagina **Completamento** fare clic su **Chiudi** per uscire dalla procedura guidata.  

###  <a name="hardware-requirements"></a><a name="BKMK_HardwareRequirements"></a> Requisiti hardware  
 Le informazioni sui requisiti hardware consentono di verificare che i computer soddisfino i requisiti hardware per i titoli software prima di sceglierli come destinazione per le distribuzioni di software. Molti requisiti hardware sono predefiniti nel catalogo di Asset Intelligence ed è possibile creare nuove informazioni per requisiti hardware definiti dall'utente per soddisfare requisiti personalizzati. Lo stato di convalida di tutti i requisiti hardware predefiniti è sempre **Convalidato**, mentre per le informazioni sui requisiti hardware definiti dall'utente aggiunti al catalogo di Asset Intelligence lo stato è **Definito da utente**.  

> [!IMPORTANT]  
>  I requisiti hardware visualizzati nella console di Configuration Manager vengono recuperati dal catalogo di Asset Intelligence nel computer locale e non sono basati sulle informazioni dei titoli software di inventario dei client di System Center 2012 Configuration Manager. Le informazioni sui requisiti hardware non vengono aggiornate nell'ambito del processo di sincronizzazione con System Center Online. È possibile creare requisiti hardware definiti dall'utente per software di inventario senza requisiti hardware associati.  

 Attenersi alla procedura seguente per creare un requisito hardware definito dall'utente.  

##### <a name="to-create-a-user-defined-hardware-requirements"></a>Per creare un requisito hardware definito dall'utente  

1. Nella console di Configuration Manager fare clic su **Asset e conformità**.  

2. Nell'area di lavoro **Asset e conformità** fare clic su **Asset Intelligence**e quindi su **Requisiti hardware**.  

3. Nel gruppo **Crea** della scheda **Home** fare clic su **Crea requisiti hardware**.  

4. Nella pagina **Generale** immettere le informazioni seguenti:  

   1. **Titolo software**: specifica il titolo software a cui sono associati i requisiti hardware. Il titolo software non può essere già presente nel catalogo di Asset Intelligence.  

   2. **Stato convalida**: elenca lo stato di convalida come **Definito dall'utente** per i requisiti hardware. È impossibile modificare questa impostazione.  

   3. **CPU minima (MHz)** : specifica la velocità minima del processore, in megahertz (MHz), richiesta dal titolo software.  

   4. **RAM minima (KB)** : specifica la quantità di RAM minima, in kilobyte (KB), richiesta dal titolo software.  

   5. **Dimensioni minime spazio su disco (KB):** : specifica la quantità minima di spazio disponibile sul disco, in KB, richiesta dal titolo software.  

   6. **Dimensioni disco minime (KB):** : specifica la dimensione minima del disco rigido, in KB, richiesta dal titolo software.  

      Fare clic su **Avanti**.  

5. Nella pagina **Riepilogo** verificare le impostazioni e quindi fare clic su **Avanti**.  

6. Nella pagina **Completamento** fare clic su **Chiudi** per uscire dalla procedura guidata.  

###  <a name="modify-categorization-information-for-inventoried-software"></a><a name="BKMK_ModifyCategorization"></a> Modificare le informazioni di categorizzazione per il software di inventario  
 Il software predefinito nel catalogo di Asset Intelligence è configurato con informazioni di categorizzazione specifiche, ad esempio nome del prodotto, fornitore, categoria software e famiglia software. Quando le informazioni di categorizzazione predefinite non soddisfano i requisiti, è possibile modificarle nelle proprietà del titolo software. Quando si modificano le informazioni di categorizzazione per software predefiniti, lo stato di convalida per le modifiche software cambia da **Convalidato** a **Definito da utente**.  

> [!IMPORTANT]  
>  Le informazioni di categorizzazione possono essere modificate solo nel sito principale.  

 Attenersi alla procedura seguente per modificare le informazioni di categorizzazione per il software di inventario.  

##### <a name="to-modify-the-categorizations-for-software-titles"></a>Per modificare le categorizzazioni per i titoli software  

1. Nella console di Configuration Manager fare clic su **Asset e conformità**.  

2. Nell'area di lavoro **Asset e conformità** fare clic su **Asset Intelligence**e quindi su **Software di inventario**.  

3. Selezionare uno o più titoli software di cui si vogliono modificare le categorizzazioni.  

4. Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

5. Nella scheda **Generale** è possibile modificare le informazioni di categorizzazione seguenti:  

   -   **Nome prodotto**: specifica il nome del titolo software di inventario.  

   -   **Fornitore**: specifica il nome del fornitore che ha sviluppato il titolo software di inventario.  

   -   **Categoria**: specifica la categoria software attualmente assegnata al titolo software di inventario.  

   -   **Famiglia**: specifica la famiglia software attualmente assegnata al titolo software di inventario.  

6. Fare clic su **OK** per salvare le modifiche.  

   Attenersi alla procedura seguente per ripristinare le informazioni di categorizzazione originali del software.  

### <a name="revert-categorization-information-to-original-settings-for-software"></a>Ripristinare le impostazioni originali delle informazioni di categorizzazione per il software  
 Configuration Manager archivia le informazioni di categorizzazione ottenute da System Center Online nel database. Le informazioni non possono essere eliminate. Dopo che le informazioni sono state modificate, è possibile ripristinare le informazioni di categorizzazione di System Center Online. È anche possibile ripristinare le impostazioni originali del software di inventario non incluso nel catalogo di Asset Intelligence.  

 Attenersi alla procedura seguente per ripristinare le impostazioni originali delle informazioni di categorizzazione.  

##### <a name="to-revert-categorization-information-to-original-settings"></a>Per ripristinare le impostazioni originali delle informazioni di categorizzazione  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità**.  

2.  Nell'area di lavoro **Asset e conformità** fare clic su **Asset Intelligence**e quindi su **Software di inventario**.  

3.  Selezionare uno o più titoli software di cui si vogliono ripristinare le impostazioni originali. È possibile ripristinare solo il software con stato **Definito da utente** .  

    > [!TIP]  
    >  Fare clic sulla colonna **Stato** per ordinare le informazioni in base allo stato di convalida. L'ordinamento consente di visualizzare tutto il software in base allo stato di convalida e selezionare rapidamente più elementi per ripristinare le impostazioni originali.  

4.  Nel gruppo **Prodotto** della scheda **Home** fare clic su **Ripristina**.  

5.  Fare clic su **Sì** per ripristinare le informazioni di categorizzazione originali del software.  

6.  Quando si ripristinano le informazioni di categorizzazione per software incluso nel catalogo di Asset Intelligence, lo stato di convalida cambia da **Definito da utente** a **Convalidato**. Quando si ripristina software non incluso nel catalogo, lo stato di convalida cambia da **Definito da utente** a **Senza categoria**.  

##  <a name="request-a-catalog-update-for-uncategorized-software-titles"></a><a name="BKMK_RequestCatalogUpdate"></a> Richiedere un aggiornamento del catalogo per i titoli software senza categoria  
 Per la ricerca e la categorizzazione, è possibile inviare informazioni di titolo di software senza categoria per System Center Online. Dopo l'invio di un titolo software senza categoria, quando ci sono almeno 4 richieste di categorizzazione dei clienti per lo stesso titolo software, i ricercatori identificano, categorizzano e quindi rendono disponibili le informazioni di categorizzazione del titolo software per tutti i clienti che usano il servizio System Center Online. Microsoft assegna la massima priorità ai titoli di software con il maggior numero di richieste di categorizzazione. È improbabile che al software personalizzato e alle applicazioni line-of-business venga assegnata una categoria e la procedura consigliata prevede di non inviare questi titoli software a Microsoft per la categorizzazione.  

 Quando le informazioni sui titoli software vengono inviate a System Center Online per la categorizzazione, si applicano le condizioni seguenti:  

-   Solo le informazioni sui titoli software di base vengono trasmesse a System Center Online e le informazioni sui titoli software da categorizzare possono essere esaminate prima dell'invio.  

-   Le informazioni sulle licenze software non vengono mai trasmesse.  

-   Tutti i titoli software caricati diventano disponibili pubblicamente come parte del catalogo di System Center Online e possono essere scaricati da altri clienti.  

-   L'origine del titolo software non viene archiviata nel catalogo di System Center Online. Tuttavia, i titoli di applicazioni che contengono informazioni riservate o proprietarie non devono essere inviati per la categorizzazione in System Center Online.  

> [!NOTE]  
>  Per altre informazioni sulla privacy di Asset Intelligence, vedere [Sicurezza e privacy per Asset Intelligence](../../../../core/clients/manage/asset-intelligence/security-and-privacy-for-asset-intelligence.md).  

 Attenersi alla procedura seguente per richiedere la categorizzazione di titoli software del catalogo di Asset Intelligence in System Center Online.  

#### <a name="to-request-a-catalog-update-for-uncategorized-software-titles"></a>Per richiedere un aggiornamento del catalogo per i titoli software senza categoria  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità**.  

2.  Nell'area di lavoro **Asset e conformità** fare clic su **Asset Intelligence**e quindi su **Software di inventario**.  

3.  Selezionare uno o più nomi di prodotto da inviare a System Center Online per la categorizzazione. Solo i titoli software di inventario senza categoria possono essere inviati a System Center Online per la categorizzazione. Se il titolo software di inventario è stato categorizzato da un amministratore con la conseguente impostazione di uno stato definito dall'utente, è necessario fare clic con il pulsante destro del mouse sul titolo software di inventario e quindi scegliere **Ripristina** per ripristinare lo stato **Senza categoria** del titolo software e poterlo quindi inviare a System Center Online per la categorizzazione.  

    > [!NOTE]  
    >  Configuration Manager può elaborare allo stesso tempo fino a 2000 titoli software per categorizzazione. Se si selezionano più di 2000 titoli software, verranno elaborati solo i primi 2000 titoli. È necessario selezionare i rimanenti titoli software per la categorizzazione in batch minori di 2000.  

    > [!TIP]  
    >  Fare clic sulla colonna **Stato** per ordinare le informazioni in base allo stato di convalida. In questo modo, è possibile visualizzare tutti i nomi di prodotto senza categoria e selezionare rapidamente più elementi da inviare per la categorizzazione.  

4.  Nel gruppo **Prodotto** della scheda **Home** fare clic su **Aggiornamento catalogo richieste**.  

5.  Esaminare il messaggio sulla privacy per l'invio per la categorizzazione a System Center Online. Fare clic su **Dettagli** per visualizzare le informazioni che verranno inviate a System Center Online.  

6.  Selezionare **Dichiaro di avere letto e compreso questo messaggio**, quindi fare clic su **OK** per consentire l'invio dei titoli software selezionati per la categorizzazione.  

7.  Verificare che lo stato dei nomi dei prodotti software di inventario inviati a System Center Online per la categorizzazione venga modificato da **Senza categoria** a **In attesa**.  

    > [!NOTE]  
    >  Il software che viene inviato a System Center Online per la categorizzazione ha uno stato di convalida **In attesa** in un sito di amministrazione centrale, ma viene ancora visualizzato con uno stato di convalida **Senza categoria** nei siti primari figlio.  

##  <a name="resolve-software-details-conflicts"></a><a name="BKMK_ResolveSoftwareDetails"></a> Risolvere i conflitti dei dettagli software  
 Dopo la categorizzazione software appena aggiornato dettagli sono stati ricevuti da System Center Online che creano conflitti con informazioni software esistente, è possibile scegliere come risolvere il conflitto. Il software che presenta un conflitto corrente ha uno stato di convalida **Aggiornabile**. Dopo la risoluzione dei conflitti dei dettagli software, le informazioni di categorizzazione software vengono conservate nel catalogo di Asset Intelligence in base all'impostazione specificata. Un conflitto dei dettagli software non si verifica di nuovo per lo stesso valore di categorizzazione software a meno che il valore di System Center Online non cambi dopo la risoluzione del conflitto.  

 Attenersi alla procedura seguente per risolvere un conflitto dei dettagli software.  

#### <a name="to-resolve-a-software-details-conflict"></a>Per risolvere un conflitto dei dettagli software  

1. Nella console di Configuration Manager fare clic su **Asset e conformità**.  

2. Nell'area di lavoro **Asset e conformità** fare clic su **Asset Intelligence**e quindi su **Software di inventario**.  

3. Esaminare la colonna **Stato** per individuare i titoli software con stato **Aggiornabile** .  

4. Selezionare il titolo software per cui è necessario risolvere un conflitto e quindi nel gruppo **Prodotto** della scheda **Home** fare clic su **Risolvi conflitto**.  

5. Esaminare le informazioni seguenti:  

   -   **Valore locale**: specifica le informazioni di categorizzazione software esistenti nel catalogo di Asset Intelligence che sono in conflitto con i dettagli di categorizzazione software più recenti di System Center Online.  

   -   **Valore scaricato**: specifica le nuove informazioni di categorizzazione software di System Center Online per le informazioni di categorizzazione software del catalogo di Asset Intelligence in conflitto.  

6. Selezionare una delle impostazioni seguenti per risolvere un conflitto dei dettagli software:  

   - **Mantieni le informazioni nel catalogo modificato localmente**: risolve il conflitto dei dettagli software mantenendo le informazioni di categorizzazione software del catalogo di Asset Intelligence esistenti. Quando si seleziona questa impostazione, lo stato del titolo software cambia da **Aggiornabile** a **Definito da utente**.  

   - **Sovrascrivi le informazioni nel catalogo modificato localmente con le informazioni del catalogo di System Center Online**: risolve il conflitto dei dettagli software sovrascrivendo le informazioni di categorizzazione software del catalogo di Asset Intelligence esistenti con le nuove informazioni ottenute da System Center Online. Quando si seleziona questa impostazione, lo stato del titolo software cambia da **Aggiornabile** a **Convalidato**.  

     Fare clic su **OK** per salvare la risoluzione del conflitto.  
