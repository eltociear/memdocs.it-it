---
title: Eseguire il debug di una sequenza di attività
titleSuffix: Configuration Manager
description: Usare lo strumento di debug delle sequenza di attività per risolvere i problemi relativi a una sequenza di attività.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 4b60b0e1-ffa4-4fd5-864e-70a0546c8b3b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 66f460b7ba5c870a9ee81d10835ceb9f660cba89
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690609"
---
# <a name="debug-a-task-sequence"></a>Eseguire il debug di una sequenza di attività

*Si applica a: Configuration Manager (Current Branch)*

<!--3612274-->

A partire dalla versione 1906, il debugger di sequenze di attività è un nuovo strumento per la risoluzione dei problemi. Si distribuisce una sequenza di attività in modalità di debug in una piccola raccolta. Consente di esaminare la sequenza di attività in modo controllato per facilitare la risoluzione dei problemi e l'analisi. Il debugger viene attualmente eseguito nello stesso dispositivo del motore della sequenza di attività, non è un debugger remoto.

> [!Note]  
> In questa versione di Configuration Manager il debugger delle sequenze di attività è una funzionalità di versione non definitiva. Per abilitarla, vedere [Funzionalità di versioni non definitive in System Center Configuration Manager](../../core/servers/manage/pre-release-features.md).  


## <a name="prerequisites"></a>Prerequisiti

- Aggiornare il client di Configuration Manager nel dispositivo di destinazione

- Accedere al dispositivo di destinazione come utente nel gruppo **Amministratori** locale. Il debugger viene eseguito solo per gli amministratori.

- Aggiornare l'immagine di avvio associata alla sequenza di attività per assicurarsi che la versione del client sia la più recente


## <a name="start-the-tool"></a>Avvia lo strumento

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**, espandere **Sistemi operativi** e selezionare **Sequenze di attività**.

1. Selezionare una sequenza di attività. Nel gruppo di distribuzione della barra multifunzione selezionare **Debug**.

    > [!Tip]  
    > In alternativa, impostare la variabile **TSDebugMode** su `TRUE` per una raccolta o un oggetto computer a cui viene distribuita la sequenza di attività. In tutti i dispositivi con questa variabile impostata, qualsiasi sequenza di attività passa in modalità di debug.

