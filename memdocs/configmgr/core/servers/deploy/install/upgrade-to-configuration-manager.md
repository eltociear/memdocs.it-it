---
title: Aggiornare a Current Branch
titleSuffix: Configuration Manager
description: Passaggi per eseguire l'aggiornamento sul posto da un sito e da una gerarchia che esegue System Center 2012 Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c64e7483-b4bb-4738-95f4-ecdaeb6a2ba6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a2a803a62f2b42c3b62a09e710a3ca74110a4257
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700409"
---
# <a name="upgrade-to-configuration-manager-current-branch"></a>Eseguire l'aggiornamento a Configuration Manager Current Branch

*Si applica a: Configuration Manager (Current Branch)*

Eseguire un aggiornamento sul posto a Configuration Manager Current Branch da un sito e da una gerarchia che esegue System Center 2012 Configuration Manager. Prima di eseguire l'aggiornamento da System Center 2012 Configuration Manager, è necessario preparare i siti. La preparazione richiede la rimozione di configurazioni specifiche che possono impedire la corretta esecuzione dell'aggiornamento. Seguire quindi la sequenza di aggiornamento quando sono presenti più siti.  

> [!TIP]  
> Quando si gestisce l'infrastruttura della gerarchia e dei siti di Configuration Manager, i termini *upgrade*, *aggiornamento* e *installazione* vengono usati per descrivere tre concetti distinti. Per informazioni su come viene usato ogni termine, vedere [Informazioni su upgrade, aggiornamento e installazione](../../../understand/upgrade-update-install.md).

## <a name="in-place-upgrade-paths"></a><a name="bkmk_path"></a> Percorsi di aggiornamento sul posto  

Attualmente per gli aggiornamenti sul posto sono supportate le opzioni seguenti:

### <a name="upgrade-to-version-2002"></a>Aggiornamento alla versione 2002

È possibile aggiornare i prodotti seguenti a una versione con *licenza completa* di Configuration Manager Current Branch versione 2002:

- Installazione di *valutazione* di Configuration Manager Current Branch versione 2002
- System Center 2012 Configuration Manager con Service Pack 1
- System Center 2012 Configuration Manager con Service Pack 2
- System Center 2012 R2 Configuration Manager
- System Center Configuration Manager 2012 R2 con Service Pack 1

Per altre informazioni, vedere [Domande frequenti relative ai rami e alle licenze di Configuration Manager](../../../understand/product-and-licensing-faq.md).

