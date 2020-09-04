---
title: Funzionalità nella Technical Preview 1511
titleSuffix: Configuration Manager
description: Informazioni sulle funzionalità disponibili nella versione Technical Preview 1511 per Configuration Manager.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 69473706-21b3-498b-a67e-670fdc988f0d
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: a7b61e1a609e0693ffcd30f3f7dc931f4cb38eef
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193639"
---
# <a name="capabilities-in-technical-preview-1511-for-configuration-manager"></a>Funzionalità della versione Technical Preview 1511 per Configuration Manager

*Si applica a: Configuration Manager (Technical Preview Branch)*

Questo articolo presenta le funzionalità disponibili nella Technical Preview per Configuration Manager versione 1511. Questa versione è un'installazione di base per la Technical Preview che è possibile usare per installare un nuovo sito Technical Preview o per eseguire l'aggiornamento da una Technical Preview precedente.   Prima di installare questa versione Technical Preview, consultare l'argomento introduttivo [Technical Preview per Center Configuration Manager](technical-preview.md) per acquisire familiarità con i requisiti generali e con le limitazioni per l'uso di una versione Technical Preview, con le modalità di aggiornamento tra le versioni e con le modalità per offrire commenti e suggerimenti sulle funzionalità di una versione Technical Preview.  

Di seguito sono riportate le nuove funzionalità disponibili con questa versione.  

##  <a name="integration-with-windows-update-for-business-in-windows-10"></a><a name="BKMK_WUfB"></a> Integrazione con Windows Update for Business in Windows 10  
 Configuration Manager ora può distinguere un computer Windows 10 che è direttamente connesso tramite Windows Update for Business (WUfB) da quelli connessi a WSUS per ottenere gli aggiornamenti di Windows 10.  Per i computer connessi tramite WUfB, gli aggiornamenti possono essere gestiti secondo la cadenza impostata da un utente amministratore in Criteri di gruppo o Criteri MDM. Gli aggiornamenti potranno essere installati direttamente da WUfB.    
Per i computer connessi tramite WUfB, Configuration Manager non potrà segnalare lo stato di conformità (inclusi gli aggiornamenti di Windows o gli aggiornamenti delle definizioni). Inoltre, Configuration Manager non potrà distribuire aggiornamenti Microsoft o aggiornamenti di terze parti in questi computer.  

 **Prerequisiti per questo scenario:**  

-   Windows 10 Desktop Pro o Windows 10 Enterprise Edition versione 1511 o successive  

-   Computer da gestire tramite [Windows Update for Business](/windows/deployment/update/waas-manage-updates-wufb).  

### <a name="try-it-out"></a>Verifica  
 Prova a completare l'attività seguente e quindi usa le informazioni relative a commenti e suggerimenti nella parte superiore di questo argomento per comunicare i risultati:  

1.  Disabilitare l'agente di Windows Update in modo che non esegua l'analisi rispetto a WSUS, se è stata precedentemente abilitata.   
    La chiave del Registro di sistema **HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU\useWSUSServer** può essere impostata in modo da indicare se il computer sta eseguendo l'analisi rispetto a Windows Update o WSUS.  Se il valore è 2, l'analisi non viene eseguita rispetto a WSUS.  

2.  Prendere nota del nuovo attributo **UseWUServer**, nel nodo **Windows Update** di Esplora inventario risorse di Configuration Manager.  

3.  Creare una raccolta sulla base dell'attributo **UseWUServer** per tutti i computer connessi tramite WUfB per gli aggiornamenti.  

4.  Creare un'impostazione dell'agente client per disabilitare il flusso di lavoro di aggiornamento software e distribuire l'impostazione nella raccolta di computer connessi direttamente a WUfB.  

5.  Lo stato di conformità dei computer gestiti tramite Windows Update for Business sarà **Sconosciuto** e quindi questi non verranno conteggiati come parte della percentuale di conformità complessiva.  

