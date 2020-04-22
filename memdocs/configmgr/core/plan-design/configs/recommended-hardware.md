---
title: Hardware consigliato
titleSuffix: Configuration Manager
description: Ottenere consigli su hardware per ridimensionare l'ambiente di Configuration Manager, oltre una distribuzione di base.
ms.date: 05/23/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5267f0af-34d3-47a0-9ab8-986c41276e6c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d741e34325da859d4fe1f0af554544ce146a42f9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702119"
---
# <a name="recommended-hardware-for-configuration-manager"></a>Hardware consigliato per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

I consigli seguenti sono linee guida che consentono di ridimensionare l'ambiente di Configuration Manager per supportare una distribuzione più avanzata di siti, sistemi del sito e client. Queste raccomandazioni non intendono coprire tutte le possibili configurazioni di siti e gerarchie.  

Usare le informazioni delle sezioni seguenti come guida per la pianificazione dell'hardware che può soddisfare i carichi di elaborazione per i client e i siti che usano le funzionalità di Configuration Manager disponibili con le configurazioni predefinite.  



##  <a name="site-systems"></a><a name="bkmk_ScaleSieSystems"></a> Sistemi del sito  
Questa sezione illustra le configurazioni hardware consigliate per i sistemi del sito di Configuration Manager per le distribuzioni che supportano il numero massimo di client e usano la maggior parte o tutte le funzionalità di Configuration Manager. Le distribuzioni che supportano meno del numero massimo di client e che non usano tutte le funzionalità disponibili possono richiedere meno risorse del computer. In generale, i fattori chiave che limitano le prestazioni dell'intero sistema includono i seguenti, nell'ordine:  

1.  Prestazioni di I/O su disco  

2.  Memoria disponibile  

3.  CPU  

Per prestazioni ottimali, usare le configurazioni RAID 10 per tutte le unità dati e una rete Ethernet da 1 Gbps.  

###  <a name="site-servers"></a><a name="bkmk_ScaleSiteServer"></a> Server del sito  

|Configurazione del sito|CPU (core)|Memoria (GB)|Allocazione di memoria per SQL Server (%)|  
|-------------------------------|---------------|---------------|----------------------------------------|  
|Server del sito primario autonomo con un ruolo del sito del database nello stesso server<sup>1</sup>|16|96|80|  
|Server del sito primario autonomo con un database del sito remoto|8|16|-|  
|Server di database remoto per un sito primario autonomo|16|72|90|  
|Server del sito di amministrazione centrale con un ruolo del sito del database nello stesso server<sup>1</sup>|20|128|80|  
|Server del sito di amministrazione centrale con un database del sito remoto|8|16|-|  
|Server di database remoto per un sito di amministrazione centrale|16|96|90|  
|Sito primario figlio con ruolo del sito del database nello stesso server|16|96|80|  
|Server del sito primario figlio con un database del sito remoto|8|16|-|  
|Server di database remoto per un sito primario figlio|16|72|90|  
|Server del sito secondario|8|16|-|  

<sup>1</sup> Quando il server del sito e SQL Server sono installati nello stesso computer, la distribuzione supporta i valori massimi di [ridimensionamento](size-and-scale-numbers.md) per siti e client. Questa configurazione può però limitare le [opzioni di disponibilità elevata per Configuration Manager](../../servers/deploy/configure/high-availability-options.md) come l'uso di un cluster di SQL Server. A causa dei più elevati requisiti di I/O necessari per supportare SQL Server e il server del sito di Configuration Manager durante l'esecuzione di entrambi i server nello stesso computer, si consiglia ai clienti con grandi distribuzioni di usare una configurazione con un computer SQL Server remoto.  

###  <a name="remote-site-system-servers"></a><a name="bkmk_RemoteSiteSystem"></a> Server di sistema del sito remoti  
Le indicazioni seguenti sono destinate ai computer che contengono un solo ruolo del sistema del sito. Pianificare delle modifiche quando si installano più ruoli del sistema del sito nello stesso computer.  

