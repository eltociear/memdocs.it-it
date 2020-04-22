---
title: Eseguire la migrazione dei dati
titleSuffix: Configuration Manager
description: Informazioni su come trasferire i dati da una gerarchia di origine a una gerarchia di destinazione di Configuration Manager.
ms.date: 11/05/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cf014eb0-f8c2-4d37-b8d7-368d63a10b89
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a3771011f2822bb93a9569ec534b77259e2e8dc3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701749"
---
# <a name="migrate-data-between-hierarchies-in-configuration-manager"></a>Eseguire la migrazione dei dati da una gerarchia all'altra in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Usare la migrazione per trasferire i dati da una gerarchia di origine supportata alla gerarchia di destinazione di Configuration Manager (Current Branch). Quando si esegue la migrazione dei dati da una gerarchia di origine:  

- Si accede ai dati dai database del sito nell'infrastruttura di origine e quindi si trasferiscono i dati nell'ambiente corrente.  

- La migrazione non modifica i dati nella gerarchia di origine. La migrazione individua i dati e archivia una copia nel database della gerarchia di destinazione.  

Quando si pianifica la strategia di migrazione, tenere presente quanto segue:  

- È possibile eseguire la migrazione di un'infrastruttura di Configuration Manager 2007 SP2 esistente in Configuration Manager (Current Branch).  

- È possibile eseguire la migrazione di alcuni o tutti i dati supportati da un sito di origine.  

- È possibile eseguire la migrazione dei dati da un singolo sito di origine a più siti diversi nella gerarchia di destinazione.  

- È possibile spostare i dati da più siti di origine a un singolo sito nella gerarchia di destinazione.  


