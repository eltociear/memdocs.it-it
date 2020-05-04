---
title: Aggiungere e assegnare app Win32 a Microsoft Intune
titleSuffix: ''
description: Informazioni su come aggiungere, assegnare e gestire app Win32 con Microsoft Intune. Questo argomento offre una panoramica delle funzionalità di distribuzione e gestione delle app Win32 di Intune, nonché informazioni sulla risoluzione dei problemi delle app Win32.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/02/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: efdc196b-38f3-4678-ae16-cdec4303f8d2
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8d1933350675a0d36042d1a4bd1e6a26c9a95814
ms.sourcegitcommit: 0e62655fef7afa7b034ac11d5f31a2a48bf758cb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/29/2020
ms.locfileid: "82254606"
---
# <a name="intune-standalone---win32-app-management"></a>Intune autonomo - Gestione di app Win32

[Intune autonomo](../fundamentals/mdm-authority-set.md) offre ora maggiori funzionalità di gestione delle app Win32. Anche se per i clienti connessi al cloud è possibile usare Configuration Manager per la gestione delle app Win32, i clienti solo di Intune avranno maggiori funzionalità di gestione per le app line-of-business Win32. Questo argomento offre una panoramica della funzionalità di gestione delle app Win32 di Intune e informazioni sulla risoluzione dei problemi.

> [!NOTE]
> Questa funzionalità di gestione delle app supporta l'architettura del sistema operativo sia a 32 bit che a 64 bit per le applicazioni di Windows.

> [!IMPORTANT]
> Quando si distribuiscono app Win32, è consigliabile usare esclusivamente l'approccio con l'[estensione di gestione di Intune](../apps/intune-management-extension.md), in particolare quando si usa un programma di installazione di app Win32 a più file. Se vengono installate sia app Win32 sia app line-of-business durante la registrazione di Autopilot, l'installazione dell'app potrebbe non riuscire. L'estensione di gestione di Intune viene installata automaticamente quando uno script di PowerShell o un'app Win32 viene assegnata all'utente o al dispositivo.

## <a name="prerequisites"></a>Prerequisiti

Per usare la gestione delle app Win32, assicurarsi che siano soddisfatti i criteri seguenti:

- Windows 10 versione 1607 o successive (edizioni Enterprise, Pro ed Education)
- Il client di Windows 10 deve essere: 
  - I dispositivi devono essere aggiunti ad Azure AD e registrati automaticamente. L'estensione di gestione di Intune supporta i dispositivi aggiunti ad Azure AD, aggiunti al dominio ibrido e registrati con Criteri di gruppo. 
  > [!NOTE]
  > Per lo scenario di registrazione con Criteri di gruppo: l'utente finale usa l'account utente locale per aggiungere ad AAD il dispositivo Windows 10. L'utente deve accedere al dispositivo usando il proprio account utente AAD ed eseguire la registrazione in Intune. Intune installerà l'estensione di gestione di Intune nel dispositivo se c'è uno script di PowerShell o un'app Win32 destinato all'utente o al dispositivo.
- Le applicazioni Windows possono avere dimensioni massime di 8 GB.

## <a name="prepare-the-win32-app-content-for-upload"></a>Preparare il contenuto delle app Win32 per il caricamento

