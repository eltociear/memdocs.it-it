---
title: Monitorare la gerarchia
titleSuffix: Configuration Manager
description: Informazioni su come monitorare l'infrastruttura in Configuration Manager usando l'area di lavoro Monitoraggio della console.
ms.date: 06/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 007dbb73-18a7-48a3-a489-97cf9fc4f140
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 504943df58c0471a0ef821a269cc22b2d12d76d8
ms.sourcegitcommit: 42882de75c8a984ba35951b1165c424a7e0ba42e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2020
ms.locfileid: "89068039"
---
# <a name="monitor-the-hierarchy"></a>Monitorare la gerarchia

*Si applica a: Configuration Manager (Current Branch)*

Per monitorare la gerarchia in Configuration Manager, usare l'area di lavoro **Monitoraggio** della console di Configuration Manager.  

> [!NOTE]  
> La migrazione dei siti costituisce un'eccezione. Questo processo viene monitorato nel nodo **Migrazione** dell'area di lavoro **Amministrazione**. Per altre informazioni, vedere [Operazioni per la migrazione a Configuration Manager Current Branch](../../migration/operations-for-migration.md).  

Per il monitoraggio, oltre alla console di Configuration Manager, usare le funzionalità seguenti:

- [Introduzione alla creazione di report](introduction-to-reporting.md)
- [File di log](../../plan-design/hierarchy/log-files.md).  

Quando si effettua il monitoraggio di siti, cercare dei segnali che indichino problemi che richiedono un intervento. Ad esempio:  

- Un backlog di file sui server del sito e sui sistemi del sito.  

- Messaggi di stato che indicano un errore o un problema.  

- Errori di comunicazione all'interno del sito.  

- Messaggi di errore e di avviso nel registro eventi di sistema sui server.  

- Messaggi di errore e di avviso nel registro degli errori di Microsoft SQL Server.  

- Siti o client che non segnalano lo stato da molto tempo.  

- Risposta lenta da parte del database di SQL Server.  

- Segnali di errore hardware.  

Se le attività di monitoraggio danno segni di problemi, analizzare l'origine dell'eventuale problema, quindi risolverlo rapidamente per ridurre al minimo il rischio di un errore del sito.  


## <a name="monitor-common-management-tasks"></a><a name="BKMK_MonintorMgmtTasks"></a> Monitorare le comuni attività di gestione

Configuration Manager include una funzionalità di monitoraggio predefinita all'interno della console.

### <a name="alerts"></a>Avvisi

