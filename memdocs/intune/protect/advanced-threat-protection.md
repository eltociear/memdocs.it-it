---
title: Usare Microsoft Defender ATP in Microsoft Intune - Azure | Microsoft Docs
description: Usare Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) con Intune, incluse le operazioni di installazione e configurazione, nonché l'onboarding dei dispositivi Intune in ATP e quindi usare una valutazione dei rischi ATP dei dispositivi con i criteri di conformità e accesso condizionale del dispositivo Intune per proteggere le risorse di rete.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: shpate
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1141879a282219cdac72273e47c84b51df172d04
ms.sourcegitcommit: 397ec824f1368dcf06c3870c89f52347852062bd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/23/2020
ms.locfileid: "85264057"
---
# <a name="enforce-compliance-for-microsoft-defender-atp-with-conditional-access-in-intune"></a>Applicare la conformità per Microsoft Defender ATP con l'accesso condizionale in Intune

È possibile integrare Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) con Microsoft Intune come soluzione Mobile Threat Defense per impedire violazioni della sicurezza e limitare l'impatto delle violazioni all'interno di un'organizzazione. Microsoft Defender ATP funziona con i dispositivi che eseguono Windows 10 o versioni successive e con i dispositivi Android.

Per un funzionamento corretto, usare le configurazioni seguenti insieme:

- **Stabilire una connessione da servizio a servizio fra Intune e Microsoft Defender ATP**. Questa connessione consente a Microsoft Defender ATP di raccogliere dati sul rischio del computer dai dispositivi supportati gestiti con Intune.
- **Usare un profilo di configurazione del dispositivo per eseguire l'onboarding dei dispositivi in Microsoft Defender ATP**. L'onboarding viene eseguito al fine di configurare i dispositivi per comunicare con Microsoft Defender ATP e rendere disponibili i dati che consentono di valutarne il livello di rischio.
- **Usare criteri di conformità del dispositivo per impostare il livello di rischio che si vuole consentire**. I livelli di rischio sono segnalati da Microsoft Defender ATP. I dispositivi che superano il livello di rischio consentito sono identificati come non conformi.
- **Usare criteri di accesso condizionale** per impedire agli utenti di accedere alle risorse aziendali da dispositivi non conformi.

Quando si integra Intune con Microsoft Defender ATP, è possibile sfruttare i vantaggi della gestione di minacce e vulnerabilità di Microsoft Defender ATP e [usare Intune per risolvere le vulnerabilità degli endpoint identificate dalla gestione stessa](atp-manage-vulnerabilities.md).

## <a name="example-of-using-microsoft-defender-atp-with-intune"></a>Esempio d'uso di Microsoft Defender ATP con Intune

L'esempio seguente illustra come queste soluzioni interagiscano per contribuire alla protezione dell'organizzazione. Per questo esempio, Microsoft Defender ATP e Intune sono già integrati.

Si consideri un evento in cui qualcuno invia un allegato di Word con codice dannoso incorporato a un utente all'interno dell'organizzazione.

- L'utente apre l'allegato e abilita il contenuto.
- Viene così avviato un attacco con privilegi elevati, che assegna a un utente malintenzionato che opera da un computer remoto diritti di amministratore sul dispositivo della vittima.
- L'utente malintenzionato accede quindi in remoto agli altri dispositivi dell'utente. Questa violazione della sicurezza può avere ripercussioni sull'intera organizzazione.

Microsoft Defender ATP può aiutare a risolvere eventi di sicurezza simili a quelli descritti in questo scenario.

