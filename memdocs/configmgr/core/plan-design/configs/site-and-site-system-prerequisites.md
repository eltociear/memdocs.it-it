---
title: Prerequisiti del sito
titleSuffix: Configuration Manager
description: Informazioni su come configurare un computer Windows come un server di sistema del sito di Configuration Manager.
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1392797b-76cb-46b4-a3e4-8f349ccaa078
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d4fb94d0ab64cb7c3dc3128c982b0c2b162b22b7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702159"
---
# <a name="site-and-site-system-prerequisites-for-configuration-manager"></a>Prerequisiti del sito e del sistema del sito per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

I computer basati su Windows richiedono configurazioni specifiche per supportare l'uso come server del sistema del sito di Configuration Manager.

Per alcuni prodotti, come Windows Server Update Services (WSUS) per il punto di aggiornamento software, è necessario fare riferimento alla documentazione dei prodotti per identificare altri prerequisiti e limitazioni per l'uso. Qui sono incluse solo le configurazioni che si applicano direttamente all'uso con Configuration Manager.

Per altre informazioni su .NET Framework, vedere le [domande frequenti sul ciclo di vita di .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework).


## <a name="general-requirements-and-limitations"></a><a name="bkmk_generalprerewq"></a> Requisiti e limitazioni di carattere generale

I requisiti seguenti sono validi per tutti i server del sistema del sito:

- Ogni server del sistema del sito deve usare un sistema operativo a 64 bit. L'unica eccezione è il ruolo del sistema del sito del punto di distribuzione, che può essere installato in alcune versioni del sistema operativo a 32 bit.  

- I sistemi del sito non sono supportati nelle installazioni Server Core per alcun sistema operativo. Un'eccezione è il fatto che le installazioni Server Core sono supportate per il ruolo del sistema del sito del punto di distribuzione. Per altre informazioni, vedere [Sistemi operativi supportati per i server dei sistemi del sito di Configuration Manager](supported-operating-systems-for-site-system-servers.md).  

- Dopo aver installato un server di sistema del sito, non è consentito modificare:  

    - Il nome di dominio in cui si trova il computer del sistema del sito (operazione detta anche **ridenominazione del dominio**).  

    - L'appartenenza del computer al dominio.  

    - Nome del computer.  

    Se è necessario modificare uno di questi elementi, rimuovere prima il ruolo del sistema del sito dal computer. Reinstallare quindi il ruolo dopo aver completato la modifica. Per le modifiche che influiscono sul server del sito, disinstallare prima il sito e quindi reinstallarlo dopo aver completato la modifica.  

- I ruoli del sistema del sito non sono supportati in un'istanza di un cluster Windows Server. L'unica eccezione è il server del database del sito. Per altre informazioni, vedere [Usare un cluster di SQL Server per il database del sito di Configuration Manager](../../servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md).  

    A partire dalla versione 1810, il programma di installazione di Configuration Manager non blocca più l'installazione del ruolo del server del sito in un computer con il ruolo Windows per il clustering di failover. Poiché SQL Always On richiede questo ruolo, non era possibile in precedenza inserire il database del sito nel server del sito. Con questa modifica, è possibile creare un sito a disponibilità elevata con un minor numero di server usando SQL Always On e un server del sito in modalità passiva. Per altre informazioni, vedere [Opzioni di disponibilità elevata](../../servers/deploy/configure/high-availability-options.md). <!--3607761, fka 1359132-->  

- La modifica delle impostazioni del tipo di avvio o di accesso per tutti i servizi di Configuration Manager non è supportata. Tale modifica potrebbe impedire il corretto funzionamento di servizi chiave.  

### <a name="prerequisites-for-windows-server-2012-and-later-operating-systems"></a><a name="bkmk_2012Prereq"></a> Prerequisiti per Windows Server 2012 e sistemi operativi successivi  

Per i prerequisiti specifici dei server e dei ruoli del sistema del sito in Windows Server 2012 e versioni successive, vedere le sezioni principali di questo articolo:

