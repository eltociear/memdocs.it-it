---
title: Creare applicazioni per computer Mac
titleSuffix: Configuration Manager
description: Questo articolo descrive le considerazioni da tenere presenti quando si creano e distribuiscono applicazioni per i computer Mac.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: ab1aecdd-d943-44f5-b0a9-e8fe7439e5d6
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 3b734dc6149c1613d986205577b46160d363d31d
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075789"
---
# <a name="create-mac-computer-applications-with-configuration-manager"></a>Creare applicazioni per computer Mac con Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Tenere presenti le seguenti considerazioni quando si creano e si distribuiscono applicazioni per i computer Mac.  

> [!IMPORTANT]  
>  Le procedure descritte in questo argomento offrono informazioni sulla distribuzione di applicazioni in computer Mac in cui è installato il client di Configuration Manager. I computer Mac registrati con Microsoft Intune non supportano la distribuzione di applicazioni.  

## <a name="general-considerations"></a>Considerazioni generali  
 È possibile usare Configuration Manager per distribuire applicazioni nei computer Mac che eseguono il client Mac di Configuration Manager. I passaggi per distribuire software nei computer Mac sono simili a quelli per distribuire software nei computer Windows. Tuttavia, prima di creare e distribuire applicazioni nei computer Mac gestiti da Configuration Manager, prendere in considerazione quanto segue:  

-   Prima di distribuire pacchetti di applicazioni Mac nei computer Mac, è necessario usare lo strumento **CMAppUtil** in un computer Mac per convertire tali applicazioni in un formato che possa essere letto da Configuration Manager.  

-   Configuration Manager non supporta la distribuzione di applicazioni Mac agli utenti. Le distribuzioni devono essere effettuate a un dispositivo. Analogamente, per le distribuzioni di applicazioni Mac, Configuration Manager non supporta l'opzione **Pre-distribuisci il software nel dispositivo primario dell'utente** nella pagina **Impostazioni distribuzione** della **Distribuzione guidata del software**.  

-   Le applicazioni Mac supportano distribuzioni simulate.  

-   Non è possibile distribuire applicazioni in computer Mac con lo scopo **Disponibile**.  

-   L'opzione per inviare pacchetti di riattivazione quando si distribuisce software non è supportata per i computer Mac.  

-   I computer Mac non supportano il Servizio trasferimento intelligente in background (BITS) per il download del contenuto dell'applicazione. Se il download dell'applicazione non ha esito positivo, verrà riavviato dall'inizio.  

-   Configuration Manager non supporta le condizioni globali quando si creano tipi di distribuzione per i computer Mac.  

## <a name="steps-to-create-and-deploy-an-application"></a>Passaggi per creare e distribuire un'applicazione  
 Nella tabella seguente vengono forniti i passaggi, i dettagli e le informazioni per la creazione e la distribuzione di applicazioni per computer Mac.  


|                                         Passaggio                                          |                                                                                                             Dettagli                                                                                                              |
|---------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|            **Passaggio 1**: Preparare le applicazioni Mac per Configuration Manager             | Per poter creare applicazioni di Configuration Manager da pacchetti software Mac, è necessario usare lo strumento **CMAppUtil** in un computer Mac per convertire il software Mac in un file <strong>CMMAC</strong> di Configuration Manager. |
| **Passaggio 2**: Creare un'applicazione di Configuration Manager che contenga il software Mac |                                                                       Usare la **Creazione guidata applicazione** per creare un'applicazione per il software Mac.                                                                       |
|             **Passaggio 3**: Creare un tipo di distribuzione per l'applicazione Mac              |                                                              Questo passaggio è necessario solo se non si effettuata l'importazione automatica di queste informazioni dall'applicazione.                                                               |
|                        **Passaggio 4**: Distribuire l'applicazione Mac                         |                                                                          Usare la **Distribuzione guidata del software** per distribuire l'applicazione nei computer Mac.                                                                          |
|               **Passaggio 5**: Monitorare la distribuzione dell'applicazione Mac               |                                                                                 Monitorare le corrette distribuzioni delle applicazioni nei computer Mac.                                                                                 |

## <a name="supplemental-procedures-to-create-and-deploy-applications-for-mac-computers"></a>Procedure supplementari per creare e distribuire applicazioni per computer Mac  
 Usare le procedure che seguono per creare e distribuire applicazioni per computer Mac gestiti da Configuration Manager.  

