---
title: Opzioni della riga di comando per la configurazione
titleSuffix: Configuration Manager
description: Creare script di automazione per installare Configuration Manager dalla riga di comando.
ms.date: 08/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0da167f1-52cf-4dfd-8f73-833ca3eb8478
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8e4950e32fa5ddc0a4fc1a13ec8e584dc1ae9ff3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700819"
---
# <a name="command-line-options-for-configuration-manager-setup"></a>Opzioni della riga di comando per la configurazione di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Usare le informazioni seguenti per configurare gli script o installare Configuration Manager dalla riga di comando.  

## <a name="command-line-options-for-setup"></a><a name="bkmk_setup"></a> Opzioni della riga di comando per l'installazione

Eseguire il programma di installazione dalla directory `\BIN\X64` del percorso di installazione di Configuration Manager nel server del sito.

### `/DEINSTALL`

Disinstallare il sito. Eseguire l'installazione dal computer del server del sito.  

### `/DONTSTARTSITECOMP`

Consente di installare un sito, ma impedisce l'avvio del servizio Gestione componenti del sito. Fino all'avvio del servizio Gestione componenti del sito, il sito non è attivo. Gestione componenti del sito si occupa dell'installazione e dell'avvio del servizio SMS_Executive, nonché di processi aggiuntivi nel sito. Al termine dell'installazione del sito, in seguito all'avvio del servizio Gestione componenti del sito verranno installati il servizio SMS_Executive e i processi aggiuntivi necessari per il funzionamento del sito.  

### `/HIDDEN`

Consente di nascondere l'interfaccia utente durante l'installazione. Usare questa opzione solo in combinazione con l'opzione **/SCRIPT**. Il file script di installazione automatica deve fornire tutte le opzioni necessarie. In caso contrario, l'installazione avrà esito negativo.  

### `/NOUSERINPUT`

Disabilita l'input utente durante l'installazione, ma visualizza l'installazione guidata. Usare questa opzione solo in combinazione con l'opzione **/SCRIPT**. Il file script di installazione automatica deve fornire tutte le opzioni necessarie. In caso contrario, l'installazione avrà esito negativo.  

### `/RESETSITE`

Consente di eseguire una reimpostazione del sito per reimpostare gli account di servizio e di database per il sito.

