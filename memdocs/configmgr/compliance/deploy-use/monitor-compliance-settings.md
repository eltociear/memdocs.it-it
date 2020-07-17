---
title: Monitorare le impostazioni di conformità
titleSuffix: Configuration Manager
description: Usare una o più delle procedure descritte in questo argomento per visualizzare lo stato di conformità della linea di base di configurazione.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 92c1ccca-a748-44cd-a52e-e41d34bf981d
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: e2a378c1f54eb9bccbcc21f50419176bd39cb3ac
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240049"
---
# <a name="monitor-compliance-settings-in-configuration-manager"></a>Monitorare le impostazioni di conformità in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Dopo aver distribuito le linee di base di configurazione di Configuration Manager nei dispositivi della gerarchia, è possibile usare una o più delle procedure di questo argomento per visualizzare lo stato di conformità della linea di base di configurazione:

> [!NOTE]  
>  I campi dei criteri di convalida nei report delle impostazioni di conformità (l'equivalente del report sul lato client è **Vincoli**) visualizzano il linguaggio SML (Service Modeling Language) sottostante. Ciò può rendere difficile la comprensione dei criteri di convalida per gli amministratori che hanno creato l'elemento di configurazione nella console di Configuration Manager e non conoscono il linguaggio SML. In questo caso usare l'area di lavoro **Monitoraggio** nella console di Configuration Manager per visualizzare le proprietà dell'elemento di configurazione e i relativi criteri di convalida.  

##  <a name="view-compliance-results-in-the-configuration-manager-console"></a>Visualizzare i risultati di conformità nella console di Configuration Manager  
 Usare questa procedura per visualizzare i dettagli sulla conformità delle linee di base di configurazione nella console di Configuration Manager.  

### <a name="view-compliance-results-in-the-configuration-manager-console"></a>Visualizzare i risultati di conformità nella console di Configuration Manager  

1.  Nella console di Configuration Manager fare clic su **Monitoraggio** > **Distribuzioni**.  

3.  Nell'elenco **Distribuzioni** selezionare la distribuzione della linea di base di configurazione per la quali si vuole esaminare le informazioni sulla conformità.  

4.  È possibile riesaminare le informazioni di riepilogo sulla conformità della distribuzione della linea di base di configurazione nella pagina principale. Per visualizzare informazioni più dettagliate, selezionare la distribuzione della linea di base di configurazione e quindi nel gruppo **Distribuzione** nella scheda **Home** fare clic su **Visualizza stato** per aprire la pagina **Stato distribuzione** .  

     La pagina **Stato distribuzione** contiene le seguenti schede:  

    -   **Conforme**: visualizza la conformità della linea di base di configurazione in base al numero degli asset interessati. È possibile fare clic su una regola per creare un nodo temporaneo nel nodo **Utenti** o **Dispositivi** dell'area di lavoro **Asset e conformità** che contiene tutti gli utenti o i dispositivi conformi a questa regola. Il riquadro **Dettagli asset** visualizza utenti o dispositivi che sono conformi alla linea di base di configurazione. Fare doppio clic su un dispositivo o su un utente presente nell'elenco per visualizzare informazioni aggiuntive.  

        > [!IMPORTANT]  
        >  Una regola dell'elemento di configurazione non viene valutata se non è rilevata o non è applicabile in un dispositivo client. Tuttavia, la regola viene restituita come conforme.  

    -   **Errore**: visualizza un elenco di tutti gli errori relativi alla distribuzione della linea di base di configurazione, in base al numero di asset interessati. È possibile fare clic su una regola per creare un nodo temporaneo nel nodo **Utenti** o **Dispositivi** dell'area di lavoro **Asset e conformità** che contiene tutti gli utenti o tutti i dispositivi che hanno generato errori con questa regola. Quando si seleziona un utente o un dispositivo, il riquadro **Dettagli asset** visualizza gli utenti o i dispositivi interessati dal problema selezionato. Fare doppio clic su un dispositivo o su un utente presente nell'elenco per visualizzare informazioni aggiuntive sul problema.  

    -   **Non conforme**: visualizza un elenco di tutte le regole non conformi all'interno della linea di base di configurazione, in base al numero di asset interessati. È possibile fare clic su una regola per creare un nodo temporaneo nel nodo **Utenti** o **Dispositivi** dell'area di lavoro **Asset e conformità** che contiene tutti gli utenti o i dispositivi non conformi a questa regola. Quando si seleziona un utente o un dispositivo, il riquadro **Dettagli asset** visualizza gli utenti o i dispositivi interessati dal problema selezionato. Fare doppio clic su un utente o su un dispositivo presente nell'elenco per visualizzare informazioni aggiuntive sul problema.  

    -   **Sconosciuto**: visualizza un elenco di tutti gli utenti e di tutti i dispositivi che non sono conformi alla distribuzione della linea di base di configurazione selezionata e lo stato del client dei dispositivi.  

5.  Nella pagina **Stato distribuzione** è possibile esaminare le informazioni dettagliate sulla conformità della linea di base di configurazione distribuita. Viene creato un nodo temporaneo nel nodo **Distribuzioni** che consente di ritrovare rapidamente queste informazioni.  

##  <a name="view-compliance-results-by-using-reports"></a>Visualizzare i risultati di conformità usando i report  
 Le impostazioni di conformità in Configuration Manager includono una serie di report predefiniti che consentono di monitorare le informazioni relative a elementi di configurazione, linee di base di configurazione e distribuzioni. Tali report dispongono della categoria report di **Gestione conformità e impostazioni**.  

> [!IMPORTANT]  
>  È necessario usare un carattere jolly ( **%** ) quando si usano i parametri **Filtro dispositivo** e Filtro utente nei report delle impostazioni di conformità.  

 Per altre informazioni sulle modalità di configurazione della creazione di report in Configuration Manager, vedere [Introduzione ai report](../../core/servers/manage/introduction-to-reporting.md).

##  <a name="view-compliance-results-on-a-configuration-manager-windows-client-computer"></a>Visualizzare i risultati di conformità in un computer client Windows di Configuration Manager

> [!NOTE]  
>  Non è possibile visualizzare informazioni relative al client Windows di Configuration Manager se si è connessi con un account Guest del dominio.    

1.  Passare a **Configuration Manager** nel Pannello di controllo del computer client e quindi fare doppio clic per aprirne le relative proprietà.  

2.  Fare clic sulla scheda **Configurazioni** e visualizzare l'elenco delle linee di base di configurazione distribuite.  

3.  Visualizzare lo **stato di conformità** per ogni linea di base di configurazione:  

    > [!IMPORTANT]  
    >  I risultati della valutazione vengono memorizzati nella cache del client per 15 minuti. Se si avvia una nuova valutazione entro l'intervallo di 15 minuti, anziché una nuova valutazione vengono restituiti i risultati di conformità memorizzati nella cache. Pertanto, se nel client si apporta una modifica che potrebbe influire sui risultati della valutazione della conformità, attendere più di 15 minuti prima di avviare una nuova valutazione.  

    -   **Conforme**: il computer client è conforme alla linea di base di configurazione valutata.  

    -   **Non conforme**: il computer client non è conforme alla linea di base di configurazione valutata.  

    -   **Sconosciuto**: la linea di base di configurazione del computer client non è ancora stata valutata. Se si vuole avviare una valutazione non compresa nella pianificazione della valutazione della conformità, selezionare le linee di base di configurazione da valutare e quindi fare clic su **Valuta**.  

        > [!NOTE]  
        >  Se si dispone di credenziali di amministratore locale nel computer client, è possibile visualizzare i dettagli di ogni linea di base di configurazione valutata per determinare l'elemento di configurazione associato a uno stato non conforme. A tale scopo, selezionare la linea di base di configurazione e quindi fare clic su **Visualizza report**.  

4.  Fare clic su **OK**.  

##  <a name="create-collections-based-on-configuration-baseline-compliance"></a>Creare raccolte basate sulla conformità della linea di base di configurazione  
 Usare la procedura seguente per creare una raccolta di Configuration Manager in base a dispositivi con una conformità specificata. È possibile creare raccolte basate sugli stati di conformità seguenti:  

-   **Conforme**  

-   **Erroree**  

-   **Non-compliant**  

-   **Sconosciuto**  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità** > **Impostazioni di conformità** > **Linee di base di configurazione**.  

3.  Nell'elenco **Linee di base di configurazione** selezionare la linea di base di configurazione da cui si vuole creare una raccolta.  

4.  Nel **gruppo di distribuzione** della scheda **Distribuzione**fare clic su **Crea nuova raccolta** e quindi nell'elenco a discesa selezionare il livello di conformità per il quale si vuole creare una raccolta.  

5.  Viene avviata la **Creazione guidata raccolta utenti** o **Creazione guidata raccolta dispositivi** , a seconda se l'elemento di configurazione viene distribuito a utenti o dispositivi. La procedura guidata viene automaticamente popolata con i valori corretti per creare la raccolta. È tuttavia possibile modificare questi valori.  

6.  Dopo aver completato la procedura guidata, la raccolta visualizza il nodo **Raccolte utenti** o **Raccolte dispositivi** nell'area di lavoro **Asset e conformità** .  
