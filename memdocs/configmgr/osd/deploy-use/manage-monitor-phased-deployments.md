---
title: Gestire e monitorare le distribuzioni in più fasi
titleSuffix: Configuration Manager
description: Informazioni su come gestire e monitorare le distribuzioni in più fasi per il software in Configuration Manager.
ms.date: 08/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: dc245916-bc11-4983-9c4d-015f655007c1
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 631a2fc3cb7df01eed1a5a6af80dd87f84455bdc
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/09/2020
ms.locfileid: "89606334"
---
# <a name="manage-and-monitor-phased-deployments"></a>Gestire e monitorare le distribuzioni in più fasi

Questo articolo descrive come gestire e monitorare le distribuzioni in più fasi. Le attività di gestione comprendono l'avvio manuale della fase successiva e la sospensione o la ripresa di una fase.

È necessario prima creare una distribuzione in più fasi:

- [Applicazione](create-phased-deployment-for-task-sequence.md?toc=/mem/configmgr/apps/toc.json&bc=/mem/configmgr/apps/breadcrumb/toc.json)  
- [Aggiornamento software](create-phased-deployment-for-task-sequence.md?toc=/mem/configmgr/sum/toc.json&bc=/mem/configmgr/sum/breadcrumb/toc.json)  
- [Sequenza di attività](create-phased-deployment-for-task-sequence.md)  

## <a name="move-to-the-next-phase"></a><a name="bkmk_move"></a> Passare alla fase successiva

Quando si seleziona l'impostazione, **Inizia manualmente la seconda fase della distribuzione**, il sito non avvia automaticamente la fase successiva in base ai criteri per l'esito positivo. È necessario spostare la distribuzione in più fasi alla fase successiva.  

1. La modalità di avvio di questa azione varia in base al tipo di software distribuito:  

    - **Applicazione**: passare all'area di lavoro **Raccolta software**, espandere **Gestione applicazioni** e selezionare **Applicazioni**.

    - **Aggiornamento software**: passare all'area di lavoro **Raccolta software** e quindi selezionare uno dei nodi seguenti:
        - Aggiornamenti software  
            - **Tutti gli aggiornamenti software**  
            - **Gruppi di aggiornamenti software**
        - Manutenzione pacchetti di Windows 10, **Aggiornamenti di tutte le piattaforme Windows 10**  
        - Gestione client di Office 365, **Aggiornamenti di Office 365**  

    - **Sequenza di attività**: passare all'area di lavoro **Raccolta software**, espandere **Sistemi operativi** e selezionare **Sequenze di attività**.

2. Selezionare il software con la distribuzione in più fasi.  

3. Nel riquadro dei dettagli passare alla scheda **Distribuzioni in più fasi**.  

4. Selezionare la distribuzione in più fasi e fare clic su **Passa alla fase successiva** nella barra multifunzione.  

    ![Menu di scelta rapida che mostra le azioni per una distribuzione in più fasi](media/Suspend-phased-deployment.PNG)

A partire dalla versione 2002, usare il cmdlet di Windows PowerShell seguente per questa attività: [Move-CMPhasedDeploymentToNext](/powershell/module/configurationmanager/move-cmphaseddeploymenttonext).

## <a name="suspend-and-resume-phases"></a><a name="bkmk_suspend"></a> Sospendere e riprendere le fasi

È possibile sospendere o riprendere manualmente una distribuzione in più fasi. Ad esempio, si crea una distribuzione in più fasi per una sequenza di attività. Durante il monitoraggio della fase nel gruppo pilota si nota un numero elevato di errori. Si sospende la distribuzione in più fasi per impedire ad altri dispositivi di eseguire la sequenza di attività. Dopo la risoluzione del problema si riprende la distribuzione in più fasi per continuare l'implementazione.

1. La modalità di avvio di questa azione varia in base al tipo di software distribuito:  

    - **Applicazione**: passare all'area di lavoro **Raccolta software**, espandere **Gestione applicazioni** e selezionare **Applicazioni**.

    - **Aggiornamento software**: passare all'area di lavoro **Raccolta software** e quindi selezionare uno dei nodi seguenti:
        - Aggiornamenti software  
            - **Tutti gli aggiornamenti software**  
            - **Gruppi di aggiornamenti software**
        - Manutenzione pacchetti di Windows 10, **Aggiornamenti di tutte le piattaforme Windows 10**  
        - Gestione client di Office 365, **Aggiornamenti di Office 365**  

    - **Sequenza di attività**: passare all'area di lavoro **Raccolta software**, espandere **Sistemi operativi** e selezionare **Sequenze di attività**. Selezionare una sequenza di attività esistente e quindi fare clic su **Crea una distribuzione in più fasi** nella barra multifunzione.  

