---
title: Come eseguire la distribuzione in un progetto pilota
titleSuffix: Configuration Manager
description: Guida pratica per eseguire la distribuzione in un gruppo pilota di Desktop Analytics.
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 637fbd8e-b8ea-4c7e-95ee-a60a323c496e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 3aa722415248ad9275c6ad065f0120bfe78d3ce4
ms.sourcegitcommit: 8a023e941d90c107c9769a1f7519875a31ef9393
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/03/2020
ms.locfileid: "84311221"
---
# <a name="how-to-deploy-to-pilot-with-desktop-analytics"></a>Come eseguire la distribuzione in un progetto pilota con Desktop Analytics

Uno dei vantaggi di Desktop Analytics è quello di poter identificare l'insieme minimo di dispositivi che consentono la più ampia copertura di fattori. Identifica i fattori ritenuti più importanti per un progetto pilota di aggiornamenti Windows. Assicurarsi che il progetto pilota sia ottimale per poter procedere in modo più rapido e sicuro a distribuzioni di grandi dimensioni in ambiente di produzione.  

[!INCLUDE [Definition of pilot and production](includes/define-pilot-prod.md)]

## <a name="identify-devices"></a>Identificare i dispositivi

Il primo passaggio consiste nell'identificare i dispositivi da includere nel progetto pilota. Desktop Analytics consiglia i dispositivi sulla base dei dati segnalati. È possibile includere o sostituire i dispositivi in questo elenco.

