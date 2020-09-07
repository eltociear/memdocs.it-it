---
title: Risoluzione dei problemi di registrazione dei dispositivi iOS/iPadOS in Microsoft Intune
titleSuffix: Microsoft Intune
description: Suggerimenti per la risoluzione di alcuni dei problemi più comuni quando si registrano i dispositivi iOS/iPadOS in Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/16/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: mghadial
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c81216ae7350beafcf1e090b278d5975d6fea086
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88993292"
---
# <a name="troubleshoot-iosipados-device-enrollment-problems-in-microsoft-intune"></a>Risoluzione dei problemi di registrazione dei dispositivi iOS/iPadOS in Microsoft Intune

Questo articolo aiuta gli amministratori di Intune a comprendere e risolvere i problemi durante la registrazione dei dispositivi iOS/iPadOS in Intune.

## <a name="prerequisites"></a>Prerequisiti

Prima di iniziare la risoluzione dei problemi, è importante raccogliere alcune informazioni di base che possono essere utili per comprendere meglio il problema e ridurre il tempo necessario per trovare una soluzione.

Raccogliere le informazioni seguenti sul problema:

- Qual è il messaggio di errore esatto?
- Dove viene visualizzato il messaggio di errore?
- Quando è iniziato il problema? La registrazione ha mai funzionato?
- Quale piattaforma (Android, iOS/iPad, Windows) presenta il problema?
- Quanti utenti sono interessati? Sono interessati tutti gli utenti o solo alcuni?
- Quanti dispositivi sono interessati? Sono interessati tutti i dispositivi o solo alcuni?
- Che cos'è l'autorità MDM?
- Come viene eseguita la registrazione? Si tratta di profili di registrazione BYOD (Bring Your Own Device) o di Registrazione automatica del dispositivo Apple?

## <a name="error-messages"></a>Messaggi di errore

### <a name="profile-installation-failed-a-network-error-has-occurred"></a>Installazione profilo non riuscita. Si è verificato un errore di rete.

**Causa:** si è verificato un problema non specificato con iOS/iPadOS nel dispositivo.

#### <a name="resolution"></a>Soluzione

