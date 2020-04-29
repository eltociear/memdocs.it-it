---
title: File di definizione del pacchetto
titleSuffix: Configuration Manager
description: Informazioni sull'uso dei file di definizione del pacchetto per creare pacchetti e programmi in Configuration Manager
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2de963d7-ffb9-43c3-9e1d-fc992b67bebd
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 0d2d0dcad06c18b13b337185ae1feb768a7ee323
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689329"
---
# <a name="package-definition-files"></a>File di definizione del pacchetto

*Si applica a: Configuration Manager (Current Branch)*

I file di definizione del pacchetto sono script che consentono di automatizzare la creazione di [pacchetti e programmi](packages-and-programs.md) in Configuration Manager. Specificano tutte le informazioni necessarie a Configuration Manager per creare un pacchetto e un programma, ad eccezione del percorso dei file origine del pacchetto.

## <a name="about-the-package-definition-file-format"></a>Informazioni sul formato di file definizioni del pacchetto

Ogni file di definizione del pacchetto è un file di testo ASCII o UTF-8 che usa il formato di file con estensione ini. Contiene le sezioni seguenti:  

### <a name="pdf"></a>[PDF]

Questa sezione identifica il file come file di definizione del pacchetto. Contiene le informazioni seguenti:  

- **Versione**: specificare la versione del formato di file di definizione del pacchetto usato dal file. Questa versione corrisponde alla versione di Configuration Manager per cui è stato scritto. Questa voce è necessaria.  

### <a name="package-definition"></a>[Package Definition]

Specificare le proprietà del pacchetto e del programma. Contiene le informazioni seguenti:  

- **Nome**: nome del pacchetto, con un massimo di 50 caratteri.  

- **Versione** (facoltativo): versione del pacchetto, con un massimo di 32 caratteri.  

- **Icona** (facoltativo): file contenente l'icona da usare per il pacchetto. Se specificata, questa icona sostituisce quella del pacchetto predefinita nella console di Configuration Manager.

- **Server di pubblicazione**: server di pubblicazione del pacchetto, con un massimo di 32 caratteri.

- **Lingua**: versione della lingua del pacchetto, con un massimo di 32 caratteri.

- **Commento** (facoltativo): commento sul pacchetto, con un massimo di 127 caratteri.

- **ContainsNoFiles**: questa voce indica se il pacchetto contiene file di origine.  

- **Programmi**: programmi definiti dall'utente per il pacchetto. Ogni nome del programma corrisponde a un **[programma]** sezione in questo file di definizione del pacchetto.  

    Esempio:  

    `Programs=Typical, Custom, Uninstall`  

- **MIFFileName**: nome del file MIF (Management Information) che contiene lo stato del pacchetto, con un massimo di 50 caratteri.  

- **MIFName**: nome del pacchetto (per la corrispondenza MIF), con un massimo di 50 caratteri.  

- **MIFVersion**: numero di versione del pacchetto (per la corrispondenza MIF), con un massimo di 32 caratteri.  

- **MIFPublisher**: autore del software del pacchetto (per la corrispondenza MIF), con un massimo di 32 caratteri.  

### <a name="program"></a>[Program]

Includere una sezione [Program] per ogni programma specificato nella voce **Programs** nella sezione **[Package Definition]** . Questa sezione definisce ogni programma. Ogni sezione Program offre le informazioni seguenti:  

- **Nome**: nome del programma, con un massimo di 50 caratteri. Questa voce deve essere univoca all'interno di un pacchetto.  

- **Icona** (facoltativo): specificare il file contenente l'icona da usare per il programma. Questa icona sostituisce quella predefinita del pacchetto nella console di Configuration Manager. Il client visualizza questa icona anche quando si distribuisce il programma in una raccolta.

- **Commento** (facoltativo): commento sul programma, con un massimo di 127 caratteri.

- **CommandLine**: specificare la riga di comando per il programma, con un massimo di 127 caratteri. Il comando è relativo alla cartella di origine del pacchetto.

- **StartIn**: specificare la cartella di lavoro per il programma, con un massimo di 127 caratteri. Questa voce può essere un percorso assoluto nel computer client o un percorso relativo della cartella di origine del pacchetto.

- **Esegui**: specificare la modalità in cui viene eseguito il programma. È possibile specificare **ridotta a icona**, **ingrandita**, o **Hidden**. Se non si include questa voce, il programma viene eseguito in modalità normale.  

- **AfterRunning**: specificare qualsiasi azione speciale da eseguire dopo che il programma è stato completato correttamente. Le opzioni disponibili sono **SMSRestart**, **ProgramRestart**, o **SMSLogoff**. Se non si include questa voce, il programma non esegue alcuna azione speciale.  

- **EstimatedDiskSpace**: specificare la quantità di spazio su disco necessaria per l'esecuzione del programma software nel computer. Il valore predefinito è **Unknown**. È possibile impostare il valore specificando un numero intero maggiore o uguale a zero. Se si specifica un valore, includere anche le unità per il valore stesso.  

    Esempio:  

    `EstimatedDiskSpace=38MB`  

- **EstimatedRunTime**: specificare la durata stimata in minuti prevista per l'esecuzione del programma nel computer client. Il valore predefinito è **120**. È possibile impostare il valore specificando un numero intero maggiore di zero o indicando **Unknown**.  

    Esempio:  

    `EstimatedRunTime=25`  

- **SupportedClients**: specificare i processori e i sistemi operativi in cui viene eseguito il programma. Separare le piattaforme tramite virgole. Se non si include questa voce, il client non controlla le piattaforme supportate per questo programma.  