1. Passare al [portale di Desktop Analytics](https://aka.ms/desktopanalytics) e selezionare **Piani di distribuzione** nel gruppo Gestisci.

1. Selezionare un piano di distribuzione.

1. Nel gruppo Preparazione del menu del piano di distribuzione selezionare **Identifica gruppo pilota**.

Verranno visualizzati i dati di Desktop Analytics e il numero di dispositivi che è consigliabile includere per la migliore copertura. Questo algoritmo si basa principalmente sull'uso di app importanti e critiche e su una varietà di configurazioni hardware.

Eseguire le azioni seguenti per l'elenco dei dispositivi consigliati aggiuntivi:

- **Aggiungere tutti i dispositivi alla distribuzione pilota**: tutti i dispositivi consigliati vengono aggiunti al gruppo pilota
- **Aggiungere al gruppo pilota**: vengono aggiunti solo singoli dispositivi
- **Sostituire** i dispositivi specifici del progetto pilota

Quando si aggiungono dispositivi dall'elenco **consigliati** all'elenco **inclusi** della distribuzione pilota, migliorano la copertura e la ridondanza per gli asset critici e importanti nel progetto pilota. Una ridondanza maggiore significa che gli asset con copertura includono un numero statisticamente significativo di dispositivi nel progetto pilota.

## <a name="global-pilot"></a><a name="bkmk_GlobalPilot"></a>Progetto pilota globale

È anche possibile prendere decisioni a livello di sistema relativamente alle raccolte di Configuration Manager da includere o escludere dai progetti pilota. Nel menu principale di Desktop Analytics selezionare **Dispositivo pilota globale** nel gruppo Impostazioni globali.

Se si connettono più gerarchie di Configuration Manager alla stessa istanza di Desktop Analytics, viene aggiunto un nome visualizzato per la gerarchia come prefisso al nome della raccolta nella configurazione pilota globale. Si tratta della proprietà **Nome visualizzato** nella connessione di Desktop Analytics nella console di Configuration Manager.<!-- 4814075 -->

> [!NOTE]
> Il supporto di più gerarchie richiede Configuration Manager versione 1910 o successiva.

- Non includere raccolte che contengono più del 20% del totale dei dispositivi registrati a Desktop Analytics. Se si include una raccolta di grandi dimensioni, nel portale viene visualizzato un avviso. È possibile includere più collezioni piccole senza preavviso, ma occorre essere comunque prudenti riguardo al numero di dispositivi nella propria distribuzione pilota. <!-- 6079184 -->

- Per ottenere consigli pilota accurati per i piani di distribuzione in una gerarchia di Configuration Manager specifica, includere solo le raccolte di tale gerarchia.

### <a name="example"></a>Esempio

- Configurare la connessione di Desktop Analytics in Configuration Manager per fare riferimento alla raccolta **Tutti i sistemi**. Questa azione consente di registrare tutti i client nel servizio.

- Configurare anche raccolte aggiuntive per eseguire la sincronizzazione con Desktop Analytics:

  - Tutti i client Windows 10 (3.000 dispositivi)

  - Tutti i dispositivi IT (200 dispositivi totali, 150 che eseguono Windows 10)

  - Ufficio CEO (20 dispositivi)

- Nelle impostazioni **Dispositivo pilota globale** includere le raccolte **Tutti i client Windows 10**. Escludere la raccolta **Ufficio amministratore delegato**.

- Creare un piano di distribuzione e selezionare la raccolta **Tutti i dispositivi IT** come **Gruppo di destinazione**. Questo piano di distribuzione è destinato solo ai dispositivi del reparto IT.

- L'elenco **Dispositivi pilota inclusi** comprende il subset di dispositivi presenti sia nel **Gruppo di destinazione**: **Tutti i dispositivi IT** che nell'elenco di *inclusione* del Progetto pilota globale: **Tutti i client Windows 10**. Questo elenco comprende 150 dispositivi, perché solo 150 dispositivi della raccolta **Tutti i dispositivi IT** eseguono Windows 10.

- L'elenco **Altri dispositivi consigliati** include un insieme di dispositivi del **Gruppo di destinazione** che offrono massima copertura e ridondanza per le risorse importanti. Desktop Analytics esclude da questo elenco tutti i dispositivi indicati nell'elenco di *esclusione* del progetto pilota globale: **Ufficio amministratore delegato**.

## <a name="address-issues"></a>Risolvere i problemi

Usare il portale di Desktop Analytics per esaminare eventuali problemi segnalati con le risorse che potrebbero bloccare la distribuzione. Quindi approvare, rifiutare o modificare la correzione consigliata. Prima di avviare la distribuzione pilota, è necessario che tutti gli elementi siano contrassegnati con **Pronto** o **Pronto (con correzione)** .

1. Passare al [portale di Desktop Analytics](https://aka.ms/desktopanalytics) e selezionare **Piani di distribuzione** nel gruppo Gestisci.  

2. Selezionare un piano di distribuzione.  

3. Nel gruppo Preparazione del menu Piano di distribuzione selezionare **Preparare il gruppo pilota**.  

4. Nella scheda **App** esaminare le app che richiedono l'input.  

5. Per ogni app, selezionare il nome dell'app. Nel riquadro informazioni esaminare il consiglio e selezionare la decisione di aggiornamento. Se si sceglie **Non riviste** o **Non possibile**, Desktop Analytics non includerà i dispositivi con questa app nella distribuzione pilota. Se si sceglie **Pronto (con correzione)** , usare le **Note di rimedio** per acquisire le azioni da intraprendere per risolvere un problema, ad esempio *reinstallare* o *trovare la versione consigliata del produttore*.

6. Ripetere questa verifica per le altre risorse.  

Per ulteriori informazioni su questo processo di revisione, vedere [Valutazione della compatibilità](compat-assessment.md).

## <a name="create-software"></a>Creare software

Per poter distribuire Windows, è prima necessario creare gli oggetti software in Configuration Manager. Per altre informazioni, vedere [Sequenza di attività per aggiornare Windows 10 sul posto](../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md).

## <a name="deploy-to-pilot-devices"></a>Distribuire nei dispositivi pilota

Configuration Manager usa i dati di Desktop Analytics per creare raccolte per le distribuzioni pilota e le distribuzioni in ambiente di produzione. Queste raccolte si trovano nella cartella **Piani di distribuzione** del nodo **Raccolte dispositivi** nell'area di lavoro **Asset e conformità**.

> [!IMPORTANT]
> Le raccolte sono gestite da Configuration Manager per i piani di distribuzione di Desktop Analytics. Le modifiche manuali non sono supportate. Se si elimina una di queste raccolte, Desktop Analytics non funziona ed è necessario [connettersi a Configuration Manager](connect-configmgr.md) nuovamente.<!--7208090-->

Per assicurarsi che i dispositivi siano integri dopo ogni fase di distribuzione, usare la procedura seguente per creare una distribuzione in più fasi integrata di Desktop Analytics:

1. Nella console di Configuration Manager passare a **Raccolta software**, espandere **Manutenzione di Desktop Analytics** e selezionare il nodo **Piani di distribuzione**.  

2. Selezionare il piano di distribuzione, quindi scegliere **Dettagli del piano di distribuzione** nella barra multifunzione.  

3. Selezionare **Crea una distribuzione in più fasi** nella barra multifunzione. Questa azione avvierà la procedura guidata Crea una distribuzione in più fasi.

    > [!Tip]  
    > Se si vuole creare una distribuzione della sequenza di attività classica solo per la raccolta pilota, selezionare **Distribuisci** nel riquadro **Stato della distribuzione pilota**. Questa azione avvierà la Distribuzione guidata del software. Per altre informazioni, vedere [Deploy a task sequence](../osd/deploy-use/deploy-a-task-sequence.md).  

4. Immettere un nome per la distribuzione e selezionare la sequenza di attività da usare. Usare l'opzione **Crea automaticamente una distribuzione predefinita in due fasi**, quindi configurare le raccolte seguenti:  

    - **Prima raccolta**: trovare e selezionare la raccolta **Pilota** per questo piano di distribuzione. La convenzione di denominazione standard per questa raccolta è `<deployment plan name> (Pilot)`.

    - **Seconda raccolta**: trovare e selezionare la raccolta **Produzione** per questo piano di distribuzione. La convenzione di denominazione standard per questa raccolta è `<deployment plan name> (Production)`.

    > [!Note]  
    > Con l'integrazione di Desktop Analytics, Configuration Manager crea automaticamente raccolte pilota e di produzione per il piano di distribuzione. Prima di poterle usare, può essere necessario attendere che venga eseguita la sincronizzazione di queste raccolte. Per altre informazioni, vedere [Risolvere i problemi - Latenza dei dati](troubleshooting.md#data-latency).<!-- 4984639 -->
    >
    > Queste raccolte sono riservate ai dispositivi del piano di distribuzione di Desktop Analytics. Le modifiche manuali a queste raccolte non sono supportate.<!-- 3866460, SCCMDocs-pr 3544 -->  

5. Completare la procedura guidata per configurare la distribuzione in più fasi. Per altre informazioni, vedere [Creare distribuzioni in più fasi](../osd/deploy-use/create-phased-deployment-for-task-sequence.md).

    > [!Note]  
    > Usare l'impostazione predefinita **Inizia automaticamente questa fase dopo un periodo di differimento (in giorni)** . Per avviare la seconda fase, è necessario soddisfare i criteri seguenti:
    >
    > 1. La prima fase soddisfa il criterio **Percentuale di esiti positivi della distribuzione** per essere ritenuta completata. Questa impostazione viene configurata nella distribuzione in più fasi.
    > 1. È necessario rivedere e decidere sugli aggiornamenti in Desktop Analytics per contrassegnare con *Pronto* le risorse importanti e critiche. Per altre informazioni, vedere [Esaminare le risorse che necessitano di una decisione di aggiornamento](deploy-prod.md#bkmk_review).
    > 1. Desktop Analytics esegue la sincronizzazione delle raccolte di Configuration Manager con tutti i dispositivi di produzione che soddisfano i criteri contrassegnati con *Pronto*.

> [!Important]  
> Queste raccolte continuano a essere sincronizzate quando viene modificata l'appartenenza. Ad esempio, se si identifica un problema con una risorsa e lo si contrassegna con **Non possibile**, i dispositivi con la risorsa interessata non soddisfano più i criteri *Pronto*. Questi dispositivi verranno eliminati dalla raccolta di distribuzioni in ambiente di produzione.

## <a name="monitor"></a>Monitoraggio

### <a name="configuration-manager-console"></a>Console di Configuration Manager

Aprire il piano di distribuzione. Il riquadro **Preparazione delle decisioni di aggiornamento - Stato generale** offre un riepilogo dello stato del piano di distribuzione. Lo stato riguarda sia le raccolte del progetto pilota sia le raccolte di produzione. I dispositivi possono essere suddivisi nelle categorie seguenti:

- **Aggiornato**: i dispositivi sono stati aggiornati alla versione di destinazione di Windows per questo piano di distribuzione

- **La decisione di aggiornamento è stata completata**: viene visualizzato uno degli stati seguenti:

  - Dispositivi con risorse importanti contrassegnati con **Pronto** o **Pronto (con correzione)**

  - Lo stato del dispositivo è **Bloccato**, [**Sostituire il dispositivo**](about-deployment-plans.md#plan-assets) o **Reinstalla il dispositivo**

- **Non rivisto**: dispositivi con risorse contrassegnate con **Non riviste** o **Revisione in corso**

Lo stato del dispositivo viene aggiornato nei riquadri **Stato della distribuzione pilota** e **Stato ambiente di produzione** con le azioni seguenti:

- Vengono apportate modifiche alla valutazione della compatibilità
- I dispositivi vengono aggiornati alla versione di destinazione di Windows
- La distribuzione è in stato di avanzamento

È anche possibile usare il monitoraggio della distribuzione di Configuration Manager come una qualsiasi altra distribuzione della sequenza di attività. Per altre informazioni, vedere [Monitorare le distribuzioni del sistema operativo](../osd/deploy-use/monitor-operating-system-deployments.md).

### <a name="desktop-analytics-portal"></a>Portale di Desktop Analytics

Usare il [portale di Desktop Analytics](https://aka.ms/desktopanalytics) per visualizzare lo stato di un piano di distribuzione. Selezionare il piano di distribuzione, quindi selezionare **Panoramica del piano**.

![Screenshot della panoramica del piano di distribuzione in Desktop Analytics](media/deployment-plan-overview.png)

Selezionare il riquadro **Pilota**. Viene riepilogato lo stato corrente della distribuzione pilota. In questo riquadro vengono visualizzati anche i dati relativi al numero di dispositivi non avviati, in corso, completati o che restituiscono problemi.

Nell'area dettaglio Pilota a destra vengono anche elencati tutti i dispositivi che segnalano errori o altri problemi. Per ottenere i dettagli del problema segnalato, selezionare **Esamina**. Questa azione modifica la visualizzazione aprendo la pagina **Stato distribuzione**.

Nella pagina **Stato distribuzione** sono elencati i dispositivi nelle categorie seguenti:

- Non avviato
- In corso
- Completed
- Richiede attenzione - Dispositivi
- Richiede attenzione - Problemi

Le categorie **Richiede attenzione** visualizzano le stesse informazioni, ma con un ordine diverso.

Selezionare un elenco specifico in una delle due visualizzazioni per ottenere più dettagli sul problema rilevato.

Quando si risolvono questi problemi di distribuzione, il dashboard continua a visualizzare lo stato dei dispositivi. Si aggiorna man mano che i dispositivi passano da **Richiede attenzione** a **Operazione completata**.

## <a name="next-steps"></a>Passaggi successivi

Lasciare in esecuzione il progetto pilota per un periodo di tempo sufficiente a raccogliere i dati operativi. Invitare gli utenti dei dispositivi pilota a testare le app.

Quando la distribuzione pilota soddisfa i criteri per un esito positivo, passare all'articolo successivo per eseguire la distribuzione nell'ambiente di produzione.
> [!div class="nextstepaction"]  
> [Distribuire nell'ambiente di produzione](deploy-prod.md)  
