---
title: Configurare Microsoft Defender ATP in Microsoft Intune - Azure | Microsoft Docs
description: Configurare Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) in Intune, inclusi la connessione ad ATP, i dispositivi di onboarding, l'assegnazione della conformità per i livelli di rischio e i criteri di accesso condizionale.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/23/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5e19315f07d803e2aab53b3724fde85f1975c0c5
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/28/2020
ms.locfileid: "87264550"
---
# <a name="configure-microsoft-defender-atp-in-intune"></a>Configurare Microsoft Defender ATP in Intune

Le informazioni e le procedure illustrate in questo articolo consentiranno di configurare l'integrazione di Microsoft Defender ATP con Intune. La configurazione include i passaggi generali seguenti:

- Abilitare Microsoft Defender ATP per il tenant
- Eseguire l'onboarding dei dispositivi che eseguono Windows e Android
- Usare i criteri di conformità per impostare i livelli di rischio dei dispositivi
- Usare i criteri di accesso condizionale per bloccare i dispositivi che superano i livelli di rischio previsti

Prima di iniziare, l'ambiente deve soddisfare i [prerequisiti](../protect/advanced-threat-protection.md#prerequisites) per usare Microsoft Defender ATP con Intune.

## <a name="enable-microsoft-defender-atp-in-intune"></a>Abilitare Microsoft Defender ATP in Intune

Il primo passaggio consiste nel configurare la connessione da servizio a servizio fra Intune e Microsoft Defender ATP. Per eseguire la configurazione è necessario l'accesso amministrativo a Microsoft Defender Security Center e a Intune.

È necessario abilitare Microsoft Defender ATP una sola volta per ogni tenant.

### <a name="to-enable-microsoft-defender-atp"></a>Per abilitare Microsoft Defender ATP

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selezionare **Endpoint Security** >  (Sicurezza endpoint) **Microsoft Defender ATP**, quindi selezionare **Aprire Microsoft Defender Security Center**.

   ![Selezionare per aprire Microsoft Defender Security Center](./media/advanced-threat-protection-configure/atp-device-compliance-open-microsoft-defender.png)

3. In **Microsoft Defender Security Center**:
   1. Selezionare **Settings** (Impostazioni)  > **Advanced features** (Funzionalità avanzate).
   2. Per **Microsoft Intune connection** (Connessione Microsoft Intune) selezionare **On** (Attivata):

      ![Abilitare la connessione a Intune](./media/advanced-threat-protection-configure/atp-security-center-intune-toggle.png)

   3. Selezionare **Save preferences** (Salva preferenze).

4. Tornare a **Microsoft Defender ATP** nell'interfaccia di amministrazione di Microsoft Endpoint Manager. In **MDM Compliance Policy Settings** (Impostazioni dei criteri di conformità MDM), a seconda delle esigenze aziendali:
   - Impostare **Connetti i dispositivi Windows con versione 10.0.15063 e successiva a Microsoft Defender ATP** su **Attivato**
   - Impostare **Connect Android devices of version 6.0.0 and above to Microsoft Defender ATP** (Connetti i dispositivi Android con versione 6.0.0 e successiva a Microsoft Defender ATP) su **On** (Attivato)

5. Selezionare **Salva**.

