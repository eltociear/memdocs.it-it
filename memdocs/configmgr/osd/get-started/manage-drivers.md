---
title: Gestire i driver
titleSuffix: Configuration Manager
description: Usare il catalogo dei driver di Configuration Manager per importare i driver dei dispositivi, raggruppare i driver in pacchetti e distribuire i pacchetti ai punti di distribuzione.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 84802d55-112e-4f7f-9a48-74a80d91a0f4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 09cf1b7ee1859043e0839d5a1b5db3518c602b74
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124432"
---
# <a name="manage-drivers-in-configuration-manager"></a>Gestire i driver in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Configuration Manager include un catalogo di driver che è possibile usare per gestire i driver di dispositivo Windows presenti nell'ambiente di Configuration Manager. Usare il catalogo dei driver per importare i driver dei dispositivi in Configuration Manager, per raggrupparli in pacchetti e per distribuire tali pacchetti ai punti di distribuzione. I driver di dispositivo possono essere usati per l'installazione del sistema operativo completo nel computer di destinazione e quando si usa Windows PE in un'immagine d'avvio. I driver di dispositivo Windows sono costituiti da un file di informazioni per l'installazione (INF) ed eventuali file aggiuntivi necessari per il supporto del dispositivo. Quando si distribuisce un sistema operativo, Configuration Manager ottiene le informazioni su piattaforma e hardware per il dispositivo dal file INF. 



## <a name="driver-categories"></a><a name="BKMK_DriverCategories"></a> Categorie di driver

Quando si importano i driver di dispositivo, è possibile assegnarli a una categoria. Le categorie di driver di dispositivo consentono di raggruppare nel catalogo i driver utilizzati in modo analogo. Ad esempio, impostare tutti i driver di dispositivo della scheda di rete su una categoria specifica. Quando si crea una sequenza di attività che include il passaggio [Applica automaticamente i driver](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers), specificare quindi una categoria di driver di dispositivo. Configuration Manager analizza l'hardware e seleziona i driver applicabili dalla categoria per eseguire un'installazione di appoggio sul sistema per l'uso da parte dell'installazione di Windows.  



## <a name="driver-packages"></a><a name="BKMK_ManagingDriverPackages"></a> Pacchetti driver

Raggruppare driver di dispositivo simili in pacchetti per semplificare le distribuzioni del sistema operativo. Ad esempio, creare un pacchetto driver per ogni produttore di computer nella rete. È possibile creare un pacchetto driver durante l'importazione dei driver nel catalogo direttamente nel nodo **Pacchetti driver**. Dopo aver creato un pacchetto driver, distribuirlo ai punti di distribuzione. I computer client di Configuration Manager possono quindi installare i driver come richiesto. 

Considerare i punti seguenti:  

- Quando si crea un pacchetto driver, il percorso di origine del pacchetto deve puntare a una condivisione di rete vuota che non viene usata da un altro pacchetto driver. Il provider SMS deve avere le autorizzazioni **Controllo completo** per tale percorso.  

- Quando si aggiungono driver di dispositivo a un pacchetto driver, Configuration Manager li copia nel percorso di origine del pacchetto. È possibile aggiungere a un pacchetto driver solo i driver di dispositivo importati e abilitati nel catalogo.  

- È possibile copiare un sottoinsieme di driver di dispositivo da un pacchetto driver esistente. Creare prima di tutto un nuovo pacchetto driver. Aggiungere quindi il sottoinsieme di driver di dispositivo al nuovo pacchetto e quindi distribuire il nuovo pacchetto a un punto di distribuzione.  

- Quando si usano sequenze di attività per installare i driver, creare pacchetti driver contenenti meno di 500 driver di dispositivo.


### <a name="create-a-driver-package"></a><a name="BKMK_CreatingDriverPackages"></a> Creare un pacchetto driver  

> [!IMPORTANT]  
> Per creare un pacchetto driver, è necessario disporre di una cartella di rete vuota non usata da un altro pacchetto driver. Nella maggior parte dei casi, creare una nuova cartella prima di avviare questa procedura.  

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**. Espandere **Sistemi operativi** e quindi selezionare il nodo **Pacchetti driver**.  

2. Nella scheda **Home** della barra multifunzione selezionare **Crea pacchetto driver** nel gruppo **Crea**.  

3. Nella casella **Nome** specificare un nome descrittivo per il pacchetto driver.  

