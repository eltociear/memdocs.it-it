---
title: Gestire gli aggiornamenti delle app Microsoft 365
titleSuffix: Configuration Manager
description: Configuration Manager sincronizza gli aggiornamenti del client di Microsoft 365 Apps dal catalogo di Windows Server Update Services nel server del sito per rendere disponibili gli aggiornamenti per la distribuzione ai client.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 08/11/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: eac542eb-9aa1-4c63-b493-f80128e4e99b
ms.openlocfilehash: e0ef22ec7bc5eb3d6b9ac3800b3e97374421944c
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/25/2020
ms.locfileid: "88819797"
---
# <a name="manage-microsoft-365-apps-with-configuration-manager"></a>Gestire Microsoft 365 Apps con Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

> [!Note]
> A partire dal 21 aprile 2020, Office 365 ProPlus viene rinominato come **App di Microsoft 365 per grandi imprese**. Per altre informazioni, vedere [Modifica del nome di Office 365 ProPlus](/deployoffice/name-change). È comunque possibile che vengano ancora visualizzati riferimenti al nome precedente nella console di Configuration Manager e nella documentazione di supporto mentre la console viene aggiornata.

Configuration Manager consente di gestire Microsoft 365 Apps nei modi seguenti:

- [Distribuire Microsoft 365 Apps](#bkmk_deploy): è possibile avviare il programma di installazione di Microsoft 365 Apps dal [dashboard di gestione client di Office 365](office-365-dashboard.md) per semplificare l'esperienza iniziale di installazione di Microsoft 365 Apps. La procedura guidata consente di configurare le impostazioni di installazione di Microsoft 365 Apps, scaricare file dalle reti di distribuzione del contenuto (CDN) e creare e distribuire un'applicazione script con il contenuto.

- [Distribuire gli aggiornamenti di Microsoft 365 Apps](#bkmk_update): è possibile gestire gli aggiornamenti del client di Microsoft 365 Apps usando il flusso di lavoro Gestione aggiornamenti software. Quando pubblica un nuovo aggiornamento del client di Microsoft 365 Apps nella rete per la distribuzione di contenuti (CDN) di Office, Microsoft pubblica anche un pacchetto di aggiornamento per Windows Server Update Services (WSUS). Dopo che Configuration Manager ha sincronizzato l'aggiornamento di Microsoft 365 Apps dal catalogo di Windows Server Update Services nel server del sito, l'aggiornamento è disponibile per la distribuzione ai client.

   > [!NOTE]
   > A partire da Configuration Manager versione 2002, è possibile importare gli aggiornamenti di Microsoft 365 Apps in ambienti disconnessi. Per altre informazioni, vedere [Sincronizzare gli aggiornamenti di Microsoft 365 Apps da un punto di aggiornamento software disconnesso](../get-started/synchronize-office-updates-disconnected.md).   

- [Aggiungere lingue per i download degli aggiornamenti di Microsoft 365 Apps](#bkmk_o365_lang): è possibile aggiungere il supporto per Configuration Manager per scaricare gli aggiornamenti in tutte le lingue supportate da Microsoft 365 Apps. Non è necessario che Configuration Manager supporti la lingua se è supportata da Microsoft 365 Apps. Prima di Configuration Manager versione 1610, è necessario scaricare e distribuire gli aggiornamenti nelle stesse lingue configurate nei client di Microsoft 365 Apps.

- [Modificare il canale di aggiornamento](#bkmk_channel): è possibile usare Criteri di gruppo per distribuire ai client di Microsoft 365 Apps la modifica del valore della chiave del Registro di sistema relativa al canale di aggiornamento.

Per esaminare le informazioni sul client di Microsoft 365 Apps e avviare alcune di queste azioni di gestione di Microsoft 365 Apps, usare il [dashboard di Gestione client di Office 365](office-365-dashboard.md).

## <a name="deploy-microsoft-365-apps"></a><a name="bkmk_deploy"></a> Distribuire Microsoft 365 Apps
Avviare il programma di installazione di Microsoft 365 Apps dal dashboard di gestione client di Office 365 per l'installazione iniziale di Microsoft 365 Apps. La procedura guidata consente di configurare le impostazioni di installazione di Microsoft 365 Apps, scaricare file dalle reti di distribuzione del contenuto (CDN) e creare e distribuire un'applicazione script per i file. Fino a quando Microsoft 365 Apps non viene installato nei client e viene eseguita l'[attività di aggiornamento automatico di Microsoft 365 Apps](/deployoffice/overview-update-process-microsoft-365-apps), gli aggiornamenti di Microsoft 365 Apps non sono applicabili. A scopo di test, è possibile eseguire l'attività di aggiornamento manualmente.

Per le versioni di Configuration Manager precedenti, è necessario eseguire la procedura seguente per installare Microsoft 365 Apps nei client per la prima volta:
- Scaricare lo Strumento di distribuzione di Office (ODT)
- Scaricare i file di origine dell'installazione di Microsoft 365 Apps, inclusi tutti i language pack necessari.
- Generare il file Configuration.xml che specifica la versione e il canale corretti di Microsoft 365 Apps.
- Creare e distribuire un pacchetto legacy oppure un'applicazione script per i client, per installare Microsoft 365 Apps.

### <a name="requirements"></a>Requisiti
- Il computer che esegue il programma di installazione deve avere accesso a Internet.  
- L'utente che esegue il programma di installazione deve avere accesso in **lettura** e **scrittura** alla condivisione dei contenuti specificata nella procedura guidata.
- Se si riceve l'errore di download 404, copiare i file seguenti nella cartella %temp% dell'utente:
  - [releasehistory.xml](https://officecdn.microsoft.com/pr/wsus/releasehistory.cab)
  - [o365client_32bit.xml](https://officecdn.microsoft.com/pr/wsus/ofl.cab)  

### <a name="deploy-microsoft-365-apps-using-configuration-manager-version-1806-or-higher"></a>Distribuire Microsoft 365 Apps usando Configuration Manager 1806 o versioni successive: 
A partire da Configuration Manager 1806, lo Strumento di personalizzazione di Office è integrato con il programma di installazione nella console di Configuration Manager. Quando si crea una distribuzione per Microsoft 365 Apps, è possibile configurare dinamicamente le impostazioni di gestibilità più recenti. <!--1358149-->

1. Nella console di Configuration Manager passare a **Raccolta software** > **Panoramica** > **Office 365 Client Management** (Gestione Client di Office 365).
2. Fare clic su **Office 365 Installer** (Programma di installazione di Office 365) nel riquadro in alto a destro. Verrà avviata l'installazione guidata.
3. Nella pagina **Impostazioni applicazione** specificare il nome e la descrizione per l'app, immettere il percorso di download per i file e quindi fare clic su **Avanti**. Il percorso deve essere specificato nel formato &#92;&#92;*server*&#92;*condivisione*.
4. Nella pagina **Impostazioni di Office** fare clic su **Vai allo Strumento di personalizzazione di Office**. Verrà aperto lo [Strumento di personalizzazione di Office per A portata di clic](https://config.office.com).
5. Configurare le impostazioni desiderate per l'installazione di Microsoft 365 Apps. Fare clic su **Invia** nell'angolo in alto a destra della pagina quando si completa la configurazione. 
6. Nella pagina **Distribuzione** stabilire se si vuole eseguire la distribuzione subito o in un secondo momento. Se si sceglie di eseguire la distribuzione in un secondo momento, è possibile trovare l'applicazione in **Raccolta Software** > **Gestione applicazioni** > **Applicazioni**.  
7. Verificare le impostazioni nella pagina **Riepilogo**. 
8. Fare clic su **Avanti** e quindi su **Chiudi** una volta completata la procedura guidata. 

### <a name="deploy-microsoft-365-apps-using-configuration-manager-version-1802-and-prior"></a>Distribuire Microsoft 365 Apps usando Configuration Manager 1802 o versioni successive:

1. Nella console di Configuration Manager passare a **Raccolta software** > **Panoramica** > **Office 365 Client Management** (Gestione Client di Office 365).
2. Fare clic su **Office 365 Installer** (Programma di installazione di Office 365) nel riquadro in alto a destro. Verrà avviata l'installazione guidata.
3. Nella pagina **Impostazioni applicazione** specificare il nome e la descrizione per l'app, immettere il percorso di download per i file e quindi fare clic su **Avanti**. Il percorso deve essere specificato nel formato &#92;&#92;*server*&#92;*condivisione*.
4. Nella pagina **Importa le impostazioni del client** scegliere se importare le impostazioni del client di Microsoft 365 Apps da un file di configurazione XML esistente o se specificare manualmente le impostazioni. Al termine fare clic su **Avanti**.  

    Se già si dispone di un file di configurazione, immettere il percorso del file e andare al passaggio 7. È necessario specificare il percorso nel formato &#92;&#92;*server*&#92;*condivisione*&#92;*nomefile*.XML.
    > [!IMPORTANT]    
    > Il file di configurazione XML deve contenere solo [lingue supportate da Office 2016](/deployoffice/office2016/language-identifiers-and-optionstate-id-values-in-office-2016).

5. Nella pagina **Prodotti client** selezionare la famiglia di prodotti Microsoft 365 Apps in uso. Selezionare le applicazioni da includere. Selezionare i prodotti aggiuntivi che devono essere inclusi e fare clic su **Avanti**.
6. Nella pagina **Impostazioni client** scegliere le impostazioni da includere e fare clic su **Avanti**.
7. Nella pagina **Distribuzione** scegliere se distribuire l'applicazione, quindi fare clic su pagina **Avanti**. <br/>Se si sceglie di non distribuire il pacchetto nella procedura guidata, andare al passaggio 9.
8. Configurare il resto delle pagine della procedura guidata con le stesse impostazioni di una distribuzione di applicazioni standard. Per i dettagli, vedere [Create and deploy an application](../../apps/get-started/create-and-deploy-an-application.md) (Creare e distribuire un'applicazione).
9. Completare la procedura guidata.
10. È possibile distribuire o modificare l'applicazione da **Raccolta software** > **Panoramica** > **Gestione applicazioni** > **Applicazioni**.

Dopo la creazione e la distribuzione di applicazioni di Microsoft 365 Apps mediante il programma di installazione, Configuration Manager non gestirà gli aggiornamenti di Microsoft 365 Apps per impostazione predefinita. Per consentire ai client di Microsoft 365 Apps di ricevere gli aggiornamenti da Configuration Manager, vedere [Distribuire gli aggiornamenti di Microsoft 365 Apps con Configuration Manager](#bkmk_update).

Dopo la distribuzione di Microsoft 365 Apps, è possibile creare regole di distribuzione automatica per gestire le app. Per creare una regola di distribuzione automatica per Microsoft 365 Apps, fare clic su **Crea una regola di distribuzione automatica** nel [dashboard di Gestione client di Office 365](office-365-dashboard.md). Selezionare **Client Office 365** quando si sceglie il prodotto. Per altre informazioni, vedere [Distribuire automaticamente gli aggiornamenti software](automatically-deploy-software-updates.md).


## <a name="drill-through-required-microsoft-365-apps-updates"></a>Eseguire il drill-through degli aggiornamenti obbligatori di Microsoft 365 Apps
<!--4224414-->
*(Funzionalità introdotta nella versione 1906)*

È possibile esaminare nel dettaglio le statistiche di conformità per trovare i dispositivi che richiedono un aggiornamento software delle app Microsoft 365. Per visualizzare l'elenco dei dispositivi, è necessaria l'autorizzazione per visualizzare gli aggiornamenti e le raccolte a cui appartengano i dispositivi. Per eseguire il drill-down nell'elenco dei dispositivi:

1. Passare a **Raccolta software** > **Gestione client di Office 365** > **Aggiornamenti di Office 365**.
1. Selezionare tutti gli aggiornamenti richiesti da almeno un dispositivo.
1. Esaminare la scheda **Riepilogo** e individuare il grafico a torta in **Statistiche**.
1. Selezionare il collegamento ipertestuale **View Required** (Visualizza richiesto) accanto al grafico a torta per eseguire il drill-down nell'elenco dei dispositivi.
1. Questa azione consente di visualizzare un nodo temporaneo in **Dispositivi** dove è possibile visualizzare i dispositivi che richiedono l'aggiornamento. È anche possibile eseguire azioni per il nodo, come creare una nuova raccolta dall'elenco.


## <a name="deploy-microsoft-365-apps-updates"></a><a name="bkmk_update"></a> Distribuire gli aggiornamenti di Microsoft 365 Apps

Eseguire i passaggi seguenti per distribuire gli aggiornamenti di Microsoft 365 Apps con Configuration Manager:

1. [Verificare i requisiti](/DeployOffice/manage-updates-to-office-365-proplus-with-system-center-configuration-manager#requirements-for-using-configuration-manager-to-manage-office-365-client-updates) per l'uso di Configuration Manager per la gestione degli aggiornamenti del client di Microsoft 365 Apps nella sezione **Requisiti per gestire gli aggiornamenti del client di Microsoft 365 Apps usando Configuration Manager** dell'articolo.  

2. [Configurare i punti di aggiornamento software](../get-started/configure-classifications-and-products.md) per sincronizzare gli aggiornamenti del client di Microsoft 365 Apps. Impostare gli **aggiornamenti** per la classificazione e selezionare il **client di Office 365** per il prodotto. Sincronizzare gli aggiornamenti software dopo aver configurato i punti di aggiornamento software per l'uso della classificazione **Aggiornamenti**.
3. Abilitare i client di Microsoft 365 Apps per la ricezione di aggiornamenti da Configuration Manager. Usare le impostazioni client di Configuration Manager o Criteri di gruppo per abilitare il client.

    **Metodo 1**: a partire dalla versione 1606 di Configuration Manager, è possibile usare l'impostazione del client di Configuration Manager per la gestione dell'agente client di Microsoft 365 Apps. Dopo aver configurato questa impostazione e distribuito gli aggiornamenti di Microsoft 365 Apps, l'agente client di Configuration Manager comunica con l'agente client di Microsoft 365 Apps per scaricare gli aggiornamenti da un punto di distribuzione e installarli. Configuration Manager esegue l'inventario delle impostazioni client di Microsoft 365 Apps.    

      1. Nella console di Configuration Manager fare clic su **Amministrazione** > **Panoramica** > **Impostazioni client**.  

      2. Aprire le impostazioni del dispositivo appropriato per abilitare l'agente client. Per altre informazioni su come configurare le impostazioni client predefinite e personalizzate, vedere [Come configurare le impostazioni client](../../core/clients/deploy/configure-client-settings.md).  

      3. Fare clic su **Aggiornamenti software** e selezionare **Sì** per l'impostazione **Abilita la gestione dell'agente client di Office 365**.  

    **Metodo 2**:  [abilitare i client di Microsoft 365 Apps per la ricezione di aggiornamenti](/DeployOffice/manage-updates-to-office-365-proplus-with-system-center-configuration-manager#BKMK_EnableClient) da Configuration Manager usando lo Strumento di distribuzione di Office o Criteri di gruppo.  

4. [Distribuire gli aggiornamenti di Microsoft 365 Apps](deploy-software-updates.md) ai client.

> [!NOTE]  
>
> Se Microsoft 365 Apps è stato installato di recente e a seconda del modo di installazione, è possibile che il canale di aggiornamento non sia ancora stato impostato. In tal caso, gli aggiornamenti distribuiti verranno rilevati come non applicabili. È presente un'[attività pianificata di aggiornamenti automatici](/deployoffice/overview-of-the-update-process-for-office-365-proplus) creata all'installazione di Microsoft 365 Apps. In questo caso, questa attività deve essere eseguita almeno una volta per configurare il canale di aggiornamento e rilevare gli aggiornamenti.
>
> Se Microsoft 365 Apps è stato installato di recente e gli aggiornamenti distribuiti non vengono rilevati, per scopi di test, è possibile avviare manualmente l'attività di aggiornamenti automatici di Office e quindi avviare il [ciclo di valutazione delle distribuzioni degli aggiornamenti software](../understand/software-updates-introduction.md#scan-for-software-updates-compliance-process) nel client. Per istruzioni su come eseguire questa operazione in una sequenza di attività, vedere [Aggiornamento di Microsoft 365 Apps in una sequenza di attività](manage-office-365-proplus-updates.md#bkmk_ts).

## <a name="restart-behavior-and-client-notifications-for-microsoft-365-apps-updates"></a>Comportamento di riavvio e notifiche client per gli aggiornamenti di Microsoft 365 Apps
Quando si distribuisce un aggiornamento a un client di Microsoft 365 Apps, il comportamento di riavvio e le notifiche client sono diversi a seconda della versione di Configuration Manager. La tabella seguente fornisce informazioni sull'esperienza dell'utente finale quando il client riceve un aggiornamento di Microsoft 365 Apps:

|Versione di Configuration Manager |Esperienza utente finale|  
|----------------|---------------------|
|1706, 1710|Il client riceve notifiche popup e in-app, nonché una finestra di dialogo con il conto alla rovescia prima dell'installazione dell'aggiornamento.|
|1802| Il client riceve notifiche popup e in-app, nonché una finestra di dialogo con il conto alla rovescia prima dell'installazione dell'aggiornamento. </br>Se Microsoft 365 Apps è in esecuzione durante l'applicazione di un aggiornamento del client, non verrà forzata la chiusura di Microsoft 365 Apps. Al contrario, l'installazione dell'aggiornamento restituisce una richiesta di riavvio del sistema <!--510006-->|


> [!Important]
>
>In Configuration Manager versione 1706 si noti quanto segue:
>
>- Viene visualizzata un'icona di notifica nell'area di notifica sulla barra delle applicazioni per le app obbligatorie la cui scadenza è entro 48 ore e per cui il contenuto dell'aggiornamento è stato scaricato. 
>- Viene visualizzata una finestra di dialogo con un conto alla rovescia per le app obbligatorie la cui scadenza è entro 7,5 ore e per cui l'aggiornamento è stato scaricato. L'utente può posticipare la finestra di dialogo del conto alla rovescia fino a tre volte prima della scadenza. Se viene posticipato, il conto alla rovescia viene visualizzato di nuovo dopo due ore. Se non viene posticipato, viene eseguito un conto alla rovescia di 30 minuti e, al termine, l'aggiornamento viene installato.
>- Potrebbe non venire visualizzata una notifica popup fino a quando l'utente non fa clic sull'icona nell'area di notifica. Inoltre, se nell'area di notifica c'è poco spazio, l'icona di notifica potrebbe non essere visibile a meno che l'utente non apra o espanda l'area. 
>- La finestra di dialogo di notifica e conto alla rovescia può essere avviata mentre l'utente non usa attivamente il dispositivo. Ad esempio, quando il dispositivo è bloccato durante la notte è possibile che l'esecuzione di Microsoft 365 Apps nel dispositivo venga chiusa per installare l'aggiornamento. Prima di chiudere l'app, Office salva i relativi dati per evitarne la perdita. 
>- Se la scadenza è passata o se l'impostazione prevede l'avvio il prima possibile, la chiusura di Microsoft 365 Apps potrebbe essere forzata senza alcuna notifica. 
>- Se l'utente installa un aggiornamento di Microsoft 365 Apps prima della scadenza, quando viene raggiunta la scadenza Configuration Manager verifica che l'aggiornamento sia installato. Se l'aggiornamento non viene rilevato nel dispositivo, viene installato. 
>- La barra di notifica in-app non viene visualizzata in un'app che è in esecuzione prima del download dell'aggiornamento. Dopo il download dell'aggiornamento, la notifica in-app viene visualizzata solo per le app aperte successivamente.
>- Per gli aggiornamenti di Microsoft 365 Apps attivati da un intervallo di servizio o pianificati per l'orario non di ufficio, è possibile che venga forzata la chiusura delle app di Office in esecuzione senza alcuna notifica. 
>- Per altre informazioni, vedere [Notifiche di aggiornamento di Microsoft 365 Apps per gli utenti finali](/deployoffice/end-user-update-notifications-microsoft-365-apps).


## <a name="add-languages-for-microsoft-365-apps-update-downloads"></a><a name="bkmk_o365_lang"></a> Aggiungere lingue per i download degli aggiornamenti di Microsoft 365 Apps
È possibile aggiungere il supporto per Configuration Manager per scaricare gli aggiornamenti in tutte le lingue supportate da Microsoft 365 Apps.

### <a name="download-updates-for-additional-languages-in-version-1902"></a>Scaricare gli aggiornamenti per altre lingue nella versione 1902
<!--3555955-->

A partire da Configuration Manager versione 1902, il flusso di lavoro di aggiornamento fa distinzione tra le 38 lingue per **Windows Update** e le numerose lingue aggiuntive per l'**aggiornamento del client di Office 365**.

Per selezionare le lingue necessarie usare la pagina **Selezione lingua** nelle seguenti posizioni:
- Creazione guidata delle regole di distribuzione automatica
- Distribuzione guidata degli aggiornamenti software
- Download guidato degli aggiornamenti software
- Proprietà Regola di distribuzione automatica

Nella pagina **Selezione lingua** selezionare **Aggiornamenti del client Office 365** e quindi fare clic su **Modifica**. Aggiungere le lingue necessarie per Microsoft 365 Apps e quindi fare clic su **OK**.

![Screenshot dell'aggiunta di altre lingue per Microsoft 365 Apps](media/office-update-languages-selection.png)

### <a name="to-add-support-to-download-updates-for-additional-languages-in-version-1810-and-earlier"></a>Per aggiungere il supporto per il download degli aggiornamenti in altre lingue nella versione 1810 e precedenti

Seguire questa procedura per il punto di aggiornamento software presso il sito di amministrazione centrale o presso il sito primario autonomo.

> [!IMPORTANT]  
> La configurazione di lingue aggiuntive per l'aggiornamento di Microsoft 365 Apps è un'impostazione a livello di sito. Dopo l'aggiunta delle lingue in base alla procedura seguente, tutti gli aggiornamenti di Microsoft 365 Apps vengono scaricati in queste lingue, oltre che nelle lingue selezionate nella pagina **Selezione lingua** del Download guidato degli aggiornamenti software o della Distribuzione guidata degli aggiornamenti software.

1. Da un prompt dei comandi digitare *wbemtest* come utente amministratore per aprire il Tester di Strumentazione gestione Windows.
2. Fare clic su **Connetti** e quindi digitare *root\sms\site_&lt;CodiceSito&gt;* .
3. Fare clic su **Query** e quindi eseguire la query seguente: *select &#42; from SMS_SCI_Component where componentname ="SMS_WSUS_CONFIGURATION_MANAGER"*  
   ![query WMI](../media/1-wmiquery.png)
4. Nel riquadro dei risultati fare doppio clic sull'oggetto con il codice corrispondente al sito di amministrazione centrale o al sito primario autonomo.
5. Selezionare la proprietà **Props**, fare clic su **Modifica proprietà** e quindi su **Visualizza ogg. incorporati**.
   ![Editor di proprietà](../media/2-propeditor.png)
6. A partire dal primo risultato della query, aprire tutti gli oggetti fino a individuare quello con **AdditionalUpdateLanguagesForO365** per la proprietà **PropertyName**.
7. Selezionare **Value2** e fare clic su **Modifica proprietà**.  
   ![Modificare la proprietà Value2](../media/3-queryresult.png)
8. Aggiungere altre lingue alla proprietà **Value2** e fare clic su **Salva proprietà**. <br/> Ad esempio, pt-pt (per Portoghese - Portogallo), af-za (per Afrikaans - Sudafrica), nn-no (per Norvegese Nynorsk - Norvegia) e così via. Nell'esempio vengono immesse le lingue `pt-pt,af-za,nn-no`. Non usare spazi tra le lingue.
 
   ![Aggiungere lingue nell'Editor di proprietà](../media/4-props.png)  
9. Fare clic su **Chiudi**, **Chiudi**, **Salva proprietà** e **Salva oggetto** (se si fa clic su **Chiudi**, i valori vengono ignorati). Fare clic su **Chiudi** e quindi su **Esci** per chiudere il tester di Strumentazione gestione Windows.
10. Nella console di Configuration Manager passare a **Raccolta software** > **Panoramica** > **Office 365 Client Management (Gestione client di Office 365)**  > **Office 365 Updates (Aggiornamenti di Office 365)** .
11. Ora gli aggiornamenti di Microsoft 365 Apps vengono scaricati nelle lingue selezionate nella procedura guidata e configurati in questa procedura. Per verificare che gli aggiornamenti vengano effettivamente scaricati nelle lingue corrette, passare all'origine pacchetto per gli aggiornamenti e cercare i file con il codice lingua nel nome.  
    ![Nomi di file con altre lingue](../media/5-verification.png)

## <a name="updating-microsoft-365-apps-in-a-task-sequence"></a><a name="bkmk_ts"></a> Aggiornamento di Microsoft 365 Apps in una sequenza di attività
Quando si usa il passaggio della sequenza di attività [Installa aggiornamenti software](../../osd/understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates) per installare gli aggiornamenti di Microsoft 365 Apps, è possibile che gli aggiornamenti distribuiti vengano rilevati come non applicabili.  Questa situazione può verificarsi se l'attività pianificata di aggiornamenti automatici di Office non è stata eseguita almeno una volta. Vedere la nota in [Distribuire gli aggiornamenti di Microsoft 365 Apps](manage-office-365-proplus-updates.md#bkmk_update). Questa situazione potrebbe verificarsi, ad esempio, se Microsoft 365 Apps è stato installato subito prima di eseguire questo passaggio.

Per assicurarsi che il canale di aggiornamento sia impostato in modo da consentire il rilevamento corretto degli aggiornamenti distribuiti, usare uno dei metodi seguenti:

**Metodo 1**:
1. In un computer con la stessa versione di Microsoft 365 Apps aprire l'Utilità di pianificazione (taskschd.msc) e individuare l'attività degli aggiornamenti automatici di Microsoft 365 Apps. Questa attività si trova in genere in **Libreria Utilità di pianificazione** >**Microsoft**>**Office**.
2. Fare clic con il pulsante destro del mouse sull'attività e selezionare **Proprietà**.
3. Passare alla scheda **Azioni** e fare clic su **Modifica**. Copiare il comando e gli eventuali argomenti. 
4. Nella console di Configuration Manager modificare la sequenza di attività.
5. Aggiungere un nuovo passaggio **Esegui riga di comando** prima del passaggio **Installa aggiornamenti software** nella sequenza di attività. Se Microsoft 365 Apps viene installato come parte della sequenza di attività stessa, assicurarsi che questo passaggio venga eseguito dopo l'installazione di Office.
6. Inserire il comando e gli argomenti raccolti dall'attività pianificata degli aggiornamenti automatici di Office. 
7. Fare clic su **OK**. 

**Metodo 2**:
1. In un computer con la stessa versione di Microsoft 365 Apps aprire l'Utilità di pianificazione (taskschd.msc) e individuare l'attività degli aggiornamenti automatici di Microsoft 365 Apps. Questa attività si trova in genere in **Libreria Utilità di pianificazione** >**Microsoft**>**Office**.
2. Nella console di Configuration Manager modificare la sequenza di attività.
3. Aggiungere un nuovo passaggio **Esegui riga di comando** prima del passaggio **Installa aggiornamenti software** nella sequenza di attività. Se Microsoft 365 Apps viene installato come parte della sequenza di attività stessa, assicurarsi che questo passaggio venga eseguito dopo l'installazione di Office.
4. Nel campo della riga di comando immettere la riga di comando per l'esecuzione dell'attività pianificata. Vedere l'esempio seguente assicurandosi che la stringa tra virgolette corrisponda al percorso e al nome dell'attività identificati nel passaggio 1.  

    Esempio: `schtasks /run /tn "\Microsoft\Office\Office Automatic Updates 2.0"`
5. Fare clic su **OK**. 

## <a name="update-channels-for-microsoft-365-apps"></a><a name="bkmk_channel"></a> Aggiornare i canali per le app Microsoft 365
<!--6298093-->
Quando Office 365 ProPlus è stato rinominato **Microsoft 365 Apps for enterprise**, sono stati rinominati anche i canali di aggiornamento. Se si usa una regola di distribuzione automatica per distribuire gli aggiornamenti, sarà necessario apportarvi delle modifiche se si basa sulla proprietà **Title**. Questo perché il nome dei pacchetti di aggiornamento nel Microsoft Update Catalog sta cambiando.

Attualmente, il titolo di un pacchetto di aggiornamento per Office 365 ProPlus inizia con "Office 365 Client Update", come illustrato nell'esempio seguente:

&nbsp; &nbsp; Office 365 Client Update - Semi-annual Channel Version 1908 for x64 based Edition (Build 11929.20648)

Per i pacchetti di aggiornamento rilasciati a partire dal 9 giugno incluso, il titolo inizierà con "Microsoft 365 Apps Update", come illustrato nell'esempio seguente:

&nbsp; &nbsp; Microsoft 365 Apps Update - Semi-annual Channel Version 1908 for x64 based Edition (Build 11929.50000)
</br>
</br>

|Nuovo nome canale|Nome canale precedente|
|--|--|
|Canale Enterprise semestrale|Canale semestrale|
|Canale Enterprise semestrale (Anteprima)|Canale semestrale (mirato)|
|Canale Enterprise mensile|N/D|
|Canale corrente|Canale mensile|
|Canale corrente (Anteprima)|Canale mensile (mirato)|
|Canale beta|Insider|

Per altre informazioni su come modificare le regole di distribuzione automatica, vedere [Distribuire automaticamente gli aggiornamenti software](automatically-deploy-software-updates.md). Per altre informazioni sulla modifica dei nomi, vedere [Modifica dei nomi di Office 365 ProPlus](/deployoffice/name-change).


## <a name="change-the-update-channel-after-you-enable-microsoft-365-apps-clients-to-receive-updates-from-configuration-manager"></a>Modificare il canale di aggiornamento dopo aver abilitato i client di Microsoft 365 Apps alla ricezione degli aggiornamenti da Configuration Manager

Dopo la distribuzione di Microsoft 365 Apps, è possibile cambiare il canale di aggiornamento con Criteri di gruppo o lo Strumento di distribuzione di Office (ODT). Ad esempio, è possibile spostare un dispositivo da Canale semestrale a Canale semestrale (mirato). Quando si cambia il canale, Office viene aggiornato automaticamente senza dover reinstallare o scaricare la versione completa. Per altre informazioni, vedere [Cambiare il canale di aggiornamento per Microsoft 365 Apps per i dispositivi nell'organizzazione](https://docs.microsoft.com/deployoffice/change-update-channels).

## <a name="next-steps"></a>Passaggi successivi

Usare il dashboard di Gestione client di Microsoft 365 Apps in Configuration Manager per esaminare le informazioni sul client di Microsoft 365 Apps e distribuire Microsoft 365 Apps. Per altre informazioni, vedere [Dashboard di Gestione client di Office 365](office-365-dashboard.md).