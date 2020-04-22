---
title: Aggiornare l'infrastruttura locale
titleSuffix: Configuration Manager
description: Informazioni su come aggiornare l'infrastruttura, ad esempio SQL Server e il sistema operativo dei sistemi del sito.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8ca970dd-e71c-404f-9435-d36e773a0db2
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 033c5de1a85ce2fa8b11fe7a187fcc4d5c023931
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704299"
---
# <a name="upgrade-on-premises-infrastructure-that-supports-configuration-manager"></a>Aggiornare l'infrastruttura locale che supporta Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Le informazioni disponibili in questo articolo consentono di aggiornare l'infrastruttura server che esegue Configuration Manager.  

- Per eseguire l'*aggiornamento* a Configuration Manager Current Branch da una versione precedente, vedere [Eseguire l'aggiornamento a Configuration Manager](../deploy/install/upgrade-to-configuration-manager.md).  

- Per *aggiornare* l'infrastruttura di Configuration Manager Current Branch a una versione più recente, vedere [Aggiornamenti per Configuration Manager](updates.md).  


## <a name="upgrade-the-os-of-site-systems"></a><a name="BKMK_SupConfigUpgradeSiteSrv"></a> Aggiornare il sistema operativo dei sistemi del sito  

Configuration Manager supporta l'aggiornamento sul posto del sistema operativo server che ospita un server del sito e un ruolo qualsiasi del sistema del sito, nelle situazioni seguenti:  

- Se Configuration Manager supporta comunque il livello di Service Pack di Windows risultante, supporta l'aggiornamento sul posto a una versione di Service Pack di Windows Server successiva.  

- Aggiornamento sul posto:  

    - Da Windows Server 2016 a Windows Server 2019  

    - Da Windows Server 2012 R2 a Windows Server 2019  

    - Da Windows Server 2012 R2 a Windows Server 2016  

    - Da Windows Server 2012 a Windows Server 2016  

    - Eseguire l'aggiornamento da Windows Server 2012 a Windows Server 2012 R2  

    - Da Windows Server 2008 R2 a Windows Server 2012 R2  

Per aggiornare un server, eseguire la procedura di aggiornamento indicata dal sistema operativo interessato dall'aggiornamento. Vedere gli articoli seguenti:  

