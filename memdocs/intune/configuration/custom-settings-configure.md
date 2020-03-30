---
title: Usare dispositivi personalizzati in Microsoft Intune - Azure | Microsoft Docs
description: Aggiungere o creare un profilo per usare le impostazioni personalizzate per i dispositivi Windows Phone, Windows 8.1, Windows 10 e versioni successive, amministratore di dispositivi Android, Android Enterprise, macOS e iOS/iPadOS tramite Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/18/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6122f4624cc40152184c1c460afa6a7a39976063
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/21/2020
ms.locfileid: "80083997"
---
# <a name="create-a-profile-with-custom-settings-in-intune"></a>Creare un profilo con impostazioni personalizzate in Intune

Microsoft Intune include molte impostazioni predefinite per controllare diverse funzionalità in un dispositivo. È anche possibile creare profili personalizzati in modo simile ai profili predefiniti. I profili personalizzati sono particolarmente utili quando si vuole usare impostazioni del dispositivo e funzionalità non incluse in Intune. Questi profili includono funzionalità e impostazioni che è possibile controllare nei dispositivi dell'organizzazione. Ad esempio, è possibile creare un profilo personalizzato che imposta la stessa funzionalità per tutti i dispositivi iOS/iPadOS.

Le impostazioni personalizzate sono configurate in modo diverso per ogni piattaforma. Ad esempio, per controllare le funzionalità nei dispositivi Android e Windows, è possibile specificare valori Open Mobile Alliance Uniform Resource Identifier (URI OMA). Per i dispositivi Apple è possibile importare un file creato con [Apple Configurator](https://itunes.apple.com/us/app/apple-configurator-2/id1037126344?mt=12) o [Apple Profile Manager](https://support.apple.com/profile-manager).

Per altre informazioni sui profili di configurazione, vedere [Informazioni sui profili di dispositivo in Microsoft Intune](device-profiles.md).

Questo articolo illustra come creare un profilo personalizzato per l'amministratore di dispositivi Android, Android Enterprise, iOS/iPados, macOS e Windows. È anche possibile visualizzare tutte le impostazioni disponibili per le varie piattaforme.

## <a name="create-the-profile"></a>Creare il profilo

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selezionare **Dispositivi** > **Profili di configurazione** > **Crea profilo**.
3. Immettere le proprietà seguenti:

    - **Nome**: immettere un nome descrittivo per il criterio. Assegnare ai criteri nomi che possano essere identificati facilmente in un secondo momento. Ad esempio, un nome di criterio valido è **Windows 10: Profilo personalizzato che abilita l'URI OMA AllowVPNOverCellular personalizzato**.
    - **Descrizione**: Immettere una descrizione del profilo. Questa impostazione è facoltativa ma consigliata.
    - **Piattaforma**: Selezionare la piattaforma dei dispositivi. Le opzioni disponibili sono:

      - **Amministratore di dispositivi Android**
      - **Android Enterprise**
      - **iOS/iPadOS**
      - **macOS**
      - **Windows 10 e versioni successive**
      - **Windows 8.1 e versioni successive**

    - **Tipo di profilo**: Selezionare **Personalizzato**.

4. Le impostazioni sono diverse per ogni piattaforma. Per visualizzare le impostazioni per una piattaforma specifica, selezionare la piattaforma:

    - [Amministratore di dispositivi Android](custom-settings-android.md)
    - [Android Enterprise](custom-settings-android-for-work.md)
    - [iOS/iPadOS](custom-settings-ios.md)
    - [macOS](custom-settings-macos.md)
    - [Windows 10](custom-settings-windows-10.md)
    - [Windows Holographic for Business](custom-settings-windows-holographic.md)
    - [Windows Phone 8.1](custom-settings-windows-phone-8-1.md)

5. Al termine, selezionare **Crea profilo** > **Crea**.

Il profilo viene creato e visualizzato nell'elenco dei profili (**Configurazione del dispositivo** > **Profili**).

## <a name="next-steps"></a>Passaggi successivi

Dopo averlo creato, il profilo è pronto per l'assegnazione. [Assegnare il profilo](device-profile-assign.md) e [monitorarne lo stato](device-profile-monitor.md).
