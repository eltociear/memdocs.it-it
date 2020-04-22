---
title: Monitoraggio dello stato di integrità
titleSuffix: Configuration Manager
description: Informazioni sul funzionamento del monitoraggio dello stato di integrità in Desktop Analytics.
ms.date: 01/16/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 343dbe2a-597c-4719-b7ac-45b1f39b49ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 359fdec13ee6bfd43e66d4bf9cec70c5a3188a32
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693049"
---
# <a name="health-status-monitoring-in-desktop-analytics"></a>Monitoraggio dello stato di integrità in Desktop Analytics

Quando si [distribuisce un aggiornamento nell'ambiente di produzione](deploy-prod.md), usare Desktop Analytics per monitorare lo stato di integrità dei dispositivi. Questo articolo spiega in dettaglio il funzionamento del monitoraggio dello stato.

Per altre informazioni su come usare questa funzionalità, vedere [Monitorare l'integrità dei dispositivi aggiornati](deploy-prod.md#bkmk_monitor).

![Screenshot della pagina Monitora integrità di Desktop Analytics](media/monitor-health.png)

> [!NOTE]  
> Desktop Analytics raccoglie dati sull'integrità solo dai dispositivi che offrono dati di utilizzo utilizzabili come denominatore. Ciò significa che non sono inclusi i dispositivi Windows 7 e Windows 10 non impostati per la condivisione dei dati di diagnostica a livello Avanzata (con limitazioni). Se più del 10% dei dispositivi che eseguono Windows 10 è impostato per la condivisione dei dati di diagnostica a livelli diversi da Avanzata (con limitazioni), nell'area banner della pagina **Monitora integrità** viene visualizzato un avviso.  

Per visualizzare altre informazioni su un'app specifica, selezionarla nell'elenco.

## <a name="apps"></a>App

### <a name="health-status-factors"></a>Fattori relativi allo stato di integrità

![Fattori dello stato di integrità per un'app in Desktop Analytics](media/monitor-health-status-factors.png)

Desktop Analytics esegue il monitoraggio dei fattori dello stato di integrità seguenti per le app:

- **% dispositivi con arresti anomali**: per le ultime due settimane, rapporto tra il numero di dispositivi in cui l'app specificata si è arrestata in modo anomalo e il numero di dispositivi in cui l'app è stata usata. Questa visualizzazione consente di verificare se la stabilità dell'app è aumentata o diminuita nella nuova versione del sistema operativo. Desktop Analytics calcola questa percentuale per i set seguenti:  

  - **Dopo l'aggiornamento**: dispositivi aggiornati alla versione del sistema operativo di destinazione specificata nel piano di distribuzione. Per ridurre il numero di risorse con dati insufficienti, Desktop Analytics raccoglie questi dati per tutti i dispositivi aggiornati. Questo set include i dispositivi non inclusi nel piano di distribuzione.  

  - **Prima dell'aggiornamento**: dispositivi con una versione del sistema operativo precedente a quanto specificato nel piano di distribuzione. Questo elenco non include i dispositivi che eseguono Windows 7.  

  - **Media commerciale**: percentuale media di arresti anomali per tutti i dispositivi commerciali. Questa media viene calcolata per *tutte* le versioni dell'app. Se per la versione in uso la percentuale di arresti anomali è superiore alla media commerciale, può essere disponibile una versione più stabile.  

- **% sessioni con arresti anomali**: simile al precedente, ma calcola la percentuale di sessioni con arresti anomali nelle ultime due settimane.  

Per determinare lo stato di integrità di un'app, Desktop Analytics ha bisogno dei dati di almeno 20 dispositivi. In caso contrario, segnala **Dati insufficienti** per l'app. Il servizio calcola lo stato di integrità in base alla *frequenza degli arresti anomali di sessione* in questi dispositivi. La frequenza degli arresti anomali di dispositivo viene indicata solo a scopo informativo e non viene usata nel calcolo dello stato di integrità.

### <a name="usage"></a>Utilizzo

<!-- 5533890 -->

- **Dispositivi attivi**: questo valore corrisponde al numero di dispositivi in cui un utente ha avviato l'app selezionata nelle ultime due settimane. Si basa sui dispositivi nel piano di distribuzione selezionato che eseguono la versione di destinazione di Windows 10.

- **Sessioni**: questo valore indica il numero totale di volte in cui un utente ha avviato l'app selezionata nella versione di destinazione di Windows.

### <a name="additional-tabs"></a>Schede aggiuntive

Nella parte inferiore della pagina dei dettagli dell'app, le tre schede seguenti possono essere utili per la risoluzione dei problemi:

- **Altre versioni**: elenco di versioni alternative dell'app. Per ogni versione, sono visualizzate le variazioni relative alla frequenza degli arresti anomali all'interno dell'organizzazione e alla media commerciale. Se si trova una versione più recente dell'app con una frequenza degli arresti anomali inferiore, può essere utile aggiornare l'app.  

    Viene anche indicato se la versione ha informazioni dettagliate avanzate. Per altre informazioni, vedere [Valutazione della compatibilità](compat-assessment.md).  

- **Problemi principali**: elenco degli ID errore più frequenti per numero di istanze. Un ID errore identifica l'analisi dello stack associata all'arresto anomalo. È possibile usare questo ID quando si chiama il fornitore dell'app per supporto.  

- **Arresti anomali recenti**:  elenco di dispositivi in cui l'app si è recentemente arrestata in modo anomalo. È possibile filtrare l'elenco per ID errore e altri criteri. Usare queste informazioni per risolvere il problema raccogliendo log o provando correzioni su dispositivi specifici prima di provare una distribuzione più ampia.  

Se si rileva una grave regressione dell'integrità che non è possibile correggere, modificare la **Decisione di aggiornamento** dell'app in **Non possibile**. Questa azione evita in futuro la distribuzione dell'aggiornamento ai dispositivi con questa risorsa.

## <a name="see-also"></a>Vedere anche

- [Valutazione della compatibilità in Desktop Analytics](compat-assessment.md)  

- [Come eseguire la distribuzione nell'ambiente di produzione con Desktop Analytics](deploy-prod.md)  
