---
title: Informazioni di riferimento sulle variabili della sequenza di attività
titleSuffix: Configuration Manager
description: Informazioni sulle variabili per controllare e personalizzare una sequenza di attività di Configuration Manager.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: reference
ms.assetid: 62f15230-d3a6-4afc-abd4-1e07e7ba6c97
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 86a19970b58747d83ae8823eb8e2a85c40c03c4d
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697348"
---
# <a name="task-sequence-variables"></a>Variabili della sequenza di attività

*Si applica a: Configuration Manager (Current Branch)*

Questo articolo include informazioni di riferimento per tutte le variabili disponibili in ordine alfabetico. Usare la funzione **Trova** del browser (in genere **CTRL** + **F**) per trovare una variabile specifica. Per le variabili viene indicato se sono specifiche per un passaggio particolare. L'articolo sui [passaggi della sequenza di attività](task-sequence-steps.md) include l'elenco delle variabili specifiche per ogni passaggio.

Per altre informazioni, vedere [Come usare le variabili della sequenza di attività](using-task-sequence-variables.md).

## <a name="task-sequence-variable-reference"></a><a name="bkmk_tsvar"></a> Informazioni di riferimento sulle variabili della sequenza di attività

### <a name="_osddetectedwindir"></a><a name="OSDDetectedWinDir"></a> _OSDDetectedWinDir

La sequenza di attività esegue l'analisi dei dischi rigidi del computer per cercare una precedente installazione del sistema operativo all'avvio di Windows PE. Il percorso della cartella Windows viene archiviato nella variabile. È possibile configurare la sequenza di attività in modo da recuperare questo valore dall'ambiente e usarlo per specificare lo stesso percorso di cartella di Windows da usare per la nuova installazione del sistema operativo.

### <a name="_osddetectedwindrive"></a><a name="OSDDetectedWinDrive"></a> _OSDDetectedWinDrive

La sequenza di attività esegue l'analisi dei dischi rigidi del computer per cercare una precedente installazione del sistema operativo all'avvio di Windows PE. Il percorso dell'unità disco rigido in cui è installato il sistema operativo viene archiviato nella variabile. È possibile configurare la sequenza di attività in modo da recuperare questo valore dall'ambiente e usarlo per specificare lo stesso percorso del disco rigido da usare per il nuovo sistema operativo.

### <a name="_osdmigrateusmtpackageid"></a><a name="OSDMigrateUsmtPackageID"></a> _OSDMigrateUsmtPackageID

