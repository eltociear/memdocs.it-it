---
title: Aggiungere e assegnare app Win32 a Microsoft Intune
titleSuffix: ''
description: Informazioni su come aggiungere, assegnare e gestire app Win32 con Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5266f354ea5806743813d1aeb4c456890fa46b19
ms.sourcegitcommit: 4b8c317c71535c2d464f336c03b5bebdd2c6d4c9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/15/2020
ms.locfileid: "90083948"
---
# <a name="add-assign-and-monitor-a-win32-app-in-microsoft-intune"></a>Aggiungere, assegnare e monitorare un'app Win32 in Microsoft Intune

Dopo aver [preparato un'app Win32 da caricare in Intune](apps-win32-prepare.md) usando lo [strumento Microsoft di preparazione dei contenuti Win32](https://go.microsoft.com/fwlink/?linkid=2065730) è possibile aggiungere l'app a Intune. Per altre informazioni sulla preparazione di un'app Win32 per il caricamento, vedere [Preparare il contenuto dell'app Win32 per il caricamento](apps-win32-prepare.md).

## <a name="prerequisites"></a>Prerequisiti

Per usare la gestione delle app Win32, assicurarsi che siano soddisfatti i criteri seguenti:

- Usare Windows 10 versione 1607 o successive (edizioni Enterprise, Pro ed Education).
- I dispositivi devono essere stati aggiunti ad Azure Active Directory (Azure AD) e registrati automaticamente. L'estensione di gestione di Intune supporta i dispositivi aggiunti ad Azure AD, aggiunti al dominio ibrido e registrati con Criteri di gruppo. 
  > [!NOTE]
  > Per lo scenario di registrazione con Criteri di gruppo, l'utente usa l'account utente locale per aggiungere ad AAD il proprio dispositivo Windows 10. L'utente deve accedere al dispositivo usando il proprio account utente Azure AD e registrarsi in Intune. Intune installerà l'estensione di gestione di Intune nel dispositivo se c'è uno script di PowerShell o un'app Win32 destinato all'utente o al dispositivo.
- Le applicazioni Windows possono avere dimensioni massime di 8 GB.

In modo analogo a un'app line-of-business standard, è possibile aggiungere un'app Win32 a Microsoft Intune. Questo tipo di app viene in genere scritto internamente o da terze parti. 

## <a name="process-flow-to-add-a-win32-app-to-intune"></a>Flusso del processo per l'aggiunta di un'app Win32 a Intune

<img alt="Flow chart of the process to add a Win32 app to Intune." src="./media/apps-win32-app-management/add-win32-app.svg" width="500">

## <a name="add-a-win32-app-to-intune"></a>Aggiungere un'app Win32 a Intune

Seguire questa procedura per aggiungere un'app di Windows a Intune:

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selezionare **App** > **Tutte le app** > **Aggiungi**.
3. Tra i tipi di app in **Altro** nel riquadro **Seleziona il tipo di app** selezionare **App Windows (Win32)** .

    > [!IMPORTANT]
    > Assicurarsi di usare la versione più recente dello strumento Microsoft di preparazione di contenuti Win32. Se non si usa la versione più recente, un avviso indica che l'app è stata assemblata con una versione legacy dello strumento. 

4. Fare clic su **Seleziona**. Viene visualizzata la procedura **Aggiungi app**.

## <a name="step-1-app-information"></a>Passaggio 1: Informazioni sull'app

### <a name="select-the-app-package-file"></a>Selezionare il file del pacchetto dell'app

1. Nel riquadro **Aggiungi app** fare clic su **Selezionare il file del pacchetto di app**. 
2. Nel riquadro **File del pacchetto dell'app** selezionare il pulsante Sfoglia. Selezionare quindi un file di installazione di Windows con l'estensione *intunewin*.
   Vengono visualizzati i dettagli dell'app.
3. Al termine, selezionare **OK** nel riquadro **File del pacchetto dell'app**.

### <a name="set-app-information"></a>Impostare le informazioni sull'app

