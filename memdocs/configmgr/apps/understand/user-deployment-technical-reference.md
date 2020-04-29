---
title: Guida di riferimento tecnico per la distribuzione di app agli utenti
titleSuffix: Configuration Manager
description: Guida di riferimento tecnico per la risoluzione dei problemi di distribuzione delle applicazioni agli utenti in Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: b8e9dbfe-a046-4e06-8dec-cf0bc41ba095
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b44aad1db96b4191b9c9537acea4e64b1d30fde6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690269"
---
# <a name="application-deployment-policy-for-users"></a>Criteri di distribuzione delle applicazioni per gli utenti

*Si applica a: Configuration Manager (Current Branch)*

Quando un'applicazione viene distribuita in una raccolta di utenti, i criteri per la distribuzione vengono creati solo per le distribuzioni richieste. Per le distribuzioni disponibili, i criteri vengono creati quando l'utente tenta di installare l'applicazione da Software Center. In questo articolo viene illustrato il processo di distribuzione sia per le distribuzioni richieste che per le disponibili.

> [!TIP]
> Tutte le informazioni necessarie per esaminare i log del client possono essere ottenute eseguendo la query SQL a cui viene fatto riferimento nella sezione [Prima di iniziare](app-deployment-technical-reference.md#before-you-begin).

## <a name="required-deployments"></a>Distribuzioni richieste

Il criterio per una distribuzione dell'applicazione richiesta in una raccolta di utenti ha come destinazione tutti gli utenti della raccolta al momento della creazione della distribuzione. L'elaborazione lato client per queste distribuzioni è simile a una distribuzione richiesta in una raccolta di dispositivi. L'attivazione della distribuzione viene eseguita all'orario disponibile specificato e viene applicata a partire dalla scadenza definita. Per altre informazioni, vedere [Distribuzione di applicazioni in raccolte di dispositivi](device-deployment-technical-reference.md).

## <a name="available-deployments"></a>Distribuzioni disponibili

Le applicazioni disponibili distribuite in una raccolta di utenti si comportano in modo diverso. Questa modifica del comportamento consente all'amministratore di rendere le applicazioni disponibili agli utenti senza causare conflitti di risorse per i criteri. Quando un utente avvia Software Center, viene eseguita una query su un elenco di applicazioni disponibili per l'utente dal punto di gestione in tempo reale. Questa richiesta viene eseguita alla directory virtuale `CMUserService_WindowsAuth` nel punto di gestione e può essere visualizzata in **SCClient_[NomeUtente].log** nel client.

```text
Using endpoint Url: https://MP.CONTOSO.COM:443/CMUserService_WindowsAuth, Windows authentication
```

Quando il punto di gestione riceve questa richiesta, esegue una query sull'elenco di applicazioni disponibili per l'utente eseguendo la stored procedure `usp_GetApplicationPropertyValuesFiltered`. Questa attività può essere rilevata in **UserService.log** nel punto di gestione.

```text
GetFilteredApplications, startItem = 0, max rows = 60, search text = '', filter = '', user = CONTOSO\UserName, api = 4.0, source = UserService_WinAuth_SoftwareCenter, platform = <OSPlatform>
GetFilteredApplications: returned 1 rows out of 1 total
```

Software Center riceve l'elenco e visualizza le applicazioni che l'utente può installare. Quando l'utente fa clic sull'applicazione, viene eseguita una query sulle informazioni aggiuntive sull'applicazione dal punto di gestione, che implica l'esecuzione di stored procedure, come ad esempio usp_GetApplicationInfo, usp_GetAppModelApplicationSupersedence, usp_GetDeploymentTypeForAnApp, e così via.

La distribuzione viene attivata quando l'utente seleziona l'applicazione e fa clic sul pulsante **Installa** e viene creato un processo dell'agente DCM per la valutazione dell'applicazione. Se l'applicazione è applicabile, viene creato un altro processo dell'agente DCM per scaricare e imporre l'applicazione. Questa attività può essere rilevata in **DCMAgent.log** nel client.

## <a name="next-steps"></a>Passaggi successivi

- [Informazioni sui componenti client di distribuzione delle applicazioni](client-components-technical-reference.md)
