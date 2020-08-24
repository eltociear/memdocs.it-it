---
title: Installa aggiornamenti software
titleSuffix: Configuration Manager
description: Suggerimenti per l'uso del passaggio della sequenza di attività Installa aggiornamenti software in Configuration Manager.
ms.date: 05/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: troubleshooting
ms.assetid: 72d1ccd5-3763-4f88-9273-e1a73e8f4286
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 73acd43ef9d7924682de9df66487c5a04297e640
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697501"
---
# <a name="install-software-updates"></a>Installa aggiornamenti software

*Si applica a: Configuration Manager (Current Branch)*

Il passaggio **Installa aggiornamenti software** è usato comunemente nelle sequenze di attività di Configuration Manager. Durante l'installazione o l'aggiornamento del sistema operativo, esso attiva i componenti di aggiornamento software per la ricerca e la distribuzione degli aggiornamenti. Questo passaggio può causare problemi per alcuni clienti, ad esempio ritardi di timeout lunghi o la mancata installazione di aggiornamenti. Usare le informazioni in questo articolo per evitare i problemi comuni relativi a questo passaggio e per una migliore risoluzione dei problemi se si verificano problemi.

Per altre informazioni su questo passaggio, vedere [Installa aggiornamenti software](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)



## <a name="recommendations"></a>Indicazioni

Per fare in modo che questo processo abbia esito positivo, tenere conto dei consigli seguenti:

