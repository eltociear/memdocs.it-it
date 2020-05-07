---
title: Gruppi di orchestrazione
titleSuffix: Configuration Manager
description: Creare gruppi di orchestrazione e distribuire gli aggiornamenti.
ms.date: 04/28/2020
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: cddbebea-b418-4839-b0a8-7809486c8a4c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e9a307df23900abb985535b2ab59a5ff172cafb7
ms.sourcegitcommit: 0e62655fef7afa7b034ac11d5f31a2a48bf758cb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/29/2020
ms.locfileid: "82254912"
---
# <a name="orchestration-groups-in-configuration-manager"></a>Gruppi di orchestrazione in Configuration Manager
<!--3098816-->
*Si applica a: Configuration Manager (Current Branch)*

A partire da Configuration Manager versione 2002, è possibile creare gruppi di orchestrazione. Per controllare meglio la distribuzione degli aggiornamenti software nei dispositivi, è possibile creare un gruppo di orchestrazione. Molti amministratori del server devono gestire attentamente gli aggiornamenti per carichi di lavoro specifici e automatizzare i comportamenti tra loro.

Un gruppo di orchestrazione consente di aggiornare i dispositivi in base a una percentuale, un numero specifico o un ordine esplicito. È anche possibile eseguire uno script PowerShell prima e dopo che i dispositivi eseguono la distribuzione degli aggiornamenti.

Tutti i client di Configuration Manager, non solo i server, possono essere membri di un gruppo di orchestrazione. Le regole del gruppo di orchestrazione vengono applicate ai dispositivi per tutte le distribuzioni di aggiornamenti software in qualsiasi raccolta contenente un membro del gruppo di orchestrazione. Altri comportamenti di distribuzione rimangono validi, ad esempio le finestre di manutenzione e le pianificazioni della distribuzione.

> [!NOTE]
> In questa versione di Configuration Manager i gruppi di orchestrazione costituiscono una funzionalità di versione non definitiva. Per abilitarla, vedere [Funzionalità di versioni non definitive in System Center Configuration Manager](../../core/servers/manage/pre-release-features.md).  
>
> La funzionalità **Gruppi di orchestrazione** è l'evoluzione della funzionalità [Gruppi di server](service-a-server-group.md). Un gruppo di orchestrazione è un oggetto in Configuration Manager.

## <a name="orchestration-group-usage-example"></a>Esempio di utilizzo di un gruppo di orchestrazione

- L'amministratore degli aggiornamenti software gestisce tutti gli aggiornamenti per l'organizzazione.
- Dispone di una raccolta di grandi dimensioni per tutti i server e di una per tutti i client. Tutti gli aggiornamenti vengono distribuiti in queste raccolte.
- Gli amministratori SQL controllano tutto il software installato nei server SQL. Devono applicare una patch a cinque server in un ordine specifico. Il processo corrente consiste nell'arrestare manualmente servizi specifici prima di installare gli aggiornamenti, quindi riavviare i servizi successivamente.
- Crea un gruppo di orchestrazione e aggiunge tutti e cinque i server SQL. È anche possibile aggiungere pre-e post-script usando gli script di PowerShell forniti dagli amministratori di SQL.
- Durante il ciclo di aggiornamento successivo, gli aggiornamenti software vengono creati e distribuiti come sempre nella raccolta di server di grandi dimensioni. Gli amministratori SQL eseguono la distribuzione e il gruppo di orchestrazione automatizza l'ordine e i servizi.

## <a name="prerequisites"></a>Prerequisiti

### <a name="site-server-and-permission-prerequisites"></a>Prerequisiti del server del sito e delle autorizzazioni
- Per visualizzare tutti i gruppi di orchestrazione e gli aggiornamenti per tali gruppi, è necessario che l'account sia un **amministratore completo**.
   - L'amministrazione basata su ruoli per i gruppi di orchestrazione non è attualmente disponibile.
