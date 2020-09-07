---
title: Configurare le impostazioni di posta elettronica per dispositivi iOS/iPadOS in Microsoft Intune - Azure | Microsoft Docs
description: Vedere l'elenco di tutte le impostazioni di posta elettronica che è possibile configurare e aggiungere ai dispositivi iOS e iPadOS in Microsoft Intune, incluso l'uso dei server Exchange e il recupero degli attributi da Azure Active Directory. È anche possibile abilitare SSL, autenticare gli utenti con certificati o nome utente/password e sincronizzare la posta elettronica nei dispositivi iOS/iPadOS usando i profili di configurazione dispositivo in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/11/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 72c4405d68d2a1c9a5294a7d05acffb106837f60
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88996402"
---
# <a name="add-e-mail-settings-for-ios-and-ipados-devices-in-microsoft-intune"></a>Aggiungere le impostazioni di posta elettronica per i dispositivi iOS e iPadOS in Microsoft Intune

In Microsoft Intune è possibile creare e configurare la posta elettronica per connettersi a un server di posta elettronica, scegliere come si autenticano gli utenti, usare S/MIME per la crittografia e altro ancora.

Questo articolo elenca e descrive tutte le impostazioni di posta elettronica disponibili per i dispositivi che eseguono iOS/iPadOS. È possibile creare un profilo di configurazione del dispositivo per eseguire il push o la distribuzione delle impostazioni di posta elettronica nei dispositivi iOS/iPadOS.

## <a name="before-you-begin"></a>Prima di iniziare

[Creare un profilo di configurazione del dispositivo](email-settings-configure.md).

> [!NOTE]
> Queste impostazioni sono disponibili per tutti i tipi di registrazione. Per altre informazioni sui tipi di registrazione, vedere [Registrazione iOS/iPadOS](../enrollment/ios-enroll.md).

## <a name="exchange-activesync-account-settings"></a>Impostazioni dell'account di Exchange ActiveSync

- **Server di posta elettronica**: immettere il nome host del server Exchange dell'azienda.
- **Nome account**: immettere il nome visualizzato dell'account di posta elettronica. Questo nome viene visualizzato nel dispositivo degli utenti.
- **Attributo nome utente da AAD**: questo nome è l'attributo che Intune ottiene da Azure Active Directory (AAD). Intune genera in modo dinamico il nome utente usato da questo profilo. Le opzioni disponibili sono:
  - **Nome entità utente**: ottiene il nome, ad esempio `user1` o `user1@contoso.com`
  - **Indirizzo SMTP primario**: ottiene il nome nel formato dell'indirizzo di posta elettronica, ad esempio `user1@contoso.com`
  - **Nome account SAM**: richiede il dominio, ad esempio `domain\user1`. Specificare anche:  
    - **Origine del nome di dominio utente**: scegliere **AAD** (Azure Active Directory) o **Personalizzato**.
      - **AAD**: ottenere gli attributi da Azure AD. Specificare anche:
        - **Attributo nome di dominio utente da AAD**: scegliere di ottenere l'attributo **Nome di dominio completo** o (`contoso.com`) o **Nome NetBIOS** (`contoso`) dell'utente.

      - **Personalizzato**: ottenere gli attributi da un nome di dominio personalizzato. Specificare anche:
        - **Nome di dominio personalizzato da usare**: immettere un valore usato da Intune per il nome di dominio, ad esempio `contoso.com` o `contoso`.

- **Attributo indirizzo di posta elettronica da AAD**: scegliere la modalità di generazione dell'indirizzo di posta elettronica per l'utente. Le opzioni disponibili sono:
  - **Nome entità utente**: usare come indirizzo e-mail il nome dell'entità completo, ad esempio `user1@contoso.com` o `user1`.
  - **Indirizzo SMTP primario**: usare l'indirizzo SMTP primario per accedere a Exchange, ad esempio `user1@contoso.com`.
