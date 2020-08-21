---
title: Eseguire la migrazione di oggetti
titleSuffix: Configuration Manager
description: Informazioni su come pianificare la migrazione di oggetti tra le gerarchie in un ambiente di Configuration Manager Current Branch.
ms.date: 01/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 066caf00-e419-4efb-93d3-ba4ba878297c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 996cff4b8b333a59b774afb979bbdd89aae536a1
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692894"
---
# <a name="plan-for-the-migration-of-configuration-manager-objects-to-configuration-manager-current-branch"></a>Pianificare la migrazione degli oggetti di Configuration Manager a Configuration Manager Current Branch

*Si applica a: Configuration Manager (Current Branch)*

Con Configuration Manager Current Branch è possibile eseguire la migrazione di molti oggetti diversi associati a funzionalità diverse in un sito di origine.

##  <a name="plan-to-migrate-software-updates"></a><a name="Plan_migrate_Software_updates"></a> Pianificare la migrazione degli aggiornamenti software  
 È possibile eseguire la migrazione degli oggetti di aggiornamento software, ad esempio i pacchetti di aggiornamento software e le distribuzioni di aggiornamento software.  

 Per eseguire la migrazione degli oggetti di aggiornamento software, è necessario configurare la gerarchia di destinazione con configurazioni corrispondenti all'ambiente della gerarchia di origine. Questa operazione richiede le seguenti azioni:  

-   Distribuire un punto di aggiornamento software attivo nella gerarchia di destinazione  

-   Configurare il catalogo dei prodotti e le lingue in modo che corrispondano alla configurazione della gerarchia di origine  

-   Sincronizzare il punto di aggiornamento software nella gerarchia di destinazione con Windows Server Update Services (WSUS)  

Quando si esegue la migrazione degli aggiornamenti software, tenere in considerazione quanto segue:  

-   La migrazione degli oggetti di aggiornamento software può avere esito negativo se le informazioni nella gerarchia di destinazione non sono state sincronizzate in modo che corrispondano alla configurazione della gerarchia di origine.  

    > [!WARNING]  
    >  Configuration Manager non supporta l'uso dello strumento WSUSutil per sincronizzare i dati tra una gerarchia di origine e di destinazione.  

-   È possibile eseguire la migrazione degli aggiornamenti personalizzati che vengono pubblicati tramite System Center Updates Publisher. Al contrario, gli aggiornamenti personalizzati devono essere ripubblicati nella gerarchia di destinazione.  

Quando si esegue una migrazione da una gerarchia di origine di Configuration Manager 2007, il processo di migrazione modifica alcuni oggetti di aggiornamento software nel formato usato dalla gerarchia di destinazione. Usare la tabella seguente per pianificare la migrazione degli oggetti di aggiornamento software da Configuration Manager 2007.  

|Oggetto di Configuration Manager 2007|Nome dell'oggetto dopo la migrazione|  
|-----------------------------------|---------------------------------|  
|Elenchi di aggiornamenti software|Gli elenchi di aggiornamenti software vengono convertiti in gruppi di aggiornamento software.|  
|Distribuzioni di aggiornamenti software|Le distribuzioni di aggiornamenti software vengono convertite in distribuzioni e gruppi di aggiornamento.<br /><br /> Dopo aver eseguito la migrazione di una distribuzione di aggiornamento software da Configuration Manager 2007, è necessario abilitarla nella gerarchia di destinazione prima di poterla distribuire.|  
|Pacchetti di aggiornamento software|I pacchetti di aggiornamento software rimangono pacchetti di aggiornamento software.|  
|Modelli di aggiornamento software|I modelli di aggiornamento software rimangono modelli di aggiornamento software.<br /><br /> Non viene eseguita la migrazione del valore **Durata** nei modelli di distribuzione di Configuration Manager 2007.|  

Quando si esegue la migrazione di oggetti dalla gerarchia di origine di System Center 2012 Configuration Manager o di Configuration Manager Current Branch, gli oggetti degli aggiornamenti software non vengono modificati.  

