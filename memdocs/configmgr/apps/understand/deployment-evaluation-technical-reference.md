---
title: Guida di riferimento tecnico per la valutazione delle applicazioni
titleSuffix: Configuration Manager
description: Guida di riferimento tecnico per la risoluzione dei problemi di valutazione delle applicazioni in Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: a7035223-d7bd-47b4-896f-08de3416a4eb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fdeec54489adfc0d2a5cceb99c7e7587ce1a41ab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688839"
---
# <a name="application-deployment-evaluation"></a>Valutazione della distribuzione delle applicazioni

*Si applica a: Configuration Manager (Current Branch)*

Prima di continuare, vedere [Componenti client di distribuzione delle applicazioni](client-components-technical-reference.md) per comprendere l'elaborazione dei processi dell'agente CI e DCM.

La valutazione delle applicazioni viene eseguita dai componenti dell'agente DCM e dell'agente CI al momento dell'attivazione della distribuzione. Per capire quando viene attivata l'assegnazione, vedere gli articoli [Distribuzione di applicazioni in raccolte di dispositivi](device-deployment-technical-reference.md) o [Distribuzione di applicazioni in raccolte di utenti](user-deployment-technical-reference.md).

## <a name="application-detection-and-evaluation"></a>Rilevamento e valutazione delle applicazioni

La valutazione delle applicazioni viene eseguita durante la fase **InvokingSdmMethod** di un processo dell'agente CI. Questa fase è il punto in cui il client valuta il metodo di rilevamento definito per l'applicazione per determinare se l'applicazione è installata nel dispositivo. Questa attività può essere rilevata in **AppDiscovery.log** usando l'ID univoco del tipo di distribuzione o il nome del tipo di distribuzione.

```text
Performing detection of app deployment type ConfigMgr Toolkit - Windows Installer (*.msi file)(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, revision 2) for system.
+++ Did not detect app deployment type ConfigMgr Toolkit - Windows Installer (*.msi file)(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, revision 2) for system.
```

> [!NOTE]
> Nell'esempio precedente viene illustrato il rilevamento di un'applicazione MSI in cui il rilevamento viene eseguito controllando se il codice prodotto MSI è installato nel dispositivo. Per le applicazioni che usano metodi di rilevamento alternativi, viene usato il metodo di rilevamento appropriato per verificare se l'applicazione è installata.

Successivamente, il client valuta lo stato desiderato dell'applicazione in base allo scopo della distribuzione. Questo passaggio comporta anche il rilevamento della presenza di dipendenze o regole sostituzione che devono essere rispettate per l'applicazione. Questa attività può essere rilevata in **AppIntentEval.log** usando l'ID univoco del tipo di distribuzione e dell'applicazione.

<pre><code class="lang-text"># Available Application Deployment

[Application or DT Unique ID] :- <b>Current State = NotInstalled, Applicability = Applicable, ResolvedState = Available</b>, ConfigureState = NotNeeded, Title = [Application or DT Name]

# Required Application Deployment

[Application or DT Unique ID] :- <b>Current State = NotInstalled, Applicability = Applicable, ResolvedState = Installed</b>, ConfigureState = NotNeeded, Title = [Application or DT Name]

# Requirement Rules Not Met

[Application or DT Unique ID] :- <b>Current State = NotInstalled, Applicability = NotApplicable, ResolvedState = None</b>, ConfigureState = NotNeeded, Title = [Application or DT Name]
</code></pre>

Nella voce di log precedente **Current State** indica se l'applicazione è attualmente installata nel dispositivo. **Applicability** indica se l'applicazione è applicabile in base alle regole dei requisiti definite. **ResolvedState** indica lo stato desiderato dell'applicazione in base allo scopo della distribuzione.

> [!TIP]
> Usare lo [strumento di monitoraggio della distribuzione](../../core/support/deployment-monitoring-tool.md) per visualizzare lo stato dell'applicazione, lo stato di applicabilità e le violazioni dei requisiti.

## <a name="next-steps"></a>Passaggi successivi

- [Download delle applicazioni](deployment-download-technical-reference.md)
