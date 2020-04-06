---
title: Funzionalità e impostazioni dei dispositivi in Microsoft Intune - Azure | Microsoft Docs
description: Panoramica dei diversi profili di dispositivo di Microsoft Intune. Informazioni su funzionalità, restrizioni, posta elettronica, WiFi, VPN, formazione, certificati, aggiornamento a Windows 10, BitLocker e Microsoft Defender, Windows Information Protection, modelli amministrativi e impostazioni di configurazione del dispositivo personalizzate nell'interfaccia di amministrazione di Microsoft Endpoint Manager. Usare questi profili per proteggere i dati e i dispositivi aziendali.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/26/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: mikedano
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 386e59fe3a7156a8bb74ed39a1b2fcad6ad91dad
ms.sourcegitcommit: 7687cf8fdecd225216f58b8113ad07a24e43d4a3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2020
ms.locfileid: "80359312"
---
# <a name="apply-features-and-settings-on-your-devices-using-device-profiles-in-microsoft-intune"></a>Applicare funzionalità e impostazioni nei dispositivi usando i profili dei dispositivi in Microsoft Intune

Microsoft Intune include impostazioni e funzionalità che è possibile abilitare o disabilitare in dispositivi diversi all'interno dell'organizzazione. Queste impostazioni e funzionalità vengono aggiunte ai "profili di configurazione". È possibile creare profili per dispositivi diversi e piattaforme diverse, tra cui iOS/iPadOS, Amministratore di dispositivi Android, Android Enterprise e Windows. Usare quindi Intune per applicare o "assegnare" il profilo ai dispositivi.

Nell'ambito della soluzione di gestione di dispositivi mobili (MDM), usare questi profili di configurazione per completare diverse attività. Di seguito sono riportati alcuni esempi di profili:

- Nei dispositivi Windows 10 usare un modello di profilo che blocca i controlli ActiveX in Internet Explorer.
- Nei dispositivi iOS/iPadOS e macOS consentire agli utenti di usare stampanti AirPrint nell'organizzazione.
- Consentire o impedire l'accesso al Bluetooth nel dispositivo.
- Creare un profilo Wi-Fi o VPN che consente a dispositivi diversi l'accesso alla rete aziendale.
- Gestire gli aggiornamenti software, incluso quando installarli.
- Eseguire un dispositivo Android come dispositivo in modalità tutto schermo dedicato che può eseguire una o più app.

Questo articolo offre una panoramica dei diversi tipi di profili che è possibile creare. Usare questi profili per autorizzare o bloccare determinate funzionalità nei dispositivi.

## <a name="administrative-templates"></a>Modelli amministrativi

La funzionalità [Modelli amministrativi](administrative-templates-windows.md) include centinaia di impostazioni che è possibile configurare per Internet Explorer, OneDrive, Desktop remoto, Word, Excel e altre applicazioni di Office.

Questi modelli offrono agli amministratori una visualizzazione semplificata delle impostazioni, simile a quella dei criteri di gruppo ma completamente basata sul cloud.

Questa funzionalità supporta:

- Windows 10 e versioni successive

## <a name="certificates"></a>Certificati

Vengono configurati [certificati](../protect/certificates-configure.md) attendibili SCEP e PKCS che vengono assegnati ai dispositivi. Questi certificati autenticano i profili Wi-Fi, VPN e di posta elettronica.

Questa funzionalità supporta:

- Amministratore dispositivo Android
- Android Enterprise
- iOS/iPadOS
- macOS
- Windows Phone 8.1
- Windows 8.1
- Windows 10 e versioni successive

## <a name="custom-profile"></a>Profilo personalizzato

Le [impostazioni personalizzate](custom-settings-configure.md) consentono agli amministratori di assegnare impostazioni dei dispositivi non incluse in Intune. Nei dispositivi Android è possibile immettere valori OMA-URI. Per i dispositivi iOS/iPadOS è possibile importare un file di configurazione creato in Apple Configurator.

Questa funzionalità supporta:

- Amministratore dispositivo Android
- Android Enterprise
- iOS/iPadOS
- macOS
- Windows Phone 8.1

## <a name="delivery-optimization"></a>Ottimizzazione recapito

[Ottimizzazione recapito](delivery-optimization-windows.md) offre un'esperienza migliore per il recapito degli aggiornamenti software. Queste impostazioni sostituiscono le impostazioni **Aggiornamenti software** > **Anelli di aggiornamento di Windows 10**.

