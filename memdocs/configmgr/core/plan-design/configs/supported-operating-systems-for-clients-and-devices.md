---
title: Client e dispositivi supportati
titleSuffix: Configuration Manager
description: Informazioni sulle versioni dei sistemi operativi supportate da Configuration Manager per client e dispositivi.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 87f4e041-67df-4c61-aa98-7444faffe565
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e573a2887bd527daac9a05fec2e83ef39fbfc4e1
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700317"
---
# <a name="supported-os-versions-for-clients-and-devices-for-configuration-manager"></a>Versioni dei sistemi operativi per client e dispositivi supportate da Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Configuration Manager supporta l'installazione di software client in computer Windows e macOS.  

## <a name="general-requirements-and-limitations"></a>Requisiti e limitazioni di carattere generale

Rivedere i requisiti e le limitazioni seguenti per tutti i client:

- La modifica delle impostazioni del tipo di avvio o di **accesso per tutti** i servizi di Configuration Manager non è supportata. Se vengono apportate modifiche, i servizi principali potrebbero non funzionare correttamente.

## <a name="windows-computers"></a>Computer Windows  

Per gestire le versioni dei sistemi operativi Windows seguenti, usare il client incluso in Configuration Manager. Per altre informazioni, vedere [Come distribuire i client nei computer Windows](../../clients/deploy/deploy-clients-to-windows-computers.md).  

### <a name="supported-client-os-versions"></a>Versioni del sistema operativo client supportate

- **Windows 10**  

    Per altre informazioni dettagliate, vedere [Supporto per Windows 10](support-for-windows-10.md).  

- **Windows 8.1** (x86, x64): Professional, Enterprise

#### <a name="windows-virtual-desktop"></a>Desktop virtuale Windows

<!--3556025-->
[Desktop virtuale Windows](/azure/virtual-desktop/) è un servizio di virtualizzazione di desktop e app eseguito su Microsoft Azure. A partire dalla versione 1906, usare Configuration Manager per gestire questi dispositivi virtuali che eseguono Windows in Azure.

Analogamente a un server terminal, alcuni di questi dispositivi virtuali consentono l'esecuzione di più sessioni utente attive simultanee. Per migliorare le prestazioni dei client, Configuration Manager disabilita ora i criteri utente su tutti i dispositivi che consentono l'esecuzione di più sessioni utente. Anche se si abilitano i criteri utente, il client li disabilita per impostazione predefinita in questi dispositivi, che includono server terminal e Windows 10 Enterprise multisessione.

Il client disabilita i criteri utente solo quando rileva questo tipo di dispositivo durante una nuova installazione. Per i client esistenti di questo tipo che vengono aggiornati alla versione corrente, viene mantenuto il comportamento precedente. In un dispositivo esistente l'impostazione dei criteri utente viene configurata anche se il dispositivo consente più sessioni utente.

Se in questo scenario è necessario usare criteri utente e si accettano le potenziali conseguenze sulle prestazioni, adottare una delle soluzioni seguenti per abilitare i criteri utente:

- Nella versione 1910 e successive usare le [impostazioni client](../../clients/deploy/configure-client-settings.md). Nel gruppo **Criteri client** configurare l'impostazione seguente: **Abilita i criteri utente per più sessioni utente**.<!-- 4737447 -->

- Nella versione 1906 usare Configuration Manager SDK con la [classe WMI del server SMS_PolicyAgentConfig](../../../develop/reference/core/clients/config/sms_policyagentconfig-server-wmi-class.md). Impostare la nuova proprietà `PolicyEnableUserPolicyOnTS` su `true`.

> [!Note]  
> Non è possibile usare la co-gestione con un client che esegue la multisessione di Windows 10 Enterprise. <!-- SCCMDocs-pr#3950 -->

A partire dalla versione 2006, la piattaforma **Windows 10 Enterprise multisessione** è ora disponibile nell'elenco delle versioni del sistema operativo supportate negli oggetti con regole dei requisiti o elenchi di applicabilità.<!--6527576-->

