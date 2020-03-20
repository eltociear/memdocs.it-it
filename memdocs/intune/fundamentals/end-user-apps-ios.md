---
title: Modalità di recupero delle app per gli utenti di iOS/iPadOS
description: Metodi per rendere disponibili le app iOS/iPadOS per gli utenti finali
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 03/11/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 7e3135c1-df26-48c9-aa4c-cdab6168897a
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 957c63c760dcc576ab30bb85440d52833307818d
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79344090"
---
# <a name="how-your-iosipados-users-get-their-apps"></a>Modalità di recupero delle app per gli utenti di iOS/iPadOS

Usare queste informazioni per comprendere come e dove gli utenti possono ottenere le app che vengono distribuite tramite Microsoft Intune.

**App richieste**: app richieste dall'amministratore che vengono installate nel dispositivo con un coinvolgimento minimo dell'utente, a seconda della piattaforma.

**App disponibili**: app che vengono messe a disposizione nell'elenco delle app Portale aziendale e che un utente può scegliere di installare.

**App gestite**: app che possono essere gestite usando i criteri e sono state sottoposte a "wrapping" in Intune o sono state compilate con Intune App Software Development Kit (SDK). Queste app possono essere gestite da Intune ed è possibile applicarvi criteri di protezione delle app.

**App non gestite**: app che gli utenti possono scaricare dall'App Store iOS/iPadOS che non sono integrate con Intune App SDK. Intune non ha alcun controllo sulla distribuzione, sulla gestione o sulla cancellazione selettiva di queste app.  

Gli utenti registrati possono ottenere le app toccando i riquadri seguenti nella schermata App dell'app Portale aziendale:

- Il riquadro **Tutte le app** punta all'elenco di tutte le app nella scheda TUTTE del [sito Web del portale aziendale](https://portal.manage.microsoft.com).

- Dal riquadro **App in evidenza** gli utenti vengono indirizzati alla scheda IN EVIDENZA del sito Web del portale aziendale.

- Il riquadro **Categorie** punta alla scheda CATEGORIE del sito Web del portale aziendale.

![Schermata delle app nel portale aziendale iOS](./media/end-user-apps-ios/ios-cp-app-main-apps-screen.png)

Per informazioni su come aggiungere app, vedere [Come aggiungere un'app a Microsoft Intune](../apps/apps-add.md).

## <a name="app-management-takeover"></a>Acquisizione della gestione delle app
Se un'app è già installata in un dispositivo dell'utente finale, nel dispositivo iOS/iPadOS viene visualizzato un avviso per consentire la gestione dell'app da parte dell'organizzazione. L'utente finale deve consentire all'organizzazione di occuparsi della gestione dell'app prima che le configurazioni dell'app possano essere applicate a un dispositivo gestito. Se l'utente annulla l'avviso, questo verrà comunque visualizzato periodicamente per tutto il tempo in cui il dispositivo è gestito e l'app assegnata.  


![Immagine dell'avviso di modifica della gestione dell'app, con le opzioni Annulla e Gestisci.](./media/end-user-apps-ios/intune-app-management-confirmation-2002.png)

## <a name="see-also"></a>Vedere anche  

[Modalità di recupero delle app per gli utenti di Android](end-user-apps-android.md)

[Modalità di recupero delle app per gli utenti di Windows](end-user-apps-windows.md)
