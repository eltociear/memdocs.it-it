---
title: Configurare siti e gerarchie
titleSuffix: Configuration Manager
description: Consultare questo elenco di controllo per verificare di aver tenuto in considerazione le configurazioni più comuni che interessano sia i siti che le gerarchie.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9efb4061-f642-48bd-8332-3357ff5b3118
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e996c31a4f1aaa9224e4c6d1d435f79adf7ac23c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704679"
---
# <a name="configure-sites-and-hierarchies-for-configuration-manager"></a>Configurare siti e gerarchie per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Dopo aver installato il primo sito di Configuration Manager o avere aggiunto altri siti alla gerarchia, usare questo elenco di controllo per verificare di avere tenuto in considerazione le configurazioni più comuni che interessano sia i siti che le gerarchie.  

Le note di configurazione seguenti sono valide per la maggior parte delle distribuzioni:  

- Alcune opzioni si basano su altre, ad esempio Individuazione foresta Active Directory, i limiti e i gruppi di limiti.  

- Diverse configurazioni presentano valori predefiniti utilizzabili usare senza apportare modifiche alla configurazione, almeno inizialmente.  

- Altre, come i gruppi di limiti e i gruppi di punti di distribuzione, devono essere configurate prima di poterle usare.  

| Action | Dettagli |  
|------------|-------------|  
| Configurare l'amministrazione basata su ruoli | Separare le assegnazioni amministrative per controllare quali utenti amministratori possono visualizzare e gestire i diversi oggetti e dati nell'ambiente di Configuration Manager.<br /><br /> Le configurazioni per l'amministrazione basata su ruoli sono condivise con tutti i siti in una gerarchia.   <br/><br/>Per altre informazioni, vedere [Configurare un'amministrazione basata su ruoli](configure-role-based-administration.md). |  
| Pubblicare i dati del sito in Active Directory Domain Services | Facilitare ai client l'individuazione dei servizi e l'uso efficiente delle risorse del sito.<br /><br /> In primo luogo, [estendere lo schema di Active Directory](../../../plan-design/network/extend-the-active-directory-schema.md). Configurare quindi singolarmente ogni sito per [pubblicare i dati del sito](publish-site-data.md). |  
| Configurare un punto di connessione del servizio | Pianificare l'installazione e la configurazione di un punto di connessione del servizio nel sito di primo livello della gerarchia. Per altre informazioni, vedere [Informazioni sul punto di connessione del servizio](about-the-service-connection-point.md). |  
| Aggiungere ruoli del sistema del sito | Installare uno o più ruoli aggiuntivi del sistema del sito per singoli siti. Per altre informazioni, vedere [Aggiungere ruoli del sistema del sito](add-site-system-roles.md). |  
| Configurare i limiti e i gruppi di limiti del sito | Specificare i limiti che definiscono i percorsi di rete nella intranet in cui possono essere presenti i dispositivi da gestire. Configurare quindi gruppi di limiti in modo che i client in tali percorsi di rete possano trovare le risorse di Configuration Manager. Per altre informazioni, vedere [Definire i limiti del sito e i gruppi di limiti](define-site-boundaries-and-boundary-groups.md). |  
| Configurare gruppi di punti di distribuzione | Configurare gruppi logici di punti di distribuzione per semplificare la gestione delle distribuzioni. Per altre informazioni, vedere [Gestire i gruppi di punti di distribuzione](install-and-configure-distribution-points.md#bkmk_manage). |  
| Eseguire l'individuazione | Eseguire l'individuazione per trovare le risorse sulla rete, tra cui l'infrastruttura, i dispositivi e gli utenti della rete.<br /><br /> Per altre informazioni, vedere [Eseguire l'individuazione](run-discovery.md). |  
| Aggiungere ridondanza e capacità per gli amministratori | Installare altri provider SMS e console di Configuration Manager per offrire agli amministratori capacità aggiuntive per la gestione dell'infrastruttura:<br /><br /> **Installare altri provider SMS** per fornire la ridondanza per la console e le connessioni API al sito. Per altre informazioni, vedere [Gestire il provider SMS](../../manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider).<br /><br /> **Installare altre console di Configuration Manager** per fornire l'accesso ad altri utenti amministratori. Per altre informazioni, vedere [Installare la console di System Center Configuration Manager](../install/install-consoles.md). |  
| Configurare i componenti del sito | Configurare i componenti del sito per modificare il comportamento dei ruoli del sistema del sito e la creazione di report sullo stato del sito. Per altre informazioni, vedere [Componenti del sito](site-components.md). |  
| Creare raccolte personalizzate | Usando le informazioni su dispositivi e utenti individuate dal sito, creare raccolte personalizzate di oggetti per semplificare le future attività di gestione. Per altre informazioni, vedere [Come creare le raccolte](../../../clients/manage/collections/create-collections.md). |  
| Configurare le impostazioni per gestire le distribuzioni ad alto rischio | Configurare le impostazioni in un sito in modo da avvisare gli amministratori quando creano una distribuzione ad alto rischio. Per altre informazioni, vedere [Impostazioni per gestire distribuzioni ad alto rischio](../../manage/settings-to-manage-high-risk-deployments.md). |  
| Configurare le repliche di database per i punti di gestione | Configurare una replica di database per ridurre il carico del processore determinato nel server di database del sito dai punti di gestione quando questi elaborano le richieste provenienti dai client. Per altre informazioni, vedere [Repliche di database per i punti di gestione](database-replicas-for-management-points.md). |  
| Configurare un gruppo di disponibilità Always On di SQL Server | Configurare i gruppi di disponibilità come soluzione a disponibilità elevata e ripristino di emergenza per ospitare il database del sito nei siti primari e nel sito di amministrazione centrale. Per altre informazioni, vedere [Preparare l'uso di gruppi di disponibilità Always On di SQL Server](sql-server-alwayson-for-a-highly-available-site-database.md). |  
| Modificare la replica tra siti | Vedere [Trasferimenti di dati tra siti](../../../plan-design/hierarchy/data-transfers-between-sites.md) per informazioni sugli argomenti seguenti:<br /><br /> Configurare la [replica basata su file](../../../plan-design/hierarchy/file-based-replication.md) tra siti secondari<br /><br /> Configurare [collegamenti di replica di database](../../../plan-design/hierarchy/database-replication.md)<br /><br /> Configurare [viste distribuite](../../../plan-design/hierarchy/database-replication.md#bkmk_distviews) |  
| Configurare i server del sito in modalità passiva | A partire dalla versione 1806, configurare un server del sito in modalità passiva per ogni sito primario e per il sito di amministrazione centrale. Questa funzionalità offre un server del sito a disponibilità elevata. Per altre informazioni, vedere [Disponibilità elevata del server del sito](site-server-high-availability.md). |  