- **Metodo di autenticazione**: scegliere il modo in cui gli utenti eseguono l'autenticazione per il server di posta elettronica. Le opzioni disponibili sono:
  - **Certificato**: selezionare un profilo certificato SCEP o PKCS creato in precedenza per autenticare la connessione di Exchange. Questa opzione offre l'esperienza più sicura e trasparente per gli utenti.
  - **Nome utente e password**: agli utenti viene richiesto di immettere il nome utente e la password.
  - **Credenziale derivata**: usare un certificato derivato dalla smart card di un utente. Per altre informazioni, vedere [Usare le credenziali derivate in Microsoft Intune](../protect/derived-credentials.md).

  >[!NOTE]
  > L'autenticazione a più fattori di Azure non è supportata.
  
- **SSL**: selezionare **Abilita** per usare la comunicazione Secure Sockets Layer (SSL) durante l'invio e la ricezione di messaggi di posta elettronica e durante la comunicazione con il server Exchange.
- **OAuth**: selezionare **Abilita** per usare la comunicazione Open Authorization (OAuth) durante l'invio e la ricezione di messaggi di posta elettronica e durante la comunicazione con Exchange. Se il server OAuth usa l'autenticazione del certificato, scegliere **Certificato** come **Metodo di autenticazione** e includere il certificato con il profilo. In caso contrario scegliere **Nome utente e password** come **Metodo di autenticazione**. Quando si usa OAuth, verificare quanto segue.

  - Verificare che la soluzione di posta elettronica supporti OAuth prima di destinare questo profilo agli utenti. Microsoft 365 Exchange Online supporta OAuth. Exchange locale e altre soluzioni partner o di terze parti potrebbero non supportare OAuth. Exchange locale può essere configurato per l'autenticazione moderna. Per altre informazioni, vedere [Panoramica dell'autenticazione moderna ibrida e prerequisiti per l'utilizzo con i server Skype for Business ed Exchange locali](/office365/enterprise/hybrid-modern-auth-overview).

    Se il profilo di posta elettronica usa Oauth e il servizio di posta elettronica non la supporta, l'opzione **Reimmettere la password** non funziona. Ad esempio, non accade nulla quando l'utente sceglie **Reimmettere la password** nelle impostazioni del dispositivo Apple.

  - Quando OAuth è abilitata, gli utenti finali hanno un'esperienza di accesso alla posta elettronica con l'autenticazione moderna diversa che supporta l'autenticazione a più fattori (MFA). 

  - Alcune organizzazioni disabilitano la possibilità dell'utente finale di eseguire l'[accesso all'applicazione self-service](/azure/active-directory/manage-apps/manage-self-service-access). In questo scenario, l'accesso con l'autenticazione moderna potrebbe non riuscire finché un amministratore non crea l'app aziendale "Account iOS" e concede agli utenti l'accesso all'app in Azure AD.

    L'azione predefinita consiste nell'aggiungere un'applicazione usando la funzionalità [Pannello di accesso dell'applicazione](/azure/active-directory/user-help/active-directory-saas-access-panel-introduction) **Aggiungi app** **senza approvazione aziendale**. Per altre informazioni, vedere [Come assegnare gli utenti alle applicazioni](/azure/active-directory/manage-apps/ways-users-get-assigned-to-applications).

  > [!NOTE]
  > Quando si abilita OAuth, si verifica quanto segue:  
  > 1. Viene rilasciato un nuovo profilo ai dispositivi già specificati come destinazione.
  > 2. Agli utenti finali viene chiesto di specificare nuovamente le credenziali.

## <a name="exchange-activesync-profile-configuration"></a>Configurazione del profilo di Exchange ActiveSync

> [!IMPORTANT]
> La configurazione di queste impostazioni distribuisce un nuovo profilo al dispositivo, anche quando viene aggiornato un profilo di posta elettronica esistente per includere queste impostazioni. Agli utenti viene richiesto di immettere la password dell'account di Exchange ActiveSync. Queste impostazioni hanno effetto quando viene immessa la password.

