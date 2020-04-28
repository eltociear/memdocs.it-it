---
title: Domande frequenti su dimensioni e prestazioni del sito
titleSuffix: Configuration Manager
description: Risposte a domande frequenti sulla definizione delle dimensioni e sulle prestazioni in Configuration Manager.
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: conceptual
ms.date: 04/19/2019
ms.openlocfilehash: 3e7b9f6bc861ef5a60e4c0857dc253e3c806a851
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073263"
---
# <a name="configuration-manager-site-sizing-and-performance-faq"></a>Domande frequenti sulla definizione delle dimensioni e sulle prestazioni dei siti di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Questo documento tratta le domande frequenti sulle linee guida relative alle dimensioni del sito di Configuration Manager e su problemi di prestazioni comuni.

## <a name="machine-and-disk-configuration-faqs-and-examples"></a>Domande frequenti sulla configurazione di computer e dischi con esempi

### <a name="how-should-i-format-the-disks-on-my-site-server-and-sql-server"></a>Come formattare i dischi nel server del sito e in SQL Server?

Separare le cartelle posta in arrivo di Configuration Manager e i file SQL collocandoli in almeno due volumi diversi. Questa separazione consente di ottimizzare le dimensioni di allocazione dei cluster per i diversi tipi di operazioni di I/O che eseguono. 

Per il volume che ospita le cartelle posta in arrivo del server del sito, usare NTFS con unità di allocazione da 4 KB o 8 KB. ReFS scrive 64 KB anche per file di piccole dimensioni. Configuration Manager include molti file di piccole dimensioni, pertanto ReFS può generare un overhead non necessario del disco.

Per i dischi contenenti i file di database SQL, usare la formattazione NTFS o ReFS con unità di allocazione da 64 KB.

### <a name="how-and-where-should-i-lay-out-my-sql-database-files"></a>Come e dove disporre i file di database SQL?

Le moderne matrici di unità SSD e Archiviazione Premium di Azure assicurano un numero elevato di operazioni di I/O al secondo in un singolo volume e con un numero limitato di dischi. Si aggiungono, in genere, altre unità a una matrice per ottenere archiviazione aggiuntiva, non per migliorare la velocità effettiva. Se si usano dischi fisici basati su spindle, potrebbe servire un numero più elevato di operazioni di I/O al secondo rispetto a quelle generabili in un singolo volume. È consigliabile allocare il 60% delle operazioni di I/O al secondo e dello spazio su disco totale consigliato al file con estensione *mdf*, il 20% al file con estensione *ldf* e il 20% ai file di log e di dati temporanei. Il file con estensione *ldf* e tutti i file temporanei possono risiedere in un unico volume con il 40%, cioè 20% + 20%, delle operazioni di I/O al secondo allocate.

Le versioni di SQL Server precedenti a SQL Server 2016 creavano per impostazione predefinita un solo file di dati temporanei. È consigliabile tuttavia crearne di più, per evitare blocchi di SQL e attese per accedere all'unico file. Le opinioni della community divergono rispetto al miglior numero di file di dati temporanei da creare, che varia da quattro a otto. I test svolti rivelano che la differenza tra quattro e otto è minima, pertanto è possibile creare quattro file di dati temporanei *delle stesse dimensioni*. I file di dati tempdb devono occupare al massimo il 20-25% delle dimensioni dell'intero database.

### <a name="are-there-any-other-recommendations-for-disk-setup"></a>Ci sono le altre indicazioni per la configurazione dei dischi?

Ove configurabile, impostare la memoria del controller RAID allocandone il 70% alle operazioni di scrittura e il 30% alle operazioni di lettura. Si consiglia di usare, in generale, una configurazione di array RAID 10 per il database del sito. Per i siti di scala ridotta con requisiti I/O contenuti o se si usano unità SSD veloci, è accettabile usare anche RAID 1. Con gli array di dischi più grandi, configurare i dischi di riserva in modo che sostituiscano automaticamente i dischi che hanno generato errori.

**Esempio: Computer fisico con dischi fisici** 

Le [linee guida per dimensioni](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines) per un server del sito e SQL Server con percorso condiviso e **100.000** client sono 1.200 operazioni di I/O al secondo per le cartelle posta in arrivo del server del sito e 5.000 operazioni di I/O al secondo per i file di SQL Server.