- [Server del sito di amministrazione centrale e del sito primario](#bkmk_2012sspreq)
- [Server del sito secondario](#bkmk_2012secpreq)
- [Server di database](#bkmk_2012dbpreq)
- [Server del provider SMS](#bkmk_2012smsprovpreq)
- [Punto per siti Web del Catalogo applicazioni](#bkmk_2012acwspreq)
- [Punto per servizi Web del Catalogo applicazioni](#bkmk_2012ACwsitepreq)
- [Punto di sincronizzazione di Asset Intelligence](#bkmk_2012AIpreq)
- [Punto di registrazione certificati](#bkmk_2012crppreq)
- [Punto di distribuzione](#bkmk_2012dppreq)
- [Punto di Endpoint Protection](#bkmk_2012EPPpreq)
- [Punto di registrazione](#bkmk_2012Enrollpreq)
- [Punto proxy di registrazione](#bkmk_2012EnrollProxpreq)
- [Punto di stato di fallback](#bkmk_2012FSPpreq)
- [Punto di gestione](#bkmk_2012MPpreq)
- [Punto di Reporting Services](#bkmk_2012RSpoint)
- [Punto di connessione del servizio](#bkmk_SCPpreq)
- [Punto di aggiornamento software](#bkmk_2012SUPpreq)
- [Punto di migrazione stato](#bkmk_2012SMPpreq)

## <a name="central-administration-site-and-primary-site-servers"></a><a name="bkmk_2012sspreq"></a> Server del sito di amministrazione centrale e del sito primario

### <a name="windows-server-roles-and-features"></a>Funzionalità e ruoli di Windows Server

- .NET Framework 3.5

- Compressione differenziale remota  

- Quando si usa un punto di aggiornamento software in un server diverso dal server del sito, installare la console di amministrazione WSUS nel server del sito.

### <a name="net-framework"></a>.NET Framework

Abilitare la funzionalità Windows per .NET Framework 3.5.

Installare anche una versione supportata di .NET Framework versione 4.5 o successiva. A partire dalla versione 1906 Configuration Manager supporta .NET Framework 4.8.

Per altre informazioni sulle versioni di .NET Framework, vedere gli articoli seguenti:

- [Versioni e dipendenze di .NET Framework](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Domande frequenti sul ciclo di vita - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="windows-adk"></a>Windows ADK  

- Prima di installare o aggiornare un sito di amministrazione centrale o un sito primario, installare la versione di Windows ADK (Windows Assessment and Deployment Kit) richiesta dalla versione di Configuration Manager che si intende installare o aggiornare. Per altre informazioni, vedere [Windows 10 ADK](support-for-windows-10.md#windows-10-adk).  

- Per altre informazioni su questo requisito, vedere [Requisiti dell'infrastruttura per la distribuzione del sistema operativo](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

### <a name="visual-c-redistributable"></a>Visual C++ Redistributable  

- Configuration Manager installa Microsoft Visual C++ 2013 Redistributable Package in ogni computer in cui viene installato un server del sito.  

- I siti di amministrazione centrale e i siti primari richiedono entrambe le versioni x86 e x64 del file ridistribuibile applicabile.  

### <a name="sql-server-native-client"></a>SQL Server Native Client

Quando si installa un nuovo sito, Configuration Manager installa automaticamente SQL Server Native Client come componente ridistribuibile. Dopo l'installazione del sito, Configuration Manager non aggiorna SQL Server Native Client. Verificare che il componente sia aggiornato. Per altre informazioni, vedere i [controlli dei prerequisiti per SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="secondary-site-server"></a><a name="bkmk_2012secpreq"></a> Server del sito secondario

### <a name="windows-server-roles-and-features"></a>Funzionalità e ruoli di Windows Server

- .NET Framework 3.5

- Compressione differenziale remota  

### <a name="net-framework"></a>.NET Framework

Abilitare la funzionalità Windows per .NET Framework 3.5.

Installare anche una versione supportata di .NET Framework versione 4.5 o successiva. A partire dalla versione 1906 Configuration Manager supporta .NET Framework 4.8.

Per altre informazioni sulle versioni di .NET Framework, vedere gli articoli seguenti:

- [Versioni e dipendenze di .NET Framework](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Domande frequenti sul ciclo di vita - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="visual-c-redistributable"></a>Visual C++ Redistributable

- Configuration Manager installa Microsoft Visual C++ 2013 Redistributable Package in ogni computer in cui viene installato un server del sito.  

- I siti secondari richiedono solo la versione x64.  

### <a name="default-site-system-roles"></a>Ruoli del sistema del sito predefiniti  

- Per impostazione predefinita, un sito secondario installa un **punto di gestione** e un **punto di distribuzione**.  

- Assicurarsi che il server del sito secondario soddisfi i prerequisiti per questi ruoli del sistema del sito.  

### <a name="sql-server-native-client"></a>SQL Server Native Client

Quando si installa un nuovo sito, Configuration Manager installa automaticamente SQL Server Native Client come componente ridistribuibile. Dopo l'installazione del sito, Configuration Manager non aggiorna SQL Server Native Client. Verificare che il componente sia aggiornato. Per altre informazioni, vedere i [controlli dei prerequisiti per SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="database-server"></a><a name="bkmk_2012dbpreq"></a> Server di database  

### <a name="remote-registry-service"></a>Servizio Registro di sistema remoto  

- Durante l'installazione del sito di Configuration Manager abilitare il servizio **Registro di sistema remoto** nel computer che ospita il database del sito.  

### <a name="sql-server"></a>SQL Server  

- Prima di installare un sito di amministrazione centrale o un sito primario, installare una versione supportata di SQL Server per ospitare il database del sito. Per altre informazioni, vedere [Versioni di SQL Server supportate](support-for-sql-server-versions.md).  

- Prima di installare un sito secondario, è possibile installare una versione supportata di SQL Server.  

- Se si sceglie di lasciare che Configuration Manager installi SQL Server Express come parte dell'installazione del sito secondario, assicurarsi che il computer soddisfi i requisiti per l'esecuzione di SQL Server Express.  

### <a name="sql-server-native-client"></a>SQL Server Native Client

Quando si installa un nuovo sito, Configuration Manager installa automaticamente SQL Server Native Client come componente ridistribuibile. Dopo l'installazione del sito, Configuration Manager non aggiorna SQL Server Native Client. Verificare che il componente sia aggiornato. Per altre informazioni, vedere i [controlli dei prerequisiti per SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="sms-provider-server"></a><a name="bkmk_2012smsprovpreq"></a> Server del provider SMS  

### <a name="windows-adk"></a>Windows ADK

- Nel computer in cui si installa un'istanza del provider SMS deve essere installata la versione di Windows ADK richiesta dalla versione di Configuration Manager che si intende installare o aggiornare. Per altre informazioni, vedere [Windows 10 ADK](support-for-windows-10.md#windows-10-adk).  

- Per altre informazioni su questo requisito, vedere [Requisiti dell'infrastruttura per la distribuzione del sistema operativo](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

### <a name="windows-server-roles-and-features"></a>Funzionalità e ruoli di Windows Server

- Se si usa il [servizio di amministrazione](../../../develop/adminservice/overview.md), il server che ospita il ruolo di provider SMS richiede .NET 4.5 o versioni successive  <!-- SCCMDocs issue #1203 -->

    > [!NOTE]
    > Configuration Manager versione 1810 richiede .NET 4.5.2 o versioni successive.

- Server Web (IIS): Ogni provider tenta di installare il [servizio di amministrazione](../../../develop/adminservice/overview.md). Questo servizio ha una dipendenza in IIS per associare un certificato alla porta HTTPS 443. Configuration Manager usa le API IIS per verificare questa configurazione del certificato. Se si configura il sito per [HTTP avanzato](../hierarchy/enhanced-http.md), Configuration Manager usa le API IIS per associare il certificato generato dal sito. A partire dalla versione 2002, il sito usa automaticamente il certificato autofirmato del sito.

### <a name="sql-server-native-client"></a>SQL Server Native Client

Quando si installa un nuovo sito, Configuration Manager installa automaticamente SQL Server Native Client come componente ridistribuibile. Dopo l'installazione del sito, Configuration Manager non aggiorna SQL Server Native Client. Verificare che il componente sia aggiornato. Per altre informazioni, vedere i [controlli dei prerequisiti per SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="application-catalog-website-point"></a><a name="bkmk_2012acwspreq"></a> Punto per siti Web del catalogo applicazioni  

> [!Important]  
> L'esperienza utente di Silverlight per il catalogo applicazioni non è supportata a partire dalla versione Current Branch 1806. A partire dalla versione 1906, i client aggiornati usano automaticamente il punto di gestione per le distribuzioni di applicazioni disponibili per gli utenti. Non è inoltre possibile installare nuovi ruoli del Catalogo applicazioni. Il supporto per i ruoli del Catalogo applicazioni termina con la versione 1910.  
>
> Per altre informazioni, vedere gli articoli seguenti:
>
> - [Configurare Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Funzionalità rimosse e deprecate](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

### <a name="windows-server-roles-and-features"></a>Funzionalità e ruoli di Windows Server

- .NET Framework 3.5

- ASP.NET 4.5  

### <a name="net-framework"></a>.NET Framework

Abilitare la funzionalità Windows per .NET Framework 3.5.

Installare anche una versione supportata di .NET Framework versione 4.5 o successiva.

Per altre informazioni sulle versioni di .NET Framework, vedere gli articoli seguenti:

- [Versioni e dipendenze di .NET Framework](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Domande frequenti sul ciclo di vita - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>Configurazione di IIS  

- Funzionalità HTTP comuni:  

    - Documento predefinito  

    - Contenuto statico  

- Sviluppo di applicazioni:  

    - ASP.NET 3.5 (e le opzioni selezionate automaticamente)  

    - ASP.NET 4.5 (e le opzioni selezionate automaticamente)  

    - Estendibilità .NET 3.5  

    - Estendibilità .NET 4.5  

- Sicurezza:  

    - Autenticazione di Windows  

- Compatibilità Gestione IIS 6:  

    - Compatibilità Metabase IIS 6  


## <a name="application-catalog-web-service-point"></a><a name="bkmk_2012ACwsitepreq"></a> Punto per servizi Web del catalogo applicazioni  

> [!Important]  
> L'esperienza utente di Silverlight per il catalogo applicazioni non è supportata a partire dalla versione Current Branch 1806. A partire dalla versione 1906, i client aggiornati usano automaticamente il punto di gestione per le distribuzioni di applicazioni disponibili per gli utenti. Non è inoltre possibile installare nuovi ruoli del Catalogo applicazioni. Il supporto per i ruoli del Catalogo applicazioni termina con la versione 1910.  
>
> Per altre informazioni, vedere gli articoli seguenti:
>
> - [Configurare Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Funzionalità rimosse e deprecate](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

### <a name="windows-server-roles-and-features"></a>Funzionalità e ruoli di Windows Server

- .NET Framework 3.5

- ASP.NET 4.5:  

    - Attivazione ASP.NET (e le opzioni selezionate automaticamente)  

### <a name="net-framework"></a>.NET Framework

Abilitare la funzionalità Windows per .NET Framework 3.5.

Installare anche una versione supportata di .NET Framework versione 4.5 o successiva.

Per altre informazioni sulle versioni di .NET Framework, vedere gli articoli seguenti:

- [Versioni e dipendenze di .NET Framework](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Domande frequenti sul ciclo di vita - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>Configurazione di IIS

- Funzionalità HTTP comuni:  

    - Documento predefinito  

- Compatibilità Gestione IIS 6:  

    - Compatibilità Metabase IIS 6  

- Sviluppo di applicazioni:  

    - ASP.NET 3.5 (e le opzioni selezionate automaticamente)  

    - Estendibilità .NET 3.5  

    - ASP.NET 4.5 (e le opzioni selezionate automaticamente)  

    - Estendibilità .NET 4.5  

### <a name="computer-memory"></a>Memoria del computer  

- Il computer che ospita questo ruolo del sistema del sito deve avere almeno il 5% di memoria libera disponibile per permettere al ruolo del sistema del sito di elaborare le richieste.  

- Quando questo ruolo del sistema del sito condivide il percorso con un altro ruolo del sistema del sito con lo stesso requisito, questo requisito di memoria per il computer non aumenta, ma rimane almeno pari al 5%.  

### <a name="sql-server-native-client"></a>SQL Server Native Client

Quando si installa un nuovo sito, Configuration Manager installa automaticamente SQL Server Native Client come componente ridistribuibile. Dopo l'installazione del sito, Configuration Manager non aggiorna SQL Server Native Client. Verificare che il componente sia aggiornato. Per altre informazioni, vedere i [controlli dei prerequisiti per SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="asset-intelligence-synchronization-point"></a><a name="bkmk_2012AIpreq"></a> Punto di sincronizzazione di Asset Intelligence  

### <a name="net-framework"></a>.NET Framework

Installare una versione supportata di .NET Framework versione 4.5 o successiva. A partire dalla versione 1906 Configuration Manager supporta .NET Framework 4.8.

Per altre informazioni sulle versioni di .NET Framework, vedere gli articoli seguenti:

- [Versioni e dipendenze di .NET Framework](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Domande frequenti sul ciclo di vita - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="sql-server-native-client"></a>SQL Server Native Client

Quando si installa un nuovo sito, Configuration Manager installa automaticamente SQL Server Native Client come componente ridistribuibile. Dopo l'installazione del sito, Configuration Manager non aggiorna SQL Server Native Client. Verificare che il componente sia aggiornato. Per altre informazioni, vedere i [controlli dei prerequisiti per SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="certificate-registration-point"></a><a name="bkmk_2012crppreq"></a> Punto di registrazione certificati  

### <a name="windows-server-roles-and-features"></a>Funzionalità e ruoli di Windows Server

- .NET Framework

    - Attivazione HTTP  

### <a name="net-framework"></a>.NET Framework

Installare una versione supportata di .NET Framework versione 4.5 o successiva. A partire dalla versione 1906 Configuration Manager supporta .NET Framework 4.8.

Per altre informazioni sulle versioni di .NET Framework, vedere gli articoli seguenti:

- [Versioni e dipendenze di .NET Framework](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Domande frequenti sul ciclo di vita - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>Configurazione di IIS

- Sviluppo di applicazioni:  

    - ASP.NET 3.5 (e le opzioni selezionate automaticamente)  

    - ASP.NET 4.5 (e le opzioni selezionate automaticamente)  

- Compatibilità Gestione IIS 6:  

    - Compatibilità Metabase IIS 6  

    - Compatibilità WMI IIS 6  

### <a name="sql-server-native-client"></a>SQL Server Native Client

Quando si installa un nuovo sito, Configuration Manager installa automaticamente SQL Server Native Client come componente ridistribuibile. Dopo l'installazione del sito, Configuration Manager non aggiorna SQL Server Native Client. Verificare che il componente sia aggiornato. Per altre informazioni, vedere i [controlli dei prerequisiti per SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="distribution-point"></a><a name="bkmk_2012dppreq"></a> Punto di distribuzione  

### <a name="windows-server-roles-and-features"></a>Funzionalità e ruoli di Windows Server

- Compressione differenziale remota  

#### <a name="iis-configuration"></a>Configurazione di IIS

- Sviluppo di applicazioni:  

    - Estensioni ISAPI  

- Sicurezza:  

    - Autenticazione di Windows  

- Compatibilità Gestione IIS 6:  

    - Compatibilità Metabase IIS 6  

    - Compatibilità WMI IIS 6  

### <a name="powershell"></a>PowerShell  

- In Windows Server 2012 o versioni successive è necessario PowerShell 3.0 o 4.0 prima di installare il punto di distribuzione.  

### <a name="visual-c-redistributable"></a>Visual C++ Redistributable

- Configuration Manager installa Microsoft Visual C++ 2013 Redistributable Package in ogni computer che ospita un punto di distribuzione.  

- La versione installata dipende dalla piattaforma del computer (x86 o x64).  

### <a name="microsoft-azure"></a>Microsoft Azure  

- È possibile usare un servizio cloud in Microsoft Azure per ospitare un punto di distribuzione.  

### <a name="to-support-pxe-or-multicast"></a>Per il supporto di PXE o del multicast  

- Abilitare un risponditore PXE in un punto di distribuzione senza Servizi di distribuzione Windows.  

- Installare e configurare il ruolo Servizi di distribuzione Windows di Windows Server.  

    > [!NOTE]  
    > Servizi di distribuzione Windows viene installato e configurato automaticamente quando si configura un punto di distribuzione per il supporto di PXE o del multicast in un server che esegue Windows Server 2012 o versioni successive.  

- Per un punto di distribuzione abilitato per multicast, verificare che il SQL Server Native Client sia installato e aggiornato. Per altre informazioni, vedere i [controlli dei prerequisiti per SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).

Per altre informazioni, vedere [Installare e configurare i punti di distribuzione](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).

<!--sms.503672 -Clarified BITS use-->
> [!NOTE]  
> Quando il punto di distribuzione trasferisce il contenuto, per eseguire il trasferimento si usa il **Servizio trasferimento intelligente in background** (BITS) incluso in Windows. Il ruolo del punto di distribuzione non richiede l'installazione della funzionalità facoltativa di estensione del server IIS BITS, perché il client non carica informazioni in tale server.  


## <a name="endpoint-protection-point"></a><a name="bkmk_2012EPPpreq"></a> Punto di Endpoint Protection  

### <a name="windows-server-roles-and-features"></a>Funzionalità e ruoli di Windows Server  

- .NET Framework 3.5

- Funzionalità di Windows Defender (Windows Server 2016 o versioni successive)  

### <a name="sql-server-native-client"></a>SQL Server Native Client

Quando si installa un nuovo sito, Configuration Manager installa automaticamente SQL Server Native Client come componente ridistribuibile. Dopo l'installazione del sito, Configuration Manager non aggiorna SQL Server Native Client. Verificare che il componente sia aggiornato. Per altre informazioni, vedere i [controlli dei prerequisiti per SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="enrollment-point"></a><a name="bkmk_2012Enrollpreq"></a> Punto di registrazione  

### <a name="windows-server-roles-and-features"></a>Funzionalità e ruoli di Windows Server

- .NET Framework 3.5

    - Attivazione ASP.NET (e le opzioni selezionate automaticamente)  

    - ASP.NET 4.5  

    - Servizi Windows Communication Foundation (WCF)<!-- SCCMDocs issue #1168 -->  

### <a name="net-framework"></a>.NET Framework

Abilitare la funzionalità Windows per .NET Framework 3.5.

Installare anche una versione supportata di .NET Framework versione 4.5 o successiva. A partire dalla versione 1906 Configuration Manager supporta .NET Framework 4.8.

> [!Note]
> Quando viene installato questo ruolo del sistema del sito, Configuration Manager installa automaticamente .NET Framework 4.5.2. Questa installazione può far sì che il server passi a uno stato di riavvio in sospeso. Se un riavvio è in sospeso per .NET Framework, le applicazioni .NET possono restituire un errore finché il server non viene riavviato e l'installazione non viene completata.  

Per altre informazioni sulle versioni di .NET Framework, vedere gli articoli seguenti:

- [Versioni e dipendenze di .NET Framework](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Domande frequenti sul ciclo di vita - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>Configurazione di IIS

- Funzionalità HTTP comuni:  

    - Documento predefinito  

- Sviluppo di applicazioni:  

    - ASP.NET 3.5 (e le opzioni selezionate automaticamente)  

    - Estendibilità .NET 3.5  

    - ASP.NET 4.5 (e le opzioni selezionate automaticamente)  

    - Estendibilità .NET 4.5  

- Compatibilità Gestione IIS 6:  

    - Compatibilità Metabase IIS 6  

### <a name="computer-memory"></a>Memoria del computer

- Il computer che ospita questo ruolo del sistema del sito deve avere almeno il 5% di memoria libera disponibile per permettere al ruolo del sistema del sito di elaborare le richieste.  

- Quando questo ruolo del sistema del sito condivide il percorso con un altro ruolo del sistema del sito con lo stesso requisito, questo requisito di memoria per il computer non aumenta, ma rimane almeno pari al 5%.  

### <a name="sql-server-native-client"></a>SQL Server Native Client

Quando si installa un nuovo sito, Configuration Manager installa automaticamente SQL Server Native Client come componente ridistribuibile. Dopo l'installazione del sito, Configuration Manager non aggiorna SQL Server Native Client. Verificare che il componente sia aggiornato. Per altre informazioni, vedere i [controlli dei prerequisiti per SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="enrollment-proxy-point"></a><a name="bkmk_2012EnrollProxpreq"></a> Punto proxy di registrazione  

### <a name="windows-server-roles-and-features"></a>Funzionalità e ruoli di Windows Server

- .NET Framework 3.5

### <a name="net-framework"></a>.NET Framework

Abilitare la funzionalità Windows per .NET Framework 3.5.

Installare anche una versione supportata di .NET Framework versione 4.5 o successiva. A partire dalla versione 1906 Configuration Manager supporta .NET Framework 4.8.

> [!Note]
> Quando viene installato questo ruolo del sistema del sito, Configuration Manager installa automaticamente .NET Framework 4.5.2. Questa installazione può far sì che il server passi a uno stato di riavvio in sospeso. Se un riavvio è in sospeso per .NET Framework, le applicazioni .NET possono restituire un errore finché il server non viene riavviato e l'installazione non viene completata.  

Per altre informazioni sulle versioni di .NET Framework, vedere gli articoli seguenti:

- [Versioni e dipendenze di .NET Framework](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Domande frequenti sul ciclo di vita - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>Configurazione di IIS

- Funzionalità HTTP comuni:  

    - Documento predefinito  

    - Contenuto statico  

- Sviluppo di applicazioni:  

    - ASP.NET 3.5 (e le opzioni selezionate automaticamente)  

    - ASP.NET 4.5 (e le opzioni selezionate automaticamente)  

    - Estendibilità .NET 3.5  

    - Estendibilità .NET 4.5  

- Sicurezza:  

    - Autenticazione di Windows  

- Compatibilità Gestione IIS 6:  

    - Compatibilità Metabase IIS 6  

### <a name="computer-memory"></a>Memoria del computer

- Il computer che ospita questo ruolo del sistema del sito deve avere almeno il 5% di memoria libera disponibile per permettere al ruolo del sistema del sito di elaborare le richieste.  

- Quando questo ruolo del sistema del sito condivide il percorso con un altro ruolo del sistema del sito con lo stesso requisito, questo requisito di memoria per il computer non aumenta, ma rimane almeno pari al 5%.  


## <a name="fallback-status-point"></a><a name="bkmk_2012FSPpreq"></a> Punto di stato di fallback

### <a name="windows-server-roles-and-features"></a>Funzionalità e ruoli di Windows Server

- Estensioni del server BITS (e le opzioni selezionate automaticamente) o Servizio trasferimento intelligente in background (BITS) (e le opzioni selezionate automaticamente)

#### <a name="iis-configuration"></a>Configurazione di IIS

È necessaria la configurazione predefinita di IIS con le aggiunte seguenti:  

- Compatibilità Gestione IIS 6:  

    - Compatibilità Metabase IIS 6  


## <a name="management-point"></a><a name="bkmk_2012MPpreq"></a> Punto di gestione  

### <a name="windows-server-roles-and-features"></a>Funzionalità e ruoli di Windows Server

- Estensioni del server BITS (e le opzioni selezionate automaticamente) o Servizio trasferimento intelligente in background (BITS) (e le opzioni selezionate automaticamente)  

### <a name="net-framework"></a>.NET Framework

Installare una versione supportata di .NET Framework versione 4.5 o successiva. A partire dalla versione 1906 Configuration Manager supporta .NET Framework 4.8.

Per altre informazioni sulle versioni di .NET Framework, vedere gli articoli seguenti:

- [Versioni e dipendenze di .NET Framework](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Domande frequenti sul ciclo di vita - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>Configurazione di IIS

- Sviluppo di applicazioni:  

    - Estensioni ISAPI  

- Sicurezza:  

    - Autenticazione di Windows  

- Compatibilità Gestione IIS 6:  

    - Compatibilità Metabase IIS 6  

    - Compatibilità WMI IIS 6  

### <a name="sql-server-native-client"></a>SQL Server Native Client

Quando si installa un nuovo sito, Configuration Manager installa automaticamente SQL Server Native Client come componente ridistribuibile. Dopo l'installazione del sito, Configuration Manager non aggiorna SQL Server Native Client. Verificare che il componente sia aggiornato. Per altre informazioni, vedere i [controlli dei prerequisiti per SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="reporting-services-point"></a><a name="bkmk_2012RSpoint"></a> Punto di Reporting Services  

### <a name="net-framework"></a>.NET Framework

Installare una versione supportata di .NET Framework versione 4.5 o successiva. A partire dalla versione 1906 Configuration Manager supporta .NET Framework 4.8.

Per altre informazioni sulle versioni di .NET Framework, vedere gli articoli seguenti:

- [Versioni e dipendenze di .NET Framework](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Domande frequenti sul ciclo di vita - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="sql-server-reporting-services"></a>SQL Server Reporting Services  

- Prima di installare il punto di reporting, installare e configurare almeno un'istanza di SQL Server per supportare SQL Server Reporting Services.  

- L'istanza usata per SQL Server Reporting Services può essere la stessa usata per il database del sito.  

- Inoltre, l'istanza usata può essere condivisa con altri prodotti System Center purché per tali prodotti non siano previste limitazioni per la condivisione dell'istanza di SQL Server.  

### <a name="sql-server-native-client"></a>SQL Server Native Client

Quando si installa un nuovo sito, Configuration Manager installa automaticamente SQL Server Native Client come componente ridistribuibile. Dopo l'installazione del sito, Configuration Manager non aggiorna SQL Server Native Client. Verificare che il componente sia aggiornato. Per altre informazioni, vedere i [controlli dei prerequisiti per SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="service-connection-point"></a><a name="bkmk_SCPpreq"></a> Punto di connessione del servizio  

### <a name="net-framework"></a>.NET Framework

Abilitare la funzionalità Windows per .NET Framework 3.5.

Installare anche una versione supportata di .NET Framework versione 4.5 o successiva. A partire dalla versione 1906 Configuration Manager supporta .NET Framework 4.8.

> [!Note]
> Quando viene installato questo ruolo del sistema del sito, Configuration Manager installa automaticamente .NET Framework 4.5.2. Questa installazione può far sì che il server passi a uno stato di riavvio in sospeso. Se un riavvio è in sospeso per .NET Framework, le applicazioni .NET possono restituire un errore finché il server non viene riavviato e l'installazione non viene completata.  

Per altre informazioni sulle versioni di .NET Framework, vedere gli articoli seguenti:

- [Versioni e dipendenze di .NET Framework](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Domande frequenti sul ciclo di vita - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="visual-c-redistributable"></a>Visual C++ Redistributable

- Configuration Manager installa Microsoft Visual C++ 2013 Redistributable Package in ogni computer che ospita un punto di distribuzione.  

- Il ruolo del sistema del sito richiede la versione x64.  

### <a name="sql-server-native-client"></a>SQL Server Native Client

Quando si installa un nuovo sito, Configuration Manager installa automaticamente SQL Server Native Client come componente ridistribuibile. Dopo l'installazione del sito, Configuration Manager non aggiorna SQL Server Native Client. Verificare che il componente sia aggiornato. Per altre informazioni, vedere i [controlli dei prerequisiti per SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="software-update-point"></a><a name="bkmk_2012SUPpreq"></a> Punto di aggiornamento software  

### <a name="windows-server-roles-and-features"></a>Funzionalità e ruoli di Windows Server

- .NET Framework 3.5

È necessaria la configurazione predefinita di IIS.

### <a name="net-framework"></a>.NET Framework

Abilitare la funzionalità Windows per .NET Framework 3.5.

Installare anche una versione supportata di .NET Framework versione 4.5 o successiva. A partire dalla versione 1906 Configuration Manager supporta .NET Framework 4.8.

Per altre informazioni sulle versioni di .NET Framework, vedere gli articoli seguenti:

- [Versioni e dipendenze di .NET Framework](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Domande frequenti sul ciclo di vita - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="windows-server-update-services"></a>Windows Server Update Services  

- Installare il ruolo del server Windows Server Update Services di Windows in un computer prima di installare un punto di aggiornamento software.  

- Per altre informazioni, vedere [Pianificare gli aggiornamenti software](../../../sum/plan-design/plan-for-software-updates.md).  

> [!NOTE]  
> Quando si usa un punto di aggiornamento software in un server diverso dal server del sito, è necessario installare la console di amministrazione WSUS nel server del sito.

### <a name="sql-server-native-client"></a>SQL Server Native Client

Quando si installa un nuovo sito, Configuration Manager installa automaticamente SQL Server Native Client come componente ridistribuibile. Dopo l'installazione del sito, Configuration Manager non aggiorna SQL Server Native Client. Verificare che il componente sia aggiornato. Per altre informazioni, vedere i [controlli dei prerequisiti per SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="state-migration-point"></a><a name="bkmk_2012SMPpreq"></a> Punto di migrazione stato

<!--SCCMDocs issue 645-->
### <a name="windows-server-roles-and-features"></a>Funzionalità e ruoli di Windows Server

- .NET Framework 3.5

    - Attivazione ASP.NET (e le opzioni selezionate automaticamente)  

    - ASP.NET 4.5  

### <a name="net-framework"></a>.NET Framework

Abilitare la funzionalità Windows per .NET Framework 3.5.

Installare anche una versione supportata di .NET Framework versione 4.5 o successiva. A partire dalla versione 1906 Configuration Manager supporta .NET Framework 4.8.

> [!Note]
> Quando viene installato questo ruolo del sistema del sito, Configuration Manager installa automaticamente .NET Framework 4.5.2. Questa installazione può far sì che il server passi a uno stato di riavvio in sospeso. Se un riavvio è in sospeso per .NET Framework, le applicazioni .NET possono restituire un errore finché il server non viene riavviato e l'installazione non viene completata.  

Per altre informazioni sulle versioni di .NET Framework, vedere gli articoli seguenti:

- [Versioni e dipendenze di .NET Framework](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Domande frequenti sul ciclo di vita - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>Configurazione di IIS

- Funzionalità HTTP comuni:  

    - Documento predefinito  

- Sviluppo di applicazioni:  

    - ASP.NET 3.5 (e le opzioni selezionate automaticamente)  

    - Estendibilità .NET 3.5  

    - ASP.NET 4.5 (e le opzioni selezionate automaticamente)  

    - Estendibilità .NET 4.5  

- Compatibilità Gestione IIS 6:  

    - Compatibilità Metabase IIS 6  

### <a name="sql-server-native-client"></a>SQL Server Native Client

Quando si installa un nuovo sito, Configuration Manager installa automaticamente SQL Server Native Client come componente ridistribuibile. Dopo l'installazione del sito, Configuration Manager non aggiorna SQL Server Native Client. Verificare che il componente sia aggiornato. Per altre informazioni, vedere i [controlli dei prerequisiti per SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).

