---
title: Gestire i dati di configurazione
titleSuffix: Configuration Manager
description: Dopo aver creato gli elementi e le linee di base di configurazione in Configuration Manager è possibile usare altri comandi per eseguire diverse azioni.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: b48c693c-d2b0-4707-a5dd-fe92172c49fe
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: c375b5d773775e1be89f1e9dda38ee04e7f9f63f
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240253"
---
# <a name="manage-configuration-data-in-configuration-manager"></a>Gestire i dati di configurazione in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Dopo aver creato gli elementi e le linee di base di configurazione in Configuration Manager è possibile usare altri comandi per eseguire diverse azioni.  

## <a name="manage-configuration-items"></a>Gestire gli elementi di configurazione  

-   Nell'area di lavoro **Asset e conformità** espandere **Impostazioni di conformità** > **Elementi di configurazione**, selezionare l'elemento di configurazione da gestire e quindi selezionare un'attività di gestione.  

|Attività di gestione|Dettagli|  
|---------------------|-------------|  
|**Crea elemento di configurazione figlio**|Apre la **Creazione guidata dell'elemento di configurazione figlio** in cui è possibile creare un elemento di configurazione figlio dall'elemento di configurazione selezionato.<br /><br /> Non è possibile creare un elemento di configurazione figlio da un elemento di configurazione del dispositivo mobile.<br /><br /> Per informazioni dettagliate, vedere [Come creare elementi di configurazione figlio](../../compliance/deploy-use/create-child-configuration-items.md).|  
|**Cronologia revisioni**|Apre la finestra di dialogo **Cronologia revisioni dell'elemento di configurazione** in cui è possibile visualizzare e gestire le revisioni precedenti dell'elemento di configurazione selezionato.|  
|**Visualizza definizione XML**|Visualizza il file di definizione XML per l'elemento di configurazione selezionato in una nuova finestra. Queste informazioni possono essere utile quando si desidera creare manualmente i dati di configurazione.|  
|**Export**|Esporta un elemento di configurazione in un file in formato cabinet (CAB) e specifica che il file è stato creato in quel sito. È quindi possibile importarlo nello stesso sito o in un sito diverso di Configuration Manager. I dati di configurazione vengono convertiti in DCM Digest.|  
|**Copia**|Crea una copia dell'elemento di configurazione selezionato con un nome specificato. Il nuovo elemento di configurazione non conserva alcuna relazione con l'elemento di configurazione originale. Ciò significa che l'elemento di configurazione duplicati non continua da cui ereditare le informazioni di configurazione dell'elemento di configurazione originale.|  
|**Eliminazione**|Apre la finestra di dialogo **Elimina elemento di configurazione** in cui è possibile esaminare i riferimenti a un elemento di configurazione specifico.<br /><br /> È necessario rimuovere tutti i riferimenti a un elemento di configurazione prima di poter eliminare l'elemento di configurazione.|  

## <a name="manage-configuration-baselines"></a>Gestire le linee di base di configurazione  

-   Nell'area di lavoro **Asset e conformità** espandere **Impostazioni di conformità** > **Linee di base di configurazione**, selezionare la linea di base di configurazione da gestire e quindi selezionare un'attività di gestione.  


|Attività di gestione|Dettagli|  
|---------------------|-------------|  
|**Mostra i membri**|Visualizza tutti gli elementi di configurazione a cui fa riferimento la linea di base di configurazione.|  
|**Pianifica riepilogo**|Configura la pianificazione in base alla quale i dati visualizzati nel nodo **Linee di base di configurazione** nella console di Configuration Manager vengono aggiornati con le informazioni più recenti del database del sito.|  
|**Esegui riepilogo**|Il riepilogo fa sì che i dati nel nodo **Linee di base di configurazione** vengano aggiornati in base ai dati più recenti del database del sito. L'esecuzione di questa operazione può richiedere alcuni minuti. Potrebbe essere necessario fare clic su **Aggiorna** prima di poter visualizzare i dati più recenti nella console.|  
|**Visualizza definizione XML**|Visualizza il file di definizione XML per la linea di base di configurazione selezionata in una nuova finestra. Queste informazioni possono essere utile quando si desidera creare manualmente i dati di configurazione.|  
|**Attiva**|Consente una configurazione di base per il monitoraggio di conformità.|  
|**Disabilitato**|Disabilita una linea di base di configurazione in modo che non ne venga valutata la conformità nei computer client. Configurazioni di base che fanno riferimento a questa configurazione di base saranno disabilitati.|  
|**Export**|Esporta una linea di base di configurazione in un file in formato cabinet (CAB) e specifica che il file è stato creato in quel sito. È quindi possibile importarlo nello stesso sito o in un sito diverso di Configuration Manager. I dati di configurazione vengono convertiti in DCM Digest.<br /><br /> Per informazioni sull'importazione dei dati di configurazione, vedere [Come importare dati di configurazione](../../compliance/deploy-use/import-configuration-data.md).|  
|**Copia**|Crea una copia della linea di base di configurazione selezionata con un nome specificato. La nuova linea di base di configurazione non vengono mantenute tutte le relazioni alla linea di base di configurazione originale.|  
|**Eliminazione**|Apre la finestra di dialogo **Elimina linea di base di configurazione** in cui è possibile esaminare i riferimenti a una linea di base di configurazione specifica.<br /><br /> È necessario rimuovere tutti i riferimenti a una linea di base di configurazione prima di poter eliminare la linea di base di configurazione.|  
|**Distribuzione**|Apre la finestra di dialogo **Distribuisci linee di base di configurazione** in cui è possibile distribuire una o più linee di base di distribuzione nei dispositivi inclusi nella gerarchia.<br /><br /> Per informazioni dettagliate, vedere [Come distribuire linee di base di configurazione](../../compliance/deploy-use/deploy-configuration-baselines.md).|  