Nella pagina **Informazioni sull'app** aggiungere i dettagli relativi all'app. A seconda dell'app scelta, è possibile che alcuni valori nella pagina vengano compilati automaticamente.

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
- **Logo**: caricare un'icona associata all'app. Questa icona viene visualizzata con l'app quando gli utenti visitano il portale aziendale.

Selezionare **Avanti** per visualizzare la pagina **Programma**.

## <a name="step-2-program"></a>Passaggio 2: Programma

Nel pagina **Programma** configurare l'installazione dell'app e rimuovere i comandi per l'app:

- **Comando di installazione**: Aggiungere la riga di comando di installazione completa per installare l'app. 

    Se ad esempio il nome file dell'app è **MyApp123**, aggiungere quanto segue:

    `msiexec /p "MyApp123.msp"`
    
    Se l'applicazione è `ApplicationName.exe`, il comando sarà il nome dell'applicazione seguito dagli argomenti di comando (opzioni) supportati dal pacchetto. Ad esempio:

    `ApplicationName.exe /quiet`
    
    Nel comando precedente il pacchetto `ApplicationName.exe` supporta l'argomento di comando `/quiet`. 
    
    Per gli argomenti specifici supportati dal pacchetto dell'applicazione, contattare il fornitore dell'applicazione.

    > [!IMPORTANT]
    > Gli amministratori devono prestare attenzione quando usano gli strumenti della riga di comando. È possibile che tramite i campi **Comando di installazione** e **Comando di disinstallazione** vengano passati comandi inattesi o dannosi.

- **Comando di disinstallazione**: aggiungere la riga di comando completa per disinstallare l'app in base al GUID dell'app stessa. 

    Ad esempio:
    
    `msiexec /x "{12345A67-89B0-1234-5678-000001000000}"`

- **Comportamento di installazione**: Impostare il comportamento di installazione su **Sistema** o **Utente**.

    > [!NOTE]
    > È possibile configurare un'app Win32 in modo che venga installata nel contesto **utente** o **di sistema**. Il contesto **utente** si riferisce solo a un utente specifico. Il contesto **di sistema** si riferisce a tutti gli utenti di un dispositivo Windows 10.
    >
    > Gli utenti non devono eseguire l'accesso al dispositivo per installare le app Win32.
    > 
    > L'installazione e la disinstallazione delle app Win32 verranno eseguite con privilegi di amministratore (per impostazione predefinita) quando l'app è configurata per l'installazione nel contesto utente e l'utente nel dispositivo dispone di privilegi di amministratore.
    
- **Comportamento riavvio dispositivo**: Selezionare una delle opzioni seguenti:
    - **Determinare il comportamento in base ai codici restituiti**: Scegliere questa opzione per riavviare il dispositivo in base ai codici restituiti.
    - **Nessuna azione specifica**: Scegliere questa opzione per impedire i riavvii del dispositivo durante l'installazione delle app basate su MSI.
    - **L'installazione dell'app può forzare il riavvio del dispositivo**: Scegliere questa opzione per consentire il completamento dell'installazione dell'app senza impedire i riavvii.
    - **Intune forzerà il riavvio obbligatorio del dispositivo**: Scegliere questa opzione per riavviare sempre il dispositivo dopo l'installazione di un'app.

- **Specificare i codici restituiti per indicare il comportamento successivo all'installazione**: Aggiungere i codici restituiti usati per specificare il comportamento in caso di nuovo tentativo di installazione dell'app o il comportamento successivo all'installazione. Le voci dei codici restituiti vengono aggiunte durante la creazione dell'app per impostazione predefinita. È tuttavia possibile aggiungere altri codici restituiti o modificare i codici restituiti esistenti.
    1. Nella colonna **Tipo di codice** impostare **Tipo di codice**  su uno dei valori seguenti:
        - **Operazione non riuscita**: valore restituito indicante un errore di installazione dell'app.
        - **Avvio a freddo**: il codice restituito di avvio a freddo non consente di installare l'app Win32 successiva nel client senza riavvio. 
        - **Avvio a caldo**: il codice restituito di avvio a caldo consente di installare l'app Win32 successiva senza richiedere un riavvio del client. Il riavvio è necessario per completare l'installazione dell'applicazione corrente.
        - **Riprova**: l'agente del codice restituito di nuovo tentativo proverà a installare l'app per tre volte. Attenderà cinque minuti tra un tentativo e l'altro. 
        - **Operazione riuscita**: valore restituito indicante che l'app è stata installata correttamente.
    2. Se necessario, selezionare **Aggiungi** per aggiungere altri codici restituiti o modificare i codici restituiti esistenti.

