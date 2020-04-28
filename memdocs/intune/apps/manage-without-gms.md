---
title: Come usare Intune in ambienti senza i servizi Google Mobile Services
titleSuffix: Microsoft Intune
description: Informazioni su come usare Intune in ambienti senza i servizi Google Mobile Services.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/01/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: priyar
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5aa91a84b2fe5d8870afc93022ab5a468b30e0db
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074793"
---
# <a name="how-to-use-intune-in-environments-without-google-mobile-services"></a>Come usare Intune in ambienti senza i servizi Google Mobile Services

Microsoft Intune usa i servizi Google Mobile Services (GMS) per comunicare con il portale aziendale di Microsoft Intune per la gestione dei dispositivi Android. In alcuni casi, i dispositivi potrebbero non avere accesso ai servizi GMS in modo temporaneo o permanente. È possibile ad esempio che il dispositivo venga fornito senza i servizi GMS oppure si connetta a una rete chiusa in cui i servizi GMS non sono disponibili. Questo documento riepiloga le differenze e le limitazioni che è possibile osservare quando si installa e si usa Intune per gestire i dispositivi Android senza i servizi GMS.

## <a name="install-the-intune-company-portal-app-without-access-to-the-google-play-store"></a>Installare l'app Portale aziendale Intune senza accedere a Google Play Store 

### <a name="for-users-outside-of-mainland-china"></a>Per utenti non residenti in Cina 

Se Google Play non è disponibile, i dispositivi Android possono scaricare il  [Portale aziendale di Microsoft Intune per Android](https://www.microsoft.com/en-us/download/details.aspx?id=49140) e trasferire localmente l'app. Se viene installata in questo modo, l'app non può ricevere automaticamente gli aggiornamenti o le correzioni. È necessario assicurarsi che gli aggiornamenti e le patch siano regolarmente installati nell'app manualmente. 

### <a name="for-users-in-mainland-china"></a>Per gli utenti residenti in Cina 

Poiché Google Play Store non è attualmente disponibile in Cina, i dispositivi Android devono ottenere le app da marketplace di app cinesi. Per altre informazioni, vedere [Installare l'app Portale aziendale in Cina](../user-help/install-company-portal-android-china.md).

## <a name="limitations-of-intune-device-administrator-management-when-gms-is-unavailable"></a>Limitazioni della gestione degli amministratori dei dispositivi di Intune quando i servizi GMS non sono disponibili 

### <a name="unavailable-intune-features"></a>Funzionalità di Intune non disponibili

Alcune funzionalità di Intune si basano su componenti dei servizi GMS, ad esempio Google Play Store o Google Play Services. Poiché questi componenti non sono disponibili in ambienti senza i servizi GMS, le funzionalità seguenti nella console di amministrazione di Intune potrebbero non essere disponibili.  

| Scenario  | Caratteristiche  |
|-----------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Criteri di conformità dei dispositivi  | Quando si creano o si modificano i criteri di conformità per l'amministratore del dispositivo Android, tutte le opzioni visualizzate in **Google Play Protect** non sono disponibili.  |
| Criteri di protezione delle app (avvio condizionale)  | Non è possibile usare le condizioni del dispositivo **Attestazione del dispositivo SafetyNet** e **Rendi obbligatoria l'analisi delle minacce nelle app** per l'avvio condizionale.  |
| App client  | Le app di tipo **Android** non sono disponibili. In alternativa, usare **App line-of-business** per distribuire e gestire le app.  |
| Mobile Threat Defense  | Contattare il fornitore MTD per scoprire se la soluzione è integrata con Intune, se è disponibile nell'area di interesse e se si basa sui servizi GMS.  |

### <a name="some-tasks-may-be-delayed"></a>Alcune attività potrebbero essere ritardate 

Negli ambienti in cui sono disponibili i servizi GMS, Intune si basa sulle notifiche push per velocizzare il completamento delle attività. Ad esempio, se si tenta di cancellare in remoto il dispositivo, le notifiche vengono in genere inviate al dispositivo in pochi secondi. Se i servizi GMS non sono disponibili, è possibile che anche le notifiche push non siano disponibili. Di conseguenza, Intune dovrà attendere il completamento della successiva sincronizzazione del dispositivo per completare le attività.  

I dispositivi Android registrati comunicano con Intune ogni 8 ore. Ad esempio, se un dispositivo comunica con Intune alle 13:00 e le attività remote vengono inviate alle 13:05, Intune contatterà il dispositivo alle 21:00 per completare le attività. 

Per completare le attività seguenti possono essere necessarie fino a 8 ore: 

**Console di Intune**:
- Cancellazione completa
- Cancellazione selettiva
- Distribuzioni di app nuove o aggiornate
- Blocco remoto
- Reimpostazione del passcode

**App Portale aziendale Intune per Android**:
- Rimozione del dispositivo remoto
- Reimpostazione del dispositivo
- Installazione delle app line-of-business disponibili

**Sito Web del portale aziendale di Intune**:
- Rimozione del dispositivo (locale e remoto)
- Reimpostazione del dispositivo
- Reimpostazione del passcode del dispositivo

Se il dispositivo è stato registrato di recente, la sincronizzazione della conformità, della non conformità e della configurazione viene eseguita con maggiore frequenza. Per altre informazioni sulle sincronizzazioni dei dispositivi, vedere [Domande e problemi comuni e soluzioni per i criteri e i profili dei dispositivi in Microsoft Intune](../configuration/device-profile-troubleshoot.md). 

## <a name="next-steps"></a>Passaggi successivi

- [Assegnare app ai gruppi con Microsoft Intune](../apps/apps-deploy.md)
