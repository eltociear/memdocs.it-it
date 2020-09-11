---
title: Usare l'editor delle sequenze di attività
titleSuffix: Configuration Manager
description: Informazioni su come usare l'editor delle sequenze di attività nella console di Configuration Manager
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: a4e8bb56-ee85-49fd-8b1c-c8f513cec671
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0964cfe73cd69fd274437681e2f7e39e80f55e0b
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/09/2020
ms.locfileid: "89608220"
---
# <a name="use-the-task-sequence-editor"></a>Usare l'editor delle sequenze di attività

*Si applica a: Configuration Manager (Current Branch)*

Per modificare le sequenze di attività nella console di Configuration Manager, usare l'**editor delle sequenze di attività**. L'editor consente di:  

- Aprire una visualizzazione di sola lettura della sequenza di attività

- Aggiungere o rimuovere passaggi della sequenza di attività  

- Modificare l'ordine dei passaggi della sequenza di attività  

- Aggiungere o rimuovere gruppi di passaggi  

- Copiare e incollare i passaggi tra sequenze di attività

- Impostare le opzioni dei passaggi, ad esempio se la sequenza di attività deve continuare quando si verifica un errore  

- Aggiungere condizioni ai passaggi e ai gruppi di una sequenza di attività  

- Copiare e incollare le condizioni tra i passaggi in una sequenza di attività

- Eseguire una ricerca nella sequenza di attività per individuare rapidamente i passaggi

Prima di modificare una sequenza di attività, è necessario crearla. Per altre informazioni, vedere [Gestire e creare le sequenze di attività](../deploy-use/manage-task-sequences-to-automate-tasks.md).

## <a name="about-the-task-sequence-editor"></a>Informazioni sull'editor delle sequenze di attività

L'editor delle sequenze di attività include i componenti seguenti:

![Screenshot con annotazioni della finestra dell'editor delle sequenze di attività di esempio](media/task-sequence-editor.png)

<!-- The following numbered steps correspond to annotations in the above screenshot. Don't change the step numbers without also revising the image! -->

1. Nome della sequenza di attività
2. Ricerca. Per altre informazioni, vedere [Cerca](#bkmk_search).
3. **Proprietà** del gruppo o del passaggio selezionato nella sequenza

    Per altre informazioni sulle proprietà e sulle opzioni di un passaggio specifico, vedere [Passaggi della sequenza di attività](task-sequence-steps.md).

4. **Opzioni** del gruppo o del passaggio selezionato nella sequenza

    Per altre informazioni sulle opzioni generali in tutti i passaggi o sulle opzioni di un passaggio specifico, vedere [Passaggi della sequenza di attività](task-sequence-steps.md).

    Per altre informazioni su come configurare le condizioni, vedere [Condizioni](#bkmk_conditions).

5. Pulsante **Aggiungi** per aggiungere un gruppo o un passaggio
6. Pulsante **Rimuovi** per rimuovere un gruppo o un passaggio
7. Comprimi tutti i gruppi o Espandi tutti i gruppi
8. Sposta la posizione di un gruppo o di un passaggio nella sequenza (Sposta su, Sposta giù)
9. La sequenza di attività:
    - Consente di vedere l'ordine dei passaggi e dei gruppi.
    - Consente di espandere o comprimere un gruppo.
    - Quando si disabilita un passaggio o un gruppo in **Opzioni**, questo viene disattivato nella sequenza.
    - L'icona di un passaggio diventa rossa in caso di errore, ad esempio se manca un valore obbligatorio.
10. **OK**: Salva e chiudi
11. **Annulla**: chiude la finestra senza salvare le modifiche
12. **Applica**: salva le modifiche e lascia aperta la finestra

È possibile ridimensionare l'editor delle sequenze di attività usando i controlli di Windows standard. Per ridimensionare la larghezza dei due riquadri principali, usare il mouse per selezionare la barra tra la sequenza di attività e le proprietà del passaggio, quindi trascinarla verso sinistra o verso destra.

## <a name="view-a-task-sequence"></a><a name="bkmk_view"></a> Visualizzare una sequenza di attività

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**, espandere **Sistemi operativi** e quindi selezionare il nodo **Sequenze di attività**.  

2. Nell'elenco **Sequenza di attività** selezionare la sequenza di attività da visualizzare.  

3. Nella scheda **Home** della barra multifunzione selezionare **Visualizza** nel gruppo **Sequenza di attività**.

    > [!TIP]
    > Questa azione corrisponde all'impostazione predefinita. Se si fa doppio clic su una sequenza di attività, questa viene **visualizzata**.

Questa azione apre l'editor delle sequenze di attività in modalità di sola lettura. In questa modalità è possibile eseguire le operazioni seguenti:

- Visualizzare tutti i gruppi, i passaggi, le proprietà e le opzioni
- Espandere e comprimere i gruppi
- Eseguire una ricerca nella sequenza di attività
- Ridimensionare la finestra dell'editor

In modalità di sola lettura non è possibile apportare modifiche, inclusa la copia di un passaggio o di una condizione. Questa azione non applica inoltre alcun blocco per la modifica della sequenza di attività. Per altre informazioni su questi blocchi, vedere [Richiamare il blocco per la modifica delle sequenze di attività](#bkmk_sedo).

Per apportare modifiche a una sequenza di attività, chiudere l'editor delle sequenze di attività che era stato aperto in modalità di sola lettura. [Modificare](#bkmk_edit) quindi la sequenza di attività.

> [!NOTE]  
> Quando si visualizza o modifica una sequenza di attività creata con la Creazione guidata della sequenza di attività, il nome del passaggio può indicare l'azione o il tipo di passaggio. Ad esempio, è possibile che venga visualizzato un passaggio denominato "Disco di partizione 0" che è l'azione per un passaggio di tipo [Formato e disco partizione](task-sequence-steps.md#BKMK_FormatandPartitionDisk). Tutti i passaggi della sequenza di attività sono documentati in base al *tipo*, non necessariamente in base al nome del passaggio visualizzato dall'editor.  

## <a name="edit-a-task-sequence"></a><a name="bkmk_edit"></a> Modificare una sequenza di attività

Usare la procedura seguente per modificare una sequenza di attività esistente:  

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**, espandere **Sistemi operativi** e quindi selezionare il nodo **Sequenze di attività**.  

2. Nell'elenco **Sequenza di attività** selezionare la sequenza di attività da modificare.  

3. Nella scheda **Home** della barra multifunzione selezionare **Modifica** nel gruppo **Sequenza di attività**. Effettuare quindi una delle azioni seguenti:  

    - **Aggiungere un passaggio**: selezionare **Aggiungi**, selezionare una categoria e quindi il passaggio da aggiungere. Ad esempio, per aggiungere il passaggio [Esegui riga di comando](task-sequence-steps.md#BKMK_RunCommandLine), selezionare **Aggiungi**, scegliere la categoria **Generale** e quindi selezionare **Esegui riga di comando**. Questa azione aggiunge il passaggio dopo quello attualmente selezionato.

    - **Aggiungere un gruppo**: selezionare **Aggiungi** e quindi scegliere **Nuovo gruppo**. Dopo aver aggiunto un gruppo, aggiungervi i passaggi.  

    - **Cambiare l'ordine**: selezionare il passaggio o il gruppo da riordinare. Usare quindi l'icona **Sposta su** o **Sposta giù**. È possibile spostare solo un passaggio o un gruppo alla volta. Queste azioni sono disponibili anche facendo clic con il pulsante destro del mouse su un gruppo o un passaggio.

        È possibile tagliare, copiare e incollare un gruppo o un passaggio. Fare clic con il pulsante destro del mouse sull'elemento e scegliere l'azione. È anche possibile usare i tasti di scelta rapida standard per ogni azione:

        - Taglia: **CTRL** + **X**
        - Copia: **CTRL** + **C**
        - Incolla: **CTRL** + **V**

    - **Rimuovere un passaggio o un gruppo**: Selezionare il passaggio o il gruppo e scegliere **Rimuovi**.  

4. Selezionare **OK** per salvare le modifiche e chiudere la finestra. Selezionare **Annulla** per annullare le modifiche e chiudere la finestra. Selezionare **Applica** per salvare le modifiche e mantenere aperto l'editor della sequenza di attività.  

Per un elenco dei passaggi della sequenza di attività disponibili, vedere [Passaggi della sequenza di attività](task-sequence-steps.md).  

> [!IMPORTANT]  
> Se la sequenza di attività include riferimenti non associati a un oggetto come risultato della modifica, l'editor richiede di correggere il riferimento prima di chiudere. Le azioni possibili includono:  
>
> - Correggere il riferimento
> - Eliminare l'oggetto senza riferimenti dalla sequenza di attività  
> - Disabilitare temporaneamente il passaggio della sequenza di attività non riuscito fino alla correzione o rimozione del riferimento interrotto  

È possibile aprire più istanze dell'editor delle sequenze di attività contemporaneamente. Questo comportamento consente di confrontare più sequenze di attività o di copiare e incollare passaggi dall'una all'altra. Si può **modificare** una sequenza di attività e **visualizzarne** un'altra, ma non è possibile eseguire entrambe le azioni sulla stessa sequenza di attività.

## <a name="conditions"></a><a name="bkmk_conditions"></a> Condizioni

Usare le condizioni per controllare il comportamento della sequenza di attività. Aggiungere condizioni a un singolo passaggio o a un gruppo di passaggi. La sequenza di attività valuta le condizioni prima di eseguire il passaggio sul dispositivo. Esegue il passaggio solo se la valutazione delle condizioni restituisce true. Se la valutazione di una condizione restituisce false, la sequenza di attività ignora il gruppo o il passaggio.

Per gestire le condizioni, usare la scheda **Opzioni**:

![Gestire le condizioni nella scheda Opzioni dell'editor delle sequenze di attività](media/4621098-copy-paste-ts-condition.png)

Sono disponibili i tipi di condizioni seguenti:

- **Istruzione if**: usare un'istruzione *if* per raggruppare le condizioni. Le opzioni di valutazione disponibili sono **Tutte le condizioni**, **Qualsiasi condizione** o **Nessuna**.

- **Variabile della sequenza di attività**. Valutare il valore corrente di una [variabile della sequenza di attività](task-sequence-variables.md) predefinita, di azione, personalizzata o di sola lettura nell'ambiente della sequenza di attività. Per altre informazioni, vedere [Condizioni dei passaggi](using-task-sequence-variables.md#bkmk_access-condition).

    > [!NOTE]
    > In questa condizione è possibile usare una variabile di matrice, ma occorre indicare il membro della matrice specifico. Ad esempio, `OSDAdapter0EnableDHCP` specifica se la *prima* scheda di rete abilita il protocollo DHCP. Per altre informazioni, vedere [Variabili di matrice](using-task-sequence-variables.md#bkmk_array).

- **Versione del sistema operativo**: valutare la versione del sistema operativo del dispositivo in cui viene eseguita la sequenza di attività. Questo elenco indica la versione generale del sistema operativo usata in Configuration Manager. Per valutare una versione del sistema operativo più dettagliata, ad esempio una versione specifica di Windows 10, usare la condizione **Esegui query WMI**.

- **Lingua sistema operativo**: valutare la lingua del sistema operativo del dispositivo in cui viene eseguita la sequenza di attività. Questo elenco include le 257 lingue supportate da Windows.

- **Proprietà file**: valutare la versione o il timestamp di qualsiasi file nel dispositivo in cui viene eseguita la sequenza di attività.

- **Proprietà cartella**: valutare il timestamp di qualsiasi cartella nel dispositivo in cui viene eseguita la sequenza di attività.

- **Impostazione del Registro di sistema**: valutare il valore di una chiave del Registro di sistema del dispositivo in cui viene eseguita la sequenza di attività.

- **Esegui query WMI**: specificare lo spazio dei nomi e la query da valutare nel dispositivo in cui viene eseguita la sequenza di attività.

- **Software installato**: specificare un file di Windows Installer per caricare le informazioni sul prodotto da confrontare nel dispositivo in cui viene eseguita la sequenza di attività. È possibile eseguire il confronto con un prodotto specifico o una versione del prodotto.

### <a name="cmdlets-for-conditions"></a>Cmdlet per le condizioni

Per gestire le condizioni, usare i cmdlet di PowerShell seguenti:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepConditionFile](/powershell/module/configurationmanager/Get-CMTSStepConditionFile)
- [Get-CMTSStepConditionFolder](/powershell/module/configurationmanager/Get-CMTSStepConditionFolder)
- [Get-CMTSStepConditionIfStatement](/powershell/module/configurationmanager/Get-CMTSStepConditionIfStatement)
- [Get-CMTSStepConditionOperatingSystem](/powershell/module/configurationmanager/Get-CMTSStepConditionOperatingSystem)
- [Get-CMTSStepConditionQueryWmi](/powershell/module/configurationmanager/Get-CMTSStepConditionQueryWmi)
- [Get-CMTSStepConditionRegistry](/powershell/module/configurationmanager/Get-CMTSStepConditionRegistry)
- [Get-CMTSStepConditionSoftware](/powershell/module/configurationmanager/Get-CMTSStepConditionSoftware)
- [Get-CMTSStepConditionVariable](/powershell/module/configurationmanager/Get-CMTSStepConditionVariable)

### <a name="copy-and-paste-conditions"></a>Copiare e incollare le condizioni

<!-- 4621098 -->

Per riutilizzare le condizioni da un passaggio a un altro, a partire dalla versione 1910 è possibile copiare e incollare le condizioni nell'editor delle sequenze di attività. Selezionare una condizione per tagliarla o copiarla. Se una condizione include elementi figlio, viene copiato l'intero blocco. Se negli Appunti è presente una condizione, è possibile incollarla con le opzioni seguenti:

- Incolla prima
- Incolla dopo
- Incolla sotto (si applica solo alle condizioni annidate)

Usare i tasti di scelta rapida standard per copiare (**CTRL** + **C**) e tagliare (**CTRL** + **X**). Il tasto di scelta rapida standard **CTRL** + **V** esegue l'operazione **Incolla dopo**.

Sono anche disponibili nuove opzioni per spostare le condizioni verso l'alto o verso il basso nell'elenco.

> [!Note]  
> È possibile copiare e incollare le condizioni tra i passaggi in una sequenza di attività. Questa azione non è supportata tra sequenze di attività diverse.

## <a name="reclaim-lock-for-editing"></a><a name="bkmk_sedo"></a> Richiamare il blocco per la modifica

<!--3699337-->
Se la console di Configuration Manager non risponde, può essere bloccata la possibilità di apportare ulteriori modifiche fino al termine del blocco, dopo 30 minuti. Questo blocco fa parte del sistema di Configuration Manager SEDO (modifica serializzata di Distributed Objects). Per altre informazioni, vedere [Configuration Manager SEDO](../../develop/core/understand/sedo.md).

A partire dalla versione 1906, è possibile cancellare il blocco su una sequenza di attività. Questa azione si applica solo al proprio account utente che ha il blocco e allo stesso dispositivo da cui il sito ha concesso il blocco. Quando si tenta di accedere a una sequenza di attività bloccata, è ora possibile **rimuovere le modifiche**e continuare a modificare l'oggetto. Queste modifiche andrebbero perse comunque al termine del blocco.

> [!TIP]
> A partire dalla versione 1910, è possibile cancellare il blocco su qualsiasi oggetto nella console di Configuration Manager. Per altre informazioni, vedere [Uso della console di Configuration Manager](../../core/servers/manage/admin-console.md#bkmk_sedo).<!--4786915-->

## <a name="search"></a><a name="bkmk_search"></a> Ricerca

<!-- 4621085 -->

Se si ha una sequenza di attività di grandi dimensioni con molti gruppi e passaggi, può essere difficile individuare passaggi specifici. A partire dalla versione 1910, è possibile eseguire ricerche nell'editor delle sequenze di attività. Questa azione consente di individuare più rapidamente i passaggi in una sequenza di attività.

![Ricerca nell'editor delle sequenze di attività](media/4621085-task-sequence-search.png)

Immettere un termine di ricerca per iniziare. È possibile definire l'ambito della ricerca usando i tipi seguenti:

- Nome del passaggio
- Descrizione del passaggio
- Tipo del passaggio
- Nome del gruppo
- Descrizione del gruppo
- Nome della variabile
- Condizioni
- Altro contenuto, ad esempio stringhe quali valori di variabili o righe di comando

Abilita tutti gli ambiti per impostazione predefinita.

È anche possibile filtrare tutti i passaggi con gli attributi seguenti:

- Continua in caso di errore
- Presenza di condizioni

Non abilita i filtri per impostazione predefinita.

Quando si esegue la ricerca, la finestra dell'editor evidenzia in giallo i passaggi che soddisfano i criteri di ricerca.

Accedere rapidamente ai campi di ricerca ed esplorare i risultati della ricerca con i tasti di scelta rapida seguenti:

- **CTRL** + **F**: immissione di una stringa di ricerca
- **CTRL** + **O**: selezione delle opzioni di ricerca per definire l'ambito dei risultati
- **F3** o **Invio**: avanzamento attraverso i risultati
- **MAIUSC** + **F3**: arretramento attraverso i risultati

## <a name="see-also"></a>Vedere anche

- [Gestire e creare le sequenze di attività](../deploy-use/manage-task-sequences-to-automate-tasks.md)

- [Informazioni sui passaggi della sequenza di attività](task-sequence-steps.md)

- [Come usare le variabili della sequenza di attività](using-task-sequence-variables.md)

- [Uso della console di Configuration Manager](../../core/servers/manage/admin-console.md)