Selezionare **Avanti** per visualizzare la pagina **Requisiti**.    

## <a name="step-3-requirements"></a>Passaggio 3: Requisiti

Nella pagina **Requisiti** specificare i requisiti che i dispositivi devono soddisfare prima di installare l'app:

- **Architettura del sistema operativo**: Scegliere le architetture necessarie per installare l'app.
- **Sistema operativo minimo**: selezionare il sistema operativo minimo in cui è necessario installare l'app.
- **Spazio su disco necessario (MB)** : aggiungere facoltativamente lo spazio libero su disco necessario nell'unità di sistema per installare l'app.
- **Memoria fisica necessaria (MB)** : aggiungere facoltativamente la memoria fisica (RAM) necessaria per installare l'app.
- **Numero minimo di processori logici necessari**: aggiungere facoltativamente il numero minimo di processori logici necessari per installare l'app.
- **Velocità di CPU minima necessaria (MHz)** : aggiungere facoltativamente la velocità di CPU minima necessaria per installare l'app.
- **Configurare regole aggiuntive relative ai requisiti**: 
    1. Selezionare **Aggiungi** per visualizzare il riquadro **Aggiungi una regola relativa ai requisiti** e configurare regole relative ai requisiti aggiuntive. Selezionare il valore di **Tipo di requisito** per scegliere il tipo di regola che si userà per determinare come viene convalidato un requisito. Le regole relative ai requisiti possono essere basate su informazioni del file system, valori del Registro di sistema o script di PowerShell. 
        - **File**: quando si sceglie **File** come valore di **Tipo di requisito**, la regola relativa ai requisiti deve rilevare un file o una cartella, una data, una versione o una dimensione. 
            - **Percorso**: percorso completo della cartella contenente il file o la cartella da rilevare.
            - **File o cartella**: file o cartella da rilevare.
            - **Proprietà**: selezionare il tipo di regola da usare per convalidare la presenza dell'app.
            - **Associata a un'app a 32 bit nei client a 64 bit**: selezionare **Sì** per espandere eventuali variabili di ambiente PATH nel contesto a 32 bit nei client a 64 bit. Selezionare **No** (impostazione predefinita) per espandere eventuali variabili di ambiente nel contesto a 64 bit nei client a 64 bit. I client a 32 bit useranno sempre il contesto a 32 bit.
        - **Registro di sistema**: quando si sceglie **Registro** come valore di **Tipo di requisito**, la regola relativa ai requisiti deve rilevare un'impostazione del Registro di sistema sulla base di un valore, una stringa, un numero intero o una versione.
            - **Percorso della chiave**: percorso completo della voce del Registro di sistema contenente il valore da rilevare.
            - **Nome valore**: nome del valore del Registro di sistema da rilevare. Se questo valore è vuoto, verrà eseguito il rilevamento della chiave. Il valore (predefinito) di una chiave verrà usato come valore di rilevamento se il metodo di rilevamento è diverso dall'esistenza del file o della cartella.
            - **Requisito relativo alla chiave del Registro di sistema**: selezionare il tipo di confronto della chiave del Registro di sistema usato per determinare come viene convalidata la regola relativa ai requisiti.
            - **Associata a un'app a 32 bit nei client a 64 bit**: selezionare **Sì** per eseguire ricerche nel Registro di sistema a 32 bit nei client a 64 bit. Selezionare **No** (impostazione predefinita) per eseguire ricerche nel Registro di sistema a 64 bit nei client a 64 bit. I client a 32 bit eseguiranno sempre ricerche nel registro di sistema a 32 bit.
        - **Script**: scegliere **Script** come valore di **Tipo di requisito**, quando non è possibile creare una regola relativa ai requisiti basata su file, Registro di sistema o qualsiasi altro metodo disponibile nella console di Intune.
            - **File di script**: Per una regola basata su un requisito di script di PowerShell, se il codice esistente è 0, l'output standard (STDOUT) verrà rilevato in modo più dettagliato. Ad esempio, è possibile rilevare STDOUT come valore intero pari a 1.
            - **Esegui lo script come processo a 32 bit su client a 64 bit**: selezionare **Sì** per eseguire lo script in un processo a 32 bit su client a 64 bit. Selezionare **No** (impostazione predefinita) per eseguire lo script in un processo a 64 bit su client a 64 bit. I client a 32 bit eseguono lo script in un processo a 32 bit.
            - **Esegui lo script con le credenziali dell'utente connesso**: selezionare **Sì** per eseguire lo script usando le credenziali del dispositivo connesso.
            - **Imponi il controllo della firma degli script**: selezionare **Sì** per verificare che lo script sia stato firmato da un autore attendibile, in modo da consentire l'esecuzione dello script senza che vengano visualizzati avvisi o richieste. Lo script verrà eseguito senza essere bloccato. Selezionare **No** (impostazione predefinita) per eseguire lo script con la conferma dell'utente senza la verifica della firma.
            - **Selezionare il tipo di dati di output**: selezionare il tipo di dati usato per determinare la corrispondenza di una regola relativa ai requisiti.
    2. Dopo aver impostato le regole relative ai requisiti, selezionare **OK**.