- **Dati di Exchange da sincronizzare**: quando si usa Exchange ActiveSync, scegliere i servizi di Exchange sincronizzati nel dispositivo: Calendario, Contatti, Promemoria, Note e Posta elettronica. Le opzioni disponibili sono:
  - **Tutti i dati** (impostazione predefinita): la sincronizzazione è abilitata per tutti i servizi.
  - **Solo posta elettronica**: la sincronizzazione è abilitata solo per la posta elettronica. La sincronizzazione è disabilitata per gli altri servizi.
  - **Solo Calendario**: la sincronizzazione è abilitata solo per il Calendario. La sincronizzazione è disabilitata per gli altri servizi.
  - **Solo Calendario e Contatti**: la sincronizzazione è abilitata solo per Calendario e Contatti. La sincronizzazione è disabilitata per gli altri servizi.
  - **Solo Contatti**: la sincronizzazione è abilitata solo per i Contatti. La sincronizzazione è disabilitata per gli altri servizi.

  Questa funzionalità si applica a:  
  - iOS 13.0 e versioni successive
  - iPadOS 13.0 e versioni successive

- **Consenti agli utenti di modificare le impostazioni di sincronizzazione**: Scegliere se gli utenti possono modificare le impostazioni di Exchange ActiveSync per i servizi di Exchange nel dispositivo: Calendario, Contatti, Promemoria, Note e Posta elettronica. Le opzioni disponibili sono:

  - **Sì** (impostazione predefinita): gli utenti possono modificare il comportamento di sincronizzazione di tutti i servizi. Se si sceglie **Sì**, è possibile apportare modifiche a *tutti* i servizi.
  - **No**: gli utenti non possono modificare le impostazioni di sincronizzazione di tutti i servizi. La scelta di **No** blocca le modifiche a *tutti* i servizi.

  > [!TIP]
  > Se è stata configurata l'impostazione **Dati di Exchange da sincronizzare** per sincronizzare solo alcuni servizi, è consigliabile selezionare **No** per questa impostazione. La scelta di **No** impedisce agli utenti di modificare il servizio di Exchange sincronizzato.

  Questa funzionalità si applica a:  
  - iOS 13.0 e versioni successive
  - iPadOS 13.0 e versioni successive

## <a name="exchange-activesync-email-settings"></a>Impostazioni di posta elettronica di Exchange ActiveSync

