---
title: Controllare l'esito positivo o negativo delle baseline di sicurezza in Microsoft Intune - Azure | Microsoft Docs
description: Controllare lo stato di errore, conflitto ed esito positivo quando si distribuiscono baseline di sicurezza a utenti e dispositivi in Microsoft Intune MDM. Informazioni su come risolvere i problemi mediante i log del client e le funzionalità di report in Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: laarrizz
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1ccf9801c7a5977485c6c1864a69be2e46a4af55
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/26/2020
ms.locfileid: "88914872"
---
# <a name="monitor-security-baselines-and-profiles-in-microsoft-intune"></a>Monitorare le baseline di sicurezza e i profili in Microsoft Intune

Intune offre diverse opzioni per monitorare le baseline di sicurezza. È possibile scegliere:

- Monitorare una baseline di sicurezza e tutti i dispositivi corrispondenti (o non corrispondenti) ai valori consigliati.
- Monitorare il profilo delle baseline di sicurezza applicabile a utenti e dispositivi.
- Vedere come sono configurate le impostazioni di un profilo selezionato in un dispositivo selezionato.

È anche possibile visualizzare le *configurazioni di sicurezza degli endpoint* applicabili a singoli dispositivi, che includono le baseline di sicurezza.

Questo articolo illustra queste opzioni di monitoraggio.

In [Baseline di sicurezza in Intune](security-baselines.md) sono disponibili maggiori dettagli sulla funzionalità delle baseline di sicurezza in Microsoft Intune.

## <a name="monitor-the-baseline-and-your-devices"></a>Monitorare la baseline e i dispositivi

Quando si monitora una baseline, si ottengono informazioni dettagliate sullo stato di sicurezza dei dispositivi in base ai consigli di Microsoft. Per visualizzare queste informazioni dettagliate, accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), passare a **Sicurezza degli endpoint** > **Baseline di sicurezza** e selezionare un tipo di baseline di sicurezza come *Baseline di sicurezza di MDM*. Nel riquadro *Profilo* selezionare quindi l'istanza del profilo per cui si vogliono visualizzare i dettagli. Verrà aperto il riquadro *Proprietà* dei profili in cui è possibile selezionare uno dei report del profilo nella sezione *Monitoraggio*. 

Sono necessarie fino a 24 ore prima che i dati vengano visualizzati dopo che si assegna per la prima volta una baseline. La visualizzazione delle modifiche apportate successivamente può richiedere fino a sei ore.

Quando si esegue il drill-in in report e dispositivi, sono disponibili vari dettagli.

<!-- UI is changing, unclear how yet: 


- **Device view** – A summary of how many devices are in each status category for the baseline.
- **Per-category** - A view that displays each category in the baseline and includes the percentage of devices for each status group for each baseline category.

Each device is represented by one of the following statuses (used in the *device* view and also the *per-category* views):

- **Matches baseline** - All the settings in the baseline match the recommended settings.
- **Does not match baseline** - One or more settings in the baseline were modified from their default values in the original baseline. The default values in each security baseline are the recommended values for that baseline.

  > [!NOTE]
  > When you create or edit a baseline profile, any change that is made to a default value or configuration setting causes a *Does not match baseline* status to occur. For help to determine the settings that were changed, contact Microsoft Support. 

- **Misconfigured** - At least one setting isn't correctly configured. This status means that the setting is in a conflict, error, or pending state.
- **Not applicable** - At least one setting isn't applicable and isn't applied.

### Device view

The Overview pane displays a chart-based summary of how many devices have a specific status for the baseline; **Security baseline posture for assigned Windows 10 devices**.

![Check the status of the devices](./media/security-baselines-monitor/overview.png)

When a device has different status from different categories in the baseline, the device is represented by a single status. The status that represents the device is taken from the following order of precedence: **Misconfigured**, **Does not match baseline**, **Not applicable**, **Matches baseline**.

For example, if a device has a setting that's classified as *misconfigured* and one or more settings that are classified as *Does not match baseline*, the device is classified as *Misconfigured*.

You can click on the chart to drill through and view a list of devices with various statuses. You can then select individual devices from that list to view details about individual devices. For example:

