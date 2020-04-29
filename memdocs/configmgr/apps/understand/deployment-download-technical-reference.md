---
title: Guida di riferimento tecnico per il download delle applicazioni
titleSuffix: Configuration Manager
description: Guida di riferimento tecnico per la risoluzione dei problemi di download delle applicazioni in Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 41c29a07-9bf6-4ec4-b3f2-1c05e001eff7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: effa8115a5023a8e0611f6bc4245a101b3a47e38
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688859"
---
# <a name="application-download-in-configuration-manager"></a>Download delle applicazioni in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Prima di continuare, vedere [Componenti client di distribuzione delle applicazioni](client-components-technical-reference.md) per comprendere l'elaborazione dei processi dell'agente CI e DCM.

## <a name="download-initiation"></a>Avvio del download

Il download del contenuto dell'applicazione viene avviato dal componente agente CI nel client durante la fase **StateDownloadingContents**. Questo processo è lo stesso, indipendentemente dal fatto che l'applicazione venga distribuita a una raccolta di dispositivi o a una raccolta di utenti.

- Per le distribuzioni con stato **Disponibile**, il contenuto dell'applicazione viene scaricato quando l'utente avvia l'installazione dell'applicazione da Software Center.
- Per le distribuzioni con stato **Richiesta**, il contenuto dell'applicazione viene scaricato quando l'assegnazione viene attivata e l'applicazione viene considerata applicabile in seguito alla valutazione. Per capire quando viene attivata l'assegnazione, vedere gli articoli [Distribuzione di applicazioni in raccolte di dispositivi](device-deployment-technical-reference.md) o [Distribuzione di applicazioni in raccolte di utenti](user-deployment-technical-reference.md).

Quando l'agente CI avvia il download del contenuto, crea un'attività che viene gestita dal componente Task Manager di CI. Task Manager di CI avvia il download del contenuto. Questa attività può essere rilevata in **CITaskMgr.log** usando l'ID univoco del tipo di distribuzione.

<pre><code class="lang-text"><b>Initiating task ContentDownload</b> for CI ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44.2 (ConfigMgr Toolkit - Windows Installer (*.msi file)) for target: , consumer: {53EA65C2-D596-4215-83E4-F7007B78E18C}
</code></pre>

## <a name="distribution-point-location"></a>Posizione del punto di distribuzione

Tutte le attività di download sono gestite dal componente di accesso al contenuto, che è responsabile della gestione della cache del client. Dopo aver creato l'attività di download, il componente di accesso ai contenuti controlla se il contenuto è già disponibile nella cache del client. Se il contenuto non è disponibile, viene creata una richiesta di posizione per ottenere un elenco di punti di distribuzione da cui è possibile ottenere il contenuto. Questa attività può essere rilevata in **CAS.log** e **LocationServices.log** sul client usando l'ID univoco del contenuto.

```text
Requesting locations synchronously for content Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1 with priority Foreground
ContentLocationRequest : <Request XML Body>
Reply Message Body : <Reply XML Body>
```

> [!IMPORTANT]
> Anche se il componente dei servizi di posizione gestisce le richieste di posizione, non richiede direttamente le posizioni dal punto di gestione. Tutte le richieste al punto di gestione in genere passano tramite il componente di messaggistica CCM, che le registra in**CcmMessaging.log**.

Il codice XML di risposta della posizione contiene l'elenco dei punti di distribuzione in base al gruppo di limiti del client. Questo elenco viene analizzato e reso persistente in WMI nel client in base alla [Priorità dell'origine del contenuto](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#content-source-priority). Questa attività può essere visualizzata in **ContentTransferManager.log**, usando l'ID univoco del contenuto e cercando `Persisted location`. 

Se il codice XML di risposta della posizione non contiene punti di distribuzione, **ContentTransferManager.log** visualizzerà `Received empty location update` e il client potrebbe rimanere bloccato allo 0% durante il download dell'applicazione. Questa risposta può in genere verificarsi a causa di problemi di configurazione del gruppo di limiti. Per altre informazioni, vedere [Errori di download](../deploy-use/troubleshoot-application-deployment.md#download-failures).

## <a name="content-download"></a>Download del contenuto

Una volta ottenute le posizioni dei punti di distribuzione, il componente di accesso al contenuto crea un processo di trasferimento del contenuto. Questa attività può essere rilevata in **CAS.log** usando l'ID univoco del contenuto.

<pre><code class="lang-text">Submitted CTM job <b>{6D0EA720-EB4E-4893-8395-8B27470A6CFB}</b> to download Content <b>Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1</b> under context System
</code></pre>

La gestione del trasferimento del contenuto crea quindi un processo del servizio di trasferimento dei dati per eseguire il download del contenuto. Questa attività può essere rilevata in **ContentTransferManager.log** nel client usando l'ID univoco del contenuto.

<pre><code class="lang-text">CTM job <b>{6D0EA720-EB4E-4893-8395-8B27470A6CFB}</b> (corresponding DTS job <b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b>) started download from '<Distribution Point URL>/<b>Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1</b>' for full content download.
</code></pre>

> [!NOTE]
> Questa voce di log può essere usata per identificare gli ID dei processi CTM e DSS che possono essere usati per tenere traccia dello stato di avanzamento del trasferimento del contenuto rispettivamente in **ContentTransferManager.log** e **DataTransferService.log**.

Il servizio di trasferimento dei dati esegue il download del contenuto dell'applicazione creando un processo di Servizio trasferimento intelligente in background e attendendo il completamento del download. Questa attività può essere rilevata in **DataTransferService.log** sul client usando l'ID del processo DTS ottenuto da **ContentTransferService.log**.

<pre><code class="lang-text">Starting BITS job '{40263E01-2EDD-462F-ABBA-A5E892CB9229}' for DTS job '<b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b>' under user 'S-1-5-18'.
DTSJob <b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b> in state 'DownloadingData'.
DTS job <b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b> has completed
</code></pre>

Al termine del download, viene inviata una notifica al componente di accesso al contenuto. Il componente di accesso al contenuto verifica quindi il contenuto scaricato per assicurarsi che non sia stato modificato durante il download. Questa attività può essere rilevata in **CAS.log** usando l'ID univoco del contenuto.

```text
Hash verification succeeded for content Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1 downloaded under context System
```

Infine, dopo aver verificato il contenuto, l'agente CI riceve la notifica di completamento dell'attività e il processo dell'agente CI passa alla fase successiva.

<pre><code class="lang-text">CIAgentJob({2BF84225-C9E8-49A6-A308-A160C4B799D3}): CAgentJob::HandleEvent(<b>Event=CITaskComplete, CurrentState=StateDownloadingContents</b>)
</code></pre>

## <a name="next-steps"></a>Passaggi successivi

- [Installazione delle applicazioni](deployment-install-technical-reference.md)