4. Immettere un **Commento** facoltativo per il pacchetto driver. Usare questa descrizione per fornire informazioni sul contenuto o sullo scopo del pacchetto driver.  

5. Nella casella **Percorso** specificare una cartella di origine vuota per il pacchetto driver. Ogni pacchetto driver deve utilizzare una cartella univoca. Questo percorso è richiesto come percorso di rete.  

   > [!IMPORTANT]  
   > L'account del server del sito deve avere le autorizzazioni **Controllo completo** per la cartella di origine specificata.  

Il nuovo pacchetto driver non contiene alcun driver. Il passaggio successivo consente di aggiungere driver al pacchetto.  

Se il nodo **Pacchetti driver** contiene diversi pacchetti, è possibile aggiungere cartelle al nodo per separare i pacchetti in gruppi logici.  


### <a name="additional-actions-for-driver-packages"></a><a name="BKMK_PackageActions"></a> Azioni aggiuntive per i pacchetti driver  

Quando si selezionano uno o più pacchetti driver dal nodo **Pacchetti driver** è possibile eseguire azioni aggiuntive per gestire i pacchetti driver. 


#### <a name="create-prestage-content-file"></a>Crea file di contenuto di pre-installazione
Crea file che possono essere usati per importare manualmente il contenuto e i metadati associati. Utilizzare il contenuto pre-installazione quando si dispone di larghezza di banda di rete bassa tra il server del sito e i punti di distribuzione in cui è archiviato il pacchetto driver.

#### <a name="delete"></a>Elimina
Rimuove il pacchetto driver dal nodo **Pacchetti driver** .

#### <a name="distribute-content"></a>Distribuisci contenuto
Distribuisce il pacchetto driver nei punti di distribuzione, nei gruppi di punti di distribuzione e nei gruppi di punti di distribuzione associati alle raccolte.

#### <a name="manage-access-accounts"></a>Gestione account di accesso
Aggiunge, modifica o rimuove gli account di accesso per il pacchetto driver.

Per altre informazioni sugli account di accesso al pacchetto, vedere [Account usati in Configuration Manager](../../core/plan-design/hierarchy/accounts.md).

#### <a name="move"></a>Sposta
Sposta il pacchetto driver in un'altra cartella del nodo **Pacchetti driver** .

#### <a name="update-distribution-points"></a>Aggiorna punti di distribuzione
Aggiorna il pacchetto driver del dispositivo in tutti i punti di distribuzione in cui è archiviato il pacchetto. Questa azione copia solo il contenuto modificato dopo l'ultima distribuzione.

#### <a name="properties"></a>Proprietà
Apre la finestra di dialogo **Proprietà**. Esaminare e modificare il contenuto e le proprietà del driver. Ad esempio, modificare il nome e la descrizione del driver, abilitarlo o disabilitarlo e specificare le piattaforme su cui può essere eseguito. 

<!--3607716, fka 1358270-->
A partire dalla versione 1810, i pacchetti driver hanno campi di metadati per **Produttore** e **Modello**. Usare questi campi per contrassegnare i pacchetti driver con informazioni utili per la manutenzione generale o per identificare driver precedenti e duplicati che è possibile eliminare. Nella scheda **Generale** selezionare un valore esistente dagli elenchi a discesa o immettere una stringa per creare una nuova voce.

Nel nodo **Pacchetti driver** questi campi sono visualizzati nell'elenco come le colonne **Produttore del driver** e **Modello del driver**. Possono anche essere usati come criteri di ricerca.

A partire dalla versione 1906, usare questi attributi per la memorizzazione anticipata nella cache dei contenuti di un client. Per altre informazioni, vedere [Configurare la pre-cache del contenuto](../deploy-use/configure-precache-content.md).<!--4224642-->  




## <a name="device-drivers"></a><a name="BKMK_DeviceDrivers"></a> Driver di dispositivo

È possibile installare i driver in computer di destinazione senza includerli nell'immagine del sistema operativo che viene distribuita. Configuration Manager offre un catalogo dei driver che contiene i riferimenti a tutti i driver importati in Configuration Manager. Il catalogo dei driver si trova nell'area di lavoro **Raccolta software** ed è costituito da due nodi: **Driver** e **Pacchetti driver**. Nel nodo **Driver** sono elencati tutti i driver importati nel catalogo dei driver.  


### <a name="import-device-drivers-into-the-driver-catalog"></a><a name="BKMK_ImportDrivers"></a> Importare i driver di dispositivo nel catalogo dei driver  

