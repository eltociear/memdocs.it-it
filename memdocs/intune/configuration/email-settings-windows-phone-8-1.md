---
title: Impostazioni di posta elettronica di Microsoft Intune per Windows Phone 8.1
titleSuffix: ''
description: Informazioni sulle impostazioni di Intune che è possibile usare per configurare le connessioni di posta elettronica nei dispositivi che eseguono Windows Phone 8.1.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 3/19/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 369e856b26ecbf8a7d6d7f8c0a87a9bfdf69e318
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/21/2020
ms.locfileid: "80086921"
---
# <a name="email-profile-settings-in-microsoft-intune-for-devices-running-windows-phone-81"></a>Impostazioni del profilo di posta elettronica in Microsoft Intune per i dispositivi che eseguono Windows Phone 8.1

Questo articolo illustra le impostazioni del profilo di posta elettronica che è possibile configurare per i dispositivi che eseguono Windows Phone 8.1.

>[!IMPORTANT]
>I profili di posta elettronica Windows Phone 8.1 vengono applicati anche ai dispositivi Windows 10.

## <a name="before-you-begin"></a>Prima di iniziare

[Creare un profilo di posta elettronica in Windows Phone 8.1](email-settings-configure.md).

## <a name="email-settings"></a>Impostazioni di posta elettronica

- **Server di posta elettronica**: immettere il nome host del server Exchange dell'azienda. Immettere ad esempio `outlook.office365.com`.
- **Nome account**: immettere il nome visualizzato dell'account di posta elettronica. Questo nome viene visualizzato nel dispositivo degli utenti.
- **Attributo nome utente da AAD**: questo nome è l'attributo che Intune ottiene da Azure Active Directory (AAD). Intune genera in modo dinamico il nome utente usato da questo profilo. Le opzioni disponibili sono:
  - **Nome entità utente**: ottiene il nome, ad esempio `user1` o `user1@contoso.com`.
  - **Indirizzo SMTP primario**: ottiene il nome nel formato dell'indirizzo di posta elettronica, ad esempio `user1@contoso.com`.
  - **Nome account SAM**: richiede il dominio, ad esempio `domain\user1`. Specificare anche:
    - **Origine del nome di dominio utente**: Le opzioni disponibili sono:
      - **AAD** (Azure Active Directory): immettere **Attributo nome di dominio utente da AAD**. Scegliere di ottenere l'attributo **Nome completo** o **Nome NetBIOS** dell'utente.
      - **Personalizzato**: Immettere **Nome di dominio personalizzato da usare**. immettere un valore usato da Intune per il nome di dominio, ad esempio `contoso.com` o `contoso`.

- **Attributo indirizzo di posta elettronica da AAD**: Intune ottiene questo attributo da Azure Active Directory (AAD). scegliere la modalità di generazione dell'indirizzo di posta elettronica per l'utente. Le opzioni disponibili sono:
  - **Nome entità utente**: usa come indirizzo di posta elettronica il nome dell'entità completo, ad esempio `user1@contoso.com` o `user1`.
  - **Indirizzo SMTP primario**: usa l'indirizzo SMTP primario per accedere a Exchange, ad esempio `user1@contoso.com`.

## <a name="security-settings"></a>Impostazioni di sicurezza

- **SSL**: selezionare **Abilita** per usare la comunicazione Secure Sockets Layer (SSL) durante l'invio e la ricezione di messaggi di posta elettronica e durante la comunicazione con il server Exchange. Se si seleziona **Disabilita** non è necessario il protocollo SSL.

## <a name="synchronization-settings"></a>Impostazioni di sincronizzazione

- **Numero di messaggi di posta elettronica da sincronizzare**: selezionare il numero di giorni di posta elettronica da sincronizzare. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Selezionare **Senza limiti** per sincronizzare tutti i messaggi di posta elettronica disponibili.
- **Pianificazione sincronizzazione**: selezionare la pianificazione in base alla quale i dispositivi devono sincronizzare i dati dal server Exchange. È anche possibile selezionare **Quando arrivano i messaggi** in modo che i dati vengano sincronizzati non appena arrivano. In alternativa, selezionare **Manuale** in modo che sia l'utente del dispositivo ad avviare la sincronizzazione.

## <a name="content-sync-settings"></a>Impostazioni di sincronizzazione del contenuto

- **Tipo di contenuto da sincronizzare**: Selezionare i tipi di contenuto da sincronizzare nei dispositivi:
  - **Contatti**: **Sì** sincronizza i contatti. **No** non sincronizza automaticamente i contatti. Gli utenti eseguono la sincronizzazione manualmente.
  - **Calendario**: **Sì** sincronizza il calendario. **No** non sincronizza automaticamente i contatti. Gli utenti eseguono la sincronizzazione manualmente.
  - **Attività**: **Sì** sincronizza le attività. **No** non sincronizza automaticamente le attività. Gli utenti eseguono la sincronizzazione manualmente.

## <a name="next-steps"></a>Passaggi successivi

È anche possibile configurare le impostazioni di posta elettronica in [Android](email-settings-android.md), [Android Enterprise](email-settings-android-enterprise.md), [iOS/iPadOS](email-settings-ios.md) e [Windows 10](email-settings-windows-10.md).

[Configurare le impostazioni di posta elettronica in Intune](email-settings-configure.md).
