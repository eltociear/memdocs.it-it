---
title: 'Configurazioni supportate per LTSB '
titleSuffix: Configuration Manager
description: Funzionamento di sistemi operativi e prodotti dipendenti con Long-Term Servicing Branch di System Center Configuration Manager.
ms.date: 05/10/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f0f818d4-7f45-402f-8758-dc88bc024953
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b72e0a14abd2b468056d4303497625633b8f64a8
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88698923"
---
# <a name="supported-configurations-for-the-long-term-servicing-branch-of-system-center-configuration-manager"></a>Configurazioni supportate per Long-Term Servicing Branch di System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Long-Term Servicing Branch)*

Questo argomento illustra i sistemi operativi e le dipendenze dei prodotti supportate per Long-Term Servicing Branch (LTSB) di Configuration Manager.
Se non specificato diversamente in questo o negli argomenti specifici per LTSB, le stesse configurazioni e limitazioni che si applicano alla versione 1606 Current Branch riguardano anche LTSB.  Quando si verificano conflitti, usare le informazioni pertinenti all'edizione in uso. In genere, LTSB è più limitato rispetto a Current Branch.

## <a name="general-statement-of-support"></a>Descrizione generale del supporto
I prodotti e tecnologie seguenti sono supportati da questo ramo di Configuration Manager. Il loro inserimento in questo contesto, tuttavia, non implica un'estensione del normale ciclo di vita del supporto per un singolo prodotto o versione. I prodotti che non rientrano nel ciclo di vita del supporto non sono supportati per l'uso con Configuration Manager. Per altre informazioni, visitare il sito Web del [ciclo di vita del supporto Microsoft](https://support.microsoft.com/lifecycle) e leggere le Domande frequenti corrispondenti.

I prodotti e le versioni di prodotto non elencati negli argomenti seguenti non sono supportati a meno che non siano annunciati nel blog [Enterprise Mobility and Security Blog](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/bg-p/enterprisemobilityandsecurity).

**Limitazioni per il supporto futuro:** LTSB ha un supporto limitato per sistemi operativi client e server futuri e per le dipendenze dei prodotti. L'elenco delle piattaforme per LTSB è fisso per tutta la durata della versione:

**Windows:**
- Per Windows sono supportati solo gli aggiornamenti di sicurezza e qualitativi.
- Non viene aggiunto alcun supporto per Current Branch (CB), Current Branch for Business (CBB) o LTSB di Windows 10.
- Nessun supporto per nuove versioni principali di Windows Server.

**SQL Server:**
- Per SQL Server sono supportati solo gli aggiornamenti di sicurezza e qualitativi o aggiornamenti secondari come i Service Pack.
- Nessun supporto per nuove versioni principali di SQL Server.  

## <a name="site-systems-and-servers"></a>Server e sistemi del sito
LTSB supporta l'uso dei seguenti sistemi operativi di computer Windows come sistemi del sito.  Ogni sistema operativo ha gli stessi requisiti e le stesse limitazioni inclusi in [Sistemi operativi supportati per i server del sistema del sito di System Center Configuration Manager](../plan-design/configs/supported-operating-systems-for-site-system-servers.md).  Ad esempio, l'installazione Server Core di Windows 2012 R2 deve avere una versione x64, è supportata solo per ospitare un punto di distribuzione e non supporta PXE o il multicast.

**Sistemi operativi supportati:**
- Windows Server 2016
- Windows Server 2012 R2 (x64): Standard, Datacenter
- Windows Server 2012 (x64): Standard, Datacenter
- Windows 10 Enterprise 2015 LTSB (x86, x64)
- Windows 10 Enterprise 2016 LTSB (x86, x64)
- Windows 8.1 (x86, x64): Professional, Enterprise
- Installazione Server Core di Windows Server 2012
- Installazione Server Core di Windows Server 2012 R2

## <a name="client-management"></a>Gestione dei client
Le sezioni seguenti identificano i sistemi operativi client che è possibile gestire con LTSB. LTSB non supporta l'aggiunta di nuovi sistemi operativi come client supportati.

### <a name="windows-computers"></a>Computer Windows
È possibile usare LTSB per gestire i seguenti sistemi operativi di computer Windows con il software client di Configuration Manager incluso in Configuration Manager. Per altre informazioni, vedere [Come distribuire i client nei computer Windows](../clients/deploy/deploy-clients-to-windows-computers.md).

**Sistemi operativi supportati:**
- Windows Server 2016
- Windows Server 2012 R2 (x64): Standard, Datacenter (Nota 1)
- Windows Server 2012 (x64): Standard, Datacenter (Nota 1)
- Windows Storage Server 2012 R2 (x64)
- Windows Storage Server 2012 (x64)
- Windows 10 Enterprise 2015 LTSB (x86, x64)
- Windows 10 Enterprise 2016 LTSB (x86, x64)
- Windows 8.1 (x86, x64): Professional, Enterprise
- Installazione Server Core di Windows Server 2012 R2 (x64) (Nota 2)
- Installazione Server Core di Windows Server 2012 (x64) (Nota 2)

**(Nota 1)** Le versioni Datacenter sono supportate, ma non certificate per Configuration Manager.  
**(Nota 2)** Per supportare l'installazione push client, il computer che esegue questa versione del sistema operativo deve eseguire il servizio ruolo file server per il ruolo del server Servizi file e archiviazione. Per informazioni sull'installazione di funzionalità di Windows in un computer Server Core, vedere [Installare i ruoli e le funzionalità server in un server Server Core](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj574158(v=ws.11)).

### <a name="windows-embedded"></a>Windows Embedded
È possibile gestire i dispositivi Windows Embedded seguenti con LTSB installando il software client nel dispositivo.  Per altre informazioni, vedere [Pianificazione della distribuzione del client in dispositivi con Windows Embedded](../clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).

**Requisiti e limitazioni:**  

-   Tutte le funzionalità client sono supportate nei sistemi Windows Embedded supportati in cui non sono abilitati filtri di scrittura.  

-   I client che usano uno dei tipi di filtro seguenti sono supportati per tutte le funzionalità tranne che per il risparmio energia:  

    -   Filtri di scrittura avanzati    

    -   Filtri di scrittura basati su file RAM    

    -   Filtri di scrittura unificati  

-   Il Catalogo applicazioni non è supportato per alcun dispositivo Windows Embedded.  

-   Prima di poter monitorare malware rilevati nei dispositivi Windows Embedded basati su Windows XP, è necessario installare il pacchetto di scripting WMI di Microsoft Windows nel dispositivo incorporato. Usare Windows Embedded Target Designer per installare questo pacchetto. I file *WBEMDISP.DLL* e *WBEMDISP.TLB* devono essere presenti e registrati nella cartella %windir%\System32\WBEM del dispositivo integrato per garantire la segnalazione del malware rilevato.  

**Sistemi operativi supportati:**  
-   Windows 10 Enterprise 2016 LTSB (x86, x64)  
-   Windows 10 Enterprise 2015 LTSB (x86, x64)  
-   Windows Embedded 8.1 Industry (x86, x64)    
-   Windows Thin PC (x86, x64)    
-   Windows Embedded POSReady 7 (x86, x64)    
-   Windows Embedded Standard 7 con SP1 (x86, x64)    
-   Windows Embedded POSReady 2009 (x86)   
-   Windows Embedded Standard 2009 (x86)  

### <a name="windows-ce"></a>Windows CE  
 È possibile gestire i dispositivi Windows CE con il client legacy del dispositivo mobile di Configuration Manager incluso in Configuration Manager.  

**Requisiti e limitazioni:**  

-   Il client del dispositivo mobile richiede 0,78 MB di spazio di archiviazione per l'installazione. Un dispositivo mobile può richiedere fino a 256 KB di spazio di archiviazione aggiuntivo per eseguire l'accesso.    

-   Le funzionalità per questi dispositivi mobili variano a seconda della piattaforma e del tipo di client. Per informazioni sul tipo di funzioni di gestione che Configuration Manager supporta per un client legacy del dispositivo mobile, vedere [Scegliere una soluzione di gestione dei dispositivi per Configuration Manager](../plan-design/choose-a-device-management-solution.md).  

**Sistemi operativi supportati:**  

-   Windows CE 7.0 (processori ARM e x86)  

**Le lingue supportate includono:**  
-   Cinese (semplificato e tradizionale)    
-   Inglese (Stati Uniti)    
-   Francese (Francia)    
-   Tedesco    
-   Italiano    
-   Giapponese  
-   Coreano  
-   Portoghese (Brasile)  
-   Russo  
-   Spagnolo (Spagna)  

### <a name="mac-computers"></a>Computer Mac  
 È possibile usare LTSB per gestire i computer Mac OS X con il client di Configuration Manager per Mac.

Il pacchetto di installazione del client per Mac non viene fornito con i supporti di Configuration Manager. È possibile scaricarlo come parte del download dei Client per sistemi operativi aggiuntivi nell'[Area download Microsoft](https://www.microsoft.com/download/details.aspx?id=47719).  

Il supporto per i sistemi operativi Mac è limitato a quelli elencati in questa sezione. Il supporto non include sistemi operativi aggiuntivi che potrebbero essere supportati da un aggiornamento futuro a pacchetti di installazione client Mac per Current Branch.

Per altre informazioni, vedere [Come distribuire i client in computer Mac](../clients/deploy/deploy-clients-to-macs.md).

**Versioni supportate:**  
-   Mac OS X 10.9 (Mavericks)  
-   Mac OS X 10.10 (Yosemite)  
-   Mac OS X 10.11 (El Capitan)  

## <a name="linux-and-unix-servers"></a>Server Linux e UNIX
È possibile usare LTSB per gestire i server Linux e UNIX con client di Configuration Manager per Linux e UNIX.

I pacchetti di installazione del client per Linux e UNIX non sono inclusi con i supporti di Configuration Manager. È possibile scaricarli come parte del download dei Client per sistemi operativi aggiuntivi nell'[Area download Microsoft](https://www.microsoft.com/download/details.aspx?id=47719). Oltre ai pacchetti di installazione client, il download del client include lo script di installazione che gestisce l'installazione del client in ogni computer.

Il supporto per i sistemi operativi Linux e UNIX è limitato a quelli elencati in questa sezione. Il supporto non include sistemi operativi aggiuntivi che potrebbero essere supportati da un aggiornamento futuro a pacchetti client Linux e UNIX per Current Branch.

**Requisiti e limitazioni:**  

-   Per informazioni dettagliate sulle dipendenze del file del sistema operativo per il client per Linux e UNIX, vedere [Prerequisites for Client Deployment to Linux and UNIX Servers](../clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_ClientDeployPrereqforLnU) (Prerequisiti per la distribuzione client a server Linux e UNIX).  
-   Per una panoramica delle funzionalità di gestione supportate per i computer che eseguono Linux o UNIX, vedere [Come distribuire i client a server UNIX e Linux](../clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  
-   Per le versioni supportate di Linux e UNIX, la versione indicata include tutte le versioni secondarie successive. Ad esempio, se la tabella indica il supporto per CentOS versione 6, questo supporto include anche tutte le versioni secondarie successive di CentOS 6, come CentOS 6.3. Analogamente, se la tabella indica il supporto per un sistema operativo che usa Service Pack, ad esempio SUSE Linux Enterprise Server 11 SP1, il supporto include i Service Pack successivi per questo sistema operativo.
-   Per informazioni sui pacchetti di installazione client e su Universal Agent, vedere [Come distribuire i client nei server UNIX e Linux](../clients/deploy/deploy-clients-to-unix-and-linux-servers.md).


**Versioni supportate:**    
Le versioni seguenti sono supportate tramite l'uso del file TAR indicato.  
### <a name="aix"></a>AIX  

|Version|File|  
|-|-|  
|Versione 5.3 (Power)|ccm-Aix53ppc.&lt;build\>.tar|  
|Version 6.1 (Power)|ccm-Aix61ppc.&lt;build\>.tar|  
|Versione 7.1 (Power)|ccm-Aix71ppc.&lt;build\>.tar|  

### <a name="centos"></a>CentOS  

|Version|File|  
|-|-|  
|Versione 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 7 x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="debian"></a>Debian  

|Version|File|    
|-|-|  
|Versione 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 7 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 7 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 8 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 8 x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="hp-ux"></a>HP-UX  

|Version|File|  
|-|-|  
|Version 11iv2 IA64|ccm-HpuxB.11.23i64.&lt;build\>.tar|  
|Versione 11iv2 PA-RISC|ccm-HpuxB.11.23PA.&lt;build\>.tar|  
|Version 11iv3 IA64|ccm-HpuxB.11.31i64.&lt;build\>.tar|  
|Versione 11iv3 PA-RISC|ccm-HpuxB.11.31PA.&lt;build\>.tar|  

### <a name="oracle-linux"></a>Oracle Linux  

|Version|File|    
|-|-|  
|Versione 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 7 x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="red-hat-enterprise-linux-rhel"></a>Red Hat Enterprise Linux (RHEL)  

|Version|File|  
|-|-|  
|Versione 4 x86|ccm-RHEL4x86.&lt;build\>.tar|  
|Versione 4 x64|ccm-RHEL4x64.&lt;build\>.tar|  
|Versione 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 7 x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="solaris"></a>Solaris  

|Version|File|   
|-|-|  
|Versione 9 SPARC|ccm-Sol9sparc.&lt;build\>.tar|  
|Versione 10 x86|ccm-Sol10x86.&lt;build\>.tar|  
|Version 10 SPARC|ccm-Sol10sparc.&lt;build\>.tar|  
|Versione 11 x86|ccm-Sol11x86.&lt;build\>.tar|  
|Versione 11 SPARC|ccm-Sol11sparc.&lt;build\>.tar|  

### <a name="suse-linux-enterprise-server-sles"></a>SUSE Linux Enterprise Server (SLES)  

|Version|File|  
|-|-|  
|Versione 9 x86|ccm-SLES9x86.&lt;build\>.tar|  
|Versione 10 SP1 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 10 SP1 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 11 SP1 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 11 SP1 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 12 x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="ubuntu"></a>Ubuntu  

|Version|File|    
|-|-|  
|Versione 10.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 10.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 12.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 12.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 14.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 14.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="exchange-server-connector"></a>Connettore Exchange Server
 LTSB supporta la gestione limitata dei dispositivi che si connettono all'istanza di Exchange Server, senza installare software client. Per altre informazioni, vedere [Gestire i dispositivi mobili con Configuration Manager ed Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).

 **Requisiti e limitazioni:**  

-   Configuration Manager offre funzionalità di gestione limitate per i dispositivi mobili. La gestione limitata è disponibile quando si usa il connettore Exchange Server per dispositivi Exchange Active Sync (EAS) che si connettono a un server che esegue Exchange Server o Exchange Online.  

-   Per altre informazioni sulle funzioni di gestione supportate da Configuration Manager per i dispositivi mobili gestiti dal connettore Exchange Server, vedere [Scegliere una soluzione di gestione dei dispositivi per Configuration Manager](../plan-design/choose-a-device-management-solution.md).  

**Versioni di Exchange Server supportate:**  
-   Exchange Server 2010 SP1  
-   Exchange Server 2010 SP2  
-   Exchange Server 2013  

> [!NOTE]
> LTSB non supporta la gestione dei dispositivi che si connettono tramite un servizio online, ad esempio Exchange Online (Office 365).


## <a name="configuration-manager-console"></a>Console di Configuration Manager
LTSB supporta i sistemi operativi seguenti per eseguire la console di Configuration Manager. Ogni computer che ospita la console deve avere almeno la versione di .NET Framework 4.5.2, ad eccezione di Windows 10, che richiede almeno .NET Framework 4.6.

**Sistemi operativi supportati:**
- Windows Server 2016
- Windows Server 2012 R2 (x64): Standard, Datacenter
- Windows Server 2012 (x64): Standard, Datacenter
- Windows 10 Enterprise 2016 LTSB (x86, x64)
- Windows 10 Enterprise 2015 LTSB (x86, x64)
- Windows 8.1 (x86, x64): Professional, Enterprise


## <a name="sql-server-versions-supported-for-the-site-database-and-reporting-point"></a>Versioni di SQL Server supportate per il database del sito e il punto di reporting
LTSB supporta le versioni seguenti di SQL Server per ospitare il database del sito e punto di reporting. Per ogni versione supportata, gli stessi requisiti di configurazione e le stesse limitazioni visualizzati in [Supporto per le versioni di SQL Server per System Center Configuration Manager](../plan-design/configs/support-for-sql-server-versions.md) per Current Branch si applicano anche a LTSB.  È incluso anche l'uso di un cluster SQL Server o di un gruppo di disponibilità SQL Server AlwaysOn.  

**Versioni supportate:**

- SQL Server 2016: Standard, Enterprise
- SQL Server 2014 SP2: Standard, Enterprise
- SQL Server 2014 SP1: Standard, Enterprise
- SQL Server 2012 SP3: Standard, Enterprise
- SQL Server 2008 R2 SP3: Standard, Enterprise, Datacenter
- SQL Server 2016 Express
- SQL Server 2014 Express SP2
- SQL Server 2014 Express SP1
- SQL Server 2012 Express SP3

## <a name="support-for-active-directory-domains"></a>Supporto per i domini di Active Directory
Tutti i sistemi del sito LTSB devono essere membri di un dominio Windows Active Directory supportato. Il supporto dei domini Active Directory presenta gli stessi requisiti e le stesse limitazioni di quelli visualizzati in [Supporto per i domini di AD](../plan-design/configs/support-for-active-directory-domains.md), ma è limitato ai livelli funzionali di dominio seguenti:

**Livelli supportati:**
- Windows Server 2008
- Windows Server 2008 R2
- Windows Server 2012
- R2 per Windows Server 2012

## <a name="additional-support-topics-that-apply-to-the-long-term-servicing-branch"></a>Argomenti di supporto aggiuntivo che si applicano a Long-Term Servicing Branch
Le informazioni negli argomenti Current Branch seguenti sono valide per LTSB:
- [Numeri di ridimensionamento e scalabilità](../plan-design/configs/size-and-scale-numbers.md)
- [Prerequisiti del sito e del sistema del sito](../plan-design/configs/site-and-site-system-prerequisites.md)
- [High availability options](../servers/deploy/configure/high-availability-options.md) (Opzioni di disponibilità elevata)
- [Recommended hardware](../plan-design/configs/recommended-hardware.md) (Hardware consigliato)
- [Supporto per le funzionalità e le reti Windows](../plan-design/configs/support-for-windows-features-and-networks.md)
- [Supporto per gli ambienti di virtualizzazione](../plan-design/configs/support-for-virtualization-environments.md)