##  <a name="plan-to-migrate-content"></a><a name="Plan_Migrate_content"></a> Pianificare la migrazione del contenuto  
 È possibile eseguire la migrazione del contenuto da una gerarchia di origine supportata alla gerarchia di destinazione. Per una gerarchia di origine di Configuration Manager 2007, il contenuto include i pacchetti e i programmi di distribuzione software e le applicazioni virtuali, ad esempio Microsoft Application Virtualization (App-V). Per le gerarchie di origine di System Center 2012 Configuration Manager e Configuration Manager Current Branch, il contenuto include applicazioni e applicazioni virtuali App-V. Quando si esegue la migrazione del contenuto tra le gerarchie, viene eseguita la migrazione dei file di origine compressi nella gerarchia di destinazione.  

### <a name="packages-and-programs"></a>Pacchetti e programmi  
 Quando si esegue la migrazione di pacchetti e programmi, non vengono modificati dalla migrazione. Tuttavia, prima di eseguirne la migrazione, è necessario configurare i pacchetti per usare un percorso UNC (Universal Naming Convention) come percorso di file di origine. Come parte della configurazione per la migrazione di pacchetti e programmi, è necessario assegnare un sito per la gestione del contenuto nella gerarchia di destinazione. Non viene eseguita la migrazione dal sito assegnato, ma dopo la migrazione il sito assegnato accede al percorso del file di origine usando il mapping UNC.  

 Quando si esegue la migrazione di un pacchetto e di un programma nella gerarchia di destinazione e mentre la migrazione dalla gerarchia di origine rimane attiva, è possibile rendere il contenuto disponibile ai client nella gerarchia usando un punto di distribuzione condiviso. Per usare un punto di distribuzione condiviso, il contenuto deve rimanere accessibile nel punto di distribuzione del sito di origine. Per altre informazioni sui punti di distribuzione condivisi, vedere [Condividere punti di distribuzione tra gerarchie di origine e destinazione](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration) in [Pianificare una strategia di migrazione per la distribuzione del contenuto](../../core/migration/planning-a-content-deployment-migration-strategy.md).  

 Per il contenuto di cui è stata eseguita la migrazione, se la versione del contenuto viene modificata nella gerarchia di origine o in quella di destinazione, i client non potranno più accedere al contenuto dal punto di distribuzione condiviso nella gerarchia di destinazione. In questo scenario, è necessario eseguire nuovamente la migrazione del contenuto per ripristinare una versione coerente del pacchetto tra la gerarchia di origine e quella di destinazione. Queste informazioni vengono sincronizzate durante il ciclo di raccolta dati.  

> [!TIP]  
>  Per ogni pacchetto di cui si esegue la migrazione, aggiornare il pacchetto nella gerarchia di destinazione. Questo può evitare problemi di distribuzione del pacchetto nei punti di distribuzione nella gerarchia di destinazione. Tuttavia, quando si aggiorna un pacchetto nel punto di distribuzione nella gerarchia di destinazione, i client in tale gerarchia non riusciranno più a ottenere il pacchetto da un punto di distribuzione condiviso. Per aggiornare un pacchetto nella gerarchia di destinazione, nella console di Configuration Manager passare alla Raccolta software, fare clic con il pulsante destro del mouse sul pacchetto e scegliere **Aggiorna punti di distribuzione**. Ripetere questa operazione per ogni pacchetto di cui si esegue la migrazione.  

> [!TIP]  
> Usare Package Conversion Manager per convertire pacchetti e programmi in applicazioni in Configuration Manager. Per altre informazioni, vedere [Package Conversion Manager](../../apps/pcm/package-conversion-manager.md).  

### <a name="virtual-applications"></a>Applicazioni virtuali  
Quando si esegue la migrazione dei pacchetti App-V da un sito supportato di Configuration Manager 2007, il processo di migrazione li converte in applicazioni nella gerarchia di destinazione. Inoltre, in base agli annunci esistenti per il pacchetto App-V, è possibile creare i seguenti tipi di distribuzione nella gerarchia di destinazione:  

-   Se non sono presenti annunci, viene creato un tipo di distribuzione che usa le impostazioni predefinite del tipo di distribuzione.  

-   Se è presente un annuncio, viene creato un tipo solo di distribuzione che usa le stesse impostazioni dell'annuncio di Configuration Manager 2007.  

-   Se sono presenti più annunci, viene creato un tipo di distribuzione per ogni annuncio di Configuration Manager 2007 usando le impostazioni per tale annuncio.  

