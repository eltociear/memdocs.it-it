---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 07/13/2020
ms.openlocfilehash: 80302a1c369c36a08cc1a55e20cf339dbc8d2883
ms.sourcegitcommit: 6d987bb69d0eb9955a3003202864f58d6aaa426a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/14/2020
ms.locfileid: "86381047"
---
<!--This file is shared by the CMPivot overview articles for both Microsoft Endpoint Manager tenant attach and Configuration Manager-->

## <a name="queries"></a>Query

Le query possono essere usate per cercare termini, identificare tendenze, analizzare schemi e offrire molte altre informazioni dettagliate in base ai dati dell'utente. CMPivot usa un sottoinsieme del modello [Analisi dei log di Azure](https://docs.microsoft.com/azure/kusto/query) di flusso di dati per l'istruzione dell'espressione tabulare. La struttura tipica di un'istruzione dell'espressione tabulare è una combinazione di entità client e di operatori di dati tabulari, ad esempio filtri e proiezioni. La combinazione è rappresentata dal carattere barra verticale (|), quindi l'istruzione ha una forma molto regolare che rappresenta visivamente il flusso di dati tabulari da sinistra a destra. Ogni operatore accetta un set di dati tabulari configurati "dalla pipe" e input aggiuntivi, inclusi altri set di dati tabulari, dal corpo dell'operatore, quindi emette un set di dati tabulari per l'operatore successivo seguente: `entity | operator1 | operator2 | ...`

Nell'esempio seguente l'entità è `CCMRecentlyUsedApplications`, vale a dire un riferimento alle applicazioni usate di recente, e l'operatore è where, che esclude i record dal rispettivo input in base a un predicato per record:

```
CCMRecentlyUsedApplications | where CompanyName like '%Microsoft%' | project CompanyName, ExplorerFileName, LastUsedTime, LaunchCount, FolderPath
```

## <a name="entities"></a>Entità

Le entità sono oggetti su cui è possibile eseguire query dal client. Attualmente sono supportate le entità seguenti:


