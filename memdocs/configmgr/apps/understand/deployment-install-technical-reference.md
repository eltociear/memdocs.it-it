---
title: Guida di riferimento tecnico per l'installazione delle applicazioni
titleSuffix: Configuration Manager
description: Guida di riferimento tecnico per la risoluzione dei problemi di installazione delle applicazioni in Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 2af4f9c3-16b8-4691-a59d-aea6241d288e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 13c96e9ad4f0608084d87bed3973221730cb2d5f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688819"
---
# <a name="application-installation"></a>Installazione dell'applicazione

*Si applica a: Configuration Manager (Current Branch)*

Prima di continuare, vedere [Componenti client di distribuzione delle applicazioni](client-components-technical-reference.md) per comprendere l'elaborazione dei processi dell'agente CI e DCM.

L'installazione delle applicazioni viene eseguita dai componenti dell'agente DCM e dell'agente CI nel momento in cui la distribuzione viene imposta. Il tempo di imposizione è diverso per le distribuzioni disponibili e richieste. Per capire quando viene imposta l'assegnazione, vedere gli articoli [Distribuzione di applicazioni in raccolte di dispositivi](device-deployment-technical-reference.md) o [Distribuzione di applicazioni in raccolte di utenti](user-deployment-technical-reference.md).

## <a name="enforcement-initiation"></a>Avvio imposizione

L'installazione dell'applicazione viene avviata dal componente dell'agente CI nel client durante la fase **StateEnforcingCIs**. Questo processo è lo stesso, indipendentemente dal fatto che l'applicazione venga distribuita a una raccolta di dispositivi o a una raccolta di utenti.

- Per le distribuzioni con stato **Disponibile**, l'applicazione viene installata quando l'utente avvia l'installazione dell'applicazione da Software Center.
- Per le distribuzioni con stato **Richiesta**, l'applicazione viene installata alla scadenza della distribuzione. Tuttavia, l'utente può avviare l'installazione da Software Center prima della scadenza.

Quando l'agente CI avvia l'installazione dell'applicazione, crea un'attività che viene gestita dal componente Task Manager di CI. Task Manager di CI quindi avvia l'installazione. Questa attività può essere rilevata in **CITaskMgr.log** usando l'ID univoco del tipo di distribuzione.

<pre><code class="lang-text"><b>Initiating task Enforce</b> for CI ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44.2 (ConfigMgr Toolkit - Windows Installer (*.msi file)) for target: , consumer: {9BC3154A-98F1-4595-A967-173D536A3F94}
Initiated application enforcement. : CITask(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44.2..Install.Enforce)
</code></pre>

## <a name="application-enforcement"></a>Imposizione dell'applicazione

Dopo l'avvio dell'imposizione dell'applicazione, il client esegue nuovamente il rilevamento dell'applicazione per assicurarsi che non sia già installata. Una volta determinato che l'applicazione non è installata, viene avviata l'installazione dell'applicazione. Questa attività può essere rilevata in **AppEnforce.log** nel client usando l'ID univoco del tipo di distribuzione.

```text
+++ Starting Install enforcement for App DT "ConfigMgr Toolkit - Windows Installer (*.msi file)" ApplicationDeliveryType - ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, Revision - 2, ContentPath - C:\WINDOWS\ccmcache\2, Execution Context - System
    Executing Command line: "C:\WINDOWS\system32\msiexec.exe" /i "ConfigMgrTools.msi" /q /qn with user context
    Process 7292 terminated with exitcode: 0
Status is switching to Success
```

## <a name="installation-verification"></a>Verifica dell'installazione

Dopo che l'applicazione è stata installata, viene usato di nuovo il metodo di rilevamento dell'applicazione per assicurarsi che venga rilevata come installata.

<pre><code class="lang-text">Performing detection of app deployment type ConfigMgr Toolkit - Windows Installer (*.msi file)(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, revision 2) for system.
+++ <b>Discovered MSI application</b> [AppDT Id: ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, Revision: 2, MSI Product code: {4FFF7ECC-CCF7-4530-B938-E7812BB91186}, MSI Product version: ]
++++++ <b>App enforcement completed</b> (3 seconds) for App DT "ConfigMgr Toolkit - Windows Installer (*.msi file)" [ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44], Revision: 2, User SID: ] ++++++
</code></pre>

Infine, dopo aver completato l'imposizione, l'agente CI riceve la notifica di completamento dell'attività e il processo dell'agente CI passa alla fase successiva.

<pre><code class="lang-text">CIAgentJob({2BF84225-C9E8-49A6-A308-A160C4B799D3}): CAgentJob::HandleEvent(<b>Event=CITaskComplete, CurrentState=StateEnforcingCIs</b>)
</code></pre>

## <a name="next-steps"></a>Passaggi successivi

[Risoluzione dei problemi relativi alla distribuzione di applicazioni](../deploy-use/troubleshoot-application-deployment.md)