2. Selezionare il software con la distribuzione in più fasi.  

3. Nel riquadro dei dettagli passare alla scheda **Distribuzioni in più fasi**.  

4. Selezionare la distribuzione in più fasi e fare clic su **Sospendi** o su **Riprendi** nella barra multifunzione.

> [!NOTE]
> A partire dal 21 aprile 2020 Office 365 ProPlus viene rinominato come **App di Microsoft 365 per grandi imprese**. Per altre informazioni, vedere [Modifica del nome di Office 365 ProPlus](/deployoffice/name-change). È comunque possibile che il nome precedente venga visualizzato in Configuration Manager e nella documentazione corrispondente mentre la console viene aggiornata.

A partire dalla versione 2002, usare i cmdlet di Windows PowerShell seguenti per questa attività:

- [Suspend-CMPhasedDeployment](/powershell/module/configurationmanager/suspend-cmphaseddeployment)
- [Resume-CMPhasedDeployment](/powershell/module/configurationmanager/resume-cmphaseddeployment)

## <a name="monitor"></a><a name="bkmk_monitor"></a> Monitoraggio
<!--1358577-->

Le distribuzioni in più fasi hanno un nodo di monitoraggio dedicato, che semplifica l'identificazione delle distribuzioni in più fasi create e il passaggio alla visualizzazione di monitoraggio delle distribuzioni in più fasi. Dall'area di lavoro di **monitoraggio** selezionare **Distribuzioni in più fasi** e fare doppio clic su una delle distribuzioni in più fasi per visualizzarne lo stato. <!--3555949-->

![Dashboard dello stato di distribuzione in più fasi che mostra lo stato delle due fasi](media/1358577-phased-deployment-status.png)

Questo dashboard visualizza le informazioni seguenti per ogni fase della distribuzione:  

- **Dispositivi totali** or **Risorse totali**: numero di dispositivi interessati da questa fase.  

- **Status** (Stato): stato corrente della fase. Ogni fase può trovarsi in uno degli stati seguenti:  

  - **La distribuzione è stata creata**: la distribuzione in più fasi ha creato una distribuzione del software nella raccolta per questa fase. Ai client viene assegnato in modo attivo questo software.  

  - **In attesa**: la fase precedente non ha ancora raggiunto i criteri di esito positivo per consentire la continuazione della distribuzione verso questa fase.  

  - **Sospeso**: un amministratore ha sospeso la distribuzione.  

- **Stato**: stati di distribuzione con codifica a colori dai client. Ad esempio: Esito positivo, In corso, Errore, Requisiti non soddisfatti e Sconosciuto.

### <a name="success-criteria-tile"></a>Riquadro Criteri per l'esito positivo

Usare l'elenco a discesa **Selezionare una fase** per modificare la visualizzazione del riquadro **Criteri per l'esito positivo**. Questo riquadro confronta il valore di **Obiettivo della fase** alla conformità corrente della distribuzione. Con le impostazioni predefinite, l'obiettivo della fase è il 95%. Questo valore indica che la distribuzione richiede una conformità del 95% per passare alla fase successiva.

In questo esempio, l'obiettivo della fase è il 65% e la conformità corrente è il 66,7%. La distribuzione in più fasi passa automaticamente alla seconda fase perché la prima fase soddisfa i criteri per l'esito positivo.  

   ![Riquadro Criteri per l'esito positivo di esempio dallo stato della distribuzione in più fasi in cui l'obiettivo è del 65%](media/pod-status-success-criteria-tile.png)

L'obiettivo della fase è lo stesso di **Percentuale di esiti positivi della distribuzione** in Impostazioni delle fasi per la fase *successiva*. Affinché la distribuzione in più fasi inizi la fase successiva, questa seconda fase definisce i criteri per l'esito positivo della prima fase. Per visualizzare questa impostazione:

1. Passare all'oggetto di distribuzione in più fasi sul software e aprire Proprietà della distribuzione in più fasi.  

2. Passare alla scheda **Fasi**. Selezionare **Fase 2** e fare clic su **Visualizza**.  

