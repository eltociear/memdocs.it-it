---
title: Creare una sequenza di attività per l'aggiornamento del sistema operativo
titleSuffix: Configuration Manager
description: Usare una sequenza di attività per eseguire automaticamente l'aggiornamento da Windows 7 o versioni successive a Windows 10
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 7591e386-a9ab-4640-8643-332dce5aa006
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6ad36978f3f3dc5207068a65d76bf8f5c7c3078c
ms.sourcegitcommit: e2ef7231d3abaf3c925b0e5ee9f66156260e3c71
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85383241"
---
# <a name="create-a-task-sequence-to-upgrade-an-os-in-configuration-manager"></a>Creare una sequenza di attività per aggiornare un sistema operativo in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Usare le sequenze di attività in Configuration Manager per aggiornare automaticamente un sistema operativo in un computer di destinazione. L'aggiornamento può essere eseguito da Windows 7 o versione successiva fino a Windows 10 o da Windows Server 2012 o versione successiva fino a Windows Server 2016. Creare una sequenza di attività che faccia riferimento al pacchetto di aggiornamento del sistema operativo e a eventuali altri contenuti da installare, ad esempio applicazioni o aggiornamenti software. La sequenza di attività per aggiornare un sistema operativo fa parte dello scenario [Aggiornare Windows alla versione più recente](upgrade-windows-to-the-latest-version.md).  


## <a name="prerequisites"></a>Prerequisiti

Prima di creare la sequenza di attività, devono essere soddisfatti i requisiti seguenti:

### <a name="required"></a>Richiesto

- Il [pacchetto di aggiornamento del sistema operativo](../get-started/manage-operating-system-upgrade-packages.md) deve essere disponibile nella console di Configuration Manager.  

- Quando si esegue l'aggiornamento a Windows Server 2016, selezionare l'impostazione **Ignore any dismissable compatibility messages** (Ignora eventuali messaggi di compatibilità che possono essere chiusi) nel passaggio della sequenza di attività Aggiorna sistema operativo. In caso contrario, l'aggiornamento ha esito negativo.  

### <a name="required-if-used"></a>Obbligatorio (se usato)  

- Gli [aggiornamenti software](../../sum/get-started/synchronize-software-updates.md) devono essere sincronizzati nella console di Configuration Manager.  

- Le [applicazioni](../../apps/deploy-use/create-applications.md) devono essere aggiunte alla console di Configuration Manager.  


## <a name="create-a-task-sequence-to-upgrade-an-os"></a><a name="BKMK_UpgradeOS"></a> Creare una sequenza di attività per aggiornare un sistema operativo  

Per aggiornare il sistema operativo nei client, è possibile creare una sequenza di attività e selezionare **Aggiorna sistema operativo dal pacchetto di aggiornamento** nella Creazione guidata della sequenza di attività. La procedura guidata aggiunge i passaggi della sequenza di attività per aggiornare il sistema operativo, applicare gli aggiornamenti software e installare le applicazioni.

1. Nella console di Configuration Manager passare all'area di lavoro **Raccolta software**, espandere **Sistemi operativi** e quindi selezionare **Sequenze di attività**.  

2. Nella scheda **Home** della barra multifunzione nel gruppo **Crea** selezionare **Crea sequenza di attività**.  

3. Nella pagina **Crea una nuova sequenza di attività** della Creazione guidata della sequenza di attività selezionare **Aggiorna sistema operativo dal pacchetto di aggiornamento** e quindi selezionare **Avanti**.  

4. Nella pagina **Informazioni sequenza di attività** specificare le impostazioni seguenti:  

    - **Nome sequenza di attività**: Specificare un nome che identifica la sequenza di attività.  

    - **Descrizione**: specificare una descrizione (facoltativo).  

