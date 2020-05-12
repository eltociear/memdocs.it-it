---
title: Monitorare le distribuzioni del sistema operativo
titleSuffix: Configuration Manager
description: Per monitorare gli oggetti di distribuzione del sistema operativo, la console di Configuration Manager offre avvisi, report e diversi indicatori di stato.
ms.date: 05/04/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 08085d94-295c-432f-b5e3-9736bce0193b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7afab9fbbb443b2f9fb4af15a3805c0b7df7a014
ms.sourcegitcommit: 14d7dd0a99ebd526c9274d5781c298c828323ebf
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82802167"
---
# <a name="monitor-operating-system-deployments-in-configuration-manager"></a>Monitorare le distribuzioni del sistema operativo in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Per monitorare gli oggetti di distribuzione del sistema operativo, la console di Configuration Manager offre i metodi descritti di seguito.  


##  <a name="alerts-for-operating-system-deployments"></a><a name="BKMK_OSDAlerts"></a> Avvisi per le distribuzioni del sistema operativo  
 È possibile configurare un avviso nelle impostazioni di distribuzione della sequenza di attività per inviare notifiche agli utenti amministratori quando i livelli di conformità per la distribuzione sono inferiori alla percentuale configurata.  

 Dopo aver configurato le impostazioni degli avvisi, Configuration Manager genera un avviso se si verificano le condizioni specificate. È possibile esaminare gli avvisi di distribuzione della sequenza di attività nei percorsi seguenti:  

1.  Gli avvisi recenti si trovano nel nodo **Sistemi operativi** dell'area di lavoro **Raccolta software** .  

2.  Gli avvisi configurati possono essere gestiti nel nodo **Avvisi** dell'area di lavoro **Monitoraggio** .  

##  <a name="task-sequence-deployment-status"></a><a name="BKMK_TSDeployStatus"></a> Stato di distribuzione della sequenza di attività  
 Dopo aver distribuito una sequenza di attività, è possibile monitorare lo stato di distribuzione. Usare la procedura seguente per monitorare lo stato della distribuzione per una sequenza di attività.  

#### <a name="to-monitor-deployment-status"></a>Per monitorare lo stato di distribuzione  

1.  Nella console di Configuration Manager fare clic su **Monitoraggio**.  

2.  Nell'area di lavoro Monitoraggio fare clic su **Distribuzioni**.  

3.  Fare clic sulla sequenza di attività per cui si vuole monitorare lo stato di distribuzione.  

4.  Nella scheda **Home** fare clic su **Visualizza stato** nel gruppo **Distribuzione**.  

> [!NOTE]  
> Quando si avvia un aggiornamento viene generato il messaggio di stato 52200. Il messaggio specifica l'utente che ha eseguito l'aggiornamento.  

##  <a name="operating-system-deployment-reports"></a><a name="BKMK_TSReports"></a> Report sulla distribuzione del sistema operativo  
 Sono disponibili numerosi report di distribuzione del sistema operativo predefiniti. Sono organizzati in diverse categorie e possono essere usati per fornire informazioni specifiche sullo stato della migrazione e sulle distribuzioni di sequenze di attività. Oltre a usare i report preconfigurati, è anche possibile creare report degli aggiornamenti software personalizzati in base alle esigenze dell'azienda. Per altre informazioni, vedere [Operazioni e manutenzione per la creazione di report](../../core/servers/manage/operations-and-maintenance-for-reporting.md).  

##  <a name="monitor-content"></a><a name="BKMK_MonitorContent"></a> Monitoraggio del contenuto  
 È possibile monitorare il contenuto nella console di Configuration Manager per verificare lo stato di tutti i tipi di pacchetti in relazione ai punti di distribuzione associati. Sono inclusi lo stato di convalida del contenuto del pacchetto, lo stato del contenuto assegnato a un gruppo di punti di distribuzione specifico, lo stato del contenuto assegnato a un punto di distribuzione e lo stato di funzionalità facoltative per ogni punto di distribuzione (convalida contenuto, PXE e multicast).  

###  <a name="content-status-monitoring"></a><a name="BKMK_ContentStatus"></a> Monitoraggio dello stato del contenuto  
 Il nodo **Stato componente** dell'area di lavoro **Monitoraggio** fornisce informazioni sui pacchetti contenuto. È possibile esaminare le informazioni generali sul pacchetto, lo stato di distribuzione del pacchetto e informazioni dettagliate sullo stato del pacchetto. Usare la procedura seguente per visualizzare lo stato del contenuto.  

#### <a name="to-monitor-content-status"></a>Per monitorare lo stato del contenuto  

1.  Nella console di Configuration Manager fare clic su **Monitoraggio**.  

2.  Nell'area di lavoro Monitoraggio, espandere **Stato distribuzione**, quindi fare clic su **Stato contenuto**. Vengono visualizzati i pacchetti.  

3.  Selezionare il pacchetto di cui visualizzare informazioni dettagliate sullo stato.  

4.  Nella scheda **Home** fare clic su **Visualizza stato**. Vengono visualizzate informazioni dettagliate sullo stato per il pacchetto.  

###  <a name="distribution-point-group-status"></a><a name="BKMK_DPGroupStatus"></a> Stato del gruppo di punti di distribuzione  
 Il nodo **Stato gruppo di punti di distribuzione** nell'area di lavoro **Monitoraggio** fornisce informazioni sui gruppi di punti di distribuzione. È possibile esaminare informazioni generali sul gruppo di punti di distribuzione, quali lo stato, il grado di conformità e le informazioni dettagliate sullo stato. Usare la procedura seguente per visualizzare lo stato del gruppo di punti di distribuzione.  

#### <a name="to-monitor-distribution-point-group-status"></a>Per monitorare lo stato del gruppo di punti di distribuzione  

1.  Nella console di Configuration Manager fare clic su **Monitoraggio**.  

2.  Nell'area di lavoro Monitoraggio, espandere **Stato distribuzione**, quindi fare clic su **Stato gruppo di punti di distribuzione**. Vengono visualizzati i gruppi di punti di distribuzione.  

3.  Selezionare il gruppo di punti di distribuzione di cui visualizzare informazioni dettagliate sullo stato.  

4.  Nella scheda **Home** fare clic su **Visualizza stato**. Vengono visualizzate le informazioni dettagliate sullo stato per il gruppo di punti di distribuzione.  

###  <a name="distribution-point-configuration-status"></a><a name="BKMK_DPConfigStatus"></a> Stato di configurazione dei punti di distribuzione  
 Il nodo **Stato di configurazione dei punti di distribuzione** nell'area di lavoro **Monitoraggio** fornisce informazioni sul punto di distribuzione. È possibile esaminare gli attributi abilitati per il punto di distribuzione, come PXE, Multicast e convalida del contenuto. È inoltre possibile visualizzare informazioni dettagliate sullo stato per il punto di distribuzione. Usare la procedura seguente per visualizzare lo stato di configurazione del punto di distribuzione.  

#### <a name="to-monitor-distribution-point-configuration-status"></a>Per monitorare lo stato di configurazione del punto di distribuzione  

1.  Nella console di Configuration Manager fare clic su **Monitoraggio**.  

2.  Nell'area di lavoro Monitoraggio, espandere **Stato distribuzione**, quindi fare clic su **Stato di configurazione dei punti di distribuzione**. Vengono visualizzati i punti di distribuzione.  

3.  Selezionare il punto di distribuzione per il quale si desidera visualizzare le informazioni sullo stato.  

4.  Nel riquadro dei risultati fare clic sulla scheda **Dettagli** . Verranno visualizzate le informazioni sullo stato per il punto di distribuzione.  