- Abilitare la funzionalità **Gruppi di orchestrazione**. Per altre informazioni, vedere [Abilitare le funzionalità facoltative](../../core/servers/manage/install-in-console-updates.md#bkmk_options).
   - Quando si abilita **Gruppi di orchestrazione**, il sito disabilita la funzionalità **Gruppi di server**. In questo modo si evitano conflitti tra le due funzionalità.

### <a name="client-prerequisites"></a>Prerequisiti client

- Aggiornare i dispositivi di destinazione alla versione più recente del client Configuration Manager.
- I membri di un gruppo di orchestrazione devono essere assegnati allo stesso sito.
- I dispositivi non possono essere in più di un gruppo di orchestrazione.
   - I dispositivi già presenti in un gruppo di orchestrazione non potranno essere selezionati quando si aggiungono nuovi membri.


## <a name="limitations"></a>Limitazioni

- È possibile avere un massimo di 1000 membri per il gruppo di orchestrazione.
- I gruppi di orchestrazione non possono essere usati in modalità di interoperabilità. Per altre informazioni, vedere [Interoperabilità tra versioni diverse di Configuration Manager](../../core/plan-design/hierarchy/interoperability-between-different-versions.md#bkmk_mixed). <!--6389000-->
- Se gli aggiornamenti vengono avviati dagli utenti da Software Center, l'orchestrazione verrà ignorata. <!--6362887-->

## <a name="server-groups-are-automatically-updated-to-orchestration-groups"></a>I gruppi di server vengono aggiornati automaticamente ai gruppi di orchestrazione

La funzionalità **Gruppi di orchestrazione** è l'evoluzione della funzionalità [Gruppi di server](service-a-server-group.md). Quando si installa Configuration Manager versione 2002 o successive ed è abilitata la funzionalità Gruppi di server, i gruppi di server vengono spostati automaticamente nei gruppi di orchestrazione.

## <a name="create-an-orchestration-group"></a>Creare un gruppo di orchestrazione

1. Nella console di Configuration Manager passare all'area di lavoro **Asset e conformità** e selezionare il nodo **Gruppo di orchestrazione**.

1. Nella barra multifunzione selezionare **Crea gruppo di orchestrazione** per aprire la **Creazione guidata gruppo di orchestrazione**.

1. Nella pagina **Generale** assegnare al gruppo di orchestrazione un **Nome** e facoltativamente una **Descrizione**. Specificare i valori per gli elementi seguenti:
   - **Timeout del gruppo di orchestrazione (in minuti)** : Limite di tempo per tutti i membri del gruppo per completare l'installazione dell'aggiornamento.
   - **Timeout del membro del gruppo di orchestrazione (in minuti)** : Limite di tempo per il completamento dell'installazione dell'aggiornamento per un singolo dispositivo nel gruppo.

1. Nella pagina **Selezionare membri** specificare prima di tutto il **Codice del sito**. Selezionare quindi **Aggiungi** per aggiungere le risorse del dispositivo come membri di questo gruppo di orchestrazione. **Cercare** i dispositivi in base al nome, quindi **aggiungerli**. È anche possibile filtrare la ricerca in base a una sola raccolta usando la **ricerca nella raccolta**.  Dopo aver aggiunto i dispositivi all'elenco delle risorse selezionate, selezionare **OK**.
   - Quando si selezionano le risorse per il gruppo, vengono visualizzati solo i client validi. Vengono eseguiti controlli per verificare il codice del sito, che il client sia installato e che le risorse non siano duplicate.

1. Nella pagina **Rule Selection** (Selezione regola) selezionare una delle opzioni seguenti:

   - **Consentire a una percentuale di computer di essere aggiornati contemporaneamente**, quindi selezionare o immettere un numero per la percentuale. Usare questa impostazione per consentire una futura flessibilità delle dimensioni del gruppo di orchestrazione. Il gruppo di orchestrazione contiene ad esempio 50 dispositivi e il valore viene impostato su 10. Durante una distribuzione degli aggiornamenti software, Configuration Manager consentirà a cinque dispositivi di eseguire contemporaneamente la distribuzione. Se in un secondo momento si aumentano le dimensioni del gruppo di orchestrazione a 100 dispositivi, verranno aggiornati contemporaneamente 10 dispositivi.

   - **Consentire a un numero di computer di essere aggiornati contemporaneamente**, quindi selezionare o immettere un valore per il numero specifico. Usare questa impostazione per limitare sempre a un numero specifico di dispositivi, indipendentemente dalle dimensioni complessive del gruppo di orchestrazione.

   - **Specifica la sequenza di manutenzione**, quindi ordinare le risorse selezionate nell'ordine corretto. Usare questa impostazione per definire in modo esplicito l'ordine in cui i dispositivi eseguono la distribuzione degli aggiornamenti software.

1. Nella pagina **Pre-script** immettere uno script di PowerShell da eseguire in ogni dispositivo *prima* che venga eseguita la distribuzione. Lo script restituirà un valore pari a `0` in caso di esito positivo o pari a `3010` in caso di esito positivo con riavvio.

1. Nella pagina **Post-script** immettere uno script di PowerShell da eseguire in ogni dispositivo *dopo* che viene eseguita la distribuzione. Il comportamento è uguale a quello di Pre-script.

1. Completare la procedura guidata.

> [!WARNING]
> Verificare che gli script pre e post vengano testati prima di usarli per i gruppi di orchestrazione. Gli script pre e post non raggiungono il timeout e verranno eseguiti fino a quando non viene raggiunto il timeout del membro del gruppo di orchestrazione.

## <a name="view-orchestration-groups-and-members"></a>Visualizzare i gruppi di orchestrazione e i membri

Nell'area di lavoro **Asset e conformità** selezionare il nodo **Gruppo di orchestrazione**. Per visualizzare i membri, selezionare un gruppo di orchestrazione e selezionare **Mostra i membri** nella barra multifunzione. Per altre informazioni sulle colonne disponibili per i nodi, vedere [Monitorare i gruppi di orchestrazione e i membri](#bkmk_orch_monitor).

## <a name="edit-or-delete-an-orchestration-group"></a>Modificare o eliminare un gruppo di orchestrazione

Per eliminare il gruppo di orchestrazione, selezionarlo e quindi fare clic su **Elimina** nella barra multifunzione o dal menu di scelta rapida. Per modificare un gruppo di orchestrazione, selezionarlo e quindi fare clic su **Proprietà** nella barra multifunzione o dal menu di scelta rapida. Modificare le impostazioni dalle schede seguenti:

   - **Generale**: 
      - **Nome**: nome del gruppo di orchestrazione
      - **Descrizione**: descrizione del gruppo di orchestrazione (facoltativa)
      - **Timeout del gruppo di orchestrazione (in minuti)** : Limite di tempo per tutti i membri del gruppo per completare l'installazione dell'aggiornamento.
      - **Timeout del membro del gruppo di orchestrazione (in minuti)** : Limite di tempo per il completamento dell'installazione dell'aggiornamento per un singolo dispositivo nel gruppo.

  - **Selezionare membri**:
     - **Site Code** (Codice del sito): codice del sito per il gruppo di orchestrazione.
     - **Membri**: fare clic su **Aggiungi** per selezionare altri dispositivi per il gruppo di orchestrazione. Fare clic su **Rimuovi** per rimuovere il dispositivo selezionato.

   - **Selezione regole**:
      - **Consentire a una percentuale di computer di essere aggiornati contemporaneamente**, quindi selezionare o immettere un numero per la percentuale. Usare questa impostazione per consentire una futura flessibilità delle dimensioni del gruppo di orchestrazione. Il gruppo di orchestrazione contiene ad esempio 50 dispositivi e il valore viene impostato su 10. Durante una distribuzione degli aggiornamenti software, Configuration Manager consentirà a cinque dispositivi di eseguire contemporaneamente la distribuzione. Se in un secondo momento si aumentano le dimensioni del gruppo di orchestrazione a 100 dispositivi, verranno aggiornati contemporaneamente 10 dispositivi.
      - **Consentire a un numero di computer di essere aggiornati contemporaneamente**, quindi selezionare o immettere un valore per il numero specifico. Usare questa impostazione per limitare sempre a un numero specifico di dispositivi, indipendentemente dalle dimensioni complessive del gruppo di orchestrazione.
      - **Specifica la sequenza di manutenzione**: ordinare le risorse selezionate in base all'ordine corretto. Usare questa impostazione per definire in modo esplicito l'ordine in cui i dispositivi eseguono la distribuzione degli aggiornamenti software.

   - **Pre-script**: 
       - Immettere uno script di PowerShell che viene eseguito in ogni dispositivo *prima* che venga eseguita la distribuzione. Lo script restituirà un valore pari a `0` in caso di esito positivo o pari a `3010` in caso di esito positivo con riavvio.
       
   - **Post-script**:
      - Immettere uno script di PowerShell da eseguire in ogni dispositivo *dopo* che viene eseguita la distribuzione. Lo script restituirà un valore pari a `0` in caso di esito positivo o pari a `3010` in caso di esito positivo con riavvio.
   > [!WARNING]
   > Verificare che gli script pre e post vengano testati prima di usarli per i gruppi di orchestrazione. Gli script pre e post non raggiungono il timeout e verranno eseguiti fino a quando non viene raggiunto il timeout del membro del gruppo di orchestrazione.


## <a name="start-orchestration"></a>Avviare l'orchestrazione

1. [Distribuire gli aggiornamenti software](deploy-software-updates.md) in una raccolta che contiene i membri del gruppo di orchestrazione.

1. L'orchestrazione viene avviata quando un client del gruppo tenta di installare un aggiornamento software qualsiasi alla scadenza o durante una finestra di manutenzione. Viene avviata per l'intero gruppo e verifica che i dispositivi vengano aggiornati seguendo le regole del gruppo di orchestrazione.
1. Per avviare manualmente l'orchestrazione, selezionarla dal nodo **Gruppo di orchestrazione**, quindi scegliere **Avvia orchestrazione** dalla barra multifunzione o dal menu di scelta rapida.
1. Se un gruppo di orchestrazione si trova in uno stato *Operazione non riuscita*:
   1. Determinare il motivo per cui l'orchestrazione non è riuscita e risolvere eventuali problemi.
   1. [Reimpostare lo stato dell'orchestrazione per i membri del gruppo](#bkmk_reset).
   1. Dal nodo **Gruppo di orchestrazione** fare clic sul pulsante **Avvia orchestrazione** per riavviare l'orchestrazione.
   [![Avvia orchestrazione ](./media/3098816-start-orchestration.png)](./media/3098816-start-orchestration.png#lightbox)


> [!TIP]
> - I gruppi di orchestrazione sono validi solo per le distribuzioni di aggiornamenti software, non per altre distribuzioni.
> - È possibile fare clic con il pulsante destro del mouse su un membro del gruppo di orchestrazione e selezionare **Reimposta il membro del gruppo di orchestrazione**. In questo modo è possibile rieseguire l'orchestrazione.


## <a name="monitor-orchestration-groups"></a><a name="bkmk_orch_monitor"></a> Monitorare i gruppi di orchestrazione

Nell'area di lavoro **Asset e conformità** selezionare il nodo **Gruppo di orchestrazione**. Aggiungere una delle colonne seguenti per ottenere informazioni sui gruppi:

- **Nome orchestrazione**: Nome del gruppo di orchestrazione.
- **Site Code** (Codice del sito): Codice del sito per il gruppo.
- **Tipo di orchestrazione**: è uno dei tipi seguenti:
   - Numero
   - Percentuale
   - Sequenza

- **Valore orchestrazione**: Il numero di membri o la percentuale di membri che possono ottenere un blocco simultaneamente. La colonna **Valore orchestrazione** viene popolata solo quando **Tipo di orchestrazione** è *Numero* o *Percentuale*.  
- **Stato orchestrazione**: In corso durante l'orchestrazione. Inattiva quando non è in corso.
- **Ora di inizio dell'orchestrazione**: Data e ora di inizio dell'orchestrazione.
- **Numero di sequenza corrente**: Indica per quale membro del gruppo è attiva l'orchestrazione. Questo numero corrisponde al **numero di sequenza** per il membro.  
- **Timeout dell'orchestrazione (in minuti)** : Valore del **timeout del gruppo di orchestrazione (in minuti)** impostato nella pagina **Generale** quando si crea il gruppo o nella scheda **Generale** quando si modifica il gruppo.
- **Timeout del membro del gruppo di orchestrazione (in minuti)** : Valore del **timeout del membro del gruppo di orchestrazione (in minuti)** impostato nella pagina **Generale** quando si crea il gruppo o nella scheda **Generale** quando si modifica il gruppo.
- **ID del gruppo di orchestrazione**: ID del gruppo, usato nei log e nel database.
- **ID univoco per il gruppo di orchestrazione**: ID univoco del gruppo, usato nei log e nel database.

## <a name="monitor-orchestration-group-members"></a>Monitorare i membri dei gruppi di orchestrazione

Nel nodo **Gruppo di orchestrazione** selezionare un gruppo di orchestrazione. Nella barra multifunzione selezionare **Mostra membri**. È possibile visualizzare i membri del gruppo e il relativo stato di orchestrazione. Aggiungere una delle colonne seguenti per ottenere informazioni sui membri:

- **Nome**: Nome del dispositivo del membro del gruppo di orchestrazione
- **Stato corrente**: Indica lo stato del dispositivo del membro.
   - **In corso** durante l'orchestrazione.
   - **In attesa**: Indica che il client attende nel blocco il proprio turno per installare gli aggiornamenti.
   - **Inattivo** se l'orchestrazione è stata completata o non è in esecuzione.
- **Codice stato**: È possibile fare clic con il pulsante destro del mouse sul membro del gruppo di orchestrazione e selezionare **Reimposta il membro del gruppo di orchestrazione**. Questa reimpostazione consente di rieseguire l'orchestrazione. Gli stati includono: 
   - Inattivo
   - In attesa, il dispositivo è in attesa del proprio turno
   - In corso, l'aggiornamento è in corso di installazione
   - Operazione non riuscita
   - Riavvio in sospeso
- **Ora del blocco acquisito**: I blocchi vengono richiesti dal client in base ai criteri. Quando il client acquisisce un blocco, l'orchestrazione viene attivata per quel blocco.  
-**Ora dell'ultimo report sullo stato**: Ora dell'ultima segnalazione di uno stato da parte del membro.
- **Numero sequenza**: Posizione del client nella coda per l'installazione degli aggiornamenti.
- **Site Code** (Codice del sito): Codice del sito per il membro.
- **Attività client**: Indica se il client è attivo o inattivo.
- **Utente/i primario/i**: Gli utenti primari per il dispositivo.
- **Tipo di client**: Tipo di dispositivo del client.
- **Utente attualmente connesso**: L'utente attualmente connesso al dispositivo.
- **ID OG**: ID del gruppo di orchestrazione a cui appartiene il membro.
- **ID OG univoco**: ID univoco del gruppo di orchestrazione a cui appartiene il membro.
- **ID risorsa**: ID risorsa del dispositivo.

## <a name="reset-the-orchestration-state-for-a-group-member"></a><a name="bkmk_reset"></a> Reimpostare lo stato dell'orchestrazione per un membro del gruppo

Se si vuole rieseguire l'orchestrazione per un membro del gruppo, è possibile cancellarne lo stato, ad esempio *Completa* o *Operazione non riuscita*. Per cancellare lo stato, fare clic con il pulsante destro del mouse sul membro del gruppo di orchestrazione e selezionare **Reimposta il membro del gruppo di orchestrazione**. È anche possibile fare clic su **Reimposta il membro del gruppo di orchestrazione** dalla barra multifunzione. Prima di reimpostare lo stato, è necessario controllare il client per verificare il motivo dell'errore e correggere eventuali problemi rilevati.
   [![Reimposta il membro del gruppo di orchestrazione](./media/3098816-reset-group-member.png)](./media/3098816-reset-group-member.png#lightbox)

## <a name="log-files"></a>File di registro

Usare i file di log seguenti nel server del sito per monitorare e risolvere i problemi:

### <a name="site-server"></a>Server del sito

- **Policypv.log**: indica che il sito destina il gruppo di orchestrazione ai client.
- **SMS_OrchestrationGroup.log**: illustra i comportamenti del gruppo di orchestrazione.

### <a name="client"></a>Client

- **MaintenanceCoordinator.log**: illustra l'acquisizione dei blocchi, l'installazione degli aggiornamenti, gli script pre e post e il processo di rilascio del blocco.
- **UpdateDeployment.log**: Illustra il processo di installazione dell'aggiornamento.
- **PolicyAgent.log**: Verifica se il client è in un gruppo di orchestrazione.

## <a name="next-steps"></a>Passaggi successivi

[Distribuire gli aggiornamenti software](deploy-software-updates.md)