Usare queste impostazioni per controllare la modalità di download degli aggiornamenti software nei dispositivi nell'organizzazione. Ad esempio, è possibile consentire agli utenti di gestire in autonomia gli aggiornamenti oppure di ottenere gli aggiornamenti tramite i servizi cloud di ottimizzazione recapito in un profilo di dispositivo.

Questa funzionalità supporta:

- Windows 10 e versioni successive

## <a name="derived-credential"></a>Credenziale derivata

Le [credenziali derivate](../protect/derived-credentials.md) sono certificati su smart card che consentono di eseguire l'autenticazione, la firma e la crittografia. In Intune è possibile creare profili con queste credenziali da usare per app, profili di posta elettronica, connessione a VPN, S/MIME e Wi-Fi.

Questa funzionalità supporta:

- Android Enterprise
- iOS/iPadOS

## <a name="device-features"></a>Funzionalità del dispositivo

[Funzionalità del dispositivo](device-features-configure.md) consente di gestire le funzionalità dei dispositivi iOS/iPadOS e macOS, come AirPrint, le notifiche e i messaggi della schermata di blocco.

Questa funzionalità supporta:

- iOS/iPadOS
- macOS

## <a name="device-firmware-configuration-interface"></a>Interfaccia di configurazione del firmware del dispositivo

L'[interfaccia di configurazione del firmware del dispositivo](device-firmware-configuration-interface-windows.md) (DFCI) consente agli amministratori di abilitare o disabilitare le impostazioni UEFI (BIOS) con Intune. Usare queste impostazioni per migliorare la sicurezza a livello di firmware, che in genere è più resiliente agli attacchi dannosi.

Questa funzionalità supporta:

- Windows 10 1809 e versioni successive nel firmware supportato

## <a name="device-restrictions"></a>Limitazioni del dispositivo

[Limitazioni del dispositivo](device-restrictions-configure.md) consente di gestire la protezione, l'hardware, la condivisione dei dati e altre impostazioni nei dispositivi. Ad esempio è possibile creare un profilo di limitazioni del dispositivo che impedisce agli utenti di dispositivi iOS/iPadOS di usare la fotocamera. 

Questa funzionalità supporta:

- Amministratore dispositivo Android
- Android Enterprise
- iOS/iPadOS
- macOS
- Windows 10 e versioni successive
- Windows 10 Team

## <a name="domain-join"></a>Aggiunta a un dominio

[Aggiunta a un dominio](domain-join-configure.md) configura le informazioni sul dominio di Active Directory locale. Queste informazioni vengono distribuite ai dispositivi aggiunti ad Azure AD ibridi quando ne viene effettuato il provisioning con Windows Autopilot e Intune. Questo profilo indica ai dispositivi il dominio e l'unità organizzativa per l'aggiunta.

Questa funzionalità supporta:

- Windows 10 e versioni successive

## <a name="edition-upgrade"></a>Aggiornamento dell'edizione

[Aggiornamento edizione di Windows 10](edition-upgrade-configure-windows-10.md) consente di aggiornare automaticamente i dispositivi che eseguono determinate versioni di Windows 10 a un'edizione più recente.

Questa funzionalità supporta:

- Windows 10 e versioni successive

## <a name="education"></a>Education

Le [impostazioni di Education - Windows 10](education-settings-configure.md) consentono di configurare le opzioni per l'[app Test ed esami di Windows](https://docs.microsoft.com/education/windows/take-tests-in-windows-10). Quando si configurano queste opzioni, nessun'altra app può essere eseguita sul dispositivo finché il test non è completato.

Le [impostazioni di Education - iOS/iPadOS](../fundamentals/education-settings-configure-ios-shared.md) usano l'app Classroom iOS/iPadOS, progettata per gestire l'insegnamento e controllare i dispositivi degli studenti in aula. È possibile configurare i dispositivi iPad in modo che molti studenti possano condividere un unico dispositivo.

## <a name="email"></a>Posta elettronica

Il profilo [Impostazioni di posta elettronica](email-settings-configure.md) consente di creare, assegnare e gestire le impostazioni di posta elettronica di Exchange ActiveSync nei dispositivi. I profili di posta elettronica garantiscono coerenza e consentono di ridurre le chiamate al supporto. Grazie ad essi gli utenti finali possono accedere alla posta elettronica aziendale dai dispositivi personali senza alcuna configurazione manuale. 

Questa funzionalità supporta:

- Amministratore dispositivo Android
- Android Enterprise
- iOS/iPadOS
- Windows Phone 8.1
- Windows 10 e versioni successive

