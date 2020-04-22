---
title: Ripristino automatico
titleSuffix: Configuration Manager
description: Usare uno script per ripristinare i siti in Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 828c31d1-3d70-4412-b1a8-c92e7e504d39
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a12de673776817330a80cb68588faf225922e241
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704399"
---
# <a name="unattended-site-recovery-for-configuration-manager"></a>Ripristino automatico del sito per Configuration Manager   

*Si applica a: Configuration Manager (Current Branch)*

 Per eseguire il [ripristino automatico](recover-sites.md#site-recovery-procedures) di un sito di amministrazione centrale o di un sito primario di Configuration Manager, è possibile creare uno script di installazione automatica e quindi usare il programma di installazione con l'opzione di comando **/script**. Lo script specifica lo stesso tipo di informazioni richieste dall'installazione guidata, ma non prevede impostazioni predefinite. Per le chiavi di installazione applicabili al tipo di ripristino che si usa, è necessario specificare tutti i valori.

 Per usare l'opzione di comando /script del programma di installazione è necessario creare un file di inizializzazione. Specificare quindi il nome del file dopo l'opzione /script. Il nome del file non è rilevante, purché l'estensione del nome file sia **INI**. Quando si fa riferimento a file di inizializzazione dell'installazione dalla riga di comando, è necessario specificare il percorso completo del file. Se ad esempio il file di inizializzazione dell'installazione è denominato *setup.ini* e viene archiviato nella cartella *C:\setup*, la riga di comando sarà:

 `setup /script c:\setup\setup.ini`

> [!IMPORTANT]  
>  Per eseguire il programma di installazione è necessario avere i diritti di amministratore. Quando il programma di installazione viene eseguito con lo script automatico, è necessario avviare il prompt dei comandi in un contesto di amministrazione usando **Esegui come amministratore**.

 Lo script contiene nomi di sezione, nomi delle chiavi e valori. I nomi delle chiavi di sezione richiesti variano a seconda del tipo di ripristino per cui si crea lo script. L'ordine delle chiavi all'interno delle sezioni e l'ordine delle sezioni all'interno del file non è rilevante. Alle chiavi non viene applicata la distinzione tra maiuscole e minuscole. Quando si specificano i valori per le chiavi, il nome della chiave deve essere seguito dal segno uguale (=) e dal valore della chiave.

 Usare le seguenti sezioni per creare lo script per il ripristino automatico del sito. Nelle tabelle sono elencate le chiavi dello script di installazione, i relativi valori, se richiesti, il tipo di installazione per cui vengono usate e una breve descrizione relativa alla chiave.

## <a name="recover-a-central-administration-site-unattended"></a>Ripristinare un sito di amministrazione centrale in modo automatico
 Usare le informazioni seguenti per configurare un file di script di installazione automatica per il ripristino di un sito di amministrazione centrale.

 **Identification**

-   **Nome chiave:** Action

    -   **Richiesto:** Sì
    -   **Valori:** RecoverCCAR
    -   **Dettagli:** ripristina un sito di amministrazione centrale


-   **Nome chiave:** CDLatest

    -   **Richiesto:** sì, solo quando si usano supporti dalla cartella CD.Latest.
    -   **Valori:** 1. Qualsiasi valore diverso da 1 presuppone che non venga usata la cartella CD.Latest.
    -   **Dettagli:** lo script deve includere la chiave e il valore quando si esegue il programma di installazione dal supporto di una cartella CD.Latest allo scopo di installare o ripristinare un sito di amministrazione centrale o primario. Questo valore indica al programma di installazione che viene usato il formato di supporto CD.Latest.

**RecoveryOptions**   
-   **Nome chiave:** ServerRecoveryOptions   

    -   **Richiesto:** Sì
    -   **Valori:** 1, 2 o 4  
         1 = Ripristina il server del sito e SQL Server.   
         2 = Ripristina solo il server del sito.  
         4 = Ripristina solo SQL Server.
    -   **Dettagli:** specifica se il programma di installazione ripristina il server del sito, SQL Server o entrambi. Le chiavi associate sono necessarie quando si imposta il valore seguente per l'impostazione ServerRecoveryOptions:  
        -   **Valore = 1** È possibile specificare un valore per la chiave **SiteServerBackupLocation** per il ripristino del sito usando un backup del sito. Se non si specifica un valore, il sito viene reinstallato senza eseguire il ripristino da un set di backup.

             La chiave **BackupLocation** è richiesta in caso di configurazione del valore **10** per la chiave **DatabaseRecoveryOptions** necessaria per il ripristino del database del sito dal backup.

        -   **Valore = 2** È possibile specificare un valore per la chiave **SiteServerBackupLocation** per il ripristino del sito usando un backup del sito. Se non si specifica un valore, il sito viene reinstallato senza eseguire il ripristino da un set di backup.

        -   **Valore = 4** La chiave **BackupLocation** è richiesta in caso di configurazione del valore **10** per la chiave **DatabaseRecoveryOptions** necessaria per il ripristino del database del sito dal backup.

-   **Nome chiave:** DatabaseRecoveryOptions

    -   **Richiesto:** Forse
    -   **Valori:**   
         - **10** = ripristina il database del sito dal backup.  
         - **20** = usa un database del sito che è stato ripristinato manualmente usando un altro metodo.   
         - **40** = crea un nuovo database per il sito. Usare questa opzione quando non è disponibile alcun backup di database del sito. I dati globali e i dati del sito vengono ripristinati tramite la replica da altri siti.  
         - **80** = ignora il ripristino del database.
    -   **Dettagli:** specifica le modalità secondo cui il programma di installazione ripristinerà il database del sito in SQL Server. Questa chiave è richiesta quando l'impostazione **ServerRecoveryOptions** ha il valore **1** o **4**.


-   **Nome chiave:** ReferenceSite  

    -   **Richiesto:** Forse
    -   **Valori:** &lt;FQDNSitoRiferimento\>
    -   **Dettagli:** specifica il sito primario di riferimento. Se il backup del database è antecedente al periodo di memorizzazione del rilevamento delle modifiche o se il sito viene ripristinato senza backup, il sito di amministrazione centrale usa il sito di riferimento per il ripristino dei dati globali.

         Se non viene specificato un sito di riferimento e il backup è antecedente al periodo di memorizzazione del rilevamento delle modifiche, tutti i siti primari vengono reinizializzati con i dati ripristinati dal sito di amministrazione centrale.

         Se non viene specificato un sito di riferimento e il backup rientra nel periodo di memorizzazione del rilevamento delle modifiche, solo le modifiche apportate dal momento del backup verranno replicate dai siti primari. In caso di modifiche in conflitto provenienti da diversi siti primari, il sito di amministrazione centrale usa la prima modifica ricevuta.

         Questa chiave è richiesta quando l'impostazione **DatabaseRecoveryOptions** ha il valore **40**.

-   **Nome chiave:** SiteServerBackupLocation

    -   **Richiesto:** No
    -   **Valori:** &lt;PercorsoSetBackupServerSito\>
    -   **Dettagli:** Specifica il percorso per il set di backup del server del sito. Questa chiave è facoltativa quando l'impostazione **ServerRecoveryOptions** ha il valore **1** o **2**. Specificare un valore affinché la chiave **SiteServerBackupLocation** ripristini il sito usando un backup del sito. Se non si specifica un valore, il sito viene reinstallato senza eseguire il ripristino da un set di backup.


-   **Nome chiave:** BackupLocation

    -   **Richiesto:** Forse
    -   **Valori:** &lt;PercorsoSetBackupDatabaseSito\>
    -   **Dettagli:** Specifica il percorso del set di backup del database del sito. La chiave **BackupLocation** è richiesta quando viene configurato il valore **1** o **4** per la chiave **ServerRecoveryOptions** e viene configurato il valore **10** per la chiave **DatabaseRecoveryOptions** .


**Opzioni**

- **Nome chiave:** ProductID
  -   **Richiesto:** Sì
  -   **Valori:**   
       - xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  
       - valutazione
  -   **Dettagli:** codice Product Key per l'installazione di Configuration Manager, trattini inclusi. Immettere **Eval** per installare la versione di valutazione di Configuration Manager.  


- **Nome chiave:** SiteCode

  -   **Richiesto:** Sì
  -   **Valori:** &lt;Codice del sito\>
  -   **Dettagli:** tre caratteri alfanumerici che identificano in modo univoco il sito nella gerarchia. Specificare il codice del sito usato dal sito prima dell'errore.


- **Nome chiave:** SiteName

  -   **Richiesto:** Sì
  -   **Valori:** SiteName
  -   **Dettagli:** Descrizione per questo sito.


- **Nome chiave:** SMSInstallDir

  - **Richiesto:** Sì
  - **Valori:** &lt;*PercorsoInstallazioneConfigMgr*>
  - **Dettagli:** specifica la cartella di installazione per i file di programma di Configuration Manager.
    > [!NOTE]   
    >  È possibile specificare il percorso originale o uno nuovo da usare per l'installazione di Configuration Manager.

- **Nome chiave:** SDKServer

  -   **Richiesto:** Sì
  -   **Valori:** &lt;*FQDN del provider SMS*>
  -   **Dettagli:** specifica l'FQDN del server che ospita il provider SMS. Specificare il server che ospitava il provider SMS prima dell'errore.

       Dopo l'installazione iniziale, è possibile configurare altri provider SMS per il sito.

- **Nome chiave:** PrerequisiteComp

  -   **Richiesto:** Sì
  -   **Valori:** 0 o 1  
       0 = scarica   
       1 = già scaricato
  -   **Dettagli:** specifica se i file dei prerequisiti di installazione sono già stati scaricati. Se ad esempio si usa il valore 0, il programma di installazione esegue il download dei file.  


- **Nome chiave:** PrerequisitePath

  -   **Richiesto:** Sì
  -   **Valori:** &lt;*PercorsoFilePrerequisitiInstallazione*>
  -   **Dettagli:** specifica il percorso dei file dei prerequisiti di installazione. A seconda del valore di **PrerequisiteComp**, il programma di installazione usa questo percorso per archiviare i file scaricati oppure per individuare file scaricati in precedenza.

- **Nome chiave:** AdminConsole

  -   **Richiesto:** Forse
  -   **Valori:** 0 o 1 0 = non installare   
       1 = installa
  -   **Dettagli:** Specifica se installare la console di Configuration Manager. Questa chiave è necessaria tranne quando l'impostazione **ServerRecoveryOptions** ha valore **4**.


- **Nome chiave:** JoinCEIP   
  > [!Note]  
  > A partire da Configuration Manager versione 1802 la funzionalità Analisi utilizzo software è stata rimossa dal prodotto.

  -   **Richiesto:** Sì
  -   **Valori:** 0 o 1  
       0 = non partecipare  
       1 = partecipa
  -   **Dettagli:** Specifica se partecipare al programma Analisi utilizzo software.

**SQLConfigOptions**

-   **Nome chiave:** SQLServerName

    -   **Richiesto:** Sì
    -   **Valori:** *&lt;NomeSQLServer\>*
    -   **Dettagli:** nome del server o dell'istanza in cluster che esegue il sistema SQL Server in cui viene ospitato il database del sito. Specificare lo stesso server in cui era ospitato il database del sito prima dell'errore.


-   **Nome chiave:** DatabaseName

    -   **Richiesto:** Sì
    -   **Valori:** *&lt;NomeDatabaseSito\>* o *&lt;NomeIstanza\>* \\ *&lt;NomeDatabaseSito\>*
    -   **Dettagli:** Il nome del database di SQL Server da creare o usare per installare il database del sito di amministrazione centrale. Specificare lo stesso nome database usato prima dell'errore.

        > [!IMPORTANT]  
        >  Se non si usa l'istanza predefinita, è necessario specificare il nome dell'istanza e il nome del database del sito.

-   **Nome chiave:** SQLSSBPort

    -   **Richiesto:** No
    -   **Valori:** &lt;*NumeroPortaSSB*>
    -   **Dettagli:** Specifica la porta di SQL Server Service Broker (SSB) usata da SQL Server. In genere, SSB è configurato per usare la porta TCP 4022, ma sono supportate anche altre porte. Specificare la stessa porta SSB usata prima dell'errore.

## <a name="recover-a-primary-site-unattended"></a>Ripristinare un sito primario automatico
 Usare le informazioni seguenti per configurare un file di script di installazione automatica per il ripristino di un sito di amministrazione centrale.

 **Identification**

-   **Nome chiave:** Action

    -   **Richiesto:** Sì
    -   **Valori:** RecoverPrimarySite
    -   **Dettagli:** Ripristina un sito primario


-   **Nome chiave:** CDLatest

    -   **Richiesto:** sì, solo quando si usano supporti dalla cartella CD.Latest.
    -   **Valori:** 1. Qualsiasi valore diverso da 1 presuppone che non venga usata la cartella CD.Latest.
    -   **Dettagli:** lo script deve includere la chiave e il valore quando si esegue il programma di installazione dal supporto di una cartella CD.Latest allo scopo di installare o ripristinare un sito di amministrazione centrale o primario. Questo valore indica al programma di installazione che viene usato il formato di supporto CD.Latest.

**RecoveryOptions**

-   **Nome chiave:** ServerRecoveryOptions

    -   **Richiesto:** Sì
    -   **Valori:** 1, 2 o 4    
         1 = Ripristina il server del sito e SQL Server.   
         2 = Ripristina solo il server del sito.  
         4 = Ripristina solo SQL Server.
    -   **Dettagli:** specifica se il programma di installazione ripristina il server del sito, SQL Server o entrambi. Le chiavi associate sono necessarie quando si imposta il valore seguente per l'impostazione ServerRecoveryOptions:

        -   **Valore = 1** È possibile specificare un valore per la chiave **SiteServerBackupLocation** per il ripristino del sito usando un backup del sito. Se non si specifica un valore, il sito viene reinstallato senza eseguire il ripristino da un set di backup.

             La chiave **BackupLocation** è richiesta in caso di configurazione del valore **10** per la chiave **DatabaseRecoveryOptions** necessaria per il ripristino del database del sito dal backup.

        -   **Valore = 2** È possibile specificare un valore per la chiave **SiteServerBackupLocation** per il ripristino del sito usando un backup del sito. Se non si specifica un valore, il sito viene reinstallato senza eseguire il ripristino da un set di backup.

        -   **Valore = 4** La chiave **BackupLocation** è richiesta in caso di configurazione del valore **10** per la chiave **DatabaseRecoveryOptions** necessaria per il ripristino del database del sito dal backup.

-   **Nome chiave:** DatabaseRecoveryOptions

    -   **Richiesto:** Forse
    -   **Valori:**   
         - **10** = ripristina il database del sito dal backup.  
         - **20** = usa un database del sito che è stato ripristinato manualmente usando un altro metodo.     
         - **40** = crea un nuovo database per il sito. Usare questa opzione quando non è disponibile alcun backup di database del sito. I dati globali e i dati del sito vengono ripristinati tramite la replica da altri siti.  
         - **80** = ignora il ripristino del database.
    -   **Dettagli:** specifica le modalità secondo cui il programma di installazione ripristinerà il database del sito in SQL Server. Questa chiave è richiesta quando l'impostazione **ServerRecoveryOptions** ha il valore **1** o **4**.


-   **Nome chiave:** SiteServerBackupLocation

    -   **Richiesto:** No
    -   **Valori:** &lt;PercorsoSetBackupServerSito\>
    -   **Dettagli:** Specifica il percorso per il set di backup del server del sito. Questa chiave è facoltativa quando l'impostazione **ServerRecoveryOptions** ha il valore **1** o **2**. Specificare un valore affinché la chiave **SiteServerBackupLocation** ripristini il sito usando un backup del sito. Se non si specifica un valore, il sito viene reinstallato senza eseguire il ripristino da un set di backup.     


-   **Nome chiave:** BackupLocation

    -   **Richiesto:** Forse
    -   **Valori:** &lt;PercorsoSetBackupDatabaseSito\>
    -   **Dettagli:** Specifica il percorso del set di backup del database del sito. La chiave **BackupLocation** è richiesta quando viene configurato il valore **1** o **4** per la chiave **ServerRecoveryOptions** e viene configurato il valore **10** per la chiave **DatabaseRecoveryOptions** .

**Opzioni**

-   **Nome chiave:** ProductID

    -   **Richiesto:** Sì
    -   **Valori:**     
         - xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  
         - valutazione     
    -   **Dettagli:** codice Product Key per l'installazione di Configuration Manager, trattini inclusi. Immettere **Eval** per installare la versione di valutazione di Configuration Manager.  


-   **Nome chiave:** SiteCode

    -   **Richiesto:** Sì
    -   **Valori:** &lt;Codice del sito\>
    -   **Dettagli:** tre caratteri alfanumerici che identificano in modo univoco il sito nella gerarchia. Specificare il codice del sito usato dal sito prima dell'errore.


-   **Nome chiave:** SiteName

    -   **Richiesto:** Sì
    -   **Valori:** SiteName
    -   **Dettagli:** Descrizione per questo sito.


-   **Nome chiave:** SMSInstallDir

    -   **Richiesto:** Sì
    -   **Valori:** &lt;*PercorsoInstallazioneConfigMgr*>
    -   **Dettagli:** specifica la cartella di installazione per i file di programma di Configuration Manager.

        > [!NOTE]   
        >  È possibile specificare il percorso originale o uno nuovo da usare per l'installazione di Configuration Manager.

-   **Nome chiave:** SDKServer

    -   **Richiesto:** Sì
    -   **Valori:** &lt;*FQDN del provider SMS*>
    -   **Dettagli:** specifica l'FQDN del server che ospita il provider SMS. Specificare il server che ospitava il provider SMS prima dell'errore.

         Dopo l'installazione iniziale, è possibile configurare altri provider SMS per il sito.

-   **Nome chiave:** PrerequisiteComp

    -   **Richiesto:** Sì
    -   **Valori:** 0 o 1    
         0 = scarica   
         1 = già scaricato   
    -   **Dettagli:** specifica se i file dei prerequisiti di installazione sono già stati scaricati. Se ad esempio si usa il valore 0, il programma di installazione esegue il download dei file.


-   **Nome chiave:** PrerequisitePath

    -   **Richiesto:** Sì
    -   **Valori:** &lt;*PercorsoFilePrerequisitiInstallazione*>
    -   **Dettagli:** specifica il percorso dei file dei prerequisiti di installazione. A seconda del valore di **PrerequisiteComp**, il programma di installazione usa questo percorso per archiviare i file scaricati oppure per individuare file scaricati in precedenza.


-   **Nome chiave:** AdminConsole

    -   **Richiesto:** Forse
    -   **Valori:** 0 o 1  
         0 = non installare   
         1 = installa  
    -   **Dettagli:** Specifica se installare la console di Configuration Manager. Questa chiave è necessaria tranne quando l'impostazione **ServerRecoveryOptions** ha valore **4**.

-   **Nome chiave:** JoinCEIP  
    > [!Note]  
    > A partire da Configuration Manager versione 1802 la funzionalità Analisi utilizzo software è stata rimossa dal prodotto.

    -   **Richiesto:** Sì
    -   **Valori:** 0 o 1    
         0 = non partecipare  
         1 = partecipa
    -   **Dettagli:** Specifica se partecipare al programma Analisi utilizzo software.


**SQLConfigOptions**

-   **Nome chiave:** SQLServerName

    -   **Richiesto:** Sì
    -   **Valori:** *&lt;NomeSQLServer\>*
    -   **Dettagli:** nome del server o dell'istanza in cluster che esegue il sistema SQL Server in cui viene ospitato il database del sito. Specificare lo stesso server in cui era ospitato il database del sito prima dell'errore.


-   **Nome chiave:** DatabaseName

    -   **Richiesto:** Sì
    -   **Valori:** *&lt;NomeDatabaseSito\>* o *&lt;NomeIstanza\>* \\ *&lt;NomeDatabaseSito\>*
    -   **Dettagli:** Il nome del database di SQL Server da creare o usare per installare il database del sito di amministrazione centrale. Specificare lo stesso nome database usato prima dell'errore.

        > [!IMPORTANT]    
        >  Se non si usa l'istanza predefinita, è necessario specificare il nome dell'istanza e il nome del database del sito.

-   **Nome chiave:** SQLSSBPort

    -   **Richiesto:** No
    -   **Valori:** &lt;*NumeroPortaSSB*>
    -   **Dettagli:** Specifica la porta di SQL Server Service Broker (SSB) usata da SQL Server. In genere, SSB è configurato per usare la porta TCP 4022, ma sono supportate anche altre porte. Specificare la stessa porta SSB usata prima dell'errore.

**Hierarchy ExpansionOption**

-   **Nome chiave:** CCARSiteServer

    -   **Richiesto:** Forse
    -   **Valori:** &lt;*CodiceSitoPerSitoAmministrazioneCentrale*>
    -   **Dettagli:** specifica il sito di amministrazione centrale a cui si collega il sito primario quando viene aggiunto alla gerarchia di Configuration Manager. Questa impostazione è necessaria se il sito primario era collegato a un sito di amministrazione centrale prima dell'errore. Specificare il codice del sito usato dal sito di amministrazione centrale prima dell'errore.

-   **Nome chiave:** CASRetryInterval

    -   **Richiesto:** No
    -   **Valori:** &lt;*Intervallo*>
    -   **Dettagli:** Specifica l'intervallo (in minuti) tra i tentativi di connessione al sito di amministrazione centrale dopo l'errore di connessione. Se ad esempio si verifica un errore di connessione al sito di amministrazione centrale, il sito primario attende il numero di minuti specificato per CASRetryInterval e quindi prova nuovamente a eseguire la connessione.


-   **Nome chiave:** WaitForCASTimeout

    -   **Richiesto:** No
    -   **Valori:** &lt;*Timeout*>
    -   **Dettagli:** Specifica il valore di timeout massimo (in minuti) per la connessione di un sito primario al sito di amministrazione centrale. Se ad esempio un sito primario non riesce a connettersi al sito di amministrazione centrale, tale sito primario proverà nuovamente a connettersi al sito di amministrazione centrale in base a CASRetryInterval finché non viene raggiunto il periodo di WaitForCASTimeout. È possibile specificare un valore compreso tra 0 e 100.
