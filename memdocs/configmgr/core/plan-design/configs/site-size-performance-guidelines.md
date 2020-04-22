---
title: Linee guida per dimensioni e prestazioni del sito
titleSuffix: Configuration Manager
description: Risultati dei test delle prestazioni correlati alle dimensioni del sito, metodologia e indicazioni.
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: conceptual
ms.date: 04/23/2019
ms.openlocfilehash: 7380621fdc7a7f4d26b4844df3ee9026f0997024
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688649"
---
# <a name="configuration-manager-site-size-and-performance-guidelines"></a>Linee guida sulle dimensioni e sulle prestazioni dei siti di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Configuration Manager è la miglior soluzione del settore per scalabilità e prestazioni. In un'altra documentazione sono descritti i [limiti massimi di scalabilità supportati](size-and-scale-numbers.md) e le [linee guida relative all'hardware](recommended-hardware.md) per i siti in esecuzione in ambienti di grandi dimensioni. Questo articolo offre ulteriori linee guida sulle prestazioni per gli ambienti di qualsiasi dimensione. Queste indicazioni consentono di individuare in modo più preciso l'hardware necessario per la distribuzione di Configuration Manager.

Questo articolo tratta in particolare l'aspetto che più contribuisce alla generazione dei colli di bottiglia per le prestazioni di Configuration Manager: il sottosistema di input/output del disco o le operazioni di I/O al secondo. L'articolo:

- Illustra i dettagli e i risultati dei test relativi alle operazioni di I/O al secondo
- Descrive come riprodurre i test con gli ambienti e l'hardware in uso
- Indica i requisiti relativi alle operazioni di I/O al secondo del disco per ambienti di dimensioni diverse 

## <a name="performance-test-methodology"></a>Metodologia dei test delle prestazioni

È possibile distribuire Configuration Manager in molti modi univoci, ma è importante comprendere alcune variabili relative a tutte le dimensioni. Una variabile è l'*intervallo delle funzionalità*, ad esempio un ciclo di inventario. Un'altra variabile è il numero di utenti, distribuzioni software o altri *oggetti* cui il sistema fa riferimento o distribuisce. I test delle prestazioni applicano queste variabili come parte di un *carico*. Il carico genera oggetti con una frequenza tipica per i clienti aziendali usando le distribuzioni di produzione in ambienti di dimensioni diverse.

> [!NOTE] 
> I dati di telemetria dei clienti consentono di testare le build del ramo corrente con gli scenari, le configurazioni e le impostazioni più comuni per la maggior parte dei clienti. Le raccomandazioni in questo articolo si basano su queste medie. Le esperienze possono variare in base alle dimensioni e alla configurazione dell'ambiente. In generale, Configuration Manager richiede buon senso relativamente agli oggetti e agli intervalli. Sebbene sia possibile raccogliere tutti i file di un sistema o impostare l'intervallo di un ciclo su un minuto, ciò non significa che queste operazioni vadano necessariamente eseguite.

Nelle sezioni seguenti sono descritte alcune impostazioni chiave e alcune configurazioni da usare per il test e la modellazione delle esigenze di elaborazione di aziende di grandi dimensioni. Queste linee guida sono utili per definire le principali aspettative sulle prestazioni di sistema per le dimensioni dell'hardware suggerite.

### <a name="feature-intervals-settings"></a>Impostazioni degli intervalli delle funzionalità 
Nella maggior parte dei test usare gli intervalli predefiniti per i cicli principali del sistema. Ad esempio, il test di inventario hardware si verifica una volta alla settimana con un file con estensione *mof* di dimensioni maggiori rispetto al file predefinito. Alcuni intervalli di funzionalità ricorrenti, in particolare i cicli di inventario hardware e software, possono avere effetti significativi sulle caratteristiche delle prestazioni di un ambiente. Gli ambienti in cui è possibile usare intervalli predefiniti aggressivi per la raccolta dati richiedono hardware di dimensioni eccessive direttamente proporzionali all'aumento dell'attività. Ad esempio, si supponga di avere 25.000 client desktop e che si desideri raccogliere l'inventario hardware in modo due volte più veloce rispetto all'intervallo predefinito. Sarà necessario iniziare definendo le dimensioni dell'hardware del sito come se si avessero 50.000 client.

