---
title: Guida di riferimento tecnico per la distribuzione di app a raccolte di dispositivi
titleSuffix: Configuration Manager
description: Guida di riferimento tecnico per la risoluzione dei problemi di distribuzione delle applicazioni alle raccolte di dispositivi in Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 4e62b04d-fe56-42ed-87dc-e673cf061d52
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1965029a1933793057dc5768bacb391afd645404
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688789"
---
# <a name="application-deployment-for-device-collections"></a>Distribuzione di applicazioni in raccolte di dispositivi

*Si applica a: Configuration Manager (Current Branch)*

Quando un'applicazione viene distribuita in una raccolta di dispositivi, la destinazione dei criteri è costituita da tutti i dispositivi della raccolta, indipendentemente dallo scopo della distribuzione. Questo articolo illustra il download dei criteri e l'elaborazione della distribuzione nel client.

> [!TIP]
> Tutte le informazioni necessarie per esaminare i log del client possono essere ottenute eseguendo la query SQL a cui viene fatto riferimento nella sezione [Prima di iniziare](app-deployment-technical-reference.md#before-you-begin).

## <a name="policy-download"></a>Download dei criteri

Dopo che ai criteri per la distribuzione dell'applicazione è stato assegnato il client come destinazione, il client scarica i criteri al successivo ciclo di polling dei criteri. Quando il client scarica i criteri, scarica i criteri correlati oltre ai criteri di distribuzione. Questi criteri correlati includono i criteri per l'applicazione, il tipo di distribuzione, le condizioni globali e così via. È possibile rilevare l'attività di download dei criteri in **PolicyAgent.log** nel client, usando l'ID univoco dell'applicazione o dell'assegnazione.

<pre><code class="lang-text">Download of policy CCM_Policy_Policy5.PolicyID="{<b>3AC57DFE-3F87-4C59-930B-B9F57CB41B91</b>}",PolicySource="SMS:PS1",PolicyVersion="1.00" completed (DTS Job ID: {AE88E639-0E59-40D7-AAA9-4403AAE6EE82})
Policy state for [CCM_Policy_Policy5.PolicyID="{<b>3AC57DFE-3F87-4C59-930B-B9F57CB41B91</b>}",PolicySource="SMS:PS1",PolicyVersion="1.00"] is currently [Active]
</code></pre>

Una volta scaricati i criteri nel client, il componente utilità di pianificazione crea pianificazioni per l'attivazione e l'imposizione della distribuzione.

## <a name="deployment-activation"></a>Attivazione della distribuzione

La valutazione dell'applicazione viene avviata quando viene attivata la distribuzione. Il componente utilità di pianificazione crea una pianificazione per attivare l'assegnazione nell'ora disponibile configurata nella distribuzione. Questa attività può essere rilevata in **Scheduler.log** nel client usando l'ID univoco di assegnazione dell'applicazione.

- Per le distribuzioni con stato **Richiesta**, viene creata la pianificazione dell'attivazione, ma è previsto un ritardo di un massimo di due ore per evitare conflitti di risorse nei server del sito e nei punti di distribuzione. Il ritardo consente di evitare conflitti perché il contenuto dell'applicazione può essere scaricato durante la valutazione se l'applicazione è applicabile in base alle regole di requisiti definite.

    <pre><code class="lang-text">SMSTrigger '15AF8C4000080000' for scheduler '<b>Machine/{5F2FA409-C9B2-4100-8BC8-051820311DE1}</b>' will fire at 08/15/2019 01:44:00 PM with randomization.
    </code></pre>

- Per le distribuzioni con stato **Disponibile**, la pianificazione dell'attivazione viene creata per essere attivata all'ora disponibile configurata nella distribuzione.

    <pre><code class="lang-text">SMSTrigger '1E4F8C4000080001' for scheduler '<b>Machine/{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}</b>' will fire at 08/15/2019 01:13:33 PM without randomization.
    </code></pre>

Al momento dell'arrivo della pianificazione, il componente utilità di pianificazione invia il messaggio di attivazione all'agente DCM per eseguire la valutazione dell'applicazione.

<pre><code class="lang-text">Sending message for schedule '<b>Machine/{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}</b>' (Target: 'direct:DCMAgent', Name: '')
</code></pre>

L'agente DCM riceve il messaggio di attivazione e crea un processo per la valutazione dell'applicazione.

```text
CDCMAgent::HandleMessage - Message received for machine: '<?xml version='1.0' ?><CIAssignmentMessage MessageType='Activation'><AssignmentID>{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}</AssignmentID></CIAssignmentMessage>'
```

## <a name="deployment-enforcement"></a>Imposizione della distribuzione

L'installazione dell'applicazione viene avviata quando viene imposta la distribuzione.

- Per le distribuzioni con stato **Richiesta**, l'utilità di pianificazione crea una pianificazione della scadenza dopo il download dei criteri per imporre l'applicazione alla scadenza della distribuzione. La pianificazione della scadenza non è casuale per impostazione predefinita. Il comportamento casuale per l'attivazione può essere controllato dall'impostazione del client [Disabilitare sequenza casuale scadenza](../../core/clients/deploy/about-client-settings.md#disable-deadline-randomization).

    <pre><code class="lang-text">SMSTrigger '15EF8C4000080000' for scheduler '<b>Machine/DEADLINE:{5F2FA409-C9B2-4100-8BC8-051820311DE1}</b>' will fire at 08/15/2019 03:05:00 PM without randomization.
    </code></pre>

    Alla scadenza, il componente utilità di pianificazione invia il messaggio di scadenza all'agente DCM. 

    <pre><code class="lang-text">Sending message for schedule '<b>Machine/DEADLINE:{5F2FA409-C9B2-4100-8BC8-051820311DE1}</b>' (Target: 'direct:DCMAgent', Name: '')
    </code></pre>

    L'agente DCM riceve il messaggio di scadenza e crea un processo per imporre l'applicazione.
  
    ```text
    CDCMAgent::HandleMessage - Message received for machine: '<?xml version='1.0' ?><CIAssignmentMessage MessageType='EnforcementDeadline'><AssignmentID>{5F2FA409-C9B2-4100-8BC8-051820311DE1}</AssignmentID></CIAssignmentMessage>'
    ```

    > [!NOTE]
    > Per le distribuzioni con scadenza nel passato, l'applicazione viene attivata e imposta immediatamente dallo stesso processo dell'agente DCM che esegue le azioni di valutazione, download e installazione.

- Per le distribuzioni con stato **Disponibile**, non è prevista alcuna pianificazione delle scadenze perché l'imposizione si verifica quando l'installazione dell'applicazione viene avviata dall'utente da Software Center. Quando l'utente avvia un'installazione, viene creato un processo dell'agente DCM per eseguire la valutazione, il download e l'installazione dell'applicazione. Questa attività può essere rilevata in **DCMAgent.log** nel client.

## <a name="next-steps"></a>Passaggi successivi

- [Informazioni sui componenti client di distribuzione delle applicazioni](client-components-technical-reference.md)