- [Windows Server Upgrade Center](https://aka.ms/upgradecenter)  

- [Opzioni di aggiornamento e conversione per Windows Server 2016](https://docs.microsoft.com/windows-server/get-started/supported-upgrade-paths)  

- [Upgrade Options for Windows Server 2012 R2](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn303416(v=ws.11)) (Opzioni di aggiornamento per Windows Server 2012 R2)  

### <a name="upgrade-to-windows-server-2016-or-2019"></a><a name="bkmk_2016-2019"></a> Eseguire l'aggiornamento a Windows Server 2016 o 2019

Seguire la procedura descritta in questa sezione per uno degli scenari di aggiornamento seguenti:  

- Aggiornamento di Windows Server 2012 R2 o Windows Server 2016 a Windows Server 2019  

- Aggiornamento di Windows Server 2012 o Windows Server 2012 R2 a Windows Server 2016  

#### <a name="before-upgrade"></a>Prima dell'aggiornamento

- (Windows Server 2012 o Windows Server 2012 R2): Rimuovere il client di System Center Endpoint Protection (SCEP). In Windows Server è ora incorporato Windows Defender, che sostituisce il client di System Center Endpoint Protection. La presenza di questo client può impedire l'aggiornamento a Windows Server.  

- Rimuovere il ruolo WSUS dal server, se installato. È possibile conservare il database WSUS e ricollegarlo dopo la reinstallazione di WSUS.  

- Se si sta aggiornando il sistema operativo del server del sito, verificare che la [replica basata su file](../../plan-design/hierarchy/file-based-replication.md) sia integra per il sito. Controllare tutte le cartelle di posta in arrivo per verificare la presenza di un backlog sia nei siti di origine che in quelli di destinazione. Se sono presenti molti processi di replica bloccati o in sospeso, attendere che vengano cancellati.<!-- SCCMDocs#1792 -->
    - Nel sito di origine esaminare **sender.log**.
    - Nel sito di destinazione esaminare **despooler.log**.

#### <a name="after-upgrade"></a>Dopo l'aggiornamento

- Verificare che Windows Defender sia abilitato, impostato per l'avvio automatico e in esecuzione.  

- Verificare che i servizi di Configuration Manager seguenti siano in esecuzione:  

    - SMS_EXECUTIVE  

    - SMS_SITE_COMPONENT_MANAGER  

- Verificare che i servizi **Attivazione processo Windows** e **WWW/W3svc** siano abilitati e impostati per l'avvio automatico. Il processo di aggiornamento disabilita questi servizi. Verificare quindi che siano in esecuzione per i ruoli del sistema del sito seguenti:  

    - Server del sito  

    - Punto di gestione  

    - Punto per servizi Web del Catalogo applicazioni  

    - Punto per siti Web del Catalogo applicazioni  

- Assicurarsi che ogni server che ospita un ruolo del sistema del sito continui a soddisfare tutti i [prerequisiti](../../plan-design/configs/site-and-site-system-prerequisites.md). Potrebbe essere necessario ad esempio reinstallare BITS, WSUS, o configurare impostazioni specifiche per IIS.  

- Dopo aver ripristinato i prerequisiti mancanti, riavviare di nuovo il server per assicurarsi che i servizi siano stati avviati e siano operativi.  

- Se si sta aggiornando il server del sito primario, [eseguire una reimpostazione del sito](modify-your-infrastructure.md#bkmk_reset).  

#### <a name="known-issue-for-remote-configuration-manager-consoles"></a>Problema noto per le console remote di Configuration Manager

Dopo aver aggiornato il server del sito o un'istanza del provider SMS, non è possibile connettersi con la console di Configuration Manager. Per risolvere questo problema, ripristinare manualmente le autorizzazioni per il gruppo **SMS Admins** in WMI. Le autorizzazioni devono essere impostate nel server del sito e in ogni server remoto che ospita un'istanza del provider SMS:

1. Nei server applicabili aprire Microsoft Management Console (MMC), aggiungere lo snap-in per **Controllo WMI** e quindi selezionare **Computer locale**.  

2. In MMC aprire le **Proprietà** di **Controllo WMI (computer locale)** e selezionare la scheda **Sicurezza**.  

3. Espandere l'albero sotto Radice, selezionare il nodo **SMS** e quindi scegliere **Sicurezza**.  Assicurarsi che il gruppo **SMS Admins** abbia le autorizzazioni seguenti:  

    - Abilita account  

    - Abilita remoto  

4. Nella scheda **Sicurezza** sotto il nodo **SMS** selezionare il nodo **site_&lt;codicesito>** e quindi scegliere **Sicurezza**. Assicurarsi che il gruppo **SMS Admins** abbia le autorizzazioni seguenti:  

    - Esegui metodi  

    - Scrittura provider  

    - Abilita account  

    - Abilita remoto  

5. Salvare le autorizzazioni per ripristinare l'accesso per la console di Configuration Manager.  

#### <a name="known-issue-for-remote-site-systems"></a>Problema noto per i sistemi del sito remoto

Dopo aver aggiornato un server che ospita un ruolo del sistema del sito, il valore `Software\Microsoft\SMS` potrebbe risultare mancante dalla chiave del Registro di sistema seguente: `HKLM\SYSTEM\CurrentControlSet\Control\SecurePipeServers\Winreg\AllowedPaths`

Se questo valore non è presente dopo l'aggiornamento di Windows nel server, aggiungerlo manualmente. In caso contrario, i ruoli del sistema del sito possono avere problemi di caricamento dei file in arrivo nel server del sito.

### <a name="upgrade-to-windows-server-2012-r2"></a><a name="bkmk_2012r2"></a> Eseguire l'aggiornamento a Windows Server 2012 R2

Quando si esegue l'aggiornamento da Windows Server 2008 R2 o da Windows Server 2012 a Windows Server 2012 R2, si applicano le condizioni seguenti:

#### <a name="before-upgrade"></a>Prima dell'aggiornamento

- In Windows Server 2012: Rimuovere il ruolo WSUS dal server, se installato. È possibile conservare il database WSUS e ricollegarlo dopo la reinstallazione di WSUS.  

- In Windows Server 2008 R2: Prima di eseguire l'aggiornamento a Windows Server 2012 R2, è necessario disinstallare WSUS 3.2 dal server. È possibile conservare il database WSUS e ricollegarlo dopo la reinstallazione di WSUS. Per altre informazioni, vedere [Windows Server Update Services Overview](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh852345(v=ws.11)#new-and-changed-functionality) (Panoramica di Windows Server Update Services).  

- Se si sta aggiornando il sistema operativo del server del sito, verificare che la [replica basata su file](../../plan-design/hierarchy/file-based-replication.md) sia integra per il sito. Controllare tutte le cartelle di posta in arrivo per verificare la presenza di un backlog sia nei siti di origine che in quelli di destinazione. Se sono presenti molti processi di replica bloccati o in sospeso, attendere che vengano cancellati.<!-- SCCMDocs#1792 -->
    - Nel sito di origine esaminare **sender.log**.
    - Nel sito di destinazione esaminare **despooler.log**.

#### <a name="after-upgrade"></a>Dopo l'aggiornamento

- Il processo di aggiornamento disabilita Servizi di distribuzione Windows. Assicurarsi che questo servizio sia avviato e in esecuzione per i ruoli del sistema del sito seguenti:  

    - Server del sito  

    - Punto di gestione  

    - Punto per servizi Web del Catalogo applicazioni  

    - Punto per siti Web del Catalogo applicazioni  

- Verificare che i servizi **Attivazione processo Windows** e **WWW/W3svc** siano abilitati e impostati per l'avvio automatico. Il processo di aggiornamento disabilita questi servizi. Verificare quindi che siano in esecuzione per i ruoli del sistema del sito seguenti:  

    - Server del sito  

    - Punto di gestione  

    - Punto per servizi Web del Catalogo applicazioni  

    - Punto per siti Web del Catalogo applicazioni  

- Assicurarsi che ogni server che ospita un ruolo del sistema del sito continui a soddisfare tutti i [prerequisiti](../../plan-design/configs/site-and-site-system-prerequisites.md). Potrebbe essere necessario ad esempio reinstallare BITS, WSUS, o configurare impostazioni specifiche per IIS.  

    Dopo aver ripristinato i prerequisiti mancanti, riavviare di nuovo il server per assicurarsi che i servizi siano stati avviati e siano operativi.  

### <a name="unsupported-upgrade-scenarios"></a>Scenari di aggiornamento non supportati

Sono solitamente richiesti, ma non sono supportati da Configuration Manager gli scenari di aggiornamento di Windows Server seguenti:  

- Da Windows Server 2008 a Windows Server 2012 o versione successiva  

- Da Windows Server 2008 R2 a Windows Server 2012  


## <a name="upgrade-the-os-of-clients"></a><a name="BKMK_SupConfigUpgradeClient"></a> Aggiornare il sistema operativo dei client  

Configuration Manager supporta un aggiornamento sul posto del sistema operativo per client di Configuration Manager nelle situazioni seguenti:  

- Se Configuration Manager supporta il livello di Service Pack risultante, supporta l'aggiornamento sul posto a una versione di Service Pack di Windows successiva.  

- Aggiornamento sul posto di Windows da una versione supportata di Windows 10. Per altre informazioni, vedere [Aggiornare Windows alla versione più recente](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md).  

- Aggiornamenti di manutenzione da build a build di Windows 10. Per altre informazioni, vedere [Gestire Windows come servizio](../../../osd/deploy-use/manage-windows-as-a-service.md).  


## <a name="upgrade-sql-server"></a><a name="BKMK_SupConfigUpgradeDBSrv"></a> Aggiornare SQL Server  

Configuration Manager supporta l'aggiornamento sul posto di SQL Server nel server di database del sito.

Per informazioni sulle versioni di SQL Server supportate da Configuration Manager, vedere [Supporto per le versioni di SQL Server](../../plan-design/configs/support-for-sql-server-versions.md).  

### <a name="upgrade-the-service-pack-version-of-sql-server"></a>Aggiornamento della versione del Service Pack di SQL Server

Se Configuration Manager supporta comunque il livello di Service Pack di SQL Server risultante, supporta l'aggiornamento sul posto a una versione di Service Pack di SQL Server successiva.

In presenza di più siti di Configuration Manager in una gerarchia, ogni sito può eseguire una versione di Service pack di SQL Server diversa. Non esiste alcuna limitazione per l'ordine di aggiornamento della versione del Service Pack di SQL Server dei siti.

### <a name="upgrade-to-a-new-version-of-sql-server"></a>Eseguire l'aggiornamento a una nuova versione di SQL Server

Configuration Manager supporta l'aggiornamento sul posto di SQL Server alle versione seguenti:

- SQL Server 2017  

- SQL Server 2016  

- SQL Server 2014  

È incluso l'aggiornamento di SQL Server Express a una versione più recente di SQL Server Express nei siti secondari.

Quando si aggiorna la versione di SQL Server che ospita il database del sito, è necessario aggiornare la versione di SQL Server usata nei siti nell'ordine seguente:

1. Eseguire prima l'aggiornamento di SQL Server nel sito di amministrazione centrale  

2. Aggiornare i siti secondari prima di eseguire l'aggiornamento del sito primario padre di un sito secondario  

3. Aggiornare per ultimo i siti primari padre. Questi siti includono sia i siti primari figlio che fanno riferimento a un sito di amministrazione centrale sia i siti primari autonomi che sono siti di livello superiore di una gerarchia.  

### <a name="sql-server-cardinality-estimation-level"></a>Livello di stima della cardinalità di SQL Server

Quando si aggiorna un database del sito da una versione precedente di SQL Server, il database mantiene il livello di stima della cardinalità SQL esistente, se questo corrisponde al minimo consentito per l'istanza di SQL Server. L'aggiornamento di SQL Server con un database a un livello di compatibilità inferiore a quello consentito imposta automaticamente il database sul livello di compatibilità più basso consentito da SQL Server.

La tabella seguente identifica i livelli di compatibilità consigliati per i database del sito di Configuration Manager:

|Versione di SQL Server | Livelli di compatibilità supportati | Livello consigliato |
|----------------|--------------------|--------|
| SQL Server 2017 | 140, 130, 120, 110  | 140 |
| SQL Server 2016 | 130, 120, 110  | 130 |
| SQL Server 2014 | 120, 110      | 110 |

Per identificare il livello di compatibilità di stima della cardinalità di SQL Server in uso per il database del sito, eseguire la query SQL seguente nel server di database del sito:  

```SQL
SELECT name, compatibility_level FROM sys.databases
```

Per altre informazioni sui livelli di compatibilità CE di SQL e su come impostarli, vedere [Livello di compatibilità ALTER DATABASE (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level?view=sql-server-2017).

Per altre informazioni sull'aggiornamento di SQL Server, vedere gli articoli su SQL Server seguenti:  

- [Eseguire l'aggiornamento a SQL Server 2017](https://docs.microsoft.com/sql/database-engine/install-windows/supported-version-and-edition-upgrades-2017)  

- [Eseguire l'aggiornamento a SQL Server 2016](https://docs.microsoft.com/sql/database-engine/install-windows/supported-version-and-edition-upgrades?view=sql-server-2016)  

- [Eseguire l'aggiornamento a SQL Server 2014](https://docs.microsoft.com/sql/database-engine/install-windows/supported-version-and-edition-upgrades?view=sql-server-2014)  

### <a name="to-upgrade-sql-server-on-the-site-database-server"></a>Per aggiornare SQL Server nel server di database del sito  

1. Arrestare tutti i servizi di Configuration Manager nel sito  

2. Aggiornare SQL Server a una versione supportata  

3. Riavviare i servizi di Configuration Manager  

> [!NOTE]  
> Quando si modifica l'edizione di SQL Server in uso presso il sito di amministrazione centrale da Standard a Datacenter o Enterprise, la partizione del database non viene modificata. Questa partizione del database limita il numero dei client supportati dalla gerarchia.  