- Select **Device configuration** > Select the profile with an Error state:

  ![View the status of a profile](./media/security-baselines-monitor/device-configuration-profile-list.png)

- Select the Error profile. A list of all settings in the profile, and their state is shown. Now, you can scroll to find the setting causing the error:

  ![See the setting causing the error](./media/security-baselines-monitor/profile-with-error-status.png)

Use this reporting to see any settings in a profile that are causing an issue. Also get more details of policies and profiles deployed to devices.

> [!NOTE]
> When a property is set to **Not configured** in the baseline, the setting is ignored, and no restrictions are enforced. The property isn't shown in any reporting.

### Per category view

The Overview pane displays a per-category chart for the baseline named **Security baseline posture by category**.  This view displays each category from the baseline, and identifies the percentage of devices that fall into a status classification for each of those categories.

![Per-Category view of status](./media/security-baselines-monitor/monitor-baseline-per-category.png)

Status for **Matches baseline** doesn't display until 100% of devices report that status for the category.

You can sort the by-category view by each column, by selecting up-down arrow icon at the top of the column.
-->

## <a name="monitor-the-profile"></a>Monitorare il profilo

Il monitoraggio del profilo offre informazioni dettagliate sullo stato di distribuzione dei dispositivi, ma non sullo stato di sicurezza basato sulle raccomandazioni della baseline.

1. In Intune selezionare **Baseline di sicurezza** e quindi selezionare una baseline per aprire il riquadro *Profili* corrispondente.

<!-- More churn  
2. Select a profile. In **Overview**, the image shows how many devices and users have this profile assigned:

   ![See how many devices and users are assigned the security baselines profile](./media/security-baselines-monitor/existing-profile-overview.png)
--> 
3. In **Gestisci** > **Proprietà** viene visualizzato un elenco di tutte le impostazioni nella baseline. È anche possibile modificare queste impostazioni:

   ![Visualizzare e aggiornare le impostazioni nel profilo delle baseline di sicurezza](./media/security-baselines-monitor/manage-settings.png)

4. In **Monitoraggio** è possibile visualizzare lo stato di distribuzione del profilo in singoli dispositivi, lo stato per ogni utente e lo stato per ogni impostazione nella baseline:

   ![Visualizzare le diverse opzioni di monitoraggio per un profilo di baseline di sicurezza](./media/security-baselines-monitor/monitor-status-options.png)

## <a name="view-settings-from-profiles-that-apply-to-a-device"></a>Visualizzare le impostazioni dai profili che si applicano a un dispositivo

È possibile selezionare un profilo per una baseline di sicurezza ed eseguire il drill-in per visualizzare un elenco di impostazioni dal profilo che si applicano a un singolo dispositivo.  Per visualizzare l'elenco, passare a **Sicurezza degli endpoint** > **Baseline di sicurezza** > *selezionare il tipo di baseline di sicurezza* > *selezionare il profilo che si vuole visualizzare* > **Stato dispositivo**. Per visualizzare l'elenco, è anche possibile passare a **Sicurezza degli endpoint** > **Tutti i dispositivi** > *selezionare un dispositivo* > **Configurazione sicurezza endpoint** > *selezionare una versione della baseline*.

Dopo aver selezionato un dispositivo, l'interfaccia di amministrazione di Microsoft Endpoint Manager visualizza un elenco delle impostazioni da tale profilo, inclusa la categoria di appartenenza dell'impostazione e lo stato di configurazione nel dispositivo. Gli stati di configurazione includono i valori seguenti:

- **Operazione riuscita** - L'impostazione del dispositivo corrisponde al valore configurato nel profilo. Si tratta del valore predefinito e consigliato per le baseline oppure di un valore personalizzato specificato da un amministratore al momento della configurazione del profilo.
- **Conflitto** - L'impostazione è in conflitto con un altro criterio, presenta un errore o è in attesa di un aggiornamento.
- **Non applicabile** - L'impostazione non viene applicata dal profilo.

> [!NOTE]
> I valori di stato per le impostazioni verranno aggiornati in una versione futura per fornire maggiori dettagli.

