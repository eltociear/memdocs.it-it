---
title: Passaggi della sequenza di attività
titleSuffix: Configuration Manager
description: Informazioni sui passaggi che è possibile aggiungere a una sequenza di attività di Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 7c888a6f-8e37-4be5-8edb-832b218f266d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 114a0a18b3eb5d416b45379ccb3ac68128e529c5
ms.sourcegitcommit: 22e1095a41213372c52d85c58b18cbabaf2300ac
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/25/2020
ms.locfileid: "85353599"
---
# <a name="task-sequence-steps"></a>Passaggi della sequenza di attività

*Si applica a: Configuration Manager (Current Branch)*

A una sequenza di attività di Configuration Manager è possibile aggiungere i passaggi seguenti. Per altre informazioni, vedere [Usare l'editor delle sequenze di attività](task-sequence-editor.md).  

## <a name="common-settings"></a>Impostazioni comuni

Le impostazioni seguenti sono comuni a tutti i passaggi della sequenza di attività:

### <a name="properties-for-all-steps"></a>Proprietà per tutti i passaggi

- **Nome**: l'editor della sequenza di attività richiede di specificare un nome breve per descrivere questo passaggio. Quando si aggiunge un nuovo passaggio, per impostazione predefinita l'editor della sequenza di attività imposta come nome il valore di Tipo. La lunghezza di **Nome** non può superare i 50 caratteri.  

- **Descrizione**: facoltativamente, aggiungere informazioni più dettagliate sul passaggio. La lunghezza di **Descrizione** non può superare i 256 caratteri.  

La parte restante di questo articolo descrive le altre impostazioni della scheda **Proprietà** per ogni passaggio della sequenza di attività.

### <a name="options-for-all-steps"></a>Opzioni per tutti i passaggi

- **Disattiva questo passaggio**: la sequenza di attività ignora questo passaggio quando viene eseguita in un computer. L'icona del passaggio è disattivata nell'editor della sequenza di attività.  

- **Continua in caso di errore**: in caso di errore durante l'esecuzione del passaggio, la sequenza di attività continua. Per altre informazioni, vedere [Considerazioni sulla pianificazione per l'automazione delle attività](../plan-design/planning-considerations-for-automating-tasks.md#BKMK_TSGroups).  

- **Aggiungi condizione**: la sequenza di attività valuta queste istruzioni condizionali per determinare se il passaggio viene eseguito. Per un esempio dell'uso di una variabile della sequenza di attività come condizione, vedere [Come usare le variabili della sequenza di attività](using-task-sequence-variables.md#bkmk_access-condition). Per altre informazioni sulle condizioni, vedere [Editor delle sequenze di attività - Condizioni](task-sequence-editor.md#bkmk_conditions).

Le sezioni seguenti relative a passaggi specifici della sequenza di attività descrivono altre impostazioni possibili della scheda **Opzioni**.



## <a name="apply-data-image"></a><a name="BKMK_ApplyDataImage"></a> Applica immagine dei dati

Usare questo passaggio per copiare l'immagine dei dati nella partizione di destinazione specificata.  

Questo passaggio può essere eseguito solo in Windows PE. Non viene eseguito nel sistema operativo completo.

Per aggiungere questo passaggio nell'editor della sequenza di attività, selezionare **Aggiungi**, selezionare **Immagini** e quindi selezionare **Applica immagine dei dati**.

### <a name="variables-for-apply-data-image"></a>Variabili per Applica immagine dei dati

Usare le variabili della sequenza di attività seguenti con questo passaggio:  

- [OSDDataImageIndex](task-sequence-variables.md#OSDDataImageIndex)  
- [OSDWipeDestinationPartition](task-sequence-variables.md#OSDWipeDestinationPartition)  

### <a name="cmdlets-for-apply-data-image"></a>Cmdlet per Applica immagine dei dati

Gestire questo passaggio con i cmdlet di PowerShell seguenti:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyDataImage](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepApplyDataImage?view=sccm-ps)
- [New-CMTSStepApplyDataImage](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepApplyDataImage?view=sccm-ps)
- [Remove-CMTSStepApplyDataImage](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepApplyDataImage?view=sccm-ps)
- [Set-CMTSStepApplyDataImage](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepApplyDataImage?view=sccm-ps)

### <a name="properties-for-apply-data-image"></a>Proprietà per Applica immagine dei dati

Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

#### <a name="image-package"></a>Pacchetto immagine

Selezionare **Sfoglia** per specificare il **Pacchetto immagine** usato da questa sequenza di attività. Selezionare il pacchetto da installare nella finestra di dialogo **Seleziona un pacchetto** . Nella parte inferiore della finestra di dialogo sono visualizzate le informazioni sulle proprietà associate per ogni pacchetto immagine esistente. Usare l'elenco a discesa per selezionare l' **Immagine** da installare dal pacchetto **Pacchetto immagine**selezionato.  

> [!NOTE]  
> Questa azione della sequenza di attività considera l'immagine come un file di dati. Questa azione non esegue nessuna configurazione per avviare l'immagine come un sistema operativo.  

#### <a name="destination"></a>Destination

Configurare una delle opzioni seguenti:

- **Next available partition** (Partizione successiva disponibile): usare la partizione sequenziale successiva non ancora sottoposta a un passaggio **Applica sistema operativo** o **Applica immagine dei dati** in questa sequenza di attività.  

- **Disco e partizione specifici**: selezionare un numero per **Disco** (a partire da 0) e per **Partizione** (a partire da 1).  

- **Lettera unità logica specifica**: specificare la **Lettera unità** assegnata alla partizione da Windows PE. Questa lettera di unità può essere diversa da quella assegnata dal sistema operativo appena distribuito.  

- **Lettera unità logica archiviata in una variabile**: specificare la variabile della sequenza di attività contenente la lettera di unità assegnata alla partizione da Windows PE. Questa variabile viene in genere impostata nella sezione Avanzate della finestra di dialogo **Proprietà della partizione** per il passaggio **Formato e disco partizione** della sequenza di attività.  

#### <a name="delete-all-content-on-the-partition-before-applying-the-image"></a>Elimina tutti i contenuti nella partizione prima di applicare l'immagine  

Specifica che la sequenza di attività elimina tutti i file nella partizione di destinazione prima di installare l'immagine. Non eliminando il contenuto della partizione, questa azione può essere usata per applicare contenuti aggiuntivi a una partizione interessata in precedenza da questa attività.  



## <a name="apply-driver-package"></a><a name="BKMK_ApplyDriverPackage"></a> Applica pacchetto di driver  

Usare questo passaggio per scaricare tutti i driver del pacchetto di driver e installarli nel sistema operativo Windows.

Il passaggio **Applica pacchetto di driver** della sequenza di attività rende disponibili tutti i driver di dispositivo inclusi in un pacchetto di driver per l'uso da parte di Windows. Aggiungere questo passaggio tra i passaggi **Applica sistema operativo** e **Imposta Windows e ConfigMgr** per rendere disponibili a Windows i driver inclusi nel pacchetto. Il passaggio **Applica pacchetto di driver** della sequenza di attività è utile anche negli scenari di distribuzione di supporti autonomi.  

Inserire driver di dispositivi simili in un pacchetto di driver e quindi distribuirli nei punti di distribuzione appropriati. Ad esempio, inserire tutti i driver di un determinato produttore in un pacchetto di driver. Quindi distribuire il pacchetto in punti di distribuzione accessibili ai computer associati.

Il passaggio **Applica pacchetto di driver** è utile per i supporti autonomi. Questo passaggio è utile anche per installare un set di driver specifico. Questi tipi di driver includono i dispositivi non rilevati da Plug-and-Play di Windows, come le stampanti di rete.  

Questo passaggio della sequenza di attività può essere eseguito solo in Windows PE. Non viene eseguito nel sistema operativo completo.

Per aggiungere questo passaggio nell'editor della sequenza di attività, selezionare **Aggiungi**, selezionare **Driver** e quindi selezionare **Applica pacchetto driver**.

> [!TIP]
> Per una panoramica sui driver di Configuration Manager, vedere [Usare le sequenze di attività per installare i driver](../get-started/manage-drivers.md#BKMK_TSDrivers).
>
> Usare la memorizzazione anticipata del contenuto nella cache per scaricare un pacchetto di driver applicabile prima che un utente installi la sequenza di attività. Per altre informazioni, vedere [Configurare la pre-cache del contenuto](../deploy-use/configure-precache-content.md).

### <a name="variables-for-apply-driver-package"></a>Variabili per Applica pacchetto di driver

Usare le variabili della sequenza di attività seguenti con questo passaggio:  

- [OSDApplyDriverBootCriticalContentUniqueID](task-sequence-variables.md#OSDApplyDriverBootCriticalContentUniqueID)  
- [OSDApplyDriverBootCriticalHardwareComponent](task-sequence-variables.md#OSDApplyDriverBootCriticalHardwareComponent)  
- [OSDApplyDriverBootCriticalID](task-sequence-variables.md#OSDApplyDriverBootCriticalID)  
- [OSDApplyDriverBootCriticalINFFile](task-sequence-variables.md#OSDApplyDriverBootCriticalINFFile)  
- [OSDInstallDriversAdditionalOptions](task-sequence-variables.md#OSDInstallDriversAdditionalOptions)<!--516679/2840016-->

### <a name="cmdlets-for-apply-driver-package"></a>Cmdlet per Applica pacchetto di driver

Gestire questo passaggio con i cmdlet di PowerShell seguenti:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyDriverPackage](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepApplyDriverPackage?view=sccm-ps)
- [New-CMTSStepApplyDriverPackage](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepApplyDriverPackage?view=sccm-ps)
- [Remove-CMTSStepApplyDriverPackage](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepApplyDriverPackage?view=sccm-ps)
- [Set-CMTSStepApplyDriverPackage](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepApplyDriverPackage?view=sccm-ps)

### <a name="properties-for-apply-driver-package"></a>Proprietà per Applica pacchetto di driver

Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

#### <a name="driver-package"></a>Pacchetto driver

Specificare il pacchetto di driver che contiene i driver di dispositivo necessari. Selezionare **Sfoglia** per avviare la finestra di dialogo **Seleziona un pacchetto**. Selezionare un pacchetto di driver esistente da applicare. Le proprietà associate del pacchetto vengono visualizzate nella parte inferiore della finestra di dialogo.  

#### <a name="install-driver-package-via-running-dism-with-recurse-option"></a>Installa il pacchetto driver eseguendo DISM con l'opzione di ricorsione

Selezionare questa opzione per aggiungere il parametro `/recurse` alla riga di comando di DISM quando Windows applica il pacchetto di driver.

Quando si abilita questa opzione, è anche possibile specificare altri parametri della riga di comando di DISM. Usare la variabile della sequenza di attività [OSDInstallDriversAdditionalOptions](task-sequence-variables.md#OSDInstallDriversAdditionalOptions) per includere altre opzioni. Per altre informazioni, vedere [Windows 10 DISM Command-Line Options](https://docs.microsoft.com/windows-hardware/manufacture/desktop/deployment-image-servicing-and-management--dism--command-line-options) (Opzioni della riga di comando di DISM Windows 10).<!-- SCCMDocs#2125 -->

#### <a name="select-the-mass-storage-driver-within-the-package-that-needs-to-be-installed-before-setup-on-pre-windows-vista-operating-systems"></a>Selezionare il driver di archiviazione di massa nel pacchetto da installare prima che Configuration Manager installi i sistemi operativi Windows precedenti a Windows Vista

Specificare gli eventuali driver di archiviazione di massa necessari per installare un sistema operativo classico.  

##### <a name="driver"></a>Driver

Selezionare il file del driver di archiviazione di massa da installare prima dell'installazione di un sistema operativo classico. L'elenco a discesa viene popolato dal pacchetto specificato.  

##### <a name="model"></a>Modello

Specificare il dispositivo critico per l'avvio necessario per le distribuzioni di sistemi operativi precedenti a Windows Vista.  

#### <a name="do-unattended-installation-of-unsigned-drivers-on-version-of-windows-where-this-is-allowed"></a>Esegui l'installazione automatica dei driver senza firma sulle versioni di Windows in cui è consentito

Questa opzione consente a Windows di installare driver senza firma digitale.  



## <a name="apply-network-settings"></a><a name="BKMK_ApplyNetworkSettings"></a> Applica impostazioni di rete  

Usare questo passaggio per specificare le informazioni di configurazione della rete o del gruppo di lavoro per il computer di destinazione. La sequenza di attività archivia questi valori nel file di risposte appropriato. Installazione di Windows usa questo file di risposte durante l'azione **Imposta Windows e ConfigMgr**.  

Questo passaggio della sequenza di attività può essere eseguito solo in Windows PE. Non viene eseguito nel sistema operativo completo.

Per aggiungere questo passaggio nell'editor della sequenza di attività, selezionare **Aggiungi**, selezionare **Impostazioni** e quindi selezionare **Applica impostazioni di rete**.

> [!NOTE]
> Se si includono più istanze di questo passaggio in una sequenza di attività, le condizioni non si applicano. Al dispositivo vengono applicate le impostazioni dell'ultima istanza di questo passaggio nella sequenza di attività. Per ovviare a questo comportamento, includere ogni passaggio in un gruppo distinto con le condizioni del gruppo.

### <a name="variables-for-apply-network-settings"></a>Variabili per Applica impostazioni di rete

Usare le variabili della sequenza di attività seguenti con questo passaggio:  

- [OSDAdapter](task-sequence-variables.md#OSDAdapter)  
- [OSDAdapterCount](task-sequence-variables.md#OSDAdapterCount)  
- [OSDDNSDomain](task-sequence-variables.md#OSDDNSDomain)  
- [OSDDNSSuffixSearchOrder](task-sequence-variables.md#OSDDNSSuffixSearchOrder)  
- [OSDDomainName](task-sequence-variables.md#OSDDomainName)  
- [OSDDomainOUName](task-sequence-variables.md#OSDDomainOUName)  
- [OSDEnableTCPIPFiltering](task-sequence-variables.md#OSDEnableTCPIPFiltering)  
- [OSDJoinAccount](task-sequence-variables.md#OSDJoinAccount)  
- [OSDJoinPassword](task-sequence-variables.md#OSDJoinPassword)  
- [OSDWorkgroupName](task-sequence-variables.md#OSDWorkgroupName)  

### <a name="cmdlets-for-apply-network-settings"></a>Cmdlet per Applica impostazioni di rete

Gestire questo passaggio con i cmdlet di PowerShell seguenti:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyNetworkSetting](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepApplyNetworkSetting?view=sccm-ps)
- [New-CMTSStepApplyNetworkSetting](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepApplyNetworkSetting?view=sccm-ps)
- [Remove-CMTSStepApplyNetworkSetting](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepApplyNetworkSetting?view=sccm-ps)
- [Set-CMTSStepApplyNetworkSetting](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepApplyNetworkSetting?view=sccm-ps)

### <a name="properties-for-apply-network-settings"></a>Proprietà per Applica impostazioni di rete

Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

#### <a name="join-a-workgroup"></a>Aggiunta a un gruppo di lavoro

Selezionare questa opzione per aggiungere il computer di destinazione al gruppo di lavoro specificato. Immettere il nome del gruppo di lavoro nella riga **Gruppo di lavoro** . Il valore acquisito dal passaggio della sequenza di attività **Acquisisci impostazioni di rete** può sostituire questo valore.

#### <a name="join-a-domain"></a>Aggiunta a un dominio

Selezionare questa opzione per aggiungere il computer di destinazione al dominio specificato. Specificare o selezionare il dominio, ad esempio `fabricam.com`. Specificare o selezionare un percorso LDAP (Lightweight Directory Access Protocol) per un'unità organizzativa. Ad esempio: `LDAP//OU=computers, DC=Fabricam.com, C=com`.  

#### <a name="account"></a>Account

Selezionare **Imposta** per specificare un account con le autorizzazioni necessarie per l'aggiunta del computer al dominio. Nella finestra di dialogo **Account utente di Windows** immettere il nome utente nel formato seguente: `Domain\User`. Per altre informazioni, vedere [Account di aggiunta dominio](../../core/plan-design/hierarchy/accounts.md#task-sequence-domain-join-account).

#### <a name="adapter-settings"></a>Impostazioni della scheda

Specificare le configurazioni di rete per ogni scheda di rete nel computer. Selezionare **Nuovo** per aprire la finestra di dialogo **Impostazioni di rete** e quindi specificare le impostazioni di rete.

- Se si usa anche il passaggio **Acquisisci impostazioni di rete**, la sequenza di attività applica le impostazioni acquisite in precedenza alla scheda di rete.
- Se la sequenza di attività non ha acquisito in precedenza le impostazioni di rete, applica le impostazioni specificate in questo passaggio.
- La sequenza di attività applica queste impostazioni alle schede di rete nell'ordine dell'enumerazione dispositivi di Windows.  
- La sequenza di attività non applica immediatamente le impostazioni specificate in questo passaggio nel computer.



## <a name="apply-operating-system-image"></a><a name="BKMK_ApplyOperatingSystemImage"></a> Applica immagine del sistema operativo  

Usare questo passaggio per installare un sistema operativo nel computer di destinazione.

Dopo l'esecuzione dell'azione **Applica sistema operativo** la variabile **OSDTargetSystemDrive** viene impostata sulla lettera di unità della partizione che include i file del sistema operativo.  

Questo passaggio della sequenza di attività può essere eseguito solo in Windows PE. Non viene eseguito nel sistema operativo completo.

Per aggiungere questo passaggio nell'editor della sequenza di attività, selezionare **Aggiungi**, selezionare **Immagini** e quindi selezionare **Applica immagine del sistema operativo**.

> [!TIP]
> A partire da Windows 10 versione 1709 il supporto include più edizioni. Quando si configura una sequenza di attività per l'uso di un pacchetto di aggiornamento del sistema operativo o di un'immagine del sistema operativo, verificare di selezionare un'[edizione supportata](../../core/plan-design/configs/support-for-windows-10.md#windows-10-as-a-client).  
>
> Usare la memorizzazione anticipata del contenuto nella cache per scaricare un pacchetto di aggiornamento del sistema operativo applicabile prima che un utente installi la sequenza di attività. Per altre informazioni, vedere [Configurare la pre-cache del contenuto](../deploy-use/configure-precache-content.md).
>
> Il passaggio **Imposta Windows e ConfigMgr** avvia l'installazione di Windows.

### <a name="variables-for-apply-os-image"></a>Variabili per Applica immagine del sistema operativo

Usare le variabili della sequenza di attività seguenti con questo passaggio:  

- [OSDConfigFileName](task-sequence-variables.md#OSDConfigFileName)  
- [OSDImageIndex](task-sequence-variables.md#OSDImageIndex)  
- [OSDTargetSystemDrive](task-sequence-variables.md#OSDTargetSystemDrive)  

### <a name="cmdlets-for-apply-os-image"></a>Cmdlet per Applica immagine del sistema operativo

Gestire questo passaggio con i cmdlet di PowerShell seguenti:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyOperatingSystem](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepApplyOperatingSystem?view=sccm-ps)
- [New-CMTSStepApplyOperatingSystem](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepApplyOperatingSystem?view=sccm-ps)
- [Remove-CMTSStepApplyOperatingSystem](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepApplyOperatingSystem?view=sccm-ps)
- [Set-CMTSStepApplyOperatingSystem](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepApplyOperatingSystem?view=sccm-ps)

### <a name="behaviors-for-apply-os-image"></a>Comportamenti per Applica immagine del sistema operativo

Questo passaggio esegue azioni diverse a seconda che si usi un'immagine del sistema operativo o un pacchetto di aggiornamento del sistema operativo.  

#### <a name="os-image-actions"></a>Azioni dell'immagine del sistema operativo

Il passaggio **Applica immagine del sistema operativo** esegue le azioni seguenti quando si usa un'immagine del sistema operativo:  

1. Eliminare tutto il contenuto del volume interessato, ad eccezione dei file nella cartella specificata dalla variabile **\_SMSTSUserStatePath**.  

2. Estrarre i contenuti del file con estensione wim specificato nella partizione di destinazione specificata.  

3. Preparare il file di risposte:  

    1. Creare un nuovo file di risposte predefinito del programma di installazione di Windows (sysprep.inf o unattend.xml) per il sistema operativo distribuito.  

    2. Unire eventuali valori disponibili nel file di risposte specificato dall'utente.  

4. Copiare i caricatori di avvio di Windows nella partizione attiva.  

5. Configurare il file boot.ini o i dati di configurazione di avvio in modo che facciano riferimento al sistema operativo appena installato.  

#### <a name="os-upgrade-package-actions"></a>Azioni del pacchetto di aggiornamento del sistema operativo

Il passaggio **Applica immagine del sistema operativo** esegue le azioni seguenti quando si usa un pacchetto di aggiornamento del sistema operativo:  

1. Eliminare tutto il contenuto del volume interessato, ad eccezione dei file nella cartella specificata dalla variabile **\_SMSTSUserStatePath**.  

2. Preparare il file di risposte:  

    1. Creare un nuovo file di risposte con valori standard generati da Configuration Manager.  

    2. Unire eventuali valori disponibili nel file di risposte specificato dall'utente.  

### <a name="properties-for-apply-os-image"></a>Proprietà per Applica immagine del sistema operativo

Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

#### <a name="apply-operating-system-from-a-captured-image"></a>Applica sistema operativo da un'immagine acquisita

Installa un'immagine del sistema operativo acquisita. Selezionare **Sfoglia** per aprire la finestra di dialogo **Seleziona pacchetto**. Selezionare quindi il pacchetto dell'immagine esistente da installare. Se al **Pacchetto immagine**specificato sono associate più immagini, selezionare l'immagine associata da usare per questa distribuzione nell'elenco a discesa. Per visualizzare le informazioni di base su ogni immagine esistente, selezionarla.  

#### <a name="apply-operating-system-image-from-an-original-installation-source"></a>Applica sistema operativo da un'origine di installazione originale

Installa un sistema operativo usando un pacchetto di aggiornamento del sistema operativo, che è anche un'origine di installazione originale. Selezionare **Sfoglia** per aprire la finestra di dialogo **Seleziona un pacchetto di aggiornamento del sistema operativo**. Selezionare quindi il pacchetto di aggiornamento del sistema operativo esistente da usare. Per visualizzare le informazioni di base su ogni origine dell'immagine esistente, selezionarla. Le proprietà associate dell'origine dell'immagine vengono visualizzate nel riquadro dei risultati nella parte inferiore della finestra di dialogo. Se al pacchetto specificato sono associate più edizioni, usare l'elenco a discesa per specificare l'**edizione** da usare.  

> [!NOTE]  
> I **pacchetti di aggiornamento del sistema operativo** sono pensati principalmente per l'uso con gli aggiornamenti sul posto e non per le nuove installazioni di Windows. Quando si distribuiscono nuove installazioni di Windows, usare l'opzione **Applica sistema operativo da un'immagine acquisita** e **install.wim** dai file dell'origine di installazione.
>
> La distribuzione di nuove installazioni di Windows effettuata con i **pacchetti di aggiornamento del sistema operativo** è ancora supportata, ma dipende dalla compatibilità dei driver con questo metodo. Quando si installa Windows da un pacchetto di aggiornamento del sistema operativo, i driver vengono installati quando si trovano ancora in Windows PE, anziché essere semplicemente inseriti mentre sono in Windows PE. Alcuni driver non sono compatibili con l'installazione da Windows PE.
>
> Se i driver non sono compatibili con l'installazione da Windows PE, creare un'**immagine del sistema operativo** con il file **install.wim** dai file dell'origine di installazione originale. Eseguire quindi la distribuzione usando in alternativa l'opzione **Applica sistema operativo da un'immagine acquisita**.

#### <a name="use-an-unattended-or-sysprep-answer-file-for-a-custom-installation"></a>Usa un file di risposta automatica o Sysprep per un'installazione personalizzata

Usare questa opzione per fornire un file di risposte del programma di installazione di Windows (**unattend.xml**, **unattend.txt** o **sysprep.inf**), in base alla versione e al metodo di installazione del sistema operativo. Il file specificato può includere qualsiasi opzione di configurazione standard supportata dai file di risposte di Windows. È ad esempio possibile usarla per specificare la home page predefinita di Internet Explorer. Specificare il pacchetto che contiene il file di risposte e il percorso associato al file nel pacchetto.  

> [!NOTE]  
> Il file di risposte del programma di installazione di Windows fornito può includere variabili incorporate della sequenza di attività con formato `%varname%`, dove *varname* indica il nome della variabile. Il passaggio **Imposta Windows e ConfigMgr** sostituisce la stringa della variabile con il valore effettivo della variabile. Non è possibile usare queste variabili incorporate della sequenza di attività in campi di tipo solo numerico in un file di risposte unattend.xml.  

Se non si specifica un file di risposte del programma di installazione di Windows, la sequenza di attività genera automaticamente un file di risposte.  

#### <a name="destination"></a>Destination

Configurare una delle opzioni seguenti:  

- **Next available partition** (Partizione successiva disponibile): usare la partizione sequenziale successiva non ancora sottoposta a un passaggio **Applica sistema operativo** o **Applica immagine dei dati** in questa sequenza di attività.  

- **Disco e partizione specifici**: selezionare un numero per **Disco** (a partire da 0) e per **Partizione** (a partire da 1).  

- **Lettera unità logica specifica**: specificare la **Lettera unità** assegnata alla partizione da Windows PE. Questa lettera di unità può essere diversa da quella assegnata dal sistema operativo appena distribuito.  

- **Lettera unità logica archiviata in una variabile**: specificare la variabile della sequenza di attività contenente la lettera di unità assegnata alla partizione da Windows PE. Questa variabile viene in genere impostata nella sezione Avanzate della finestra di dialogo **Proprietà della partizione** per il passaggio **Formato e disco partizione** della sequenza di attività.  

### <a name="options-for-apply-os-image"></a>Opzioni per Applica immagine del sistema operativo

Oltre alle opzioni predefinite, nella scheda **Opzioni** di questo passaggio della sequenza di attività configurare le impostazioni aggiuntive seguenti:  

#### <a name="access-content-directly-from-the-distribution-point"></a>Accedi al contenuto direttamente dal punto di distribuzione

Configurare la sequenza di attività in modo che acceda all'immagine del sistema operativo direttamente dal punto di distribuzione. Usare questa opzione ad esempio quando si distribuiscono sistemi operativi in dispositivi incorporati con capacità di archiviazione limitata. Quando si seleziona questa opzione è necessario configurare anche le impostazioni di condivisione pacchetto nella scheda **Accesso dati** delle proprietà dell'immagine del sistema operativo.  

> [!NOTE]  
> Questa impostazione sostituisce l'opzione di distribuzione configurata nella pagina **Punti di distribuzione** di **Distribuzione guidata del software**. La sostituzione è valida solo per l'immagine del sistema operativo specificata in questo passaggio e non per l'intero contenuto della sequenza di attività.  

> [!IMPORTANT]  
> Per mantenere la massima sicurezza, è consigliabile non selezionare questa opzione. Questa opzione è progettata principalmente per l'uso in dispositivi con capacità di archiviazione limitata. Questa opzione non ha lo scopo di aumentare la velocità della sequenza di attività. Quando questa opzione è selezionata, l'hash del pacchetto non viene verificato per il pacchetto del sistema operativo. Pertanto, l'integrità del pacchetto non può essere garantita perché gli utenti con diritti amministrativi possono modificare o alterare i contenuti del pacchetto.



## <a name="apply-windows-settings"></a><a name="BKMK_ApplyWindowsSettings"></a> Applica impostazioni Windows

Usare questa attività per configurare le impostazioni di Windows per il computer di destinazione. La sequenza di attività archivia questi valori nel file di risposte appropriato. Installazione di Windows usa questo file di risposte durante il passaggio **Imposta Windows e ConfigMgr**.  

Questo passaggio della sequenza di attività può essere eseguito solo in Windows PE. Non viene eseguito nel sistema operativo completo.  

Per aggiungere questo passaggio nell'editor della sequenza di attività, selezionare **Aggiungi**, selezionare **Impostazioni** e quindi selezionare **Applica impostazioni Windows**.

### <a name="variables-for-apply-windows-settings"></a>Variabili per Applica impostazioni Windows

Usare le variabili della sequenza di attività seguenti con questo passaggio:  

- [OSDComputerName](task-sequence-variables.md#OSDComputerName-input)  
- [OSDLocalAdminPassword](task-sequence-variables.md#OSDLocalAdminPassword)  
- [OSDProductKey](task-sequence-variables.md#OSDProductKey)  
- [OSDRandomAdminPassword](task-sequence-variables.md#OSDRandomAdminPassword)  
- [OSDRegisteredOrgName](task-sequence-variables.md#OSDRegisteredOrgName-input)  
- [OSDRegisteredUserName](task-sequence-variables.md#OSDRegisteredUserName)  
- [OSDServerLicenseConnectionLimit](task-sequence-variables.md#OSDServerLicenseConnectionLimit)  
- [OSDServerLicenseMode](task-sequence-variables.md#OSDServerLicenseMode)  
- [OSDTimeZone](task-sequence-variables.md#OSDTimeZone-input)  
- [OSDWindowsSettingsInputLocale](task-sequence-variables.md#OSDWindowsSettingsInputLocale)
- [OSDWindowsSettingsSystemLocale](task-sequence-variables.md#OSDWindowsSettingsSystemLocale)
- [OSDWindowsSettingsUILanguage](task-sequence-variables.md#OSDWindowsSettingsUILanguage)
- [OSDWindowsSettingsUILanguageFallback](task-sequence-variables.md#OSDWindowsSettingsUILanguageFallback)
- [OSDWindowsSettingsUserLocale](task-sequence-variables.md#OSDWindowsSettingsUserLocale)

### <a name="cmdlets-for-apply-windows-settings"></a>Cmdlet per Applica impostazioni Windows

Gestire questo passaggio con i cmdlet di PowerShell seguenti:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyWindowsSetting](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepApplyWindowsSetting?view=sccm-ps)
- [New-CMTSStepApplyWindowsSetting](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepApplyWindowsSetting?view=sccm-ps)
- [Remove-CMTSStepApplyWindowsSetting](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepApplyWindowsSetting?view=sccm-ps)
- [Set-CMTSStepApplyWindowsSetting](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepApplyWindowsSetting?view=sccm-ps)

### <a name="properties-for-apply-windows-settings"></a>Proprietà per Applica impostazioni Windows

Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

#### <a name="user-name"></a>Nome utente

Specificare il nome dell'utente registrato da associare al computer di destinazione. Il valore acquisito dal passaggio della sequenza di attività **Acquisisci impostazioni Windows** può sostituire questo valore.  

#### <a name="organization-name"></a>Nome organizzazione

Specificare il nome dell'organizzazione registrata da associare al computer di destinazione. Il valore acquisito dal passaggio della sequenza di attività **Acquisisci impostazioni Windows** può sostituire questo valore.  

#### <a name="product-key"></a>Codice Product Key  

Specificare il codice Product Key da usare per l'installazione di Windows nel computer di destinazione.  

#### <a name="server-licensing"></a>Licenze server

Specificare la modalità di gestione delle licenza del server,

- ovvero **Per server** o **Per Utente**.  
- Se si sceglie **Per server** specificare anche il numero massimo di connessioni consentite in base al contratto di licenza.  
- Se il computer di destinazione non è un server o se non si vuole specificare la modalità di gestione delle licenze, selezionare **Non specificare**.  

#### <a name="maximum-connections"></a>Numero massimo di connessioni

> [!NOTE]
> Questa impostazione si applica solo alle versioni legacy di Windows che non sono più supportate.<!-- #4833 -->

#### <a name="randomly-generate-the-local-administrator-password-and-disable-the-account-on-all-supported-platforms-recommended"></a>Genera in modo casuale la password dell'amministratore locale e disattiva l'account su tutte le piattaforme supportate (consigliato)  

Selezionare questa opzione per impostare come password per l'amministratore locale una stringa generata in modo casuale. Questa opzione disabilita anche l'account amministratore locale sulle piattaforme che supportano questa funzionalità.  

#### <a name="enable-the-account-and-specify-the-local-administrator-password"></a>Attiva l'account e specifica la password dell'amministratore locale  

Selezionare questa opzione per abilitare l'account dell'amministratore locale mediante la password specificata. Immettere la password nella riga **Password** e confermare la password nella riga **Conferma password** .  

#### <a name="time-zone"></a>Fuso orario

Specificare il fuso orario da configurare nel computer di destinazione. Il valore acquisito dal passaggio della sequenza di attività **Acquisisci impostazioni Windows** può sostituire questo valore.  

#### <a name="language-settings"></a>Impostazione della lingua

<!--5411057, 5138936-->

A partire dalla versione 1910, controllare la configurazione della lingua durante la distribuzione del sistema operativo. Se si stanno già applicando queste impostazioni della lingua, la modifica consente di semplificare la sequenza di attività di distribuzione del sistema operativo. Invece di usare più passaggi per lingua o script distinti, usare una sola istanza per ogni lingua del passaggio con una condizione per tale lingua.

Configurare le seguenti impostazioni:

- Impostazioni locali per l'input (layout di tastiera predefinito)
- Impostazioni locali di sistema
- Lingua dell'interfaccia utente
- Fallback della lingua dell'interfaccia utente
- Impostazioni locali dell'utente

Per altre informazioni sui valori dei file di risposte dell'installazione di Windows, vedere [Microsoft-Windows-International-Core](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core).

> [!NOTE]
> Se si crea un file di risposte personalizzato per l'installazione di Windows (unattend.xml), questo passaggio sovrascrive tutti i valori esistenti. Per automatizzare un processo dinamico per queste impostazioni, usare le variabili della sequenza di attività correlate, ad esempio, [OSDWindowsSettingsInputLocale](task-sequence-variables.md#OSDWindowsSettingsInputLocale). 

## <a name="auto-apply-drivers"></a><a name="BKMK_AutoApplyDrivers"></a> Applica automaticamente i driver

Usare questo passaggio per associare e installare i driver come parte della distribuzione del sistema operativo.  

> [!IMPORTANT]  
> I supporti autonomi non possono usare il passaggio **Applica automaticamente i driver**. La sequenza di attività non ha connessioni al sito di Configuration Manager in questo scenario.  

Questo passaggio della sequenza di attività può essere eseguito solo in Windows PE. Non viene eseguito nel sistema operativo completo.

Per aggiungere questo passaggio nell'editor della sequenza di attività, selezionare **Aggiungi**, selezionare **Driver** e quindi selezionare **Applica automaticamente i driver**.

> [!TIP]
> Per una panoramica dei driver di Configuration Manager, vedere [Usare le sequenze di attività per installare i driver](../get-started/manage-drivers.md#BKMK_TSDrivers).

### <a name="behaviors-for-auto-apply-drivers"></a>Comportamenti per Applica automaticamente i driver

Il passaggio **Applica automaticamente i driver** della sequenza di attività esegue le azioni seguenti:  

1. Analizzare l'hardware e trovare gli ID plug-and-play per tutti i dispositivi presenti nel sistema.  

2. Inviare l'elenco dei dispositivi e dei rispettivi ID plug-and-play al punto di gestione. Il punto di gestione restituisce un elenco di driver compatibili dal catalogo di driver per ogni dispositivo hardware. L'elenco include tutti i driver abilitati indipendentemente dal pacchetto di driver in cui si trovano e i driver contrassegnati con la categoria di driver specificata.  

3. La sequenza di attività sceglie il driver ottimale per ogni dispositivo hardware. Questo driver è appropriato per il sistema operativo distribuito e si trova in un punto di distribuzione accessibile.  

4. La sequenza di attività scarica i driver selezionati da un punto di distribuzione e li prepara nel sistema operativo di destinazione.  

    1. Quando si usa un'immagine del sistema operativo, la sequenza di attività posiziona i driver nell'archivio driver del sistema operativo.  

    2. Quando si usa un pacchetto di aggiornamento del sistema operativo come origine di installazione originale, la sequenza di attività configura Installazione di Windows con il percorso dei driver.  

5. Durante il passaggio **Imposta Windows e ConfigMgr** della sequenza di attività, Installazione di Windows individua i driver preparati da questo passaggio.  

### <a name="variables-for-auto-apply-drivers"></a>Variabili per Applica automaticamente i driver

Usare le variabili della sequenza di attività seguenti con questo passaggio:  

- [OSDAutoApplyDriverBestMatch](task-sequence-variables.md#OSDAutoApplyDriverBestMatch)  
- [OSDAutoApplyDriverCategoryList](task-sequence-variables.md#OSDAutoApplyDriverCategoryList)  
- [SMSTSDriverRequestConnectTimeOut](task-sequence-variables.md#SMSTSDriverRequestConnectTimeOut)  
- [SMSTSDriverRequestReceiveTimeOut](task-sequence-variables.md#SMSTSDriverRequestReceiveTimeOut)  
- [SMSTSDriverRequestResolveTimeOut](task-sequence-variables.md#SMSTSDriverRequestResolveTimeOut)  
- [SMSTSDriverRequestSendTimeOut](task-sequence-variables.md#SMSTSDriverRequestSendTimeOut)  

### <a name="cmdlets-for-auto-apply-drivers"></a>Cmdlet per Applica automaticamente i driver

Gestire questo passaggio con i cmdlet di PowerShell seguenti:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepAutoApplyDriver](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepAutoApplyDriver?view=sccm-ps)
- [New-CMTSStepAutoApplyDriver](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepAutoApplyDriver?view=sccm-ps)
- [Remove-CMTSStepAutoApplyDriver](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepAutoApplyDriver?view=sccm-ps)
- [Set-CMTSStepAutoApplyDriver](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepAutoApplyDriver?view=sccm-ps)

### <a name="properties-for-auto-apply-drivers"></a>Proprietà per Applica automaticamente i driver

Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

#### <a name="install-only-the-best-matched-compatible-drivers"></a>Installa solo i driver compatibili con la corrispondenza migliore

Indica che il passaggio della sequenza di attività installa solo i driver con la corrispondenza migliore per ogni dispositivo hardware rilevato.  

#### <a name="install-all-compatible-drivers"></a>Installa tutti i driver compatibili

La sequenza di attività installa tutti i driver compatibili per ogni dispositivo hardware rilevato. Quindi l'installazione di Windows sceglie il driver ottimale. Questa opzione richiede più larghezza di banda di rete e una maggior quantità di spazio su disco. La sequenza di attività scarica un numero maggiore di driver, ma Windows è in grado di selezionare un driver migliore.  

#### <a name="consider-drivers-from-all-categories"></a>Considera i driver di tutte le categorie

La sequenza di attività cerca i driver di dispositivo appropriati in tutte le categorie di driver disponibili.  

#### <a name="limit-driver-matching-to-only-consider-drivers-in-selected-categories"></a>Limita la corrispondenza dei driver in modo da considerare solo i driver delle categorie selezionate

La sequenza di attività cerca i driver di dispositivo appropriati nelle categorie di driver specificate.  

Se si selezionano più categorie, restituisce tutti i driver corrispondenti presenti in qualsiasi categoria. Equivale a un'operazione `OR`.<!-- SCCMDocs issue 851 -->

#### <a name="do-unattended-installation-of-unsigned-drivers-on-versions-of-windows-where-this-is-allowed"></a>Esegui l'installazione automatica dei driver senza firma sulle versioni di Windows in cui è consentito

Questa opzione consente a Windows di installare driver senza firma digitale.  

> [!IMPORTANT]  
> Questa opzione non è applicabile ai sistemi operativi in cui non è possibile configurare i criteri di firma dei driver.  



## <a name="capture-network-settings"></a><a name="BKMK_CaptureNetworkSettings"></a> Acquisisci impostazioni di rete

Usare questo passaggio per acquisire le impostazioni di rete Microsoft dal computer che esegue la sequenza di attività. La sequenza di attività salva queste impostazioni nelle variabili della sequenza di attività. Queste impostazioni sostituiscono le impostazioni predefinite configurate nel passaggio **Applica impostazioni di rete**.  

Questo passaggio della sequenza di attività viene eseguito solo nel sistema operativo completo. Non viene eseguito in Windows PE.  

Per aggiungere questo passaggio nell'editor della sequenza di attività, selezionare **Aggiungi**, selezionare **Impostazioni** e quindi selezionare **Acquisisci impostazioni di rete**.

### <a name="variables-for-capture-network-settings"></a>Variabili per Acquisisci impostazioni di rete

Usare le variabili della sequenza di attività seguenti con questo passaggio:  

- [OSDMigrateAdapterSettings](task-sequence-variables.md#OSDMigrateAdapterSettings)  
- [OSDMigrateNetworkMembership](task-sequence-variables.md#OSDMigrateNetworkMembership)  

### <a name="cmdlets-for-capture-network-settings"></a>Cmdlet per Acquisisci impostazioni di rete

Gestire questo passaggio con i cmdlet di PowerShell seguenti:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepCaptureNetworkSettings](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepCaptureNetworkSettings?view=sccm-ps)
- [New-CMTSStepCaptureNetworkSettings](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepCaptureNetworkSettings?view=sccm-ps)
- [Remove-CMTSStepCaptureNetworkSettings](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepCaptureNetworkSettings?view=sccm-ps)
- [Set-CMTSStepCaptureNetworkSettings](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepCaptureNetworkSettings?view=sccm-ps)

### <a name="properties-for-capture-network-settings"></a>Proprietà per Acquisisci impostazioni di rete

Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

#### <a name="migrate-domain-and-workgroup-membership"></a>Esegui la migrazione del dominio e dell'appartenenza a gruppi di lavoro

Acquisisce le informazioni sull'appartenenza a domini e gruppi di lavoro del computer di destinazione.  

#### <a name="migrate-network-adapter-configuration"></a>Esegui la migrazione della configurazione della scheda di rete

Acquisisce la configurazione della scheda di rete del computer di destinazione. Vengono acquisite le informazioni seguenti:

- Impostazioni di rete globali  
- Numero di schede  
- Le impostazioni di rete seguenti associate a ogni scheda di rete: DNS, WINS, IP e filtri delle porte



## <a name="capture-operating-system-image"></a><a name="BKMK_CaptureOperatingSystemImage"></a> Acquisisci immagine del sistema operativo

Questo passaggio consente di acquisire una o più immagini da un computer di riferimento. La sequenza di attività crea un file immagine di Windows con estensione wim nella condivisione di rete specificata. Usare quindi la procedura guidata **Aggiungi pacchetto immagine sistema operativo** per importare l'immagine in Configuration Manager per le distribuzioni del sistema operativo basate su immagine.  

Configuration Manager acquisisce ogni volume (unità) nel computer di riferimento come immagine distinta nel file con estensione wim. Se il computer a cui si fa riferimento include più volumi, il file con estensione wim risultante contiene un'immagine distinta per ogni volume. Questo passaggio acquisisce solo i volumi con formattazione NTFS o FAT32. I volumi con formati diversi e i volumi USB vengono ignorati.  

Il sistema operativo installato nel computer di riferimento deve essere una versione di Windows supportata da Configuration Manager. Usare lo strumento SysPrep per preparare il sistema operativo nel computer di riferimento. Il volume del sistema operativo installato deve essere uguale al volume di avvio.  

Specificare un account con autorizzazioni di scrittura per la condivisione di rete selezionata. Per altre informazioni sull'account per l'acquisizione dell'immagine del sistema operativo, vedere [Account](../../core/plan-design/hierarchy/accounts.md#capture-os-image-account).

Questo passaggio della sequenza di attività può essere eseguito solo in Windows PE. Non viene eseguito nel sistema operativo completo.

Per aggiungere questo passaggio nell'editor della sequenza di attività, selezionare **Aggiungi**, selezionare **Immagini** e quindi selezionare **Acquisisci immagine del sistema operativo**.

### <a name="variables-for-capture-os-image"></a>Variabili per Acquisisci immagine del sistema operativo

Usare le variabili della sequenza di attività seguenti con questo passaggio:  

- [OSDCaptureAccount](task-sequence-variables.md#OSDCaptureAccount)  
- [OSDCaptureAccountPassword](task-sequence-variables.md#OSDCaptureAccountPassword)  
- [OSDCaptureDestination](task-sequence-variables.md#OSDCaptureDestination)  
- [OSDImageCreator](task-sequence-variables.md#OSDImageCreator)  
- [OSDImageDescription](task-sequence-variables.md#OSDImageDescription)  
- [OSDImageVersion](task-sequence-variables.md#OSDImageVersion)  
- [OSDTargetSystemRoot](task-sequence-variables.md#OSDTargetSystemRoot-input)  

### <a name="cmdlets-for-capture-os-image"></a>Cmdlet per Acquisisci immagine del sistema operativo

Gestire questo passaggio con i cmdlet di PowerShell seguenti:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepCaptureSystemImage](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepCaptureSystemImage?view=sccm-ps)
- [New-CMTSStepCaptureSystemImage](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepCaptureSystemImage?view=sccm-ps)
- [Remove-CMTSStepCaptureSystemImage](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepCaptureSystemImage?view=sccm-ps)
- [Set-CMTSStepCaptureSystemImage](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepCaptureSystemImage?view=sccm-ps)

### <a name="properties-for-capture-os-image"></a>Proprietà per Acquisisci immagine del sistema operativo

Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

#### <a name="target"></a>Destinazione  

Percorso del file system usato da Configuration Manager per l'archiviazione dell'immagine acquisita del sistema operativo.  

#### <a name="description"></a>Descrizione  

Descrizione facoltativa definita dall'utente dell'immagine acquisita del sistema operativo archiviata nel file dell'immagine.  

#### <a name="version"></a>Version  

Numero di versione facoltativo definito dall'utente da assegnare all'immagine del sistema operativo acquisita. Questo valore può essere costituito da qualsiasi combinazione di lettere e numeri. Viene archiviato nel file dell'immagine.  

#### <a name="created-by"></a>Creato da  

Nome facoltativo dell'utente che ha creato l'immagine del sistema operativo. Viene archiviato nel file dell'immagine.  

#### <a name="capture-operating-system-image-account"></a>Account di acquisizione immagine del sistema operativo  

Immettere l'account di Windows con autorizzazioni per la condivisione di rete specificata. Selezionare **Imposta** per specificare il nome dell'account di Windows.  



## <a name="capture-user-state"></a><a name="BKMK_CaptureUserState"></a> Acquisisci stato utente

Eseguire questo passaggio per usare l'Utilità di migrazione stato utente (USMT, User State Migration Tool) per acquisire lo stato utente e le impostazioni dal computer che esegue la sequenza di attività. Questo passaggio della sequenza di attività viene usato insieme al passaggio **Ripristina stato utente** . Questo passaggio crittografa sempre l'archivio degli stati USMT usando una chiave di crittografia generata e gestita da Configuration Manager.  

Per altre informazioni sulla gestione dello stato utente durante la distribuzione di sistemi operativi, vedere [Manage user state](../get-started/manage-user-state.md) (Gestire lo stato utente).  

Per salvare e ripristinare le impostazioni dello stato utente da un punto di migrazione stato, usare questo passaggio con i passaggi **Richiedi archiviazione stati** e **Rilascia archiviazione stati**.  

Questo passaggio consente il controllo di un sottoinsieme limitato delle opzioni USMT usate più comunemente. Specificare opzioni aggiuntive da riga di comando usando la variabile della sequenza di attività **OSDMigrateAdditionalCaptureOptions**.  

Questo passaggio della sequenza di attività può essere eseguito solo in Windows PE. Non viene eseguito nel sistema operativo completo.  

Per aggiungere questo passaggio nell'editor della sequenza di attività, selezionare **Aggiungi**, selezionare **Stato utente** e quindi selezionare **Acquisisci stato utente**.

### <a name="variables-for-capture-user-state"></a>Variabili per Acquisisci stato utente

Usare le variabili della sequenza di attività seguenti con questo passaggio:  

- [_OSDMigrateUsmtPackageID](task-sequence-variables.md#OSDMigrateUsmtPackageID)  
- [OSDMigrateAdditionalCaptureOptions](task-sequence-variables.md#OSDMigrateAdditionalCaptureOptions)  
- [OSDMigrateConfigFiles](task-sequence-variables.md#OSDMigrateConfigFiles)  
- [OSDMigrateContinueOnLockedFiles](task-sequence-variables.md#OSDMigrateContinueOnLockedFiles)  
- [OSDMigrateEnableVerboseLogging](task-sequence-variables.md#OSDMigrateEnableVerboseLogging)  
- [OSDMigrateMode](task-sequence-variables.md#OSDMigrateMode)  
- [OSDMigrateSkipEncryptedFiles](task-sequence-variables.md#OSDMigrateSkipEncryptedFiles)  
- [OSDStateStorePath](task-sequence-variables.md#OSDStateStorePath)  

### <a name="cmdlets-for-capture-user-state"></a>Cmdlet per Acquisisci stato utente

Gestire questo passaggio con i cmdlet di PowerShell seguenti:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepCaptureUserState](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepCaptureUserState?view=sccm-ps)
- [New-CMTSStepCaptureUserState](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepCaptureUserState?view=sccm-ps)
- [Remove-CMTSStepCaptureUserState](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepCaptureUserState?view=sccm-ps)
- [Set-CMTSStepCaptureUserState](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepCaptureUserState?view=sccm-ps)

### <a name="properties-for-capture-user-state"></a>Proprietà per Acquisisci stato utente

Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

#### <a name="user-state-migration-tool-package"></a>Pacchetto degli strumenti di migrazione dello stato utente

Specificare il pacchetto che contiene l'Utilità di migrazione stato utente (USMT) per ripristinare i dati sullo stato dell'utente. La sequenza di attività usa questa versione di USMT per acquisire lo stato e le impostazioni dell'utente. Questo pacchetto non richiede un programma. Specificare un pacchetto contenente la versione di USMT a 32 bit o a 64 bit. L'architettura di USMT dipende dall'architettura del sistema operativo da cui la sequenza di attività esegue l'acquisizione dello stato.  

#### <a name="capture-all-user-profiles-with-standard-options"></a>Acquisisci tutti i profili utente usando le opzioni standard

Eseguire la migrazione di tutte le informazioni del profilo utente. Questa opzione corrisponde all'impostazione predefinita.  

Se si seleziona questa opzione ma non si seleziona **Ripristina profili utente del computer locale** nel passaggio **Ripristina stato utente**, la sequenza di attività ha esito negativo. Configuration Manager non può eseguire la migrazione di nuovi account senza assegnare password.

Quando si usa l'opzione **Installa un pacchetto immagine esistente** della procedura guidata **New Task Sequence** (Nuova sequenza di attività), la sequenza di attività predefinita risultante è **Capture all user profiles with standard options** (Acquisisci tutti i profili utente con le opzioni standard). Questa sequenza di attività predefinita non seleziona l'opzione **Ripristina profili utente del computer locale**, ovvero gli account utente non del dominio.  

Selezionare **Ripristina profili utente del computer locale** e fornire una password per l'account di cui deve essere eseguita la migrazione. In una sequenza di attività creata manualmente questa impostazione è disponibile nel passaggio **Ripristina stato utente**. In una sequenza di attività creata dalla procedura guidata **Crea nuova sequenza di attività** questa impostazione è disponibile nella pagina della procedura guidata **Ripristina file utente e impostazioni** .  

In assenza di account utente locali, questa impostazione non è applicabile.  

#### <a name="customize-how-user-profiles-are-captured"></a>Personalizza modalità di acquisizione dei profili utente

Selezionare questa opzione per specificare un file di profilo personalizzato per la migrazione. Selezionare **File** per selezionare i file di configurazione che USMT dovrà usare con questo passaggio. Specificare un file con estensione xml personalizzato contenente le regole che definiscono i file di stato utente di cui eseguire la migrazione.  

#### <a name="click-here-to-select-configuration-files"></a>Fare clic qui per selezionare i file di configurazione

Selezionare questa opzione per selezionare i file di configurazione nel pacchetto USMT da usare per l'acquisizione dei profili utente. Selezionare **File** per aprire la finestra di dialogo **File di configurazione**. Per specificare un file di configurazione, immettere il nome del file nella riga **Nome file** e selezionare il pulsante **Aggiungi**.  

#### <a name="enable-verbose-logging"></a>Abilita la registrazione dettagliata

Abilitare questa opzione per generare informazioni di file di log più dettagliate. Durante l'acquisizione dello stato, per impostazione predefinita la sequenza di attività genera il file **ScanState.log** nella cartella dei log della sequenza di attività, `%WinDir%\ccm\logs`.  

#### <a name="skip-files-using-encrypted-file-system"></a>Ignora file che usano Encrypting File System (EFS)

Abilitare questa opzione per ignorare l'acquisizione di file crittografati con EFS (Encrypting File System). Questi file includono i file profilo utente. A seconda del sistema operativo e della versione di USMT, è possibile che i file crittografati non siano leggibili dopo il ripristino. Per altre informazioni, vedere la documentazione relativa a USMT.  

#### <a name="copy-by-using-file-system-access"></a>Copia usando l'accesso al file system

Abilitare questa opzione per specificare una delle impostazioni seguenti:  

- **Continua se non è possibile acquisire alcuni file**: abilitare questa impostazione per continuare il processo di migrazione, anche se non è possibile acquisire alcuni file. Se si disabilita questa opzione e non è possibile acquisire un file, il passaggio ha esito negativo. Questa opzione è attivata per impostazione predefinita.  

- **Esegui acquisizione localmente utilizzando i collegamenti invece di copiare i file**: Abilitare questa impostazione per usare i collegamenti reali NTFS per l'acquisizione dei file.  

    Per altre informazioni sulla migrazione di dati tramite i collegamenti reali, vedere [Archivio delle migrazioni con collegamento reale](https://docs.microsoft.com/windows/deployment/usmt/usmt-hard-link-migration-store).  

- **Acquisisci in modalità non in linea (solo Windows PE)** : abilitare questa impostazione per acquisire lo stato utente in Windows PE invece che nel sistema operativo completo.  

#### <a name="capture-by-using-volume-copy-shadow-services-vss"></a>Acquisisci usando Servizio Copia Shadow del volume (VSS)

Questa opzione consente di acquisire file anche se sono bloccati per la modifica da un'altra applicazione.  



## <a name="capture-windows-settings"></a><a name="BKMK_CaptureWindowsSettings"></a> Acquisisci impostazioni Windows

Usare questo passaggio per acquisire le impostazioni di Windows dal computer che esegue la sequenza di attività. La sequenza di attività salva queste impostazioni nelle variabili della sequenza di attività. Queste impostazioni acquisite sostituiscono le impostazioni predefinite configurate nel passaggio **Applica impostazioni Windows**.  

Questo passaggio della sequenza di attività può essere eseguito in Windows PE o nel sistema operativo completo.  

Per aggiungere questo passaggio nell'editor della sequenza di attività, selezionare **Aggiungi**, selezionare **Impostazioni** e quindi selezionare **Acquisisci impostazioni Windows**.

### <a name="variables-for-capture-windows-settings"></a>Variabili per Acquisisci impostazioni Windows

Usare le variabili della sequenza di attività seguenti con questo passaggio:  

- [OSDComputerName](task-sequence-variables.md#OSDComputerName-output)  
- [OSDMigrateComputerName](task-sequence-variables.md#OSDMigrateComputerName)  
- [OSDMigrateRegistrationInfo](task-sequence-variables.md#OSDMigrateRegistrationInfo)  
- [OSDMigrateTimeZone](task-sequence-variables.md#OSDMigrateTimeZone)  
- [OSDRegisteredOrgName](task-sequence-variables.md#OSDRegisteredOrgName-output)  
- [OSDTimeZone](task-sequence-variables.md#OSDTimeZone-output)  

### <a name="cmdlets-for-capture-windows-settings"></a>Cmdlet per Acquisisci impostazioni Windows

Gestire questo passaggio con i cmdlet di PowerShell seguenti:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepCaptureWindowsSettings](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepCaptureWindowsSettings?view=sccm-ps)
- [New-CMTSStepCaptureWindowsSettings](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepCaptureWindowsSettings?view=sccm-ps)
- [Remove-CMTSStepCaptureWindowsSettings](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepCaptureWindowsSettings?view=sccm-ps)
- [Set-CMTSStepCaptureWindowsSettings](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepCaptureWindowsSettings?view=sccm-ps)

### <a name="properties-for-capture-windows-settings"></a>Proprietà per Acquisisci impostazioni Windows

Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

#### <a name="migrate-computer-name"></a>Esegui la migrazione del nome computer

Acquisire il nome NetBIOS del computer.  

#### <a name="migrate-registered-user-and-organization-names"></a>Esegui la migrazione dell'utente registrato e dei nomi organizzazione

Acquisire l'utente registrato e i nomi dell'organizzazione dal computer.  

#### <a name="migrate-time-zone"></a>Esegui la migrazione del fuso orario

Acquisire l'impostazione relativa al fuso orario nel computer.  



## <a name="check-readiness"></a><a name="BKMK_CheckReadiness"></a> Verifica conformità

Usare questo passaggio per verificare se il computer di destinazione soddisfa le condizioni dei prerequisiti di distribuzione specificate.  

Per aggiungere questo passaggio nell'editor della sequenza di attività, selezionare **Aggiungi**, selezionare **Generale** e quindi selezionare **Verifica conformità**.

A partire dalla versione 2002, questo passaggio include otto nuovi controlli. Nessuno di questi nuovi controlli è selezionato per impostazione predefinita nelle istanze nuove o esistenti del passaggio.<!--6005561--> Per altre informazioni su ogni controllo, vedere le sezioni specifiche di seguito.

- **Architettura del sistema operativo corrente**
- **Versione minima del sistema operativo**
- **Versione massima del sistema operativo**
- **Versione minima del client**
- **Lingua del sistema operativo corrente**
- **Alimentazione da rete elettrica collegata**
- **Scheda di rete connessa**
  - **La scheda di rete non è wireless**

> [!IMPORTANT]
> Per sfruttare i vantaggi di questa nuova funzionalità di Configuration Manager, dopo l'aggiornamento del sito aggiornare anche i client alla versione più recente. Anche se le nuove funzionalità vengono visualizzate nella console di Configuration Manager quando si esegue l'aggiornamento del sito e della console, lo scenario completo risulta funzionante solo dopo l'aggiornamento alla versione più recente del client.

Il file **smsts.log** include il risultato di tutti i controlli. Se un controllo ha esito negativo, il motore della sequenza di attività continua a valutare gli altri controlli. Il passaggio non risulta non riuscito fino a quando non vengono completati tutti i controlli. Se almeno un controllo ha esito negativo, il passaggio ha esito negativo e restituisce il codice di errore **4316**. Questo codice di errore corrisponde a "La risorsa necessaria per l'operazione specificata non esiste".

### <a name="variables-for-check-readiness"></a>Variabili per Verifica conformità

Usare le variabili della sequenza di attività seguenti con questo passaggio:  

- [_TS_CRMEMORY](task-sequence-variables.md#TSCRMEMORY)
- [_TS_CRSPEED](task-sequence-variables.md#TSCRSPEED)
- [_TS_CRDISK](task-sequence-variables.md#TSCRDISK)
- [_TS_CROSTYPE](task-sequence-variables.md#TSCROSTYPE)
- [_TS_CRARCH](task-sequence-variables.md#TSCRARCH)
- [_TS_CRMINOSVER](task-sequence-variables.md#TSCRMINOSVER)
- [_TS_CRMAXOSVER](task-sequence-variables.md#TSCRMAXOSVER)
- [_TS_CRCLIENTMINVER](task-sequence-variables.md#TSCRCLIENTMINVER)
- [_TS_CROSLANGUAGE](task-sequence-variables.md#TSCROSLANGUAGE)
- [_TS_CRACPOWER](task-sequence-variables.md#TSCRACPOWER)
- [_TS_CRNETWORK](task-sequence-variables.md#TSCRNETWORK)
- [_TS_CRWIRED](task-sequence-variables.md#TSCRWIRED)

### <a name="cmdlets-for-check-readiness"></a>Cmdlet per Verifica conformità

Gestire questo passaggio con i cmdlet di PowerShell seguenti:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepPrestartCheck](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepPrestartCheck?view=sccm-ps)
- [New-CMTSStepPrestartCheck](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepPrestartCheck?view=sccm-ps)
- [Remove-CMTSStepPrestartCheck](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepPrestartCheck?view=sccm-ps)
- [Set-CMTSStepPrestartCheck](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepPrestartCheck?view=sccm-ps)

### <a name="properties-for-check-readiness"></a>Proprietà per Verifica conformità

Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

#### <a name="minimum-memory-mb"></a>Memoria minima (MB)

Verificare che la quantità di memoria in megabyte (MB) sia uguale o superiore alla quantità specificata. Il passaggio abilita questa opzione per impostazione predefinita.  

#### <a name="minimum-processor-speed-mhz"></a>Velocità minima del processore (MHz)  

Verificare che la velocità del processore in megahertz (MHz) sia uguale o superiore al valore specificato. Il passaggio abilita questa opzione per impostazione predefinita.  

#### <a name="minimum-free-disk-space-mb"></a>Spazio disponibile su disco minimo (MB)

Verificare che la quantità di spazio su disco disponibile in megabyte (MB) sia uguale o superiore al valore specificato.  

#### <a name="current-os-to-be-refreshed-is"></a>Il sistema operativo corrente da aggiornare è

Verificare che il sistema operativo installato nel computer client soddisfi i requisiti specificati. Il passaggio imposta questo valore su **CLIENT** per impostazione predefinita.  

#### <a name="architecture-of-current-os"></a>Architettura del sistema operativo corrente

A partire dalla versione 2002, verificare se il sistema operativo corrente è a **32 bit** o a **64 bit**.

#### <a name="minimum-os-version"></a>Versione minima del sistema operativo

A partire dalla versione 2002, verificare che il sistema operativo corrente esegua una versione successiva a quella specificata. Specificare la versione principale, la versione secondaria e il numero di build. Ad esempio, `10.0.16299`

#### <a name="maximum-os-version"></a>Versione massima del sistema operativo

A partire dalla versione 2002, verificare che il sistema operativo corrente esegua una versione precedente a quella specificata. Specificare la versione principale, la versione secondaria e il numero di build. Ad esempio, `10.0.18356`

#### <a name="minimum-client-version"></a>Versione minima del client

A partire dalla versione 2002, verificare che la versione del client Gestione configurazione corrisponda almeno alla versione specificata. Specificare la versione del client nel formato seguente: `5.00.8913.1005`.

#### <a name="language-of-current-os"></a>Lingua del sistema operativo corrente

A partire dalla versione 2002, verificare che la lingua del sistema operativo corrente corrisponda a quella specificata. Selezionare il nome della lingua. Il passaggio confronta il codice lingua associato. Questo controllo confronta la lingua selezionata con la proprietà **OSLanguage** della classe WMI **Win32_OperatingSystem** nel client.

#### <a name="ac-power-plugged-in"></a>Alimentazione da rete elettrica collegata

A partire dalla versione 2002, verificare che il dispositivo sia collegato e non alimentato a batteria.

#### <a name="network-adapter-connected"></a>Scheda di rete connessa

A partire dalla versione 2002, verificare che il dispositivo disponga di una scheda di rete connessa alla rete. Si può anche selezionare il controllo dipendente per verificare che **la scheda di rete non sia wireless**.

### <a name="options-for-check-readiness"></a>Opzioni per Verifica conformità

> [!NOTE]  
> Se si abilita l'impostazione **Continua in caso di errore** della scheda **Opzioni**, il passaggio si limita a registrare i risultati del controllo di conformità. Se un controllo ha esito negativo, la sequenza di attività non viene arrestata.  



## <a name="connect-to-network-folder"></a><a name="BKMK_ConnectToNetworkFolder"></a> Connetti alla cartella di rete

Usare questo passaggio per creare una connessione a una cartella di rete condivisa.  

Questo passaggio della sequenza di attività viene eseguito nel sistema operativo completo o in Windows PE.  

Per aggiungere questo passaggio nell'editor della sequenza di attività, selezionare **Aggiungi**, selezionare **Generale** e quindi selezionare **Connetti alla cartella di rete**.

### <a name="variables-for-connect-to-network-folder"></a>Variabili per Connetti alla cartella di rete

Usare le variabili della sequenza di attività seguenti con questo passaggio:  

- [SMSConnectNetworkFolderAccount](task-sequence-variables.md#SMSConnectNetworkFolderAccount)  
- [SMSConnectNetworkFolderDriveLetter](task-sequence-variables.md#SMSConnectNetworkFolderDriveLetter)  
- [SMSConnectNetworkFolderPassword](task-sequence-variables.md#SMSConnectNetworkFolderPassword)  
- [SMSConnectNetworkFolderPath](task-sequence-variables.md#SMSConnectNetworkFolderPath)  

### <a name="cmdlets-for-connect-to-network-folder"></a>Cmdlet per Connetti alla cartella di rete

Gestire questo passaggio con i cmdlet di PowerShell seguenti:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepConnectNetworkFolder](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConnectNetworkFolder?view=sccm-ps)
- [New-CMTSStepConnectNetworkFolder](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepConnectNetworkFolder?view=sccm-ps)
- [Remove-CMTSStepConnectNetworkFolder](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepConnectNetworkFolder?view=sccm-ps)
- [Set-CMTSStepConnectNetworkFolder](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepConnectNetworkFolder?view=sccm-ps)

### <a name="properties-for-connect-to-network-folder"></a>Proprietà per Connetti alla cartella di rete

Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

#### <a name="path"></a>Percorso  

Selezionare **Sfoglia** per specificare il percorso della cartella di rete. Usare il formato `\\server\share`.

#### <a name="drive"></a>Unità  

Selezionare la lettera dell'unità locale da assegnare per questa connessione.

#### <a name="account"></a>Account

Selezionare **Imposta** per specificare l'account utente con le autorizzazioni per la connessione a questa cartella di rete. Per altre informazioni sull'account di connessione per la cartella di rete della sequenza di attività, vedere [Account](../../core/plan-design/hierarchy/accounts.md#task-sequence-network-folder-connection-account).



## <a name="disable-bitlocker"></a><a name="BKMK_DisableBitLocker"></a> Disattiva BitLocker

Usare questo passaggio per disabilitare la crittografia BitLocker nell'unità del sistema operativo corrente o in un'unità specifica. Questa azione lascia che le protezioni con chiave visibili siano visibili in testo non crittografato nel disco rigido, ma non decrittografa il contenuto dell'unità. Questa azione viene completata quasi istantaneamente.  

> [!NOTE]  
> La crittografia unità BitLocker offre una crittografia di basso livello dei contenuti di un volume del disco.  

Se sono disponibili più unità crittografate, disabilitare BitLocker in qualsiasi unità di dati prima di disabilitare BitLocker nell'unità del sistema operativo.  

Questo passaggio può essere eseguito solo nel sistema operativo completo. Non viene eseguito in Windows PE.  

Per aggiungere questo passaggio nell'editor della sequenza di attività, selezionare **Aggiungi**, selezionare **Dischi** e quindi selezionare **Disattiva BitLocker**.

### <a name="variables-for-disable-bitlocker"></a>Variabili per Disattiva BitLocker

A partire dalla versione 1906, con questo passaggio usare le variabili della sequenza di attività seguenti:  

- [OSDBitLockerRebootCount](task-sequence-variables.md#OSDBitLockerRebootCount)  
- [OSDBitLockerRebootCountOverride](task-sequence-variables.md#OSDBitLockerRebootCountOverride)  

### <a name="cmdlets-for-disable-bitlocker"></a>Cmdlet per Disattiva BitLocker

Gestire questo passaggio con i cmdlet di PowerShell seguenti:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepDisableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepDisableBitLocker?view=sccm-ps)
- [New-CMTSStepDisableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepDisableBitLocker?view=sccm-ps)
- [Remove-CMTSStepDisableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepDisableBitLocker?view=sccm-ps)
- [Set-CMTSStepDisableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepDisableBitLocker?view=sccm-ps)

### <a name="properties-for-disable-bitlocker"></a>Proprietà per Disattiva BitLocker

Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

#### <a name="current-operating-system-drive"></a>Unità del sistema operativo corrente

Disabilita BitLocker nell'unità del sistema operativo corrente.  

#### <a name="specific-drive"></a>Unità specifica  

Disabilita BitLocker in un'unità specifica. Usare l'elenco a discesa per specificare l'unità in cui BitLocker è disabilitato.  

#### <a name="resume-protection-after-windows-has-been-restarted-the-specified-number-of-times"></a>Riprendi la protezione dopo che Windows è stato riavviato per il numero specificato di volte

<!-- 4512937 -->
A partire dalla versione 1906, usare questa opzione per specificare il numero di riavvii per mantenere BitLocker disabilitato. Anziché aggiungere più istanze di questo passaggio, impostare un valore compreso tra 1 (valore predefinito) e 15.

È possibile impostare e modificare questo comportamento con le variabili della sequenza di attività [OSDBitLockerRebootCount](task-sequence-variables.md#OSDBitLockerRebootCount) e [OSDBitLockerRebootCountOverride](task-sequence-variables.md#OSDBitLockerRebootCountOverride).


## <a name="download-package-content"></a><a name="BKMK_DownloadPackageContent"></a> Scarica contenuto pacchetto

Usare questo passaggio per scaricare uno dei tipi di pacchetto seguenti:  

- Immagini dei sistemi operativi  
- Pacchetti di aggiornamento del sistema operativo  
- Pacchetti driver  
- Pacchetti  
- Immagini d'avvio <sup> [Nota 1](#bkmk_note1)</sup>  

Questo passaggio funziona bene in una sequenza di attività per eseguire l'aggiornamento di un sistema operativo negli scenari seguenti:  

- Usare una singola sequenza di attività di aggiornamento che può funzionare con piattaforme x86 e x64. Includere due passaggi **Scarica contenuto pacchetto** nel gruppo **Preparazione dell'aggiornamento**. Specificare nella scheda **Opzioni** le condizioni necessarie per rilevare l'architettura client e scaricare solo il pacchetto di aggiornamento del sistema operativo appropriato. Configurare ogni passaggio **Scarica contenuto pacchetto** in modo che usi la stessa variabile. Usare la variabile per il percorso del supporto nel passaggio **Aggiorna sistema operativo**.  

- Per scaricare in modo dinamico un pacchetto di driver applicabile, usare due passaggi **Scarica contenuto pacchetto** con le condizioni per rilevare il tipo di hardware appropriato per ogni pacchetto driver. Configurare ogni passaggio **Scarica contenuto pacchetto** in modo che usi la stessa variabile. Usare la variabile per il valore **Contenuto preconfigurato** nella sezione Driver del passaggio **Aggiorna sistema operativo**.  

> [!NOTE]  
> Quando si distribuisce una sequenza di attività che contiene questo passaggio, non selezionare **Scaricare tutto il contenuto localmente prima di avviare la sequenza di attività** o **Accedi al contenuto direttamente dl punto di distribuzione** per **Opzioni di distribuzione** nella pagina **Punti di distribuzione** della Distribuzione guidata del software.  

Questo passaggio viene eseguito nel sistema operativo completo o in Windows PE. L'opzione relativa al salvataggio del pacchetto nella cache del client di Configuration Manager non è supportata in Windows PE.

> [!NOTE]  
> L'attività **Scarica contenuto pacchetto** non è supportata per l'uso con supporti autonomi. Per altre informazioni, vedere [Azioni non supportate per i supporti autonomi](../deploy-use/create-stand-alone-media.md#unsupported-actions-for-stand-alone-media).  

Per aggiungere questo passaggio nell'editor della sequenza di attività, selezionare **Aggiungi**, selezionare **Software** e quindi selezionare **Scarica contenuto pacchetto**.

### <a name="cmdlets-for-download-package-content"></a>Cmdlet per Scarica contenuto pacchetto

Gestire questo passaggio con i cmdlet di PowerShell seguenti:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepDownloadPackageContent](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepDownloadPackageContent?view=sccm-ps)
- [New-CMTSStepDownloadPackageContent](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepDownloadPackageContent?view=sccm-ps)
- [Remove-CMTSStepDownloadPackageContent](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepDownloadPackageContent?view=sccm-ps)
- [Set-CMTSStepDownloadPackageContent](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepDownloadPackageContent?view=sccm-ps)

### <a name="properties-for-download-package-content"></a>Proprietà per Scarica contenuto pacchetto

Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

#### <a name="select-package"></a>Selezione pacchetto  

Selezionare l'icona per scegliere il pacchetto da scaricare. Dopo aver scelto un pacchetto, selezionare di nuovo l'icona per scegliere un altro pacchetto.  

#### <a name="place-into-the-following-location"></a>Inserire nel seguente percorso

Scegliere di salvare il pacchetto in una delle posizioni seguenti:  

- **Directory di lavoro della sequenza di attività**: questa posizione è nota anche come cache della sequenza di attività.  

- **Cache del client di Configuration Manager**: usare questa opzione per archiviare il contenuto nella cache del client. Per impostazione predefinita, il percorso è `%WinDir%\ccmcache`.  

- **Percorso personalizzato**: il motore della sequenza di attività scarica prima di tutto il pacchetto nella directory di lavoro della sequenza di attività e quindi lo sposta nel percorso specificato con questa opzione. Il motore di esecuzione della sequenza di attività aggiunge il percorso con l'ID pacchetto.  

#### <a name="save-path-as-a-variable"></a>Salvare il percorso come variabile

Salvare il percorso del pacchetto in una variabile della sequenza di attività personalizzata. Usare quindi questa variabile in un altro passaggio della sequenza di attività.

Configuration Manager aggiunge un suffisso numerico al nome della variabile. Ad esempio, si specifica una variabile `%MyContent%` come variabile personalizzata. È la radice della posizione in cui la sequenza di attività archivia tutto il contenuto a cui si fa riferimento per questo passaggio. Il contenuto può essere costituito da più pacchetti. Quando si fa riferimento alla variabile, aggiungere un suffisso numerico. Per il primo pacchetto, fare riferimento a `%MyContent01%`. Quando si fa riferimento alla variabile in passaggi successivi, ad esempio in **Aggiorna sistema operativo**, usare `%MyContent02%` o `%MyContent03%`, dove il numero corrisponde all'ordine di elenco dei pacchetti nel passaggio **Scarica contenuto pacchetto**.  

#### <a name="if-a-package-download-fails-continue-downloading-other-packages-in-the-list"></a>Se il download di un pacchetto non riesce, continuare a scaricare gli altri pacchetti nell'elenco

Se la sequenza di attività non riesce a scaricare un pacchetto, inizia a scaricare il pacchetto successivo nell'elenco.  

### <a name="note-1-use-of-boot-images-in-the-download-package-content-step"></a><a name="bkmk_note1"></a> Nota 1: Usare le immagini d'avvio nel passaggio Scarica contenuto pacchetto

*Si applica alla versione 1910 e successive*<!-- SCCMDocs-pr #4202 -->

Se si configurano le [proprietà della sequenza di attività](../deploy-use/manage-task-sequences-to-automate-tasks.md#bkmk_prop-advanced) su **Usa un'immagine d'avvio**, l'aggiunta di un'immagine di avvio a questo passaggio è ridondante. Aggiungere un'immagine d'avvio a questo passaggio solo se non è specificata nelle proprietà della sequenza di attività.

#### <a name="example-use-case"></a>Esempio di caso d'uso

- Sequenza di attività singola per il pre-download del contenuto:
  - Nessuna immagine d'avvio associata.
  - Esecuzione solo nel sistema operativo completo, probabilmente senza interazione dell'utente.
  - Uso di più passaggi **Scarica contenuto pacchetto** con condizioni. A seconda della lingua e dell'architettura specifiche, scarica il contenuto nella cache del client in preparazione alla sequenza di attività di distribuzione del sistema operativo.
  - Unica istanza della sequenza di attività, con tutte le opzioni di contenuto possibili.

- Più sequenze di attività di distribuzione del sistema operativo:
  - Una normale sequenza di attività di distribuzione del sistema operativo.
  - Un'immagine di avvio a cui viene fatto riferimento nelle proprietà.
  - Più istanze della sequenza di attività, con immagini di avvio diverse in base alle esigenze di architettura e lingua

## <a name="enable-bitlocker"></a><a name="BKMK_EnableBitLocker"></a> Attiva BitLocker

Usare questo passaggio per attivare la crittografia BitLocker in almeno due partizioni nel disco rigido. La prima partizione attiva include il codice bootstrap di Windows. Un'altra partizione contiene il sistema operativo. La partizione bootstrap deve rimanere non crittografata.  

Usare il passaggio **Pre-provisioning di BitLocker** per abilitare BitLocker in un'unità in Windows PE. Per altre informazioni, vedere [Pre-provisioning di BitLocker](#BKMK_PreProvisionBitLocker).  

> [!NOTE]  
> La crittografia unità BitLocker offre una crittografia di basso livello dei contenuti di un volume del disco.  

Questo passaggio può essere eseguito solo nel sistema operativo completo. Non viene eseguito in Windows PE.

Per aggiungere questo passaggio nell'editor della sequenza di attività, selezionare **Aggiungi**, selezionare **Dischi** e quindi selezionare **Attiva BitLocker**.

Quando si specifica **Solo TPM**, **TPM e chiave di avvio su USB** o **TPM e PIN**, lo stato di TPM (Trusted Platform Module) deve essere il seguente perché sia possibile eseguire il passaggio **Attiva BitLocker**:  

- Abilitato  
- Attivato  
- Proprietà consentita  

Questo passaggio completa le eventuali operazioni rimanenti di inizializzazione TPM. I passaggi rimanenti non richiedono la presenza fisica né operazioni di riavvio. Se necessario, il passaggio**Attiva BitLocker** completa in modo trasparente i passaggi rimanenti dell'inizializzazione TPM seguenti:  

- Creazione della coppia di chiavi di verifica autenticità.  
- Creazione di un valore di autorizzazione del proprietario e del deposito in Active Directory, che deve essere stato esteso per supportare questo valore.  
- Acquisizione della proprietà.  
- Creazione della chiave radice di archiviazione o reimpostazione nel caso in cui la chiave sia già presente ma non sia compatibile.  

Se si vuole che la sequenza di attività attenda il completamento del processo di crittografia unità nel passaggio **Attiva BitLocker**, selezionare l'opzione **Attendi**. Se non si seleziona l'opzione **Attendi** il processo di crittografia unità avviene in background. La sequenza di attività procede immediatamente al passaggio successivo.  

È possibile usare BitLocker per crittografare più unità in un sistema di computer, sia nelle unità del sistema operativo che nelle unità dati. Per crittografare un'unità dati, crittografare in primo luogo l'unità del sistema operativo e completare il processo di crittografia. Questo requisito dipende dal fatto che l'unità del sistema operativo archivia le protezioni con chiave per le unità dati. Se l'unità del sistema operativo e l'unità dati vengono crittografate nella stessa sequenza di attività, selezionare l'opzione **Attendi** nel passaggio **Attiva BitLocker** per l'unità del sistema operativo.  

Se il disco rigido è già crittografato ma BitLocker è disabilitato, il passaggio **Attiva BitLocker** abilita di nuovo le protezioni con chiave e viene completato rapidamente. In questo caso non è necessario ripetere la crittografia del disco rigido.  

### <a name="variables-for-enable-bitlocker"></a>Variabili per Attiva BitLocker

Usare le variabili della sequenza di attività seguenti con questo passaggio:  

- [OSDBitLockerRecoveryPassword](task-sequence-variables.md#OSDBitLockerRecoveryPassword)  
- [OSDBitLockerStartupKey](task-sequence-variables.md#OSDBitLockerStartupKey)  

### <a name="cmdlets-for-enable-bitlocker"></a>Cmdlet per Attiva BitLocker

Gestire questo passaggio con i cmdlet di PowerShell seguenti:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepEnableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepEnableBitLocker?view=sccm-ps)
- [New-CMTSStepEnableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepEnableBitLocker?view=sccm-ps)
- [Remove-CMTSStepEnableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepEnableBitLocker?view=sccm-ps)
- [Set-CMTSStepEnableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepEnableBitLocker?view=sccm-ps)

### <a name="properties-for-enable-bitlocker"></a>Proprietà per Attiva BitLocker

Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

#### <a name="choose-the-drive-to-encrypt"></a>Scegli l'unità da crittografare

Specifica l'unità da crittografare Per crittografare l'unità del sistema operativo corrente, selezionare **Unità del sistema operativo corrente**. Configurare quindi una delle opzioni seguenti per la gestione delle chiavi:  

- **Solo TPM**: Selezionare questa opzione per usare solo Trusted Platform Module (TPM).  

- **Chiave di avvio solo su USB**: Selezionare questa opzione per usare una chiave di avvio archiviata in un'unità flash USB. Quando si seleziona questa opzione, BitLocker blocca il normale processo di avvio fino al collegamento di un dispositivo USB contenente una chiave di avvio BitLocker al computer.  

- **TPM e chiave di avvio su USB**: Selezionare questa opzione per usare TPM e una chiave di avvio archiviata in un'unità flash USB. Quando si seleziona questa opzione, BitLocker blocca il normale processo di avvio fino al collegamento di un dispositivo USB contenente una chiave di avvio BitLocker al computer.  

- **TPM e PIN**: selezionare questa opzione per usare TPM e un codice PIN. Quando si seleziona questa opzione, BitLocker blocca il normale processo di avvio fino a quando l'utente fornisce il codice PIN.  

Per crittografare un'unità dati specifica, non del sistema operativo, selezionare **Unità specifica**. Selezionare quindi l'unità nell'elenco.  

#### <a name="use-full-disk-encryption"></a>Usa la crittografia del disco completo

<!--SCCMDocs-pr issue 2671-->
Per impostazione predefinita, questo passaggio consente di crittografare solo lo spazio usato nell'unità. Questo comportamento predefinito è consigliato perché è più veloce ed efficiente. Se l'organizzazione richiede di crittografare l'intera unità durante l'installazione, abilitare questa opzione. Installazione di Windows attende la crittografia dell'intera unità, operazione che richiede molto tempo soprattutto nelle unità di grandi dimensioni.

> [!TIP]
> A partire dalla versione 1910, è possibile creare e distribuire criteri di gestione di BitLocker, che usano la crittografia *del disco completo*. Per gestire BitLocker nei dispositivi dopo la distribuzione del sistema operativo da parte della sequenza di attività, abilitare questa opzione. Per altre informazioni, vedere [Pianificare la gestione di BitLocker](../../protect/plan-design/bitlocker-management.md).

#### <a name="choose-where-to-create-the-recovery-key"></a>Scegliere dove creare la chiave di ripristino

Per specificare la posizione in cui BitLocker crea la password di ripristino e depositarla in Active Directory, selezionare **In Active Directory**. Questa opzione richiede che si estenda Active Directory per il deposito delle chiavi di BitLocker. In questo modo BitLocker può salvare le informazioni di ripristino associate in Active Directory. Selezionare **Non creare una chiave di ripristino** per non creare una password. La creazione di una password è l'opzione consigliata.  

#### <a name="wait-for-bitlocker-to-complete-the-drive-encryption-process-on-all-drives-before-continuing-task-sequence-execution"></a>Attendi il completamento del processo di crittografia di tutte le unità di BitLocker prima di continuare l'esecuzione della sequenza di attività con Configuration Manager

Selezionare questa opzione per consentire il completamento della crittografia unità BitLocker prima dell'esecuzione del passaggio successivo nella sequenza di attività. Se si seleziona questa opzione, BitLocker esegue la crittografia dell'intero volume del disco prima che l'utente possa accedere al computer.  

In caso di dischi rigidi di grandi dimensioni il processo di crittografia può richiedere diverse ore. Se non si seleziona questa opzione, la sequenza di attività può proseguire immediatamente.  



## <a name="format-and-partition-disk"></a><a name="BKMK_FormatandPartitionDisk"></a> Formato e disco partizione

Usare questo passaggio per formattare e partizionare un disco specificato nel computer di destinazione.  

> [!IMPORTANT]  
> Ogni impostazione specificata per questo passaggio è applicabile a un singolo disco specificato. Per formattare e partizionare un altro disco nel computer di destinazione, aggiungere un altro passaggio **Formato e disco partizione** alla sequenza di attività.  

Questo passaggio può essere eseguito solo in Windows PE. Non viene eseguito nel sistema operativo completo.  

Per aggiungere questo passaggio nell'editor della sequenza di attività, selezionare **Aggiungi**, selezionare **Dischi** e quindi selezionare **Formato e disco partizione**.

### <a name="variables-for-format-and-partition-disk"></a>Variabili per Formato e disco partizione

Usare le variabili della sequenza di attività seguenti con questo passaggio:  

- [OSDDiskIndex](task-sequence-variables.md#OSDDiskIndex)  
- [OSDGPTBootDisk](task-sequence-variables.md#OSDGPTBootDisk)  
- [OSDPartitions](task-sequence-variables.md#OSDPartitions)  
- [OSDPartitionStyle](task-sequence-variables.md#OSDPartitionStyle)  

### <a name="cmdlets-for-format-and-partition-disk"></a>Cmdlet per Formato e disco partizione

Gestire questo passaggio con i cmdlet di PowerShell seguenti:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepPartitionDisk](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtssteppartitiondisk?view=sccm-ps)
- [New-CMTSStepPartitionDisk](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtssteppartitiondisk?view=sccm-ps)
- [Remove-CMTSStepPartitionDisk](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtssteppartitiondisk?view=sccm-ps)
- [Set-CMTSStepPartitionDisk](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtssteppartitiondisk?view=sccm-ps)

### <a name="properties-for-format-and-partition-disk"></a>Proprietà per Formato e disco partizione

Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

#### <a name="disk-number"></a>Numero disco

Numero del disco fisico da formattare. Il numero è basato sull'ordinamento di enumerazione dei dischi Windows.  

#### <a name="disk-type"></a>Tipo di disco

Il tipo del disco da formattare. Nell'elenco a discesa è possibile selezionare le due opzioni seguenti:

- **Standard (MBR)** : record di avvio principale  
- **GPT**: tabella delle partizioni GUID  

> [!NOTE]  
> Se si cambia il tipo di disco da **Standard (MBR)** a **GPT** e il layout della partizione include una partizione estesa, la sequenza di attività rimuove dal layout tutte le partizioni estese e logiche. L'editor della sequenza di attività richiede conferma prima di modificare il tipo di disco.  

#### <a name="volume"></a>Volume

Informazioni specifiche sulla partizione o sul volume creato dalla sequenza di attività, inclusi gli attributi seguenti:  

- Name  
- Spazio su disco rimanente  

Per creare una nuova partizione, selezionare **Nuovo** per aprire la finestra di dialogo **Proprietà della partizione**. Specificare il tipo e la dimensione della partizione e se si tratta di una partizione di avvio. Per modificare una partizione esistente, selezionare la partizione da modificare e quindi selezionare il pulsante **Proprietà**. Per altre informazioni su come configurare le partizioni del disco rigido, vedere uno degli articoli seguenti:  

- [Partizioni in un disco rigido basato su UEFI/GPT](https://docs.microsoft.com/windows-hardware/manufacture/desktop/configure-uefigpt-based-hard-drive-partitions)  
- [Partizioni in un disco rigido basato su BIOS/MBR](https://docs.microsoft.com/windows-hardware/manufacture/desktop/configure-biosmbr-based-hard-drive-partitions)  

Per eliminare una partizione, scegliere la partizione e quindi selezionare **Elimina**.  



## <a name="install-application"></a><a name="BKMK_InstallApplication"></a> Installa applicazione

Questo passaggio consente di installare le applicazioni specificate o un set di applicazioni definito da un elenco dinamico di variabili della sequenza di attività. Quando la sequenza di attività esegue questo passaggio, l'installazione dell'applicazione inizia immediatamente, senza attendere il termine dell'intervallo di polling dei criteri.  

Le applicazioni devono soddisfare i criteri seguenti:  

- L'applicazione deve essere un tipo di distribuzione **Windows Installer** o **Programma di installazione dello script**. Non sono supportati i tipi di distribuzione Pacchetto app Windows (file con estensione appx).  

- Deve essere in esecuzione con l'account di sistema locale e non con l'account utente.  

- Non deve interagire con il desktop. Il programma deve essere eseguito automaticamente o in modalità automatica.  

- Non deve dare inizio autonomamente a un riavvio. L'applicazione deve richiedere un riavvio usando il codice di riavvio standard, ovvero 3010. Questo comportamento garantisce che questo passaggio gestisca correttamente il riavvio. Se l'applicazione restituisce un codice di uscita 3010, il motore della sequenza di attività riavvia il computer. Dopo il riavvio, la sequenza di attività continua automaticamente.  

> [!Note]
> Se l'applicazione [controlla se alcuni file eseguibili sono in esecuzione](../../apps/deploy-use/deploy-applications.md#bkmk_exe-check), la sequenza di attività non riuscirà a installarla. La sequenza di attività verrà eseguita correttamente solo se si configura questo passaggio in modo che continui in caso di errore.

Quando si esegue questo passaggio, l'applicazione verifica l'applicabilità delle regole dei requisiti e del metodo di rilevamento nei tipi di distribuzione dell'applicazione stessa. In base ai risultati di questa verifica, l'applicazione installa il tipo di distribuzione applicabile. Se il tipo di distribuzione contiene dipendenze, il tipo di distribuzione dipendente viene valutato e installato come parte di questo passaggio. Le dipendenze delle applicazioni non sono supportate per i supporti autonomi.  

> [!NOTE]  
> Per installare un'applicazione che sostituisce un'altra applicazione è necessario che i file di contenuto per l'applicazione sostituita siano disponibili. In caso contrario questo passaggio della sequenza di attività ha esito negativo. Ad esempio, Microsoft Visio 2010 viene installato in un client o in un'immagine acquisita. Quando il passaggio **Installa applicazione** installa Microsoft Visio 2013, i file di contenuto per Microsoft Visio 2010 (l'applicazione sostituita) devono essere disponibili in un punto di distribuzione. Se Microsoft Visio non è installato in un client o in un'immagine acquisita, la sequenza di attività installa Microsoft Visio 2013 senza verificare i file di contenuto di Microsoft Visio 2010.  
>
> Se si ritira un'app sostituita e si fa riferimento alla nuova app in una sequenza di attività, quest'ultima non si avvia.
Questo comportamento è previsto dalla progettazione: la sequenza di attività richiede tutti i riferimenti alle app.<!-- SCCMDocs 1711 -->  

Questo passaggio della sequenza di attività viene eseguito solo nel sistema operativo completo. Non viene eseguito in Windows PE.  

Per aggiungere questo passaggio nell'editor della sequenza di attività, selezionare **Aggiungi**, selezionare **Software** e quindi selezionare **Installa applicazione**.

### <a name="variables-for-install-application"></a>Variabili per Installa applicazione

Usare le variabili della sequenza di attività seguenti con questo passaggio:  

- [_TSAppInstallStatus](task-sequence-variables.md#TSAppInstallStatus)  
- [SMSTSMPListRequestTimeoutEnabled](task-sequence-variables.md#SMSTSMPListRequestTimeoutEnabled)  
- [SMSTSMPListRequestTimeout](task-sequence-variables.md#SMSTSMPListRequestTimeout)  
- [TSErrorOnWarning](task-sequence-variables.md#TSErrorOnWarning)  

> [!NOTE]  
> Se il client non riesce a recuperare l'elenco dei punti di gestione dai servizi di posizione, usare le variabili della sequenza di attività **SMSTSMPListRequestTimeoutEnabled** e **SMSTSMPListRequestTimeout**. Queste variabili specificano quanti millisecondi deve attendere una sequenza di attività prima di provare nuovamente a installare un'applicazione. Per altre informazioni, vedere [Variabili della sequenza di attività](task-sequence-variables.md).

### <a name="cmdlets-for-install-application"></a>Cmdlet per Installa applicazione

Gestire questo passaggio con i cmdlet di PowerShell seguenti:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepInstallApplication](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtsstepinstallapplication?view=sccm-ps)
- [New-CMTSStepInstallApplication](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtsstepinstallapplication?view=sccm-ps)
- [Remove-CMTSStepInstallApplication](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtsstepinstallapplication?view=sccm-ps)
- [Set-CMTSStepInstallApplication](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtsstepinstallapplication?view=sccm-ps)

### <a name="properties-for-install-application"></a>Proprietà per Installa applicazione

Nella scheda **Proprietà** per questo passaggio configurare le impostazioni illustrate in questa sezione.  

#### <a name="install-the-following-applications"></a>Installa le seguenti applicazioni

La sequenza di attività installa queste applicazioni nell'ordine specificato.  

Configuration Manager esclude tramite filtro le applicazioni disabilitate o le applicazioni con le impostazioni seguenti:  

- Solo se un utente è connesso  
- Esegui con diritti dell'utente  

Queste applicazioni non vengono visualizzate nella finestra di dialogo **Seleziona l'applicazione da installare**.

#### <a name="install-applications-according-to-dynamic-variable-list"></a>Installa le applicazioni in base all'elenco di variabili dinamiche

La sequenza di attività installa le applicazioni usando questo nome variabile di base. Il nome variabile di base indica un set di variabili della sequenza di attività definite per una raccolta o un computer. Queste variabili specificano le applicazioni che vengono installate dalla sequenza di attività per tale raccolta o computer. Ogni nome di variabile comprende il nome base comune e un suffisso numerico che inizia con 01. Il valore di ogni variabili deve contenere soltanto il nome dell'applicazione.  

Per consentire alla sequenza di attività di installare applicazioni usando un elenco di variabili dinamiche, abilitare l'impostazione seguente nella scheda **Generale** della finestra **Proprietà** dell'applicazione: **Consenti l'installazione dell'applicazione dall'operazione sequenza di attività Installazione applicazione senza distribuzione**.  

> [!NOTE]  
> Non è possibile installare le applicazioni usando un elenco dinamico di variabili per distribuzioni con supporti autonomi.  

Ad esempio, per installare una singola applicazione tramite una variabile della sequenza di attività denominata AA01, specificare la variabile seguente:  

|Nome variabile|Valore variabile|  
|-------------------|--------------------|  
|AA01|Microsoft Office|  

Per installare due applicazioni, specificare le variabili seguenti:  

|Nome variabile|Valore variabile|  
|-------------------|--------------------|  
|AA01|Microsoft Lync|  
|AA02|Microsoft Office|  

Le condizioni seguenti influiscono sulle applicazioni installate dalla sequenza di attività:  

- Se il valore di una variabile include informazioni diverse dal nome dell'applicazione, la sequenza di attività non installa l'applicazione e continua l'esecuzione.  

- Se la sequenza di attività non trova una variabile con il nome di base specificato e il suffisso "01", non installa alcuna applicazione.  

> [!Important]  
> Per questi valori viene fatta distinzione tra maiuscole e minuscole. Ad esempio, "installare" è diverso da "Installare". Se è necessario modificare il valore, l'editor della sequenza di attività non rileva una modifica della combinazione di maiuscole/minuscole. È necessario effettuare un'altra modifica allo stesso tempo, ad esempio, modificare la descrizione del passaggio.<!--509714-->

#### <a name="if-an-application-fails-continue-installing-other-applications-in-the-list"></a>Se l'installazione di un'applicazione non riesce, continuare installando le altre applicazioni dell'elenco

Questa impostazione specifica che il passaggio continua in caso di errore di installazione di una singola applicazione. Se si specifica questa impostazione, la sequenza di attività continua indipendentemente da eventuali errori di installazione. Se non si specifica questa impostazione e l'installazione non riesce, il passaggio termina immediatamente.  

#### <a name="clear-application-content-from-cache-after-installing"></a>Cancella il contenuto dell'applicazione dalla cache dopo l'installazione

<!--4485675-->
A partire dalla versione 1906, eliminare il contenuto dell'app dalla cache del client dopo l'esecuzione del passaggio. Questo comportamento è utile per i dispositivi con unità disco di piccole dimensioni o durante l'installazione di un numero elevato di app di grandi dimensioni in successione.


### <a name="options-for-install-application"></a>Opzioni per Installa applicazione

> [!NOTE]  
> Quando si seleziona **Continua in caso di errore** nella scheda **Opzioni** di questo passaggio, la sequenza di attività continua in caso di errore di installazione di un'applicazione. Quando non si abilita questa opzione, la sequenza di attività ha esito negativo e non installa le applicazioni rimanenti.  

Oltre alle opzioni predefinite, nella scheda **Opzioni** di questo passaggio della sequenza di attività configurare le impostazioni aggiuntive seguenti:  

#### <a name="retry-this-step-if-computer-unexpectedly-restarts"></a>Ripeti passaggio se il computer viene riavviato in modo imprevisto

Se l'installazione di una delle applicazioni riavvia il computer in modo imprevisto, ripetere questo passaggio. Per impostazione predefinita, il passaggio abilita questa impostazione con due tentativi. È possibile specificare da uno a cinque tentativi.  



## <a name="install-package"></a><a name="BKMK_InstallPackage"></a> Installa pacchetto

Usare questo passaggio per installare un pacchetto software come parte della sequenza di attività. Quando si esegue questo passaggio, l'installazione inizia immediatamente, senza attendere un intervallo di polling dei criteri.  

Il pacchetto deve soddisfare i criteri seguenti:  

- Deve essere eseguito con l'account di sistema locale e non con un account utente.  

- Non deve interagire con il desktop. Il programma deve essere eseguito automaticamente o in modalità automatica.  

- Non deve dare inizio autonomamente a un riavvio. Il software deve richiedere un riavvio usando il codice di riavvio standard, ovvero 3010. Questo comportamento garantisce che la sequenza di attività gestisca adeguatamente il riavvio. Se il software restituisce un codice di uscita 3010, il motore della sequenza di attività riavvia il computer. Dopo il riavvio, la sequenza di attività continua automaticamente.  

I programmi che usano l'opzione **Esegui prima un altro programma** per installare un programma dipendente non sono supportati durante la distribuzione di un sistema operativo. Se si abilita l'opzione del pacchetto **Esegui prima un altro programma** e il programma dipendente è già stato eseguito nel computer di destinazione, il programma dipendente viene eseguito e la sequenza di attività continua. Se tuttavia il programma dipendente non è ancora stato eseguito nel computer di destinazione, il passaggio della sequenza di attività ha esito negativo.  

> [!NOTE]  
> Il sito di amministrazione centrale non dispone dei criteri di configurazione client necessari per abilitare l'agente di distribuzione del software durante la sequenza di attività. Quando si creano supporti autonomi per una sequenza di attività in un sito di amministrazione centrale e la sequenza di attività include il passaggio **Installa pacchetto** , è possibile che nel file CreateTsMedia.log venga visualizzato il seguente errore:  
>
> `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`  
>
> Per i supporti autonomi che includono un passaggio **Installa pacchetto**, creare il supporto autonomo in un sito primario nel quale è abilitato l'agente di distribuzione software. In alternativa aggiungere un passaggio **Esegui riga di comando** dopo il passaggio **Imposta Windows e ConfigMgr** e prima del primo passaggio **Installa pacchetto**. Il passaggio **Esegui riga di comando** esegue un comando WMIC per abilitare l'agente di distribuzione software prima del primo passaggio **Installa pacchetto**. Usare il comando seguente nel passaggio **Esegui riga di comando**:  
>
> `WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE`  
>
> Per altre informazioni sulla creazione di supporti autonomi, vedere [Create stand-alone media](../deploy-use/create-stand-alone-media.md) (Creare supporti autonomi).  

Questo passaggio della sequenza di attività viene eseguito solo nel sistema operativo completo. Non viene eseguito in Windows PE.  

Per aggiungere questo passaggio nell'editor della sequenza di attività, selezionare **Aggiungi**, selezionare **Software** e quindi selezionare **Installa pacchetto**.

### <a name="variables-for-install-package"></a>Variabili per Installa pacchetto

Usare le variabili della sequenza di attività seguenti con questo passaggio:  

- [OSDDoNotLogCommand](task-sequence-variables.md#OSDDoNotLogCommand) <!--1358493-->  

### <a name="cmdlets-for-install-package"></a>Cmdlet per Installa pacchetto

Gestire questo passaggio con i cmdlet di PowerShell seguenti:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepInstallSoftware](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtsstepinstallsoftware?view=sccm-ps)
- [New-CMTSStepInstallSoftware](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtsstepinstallsoftware?view=sccm-ps)
- [Remove-CMTSStepInstallSoftware](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtsstepinstallsoftware?view=sccm-ps)
- [Set-CMTSStepInstallSoftware](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtsstepinstallsoftware?view=sccm-ps)

> [!TIP]
> Usare la memorizzazione anticipata del contenuto nella cache per scaricare un pacchetto di aggiornamento del sistema operativo applicabile prima che un utente installi la sequenza di attività. Per altre informazioni, vedere [Configurare la pre-cache del contenuto](../deploy-use/configure-precache-content.md).

### <a name="properties-for-install-package"></a>Proprietà per Installa pacchetto

Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

#### <a name="install-a-single-software-package"></a>Installa un solo pacchetto software

Questa impostazione specifica un pacchetto software di Configuration Manager. Il passaggio attende fino al completamento dell'installazione.  

#### <a name="install-software-packages-according-to-dynamic-variable-list"></a>Installa i pacchetti software in base all'elenco di variabili dinamiche

La sequenza di attività installa i pacchetti usando questo nome variabile di base. Il nome variabile di base indica un set di variabili della sequenza di attività definite per una raccolta o un computer. Queste variabili specificano i pacchetti che vengono installati dalla sequenza di attività per la raccolta o il computer. Ogni nome di variabile comprende il nome base comune e un suffisso numerico che inizia con 001. Il valore di ogni variabile deve includere un ID pacchetto e il nome del software separati da due punti.  

Per consentire alla sequenza di attività di installare un software usando un elenco di variabili dinamiche, abilitare l'impostazione seguente nella scheda **Avanzate** della finestra **Proprietà** del pacchetto: **Consenti l'installazione di questo programma dalla sequenza di attività Installa pacchetto senza che venga distribuito**.  

> [!NOTE]  
> Non è possibile installare pacchetti software usando un elenco dinamico di variabili per distribuzioni con supporti autonomi.  

Ad esempio, per installare un singolo pacchetto software tramite una variabile della sequenza di attività denominata AA001, è necessario specificare la variabile seguente:  

|Nome variabile|Valore variabile|  
|-------------------|--------------------|  
|AA001|CEN00054:Install|  

Per installare tre pacchetti software, è necessario specificare le variabili seguenti:  

|Nome variabile|Valore variabile|  
|-------------------|--------------------|  
|AA001|CEN00054:Install|  
|AA002|CEN00107:Install Silent|  
|AA003|CEN00031:Install|  

Le condizioni seguenti influiscono sui pacchetti installati dalla sequenza di attività:  

- Se il valore di una variabile non viene creato con il formato corretto o se non specifica un ID e un nome del pacchetto validi, l'installazione del software ha esito negativo.  

- Se l'ID del pacchetto include caratteri minuscoli, l'installazione del software ha esito negativo.  

- Se la sequenza di attività non trova una variabile con il nome di base specificato e il suffisso "001" non installa alcun pacchetto. La sequenza di attività continua.  

> [!Important]  
> Per questi valori viene fatta distinzione tra maiuscole e minuscole. Ad esempio, "installare" è diverso da "Installare". Se è necessario modificare il valore, l'editor della sequenza di attività non rileva una modifica della combinazione di maiuscole/minuscole. È necessario effettuare un'altra modifica allo stesso tempo, ad esempio, modificare la descrizione del passaggio.<!--509714-->

#### <a name="if-installation-of-a-software-package-fails-continue-installing-other-packages-in-the-list"></a>Se l'installazione di un pacchetto software non riesce, continuare con l'installazione degli altri pacchetti dell'elenco

Questa impostazione specifica che il passaggio procederà in caso di errore di installazione di un singolo pacchetto software. Se si specifica questa impostazione, la sequenza di attività continua indipendentemente da eventuali errori di installazione. Se non si specifica questa impostazione e l'installazione non riesce, il passaggio termina immediatamente.  



## <a name="install-software-updates"></a><a name="BKMK_InstallSoftwareUpdates"></a> Installa aggiornamenti software

Usare questo passaggio per installare gli aggiornamenti software nel computer di destinazione. Il computer di destinazione viene valutato alla ricerca di aggiornamenti software applicabili solo in corrispondenza con l'esecuzione di questo passaggio della sequenza di attività, quando il computer di destinazione viene valutato per gli aggiornamenti software come qualsiasi altro client gestito da Configuration Manager. Per far sì che questo passaggio installi gli aggiornamenti software, distribuire prima di tutto gli aggiornamenti a una raccolta di cui è membro il computer di destinazione.  

> [!IMPORTANT]  
> Per ottenere prestazioni ottimali, installare la versione più recente dell'agente Windows Update.  

Questo passaggio della sequenza di attività viene eseguito solo nel sistema operativo completo. Non viene eseguito in Windows PE.

Per aggiungere questo passaggio nell'editor della sequenza di attività, selezionare **Aggiungi**, selezionare **Software** e quindi selezionare **Installa aggiornamenti software**.

### <a name="variables-for-install-software-updates"></a>Variabili per Installa aggiornamenti software

Usare le variabili della sequenza di attività seguenti con questo passaggio:  

- [SMSInstallUpdateTarget](task-sequence-variables.md#SMSInstallUpdateTarget)  
- [SMSTSMPListRequestTimeoutEnabled](task-sequence-variables.md#SMSTSMPListRequestTimeoutEnabled)  
- [SMSTSMPListRequestTimeout](task-sequence-variables.md#SMSTSMPListRequestTimeout)  
- [SMSTSSoftwareUpdateScanTimeout](task-sequence-variables.md#SMSTSSoftwareUpdateScanTimeout)  
- [SMSTSWaitForSecondReboot](task-sequence-variables.md#SMSTSWaitForSecondReboot)  

> [!NOTE]  
> Se il client non riesce a recuperare l'elenco dei punti di gestione dai servizi di posizione, usare le variabili **SMSTSMPListRequestTimeoutEnabled** e **SMSTSMPListRequestTimeout**. Queste variabili specificano quanti millisecondi deve attendere una sequenza di attività prima di provare nuovamente a installare un'applicazione o un aggiornamento del software. Per altre informazioni, vedere [Variabili della sequenza di attività](task-sequence-variables.md).  

### <a name="cmdlets-for-install-software-updates"></a>Cmdlet per Installa aggiornamenti software

Gestire questo passaggio con i cmdlet di PowerShell seguenti:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepInstallUpdate](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtsstepinstallupdate?view=sccm-ps)
- [New-CMTSStepInstallUpdate](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtsstepinstallupdate?view=sccm-ps)
- [Remove-CMTSStepInstallUpdate](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtsstepinstallupdate?view=sccm-ps)
- [Set-CMTSStepInstallUpdate](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtsstepinstallupdate?view=sccm-ps)

Per altre indicazioni e un diagramma di flusso tecnico per questo passaggio, vedere [Installa aggiornamenti software](install-software-updates.md).

### <a name="properties-for-install-software-updates"></a>Proprietà per Installa aggiornamenti software

Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

#### <a name="required-for-installation---mandatory-software-updates-only"></a>Necessario per l'installazione - Solo aggiornamenti software obbligatori

Selezionare questa opzione per installare tutti gli aggiornamenti software obbligatori, con date di installazione definite dall'amministratore.  

#### <a name="available-for-installation---all-software-updates"></a>Disponibile per l'installazione - Tutti gli aggiornamenti software

Selezionare questa opzione per installare tutti gli aggiornamenti software disponibili. Distribuire prima di tutto questi aggiornamenti in una raccolta di cui il computer è membro. La sequenza di attività installa tutti gli aggiornamenti software disponibili nei computer di destinazione.  

#### <a name="evaluate-software-updates-from-cached-scan-results"></a>Valuta gli aggiornamenti software dai risultati di analisi memorizzati nella cache

Per impostazione predefinita, questo passaggio usa i risultati di analisi memorizzati nella cache dall'agente Windows Update. Disabilitare questa opzione per indicare all'agente Windows Update di scaricare il catalogo più recente dal punto di aggiornamento software. Abilitare questa opzione quando si usa una sequenza di attività per [acquisire e compilare un'immagine del sistema operativo](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md). In questo scenario è probabile che si presenti numero elevato di aggiornamenti software.

Molti di questi aggiornamenti hanno dipendenze. Ad esempio, viene visualizzata l'indicazione di installare l'aggiornamento ABC prima dell'aggiornamento XYZ, a seconda dei casi. Se si disabilita questa impostazione e si distribuisce la sequenza di attività a molti client, tutti i client si connettono contemporaneamente al punto di aggiornamento software. Questo comportamento causa problemi di prestazioni durante il processo e il download del catalogo degli aggiornamenti.

Nella maggior parte dei casi, usare l'impostazione predefinita per usare i risultati di analisi memorizzati nella cache.

La variabile **SMSTSSoftwareUpdateScanTimeout** controlla il timeout dell'analisi degli aggiornamenti software durante questo passaggio. Il valore predefinito è 60 minuti. Per altre informazioni, vedere [Variabili della sequenza di attività](task-sequence-variables.md#SMSTSSoftwareUpdateScanTimeout).

### <a name="options-for-install-software-updates"></a>Opzioni per Installa aggiornamenti software

Oltre alle opzioni predefinite, nella scheda **Opzioni** di questo passaggio della sequenza di attività configurare le impostazioni aggiuntive seguenti:  

#### <a name="retry-this-step-if-computer-unexpectedly-restarts"></a>Ripeti passaggio se il computer viene riavviato in modo imprevisto

Se uno degli aggiornamenti riavvia il computer in modo imprevisto, ripetere questo passaggio. Per impostazione predefinita, il passaggio abilita questa impostazione con due tentativi. È possibile specificare da uno a cinque tentativi.  

> [!NOTE]  
> Configurare la variabile **SMSTSWaitForSecondReboot** per specificare i secondi di sospensione della sequenza di attività dopo il riavvio del computer in questo scenario. Per altre informazioni, vedere [Variabili della sequenza di attività](task-sequence-variables.md#SMSTSWaitForSecondReboot).  



## <a name="join-domain-or-workgroup"></a><a name="BKMK_JoinDomainorWorkgroup"></a> Aggiunta a dominio o gruppo di lavoro

Usare questo passaggio per aggiungere il computer di destinazione a un dominio o un gruppo di lavoro.  

Questo passaggio della sequenza di attività viene eseguito solo nel sistema operativo completo. Non viene eseguito in Windows PE.

Per aggiungere questo passaggio nell'editor della sequenza di attività, selezionare **Aggiungi**, selezionare **Generale** e quindi selezionare **Aggiunta a dominio o gruppo di lavoro**.

### <a name="variables-for-join-domain-or-workgroup"></a>Variabili per Aggiunta a dominio o gruppo di lavoro

Usare le variabili della sequenza di attività seguenti con questo passaggio:  

- [OSDJoinAccount](task-sequence-variables.md#OSDJoinAccount)  
- [OSDJoinDomainName](task-sequence-variables.md#OSDJoinDomainName)  
- [OSDJoinDomainOUName](task-sequence-variables.md#OSDJoinDomainOUName)  
- [OSDJoinPassword](task-sequence-variables.md#OSDJoinPassword)  
- [OSDJoinSkipReboot](task-sequence-variables.md#OSDJoinSkipReboot)  
- [OSDJoinType](task-sequence-variables.md#OSDJoinType)  
- [OSDJoinWorkgroupName](task-sequence-variables.md#OSDJoinWorkgroupName)  

### <a name="cmdlets-for-join-domain-or-workgroup"></a>Cmdlet per Aggiunta a dominio o gruppo di lavoro

Gestire questo passaggio con i cmdlet di PowerShell seguenti:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepJoinDomainWorkgroup](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepJoinDomainWorkgroup?view=sccm-ps)
- [New-CMTSStepJoinDomainWorkgroup](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepJoinDomainWorkgroup?view=sccm-ps)
- [Remove-CMTSStepJoinDomainWorkgroup](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepJoinDomainWorkgroup?view=sccm-ps)
- [Set-CMTSStepJoinDomainWorkgroup](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepJoinDomainWorkgroup?view=sccm-ps)

### <a name="properties-for-join-domain-or-workgroup"></a>Proprietà per Aggiunta a dominio o gruppo di lavoro

Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

#### <a name="join-a-workgroup"></a>Aggiunta a un gruppo di lavoro

Selezionare questa opzione per aggiungere il computer di destinazione al gruppo di lavoro specificato. Se il computer è attualmente membro di un dominio, la selezione di questa opzione determina il riavvio del computer.  

#### <a name="join-a-domain"></a>Aggiunta a un dominio

Selezionare questa opzione per aggiungere il computer di destinazione al dominio specificato.  

Facoltativamente, immettere o selezionare un'unità organizzativa nel dominio specificato a cui aggiungere il computer. Se il computer è attualmente membro di un altro dominio o un altro gruppo di lavoro, questa opzione determina il riavvio del computer. Se il computer è già membro di un'altra unità organizzativa, dato che Active Directory Domain Services non consente la modifica dell'unità organizzativa con questo metodo, l'installazione di Windows ignora l'impostazione.  

#### <a name="enter-the-account-which-has-permission-to-join-the-domain"></a>Immettere l'account con le autorizzazioni per l'aggiunta al dominio

Selezionare **Imposta** per immettere il nome utente e la password di un account con autorizzazioni per l'aggiunta al dominio. Immettere l'account nel formato: `Domain\account`. Per altre informazioni sull'account di aggiunta del dominio della sequenza di attività, vedere [Account](../../core/plan-design/hierarchy/accounts.md#task-sequence-domain-join-account).  



## <a name="prepare-configmgr-client-for-capture"></a><a name="BKMK_PrepareConfigMgrClientforCapture"></a> Prepara client ConfigMgr per l'acquisizione

Usare questo passaggio per rimuovere o configurare il client di Configuration Manager nel computer di riferimento. Questa azione prepara il computer per l'acquisizione come parte del processo di creazione immagine.

Questo passaggio rimuove completamente il client di Configuration Manager, invece di rimuovere solo le informazioni sulla chiave. Quando la sequenza di attività distribuisce l'immagine del sistema operativo acquisita, installa ogni volta un nuovo client di Configuration Manager.  

> [!Note]  
> Il motore di esecuzione della sequenza di attività rimuove il client solo durante la sequenza di attività **Crea e acquisisci un'immagine del sistema operativo di riferimento**. Il motore di esecuzione della sequenza di attività non rimuove il client durante l'esecuzione di altri metodi di acquisizione, quali Acquisisci supporto o una sequenza di attività personalizzata.  

Questo passaggio della sequenza di attività viene eseguito solo nel sistema operativo completo. Non viene eseguito in Windows PE.  

Per aggiungere questo passaggio nell'editor della sequenza di attività, selezionare **Aggiungi**, selezionare **Immagini** e quindi selezionare **Prepara client ConfigMgr per l'acquisizione**.

### <a name="cmdlets-for-prepare-configmgr-client-for-capture"></a>Cmdlet per Prepara client ConfigMgr per l'acquisizione

Gestire questo passaggio con i cmdlet di PowerShell seguenti:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepPrepareConfigMgrClient](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepPrepareConfigMgrClient?view=sccm-ps)
- [New-CMTSStepPrepareConfigMgrClient](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepPrepareConfigMgrClient?view=sccm-ps)
- [Remove-CMTSStepPrepareConfigMgrClient](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepPrepareConfigMgrClient?view=sccm-ps)
- [Set-CMTSStepPrepareConfigMgrClient](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepPrepareConfigMgrClient?view=sccm-ps)



## <a name="prepare-windows-for-capture"></a><a name="BKMK_PrepareWindowsforCapture"></a> Prepara Windows per l'acquisizione

Usare questo passaggio per specificare le opzioni di Sysprep per l'acquisizione di un'immagine del sistema operativo nel computer di riferimento. Questo passaggio esegue Sysprep e quindi riavvia il computer nell'immagine di avvio di Windows PE specificata per la sequenza di attività. Questa operazione non riesce se il computer di riferimento fa parte di un dominio.  

Questo passaggio può essere eseguito solo nel sistema operativo completo. Non viene eseguito in Windows PE.

Per aggiungere questo passaggio nell'editor della sequenza di attività, selezionare **Aggiungi**, selezionare **Immagini** e quindi selezionare **Prepara Windows per l'acquisizione**.

### <a name="variables-for-prepare-windows-for-capture"></a>Variabili per Prepara Windows per l'acquisizione

Usare le variabili della sequenza di attività seguenti con questo passaggio:  

- [OSDKeepActivation](task-sequence-variables.md#OSDKeepActivation)  
- [OSDTargetSystemRoot](task-sequence-variables.md#OSDTargetSystemRoot-output)  

### <a name="cmdlets-for-prepare-windows-for-capture"></a>Cmdlet per Prepara Windows per l'acquisizione

Gestire questo passaggio con i cmdlet di PowerShell seguenti:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepPrepareWindows](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepPrepareWindows?view=sccm-ps)
- [New-CMTSStepPrepareWindows](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepPrepareWindows?view=sccm-ps)
- [Remove-CMTSStepPrepareWindows](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepPrepareWindows?view=sccm-ps)
- [Set-CMTSStepPrepareWindows](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepPrepareWindows?view=sccm-ps)

### <a name="properties-for-prepare-windows-for-capture"></a>Proprietà per Prepara Windows per l'acquisizione

Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

#### <a name="automatically-build-mass-storage-driver-list"></a>Crea automaticamente l'elenco di driver di archiviazione di massa

Selezionare questa opzione per fare in modo che Sysprep crei automaticamente un elenco di driver di archiviazione di massa dal computer di riferimento. Questa opzione abilita l'opzione per la creazione di driver di archiviazione di massa del file sysprep.inf nel computer di riferimento. Per altre informazioni su questa impostazione, vedere la documentazione di Sysprep.  

#### <a name="do-not-reset-activation-flag"></a>Non reimpostare il flag di attivazione

Selezionare questa opzione per impedire a Sysprep di reimpostare il flag di attivazione del prodotto.  

#### <a name="shutdown-the-computer-after-running-this-action"></a>Arresta il computer dopo l'esecuzione di questa azione

<!--SCCMDocs-pr issue 2695-->
Questa opzione indica a Sysprep di arrestare il computer in sostituzione del comportamento di riavvio predefinito.

La sequenza di attività [Windows Autopilot per dispositivi esistenti](../deploy-use/windows-autopilot-for-existing-devices.md) usa questo passaggio con questa opzione.

- Se si vuole che la sequenza di attività aggiorni il dispositivo e quindi avvii immediatamente la Configurazione guidata per Autopilot, lasciare deselezionata questa opzione.  

- Abilitare questa opzione per arrestare il dispositivo dopo la creazione dell'immagine. È quindi possibile distribuire il dispositivo a un utente, che avvia la Configurazione guidata con Autopilot alla prima accensione.  



## <a name="pre-provision-bitlocker"></a><a name="BKMK_PreProvisionBitLocker"></a> Eseguire il pre-provisioning di BitLocker

Usare questo passaggio per attivare BitLocker in un'unità mentre si trova in Windows PE. Per impostazione predefinita, viene crittografato solo lo spazio su disco usato e pertanto i tempi di crittografia sono molto più veloci. È possibile applicare le opzioni di gestione delle chiavi usando il passaggio [Attiva BitLocker](#BKMK_EnableBitLocker) dopo l'installazione del sistema operativo.

> [!IMPORTANT]
> Per effettuare il pre-provisioning di BitLocker è necessario che il computer disponga di un Trusted Platform Module (TPM) supportato e abilitato.

Questo passaggio può essere eseguito solo in Windows PE. Non viene eseguito nel sistema operativo completo.  

Per aggiungere questo passaggio nell'editor della sequenza di attività, selezionare **Aggiungi**, selezionare **Dischi** e quindi selezionare **Pre-provisioning di BitLocker**.

### <a name="cmdlets-for-pre-provision-bitlocker"></a>Cmdlet per Pre-provisioning di BitLocker

Gestire questo passaggio con i cmdlet di PowerShell seguenti:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepOfflineEnableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepOfflineEnableBitLocker?view=sccm-ps)
- [New-CMTSStepOfflineEnableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepOfflineEnableBitLocker?view=sccm-ps)
- [Remove-CMTSStepOfflineEnableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepOfflineEnableBitLocker?view=sccm-ps)
- [Set-CMTSStepOfflineEnableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepOfflineEnableBitLocker?view=sccm-ps)

### <a name="properties-for-pre-provision-bitlocker"></a>Proprietà per Pre-provisioning di BitLocker

Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

#### <a name="apply-bitlocker-to-the-specified-drive"></a>Applica BitLocker all'unità specificata

Specificare l'unità per cui si vuole abilitare BitLocker. BitLocker consente di crittografare solo lo spazio usato nell'unità.  

#### <a name="use-full-disk-encryption"></a>Usa la crittografia del disco completo

<!--SCCMDocs-pr issue 2671-->
Per impostazione predefinita, questo passaggio consente di crittografare solo lo spazio usato nell'unità. Questo comportamento predefinito è consigliato perché è più veloce ed efficiente. Se l'organizzazione richiede di crittografare l'intera unità durante l'installazione, abilitare questa opzione. Installazione di Windows attende la crittografia dell'intera unità, operazione che richiede molto tempo soprattutto nelle unità di grandi dimensioni.

#### <a name="skip-this-step-for-computers-that-do-not-have-a-tpm-or-when-tpm-is-not-enabled"></a>Ignora questo passaggio per computer senza TPM o con TPM non abilitato

Selezionare questa opzione per ignorare la crittografia delle unità in un computer che non contiene un modulo TPM supportato o abilitato. Ad esempio, usare questa opzione quando si distribuisce un sistema operativo in una macchina virtuale.  



## <a name="release-state-store"></a><a name="BKMK_ReleaseStateStore"></a> Rilascia archiviazione stati

Usare questo passaggio per notificare al punto di migrazione stato il completamento dell'azione di acquisizione o ripristino. Usare questo passaggio insieme ai passaggi **Richiedi archiviazione stati**, **Acquisisci stato utente** e **Ripristina stato utente**. Usare questi passaggi per eseguire la migrazione di dati dello stato utente mediante un punto di migrazione stato e l'Utilità di migrazione stato utente (USMT).  

Per altre informazioni sulla gestione dello stato utente durante la distribuzione di sistemi operativi, vedere [Manage user state](../get-started/manage-user-state.md) (Gestire lo stato utente).  

Se si usa il passaggio **Richiedi archiviazione stati** per richiedere l'accesso a un punto di migrazione per *acquisire* lo stato utente, questo passaggio segnala al punto di migrazione stato che il processo di acquisizione è stato completato. Quindi il punto di migrazione stato contrassegna i dati dello stato utente come disponibili per il ripristino. Il punto di migrazione stato imposta le autorizzazioni di controllo dell'accesso per i dati dello stato utente, in modo che solo il computer di ripristino disponga di accesso di sola lettura.  

Se si usa il passaggio **Richiedi archiviazione stati** per richiedere l'accesso a un punto di migrazione per *ripristinare* lo stato utente, questo passaggio segnala al punto di migrazione stato che il processo di ripristino è stato completato. Quindi il punto di migrazione stato attiva le proprie impostazioni di memorizzazione dati configurate.  

> [!IMPORTANT]  
> Impostare l'opzione **Continua in caso di errori** per tutti i passaggi inclusi tra il passaggio **Richiedi archiviazione stati** e il passaggio **Rilascia archiviazione stati**. Per ogni passaggio **Richiedi archiviazione stati** deve essere presente un passaggio **Rilascia archiviazione stati**.  

Questo passaggio può essere eseguito solo nel sistema operativo completo. Non viene eseguito in Windows PE.

Per aggiungere questo passaggio nell'editor della sequenza di attività, selezionare **Aggiungi**, selezionare **Stato utente** e quindi selezionare **Rilascia archiviazione stati**.

### <a name="variables-for-release-state-store"></a>Variabili per Rilascia archiviazione stati

Usare le variabili della sequenza di attività seguenti con questo passaggio:  

- [OSDStateStorePath](task-sequence-variables.md#OSDStateStorePath)  

### <a name="cmdlets-for-release-state-store"></a>Cmdlet per Rilascia archiviazione stati

Gestire questo passaggio con i cmdlet di PowerShell seguenti:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepReleaseStateStore](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepReleaseStateStore?view=sccm-ps)
- [New-CMTSStepReleaseStateStore](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepReleaseStateStore?view=sccm-ps)
- [Remove-CMTSStepReleaseStateStore](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepReleaseStateStore?view=sccm-ps)
- [Set-CMTSStepReleaseStateStore](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepReleaseStateStore?view=sccm-ps)

### <a name="properties-for-release-state-store"></a>Proprietà per Rilascia archiviazione stati

Questo passaggio non richiede alcuna impostazione nella scheda **Proprietà**.



## <a name="request-state-store"></a><a name="BKMK_RequestStateStore"></a> Richiedi archiviazione stati

Usare questo passaggio per richiedere l'accesso a un punto di migrazione stato durante l'acquisizione o il ripristino dello stato.  

Per altre informazioni sulla gestione dello stato utente durante la distribuzione di sistemi operativi, vedere [Manage user state](../get-started/manage-user-state.md) (Gestire lo stato utente).  

Usare questo passaggio insieme ai passaggi **Rilascia archiviazione stati**, **Acquisisci stato utente** e **Ripristina stato utente**. Usare questi passaggi per eseguire la migrazione dello stato del computer mediante un punto di migrazione stato e l'Utilità di migrazione stato utente (USMT).  

> [!NOTE]  
> Dopo la creazione di un nuovo punto di migrazione stato, l'archiviazione dello stato utente non è disponibile per un tempo massimo pari a un'ora. Per attivare più rapidamente la disponibilità, modificare le impostazioni delle proprietà del punto di migrazione stato in modo da attivare un aggiornamento del file di controllo del sito.  

Questo passaggio viene eseguito nel sistema operativo completo e in Windows PE per USMT offline.

Per aggiungere questo passaggio nell'editor della sequenza di attività, selezionare **Aggiungi**, selezionare **Stato utente** e quindi selezionare **Richiedi archiviazione stati**.

### <a name="variables-for-request-state-store"></a>Variabili per Richiedi archiviazione stati

Usare le variabili della sequenza di attività seguenti con questo passaggio:  

- [OSDStateFallbackToNAA](task-sequence-variables.md#OSDStateFallbackToNAA)  
- [OSDStateSMPRetryCount](task-sequence-variables.md#OSDStateSMPRetryCount)  
- [OSDStateSMPRetryTime](task-sequence-variables.md#OSDStateSMPRetryTime)  
- [OSDStateStorePath](task-sequence-variables.md#OSDStateStorePath)  

### <a name="cmdlets-for-request-state-store"></a>Cmdlet per Richiedi archiviazione stati

Gestire questo passaggio con i cmdlet di PowerShell seguenti:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepRequestStateStore](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepRequestStateStore?view=sccm-ps)
- [New-CMTSStepRequestStateStore](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepRequestStateStore?view=sccm-ps)
- [Remove-CMTSStepRequestStateStore](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepRequestStateStore?view=sccm-ps)
- [Set-CMTSStepRequestStateStore](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepRequestStateStore?view=sccm-ps)

### <a name="properties-for-request-state-store"></a>Proprietà per Richiedi archiviazione stati

Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

#### <a name="capture-state-from-the-computer"></a>Acquisisci stato dal computer

Trovare un punto di migrazione stato che soddisfi i requisiti minimi definiti nelle impostazioni del punto di migrazione stato. Ad esempio **Numero massimo di client** e **Minimum amount of free disk space** (Quantità minima di spazio libero su disco). Questa opzione non garantisce che al momento della migrazione dello stato sia disponibile spazio su disco sufficiente. L'opzione richiede l'accesso al punto di migrazione stato per l'acquisizione dello stato utente e delle impostazioni da un computer.  

Se il sito di Configuration Manager dispone di più punti di migrazione stato attivi, questo passaggio consente di trovare un punto di migrazione stato con spazio su disco disponibile. La sequenza di attività definisce un elenco di punti di migrazione stato nel punto di gestione, quindi valuta ogni punto di migrazione finché non ne rileva uno che soddisfa i requisiti minimi.  

#### <a name="restore-state-from-another-computer"></a>Ripristina stato da un altro computer

Richiedere l'accesso a un punto di migrazione stato per ripristinare le impostazioni e lo stato utente acquisiti in precedenza in un computer di destinazione.  

Se sono presenti più punti di migrazione stato, questo passaggio individua il punto di migrazione stato che dispone dello stato per il computer di destinazione.  

#### <a name="number-of-retries"></a>Numero di tentativi

Numero di tentativi effettuati da questo passaggio per trovare un punto di migrazione stato appropriato prima di restituire un esito negativo.  

#### <a name="retry-delay-in-seconds"></a>Intervallo tra tentativi (in secondi)

Quantità di tempo, in secondi, di attesa da parte del passaggio della sequenza di attività prima di effettuare nuovi tentativi.  

#### <a name="if-computer-account-fails-to-connect-to-a-state-store-use-the-network-access-account"></a>Se l'account del computer non riesce a connettersi all'archiviazione stati, utilizzare l'account di accesso di rete

Se la sequenza di attività non può accedere al punto di migrazione stato tramite l'account del computer, esegue la connessione con le credenziali dell'account di accesso di rete. Questa opzione è meno sicura perché è possibile che altri computer usino l'account di accesso di rete per accedere allo stato archiviato. L'opzione potrebbe essere necessaria se il computer di destinazione non è aggiunto a un dominio.  



## <a name="restart-computer"></a><a name="BKMK_RestartComputer"></a> Riavvia computer

Usare questo passaggio per riavviare il computer che esegue la sequenza di attività. Dopo il riavvio il computer continua automaticamente con il passaggio successivo della sequenza di attività.  

Questo passaggio può essere eseguito nel sistema operativo completo o in Windows PE.

Per aggiungere questo passaggio nell'editor della sequenza di attività, selezionare **Aggiungi**, selezionare **Generale** e quindi selezionare **Riavvia computer**.

### <a name="variables-for-restart-computer"></a>Variabili per Riavvia computer

Usare le variabili della sequenza di attività seguenti con questo passaggio:  

- [SMSRebootMessage](task-sequence-variables.md#SMSRebootMessage)  
- [SMSRebootTimeout](task-sequence-variables.md#SMSRebootTimeout)  

### <a name="cmdlets-for-restart-computer"></a>Cmdlet per Riavvia computer

Gestire questo passaggio con i cmdlet di PowerShell seguenti:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepReboot](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtsstepreboot?view=sccm-ps)
- [New-CMTSStepReboot](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtsstepreboot?view=sccm-ps)
- [Remove-CMTSStepReboot](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtsstepreboot?view=sccm-ps)
- [Set-CMTSStepReboot](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtsstepreboot?view=sccm-ps)

### <a name="properties-for-restart-computer"></a>Proprietà per Riavvia computer

Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

#### <a name="the-boot-image-assigned-to-this-task-sequence"></a>L'immagine di avvio assegnata a questa sequenza di attività

Selezionare questa opzione per far sì che il computer di destinazione usi l'immagine di avvio assegnata alla sequenza di attività. La sequenza di attività usa l'immagine di avvio per eseguire i passaggi successivi in Windows PE.  

#### <a name="the-currently-installed-default-operating-system"></a>Il sistema operativo predefinito attualmente installato

Selezionare questa opzione per il computer di destinazione per il riavvio nel sistema operativo installato.  

#### <a name="notify-the-user-before-restarting"></a>Invia notifica all'utente prima del riavvio

Selezionare questa opzione per visualizzare una notifica all'utente prima del riavvio del computer di destinazione. Il passaggio seleziona questa opzione per impostazione predefinita.  

#### <a name="notification-message"></a>Messaggio di notifica

Immettere un messaggio di notifica da visualizzare all'utente prima del riavvio del computer di destinazione.  

#### <a name="message-display-time-out"></a>Timeout della visualizzazione messaggio

Specificare la quantità di tempo in secondi prima del riavvio del computer di destinazione. Il valore predefinito è 60 secondi.  



## <a name="restore-user-state"></a><a name="BKMK_RestoreUserState"></a> Ripristina stato utente

Usare questo passaggio per avviare l'Utilità di migrazione stato utente (USMT) e ripristinare lo stato utente e le impostazioni nel computer di destinazione. Usare questo passaggio in combinazione con il passaggio **Acquisisci stato utente**.  

Per altre informazioni sulla gestione dello stato utente durante la distribuzione di sistemi operativi, vedere [Manage user state](../get-started/manage-user-state.md) (Gestire lo stato utente).  

Usare questo passaggio con i passaggi **Richiedi archiviazione stati** e **Rilascia archiviazione stati** per salvare o ripristinare le impostazioni dello stato con un punto di migrazione stato. Questa opzione decrittografa sempre l'archivio degli stati USMT usando una chiave di crittografia generata e gestita da Configuration Manager.  

Il passaggio **Ripristina stato utente** consente il controllo di un sottoinsieme limitato delle opzioni USMT più usate. Specificare opzioni della riga di comando aggiuntive con la variabile **OSDMigrateAdditionalRestoreOptions**.  

> [!IMPORTANT]  
> Se si usa questo passaggio per uno scopo non associato a uno scenario di distribuzione del sistema operativo, aggiungere il passaggio [Riavvia computer](#BKMK_RestartComputer) subito dopo il passaggio **Ripristina stato utente**.  

Questo passaggio può essere eseguito solo nel sistema operativo completo. Non viene eseguito in Windows PE.

Per aggiungere questo passaggio nell'editor della sequenza di attività, selezionare **Aggiungi**, selezionare **Stato utente** e quindi selezionare **Ripristina stato utente**.

### <a name="variables-for-restore-user-state"></a>Variabili per Ripristina stato utente

Usare le variabili della sequenza di attività seguenti con questo passaggio:  

- [_OSDMigrateUsmtRestorePackageID](task-sequence-variables.md#OSDMigrateUsmtRestorePackageID)  
- [OSDMigrateAdditionalRestoreOptions](task-sequence-variables.md#OSDMigrateAdditionalRestoreOptions)  
- [OSDMigrateContinueOnRestore](task-sequence-variables.md#OSDMigrateContinueOnRestore)  
- [OSDMigrateEnableVerboseLogging](task-sequence-variables.md#OSDMigrateEnableVerboseLogging)  
- [OSDMigrateLocalAccounts](task-sequence-variables.md#OSDMigrateLocalAccounts)  
- [OSDMigrateLocalAccountPassword](task-sequence-variables.md#OSDMigrateLocalAccountPassword)  
- [OSDStateStorePath](task-sequence-variables.md#OSDStateStorePath)  

### <a name="cmdlets-for-restore-user-state"></a>Cmdlet per Ripristina stato utente

Gestire questo passaggio con i cmdlet di PowerShell seguenti:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepRestoreUserState](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepRestoreUserState?view=sccm-ps)
- [New-CMTSStepRestoreUserState](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepRestoreUserState?view=sccm-ps)
- [Remove-CMTSStepRestoreUserState](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepRestoreUserState?view=sccm-ps)
- [Set-CMTSStepRestoreUserState](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepRestoreUserState?view=sccm-ps)

### <a name="properties-for-restore-user-state"></a>Proprietà per Ripristina stato utente

Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

#### <a name="user-state-migration-tool-package"></a>Pacchetto degli strumenti di migrazione dello stato utente

Specificare il pacchetto contenente la versione di USMT che verrà usata in questo passaggio. Questo pacchetto non richiede un programma. Quando viene eseguito il passaggio la sequenza di attività usa la versione di USMT del pacchetto specificato. Specificare un pacchetto contenente la versione di USMT a 32 bit o a 64 bit. L'architettura di USMT dipende dall'architettura del sistema operativo nel quale la sequenza di attività ripristina lo stato.

#### <a name="restore-all-captured-user-profiles-with-standard-options"></a>Ripristina tutti i profili utente acquisiti con le opzioni standard

Ripristina i profili utente acquisiti con le opzioni standard. Per personalizzare le opzioni ripristinate da USMT, selezionare **Customize user profile capture** (Personalizza acquisizione dei profili utente).  

#### <a name="customize-how-user-profiles-are-restored"></a>Personalizza le modalità di ripristino dei profili utente

Permette di personalizzare i file da ripristinare nel computer di destinazione. Selezionare **File** per specificare i file di configurazione nel pacchetto USMT da usare per il ripristino dei profili utente. Per aggiungere un file di configurazione, immettere il nome del file nella casella **Nome file** e quindi selezionare **Aggiungi**. Nel riquadro File sono elencati i file di configurazione usati da USMT. Il file con estensione xml specificato definisce il file utente che viene ripristinato da USMT.  

#### <a name="restore-local-computer-user-profiles"></a>Ripristina profili utente del computer locale

Ripristina i profili utente del computer locale. Questi profili non sono disponibili per gli utenti di dominio. Assegnare nuove password agli account utente locali ripristinati. USMT non esegue la migrazione delle password originali. Immettere la nuova password nella casella **Password** e confermare la password nella casella **Conferma password** .  

#### <a name="continue-if-some-files-cannot-be-restored"></a>Continua se non è possibile ripristinare dei file

Continua a ripristinare lo stato utente e le impostazioni anche se USMT non riesce a ripristinare alcuni file. Il passaggio abilita questa opzione per impostazione predefinita. Se si disabilita questa opzione e USMT rileva errori durante il ripristino dei file, questo passaggio restituisce immediatamente un errore. USMT non ripristina tutti i file.

#### <a name="enable-verbose-logging"></a>Abilita la registrazione dettagliata

Abilitare questa opzione per generare informazioni di file di log più dettagliate. Durante il ripristino dello stato, per impostazione predefinita la sequenza di attività genera il file **Loadstate.log** nella cartella dei log della sequenza di attività, `%WinDir%\ccm\logs`.  



## <a name="run-command-line"></a><a name="BKMK_RunCommandLine"></a> Esegui riga di comando

Usare questo passaggio per eseguire la riga di comando specificata.  

Il comando in esecuzione deve soddisfare i criteri seguenti:  

- Non deve interagire con il desktop. Il comando deve essere eseguito in modalità invisibile all'utente o automatica.  

- Non deve dare inizio autonomamente a un riavvio. Il comando deve richiedere un riavvio usando il codice di riavvio standard, ovvero 3010. Questo comportamento garantisce che la sequenza di attività gestisca adeguatamente il riavvio. Se il comando restituisce un codice di uscita 3010, il motore della sequenza di attività riavvia il computer. Dopo il riavvio, la sequenza di attività continua automaticamente.

Questo passaggio può essere eseguito nel sistema operativo completo o in Windows PE.

Per aggiungere questo passaggio nell'editor della sequenza di attività, selezionare **Aggiungi**, selezionare **Generale** e quindi selezionare **Esegui riga di comando**.

### <a name="variables-for-run-command-line"></a>Variabili per Esegui riga di comando

Usare le variabili della sequenza di attività seguenti con questo passaggio:  

- [OSDDoNotLogCommand](task-sequence-variables.md#OSDDoNotLogCommand) (a partire dalla versione 1902)<!--3654172-->  
- [SMSTSDisableWow64Redirection](task-sequence-variables.md#SMSTSDisableWow64Redirection)  
- [SMSTSRunCommandLineUserName](task-sequence-variables.md#SMSTSRunCommandLineUserName)  
- [SMSTSRunCommandLineUserPassword](task-sequence-variables.md#SMSTSRunCommandLineUserPassword)  
- [SMSTSRunCommandLineAsUser](task-sequence-variables.md#SMSTSRunCommandLineAsUser) (a partire dalla versione 2002)<!-- 5573175 -->
- [WorkingDirectory](task-sequence-variables.md#WorkingDirectory)  

### <a name="cmdlets-for-run-command-line"></a>Cmdlet per Esegui riga di comando

Gestire questo passaggio con i cmdlet di PowerShell seguenti:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepRunCommandLine](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtsstepruncommandline?view=sccm-ps)
- [New-CMTSStepRunCommandLine](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtsstepruncommandline?view=sccm-ps)
- [Remove-CMTSStepRunCommandLine](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtsstepruncommandline?view=sccm-ps)
- [Set-CMTSStepRunCommandLine](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtsstepruncommandline?view=sccm-ps)

### <a name="properties-for-run-command-line"></a>Proprietà per Esegui riga di comando

Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

#### <a name="command-line"></a>Riga di comando

Specifica la riga di comando che esegue la sequenza di attività. Questo campo è obbligatorio. Includere le estensioni del nome file, ad esempio vbs ed exe. Includere tutti i file di impostazione necessari e le opzioni della riga di comando.  

Se non si specifica l'estensione, Configuration Manager prova a usare le estensioni com, exe e bat. Se il nome file ha un'estensione che non corrisponde a un tipo di file eseguibile, Configuration Manager prova ad applicare un'associazione locale. Ad esempio, se la riga di comando è readme.gif, Configuration Manager avvia l'applicazione specificata nel computer di destinazione per l'apertura dei file con estensione gif.  

Esempi:  

`setup.exe /a`  

`cmd.exe /c copy Jan98.dat c:\sales\Jan98.dat`  

> [!NOTE]  
> Per un'esecuzione corretta, far precedere alle azioni della riga di comando il comando **cmd.exe /c**. Sono esempi di queste azioni i comandi di reindirizzamento output, piping e copia.  

#### <a name="output-to-task-sequence-variable"></a>Output nella variabile della sequenza di attività

<!--user story 4977616/bug 4798352-->

A partire dalla versione 1910, salvare l'output del comando in una variabile personalizzata della sequenza di attività.

> [!Note]  
> Configuration Manager limita questo output agli ultimi 1000 caratteri.

#### <a name="disable-64-bit-file-system-redirection"></a>Disattiva il reindirizzamento del file system a 64 bit

Per impostazione predefinita, i sistemi operativi a 64 bit usano il redirector del file system WOW64 per l'esecuzione di righe di comando. Il comportamento consiste nel trovare versioni a 32 bit di file eseguibili e librerie del sistema operativo. Selezionare questa opzione per disabilitare l'uso del redirector del file system WOW64. Windows esegue il comando con versioni native a 64 bit dei file eseguibili e delle librerie del sistema operativo. Questa opzione non produce alcun effetto se eseguita in un sistema operativo a 32 bit.  

#### <a name="start-in"></a>Da

Specifica la cartella eseguibile per il programma. Sono consentiti al massimo 127 caratteri. Questa cartella può essere un percorso assoluto nel computer di destinazione o un percorso relativo alla cartella del punto di distribuzione contenente il pacchetto. Questo campo è facoltativo.  

Esempi:  

`c:\officexp`  

`i386`  

> [!NOTE]  
> Il pulsante **Sfoglia** consente di cercare file e cartelle nel computer locale. Qualsiasi elemento selezionato deve essere presente anche nel computer di destinazione. Deve esistere nella stessa posizione e con gli stessi nomi di file e cartelle.  

#### <a name="package"></a>Pacchetto

Quando nella riga di comando si specificano file o programmi che non sono già presenti nel computer di destinazione, selezionare questa opzione per specificare il pacchetto di Configuration Manager contenente i file necessari. Questo pacchetto non richiede alcun programma. Questa opzione non è necessaria se i file specificati esistono nel computer di destinazione.  

#### <a name="time-out"></a>Timeout

Specifica un valore che rappresenta il tempo concesso da Configuration Manager per l'esecuzione della riga di comando. Questo valore può essere compreso tra 1 e 999 minuti. Il valore predefinito è 15 minuti. Questa opzione è disabilitata per impostazione predefinita.  

> [!IMPORTANT]  
> Se si immette un valore insufficiente per il completamento del comando specificato, il passaggio ha esito negativo. È possibile che l'intera sequenza di attività abbia esito negativo, a seconda delle condizioni del passaggio o del gruppo. In caso di scadenza del timeout, Configuration Manager termina il processo della riga di comando.  

#### <a name="run-this-step-as-the-following-account"></a>Esegui questo passaggio come account specificato

Specifica che la riga di comando viene eseguita come account utente Windows diverso dall'account di sistema locale.  

> [!NOTE]  
> Per eseguire semplici script o comandi con un altro account dopo l'installazione del sistema operativo, aggiungere prima di tutto l'account al computer. Potrebbe anche essere necessario ripristinare i profili utente di Windows per eseguire programmi più complessi, ad esempio Windows Installer.  

#### <a name="account"></a>Account

Specifica l'account utente di Windows usato da questo passaggio per eseguire la riga di comando. La riga di comando viene eseguita con le autorizzazioni dell'account specificato. Selezionare **Imposta** per specificare l'utente locale o l'account di dominio. Per altre informazioni sull'account Esegui come per la sequenza di attività, vedere [Account](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account).

> [!IMPORTANT]  
> Se questo passaggio specifica un account utente e viene eseguito in Windows PE, l'azione ha esito negativo. Non è possibile aggiungere Windows PE a un dominio. Questo errore viene registrato nel file **smsts.log**.  

### <a name="options-for-run-command-line"></a>Opzioni per Esegui riga di comando

Oltre alle opzioni predefinite, nella scheda **Opzioni** di questo passaggio della sequenza di attività configurare le impostazioni aggiuntive seguenti:  

#### <a name="success-codes"></a>Codici di riuscita

Includere altri codici di uscita dallo script che devono essere valutati come esiti positivi.



## <a name="run-powershell-script"></a><a name="BKMK_RunPowerShellScript"></a> Esegui script PowerShell

Usare questo passaggio per eseguire lo script di Windows PowerShell specificato.  

Lo script deve soddisfare i criteri seguenti:  

- Non deve interagire con il desktop. Lo script deve essere eseguito in modalità invisibile all'utente o automatica.  

- Non deve dare inizio autonomamente a un riavvio. Lo script deve richiedere un riavvio usando il codice di riavvio standard, ovvero 3010. Questo comportamento garantisce che la sequenza di attività gestisca adeguatamente il riavvio. Se lo script restituisce un codice di uscita 3010, il motore della sequenza di attività riavvia il computer. Dopo il riavvio, la sequenza di attività continua automaticamente.

Questo passaggio può essere eseguito nel sistema operativo completo o in Windows PE. Per eseguire questo passaggio in Windows PE, abilitare PowerShell nell'immagine di avvio. Abilitare il componente WinPE-PowerShell dalla scheda **Componenti facoltativi** nelle proprietà per l'immagine di avvio. Per altre informazioni su come modificare un'immagine d'avvio, vedere [Manage boot images](../get-started/manage-boot-images.md) (Gestire le immagini d'avvio).  

> [!NOTE]  
> PowerShell non è abilitato per impostazione predefinita nei sistemi operativi Windows Embedded.  

> [!WARNING]
> Alcuni software antimalware possono attivare inavvertitamente eventi per il passaggio sequenza di attività Esegui script PowerShell di Configuration Manager. Si consiglia di escludere %windir%\temp\smstspowershellscripts in modo che il software antimalware consenta l'esecuzione di tali script senza interferenze.

Per aggiungere questo passaggio nell'editor della sequenza di attività, selezionare **Aggiungi**, selezionare **Generale** e quindi selezionare **Esegui script PowerShell**.

### <a name="variables-for-run-powershell-script"></a>Variabili per Esegui script PowerShell

Usare le variabili della sequenza di attività seguenti con questo passaggio:  

- [OSDLogPowerShellParameters](task-sequence-variables.md#OSDLogPowerShellParameters) (a partire dalla versione 1902)<!--3556028-->  
- [SMSTSRunPowerShellAsUser](task-sequence-variables.md#SMSTSRunPowerShellAsUser) (a partire dalla versione 2002)<!-- 5573175 -->
- [SMSTSRunPowerShellUserName](task-sequence-variables.md#SMSTSRunPowerShellUserName)  
- [SMSTSRunPowerShellUserPassword](task-sequence-variables.md#SMSTSRunPowerShellUserPassword)  

### <a name="cmdlets-for-run-powershell-script"></a>Cmdlet per Esegui script PowerShell

Gestire questo passaggio con i cmdlet di PowerShell seguenti:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepRunPowerShellScript](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtssteprunpowershellscript?view=sccm-ps)
- [New-CMTSStepRunPowerShellScript](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtssteprunpowershellscript?view=sccm-ps)
- [Remove-CMTSStepRunPowerShellScript](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtssteprunpowershellscript?view=sccm-ps)
- [Set-CMTSStepRunPowerShellScript](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtssteprunpowershellscript?view=sccm-ps)

> [!Note]  
> Usare gli script PowerShell firmati in formato Unicode. Il formato ANSI, ovvero l'impostazione predefinita, non funziona con questo passaggio.

### <a name="properties-for-run-powershell-script"></a>Proprietà per Esegui script PowerShell

Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

#### <a name="package"></a>Pacchetto

Specifica il pacchetto di Configuration Manager contenente lo script PowerShell. Un pacchetto può includere più script PowerShell.  

#### <a name="script-name"></a>Nome script

Specifica il nome dello script PowerShell da eseguire. Questo campo è obbligatorio.  

#### <a name="enter-a-powershell-script"></a>Immettere uno script di PowerShell

<!-- 3556028 -->
A partire dalla versione 1902, è possibile immettere direttamente il codice di Windows PowerShell in questo passaggio. Questa funzionalità consente di eseguire i comandi PowerShell durante una sequenza di attività senza prima creare e distribuire un pacchetto con lo script.

Quando si aggiunge o modifica uno script, la finestra dello script di PowerShell consente le azioni seguenti:  

- Modificare lo script direttamente  

- Aprire uno script esistente dal file  

- Passare a uno [script](../../apps/deploy-use/create-deploy-scripts.md) esistente approvato in Configuration Manager

> [!Important]  
> Per sfruttare i vantaggi di questa nuova funzionalità di Configuration Manager, dopo l'aggiornamento del sito aggiornare anche i client alla versione più recente. Anche se le nuove funzionalità vengono visualizzate nella console di Configuration Manager quando si esegue l'aggiornamento del sito e della console, lo scenario completo risulta funzionante solo dopo l'aggiornamento alla versione più recente del client.

#### <a name="parameters"></a>Parametri

Specifica i parametri passati allo script di PowerShell. Questi parametri corrispondono ai parametri di script di PowerShell nella riga di comando.  

Specificare i parametri usati dallo script, non per la riga di comando di Windows PowerShell.  
L'esempio seguente include parametri validi:  

`-MyParameter1 MyValue1 -MyParameter2 MyValue2`  

L'esempio seguente include parametri non validi: I primi due elementi sono parametri della riga di comando di Windows PowerShell ( **-NoLogo** e **-ExecutionPolicy Unrestricted**). Lo script non utilizza questi parametri.  

`-NoLogo -ExecutionPolicy Unrestricted -File MyScript.ps1 -MyParameter1 MyValue1 -MyParameter2 MyValue2`

<!-- SCCMDocs-pr issue 3561 -->
Se il valore di un parametro include un carattere speciale, racchiudere il valore tra virgolette singole (`'`). L'uso delle virgolette doppie (`"`) può determinare l'elaborazione non corretta del parametro nel passaggio della sequenza di attività.

ad esempio `-Arg1 '%TSVar1%' -Arg2 '%TSVar2%'`

A partire dalla versione 2002, impostare questa proprietà su una variabile.<!-- 5690481 --> Ad esempio, se si specifica `%MyScriptVariable%`, quando la sequenza di attività esegue lo script, aggiunge il valore di questa variabile personalizzata alla riga di comando di PowerShell.

#### <a name="powershell-execution-policy"></a>Criteri di esecuzione di PowerShell

Determinare quali script di PowerShell possono essere eseguiti nel computer. Scegliere uno dei criteri di esecuzione seguenti:  

- **AllSigned**: vengono eseguiti solo gli script firmati da un editore attendibile  

- **Non definito**: non viene definito alcun criterio di esecuzione  

- **Ignora**: vengono caricati tutti i file di configurazione e vengono eseguiti tutti gli script. Se si scarica uno script non firmato da Internet, Windows PowerShell non richiede l'autorizzazione prima di eseguire tale script.  

> [!IMPORTANT]  
> PowerShell 1.0 non supporta i criteri di esecuzione Non definito e Ignora.  

#### <a name="output-to-task-sequence-variable"></a>Output nella variabile della sequenza di attività

<!-- 3556028 -->
A partire dalla versione 1902, è possibile salvare l'output dello script in una variabile personalizzata della sequenza di attività.

> [!Note]  
> A partire dalla versione 1910 Configuration Manager limita questo output agli ultimi 1000 caratteri.

Per un esempio di come usare questa proprietà del passaggio, vedere [Come impostare le variabili](using-task-sequence-variables.md#bkmk_run-ps).

#### <a name="start-in"></a>Da

<!-- 3556028 -->
A partire dalla versione 1902, è possibile specificare la cartella di avvio per lo script, fino a 127 caratteri. Questa cartella può essere un percorso assoluto nel computer di destinazione o un percorso relativo alla cartella del punto di distribuzione contenente il pacchetto. Questo campo è facoltativo.  

> [!NOTE]  
> Il pulsante **Sfoglia** consente di cercare file e cartelle nel computer locale. Qualsiasi elemento selezionato deve essere presente anche nel computer di destinazione. Deve esistere nella stessa posizione e con gli stessi nomi di file e cartelle.  

#### <a name="time-out"></a>Timeout

<!-- 3556028 -->
A partire dalla versione 1902, è possibile specificare un valore che rappresenta il tempo di esecuzione consentito da Configuration Manager per lo script di PowerShell. Questo valore può essere compreso tra 1 e 999 minuti. Il valore predefinito è 15 minuti. Questa opzione è disabilitata per impostazione predefinita.  

> [!IMPORTANT]  
> Se si immette un valore insufficiente per il completamento dello script specificato, il passaggio ha esito negativo. È possibile che l'intera sequenza di attività abbia esito negativo, a seconda delle condizioni del passaggio o del gruppo. In caso di scadenza del timeout, Configuration Manager termina il processo di PowerShell.  

#### <a name="run-this-step-as-the-following-account"></a>Esegui questo passaggio come account specificato

<!-- 3556028 -->
A partire dalla versione 1902, è possibile specificare che lo script di PowerShell viene eseguito con un account utente Windows diverso dall'account di sistema locale.  

> [!NOTE]  
> Per eseguire semplici script o comandi con un altro account dopo l'installazione del sistema operativo, aggiungere prima di tutto l'account al computer. Per eseguire azioni più complesse potrebbe inoltre essere necessario ripristinare i profili utente di Windows.  

#### <a name="account"></a>Account

<!-- 3556028 -->
A partire dalla versione 1902, è possibile specificare l'account utente Windows usato in questo passaggio per eseguire lo script di PowerShell. L'account specificato deve corrispondere a un amministratore locale del sistema. Lo script viene eseguito con le autorizzazioni di questo account. Selezionare **Imposta** per specificare l'utente locale o l'account di dominio. Per altre informazioni sull'account Esegui come per la sequenza di attività, vedere [Account](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account).

> [!IMPORTANT]  
> Se questo passaggio specifica un account utente e viene eseguito in Windows PE, l'azione ha esito negativo. Non è possibile aggiungere Windows PE a un dominio. Questo errore viene registrato nel file **smsts.log**.  

### <a name="options-for-run-powershell-script"></a>Opzioni per Esegui script PowerShell

Oltre alle opzioni predefinite, nella scheda **Opzioni** di questo passaggio della sequenza di attività configurare le impostazioni aggiuntive seguenti:  

#### <a name="success-codes"></a>Codici di riuscita

<!-- 3556028 -->
A partire dalla versione 1902, è possibile includere altri codici di uscita dallo script che devono essere valutati come esiti positivi.



## <a name="run-task-sequence"></a><a name="child-task-sequence"></a> Esegui la sequenza di attività

> [!Note]  
> Nella versione 1910 Configuration Manager abilita questa funzionalità per impostazione predefinita. Nella versione 1906 o nelle versioni precedenti Configuration Manager non abilita questa funzionalità facoltativa per impostazione predefinita. Abilitare questa funzionalità prima di usarla. Per altre informazioni, vedere [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options) (Abilitare le funzioni facoltative dagli aggiornamenti).

Questo passaggio esegue un'altra sequenza di attività. Crea una relazione padre-figlio tra le sequenze di attività. Le sequenze di attività figlio consentono di creare sequenze di attività più modulari e riutilizzabili.

Per aggiungere questo passaggio nell'editor della sequenza di attività, selezionare **Aggiungi**, selezionare **Generale** e quindi selezionare **Esegui la sequenza di attività**.

### <a name="specifications-and-limitations-for-run-task-sequence"></a>Specifiche e limitazioni per Esegui la sequenza di attività

Quando si aggiunge una sequenza di attività figlio a una sequenza di attività, tenere presente quanto segue:  

- Le sequenze di attività padre e figlio sono di fatto combinate in un unico criterio eseguito dal client.  

- L'ambiente è globale. Se la sequenza di attività padre imposta una variabile e quindi la sequenza di attività figlio la modifica, la variabile mantiene il valore più recente. Se la sequenza di attività figlio crea una nuova variabile, la variabile è disponibile per la parte restante della sequenza di attività padre.  

- I messaggi di stato vengono inviati con la procedura normale per un'operazione sequenza di attività singola.  

- Le sequenze di attività scrivono voci nel file **smsts.log**. Le nuove voci di log indicano chiaramente l'avvio di una sequenza di attività figlio.  

<!--the following points are from SCCMdocs issue #1079-->

- Non è possibile selezionare una sequenza di attività con un riferimento all'immagine d'avvio. Per qualsiasi distribuzione che richiede un'immagine d'avvio, specificarla nella sequenza di attività padre.  

- Se una sequenza di attività figlio è disabilitata, la distribuzione ha esito negativo. Non è possibile usare l'opzione **Continua in caso di errore** per ignorare questa limitazione.  

- Se una sequenza di attività figlio contiene passaggi che sono considerati *a impatto elevato*, Software Center non lo rileva e non visualizza la notifica di impatto elevato. Modificare le proprietà della sequenza di attività padre, nella scheda Notifica all'utente, per specificare l'opzione **Questa è una sequenza di attività a impatto elevato**.  

- Se una sequenza di attività figlio include un riferimento a pacchetto mancante, la visualizzazione della sequenza di attività padre non rileva questo stato. Se si modifica la sequenza di attività padre, eventuali riferimenti mancanti nelle sequenze di attività figlio vengono rilevati quando si apportano modifiche alla sequenza padre.  

### <a name="cmdlets-for-run-task-sequence"></a>Cmdlet per Esegui la sequenza di attività

A partire dalla versione 1906, gestire questo passaggio con i cmdlet di PowerShell seguenti:<!-- 2839943, SCCMDocs#1118 -->

- **Get-CMTSStepRunTaskSequence**
- **New-CMTSStepRunTaskSequence**
- **Remove-CMTSStepRunTaskSequence**
- **Set-CMTSStepRunTaskSequence**

Per altre informazioni, vedere [Note sulla versione 1906 - Nuovi cmdlet](https://docs.microsoft.com/powershell/sccm/1906-release-notes?view=sccm-ps#new-cmdlets).

### <a name="properties-for-run-task-sequence"></a>Proprietà per Esegui la sequenza di attività

Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

#### <a name="select-task-sequence-to-run"></a>Selezionare la sequenza di attività da eseguire

Selezionare **Sfoglia** per selezionare la sequenza di attività figlio. La finestra di dialogo **Seleziona una sequenza di attività** non visualizza la sequenza di attività padre.



## <a name="set-dynamic-variables"></a><a name="BKMK_SetDynamicVariables"></a> Imposta variabili dinamiche

Usare questo passaggio per eseguire le azioni seguenti:  

1. Raccogliere informazioni dal computer e il relativo ambiente. Impostare quindi le variabili della sequenza di attività con le informazioni.  

2. Valutare le regole definite. Impostare le variabili della sequenza di attività in base alle regole che risultano vere.  

Questo passaggio può essere eseguito nel sistema operativo completo o in Windows PE.  

Per aggiungere questo passaggio nell'editor della sequenza di attività, selezionare **Aggiungi**, selezionare **Generale** e quindi selezionare **Imposta variabili dinamiche**.

### <a name="variables-for-set-dynamic-variables"></a>Variabili per Imposta variabili dinamiche

La sequenza di attività imposta automaticamente le variabili della sequenza di attività di sola lettura seguenti:  

- [\_SMSTSMake](task-sequence-variables.md#SMSTSMake)  
- [\_SMSTSModel](task-sequence-variables.md#SMSTSModel)  
- [\_SMSTSMacAddresses](task-sequence-variables.md#SMSTSMacAddresses)  
- [\_SMSTSIPAddresses](task-sequence-variables.md#SMSTSIPAddresses)  
- [\_SMSTSSerialNumber](task-sequence-variables.md#SMSTSSerialNumber)  
- [\_SMSTSAssetTag](task-sequence-variables.md#SMSTSAssetTag)  
- [\_SMSTSUUID](task-sequence-variables.md#SMSTSUUID)  

### <a name="cmdlets-for-set-dynamic-variables"></a>Cmdlet per Imposta variabili dinamiche

Gestire questo passaggio con i cmdlet di PowerShell seguenti:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepSetDynamicVariable](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtsstepsetdynamicvariable?view=sccm-ps)
- [New-CMTSStepSetDynamicVariable](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtsstepsetdynamicvariable?view=sccm-ps)
- [Remove-CMTSStepSetDynamicVariable](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtsstepsetdynamicvariable?view=sccm-ps)
- [Set-CMTSStepSetDynamicVariable](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtsstepsetdynamicvariable?view=sccm-ps)

### <a name="properties-for-set-dynamic-variables"></a>Proprietà per Imposta variabili dinamiche

Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

#### <a name="dynamic-rules-and-variables"></a>Variabili e regole dinamiche

Per impostare una variabile dinamica da usare nella sequenza di attività, aggiungere una regola. Quindi impostare un valore per ogni variabile specificata nella regola. È anche possibile aggiungere una o più variabili senza aggiungere una regola. Quando si aggiunge una regola, scegliere tra le categorie seguenti:  

- **Computer**: valutare i valori per il tag asset hardware, l'UUID, il numero di serie o l'indirizzo MAC. Impostare più valori in base alle esigenze. Se uno dei valori è true, la regola restituisce true. Ad esempio la regola seguente restituisce true se il numero di serie è 5892087 e l'indirizzo MAC è 22-A4-5A-13-78-26:  

    `IF Serial Number = 5892087 OR MAC address = 26-78-13-5A-A4-22 THEN`  

- **Location** (Percorso): valutare i valori per il gateway di rete predefinito  

- **Marca e modello**: valutare i valori relativi a marca e modello di un computer. La regola restituisce true solo se entrambi i valori restituiscono true.

    Specificare un asterisco (`*`) e un punto interrogativo (`?`) come caratteri jolly. L'asterisco corrisponde a più caratteri e il punto interrogativo corrisponde a un singolo carattere. Ad esempio, la stringa `DELL*900?` corrisponde sia a `DELL-ABC-9001` che a `DELL9009`.  

- **Variabile della sequenza di attività**: aggiungere una variabile della sequenza di attività, una condizione e un valore da valutare. La regola restituisce true quando il valore impostato per la variabile soddisfa la condizione specificata.  

    Specificare una o più variabili da impostare per una regola che restituisce true oppure impostare variabili senza usare una regola. Selezionare una variabile esistente o creare una variabile personalizzata.  

    - **Existing task sequence variables** (Variabili esistenti della sequenza di attività): selezionare una o più variabili da un elenco di variabili esistenti della sequenza di attività. Le variabili di matrice non sono disponibili per la selezione.  

    - **Custom task sequence variables** (Variabili personalizzate della sequenza di attività): definire una variabile personalizzata della sequenza di attività. È anche possibile specificare una variabile esistente della sequenza di attività. Questa impostazione è utile per specificare una matrice di variabili esistenti, ad esempio **OSDAdapter**, perché le matrici di variabili non sono incluse nell'elenco di variabili esistenti della sequenza di attività.  

Dopo aver selezionato le variabili per una regola, specificare un valore per ogni variabile. La variabile è impostata sul valore specificato quando la regola restituisce true. Per ogni variabile è possibile selezionare **Valore segreto** per nascondere il valore della variabile. Per impostazione predefinita, alcune variabili esistenti nascondono i valori, ad esempio la variabile **OSDCaptureAccountPassword**.  

> [!IMPORTANT]  
> Configuration Manager rimuove tutti i valori contrassegnati come **Valore segreto** quando si importa una sequenza di attività con il passaggio **Imposta variabili dinamiche**. Immettere di nuovo il valore per la variabile dinamica dopo l'importazione della sequenza di attività.  



## <a name="set-task-sequence-variable"></a><a name="BKMK_SetTaskSequenceVariable"></a> Imposta variabile della sequenza di attività

Usare questo passaggio per configurare il valore di una variabile usata con la sequenza di attività.  

Questo passaggio può essere eseguito nel sistema operativo completo o in Windows PE.

Per aggiungere questo passaggio nell'editor della sequenza di attività, selezionare **Aggiungi**, selezionare **Generale** e quindi selezionare **Imposta variabile della sequenza di attività**.

### <a name="variables-for-set-task-sequence-variable"></a>Variabili per Imposta variabile della sequenza di attività

Le variabili della sequenza di attività vengono lette dalle azioni della sequenza di attività e specificano il comportamento di tali azioni. Per altre informazioni su variabili specifiche della sequenza attività e su come usarle, vedere gli articoli seguenti:  

- [Come usare le variabili della sequenza di attività](using-task-sequence-variables.md)  
- [Variabili della sequenza di attività](task-sequence-variables.md)  

### <a name="cmdlets-for-set-task-sequence-variable"></a>Cmdlet per Imposta variabile della sequenza di attività

Gestire questo passaggio con i cmdlet di PowerShell seguenti:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepSetVariable](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtsstepsetvariable?view=sccm-ps)
- [New-CMTSStepSetVariable](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtsstepsetvariable?view=sccm-ps)
- [Remove-CMTSStepSetVariable](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtsstepsetvariable?view=sccm-ps)
- [Set-CMTSStepSetVariable](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtsstepsetvariable?view=sccm-ps)

### <a name="properties-for-set-task-sequence-variable"></a>Proprietà per Imposta variabile della sequenza di attività

Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

#### <a name="task-sequence-variable"></a>Variabile della sequenza di attività

Specificare il nome di una variabile di azione o predefinita della sequenza di attività oppure specificare un nome di variabile definito dall'utente.  

#### <a name="do-not-display-this-value"></a>Non visualizzare questo valore

<!--1358330-->
Abilitare questa opzione per mascherare i dati sensibili archiviati nelle variabili della sequenza di attività. ad esempio quando si specifica una password.

> [!Note]  
> Abilitare questa opzione e quindi impostare il valore della variabile della sequenza di attività. In caso contrario, il valore della variabile non viene impostato nel modo desiderato e ciò potrebbe causare comportamenti imprevisti quando viene eseguita la sequenza di attività.<!--SCCMdocs issue #800-->

#### <a name="value"></a>Valore  

La sequenza di attività imposta la variabile su questo valore. Impostare questa variabile della sequenza di attività sul valore di un'altra variabile della sequenza di attività con la sintassi `%varname%`.  



## <a name="setup-windows-and-configmgr"></a><a name="BKMK_SetupWindowsandConfigMgr"></a> Imposta Windows e ConfigMgr

Usare questo passaggio per eseguire la transizione da Windows PE al nuovo sistema operativo. Questo passaggio della sequenza di attività è una parte necessaria di qualsiasi distribuzione del sistema operativo. Installa il client di Configuration Manager nel nuovo sistema operativo e prepara la sequenza di attività per continuare l'esecuzione nel nuovo sistema operativo.  

Questo passaggio è responsabile della transizione della sequenza di attività da Windows PE al sistema operativo completo. A causa di questa transizione, il passaggio viene eseguito sia in Windows PE che nel sistema operativo completo. Poiché la transizione viene avviata in Windows PE, tuttavia, può essere aggiunto solo durante la parte relativa a Windows PE della sequenza di attività.  

Questo passaggio sostituisce le variabili della directory sysprep.inf o unattend.xml, ad esempio `%WINDIR%` e `%ProgramFiles%`, con la directory di installazione di Windows PE, `X:\Windows`. La sequenza di attività ignora le variabili specificate usando queste variabili di ambiente.  

Per aggiungere questo passaggio nell'editor della sequenza di attività, selezionare **Aggiungi**, selezionare **Immagini** e quindi selezionare **Imposta Windows e ConfigMgr**.

### <a name="behaviors-for-setup-windows-and-configmgr"></a>Comportamenti per Imposta Windows e ConfigMgr

Questo passaggio esegue le azioni seguenti:  

#### <a name="preliminaries-windows-pe"></a>Operazioni preliminari: Windows PE  

1. Sostituire le variabili della sequenza di attività nel file unattend.xml.  

2. Scaricare il pacchetto contenente il client di Configuration Manager. Aggiungere il pacchetto all'immagine distribuita.  

#### <a name="set-up-windows"></a>Configurazione di Windows  

- Installazione basata su immagine  

    1. Disabilitare il client di Configuration Manager nell'immagine, se presente. In altre parole, disabilitare l'avvio automatico del servizio client di Configuration Manager.  

    2. Aggiornare il Registro di sistema nell'immagine distribuita per avviare il sistema operativo distribuito con la stessa lettera di unità del computer di riferimento.  

    3. Riavviare nel sistema operativo distribuito.  

    4. L'installazione minima di Windows viene eseguita usando un file di risposte sysprep.inf o unattend.xml specificato in precedenza e in cui sono state rimosse tutte le interazioni con gli utenti finali. Se si usa il passaggio **Applica impostazioni di rete** per l'aggiunta a un dominio, queste informazioni si trovano nel file di risposte. L'installazione minima di Windows aggiunge il computer al dominio.  

- Installazione basata su Setup.exe. Esegue Setup.exe con il processo di installazione di Windows tipico:  

    1. Copiare nell'unità disco rigido il pacchetto di aggiornamento del sistema operativo specificato nel passaggio **Applica sistema operativo**.  

    2. Eseguire il riavvio nel sistema operativo appena distribuito.  

    3. L'installazione minima di Windows viene eseguita usando il file di risposte sysprep.inf o unattend.xml specificato in precedenza e in cui sono state rimosse tutte le impostazioni dell'interfaccia utente. Se si usa il passaggio **Applica impostazioni di rete** per l'aggiunta a un dominio, queste informazioni si trovano nel file di risposte. L'installazione minima di Windows aggiunge il computer al dominio.  

#### <a name="set-up-the-configuration-manager-client"></a>Impostazione del client di Configuration Manager  

1. Al termine dell'installazione minima di Windows, verrà ripresa la sequenza di attività usando setupcomplete.cmd. Per altre informazioni, vedere [Eseguire uno script al termine dell'installazione (SetupComplete. cmd)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/add-a-custom-script-to-windows-setup#run-a-script-after-setup-is-complete-setupcompletecmd).  

2. Abilitare o disabilitare l'account Administrator locale, in base all'opzione selezionata nel passaggio **Applica impostazioni Windows**.  

3. Installare il client di Configuration Manager usando il pacchetto scaricato in precedenza e le proprietà di installazione specificate in questo passaggio. Il client viene installato in "modalità di provisioning". Questa modalità impedisce che il client elabori nuove richieste di criteri fino al completamento della sequenza di attività. Per altre informazioni, vedere [Modalità di provisioning](provisioning-mode.md).  

4. Attendere la completa operatività del client.  

#### <a name="the-step-completes"></a>Il passaggio viene completato

L'esecuzione della sequenza di attività continua con il passaggio successivo.  

> [!Note]  
> Criteri di gruppo di Windows viene in genere eseguito dopo il completamento della sequenza di attività. Questo comportamento è coerente nelle diverse versioni di Windows. Altre azioni personalizzate durante la sequenza di attività possono attivare la valutazione di Criteri di gruppo. Per altre informazioni sull'ordine delle operazioni, vedere [Eseguire uno script al termine dell'installazione (SetupComplete. cmd)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/add-a-custom-script-to-windows-setup#run-a-script-after-setup-is-complete-setupcompletecmd). <!-- 2841304 -->


### <a name="variables-for-setup-windows-and-configmgr"></a>Variabili per Imposta Windows e ConfigMgr

Usare le variabili della sequenza di attività seguenti con questo passaggio:  

- [SMSClientInstallProperties](task-sequence-variables.md#SMSClientInstallProperties)  

### <a name="cmdlets-for-setup-windows-and-configmgr"></a>Cmdlet per Imposta Windows e ConfigMgr

Gestire questo passaggio con i cmdlet di PowerShell seguenti:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepSetupWindowsAndConfigMgr](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtsstepsetupwindowsandconfigmgr?view=sccm-ps)
- [New-CMTSStepSetupWindowsAndConfigMgr](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtsstepsetupwindowsandconfigmgr?view=sccm-ps)
- [Remove-CMTSStepSetupWindowsAndConfigMgr](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtsstepsetupwindowsandconfigmgr?view=sccm-ps)
- [Set-CMTSStepSetupWindowsAndConfigMgr](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtsstepsetupwindowsandconfigmgr?view=sccm-ps)

### <a name="properties-for-setup-windows-and-configmgr"></a>Proprietà per Imposta Windows e ConfigMgr

Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

#### <a name="client-package"></a>Pacchetto client

Selezionare **Sfoglia** e quindi scegliere il pacchetto di installazione del client di Configuration Manager da usare in questo passaggio.  

#### <a name="use-pre-production-client-package-when-available"></a>Usa il pacchetto client di pre-produzione se disponibile

Se è disponibile un pacchetto client di pre-produzione e il computer è un membro della raccolta di distribuzione pilota, la sequenza di attività usa tale pacchetto invece del pacchetto client di produzione. Il client di pre-produzione è una versione più recente per il testing nell'ambiente di produzione. Selezionare **Sfoglia** e quindi scegliere il pacchetto di installazione del client di pre-produzione da usare in questo passaggio.  

#### <a name="installation-properties"></a>Proprietà di installazione

Il passaggio della sequenza di attività specifica automaticamente l'assegnazione del sito e la configurazione predefinita. Usare questo campo per specificare eventuali proprietà di installazione aggiuntive da usare quando si installa il client. Per immettere più proprietà di installazione, separarle con uno spazio.  

Specificare le opzioni della riga di comando da usare durante l'installazione del client. Ad esempio, immettere `/skipprereq: silverlight.exe` per segnalare a CCMSetup.exe di non installare i prerequisiti di Microsoft Silverlight. Per altre informazioni sulle opzioni della riga di comando disponibili per CCMSetup.exe, vedere [About client installation properties](../../core/clients/deploy/about-client-installation-properties.md) (Informazioni sulle proprietà di installazione del client).  

### <a name="options-for-setup-windows-and-configmgr"></a>Opzioni per Imposta Windows e ConfigMgr

> [!NOTE]  
> Non abilitare **Continua in caso di errore** nella scheda **Opzioni**. Sia che questa opzione sia abilitata o meno, se si verifica un errore durante questo passaggio la sequenza di attività ha esito negativo.  



## <a name="upgrade-operating-system"></a><a name="BKMK_UpgradeOS"></a> Aggiorna sistema operativo

Usare questo passaggio per aggiornare una versione precedente di Windows a una versione più recente di Windows 10.  

Questo passaggio della sequenza di attività viene eseguito solo nel sistema operativo completo. Non viene eseguito in Windows PE.  

Per aggiungere questo passaggio nell'editor della sequenza di attività, selezionare **Aggiungi**, selezionare **Immagini** e quindi selezionare **Aggiorna sistema operativo**.

> [!TIP]
> A partire da Windows 10 versione 1709 il supporto include più edizioni. Quando si configura una sequenza di attività per l'uso di un pacchetto di aggiornamento del sistema operativo o di un'immagine del sistema operativo, verificare di selezionare un'[edizione supportata](../../core/plan-design/configs/support-for-windows-10.md#windows-10-as-a-client).  
>
> Usare la memorizzazione anticipata del contenuto nella cache per scaricare un pacchetto di aggiornamento del sistema operativo applicabile prima che un utente installi la sequenza di attività. Per altre informazioni, vedere [Configurare la pre-cache del contenuto](../deploy-use/configure-precache-content.md).

### <a name="variables-for-upgrade-os"></a>Variabili per Aggiorna sistema operativo

Usare le variabili della sequenza di attività seguenti con questo passaggio:  

- [_SMSTSOSUpgradeActionReturnCode](task-sequence-variables.md#SMSTSOSUpgradeActionReturnCode)  
- [SetupCompletePause](task-sequence-variables.md#SetupCompletePause)
- [OSDSetupAdditionalUpgradeOptions](task-sequence-variables.md#OSDSetupAdditionalUpgradeOptions)  

### <a name="cmdlets-for-upgrade-os"></a>Cmdlet per Aggiorna sistema operativo

Gestire questo passaggio con i cmdlet di PowerShell seguenti:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepUpgradeOperatingSystem](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepUpgradeOperatingSystem?view=sccm-ps)
- [New-CMTSStepUpgradeOperatingSystem](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepUpgradeOperatingSystem?view=sccm-ps)
- [Remove-CMTSStepUpgradeOperatingSystem](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepUpgradeOperatingSystem?view=sccm-ps)
- [Set-CMTSStepUpgradeOperatingSystem](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepUpgradeOperatingSystem?view=sccm-ps)

### <a name="properties-for-upgrade-os"></a>Proprietà per Aggiorna sistema operativo

Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

#### <a name="upgrade-package"></a>Pacchetto di aggiornamento

Selezionare questa opzione per specificare il pacchetto di aggiornamento del sistema operativo Windows 10 da usare per l'aggiornamento.  

#### <a name="source-path"></a>Percorso di origine

Specifica un percorso locale o di rete per il supporto Windows 10 usato dall'installazione di Windows. Questa impostazione corrisponde all'opzione della riga di comando `/InstallFrom` di Installazione di Windows.

È anche possibile specificare una variabile, ad esempio `%MyContentPath%` o `%DPC01%`. Quando si usa una variabile per il percorso di origine, impostarne il valore prima nella sequenza di attività. Ad esempio, usare il passaggio [Scarica contenuto pacchetto](#BKMK_DownloadPackageContent) per specificare una variabile per il percorso del pacchetto di aggiornamento del sistema operativo. Usare quindi tale variabile per il percorso di origine per questo passaggio.  

#### <a name="edition"></a>Edizione

Specificare l'edizione all'interno del supporto del sistema operativo da usare per l'aggiornamento.  

#### <a name="product-key"></a>Codice Product Key

Specificare il codice Product Key da applicare al processo di aggiornamento.  

#### <a name="provide-the-following-driver-content-to-windows-setup-during-upgrade"></a>Specifica il seguente contenuto del driver in Installazione di Windows durante l'aggiornamento

Aggiungere driver al computer di destinazione durante il processo di aggiornamento. I driver devono essere compatibili con Windows 10. Questa impostazione corrisponde all'opzione della riga di comando `/InstallDriver` di Installazione di Windows. Per altre informazioni, vedere [Opzioni della riga di comando di Installazione di Windows](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#installdrivers).

Specificare una delle opzioni seguenti:  

- **Pacchetto driver**: selezionare **Sfoglia** e scegliere un pacchetto driver esistente nell'elenco.

- **Contenuto preconfigurato**: selezionare questa opzione per specificare il percorso del contenuto del driver. È possibile specificare una cartella locale, un percorso di rete o una variabile della sequenza di attività. Quando si usa una variabile per il percorso di origine, impostarne il valore prima nella sequenza di attività. Ad esempio, usando il passaggio [Scarica contenuto pacchetto](task-sequence-steps.md#BKMK_DownloadPackageContent).  

> [!TIP]
> Se si vuole disporre di contenuto dinamico per più tipi di hardware:
>
> - Usare più istanze di questo passaggio con le condizioni per i tipi di hardware e il contenuto del driver separato.
>
> - Usare più istanze del passaggio [Scarica contenuto pacchetto](task-sequence-steps.md#BKMK_DownloadPackageContent). Inserire il contenuto in un percorso comune e quindi usare l'opzione **Contenuto preconfigurato**. Il vantaggio di questo metodo è che la sequenza di attività ha un solo passaggio **Aggiorna sistema operativo**.

#### <a name="time-out-minutes"></a>Timeout (minuti)

Specificare il numero di minuti prima che questo passaggio di Configuration Manager abbia esito negativo. Questa opzione è utile se Installazione di Windows interrompe l'elaborazione ma non termina.  

#### <a name="perform-windows-setup-compatibility-scan-without-starting-upgrade"></a>Esegui analisi compatibilità Installazione di Windows senza avviare l'aggiornamento

Esegue l'analisi di compatibilità di Installazione di Windows senza avviare il processo di aggiornamento. Questa impostazione corrisponde all'opzione della riga di comando `/Compat ScanOnly` di Installazione di Windows. Distribuire l'intero pacchetto di aggiornamento del sistema operativo con questa opzione.

<!--SCCMDocs-pr issue 2812-->
Quando si abilita questa opzione, questo passaggio non attiva la modalità di provisioning per il client di Configuration Manager. Installazione di Windows viene eseguito automaticamente in background e il client continuerà a funzionare normalmente. Per altre informazioni, vedere [Modalità di provisioning](provisioning-mode.md).

Il programma di installazione restituisce un codice di uscita come risultato dell'analisi. Nella tabella seguente sono elencati alcuni dei più comuni codici di uscita:  

|Codice di uscita|Dettagli|  
|-|-|  
|MOSETUP_E_COMPAT_SCANONLY (0xC1900210)|Nessun problema di compatibilità ("esito positivo").|  
|MOSETUP_E_COMPAT_INSTALLREQ_BLOCK (0xC1900208)|Problemi di compatibilità su cui è possibile intervenire.|  
|MOSETUP_E_COMPAT_MIGCHOICE_BLOCK (0xC1900204)|L'opzione di migrazione selezionata non è disponibile. Ad esempio, un aggiornamento da Enterprise a Professional.|  
|MOSETUP_E_COMPAT_SYSREQ_BLOCK (0xC1900200)|Non idoneo per Windows 10.|  
|MOSETUP_E_COMPAT_INSTALLDISKSPACE_BLOCK (0xC190020E)|Spazio libero su disco insufficiente.|  

Per altre informazioni su questo parametro, vedere [Opzioni della riga di comando di Installazione di Windows](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#compat).  

#### <a name="ignore-any-dismissible-compatibility-messages"></a>Ignora tutti i messaggi sulla compatibilità non rilevanti

Specifica che il programma di installazione completa l'installazione ignorando eventuali messaggi di compatibilità non rilevanti. Questa impostazione corrisponde all'opzione della riga di comando `/Compat IgnoreWarning` di Installazione di Windows.  

#### <a name="dynamically-update-windows-setup-with-windows-update"></a>Aggiorna dinamicamente Installazione di Windows con Windows Update

Abilitare il programma di installazione per l'esecuzione di operazioni di aggiornamento dinamico, quali la ricerca, il download e l'installazione di aggiornamenti. Questa impostazione corrisponde all'opzione della riga di comando `/DynamicUpdate` di Installazione di Windows. Questa impostazione non è compatibile con gli aggiornamenti software di Configuration Manager. Abilitare questa opzione quando si gestiscono gli aggiornamenti con Windows Server Update Services (WSUS) in modalità autonoma o con Windows Update per le aziende.  

#### <a name="override-policy-and-use-default-microsoft-update"></a>Sostituisci i criteri e usa Microsoft Update predefinito

Ignorare temporaneamente i criteri locali in tempo reale per eseguire operazioni di aggiornamento dinamico. Il computer ottiene gli aggiornamenti da Windows Update.
