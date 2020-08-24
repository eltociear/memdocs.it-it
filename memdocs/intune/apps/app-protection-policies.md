---
title: Creare e distribuire i criteri di protezione delle app
titleSuffix: Microsoft Intune
description: Questo argomento illustra come creare e assegnare criteri di protezione delle app di Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 08/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: f31b2964-e932-4cee-95c4-8d5506966c85
ms.reviewer: joglocke
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1cb05cb518d4edfb443bf4f70ff1c51154e17f4c
ms.sourcegitcommit: 1aeb4a11e89f68e8081d76ab013aef6b291c73c1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/14/2020
ms.locfileid: "88217639"
---
# <a name="how-to-create-and-assign-app-protection-policies"></a>Come creare e assegnare criteri di protezione delle app

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Informazioni su come creare e assegnare criteri di protezione delle app di Microsoft Intune per gli utenti dell'organizzazione. In questo argomento viene anche descritto come apportare modifiche a criteri esistenti.

## <a name="before-you-begin"></a>Prima di iniziare

I criteri di protezione delle app possono essere applicati in app eseguite su dispositivi gestiti o non gestiti da Intune. Per una descrizione più dettagliata del funzionamento dei criteri di protezione delle app e degli scenari supportati dai criteri di protezione delle app di Intune, vedere la [Panoramica dei criteri di protezione app](app-protection-policy.md).

Le scelte disponibili sui criteri di protezione delle app (APP) consentono alle organizzazioni di adattare la protezione alle proprie esigenze specifiche. Per alcuni utenti potrebbe non essere semplice individuare le impostazioni dei criteri necessarie per implementare uno scenario completo. Per aiutare le organizzazioni a dare la priorità alla protezione avanzata degli endpoint di client mobili, Microsoft ha introdotto la tassonomia per il framework di protezione dei dati dell'APP per la gestione di dispositivi mobili iOS e Android.

Il framework di protezione dei dati dell'APP è organizzato in tre livelli di configurazione distinti, ognuno dei quali si basa sul livello precedente:

- **Protezione di base dei dati aziendali** (livello 1) garantisce che le app siano protette con un PIN e crittografate ed esegue operazioni di cancellazione selettiva. Per i dispositivi Android questo livello convalida l'attestazione dei dispositivi Android. Si tratta di una configurazione a livello di voce che offre un controllo simile di protezione dei dati nei criteri della cassetta postale di Exchange Online e introduce l'IT e la popolazione di utente nell'APP.
- **Protezione avanzata dei dati aziendali** (livello 2) introduce i meccanismi di protezione della perdita dei dati aziendali dell'APP e i requisiti minimi del sistema operativo. Questa configurazione è applicabile alla maggior parte degli utenti di dispositivi mobili che accedono ai dati aziendali o dell'istituto di istruzione.
- **Protezione elevata dei dati aziendali** (livello 3) introduce meccanismi avanzati per la protezione dei dati, configurazione del PIN avanzata e Mobile Threat Defense dell'APP. Questa configurazione è utile per gli utenti che accedono a dati ad alto rischio.

Per visualizzare le raccomandazioni specifiche per ciascun livello di configurazione e le app minime che devono essere protette, consultare il [Framework di protezione dei dati con criteri di protezione delle app](app-protection-framework.md).

Se si sta cercando un elenco di app che hanno integrato Intune SDK, vedere [App protette di Microsoft Intune](apps-supported-intune-apps.md).

Per informazioni sull'aggiunta di app line-of-business (LOB) dell'organizzazione in Microsoft Intune per preparare i criteri di protezione delle app, vedere [Aggiungere app in Microsoft Intune](apps-add.md).

## <a name="app-protection-policies-for-iosipados-and-android-apps"></a>Criteri di protezione delle app per app iOS/iPadOS e Android

Quando si crea un criterio di protezione delle app per app iOS/iPadOS e Android, si segue un flusso di processo di Intune moderno che comporta la creazione di un nuovo criterio di protezione delle app. Per informazioni sulla creazione di criteri di protezione delle app per app Windows, vedere [Creare e distribuire i criteri di Windows Information Protection (WIP) con Intune](../apps/windows-information-protection-policy-create.md).