> [!IMPORTANT]  
>  Se si esegue la migrazione di un pacchetto App-V di Configuration Manager 2007 di cui è stata eseguita prima la migrazione, la migrazione avrà esito negativo perché i pacchetti delle applicazioni virtuali non supportano il comportamento di sovrascrittura della migrazione. In questo scenario è necessario eliminare il pacchetto di applicazioni virtuali di cui è stata eseguita la migrazione dalla gerarchia di destinazione e quindi creare un nuovo processo di migrazione per eseguire la migrazione dell'applicazione virtuale.  

> [!NOTE]  
>  Dopo la migrazione di un pacchetto App-V, è possibile usare l'Aggiornamento guidato contenuto per modificare il percorso di origine per i tipi di distribuzione di App-V. Per altre informazioni su come aggiornare il contenuto per un tipo di distribuzione, vedere Come gestire i tipi di distribuzione in [Attività di gestione per applicazioni di Configuration Manager](../../apps/deploy-use/management-tasks-applications.md).  

Quando si esegue la migrazione da una gerarchia di origine di System Center 2012 Configuration Manager o Configuration Manager Current Branch, è possibile eseguire la migrazione di oggetti per l'ambiente virtuale App-V oltre che di tipi e applicazioni di distribuzione App-V. Per altre informazioni sugli ambienti App-V, vedere [Distribuzione di applicazioni virtuali App-Vr](../../apps/get-started/deploying-app-v-virtual-applications.md).  

### <a name="advertisements"></a>Annunci  
È possibile eseguire la migrazione degli annunci da un sito di origine supportato di Configuration Manager 2007 alla gerarchia di destinazione usando la migrazione basata su raccolte. Se si aggiorna un client, verrà mantenuta la cronologia degli annunci eseguiti in precedenza per impedire che il client esegua nuovamente gli annunci migrati.  

> [!NOTE]  
>  Non è possibile eseguire la migrazione di annunci per i pacchetti virtuali. Si tratta di un'eccezione alla migrazione degli annunci.  

### <a name="applications"></a>Applicazioni  
 È possibile eseguire la migrazione di applicazioni da una gerarchia di origine supportata di System Center 2012 Configuration Manager o Configuration Manager Current Branch a una gerarchia di destinazione. Se si riassegna un client dalla gerarchia di origine alle gerarchia di destinazione, il client mantiene la cronologia delle applicazioni precedentemente installate per evitare che il client esegua di nuovo l'applicazione migrata.  

##  <a name="plan-to-migrate-collections"></a><a name="BKMK_MigrateCollections"></a> Pianificare la migrazione delle raccolte  
 È possibile eseguire la migrazione dei criteri per le raccolte da una gerarchia di origine supportata di System Center 2012 Configuration Manager o Configuration Manager Current Branch. A tale scopo, si usa un processo di migrazione basato su oggetti. Quando si esegue la migrazione di una raccolta, vengono trasferite le regole per la raccolta e non le informazioni relative ai membri della raccolta o informazioni o oggetti relativi ai membri della raccolta.  

 La migrazione dell'oggetto della raccolta non è supportata quando si esegue la migrazione da una gerarchia di origine di Configuration Manager 2007.  

##  <a name="plan-to-migrate-operating-system-deployments"></a><a name="Plan_migrate_OSD"></a> Pianificare la migrazione delle distribuzioni del sistema operativo  
È possibile eseguire la migrazione dei seguenti oggetti della distribuzione del sistema operativo da una gerarchia di origine supportata:  

-   Immagini del sistema operativo e pacchetti. Il percorso di origine delle immagini di avvio viene aggiornato con il percorso dell'immagine predefinito per Windows Administrative Installation Kit (Windows AIK) nel sito di destinazione. Di seguito sono riportati i requisiti e le limitazioni alla migrazione delle immagini del sistema operativo e dei pacchetti:  

    -   Per eseguire la migrazione dei file di immagine, l'account computer del server del provider SMS per il sito di livello superiore della gerarchia di destinazione deve avere le autorizzazioni di **Lettura** e **Scrittura** nei file di origine dell'immagine del percorso Windows AIK dei siti di origine.  

    -   Quando si esegue la migrazione del pacchetto di installazione del sistema operativo, verificare che la configurazione del pacchetto nel sito di origine faccia riferimento alla cartella che contiene il file WIM e non direttamente al file WIM. Se il pacchetto di installazione fa riferimento al file WIM, la migrazione del pacchetto di installazione avrà esito negativo.  

    -   Quando viene eseguita la migrazione del pacchetto di immagini di avvio da un sito di origine supportato di Configuration Manager 2007, l'ID pacchetto non viene mantenuto nel sito di destinazione. Il risultato è che i client nella gerarchia di destinazione non possono usare i pacchetti di immagini di avvio disponibili nei punti di distribuzione condivisa.  