Usare lo [strumento Microsoft di preparazione dei contenuti Win32](https://go.microsoft.com/fwlink/?linkid=2065730) per eseguire l'analisi preliminare delle app di Windows classico (Win32). Lo strumento converte i file di installazione delle applicazioni nel formato *intunewin*. Lo strumento rileva anche alcuni attributi richiesti da Intune per determinare lo stato di installazione delle applicazioni. Dopo aver usato questo strumento nella cartella di installazione delle app, sarà possibile creare un'app Win32 nella console di Intune.

> [!IMPORTANT]
> Lo [strumento Microsoft di preparazione dei contenuti Win32](https://go.microsoft.com/fwlink/?linkid=2065730) comprime tutti i file e le sottocartelle quando crea il file con estensione *intunewin*. Assicurarsi di mantenere lo strumento Microsoft di preparazione dei contenuti Win32 separato da file e cartelle del programma di installazione, in modo da non includere lo strumento o altri file o cartelle non necessari nel file con estensione *intunewin*.

È possibile scaricare lo [strumento Microsoft di preparazione dei contenuti Win32](https://go.microsoft.com/fwlink/?linkid=2065730) da GitHub come file ZIP. Il file compresso contiene una cartella denominata **Microsoft-Win32-Content-Prep-Tool-master**. La cartella contiene lo strumento di preparazione, la licenza, un file leggimi e le note sulla versione. 

### <a name="process-flow-to-create-intunewin-file"></a>Flusso del processo per la creazione del file con estensione intunewin

   <img alt="Process flow to create a .intunewin file" src="./media/apps-win32-app-management/prepare-win32-app.png" width="700">

### <a name="run-the-microsoft-win32-content-prep-tool"></a>Eseguire lo strumento Microsoft di preparazione dei contenuti Win32

Se si esegue `IntuneWinAppUtil.exe` dalla finestra di comando senza parametri, lo strumento guiderà l'utente nell'immissione dei parametri necessari. In alternativa, è possibile aggiungere i parametri al comando facendo riferimento ai seguenti parametri della riga di comando disponibili.

### <a name="available-command-line-parameters"></a>Parametri della riga di comando disponibili 

|    **Parametro della riga di comando**    |    **Descrizione**    |
|:------------------------------:|:----------------------------------------------------------:|
|    `-h`     |    Help    |
|    `-c <setup_folder>`     |    Cartella per tutti i file di installazione. Tutti i file in questa cartella verranno compressi in un file con estensione *intunewin*.    |
|    `-s <setup_file>`     |    File di installazione (ad esempio, *setup.exe* o *setup.msi*).    |
|    `-o <output_folder>`     |    Cartella di output per il file con estensione *intunewin* generato.    |
|    `-q`       |    Modalità non interattiva    |

### <a name="example-commands"></a>Comandi di esempio

|    **Comando di esempio**    |    **Descrizione**    |
|:-----------------------------------------------------------------------------------------:|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
|    `IntuneWinAppUtil -h`    |    Questo comando mostrerà le informazioni di utilizzo per lo strumento.    |
|    `IntuneWinAppUtil -c c:\testapp\v1.0 -s c:\testapp\v1.0\setup.exe -o c:\testappoutput\v1.0 -q`    |    Questo comando genererà il file `.intunewin` dalla cartella di origine e dal file di installazione specificati. Per il file di installazione MSI, questo strumento recupererà le informazioni necessarie per Intune. Se è specificato `-q`, il comando verrà eseguito in modalità non interattiva e se il file di output esiste già, verrà sovrascritto. Inoltre, se la cartella di output non esiste, verrà creata automaticamente.    |

Durante la generazione di un file con estensione *intunewin*, inserire gli eventuali file a cui è necessario fare riferimento in una sottocartella della cartella di installazione. Usare quindi un percorso relativo per fare riferimento al file specifico necessario. Ad esempio:

**Cartella di origine dell'installazione:** *c:\testapp\v1.0*<br>
**File di licenza:** *c:\testapp\v1.0\licenses\license.txt*

Fare riferimento al file *license.txt* usando il percorso relativo *licenses\license.txt*.

## <a name="create-assign-and-monitor-a-win32-app"></a>Creare, assegnare e monitorare un'app Win32

In modo analogo a un'app line-of-business, è possibile aggiungere un'app Win32 a Microsoft Intune. Questo tipo di app viene in genere scritto internamente o da terze parti. 

### <a name="process-flow-to-add-a-win32-app-to-intune"></a>Flusso del processo per l'aggiunta di un'app Win32 a Intune

<img alt="Process flow to add a Win32 app to Intune" src="./media/apps-win32-app-management/add-win32-app.svg" width="500">

### <a name="add-a-win32-app-to-intune"></a>Aggiungere un'app Win32 a Intune

I passaggi seguenti forniscono istruzioni per l'aggiunta di un'app di Windows a Intune.

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selezionare **App** > **Tutte le app** > **Aggiungi**.
3. Tra i tipi di app in **Altro** nel riquadro **Seleziona il tipo di app** selezionare **App Windows (Win32)** .

    > [!IMPORTANT]
    > Assicurarsi di usare la versione più recente dello strumento Microsoft di preparazione di contenuti Win32. Se non si usa la versione più recente, verrà visualizzato un avviso che indica che il pacchetto dell'app è stato compilato con una versione precedente dello strumento. 

4. Fare clic su **Seleziona**. Verrà visualizzata la procedura **Aggiungi app**.

## <a name="step-1---app-information"></a>Passaggio 1 - Informazioni sull'app

### <a name="select-the-app-package-file"></a>Selezionare il file del pacchetto dell'app

1. Nel riquadro **Aggiungi app** fare clic su **Selezionare il file del pacchetto di app**. 
2. Nel riquadro **File del pacchetto dell'app** selezionare il pulsante Sfoglia. Selezionare quindi un file di installazione di Windows con l'estensione *intunewin*.
   Verranno visualizzati i dettagli dell'app.
3. Al termine, selezionare **OK** nel riquadro **File del pacchetto dell'app**.

### <a name="set-app-information"></a>Impostare le informazioni sull'app

1. Nella pagina **Informazioni sull'app** aggiungere i dettagli relativi all'app. A seconda dell'app scelta, è possibile che alcuni valori nel riquadro vengano compilati automaticamente.
    - **Nome**: immettere il nome dell'app che viene visualizzato nel portale aziendale. Verificare che tutti i nomi di app usati siano univoci. Se il nome di un'app è usato due volte, solo una delle due app viene visualizzata nel portale aziendale.
    - **Descrizione**: immettere la descrizione dell'app. La descrizione viene visualizzata nel portale aziendale.
    - **Autore**: Immettere il nome dell'autore dell'app.
    - **Categoria**: selezionare una o più categorie di app predefinite o una categoria creata dall'utente. Le categorie consentono agli utenti di trovare più facilmente l'app nel portale aziendale.
    - **Visualizza come app in primo piano nel portale aziendale**: Visualizzare chiaramente l'app nella pagina principale del portale aziendale quando gli utenti cercano le app.
    - **URL di informazioni**: Immettere l'URL di un sito Web che include informazioni sull'app (facoltativo). L'URL viene visualizzato nel portale aziendale.
    - **URL privacy**: Immettere l'URL di un sito Web che include informazioni sulla privacy per l'app (facoltativo). L'URL viene visualizzato nel portale aziendale.
    - **Sviluppatore**: immettere il nome dello sviluppatore dell'app (facoltativo).
    - **Proprietario**: immettere un nome per il proprietario dell'app (facoltativo). Un esempio è **Reparto risorse umane**.
    - **Note**: immettere eventuali note da associare a questa app.
    - **Logo**: caricare un'icona che viene associata all'app. Questa icona viene visualizzata con l'app quando gli utenti visitano il portale aziendale.
2. Fare clic su **Avanti** per visualizzare la pagina **Programma**.

## <a name="step-2-program"></a>Passaggio 2: Programma

1. Nel pagina **Programma** configurare l'installazione dell'app e rimuovere i comandi per l'app:
    - **Comando di installazione**: Aggiungere la riga di comando di installazione completa per installare l'app. 

        Se, ad esempio, il nome file dell'app è **MyApp123**, aggiungere quanto segue:<br>
        `msiexec /p "MyApp123.msp"`<p>
        E, se l'applicazione è `ApplicationName.exe`, il comando sarà il nome dell'applicazione seguito dagli argomenti di comando (opzioni) supportati dal pacchetto. <br>
        Ad esempio:<br>
        `ApplicationName.exe /quiet`<br>
        Nel comando precedente il pacchetto `ApplicationName.exe` supporta l'argomento di comando `/quiet`.<p> 
        Per gli argomenti specifici supportati dal pacchetto dell'applicazione, contattare il fornitore dell'applicazione.

        > [!IMPORTANT]
        > Gli amministratori devono prestare attenzione quando usano gli strumenti da riga di comando. È possibile passare comandi imprevisti o dannosi usando il campo dei comandi di installazione e disinstallazione.

    - **Comando di disinstallazione**: Aggiungere la riga di comando di disinstallazione completa per disinstallare l'app in base al GUID dell'app stessa. 

        Ad esempio:<br>
        `msiexec /x "{12345A67-89B0-1234-5678-000001000000}"`

    - **Comportamento di installazione**: Impostare il comportamento di installazione su **Sistema** o **Utente**.

        > [!NOTE]
        > È possibile configurare un'app Win32 in modo che venga installata nel contesto **utente** o **di sistema**. Il contesto **utente** si riferisce solo a un determinato utente. Il contesto **di sistema** si riferisce a tutti gli utenti di un dispositivo Windows 10.
        >
        > Gli utenti finali non devono eseguire l'accesso al dispositivo per installare le app Win32.
        > 
        > L'installazione e la disinstallazione delle app Win32 verranno eseguite con privilegi di amministratore (per impostazione predefinita) quando l'app è configurata per l'installazione nel contesto utente e l'utente finale nel dispositivo dispone di privilegi amministrativi.
    
    - **Comportamento riavvio dispositivo**: Selezionare una delle opzioni seguenti:
        - **Determinare il comportamento in base ai codici restituiti**: Scegliere questa opzione per riavviare il dispositivo in base ai codici restituiti.
        - **Nessuna azione specifica**: Scegliere questa opzione per impedire i riavvii del dispositivo durante l'installazione delle app basate su MSI.
        - **L'installazione dell'app può forzare il riavvio del dispositivo**: Scegliere questa opzione per consentire il completamento dell'installazione dell'app senza impedire i riavvii.
        - **Intune forzerà il riavvio obbligatorio del dispositivo**: Scegliere questa opzione per riavviare sempre il dispositivo dopo l'installazione di un'app.

    - **Specificare i codici restituiti per indicare il comportamento successivo all'installazione**: Aggiungere i codici restituiti usati per specificare il comportamento in caso di nuovo tentativo di installazione dell'app o il comportamento successivo all'installazione. Le voci dei codici restituiti vengono aggiunte durante la creazione dell'app per impostazione predefinita. È tuttavia possibile aggiungere altri codici restituiti o modificare i codici restituiti esistenti.
        1. Nella colonna **Tipo di codice** impostare **Tipo di codice**  su uno dei valori seguenti:
            - **Errore**: valore restituito indicante un errore di installazione dell'app.
            - **Avvio a freddo**: Il codice restituito di avvio a freddo non consente di installare le app Win32 successive nel client senza riavvio. 
            - **Avvio a caldo**: il codice restituito di avvio a caldo consente di installare le app Win32 successive senza richiedere un riavvio del client. Il riavvio è necessario per completare l'installazione dell'applicazione corrente.
            - **Riprova**: l'agente del codice restituito di nuovo tentativo proverà a installare l'app tre volte. Attenderà 5 minuti tra un tentativo e l'altro. 
            - **Riuscita**: valore restituito indicante che l'app è stata installata correttamente.
        2. Se necessario, fare clic su **Aggiungi** per aggiungere i codici restituiti o modificare i codici restituiti esistenti.
2. Fare clic su **Avanti** per visualizzare la pagina **Requisiti**.        

## <a name="step-3-requirements"></a>Passaggio 3: Requisiti

1. Nella pagina **Requisiti** specificare i requisiti che i dispositivi devono soddisfare prima di installare l'app:
    - **Architettura del sistema operativo**: scegliere l'architettura necessaria per installare l'app.
    - **Sistema operativo minimo**: selezionare il sistema operativo minimo in cui è necessario installare l'app.
    - **Spazio su disco necessario (MB)** : aggiungere facoltativamente lo spazio libero su disco necessario nell'unità di sistema per installare l'app.
    - **Memoria fisica necessaria (MB)** : aggiungere facoltativamente la memoria fisica (RAM) necessaria per installare l'app.
    - **Numero minimo di processori logici necessari**: aggiungere facoltativamente il numero minimo di processori logici necessari per installare l'app.
    - **Velocità di CPU minima necessaria (MHz)** : aggiungere facoltativamente la velocità di CPU minima necessaria per installare l'app.
    - **Configurare regole aggiuntive relative ai requisiti**: 
        1. Fare clic su **Aggiungi** per visualizzare il riquadro **Aggiungi una regola relativa ai requisiti** e configurare le regole relative ai requisiti aggiuntive. Selezionare un'opzione per **Tipo di requisito** per scegliere il tipo di regola che si userà per determinare come viene convalidato un requisito. Le regole relative ai requisiti possono essere basate su informazioni del file system, valori del Registro di sistema o script di PowerShell. 
            - **File**: quando si sceglie **File** come **Tipo di requisito**, la regola relativa ai requisiti deve rilevare un file o una cartella, una data, una versione o una dimensione. 
                - **Percorso**: percorso completo della cartella contenente il file o la cartella da rilevare.
                - **File o cartella**: file o cartella da rilevare.
                - **Proprietà**: selezionare il tipo di regola da usare per convalidare la presenza dell'app.
                - **Associata a un'app a 32 bit nei client a 64 bit**: selezionare **Sì** per espandere eventuali variabili di ambiente PATH nel contesto a 32 bit nei client a 64 bit. Selezionare **No** (impostazione predefinita) per espandere eventuali variabili di ambiente nel contesto a 64 bit nei client a 64 bit. I client a 32 bit useranno sempre il contesto a 32 bit.
            - **Registro di sistema**: quando si sceglie **Registro** come **Tipo di requisito**, la regola relativa ai requisiti deve rilevare un'impostazione del Registro di sistema basata su un valore, una stringa, un numero intero o una versione.
                - **Percorso della chiave**: percorso completo della voce del Registro di sistema contenente il valore da rilevare.
                - **Nome valore**: nome del valore del Registro di sistema da rilevare. Se questo valore è vuoto, verrà eseguito il rilevamento della chiave. Il valore (predefinito) di una chiave verrà usato come valore di rilevamento se il metodo di rilevamento è diverso dall'esistenza del file o della cartella.
                - **Requisito relativo alla chiave del Registro di sistema**: selezionare il tipo di confronto della chiave del Registro di sistema usato per determinare come viene convalidata la regola relativa ai requisiti.
                - **Associata a un'app a 32 bit nei client a 64 bit**: selezionare **Sì** per eseguire ricerche nel Registro di sistema a 32 bit nei client a 64 bit. Selezionare **No** (impostazione predefinita) per eseguire ricerche nel Registro di sistema a 64 bit nei client a 64 bit. I client a 32 bit eseguiranno sempre ricerche nel registro di sistema a 32 bit.
            - **Script**: scegliere **Script** come **Tipo di requisito**, quando non è possibile creare una regola relativa ai requisiti basata su file, Registro di sistema o qualsiasi altro metodo disponibile nella console di Intune.
                - **File di script**: per una regola relativa ai requisiti basata su script di PowerShell, se il codice di uscita è 0, viene rilevato il contenuto di STDOUT in modio più dettagliato. Ad esempio, è possibile rilevare STDOUT come valore intero pari a 1.
                - **Esegui lo script come processo a 32 bit nei client a 64 bit**: selezionare **Sì** per eseguire lo script in un processo a 32 bit su client a 64 bit. Selezionare **No** (impostazione predefinita) per eseguire lo script in un processo a 64 bit su client a 64 bit. I client a 32 bit eseguono lo script in un processo a 32 bit.
                - **Esegui lo script con le credenziali dell'utente connesso**: selezionare **Sì** per eseguire lo script usando le credenziali del dispositivo connesso**.
                - **Imponi il controllo della firma degli script**: selezionare **Sì** per verificare che lo script sia firmato da un'entità di pubblicazione attendibile, in modo da consentire l'esecuzione dello script senza la visualizzazione di avvisi o richieste. Lo script verrà eseguito senza essere bloccato. Selezionare **No** (impostazione predefinita) per eseguire lo script con la conferma dell'utente finale senza la verifica della firma.
                - **Selezionare il tipo di dati di output**: selezionare il tipo di dati usato per determinare la corrispondenza di una regola relativa ai requisiti.
        2. Dopo aver impostato le regole relative ai requisiti, selezionare **OK**.
2. Fare clic su **Avanti** per visualizzare la pagina **Regole di rilevamento**.   

## <a name="step-4-detection-rules"></a>Passaggio 4: Regole di rilevamento

1. Nella pagina **Regole di rilevamento** configurare le regole per rilevare la presenza dell'app:
    
    **Formato delle regole**: selezionare come verrà rilevata la presenza dell'app. È possibile scegliere di configurare manualmente le regole di rilevamento oppure usare uno script personalizzato per rilevare la presenza dell'app. È necessario scegliere almeno una regola di rilevamento. 

    > [!NOTE]
    > Nel riquadro **Regole di rilevamento** è possibile scegliere di aggiungere più regole. Per rilevare l'app, devono essere soddisfatte le condizioni per **tutte** le regole.
    >
    > Se Intune rileva che l'app non è presente nel dispositivo, Intune offre di nuovo l'app dopo 24 ore. Questa situazione si verifica solo per le app a cui è assegnata la finalità obbligatoria.

    - **Configura manualmente le regole di rilevamento** - È possibile selezionare uno dei tipi di regole seguenti:
        1. **MSI**: eseguire una verifica in base al controllo della versione MSI. Questa opzione può essere aggiunta una sola volta. Quando si sceglie questo tipo di regola, sono disponibili due impostazioni:
            - **Codice prodotto MSI**: aggiungere un codice prodotto MSI valido per l'app.
            - **Verifica della versione del prodotto MSI**: selezionare **Sì** per verificare la versione del prodotto MSI oltre al codice del prodotto MSI.
        2. **File**: eseguire una verifica in base a rilevamento, data, versione o dimensioni del file o della cartella.
            - **Percorso**: percorso completo della cartella contenente il file o la cartella da rilevare.
            - **File o cartella**: file o cartella da rilevare.
            - **Metodo di rilevamento**: selezionare il tipo di metodo di rilevamento usato per convalidare la presenza dell'app.
            - **Associata a un'app a 32 bit nei client a 64 bit**: selezionare **Sì** per espandere eventuali variabili di ambiente PATH nel contesto a 32 bit nei client a 64 bit. Selezionare **No** (impostazione predefinita) per espandere eventuali variabili di ambiente nel contesto a 64 bit nei client a 64 bit. I client a 32 bit useranno sempre il contesto a 32 bit.
            
            **Esempi di rilevamento basato su file**
            1. Verificare la presenza del file.
         
                ![Screenshot del riquadro Regola di rilevamento - esistenza del file](./media/apps-win32-app-management/apps-win32-app-03.png)
        
            2. Verificare l'esistenza della cartella.
         
                ![Screenshot del riquadro Regola di rilevamento - esistenza della cartella](./media/apps-win32-app-management/apps-win32-app-04.png)
        
        3. **Registro**: eseguire una verifica in base a valore, stringa, Integer o versione.
            - **Percorso della chiave**: percorso completo della voce del Registro di sistema contenente il valore da rilevare.
            - **Nome valore**: nome del valore del Registro di sistema da rilevare. Se questo valore è vuoto, verrà eseguito il rilevamento della chiave. Il valore (predefinito) di una chiave verrà usato come valore di rilevamento se il metodo di rilevamento è diverso dall'esistenza del file o della cartella.
            - **Metodo di rilevamento**: selezionare il tipo di metodo di rilevamento usato per convalidare la presenza dell'app.
            - **Associata a un'app a 32 bit nei client a 64 bit**: selezionare **Sì** per eseguire ricerche nel Registro di sistema a 32 bit nei client a 64 bit. Selezionare **No** (impostazione predefinita) per eseguire ricerche nel Registro di sistema a 64 bit nei client a 64 bit. I client a 32 bit eseguiranno sempre ricerche nel registro di sistema a 32 bit.
            
            **Esempi di rilevamento basato sul Registro di sistema**
            1. Cercare la chiave del Registro di sistema esistente.
            
                ![Screenshot del riquadro Regola di rilevamento - chiave del Registro di sistema esistente](./media/apps-win32-app-management/apps-win32-app-05.png)    
            
            2. Verificare che il valore del Registro di sistema esista.
        
                ![Screenshot del riquadro Regola di rilevamento - valore del Registro di sistema esistente](./media/apps-win32-app-management/apps-win32-app-06.png)    
        
            3. Cercare la stringa del valore del Registro di sistema Equals.
        
                ![Screenshot del riquadro Regola di rilevamento - stringa del valore del Registro di sistema Equals](./media/apps-win32-app-management/apps-win32-app-07.png)    
     
    - **Usa uno script di rilevamento personalizzato**: specificare lo script di PowerShell che verrà usato per rilevare questa app. 
    
       1. **File di script**: selezionare uno script di PowerShell che rileverà la presenza dell'app nel client. L'app verrà rilevata quando lo script restituirà un codice di uscita con valore 0 e scriverà un valore stringa in STDOUT.

       2. **Esegui lo script come processo a 32 bit nei client a 64 bit**: selezionare **Sì** per eseguire lo script in un processo a 32 bit su client a 64 bit. Selezionare **No** (impostazione predefinita) per eseguire lo script in un processo a 64 bit su client a 64 bit. I client a 32 bit eseguono lo script in un processo a 32 bit.

       3. **Imponi il controllo della firma degli script**: selezionare **Sì** per verificare che lo script sia firmato da un'entità di pubblicazione attendibile, in modo da consentire l'esecuzione dello script senza la visualizzazione di avvisi o richieste. Lo script verrà eseguito senza essere bloccato. Selezionare **No** (impostazione predefinita) per eseguire lo script con la conferma dell'utente finale senza la verifica della firma.
    
            L'agente di Intune controlla i risultati dello script. Legge i valori scritti dallo script nel flusso di output standard (STDOUT) e nel flusso degli errori standard (STDERR), nonché il codice di uscita. Se il codice di uscita dello script è un valore diverso da zero, lo script non è riuscito e lo stato del rilevamento dell'applicazione è non installato. Se il codice di uscita è pari a zero e STDOUT contiene dati, lo stato di rilevamento dell'applicazione è installato. 

            > [!NOTE]
            > Microsoft consiglia la codifica dello script come UTF-8. Quando lo script viene chiuso con il valore 0, l'esecuzione dello script ha avuto esito positivo. Il secondo canale di output indica che l'app è stata rilevata e i dati di STDOUT indicano che l'app è stata trovata nel client. Non è necessario cercare una determinata stringa di STDOUT.

2. Dopo aver aggiunto le regole, selezionare **Avanti** per visualizzare la pagina **Dipendenze**.

## <a name="step-5-dependencies"></a>Passaggio 5: Dipendenze

Le dipendenze dell'app sono applicazioni che devono essere installate prima di poter installare l'app Win32. È possibile richiedere che altre app vengano installate come dipendenze. In particolare, il dispositivo deve installare le app dipendenti prima di installare l'app Win32. È previsto un massimo di 100 dipendenze, che include le dipendenze specificate e l'app stessa. È possibile aggiungere le dipendenze di un'app Win32 solo dopo aver aggiunto e caricato l'app Win32 in Intune. Una volta aggiunta l'app Win32, verrà visualizzata l'opzione **Dipendenze** nel riquadro dell'app Win32. 

Anche tutte le dipendenze dell'app Win32 devono essere un'app Win32. Non sono supportate dipendenze da altri tipi di app, ad esempio singole app LOB MSI o app dello Store.

Quando si aggiunge una dipendenza tra app, è possibile eseguire ricerche in base al nome dell'app e all'editore. Inoltre, è possibile ordinare le dipendenze aggiunte in base al nome dell'app e all'editore. Le dipendenze dell'app aggiunte in precedenza non possono essere selezionate nell'elenco di dipendenze tra app aggiunte. 

È possibile scegliere se installare o meno ogni app dipendente automaticamente. Per impostazione predefinita, l'opzione **Installazione automatica** è impostata su **Sì** per ogni dipendenza. Se si installa automaticamente un'app dipendente, anche se questa non è destinata all'utente o al dispositivo, Intune installerà l'app sul dispositivo per soddisfare la dipendenza prima di installare l'app Win32. È importante notare che una dipendenza può avere dipendenze secondarie ricorsive e ogni dipendenza secondaria verrà installata prima di installare la dipendenza principale. Inoltre, l'installazione delle dipendenze non segue un ordine di installazione a un livello di dipendenza specifico.

### <a name="select-the-dependencies"></a>Selezionare le dipendenze

Nella pagina **Dipendenze** selezionare le applicazioni che devono essere installate prima di poter installare l'app Win32:
1. Fare clic su **Aggiungi** per visualizzare il riquadro **Aggiungi una dipendenza**.
3. Una volta aggiunte le app dipendenti, fare clic su **Seleziona**.
4. Scegliere se installare automaticamente l'app dipendente selezionando **Sì** o **No** nella colonna **Installazione automatica**.
5. Fare clic su **Avanti** per visualizzare la pagina **Tag di ambito**.

### <a name="understand-additional-dependency-details"></a>Informazioni dettagliate sulle dipendenze aggiuntive

L'utente finale vedrà una notifica di tipo avviso popup di Windows che indica che sono in corso il download e l'installazione delle app dipendenti come parte del processo di installazione dell'app Win32. Inoltre, quando un'app dipendente non viene installata, l'utente finale vedrà in genere una delle notifiche seguenti:
- Non è stato possibile installare 1 o più app dipendenti
- I requisiti per 1 o più app dipendenti non sono stati rispettati
- 1 o più app dipendenti sono in attesa del riavvio del dispositivo

Se si sceglie No per l'opzione **Installazione automatica** per una dipendenza, non verrà eseguito un tentativo di installazione dell'app Win32. Inoltre, la segnalazione app indicherà che la dipendenza è stata contrassegnata come `failed`, oltre a fornire un motivo dell'errore. È possibile visualizzare l'errore di installazione delle dipendenze facendo clic su un errore (o un avviso) fornito nei [dettagli di installazione](troubleshoot-app-install.md#win32-app-installation-troubleshooting) dell'app Win32.

Ogni dipendenza dovrà rispettare la logica di ripetizione dei tentativi dell'app Win32 di Intune (3 tentativi di installazione dopo un'attesa di 5 minuti) e la pianificazione di rivalutazione globale. Le dipendenze, inoltre, sono applicabili solo al momento dell'installazione dell'app Win32 nel dispositivo. Le dipendenze non sono applicabili per la disinstallazione di un'app Win32. Per eliminare una dipendenza, è necessario fare clic sui puntini di sospensione (tre punti) a sinistra dell'app dipendente, alla fine della riga dell'elenco di dipendenze. 

## <a name="step-6---select-scope-tags-optional"></a>Passaggio 6: selezionare i tag di ambito (facoltativo)
È possibile usare i tag di ambito per determinare chi può visualizzare le informazioni sull'app client in Intune. Per informazioni dettagliate complete sui tag di ambito, vedere [Use role-based access control and scope tags for distributed IT](../fundamentals/scope-tags.md) (Usare il controllo degli accessi in base al ruolo e i tag di ambito per l'IT distribuito).

1. Fare clic su **Selezionare i tag di ambito** per aggiungere facoltativamente tag di ambito per l'app. 
2. Fare clic su **Avanti** per visualizzare la pagina **Assegnazioni**.

## <a name="step-7---assignments"></a>Passaggio 7: assegnazioni

Per l'assegnazione dell'app a gruppi, selezionare **Obbligatoria**, **Disponibile per i dispositivi registrati** o **Disinstalla**. Per altre informazioni, vedere [Aggiungere gruppi per organizzare utenti e dispositivi](../fundamentals/groups-add.md) e [Assegnare app ai gruppi con Microsoft Intune](apps-deploy.md).

1. Per l'app specifica, selezionare un tipo di assegnazione:
    - **Richiesto**: l'app viene installata nei dispositivi nei gruppi selezionati.
    - **Disponibile per i dispositivi registrati**: gli utenti installano l'app dall'app Portale aziendale o dal relativo sito Web.
    - **Uninstall** (Disinstalla): l'app viene disinstallata dai dispositivi nei gruppi selezionati.
2. Fare clic su **Aggiungi gruppi** e assegnare i gruppi che useranno questa app.
3. Nel riquadro **Selezionare i gruppi** selezionare l'assegnazione in base a utenti o dispositivi.
4. Dopo aver selezionato i gruppi, è anche possibile impostare **Notifiche per l'utente finale**, **Disponibilità** e **Scadenza installazione**. Per altre informazioni, vedere [Impostare la disponibilità e le notifiche delle app Win32](apps-win32-app-management.md#set-win32-app-availability-and-notifications).
5. Per escludere gruppi di utenti da questa assegnazione di app, selezionare **Incluso** nella colonna **Modalità**. Verrà visualizzato il riquadro **Modifica assegnazione**. È possibile modificare **modalità** da **Incluso** a **Escluso**. Fare clic su **OK** per chiudere il riquadro **Modifica assegnazione**.
6. Nella sezione **Impostazioni app** selezionare **Priorità di ottimizzazione recapito** per l'app. Questa impostazione determina come deve essere scaricato il contenuto dell'app. È possibile scegliere di scaricare il contenuto dell'app in modalità background o in primo piano a seconda dell'assegnazione. 
7. Dopo aver completato l'impostazione delle assegnazioni per le app, fare clic su **Avanti** per visualizzare la pagina **Rivedi e crea**.

## <a name="step-8---review--create"></a>Passaggio 8: verificare e creare

1. Verificare i valori e le impostazioni immessi per l'app. Verificare di aver configurato correttamente le informazioni sull'app.
2. Al termine, fare clic su **Crea** per aggiungere l'app a Intune.

    Verrà visualizzato il pannello **Panoramica** per l'app line-of-business.

A questo punto, sono stati completati i passaggi per l'aggiunta di un'app Win32 a Intune. Per informazioni sull'assegnazione e il monitoraggio di app, vedere [Assegnare app ai gruppi con Microsoft Intune](apps-deploy.md) e [Monitorare le informazioni sulle app e le assegnazioni con Microsoft Intune](apps-monitor.md).

## <a name="delivery-optimization"></a>Ottimizzazione recapito

I client Windows 10 1709 e versioni successive scaricheranno il contenuto dell'app Win32 di Intune mediante un componente di Ottimizzazione recapito nel client Windows 10. Ottimizzazione recapito offre funzionalità peer-to-peer attivate per impostazione predefinita. È possibile configurare l'agente di ottimizzazione recapito per scaricare il contenuto dell'app Win32 in background o in primo piano in base all'assegnazione. È possibile configurare Ottimizzazione recapito tramite Criteri di gruppo e tramite la configurazione dei dispositivi di Intune. Per altre informazioni, vedere [Ottimizzazione recapito per Windows 10](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization). 

> [!NOTE]
> È anche possibile installare un server Microsoft Connected Cache nei punti di distribuzione di Configuration Manager per memorizzare nella cache il contenuto dell'app Win32 di Intune. Per altre informazioni, vedere [Microsoft Connected Cache in Configuration Manager - Supporto per le app Win32 di Intune](https://docs.microsoft.com/configmgr/core/plan-design/hierarchy/microsoft-connected-cache#bkmk_intune).

## <a name="install-required-and-available-apps-on-devices"></a>Installare le app obbligatorie e disponibili nei dispositivi

L'utente finale riceverà le notifiche di tipo avviso popup di Windows per le installazioni delle app obbligatorie e disponibili. L'immagine seguente mostra un esempio di notifica di tipo avviso popup in cui l'installazione dell'app non risulta completa fino al riavvio del dispositivo. 

![Screenshot delle notifiche di tipo avviso popup di Windows per l'installazione di un'app](./media/apps-win32-app-management/apps-win32-app-08.png)    

Nell'immagine seguente l'utente finale riceve una notifica indicante che sono in corso modifiche all'app nel dispositivo.

![Screenshot di invio della notifica relativa alle modifiche in corso per l'app](./media/apps-win32-app-management/apps-win32-app-09.png)    

L'app Portale aziendale mostra inoltre i messaggi aggiuntivi sullo stato dell'installazione dell'app per gli utenti finali. Alle funzionalità di dipendenza Win32 vengono applicate le condizioni seguenti:
- Non è stato possibile installare l'app. Le dipendenze definite dall'amministratore non sono state soddisfatte.
- L'app è stata installata correttamente, ma è necessario un riavvio.
- È in corso l'installazione dell'app, ma è necessario un riavvio per continuare.

## <a name="set-win32-app-availability-and-notifications"></a>Impostare la disponibilità e le notifiche delle app Win32
È possibile configurare l'ora di inizio e l'ora di scadenza per un'app Win32. All'ora di inizio, l'estensione di gestione di Intune avvia il download del contenuto dell'app e lo memorizza nella cache. L'app viene installata all'ora di scadenza. Per le app disponibili, l'ora di inizio determina quando l'app sarà visibile nel Portale aziendale e il contenuto verrà scaricato quando l'utente finale richiede l'app dal Portale aziendale. È anche possibile abilitare un periodo di tolleranza per il riavvio. 

> [!IMPORTANT]
> L'impostazione **Periodo di tolleranza per il riavvio** nella sezione **Assegnazione** è disponibile solo quando **Comportamento riavvio dispositivo** della sezione **Programma** è impostato su una delle opzioni seguenti:
> - **Determinare il comportamento in base ai codici restituiti**
> - **Intune forzerà il riavvio obbligatorio del dispositivo**

Impostare la disponibilità dell'app in base a una data e un'ora per un'app obbligatoria seguendo questa procedura:

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selezionare **App** > **Tutte le app**.
3. Selezionare un'**App Windows (Win32)** esistente dall'elenco. 
4. Nel riquadro dell'app selezionare **Proprietà** > **Modifica** accanto alla sezione **Assegnazioni** > **Aggiungi gruppi** sotto il tipo di assegnazione **Obbligatoria**. 
   Si noti che la disponibilità dell'app può essere impostata in base al tipo di assegnazione. Il **Tipo di assegnazione** può essere **Obbligatorio**, **Disponibile per i dispositivi registrati** o **Disinstalla**.
5. Selezionare un gruppo nel riquadro **Seleziona gruppo** per specificare a quale gruppo di utenti verrà assegnata l'app. 

    > [!NOTE]
    > **Tipo di assegnazione** include le opzioni seguenti:<br>
    > - **Richiesto**: È possibile scegliere **Rendi questa app obbligatoria per tutti gli utenti** e/o **Rendi questa app obbligatoria in tutti i dispositivi**.<br>
    > - **Disponibile per i dispositivi registrati**: È possibile scegliere **Rendi questa app disponibile per tutti gli utenti con dispositivi registrati**.<br>
    > - **Uninstall** (Disinstalla): È possibile scegliere ***Disinstalla questa app per tutti gli utenti** e/o **Disinstalla questa app per tutti i dispositivi**.

6. Per modificare le opzioni di **Notifiche per l'utente finale**, selezionare **Mostra tutte le notifiche di tipo avviso popup**.
7. Nel riquadro **Modifica assegnazione** impostare **Notifiche per l'utente finale** su **Mostra tutte le notifiche di tipo avviso popup**. Si noti che è possibile impostare **Notifiche per l'utente finale** su **Mostra tutte le notifiche di tipo avviso popup**, **Mostra le notifiche di tipo avviso popup per i riavvii dei computer** o **Nascondi tutte le notifiche di tipo avviso popup**.
8. Impostare **Disponibilità dell'app** su **Data o ora specifiche** e selezionare la data e l'ora. La data e l'ora specificano quando l'app viene scaricata nel dispositivo degli utenti finali. 
9. Impostare **Scadenza dell'installazione app** su **Data o ora specifiche** e selezionare la data e l'ora. La data e l'ora specificano quando l'app viene installata nel dispositivo degli utenti finali. Quando viene effettuata più di un'assegnazione per lo stesso utente o dispositivo, viene selezionata l'ora di scadenza dell'installazione dell'app in base alla prima ora possibile.

10. Fare clic su **Abilitato** accanto a **Periodo di tolleranza per il riavvio**. Il periodo di tolleranza per il riavvio viene avviato non appena l'installazione dell'app è stata completata nel dispositivo. Quando è disabilitato, il dispositivo può essere riavviato senza preavviso. <br>È possibile personalizzare le opzioni seguenti:
    - **Periodo di tolleranza per il riavvio del dispositivo (minuti)** : Il valore predefinito è 1440 minuti (24 ore). Il valore massimo è di 2 settimane.
    - **Selezionare quando visualizzare la finestra di dialogo per il conto alla rovescia prima del riavvio (minuti)** : Il valore predefinito è 15 minuti.
    - **Consenti all'utente di posporre la notifica di riavvio**: È possibile scegliere **Sì** o **No**.
        - **Selezionare la durata della posposizione (minuti)** : Il valore predefinito è 240 minuti (4 ore). Il valore della posposizione non può essere maggiore del periodo di tolleranza per il riavvio.

11. Fare clic su **Verifica e salva**.

## <a name="toast-notifications-for-win32-apps"></a>Notifiche di tipo avviso popup per app Win32 
Se necessario, è possibile eliminare la visualizzazione delle notifiche di tipo avviso popup degli utenti finali per ogni assegnazione di app. In Intune selezionare **App** > **Tutte le app** > selezionare l'app > **Assegnazioni** > **Includi gruppi**. 

> [!NOTE]
> Le app Win32 installate dall'estensione di gestione di Intune non verranno disinstallate nei dispositivi di cui è stata annullata la registrazione. Gli amministratori possono sfruttare l'esclusione di assegnazione per non offrire l'app Win32 ai dispositivi BYOD.

## <a name="troubleshoot-win32-app-issues"></a>Risolvere i problemi delle app Win32
I log dell'agente nel computer client si trovano in genere in `C:\ProgramData\Microsoft\IntuneManagementExtension\Logs`. È possibile usare `CMTrace.exe` per visualizzare questi file di log. Per altre informazioni, vedere [CMTrace](https://docs.microsoft.com/configmgr/core/support/cmtrace).

![Screenshot dei log dell'agente nel computer client](./media/apps-win32-app-management/apps-win32-app-10.png)    

> [!IMPORTANT]
> Per consentire la corretta installazione e l'esecuzione delle app line-of-business Win32, le impostazioni antimalware devono escludere l'analisi delle directory seguenti:<p>
> **Nei computer client X64**:<br>
> *C:\Programmi (x86)\Microsoft Intune Management Extension\Content*<br>
> *C:\windows\IMECache*
>  
> **Nei computer client X86**:<br>
> *C:\Programmi\Microsoft Intune Management Extension\Content*<br>
> *C:\windows\IMECache*
>
> Per altre informazioni, vedere [Raccomandazioni per la ricerca di virus per computer aziendali che eseguono versioni attualmente supportate di Windows](https://support.microsoft.com/help/822158/virus-scanning-recommendations-for-enterprise-computers).

### <a name="detecting-the-win32-app-file-version-using-powershell"></a>Rilevare la versione del file dell'app Win32 con PowerShell

Se si hanno difficoltà nel rilevare la versione del file dell'app Win32, provare a usare o modificare il comando di PowerShell seguente:

``` PowerShell

$FileVersion = [System.Diagnostics.FileVersionInfo]::GetVersionInfo("<path to binary file>").FileVersion
#The below line trims the spaces before and after the version name
$FileVersion = $FileVersion.Trim();
if ("<file version of successfully detected file>" -eq $FileVersion)
{
#Write the version to STDOUT by default
$FileVersion
exit 0
}
else
{
#Exit with non-zero failure code
exit 1
}
```

Nel comando di PowerShell precedente sostituire la stringa `<path to binary file>` con il percorso del file dell'app Win32. Di seguito è illustrato un percorso di esempio:<br>
`C:\Program Files (x86)\Microsoft SQL Server Management Studio 18\Common7\IDE\ssms.exe`

Sostituire anche la stringa `<file version of successfully detected file>` con la versione del file da rilevare. Di seguito è illustrata una stringa di versione del file di esempio:<br>
`2019.0150.18118.00 ((SSMS_Rel).190420-0019)`

Se è necessario ottenere le informazioni sulla versione dell'app Win32, è possibile usare il comando di PowerShell seguente:

``` PowerShell

[System.Diagnostics.FileVersionInfo]::GetVersionInfo("<path to binary file>").FileVersion

```

Nel comando di PowerShell precedente sostituire `<path to binary file>` con il percorso del file.

### <a name="additional-troubleshooting-areas-to-consider"></a>Altre aree della risoluzione dei problemi da tenere in considerazione
- Controllare la destinazione per verificare che l'agente sia installato nel dispositivo: l'app Win32 destinata a un gruppo o lo script di PowerShell destinato a un gruppo creerà criteri di installazione dell'agente per il gruppo di sicurezza.
- Controllare la versione del sistema operativo: Windows 10 1607 e versioni successive.  
- Controllare lo SKU di Windows 10: Windows 10 S o le versioni di Windows in esecuzione con la modalità S abilitata non supportano l'installazione MSI.

Per altre informazioni sulla risoluzione dei problemi relativi alle app Win32, vedere [Risolvere i problemi di installazione delle app Win32](troubleshoot-app-install.md#win32-app-installation-troubleshooting).

## <a name="next-steps"></a>Passaggi successivi

- Per altre informazioni sull'aggiunta di app a Intune, vedere [Aggiungere app in Microsoft Intune](apps-add.md).
