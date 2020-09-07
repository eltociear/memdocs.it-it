---
title: 'Esercitazione: Proteggere la posta elettronica di Exchange Online nei dispositivi non gestiti'
titleSuffix: Microsoft Intune
description: Informazioni su come proteggere Microsoft 365 Exchange Online con i criteri di protezione delle app di Intune e l'accesso condizionale di Azure AD.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/30/2020
ms.topic: tutorial
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 12b776af250a9d4a9bf0fb6c8ba7eec98540f883
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88993954"
---
# <a name="tutorial-protect-exchange-online-email-on-unmanaged-devices"></a>Esercitazione: Proteggere la posta elettronica di Exchange Online nei dispositivi non gestiti

Informazioni sull'uso di criteri di protezione delle app con accesso condizionale per proteggere Exchange Online, anche quando i dispositivi non sono registrati in una specifica soluzione di gestione dei dispositivi come Intune. In questa esercitazione si apprenderà come:

> [!div class="checklist"]
> * Creare criteri di protezione delle app di Intune per l'app Outlook. Si imposteranno limiti relativi alle operazioni che l'utente può eseguire con i dati dell'app, impedendo l'esecuzione del comando "Salva con nome" e limitando le operazioni Taglia, Copia e Incolla.
> * Creare criteri di accesso condizionale di Azure Active Directory (Azure AD) che consentano solo all'app Outlook di accedere alla posta elettronica aziendale in Exchange Online. Si richiederà inoltre l'autenticazione a più fattori (MFA) per i client con autenticazione moderna, come Outlook per iOS e Android.

## <a name="prerequisites"></a>Prerequisiti

Per questa esercitazione sarà necessario un tenant di test con le sottoscrizioni seguenti:

