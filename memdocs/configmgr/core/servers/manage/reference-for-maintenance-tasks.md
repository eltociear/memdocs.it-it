---
title: Informazioni di riferimento per le attività di manutenzione
titleSuffix: Configuration Manager
description: Dettagli per ogni attività di manutenzione del sito di Configuration Manager
ms.date: 06/04/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 68dc6acd-5848-47a4-b4c1-ffa40e47890b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f686547e4698f1941a64f5b0346ba2d723248c31
ms.sourcegitcommit: 4f10625e8d12aec294067a1d9138cbce19707560
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2020
ms.locfileid: "87912512"
---
# <a name="reference-for-maintenance-tasks-in-configuration-manager"></a>Informazioni di riferimento per le attività di manutenzione | Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Questo articolo elenca informazioni dettagliate per ogni attività di manutenzione del sito di Configuration Manager. Ogni voce specifica i tipi di sito in cui l'attività è disponibile e se è abilitata per impostazione predefinita.

Per altre informazioni, vedere [Impostare le attività di manutenzione](maintenance-tasks.md#set-up-maintenance-tasks).  

## <a name="tasks"></a>Attività

### <a name="backup-site-server"></a>Backup server sito

Usare questa attività per creare un backup delle informazioni critiche per ripristinare un sito e il database di Configuration Manager. Per altre informazioni, vedere [Eseguire il backup di un sito di Configuration Manager](backup-and-recovery.md).  

| Tipo di sito | Stato |
| --------- | ------ |
|**Sito di amministrazione centrale**|Abilitato|
|**Sito primario**|Non abilitato|
|Sito secondario|Non disponibile|

### <a name="check-application-title-with-inventory-information"></a>Verifica titolo applicazione con le informazioni di inventario

Usare questa attività per mantenere la coerenza dei titoli software tra l'inventario software e il catalogo Asset Intelligence. Per altre informazioni, vedere [Introduzione ad Asset Intelligence](../../clients/manage/asset-intelligence/introduction-to-asset-intelligence.md).  

| Tipo di sito | Stato |
| --------- | ------ |
|**Sito di amministrazione centrale**|Abilitato|
|Sito primario|Non disponibile|
|Sito secondario|Non disponibile|

### <a name="clear-undiscovered-clients"></a>Clear Undiscovered Clients (Cancella client non individuati)

> [!Tip]
> Questa attività potrebbe anche essere visualizzata nella console con il nome **Cancella flag di installazione**.

usare questa attività per rimuovere il flag installato per i client che non inviano un record dell'individuazione heartbeat durante il **Periodo nuova individuazione client**. Il flag installato impedisce l'installazione push client automatica a un computer che potrebbe avere un client attivo di Configuration Manager.  

| Tipo di sito | Stato |
| --------- | ------ |
|Sito di amministrazione centrale|Non disponibile|
|**Sito primario**|Non abilitato|
|Sito secondario|Non disponibile|

### <a name="delete-aged-application-request-data"></a>Elimina dati richiesta applicazione obsoleti

Usare questa attività per eliminare dal database le richieste di applicazioni obsolete. Per altre informazioni, vedere [Create and deploy an application](../../../apps/get-started/create-and-deploy-an-application.md) (Creare e distribuire un'applicazione).  

| Tipo di sito | Stato |
| --------- | ------ |
|Sito di amministrazione centrale|Non disponibile|
|**Sito primario**|Abilitato|
|Sito secondario|Non disponibile|

### <a name="delete-aged-application-revisions"></a>Elimina revisioni applicazioni obsolete

Usare questa attività per eliminare le revisioni applicazione a cui non viene più fatto riferimento. Per altre informazioni, vedere [Come rivedere e sostituire le applicazioni](../../../apps/deploy-use/revise-and-supersede-applications.md).

| Tipo di sito | Stato |
| --------- | ------ |
|**Sito di amministrazione centrale**|Abilitato|
|**Sito primario**|Abilitato|
|Sito secondario|Non disponibile|

### <a name="delete-aged-client-download-history"></a>Eliminare la cronologia di download del client obsoleti

usare questa attività per eliminare i dati della cronologia relativi all'origine dei download usata dai client. Questo sito usa le informazioni sull'origine dei download per popolare il [dashboard Origini dati del client](../deploy/configure/monitor-content-you-have-distributed.md#client-data-sources-dashboard).

| Tipo di sito | Stato |
| --------- | ------ |
|Sito di amministrazione centrale|Non disponibile|
|**Sito primario**|Abilitato|
|Sito secondario|Non disponibile|

### <a name="delete-aged-client-operations"></a>Elimina operazioni client obsolete

Usare questa attività per eliminare dal database del sito tutti i dati obsoleti per le operazioni client. Questi dati includono, ad esempio, le operazioni seguenti:

- Notifiche client obsolete o scadute, ad esempio richieste di download per criteri computer o utente
- Endpoint Protection, come le richieste da parte di un utente amministratore ai client di eseguire un'analisi o scaricare definizioni aggiornate
- Risultati dello stato di esecuzione degli script

| Tipo di sito | Stato |
| --------- | ------ |
|**Sito di amministrazione centrale**|Abilitato|
|**Sito primario**|Abilitato|
|Sito secondario|Non disponibile|

### <a name="delete-aged-client-presence-history"></a>Elimina cronologia presenze client obsolete
<!-- not listed in dogfood for either primary or CAS, was it renamed? -->
Usare questa attività per eliminare le informazioni sulla cronologia relative allo stato online dei client, registrato tramite notifica client. Elimina le informazioni per i client con stato precedente all'ora specificata. Per altre informazioni, vedere [Come monitorare i client](../../clients/manage/monitor-clients.md).

| Tipo di sito | Stato |
| --------- | ------ |
|**Sito di amministrazione centrale**|Abilitato|
|**Sito primario**|Abilitato|
|Sito secondario|Non disponibile|

### <a name="delete-aged-cloud-management-gateway-traffic-data"></a>Elimina i dati di traffico del gateway di gestione cloud obsoleti

Usare questa attività per eliminare dal database del sito tutti i dati obsoleti relativi al traffico che passa attraverso il [gateway di gestione cloud](../../clients/manage/cmg/plan-cloud-management-gateway.md). Questi dati includono:

- Numero di richieste
- Byte totali delle richieste
- Byte totali delle risposte
- Numero di richieste non riuscite
- Numero massimo di richieste simultanee

| Tipo di sito | Stato |
| --------- | ------ |
|**Sito di amministrazione centrale**|Abilitato|
|**Sito primario**|Abilitato|
|Sito secondario|Non disponibile|

### <a name="delete-aged-cmpivot-results"></a>Delete Aged CMPivot Results (Elimina risultati CMPivot obsoleti)

Usare questa attività per eliminare dal database del sito le informazioni obsolete dai client nelle query CMPivot. Per altre informazioni, vedere [CMPivot per i dati in tempo reale in Configuration Manager](cmpivot.md).

| Tipo di sito | Stato |
| --------- | ------ |
|Sito di amministrazione centrale|Non disponibile|
|**Sito primario**|Abilitato|
|Sito secondario|Non disponibile|

### <a name="delete-aged-collected-files"></a>Elimina file raccolti obsoleti

Usare questa attività per eliminare dal database le informazioni obsolete sui file raccolti. Questa attività elimina anche i file raccolti dalla struttura delle cartelle del server del sito nel sito selezionato. Per impostazione predefinita, le cinque copie più recenti dei file raccolti sono archiviate sul server del sito nella directory **Inboxes\sinv.box\FileCol**. Per altre informazioni, vedere [Introduzione all'inventario software](../../clients/manage/inventory/introduction-to-software-inventory.md).  

| Tipo di sito | Stato |
| --------- | ------ |
|Sito di amministrazione centrale|Non disponibile|
|**Sito primario**|Abilitato|
|Sito secondario|Non disponibile|

### <a name="delete-aged-computer-association-data"></a>Elimina dati di associazione computer obsoleti

Usare questa attività per eliminare dal database i dati obsoleti di associazione computer della distribuzione del sistema operativo. Queste informazioni vengono usate per il ripristino dello stato utente durante una sequenza di attività. Per altre informazioni, vedere [Gestire lo stato utente](../../../osd/get-started/manage-user-state.md).  

| Tipo di sito | Stato |
| --------- | ------ |
|Sito di amministrazione centrale|Non disponibile|
|**Sito primario**|Abilitato|
|Sito secondario|Non disponibile|

### <a name="delete-aged-console-connection-data"></a>Eliminare i dati di connessione alla console obsoleti

Questa attività elimina i dati dal database del sito sulle connessioni della console al sito.<!-- SCCMDocs#528 -->

| Tipo di sito | Stato |
| --------- | ------ |
|**Sito di amministrazione centrale**|Abilitato|
|**Sito primario**|Abilitato|
|Sito secondario|Non disponibile|

### <a name="delete-aged-delete-detection-data"></a>Elimina dati di rilevamento eliminazione obsoleti

Usare questa attività per eliminare dal database i dati obsoleti creati dalle visualizzazioni di estrazione. Elimina le informazioni sulle modifiche ai dati obsolete usate dai sistemi esterni estraendo i dati dal database.<!--SCCMDocs#1590--><!--By default, Extraction Views are disabled. You only enable them by using the Configuration Manager SDK. Unless Extraction Views are enabled, there is no data for this task to delete.-->

| Tipo di sito | Stato |
| --------- | ------ |
|**Sito di amministrazione centrale**|Abilitato|
|**Sito primario**|Abilitato|
|Sito secondario|Non disponibile|

### <a name="delete-aged-device-wipe-record"></a>Elimina record di cancellazione dati dispositivo obsoleto

Usare questa attività per eliminare dal database i dati obsoleti sulle azioni di cancellazione dei dati dei dispositivi mobili. Per altre informazioni, vedere [Proteggere i dati con cancellazione remota, blocco remoto o reimpostazione passcode](../../../mdm/deploy-use/wipe-lock-reset-devices.md).  

| Tipo di sito | Stato |
| --------- | ------ |
|Sito di amministrazione centrale|Non disponibile|
|**Sito primario**|Abilitato|
|Sito secondario|Non disponibile|

### <a name="delete-aged-discovery-data"></a>Elimina dati di individuazione obsoleti

Usare questa attività per eliminare dal database i dati di individuazione obsoleti. Questi dati possono includere record da:

- Individuazione heartbeat
- Individuazione della rete
- Metodi di individuazione di Active Directory: sistema, utente e gruppo

Questa attività rimuove anche i dispositivi obsoleti contrassegnati come non autorizzati. Quando questa attività viene eseguita in un sito, i dati associati a tale sito vengono eliminati e le modifiche vengono replicate in altri siti. Per altre informazioni, vedere [Eseguire l'individuazione](../deploy/configure/run-discovery.md).

| Tipo di sito | Stato |
| --------- | ------ |
|Sito di amministrazione centrale|Non disponibile|
|**Sito primario**|Abilitato|
|Sito secondario|Non disponibile|

### <a name="delete-aged-distribution-point-usage-stats"></a>Elimina statistiche di utilizzo punti di distribuzione obsolete

Usare questa attività per eliminare dal database i dati obsoleti per i punti di distribuzione che sono archiviati da più tempo rispetto a un intervallo specificato.  

| Tipo di sito | Stato |
| --------- | ------ |
|**Sito di amministrazione centrale**|Abilitato|
|**Sito primario**|Abilitato|
|Sito secondario|Non disponibile|

### <a name="delete-aged-enrolled-devices"></a>Elimina dispositivi registrati obsoleti

Usare questa attività per eliminare dal database del sito i dati obsoleti relativi ai dispositivi mobili che non hanno inviato informazioni al sito per un determinato periodo di tempo.

Questa attività si applica ai dispositivi registrati in una [soluzione MDM locale](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) di Configuration Manager. Per altre informazioni su questi dispositivi, vedere [Sistemi operativi supportati per client e dispositivi](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_OnpremOS).

| Tipo di sito | Stato |
| --------- | ------ |
|Sito di amministrazione centrale|Non disponibile|
|**Sito primario**|Non abilitato|
|Sito secondario|Non disponibile|

### <a name="delete-aged-ep-health-status-history-data"></a>Elimina dati cronologia stato integrità di Endpoint Protection obsoleti

Usare questa attività per eliminare dal database le informazioni di stato obsolete per Endpoint Protection. Per altre informazioni, vedere [Come monitorare Endpoint Protection](../../../protect/deploy-use/monitor-endpoint-protection.md).

| Tipo di sito | Stato |
| --------- | ------ |
|Sito di amministrazione centrale|Non disponibile|
|**Sito primario**|Abilitato|
|Sito secondario|Non disponibile|

### <a name="delete-aged-exchange-partnership"></a>Delete Aged Exchange Partnership (Elimina relazione Exchange obsoleta)

> [!Tip]
> > Questa attività potrebbe essere anche visualizzata nella console con il nome **Elimina dispositivi gestiti dal connettore Exchange Server obsoleti**.

Usare questa attività per eliminare i dati obsoleti sui dispositivi mobili gestiti dal connettore Exchange Server. Il sito elimina questi dati in base all'impostazione **Ignora dispositivi mobili inattivi da più di (giorni)** nella scheda **Individuazione** delle proprietà del connettore Exchange Server. Per altre informazioni, vedere [Gestire i dispositivi mobili con Configuration Manager ed Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).

| Tipo di sito | Stato |
| --------- | ------ |
|Sito di amministrazione centrale|Non disponibile|
|**Sito primario**|Abilitato|
|Sito secondario|Non disponibile|

### <a name="delete-aged-inventory-history"></a>Elimina cronologia inventario obsoleta

Usare questa attività per eliminare dal database i dati di inventario che sono archiviati da più tempo rispetto a un intervallo specificato. Per altre informazioni, vedere [Come usare Esplora inventario risorse per visualizzare l'inventario hardware](../../clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md).

| Tipo di sito | Stato |
| --------- | ------ |
|Sito di amministrazione centrale|Non disponibile|
|**Sito primario**|Abilitato|
|Sito secondario|Non disponibile|

### <a name="delete-aged-log-data"></a>Elimina dati registro obsoleti

Usare questa attività per eliminare dal database i dati dei log obsoleti usati per la risoluzione dei problemi. Questi dati non sono correlati alle operazioni dei componenti di Configuration Manager.  

> [!IMPORTANT]  
> Per impostazione predefinita, questa attività viene eseguita ogni giorno in ogni sito. In un sito di amministrazione centrale e nei siti primari, l'attività elimina i dati che hanno più di 30 giorni. Quando si usa SQL Server Express in un sito secondario, assicurarsi che questa attività venga eseguita ogni giorno e che elimini i dati non attivi da sette giorni.  

| Tipo di sito | Stato |
| --------- | ------ |
|**Sito di amministrazione centrale**|Abilitato|
|**Sito primario**|Abilitato|
|**Sito secondario**|Abilitato|

### <a name="delete-aged-metering-data"></a>Elimina dati di controllo software obsoleti

Usare questa attività per eliminare dal database i dati obsoleti per il controllo software che sono archiviati da più tempo rispetto a un intervallo specificato. Per altre informazioni, vedere [Controllo del software](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).

| Tipo di sito | Stato |
| --------- | ------ |
|Sito di amministrazione centrale|Non disponibile|
|**Sito primario**|Abilitato|
|Sito secondario|Non disponibile|

### <a name="delete-aged-metering-summary-data"></a>Elimina dati di riepilogo di controllo software obsoleti

Usare questa attività per eliminare dal database i dati obsoleti di riepilogo per il controllo software che sono archiviati da più tempo rispetto a un intervallo specificato. Per altre informazioni, vedere [Controllo del software](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).

| Tipo di sito | Stato |
| --------- | ------ |
|Sito di amministrazione centrale|Non disponibile|
|**Sito primario**|Abilitato|
|Sito secondario|Non disponibile|

### <a name="delete-aged-notification-server-history"></a>Delete Aged Notification (Elimina cronologia server notifiche obsolete)

Questa attività elimina la cronologia delle presenze client obsolete.

| Tipo di sito | Stato |
| --------- | ------ |
|**Sito di amministrazione centrale**|Abilitato|
|**Sito primario**|Abilitato|
|Sito secondario|Non disponibile|

### <a name="delete-aged-notification-task-history"></a>Elimina cronologia attività di notifica obsolete

Usare questa attività per eliminare dal database del sito le informazioni sulle attività di notifica client. Questa attività si applica ai dati che non sono stati aggiornati per un determinato periodo di tempo. Per altre informazioni, vedere [Client notifications](../../clients/manage/client-notification.md) (Notifiche client).

| Tipo di sito | Stato |
| --------- | ------ |
|Sito di amministrazione centrale|Non disponibile|
|**Sito primario**|Abilitato|
|Sito secondario|Non disponibile|

### <a name="delete-aged-passcode-records"></a>Elimina record passcode obsoleti

Usare questa attività nel sito principale della gerarchia per eliminare i dati obsoleti di reimpostazione dei passcode per i dispositivi Windows Phone. I dati di reimpostazione dei passcode sono crittografati ma non includono il PIN per i dispositivi. Per impostazione predefinita, questa attività è abilitata ed elimina i dati che hanno più di un giorno.  

| Tipo di sito | Stato |
| --------- | ------ |
|**Sito di amministrazione centrale**|Abilitato|
|**Sito primario**|Abilitato|
|Sito secondario|Non disponibile|

### <a name="delete-aged-replication-data"></a>Delete Aged Replication Data (Elimina dati di replica obsoleti)

Usare questa attività per eliminare dal database i dati obsoleti relativi alla replica di database tra siti di Configuration Manager. Quando si modifica la configurazione di questa attività di manutenzione, le modifiche si applicano ad ogni sito applicabile della gerarchia. Per altre informazioni, vedere [Monitorare la replica di database](monitor-replication.md).  

| Tipo di sito | Stato |
| --------- | ------ |
|**Sito di amministrazione centrale**|Abilitato|
|**Sito primario**|Abilitato|
|**Sito secondario**|Abilitato|

### <a name="delete-aged-replication-summary-data"></a>Elimina dati di riepilogo replica obsoleti

Usare questa attività per eliminare i dati di riepilogo replica obsoleti dal database del sito quando tale database non è stato aggiornato per un determinato periodo. Per altre informazioni, vedere [Monitorare la replica di database](monitor-replication.md).  

| Tipo di sito | Stato |
| --------- | ------ |
|**Sito di amministrazione centrale**|Abilitato|
|**Sito primario**|Abilitato|
|**Sito secondario**|Abilitato|

### <a name="delete-aged-status-messages"></a>Elimina messaggi di stato obsoleti

Usare questa attività per eliminare dal database i dati dei messaggi di stato obsoleti configurati nelle regole di filtro dello stato. Per altre informazioni, vedere [Monitorare il sistema di stato di Configuration Manager](use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus).

| Tipo di sito | Stato |
| --------- | ------ |
|**Sito di amministrazione centrale**|Abilitato|
|**Sito primario**|Abilitato|
|Sito secondario|Non disponibile|

### <a name="delete-aged-threat-data"></a>Elimina dati sulle minacce obsoleti

Usare questa attività per eliminare dal database i dati sulle minacce obsoleti di Endpoint Protection che sono archiviati da più tempo rispetto a un intervallo specificato. Per altre informazioni, vedere [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md).

| Tipo di sito | Stato |
| --------- | ------ |
|Sito di amministrazione centrale|Non disponibile|
|**Sito primario**|Abilitato|
|Sito secondario|Non disponibile|

### <a name="delete-aged-unknown-computers"></a>Elimina computer sconosciuti obsoleti

usare questa attività per eliminare le informazioni relative ai computer sconosciuti dal database del sito quando tale database non è stato aggiornato per un determinato periodo. Per altre informazioni, vedere [Operazioni preliminari alle distribuzioni in computer sconosciuti](../../../osd/get-started/prepare-for-unknown-computer-deployments.md).

| Tipo di sito | Stato |
| --------- | ------ |
|Sito di amministrazione centrale|Non disponibile|
|**Sito primario**|Abilitato|
|Sito secondario|Non disponibile|

### <a name="delete-aged-user-device-affinity-data"></a>Elimina dati di affinità utente dispositivo obsoleti

Usare questa attività per eliminare dal database i dati di affinità utente dispositivo obsoleti. Per altre informazioni, vedere [Collegare utenti e dispositivi mediante l'affinità utente dispositivo](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

| Tipo di sito | Stato |
| --------- | ------ |
|Sito di amministrazione centrale|Non disponibile|
|**Sito primario**|Abilitato|
|Sito secondario|Non disponibile|

### <a name="delete-duplicate-system-discovery-data"></a>Elimina dati di individuazione di sistema duplicati

Usare questa attività per eliminare dal database del sito tutti i record duplicati generati dall'individuazione di sistema.<!-- SCCMDocs#1339 -->

| Tipo di sito | Stato |
| --------- | ------ |
|**Sito di amministrazione centrale**|Abilitato|
|Sito primario|Non disponibile|
|Sito secondario|Non disponibile|

### <a name="delete-expired-mdm-bulk-enroll-package-records"></a>Elimina i record dei pacchetti di registrazione in blocco di MDM scaduti

usare questa attività per eliminare i certificati di registrazione in blocco precedenti e i profili corrispondenti dopo la scadenza del certificato di registrazione. Per altre informazioni, vedere [Creare i profili certificato](../../../protect/deploy-use/create-certificate-profiles.md).

| Tipo di sito | Stato |
| --------- | ------ |
|**Sito di amministrazione centrale**|Abilitato|
|**Sito primario**|Abilitato|
|Sito secondario|Non disponibile|

### <a name="delete-inactive-client-discovery-data"></a>Elimina dati di individuazione client non attivi

Usare questa attività per eliminare dal database i dati di individuazione per i client inattivi. Il sito contrassegna i client come inattivi in base a configurazioni relative allo stato del client oppure quando riportano il flag obsoleto.

Questa attività funziona solo nelle risorse che sono client di Configuration Manager. È diversa dall'attività **Elimina dati di individuazione obsoleti** che elimina qualsiasi record dei dati di individuazione obsoleti. Quando questa attività viene eseguita su un sito, rimuove i dati dal database da tutti i siti di una gerarchia. Per altre informazioni, vedere [Come configurare lo stato del client](../../clients/deploy/configure-client-status.md).

> [!IMPORTANT]  
> Quando abilitata, configurare questa attività in modo che venga eseguita con un intervallo maggiore rispetto a **Individuazione heartbeat**. Questa configurazione abilita i client attivi all'invio di un record di Individuazione heartbeat per contrassegnare il record client come attivo e impedirne così l'eliminazione da parte dell'attività.  

| Tipo di sito | Stato |
| --------- | ------ |
|Sito di amministrazione centrale|Non disponibile|
|**Sito primario**|Non abilitato|
|Sito secondario|Non disponibile|

### <a name="delete-obsolete-alerts"></a>Elimina avvisi obsoleti

Usare questa attività per eliminare dal database gli avvisi scaduti che sono archiviati da più tempo rispetto a un intervallo specificato. Per altre informazioni, vedere [Usare gli avvisi e il sistema di stato](use-alerts-and-the-status-system.md).

| Tipo di sito | Stato |
| --------- | ------ |
|**Sito di amministrazione centrale**|Abilitato|
|**Sito primario**|Abilitato|
|Sito secondario|Non disponibile|

### <a name="delete-obsolete-client-discovery-data"></a>Elimina dati di individuazione client obsoleti

Usare questa attività per eliminare dal database i record dei client obsoleti. Un record contrassegnato come obsoleto è stato in genere sostituito da un record più recente per lo stesso client. Il record più recente diventa il record corrente del client. Per informazioni sull'individuazione, vedere [Eseguire l'individuazione](../deploy/configure/run-discovery.md).

> [!IMPORTANT]  
> Quando abilitata, configurare questa attività in modo che venga eseguita con un intervallo maggiore rispetto a Individuazione heartbeat. Questa configurazione abilita il client per l'invio di un record Individuazione heartbeat che imposta correttamente lo stato obsoleto.  

| Tipo di sito | Stato |
| --------- | ------ |
|Sito di amministrazione centrale|Non disponibile|
|**Sito primario**|Non abilitato|
|Sito secondario|Non disponibile|

### <a name="delete-obsolete-forest-discovery-sites-and-subnets"></a>Elimina siti e subnet di individuazione foresta obsoleti

Usare questa attività per eliminare i dati relativi a siti, subnet e domini di Active Directory. Rimuove i dati che il sito non ha individuato dal metodo di individuazione della foresta Active Directory negli ultimi 30 giorni. Questa attività rimuove i dati di individuazione, ma non influisce sui limiti creati da tali dati. Per altre informazioni, vedere [Eseguire l'individuazione](../deploy/configure/run-discovery.md).

| Tipo di sito | Stato |
| --------- | ------ |
|**Sito di amministrazione centrale**|Abilitato|
|**Sito primario**|Abilitato|
|Sito secondario|Non disponibile|

### <a name="delete-orphaned-client-deployment-state-records"></a>Elimina i record sullo stato di distribuzione del client orfano

usare questa attività per ripulire periodicamente la tabella contenente le informazioni sullo stato di distribuzione dei client. Questa attività elimina i record associati a dispositivi obsoleti o non autorizzati.  

| Tipo di sito | Stato |
| --------- | ------ |
|Sito di amministrazione centrale|Non disponibile|
|**Sito primario**|Abilitato|
|Sito secondario|Non disponibile|

### <a name="evaluate-collection-members"></a>Valuta membri raccolta

Configurare la valutazione appartenenza alla raccolta come componente del sito. Per altre informazioni, vedere [Componenti del sito](../deploy/configure/site-components.md).

| Tipo di sito | Stato |
| --------- | ------ |
|Sito di amministrazione centrale|Non disponibile|
|**Sito primario**|Abilitato|
|Sito secondario|Non disponibile|

### <a name="monitor-keys"></a>Esegui monitoraggio chiavi

usare questa attività per monitorare l'integrità delle chiavi primarie del database di Configuration Manager. Una chiave primaria è una colonna o una combinazione di colonne che identifica in modo univoco una riga. La chiave distingue la riga da qualsiasi altra riga in una tabella di database di Microsoft SQL Server.

| Tipo di sito | Stato |
| --------- | ------ |
|**Sito di amministrazione centrale**|Abilitato|
|**Sito primario**|Abilitato|
|Sito secondario|Non disponibile|

### <a name="rebuild-indexes"></a>Ricompila indici

usare questa attività per ricompilare gli indici del database di Configuration Manager. Un indice è una struttura di database creata in una tabella di database per velocizzare il recupero dei dati. Ad esempio, la ricerca in una colonna indicizzata è spesso molto più veloce rispetto alla ricerca in una colonna non indicizzata.

Per migliorare le prestazioni, gli indici del database di Configuration Manager vengono aggiornati di frequente, in modo che rimangano sincronizzati con i dati costantemente modificati archiviati nel database. Questa attività:

- Crea indici per le colonne del database che sono univoche almeno al 50%
- Elimina gli indici per colonne che sono univoche meno del 50%
- Ricompila tutti gli indici esistenti che soddisfano i criteri di univocità dei dati

| Tipo di sito | Stato |
| --------- | ------ |
|**Sito di amministrazione centrale**|Non abilitato|
|**Sito primario**|Non abilitato|
|**Sito secondario**|Non abilitato|

### <a name="summarize-file-usage-metering-data"></a>Riepiloga dati utilizzo file di controllo software

Usare questa attività per riepilogare in un unico record generale i dati di più record sull'utilizzo di file di controllo software. L'attività di riepilogo dei dati può ridurre la quantità di dati archiviati nel database di Configuration Manager.

Per riepilogare i dati di controllo software contenendo lo spazio occupato nel database, usare questa attività insieme all'attività **Riepiloga dati utilizzo mensile di controllo software**. Per altre informazioni, vedere [Controllo del software](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).

| Tipo di sito | Stato |
| --------- | ------ |
|Sito di amministrazione centrale|Non disponibile|
|**Sito primario**|Abilitato|
|Sito secondario|Non disponibile|

### <a name="summarize-installed-software-data"></a>Riepiloga dati software installato

Usare questa attività per riepilogare le informazioni sul software di asset intelligence raccolte tramite l'inventario hardware per unire più record in un unico record generale. L'attività di riepilogo dei dati può ridurre la quantità di dati archiviati nel database di Configuration Manager. Per altre informazioni, vedere [Configurare le attività di manutenzione di Asset Intelligence](../../clients/manage/asset-intelligence/configuring-asset-intelligence.md#BKMK_ConfigureMaintenanceTasks).

| Tipo di sito | Stato |
| --------- | ------ |
|Sito di amministrazione centrale|Non disponibile|
|**Sito primario**|Abilitato|
|Sito secondario|Non disponibile|

### <a name="summarize-monthly-usage-metering-data"></a>Riepiloga dati utilizzo mensile di controllo software

Usare questa attività per riepilogare in un unico record generale i dati di più record sull'utilizzo mensile del controllo software. L'attività di riepilogo dei dati può ridurre la quantità di dati archiviati nel database di Configuration Manager.

Per riepilogare i dati di controllo software contenendo lo spazio occupato nel database, usare questa attività insieme all'attività **Riepiloga dati utilizzo file di controllo software**. Per altre informazioni, vedere [Controllo del software](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).

| Tipo di sito | Stato |
| --------- | ------ |
|Sito di amministrazione centrale|Non disponibile|
|**Sito primario**|Abilitato|
|Sito secondario|Non disponibile|

### <a name="update-application-available-targeting"></a>Aggiorna assegnazione disponibile per l'applicazione

usare questa attività per fare in modo che Configuration Manager ricalcoli il mapping dei criteri e le distribuzioni delle applicazioni alle risorse nelle raccolte. Quando si distribuiscono criteri o applicazioni a una raccolta, Configuration Manager crea un mapping iniziale tra gli oggetti distribuiti e i membri della raccolta.

Questi mapping sono memorizzati in una tabella di riferimento rapido. Quando cambia l'appartenenza alle raccolte, il sito aggiorna questi mapping archiviati per riflettere tali modifiche. È comunque possibile che questi mapping perdano la sincronizzazione. Ad esempio, se il sito non riesce a elaborare correttamente un file di notifica, la modifica potrebbe non essere rispecchiata nei mapping. Questa attività aggiorna il mapping in base all'appartenenza alla raccolta corrente.  

| Tipo di sito | Stato |
| --------- | ------ |
|Sito di amministrazione centrale|Non disponibile|
|**Sito primario**|Abilitato|
|Sito secondario|Non disponibile|

### <a name="update-application-catalog-tables"></a>Aggiorna tabelle del Catalogo applicazioni

Usare questa attività per sincronizzare la cache del database del sito Web del Catalogo applicazioni con le ultime informazioni sulle applicazioni. Quando si modifica la configurazione di questa attività di manutenzione, le modifiche si applicano a tutti i siti primari della gerarchia.  

| Tipo di sito | Stato |
| --------- | ------ |
|Sito di amministrazione centrale|Non disponibile|
|**Sito primario**|Abilitato|
|Sito secondario|Non disponibile|


## <a name="see-also"></a>Vedere anche

[Attività di manutenzione](maintenance-tasks.md)
