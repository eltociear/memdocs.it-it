---
title: Controlli dei prerequisiti
titleSuffix: Configuration Manager
description: Informazioni di riferimento sugli specifici controlli dei prerequisiti per gli aggiornamenti di Configuration Manager.
ms.date: 05/07/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6a279624-ffc9-41aa-8132-df1809708dd5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2dd722ddcf0e5ea6e944a76366204ac83ede05ec
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88698957"
---
# <a name="list-of-prerequisite-checks-for-configuration-manager"></a>Elenco dei controlli dei prerequisiti per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Questo articolo illustra in dettaglio i controlli dei prerequisiti che vengono eseguiti quando si installa o si aggiorna Configuration Manager. Per altre informazioni, vedere [Controllo prerequisiti](prerequisite-checker.md).  



## <a name="errors"></a>Errori

### <a name="active-migration-mappings-on-the-target-primary-site"></a>Mapping di migrazione attivi nel sito primario di destinazione

*Si applica a: sito di amministrazione centrale*

Non sono presenti mapping di migrazione attivi nei siti primari.

### <a name="active-replica-mp"></a>Replica di MP attiva

*Si applica a: sito primario*

È presente una replica del punto di gestione attiva.

### <a name="administrative-rights-on-expand-primary-site"></a>Diritti amministrativi nel sito primario di espansione

*Si applica a: sito di amministrazione centrale*

Quando un sito primario viene espanso in una gerarchia, l'account utente che esegue l'installazione ha privilegi di **amministratore** nel server del sito primario autonomo.

### <a name="administrative-rights-on-site-system"></a>Diritti amministrativi sul sistema del sito

*Si applica a: sito di amministrazione centrale, sito primario, sito secondario*

L'account utente che esegue l'installazione di Configuration Manager ha privilegi di **amministratore** per il server del sito.

### <a name="administrator-rights-on-central-administration-site"></a>Diritti di amministratore per il sito di amministrazione centrale

*Si applica a: sito primario*

L'account utente che esegue l'installazione di Configuration Manager ha privilegi di **amministratore** per il server del sito di amministrazione centrale.

### <a name="asset-intelligence-synchronization-point-on-the-expanded-primary-site"></a>Punto di sincronizzazione di Asset Intelligence nel sito primario espanso

*Si applica a: sito di amministrazione centrale*

Quando si espande un sito primario in una gerarchia, il ruolo del punto di sincronizzazione di Asset Intelligence non è installato nel sito primario autonomo.

### <a name="bits-enabled"></a>BITS attivato

*Si applica a: punto di gestione*

Servizio trasferimento intelligente in background (BITS, Background Intelligent Transfert Service) è installato nel punto di gestione. Questo controllo può non riuscire per uno dei motivi seguenti:

- BITS non è installato  

- Il componente di compatibilità WMI IIS 6.0 per IIS 7.0 non è installato nel server o nell'host IIS remoto  

- Non è stato possibile verificare le impostazioni IIS remote I componenti comuni IIS non sono installati nel server del sito.  

### <a name="case-insensitive-collation-on-sql-server"></a>Regole di confronto senza distinzione tra maiuscole e minuscole nel server SQL

*Si applica a: server di database del sito*

L'installazione di SQL Server usa regole di confronto senza distinzione tra maiuscole e minuscole, come ad esempio **SQL_Latin1_General_CP1_CI_AS**.

### <a name="central-administration-site-server-administrative-rights-on-expand-primary-site"></a>Privilegi di amministratore per il server del sito di amministrazione centrale su espansione sito primario

*Si applica a: sito di amministrazione centrale*

Quando si espande un sito primario in una gerarchia, l'account computer del sito di amministrazione centrale ha privilegi di **amministratore** per il sito primario autonomo.

### <a name="client-version-on-management-point-computer"></a>Versione client nel computer del punto di gestione

*Si applica a: punto di gestione*

Si sta installando il punto di gestione in un server che non ha una versione diversa del client di Configuration Manager installato.

### <a name="cloud-management-gateway-on-the-expanded-primary-site"></a>Gateway di gestione cloud nel sito primario espanso

*Si applica a: sito di amministrazione centrale*

Quando si espande un sito primario in una gerarchia, il ruolo gateway di gestione cloud non è installato nel sito primario autonomo.

### <a name="connection-to-sql-server-on-central-administration-site"></a>Connessione a SQL Server nel sito di amministrazione centrale

*Si applica a: sito primario*

L'account utente che esegue l'installazione di Configuration Manager nel sito primario per l'aggiunta a una gerarchia esistente ha il ruolo **sysadmin** per l'istanza di SQL Server per il sito di amministrazione centrale.

### <a name="custom-client-agent-settings-have-nap-enabled"></a>Protezione accesso alla rete abilitata nelle impostazioni personalizzate dell'agente client

*Si applica a: sito di amministrazione centrale, sito primario*

Non esistono impostazioni personalizzate del client che abilitano protezione accesso alla rete.

### <a name="data-warehouse-service-point-on-the-expanded-primary-site"></a>Punto di servizio del data warehouse non supportato nel sito primario espanso

*Si applica a: sito di amministrazione centrale*

Quando si espande un sito primario in una gerarchia, il ruolo Punto di servizio del data warehouse non è installato nel sito primario autonomo.

### <a name="dedicated-sql-server-instance"></a>Istanza di SQL Server dedicata

*Si applica a: sito di amministrazione centrale, sito primario, sito secondario*

È stata configurata un'istanza dedicata di SQL Server per ospitare il database del sito di Configuration Manager.

