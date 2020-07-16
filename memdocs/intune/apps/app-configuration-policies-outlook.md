---
title: Gestire Outlook per iOS e Android con Intune
description: Usare i criteri di protezione e di configurazione delle app di Intune con Outlook per iOS e Android per garantire che l'accesso alle esperienze di collaborazione in team venga sempre eseguito con misure di sicurezza applicate.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/11/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: smithre4
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3db207e4c1c75706c1f54762bf74c1757d342ac1
ms.sourcegitcommit: c7afcc3a2232573091c8f36d295a803595708b6c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84973044"
---
# <a name="manage-messaging-collaboration-access-by-using-outlook-for-ios-and-android-with-microsoft-intune"></a>Gestire l'accesso alla collaborazione tramite messaggistica usando Outlook per iOS e Android con Microsoft Intune

L'app Outlook per iOS e Android è progettata per consentire agli utenti dell'organizzazione di essere più efficienti con i propri dispositivi mobili, riunendo posta elettronica, calendario, contatti e altri file.

Le funzionalità di protezione più complete e più ampie per i dati di Office 365 sono disponibili con l'abbonamento alla suite Enterprise Mobility + Security, che include funzionalità di Microsoft Intune e Azure Active Directory Premium, come l'accesso condizionale. Come minimo, è consigliabile distribuire criteri di accesso condizionale che consentono di connettersi a Outlook per iOS e Android solo dai dispositivi mobili e criteri di protezione delle app di Intune che garantiscono la protezione dell'esperienza di collaborazione.

## <a name="apply-conditional-access"></a>Applicare l'accesso condizionale
Le organizzazioni possono usare i criteri di accesso condizionale di Azure AD per assicurarsi che gli utenti possano accedere solo ai contenuti aziendali o dell'istituto di istruzione usando Outlook per iOS e Android. A tale scopo, è necessario disporre di criteri di accesso condizionale destinati a tutti i potenziali utenti. Per informazioni dettagliate sulla creazione di questi criteri, vedere [Richiedere i criteri di protezione delle app per l'accesso alle app cloud con accesso condizionale](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access).

