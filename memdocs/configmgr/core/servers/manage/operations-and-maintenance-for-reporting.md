---
title: Operazioni e manutenzione per la creazione di report
titleSuffix: Configuration Manager
description: Informazioni dettagliate sulla gestione di report e sottoscrizioni report in Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b89bcfbf-f5b6-4fb1-bb5e-a5cc18ec0c78
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 414d1138a7682d6b9acbc7731035fff1842a1fe7
ms.sourcegitcommit: c1afc8abd0d7da48815bd2b0e45147774c72c2df
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/05/2020
ms.locfileid: "87815413"
---
# <a name="operations-and-maintenance-for-reporting-in-configuration-manager"></a>Operazioni e manutenzione per la creazione di report in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Dopo aver definito l'infrastruttura per la creazione di report in Configuration Manager, è in genere necessario eseguire alcune operazioni per la gestione di report e di sottoscrizioni report.

> [!NOTE]
> Questo articolo è incentrato sui report in SQL Server Reporting Services. A partire dalla versione 2002, è possibile integrare la creazione di report con il server di report di Power BI. Per altre informazioni, vedere [Integrare il server di report di Power BI](powerbi-report-server.md).

## <a name="run-a-report-from-reporting-services"></a>Eseguire un report da Reporting Services

Configuration Manager archivia i report in SQL Server Reporting Services. I report recuperano i dati dal database del sito di Configuration Manager. È possibile accedere ai report nella console di Configuration Manager oppure usando Gestione report, accessibile tramite Web browser. Aprire i report da un Web browser in qualsiasi computer in grado di accedere al punto di Reporting Services, con un utente dotato di diritti sufficienti per la visualizzazione dei report. Per eseguire i report sono necessari diritti di **Lettura** per l'autorizzazione **Sito** e l'autorizzazione **Esegui report** per oggetti specifici.