-   Sequenze attività. Quando si esegue la migrazione di una sequenza di attività che contiene un riferimento a un pacchetto di installazione client, il riferimento viene sostituito da un riferimento al pacchetto di installazione client della gerarchia di destinazione.  

    > [!NOTE]  
    >  Quando si esegue la migrazione di una sequenza di attività, Configuration Manager potrebbe trasferire oggetti che non sono necessari nella gerarchia di destinazione. Questi oggetti includono le immagini di avvio e i pacchetti di installazione client di Configuration Manager 2007.  

-   Driver e pacchetti driver. Quando si esegue la migrazione di pacchetti driver, l'account computer del Provider SMS nella gerarchia di destinazione deve avere il pieno controllo all'origine del pacchetto.

##  <a name="plan-to-migrate-desired-configuration-management"></a><a name="Plan_Migrate_Compliance_settings"></a> Pianificare la migrazione della gestione configurazione desiderata  
È possibile eseguire la migrazione di elementi e linee di base di configurazione.  

> [!NOTE]  
>  Gli elementi di configurazione non interpretati delle gerarchie di origine di Configuration Manager 2007 non sono supportati per la migrazione. Non è possibile eseguire la migrazione o importare questi elementi di configurazione nella gerarchia di destinazione. Per altre informazioni sugli elementi di configurazione non interpretati, vedere Uninterpreted Configuration Item (Elemento di configurazione non interpretato) nell'argomento [About Configuration Items in Desired Configuration Management](/previous-versions/system-center/configuration-manager-2007/bb694136(v=technet.10)#uninterpreted-configuration-item) (Informazioni sugli elementi di configurazione nella gestione configurazione desiderata) nella libreria della documentazione di Configuration Manager 2007.  

È possibile importare pacchetti di configurazione di Configuration Manager 2007. Il processo di importazione converte automaticamente i pacchetti di configurazione in un formato compatibile con Configuration Manager Current Branch.  

##  <a name="plan-to-migrate-boundaries"></a><a name="Plan_migrate_Boundaries"></a> Pianificare la migrazione dei limiti  
 È possibile eseguire la migrazione di limiti da una gerarchia all'altra. Quando si esegue la migrazione di limiti da Configuration Manager 2007, ogni limite del sito di origine viene sottoposto a migrazione allo stesso tempo e viene aggiunto a un nuovo gruppo di limiti creato nella gerarchia di destinazione. Quando si esegue la migrazione di limiti da una gerarchia di System Center 2012 Configuration Manager o Configuration Manager Current Branch, ogni limite selezionato viene aggiunto a un nuovo gruppo di limiti nella gerarchia di destinazione.  

 Ogni gruppo di limiti creato automaticamente viene abilitato per la posizione del contenuto ma non per l'assegnazione di siti. Ciò consente di evitare la sovrapposizione di limiti per le assegnazioni di siti tra le gerarchie di origine e di destinazione. Se si esegue la migrazione da un sito di origine di Configuration Manager 2007, ciò evita che i nuovi client Configuration Manager 2007 installati vengano assegnati erroneamente alla gerarchia di destinazione. Per impostazione predefinita, i client di Configuration Manager Current Branch non vengono assegnati automaticamente a siti di Configuration Manager 2007.  

 Durante la migrazione, se si condivide un punto di distribuzione con la gerarchia di destinazione, verrà eseguita automaticamente la migrazione nella gerarchia di destinazione di eventuali limiti associati a tale distribuzione. Nella gerarchia di destinazione, la migrazione crea un nuovo gruppo di limiti di sola lettura per ogni punto di distribuzione condiviso. Se si modificano i limiti per il punto di distribuzione nella gerarchia di origine, il gruppo di limiti nella gerarchia di destinazione verrà aggiornato con tali modifiche nel corso del successivo ciclo di raccolta di dati.  

