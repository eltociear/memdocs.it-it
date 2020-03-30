---
title: Che cos'è la registrazione dei dispositivi | Microsoft Docs
description: Informazioni su cosa significa registrare il dispositivo nell'app Portale aziendale e in Microsoft Intune.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 09/13/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 523caa6b-d792-4bb6-bddb-24b2479932d8
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 95f9677b95dc9dde4b12e60e3006b4cee5081471
ms.sourcegitcommit: 670c90a2e2d3106048f53580af76cabf40fd9197
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/25/2020
ms.locfileid: "80233414"
---
# <a name="what-is-device-enrollment"></a>Che cos'è la registrazione dei dispositivi?
Per ottenere l'accesso alle risorse aziendali o dell'istituto di istruzione dal dispositivo, è necessario registrarlo nell'app Portale aziendale Intune o nell'app Microsoft Intune. 

Durante la registrazione del dispositivo:

* Il dispositivo viene registrato nell'organizzazione. Questo passaggio assicura che l'utente sia autorizzato ad accedere alla posta elettronica, alle app e al Wi-Fi dell'organizzazione. 
* I criteri di gestione dei dispositivi dell'organizzazione vengono applicati al dispositivo. I criteri possono includere requisiti per elementi quali crittografia e password dei dispositivi. Lo scopo di questi requisiti è quello di proteggere i dati del dispositivo e dell'organizzazione da accessi non autorizzati.

Una volta aggiornate le impostazioni del dispositivo in modo da soddisfare i requisiti dell'organizzazione, la registrazione è stata completata. È possibile accedere in modo sicuro all'account aziendale o dell'istituto di istruzione pressoché ovunque ci si trovi.  

Questo articolo descrive altri aspetti della registrazione, ad esempio come ottenere le app, i dispositivi supportati e la rimozione o la reimpostazione del dispositivo.  

## <a name="company-portal-and-microsoft-intune-app"></a>App Portale aziendale e Microsoft Intune

Le app Portale aziendale e Microsoft Intune avvisano l'utente delle eventuali modifiche alle impostazioni o ai criteri, in modo che possa intervenire senza perdere l'accesso alle risorse aziendali o dell'istituto di istruzione. 

L'app Portale aziendale mantiene separate le informazioni personali e di lavoro, permettendo di restare produttivi e concentrati. Rende inoltre disponibili le app aziendali e dell'istituto di istruzione, in modo che sia possibile trovare e installare quelle rilevanti per il proprio lavoro.  

### <a name="get-company-portal"></a>Ottenere l'app Portale aziendale