- [Usare l'installazione offline](#use-offline-servicing)
- [Indice singolo](#single-index)
- [Ridurre le dimensioni dell'immagine](#bkmk_resetbase)

### <a name="use-offline-servicing"></a>Usare l'installazione offline

Usare Configuration Manager per installare regolarmente gli aggiornamenti software applicabili ai file di immagine. Questa abitudine consente di ridurre il numero di aggiornamenti che devono essere installati durante la sequenza di attività.

Per altre informazioni, vedere [Applicare aggiornamenti software a un'immagine del sistema operativo](../get-started/manage-operating-system-images.md#BKMK_OSImagesApplyUpdates).

### <a name="single-index"></a>Indice singolo

Molti file di immagine includono più indici, ad esempio per diverse edizioni di Windows. Ridurre il file di immagine al singolo indice necessario. Ciò consente di ridurre la quantità di tempo richiesta per applicare gli aggiornamenti software all'immagine, oltre a contribuire al consiglio successivo di ridurre le dimensioni dell'immagine.

A partire dalla versione 1902, automatizzare questo processo quando si aggiunge un'immagine del sistema operativo al sito. Per altre informazioni, vedere [Aggiungere un'immagine del sistema operativo](../get-started/manage-operating-system-images.md#BKMK_AddOSImages).<!--3719699-->

### <a name="reduce-image-size"></a><a name="bkmk_resetbase"></a> Ridurre le dimensioni dell'immagine

Quando si applicano aggiornamenti software all'immagine, è possibile ottimizzare l'output rimuovendo tutti gli aggiornamenti sostituiti. Usare lo strumento da riga di comando Gestione e manutenzione immagini distribuzione, ad esempio:

``` Command
dism /Mount-Image /ImageFile:C:\Data\install.wim /MountDir:C:\Mountdir
dism /Image:C:\Mountdir /Cleanup-Image /StartComponentCleanup /ResetBase
dism /Unmount-Image /MountDir:C:\Mountdir /Commit  
```

A partire dalla versione 1902, è disponibile una nuova opzione per automatizzare questo processo. Per altre informazioni, vedere [Servizio immagini ottimizzato](../get-started/manage-operating-system-images.md#bkmk_resetbase).<!--3555951-->


## <a name="image-engineering-decisions"></a>Decisioni per la progettazione delle immagini

Quando si progetta il processo di creazione dell'immagine, esistono diverse opzioni che possono influire sull'installazione degli aggiornamenti software:

- [Riacquisire periodicamente l'immagine](#bkmk_goldimage)  
- [Usare l'installazione offline](#bkmk_offline)  
- [Usare solo l'immagine predefinita](#bkmk_installwim)

### <a name="periodically-recapture-the-image"></a><a name="bkmk_goldimage"></a> Riacquisire periodicamente l'immagine

È disponibile un processo automatizzato per acquisire un'immagine del sistema operativo personalizzata in base a una regolare pianificazione. Questa sequenza di attività di acquisizione installa gli aggiornamenti software più recenti. Questi aggiornamenti possono includere gli aggiornamenti cumulativi e non cumulativi, oltre ad altri aggiornamenti critici, ad esempio gli aggiornamenti dello stack di manutenzione. La sequenza di attività di distribuzione installa eventuali aggiornamenti aggiuntivi che diventano disponibili dopo l'acquisizione.

Per altre informazioni su questo processo, vedere [Creare una sequenza di attività per acquisire un sistema operativo](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md).

#### <a name="advantages"></a>Vantaggi

- Un minor numero di aggiornamenti da applicare al momento della distribuzione per ogni client, con conseguente risparmio di tempo e di larghezza di banda durante la distribuzione
- Un minor numero di aggiornamenti di cui preoccuparsi che causano riavvii
- Immagine personalizzata per l'organizzazione
- Meno variabili in fase di distribuzione

#### <a name="disadvantages"></a>Svantaggi

- Tempo necessario per creare e acquisire l'immagine, anche se il processo è per lo più automatizzato
- Maggior tempo per distribuire l'immagine ai punti di distribuzione, operazione che può essere considerata un'interruzione per le distribuzioni attive
- I tempi per testare gli ambienti di pre-produzione possono essere più lunghi rispetto al ciclo di applicazione delle patch al sistema operativo e ciò potrebbe rendere irrilevante l'immagine aggiornata


### <a name="use-offline-servicing"></a><a name="bkmk_offline"></a> Usare l'installazione offline

Pianificare Configuration Manager per applicare gli aggiornamenti software alle immagini.

Per altre informazioni, vedere [Applicare aggiornamenti software a un'immagine del sistema operativo](../get-started/manage-operating-system-images.md#BKMK_OSImagesApplyUpdates).

#### <a name="advantages"></a>Vantaggi

- Un minor numero di aggiornamenti da applicare al momento della distribuzione per ogni client, con conseguente risparmio di tempo e di larghezza di banda durante la distribuzione
- Un minor numero di aggiornamenti di cui preoccuparsi che causano riavvii
- È possibile pianificare il processo di manutenzione nel sito

#### <a name="disadvantages"></a>Svantaggi

- Selezione manuale degli aggiornamenti
- Maggiore tempo per distribuire l'immagine ai punti di distribuzione
- Supporta solo aggiornamenti basati su CBS. Non può applicare aggiornamenti di Microsoft 365 Apps

> [!Tip]  
> È possibile automatizzare la selezione degli aggiornamenti software tramite PowerShell. Usare il cmdlet [Get-CMSoftwareUpdate](/powershell/module/configurationmanager/get-cmsoftwareupdate?view=sccm-ps) per ottenere un elenco degli aggiornamenti. Usare quindi il cmdlet [New-CMOperatingSystemImageUpdateSchedule](/powershell/module/configurationmanager/new-cmoperatingsystemimageupdateschedule?view=sccm-ps) per creare la pianificazione delle installazioni offline. L'esempio seguente illustra un metodo per automatizzare questa azione:
>
> ```PowerShell
> # Get the OS image
> $Win10Image = Get-CMOperatingSystemImage -Name "Windows 10 Enterprise"
>
> # Get the latest cumulative update for Windows 10 1809
> $OSBuild = "1809"
> $LatestUpdate = Get-CMSoftwareUpdate -Fast | Where {$_.LocalizedDisplayName -Like "*Cumulative Update for Windows 10 Version $OSBuild for x64*" -and $_.LocalizedDisplayName -notlike "*Dynamic*"} | Sort-Object ArticleID -Descending | Select -First 1
> Write-Host "Latest update for Windows 10 build" $OSBuild "is" $LatestUpdate.LocalizedDisplayName
>
> # Create a new update schedule to apply the latest update
> New-CMOperatingSystemImageUpdateSchedule -Name $Win10Image.Name -SoftwareUpdate $LatestUpdate -RunNow -ContinueOnError $True
> ```


### <a name="use-default-image-only"></a><a name="bkmk_installwim"></a> Usare solo l'immagine predefinita

Usare il file di immagine install.wim di Windows predefinito nelle sequenze di attività di distribuzione.

#### <a name="advantages"></a>Vantaggi

- Un'origine valida nota, che riduce il rischio di danneggiamento delle immagini come possibile problema
- Elimina le modifiche dell'immagine come possibile problema

#### <a name="disadvantages"></a>Svantaggi

- Un volume di aggiornamenti potenzialmente elevato durante la distribuzione
- Maggiore tempo per la distribuzione per ogni dispositivo
- Potrebbero non essere incluse personalizzazioni necessarie e potrebbero essere necessari passaggi aggiuntivi della sequenza di attività per la personalizzazione



## <a name="flowchart"></a>Diagramma di flusso

Questo diagramma di flusso illustra il processo quando si include il passaggio Installa aggiornamenti software in una sequenza di attività.

[Visualizzare il diagramma per intero](media/ts-step-install-software-updates.svg)

![Diagramma di flusso per il passaggio della sequenza di attività Installa aggiornamenti software](media/ts-step-install-software-updates.svg)  

1. **Il processo inizia nel client**: una sequenza di attività in esecuzione in un client include il passaggio Installa aggiornamenti software.
2. **Compila e valuta criteri**: il client compila tutti i criteri di aggiornamento software nello spazio dei nomi WMI RequestedConfigs. (CIAgent.log)
3. *È la prima volta che viene chiamata questa istanza?*  
    1. **Sì**: passare a **Analisi completa**  
    2. **No**: *il passaggio è configurato con l'opzione [Valuta gli aggiornamenti software dai risultati di analisi memorizzati nella cache](task-sequence-steps.md#evaluate-software-updates-from-cached-scan-results)?*
        1. **Sì**: passare a **Analisi da risultati nella cache**
        2. **No**: passare a **Analisi completa**
4. Processo di analisi: analisi completa o analisi dai risultati memorizzati nella cache, con il processo di monitoraggio in parallelo.
    1. **Analisi completa**: il motore della sequenza di attività chiama l'agente di aggiornamento software tramite l'API di analisi degli aggiornamenti per eseguire un'analisi *completa*. (WUAHandler.log, ScanAgent.log)  
        1. **Analisi agente SUM - completa**: processo di analisi normale tramite l'agente di Windows Update (WUA), che comunica con il punto di aggiornamento software che esegue WSUS. Aggiunge tutti gli aggiornamenti applicabili all'archivio degli aggiornamenti locale. (WindowsUpdate.log, UpdateStore.log)
    2. **Analisi da risultati nella cache**: il motore della sequenza di attività chiama l'agente di aggiornamento software tramite l'API di analisi degli aggiornamenti per eseguire l'analisi in base ai metadati memorizzati nella cache. (WUAHandler.log, ScanAgent.log)
        1. **Analisi agente SUM - cache**: l'agente di Windows Update esegue un controllo in base agli aggiornamenti già memorizzati nella cache nell'archivio degli aggiornamenti locale. (WindowsUpdate.log, UpdateStore.log)
    3. **Avvia timer analisi**: il motore della sequenza di attività avvia un timer e resta in attesa. (Questo processo avviene in parallelo con il processo di analisi completa o di analisi dei risultati nella cache.)
        1. **Monitoraggio**: il motore della sequenza di attività esegue il monitoraggio dello stato dell'agente SUM.
        2. *Qual è la risposta dall'agente SUM?*
            - **In corso**: il timer ha raggiunto il valore nella variabile della sequenza di attività [SMSTSSoftwareUpdateScanTimeout](task-sequence-variables.md#SMSTSSoftwareUpdateScanTimeout)? (Valore predefinito 1 ora)
                - **Sì**: il passaggio non riesce.
                - **No**: passare a **Monitoraggio**
            - **Operazione non riuscita**: il passaggio non riesce.
            - **Completa**: passare a **Enumera elenco aggiornamenti**
5. **Enumera elenco aggiornamenti**: l'agente SUM enumera l'elenco degli aggiornamenti restituiti dall'analisi, stabilendo quali sono disponibili o obbligatori.
6. *Sono presenti aggiornamenti nell'elenco dei risultati dell'analisi?*
    - **Sì**: passare a **Installa aggiornamenti**
    - **No**: niente da installare, il passaggio viene completato correttamente.
7. Processo di distribuzione: il processo di installazione degli aggiornamenti avviene in parallelo con il processo di monitoraggio della distribuzione.
    1. **Installa aggiornamenti**: il motore della sequenza di attività chiama l'agente SUM tramite l'API di distribuzione degli aggiornamenti per installare tutti gli aggiornamenti disponibili o solo quelli obbligatori. Questo comportamento si basa sulla configurazione del passaggio. Se si seleziona **Necessario per l'installazione - Solo aggiornamenti software obbligatori** oppure **Disponibile per l'installazione - Tutti gli aggiornamenti software**. È anche possibile specificare questo comportamento usando la variabile [SMSInstallUpdateTarget](task-sequence-variables.md#SMSInstallUpdateTarget).
        1. **Installazione agente SUM**: processo di installazione normale con l'elenco esistente memorizzato nella cache degli aggiornamenti, con download del contenuto standard. L'aggiornamento viene installato tramite l'agente di Windows Update. (UpdatesDeployment.log, UpdatesHandler.log, WuaHandler.log, WindowsUpdate.log)
    2. **Avvia timer distribuzione e visualizza stato**: il motore della sequenza di attività avvia un timer per l'installazione, mostra lo stato di avanzamento a intervalli del 10% nell'interfaccia utente di stato di TS e rimane in attesa.
        1. **Monitoraggio**: il motore della sequenza di attività esegue il polling dell'agente SUM per ottenere informazioni sullo stato.
        2. *Qual è la risposta dall'agente SUM?*
            - **In corso**: *Il processo di installazione è rimasto inattivo per 8 ore?*
                - **Sì**: il passaggio non riesce.
                - **No**: passare a **Monitoraggio**
            - **Operazione non riuscita**: il passaggio non riesce.
            - **Completa**: passare a *Il passaggio è configurato con l'opzione **Valuta gli aggiornamenti software dai risultati di analisi memorizzati nella cache**?*


### <a name="timeouts"></a>Timeout

Il diagramma include due variabili di timeout che si applicano a questo passaggio. Esistono altri timer standard da altri componenti che possono influire su questo processo.

- Timeout di ricerca degli aggiornamenti: 1 ora (smsts.log)  
- Timeout della richiesta di posizione: 1 ora (LocationServices.log, CAS.log)  
- Timeout di download del contenuto: 1 ora (DTS.log)  
- Timeout di punto di distribuzione inattivo: 1 ora (LocationServices.log, CAS.log)  
- Timeout installazioni totalmente inattive: 8 ore (smsts.log)  



## <a name="troubleshooting"></a>Risoluzione dei problemi

Usare le risorse e le informazioni aggiuntive seguenti per risolvere i problemi con questo passaggio:

- Assicurarsi di impostare come destinazione delle distribuzioni di aggiornamento software la stessa raccolta della distribuzione della sequenza di attività.  

- Assicurarsi di includere i punti di aggiornamento software nei gruppi di limiti. Per altre informazioni, vedere questo [articolo del supporto tecnico Microsoft](https://support.microsoft.com/help/4041012/1702-clients-do-not-get-software-updates-from-configuration-manager).  

- Per risolvere i problemi relativi al il processo di gestione degli aggiornamenti software, vedere [Risoluzione dei problemi di gestione degli aggiornamenti software](https://support.microsoft.com/help/10680/software-update-management-troubleshooting-in-configuration-manager).  

- Per contribuire a migliorare le prestazioni complessive, ridurre le dimensioni del catalogo di aggiornamenti software. Ad esempio:  

    - rimuovere eventuali classificazioni, prodotti e lingue non necessari. Per altre informazioni, vedere [Configurare le classificazioni e i prodotti per la sincronizzazione](../../sum/get-started/configure-classifications-and-products.md).  

    - Reindicizzare il database del sito e ricompilare le statistiche. Per altre informazioni, vedere il [white paper dedicato alle linee guida per le prestazioni e la scalabilità di Configuration Manager](https://gallery.technet.microsoft.com/Configuration-Manager-ba55428e).  

    - Rifiutare eventuali aggiornamenti non necessari, ad esempio:
        - Componenti sostituiti (a partire dalla versione 1810, Configuration Manager esegue automaticamente questa azione. Per altre informazioni, vedere [Comportamento del processo di pulizia WSUS a partire dalla versione 1810](../../sum/deploy-use/software-updates-maintenance.md#wsus-cleanup-behavior-starting-in-version-1810)).
        - Itanium
        - Beta
        - Version Next
        - ARM
        - Versioni di Windows non distribuite