### <a name="create-an-iosipados-or-android-app-protection-policy"></a>Creare un criterio di protezione delle app iOS/iPadOS o Android

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Nel portale di Intune scegliere **App** > **Criteri di protezione delle app**. Questa selezione determina la visualizzazione dei dettagli dei **Criteri di protezione delle app**, in cui è possibile creare nuovi criteri e modificare i criteri esistenti.
3. Selezionare **Crea criteri** e selezionare **iOS/iPadOS** o **Android**. Viene visualizzato il riquadro **Crea criterio**.
4. Nella pagina **Informazioni di base** aggiungere i valori seguenti:

    | Valore | Descrizione |
    |--------------|------------------------------------------------|
    | Name | Nome dei criteri di protezione delle app. |
    | Descrizione | [Facoltativo] Descrizione dei criteri di protezione delle app. |


    Il valore **Piattaforma** viene impostato in base alla scelta effettuata in precedenza.

    ![Screenshot della pagina Informazioni di base del riquadro Crea criterio](./media/app-protection-policies/app-protection-add-policies-01.png)

5. Fare clic su **Avanti** per visualizzare la pagina **App**.<br>
    La pagina **App** consente di scegliere come applicare questo criterio alle app su dispositivi diversi. È necessario aggiungere almeno un'app.<p>

    | Valore/opzione | Descrizione |
    |-------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
    | Specifica come destinatari le app in tutti i tipi di dispositivo | Usare questa opzione per destinare i criteri alle app nei dispositivi con qualsiasi stato di gestione. Scegliere **No** per destinare i criteri ad app su tipi di dispositivi specifici. Per altre informazioni, vedere [Assegnare i criteri di protezione delle app in base allo stato di gestione del dispositivo](#target-app-protection-policies-based-on-device-management-state) |
    |     Tipi di dispositivi | Usare questa opzione per specificare se i criteri di applicano ai dispositivi gestiti MDM o ai dispositivi non gestiti. Per i criteri di protezione delle app iOS/iPadOS selezionare **Non gestito** o **Gestito** per i dispositivi. Per i criteri di protezione delle app Android selezionare **Non gestito**, **Amministratore di dispositivi Android** e **Android Enterprise**.  |
    | App pubbliche | Fare clic su **Select public apps** (Selezionare le app pubbliche) per scegliere le app di destinazione. |
    | App personalizzate | Fare clic su **Select custom apps** (Selezionare le app personalizzate) per selezionare le app personalizzate di destinazione in base a un ID di bundle. |

    Le app selezionate verranno visualizzate nell'elenco delle app pubbliche e personalizzate.
6. Fare clic su **Avanti** per visualizzare la pagina **Protezione dei dati**.<br>
    Questa pagina fornisce le impostazioni per i controlli di prevenzione della perdita dei dati (DLP), incluse le limitazioni per le operazioni Taglia, Copia, Incolla e Salva con nome. Queste impostazioni determinano il modo in cui gli utenti interagiscono con i dati nelle app a cui vengono applicati questi criteri di protezione delle app.

    **Impostazioni di protezione dati**:<br>
    - **Protezione dati iOS/iPadOS** - Per informazioni, vedere [Impostazioni dei criteri di protezione delle app per iOS/iPadOS - Protezione dati](app-protection-policy-settings-ios.md#data-protection).
    - **Protezione dati Android** - Per informazioni, vedere [Impostazioni dei criteri di protezione delle app per Android - Protezione dati](app-protection-policy-settings-android.md#data-protection).

7. Fare clic su **Avanti** per visualizzare la pagina **Requisiti di accesso**.<br>
    Questa pagina fornisce le impostazioni che consentono di configurare i requisiti di PIN e credenziali che gli utenti devono soddisfare per accedere alle app in un contesto aziendale.
 
    **Impostazioni dei requisiti di accesso**:<br>
    - **Requisiti di accesso per iOS/iPadOS** - Per informazioni, vedere [Impostazioni dei criteri di protezione delle app per iOS/iPadOS - Requisiti di accesso](app-protection-policy-settings-ios.md#access-requirements).
    - **Requisiti di accesso per Android** - Per informazioni, vedere [Impostazioni dei criteri di protezione delle app per Android - Requisiti di accesso](app-protection-policy-settings-android.md#access-requirements).

8. Fare clic su **Avanti** per visualizzare la pagina **Avvio condizionale**.<br>
    Questa pagina fornisce le impostazioni per impostare i requisiti di sicurezza per l'accesso per i criteri di protezione delle app. Selezionare una **impostazione** e immettere il **valore** che gli utenti devono soddisfare per accedere all'app aziendale. Selezionare l'**azione** da intraprendere se gli utenti non soddisfano i requisiti. In alcuni casi è possibile configurare più azioni per una singola impostazione.

    **Impostazioni di avvio condizionale**:<br>
    - **Avvio condizionale per iOS/iPadOS** - Per informazioni, vedere [Impostazioni dei criteri di protezione delle app per iOS/iPadOS - Avvio condizionale](app-protection-policy-settings-ios.md#conditional-launch).
    - **Avvio condizionale per Android** - Per informazioni, vedere [Impostazioni dei criteri di protezione delle app per Android - Avvio condizionale](app-protection-policy-settings-android.md#conditional-launch).

9. Fare clic su **Avanti** per visualizzare la pagina **Assegnazioni**.<br>
   La pagina **Assegnazioni** consente di assegnare i criteri di protezione delle app a gruppi di utenti. Per rendere effettivi i criteri, è necessario applicarli a un gruppo di utenti.

10. Fare clic su **Avanti: Rivedi e crea** per esaminare i valori e le impostazioni immessi per i criteri di protezione delle app.

11. Al termine, fare clic su **Crea** per creare i criteri di protezione delle app in Intune.

    > [!TIP]
    > Queste impostazioni dei criteri vengono applicate solo quando si usano le app nel contesto aziendale. Quando gli utenti finali usano l'app per eseguire un'attività personale, questi criteri non hanno effetto. Si noti che ogni nuovo file creato viene considerato un file personale.

    > [!IMPORTANT]
    > L'applicazione dei criteri di protezione delle app ai dispositivi esistenti può richiedere del tempo. Quando i criteri saranno applicati, gli utenti finali riceveranno una notifica sul dispositivo. Applicare i criteri di protezione delle app ai dispositivi prima di applicare le regole di accesso condizionale.

Gli utenti finali possono scaricare le app dall'Apple Store o da Google Play. Per altre informazioni, vedere:
* [Aspettative dalla gestione dell'app per Android con criteri di protezione delle app](../fundamentals/end-user-mam-apps-android.md)
* [Aspettative dalla gestione dell'app per iOS/iPadOS con criteri di protezione delle app](../fundamentals/end-user-mam-apps-ios.md)

## <a name="change-existing-policies"></a>Modificare i criteri esistenti
È possibile modificare criteri esistenti e applicarli agli utenti di destinazione. Quando tuttavia si modificano criteri esistenti, gli utenti che hanno già effettuato l'accesso alle app non vedranno le modifiche per un intervallo di tempo di otto ore.

Per visualizzare immediatamente l'effetto delle modifiche, l'utente finale deve disconnettersi dall'app e quindi eseguire nuovamente l'accesso.

### <a name="to-change-the-list-of-apps-associated-with-the-policy"></a>Per modificare l'elenco delle app associate al criterio

1. Nel riquadro **Criteri di protezione delle app** selezionare i criteri che si vuole modificare.

2. Nel riquadro *Protezione app di Intune* selezionare **Proprietà**.

3. Accanto alla sezione intitolata *Applicazioni* selezionare **Modifica**.

4. La pagina **App** consente di scegliere come applicare questo criterio alle app su dispositivi diversi. È necessario aggiungere almeno un'app.<p>
    
    | Valore/opzione | Descrizione |
    |-------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
    | Specifica come destinatari le app in tutti i tipi di dispositivo | Usare questa opzione per destinare i criteri alle app nei dispositivi con qualsiasi stato di gestione. Scegliere **No** per destinare i criteri ad app su tipi di dispositivi specifici. Per questa impostazione può essere necessaria una configurazione aggiuntiva dell'app. Per altre informazioni, vedere [Target app protection policies based on device management state](#target-app-protection-policies-based-on-device-management-state) (Assegnare i criteri di protezione delle app in base allo stato di gestione del dispositivo). |
    |     Tipi di dispositivi | Usare questa opzione per specificare se i criteri di applicano ai dispositivi gestiti MDM o ai dispositivi non gestiti. Per i criteri di protezione delle app iOS/iPadOS selezionare **Non gestito** o **Gestito** per i dispositivi. Per i criteri di protezione delle app Android selezionare **Non gestito**, **Amministratore di dispositivi Android** e **Android Enterprise**.  |
    | App pubbliche | Fare clic su **Select public apps** (Selezionare le app pubbliche) per scegliere le app di destinazione. |
    | App personalizzate | Fare clic su **Select custom apps** (Selezionare le app personalizzate) per selezionare le app personalizzate di destinazione in base a un ID di bundle. |

    Le app selezionate verranno visualizzate nell'elenco delle app pubbliche e personalizzate.

5. Fare clic su **Rivedi e crea** per esaminare le app selezionate per i criteri.

6. Al termine, fare clic su **Salva** per aggiornare i criteri di protezione delle app.
 
#### <a name="to-change-the-list-of-user-groups"></a>Per modificare l'elenco dei gruppi di utenti

1. Nel riquadro **Criteri di protezione delle app** selezionare i criteri che si vuole modificare.

2. Nel riquadro *Protezione app di Intune* selezionare **Proprietà**.

3. Accanto alla sezione intitolata *Assegnazioni* selezionare **Modifica**.

4. Per aggiungere un nuovo gruppo di utenti ai criteri, nella scheda *Includi* scegliere **Selezionare i gruppi da includere** e selezionare il gruppo di utenti. Scegliere **Seleziona** per aggiungere il gruppo. 

5. Per escludere un gruppo di utenti, nella scheda *Escludi* scegliere **Selezionare i gruppi da escludere** e selezionare il gruppo di utenti. Scegliere **Seleziona** per rimuovere il gruppo di utenti.  

6. Per eliminare gruppi aggiunti in precedenza, nella scheda *Includi* o *Escludi* selezionare i puntini di sospensione (...) e selezionare **Elimina**.

7. Fare clic su **Rivedi e crea** per esaminare i gruppi utenti selezionati per i criteri.

8. Quando le modifiche delle assegnazioni sono pronte, selezionare **Salva** per salvare la configurazione e distribuire i criteri al nuovo set di utenti. Se si seleziona **Annulla** prima di salvare la configurazione, verranno eliminate tutte le modifiche apportate nelle schede *Includi* ed *Escludi*.

### <a name="to-change-policy-settings"></a>Per modificare le impostazioni dei criteri

1. Nel riquadro **Criteri di protezione delle app** selezionare i criteri che si vuole modificare.

2. Nel riquadro *Protezione app di Intune* selezionare **Proprietà**.

3. Accanto alla sezione contenente le impostazioni che si vuole modificare selezionare **Modifica**. quindi configurare i nuovi valori per le impostazioni.

7. Fare clic su **Rivedi e crea** per esaminare le impostazioni aggiornate per i criteri.

4. Selezionare **Salva** per salvare le modifiche. Ripetere il processo per selezionare un'area di impostazioni e apportare e quindi salvare le modifiche, fino al completamento di tutte le modifiche. È quindi possibile chiudere il riquadro *Protezione app di Intune - Proprietà*. 

## <a name="target-app-protection-policies-based-on-device-management-state"></a>Assegnare i criteri di protezione delle app in base allo stato di gestione del dispositivo
In molte organizzazioni è consuetudine consentire agli utenti finali di usare sia i dispositivi gestiti Intune Mobile Device Management (MDM), ad esempio i dispositivi di proprietà aziendale, sia i dispositivi non gestiti protetti solo con criteri di protezione delle app di Intune. I dispositivi non gestiti sono spesso noti come dispositivi Bring Your Own Device (BYOD).

Poiché i criteri di protezione delle app di Intune usano come destinazione l'identità di un utente, le impostazioni di protezione per un utente possono essere applicate sia ai dispositivi registrati (dispositivi MDM gestiti) che ai dispositivi non registrati (non MDM). È quindi possibile assegnare un criterio di protezione delle app di Intune sia a dispositivi Intune registrati che a dispositivi non registrati iOS/iPadOS e Android. È possibile avere criteri di protezione per dispositivi non gestiti, in cui vengono applicati severi controlli di prevenzione dalla perdita dei dati, e criteri di protezione dati separati per la gestione di dispositivi MDM gestiti, in cui i controlli DLP possono essere meno severi. Per altre informazioni sul funzionamento in dispositivi Android Enterprise personali, vedere [Criteri di protezione delle app e profili di lavoro](android-deployment-scenarios-app-protection-work-profiles.md).

Per creare questi criteri, passare ad **App** > **Criteri di protezione delle app** nella console di Intune e quindi selezionare **Crea criterio**. È anche possibile modificare un criterio di protezione delle app esistente. Per fare in modo che i criteri di protezione delle app vengano applicati sia ai dispositivi gestiti che non gestiti, passare alla pagina **App** e verificare che l'opzione **Specifica come destinatari le app in tutti i tipi di dispositivo** sia impostata su **Sì**, ovvero il valore predefinito. Per assegnare i criteri in modo granulare sulla base dello stato di gestione, impostare **Specifica come destinatari le app in tutti i tipi di dispositivo** su **No**. 

### <a name="device-types"></a>Tipi di dispositivi

- **Non gestito**: Per i dispositivi iOS/iPadOS, i dispositivi non gestiti sono tutti i dispositivi in cui la gestione MDM di Intune o una soluzione MDM/EMM di terze parti non passa la chiave `IntuneMAMUPN`. Per i dispositivi Android, i dispositivi non gestiti sono dispositivi in cui non è stata rilevata la gestione MDM di Intune. Sono inclusi i dispositivi gestiti da fornitori di software MDM di terze parti.
- **Dispositivi gestiti da Intune**: i dispositivi gestiti sono gestiti dalla gestione di dispositivi mobili di Intune.
- **Amministratore di dispositivi Android**: dispositivi gestiti da Intune che usano l'API di amministrazione dei dispositivi Android.
- **Android Enterprise**: dispositivi gestiti da Intune che usano i profili di lavoro Android Enterprise o la gestione dei dispositivi completa di Android Enterprise.

In Android i dispositivi Android richiederanno di installare l'app Portale aziendale Intune indipendentemente dal tipo di dispositivo scelto. Ad esempio, se si seleziona "Android Enterprise", la richiesta verrà visualizzata anche agli utenti con dispositivi Android non gestiti.

Per iOS/iPadOS, per applicare la selezione 'Tipo di dispositivo' ai dispositivi gestiti da Intune, sono necessarie altre impostazioni di configurazione dell'app. Queste configurazioni comunicheranno al servizio APP gestito che una determinata app è gestita e che non verranno applicate le impostazioni dell'APP:

- È necessario configurare **IntuneMAMUPN** per tutte le applicazioni gestite da MDM. Per altre informazioni, vedere [Come gestire il trasferimento di dati tra app iOS/iPadOS in Microsoft Intune](data-transfer-between-apps-manage-ios.md#configure-user-upn-setting-for-microsoft-intune-or-third-party-emm).
- È necessario configurare **IntuneMAMDeviceID** per tutte le applicazioni gestite di terze parti e line-of-business. È necessario impostare **IntuneMAMDeviceID** sul token dell'ID del dispositivo. Ad esempio, `key=IntuneMAMDeviceID, value={{deviceID}}` Per altre informazioni, vedere [Aggiungere criteri di configurazione delle app per i dispositivi iOS/iPadOS gestiti](app-configuration-policies-use-ios.md).
- Se si configura solo **IntuneMAMDeviceID**, l'app di Intune considererà il dispositivo come non gestito.

> [!NOTE]
> Per informazioni sul supporto iOS/iPadOS in merito ai criteri di protezione delle app sulla base dello stato di gestione del dispositivo, vedere [Criteri di protezione MAM assegnati sulla base dello stato di gestione](../fundamentals/whats-new-archive.md#mam-protection-policies-targeted-based-on-management-state).

## <a name="policy-settings"></a>Impostazioni dei criteri
Per visualizzare l'elenco completo delle impostazioni dei criteri per iOS/iPadOS e Android, selezionare uno dei collegamenti seguenti:

- [Criteri iOS/iPadOS](app-protection-policy-settings-ios.md)
- [Criteri Android](app-protection-policy-settings-android.md)

## <a name="next-steps"></a>Passaggi successivi
[Monitorare la conformità e lo stato utente](app-protection-policies-monitor.md)

## <a name="see-also"></a>Vedere anche
* [Aspettative dalla gestione dell'app per Android con criteri di protezione delle app](../fundamentals/end-user-mam-apps-android.md)
* [Aspettative dalla gestione dell'app per iOS/iPadOS con criteri di protezione delle app](../fundamentals/end-user-mam-apps-ios.md)