Quando si esegue un report, il titolo, la descrizione e la categoria del report vengono visualizzati nella lingua del sistema operativo locale. Per altre informazioni, vedere [Lingue per i report](configuring-reporting.md#-languages-for-reports).

> [!NOTE]  
> Gestione report è uno strumento di gestione e accesso ai report basato sul Web. È possibile usarlo per amministrare una singola istanza del server di report tramite una connessione HTTPS. Usare Gestione report per attività operative, ad esempio per visualizzare i report, modificarne proprietà e gestire le sottoscrizioni di report associate. Questo articolo illustra la procedura per visualizzare un report e modificare le proprietà di un report in Gestione report. Per informazioni sulle altre opzioni di Gestione report, vedere [Che cos'è Gestione report?](https://docs.microsoft.com/sql/reporting-services/report-server/manage-a-reporting-services-native-mode-report-server)

Utilizzare le procedure seguenti per eseguire un report di Configuration Manager.

### <a name="run-a-report-in-the-configuration-manager-console"></a>Eseguire un report nella console di Configuration Manager

1. Nella console di Configuration Manager passare all'area di lavoro **Monitoraggio**. Espandere **Creazione report** e selezionare **Report**. Questo nodo elenca i report disponibili.

    > [!TIP]
    > Se nel nodo non sono elencati report, verificare che il punto di Reporting Services sia installato e configurato. Per altre informazioni, vedere [Configurare la creazione di report in Reporting Manager](configuring-reporting.md).

1. Selezionare il report che si vuole eseguire. Nella scheda **Home** sulla barra multifunzione, nella sezione **Gruppo Report** selezionare **Esegui** per aprire il report.

1. Se sono previsti parametri obbligatori, specificarli e quindi selezionare **Visualizza report**.

### <a name="run-a-report-in-a-web-browser"></a>Eseguire un report in un Web browser

1. Nel Web browser passare all'URL di Gestione report, ad esempio `https://Server1/Reports`. È possibile trovare questo indirizzo nella pagina **URL Gestione report** in Gestione configurazione Reporting Services.

1. In Gestione report selezionare la cartella dei report per Configuration Manager, ad esempio **ConfigMgr_CAS**.

    > [!TIP]
    > Se in Gestione report non sono elencati report, verificare che il punto di Reporting Services sia installato e configurato. Per altre informazioni, vedere [Configurare la creazione di report in Reporting Manager](configuring-reporting.md).

1. Selezionare la categoria per il report che si vuole eseguire e quindi selezionare lo specifico report. Il report verrà aperto in Gestione Report.

1. Se sono previsti parametri obbligatori, specificarli e quindi selezionare **Visualizza report**.

## <a name="modify-the-properties-of-a-report"></a>Modificare le proprietà di un report

Le proprietà del report includono il nome e la descrizione del report. È possibile visualizzare le proprietà di un report nella console di Configuration Manager.

Per modificare le proprietà, usare Gestione report:

1. Nel Web browser passare all'URL di Gestione report, ad esempio `https://Server1/Reports`.

1. In Gestione report selezionare la cartella dei report per Configuration Manager, ad esempio **ConfigMgr_CAS**.

1. Selezionare la categoria di report, quindi selezionare il report specifico. Il report verrà aperto in Gestione Report.

1. Selezionare la scheda **Proprietà**. Modificare il nome e la descrizione del report e quindi selezionare **Applica**.

Gestione report salva le proprietà del report nel server di report. Nella console di Configuration Manager vengono visualizzate le proprietà aggiornate per il report.

## <a name="edit-a-report"></a><a name="bkmk_edit"></a> Modificare un report

Quando un report di Configuration Manager esistente non recupera le informazioni desiderate, modificarlo in Generatore report. Si può usare Generatore report anche per modificare il layout o la progettazione del report. Sebbene sia possibile modificare direttamente un report predefinito, è preferibile clonarlo. Aprire il report da modificare e quindi selezionare **Salva con nome**.

Per modificare un report sono necessarie le autorizzazioni di**Modifica del sito** e **Modifica report** per gli specifici oggetti del report.

> [!IMPORTANT]
> Gli aggiornamenti del sito non incidono sui report predefiniti. Se si modifica un report standard, quando il sito viene aggiornato, il report viene rinominato con un prefisso di sottolineatura (`_`). Questo comportamento assicura che l'aggiornamento del sito non sovrascriva il report modificato dal report standard.
>
> Se si modificano i report predefiniti, prima di installare un aggiornamento del sito, eseguire il backup dei report personalizzati. Dopo l'aggiornamento, ripristinare il report in Reporting Services. Anziché apportare modifiche significative a un report predefinito, è preferibile creare un nuovo report. I nuovi report creati prima dell'aggiornamento di un sito non verranno sovrascritti.

Seguire la procedura seguente per modificare le proprietà di un report di Configuration Manager.

1. Nella console di Configuration Manager passare all'area di lavoro **Monitoraggio**. Espandere **Creazione report** e selezionare il nodo **Report**.

1. Selezionare il report che si vuole modificare. Nella scheda **Home** sulla barra multifunzione, nella sezione **Gruppo Report** selezionare **Modifica**. Potrebbe essere richiesto di immettere le credenziali. Se Generatore report non è installato nel computer, Configuration Manager richiede di installarlo. Generatore report è necessario per la modifica e la creazione di report.

1. Modificare le impostazioni di report appropriate in Generatore report. Fare clic su **Salva** per salvare il report nel server di report.

## <a name="create-reports"></a>Creare report

Si possono creare due tipi di report:

- Un **report basato su modello** consente di selezionare in modo interattivo gli elementi da includere. Per altre informazioni sulla creazione di modelli di report personalizzati, vedere [Creazione di modelli di report personalizzati per Configuration Manager in SQL Server Reporting Services](creating-custom-report-models-in-sql-server-reporting-services.md).

- Un **report basato su SQL** consente di recuperare i dati che si basano su un'istruzione SQL del report.

> [!IMPORTANT]
> Per creare un nuovo report, l'account deve disporre di autorizzazioni di **modifica del sito**. Si può creare un report solo nelle cartelle per cui si hanno autorizzazioni di tipo **Modifica report**.

### <a name="create-a-model-based-report"></a>Creare un report basato su modello

Seguire questa procedura per creare un report di Configuration Manager basato su modello.

1. Nella console di Configuration Manager passare all'area di lavoro **Monitoraggio**, espandere **Report** e selezionare il nodo **Report**.

1. Nella scheda **Home** della barra multifunzione selezionare **Crea report** nella sezione **Crea**. Si aprirà la **Creazione guidata report**.

1. Nella pagina **Informazioni** è possibile configurare le impostazioni seguenti:

    - **Tipo**: selezionare **Report basato su modello**.

    - **Nome**: specificare un nome per il report.

    - **Descrizione**: specificare una descrizione per il report.

    - **Server**: visualizza il nome del server di report in cui si sta creando il report.

    - **Percorso**: selezionare **Sfoglia** per specificare una cartella in cui archiviare il report.

1. Nella pagina **Selezione modello** selezionare un modello disponibile dall'elenco per creare questo report. La sezione **Anteprima** mostra le entità e le viste di SQL Server disponibili in questo modello di report.

1. Completare la Creazione guidata report.

1. Aprire Generatore report per configurare le impostazioni del report. Per altre informazioni, vedere [Modificare un report di Configuration Manager](#bkmk_edit).

1. In Generatore Report creare il layout del report, selezionare i dati nelle viste di SQL Server disponibili e aggiungere parametri al report.

1. Fare clic su **Esegui** per eseguire il report. Verificare che il report fornisca le informazioni previste. Se necessario, selezionare **Progettazione** per modificare ulteriormente il report.

1. Fare clic su **Salva** per salvare il report nel server di report.

### <a name="create-a-sql-based-report"></a>Creare un report basato su SQL

Quando si crea un'istruzione SQL per un report personalizzato, non fare riferimento direttamente alle tabelle di SQL Server. Fare sempre riferimento alle viste di SQL Server per la creazione di report supportate nel database del sito. Queste viste hanno nomi che iniziano con `v_`. Per altre informazioni, vedere [Creazione di report personalizzati usando viste di SQL Server in Configuration Manager](../../../develop/core/understand/sqlviews/create-custom-reports-using-sql-server-views.md).

È anche possibile fare riferimento a stored procedure pubbliche dal database del sito. Queste stored procedure hanno nomi che iniziano con `sp_`.

Seguire questa procedura per creare un report di Configuration Manager basato su SQL.

1. Nella console di Configuration Manager passare all'area di lavoro **Monitoraggio**, espandere **Report** e selezionare il nodo **Report**.

1. Nella scheda **Home** della barra multifunzione selezionare **Crea report** nella sezione **Crea**. Si aprirà la **Creazione guidata report**.

1. Nella pagina **Informazioni** è possibile configurare le impostazioni seguenti:

    - **Tipo**: Selezionare **Report basato su SQL**.

    - **Nome**: specificare un nome per il report.

    - **Descrizione**: specificare una descrizione per il report.

    - **Server**: visualizza il nome del server di report in cui si sta creando il report.

    - **Percorso**: selezionare **Sfoglia** per specificare una cartella in cui archiviare il report.

1. Completare la Creazione guidata report.

1. Aprire Generatore report per configurare le impostazioni del report. Per altre informazioni, vedere [Modificare un report di Configuration Manager](#bkmk_edit).

1. In Generatore report specificare l'istruzione SQL per il report. Si può creare l'istruzione SQL anche usando le colonne presenti nelle viste disponibili. Se necessario, aggiungere parametri al report.

1. Fare clic su **Esegui** per eseguire il report. Verificare che il report fornisca le informazioni previste. Se necessario, selezionare **Progettazione** per modificare ulteriormente il report.

1. Fare clic su **Salva** per salvare il report nel server di report.

## <a name="manage-report-subscriptions"></a><a name="bkmk_subscription"></a> Gestire le sottoscrizioni report

Le sottoscrizioni report in SQL Server Reporting Services consentono di configurare l'individuazione automatica dei report specificati tramite posta elettronica o in una condivisione file a intervalli pianificati. Usare la **Creazione guidata sottoscrizione** in Configuration Manager per configurare le sottoscrizioni report.

### <a name="create-a-report-subscription-to-deliver-a-report-to-a-file-share"></a>Creare una sottoscrizione report per il recapito di un report in una condivisione file

Quando si crea una sottoscrizione report per il recapito di un report in una condivisione file, Reporting Services copia il report nel formato specificato nella condivisione file specificata. È possibile effettuare la sottoscrizione e richiedere il recapito per un solo report alla volta.

Quando si crea una sottoscrizione che usa una condivisione file, specificare una cartella esistente come destinazione. Il server di report non crea la cartella o la condivisione di rete. Quando si specifica la cartella di destinazione in una sottoscrizione, usare un percorso UNC e non includere barre rovesciate finali (`\`) nel percorso della cartella. Ecco un esempio di percorso UNC valido per la cartella di destinazione: `\\server\reportfiles\operations\2001`.

> [!NOTE]
> Quando si crea la sottoscrizione, è necessario specificare un nome utente e una password. Questo account deve avere accesso alla condivisione con autorizzazioni di **Scrittura** per la cartella di destinazione.

Reporting Services può eseguire il rendering dei report in più formati di file. Ad esempio, MHTML o Excel. È possibile selezionare il formato quando si crea la sottoscrizione. Sebbene sia possibile selezionare qualsiasi formato di rendering supportato, alcuni formati funzionano meglio di altri durante il rendering in un file.

### <a name="limitations-for-report-subscriptions-to-a-file-share"></a>Limitazioni per le sottoscrizioni report con recapito a una condivisione file

Di seguito sono elencate le limitazioni delle sottoscrizioni report con recapito a una condivisione file:

- A differenza dei report ospitati e gestiti in un server di report, Reporting Services recapita i report in una cartella condivisa sotto forma di file statici.

- Le funzionalità interattive del report non funzionano per i report archiviati come file. Il report rappresenta le eventuali funzionalità interattive come elementi statici.

- Se il report include grafici, usa la presentazione predefinita.

- Se il report contiene un collegamento a un altro report, esegue il rendering del collegamento come testo statico.

Se si vogliono conservare le funzionalità interattive in un report recapitato, usare il recapito tramite posta elettronica. Per altre informazioni, vedere [Creare una sottoscrizione report per il recapito di un report tramite posta elettronica](#bkmk_subscription-email).

### <a name="process-to-create-a-report-subscription-for-a-file-share"></a>Processo per la creazione di una sottoscrizione report per una condivisione file

Utilizzare la procedura seguente per creare una sottoscrizione report per il recapito di un report in una condivisione file.  

1. Nella console di Configuration Manager passare all'area di lavoro **Monitoraggio**, espandere **Report** e selezionare il nodo **Report**.

1. Selezionare una cartella di report, quindi selezionare il report che si vuole sottoscrivere. Nella scheda **Home** sulla barra multifunzione, nella sezione **Gruppo Report** selezionare **Crea sottoscrizione**. Si aprirà la **Creazione guidata sottoscrizione**.

1. Nella pagina **Recapito sottoscrizione** è possibile configurare le impostazioni seguenti:  

    - **Report recapitato da**: selezionare **Condivisione file di Windows**.

    - **Nome file**: specificare il nome del file per il report. Per impostazione predefinita, il file di report non include alcuna estensione di nome file. Selezionare **Aggiungi estensione file al momento della creazione** per aggiungere automaticamente un'estensione di nome file in base al formato.

    - **Percorso**: specificare un percorso UNC per una cartella esistente in cui recapitare il report. Ad esempio, `\\server\reportfiles\operations`

    - **Formato rendering**: selezionare uno dei formati seguenti per il file di report:

      - **File XML con dati report**
      - **CSV (delimitato da virgole)**
      - **File TIFF**
      - **File Acrobat (PDF)**
      - **HTML 4.0**
        > [!NOTE]
        > Se il report contiene immagini, il formato HTML 4.0 non le include.
      - **MHTML (archivio Web)**
      - **Renderer RPL** (Report Page Layout)
      - **Excel**
      - **Word**

    - **Nome utente**: Specificare un account utente di Windows con autorizzazioni di *scrittura* per il **Percorso specificato**.

    - **Password**: specificare la password per l'account utente di Windows indicato.

    - **Opzione di sovrascrittura**: Selezionare una delle seguenti opzioni per configurare il comportamento quando esiste un file con lo stesso nome nella cartella di destinazione:

      - **Sovrascrivi un file esistente con una versione più recente**
      - **Non sovrascrivere un file esistente**
      - **Incrementa i nomi di file quando vengono aggiunte versioni più recenti**: questa opzione consente di aggiungere un numero al nome file del nuovo report per distinguerlo dalle versioni precedenti.

    - **Descrizione**: facoltativamente, specificare ulteriori informazioni su questa sottoscrizione report.

1. Nella pagina **Pianificazione della sottoscrizione** selezionare una delle opzioni seguenti della pianificazione di recapito per la sottoscrizione report:

    - **Usa pianificazione condivisa**: una pianificazione condivisa è una pianificazione definita in precedenza che può essere usata da altre sottoscrizioni report. Quando si seleziona questa opzione, selezionare anche una pianificazione condivisa. Se non esistono pianificazioni condivise, selezionare l'opzione per creare una nuova pianificazione.

    - **Crea nuova pianificazione**: configurare la pianificazione in base a cui viene eseguito il report. La pianificazione include intervallo, ora e data di inizio e data di fine per la sottoscrizione. Per impostazione predefinita, una nuova sottoscrizione crea una nuova pianificazione che prevede l'esecuzione ogni ora a partire dalla data e dall'ora correnti.

1. Nella pagina **Parametri sottoscrizione** specificare i parametri necessari per l'esecuzione automatica di questo report. Se il report non ha parametri, la pagina non verrà visualizzata.

1. Completare la procedura guidata.

1. Verificare che Configuration Manager abbia creato correttamente la sottoscrizione report. Selezionare il nodo **Sottoscrizioni** per visualizzare e modificare le sottoscrizioni report.

### <a name="create-a-report-subscription-to-deliver-a-report-by-email"></a><a name="bkmk_subscription-email"></a> Creare una sottoscrizione report per recapitare un report tramite posta elettronica

Quando si crea una sottoscrizione report per il recapito di un report tramite posta elettronica, Reporting Services invia un messaggio di posta elettronica ai destinatari configurati. Il messaggio include il report come allegato. Il server di report non convalida gli indirizzi di posta elettronica né li ottiene da un server di posta elettronica. È possibile inviare tramite posta elettronica i report a qualsiasi account di posta elettronica valido interno o esterno all'organizzazione.

> [!NOTE]
> Per abilitare l'opzione di sottoscrizione **Posta elettronica** è necessario configurare le impostazioni di posta elettronica in Reporting Services. Per altre informazioni, vedere [Recapito tramite posta elettronica in Reporting Services](https://docs.microsoft.com/sql/reporting-services/subscriptions/e-mail-delivery-in-reporting-services).

È possibile selezionare una o entrambe le seguenti opzioni di recapito tramite posta elettronica:

- Inviare una notifica con un collegamento al report generato.

- Inviare un report collegato o incorporato. Il formato di rendering e il browser determinano se il report è incorporato o collegato.

  - Se il browser supporta HTML 4.0 e MHTML e si seleziona il formato di rendering **MHTML (archivio Web)** , il report verrà incorporato nel messaggio di posta elettronica.
  - Tutti gli altri formati prevedono il recapitano dei report come allegati.
  - Reporting Services non controlla la dimensione dell'allegato o del messaggio prima di inviare il report. Se l'allegato o messaggio supera il limite massimo consentito dal server di posta elettronica, il report non verrà recapitato.

Utilizzare la procedura seguente per creare una sottoscrizione report per recapitare un report tramite posta elettronica.  

1. Nella console di Configuration Manager passare all'area di lavoro **Monitoraggio**, espandere **Report** e selezionare il nodo **Report**.

1. Selezionare una cartella di report, quindi selezionare il report che si vuole sottoscrivere. Nella scheda **Home** sulla barra multifunzione, nella sezione **Gruppo Report** selezionare **Crea sottoscrizione**. Si aprirà la **Creazione guidata sottoscrizione**.

1. Nella pagina **Recapito sottoscrizione** è possibile configurare le impostazioni seguenti:  

    - **Report recapitato da**: selezionare **Posta elettronica**.

    - **A**: specificare un indirizzo di posta elettronica valido come destinatario.

        > [!NOTE]
        > Per immettere più destinatari, separare ogni indirizzo di posta elettronica con un punto e virgola (`;`).

    - **Cc**: facoltativamente, specificare un indirizzo di posta elettronica a cui inviare una copia di questo report.

    - **Ccn**: facoltativamente, specificare un indirizzo di posta elettronica a cui inviare una copia nascosta di questo report.

    - **Rispondi a**: specificare l'indirizzo di risposta. Se il destinatario risponde al messaggio di posta elettronica, la risposta verrà inviata a questo indirizzo.

    - **Oggetto**: specificare un oggetto per il messaggio di posta elettronica di sottoscrizione.

    - **Priorità**: selezionare il flag di priorità per il messaggio di posta elettronica, **Bassa**, **Normale** o **Alta**. Microsoft Exchange usa questo flag per indicare l'importanza del messaggio di posta elettronica.

    - **Commento**: specificare il testo del corpo del messaggio di posta elettronica di sottoscrizione.

    - **Descrizione**: facoltativamente, specificare ulteriori informazioni su questa sottoscrizione report.

    - **Includi collegamento**: includere l'URL del report nel corpo del messaggio di posta elettronica.

    - **Includi report**: allegare il report al messaggio di posta elettronica. Usare l'opzione **Formato rendering** per specificare il formato del report da allegare.

    - **Formato rendering**: selezionare uno dei formati seguenti per il file di report allegato:

      - **File XML con dati report**
      - **CSV (delimitato da virgole)**
      - **File TIFF**
      - **File Acrobat (PDF)**
      - **MHTML (archivio Web)**
      - **Excel**
      - **Word**

1. Nella pagina **Pianificazione della sottoscrizione** selezionare una delle opzioni seguenti della pianificazione di recapito per la sottoscrizione report:

    - **Usa pianificazione condivisa**: una pianificazione condivisa è una pianificazione definita in precedenza che può essere usata da altre sottoscrizioni report. Quando si seleziona questa opzione, selezionare anche una pianificazione condivisa. Se non esistono pianificazioni condivise, selezionare l'opzione per creare una nuova pianificazione.

    - **Crea nuova pianificazione**: configurare la pianificazione in base a cui viene eseguito il report. La pianificazione include intervallo, ora e data di inizio e data di fine per la sottoscrizione. Per impostazione predefinita, una nuova sottoscrizione crea una nuova pianificazione che prevede l'esecuzione ogni ora a partire dalla data e dall'ora correnti.

1. Nella pagina **Parametri sottoscrizione** specificare i parametri necessari per l'esecuzione automatica di questo report. Se il report non ha parametri, la pagina non verrà visualizzata.

1. Completare la procedura guidata.

1. Verificare che Configuration Manager abbia creato correttamente la sottoscrizione report. Selezionare il nodo **Sottoscrizioni** per visualizzare e modificare le sottoscrizioni report.