La configurazione del disco risultante potrebbe essere simile alla seguente:

| Unità<sup>1</sup> | RAID | Format | Contenuto del volume | N. minimo di operazioni di I/O al secondo richiesto| N. approssimativo di operazioni fornito<sup>2</sup>  |
|----------------|-----------|-------------|----------------------|---------------------|------------------|
| 2x10k          | 1         | -           | Windows              |                     | -                |
| 6x15k          | 10        | NTFS 8k     | Cartelle posta in arrivo di ConfigMgr    |     1700            | 1751             |
| 12x15k         | 10        | 64k ReFS    | File mdf di SQL             | 60%*5000 = 3000     | 3476             |
| 8x15k          | 10        | 64k ReFS    | File ldf di SQL, file temporanei | 40%*5000 = 2000     | 2322             |

1. Non include i dischi di riserva consigliati. 
2. Questo valore proviene da [Configurazioni del disco di esempio](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations). 

### <a name="i-use-hyper-v-on-windows-server-how-should-i-configure-the-disks-for-my-configuration-manager-vms-for-best-performance"></a>Se si usa Hyper-V in Windows Server 2012, in che modo si devono configurare i dischi per le macchine virtuali di Configuration Manager per ottenere prestazioni ottimali?

Hyper-V offre prestazioni simili a quelle di un server fisico, a condizione che le risorse hardware (core della CPU e archiviazione pass-through) siano dedicate al 100% alla macchina virtuale. L'uso di file del disco con estensione *vhd* o *vhdx* di dimensione fissa ha un impatto minimo sulle prestazioni di I/O dell'ordine dell'1-5%. L'uso di file del disco con estensione *vhd* o *vhdx* a espansione dinamica ha un impatto che arriva fino al 25% sulle prestazioni di I/O per il carico di lavoro di Configuration Manager. Se è necessario dotarsi di dischi a espansione dinamica, compensare aggiungendo alla matrice un ulteriore 25% di prestazioni per le operazioni di I/O.

Quando si esegue il server del sito di Configuration Manager o SQL all'interno di una macchina virtuale, isolare le unità del sistema operativo host Hyper-V dalle unità del sistema operativo e dei dati della macchina virtuale.

Per altre informazioni sull'ottimizzazione delle macchine virtuali, vedere [Ottimizzazione delle prestazioni di server Hyper-V](/windows-server/administration/performance-tuning/role/hyper-v-server/).

**Esempio: server del sito basato su macchina virtuale Hyper-V** 

Le [linee guida per dimensioni](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines) per un server del sito e SQL Server con percorso condiviso e **150.000** client sono 1.800 operazioni di I/O al secondo per le cartelle posta in arrivo del server del sito e 7.400 operazioni di I/O al secondo per i file di SQL Server.

La configurazione del disco risultante potrebbe essere simile alla seguente:

| Unità<sup>1</sup> | RAID | Formato<sup>2</sup> | Contenuto del volume | N. minimo di operazioni di I/O al secondo richiesto| N. approssimativo di operazioni fornito<sup>3</sup>  |
|----------------|-----------|----------------|---------------------------|----------------------|------------------|
| 2x10k          | 1         | -              | Sistema operativo host Hyper-V           | -                    | -                |
| 2x10k          | 1         | -              | (VM) Sistema operativo server del sito       | -                    | -                |
| Firma di accesso condiviso 2xSSD      | 1         | NTFS 8k        | (VM) Cartelle posta in arrivo di ConfigMgr    | 1800                 | 7539             |
| Firma di accesso condiviso 4xSSD      | 10        | 64k ReFS       | (VM) SQL host (tutti i file) | 7400                 | 14346            |

1. Non include i dischi di riserva consigliati. 
2. File di dimensioni fisse con estensione *vhdx* pass-through per l'unità della macchina virtuale dedicata al volume sottostante. 
3. Questo valore proviene da [Configurazioni del disco di esempio](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations). 

### <a name="are-there-any-suggestions-for-configuration-manager-environments-in-microsoft-azure"></a>Sono disponibili suggerimenti per gli ambienti di Configuration Manager in Microsoft Azure?