###  <a name="step-1-prepare-mac-applications-for-configuration-manager"></a>Passaggio 1: Preparare le applicazioni Mac per Configuration Manager  
 Il processo per la creazione e la distribuzione di applicazioni di Configuration Manager nei computer Mac è simile al processo di distribuzione per i computer Windows. Tuttavia, prima di creare applicazioni di Configuration Manager che contengono tipi di distribuzione Mac, occorre preparare le applicazioni usando lo strumento **CMAppUtil** . Questo strumento viene scaricato con i file di installazione client Mac. Lo strumento **CMAppUtil** può raccogliere informazioni sull'applicazione, che includono i dati di rilevamento dai seguenti pacchetti Mac:  

-   Immagine disco Apple (.dmg)  

-   File meta pacchetto (.mpkg)  

-   Pacchetto di Mac OS X Installer (.pkg)  

-   Applicazione di Mac OS X (.app)  

Dopo aver raccolto informazioni sull'applicazione, **CMAppUtil** crea un file con estensione **.cmmac**. Questo file contiene i file di installazione per il software Mac e le informazioni sui metodi di rilevamento da usare per stabilire se l'applicazione sia stata già installata. **CMAppUtil** è anche in grado di elaborare i file **.dmg** che contengono più applicazioni Mac e di creare tipi di distribuzione diversi per ogni applicazione.  

1.  Copiare il pacchetto di installazione software Mac nella cartella sul computer Mac in cui sono stati estratti i contenuti del file **macclient.dmg** scaricato dall'Area download Microsoft.  

2.  Nello stesso computer Mac, aprire una finestra terminale e spostarsi nella cartella in cui sono stati estratti i contenuti del file **macclient.dmg** .  

3.  Spostarsi nella cartella **Strumenti** e digitare il seguente comando della riga di comando:  

     **./CMAppUtil** *<proprietà\>*  

     Ad esempio, potrebbe essere necessario convertire i contenuti di un file di immagine disco Apple denominato **MySoftware.dmg** memorizzato nella cartella desktop dell'utente in un file **cmmac** nella stessa cartella, nonché creare file **cmmac** per tutte le applicazioni trovate nel file di immagine disco. A tale scopo, utilizzare la seguente riga di comando:  

     **./CMApputil –c /Users/** *<Nome utente\>* **/Desktop/MySoftware.dmg -o /Users/** *<Nome utente\>* **/Desktop -a**  

    > [!NOTE]  
    >  Il nome dell'applicazione non deve essere lungo più di 128 caratteri.  

     Per configurare le opzioni per **CMAppUtil**, utilizzare le proprietà della riga di comando riportate nella tabella seguente:  

    |Proprietà|Altre informazioni|  
    |--------------|----------------------|  
    |**-h**|Visualizza le proprietà della riga di comando disponibili.|  
    |**-r**|Visualizza come output **detection.xml** del file **.cmmac** fornito in **stdout**. L'output contiene i parametri di rilevamento e la versione di **CMAppUtil** utilizzata per creare il file **.cmmac** .|  
    |**-c**|Specifica il file di origine da convertire.|  
    |**-o**|Specifica il percorso di output in combinazione con la proprietà –c.|  
    |**-a**|Crea automaticamente file con estensione cmmac in combinazione con la proprietà –c per tutte le applicazioni e i pacchetti nel file di immagine disco.|  
    |**-s**|Ignora la generazione di **detection.xml** se non vengono trovati parametri di rilevamento e forza la creazione del file **.cmmac** senza il file **detection.xml** .|  
    |**-v**|Visualizza un output più dettagliato dallo strumento **CMAppUtil** insieme a informazioni di diagnostica.|  

4.  Assicurarsi che il file **.cmmac** sia stato creato nella cartella di output specificata.  

###  <a name="create-a-configuration-manager-application-that-contains-the-mac-software"></a>Creare un'applicazione di Configuration Manager che contenga il software Mac  

Usare la procedura che segue per creare e distribuire un'applicazione per computer Mac gestiti da Configuration Manager.  

1.  Nella console di Configuration Manager scegliere **Raccolta software** > **Gestione applicazioni** > **Applicazioni**.  

3.  Nella scheda **Home**, nel gruppo **Crea**, scegliere **Crea applicazione**.  

