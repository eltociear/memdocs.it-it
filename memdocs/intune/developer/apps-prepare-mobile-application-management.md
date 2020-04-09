---
title: Preparare le app per la gestione di applicazioni mobili con Microsoft Intune
description: Le informazioni contenute in questo argomento consentono di stabilire quando è necessario usare lo strumento di wrapping delle app e App SDK per abilitare le app line-of-business personalizzate per l'uso dei criteri di gestione delle app mobili.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/02/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 29e22121-8268-48b5-a671-f940a6be1d24
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6a26e32d0a719df7c3982591042991ae760d9281
ms.sourcegitcommit: db511e03f14e6120968b60def8990485eb42529b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/02/2020
ms.locfileid: "80611712"
---
# <a name="prepare-line-of-business-apps-for-app-protection-policies"></a>Preparare le app line-of-business per i criteri di protezione delle app

È possibile consentire alle app di usare i criteri di protezione delle app tramite lo strumento di wrapping delle app di Intune o Intune App SDK. In questo articolo vengono fornite informazioni su questi due metodi e su quando usarli.

## <a name="intune-app-wrapping-tool"></a>Strumento di wrapping delle app di Intune

Lo strumento di wrapping delle app viene usato principalmente per le app line-of-business (LOB) **interne**. Lo strumento è un'applicazione della riga di comando che crea un wrapper per l'app, consentendo quindi all'app di essere gestita da un criterio di protezione delle app di Intune. Quando si protegge un'app fornita da un fornitore di software indipendenti (ISV), è importante chiarire se l'ISV continuerà a supportare l'app con wrapping.

