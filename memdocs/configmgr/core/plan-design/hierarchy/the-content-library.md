---
title: Raccolta contenuto
titleSuffix: Configuration Manager
description: Informazioni sulla raccolta contenuto che Configuration Manager usa per ridurre le dimensioni complessive del contenuto distribuito.
ms.date: 07/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 65c88e54-3574-48b0-a127-9cc914a89dca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 253de522937e48fa1f3939c7303faf7e43e4e047
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704539"
---
# <a name="the-content-library-in-configuration-manager"></a>Raccolta contenuto in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

La raccolta contenuto è un archivio a istanza singola del contenuto in Configuration Manager. Il sito la usa per ridurre le dimensioni complessive del corpo combinato del contenuto distribuito. La raccolta contenuto archivia tutti i file di contenuto per le distribuzioni software, ad esempio: aggiornamenti software, applicazioni, distribuzioni di sistemi operativi.  

- Il sito crea e gestisce automaticamente una copia della raccolta contenuto in ogni server del sito e in ogni punto di distribuzione.  

- Prima di aggiungere i file di contenuto al server del sito o di copiare i file nei punti di distribuzione, Configuration Manager verifica se ogni file di contenuto si trova già nella raccolta contenuto.  

- Se il file di contenuto è disponibile, Configuration Manager non copia il file. Associa invece il file di contenuto esistente all'applicazione o al pacchetto.  

Nei server del punto di distribuzione configurare le opzioni seguenti:

- Una o più unità disco in cui creare la raccolta contenuto.  

- Una priorità per ogni unità usata.  

Configuration Manager copia i file di contenuto nell'unità con la priorità massima fino a quando lo spazio disponibile sull'unità è inferiore al valore specificato.  

- Durante l'installazione del punto di distribuzione, si configurano le impostazioni dell'unità.  

- Dopo il completamento dell'installazione non è possibile configurare le impostazioni dell'unità nelle proprietà del punto di distribuzione.  

Per altre informazioni su come configurare le impostazioni dell'unità per il punto di distribuzione, vedere [Gestire il contenuto e l'infrastruttura del contenuto](../../servers/deploy/configure/manage-content-and-content-infrastructure.md).  

> [!IMPORTANT]
> Per spostare la raccolta contenuto in un percorso diverso in un punto di distribuzione dopo l'installazione, usare lo **strumento per il trasferimento di raccolte contenuto** negli Strumenti di Configuration Manager. Per altre informazioni, vedere lo [strumento per il trasferimento di raccolte contenuto](../../support/content-library-transfer.md).  


## <a name="about-the-content-library-on-the-central-administration-site"></a>Informazioni sulla raccolta contenuto nel sito di amministrazione centrale

Per impostazione predefinita, Configuration Manager crea una raccolta contenuto nel sito di amministrazione centrale quando viene installato il sito. La raccolta contenuto viene collocata nell'unità del server del sito che dispone della maggior parte di spazio libero su disco. Dato che non è possibile installare un punto di distribuzione nel sito di amministrazione centrale, non è possibile assegnare priorità alle unità usate dalla raccolta contenuto. In modo simile alla raccolta contenuto sugli altri server del sito e sui punti di distribuzione, quando l'unità che contiene la raccolta contenuto esaurisce lo spazio su disco disponibile, la raccolta contenuto si espande automaticamente sull'unità successiva disponibile.  

Configuration Manager usa la raccolta contenuto nel sito di amministrazione centrale negli scenari seguenti:  

- Per creare contenuto nel sito di amministrazione centrale.  

- Per eseguire la migrazione del contenuto da un altro sito di Configuration Manager e assegnare il sito di amministrazione centrale come sito che si occuperà della gestione del contenuto.  