> [!TIP]
> Quando si integra una nuova applicazione in Intune Mobile Threat Defense e si abilita la connessione per Intune, Intune crea criteri di accesso condizionale classici in Azure Active Directory. Ogni app MTD integrata, inclusi [Microsoft Defender ATP](advanced-threat-protection.md) o uno qualsiasi dei [partner MTD](mobile-threat-defense.md#mobile-threat-defense-partners) aggiuntivi, crea nuovi criteri di accesso condizionale classici. Questi criteri possono essere ignorati, ma non devono essere modificati, eliminati o disabilitati.
>
> Se i criteri classici vengono eliminati, sarà necessario eliminare la connessione a Intune che li ha creati e poi riconfigurarla. In questo modo si ricreano i criteri classici. Non è possibile eseguire la migrazione dei criteri classici per le app MTD al nuovo tipo di criteri per l'accesso condizionale.
>
> I criteri di accesso condizionale classici per le app gestite:
>
> - Vengono usati da Intune MTD per richiedere che i dispositivi vengano registrati in Azure AD in modo da avere un ID dispositivo prima di comunicare con i partner MTD. L'ID è necessario per consentire ai dispositivi di segnalare correttamente lo stato a Intune.
> - Non ha alcun effetto su altre app o risorse cloud.
> - Sono diversi dai criteri di accesso condizionale che è possibile creare per facilitare la gestione di MTD.
> - Per impostazione predefinita, non interagiscono con altri criteri di accesso condizionale usati per la valutazione.
>
> Per visualizzare i criteri di accesso condizionale classici, in [Azure](https://portal.azure.com/#home) passare a **Azure Active Directory** > **Accesso condizionale** > **Criteri classici**.

## <a name="onboard-devices"></a>Eseguire l'onboarding dei dispositivi

Quando è stato abilitato il supporto per Microsoft Defender ATP in Intune, è stata stabilita una connessione da servizio a servizio tra Intune e Microsoft Defender ATP. È quindi possibile eseguire l'onboarding dei dispositivi gestiti con Intune in Microsoft Defender ATP per consentire la raccolta di dati sui livelli di rischio dei dispositivi.

### <a name="onboard-windows-devices"></a>Eseguire l'onboarding di dispositivi Windows

Quando è stata stabilita la connessione tra Intune e Microsoft Defender ATP, Intune ha ricevuto un pacchetto di configurazione di onboarding di Microsoft Defender ATP da quest'ultimo. Questo pacchetto di configurazione viene distribuito nei dispositivi Windows con un profilo di configurazione del dispositivo per Microsoft Defender ATP.

Il pacchetto di configurazione configura i dispositivi per la comunicazione con i [servizi Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) per analizzare file e rilevare minacce. Il dispositivo viene configurato anche per segnalare a Microsoft Defender ATP il livello di rischio dei dispositivi in base ai criteri di conformità che verranno creati.

Dopo aver eseguito l'onboarding di un dispositivo con il pacchetto di configurazione, non è necessario ripetere l'operazione. È possibile eseguire l'onboarding dei dispositivi anche usando un [criterio di gruppo o Microsoft Endpoint Configuration Manager](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints).

### <a name="create-the-device-configuration-profile-to-onboard-windows-devices"></a>Creare il profilo di configurazione del dispositivo per eseguire l'onboarding dei dispositivi Windows

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selezionare **Dispositivi** > **Profili di configurazione** > **Crea profilo**.
3. Immettere un **nome** e una **descrizione**.
4. In **Piattaforma** selezionare **Windows 10 e versioni successive**.
5. In **Tipo di profilo** selezionare **Microsoft Defender ATP (Windows 10 Desktop)** .
6. Configurare le impostazioni:

   - **Tipo del pacchetto di configurazione client di Microsoft Defender ATP**: selezionare **Onboarding** per aggiungere il pacchetto di configurazione al profilo. Selezionare **Offboarding** per rimuovere il pacchetto di configurazione dal profilo.
  
     > [!NOTE]
     > Se è stata stabilita correttamente una connessione a Microsoft Defender ATP, Intune esegue automaticamente l'**onboarding** del profilo di configurazione e l'impostazione **Tipo del pacchetto di configurazione client di Microsoft Defender ATP** non sarà disponibile.
  
   - **Condivisione di esempi per tutti i file**: **Abilita** consente di raccogliere gli esempi e di condividerli con Microsoft Defender ATP. Ad esempio, se viene rilevato un file sospetto, è possibile inviarlo a Microsoft Defender ATP per un'analisi approfondita. **Non configurato** non condivide alcun esempio con Microsoft Defender ATP.
   - **Accelera la frequenza di creazione di report di telemetria**: **abilitare** questa impostazione per i dispositivi ad alto rischio, in modo che i dati di telemetria vengano segnalati più frequentemente al servizio Microsoft Defender ATP.

     Per informazioni più dettagliate su queste impostazioni di Microsoft Defender ATP, vedere [Eseguire l'onboarding di computer Windows 10 tramite Microsoft Endpoint Configuration Manager](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints-sccm).

7. Scegliere **OK** e quindi **Crea** per salvare le modifiche e creare il profilo.
8. [Assegnare il profilo di configurazione dispositivi](../configuration/device-profile-assign.md) ai dispositivi da valutare con Microsoft Defender ATP.

### <a name="onboard-android-devices"></a>Eseguire l'onboarding dei dispositivi Android

Dopo aver stabilito la connessione da servizio a servizio tra Intune e Microsoft Defender ATP, è possibile eseguire l'onboarding dei dispositivi Android in Microsoft Defender ATP. L'onboarding configura i dispositivi per la comunicazione con Defender ATP che quindi raccoglie i dati sul livello di rischio dei dispositivi.

Diversamente da quanto avviene per i dispositivi Windows, non è disponibile un pacchetto di configurazione per i dispositivi che eseguono Android. Vedere invece [Panoramica di Microsoft Defender ATP per Android](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-android) nella documentazione di Microsoft Defender ATP per i prerequisiti e le istruzioni per l'onboarding per Android.

Per i dispositivi che eseguono Android, è anche possibile usare i criteri di Intune per modificare Microsoft Defender ATP in Android. Per altre informazioni, vedere [Protezione Web di Microsoft Defender ATP](../protect/advanced-threat-protection-manage-android.md).

## <a name="create-and-assign-compliance-policy-to-set-device-risk-level"></a>Creare e assegnare i criteri di conformità per impostare il livello di rischio del dispositivo

Per i dispositivi Windows e Android, i criteri di conformità determinano il livello di rischio considerato accettabile per un dispositivo.

Se non si ha familiarità con la creazione dei criteri di conformità, fare riferimento alla procedura [Creare un criterio](../protect/create-compliance-policy.md#create-the-policy) nell'articolo *Creare criteri di conformità in Microsoft Intune*. Le informazioni seguenti sono specifiche per la configurazione di Microsoft Defender ATP nell'ambito dei criteri di conformità.

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selezionare **Dispositivi** > **Criteri di conformità** > **Criteri** > **Crea criterio**.

3. Per **Piattaforma** usare la casella di riepilogo a discesa per selezionare una delle opzioni seguenti:
   - **Windows 10 e versioni successive**
   - **Amministratore di dispositivi Android**
   - **Android Enterprise**

   Selezionare quindi **Crea** per aprire la finestra di configurazione **Crea criterio**.

4. Specificare un **Nome** per identificare facilmente i criteri in un secondo momento. È anche possibile specificare una **Descrizione**.
  
5. Nella scheda **Impostazioni di conformità** espandere il gruppo **Microsoft Defender ATP** e impostare l'opzione **Richiedi che il dispositivo si trovi al massimo al punteggio di rischio del computer** sul livello preferito.

   Le classificazioni dei livelli delle minacce vengono [determinate da Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/alerts-queue).

   - **Cancella**: questo livello è il più sicuro. Nel dispositivo non possono essere presenti minacce per poter accedere alle risorse aziendali. Se viene rilevata qualsiasi minaccia, il dispositivo viene valutato come non conforme. Microsoft Defender ATP usa il valore *Sicuro*.
   - **Bassa**: il dispositivo è conforme se sono presenti solo minacce di livello basso. I dispositivi con un livello di minaccia medio o alto non sono conformi.
   - **Media**: il dispositivo è conforme se le minacce presenti nel dispositivo sono di livello basso o medio. Se viene rilevata la presenza di minacce di livello alto, il dispositivo viene determinato come non conforme.
   - **Alta**: questo livello è il meno sicuro e consente tutti i livelli di minaccia. Sono considerati conformi i dispositivi con un livello di minaccia alto, medio o basso.

6. Completare la configurazione dei criteri, inclusa l'assegnazione dei criteri ai gruppi applicabili.


## <a name="create-a-conditional-access-policy"></a>Creare criteri di accesso condizionale

I criteri di accesso condizionale possono usare i dati di Microsoft Defender ATP per bloccare l'accesso alle risorse per i dispositivi che superano il livello di minaccia impostato. È possibile bloccare l'accesso dal dispositivo alle risorse aziendali, ad esempio SharePoint o Exchange Online.

> [!TIP]
> L'accesso condizionale è una tecnologia di Azure Active Directory (Azure AD). Il nodo *Accesso condizionale* nell'interfaccia di amministrazione di Microsoft Endpoint Manager è il nodo da *Azure AD*.

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selezionare **Endpoint Security** (Sicurezza endpoint) > **Accesso condizionale** > **Nuovi criteri**.

3. Immettere un **nome** per il criterio e selezionare **Utenti e gruppi**. Usare l'opzione Includi o Escludi per aggiungere i gruppi per il criterio e selezionare **Fatto**.

4. Selezionare **App cloud** e scegliere le app da proteggere. Ad esempio, scegliere **Seleziona le app** e quindi selezionare **Office 365 SharePoint Online**e **Office 365 Exchange Online**.

   Selezionare **Fatto** per salvare le modifiche.

5. Selezionare **Condizioni** > **App client** per applicare il criterio alle app e ai browser. Ad esempio, selezionare **Sì** e quindi abilitare **Browser** e **App per dispositivi mobili e client desktop**.

   Selezionare **Fatto** per salvare le modifiche.

6. Selezionare **Concedi** per applicare l'accesso condizionale basato sulla conformità del dispositivo. Ad esempio, selezionare **Concedi accesso** > **Richiedi che i dispositivi siano contrassegnati come conformi**.

    Scegliere **OK** per salvare le modifiche.

7. Selezionare **Abilita criterio** e quindi **Crea** per salvare le modifiche.

## <a name="next-steps"></a>Passaggi successivi

- [Configure le impostazioni di Microsoft Defender ATP in Android](../protect/advanced-threat-protection-manage-android.md)
- [Monitorare la conformità per i livelli di rischio](../protect/advanced-threat-protection-monitor.md)

Per altre informazioni, vedere la documentazione di Intune:

- [Usare le attività di sicurezza con Vulnerability Management di ATP per risolvere i problemi nei dispositivi](atp-manage-vulnerabilities.md)
- [Introduzione ai criteri di conformità dei dispositivi](device-compliance-get-started.md)

Per altre informazioni, vedere la documentazione di Microsoft Defender ATP:

- [Accesso condizionale di Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/conditional-access)
- [Dashboard dei rischi di Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/security-operations-dashboard)