|Entità|Descrizione|
|---|---|
|AadStatus|Stato di Azure Active Directory|
|Administrators|Membri del gruppo di amministratori locale|
|AppCrash|Report degli arresti anomali recenti dell'applicazione|
|AppVClientApplication|Applicazione client AppV|
|AppVClientPackage|Pacchetto client AppV|
|AutoStartSoftware|Software avviato automaticamente con o immediatamente dopo il sistema operativo|
|Scheda di base|Scheda di base|
|Batteria|Batteria|
|Bios|Informazioni BIOS del sistema|
|BitLocker|BitLocker|
|BitLockerEncryptionDetails|Dettagli della crittografia di BitLocker|
|BitLockerPolicy|Criteri di BitLocker|
|BootConfiguration|Configurazione di avvio|
|BrowserHelperObject|Oggetto browser helper|
|BrowserUsage|Utilizzo del browser|
|CcmLog()|Righe entro 24 ore (per impostazione predefinita) da un file di log Ccm|
|CCMRAX|CCM_RAX|
|CCMRecentlyUsedApplications|Applicazioni usate di recente|
|CCMWebAppInstallInfo|Applicazioni Web|
|CDROM|Unità CD-ROM|
|ClientEvents|Eventi client|
|ComputerSystem|Sistema computer|
|ComputerSystemEx|Sistema computer esteso|
|ComputerSystemProduct|Prodotto di sistema|
|ConnectedDevice|Dispositivo connesso|
|Connessioni|Connessione TCP attiva verso o dal dispositivo|
|Desktop|Desktop|
|DesktopMonitor|Monitor da tavolo|
|Dispositivo|Informazioni di base sul dispositivo|
|Disco|Informazioni sul dispositivo di archiviazione locale in un sistema informatico che esegue Windows|
|DMA|DMA|
|DMAChannel|Canale DMA|
|DriverVxD|Driver - VxD|
|EmbeddedDeviceInformation|Informazioni sul dispositivo incorporato|
|Ambiente|Ambiente|
|EPStatus|Stato del software antimalware nel computer|
|EventLog()|Eventi entro 24 ore (per impostazione predefinita) da un log eventi|
|File()|Informazioni su un file specifico|
|FileShare|Informazioni sulle condivisioni file attive|
|Firmware|Firmware|
|IDEController|Controller IDE|
|InstalledExecutable|Eseguibile installato|
|InstalledSoftware|Applicazione installata nel dispositivo|
|IPConfig|Consente di ottenere la configurazione di rete, incluse le interfacce utilizzabili, gli indirizzi IP e i server DNS|
|IRQTable|Tabella IRQ|
|Tastiera|Tastiera|
|LoadOrderGroup|Gruppo ordine di caricamento|
|LogicalDisk|Disco logico|
|MDMDevDetail|Informazioni sul dispositivo|
|Memoria|Memoria|
|Modem|Modem|
|Scheda madre|Scheda madre|
|NetworkAdapter|Scheda di rete|
|NetworkAdapterConfiguration|Configurazione della scheda di rete|
|NetworkClient|Client di rete|
|NetworkLoginProfile|Profilo di accesso della rete|
|NTEventlogFile|File del registro eventi di NT|
|Office365ProPlusConfigurations|Configurazioni di Office 365 ProPlus|
|OfficeAddin|Componenti aggiuntivi per Office|
|OfficeClientMetric|Metrica client di Office|
|OfficeDeviceSummary|Riepilogo dispositivi di Office|
|OfficeDocumentMetric|Metriche dei documenti di Office|
|OfficeDocumentSolution|Soluzione documenti di Office|
|OfficeMacroError|Errore macro di Office|
|OfficeProductInfo|Informazioni sul prodotto Office|
|OfficeVbaRuleViolation|Violazione della regola VBA di Office|
|OfficeVbaSummary|Riepilogo delle analisi VBA di Office|
|OperatingSystem|Sistema operativo|
|OperatingSystemEx|Sistema operativo esteso|
|OperatingSystemRecoveryConfiguration|Configurazione di ripristino del sistema operativo|
|OptionalFeature|Funzionalità facoltativa|
|Sistema operativo|Informazioni di base sul sistema operativo|
|PageFileSetting|Impostazione file di paging|
|ParallelPort|Porta parallela|
|Partizione|Partizioni disco|
|PCMCIAController|Controller PCMCIA|
|Disco fisico|Disco fisico|
|PhysicalMemory|Memoria fisica|
|PNPDEVICEDRIVER|Driver di dispositivo PNP|
|PointingDevice|Dispositivo di puntamento|
|PortableBattery|Batteria portatile|
|Porte|Porte|
|PowerCapabilities|Funzionalità alimentazione|
|PowerClientOptOutSettings|Impostazioni esclusione risparmio energia|
|PowerConfigurations|Configurazione risparmio energia|
|PowerManagementDaily|Dati giornalieri per risparmio energia|
|PowerManagementInsomniaReasons|Motivi di errore sospensione del risparmio energia|
|PowerManagementMonthly|Dati mensili di risparmio energia|
|PowerSettings|Impostazioni di risparmio energia|
|PrinterConfiguration|Configurazione stampante|
|PrinterDevice|Dispositivo stampante|
|PrintJobs|Processi di stampa|
|Processo|Processo in un sistema operativo|
|ProcessModule()|Moduli caricati da processi specificati|
|Processore|Processore|
|ProtectedVolumeInformation|Informazioni sul volume protette|
|Protocollo|Protocollo|
|QuickFixEngineering|Quick Fix Engineering|
|SCSIController|Controller SCSI|
|SerialPortConfiguration|Configurazione della porta seriale|
|SerialPorts|Porte seriali|
|ServerFeature|Funzionalità server|
|Servizio|Servizio in un sistema informatico che esegue Windows|
|Servizi|Servizi|
|Condivisioni|Condivisioni|
|SMBConfig|Configurazione SMB di un dispositivo|
|SMSAdvancedClientPorts|Porte del client di Configuration Manager|
|SMSAdvancedClientSSLConfigurations|Configurazioni SSL del client di Configuration Manager|
|SMSAdvancedClientState|Stato client di Configuration Manager|
|SMSDefaultBrowser|Browser predefinito|
|SMSSoftwareTag|Tag software|
|SMSWindows8Application|App di Windows|
|SMSWindows8ApplicationUserInfo|Informazioni per l'utente dell'app di Windows|
|SoftwareShortcut|Collegamento software|
|SoftwareUpdate|Aggiornamento software applicabile ma non installato nel dispositivo|
|SoundDevices|Dispositivi audio|
|SWLicensingProduct|Prodotto con gestione licenze software|
|SWLicensingService|Servizio gestione licenze software|
|SystemAccount|Account di sistema|
|SystemBootData|Dati avvio del sistema|
|SystemBootSummary|Riepilogo avvio del sistema|
|SystemConsoleUsage|Utilizzo console di sistema|
|SystemConsoleUser|Utente console di sistema|
|SystemDevices|Dispositivi di sistema|
|SystemDrivers|Driver di sistema|
|SystemEnclosure|System Enclosure|
|TapeDrive|Unità nastro|
|TimeZone|Fuso orario|
|TPM|TPM|
|TPMStatus|Stato TPM|
|TSIssuedLicense|Licenza rilasciata a TS|
|TSLicenseKeyPack|Key pack per le licenze TS|
|UninterruptiblePowerSupply|Gruppo di continuità|
|USBController|Controller USB|
|USBDevice|Dispositivo USB|
|Utente|Account utente con una connessione attiva al dispositivo|
|USMFolderRedirectionHealth|Integrità reindirizzamento cartelle|
|USMUserProfile|Integrità profilo utente|
|VideoController|Controller video|
|VirtualMachine|Macchina virtuale|
|VirtualMachine64|Macchina virtuale (64)|
|Volume|Volume|
|WindowsUpdate|Windows Update|
|WindowsUpdateAgentVersion|Versione dell'agente di Windows Update|
|WinEvent()|Eventi entro 24 ore (per impostazione predefinita) da un registro eventi di Windows|
|WriteFilterState|Stato del filtro di scrittura|