|Ruolo del sistema del sito|CPU (core)|Memoria (GB)|Spazio su disco (GB)|  
|----------------------|---------------|---------------|--------------------|  
|Punto di gestione|4|8|50|  
|Punto di distribuzione|2|8|Come richiesto dal sistema operativo e per archiviare il contenuto distribuito|  
|Punto di aggiornamento software<sup>1</sup>|8|16|Come richiesto dal sistema operativo e per archiviare gli aggiornamenti distribuiti|  
|Tutti gli altri ruoli del sistema del sito|4|8|50|  

<sup>1</sup> Il computer che ospita un punto di aggiornamento software richiede le configurazioni seguenti per i pool di applicazioni di IIS:  

- Aumentare la **lunghezza della coda WsusPool** a **2000**.  

- Aumentare il **limite di memoria privata WsusPool** di quattro volte oppure impostarlo su **0** (nessun limite).  

###  <a name="disk-space-for-site-systems"></a><a name="bkmk_DiskSpace"></a> Spazio su disco per i sistemi del sito  
La configurazione e l'allocazione dei dischi contribuisce alle prestazioni di Configuration Manager. Dal momento che ogni ambiente di Configuration Manager è diverso, i valori implementati possono variare rispetto alle indicazioni seguenti.  

Per ottenere migliori prestazioni, posizionare ogni oggetto in un volume RAID dedicato separato. Per tutti i volumi di dati (Configuration Manager e relativi file di database), usare RAID 10 per ottenere le migliori prestazioni.  

|Utilizzo dei dati|Spazio minimo su disco|25.000 client|50.000 client|100.000 client|150.000 client|700.000 client (sito di amministrazione centrale)|  
|----------------|------------------------|--------------------|--------------------|---------------------|---------------------|-----------------------------------------------------|  
|Sistema operativo|Consultare le informazioni disponibili per il sistema operativo.|Consultare le informazioni disponibili per il sistema operativo.|Consultare le informazioni disponibili per il sistema operativo.|Consultare le informazioni disponibili per il sistema operativo.|Consultare le informazioni disponibili per il sistema operativo.|Consultare le informazioni disponibili per il sistema operativo.|  
|Applicazione e file di log di Configuration Manager|25 GB|50 GB|100 GB|200 GB|300 GB|200 GB|  
|File con estensione MDF del database del sito|75 GB ogni 25.000 client|75 GB|150 GB|300 GB|500 GB|2 TB|  
|File con estensione LDF del database del sito|25 GB ogni 25.000 client|25 GB|50 GB|100 GB|150 GB|100 GB|  
|File di database temporaneo (con estensione MDF e LDF)|Secondo le necessità|Secondo le necessità|Secondo le necessità|Secondo le necessità|Secondo le necessità|Secondo le necessità|  
|Contenuto (condivisioni del punto di distribuzione)|Secondo le necessità<sup>1</sup>|Secondo le necessità<sup>1</sup>|Secondo le necessità<sup>1</sup>|Secondo le necessità<sup>1</sup>|Secondo le necessità<sup>1</sup>|Secondo le necessità<sup>1</sup>|  

<sup>1</sup> Le indicazioni relative allo spazio su disco non includono lo spazio richiesto per il contenuto che si trova nella raccolta contenuto nel server del sito o nel punto di distribuzione. Per informazioni sulla pianificazione della raccolta contenuto, vedere [Raccolta contenuto](../../../core/plan-design/hierarchy/the-content-library.md).  

Oltre alle informazioni aggiuntive precedenti, prendere in considerazione le linee guida seguenti quando si pianificano i requisiti per lo spazio su disco:  

- Ogni client richiede circa 5 MB di spazio.  

- Durante la pianificazione della dimensione del database temporaneo per un sito primario, prevedere una dimensione combinata compresa tra il 25% e il 30% del file con estensione MDF del database del sito. Le dimensioni effettive possono essere sensibilmente inferiori o superiori, a seconda dalle prestazioni del server del sito e del volume di dati in ingresso durante periodi di tempo lunghi e brevi.  

  > [!NOTE]  
  >  Quando sono disponibili 50.000 o più client in un sito, prevedere l'uso di quattro o più file mdf del database temporaneo.  

- Le dimensioni del database temporaneo per un sito di amministrazione centrale sono in genere molto inferiori rispetto a quelle di un sito primario.  

- Le dimensioni del database del sito secondario hanno le limitazioni seguenti:  

  - SQL Server 2012 Express: 10 GB  

  - SQL Server 2014 Express: 10 GB  

