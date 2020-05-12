---
title: Cluster di SQL Server
titleSuffix: Configuration Manager
description: Usare un cluster di SQL Server per ospitare il database del sito di Configuration Manager
ms.date: 04/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d09a82c6-bbd1-49ca-8ffe-e3ce87b85d33
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d035e6fbd776a03ce38a4cd0fc12755100b60c91
ms.sourcegitcommit: 2aa97d1b6409575d731c706faa2bc093c2b298c4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82643239"
---
# <a name="use-a-sql-server-cluster-for-the-site-database"></a>Usare un cluster di SQL Server per il database del sito

*Si applica a: Configuration Manager (Current Branch)*

È possibile usare un cluster di failover di SQL Server per ospitare il database del sito di Configuration Manager. Un cluster offre il supporto per il failover e migliora l'affidabilità del database del sito. Non offre tuttavia vantaggi aggiuntivi di elaborazione o bilanciamento del carico. Un cluster di failover di SQL Server, inoltre, usa l'archiviazione condivisa e introduce un singolo punto di guasto. Può verificarsi una riduzione delle prestazioni perché il server del sito deve trovare il nodo attivo del cluster di SQL Server prima di connettersi al database del sito.  

> [!IMPORTANT]  
> La configurazione corretta dei cluster di SQL Server si basa sulla documentazione e le procedure incluse nella libreria della documentazione di SQL Server.  