Se un altro sito usa l'istanza, è necessario selezionare un'istanza diversa per il nuovo sito. È anche possibile disinstallare l'altro sito o spostare il relativo database in un'istanza diversa di SQL Server.

### <a name="default-client-agent-settings-have-nap-enabled"></a>Protezione accesso alla rete abilitata nelle impostazioni predefinite dell'agente client

*Si applica a: sito di amministrazione centrale, sito primario*

Le impostazioni predefinite del client non abilitano protezione accesso alla rete.

### <a name="domain-membership-error"></a>Appartenenza al dominio (errore)

*Si applica a: sito di amministrazione centrale, sito primario, sito secondario, provider SMS, SQL Server*

Il computer di Configuration Manager è membro di un dominio di Windows.

### <a name="endpoint-protection-point-on-the-expanded-primary-site"></a>Punto di Endpoint Protection nel sito primario espanso

*Si applica a: sito di amministrazione centrale*

Quando si espande un sito primario in una gerarchia, il ruolo del punto di Endpoint Protection non è installato nel sito primario autonomo.

### <a name="existing-configuration-manager-server-components-on-server"></a>Componenti del server di Configuration Manager esistenti nel server

*Si applica a: sito di amministrazione centrale, sito primario, sito secondario*

Un server del sito o un ruolo del sistema del sito non è installato nel server selezionato per l'installazione del sito.

### <a name="existing-stand-alone-primary-site-for-version-and-site-code"></a>Versione e codice sito del sito primario autonomo esistente

*Si applica a: sito di amministrazione centrale, sito primario*

Il sito primario che si intende espandere è un sito primario autonomo. Ha la stessa versione di Configuration Manager, ma un codice sito diverso rispetto al sito di amministrazione centrale da installare.

### <a name="firewall-exception-for-sql-server"></a>Eccezione firewall per SQL Server

*Si applica a: sito di amministrazione centrale, sito primario, sito secondario, punto di gestione*

Windows Firewall è disattivato o è stata generata un'eccezione rilevante di Windows Firewall per SQL Server.

Consentire l'accesso remoto a Sqlservr.exe o alle porte TCP richieste. Per impostazione predefinita, SQL Server è in ascolto sulla porta TCP 1433 e SQL Server Service Broker (SSB) usa la porta TCP 4022.

### <a name="free-disk-space-on-site-server"></a>Spazio su disco disponibile nel server di sito

*Si applica a: sito di amministrazione centrale, sito primario, sito secondario*

Per installare il server del sito, il computer deve avere almeno 15 GB di spazio libero su disco. Se si installa il provider SMS nello stesso server, è necessario 1 GB di spazio libero aggiuntivo.

### <a name="iis-service-running"></a>Servizio IIS in esecuzione

*Si applica a: punto di gestione, punto di distribuzione*

IIS è installato e in esecuzione nel server per il punto di gestione o il punto di distribuzione.

### <a name="incompatible-collection-references"></a>Riferimenti a raccolte non compatibili

*Si applica a: sito di amministrazione centrale*

Durante un aggiornamento le raccolte fanno riferimento solo ad altre raccolte dello stesso tipo.

### <a name="match-collation-of-expand-primary-site"></a>Creare corrispondenze con le regole di confronto del sito primario di espansione

*Si applica a: sito di amministrazione centrale*

Quando si espande un sito primario in una gerarchia, il sito del database per il sito primario autonomo usa le stesse regole di confronto del database del sito nel sito di amministrazione centrale.

### <a name="maximum-text-replication-size-for-sql-server-always-on-availability-groups"></a>Dimensioni massime replica testo per i gruppi di disponibilità Always On di SQL Server

*Si applica a: server di database del sito*

Quando si usa SQL Server Always On, l'impostazione **max text repl size** deve essere configurata correttamente. Per altre informazioni, vedere [Preparare l'uso di gruppi di disponibilità Always On di SQL Server con Configuration Manager](../configure/sql-server-alwayson-for-a-highly-available-site-database.md).

### <a name="microsoft-intune-connector-on-the-expanded-primary-site"></a>Connettore Microsoft Intune nel sito primario espanso

*Si applica a: sito di amministrazione centrale*

Quando si espande un sito primario in una gerarchia, il ruolo del connettore Microsoft Intune non è installato nel sito primario autonomo.

### <a name="microsoft-remote-differential-compression-rdc-library-registered"></a>Libreria di Compressione differenziale remota Microsoft (RDC) registrata

*Si applica a: sito di amministrazione centrale, sito primario, sito secondario*

La libreria Connessione Desktop remoto è registrata nel server del sito di Configuration Manager.

### <a name="microsoft-windows-installer"></a>Microsoft Windows Installer

*Si applica a: sito di amministrazione centrale, sito primario, sito secondario*

Verifica la versione di Windows Installer.

Se questo controllo ha esito negativo, l'installazione non riesce a verificare la versione oppure la versione installata non soddisfa il requisito minimo di Windows Installer 4.5.

### <a name="minimum-net-framework-version-for-configuration-manager-console"></a>Versione minima di .NET Framework per la console di Configuration Manager

*Si applica a: console di Configuration Manager*

Microsoft .NET Framework 4.0 è installato nel computer della console di Configuration Manager.

### <a name="minimum-net-framework-version-for-configuration-manager-site-server"></a>Versione minima di .NET Framework per il server del sito di Configuration Manager

*Si applica a: sito di amministrazione centrale, sito primario, sito secondario*

.NET Framework 3.5 è installato o abilitato nel server del sito di Configuration Manager.

### <a name="minimum-net-framework-version-for-sql-server-express-edition-installation-for-configuration-manager-secondary-site"></a>Versione minima di .NET Framework per l'installazione di SQL Server Express per il sito secondario di Configuration Manager