## <a name="table-operators"></a>Operatori di tabella

Gli operatori di tabella possono essere usati per filtrare, riepilogare e trasformare i flussi di dati. Sono attualmente supportati gli operatori seguenti:

|Operatori di tabella|Descrizione|
|---|---|
|count|Restituisce una tabella con un singolo record contenente il numero di record|
|distinct|Produce una tabella con la combinazione distinta delle colonne specificate della tabella di input|
|join|Consente di unire le righe di due tabelle in modo da formare una nuova tabella tramite la corrispondenza della riga per lo stesso dispositivo|
|order by|Ordina le righe della tabella di input in base a una o più colonne|
|project|Seleziona le colonne da includere, rinominare o eliminare e inserire nuove colonne calcolate|
|summarize|Produce una tabella che aggrega il contenuto della tabella di input|
|take|Restituisce fino al numero specificato di righe|
|top|Restituisce i primi record N ordinati in base alle colonne specificate|
|where|Filtra una tabella per ottenere il sottoinsieme di righe che soddisfa un predicato|

## <a name="scalar-operators"></a>Operatori scalari

La tabella seguente riepiloga gli operatori:

|Operatori|Descrizione|Esempio
|---|---|---|
|==|Uguale|`1 == 1, 'aBc' == 'AbC'`|
|!=|Diverso da|`1 != 2, 'abc' != 'abcd'`|
|< |Minore|`1 < 2, 'abc' < 'DEF'`|
|> |Maggiore|`2 > 1, 'xyz' > 'XYZ'`|
|<=|Minore o uguale a|`1 <= 2, 'abc' <= 'abc'`|
|>=|Maggiore o uguale a|`2 >= 1, 'abc' >= 'ABC'`|
|+|Aggiunta|`2 + 1, now() + 1d`|
|-|Sottrazione|`2 - 1, now() - 1h`|
|*|Moltiplicazione|`2 * 2`|
|/|Divisione|`2 / 1`|
|%|Modulo|`2 % 1`|
|like|Parte sinistra contiene una corrispondenza per Parte destra|`'abc' like '%B%'`|
|!like|LHS non contiene una corrispondenza per RHS|`'abc' !like '_d_'`|
|contains|RHS si verifica come sottosequenza di LHS|`'abc' contains 'b'`|
|!contains|RHS non si verifica in LHS|`'team' !contains 'i'`|
|startswith|RHS è una sottosequenza iniziale di LHS|`'team' startswith 'tea'`|
|!startswith|RHS non è una sottosequenza iniziale di LHS|`'abc' !startswith 'bc'`|
|endswith|RHS è una sottosequenza di chiusura di LHS|`'abc' endswith 'bc'`|
|!endswith|RHS non è una sottosequenza di chiusura di LHS|`'abc' !endswith 'a'`|
|e|True se e solo se RHS e LHS sono true|`(1 == 1) and (2 == 2)`|
|Oppure|True se e solo se RHS o LHS è true|`(1 == 1) or (1 == 2)`|