- Azure Active Directory Premium ([versione di valutazione gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F))
- Sottoscrizione di Intune ([versione di valutazione gratuita](../fundamentals/free-trial-sign-up.md))
- Abbonamento a Microsoft 365 Apps for business che include Exchange ([versione di valutazione gratuita](https://go.microsoft.com/fwlink/p/?LinkID=510938))

## <a name="sign-in-to-intune"></a>Accedere a Intune

Per questa esercitazione, quando si accede all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), accedere come [Amministratore globale](../fundamentals/users-add.md#types-of-administrators) o come [Amministratore del servizio](../fundamentals/users-add.md#types-of-administrators) Intune. Se è stata creata una sottoscrizione di valutazione di Intune, l'account con cui è stata creata la sottoscrizione sarà l'amministratore globale.

## <a name="create-the-app-protection-policy"></a>Creare criteri di protezione delle app

In questa esercitazione si imposteranno criteri di protezione delle app di Intune per iOS per l'app Outlook in modo da applicare meccanismi di protezione a livello di app. Si richiederà un PIN per aprire l'app in un contesto aziendale. Si limiterà inoltre la condivisione dei dati tra app e si impedirà che i dati aziendali vengano salvati in un percorso personale.

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selezionare **App** > **Criteri di protezione delle app** > **Crea criterio** e selezionare **iOS/iPadOS** per la piattaforma.

3. Nella pagina **Informazioni di base** è possibile configurare le impostazioni seguenti:

   - **Nome**: Immettere **Outlook app policy test**.
   - **Descrizione**: Immettere **Outlook app policy test**.

   Il valore per **Piattaforma** viene impostato sulla base della scelta precedente.

   Fare clic su **Avanti** per continuare.

4. La pagina **App** consente di scegliere come applicare questo criterio alle app su dispositivi diversi. Configurare le opzioni seguenti:

   - Per **Includi tutti i tipi di app**: Selezionare **No** e quindi per **Tipi di app** selezionare la casella di controllo relativa a **App nei dispositivi non gestiti**.
   - Fare clic su **Selezionare app pubbliche**. Nell'elenco di app selezionare **Outlook** e quindi scegliere **Seleziona**.  Outlook viene ora visualizzato in *App pubbliche*.

   Fare clic su **Avanti** per continuare.

5. La pagina **Protezione dei dati** include impostazioni che determinano il modo in cui gli utenti interagiscono con i dati nelle app a cui vengono applicati questi criteri di protezione delle app. Configurare le opzioni seguenti:

   In *Trasferimento di dati* configurare le impostazioni seguenti, lasciando i valori predefiniti per tutte le altre impostazioni:

   - Per **Invia i dati dell'organizzazione ad altre app** selezionare **Nessuno**.  
   - Per **Ricevi dati da altre app** selezionare **Nessuno**.  
   - Per **Salva copie dei dati dell'organizzazione** selezionare **Blocca**.  
   - Per **Limita le operazioni taglia, copia e incolla tra altre app** selezionare **Bloccato**. 

   ![Selezionare le impostazioni di rilocazione dei dati per i criteri di protezione delle app per Outlook](./media/tutorial-protect-email-on-unmanaged-devices/data-protection-settings.png)

   Selezionare **Avanti** per continuare.

6. La pagina **Requisiti di accesso** include impostazioni che consentono di configurare i requisiti di PIN e credenziali che gli utenti devono soddisfare per accedere alle app in un contesto aziendale. Configurare le impostazioni seguenti, lasciando i valori predefiniti per tutte le altre impostazioni:

   - Per **PIN per l'accesso** selezionare **Richiedi**.
   - Per **Credenziali dell'account aziendale o dell'istituto di istruzione per l'accesso** selezionare **Richiedi**.

   ![Selezionare le azioni di accesso per i criteri di protezione delle app per Outlook](./media/tutorial-protect-email-on-unmanaged-devices/access-requirements-settings.png)

   Selezionare **Avanti** per continuare.

7. La pagina **Avvio condizionale** include impostazioni per definire i requisiti di sicurezza per l'accesso per i criteri di protezione delle app. Per questa esercitazione non è necessario configurare queste impostazioni.

   Fare clic su **Avanti** per continuare.

8. Usare la pagina **Assegnazioni** per assegnare i criteri di protezione delle app a gruppi di utenti. Per questa esercitazione non verranno assegnati questi criteri a un gruppo.  

   Fare clic su **Avanti** per continuare.

9. Nella pagina **Avanti: Verifica + Crea**, verificare i valori e le impostazioni immessi per i criteri di protezione delle app. Fare clic su **Crea** per creare i criteri di protezione delle app in Intune.

La creazione dei criteri di protezione delle app per Outlook è completata. È quindi possibile configurare l'accesso condizionale per richiedere ai dispositivi di usare l'app Outlook.

## <a name="create-conditional-access-policies"></a>Creare criteri di accesso condizionale

Si definiranno ora due impostazioni di criteri di accesso condizionale in modo da supportare tutte le piattaforme per dispositivi.  

- Il primo criterio richiederà che i client con autenticazione moderna usino l'app Outlook approvata e l'autenticazione a più fattori (MFA). I client con autenticazione moderna includono Outlook per iOS e Outlook per Android.  

- Il secondo criterio richiederà che i client Exchange ActiveSync usino l'app Outlook approvata. Attualmente, Exchange ActiveSync non supporta condizioni diverse dalla piattaforma per dispositivi. È possibile configurare i criteri di accesso condizionale nel portale di Azure AD o in quello di Intune. Dato che finora è stato usato il portale di Intune, i criteri verranno creati in questo portale.  

### <a name="create-an-mfa-policy-for-modern-authentication-clients"></a>Creare criteri di autenticazione a più fattori per i client con autenticazione moderna  

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selezionare **Endpoint Security** >  **Accesso condizionale** > **Nuovi criteri**.  

3. Per **Nome** immettere **Test policy for modern auth clients**.  

4. In **Assegnazioni** selezionare **Utenti e gruppi**. Nella scheda **Includi** selezionare **Tutti gli utenti** e quindi selezionare **Fine**.

5. In **Assegnazioni** selezionare **Applicazioni cloud o azioni**. Dato che si vuole proteggere la posta elettronica di Microsoft 365 Exchange Online, si selezionerà questa app tramite la procedura seguente:

   1. Nella scheda **Includi** scegliere **Selezionare le app**.
   2. Scegliere **Seleziona**.
   3. Nell'elenco delle applicazioni selezionare **Office 365 Exchange Online** e quindi scegliere **Seleziona**.
   4. Selezionare **Fine** per tornare al riquadro Nuovi criteri.

   ![Selezionare l'app Office 365 Exchange Online](./media/tutorial-protect-email-on-unmanaged-devices/modern-auth-policy-cloud-apps.png)

6. In **Assegnazioni** selezionare **Condizioni** > **Piattaforme del dispositivo**.

   1. In **Configura** selezionare **Sì**.
   2. Nella scheda **Includi** selezionare **Qualsiasi dispositivo**.
   3. Seleziona **Chiudi**.

7. Nel riquadro **Condizioni** selezionare **App client**.

   1. In **Configura** selezionare **Sì**.
   2. Selezionare **App per dispositivi mobili e client desktop** e **Client con autenticazione moderna**.
   3. Deselezionare le altre caselle di controllo.
   4. Selezionare **Fine** > **Fine** per tornare al riquadro Nuovi criteri.

   ![Selezionare App per dispositivi mobili e client](./media/tutorial-protect-email-on-unmanaged-devices/modern-auth-policy-client-apps.png)

8. In **Controlli di accesso** selezionare **Concedi**.

   1. Nel riquadro **Concedi** selezionare **Concedi accesso**.
   2. Selezionare **Richiedi autenticazione a più fattori** .
   3. Selezionare **Richiedi app client approvata**.
   4. In **Per più controlli** selezionare **Richiedi tutti i controlli selezionati**. Questa impostazione garantisce che entrambi i requisiti selezionati vengano applicati quando un dispositivo tenta di accedere alla posta elettronica.
   5. Scegliere **Seleziona**.

   ![Selezionare i controlli di accesso](./media/tutorial-protect-email-on-unmanaged-devices/modern-auth-policy-mfa.png)

9. In **Attiva criterio** selezionare **Sì** e quindi **Crea**.

   ![Creare i criteri](./media/tutorial-protect-email-on-unmanaged-devices/enable-policy.png)  

La creazione dei criteri di accesso condizionale per i client con autenticazione moderna è completata. È ora possibile creare i criteri per i client di Exchange ActiveSync.

### <a name="create-a-policy-for-exchange-active-sync-clients"></a>Creare criteri per i client di Exchange ActiveSync

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selezionare **Endpoint Security** (Sicurezza endpoint) > **Accesso condizionale** > **Nuovi criteri**.

3. In **Nome** immettere **Test policy for EAS clients**.

4. In **Assegnazioni** selezionare **Utenti e gruppi**. Nella scheda *Includi* selezionare **Tutti gli utenti** e quindi selezionare **Fine**.

5. In **Assegnazioni** selezionare **Applicazioni cloud o azioni**. Selezionare la posta elettronica di Microsoft 365 Exchange Online seguendo questa procedura:

   1. Nella scheda *Includi* scegliere **Selezionare le app**.
   2. Scegliere **Seleziona**.
   3. Nell'elenco *Applicazioni* selezionare **Office 365 Exchange Online**, scegliere **Seleziona** e quindi **Fine**.
  
6. In **Assegnazioni** selezionare **Condizioni** > **Piattaforme del dispositivo**.

   1. In **Configura** selezionare **Sì**.
   2. Nella scheda **Includi** selezionare **Qualsiasi dispositivo** e quindi selezionare **Fine**.

7. Nel riquadro **Condizioni** selezionare **App client**.

   1. In **Configura** selezionare **Sì**.
   2. Selezionare **App per dispositivi mobili e client desktop**.
   3. Selezionare **Client Exchange ActiveSync** e **Applica i criteri solo alle piattaforme supportate**.  
   4. Deselezionare tutte le altre caselle di controllo.  
   5. Selezionare **Fine** e quindi di nuovo **Fine**.  

   ![Applicare alle piattaforme supportate](./media/tutorial-protect-email-on-unmanaged-devices/eas-client-apps.png)  

8. In **Controlli di accesso** selezionare **Concedi**.

   1. Nel riquadro **Concedi** selezionare **Concedi accesso**.
   2. Selezionare **Richiedi app client approvata**. Deselezionare tutte le altre caselle di controllo.
   3. Scegliere **Seleziona**.

   ![Richiedi app client approvata](./media/tutorial-protect-email-on-unmanaged-devices/eas-grant-access.png)

9. In **Attiva criterio** selezionare **Sì** e quindi **Crea**.

I criteri di protezione delle app e l'accesso condizionale sono ora configurati e pronti per il test.

## <a name="try-it-out"></a>Procedura

Con i criteri creati, i dispositivi dovranno essere registrati in Intune e usare l'app Outlook per dispositivi mobili per accedere alla posta elettronica di Microsoft 365. Per testare questo scenario in un dispositivo iOS, provare ad accedere a Exchange Online usando le credenziali di un utente nel tenant di test.

1. Per testare in un iPhone, passare a **Impostazioni** > **Password e account** > **Aggiungi account** > **Exchange**.

2. Immettere l'indirizzo di posta elettronica per un utente nel tenant e quindi premere **Avanti**.  
3. Premere **Accedi**.

4. Immettere la password dell'utente di test e premere **Accedi**.

5. Verrà visualizzato un messaggio per segnalare che **sono necessarie altre informazioni**, ovvero che è necessario configurare l'autenticazione a più fattori. Proseguire e configurare un metodo di verifica aggiuntivo.

6. Verrà quindi visualizzato un messaggio per segnalare che si sta provando ad aprire la risorsa con un'app che non è approvata dal reparto IT. Ciò significa che non si è autorizzati a usare l'app di posta elettronica nativa. Annullare l'accesso.

7. Aprire l'app Outlook e selezionare **Impostazioni** > **Aggiungi account** > **Aggiungi account di posta elettronica**.

8. Immettere l'indirizzo di posta elettronica per un utente nel tenant e quindi premere **Avanti**.

9. Scegliere **Accedi a Office 365** . Verrà chiesto di eseguire operazioni di autenticazione e registrazione aggiuntive. Dopo aver eseguito l'accesso, è possibile testare le azioni, ad esempio le operazioni Taglia, Copia, Incolla e "Salva con nome".

## <a name="clean-up-resources"></a>Pulizia delle risorse

Quando i criteri di test non sono più necessari, è possibile rimuoverli.

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selezionare **Dispositivi** **Criteri di conformità**.

3. Nell'elenco **Nome criteri** selezionare il menu di scelta rapida ( **...** ) per i criteri di test e quindi selezionare **Elimina**. Selezionare **OK** per confermare.

4. Selezionare **Endpoint Security** (Sicurezza degli endpoint) > **Accesso condizionale**.

5. Nell'elenco **Nome criteri** selezionare il menu di scelta rapida ( **...** ) per ciascuno dei criteri di test e quindi selezionare **Elimina**. Selezionare **Sì** per confermare.

## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione sono stati creati criteri di protezione delle app, per limitare le operazioni che gli utenti possono eseguire con l'app Outlook, e criteri di accesso condizionale, per richiedere l'uso dell'app Outlook e dell'autenticazione a più fattori per i client con autenticazione moderna. Per informazioni sull'uso di Intune con l'accesso condizionale per proteggere altri servizi e app, vedere [Configurare l'accesso condizionale](conditional-access.md).
