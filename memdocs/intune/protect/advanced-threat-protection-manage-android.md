---
title: Gestire la protezione Web di Microsoft Defender ATP per dispositivi Android in Microsoft Intune - Azure | Microsoft Docs
description: Configurare la protezione Web di Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) per Android in Intune.
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
ms.openlocfilehash: 49423d1d1b887aaf3ed3323ff36678bb7319b1ad
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/26/2020
ms.locfileid: "88909466"
---
# <a name="configure-microsoft-defender-atp-on-android-devices-you-manage-with-intune"></a>Configurare Microsoft Defender ATP nei dispositivi Android gestiti con Intune

Quando si integrano Microsoft Intune e Microsoft Defender Advanced Threat Protection (ATP), è possibile usare i profili di configurazione dei dispositivi per modificare alcune impostazioni di Microsoft Defender ATP nei dispositivi Android.

Prima di procedere, è necessario [configurare Microsoft Defender ATP in Intune](../protect/advanced-threat-protection-configure.md) ed eseguire l'onboarding dei dispositivi Android in Microsoft Defender ATP.

## <a name="configure-web-protection-on-devices-that-run-android"></a>Configurare la protezione Web nei dispositivi che eseguono Android

Per impostazione predefinita, Microsoft Defender ATP per Android include e abilita la funzionalità di protezione Web. [Protezione Web](/windows/security/threat-protection/microsoft-defender-atp/web-protection-overview) consente di proteggere i dispositivi da minacce Web e di proteggere gli utenti da attacchi di phishing.

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

## <a name="next-steps"></a>Passaggi successivi

- [Monitorare la conformità per i livelli di rischio](../protect/advanced-threat-protection-monitor.md)
- [Usare le attività di sicurezza con Vulnerability Management di ATP per risolvere i problemi nei dispositivi](../protect/atp-manage-vulnerabilities.md)

Per altre informazioni, vedere la documentazione di Microsoft Defender ATP:

- [Accesso condizionale di Microsoft Defender ATP](/windows/security/threat-protection/microsoft-defender-atp/conditional-access)
- [Dashboard dei rischi di Microsoft Defender ATP](/windows/security/threat-protection/microsoft-defender-atp/security-operations-dashboard)