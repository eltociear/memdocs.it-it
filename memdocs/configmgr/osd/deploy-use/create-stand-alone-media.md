---
title: Creare supporti autonomi
titleSuffix: Configuration Manager
description: Usare supporti autonomi per distribuire il sistema operativo in un computer senza connessione di rete.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: c6b9ccd2-78d9-4f0e-b25a-70d0866300ba
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8ff3e0ee8f002a21e283b8a56f55d0daa2490253
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/09/2020
ms.locfileid: "89606362"
---
# <a name="create-stand-alone-media"></a>Creare supporti autonomi

*Si applica a: Configuration Manager (Current Branch)*

Il supporto autonomo in Configuration Manager contiene tutto il necessario per distribuire il sistema operativo in un computer senza connessione di rete.

Usare il supporto autonomo con gli scenari di distribuzione del sistema operativo seguenti:  

- [Aggiornare un computer esistente con una nuova versione di Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

- [Installare una nuova versione di Windows in un nuovo computer (bare metal)](install-new-windows-version-new-computer-bare-metal.md)  

- [Aggiornare Windows alla versione più recente](upgrade-windows-to-the-latest-version.md)  


## <a name="usage"></a>Utilizzo

I supporti autonomi includono la sequenza di attività che automatizza i passaggi per installare il sistema operativo e tutti gli altri contenuti necessari. Questi contenuti includono l'immagine d'avvio, l'immagine del sistema operativo e i driver di dispositivo. Poiché i supporti autonomi archiviano tutto il necessario per la distribuzione del sistema operativo, lo spazio su disco richiesto è superiore a quello richiesto per altri tipi di supporti.

Quando si creano supporti autonomi in un sito di amministrazione centrale, il client recupera il relativo codice del sito assegnato da Active Directory. I supporti autonomi creati nei siti figlio assegnano automaticamente al client il codice del sito per tale sito.  


## <a name="prerequisites"></a>Prerequisiti

Prima di creare supporti autonomi usando la Creazione guidata del supporto per la sequenza di attività, assicurarsi che tutte queste condizioni siano soddisfatte.

### <a name="create-a-task-sequence-to-deploy-an-os"></a>Creare una sequenza di attività per distribuire un sistema operativo

Nell'ambito del supporto autonomo, specificare la sequenza di attività per la distribuzione di un sistema operativo. Per altre informazioni, vedere [Creare una sequenza di attività per installare un sistema operativo](create-a-task-sequence-to-install-an-operating-system.md).

#### <a name="unsupported-actions-for-stand-alone-media"></a>Azioni non supportate per i supporti autonomi

Per i supporti autonomi non sono supportate le azioni seguenti:

- Passaggio [Applica automaticamente i driver](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers) nella sequenza di attività. I supporti autonomi non supportano l'applicazione automatica di driver di dispositivo dal catalogo di driver. Usare il passaggio [Applica pacchetto di driver](../understand/task-sequence-steps.md#BKMK_ApplyDriverPackage) per rendere disponibile per Installazione di Windows un set specificato di driver.  

- Passaggio [Scarica contenuto pacchetto](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent) nella sequenza di attività. Le informazioni relative ai punti di gestione non sono disponibili nei supporti autonomi, quindi il tentativo di enumerazione dei percorsi del contenuto non riesce.  

- Istallazione di aggiornamenti software.  

- Installazione del software prima della distribuzione del sistema operativo.  

- Sequenze di attività personalizzate per distribuzioni non di sistema operativo.  

- Associazione di utenti al computer di destinazione per il supporto dell'affinità utente dispositivo.  

- Installazione dinamica dei pacchetti tramite il passaggio [Installa pacchetto](../understand/task-sequence-steps.md#BKMK_InstallPackage).  

- Installazione dinamica delle applicazioni tramite il passaggio [Installa applicazione](../understand/task-sequence-steps.md#BKMK_InstallApplication).

- Impostazione **Usa il pacchetto client di pre-produzione se disponibile** nel passaggio della sequenza di attività **Imposta Windows e ConfigMgr**. Per altre informazioni su questa impostazione, vedere [Configurare Windows e ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr).  

> [!NOTE]  
> Può verificarsi un errore se la sequenza di attività include il passaggio [Installa pacchetto](../understand/task-sequence-steps.md#BKMK_InstallPackage) e si crea il supporto autonomo in un sito di amministrazione centrale. Il sito di amministrazione centrale non ha i criteri di configurazione client necessari. Questi criteri sono necessari per abilitare l'agente di distribuzione software durante l'esecuzione della sequenza di attività. Nel file **CreateTsMedia.log** può essere visualizzato l'errore seguente:  
>
> `WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)`
>
> Per i supporti autonomi che includono un passaggio **Installa pacchetto**, creare il supporto autonomo in un sito primario nel quale è abilitato l'agente di distribuzione software.
>
> In alternativa, usare un passaggio [Esegui riga di comando](../understand/task-sequence-steps.md#BKMK_RunCommandLine) personalizzato. Aggiungerlo dopo il passaggio [Imposta Windows e ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) e prima del primo passaggio **Installa pacchetto**. Il passaggio **Esegui riga di comando** esegue il comando WMIC seguente per abilitare l'agente di distribuzione software prima del primo passaggio Installa pacchetto:  
>
> `WMIC /namespace:\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE`

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Distribuire tutto il contenuto associato alla sequenza di attività

Distribuire tutto il contenuto richiesto dalla sequenza di attività in almeno un punto di distribuzione. Tale contenuto include l'immagine d'avvio, l'immagine del sistema operativo e altri file associati. La procedura guidata raccoglie il contenuto dal punto di distribuzione quando crea il supporto.

L'account utente usato deve avere almeno diritti di accesso in **lettura** per la raccolta contenuto nel punto di distribuzione. Per altre informazioni, vedere [Distribuire il contenuto](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

### <a name="prepare-the-removable-usb-drive"></a>Preparare l'unità USB rimovibile

Se si usa un'unità USB rimovibile, connetterla al computer in cui si esegue la Creazione guidata del supporto per la sequenza di attività. L'unità USB deve essere rilevabile da Windows come dispositivo rimovibile. La procedura guidata scrive direttamente nell'unità USB durante la creazione del supporto.

Supporto autonomo usa un file system FAT32. Non è possibile creare supporti autonomi in un'unità USB rimovibile il cui contenuto includa un file di oltre 4 GB.

### <a name="create-an-output-folder"></a>Creare una cartella di output

Prima di eseguire la Creazione guidata del supporto per la sequenza di attività per creare il supporto per un set di CD o DVD, creare una cartella per i file di output creati dalla procedura guidata. Il supporto creato per un set di CD o DVD viene scritto come file con estensione iso direttamente nella cartella.


## <a name="process"></a>Processo

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**, espandere **Sistemi operativi** e selezionare il nodo **Sequenze di attività**.  

2. Nella scheda **Home** della barra multifunzione nel gruppo **Crea** selezionare **Crea supporto per sequenza attività**. Questa azione avvia la Creazione guidata del supporto per la sequenza di attività.  

3. Nella pagina **Seleziona tipo di supporto** specificare le opzioni seguenti:  

    - Selezionare **Supporto autonomo**.  

    - Se si vuole solo consentire la distribuzione del sistema operativo senza richiedere input da parte dell'utente, è possibile selezionare **Consenti distribuzione automatica del sistema operativo**.  

        > [!IMPORTANT]  
        > Quando si seleziona questa opzione, all'utente non vengono richieste informazioni sulla configurazione di rete o su sequenze di attività facoltative. Se tuttavia si configura il supporto per la protezione con password, all'utente viene richiesta una password.  

4. Nella pagina **Tipo di supporto** specificare se il supporto è **un'unità USB rimovibile** o un **set di CD/DVD**. Configurare quindi le opzioni seguenti:  

    > [!IMPORTANT]  
    > Il supporto usa il file system FAT32. Non è possibile creare supporti in un'unità USB il cui contenuto include un file di oltre 4 GB.  

    - Se si seleziona **Unità USB rimovibile**, è necessario selezionare l'unità in cui archiviare il contenuto.  

        - **Formatta unità USB rimovibile (FAT32) e consenti l'avvio**: per impostazione predefinita, consente a Configuration Manager di preparare l’unità USB. Molti dispositivi UEFI più recenti richiedono una partizione FAT32 di avvio. Questo formato tuttavia limita anche le dimensioni dei file e la capacità complessiva dell'unità. Se l'unità rimovibile è già stata formattata e configurata, disabilitare questa opzione.

    - Se si seleziona l'opzione **CD/DVD impostato**, specificare la capacità del supporto (**Dimensione supporto**) e il nome e il percorso dei file di output (**File supporto**). La procedura guidata scrive i file di output in questa posizione. ad esempio `\\servername\folder\outputfile.iso`  

        Se la capacità del supporto non è sufficiente per archiviare l'intero contenuto, vengono creati più file. È quindi necessario archiviare il contenuto in più CD o DVD. Quando sono necessari più supporti, Configuration Manager aggiunge un numero di sequenza al nome di ogni file di output creato.  

        Se insieme al sistema operativo si distribuisce un'applicazione e questa non può essere contenuta in un unico supporto, Configuration Manager archivia l'applicazione in più supporti. Quando il supporto autonomo viene eseguito Configuration Manager chiede all'utente il supporto successivo contenente l'applicazione.  

        > [!IMPORTANT]  
        > Se si seleziona un'immagine iso esistente, la Creazione guidata del supporto per la sequenza di attività elimina l'immagine dall'unità o dalla condivisione non appena si passa alla pagina successiva della procedura guidata. L'immagine esistente viene eliminata, anche se si annulla la procedura guidata.  

    - **Cartella di gestione temporanea**<!--1359388-->: il processo di creazione del supporto può richiedere molto spazio temporaneo sul disco. Per impostazione predefinita questo percorso è simile al seguente: `%UserProfile%\AppData\Local\Temp`. A partire dalla versione 1902, per offrire maggiore flessibilità dal punto di vista del percorso di archiviazione dei file temporanei, modificare questo valore con un'altra unità e un altro percorso.  

    - **Etichetta supporto**<!--1359388-->: a partire dalla versione 1902, è possibile aggiungere un'etichetta al supporto della sequenza di attività. Questa etichetta consente di identificare più facilmente il supporto creato. Il valore predefinito è `Configuration Manager`. Questo campo di testo viene visualizzato nelle posizioni seguenti:  

        - Se si monta un file ISO, Windows visualizza questa etichetta come nome dell'unità montata  

        - Se si formatta un'unità USB, vengono utilizzati i primi 11 caratteri dell'etichetta come nome  

        - Configuration Manager scrive un file di testo denominato `MediaLabel.txt` nella radice del supporto. Per impostazione predefinita, il file include un'unica riga di testo: `label=Configuration Manager`. Se si personalizza l'etichetta del supporto, verrà utilizzata l'etichetta personalizzata anziché il valore predefinito.  

    - **Includi il file autorun.inf sul supporto**<!-- 4090666 -->: a partire dalla versione 1906, Configuration Manager non aggiunge il file autorun.inf per impostazione predefinita. Questo file è generalmente bloccato da prodotti antimalware. Per altre informazioni sulla funzionalità di esecuzione automatica di Windows, vedere [Creating an AutoRun-enabled CD-ROM Application](/windows/desktop/shell/autoplay) (Creazione di un'applicazione CD-ROM abilitata per l'esecuzione automatica). Se il file è ancora richiesto dallo scenario, selezionare questa opzione per includerlo.  

5. Nella pagina **Sicurezza** specificare le opzioni seguenti:

    - **Proteggi supporto con password**: immettere una password complessa per proteggere il supporto dall'accesso non autorizzato. Quando si specifica una password, l'utente deve immetterla per usare il supporto.  

        > [!IMPORTANT]  
        > Come procedura consigliata di sicurezza, assegnare sempre una password per proteggere il supporto.  
        >
        > In un supporto autonomo vengono crittografati solo i passaggi delle sequenze di attività e le relative variabili. Il contenuto rimanente del supporto non viene crittografato. Non includere informazioni riservate negli script di sequenza di attività. Archiviare e implementare tutte le informazioni riservate usando variabili della sequenza di attività.  

    - **Seleziona l'intervallo di date di validità per il supporto autonomo**: impostare le date di inizio e di scadenza facoltative per il supporto. Per impostazione predefinita, questa impostazione è disabilitata. Le date vengono confrontate con l'ora di sistema nel computer prima che il supporto autonomo venga eseguito. Quando l'ora di sistema è precedente all'ora di inizio o successiva all'ora di scadenza, il supporto autonomo non si avvia. Queste opzioni sono disponibili anche tramite il cmdlet PowerShell [New-CMStandaloneMedia](/powershell/module/configurationmanager/new-cmstandalonemedia).  

6. Nella pagina **CD/DVD autonomo** selezionare la sequenza di attività per la distribuzione del sistema operativo. È possibile selezionare solo le sequenze di attività associate a un'immagine d'avvio. Verificare l'elenco di contenuti a cui si fa riferimento nella sequenza di attività.  

    - **Rileva le dipendenze dell'applicazione associata e aggiungile a questo contenuto multimediale**: aggiungere anche contenuto al supporto per le dipendenze dell'applicazione.  

        > [!TIP]  
        > Se le dipendenze dell'applicazione previste non vengono visualizzate, deselezionare e selezionare nuovamente questa opzione per aggiornare l'elenco.  

7. Nella pagina **Selezione applicazione** specificare contenuto aggiuntivo per l'applicazione, da includere come parte del file del supporto.  

8. Nella pagina **Selezione pacchetto** specificare contenuto aggiuntivo per il pacchetto, da includere come parte del file del supporto.  

9. Nella pagina **Selezionare il pacchetto driver** specificare contenuto aggiuntivo per il pacchetto driver, da includere come parte del file del supporto.  

10. Nella pagina **Punti di distribuzione** specificare i punti di distribuzione che includono il contenuto richiesto.  

    Configuration Manager visualizza solo i punti di distribuzione che includono il contenuto. Per continuare, distribuire tutto il contenuto associato alla sequenza di attività in almeno un punto di distribuzione. Dopo avere distribuito il contenuto, aggiornare l'elenco di punti di distribuzione. Rimuovere i punti di distribuzione già selezionati in questa pagina, andare alla pagina precedente e quindi di nuovo alla pagina **Punti di distribuzione**. In alternativa, riavviare la procedura guidata. Per altre informazioni, vedere [Distribuire il contenuto a cui fa riferimento una sequenza di attività](manage-task-sequences-to-automate-tasks.md#BKMK_DistributeTS) e [Gestire il contenuto e l'infrastruttura del contenuto](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

11. Nella pagina **Personalizzazione** specificare le opzioni seguenti:  

    - Aggiungere eventuali variabili usate dalla sequenza di attività.  

    - **Attiva comando di preavvio**: Specificare i comandi preavvio da eseguire prima dell'esecuzione della sequenza di attività. I comandi di preavvio sono costituiti da uno script o da un eseguibile che può interagire con l'utente in Windows PE prima che venga eseguita la sequenza di attività. Per altre informazioni vedere [Comandi di preavvio del supporto per sequenza attività](../understand/prestart-commands-for-task-sequence-media.md).  

        > [!TIP]  
        > Durante la creazione del supporto, tale sequenza scrive l'ID del pacchetto e la riga di comando di preavvio, incluso il valore per eventuali variabili della sequenza di attività, nel file **CreateTSMedia.log** nel computer che esegue la console di Configuration Manager. È possibile rivedere questo file di registro per verificare il valore per le variabili della sequenza di attività.  

        Se il comando di preavvio richiede contenuto, selezionare l'opzione **Includi file per il comando di preavvio**.  

12. Completare la procedura guidata.  

I file di supporto autonomo (con estensione ISO) vengono creati nella cartella di destinazione. Se è stata selezionata l'opzione **CD/DVD impostato**, copiare i file di output in un set di CD o DVD.


## <a name="next-steps"></a>Passaggi successivi

[Use stand-alone media to deploy Windows without using the network](use-stand-alone-media-to-deploy-windows-without-using-the-network.md) (Usare i supporti autonomi per distribuire Windows senza usare la rete)