## <a name="aggregation-functions"></a>Funzioni di aggregazione

Le funzioni di aggregazione possono essere usate con l'operatore di tabella summarize per calcolare i valori riepilogati. Sono attualmente supportate le funzioni di aggregazione seguenti:

|Funzione|Descrizione|
|---|---|
|avg()|Restituisce la media dei valori nel gruppo|
|count()|Restituisce un numero di record per gruppo di riepilogo|
|countif()|Restituisce un numero di righe per cui il predicato restituisce true|
|dcount()|Restituisce il numero di valori distinti nel gruppo|
|max()|Restituisce il valore massimo nel gruppo|
|min()|Restituisce il valore minimo nel gruppo|
|percentile()|Restituisce una stima per il percentile specificato con classificazione più prossima della popolazione definita da Expr|
|sum()|Restituisce la somma di valori nel gruppo|
|sumif()|Restituisce una somma di espressioni per la quale il predicato restituisce true|

## <a name="scalar-functions"></a>Funzioni scalari

Le funzioni scalari possono essere usate nelle espressioni. Sono attualmente supportate le funzioni scalari seguenti:

|Funzione|Descrizione|
|---|---|
|ago()|sottrarre l'intervallo di tempo specificato dall'ora UTC corrente|
|bin()|Consente di arrotondare per difetto i valori a un numero di valori datetime multiplo di una dimensione di contenitore specificata|
|case()|Valuta un elenco di predicati e restituisce la prima espressione di risultato per la quale il predicato è soddisfatto|
|datetime_add()|Calcola un nuovo valore datetime da un valore datepart specificato moltiplicato per un importo specificato, aggiunto a un valore datetime specificato|
|datetime_diff()|Calcola la differenza tra due valori di tipo data/ora|
|iif()|Valuta il primo argomento e restituisce il valore del secondo o del terzo argomento, a seconda che il predicato restituisca true (secondo) o false (terzo)|
|indexof()|Funzione che restituisce l'indice in base zero della prima ricorrenza di una stringa specificata nella stringa di input|
|isnotnull()|Valuta il rispettivo argomento unico e restituisce un valore booleano che indica se l'argomento restituisce un valore non Null|
|isnull()|Valuta il rispettivo argomento unico e restituisce un valore booleano che indica se l'argomento restituisce un valore Null|
|now()|restituisce l'ora UTC corrente|
|strcat()|Concatena da 1 a 64 argomenti|
|strlen()|Restituisce la lunghezza in caratteri della stringa di input|
|substring()|Estrae una sottostringa da una stringa di origine a partire da un indice e fino alla fine della stringa|
|tostring()|Converte l'input in una rappresentazione di stringa|

## <a name="additional-entities-operators-and-functions-for-cmpivot-from-configuration-manager"></a><a name="bkmk_onprem_only"></a> Entità, operatori e funzioni aggiuntive per CMPivot da Configuration Manager

> [!Important]
> Gli elementi seguenti non sono supportati quando si esegue CMPivot dall'interfaccia di amministrazione di Microsoft Endpoint Manager.

|Tipo|Elemento|Descrizione|
|--|--|---|
|Entità|AccountSID|SID dell'account|
|Entità|FileContent()|Contenuto di un file specifico|
|Entità|NAPClient|Client NAP|
|Entità|NAPSystemHealthAgent|Agente integrità sistema NAP|
|Entità|Registry()|Tutti i valori per una chiave del Registro di sistema specifica<!--7371183-->|
|Operatore di tabella|render|Esegue il rendering dei risultati come output grafico|