## <a name="endpoint-protection"></a>Protezione degli endpoint

[Endpoint Protection](../protect/endpoint-protection-configure.md) configura le impostazioni di BitLocker e Microsoft Defender per i dispositivi Windows 10. Configurare quindi il firewall, il gateway e altre risorse nei dispositivi macOS.

Per l'onboarding di Microsoft Defender Advanced Threat Protection (MDATP) in Microsoft Intune, vedere [Configure endpoints using Mobile Device Management (MDM) tools](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints-mdm) (Configurare endpoint con gli strumenti di gestione dei dispositivi mobili).

Questa funzionalità supporta:

- macOS
- Windows 10 e versioni successive

## <a name="esim-cellular---public-preview"></a>Cellulare eSIM - Anteprima pubblica

La funzionalità [Profili cellulare eSIM](esim-device-configuration.md) consente agli amministratori di configurare piani di rete dati nei dispositivi gestiti, per l'accesso a Internet e ai dati. Dopo aver ottenuto i codici di attivazione dall'operatore di telefonia mobile, usare Intune per importare questi codici di attivazione e quindi assegnarli ai dispositivi che supportano eSIM.

Questa funzionalità supporta:

- Windows 10 Fall Creators Update e versioni successive

## <a name="extensions"></a>Estensioni

Le [estensioni del kernel](kernel-extensions-overview-macos.md) consentono agli amministratori di aggiungere funzionalità o programmi a livello di kernel nei dispositivi macOS. Configurare queste impostazioni in modo da considerare attendibili tutte le estensioni di uno sviluppatore o un partner specifico oppure in modo da consentire estensioni del kernel specifiche.

Questa funzionalità supporta:

- macOS

## <a name="identity-protection"></a>Protezione dell'identità

