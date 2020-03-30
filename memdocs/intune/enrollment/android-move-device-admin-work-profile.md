---
title: Aggiornare i dispositivi Android da amministratore di dispositivi alla gestione del profilo di lavoro
titleSuffix: Microsoft Intune
description: Aggiornare i dispositivi Android da amministratore di dispositivi alla gestione del profilo di lavoro in Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: b66777e9c108ab4a6b84e4d4fa0942532685912f
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/21/2020
ms.locfileid: "80086728"
---
# <a name="move-android-devices-from-device-administrator-to-work-profile-management"></a>Aggiornare i dispositivi Android da amministratore di dispositivi alla gestione del profilo di lavoro

È possibile consentire agli utenti di aggiornare i dispositivi Android da amministratore di dispositivi alla gestione del profilo di lavoro usando l'impostazione di conformità **Blocca i dispositivi gestiti con amministratore di dispositivi**. Questa impostazione consente di rendere un dispositivo non conforme se gestito con amministratore di dispositivi. 

Quando gli utenti notano che non sono conformi per questo motivo, possono toccare **Risolvi**. Verranno indirizzati a un elenco di controllo che li guiderà nelle attività seguenti:
1. Annullamento della registrazione nella gestione degli amministratori dei dispositivi
2. Registrazione nella gestione del profilo di lavoro
3. Risoluzione dei problemi di conformità. 

## <a name="prerequisites"></a>Prerequisiti