4.  Nella pagina **Generale** della **Creazione guidata applicazione**selezionare **Rileva automaticamente le informazioni sull'applicazione dai file di installazione**.  

    > [!NOTE]  
    >  Se si vogliono specificare informazioni sull'applicazione manualmente, selezionare **Specifica manualmente le informazioni dell'applicazione**. Per altre informazioni su come specificare manualmente le informazioni, vedere [Come creare applicazioni con Configuration Manager](../../apps/deploy-use/create-applications.md).  

5.  Nell'elenco a discesa **Tipo** , selezionare **Mac OS X**.  

6.  Nel campo **Percorso** specificare il percorso UNC nel formato *\\\\<server\>\\<condivisione\>\\<nomefile\>* al file di installazione dell'applicazione Mac (file **CMMAC**) che rileverà le informazioni dell'applicazione. In alternativa, scegliere **Sfoglia** per individuare e specificare il percorso del file di installazione.  

    > [!NOTE]  
    >  È necessario accedere al percorso UNC che contiene l'applicazione.  

7.  Scegliere **Avanti**.  

8.  Nella pagina **Importazione informazioni** della **Creazione guidata applicazione** esaminare le informazioni che sono state importate. Se necessario, è possibile scegliere **Indietro** per tornare indietro e correggere eventuali errori. Scegliere **Avanti** per continuare.  

9. Nella pagina **Informazioni generali** della **Creazione guidata applicazione** specificare informazioni sull'applicazione quali nome dell'applicazione, commenti, versione e riferimenti facoltativi che consentono di fare riferimento all'applicazione nella console di Configuration Manager.  

    > [!NOTE]  
    >  Alcune delle informazioni dell'applicazione potrebbero essere già presenti in questa pagina se sono state ottenute in precedenza dai file di installazione dell'applicazione.  

10. Scegliere **Avanti**, riesaminare le informazioni sull'applicazione nella pagina **Riepilogo** e quindi completare la **Creazione guidata applicazione**.  

11. La nuova applicazione viene visualizzata nel nodo **Applicazioni** della console di Configuration Manager.  

###  <a name="step-3-create-a-deployment-type-for-the-mac-application"></a>Passaggio 3: Creare un tipo di distribuzione per l'applicazione Mac  
 Usare la procedura che segue per creare un tipo di distribuzione per i computer Mac gestiti da Configuration Manager.  

> [!NOTE]  
>  Se si è effettuata l'importazione automatica delle informazioni sull'applicazione nella **Creazione guidata applicazione**, potrebbe essere già stato creato un tipo di distribuzione per l'applicazione.  

1.  Nella console di Configuration Manager scegliere **Raccolta software** > **Gestione applicazioni** > **Applicazioni**.  

3.  Selezionare un'applicazione. Quindi, nel gruppo **Applicazione** della scheda **Home** scegliere **Crea tipo di distribuzione** per creare un nuovo tipo di distribuzione per questa applicazione.  

    > [!NOTE]  
    >  È anche possibile avviare la **Creazione guidata tipo di distribuzione** dalla **Creazione guidata applicazione** e dalla scheda **Tipi di distribuzione** della finestra di dialogo **Proprietà** di *<nome applicazione\>* .  

4.  Nella pagina **Generale** della **Creazione guidata tipo di distribuzione**, nell'elenco a discesa **Tipo**, selezionare **Mac OS X**.  

5.  Nel campo **Percorso** specificare il percorso UNC nel formato \\\\<server\>\\<condivisione\>\\<nomefile\> nel file di installazione dell'applicazione (file **CMMAC**). In alternativa, scegliere **Sfoglia** per individuare e specificare il percorso del file di installazione.  

    > [!NOTE]  
    >  È necessario accedere al percorso UNC che contiene l'applicazione.  

6.  Scegliere **Avanti**.  

7.  Nella pagina **Importazione informazioni** della **Creazione guidata tipo di distribuzione**, esaminare le informazioni che sono state importate. Se necessario, scegliere **Indietro** per tornare indietro e correggere eventuali errori. Scegliere **Avanti** per continuare.  

8.  Nella pagina **Informazioni generali** della **Creazione guidata tipo di distribuzione**, specificare informazioni sull'applicazione, come il nome dell'applicazione, commenti e lingue in cui è disponibile il tipo di distribuzione.  

    > [!NOTE]  
    >  Alcune delle informazioni sul tipo di distribuzione potrebbero essere già presenti in questa pagina se sono state ottenute in precedenza dai file di installazione dell'applicazione.  