Selezionare **Avanti** per visualizzare la pagina **Regole di rilevamento**. 

## <a name="step-4-detection-rules"></a>Passaggio 4: Regole di rilevamento

Nella pagina **Regole di rilevamento** configurare le regole per rilevare la presenza dell'app:
    
- **Formato delle regole**: selezionare come verrà rilevata la presenza dell'app. È possibile scegliere di configurare manualmente le regole di rilevamento oppure usare uno script personalizzato per rilevare la presenza dell'app. È necessario scegliere almeno una regola di rilevamento. 

  > [!NOTE]
  > Nel riquadro **Regole di rilevamento** è possibile scegliere di aggiungere più regole. Per rilevare l'app, devono essere soddisfatte le condizioni per *tutte* le regole.
  >
  > Se Intune rileva che l'app non è presente nel dispositivo, Intune offre di nuovo l'app dopo 24 ore. Questa situazione si verificherà solo per le app destinate alla finalità richiesta.

- **Configura manualmente le regole di rilevamento**: è possibile selezionare uno dei tipi di regola seguenti:
    - **MSI**: eseguire una verifica in base a un controllo della versione MSI. Questa opzione può essere aggiunta una sola volta. Quando si sceglie questo tipo di regola, sono disponibili due impostazioni:
        - **Codice prodotto MSI**: aggiungere un codice prodotto MSI valido per l'app.
        - **Verifica della versione del prodotto MSI**: selezionare **Sì** per verificare la versione del prodotto MSI oltre al codice prodotto MSI.
    - **File**: eseguire una verifica in base a rilevamento, data, versione o dimensioni del file o della cartella.
        - **Percorso**: immettere il percorso completo della cartella contenente il file o la cartella da rilevare.
        - **File o cartella**: immettere il file o la cartella da rilevare.
        - **Metodo di rilevamento**: selezionare il tipo di metodo di rilevamento usato per convalidare la presenza dell'app.
        - **Associata a un'app a 32 bit nei client a 64 bit**: selezionare **Sì** per espandere eventuali variabili di ambiente PATH nel contesto a 32 bit nei client a 64 bit. Selezionare **No** (impostazione predefinita) per espandere eventuali variabili di ambiente nel contesto a 64 bit nei client a 64 bit. I client a 32 bit useranno sempre il contesto a 32 bit.
            
        **Esempi di rilevamento basato su file**

        Verificare la presenza del file.
         
        ![Screenshot del riquadro Regola di rilevamento - esistenza del file.](./media/apps-win32-app-management/apps-win32-app-03.png)
        
        Verificare l'esistenza della cartella.
        
        ![Screenshot del riquadro Regola di rilevamento - esistenza della cartella.](./media/apps-win32-app-management/apps-win32-app-04.png)
        
    - **Registro di sistema**: eseguire una verifica in base a valore, stringa, Integer o versione.
        - **Percorso della chiave**: percorso completo della voce del Registro di sistema contenente il valore da rilevare. Una sintassi valida è HKEY_LOCAL_MACHINE\Software\WinRAR o HKLM\Software\WinRAR.
        - **Nome valore**: nome del valore del Registro di sistema da rilevare. Se questo valore è vuoto, verrà eseguito il rilevamento della chiave. Il valore (predefinito) di una chiave verrà usato come valore di rilevamento se il metodo di rilevamento è diverso dall'esistenza del file o della cartella.
        - **Metodo di rilevamento**: selezionare il tipo di metodo di rilevamento usato per convalidare la presenza dell'app.
        - **Associata a un'app a 32 bit nei client a 64 bit**: selezionare **Sì** per eseguire ricerche nel Registro di sistema a 32 bit nei client a 64 bit. Selezionare **No** (impostazione predefinita) per eseguire ricerche nel Registro di sistema a 64 bit nei client a 64 bit. I client a 32 bit eseguiranno sempre ricerche nel registro di sistema a 32 bit.
            
        **Esempi di rilevamento basato sul Registro di sistema**
        
        Verificare che la chiave del Registro di sistema esista.
            
        ![Screenshot del riquadro Regola di rilevamento - chiave del Registro di sistema esistente.](./media/apps-win32-app-management/apps-win32-app-05.png)    
            
        Verificare che il valore del Registro di sistema esista.
        
        ![Screenshot del riquadro Regola di rilevamento - valore del Registro di sistema esistente.](./media/apps-win32-app-management/apps-win32-app-06.png)    
        
        Cercare la stringa del valore del Registro di sistema Equals.
        
        ![Screenshot del riquadro Regola di rilevamento - stringa del valore del Registro di sistema Uguale a.](./media/apps-win32-app-management/apps-win32-app-07.png)    
     