- Gli utenti devono avere [Dispositivi registrati con amministratore di dispositivi Android](android-enroll-device-administrator.md) con il Portale aziendale Android versione 5.0.4720.0 o successiva.
- Configurare la gestione dei profili di lavoro Android [connettendo l'account del tenant di Intune all'account di Android Enterprise](connect-intune-android-enterprise.md).
- [Impostare la registrazione del profilo di lavoro Android Enterprise](android-work-profile-enroll.md) per il gruppo di utenti che passano al profilo di lavoro Android.
- È consigliabile aumentare i limiti di dispositivi utente. Quando si annulla la registrazione dei dispositivi dalla gestione di amministratore di dispositivi, i record dei dispositivi potrebbero non essere rimossi immediatamente. Per offrire protezione durante questo periodo, potrebbe essere necessario aumentare la capacità dei limiti dei dispositivi in modo che gli utenti possano eseguire la registrazione nella gestione del profilo di lavoro.
  - [Configurare le impostazioni dispositivo in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/devices/device-management-azure-portal.md#configure-device-settings) per il numero massimo di dispositivi per utente.
  - Modificare le [restrizioni relative al limite dei dispositivi Intune](enrollment-restrictions-set.md#create-a-device-limit-restriction) impostando il limite di dispositivi. 

## <a name="create-device-compliance-policy"></a>Creare criteri di conformità dei dispositivi

1. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) selezionare **Dispositivi** > **Criteri di conformità** > **Criteri** > **Crea criterio**.

    ![Creare i criteri](./media/android-move-device-admin-work-profile/create-policy.png)

2. Nella pagina **Crea un criterio** impostare **Piattaforma** su **Amministratore di dispositivi Android** > **Crea**.
3. Nella pagina **Informazioni di base** specificare un **Nome** e una **Descrizione** > **Avanti**.

    ![Pagina Informazioni di base](./media/android-move-device-admin-work-profile/basics.png)
    
4. Nella pagina **Impostazioni di conformità** nella sezione **Integrità del dispositivo** impostare **Blocca i dispositivi gestiti con amministratore di dispositivi** su **Sì** > **Avanti**.

    ![Bloccare dispositivi](./media/android-move-device-admin-work-profile/block-devices.png)

5. Nella pagina **Percorsi**  è possibile aggiungere percorsi > **Avanti**.
6. In **Azioni per la non conformità** è possibile impostare l'azione di **Invia un messaggio di posta elettronica all'utente finale**.

    ![Inviare messaggio di posta elettronica](./media/android-move-device-admin-work-profile/send-email.png)


    Nel messaggio di posta elettronica è possibile includere l'URL seguente nei messaggi agli utenti. L'URL avvierà il Portale aziendale Android nella pagina **Aggiorna impostazioni del dispositivo**. Questa pagina avvia il flusso per passare alla gestione del profilo di lavoro.
    - [https://portal.manage.microsoft.com/UpdateSettings.aspx](https://portal.manage.microsoft.com/UpdateSettings.aspx).
    - Per il governo degli Stati Uniti è invece possibile usare questo collegamento: [https://portal.manage.microsoft.us/UpdateSettings.aspx](https://portal.manage.microsoft.us/UpdateSettings.aspx).
  
    > [!NOTE]
    > - Naturalmente, è possibile usare collegamenti in hyper text intuitivo per le comunicazioni con gli utenti. Tuttavia, non usare URL abbreviati perché i collegamenti potrebbero non funzionare se modificati in questo modo.
    > - Se il Portale aziendale Android è aperto e in background, quando un utente tocca il collegamento è possibile che venga visualizzata l'ultima pagina in cui si trovava.

    Scegliere **Avanti**.

7. Nella pagina **Tag di ambito** selezionare i tag dell'ambito da includere.
8. Nella pagina **Assegnazioni** assegnare i criteri a un gruppo che ha dispositivi registrati con la gestione dell'amministratore di dispositivi > **Avanti**.
9. Nella pagina **Rivedi e crea** confermare tutte le impostazioni e selezionare **Crea**.

## <a name="troubleshooting"></a>Risoluzione dei problemi

Il [flusso per l'utente finale per passare alla nuova configurazione di gestione dei dispositivi](https://docs.microsoft.com/mem/intune/user-help/move-to-new-device-management-setup.md) guida gli utenti nel processo di annullamento della registrazione nella gestione amministratore di dispositivi e di configurazione della gestione profilo di lavoro. Gli utenti devono avere [dispositivi registrati con amministratore di dispositivi Android](android-enroll-device-administrator.md) con il Portale aziendale Android versione 5.0.4720.0 o successiva.

### <a name="user-sees-an-error-after-tapping-resolve"></a>L'utente visualizza un errore quando tocca Risolvi
Se gli utenti visualizzano un errore dopo aver toccato il pulsante **Risolvi**, è probabile che la causa sia uno dei motivi seguenti:
- La registrazione del profilo di lavoro non è configurata correttamente. Un account Android Enterprise non è connesso o le restrizioni di registrazione sono impostate per bloccare la registrazione del profilo di lavoro.
- Nel dispositivo è in esecuzione Android 4.4 o versione precedente, che non supporta la registrazione del profilo di lavoro. 
- Il produttore del dispositivo non supporta la registrazione del profilo di lavoro nel modello di dispositivo.

### <a name="resolve-button-doesnt-appear-on-the-users-device"></a>Il pulsante Risolvi non viene visualizzato nel dispositivo dell'utente
Il pulsante **Risolvi** non viene visualizzato nel dispositivo dell'utente se l'utente esegue la registrazione alla gestione amministratore di dispositivi dopo che al dispositivo sono stati assegnati i criteri di conformità descritti in precedenza.

Per visualizzare il pulsante **Risolvi**, l'utente deve posticipare la configurazione e riavviare il processo dalla notifica.

Per evitare questa condizione, usare le restrizioni di registrazione per bloccare la registrazione nella gestione amministratore di dispositivi.

### <a name="user-sees-an-error-after-tapping-url-to-update-device-settings-page"></a>L'utente visualizza un errore dopo aver toccato l'URL per accedere alla pagina Aggiorna impostazioni del dispositivo
Gli utenti potrebbero visualizzare una pagina di errore nel browser quando toccano l'URL per accedere alla pagina **Aggiorna impostazioni del dispositivo** del Portale aziendale Android. La causa dell'errore può essere una delle seguenti:
- Il dispositivo non è un dispositivo Android.
- Il dispositivo Android non ha l'app Portale aziendale.
- La versione del Portale aziendale Android è precedente a 5.0.4720.0.
- Il dispositivo Android usa Android 6 o versioni precedenti. 

## <a name="next-steps"></a>Passaggi successivi
[Visualizzare il flusso per l'utente finale](https://docs.microsoft.com/mem/intune/user-help/move-to-new-device-management-setup.md)

[Gestire i dispositivi del profilo di lavoro Android con Intune](android-enterprise-overview.md)