> [!TIP]  
> Se si esegue l'aggiornamento da una versione di System Center 2012 Configuration Manager alla versione Current Branch, il processo di aggiornamento potrebbe risultare semplificato. Per altre informazioni, vedere  
>
> - [Baseline and update versions](../../manage/updates.md#bkmk_Baselines) (Versioni di base e di aggiornamento)  
> - [Cartella CD.Latest](../../manage/the-cd.latest-folder.md)  

### <a name="unsupported-paths"></a>Percorsi non supportati

I percorsi seguenti non sono supportati:

- Non è supportato l'aggiornamento di una versione Technical Preview Branch a un'installazione con licenza completa. Una versione Technical Preview può essere aggiornata solo a una versione Technical Preview successiva.  

- Non è supportata la migrazione da una versione Technical Preview a una versione con licenza completa.  

## <a name="upgrade-checklists"></a><a name="bkmk_checklist"></a> Eseguire l'aggiornamento degli elenchi di controllo  

Gli elenchi di controllo seguenti possono aiutare a pianificare un aggiornamento a Configuration Manager.  

### <a name="before-you-upgrade"></a>Prima dell'aggiornamento  

Esaminare questi passaggi prima di eseguire l'aggiornamento a Configuration Manager.

#### <a name="review-your-system-center-2012-configuration-manager-environment"></a>Esaminare l'ambiente di System Center 2012 Configuration Manager

Risolvere i problemi come descritto in dettaglio nell'articolo di supporto tecnico Microsoft seguente: [Configuration Manager clients reinstall every five hours because of a recurring retry task and may cause an inadvertent client upgrade](https://support.microsoft.com/help/4018655).

#### <a name="make-sure-your-environment-meets-the-supported-configurations"></a>Assicurarsi che l'ambiente soddisfi le configurazioni supportate

- Esaminare la versione del sistema operativo server in uso per ospitare i ruoli del sistema del sito:  

  - Alcuni sistemi operativi precedenti supportati da System Center 2012 Configuration Manager non sono supportati da Configuration Manager Current Branch. Prima dell'aggiornamento, rimuovere i ruoli del sistema del sito in tali versioni del sistema operativo. Per altre informazioni, vedere [Sistemi operativi supportati per i server dei sistemi del sito](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md).

  - Il controllo dei prerequisiti per Configuration Manager non verifica i prerequisiti per i ruoli del sistema del sito nel server del sito o nei sistemi del sito remoto  

- Esaminare i prerequisiti richiesti in ciascun computer che ospita un ruolo del sistema del sito. Ad esempio, per distribuire un sistema operativo, Configuration Manager usa Windows 10 Assessment and Deployment Kit (Windows ADK). Prima di eseguire l'installazione, è necessario scaricare e installare Windows 10 ADK nel server del sito e in ciascun computer in cui è in esecuzione un'istanza del provider SMS.  

Per informazioni generali sulle piattaforme supportate e sulle configurazioni dei prerequisiti, vedere [Configurazioni supportate](../../../plan-design/configs/supported-configurations.md).  

Per altre informazioni sull'uso di Windows ADK con Configuration Manager, vedere [Requisiti dell'infrastruttura per la distribuzione del sistema operativo](../../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

#### <a name="review-the-site-and-hierarchy-status-and-verify-that-there-are-no-unresolved-issues"></a>Esaminare lo stato del sito e della gerarchia e verificare che non ci siano problemi non risolti

Prima di aggiornare un sito, risolvere tutti i problemi operativi per il server del sito, il server del database del sito e i ruoli del sistema del sito installati sui computer remoti. Un aggiornamento del sito può avere esito negativo a causa di problemi operativi esistenti.  

#### <a name="install-all-applicable-critical-updates-for-operating-systems-on-computers-that-host-the-site-the-site-database-server-and-remote-site-system-roles"></a>Installare tutti gli aggiornamenti critici applicabili per i sistemi operativi nei computer che ospitano il sito, il server di database del sito e i ruoli del sistema del sito remoto

Prima di aggiornare un sito, installare eventuali aggiornamenti critici per ogni sistema del sito applicabile. Se un aggiornamento installato richiede un riavvio, riavviare i computer interessati prima di iniziare l'aggiornamento del Service Pack.  

#### <a name="uninstall-the-site-system-roles-not-supported-by-configuration-manager"></a>Disinstallare i ruoli del sistema del sito non supportati da Configuration Manager

I ruoli del sistema del sito seguenti non vengono più usati in Configuration Manager. Disinstallarli prima di eseguire l'aggiornamento da System Center 2012 Configuration Manager:  

- Punto di gestione fuori banda  

- Punto di Convalida integrità sistema  

- Punto per siti Web e punto per servizi Web del Catalogo applicazioni

#### <a name="disable-database-replicas-for-management-points-at-primary-sites"></a>Disabilitare le repliche di database per i punti di gestione nei siti primari

Configuration Manager non può aggiornare un sito primario che ha una replica di database per i punti di gestione. Disabilitare la replica di database prima di:  

- Creare un backup del database del sito per verificare l'aggiornamento del database  

- Eseguire l'aggiornamento del sito di produzione a Configuration Manager Current Branch  

Per altre informazioni, vedere gli articoli seguenti:  

- System Center 2012 Configuration Manager: [Configurare le repliche di database per i punti di gestione](../configure/database-replicas-for-management-points.md#BKMK_DBReplica_Config)  

- Configuration Manager, Current Branch: [Repliche di database per i punti di gestione](../configure/database-replicas-for-management-points.md)  

#### <a name="reconfigure-software-update-points-that-use-nlb"></a>Riconfigurare i punti di aggiornamento software che usano Bilanciamento carico di rete

Configuration Manager non può aggiornare un sito che usa un cluster di Bilanciamento carico di rete per ospitare i punti di aggiornamento software.  

Se si usano i cluster NLB per i punti di aggiornamento software, usare PowerShell per rimuovere il cluster NLB. A partire da System Center 2012 Configuration Manager SP1, nella console di Configuration Manager non sono disponibili opzioni per configurare un cluster di Bilanciamento carico di rete.  

#### <a name="disable-all-site-maintenance-tasks-at-each-site-for-the-duration-of-that-sites-upgrade"></a>Disabilitare tutte le attività di manutenzione in ogni sito per l'intera durata dell'aggiornamento del sito

Prima di eseguire l'aggiornamento a Configuration Manager, disabilitare le eventuali attività di manutenzione del sito che potrebbero venire eseguite mentre è in corso il processo di aggiornamento. Queste comprendono, in via esemplificativa, le attività seguenti:  

- Backup server sito  
- Elimina operazioni client obsolete  
- Elimina dati di individuazione obsoleti  

Se un'attività di manutenzione del database del sito viene eseguita durante il processo di aggiornamento, l'aggiornamento del sito potrebbe non riuscire.  

Prima di disattivare un'attività, registrare la pianificazione dell'attività in modo da poter ripristinare la sua configurazione al termine dell'aggiornamento del sito.

Per altre informazioni sulle attività di manutenzione del sito, vedere gli articoli seguenti:  

- System Center 2012 Configuration Manager: [Pianificazione delle operazioni del sito](../../../plan-design/hierarchy/plan-for-the-site-database.md)  

- Configuration Manager, Current Branch: [Riferimento per le attività di manutenzione](../../manage/reference-for-maintenance-tasks.md)  

#### <a name="run-setup-prerequisite-checker"></a>Eseguire il controllo dei prerequisiti di installazione

Prima di aggiornare un sito, è possibile eseguire il **controllo dei prerequisiti** in modo indipendente dal programma di installazione per verificare che i prerequisiti per il sito siano soddisfatti. Successivamente, quando si aggiorna il sito, il controllo dei prerequisiti viene ripetuto.  

Il controllo dei prerequisiti indipendente valuta il sito per l'aggiornamento sia alla versione Current Branch sia alla versione Long-Term Servicing Branch (LTSB) di Configuration Manager. Poiché alcune funzionalità non sono supportate dalla versione LTSB, è possibile che in **ConfigMgrPrereq.log** siano presenti voci simili alle seguenti:

- `INFO: The site is a LTSB edition.`
- `Unsupported site system role 'Asset Intelligence synchronization point' for the LTSB edition;    Error;    Configuration Manager has detected that the 'Asset Intelligence synchronization point' is installed. Asset Intelligence is not supported on the LTSB edition. You must uninstall the Asset Intelligence synchronization point site system role before you can continue.`

Se si prevede di eseguire l'aggiornamento a Current Branch, è possibile ignorare gli errori per la versione LTSB. Tali errori sono rilevanti solo se si prevede di eseguire l'aggiornamento a LTSB.

Successivamente, quando si esegue l'installazione di Configuration Manager per l'aggiornamento, il controllo dei prerequisiti viene ripetuto. Questo controllo valuta il sito in base al ramo di Configuration Manager che si sceglie di installare (Current Branch o LTSB). Se si sceglie di eseguire l'aggiornamento a Current Branch, non viene eseguito il controllo delle funzionalità non supportate da LTSB.

Per altre informazioni, vedere [Controllo dei prerequisiti](prerequisite-checker.md) ed [Elenco dei controlli dei prerequisiti](list-of-prerequisite-checks.md).  

#### <a name="download-prerequisite-files-and-redistributable-files-for-configuration-manager"></a>Scaricare i file dei prerequisiti e i file ridistribuibili per Configuration Manager

Usare il **downloader di installazione** per scaricare i file ridistribuibili dei prerequisiti, i Language Pack e i più recenti aggiornamenti del prodotto per Configuration Manager.  

Per informazioni, vedere [Downloader di installazione](setup-downloader.md).  

#### <a name="plan-to-manage-server-and-client-languages"></a>Pianificare la gestione delle lingue di server e client

Quando si aggiorna un sito, l'aggiornamento del sito consente di installare solo le versioni di Language Pack selezionate durante l'aggiornamento.  

- Il programma di installazione esamina la configurazione della lingua corrente del sito. Identifica quindi i Language Pack disponibili nella cartella in cui sono stati archiviati in precedenza i file dei prerequisiti.  

- È possibile confermare la selezione dei Language Pack di server e client correnti oppure modificare le selezioni per aggiungere o rimuovere il supporto per le lingue.  

- È possibile selezionare solo i Language Pack che sono disponibili quando si esegue il programma di installazione.  

> [!NOTE]  
> Non è possibile usare i Language Pack di System Center 2012 Configuration Manager per abilitare le lingue per un sito di Configuration Manager Current Branch.  

Per altre informazioni sui Language Pack, vedere [Language Pack](language-packs.md).  

#### <a name="review-considerations-for-site-upgrades"></a>Esaminare le considerazioni per gli aggiornamenti del sito

Quando si aggiorna un sito, alcune funzionalità e configurazioni vengono ripristinati a una configurazione predefinita. Per prepararsi a queste modifiche e ad altre correlate, esaminare le informazioni in [Considerazioni sull'aggiornamento](#bkmk_considerations).  

#### <a name="create-a-backup-of-the-site-database-at-the-central-administration-site-and-primary-sites"></a>Creare un backup del database del sito nel sito di amministrazione centrale e nei siti primari

Prima di aggiornare un sito, eseguire il backup del database del sito per assicurarsi di disporre di un backup effettuato correttamente da usare in caso di ripristino di emergenza.  

Per altre informazioni, vedere [Backup e ripristino](../../manage/backup-and-recovery.md).  

#### <a name="back-up-a-customized-configurationmof-file"></a>Eseguire il backup di un file configuration.mof personalizzato

Se si usa un file configuration.mof personalizzato per definire le classi di dati usate con l'inventario hardware, creare un backup di tale file. Dopo l'aggiornamento, ripristinare il file nel sito. Per altre informazioni, vedere [Come estendere l'inventario hardware](../../../clients/manage/inventory/extend-hardware-inventory.md).  

#### <a name="test-the-database-upgrade-process-on-a-copy-of-the-most-recent-site-database-backup"></a>Testare il processo di aggiornamento del database in una copia del backup del database del sito più recente

Prima di effettuare l'aggiornamento di un sito di amministrazione centrale o sito primario di Configuration Manager, verificare il processo di aggiornamento del database del sito su una copia del database del sito.  

- Testare il processo di aggiornamento del database del sito. Quando si aggiorna un sito, il database del sito potrebbe venire modificato.  

- Il test dell'aggiornamento non è obbligatorio, ma permette di identificare i problemi per l'aggiornamento prima che influiscano sul database di produzione  

- Un aggiornamento non riuscito del database del sito può rendere inutilizzabile il database del sito e potrebbe richiedere un ripristino del sito per il relativo ripristino delle funzionalità  

- Nonostante il database del sito sia condiviso tra i siti nella gerarchia, pianificare un test del database in ciascun sito applicabile prima di aggiornare tale sito  

- Se si usano le repliche di database per i punti di gestione in un sito primario, disabilitare la replica prima di creare il backup del database del sito  

Configuration Manager non supporta né il backup di siti secondari, né l'aggiornamento di test del database di un sito secondario.  

L'esecuzione di un aggiornamento del database di test nel database del sito di produzione non è supportata. Questa operazione consente di aggiornare il database del sito e potrebbe rendere inutilizzabile il sito.  

Per altre informazioni, vedere [Testare l'aggiornamento del database del sito](#bkmk_test).  

#### <a name="restart-the-site-server-and-each-computer-that-hosts-a-site-system-role"></a>Riavviare il server del sito e ogni computer che ospita un ruolo del sistema del sito

Questa operazione ha lo scopo di garantire che non ci siano azioni in sospeso di un'installazione recente di aggiornamenti o dei prerequisiti.  

#### <a name="upgrade-sites"></a>Aggiornare i siti

A partire dal sito principale della gerarchia, eseguire Setup.exe dal supporto di origine di Configuration Manager.  

Dopo gli aggiornamenti del sito principale, è possibile iniziare l'aggiornamento di ogni sito figlio. Completare l'aggiornamento di ogni sito prima di iniziare l'aggiornamento del sito successivo.  

Finché tutti i siti della gerarchia non sono stati aggiornati a Configuration Manager, la gerarchia funziona in modalità mista.  

Per informazioni su come eseguire l'aggiornamento, vedere [Aggiornare i siti](#bkmk_upgrade).  

### <a name="after-you-upgrade"></a>Dopo l'aggiornamento  

Esaminare questi passaggi dopo l'aggiornamento a Configuration Manager.

#### <a name="upgrade-stand-alone-configuration-manager-consoles"></a>Aggiornare le console autonome di Configuration Manager

Per impostazione predefinita, quando si aggiorna un sito di amministrazione centrale o un sito primario, l'installazione aggiorna anche la console di Configuration Manager installata nel server del sito. Aggiornare manualmente ogni console installata in un computer diverso dal server del sito.  

> [!TIP]  
> Chiudere una console aperta prima di iniziare l'aggiornamento.  

Per altre informazioni, vedere [Installare la console di System Center Configuration Manager](install-consoles.md).  

#### <a name="reconfigure-database-replicas-for-management-points-at-primary-sites"></a>Riconfigurare le repliche di database per i punti di gestione nei siti primari

Se si usano repliche di database per i punti di gestione nei siti primari, disinstallare le repliche di database prima di aggiornare il sito. Dopo l'aggiornamento di un sito primario riconfigurare la replica di database per i punti di gestione.

Per altre informazioni, vedere [Repliche di database per i punti di gestione](../configure/database-replicas-for-management-points.md).  

#### <a name="reconfigure-any-database-maintenance-tasks-you-disabled-before-the-upgrade"></a>Riconfigurare eventuali attività di manutenzione del database disabilitate prima dell'aggiornamento

Se le [attività di manutenzione](../../manage/reference-for-maintenance-tasks.md) del database in un sito sono state disabilitate prima dell'aggiornamento, riconfigurare tali attività nel sito usando le stesse impostazioni presenti prima dell'aggiornamento.  

#### <a name="upgrade-clients"></a>Aggiornare i client

Dopo che tutti i siti sono stati aggiornati a Configuration Manager, pianificare l'aggiornamento dei client.  

Quando si aggiorna un client, il software client corrente viene disinstallato e viene installata la nuova versione del software client. Per aggiornare i client, è possibile usare qualsiasi metodo supportato da Configuration Manager.  

> [!TIP]  
> Quando si aggiorna il sito di livello superiore di una gerarchia, viene aggiornato anche il pacchetto di installazione del client in ogni punto di distribuzione presente nella gerarchia. Quando si aggiorna un sito primario, viene aggiornato il pacchetto di aggiornamento client disponibile da tale sito.  

Per altre informazioni, vedere [Come aggiornare i client per i computer Windows in System Center Configuration Manager](../../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

## <a name="considerations-for-upgrading"></a><a name="bkmk_considerations"></a> Considerazioni sull'aggiornamento  

### <a name="automatic-actions"></a>Azioni automatiche

Quando si esegue l'aggiornamento a Configuration Manager, vengono eseguite automaticamente le azioni seguenti:  

- Reimpostazione del sito. Questa azione include una reinstallazione di tutti i ruoli del sistema del sito.  

- Se il sito è il sito di livello superiore di una gerarchia, questo aggiorna il pacchetto di installazione del client in ogni punto di distribuzione presente nella gerarchia. Il sito aggiorna anche le immagini d'avvio predefinite per usare la nuova versione di Windows PE inclusa in Windows Assessment and Deployment Kit 10. Tuttavia, l'aggiornamento non aggiorna il supporto esistente da usare per la distribuzione delle immagini.  

- Se il sito è un sito primario, questo aggiorna il pacchetto di aggiornamento del client per tale sito.  

### <a name="manual-actions-after-an-upgrade"></a>Azioni manuali dopo un aggiornamento

Dopo l'aggiornamento di un sito, assicurarsi di eseguire le azioni seguenti:  

- Verificare che vengano eseguiti l'aggiornamento e l'installazione della nuova versione per i client assegnati a ogni sito primario  

- Aggiornare ogni console di Configuration Manager che si connette al sito e che viene eseguita in un computer remoto dal server del sito  

- Nei siti primari in cui si usano repliche di database per i punti di gestione, riconfigurare le repliche di database  

- Dopo che il sito viene aggiornato, aggiornare manualmente i supporti fisici come file ISO per CD, DVD o unità flash USB. Sono inclusi anche i supporti pre-installati forniti ai fornitori di hardware. L'aggiornamento del sito aggiorna le immagini d'avvio predefinite, ma non può aggiornate questi file dei supporti o i dispositivi usati esternamente a Configuration Manager.  

- Panificare l'aggiornamento delle immagini d'avvio personalizzate quando non è necessaria la versione precedente di Windows PE.  

### <a name="actions-that-affect-configurations-and-settings"></a>Azioni che influiscono su configurazioni e impostazioni

Quando un sito viene aggiornato a Configuration Manager, alcune configurazioni e impostazioni non vengono mantenute dopo l'aggiornamento. Per alcune configurazioni viene applicata una nuova impostazione predefinita. L'elenco seguente include alcune impostazioni che non vengono mantenute o che cambiano:  

- **Software Center**  
    I seguenti elementi di Software Center vengono reimpostati sui relativi valori predefiniti:  

  - **Informazioni di lavoro** viene reimpostato sull'orario di ufficio: dal lunedì al venerdì dalle **05.00** alle **22.00** .  

  - Il valore per **Manutenzione computer** è impostato su **Sospendi le attività di Software Center quando il computer si trova in modalità presentazione**.  

  - Il valore per **Controllo remoto** è impostato sul valore delle impostazioni client assegnate al computer.  

- **Pianificazioni dell'esecuzione del riepilogo degli aggiornamenti software**: Le pianificazioni di riepilogo personalizzate per gli aggiornamenti software o i gruppi di aggiornamenti software vengono reimpostate sul valore predefinito di 1 ora. Al termine dell'aggiornamento ripristinare i valori di riepilogo personalizzati sulla frequenza necessaria.  

## <a name="test-the-site-database-upgrade"></a><a name="bkmk_test"></a> Testare l'aggiornamento del database del sito  

Le informazioni seguenti si applicano solo quando si aggiorna un versione precedente, ad esempio System Center 2012 Configuration Manager, a Configuration Manager Current Branch.

Prima di aggiornare un sito, testare una copia del database di tale sito per l'aggiornamento.  

Per testare il database per un aggiornamento, ripristinare prima una copia del database del sito in un'istanza di SQL Server che non ospita un sito di Configuration Manager. La versione di SQL Server che si usa per ospitare la copia del database deve essere una versione supportata da Configuration Manager.  

Dopo il ripristino del database del sito, nel computer con SQL Server eseguire il programma di installazione di Configuration Manager dalla cartella dei supporti di origine per Configuration Manager. Usare l'opzione della riga di comando `/TESTDBUPGRADE`.  

Per altre informazioni, vedere gli articoli seguenti:

- [Eseguire il backup di un sito di Configuration Manager](../../manage/backup-and-recovery.md)  

- [Opzioni della riga di comando per l'installazione](command-line-options-for-setup.md#bkmk_setup)  

- [Supporto per le versioni di SQL Server](../../../plan-design/configs/support-for-sql-server-versions.md)  

> [!TIP]  
> Integrazione di Microsoft Intune con Configuration Manager:  
>
> quando si esegue un aggiornamento del database di test nella copia del database del sito che risale a 5 o più giorni fa, è possibile ricevere uno dei messaggi seguenti:  
>
> - WARN: Upgrade will force full sync to cloud.  
> - ERRORE: Database upgrade will force full sync to cloud.  
>
> Entrambi i messaggi possono essere ignorati durante il test di un aggiornamento del database. Non indicano un errore o un problema con l'aggiornamento di test. Indicano piuttosto che, durante l'aggiornamento effettivo, i dati del gruppo di replica di database **Cloud** potrebbero essere sincronizzati con Microsoft Intune.  

### <a name="test-a-site-database-for-upgrade"></a>Testare un database del sito per l'aggiornamento  

Usare la procedura seguente in ogni sito di amministrazione centrale e sito primario che si prevede di aggiornare:  

1. Eseguire una copia del database del sito. Ripristinare quindi tale copia in un'istanza di SQL Server che usa la stessa edizione del database del sito e che non ospita un sito di Configuration Manager. Ad esempio, se il sito del database esegue un'istanza dell'edizione Enterprise di SQL Server, assicurarsi di ripristinare il database in un'istanza di SQL Server che esegue anche l'edizione Enterprise di SQL Server.  

2. Dopo aver ripristinato la copia del database, eseguire il programma di installazione dal supporto di origine per Configuration Manager Current Branch. Quando si esegue l'installazione, usare l'opzione della riga di comando `/TESTDBUPGRADE`. Se l'istanza di SQL Server che ospita la copia del database non è quella predefinita, fornire anche gli argomenti della riga di comando per identificare l'istanza che ospita la copia del database del sito.  

    Ad esempio, si pianifica di aggiornare un database del sito con il nome database SMS_ABC. Si ripristina una copia di questo database del sito in un'istanza supportata di SQL Server con il nome istanza DBTest. Per testare un aggiornamento di questa copia del database del sito, usare la riga di comando seguente: `Setup.exe /TESTDBUPGRADE DBtest\CM_ABC`  

    Setup.exe si trova nel percorso seguente nel supporto di origine di Configuration Manager: `SMSSETUP\BIN\X64`  

3. Nell'istanza di SQL Server in cui si esegue il test di aggiornamento del database, monitorare ConfigMgrSetup.log nella radice dell'unità di sistema per l'avanzamento e il completamento:  

    - Se l'aggiornamento di test ha esito negativo, risolvere eventuali problemi correlati all'errore di aggiornamento del database del sito. Creare quindi un nuovo backup del database del sito e testare l'aggiornamento della nuova copia del database.  

    - Una volta completato il processo in modo corretto, è possibile eliminare la copia del database.  

        > [!NOTE]  
        > Non è supportato il ripristino della copia del database del sito usata per l'aggiornamento di test per l'uso in un database in qualsiasi sito.  

Dopo aver completato l'aggiornamento di una copia del database del sito, procedere con l'aggiornamento del sito di Configuration Manager e dei relativi database.  

## <a name="upgrade-sites"></a><a name="bkmk_upgrade"></a> Aggiornare i siti  

Una volta completate le attività seguenti, si è pronti per l'aggiornamento del sito di Configuration Manager:

- Configurazioni pre-aggiornamento per il sito
- Testare l'aggiornamento del database del sito su una copia del database
- Scaricare i file dei prerequisiti e i Language Pack per la versione che si prevede di installare

Quando si aggiorna un sito in una gerarchia, si aggiorna innanzitutto il sito di livello superiore della gerarchia. Questo sito di livello superiore è un sito di amministrazione centrale o un sito primario autonomo. Una volta completato l'aggiornamento di un sito di amministrazione centrale, è possibile aggiornare i siti primari figlio nell'ordine desiderato. Dopo aver aggiornato un sito primario, è possibile aggiornare i siti figlio secondari di tale sito oppure aggiornare i siti primari aggiuntivi prima di aggiornare eventuali siti secondari.  

Per aggiornare un sito di amministrazione centrale o un sito primario, eseguire il programma di installazione dal supporto di origine di Configuration Manager. Non eseguire il programma di installazione per aggiornare i siti secondari. Usare piuttosto la console di Configuration Manager per aggiornare un sito secondario dopo aver completato l'aggiornamento del relativo sito padre primario.  

Prima di aggiornare un sito, chiudere la console di Configuration Manager nel server del sito fino al completamento dell'aggiornamento del sito. Chiudere anche tutte le console di Configuration Manager in esecuzione in computer diversi dal server del sito. Una volta completato l'aggiornamento del sito, è possibile riconnettere la console. Finché una console di Configuration Manager non viene aggiornata alla nuova versione di Configuration Manager, tale console non visualizzerà comunque alcuni oggetti e informazioni disponibili nella nuova versione di Configuration Manager.  

### <a name="upgrade-a-central-administration-site-or-primary-site"></a>Aggiornare un sito di amministrazione centrale o un sito primario  

1. Verificare che l'utente che esegue l'installazione disponga dei seguenti privilegi di protezione:  

    - Diritti di **amministratore** locale nel server del sito  

    - Se il server di database del sito si trova in una posizione remota rispetto al server del sito, diritti di **amministratore** locale in tale server.  

2. Nel server del sito aprire il programma seguente: `<ConfigMgSourceMedia>\SMSSETUP\BIN\X64\Setup.exe`. Verrà avviata l'installazione guidata di Configuration Manager.  

3. Leggere le istruzioni nella pagina **Prima di iniziare** e quindi selezionare **Avanti**.  

4. Nella pagina **Introduzione** selezionare **Eseguire l'aggiornamento di questo sito di Configuration Manager** e quindi selezionare **Avanti**.  

5. Nella pagina **Codice Product Key**:  

    Se in precedenza è stata installata una versione di valutazione di Configuration Manager, è possibile selezionare **Installa versione con licenza di questo prodotto**. Immettere quindi il codice Product Key per l'installazione completa di Configuration Manager. In questo modo il sito verrà convertito alla versione completa.  

    È anche possibile specificare un valore in **Data di scadenza di Software Assurance** per il contratto di licenza, come utile promemoria per l'utente. Se non si immette questa data durante l'installazione, è possibile specificarla in un secondo momento dalla console di Configuration Manager.  

    > [!NOTE]  
    > Microsoft non convalida la data di scadenza immessa e non userà tale data per la convalida della licenza. È possibile usarla come promemoria della data di scadenza. Configuration Manager controlla periodicamente online la disponibilità di nuovi aggiornamenti software. Per usufruire di questi aggiornamenti aggiuntivi, è necessario che lo stato della licenza di Software Assurance sia valido.

    Per altre informazioni, vedere [Licenze e rami](../../../understand/learn-more-editions.md).

6. Nella pagina **Condizioni di licenza software Microsoft** leggere e accettare le condizioni di licenza e scegliere **Avanti**.  

7. Nella pagina **Licenze prerequisite** leggere e accettare le condizioni di licenza per i prerequisiti software e quindi selezionare **Avanti**. Il programma di installazione scarica e installa automaticamente il software nei client o nei sistemi del sito quando è necessario. Prima di procedere alla pagina successiva, è necessario accettare tutte le condizioni.  

8. Nella pagina **Download prerequisiti** specificare se il programma di installazione deve scaricare da Internet i contenuti più recenti o se usare i file scaricati in precedenza. Questi contenuti includono i file ridistribuibili dei prerequisiti, i Language Pack e i più recenti aggiornamenti di prodotto. Se i file sono stati scaricati in precedenza tramite Setup Downloader, selezionare **Usa file scaricati precedentemente** e specificare la cartella di download. Per altre informazioni, vedere [Setup Downloader](setup-downloader.md) (Downloader di installazione).  

    > [!NOTE]  
    > Quando si usano i file scaricati in precedenza, verificare che il percorso alla cartella di download contenga la versione più recente dei file.  

9. Nella pagina **Selezione della lingua server** , visualizzare l'elenco delle lingue installate al momento per il sito. Selezionare le lingue aggiuntive disponibili nel sito per la console di Configuration Manager e per i report. È anche possibile deselezionare le lingue per le quali non è più necessario il supporto nel sito. La lingua inglese è selezionata per impostazione predefinita e non può essere rimossa.  

    > [!IMPORTANT]  
    > Nessuna versione di Configuration Manager può usare i Language Pack di una versione precedente di Configuration Manager. Per abilitare il supporto per un lingua in un sito di Configuration Manager che viene aggiornato, è necessario usare la versione del Language Pack per quella nuova versione. Se, ad esempio, durante l'aggiornamento da System Center 2012 Configuration Manager a Configuration Manager Current Branch la versione di un Language Pack di Current Branch non è disponibile nei file dei prerequisiti scaricati, non sarà possibile installare il supporto per tale lingua.  

10. Nella pagina **Selezione della lingua client** , visualizzare l'elenco delle lingue installate al momento per il sito. Selezionare le lingue aggiuntive disponibili su questo sito per i computer client oppure deselezionare le lingue che non si desidera più supportare nel sito. Specificare se si desidera abilitare tutte le lingue client per i client dei dispositivi mobili, quindi fare clic su **Avanti**. La lingua inglese è selezionata per impostazione predefinita e non può essere rimossa.  

11. Nella pagina **Riepilogo impostazioni** esaminare la configurazione. Quando si è pronti, selezionare **Avanti** per avviare il controllo dei prerequisiti e verificare l'idoneità del server all'aggiornamento del sito.  

12. Nella pagina **Controllo prerequisiti dell'installazione** se non sono segnalati problemi selezionare **Avanti** per aggiornare il sito e i ruoli del sistema del sito.

    Se il controllo dei prerequisiti rileva un problema, selezionare un elemento nell'elenco per informazioni dettagliate su come risolverlo. Risolvere tutte le anomalie associate agli elementi nell'elenco con uno stato di **Errore** prima di procedere con l'installazione. Dopo aver risolto il problema, fare clic su **Esegui controllo** per riavviare il controllo dei prerequisiti. È inoltre possibile aprire il file ConfigMgrPrereq.log nella radice dell'unità di sistema per esaminare i risultati del controllo dei prerequisiti. Il file di log può contenere informazioni aggiuntive che non vengono visualizzate nell'interfaccia utente. Per un elenco delle regole e delle descrizioni dei prerequisiti di installazione, vedere [List of Prerequisite Checks for System Center Configuration Manager](list-of-prerequisite-checks.md) (Elenco dei controlli dei prerequisiti per System Center Configuration Manager).

Nella pagina **Aggiorna** il programma di installazione consente di visualizzare lo stato di avanzamento generale. Quando il programma di installazione completa l'installazione del sistema del sito e del server del sito di base, è possibile chiudere la procedura guidata. La configurazione del sito continua in background.  

### <a name="upgrade-a-secondary-site"></a>Aggiornare un sito secondario  

1. Verificare che l'utente amministratore che esegue il programma di installazione disponga dei seguenti privilegi di protezione:  

    - Diritti di **amministratore** locale nel server del sito secondario  

    - Ruolo di sicurezza **Amministratore infrastruttura** o **Amministratore completo** nel sito primario padre  

    - Diritti di **amministratore di sistema** nel database del sito secondario  

2. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito** e selezionare il nodo **Siti**.  

3. Selezionare il sito secondario da aggiornare. Nella scheda **Home** della barra multifunzione selezionare **Aggiorna** nel gruppo **Sito**.  

4. Selezionare **Sì** per confermare la decisione e avviare l'aggiornamento del sito secondario.  

L'aggiornamento del sito secondario viene eseguito in background. Dopo aver completato l'aggiornamento, verificare lo stato nella console di Configuration Manager. Selezionare il server del sito secondario e quindi nella scheda **Home** della barra multifunzione selezionare **Mostra stato installazione** nel gruppo **Sito**.  

## <a name="post-upgrade-tasks"></a><a name="BKMK_PostUpgrade"></a> Attività successive all'aggiornamento  

Dopo aver aggiornato un sito, potrebbe essere necessario eseguire attività aggiuntive per completare l'aggiornamento o riconfigurare il sito. Queste attività possono includere quanto segue:

- Aggiornare i client di Configuration Manager
- Aggiornare le console di Configuration Manager
- Riabilitare le repliche di database per i punti di gestione
- Ripristinare le impostazioni per le funzionalità di Configuration Manager usate che non vengono mantenute dopo l'aggiornamento  