- **SupportedClientMinVersionX**, **SupportedClientMaxVersionX**: specificare l'intervallo tra numero di versione iniziale e finale per i sistemi operativi specificati alla voce **SupportedClients**.  

    Esempio:  

    ```INI
    SupportedClients=Win NT (I386),Win NT (IA64),Win NT (x64)  
    Win NT (I386) MinVersion1=5.00.2195.4  
    Win NT (I386) MaxVersion1=5.00.2195.4  
    Win NT (I386) MinVersion2=5.10.2600.2  
    Win NT (I386) MaxVersion2=5.10.2600.2  
    Win NT (I386) MinVersion3=5.20.0000.0  
    Win NT (I386) MaxVersion3=5.20.9999.9999  
    Win NT (I386) MinVersion4=5.20.3790.0  
    Win NT (I386) MaxVersion4=5.20.3790.2  
    Win NT (I386) MinVersion5=6.00.0000.0  
    Win NT (I386) MaxVersion5=6.00.9999.9999  
    Win NT (IA64) MinVersion1=5.20.0000.0  
    Win NT (IA64) MaxVersion1=5.20.9999.9999  
    Win NT (x64) MinVersion1=5.20.0000.0  
    Win NT (x64) MaxVersion1=5.20.9999.9999  
    Win NT (x64) MinVersion2=5.20.3790.0  
    Win NT (x64) MaxVersion2=5.20.9999.9999  
    Win NT (x64) MinVersion3=5.20.3790.0  
    Win NT (x64) MaxVersion3=5.20.3790.2  
    Win NT (x64) MinVersion4=6.00.0000.0  
    Win NT (x64) MaxVersion4=6.00.9999.9999
    ```  

- **AdditionalProgramRequirements** (facoltativo): specificare qualsiasi altro requisito o informazione per i computer client, con un massimo di 127 caratteri.

- **CanRunWhen**: specificare lo stato dell'utente necessario per l'esecuzione del programma nel computer client. I valori disponibili sono **UserLoggedOn**, **NoUserLoggedOn**, o **AnyUserStatus**. Il valore predefinito è **UserLoggedOn**.  

- **UserInputRequired**: specificare se il programma richiede interazione con l'utente. I valori disponibili sono **True** o **False**. Il valore predefinito è **True**. Questa voce è impostata su **False** se **CanRunWhen** non è impostato su **UserLoggedOn**.  

- **AdminRightsRequired**: specificare se per l'esecuzione del programma è necessario immettere credenziali amministrative nel computer. I valori disponibili sono **True** o **False**. Il valore predefinito è **False**. Questa voce è impostata su **True** se **CanRunWhen** non è impostato su **UserLoggedOn**.  

- **UseInstallAccount**: specificare se il programma usa l'account di installazione software client per l'esecuzione nei computer client. Per impostazione predefinita, questo valore è **False**. Questo valore corrisponde anche **False** se **CanRunWhen** è impostato su **UserLoggedOn**.  

- **DriveLetterConnection**: specificare se il programma richiede una connessione con lettera di unità per i file del pacchetto che si trovano nel punto di distribuzione. È possibile specificare **True** o **False**. Il valore predefinito è **False**, che consente al programma di usare una connessione UNC (Universal Naming Convention). Quando questo valore è impostato su **True**, il client usa la lettera di unità successiva disponibile, a partire da Z: e andando a ritroso.  

- **SpecifyDrive** (facoltativo): specificare una lettera di unità necessaria al programma per connettersi ai file del pacchetto nel punto di distribuzione. Questa impostazione forza l'uso della lettera di unità specificata per le connessioni client ai punti di distribuzione.

- **ReconnectDriveAtLogon**: specificare se il computer si riconnette al punto di distribuzione quando l'utente esegue l'accesso. I valori disponibili sono **True** o **False**. Il valore predefinito è **False**.  

- **DependentProgram**: specificare un programma in questo pacchetto che deve essere eseguito prima del programma corrente. Questa voce usa il formato `DependentProgram=<ProgramName>`, dove `<ProgramName>` corrisponde alla voce **Name** per il programma nel file di definizione del pacchetto. Se non sono presenti programmi dipendenti, lasciare vuota questa voce.  

    Esempi:  

    `DependentProgram=Admin`  
    `DependentProgram=`  

- **Assignment**: specificare come il programma viene assegnato agli utenti. Questo valore può essere:

    - **FirstUser**: solo il primo utente che accede al client esegue il programma
    - **EveryUser**: ogni utente che accede esegue il programma

    Quando **CanRunWhen** non è impostato su **UserLoggedOn**, questa voce è impostata su **FirstUser**.  

- **Disabilitato**: consente di specificare se è possibile distribuire il programma ai client. I valori disponibili sono **True** o **False**. Il valore predefinito è **False**.  


## <a name="use-a-package-definition-file"></a>Usare un file di definizione del pacchetto  

1. Nella console di Configuration Manager passare all'area di lavoro **Raccolta software**, espandere **Gestione applicazioni** e selezionare il nodo **Pacchetti**.  

2. Nel gruppo **Crea** della scheda **Home** della barra multifunzione scegliere **Crea pacchetto da definizione**.  

3. Nella pagina **Definizione pacchetto** della **Creazione guidata pacchetto da definizione** scegliere un file di definizione del pacchetto esistente. Per aprire un nuovo file di definizione del pacchetto, scegliere **Sfoglia**. Dopo aver specificato un nuovo file di definizione del pacchetto, selezionarlo nell'elenco **Definizione pacchetto**.

4. Nella pagina **File di origine** specificare le informazioni su tutti i file di origine necessari per il pacchetto e per il programma.  

5. Se il pacchetto richiede file di origine, nella pagina **Cartella di origine** specificare il percorso da cui il sito può ottenere i file di origine.  

6. Completare la procedura guidata.  


## <a name="see-also"></a>Vedere anche

[Pacchetti e programmi](packages-and-programs.md)
