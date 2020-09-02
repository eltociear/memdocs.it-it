---
title: Impostazioni per dispositivi Windows Holographic for Business - Microsoft Intune - Azure | Microsoft Docs
description: Conoscere e configurare le impostazioni relative alle restrizioni dei dispositivi in Microsoft Intune per Windows Holographic for Business. Controllare annullamento della registrazione, georilevazione, password, installazione di app dall'App Store, cookie e popup in Microsoft Edge, Microsoft Defender, ricerca, cloud e archiviazione, connettività Bluetooth, orario di sistema e dati di utilizzo.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2cd769b8e3ca4497c095210ea266d225354db24c
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/26/2020
ms.locfileid: "88912832"
---
# <a name="windows-holographic-for-business-device-settings-to-allow-or-restrict-features-using-intune"></a>Impostazioni dei dispositivi Windows Holographic for Business per consentire o limitare l'uso delle funzionalità tramite Intune

Questo articolo descrive le diverse impostazioni che è possibile controllare nei dispositivi Windows Holographic for Business, come Microsoft HoloLens. Usare queste impostazioni nella propria soluzione di gestione di dispositivi mobili (MDM) per abilitare o disabilitare funzionalità, controllare le impostazioni di sicurezza e altro ancora.

Come amministratore di Intune, è possibile creare e assegnare queste impostazioni ai dispositivi.

## <a name="before-you-begin"></a>Prima di iniziare