Il video seguente descrive e illustra due [scenari di migrazione](#BKMK_MigrationScenarios) comuni. Contiene anche le opzioni per includere Microsoft Azure nelle pianificazioni delle migrazioni.
> [!VIDEO https://www.youtube.com/embed/6_0EwW-5b4E]



##  <a name="concepts"></a><a name="BKMK_MigrationConcepts"></a> Concetti  

 Durante la migrazione Configuration Manager usa i concetti e i termini seguenti.  

#### <a name="source-hierarchy"></a>Gerarchia di origine
Gerarchia che esegue una versione supportata di Configuration Manager e che contiene i dati di cui si vuole eseguire la migrazione. Quando si configura la migrazione, la gerarchia di origine viene identificata quando si specifica il sito principale di una gerarchia di origine. Dopo aver specificato una gerarchia di origine, il sito di livello superiore della gerarchia di destinazione raccoglie i dati dal database del sito di origine designato per rilevare i dati che è possibile migrare. 

Per altre informazioni, vedere [Gerarchie di origine](planning-a-source-hierarchy-strategy.md#BKMK_Source_Hierarchies).

#### <a name="source-sites"></a>Siti di origine
I siti nella gerarchia di origine che includono i dati che è possibile migrare alla gerarchia di destinazione. 

Per altre informazioni, vedere [Siti di origine](planning-a-source-hierarchy-strategy.md#BKMK_Source_Sites).

#### <a name="destination-hierarchy"></a>Gerarchia di destinazione
Gerarchia di Configuration Manager (Current Branch) in cui viene eseguita la migrazione per l'importazione dei dati da una gerarchia di origine.

#### <a name="data-gathering"></a>Raccolta dati
Il processo continuo di rilevamento delle informazioni in una gerarchia di origine che è possibile migrare nella gerarchia di destinazione. Configuration Manager controlla la gerarchia di origine in una pianificazione. Il processo rileva eventuali modifiche alle informazioni contenute nella gerarchia di origine migrate in precedenza e che è possibile aggiornare nella gerarchia di destinazione.

Per altre informazioni, vedere [Raccolta dati](planning-a-source-hierarchy-strategy.md#BKMK_Data_Gathering).

#### <a name="migration-jobs"></a>Processi di migrazione
Il processo di configurazione di oggetti specifici da migrare e quindi la gestione della migrazione di tali oggetti nella gerarchia di destinazione.

Per altre informazioni, vedere [Pianificazione di una strategia di processo di migrazione](planning-a-migration-job-strategy.md).

#### <a name="client-migration"></a>Migrazione client
Il processo di trasferimento delle informazioni che i client utilizzano dal database del sito di origine al database della gerarchia di destinazione. Il processo di migrazione dei dati è quindi seguito da un aggiornamento del software client dei dispositivi alla versione del software client dalla gerarchia di destinazione.

Per altre informazioni, vedere [Pianificazione di una strategia di migrazione client](planning-a-client-migration-strategy.md).

#### <a name="shared-distribution-points"></a>Punti di distribuzione condivisi
I punti di distribuzione della gerarchia di origine che Configuration Manager condivide con la gerarchia di destinazione durante il periodo di migrazione.

Durante il periodo di migrazione, i client assegnati ai siti nella gerarchia di destinazione possono ottenere il contenuto dai punti di distribuzione condivisi.

Per altre informazioni, vedere [Condividere punti di distribuzione tra gerarchie di origine e destinazione](planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration).

#### <a name="monitoring-migration"></a>Monitoraggio della migrazione
Il processo di monitoraggio delle attività di migrazione. È possibile monitorare lo stato e l'esito migrazione dal nodo **Migrazione** nell'area di lavoro **Amministrazione** .

Per altre informazioni, vedere [Pianificazione del monitoraggio dell'attività di migrazione](planning-to-monitor-migration-activity.md).

#### <a name="stop-gathering-data"></a>Interrompere la raccolta dati
Il processo di interruzione della raccolta dati dai siti di origine. Quando non sono più disponibili dati da migrare da una gerarchia di origine oppure se si vuole sospendere le attività relative alla migrazione, è possibile configurare la gerarchia di destinazione per l'interruzione della raccolta dati da tale gerarchia.

Per altre informazioni, vedere [Raccolta dati](planning-a-source-hierarchy-strategy.md#BKMK_Data_Gathering).

#### <a name="clean-up-migration-data"></a>Pulire i dati della migrazione
Il processo di completamento della migrazione da una gerarchia di origine tramite la rimozione delle informazioni sulla migrazione dal database delle gerarchie di destinazione.

Per altre informazioni, vedere [Pianificazione del completamento della migrazione](planning-to-complete-migration.md).



## <a name="typical-workflow"></a>Flusso di lavoro tipico  

Per configurare un flusso di lavoro per la migrazione:

1.  Specificare una gerarchia di origine supportata.  

2.  Configurare la raccolta dati. La raccolta dati consente a Configuration Manager di raccogliere informazioni sui dati che è possibile migrare dalla gerarchia di origine.  

     Configuration Manager ripete automaticamente il processo di raccolta dati in una pianificazione semplice finché il processo non viene interrotto. Per impostazione predefinita, il processo di raccolta dati si ripete ogni quattro ore in modo che Configuration Manager possa rilevare le modifiche ai dati nella gerarchia di origine. La raccolta dati è necessaria anche per condividere i punti di distribuzione.  

3.  Creare processi di migrazione per la migrazione di dati tra la gerarchia di origine e la gerarchia di destinazione.  

4.  È possibile interrompere il processo di raccolta dati in qualsiasi momento usando l'azione **Interrompi raccolta dati**. Quando si interrompe una raccolta dati, Configuration Manager non rileva più le modifiche ai dati nella gerarchia di origine e non è più in grado di condividere i punti di distribuzione. In genere, è possibile utilizzare questa azione se si prevede di non migrare più i dati né di condividere i punti di distribuzione dalla gerarchia di origine.  

5.  Facoltativamente, dopo che la raccolta dati è stata interrotta in tutti i siti per la gerarchia di origine, è possibile pulire i dati della migrazione usando l'azione **Pulisci dati migrazione**. Questa azione consente di eliminare i dati cronologici sulla migrazione da una gerarchia di origine dal database della gerarchia di destinazione.  

Dopo aver eseguito la migrazione dei dati, quando la gerarchia di origine non è più necessaria per la gestione dei dispositivi nell'ambiente, è possibile rimuovere le autorizzazioni per la gerarchia di origine e l'infrastruttura.  



##  <a name="scenarios"></a><a name="BKMK_MigrationScenarios"></a> Scenari  

 Configuration Manager supporta gli scenari di migrazione seguenti:
- [Migrazione da gerarchie di Configuration Manager 2007](#bkmk_2007)  
- [Migrazione da Configuration Manager 2012 o un'altra gerarchia di Configuration Manager](#bkmk_2012)

> [!NOTE]  
>  L'espansione di una gerarchia con sito autonomo in una gerarchia con sito di amministrazione centrale non viene classificata come migrazione. Per informazioni sull'espansione delle gerarchie, vedere [Espandere un sito primario autonomo](../servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand).  


### <a name="migration-from-configuration-manager-2007-hierarchies"></a><a name="bkmk_2007"></a> Migrazione da gerarchie di Configuration Manager 2007  

 Quando si usa la migrazione per migrare i dati da Configuration Manager 2007 è possibile mantenere l'investimento nell'infrastruttura del sito esistente e ottenere i vantaggi seguenti:  

#### <a name="site-database-improvements"></a>Miglioramenti del database del sito
Il database di Configuration Manager (Current Branch) supporta Unicode.

#### <a name="database-replication-between-sites"></a>Replica di database tra siti
La replica in Configuration Manager (Current Branch) è basata su Microsoft SQL Server. Questo comportamento migliora le prestazioni del trasferimento dati da sito a sito.

#### <a name="user-centric-management"></a>Gestione incentrata sull'utente
In Configuration Manager (Current Branch) le attività di gestione sono incentrate sugli utenti. Ad esempio, è possibile distribuire il software a un utente anche se non si conosce il nome del dispositivo per l'utente. Configuration Manager offre agli utenti un maggiore controllo sul software da installare nei dispositivi e su quando installarlo.

#### <a name="hierarchy-simplification"></a>Semplificazione della gerarchia
Configuration Manager (Current Branch) consente di creare una gerarchia dei siti più semplice. Questo miglioramento è dovuto all'introduzione del tipo di sito di amministrazione centrale e alle modifiche al comportamento dei siti primari e secondari. Configuration Manager (Current Branch) usa una minor quantità di larghezza di banda e richiede un minor numero di server rispetto alle versioni precedenti.

#### <a name="role-based-administration"></a>Amministrazione basata su ruoli
Questo modello di sicurezza centrale in Configuration Manager (Current Branch) offre sicurezza a livello di gerarchia e una gestione che risponde ai requisiti aziendali e amministrativi.

> [!NOTE]  
>  A causa delle modifiche alla progettazione introdotte in System Center 2012 Configuration Manager, non è possibile aggiornare Configuration Manager 2007 a Configuration Manager (Current Branch). L'aggiornamento sul posto è supportato da System Center 2012 Configuration Manager a Configuration Manager (Current Branch).  


### <a name="migration-from-configuration-manager-2012-or-another-configuration-manager-hierarchy"></a><a name="bkmk_2012"></a> Migrazione da Configuration Manager 2012 o un'altra gerarchia di Configuration Manager  
 Il processo di migrazione dei dati da una gerarchia di System Center 2012 Configuration Manager o di Configuration Manager è uguale. Il processo include la migrazione dei dati da più gerarchie di origine a una singola gerarchia di destinazione. È possibile usare questo processo quando la società acquisisce risorse aggiuntive già gestite da Configuration Manager. È anche possibile eseguire la migrazione dei dati da un ambiente di test all'ambiente di produzione di Configuration Manager. Questo processo consente di preservare gli investimenti effettuati per l'ambiente di test di Configuration Manager.  



## <a name="see-also"></a>Vedere anche  

-   [Pianificare la migrazione a Configuration Manager](planning-for-migration.md)  

-   [Configurazione di gerarchie di origine e siti di origine per la migrazione](configuring-source-hierarchies-and-source-sites-for-migration.md)  

-   [Operazioni per la migrazione](operations-for-migration.md)  

-   [Sicurezza e privacy per la migrazione](security-and-privacy-for-migration.md)  

-   [Iniziare a usare Configuration Manager](../servers/deploy/start-using.md)
