---
title: Elenco di controllo per la versione 1610
titleSuffix: Configuration Manager
description: Informazioni sulle azioni da intraprendere prima di eseguire l'aggiornamento di Configuration Manager alla versione 1610.
ms.date: 06/6/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7b411cb0-4fd1-41f2-a2f6-33738a5bde96
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 25d0302c4c35f2c66ce06febde63809b4a11116c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688779"
---
# <a name="checklist-for-installing-update-1610-for-configuration-manager"></a>Elenco di controllo per l'installazione dell'aggiornamento 1610 di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Quando si usa la versione Current Branch di Configuration Manager, è possibile installare l'aggiornamento nella console per la versione 1610 per aggiornare la gerarchia dalla versione 1606. Se la gerarchia esegue la versione 1511, 1602 o 1606, è possibile eseguire l'aggiornamento alla versione 1610.

Per ottenere l'aggiornamento per la versione 1610, è necessario usare un ruolo del sistema del sito punto di connessione del servizio nel sito principale della gerarchia. Questo può essere in modalità online o offline. Dopo che la gerarchia ha scaricato il pacchetto di aggiornamento da Microsoft, questo è disponibile nella console, in **Amministrazione &gt; Panoramica &gt; Servizi cloud &gt; Aggiornamenti e manutenzione**.

