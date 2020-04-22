---
title: Gestire gli aggiornamenti
titleSuffix: Configuration Manager
description: Gestire gli aggiornamenti distribuiti e creati con System Center Updates Publisher
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: cd64994c-b426-4465-96cd-54b0edc2778d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d2cb1d1547c23357adbaa26e649e4e22a78e0f39
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700189"
---
# <a name="manage-software-updates-in-updates-publisher"></a>Distribuire e gestire gli aggiornamenti software

*Si applica a: System Center Updates Publisher*     

In System Center Updates Publisher l'**area di lavoro Aggiornamenti** viene usata per gestire le aggregazioni e gli aggiornamenti software importati nel repository.  

Le attività di gestione includono la duplicazione, la modifica, la cancellazione o la riattivazione di aggiornamenti e aggregazioni, nonché l'assegnazione di aggiornamenti e aggregazioni alla pubblicazione. È inoltre possibile esportare cataloghi personalizzati per usarli con le altre installazioni di Updates Publisher.

Per ottenere aggiornamenti che è possibile gestire, effettuare le operazioni seguenti:
-  [Aggiungere un catalogo di aggiornamenti](updates-publisher-catalogs.md#add-software-update-catalogs) all'installazione di Updates Publisher
-  [Importare](updates-publisher-catalogs.md#import-updates) gli aggiornamenti dal catalogo nel repository.

È anche possibile [creare aggiornamenti personalizzati](create-updates-with-updates-publisher.md).



## <a name="create-a-duplicate-of-an-update"></a>Creare un duplicato di un aggiornamento
È possibile creare duplicati, o copie, degli aggiornamenti presenti nel repository. È quindi possibile modificare la copia anziché l'aggiornamento originale. Non è possibile creare copie di aggregazioni di aggiornamenti.

To creare una copia, selezionare un aggiornamento nell'**area di lavoro Aggiornamenti** e quindi scegliere **Duplica**. La copia dell'aggiornamento viene visualizzata nella stessa posizione all'interno dell'area di lavoro Aggiornamenti, con la dicitura *Copy of* (Copia di) aggiunta al nome.

Una nuova copia ha lo stato **Unexpired** (Non scaduto) e mantiene le impostazioni dell'originale.

## <a name="edit-updates-and-bundles"></a>Modificare aggiornamenti e aggregazioni
È possibile selezionare aggiornamenti e aggregazioni presenti nel repository per modificarli.

Nell'**area di lavoro Aggiornamenti** selezionare un aggiornamento o un'aggregazione e quindi selezionare **Modifica** nella scheda **Home** per aprire la Modifica guidata. Per gli aggiornamenti e le aggregazioni sono disponibili procedure guidate separate, ma strettamente correlate, che presentano le stesse opzioni della [Creazione guidata aggiornamento](create-updates-with-updates-publisher.md#use-the-create-update-wizard) o della [Creazione guidata aggregazione](create-updates-with-updates-publisher.md#use-the-create-bundle-wizard).

Quando si apportano modifiche, è possibile cambiare qualsiasi dettaglio riguardante l'aggiornamento o l'aggregazione così da consentirne l'utilizzo nell'ambiente in uso. È possibile, ad esempio, modificare le regole di precedenza o applicabilità oppure cambiare la lingua. È inoltre possibile cambiare il prodotto e il fornitore per spostare l'aggiornamento o l'aggregazione in una cartella personalizzata, in modo da raggruppare gli aggiornamenti per uso personale.

## <a name="assign-updates-and-bundles-to-a-publication"></a>Assegnare aggiornamenti e aggregazioni a una pubblicazione
È possibile selezionare aggiornamenti e aggregazioni nell'**area di lavoro Aggiornamenti** e quindi scegliere **Assegna** nella scheda **Home** della barra multifunzione per aggiungerli a una pubblicazione. Questa operazione avvia l'**Assegnazione guidata aggiornamenti software**.
-  Per informazioni su come selezionare e pubblicare aggiornamenti e aggregazioni come singola attività, vedere [Pubblicare aggiornamenti e aggregazioni](#publish-updates-and-bundles-from-the-updates-workspace).
-  Per informazioni su come gestire gruppi di aggiornamenti e aggregazioni come singolo oggetto, vedere [Manage publications](updates-publisher-publications.md) (Gestire le pubblicazioni). Dopo aver assegnato gli aggiornamenti a una pubblicazione, è possibile gestirla. La pubblicazione include tutti gli aggiornamenti che le sono stati assegnati.

Quando si assegnano aggiornamenti a una pubblicazione, tenere presente quanto segue:

-   È possibile includere nella stessa pubblicazione aggregazioni e aggiornamenti sia scaduti che non scaduti.

-   Specificare il tipo di pubblicazione:

    -   **Full Content** (Contenuto completo): l'intero contenuto dell'aggiornamento viene pubblicato nel server WSUS. Sono inclusi i metadati e i file binari dell'aggiornamento.

    -   **Metadata only** (Solo metadati): vengono pubblicati soltanto i metadati, non i file binari. È possibile scegliere questa opzione quando si desiderano raccogliere dati di conformità.

    -   **Automatic** (Automatica): questa modalità è disponibile solo quando si è collegato Updates Publisher a Configuration Manager. Vedere l'opzione [ConfigMgr Server](updates-publisher-options.md#configmgr-server) (Server ConfigMgr).

    Con questo tipo di pubblicazione, Updates Publisher esegue una query in Configuration Manager per stabilire se le aggregazioni o gli aggiornamenti devono essere pubblicati con il contenuto completo o solo con i metadati. Il contenuto completo di un aggiornamento viene pubblicato solo quando quest'ultimo soddisfa i requisiti **Requested client count threshold** (Soglia numero di client con richiesta) e **Package source size threshold** (Soglia dimensioni di origine del pacchetto) specificati nella pagina **ConfigMgr Server** (Server ConfigMgr) delle opzioni di Updates Publisher.

-   Selezionare una pubblicazione:

    -   Quando l'applicazione che si vuole usare è già stata creata, usare l'opzione **Assign software update to existing publications** (Assegna aggiornamento software a pubblicazioni esistenti). Questa opzione è disponibile solo se è presente almeno una pubblicazione.

    -   Se non sono disponibili pubblicazioni appropriate, usare l'opzione **Assign software update to a new publication** (Assegna aggiornamento software a nuova pubblicazione). In questo modo viene creata una nuova pubblicazione con il nome specificato.

Dopo aver assegnato gli aggiornamenti a una pubblicazione, è possibile usare l'**area di lavoro Pubblicazioni** per [pubblicare](updates-publisher-publications.md#publish-publications) o [esportare](updates-publisher-publications.md#export-a-publication) la pubblicazione come gruppo.

## <a name="publish-updates-and-bundles-from-the-updates-workspace"></a>Pubblicare aggiornamenti e aggregazioni dall'area di lavoro Aggiornamenti
Quando si pubblicano aggiornamenti e aggregazioni, Updates Publisher aggiunge informazioni sugli aggiornamenti e le aggregazioni (metadati) e, se possibile, i file binari degli aggiornamenti (contenuto completo) a un server di aggiornamento per la distribuzione ai dispositivi.

Per poter eseguire la pubblicazione, è prima necessario configurare l'opzione [Server di aggiornamento](updates-publisher-options.md#update-server) per Updates Publisher. Per aprire questa opzione di configurazione, passare all'**area di lavoro Aggiornamenti** &gt; **Panoramica** e selezionare **Configure WSUS and Signing Certificate** (Configura WSUS e certificato di firma). È inoltre possibile passare alla pagina Server di aggiornamento nelle opzioni di Updates Publisher.

Esistono due modi per pubblicare gli aggiornamenti e le aggregazioni:
-   Direttamente dall'area di lavoro Aggiornamenti. Vedere la procedura seguente, *Per pubblicare aggiornamenti e aggregazioni*.
-   Come [pubblicazione](updates-publisher-publications.md#publish-publications) dall'area di lavoro Pubblicazioni.  

> [!NOTE]   
> Updates Publisher può pubblicare soltanto aggiornamenti di dimensioni pari o inferiori a 375 megabyte (MB).

### <a name="to-publish-updates-and-bundles"></a>Per pubblicare aggiornamenti e aggregazioni
1.  Passare all'**area di lavoro Aggiornamenti** e selezionare uno o più aggiornamenti e aggregazioni da pubblicare. Scegliere quindi **Pubblica** nella scheda **Home** della barra multifunzione.

2.  Nella pagina **Seleziona** della **Pubblicazione** guidata selezionare la modalità di pubblicazione degli aggiornamenti. Le opzioni disponibili coincidono con quelle disponibili per l'[assegnazione di aggiornamenti](#assign-updates-and-bundles-to-a-publication): **Full Content** (Contenuto completo), **Metadata only** (Solo metadati) o **Automatic** (Automatica).

    È anche possibile scegliere di firmare tutti gli aggiornamenti con un nuovo certificato di pubblicazione.

3.  Completare la procedura guidata.

Se la pubblicazione ha esito negativo, viene visualizzato un collegamento al file UpdatesPublisher.log in cui sono disponibili maggiori informazioni.

## <a name="export-updates"></a>Esportare gli aggiornamenti
È possibile esportare aggiornamenti e aggregazioni dal repository di Updates Publisher per creare un catalogo di aggiornamenti personalizzato. È possibile [aggiungere](updates-publisher-catalogs.md#add-software-update-catalogs) e quindi [importare](updates-publisher-catalogs.md#import-updates) tale catalogo in un'altra istanza di Updates Publisher. È anche possibile [esportare gli aggiornamenti come una pubblicazione](updates-publisher-publications.md#export-a-publication).

Per esportarli direttamente, passare all'**area di lavoro Aggiornamenti** > **All Software Updates** (Tutti gli aggiornamenti software) e selezionare uno o più aggiornamenti o aggregazioni. Non è possibile esportare una cartella di fornitori o prodotti, ma è possibile selezionare una cartella e quindi selezionare gli aggiornamenti in essa presenti per esportarli.

Dopo aver selezionato uno o più aggiornamenti, scegliere **Esporta** nella scheda **Home** della barra multifunzione e specificare un percorso e un nome file per l'esportazione del catalogo.

È possibile esportare (includere) aggiornamenti software dipendenti.

## <a name="delete-updates-and-bundles"></a>Eliminare aggiornamenti e aggregazioni
È possibile eliminare aggiornamenti e aggregazioni di aggiornamenti per rimuoverli dal repository di Updates Publisher.

Passare all'**area di lavoro Aggiornamenti** > **All Software Updates** (Tutti gli aggiornamenti software) e selezionare uno o più aggiornamenti. Scegliere quindi **Elimina** nella scheda **Home** della barra multifunzione.

-   Se la selezione contiene solo aggregazioni o aggiornamenti non pubblicati o scaduti, prima che vengano rimossi viene chiesto di confermare l'eliminazione.

-   Se la selezione include un'aggregazione o un aggiornamento pubblicato e non ancora scaduto, viene visualizzato un avviso. È necessario impostare tali aggiornamenti come [scaduti](updates-publisher-publications.md#expire-or-reactivate-updates-and-bundles) e quindi pubblicare la modifica prima di eliminarli dal repository.  

Se si elimina un aggiornamento o un'aggregazione di un particolare fornitore e quindi si importa di nuovo il catalogo, l'aggiornamento viene ripristinato nel repository.

## <a name="manage-vendor-and-product-folders"></a>Gestire cartelle di fornitori e prodotti
Per visualizzare un elenco dei fornitori e i prodotti di ciascun fornitore per i quali sono stati importati o creati aggiornamenti, passare all'**area di lavoro Aggiornamenti** > **Panoramica** > **All Software Updates** (Tutti gli aggiornamenti software).

Le cartelle dei fornitori e dei prodotti vengono create automaticamente da Updates Publisher quando si esegue l'importazione o la creazione di un aggiornamento o di un'aggregazione usando una procedura guidata. È possibile creare queste cartelle anche manualmente.

-   Per creare una cartella di fornitori, nel riquadro di spostamento dell'**area di lavoro Aggiornamenti** fare clic con il pulsante destro del mouse su **All Software Updates** (Tutti gli aggiornamenti software) e scegliere **Create Vendor** (Crea fornitore).

-   Per creare una cartella di prodotti al di sotto della cartella dei fornitori, fare clic con il pulsante destro del mouse su quest'ultima e scegliere **Create Product** (Crea prodotto).

Oltre a creare cartelle, è possibile rinominare o eliminare qualsiasi cartella di fornitori o prodotti presente nel repository. A tale scopo, fare clic con il pulsante destro del mouse e scegliere l'opzione **Rinomina** o **Elimina**. L'eliminazione di una cartella determina la rimozione di tutte le aggregazioni e gli aggiornamenti in essa contenuti, oltre che delle relative cartelle di prodotti, dal repository di Updates Publisher.

È possibile spostare gli aggiornamenti tra le cartelle di fornitori e quelle di prodotti, incluse le cartelle create. Per spostare un aggiornamento o un'aggregazione in una nuova cartella, è necessario selezionare e quindi modificare l'aggiornamento o l'aggregazione usando l'opzione **Modifica**. Nella pagina **Informazioni** della Modifica guidata aggiornamento è quindi possibile riassegnare il fornitore e il prodotto. Al termine della **Modifica guidata aggiornamento** la modifica viene applicata e l'aggiornamento viene spostato nella nuova cartella.

## <a name="view-the-xml-of-an-update-or-bundle"></a>Visualizzare la struttura XML di un aggiornamento o un'aggregazione
È possibile selezionare un singolo aggiornamento o una singola aggregazione nell'**area di lavoro Aggiornamenti** e quindi scegliere **Visualizza** XML per visualizzare la relativa struttura XML. Non sono disponibili opzioni per la modifica diretta della struttura XML.