*Si applica a: sito secondario*

.NET Framework 4.0 è installato o abilitato nel server del sito secondario di Configuration Manager. Questa versione è necessaria per SQL Server Express.

### <a name="parent-database-collation"></a>Regole di confronto database principale

*Si applica a: sito primario, sito secondario*

Le regole di confronto del database del sito corrispondono a quelle del database del sito padre. Tutti i siti in una gerarchia devono usare le stesse regole di confronto del database.

### <a name="parent-site-replication-status"></a>Stato di replica del sito padre

*Si applica a: sito di amministrazione centrale, sito primario*

Lo stato della replica del sito padre è **Replica attiva** (stato **125**).

### <a name="pending-system-restart"></a>Riavvio del sistema in sospeso

*Si applica a: sito di amministrazione centrale, sito primario, sito secondario*

Prima di eseguire l'installazione, un altro programma necessita del riavvio del server.

A partire dalla versione 1810, questo controllo è più resiliente. Per verificare se il computer è in uno stato di riavvio in sospeso, vengono controllate le posizioni del Registro di sistema seguenti:<!--SCCMDocs-pr issue 3010-->  

- `HKLM:Software\Microsoft\Windows\CurrentVersion\Component Based Servicing\RebootPending`  

- `HKLM:SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired`  

- `HKLM:SYSTEM\CurrentControlSet\Control\Session Manager, PendingFileRenameOperations`  

- `HKLM:Software\Microsoft\ServerManager, CurrentRebootAttempts`  

### <a name="primary-fqdn"></a>FQDN primario

*Si applica a: sito di amministrazione centrale, sito primario, sito secondario, server di database del sito*

Il nome NetBIOS del computer corrisponde al nome host locale nel nome di dominio completo (FQDN).

### <a name="read-only-domain-controller"></a>Controller di dominio di sola lettura

*Si applica a: sito di amministrazione centrale, sito primario, sito secondario*

I server di database del sito e i server dei siti secondari non sono supportati in un controller di dominio di sola lettura.

Per altre informazioni, vedere l'articolo del supporto tecnico Microsoft relativo ai [problemi riscontrati durante l'installazione di SQL Server in un controller di dominio](https://support.microsoft.com/help/2032911).

### <a name="required-sql-server-collation"></a>Regole di confronto di SQL Server richieste

*Si applica a: sito di amministrazione centrale, sito primario, sito secondario*

L'istanza di SQL Server è configurata per usare le regole di confronto **SQL_Latin1_General_CP1_CI_AS**.

Se il database del sito di Configuration Manager è già installato, questo controllo si applica anche al database. Per informazioni su come modificare le regole di confronto del database e dell'istanza di SQL Server, vedere [Regole di confronto e supporto Unicode di SQL](/sql/relational-databases/collations/collation-and-unicode-support).

Se si usa un sistema operativo cinese ed è necessario il supporto GB18030, questo controllo non è applicabile. Per altre informazioni sull'attivazione del supporto GB18030, vedere [Supporto internazionale](../../../plan-design/hierarchy/international-support.md).

### <a name="server-service-is-running"></a>Il servizio Server è in esecuzione

*Si applica a: sito di amministrazione centrale, sito primario, sito secondario*

Il servizio Server è avviato e in esecuzione.

### <a name="setup-source-folder"></a>Cartella di origine di installazione

*Si applica a: sito secondario*

L'account computer per il sito secondario ha le autorizzazioni seguenti per accedere alla cartella origine di installazione e per la condivisione:

- Autorizzazioni **Read** del file system NTFS  

- Autorizzazioni **Read** di condivisione  

> [!Note]  
> Se si usano condivisioni amministrative, ad esempio C$ e D$, l'account computer del sito secondario deve essere un **amministratore** nel server.  

### <a name="setup-source-version"></a>Versione dell'origine installazione

*Si applica a: sito secondario*

La versione di Configuration Manager nella cartella di origine specificata per l'installazione del sito secondario corrisponde alla versione di Configuration Manager del sito primario.

### <a name="site-code-in-use"></a>Codice del sito in uso

*Si applica a: sito primario*

Il codice del sito specificato non è già in uso nella gerarchia di Configuration Manager. Specificare un codice univoco per questo sito.

### <a name="site-server-computer-account-administrative-rights"></a>Diritti amministrativi dell'account computer del server di sito

*Si applica a: sito primario, server di database del sito*

L'account computer del server del sito ha i privilegi di **amministratore** per SQL Server e il punto di gestione.

### <a name="site-server-fqdn-length"></a>Lunghezza del nome di dominio completo del server del sito

*Si applica a: sito di amministrazione centrale, sito primario, sito secondario*

Lunghezza del nome di dominio completo del server del sito.

### <a name="site-server-in-passive-mode-on-the-expanded-primary-site"></a>Server del sito in modalità passiva sul sito primario espanso

*Si applica a: sito di amministrazione centrale*

Quando si espande un sito primario in una gerarchia, il ruolo Server del sito in modalità passiva non è installato nel sito primario autonomo.

### <a name="sms-provider-in-same-domain-as-site-server"></a>Il provider SMS ha lo stesso dominio del server del sito

*Si applica a: provider SMS*

Tutte le istanze del provider SMS sono nello stesso dominio del server del sito.

### <a name="software-update-point-in-nlb-configuration"></a>Punto di aggiornamento software nella configurazione di Bilanciamento carico di rete

*Si applica a: Punto di aggiornamento software*

Il sito non sta usando Bilanciamento carico di rete con alcuna posizione virtuale per i punti di aggiornamento software attivi.

### <a name="software-update-point-using-a-load-balancer"></a>Punto di aggiornamento software che usa un servizio di bilanciamento del carico

*Si applica a: Punto di aggiornamento software*

Configuration Manager non supporta i punti di aggiornamento software nei servizi di bilanciamento del carico di rete o hardware.

### <a name="sql-server-always-on-availability-groups"></a>Gruppi di disponibilità Always On di SQL Server

*Si applica a: server di database del sito*

Quando si usa SQL Server Always On, deve rispettare i requisiti minimi per l'hosting di un gruppo di disponibilità. Per altre informazioni, vedere [Preparare l'uso di gruppi di disponibilità Always On di SQL Server con Configuration Manager](../configure/sql-server-alwayson-for-a-highly-available-site-database.md).