Iniziare leggendo [Configuration Manager in Azure: domande frequenti](configuration-manager-on-azure.md).

Nelle macchine virtuali IaaS di Azure che usano dischi basati su Archiviazione Premium il numero di operazioni di I/O al secondo può essere elevato. In queste macchine virtuali è opportuno configurare dischi aggiuntivi per le esigenze di spazio su disco previste anziché per operazioni di I/O al secondo aggiuntive.

Archiviazione di Azure è intrinsecamente ridondante e non richiede più dischi per la disponibilità. È possibile eseguire lo striping dei dischi in Gestione dischi o Spazi di archiviazione per aumentare lo spazio disponibile e le prestazioni.

Per altre informazioni e consigli su come ottimizzare le prestazioni di Archiviazione Premium ed eseguire SQL Server nelle macchine virtuali IaaS in Azure, vedere:

- [Ottimizzare le prestazioni delle applicazioni](/azure/storage/storage-premium-storage-performance#optimize-application-performance)
 
- [Linee guida per i dischi](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance)

**Esempio: server del sito basato su Azure** 

Le [linee guida per dimensioni](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines) per un server del sito e SQL Server con percorso condiviso e **50.000** client sono otto core, 32 GB e 1.200 operazioni di I/O al secondo per le cartelle posta in arrivo del server del sito e 2.800 operazioni di I/O al secondo per i file di SQL Server.

La macchina di Azure ottenuta potrebbe essere di tipo DS13v2 (8 core, 56 GB) con la configurazione del disco seguente:

| Unità | Format | Contiene | N. minimo di operazioni di I/O al secondo richiesto| N. approssimativo di operazioni fornito<sup>1</sup>  |
|------------------|---------------|--------------------|----------------------|------------------|
| &lt;standard&gt; | -             | Sistema operativo server del sito     | -                    | -                |
| 1xP20 (512 GB)    | NTFS 8k       | Cartelle posta in arrivo di ConfigMgr  | 1200                 | 2334             |
| 1xP30 (1024 GB)   | 64k ReFS      | SQL (tutti i file<sup>2</sup>) | 2800                 | 3112             |

1. Questo valore proviene da [Configurazioni del disco di esempio](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations).
2. Le [linee guida di Azure](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance) consentono di inserire il TempDB nell'unità *D:* locale basata su SSD, a condizione che non superi lo spazio disponibile e consenta la distribuzione aggiuntiva delle operazioni I/O del disco.

**Esempio: server del sito basato su Azure (per l'aumento istantaneo delle prestazioni)** 

La velocità effettiva del disco di Azure è limitata dalle dimensioni della macchina virtuale. La configurazione nell'esempio precedente di Azure potrebbe limitare l'espansione futura o il miglioramento delle prestazioni. Se si aggiungono altri dischi durante la distribuzione iniziale della macchina virtuale di Azure, in futuro sarà possibile effettuare l'upsize della macchina virtuale di Azure per aumentare la potenza di elaborazione, con un investimento iniziale minimo. È molto più semplice pianificare in anticipo l'aumento delle prestazioni del sito in vista di nuovi requisiti che essere costretti a eseguire una migrazione più complessa in un secondo momento.

Modificare i dischi nell'esempio di Azure precedente per vedere come cambia il numero di operazioni di I/O al secondo.

**DS13v2** 

| Unità<sup>1</sup> | Format | Contiene | N. minimo di operazioni di I/O al secondo richiesto| N. approssimativo di operazioni fornito<sup>2</sup>  |
|------------------|---------------|--------------------|----------------------|------------------|
| &lt;standard&gt; | -             | Sistema operativo server del sito     | -                    | -                |
| 2xP20 (1024 GB)   | NTFS 8k       | Cartelle posta in arrivo di ConfigMgr  | 1200                 | 3984             |
| 2xP30 (2048 GB)   | 64k ReFS      | SQL (tutti i file<sup>3</sup>) | 2800                 | 3984             |

1. Lo striping dei dischi viene eseguito usando Spazi di archiviazione.
2. Questo valore proviene da [Configurazioni del disco di esempio](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations). Le dimensioni della macchina virtuale limitano le prestazioni.
3. Le [linee guida di Azure](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance) consentono di inserire il TempDB nell'unità *D:* locale basata su SSD, a condizione che non superi lo spazio disponibile e consenta la distribuzione aggiuntiva delle operazioni I/O del disco.

Se sono necessarie prestazioni superiori in futuro, sarà possibile eseguire l'upsize della macchina virtuale a DS14v2, operazione che raddoppia la CPU e la memoria. La larghezza di banda aggiuntiva del disco consentita da questa dimensione di macchina virtuale, tra l'altro, incrementa immediatamente le operazioni di I/O al secondo disponibili nei dischi configurati in precedenza.

**DS14v2**

| Unità<sup>1</sup> | RAID | Format | Contiene | N. minimo di operazioni di I/O al secondo richiesto| N. approssimativo di operazioni fornito<sup>2</sup>  |
|------------------|---------------|--------------------|----------------------|------------------|
| &lt;standard&gt; | -             | Sistema operativo server del sito     | -                    | -                |
| 2xP20 (1024 GB)   | NTFS 8k       | Cartelle posta in arrivo di ConfigMgr  | 1200                 | 4639             |
| 2xP30 (2048 GB)   | 64k ReFS      | SQL (tutti i file<sup>3</sup>) | 2800                 | 6182             |

1. Lo striping dei dischi viene eseguito usando Spazi di archiviazione.
2. Questo valore proviene da [Configurazioni del disco di esempio](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations). Le dimensioni della macchina virtuale limitano le prestazioni.
3. Le [linee guida di Azure](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance) consentono di inserire il TempDB nell'unità *D:* locale basata su SSD, a condizione che non superi lo spazio disponibile e consenta la distribuzione aggiuntiva delle operazioni I/O del disco.

## <a name="other-common-sql-server-related-performance-questions"></a>Altre domande frequenti sulle prestazioni di SQL Server 

### <a name="is-it-better-to-run-with-sql-colocated-with-the-site-server-or-run-it-on-a-remote-server"></a>È preferibile eseguire SQL Server condividendo il percorso con il server del sito oppure eseguirlo in un server remoto?

Entrambe le modalità assicurano prestazioni adeguate, a condizione che le dimensioni dell'unico server siano appropriate o che la connettività di rete tra i due server sia sufficiente.

L'utilizzo di SQL in remoto comporta l'assunzione dei costi iniziali e operativi di un server aggiuntivo, ma è la scelta comune che opera la maggior parte dei clienti di grosse dimensioni. I vantaggi che offre questa configurazione includono:

- Maggiori opzioni di disponibilità del sito, ad esempio SQL Always On
- Possibilità di eseguire attività di reporting intense con meno overhead di elaborazione per il sito
- Ripristino di emergenza più semplice in alcune situazioni
- Gestione sicurezza più facile
- Separazione dei ruoli per la gestione di SQL, ad esempio con un team DBA separato

SQL con percorso condiviso richiede un unico server ed è la scelta tipica dei clienti di dimensioni più ridotte. I vantaggi che offre questa configurazione includono:

- Minori costi per computer, licenze e manutenzione
- Minor numero di punti di errore nel sito
- Controllo migliore per la pianificazione del tempo di inattività

### <a name="how-much-ram-should-i-allocate-for-sql"></a>Quanta RAM allocare a SQL?

SQL usa, per impostazione predefinita, tutta la memoria disponibile nel server, potenzialmente sottraendo anche quella destinata al sistema operativo e ad altri processi nel computer. Per evitare potenziali problemi di prestazioni, è importante allocare la memoria a SQL in modo esplicito. Nei server del sito che condividono il percorso con SQL Server, verificare che il sistema operativo disponga di RAM sufficiente per la memorizzazione nella cache dei file e altre operazioni. Assicurarsi che rimanga sufficiente memoria RAM per SMSExec e gli altri processi di Configuration Manager. Quando si esegue SQL in un server remoto, è possibile allocare la *maggior parte* della memoria a SQL, ma non tutta. Rivedere le [linee guida per dimensioni](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines) per individuare le indicazioni iniziali. 

La quantità di memoria allocata a SQL Server deve essere arrotondata al GB intero. Man mano che la RAM raggiunge quantità elevate, inoltre, è possibile allocare a SQL una percentuale di memoria più elevata. Quando sono disponibili più di 256 GB di RAM, ad esempio, è possibile allocare a SQL fino al 95% di memoria, perché per il sistema operativo rimane comunque disponibile una notevole quantità di memoria. Il monitoraggio del file di paging è un buon metodo per assicurarsi che ci sia memoria sufficiente per il sistema operativo e i processi di Configuration Manager.

### <a name="cores-are-cheap-these-days-should-i-just-add-a-bunch-of-them-to-my-sql-server"></a>Al giorno d'oggi, i core fisici sono economici. È il caso di aggiungerne alcuni a SQL Server?

Se SQL Server include più di 16 core fisici ma non abbastanza RAM, è possibile che si verifichino problemi di contesa della memoria. Il carico di lavoro di Configuration Manager assicura prestazioni migliori quando per SQL sono disponibili almeno 3 o 4 GB di RAM per core. Quando si aggiungono core a SQL Server, assicurarsi di aumentare la RAM in quantità proporzionale.

### <a name="will-sql-always-on-impact-my-performance"></a>SQL Always On influirà sulle prestazioni?

SQL Always On ha, in generale, un impatto trascurabile sulle prestazioni del sistema se tra i server di replica SQL sono disponibili sufficienti funzionalità di rete. In ambienti SQL Always On affollati è possibile che si verifichi una crescita rapida del log di database, il file con estensione *ldf*. Lo spazio per il file di log viene tuttavia rilasciato automaticamente dopo un backup del database che ha avuto esito positivo. Aggiungere un processo SQL che esegua il backup del database di Configuration Manager, ad esempio ogni 24 ore, e il backup del file con estensione *ldf* ogni sei ore. Per altre informazioni su SQL Always On e Configuration Manager, e altre informazioni sulle strategie di backup di SQL, vedere [SQL Server Always On per un database del sito a disponibilità elevata](../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

### <a name="should-i-enable-sql-compression-on-my-database"></a>È consigliabile abilitare la compressione di SQL nel database?

La compressione di SQL per il database di Configuration Manager non è consigliata. Sebbene l'abilitazione della compressione in un database di Configuration Manager non comporti problemi funzionali, i risultati dei test non indicano una riduzione delle dimensioni tale da giustificare il potenziale considerevole impatto sulle prestazioni del sistema.

### <a name="should-i-enable-sql-encryption-on-my-database"></a>È consigliabile abilitare la crittografia SQL nel database?

Tutti i segreti memorizzati nel database di Configuration Manager sono già archiviati in modo sicuro, ma l'aggiunta della crittografia SQL può determinare un ulteriore livello di sicurezza. L'abilitazione della crittografia nel database non comporta problemi funzionali, ma può verificarsi una riduzione delle prestazioni che può arrivare al 25%, a seconda delle tabelle che si sceglie di crittografare e della versione di SQL che si sta usando. Applicare quindi la crittografia con cautela, soprattutto in ambienti di grandi dimensioni. Ricordare anche di aggiornare i piani di backup e ripristino per assicurarsi che sia possibile ripristinare correttamente i dati crittografati.

### <a name="what-version-of-sql-should-i-run"></a>Quale versione di SQL è consigliabile eseguire?

Per conoscere le versioni supportate di SQL, vedere [Versioni di SQL Server supportate](../plan-design/configs/support-for-sql-server-versions.md). Dal punto di vista delle prestazioni, tutte le versioni di SQL supportate soddisfano i criteri delle prestazioni richiesti. SQL 2012 e SQL 2016, o le versioni successive, tuttavia, tendono ad avere prestazioni migliori di SQL 2014 in alcuni aspetti del carico di lavoro di Configuration Manager. L'esecuzione di SQL 2014 al livello di compatibilità di SQL 2012 (110) migliora, inoltre, le prestazioni complessive. Al momento dell'installazione, i database di Configuration Manager in esecuzione in SQL 2012 e 2014 SQL vengono impostati al livello di compatibilità 110. A partire da SQL 2016 è impostato il livello di compatibilità predefinito per la versione, ad esempio 130 per SQL 2016. L'aggiornamento di SQL sul posto non aggiorna i livelli di compatibilità fino a quando non si installa la successiva versione principale di Configuration Manager Current Branch. 

In caso di lentezza o timeout insoliti durante l'esecuzione di determinate query SQL in SQL 2016 o versione successiva, ad esempio quando si usa il controllo degli accessi in base al ruolo nella Console di amministrazione, provare a impostare su 110 il livello di compatibilità SQL nel database di Configuration Manager. L'esecuzione di SQL 2014 o versione successiva con il livello di compatibilità 110 è completamente supportata. Per altre informazioni, vedere [SQL query timeout o console lenta in determinate query di database di Configuration Manager](https://support.microsoft.com/help/3196320/sql-query-times-out-or-console-slow-on-certain-configuration-manager-d).

A partire da gennaio 2018 si dovrebbero *evitare* le seguenti versioni SQL, a causa di vari problemi relativi alle prestazioni o di altri potenziali problemi noti:

- Da SQL 2012 SP3 CU1 a CU5
- Da SQL 2014 SP1 CU6 a SP2 CU2
- Da SQL 2016 RTM a CU3, da SP1 CU3 a CU5

### <a name="should-i-implement-any-additional-sql-indexing-tasks"></a>È consigliabile implementare ulteriori attività di indicizzazione in SQL?

Sì, aggiornare gli indici una volta alla settimana e le statistiche una volta al giorno per migliorare le prestazioni di SQL. Gli script di terze parti e le informazioni aggiuntive disponibili nelle community di Configuration Manager e SQL consentono di ottimizzare queste attività.

Nei siti di grandi dimensioni alcune tabelle SQL, ad esempio CI\_CurrentComplianceStatusDetails, HinvChangeLog, potrebbero avere dimensioni importanti, a seconda dei modelli di utilizzo. Per questi elementi potrebbe essere necessario ridurre o modificare singolarmente l'approccio alla manutenzione.

### <a name="when-should-i-use-full-sql-server-instead-of-sql-express-on-my-secondary-sites"></a>Quando usare un'installazione completa di SQL Server invece di SQL Express nei siti secondari?

SQL Express non influisce in modo significativo sulle prestazioni nei siti secondari ed è adatto alla maggior parte dei clienti. Poiché è anche facile da distribuire e gestire, è la configurazione consigliata per quasi tutti i clienti di qualsiasi dimensione.

Esiste però una situazione in cui potrebbe essere necessaria un'installazione completa di SQL Server. Se l'ambiente in uso include un numero elevato di punti di distribuzione e pacchetti o origini, è possibile che il limite di dimensione di 10 GB di SQL Express venga superato. Se il numero di pacchetti moltiplicato per il numero di punti di distribuzione supera 4.000.000, ad esempio 2.000 punti di distribuzione per 2.000 parti di contenuto, è consigliabile usare un'installazione completa di SQL Server nei siti secondari. 

### <a name="should-i-change-maxdop-settings-on-my-database"></a>È consigliabile modificare le impostazioni MaxDOP nel database?

Lasciando l'impostazione 0, vale a dire usare tutti i processori disponibili, permette di ottenere prestazioni di elaborazione complessivamente ottimali nella maggior parte dei casi.

Molti amministratori di Configuration Manager seguono le indicazioni di [Consigli e linee guida per l'opzione di configurazione "max degree of parallelism" in SQL Server](https://support.microsoft.com/help/2806535/recommendations-and-guidelines-for-the-max-degree-of-parallelism-confi). Nella maggior parte degli hardware moderni di grandi dimensioni le linee guida suggeriscono un'impostazione massima di 8. Tuttavia, se si eseguono molte query di dimensioni inferiori rispetto al numero di processori, può essere utile impostarla su un numero più alto. Limitarsi a 8 non è necessariamente l'impostazione ottimale nei siti più grandi dove sono disponibili più core. 

Se SQL Server include più di 8 core, iniziare con l'impostazione 0 e modificarla solo se si verificano problemi di prestazioni o blocchi eccessivi. Se è necessario modificare MaxDOP perché si sono verificati problemi di prestazioni con l'impostazione 0, iniziare con un valore che sia maggiore o uguale al numero minimo di core consigliati per la dimensione di SQL Server del sito. La scelta di un numero inferiore a questo ha quasi sempre un effetto negativo sulle prestazioni. Un SQL Server remoto per un sito con 100.000 client, ad esempio, deve avere almeno 12 core. Se SQL Server include 16 core, avviare il test dell'impostazione MaxDOP con il valore 12.

## <a name="other-common-performance-related-questions"></a>Altre domande frequenti relative alle prestazioni

### <a name="which-folders-on-the-site-server-or-other-roles-should-i-exclude-for-antivirus-software"></a>Quali cartelle nel server del sito, o altri ruoli, è consigliabile escludere dal software antivirus?

Decidere di disabilitare la protezione antivirus in qualsiasi sistema prestando attenzione. In ambienti protetti e con volume elevato di attività, si consiglia di disabilitare il *monitoraggio attivo* per ottenere prestazioni ottimali.

Per altre informazioni sulle esclusioni antivirus consigliate, vedere [Recommended antivirus exclusions for Configuration Manager 2012 and Current Branch Site Servers, Site Systems, and Clients](https://support.microsoft.com/help/327453/recommended-antivirus-exclusions-for-configuration-manager-2012-and-cu) (Esclusioni antivirus consigliate per Configuration Manager 2012 e server del sito, sistemi del sito e client Current Branch).

### <a name="what-can-i-do-to-make-wsus-perform-better-when-its-used-with-configuration-manager"></a>Come migliorare le prestazioni di WSUS quando viene usato con Configuration Manager?

La modifica di alcune impostazioni chiave di IIS, come la lunghezza della coda WsusPool e il limite di memoria privata WsusPool, può migliorare le prestazioni di WSUS anche nelle installazioni di dimensioni più ridotte. Per altre informazioni, vedere [Hardware consigliato](../plan-design/configs/recommended-hardware.md).

Assicurarsi anche di aver installato gli ultimi aggiornamenti per il sistema operativo che esegue WSUS:

- Windows Server 2012: qualsiasi aggiornamento cumulativo non "Solo sicurezza" rilasciato da ottobre 2017 in poi. ([KB4041690](https://support.microsoft.com/help/4041690/windows-server-2012-update-kb4041690))
- Windows Server 2012 R2: qualsiasi aggiornamento cumulativo non "Solo sicurezza" rilasciato da agosto 2017 in poi. ([KB4039871](https://support.microsoft.com/help/4039871/windows-8-1-windows-server-2012-r2-update-kb4039871))
- Window Server 2016: qualsiasi aggiornamento cumulativo non "Solo sicurezza" rilasciato da agosto 2017 in poi. ([KB4039396](https://support.microsoft.com/help/4039396/windows-10-update-kb4039396))

### <a name="what-type-of-maintenance-should-i-run-on-my-wsus-servers"></a>Che tipo di manutenzione è necessario eseguire nei server WSUS?

Vedere [The complete guide to Microsoft WSUS and Configuration Manager SUP maintenance](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint) (Guida completa alla manutenzione di Microsoft WSUS e dei punti di aggiornamento software di Configuration Manager).

### <a name="i-want-to-set-up-basic-performance-monitoring-for-my-site-what-should-i-watch"></a>Per configurare il monitoraggio delle prestazioni di base del sito, che cosa è consigliabile controllare?

Il monitoraggio tradizionale delle prestazioni del server funziona in modo efficace per un controllo generale di Configuration Manager. Per monitorare l'integrità di base dei server, è anche possibile usare i vari Management Pack di System Center Operations Manager per Configuration Manager, SQL Server e Windows Server. È anche possibile monitorare direttamente i contatori Monitoraggio prestazioni di Windows (PerfMon) che offre Configuration Manager. Monitorare i backlog nelle varie cartelle posta in arrivo per individuare i primi segnali di potenziali problemi di prestazioni del sito o i backlog.

## <a name="see-also"></a>Vedere anche

- [Linee guida per dimensioni e prestazioni del sito](../plan-design/configs/site-size-performance-guidelines.md)
- [Configuration Manager in Azure: domande frequenti](configuration-manager-on-azure.md)
