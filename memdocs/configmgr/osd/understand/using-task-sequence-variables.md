---
title: Come usare le variabili della sequenza di attività
titleSuffix: Configuration Manager
description: Informazioni su come usare le variabili in una sequenza di attività di Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: bc7de742-9e5c-4a70-945c-df4153a61cc3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1cf428b479e9311c92f6d14d9c376817ee5e3ab5
ms.sourcegitcommit: b90d51f7ce09750e024b97baf6950a87902a727c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/06/2020
ms.locfileid: "86022263"
---
# <a name="how-to-use-task-sequence-variables-in-configuration-manager"></a>Come usare le variabili della sequenza di attività in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

 Il motore di esecuzione della sequenza di attività nella funzionalità di distribuzione del sistema operativo di Configuration Manager usa numerose variabili per controllarne i comportamenti. Usare queste variabili per:

- Impostare le condizioni sui passaggi  
- Cambiare i comportamenti per passaggi specifici  
- Creare azioni più complesse con gli script  

Per informazioni di riferimento su tutte le variabili della sequenza di attività disponibili, vedere [Task sequence variables](task-sequence-variables.md) (Variabili della sequenza di attività).

## <a name="types-of-variables"></a><a name="bkmk_types"></a> Tipi di variabili

Sono disponibili diversi tipi di variabili:  