### <a name="sql-server-availability-group-configured-for-readable-secondaries"></a>Gruppo di disponibilità SQL Server configurato per le repliche secondarie leggibili

*Si applica a: server di database del sito*

Quando si usa SQL Server Always On, controllare lo stato di lettura delle repliche secondarie del gruppo di disponibilità.

### <a name="sql-server-availability-group-configured-for-manual-failover"></a>Gruppo di disponibilità SQL Server configurato per il failover manuale

*Si applica a: server di database del sito*

Quando si usa SQL Server Always On, le repliche del gruppo di disponibilità sono configurate per il failover manuale.

### <a name="sql-server-availability-group-replicas-on-default-instance"></a>Repliche del gruppo di disponibilità SQL Server nell'istanza predefinita

*Si applica a: server di database del sito*

Quando si usa SQL Server Always On, le repliche del gruppo di disponibilità sono nell'istanza predefinita.

### <a name="sql-availability-group-replicas-must-all-have-the-same-seeding-mode"></a>Tutte le repliche dei gruppi di disponibilità SQL devono avere la stessa modalità seeding

<!-- SCCMDocs-pr#3899 -->
*Si applica a: server di database del sito*

A partire dalla versione 1906, quando si usa SQL Server Always On è necessario configurare le repliche dei gruppi di disponibilità con la stessa [modalità seeding](/sql/database-engine/availability-groups/windows/automatic-seeding-secondary-replicas).

### <a name="sql-availability-group-replicas-must-be-healthy"></a>Le repliche dei gruppi di disponibilità di SQL devono essere integre

<!-- SCCMDocs-pr#3899 -->
*Si applica a: server di database del sito*

A partire dalla versione 1906, quando si usa SQL Server Always On, le repliche del gruppo di disponibilità sono integre.

### <a name="sql-server-configuration-for-site-upgrade"></a>Configurazione di SQL Server per l'aggiornamento del sito

*Si applica a: server di database del sito*

SQL Server rispetta i requisiti minimi per l'aggiornamento del sito. Per altre informazioni, vedere [Versioni di SQL Server supportate](../../../plan-design/configs/support-for-sql-server-versions.md).

### <a name="sql-server-edition"></a>Edizione di SQL Server

*Si applica a: server di database del sito*

SQL Server nel sito non è SQL Server Express.

### <a name="sql-server-express-on-secondary-site"></a>SQL Server Express nel sito secondario

*Si applica a: sito secondario*

SQL Server Express può essere installato correttamente nel server del sito secondario.

### <a name="sql-server-on-the-secondary-site-server"></a>SQL Server nel server del sito secondario

*Si applica a: sito secondario*

SQL Server è installato nel server del sito secondario. Non è possibile installare SQL Server in un sistema del sito remoto per un sito secondario.

> [!Warning]  
> Il controllo viene eseguito solo quando si configura il programma di installazione in modo che usi un'istanza esistente di SQL Server.  

### <a name="sql-server-service-running-account"></a>Account di esecuzione del servizio SQL Server

*Si applica a: sito di amministrazione centrale, sito primario, sito secondario*

L'account di accesso per il servizio SQL Server non è un account utente locale o di tipo **LOCAL SERVICE**.

È necessario configurare il servizio SQL Server per usare un account di dominio valido, di tipo **NETWORK SERVICE** o **LOCAL SYSTEM**.

### <a name="sql-server-site-database-consistency"></a>Coerenza del database del sito SQL Server

*Si applica a: server di database del sito*

Verificare la coerenza del database.

### <a name="sql-server-sysadmin-rights"></a>Diritti di amministratore di sistema di SQL Server

*Si applica a: server di database del sito*

L'account utente che esegue l'installazione di Configuration Manager ha il ruolo **sysadmin** per l'istanza di SQL Server selezionata per l'installazione del database del sito. Questo controllo ha esito negativo anche quando l'installazione non riesce ad accedere all'istanza di SQL Server per verificare le autorizzazioni.

### <a name="sql-server-sysadmin-rights-for-reference-site"></a>Diritti di amministratore di sistema SQL Server per sito di riferimento

*Si applica a: server di database del sito*

L'account utente che esegue l'installazione di Configuration Manager ha il ruolo **sysadmin** per l'istanza del ruolo di SQL Server selezionata come database del sito di riferimento. Le autorizzazioni del ruolo **sysadmin** di SQL Server sono necessarie per modificare il database del sito.

### <a name="sql-server-tcp-port"></a>Porta TCP di SQL Server

*Si applica a: server di database del sito*

Il protocollo TCP è abilitato per l'istanza di SQL Server ed è impostato per usare una porta statica.

### <a name="sql-server-version"></a>Versione di SQL Server

*Si applica a: server di database del sito*

Una versione supportata di SQL Server è installata nel server di database del sito specificato.

