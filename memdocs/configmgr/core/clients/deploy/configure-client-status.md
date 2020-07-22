---
title: Configurare lo stato del client
titleSuffix: Configuration Manager
description: Selezionare le impostazioni relative allo stato del client in Configuration Manager.
ms.date: 07/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a2275ba2-c83d-43e7-90ed-418963a707fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a352e53a672f7fb47416214884fe7adf0fb829cc
ms.sourcegitcommit: 488db8a6ab272f5d639525d70718145c63d0de8f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/14/2020
ms.locfileid: "86384911"
---
# <a name="how-to-configure-client-status-in-configuration-manager"></a>Come configurare lo stato del client in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Prima di poter monitorare i client di Configuration Manager e risolvere i problemi, è necessario configurare le impostazioni stato client del sito. Con queste impostazioni si specificano i parametri usati per contrassegnare i client come inattivi. Configurare anche le opzioni che consentono di ricevere un avviso se l'attività del client scende sotto una specifica soglia.

## <a name="configure-client-status"></a>Configurare lo stato del client

1. Nella console di Configuration Manager passare all'area di lavoro **Monitoraggio** e selezionare il nodo **Stato client**. Nella scheda **Home** della barra multifunzione selezionare **Impostazioni stato client** nel gruppo **Stato client**.

1. Configurare le seguenti impostazioni:

    > [!NOTE]
    > Se un client non soddisfa nessuna delle impostazioni, il sito lo contrassegna come inattivo.

    - **Richieste di criteri client nei seguenti giorni:** Specificare il numero di giorni dalla richiesta di criteri client da parte del sito. Il valore predefinito è `7` giorni.

      Confrontare questo valore con l'impostazione **Intervallo di polling dei criteri client** disponibile nel gruppo di impostazioni client **Criteri client**. Il valore predefinito è 60 minuti. In altre parole, un client deve eseguire il polling dei criteri nel sito a intervalli di un'ora. Se dopo una settimana il client non ha ancora eseguito la richiesta dei criteri, il sito lo contrassegna come inattivo.

    - **Individuazione heartbeat nei seguenti giorni:** Specificare il numero di giorni dall'invio del record di individuazione heartbeat al sito da parte del client. Il valore predefinito è `7` giorni.

      Confrontare questo valore con la pianificazione relativa al [Metodo di individuazione heartbeat](../../servers/deploy/configure/about-discovery-methods.md). Per impostazione predefinita, il sito esegue l'individuazione heartbeat a intervalli settimanali.

    - **Inventario hardware nei seguenti giorni:** Specificare il numero di giorni dall'invio del record di inventario hardware al sito da parte del client. Il valore predefinito è `7` giorni.

      Confrontare questo valore con l'impostazione **Pianificazione inventario hardware** disponibile nel gruppo di impostazioni **Inventario hardware**. Il valore predefinito è sette giorni.

    - **Inventario software nei seguenti giorni:** Specificare il numero di giorni dall'invio del record di inventario software al sito da parte del client. Il valore predefinito è `7` giorni.

      Confrontare questo valore con l'impostazione **Pianificare inventario software e raccolta file**  disponibile nel gruppo di impostazioni **Inventario software**. Il valore predefinito è sette giorni.

    - **Messaggi di stato nei seguenti giorni:** Specificare il numero di giorni dall'invio di eventuali messaggi di stato al sito da parte del client. Il valore predefinito è `7` giorni. Il client può inviare messaggi di stato per diversi tipi di attività, inclusa l'esecuzione di una sequenza di attività. Il sito elimina i messaggi di stato obsoleti nell'ambito dell'attività di manutenzione **Elimina messaggi di stato obsoleti**.

1. Specificare il valore seguente per determinare il periodo di conservazione dei dati di cronologia dello stato del client:

    - **Conservare la cronologia dello stato client per il seguente numero di giorni:** Per impostazione predefinita, il sito mantiene le informazioni sullo stato del client per `31` giorni. Questa impostazione non incide in un alcun modo sul comportamento del client o del sito, ma può essere paragonata a un'attività di manutenzione relativa alla cronologia dello stato del client.

## <a name="configure-the-schedule"></a>Configurare la pianificazione

1. Nella console di Configuration Manager passare all'area di lavoro **Monitoraggio** e selezionare il nodo **Stato client**. Nella scheda **Home** della barra multifunzione selezionare **Pianifica aggiornamento stato client** nel gruppo **Stato client**.

1. Configurare l'intervallo con cui si vuole aggiornare lo stato del client.

    > [!NOTE]
    > Quando si modifica la pianificazione degli aggiornamenti dello stato del client, la nuova pianificazione entra in vigore solo dopo il successivo aggiornamento dello stato del client (in base alla pianificazione precedente).

## <a name="configure-alerts"></a>Configurare gli avvisi

1. Nella console di Configuration Manager passare all'area di lavoro **Asset e conformità** e selezionare il nodo **Raccolte dispositivi**.

1. Selezionare la raccolta per cui si vuole configurare gli avvisi. Nella scheda **Home** della barra multifunzione selezionare **Proprietà** nel gruppo **Proprietà**.

    > [!NOTE]
    > non è possibile configurare avvisi per raccolte di utenti.

1. Passare alla scheda **Avvisi** e selezionare **Aggiungi**.

   > [!TIP]
   > È possibile visualizzare la scheda **Avvisi** solo se il ruolo di sicurezza a cui si è associati dispone delle autorizzazioni per gli avvisi.

    Scegliere gli avvisi che si vuole vengano generati dal sito in funzione delle soglie di stato del client e selezionare **OK**.

1. Nell'elenco **Condizioni** della scheda **Avvisi** selezionare ogni avviso relativo allo stato del client e quindi specificare le informazioni seguenti:

    - **Nome avviso**: accettare il nome predefinito o immettere un nome nuovo per l'avviso.

    - **Gravità avviso**: scegliere il livello di avviso visualizzato dalla console di Configuration Manager.

    - **Genera avviso**: specificare la percentuale di soglia per l'avviso.

## <a name="automatic-remediation-exclusion"></a>Esclusione da monitoraggio e aggiornamento automatici

1. Aprire l'editor del Registro di sistema nel computer client in cui si vuole disattivare il monitoraggio e aggiornamento automatici.

    > [!WARNING]
    > L'uso non corretto dell'editor del Registro di sistema può provocare gravi problemi che potrebbero richiedere la reinstallazione di Windows. Non è garantita la risoluzione di eventuali problemi derivanti dall'uso errato dell'editor del Registro di sistema, che viene quindi usato dall'utente a proprio rischio.

1. Passare alla chiave del registro di sistema **HKEY_LOCAL_MACHINE\Software\Microsoft\CCM\CcmEval**.

1. Modificare il valore della voce **NotifyOnly**:

    - `TRUE`: Il client non correggerà automaticamente eventuali problemi rilevati. L'utente riceverà tuttavia un avviso nell'area di lavoro **Monitoraggio** in caso di problemi con il client.

    - `FALSE`: È l'impostazione predefinita. Il client corregge automaticamente eventuali problemi rilevati durante la ricerca e l'utente riceve un avviso nell'area di lavoro **Monitoraggio**.

Quando si installano i client, è possibile escluderli dai processi di monitoraggio e aggiornamento automatici con la proprietà di installazione **NotifyOnly**. Per altre informazioni, vedere [Proprietà di installazione client](about-client-installation-properties.md).

## <a name="next-steps"></a>Passaggi successivi

[Monitorare i client](../manage/monitor-clients.md)