1. Il ripristino di iOS/iPadOS elimina tutti i dati nel dispositivo. Per evitare quindi la perdita dei dati nei passaggi seguenti, assicurarsi di eseguire il backup dei dati.
2. Impostare il dispositivo in modalità di ripristino, quindi ripristinarlo. Controllare che sia configurato come nuovo dispositivo. Per altre informazioni su come ripristinare i dispositivi iOS/iPadOS, vedere [https://support.apple.com/HT201263](https://support.apple.com/HT201263).
3. Registrare nuovamente il dispositivo.

### <a name="profile-installation-failed-connection-to-the-server-could-not-be-established"></a>Installazione profilo non riuscita. Non è stato possibile stabilire una connessione al server.

**Causa:** il tenant di Intune è configurato per consentire solo i dispositivi di proprietà dell'azienda. 

#### <a name="resolution"></a>Soluzione
1. Accedere al portale di Azure.
2. Selezionare **Altri servizi**, cercare Intune e quindi selezionare **Intune**.
3. Selezionare **Registrazione del dispositivo** > **Restrizioni registrazione**.
4. In **Restrizioni dei tipi di dispositivo** selezionare la restrizione che si vuole impostare > **Proprietà** > **Seleziona le piattaforme**> selezionare **Consenti** per**iOS**, quindi fare clic su **OK**.
5. Selezionare **Configura le piattaforme**, selezionare **Consenti** per i dispositivi iOS/iPadOS di proprietà personale, quindi fare clic su **OK**.
6. Registrare nuovamente il dispositivo.

**Causa:** si registra un dispositivo registrato precedentemente con un account utente diverso e l'utente precedente non è stato rimosso in modo appropriato da Intune.

#### <a name="resolution"></a>Soluzione
1. Annullare l'installazione del profilo corrente.
2. Aprire [https://portal.manage.microsoft.com](https://portal.manage.microsoft.com) in Safari.
3. Registrare nuovamente il dispositivo.

> [!NOTE]
> Se il dispositivo non viene ancora registrato, rimuovere i cookie in Safari (non bloccare i cookie), quindi registrare nuovamente il dispositivo.

**Causa:** il dispositivo è già registrato con un altro provider MDM.

#### <a name="resolution"></a>Soluzione
1. Aprire **Impostazioni** nel dispositivo iOS/iPadOS, passare a **Generale > Gestione dei dispositivi**.
2. Rimuovere qualsiasi profilo di gestione esistente.
3. Registrare nuovamente il dispositivo.

**Causa:** l'utente che tenta di registrare il dispositivo non dispone di una licenza di Microsoft Intune.

#### <a name="resolution"></a>Soluzione
1. Passare all'[Interfaccia di amministrazione di Microsoft 365](https://admin.microsoft.com) e quindi scegliere **Utenti > Utenti attivi**.
2. Selezionare l'account utente a cui si vuole assegnare una licenza utente di Intune e quindi scegliere **Licenze di prodotto > Modifica**.
3. **Attivare** la licenza che si vuole assegnare all'utente, quindi scegliere **Salva**.
4. Registrare nuovamente il dispositivo.

### <a name="this-service-is-not-supported-no-enrollment-policy"></a>Questo servizio non è supportato. Nessun criterio di registrazione.

**Causa**: un certificato per le notifiche push MDM Apple non è configurato in Intune o il certificato non è valido. 

#### <a name="resolution"></a>Soluzione

- Se il certificato per le notifiche push MDM non è configurato, attenersi alla procedura descritta in [Ottenere un certificato per le notifiche push MDM Apple](apple-mdm-push-certificate-get.md#steps-to-get-your-certificate).
- Se il certificato per le notifiche push MDM non è valido, attenersi alla procedura descritta in [Rinnovare il certificato per le notifiche push Apple](apple-mdm-push-certificate-get.md#renew-apple-mdm-push-certificate).

### <a name="company-portal-temporarily-unavailable-the-company-portal-app-encountered-a-problem-if-the-problem-persists-contact-your-system-administrator"></a>Portale aziendale temporaneamente non disponibile. Si è verificato un problema nell'app Portale aziendale. Se il problema persiste, contattare l'amministratore del sistema.

**Causa:** l'app Portale aziendale non è aggiornata o è danneggiata.

#### <a name="resolution"></a>Soluzione
1. Rimuovere l'app Portale aziendale dal dispositivo.
2. Scaricare e installare l'app **Portale aziendale Microsoft Intune** da **App Store**.
3. Registrare nuovamente il dispositivo.

> [!NOTE]
> Questo errore può verificarsi anche se l'utente tenta di registrare più dispositivi rispetto a quanto consentito dalla registrazione dei dispositivi. Seguire i passaggi per la risoluzione descritti nella sezione **Numero massimo dispositivi raggiunto** riportata sotto, se questa procedura non risolve il problema.

### <a name="device-cap-reached"></a>Numero massimo dispositivi raggiunto

**Causa:** l'utente tenta di registrare più dispositivi rispetto al limite consentito.

#### <a name="resolution"></a>Soluzione
1. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager ](https://go.microsoft.com/fwlink/?linkid=2109431) scegliere **Dispositivi** > **Tutti i dispositivi** e verificare il numero di dispositivi registrati dall'utente.
    > [!NOTE]
    > È anche consigliabile accedere con l'utente interessato al [portale utenti di Intune](https://portal.manage.microsoft.com/) e controllare i dispositivi registrati. Potrebbero essere presenti dispositivi che vengono visualizzati nel [portale utenti di Intune](https://portal.manage.microsoft.com/) ma non nel [portale di amministrazione di Intune](https://portal.azure.com/?Microsoft_Intune=1&Microsoft_Intune_DeviceSettings=true&Microsoft_Intune_Enrollment=true&Microsoft_Intune_Apps=true&Microsoft_Intune_Devices=true#blade/Microsoft_Intune_DeviceSettings/ExtensionLandingBlade/overview). Questi dispositivi vengono comunque conteggiati nel limite di registrazione dispositivi.
2. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) scegliere **Dispositivi** > **Restrizioni registrazione** > verificare il limite di registrazione dispositivi. Per impostazione predefinita, il limite è impostato su 15. 
3. Se il numero di dispositivi registrati ha raggiunto il limite, rimuovere i dispositivi non necessari o aumentare il limite di registrazione dispositivi. Poiché ogni dispositivo registrato usa una licenza di Intune, è consigliabile rimuovere sempre i dispositivi non necessari.
4. Registrare nuovamente il dispositivo.

### <a name="workplace-join-failed"></a>Workplace Join non riuscito

**Causa:** l'app Portale aziendale non è aggiornata o è danneggiata.  

#### <a name="resolution"></a>Soluzione
1. Rimuovere l'app Portale aziendale dal dispositivo.
2. Scaricare e installare l'app **Portale aziendale Microsoft Intune** da **App Store**.
3. Registrare nuovamente il dispositivo.

### <a name="user-license-type-invalid"></a>Tipo di licenza utente non valido

**Causa:** l'utente che tenta di registrare il dispositivo non ha una licenza di Intune valida.

#### <a name="resolution"></a>Soluzione
1. Passare all'[interfaccia di amministrazione di Microsoft 365](https://admin.microsoft.com), quindi scegliere **Utenti** > **Utenti attivi**.
2. Selezionare l'account utente interessato > **Licenze di prodotto** > **Modifica**.
3. Verificare che all'utente sia assegnata una licenza di Intune valida.
4. Registrare nuovamente il dispositivo.

### <a name="user-name-not-recognized-this-user-account-is-not-authorized-to-use-microsoft-intune-contact-your-system-administrator-if-you-think-you-have-received-this-message-in-error"></a>Nome utente non riconosciuto. Questo account utente non è autorizzato a usare Microsoft Intune. Se si ritiene di aver ricevuto questo messaggio per errore, contattare l'amministratore di sistema.

**Causa:** l'utente che tenta di registrare il dispositivo non ha una licenza di Intune valida.

1. Passare all'[interfaccia di amministrazione di Microsoft 365](https://admin.microsoft.com), quindi scegliere **Utenti** > **Utenti attivi**.
2. Selezionare l'account utente interessato, quindi scegliere **Licenze di prodotto** > **Modifica**.
3. Verificare che all'utente sia assegnata una licenza di Intune valida.
4. Registrare nuovamente il dispositivo.

### <a name="profile-installation-failed-the-new-mdm-payload-does-not-match-the-old-payload"></a>Installazione profilo non riuscita. Il nuovo payload di MDM non corrisponde al payload precedente.

**Causa:** nel dispositivo è già installato un profilo di gestione.

#### <a name="resolution"></a>Soluzione

1. Aprire **Impostazioni** nel dispositivo iOS/iPadOS > **Generale** >  **Gestione dei dispositivi**.
2. Toccare il profilo di gestione esistente, quindi **Remove Management** (Rimuovi gestione).
3. Registrare nuovamente il dispositivo.

### <a name="noenrollmentpolicy"></a>NoEnrollmentPolicy

**Causa:** il certificato APN (Apple Push Notification Service) manca, non è valido o è scaduto.

#### <a name="resolution"></a>Soluzione
Verificare che in Intune sia stato aggiunto un certificato APN valido. Per altre informazioni, vedere [Configurare la registrazione di dispositivi iOS/iPadOS](ios-enroll.md).

### <a name="accountnotonboarded"></a>AccountNotOnboarded

**Causa:** si è verificato un problema con il certificato APN (Apple Push Notification Service) configurato in Intune.

#### <a name="resolution"></a>Soluzione
Rinnovare il certificato APN, quindi eseguire di nuovo la registrazione del dispositivo.

> [!IMPORTANT]
> Assicurarsi di rinnovare il certificato APN. Non sostituire il certificato APN. Se si sostituisce il certificato, è necessario registrare di nuovo tutti i dispositivi iOS/iPadOS in Intune. 

- Per rinnovare il certificato APN in Intune autonomo, vedere [Rinnovare il certificato per le notifiche push MDM Apple](apple-mdm-push-certificate-get.md#renew-apple-mdm-push-certificate).
- Per rinnovare il certificato APN in Microsoft 365, vedere [Creare un certificato APN per dispositivi iOS/iPadOS](https://support.office.com/article/Create-an-APNs-Certificate-for-iOS-devices-522b43f4-a2ff-46f6-962a-dd4f47e546a7).

### <a name="xpc_type_error-connection-invalid"></a>Connessione XPC_TYPE_ERROR non valida

Quando si attiva un dispositivo gestito da Registrazione automatica del dispositivo a cui è assegnato un profilo di registrazione, la registrazione ha esito negativo e viene visualizzato il messaggio di errore seguente:

```output
asciidoc
mobileassetd[83] <Notice>: 0x1a49aebc0 Client connection: XPC_TYPE_ERROR Connection invalid <error: 0x1a49aebc0> { count = 1, transaction: 0, voucher = 0x0, contents = "XPCErrorDescription" => <string: 0x1a49aee18> { length = 18, contents = "Connection invalid" } }
iPhone mobileassetd[83] <Notice>: Client connection invalid (Connection invalid); terminating connection
iPhone com.apple.accessibility.AccessibilityUIServer(MobileAsset)[288] <Notice>: [MobileAssetError:29] Unable to copy asset information from https://mesu.apple.com/assets/ for asset type com.apple.MobileAsset.VoiceServices.CombinedVocalizerVoices
iPhone mobileassetd[83] <Notice>: 0x1a49aebc0 Client connection: XPC_TYPE_ERROR Connection invalid <error: 0x1a49aebc0> { count = 1, transaction: 0, voucher = 0x0, contents = "XPCErrorDescription" => <string: 0x1a49aee18> { length = 18, contents = "Connection invalid" }
```

**Causa:** si è verificato un problema di connessione tra il dispositivo e il servizio Registrazione automatica del dispositivo di Apple.

#### <a name="resolution"></a>Soluzione
Risolvere il problema di connessione oppure usare una connessione di rete diversa per registrare il dispositivo. Se il problema persiste, potrebbe essere anche necessario contattare Apple.


## <a name="other-issues"></a>Altri problemi

### <a name="ade-enrollment-doesnt-start"></a>Il processo di Registrazione automatica del dispositivo non viene avviato
Quando si accende un dispositivo gestito da Registrazione automatica del dispositivo a cui è assegnato un profilo di registrazione, il processo di registrazione di Intune non viene avviato.

**Causa:** il profilo di registrazione è stato creato prima di aver caricato il token di Registrazione automatica del dispositivo in Intune.

#### <a name="resolution"></a>Soluzione

1. Modificare il profilo di registrazione. È possibile apportare qualsiasi modifica al profilo. Lo scopo è aggiornare l'ora di modifica del profilo.
2. Sincronizzare i dispositivi gestiti tramite Registrazione automatica del dispositivo: Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) scegliere **Dispositivi** > **iOS** > **Registrazione di iOS** > **Token del programma di registrazione** > scegliere un token > **Sincronizza ora**. Viene inviata una richiesta di sincronizzazione ad Apple.

### <a name="ade-enrollment-stuck-at-user-login"></a>Registrazione automatica del dispositivo bloccata all'accesso dell'utente
Quando si accende un dispositivo gestito da Registrazione automatica del dispositivo a cui è assegnato un profilo di registrazione, la configurazione iniziale si blocca dopo che l'utente immette le credenziali.

**Causa:** è abilitata l'autenticazione a più fattori (MFA). Attualmente l'autenticazione a più fattori non funziona durante la registrazione nei dispositivi gestiti con Registrazione automatica del dispositivo.

#### <a name="resolution"></a>Soluzione
Disabilitare l'autenticazione a più fattori, quindi eseguire di nuovo la registrazione del dispositivo.

### <a name="authentication-doesnt-redirect-to-the-government-cloud"></a>L'autenticazione non viene reindirizzata al cloud per enti pubblici 

Gli utenti di enti pubblici che accedono da un altro dispositivo vengono reindirizzati al cloud pubblico per l'autenticazione anziché al cloud per enti pubblici. 

**Causa:** Azure AD non supporta ancora il reindirizzamento al cloud per enti pubblici quando si accede da un altro dispositivo. 

#### <a name="resolution"></a>Soluzione 
Usare l'impostazione **Cloud** del Portale aziendale iOS nell'app **Impostazioni** per reindirizzare l'autenticazione degli utenti di enti pubblici verso il cloud per enti pubblici. Per impostazione predefinita, l'impostazione **Cloud** è impostata su **Automatico** e Portale aziendale indirizza l'autenticazione verso il cloud rilevato automaticamente dal dispositivo, ad esempio pubblico o per enti pubblici. Gli utenti di enti pubblici che accedono da un altro dispositivo dovranno selezionare manualmente il cloud per enti pubblici per l'autenticazione. 

Aprire l'app **Impostazioni** e selezionare Portale aziendale. Nelle impostazioni di Portale aziendale selezionare **Cloud**. Impostare **Cloud** su Enti pubblici.  

## <a name="next-steps"></a>Passaggi successivi

- [Risolvere i problemi di registrazione dei dispositivi in Intune](troubleshoot-device-enrollment-in-intune.md)
- [Porre una domanda nel forum di Intune](https://social.technet.microsoft.com/Forums/%7Blang-locale%7D/home?category=microsoftintune&filter=alltypes&sort=lastpostdesc)
- [Controllare il blog del team di supporto di Microsoft Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/bg-p/IntuneCustomerSuccess)
- [Controllare il blog di Microsoft Enterprise Mobility + Security](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-Identity/Announcing-the-public-preview-of-Azure-AD-group-based-license/ba-p/245210)