- [Predefinite](#bkmk_built-in)  
- [Azione](#bkmk_action)  
- [Personalizzato](#bkmk_custom)  
- [Di sola lettura](#bkmk_read-only)  
- [Di matrice](#bkmk_array)  

### <a name="built-in-variables"></a><a name="bkmk_built-in"></a> Variabili predefinite

Le variabili predefinite forniscono informazioni sull'ambiente in cui viene eseguita la sequenza di attività. I relativi valori sono disponibili nell'intera sequenza di attività. In genere il motore di esecuzione della sequenza di attività inizializza le variabili predefinite prima di eseguire qualsiasi passaggio.

Ad esempio, `_SMSTSLogPath` è una variabile di ambiente che specifica il percorso in cui i componenti di Configuration Manager scrivono i file di log. Qualsiasi passaggio della sequenza di attività può accedere a questa variabile di ambiente.

La sequenza di attività valuta alcune variabili prima di ogni passaggio. Ad esempio, `_SMSTSCurrentActionName` elenca il nome del passaggio corrente.

### <a name="action-variables"></a><a name="bkmk_action"></a> Variabili di azione

Le variabili di azione della sequenza di attività specificano le impostazioni di configurazione usate da un singolo passaggio della sequenza di attività. Per impostazione predefinita, il passaggio inizializza le proprie impostazioni prima dell'esecuzione. Queste impostazioni sono disponibili solo mentre il passaggio della sequenza di attività associato è in esecuzione. La sequenza di attività aggiunge la variabile di azione all'ambiente prima di eseguire il passaggio. Rimuove quindi il valore dall'ambiente dopo l'esecuzione del passaggio.

Ad esempio, aggiungere il passaggio **Esegui riga di comando** a una sequenza di attività. Questo passaggio include una proprietà **Da**. La sequenza di attività archivia un valore predefinito per questa proprietà come variabile `WorkingDirectory`. La sequenza di attività inizializza questo valore prima di eseguire il passaggio **Esegui riga di comando**. Durante l'esecuzione di questo passaggio, accedere al valore della proprietà **Da** dal valore `WorkingDirectory`. Dopo il completamento del passaggio, la sequenza di attività rimuove il valore della variabile `WorkingDirectory` dall'ambiente. Se la sequenza di attività include un altro passaggio **Esegui riga di comando**, inizializza una nuova variabile `WorkingDirectory`. A questo punto la sequenza di attività imposta la variabile sul valore iniziale del passaggio corrente. Per altre informazioni, vedere [WorkingDirectory](task-sequence-variables.md#WorkingDirectory).  

Il valore *predefinito* per una variabile di azione è presente quando il passaggio viene eseguito. Se si imposta un *nuovo* valore, questo è disponibile per più passaggi della sequenza di attività. Se si esegue l'override di un valore predefinito, il nuovo valore rimane nell'ambiente. Questo nuovo valore esegue l'override del valore predefinito per altri passaggi della sequenza di attività. Supponiamo ad esempio di aggiungere un passaggio **Imposta variabile della sequenza di attività** come primo passaggio della sequenza di attività. Questo passaggio imposta la variabile `WorkingDirectory` su `C:\`. Qualsiasi passaggio **Esegui riga di comando** nella sequenza di attività usa il nuovo valore della directory iniziale.  

Alcuni passaggi della sequenza di attività contrassegnano determinate variabili di azione come *output*. I passaggi successivi della sequenza di attività leggono queste variabili di output.

> [!Note]  
> Non tutti i passaggi della sequenza di attività contengono variabili di azione. Ad esempio, anche se ci sono variabili associate all'azione **Attiva BitLocker**, non ci sono variabili associate all'azione **Disattiva BitLocker**.  

### <a name="custom-variables"></a><a name="bkmk_custom"></a> Variabili personalizzate

Le variabili personalizzate sono tutte le variabili non create da Configuration Manager. Inizializzare le variabili personalizzate da usare come condizioni, in righe di comando o in script.

Quando si specifica un nome per una nuova variabile della sequenza di attività, usare le seguenti linee guida:  

- Il nome della variabile della sequenza di attività può contenere lettere, numeri, il carattere di sottolineatura (`_`) e un trattino (`-`).  

- I nomi delle variabili della sequenza di attività hanno una lunghezza minima di un carattere e una lunghezza massima di 256 caratteri.  

- Le variabili definite dall'utente devono iniziare con una lettera (`A-Z` o `a-z`).  

- I nomi delle variabili definite dall'utente non possono iniziare con il carattere di sottolineatura. Solo le variabili della sequenza di attività di sola lettura sono precedute dal carattere di sottolineatura.  

- Ai nomi delle variabili della sequenza di attività non viene applicata la distinzione tra maiuscole e minuscole. Ad esempio, `OSDVAR` e `osdvar` sono la stessa variabile della sequenza di attività.  

- I nomi delle variabili della sequenza di attività non possono iniziare o finire con uno spazio né contenere spazi. Gli spazi lasciati all'inizio o alla fine di un nome di variabile vengono ignorati dalla sequenza di attività.  

Non è previsto un limite massimo di variabili della sequenza di attività che possono essere create. Tuttavia, il numero di variabili è limitato dalle dimensioni dell'ambiente della sequenza di attività. Il limite di dimensione totale per l'ambiente della sequenza di attività è 32 MB.  

### <a name="read-only-variables"></a><a name="bkmk_read-only"></a> Variabili di sola lettura

Le variabili di sola lettura sono variabili di cui non è possibile cambiare il valore. In genere il nome inizia con un carattere di sottolineatura (`_`). La sequenza di attività usa queste variabili per le sue operazioni. Le variabili di sola lettura sono visibili nell'ambiente della sequenza di attività.

Queste variabili sono utili negli script o nelle righe di comando. Ad esempio, è possibile eseguire una riga di comando e inviare pipe dell'output a un file di log in `_SMSTSLogPath` con gli altri file di log.

> [!NOTE]  
> Le variabili della sequenza di attività di sola lettura possono essere lette dai passaggi di una sequenza di attività, ma non possono essere impostate. Ad esempio, usare una variabile di sola lettura come parte della riga di comando di un passaggio **Esegui riga di comando**. Non è possibile impostare una variabile di sola lettura usando il passaggio **Imposta variabile della sequenza di attività**.  

### <a name="array-variables"></a><a name="bkmk_array"></a> Variabili di matrice

La sequenza di attività archivia alcune variabili come matrice. Ogni elemento della matrice rappresenta le impostazioni per un singolo oggetto. Usare queste variabili quando un dispositivo ha più oggetti da configurare. I passaggi seguenti della sequenza di attività usano variabili di matrice:

- [Applica impostazioni di rete](task-sequence-steps.md#BKMK_ApplyNetworkSettings)  

- [Formato e disco partizione](task-sequence-steps.md#BKMK_FormatandPartitionDisk)  

## <a name="how-to-set-variables"></a><a name="bkmk_set"></a> Come impostare le variabili

Sono disponibili diversi metodi che consentono di inizializzare e impostare il valore delle variabili personalizzate o non di sola lettura:  

- Passaggio [Imposta variabile della sequenza di attività](#bkmk_set-ts-step)
- Passaggio [Imposta variabili dinamiche](#bkmk_set-dyn-step)
- Passaggio [Esegui script PowerShell](#bkmk_run-ps)
- [Variabili di raccolta e dispositivo](#bkmk_set-coll-var)  
- [Oggetto COM TSEnvironment](#bkmk_set-com)  
- [Comando di preavvio](#bkmk_set-prestart)  
- [Creazione guidata sequenza di attività](#bkmk_set-tswiz)
- [Creazione guidata del supporto per la sequenza di attività](#bkmk_set-media)  

Eliminare una variabile dall'ambiente usando gli stessi metodi usati per crearla. Per eliminare una variabile, impostarne il valore su una stringa vuota.  

È possibile combinare metodi per impostare una variabile della sequenza di attività su valori diversi per la stessa sequenza. Ad esempio, impostare i valori predefiniti usando l'editor delle sequenze di attività e i valori personalizzati usando uno script.

Se si imposta la stessa variabile con metodi diversi, il motore di esecuzione della sequenza di attività usa l'ordine seguente:  

1. Prima di tutto valuta le variabili di raccolta.  

2. Le variabili specifiche del dispositivo eseguono l'override dello stesso set di variabili in una raccolta.  

3. Le variabili impostate da un qualsiasi metodo durante la sequenza di attività hanno la precedenza sulle variabili di raccolta o dispositivo.  

### <a name="general-limitations-for-task-sequence-variable-values"></a>Limitazioni generali per i valori delle variabili della sequenza di attività

- I valori delle variabili della sequenza di attività non possono superare i 4.000 caratteri.  

- Non è possibile modificare una variabile della sequenza di attività di sola lettura. Le variabili di sola lettura hanno nomi che iniziano con un carattere di sottolineatura (`_`).  

- I valori delle variabili della sequenza di attività possono applicare la distinzione tra maiuscole e minuscole a seconda dell'uso del valore. Nella maggior parte dei casi, ai valori delle variabili della sequenza di attività non viene applicata la distinzione tra maiuscole e minuscole. Viene invece applicata alle variabili che includono una password.  

### <a name="set-task-sequence-variable"></a><a name="bkmk_set-ts-step"></a> Imposta variabile della sequenza di attività

Usare questo passaggio nella sequenza di attività per impostare una singola variabile su un singolo valore.

Per altre informazioni, vedere [Imposta variabile della sequenza di attività](task-sequence-steps.md#BKMK_SetTaskSequenceVariable).

### <a name="set-dynamic-variables"></a><a name="bkmk_set-dyn-step"></a> Imposta variabili dinamiche

Usare questo passaggio nella sequenza di attività per impostare una o più variabili della sequenza di attività. Occorre definire le regole in questo passaggio per determinare quali variabili e valori usare.

Per altre informazioni, vedere [Imposta variabili dinamiche](task-sequence-steps.md#BKMK_SetDynamicVariables).

### <a name="run-powershell-script"></a><a name="bkmk_run-ps"></a> Esegui script PowerShell

<!-- 6315548 -->

Usare questo passaggio nella sequenza di attività per usare uno script di PowerShell per impostare una variabile della sequenza di attività.

È possibile specificare un nome di script da un pacchetto oppure immettere direttamente uno script di PowerShell nel passaggio. Usare quindi la proprietà del passaggio **Output nella variabile della sequenza di attività** per salvare l'output dello script in una variabile della sequenza di attività personalizzata.

Per altre informazioni su questo passaggio, vedere [Eseguire script di PowerShell](task-sequence-steps.md#BKMK_RunPowerShellScript).

> [!NOTE]
> È anche possibile usare uno script di PowerShell per impostare una o più variabili con l'oggetto **TSEnvironment**. Per altre informazioni, vedere [How to use variables in a running task sequence](../../develop/osd/how-to-use-task-sequence-variables-in-a-running-task-sequence.md) (Come usare le variabili in una sequenza di attività in esecuzione) in Configuration Manager SDK.

#### <a name="example-scenario-with-run-powershell-script-step"></a>Scenario di esempio con il passaggio Esegui script PowerShell

L'ambiente include utenti in più paesi/aree, pertanto si vuole eseguire una query sulla lingua del sistema operativo per impostarla come condizione per più passaggi **Applica sistema operativo** specifici della lingua.

1. Aggiungere un'istanza del passaggio **Esegui script PowerShell** alla sequenza di attività prima dei passaggi **Applica sistema operativo**.

1. Usare l'opzione **Immettere uno script di PowerShell** per specificare il comando seguente:

    ```powershell
    (Get-Culture).TwoLetterISOLanguageName
    ```

    Per altre informazioni sul cmdlet, vedere [Get-Culture](https://docs.microsoft.com/powershell/module/microsoft.powershell.utility/get-culture). Per altre informazioni sui nomi di lingua ISO di due lettere, vedere l'[elenco di codici ISO 639-1](https://wikipedia.org/wiki/List_of_ISO_639-1_codes).

1. Per l'opzione **Output nella variabile della sequenza di attività** specificare `CurrentOSLanguage`.

    ![Screenshot del passaggio di esempio Esegui script PowerShell](media/run-powershell-script-example-language.png)

1. Nel passaggio **Applica sistema operativo** per l'immagine in lingua inglese, creare la condizione seguente: `Task Sequence Variable CurrentOSLanguage equals "en"`

    ![Screenshot della condizione di esempio nel passaggio Applica sistema operativo](media/condition-custom-task-sequence-variable.png)

    > [!TIP]
    > Per altre informazioni su come creare una condizione in un passaggio, vedere [Come usare le variabili della sequenza di attività - Condizione del passaggio](#bkmk_access-condition).

1. Salvare e distribuire la sequenza di attività.

Quando il passaggio **Esegui script PowerShell** viene eseguito in un dispositivo con la versione in lingua inglese di Windows, il comando restituisce il valore `en`. Il valore viene quindi salvato nella variabile personalizzata. Quando il passaggio **Applica sistema operativo** per l'immagine in lingua inglese viene eseguito nello stesso dispositivo, la condizione restituisce true. Se sono presenti più istanze del passaggio **Applica sistema operativo** per lingue diverse, la sequenza di attività esegue dinamicamente il passaggio corrispondente alla lingua del sistema operativo.

### <a name="collection-and-device-variables"></a><a name="bkmk_set-coll-var"></a> Variabili di raccolta e dispositivo

È possibile definire variabili della sequenza di attività personalizzate per dispositivi e raccolte. Le variabili definite per un dispositivo vengono definite variabili della sequenza di attività con ambito dispositivo. Le variabili definite per una raccolta vengono definite variabili della sequenza di attività con ambito raccolta. Se si verifica un conflitto, le variabili con ambito dispositivo hanno la precedenza sulle variabili con ambito raccolta. Questo significa che le variabili della sequenza di attività assegnate a un dispositivo specifico assumono automaticamente una priorità maggiore di quelle assegnate alla raccolta che contiene il dispositivo.  

Il dispositivo XYZ, ad esempio, è un membro della raccolta ABC. Si assegna MyVariable alla raccolta ABC con il valore 1. Si assegna MyVariable anche al dispositivo XYZ con il valore 2. La variabile assegnata al dispositivo XYZ ha priorità più alta rispetto alla variabile assegnata alla raccolta ABC. Quando una sequenza di attività con questa variabile viene eseguita nel dispositivo XYZ, MyVariable ha il valore 2.

Se si vuole che le variabili con ambito dispositivo e raccolta non siano visibili nella console di Configuration Manager, è possibile nasconderle. Quando si usa l'opzione **Non visualizzare questo valore nella console di Configuration Manager**, il valore della variabile non viene visualizzato nella console. La variabile è ancora utilizzabile dalla sequenza di attività durante l'esecuzione. Se non è più necessario nascondere queste variabili, prima di tutto eliminarle, quindi ridefinire le variabili senza selezionare l'opzione per nasconderle.  

> [!WARNING]  
> L'impostazione **Non visualizzare questo valore nella console di Configuration Manager** si applica solo alla console di Configuration Manager. I valori per le variabili vengono comunque visualizzati nel file di log della sequenza di attività (**smsts.log**).

È possibile gestire le variabili per dispositivo in un sito primario oppure in un sito di amministrazione centrale. Configuration Manager non supporta più di 1.000 variabili assegnate per dispositivo.  

> [!IMPORTANT]  
> Quando si usano variabili con ambito raccolta per le sequenze di attività, considerare i comportamenti seguenti:  
>
> - Le modifiche alle raccolte vengono sempre replicate in tutta la gerarchia. Qualsiasi modifica apportata alle variabili della raccolta si applica non solo ai membri del sito corrente ma a tutti i membri della raccolta in tutta la gerarchia.  
>  
> - Quando si elimina una raccolta, questa azione elimina anche le variabili della sequenza di attività configurate per la raccolta.  

#### <a name="create-task-sequence-variables-for-a-device"></a>Creare variabili della sequenza di attività per un *dispositivo*

1. Nella console di Configuration Manager passare all'area di lavoro **Asset e conformità** e selezionare il nodo **Dispositivi**.  

2. Selezionare il dispositivo di destinazione e selezionare **Proprietà**.  

3. Nella finestra di dialogo **Proprietà** passare alla scheda **Variabili**.  

4. Per ogni variabile che si vuole creare, selezionare l'icona **Nuova**. Specificare il **nome** e il **valore** della variabile della sequenza di attività. Per nascondere le variabili in modo che non siano visibili nella console di Configuration Manager, selezionare l'opzione **Non visualizzare questo valore nella console di Configuration Manager**.  

5. Dopo aver aggiunto tutte le variabili alle proprietà del dispositivo, selezionare **OK**.  

#### <a name="create-task-sequence-variables-for-a-collection"></a>Creare variabili della sequenza di attività per una *raccolta*

1. Nella console di Configuration Manager passare all'area di lavoro **Asset e conformità** e selezionare il nodo **Raccolte dispositivi**. Selezionare la raccolta di destinazione e scegliere **Proprietà**.  

2. Nella finestra di dialogo **Proprietà** passare alla scheda **Variabili raccolta**.  

3. Per ogni variabile che si vuole creare, selezionare l'icona **Nuova**. Specificare il **nome** e il **valore** della variabile della sequenza di attività. Per nascondere le variabili in modo che non siano visibili nella console di Configuration Manager, selezionare l'opzione **Non visualizzare questo valore nella console di Configuration Manager**.  

4. È anche possibile specificare la priorità in base alla quale Configuration Manager valuterà le variabili della sequenza di attività.  

5. Dopo aver aggiunto tutte le variabili alle proprietà della raccolta, selezionare **OK**.  

### <a name="tsenvironment-com-object"></a><a name="bkmk_set-com"></a> Oggetto COM TSEnvironment

Per lavorare con le variabili da uno script, usare l'oggetto **TSEnvironment**.

Per altre informazioni, vedere [How to use variables in a running task sequence](../../develop/osd/how-to-use-task-sequence-variables-in-a-running-task-sequence.md) (Come usare le variabili in una sequenza di attività in esecuzione) in Configuration Manager SDK.

### <a name="prestart-command"></a><a name="bkmk_set-prestart"></a> Comando di preavvio

Il comando di preavvio è uno script o un file eseguibile che viene eseguito in Windows PE prima che l'utente selezioni la sequenza di attività. Può eseguire query su una variabile o richiedere informazioni all'utente e quindi salvarle nell'ambiente. Usare l'oggetto COM [TSEnvironment](#bkmk_set-com) per leggere e scrivere variabili dal comando di preavvio.

Per altre informazioni vedere [Comandi di preavvio del supporto per sequenza attività](prestart-commands-for-task-sequence-media.md).

### <a name="task-sequence-wizard"></a><a name="bkmk_set-tswiz"></a> Creazione guidata sequenza di attività

A partire dalla versione 1906, dopo la selezione di una sequenza di attività nella finestra Creazione guidata sequenza di attività, la pagina per la modifica delle variabili della sequenza di attività include un pulsante **Modifica**. È possibile usare scelte rapide da tastiera per modificare le variabili. Questa modifica è utile nei casi in cui non è disponibile un mouse.<!-- 4668846 -->

### <a name="task-sequence-media-wizard"></a><a name="bkmk_set-media"></a> Creazione guidata del supporto per la sequenza di attività

Specificare le variabili per le sequenze di attività che vengono eseguite da supporti. Quando si usa un supporto per la distribuzione del sistema operativo, al momento della creazione del supporto occorre aggiungere le variabili della sequenza di attività e specificarne i valori. Le variabili e i loro valori vengono memorizzati nel supporto.  

> [!NOTE]  
> Le sequenze attività vengono memorizzate su un supporto autonomo. Tutti gli altri tipi di supporto, ad esempio i supporti pre-installati, recuperano invece la sequenza di attività da un punto di gestione.  

Quando si esegue una sequenza di attività da un supporto, è possibile aggiungere una variabile nella pagina **Personalizzazione** della procedura guidata.

Usare le variabili con ambito supporto anziché le variabili con ambito raccolta o computer. Se la sequenza di attività viene eseguita dal supporto, le variabili con ambito computer e raccolta non sono valide e non vengono usate.  

> [!TIP]  
> La sequenza di attività scrive l'ID del pacchetto e la riga di comando di preavvio nel file di log **CreateTSMedia.log** nel computer che esegue la console di Configuration Manager. Questo file di log include il valore di tutte le variabili della sequenza di attività. Rivedere questo file di log per verificare il valore per le variabili della sequenza di attività.  

Per altre informazioni, vedere [Creare supporti per sequenza di attività](../deploy-use/create-task-sequence-media.md).

## <a name="how-to-access-variables"></a><a name="bkmk_access"></a> Come accedere alle variabili

Dopo aver specificato la variabile e il relativo valore tramite uno dei metodi descritti nella sezione precedente, usarla nelle sequenze di attività. Ad esempio, accedere ai valori predefiniti delle variabili delle sequenze di attività predefinite o rendere un passaggio condizionale in base al valore della variabile.  

Usare i metodi seguenti per accedere ai valori delle variabili nell'ambiente della sequenza di attività:

- [Uso in un passaggio](#bkmk_access-step)  
- [Condizione del passaggio](#bkmk_access-condition)  
- [Script personalizzato](#bkmk_access-script)  
- [File di risposte del programma di installazione di Windows](#bkmk_access-answer)  
  
### <a name="use-in-a-step"></a><a name="bkmk_access-step"></a> Uso in un passaggio

Specificare un valore di variabile per un'impostazione in un passaggio della sequenza di attività. Nell'editor di testo delle sequenze di attività modificare il passaggio e specificare il nome della variabile come valore del campo. Racchiudere il nome della variabile tra simboli di percentuale (`%`).

Ad esempio, usare il nome della variabile come parte del campo **Riga di comando** del passaggio **Esegui riga di comando**. La riga di comando seguente scrive il nome computer in un file di testo.

`cmd.exe /c %_SMSTSMachineName% > C:\File.txt`

### <a name="step-condition"></a><a name="bkmk_access-condition"></a> Condizione del passaggio

Usare variabili della sequenza di attività predefinite o personalizzate come parte di una condizione per un passaggio o un gruppo. La sequenza di attività valuta il valore della variabile prima di eseguire il passaggio o il gruppo.

Per aggiungere una condizione che valuti un valore della variabile, eseguire i passaggi seguenti:  

1. Nell'editor delle sequenze di attività selezionare il passaggio o il gruppo a cui si vuole aggiungere la condizione.  

2. Passare alla scheda **Opzioni** relativa al passaggio o al gruppo. Fare clic su **Aggiungi condizione** e selezionare **Variabile della sequenza di attività**.  

3. Nella finestra di dialogo **Variabile della sequenza di attività** specificare le impostazioni seguenti:  

    - **Variabile**: nome della variabile. Ad esempio, `_SMSTSInWinPE`  

    - **Condizione**: condizione in base alla quale valutare il valore della variabile. Ad esempio, **uguale a**.  

    - **Valore**: valore della variabile da controllare. Ad esempio, `false`  

I tre esempi riportati sopra formano una condizione in base a cui verificare se la sequenza di attività è in esecuzione da un'immagine d'avvio in Windows PE:

> **Variabile della sequenza di attività** `_SMSTSInWinPE equals "false"`

Vedere questa condizione nel gruppo **Acquisisci file e impostazioni** del modello di sequenza di attività predefinita per installare un'immagine del sistema operativo esistente.

Per altre informazioni sulle condizioni, vedere [Editor delle sequenze di attività - Condizioni](task-sequence-editor.md#bkmk_conditions).

### <a name="custom-script"></a><a name="bkmk_access-script"></a> Script personalizzato

Le variabili possono essere lette e scritte usando l'oggetto COM **Microsoft.SMS.TSEnvironment** durante l'esecuzione della sequenza di attività.

L'esempio di Windows PowerShell seguente esegue una query sulla variabile **_SMSTSLogPath** per ottenere il percorso del log corrente. Lo script imposta inoltre una variabile personalizzata.

```PowerShell
# Create an object to access the task sequence environment
$tsenv = New-Object -ComObject Microsoft.SMS.TSEnvironment

# Query the environment to get an existing variable
# Set a variable for the task sequence log path
$LogPath = $tsenv.Value("_SMSTSLogPath")

# Or, convert all of the variables currently in the environment to PowerShell variables
$tsenv.GetVariables() | % { Set-Variable -Name "$_" -Value "$($tsenv.Value($_))" }

# Write a message to a log file
Write-Output "Hello world!" | Out-File -FilePath "$_SMSTSLogPath\mylog.log" -Encoding "Default" -Append

# Set a custom variable "startTime" to the current time
$tsenv.Value("startTime") = (Get-Date -Format HH:mm:ss) + ".000+000"
```

### <a name="windows-setup-answer-file"></a><a name="bkmk_access-answer"></a> File di risposte del programma di installazione di Windows

Il file di risposte del programma di installazione di Windows che si specifica può contenere variabili della sequenza di attività incorporate. Usare il formato `%varname%`, dove *varname* è il nome della variabile. Il passaggio **Imposta Windows e ConfigMgr** sostituisce la stringa del nome della variabile con il valore effettivo della variabile. Queste variabili incorporate della sequenza di attività non possono essere usate in campi di tipo solo numerico in un file di risposte unattend.xml.

Per altre informazioni, vedere [Impostare Windows e Configuration Manager](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr).

## <a name="see-also"></a>Vedere anche

- [Passaggi della sequenza di attività](task-sequence-steps.md)

- [Variabili della sequenza di attività](task-sequence-variables.md)

- [Considerazioni sulla pianificazione dell'automazione delle attività](../plan-design/planning-considerations-for-automating-tasks.md)

- [Editor delle sequenze di attività](task-sequence-editor.md)