- In questo esempio Microsoft Defender ATP rileva che il dispositivo ha eseguito codice anomalo, ha sperimentato un'elevazione dei privilegi per un processo, ha inserito codice dannoso e ha eseguito un comando sospetto da shell remota.
- In base a queste azioni del dispositivo, Microsoft Defender ATP [classifica il dispositivo come ad alto rischio](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/alerts-queue#severity) e include un report dettagliato delle attività sospette nel portale Microsoft Defender Security Center.

Poiché sono presenti criteri di conformità dei dispositivi Intune per classificare come non conformi i dispositivi con un livello di rischio *Medio* o *Alto*, il dispositivo compromesso viene classificato come non conforme. Questa classificazione consente di attivare i criteri di accesso condizionale e di bloccare l'accesso dal dispositivo alle risorse aziendali.

È anche possibile usare i criteri di Intune per modificare alcune configurazioni per Microsoft Defender ATP in Android. Per altre informazioni, vedere [Configurare la protezione Web nei dispositivi che eseguono Android](#configure-web-protection-on-devices-that-run-android), più avanti in questo articolo.

## <a name="prerequisites"></a>Prerequisiti

Per usare Microsoft Defender ATP con Intune, verificare che gli elementi seguenti siano configurati e pronti per l'uso:

- Tenant con licenza per Enterprise Mobility + Security E3 e Windows E5 (o Microsoft 365 Enterprise E5)
- Ambiente Microsoft Intune, con dispositivi Windows 10 o Android [gestiti da Intune](../enrollment/windows-enroll.md) che siano anche aggiunti ad Azure AD
- [Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) e accesso a Microsoft Defender Security Center (portale ATP)

> [!NOTE]
> Microsoft Defender ATP non è supportato con i criteri di protezione delle app di Intune per iOS/iPadOS e Android.

## <a name="enable-microsoft-defender-atp-in-intune"></a>Abilitare Microsoft Defender ATP in Intune

Il primo passaggio consiste nel configurare la connessione da servizio a servizio fra Intune e Microsoft Defender ATP. Per questa operazione è necessario l'accesso amministrativo a Microsoft Defender Security Center e a Intune.

### <a name="to-enable-microsoft-defender-atp"></a>Per abilitare Microsoft Defender ATP

È necessario abilitare Microsoft Defender ATP una sola volta per ogni tenant.

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selezionare **Endpoint Security** >  (Sicurezza endpoint) **Microsoft Defender ATP**, quindi selezionare **Aprire Microsoft Defender Security Center**.

   ![Selezionare per aprire Microsoft Defender Security Center](./media/advanced-threat-protection/atp-device-compliance-open-microsoft-defender.png)

3. In **Microsoft Defender Security Center**:
   1. Selezionare **Settings** (Impostazioni)  > **Advanced features** (Funzionalità avanzate).
   2. Per **Microsoft Intune connection** (Connessione Microsoft Intune) selezionare **On** (Attivata):

      ![Abilitare la connessione a Intune](./media/advanced-threat-protection/atp-security-center-intune-toggle.png)

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

## <a name="onboard-windows-devices-by-using-a-configuration-profile"></a>Eseguire l'onboarding dei dispositivi Windows usando un profilo di configurazione

Per la piattaforma Windows, dopo aver stabilito la connessione da servizio a servizio tra Intune e Microsoft Defender ATP, eseguire l'onboarding dei dispositivi gestiti da Intune in Microsoft Defender ATP in modo da poter raccogliere e usare i dati relativi al livello di rischio. Per eseguire l'onboarding dei dispositivi, usare un profilo di configurazione dispositivi per Microsoft Defender ATP.

Quando è stata stabilita la connessione a Microsoft Defender ATP, Intune ha ricevuto un pacchetto di configurazione di onboarding di Microsoft Defender ATP da quest'ultimo. Questo pacchetto viene distribuito ai dispositivi con il profilo di configurazione dispositivi. Il pacchetto di configurazione configura i dispositivi per la comunicazione con i [servizi Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) per analizzare file, rilevare minacce e segnalare il rischio a Microsoft Defender ATP. Dopo l'onboarding di un dispositivo con il pacchetto di configurazione, non è necessario ripetere l'operazione. È possibile eseguire l'onboarding dei dispositivi anche usando un [criterio di gruppo o Microsoft Endpoint Configuration Manager](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints).

### <a name="create-the-device-configuration-profile"></a>Creare il profilo di configurazione dispositivi

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

## <a name="onboard-android-devices"></a>Eseguire l'onboarding dei dispositivi Android
Dopo aver stabilito la connessione da servizio a servizio tra Intune e Microsoft Defender ATP, è necessario eseguire l'onboarding dei dispositivi gestiti in Microsoft Defender ATP in modo da poter raccogliere e usare i dati relativi al livello di rischio.

Per istruzioni dettagliate sull'onboarding di dispositivi Android, inclusi i prerequisiti per gli amministratori e gli utenti finali, vedere [Microsoft Defender Advanced Threat Protection per Android](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-android) nella documentazione di Microsoft Defender ATP.

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

## <a name="configure-web-protection-on-devices-that-run-android"></a>Configurare la protezione Web nei dispositivi che eseguono Android

Per impostazione predefinita, Microsoft Defender ATP per Android include e abilita la funzionalità di protezione Web. [Protezione Web](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/web-protection-overview) consente di proteggere i dispositivi da minacce Web e di proteggere gli utenti da attacchi di phishing.

Anche se è abilitata per impostazione predefinita, esistono motivi validi per disabilitare questa protezione in alcuni dispositivi Android. Ad esempio, è possibile scegliere di usare solo la funzionalità di analisi delle app di Microsoft Defender ATP oppure impedire alla protezione Web di usare la VPN durante l'analisi di URL dannosi.

Intune supporta la disattivazione di tutta o parte della funzionalità di protezione Web. Il metodo usato e le funzionalità che è possibile disabilitare dipendono dal modo in cui il dispositivo Android è registrato in Intune:

- **Amministratore di dispositivi Android**: Usare un profilo di configurazione per specificare impostazioni OMA-URI personalizzate nel dispositivo per disabilitare l'intera funzionalità di protezione Web o per disabilitare solo l'uso di VPN. Per informazioni generali sulle impostazioni personalizzate per i dispositivi Android, vedere [Impostazioni personalizzate](../configuration/custom-settings-android.md).

- **Profilo di lavoro di Android Enterprise**: usare un profilo di configurazione dell'app e la *finestra di progettazione della configurazione* per disabilitare la protezione Web. Questo metodo e il tipo di registrazione supportano la disabilitazione di tutte le funzionalità di protezione Web, ma non supportano la disabilitazione solo dell'uso di VPN. Per informazioni generali sui criteri di configurazione delle app, vedere [Usare la finestra di progettazione della configurazione](../apps/app-configuration-policies-use-android.md#use-the-configuration-designer).

Per configurare la protezione Web nei dispositivi, usare le procedure seguenti per creare e distribuire la configurazione applicabile.

### <a name="disable-web-protection-for-android-device-administrator"></a>Disabilitare la protezione Web per l'amministratore di dispositivi Android

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selezionare **Dispositivi** > **Profili di configurazione** > **Crea profilo**.

3. Immettere le impostazioni seguenti:

   - **Piattaforma**: Selezionare **Amministratore di dispositivi Android**
   - **Profilo**: Selezionare **Personalizzata**

   Selezionare **Crea**.

4. In **Informazioni di base** immettere le informazioni seguenti:

   - **Nome**: immettere un nome descrittivo per il profilo. Assegnare ai profili nomi che possano essere identificati facilmente in un secondo momento. Ad esempio, *Profilo personalizzato Android per la protezione Web di Microsoft Defender ATP*
   - **Descrizione**: Immettere una descrizione del profilo. Questa impostazione è facoltativa ma consigliata.

5. In **Impostazioni di configurazione** selezionare **Aggiungi**.

   Specificare le impostazioni per la configurazione che si vuole distribuire:

   - **Disabilitare la protezione Web**:
     - **Nome**: immettere un nome univoco per questa impostazione OMA-URI in modo da poterla individuare facilmente. Ad esempio, *Disabilitare la protezione Web di Microsoft Defender ATP*
     - **Descrizione**: (facoltativo) immettere una descrizione che offra una panoramica dell'impostazione e altri dettagli importanti.
     - **OMA-URI**: immettere **./Vendor/MSFT/DefenderATP/AntiPhishing**
     - **Tipo di dati**: usare l'elenco a discesa e selezionare **Integer**
     - **Valore**: immettere **0** per disabilitare la protezione Web, inclusa l'analisi basata su VPN.
       > [!NOTE]
       > Immettere **1** per abilitare la protezione Web, ovvero l'impostazione predefinita per la protezione Web.

   - **Disabilitare solo l'uso di reti VPN dalla funzionalità di protezione Web**:
     - **Nome**: immettere un nome univoco per questa impostazione OMA-URI in modo da poterla individuare facilmente. Ad esempio, *Disabilitare VPN per la protezione Web di Microsoft Defender ATP*
     - **Descrizione**: (facoltativo) immettere una descrizione che offra una panoramica dell'impostazione e altri dettagli importanti.
     - **OMA-URI**: immettere **./Vendor/MSFT/DefenderATP/Vpn**
     - **Tipo di dati**: usare l'elenco a discesa e selezionare **Integer**
     - **Valore**: Immettere **0** per disabilitare l'analisi basata su VPN.
       > [!NOTE]
       > Immettere **1** per abilitare la protezione Web, ovvero l'impostazione predefinita per la protezione Web.

   Selezionare **Aggiungi** per salvare la configurazione delle impostazioni OMA-URI, quindi selezionare **Avanti** per continuare.

6. In **Assegnazioni** specificare i gruppi che riceveranno questo profilo. Per altre informazioni sull'assegnazione di profili, vedere [Assegnare profili utente e dispositivo](../configuration/device-profile-assign.md).

7. Al termine, in **Rivedi e crea** scegliere **Crea**. Il nuovo profilo viene visualizzato nell'elenco quando si seleziona il tipo di criterio per il profilo creato.

### <a name="disable-web-protection-for-android-enterprise-work-profile"></a>Disabilitare la protezione Web per il profilo di lavoro di Android Enterprise

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selezionare **App** > **Criteri di configurazione dell'app** > **Aggiungi** e quindi selezionare Dispositivi gestiti.

3. In **Informazioni di base** immettere le informazioni seguenti:

   - **Nome**: immettere un nome descrittivo per il profilo. Assegnare ai profili nomi che possano essere identificati facilmente in un secondo momento. Ad esempio, *Configurazione delle app Android per la protezione Web di Microsoft Defender ATP*.
   - **Descrizione**: Immettere una descrizione del profilo. Questa impostazione è facoltativa ma consigliata.
   - **Piattaforma**: selezionare **Android Enterprise**
   - **Tipo di profilo**: selezionare **Solo profilo di lavoro**
   - **App interessate**: fare clic su **Seleziona app**.

4. In **App associata** individuare e selezionare **Defender ATP** e quindi selezionare **OK** > **Avanti**.

5. In **Impostazioni** usare l'elenco a discesa per **Formato delle impostazioni di configurazione**, selezionare **Usa progettazione configurazione** e quindi fare clic su **Aggiungi**. Verrà aperto l'editor JSON.

6. Individuare e selezionare **Protezione Web** e quindi selezionare **OK** per tornare alla pagina **Impostazioni**.

7. Per **Valore di configurazione** immettere **0** per disabilitare la protezione Web.

   > [!NOTE]
   > Immettere **1** per abilitare la protezione Web, ovvero l'impostazione predefinita per la protezione Web.

   Selezionare **Avanti** per continuare.

8. In **Assegnazioni** specificare i gruppi che riceveranno questo profilo. Per altre informazioni sull'assegnazione di profili, vedere [Assegnare profili utente e dispositivo](../configuration/device-profile-assign.md).

9. Al termine, in **Rivedi e crea** scegliere **Crea**. Il nuovo profilo viene visualizzato nell'elenco quando si seleziona il tipo di criterio per il profilo creato.

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

## <a name="monitor-device-compliance"></a>Monitorare la conformità dei dispositivi

Monitorare lo stato dei dispositivi in cui sono applicati i criteri di conformità di Microsoft Defender ATP.

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selezionare **Dispositivi** > **Monitoraggio** > **Conformità dei criteri**.

3. Trovare il proprio criterio di Microsoft Defender ATP nell'elenco e verificare quali dispositivi sono conformi o non conformi.

È anche possibile usare il report *operativo* per i dispositivi non conformi dallo stesso percorso:

1. Selezionare **Dispositivi** > **Monitoraggio** > **Dispositivi non conformi**.

Per altre informazioni sui report, vedere [Report di Intune](../fundamentals/reports.md).

## <a name="view-onboarding-status"></a>Visualizzare lo stato di onboarding

È possibile visualizzare lo stato di onboarding di tutti i dispositivi gestiti da Intune accedendo a **Sicurezza degli endpoint** > **Microsoft Defender ATP**. Da questa pagina è anche possibile avviare la creazione di un profilo di configurazione dispositivi per l'onboarding di altri dispositivi in Microsoft Defender ATP.

## <a name="next-steps"></a>Passaggi successivi

[Accesso condizionale di Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/conditional-access)

[Dashboard dei rischi di Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/security-operations-dashboard)

[Usare le attività di sicurezza con Vulnerability Management di ATP per risolvere i problemi nei dispositivi](atp-manage-vulnerabilities.md).

[Introduzione ai criteri di conformità dei dispositivi](device-compliance-get-started.md)
