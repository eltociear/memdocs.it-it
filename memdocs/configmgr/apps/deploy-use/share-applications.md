---
title: Condividere le applicazioni nel Software Center
titleSuffix: Configuration Manager
description: Condividere un collegamento a un'applicazione in Software Center in Configuration Manager.
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: be2e930e3f59bc5a4d7db9e27ce2f875814fd358
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689239"
---
# <a name="share-an-application-from-software-center"></a>Condividere un'applicazione da Software Center

*Si applica a: Configuration Manager (Current Branch)* <!-- 1706 -->

È possibile copiare un collegamento ipertestuale in un'applicazione in Software Center usando il pulsante ![Condividi](media/share15.png)  **Condividi** nella vista Dettagli applicazione. È possibile condividere collegamenti ipertestuali solo per le applicazioni. Se un'applicazione non è più disponibile, il collegamento ipertestuale apre una finestra con un messaggio che informa dell'indisponibilità dell'applicazione.

1. Scegliere **Applicazioni** e quindi scegliere l'applicazione.
2. Fare clic sul pulsante ![Condividi](media/share15.png) **Condividi**.
3. Fare clic su **Copia** nella finestra.
4. Incollare l'URL in un messaggio di posta elettronica per condividere l'applicazione.  

> [!TIP]  
>  Per creare un collegamento in un messaggio di posta elettronica di Outlook, premere **CTRL** + **K** e quindi incollare l'URL.  
>  
> Per impostazione predefinita, Outlook visualizza un avviso di sicurezza per il protocollo Software Center quando il destinatario fa clic sul collegamento. Evitare questo problema nel proprio ambiente mediante l'aggiunta di una chiave di protocollo attendibile al registro. Ad esempio: `HKCU\Software\Policies\Microsoft\Office\16.0\Common\Security\Trusted Protocols\All Applications\softwarecenter:`  