Prima di poter usare un driver quando si distribuisce un sistema operativo, importarlo nel catalogo dei driver. Per facilitare la gestione, importare solo i driver che si intende installare come parte delle distribuzioni del sistema operativo. Archiviare più versioni di driver nel catalogo dei driver per aggiornare in modo semplice i driver esistenti quando cambiano i requisiti dei dispositivi hardware nella rete.  

Come parte del processo di importazione per il driver di dispositivo, Configuration Manager legge le proprietà seguenti riguardanti il driver:
- Provider
- Class
- Version
- Firma
- Hardware supportato
- Informazioni sulla piattaforma supportata

Per impostazione predefinita, il driver viene denominato come il primo dispositivo hardware supportato. È possibile rinominare il driver di dispositivo in un secondo momento. L'elenco di piattaforme supportate si basa sulle informazioni contenute nel file INF del driver. Dal momento che l'accuratezza di queste informazioni può variare, è necessario verificare manualmente che il driver sia supportato dopo l'importazione nel catalogo.  

Dopo aver importato i driver di dispositivo nel catalogo, aggiungerli ai pacchetti driver o ai pacchetti di immagini d'avvio.  

> [!IMPORTANT]  
> Non è possibile importare i driver di dispositivo direttamente in una sottocartella del nodo **Driver**. Per importare un driver di dispositivo in una sottocartella, è innanzitutto necessario importare il driver di dispositivo nel nodo **Driver** , quindi spostare il driver nella sottocartella.  


#### <a name="process-to-import-windows-device-drivers-into-the-driver-catalog"></a>Processo per importare i driver di dispositivo Windows nel catalogo dei driver  

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**. Espandere **Sistemi operativi** e selezionare il nodo **Driver**.  

2. Nella scheda **Home** della barra multifunzione, nel gruppo **Crea**, selezionare **Importa driver** per avviare **Importazione guidata nuovo driver**.  

3. Nella pagina **Trova driver** specificare le opzioni seguenti:  

    - **Importa tutti i driver presenti nel percorso di rete seguente (UNC)** : Per importare tutti i driver di dispositivo in una cartella specifica, specificare il relativo percorso di rete. Ad esempio: `\\servername\share\folder`.  

        > [!NOTE]  
        > Se sono presenti numerose sottocartelle e numerosi file INF di driver, questo processo può richiedere tempo.  

    - **Importa un driver specifico**: Per importare un driver specifico da una cartella, specificare il percorso di rete del file INF del driver di dispositivo Windows.  

    - **Specifica l'opzione per i driver duplicati**: Selezionare la modalità di gestione delle categorie di driver da parte di Configuration Manager quando si importa un driver di dispositivo duplicato.  
        - **Importa il driver e aggiungi una nuova categoria alle categorie esistenti**  
        - **Importa il driver e mantieni le categorie esistenti**  
        - **Importa il driver e sovrascrivi le categorie esistenti**  
        - **Non importare il driver**  

    > [!IMPORTANT]  
    > Quando si importano i driver, se il server del sito non dispone dell'autorizzazione **Lettura** per la cartella, l'importazione non riesce.  