### <a name="objects"></a>Oggetti 
I test dovranno usare la *media maggiore* degli oggetti usati in genere dalle aziende di grandi dimensioni con il sistema. I valori tipici corrispondono a migliaia di raccolte e applicazioni che vengono distribuite a centinaia di migliaia di utenti o sistemi. I test dovranno essere eseguiti simultaneamente in *tutti* gli oggetti del sistema con questi limiti. Molti clienti usano diverse funzionalità, ma solitamente non usano tutte le funzionalità del prodotto a questi limiti massimi. I test con tutte le funzionalità del prodotto garantiscono le migliori prestazioni possibili a livello di sistema e offrono un margine per le funzionalità che alcuni clienti potrebbero usare al di sopra della media. 

### <a name="loads"></a>Carichi 
I test dovranno inoltre essere eseguiti su carichi *medi giornalieri* maggiori dei carichi standard eseguendo simulazioni che generano picchi di domanda di utilizzo nel sistema. Un esempio consiste nel simulare le implementazioni Patch Tuesday per assicurarsi che il sistema sia in grado di restituire rapidamente i dati di conformità degli aggiornamenti nelle giornate di picco dell'attività. Un altro esempio è la simulazione dell'attività del sito durante un attacco malware diffuso per garantire una notifica e una risposta tempestive. Anche se le macchine distribuite della dimensione consigliata potrebbero risultare sottoutilizzate in determinate giornate, altre condizioni più estreme richiedono un buffer di elaborazione.

### <a name="configurations"></a>Configurazioni
Eseguire i test in più hardware fisici, Hyper-V e Azure con diversi sistemi operativi supportati e diverse versioni di SQL Server. Convalidare sempre i casi più critici per la configurazione supportata. In generale, Hyper-V e Azure offrono prestazioni paragonabili in hardware fisici equivalenti con configurazione simile. I sistemi operativi server più recenti offrono prestazioni equivalenti o migliori rispetto alle versioni precedenti dei sistemi operativi server supportati. Sebbene tutte le piattaforme supportate soddisfino i requisiti minimi, le versioni più recenti dei prodotti supportati come Windows e SQL offrono solitamente prestazioni migliori. 