> [!NOTE]  
> Quando si crea contenuto in un sito primario e lo si distribuisce in un sito primario diverso o in un sito secondario di un sito primario diverso, il sito di amministrazione centrale archivia temporaneamente quel contenuto nella posta in arrivo dell'Utilità di pianificazione del sito di amministrazione centrale, ma non lo aggiunge alla propria raccolta contenuto.  

Utilizzare le seguenti opzioni per gestire la raccolta contenuto nel sito di amministrazione centrale:  

- Per evitare che la raccolta contenuto venga installata in un'unità specifica, creare un file vuoto denominato **no_sms_on_drive.sms**. Copiarlo nella radice dell'unità prima che venga creata la raccolta contenuto.  

- Dopo la creazione della raccolta contenuto, usare lo **strumento per il trasferimento di raccolte contenuto** negli Strumenti di Configuration Manager per gestire la posizione della raccolta contenuto. Per altre informazioni, vedere lo [strumento per il trasferimento di raccolte contenuto](../../support/content-library-transfer.md).  

> [!Note]  
> I punti di distribuzione del cloud non usano l'archiviazione a istanza singola. Il sito esegue la crittografia dei pacchetti prima dell'invio ad Azure e ogni pacchetto ha una chiave crittografata univoca. Anche se i due file sono identici, le versioni crittografate non saranno uguali.  


## <a name="configure-a-remote-content-library-for-the-site-server"></a><a name="bkmk_remote"></a> Configurare una raccolta contenuto remota per il server del sito

<!--1357525-->
A partire dalla versione 1806 per configurare la [disponibilità elevata del server del sito](../../servers/deploy/configure/site-server-high-availability.md) o per liberare spazio sul disco rigido nei server del sito di amministrazione centrale o del sito primario, spostare la raccolta contenuto in un'altra posizione di archiviazione. Spostare la raccolta contenuto in un'altra unità sul server del sito, su un server distinto o su dischi a tolleranza d'errore in una rete di archiviazione (SAN). È consigliabile una SAN perché è a disponibilità elevata e fornisce uno spazio di archiviazione elastico, che può aumentare o ridursi nel tempo per soddisfare i requisiti mutevoli del contenuto. Per altre informazioni, vedere [Opzioni di disponibilità elevata](../../servers/deploy/configure/site-server-high-availability.md).

Una raccolta contenuto remota è un prerequisito per la [disponibilità elevata del server del sito](../../servers/deploy/configure/site-server-high-availability.md).

> [!Note]  
> Questa azione sposta solo la raccolta contenuto nel server del sito. Non influisce sulla posizione della raccolta contenuto nei punti di distribuzione. 