4. Nella pagina **Dettagli driver** specificare le opzioni seguenti:  

    - **Nascondi driver non inclusi in una classe di archiviazione o di rete (per immagini d'avvio)** : Usare questa impostazione per visualizzare solo i driver di archiviazione e rete. Questa opzione consente di nascondere altri driver in genere non necessari per le immagini d'avvio, ad esempio i driver video o quelli per modem.  

    - **Nascondi driver senza firma digitale**: Microsoft consiglia di usare solo i driver firmati digitalmente  

    - Nell'elenco dei driver, selezionare i driver che si desidera importare nel catalogo dei driver.  

    - **Abilita questi driver e consenti ai computer di installarli**: selezionare questa impostazione per consentire ai computer di installare i driver di dispositivo. Questa opzione è attivata per impostazione predefinita.  

        > [!IMPORTANT]  
        > Se un driver di dispositivo causa un problema o si vuole sospendere l'installazione di un driver di dispositivo, disabilitarlo durante l'importazione. È anche possibile disabilitare i driver dopo averli importati.  

    - Per assegnare i driver di dispositivo a una categoria amministrativa per l'applicazione di filtri, ad esempio "Desktop" o "Notebook", selezionare **Categorie**. Scegliere quindi una categoria esistente oppure creare una nuova categoria. Usare le categorie per controllare i driver di dispositivo che vengono applicati dal passaggio della sequenza di attività [Applica automaticamente i driver](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers).  

5. Nella pagina **Aggiungi driver ai pacchetti** scegliere se aggiungere i driver a un pacchetto.  

    - Selezionare i pacchetti driver utilizzati per distribuire i driver di dispositivo.  

        Se necessario, selezionare **Nuovo pacchetto** per creare un nuovo pacchetto driver. Quando viene creato un nuovo pacchetto driver, è necessario specificare una condivisione di rete non usata da altri pacchetti driver.  

    - Se il pacchetto è già stato distribuito ai punti di distribuzione, selezionare **Sì** nella finestra di dialogo per aggiornare le immagini d'avvio nei punti di distribuzione. Fino a quando i driver di dispositivo non vengono distribuiti ai punti di distribuzione non è possibile usarli. Se si seleziona **No**, eseguire l'azione **Aggiorna punto di distribuzione** prima di usare l'immagine d'avvio. Se il pacchetto driver non è mai stato distribuito, è necessario usare l'azione **Distribuisci contenuto** nel nodo **Pacchetti driver**.  

6. Nella pagina **Aggiungi driver alle immagini d'avvio** scegliere se aggiungere i driver di dispositivo alle immagini d'avvio esistenti.  

    > [!NOTE]  
    > Aggiungere solo driver di archiviazione e rete alle immagini d'avvio.  

    - Selezionare **Sì** nella finestra di dialogo per aggiornare le immagini d'avvio nei punti di distribuzione. Fino a quando i driver di dispositivo non vengono distribuiti ai punti di distribuzione non è possibile usarli. Se si seleziona **No**, eseguire l'azione **Aggiorna punto di distribuzione** prima di usare l'immagine d'avvio. Se il pacchetto driver non è mai stato distribuito, è necessario usare l'azione **Distribuisci contenuto** nel nodo **Pacchetti driver**.  

    - Configuration Manager segnala se l'architettura per uno o più driver non corrisponde all'architettura delle immagini d'avvio selezionate. In caso di non corrispondenza, selezionare **OK**. Tornare alla pagina **Dettagli driver** e deselezionare i driver che non corrispondono all'architettura dell'immagine d'avvio selezionata. Ad esempio, se si seleziona un'immagine di avvio x64 e x86, tutti i driver devono supportare entrambe le architetture. Se si seleziona un'immagine di avvio x64, tutti i driver devono supportare l'architettura x64.  

        > [!NOTE]  
        > - L'architettura è basata su quella indicata nel file con estensione inf fornito dal produttore.  
        > - Se un driver segnala che supporta entrambe le architetture, è possibile importarlo in un'immagine d'avvio.  

    - Configuration Manager segnala se si aggiungono driver di dispositivo che non sono driver di rete o archiviazione a un'immagine d'avvio. Nella maggior parte dei casi, non sono necessari per l'immagine d'avvio. Selezionare **Sì** per aggiungere i driver all'immagine d'avvio oppure **No** per tornare indietro e modificare la selezione dei driver.  

    - Configuration Manager segnala se uno o più driver selezionati non includono una firma digitale corretta. Selezionare **Sì** per continuare o selezionare **No** per tornare indietro e apportare modifiche alla selezione dei driver.  

7. Completare la procedura guidata.  


### <a name="manage-device-drivers-in-a-driver-package"></a><a name="BKMK_ModifyDriverPackage"></a> Gestire i driver di dispositivo in un pacchetto driver  

Utilizzare le seguenti procedure per modificare i pacchetti driver e le immagini di avvio. Per aggiungere o rimuovere un driver, individuarlo prima di tutto nel nodo **Driver**. Modificare quindi i pacchetti o le immagini d'avvio a cui è associato il driver selezionato.  

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**. Espandere **Sistemi operativi** e quindi selezionare il nodo **Driver**.  

2. Selezionare i driver di dispositivo che si vuole aggiungere a un pacchetto driver.  

3. Nella scheda **Home** della barra multifunzione, nel gruppo **Driver**, selezionare **Modifica** e quindi scegliere **Pacchetti driver**.  

4. Per aggiungere un driver di dispositivo, selezionare la casella di controllo dei pacchetti driver a cui si desidera aggiungere i driver di dispositivo. Per rimuovere un driver di dispositivo, deselezionare la casella di controllo dei pacchetti driver da cui si desidera rimuovere il driver di dispositivo.  

    Se si aggiungono driver di dispositivo associati a pacchetti driver, è possibile creare facoltativamente un nuovo pacchetto. Selezionare **Nuovo pacchetto**. Verrà visualizzata la finestra di dialogo **Nuovo pacchetto driver**.  

5. Se il pacchetto è già stato distribuito ai punti di distribuzione, selezionare **Sì** nella finestra di dialogo per aggiornare le immagini d'avvio nei punti di distribuzione. Fino a quando i driver di dispositivo non vengono distribuiti ai punti di distribuzione non è possibile usarli. Se si seleziona **No**, eseguire l'azione **Aggiorna punto di distribuzione** prima di usare l'immagine d'avvio. Se il pacchetto driver non è mai stato distribuito, è necessario usare l'azione **Distribuisci contenuto** nel nodo **Pacchetti driver**. Prima che i driver siano disponibili, è necessario aggiornare il pacchetto driver nei punti di distribuzione.  

    Selezionare **OK** al termine.  


### <a name="manage-device-drivers-in-a-boot-image"></a><a name="BKMK_ManageDriversBootImage"></a> Gestire i driver di dispositivo in un'immagine di avvio  

È possibile aggiungere alle immagini d'avvio i driver di dispositivo Windows importati nel catalogo. Quando si aggiungono driver di dispositivo a un'immagine di avvio, utilizzare le seguenti linee guida:  

- Aggiungere solo driver di archiviazione e rete alle immagini d'avvio. Altri tipi di driver non sono in genere necessari in Windows PE. I driver superflui aumentano inutilmente le dimensioni dell'immagine d'avvio.  

- Aggiungere solo driver di dispositivo per Windows 10 a un'immagine d'avvio. La versione richiesta di Windows PE si basa su Windows 10.  

- Assicurarsi di usare il driver di dispositivo corretto per l'architettura dell'immagine d'avvio. Non aggiungere un driver di dispositivo x86 a un'immagine d'avvio x64.  

#### <a name="process-to-modify-the-device-drivers-associated-with-a-boot-image"></a>Processo per modificare i driver di dispositivo associati a un'immagine d'avvio  

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**. Espandere **Sistemi operativi** e quindi selezionare il nodo **Driver**.  

2. Selezionare i driver di dispositivo che si vuole aggiungere al pacchetto driver.  

3. Nella scheda **Home** della barra multifunzione, nel gruppo **Driver**, selezionare **Modifica** e quindi scegliere **Immagini d'avvio**.  

4. Per aggiungere un driver di dispositivo, selezionare la casella di controllo dell'immagine di avvio a cui si desidera aggiungere i driver di dispositivo. Per rimuovere un driver di dispositivo, deselezionare la casella di controllo dell'immagine di avvio da cui si desidera rimuovere il driver di dispositivo.  

5. Se non si vogliono aggiornare i punti di distribuzione in cui è archiviata l'immagine d'avvio, deselezionare la casella di controllo **Al termine aggiorna punti di distribuzioni**. Per impostazione predefinita, i punti di distribuzione vengono aggiornati quando viene aggiornata l'immagine di avvio.  

    - Selezionare **Sì** nella finestra di dialogo per aggiornare le immagini d'avvio nei punti di distribuzione. Fino a quando i driver di dispositivo non vengono distribuiti ai punti di distribuzione non è possibile usarli. Se si seleziona **No**, eseguire l'azione **Aggiorna punto di distribuzione** prima di usare l'immagine d'avvio. Se il pacchetto driver non è mai stato distribuito, è necessario usare l'azione **Distribuisci contenuto** nel nodo **Pacchetti driver**.  

    - Configuration Manager segnala se l'architettura per uno o più driver non corrisponde all'architettura delle immagini d'avvio selezionate. In caso di non corrispondenza, selezionare **OK**. Tornare alla pagina **Dettagli driver** e deselezionare i driver che non corrispondono all'architettura dell'immagine d'avvio selezionata. Ad esempio, se si seleziona un'immagine di avvio x64 e x86, tutti i driver devono supportare entrambe le architetture. Se si seleziona un'immagine di avvio x64, tutti i driver devono supportare l'architettura x64.  

        > [!NOTE]
        > - L'architettura è basata su quella indicata nel file con estensione inf fornito dal produttore.  
        > - Se un driver segnala che supporta entrambe le architetture, è possibile importarlo in un'immagine di avvio.  

    - Configuration Manager segnala se si aggiungono driver di dispositivo che non sono driver di rete o archiviazione a un'immagine d'avvio. Nella maggior parte dei casi, non sono necessari per l'immagine d'avvio. Selezionare **Sì** per aggiungere i driver all'immagine d'avvio oppure **No** per tornare indietro e modificare la selezione dei driver.  

    - Configuration Manager segnala se uno o più driver selezionati non includono una firma digitale corretta. Selezionare **Sì** per continuare o selezionare **No** per tornare indietro e apportare modifiche alla selezione dei driver.  


### <a name="additional-actions-for-device-drivers"></a><a name="BKMK_DriverActions"></a> Azioni aggiuntive per i driver di dispositivo  

È possibile eseguire azioni aggiuntive per gestire i driver quando li si selezione nel nodo **Driver**.  

#### <a name="categorize"></a>Categorizza
Consente di cancellare, gestire o impostare una categoria amministrativa per i driver selezionati.

#### <a name="delete"></a>Elimina
Rimuove il driver dal nodo **Driver** e anche dai punti di distribuzione associati.

#### <a name="disable"></a>Disabilitato
Impedisce l'installazione del driver. Questa azione disabilita temporaneamente il driver. La sequenza di attività non può installare un driver disabilitato quando si distribuisce un sistema operativo. 

> [!Note]  
> Questa azione impedisce solo l'installazione dei driver con il passaggio della sequenza di attività **Applica automaticamente i driver**.

#### <a name="enable"></a>Abilitare
Consente alle sequenze di attività e ai computer client di Configuration Manager di installare il driver di dispositivo durante la distribuzione del sistema operativo.

#### <a name="move"></a>Sposta
Sposta il driver di dispositivo in un'altra cartella del nodo **Driver** .

#### <a name="properties"></a>Proprietà
Apre la finestra di dialogo **Proprietà**. Verificare e modificare le proprietà del driver. Ad esempio, modificare il nome e descrizione, abilitarlo o disabilitarlo e specificare le piattaforme su cui è possibile eseguirlo in.



## <a name="use-task-sequences-to-install-drivers"></a><a name="BKMK_TSDrivers"></a> Usare le sequenze di attività per installare i driver  

Usare le sequenze di attività per automatizzare la modalità di distribuzione del sistema operativo. Ogni passaggio della sequenza di attività può eseguire un'azione specifica, ad esempio l'installazione di un driver. È possibile usare i due passaggi di sequenza di attività seguenti per installare i driver di dispositivo quando si distribuisce un sistema operativo:  

- [Applica automaticamente i driver](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers): Questo passaggio consente di associare e installare automaticamente i driver di dispositivo all'interno della distribuzione di un sistema operativo. È possibile configurare il passaggio della sequenza di attività per installare solo il driver con la corrispondenza migliore per ogni dispositivo hardware rilevato. In alternativa, specificare che il passaggio include l'installazione di tutti i driver compatibili per ogni dispositivo hardware rilevato e quindi consentire al programma di installazione di Windows di scegliere il driver migliore. È anche possibile specificare una categoria di driver per limitare i driver disponibili per questo passaggio.  

- [Applica pacchetto di driver](../understand/task-sequence-steps.md#BKMK_ApplyDriverPackage): Questo passaggio consente di rendere disponibili tutti i driver di dispositivo in un pacchetto driver specifico per l'installazione di Windows. Nei pacchetti driver specificati l'installazione di Windows cerca i driver di dispositivo necessari. Quando si creano supporti autonomi, è necessario usare questo passaggio per installare i driver di dispositivo.  

Quando si usano questi passaggi della sequenza di attività, è anche possibile specificare la modalità di installazione dei driver nel computer in cui viene distribuito il sistema operativo. Per altre informazioni, vedere [Gestire le sequenze di attività per automatizzare le attività](../deploy-use/manage-task-sequences-to-automate-tasks.md).  



## <a name="driver-reports"></a><a name="BKMK_DriverReports"></a> Report per i driver  

È possibile utilizzare diversi report nella categoria di report **Gestione driver** per determinare informazioni generali sui driver di dispositivo nel catalogo. Per altre informazioni sui report, vedere [Introduzione ai report](../../core/servers/manage/introduction-to-reporting.md).