- **Usa uno script di rilevamento personalizzato**: Specificare lo script che verrà usato per rilevare l'applicazione. 
    
   - **File di script**: selezionare uno script di PowerShell che rileverà la presenza dell'app nel client. L'app verrà rilevata quando lo script restituirà un codice di uscita con valore **0** e scriverà un valore stringa in STDOUT.

   - **Esegui lo script come processo a 32 bit su client a 64 bit**: selezionare **Sì** per eseguire lo script in un processo a 32 bit su client a 64 bit. Selezionare **No** (impostazione predefinita) per eseguire lo script in un processo a 64 bit su client a 64 bit. I client a 32 bit eseguono lo script in un processo a 32 bit.

   - **Imponi il controllo della firma degli script**: selezionare **Sì** per verificare che lo script sia stato firmato da un autore attendibile, in modo da consentire l'esecuzione dello script senza che vengano visualizzati avvisi o richieste. Lo script verrà eseguito senza essere bloccato. Selezionare **No** (impostazione predefinita) per eseguire lo script con la conferma dell'utente senza la verifica della firma.
    
   L'agente di Intune controlla i risultati dello script. Legge i valori scritti dallo script nel flusso STDOUT e nel flusso degli errori standard (STDERR), nonché il codice di uscita. Se il codice di uscita dello script è un valore diverso da zero, lo script non è riuscito e lo stato del rilevamento dell'applicazione è non installato. Se il codice di uscita è pari a zero e STDOUT contiene dati, lo stato di rilevamento dell'applicazione è installato. 

   > [!NOTE]
   > È consigliabile codificare lo script come UTF-8. Quando lo script viene chiuso con il valore **0**, l'esecuzione dello script ha avuto esito positivo. Il secondo canale di output indica che l'app è stata rilevata. I dati STDOUT indicano che l'app è stata trovata nel client. Non è necessario cercare una determinata stringa di STDOUT.

