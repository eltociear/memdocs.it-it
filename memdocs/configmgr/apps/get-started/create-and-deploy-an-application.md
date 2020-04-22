---
title: Creare e distribuire un'applicazione
titleSuffix: Configuration Manager
description: Creare e distribuire un'applicazione contenente un'app line-of-business e informazioni su come gestire le applicazioni in modo efficace.
ms.date: 07/19/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 3bd1e487-ea18-43c1-b7c3-acbd9b86d429
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: b2d2a3465aebf66db37722629991078093abaaa7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689859"
---
# <a name="create-and-deploy-an-application-with-configuration-manager"></a>Creare e distribuire un'applicazione con Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Questo argomento include informazioni che consentono di creare subito un'applicazione con Configuration Manager. In questo esempio viene creata e distribuita un'applicazione contenente una riga per un'app aziendale per PC Windows denominata **Contoso.msi** che deve essere installata in tutti i PC che eseguono Windows 10 all'interno dell'azienda. Durante questo processo verranno fornite informazioni su gran parte delle operazioni che è possibile eseguire per gestire le applicazioni in modo efficace.  

 Questa procedura è progettata per offrire una panoramica su come creare e distribuire le applicazioni di Configuration Manager. Tuttavia, non copre tutte le opzioni di configurazione e non fornisce tutte le informazioni su come creare e distribuire applicazioni per altre piattaforme.  

 Per informazioni specifiche su ogni piattaforma, vedere uno degli argomenti seguenti:  