Non è necessario il codice sorgente per usare lo strumento, ma sono necessarie le credenziali di firma. Per altre informazioni sulle credenziali di firma, vedere il [blog di Intune](https://blogs.technet.microsoft.com/enterprisemobility/2015/02/25/how-to-obtain-the-prerequisites-for-the-intune-app-wrapping-tool-for-ios/). Per la documentazione dello strumento di wrapping delle app, vedere [Strumento di wrapping delle app per Android](app-wrapper-prepare-android.md) e [Strumento di wrapping delle app per iOS](app-wrapper-prepare-ios.md).

Lo strumento di wrapping delle app **non** supporta le app nell'App Store Apple o in Google Play Store, né alcune funzionalità che richiedono un'integrazione dello sviluppatore (vedere la tabella di confronto delle funzionalità seguente).

Per altre informazioni sullo strumento di wrapping delle app per i criteri di protezione delle app sui dispositivi non registrati in Intune, vedere [Proteggere app e dati line-of-business su dispositivi non registrati in Microsoft Intune](../apps/apps-add.md).

### <a name="reasons-to-use-the-app-wrapping-tool"></a>Motivi per usare lo strumento di wrapping delle app

* L'app non ha funzionalità per la protezione dei dati incorporate
* L'app è distribuita internamente
* Non si ha accesso al codice sorgente dell'app.
* Non si è lo sviluppatore dell'app
* L'app offre esperienze minime di autenticazione utente

### <a name="supported-app-development-platforms"></a>Piattaforme di sviluppo delle app supportate

|**Strumento di wrapping delle app** | **Xamarin** |**Cordova** |
|------|----|----|
|**iOS** |Sì|Sì|
|**Android**|No: usare i [binding Xamarin per Intune App SDK](app-sdk-xamarin.md).|Sì|

## <a name="intune-app-sdk"></a>Intune App SDK

App SDK è progettato principalmente per i clienti che hanno le app nell'App Store Apple o in Google Play Store e che vogliono poter gestire le app con Intune. Tuttavia, qualsiasi app può sfruttare l'integrazione dell'SDK, anche se si tratta di un'app line-of-business.

Per altre informazioni sull'SDK, vedere la [panoramica](app-sdk.md). Per un'introduzione all'SDK, vedere [Introduzione a Microsoft Intune App SDK](app-sdk-get-started.md)

### <a name="reasons-to-use-the-sdk"></a>Motivi per usare l'SDK

* L'app non ha funzionalità per la protezione dei dati incorporate
* L'app è distribuita a un App Store pubblico, ad esempio Google Play o l'App Store Apple
* Si è uno sviluppatore di app e si ha il background tecnico per l'uso dell'SDK
* L'app ha altre integrazioni dell'SDK
* L'app viene aggiornata di frequente

### <a name="supported-app-development-platforms"></a>Piattaforme di sviluppo delle app supportate

|**Intune App SDK** |**Xamarin** |**Cordova**
|------|----|----|
|**iOS**|Sì: usare i [binding Xamarin per Intune App SDK](app-sdk-xamarin.md).|No|
|**Android**| Sì: usare i [binding Xamarin per Intune App SDK](app-sdk-xamarin.md).|No|

## <a name="not-using-an-app-development-platform-listed-above"></a>Non si usa una di queste piattaforme per lo sviluppo di app?

Il team di sviluppo di Intune SDK verifica e gestisce attivamente il supporto per le app compilate con la piattaforme native Android, iOS (Obj-C, Swift), Xamarin e Xamarin.Forms. Anche se alcuni clienti sono riusciti a integrare Intune SDK con altre piattaforme, ad esempio React Native e NativeScript, Microsoft non offre linee guida o plug-in specifici per gli sviluppatori di app che usano piattaforme diverse da quelle supportate da Microsoft. 

## <a name="feature-comparison"></a>Confronto delle funzionalità

Questa tabella elenca le impostazioni abilitate se un'app usa App SDK o App Wrapping Tool. Alcune funzionalità richiedono agli sviluppatori di app di applicare una logica esterna all'integrazione di base con Intune SDK e, pertanto, non sono abilitate se l'app usa App Wrapping Tool. 

|Funzionalità|App SDK|Strumento di wrapping delle app|
|-----------|---------------------|-----------|
|Limitare il contenuto Web per la visualizzazione in Managed Browser dell'azienda|X|X|
|Impedire backup in Android, iTunes o iCloud|X|X|
|Consenti all'app di trasferire i dati ad altre app|X|X|
|Consenti all'app di ricevere i dati da altre app|X|X|
|Limita le operazioni taglia, copia e incolla con le altre app|X|X|
|Specificare il numero di caratteri che è possibile tagliare o copiare da un'app gestita|X|X|
|Richiedi PIN semplice per l'accesso|X|X|
|Specificare il numero di tentativi prima della reimpostazione del PIN|X|X|
|Consenti impronta digitale anziché PIN|X|X|
|Consenti il riconoscimento facciale invece del PIN (solo iOS)|X|X|
|Richiedi credenziali aziendali per l'accesso|X|X|
|Impostare una scadenza del PIN|X|X|
|Blocca l'esecuzione delle app gestite nei dispositivi jailbroken o rooted|X|X|
|Crittografa dati app|X|X|
|Ricontrollare i requisiti di accesso dopo un numero di minuti specificato|X|X|
|Specificare il periodo di prova offline|X|X|
|Bloccare l'acquisizione schermo (solo Android)|X|X|
|Supportare la gestione delle applicazioni mobili senza registrazione del dispositivo|X|X|
|Cancellazione completa dei dati delle app|X|X|
|Cancellazione selettiva di dati aziendali e dell'istituto di istruzione in scenari con identità multiple <br><br>**Nota:** per iOS/iPadOS, quando viene rimosso il profilo di gestione, viene rimossa anche l'app.|X||
|Impedire "Salva con nome"|X||
|Configurazione dell'applicazione di destinazione (o configurazione dell'app tramite il "canale MAM")|X|X|
|Supportare più identità|X||
|Stile personalizzabile |X|||
|Connessioni VPN dell'applicazione su richiesta con Citrix mVPN|X|X| 
|Disabilita la sincronizzazione dei contatti|X|X|
|Disabilita stampa|X|X|
|Richiedi una versione minima dell'app|X|X|
|Richiedi un sistema operativo minimo|X|X|
|Richiedi una versione minima della patch di protezione Android (solo Android)|X|X|
|Richiedi un Intune SDK minimo per iOS (solo iOS)|X|X|
|Attestazione del dispositivo SafetyNet (solo Android)|X|X|
|Analisi delle minacce nelle app (solo Android)|X|X|
|Richiedere il livello di rischio massimo di Mobile Threat Defense per il dispositivo del fornitore|X||
|Configurare il contenuto delle notifiche dell'app per gli account dell'organizzazione|X|X|
|Richiedere l'uso di tastiere approvate (solo Android)|X|X|
|Richiedere i criteri di protezione dell'app (accesso condizionale)|X||
|Richiedere l'approvazione dell'app client (accesso condizionale)|X||

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui criteri di protezione delle app e Intune, vedere gli argomenti seguenti:

- [Strumento di wrapping delle app per Android](app-wrapper-prepare-android.md)<br>
- [Strumento di wrapping delle app per iOS](app-wrapper-prepare-ios.md)<br>
- [Usare l'SDK per abilitare le app per la gestione delle applicazioni mobili](app-sdk.md)
