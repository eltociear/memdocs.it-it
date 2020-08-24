---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 08/11/2020
ms.openlocfilehash: 98e3dd75316acfeaf88715b8f80762b1d6c587c6
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128334"
---
<!--This file is shared by the cmpivot.md file and the cmpivot-changes.md file and contains information on how to run CMPivot standalone. H2s or HJ3s are determined by the article for which the include file is used.-->
<!--3555890, 4619340, 4683130 -->

A partire dalla versione 1906 è possibile usare CMPivot come app autonoma. La versione autonoma di CMPivot è disponibile solo in inglese. Eseguire CMPivot all'esterno della console di Configuration Manager per visualizzare in tempo reale lo stato dei dispositivi presenti nell'ambiente. Questa modifica consente di usare CMPivot in un dispositivo senza aver prima installato la console.

> [!Tip]  
> Questa funzionalità è stata introdotta per la prima volta nella versione 1906 come [funzionalità di versione non definitiva](../pre-release-features.md). A partire dalla versione 2002, non è più una funzionalità di versione non definitiva.  

È possibile condividere le funzionalità di CMPivot con altri utenti tipo, ad esempio operatori di help desk o amministratori della sicurezza, che non hanno la console installata nel proprio computer. Queste altre persone possono usare CMPivot per eseguire query su Configuration Manager insieme agli altri strumenti che usano solitamente. Condividendo questi dati di gestione completi, è possibile collaborare per risolvere proattivamente i problemi aziendali che riguardano più ruoli.

#### <a name="install-cmpivot-standalone"></a>Installare la versione autonoma di CMPivot

1. Configurare le autorizzazioni necessarie per eseguire CMPivot. Per altre informazioni, vedere i [prerequisiti](../cmpivot.md#prerequisites). È anche possibile usare il [ruolo Amministratore della protezione](../cmpivot-changes.md#bkmk_cmpivot_secadmin1906) se le autorizzazioni sono appropriate per l'utente.
2. Il programma di installazione dell'app CMPivot è disponibile nel percorso seguente: `<site install path>\tools\CMPivot\CMPivot.msi`. È possibile eseguirlo da questo percorso oppure copiarlo in un'altra posizione.
3. Quando si esegue l'app autonoma CMPivot, viene chiesto di connettersi a un sito. Specificare il nome di dominio completo o il nome del computer del server del sito di amministrazione centrale o primario.
   - Ogni volta che si apre la versione autonoma di CMPivot viene chiesto di connettersi a un server del sito.
4. Passare alla raccolta in cui si vuole eseguire CMPivot, quindi eseguire la query.

   ![Passare alla raccolta in cui si vuole eseguire la query](../media/3555890-cmpivot-standalone-browse-collection.png)

> [!NOTE]
> - Azioni con il pulsante destro del mouse, come **Esegui script**, **Esplora inventario risorse** e la ricerca Web non sono disponibili nella versione autonoma di CMPivot. L'uso principale della versione autonoma di CMPivot consiste nell'esecuzione di query indipendentemente dall'infrastruttura di Configuration Manager. Per facilitare gli amministratori della sicurezza, la versione autonoma di CMPivot include la possibilità di connettersi a Microsoft Defender Security Center. <!--5605358-->
> - A partire dalla versione 1910, si può eseguire [la valutazione delle query sul dispositivo locale con la versione autonoma di CMPivot](../cmpivot-changes.md#bkmk_local-eval). <!--3197353--> 