Per altre informazioni, vedere [Supporto per le versioni di SQL Server](../../../plan-design/configs/support-for-sql-server-versions.md).

### <a name="unsupported-os-for-configuration-manager-console"></a>Sistemi operativi non supportati per la console di Configuration Manager

*Si applica a: console di Configuration Manager*

Installare la console di Configuration Manager in computer che eseguono una versione del sistema operativo supportata.

Per altre informazioni, vedere [Sistemi operativi supportati per le console di Configuration Manager](../../../plan-design/configs/supported-operating-systems-consoles.md).

### <a name="unsupported-os-for-site-server"></a>Sistema operativo non supportato per il server del sito

*Si applica a: sito di amministrazione centrale, sito primario, sito secondario, console di Configuration Manager, punto di gestione, punto di distribuzione*

Il server esegue una versione supportata del sistema operativo.

Per altre informazioni, vedere [Sistemi operativi supportati per i server dei sistemi del sito di Configuration Manager](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md).

### <a name="unsupported-site-system-role-out-of-band-service-point"></a>Ruolo del sistema del sito non supportato: Punto di servizio fuori banda

*Si applica a: sito primario*

Il ruolo del sistema del sito Punto di servizio fuori banda non è installato.

### <a name="unsupported-site-system-role-system-health-validation-point"></a>Ruolo del sistema del sito non supportato: Punto di Convalida integrità sistema

*Si applica a: sito primario*

Il ruolo del sistema del sito Punto di Convalida integrità sistema non è installato.

### <a name="unsupported-upgrade-path"></a>Percorso di aggiornamento non supportato

*Si applica a: sito di amministrazione centrale, sito primario*

Tutti i server del sito della gerarchia sono conformi alla versione minima di Configuration Manager richiesta per l'aggiornamento.

### <a name="usmt-installed"></a>USMT non installata

*Si applica a: sito di amministrazione centrale, sito primario (solo autonomo)*

Il componente Utilità di migrazione stato utente (USMT) di Windows Assessment and Deployment Kit (ADK) per Windows è installato.

### <a name="validate-fqdn-of-sql-server"></a>Convalida del nome di dominio completo di SQL Server

*Si applica a: server di database del sito*

È stato specificato un nome di dominio completo valido per il computer SQL Server.

### <a name="verify-central-administration-site-version"></a>Verificare la versione del sito di amministrazione centrale

*Si applica a: sito primario*

La versione del sito di amministrazione centrale è la stessa di Configuration Manager.

### <a name="verify-database-consistency"></a>Verificare la coerenza del database

*Si applica a: sito di amministrazione centrale, sito primario*

Verifica la coerenza del database del sito in SQL Server.  

### <a name="windows-deployment-tools-installed"></a>Strumenti di distribuzione Windows installati

*Si applica a: provider SMS*

Il componente Strumenti di distribuzione Windows di Windows ADK è installato.

### <a name="windows-failover-cluster"></a>Cluster di failover Windows

*Si applica a: server del sito, punto di gestione, punto di distribuzione*

Server con i ruoli del server del sito, del punto di gestione o del punto di distribuzione che non fanno parte di un cluster Windows.

A partire dalla versione 1810, il programma di installazione di Configuration Manager non blocca più l'installazione del ruolo del server del sito in un computer con il ruolo Windows per il clustering di failover. Poiché SQL Always On richiede questo ruolo, non era possibile in precedenza inserire il database del sito nel server del sito. Con questa modifica, è possibile creare un sito a disponibilità elevata con un minor numero di server usando SQL Always On e un server del sito in modalità passiva. Per altre informazioni, vedere [Opzioni di disponibilità elevata](../configure/high-availability-options.md). <!--1359132-->  

### <a name="windows-pe-installed"></a>Windows PE installato

*Si applica a: provider SMS*

Il componente Ambiente preinstallazione di Windows di Windows ADK è installato.



## <a name="warnings"></a>avvisi

### <a name="active-directory-domain-functional-level"></a>Livello di funzionalità del dominio di Active Directory

*Si applica a: sito di amministrazione centrale, sito primario*

Il livello di funzionalità del dominio e delle foreste di Active Directory è almeno Windows Server 2008 R2. Per altre informazioni, vedere [Supporto per i domini di Active Directory](../../../plan-design/configs/support-for-active-directory-domains.md).

### <a name="administrative-rights-on-distribution-point"></a>Diritti amministrativi sul punto di distribuzione

*Si applica a: punto di distribuzione*

L'account utente che esegue il programma di installazione ha i privilegi di **amministratore** per il punto di distribuzione.

### <a name="administrative-rights-on-management-point"></a>Diritti amministrativi sul punto di gestione

*Si applica a: punto di gestione, punto di distribuzione*

L'account computer del server del sito ha i privilegi di **amministratore** per il punto di gestione e il punto di distribuzione.

### <a name="administrative-share-site-system"></a>Condivisione amministrativa (sistema del sito)

*Si applica a: punto di gestione*

Le condivisioni amministrative necessarie sono presenti nel computer del sistema del sito.

### <a name="application-compatibility"></a>Compatibilità delle applicazioni

*Si applica a: sito di amministrazione centrale, sito primario*

Le applicazioni correnti sono compatibili con lo schema dell'applicazione.

### <a name="backlogged-inboxes"></a>Cartelle posta in arrivo con backlog

*Si applica a: sito di amministrazione centrale, sito primario*

Il server del sito elabora tempestivamente le cartelle di posta in arrivo critiche. Tali cartelle non contengono file antecedenti a un giorno.

Controlla le cartelle della posta in arrivo seguenti:

- `despoolr.box\receive\*.i??`

- `despoolr.box\receive\*.s??`

