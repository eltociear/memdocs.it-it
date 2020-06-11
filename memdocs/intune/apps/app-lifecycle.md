---
title: Panoramica del ciclo di vita dell'app per Microsoft Intune
description: Informazioni sul ciclo di vita delle app gestite in Microsoft Intune. Il ciclo di vita delle app include l'aggiunta, la distribuzione, la configurazione, la protezione e il ritiro delle app.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/03/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 60347012-bc3f-4b9a-a4f4-6d3c5021a6e6
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: apps; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8605b33d8fb83fb4537182127860f0cbb098e620
ms.sourcegitcommit: 92e6d2899b1cf986c29c532d0cd0555cad32bc0c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84428604"
---
# <a name="overview-of-the-app-lifecycle-in-microsoft-intune"></a>Panoramica del ciclo di vita dell'app in Microsoft Intune

Il ciclo di vita di un'app di Microsoft Intune inizia quando si aggiunge l'app e termina, dopo alcuni passaggi intermedi, quando si rimuove l'app. Grazie alla conoscenza di queste fasi, si avranno a disposizione i dettagli necessari per iniziare a gestire le app in Intune.

![Ciclo di vita delle app: aggiunta, distribuzione, configurazione, protezione e ritiro.](./media/app-lifecycle/app-lifecycle.png "Ciclo di vita delle app in Intune")

## <a name="add"></a>Aggiunta

Il primo passaggio della distribuzione di app consiste nell'aggiungere a Intune le app da gestire e assegnare. Le procedure di base per i molti tipi di app che possono essere usati sono le stesse. Con Intune è possibile aggiungere diversi tipi di app, incluse le app sviluppate internamente (line-of-business), le app dello Store, le app predefinite e le app sul Web. Per altre informazioni sui ogni tipo di app, vedere [Come aggiungere un'app a Microsoft Intune](apps-add.md).

## <a name="deploy"></a>Distribuisci

Dopo aver aggiunto l'app a Intune è possibile [assegnarla agli utenti e ai dispositivi gestiti](apps-deploy.md). Intune semplifica questo processo e, dopo la distribuzione dell'app, consente di [monitorare il risultato](apps-monitor.md) da Intune nel portale di Azure. In alcuni App Store, ad esempio quelli di [Apple](vpp-apps-ios.md) e [Windows](windows-store-for-business.md), è anche possibile acquistare licenze di app in blocco per l'azienda. Intune consente di sincronizzare i dati con gli App Store per distribuire e monitorare l'uso delle licenze per determinati tipi di app direttamente dalla console di amministrazione di Intune.

## <a name="configure"></a>Configura

Come parte del ciclo di vita, vengono rilasciate regolarmente nuove versioni delle app. Intune offre strumenti con cui è possibile [aggiornare facilmente le app](apps-add.md) distribuite a una versione più recente. Alcune app consentono anche di configurare funzionalità aggiuntive, ad esempio:

- I [criteri di configurazione delle app iOS/iPadOS](app-configuration-policies-use-ios.md) applicano le impostazioni per le app iOS/iPadOS compatibili usate quando si esegue l'app. Ad esempio, un'app può richiedere impostazioni di personalizzazione specifiche o il nome di un server a cui deve connettersi.
- I [criteri di Managed Browser](app-configuration-managed-browser.md) consentono di configurare le impostazioni per [Microsoft Edge](apps-supported-intune-apps.md#microsoft-apps) che sostituisce il browser predefinito del dispositivo e consente di limitare i siti Web che gli utenti possono visitare.

## <a name="protect"></a>Protezione

Intune offre molti modi per proteggere i dati nelle app. I metodi principali sono:

- L'[accesso condizionale](../protect/conditional-access.md), che controlla l'accesso alla posta elettronica e agli altri servizi in base alle condizioni specificate. Le condizioni includono i tipi di dispositivo o la conformità con un [criterio di conformità del dispositivo](../protect/device-compliance-get-started.md) che è stato distribuito.
- I [criteri di protezione delle app](app-protection-policy.md) funzionano con singole app e consentono di proteggere i dati aziendali che usano. Ad esempio, è possibile limitare la copia dei dati tra app non gestite e app gestite dall'utente oppure impedire l'esecuzione delle app su dispositivi jailbroken o rooted.

## <a name="retire"></a>Ritiro

È probabile che le app distribuite a un certo punto diventino obsolete e vadano rimosse. Intune semplifica la disinstallazione delle app. Per altre informazioni, vedere [Disinstallare un'app](../apps/apps-add.md#uninstall-an-app).

## <a name="next-steps"></a>Passaggi successivi

- Informazioni sulla [gestione delle app in Microsoft Intune](app-management.md)
