---
title: Gestire cataloghi di aggiornamenti
titleSuffix: Configuration Manager
description: Gestire cataloghi di aggiornamenti software per System Center Updates Publisher
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 887f8029-1a3a-423c-a9c1-31dc0d693386
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1314e2b4a6adc21b876e6bdbf8b25aa9e4fd3e9a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700129"
---
# <a name="manage-software-update-catalogs-in-updates-publisher"></a>Gestire cataloghi di aggiornamenti software in Updates Publisher

*Si applica a: System Center Updates Publisher*

Usare l'**area di lavoro** **Cataloghi** per gestire i cataloghi di aggiornamenti software. Questo include l'aggiunta di nuovi cataloghi, la gestione di sottoscrizioni di cataloghi esistenti e l'importazione di informazioni sugli aggiornamenti da un catalogo al repository di Updates Publisher repository.

I cataloghi di aggiornamenti software contengono informazioni sugli aggiornamenti correlati creati da organizzazioni diverse da Microsoft. Tali organizzazioni includono l'organizzazione dell'utente e i fornitori di software di terze parti che hanno registrato i propri cataloghi con Microsoft. I cataloghi registrati da fornitori di software sono denominati *cataloghi partner*. I cataloghi creati dall'utente e non registrati con Microsoft sono denominati cataloghi *utente*.

## <a name="add-software-update-catalogs"></a>Aggiungere cataloghi di aggiornamenti software
Per poter gestire gli aggiornamenti contenuti in un catalogo di aggiornamenti, è prima necessario aggiungere quest'ultimo a Updates Publisher. Quando si aggiunge un catalogo, Updates Publisher:
-   Crea una sottoscrizione al catalogo in questione, così da consentire la verifica della disponibilità di aggiornamenti.
-   Aggiunge il catalogo a un elenco nella finestra **My Software Update Catalogs** (Cataloghi di aggiornamenti software personali) dell'area di lavoro **Cataloghi**.  

Nella console sono disponibili informazioni su ciascun catalogo sottoscritto. Le informazioni includono l'URL o il percorso di download, il nome della società o dell'organizzazione che ha creato il catalogo e la data dell'ultima importazione o modifica.