3. Nella finestra delle proprietà della fase passare alla scheda **Impostazioni delle fasi**.  

4. Visualizzare il valore per **Percentuale di esiti positivi della distribuzione** nel gruppo *Criteri per l'esito positivo della fase precedente*.  

Ad esempio, le proprietà seguenti sono relative alla stessa fase del riquadro dei criteri per l'esito positivo riportato, in cui il criterio è il 65%:  

![Scheda Impostazioni delle fasi nelle proprietà della fase](media/phase-properties-phase-settings.png)

## <a name="powershell"></a>PowerShell

Usare i cmdlet di Windows PowerShell seguenti per gestire le distribuzioni in più fasi:

### <a name="automatically-create-phased-deployments"></a>Creare automaticamente distribuzioni in più fasi

- [New-CMApplicationAutoPhasedDeployment](/powershell/module/configurationmanager/new-cmapplicationautophaseddeployment)
- [New-CMSoftwareUpdateAutoPhasedDeployment](/powershell/module/configurationmanager/new-cmsoftwareupdateautophaseddeployment)
- [New-CMTaskSequenceAutoPhasedDeployment](/powershell/module/configurationmanager/new-cmtasksequenceautophaseddeployment)

### <a name="manually-create-phased-deployments"></a>Creare manualmente distribuzioni in più fasi

- [New-CMSoftwareUpdatePhase](/powershell/module/configurationmanager/new-cmsoftwareupdatephase)
- [New-CMSoftwareUpdateManualPhasedDeployment](/powershell/module/configurationmanager/new-cmsoftwareupdatemanualphaseddeployment)
- [New-CMTaskSequencePhase](/powershell/module/configurationmanager/new-cmtasksequencephase)
- [New-CMTaskSequenceManualPhasedDeployment](/powershell/module/configurationmanager/new-cmtasksequencemanualphaseddeployment)

### <a name="get-existing-phased-deployment-objects"></a>Ottenere oggetti di distribuzione in più fasi esistenti

- [Get-CMApplicationPhasedDeployment](/powershell/module/configurationmanager/get-cmapplicationphaseddeployment)
- [Get-CMSoftwareUpdatePhasedDeployment](/powershell/module/configurationmanager/get-cmsoftwareupdatephaseddeployment)
- [Get-CMTaskSequencePhasedDeployment](/powershell/module/configurationmanager/get-cmtasksequencephaseddeployment)
- [Get-CMPhase](/powershell/module/configurationmanager/get-cmphase)

### <a name="monitor-phased-deployment-status"></a>Monitorare lo stato della distribuzione in più fasi

- [Get-CMPhasedDeploymentStatus](/powershell/module/configurationmanager/get-cmphaseddeploymentstatus)

### <a name="manage-existing-phased-deployments"></a>Gestire distribuzioni in più fasi esistenti

- [Move-CMPhasedDeploymentToNext](/powershell/module/configurationmanager/move-cmphaseddeploymenttonext)
- [Resume-CMPhasedDeployment](/powershell/module/configurationmanager/resume-cmphaseddeployment)
- [Suspend-CMPhasedDeployment](/powershell/module/configurationmanager/suspend-cmphaseddeployment)

### <a name="modify-existing-phased-deployments"></a>Modificare distribuzioni in più fasi esistenti

- [Set-CMApplicationPhasedDeployment](/powershell/module/configurationmanager/set-cmapplicationphaseddeployment)
- [Set-CMSoftwareUpdatePhase](/powershell/module/configurationmanager/set-cmsoftwareupdatephase)
- [Set-CMSoftwareUpdatePhasedDeployment](/powershell/module/configurationmanager/set-cmsoftwareupdatephaseddeployment)
- [Set-CMTaskSequencePhase](/powershell/module/configurationmanager/set-cmtasksequencephase)
- [Set-CMTaskSequencePhasedDeployment](/powershell/module/configurationmanager/set-cmtasksequencephaseddeployment)
- [Remove-CMApplicationPhasedDeployment](/powershell/module/configurationmanager/remove-cmapplicationphaseddeployment)
- [Remove-CMSoftwareUpdatePhasedDeployment](/powershell/module/configurationmanager/remove-cmsoftwareupdatephaseddeployment)
- [Remove-CMTaskSequencePhasedDeployment](/powershell/module/configurationmanager/remove-cmtasksequencephaseddeployment)
