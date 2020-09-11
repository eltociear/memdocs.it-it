---
title: Usare finestre di manutenzione
titleSuffix: Configuration Manager
description: Usare le raccolte e le finestre di manutenzione per gestire in modo efficace i client in Configuration Manager.
ms.date: 06/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4564ebcb-41a8-4eb0-afdb-2e1f0795cfa2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 884adddf8eb469bb0b21c48d239d48b04a530f44
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/09/2020
ms.locfileid: "89607952"
---
# <a name="how-to-use-maintenance-windows-in-configuration-manager"></a>Come usare le finestre di manutenzione in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Le finestre di manutenzione consentono di definire quando Configuration Manager può eseguire attività con impatto sui dispositivi. È possibile usare le finestre di manutenzione per garantire che le modifiche alla configurazione client vengano eseguite quando non influiscono sulla produttività. In Software Center gli utenti possono visualizzare la finestra di manutenzione successiva del dispositivo nella scheda **Stato dell'installazione**. <!--1358131-->

Le finestre di manutenzione sono supportate dalle attività seguenti:

- Distribuzioni di applicazioni e pacchetti

- Distribuzioni di aggiornamenti software

- Distribuzione e valutazione delle impostazioni di conformità

- Distribuzioni del sistema operativo e di sequenze di attività personalizzate

Configurare le finestre di manutenzione con una data di inizio, un'ora di inizio e di fine e un criterio di ricorrenza. La durata massima di una finestra deve essere inferiore a 24 ore. La console non consente una singola finestra di manutenzione superiore a 24 ore. Se ad esempio si vuole consentire la manutenzione per tutta la giornata sabato e domenica, creare due finestre di manutenzione di 24 ore per ogni giorno.<!-- MEMDocs#310 -->

Per impostazione predefinita, i riavvii del computer causati da una distribuzione non sono consentiti al di fuori di una finestra di manutenzione, ma è possibile eseguire l'override di questa impostazione. Le finestre di manutenzione interessano solo il momento in cui viene eseguita la distribuzione. Le distribuzioni configurate per il download e l'esecuzione in locale possono scaricare contenuto al di fuori della finestra.

Quando un client è membro di una raccolta di dispositivi a cui è associata una finestra di manutenzione, una distribuzione viene eseguita solo se il tempo di esecuzione massimo consentito non supera la durata della finestra. Se non è possibile eseguire la distribuzione, il client genera un avviso e quindi esegue nuovamente la distribuzione durante la successiva finestra di manutenzione pianificata con tempo disponibile.

## <a name="multiple-maintenance-windows"></a>Uso di più finestre di manutenzione

Quando un computer client appartiene a più raccolte dispositivi con finestre di manutenzione, vengono applicate queste regole:  

- Se le finestre di manutenzione non si sovrappongono, il client le considera come due finestre indipendenti.

- Se le finestre di manutenzione si sovrappongono, il client le considera come una singola finestra per l'intero tempo di entrambe le finestre. Vengono create ad esempio due finestre di manutenzione in una raccolta. La prima è valida dalle 6.00 alle 7.00 e la seconda dalle 6.30 alle 7.30. Poiché le finestre si sovrappongono per 30 minuti, la durata effettiva della finestra di manutenzione combinata è di 90 minuti, dalle 6.00 alle 7.30.

Quando un utente installa un'applicazione da Software Center, l'applicazione viene avviata immediatamente dal client. Viene assegnata la priorità alla finalità dell'utente rispetto a quella dell'amministratore.

Se la distribuzione di un'applicazione con scopo **Richiesto** raggiunge la scadenza dell'installazione durante l'orario non lavorativo configurato da un utente in Software Center, il client installa l'applicazione assegnando la priorità alla finalità dell'amministratore rispetto a quella dell'utente.