- **S/MIME**: S/MIME usa i certificati di posta elettronica che offrono ulteriore sicurezza alle comunicazioni di posta elettronica tramite la firma, la crittografia e la decrittografia. Quando si usa S/MIME con un messaggio di posta elettronica, si conferma l'autenticità del mittente e l'integrità e la riservatezza del messaggio.

  Le opzioni disponibili sono:

  - **Disabilita S/MIME** (impostazione predefinita): non usa un certificato di posta elettronica S/MIME per firmare, crittografare o decrittografare i messaggi di posta elettronica.
  - **Abilita S/MIME**: consente agli utenti di firmare e/o crittografare la posta elettronica nell'applicazione di posta elettronica nativa iOS/iPadOS. Specificare anche:

    - **Firma S/MIME abilitata**: l'impostazione predefinita **Disabilita** non consente agli utenti di firmare digitalmente il messaggio. **Abilita** consente agli utenti di firmare digitalmente i messaggi di posta elettronica in uscita per l'account specificato. La firma consente agli utenti che ricevono i messaggi di essere sicuri che il messaggio proveniva da quell'utente specifico e non da qualcuno che fingeva di essere il mittente.
      - **Allow user to change setting** (Consenti all'utente di modificare l'impostazione): **Abilita** consente agli utenti di modificare le opzioni di firma. **Disabilita** (impostazione predefinita) impedisce agli utenti di modificare la firma e impone agli utenti di usare la firma configurata.
      - **Tipo di certificato di firma**: Le opzioni disponibili sono:
        - **Non configurata**: Intune non aggiorna o modifica questa impostazione.
        - **Nessuno**: l'amministratore non impone un certificato specifico. Selezionare questa opzione in modo che gli utenti possano scegliere il proprio certificato.
        - **Credenziale derivata**: usare un certificato derivato dalla smart card di un utente. Per altre informazioni, vedere [Usare le credenziali derivate in Microsoft Intune](../protect/derived-credentials.md).
        - **Certificati**: Selezionare un profilo esistente del certificato PKCS o SCEP usato per firmare i messaggi di posta elettronica.
      - **Allow user to change setting** (Consenti all'utente di modificare l'impostazione): **Abilita** consente agli utenti di modificare il certificato di firma. **Disabilita** (impostazione predefinita) impedisce agli utenti di modificare il certificato di firma e imporre di usare il certificato configurato.

        Questa funzionalità si applica a:  
        - iOS 12 e versioni successive
        - iPadOS 12 e versioni successive

    - **Encrypt by default** (Crittografa per impostazione predefinita): selezionare **Abilita** per crittografare tutti i messaggi come comportamento predefinito. **Disabilita** (impostazione predefinita) non crittografa tutti i messaggi come comportamento predefinito.
      - **Allow user to change setting** (Consenti all'utente di modificare l'impostazione): **Abilita** consente agli utenti di modificare il comportamento di crittografia predefinito. **Disabilita** impedisce agli utenti di modificare il comportamento di crittografia predefinito e impone agli utenti di usare la crittografia configurata.

        Questa funzionalità si applica a:  
        - iOS 12 e versioni successive
        - iPadOS 12 e versioni successive

    - **Force per-message encryption** (Forza crittografia per singoli messaggi): la crittografia per singoli messaggi consente agli utenti di scegliere quali messaggi di posta elettronica crittografare prima dell'invio.

      **Abilita** mostra l'opzione di crittografia per singoli messaggi quando si crea un nuovo messaggio di posta elettronica. Gli utenti possono quindi scegliere se usare o non usare la crittografia per singoli messaggi. Se l'impostazione **Crittografa per impostazione predefinita** è abilitata, abilitando la crittografia per singoli messaggi si consente agli utenti di non usare la crittografia per singoli messaggi.

      **Disabilita** (impostazione predefinita) impedisce agli utenti di visualizzare l'opzione di crittografia per singoli messaggi. Se l'impostazione **Crittografa per impostazione predefinita** è disabilitata, abilitando la crittografia per singoli messaggi si consente agli utenti di usare la crittografia per singoli messaggi.

      - **Tipo di certificato di crittografia**: Le opzioni disponibili sono:
        - **Non configurata**: Intune non aggiorna o modifica questa impostazione.
        - **Nessuno**: l'amministratore non impone un certificato specifico. Selezionare questa opzione in modo che gli utenti possano scegliere il proprio certificato.
        - **Credenziale derivata**: usare un certificato derivato dalla smart card di un utente. Per altre informazioni, vedere [Usare le credenziali derivate in Microsoft Intune](../protect/derived-credentials.md).
        - **Certificati**: Selezionare un profilo esistente del certificato PKCS o SCEP usato per firmare i messaggi di posta elettronica.
      - **Allow user to change setting** (Consenti all'utente di modificare l'impostazione): **Abilita** consente agli utenti di modificare il certificato di crittografia. **Disabilita** (impostazione predefinita) impedisce agli utenti di modificare il certificato di crittografia e impone agli utenti di usare il certificato configurato.

        Questa funzionalità si applica a:  
        - iOS 12 e versioni successive
        - iPadOS 12 e versioni successive

- **Numero di messaggi di posta elettronica da sincronizzare**: selezionare il numero di giorni di posta elettronica da sincronizzare. In alternativa, selezionare **Illimitata** per sincronizzare tutti i messaggi di posta elettronica disponibili.
- **Consenti di spostare i messaggi negli altri account di posta elettronica**: **Abilita** (impostazione predefinita) consente agli utenti di spostare i messaggi di posta elettronica tra i diversi account configurati nei dispositivi.
- **Consenti di inviare i messaggi di posta elettronica dalle applicazioni di terze parti**: **Abilita** (impostazione predefinita) consente agli utenti di selezionare questo profilo come account predefinito per l'invio di posta elettronica. Ciò consente alle applicazioni di terze parti di aprire i messaggi di posta elettronica nell'app nativa, ad esempio per allegare file ai messaggi.
- **Sincronizza gli indirizzi di posta elettronica utilizzati di recente**: **Abilita** (impostazione predefinita) consente agli utenti di sincronizzare con il server l'elenco di indirizzi e-mail usati di recente sul dispositivo.

## <a name="next-steps"></a>Passaggi successivi

Il profilo è stato creato, ma non è ancora operativo. [Assegnare il profilo](device-profile-assign.md) e [monitorarne lo stato](device-profile-monitor.md).

Configurare le impostazioni di posta elettronica nei dispositivi [Android](email-settings-android.md), [Android Enterprise](email-settings-android-enterprise.md) e [Windows 10](email-settings-windows-10.md).