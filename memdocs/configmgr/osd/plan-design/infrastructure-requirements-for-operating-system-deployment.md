---
title: Requisiti dell'infrastruttura di distribuzione del sistema operativo
titleSuffix: Configuration Manager
description: Informazioni sulle dipendenze esterne e dei prodotti e sui requisiti per la distribuzione del sistema operativo in Configuration Manager
ms.date: 07/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 1dc74219-7ff5-4e3b-b4f6-5aad663bb75b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f34c803cb2b43a2c69cee4c16f5029474e318eb2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709339"
---
# <a name="infrastructure-requirements-for-os-deployment-in-configuration-manager"></a>Requisiti dell'infrastruttura per la distribuzione del sistema operativo in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

La distribuzione del sistema operativo in Configuration Manager ha dipendenze esterne e dipendenze all'interno del prodotto. Usare questo articolo per agevolare la preparazione dell'infrastruttura per la distribuzione del sistema operativo.  

##  <a name="dependencies-external-to-configuration-manager"></a><a name="BKMK_ExternalDependencies"></a> Dipendenze esterne a Configuration Manager  

Questa sezione offre informazioni su strumenti esterni, kit di installazione e versioni di sistemi operativi richiesti per distribuire sistemi operativi in Configuration Manager.  

### <a name="windows-adk-for-windows-10"></a>Windows ADK per Windows 10  

Windows Assessment and Deployment Kit (ADK) è un set di strumenti e documentazione a supporto della configurazione e della distribuzione di Windows. Configuration Manager usa Windows ADK per automatizzare azioni quali l'installazione di Windows, l'acquisizione di immagini e la migrazione di dati e profili utente.  

Per altre informazioni, vedere gli articoli seguenti:  

