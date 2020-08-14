---
title: Registri eventi del server
titleSuffix: Configuration Manager
description: Riferimento tecnico per le possibili voci del server BitLocker (MBAM) nel registro eventi di Windows
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: reference
ms.assetid: c3279b7d-654d-444b-bd17-1262894590c3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fe7d24bc1cad27094d720a5cb5aa487caec9199d
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127866"
---
# <a name="server-event-logs"></a>Registri eventi del server

*Si applica a: Configuration Manager (Current Branch)*

<!--3601034-->

Usare il Visualizzatore eventi Windows per visualizzare i registri eventi per i componenti del server di gestione BitLocker seguenti in Configuration Manager:

- Servizio di ripristino nel punto di gestione
- Portale self-service
- Sito Web di amministrazione e monitoraggio

In un server che ospita uno o più di questi componenti, aprire il Visualizzatore eventi. Quindi passare a **Registri applicazioni e servizi**, **Microsoft**, **Windows** ed espandere **MBAM-Web**. Per impostazione predefinita sono presenti log eventi [Admin](#admin) e [Operativo](#operational).

Le sezioni seguenti contengono messaggi e informazioni per la risoluzione dei problemi relativi agli ID di eventi che possono verificarsi con i componenti del server di gestione BitLocker.

## <a name="admin"></a>Amministratore

### <a name="1-webappspnerror"></a>1: WebAppSpnError

Application: {SiteName}{VirtualDirectory} is missing the following Service Principal Names (SPNs):{ListOfSpns} Register the required SPNs on the account: {ExecutionAccount}. (L'applicazione: {SiteName}{VirtualDirectory} non dispone dei seguenti nomi dell'entità servizio (SPN):{ListOfSpns} Registrare i nomi SPN richiesti nell'account: {ExecutionAccount}).

Per il funzionamento dell'Autenticazione integrata di Windows devono essere presenti i nomi dell'entità servizio (SPN) necessari. Questo messaggio indica che il nome SPN richiesto per l'applicazione non è configurato correttamente. I dettagli inclusi in questo evento offrono altre informazioni.

<!-- See "Service Principal Name (SPN)" in MBAM 2.5 Server Prerequisites for Stand-alone and Configuration Manager Integration Topologies for more information. -->

### <a name="100-adminservicerecoverydberror"></a>100: AdminServiceRecoveryDbError

I possibili messaggi di errore sono:

- GetMachineUsers: An error occurred while getting user information from the database (errore durante il recupero delle informazioni utente dal database).
- GetRecoveryKey: an error occurred while getting recovery key from the database (errore durante il recupero della chiave di ripristino dal database).
- GetRecoveryKey: an error occurred while getting user information from the database (errore durante il recupero delle informazioni utente dal database).
- GetRecoveryKeyIds: an error occurred while getting recovery key Ids from the database (errore durante il recupero degli ID chiave di ripristino dal database).
- GetTpmHashForUser: An error occurred while getting TPM hash data from the recovery database (errore durante il recupero dei dati hash TPM dal database di ripristino).
- GetTpmHashForUser: An error occurred while getting TPM hash data from the recovery database (errore durante il recupero dei dati hash TPM dal database di ripristino).
- QueryDriveRecoveryData: An error occurred while getting drive recovery data from the database (errore durante il recupero dei dati di ripristino dell'unità dal database).
- QueryRecoveryKeyIdsForUser: An error occurred while getting recovery key Ids from the database (errore durante il recupero degli ID chiave di ripristino dal database).
- QueryVolumeUsers: An error occurred while getting user information from the database (errore durante il recupero delle informazioni utente dal database).

Questo messaggio viene registrato ogni volta che viene generata un'eccezione durante le comunicazioni con il database di ripristino. Leggere le informazioni contenute nella traccia per ottenere dettagli specifici sull'eccezione.

### <a name="101-adminservicecompliancedberror"></a>101: AdminServiceComplianceDbError

I possibili messaggi di errore sono:

- GetRecoveryKey: An error occurred while logging an audit event to the compliance database (errore durante la registrazione di un evento di controllo nel database di conformità).
- GetRecoveryKeyIds: An error occurred while logging an audit event to the compliance database (errore durante la registrazione di un evento di controllo nel database di conformità).
- GetTpmHashForUser: An error occurred while logging an audit event to the compliance database (errore durante la registrazione di un evento di controllo nel database di conformità).
- QueryRecoveryKeyIdsForUser: An error occurred while logging an audit event to the compliance database (errore durante la registrazione di un evento di controllo nel database di conformità).
- QueryDriveRecoveryData: An error occurred while logging an audit event to the compliance database (errore durante la registrazione di un evento di controllo nel database di conformità).

Questo messaggio viene registrato ogni volta che viene generata un'eccezione durante le comunicazioni con il database di conformità. Leggere le informazioni contenute nella traccia per ottenere dettagli specifici sull'eccezione.

### <a name="102-agentservicerecoverydberror"></a>102: AgentServiceRecoveryDbError

Questo messaggio indica un'eccezione quando il servizio prova a comunicare con il database di ripristino. Leggere il messaggio contenuto nell'evento per ottenere dettagli specifici sull'eccezione.

Verificare che l'account del pool di app MBAM abbia le autorizzazioni necessarie per connettersi al database di ripristino.

### <a name="103-agentserviceerror"></a>103: AgentServiceError

I possibili messaggi di errore sono:

- Unable to detect client machine account or data migration user account (Non è possibile rilevare l'account del computer client o l'account utente per la migrazione dei dati).

    Ogni volta che viene eseguita una chiamata ai metodi Web `PostKeyRecoveryInfo`, `IsRecoveryKeyResetRequired`, `CommitRecoveryKeyRest` o `GetTpmHash`, viene recuperato il contesto del chiamante per ottenere le credenziali del chiamante. Se il contesto del chiamante è null o vuoto, il servizio registra questo messaggio.

- Account verification failed for caller identity (Verifica dell'account non riuscita per l'identità del chiamante).

    Questo messaggio viene registrato se il metodo Web prevede che il chiamante sia un account di computer, ma è un'altra entità. Può anche verificarsi se il metodo Web prevede che il chiamante sia un account utente e non è un account utente né un membro di un account di gruppo di migrazione dati.

### <a name="104-statusservicecompliancedbconfigerror"></a>104: StatusServiceComplianceDbConfigError

The compliance database connection string in the registry is empty (La stringa di connessione del database di conformità nel Registro di sistema è vuota).

Questo messaggio viene registrato ogni volta che la stringa di connessione del database di conformità non è valida. Verificare il valore nella chiave del Registro di sistema `HKLM\Software\Microsoft\MBAM Server\Web\ComplianceDBConnectionString`.

### <a name="105-statusservicecompliancedberror"></a>105: StatusServiceComplianceDbError

Questo errore indica che i siti Web o i servizi Web non sono riusciti a connettersi al database di conformità. Verificare che l'account del pool di app IIS sia in grado di connettersi al database.

### <a name="106-helpdeskerror"></a>106: HelpdeskError

Errori noti e possibili cause:

- The request to URL caused an internal error (La richiesta all'URL ha causato un errore interno).

    Nell'applicazione è stata generata un'eccezione non gestita per il sito Web di amministrazione e monitoraggio (supporto tecnico). Per trovare l'eccezione specifica esaminare le voci di log nel registro eventi **Admin**.

- An error occurred while obtaining execution context information. Unable to verify Service Principal Name (SPN) registration (Errore durante il recupero di informazioni sul contesto di esecuzione. Non è possibile verificare la registrazione del nome dell'entità servizio (SPN)).

    Durante l'operazione iniziale di caricamento del sito Web del supporto tecnico, viene verificato il nome SPN. Per verificare il nome SPN sono necessarie le informazioni dell'account, il nome sito IIS e il valore ApplicationVirtualPath corrispondenti al sito Web del supporto tecnico. Questo messaggio di errore viene registrato quando uno o più di questi attributi non sono validi o sono mancanti.

- An error occurred while verifying Service Principal Name (SPN) registration (Errore durante la verifica della registrazione del nome dell'entità servizio (SPN)).

    Questo messaggio indica che viene generata un'eccezione di sicurezza durante la verifica del nome SPN. Vedere l'eccezione contenuta nei dettagli dell'evento.

### <a name="107-selfserviceportalerror"></a>107: SelfServicePortalError

Errori noti e possibili cause:

- An error occurred while getting recovery key for a user (Errore durante il recupero della chiave di ripristino per un utente)

    Indica che è stata generata un'eccezione imprevista quando è stata inoltrata una richiesta per il recupero di una chiave di ripristino. Vedere il messaggio dell'eccezione nei dettagli dell'evento. Se nell'app helpdesk è abilitata la traccia, vedere i dati di traccia per ottenere messaggi di eccezione dettagliati.

- An error occurred while obtaining execution context information. Unable to verify Service Principal Name (SPN) registration (Errore durante il recupero di informazioni sul contesto di esecuzione. Non è possibile verificare la registrazione del nome dell'entità servizio (SPN)).

    Durante un'operazione di caricamento iniziale il portale self-service recupera le informazioni sull'account, il nome sito IIS e ApplicationVirtualPath del sito Web self-service per la verifica del nome SPN. Questo messaggio di errore viene registrato quando uno o più di questi attributi non sono validi.

- An error occurred while verifying Service Principal Name (SPN) registration (Errore durante la verifica della registrazione del nome dell'entità servizio (SPN)). EventDetails:{ExceptionMessage}

    Questo messaggio indica che è stata generata un'eccezione di sicurezza durante la verifica del nome SPN. Vedere l'eccezione contenuta nei dettagli dell'evento.

### <a name="108-domaincontrollererror"></a>108: DomainControllerError

Errori noti e possibili cause:

- An error occurred while resolving domain name {DomainName}, a memory allocation failure occurred (Errore durante la risoluzione del nome di dominio {DomainName}, errore di allocazione della memoria).

    Per risolvere il nome di dominio, viene chiamata l'API Windows `DsGetDcName`. Questo messaggio viene registrato quando l'API restituisce `ERROR_NOT_ENOUGH_MEMORY`, che indica un errore di allocazione della memoria.

- Could not invoke DsGetDcName method (Non è stato possibile chiamare il metodo DsGetDcName)

    Questo messaggio indica che l'API `DsGetDcName` non è disponibile nell'host.

### <a name="109-webapprecoverydberror"></a>109: WebAppRecoveryDbError

Errori noti e possibili cause:

- An error occurred while reading the configuration of the Recovery database. The connection string to the Recovery database is not configured (Errore durante la lettura della configurazione del database di ripristino. La stringa di connessione al database di ripristino non è configurata).

    Questo messaggio indica che le informazioni nella stringa di connessione del database di ripristino in `HKLM\Software\Microsoft\MBAM Server\Web\RecoveryDBConnectionString` non sono valide. Verificare il valore della chiave del Registro di sistema specificata.

Se viene visualizzato uno dei messaggi seguenti, verificare se le credenziali del pool di applicazioni del server IIS consentono di stabilire una connessione al database di ripristino:

- DoesUserHaveMatchingRecoveryKey: an error occurred while getting recovery key Ids for a user (errore durante il recupero della chiave di ripristino per un utente).
- QueryDriveRecoveryData: an error occurred while getting drive recovery data (errore durante il recupero dei dati di ripristino dell'unità).
- QueryRecoveryKeyIdsForUser: an error occurred while getting recovery key Ids for a user (errore durante il recupero degli ID chiave di ripristino per un utente).
- An error occurred while getting TPM password hash from the Recovery database (Errore durante il recupero dell'hash della password TPM dal database di ripristino).

### <a name="110-webappcompliancedberror"></a>110: WebAppComplianceDbError

Errori noti e possibili cause:

- An error occurred while reading the configuration of the Compliance database. The connection string to the Compliance database is not configured. (Errore durante la lettura della configurazione del database di conformità. La stringa di connessione al database di conformità non è configurata).

    Questo messaggio indica che le informazioni nella stringa di connessione del database di conformità in `HKLM\Software\Microsoft\MBAM Server\Web\ComplianceDBConnectionString` non sono valide. Verificare il valore di questa chiave del Registro di sistema.

Se viene visualizzato uno dei messaggi seguenti, verificare se le credenziali del pool di applicazioni del server IIS consentono di stabilire una connessione al database di conformità:

- GetRecoveryKeyForCurrentUser: an error occurred while logging an audit event to the Compliance database (errore durante la registrazione di un evento di controllo nel database di conformità).
- QueryRecoveryKeyIdsForUser: an error occurred while logging an audit event to the Compliance database (errore durante la registrazione di un evento di controllo nel database di conformità).
- QueryRecoveryKeyIdsForUser: an error occurred while logging an audit event to the Compliance database (errore durante la registrazione di un evento di controllo nel database di conformità).

### <a name="111-webappdberror"></a>111: WebAppDbError

Questi errori indicano una delle due condizioni seguenti

- I siti Web e i servizi Web MBAM non sono riusciti a connettersi al database di conformità o di ripristino
- L'account di esecuzione dei siti Web/servizi Web MBAM (account del pool di app) non è riuscito a eseguire la stored procedure `GetVersion` nel database di conformità o di ripristino

Il messaggio contenuto nell'evento include altri dettagli sull'eccezione.

Verificare che l'account del pool di applicazioni sia in grado di connettersi ai database di conformità o di ripristino. Verificare anche che disponga delle autorizzazioni per eseguire la stored procedure `GetVersion`.

### <a name="112-webapperror"></a>112: WebAppError

An error occurred while verifying Service Principal Name (SPN) registration (Errore durante la verifica della registrazione del nome dell'entità servizio (SPN)).

Per verificare il nome SPN, viene eseguita una query in Active Directory per recuperare un elenco di account di esecuzione SPN mappati. Viene anche eseguita una query su `ApplicationHost.config` per ottenere i binding del sito Web. Questo messaggio di errore indica che non è stato possibile comunicare con Active Directory oppure non è stato possibile caricare il file `ApplicationHost.config`.

Verificare che l'account del pool di app disponga delle autorizzazioni per eseguire query in Active Directory o nel file `ApplicationHost.config`. Verificare anche le voci di binding del sito nel file `ApplicationHost.config`.

## <a name="operational"></a>Operativo

### <a name="4-performancecountererror"></a>4: PerformanceCounterError

An error occurred while retrieving a performance counter (Errore durante il recupero di un contatore delle prestazioni).

Il messaggio di traccia contiene il messaggio di eccezione. Alcuni di questi messaggi sono elencati di seguito:

- ArgumentNullException: This exception is thrown if the category, counter, or instance of requested Performance counter is invalid (questa eccezione viene generata se la categoria, il contatore o l'istanza del contatore delle prestazioni richiesto non sono validi).
- System.InvalidOperationException: categoryName is an empty string ("") (categoryName è una stringa vuota ("")). counterName is an empty string("") (counterName è una stringa vuota ("")).
- The read/write permission setting requested is invalid for this counter (L'impostazione dell'autorizzazione di lettura/scrittura richiesta non è valida per questo contatore).
- The category specified does not exist (if readOnly is true) (La categoria specificata non esiste (se readOnly è true)).
- The category specified is not a .NET Framework custom category (if readOnly is false) (La categoria specificata non è una categoria .NET Framework personalizzata (se readOnly è false)).
- The category specified is marked as multi-instance and requires the performance counter to be created with an instance name (La categoria specificata è contrassegnata come categoria a più istanze ed è necessario che il contatore delle prestazioni venga creato con un nome di istanza).
- instanceName is longer than 127 characters (La lunghezza di instanceName è maggiore di 127 caratteri).
- categoryName and counterName have been localized into different languages (categoryName e counterName sono stati localizzati in lingue diverse).
- System.ComponentModel.Win32Exception: An error occurred when accessing a system API (errore durante l'accesso a un'API di sistema).
- System.UnauthorizedAccessException: Code that is executing without administrative privileges attempted to read a performance counter (Il codice in esecuzione senza privilegi amministrativi ha provato a leggere un contatore delle prestazioni).

Il messaggio contenuto nell'evento include altri dettagli sull'eccezione.

Per `System.UnauthorizedAccessException`, verificare che l'account del pool di app abbia accesso alle API del contatore delle prestazioni.

### <a name="200-helpdeskinformation"></a>200: HelpDeskInformation

The administration website application successfully found and connected to a supported version of the recovery/compliance database (L'applicazione del sito Web di amministrazione ha rilevato e stabilito la connessione a una versione supportata del database di ripristino/conformità).

Indica una connessione riuscita al database di ripristino o di conformità dal sito Web del supporto tecnico.

### <a name="201-selfserviceportalinformation"></a>201: SelfServicePortalInformation

The self-service portal application successfully found and connected to a supported version of the recovery/compliance database (L'applicazione del portale self-service ha rilevato e stabilito la connessione a una versione supportata del database di ripristino/conformità).

Indica una connessione riuscita al database di ripristino o di conformità dal portale self-service.

### <a name="202-webappinformation"></a>202: WebAppInformation

Application has its SPNs registered correctly (I nomi SPN dell'applicazione sono registrati correttamente).

Indica che i nomi SPN richiesti per il sito Web del supporto tecnico sono registrati correttamente rispetto all'account in esecuzione.

## <a name="see-also"></a>Vedere anche

Per altre informazioni sull'uso di questi registri, vedere [Registri eventi di BitLocker](about-event-logs.md).

Per altre informazioni sulla risoluzione dei problemi, vedere [Risolvere i problemi relativi a BitLocker](troubleshoot.md).

Per altre informazioni sull'installazione di questi siti Web, vedere [Configurare i report e i portali di BitLocker](../../deploy-use/bitlocker/setup-websites.md).