1. Seguire "Passaggio 1: configurare criteri di accesso condizionale di Azure AD per Office 365"in [Scenario 1: Le app di Office 365 richiedono app approvate con criteri di protezione delle app](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access#scenario-1-office-365-apps-require-approved-apps-with-app-protection-policies), che consente Outlook per iOS e Android, ma blocca la connessione a Exchange Online dai client Exchange ActiveSync compatibili con OAuth.

   > [!NOTE]
   > Questo criterio garantisce che gli utenti di dispositivi mobili possano accedere a tutti gli endpoint di Office usando le app applicabili.

2. Seguire "Passaggio 2: configurare criteri di accesso condizionale di Azure AD per Exchange Online con Active Sync (EAS)" in [Scenario 1: Le app di Office 365 richiedono app approvate con criteri di protezione delle app](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access#scenario-1-office-365-apps-require-approved-apps-with-app-protection-policies), che impedisce ai client di Exchange ActiveSync che usano l'autenticazione di base di connettersi a Exchange Online.

   I criteri precedenti sfruttano il controllo di concessione [Richiedi criteri di protezione dell'app](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-technical-reference), assicurando che un criterio di Protezione app di Intune venga applicato all'account associato in Outlook per iOS e Android prima di concedere l'accesso. Se l'utente non è assegnato a un criterio di Protezione app di Intune, non ha una licenza per Intune o l'app non è inclusa nel criterio Protezione app di Intune, il criterio impedisce all'utente di ottenere un token di accesso e di accedere ai dati di messaggistica.

3. Infine, seguire [Procedura: Bloccare l'autenticazione legacy ad Azure AD con l'accesso condizionale](https://docs.microsoft.com/azure/active-directory/conditional-access/block-legacy-authentication) per bloccare l'autenticazione legacy per altri protocolli di Exchange su dispositivi iOS e Android. Questo criterio deve essere destinato solo all'app cloud Office 365 Exchange Online e alle piattaforme per dispositivi iOS e Android. Ciò garantisce che le app per dispositivi mobili che usano i protocolli Servizi Web di Exchange, IMAP4 o POP3 con l'autenticazione di base non possano connettersi a Exchange Online.

## <a name="create-intune-app-protection-policies"></a>Creare criteri di protezione delle app di Intune

I criteri di protezione delle app definiscono quali app sono consentite e le azioni che queste possono eseguire con i dati dell'organizzazione. Le scelte disponibili sull'APP consentono alle organizzazioni di adattare la protezione alle loro esigenze specifiche. Per alcuni utenti potrebbe non essere semplice individuare le impostazioni dei criteri necessarie per implementare uno scenario completo. Per aiutare le organizzazioni a dare la priorità alla protezione avanzata degli endpoint di client mobili, Microsoft ha introdotto la tassonomia per il framework di protezione dei dati dell'APP per la gestione di dispositivi mobili iOS e Android.

Il framework di protezione dei dati dell'APP è organizzato in tre livelli di configurazione distinti, ognuno dei quali si basa sul livello precedente:

- **Protezione di base dei dati aziendali** (livello 1) garantisce che le app siano protette con un PIN e crittografate ed esegue operazioni di cancellazione selettiva. Per i dispositivi Android questo livello convalida l'attestazione dei dispositivi Android. Si tratta di una configurazione a livello di voce che offre un controllo simile di protezione dei dati nei criteri della cassetta postale di Exchange Online e introduce l'IT e la popolazione di utente nell'APP.
- **Protezione avanzata dei dati aziendali** (livello 2) introduce i meccanismi di protezione della perdita dei dati aziendali dell'APP e i requisiti minimi del sistema operativo. Questa configurazione è applicabile alla maggior parte degli utenti di dispositivi mobili che accedono ai dati aziendali o dell'istituto di istruzione.
- **Protezione elevata dei dati aziendali** (livello 3) introduce meccanismi avanzati per la protezione dei dati, configurazione del PIN avanzata e Mobile Threat Defense dell'APP. Questa configurazione è utile per gli utenti che accedono a dati ad alto rischio.

Per visualizzare le raccomandazioni specifiche per ogni livello di configurazione e le app minime che devono essere protette, consultare il [Framework di protezione dei dati con criteri di protezione delle app](app-protection-framework.md).

Indipendentemente dal fatto che il dispositivo sia registrato in una soluzione di gestione unificata degli endpoint (UEM), è necessario creare un criterio di protezione delle app di Intune per le app iOS e Android, seguendo la procedura descritta in [Come creare e assegnare criteri di protezione delle app](app-protection-policies.md). Questi criteri, come minimo, devono soddisfare le condizioni seguenti:

1. Sono incluse tutte le app Microsoft 365 per dispositivi mobili, ad esempio Microsoft Edge, Outlook, OneDrive, Office o Teams, in modo da garantire che gli utenti possano accedere e modificare i dati aziendali o dell'istituto di istruzione in qualsiasi app Microsoft in modo sicuro.

2. Sono assegnati a tutti gli utenti. Ciò garantisce che tutti gli utenti siano protetti, indipendentemente dal fatto che usino Outlook per iOS o Android.

3. Determinare il livello di framework che soddisfa i requisiti. La maggior parte delle organizzazioni deve implementare le impostazioni definite in **Protezione avanzata dei dati aziendali** (livello 2), in quanto consente di controllare i requisiti di protezione e accesso ai dati.

Per altre informazioni sulle impostazione disponibili, vedere gli articoli [Impostazioni dei criteri di protezione delle app di Android](app-protection-policy-settings-android.md) e [Impostazioni dei criteri di protezione delle app per iOS](app-protection-policy-settings-ios.md).

> [!IMPORTANT]
> Per applicare i criteri di protezione delle app di Intune alle app nei dispositivi Android che non sono registrati in Intune, l'utente deve anche installare il Portale aziendale Intune. Per altre informazioni, consultare l'articolo [Aspettative relative alla gestione dell'app per Android con criteri di protezione delle app](../fundamentals/end-user-mam-apps-android.md).

## <a name="utilize-app-configuration"></a>Utilizzare la configurazione delle app

Outlook per iOS e Android supporta le impostazioni dell'app che consentono agli amministratori della gestione unificata degli endpoint, ad esempio Microsoft Endpoint Manager, di personalizzare il comportamento dell'app.

La configurazione dell'app può essere eseguita tramite il canale di gestione di dispositivi mobili (MDM) del sistema operativo sui dispositivi registrati (canale [Configurazione delle app gestite](https://developer.apple.com/library/content/samplecode/sc2279/Introduction/Intro.html) per iOS o [Android nel canale Enterprise](https://developer.android.com/work/managed-configurations) per Android) o tramite il canale Criteri di protezione delle app (APP) di Intune. Outlook per iOS e Android supporta gli scenari di configurazione seguenti:

- Ammettere solo account aziendali o di un istituto di istruzione
- Impostazioni generali di configurazione delle app
- Impostazioni S/MIME
- Impostazioni di protezione dati

Per procedure specifiche e documentazione dettagliata sulle impostazioni di configurazione delle app supportate da Outlook per iOS e Android, vedere [Distribuzione di impostazioni di configurazione delle app Outlook per iOS e Android](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune).

## <a name="next-steps"></a>Passaggi successivi

- [Che cosa sono i criteri di protezione delle app?](app-protection-policy.md) 
- [Criteri di configurazione delle app per Microsoft Intune](app-configuration-policies-overview.md)