---
title: Come distribuire nell'ambiente di produzione
titleSuffix: Configuration Manager
description: Guida pratica per la distribuzione in un gruppo di produzione di Desktop Analytics.
ms.date: 06/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 637fbd8e-b8ea-4c7e-95ee-a60a323c496e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c7a14da1505e89dfd61a3dc4f13385fbf5c21d41
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708229"
---
# <a name="how-to-deploy-to-production-with-desktop-analytics"></a>Come eseguire la distribuzione nell'ambiente di produzione con Desktop Analytics

Dopo aver [eseguito la distribuzione in un progetto pilota](deploy-pilot.md) e aver esaminato lo stato delle risorse, è possibile eseguire l'aggiornamento della parte restante dell'ambiente di produzione.

[!INCLUDE [Definition of pilot and production](includes/define-pilot-prod.md)]

Per eseguire la distribuzione degli aggiornamenti nei dispositivi di produzione, eseguire le tre principali operazioni seguenti:

1. [Esaminare le risorse che necessitano di una decisione di aggiornamento](#bkmk_review): perché i dispositivi siano pronti per la distribuzione nell'ambiente di produzione, è necessario che la decisione di aggiornamento delle relative risorse sia impostata su **Pronto** o **Pronto, Correzione richiesta**.  

2. [Eseguire la distribuzione nei dispositivi pronti](#bkmk_deploy): usare Configuration Manager per aggiornare i dispositivi pronti. Desktop Analytics offre l'elenco dei dispositivi pronti per la distribuzione nell'ambiente di produzione e i report per monitorare se la distribuzione ha esito positivo.  

3. [Monitorare l'integrità dei dispositivi aggiornati](#bkmk_monitor): man mano che la distribuzione degli aggiornamenti procede, monitorare l'integrità delle risorse importanti. Se alcune risorse richiedono attenzione, risolvere i problemi. Se si ritiene che i problemi non possano essere risolti, arrestare la distribuzione nei dispositivi interessati impostando la decisione di aggiornamento su **Non possibile**.  

> [!NOTE]  
> Quando si è sicuri di poter completare con successo la distribuzione del progetto pilota, avviare la distribuzione nell'ambiente di produzione in qualsiasi momento. Non è necessario che tutti i dispositivi pilota raggiungano prima lo stato "Operazione completata".  



## <a name="review-assets-that-need-an-upgrade-decision"></a><a name="bkmk_review"></a> Esaminare le risorse che necessitano di una decisione di aggiornamento

Desktop Analytics consente di esaminare le risorse per la distribuzione nell'ambiente di produzione. Nella portale di Azure passare a **Piani di distribuzione**, selezionare un piano di distribuzione, quindi selezionare **Prepara produzione** nel menu a sinistra.

![Screenshot della visualizzazione Prepara produzione in Desktop Analytics](media/prepare-production.png)

Esaminare lo stato delle app. Usare queste informazioni per impostare la decisione di aggiornamento per ognuna di tali risorse.

Usare ognuna delle schede per esaminare lo stato delle app. In ogni visualizzazione a schede è possibile filtrare i risultati per visualizzare i dispositivi che devono essere monitorati per l'aggiornamento, i dispositivi che richiedono attenzione, i dispositivi con risultati misti e quelli che si trovano in uno stato indeterminato.

Selezionare **Raggiungimento degli obiettivi** per filtrare la visualizzazione in base alle risorse che sono probabilmente pronte per la distribuzione nell'ambiente di produzione in base ai criteri seguenti:

- Rischio: valutazione pre-aggiornamento dei rischi noti per l'aggiornamento dei dispositivi in cui è installata questa risorsa  

- Stato integrità: valutazione successiva all'aggiornamento dei dispositivi in altre distribuzioni e valutazione di eventuali problemi riscontrati dopo l'installazione dell'aggiornamento. Per altre informazioni sull'integrità, vedere [Monitorare l'integrità dei dispositivi aggiornati](#bkmk_monitor).  

Per approvare l'aggiornamento di una risorsa, selezionare il nome nell'elenco, quindi selezionare una delle opzioni seguenti nell'elenco **Decisione aggiornamento**:

- Revisione in corso
- Pronto
- Pronto (con correzione)
- Non possibile
- Non riviste

Per impostare questo valore per più app contemporaneamente, usare la prima colonna per **selezionare l'elemento**, quindi scegliere **Imposta decisione di aggiornamento**.

![Imposta decisione di aggiornamento in più app](media/prep-prod-set-upgrade-decision.png)

Selezionare **Nessun dato** per visualizzare le risorse che non possono essere classificate. Si tratta in genere delle risorse che non hanno copertura sufficiente perché Desktop Analytics possa eseguire un'analisi del rischio o dello stato integrità. Per migliorare la copertura, aggiungere altri dispositivi con queste risorse al progetto pilota o richiedere agli utenti del progetto pilota di provare queste risorse.

Alcune risorse potrebbero avere lo stato **Intervento necessario** o **Mixed Results** (Risultati misti). Per queste risorse può essere necessaria una verifica aggiuntiva prima di prendere una decisione di aggiornamento.

Rivedere tutte le app. Quando a un determinato dispositivo viene assegnata una decisione di aggiornamento positiva per tutte le risorse, lo stato diventa "pronto per la produzione". Vedere il conteggio corrente nella pagina principale per il piano di distribuzione selezionando il terzo passaggio della distribuzione, vala a dire **Distribuire**.


## <a name="deploy-to-devices-that-are-ready"></a><a name="bkmk_deploy"></a> Eseguire la distribuzione nei dispositivi pronti

Configuration Manager usa i dati di Desktop Analytics per creare una raccolta per la distribuzione nell'ambiente di produzione. Non distribuire la sequenza di attività usando una distribuzione tradizionale. Usare la procedura seguente per creare una distribuzione integrata di Desktop Analytics:

Se è stata seguita la procedura consigliata per [distribuire nei dispositivi pilota](deploy-pilot.md#deploy-to-pilot-devices), la distribuzione in più fasi di Configuration Manager è pronta. Quando le risorse vengono contrassegnate con lo stato *Pronto*, Desktop Analytics sincronizza automaticamente tali dispositivi con Configuration Manager. I dispositivi vengono quindi aggiunti alla raccolta di produzione. Quando la distribuzione in più fasi passa alla seconda fase, i dispositivi di produzione ricevono la distribuzione dell'aggiornamento.

Se la distribuzione in più fasi è stata configurata in modo da **iniziare manualmente la seconda fase della distribuzione**, è necessario passare manualmente alla fase successiva. Per altre informazioni, vedere questo articolo: [Gestire e monitorare le distribuzioni in più fasi](../osd/deploy-use/manage-monitor-phased-deployments.md#bkmk_move).

Se è stata creata un'unica distribuzione integrata di Desktop Analytics nella raccolta pilota, è necessario ripetere il processo per eseguire la distribuzione nella raccolta di produzione.


### <a name="address-deployment-alerts"></a>Risolvere gli avvisi di distribuzione

Come per la distribuzione pilota, è consigliabile individuare eventuali problemi che richiedono attenzione durante la distribuzione nell'ambiente di produzione. In Desktop Analytics passare al piano di distribuzione e selezionare **Stato distribuzione** nel menu a sinistra. Nella visualizzazione Stato distribuzione sono elencati i dispositivi nelle categorie seguenti:  

- Non avviato
- In corso
- Completed
- Richiede attenzione - Dispositivi (ordinati per nome dispositivo)
- Richiede attenzione - Problemi (ordinati per tipo di problema)

![Screenshot di Stato distribuzione nell'ambiente di produzione di Desktop Analytics](media/prod-deployment-status.png)


## <a name="monitor-the-health-of-updated-devices"></a><a name="bkmk_monitor"></a> Monitorare l'integrità dei dispositivi aggiornati

La pagina **Prepara produzione** offre supporto per prendere decisioni di aggiornamento per le risorse. Per impostazione predefinita, questa pagina visualizza solo le risorse che non si trovano ancora nello stato **Pronto**. La pagina **Monitora integrità** visualizza i problemi di integrità nelle risorse importanti, anche in quelle contrassegnate con **Pronto**. Se vengono individuati problemi, è possibile risolvere il problema oppure modificare la decisione di aggiornamento in **Non possibile**. Quando si modifica la decisione di aggiornamento, si impedisce l'aggiornamento futuro nei dispositivi con questa risorsa.

Filtrare la pagina in base alle risorse usando gli stati di integrità seguenti:

| Filtro per lo stato di integrità | Descrizione |
|----------------------|-------------|
| **Intervento necessario** | (Filtro predefinito) Desktop Analytics rileva una regressione statisticamente significativa a una metrica di integrità per la risorsa
| **Raggiungimento degli obiettivi** | Desktop Analytics non rileva alcuna regressione nel comportamento |
| **Dati insufficienti** | Desktop Analytics non dispone di dati sufficienti su questa risorsa per dare consigli |
| **Nessun dato** | Non sono ancora disponibili dati per questa risorsa |

Per una visualizzazione senza filtro di tutte le risorse, selezionare il filtro corrente. Si rimuove così il filtro applicato.

> [!NOTE]  
> Per ridurre il numero delle risorse con dati insufficienti, Desktop Analytics monitora le risorse in tutti i dispositivi che hanno eseguito l'aggiornamento alla versione di Windows di destinazione specificata nel piano di distribuzione. Nei dispositivi sono inclusi quelli non presenti nel piano di distribuzione specificato.  

Per impostazione predefinita, i dispositivi vengono ordinati in base al numero di volte in cui si è verificato un incidente con una risorsa in particolare. In questo modo è possibile individuare rapidamente quali risorse causano la maggior parte dei problemi. Ad esempio, quando si visualizza **App**, viene eseguito l'ordinamento in base ai **Dispositivi con arresti anomali di app nelle ultime 2 settimane**.

Se si vuole esaminare lo stato di integrità di tutte le risorse, anche di quelle con dati insufficienti per consentire a Desktop Analytics di eseguire inferenze statistiche, usare il processo seguente:

1. Selezionare l'elenco a discesa nella colonna **Dispositivi con incidenti nelle ultime 2 settimane**. Aggiungere un filtro solo a quelle risorse in cui si sono verificati incidenti in un numero minimo di dispositivi. Visualizzare ad esempio gli elementi con valori **maggiori di** 100.  

2. Selezionare l'elenco a discesa nella colonna **% Dispositivi con incidenti nelle ultime 2 settimane** e ordinare per **Decrescente**.  

    La visualizzazione risultante include le risorse con la massima frequenza di incidente in un numero minimo di incidenti.  

3. Selezionare una risorsa per ottenere altri dettagli o modificare la decisione di aggiornamento.  

Per altre informazioni, vedere [Monitoraggio dello stato di integrità](health-status-monitoring.md).
