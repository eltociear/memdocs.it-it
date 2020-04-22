---
title: Elenco di controllo per la versione 1802
titleSuffix: Configuration Manager
description: Informazioni sulle azioni da intraprendere prima di eseguire l'aggiornamento di Configuration Manager alla versione 1802.
ms.date: 06/08/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6af92de2-b2c7-4d5c-affd-6cce81979fb5
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: f9c0c44d6a5f3921fd9a2ea4292e94cff1fa7d9f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707679"
---
# <a name="checklist-for-installing-update-1802-for-configuration-manager"></a>Elenco di controllo per l'installazione dell'aggiornamento 1802 di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Quando si usa la versione Current Branch di Configuration Manager, è possibile installare l'aggiornamento nella console per la versione 1802 per aggiornare la gerarchia da una versione precedente. <!-- baseline only statement: -->Dal momento che la versione 1802 è disponibile anche come [supporto di base](updates.md#bkmk_Baselines), è possibile usare il supporto di installazione per installare il primo sito di una nuova gerarchia.

Per ottenere l'aggiornamento per la versione 1802, è necessario usare un punto di connessione del servizio nel sito principale della gerarchia. Questo ruolo del sistema del sito può essere in modalità online o offline. Dopo che la gerarchia ha scaricato il pacchetto di aggiornamento da Microsoft, questo è disponibile all'interno della console all'interno dell'area di lavoro **Amministrazione** , nel nodo **Aggiornamenti e manutenzione**.

