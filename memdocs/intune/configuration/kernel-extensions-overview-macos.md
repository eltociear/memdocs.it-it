---
title: Creare un profilo di dispositivo per le estensioni del kernel macOS con Microsoft Intune - Azure | Microsoft Docs
titleSuffix: ''
description: Aggiungere o creare un profilo di dispositivo macOS e quindi configurare le estensioni del kernel per consentire l'override dell'utente, aggiungere l'identificatore del team e un bundle e l'identificatore del team in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/25/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 191b2cdfa8fd99078bccee8edf99eb9b0cb275ee
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79360964"
---
# <a name="add-macos-kernel-extensions-in-intune"></a>Aggiungere le estensioni del kernel macOS in Intune

> [!NOTE]
> Le estensioni del kernel macOS verranno sostituite con estensioni di sistema. Per altre informazioni, vedere [Suggerimento per il supporto: Uso delle estensioni di sistema anziché delle estensioni del kernel per macOS Catalina 10.15 in Intune](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-using-system-extensions-instead-of-kernel-extensions/ba-p/1191413).

Nei dispositivi macOS è possibile aggiungere funzionalità a livello di kernel. Queste funzionalità accedono a parti del sistema operativo a cui i normali programmi non possono accedere. È possibile che l'organizzazione abbia esigenze o requisiti specifici che non sono disponibili in un'app, una funzionalità del dispositivo e così via. 

Per aggiungere estensioni del kernel per cui è sempre consentito il caricamento nei dispositivi, aggiungere "estensioni del kernel" (KEXT) in Microsoft Intune e quindi distribuire tali estensioni nei dispositivi.

Si dispone, ad esempio, di un programma di scansione antivirus che analizza il dispositivo alla ricerca di contenuto dannoso. È possibile aggiungere l'estensione del kernel di questo programma di scansione antivirus come estensione del kernel consentita in Intune. "Assegnare" quindi l'estensione ai dispositivi macOS.

Con questa funzionalità gli amministratori possono consentire agli utenti di eseguire l'override delle estensioni del kernel, aggiungere identificatori del team e aggiungere estensioni del kernel specifiche in Intune.

Questa funzionalità si applica a:

- macOS 10.13.2 e versioni successive

Per usare questa funzionalità, i dispositivi devono essere:

- Registrati in Intune tramite il Device Enrollment Program (DEP) di Apple. In [Registrare automaticamente i dispositivi macOS](../enrollment/device-enrollment-program-enroll-macos.md) sono disponibili altre informazioni.

  OPPURE

- Registrati in Intune con "Registrazione approvata dall'utente" (termine Apple). In [Come prepararsi alle modifiche apportate alle estensioni del kernel in macOS High Sierra](https://support.apple.com/en-us/HT208019) sono disponibili altre informazioni. Si aprirà il sito Web di Apple.

Intune usa "profili di configurazione" per creare e personalizzare queste impostazioni per le esigenze dell'organizzazione. Dopo aver aggiunto queste funzionalità in un profilo, è possibile eseguire il push del profilo o distribuirlo nei dispositivi macOS nell'organizzazione.

Questo articolo illustra come creare un profilo di configurazione del dispositivo usando le estensioni del kernel in Intune.

> [!TIP]
> Per altre informazioni sulle estensioni del kernel, vedere [Panoramica sulle estensioni del kernel](https://developer.apple.com/library/archive/documentation/Darwin/Conceptual/KernelProgramming/Extend/Extend.html). Si aprirà il sito Web di Apple.

## <a name="what-you-need-to-know"></a>Informazioni importanti

- È possibile aggiungere estensioni del kernel legacy non firmate.
- Assicurarsi di immettere l'identificatore del team e l'ID bundle corretti dell'estensione del kernel. Intune non convalida i valori immessi. Se si immettono informazioni errate, l'estensione non funzionerà nel dispositivo. Un identificatore del team è esattamente di 10 caratteri alfanumerici. 

> [!NOTE]
> Apple ha rilasciato informazioni relative alla firma e all'autenticazione per tutto il software. In macOS 10.14.5 e versioni successive le estensioni del kernel distribuite tramite Intune non devono soddisfare i criteri di autenticazione di Apple.
>
> Per informazioni sui criteri di autenticazione e sugli eventuali aggiornamenti o modifiche, vedere le risorse seguenti:
>
> - [Autenticazione dell'app prima della distribuzione](https://developer.apple.com/documentation/security/notarizing_your_app_before_distribution) (si aprirà il sito Web di Apple) 
> - [Come prepararsi alle modifiche apportate alle estensioni del kernel in macOS High Sierra](https://support.apple.com/en-us/HT208019) (si aprirà il sito Web di Apple)

## <a name="create-the-profile"></a>Creare il profilo

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selezionare **Dispositivi** > **Profili di configurazione** > **Crea profilo**.
3. Immettere le proprietà seguenti:

    - **Nome**: immettere un nome descrittivo per il nuovo profilo.
    - **Descrizione**: Immettere una descrizione del profilo. Questa impostazione è facoltativa ma consigliata.
    - **Piattaforma**: Selezionare **macOS**.
    - **Tipo di profilo**: selezionare **Estensioni**.
    - **Settings** (Impostazioni): immettere le impostazioni da configurare. Per un elenco di tutte le impostazioni e delle operazioni corrispondenti, vedere:

        - [macOS](kernel-extensions-settings-macos.md)

4. Al termine, selezionare **OK** > **Crea** per salvare le modifiche.

Il profilo viene creato e visualizzato nell'elenco. Assicurarsi di [assegnare il profilo](device-profile-assign.md) e [monitorarne lo stato](device-profile-monitor.md).

## <a name="next-steps"></a>Passaggi successivi

Dopo averlo creato, il profilo è pronto per l'assegnazione. [Assegnare il profilo](device-profile-assign.md) e [monitorarne lo stato](device-profile-monitor.md).
