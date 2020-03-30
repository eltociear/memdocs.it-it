---
title: Impostazioni di posta elettronica per dispositivi Windows 10 in Microsoft Intune - Azure | Microsoft Docs
description: Creare un profilo di posta elettronica di configurazione del dispositivo che usa server Exchange e recupera gli attributi da Azure Active Directory. È anche possibile abilitare SSL e sincronizzare la posta elettronica e le pianificazioni nei dispositivi Windows 10 con Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/19/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: fa861a266f89b82fdd2d6e73d30fdc2e58da33b4
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/21/2020
ms.locfileid: "80086925"
---
# <a name="email-profile-settings-for-devices-running-windows-10-in-microsoft-intune"></a>Impostazioni del profilo di posta elettronica per i dispositivi che eseguono Windows 10 in Microsoft Intune

Usare le impostazioni del profilo di posta elettronica per configurare l'app di posta elettronica nei dispositivi che eseguono Windows 10 e versioni successive.

## <a name="before-you-begin"></a>Prima di iniziare

[Creare il profilo](email-settings-configure.md).

## <a name="email-settings"></a>Impostazioni di posta elettronica

- **Server di posta elettronica**: immettere il nome host del server Exchange dell'azienda. Immettere ad esempio `outlook.office365.com`.
- **Nome account**: immettere il nome visualizzato dell'account di posta elettronica. Questo nome viene visualizzato nel dispositivo degli utenti.
- **Attributo nome utente da AAD**: questo nome è l'attributo che Intune ottiene da Azure Active Directory (AAD). Intune genera in modo dinamico il nome utente usato da questo profilo. Le opzioni disponibili sono:
  - **Nome entità utente**: ottiene il nome, ad esempio `user1` o `user1@contoso.com`.
  - **Indirizzo SMTP primario**: ottiene il nome nel formato dell'indirizzo di posta elettronica, ad esempio `user1@contoso.com`.
  - **Nome account SAM**: richiede il dominio, ad esempio `domain\user1`. Specificare anche:  
    - **Origine del nome di dominio utente**: scegliere **AAD** (Azure Active Directory) o **Personalizzato**.

      Quando si sceglie di ottenere gli attributi da **AAD**, specificare:
      - **Attributo nome di dominio utente da AAD**: scegliere di ottenere l'attributo **Nome completo** o **Nome NetBIOS** dell'utente.

      Quando si sceglie di usare attributi di tipo **Personalizzato**, specificare:
      - **Nome di dominio personalizzato da usare**: immettere un valore usato da Intune per il nome di dominio, ad esempio `contoso.com` o `contoso`.

- **Attributo indirizzo di posta elettronica da AAD**: Intune ottiene questo attributo da Azure Active Directory (AAD). scegliere la modalità di generazione dell'indirizzo di posta elettronica per l'utente. Le opzioni disponibili sono:
  - **Nome entità utente**: usa come indirizzo di posta elettronica il nome dell'entità completo, ad esempio `user1@contoso.com` o `user1`.
  - **Indirizzo SMTP primario**: usa l'indirizzo SMTP primario per accedere a Exchange, ad esempio `user1@contoso.com`.

### <a name="security"></a>Sicurezza

- **SSL**: selezionare **Abilita** per usare la comunicazione Secure Sockets Layer (SSL) durante l'invio e la ricezione di messaggi di posta elettronica e durante la comunicazione con il server Exchange. Se si seleziona **Disabilita** non è necessario il protocollo SSL.

### <a name="synchronization"></a>Sincronizzazione

- **Numero di messaggi di posta elettronica da sincronizzare**: selezionare il numero di giorni di posta elettronica da sincronizzare. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Selezionare **Senza limiti** per sincronizzare tutti i messaggi di posta elettronica disponibili.
- **Pianificazione sincronizzazione**: selezionare la pianificazione in base alla quale i dispositivi devono sincronizzare i dati dal server Exchange. È anche possibile selezionare **Quando arrivano i messaggi** in modo che i dati vengano sincronizzati non appena arrivano. In alternativa, selezionare **Manuale** in modo che sia l'utente del dispositivo ad avviare la sincronizzazione.

### <a name="content-sync"></a>Sincronizzazione contenuto

- **Tipo di contenuto da sincronizzare**: Selezionare i tipi di contenuto da sincronizzare nei dispositivi:
  - **Contatti**: **Sì** sincronizza i contatti. **No** non sincronizza automaticamente i contatti. Gli utenti eseguono la sincronizzazione manualmente.
  - **Calendario**: **Sì** sincronizza il calendario. **No** non sincronizza automaticamente i contatti. Gli utenti eseguono la sincronizzazione manualmente.
  - **Attività**: **Sì** sincronizza le attività. **No** non sincronizza automaticamente le attività. Gli utenti eseguono la sincronizzazione manualmente.

## <a name="next-steps"></a>Passaggi successivi

È anche possibile configurare le impostazioni di posta elettronica in [Android](email-settings-android.md), [Android Enterprise](email-settings-android-enterprise.md), e [iOS/iPadOS](email-settings-ios.md). 

[Configurare le impostazioni di posta elettronica in Intune](email-settings-configure.md).