Dopo aver aggiunto le regole, selezionare **Avanti** per visualizzare la pagina **Dipendenze**.

## <a name="step-5-dependencies"></a>Passaggio 5: Dipendenze

Le dipendenze dell'app sono applicazioni che devono essere installate prima di poter installare l'app Win32. È possibile richiedere che altre app vengano installate come dipendenze. 

In particolare, il dispositivo deve installare le app dipendenti prima di installare l'app Win32. È previsto un massimo di 100 dipendenze, che include le dipendenze specificate e l'app stessa. 

È possibile aggiungere le dipendenze di un'app Win32 solo dopo aver aggiunto e caricato l'app Win32 in Intune. Dopo l'aggiunta dell'app Win32, nel riquadro dell'app Win32 verrà visualizzata l'opzione **Dipendenze**. 

Anche tutte le dipendenze dell'app Win32 devono essere app Win32. Non sono supportate dipendenze da altri tipi di app, ad esempio singole app LOB MSI o app di Microsoft Store.

Quando si aggiunge una dipendenza tra app, è possibile eseguire ricerche in base al nome dell'app e all'editore. Inoltre, è possibile ordinare le dipendenze aggiunte in base al nome dell'app e all'editore. Le dipendenze dell'app aggiunte in precedenza non possono essere selezionate nell'elenco di dipendenze tra app aggiunte. 

È possibile scegliere se installare o meno ogni app dipendente automaticamente. Per impostazione predefinita, l'opzione **Installazione automatica** è impostata su **Sì** per ogni dipendenza. Se si installa automaticamente un'app dipendente, anche se questa non è destinata all'utente o al dispositivo, Intune installerà l'app sul dispositivo per soddisfare la dipendenza prima di installare l'app Win32. 

È importante notare che una dipendenza può avere dipendenze secondarie ricorsive e ogni dipendenza secondaria verrà installata prima di installare la dipendenza principale. Inoltre l'installazione delle dipendenze non segue un ordine specifico per un livello di dipendenza.

### <a name="select-the-dependencies"></a>Selezionare le dipendenze

Nella pagina **Dipendenze** selezionare le applicazioni che devono essere installate prima di poter installare l'app Win32:
1. Selezionare **Aggiungi** per visualizzare il riquadro **Aggiungi una dipendenza**.
3. Aggiungere le app dipendenti, quindi fare clic su **Seleziona**.
4. Scegliere se installare automaticamente le app dipendenti selezionando **Sì** o **No** nella colonna **Installazione automatica**.

Dopo aver selezionato le dipendenze, selezionare **Avanti** per visualizzare la pagina **Tag di ambito**.

### <a name="understand-additional-dependency-details"></a>Informazioni dettagliate sulle dipendenze aggiuntive

L'utente vedrà notifiche di Windows indicanti che sono in corso il download e l'installazione delle app dipendenti come parte del processo di installazione dell'app Win32. Inoltre quando un'app dipendente non viene installata l'utente vede in genere una delle notifiche seguenti:
- Non è stato possibile installare una o più app dipendenti.
- I requisiti per una o più app dipendenti non sono stati rispettati.
- Una o più app dipendenti sono in attesa del riavvio del dispositivo.

Se si sceglie di non inserire una dipendenza nella colonna **Installazione automatica**, non verrà tentata l'installazione dell'app Win32. La segnalazione app indicherà anche che la dipendenza è stata contrassegnata come `failed` e specificherà un motivo dell'errore. È possibile visualizzare l'errore di installazione delle dipendenze selezionando un errore (o un avviso) visualizzato nei [dettagli di installazione](troubleshoot-app-install.md#win32-app-installation-troubleshooting) dell'app Win32.

Ogni dipendenza dovrà rispettare la logica di ripetizione dei tentativi dell'app Win32 di Intune (tre tentativi di installazione dopo un'attesa di cinque minuti) e la pianificazione di rivalutazione globale. Le dipendenze sono anche applicabili solo al momento dell'installazione dell'app Win32 nel dispositivo. Le dipendenze non sono applicabili per la disinstallazione di un'app Win32. Per eliminare una dipendenza, selezionare i puntini di sospensione (tre punti) a sinistra dell'app dipendente, alla fine della riga dell'elenco di dipendenze. 