##  <a name="clients"></a><a name="bkmk_ScaleClient"></a> Client  
Questa sezione illustra le configurazioni hardware consigliate per i computer gestiti con il software client di Configuration Manager.  

### <a name="client-for-windows-computers"></a>Client per i computer Windows  
Di seguito sono indicati i requisiti hardware minimi per i computer basati su Windows gestiti con Configuration Manager, inclusi i sistemi operativi Embedded:  

- **Processore e memoria:** fare riferimento ai requisiti per il processore e la RAM specifici del sistema operativo del computer.  

- **Spazio su disco:** 500 MB di spazio disponibile su disco, con 5 GB consigliati per la cache del client di Configuration Manager. Se si usano le impostazioni personalizzate per installare il client di Configuration Manager, è necessario meno spazio:  

    - Usare la proprietà Client. msi SMSCACHESIZE per impostare un file di cache inferiore a quello predefinito di 5120 MB. La dimensione minima è 1 MB. Ad esempio, `CCMSetup.exe SMSCachesize=2` crea una cache di 2 MB.  

    Per altre informazioni su queste impostazioni di installazione del client, vedere [Informazioni sulle proprietà di installazione del client](../../../core/clients/deploy/about-client-installation-properties.md).  

    > [!TIP]  
    > L'installazione del client con lo spazio minimo su disco è utile per i dispositivi Windows Embedded, che in genere hanno dimensioni di disco inferiori a quelle dei computer Windows standard.  

Di seguito sono indicati altri requisiti hardware minimi per la funzionalità facoltativa in Configuration Manager.  

- **Distribuzione del sistema operativo:** 384 MB di RAM  

- **Software Center:** Processore da 500 MHz  

- **Controllo remoto**: Pentium 4 Hyper-Threaded 3 GHz (core singolo) o CPU comparabile, con almeno un 1 GB di RAM per un'esperienza ottimale  

### <a name="client-for-linux-and-unix"></a>Client per Linux e UNIX  
Di seguito sono indicati i requisiti minimi per i server Linux e UNIX gestiti con Configuration Manager.  

|Requisito|Dettagli|  
|-----------------|-------------|  
|Processore e memoria|Consultare i requisiti per il processore e la RAM specifici del sistema operativo del computer.|  
|Spazio su disco|500 MB di spazio disponibile su disco, con 5 GB consigliati per la cache del client di Configuration Manager.|  
|Connettività di rete|I computer client di Configuration Manager devono avere una connettività di rete con i sistemi del sito di Configuration Manager per abilitare la gestione.|  

##  <a name="configuration-manager-console"></a><a name="bkmk_ScaleConsole"></a> Console di Configuration Manager  
I requisiti riportati nella tabella seguente si applicano a ogni computer che esegue la console di Configuration Manager.  

**Configurazione hardware minima:**  

- Intel i3 o CPU comparabile  

- 2 GB di RAM  

- 2 GB di spazio su disco  

|Impostazione DPI|Risoluzione minima|  
|-----------------|------------------------|  
|96/100%|1024 x 768|  
|120/125%|1280 x 960|  
|144/150%|1600 x 1200|  
|196/200%|2500 x 1600|  

**Supporto per PowerShell:**  

Quando si installa il supporto per PowerShell in un computer che esegue la console di Configuration Manager, è possibile eseguire i cmdlet di PowerShell in tale computer per gestire Configuration Manager.

- È supportato PowerShell 3.0 o versione successiva

Oltre a PowerShell, è supportato anche Windows Management Framework (WMF) 3.0 o versione successiva.   


##  <a name="lab-deployments"></a><a name="bkmk_ScaleLab"></a> Distribuzioni di lab  
Seguire questi consigli in termini di requisiti hardware minimi per le distribuzioni di lab e di prova di Configuration Manager. Questi consigli si applicano a tutti i tipi di sito, fino a un massimo di 100 client:  

|Ruolo|CPU (core)|Memoria (GB)|Spazio su disco (GB)|  
|----------|---------------|-------------------|-----------------------|  
|Server del sito e di database|2 - 4|8 - 12|100|  
|Server del sistema del sito|1 - 4|2 - 4|50|  
|Client|1 - 2|1 - 3|30|  
