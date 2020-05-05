---
title: Risolvere i problemi relativi all'azione del dispositivo
titleSuffix: Configuration Manager
description: Risolvere i problemi di riferimento tecnico sulle azioni del dispositivo per Configuration Manager
ms.date: 04/01/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 44c2eb8a-3ccc-471f-838b-55d7971bb79e
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 72da589a3f4213fb64b4123d5580cb1be945de0e
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "82140276"
---
# <a name="troubleshooting-device-actions-for-configuration-manager-devices"></a>Risoluzione dei problemi relativi alle azioni del dispositivo per dispositivi Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

A partire da Configuration Manager 2002, i client Configuration Manager possono essere sincronizzati con l'interfaccia di amministrazione di Microsoft Endpoint Manager. Alcune azioni client possono essere eseguite dall'interfaccia di amministrazione di Microsoft Endpoint Manager nei client sincronizzati.

Sono disponibili le azioni seguenti:
- Criteri computer di sincronizzazione
- Criteri utente di sincronizzazione
- Ciclo di valutazione dell'app


[![Panoramica del dispositivo nell'interfaccia di amministrazione di Microsoft Endpoint Manager](./media/3555758-device-overview-actions.png)](./media/3555758-device-overview-actions.png#lightbox)
  
Quando un amministratore esegue un'azione dall'interfaccia di amministrazione di Microsoft Endpoint Manager, la richiesta di notifica viene trasmessa al sito Configuration Manager e dal sito al client.

## <a name="configuration-manager-components"></a>Componenti Configuration Manager

- **SMS_SERVICE_CONNECTOR**: usa il ruolo di lavoro notifiche del gateway per elaborare la notifica dall'interfaccia di amministrazione di Microsoft Endpoint Manager.
- **SMS_NOTIFICATION_SERVER**: ottiene la notifica e crea una notifica client.
- **BgbAgent**: il client ottiene l'attività ed esegue l'azione richiesta.

## <a name="sms_service_connector"></a>SMS_SERVICE_CONNECTOR

Quando viene avviata un'azione dall'interfaccia di amministrazione di Microsoft Endpoint Manager, **CMGatewayNotificationWorker. log** elabora la richiesta.  

```text
Received new notification. Validating basic notification details...
Validating device action message content...
Authorized to perform client action. TemplateID: RequestMachinePolicy TenantId: a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2 AADUserID:     a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2
Forwarded BGB remote task. TemplateID: 1 TaskGuid: a43dd1b3-a006-4604-b012-5529380b3b6f TaskParam: TargetDeviceIDs: 1  
```
 
1. Viene ricevuta una notifica dall'interfaccia di amministrazione di Microsoft Endpoint Manager.

   ```text
   Received new notification. Validating basic notification details..
   ```

1. Vengono convalidate le azioni utente e dispositivo.

   ```text
   Validating device action message content... 
   Authorized to perform client action. TemplateID: RequestMachinePolicy TenantId: a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2 AADUserID:     a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2
   ```

1. L'attività remota viene trasmessa all'SMS_NOTIFICATION_SERVER.

    ```text
   Forwarded BGB remote task. TemplateID: 1 TaskGuid: a43dd1b3-a006-4604-b012-5529380b3b6f TaskParam: TargetDeviceIDs: 1  
    ```


## <a name="sms_notification_server"></a>SMS_NOTIFICATION_SERVER

Una volta inviato il messaggio alla SMS_NOTIFICATION_SERVER, un'attività viene inviata dal punto di gestione al client corrispondente. In **BgbServer. log**verrà visualizzato quanto segue, che si trova nel punto di gestione:

```text
Get one push message from database.
Starting to send push task (PushID: 7 TaskID: 8 TaskGUID: A43DD1B3-A006-4604-B012-5529380B3B6F TaskType: 1 TaskParam: ) to 1 clients  with throttling (strategy: 1 param: 42)
```

## <a name="bgbagent"></a>BgbAgent

L'ultimo passaggio si verifica nel client e può essere visualizzato in **CcmNotificationAgent. log**. Una volta ricevuta l'attività, verrà richiesta l'utilità di pianificazione per eseguire l'azione. Quando viene eseguita l'azione, verrà visualizzato un messaggio di conferma:

```text
Receive task from server with pushid=7, taskid=8, taskguid=A43DD1B3-A006-4604-B012-5529380B3B6F, tasktype=1 and taskParam=

Send Task response message <BgbResponseMessage TimeStamp="2020-01-21T15:43:43Z"><PushID>8</PushID><TaskID>9</TaskID><ReturnCode>1</ReturnCode></BgbResponseMessage> successfully.
```

## <a name="common-issues"></a>Problemi comuni

Se l'amministratore non ha le autorizzazioni necessarie in Configuration Manager, verrà visualizzata una `Unauthorized` risposta in **CMGatewayNotificationWorker. log**.

```text
Received new notification. Validating basic notification details..
Validating device action message content...
Unauthorized to perform client action. TemplateID: RequestMachinePolicy TenantId: a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2 AADUserID: 3a1e89e6-e190-4615-9d38-a208b0eb1c78
```  

Verificare che l'utente che esegue l'azione dal centro di amministrazione di Microsoft Endpoint Manager disponga delle autorizzazioni necessarie per Configuration Manager sito. Per ulteriori informazioni, vedere [prerequisiti di connessione tenant di Microsoft Endpoint Manager](device-sync-actions.md#prerequisites).

## <a name="next-steps"></a>Passaggi successivi

[Abilitare la co-gestione](../comanage/overview.md) per ottenere altre funzionalità basate sul cloud, ad esempio l'accesso condizionale.