Per altre informazioni, vedere [Avvisi di monitoraggio](use-alerts-and-the-status-system.md#BKMK_MonitorAlerts).  

### <a name="compliance-settings"></a>Impostazioni di conformità

Per altre informazioni, vedere [Come monitorare le impostazioni di conformità](../../../compliance/deploy-use/monitor-compliance-settings.md).

### <a name="content"></a>Content

Per informazioni generali sul monitoraggio del contenuto, vedere [Gestire il contenuto e l'infrastruttura del contenuto](../deploy/configure/manage-content-and-content-infrastructure.md).  

Per altre informazioni sul monitoraggio di tipi specifici di contenuto:

- [Monitorare le applicazioni](../../../apps/deploy-use/monitor-applications-from-the-console.md)

- [Monitorare pacchetti e programmi](../../../apps/deploy-use/packages-and-programs.md#monitor-packages-and-programs)  

- [Monitorare il contenuto per gli aggiornamenti software](../../../sum/deploy-use/monitor-software-updates.md#BKMK_MonitorContent)

- [Monitorare il contenuto per le distribuzioni del sistema operativo](../../../osd/deploy-use/monitor-operating-system-deployments.md#BKMK_MonitorContent)

### <a name="endpoint-protection"></a>Endpoint Protection

Per altre informazioni, vedere [Come monitorare Endpoint Protection](../../../protect/deploy-use/monitor-endpoint-protection.md).  

### <a name="os-deployment"></a>Distribuzione del sistema operativo

Per altre informazioni, vedere [Monitorare le distribuzioni del sistema operativo](../../../osd/deploy-use/monitor-operating-system-deployments.md).

### <a name="monitor-power-management"></a>Monitorare il risparmio energia

Per altre informazioni, vedere [How to monitor and plan for power management](../../clients/manage/power/monitor-and-plan-for-power-management.md) (Come monitorare e pianificare il risparmio energia ).  

### <a name="monitor-software-metering"></a>Monitorare il controllo del software

Per altre informazioni, vedere [Monitorare l'utilizzo delle app con la misurazione del software](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

### <a name="monitor-software-updates"></a>Monitorare gli aggiornamenti software

Per altre informazioni, vedere [Monitorare gli aggiornamenti software](../../../sum/deploy-use/monitor-software-updates.md).  


## <a name="monitor-the-site-hierarchy"></a><a name="BKMK_SH_Node"></a> Monitorare la gerarchia di siti

Il nodo **Gerarchia siti** dell'area di lavoro **Monitoraggio** offre una panoramica della gerarchia e dei collegamenti tra siti di Configuration Manager. 

Usare il nodo **Gerarchia siti** per monitorare l'integrità di ogni sito. Monitorare anche i collegamenti di replica tra siti e la loro relazione con fattori esterni, come la posizione geografica.  

Sia lo stato del sito che lo stato del collegamento tra siti vengono replicati come dati del sito e non come dati globali. Quando si collega la console di Configuration Manager a un sito primario figlio, non è possibile visualizzare lo stato del sito o del collegamento per gli altri siti primari o i relativi siti secondari figlio. Ad esempio, in una gerarchia con più siti primari, quando si connette la console a un sito primario, è possibile visualizzare lo stato dei siti secondari figlio, del sito primario e del sito di amministrazione centrale. Da questa vista non è possibile visualizzare lo stato di altri siti al di sotto del sito di amministrazione centrale.  

Per controllare la visualizzazione nel nodo **Gerarchia siti**, usare l'azione **Configura impostazioni**. La gerarchia replica le impostazioni configurate in questo nodo.  

### <a name="hierarchy-diagram"></a>Diagramma gerarchia

Il diagramma gerarchia visualizza i siti in una mappa topologica. Selezionare un sito e visualizzare un riepilogo dei messaggi di stato da tale sito. Eseguire il drill-through per visualizzare i messaggi di stato e accedere alle **proprietà** del sito.  

Per visualizzare lo stato di alto livello per un sito o un collegamento di replica tra siti, posizionare il puntatore del mouse sull'oggetto. Lo stato del collegamento di replica non viene replicato a livello globale. Per visualizzare i dettagli del collegamento di replica tra tutti i siti primari in una gerarchia, connettere la console di al sito di amministrazione centrale.  

Le seguenti opzioni di modificano il diagramma gerarchia:  

#### <a name="groups"></a>Gruppi

Configurare il numero di siti primari e secondari che attivano una modifica nel diagramma gerarchia. Questa modifica nella visualizzazione combina i siti in un unico oggetto, quindi si visualizza il numero totale di siti e un rollup di alto livello di messaggi di stato e stato dei siti.

#### <a name="favorite-sites"></a>Siti preferiti

Specificare i singoli siti come sito preferito. Un'icona a stella identifica un sito preferito nel diagramma gerarchia. I siti preferiti non sono combinati con altri siti quando si usano i gruppi. Vengono sempre visualizzati singolarmente.  

### <a name="geographical-view"></a>Vista geografica

> [!IMPORTANT]
> A partire dall'agosto 2020, questa funzionalità è deprecata. Usare l'opzione **Diagramma gerarchia**.<!--8116777-->

la vista geografica visualizza la posizione di ogni sito su una mappa geografica. Visualizza solo i siti che è possibile configurare con una posizione. Quando si seleziona un sito in questa vista, vengono visualizzati i collegamenti di replica a siti padre o figlio. A differenza della vista Diagramma gerarchia, in questa vista non è possibile visualizzare i dettagli del messaggio di stato del sito o del collegamento di replica.  

> [!NOTE]  
> Per utilizzare la vista geografica, sul computer a cui si collega la console di Configuration Manager deve essere installato Internet Explorer e deve essere possibile l'accesso a Bing Maps tramite il protocollo HTTP.  

L'opzione seguente modifica la vista geografica:  

#### <a name="site-location"></a>Percorso sito

Specificare una località geografica per ogni sito usando uno dei tipi seguenti:

- Via e numero civico
- Nome del luogo, ad esempio il nome di una città
- Coordinate di latitudine e longitudine

Ad esempio, per usare la latitudine e la longitudine di Redmond, Washington, specificare **N 47 40 26.3572 W 122 7 17.4432** come posizione del sito. Non è necessario specificare i simboli per i gradi, minuti o secondi della latitudine o longitudine. Configuration Manager usa Bing Maps per visualizzare la posizione nella vista geografica. Sarà quindi possibile visualizzare la gerarchia con le località geografiche. Questa vista fornisce informazioni dettagliate sui problemi a livello di area che potrebbero influire su siti specifici o sulla replica tra siti.  

Quando si specifica una posizione, è possibile utilizzare la casella **Percorso** per effettuare la ricerca di un sito specifico nella gerarchia. Una volta selezionato il sito, immettere la posizione come il nome di una città o un indirizzo nella colonna **Percorso** . Configuration Manager usa Bing Maps per risolvere il percorso.  

<a name="BKMK_MonitorRepLinksAndStatuss"></a>

## <a name="next-steps"></a>Passaggi successivi

[Monitorare la replica di database](monitor-replication.md)