-   Quando l'aggiornamento risulta **Disponibile**, è pronto per l'installazione. Prima di installare la versione 1610, leggere le informazioni seguenti [sull'installazione dell'aggiornamento 1610](#about-installing-update-1610) e l'[elenco di controllo](#checklist) delle configurazioni da eseguire prima dell'avvio dell'aggiornamento.

-   Se l'aggiornamento risulta come **Download** e non cambia, esaminare eventuali errori in **hman. log** e in **dmpdownloader. log**.

    -   In genere, è anche possibile riavviare il servizio **SMS_Executive** nel server del sito per riavviare il download dei file di ridistribuzione dell'aggiornamento.

    -   Un altro problema di download comune si verifica quando le impostazioni del server proxy impediscono il download da `silverlight.dlservice.microsoft.com` e da `download.microsoft.com`.

Per altre informazioni sull'installazione degli aggiornamenti, vedere [Aggiornamenti e manutenzione nella console](updates.md#bkmk_inconsole).

Per informazioni sulle versioni di Current Branch, vedere [Versioni di base e di aggiornamento](updates.md#bkmk_Baselines) in [Aggiornamenti per Configuration Manager](updates.md).

## <a name="about-installing-update-1610"></a>Informazioni sull'installazione dell'aggiornamento 1610

**Siti:**  
L'aggiornamento 1610 può essere installato solo nel sito principale della gerarchia. Ciò significa che l'installazione deve essere avviata dal sito di amministrazione centrale, se disponibile, o dal sito primario autonomo. Dopo l'installazione dell'aggiornamento nel sito di livello più alto, il comportamento dell'aggiornamento dei siti figlio è il seguente:

-   I siti primari figlio installano automaticamente l'aggiornamento al termine dell'installazione dell'aggiornamento del sito di amministrazione centrale. È possibile usare gli intervalli di servizio per controllare quando eseguire l'installazione di aggiornamenti in un sito. Prima della versione 1606 gli intervalli di servizio si chiamavano finestre di manutenzione. Per altre informazioni, vedere [Intervalli di servizio per i server del sito](service-windows.md).

-   Dopo che il sito primario padre ha completato l'installazione dell'aggiornamento, è necessario aggiornare manualmente i siti secondari dalla console di Configuration Manager. L'aggiornamento automatico dei server del sito secondario non è supportato.

**Ruoli del sistema del sito:**  
Quando il server del sito installa l'aggiornamento, i ruoli del sistema del sito installati nel server e quelli installati nei computer remoti vengono aggiornati automaticamente. Pertanto, prima di installare l'aggiornamento, verificare che ogni server del sistema del sito soddisfi i nuovi prerequisiti per il funzionamento con la nuova versione di aggiornamento.

**Console di Configuration Manager:**    
La prima volta che si usa una console di Configuration Manager dopo l'aggiornamento, viene richiesto di aggiornare tale console. A tale scopo, è necessario eseguire l'installazione di Configuration Manager nel computer che ospita la console e quindi selezionare l'opzione per aggiornare la console. Si consiglia di installare al più presto l'aggiornamento della console.



## <a name="checklist"></a>Elenco di controllo

**Verificare che tutti i siti eseguano una versione supportata di Configuration Manager:** prima di iniziare l'installazione dell'aggiornamento 1610, è necessario che ogni sito nella gerarchia esegua la stessa versione di Configuration Manager, ovvero la versione 1511, 1602 o 1606.

**Controllare lo stato di Software Assurance o dei diritti di sottoscrizione equivalenti:**    
Per installare l'aggiornamento 1610, è necessario disporre di un contratto Software Assurance attivo. Quando si installa la versione 1610, nella scheda **Licenza** è disponibile l'opzione per la conferma della **data di scadenza di Software Assurance**.

Si tratta di un valore facoltativo, che è possibile specificare come utile promemoria della data di scadenza della licenza e che verrà visualizzato quando si installeranno aggiornamenti in futuro. Se per l'installazione di Configuration Manager si è usato il supporto di base della versione 1606, è possibile che questo valore sia stato specificato in precedenza durante l'installazione oppure nella scheda **Licenza** di **Impostazioni gerarchia** dopo l'installazione del sito.

Per altre informazioni, vedere [Licenze e rami per Configuration Manager](../../understand/learn-more-editions.md).

**Controllare le versioni di Microsoft .NET installate nei server del sistema del sito:** quando l'aggiornamento 1610 viene installato in un sito, Configuration Manager esegue in automatico l'installazione di .NET Framework 4.5.2 in ogni computer che ospita uno dei ruoli del sistema del sito seguenti se .NET Framework 4.5 o versione successiva non è già installato:

-   Punto proxy di registrazione
-   Punto di registrazione
-   Punto di gestione
-   Punto di connessione del servizio

Questa installazione consente di impostare il server del sistema del sito in uno stato di riavvio in sospeso e segnala gli errori al visualizzatore di stato dei componenti di Configuration Manager. Inoltre, le applicazioni .NET sul server possono presentare errori casuali fino a quando il server non viene riavviato.

Per altre informazioni, vedere [Prerequisiti del sito e del sistema del sito](../../plan-design/configs/site-and-site-system-prerequisites.md).

**Esaminare lo stato del sito e della gerarchia e verificare che non siano presenti problemi non risolti:** Prima di aggiornare un sito, risolvere tutti i problemi operativi per il server del sito, il server del database del sito e i ruoli del sistema del sito installati nei computer remoti. Un aggiornamento del sito può avere esito negativo a causa di problemi operativi esistenti.

Per altre informazioni, vedere [Usare gli avvisi e il sistema di stato per Configuration Manager](use-alerts-and-the-status-system.md).

**Esaminare la replica di file e dati tra siti:** verificare che la replica di file e database tra siti sia funzionante e aggiornata. Eventuali ritardi o backlog in uno dei due ambiti possono complicare o compromettere l'aggiornamento.
Per la replica di database è possibile usare Replication Link Analyzer per risolvere i problemi prima di avviare l'aggiornamento.

Per altre informazioni, vedere [Replication Link Analyzer](monitor-replication.md#BKMK_RLA)nell'argomento [Monitorare la replica di database](monitor-replication.md).

**Installare tutti gli aggiornamenti critici disponibili per i sistemi operativi dei computer che ospitano il sito, il server di database del sito e i ruoli del sistema del sito remoto:** prima di installare un aggiornamento per Configuration Manager, installare gli aggiornamenti critici del sistema operativo per ogni sistema del sito applicabile. Se un aggiornamento installato richiede un riavvio, riavviare i computer interessati prima di iniziare l'aggiornamento di Configuration Manager.

**Disabilitare le repliche di database per i punti di gestione nei siti primari:**    
Configuration Manager non può aggiornare un sito primario per il quale esista una replica del database per i punti di gestione abilitati. Prima di installare un aggiornamento per Configuration Manager, disabilitare la replica di database.

Per altre informazioni, vedere [Repliche di database per i punti di gestione per Configuration Manager](../deploy/configure/database-replicas-for-management-points.md).

**Impostare i gruppi di disponibilità SQL Server AlwaysOn per eseguire il failover manuale:**    
Prima di installare gli aggiornamenti, ad esempio la versione 1610, verificare che il gruppo di disponibilità sia impostato sul failover manuale. Dopo l'aggiornamento del sito, è possibile ripristinare la modalità di failover automatico. Per altre informazioni, vedere [Server AlwaysOn per database del sito](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

**Riconfigurare i punti di aggiornamento software che usano Bilanciamento carico di rete:**    
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

<!-- Removed from update guidance 6/6/2017
**Test the database upgrade on a copy of the most recent site database backup:** 
Before you update a Configuration Manager central administration site or primary site, test the site database upgrade process on a copy of the site database.

-   We recommend that you test the site database upgrade process because when you upgrade a site, the site database might be modified.

-   Although a test database upgrade is not required, it can identify problems for the upgrade before your production database is affected.

-   A failed site database upgrade can render your site database inoperable and might require a site recovery to restore functionality.

-   Although the site database is shared between sites in a hierarchy, plan to test the database at each applicable site before you upgrade that site.

-   If you use database replicas for management points at a primary site, disable replication before you create the backup of the site database.

Configuration Manager does not support the backup of secondary sites nor does it support the test upgrade of a secondary site database.

Do not run a test database upgrade on the production site database. Doing so updates the site database and could render your site inoperable. For more information, see [Step 2: Test the database upgrade before installing an update](install-in-console-updates.md#bkmk_step2) from **Before you install an in-console update**.
-->

**Pianificare la distribuzione pilota del client:**    
Quando si installa un aggiornamento per il client, è possibile testare quest'ultimo in un ambiente di pre-produzione prima della distribuzione e dell'aggiornamento di tutti i client attivi.

Per sfruttare i vantaggi di questa opzione, è necessario configurare il sito in modo da supportare gli aggiornamenti automatici di pre-produzione prima di iniziare l'installazione dell'aggiornamento.

Per altre informazioni, vedere [Aggiornare i client](../../clients/manage/upgrade/upgrade-clients.md) e [Come testare gli aggiornamenti client in una raccolta di pre-produzione](../../clients/manage/upgrade/test-client-upgrades.md).

**Pianificare l'uso di intervalli di servizio per controllare quando vengono installati gli aggiornamenti ai server del sito:**    
È possibile usare gli intervalli di servizio per definire un periodo durante il quale possono essere installati gli aggiornamenti a un server del sito.

Questo permette di controllare quando i siti nella gerarchia installano l'aggiornamento. Prima della versione 1606 gli intervalli di servizio si chiamavano finestre di manutenzione. Per altre informazioni, vedere [Intervalli di servizio per i server del sito](service-windows.md).

**Eseguire il controllo dei prerequisiti di installazione:**    
Quando l'aggiornamento risulta**Disponibile** nella console, è possibile eseguire il controllo dei prerequisiti in modo indipendente prima di procedere all'installazione. Quando si installa l'aggiornamento nel sito, il controllo dei prerequisiti viene eseguito nuovamente.

Per eseguire il controllo dei prerequisiti dalla console, passare ad **Amministrazione > Panoramica > Servizi cloud > Aggiornamenti e manutenzione.** Fare quindi clic con il pulsante destro del mouse sul **pacchetto di aggiornamento di Configuration Manager 1610** e scegliere **Esegui controllo prerequisiti**.

Per altre informazioni sull'avvio e sul monitoraggio del controllo dei prerequisiti, vedere **Passaggio 3: Eseguire il controllo dei prerequisiti prima di installare un aggiornamento** nell'argomento [Installare gli aggiornamenti nella console per Configuration Manager](install-in-console-updates.md).

> [!IMPORTANT]  
> Quando viene eseguito il controllo dei prerequisiti in modo indipendente o nel contesto dell'installazione di un aggiornamento, il processo aggiorna alcuni file di origine del prodotto usati per le attività di manutenzione del sito. Di conseguenza, dopo aver eseguito il controllo dei prerequisiti ma prima di installare l'aggiornamento 1610, se si deve svolgere un'attività di manutenzione del sito, eseguire **Setupwfe.exe** (il programma di installazione di Configuration Manager) dalla cartella CD.Latest nel server del sito.

**Aggiornare i siti:** A questo punto è possibile avviare l'installazione dell'aggiornamento per la gerarchia. Per altre informazioni sull'installazione dell'aggiornamento, vedere [Installare gli aggiornamenti nella console.](install-in-console-updates.md#bkmk_install)

È consigliabile pianificare l'installazione dell'aggiornamento per ogni sito al di fuori del normale orario di ufficio in modo che il processo di installazione dell'aggiornamento e le azioni per reinstallare i componenti del sito e i ruoli del sistema del sito abbiano un impatto minimo sulle operazioni aziendali.

Per altre informazioni, vedere  [Aggiornamenti per Configuration Manager](updates.md).