Per impostazione predefinita, quando sono presenti più finestre di manutenzione, il client installa solo gli aggiornamenti software durante le finestre di tipo **Aggiornamento software**, ignorando tutte le finestre di manutenzione di tipo **Tutte le distribuzioni**, a meno che non siano l'unico tipo. È possibile configurare questo comportamento con l'impostazione client seguente nel gruppo **Aggiornamenti software**: **Consenti l'installazione degli aggiornamenti software nella finestra di manutenzione "Tutte le distribuzioni" quando la finestra di manutenzione "Aggiornamento software" è disponibile**. Per altre informazioni, vedere [About client settings](../../deploy/about-client-settings.md#bkmk_SUMMaint) (Informazioni sulle impostazioni client).<!-- SCCMDocs#1317 -->

> [!NOTE]
> Questa impostazione si applica anche alle finestre di manutenzione configurate per l'applicazione a **Sequenze di attività**.<!-- SCCMDocs-pr #4596 -->
>
> Se ha una sola finestra **Tutte le distribuzioni** disponibile, il client installa comunque gli aggiornamenti software o le sequenze di attività nella finestra.

## <a name="configure-maintenance-windows"></a>Configurare le finestre di manutenzione

1. Nella console di Configuration Manager passare all'area di lavoro **Asset e conformità**.

1. Selezionare il nodo **Raccolte dispositivi** e quindi selezionare una raccolta.

    > [!NOTE]
    > Non è possibile creare finestre di manutenzione per la raccolta **Tutti i sistemi**.

1. Nella scheda **Home** della barra multifunzione scegliere **Proprietà** nel gruppo **Proprietà**.

1. Passare alla scheda **Finestre di manutenzione** e quindi selezionare l'icona **Nuovo**.

    1. Specificare un valore nel campo **Nome** per identificare in modo univoco la finestra di manutenzione per la raccolta.

    1. Configurare le impostazioni per **Ora**:

        - **Data di validità**: data di inizio della finestra di manutenzione. L'impostazione predefinita è la data corrente.

        - **Inizio** e **Fine**: Ora di inizio e di fine della finestra di manutenzione. Tali opzioni consentono di calcolare il valore del campo **Durata** per la finestra. La durata minima è cinque minuti, mentre la massima è 24 ore. La durata predefinita è di tre ore, dalle 01.00 alle 04.00.

        - **UTC (Coordinated Universal Time)** : abilitare questa opzione in modo che il client interpreti le ore di inizio e di fine nel fuso orario UTC. Per i dispositivi distribuiti a livello di area o globale nella stessa raccolta, questa opzione imposta la finestra di manutenzione in modo che venga eseguita contemporaneamente in tutti i dispositivi della raccolta. Disabilitare questa opzione in modo che il client usi il fuso orario locale del dispositivo. Questa opzione è disabilitata per impostazione predefinita.

    1. Configurare il criterio di ricorrenza. Il valore predefinito è una volta alla settimana nel giorno corrente della settimana.

    1. **Applica questa pianificazione a**: per impostazione predefinita, la finestra si applica all'opzione **Tutte le distribuzioni**. È possibile selezionare **Aggiornamenti software** o **Sequenze attività** per controllare ulteriormente le distribuzioni eseguite durante questa finestra.

        > [!TIP]
        > Se si configurano più finestre di manutenzione di tipi diversi nella stessa raccolta, verificare di comprendere i comportamenti del client. Per altre informazioni, vedere [Uso di più finestre di manutenzione](#multiple-maintenance-windows).

1. Selezionare **OK** per salvare e chiudere la finestra.

Nella scheda **Finestre di manutenzione** delle proprietà della raccolta vengono visualizzate tutte le finestre configurate.

## <a name="use-powershell"></a><a name="bkmk_powershell"></a> Usare PowerShell

È possibile usare PowerShell per configurare le finestre di manutenzione. Per altre informazioni, vedere gli articoli seguenti:

- [Get-CMMaintenanceWindow](/powershell/module/configurationmanager/get-cmmaintenancewindow)
- [New-CMMaintenanceWindow](/powershell/module/configurationmanager/new-cmmaintenancewindow)
- [Remove-CMMaintenanceWindow](/powershell/module/configurationmanager/remove-cmmaintenancewindow)
- [Set-CMMaintenanceWindow](/powershell/module/configurationmanager/set-cmmaintenancewindow)