> [!NOTE]
> Se in precedenza era stata selezionata la piattaforma **Windows 10** di primo livello, con questa azione sono state selezionate automaticamente tutte le piattaforme figlio. Questa nuova piattaforma non viene selezionata automaticamente. Se si vuole aggiungere **Windows 10 Enterprise multisessione**, selezionarla manualmente nell'elenco.

Per altre informazioni, vedere gli articoli seguenti:

- [Supporto per gli ambienti di virtualizzazione](support-for-virtualization-environments.md)
- [Gestire i client di Configuration Manager in un'infrastruttura VDI (Virtual Desktop Infrastructure)](../../clients/deploy/plan/considerations-for-managing-clients-in-a-vdi.md)

### <a name="supported-server-os-versions"></a>Versioni del sistema operativo server supportate

- **Windows Server 2019**: Standard, Datacenter <sup>[Nota 1](#bkmk_note1)</sup>  
    (A partire da Configuration Manager versione 1806.)

- **Windows Server 2016**: Standard, Datacenter <sup>[Nota 1](#bkmk_note1)</sup>  

- **Windows Storage Server 2016**: Workgroup, Standard  

- **Windows Server 2012 R2** (x64): Standard, Datacenter <sup>[Nota 1](#bkmk_note1)</sup>

- **Windows Storage Server 2012 R2** (x64)

- **Windows Server 2012** (x64): Standard, Datacenter <sup>[Nota 1](#bkmk_note1)</sup>

- **Windows Storage Server 2012** (x64)

#### <a name="server-core"></a>Server Core

Le versioni seguenti fanno riferimento in modo specifico all'installazione Server Core del sistema operativo. <sup>[Nota 3](#bkmk_note3)</sup>  

Le versioni del canale semestrale di Windows Server sono installazioni Server Core, ad esempio Windows Server versione 1809. Come client di Configuration Manager, sono supportate come la versione del canale semestrale di Windows 10 associata. Per altre informazioni, vedere [Supporto per Windows 10](support-for-windows-10.md).

- **Windows Server 2019** (x64) <sup>[Nota 2](#bkmk_note2)</sup>

- **Windows Server 2016** (x64) <sup>[Nota 2](#bkmk_note2)</sup>

- **Windows Server 2012 R2** (x64) <sup>[Nota 2](#bkmk_note2)</sup>

- **Windows Server 2012** (x64) <sup>[Nota 2](#bkmk_note2)</sup>

#### <a name="note-1"></a><a name="bkmk_note1"></a> Nota 1

Configuration Manager verifica e supporta le edizioni di Windows Server Datacenter, ma non è ufficialmente certificato per Windows Server. Il supporto hotfix di Configuration Manager non è disponibile per problemi specifici di Windows Server Datacenter Edition. Per altre informazioni sul programma di certificazione di Windows Server, vedere [Catalogo di Windows Server](https://www.windowsservercatalog.com/).

#### <a name="note-2"></a><a name="bkmk_note2"></a> Nota 2

Per supportare l'[installazione push client](../../clients/deploy/plan/client-installation-methods.md#client-push-installation), aggiungere il servizio File server del ruolo del server Servizi file e archiviazione. Per altre informazioni sull'installazione di funzionalità di Windows in Server Core, vedere [Install roles, role services, and features by using Windows PowerShell cmdlets](/windows-server/administration/server-manager/install-or-uninstall-roles-role-services-or-features#install-roles-role-services-and-features-by-using-windows-powershell-cmdlets) (Installare ruoli, servizi ruolo e funzionalità tramite cmdlet di Windows PowerShell).  

#### <a name="note-3"></a><a name="bkmk_note3"></a> Nota 3

La nuova app Software Center non è supportata in alcuna versione di Windows Server Core.<!--SCCMDocs issue 683-->

## <a name="windows-embedded-computers"></a>Computer Windows Embedded  

È possibile gestire i dispositivi Windows Embedded installando il client di Configuration Manager nel dispositivo. Per altre informazioni, vedere [Pianificazione della distribuzione del client in dispositivi con Windows Embedded](../../clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

### <a name="requirements-and-limitations"></a>Requisiti e limitazioni

- Tutte le funzionalità client sono supportate nei sistemi Windows Embedded in cui non sono abilitati filtri di scrittura.  

- I client che usano uno dei tipi di filtro seguenti sono supportati per tutte le funzionalità tranne che per il risparmio energia:  

  - Filtri di scrittura avanzati

  - Filtri di scrittura basati su file RAM

  - Filtri di scrittura unificati  

- Il Catalogo applicazioni non è supportato per alcun dispositivo Windows Embedded.  

### <a name="supported-os-versions"></a>Versioni dei sistemi operativi supportate  

- **Windows 10 Enterprise** (x86, x64)  

- **Windows 10 IoT Enterprise** (x86, x64)  
    Questa versione include il canale di manutenzione a lungo termine. Per altre informazioni, vedere [Panoramica di Windows 10 IoT Enterprise](/windows/iot-core/windows-iot-enterprise).<!--SCCMDocs issue 560-->  

- **Windows Embedded 8.1 Industry** (x86, x64)

- **Windows Embedded 8 Standard** (x86, x64)

- **Windows Thin PC** (x86, x64)

- **Windows Embedded POSReady 7** (x86, x64)

- **Windows Embedded Standard 7 con SP1** (x86, x64)

## <a name="windows-ce-computers"></a>Computer Windows CE

È possibile gestire i dispositivi Windows CE con il client legacy del dispositivo mobile di Configuration Manager incluso in Configuration Manager.  

### <a name="requirements-and-limitations"></a>Requisiti e limitazioni

- Il client del dispositivo mobile richiede 0,78 MB di spazio di archiviazione per l'installazione. L'accesso può richiedere fino a 256 KB di spazio di archiviazione aggiuntivo.

- Le funzionalità per questi dispositivi mobili variano a seconda della piattaforma e del tipo di client. Per informazioni sulle funzioni di gestione supportate, vedere [Scegliere una soluzione di gestione dei dispositivi](../choose-a-device-management-solution.md).  

### <a name="supported-os-versions"></a>Versioni dei sistemi operativi supportate

- Windows CE 7.0 (processori ARM e x86)  

    > [!IMPORTANT]
    > La versione 2006 di Configuration Manager elimina il supporto per Windows CE 7.0 come client. La deprecazione è stata annunciata con la [versione 1906](../changes/whats-new-in-version-1906.md#bkmk_deprecated).

#### <a name="supported-languages-include"></a>Le lingue supportate includono

- Cinese (semplificato e tradizionale)

- Inglese (Stati Uniti)

- Francese (Francia)

- Tedesco

- Italiano

- Giapponese  

- Coreano  

- Portoghese (Brasile)  

- Russo  

- Spagnolo (Spagna)  

## <a name="extended-security-updates-and-configuration-manager"></a><a name="bkmk_ESU"></a> Aggiornamenti della sicurezza estesa e Configuration Manager

Gli [aggiornamenti della sicurezza estesa (ESU, Extended Security Updates) ](https://support.microsoft.com/help/4497181/lifecycle-faq-extended-security-updates) sono un'ultima soluzione per i clienti che devono eseguire alcuni prodotti Microsoft legacy oltre la fine del supporto. Ad esempio, Windows 7. Il programma ESU include aggiornamenti della sicurezza critici e/o importanti definiti dal [Microsoft Security Response Center (MSRC) ](https://www.microsoft.com/msrc) per un massimo di tre anni dopo la data di fine del supporto "Extended" del prodotto.

I prodotti che non rientrano nel ciclo di vita del supporto non sono supportati per l'uso con Configuration Manager. Sono inclusi tutti i prodotti coperti dal programma ESU. Gli aggiornamenti della sicurezza rilasciati nel programma ESU verranno pubblicati in Windows Server Update Services (WSUS). Gli aggiornamenti saranno visualizzati nella console di Configuration Manager. Mentre i prodotti coperti dal programma ESU non sono più supportati per l'uso con Configuration Manager, è possibile usare la [versione più recente di Configuration Manager (Current Branch)](../../servers/manage/updates.md#version-details) per distribuire e installare gli aggiornamenti della sicurezza di Windows rilasciati nel programma. La versione rilasciata più recente può essere usata anche per distribuire Windows 10 nei dispositivi che eseguono Windows 7.

Le funzionalità di gestione client che non sono correlate alla gestione degli aggiornamenti software Windows o alla distribuzione del sistema operativo non vengono più testate nei sistemi operativi coperti dal programma ESU e non si garantisce che continueranno a funzionare. È consigliabile eseguire l'aggiornamento o la migrazione a una versione corrente dei sistemi operativi appena possibile per ricevere supporto per la gestione dei client.

## <a name="mac-computers"></a>Computer Mac  

È possibile gestire i computer Apple Mac con il client di Configuration Manager per macOS.  

Il pacchetto di installazione del client macOS non viene fornito con i supporti di Configuration Manager. Scaricarlo dall'Area download Microsoft, [Microsoft Endpoint Configuration Manager - macOS Client (64-bit)](https://www.microsoft.com/download/details.aspx?id=100850).  

Per altre informazioni, vedere [Come distribuire i client in computer Mac](../../clients/deploy/deploy-clients-to-macs.md).  

### <a name="requirements-and-limitations"></a>Requisiti e limitazioni

- Non è consentito installare o eseguire il client di Configuration Manager per macOS nei computer con un account diverso dall'account radice. In caso contrario, i servizi principali potrebbero non funzionare correttamente.  

### <a name="supported-versions"></a>Versioni supportate

- **macOS Catalina (10.15)** (richiede la versione del sito di Configuration Manager 1910 o successiva e il client di Configuration Manager per macOS versione 5.0.8742.1000 o successiva)

- **macOS Mojave (10.14)**

- **macOS High Sierra (10.13)**

## <a name="linux-and-unix-servers"></a>Server Linux e UNIX  

> [!Important]  
> Configuration Manager versione 1902 elimina il supporto per Linux e UNIX come client. La deprecazione è stata annunciata con la [versione 1802](../changes/whats-new-in-version-1802.md#deprecation-announcement-for-linux-and-unix-client-support). Per la gestione dei server Linux, è possibile usare la gestione di Microsoft Azure. Le soluzioni di Azure includono un ampio supporto per Linux che nella maggior parte dei casi supera le funzionalità di Configuration Manager, inclusa la gestione end-to-end delle patch per Linux.

I pacchetti di installazione del client per Linux e UNIX non sono inclusi con i supporti di Configuration Manager. Scaricare i **client per altri sistemi operativi** dall'[Area download Microsoft](https://www.microsoft.com/download/details.aspx?id=47719). Oltre ai pacchetti di installazione client, il download del client include lo script che gestisce l'installazione del client in ogni computer.  

### <a name="requirements-and-limitations"></a>Requisiti e limitazioni

- Per informazioni dettagliate sulle dipendenze del file del sistema operativo per il client per Linux e UNIX, vedere [Prerequisiti per la distribuzione dei client ai server Linux e UNIX](../../clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_ClientDeployPrereqforLnU).  

- Per una panoramica delle funzionalità di gestione supportate per Linux o UNIX, vedere [Come distribuire i client nei server UNIX e Linux](../../clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  

- Per le versioni supportate di Linux e UNIX, la versione indicata include tutte le versioni secondarie successive. Ad esempio, la versione 6 di CentOS include CentOS 6.3. Analogamente, il supporto per un sistema operativo che usa Service Pack, ad esempio SUSE Linux Enterprise Server 11 SP1, include i Service Pack successivi per tale versione del sistema operativo.  

- Per informazioni sui pacchetti di installazione client e su Universal Agent, vedere [Come distribuire i client nei server UNIX e Linux](../../clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  

### <a name="supported-versions"></a>Versioni supportate

Le versioni seguenti sono supportate tramite l'uso del file TAR indicato.  

#### <a name="aix"></a>AIX  

|Version|File TAR|  
|-|-|  
|Version 6.1 (Power)|ccm-Aix61ppc.&lt;build\>.tar|  
|Versione 7.1 (Power)|ccm-Aix71ppc.&lt;build\>.tar|  

#### <a name="centos"></a>CentOS  

|Version|File TAR|  
|-|-|  
|Versione 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 7 x64|ccm-Universalx64.&lt;build\>.tar|  

#### <a name="debian"></a>Debian  

|Version|File TAR|  
|-|-|  
|Versione 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 7 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 7 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 8 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 8 x64|ccm-Universalx64.&lt;build\>.tar|  

#### <a name="hp-ux"></a>HP-UX  

|Version|File TAR|  
|-|-|  
|Version 11iv3 IA64|ccm-HpuxB.11.31i64.&lt;build\>.tar|  

#### <a name="oracle-linux"></a>Oracle Linux  

|Version|File TAR|  
|-|-|  
|Versione 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 7 x64|ccm-Universalx64.&lt;build\>.tar|  

#### <a name="red-hat-enterprise-linux-rhel"></a>Red Hat Enterprise Linux (RHEL)  

|Version|File TAR|  
|-|-|  
|Versione 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 7 x64|ccm-Universalx64.&lt;build\>.tar|  

#### <a name="solaris"></a>Solaris  

|Version|File TAR|  
|-|-|  
|Versione 10 x86|ccm-Sol10x86.&lt;build\>.tar|  
|Version 10 SPARC|ccm-Sol10sparc.&lt;build\>.tar|  
|Versione 11 x86|ccm-Sol11x86.&lt;build\>.tar|  
|Versione 11 SPARC|ccm-Sol11sparc.&lt;build\>.tar|  

#### <a name="suse-linux-enterprise-server-sles"></a>SUSE Linux Enterprise Server (SLES)  

|Version|File TAR|  
|-|-|  
|Versione 10 SP1 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 10 SP1 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 11 SP1 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 11 SP1 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 12 x64|ccm-Universalx64.&lt;build\>.tar|  

#### <a name="ubuntu"></a>Ubuntu  

|Version|File TAR|  
|-|-|  
|Versione 10.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 10.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 12.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 12.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 14.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 14.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 16.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 16.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  


## <a name="on-premises-mdm"></a><a name="bkmk_OnpremOS"></a> Software MDM locale

Configuration Manager include funzionalità predefinite per la gestione dei dispositivi mobili locali senza installare software client. Per altre informazioni, vedere [Gestire i dispositivi mobili con l'infrastruttura locale](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

### <a name="supported-operating-systems"></a>Sistemi operativi supportati

- **Windows 10 Pro** (x86, x64)  

- **Windows 10 Pro Enterprise** (x86, x64)  

- **Windows 10 IoT Enterprise** (x86, x64)  
    Questa versione include il canale di manutenzione a lungo termine. Per altre informazioni, vedere [Panoramica di Windows 10 IoT Enterprise](/windows/iot-core/windows-iot-enterprise).<!--SCCMDocs issue 560-->  

- **Windows 10 IoT Mobile Enterprise**  

- **Windows 10 Team per Surface Hub**  

- **Windows 10 Mobile**  

- **Windows 10 Mobile Enterprise**  

    > [!IMPORTANT]
    > La versione 2006 di Configuration Manager elimina il supporto per Windows 10 Mobile e Windows 10 Mobile Enterprise come client. La deprecazione è stata annunciata con la [versione 1906](../changes/whats-new-in-version-1906.md#bkmk_deprecated).

## <a name="exchange-server-connector"></a><a name="bkmk_ExSrvConOS"></a> Connettore Exchange Server  

Configuration Manager supporta la gestione limitata dei dispositivi che si connettono a Exchange Server, senza installare il client di Configuration Manager. Per altre informazioni, vedere [Gestire i dispositivi mobili con Configuration Manager ed Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

### <a name="supported-versions-of-exchange-server"></a>Versioni di Exchange Server supportate

- **Exchange Online (Office 365)** : questa versione include Business Productivity Online Standard Suite  

- **Exchange Server 2016**  

- **Exchange Server 2013**  

- **Exchange Server 2010 SP1** o **Exchange Server 2010 SP2**