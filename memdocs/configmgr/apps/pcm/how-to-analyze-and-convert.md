---
title: Come analizzare e convertire i pacchetti
titleSuffix: Configuration Manager
description: Informazioni su come analizzare e convertire i pacchetti con Package Conversion Manager in Configuration Manager.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: f3bf1737-827d-48fa-8bb1-f48fe71afe0c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f72e7330909bc5653e69790e38ae043e539cc239
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689039"
---
# <a name="how-to-analyze-and-convert-packages-with-package-conversion-manager"></a>Come analizzare e convertire i pacchetti con Package Conversion Manager

*Si applica a: Configuration Manager (Current Branch)*

<!--1357861-->

Prima di convertire un pacchetto, è necessario analizzarlo. In base ai risultati dell'analisi, è quindi possibile eseguire una delle operazioni seguenti:

- **Convertire** il pacchetto in un'applicazione. Nell'elenco **Pacchetto** della console lo stato di conformità è **Automatico**.  

- **Correggere e convertire** il pacchetto, collegare le raccolte e creare condizioni globali. Nell'elenco **Pacchetto** della console lo stato di conformità è **Automatico**.  

- **Correggere e convertire** il pacchetto. Nell'elenco **Pacchetto** della console lo stato di conformità è **Manuale**.  

- Lasciare il pacchetto non convertito. Nell'elenco **Pacchetto** della console lo stato di conformità è **Non applicabile**.  



## <a name="how-to-analyze-packages"></a><a name="bkmk_analyze"></a> Come analizzare i pacchetti

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**. Espandere **Gestione applicazioni** e selezionare il nodo **Pacchetti**.  

2. Selezionare il pacchetto da convertire. Nella scheda **Home** della barra multifunzione selezionare **Analyze Package** (Analizza pacchetto) nel gruppo **Conversione pacchetti**. Package Conversion Manager analizza il pacchetto.  

3. Per visualizzare lo stato di conformità del pacchetto, aggiungere la colonna **Conformità** all'elenco di pacchetti. Lo stato di conformità del pacchetto determina l'operazione successiva:  

    - **Automatico**: [Come convertire i pacchetti](#bkmk_convert)  

        Se si vuole anche collegare raccolte e creare condizioni globali con uno stato di conformità **Automatico**, vedere [Come correggere e convertire i pacchetti](#bkmk_fix).  

    - **Manuale**: [Come correggere e convertire i pacchetti](#bkmk_fix)

    - **Non applicabile**: un programma o il contenuto richiesto non è presente nel pacchetto. Aggiungere eventuali contenuti o programmi mancanti e ripetere l'analisi. In alternativa, lasciare il pacchetto in uno stato non convertito e continuare a distribuirlo come pacchetto.  

    - **Sconosciuto**: Eseguire prima l'attività **Analizza** oppure attendere la successiva analisi pianificata. Se lo stato non cambia, vedere [Risolvere i problemi di Package Conversion Manager](troubleshoot-pcm.md).<!-- SCCMDocs#2044 -->

## <a name="how-to-convert-packages"></a><a name="bkmk_convert"></a> Come convertire i pacchetti

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**. Espandere **Gestione applicazioni** e selezionare il nodo **Pacchetti**.  

2. Selezionare il pacchetto da convertire con uno stato di conformità **Automatico**. Nella scheda **Home** della barra multifunzione selezionare **Converti pacchetto** nel gruppo **Conversione pacchetti**. Verrà visualizzata la procedura guidata Converti il pacchetto in applicazione.  

3. Nella procedura guidata Converti il pacchetto in applicazione esaminare l'elenco dei pacchetti selezionati. Rimuovere eventuali pacchetti che non si vuole convertire e selezionare **OK**. Package Conversion Manager converte il pacchetto. Nella finestra Conversione completata viene visualizzato lo stato di conversione delle nuove applicazioni.  

    > [!Note]  
    > Quando si converte un pacchetto, il sito registra la data e l'ora della conversione in formato UTC.  

4. Seguire le istruzioni nella finestra. Selezionare **Visualizza applicazioni** o **Chiudi**.  



## <a name="how-to-fix-and-convert-packages"></a><a name="bkmk_fix"></a> Come correggere e convertire i pacchetti

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**. Espandere **Gestione applicazioni** e selezionare il nodo **Pacchetti**.  

2. Selezionare un pacchetto con uno stato di conformità **Manuale** o **Automatico**. Nella scheda **Home** della barra multifunzione selezionare **Correggi e converti** nel gruppo **Conversione pacchetti**.  

3. Nella Conversione guidata pacchetti esaminare le informazioni nella pagina **Selezione pacchetto** analizzando quanto indicato in **Items to Fix** (Elementi da correggere). Selezionare quindi **Avanti**.  

4. Nella pagina **Esame delle dipendenze** verificare se il pacchetto dipende da altri pacchetti elencati e quindi selezionare **Avanti**.  

    > [!Note]  
    > Se i pacchetti dipendenti elencati non sono ancora stati convertiti, convertire prima di tutto tali pacchetti. Riavviare quindi il processo di conversione dei pacchetti.  
    >  
    > Se una dipendenza non è necessaria, eliminarla oppure ignorarla e continuare la conversione.  

5. Nella pagina **Tipo di distribuzione** esaminare i tipi di distribuzione per la nuova applicazione. Modificare le priorità o eliminare i tipi di distribuzione.  

6. Se uno dei nuovi tipi di distribuzione non ha un metodo di rilevamento associato, nella colonna **Metodo di rilevamento** viene visualizzata un'icona di avviso. Completare le operazioni seguenti:  

    1. Selezionare **Modifica il metodo di rilevamento**.  

    2. Selezionare **Aggiungi**.  

    3. Nella finestra di dialogo Regola di rilevamento specificare un valore per **Tipo di impostazione**.  

    4. Per il tipo di impostazione specificato immettere le informazioni aggiuntive necessarie per la regola di rilevamento.  

    5. Selezionare **OK**. Se necessario, ripetere questo processo per aggiungere più metodi di rilevamento per ogni tipo di distribuzione.  

    6. Selezionare **OK**. Verificare che nella colonna **Metodo di rilevamento** sia presente un'icona per confermare un metodo di rilevamento specificato correttamente.  

7. Selezionare **Avanti**.  

8. Nella pagina **Selezione dei requisiti** esaminare i tipi di distribuzione della nuova applicazione. Selezionare un tipo di distribuzione ed esaminare i relativi requisiti.  

    > [!Note]  
    > La procedura guidata mostra solo i requisiti convertiti da Package Conversion Manager. Non vengono convertite tutte le query WQL delle raccolte di dispositivi in requisiti.  

9. Aggiungere i requisiti per un tipo di distribuzione, se necessario.  

10. Selezionare **Avanti**.  

11. Completare la procedura guidata per creare l'applicazione.  

    > [!Note]  
    > Quando si converte un pacchetto, il sito registra la data e l'ora della conversione in formato UTC.  



## <a name="monitor"></a><a name="bkmk_monitor"></a> Monitoraggio

Passare all'area di lavoro **Monitoraggio** della console di Configuration Manager e selezionare **Stato della conversione pacchetti**. Questo dashboard mostra l'analisi globale e lo stato di conversione dei pacchetti nel sito. Una nuova attività in background sintetizza automaticamente i dati di analisi.

> [!Tip]  
> Package Conversion Manager integrato con Configuration Manager non richiede la pianificazione dell'analisi dei pacchetti. Questa operazione viene gestita dall'attività di riepilogo integrata.

![Screenshot del dashboard Stato della conversione pacchetti di esempio](media/1357861-pcm-dashboard.png)