Per altre informazioni, vedere [Eseguire una reimpostazione del sito](../../manage/modify-your-infrastructure.md#bkmk_reset).  

### `/TESTDBUPGRADE`

Consente di eseguire un test in un backup del database del sito per verificare che il database possa essere aggiornato.

> [!IMPORTANT]  
> Non eseguire questa opzione della riga di comando nel database del sito di produzione. L'esecuzione di questa opzione della riga di comando nel database del sito di produzione comporta l'aggiornamento del database del sito e potrebbe rendere inutilizzabile il sito.

#### <a name="usage"></a>Utilizzo

Specificare il nome dell'istanza e il nome del database per il database del sito. Se si specifica solo il nome del database, il programma di installazione usa il nome dell'istanza predefinita.  

`/TESTDBUPGRADE <Instance name>\<Database name>`

`/TESTDBUPGRADE CM_ABC`

`/TESTDBUPGRADE Named\CM_ABC`

### `/UPGRADE`

Consente di eseguire l'aggiornamento automatico di un sito. Specificare il codice Product Key compresi i trattini (`-`). Specificare anche il percorso dei file di prerequisito dell'installazione scaricati in precedenza.  

Per altre informazioni sui file di prerequisito dell'installazione, vedere la sezione [Downloader di installazione](setup-downloader.md).  

#### <a name="usage"></a>Utilizzo

`setupwpf.exe /UPGRADE xxxxx-xxxxx-xxxxx-xxxxx-xxxxx <path to external component files>`  

### `/SCRIPT`

Consente di eseguire un'installazione automatica. Con questa opzione usare un file di inizializzazione dell'installazione. Per altre informazioni su come eseguire l'installazione automatica, vedere [Usare una riga di comando per Installare siti tramite la riga di comando](use-a-command-line-to-install-sites.md).  

#### <a name="usage"></a>Utilizzo

`/SCRIPT <setup script path>`

### `/SDKINST`

Consente di installare il provider SMS nel computer specificato. Specificare il nome di dominio completo (FQDN) per il computer del provider SMS. Per altre informazioni sul provider SMS, vedere [Pianificare per il provider SMS](../../../plan-design/hierarchy/plan-for-the-sms-provider.md).  

#### <a name="usage"></a>Utilizzo

`/SDKINST <SMS Provider FQDN>`

### `/SDKDEINST`

Consente di disinstallare il provider SMS nel computer specificato. Specificare l'FQDN per il computer del provider SMS.  

#### <a name="usage"></a>Utilizzo

`/SDKDEINST <SMS Provider FQDN>`

### `/MANAGELANGS`

Consente di gestire le lingue installate in un sito installato precedentemente. Specificare il percorso per il file script delle lingue che contiene le impostazioni delle lingue. Per altre informazioni, vedere la sezione [Opzioni della riga di comando per la gestione delle lingue](#bkmk_Lang).  

#### <a name="usage"></a>Utilizzo

`/MANAGELANGS <Language script path>`


## <a name="command-line-options-to-manage-languages"></a><a name="bkmk_Lang"></a> Opzioni della riga di comando per la gestione delle lingue

### <a name="identification"></a>Identification

- **Nome chiave:** Action  

    - **Richiesto:** Sì  

    - **Valori:** `ManageLanguages`  

    - **Dettagli:** Gestisce il supporto lingua di client per dispositivi mobili, client e server in un sito.  

### <a name="options"></a>Options

- **Nome chiave:** AddServerLanguages  

    - **Richiesto:** No  

    - **Valori:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    - **Dettagli:** specifica le lingue del server che saranno disponibili per la console di Configuration Manager, i report e gli oggetti di Configuration Manager. L'inglese è disponibile per impostazione predefinita.  

- **Nome chiave:** AddClientLanguages  

    - **Richiesto:** No  

    - **Valori:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    - **Dettagli:** Specifica le lingue che saranno disponibili per i computer client. L'inglese è disponibile per impostazione predefinita.  

- **Nome chiave:** DeleteServerLanguages  

    - **Richiesto:** No  

    - **Valori:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    - **Dettagli:** Specifica le lingue da rimuovere e che non saranno più disponibili per la console di Configuration Manager, i report e gli oggetti di Configuration Manager. La lingua inglese è disponibile per impostazione predefinita e non può essere rimossa.  

- **Nome chiave:** DeleteClientLanguages  

    - **Richiesto:** No  

    - **Valori:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    - **Dettagli:** Specifica le lingue da rimuovere e che non saranno più disponibili per i computer client. La lingua inglese è disponibile per impostazione predefinita e non può essere rimossa.  

- **Nome chiave:** MobileDeviceLanguage  

    - **Richiesto:** Sì  

    - **Valori:**

        - `0` = Non installare  

        - `1` = Installare  

    - **Dettagli:** Specifica se le lingue del dispositivo mobile client sono installate.  

- **Nome chiave:** PrerequisiteComp  

    - **Richiesto:** Sì  

    - **Valori:**

        - `0` = Scaricare  

        - `1` = Già scaricato  

    - **Dettagli:** specifica se i file dei prerequisiti di installazione sono già stati scaricati. Se ad esempio si usa il valore `0`, il programma di installazione eseguirà il download dei file.  

- **Nome chiave:** PrerequisitePath  

    - **Richiesto:** Sì  

    - **Valori:**  <*Percorso dei file dei prerequisiti di installazione*>  

    - **Dettagli:** specifica il percorso dei file dei prerequisiti di installazione. A seconda del valore di **PrerequisiteComp**, il programma di installazione usa questo percorso per archiviare i file scaricati oppure per individuare file scaricati in precedenza.  


## <a name="unattended-setup-script-file-keys"></a><a name="bkmk_Unattended"></a> Chiavi di file script di installazione automatica

Usare le sezioni seguenti per facilitare la creazione dello script per l'installazione automatica. Gli elenchi mostrano quanto segue:

- Chiavi dello script di installazione disponibili e valori corrispondenti
- Se sono necessarie
- Tipo di installazione per cui vengono usate
- Descrizione breve della chiave

### <a name="unattended-install-for-a-central-administration-site-cas"></a>Installare automaticamente un sito di amministrazione centrale

Usare i dettagli seguenti per installare un sito di amministrazione centrale usando un file script di installazione automatica.  

#### <a name="identification"></a>Identification

- **Nome chiave:** Action  

    - **Richiesto:** Sì  

    - **Valori:** `InstallCAS`  

    - **Dettagli:** Installa un sito di amministrazione centrale.  

- **Nome chiave:** CDLatest  

    - **Richiesto:** sì, solo quando si usano supporti dalla cartella CD.Latest.

    - **Valori:**

        - `1` = si usano supporti dalla cartella CD.Latest

        - Qualsiasi valore diverso da 1 indica che non si usano supporti dalla cartella CD.Latest

    - **Dettagli:** Quando si installa o si ripristina un sito primario o un sito di amministrazione centrale e si esegue il programma di installazione dalla cartella CD.Latest, includere questa chiave e il valore. Questo valore indica al programma di installazione che si usano supporti dalla cartella CD.Latest.

#### <a name="options"></a>Options

- **Nome chiave:** ProductID  

    - **Richiesto:** Sì  

    - **Valori:**

        - `<xxxxx-xxxxx-xxxxx-xxxxx-xxxxx>` = un codice Product Key valido con trattini

        - `Eval` = installa la versione di valutazione di Configuration Manager

    - **Dettagli:** specifica il codice Product Key per l'installazione di Configuration Manager, trattini inclusi.

- **Nome chiave:** SiteCode  

    - **Richiesto:** Sì  

    - **Valori:**  <*codice del sito*>, ad esempio `ABC`

    - **Dettagli:** Specifica i tre caratteri alfanumerici che identificano in modo univoco il sito nella gerarchia.  

- **Nome chiave:** Nome sito  

    - **Richiesto:** Sì  

    - **Valori:**  <*Nome del sito*>  

    - **Dettagli:** Specifica il nome del sito.  

- **Nome chiave:** SMSInstallDir  

    - **Richiesto:** Sì  

    - **Valori:**  <*Percorso di installazione di Configuration Manager*>  

    - **Dettagli:** specifica la cartella di installazione per i file di programma di Configuration Manager.  

- **Nome chiave:** SDKServer  

    - **Richiesto:** Sì  

    - **Valori:**  <*FQDN del provider SMS*>  

    - **Dettagli:** Specifica il nome FQDN del server che ospiterà il provider SMS. Dopo l'installazione iniziale, è possibile configurare altri provider SMS per il sito.  

- **Nome chiave:** PrerequisiteComp  

    - **Richiesto:** Sì  

    - **Valori:**

        - `0` = Scaricare  

        - `1` = Già scaricato  

    - **Dettagli:** specifica se i file dei prerequisiti di installazione sono già stati scaricati. Se ad esempio si usa il valore `0`, il programma di installazione eseguirà il download dei file.  

- **Nome chiave:** PrerequisitePath  

    - **Richiesto:** Sì  

    - **Valori:**  <*Percorso dei file dei prerequisiti di installazione*>  

    - **Dettagli:** specifica il percorso dei file dei prerequisiti di installazione. A seconda del valore di **PrerequisiteComp**, il programma di installazione usa questo percorso per archiviare i file scaricati oppure per individuare file scaricati in precedenza.  

- **Nome chiave:** AdminConsole  

    - **Richiesto:** Sì  

    - **Valori:**

        - `0` = Non installare  

        - `1` = Installare  

    - **Dettagli:** Specifica se installare la console di Configuration Manager.  

- **Nome chiave:** JoinCEIP  

    > [!Note]  
    > A partire da Configuration Manager versione 1802 la funzionalità Analisi utilizzo software è stata rimossa dal prodotto.

    - **Richiesto:** Sì  

    - **Valori:**

        - `0` = Non partecipare  

        - `1` = Partecipare  

    - **Dettagli:** Specifica se partecipare all'Analisi utilizzo software (CEIP).  

- **Nome chiave:** AddServerLanguages  

    - **Richiesto:** No  

    - **Valori:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    - **Dettagli:** specifica le lingue del server che saranno disponibili per la console di Configuration Manager, i report e gli oggetti di Configuration Manager. L'inglese è disponibile per impostazione predefinita.  

- **Nome chiave:** AddClientLanguages  

    - **Richiesto:** No  

    - **Valori:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    - **Dettagli:** Specifica le lingue che saranno disponibili per i computer client. L'inglese è disponibile per impostazione predefinita.  

- **Nome chiave:** DeleteServerLanguages  

    - **Richiesto:** No  

    - **Valori:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    - **Dettagli:** Modifica un sito dopo l'installazione. Specifica le lingue da rimuovere e che non saranno più disponibili per la console di Configuration Manager, i report e gli oggetti di Configuration Manager. La lingua inglese è disponibile per impostazione predefinita e non può essere rimossa.  

- **Nome chiave:** DeleteClientLanguages  

    - **Richiesto:** No  

    - **Valori:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    - **Dettagli:** Modifica un sito dopo l'installazione. Specifica le lingue da rimuovere e che non saranno più disponibili per i computer client. La lingua inglese è disponibile per impostazione predefinita e non può essere rimossa.  

- **Nome chiave:** MobileDeviceLanguage  

    - **Richiesto:** Sì  

    - **Valori:**

        - `0` = Non installare  

        - `1` = Installare  

    - **Dettagli:** Specifica se le lingue del dispositivo mobile client sono installate.  

#### <a name="sqlconfigoptions"></a>SQLConfigOptions

- **Nome chiave:** SQLServerName  

    - **Richiesto:** Sì  

    - **Valori:**  <*Nome dell'istanza di SQL Server*>  

    - **Dettagli:** specifica il nome del server o il nome dell'istanza in cluster che esegue SQL Server per ospitare il database del sito.  

- **Nome chiave:** DatabaseName  

    - **Richiesto:** Sì  

    - **Valori:**  <*Nome del database del sito*> oppure <*Nome dell'istanza*>\\<*Nome del database del sito*>  

    - **Dettagli:** specifica il nome del database SQL Server da creare o del database SQL Server da usare per l'installazione del database del sito di amministrazione centrale.  

        > [!IMPORTANT]  
        > Se non si usa l'istanza predefinita, specificare il nome dell'istanza e il nome del database del sito.  

- **Nome chiave:** SQLSSBPort  

    - **Richiesto:** No  

    - **Valori:**  <*Numero della porta SSB*>  

    - **Dettagli:** Specifica la porta di SQL Server Service Broker (SSB) usata da SQL Server. Per impostazione predefinita, SSB usa la porta TCP 4022, ma è possibile usare una porta diversa.  

- **Nome chiave:** SQLDataFilePath  

    - **Richiesto:** No  

    - **Valori:**  <*Percorso del file mdb del database*>  

    - **Dettagli:** specifica un percorso alternativo per creare il file mdb del database.  

- **Nome chiave:** SQLLogFilePath  

    - **Richiesto:** No  

    - **Valori:**  <*Percorso del file ldf del database*>  

    - **Dettagli:** specifica un percorso alternativo per creare il file ldf del database.  

#### <a name="cloudconnectoroptions"></a>CloudConnectorOptions

- **Nome chiave:** CloudConnector  

    - **Richiesto:** Sì  

    - **Valori:**

        - `0` = Non installare  

        - `1` = Installare  

    - **Dettagli:** specifica se installare un punto di connessione del servizio in questo sito. Poiché il punto di connessione del servizio può essere installato solo nel sito di livello superiore di una gerarchia, impostare questo valore su `1` per un sito primario figlio.  

- **Nome chiave:** CloudConnectorServer  

    - **Richiesto:** obbligatorio quando **CloudConnector** è uguale a 1  

    - **Valori:**  <*FQDN del server del punto di connessione del servizio*>  

    - **Dettagli:** specifica il nome FQDN del server che ospiterà il ruolo del sistema del sito del punto di connessione del servizio.  

- **Nome chiave:** UseProxy  

    - **Richiesto:** obbligatorio quando **CloudConnector** è uguale a 1  

    - **Valori:**

        - `0` = Non installare  

        - `1` = Installare  

    - **Dettagli:** specifica se il punto di connessione del servizio usa un server proxy.  

- **Nome chiave:** ProxyName  

    - **Richiesto:** obbligatorio quando **UseProxy** è uguale a 1  

    - **Valori:**  <*FQDN del server proxy*>  

    - **Dettagli:** specifica il nome FQDN del server proxy usato dal punto di connessione del servizio.  

- **Nome chiave:** ProxyPort  

    - **Richiesto:** obbligatorio quando **UseProxy** è uguale a 1  

    - **Valori:**  <*Numero della porta*>  

    - **Dettagli:** specifica il numero della porta da usare per la porta del proxy.  

#### <a name="sabranchoptions"></a>SABranchOptions

<!-- SCCMDocs#390 -->

- **Nome chiave:** SAActive

    - **Richiesto:** No

    - **Valori:**

        - `0` = Non si ha Software Assurance

        - `1` = Software Assurance è attivo

    - **Dettagli:** specifica se si ha Software Assurance attivo. Per altre informazioni, vedere [Domande frequenti su prodotto e licenze](../../../understand/product-and-licensing-faq.md).

- **Nome chiave:** CurrentBranch

    - **Richiesto:** No

    - **Valori:**

        - `0` = Installa LTSB

        - `1` = Installa Current Branch

    - **Dettagli:** specifica se usare Configuration Manager (Current Branch) o Configuration Manager (Long-Term Servicing Branch, LTSB). Per altre informazioni, vedere [Scelta del ramo di Configuration Manager da usare](../../../understand/which-branch-should-i-use.md).

### <a name="unattended-install-for-a-primary-site"></a>Installare automaticamente un sito primario

Usare i dettagli seguenti per installare un sito primario usando un file script di installazione automatica.  

#### <a name="identification"></a>Identification

- **Nome chiave:** Action  

    - **Richiesto:** Sì  

    - **Valori:** `InstallPrimarySite`  

    - **Dettagli:** Installa un sito primario.  

- **Nome chiave:** CDLatest  

    - **Richiesto:** sì, solo quando si usano supporti dalla cartella CD.Latest.

    - **Valori:**

        - `1` = si usano supporti dalla cartella CD.Latest

        - Qualsiasi valore diverso da 1 indica che non si usano supporti dalla cartella CD.Latest

    - **Dettagli:** Quando si installa o si ripristina un sito primario o un sito di amministrazione centrale e si esegue il programma di installazione dalla cartella CD.Latest, includere questa chiave e il valore. Questo valore indica al programma di installazione che si usano supporti dalla cartella CD.Latest.

#### <a name="options"></a>Options

- **Nome chiave:** ProductID  

    - **Richiesto:** Sì  

    - **Valori:**

        - `<xxxxx-xxxxx-xxxxx-xxxxx-xxxxx>` = un codice Product Key valido con trattini

        - `Eval` = installa la versione di valutazione di Configuration Manager

    - **Dettagli:** specifica il codice Product Key per l'installazione di Configuration Manager, trattini inclusi.

- **Nome chiave:** SiteCode  

    - **Richiesto:** Sì  

    - **Valori:**  <*Codice del sito*>  

    - **Dettagli:** Specifica i tre caratteri alfanumerici che identificano in modo univoco il sito nella gerarchia.  

- **Nome chiave:** SiteName  

    - **Richiesto:** Sì  

    - **Valori:**  <*Nome del sito*>  

    - **Dettagli:** Specifica il nome del sito.  

- **Nome chiave:** SMSInstallDir  

    - **Richiesto:** Sì  

    - **Valori:**  <*Percorso di installazione di Configuration Manager*>

    - **Dettagli:** specifica la cartella di installazione per i file di programma di Configuration Manager.  

- **Nome chiave:** SDKServer  

    - **Richiesto:** Sì  

    - **Valori:**  <*FQDN del provider SMS*>  

    - **Dettagli:** Specifica il nome FQDN del server che ospiterà il provider SMS. Dopo l'installazione iniziale, è possibile configurare altri provider SMS per il sito.  

- **Nome chiave:** PrerequisiteComp  

    - **Richiesto:** Sì  

    - **Valori:**

        - `0` = Scaricare  

        - `1` = Già scaricato  

    - **Dettagli:** specifica se i file dei prerequisiti di installazione sono già stati scaricati. Se ad esempio si usa il valore `0`, il programma di installazione eseguirà il download dei file.  

- **Nome chiave:** PrerequisitePath  

    - **Richiesto:** Sì  

    - **Valori:**  <*Percorso dei file dei prerequisiti di installazione*>  

    - **Dettagli:** specifica il percorso dei file dei prerequisiti di installazione. A seconda del valore di **PrerequisiteComp**, il programma di installazione usa questo percorso per archiviare i file scaricati oppure per individuare file scaricati in precedenza.  

- **Nome chiave:** AdminConsole  

    - **Richiesto:** Sì  

    - **Valori:**

        - `0` = Non installare  

        - `1` = Installare  

    - **Dettagli:** Specifica se installare la console di Configuration Manager.  

- **Nome chiave:** JoinCEIP  

    > [!Note]  
    > A partire da Configuration Manager versione 1802 la funzionalità Analisi utilizzo software è stata rimossa dal prodotto.

    - **Richiesto:** Sì  

    - **Valori:**

        - `0` = Non partecipare  

        - `1` = Partecipare  

    - **Dettagli:** specifica se partecipare al programma Analisi utilizzo software.  

- **Nome chiave:** ManagementPoint  

    - **Richiesto:** No  

    - **Valori:**  < *FQDN del server del sito del punto di gestione*>  

    - **Dettagli:** Specifica il nome FQDN del server che ospiterà il ruolo del sistema del sito del punto di gestione.  

- **Nome chiave:** ManagementPointProtocol  

    - **Richiesto:** No  

    - **Valori:** `HTTPS` o `HTTP`  

    - **Dettagli:** Specifica il protocollo da usare per il punto di gestione.  

- **Nome chiave:** DistributionPoint  

    - **Richiesto:** No  

    - **Valori:**  <*FQDN del server del sito del punto di distribuzione*>  

    - **Dettagli:** specifica il nome FQDN del server che ospiterà il ruolo del sistema del sito del punto di distribuzione.  

- **Nome chiave:** DistributionPointProtocol  

    - **Richiesto:** No  

    - **Valori:** `HTTPS` o `HTTP`  

    - **Dettagli:** Specifica il protocollo da usare per il punto di distribuzione.  

- **Nome chiave:** RoleCommunicationProtocol  

    - **Richiesto:** Sì  

    - **Valori:** `EnforceHTTPS` o `HTTPorHTTPS`  

    - **Dettagli:** specifica se configurare tutti i sistemi del sito per l'accettazione delle sole comunicazioni HTTPS dai client oppure se configurare un metodo di comunicazione per ogni ruolo del sistema del sito. Se si seleziona `EnforceHTTPS`, i client devono avere un certificato di infrastruttura a chiave pubblica (PKI) valido per l'autenticazione client.  

- **Nome chiave:** ClientsUsePKICertificate  

    - **Richiesto:** Sì  

    - **Valori:**

        - `0` = Non usare  

        - `1` = Usare  

    - **Dettagli:** Specifica se i client useranno un certificato PKI client per la comunicazione con i ruoli del sistema del sito.  

- **Nome chiave:** AddServerLanguages  

    - **Richiesto:** No  

    - **Valori:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    - **Dettagli:** specifica le lingue del server che saranno disponibili per la console di Configuration Manager, i report e gli oggetti di Configuration Manager. L'inglese è disponibile per impostazione predefinita.  

- **Nome chiave:** AddClientLanguages  

    - **Richiesto:** No  

    - **Valori:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    - **Dettagli:** Specifica le lingue che saranno disponibili per i computer client. L'inglese è disponibile per impostazione predefinita.  

- **Nome chiave:** DeleteServerLanguages  

    - **Richiesto:** No  

    - **Valori:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    - **Dettagli:** Modifica un sito dopo l'installazione. Specifica le lingue da rimuovere e che non saranno più disponibili per la console di Configuration Manager, i report e gli oggetti di Configuration Manager. La lingua inglese è disponibile per impostazione predefinita e non può essere rimossa.  

- **Nome chiave:** DeleteClientLanguages  

    - **Richiesto:** No  

    - **Valori:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    - **Dettagli:** Modifica un sito dopo l'installazione. Specifica le lingue da rimuovere e che non saranno più disponibili per i computer client. La lingua inglese è disponibile per impostazione predefinita e non può essere rimossa.  

- **Nome chiave:** MobileDeviceLanguage  

    - **Richiesto:** Sì  

    - **Valori:**

        - `0` = Non installare  

        - `1` = Installare  

    - **Dettagli:** Specifica se le lingue del dispositivo mobile client sono installate.  

#### <a name="sqlconfigoptions"></a>SQLConfigOptions

- **Nome chiave:** SQLServerName  

    - **Richiesto:** Sì  

    - **Valori:**  <*Nome dell'istanza di SQL Server*>  

    - **Dettagli:** specifica il nome del server o il nome dell'istanza in cluster che esegue SQL Server per ospitare il database del sito.  

- **Nome chiave:** DatabaseName  

    - **Richiesto:** Sì  

    - **Valori:**  <*Nome del database del sito*> oppure <*Nome dell'istanza*>\\<*Nome del database del sito*>  

    - **Dettagli:** specifica il nome del database di SQL Server da creare o del database di SQL Server da usare per l'installazione del database del sito primario.  

        > [!IMPORTANT]  
        > Se non si usa l'istanza predefinita, specificare il nome dell'istanza e il nome del database del sito.  

- **Nome chiave:** SQLSSBPort  

    - **Richiesto:** No  

    - **Valori:**  <*Numero della porta SSB*>  

    - **Dettagli:** specifica la porta SSB usata da SQL Server. Per impostazione predefinita, SSB usa la porta TCP 4022, ma è possibile usare una porta diversa.  

- **Nome chiave:** SQLDataFilePath  

    - **Richiesto:** No  

    - **Valori:**  <*Percorso del file mdb del database*>  

    - **Dettagli:** specifica un percorso alternativo per creare il file mdb del database.  

- **Nome chiave:** SQLLogFilePath  

    - **Richiesto:** No  

    - **Valori:**  <*Percorso del file ldf del database*>  

    - **Dettagli:** specifica un percorso alternativo per creare il file ldf del database.  

#### <a name="hierarchyexpansionoption"></a>HierarchyExpansionOption

- **Nome chiave:** CCARSiteServer  

    - **Richiesto:** No  

    - **Valori:**  <*FQDN del sito di amministrazione centrale*>  

    - **Dettagli:** specifica il sito di amministrazione centrale a cui si collega il sito primario quando viene aggiunto alla gerarchia di Configuration Manager. Specificare il sito di amministrazione centrale durante l'installazione.  

- **Nome chiave:** CASRetryInterval  

    - **Richiesto:** No  

    - **Valori:**  <*Intervallo in minuti*>  

    - **Dettagli:** specifica l'intervallo in minuti tra i tentativi di connessione al sito di amministrazione centrale dopo l'errore di connessione. Se ad esempio si verifica un errore di connessione al sito di amministrazione centrale, il sito primario attende il numero di minuti specificato dall'utente per il valore **CASRetryInterval** e quindi tenta nuovamente di eseguire la connessione.  

- **Nome chiave:** WaitForCASTimeout  

    - **Richiesto:** No  

    - **Valori:**  <*Timeout in minuti da 0 a 100*>  

    - **Dettagli:** specifica il valore di timeout massimo in minuti per la connessione di un sito primario al sito di amministrazione centrale. Se ad esempio un sito primario non riesce a connettersi al sito di amministrazione centrale, tale sito primario proverà nuovamente a connettersi al sito di amministrazione centrale in base al valore **CASRetryInterval** finché non viene raggiunto il periodo di **WaitForCASTimeout**. È possibile specificare un valore compreso tra `0` e `100`.  

#### <a name="cloudconnectoroptions"></a>CloudConnectorOptions

- **Nome chiave:** CloudConnector  

    - **Richiesto:** Sì  

    - **Valori:**

        - `0` = Non installare  

        - `1` = Installare  

    - **Dettagli:** specifica se installare un punto di connessione del servizio in questo sito. Poiché il punto di connessione del servizio può essere installato solo nel sito di livello superiore di una gerarchia, impostare questo valore su `0` per un sito primario figlio.  

- **Nome chiave:** CloudConnectorServer  

    - **Richiesto:** obbligatorio quando **CloudConnector** è uguale a 1  

    - **Valori:**  <*FQDN del server del punto di connessione del servizio*\>  

    - **Dettagli:** specifica il nome FQDN del server che ospiterà il ruolo del sistema del sito del punto di connessione del servizio.  

- **Nome chiave:** UseProxy  

    - **Richiesto:** obbligatorio quando **CloudConnector** è uguale a 1  

    - **Valori:**

        - `0` = Non installare  

        - `1` = Installare  

    - **Dettagli:** specifica se il punto di connessione del servizio usa un server proxy.  

- **Nome chiave:** ProxyName  

    - **Richiesto:** obbligatorio quando **UseProxy** è uguale a 1  

    - **Valori:**  <*FQDN del server proxy*>  

    - **Dettagli:** specifica il nome FQDN del server proxy usato dal punto di connessione del servizio.  

- **Nome chiave:** ProxyPort  

    - **Richiesto:** obbligatorio quando **UseProxy** è uguale a 1  

    - **Valori:**  <*Numero della porta*>  

    - **Dettagli:** specifica il numero della porta da usare per la porta del proxy.  

#### <a name="sabranchoptions"></a>SABranchOptions

<!-- SCCMDocs#390 -->

- **Nome chiave:** SAActive

    - **Richiesto:** No

    - **Valori:**

        - `0` = Non si ha Software Assurance

        - `1` = Software Assurance è attivo

    - **Dettagli:** specifica se si ha Software Assurance attivo. Per altre informazioni, vedere [Domande frequenti su prodotto e licenze](../../../understand/product-and-licensing-faq.md).

- **Nome chiave:** CurrentBranch

    - **Richiesto:** No

    - **Valori:**

        - `0` = Installa LTSB

        - `1` = Installa Current Branch

    - **Dettagli:** specifica se usare Configuration Manager (Current Branch) o Configuration Manager (Long-Term Servicing Branch, LTSB). Per altre informazioni, vedere [Scelta del ramo di Configuration Manager da usare](../../../understand/which-branch-should-i-use.md).

### <a name="unattended-recovery-for-a-cas"></a>Ripristinare automaticamente un sito di amministrazione centrale

Usare i dettagli seguenti per ripristinare un sito di amministrazione centrale usando un file script di installazione automatica.  

#### <a name="identification"></a>Identification

- **Nome chiave:** Action  

    - **Richiesto:** Sì  

    - **Valori:** `RecoverCCAR`  

    - **Dettagli:** consente di ripristinare un sito di amministrazione centrale.  

- **Nome chiave:** CDLatest  

    - **Richiesto:** sì, solo quando si usano supporti dalla cartella CD.Latest.

    - **Valori:**

        - `1` = si usano supporti dalla cartella CD.Latest

        - Qualsiasi valore diverso da 1 indica che non si usano supporti dalla cartella CD.Latest

    - **Dettagli:** Quando si installa o si ripristina un sito primario o un sito di amministrazione centrale e si esegue il programma di installazione dalla cartella CD.Latest, includere questa chiave e il valore. Questo valore indica al programma di installazione che si usano supporti dalla cartella CD.Latest.

#### <a name="recoveryoptions"></a>RecoveryOptions

- **Nome chiave:** ServerRecoveryOptions  

    - **Richiesto:** Sì  

    - **Valori:**

        - `1` = Ripristina il server del sito e SQL Server

        - `2` = Ripristina solo il server del sito

        - `4` = Ripristina solo SQL Server  

    - **Dettagli:** specifica se il programma di installazione ripristina il server del sito, SQL Server o entrambi. Sono inoltre necessarie le seguenti opzioni in base al valore specificato:  

        - **1** o **2**: specificare un valore per **SiteServerBackupLocation** per ripristinare il sito usando un backup del sito. Se non si specifica un valore, il sito viene reinstallato senza eseguire il ripristino da un set di backup.  

        - **4**: La chiave **BackupLocation** è richiesta in caso di configurazione del valore **10** per la chiave **DatabaseRecoveryOptions** necessaria per il ripristino del database del sito dal backup.  

- **Nome chiave:** DatabaseRecoveryOptions  

    - **Richiesto:** Questa chiave è richiesta quando l'impostazione **ServerRecoveryOptions** ha il valore **1** o **4**.  

    - **Valori:**

        - `10` = Ripristina il database del sito dal backup.  

        - `20` = Usa un database del sito che è stato ripristinato manualmente usando un altro metodo.  

        - `40` = Crea un nuovo database per il sito. Usare questa opzione quando non è disponibile alcun backup di database del sito. I dati globali e i dati del sito vengono ripristinati tramite la replica da altri siti.  

        - `80` = Ignora il ripristino del database.  

    - **Dettagli:** specifica le modalità secondo cui il programma di installazione ripristinerà il database del sito in SQL Server.  

- **Nome chiave:** ReferenceSite  

    - **Richiesto:** Questa chiave è richiesta quando l'impostazione **DatabaseRecoveryOptions** ha il valore **40**.  

    - **Valori:**  <*FQDN del sito di riferimento*>  

    - **Dettagli:** specifica il sito primario di riferimento usato dal sito di amministrazione centrale per il ripristino dei dati globali se il backup del database è antecedente al periodo di memorizzazione del rilevamento delle modifiche o se il sito viene ripristinato senza backup.  

        Se non viene specificato un sito di riferimento e il backup è antecedente al periodo di memorizzazione del rilevamento delle modifiche, tutti i siti primari vengono reinizializzati con i dati ripristinati dal sito di amministrazione centrale.  

        Se non viene specificato un sito di riferimento e il backup rientra nel periodo di memorizzazione del rilevamento delle modifiche, solo le modifiche apportate dal momento del backup verranno replicate dai siti primari. In caso di modifiche in conflitto provenienti da diversi siti primari, il sito di amministrazione centrale usa la prima modifica ricevuta.  

- **Nome chiave:** SiteServerBackupLocation  

    - **Richiesto:** No  

    - **Valori:**  <*Percorso del set di backup del server del sito*>  

    - **Dettagli:** Specifica il percorso per il set di backup del server del sito. Questa chiave è facoltativa quando l'impostazione **ServerRecoveryOptions** ha il valore **1** o **2**. Specificare un valore affinché la chiave **SiteServerBackupLocation** ripristini il sito usando un backup del sito. Se non si specifica un valore, il sito viene reinstallato senza eseguire il ripristino da un set di backup.  

- **Nome chiave:** BackupLocation  

    - **Richiesto:** questa chiave è richiesta quando si configura il valore **1** o **4** per la chiave **ServerRecoveryOptions** e si configura il valore **10** per la chiave **DatabaseRecoveryOptions**.  

    - **Valori:**  <*Percorso del set di backup del database del sito*>  

    - **Dettagli:** Specifica il percorso del set di backup del database del sito.  

#### <a name="options"></a>Options

- **Nome chiave:** ProductID  

    - **Richiesto:** Sì  

    - **Valori:**

        - `<xxxxx-xxxxx-xxxxx-xxxxx-xxxxx>` = un codice Product Key valido con trattini

        - `Eval` = installa la versione di valutazione di Configuration Manager

    - **Dettagli:** specifica il codice Product Key per l'installazione di Configuration Manager, trattini inclusi.

- **Nome chiave:** SiteCode  

    - **Richiesto:** Sì  

    - **Valori:**  <*Codice del sito*>  

    - **Dettagli:** Specifica i tre caratteri alfanumerici che identificano in modo univoco il sito nella gerarchia. Specificare il codice del sito usato dal sito prima dell'errore.

- **Nome chiave:** SiteName  

    - **Richiesto:** No  

    - **Valori:**  <*Nome del sito*>  

    - **Dettagli:** Specifica il nome del sito.  

- **Nome chiave:** SMSInstallDir  

    - **Richiesto:** Sì  

    - **Valori:**  <*Percorso di installazione di Configuration Manager*>  

    - **Dettagli:** specifica la cartella di installazione per i file di programma di Configuration Manager.  

- **Nome chiave:** SDKServer  

    - **Richiesto:** Sì  

    - **Valori:**  <*FQDN del provider SMS*>  

    - **Dettagli:** specifica l'FQDN del server che ospita il provider SMS. Specificare il server che ospitava il provider SMS prima dell'errore.  

        Dopo l'installazione iniziale, è possibile configurare altri provider SMS per il sito. Per altre informazioni sul provider SMS, vedere [Pianificare per il provider SMS](../../../plan-design/hierarchy/plan-for-the-sms-provider.md).  

- **Nome chiave:** PrerequisiteComp  

    - **Richiesto:** Sì  

    - **Valori:**

        - `0` = Scaricare  

        - `1` = Già scaricato  

    - **Dettagli:** specifica se i file dei prerequisiti di installazione sono già stati scaricati. Se ad esempio si usa un valore pari a **0**, il programma di installazione esegue il download dei file.  

- **Nome chiave:** PrerequisitePath  

    - **Richiesto:** Sì  

    - **Valori:**  <*Percorso dei file dei prerequisiti di installazione*>  

    - **Dettagli:** specifica il percorso dei file dei prerequisiti di installazione. A seconda del valore di **PrerequisiteComp**, il programma di installazione usa questo percorso per archiviare i file scaricati oppure per individuare file scaricati in precedenza.  

- **Nome chiave:** AdminConsole  

    - **Richiesto:** Questa chiave è necessaria tranne quando l'impostazione **ServerRecoveryOptions** ha valore **4**.  

    - **Valori:**

        - `0` = Non installare  

        - `1` = Installare  

    - **Dettagli:** Specifica se installare la console di Configuration Manager.  

- **Nome chiave:** JoinCEIP  

    > [!Note]  
    > A partire da Configuration Manager versione 1802 la funzionalità Analisi utilizzo software è stata rimossa dal prodotto.

    - **Richiesto:** Sì  

    - **Valori:**

        - `0` = Non partecipare  

        - `1` = Partecipare  

    - **Dettagli:** specifica se partecipare al programma Analisi utilizzo software.  

#### <a name="sqlconfigoptions"></a>SQLConfigOptions

- **Nome chiave:** SQLServerName  

    - **Richiesto:** Sì  

    - **Valori:**  <*Nome dell'istanza di SQL Server*>  

    - **Dettagli:** specifica il nome del server o il nome dell'istanza in cluster che esegue SQL Server e che ospita il database del sito. Specificare lo stesso server in cui era ospitato il database del sito prima dell'errore.  

- **Nome chiave:** DatabaseName  

    - **Richiesto:** Sì  

    - **Valori:**  <*Nome del database del sito*> oppure <*Nome dell'istanza*>\\<*Nome del database del sito*>  

    - **Dettagli:** specifica il nome del database di SQL Server da creare o del database di SQL Server da usare per l'installazione del database del sito di amministrazione centrale. Specificare lo stesso nome database usato prima dell'errore.  

        > [!IMPORTANT]  
        > Se non si usa l'istanza predefinita, specificare il nome dell'istanza e il nome del database del sito.  

- **Nome chiave:** SQLSSBPort  

    - **Richiesto:** Sì  

    - **Valori:**  <*Numero della porta SSB*>  

    - **Dettagli:** specifica la porta SSB usata da SQL Server. Per impostazione predefinita, SSB usa la porta TCP 4022. Specificare la stessa porta SSB usata prima dell'errore.  

- **Nome chiave:** SQLDataFilePath  

    - **Richiesto:** No  

    - **Valori:**  <*Percorso del file mdb del database*>  

    - **Dettagli:** specifica un percorso alternativo per creare il file mdb del database.  

- **Nome chiave:** SQLLogFilePath  

    - **Richiesto:** No  

    - **Valori:**  <*Percorso del file ldf del database*>  

    - **Dettagli:** specifica un percorso alternativo per creare il file ldf del database.  

#### <a name="cloudconnectoroptions"></a>CloudConnectorOptions

- **Nome chiave:** CloudConnector  

    - **Richiesto:** Sì  

    - **Valori:**

        - `0` = Non installare  

        - `1` = Installare  

    - **Dettagli:** specifica se installare un punto di connessione del servizio in questo sito. Poiché il punto di connessione del servizio può essere installato solo nel sito di livello superiore di una gerarchia, impostare questo valore su **0** per un sito primario figlio.  

- **Nome chiave:** CloudConnectorServer  

    - **Richiesto:** obbligatorio quando **CloudConnector** è uguale a 1  

    - **Valori:**  <*FQDN del server del punto di connessione del servizio*>  

    - **Dettagli:** specifica il nome FQDN del server che ospiterà il ruolo del sistema del sito del punto di connessione del servizio.  

- **Nome chiave:** UseProxy  

    - **Richiesto:** obbligatorio quando **CloudConnector** è uguale a 1  

    - **Valori:**

        - `0` = Non installare  

        - `1` = Installare  

    - **Dettagli:** specifica se il punto di connessione del servizio usa un server proxy.  

- **Nome chiave:** ProxyName  

    - **Richiesto:** obbligatorio quando **CloudConnector** è uguale a 1  

    - **Valori:**  <*FQDN del server proxy*>  

    - **Dettagli:** specifica il nome FQDN del server proxy usato dal punto di connessione del servizio.  

- **Nome chiave:** ProxyPort  

    - **Richiesto:** obbligatorio quando **CloudConnector** è uguale a 1  

    - **Valori:**  <*Numero della porta*>  

    - **Dettagli:** specifica il numero della porta da usare per la porta del proxy.  

### <a name="unattended-recovery-for-a-primary-site"></a>Ripristinare automaticamente un sito primario

Usare i dettagli seguenti per recuperare un sito primario usando un file script di installazione automatica.  

#### <a name="identification"></a>Identification

- **Nome chiave:** Action  

    - **Richiesto:** Sì  

    - **Valori:** `RecoverPrimarySite`  

    - **Dettagli:** Ripristina un sito primario.  

- **Nome chiave:** CDLatest  

    - **Richiesto:** sì, solo quando si usano supporti dalla cartella CD.Latest.

    - **Valori:**

        - `1` = si usano supporti dalla cartella CD.Latest

        - Qualsiasi valore diverso da 1 indica che non si usano supporti dalla cartella CD.Latest

    - **Dettagli:** Quando si installa o si ripristina un sito primario o un sito di amministrazione centrale e si esegue il programma di installazione dalla cartella CD.Latest, includere questa chiave e il valore. Questo valore indica al programma di installazione che si usano supporti dalla cartella CD.Latest.

#### <a name="recoveryoptions"></a>RecoveryOptions

- **Nome chiave:** ServerRecoveryOptions  

    - **Richiesto:** Sì  

    - **Valori:**

        - `1` = Ripristina il server del sito e SQL Server

        - `2` = Ripristina solo il server del sito

        - `4` = Ripristina solo SQL Server  

    - **Dettagli:** specifica se il programma di installazione ripristina il server del sito, SQL Server o entrambi. Sono inoltre necessarie le seguenti opzioni in base al valore specificato:  

        - **1** o **2**: specificare un valore per **SiteServerBackupLocation** per ripristinare il sito usando un backup del sito. Se non si specifica un valore, il sito viene reinstallato senza eseguire il ripristino da un set di backup.  

        - **4**: La chiave **BackupLocation** è richiesta in caso di configurazione del valore **10** per la chiave **DatabaseRecoveryOptions** necessaria per il ripristino del database del sito dal backup.  

- **Nome chiave:** DatabaseRecoveryOptions  

    - **Richiesto:** Questa chiave è richiesta quando l'impostazione **ServerRecoveryOptions** ha il valore **1** o **4**.  

    - **Valori:**

        - `10` = Ripristina il database del sito dal backup.  

        - `20` = Usa un database del sito che è stato ripristinato manualmente usando un altro metodo.  

        - `40` = Crea un nuovo database per il sito. Usare questa opzione quando non è disponibile alcun backup di database del sito. I dati globali e i dati del sito vengono ripristinati tramite la replica da altri siti.  

        - `80` = Ignora il ripristino del database.  

    - **Dettagli:** specifica le modalità secondo cui il programma di installazione ripristinerà il database del sito in SQL Server.  

- **Nome chiave:** SiteServerBackupLocation  

    - **Richiesto:** No  

    - **Valori:**  <*Percorso del set di backup del server del sito*>  

    - **Dettagli:** Specifica il percorso per il set di backup del server del sito. Questa chiave è facoltativa quando l'impostazione **ServerRecoveryOptions** ha il valore **1** o **2**. Specificare un valore affinché la chiave **SiteServerBackupLocation** ripristini il sito usando un backup del sito. Se non si specifica un valore, il sito viene reinstallato senza eseguire il ripristino da un set di backup.  

- **Nome chiave:** BackupLocation  

    - **Richiesto:** la chiave è richiesta quando si configura il valore **1** o **4** per la chiave **ServerRecoveryOptions** e il valore **10** per la chiave **DatabaseRecoveryOptions**.  

    - **Valori:**  <*Percorso del set di backup del database del sito*>  

    - **Dettagli:** Specifica il percorso del set di backup del database del sito.  

#### <a name="options"></a>Options

- **Nome chiave:** ProductID  

    - **Richiesto:** Sì  

    - **Valori:**

        - `<xxxxx-xxxxx-xxxxx-xxxxx-xxxxx>` = un codice Product Key valido con trattini

        - `Eval` = installa la versione di valutazione di Configuration Manager

    - **Dettagli:** specifica il codice Product Key per l'installazione di Configuration Manager, trattini inclusi.

- **Nome chiave:** SiteCode  

    - **Richiesto:** Sì  

    - **Valori:**  <*Codice del sito*>  

    - **Dettagli:** Specifica i tre caratteri alfanumerici che identificano in modo univoco il sito nella gerarchia. Specificare il codice del sito usato dal sito prima dell'errore.

- **Nome chiave:** SiteName  

    - **Richiesto:** No  

    - **Valori:**  <*Nome del sito*>  

    - **Dettagli:** Specifica il nome del sito.  

- **Nome chiave:** SMSInstallDir  

    - **Richiesto:** Sì  

    - **Valori:**  <*Percorso di installazione di Configuration Manager*>  

    - **Dettagli:** specifica la cartella di installazione per i file di programma di Configuration Manager.  

- **Nome chiave:** SDKServer  

    - **Richiesto:** Sì  

    - **Valori:**  <*FQDN del provider SMS*>  

    - **Dettagli:** specifica l'FQDN del server che ospita il provider SMS. Specificare il server che ospitava il provider SMS prima dell'errore. Dopo l'installazione iniziale, è possibile configurare altri provider SMS per il sito. Per altre informazioni sul provider SMS, vedere [Pianificare per il provider SMS](../../../plan-design/hierarchy/plan-for-the-sms-provider.md).  

- **Nome chiave:** PrerequisiteComp  

    - **Richiesto:** Sì  

    - **Valori:**

        - `0` = Scaricare  

        - `1` = Già scaricato  

    - **Dettagli:** specifica se i file dei prerequisiti di installazione sono già stati scaricati. Se ad esempio si usa un valore pari a **0**, il programma di installazione esegue il download dei file.  

- **Nome chiave:** PrerequisitePath  

    - **Richiesto:** Sì  

    - **Valori:**  <*Percorso dei file dei prerequisiti di installazione*>  

    - **Dettagli:** specifica il percorso dei file dei prerequisiti di installazione. A seconda del valore di **PrerequisiteComp**, il programma di installazione usa questo percorso per archiviare i file scaricati oppure per individuare file scaricati in precedenza.  

- **Nome chiave:** AdminConsole  

    - **Richiesto:** Questa chiave è necessaria tranne quando l'impostazione **ServerRecoveryOptions** ha valore **4**.  

    - **Valori:**

        - `0` = Non installare  

        - `1` = Installare  

    - **Dettagli:** Specifica se installare la console di Configuration Manager.  

- **Nome chiave:** JoinCEIP  

    > [!Note]  
    > A partire da Configuration Manager versione 1802 la funzionalità Analisi utilizzo software è stata rimossa dal prodotto.

    - **Richiesto:** Sì  

    - **Valori:**

        - `0` = Non partecipare  

        - `1` = Partecipare  

    - **Dettagli:** specifica se partecipare al programma Analisi utilizzo software.  

#### <a name="sqlconfigoptions"></a>SQLConfigOptions

- **Nome chiave:** SQLServerName  

    - **Richiesto:** Sì  

    - **Valori:**  <*Nome dell'istanza di SQL Server*>  

    - **Dettagli:** specifica il nome del server o il nome dell'istanza in cluster che esegue SQL Server per ospitare il database del sito. Specificare lo stesso server in cui era ospitato il database del sito prima dell'errore.  

- **Nome chiave:** DatabaseName  

    - **Richiesto:** Sì  

    - **Valori:**  <*Nome del database del sito*> oppure <*Nome dell'istanza*>\\<*Nome del database del sito*>

    - **Dettagli:** specifica il nome del database di SQL Server da creare o del database di SQL Server da usare per l'installazione del database del sito di amministrazione centrale. Specificare lo stesso nome database usato prima dell'errore.  

        > [!IMPORTANT]  
        > Se non si usa l'istanza predefinita, specificare il nome dell'istanza e il nome del database del sito.  

- **Nome chiave:** SQLSSBPort  

    - **Richiesto:** Sì  

    - **Valori:**  <*Numero della porta SSB*>  

    - **Dettagli:** specifica la porta SSB usata da SQL Server. Per impostazione predefinita, SSB usa la porta TCP 4022. Specificare la stessa porta SSB usata prima dell'errore.  

- **Nome chiave:** SQLDataFilePath  

    - **Richiesto:** No  

    - **Valori:**  <*Percorso del file mdb del database*>  

    - **Dettagli:** specifica un percorso alternativo per creare il file mdb del database.  

- **Nome chiave:** SQLLogFilePath  

    - **Richiesto:** No  

    - **Valori:**  <*Percorso del file ldf del database*>  

    - **Dettagli:** specifica un percorso alternativo per creare il file ldf del database.  

#### <a name="hierarchyexpansionoptions"></a>HierarchyExpansionOptions

- **Nome chiave:** CCARSiteServer  

    - **Richiesto:** Visualizzare i dettagli.  

    - **Valori:**  <*Codice del sito per il sito di amministrazione centrale*>  

    - **Dettagli:** specifica il sito di amministrazione centrale a cui si collega il sito primario quando viene aggiunto alla gerarchia di Configuration Manager. Questa impostazione è necessaria se il sito primario era collegato a un sito di amministrazione centrale prima dell'errore. Specificare il codice del sito usato per il sito di amministrazione centrale prima dell'errore.  

- **Nome chiave:** CASRetryInterval  

    - **Richiesto:** No  

    - **Valori:**  <*Intervallo in minuti*>  

    - **Dettagli:** specifica l'intervallo in minuti tra i tentativi di connessione al sito di amministrazione centrale dopo l'errore di connessione. Se ad esempio si verifica un errore di connessione al sito di amministrazione centrale, il sito primario attende il numero di minuti specificato dall'utente per il valore **CASRetryInterval** e quindi tenta nuovamente di eseguire la connessione.  

- **Nome chiave:** WaitForCASTimeout  

    - **Richiesto:** No  

    - **Valori:**  <*Timeout in minuti*>  

    - **Dettagli:** specifica il valore di timeout massimo in minuti per la connessione di un sito primario al sito di amministrazione centrale. Se ad esempio un sito primario non riesce a connettersi al sito di amministrazione centrale, tale sito primario proverà nuovamente a connettersi al sito di amministrazione centrale in base al valore **CASRetryInterval** finché non viene raggiunto il periodo di **WaitForCASTimeout**. È possibile specificare un valore compreso tra `0` e `100`.  

#### <a name="cloudconnectoroptions"></a>CloudConnectorOptions

- **Nome chiave:** CloudConnector  

    - **Richiesto:** Sì  

    - **Valori:**

        - `0` = Non installare  

        - `1` = Installare  

    - **Dettagli:** specifica se installare un punto di connessione del servizio in questo sito. Poiché il punto di connessione del servizio può essere installato solo nel sito di livello superiore di una gerarchia, impostare questo valore su `0` per un sito primario figlio.  

- **Nome chiave:** CloudConnectorServer  

    - **Richiesto:** obbligatorio quando **CloudConnector** è uguale a 1  

    - **Valori:**  <*FQDN del server del punto di connessione del servizio*>  

    - **Dettagli:** specifica il nome FQDN del server che ospiterà il ruolo del sistema del sito del punto di connessione del servizio.  

- **Nome chiave:** UseProxy  

    - **Richiesto:** obbligatorio quando **CloudConnector** è uguale a 1  

    - **Valori:**

        - `0` = Non installare  

        - `1` = Installare  

    - **Dettagli:** specifica se il punto di connessione del servizio usa un server proxy.  

- **Nome chiave:** ProxyName  

    - **Richiesto:** obbligatorio quando **CloudConnector** è uguale a 1  

    - **Valori:**  <*FQDN del server proxy*>  

    - **Dettagli:** specifica il nome FQDN del server proxy usato dal punto di connessione del servizio.  

- **Nome chiave:** ProxyPort  

    - **Richiesto:** obbligatorio quando **CloudConnector** è uguale a 1  

    - **Valori:**  <*Numero della porta*>  

    - **Dettagli:** specifica il numero della porta da usare per la porta del proxy.  