- `despoolr.box\receive\*.nil`

- `schedule.box\requests\*.sr?`

Per risolvere questo avviso, controllare se i componenti despooler e utilità di pianificazione del sistema del sito sono in esecuzione.

### <a name="bits-installed"></a>BITS installato

*Si applica a: punto di gestione*

Servizio trasferimento intelligente in background (BITS, Background Intelligent Transfert Service) è installato e abilitato in IIS.

### <a name="check-if-the-site-uses-upgrade-readiness-cloud-service-connector"></a>Controlla se il sito usa il connettore del servizio cloud Preparazione aggiornamenti

*Si applica a: sito di amministrazione centrale, sito primario*

Il servizio Preparazione aggiornamenti è stato ritirato il 31 gennaio 2020. Per altre informazioni, vedere [KB 4521815: Ritiro di Windows Analytics il 31 gennaio 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement).

Desktop Analytics è l'evoluzione di Windows Analytics. Per altre informazioni, vedere [Che cos'è Desktop Analytics](../../../../desktop-analytics/overview.md).

Se il sito di Configuration Manager aveva una connessione a Preparazione aggiornamenti, è necessario rimuoverla e riconfigurare i client. Per altre informazioni, vedere [Rimuovere la connessione a Preparazione aggiornamenti](../../../clients/manage/upgrade-readiness.md#bkmk_remove).

Se si ignora questo avviso sui prerequisiti, il programma di installazione di Configuration Manager rimuove automaticamente il connettore Preparazione aggiornamenti.<!-- #4898 -->

### <a name="cloud-management-gateway-requires-either-token-based-authentication-or-an-https-management-point"></a>Cloud Management Gateway richiede l'autenticazione basata su token o un punto di gestione HTTP

*Si applica a: Cloud Management Gateway*

Con alcune versioni di Configuration Manager, non è possibile usare un punto di gestione HTTP con Cloud Management Gateway. Configurare Cloud Management Gateway per HTTPS oppure configurare il sito per l'HTTP migliorato. Per altre informazioni, vedere [Plan for cloud management gateway](../../../clients/manage/cmg/plan-cloud-management-gateway.md) (Pianificare il gateway di gestione cloud).

### <a name="configuration-for-sql-server-memory-usage"></a>Configurazione per l'utilizzo della memoria di SQL Server

*Si applica a: server di database del sito*

SQL Server è configurato per un uso illimitato della memoria. Configurare la memoria di SQL Server impostando un limite massimo.

### <a name="distribution-point-package-version"></a>Versione del pacchetto dei punti di distribuzione

*Si applica a: Punti di distribuzione*

Tutti i punti di distribuzione del sito dispongono della versione più recente dei pacchetti di distribuzione software.

### <a name="domain-membership-warning"></a>Appartenenza al dominio (avviso)

*Si applica a: punto di gestione, punto di distribuzione*

Il computer di Configuration Manager è membro di un dominio di Windows.

### <a name="firewall-exception-for-sql-server-standalone-primary-site"></a>Eccezione firewall per SQL Server (sito primario autonomo)

*Si applica a: sito primario (solo autonomo)*

Windows Firewall è disattivato o è stata generata un'eccezione rilevante di Windows Firewall per SQL Server.

Consentire l'accesso remoto a Sqlservr.exe o alle porte TCP richieste. Per impostazione predefinita, SQL Server è in ascolto sulla porta TCP 1433 e SQL Server Service Broker usa la porta TCP 4022.

### <a name="firewall-exception-for-sql-server-for-management-point"></a>Eccezione del firewall di SQL Server per il punto di gestione

*Si applica a: punto di gestione*

Windows Firewall è disattivato o è stata generata un'eccezione rilevante di Windows Firewall per SQL Server.

### <a name="iis-https-configuration"></a>Configurazione HTTPS di IIS

*Si applica a: punto di gestione, punto di distribuzione*

Binding del sito Web IIS per il protocollo di comunicazione HTTPS.

Quando si installano ruoli del sito che richiedono HTTPS, configurare i binding del sito IIS nel server specificato con un certificato di infrastruttura a chiave pubblica (PKI) valido.

### <a name="invalid-discovery-records"></a>Record di individuazione non validi

*Si applica a: sito di amministrazione centrale*

Sono presenti record di individuazione non più validi, che verranno contrassegnati per l'eliminazione.

### <a name="microsoft-xml-core-services-60-msxml60"></a>Microsoft XML Core Services 6.0 (MSXML60)

*Si applica a sito di amministrazione centrale, sito primario, sito secondario, console di Configuration Manager, punto di gestione, punto di distribuzione*

Verifica che sia installato MSXML 6.0 o versione successiva.

### <a name="network-access-protection-nap-is-no-longer-supported"></a>Lo strumento Protezione accesso alla rete non è più supportato

*Si applica a: sito primario*

Non sono presenti aggiornamenti software abilitati per Protezione accesso alla rete.

### <a name="ntfs-drive-on-site-server"></a>Unità NTFS nel server del sito

*Si applica a: sito primario*

L'unità disco deve essere formattata con il file system NTFS. Per una protezione migliore, installare i componenti del server del sito in unità disco formattate con il file system NTFS.

### <a name="pending-configuration-item-policy-updates"></a><a name="bkmk_pending-policy"></a> Aggiornamenti dei criteri per elementi di configurazione in sospeso

<!--SCCMDocs-pr issue 2814-->

*Si applica a: sito primario*

A partire dalla versione 1806, se si esegue l'aggiornamento dalla versione 1706 o successiva, potrebbe essere visualizzato questo avviso se sono presenti molte distribuzioni di applicazioni e almeno una di esse richiede l'approvazione.

Sono disponibili due opzioni:  

- Ignorare l'avviso e continuare l'aggiornamento. Questa azione comporta una maggiore elaborazione sul server del sito durante l'aggiornamento a causa dell'elaborazione dei criteri. È inoltre possibile osservare un aumento del carico del processore nel punto di gestione dopo l'aggiornamento.  

- Modificare una delle applicazioni che non prevedono requisiti o che ne prevedono uno per un sistema operativo specifico. Eseguire la pre-elaborazione di parte del carico nel server del sito in questa fase. Esaminare **objreplmgr.log** e quindi monitorare il processore nel punto di gestione. Dopo aver completato l'elaborazione, aggiornare il sito. Sarà ancora presente un certo livello di elaborazione aggiuntiva dopo l'aggiornamento, ma sarà inferiore a quella che si verifica ignorando l'avviso con la prima opzione.  

### <a name="pending-system-restart-on-the-remote-sql-server"></a>Riavvio del sistema in sospeso nell'istanza remota di SQL Server

*Si applica a: Versione 1902 e versioni successive, istanza remota di SQL Server*

Prima di eseguire l'installazione, un altro programma necessita del riavvio del server.

Per verificare se il computer è in uno stato di riavvio in sospeso, vengono controllate le posizioni del Registro di sistema seguenti:<!--SCCMDocs-pr issue 3377-->  

- `HKLM:Software\Microsoft\Windows\CurrentVersion\Component Based Servicing\RebootPending`  

- `HKLM:SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired`  

- `HKLM:SYSTEM\CurrentControlSet\Control\Session Manager, PendingFileRenameOperations`  

- `HKLM:Software\Microsoft\ServerManager, CurrentRebootAttempts`  

### <a name="powershell-20-on-site-server"></a>PowerShell 2.0 nel server di sito

*Si applica a: sito primario con Exchange Connector*

Windows PowerShell 2.0 o versione successiva è installato nel server del sito per Configuration Manager Exchange Connector.

### <a name="remote-connection-to-wmi-on-secondary-site"></a>Connessione remota a WMI nel sito secondario

*Si applica a: sito secondario*

Il programma di installazione può stabilire una connessione remota a WMI nel server del sito secondario.

### <a name="schema-extensions"></a>Estensioni dello schema

*Si applica a: sito di amministrazione centrale, sito primario*

Lo schema di Active Directory è stato esteso. Se è esteso, il controllo verifica la versione delle estensioni dello schema usate.

Configuration Manager non richiede le estensioni dello schema di Active Directory per l'installazione del server del sito. Microsoft le consiglia per l'uso completo di tutte le funzionalità di Configuration Manager. Per altre informazioni sui vantaggi offerti dall'estensione dello schema, vedere [Preparare Active Directory per la pubblicazione di siti](../../../plan-design/network/extend-the-active-directory-schema.md).

### <a name="share-name-in-package"></a>Nome della condivisione nel pacchetto

*Si applica a: sito di amministrazione centrale, sito primario*

I pacchetti non contengono caratteri non validi nel nome della condivisione, ad esempio `#`.

### <a name="site-system-to-sql-server-communication"></a>Comunicazione dal sistema del sito a SQL Server

*Si applica a: sito secondario, punto di gestione*

L'account configurato per eseguire il servizio SQL Server per l'istanza di database del sito ha un nome dell'entità servizio (SPN, service principal name) valido in Active Directory Domain Services. Registrare un SPN valido in Active Directory Domain Services per supportare l'autenticazione Kerberos.

### <a name="sql-server-change-tracking-cleanup"></a><a name="bkmk_changetracking"></a> Pulizia rilevamento modifiche di SQL

*Si applica a: server di database del sito*

A partire dalla versione 1810, è possibile controllare se il database del sito ha un backlog di dati di rilevamento modifiche di SQL.<!--SCCMDocs-pr issue 3023-->  

Eseguire manualmente il controllo tramite una stored procedure nel database del sito. Creare prima di tutto una [connessione di diagnostica](/sql/database-engine/configure-windows/diagnostic-connection-for-database-administrators?view=sql-server-2017) al database del sito. Il metodo più semplice è usare l'editor di query del motore di database di SQL Server Management Studio e connettersi a `admin:<instance name>`.

In una finestra di query di connessione amministrativa dedicata, eseguire i comandi seguenti:

```SQL
USE <ConfigMgr database name>
EXEC spDiagChangeTracking
```

A seconda delle dimensioni del database e del backlog, l'esecuzione della stored procedure può richiedere alcuni minuti o diverse ore. Al termine della query, vengono visualizzate due sezioni di dati correlati al backlog. Esaminare per prima cosa **CT_Days_Old**. Questo valore indica il numero di giorni trascorsi da quando è stata immessa la prima voce nella tabella syscommittab. Dovrebbe essere pari a cinque giorni, il valore predefinito di Configuration Manager. Non modificare questo valore predefinito. In caso di elaborazione dati o repliche di dimensioni molto elevate, la prima voce nella tabella syscommittab potrebbe essere stata immessa più di cinque giorni prima. Se il valore supera i sette giorni, eseguire una pulizia manuale dei dati di rilevamento delle modifiche.  

Per eseguire la pulizia dei dati di rilevamento delle modifiche, eseguire il comando seguente nella connessione amministrativa dedicata:

```SQL
USE <ConfigMgr database name>
EXEC spDiagChangeTracking @CleanupChangeTracking = 1
```

Questo comando avvia una pulizia di syscommittab e di tutte le tabelle laterali associate. L'esecuzione del comando può richiedere da alcuni minuti a diverse ore. Per monitorarne l'avanzamento, eseguire una query sulla vista **vLogs**. Per visualizzare lo stato di avanzamento corrente, eseguire la query seguente:

```SQL
SELECT * FROM vLogs WHERE ProcedureName = 'spDiagChangeTracking'
```

### <a name="sql-server-native-client"></a>SQL Server Native Client

<!--SCCMDocs-pr issue 3094-->

Quando si installa un nuovo sito, Configuration Manager installa automaticamente SQL Server Native Client come componente ridistribuibile. Dopo l'installazione del sito, Configuration Manager non aggiorna SQL Server Native Client. L'aggiornamento di SQL Server Native Client potrebbe richiedere un riavvio, che può rallentare il processo di installazione del sito.

Questo controllo garantisce che il server del sito abbia una versione supportata di SQL Native Client. Il controllo dei prerequisiti non verifica la versione di SQL Native Client nei sistemi del sito remoti.

La versione minima è SQL 2012 SP4 (`11.*.7001.0`). Questa versione di SQL Native Client supporta TLS 1.2. Per altre informazioni, vedere gli articoli seguenti:

- [Supporto di TLS 1.2 per Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)  

- [Come abilitare TLS 1.2 per Configuration Manager](../../../plan-design/security/enable-tls-1-2.md)  

Configuration Manager usa SQL Server Native Client nei seguenti ruoli del sistema del sito:<!-- SCCMDocs issue 1150 -->

- Server di database del sito
- Server del sito: sito di amministrazione centrale, sito primario o sito secondario
- Punto di gestione
- Punto di gestione dei dispositivi
- Punto di migrazione stato
- Provider SMS
- Punto di aggiornamento software
- Punto di distribuzione abilitato per multicast
- Punto di servizio aggiornamento AI
- Punto di Reporting Services
- Servizio Web del Catalogo applicazioni
- Punto di registrazione
- Punto di Endpoint Protection
- punto di connessione del servizio
- Punto di registrazione certificati
- Punto di servizio del data warehouse

### <a name="sql-server-process-memory-allocation"></a>Allocazione di memoria per il processo di SQL Server

*Si applica a: server di database del sito*

SQL Server riserva almeno 8 GB di memoria per il sito di amministrazione centrale e per il sito primario e almeno 4 GB di memoria per il sito secondario.

Per altre informazioni, vedere [Come configurare le opzioni di memoria tramite SQL Server Management Studio](/sql/database-engine/configure-windows/server-memory-server-configuration-options#how-to-configure-memory-options-using-).

> [!NOTE]  
> Questo controllo non è applicabile a SQL Server Express in un sito secondario. In questa edizione la memoria riservata è limitata a 1 GB.  

### <a name="sql-server-security-mode"></a>Modalità di sicurezza di SQL Server

*Si applica a: server di database del sito*

SQL Server è configurato per la sicurezza di autenticazione di Windows.

### <a name="unsupported-site-system-os-version-for-upgrade"></a>Versione del sistema operativo non supportata per l'aggiornamento

*Si applica a: sito primario, sito secondario*

Ruoli del sistema del sito diversi dai punti di distribuzione sono installati nei server che eseguono Windows Server 2012 o versione successiva.

Per altre informazioni, vedere [Sistemi operativi supportati per i server dei sistemi del sito di Configuration Manager](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md).

> [!NOTE]  
> Questo controllo non può risolvere lo stato dei ruoli del sistema del sito installati in Azure o per l'archiviazione nel cloud usata da Microsoft Intune. Ignorare gli avvisi per questi ruoli come falsi positivi.

### <a name="upgrade-assessment-toolkit-is-unsupported"></a>Il toolkit di valutazione dell'aggiornamento non è supportato

*Si applica a: sito di amministrazione centrale, sito primario*

Il toolkit di valutazione dell'aggiornamento non è installato. Per altre informazioni, vedere [Funzionalità rimosse e deprecate](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).

### <a name="verify-site-server-permissions-to-publish-to-active-directory"></a>Verificare le autorizzazioni del server del sito da pubblicare in Active Directory Domain Services

*Si applica a: sito di amministrazione centrale, sito primario, sito secondario*

L'account computer per il server del sito dispone di autorizzazioni di tipo **Controllo completo** per il contenitore **System Management** nel dominio di Active Directory.

Per altre informazioni, vedere [Preparare Active Directory per la pubblicazione di siti](../../../plan-design/network/extend-the-active-directory-schema.md).

> [!NOTE]  
> È possibile ignorare questo avviso se si verificano manualmente le autorizzazioni.

### <a name="windows-remote-management-winrm-v11"></a>Gestione remota Windows (WinRM) v1.1

*Si applica a: sito primario, console di Configuration Manager*

WinRM 1.1 è installato nel server del sito primario o nel computer della console di Configuration Manager per l'esecuzione della console di gestione fuori banda.

WinRM viene installato automaticamente con tutte le versioni di Windows attualmente supportate. Per altre informazioni, vedere [Installazione e configurazione di Gestione remota Windows](/windows/win32/winrm/installation-and-configuration-for-windows-remote-management).

### <a name="wsus-on-site-server"></a>WSUS nel server di sito

*Si applica a: sito di amministrazione centrale, sito primario*

Una versione supportata di Windows Server Update Services (WSUS) è installata nel server del sito.

Quando si usa un punto di aggiornamento software in un server diverso rispetto al server del sito, è necessario installare la console di amministrazione WSUS nel server del sito. Per altre informazioni su WSUS, vedere [Windows Server Update Services](/windows-server/administration/windows-server-update-services/get-started/windows-server-update-services-wsus).