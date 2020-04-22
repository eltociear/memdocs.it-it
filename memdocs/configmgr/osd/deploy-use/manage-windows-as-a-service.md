---
title: Gestire Windows come servizio
titleSuffix: Configuration Manager
description: Visualizzare lo stato di Windows as a Service (WaaS) usando Configuration Manager, definire piani di manutenzione per formare anelli di distribuzione e visualizzare avvisi quando i client Windows 10 si avvicinano alla scadenza del supporto.
ms.date: 03/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: da1e687b-28f6-43c4-b14a-ff2b76e60d24
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9a682ec0b3d438a26429486f119d641fd150404f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690329"
---
# <a name="manage-windows-as-a-service-using-configuration-manager"></a>Gestire Windows come servizio con Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

In Configuration Manager è possibile visualizzare lo stato di Windows as a Service (WaaS) nell'ambiente in uso. È possibile creare piani di manutenzione per formare anelli di distribuzione, verificare che i sistemi Windows 10 siano mantenuti aggiornati quando vengono rilasciate nuove build e visualizzare avvisi quando i client Windows 10 si avvicinano alla scadenza del supporto per la build di canale semestrale in uso.

Per altre informazioni sulle opzioni di manutenzione di Windows 10, vedere [Panoramica di Windows as a Service](/windows/deployment/update/waas-overview#servicing-channels).

Usare le sezioni seguenti per gestire Windows come servizio.

## <a name="prerequisites"></a><a name="BKMK_Prerequisites"></a> Prerequisiti

Per visualizzare i dati nel dashboard di manutenzione di Windows 10 è necessario seguire questa procedura:

- I computer Windows 10 devono usare gli aggiornamenti software di Configuration Manager con Windows Server Update Services (WSUS) per la gestione degli aggiornamenti software. Se la gestione degli aggiornamenti software avviene tramite Windows Update per le aziende o Windows Insider, il computer non viene valutato nei piani di manutenzione di Windows 10. Per altre informazioni, vedere [Integrazione con Windows Update for Business in Windows 10](../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md).

- Usare una versione supportata di WSUS:
  - WSUS 10.0.14393 (ruolo in Windows Server 2016)
  - WSUS 10.0.17763 (ruolo in Windows Server 2019) (richiede Configuration Manager 1810 o versioni successive)
  - WSUS 6.2 e 6.3 (ruolo in Windows Server 2012 e Windows Server 2012 R2)
    - [KB 3095113 e KB 3159706 (o un aggiornamento equivalente) devono essere installati](../../sum/plan-design/prerequisites-for-software-updates.md#BKMK_wsus2012) in WSUS 6.2 e 6.3.

- Abilitare Individuazione heartbeat. I dati visualizzati nel dashboard di manutenzione di Windows 10 vengono rilevati con l'individuazione. Per altre informazioni, vedere [Configure Heartbeat Discovery](../../core/servers/deploy/configure/configure-discovery-methods.md#BKMK_ConfigHBDisc).

    Le informazioni sul canale e sulla build di Windows 10 riportate di seguito vengono rilevate e archiviate negli attributi seguenti:  

    - **Ramo per la conformità del sistema operativo**: specifica il canale del sistema operativo. Ad esempio, **0** = Canale semestrale - Mirato (non rinviare gli aggiornamenti), **1** = Canale semestrale (rinvia gli aggiornamenti), **2** = Canale di manutenzione a lungo termine (LTSC, Long-Term Servicing Channel)

    - **Build del sistema operativo**: Specifica la build del sistema operativo. Ad esempio, **10.0.10240** (RTM) o **10.0.10586** (versione 1511)

- Per visualizzare i dati nel dashboard di manutenzione di Windows 10 è necessario installare il punto di connessione del servizio e configurarlo per la modalità **Online, connessione permanente**. In modalità offline gli aggiornamenti dei dati non vengono visualizzati nel dashboard fino a quando non si ottengono aggiornamenti di manutenzione di Configuration Manager. Per altre informazioni, vedere [Informazioni sul punto di connessione del servizio](../../core/servers/deploy/configure/about-the-service-connection-point.md).

- Verificare che nel computer che esegue la console di Configuration Manager sia installato Internet Explorer 9 o versione successiva.

- Assicurarsi che gli aggiornamenti software siano configurati e sincronizzati nella console. Per rendere disponibili gli eventuali aggiornamenti delle funzionalità di Windows 10 nella console di Configuration Manager, selezionare la classificazione **Aggiornamenti** e sincronizzare gli aggiornamenti software. Per altre informazioni, vedere [Prerequisiti per aggiornamenti software](../../sum/get-started/prepare-for-software-updates-management.md).

- A partire da Configuration Manager versione 1902 verificare [l'impostazione client](../../core/clients/deploy/about-client-settings.md#bkmk_thread-priority) **Specificare la priorità del thread per gli aggiornamenti delle funzionalità** per assicurarsi che sia appropriata per l'ambiente in uso.

- A partire da Configuration Manager versione 1906, verificare l'[impostazione client](../../core/clients/deploy/about-client-settings.md#bkmk_du) **Enable Dynamic Update for feature updates** (Abilita aggiornamento dinamico per gli aggiornamenti delle funzionalità) per assicurarsi che sia appropriata per l'ambiente in uso. <!--4062619-->

## <a name="windows-10-servicing-dashboard"></a><a name="BKMK_ServicingDashboard"></a> Dashboard di manutenzione di Windows 10

Il dashboard di manutenzione di Windows 10 fornisce informazioni sui computer Windows 10 nell'ambiente, piani di manutenzione attivi, informazioni di conformità e così via. I dati disponibili nel dashboard di manutenzione di Windows 10 variano a seconda che il punto di connessione del servizio sia installato o meno. Il dashboard include i riquadri seguenti:

- **Riquadro Utilizzo di Windows 10**: contiene un riepilogo delle build pubbliche di Windows 10. Le build di Windows Insider sono elencate come **altro** insieme ad altre eventuali build che non sono note al sito. Il punto di connessione del servizio scarica i metadati contenenti informazioni sulle build di Windows. Questi dati vengono quindi confrontati con i dati di individuazione.

- **Riquadro Anelli di Windows 10**: contiene un riepilogo di Windows 10 in base ai canali e allo stato di conformità. Il segmento LTSC include tutte le versioni LTSC. Il primo riquadro contiene un riepilogo dettagliato di versioni specifiche, ad esempio Windows 10 LTSC 2015.

- **Riquadro Crea piano di manutenzione**: offre un modo rapido per creare un piano di manutenzione. Specificare il nome e la raccolta, tenendo presente che vengono visualizzate solo le prime 10 raccolte per dimensioni, a partire dalla più piccola. Specificare anche lo stato di conformità e il pacchetto di distribuzione, tenendo presente che vengono visualizzati solo i primi 10 pacchetti modificati più di recente. Per le altre impostazioni vengono usati i valori predefiniti. Fare clic su **Impostazioni avanzate** per avviare la procedura guidata Crea piano di manutenzione in cui è possibile configurare tutte le impostazioni del piano di servizio.

- **Riquadro Scaduta**: visualizza la percentuale di dispositivi presenti in una build di Windows 10 che ha superato la scadenza. Configuration Manager determina questa percentuale dai metadati scaricati dal punto di connessione del servizio messi a confronto con i dati di individuazione. Una build che ha superato la scadenza non riceve più gli aggiornamenti cumulativi mensili, inclusi gli aggiornamenti della sicurezza. I computer in questa categoria devono essere aggiornati alla versione successiva della build. Configuration Manager arrotonda al numero intero successivo. Ad esempio, se si hanno 10.000 computer e soltanto uno con una build scaduta, il riquadro restituisce 1%.

- **Riquadro Scade a breve**: visualizza la percentuale di computer presenti in una build in procinto di scadere nei quattro mesi successivi, analogamente al riquadro **Scaduta**. Configuration Manager arrotonda al numero intero successivo.

- **Riquadro Avvisi**: visualizza gli avvisi attivi.

- **Riquadro Monitoraggio piano di manutenzione**: visualizza i piani di manutenzione creati e un grafico della conformità per ognuno. Questo riquadro offre una rapida panoramica dello stato attuale delle distribuzioni del piano di manutenzione. Se un anello di distribuzione precedente soddisfa le previsioni di conformità, è possibile selezionare un piano di manutenzione o un anello di distribuzione successivo e fare clic su **Distribuisci ora** , anziché attendere l'attivazione automatica delle regole del piano di manutenzione.

- **Riquadro Build di Windows 10**: visualizza l'immagine fissa di una sequenza temporale che offre una panoramica delle build di Windows 10 attualmente rilasciate e informazioni generali sul momento in cui passeranno a stati diversi. Questo riquadro è stato rimosso a partire da Configuration Manager versione 1902. Sono infatti disponibili informazioni più dettagliate nel [dashboard del ciclo di vita del prodotto](../../core/clients/manage/asset-intelligence/product-lifecycle-dashboard.md). <!--3446861-->

> [!IMPORTANT]
> Le informazioni visualizzate nel dashboard di manutenzione di Windows 10, ad esempio il ciclo di vita del supporto per le versioni di Windows 10, vengono fornite per agevolare l'utente e sono destinate solo all'uso interno all'azienda. Non fare affidamento esclusivamente su queste informazioni per accertare la conformità dell'aggiornamento. Verificare l'accuratezza delle informazioni fornite.

## <a name="drill-through-required-updates"></a>Drill-through degli aggiornamenti obbligatori
<!--4224414-->
*(Funzionalità introdotta nella versione 1906)*

È possibile esaminare nel dettaglio le statistiche di conformità per individuare i dispositivi che richiedono un aggiornamento delle funzionalità di Windows 10 specifico. Per visualizzare l'elenco dei dispositivi, è necessaria l'autorizzazione per visualizzare gli aggiornamenti e le raccolte a cui appartengano i dispositivi. Per eseguire il drill-down nell'elenco dei dispositivi:

1. Passare a **Raccolta software** > **Manutenzione pacchetti di Windows 10** > **Tutti gli aggiornamenti di Windows 10**.
1. Selezionare tutti gli aggiornamenti richiesti da almeno un dispositivo.
1. Esaminare la scheda **Riepilogo** e individuare il grafico a torta in **Statistiche**.
1. Selezionare il collegamento ipertestuale **View Required** (Visualizza richiesto) accanto al grafico a torta per eseguire il drill-down nell'elenco dei dispositivi.
1. Questa azione consente di visualizzare un nodo temporaneo in **Dispositivi** dove è possibile visualizzare i dispositivi che richiedono l'aggiornamento. È anche possibile eseguire azioni per il nodo, come creare una nuova raccolta dall'elenco.

## <a name="servicing-plan-workflow"></a>Flusso di lavoro del piano di manutenzione

I piani di manutenzione di Windows 10 in Configuration Manager sono molto simili alle regole di distribuzione automatica degli aggiornamenti software. Creare un piano di manutenzione con i criteri seguenti, che verrà valutato da Configuration Manager:

- **Classificazione aggiornamenti**: vengono valutati solo gli aggiornamenti presenti nella classificazione **Aggiornamenti**.

- **Stato di conformità**: lo stato di conformità definito nel piano di manutenzione viene confrontato con lo stato di conformità per l'aggiornamento. I metadati per l'aggiornamento vengono recuperati quando il punto di connessione del servizio verifica la disponibilità di aggiornamenti.

- **Differimento**: numero di giorni specificato per l'impostazione **Dopo quanti giorni dalla pubblicazione di un nuovo aggiornamento di Microsoft si vuole eseguire la distribuzione nell'ambiente** nel piano di manutenzione. Se la data corrente è successiva alla data di rilascio più il numero di giorni configurato, Configuration Manager valuta se includere un aggiornamento nella distribuzione.

  Quando un aggiornamento soddisfa i criteri, il piano di manutenzione aggiunge l'aggiornamento al pacchetto di distribuzione, distribuisce il pacchetto nei punti di distribuzione e distribuisce l'aggiornamento nella raccolta in base alle impostazioni configurate nel piano di manutenzione. È possibile monitorare le distribuzioni nel riquadro piano di monitoraggio del piano del servizio, nel dashboard di manutenzione di Windows 10. Per altre informazioni, vedere [Monitorare gli aggiornamenti software](../../sum/deploy-use/monitor-software-updates.md).

> [!NOTE]
> **Windows 10 versione 1903 e successive** è stato aggiunto a Microsoft Update come prodotto a sé stante, anziché all'interno del prodotto **Windows 10** come le versioni precedenti. A causa di questa modifica è necessario eseguire una serie di passaggi manuali per assicurarsi che i client visualizzino questi aggiornamenti. Si è cercato di ridurre il numero di passaggi manuali che è necessario eseguire per il nuovo prodotto in Configuration Manager versione 1906. Per altre informazioni, vedere [Configurazione dei prodotti per le versioni di Windows 10](../../sum/get-started/configure-classifications-and-products.md#windows-10-version-1903-and-later).<!--4682946-->

## <a name="windows-10-servicing-plan"></a><a name="BKMK_ServicingPlan"></a> Piano di manutenzione di Windows 10

Quando si distribuisce il canale semestrale di Windows 10, è possibile creare uno o più piani di manutenzione per definire gli anelli di distribuzione per l'ambiente in uso e monitorarli successivamente nel dashboard di manutenzione di Windows 10. I piani di manutenzione usano solo la classificazione degli aggiornamenti software **Aggiornamenti** e non gli aggiornamenti cumulativi per Windows 10. Per questi aggiornamenti è ancora necessario eseguire la distribuzione usando il flusso di lavoro degli aggiornamenti software. Il piano di manutenzione e gli aggiornamenti software offrono la stessa esperienza all'utente finale, incluse le impostazioni configurate nel piano di manutenzione.  

> [!NOTE]
> È possibile usare una sequenza di attività per distribuire un aggiornamento per ogni build di Windows 10, ma questo richiede un maggiore intervento manuale. Sarebbe necessario importare i file di origine aggiornati come un pacchetto di aggiornamento del sistema operativo e quindi creare e distribuire la sequenza di attività per il set di computer appropriato. Tuttavia, una sequenza di attività offre altre opzioni personalizzate, ad esempio le azioni di pre-distribuzione e post-distribuzione.

È possibile creare un piano di manutenzione di base dal dashboard di manutenzione di Windows 10. Dopo aver specificato il nome, la raccolta (vengono visualizzate solo le prime 10 raccolte per dimensioni, a partire dalla più piccola), il pacchetto di distribuzione (vengono visualizzati solo i primi 10 pacchetti modificati più di recente) e lo stato di conformità, Configuration Manager crea il piano di manutenzione con valori predefiniti per le altre impostazioni. È anche possibile avviare la procedura guidata Crea piano di manutenzione per configurare tutte le impostazioni. Usare la procedura seguente per creare un piano di manutenzione con la procedura guidata Crea piano di manutenzione.  

> [!NOTE]  
> È possibile gestire il comportamento relativo alle distribuzioni ad alto rischio. Una distribuzione ad alto rischio viene installata automaticamente e può causare risultati imprevisti. Ad esempio, una sequenza di attività con scopo impostato su **Obbligatorio** e che distribuisce Windows 10 viene considerata una distribuzione ad alto rischio. Per altre informazioni, vedere [Impostazioni per gestire distribuzioni ad alto rischio](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).

### <a name="to-create-a-windows-10-servicing-plan"></a>Per creare un piano di manutenzione di Windows 10

1. Nella console di Configuration Manager fare clic su **Raccolta software**.

1. Nell'area di lavoro Raccolta software espandere **Manutenzione di Windows 10**e quindi fare clic su **Piani di manutenzione**.

1. Nella scheda **Home** nel gruppo **Crea** fare clic su **Crea piano di manutenzione**. Verrà avviata la procedura guidata Crea piano di manutenzione.

1. Nella pagina **Generale** è possibile configurare le seguenti impostazioni:

    - **Nome**: specificare il nome per il piano di manutenzione. Il nome deve essere univoco, descrivere l'obiettivo della regola e contribuire a differenziarla dalle altre presenti nel sito di Configuration Manager.

    - **Descrizione**: specificare una descrizione per il piano di manutenzione. La descrizione deve fornire una panoramica del piano di manutenzione e qualsiasi altra informazione rilevante per identificare e differenziare il piano dagli altri nel sito di Configuration Manager. Il campo della descrizione è facoltativo, ha un limite di 256 caratteri e un valore vuoto per impostazione predefinita.

1. Nella pagina Piano di manutenzione specificare la **Raccolta di destinazione**. I membri della raccolta ricevono gli aggiornamenti di Windows 10 definiti nel piano di manutenzione.

    - Quando si esegue una distribuzione ad alto rischio, ad esempio quella di un piano di manutenzione, nella finestra **Seleziona raccolta** vengono visualizzate soltanto le raccolte personalizzate che soddisfano le impostazioni di verifica della distribuzione configurate nelle proprietà del sito.

    - Le distribuzioni ad alto rischio sono sempre limitate alle raccolte personalizzate (quelle create dall'utente) e alla racconta predefinita **Computer sconosciuti** . Quando si crea una distribuzione ad alto rischio, non è possibile selezionare una raccolta predefinita quale **Tutti i sistemi**. Deselezionare **Nascondi le raccolte con un numero di membri maggiore della configurazione delle dimensioni minime del sito** per visualizzare tutte le raccolte personalizzate che contengono un numero di client inferiore rispetto alla dimensione massima configurata. Per altre informazioni, vedere [Impostazioni per gestire distribuzioni ad alto rischio](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).

    - Le impostazioni di verifica della distribuzione sono basate sull'appartenenza attuale della raccolta. Dopo aver distribuito il piano di manutenzione, l'appartenenza alla raccolta non viene rivalutata per le impostazioni di distribuzione ad alto rischio.

      - Ad esempio, si supponga di impostare **Dimensione predefinita** su 100 e **Dimensione massima** su 1000. Quando si crea una distribuzione ad alto rischio, nella finestra **Seleziona raccolta** verranno visualizzate solo le raccolte che contengono meno di 100 client. Se si deseleziona l'impostazione **Nascondi le raccolte con un numero di membri maggiore della configurazione delle dimensioni minime del sito**, nella finestra vengono visualizzate le raccolte che includono meno di 1000 client.  
      Quando si seleziona una raccolta che include un ruolo del sito, si applicano i criteri seguenti:
        - Se la raccolta contiene un server di sistema del sito e le impostazioni di verifica della distribuzione sono state configurate in modo da bloccare le raccolte con server di sistema del sito, si verifica un errore e la procedura si arresta.
        - Se la raccolta include un server di sistema del sito e nelle impostazioni di verifica della distribuzione configurate dall'utente viene riportata la presenza di tali server di sistema del sito, se la raccolta supera la dimensione predefinita oppure se la raccolta include un server, nella distribuzione guidata del software verrà visualizzato un messaggio sul rischio elevato dell'operazione. È necessario accettare di creare una distribuzione ad alto rischio, quindi viene creato un messaggio di stato relativo al controllo.

1. Nella pagina Anello di distribuzione configurare le impostazioni seguenti:

   - **Specificare lo stato di conformità di Windows a cui applicare questo piano di manutenzione**: Selezionare una delle opzioni seguenti:

      - **Canale semestrale (mirato)** : in questo modello di manutenzione gli aggiornamenti delle funzionalità sono disponibili non appena vengono rilasciati da Microsoft.

      - **Canale semestrale**: questo canale di manutenzione viene in genere usato per distribuzioni di grandi dimensioni. I client Windows 10 nel canale semestrale ricevono la stessa build di Windows 10 dei dispositivi nel canale mirato, ma in un momento successivo.

        Per altre informazioni sui canali di manutenzione e sulle opzioni più adatte alle proprie esigenze, vedere [Canali di manutenzione](/windows/deployment/update/waas-overview#servicing-channels).

   - **Dopo quanti giorni dalla pubblicazione di un nuovo aggiornamento di Microsoft si vuole eseguire la distribuzione nell'ambiente**: se la data corrente è successiva alla data di rilascio più il numero di giorni configurato per questa impostazione, Configuration Manager valuta se includere un aggiornamento nella distribuzione.

1. Nella pagina Aggiornamenti configurare i criteri di ricerca per filtrare gli aggiornamenti che vengono aggiunti al piano di manutenzione. Vengono aggiunti alla distribuzione associata solo gli aggiornamenti che soddisfano i criteri specificati. Sono disponibili i filtri proprietà seguenti: <!--3098809, 3113836, 3204570 -->

   - **Architettura** (a partire dalla versione 1810)
   - **Lingua**
   - **Categoria prodotto** (a partire dalla versione 1810)
   - **Richiesto**
      > [!IMPORTANT]
      > Nell'ambito dei criteri di ricerca è consigliabile impostare il valore **>=1** nel campo **Richiesto**. L'applicazione di questi criteri assicura che vengano aggiunti al piano di manutenzione solo gli aggiornamenti applicabili.
   - **Sostituito** (a partire dalla versione 1810)
   - **Titolo**

    Fare clic su **Anteprima** per visualizzare gli aggiornamenti che soddisfano i criteri specificati.

1. Nella pagina Pianificazione della distribuzione configurare le seguenti impostazioni:

   - **Pianificazione della valutazione**: specificare se Configuration Manager valuta il tempo disponibile e le scadenze dell'installazione in base all'ora UTC o all'ora locale del computer in cui è in esecuzione la console di Configuration Manager.

       > [!NOTE]
       > Quando si seleziona l'ora locale e quindi si sceglie **Appena possibile** per **Tempo disponibile software** o **Scadenza installazione**, per valutare quando sono disponibili aggiornamento o quando vengono installati in un client, viene usata l'ora corrente del computer che esegue la console di Configuration Manager. Se il client si trova in un fuso orario diverso, verranno eseguite le azioni seguenti quando l'ora del client raggiunge quella impostata per la valutazione.

   - **Tempo disponibile software**: selezionare una delle seguenti impostazioni per specificare quando gli aggiornamenti software saranno disponibili per i client:

        - **Appena possibile**: selezionare questa impostazione per rendere disponibili il prima possibile gli aggiornamenti software inclusi nella distribuzione per i computer client. Quando si crea la distribuzione con questa impostazione selezionata, Configuration Manager aggiorna i criteri client. Quindi, al successivo ciclo di polling dei criteri client, ai client viene comunicata la distribuzione e possono ottenere gli aggiornamenti disponibili per l'installazione.

        - **Orario specifico**: selezionare questa impostazione per rendere disponibili gli aggiornamenti software inclusi nella distribuzione per i computer client in una data e a un orario specifici. Quando si crea la distribuzione con questa impostazione attivata, Configuration Manager aggiorna i criteri client. Quindi, al successivo ciclo di polling dei criteri client, ai client viene comunicata la distribuzione. Gli aggiornamenti del software nella distribuzione non sono però disponibili per l'installazione prima della data e dell'orario configurati.

   - **Scadenza installazione**: selezionare una delle impostazioni seguenti per specificare la scadenza per l'installazione degli aggiornamenti software nella distribuzione:

        - **Appena possibile**: selezionare questa impostazione per installare automaticamente gli aggiornamenti software nella distribuzione appena possibile.

        - **Orario specifico**: selezionare questa impostazione per installare automaticamente gli aggiornamenti software nella distribuzione in una data e a un orario specifici. Configuration Manager determina la scadenza per installare gli aggiornamenti software aggiungendo l'intervallo **Orario specifico** configurato a **Tempo disponibile software**.

           > [!NOTE]
           > L'orario effettivo di scadenza dell'installazione corrisponde all'ora di scadenza visualizzata più una quantità di tempo casuale di massimo 2 ore. Ciò consente di ridurre il potenziale impatto di un'installazione simultanea degli aggiornamenti nella distribuzione da parte di tutti i computer client nella raccolta di destinazione.
           >
           > È possibile configurare l'impostazione **Disabilitare sequenza casuale scadenza** del client **Agente computer** per disabilitare il ritardo della sequenza casuale di installazione per gli aggiornamenti richiesti. Per ulteriori informazioni, vedere [Computer Agent](../../core/clients/deploy/about-client-settings.md#computer-agent).

        - **Ritardare l'imposizione di questa distribuzione in base alle preferenze dell'utente, fino al periodo di tolleranza massimo definito nel client**: Selezionare questa opzione per rispettare l'[impostazione client **Periodo di tolleranza per l'imposizione dopo la scadenza della distribuzione (ore)** ](../../core/clients/deploy/about-client-settings.md#grace-period-for-enforcement-after-deployment-deadline-hours).

1. Nella pagina Esperienza utente, è possibile configurare le seguenti impostazioni:  

    - **Notifiche utente**: specificare se visualizzare la notifica degli aggiornamenti in Software Center nel computer client in base al **Tempo disponibile software** configurato e se visualizzare le notifiche utente nei computer client.

    - **Comportamento scadenza**: specificare il comportamento che deve verificarsi quando si raggiunge la data di scadenza per la distribuzione degli aggiornamenti. Specificare se installare gli aggiornamenti nella distribuzione. Specificare anche se eseguire un riavvio del sistema dopo l'installazione dell'aggiornamento, indipendentemente da una finestra di manutenzione configurata. Per altre informazioni sulle finestre di manutenzione, vedere [Come usare le finestre di manutenzione](../../core/clients/manage/collections/use-maintenance-windows.md).  

    - **Comportamento riavvio dispositivo**: specificare se evitare un riavvio del sistema in server e workstation dopo l'installazione degli aggiornamenti e se è richiesto un riavvio del sistema per completare l'installazione.

    - **Gestione filtri di scrittura per dispositivi con Windows Embedded**: quando si distribuiscono aggiornamenti in dispositivi con Windows Embedded abilitati per i filtri di scrittura, è possibile specificare di installare l'aggiornamento nell'overlay temporaneo ed eseguire il commit delle modifiche in seguito oppure alla scadenza dell'installazione o all'interno di una finestra di manutenzione. Quando si confermano le modifiche alla scadenza dell'installazione o all'interno di una finestra di manutenzione, è necessario il riavvio per mantenere le modifiche nel dispositivo.
        - Quando si distribuisce un aggiornamento in un dispositivo con Windows Embedded, verificare che il dispositivo appartenga a una raccolta con una finestra di manutenzione configurata.

    - **Comportamento di rivalutazione della distribuzione degli aggiornamenti software al riavvio**: Per forzare un altro ciclo di valutazione della distribuzione degli aggiornamenti, selezionare l'opzione **Se un aggiornamento di questa distribuzione richiede un riavvio del sistema, eseguire un ciclo di valutazione della distribuzione degli aggiornamenti dopo il riavvio**.

1. Nella pagina Pacchetto di distribuzione selezionare un pacchetto di distribuzione esistente, nessun pacchetto di distribuzione o configurare le impostazioni seguenti per creare un nuovo pacchetto di distribuzione:

    1. **Nome**: specificare il nome del pacchetto di distribuzione. Questo nome deve essere univoco e descrivere il contenuto del pacchetto. Il nome può contenere un massimo di 50 caratteri.

    1. **Descrizione**: specificare una descrizione che includa informazioni sul pacchetto di distribuzione. La descrizione deve contenere un massimo di 127 caratteri.

    1. **Origine pacchetto**: specifica il percorso dei file di origine dell'aggiornamento software. Digitare un percorso di rete per il percorso di origine, ad esempio **\\\server\\nomecondivisione\\percorso** oppure fare clic su **Sfoglia** per trovare il percorso di rete. Prima di procedere alla pagina successiva, è necessario creare la cartella condivisa per i file di origine del pacchetto di distribuzione.
        - Il percorso di origine del pacchetto di distribuzione specificato non può essere usato da un altro pacchetto di distribuzione software.
        - L'account computer del provider SMS e l'utente che esegue la procedura guidata per scaricare gli aggiornamenti software devono disporre entrambi delle autorizzazioni NTFS di **Scrittura** nel percorso download. È necessario limitare con attenzione l'accesso al percorso di download per ridurre il rischio di manomissioni da parte di utenti malintenzionati dei file origine degli aggiornamenti software.
        - È possibile modificare il percorso di origine del pacchetto nelle proprietà del pacchetto di distribuzione dopo che Configuration Manager ha creato il pacchetto di distribuzione. Ma in tal caso, è prima necessario copiare il contenuto dall'origine del pacchetto originale nel nuovo percorso di origine del pacchetto.

    1. **Priorità di invio**: specificare la priorità di invio per il pacchetto di distribuzione. Configuration Manager usa la priorità di invio quando invia il pacchetto di distribuzione ai punti di distribuzione. I pacchetti di distribuzione vengono inviati in ordine di priorità: Alta, Media o Bassa. I pacchetti con priorità identiche vengono inviati nell'ordine in cui sono stati creati. Se non esiste alcun backlog, il pacchetto esegue immediatamente l'elaborazione, indipendentemente dalla priorità configurata.

    1. **Abilita replica differenziale binaria**: Abilitare questa opzione se si vuole usare la replica differenziale binaria.

1. Nella pagina Punti di distribuzione specificare i punti di distribuzione o i gruppi di punti di distribuzione che ospitano i file di aggiornamento. Per altre informazioni, vedere [Configurare un punto di distribuzione](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs).

    > [!NOTE]
    > Questa pagina è disponibile solo quando si crea un nuovo pacchetto di distribuzione di aggiornamento software.  

1. Nella pagina Percorso download specificare se scaricare i file di aggiornamento da Internet o dalla rete locale. Configurare le seguenti impostazioni:

    - **Scarica aggiornamenti software da Internet**: selezionare questa impostazione per scaricare gli aggiornamenti da un percorso specificato su Internet. Questa opzione è attivata per impostazione predefinita.

    - **Scarica aggiornamenti software dal seguente percorso nella rete locale**: selezionare questa impostazione per scaricare gli aggiornamenti da una directory locale o una cartella condivisa. Questa impostazione è utile quando il computer che esegue la procedura guidata non ha accesso a Internet. I computer con accesso a Internet possono scaricare preventivamente gli aggiornamenti e archiviarli in un percorso di rete locale accessibile al computer che esegue la procedura guidata.

1. Nella pagina Selezione lingua selezionare le lingue per cui vengono scaricati gli aggiornamenti selezionati. Gli aggiornamenti vengono scaricati solo se sono disponibili nelle lingue selezionate. Gli aggiornamenti non specifici della lingua vengono sempre scaricati. Per impostazione predefinita, la procedura guidata consente di selezionare le lingue configurate nelle proprietà del punto di aggiornamento software. Prima di procedere alla pagina successiva, è necessario selezionare almeno una lingua. Quando si selezionano solo lingue non supportate da un aggiornamento, il download dell'aggiornamento non riesce.

1. Nella pagina Riepilogo rivedere le impostazioni e fare clic su **Avanti** per creare il piano di manutenzione.  

Dopo aver completato la procedura guidata, verrà eseguito il piano di manutenzione. Gli aggiornamenti che soddisfano i criteri specificati vengono aggiunti a un gruppo di aggiornamenti software, scaricati nella raccolta contenuto nel server del sito e distribuiti ai punti di distribuzione configurati. Il gruppo di aggiornamenti software viene quindi distribuito ai client inclusi nella raccolta di destinazione.

## <a name="modify-a-servicing-plan"></a><a name="BKMK_ModifyServicingPlan"></a> Modificare un piano di manutenzione

Dopo aver creato un piano di manutenzione di base dal dashboard di manutenzione di Windows 10 oppure se è necessario modificare le impostazioni per un piano di manutenzione esistente, è possibile passare alle proprietà del piano di manutenzione.

> [!NOTE]
> È possibile configurare le impostazioni nelle proprietà per il piano di manutenzione che non sono disponibili nella procedura guidata usata per la creazione del piano di manutenzione. La procedura guidata usa valori predefiniti per le impostazioni di download, le impostazioni di distribuzione e gli avvisi.  

Per modificare le proprietà di un piano di manutenzione, seguire la procedura riportata di seguito. 

### <a name="to-modify-the-properties-of-a-servicing-plan"></a>Per modificare le proprietà di un piano di manutenzione

1. Nella console di Configuration Manager fare clic su **Raccolta software**.

1. Nell'area di lavoro Raccolta software espandere **Manutenzione di Windows 10**, fare clic su **Piani di manutenzione** e quindi selezionare il piano di manutenzione che si vuole modificare.

1. Nella scheda **Home** fare clic su **Proprietà** per aprire le proprietà del piano di manutenzione selezionato.

    Le impostazioni seguenti sono disponibili nelle proprietà del piano di manutenzione non configurate nella procedura guidata:

    **Impostazioni distribuzione**: nella scheda Impostazioni distribuzione configurare le impostazioni seguenti:

    - **Usa riattivazione LAN per riattivare i client per le distribuzioni richieste**: specificare se abilitare la riattivazione LAN alla scadenza per inviare pacchetti di riattivazione ai computer che richiedono uno o più aggiornamenti software nella distribuzione. Tutti i computer in modalità sospensione all'ora di scadenza dell'installazione vengono riattivati in modo che si possa avviare l'installazione degli aggiornamenti software. I client in modalità sospensione che non richiedono aggiornamenti software nella distribuzione non vengono avviati. Per impostazione predefinita, questa impostazione non è abilitata.

        > [!WARNING]
        > Prima di usare questa opzione, i computer e le reti devono essere configurati per riattivazione LAN.

    - **Livello dettaglio**: specificare il livello di dettaglio per i messaggi di stato segnalati dai computer client.

    **Impostazioni download**: nella scheda Impostazioni download configurare le impostazioni seguenti:

    - Specificare se il client scarica e installa gli aggiornamenti software durante una connessione a una rete lenta o quando usa un percorso di fallback per il contenuto.

    - Specificare se il client dovrà scaricare e installare gli aggiornamenti software da un punto di distribuzione di fallback nel caso in cui il contenuto per tali aggiornamenti non fosse disponibile in un punto di distribuzione preferito.

    - **Consenti ai client di condividere il contenuto con altri client nella stessa subnet**: specificare se consentire l'uso di BranchCache per i download del contenuto. Per altre informazioni su BranchCache, vedere [Concetti di base per la gestione dei contenuti](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).

    - Specificare se far scaricare ai client gli aggiornamenti software da Microsoft Update nel caso in cui gli aggiornamenti non fossero disponibili nei punti di distribuzione.
        > [!IMPORTANT]
        > Non usare questa impostazione per gli aggiornamenti di manutenzione di Windows 10. Almeno fino alla versione 1610 di Configuration Manager non è possibile scaricare gli aggiornamenti di manutenzione di Windows 10 da Microsoft Update.

    - Specificare se consentire ai client di eseguire il download dopo una scadenza dell'installazione quando usano connessioni Internet a consumo. I provider Internet talvolta applicano un addebito per il traffico dati in entrata e in uscita quando si usa una connessione Internet a consumo.

    **Avvisi**: la scheda Avvisi consente di configurare la modalità usata da Configuration Manager e System Center Operations Manager per generare avvisi relativi alla distribuzione.
    - È possibile riesaminare gli avvisi recenti sugli aggiornamenti software dal nodo **Aggiornamenti software** nell'area di lavoro **Raccolta software** .

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni, vedere [Nozioni di base su Configuration Manager come servizio e Windows come servizio](../../core/understand/configuration-manager-and-windows-as-service.md).