La variazione più grande deriva dalle versioni di SQL Server in uso. Per altre informazioni sulle versioni di SQL Server, vedere [Quale versione di SQL è consigliabile eseguire?](../../understand/site-size-performance-faq.md#what-version-of-sql-should-i-run) 

## <a name="key-performance-determinants"></a>Fattori chiave delle prestazioni

È possibile testare e misurare le prestazioni di Configuration Manager con un'ampia gamma di impostazioni, in modi diversi e in siti di dimensioni differenti. Le impostazioni e gli oggetti seguenti possono influire notevolmente sulle prestazioni. Assicurarsi di prenderli in considerazione durante il test e la modellazione delle prestazioni nell'ambiente.

> [!CAUTION]
> Mentre alcuni aspetti di Configuration Manager hanno limiti massimi o limiti di interfaccia utente ufficiali che impediscono l'utilizzo eccessivo, il superamento delle linee guida può avere effetti negativi significativi sulle prestazioni di un sito. Il superamento dei livelli consigliati ignorando le linee guida sulle dimensioni richiede un hardware di livello superiore e potrebbe compromettere la gestione dell'ambiente fino a quando non si riduce la frequenza o il totale dei diversi oggetti.

### <a name="hardware-inventory"></a>Inventario hardware
Per testare le prestazioni di base, impostare la raccolta dell'inventario hardware su una volta alla settimana, con le dimensioni del file con estensione *mof* predefinite a cui si aggiunge circa il 20% delle proprietà aggiuntive. Non abilitare tutte le proprietà e raccogliere solo le proprietà effettivamente necessarie. Prestare particolare attenzione durante la raccolta di proprietà, ad esempio la memoria virtuale disponibile, che cambiano *sempre* a *ogni* ciclo di inventario. La raccolta di queste proprietà può causare una varianza eccessiva in ogni ciclo di inventario da qualsiasi client.

### <a name="software-inventory"></a>Inventario software
Per testare le prestazioni di base, impostare la raccolta dell'inventario software su una volta alla settimana con i dettagli *Solo prodotto*. La raccolta di numerosi file può mettere a dura prova il sottosistema di inventario. Evitare di specificare filtri che possono causare la raccolta di migliaia di file di diversi client, ad esempio di file con estensione *\*exe* o *\*dll*.

### <a name="collections"></a>Raccolte
Il test delle prestazioni di base può includere diverse migliaia di raccolte con una varietà di ambiti, dimensioni, complessità e impostazioni di aggiornamento. Le prestazioni del sito non sono una funzione diretta del numero di raccolte in un sito. Le prestazioni sono anche il risultato della complessità delle query, degli aggiornamenti completi e incrementali e della frequenza di modifica delle raccolte, delle dipendenze tra le raccolte e del totale di client nelle raccolte.

Dove possibile, ridurre al minimo le raccolte con query complesse e con regole dinamiche. Per le raccolte che richiedono questi tipi di regole, impostare intervalli e orari di aggiornamento appropriati per ridurre al minimo l'impatto della rivalutazione della raccolta nel sistema. Ad esempio, eseguire l'aggiornamento a mezzanotte anziché alle 8:00 del mattino.

L'abilitazione di aggiornamenti incrementali per le raccolte garantisce aggiornamenti rapidi e tempestivi all'appartenenza alla raccolta. Tuttavia, sebbene risultino efficienti, gli aggiornamenti incrementali comportano comunque un carico sul sistema. Bilanciare la frequenza di modifica prevista con l'esigenza di aggiornamenti quasi in tempo reale all'appartenenza. Ad esempio, si supponga di prevedere una varianza elevata nei membri della raccolta, ma di non avere la necessità di aggiornamenti dell'appartenenza quasi in tempo reale. Un aggiornamento completo pianificato della raccolta con un determinato intervallo risulta più efficiente e produce minor carico sul sistema rispetto all'abilitazione degli aggiornamenti incrementali. 

Quando si abilitano gli aggiornamenti incrementali, ridurre gli aggiornamenti completi pianificati per le stesse raccolte. Gli aggiornamenti completi rappresentano soltanto un metodo di backup di valutazione poiché gli aggiornamenti incrementali mantengono aggiornata l'appartenenza alla raccolta quasi in tempo reale. Sebbene nelle [procedure consigliate per le raccolte](../../clients/manage/collections/best-practices-for-collections.md#bkmk_incremental) sia consigliato un numero massimo di raccolte per gli aggiornamenti incrementali, l'esperienza può variare in base a numerosi fattori.

Le raccolte che includono solo regole di appartenenza diretta e con una raccolta di limitazione che non esegue gli aggiornamenti incrementali non richiedono aggiornamenti completi pianificati. Disabilitare le pianificazioni degli aggiornamenti per questi tipi di raccolte per evitare un carico superfluo sul sistema. Se la raccolta di limitazione usa gli aggiornamenti incrementali, le raccolte che includono solo regole di appartenenza diretta potrebbero non riflettere gli aggiornamenti di appartenenza per un massimo di 24 ore o fino a quando non viene eseguito un aggiornamento pianificato.

Sebbene non sia una procedura consigliata, alcune organizzazioni creano centinaia o persino migliaia di raccolte come parte dei diversi processi aziendali. Se si usa l'automazione per creare le raccolte, è importante abilitare correttamente tutti gli aggiornamenti incrementali necessari. Ridurre al minimo e distribuire eventuali pianificazioni di aggiornamenti completi per evitare le aree sensibili della valutazione delle raccolte durante un singolo periodo di tempo. Definire un processo di pulitura regolare per eliminare le raccolte non usate, in particolare se vengono create automaticamente raccolte che non sono più necessarie dopo poco tempo.

Tenere presente che Configuration Manager crea criteri per tutti gli oggetti delle raccolte quando la destinazione è costituita da attività come le distribuzioni negli oggetti. Le modifiche all'appartenenza, tramite aggiornamento pianificato o aggiornamenti incrementali, possono creare ulteriore carico per l'intero sistema. Le build del ramo corrente più recenti includono speciali ottimizzazioni dei criteri per le raccolte Tutti i sistemi e Tutti gli utenti. Quando la destinazione è l'intera organizzazione, usare le raccolte predefinite anziché un clone delle raccolte predefinite.

Per analizzare le prestazioni delle raccolte in maggior dettaglio, è possibile usare Collection Evaluation Viewer (CEViewer) nel [toolkit di Configuration Manager](https://www.microsoft.com/download/details.aspx?id=50012).

### <a name="discovery-methods"></a>Metodi di individuazione
Per il test delle prestazioni di base, eseguire i metodi di individuazione basati su server una volta alla settimana, abilitando l'individuazione differenziale appropriata per mantenere aggiornati i dati durante la settimana. I test devono individuare una quantità di oggetti proporzionale alle dimensioni dell'azienda simulate. Anche il test delle prestazioni di base per l'individuazione heartbeat deve essere eseguito una volta alla settimana.

I dati di individuazione sono dati globali. Un problema comune legato alle prestazioni è la configurazione errata dei metodi di individuazione basati su server in una gerarchia che causa l'individuazione duplicata delle stesse risorse di più siti primari. Configurare con attenzione i metodi di individuazione per ottimizzare la comunicazione con il servizio di destinazione, ad esempio con i controller di dominio Active Directory, evitando la duplicazione dello stesso ambito di individuazione su più siti primari.

## <a name="general-sizing-guidelines"></a>Linee guida generali sulle dimensioni 

In base alla [metodologia di test delle prestazioni](#performance-test-methodology) precedente, la tabella seguente offre le linee guida relative ai requisiti hardware *minimi* generali per numeri specifici di client gestiti. Questi valori consentiranno alla maggior parte dei clienti con il numero di client specificato di elaborare gli oggetti in modo sufficientemente rapido per gestire il sito specificato. La potenza di elaborazione continua a diminuire di prezzo di anno in anno e alcuni dei requisiti riportati di seguito possono apparire limitati per le configurazioni hardware dei server moderni. L'hardware che supera le linee guida seguenti aumenta in modo proporzionale le prestazioni per i siti che richiedono maggiore potenza di elaborazione o hanno modelli di utilizzo del prodotto speciali. 

| Client desktop  | Tipo/ruolo del sito  | Core<sup>1</sup>   | Memoria (GB)   | Allocazione di memoria SQL  | Operazioni di I/O al secondo:  Cartelle posta in arrivo<sup>2</sup>  | Operazioni di I/O al secondo: SQL<sup>2</sup>   | Spazio di archiviazione richiesto (GB)<sup>3</sup>   |
|------|-------------------------------------------------------------|-----|-----|-----|------|------|------|
| 25 KB  | Primario o CAS con ruolo del sito del database nello stesso server   | 6   | 24  | 65% | 600  | 1700 | 350  |
| 25 KB  | Primario o CAS                                              | 4   | 8   |     | 600  |      | 100  |
|      | SQL remoto                                                  | 4   | 16  | 70% |      | 1700 | 250  |
|      |                                                             |     |     |     |      |      |      |
| 50 KB  | Primario o CAS con ruolo del sito del database nello stesso server   | 8   | 32  | 70% | 1200 | 2800 | 600  |
| 50 KB  | Primario o CAS                                              | 4   | 8   |     | 1200 |      | 200  |
|      | SQL remoto                                                  | 8   | 24  | 70% |      | 2800 | 400  |
|      |                                                             |     |     |     |      |      |      |
| 100 KB | Primario o CAS con ruolo del sito del database nello stesso server   | 12  | 64  | 70% | 1200 | 5000 | 1100 |
| 100 KB | Primario o CAS                                              | 6   | 12  |     | 1200 |      | 300  |
|      | SQL remoto                                                  | 12  | 48  | 80% |      | 5000 | 800  |
|      |                                                             |     |     |     |      |      |      |
| 150 KB | Primario o CAS con ruolo del sito del database nello stesso server   | 16  | 96  | 70% | 1800 | 7400 | 1600 |
| 150 KB | Primario o CAS                                   | 8   | 16   |     | 1800  |         | 400   |
|      | SQL remoto                                       | 16  | 72   | 90% |       | 7400    | 1200  |
|      |                                                             |     |     |     |      |      |      |
| 700 KB | CAS con ruolo del sito del database nello stesso server   | 20+ | 128+ | 80% | 1800+ | 9000+   | 5000+ |
| 700 KB | CAS                                              | 8+  | 16+  |     | 1800+ |         | 500+  |
|      | SQL remoto                                       | 16+ | 96+  | 90% |       | 9000+   | 4500+ |
|      |                                                             |     |     |     |      |      |      |
| 5 KB   | Sito secondario                                   | 4   | 8    |     | 500   | -       | 200   |
| 15 KB  | Sito secondario                                   | 8   | 16   |     | 500   | -       | 300   |

**Note**

1. **Core**: Poiché esegue numerosi processi simultanei, Configuration Manager richiede un determinato numero minimo di core della CPU per i siti di dimensioni diverse. Sebbene i core diventino sempre più veloci di anno in anno, è importante assicurarsi che un determinato numero minimo di core vengano usati in parallelo. In generale, qualsiasi CPU a livello server prodotta dopo il 2015 soddisfa i requisiti di prestazioni di base per i core specificati nella tabella. Sebbene Configuration Manager usi i core aggiuntivi, in generale quando si ha a disposizione il numero minimo di core consigliati, è consigliabile dare priorità all'investimento sulle risorse delle CPU per aumentare la velocità dei core esistenti anziché aggiungere core più lenti. Ad esempio, Configuration Manager offrirà prestazioni migliori nelle attività di elaborazione chiave usando 16 core veloci rispetto a 24 core più lenti, a condizione che siano disponibili altre risorse di sistema sufficienti come le operazioni di I/O al secondo del disco.
   
   Anche la relazione tra core e memoria è importante. In generale, avere meno di 3-4 GB di RAM per core riduce la capacità di elaborazione totale sui server SQL. Quando SQL si trova con i componenti server del sito è necessaria una maggior quantità di RAM per core.
   
   > [!NOTE]
   > Per tutti i test vengono impostate combinazioni per il risparmio di energia che offrono il massimo risparmio di energia della CPU e le migliori prestazioni.
   
2. **Operazioni di I/O al secondo: Cartelle posta in arrivo e Operazioni di I/O al secondo: SQL** fanno riferimento alle operazioni di I/O al secondo necessarie per Configuration Manager e le unità logiche SQL. La colonna **Operazioni di I/O al secondo: Cartelle posta in arrivo** indica i requisiti di operazioni di I/O al secondo per l'unità logica in cui si trovano le directory delle cartelle posta in arrivo di Configuration Manager. La colonna **Operazioni di I/O al secondo: SQL** mostra il numero totale di operazioni di I/O al secondo necessarie per le unità logiche usate dai diversi file SQL. Queste colonne sono diverse poiché le due unità devono avere una formattazione diversa. Per altre informazioni ed esempi di configurazioni del disco SQL consigliate e per le procedure consigliate per i file, incluse informazioni dettagliate sulla suddivisione dei file su più volumi, vedere le [domande frequenti sulle dimensioni del sito e le prestazioni](../../understand/site-size-performance-faq.md).
   
   Entrambe le colonne Operazioni di I/O al secondo usano i dati provenienti dallo strumento standard di settore *Diskspd*. Per istruzioni sulla duplicazione di queste misure, vedere [Come misurare le prestazioni del disco](#how-to-measure-disk-performance). In generale, quando i requisiti di memoria e CPU di base sono soddisfatti, il sottosistema di archiviazione è il componente che ha maggior impatto sulle prestazioni del sito e i miglioramenti al sottosistema di archiviazione offrono il maggior ritorno sull'investimento.
   
3.  **Spazio di archiviazione richiesto:** Questi valori reali possono differire dalle altre raccomandazioni documentate. Questi valori sono indicati a solo scopo di linea guida generale; i requisiti individuali possono variare notevolmente. Pianificare con attenzione le esigenze di spazio su disco prima dell'installazione del sito. Presupporre che una parte dello spazio di archiviazione rimanga come spazio libero su disco per la maggior parte del tempo. È possibile usare questo spazio di buffer in uno scenario di ripristino o per scenari di aggiornamento che di spazio libero su disco per l'espansione del pacchetto di installazione. Il sito potrebbe richiedere ulteriore spazio di archiviazione per grandi quantità di raccolte dati, periodi di conservazione dei dati più lunghi e grandi quantità di contenuti di distribuzione del software. È anche possibile archiviare questi elementi in volumi separati con velocità effettiva inferiore.

## <a name="how-to-measure-disk-performance"></a>Come misurare le prestazioni del disco 

È possibile usare lo strumento standard di settore *Diskspd* per offrire indicazioni standardizzate sulle operazioni di I/O al secondo richieste dagli ambienti di Configuration Manager di dimensioni diverse. Pur non essendo esaustive, la procedura per il test e le righe di comando seguenti offrono un metodo semplice e riproducibile per stimare la velocità effettiva del sottosistema del disco dei server. È possibile confrontare i risultati ottenuti con il numero minimo di operazioni di I/O al secondo consigliato nella tabella delle [Linee guida generali sulle dimensioni](#general-sizing-guidelines). 

Per i risultati dei test di diverse configurazioni hardware in ambienti lab, vedere [Configurazioni del disco di esempio](#example-disk-configurations). È possibile usare i dati come base di partenza per la progettazione del sottosistema di archiviazione per un nuovo ambiente.

### <a name="to-test-disk-iops"></a>Per testare le operazioni di I/O al secondo del disco  
1. Scaricare l'utilità *Diskspd* all'indirizzo: [https://gallery.technet.microsoft.com/DiskSpd-A-Robust-Storage-6ef84e62](https://gallery.technet.microsoft.com/DiskSpd-A-Robust-Storage-6ef84e62).
   
1. Assicurarsi di avere almeno 100 GB di spazio libero su disco. Disabilitare tutte le app che potrebbero interferire o causare un carico aggiuntivo sul disco, ad esempio l'analisi antivirus attiva della directory, di SQL o di SMSExec.
   
1. Eseguire *Diskspd* da un prompt dei comandi con privilegi elevati. 
   
   Eseguire lo strumento due volte in sequenza per il volume che si vuole testare. Il primo test esegue operazioni di scrittura casuali a 64 KB per un minuto. Questo test verifica il caricamento della cache del controller e l'allocazione di spazio su disco, nel caso in cui il volume abbia un'espansione dinamica. Eliminare i risultati del primo test. Il secondo test deve essere eseguito *immediatamente* dopo il primo ed eseguire lo stesso carico per cinque minuti.
   
   Ad esempio, usare le righe di comando specifiche seguenti per testare il volume G:\\.
   
   `DiskSpd.exe -r -w100 -t8 -o8 -b64K -c100G -d60 -h -L G:\\test\testfile.dat` 
   
   `del G:\\test\testfile.dat`
   
   `DiskSpd.exe -r -w100 -t8 -o8 -b64K -c100G -d300 -h -L G:\\test\testfile.dat`
   
1. Esaminare l'output del secondo test per individuare il numero totale di operazioni di I/O al secondo nella colonna **Operazioni di I/O al secondo**. Nell'esempio seguente il numero totale di operazioni di I/O al secondo è **3929,18**.

   ``` Output
   Total IO
   | thread |  bytes      |  I/Os   |  MB/s  | I/O per s | AvgLat | LatStdDev |
   |--------|-------------|---------|--------|-----------|--------|-----------|
   |   1    |  9651814400 |  147275 |  30.68 |    490.92 | 16.294 | 10.210    |
   |   2    |  9676652544 |  147654 |  30.76 |    492.18 | 16.252 |  9.998    |
   |   3    |  9638248448 |  147068 |  30.64 |    490.23 | 16.317 | 10.295    |
   |   4    |  9686089728 |  147798 |  30.79 |    492.66 | 16.236 | 10.072    |
   |   5    |  9590931456 |  146346 |  30.49 |    487.82 | 16.398 | 10.384    |
   |   6    |  9677242368 |  147663 |  30.76 |    492.21 | 16.251 | 10.067    |
   |   7    |  9637330944 |  147054 |  30.64 |    490.18 | 16.319 | 10.249    |
   |   8    |  9692577792 |  147897 |  30.81 |    492.99 | 16.225 | 10.125    |
   | Total: | 77250887680 | 1178755 | 245.57 |   3929.18 | 16.286 | 10.176    |
   ```

## <a name="example-disk-configurations"></a>Configurazioni del disco di esempio

Le tabelle seguenti illustrano i risultati della procedura di test descritta in [Come misurare le prestazioni del disco](#how-to-measure-disk-performance) con diverse configurazioni lab di test. Usare questi dati come *base* di partenza per la progettazione del sottosistema di archiviazione per un nuovo ambiente. 

### <a name="physical-machines-and-hyper-v"></a>Computer fisici e Hyper-V 
L'hardware è in continuo miglioramento. Prevedere l'uso di hardware di nuova generazione e di diverse combinazioni di hardware, come SSD e SAN, per ottenere prestazioni migliori di quelle indicate di seguito. Questi risultati rappresentano un punto di partenza per la progettazione di un server o per le richieste al fornitore dell'hardware.

La tabella seguente mostra i risultati dei test in diversi sottosistemi del disco, inclusi i dischi rigidi spindle e basati su SSD, in diverse configurazioni lab di test. Tutte le configurazioni formattano i dischi con cluster di 64 KB e li collegano a un controller del disco di classe enterprise. Oltre al numero di dischi della matrice RAID, ogni configurazione include almeno un disco di riserva.

| Tipo di disco   | Numero di dischi, disco di riserva escluso | RAID     | Operazioni di I/O al secondo misurate  |
|------------------|----------------------------------------------------|---------------|---------------|
| SAS 15 KB          | 2                                                  |           1   | 620           |
| SAS 15 KB          | 4                                                  |           10  | 1206          |
| SAS 15 KB          | 6                                                  |           10  | 1751          |
| SAS 15 KB          | 8                                                  |           10  | 2322          |
| SAS 15 KB          | 10                                                 |           10  | 2882          |
| SAS 15 KB          | 12                                                 |           10  | 3476          |
| SAS 15 KB          | 16                                                 |           10  | 4236          |
| SAS 15 KB          | 20                                                 |           10  | 5148          |
| SAS 15 KB          | 30                                                 |           10  | 7398          |
| SAS 15 KB          | 40                                                 |           10  | 9913          |
| SATA SSD         | 2                                                  |           1   | 3300          |
| SATA SSD         | 4                                                  |           10  | 5542          |
| SATA SSD         | 6                                                  |           10  | 7201          |
| SAS SSD          | 2                                                  |           1   | 7539          |
| SAS SSD          | 4                                                  |           10  | 14346         |
| SAS SSD          | 6                                                  |           10  | 15607         |

Di seguito sono elencati i dispositivi usati nell'esempio. Queste informazioni non costituiscono una raccomandazione per tutti i modelli di hardware o i produttori hardware. 

| Tipo di disco    | Modello      | Controller RAID | Memoria cache e configurazione |
|-------------------|-----------------|----------------------|-------------------------------------|
| HD SAS 15 KB RPM    | HP EH0300JDYTH  | Smart Array P822     | 2 GB, 20% in lettura/80% in scrittura           |
| SATA SSD          | ATA MK0200GCTYV | Smart Array P420i    | 1 GB, 20% in lettura/80% in scrittura           |
| SAS SSD           | HP MO0800 JEFPB | Smart Array P420i    | 1 GB, 20% in lettura/80% in scrittura           |

### <a name="azure-machine-and-disk-performance"></a>Computer e prestazioni del disco di Azure 
Le prestazioni del disco di Azure dipendono da diversi fattori, ad esempio dalle dimensioni della macchina virtuale di Azure e dal numero e dal tipo di dischi usati. Azure continua inoltre ad aggiungere nuovi tipi di computer e velocità del disco non incluse nella tabella seguente. Per altre informazioni su Configuration Manager in esecuzione in Azure e informazioni aggiuntive sull'I/O del disco in Azure, vedere le [domande frequenti su Configuration Manager in Azure](../../understand/configuration-manager-on-azure.md).

Tutti i dischi sono formattati in cluster NTFS a 64 KB e le righe con più dischi sono configurate come volumi con striping tramite l'utilità Gestione disco di Windows.

| Macchina virtuale Azure| Disco Azure| Numero di dischi | Spazio disponibile | Operazioni di I/O al secondo misurate   | Fattore di limitazione   |
|--------------------------------------------|-------------------------|---------------------|---------------------------|-------|-----------------|
| **DS2/DS11**                              | P20                     | 1                   | 512 MB                    | 965   | Dimensione della macchina virtuale di Azure   |
| **DS2/DS11**                              | P20                     | 2                   | 1024 MB                   | 996   | Dimensione della macchina virtuale di Azure   |
| **DS2/DS11**                              | P30                     | 1                   | 1024 MB                   | 996   | Dimensione della macchina virtuale di Azure   |
| **DS2/DS11**                              | P30                     | 2                   | 2048 MB                   | 996   | Dimensione della macchina virtuale di Azure   |
| **DS3/DS12/F4S**                          | P20                     | 1                   | 512 MB                    | 1994  | Dimensione della macchina virtuale di Azure   |
| **DS3/DS12/F4S**                          | P20                     | 2                   | 1024 MB                   | 1992  | Dimensione della macchina virtuale di Azure   |
| **DS3/DS12/F4S**                          | P30                     | 1                   | 1024 MB                   | 1993  | Dimensione della macchina virtuale di Azure   |
| **DS3/DS12/F4S**                          | P30                     | 2                   | 2048 MB                   | 1992  | Dimensione della macchina virtuale di Azure   |
| **DS4/DS13/F8S**                          | P20                     | 1                   | 512 MB                    | 2334  | Disco P20        |
| **DS4/DS13/F8S**                          | P20                     | 2                   | 1024 MB                   | 3984  | Dimensione della macchina virtuale di Azure   |
| **DS4/DS13/F8S**                          | P20                     | 3                   | 1536 MB                   | 3984  | Dimensione della macchina virtuale di Azure   |
| **DS4/DS13/F8S**                          | P30                     | 1                   | 1024 MB                   | 3112  | Disco P30        |
| **DS4/DS13/F8S**                          | P30                     | 2                   | 2048 MB                   | 3984  | Dimensione della macchina virtuale di Azure   |
| **DS4/DS13/F8S**                          | P30                     | 3                   | 3072 MB                   | 3996  | Dimensione della macchina virtuale di Azure   |
| **DS5/DS14/F16S**                         | P20                     | 1                   | 512 MB                    | 2335  | Disco P20        |
| **DS5/DS14/F16S**                         | P20                     | 2                   | 1024 MB                   | 4639  | Disco P20        |
| **DS5/DS14/F16S**                         | P20                     | 3                   | 1536 MB                   | 6913  | Disco P20        |
| **DS5/DS14/F16S**                         | P20                     | 4                   | 2048 MB                   | 7966  | Dimensione della macchina virtuale di Azure   |
| **DS5/DS14/F16S**                         | P30                     | 1                   | 1024 MB                   | 3112  | Disco P30        |
| **DS5/DS14/F16S**                         | P30                     | 2                   | 2048 MB                   | 6182  | Disco P30        |
| **DS5/DS14/F16S**                         | P30                     | 3                   | 3072 MB                   | 7963  | Dimensione della macchina virtuale di Azure   |
| **DS5/DS14/F16S**                         | P30                     | 4                   | 4096 MB                   | 7968  | Dimensione della macchina virtuale di Azure   |
| **DS15**                                  | P30                     | 1                   | 1024 MB                   | 3113  | Disco P30        |
| **DS15**                                  | P30                     | 2                   | 2048 MB                   | 6184  | Disco P30        |
| **DS15**                                  | P30                     | 3                   | 3072 MB                   | 9225  | Disco P30        |
| **DS15**                                  | P30                     | 4                   | 4096 MB                   | 10200 | Dimensioni macchina virtuale Azure   |

## <a name="see-also"></a>Vedere anche

- [Domande frequenti sulle dimensioni e le prestazioni del sito](../../understand/site-size-performance-faq.md)
- [Domande frequenti su Configuration Manager in Azure](../../understand/configuration-manager-on-azure.md)
- [Numeri di ridimensionamento e scalabilità](size-and-scale-numbers.md)
- [Recommended hardware](recommended-hardware.md) (Hardware consigliato)