5. Nella pagina **Aggiorna il sistema operativo Windows** specificare le impostazioni seguenti:  

    - **Pacchetto di aggiornamento**: specificare il pacchetto di aggiornamento che contiene i file di origine per l'aggiornamento del sistema operativo. Verificare di avere selezionato il pacchetto di aggiornamento corretto esaminando le informazioni nel riquadro **Proprietà**. Per altre informazioni, vedere [Gestire i pacchetti di aggiornamento del sistema operativo](../get-started/manage-operating-system-upgrade-packages.md).  

    - **Indice dell'edizione**: se nel pacchetto sono disponibili più indici dell'edizione del sistema operativo, selezionare l'indice dell'edizione desiderato. Per impostazione predefinita, la procedura guidata seleziona il primo indice.  

    - **Codice Product Key**: specificare il codice Product Key Windows per il sistema operativo da installare. Specificare i codici Product Key per contratti multilicenza codificati o i codici Product Key standard. Se si usa un codice Product Key standard, separare ogni gruppo di cinque caratteri con un trattino (`-`). Ad esempio: `XXXXX-XXXXX-XXXXX-XXXXX-XXXXX`. Se l'aggiornamento è per un'edizione per contratti multilicenza, il codice Product Key potrebbe non essere obbligatorio.  

        > [!Note]  
        > Questo codice Product Key può essere un codice ad attivazione multipla (MAK) o un codice generico di contratti multilicenza (GVLK). Un codice GVLK è anche definito codice di configurazione client del servizio di gestione delle chiavi (KMS). Per altre informazioni, vedere [Pianificare l'attivazione dei contratti multilicenza](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client). Per un elenco di codici di configurazione client KMS, vedere l'[Appendice A](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys) della Guida di attivazione di Windows Server.

    - **Ignora tutti i messaggi sulla compatibilità non rilevanti**: selezionare questa impostazione se si esegue l'aggiornamento a Windows Server 2016. Se non si seleziona questa impostazione, la sequenza di attività non può essere completata perché il programma di installazione di Windows rimane in attesa che l'utente selezioni **Conferma** in una finestra di dialogo di compatibilità delle app di Windows.  

6. Nella pagina **Includi aggiornamenti** specificare se installare gli aggiornamenti software obbligatori, tutti gli aggiornamenti software o nessuno. Selezionare quindi **Avanti**. Se si sceglie di installare gli aggiornamenti software, Configuration Manager installa solo gli aggiornamenti assegnati alle raccolte di cui il computer di destinazione è membro.  

7. Nella pagina **Installa applicazioni** specificare le applicazioni da installare nel computer di destinazione e quindi selezionare **Avanti**. Se si seleziona più di un'applicazione, specificare anche se la sequenza di attività deve continuare se l'installazione di un'applicazione specifica non riesce.  

8. Completare la procedura guidata.  

> [!Important]  
> Quando la sequenza di attività viene eseguita in un dispositivo, il client di Configuration Manager crea diversi script per controllare il comportamento della sequenza di attività nei vari scenari. Al termine dell'esecuzione della sequenza di attività, il client non rimuove questi script fino a quando il computer non viene riavviato. Questi file di script non contengono informazioni riservate.  

Il modello di sequenza di attività predefinita per l'aggiornamento sul posto di Windows 10 include gruppi aggiuntivi con azioni consigliate da aggiungere prima e dopo il processo di aggiornamento. Queste azioni sono comuni tra numerosi clienti che stanno aggiornando i propri dispositivi a Windows 10. Per altre informazioni, vedere i passaggi della sequenza di attività consigliata [per preparare l'aggiornamento](#recommended-task-sequence-steps-to-prepare-for-upgrade) e [ post-elaborazione](#recommended-task-sequence-steps-for-post-processing).

A partire dalla versione 1806, questo modello di sequenza di attività include anche un gruppo con azioni consigliate da aggiungere in caso di esito negativo del processo di aggiornamento. Queste azioni facilitano la risoluzione dei problemi. Per altre informazioni, vedere [Passaggi della sequenza di attività consigliati in caso di errore](#recommended-task-sequence-steps-on-failure).<!--1358500-->  


## <a name="configure-pre-cache-content"></a>Configurare la pre-cache del contenuto

<!--1021244-->
La funzionalità pre-cache per le distribuzioni di sequenze di attività disponibili consente ai client di scaricare il contenuto pertinente dei pacchetti di aggiornamento del sistema operativo prima che un utente installi la sequenza di attività.  

Per altre informazioni, vedere [Configurare la pre-cache del contenuto](configure-precache-content.md).


## <a name="recommended-task-sequence-steps-to-prepare-for-upgrade"></a>Passaggi della sequenza di attività consigliati per la preparazione dell'aggiornamento

Il modello di sequenza di attività predefinita per l'aggiornamento sul posto di Windows 10 include gruppi aggiuntivi con azioni consigliate da aggiungere prima del processo di aggiornamento. Queste azioni nel gruppo **Preparazione dell'aggiornamento** sono comuni tra numerosi clienti che stanno aggiornando i propri dispositivi a Windows 10. Se in una sequenza di attività queste azioni non sono già presenti, aggiungerle manualmente ad essa nel gruppo **Preparazione dell'aggiornamento**.  

### <a name="battery-checks"></a>Verifiche della batteria

consente di aggiungere passaggi in questo gruppo per verificare se il computer usa la batteria o l'alimentazione tramite cavo. Per eseguire questo controllo serve un'utilità o uno script personalizzato.

#### <a name="battery-check-example"></a>Esempio: controllo della batteria

Usando WbemTest, connettersi allo spazio dei nomi `root\cimv2`. Eseguire quindi la query seguente:

`Select BatteryStatus From Win32_Battery where BatteryStatus != 2`

Se restituisce un risultato, il dispositivo è alimentato a batteria. In caso contrario, il dispositivo usa l'alimentazione tramite cavo.  

### <a name="networkwired-connection-checks"></a>Verifiche della connessione di rete/via cavo

consente di aggiungere passaggi in questo gruppo per verificare se il computer è connesso a una rete e non usa una connessione wireless. Per eseguire questo controllo serve un'utilità o uno script personalizzato.

#### <a name="network-check-example"></a>Esempio: controllo della rete

Usando WbemTest, connettersi allo spazio dei nomi `root\cimv2`. Eseguire quindi la query seguente:

`Select * From Win32_NetworkAdapter Where NetConnectionStatus = 2 and PhysicalAdapter = 'True' and NetConnectionID = 'Wi-Fi'`

Se restituisce un risultato, il dispositivo è connesso al Wi-Fi. In caso contrario, il dispositivo usa una connessione di rete cablata.

### <a name="remove-incompatible-applications"></a>Rimuovi le applicazioni non compatibili

consente di aggiungere passaggi in questo gruppo per rimuovere eventuali applicazioni non compatibili con questa versione di Windows 10. Il metodo per disinstallare un'applicazione varia a seconda dei casi.  

Se l'applicazione usa Windows Installer, copiare la riga di comando **Disinstalla programma** dalla scheda **Programmi** nelle proprietà del tipo di distribuzione di Windows Installer dell'applicazione. Quindi aggiungere un passaggio **Esegui riga di comando** in questo gruppo con la riga di comando Disinstalla programma. Ad esempio:

`msiexec /x {150031D8-1234-4BA8-9F52-D6E5190D1CBA} /q`  

### <a name="remove-incompatible-drivers"></a>Rimuovi i driver non compatibili

consente di aggiungere passaggi in questo gruppo per rimuovere eventuali driver non compatibili con questa versione di Windows 10.  

### <a name="removesuspend-third-party-security"></a>Rimuovi/Sospendi la sicurezza di terze parti

consente di aggiungere passaggi in questo gruppo per rimuovere o sospendere programmi di sicurezza di terze parti, ad esempio l'antivirus.  

Se si usa un programma di crittografia dischi di terze parti, specificare il relativo driver di crittografia al programma di installazione di Windows con `/ReflectDrivers`, [opzione della riga di comando](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#reflectdrivers). Aggiungere un passaggio [Imposta variabile della sequenza di attività](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) alla sequenza di attività in questo gruppo. Impostare la variabile della sequenza di attività su **OSDSetupAdditionalUpgradeOptions**. Impostare il valore su `/ReflectDrivers` con il percorso del driver. Questa [variabile della sequenza di attività](../understand/task-sequence-variables.md#OSDSetupAdditionalUpgradeOptions) accoda la riga di comando di Installazione di Windows usata dalla sequenza di attività. Per ulteriori indicazioni su questo processo, contattare il fornitore del software in uso.  

### <a name="download-package-content-task-sequence-step"></a>Passaggio della sequenza di attività Scaricare il contenuto del pacchetto  

Usare il passaggio [Scaricare il contenuto del pacchetto](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent) prima del passaggio **Aggiorna sistema operativo** negli scenari seguenti:  

- Si usa una singola sequenza di attività di aggiornamento per le piattaforme x86 e x64. Includere due passaggi **Scarica contenuto pacchetto** nel gruppo **Preparazione dell'aggiornamento**. Impostare le condizioni in ogni passaggio per rilevare l'architettura client. Questa condizione fa in modo che il passaggio scarichi solo il pacchetto di aggiornamento del sistema operativo appropriato. Configurare ogni passaggio **Scarica contenuto pacchetto** in modo da usare la stessa variabile e usare la variabile per il percorso del supporto durante il passaggio **Aggiorna sistema operativo** .  

- Per scaricare in modo dinamico un pacchetto di driver applicabile, usare due passaggi **Scarica contenuto pacchetto** con le condizioni per rilevare il tipo di hardware appropriato per ogni pacchetto driver. Configurare ogni passaggio **Scarica contenuto pacchetto** in modo che usi la stessa variabile. Quindi usare tale variabile per il valore **Contenuto preconfigurato** nella sezione dei driver del passaggio **Aggiorna sistema operativo**.  

    > [!NOTE]  
    > Configuration Manager aggiunge un suffisso numerico al nome di questa variabile. Ad esempio, se si specifica `%mycontent%` come variabile personalizzata, il client archivia tutto il contenuto a cui si fa riferimento in questo percorso. Quando si fa riferimento alla variabile in un passaggio successivo, ad esempio **Aggiorna sistema operativo**, usare la variabile con un suffisso numerico. In questo esempio, `%mycontent01%` o `%mycontent02%`, dove il numero corrisponde all'ordine in cui il passaggio **Scarica contenuto pacchetto** indica il contenuto specifico.  


## <a name="recommended-task-sequence-steps-for-post-processing"></a>Passaggi della sequenza di attività consigliati per la post-elaborazione

Dopo aver creato la sequenza di attività, aggiungere questi passaggi nel gruppo **Post-elaborazione** della sequenza di attività stessa.  

> [!NOTE]  
> Questa sequenza di attività non è lineare. I passaggi sono soggetti a condizioni che possono influire sui risultati della sequenza di attività. Questo comportamento varia a seconda che l'aggiornamento del sistema operativo del computer client venga completato o che venga eseguito il rollback del computer client al sistema operativo originale.  

Il modello di sequenza di attività predefinita per l'aggiornamento sul posto di Windows 10 include gruppi aggiuntivi con azioni consigliate da aggiungere dopo il processo di aggiornamento. Queste azioni nel gruppo **Post-elaborazione** sono comuni tra numerosi clienti che stanno aggiornando i propri dispositivi a Windows 10. Se in una sequenza di attività queste azioni non sono già presenti, aggiungerle manualmente ad essa nel gruppo **Post-elaborazione**.  

### <a name="apply-setup-based-drivers"></a>Applica driver basati su installazione

consente di aggiungere passaggi in questo gruppo per installare driver basati su installazione (EXE) dai pacchetti.  

### <a name="installenable-third-party-security"></a>Installa/Abilita la sicurezza di terze parti

consente di aggiungere passaggi in questo gruppo per installare o abilitare i programmi di sicurezza di terze parti, ad esempio l'antivirus.  

### <a name="set-windows-default-apps-and-associations"></a>Imposta le app predefinite e le associazioni di Windows

consente di aggiungere passaggi in questo gruppo per impostare le app predefinite e le associazioni di file di Windows.

1. Preparare un computer di riferimento con le associazioni di app desiderate.
1. Eseguire la riga di comando seguente per esportare:  
    `dism /online /Export-DefaultAppAssociations:"%UserProfile%\Desktop\DefaultAppAssociations.xml"`  
1. Aggiungere il file XML a un pacchetto.
1. Aggiungere un passaggio [Esegui riga di comando](../understand/task-sequence-steps.md#BKMK_RunCommandLine) nel gruppo. Specificare il pacchetto che contiene il file XML, quindi specificare la riga di comando seguente:  
    `dism /online /Import-DefaultAppAssociations:DefaultAppAssociations.xml`  

Per altre informazioni, vedere [Export or import default application associations](/windows-hardware/manufacture/desktop/export-or-import-default-application-associations) (Esportare o importare associazioni di applicazioni predefinite).

### <a name="apply-customizations-and-personalization"></a>Applica personalizzazioni

consente di aggiungere passaggi in questo gruppo per applicare le personalizzazioni del menu Start, ad esempio l'organizzazione di gruppi di programmi. Per altre informazioni, vedere [Customize the Start screen](/windows-hardware/manufacture/desktop/customize-the-start-screen) (Personalizzare la schermata iniziale).  


## <a name="optional-task-sequence-steps-for-rollback"></a>Passaggi facoltativi della sequenza di attività per il rollback  

Quando si verificano problemi nel processo di aggiornamento dopo il riavvio del computer, l'installazione di Windows esegue il rollback del sistema ripristinando il sistema operativo precedente. La sequenza di attività continua quindi con i passaggi del gruppo **Rollback**. Dopo aver creato la sequenza di attività, aggiungere i passaggi facoltativi in questo gruppo, se necessario. È ad esempio possibile annullare eventuali modifiche apportate al sistema nel gruppo Preparazione dell'aggiornamento, ad esempio la disinstallazione di software non compatibile.


## <a name="recommended-task-sequence-steps-on-failure"></a>Passaggi della sequenza di attività consigliati in caso di errore

<!--1358500-->
A partire dalla versione 1806, il modello di sequenza di attività predefinito per l'aggiornamento sul posto di Windows 10 include un gruppo per **eseguire le azioni in caso di errore**. Questo gruppo include le azioni consigliate da aggiungere nel caso in cui il processo di aggiornamento ha esito negativo. Queste azioni facilitano la risoluzione dei problemi.

### <a name="collect-logs"></a>Raccogli registri

per raccogliere i log dal client, aggiungere passaggi in questo gruppo.  

- Una pratica comune prevede la copia dei file di log in una condivisione di rete. Per stabilire questa connessione, usare il passaggio [Connetti alla cartella di rete](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder).  

- Per eseguire l'operazione di copia, usare un'utilità o uno script personalizzato con il passaggio [Esegui riga di comando](../understand/task-sequence-steps.md#BKMK_RunCommandLine) oppure [Esegui script PowerShell](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript).  

- I file da raccogliere potrebbero includere i log seguenti:  
     `%_SMSTSLogPath%\*.log`  
     `%SystemDrive%\$Windows.~BT\Sources\Panther\setupact.log`  

- Per altre informazioni su setupact.log e altri log di Installazione di Windows, vedere [Windows Setup Log files](https://docs.microsoft.com/windows/deployment/upgrade/log-files) (File di log di Installazione di Windows).  

- Per altre informazioni sui log client di Configuration Manager, vedere [Log client di Configuration Manager](../../core/plan-design/hierarchy/log-files.md#BKMK_ClientLogs).  

- Per altre informazioni su **_SMSTSLogPath** e altre variabili utili, vedere [Variabili della sequenza di attività](../understand/task-sequence-variables.md).  

### <a name="run-diagnostic-tools"></a>Esegui gli strumenti di diagnostica

per eseguire strumenti di diagnostica aggiuntivi, aggiungere passaggi in questo gruppo. Automatizzare questi strumenti per la raccolta di informazioni aggiuntive dal sistema subito dopo l'errore.  

Uno di questi strumenti è [SetupDiag](https://docs.microsoft.com/windows/deployment/upgrade/setupdiag) di Windows. È uno strumento di diagnostica autonomo per ottenere i dettagli sui motivi per cui un aggiornamento a Windows 10 non è riuscito.  

- In Configuration Manager [creare un pacchetto](../../apps/deploy-use/packages-and-programs.md#create-a-package-and-program) per lo strumento.  

- Aggiungere un passaggio [Esegui riga di comando](../understand/task-sequence-steps.md#BKMK_RunCommandLine) a questo gruppo della sequenza di attività. Usare l'opzione **Pacchetto** per fare riferimento allo strumento. La stringa seguente è un esempio di **Riga di comando**:  
    `SetupDiag.exe /Output:"%_SMSTSLogPath%\SetupDiagResults.log"`  

> [!TIP]
> Usare sempre la versione più recente di SetupDiag per avere a disposizione le funzionalità più recenti e le correzioni ai problemi noti. Per altre informazioni, vedere [SetupDiag](https://docs.microsoft.com/windows/deployment/upgrade/setupdiag).

## <a name="additional-recommendations"></a>Suggerimenti aggiuntivi

### <a name="windows-documentation"></a>Documentazione di Windows

Vedere l'articolo [Risolvere gli errori di aggiornamento di Windows 10](https://docs.microsoft.com/windows/deployment/upgrade/resolve-windows-10-upgrade-errors) nella documentazione di Windows. Questo articolo include anche informazioni dettagliate sul processo di aggiornamento.  

### <a name="check-minimum-disk-space"></a>Controllare lo spazio minimo su disco

Nel passaggio predefinito **Verifica conformità** abilitare **Verifica lo spazio minimo disponibile su disco (MB)** . Impostare il valore su almeno **16384** (16 GB) per un pacchetto di aggiornamento del sistema operativo a 32 bit o su **20480** (20 GB) per un pacchetto a 64 bit.  

### <a name="retry-downloading-policy"></a>Tentativi di download dei criteri

Usare la **variabile della sequenza di attività** [SMSTSDownloadRetryCount](../understand/task-sequence-variables.md#SMSTSDownloadRetryCount) per riprovare a scaricare i criteri. Per impostazione predefinita, attualmente il client esegue due tentativi; questa variabile è impostata su due (2). Se i client non sono su una connessione di rete Intranet cablata, ulteriori tentativi possono aiutare a ottenere i criteri per tali client. L'uso di questa variabile non ha effetti collaterali negativi, se non un errore ritardato nel caso in cui il download dei criteri non riesca.<!--501016--> Aumentare inoltre il valore della variabile **SMSTSDownloadRetryDelay** dai 15 secondi predefiniti.  

### <a name="perform-an-inline-compatibility-assessment"></a>Eseguire una valutazione della compatibilità inline

1. Aggiungere un secondo passaggio **Aggiorna sistema operativo** nel gruppo **Preparazione dell'aggiornamento**.  

    1. Assegnargli in nome *Valutazione aggiornamento*.
    1. Specificare lo stesso pacchetto di aggiornamento e quindi abilitare l'opzione **Esegui analisi compatibilità Installazione di Windows senza avviare l’aggiornamento**.
    1. Abilitare **Continua in caso di errore** nella scheda Opzioni.  

1. Subito dopo questo passaggio *Valutazione aggiornamento* aggiungere un passaggio **Esegui riga di comando**. Specificare la riga di comando seguente:

    `cmd /c exit %_SMSTSOSUpgradeActionReturnCode%`

1. Nella scheda **Opzioni** aggiungere la condizione seguente:

    `Task Sequence Variable _SMSTSOSUpgradeActionReturnCode not equals 3247440400`

Questo codice restituito è l'equivalente in formato decimale di MOSETUP_E_COMPAT_SCANONLY (0xC1900210), che indica una valutazione della compatibilità riuscita senza problemi. Se il passaggio *Valutazione aggiornamento* riesce e restituisce questo codice, la sequenza di attività ignora questo passaggio. Se invece il passaggio di valutazione restituisce qualsiasi altro codice, questo passaggio esegue con errori la sequenza di attività con il codice restituito dall'analisi di compatibilità di Installazione di Windows. Per altre informazioni su **_SMSTSOSUpgradeActionReturnCode**, vedere [Variabili della sequenza di attività](../understand/task-sequence-variables.md#SMSTSOSUpgradeActionReturnCode).

Per altre informazioni, vedere [Aggiorna sistema operativo](../understand/task-sequence-steps.md#BKMK_UpgradeOS).  

### <a name="convert-from-bios-to-uefi"></a>Eseguire la conversione da BIOS a UEFI

Se si vuole modificare il dispositivo da BIOS a UEFI durante questa sequenza di attività, vedere [Conversione da BIOS a UEFI durante un aggiornamento sul posto](task-sequence-steps-to-manage-bios-to-uefi-conversion.md#bkmk_ipu).  

### <a name="manage-bitlocker"></a>Gestire BitLocker

<!--SCCMDocs issue #494-->
Se si usa la crittografia dischi BitLocker, per impostazione predefinita il programma di installazione di Windows la sospenderà automaticamente durante l'aggiornamento. A partire da Windows 10 versione 1803, il programma di installazione di Windows include il parametro della riga di comando `/BitLocker` per controllare questo comportamento. Se i requisiti di sicurezza richiedono di mantenere sempre attiva la crittografia dischi, usare la **variabile della sequenza di attività** [OSDSetupAdditionalUpgradeOptions](../understand/task-sequence-variables.md#OSDSetupAdditionalUpgradeOptions) nel gruppo **Preparazione dell'aggiornamento** per includere `/BitLocker TryKeepActive`. Per altre informazioni, vedere [Opzioni della riga di comando di Installazione di Windows](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#bitlocker).

### <a name="remove-default-apps"></a>Rimuovere le app predefinite

<!--SCCMDocs issue #526-->
Alcuni clienti rimuovono le app predefinite di cui è stato effettuato il provisioning in Windows 10. Ad esempio, l'app Bing Meteo o Microsoft Solitaire Collection. In alcune situazioni, queste app ritornano dopo l'aggiornamento di Windows 10. Per altre informazioni, vedere l'articolo su [come mantenere le app rimosse da Windows 10](https://docs.microsoft.com/windows/application-management/remove-provisioned-apps-during-update).

Aggiungere il passaggio **Esegui riga di comando** alla sequenza di attività nel gruppo **Preparazione dell'aggiornamento**. Specificare una riga di comando simile a quella dell'esempio seguente:

`cmd /c reg add "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Appx\AppxAllUserStore\Deprovisioned\Microsoft.BingWeather_8wekyb3d8bbwe" /f`
