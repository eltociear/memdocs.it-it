---
title: Piani di distribuzione in Desktop Analytics
titleSuffix: Configuration Manager
description: Informazioni sui piani di distribuzione in Desktop Analytics.
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 0f369f3a-f251-4f34-9302-1bdc6ea5d139
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: ccc325ac4b8e02142a1442862ad661a77b0561f2
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268488"
---
# <a name="about-deployment-plans-in-desktop-analytics"></a>Informazioni sui pani di distribuzione in Desktop Analytics

Desktop Analytics raccoglie e analizza i dati dei dispositivi, delle applicazioni e dei driver nell'organizzazione. In base a questa analisi e all'input dell'utente, è possibile usare il servizio per creare piani di distribuzione per Windows 10. I piani di distribuzione hanno le caratteristiche seguenti:  

- Suggeriscono automaticamente quali dispositivi includere nei progetti pilota  

- Identificano i problemi di compatibilità e suggeriscono le mitigazioni  

- Valutano l'integrità della distribuzione prima, durante e dopo gli aggiornamenti  

- Tengono traccia dello stato della distribuzione  

Nel piano di distribuzione sono previste le azioni seguenti:  

- Definire le versioni di Windows 10 da distribuire  

- Scegliere i gruppi di dispositivi in cui si vuole eseguire la distribuzione  

- Creare regole di idoneità per la distribuzione  

- Definire l'importanza delle app  

- Scegliere i dispositivi pilota in base ai consigli automatici  

- Decidere come risolvere i problemi con le app in base ai consigli di Desktop Analytics  

Per impostazione predefinita, Desktop Analytics aggiorna quotidianamente i dati del piano di distribuzione. Tutte le modifiche apportate in un piano di distribuzione, ad esempio l'assegnazione dell'importanza a un'app o la scelta di un dispositivo da includere in un progetto pilota, vengono elaborate nelle 24 ore. Per velocizzare questo processo, richiedere un aggiornamento dati su richiesta. Per altre informazioni, vedere [Domande frequenti su Desktop Analytics](faq.md#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).  

Dopo aver connesso Desktop Analytics a Configuration Manager, selezionare le raccolte nei piani di distribuzione. Questa integrazione consente di distribuire Windows in una raccolta che si basa sui dati di Desktop Analytics.

## <a name="readiness-rules"></a>Regole di idoneità

Nei piani di distribuzione sono disponibili le regole di idoneità seguenti:

- Se i dispositivi ricevono automaticamente i driver da Windows Update. Se i dispositivi ricevono gli aggiornamenti dei driver da Windows Update, tutti i problemi relativi ai driver identificati nella valutazione dell'idoneità vengono contrassegnati automaticamente con **Pronto**.  

- Soglia del numero di installazioni basso per le app Windows. Se un'app viene installata in una percentuale di computer superiore a questa soglia, il piano di distribuzione contrassegna l'app come **Importante**. In questo modo si può decidere quanto sia importante eseguire il test dell'app durante la fase pilota.  

## <a name="plan-assets"></a>Risorse del piano

<!-- 4670224 -->

Mentre l'area [Risorse](about-assets.md) visualizza anche i dispositivi e le app, l'area **Risorse del piano** in un piano di distribuzione specifico include informazioni aggiuntive.

### <a name="devices"></a>Dispositivi

Vedere la **Decisione relativa all'aggiornamento di Windows** per ogni dispositivo nel piano di distribuzione.

La decisione di aggiornamento di Windows di **sostituire il dispositivo** può essere presa per uno dei motivi seguenti:

- Il controllo del processore richiesto di Windows 10 non è riuscito. Per altre informazioni, vedere [Requisiti hardware minimi](https://docs.microsoft.com/windows-hardware/design/minimum/minimum-hardware-requirements-overview#31-processor).
- È presente un blocco BIOS
- La memoria non è sufficiente
- Un componente critico di avvio nel sistema ha un driver bloccato
- Non è possibile aggiornare la marca e il modello specifici
- Un componente della classe di visualizzazione ha un blocco di driver con tutti gli attributi seguenti:
  - Non eseguire l'override
  - Non esistono driver nella nuova versione del sistema operativo
  - Non è ancora in Windows Update
- Un altro componente Plug and Play nel sistema blocca l'aggiornamento
- Un componente wireless usa un driver di emulazione XP
- Un componente di rete con una connessione attiva perderà il driver. In altre parole, dopo l'aggiornamento potrebbe verificarsi una perdita di connettività di rete.

La scelta dell'opzione **Reinstalla** indica che per Windows sarà necessaria una reinstallazione rispetto a un aggiornamento sul posto.

Una decisione di aggiornamento di Windows **Bloccata** può essere causata dai motivi seguenti:

- La decisione di aggiornamento di uno o più asset è stata impostata su **Non possibile**.

- I dati di inventario per il dispositivo sono incompleti e Desktop Analytics non può eseguire una valutazione della compatibilità completa.

### <a name="apps"></a>App

Impostare la **Decisione di aggiornamento** e l'**Importanza** per questa app in questo piano di distribuzione. Per altre informazioni, vedere [Come creare i piani di distribuzione](create-deployment-plans.md).

Nei dettagli dell'app è possibile individuare anche le informazioni seguenti: consigli, fattori di rischio di compatibilità e problemi noti in Microsoft. Usare queste informazioni per impostare la **Decisione di aggiornamento**. Per altre informazioni, vedere [Valutazione della compatibilità](compat-assessment.md).

Le app ritenute *importanti* da Desktop Analytics si basano sulla soglia del numero di installazioni basso per le regole di idoneità del piano di distribuzione. Per altre informazioni, vedere [Regole di idoneità](create-deployment-plans.md#readiness-rules).

   > [!Tip]
   > Per altre informazioni sulla categoria delle app "Non importante", vedere [Decisione di aggiornamento automatico delle app di sistema e dello Store](about-assets.md#bkmk_plan-autoapp). <!-- 3587232 -->

L'impostazione **Dettagli delle versioni dell'app** è disattivata per impostazione predefinita. Questa scheda, quindi, combina tutte le versioni delle app con lo stesso nome e lo stesso autore.<!-- 5542186 --> Il comportamento predefinito contribuisce a ridurre il numero totale di app visualizzate, consentendo di ridurre l'impegno richiesto per l'annotazione delle app. Il numero di app nel riquadro **App degne di nota** riflette anche questa impostazione. Ad esempio, anziché un elenco di centinaia di istanze di Microsoft Edge, è presente una sola istanza per tutte le versioni. È possibile prendere decisioni una volta per tutte le versioni. Se è necessario prendere decisioni per versioni specifiche di un'app, attivare questa impostazione. È possibile configurare questa impostazione anche quando si lavora a livello di asset globali. Per altre informazioni, vedere [Informazioni sugli asset - App](about-assets.md#apps).

Quando l'impostazione **Dettagli delle versioni dell'app** è disattivata, il riquadro dei dettagli dell'app visualizza il numero di versioni e lingue delle app combinate. Se si salvano eventuali modifiche apportate ai dettagli dell'app, queste vengono applicate a tutte le versioni. Impostare, ad esempio, la **decisione di aggiornamento** o l'**importanza**. Alcuni valori visualizzano "Più valori", che significa che non è presente un solo valore coerente in tutte le versioni. Il servizio esegue comunque una valutazione del rischio di compatibilità per ogni versione. Attivare **Dettagli delle versioni dell'app** per visualizzare la valutazione del rischio di compatibilità per una versione specifica dell'app.

### <a name="drivers"></a>Driver

Vedere l'elenco dei driver inclusi in questo piano di distribuzione. Impostare la **Decisione di aggiornamento**, rivedere i consigli di Microsoft e i fattori di rischio di compatibilità.

## <a name="importance"></a>Importanza

Il piano di distribuzione prevede l'impostazione dell'*importanza* delle app. Desktop Analytics rileva queste app come app installate nei dispositivi di destinazione. Questa impostazione consente a Desktop Analytics di determinare quali dispositivi includere nella fase pilota della distribuzione.

Se un'app è installata in meno del 2% dei dispositivi di destinazione, viene impostato il contrassegno **Numero di installazioni basso**. Il 2% è il valore predefinito. È possibile regolare la soglia nelle impostazioni di idoneità definendo un valore compreso tra da 0% e 10%. Desktop Analytics contrassegna automaticamente queste app come **Pronte per l'aggiornamento**.  

Scegliere un'importanza per le app che può essere **Critica**, **Importante** o **Non importante**. Se si contrassegna un'app come critica o importante, Desktop Analytics include nella distribuzione pilota alcuni dispositivi con tale app. Il servizio include nel progetto pilota più istanze di un'app critica. Se si contrassegna un'app come non importante, Desktop Analytics la imposta automaticamente come **Pronta per l'aggiornamento**.

## <a name="pilot-devices"></a>Dispositivi pilota

Desktop Analytics combina le informazioni relative all'importanza con le impostazioni del progetto pilota globali. Consiglia quindi quali dispositivi includere nella distribuzione pilota. La distribuzione pilota consigliata include dispositivi con diverse configurazioni hardware e una o più istanze di tutte le app critiche e importanti. Se un'app è contrassegnata come critica, il servizio consiglia più dispositivi con tale app nel progetto pilota.

## <a name="deployment-plans-in-configuration-manager"></a>Piani di distribuzione in Configuration Manager

Dopo aver creato un piano di distribuzione, usare Configuration Manager per distribuire i prodotti. Quando la distribuzione viene avviata, Desktop Analytics la monitora in base alle impostazioni del piano.

## <a name="next-steps"></a>Passaggi successivi

- [Informazioni sugli asset di Desktop Analytics](about-assets.md): dispositivi, driver e app  

- [Informazioni sugli aggiornamenti della sicurezza e delle funzionalità](about-updates.md)  

- [Creare un piano di distribuzione](create-deployment-plans.md)  