Ad ogni avvio, Updates Publisher può controllare automaticamente le sottoscrizioni per verificare la presenza di eventuali modifiche. Questa possibilità viene configurata come una delle opzioni [Avanzate](updates-publisher-options.md#advanced). Quando questa opzione è configurata, Updates Publisher fa riferimento alle informazioni sull'URL o sul percorso di download e invia un avviso se rileva modifiche al catalogo eseguite dopo l'ultima importazione di quest'ultimo nel repository.

Per verificare manualmente la presenza di un catalogo di aggiornamenti, selezionare il catalogo dall'elenco **My Software Update Catalogs** (Cataloghi di aggiornamenti software personali) e quindi selezionare **Aggiorna** dalla barra multifunzione.

Oltre all'aggiunta di cataloghi e alla visualizzazione di informazioni sui cataloghi sottoscritti, è possibile effettuare le operazioni seguenti:
-  **Modificare** informazioni per i cataloghi *utente*.
-  **Eliminare** (rimuovere) un catalogo da Updates Publisher.
-  **Importare** aggiornamenti da un catalogo nel repository di Updates Publisher. Quando si importano aggiornamenti, si importano tutti gli aggiornamenti presenti in tale catalogo. È quindi possibile visualizzare gli aggiornamenti nell'area di lavoro Aggiornamenti, dove è possibile selezionare e pubblicare aggiornamenti nel server di aggiornamento.

> [!NOTE]   
> L'eliminazione di un catalogo da Updates Publisher determina la rimozione dal repository degli aggiornamenti presenti in tale catalogo. Questo non influisce sugli aggiornamenti pubblicati nel server di aggiornamento. Per rimuovere dal server di aggiornamento gli aggiornamenti che non sono più presenti nel repository, vedere [Impostare come scaduti gli aggiornamenti senza riferimenti](updates-publisher-options.md#expire-unreferenced-software-updates).

## <a name="manage-update-catalogs"></a>Gestire cataloghi di aggiornamenti
È possibile visualizzare i cataloghi dell'elenco importati nella finestra **My Software Update Catalogs** (Cataloghi di aggiornamenti software personali) dell'**area di lavoro Cataloghi**. In quest'area di lavoro è possibile:

-   **Aggiungere un catalogo partner:** usare uno dei metodi seguenti per trovare nuovi cataloghi partner:

    -   Nelle console passare all'**area di lavoro Aggiornamenti** > **Panoramica**. Nella finestra **Operazioni preliminari** scegliere **Add Partner Software Updates Catalogs** (Aggiungi cataloghi di aggiornamento software partner).

    -   Nella console passare all'**area di lavoro Cataloghi** > **My Catalogs** (Cataloghi personali). Scegliere quindi **Add Catalogs** (Aggiungi cataloghi) dalla barra multifunzione.

-   **Aggiungere un catalogo utente:** nella console passare all'**area di lavoro Cataloghi** > **My Catalogs** (Cataloghi personali). Scegliere quindi **Add Catalogs** (Aggiungi cataloghi) dalla barra multifunzione. Oltre al percorso del file con estensione cab, è necessario specificare un fornitore, un nome e una descrizione per identificare il catalogo.


-   **Verificare la presenza di aggiornamenti dei cataloghi:** selezionare uno o più cataloghi, quindi scegliere **Aggiorna** dalla barra multifunzione.

-   **Modificare un catalogo utente:** selezionare un catalogo *utente* e quindi scegliere **Modifica** dalla barra multifunzione. È quindi possibile modificare le proprietà definite dall'utente.

-   **Eliminare cataloghi:** selezionare uno o più cataloghi e quindi scegliere **Rimuovi** dalla barra multifunzione. Questa azione rimuove il catalogo, la sottoscrizione e gli aggiornamenti di questi cataloghi dal repository di Updates Publisher.

-   **Aggiungere aggiornamenti da un catalogo al repository**: scegliere **Importa** dalla barra multifunzione per avviare l'**Importazione guidata catalogo**. Per altre informazioni, vedere [Importare aggiornamenti](#import-updates)

## <a name="import-updates"></a>Importare aggiornamenti
Quando si importa un catalogo, Updates Manager aggiunge gli aggiornamenti da tale catalogo nel repository di Updates Publisher. Dopo l'importazione degli aggiornamenti, è possibile pubblicarli nel server di aggiornamento per renderli disponibili ai dispositivi gestiti.

### <a name="to-import-updates"></a>Per importare aggiornamenti
1. Per avviare l'**Importazione guidata catalogo**, scegliere **Importa** dalla barra multifunzione in una delle aree di lavoro seguenti:

   -   Area di lavoro Cataloghi

   -   Area di lavoro Aggiornamenti

2. Nella pagina **Tipo di importazione** selezionare uno o più cataloghi aggiunti ad Updates Publisher. In alternativa, specificare un percorso a un catalogo non ancora aggiunto come sottoscrizione. Scegliere **Avanti** per visualizzare la schermata di riepilogo, quindi, dopo aver verificato le informazioni immesse, scegliere **Avanti** per avviare l'importazione.

3. Scegliere **Avanti** per visualizzare la schermata di riepilogo, quindi, dopo aver verificato le informazioni immesse, scegliere **Avanti** per avviare l'importazione.

   > [!CAUTION]
   > Accettare aggiornamenti solo da autori attendibili. Gli aggiornamenti software offerti da autori non attendibili possono potenzialmente danneggiare i computer client durante la ricerca di aggiornamenti.
   > 
   >  Se si ritiene che un autore non sia più attendibile, rimuoverlo dall'elenco degli autori attendibili. Per trovare altre informazioni sull'accettazione dei cataloghi, fare clic su **Tell Me More** (Ulteriori informazioni) nella finestra di dialogo **Security Warning – Catalog Validation** (Avviso di protezione – Convalida catalogo).

   Se si sceglie di accettare i cataloghi di un particolare autore, tale autore viene aggiunto all'[elenco degli autori attendibili](updates-publisher-options.md#trusted-publishers). È possibile esaminare e modificare questo elenco come opzione di Updates Publisher.

4. L'importazione di un aggiornamento non viene eseguita quando quest'ultimo si trova già nel repository e si verifica una delle condizioni seguenti:

   -   L'aggiornamento non è stato modificato dall'ultima importazione.

   -   L'aggiornamento è stato modificato e dispone di un nuovo hash digitale. La modifica di un aggiornamento impedisce che un nuovo aggiornamento sovrascriva quello originale. La sovrascrittura dell'originale determinerebbe infatti la sovrascrittura delle modifiche eventualmente distribuite.

5. Nella pagina **Conferma** esaminare i risultati dell'importazione.

6. Fare clic su **Chiudi** per completare la procedura guidata. È ora possibile visualizzare gli aggiornamenti per il catalogo in Updates Workspace.

## <a name="next-steps"></a>Passaggi successivi
Dopo l'importazione degli aggiornamenti, le azioni comuni includono le seguenti:
-   [Gestire gli aggiornamenti](manage-updates-with-updates-publisher.md) per aggregarli, assegnarli e distribuirli al server di aggiornamento.
-   [Creare regole di applicabilità](updates-publisher-applicability-rules.md) che consentono di determinare quando è opportuno distribuire gli aggiornamenti al server di aggiornamento.