## <a name="step-6-select-scope-tags-optional"></a>Passaggio 6: Selezionare i tag di ambito (facoltativo)
È possibile usare i tag di ambito per determinare chi può visualizzare le informazioni sull'app client in Intune. Per informazioni dettagliate complete sui tag di ambito, vedere [Use role-based access control and scope tags for distributed IT](../fundamentals/scope-tags.md) (Usare il controllo degli accessi in base al ruolo e i tag di ambito per l'IT distribuito).

Fare clic su **Selezionare i tag di ambito** per aggiungere facoltativamente tag di ambito per l'app. Quindi selezionare **Avanti** per visualizzare la pagina **Assegnazioni**.

## <a name="step-7-assignments"></a>Passaggio 7: Assignments

Per l'assegnazione dell'app a gruppi, selezionare **Obbligatoria**, **Disponibile per i dispositivi registrati** o **Disinstalla**. Per altre informazioni, vedere [Aggiungere gruppi per organizzare utenti e dispositivi](../fundamentals/groups-add.md) e [Assegnare app ai gruppi con Microsoft Intune](apps-deploy.md).

1. Per l'app specifica, selezionare un tipo di assegnazione:
    - **Richiesto**: l'app viene installata nei dispositivi nei gruppi selezionati.
    - **Disponibile per i dispositivi registrati**: gli utenti installano l'app dall'app del portale aziendale o dal relativo sito Web.
    - **Uninstall** (Disinstalla): l'app viene disinstallata dai dispositivi nei gruppi selezionati.
2. Selezionare **Aggiungi gruppi** e assegnare i gruppi che useranno questa app.
3. Nel riquadro **Seleziona gruppi** selezionare l'assegnazione in base a utenti o dispositivi.
4. Dopo aver selezionato i gruppi è anche possibile impostare **Notifiche per l'utente finale**, **Disponibilità** e **Scadenza installazione**. Per altre informazioni, vedere [Impostare la disponibilità e le notifiche delle app Win32](apps-win32-app-management.md#set-win32-app-availability-and-notifications).
5. Se non si vuole che questa assegnazione di app influisca sui gruppi di utenti, selezionare **Inclusi** nella colonna **Modalità**. Nel riquadro **Modifica assegnazione** modificare il valore di **Modalità** da  **Inclusi** a **Esclusi**. Selezionare **OK** per chiudere il riquadro **Modifica assegnazione**.
6. Nella sezione **Impostazioni app** selezionare il valore di **Priorità di ottimizzazione recapito** per l'app. Questa impostazione determina come deve essere scaricato il contenuto dell'app. È possibile scegliere di scaricare il contenuto dell'app in modalità background o in primo piano a seconda dell'assegnazione. 

Al termine dell'impostazione delle assegnazioni per le app, selezionare **Avanti** per visualizzare la pagina **Rivedi e crea**.

## <a name="step-8-review-and-create"></a>Passaggio 8: Rivedi e crea

1. Verificare le impostazioni e i valori specificati per l'app. Verificare di aver configurato correttamente le informazioni sull'app.
2. Selezionare **Crea** per aggiungere l'app a Intune.

    Viene visualizzato il riquadro **Panoramica** per l'app line-of-business.

A questo punto sono stati completati i passaggi per l'aggiunta di un'app Win32 a Intune. Per informazioni sull'assegnazione e il monitoraggio di app, vedere [Assegnare app ai gruppi con Microsoft Intune](apps-deploy.md) e [Monitorare le informazioni sulle app e le assegnazioni con Microsoft Intune](apps-monitor.md).

## <a name="next-steps"></a>Passaggi successivi

- [Monitorare le informazioni sulle app e le assegnazioni con Microsoft Intune](apps-monitor.md)
- [Risolvere i problemi delle app Win32](apps-win32-troubleshoot.md)