In alcuni casi sarà l'organizzazione a installare l'app Portale aziendale nel dispositivo. L'app è disponibile per l'installazione anche negli App Store, ad esempio Microsoft Store, App Store e Google Play Store. Per accedere all'app da un Web browser, eseguire l'accesso al [sito Web Portale aziendale](https://go.microsoft.com/fwlink/?linkid=2010980) con l'account aziendale o dell'istituto di istruzione.  

### <a name="get-microsoft-intune-app"></a>Ottenere l'app Microsoft Intune

Se è necessario usare l'app Microsoft Intune, l'organizzazione la installerà nel dispositivo.  

## <a name="whats-the-difference-between-the-apps-and-the-website"></a>Qual è la differenza tra app e sito Web?
L'app Portale aziendale è disponibile per i dispositivi Windows 10, iOS, macOS e Android. Si integra perfettamente con la piattaforma del dispositivo. La versione nel sito Web è accessibile da qualsiasi dispositivo e offre la stessa esperienza universale indipendentemente dal dispositivo in uso. 

L'app Microsoft Intune è destinata ai dispositivi Android di proprietà dell'azienda e non ha un sito Web.  

## <a name="what-kind-of-devices-can-you-enroll-with-company-portal"></a>Quali tipi di dispositivi è possibile registrare in Portale aziendale?
In Portale aziendale è possibile registrare i dispositivi seguenti:  

- Dispositivi Windows
  - Windows 10 Mobile
  - Windows 10 Desktop
  - Windows Phone 8.1
  - Windows 8.1
- Dispositivi Apple
    - iOS
    - macOS
- Dispositivi Android


## <a name="what-kind-of-devices-can-you-enroll-with-the-microsoft-intune-app"></a>Quali tipi di dispositivi è possibile registrare nell'app Microsoft Intune?  
È possibile registrare i dispositivi Android di proprietà dell'azienda che l'organizzazione ha configurato per l'uso con l'app. L'app supporta Android 6.0 e versioni successive. 

## <a name="can-you-remove-a-device-from-the-company-portal"></a>È possibile rimuovere un dispositivo dal portale aziendale?
È possibile rimuovere un dispositivo da Portale aziendale. Esiste una differenza tra **rimuovere** e **reimpostare**.

Durante la rimozione, Portale aziendale annulla la registrazione del dispositivo. Il dispositivo perde l'accesso a Portale aziendale. Potrebbero essere rimossi anche i dati aziendali o dell'istituto di istruzione. 

Durante la reimpostazione di un dispositivo, il Portale aziendale tenta di ripristinare le impostazioni predefinite del produttore del computer o del dispositivo stesso. Tutti i dati aziendali o dell'istituto di istruzione e tutti i dati personali vengono rimossi dal dispositivo. Una reimpostazione è utile se, ad esempio, si perde il dispositivo. È possibile reimpostarlo in modalità remota dal sito Web Portale aziendale.  

## <a name="can-you-remove-a-device-from-the-microsoft-intune-app"></a>È possibile rimuovere un dispositivo dall'app Microsoft Intune?
No, non è possibile rimuovere un dispositivo di proprietà dell'azienda dall'app Microsoft Intune.  

## <a name="what-if-i-cant-see-my-device-in-the-company-portal-or-microsoft-intune-app"></a>Cosa fare se il dispositivo non è visibile nell'app Microsoft Intune o Portale aziendale?
Per visualizzare un dispositivo in Portale aziendale, deve prima essere registrato. Se dopo la registrazione non vengono ancora visualizzati tutti i dispositivi, provare a eseguire la sincronizzazione o controllare l'accesso tramite Portale aziendale. Non saranno più visualizzati i dispositivi di proprietà dall'azienda e gestiti da questa.

Nell'app Microsoft Intune viene visualizzato solo il dispositivo attualmente in uso. Altri dispositivi registrati non saranno visibili all'utente nell'app.  

## <a name="where-else-can-i-go-for-help"></a>Dove è possibile trovare altre informazioni?  
Per risolvere i problemi comuni, vedere questi documenti specifici della piattaforma:  

- [Risolvere problemi comuni con il dispositivo Android](check-compliance-on-your-device-android.md)  
- [Risolvere problemi comuni con il dispositivo iOS](troubleshoot-your-device-ios.md)
- [Risolvere problemi comuni con il dispositivo macOS](troubleshoot-your-device-macos.md)
- [Risolvere problemi comuni con il dispositivo Windows](troubleshoot-your-device-windows.md)

È anche possibile contattare il responsabile del supporto IT. Le app Portale aziendale e Microsoft Intune offrono pagine di guida e supporto tecnico con le informazioni di contatto e i modi per segnalare un problema. Le informazioni di contatto sono disponibili anche nel [sito Web Portale aziendale](https://go.microsoft.com/fwlink/?linkid=2010980) dell'organizzazione.  

## <a name="next-steps"></a>Passaggi successivi  

Se si è pronti ad accedere all'account aziendale o dell'istituto di istruzione, seguire le istruzioni della propria organizzazione per la registrazione del dispositivo. È anche possibile trovare istruzioni dettagliate per la registrazione negli articoli seguenti.

* [Registrare il dispositivo Windows 10](enroll-windows-10-device.md)
* [Registrare il dispositivo Android](enroll-device-android-company-portal.md)
* [Eseguire la registrazione con il profilo di lavoro Android](enroll-device-android-work-profile.md)
* [Eseguire la registrazione con l'app Microsoft Intune](enroll-device-android-microsoft-intune-app.md)
* [Registrare il dispositivo iOS](enroll-your-device-in-intune-ios.md)
* [Registrare il dispositivo iOS fornito dall'organizzazione](enroll-your-device-dep-ios.md)
* [Registrare il dispositivo macOS](enroll-your-device-in-intune-macos-cp.md)
* [Registrare il dispositivo macOS fornito dall'organizzazione](enroll-company-device-macos.md)