Prima di installare Configuration Manager, preparare il cluster di SQL Server per il supporto di Configuration Manager. Per altre informazioni, vedere [Preparare un'istanza di SQL Server in cluster](#bkmk_prepare).

Durante l'installazione di Configuration Manager il writer del Servizio Copia Shadow del volume (VSS) viene installato su ogni nodo dei computer fisici del cluster di Microsoft Windows Server. Questo servizio supporta l'attività di manutenzione **Backup server sito**.  

Dopo aver installato il sito, Configuration Manager controlla le modifiche al nodo del cluster ogni ora. Configuration Manager gestisce automaticamente le modifiche rilevate che interessano le installazioni dei componenti. Ad esempio, il failover di un nodo o l'aggiunta di un nuovo nodo al cluster di SQL Server.  



## <a name="supported-options"></a>Opzioni supportate

Le opzioni seguenti sono supportate per i cluster di failover di SQL Server usati come database del sito:

- Cluster a istanza singola  

- Configurazioni di più istanze  

- Più nodi attivi  

- Istanza predefinita o denominata  



## <a name="prerequisites"></a>Prerequisiti

Tenere presente i prerequisiti seguenti:  

- Il database del sito deve essere lontano dal server del sito. Il cluster non può includere il server di sistema del sito.  

    > [!Note]  
    > A partire dalla versione 1810, il programma di installazione di Configuration Manager non blocca più l'installazione del ruolo del server del sito in un computer con il ruolo Windows per il clustering di failover. In precedenza non era possibile inserire il database del sito nel server del sito. Con questa modifica, è possibile creare un sito a disponibilità elevata con un minor numero di server usando un cluster di SQL Server e un server del sito in modalità passiva. Per altre informazioni, vedere [Opzioni di disponibilità elevata](high-availability-options.md). <!--3607761, fka 1359132-->  

- Aggiungere l'account computer del server del sito al gruppo **Administrators** locale di ogni server nel cluster.  

- Per supportare l'autenticazione Kerberos, abilitare il protocollo di comunicazione di rete **TCP/IP** per la connessione di rete di ogni nodo del cluster di SQL Server. Il protocollo **Named pipe** non è obbligatorio, ma può essere usato per risolvere i problemi relativi all'autenticazione Kerberos. Le impostazioni del protocollo di rete vengono configurate in **Gestione configurazione SQL Server** di **Configurazione di rete SQL Server**.  

- Quando si usa un cluster di SQL Server per il database del sito, ci sono requisiti dei certificati specifici. Per altre informazioni, vedere gli articoli seguenti:
  - [Installare un certificato in una configurazione del cluster di failover di SQL](https://docs.microsoft.com/sql/database-engine/configure-windows/manage-certificates?view=sql-server-ver15#provision-failover-cluster-cert)
  - [Requisiti dei certificati PKI per Configuration Manager](../../../plan-design/network/pki-certificate-requirements.md#BKMK_PKIcertificates_for_servers)

  > [!NOTE]
  > Se non si esegue il pre-provisioning di un certificato in SQL, Configuration Manager crea ed esegue il provisioning di un certificato autofirmato per SQL.<!-- 7099499 -->

## <a name="limitations"></a>Limitazioni

Tenere presente le limitazioni seguenti:  


### <a name="installation-and-configuration"></a>Installazione e configurazione

- I siti secondari non possono usare un cluster di SQL Server.  

- Quando si specifica un cluster di SQL Server, l'opzione per specificare percorsi file non predefiniti per il database del sito non è disponibile.  


### <a name="sms-provider"></a>Provider SMS

Non è possibile installare un'istanza del provider SMS in un cluster di SQL Server. Questa opzione non è supportata nemmeno in un computer che esegue un nodo di SQL Server in cluster.  


### <a name="data-replication-options"></a>Opzioni di replica dei dati

Se si usano **viste distribuite**, non è possibile usare un cluster di SQL Server per ospitare il database del sito.  


### <a name="backup-and-recovery"></a>Backup e ripristino

Configuration Manager non supporta il backup di Data Protection Manager (DPM) per un cluster di SQL Server che usa un'istanza denominata. Supporta tuttavia il backup di DPM in un cluster di SQL Server che usa l'istanza predefinita di SQL Server.  



## <a name="prepare-a-clustered-sql-server-instance"></a><a name="bkmk_prepare"></a> Preparare un'istanza di SQL Server in cluster  

Ecco le attività principali da completare per preparare il database del sito:

- Creare il cluster di SQL Server virtuale per ospitare il database del sito in un ambiente cluster di Windows Server esistente. Per passaggi dettagliati sull'installazione e configurazione di un cluster di SQL Server, vedere la documentazione specifica della versione di SQL Server in uso. Per altre informazioni, vedere [Creare un nuovo cluster di failover di SQL Server](https://docs.microsoft.com/sql/sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup?view=sql-server-2017).  

- In ogni computer nel cluster di SQL Server inserire un file nella cartella radice di ogni unità in cui non si vuole che Configuration Manager installi i componenti del sito. Assegnare al file il nome `NO_SMS_ON_DRIVE.SMS`. Per impostazione predefinita, Configuration Manager installa alcuni componenti in ogni nodo fisico per supportare alcune operazioni, ad esempio il backup.  

- Aggiungere l'account computer del server del sito al gruppo **Administrators** locale di ogni computer del nodo del cluster di Windows Server.  

- Nell'istanza di SQL Server virtuale assegnare il ruolo **sysadmin** di SQL Server all'account utente che esegue l'installazione di Configuration Manager.  


### <a name="to-install-a-new-site-using-a-clustered-sql-server"></a>Per installare un nuovo sito usando un'istanza cluster di SQL Server  

Per installare un sito che usa un database del sito in cluster, eseguire il programma di installazione di Configuration Manager seguendo la normale procedura per l'installazione di un sito con la modifica seguente:  

- Nella pagina **Informazioni database** specificare il nome dell'istanza virtuale del cluster di SQL Server che ospita il database del sito. L'istanza virtuale sostituisce il nome del computer che esegue SQL Server.  

    > [!IMPORTANT]  
    > Quando si immette il nome dell'istanza del cluster di SQL Server virtuale, non immettere il nome di Windows Server virtuale creato dal cluster di Windows Server. Se si usa il nome virtuale di Windows Server, il database del sito viene installato nel disco rigido locale del nodo del cluster di Windows Server attivo. In questo modo, si impedisce il failover se il nodo non riesce.  
