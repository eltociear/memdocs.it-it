---
title: Hardware consigliato
titleSuffix: Configuration Manager
description: Ottenere consigli su hardware per ridimensionare l'ambiente di Configuration Manager, oltre una distribuzione di base.
ms.date: 05/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5267f0af-34d3-47a0-9ab8-986c41276e6c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 36b90627f25c5cf19b867a78e141b69266478c58
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83428794"
---
# <a name="recommended-hardware-for-configuration-manager"></a>Hardware consigliato per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

I consigli seguenti sono linee guida che consentono di ridimensionare l'ambiente di Configuration Manager per supportare una distribuzione più avanzata di siti, sistemi del sito e client. Queste linee guida non intendono coprire tutte le possibili configurazioni di siti e gerarchie.  

Usare le informazioni nelle sezioni riportate di seguito per pianificare l'aggiornamento dell'hardware. Assicurarsi che l'hardware possa soddisfare i carichi di elaborazione per i client e i siti che usano le funzionalità di Configuration Manager disponibili.

Per altre informazioni, vedere il [white paper dedicato alle linee guida per le prestazioni e la scalabilità di Configuration Manager](https://gallery.technet.microsoft.com/Configuration-Manager-ba55428e).

## <a name="site-systems"></a><a name="bkmk_ScaleSieSystems"></a> Sistemi del sito

In questa sezione vengono illustrate le configurazioni hardware consigliate per i sistemi del sito di Configuration Manager. Usare questi elementi consigliati per supportare il numero massimo di client e usare la maggior parte o tutte le funzionalità di Configuration Manager. Se l'ambiente supporta meno client del massimo consentito e non usa tutte le funzionalità disponibili, è possibile che richieda meno risorse. In generale i fattori chiave seguenti limitano le prestazioni del sistema complessivo:

1. Prestazioni di I/O su disco

2. Memoria disponibile

3. CPU

Per prestazioni ottimali, usare le configurazioni RAID 10 per tutte le unità dati e una rete Ethernet da 1 Gbps.

### <a name="site-servers"></a><a name="bkmk_ScaleSiteServer"></a> Server del sito

|Configurazione del sito|CPU (core)|Memoria (GB)|Allocazione di memoria per SQL Server (%)|  
|-------------------------------|---------------|---------------|----------------------------------------|  
|Server del sito primario autonomo con un ruolo del sito del database nello stesso server <sup>[Nota 1](#bkmk_note1)</sup>|16|96|80|  
|Server del sito primario autonomo con un database del sito remoto|8|16|-|  
|Server di database remoto per un sito primario autonomo|16|72|90|  
|Server del sito di amministrazione centrale con un ruolo del sito del database nello stesso server <sup>[Nota 1](#bkmk_note1)</sup>|20|128|80|  
|Server del sito di amministrazione centrale con un database del sito remoto|8|16|-|  
|Server di database remoto per un sito di amministrazione centrale|16|96|90|  
|Sito primario figlio con ruolo del sito del database nello stesso server|16|96|80|  
|Server del sito primario figlio con un database del sito remoto|8|16|-|  
|Server di database remoto per un sito primario figlio|16|72|90|  
|Server del sito secondario|8|16|-|  

#### <a name="note-1-collocated-sql"></a><a name="bkmk_note1"></a> Nota 1: posizionamento SQL Server

Quando il server del sito e SQL Server sono installati nello stesso computer, la distribuzione supporta i valori massimi di [dimensionamento](size-and-scale-numbers.md) per siti e client. Questa configurazione può limitare le [opzioni di disponibilità elevata](../../servers/deploy/configure/high-availability-options.md), come ad esempio l'uso di un cluster di SQL Server. Se si ha un ambiente di grandi dimensioni, a causa dei requisiti di I/O più elevati per supportare entrambi i ruoli nello stesso computer, è consigliabile usare SQL Server remoto.

### <a name="remote-site-system-servers"></a><a name="bkmk_RemoteSiteSystem"></a> Server di sistema del sito remoti

Le indicazioni seguenti sono destinate ai computer che contengono un solo ruolo del sistema del sito. Quando si installano più ruoli del sistema del sito nello stesso computer è necessario pianificare delle modifiche.

|Ruolo del sistema del sito|CPU (core)|Memoria (GB)|Spazio su disco (GB)|  
|----------------------|---------------|---------------|--------------------|  
|Punto di gestione|4|8|50|  
|Punto di distribuzione|2|8|Come richiesto dal sistema operativo e per archiviare il contenuto distribuito|  
|Punto di aggiornamento software <sup>[Nota 2](#bkmk_note2)</sup>|8|16|Come richiesto dal sistema operativo e per archiviare gli aggiornamenti distribuiti|  
|Tutti gli altri ruoli del sistema del sito|4|8|50|  

#### <a name="note-2-wsus-configurations"></a><a name="bkmk_note2"></a> Nota 2: Configurazioni WSUS

Il computer che ospita un punto di aggiornamento software richiede le configurazioni seguenti per i pool di applicazioni di IIS:  

- Aumentare la **lunghezza della coda WsusPool** a **2000**.  

- Aumentare il **limite di memoria privata WsusPool** di quattro volte oppure impostarlo su **0** (nessun limite).  

### <a name="disk-space-for-site-systems"></a><a name="bkmk_DiskSpace"></a> Spazio su disco per i sistemi del sito

La configurazione e l'allocazione dei dischi contribuiscono alle prestazioni di Configuration Manager. Dal momento che ogni ambiente di Configuration Manager è diverso, i valori implementati possono variare rispetto alle indicazioni seguenti.

Per ottenere migliori prestazioni, posizionare ogni oggetto in un volume RAID dedicato separato. Per tutti i volumi di dati per Configuration Manager e i relativi file di database, usare RAID 10 per ottimizzare le prestazioni.

|Utilizzo dei dati|Spazio minimo su disco|25.000 client|50.000 client|100.000 client|150.000 client|700.000 client (sito di amministrazione centrale)|  
|----------------|------------------------|--------------------|--------------------|---------------------|---------------------|-----------------------------------------------------|  
|Applicazione e file di log di Configuration Manager|25 GB|50 GB|100 GB|200 GB|300 GB|200 GB|  
|File con estensione MDF del database del sito|75 GB ogni 25.000 client|75 GB|150 GB|300 GB|500 GB|2 TB|  
|File con estensione LDF del database del sito|25 GB ogni 25.000 client|25 GB|50 GB|100 GB|150 GB|100 GB|  
|File di database temporaneo (con estensione MDF e LDF)|Secondo le necessità|Secondo le necessità|Secondo le necessità|Secondo le necessità|Secondo le necessità|Secondo le necessità|  

Per il disco di sistema Windows, vedere le linee guida per il dimensionamento relative alla versione del sistema operativo installata.

Per il contenuto nei punti di distribuzione, tutto dipende dalle distribuzioni: queste linee guida non includono indicazioni relative allo spazio su disco richiesto per la raccolta di contenuti nel server del sito o nei punti di distribuzione. Per altre informazioni, vedere [Raccolta contenuto](../../../core/plan-design/hierarchy/the-content-library.md).

Quando si pianificano i requisiti per lo spazio su disco, tenere presente anche le linee guida seguenti:

- Ogni client richiede circa 5-10 MB di spazio nel database. Questo numero dipende dal tipo di gerarchia, dalla configurazione e dal numero di client. Per ambienti più grandi le dimensioni sono in genere inferiori. I siti più piccoli hanno un maggiore utilizzo del database per ogni client.<!-- SCCMDocs#1048 -->

- Per il database temporaneo, prevedere dimensioni combinate comprese tra il 25% e il 30% del file con estensione mdf del database del sito. Le dimensioni effettive possono essere minori o maggiori, a seconda dalle prestazioni del server del sito e del volume di dati in ingresso durante periodi di tempo lunghi e brevi.

  > [!NOTE]
  > Quando si hanno 50.000 o più client in un sito, prevedere l'uso di quattro o più file con estensione mdf del database temporaneo.

- Le dimensioni del database temporaneo per un sito di amministrazione centrale sono in genere molto inferiori rispetto a quelle di un sito primario.

- Se si usa SQL Server Express per il database del sito secondario, le dimensioni del database sono limitate a 10 GB.

## <a name="clients"></a><a name="bkmk_ScaleClient"></a> Client

Questa sezione illustra le configurazioni hardware consigliate per i computer gestiti con il software client di Configuration Manager.

### <a name="client-for-windows-computers"></a>Client per i computer Windows

Di seguito sono indicati i requisiti hardware minimi per i computer basati su Windows gestiti con Configuration Manager, incluse le edizioni Embedded:

- **Processore e memoria:** fare riferimento ai requisiti per il processore e la RAM per il sistema operativo.

- **Spazio su disco:** 500 MB di spazio disponibile su disco, con 5 GB consigliati per la cache del client di Configuration Manager. Se si usano le impostazioni personalizzate per installare il client di Configuration Manager, è necessario meno spazio.

  - Usare la proprietà client.msi **SMSCACHESIZE** per impostare dimensioni di cache inferiori a quelle predefinite di 5120 MB. La dimensione minima è 1 MB. L'esempio seguente crea una cache di 2 MB: `CCMSetup.exe SMSCACHESIZE=2`

    Per altre informazioni, vedere [Proprietà di installazione client](../../../core/clients/deploy/about-client-installation-properties.md).

    > [!TIP]
    > L'installazione del client con lo spazio minimo su disco è utile per i dispositivi Windows Embedded, che in genere hanno dimensioni di disco inferiori a quelle dei computer Windows standard.

Di seguito sono indicati altri requisiti hardware minimi per la funzionalità facoltativa in Configuration Manager:

- **Distribuzione del sistema operativo:** almeno 384 MB di RAM

- **Software Center:** almeno un processore a 500 MHz

- **Controllo remoto**: per un'esperienza ottimizzata, almeno Pentium 4 Hyper-Threaded 3 GHz (core singolo) o CPU comparabile, con almeno un 1 GB di RAM.

### <a name="client-for-linux-and-unix"></a>Client per Linux e UNIX

Di seguito sono indicati i requisiti minimi per i server Linux e UNIX gestiti con Configuration Manager.

|Requisito|Dettagli|  
|-----------------|-------------|  
|Processore e memoria|Fare riferimento ai requisiti per processore e RAM per il sistema operativo del computer.|  
|Spazio su disco|500 MB di spazio disponibile su disco, con 5 GB consigliati per la cache del client di Configuration Manager.|  
|Connettività di rete|I computer client di Configuration Manager devono avere una connettività di rete con i sistemi del sito di Configuration Manager per abilitare la gestione.|  

## <a name="configuration-manager-console"></a><a name="bkmk_ScaleConsole"></a> Console di Configuration Manager

I requisiti hardware minimi riportati di seguito si applicano a ogni computer che esegue la console di Configuration Manager:

- Intel i3 o CPU comparabile  

- 2 GB di RAM  

- 2 GB di spazio su disco  

|Impostazione DPI|Risoluzione minima|  
|-----------------|------------------------|  
|96/100%|1024 x 768|  
|120/125%|1280 x 960|  
|144/150%|1600 x 1200|  
|196/200%|2500 x 1600|  

## <a name="lab-deployments"></a><a name="bkmk_ScaleLab"></a> Distribuzioni di lab

Seguire questi consigli in termini di requisiti hardware minimi per le distribuzioni di lab e di prova di Configuration Manager. Questi consigli si applicano a tutti i tipi di sito, fino a un massimo di 100 client:  

|Ruolo|CPU (core)|Memoria (GB)|Spazio su disco (GB)|  
|----------|---------------|-------------------|-----------------------|  
|Server del sito e di database|2 - 4|8 - 12|100|  
|Server del sistema del sito|1 - 4|2 - 4|50|  
|Client|1 - 2|1 - 3|30|  