## <a name="view-endpoint-security-configurations-per-device"></a>Visualizzare le configurazioni della sicurezza degli endpoint per dispositivo

Visualizzare i dettagli sulle configurazioni della sicurezza applicabili a un singolo dispositivo, che consentono di isolare le impostazioni che non sono configurate correttamente.

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Passare a **Dispositivi**  > **Tutti i dispositivi** e selezionare il dispositivo da visualizzare.

3. Nella categoria *Monitor* selezionare **Configurazione della sicurezza degli endpoint** per visualizzare l'elenco delle configurazioni della sicurezza applicabili al dispositivo.

4. È possibile selezionare una configurazione della sicurezza degli endpoint per eseguire il drill-down e visualizzare altri dettagli sulla valutazione di tale configurazione della sicurezza nel dispositivo.

## <a name="troubleshoot-using-per-setting-status"></a>Risolvere i problemi con lo stato per singola impostazione

Si supponga di aver distribuito una baseline di sicurezza, ma che lo stato di distribuzione indichi un errore. La procedura seguente offre alcune indicazioni per la risoluzione dell'errore.

1. In Intune selezionare **Baseline di sicurezza** > selezionare una baseline > **Profili**.

2. Selezionare un profilo > in **Monitoraggio** > **Stato per singola impostazione**.

3. La tabella mostra tutte le impostazioni e lo stato di ognuna. Selezionare la colonna **Errore** o la colonna **Conflitto** per visualizzare l'impostazione che causa l'errore.

### <a name="mdm-diagnostic-information"></a>Informazioni di diagnostica MDM

A questo punto è stata individuata l'impostazione problematica. Il passaggio successivo consiste nello scoprire il motivo per cui questa impostazione sta causando un errore o un conflitto.

Nei dispositivi Windows 10 è disponibile un report di informazioni diagnostiche MDM predefinito. Questo report include i valori predefiniti, i valori correnti, elenca i criteri, mostra se sono distribuiti per il dispositivo o per l'utente e altro ancora. Usare questo report per determinare il motivo per cui l'impostazione sta causando un conflitto o un errore.

1. Nel dispositivo passare a **Impostazioni** > **Account** > **Accedi all'azienda o all'istituto di istruzione**.

2. Selezionare l'account > **Informazioni** > **Advanced Diagnostic Report** > **Create report** (Report di diagnostica avanzato, Crea report).

3. Scegliere **Esporta** e aprire il file generato.

4. Nel report cercare l'impostazione con errore o conflitto nelle diverse sezioni del report.

  Ad esempio, cercare nella sezione **Enrolled configuration sources and target resources** (Origini di configurazione registrate e risorse di destinazione) o nella sezione **Unmanaged policies** (Criteri non gestiti). È possibile farsi un'idea del motivo per cui l'impostazione causa un errore o un conflitto.

In [Diagnose MDM failures in Windows 10](/windows/client-management/mdm/diagnose-mdm-failures-in-windows-10) (Diagnosticare gli errori MDM in Windows 10) sono disponibili altre informazioni su questo report predefinito.

> [!TIP]
>
> - Per alcune impostazioni viene elencato anche il GUID. È possibile cercare questo GUID nel Registro di sistema locale (regedit) per verificare gli eventuali valori impostati.
> - Anche i log di Visualizzatore eventi potrebbero includere alcune informazioni sull'errore dell'impostazione problematica (**Visualizzatore eventi** > **Registri applicazioni e servizi** > **Microsoft** > **Windows** > **DeviceManagement-Enterprise-Diagnostics-Provider** > **Amministratore**).

## <a name="next-steps"></a>Passaggi successivi

- [Informazioni sulle baseline di sicurezza](security-baselines.md)
- [Evitare conflitti](security-baselines.md#avoid-conflicts)
- [Monitorare i profili di dispositivo](../configuration/device-profile-monitor.md) 
- [Problemi e risoluzioni comuni](../configuration/device-profile-troubleshoot.md)
- [Risolvere problemi relativi a criteri e profili in Intune](../configuration/troubleshoot-policies-in-microsoft-intune.md)