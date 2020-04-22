---
title: Elenco di controllo per la versione 1602
titleSuffix: Configuration Manager
description: Informazioni sulle azioni da intraprendere prima di eseguire l'aggiornamento di Configuration Manager dalla versione 1511 alla versione 1602.
ms.date: 02/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b63ef197-01f0-4894-b929-5ef8403c5195
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: b330c4049dce06b1e47d1088993b09ec16e724a8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700259"
---
# <a name="checklist-for-installing-update-1602-for-configuration-manager"></a>Elenco di controllo per l'installazione dell'aggiornamento 1602 di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Prima di aggiornare Configuration Manager dalla versione 1511 alla 1602, esaminare le informazioni e l'elenco di controllo seguenti per le azioni da eseguire prima di iniziare l'aggiornamento.  

 **Informazioni sull'installazione dell'aggiornamento 1602:**  

 L'aggiornamento 1602 può essere installato solo nel sito principale della gerarchia. Ciò significa che l'installazione deve essere avviata dal sito di amministrazione centrale, se disponibile, o dal sito primario autonomo.  

-   I siti primari figlio installano automaticamente l'aggiornamento al termine dell'installazione dell'aggiornamento del sito di amministrazione centrale. È possibile usare le finestre di manutenzione per controllare quando vengono installati gli aggiornamenti in un sito. A partire dal rilascio dell'aggiornamento 1602, le finestre di manutenzione sono chiamate *intervalli di servizio*. Per altre informazioni, vedere [Intervalli di servizio per i server del sito](service-windows.md).  

-   Dopo che il sito primario padre ha completato l'installazione dell'aggiornamento, è necessario aggiornare manualmente i siti secondari dalla console di Configuration Manager. L'aggiornamento automatico dei server del sito secondario non è supportato.  

Quando il server del sito installa l'aggiornamento, i ruoli del sistema del sito installati nel server e quelli installati nei computer remoti vengono aggiornati automaticamente. Pertanto, prima di installare l'aggiornamento, verificare che ogni server del sistema del sito soddisfi i nuovi prerequisiti per il funzionamento con la nuova versione di aggiornamento.  

La prima volta che si usa una console di Configuration Manager dopo l'aggiornamento, viene richiesto di aggiornare tale console. A tale scopo, è necessario eseguire l'installazione di Configuration Manager nel computer che ospita la console e scegliere l'opzione per aggiornare la console. Si consiglia di installare al più presto l'aggiornamento della console.  

 **Elenco di controllo:**  

 **Verificare che tutti i siti eseguano una versione supportata di Configuration Manager:**  prima di iniziare l'installazione dell'aggiornamento 1602, è necessario che ogni server del sito nella gerarchia esegua Configuration Manager versione 1511.  

 **Controllare le versioni di Microsoft .NET installate nei server del sistema del sito:** quando l'aggiornamento 1602 viene installato in un sito, Configuration Manager esegue in automatico l'installazione di .NET Framework 4.5.2 in ogni computer che ospita uno dei ruoli del sistema del sito seguenti (se .NET Framework 4.5 o versione successiva non è già installato):  

-   Punto proxy di registrazione  

-   Punto di registrazione  

-   Punto di gestione  

-   punto di connessione del servizio  

