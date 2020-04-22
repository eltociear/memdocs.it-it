---
title: Creare report personalizzati
titleSuffix: Configuration Manager
description: È possibile definire modelli di report adeguati ai requisiti aziendali e quindi distribuire tali modelli in Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f2df88b4-c348-4dcf-854a-54fd6eedf485
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 590f3adec168fe6d7f4718505bd6f7d6b9f7c25f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692729"
---
# <a name="creating-custom-report-models-for-configuration-manager-in-sql-server-reporting-services"></a>Creazione di modelli di report personalizzati per Configuration Manager in SQL Server Reporting Services

*Si applica a: Configuration Manager (Current Branch)*

In Configuration Manager sono inclusi modelli di report di esempio, ma è possibile definire anche modelli di report che soddisfino requisiti aziendali specifici e quindi distribuire i modelli di report in Configuration Manager per usarli quando si creano nuovi report basati su modelli. Nella seguente tabella vengono illustrati i passaggi per creare e distribuire un modello di report di base.  

> [!NOTE]  
>  Per i passaggi relativi alla creazione di un modello di report più avanzato, vedere la sezione [Passaggi per la creazione di un modello di report avanzato in SQL Server Reporting Services](#AdvancedReportModel) di questo argomento.  

|Passaggio|Descrizione|Altre informazioni|  
|----------|-----------------|----------------------|  
|Verificare che sia installato SQL Server Business Intelligence Development Studio|I modelli di report sono progettati e creati utilizzando SQL Server Business Intelligence Development Studio. Verificare che SQL Server Business Intelligence Development Studio sia installato nel computer in cui viene creato il modello di report personalizzato.|Per ulteriori informazioni su SQL Server Business Intelligence Development Studio, vedere la documentazione di SQL Server 2008.|  
|Creare un progetto modello di report|Un progetto modello di report contiene la definizione dell'origine dei dati (un file DS), la definizione di una vista origine dati (un file DSV) e il modello di report (un file SMDL).|Per altre informazioni, vedere la sezione [Per creare il progetto modello di report](#BKMK_CreateReportModelProject) in questo argomento.|  
|Definire un'origine dati per un modello di report|Dopo aver creato un progetto modello di report, è necessario definire un'origine dati da cui estrarre i dati aziendali. In genere è il database del sito di Configuration Manager.|Per altre informazioni, vedere la sezione [Per definire l'origine dati per il modello di report](#BKMK_DefineReportModelDataSource) in questo argomento.|  
|Definire una vista origine dati per un modello di report|Al termine della definizione delle origini dati utilizzate nel progetto modello di report, il passaggio successivo consiste nella definizione di una vista origine dati per il progetto. Una vista origine dati è un modello di dati logico basato su uno o più origini dati. Le viste origine dati incapsulano l'accesso agli oggetti fisici, ad esempio tabelle e viste, contenuti in origini dati sottostanti. SQL Server Reporting Services genera il modello di report dalla vista origine dati.<br /><br /> Le viste origine dati facilitano il processo di progettazione del modello, offrendo una rappresentazione utile dei dati specificati. Senza modificare l'origine dati sottostante, è possibile rinominare campi e tabelle, nonché aggiungere campi aggregati e tabelle derivate in una vista origine dati. Per un modello efficiente, aggiungere alla vista origine dati solo le tabelle che si desidera utilizzare.|Per altre informazioni, vedere la sezione [Per definire la vista dell'origine dati per il modello di report](#BKMK_DefineReportModelDataSourceView) in questo argomento.|  
|Creare un modello di report|Un modello di report è un livello superiore di un database che identifica i ruoli, i campi e le entità aziendali. Se è stata eseguita la pubblicazione, utilizzando questi modelli gli utenti di Generatore report possono sviluppare report anche se non hanno familiarità con le strutture del database o se non sono in grado di comprendere e scrivere query. I modelli sono composti da set di elementi report correlati raggruppati con un nome descrittivo, rapporti predefiniti tra gli elementi aziendali e calcoli predefiniti. I modelli vengono definiti utilizzando un linguaggio XML denominato Semantic Model Definition Language (SMDL). L'estensione del nome file per i file del modello di report è SMDL.|Per altre informazioni, vedere la sezione [Per creare il modello di report](#BKMK_CreateReportModel) in questo argomento.|  
|Pubblicare un modello di report|Per creare un report utilizzando il modello appena creato, è necessario pubblicarlo in un server di report. In fase di pubblicazione, l'origine dati e la vista origine dati sono incluse nel modello.|Per altre informazioni, vedere la sezione [Per pubblicare il modello di report per l'utilizzo in SQL Server Reporting Services](#BKMK_PublishReportModel) in questo argomento.|  
|Distribuire il modello di report in Configuration Manager|Prima di usare un modello di report personalizzato in **Creazione guidata report** per creare un report basato su modello, è necessario distribuire il modello di report in Configuration Manager.|Per altre informazioni, vedere la sezione [Per distribuire il modello di report personalizzato in Configuration Manager](#BKMK_DeployReportModel) in questo argomento.|  

## <a name="steps-for-creating-a-basic-report-model-in-sql-server-reporting-services"></a>Passaggi per la creazione di un modello di report di base in SQL Server Reporting Services  
 Usare le procedure seguenti per creare un modello di report di base che gli utenti del sito possono usare per compilare report basati su modello specifici in base ai dati presenti in una singola vista del database di Configuration Manager. Creare un modello di report che fornisca informazioni sui computer client nel sito all'autore del report. Queste informazioni provengono dalla vista **v_R_System** nel database di Configuration Manager.  

 Verificare che nel computer in cui vengono eseguite tali procedure sia installato SQL Server Business Intelligence Development Studio e che il computer disponga della connettività di rete al server del punto di Reporting Services. Per informazioni dettagliate su SQL Server Business Intelligence Development Studio, vedere la documentazione di SQL Server 2008.  

###  <a name="to-create-the-report-model-project"></a><a name="BKMK_CreateReportModelProject"></a> Per creare il modello di report  

1.  Sul desktop fare clic su **Start**, quindi su **Microsoft SQL Server 2008**e selezionare **SQL Server Business Intelligence Development Studio**.  

2.  In seguito all'apertura di **SQL Server Business Intelligence Development Studio** in Microsoft Visual Studio, fare clic su **File**, quindi su **Nuovo**e selezionare **Progetto**.  

3.  Nella finestra di dialogo **Nuovo progetto** selezionare **Progetto modello di report** nell'elenco **Modelli** .  

4.  Nella casella **Nome** specificare un nome per questo modello di report. Per questo esempio, digitare **Modello_Semplificato**.  

5.  Per creare il progetto di modello di report, fare clic su **OK**.  

6.  La soluzione **Modello_Semplificato** viene visualizzata in **Esplora soluzioni**.  

    > [!NOTE]  
    >  Se il riquadro **Esplora soluzioni** non viene visualizzato, fare clic su **Visualizza**, quindi su **Esplora soluzioni**.  

###  <a name="to-define-the-data-source-for-the-report-model"></a><a name="BKMK_DefineReportModelDataSource"></a> Per definire la vista dell'origine dati per il modello di report  

1.  Nel riquadro **Esplora soluzioni** di **SQL Server Business Intelligence Development Studio**fare clic con il pulsante destro del mouse su **Origini dati** per selezionare **Aggiungi nuova origine dati**.  

2.  Nella pagina **Creazione guidata origine dati** fare clic su **Avanti**.  

3.  Nella pagina **Selezione metodo di definizione connessione** verificare che **Crea un'origine dati basata su una connessione nuova o esistente** sia selezionato, quindi fare clic su **Nuovo**.  

4.  Nella finestra di dialogo **Gestione connessione** specificare le proprietà di connessione seguenti per l'origine dati:  

    -   **Nome server**: digitare il nome del server di database del sito di Configuration Manager oppure selezionarlo nell'elenco. Se si usa un'istanza denominata anziché l'istanza predefinita, digitare &lt;*server database* >\\&lt;*nome istanza*>.  

    -   Selezionare **Usa autenticazione di Windows**.  

    -   Nell'elenco **Selezionare o immettere un nome di database** selezionare il nome del database del sito di Configuration Manager.  

5.  Per verificare la connessione al database, fare clic su **Verifica connessione**.  

6.  Se la connessione ha esito positivo, fare clic su **OK** per chiudere la finestra di dialogo **Gestione connessione** . Se non è possibile effettuare la connessione, verificare la correttezza delle informazioni immesse, quindi fare di nuovo clic su **Verifica connessione** .  

7.  Nella pagina **Selezione metodo di definizione connessione** verificare che **Crea un'origine dati basata su una connessione nuova o esistente** sia selezionato, assicurarsi che l'origine dati appena specificata sia selezionata in **Connessioni dati**e infine fare clic su **Avanti**.  

8.  In **Nome origine dati**specificare un nome per l'origine dati, quindi fare clic su **Fine**. Per questo esempio, digitare **Modello_Semplificato**.  

9. L'origine dati **Modello_Semplificato.ds** viene ora visualizzata in **Esplora soluzioni** sotto il nodo **Origini dati** .  

    > [!NOTE]  
    >  Per modificare le proprietà di un'origine dati esistente, fare doppio clic sull'origine dati nella cartella **Origini dati** del riquadro **Esplora soluzioni** per visualizzare le proprietà delle origini dati in Progettazione origine dati.  

###  <a name="to-define-the-data-source-view-for-the-report-model"></a><a name="BKMK_DefineReportModelDataSourceView"></a> Per definire la vista dell'origine dati per il modello di report  

1.  In **Esplora soluzioni**fare clic con il pulsante destro del mouse su **Viste origine dati** per selezionare **Aggiungi nuova vista origine dati**.  

2.  Nella pagina **Creazione guidata vista origine dati** fare clic su **Avanti**. Verrà visualizzata la pagina **Selezione origine dati** .  

3.  Nella finestra **Origini dati relazionali** verificare che l'origine dati **Modello_Semplificato** sia selezionata, quindi fare clic su **Avanti**.  

4.  Nella pagina **Selezione tabelle e viste** selezionare la seguente vista dall'elenco **Oggetti disponibili** per l'uso nel modello di report: **v_R_System (dbo)** .  

    > [!TIP]  
    >  Per agevolare l'individuazione delle viste nell'elenco **Oggetti disponibili** , fare clic sull'intestazione **Nome** nella parte superiore dell'elenco per disporre gli oggetti in ordine alfabetico.  

5.  Dopo avere selezionato la vista, fare clic su **>** per trasferire l'oggetto nell'elenco **Oggetti inclusi** .  

6.  Se viene visualizzata la pagina **Corrispondenza nomi** , accettare le selezioni predefinite, quindi fare clic su **Avanti**.  

7.  Dopo avere selezionato gli oggetti necessari, fare clic su **Avanti**, quindi specificare un nome per la vista dell'origine dati. Per questo esempio, digitare **Modello_Semplificato**.  

8.  Fare clic su **Fine**. La vista dell'origine dati **Modello_Semplificato.dsv** viene visualizzata nella cartella **Viste origine dati** di **Esplora soluzioni**.  

###  <a name="to-create-the-report-model"></a><a name="BKMK_CreateReportModel"></a> To create the report model  

1.  In **Esplora soluzioni**fare clic con il pulsante destro del mouse su **Modelli di report** per selezionare **Aggiungi nuovo modello di report**.  

2.  Nella pagina **Creazione guidata modello report** fare clic su **Avanti**.  

3.  Nella pagina **Selezione vista origine dati** selezionare la vista dell'origine dati dall'elenco **Viste origine dati disponibili** , quindi fare clic su **Avanti**. Per questo esempio, selezionare **Modello_Semplificato.dsv**.  

4.  Nella pagina **Selezionare regole generazione modello di report** accettare i valori predefiniti, quindi fare clic su **Avanti**.  

5.  Nella pagina **Raccolta statistiche modello** verificare che **Aggiorna statistiche modello prima di generare** sia selezionato, quindi fare clic su **Avanti**.  

6.  Nella pagina **Completamento procedura guidata** specificare un nome per il modello di report. Per questo esempio, verificare che **Modello_Semplificato** venga visualizzato.  

7.  Per completare la procedura guidata e creare il modello di report, fare clic su **Esegui**.  

8.  Per uscire dalla procedura guidata, fare clic su **Fine**. Il modello di report viene visualizzato nella finestra di progettazione.  

###  <a name="to-publish-the-report-model-for-use-in-sql-server-reporting-services"></a><a name="BKMK_PublishReportModel"></a> Per pubblicare il modello di report per l'utilizzo in SQL Server Reporting Services  

1.  In **Esplora soluzioni**fare clic con il pulsante destro del mouse sul modello di report, quindi selezionare **Distribuisci**. Per questo esempio, il modello di report è **Modello_Semplificato.smdl**.  

2.  Esaminare lo stato della distribuzione nell'angolo inferiore sinistro della finestra **SQL Server Business Intelligence Development Studio** . Al termine della distribuzione, verrà visualizzato il messaggio **Distribuzione completata** . Se la distribuzione non riesce, il motivo dell'errore verrà visualizzato nella finestra **Output** . Il nuovo modello di report è ora disponibile nel sito Web di SQL Server Reporting Services.  

3.  Fare clic su **File**, quindi su **Salva tutto**e infine chiudere **SQL Server Business Intelligence Development Studio**.  

###  <a name="to-deploy-the-custom-report-model-to-configuration-manager"></a><a name="BKMK_DeployReportModel"></a> To deploy the custom report model to Configuration Manager  

1. Individuare la cartella in cui è stato creato il progetto di modello di report. Ad esempio, %*PROFILOUTENTE*%\Documents\Visual Studio 2008\Projects\\ *&lt;Nome progetto\>.*  

2. Copiare i seguenti file dalla cartella del progetto di modello di report in una cartella temporanea nel computer:  

   -   *&lt;Nome modello\>* **.dsv**  

   -   *&lt;Nome modello\>* **.smdl**  

3. Aprire i file precedenti utilizzando un editor di testo, ad esempio Blocco note.  

4. Nel file _&lt;Nome modello\>_ **.dsv** individuare la prima riga del file, simile alla seguente:  

    `<DataSourceView xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">`

    Modificare la riga come segue:  

    `<DataSourceView xmlns="<https://schemas.microsoft.com/analysisservices/2003/engine>" xmlns:xsi="RelationalDataSourceView">`  

5. Copiare l'intero contenuto del file negli Appunti di Windows.  

6. Chiudere il file _&lt;Nome modello\>_ **.dsv**.  

7. Nel file _&lt;Nome modello\>_ **.smdl** individuare le ultime tre righe del file, simili alle seguenti:  

    `</Entity>`  

    `</Entities>`  

    `</SemanticModel>`  

8. Incollare il contenuto del file _&lt;Nome modello\>_ **.dsv** direttamente prima dell'ultima riga del file ( **&lt;SemanticModel\>** ).  

9. Salvare e chiudere il file _&lt;Nome modello\>_ **.smdl**.  

10. Copiare il file _&lt;Nome modello\>_ **.smdl** nella cartella *%programmi%* \Microsoft Configuration Manager \AdminConsole\XmlStorage\Other nel server del sito di Configuration Manager.  

    > [!IMPORTANT]  
    >  Dopo aver copiato il file del modello di report nel server del sito di Configuration Manager, sarà necessario chiudere e riavviare la console di Configuration Manager prima di usare il modello di report in **Creazione guidata report**.  

##  <a name="steps-for-creating-an-advanced-report-model-in-sql-server-reporting-services"></a><a name="AdvancedReportModel"></a> Passaggi per la creazione di un modello di report avanzato in SQL Server Reporting Services  
 Usare le procedure seguenti per creare un modello di report avanzato che gli utenti del sito possono usare per compilare report basati su modello specifici in base ai dati presenti in più viste del database di Configuration Manager. Creare un modello di report che fornisca all'autore del report informazioni sui computer client e sul sistema operativo installato in tali computer. Queste informazioni provengono dalle seguenti viste del database di Configuration Manager:  

- **V_R_System**: contiene informazioni sui computer individuati e sul client di Configuration Manager.  

- **V_GS_OPERATING_SYSTEM**: contiene informazioni sul sistema operativo installato nel computer client.  

  Gli elementi selezionati nelle visualizzazioni precedenti vengono consolidati in un unico elenco, vengono associati a nomi descrittivi e quindi forniti all'autore del report in Generatore report per l'inclusione in report specifici.  

  Verificare che nel computer in cui vengono eseguite tali procedure sia installato SQL Server Business Intelligence Development Studio e che il computer disponga della connettività di rete al server del punto di Reporting Services. Per informazioni dettagliate su SQL Server Business Intelligence Development Studio, vedere la documentazione di SQL Server.  

#### <a name="to-create-the-report-model-project"></a>To create the report model project  

1.  Sul desktop fare clic su **Start**, quindi su **Microsoft SQL Server 2008**e selezionare **SQL Server Business Intelligence Development Studio**.  

2.  In seguito all'apertura di **SQL Server Business Intelligence Development Studio** in Microsoft Visual Studio, fare clic su **File**, quindi su **Nuovo**e selezionare **Progetto**.  

3.  Nella finestra di dialogo **Nuovo progetto** selezionare **Progetto modello di report** nell'elenco **Modelli** .  

4.  Nella casella **Nome** specificare un nome per questo modello di report. Per questo esempio, digitare **Modello_Avanzato**.  

5.  Per creare il progetto di modello di report, fare clic su **OK**.  

6.  La soluzione **Modello_Avanzato** viene visualizzata in **Esplora soluzioni**.  

    > [!NOTE]  
    >  Se il riquadro **Esplora soluzioni** non viene visualizzato, fare clic su **Visualizza**, quindi su **Esplora soluzioni**.  

#### <a name="to-define-the-data-source-for-the-report-model"></a>Per definire l'origine dati per il modello di report  

1.  Nel riquadro **Esplora soluzioni** di **SQL Server Business Intelligence Development Studio**fare clic con il pulsante destro del mouse su **Origini dati** per selezionare **Aggiungi nuova origine dati**.  

2.  Nella pagina **Creazione guidata origine dati** fare clic su **Avanti**.  

3.  Nella pagina **Selezione metodo di definizione connessione** verificare che **Crea un'origine dati basata su una connessione nuova o esistente** sia selezionato, quindi fare clic su **Nuovo**.  

4.  Nella finestra di dialogo **Gestione connessione** specificare le proprietà di connessione seguenti per l'origine dati:  

    -   **Nome server**: digitare il nome del server di database del sito di Configuration Manager oppure selezionarlo nell'elenco. Se si usa un'istanza denominata anziché l'istanza predefinita, digitare &lt;*server database* >\\&lt;*nome istanza*>.  

    -   Selezionare **Usa autenticazione di Windows**.  

    -   Nell'elenco **Selezionare o immettere un nome di database** selezionare il nome del database del sito di Configuration Manager.  

5.  Per verificare la connessione al database, fare clic su **Verifica connessione**.  

6.  Se la connessione ha esito positivo, fare clic su **OK** per chiudere la finestra di dialogo **Gestione connessione** . Se non è possibile effettuare la connessione, verificare la correttezza delle informazioni immesse, quindi fare di nuovo clic su **Verifica connessione** .  

7.  Nella pagina **Selezione metodo di definizione connessione** verificare che **Crea un'origine dati basata su una connessione nuova o esistente** sia selezionato, assicurarsi che l'origine dati appena specificata sia selezionata nella casella di riepilogo **Connessioni dati** e infine fare clic su **Avanti**.  

8.  In **Nome origine dati**specificare un nome per l'origine dati, quindi fare clic su **Fine**. Per questo esempio, digitare **Modello_Avanzato**.  

9. L'origine dati **Modello_Avanzato.ds** viene visualizzata in **Esplora soluzioni** sotto il nodo **Origini dati** .  

    > [!NOTE]  
    >  Per modificare le proprietà di un'origine dati esistente, fare doppio clic sull'origine dati nella cartella **Origini dati** del riquadro **Esplora soluzioni** per visualizzare le proprietà delle origini dati in Progettazione origine dati.  

#### <a name="to-define-the-data-source-view-for-the-report-model"></a>Per definire la vista dell'origine dati per il modello di report  

1. In **Esplora soluzioni**fare clic con il pulsante destro del mouse su **Viste origine dati** per selezionare **Aggiungi nuova vista origine dati**.  

2. Nella pagina **Creazione guidata vista origine dati** fare clic su **Avanti**. Verrà visualizzata la pagina **Selezione origine dati** .  

3. Nella finestra **Origini dati relazionali** verificare che l'origine dati **Modello_Avanzato** sia selezionata, quindi fare clic su **Avanti**.  

4. Nella pagina **Selezione tabelle e viste** selezionare le viste seguenti dall'elenco **Oggetti disponibili** per l'utilizzo nel modello di report:  

   - **v_R_System (dbo)**  

   - **v_GS_OPERATING_SYSTEM (dbo)**  

     Dopo avere selezionato ogni vista, fare clic su **>** per trasferire l'oggetto nell'elenco **Oggetti inclusi** .  

   > [!TIP]  
   >  Per agevolare l'individuazione delle viste nell'elenco **Oggetti disponibili** , fare clic sull'intestazione **Nome** nella parte superiore dell'elenco per disporre gli oggetti in ordine alfabetico.  

5. Se viene visualizzata la finestra di dialogo **Corrispondenza nomi** , accettare le selezioni predefinite, quindi fare clic su **Avanti**.  

6. Dopo avere selezionato gli oggetti necessari, fare clic su **Avanti**, quindi specificare un nome per la vista dell'origine dati. Per questo esempio, digitare **Modello_Avanzato**.  

7. Fare clic su **Fine**. La vista dell'origine dati **Modello_Avanzato.dsv** viene visualizzata nella cartella **Viste origine dati** di **Esplora soluzioni**.  

#### <a name="to-define-relationships-in-the-data-source-view"></a>Per definire le relazioni nella vista dell'origine dati  

1.  In **Esplora soluzioni**fare doppio clic su **Modello_Avanzato.dsv** per aprire la finestra di progettazione.  

2.  Fare clic con il pulsante destro del mouse sulla barra del titolo della finestra **v_R_System** per selezionare **Sostituisci tabella**, quindi fare clic su **Con nuova query denominata**.  

3.  Nella finestra di dialogo **Crea query denominata** fare clic sull'icona **Aggiungi tabella** . In genere è l'ultima icona sulla barra multifunzione.  

4.  Nella finestra di dialogo **Aggiungi tabella** fare clic sulla scheda **Viste** , selezionare **V_GS_OPERATING_SYSTEM** dall'elenco, quindi fare clic su **Aggiungi**.  

5.  Fare clic su **Chiudi** per chiudere la finestra di dialogo **Aggiungi tabella** .  

6.  Nella finestra di dialogo **Crea query denominata** specificare le seguenti informazioni:  

    -   **Nome:** specificare il nome per la query. Per questo esempio, digitare **Modello_Avanzato**.  

    -   **Descrizione:** specificare una descrizione per la query. Per questo esempio, digitare **Esempio di modello di report di Reporting Services**.  

7.  Nella finestra **v_R_System** selezionare gli elementi seguenti dall'elenco di oggetti da visualizzare nel modello di report:  

    -   **ResourceID**  

    -   **ResourceType**  

    -   **Active0**  

    -   **AD_Domain_Name0**  

    -   **AD_SiteName0**  

    -   **Client0**  

    -   **Client_Type0**  

    -   **Client_Version0**  

    -   **CPUType0**  

    -   **Hardware_ID0**  

    -   **User_Domain0**  

    -   **User_Name0**  

    -   **Netbios_Name0**  

    -   **Operating_System_Name_and0**  

8.  Nella casella **v_GS_OPERATING_SYSTEM** selezionare gli elementi seguenti dall'elenco di oggetti da visualizzare nel modello di report:  

    -   **ResourceID**  

    -   **Caption0**  

    -   **CountryCode0**  

    -   **CSDVersion0**  

    -   **Description0**  

    -   **InstallDate0**  

    -   **LastBootUpTime0**  

    -   **Locale0**  

    -   **Manufacturer0**  

    -   **Version0**  

    -   **WindowsDirectory0**  

9. Per presentare gli oggetti in queste viste come un unico elenco per l'autore del report, sarà necessario specificare una relazione tra le due tabelle o viste, utilizzando un join. È possibile unire le due viste utilizzando l'oggetto **ResourceID**, che viene visualizzato in entrambe le visualizzazioni.  

10. Nella finestra **v_R_System** fare clic sull'oggetto **ResourceID** e, tenendo premuto il pulsante del mouse, trascinarlo sull'oggetto **ResourceID** nella finestra **v_GS_OPERATING_SYSTEM** .  

11. Fare clic su **OK**.  

12. La finestra **Modello_Avanzato** sostituirà la finestra **v_R_System** e conterrà tutti gli oggetti necessari per il modello di report dalle viste **v_R_System** e **v_GS_OPERATING_SYSTEM** . È ora possibile eliminare la finestra **v_GS_OPERATING_SYSTEM** dalla finestra di progettazione delle viste di origine dati. Fare clic con il pulsante destro del mouse sulla barra del titolo della finestra **v_GS_OPERATING_SYSTEM** per selezionare **Elimina tabella da vista origine dati**. Nella finestra di dialogo **Elimina oggetti** fare clic su **OK** per confermare l'eliminazione.  

13. Fare clic su **File**, quindi su **Salva tutto**.  

#### <a name="to-create-the-report-model"></a>To create the report model  

1.  In **Esplora soluzioni**fare clic con il pulsante destro del mouse su **Modelli di report** per selezionare **Aggiungi nuovo modello di report**.  

2.  Nella pagina **Creazione guidata modello report** fare clic su **Avanti**.  

3.  Nella pagina **Selezione vista origine dati** selezionare la vista dell'origine dati dall'elenco **Viste origine dati disponibili** , quindi fare clic su **Avanti**. Per questo esempio, selezionare **Modello_Semplificato.dsv**.  

4.  Nella pagina **Selezionare regole generazione modello di report** non modificare i valori predefiniti, quindi fare clic su **Avanti**.  

5.  Nella pagina **Raccolta statistiche modello** verificare che **Aggiorna statistiche modello prima di generare** sia selezionato, quindi fare clic su **Avanti**.  

6.  Nella pagina **Completamento procedura guidata** specificare un nome per il modello di report. Per questo esempio, verificare che **Modello_Avanzato** venga visualizzato.  

7.  Per completare la procedura guidata e creare il modello di report, fare clic su **Esegui**.  

8.  Per uscire dalla procedura guidata, fare clic su **Fine**.  

9. Il modello di report viene visualizzato nella finestra di progettazione.  

#### <a name="to-modify-object-names-in-the-report-model"></a>Per modificare i nomi degli oggetti nel modello di report  

1.  In **Esplora soluzioni**fare clic con il pulsante destro del mouse su un modello di report, quindi scegliere **Visualizza finestra di progettazione**. Per questo esempio, selezionare **Modello_Avanzato.dsv**.  

2.  Nella vista di progettazione del modello di report fare clic con il pulsante destro del mouse su qualsiasi nome di oggetto, quindi scegliere **Rinomina**.  

3.  Digitare un nuovo nome per l'oggetto selezionato e quindi premere INVIO. È ad esempio possibile rinominare l'oggetto **CSD_Version_0** come **Versione del Service Pack di Windows**.  

4.  Dopo avere rinominato gli oggetti, fare clic su **File**, quindi su **Salva tutto**.  

#### <a name="to-publish-the-report-model-for-use-in-sql-server-reporting-services"></a>Per pubblicare il modello di report per l'utilizzo in SQL Server Reporting Services  

1.  In **Esplora soluzioni**fare clic con il pulsante destro del mouse su **Modello_Avanzato.dsv** , quindi scegliere **Distribuisci**.  

2.  Esaminare lo stato della distribuzione nell'angolo inferiore sinistro della finestra **SQL Server Business Intelligence Development Studio** . Al termine della distribuzione, verrà visualizzato il messaggio **Distribuzione completata** . Se la distribuzione non riesce, il motivo dell'errore verrà visualizzato nella finestra **Output** . Il nuovo modello di report è ora disponibile nel sito Web di SQL Server Reporting Services.  

3.  Fare clic su **File**, quindi su **Salva tutto**e infine chiudere **SQL Server Business Intelligence Development Studio**.  

#### <a name="to-deploy-the-custom-report-model-to-configuration-manager"></a>To deploy the custom report model to Configuration Manager  

1. Individuare la cartella in cui è stato creato il progetto di modello di report. Ad esempio, %*PROFILOUTENTE*%\Documents\Visual Studio 2008\Projects\\ *&lt;Nome progetto\>.*  

2. Copiare i seguenti file dalla cartella del progetto di modello di report in una cartella temporanea nel computer:  

   -   *&lt;Nome modello\>* **.dsv**  

   -   *&lt;Nome modello\>* **.smdl**  

3. Aprire i file precedenti utilizzando un editor di testo, ad esempio Blocco note.  

4. Nel file _&lt;Nome modello\>_ **.dsv** individuare la prima riga del file, simile alla seguente:  

    `<DataSourceView xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">`

    Modificare la riga come segue:  

    `<DataSourceView xmlns="<https://schemas.microsoft.com/analysisservices/2003/engine>" xmlns:xsi="RelationalDataSourceView">`

5. Copiare l'intero contenuto del file negli Appunti di Windows.  

6. Chiudere il file _&lt;Nome modello\>_ **.dsv**.  

7. Nel file _&lt;Nome modello\>_ **.smdl** individuare le ultime tre righe del file, simili alle seguenti:  

    `</Entity>`  

    `</Entities>`  

    `</SemanticModel>`  

8. Incollare il contenuto del file _&lt;Nome modello\>_ **.dsv** direttamente prima dell'ultima riga del file ( **&lt;SemanticModel\>** ).  

9. Salvare e chiudere il file _&lt;Nome modello\>_ **.smdl**.  

10. Copiare il file _&lt;Nome modello\>_ **.smdl** nella cartella *%programmi%* \Microsoft Configuration Manager\AdminConsole\XmlStorage\Other nel server del sito di Configuration Manager.  

    > [!IMPORTANT]  
    >  Dopo aver copiato il file del modello di report nel server del sito di Configuration Manager, sarà necessario chiudere e riavviare la console di Configuration Manager prima di usare il modello di report in **Creazione guidata report**.  