> [!Tip]  
> Pianificare inoltre la gestione del contenuto di origine del pacchetto, che è esterno alla raccolta contenuto. Ogni oggetto software in Configuration Manager ha un'origine del pacchetto in una condivisione di rete. Provare a centralizzare tutte le origini in una singola condivisione, ma assicurarsi che questo percorso sia ridondante e a disponibilità elevata.
>
> Se si sposta la raccolta contenuto nello stesso volume di archiviazione delle origini del pacchetto, non è possibile contrassegnare il volume per la deduplicazione dei dati. Anche se la raccolta contenuto supporta la deduplicazione dei dati, il volume delle origini del pacchetto non la supporta. Per altre informazioni, vedere [Deduplicazione dei dati](../configs/support-for-windows-features-and-networks.md#bkmmk_datadedup).<!--SCCMDOcs issue #831-->  

### <a name="prerequisites"></a>Prerequisiti  

- L'account computer del server del sito deve avere le autorizzazioni **Controllo completo** per il percorso di rete in cui deve essere spostata la raccolta contenuto. Questa autorizzazione è applicabile sia alla condivisione che al file system. Non sono installati componenti nel sistema remoto.

- Il server del sito non può avere il ruolo di punto di distribuzione. Il punto di distribuzione usa anche la raccolta contenuto e questo ruolo non supporta una raccolta contenuto remota. Dopo aver spostato la raccolta contenuto, non è possibile aggiungere il ruolo di punto di distribuzione al server del sito.  

> [!Important]  
> Non riusare un percorso di rete condiviso tra più siti. Ad esempio, non usare lo stesso percorso sia per un sito di amministrazione centrale che per un sito primario figlio. Questa configurazione potrebbe danneggiare la raccolta contenuto che dovrà essere ricompilata.<!--SCCMDocs-pr issue 2764-->  

### <a name="process-to-manage-the-content-library"></a>Processo per gestire la raccolta contenuto

1. Creare una cartella in una condivisione di rete come la destinazione per la raccolta contenuto. Ad esempio, `\\server\share\folder`  

    > [!Warning]  
    > Non riusare una cartella esistente con contenuto. Ad esempio, non usare la stessa cartella delle origini del pacchetto. Prima di copiare la raccolta contenuto, Configuration Manager rimuove qualsiasi contenuto esistente dalla posizione specificata.  

2. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**. Espandere **Configurazione del sito**, selezionare il nodo **Siti** e selezionare il sito. Nella scheda **Riepilogo** nella parte inferiore del riquadro dei dettagli è visibile una nuova colonna **Raccolta contenuto**.  

3. Selezionare **Gestisci la raccolta contenuto** nella barra multifunzione.  

4. Il campo **Posizione corrente** nella finestra Gestisci la raccolta contenuto mostra l'unità e il percorso locali. Immettere un percorso di rete valido in **Nuova posizione**. Questo percorso è la posizione in cui il sito sposta la raccolta contenuto. Deve includere un nome di cartella già esistente nella condivisione, ad esempio, `\\server\share\folder`. Selezionare **OK**.  

5. Notare il valore **Stato** nella colonna Raccolta contenuto della scheda Riepilogo nel riquadro dei dettagli. Viene aggiornata per mostrare lo stato di avanzamento del sito durante lo spostamento della raccolta contenuto.  

   - Quando è **In corso**, il valore **Stato dello spostamento (%)** visualizza la percentuale di completamento.  

        > [!Note]  
        > Se è disponibile una raccolta contenuto di grandi dimensioni, potrebbe essere indicato lo stato di avanzamento `0%` nella console per un periodo di tempo. Ad esempio, con una raccolta di 1 TB devono essere copiati 10 GB prima che il valore di avanzamento diventi `1%`. Esaminare **distmgr.log**, che mostra il numero di file e byte copiati. A partire dalla versione 1810, il file di log mostra anche il tempo stimato rimanente.

   - Se è presente uno stato di errore, viene visualizzato l'errore. Gli errori tipici comprendono **accesso negato** o **disco pieno**.  

   - Al termine, viene visualizzato **Completo**.  

     Per informazioni dettagliate, vedere **distmgr.log**. Per altre informazioni, vedere [Log del server del sito e del server di sistema del sito](log-files.md#BKMK_SiteSiteServerLog).  

Per altre informazioni su questo processo, vedere [Diagramma di flusso - Gestire la raccolta contenuto](manage-content-library-flowchart.md).

Il sito *copia* effettivamente file della raccolta contenuto nel percorso remoto. Questo processo non elimina i file della raccolta contenuto nel percorso originale del server del sito. Per liberare spazio, un amministratore deve eliminare manualmente questi file originali.

Se la raccolta contenuto originale si estende su due unità, viene unita in un'unica cartella nella nuova destinazione.

A partire dalla versione 1810, durante il processo di copia, i componenti **Despooler** e **Distribution Manager** non elaborano i nuovi pacchetti. Questa azione assicura che non venga aggiunto contenuto alla raccolta durante lo spostamento. Ciò nonostante, pianificare questa modifica durante una finestra di manutenzione del sistema.

Se è necessario spostare nuovamente la raccolta contenuto nel server del sito, ripetere questo processo, ma immettere un'unità e un percorso locali in **Nuova posizione**. Deve includere un nome di cartella già esistente nell'unità, ad esempio, `D:\SCCMContentLib`. Quando il contenuto originale è ancora presente, il processo sposta rapidamente la configurazione nel percorso locale al server del sito.

> [!Tip]  
> Per spostare il contenuto in un'altra unità nel server del sito, usare lo **strumento per il trasferimento di raccolte di contenuto**. Per altre informazioni, vedere lo [strumento per il trasferimento di raccolte contenuto](../../support/content-library-transfer.md).  


## <a name="inside-the-content-library"></a>All'interno della raccolta contenuto

> [!Warning]  
> La sezione seguente viene fornita esclusivamente a scopo informativo. Non modificare, aggiungere o rimuovere i file o le cartelle nella raccolta contenuto. In caso contrario, si potrebbero danneggiare pacchetti, contenuti o l'intera raccolta contenuto. Se si ritiene che ci siano dati mancanti, danneggiati o non validi, usare la funzionalità di convalida nella console di Configuration Manager per rilevare tali problemi. Ridistribuire quindi il contenuto interessato per correggere i problemi.

Per impostazione predefinita, la raccolta contenuto viene archiviata nella radice di un'unità in una cartella denominata **SCCMContentLib**. Questa cartella viene condivisa per impostazione predefinita come **SCCMContentLib$** . La cartella e la condivisione hanno autorizzazioni limitate per impedire danni accidentali. Tutte le modifiche devono essere apportate dalla console di Configuration Manager. In questa cartella sono presenti gli oggetti seguenti:  

- Raccolta pacchetti (cartella **PkgLib**): informazioni su quali pacchetti sono presenti nel punto di distribuzione.  

- Raccolta dati (cartella **DataLib**): informazioni sulla struttura originale dei pacchetti.  

- Raccolta file (cartella **FileLib**): file originali del pacchetto. Questa cartella è in genere quella che usa la maggior parte dello spazio di archiviazione.  

![Panoramica del diagramma della raccolta contenuto di Configuration Manager](media/content-library-overview.png)

> [!Tip]  
> Usare lo strumento **Content Library Explorer** presente negli strumenti di Configuration Manager per visualizzare il contenuto della raccolta contenuto. È possibile usare questo strumento per modificare il contenuto. Fornisce informazioni dettagliate sugli elementi presenti, nonché ne consente la convalida e la ridistribuzione. Per altre informazioni, vedere [Content Library Explorer](../../support/content-library-explorer.md).  

### <a name="package-library"></a>Raccolta pacchetti

La cartella della raccolta pacchetti, **PkgLib**, include un file per ogni pacchetto distribuito nel punto di distribuzione. Il nome del file è l'ID del pacchetto, ad esempio `ABC00001.INI`. Nella sezione `[Packages]` di questo file è presente un elenco di ID contenuto che fanno parte del pacchetto, nonché altre informazioni come ad esempio la versione. Ad esempio, **ABC00001** è un pacchetto legacy con versione **1**. L'ID contenuto in questo file è `ABC00001.1`.

### <a name="data-library"></a>Raccolta dati

La cartella della raccolta dati, **DataLib**, include un file e una cartella per ogni contenuto di ciascun pacchetto. Ad esempio, il file e la cartella sono denominati rispettivamente `ABC00001.1.INI` e `ABC00001.1`. Il file include informazioni per la convalida. La cartella ricrea la struttura di cartelle del pacchetto originale.

I file presenti nella raccolta dati vengono sostituiti dai file con estensione INI con il nome del file originale nel pacchetto. Ad esempio, `MyFile.exe.INI` Questi file contengono informazioni sul file originale, ad esempio le dimensioni, l'ora di modifica e l'hash. Usare i primi quattro caratteri dell'hash per trovare il file originale nella raccolta file. Ad esempio, l'hash in MyFile.exe.INI è **DEF98765** e i primi quattro caratteri sono **DEF9**.

### <a name="file-library"></a>Raccolta file

Se la raccolta contenuto si estende in più unità, i file del pacchetto potrebbero trovarsi nella cartella della raccolta file, **FileLib**, in una qualsiasi delle unità.

Trovare un file specifico usando i primi quattro caratteri dell'hash usato nella raccolta dati. All'interno della cartella della raccolta file sono presenti molte cartelle, ognuna con un nome di quattro caratteri. Trovare la cartella che corrisponde ai primi quattro caratteri dell'hash. Questa cartella include uno o più set di tre file. Questi file condividono lo stesso nome, ma uno ha l'estensione INI, uno ha l'estensione SIG e uno non ha alcuna estensione di file. Il file originale è quello con nessuna estensione il cui nome è uguale all'hash della raccolta dati.

Ad esempio, la cartella **DEF9** include `DEF98765.INI`, `DEF98765.SIG` e `DEF98765`. `DEF98765` è il file `MyFile.exe` originale. Il file con estensione INI include un elenco di "utenti" o ID contenuto che condividono lo stesso file. Il sito non rimuove un file a meno che non vengono rimossi anche tutti i contenuti.

### <a name="drive-spanning"></a>Estensione in più unità

La raccolta contenuto può essere estesa in più unità. È possibile scegliere le unità quando si crea il punto di distribuzione. Per impostazione predefinita, Configuration Manager sceglie automaticamente le unità durante l'estensione della raccolta contenuto.

Quando si scelgono le unità, selezionare un'unità principale e un'unità secondaria. Il sito archivia tutti i metadati nell'unità primaria. Estende solo la raccolta file nell'unità secondaria. Il nome condivisione della cartella per le unità secondarie include la lettera di unità. Ad esempio, se D: ed E: sono le unità secondarie per la raccolta contenuta, i nomi condivisione saranno **SCCMContentLibD$** e **SCCMContentLibE$** .

Se si sceglie l'opzione **Automatico**, Configuration Manager seleziona l'unità con la maggiore quantità di spazio disponibile come unità primaria. Archivia tutti i metadati in questa unità. Il sito estende solo la raccolta file nelle unità secondarie.

È possibile specificare una quantità di spazio di riserva durante la configurazione. Configuration Manager prova a usare un disco secondario dopo che nel miglior disco disponibile è rimasta libera solo questa quantità di spazio di riserva. Ogni volta che viene selezionata una nuova unità da usare, viene selezionata l'unità con la maggiore quantità di spazio disponibile.

Non è possibile specificare che un punto di distribuzione deve usare tutte le unità, ad eccezione di un set specifico. In alternativa, è possibile creare un file vuoto nella radice dell'unità denominato `NO_SMS_ON_DRIVE.SMS`. Inserire questo file prima che Configuration Manager selezioni l'unità da usare. Se Configuration Manager rileva questo file nella radice dell'unità, non userà l'unità per la raccolta contenuto.


## <a name="troubleshooting"></a>Risoluzione dei problemi

I suggerimenti seguenti consentono di risolvere i problemi con la raccolta contenuto:  

- Esaminare i log nel server del sito (**distmgr.log** e **PkgXferMgr.log**) e il punto di distribuzione (**smsdpprov.log**) per tutti i puntatori agli errori.  

- Usare lo strumento [Content Library Explorer](../../support/content-library-explorer.md).  

- Verificare se sono presenti blocchi di file di altri processi, ad esempio un software antivirus. Escludere la raccolta contenuto in tutte le unità dalle analisi antivirus automatiche, nonché la directory di gestione temporanea, **SMS_DP$** , in ciascuna unità.  

- Per verificare se sono presenti hash non corrispondenti, convalidare il pacchetto dalla console di Configuration Manager.  

- Come ultima opzione, ridistribuire il contenuto. Questa azione dovrebbe risolvere la maggior parte dei problemi.  