-   Quando l'aggiornamento risulta **Disponibile**, è pronto per l'installazione. Prima di installare la versione 1802, leggere le informazioni seguenti [sull'installazione dell'aggiornamento 1802](#about-installing-update-1802) e l'[elenco di controllo](#checklist) delle configurazioni da eseguire prima dell'avvio dell'aggiornamento.

-   Se l'aggiornamento risulta come **Download** e non cambia, esaminare eventuali errori in **hman. log** e in **dmpdownloader. log**.

    -   Se il file dmpdownloader.log indica che il processo dmpdownloader è in stato di sospensione ed è in attesa di un intervallo prima di verificare la disponibilità di aggiornamenti, è possibile riavviare il servizio **SMS_Executive** sul server del sito per riavviare il download dei file di ridistribuzione dell'aggiornamento.

    -   Un altro problema di download comune si verifica quando le impostazioni del server proxy impediscono il download da `silverlight.dlservice.microsoft.com` e da `download.microsoft.com`.

Per altre informazioni sull'installazione degli aggiornamenti, vedere [Aggiornamenti e manutenzione nella console](updates.md#bkmk_inconsole).

Per informazioni sulle versioni di Current Branch, vedere [Versioni di base e di aggiornamento](updates.md#bkmk_Baselines) in [Aggiornamenti per Configuration Manager](updates.md).

## <a name="about-installing-update-1802"></a>Informazioni sull'installazione dell'aggiornamento 1802

**Siti:**  
L'aggiornamento 1802 viene installato nel sito principale della gerarchia. Ciò significa che l'installazione deve essere avviata dal sito di amministrazione centrale, se disponibile, o dal sito primario autonomo. Dopo l'installazione dell'aggiornamento nel sito di livello più alto, l'aggiornamento nei siti figlio viene eseguito nel modo seguente:

-   I siti primari figlio installano automaticamente l'aggiornamento al termine dell'installazione dell'aggiornamento nel sito di amministrazione centrale. È possibile usare gli intervalli di servizio per controllare quando eseguire l'installazione dell'aggiornamento in un sito. Per altre informazioni, vedere [Intervalli di servizio per i server del sito](service-windows.md).

-   Dopo che il sito primario padre ha completato l'installazione dell'aggiornamento, è necessario aggiornare manualmente ogni sito secondario dalla console di Configuration Manager. L'aggiornamento automatico dei server del sito secondario non è supportato.

**Ruoli del sistema del sito:**  
Quando un server del sito installa l'aggiornamento, i ruoli del sistema del sito installati nel computer server e quelli installati nei computer remoti vengono aggiornati automaticamente. Pertanto, prima di installare l'aggiornamento, verificare che ogni server del sistema del sito soddisfi i prerequisiti per il funzionamento con la nuova versione di aggiornamento.

**Console di Configuration Manager:**    
La prima volta che si usa una console di Configuration Manager dopo l'aggiornamento, viene richiesto di aggiornare tale console. A tale scopo, è necessario eseguire l'installazione di Configuration Manager nel computer che ospita la console e quindi selezionare l'opzione per aggiornare la console. Si consiglia di installare al più presto l'aggiornamento della console.

> [!IMPORTANT]  
> Quando si installa un aggiornamento nel sito di amministrazione centrale, considerare le limitazioni e i ritardi seguenti che si verificano finché tutti i siti primari figlio non hanno completato l'installazione dell'aggiornamento:    
> - Gli **aggiornamenti client** non vengono avviati. Sono inclusi gli aggiornamenti automatici dei client e quelli dei client pre-produzione. Inoltre, non è possibile promuovere i client di pre-produzione nell'ambiente di produzione finché l'ultimo sito non ha completato l'installazione dell'aggiornamento. Al termine dell'installazione dell'aggiornamento nell'ultimo sito, gli aggiornamenti client vengono avviati in base alle scelte di configurazione.   
> - Le **nuove funzionalità** abilitate con l'aggiornamento non sono disponibili. Ciò consente di evitare che la replica dei dati relativi a una funzionalità venga inviata a un sito in cui non è ancora installato il supporto per tale funzionalità. Una volta installato l'aggiornamento in tutti i siti primari, la funzionalità specificata sarà disponibile per l'uso.   
> - I **collegamenti di replica** tra il sito di amministrazione centrale e i siti primari figlio non risultano aggiornati. Questa condizione è segnalata dallo stato di installazione del pacchetto di aggiornamento impostato come Completato con avviso per Monitoraggio dell'inizializzazione della replica. Nel nodo Monitoraggio della console, questa condizione viene visualizzata come *Configurazione collegamento in corso*.


## <a name="checklist"></a>Elenco di controllo

**Verificare che tutti i siti eseguano una versione di Configuration Manager che supporta l'aggiornamento alla versione 1802:**    
prima di iniziare l'installazione dell'aggiornamento 1802, è necessario che ogni server del sito nella gerarchia esegua la stessa versione di Configuration Manager. Per eseguire l'aggiornamento alla versione 1802, è necessario usare la versione 1702, 1706 o 1710.

**Controllare lo stato di Software Assurance o dei diritti di sottoscrizione equivalenti:**    
Per installare l'aggiornamento 1802, è necessario avere un contratto Software Assurance attivo. Quando si installa questo aggiornamento, nella scheda **Licenze** è disponibile l'opzione per la conferma della **data di scadenza di Software Assurance**.

Questo è un valore facoltativo che è possibile specificare come utile promemoria della data di scadenza della licenza. Questa data è visibile quando si installano gli aggiornamenti futuri. È possibile che questo valore sia stato specificato in precedenza durante la configurazione o l'installazione di un aggiornamento oppure nella scheda **Licenze** di **Impostazioni gerarchia** nella console di Configuration Manager.

Per altre informazioni, vedere [Licenze e rami per Configuration Manager](../../understand/learn-more-editions.md).

**Controllare le versioni di Microsoft .NET installate nei server del sistema del sito:** quando questo aggiornamento viene installato in un sito, Configuration Manager esegue in automatico l'installazione di .NET Framework 4.5.2 in ogni computer che ospita uno dei seguenti ruoli del sistema del sito, se non è già installato .NET Framework 4.5 o versione successiva:

-   Punto proxy di registrazione
-   Punto di registrazione
-   Punto di gestione
-   Punto di connessione del servizio

Questa installazione consente di impostare il server del sistema del sito in uno stato di riavvio in sospeso e segnala gli errori al visualizzatore di stato dei componenti di Configuration Manager. Inoltre, le applicazioni .NET sul server possono presentare errori casuali fino a quando il server non viene riavviato.

Per altre informazioni, vedere [Prerequisiti del sito e del sistema del sito](../../plan-design/configs/site-and-site-system-prerequisites.md).

**Controllare la versione di Windows Assessment and Deployment Kit (ADK) per Windows 10**: la versione di Windows 10 ADK deve essere 1703 o successiva. (Per ulteriori informazioni sulle versioni supportate di Windows ADK, vedere [Windows 10 ADK](../../plan-design/configs/support-for-windows-10.md#windows-10-adk)) Se è necessario aggiornare l'ADK Windows, eseguire questa operazione prima di iniziare l'aggiornamento di Configuration Manager. In questo modo, le immagini di avvio predefinite vengono aggiornate automaticamente alla versione più recente di Windows PE. Le immagini di avvio personalizzate devono essere aggiornate manualmente.

Se si aggiorna il sito prima di aggiornare Windows ADK, vedere [Aggiornare i punti di distribuzione con l'immagine di avvio](../../../osd/get-started/manage-boot-images.md#update-distribution-points-with-the-boot-image).

**Esaminare lo stato del sito e della gerarchia e verificare che non siano presenti problemi non risolti:** Prima di aggiornare un sito, risolvere tutti i problemi operativi per il server del sito, il server del database del sito e i ruoli del sistema del sito installati nei computer remoti. Un aggiornamento del sito può avere esito negativo a causa di problemi operativi esistenti.

Per altre informazioni, vedere [Usare gli avvisi e il sistema di stato per Configuration Manager](use-alerts-and-the-status-system.md).

**Esaminare la replica di file e dati tra siti:**    
verificare che la replica di file e database tra siti sia funzionante e aggiornata. Eventuali ritardi o backlog in uno dei due ambiti possono complicare o compromettere l'aggiornamento.
Per la replica di database è possibile usare Replication Link Analyzer per risolvere i problemi prima di avviare l'aggiornamento.

Per altre informazioni, vedere [Informazioni su Replication Link Analyzer](monitor-replication.md#BKMK_RLA).

**Installare tutti gli aggiornamenti critici disponibili per i sistemi operativi dei computer che ospitano il sito, il server di database del sito e i ruoli del sistema del sito remoto:** prima di installare un aggiornamento per Configuration Manager, installare gli aggiornamenti critici del sistema operativo per ogni sistema del sito applicabile. Se un aggiornamento installato richiede un riavvio, riavviare i computer interessati prima di iniziare l'aggiornamento.

**Disabilitare le repliche di database per i punti di gestione nei siti primari:**    
Configuration Manager non può aggiornare un sito primario per il quale esista una replica del database per i punti di gestione abilitati. Prima di installare un aggiornamento per Configuration Manager, disabilitare la replica di database.

Per altre informazioni, vedere [Repliche di database per i punti di gestione per Configuration Manager](../deploy/configure/database-replicas-for-management-points.md).

**Impostare i gruppi di disponibilità SQL Server AlwaysOn per eseguire il failover manuale:**    
Se si usa un gruppo di disponibilità, prima di iniziare l'installazione dell'aggiornamento verificare che il gruppo di disponibilità sia impostato sul failover manuale. Dopo l'aggiornamento del sito, è possibile ripristinare la modalità di failover automatico. Per altre informazioni, vedere [Server AlwaysOn per database del sito](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

**Riconfigurare i punti di aggiornamento software che usano Bilanciamento carico di rete:**    
<!-- Support for NLBs is fully removed with 1702. When 1702 is no longer in support, this statement can drop -->
Configuration Manager non può aggiornare un sito che usa un cluster Bilanciamento carico di rete (NLB) per ospitare i punti di aggiornamento software.

Se si usano cluster NLB per i punti di aggiornamento software, usare Windows PowerShell per rimuovere il cluster NLB.
Per altre informazioni, vedere [Pianificare gli aggiornamenti software](../../../sum/plan-design/plan-for-software-updates.md).

**Disabilitare tutte le attività di manutenzione del sito in ogni sito per la durata dell'aggiornamento del sito in questione:**    
Prima di installare l'aggiornamento , disabilitare le eventuali attività di manutenzione che potrebbero essere eseguite mentre è in corso il processo di aggiornamento. Queste comprendono, ma non sono limitate alle seguenti attività:

-   Backup server sito
-   Elimina operazioni client obsolete
-   Elimina dati di individuazione obsoleti

Quando un'attività di manutenzione del database del sito viene eseguita durante l'installazione dell'aggiornamento, quest'ultima potrebbe avere esito negativo. Prima di disabilitare un'attività, registrarne la pianificazione per poter ripristinare la sua configurazione dopo l'installazione dell'aggiornamento.

Per altre informazioni, vedere [Attività di manutenzione per Configuration Manager](maintenance-tasks.md) e [Informazioni di riferimento per le attività di manutenzione per Configuration Manager](reference-for-maintenance-tasks.md).

**Arrestare temporaneamente il software antivirus nei server di Configuration Manager:** prima di aggiornare un sito, assicurarsi di aver arrestato il software antivirus sui server Configuration Manager. <!--SMS.503481--> 

**Creare un backup del database del sito nel sito di amministrazione centrale e nei siti primari:** prima di aggiornare un sito, eseguire il backup del database del sito per assicurarsi di disporre di un backup effettuato correttamente da usare in caso di ripristino di emergenza.

Per altre informazioni, vedere [Eseguire il backup e il ripristino per Configuration Manager](backup-and-recovery.md).

**Pianificare la distribuzione pilota del client:**    
Quando si installa un aggiornamento per il client, è possibile testare quest'ultimo in un ambiente di pre-produzione prima della distribuzione e dell'aggiornamento di tutti i client attivi.

Per sfruttare i vantaggi di questa opzione, è necessario configurare il sito in modo da supportare gli aggiornamenti automatici di pre-produzione prima di iniziare l'installazione dell'aggiornamento.

Per altre informazioni, vedere [Aggiornare i client](../../clients/manage/upgrade/upgrade-clients.md) e [Come testare gli aggiornamenti client in una raccolta di pre-produzione](../../clients/manage/upgrade/test-client-upgrades.md).

**Pianificare l'uso di intervalli di servizio per controllare quando vengono installati gli aggiornamenti ai server del sito:**    
Usare gli intervalli di servizio per definire un periodo durante il quale possono essere installati gli aggiornamenti a un server del sito.

Questo permette di controllare quando i siti nella gerarchia installano l'aggiornamento. Per altre informazioni, vedere [Intervalli di servizio per i server del sito](service-windows.md).

**Verificare le estensioni supportate** :  
<!--SCCMdocs#587-->   
Se si estende Configuration Manager usando altri prodotti Microsoft o di suoi partner, assicurarsi la versione 1802 sia supportata da tali prodotti. Rivolgersi al fornitore del prodotto per verificare questa informazione. Ad esempio, vedere le [note sulla versione](../../../mdt/release-notes.md) di Microsoft Deployment Toolkit.

**Eseguire il controllo dei prerequisiti di installazione:**    
Quando l'aggiornamento risulta**Disponibile** nella console, è possibile eseguire il controllo dei prerequisiti in modo indipendente prima di procedere all'installazione. Quando si installa l'aggiornamento nel sito, il controllo dei prerequisiti viene eseguito nuovamente.

Per eseguire il controllo dei prerequisiti dalla console, passare all'area di lavoro **Amministrazione** e selezionare **Aggiornamenti e manutenzione**. Selezionare il pacchetto di aggiornamento **Configuration Manager 1802**, quindi fare clic su **Esegui controllo prerequisiti**.

Per altre informazioni sull'avvio e sul monitoraggio del controllo dei prerequisiti, vedere **Passaggio 3: Eseguire il controllo dei prerequisiti prima di installare un aggiornamento** nell'argomento [Installare gli aggiornamenti nella console per Configuration Manager](install-in-console-updates.md).

> [!IMPORTANT]  
> Quando viene eseguito il controllo dei prerequisiti in modo indipendente o nel contesto dell'installazione di un aggiornamento, il processo aggiorna alcuni file di origine del prodotto usati per le attività di manutenzione del sito. Di conseguenza, dopo aver eseguito il controllo dei prerequisiti, ma prima di installare l'aggiornamento, se si deve svolgere un'attività di manutenzione del sito, eseguire **Setupwfe.exe** (il programma di installazione di Configuration Manager) dalla cartella CD.Latest nel server del sito.

**Aggiornare i siti:**    
A questo punto è possibile avviare l'installazione dell'aggiornamento per la gerarchia. Per altre informazioni sull'installazione dell'aggiornamento, vedere [Installare gli aggiornamenti nella console](install-in-console-updates.md#bkmk_install).

È consigliabile pianificare l'installazione dell'aggiornamento per ogni sito al di fuori del normale orario di ufficio in modo che il processo di installazione dell'aggiornamento e le azioni per reinstallare i componenti del sito e i ruoli del sistema del sito abbiano un impatto minimo sulle operazioni aziendali.

Per altre informazioni, vedere [Aggiornamenti per Configuration Manager](updates.md).

## <a name="post-update-checklist"></a>Elenco di controllo post-aggiornamento
Esaminare le azioni seguenti da eseguire al termine dell'installazione dell'aggiornamento.
1. Verificare che la replica da sito a sito sia attiva. Nella console visualizzare **Monitoraggio** > **Gerarchia del sito** e **Monitoraggio** > **Replica di database** per ottenere indicazioni sui problemi o ricevere conferma che i collegamenti di replica sono attivi.
2. Assicurarsi che ogni server del sito e ogni ruolo del sistema del sito siano aggiornati alla versione 1802. Nella console è possibile aggiungere la colonna **Versione** facoltativa alla visualizzazione di alcuni nodi tra cui **Siti** e **Punti di distribuzione**.

   Se necessario, un ruolo del sistema del sito verrà reinstallato automaticamente per l'aggiornamento alla nuova versione. Provare a riavviare i sistemi del sito remoti che non vengono aggiornati.
3. Riconfigurare le repliche di database per i punti di gestione nei siti primari che sono stati disabilitati prima di avviare l'aggiornamento.
4. Riconfigurare le attività di manutenzione di database che sono state disabilitate prima di avviare l'aggiornamento.
5. Se si è configurata la distribuzione client pilota prima di installare l'aggiornamento, aggiornare i client in base al piano che è stato creato.
6. Se si usano estensioni di Configuration Manager, eseguire l'aggiornamento alla versione più recente per supportare l'aggiornamento di Configuration Manager. 