##  <a name="managing-microsoft-365-apps-for-enterprise-client-update-through-configuration-manager"></a><a name="BKMK_Office365ProPlus"></a> Gestione degli aggiornamenti client di Microsoft 365 Apps for enterprise tramite Configuration Manager  
Configuration Manager consente ora di gestire gli aggiornamenti dei client desktop di Microsoft 365 usando il flusso di lavoro Gestione aggiornamenti software di Configuration Manager.
Quando Microsoft pubblica un nuovo aggiornamento dei client desktop di Microsoft 365 in Windows Server Updates Services (WSUS), Configuration Manager potrà sincronizzare l'aggiornamento con il relativo catalogo se l'aggiornamento di Microsoft 365 è configurato come parte della sincronizzazione del catalogo.  Il server del sito di Configuration Manager scaricherà gli aggiornamenti client di Microsoft 365 e distribuirà il pacchetto ai punti di distribuzione di Configuration Manager.  Il client di Configuration Manager indicherà quindi ai client desktop di Microsoft 365 dove ottenere gli aggiornamenti e quando avviarne il processo di installazione.  

**Prerequisiti per questo scenario:**  

### <a name="try-it-out"></a>Verifica  
 Prova a completare l'attività seguente e quindi usa le informazioni relative a commenti e suggerimenti nella parte superiore di questo argomento per comunicare i risultati:  

1. È possibile sincronizzare gli aggiornamenti di Microsoft 365 con il server del sito di Configuration Manager e visualizzarli dalla console di Configuration Manager.  

2. È possibile approvare e distribuire correttamente gli aggiornamenti di Microsoft 365.  

3. È possibile scaricare correttamente gli aggiornamenti di Microsoft 365 nei client.  

4. È possibile verificare la conformità degli aggiornamenti di Microsoft 365 usando il monitoraggio integrato nella console o i report.  

   Per istruzioni dettagliate, vedere [Gestire gli aggiornamenti del client di Microsoft 365 con Configuration Manager Technical Preview](/deployoffice/manage-microsoft-365-apps-updates-configuration-manager).  

##  <a name="support-for-sql-server-alwayson-for-highly-available-databases"></a><a name="BKMK_AlwasyOn"></a> Supporto per SQL Server AlwaysOn per database a disponibilità elevata  
 Configuration Manager ora supporta l'utilizzo di un gruppo di disponibilità SQL Server AlwaysOn per ospitare il database del sito.  Quando si installa un nuovo sito, è possibile indirizzare il programma di installazione all'uso del gruppo di disponibilità anziché una normale istanza di SQL Server.  

> [!NOTE]  
>  Per la configurazione e l'uso corretti dei gruppi di disponibilità occorre che l'utente abbia una certa familiarità con la configurazione dei gruppi di disponibilità di SQL Server, in base alla documentazione e alle procedure fornite nella libreria della documentazione di SQL Server.  

Il processo generale per configurare e usare i gruppi di disponibilità include le operazioni seguenti:  

1.  Configurazione del gruppo di disponibilità in SQL Server.  

2.  Installare un nuovo sito di Configuration Manager indicando al sito, durante l'installazione, di usare il gruppo di disponibilità specificando l'endpoint dei gruppi.  

**Prerequisiti per questo scenario:**  

-   Richiede una versione di SQL Server supportata da Configuration Manager Technical Preview  

-   È necessario creare e configurare il gruppo di disponibilità di SQL Server prima di installare Configuration Manager  

-   Il gruppo di disponibilità deve disporre di una replica primaria e può avere fino a due repliche secondarie sincrone  

-   Il gruppo di disponibilità deve disporre di almeno un endpoint  

-   È necessario disporre di un percorso di rete al quale ogni computer SQL Server nel gruppo di disponibilità sia in grado di accedere. Questo percorso viene utilizzato dal programma di installazione quando si configura il gruppo di disponibilità e può essere rimosso al termine dell'installazione.  

**Problemi noti per questa versione:**  

