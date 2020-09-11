---
title: Creare distribuzioni in fasi
titleSuffix: Configuration Manager
description: Usare distribuzioni in più fasi per automatizzare l'implementazione del software in diverse raccolte.
ms.date: 08/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: b634ff68-b909-48d2-9e2c-0933486673c5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 71e7f9c23b55beecc98bffb5da73465f0681a4a4
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/09/2020
ms.locfileid: "89606389"
---
# <a name="create-phased-deployments-with-configuration-manager"></a>Creare distribuzioni in più fasi con Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Le distribuzioni in più fasi automatizzano un'implementazione del software coordinata e in sequenza in più raccolte. È possibile, ad esempio, distribuire il software in una raccolta pilota e quindi continuare automaticamente l'implementazione in base ai criteri di superamento. È possibile creare distribuzioni in più fasi con l'impostazione predefinita di due fasi oppure configurare manualmente più fasi.

Creare distribuzioni in più fasi per gli oggetti seguenti:

- **Sequenza di attività**
  - La distribuzione in più fasi delle sequenze di attività non supporta l'installazione di PXE o di supporti
- **Applicazione** <!--1358147-->  
- **Aggiornamento software** <!--1358146-->  
  - Non è possibile usare una regola di distribuzione automatica con una distribuzione in più fasi

## <a name="prerequisites"></a>Prerequisiti

### <a name="security-scope"></a>Ambito di protezione