[La protezione dell'identità](../protect/identity-protection-configure.md) controlla l'esperienza Windows Hello for Business nei dispositivi Windows 10 e Windows 10 Mobile. Configurare queste impostazioni per rendere Windows Hello for Business disponibile per gli utenti e i dispositivi e per specificare i requisiti per i pin e i gesti dispositivo.  

Questa funzionalità supporta:  

- Windows 10 e versioni successive
- Windows Holographic for Business  

## <a name="kiosk"></a>Modalità tutto schermo

Il profilo delle [impostazioni della modalità tutto schermo](kiosk-settings.md) consente di configurare un dispositivo per l'esecuzione di una singola app o di molte app. È anche possibile personalizzare altre funzionalità sulla modalità tutto schermo, inclusi un menu di avvio e un Web browser.

Questa funzionalità supporta:

- Windows 10 e versioni successive

Impostazioni per la modalità tutto schermo disponibili anche come restrizioni del dispositivo per [Android](device-restrictions-android.md#kiosk), [Android Enterprise](device-restrictions-android-for-work.md#dedicated-devices) e [iOS/iPadOS](device-restrictions-ios.md#kiosk).

## <a name="microsoft-defender-atp"></a>Microsoft Defender ATP

[Microsoft Defender Advanced Threat Protection (ATP)](../protect/advanced-threat-protection.md) si integra con Intune per monitorare e proteggere i dispositivi. È possibile impostare i livelli di rischio e determinare cosa accade se i dispositivi superano tale livello. In combinazione con l'accesso condizionale, è possibile evitare attività dannose nell'organizzazione.

Questa funzionalità supporta:

- Windows 10 e versioni successive

## <a name="oemconfig"></a>OEMConfig

[OEMConfig](android-oem-configuration-overview.md) è uno standard che consente a OEM (Original Equipment Manufacturer) e EMM (Enterprise Mobility Management) di creare e supportare funzionalità specifiche degli OEM in modo standardizzato nei dispositivi Android Enterprise. Con OEMConfig un OEM crea uno schema che definisce le funzionalità di gestione specifiche dell'OEM e lo incorpora in un'app caricata in Google Play. Intune legge lo schema dall'app e consente agli amministratori di Intune di configurare le impostazioni nello schema.

Questa funzionalità supporta:

- Android Enterprise (OEMConfig)

## <a name="powershell-scripts"></a>Script PowerShell

Gli [script PowerShell nei dispositivi Windows 10](../apps/intune-management-extension.md) usano Intune Management Extension per caricare gli script PowerShell in Intune, quindi eseguono tali script nei dispositivi. L'argomento descrive anche cosa è necessario per usare le estensioni, come aggiungerle a Intune e altre informazioni importanti.

Questa funzionalità supporta:

- Windows 10 e versioni successive
- Windows Holographic for Business

## <a name="preference-file"></a>File delle preferenze

I [file delle preferenze](preference-file-settings-macos.md) nei dispositivi macOS includono informazioni sulle app. Ad esempio, è possibile usare i file delle preferenze per controllare le impostazioni del Web browser, personalizzare le app e altro ancora.

Questa funzionalità supporta:

- macOS

## <a name="shared-multi-user-device"></a>Dispositivo multiutente condiviso

[Windows 10](shared-user-device-settings-windows.md) e [Windows Holographic for Business](shared-user-device-settings-windows-holographic.md) includono le impostazioni per gestire i dispositivi con più utenti, noti anche come dispositivi condivisi o PC condivisi. Quando un utente accede al dispositivo, si sceglie se l'utente può modificare le opzioni di sospensione o salvare i file nel dispositivo. In un altro esempio è possibile creare un criterio che elimina le credenziali inattive dai dispositivi Windows HoloLens per risparmiare spazio.

Queste impostazioni del dispositivo multiutente condiviso consentono agli amministratori di controllare alcune delle funzionalità del dispositivo e di gestire questi dispositivi condivisi con Intune.

Questa funzionalità supporta:

- Windows 10 e versioni successive
- Windows Holographic for Business

## <a name="update-policies"></a>Criteri di aggiornamento

I [criteri di aggiornamento di iOS/iPadOS](../protect/software-updates-ios.md) spiegano come creare e assegnare i criteri di iOS/iPadOS per installare gli aggiornamenti software nei dispositivi iOS/iPadOS. È anche possibile rivedere lo stato dell'installazione.

Per i criteri di aggiornamento nei dispositivi Windows, vedere [Ottimizzazione recapito](delivery-optimization-windows.md). 

Questa funzionalità supporta:

- iOS/iPadOS

## <a name="vpn"></a>Connessione

[Impostazioni VPN](vpn-settings-configure.md) assegna le impostazioni VPN agli utenti e ai dispositivi dell'organizzazione in modo che possano connettersi in modo facile e sicuro alla rete. 

Le reti private virtuali (VPN) offrono agli utenti accesso remoto sicuro alla rete aziendale. I dispositivi usano un profilo di connessione VPN per avviare una connessione con il server VPN. 

Questa funzionalità supporta: 

- Amministratore dispositivo Android
- Android Enterprise
- iOS/iPadOS
- macOS
- Windows Phone 8.1
- Windows 8.1
- Windows 10 e versioni successive

## <a name="wi-fi"></a>Wi-Fi

[Impostazioni Wi-Fi](wi-fi-settings-configure.md) assegna le impostazioni di rete wireless a utenti e dispositivi. Quando si assegna un profilo Wi-Fi, gli utenti dispongono dell'accesso alla rete Wi-Fi aziendale senza doverlo configurare. 

Questa funzionalità supporta: 

- Amministratore dispositivo Android
- Android Enterprise
- iOS/iPadOS
- macOS
- Windows 8.1 (solo importazione)
- Windows 10 e versioni successive

## <a name="zebra-mobility-extensions-mx"></a>Estensioni di mobilità nei dispositivi Zebra

Le [estensioni di mobilità nei dispositivi Zebra](android-zebra-mx-overview.md) consentono agli amministratori di usare e gestire dispositivi Zebra in Intune. Occorre creare profili StageNow con le proprie impostazioni e quindi usare Intune per assegnare e distribuire questi profili ai dispositivi Zebra. L'articolo [Log di StageNow e problemi comuni](android-zebra-mx-logs-troubleshoot.md) è un'ottima risorsa per la risoluzione dei problemi relativi ai profili e per informazioni su alcuni problemi potenziali che possono verificarsi durante l'uso di StageNow.

Questa funzionalità supporta:

- Amministratore di dispositivi Android (Mobility Extensions)

## <a name="manage-and-troubleshoot"></a>Monitorare e risolvere problemi

[Gestire i profili](device-profile-monitor.md) per controllare lo stato dei dispositivi e i profili assegnati. Ciò agevola anche la risoluzione dei conflitti grazie alla visualizzazione delle impostazioni che causano conflitto e dei profili che le contengono. [Problemi e risoluzioni comuni](device-profile-troubleshoot.md) è una risorsa utile per gli amministratori che devono gestire i profili. Descrive cosa accade quando si elimina un profilo, cosa causa l'invio di notifiche ai dispositivi e altro ancora.

## <a name="next-steps"></a>Passaggi successivi

Scegliere la piattaforma e iniziare.