9. Scegliere **Avanti**.  

10. Nella pagina **Requisiti** della **Creazione guidata tipo di distribuzione** è possibile specificare le condizioni da soddisfare prima di poter installare il tipo di distribuzione nei computer Mac.  

11. Scegliere **Aggiungi** per aprire la finestra di dialogo **Creazione requisito** e aggiungere un nuovo requisito.  

    > [!NOTE]  
    >  È anche possibile aggiungere nuovi requisiti nella scheda **Requisiti** della finestra di dialogo **Proprietà** di *<nome del tipo di distribuzione\>* .  

12. Dall'elenco a discesa **Categoria** , selezionare che questo requisito riguarda un dispositivo.  

13. Dall'elenco a discesa **Condizione** selezionare la condizione da usare per valutare se il computer Mac soddisfa i requisiti di installazione. Il contenuto di questo elenco varia a seconda della categoria selezionata.  

14. Dall'elenco a discesa **Operatore** scegliere l'operatore da usare per confrontare la condizione selezionata con il valore specificato per valutare se l'utente o il dispositivo soddisfa i requisiti d'installazione. Gli operatori disponibili variano a seconda della condizione selezionata.  

15. Nel campo **Valore** specificare i valori da usare con la condizione e l'operatore selezionati per valutare se l'utente o il dispositivo soddisfa i requisiti d'installazione. I valori disponibili variano a seconda della condizione e dell'operatore selezionati.

16. Scegliere **OK** per salvare la regola requisito e chiudere la finestra di dialogo **Creazione requisito**.  

17. Nella pagina **Requisiti** della **Creazione guidata tipo di distribuzione** scegliere **Avanti**.  

18. Nella pagina **Riepilogo** della **Creazione guidata tipo di distribuzione**esaminare le azioni che saranno eseguite nella procedura guidata.  Se necessario, scegliere **Indietro** per tornare indietro e modificare le impostazioni del tipo di distribuzione. Scegliere **Avanti** per creare il tipo di distribuzione.  

19. Al termine della pagina **Avanzamento** esaminare le azioni eseguite e scegliere **Chiudi** per completare la **Creazione guidata tipo di distribuzione**.  

20. Se tale procedura guidata è stata avviata da **Creazione guidata applicazione**, verrà visualizzata di nuovo la pagina **Tipi di distribuzione**.  

###  <a name="deploy-the-mac-application"></a>Distribuire l'applicazione Mac  
 I passaggi per distribuire un'applicazione nei computer Mac sono gli stessi di quelli per distribuire un'applicazione nei computer Windows, tranne per le differenze riportate di seguito:  

-   La distribuzione di applicazioni in utenti non è supportata.  

-   Le distribuzioni con scopo **Disponibile** non sono supportate.  

-   L'opzione **Pre-distribuisci il software nel dispositivo primario dell'utente** nella pagina **Impostazioni distribuzione** della **Distribuzione guidata del software** non è supportata.  

-   Poiché i computer Mac non supportano Software Center, l'impostazione **Notifiche utente** nella pagina **Esperienza utente** della **Distribuzione guidata del software** viene ignorata.  

-   L'opzione per inviare pacchetti di riattivazione quando si distribuisce software non è supportata per i computer Mac.  

> [!NOTE]  
>  È possibile creare una raccolta che contenga solo i computer Mac. Per farlo, creare una raccolta che usi una regola di query e usare la query WQL di esempio illustrata nell'argomento [Come creare query](../../core/servers/manage/create-queries.md).  

 Per altre informazioni, vedere l'argomento relativo alla [distribuzione delle applicazioni](../../apps/deploy-use/deploy-applications.md).  

###  <a name="step-5-monitor-the-deployment-of-the-mac-application"></a>Passaggio 5: Monitorare la distribuzione dell'applicazione Mac  
 Per monitorare le distribuzioni di applicazioni nei computer Mac, è possibile usare lo stesso processo usato per la distribuzione di applicazioni nei computer Windows.  

 Per altre informazioni, vedere l'argomento relativo al [monitoraggio delle applicazioni](../deploy-use/monitor-applications-from-the-console.md).  