Le distribuzioni create da distribuzioni in più fasi non sono visualizzabili per l'utente amministratore che non ha l'ambito di protezione **Tutto**. Per altre informazioni, vedere [Ambiti di protezione](../../core/understand/fundamentals-of-role-based-administration.md#bkmk_PlanScope).

### <a name="distribute-content"></a>Distribuire il contenuto

Prima di creare una distribuzione in più fasi, distribuire il contenuto associato in un punto di distribuzione.<!--518293-->  

- **Applicazione**: selezionare l'applicazione di destinazione nella console e usare l'azione **Distribuisci contenuto** nella barra multifunzione. Per altre informazioni, vedere [Distribuire e gestire contenuto](../../core/servers/deploy/configure/deploy-and-manage-content.md).

- **Sequenza di attività**: è necessario creare oggetti con riferimenti come il pacchetto di aggiornamento del sistema operativo prima di creare la sequenza di attività. Distribuire questi oggetti prima di creare una distribuzione. Usare l'azione **Distribuisci contenuto** per ogni oggetto o la sequenza di attività. Per visualizzare lo stato di tutti i contenuti con riferimenti, selezionare la sequenza di attività e passare alla scheda **Riferimenti** nel riquadro dei dettagli. Per altre informazioni, vedere il tipo di oggetto in [Preparativi per la distribuzione del sistema operativo](../get-started/prepare-for-operating-system-deployment.md).

- **Aggiornamento software**: creare il pacchetto di distribuzione e distribuirlo. Usare il Download guidato degli aggiornamenti software. Per altre informazioni, vedere [Scaricare gli aggiornamenti software](../../sum/deploy-use/download-software-updates.md).  

## <a name="phase-settings"></a><a name="bkmk_settings"></a> Impostazioni delle fasi

Queste impostazioni sono univoche per le distribuzioni in più fasi. Configurare queste impostazioni durante la creazione o la modifica delle fasi per controllare la pianificazione e il comportamento del processo di distribuzione in più fasi.

A partire dalla versione 2002, usare i cmdlet di Windows PowerShell seguenti per configurare manualmente le fasi per le distribuzioni in più fasi di aggiornamenti software e sequenze di attività:

- [New-CMSoftwareUpdatePhase](/powershell/module/configurationmanager/new-cmsoftwareupdatephase)
- [New-CMTaskSequencePhase](/powershell/module/configurationmanager/new-cmtasksequencephase)

### <a name="criteria-for-success-of-the-first-phase"></a>Criteri per l'esito positivo della prima fase

- **Percentuale di esiti positivi della distribuzione**: specificare la percentuale di dispositivi che devono completare la distribuzione per la riuscita della prima fase. Per impostazione predefinita, questo valore è impostato su 95%. In altre parole, il sito considera la prima fase riuscita quando lo stato di conformità del 95% dei dispositivi è **Riuscito** per questa distribuzione. Il sito procede quindi alla seconda fase e crea una distribuzione del software nella raccolta successiva.

- **Numero di dispositivi distribuiti correttamente**: specificare il numero di dispositivi che devono completare la distribuzione per la riuscita della prima fase. Questa opzione è utile quando le dimensioni della raccolta sono variabili ed è necessario verificare l'esito positivo per un numero specifico di dispositivi prima di passare alla fase successiva. <!--3555946-->

### <a name="conditions-for-beginning-second-phase-of-deployment-after-success-of-the-first-phase"></a>Condizioni per l'inizio della seconda fase della distribuzione dopo la riuscita della prima fase  

- **Inizia automaticamente questa fase dopo un periodo di differimento (in giorni)** : scegliere il numero di giorni di attesa prima di iniziare la seconda fase dopo l'esito positivo della prima. Per impostazione predefinita, questo valore è un giorno.  

- **Inizia manualmente la seconda fase della distribuzione**: il sito non inizia automaticamente la seconda fase dopo la riuscita della prima fase. Questa opzione richiede l'avvio manuale della seconda fase. Per altre informazioni, vedere [Passare alla fase successiva](manage-monitor-phased-deployments.md#bkmk_move).  

    > [!Note]  
    > Questa opzione non è disponibile per le distribuzioni in più fasi delle applicazioni.  

### <a name="gradually-make-this-software-available-over-this-period-of-time-in-days"></a>Rendere gradualmente disponibile il software in questo periodo di tempo (in giorni)
<!--1358578-->
Configurare questa impostazione affinché l'implementazione in ogni fase avvenga gradualmente. Questo comportamento consente di ridurre il rischio di problemi di distribuzione e diminuisce il carico sulla rete causato dalla distribuzione di contenuto nei client. Il sito rende gradualmente disponibile il software a seconda della configurazione per ogni fase. Tutti i client in una fase hanno una scadenza definita in base al momento in cui il software viene reso disponibile. L'intervallo di tempo tra l'ora di disponibilità e la scadenza è uguale per tutti i client in una fase. Il valore predefinito di questa impostazione è zero, ovvero la distribuzione non è limitata per impostazione predefinita. Non impostare un valore maggiore di 30.<!--SCCMDocs-pr issue 2767-->

![Criteri di distribuzione in più fasi per le impostazioni di esito positivo](media/phased-deployment-criteria-for-success.png)

### <a name="configure-the-deadline-behavior-relative-to-when-the-software-is-made-available"></a>Configurare il comportamento della scadenza rispetto al momento in cui viene reso disponibile il software

- **L'installazione è obbligatoria non appena possibile**: imposta come scadenza per l'installazione nel dispositivo il momento in cui il dispositivo viene incluso.  

- **L'installazione è obbligatoria dopo questo periodo di tempo**: imposta la scadenza per l'installazione su un determinato numero di giorni dopo l'inclusione del dispositivo. Per impostazione predefinita, questo valore è 7 giorni.

## <a name="automatically-create-a-default-two-phase-deployment"></a><a name="bkmk_auto"></a> Creare automaticamente una distribuzione predefinita in due fasi

1. Avviare la procedura guidata Crea una distribuzione in più fasi nella console di Configuration Manager. Questa azione varia in base al tipo di software da distribuire:  

    - **Applicazione**: passare a **Raccolta software**, espandere **Gestione applicazioni** e selezionare **Applicazioni**. Selezionare un'applicazione esistente e quindi scegliere **Crea una distribuzione in più fasi** nella barra multifunzione.  

    - **Aggiornamento software**: passare a **Raccolta software**, espandere **Aggiornamenti software** e selezionare **Tutti gli aggiornamenti software**. Selezionare uno o più aggiornamenti e quindi scegliere **Crea una distribuzione in più fasi** nella barra multifunzione.  

        Questa azione è disponibile per gli aggiornamenti software dai seguenti nodi:  
        - Aggiornamenti software  
            - **Tutti gli aggiornamenti software**  
            - **Gruppi di aggiornamenti software**
        - Manutenzione pacchetti di Windows 10, **Aggiornamenti di tutte le piattaforme Windows 10**  
        - Gestione client di Office 365, **Aggiornamenti di Office 365**  

    - **Sequenza di attività**: passare all'area di lavoro **Raccolta software**, espandere **Sistemi operativi** e selezionare **Sequenze di attività**. Selezionare una sequenza di attività esistente e quindi scegliere **Crea una distribuzione in più fasi** nella barra multifunzione.  

2. Nella pagina **Generale** assegnare alla distribuzione in più fasi un **Nome** e una **Descrizione** (facoltativa), quindi selezionare **Crea automaticamente una distribuzione predefinita in due fasi**.  

3. Selezionare **Sfoglia** e scegliere una raccolta di destinazione per i campi **Prima raccolta** e **Seconda raccolta**. Per una sequenza di attività e per gli aggiornamenti software selezionare le raccolte di dispositivi. Per un'applicazione selezionare le raccolte di utenti o dispositivi. Selezionare **Avanti**.  

    > [!Important]  
    > La procedura guidata Crea una distribuzione in più fasi non segnala all'utente se una distribuzione è potenzialmente ad alto rischio. Per altre informazioni, vedere [Impostazioni per gestire le distribuzioni ad alto rischio](../../core/servers/manage/settings-to-manage-high-risk-deployments.md) e la nota della sezione [Distribuire una sequenza di attività](deploy-a-task-sequence.md).  

4. Nella pagina **Impostazioni** scegliere un'opzione per ogni impostazione di pianificazione. Per altre informazioni, vedere [Impostazioni delle fasi](#bkmk_settings). Al termine, selezionare **Avanti**.  

5. Nella pagina **Fasi** vedere le due fasi create dalla procedura guidata per le raccolte specificate. Selezionare **Avanti**. Queste istruzioni descrivono la procedura per creare automaticamente una distribuzione predefinita in due fasi. La procedura guidata consente di aggiungere, rimuovere, riordinare, modificare o visualizzare le fasi per una distribuzione in più fasi. Per altre informazioni su queste azioni aggiuntive, vedere [Creare una distribuzione in più fasi con fasi configurate manualmente](#bkmk_manual).  

6. Verificare le selezioni nella scheda **Riepilogo** e quindi selezionare **Avanti** per completare la procedura guidata.  

> [!NOTE]
> A partire dal 21 aprile 2020, Office 365 ProPlus viene rinominato come **App di Microsoft 365 per grandi imprese**. Per altre informazioni, vedere [Modifica del nome di Office 365 ProPlus](/deployoffice/name-change). È comunque possibile che il nome precedente venga visualizzato in Configuration Manager e nella documentazione corrispondente mentre la console viene aggiornata.  

A partire dalla versione 2002, usare i cmdlet di Windows PowerShell seguenti per questa attività:

- [New-CMApplicationAutoPhasedDeployment](/powershell/module/configurationmanager/new-cmapplicationautophaseddeployment)
- [New-CMSoftwareUpdateAutoPhasedDeployment](/powershell/module/configurationmanager/new-cmsoftwareupdateautophaseddeployment)
- [New-CMTaskSequenceAutoPhasedDeployment](/powershell/module/configurationmanager/new-cmtasksequenceautophaseddeployment)

## <a name="create-a-phased-deployment-with-manually-configured-phases"></a><a name="bkmk_manual"></a> Creare una distribuzione in più fasi con fasi configurate manualmente
<!--1358148-->

Creare una distribuzione in più fasi con fasi configurate manualmente per una sequenza di attività. Aggiungere fino a 10 fasi aggiuntive dalla scheda **Fasi** della procedura guidata Crea una distribuzione in più fasi.

> [!Note]  
> Al momento non è possibile creare manualmente le fasi per un'applicazione. La procedura guidata crea automaticamente due fasi per le distribuzioni di applicazioni.

1. Avviare la procedura guidata Crea una distribuzione in più fasi per una sequenza di attività o per gli aggiornamenti software.  

1. Nella pagina **Generale** della procedura guidata Crea una distribuzione in più fasi assegnare alla distribuzione in più fasi un **Nome** e una **Descrizione** (facoltativa) e quindi selezionare **Configura manualmente tutte le fasi**.  

1. Nella pagina **Fasi** della procedura guidata Crea una distribuzione in più fasi sono disponibili le azioni seguenti:  

    - **Filtrare** l'elenco di fasi di distribuzione. Immettere una stringa di caratteri per trovare una corrispondenza senza distinzione tra maiuscole e minuscole delle colonne Ordine, Nome o Raccolta.

    - **Aggiungere** una nuova fase:  

        1. Nella pagina **Generale** dell'Aggiunta guidata fasi specificare un **Nome** per la fase e quindi selezionare la **Raccolta di fasi** di destinazione. Le impostazioni aggiuntive in questa pagina sono uguali a quelle usate quando si distribuisce normalmente una sequenza di attività o gli aggiornamenti software.  

        1. Nella pagina **Impostazioni delle fasi** dell'Aggiunta guidata fasi configurare le impostazione di pianificazione e al termine selezionare **Avanti**. Per altre informazioni, vedere [Impostazioni](#bkmk_settings).

            > [!Note]  
            > Non è possibile modificare le impostazioni delle fasi **Percentuale di esiti positivi della distribuzione** o **Numero di dispositivi distribuiti correttamente** nella prima fase. Queste impostazioni si applicano solo alle fasi che hanno una fase precedente.

        1. Le impostazioni nelle pagine **Esperienza utente** e **Punti di distribuzione** dell'Aggiunta guidata fasi sono uguali a quelle usate quando si distribuisce normalmente una sequenza di attività o gli aggiornamenti software.  

        1. Controllare le impostazioni nella pagina **Riepilogo** e quindi completare l'Aggiunta guidata fasi.  

    - **Modifica**: questa azione apre la finestra Proprietà della fase selezionata, le cui schede sono uguali alle pagine dell'Aggiunta guidata fasi.  

    - **Rimuovi**: questa azione elimina la fase selezionata.  

       > [!Warning]  
       > Non viene visualizzata alcuna conferma e non è possibile in alcun modo annullare questa azione.  

    - **Sposta su** o **Sposta giù**: la procedura guidata ordina le fasi in base a come vengono aggiunte. La fase aggiunta più di recente è l'ultima nell'elenco. Per modificare l'ordine, selezionare una fase e quindi usare uno di questi pulsanti per spostare la posizione della fase nell'elenco.  

       > [!Important]  
       > Dopo aver modificato l'ordine, controllare le impostazioni delle fasi. Verificare che le impostazioni seguenti siano ancora coerenti con i requisiti per la distribuzione in più fasi:  
       >
       > - Criteri per la riuscita della fase precedente  
       > - Condizioni per l'inizio di questa fase della distribuzione dopo l'esito positivo della fase precedente

1. Selezionare **Avanti**. Controllare le impostazioni nella pagina **Riepilogo** e quindi completare la procedura guidata Crea una distribuzione in più fasi.

A partire dalla versione 2002, usare i cmdlet di Windows PowerShell seguenti per questa attività:

- [New-CMSoftwareUpdateManualPhasedDeployment](/powershell/module/configurationmanager/new-cmsoftwareupdatemanualphaseddeployment)
- [New-CMTaskSequenceManualPhasedDeployment](/powershell/module/configurationmanager/new-cmtasksequencemanualphaseddeployment)

Dopo aver creato una distribuzione in più fasi, aprirne le proprietà per apportare le modifiche:  

- **Aggiungere** fasi aggiuntive a una distribuzione in più fasi esistente.  

- Se una fase non è attiva, è possibile **modificarla**, **rimuoverla** o **spostarla** verso l'alto o verso il basso. Non è possibile spostarla prima di una fase attiva.  

- Quando una fase è attiva, è di sola lettura. Non è possibile modificarla, rimuoverla o spostarne la posizione nell'elenco. L'unica opzione consiste nel **visualizzare** le proprietà della fase.  

- Una distribuzione in più fasi di un'applicazione è sempre di sola lettura.  

## <a name="next-steps"></a>Passaggi successivi

Gestire e monitorare le distribuzioni in più fasi:

- [Applicazione](manage-monitor-phased-deployments.md?toc=/mem/configmgr/apps/toc.json&bc=/mem/configmgr/apps/breadcrumb/toc.json)
- [Aggiornamento software](manage-monitor-phased-deployments.md?toc=/mem/configmgr/sum/toc.json&bc=/mem/configmgr/sum/breadcrumb/toc.json)  
- [Sequenza di attività](manage-monitor-phased-deployments.md)  
