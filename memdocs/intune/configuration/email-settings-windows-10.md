---
title: Impostazioni di posta elettronica per dispositivi Windows 10 in Microsoft Intune - Azure | Microsoft Docs
description: Creare un profilo di posta elettronica di configurazione del dispositivo che usa server Exchange e recupera gli attributi da Azure Active Directory. È anche possibile abilitare SSL e sincronizzare la posta elettronica e le pianificazioni nei dispositivi Windows 10 con Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/29/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 86a792505a07a48d545ab0c5fd115f3aa8dae0eb
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79343635"
---
# <a name="email-profile-settings-for-devices-running-windows-10---intune"></a>Impostazioni del profilo di posta elettronica per i dispositivi che eseguono Windows 10 - Intune

Usare le impostazioni del profilo di posta elettronica per configurare l'app di posta elettronica nei dispositivi che eseguono Windows 10.

- **Server di posta elettronica**: immettere il nome host del server Exchange dell'azienda.
- **Nome account**: immettere il nome visualizzato dell'account di posta elettronica. Questo nome viene visualizzato nel dispositivo degli utenti.
- **Attributo nome utente da AAD**: questo nome è l'attributo che Intune ottiene da Azure Active Directory (AAD). Intune genera in modo dinamico il nome utente usato da questo profilo. Le opzioni disponibili sono:
  - **Nome entità utente**: ottiene il nome, ad esempio `user1` o `user1@contoso.com`
  - **Indirizzo SMTP primario**: ottiene il nome nel formato dell'indirizzo di posta elettronica, ad esempio `user1@contoso.com`
  - **Nome account SAM**: richiede il dominio, ad esempio `domain\user1`.

    Specificare anche:  
    - **Origine del nome di dominio utente**: scegliere **AAD** (Azure Active Directory) o **Personalizzato**.

      Quando si sceglie di ottenere gli attributi da **AAD**, specificare:
      - **Attributo nome di dominio utente da AAD**: scegliere di ottenere l'attributo **Nome di dominio completo** o **Nome NetBIOS** dell'utente

      Quando si sceglie di usare attributi di tipo **Personalizzato**, specificare:
      - **Nome di dominio personalizzato da usare**: immettere un valore usato da Intune per il nome di dominio, ad esempio `contoso.com` o `contoso`

- **Attributo indirizzo di posta elettronica da AAD**: scegliere la modalità di generazione dell'indirizzo di posta elettronica per l'utente. Selezionare **Nome dell'entità utente** (`user1@contoso.com` o `user1`) per usare il nome completo dell'entità utente come indirizzo di posta elettronica oppure selezionare **Indirizzo SMTP primario** (`user1@contoso.com`)per usare l'indirizzo SMTP primario per accedere a Exchange.

## <a name="security-settings"></a>Impostazioni di sicurezza

- **SSL**: Consente di usare la comunicazione Secure Sockets Layer (SSL) durante l'invio e la ricezione di messaggi di posta elettronica e durante la comunicazione con il server Exchange.

## <a name="synchronization-settings"></a>Impostazioni di sincronizzazione

- **Numero di messaggi di posta elettronica da sincronizzare**: selezionare il numero di giorni di posta elettronica da sincronizzare. In alternativa, selezionare **Illimitata** per sincronizzare tutti i messaggi di posta elettronica disponibili.
- **Pianificazione sincronizzazione**: selezionare la pianificazione per la sincronizzazione dei dati dei dispositivi dal server Exchange. È anche possibile selezionare **Quando arrivano i messaggi** per sincronizzare i dati non appena arrivano oppure **Manuale** per consentire all'utente del dispositivo di avviare la sincronizzazione.

## <a name="content-sync-settings"></a>Impostazioni di sincronizzazione del contenuto

- **Tipo di contenuto da sincronizzare**: selezionare i tipi di contenuto da sincronizzare nei dispositivi da:
  - **Contatti**
  - **Calendario**
  - **Attività**

## <a name="next-steps"></a>Passaggi successivi
[Configurare le impostazioni di posta elettronica in Intune](email-settings-configure.md)