-   Non è possibile aggiungere correttamente un nuovo membro di replica a un gruppo di disponibilità che è già in uso come database del sito. In alternativa, è necessario reinstallare il sito dopo aver aggiunto il nuovo membro di replica.  

-   Per questo scenario potrebbe essere necessario installare il **client nativo di SQL Server 2012** ([da SQL Server 2012 Feature Pack](https://www.microsoft.com/download/details.aspx?id=29065)) nel server del punto di gestione. In questo modo vengono evitati gli errori di connessione SQL (che vengono registrati in **mp_getauth.log** nel server del punto di gestione).  

### <a name="try-it-out"></a>Verifica  
Prova a completare le attività seguenti, quindi usa le informazioni relative a commenti e suggerimenti nella parte superiore di questo argomento per comunicare i risultati:  

-   Sono in grado di installare un sito primario che utilizza un server di database configurato per i gruppi di disponibilità SQL AlwaysOn  

-   Sono riuscito a eseguire il failover del gruppo di disponibilità SQL AlwaysOn a una nuova replica del gruppo e il sito primario è ancora operativo  

### <a name="configuring-sql-server-alwayson-for-configuration-manager"></a>Configurazione di SQL Server AlwaysOn per Configuration Manager  
 Usare le procedure seguenti per creare e configurare prima di tutto il gruppo di disponibilità e quindi installare un nuovo sito di Configuration Manager che utilizza il gruppo di disponibilità.  

#### <a name="to-create-a-sql-server-alwayson-availability-group"></a>Per creare un gruppo di disponibilità SQL Server AlwaysOn  
Il processo per [creare un gruppo di disponibilità di SQL Server](/sql/database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server?view=sql-server-ver15) è documentato nella raccolta di documentazione di SQL Server.  Quando si crea il gruppo di disponibilità, verificare che siano soddisfatti i requisiti seguenti per l'uso con Configuration Manager:  

-   Un massimo di tre membri:  

    -   Una replica primaria e fino a due repliche secondarie  

    -   Le repliche secondarie devono essere sincrone.  

        > [!TIP]  
        >  È consigliabile che le repliche secondarie siano configurate per essere di sola lettura. In questo modo è possibile utilizzare una replica secondaria per funzioni quali la creazione di report mantenendo al contempo le prestazioni della replica primaria per le operazioni del sito.  

-   Almeno un endpoint. Quando si installa il sito di Configuration Manager verrà utilizzato il nome virtuale di questo endpoint.  

    > [!TIP]  
    >  Anche se il gruppo può contenere più endpoint, Configuration Manager può utilizzarne solo uno.  

#### <a name="to-install-a-configuration-manager-site-that-uses-the-availability-group"></a>Per installare un sito di Configuration Manager che utilizza il gruppo di disponibilità  
Per installare un sito che utilizza un gruppo di disponibilità di SQL Server:  

1.  Sostituire gli elementi indicati di seguito quando richiesto dal programma di installazione di Configuration Manager:  

    -   **Nome SQL Server**: immettere il nome virtuale per l'endpoint configurato al momento della creazione del gruppo di disponibilità. Il nome virtuale deve essere un nome DNS completo, ad esempio **&lt;serverEndpoint\>.fabrikam.com**.  

    -   **Istanza**:  questo valore deve rimanere vuoto. In questa configurazione non esiste alcuna istanza.  

    -   **Database**: immettere il nome del database creato nella replica primaria del gruppo di disponibilità.  

2.  Successivamente, è necessario fornire un percorso di rete al quale ciascun SQL Server del gruppo sia in grado di accedere:  

    -   L'account computer e l’account di servizio da ogni computer SQL Server richiedono l'accesso con controllo completo a questo percorso.  

    -   Questo percorso viene utilizzato solo durante l'installazione ed è possibile rimuoverne la condivisione oppure eliminarlo al termine della configurazione e dell'installazione del sito.  

3.  Dopo aver fornito queste informazioni, completare l'installazione con il processo e le configurazioni normali.  

##  <a name="service-a--server-cluster"></a><a name="BKMK_ClusterServerUpdates"></a> Eseguire la manutenzione di un cluster di server  
Ora è possibile creare una raccolta che contiene i server in un cluster e quindi configurare le impostazioni del cluster da utilizzare quando si distribuiscono gli aggiornamenti al cluster. È possibile controllare la percentuale di server che sono in linea in dato momento, oltre che configurare script PowerShell di pre-distribuzione e post-distribuzione per eseguire azioni personalizzate.  

**Problemi noti per questa versione:**  

-   La creazione di report non è disponibile per controllare lo stato della distribuzione degli aggiornamenti software per i server del cluster.  

-   L'opzione della sequenza di manutenzione nella pagina **Impostazioni cluster** è disabilitata e non è disponibile in questa release.  

### <a name="try-it-out"></a>Verifica  
Prova a completare l'attività seguente e quindi usa le informazioni relative a commenti e suggerimenti nella parte superiore di questo argomento per comunicare i risultati:  

-   Sono in grado di creare una raccolta che rappresenta un cluster di server. Per questo test, è possibile configurare le regole di appartenenza alla raccolta in modo che nella raccolta siano presenti 2 macchine.  

-   Sono in grado di specificare che solo il 50% dei server del cluster può essere offline in qualsiasi punto della manutenzione del cluster. Utilizzare gli script di esempio nella procedura per specificare gli script di pre-distribuzione e post-distribuzione.  

-   Distribuire un aggiornamento a questa raccolta. Esaminare i file start.txt ed end.txt in C:\temp e verificare l'ora di inizio e fine per la distribuzione nei server del cluster. Esaminare il file UpdatesDeployment.log per ulteriori informazioni.  

#### <a name="to-create-a-collection-for-a-server-cluster"></a>Per creare una raccolta per un cluster di server  

1.  [Creare una raccolta di dispositivi](../clients/manage/collections/create-collections.md) che contenga i server nel cluster.  

2.  Nell'area di lavoro **Asset e conformità** fare clic su **Raccolte di dispositivi**, quindi fare clic con il pulsante destro del mouse sulla raccolta che contiene i server nel cluster e scegliere **Proprietà**.  

3.  Nella scheda **Generale** selezionare **Tutti i dispositivi fanno parte dello stesso cluster di server**, quindi fare clic su **Impostazioni**.  

4.  Nella pagina **Impostazioni cluster** selezionare la percentuale di server che possono essere portati offline contemporaneamente per l'installazione di aggiornamenti software. È possibile portare offline un server del cluster alla volta indipendentemente dalla percentuale specificata. Configuration Manager eseguirà l'arrotondamento per difetto quando si seleziona il numero di server di cui eseguire la manutenzione contemporaneamente. Ad esempio, se si sceglie il 51% e nel cluster sono presenti 4 server, verranno portati offline contemporaneamente 2 server.  

5.  Specificare se usare uno script di pre-distribuzione (svuotamento del nodo) o di post-distribuzione (ripresa del nodo).  

    > [!TIP]  
    >  Di seguito sono riportati alcuni esempi che è possibile usare nei test degli script di pre-distribuzione e post-distribuzione, con cui viene scritta l'ora corrente in un file di testo:  
    >   
    >  **Pre-distribuzione**  
    >   
    >  `#Start`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\start.txt`  
    >   
    >  **Post-distribuzione**  
    >   
    >  `#End`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\end.txt`  

#### <a name="to-deploy-software-updates-to-the-server-cluster"></a>Per distribuire gli aggiornamenti software nel cluster di server  

1.  [Distribuire gli aggiornamenti software](../../sum/deploy-use/deploy-software-updates.md) nella raccolta del cluster di server.  

2.  [Monitorare la distribuzione degli aggiornamenti software](../../sum/deploy-use/monitor-software-updates.md).