- [Scenari di Windows ADK per Windows 10 per i professionisti IT](https://docs.microsoft.com/windows/deployment/windows-adk-scenarios-for-it-pros)  

- [Scaricare Windows ADK per Windows 10](https://docs.microsoft.com/windows-hardware/get-started/adk-install)  

    > [!IMPORTANT]
    > Assicurarsi di scaricare sia **Windows ADK per Windows 10** che il **componente aggiuntivo Windows PE per l'ADK**.

- [Supporto per Windows 10](../../core/plan-design/configs/support-for-windows-10.md)  

#### <a name="site-systems"></a>Sistemi del sito
Windows ADK è un prerequisito per i server dei sistemi del sito seguenti:

- Server del sito del sito di primo livello nella gerarchia  

- Server del sito del sito di ogni sito primario nella gerarchia  

- Ogni istanza del provider SMS  


> [!NOTE]  
> Installare manualmente Windows ADK in ogni server del sito prima di installare il sito di Configuration Manager.  

#### <a name="windows-adk-features"></a>Funzionalità di Windows ADK
Installare le funzionalità seguenti di Windows ADK:  

-   Utilità di migrazione stato utente (USMT)  

    > [!Note]  
    > L'Utilità di migrazione stato utente non è richiesta nel provider SMS.

-   Strumenti di distribuzione Windows  

-   Ambiente preinstallazione di Windows (Windows PE)  

    > [!Important]  
    > A partire da Windows 10 versione 1809, Windows PE è un programma di installazione separato. Non ci sono altre differenze funzionali.<!--SCCMDocs-pr issue 2908-->  

Per un elenco delle versioni di Windows 10 ADK che è possibile usare con versioni diverse di Configuration Manager, vedere [Supporto per Windows 10](../../core/plan-design/configs/support-for-windows-10.md#windows-10-adk).


### <a name="user-state-migration-tool-usmt"></a>Utilità di migrazione stato utente (USMT)  

Configuration Manager usa un pacchetto USMT che include i file di origine di USMT 10 per acquisire e ripristinare lo stato utente nell'ambito della distribuzione del sistema operativo. Il programma di installazione di Configuration Manager crea automaticamente il pacchetto USMT nel sito di livello superiore. USMT 10 acquisisce lo stato utente da Windows 7, Windows 8, Windows 8.1 e Windows 10.  

Per altre informazioni, vedere gli articoli seguenti:  

- [Scenari di migrazione comuni per USMT 10](https://docs.microsoft.com/windows/deployment/usmt/usmt-common-migration-scenarios)  

- [Gestire lo stato utente](../get-started/manage-user-state.md)  


### <a name="windows-pe"></a>Windows PE  

Windows PE viene usato per le immagini di avvio per avviare un computer. Si tratta di una versione di Windows con servizi limitati che viene usata durante la pre-installazione e la distribuzione di Windows. L'elenco seguente include le versioni supportate di Windows ADK per Configuration Manager, Current Branch:  

#### <a name="windows-adk-version"></a>Versione di Windows ADK  
Windows ADK per Windows 10. Per altre informazioni, vedere [Supporto per Windows 10](../../core/plan-design/configs/support-for-windows-10.md#windows-10-adk).

#### <a name="windows-pe-versions-for-boot-images-customizable-from-the-configuration-manager-console"></a>Versioni di Windows PE per le immagini d'avvio personalizzabili dalla console di Configuration Manager  
Windows PE 10  

#### <a name="supported-windows-pe-versions-for-boot-images-not-customizable-from-the-configuration-manager-console"></a>Versioni di Windows PE supportate per le immagini d'avvio non personalizzabili dalla console di Configuration Manager  
Windows PE 3.1<sup>1</sup> e Windows PE 5  

<sup>1</sup> È possibile aggiungere un'immagine d'avvio a Configuration Manager solo se è basata su Windows PE 3.1. Installare il supplemento Windows AIK per Windows 7 SP1 per aggiornare Windows AIK per Windows 7 (basato su Windows PE 3) con il supplemento Windows AIK per Windows 7 SP1 (basato su Windows PE 3.1). Scaricare il supplemento Windows AIK per Windows 7 SP1 dall'[Area download Microsoft](https://www.microsoft.com/download/details.aspx?id=5188).  

Ad esempio, se si ha Configuration Manager, è possibile personalizzare le immagini d'avvio da Windows ADK per Windows 10 (basato su Windows PE 10) dalla console di Configuration Manager. Anche se le immagini d'avvio basate su Windows PE 5 sono supportate, è comunque necessario personalizzarle da un computer diverso e usare la versione di Gestione e manutenzione immagini distribuzione installata con Windows AIK per Windows 8. Aggiungere quindi l'immagine d'avvio alla console di Configuration Manager. Per altre informazioni sui passaggi per personalizzare un'immagine d'avvio (aggiungere componenti e driver facoltativi), abilitare il supporto comandi nell'immagine d'avvio, aggiungere l'immagine d'avvio alla console di Configuration Manager e aggiornare i punti di distribuzione con l'immagine d'avvio, vedere [Customize boot images](../get-started/customize-boot-images.md) (Personalizzare le immagini d'avvio). Per altre informazioni sulle immagini d'avvio, vedere [Gestire le immagini d'avvio con System Center Configuration Manager](../get-started/manage-boot-images.md).  


### <a name="windows-server-update-services-wsus"></a>Windows Server Update Services (WSUS)  

WSUS è necessario per il punto di aggiornamento software, richiesto per installare gli aggiornamenti software durante la distribuzione del sistema operativo. Per altre informazioni, vedere [Installare e configurare un punto di aggiornamento software](../../sum/get-started/install-a-software-update-point.md).


### <a name="internet-information-services-iis-on-the-site-system-servers"></a>Internet Information Services (IIS) nei server del sistema del sito  

IIS è necessario per il punto di distribuzione, per il punto di migrazione stato e per il punto di gestione. Per altre informazioni, vedere [Prerequisiti del sito e del sistema del sito](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  


### <a name="windows-deployment-services-wds"></a>Servizi di distribuzione Windows (WDS)  

Fino alla versione 1802 per le distribuzioni PXE è necessario WDS. A partire dalla versione 1806 è possibile abilitare PXE in un punto di distribuzione senza WDS. Per altre informazioni, vedere [Servizi di distribuzione Windows](#BKMK_WDS) in questo articolo. 


### <a name="dynamic-host-configuration-protocol-dhcp"></a>Dynamic Host Configuration Protocol (DHCP)  

DHCP è necessario per le distribuzioni PXE. È necessario un server DHCP funzionante con un host attivo per distribuire i sistemi operativi utilizzando PXE. Per altre informazioni sulle distribuzioni PXE, vedere [Usare PXE per distribuire Windows in rete](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  


### <a name="supported-operating-systems-and-hard-disk-configurations"></a>Sistemi operativi supportati e configurazioni del disco rigido  

Per altre informazioni sulle versioni del sistema operativo e sulle configurazioni del disco rigido supportate da Configuration Manager per la distribuzione di sistemi operativi, vedere [Sistemi operativi supportati](#BKMK_SupportedOS) e [Configurazioni supportate per i dischi](#BKMK_SupportedDiskConfig).  


### <a name="windows-device-drivers"></a>Driver di dispositivo Windows  

Quando si installa Windows nel computer di destinazione, è possibile usare i driver di dispositivo di Windows. È possibile usare questi driver anche quando si esegue Windows PE in un'immagine d'avvio. Per altre informazioni, vedere [Gestire i driver](../get-started/manage-drivers.md).  



##  <a name="configuration-manager-dependencies"></a><a name="BKMK_InternalDependencies"></a> Dipendenze di Configuration Manager  

Questa sezione offre informazioni sui prerequisiti di distribuzione del sistema operativo di Configuration Manager.  


### <a name="os-image"></a>Immagine del sistema operativo  

Le immagini del sistema operativo in Configuration Manager vengono archiviate nel formato di file Windows Imaging (WIM). Tali immagini costituiscono una raccolta compressa di cartelle e file di riferimento e sono necessarie per installare e configurare correttamente un sistema operativo in un computer. Per altre informazioni, vedere [Gestire le immagini del sistema operativo](../get-started/manage-operating-system-images.md).  


### <a name="driver-catalog"></a>Catalogo driver  

Per distribuire un driver di dispositivo, importare tale driver, attivarlo e renderlo disponibile in un punto di distribuzione accessibile al client di Configuration Manager. Per altre informazioni sul catalogo driver, vedere [Gestire i driver](../get-started/manage-drivers.md).  


### <a name="management-point"></a>Punto di gestione  

I punti di gestione trasferiscono le informazioni tra i client e il sito di Configuration Manager. I client usano un punto di gestione per eseguire la sequenza di attività per completare la distribuzione del sistema operativo. Per altre informazioni sulle sequenze di attività, vedere [Considerazioni sulla pianificazione dell'automazione delle attività](planning-considerations-for-automating-tasks.md).  


### <a name="distribution-point"></a>Punto di distribuzione  

I punti di distribuzione vengono usati nella maggior parte delle distribuzioni per archiviare i dati usati per distribuire un sistema operativo, ad esempio il pacchetto dell'immagine o dei driver. In genere, per distribuire il sistema operativo le sequenze di attività recuperano i dati da un punto di distribuzione. Per altre informazioni su come installare i punti di distribuzione e gestire il contenuto, vedere [Gestire il contenuto e l'infrastruttura del contenuto](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  


### <a name="pxe-enabled-distribution-point"></a>Punto di distribuzione che supporta PXE  

Per distribuire le distribuzioni avviate da PXE, configurare un punto di distribuzione in modo che accetti le richieste PXE inviate dai client. Per altre informazioni, vedere [Configurare un punto di distribuzione](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).


### <a name="multicast-enabled-distribution-point"></a>Punto di distribuzione abilitato per multicast  

Per ottimizzare le distribuzioni del sistema operativo tramite multicast, configurare un punto di distribuzione per il supporto di questa funzionalità. Per altre informazioni, vedere [Configurare un punto di distribuzione](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-multicast).   


### <a name="state-migration-point"></a>Punto di migrazione stato  

Quando vengono acquisiti e ripristinati i dati sullo stato dell'utente per distribuzioni side-by-side e di aggiornamento, configurare un punto di migrazione stato per archiviare i dati sullo stato dell'utente in un altro computer.  

Per altre informazioni su come configurare il punto di migrazione stato, vedere [Punto di migrazione stato](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints)  

Per altre informazioni su come acquisire e ripristinare lo stato utente, vedere [Gestire lo stato utente](../get-started/manage-user-state.md).  


### <a name="reporting-services-point"></a>Punto di Reporting Services  

Per usare i report di Configuration Manager per le distribuzioni del sistema operativo, installare e configurare un punto di reporting. Per altre informazioni, vedere [Introduzione ai report](../../core/servers/manage/introduction-to-reporting.md).  


### <a name="security-permissions-for-os-deployments"></a>Autorizzazioni di sicurezza per le distribuzioni del sistema operativo  

Il ruolo di sicurezza **Gestione distribuzione del sistema operativo** è un ruolo predefinito che non può essere modificato. Tuttavia, è possibile copiare il ruolo, apportare modifiche e quindi salvare tali modifiche come un nuovo ruolo di sicurezza personalizzato. Di seguito vengono riportate alcune delle autorizzazioni che si applicano direttamente alle distribuzioni del sistema operativo:  

- **Pacchetto di immagine di avvio**: Crea, Elimina, Modifica, Modifica cartella, Sposta oggetto, Lettura, Imposta ambito di protezione  

- **Driver di dispositivo**: Crea, Elimina, Modifica, Modifica cartella, Modificare report, Sposta oggetto, Lettura, Esegui report  

- **Pacchetto driver**: Crea, Elimina, Modifica, Modifica cartella, Sposta oggetto, Lettura, Imposta ambito di protezione  

- **Immagine del sistema operativo**: Crea, Elimina, Modifica, Modifica cartella, Sposta oggetto, Lettura, Imposta ambito di protezione  

- **Pacchetto di aggiornamento del sistema operativo**: Crea, Elimina, Modifica, Modifica cartella, Sposta oggetto, Lettura, Imposta ambito di protezione  

- **Pacchetto sequenza attività**: Crea, Crea supporto per sequenza attività, Elimina, Modifica, Modifica cartella, Modifica report, Sposta oggetto, Lettura, Esegui report, Imposta ambito di protezione  

Per altre informazioni, vedere [Creare ruoli di sicurezza personalizzati](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole).  


### <a name="security-scopes-for-os-deployments"></a>Ambiti di protezione per le distribuzioni del sistema operativo  

Usare gli ambiti di protezione per consentire agli utenti amministratori di accedere agli oggetti a protezione diretta usati nelle distribuzioni del sistema operativo, quali immagini d'avvio e del sistema operativo, pacchetti di driver e pacchetti di sequenze di attività. Per altre informazioni, vedere [Ambiti di protezione](../../core/understand/fundamentals-of-role-based-administration.md#bkmk_PlanScope).  



##  <a name="windows-deployment-services"></a><a name="BKMK_WDS"></a> Servizi di distribuzione Windows  

Fino alla versione 1802 è necessario installare Servizi di distribuzione Windows (WDS) nello stesso server dei punti di distribuzione configurati per il supporto di multicast o PXE. WDS è incluso nel sistema operativo server. Per le distribuzioni PXE, WDS è il servizio che esegue l'avvio PXE. Quando il punto di distribuzione viene installato e attivato per PXE, Configuration Manager installa un provider in WDS che usa le funzioni di avvio PXE di WDS.  

A partire dalla versione 1806 è possibile abilitare PXE in un punto di distribuzione senza WDS. Per altre informazioni, vedere l'opzione **Abilita un risponditore PXE senza i Servizi di distribuzione Windows** in [Installare e configurare punti di distribuzione](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).


> [!NOTE]  
>  Se il server richiede un riavvio, l'installazione di WDS potrebbe non riuscire. 


### <a name="wds-requirements"></a>Requisiti di WDS  

-   Per l'installazione di WDS nel server è necessario che l'amministratore sia un membro del gruppo Administrators locale.  

-   È necessario che il server di WDS sia membro di un dominio Active Directory oppure controller di dominio per un dominio Active Directory. Tutte le configurazioni della foresta e del dominio di Windows supportano WDS.  

-   Se il provider è installato in un server remoto, installare WDS nel server del sito e nel provider remoto.  


###  <a name="considerations-when-you-have-wds-and-dhcp-on-the-same-server"></a><a name="BKMK_WDSandDHCP"></a> Considerazioni in presenza di Servizi di distribuzione Windows e DHCP nello stesso server  

Se si prevede di co-ospitare il punto di distribuzione in un server che esegue DHCP, valutare i problemi di configurazione seguenti:  

-   È necessario disporre di un server DHCP funzionante con un ambito attivo. WDS usa PXE, che richiede un server DHCP.  

-   Per eseguire WDS è necessario un server DNS.  

-   Nel server WDS devono essere aperte le porte UDP seguenti:  

    -   Porta 67 (DHCP)  

    -   Porta 69 (TFTP)  

    -   Porta 4011 (PXE)  

    > [!NOTE]  
    >  Se è necessaria l'autorizzazione DHCP per il server, occorre che la porta 68 del client DHCP nel server sia aperta.  

-   DHCP e WDS richiedono entrambi il numero di porta 67. Se WDS e DHCP sono co-ospitati, è possibile spostare DHCP o il punto di distribuzione configurato per PXE in un server separato. In alternativa, è possibile usare la procedura seguente per configurare il server WDS in modo che sia in ascolto su una porta diversa.  

#### <a name="to-configure-the-wds-server-to-listen-on-a-different-port"></a>Per configurare il server WDS in modo che sia in ascolto su una porta diversa  

1.  Modificare la seguente chiave del Registro di sistema:  

     `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WDSServer\Providers\WDSPXE`  

2.  Impostare il valore del Registro di sistema **UseDHCPPorts** su **0**.  

3.  Affinché la nuova configurazione abbia effetto, è necessario eseguire il comando seguente sul server:  

     `WDSUTIL /Set-Server /UseDHCPPorts:No /DHCPOption60:Yes`  

> [!NOTE]
> Nella versione 1810 e precedenti non è supportato l'uso del risponditore PXE senza WDS nei server che eseguono anche un server DHCP.
>
> A partire dalla versione 1902, quando si abilita un risponditore PXE in un punto di distribuzione senza i Servizi di distribuzione Windows, è ora possibile abilitarlo sullo stesso server del servizio DHCP. Per altre informazioni, vedere [Configurare almeno un punto di distribuzione per accettare le richieste PXE](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md#BKMK_Configure).


##  <a name="supported-operating-systems"></a><a name="BKMK_SupportedOS"></a> Sistemi operativi supportati  

Tutti i sistemi operativi Windows indicati come client supportati in [Sistemi operativi supportati per client e dispositivi](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md) sono supportati per la distribuzione del sistema operativo.  



##  <a name="supported-disk-configurations"></a><a name="BKMK_SupportedDiskConfig"></a> Configurazioni supportate per i dischi  

Le combinazioni di configurazioni di dischi rigidi nei computer di riferimento e di destinazione supportate per la distribuzione del sistema operativo con Configuration Manager sono visualizzate nella tabella seguente:  

|Configurazione del disco rigido del computer di riferimento|Configurazione del disco rigido del computer di destinazione|  
|------------------------------------------------|--------------------------------------------------|  
|Disco di base|Disco di base|  
|Volume semplice su un disco dinamico|Volume semplice su un disco dinamico|  

Configuration Manager supporta l'acquisizione di un'immagine del sistema operativo solo da computer configurati con volumi semplici. Le configurazioni di dischi rigidi seguenti non sono supportate:  

-   Volumi con spanning  

-   Volumi con striping (RAID 0)  

-   Volumi con mirroring (RAID 1)  

-   Volumi di parità (RAID 5)  

La tabella seguente elenca una configurazione di disco rigido aggiuntiva per i computer di riferimento e di destinazione non supportata con la distribuzione del sistema operativo di Configuration Manager.  

|Configurazione del disco rigido del computer di riferimento|Configurazione del disco rigido del computer di destinazione|  
|------------------------------------------------|--------------------------------------------------|  
|Disco di base|Disco dinamico|  



## <a name="next-steps"></a>Passaggi successivi

- [Preparare i ruoli del sistema del sito per le distribuzioni del sistema operativo](../get-started/prepare-site-system-roles-for-operating-system-deployments.md)
- [Preparativi per la distribuzione del sistema operativo](../get-started/prepare-for-operating-system-deployment.md)