Questa installazione consente di impostare il server del sistema del sito in uno stato di riavvio in sospeso e segnala gli errori al visualizzatore di stato dei componenti di Configuration Manager. Inoltre, le applicazioni .NET sul server possono presentare errori casuali finché il server non viene riavviato.  

 Per altre informazioni, vedere [Prerequisiti del sito e del sistema del sito](../../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

 **Esaminare lo stato del sito e della gerarchia e verificare che non siano presenti problemi non risolti:** Prima di aggiornare un sito, risolvere tutti i problemi operativi per il server del sito, il server del database del sito e i ruoli del sistema del sito installati nei computer remoti. Un aggiornamento del sito può avere esito negativo a causa di problemi operativi esistenti.  

Per altre informazioni, vedere [Usare gli avvisi e il sistema di stato per Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

 **Esaminare la replica di file e dati tra siti:**  verificare che la replica di file e database tra siti sia funzionante e aggiornata. Eventuali ritardi o backlog in uno dei due ambiti possono complicare o compromettere l'aggiornamento.    

Per la replica di database è possibile usare Replication Link Analyzer per risolvere i problemi prima di avviare l'aggiornamento.    

 Per altre informazioni, vedere [Informazioni su Replication Link Analyzer](monitor-replication.md#BKMK_RLA).  

 **Installare tutti gli aggiornamenti critici disponibili per i sistemi operativi dei computer che ospitano il sito, il server di database del sito e i ruoli del sistema del sito remoto:** prima di installare un aggiornamento per Configuration Manager, installare gli aggiornamenti critici del sistema operativo per ogni sistema del sito applicabile. Se un aggiornamento installato richiede un riavvio, riavviare i computer interessati prima di iniziare l'aggiornamento.  

 **Disabilitare le repliche di database per i punti di gestione nei siti primari:** Configuration Manager non può aggiornare un sito primario per il quale esista una replica del database per i punti di gestione abilitati. Disabilitare la replica di database prima di:  

-   Creare un backup del database del sito per testare l'aggiornamento del database.  

-   Installare un aggiornamento per Configuration Manager.  

Per altre informazioni, vedere [Repliche di database per i punti di gestione per Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

 **Riconfigurare i punti di aggiornamento software che usano NLB:** Configuration Manager non può aggiornare un sito che usa un cluster Bilanciamento carico di rete per ospitare i punti di aggiornamento software.  Se si usano cluster NLB per i punti di aggiornamento software, usare Windows PowerShell per rimuovere il cluster NLB.    

 Per altre informazioni, vedere [Pianificare gli aggiornamenti software](../../../sum/plan-design/plan-for-software-updates.md).  

 **Disabilitare tutte le attività di manutenzione del sito in ogni sito per la durata dell'aggiornamento del sito in questione:** prima di installare gli aggiornamenti, disabilitare le eventuali attività di manutenzione che potrebbero essere eseguite mentre è in corso il processo di aggiornamento. Queste attività includono, tra le altre, le operazioni seguenti:  

-   Backup server sito  

-   Elimina operazioni client obsolete  

-   Elimina dati di individuazione obsoleti  

Quando un'attività di manutenzione del database del sito viene eseguita durante l'installazione dell'aggiornamento, quest'ultima potrebbe avere esito negativo. Prima di disabilitare un'attività, registrarne la pianificazione per poter ripristinare la sua configurazione dopo l'installazione dell'aggiornamento.  

 Per altre informazioni, vedere [Attività di manutenzione per Configuration Manager](../../../core/servers/manage/maintenance-tasks.md) e [Informazioni di riferimento per le attività di manutenzione per Configuration Manager](../../../core/servers/manage/reference-for-maintenance-tasks.md). 

**Arrestare temporaneamente il software antivirus nei server di Configuration Manager:** prima di aggiornare un sito, assicurarsi di aver arrestato il software antivirus sui server Configuration Manager. <!--SMS.503481--> 

 **Creare un backup del database del sito nel sito di amministrazione centrale e nei siti primari:** prima di aggiornare un sito, eseguire il backup del database del sito per assicurarsi di avere un backup corretto da usare in caso di ripristino di emergenza.   

Per altre informazioni, vedere [Eseguire il backup e il ripristino per Configuration Manager](backup-and-recovery.md).  

 **Eseguire il backup di un file Configuration.mof personalizzato:** se si usa un file Configuration.mof personalizzato per definire le classi di dati usate con l'inventario hardware, creare un backup del file prima di aggiornare il sito. Dopo l'aggiornamento, ripristinare il file nel sito con la versione 1602. Quando si aggiorna un sito, il file corrente viene sovrascritto con la versione originale (predefinita) del file. Per altre informazioni sull'uso di questo file, vedere [Come estendere l'inventario hardware](../../../core/clients/manage/inventory/extend-hardware-inventory.md).  

 **Testare l'aggiornamento del database in una copia del backup più recente del database del sito:** Prima di eseguire l'aggiornamento di un sito primario o di amministrazione centrale di Configuration Manager, testare il processo di aggiornamento del database del sito in una copia del database del sito.  

-   È opportuno testare il processo di aggiornamento del database del sito perché, quando si aggiorna un sito, è possibile che il database del sito venga modificato.  

-   Anche se non è obbligatorio, un aggiornamento di test del database permette di identificare i problemi relativi all'aggiornamento prima che questi influiscano sul database di produzione.  

-   Un aggiornamento non riuscito del database del sito può rendere inutilizzabile il database del sito e potrebbe richiedere un ripristino del sito per il relativo ripristino delle funzionalità.  

-   Nonostante il database del sito sia condiviso tra i siti nella gerarchia, pianificare un test del database in ciascun sito applicabile prima di aggiornare tale sito.  

-   Se si usano le repliche di database per i punti di gestione in un sito primario, disabilitare la replica prima di creare il backup del database del sito.  

Configuration Manager non supporta né il backup di siti secondari né l'aggiornamento di test del database di un sito secondario.   
Non eseguire un aggiornamento di test sul database del sito di produzione. Questa operazione aggiorna il database del sito e potrebbe rendere inutilizzabile il sito. Per altre informazioni, vedere [Passaggio 2: Testare l'aggiornamento del database prima di installare un aggiornamento](install-in-console-updates.md#bkmk_step2) in **Prima di installare un aggiornamento nella console**.  

 **Pianificare la distribuzione pilota del client:** Quando si installa un aggiornamento per il client, è possibile testare quest'ultimo in un ambiente di pre-produzione prima della distribuzione e dell'aggiornamento di tutti i client attivi.   

 Per sfruttare i vantaggi di questa opzione, è necessario configurare il sito in modo da supportare gli aggiornamenti automatici di pre-produzione prima di iniziare l'installazione dell'aggiornamento. Per altre informazioni, vedere [Aggiornare i client](../../../core/clients/manage/upgrade/upgrade-clients.md) e   
[Come testare gli aggiornamenti client in una raccolta di pre-produzione](../../../core/clients/manage/upgrade/test-client-upgrades.md).  

 **Pianificare l'uso di finestre di manutenzione per controllare quando i server del sito installano gli aggiornamenti:** è possibile usare le finestre di manutenzione per definire un periodo durante il quale gli aggiornamenti al server del sito possono essere installati. Questo permette di controllare quando i siti nella gerarchia installano l'aggiornamento.   

A partire dal rilascio dell'aggiornamento 1602, le finestre di manutenzione sono chiamate *intervalli di servizio*. Per altre informazioni, vedere [Intervalli di servizio per i server del sito](service-windows.md).  

 **Eseguire il controllo dei prerequisiti di installazione:**  prima di installare l'aggiornamento 1602, è possibile eseguire il controllo dei prerequisiti in modo indipendente dall'installazione dell'aggiornamento. Quando si installa l'aggiornamento nel sito, il controllo dei prerequisiti viene eseguito nuovamente.  

Per altre informazioni, vedere **Passaggio 3: Eseguire il controllo dei prerequisiti prima di installare un aggiornamento** nell'argomento [Aggiornamenti per Configuration Manager](../../../core/servers/manage/updates.md).  

> [!IMPORTANT]  
>  Quando viene eseguito il controllo dei prerequisiti in modo indipendente o nel contesto dell'installazione di un aggiornamento, il processo aggiorna alcuni file di origine del prodotto usati per le attività di manutenzione del sito. Di conseguenza, dopo aver eseguito il controllo dei prerequisiti ma prima di installare l'aggiornamento 1602, se si deve svolgere un'attività di manutenzione del sito, eseguire **Setupwfe.exe** (il programma di installazione di Configuration Manager) dalla cartella CD.Latest nel server del sito.  

 **Aggiornare i siti:** A questo punto è possibile avviare l'installazione dell'aggiornamento per la gerarchia. È consigliabile pianificare l'installazione dell'aggiornamento per ogni sito al di fuori del normale orario di ufficio in modo che il processo di installazione dell'aggiornamento e le azioni per reinstallare i componenti del sito e i ruoli del sistema del sito abbiano un impatto minimo sulle operazioni aziendali.

Per altre informazioni, vedere [Aggiornamenti per Configuration Manager](../../../core/servers/manage/updates.md).  

## <a name="see-also"></a>Vedere anche  
 [Aggiornamenti per Configuration Manager](../../../core/servers/manage/updates.md)