##  <a name="plan-to-migrate-reports"></a><a name="Plan_Migrate_reports"></a> Pianificare la migrazione di report  
Configuration Manager non supporta la migrazione dei report. Usare invece il Generatore report di SQL Server Reporting Services per esportare report dalla gerarchia di origine, quindi importarli nella gerarchia di destinazione.  

> [!NOTE]  
>  Poiché ci sono differenze nello schema per i report tra Configuration Manager 2007 e Configuration Manager Current Branch, testare ogni report importato da una gerarchia di Configuration Manager 2007 per assicurarsi che funzioni come previsto.  

Per altre informazioni sui report, vedere [Introduzione ai report](../servers/manage/introduction-to-reporting.md).  

##  <a name="plan-to-migrate-organizational-and-search-folders"></a><a name="Plan_Migrate_Org_Folders"></a> Pianificare la migrazione di cartelle organizzative e di ricerca  
 È possibile eseguire la migrazione di cartelle organizzative e cartelle di ricerca da una gerarchia di origine supportata a una gerarchia di destinazione. Da una gerarchia di origine di System Center 2012 Configuration Manager o Configuration Manager Current Branch, è possibile eseguire la migrazione dei criteri da una ricerca salvata a una gerarchia di destinazione.  

 Per impostazione predefinita, quando si esegue la migrazione il processo di migrazione mantiene le strutture delle cartelle di ricerca e delle cartelle amministrative per gli oggetti e per le raccolte. Nella pagina **Impostazioni** della Creazione guidata del processo di migrazione è tuttavia possibile configurare un processo di migrazione in modo che non esegua la migrazione della struttura organizzativa per gli oggetti, deselezionando la casella corrispondente a tale opzione. Le strutture organizzative delle raccolte vengono mantenute sempre.  

 Unica eccezione è una cartella di ricerca che contiene applicazioni virtuali. Quando viene eseguita la migrazione di un pacchetto App-V, tale pacchetto viene trasformato in un'applicazione in Configuration Manager. Dopo la migrazione della cartella di ricerca, verranno trovati solo i pacchetti rimanenti e la cartella di ricerca non potrà individuare alcun pacchetto App-V a causa della conversione in applicazione durante la migrazione di tale pacchetto.  

 Se si esegue la migrazione di una ricerca salvata da una gerarchia di origine di System Center 2012 Configuration Manager o Configuration Manager Current Branch, viene eseguita la migrazione dei criteri per la ricerca e non delle informazioni sui risultati della ricerca. La migrazione di una ricerca salvata non è applicabile a partire da un sito di origine di Configuration Manager 2007.  

##  <a name="plan-to-migrate-asset-intelligence-customizations"></a><a name="Plan_Migrate_AI"></a> Pianificare la migrazione delle personalizzazioni di Asset Intelligence  
 È possibile eseguire la migrazione delle personalizzazioni di Asset Intelligence da una gerarchia di origine supportata a una gerarchia di destinazione. La struttura delle personalizzazioni di Asset Intelligence non presenta modifiche significative tra Configuration Manager 2007 e Configuration Manager Current Branch.  

> [!NOTE]  
> Configuration Manager Current Branch non supporta la migrazione di oggetti di Asset Intelligence da un sito di Configuration Manager 2007 che usa Asset Intelligence Service 2.0 (AIS 2.0).  

##  <a name="plan-to-migrate-software-metering-rules-customizations"></a><a name="Plan_Migrate_SWM_Rules"></a> Pianificare la migrazione di personalizzazioni delle regole di misurazione del software  
 La misurazione del software non presenta modifiche significative tra Configuration Manager 2007 e Configuration Manager Current Branch. È possibile eseguire la migrazione delle regole di controllo software da una gerarchia di origine supportata a una gerarchia di destinazione.  

 Per impostazione predefinita, le regole di controllo software di cui viene eseguita la migrazione in una gerarchia di destinazione non sono associate ad alcun sito specifico nella gerarchia di destinazione, ma vengono invece applicate a tutti i client della gerarchia. Per applicare una regola di controllo software ai client di un sito specifico, è necessario modificare la regola di controllo dopo la migrazione.