*Si applica al passaggio [Acquisisci stato utente](task-sequence-steps.md#BKMK_CaptureUserState).*

(input)

Specifica l'ID del pacchetto di Configuration Manager che contiene i file USMT. Questa variabile è obbligatoria.

### <a name="_osdmigrateusmtrestorepackageid"></a><a name="OSDMigrateUsmtRestorePackageID"></a> _OSDMigrateUsmtRestorePackageID

*Si applica al passaggio [Ripristina stato utente](task-sequence-steps.md#BKMK_RestoreUserState).*

(input)

Specifica l'ID del pacchetto di Configuration Manager che contiene i file USMT. Questa variabile è obbligatoria.

### <a name="_smstsadvertid"></a><a name="SMSTSAdvertID"></a> _SMSTSAdvertID

Archivia l'ID univoco di distribuzione della sequenza di attività. Usa lo stesso formato di un ID di distribuzione software di Configuration Manager. Se la sequenza di attività viene eseguita da un supporto autonomo, la variabile non è definita.

#### <a name="example"></a>Esempio

`ABC20001`

### <a name="_smstsassettag"></a><a name="SMSTSAssetTag"></a> _SMSTSAssetTag

*Si applica al passaggio [Imposta variabili dinamiche](task-sequence-steps.md#BKMK_SetDynamicVariables).*

Specifica il tag asset per il computer.

### <a name="_smstsbootimageid"></a><a name="SMSTSBootImageID"></a> _SMSTSBootImageID

Se la sequenza di attività attualmente in esecuzione fa riferimento a un pacchetto dell'immagine d'avvio, questa variabile archivia l'ID del pacchetto dell'immagine d'avvio. Se la sequenza di attività non fa riferimento a un pacchetto dell'immagine d'avvio, questa variabile non viene impostata.

#### <a name="example"></a>Esempio

`ABC00001`  

### <a name="_smstsbootuefi"></a><a name="SMSTSBootUEFI"></a> _SMSTSBootUEFI

La sequenza di attività imposta questa variabile quando rileva un computer in modalità UEFI.

### <a name="_smstsclientcache"></a><a name="SMSTSClientCache"></a> _SMSTSClientCache

<!-- SCCMDocs issue 1400 -->
La sequenza di attività imposta questa variabile quando memorizza il contenuto nella cache dell'unità locale. La variabile contiene il percorso della cache. Se questa variabile non esiste, la cache non è presente.

### <a name="_smstsclientguid"></a><a name="SMSTSClientGUID"></a> _SMSTSClientGUID

Archivia il valore del GUID del client di Configuration Manager. Se la sequenza di attività viene eseguita da un supporto autonomo, la variabile non viene impostata.

#### <a name="example"></a>Esempio

`0a1a9a4b-fc56-44f6-b7cd-c3f8ee37c04c`

### <a name="_smstscurrentactionname"></a><a name="SMSTSCurrentActionName"></a> _SMSTSCurrentActionName

Specifica il nome del passaggio della sequenza di attività attualmente in esecuzione. Questa variabile viene impostata prima che il motore di esecuzione della sequenza di attività esegua ogni singolo passaggio.

#### <a name="example"></a>Esempio

`run command line`

### <a name="_smstsdefaultgateways"></a><a name="SMSTSDefaultGateways"></a> _SMSTSDefaultGateways

*Si applica al passaggio [Imposta variabili dinamiche](task-sequence-steps.md#BKMK_SetDynamicVariables).*

Specifica i gateway predefiniti usati dal computer.

### <a name="_smstsdownloadondemand"></a><a name="SMSTSDownloadOnDemand"></a> _SMSTSDownloadOnDemand

Se la sequenza di attività corrente è in esecuzione in modalità di download su richiesta, questa variabile è `true`. La modalità di download su richiesta indica che il motore di esecuzione della sequenza di attività scarica il contenuto localmente solo quando deve accedere al contenuto.

### <a name="_smstsinwinpe"></a><a name="SMSTSInWinPE"></a> _SMSTSInWinPE

Quando il passaggio della sequenza di attività corrente è in esecuzione in Windows PE, questa variabile è `true`. Testare questa variabile della sequenza di attività per determinare l'ambiente del sistema operativo corrente.

### <a name="_smstsipaddresses"></a><a name="SMSTSIPAddresses"></a> _SMSTSIPAddresses

*Si applica al passaggio [Imposta variabili dinamiche](task-sequence-steps.md#BKMK_SetDynamicVariables).*

Specifica gli indirizzi IP usati dal computer.

### <a name="_smstslastactionname"></a><a name="SMSTSLastActionName"></a> _SMSTSLastActionName

Archivia il nome dell'ultima azione eseguita. Questa variabile è associata a **_SMSTSLastActionRetCode**. La sequenza di attività registra questi valori nel file smsts.log. Questa variabile è utile per la risoluzione dei problemi di una sequenza di attività. Quando un passaggio non riesce, uno script personalizzato può includere il nome del passaggio e il codice restituito.

### <a name="_smstslastactionretcode"></a><a name="SMSTSLastActionRetCode"></a> _SMSTSLastActionRetCode

Archivia il codice restituito dall'ultima azione eseguita. Questa variabile può essere usata come condizione per determinare se il passaggio successivo viene eseguito.

#### <a name="example"></a>Esempio

`0`

### <a name="_smstslastactionsucceeded"></a><a name="SMSTSLastActionSucceeded"></a> _SMSTSLastActionSucceeded

- Se l'ultimo passaggio è riuscito, questa variabile è `true`.  

- Se l'ultimo passaggio non è riuscito, è `false`.  

- Se la sequenza di attività ha ignorato l'ultima azione, perché il passaggio è disabilitato o la condizione associata ha restituito **false**, questa variabile non viene reimpostata. Mantiene ancora il valore dell'azione precedente.  

### <a name="_smstslastcontentdownloadlocation"></a><a name="SMSTSLastContentDownloadLocation"></a> _SMSTSLastContentDownloadLocation

<!-- 2840337 -->
A partire dalla versione 1906, questa variabile contiene l'ultimo percorso in cui la sequenza di attività ha scaricato o ha provato a scaricare contenuto. Esaminare questa variabile anziché analizzare i log del client per individuare il percorso del contenuto.

### <a name="_smstslaunchmode"></a><a name="SMSTSLaunchMode"></a> _SMSTSLaunchMode

Specifica che la sequenza di attività è stata avviata tramite uno dei metodi seguenti:  

- **SMS**: il client di Configuration Manager, ad esempio quando un utente la avvia da Software Center
- **UFD**: supporti USB legacy
- **UFD + FORMAT**: supporti USB più recenti
- **CD**: un CD di avvio
- **DVD**: un DVD di avvio
- **PXE**: avvio di rete con PXE
- **HD**: supporti pre-installati in un disco rigido

### <a name="_smstslogpath"></a><a name="SMSTSLogPath"></a> _SMSTSLogPath

Archivia il percorso completo della directory di log. Usare questo valore per determinare dove i passaggi della sequenza di attività registrano le azioni. Questo valore non viene impostato quando non è disponibile un disco rigido.

### <a name="_smstsmacaddresses"></a><a name="SMSTSMacAddresses"></a> _SMSTSMacAddresses

*Si applica al passaggio [Imposta variabili dinamiche](task-sequence-steps.md#BKMK_SetDynamicVariables).*

Specifica gli indirizzi MAC usati dal computer.

### <a name="_smstsmachinename"></a><a name="SMSTSMachineName"></a> _SMSTSMachineName

Archivia e specifica il nome del computer. Archivia il nome del computer che viene usato dalla sequenza di attività per registrare tutti i messaggi di stato. Per modificar il nome computer nel nuovo sistema operativo, usare la variabile [OSDComputerName](#OSDComputerName-input).

### <a name="_smstsmake"></a><a name="SMSTSMake"></a> _SMSTSMake

*Si applica al passaggio [Imposta variabili dinamiche](task-sequence-steps.md#BKMK_SetDynamicVariables).*

Specifica la marca del computer.

### <a name="_smstsmdatapath"></a><a name="SMSTSMDataPath"></a> _SMSTSMDataPath

Specifica il percorso definito dalla variabile [SMSTSLocalDataDrive](#SMSTSLocalDataDrive). Questo percorso specifica la posizione del computer di destinazione in cui la sequenza di attività archivia i file della cache temporanei durante l'esecuzione. Quando si definisce SMSTSLocalDataDrive prima dell'inizio della sequenza di attività, impostando ad esempio una variabile di raccolta, Configuration Manager definisce la variabile _SMSTSMDataPath dopo aver avviato la sequenza di attività.

### <a name="_smstsmediatype"></a><a name="SMSTSMediaType"></a> _SMSTSMediaType

Specifica il tipo di supporti usato per avviare l'installazione. Esempi di tipi di supporto sono supporti di avvio, supporti completi, PXE e supporti pre-installati.

### <a name="_smstsmodel"></a><a name="SMSTSModel"></a> _SMSTSModel

*Si applica al passaggio [Imposta variabili dinamiche](task-sequence-steps.md#BKMK_SetDynamicVariables).*

Specifica il modello del computer.

### <a name="_smstsmp"></a><a name="SMSTSMP"></a> _SMSTSMP

Archivia l'URL o l'indirizzo IP di un punto di gestione di Configuration Manager.

### <a name="_smstsmpport"></a><a name="SMSTSMPPort"></a> _SMSTSMPPort

Archivia il numero di porta di un punto di gestione di Configuration Manager.

### <a name="_smstsorgname"></a><a name="SMSTSOrgName"></a> _SMSTSOrgName

Archivia il nome titolo personalizzazione visualizzato dalla sequenza di attività nella finestra di dialogo relativa all'avanzamento.

### <a name="_smstsosupgradeactionreturncode"></a><a name="SMSTSOSUpgradeActionReturnCode"></a> _SMSTSOSUpgradeActionReturnCode

*Si applica al passaggio [Aggiorna sistema operativo](task-sequence-steps.md#BKMK_UpgradeOS).*

Archivia il valore del codice di uscita restituito da Installazione di Windows per indicare l'esito positivo o negativo. Questa variabile è utile con l'opzione della riga di comando `/Compat`.

#### <a name="example"></a>Esempio

Nei passaggi successivi al completamento di un'analisi compat-only eseguire un'azione diversa a seconda del codice di uscita (esito positivo o negativo) di questa opzione. In caso di esito positivo avviare l'aggiornamento oppure impostare un marcatore nell'ambiente per la raccolta con l'inventario hardware. Ad esempio, aggiungere un file o impostare una chiave del Registro di sistema. Usare questo marcatore per creare una raccolta di computer pronti per l'aggiornamento o da sottoporre a un'azione specifica prima dell'aggiornamento.

### <a name="_smstspackageid"></a><a name="SMSTSPackageID"></a> _SMSTSPackageID

Archivia l'ID della sequenza di attività in esecuzione. L'ID usa lo stesso formato dell'ID del pacchetto di Configuration Manager.

#### <a name="example"></a>Esempio

`HJT00001`

### <a name="_smstspackagename"></a><a name="SMSTSPackageName"></a> _SMSTSPackageName

Archivia il nome della sequenza di attività in esecuzione. Il nome viene specificato da un amministratore di Configuration Manager durante la creazione della sequenza di attività.

#### <a name="example"></a>Esempio

`Deploy Windows 10 task sequence`

### <a name="_smstsrunfromdp"></a><a name="SMSTSRunFromDP"></a> _SMSTSRunFromDP

Impostare su `true` se la sequenza di attività corrente è in esecuzione in modalità Esegui da punto di distribuzione. Questa modalità significa che il motore di esecuzione della sequenza di attività ottiene le condivisioni pacchetto richieste dal punto di distribuzione.

### <a name="_smstsserialnumber"></a><a name="SMSTSSerialNumber"></a> _SMSTSSerialNumber

*Si applica al passaggio [Imposta variabili dinamiche](task-sequence-steps.md#BKMK_SetDynamicVariables).*

Specifica il numero di serie del computer.

### <a name="_smstssetuprollback"></a><a name="SMSTSSetupRollback"></a> _SMSTSSetupRollback

Specifica se il programma di installazione di Windows ha eseguito un'operazione di ripristino dello stato precedente durante un aggiornamento sul posto. I valori possibili della variabile sono `true` o `false`.

### <a name="_smstssitecode"></a><a name="SMSTSSiteCode"></a> _SMSTSSiteCode

Archivia il codice del sito nel sito di Configuration Manager.

#### <a name="example"></a>Esempio

`ABC`

### <a name="_smststimezone"></a><a name="SMSTSTimezone"></a> _SMSTSTimezone

Questa variabile archivia le informazioni sul fuso orario nel formato seguente:

`Bias,StandardBias,DaylightBias,StandardDate.wYear,wMonth,wDayOfWeek,wDay,wHour,wMinute,wSecond,wMilliseconds,DaylightDate.wYear,wMonth,wDayOfWeek,wDay,wHour,wMinute,wSecond,wMilliseconds,StandardName,DaylightName`

#### <a name="example"></a>Esempio

Per il fuso orario **Fuso orientale (USA e Canada)** :

`300,0,-60,0,11,0,1,2,0,0,0,0,3,0,2,2,0,0,0,Eastern Standard Time,Eastern Daylight Time`

### <a name="_smststype"></a><a name="SMSTSType"></a> _SMSTSType

Specifica il tipo di sequenza di attività attualmente in esecuzione. Può avere uno dei valori seguenti:  

- **1**: sequenza di attività generica
- **2**: sequenza di attività di distribuzione del sistema operativo

### <a name="_smstsusecrl"></a><a name="SMSTSUseCRL"></a> _SMSTSUseCRL

Quando la sequenza di attività usa HTTPS per comunicare con il punto di gestione, questa variabile specifica se usa l'elenco di revoche di certificati (CRL).

### <a name="_smstsuserstarted"></a><a name="SMSTSUserStarted"></a> _SMSTSUserStarted

Specifica se un utente ha avviato la sequenza di attività. Questa variabile viene impostata solo se la sequenza di attività viene avviata da Software Center. Ad esempio, se la variabile [_SMSTSLaunchMode](#SMSTSLaunchMode) è impostata su `SMS`.

Questa variabile può avere i valori seguenti:  

- `true`: specifica che la sequenza di attività viene avviata manualmente da un utente da Software Center.  

- `false`: specifica che la sequenza di attività viene avviata automaticamente dall'utilità di pianificazione di Configuration Manager.

### <a name="_smstsusessl"></a><a name="SMSTSUseSSL"></a> _SMSTSUseSSL

Specifica se la sequenza di attività usa SSL per comunicare con il punto di gestione di Configuration Manager. Se si configurano i sistemi del sito per HTTPS, il valore viene impostato su `true`.

### <a name="_smstsuuid"></a><a name="SMSTSUUID"></a> _SMSTSUUID

*Si applica al passaggio [Imposta variabili dinamiche](task-sequence-steps.md#BKMK_SetDynamicVariables).*

Specifica l'UUID del computer.

### <a name="_smstswtg"></a><a name="SMSTSWTG"></a> _SMSTSWTG

specifica se il computer è in esecuzione come dispositivo Windows To Go.

### <a name="_ts_crmemory"></a><a name="TSCRMEMORY"></a> _TS_CRMEMORY

*A partire dalla versione 2002* <!--6005561-->  
*Si applica al passaggio [Verifica conformità](task-sequence-steps.md#BKMK_CheckReadiness).*

Variabile di sola lettura che indica se il controllo di **Memoria minima (MB)** ha restituito true (`1`) o false (`0`). Se non si abilita il controllo, il valore di questa variabile di sola lettura è vuoto.

### <a name="_ts_crspeed"></a><a name="TSCRSPEED"></a> _TS_CRSPEED

*A partire dalla versione 2002* <!--6005561-->  
*Si applica al passaggio [Verifica conformità](task-sequence-steps.md#BKMK_CheckReadiness).*

Variabile di sola lettura che indica se il controllo di **Velocità minima del processore (MHz)** ha restituito true (`1`) o false (`0`). Se non si abilita il controllo, il valore di questa variabile di sola lettura è vuoto.

### <a name="_ts_crdisk"></a><a name="TSCRDISK"></a> _TS_CRDISK

*A partire dalla versione 2002* <!--6005561-->  
*Si applica al passaggio [Verifica conformità](task-sequence-steps.md#BKMK_CheckReadiness).*

Variabile di sola lettura che indica se il controllo di **Spazio disponibile su disco minimo (MB)** ha restituito true (`1`) o false (`0`). Se non si abilita il controllo, il valore di questa variabile di sola lettura è vuoto.

### <a name="_ts_crostype"></a><a name="TSCROSTYPE"></a> _TS_CROSTYPE

*A partire dalla versione 2002* <!--6005561-->  
*Si applica al passaggio [Verifica conformità](task-sequence-steps.md#BKMK_CheckReadiness).*

Variabile di sola lettura che indica se il controllo di **Il sistema operativo corrente da aggiornare è** ha restituito true (`1`) o false (`0`). Se non si abilita il controllo, il valore di questa variabile di sola lettura è vuoto.

### <a name="_ts_crarch"></a><a name="TSCRARCH"></a> _TS_CRARCH

*A partire dalla versione 2002* <!--6005561-->  
*Si applica al passaggio [Verifica conformità](task-sequence-steps.md#BKMK_CheckReadiness).*

Variabile di sola lettura che indica se il controllo di **Architettura del sistema operativo corrente** ha restituito true (`1`) o false (`0`). Se non si abilita il controllo, il valore di questa variabile di sola lettura è vuoto.

### <a name="_ts_crminosver"></a><a name="TSCRMINOSVER"></a> _TS_CRMINOSVER

*A partire dalla versione 2002* <!--6005561-->  
*Si applica al passaggio [Verifica conformità](task-sequence-steps.md#BKMK_CheckReadiness).*

Variabile di sola lettura che indica se il controllo di **Versione minima del sistema operativo** ha restituito true (`1`) o false (`0`). Se non si abilita il controllo, il valore di questa variabile di sola lettura è vuoto.

### <a name="_ts_crmaxosver"></a><a name="TSCRMAXOSVER"></a> _TS_CRMAXOSVER

*A partire dalla versione 2002* <!--6005561-->  
*Si applica al passaggio [Verifica conformità](task-sequence-steps.md#BKMK_CheckReadiness).*

Variabile di sola lettura che indica se il controllo di **Versione massima del sistema operativo** ha restituito true (`1`) o false (`0`). Se non si abilita il controllo, il valore di questa variabile di sola lettura è vuoto.

### <a name="_ts_crclientminver"></a><a name="TSCRCLIENTMINVER"></a> _TS_CRCLIENTMINVER

*A partire dalla versione 2002* <!--6005561-->  
*Si applica al passaggio [Verifica conformità](task-sequence-steps.md#BKMK_CheckReadiness).*

Variabile di sola lettura che indica se il controllo di **Versione minima del client** ha restituito true (`1`) o false (`0`). Se non si abilita il controllo, il valore di questa variabile di sola lettura è vuoto.

### <a name="_ts_croslanguage"></a><a name="TSCROSLANGUAGE"></a> _TS_CROSLANGUAGE

*A partire dalla versione 2002* <!--6005561-->  
*Si applica al passaggio [Verifica conformità](task-sequence-steps.md#BKMK_CheckReadiness).*

Variabile di sola lettura che indica se il controllo di **Lingua del sistema operativo corrente** ha restituito true (`1`) o false (`0`). Se non si abilita il controllo, il valore di questa variabile di sola lettura è vuoto.

### <a name="_ts_cracpower"></a><a name="TSCRACPOWER"></a> _TS_CRACPOWER

*A partire dalla versione 2002* <!--6005561-->  
*Si applica al passaggio [Verifica conformità](task-sequence-steps.md#BKMK_CheckReadiness).*

Variabile di sola lettura che indica se il controllo di **Alimentazione da rete elettrica collegata** ha restituito true (`1`) o false (`0`). Se non si abilita il controllo, il valore di questa variabile di sola lettura è vuoto.

### <a name="_ts_crnetwork"></a><a name="TSCRNETWORK"></a> _TS_CRNETWORK

*A partire dalla versione 2002* <!--6005561-->  
*Si applica al passaggio [Verifica conformità](task-sequence-steps.md#BKMK_CheckReadiness).*

Variabile di sola lettura che indica se il controllo di **Scheda di rete connessa** ha restituito true (`1`) o false (`0`). Se non si abilita il controllo, il valore di questa variabile di sola lettura è vuoto.

### <a name="_ts_cruefi"></a><a name="TSCRUEFI"></a> _TS_CRUEFI

*A partire dalla versione 2006* <!--6452769-->
*Si applica al passaggio [Verifica conformità](task-sequence-steps.md#BKMK_CheckReadiness).*

Variabile di sola lettura che indica che **Computer is in UEFI mode** (Computer in modalità UEFI) ha restituito il valore BIOS (`0`) o UEFI (`1`). Se non si abilita il controllo, il valore di questa variabile di sola lettura è vuoto.

### <a name="_ts_crwired"></a><a name="TSCRWIRED"></a> _TS_CRWIRED

*A partire dalla versione 2002* <!--6005561-->  
*Si applica al passaggio [Verifica conformità](task-sequence-steps.md#BKMK_CheckReadiness).*

Variabile di sola lettura che indica se il controllo di **La scheda di rete non è wireless** ha restituito true (`1`) o false (`0`). Se non si abilita il controllo, il valore di questa variabile di sola lettura è vuoto.

### <a name="_tsappinstallstatus"></a><a name="TSAppInstallStatus"></a> _TSAppInstallStatus

La sequenza di attività imposta questa variabile con lo stato di installazione dell'applicazione durante il passaggio [Installa applicazione](task-sequence-steps.md#BKMK_InstallApplication). Imposta uno dei valori seguenti:  

- **Non definito**: il passaggio Installa applicazione non è stato eseguito.  

- **Errore**: non è stato possibile eseguire almeno un'applicazione a causa di un errore durante il passaggio Installa applicazione.  

- **Avviso**: non si sono verificati errori durante il passaggio Installa applicazione. Una o più applicazioni oppure una dipendenza necessaria non sono state installate perché un requisito non è stato soddisfatto.  

- **Operazione riuscita**: impostato quando non vengono rilevati errori o avvisi durante il passaggio Installa applicazione.  

### <a name="_tssecureboot"></a><a name="TSSecureBoot"></a> _TSSecureBoot

*A partire dalla versione 2002* <!--5842295-->  

Usare questa variabile per determinare lo stato dell'avvio protetto in un dispositivo abilitato per UEFI. La variabile può avere uno dei valori seguenti:

- `NA`: il valore del Registro di sistema associato non esiste, il che significa che il dispositivo non supporta l'avvio protetto.
- `Enabled`: l'avvio protetto è abilitato per il dispositivo.
- `Disabled`: l'avvio protetto è disabilitato per il dispositivo.

### <a name="osdadapter"></a><a name="OSDAdapter"></a> OSDAdapter

*Si applica al passaggio [Applica impostazioni di rete](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

(input)

Questa variabile della sequenza di attività è una variabile *matrice*. Ogni elemento della matrice rappresenta le impostazioni per una singola scheda di rete nel computer. Accedere alle impostazioni per ogni scheda combinando il nome della variabile di matrice con l'indice in base zero della scheda di rete e il nome della proprietà.

Se il passaggio Applica impostazioni di rete configura più schede di rete, definisce le proprietà per la *seconda* scheda di rete usando l'indice **1** nel nome della variabile. Ad esempio: OSDAdapter1EnableDHCP, OSDAdapter1IPAddressList e OSDAdapter1DNSDomain.

Usare i nomi di variabile seguenti per definire le proprietà per configurare la *prima* scheda di rete per questo passaggio:

#### <a name="osdadapter0enabledhcp"></a>OSDAdapter0EnableDHCP

Questa impostazione è necessaria. I possibili valori sono `True` o `False`. Ad esempio:

`true`: abilitare il protocollo DHCP (Dynamic Host Configuration Protocol) per la scheda

#### <a name="osdadapter0ipaddresslist"></a>OSDAdapter0IPAddressList

Elenco di indirizzi IP delimitati da virgole per la scheda. Questa proprietà viene ignorata a meno che il valore di **EnableDHCP** non sia impostato su `false`. Questa impostazione è necessaria.

#### <a name="osdadapter0subnetmask"></a>OSDAdapter0SubnetMask

Elenco delimitato da virgole di subnet mask. Questa proprietà viene ignorata a meno che il valore di **EnableDHCP** non sia impostato su `false`. Questa impostazione è necessaria.

#### <a name="osdadapter0gateways"></a>OSDAdapter0Gateways

Elenco di indirizzi IP del gateway delimitati da virgole. Questa proprietà viene ignorata a meno che il valore di **EnableDHCP** non sia impostato su `false`. Questa impostazione è necessaria.

#### <a name="osdadapter0dnsdomain"></a>OSDAdapter0DNSDomain

Dominio DNS (Domain Name System) per la scheda.

#### <a name="osdadapter0dnsserverlist"></a>OSDAdapter0DNSServerList

Elenco di server DNS delimitati da virgole per la scheda. Questa impostazione è necessaria.

#### <a name="osdadapter0enablednsregistration"></a>OSDAdapter0EnableDNSRegistration

Impostare su `true` per registrare l'indirizzo IP per la scheda in DNS.

#### <a name="osdadapter0enablefulldnsregistration"></a>OSDAdapter0EnableFullDNSRegistration

Impostare su `true` per registrare l'indirizzo IP per la scheda in DNS con il nome DNS completo per il computer.

#### <a name="osdadapter0enableipprotocolfiltering"></a>OSDAdapter0EnableIPProtocolFiltering

Impostare su `true` per abilitare il filtro del protocollo IP nella scheda.

#### <a name="osdadapter0ipprotocolfilterlist"></a>OSDAdapter0IPProtocolFilterList

Elenco di protocolli delimitati da virgole di cui è consentita l'esecuzione su IP. Questa proprietà viene ignorata se **EnableIPProtocolFiltering** è impostato su `false`.

#### <a name="osdadapter0enabletcpfiltering"></a>OSDAdapter0EnableTCPFiltering

Impostare su `true` per abilitare il filtro della porta TCP per la scheda.

#### <a name="osdadapter0tcpfilterportlist"></a>OSDAdapter0TCPFilterPortList

Elenco di porte delimitate da virgole a cui concedere le autorizzazioni di accesso per TCP. Questa proprietà viene ignorata se il valore di **EnableTCPFiltering** è impostato su `false`.

#### <a name="osdadapter0tcpipnetbiosoptions"></a>OSDAdapter0TcpipNetbiosOptions

Opzioni per NetBIOS su TCP/IP. I possibili valori sono i seguenti:  

- `0`: usa le impostazioni NetBIOS del server DHCP  
- `1`: abilita NetBIOS su TCP/IP  
- `2`: disabilita NetBIOS su TCP/IP  

#### <a name="osdadapter0enablewins"></a>OSDAdapter0EnableWINS

Impostare su `true` per usare WINS per la risoluzione dei nomi.

#### <a name="osdadapter0winsserverlist"></a>OSDAdapter0WINSServerList

Elenco di indirizzi IP del server WINS delimitati da virgole. Questa proprietà viene ignorata a meno che il valore di **EnableWINS** non sia impostato su `true`.

#### <a name="osdadapter0macaddress"></a>OSDAdapter0MacAddress

Indirizzo MAC usato per mettere in corrispondenza le impostazioni con la scheda di rete fisica.

#### <a name="osdadapter0name"></a>OSDAdapter0Name

Nome della connessione di rete visualizzato nel pannello di controllo delle connessioni di rete. Il nome è composto da un numero di caratteri compreso tra 0 e 255.

#### <a name="osdadapter0index"></a>OSDAdapter0Index

Indice delle impostazioni della scheda di rete nella matrice di impostazioni.

#### <a name="example"></a>Esempio

- **OSDAdapterCount** = `1`  
- **OSDAdapter0EnableDHCP** = `FALSE`  
- **OSDAdapter0IPAddressList** = `192.168.0.40`  
- **OSDAdapter0SubnetMask** = `255.255.255.0`  
- **OSDAdapter0Gateways** = `192.168.0.1`  
- **OSDAdapter0DNSSuffix** = `contoso.com`  

### <a name="osdadaptercount"></a><a name="OSDAdapterCount"></a> OSDAdapterCount

*Si applica al passaggio [Applica impostazioni di rete](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

(input)

Specifica il numero di schede di rete installate nel computer di destinazione. Quando si imposta il valore di **OSDAdapterCount**, impostare anche tutte le opzioni di configurazione per ogni scheda.

Ad esempio, se si imposta il valore di **OSDAdapter0TCPIPNetbiosOptions** per la prima scheda, è necessario configurare anche tutti i valori per tale scheda.

Se non si specifica questo valore, la sequenza di attività ignora tutti i valori **OSDAdapter**.

### <a name="osdapplydriverbootcriticalcontentuniqueid"></a><a name="OSDApplyDriverBootCriticalContentUniqueID"></a> OSDApplyDriverBootCriticalContentUniqueID

*Si applica al passaggio [Applica pacchetto di driver](task-sequence-steps.md#BKMK_ApplyDriverPackage).*

(input)

Specifica l'ID contenuto del driver di dispositivo di archiviazione di massa da installare dal pacchetto di driver. Se questa variabile non viene specificata, non viene installato alcun driver di archiviazione di massa.

### <a name="osdapplydriverbootcriticalhardwarecomponent"></a><a name="OSDApplyDriverBootCriticalHardwareComponent"></a> OSDApplyDriverBootCriticalHardwareComponent

*Si applica al passaggio [Applica pacchetto di driver](task-sequence-steps.md#BKMK_ApplyDriverPackage).*

(input)

Specifica se è installato un driver del dispositivo di archiviazione di massa. La variabile deve essere **scsi**.

Se si imposta [OSDApplyDriverBootCriticalContentUniqueID](#OSDApplyDriverBootCriticalContentUniqueID) questa variabile è obbligatoria.

### <a name="osdapplydriverbootcriticalid"></a><a name="OSDApplyDriverBootCriticalID"></a> OSDApplyDriverBootCriticalID

*Si applica al passaggio [Applica pacchetto di driver](task-sequence-steps.md#BKMK_ApplyDriverPackage).*

(input)

Specifica l'ID critico per l'avvio del driver di dispositivo di archiviazione di massa da installare. Questo ID è elencato nella sezione **scsi** del file txtsetup.oem del driver del dispositivo.

Se si imposta [OSDApplyDriverBootCriticalContentUniqueID](#OSDApplyDriverBootCriticalContentUniqueID) questa variabile è obbligatoria.

### <a name="osdapplydriverbootcriticalinffile"></a><a name="OSDApplyDriverBootCriticalINFFile"></a> OSDApplyDriverBootCriticalINFFile

*Si applica al passaggio [Applica pacchetto di driver](task-sequence-steps.md#BKMK_ApplyDriverPackage).*

(input)

Specifica il file INF del driver di archiviazione di massa da installare.

Se si imposta [OSDApplyDriverBootCriticalContentUniqueID](#OSDApplyDriverBootCriticalContentUniqueID) questa variabile è obbligatoria.

### <a name="osdautoapplydriverbestmatch"></a><a name="OSDAutoApplyDriverBestMatch"></a> OSDAutoApplyDriverBestMatch

*Si applica al passaggio [Applica automaticamente i driver](task-sequence-steps.md#BKMK_AutoApplyDrivers).*

(input)

Se nel catalogo driver ci sono più driver di dispositivo compatibili con un dispositivo hardware, questa variabile determina l'azione del passaggio.

#### <a name="valid-values"></a>Valori validi

- `true` (impostazione predefinita): installa solo il driver di dispositivo migliore  

- `false`: installa tutti i driver di dispositivo compatibili e Windows sceglie il driver migliore da usare  

### <a name="osdautoapplydrivercategorylist"></a><a name="OSDAutoApplyDriverCategoryList"></a> OSDAutoApplyDriverCategoryList

*Si applica al passaggio [Applica automaticamente i driver](task-sequence-steps.md#BKMK_AutoApplyDrivers).*

(input)

Elenco delimitato da virgole di ID categoria univoci del catalogo driver. Il passaggio **Applica automaticamente i driver** considera solo i driver in almeno una delle categorie specificate. Questo valore è facoltativo e non specificato per impostazione predefinita. Ottenere gli ID categoria disponibili enumerando l'elenco di oggetti **SMS_CategoryInstance** nel sito.

### <a name="osdbitlockerrebootcount"></a><a name="OSDBitLockerRebootCount"></a> OSDBitLockerRebootCount

*Si applica al passaggio [Disattiva BitLocker](task-sequence-steps.md#BKMK_DisableBitLocker).*

<!-- 4512937 -->
A partire dalla versione 1906, usare questa variabile per impostare il numero di riavvii dopo i quali riprendere la protezione.

#### <a name="valid-values"></a>Valori validi

Un numero intero compreso tra `1` e `15`.

### <a name="osdbitlockerrebootcountoverride"></a><a name="OSDBitLockerRebootCountOverride"></a> OSDBitLockerRebootCountOverride

*Si applica al passaggio [Disattiva BitLocker](task-sequence-steps.md#BKMK_DisableBitLocker).*

<!-- 4512937 -->
A partire dalla versione 1906, impostare questo valore per eseguire l'override del conteggio impostato dal passaggio o dalla variabile [OSDBitLockerRebootCount](#OSDBitLockerRebootCount). Mentre gli altri metodi accettano solo i valori da 1 a 15, se si imposta questa variabile su 0, BitLocker rimane disattivato per un periodo indefinito. Questa variabile è utile quando la sequenza di attività imposta un solo valore, ma si vuole impostare un valore distinto per ogni dispositivo o per ogni raccolta.

#### <a name="valid-values"></a>Valori validi

Un numero intero compreso tra `0` e `15`.

### <a name="osdbitlockerrecoverypassword"></a><a name="OSDBitLockerRecoveryPassword"></a> OSDBitLockerRecoveryPassword

*Si applica al passaggio [Attiva BitLocker](task-sequence-steps.md#BKMK_EnableBitLocker).*

(input)

Invece di generare una password di ripristino casuale, il passaggio **Attiva BitLocker** usa il valore specificato come password di ripristino. Il valore deve essere una password di ripristino di BitLocker numerica valida.

### <a name="osdbitlockerstartupkey"></a><a name="OSDBitLockerStartupKey"></a> OSDBitLockerStartupKey

*Si applica al passaggio [Attiva BitLocker](task-sequence-steps.md#BKMK_EnableBitLocker).*

(input)

Invece di generare una chiave di avvio casuale per l'opzione **Chiave di avvio solo su USB** per la gestione delle chiavi, il passaggio **Attiva BitLocker** usa il modulo TPM (Trusted Platform Module) come chiave di avvio. Il valore deve essere una chiave di avvio di BitLocker con codifica Base64 a 256 bit valida.

### <a name="osdcaptureaccount"></a><a name="OSDCaptureAccount"></a> OSDCaptureAccount

*Si applica al passaggio [Acquisisci immagine del sistema operativo](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).*

(input)

Specifica un nome account di Windows con le autorizzazioni per l'archiviazione dell'immagine acquisita in una condivisione di rete ([OSDCaptureDestination](#OSDCaptureDestination)). Specificare anche [OSDCaptureAccountPassword](#OSDCaptureAccountPassword).

Per altre informazioni sull'account per l'acquisizione dell'immagine del sistema operativo, vedere [Account](../../core/plan-design/hierarchy/accounts.md#capture-os-image-account).

### <a name="osdcaptureaccountpassword"></a><a name="OSDCaptureAccountPassword"></a> OSDCaptureAccountPassword

*Si applica al passaggio [Acquisisci immagine del sistema operativo](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).*

(input)

Specifica la password per l'account di Windows ([OSDCaptureAccount](#OSDCaptureAccount)) usato per archiviare l'immagine acquisita in una condivisione di rete ([OSDCaptureDestination](#OSDCaptureDestination)).

### <a name="osdcapturedestination"></a><a name="OSDCaptureDestination"></a> OSDCaptureDestination

*Si applica al passaggio [Acquisisci immagine del sistema operativo](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).*

(input)

Specifica la posizione in cui la sequenza di attività salva l'immagine del sistema operativo acquisita. La lunghezza massima del nome directory è di 255 caratteri. Se la condivisione di rete richiede l'autenticazione, specificare le variabili [OSDCaptureAccount](#OSDCaptureAccount) e [OSDCaptureAccountPassword](#OSDCaptureAccountPassword).

### <a name="osdcomputername-input"></a><a name="OSDComputerName-input"></a> OSDComputerName (input)

*Si applica al passaggio [Applica impostazioni Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

Specifica il nome del computer di destinazione.

#### <a name="example"></a>Esempio

`%_SMSTSMachineName%` (impostazione predefinita)

### <a name="osdcomputername-output"></a><a name="OSDComputerName-output"></a> OSDComputerName (output)

*Si applica al passaggio [Acquisisci impostazioni Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings).*

Valore impostato sul nome NetBIOS del computer. Il valore viene impostato solo se la variabile [OSDMigrateComputerName](#OSDMigrateComputerName) è impostata su `true`.

### <a name="osdconfigfilename"></a><a name="OSDConfigFileName"></a> OSDConfigFileName

*Si applica al passaggio [Applica immagine del sistema operativo](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).*

(input)

Specifica il nome del file di risposte per la distribuzione del sistema operativo associato al pacchetto dell'immagine di distribuzione del sistema operativo.  

### <a name="osddataimageindex"></a><a name="OSDDataImageIndex"></a> OSDDataImageIndex

*Si applica al passaggio [Applica immagine dei dati](task-sequence-steps.md#BKMK_ApplyDataImage).*

(input)

Specifica il valore di indice dell'immagine che viene applicata al computer di destinazione.

### <a name="osddiskindex"></a><a name="OSDDiskIndex"></a> OSDDiskIndex

*Si applica al passaggio [Formato e disco partizione](task-sequence-steps.md#BKMK_FormatandPartitionDisk).*

(input)

Specifica il numero del disco fisico da partizionare.

### <a name="osddnsdomain"></a><a name="OSDDNSDomain"></a> OSDDNSDomain

*Si applica al passaggio [Applica impostazioni di rete](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

(input)

Specifica il server DNS primario usato dal computer di destinazione.

### <a name="osddnssuffixsearchorder"></a><a name="OSDDNSSuffixSearchOrder"></a> OSDDNSSuffixSearchOrder

*Si applica al passaggio [Applica impostazioni di rete](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

(input)

Specifica l'ordine di ricerca DNS per il computer di destinazione.

### <a name="osddomainname"></a><a name="OSDDomainName"></a> OSDDomainName

*Si applica al passaggio [Applica impostazioni di rete](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

(input)

Specifica il nome del dominio di Active Directory a cui viene aggiunto il computer di destinazione. Il valore specificato deve essere un nome di dominio di Servizi di dominio Active Directory valido.

### <a name="osddomainouname"></a><a name="OSDDomainOUName"></a> OSDDomainOUName

*Si applica al passaggio [Applica impostazioni di rete](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

(input)

Specifica il nome in formato RFC 1779 dell'unità organizzativa (OU) a cui viene aggiunto il computer di destinazione. Se specificato, il valore deve contenere il percorso completo.

#### <a name="example"></a>Esempio

`LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com`

### <a name="osddonotlogcommand"></a><a name="OSDDoNotLogCommand"></a> OSDDoNotLogCommand

<!--1358493-->
*Si applica al passaggio [Installa pacchetto](task-sequence-steps.md#BKMK_InstallPackage).*

*A partire dalla versione 1902*  
*Si applica al passaggio [Esegui riga di comando](task-sequence-steps.md#BKMK_RunCommandLine).*

(input)

Per impedire la visualizzazione o la registrazione di dati potenzialmente sensibili, impostare la variabile su `TRUE`. Questa variabile maschera il nome del programma in **smsts.log** durante il passaggio **Installa pacchetto**.

A partire dalla versione 1902, quando si imposta questa variabile su `TRUE`, viene nascosta anche la riga di comando del passaggio **Esegui riga di comando** nel file di log.<!--3654172-->

### <a name="osdenabletcpipfiltering"></a><a name="OSDEnableTCPIPFiltering"></a> OSDEnableTCPIPFiltering

*Si applica al passaggio [Applica impostazioni di rete](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

(input)

Specifica se il filtro TCP/IP è abilitato.

#### <a name="valid-values"></a>Valori validi

- `true`  
- `false` (impostazione predefinita)  

### <a name="osdgptbootdisk"></a><a name="OSDGPTBootDisk"></a> OSDGPTBootDisk

*Si applica al passaggio [Formato e disco partizione](task-sequence-steps.md#BKMK_FormatandPartitionDisk).*

(input)

Specifica se creare una partizione EFI su un disco rigido GPT. I computer basati su EFI usano questa partizione come disco di avvio.

#### <a name="valid-values"></a>Valori validi

- `true`  
- `false` (impostazione predefinita)

### <a name="osdimagecreator"></a><a name="OSDImageCreator"></a> OSDImageCreator

*Si applica al passaggio [Acquisisci immagine del sistema operativo](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).*

(input)

Nome facoltativo dell'utente che ha creato l'immagine. Questo nome viene archiviato nel file WIM. La lunghezza massima del nome utente è di 255 caratteri.

### <a name="osdimagedescription"></a><a name="OSDImageDescription"></a> OSDImageDescription

*Si applica al passaggio [Acquisisci immagine del sistema operativo](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).*

(input)

Descrizione facoltativa definita dall'utente dell'immagine del sistema operativo acquisita. Questa descrizione viene archiviata nel file WIM. La lunghezza massima della descrizione è di 255 caratteri.

### <a name="osdimageindex"></a><a name="OSDImageIndex"></a> OSDImageIndex

*Si applica al passaggio [Applica immagine del sistema operativo](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).*

(input)

Specifica il valore di indice dell'immagine del file WIM applicato al computer di destinazione.

### <a name="osdimageversion"></a><a name="OSDImageVersion"></a> OSDImageVersion

*Si applica al passaggio [Acquisisci immagine del sistema operativo](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).*

(input)

Numero di versione facoltativo definito dall'utente da assegnare all'immagine del sistema operativo acquisita. Questo numero di versione viene archiviato nel file WIM. Questo valore può essere costituito da qualsiasi combinazione di caratteri alfanumerici, con una lunghezza massima di 32 caratteri.

### <a name="osdinstalldriversadditionaloptions"></a><a name="OSDInstallDriversAdditionalOptions"></a> OSDInstallDriversAdditionalOptions

<!--516679/2840016-->
*Si applica al passaggio [Applica pacchetto di driver](task-sequence-steps.md#BKMK_ApplyDriverPackage).*

(input)

Specifica opzioni aggiuntive da aggiungere alla riga di comando di DISM durante l'applicazione di un pacchetto di driver. La sequenza di attività non verifica le opzioni della riga di comando.

Per usare questa variabile, abilitare l'impostazione **Installa il pacchetto driver eseguendo DISM con l'opzione di ricorsione** nel passaggio **Applica pacchetto di driver**.

Per altre informazioni, vedere [Windows 10 DISM Command-Line Options](/windows-hardware/manufacture/desktop/deployment-image-servicing-and-management--dism--command-line-options) (Opzioni della riga di comando di DISM Windows 10).

### <a name="osdjoinaccount"></a><a name="OSDJoinAccount"></a> OSDJoinAccount

*Si applica ai passaggi seguenti:*  

- [Applica impostazioni di rete](task-sequence-steps.md#BKMK_ApplyNetworkSettings)  
- [Aggiunta a dominio o gruppo di lavoro](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)  

(input)

Specifica l'account utente di dominio usato per aggiungere il computer di destinazione al dominio. Questa variabile è obbligatoria per l'aggiunta a un dominio.

Per altre informazioni sull'account di aggiunta del dominio della sequenza di attività, vedere [Account](../../core/plan-design/hierarchy/accounts.md#task-sequence-domain-join-account).

### <a name="osdjoindomainname"></a><a name="OSDJoinDomainName"></a> OSDJoinDomainName

*Si applica al passaggio [Aggiunta a dominio o gruppo di lavoro](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup).*

(input)

Specifica il nome di un dominio di Active Directory a cui viene aggiunto il computer di destinazione. La lunghezza del nome di dominio deve essere compresa tra 1 e 255 caratteri.

### <a name="osdjoindomainouname"></a><a name="OSDJoinDomainOUName"></a> OSDJoinDomainOUName

*Si applica al passaggio [Aggiunta a dominio o gruppo di lavoro](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup).*

(input)

Specifica il nome in formato RFC 1779 dell'unità organizzativa (OU) a cui viene aggiunto il computer di destinazione. Se specificato, il valore deve contenere il percorso completo. La lunghezza del nome OU deve essere compresa tra 0 e 32.767 caratteri. Questo valore non è impostato se la variabile [OSDJoinType](#OSDJoinType) è impostata su `1` (aggiunta a un gruppo di lavoro).

#### <a name="example"></a>Esempio

`LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com`  

### <a name="osdjoinpassword"></a><a name="OSDJoinPassword"></a> OSDJoinPassword

*Si applica ai passaggi seguenti:*  

- [Applica impostazioni di rete](task-sequence-steps.md#BKMK_ApplyNetworkSettings)  
- [Aggiunta a dominio o gruppo di lavoro](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)  

(input)

Specifica la password per l'account [OSDJoinAccount](#OSDJoinAccount) usato dal computer di destinazione per l'aggiunta al dominio di Active Directory. Se l'ambiente della sequenza di attività non include questa variabile, Installazione di Windows prova una password vuota. Se la variabile [OSDJoinType](#OSDJoinType) è impostata su `0` (aggiunta a un dominio), questo valore è obbligatorio.

### <a name="osdjoinskipreboot"></a><a name="OSDJoinSkipReboot"></a> OSDJoinSkipReboot

*Si applica al passaggio [Aggiunta a dominio o gruppo di lavoro](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup).*

(input)

Specifica se ignorare il riavvio dopo l'aggiunta del computer di destinazione al dominio o al gruppo di lavoro.

#### <a name="valid-values"></a>Valori validi

- `true`  
- `false`  

### <a name="osdjointype"></a><a name="OSDJoinType"></a> OSDJoinType

*Si applica al passaggio [Aggiunta a dominio o gruppo di lavoro](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup).*

(input)

Specifica se il computer di destinazione viene aggiunto a un gruppo di lavoro o a un dominio Windows.

#### <a name="valid-values"></a>Valori validi

- `0`: aggiunge il computer di destinazione a un dominio Windows  
- `1`: aggiunge il computer di destinazione a un gruppo di lavoro  

### <a name="osdjoinworkgroupname"></a><a name="OSDJoinWorkgroupName"></a> OSDJoinWorkgroupName

*Si applica al passaggio [Aggiunta a dominio o gruppo di lavoro](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup).*

(input)

Specifica il nome del gruppo di lavoro a cui viene aggiunto il computer di destinazione. La lunghezza del nome del gruppo di lavoro deve essere compresa tra 1 e 32 caratteri.

### <a name="osdkeepactivation"></a><a name="OSDKeepActivation"></a> OSDKeepActivation

*Si applica al passaggio [Prepara Windows per l'acquisizione](task-sequence-steps.md#BKMK_PrepareWindowsforCapture).*

(input)

Specifica se sysprep mantiene o reimposta il flag di attivazione del prodotto.

#### <a name="valid-values"></a>Valori validi

- `true`: mantiene il flag di attivazione
- `false` (impostazione predefinita): reimposta il flag di attivazione

### <a name="osdlocaladminpassword"></a><a name="OSDLocalAdminPassword"></a> OSDLocalAdminPassword

*Si applica al passaggio [Applica impostazioni Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

(input)

Specifica la password dell'account amministratore locale. Se si abilita l'opzione **Genera in modo casuale la password dell'amministratore locale e disattiva l'account su tutte le piattaforme supportate**, il passaggio ignora questa variabile. Il valore specificato deve essere compreso tra 1 e 255 caratteri.

### <a name="osdlogpowershellparameters"></a><a name="OSDLogPowerShellParameters"></a> OSDLogPowerShellParameters

<!--3556028-->
*A partire dalla versione 1902*  
*Si applica al passaggio [Esegui script PowerShell](task-sequence-steps.md#BKMK_RunPowerShellScript).*

(input)

Per evitare la registrazione di dati potenzialmente sensibili, il passaggio **Esegui script PowerShell** non registra i parametri dello script nel file **smsts.log**. Per includere i parametri dello script nel log della sequenza di attività, impostare questa variabile su **TRUE**.

### <a name="osdmigrateadaptersettings"></a><a name="OSDMigrateAdapterSettings"></a> OSDMigrateAdapterSettings

*Si applica al passaggio [Acquisisci impostazioni di rete](task-sequence-steps.md#BKMK_CaptureNetworkSettings).*

(input)

Specifica se la sequenza di attività acquisisce le informazioni sulla scheda di rete. Queste informazioni includono le impostazioni di configurazione per TCP/IP, DNS e WINS.

#### <a name="valid-values"></a>Valori validi

- `true` (impostazione predefinita)
- `false`

### <a name="osdmigrateadditionalcaptureoptions"></a><a name="OSDMigrateAdditionalCaptureOptions"></a> OSDMigrateAdditionalCaptureOptions

*Si applica al passaggio [Acquisisci stato utente](task-sequence-steps.md#BKMK_CaptureUserState).*

(input)

Specificare le opzioni aggiuntive della riga di comando dell'Utilità di migrazione stato utente (USMT, User State Migration Tool) che vengono usate dalla sequenza di attività per acquisire lo stato utente. Il passaggio non espone queste impostazioni nell'editor delle sequenze di attività. Specificare queste opzioni come stringa, che la sequenza di attività aggiunge alla riga di comando USMT generata automaticamente per ScanState.

Le opzioni USMT specificate con questa variabile della sequenza di attività non vengono convalidate per verificarne l'accuratezza prima di eseguire la sequenza di attività.

Per altre informazioni sulle opzioni disponibili, vedere [ScanState Syntax](https://docs.microsoft.com/windows/deployment/usmt/usmt-scanstate-syntax) (Sintassi di ScanState).

### <a name="osdmigrateadditionalrestoreoptions"></a><a name="OSDMigrateAdditionalRestoreOptions"></a> OSDMigrateAdditionalRestoreOptions

*Si applica al passaggio [Ripristina stato utente](task-sequence-steps.md#BKMK_RestoreUserState).*

(input)

Specifica le opzioni aggiuntive della riga di comando dell'Utilità di migrazione stato utente (USMT, User State Migration Tool) che vengono usate dalla sequenza di attività per ripristinare lo stato utente. Specificare le opzioni aggiuntive come stringa, che la sequenza di attività aggiunge alla riga di comando USMT generata automaticamente per LoadState.

Le opzioni USMT specificate con questa variabile della sequenza di attività non vengono convalidate per verificarne l'accuratezza prima di eseguire la sequenza di attività.

Per altre informazioni sulle opzioni disponibili, vedere [LoadState Syntax](https://docs.microsoft.com/windows/deployment/usmt/usmt-loadstate-syntax) (Sintassi di LoadState).

### <a name="osdmigratecomputername"></a><a name="OSDMigrateComputerName"></a> OSDMigrateComputerName

*Si applica al passaggio [Acquisisci impostazioni Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings).*

(input)

Specifica se viene eseguita la migrazione del nome del computer.

#### <a name="valid-values"></a>Valori validi

- `true` (impostazione predefinita). La variabile [OSDComputerName (output)](#OSDComputerName-output) viene impostata sul nome NetBIOS del computer.  
- `false`  

### <a name="osdmigrateconfigfiles"></a><a name="OSDMigrateConfigFiles"></a> OSDMigrateConfigFiles

*Si applica al passaggio [Acquisisci stato utente](task-sequence-steps.md#BKMK_CaptureUserState).*

(input)

Specifica i file di configurazione usati per controllare l'acquisizione dei profili utente. Questa variabile viene usata solo se il valore di [OSDMigrateMode](#OSDMigrateMode) è impostato su `Advanced`. Questo valore di elenco delimitato da virgole è impostato per eseguire la migrazione personalizzata dei profili utente.

#### <a name="example"></a>Esempio

`miguser.xml,migsys.xml,migapps.xml`  

### <a name="osdmigratecontinueonlockedfiles"></a><a name="OSDMigrateContinueOnLockedFiles"></a> OSDMigrateContinueOnLockedFiles

*Si applica al passaggio [Acquisisci stato utente](task-sequence-steps.md#BKMK_CaptureUserState).*

(input)

Se USMT non riesce ad acquisire alcuni file, questa variabile consente all'acquisizione dello stato utente di continuare.

#### <a name="valid-values"></a>Valori validi

- `true` (impostazione predefinita)  
- `false`  

### <a name="osdmigratecontinueonrestore"></a><a name="OSDMigrateContinueOnRestore"></a> OSDMigrateContinueOnRestore

*Si applica al passaggio [Ripristina stato utente](task-sequence-steps.md#BKMK_RestoreUserState).*

(input)

Continuare il processo, anche se USMT non può ripristinare alcuni file.

#### <a name="valid-values"></a>Valori validi

- `true` (impostazione predefinita)  
- `false`  

### <a name="osdmigrateenableverboselogging"></a><a name="OSDMigrateEnableVerboseLogging"></a> OSDMigrateEnableVerboseLogging

*Si applica ai passaggi seguenti:*  

- [Acquisisci stato utente](task-sequence-steps.md#BKMK_CaptureUserState)  
- [Ripristina stato utente](task-sequence-steps.md#BKMK_RestoreUserState)  

(input)

Consente la registrazione dettagliata per USMT. Questo valore è obbligatorio per il passaggio.

#### <a name="valid-values"></a>Valori validi

- `true`  
- `false` (impostazione predefinita)  

### <a name="osdmigratelocalaccounts"></a><a name="OSDMigrateLocalAccounts"></a> OSDMigrateLocalAccounts

*Si applica al passaggio [Ripristina stato utente](task-sequence-steps.md#BKMK_RestoreUserState).*

(input)

Specifica se l'account computer locale viene ripristinato.

#### <a name="valid-values"></a>Valori validi

- `true`  
- `false` (impostazione predefinita)  

### <a name="osdmigratelocalaccountpassword"></a><a name="OSDMigrateLocalAccountPassword"></a> OSDMigrateLocalAccountPassword

*Si applica al passaggio [Ripristina stato utente](task-sequence-steps.md#BKMK_RestoreUserState).*

(input)

Se la variabile [OSDMigrateLocalAccounts](#OSDMigrateLocalAccounts) è `true`, questa variabile deve contenere la password assegnata a *tutti* gli account locali di cui viene eseguita la migrazione. USMT assegna la stessa password a tutti gli account locali di cui viene eseguita la migrazione. Considerare questa password come temporanea e cambiarla in seguito con un altro metodo.

### <a name="osdmigratemode"></a><a name="OSDMigrateMode"></a> OSDMigrateMode

*Si applica al passaggio [Acquisisci stato utente](task-sequence-steps.md#BKMK_CaptureUserState).*

(input)

Consente di personalizzare i file acquisiti da USMT.

#### <a name="valid-values"></a>Valori validi

- `Simple`: la sequenza di attività usa solo i file di configurazione USMT standard  

- `Advanced`: la variabile della sequenza di attività [OSDMigrateConfigFiles](#OSDMigrateConfigFiles) specifica i file di configurazione usati da USMT  

### <a name="osdmigratenetworkmembership"></a><a name="OSDMigrateNetworkMembership"></a> OSDMigrateNetworkMembership

*Si applica al passaggio [Acquisisci impostazioni di rete](task-sequence-steps.md#BKMK_CaptureNetworkSettings).*

(input)

Specifica se la sequenza di attività esegue la migrazione delle informazioni di appartenenza al gruppo di lavoro o al dominio.

#### <a name="valid-values"></a>Valori validi

- `true` (impostazione predefinita)
- `false`

### <a name="osdmigrateregistrationinfo"></a><a name="OSDMigrateRegistrationInfo"></a> OSDMigrateRegistrationInfo

*Si applica al passaggio [Acquisisci impostazioni Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings).*

(input)

Specifica se il passaggio esegue la migrazione delle informazioni sull'organizzazione e sugli utenti.

#### <a name="valid-values"></a>Valori validi

- `true` (impostazione predefinita). La variabile [OSDRegisteredOrgName (output)](#OSDRegisteredOrgName-output) viene impostata sul nome dell'organizzazione registrata del computer.  
- `false`  

### <a name="osdmigrateskipencryptedfiles"></a><a name="OSDMigrateSkipEncryptedFiles"></a> OSDMigrateSkipEncryptedFiles

*Si applica al passaggio [Acquisisci stato utente](task-sequence-steps.md#BKMK_CaptureUserState).*

(input)

Specifica se i file crittografati vengono acquisiti.

#### <a name="valid-values"></a>Valori validi

- `true`  
- `false` (impostazione predefinita)  

### <a name="osdmigratetimezone"></a><a name="OSDMigrateTimeZone"></a> OSDMigrateTimeZone

*Si applica al passaggio [Acquisisci impostazioni Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings).*

(input)

Specifica se viene eseguita la migrazione del fuso orario del computer.

#### <a name="valid-values"></a>Valori validi

- `true` (impostazione predefinita). La variabile [OSDTimeZone (output)](#OSDTimeZone-output) viene impostata sul fuso orario del computer.  
- `false`  

### <a name="osdnetworkjointype"></a><a name="OSDNetworkJoinType"></a> OSDNetworkJoinType

*Si applica al passaggio [Applica impostazioni di rete](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

(input)

Specifica se il computer di destinazione viene aggiunto a un dominio o a un gruppo di lavoro di Active Directory.

#### <a name="value-values"></a>Valori validi

- `0`: aggiunta a un dominio di Active Directory  
- `1`: Aggiunta a un gruppo di lavoro

### <a name="osdpartitions"></a><a name="OSDPartitions"></a> OSDPartitions

*Si applica al passaggio [Formato e disco partizione](task-sequence-steps.md#BKMK_FormatandPartitionDisk).*

(input)

Questa variabile della sequenza di attività è una variabile di matrice delle impostazioni della partizione. Ogni elemento della matrice rappresenta le impostazioni per una singola partizione del disco rigido. Accedere alle impostazioni definite per ogni partizione combinando il nome della variabile di matrice con il numero in base zero della partizione del disco e il nome della proprietà.

Usare i nomi di variabile seguenti per definire le proprietà per la *prima* partizione che viene creata da questo passaggio nel disco rigido:

#### <a name="osdpartitions0type"></a>OSDPartitions0Type

Specifica il tipo di partizione. Questa proprietà è obbligatoria. I valori validi sono `Primary`, `Extended`, `Logical` e `Hidden`.

#### <a name="osdpartitions0filesystem"></a>OSDPartitions0FileSystem

Specifica il tipo di file system da usare quando si formatta la partizione. Questa proprietà è facoltativa. Se non si specifica un file system, il passaggio non formatta la partizione. I valori validi sono `FAT32` e `NTFS`.

#### <a name="osdpartitions0bootable"></a>OSDPartitions0Bootable

Specifica se la partizione è di avvio. Questa proprietà è obbligatoria. Se questo valore è impostato su `TRUE` per i dischi MBR, il passaggio contrassegna questa partizione come attiva.

#### <a name="osdpartitions0quickformat"></a>OSDPartitions0QuickFormat

Specifica il tipo di formato usato. Questa proprietà è obbligatoria. Se questo valore è impostato su `TRUE`, il passaggio esegue una formattazione rapida. In caso contrario, il passaggio esegue una formattazione completa.

#### <a name="osdpartitions0volumename"></a>OSDPartitions0VolumeName

Specifica il nome assegnato al volume quando viene formattato. Questa proprietà è facoltativa.

#### <a name="osdpartitions0size"></a>OSDPartitions0Size

Specifica le dimensioni della partizione. Questa proprietà è facoltativa. Se questa proprietà non è specificata, la partizione viene creata usando tutto lo spazio disponibile rimanente. Le unità vengono specificate dalla variabile **OSDPartitions0SizeUnits** .

#### <a name="osdpartitions0sizeunits"></a>OSDPartitions0SizeUnits

Il passaggio usa queste unità per interpretare la variabile **OSDPartitions0Size**. Questa proprietà è facoltativa. I valori validi sono `MB` (impostazione predefinita), `GB` e `Percent`.

#### <a name="osdpartitions0volumelettervariable"></a>OSDPartitions0VolumeLetterVariable

Quando questo passaggio crea le partizioni, usa sempre la lettera di unità disponibile successiva in Windows PE. Usare questa proprietà facoltativa per specificare il nome di un'altra variabile della sequenza di attività. Il passaggio usa questa variabile per salvare la nuova lettera di unità per riferimenti futuri.

Se si definiscono più partizioni con questo passaggio della sequenza di attività, le proprietà per la *seconda* partizione vengono definite usando l'indice **1** nel nome della variabile. Ad esempio: **OSDPartitions1Type**, **OSDPartitions1FileSystem**, **OSDPartitions1Bootable**, **OSDPartitions1QuickFormat** e **OSDPartitions1VolumeName**.

### <a name="osdpartitionstyle"></a><a name="OSDPartitionStyle"></a> OSDPartitionStyle

*Si applica al passaggio [Formato e disco partizione](task-sequence-steps.md#BKMK_FormatandPartitionDisk).*

(input)

Specifica lo stile di partizione da usare per il partizionamento del disco.

#### <a name="valid-values"></a>Valori validi

- `GPT`: usa lo stile di tabella delle partizioni GUID
- `MBR`: usa lo stile di partizione MBR (Master Boot Record, record di avvio principale)

### <a name="osdproductkey"></a><a name="OSDProductKey"></a> OSDProductKey

*Si applica al passaggio [Applica impostazioni Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

(input)

Specifica il codice Product Key di Windows. Il valore specificato deve essere compreso tra 1 e 255 caratteri.

### <a name="osdrandomadminpassword"></a><a name="OSDRandomAdminPassword"></a> OSDRandomAdminPassword

*Si applica al passaggio [Applica impostazioni Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

(input)

Specifica una password generata in modo casuale per l'account amministratore locale nel nuovo sistema operativo.

#### <a name="valid-values"></a>Valori validi

- `true` (impostazione predefinita): Installazione di Windows disabilita l'account Administrator locale nel computer di destinazione  

- `false`: Installazione di Windows abilita l'account Administrator locale nel computer di destinazione e imposta la password dell'account sul valore di [OSDLocalAdminPassword](#OSDLocalAdminPassword)  

### <a name="osdregisteredorgname-input"></a><a name="OSDRegisteredOrgName-input"></a> OSDRegisteredOrgName (input)

*Si applica al passaggio [Applica impostazioni Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

Specifica il nome predefinito dell'organizzazione registrata nel nuovo sistema operativo. Il valore specificato deve essere compreso tra 1 e 255 caratteri.

### <a name="osdregisteredorgname-output"></a><a name="OSDRegisteredOrgName-output"></a> OSDRegisteredOrgName (output)

*Si applica al passaggio [Acquisisci impostazioni Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings).*

Valore impostato sul nome dell'organizzazione registrata del computer. Il valore viene impostato solo se la variabile [OSDMigrateRegistrationInfo](#OSDMigrateRegistrationInfo) è impostata su `true`.

### <a name="osdregisteredusername"></a><a name="OSDRegisteredUserName"></a> OSDRegisteredUserName

*Si applica al passaggio [Applica impostazioni Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

(input)

Specifica il nome predefinito dell'utente registrato nel nuovo sistema operativo. Il valore specificato deve essere compreso tra 1 e 255 caratteri.

### <a name="osdserverlicenseconnectionlimit"></a><a name="OSDServerLicenseConnectionLimit"></a> OSDServerLicenseConnectionLimit

*Si applica al passaggio [Applica impostazioni Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

(input)

Specifica il numero massimo di connessioni consentito. Il numero specificato deve essere compreso tra 5 e 9999 connessioni.

### <a name="osdserverlicensemode"></a><a name="OSDServerLicenseMode"></a> OSDServerLicenseMode

*Si applica al passaggio [Applica impostazioni Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

(input)

Specifica la modalità di licenza di Windows Server usata.

#### <a name="valid-values"></a>Valori validi

- `PerSeat`
- `PerServer`

### <a name="osdsetupadditionalupgradeoptions"></a><a name="OSDSetupAdditionalUpgradeOptions"></a> OSDSetupAdditionalUpgradeOptions

*Si applica al passaggio [Aggiorna sistema operativo](task-sequence-steps.md#BKMK_UpgradeOS).*

(input)

Specifica le opzioni aggiuntive della riga di comando che vengono aggiunte a Installazione di Windows durante un aggiornamento a Windows 10. La sequenza di attività non verifica le opzioni della riga di comando.

Per altre informazioni, vedere [Opzioni della riga di comando di Installazione di Windows](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options).

### <a name="osdstatefallbacktonaa"></a><a name="OSDStateFallbackToNAA"></a> OSDStateFallbackToNAA

*Si applica al passaggio [Richiedi archiviazione stati](task-sequence-steps.md#BKMK_RequestStateStore).*

(input)

Quando l'account computer non riesce a connettersi al punto di migrazione stato, questa variabile specifica se la sequenza di attività esegue il fallback per usare l'account di accesso alla rete.

Per altre informazioni sull'account di accesso alla rete, vedere [Account](../../core/plan-design/hierarchy/accounts.md#network-access-account).

#### <a name="valid-values"></a>Valori validi

- `true`  
- `false` (impostazione predefinita)  

### <a name="osdstatesmpretrycount"></a><a name="OSDStateSMPRetryCount"></a> OSDStateSMPRetryCount

*Si applica al passaggio [Richiedi archiviazione stati](task-sequence-steps.md#BKMK_RequestStateStore).*

(input)

Specifica il numero di tentativi effettuati dal passaggio della sequenza di attività per trovare un punto di migrazione stato prima di restituire un esito negativo. Il numero specificato deve essere compreso tra 0 e 600.

### <a name="osdstatesmpretrytime"></a><a name="OSDStateSMPRetryTime"></a> OSDStateSMPRetryTime

*Si applica al passaggio [Richiedi archiviazione stati](task-sequence-steps.md#BKMK_RequestStateStore).*

(input)

Specifica il numero di secondi di attesa da parte del passaggio della sequenza di attività prima di effettuare nuovi tentativi. Il numero di secondi può essere composto da un massimo di 30 caratteri.

### <a name="osdstatestorepath"></a><a name="OSDStateStorePath"></a> OSDStateStorePath

*Si applica ai passaggi seguenti:*  

- [Acquisisci stato utente](task-sequence-steps.md#BKMK_CaptureUserState)  
- [Rilascia archiviazione stati](task-sequence-steps.md#BKMK_ReleaseStateStore)  
- [Richiedi archiviazione stati](task-sequence-steps.md#BKMK_RequestStateStore)  
- [Ripristina stato utente](task-sequence-steps.md#BKMK_RestoreUserState)  

(input)

Condivisione di rete o nome di percorso locale della cartella in cui la sequenza di attività salva o ripristina lo stato utente. Non è disponibile alcun valore predefinito.

### <a name="osdtargetsystemdrive"></a><a name="OSDTargetSystemDrive"></a> OSDTargetSystemDrive

*Si applica al passaggio [Applica immagine del sistema operativo](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).*

(output)

Specifica la lettera di unità della partizione che contiene i file del sistema operativo dopo l'applicazione dell'immagine.

### <a name="osdtargetsystemroot-input"></a><a name="OSDTargetSystemRoot-input"></a> OSDTargetSystemRoot (input)

*Si applica al passaggio [Acquisisci immagine del sistema operativo](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).*

Specifica il percorso della directory di Windows del sistema operativo installato nel computer di riferimento. La sequenza di attività verifica se si tratta di un sistema operativo supportato per l'acquisizione da Configuration Manager.

### <a name="osdtargetsystemroot-output"></a><a name="OSDTargetSystemRoot-output"></a> OSDTargetSystemRoot (output)

*Si applica al passaggio [Prepara Windows per l'acquisizione](task-sequence-steps.md#BKMK_PrepareWindowsforCapture).*

Specifica il percorso della directory di Windows del sistema operativo installato nel computer di riferimento. La sequenza di attività verifica se si tratta di un sistema operativo supportato per l'acquisizione da Configuration Manager.

### <a name="osdtimezone-input"></a><a name="OSDTimeZone-input"></a> OSDTimeZone (input)

*Si applica al passaggio [Applica impostazioni Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

Specifica l'impostazione predefinita del fuso orario usata nel nuovo sistema operativo.

Impostare il valore di questa variabile sul nome non dipendente dalla lingua del fuso orario. Usare la stringa, ad esempio, nel valore `Std` per un fuso orario nella chiave seguente del Registro di sistema: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Time Zones`.

### <a name="osdtimezone-output"></a><a name="OSDTimeZone-output"></a> OSDTimeZone (output)

*Si applica al passaggio [Acquisisci impostazioni Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings).*

Valore impostato sul fuso orario del computer. Il valore viene impostato solo se la variabile [OSDMigrateTimeZone](#OSDMigrateTimeZone) è impostata su `true`.

### <a name="osdwindowssettingsinputlocale"></a><a name="OSDWindowsSettingsInputLocale"></a> OSDWindowsSettingsInputLocale

*Si applica al passaggio [Applica impostazioni Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

Specifica le impostazioni locali di input predefinite usate nel nuovo sistema operativo.

Per altre informazioni sul valore del file di risposte dell'installazione di Windows, vedere [Microsoft-Windows-International-Core - InputLocale](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-inputlocale).

### <a name="osdwindowssettingssystemlocale"></a><a name="OSDWindowsSettingsSystemLocale"></a> OSDWindowsSettingsSystemLocale

*Si applica al passaggio [Applica impostazioni Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

Specifica le impostazioni locali del sistema predefinite usate nel nuovo sistema operativo.

Per altre informazioni sul valore del file di risposte dell'installazione di Windows, vedere [Microsoft-Windows-International-Core - SystemLocale](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-systemlocale).

### <a name="osdwindowssettingsuilanguage"></a><a name="OSDWindowsSettingsUILanguage"></a> OSDWindowsSettingsUILanguage

*Si applica al passaggio [Applica impostazioni Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

Specifica l'impostazione predefinita della lingua dell'interfaccia utente usata nel nuovo sistema operativo.

Per altre informazioni sul valore del file di risposte dell'installazione di Windows, vedere [Microsoft-Windows-International-Core - UILanguage](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-uilanguage).

### <a name="osdwindowssettingsuilanguagefallback"></a><a name="OSDWindowsSettingsUILanguageFallback"></a> OSDWindowsSettingsUILanguageFallback

*Si applica al passaggio [Applica impostazioni Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

Specifica l'impostazione di fallback della lingua dell'interfaccia utente usata nel nuovo sistema operativo.

Per altre informazioni sul valore del file di risposte dell'installazione di Windows, vedere [Microsoft-Windows-International-Core - UILanguageFallback](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-uilanguagefallback).

### <a name="osdwindowssettingsuserlocale"></a><a name="OSDWindowsSettingsUserLocale"></a> OSDWindowsSettingsUserLocale

*Si applica al passaggio [Applica impostazioni Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

Specifica le impostazioni locali dell'utente predefinite usate nel nuovo sistema operativo.

Per altre informazioni sul valore del file di risposte dell'installazione di Windows, vedere [Microsoft-Windows-International-Core - UserLocale](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-userlocale).

### <a name="osdwipedestinationpartition"></a><a name="OSDWipeDestinationPartition"></a> OSDWipeDestinationPartition

*Si applica al passaggio [Applica immagine dei dati](task-sequence-steps.md#BKMK_ApplyDataImage).*

(input)

Specifica se eliminare i file contenuti nella partizione di destinazione.

#### <a name="valid-values"></a>Valori validi

- `true` (impostazione predefinita)
- `false`

### <a name="osdworkgroupname"></a><a name="OSDWorkgroupName"></a> OSDWorkgroupName

*Si applica al passaggio [Applica impostazioni di rete](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

(input)

Specifica il nome del gruppo di lavoro a cui viene aggiunto il computer di destinazione.

Specificare questa variabile o la variabile [OSDDomainName](#OSDDomainName). Il nome del gruppo di lavoro può essere costituito da un massimo di 32 caratteri.

### <a name="setupcompletepause"></a><a name="SetupCompletePause"></a> SetupCompletePause

*Si applica al passaggio [Aggiorna sistema operativo](task-sequence-steps.md#BKMK_UpgradeOS).*

<!-- 4680263 -->

A partire dalla versione 1910, usare questa variabile per risolvere i problemi di temporizzazione con la sequenza di attività di aggiornamento sul posto di Windows 10 nei dispositivi con prestazioni elevate al completamento dell'installazione di Windows. Quando si assegna un valore in secondi a questa variabile, il processo di installazione di Windows ritarda questo intervallo di tempo prima di avviare la sequenza di attività. Questo timeout fornisce al client di Configuration Manager altro tempo per l'inizializzazione.

Le voci di log seguenti sono esempi comuni di questo problema che è possibile correggere con questa variabile:

- Il componente TSManager registra voci simili agli errori seguenti in **smsts.log**:

    ``` log
    Failed to initate policy evaluation for namespace 'root\ccm\policy\machine', hr=0x80041010
    Error compiling client config policies. code 80041010
    Task Sequence Manager could not initialize Task Sequence Environment. code 80041010
    ```

- Il programma di installazione di Windows registra voci simili agli errori seguenti in **setupcomplete.log**:

    ``` log
    Running C:\windows\CCM\\TSMBootstrap.exe to resume task sequence
    ERRORLEVEL = -1073741701
    TSMBootstrap did not request reboot, resetting registry
    Exiting setupcomplete.cmd
    ```

### <a name="smsclientinstallproperties"></a><a name="SMSClientInstallProperties"></a> SMSClientInstallProperties

*Si applica al passaggio [Imposta Windows e ConfigMgr](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr).*

(input)

Specifica le proprietà di installazione del client usate dalla sequenza di attività per l'installazione del client di Configuration Manager.

Per altre informazioni vedere [Proprietà e parametri di installazione client](../../core/clients/deploy/about-client-installation-properties.md).

### <a name="smsconnectnetworkfolderaccount"></a><a name="SMSConnectNetworkFolderAccount"></a> SMSConnectNetworkFolderAccount

*Si applica al passaggio [Connetti alla cartella di rete](task-sequence-steps.md#BKMK_ConnectToNetworkFolder).*

(input)

Specifica l'account utente usato per connettersi alla condivisione di rete in [SMSConnectNetworkFolderPath](#SMSConnectNetworkFolderPath). Specificare la password dell'account con il valore [SMSConnectNetworkFolderPassword](#SMSConnectNetworkFolderPassword).

Per altre informazioni sull'account di connessione per la cartella di rete della sequenza di attività, vedere [Account](../../core/plan-design/hierarchy/accounts.md#task-sequence-network-folder-connection-account).

### <a name="smsconnectnetworkfolderdriveletter"></a><a name="SMSConnectNetworkFolderDriveLetter"></a> SMSConnectNetworkFolderDriveLetter

*Si applica al passaggio [Connetti alla cartella di rete](task-sequence-steps.md#BKMK_ConnectToNetworkFolder).*

(input)

Specifica la lettera di unità di rete a cui connettersi. Questo valore è facoltativo. Se non viene specificato, la connessione di rete non viene mappata a una lettera di unità. Se questo valore viene specificato, il valore deve essere compreso nell'intervallo tra D e z. Non usare X perché è la lettera di unità usata da Windows PE durante la fase Windows PE.

#### <a name="examples"></a>Esempi

- `D:`  
- `E:`  

### <a name="smsconnectnetworkfolderpassword"></a><a name="SMSConnectNetworkFolderPassword"></a> SMSConnectNetworkFolderPassword

*Si applica al passaggio [Connetti alla cartella di rete](task-sequence-steps.md#BKMK_ConnectToNetworkFolder).*

(input)

Specifica la password per l'account [SMSConnectNetworkFolderAccount](#SMSConnectNetworkFolderAccount) usato per connettersi alla condivisione di rete in [SMSConnectNetworkFolderPath](#SMSConnectNetworkFolderPath).

### <a name="smsconnectnetworkfolderpath"></a><a name="SMSConnectNetworkFolderPath"></a> SMSConnectNetworkFolderPath

*Si applica al passaggio [Connetti alla cartella di rete](task-sequence-steps.md#BKMK_ConnectToNetworkFolder).*

(input)

Specifica il percorso di rete per la connessione. Se è necessario mappare questo percorso a una lettera di unità, usare il valore [SMSConnectNetworkFolderDriveLetter](#SMSConnectNetworkFolderDriveLetter).

#### <a name="example"></a>Esempio

`\\server\share`

### <a name="smsinstallupdatetarget"></a><a name="SMSInstallUpdateTarget"></a> SMSInstallUpdateTarget

*Si applica al passaggio [Installa aggiornamenti software](task-sequence-steps.md#BKMK_InstallSoftwareUpdates).*

(input)

Specifica se installare tutti gli aggiornamenti o solo quelli obbligatori.

#### <a name="valid-values"></a>Valori validi

- `All`  
- `Mandatory`  

### <a name="smsrebootmessage"></a><a name="SMSRebootMessage"></a> SMSRebootMessage

*Si applica al passaggio [Riavvia computer](task-sequence-steps.md#BKMK_RestartComputer).*

(input)

Specifica il messaggio da visualizzare agli utenti prima di riavviare il computer di destinazione. Se questa variabile non è impostata, viene visualizzato il testo del messaggio predefinito. Il messaggio specificato non può superare i 512 caratteri.

#### <a name="example"></a>Esempio

`Save your work before the computer restarts.`  

### <a name="smsreboottimeout"></a><a name="SMSRebootTimeout"></a> SMSRebootTimeout

*Si applica al passaggio [Riavvia computer](task-sequence-steps.md#BKMK_RestartComputer).*

(input)

Specifica il numero di secondi durante i quali l'avviso viene visualizzato all'utente prima del riavvio del computer.

#### <a name="examples"></a>Esempi

- `0` (impostazione predefinita): non visualizza un messaggio di riavvio  
- `60`: visualizza l'avviso per un minuto  

### <a name="smstsassignmentsdownloadinterval"></a><a name="SMSTSAssignmentsDownloadInterval"></a> SMSTSAssignmentsDownloadInterval

Numero di secondi di attesa prima che il client provi a eseguire il tentativo di download dei criteri dopo l'ultimo tentativo che non ha restituito alcun criterio. Per impostazione predefinita, il client attende **0** secondi prima di riprovare.

È possibile impostare questa variabile usando un comando di preavvio da un supporto o da PXE.

### <a name="smstsassignmentsdownloadretry"></a><a name="SMSTSAssignmentsDownloadRetry"></a> SMSTSAssignmentsDownloadRetry

Numero di tentativi di download dei criteri da parte del client dopo che non è stato rilevato alcun criterio durante il primo tentativo. Per impostazione predefinita, il client riprova **0** volte.

È possibile impostare questa variabile usando un comando di preavvio da un supporto o da PXE.

### <a name="smstsassignusersmode"></a><a name="SMSTSAssignUsersMode"></a> SMSTSAssignUsersMode

Specifica in che modo una sequenza di attività associa gli utenti al computer di destinazione. Impostare la variabile su uno dei seguenti valori:  

- **Auto**: la sequenza di attività crea una relazione tra gli utenti specificati e il computer di destinazione quando distribuisce il sistema operativo nel computer di destinazione.  

- **Pending**: la sequenza di attività crea una relazione tra gli utenti specificati e il computer di destinazione. Un amministratore deve approvare la relazione per impostarla.  

- **Disabilitato**: la sequenza di attività non associa gli utenti al computer di destinazione quando distribuisce il sistema operativo.

### <a name="smstsdisablestatusretry"></a><a name="SMSTSDisableStatusRetry"></a> SMSTSDisableStatusRetry

<!--512358-->
Negli scenari disconnessi il motore di esecuzione della sequenza di attività prova ripetutamente a inviare messaggi di stato al punto di gestione. Questo comportamento in questo scenario causa ritardi nell'elaborazione della sequenza di attività.

Impostare questa variabile su `true` per evitare che il motore di esecuzione della sequenza di attività provi a mandare di nuovo i messaggi di stato dopo il primo errore. Il primo tentativo include diversi tentativi.

Quando la sequenza di attività viene riavviata, il valore della variabile viene mantenuto. Tuttavia, la sequenza di attività tenta di inviare un messaggio di stato iniziale. Il primo tentativo include diversi tentativi. Se l'operazione riesce, la sequenza di attività continua a inviare lo stato indipendentemente dal valore della variabile. Se l'invio dello stato non riesce, la sequenza di attività usa il valore della variabile.

> [!NOTE]  
> La [creazione di report sullo stato della sequenza di attività](../../core/servers/manage/list-of-reports.md#task-sequence---deployment-status) si basa su questi messaggi di stato per la visualizzazione dell'avanzamento, della cronologia e dei dettagli di ogni passaggio. Se l'invio di messaggi di stato non riesce, i messaggi non vengono accodati. Non vengono inviati in seguito, quando la connettività al punto di gestione viene ripristinata. Questo comportamento ha come risultato la creazione di report di stato della sequenza di attività incompleti e con elementi mancanti.

### <a name="smstsdisablewow64redirection"></a><a name="SMSTSDisableWow64Redirection"></a> SMSTSDisableWow64Redirection

*Si applica al passaggio [Esegui riga di comando](task-sequence-steps.md#BKMK_RunCommandLine).*

(input)

Per impostazione predefinita, in un sistema operativo a 64 bit la sequenza di attività individua ed esegue il programma nella riga di comando usando il redirector del file system WOW64. Questo comportamento consente al comando di trovare le versioni a 32 bit dei programmi e delle DLL del sistema operativo. L'impostazione di questa variabile su `true` disabilita l'uso del redirector del file system WOW64. Il comando trova le versioni a 64 bit native dei programmi e delle DLL del sistema operativo. Questa variabile non ha effetto quando l'esecuzione avviene in un sistema operativo a 32 bit.

### <a name="smstsdownloadabortcode"></a><a name="SMSTSDownloadAbortCode"></a> SMSTSDownloadAbortCode

Questa variabile contiene il valore del codice di interruzione per il downloader del programma esterno. Questo programma viene specificato dalla variabile [SMSTSDownloadProgram](#SMSTSDownloadProgram). Se il programma restituisce un codice di errore uguale al valore della variabile SMSTSDownloadAbortCode, il download del contenuto ha esito negativo e non viene tentato alcun altro metodo di download.

### <a name="smstsdownloadprogram"></a><a name="SMSTSDownloadProgram"></a> SMSTSDownloadProgram

Usare questa variabile per specificare un provider di contenuto alternativo (ACP). Un ACP è un programma downloader usato per scaricare contenuto. La sequenza di attività usa l'ACP invece del downloader predefinito di Configuration Manager. Come parte del processo di download del contenuto, la sequenza di attività controlla questa variabile. Se specificata, la sequenza di attività esegue il programma per scaricare il contenuto.

### <a name="smstsdownloadretrycount"></a><a name="SMSTSDownloadRetryCount"></a> SMSTSDownloadRetryCount

Numero di tentativi eseguiti da Configuration Manager per scaricare contenuto da un punto di distribuzione. Per impostazione predefinita, il client riprova **2** volte.

### <a name="smstsdownloadretrydelay"></a><a name="SMSTSDownloadRetryDelay"></a> SMSTSDownloadRetryDelay

Numero di secondi di attesa prima che Configuration Manager provi a scaricare il contenuto da un punto di distribuzione. Per impostazione predefinita, il client attende **15** secondi prima di riprovare.

### <a name="smstsdriverrequestconnecttimeout"></a><a name="SMSTSDriverRequestConnectTimeOut"></a> SMSTSDriverRequestConnectTimeOut

*Si applica al passaggio [Applica automaticamente i driver](task-sequence-steps.md#BKMK_AutoApplyDrivers).*

Quando si richiede il catalogo driver, questa variabile indica per quanti secondi la sequenza di attività attende la connessione al server HTTP. Se la connessione richiede più tempo rispetto all'impostazione del timeout, la sequenza di attività annulla la richiesta. L'impostazione predefinita del timeout è di **60** secondi.

### <a name="smstsdriverrequestreceivetimeout"></a><a name="SMSTSDriverRequestReceiveTimeOut"></a> SMSTSDriverRequestReceiveTimeOut

*Si applica al passaggio [Applica automaticamente i driver](task-sequence-steps.md#BKMK_AutoApplyDrivers).*

Quando si richiede il catalogo driver, questa variabile indica per quanti secondi la sequenza di attività attende una risposta. Se la connessione richiede più tempo rispetto all'impostazione del timeout, la sequenza di attività annulla la richiesta. L'impostazione predefinita del timeout è di **480** secondi.

### <a name="smstsdriverrequestresolvetimeout"></a><a name="SMSTSDriverRequestResolveTimeOut"></a> SMSTSDriverRequestResolveTimeOut

*Si applica al passaggio [Applica automaticamente i driver](task-sequence-steps.md#BKMK_AutoApplyDrivers).*

Quando si richiede il catalogo driver, questa variabile indica per quanti secondi la sequenza di attività attende la risoluzione dei nomi HTTP. Se la connessione richiede più tempo rispetto all'impostazione del timeout, la sequenza di attività annulla la richiesta. L'impostazione predefinita del timeout è di **60** secondi.

### <a name="smstsdriverrequestsendtimeout"></a><a name="SMSTSDriverRequestSendTimeOut"></a> SMSTSDriverRequestSendTimeOut

*Si applica al passaggio [Applica automaticamente i driver](task-sequence-steps.md#BKMK_AutoApplyDrivers).*

Quando si invia una richiesta per il catalogo driver, questa variabile indica per quanti secondi la sequenza di attività attende prima di inviare la richiesta. Se la richiesta richiede più tempo rispetto all'impostazione del timeout, la sequenza di attività annulla la richiesta. L'impostazione predefinita del timeout è di **60** secondi.

### <a name="smstserrordialogtimeout"></a><a name="SMSTSErrorDialogTimeout"></a> SMSTSErrorDialogTimeout

Quando si verifica un errore nella sequenza di attività, viene visualizzata una finestra di dialogo con l'errore. La sequenza di attività la ignora automaticamente dopo il numero di secondi specificato da questa variabile. Per impostazione predefinita, questo valore è pari a **900** secondi (15 minuti).

### <a name="smstslanguagefolder"></a><a name="SMSTSLanguageFolder"></a> SMSTSLanguageFolder

usare questa variabile per modificare la lingua di visualizzazione di un'immagine di avvio indipendente dalla lingua.

### <a name="smstslocaldatadrive"></a><a name="SMSTSLocalDataDrive"></a> SMSTSLocalDataDrive

Specifica la posizione del computer di destinazione in cui la sequenza di attività archivia i file della cache temporanei durante l'esecuzione.

Impostare questa variabile prima dell'inizio della sequenza di attività, ad esempio impostando una variabile raccolta. Dopo l'avvio della sequenza di attività, Configuration Manager definisce la variabile [_SMSTSMDataPath](#SMSTSMDataPath) in base alla definizione della variabile SMSTSLocalDataDrive.

### <a name="smstsmp"></a><a name="SMSTSMP"></a> SMSTSMP

Usare questa variabile per specificare l'URL o l'indirizzo IP del punto di gestione di Configuration Manager.

### <a name="smstsmplistrequesttimeoutenabled"></a><a name="SMSTSMPListRequestTimeoutEnabled"></a> SMSTSMPListRequestTimeoutEnabled

*Si applica ai passaggi seguenti:*  

- [Installa applicazione](task-sequence-steps.md#BKMK_InstallApplication)  
- [Installa aggiornamenti software](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

(input)

Se il client non si trova nella Intranet, usare questa variabile per abilitare le richieste MPList ripetute per aggiornare il client. Per impostazione predefinita, questa variabile è impostata su `True`.

Quando i client sono su Internet, impostare questa variabile su `False` per evitare inutili ritardi.

### <a name="smstsmplistrequesttimeout"></a><a name="SMSTSMPListRequestTimeout"></a> SMSTSMPListRequestTimeout

*Si applica ai passaggi seguenti:*  

- [Installa applicazione](task-sequence-steps.md#BKMK_InstallApplication)  
- [Installa aggiornamenti software](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

(input)

Se la sequenza di attività non riesce a recuperare l'elenco dei punti di gestione (MPList) dai servizi di posizione, questa variabile specifica quanti millisecondi attendere prima di riprovare a eseguire il passaggio. Per impostazione predefinita, la sequenza di attività attende `60000` millisecondi (60 secondi) prima di riprovare a eseguire il passaggio. Vengono eseguiti al massimo tre tentativi.

### <a name="smstspeerdownload"></a><a name="SMSTSPeerDownload"></a> SMSTSPeerDownload

Usare questa variabile per consentire al client l'impiego della peer cache di Windows PE. L'impostazione di questa variabile su `true` abilita questa funzionalità.

### <a name="smstspeerrequestport"></a><a name="SMSTSPeerRequestPort"></a> SMSTSPeerRequestPort

Porta di rete personalizzata usata dalla cache peer di Windows PE per la trasmissione iniziale. La porta predefinita configurata nelle impostazioni client è la **8004**.

### <a name="smstspersistcontent"></a><a name="SMSTSPersistContent"></a> SMSTSPersistContent

usare questa variabile per mantenere temporaneamente il contenuto nella cache della sequenza di attività. Questa variabile è diversa da [SMSTSPreserveContent](#SMSTSPreserveContent), che mantiene il contenuto nella cache del client di Configuration Manager dopo il completamento della sequenza di attività. SMSTSPersistContent usa la cache della sequenza di attività, SMSTSPreserveContent usa la cache del client Configuration Manager.

### <a name="smstspostaction"></a><a name="SMSTSPostAction"></a> SMSTSPostAction

Specifica un comando che viene eseguito al termine della sequenza di attività. Ad esempio, specificare `shutdown.exe /r /t 30 /f` per riavviare il computer 30 secondi dopo il completamento della sequenza di attività.

### <a name="smstspreferredadvertid"></a><a name="SMSTSPreferredAdvertID"></a> SMSTSPreferredAdvertID

Forza la sequenza di attività a eseguire una distribuzione di destinazione specifica sul computer di destinazione. Impostare questa variabile tramite un comando di preavvio dai supporti o da PXE. Se questa variabile viene impostata, la sequenza di attività esegue l'override di tutte le distribuzioni richieste.

### <a name="smstspreservecontent"></a><a name="SMSTSPreserveContent"></a> SMSTSPreserveContent

Questa variabile contrassegna il contenuto nella sequenza di attività da mantenere nella cache del client di Configuration Manager dopo la distribuzione. Questa variabile è diversa da [SMSTSPersistContent](#SMSTSPersistContent), che mantiene il contenuto solo per la durata della sequenza di attività. SMSTSPersistContent usa la cache della sequenza di attività, SMSTSPreserveContent usa la cache del client Configuration Manager. Impostare SMSTSPreserveContent su `true` per abilitare questa funzionalità.

### <a name="smstsrebootdelay"></a><a name="SMSTSRebootDelay"></a> SMSTSRebootDelay

Specifica il tempo di attesa in secondi prima del riavvio del computer. Se questa variabile è zero (0), il motore di esecuzione della sequenza di attività non visualizza una finestra di dialogo di notifica prima del riavvio.

#### <a name="example"></a>Esempio

- `0`: non visualizza una notifica  

- `60`: visualizza una notifica per un minuto  

### <a name="smstsrebootdelaynext"></a><a name="SMSTSRebootDelayNext"></a> SMSTSRebootDelayNext

<!--4447680-->
A partire dalla versione 1906, usare questa variabile insieme alla variabile [SMSTSRebootDelay](task-sequence-variables.md#SMSTSRebootDelay) esistente. Se si vuole che i riavvii successivi si verifichino con un timeout diverso rispetto al primo, impostare SMSTSRebootDelayNext su un valore diverso in secondi.

#### <a name="example"></a>Esempio

Si vuole inviare all'utente una notifica di riavvio di 60 secondi all'inizio di una sequenza di attività di aggiornamento sul posto di Windows 10. In questo caso, dopo il primo riavvio lungo, i timeout aggiuntivi si dovranno impostare su 60 secondi. Impostare SMSTSRebootDelay su `3600` e SMSTSRebootDelayNext su `60`.  


### <a name="smstsrebootmessage"></a><a name="SMSTSRebootMessage"></a> SMSTSRebootMessage

Specifica il messaggio da visualizzare nella finestra di dialogo di notifica di riavvio. Se questa variabile non è impostata, viene visualizzato un messaggio predefinito.

#### <a name="example"></a>Esempio

`The task sequence is restarting this computer`

### <a name="smstsrebootrequested"></a><a name="SMSTSRebootRequested"></a> SMSTSRebootRequested

Indica che un riavvio è richiesto al termine del passaggio della sequenza di attività corrente. Se il passaggio della sequenza di attività richiede un riavvio per completare l'azione, impostare questa variabile. Dopo il riavvio del computer, la sequenza di attività continua a essere eseguita dal passaggio successivo della sequenza di attività.

- `HD`: Riavviare con il sistema operativo installato
- `WinPE`: Riavviare con l'immagine di avvio associata

### <a name="smstsretryrequested"></a><a name="SMSTSRetryRequested"></a> SMSTSRetryRequested

Richiede un nuovo tentativo dopo il completamento del passaggio della sequenza di attività. Se questa variabile della sequenza di attività è impostata, impostare la variabile [SMSTSRebootRequested](#SMSTSRebootRequested) su `true`. Dopo il riavvio del computer, il motore di esecuzione della sequenza di attività ripete lo stesso passaggio della sequenza di attività.

### <a name="smstsruncommandlineasuser"></a><a name="SMSTSRunCommandLineAsUser"></a> SMSTSRunCommandLineAsUser

*A partire dalla versione 2002* <!-- 5573175 -->  
*Si applica al passaggio [Esegui riga di comando](task-sequence-steps.md#BKMK_RunCommandLine).*

Usare le variabili della sequenza di attività per configurare il contesto utente per il passaggio **Esegui riga di comando**. Non è necessario configurare il passaggio **Esegui riga di comando** con un account segnaposto per usare le variabili [SMSTSRunCommandLineUserName](task-sequence-variables.md#SMSTSRunCommandLineUserName) e [SMSTSRunCommandLineUserPassword](task-sequence-variables.md#SMSTSRunCommandLineUserPassword).

Configurare `SMSTSRunCommandLineAsUser` con uno dei valori seguenti:

- `true`: ogni ulteriore passaggio **Esegui riga di comando** viene eseguito nel contesto dell'utente specificato in `SMSTSRunCommandLineUserName`.

- `false`: ogni ulteriore passaggio **Esegui riga di comando** viene eseguito nel contesto configurato per il passaggio.

### <a name="smstsruncommandlineusername"></a><a name="SMSTSRunCommandLineUserName"></a> SMSTSRunCommandLineUserName

*Si applica al passaggio [Esegui riga di comando](task-sequence-steps.md#BKMK_RunCommandLine).*

(input)

Specifica l'account da cui viene eseguita la riga di comando. Il valore è una stringa nel formato nomeutente o dominio\nome utente. Specificare la password dell'account con la variabile [SMSTSRunCommandLineUserPassword](#SMSTSRunCommandLineUserPassword).

> [!NOTE]
> A partire dalla versione 2002, usare la variabile [SMSTSRunCommandLineAsUser](task-sequence-variables.md#SMSTSRunCommandLineAsUser) con questa variabile per configurare il contesto utente per questo passaggio.
>
> Nella versione 1910 e precedenti, configurare il passaggio **Esegui riga di comando** con l'impostazione **Esegui questo passaggio come account specificato**. Quando si abilita questa opzione, se si impostano il nome utente e la password tramite variabili, specificare un valore per l'account.

Per altre informazioni sull'account Esegui come per la sequenza di attività, vedere [Account](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account).

### <a name="smstsruncommandlineuserpassword"></a><a name="SMSTSRunCommandLineUserPassword"></a> SMSTSRunCommandLineUserPassword

*Si applica al passaggio [Esegui riga di comando](task-sequence-steps.md#BKMK_RunCommandLine).*

(input)

Specifica la password per l'account specificato dalla variabile [SMSTSRunCommandLineUserName](#SMSTSRunCommandLineUserName).

### <a name="smstsrunpowershellasuser"></a><a name="SMSTSRunPowerShellAsUser"></a> SMSTSRunPowerShellAsUser

*A partire dalla versione 2002* <!-- 5573175 -->  
*Si applica al passaggio [Esegui script PowerShell](task-sequence-steps.md#BKMK_RunPowerShellScript).*

Usare le variabili della sequenza di attività per configurare il contesto utente per i passaggi **Esegui script PowerShell**. Non è necessario configurare il passaggio **Esegui script PowerShell** con un account segnaposto per usare le variabili [SMSTSRunPowerShellUserName](task-sequence-variables.md#SMSTSRunPowerShellUserName) e [SMSTSRunPowerShellUserPassword](task-sequence-variables.md#SMSTSRunPowerShellUserPassword).

Configurare `SMSTSRunPowerShellAsUser` con uno dei valori seguenti:

- `true`: ogni ulteriore passaggio **Esegui script PowerShell** viene eseguito nel contesto dell'utente specificato in `SMSTSRunPowerShellUserName`.

- `false`: ogni ulteriore passaggio **Esegui script PowerShell** viene eseguito nel contesto configurato per il passaggio.

### <a name="smstsrunpowershellusername"></a><a name="SMSTSRunPowerShellUserName"></a> SMSTSRunPowerShellUserName

*Si applica al passaggio [Esegui script PowerShell](task-sequence-steps.md#BKMK_RunPowerShellScript).*

(input)

Specifica l'account dal quale viene eseguito lo script di PowerShell. Il valore è una stringa nel formato nomeutente o dominio\nome utente. Specificare la password dell'account con la variabile [SMSTSRunPowerShellUserPassword](#SMSTSRunPowerShellUserPassword).

> [!NOTE]
> Per usare queste variabili, configurare il passaggio **Esegui script PowerShell** con l'impostazione **Esegui questo passaggio come account specificato**. Quando si abilita questa opzione, se si impostano il nome utente e la password tramite variabili, specificare un valore per l'account.

Per altre informazioni sull'account Esegui come per la sequenza di attività, vedere [Account](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account).

### <a name="smstsrunpowershelluserpassword"></a><a name="SMSTSRunPowerShellUserPassword"></a> SMSTSRunPowerShellUserPassword

*Si applica al passaggio [Esegui script PowerShell](task-sequence-steps.md#BKMK_RunPowerShellScript).*

(input)

Specifica la password per l'account specificato dalla variabile [SMSTSRunPowerShellUserName](#SMSTSRunPowerShellUserName).

### <a name="smstssoftwareupdatescantimeout"></a><a name="SMSTSSoftwareUpdateScanTimeout"></a> SMSTSSoftwareUpdateScanTimeout

*Si applica al passaggio [Installa aggiornamenti software](task-sequence-steps.md#BKMK_InstallSoftwareUpdates).*

(input)

Controllare il timeout per l'analisi degli aggiornamenti software durante questo passaggio. Ad esempio, aumentare il valore se si prevedono numerosi aggiornamenti durante l'analisi. Il valore predefinito è `3600` secondi (60 minuti). Il valore della variabile è impostato in secondi.

### <a name="smstsudausers"></a><a name="SMSTSUDAUsers"></a> SMSTSUDAUsers

Specifica gli utenti primari del computer di destinazione usando il formato seguente: `<DomainName>\<UserName>`. Separare più utenti mediante una virgola (`,`). Per altre informazioni, vedere [Associate users with a destination computer](../get-started/associate-users-with-a-destination-computer.md) (Associare gli utenti a un computer di destinazione).

#### <a name="example"></a>Esempio

`contoso\jqpublic, contoso\megb, contoso\janedoh`

### <a name="smstswaitforsecondreboot"></a><a name="SMSTSWaitForSecondReboot"></a> SMSTSWaitForSecondReboot

*Si applica al passaggio [Installa aggiornamenti software](task-sequence-steps.md#BKMK_InstallSoftwareUpdates).*

(input)

Questa variabile della sequenza di attività facoltativa controlla il comportamento del client quando l'installazione dell'aggiornamento software richiede due riavvii. Impostare questa variabile prima di questo passaggio per impedire che una sequenza di attività non riesca a causa di un secondo riavvio dall'installazione dell'aggiornamento software.

Impostare il valore SMSTSWaitForSecondReboot in secondi per specificare il tempo di sospensione della sequenza di attività in questo passaggio durante il riavvio del computer. Consentire il tempo necessario in caso di un secondo riavvio.

Ad esempio, se si imposta SMSTSWaitForSecondReboot su `600`, la sequenza di attività viene sospesa per 10 minuti dopo un riavvio prima di eseguire i passaggi aggiuntivi. Questa variabile è utile quando un singolo passaggio della sequenza di attività Installa aggiornamenti software installa centinaia di aggiornamenti software.

> [!Note]
> Questa variabile si applica solo a una sequenza di attività che distribuisce un sistema operativo. Non funziona in una sequenza di attività personalizzata. <!-- 2839998 -->

### <a name="tsdebugmode"></a><a name="TSDebugMode"></a> TSDebugMode

<!--3612274-->
A partire dalla versione 1906, impostare questa variabile su `TRUE` per una raccolta o un oggetto computer a cui viene distribuita la sequenza di attività. In tutti i dispositivi con questa variabile impostata, qualsiasi sequenza di attività passa in modalità di debug.

Per altre informazioni, vedere [Eseguire il debug di una sequenza di attività](../deploy-use/debug-task-sequence.md).

### <a name="tsdebugonerror"></a><a name="TSDebugOnError"></a> TSDebugOnError

<!-- 5012536 -->
A partire dalla versione 1910, impostare questa variabile su `TRUE` per avviare automaticamente il [debugger delle sequenze di attività](../deploy-use/debug-task-sequence.md) quando la sequenza di attività restituisce un errore.

Impostare questa variabile usando:

- Il passaggio [Imposta variabile della sequenza di attività](task-sequence-steps.md#BKMK_SetTaskSequenceVariable)

- Una variabile raccolta. Per altre informazioni, vedere [Come impostare le variabili](using-task-sequence-variables.md#bkmk_set).

### <a name="tsdisableprogressui"></a><a name="TSDisableProgressUI"></a> TSDisableProgressUI

<!-- 1354291 -->
Usare questa variabile per controllare la visualizzazione, da parte degli utenti finali, dello stato della sequenza di attività. Per nascondere o visualizzare lo stato in momenti diversi, impostare questa variabile più volte in una sequenza di attività.  

- `true`: Nascondere l'avanzamento della sequenza di attività  

- `false`: visualizzare lo stato della sequenza di attività  

### <a name="tserroronwarning"></a><a name="TSErrorOnWarning"></a> TSErrorOnWarning

*Si applica al passaggio [Installa applicazione](task-sequence-steps.md#BKMK_InstallApplication).*

(input)

Specificare se il motore di esecuzione della sequenza di attività considera un avviso rilevato come errore durante questo passaggio. La sequenza di attività imposta la variabile [_TSAppInstallStatus](#TSAppInstallStatus) su `Warning` quando una o più applicazioni o una dipendenza richiesta non vengono installate perché non soddisfano un requisito. Quando si imposta questa variabile su `True` e la sequenza di attività imposta **_TSAppInstallStatus** su `Warning`, il risultato è un errore. Il comportamento predefinito è `False`.

### <a name="tsprogressinfolevel"></a><a name="TSProgressInfoLevel"></a> TSProgressInfoLevel

*A partire dalla versione 2002*<!--5932692-->  

Specificare questa variabile per controllare il tipo di informazioni visualizzate nella finestra di stato della sequenza di attività. Usare i valori seguenti per questa variabile:

- `1`: includere il passaggio corrente e i passaggi totali per il testo di stato. Ad esempio, **2 di 10**.
- `2`: includere il passaggio corrente, i passaggi totali e la percentuale di completamento. Ad esempio, **2 di 10 (20% completato)** .
- `3`: includere la percentuale di completamento. Ad esempio, **(20% completato)** .

### <a name="tsuefidrive"></a><a name="TSUEFIDrive"></a> TSUEFIDrive

Usare le proprietà di una partizione FAT32 nel campo **Variabile**. Quando la sequenza di attività rileva questa variabile, avvia la preparazione del disco per la transizione a UEFI prima di riavviare il computer. Per altre informazioni, vedere [Passaggi della sequenza di attività per la gestione della conversione da BIOS a UEFI](../deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md).

### <a name="workingdirectory"></a><a name="WorkingDirectory"></a> WorkingDirectory

*Si applica al passaggio [Esegui riga di comando](task-sequence-steps.md#BKMK_RunCommandLine).*

(input)

Specifica la directory di avvio per un'azione della riga di comando. Il nome di directory specificato non può superare i 255 caratteri.

#### <a name="examples"></a>Esempi

- `C:\`  
- `%SystemRoot%`  


## <a name="deprecated-variables"></a>Variabili deprecate

Le variabili seguenti sono deprecate:

- **OSDAllowUnsignedDriver**: non viene usata in caso di distribuzione di Windows Vista e di sistemi operativi successivi
- **OSDBuildStorageDriverList**: si applica solo a Windows XP e Windows Server 2003
- **OSDDiskpartBiosCompatibilityMode**: necessaria solo durante la distribuzione di Windows XP o Windows Server 2003
- **OSDInstallEditionIndex**: non necessaria dopo Windows Vista
- **OSDPreserveDriveLetter**: Per altre informazioni, vedere [OSDPreserveDriveLetter](#osdpreservedriveletter)

### <a name="osdpreservedriveletter"></a>OSDPreserveDriveLetter

> [!Important]
> Questa variabile della sequenza di attività è deprecata.
>
> Durante la distribuzione del sistema operativo, per impostazione predefinita Installazione di Windows stabilisce qual è la lettera di unità migliore da usare (in genere C:).

*Comportamento precedente*: quando si applica un'immagine, la variabile OSDPreverveDriveLetter determina se la sequenza di attività usa la lettera di unità acquisita nel file di immagine (WIM). Impostare il valore per questa variabile su `false` per usare il percorso specificato per l'impostazione **Destinazione** nel passaggio della sequenza di attività **Applica sistema operativo**. Per altre informazioni, vedere [Applica immagine del sistema operativo](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).


## <a name="see-also"></a>Vedere anche

- [Passaggi della sequenza di attività](task-sequence-steps.md)
- [Come usare le variabili della sequenza di attività](using-task-sequence-variables.md)
- [Considerazioni sulla pianificazione dell'automazione delle attività](../plan-design/planning-considerations-for-automating-tasks.md)