[Creare un profilo di configurazione delle restrizioni del dispositivo Windows 10](device-restrictions-configure.md#create-the-profile).

Quando si crea un profilo di configurazione delle restrizioni del dispositivo Windows 10, sono disponibili altre impostazioni rispetto a quelle elencate in questo articolo. I dispositivi Windows Holographic for Business supportano le impostazioni indicate in questo articolo.

## <a name="app-store"></a>App Store

- **Aggiorna automaticamente le app dallo Store**: **Blocca** impedisce l'installazione automatica degli aggiornamenti da Microsoft Store. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'aggiornamento automatico delle app installate da Microsoft Store.

  [ApplicationManagement/AllowAppStoreAutoUpdate CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowappstoreautoupdate)

- **Installazione di app attendibile**: scegliere se è possibile installare app non Microsoft Store, operazione nota anche come sideload. Il termine sideload indica l'installazione e poi l'esecuzione e il test di un'app non certificata da Microsoft Store. Ad esempio, un'app interna usata solo dall'azienda. Le opzioni disponibili sono:
  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione.
  - **Blocca**: impedisce il sideload. Non è possibile installare app non Microsoft Store.
  - **Consenti**: consente il sideload. È possibile installare app non Microsoft Store.

  [ApplicationManagement/AllowAllTrustedApps CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowalltrustedapps)

- **Sblocco dallo sviluppatore**: consente agli utenti di modificare le impostazioni per gli sviluppatori Windows, ad esempio consentire il sideload delle app. Le opzioni disponibili sono:
  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione.
  - **Blocca**: impedisce la modalità sviluppatore e il sideload delle app.
  - **Consenti**: consente la modalità sviluppatore e il sideload delle app.

  [ApplicationManagement/AllowDeveloperUnlock CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowdeveloperunlock)

## <a name="cellular-and-connectivity"></a>Rete cellulare e connettività

- **Bluetooth**: **Blocca** impedisce agli utenti di abilitare Bluetooth. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire Bluetooth nel dispositivo.

  [Connectivity/AllowBluetooth CSP](/windows/client-management/mdm/policy-csp-connectivity#connectivity-allowbluetooth)

- **Individuabilità di Bluetooth**: **Blocca** impedisce che il dispositivo sia individuabile da altri dispositivi Bluetooth. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire ad altri dispositivi Bluetooth, ad esempio le cuffie, di individuare il dispositivo.

  [Bluetooth/AllowDiscoverableMode CSP](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowdiscoverablemode)

- **Annunci con Bluetooth**: **Blocca** impedisce al dispositivo di inviare annunci Bluetooth. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire al dispositivo di inviare annunci Bluetooth.

  [Bluetooth/AllowAdvertising CSP](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowadvertising)

## <a name="cloud-and-storage"></a>Cloud e risorse di archiviazione

- **Account Microsoft**: **Blocca** impedisce agli utenti di associare un account Microsoft al dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'aggiunta e l'uso di un account Microsoft.

  [Accounts/AllowMicrosoftAccountConnection CSP](/windows/client-management/mdm/policy-csp-accounts#accounts-allowmicrosoftaccountconnection)

## <a name="control-panel-and-settings"></a>Pannello di controllo e impostazioni

- **Modifica dell'ora di sistema**: **Blocca** impedisce agli utenti di modificare le impostazioni di data e ora nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di modificare queste impostazioni.

  [Settings/AllowDateTime CSP](/windows/client-management/mdm/policy-csp-settings#settings-allowdatetime)

## <a name="general"></a>Generale

- **Annullamento manuale della registrazione**: **Blocca** impedisce agli utenti di eliminare l'account aziendale usando il pannello di controllo dell'area di lavoro nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.

  [Experience/AllowManualMDMUnenrollment CSP](/windows/client-management/mdm/policy-csp-experience#experience-allowmanualmdmunenrollment)

- **Georilevazione**: **Blocca** impedisce agli utenti di attivare servizi di georilevazione nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.

  [Experience/AllowFindMyDevice CSP](/windows/client-management/mdm/policy-csp-experience#experience-allowfindmydevice)

- **Cortana**: **Blocca** disabilita l'assistente vocale Cortana nel dispositivo. Quando Cortana è disattivata, gli utenti possono comunque eseguire una ricerca per trovare elementi nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire Cortana.

  [Experience/AllowCortana CSP](/windows/client-management/mdm/policy-csp-experience#experience-allowcortana)

## <a name="microsoft-edge-browser"></a>Browser Microsoft Edge

- **Esperienza di avvio** > **Consenti popup**: **Sì** (impostazione predefinita) consente i popup nel Web browser. **No** non consente le finestre popup nel browser.

  [Browser/AllowPopups CSP](/windows/client-management/mdm/policy-csp-browser#browser-allowpopups)

- **Preferiti e ricerca** > **Mostra i suggerimenti per la ricerca**: **S**ì (impostazione predefinita) consente al motore di ricerca di suggerire siti durante la digitazione delle frasi di ricerca nella barra degli indirizzi. **No** impedisce questa funzionalità.

  [Browser/AllowSearchSuggestionsinAddressBar CSP](/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar)

- **Privacy e sicurezza** > **Consenti lo strumento per la gestione delle password**: **Sì** (impostazione predefinita) consente a Microsoft Edge di usare automaticamente lo strumento di gestione delle password, che consente agli utenti di salvare e gestire le password nel dispositivo. **No** impedisce l'uso dello strumento di gestione delle password in Microsoft Edge.

  [Browser/AllowPasswordManager CSP](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)

- **Privacy e sicurezza** > **Cookie**: scegliere la modalità di gestione dei cookie nel Web browser. Le opzioni disponibili sono:
  - **Consenti**: i cookie vengono archiviati nel dispositivo.
  - **Blocca tutti i cookie**: i cookie non vengono archiviati nel dispositivo.
  - **Blocca solo i cookie di terze parti**: i cookie di partner o terze parti non vengono archiviati nel dispositivo.

  [Browser/AllowCookies CSP](/windows/client-management/mdm/policy-csp-browser#browser-allowcookies)

- **Privacy e sicurezza** > **Invia intestazioni Do Not Track**: **Sì** invia intestazioni DNT (Do Not Track) ai siti Web che richiedono informazioni di traccia (scelta consigliata). Con l'impostazione **No** (predefinita) non vengono inviate intestazioni che consentono ai siti Web di tenere traccia dell'utente. Gli utenti possono configurare questa impostazione.

  [Browser/AllowDoNotTrack CSP](/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack)

## <a name="microsoft-defender-smartscreen"></a>Microsoft Defender SmartScreen

- **SmartScreen per Microsoft Edge**: **Rendi obbligatorio** attiva Microsoft Defender SmartScreen e impedisce agli utenti di disattivarlo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo può attivare SmartScreen e consentire agli utenti di attivarlo e disattivarlo.

  [Provider di servizi di configurazione Browser/AllowSmartScreen](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)

## <a name="password"></a>Password

- **Password**: **Rendi obbligatorio** richiede agli utenti di immettere una password per accedere al dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'accesso ai dispositivi senza password. Si applica solo agli account locali. Le password dell'account di dominio restano configurate da Active Directory (AD) e Azure AD.

  [DeviceLock/DevicePasswordEnabled CSP](/windows/client-management/mdm/policy-csp-devicelock#devicelock-devicepasswordenabled)

- **Richiedi una password quando il dispositivo torna attivo dopo uno stato di inattività**: **Rendi obbligatorio** richiede agli utenti di immettere una password per sbloccare il dispositivo dopo l'inattività. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe non richiedere un PIN o una password dopo l'inattività.

  [DeviceLock/AllowIdleReturnWithoutPassword CSP](/windows/client-management/mdm/policy-csp-devicelock#devicelock-allowidlereturnwithoutpassword)

## <a name="reporting-and-telemetry"></a>Creazione di report e telemetria

- **Condividi i dati di utilizzo**: scegliere il livello di dati di diagnostica inviati. Le opzioni disponibili sono:

  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione. nessuna impostazione viene imposta. Gli utenti scelgono il livello inviato. Per impostazione predefinita, il sistema operativo potrebbe non condividere i dati.
  - **Sicurezza**: le informazioni necessarie per mantenere più sicuro Windows, inclusi i dati sulle impostazioni del componente Esperienze utente connesse e telemetria, Strumento di rimozione malware e Microsoft Defender
  - **Base**: informazioni di base sul dispositivo, inclusi dati relativi a qualità, compatibilità delle app, utilizzo delle app e i dati dal livello Sicurezza
  - **Avanzato**: informazioni dettagliate aggiuntive, ad esempio come vengono usati Windows, Windows Server, System Center e le app, le relative prestazioni, dati avanzati sull'affidabilità e i dati dei livelli Base e Sicurezza
  - **Completa**: tutti i dati necessari per identificare e contribuire alla risoluzione dei problemi, oltre ai dati dal livello Sicurezza, Base e Avanzato.

  [Provider di servizi di configurazione System/AllowTelemetry](/windows/client-management/mdm/policy-csp-system#system-allowtelemetry)

## <a name="search"></a>Cerca

- **Cerca percorso**: **Blocca** impedisce a Windows Search di usare il percorso. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire questa funzionalità.

  [Search/AllowSearchToUseLocation CSP](/windows/client-management/mdm/policy-csp-search#search-allowsearchtouselocation)

## <a name="next-steps"></a>Passaggi successivi

[Assegnare il profilo](device-profile-assign.md) e [monitorarne lo stato](device-profile-monitor.md).