- [Creare applicazioni Windows](creating-windows-applications.md)
- [Creazione di applicazioni Windows Phone](../../mdm/deploy-use/management-tasks-applications.md#bkmk_winphone)
- [Creazione di applicazioni per computer Mac](creating-mac-computer-applications.md)
- [Creazione di applicazioni server Linux e UNIX](creating-linux-and-unix-server-applications.md)
- [Creazione di applicazioni Windows Embedded](creating-windows-embedded-applications.md)


Se si ha già familiarità con le applicazioni di Configuration Manager, è possibile ignorare questo argomento. Tuttavia, è consigliabile rivedere l'argomento [Create applications](../../apps/deploy-use/create-applications.md) (Creazione di applicazioni) per scoprire tutte le opzioni disponibili quando si creano e si distribuiscono le applicazioni.  

## <a name="before-you-start"></a>Prima di iniziare  

Assicurarsi di aver esaminato le informazioni contenute in [Introduzione alla gestione delle applicazioni](../understand/introduction-to-application-management.md) che indicano come preparare il sito per installare le applicazioni e di comprendere la terminologia usata in questo argomento.  

 Assicurarsi inoltre che i file di installazione per l'app **Contoso.msi** si trovino in un percorso accessibile sulla rete.  

## <a name="create-the-configuration-manager-application"></a>Creare l'applicazione di Configuration Manager  

### <a name="to-start-the-create-application-wizard-and-create-the-application"></a>Per avviare la Creazione guidata applicazione e creare l'applicazione  

1. Nella console di Configuration Manager scegliere **Raccolta software** > **Gestione applicazioni** > **Applicazioni**.  

2. Nella scheda **Home**, nel gruppo **Crea**, scegliere **Crea applicazione**.  

3. Nella pagina **Generale** della **Creazione guidata applicazione** selezionare **Rileva automaticamente le informazioni sull'applicazione dai file di installazione**. Alcune sezioni della procedura guidata vengono prepopolate con le informazioni estratte dal file di installazione con estensione msi. A questo punto, specificare le informazioni seguenti:  

   - **Tipo**: scegliere **Windows Installer (file \*.msi)** .  

   - **Percorso**: immettere il percorso del file di installazione **Contoso.msi** o fare clic su **Sfoglia** per selezionare il percorso. Per trovare i file di installazione con Configuration Manager, il percorso deve essere specificato nel formato *\\\Server\Share\File*.  

   Al termine, verrà visualizzata una schermata simile alla seguente:  

   ![Pagina generica di Gestione guidata applicazioni](media/App-management-wizard-general-page.png)  

4. Scegliere **Avanti**. Nella pagina **Importazione informazioni** verranno visualizzate alcune informazioni sull'app e tutti i file associati importati in Configuration Manager. Al termine, scegliere di nuovo **Avanti**.  

5. Nella pagina **Informazioni generali**, è possibile fornire altre informazioni sull'applicazione che consentono di ordinarla e individuarla nella console di Configuration Manager.  

    Inoltre, il campo **Programma di installazione** consente di specificare l'intera riga di comando usata per installare l'applicazione nei computer. È possibile modificare questa opzione per aggiungere proprietà personalizzate (ad esempio **/q** per un'installazione automatica).  

   > [!TIP]  
   > Alcuni dei campi in questa pagina della procedura guidata potrebbero essere stati compilati automaticamente durante l'importazione dei file di installazione dell'applicazione.  

    Al termine, verrà visualizzata una schermata simile alla seguente:  

    ![Pagina generica di informazioni di Gestione guidata applicazioni](media/App-management-wizard-general-information-page.png)  

6. Scegliere **Avanti**. Nella pagina di riepilogo è possibile confermare le impostazioni dell'applicazione e quindi completare la procedura guidata.  

   L'app viene creata. Per trovarla, espandere **Gestione applicazioni** nell'area di lavoro **Raccolta software** e quindi fare clic su **Applicazioni**. Per questo esempio verrà visualizzato:  

   ![Immagine finale dell'app](media/Final-app-graphic.png)  

## <a name="examine-the-properties-of-the-application-and-its-deployment-type"></a>Esaminare le proprietà dell'applicazione e il tipo di distribuzione  

Dopo aver creato un'applicazione, è possibile ridefinire le impostazioni dell'applicazione, se necessario. Per esaminare le proprietà dell'applicazione, selezionare l'app e quindi scegliere **Proprietà** nel gruppo **Proprietà** della scheda **Home**.  

 Nella finestra di dialogo **Proprietà applicazione \><Contoso** verranno visualizzati diversi elementi che è possibile configurare per perfezionare il comportamento dell'applicazione. Per informazioni dettagliate su tutte le impostazioni che è possibile configurare, vedere [Creazione di applicazioni](../../apps/deploy-use/create-applications.md). Ai fini di questo esempio, verranno modificate solo alcune delle proprietà del tipo di distribuzione dell'applicazione.  

 Fare clic sulla scheda **Tipi di distribuzione** > tipo di distribuzione **Applicazione Contoso** > **Modifica**.

Viene visualizzata una finestra di dialogo simile alla seguente:  

![Pagina delle proprietà dell'app di gestione](media/App-management-app-properties-page.png)  

## <a name="add-a-requirement-to-the-deployment-type"></a>Aggiungere un requisito al tipo di distribuzione

 I requisiti specificano le condizioni che devono essere soddisfatte prima di installare un'applicazione in un dispositivo.  È possibile scegliere tra i requisiti predefiniti o crearne di personalizzati. In questo esempio viene aggiunto un requisito che consente l'installazione dell'applicazione solo nei computer che eseguono Windows 10.  

1. Nella pagina delle proprietà del tipo di distribuzione appena aperta scegliere la scheda **Requisiti**.  

2. Scegliere **Aggiungi** per aprire la finestra di dialogo **Crea requisito**.  

3. Nella finestra di dialogo **Crea requisito** specificare le seguenti informazioni:  

    - **Categoria**: **Dispositivo**  

    - **Condizione**: **Sistema operativo**  

    - **Tipo di regola**: **Valore**  

    - **Operatore**: **Uno**  

    - Nell'elenco di sistemi operativi selezionare **Windows 10**.  

    Al termine, verrà visualizzata una finestra di dialogo simile alla seguente:  

    ![Pagina dei requisiti dell'app di gestione](media/App-management-requirements-page.png)  

4. Scegliere **OK** per chiudere le singole pagine delle proprietà aperte e quindi tornare all'elenco **Applicazioni** nella console di Configuration Manager.  

> [!TIP]  
> I requisiti consentono di ridurre il numero di raccolte di Configuration Manager necessario. Poiché è stato specificato che l'applicazione può essere installata solo nei computer che eseguono Windows 10, successivamente sarà possibile distribuirla in una raccolta contenente computer che eseguono sistemi operativi diversi. Tuttavia l'applicazione verrà installata solo nei PC con Windows 10.

## <a name="add-the-application-content-to-a-distribution-point"></a>Aggiungere il contenuto dell'applicazione a un punto di distribuzione  

Successivamente, per distribuire l'applicazione nei PC, è necessario assicurarsi che il contenuto dell'applicazione venga copiato in un punto di distribuzione. I PC accedono al punto di distribuzione per installare l'applicazione.  

> [!TIP]  
> Per altre informazioni sui punti di distribuzione e la gestione del contenuto in Configuration Manager, vedere [Gestire il contenuto e l'infrastruttura del contenuto](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).

1. Nella console di Configuration Manager scegliere **Raccolta software**.  

2. Nell'area di lavoro **Raccolta software** espandere **Applicazioni** e quindi selezionare dall'elenco di applicazioni l'**applicazione Contoso** creata.  

3. Nella scheda **Home**, nel gruppo **Distribuzione**, scegliere **Distribuisci contenuto**.  

4. Nella pagina **Generale** della **Distribuzione guidata contenuto** verificare che il nome dell'applicazione sia corretto e quindi scegliere **Avanti**.  

5. Nella pagina **Contenuto** esaminare le informazioni che verranno copiate nel punto di distribuzione e quindi scegliere **Avanti**.  

6. Nella pagina **Destinazione del contenuto** fare clic su **Aggiungi** per selezionare uno o più punti di distribuzione o gruppi di punti di distribuzione in cui installare il contenuto dell'applicazione.  

7. Completare la procedura guidata.  

È possibile verificare che il contenuto dell'applicazione sia stato copiato correttamente nel punto di distribuzione dall'area di lavoro **Monitoraggio** in **Stato di distribuzione** > **Stato contenuto**.  

## <a name="deploy-the-application"></a>Distribuire l'applicazione  

Successivamente, distribuire l'applicazione a una raccolta di dispositivi nella gerarchia. In questo esempio l'applicazione viene distribuita alla raccolta dispositivi **Tutti i sistemi**.  

> [!TIP]  
> Tenere presente che l'applicazione verrà installata solo nei computer Windows 10 a causa dei requisiti selezionati in precedenza.

1. Nella console di Configuration Manager scegliere **Raccolta software** > **Gestione applicazioni** > **Applicazioni**.  

2. Dall'elenco delle applicazioni selezionare l'applicazione creata in precedenza (**Applicazione Contoso**) e quindi scegliere **Distribuisci** nel gruppo **Distribuzione** della scheda **Home**.  

3. Nella pagina **Generale** della **Distribuzione guidata del software** fare clic su **Sfoglia** per selezionare la raccolta di dispositivi **Tutti i sistemi**.  

4. Nella pagina **Contenuto** verificare che il punto di distribuzione da cui si vuole consentire ai PC di installare l'applicazione sia selezionato.  

5. Nella pagina **Impostazioni di distribuzione** assicurarsi che l'azione di distribuzione sia impostata su **Installa** e che lo scopo della distribuzione sia impostato su **Richiesto**.  

    > [!TIP]  
    > Impostando lo scopo della distribuzione su **Richiesto** si garantisce che l'applicazione venga installata nei PC che soddisfano i requisiti impostati. Se si imposta questo valore su **Disponibile**, gli utenti possono installare l'applicazione su richiesta da Software Center.

6. Nella pagina **Pianificazione** è possibile configurare il momento in cui verrà installata l'applicazione. Per questo esempio, selezionare **Appena possibile dopo il tempo disponibile**.  

7. Nella pagina **Esperienza utente** scegliere **Avanti** per accettare i valori predefiniti.  

8. Completare la procedura guidata.  

Usare le informazioni della sezione seguente **Monitorare l'applicazione** per visualizzare lo stato della distribuzione dell'applicazione.  

## <a name="monitor-the-application"></a>Monitorare l'applicazione

 In questa sezione verrà esaminato rapidamente lo stato di distribuzione dell'applicazione appena distribuita.  

### <a name="to-review-the-deployment-status"></a>Per esaminare lo stato di distribuzione  

1. Nella console di Configuration Manager scegliere **Monitoraggio** > **Distribuzioni**.  

2. Selezionare **Applicazione Contoso**dall'elenco delle distribuzioni.  

3. Nella scheda **Home** scegliere **Visualizza stato** nel gruppo **Distribuzione**.  

4. Selezionare una delle schede seguenti per visualizzare più aggiornamenti di stato sulla distribuzione delle applicazioni:  

    - **Operazione riuscita**: l'applicazione è stata installata correttamente nei PC indicati.  

    - **In corso**: l'installazione dell'applicazione non è ancora terminata.  

    - **Errore**: si è verificato un errore durante l'installazione dell'applicazione nei PC indicati. Vengono visualizzate anche altre informazioni sull'errore.  

    - **Requisiti non soddisfatti**: non è stato effettuato alcun tentativo di installazione nei dispositivi indicati perché non soddisfano i requisiti configurati (in questo esempio, perché non eseguono Windows 10).  

    - **Sconosciuto**: Configuration Manager non è riuscito a segnalare lo stato della distribuzione. Ricontrollare in seguito.  

> [!TIP]  
> Esistono diversi modi in cui è possibile monitorare le distribuzioni di applicazioni. Per informazioni dettagliate, vedere [Monitorare le applicazioni](../deploy-use/monitor-applications-from-the-console.md).

## <a name="end-user-experience"></a>Esperienza utente finale  

Gli utenti con PC gestiti da Configuration Manager che eseguono Windows 10 visualizzano un messaggio che informa della necessità di installare l'applicazione Contoso. Una volta accettata l'installazione, l'applicazione viene installata.  

A partire da Configuration Manager versione 1906, la notifica **È disponibile nuovo software** viene visualizzata una sola volta per un utente per un'applicazione e una versione specifiche. L'utente non visualizzerà più la notifica a ogni accesso. Gli utenti visualizzeranno un'altra notifica solo se l'applicazione è stata modificata o ridistribuita.

## <a name="next-steps"></a>Passaggi successivi

[Monitorare le applicazioni](../deploy-use/monitor-applications-from-the-console.md)