1. Creare una distribuzione di debug. Le impostazioni di distribuzione sono le stesse di una normale distribuzione della sequenza di attività. Per altre informazioni, vedere [Deploy a task sequence](deploy-a-task-sequence.md#process).

    > [!Note]  
    > È possibile selezionare solo una piccola raccolta per una distribuzione di debug. Vengono visualizzate solo le raccolte di dispositivi con al massimo 10 membri.

A partire dalla versione 1910, usare la nuova variabile della sequenza di attività **TSDebugOnError** per avviare automaticamente il debugger quando la sequenza di attività restituisce un errore.<!-- 5012536 --> Per altre informazioni, vedere [Variabili della sequenza di attività - TSDebugOnError](../understand/task-sequence-variables.md#TSDebugOnError).

## <a name="use-the-tool"></a>Usare lo strumento

Quando la sequenza di attività viene eseguita nel dispositivo, viene visualizzata la finestra Debugger delle sequenze di attività come mostra lo screenshot seguente:

![Screenshot del debugger di sequenze di attività](media/3612274-tsdebug.png)

Il debugger include i controlli seguenti:

- **Step** (Passaggio): Dalla posizione *corrente* eseguire solo il passaggio successivo nella sequenza di attività.  

    > [!Note]  
    > Quando la sequenza di attività è in modalità di debug, se un passaggio restituisce un errore irreversibile, la sequenza di attività non ha esito negativo come di consueto. Questo comportamento consente di ripetere un passaggio dopo avere apportato una modifica esterna.

- **Esegui**: Dalla posizione *corrente* eseguire normalmente la sequenza di attività fino alla fine o al punto di *interruzione* successivo oppure se un passaggio non viene eseguito. Prima di usare questa azione, assicurarsi di impostare eventuali punti di interruzione con l'azione **Set Break** (Imposta interruzione).

- **Set Current** (Imposta corrente): Selezionare un passaggio nel debugger, quindi selezionare **Set Current** (Imposta corrente). Questa azione sposta il puntatore *corrente* su quel passaggio. Questa azione consente di saltare passaggi o spostarsi all'indietro.  

    > [!Warning]  
    > Il debugger non considera il tipo di passaggio quando si modifica la posizione corrente nella sequenza. Alcuni passaggi possono impostare le variabili della sequenza di attività necessarie per la valutazione della condizione nei passaggi successivi. Se l'ordine di esecuzione non è corretto, alcuni passaggi possono non riuscire o causare danni significativi a un dispositivo. Usare questa opzione a proprio rischio.  

- **Set Break** (Imposta interruzione): Selezionare un passaggio nel debugger, quindi selezionare **Set Break** (Imposta interruzione). Questa azione aggiunge un punto di *interruzione* nel debugger. Durante l'**esecuzione** la sequenza di attività si ferma in corrispondenza di un'*interruzione*.  

    - Prima di usare l'azione **Run** (Esegui), impostare i punti di interruzione.

    - A partire dalla versione 1910, se si crea un punto di interruzione nel debugger e quindi la sequenza di attività riavvia il computer, il debugger mantiene i punti di interruzione dopo il riavvio.<!-- 5012509 -->

    - Nella versione 1906 i punti di interruzione non vengono salvati dopo il riavvio del computer, ad esempio con il passaggio [Riavvia il computer](../understand/task-sequence-steps.md#BKMK_RestartComputer). Se ad esempio si avvia il debugger da Software Center per una sequenza di attività per la creazione di immagini, non impostare interruzioni nella fase di Windows PE. Quando il computer viene riavviato in Windows PE, il debugger sospende la sequenza di attività in modo da consentire l'impostazione delle interruzioni.

- **Cancella tutte le interruzioni**: Consente di rimuovere tutti i punti di interruzione.

- **File di log**: Apre il file di log della sequenza di attività corrente, **smsts.log**, con [CMTrace](../../core/support/cmtrace.md). È possibile visualizzare le voci di log quando il motore della sequenza di attività è "in attesa del debugger".

- **Prompt dei comandi**: In Windows PE apre un prompt dei comandi.

- **Annulla**: Consente di chiudere il debugger e interrompere la sequenza di attività.

- **Quit** (Esci): Consente di scollegare e chiudere il debugger, ma la sequenza di attività continua a essere eseguita normalmente.

La finestra delle **variabili della sequenza di attività** contiene i valori correnti per tutte le variabili nell'ambiente della sequenza di attività. Per altre informazioni, vedere [Variabili della sequenza di attività](../understand/task-sequence-variables.md). Se si usa il passaggio [Imposta variabile della sequenza di attività](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) con l'opzione **Non visualizzare questo valore**, il debugger non visualizza il valore della variabile. Non è possibile modificare i valori delle variabili nel debugger.

> [!Note]
> Alcune variabili della sequenza di attività sono solo per uso interno e non sono elencate nella documentazione di riferimento.

Il debugger delle sequenze di attività continua a essere eseguito dopo un passaggio di [riavvio del computer](../understand/task-sequence-steps.md#BKMK_RestartComputer), ma è necessario ricreare eventuali punti di interruzione. Anche se la sequenza di attività potrebbe non richiederlo, dal momento che il debugger richiede l'interazione dell'utente, è necessario accedere a Windows per continuare. Se non si esegue l'accesso dopo un'ora per continuare il debug, la sequenza di attività ha esito negativo.

Si entra anche in una sequenza di attività figlio con il passaggio di [esecuzione della sequenza di attività](../understand/task-sequence-steps.md#child-task-sequence). La finestra del debugger indica i passaggi della sequenza di attività figlio insieme alla sequenza di attività principale.


## <a name="known-issues"></a>Problemi noti

Se si ha come destinazione una distribuzione normale e una distribuzione di debug nello stesso dispositivo usando più distribuzioni, è possibile che il debugger delle sequenze di attività non venga avviato.


## <a name="see-also"></a>Vedere anche

- [Informazioni sui passaggi della sequenza di attività](../understand/task-sequence-steps.md)
- [Variabili della sequenza di attività](../understand/task-sequence-variables.md)
- [Come usare le variabili della sequenza di attività](../understand/using-task-sequence-variables.md)
- [Distribuire una sequenza di attività](deploy-a-task-sequence.md)
