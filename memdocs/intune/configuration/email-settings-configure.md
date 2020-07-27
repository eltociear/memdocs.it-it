---
title: Configurare le impostazioni di posta elettronica in Microsoft Intune - Azure | Microsoft Docs
titleSuffix: ''
description: Creare un profilo di posta elettronica in Microsoft Intune e distribuire questo profilo ai dispositivi amministratore di dispositivi Android e Android Enterprise, iOS, iPadOS e Windows. Usare i profili di posta elettronica per configurare le impostazioni di posta elettronica comuni, tra cui un server e i metodi di autenticazione per la connessione alla posta elettronica aziendale nei dispositivi gestiti.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 07/20/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5bb01770909192b17f0e72b852e4094ff7ad3a04
ms.sourcegitcommit: d3992eda0b89bf239cea4ec699ed4711c1fb9e15
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/21/2020
ms.locfileid: "86565649"
---
# <a name="add-email-settings-to-devices-using-intune"></a>Aggiungere impostazioni di posta elettronica ai dispositivi con Intune

Microsoft Intune include impostazioni di posta elettronica diverse che è possibile distribuire nei dispositivi dell'organizzazione. Un amministratore IT crea profili di posta elettronica con impostazioni specifiche per la connessione a un server di posta, ad esempio Office 365 e Gmail. Gli utenti finali quindi si connettono, eseguono l'autenticazione e sincronizzano gli account di posta elettronica dell'organizzazione nei dispositivi mobili. Creando e distribuendo un profilo di posta elettronica, è possibile assicurarsi che le impostazioni siano standard in più dispositivi e ridurre così le chiamate al supporto da parte degli utenti finali che non conoscono le impostazioni di posta elettronica corrette.

È possibile usare i profili di posta elettronica per configurare le impostazioni di posta elettronica predefinite per i dispositivi seguenti:

- Amministratore di dispositivi Android in Samsung Knox Standard 5.0 e versioni successive
- Android Enterprise
- iOS 11.0 e versioni successive
- iPadOS 13.0 e versioni successive
- Windows Phone 8.1 e versioni successive
- Windows 10 (Desktop) e Windows 10 Mobile

Questo articolo illustra come creare un profilo di posta elettronica in Microsoft Intune e include i collegamenti alle diverse piattaforme per impostazioni più specifiche.

## <a name="create-the-profile"></a>Creare il profilo

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selezionare **Dispositivi** > **Profili di configurazione** > **Crea profilo**.
3. Immettere le proprietà seguenti:

    - **Piattaforma**: scegliere la piattaforma dei dispositivi. Le opzioni disponibili sono:  

        - **Amministratore di dispositivi Android** (solo Samsung Android Knox Standard)
        - **Android Enterprise**
        - **iOS/iPadOS**
        - **Windows 10 e versioni successive**
        - **Windows Phone 8.1**

    - **Profilo**: Selezionare **Posta elettronica**.

4. Selezionare **Crea**.
5. In **Informazioni di base** immettere le proprietà seguenti:

    - **Nome**: immettere un nome descrittivo per il criterio. Assegnare ai criteri nomi che possano essere identificati facilmente in un secondo momento. Ad esempio, un nome di criterio valido è **Windows 10: Impostazioni di posta elettronica per tutti i dispositivi Windows 10**.
    - **Descrizione**: immettere una descrizione del criterio. Questa impostazione è facoltativa ma consigliata.

6. Selezionare **Avanti**.

7. In **Impostazioni di configurazione** le impostazioni configurabili variano in base alla piattaforma scelta. Scegliere la piattaforma per le impostazioni dettagliate:

    - [Amministratore di dispositivi Android (solo Samsung Android Knox Standard)](email-settings-android.md)
    - [Android Enterprise](email-settings-android-enterprise.md)
    - [iOS/iPadOS](email-settings-ios.md)
    - [Windows 10](email-settings-windows-10.md)
    - [Windows Phone 8.1](email-settings-windows-phone-8-1.md)

8. Selezionare **Avanti**.
9. In **Tag ambito** (facoltativo) assegnare un tag per filtrare il profilo a gruppi IT specifici, ad esempio `US-NC IT Team` o `JohnGlenn_ITDepartment`. Per altre informazioni sui tag di ambito, vedere [Usare il controllo degli accessi in base al ruolo (RBAC) e i tag di ambito per l'infrastruttura IT distribuita](../fundamentals/scope-tags.md).

    Selezionare **Avanti**.

10. In **Assegnazioni** selezionare i gruppi di utenti o di dispositivi che riceveranno il profilo. Per altre informazioni sull'assegnazione di profili, vedere [Cosa è necessario sapere](#what-you-need-to-know) (in questo articolo). Anche in [Assegnare profili utente e profili di dispositivo](device-profile-assign.md) sono disponibili alcune linee guida.

    Selezionare **Avanti**.

11. In **Rivedi e crea** rivedere le impostazioni. Quando si seleziona **Crea**, le modifiche vengono salvate e il profilo viene assegnato. Il criterio viene visualizzato anche nell'elenco dei profili.

## <a name="what-you-need-to-know"></a>Informazioni importanti

- I profili di posta elettronica vengono distribuiti per l'utente che ha registrato il dispositivo. Per configurare il profilo di posta elettronica, Intune usa le proprietà di Azure Active Directory (AD) nel profilo di posta elettronica dell'utente durante la registrazione.

- Microsoft Outlook per i dispositivi iOS/iPadOS e Android non supportano i profili di posta elettronica. Distribuire invece i criteri di configurazione delle app. Per altre informazioni, vedere [Impostazioni di configurazione di Outlook](../apps/app-configuration-policies-outlook.md).

  Nei dispositivi Android Enterprise, distribuire Gmail o Nine for Work usando Google Play Store gestito. In [Aggiungere app Google Play gestite](../apps/apps-add-android-for-work.md) sono illustrati i passaggi.

- La posta elettronica si basa sulle impostazioni di identità e utente. I profili di posta elettronica vengono in genere assegnati a gruppi di utenti, non a gruppi di dispositivi. Alcune considerazioni:

  - Se il profilo di posta elettronica include certificati utente, assegnare il profilo di posta elettronica a gruppi di utenti. È possibile che siano presenti più profili certificato utente assegnati. Questi profili creano una catena di distribuzioni di profili. Distribuire questa catena di profili a gruppi di utenti.

    Se un profilo della catena viene distribuito in un gruppo di dispositivi, è possibile che venga richiesto continuamente agli utenti di immettere la password.

  - I gruppi di dispositivi vengono in genere usati quando non è presente un utente primario o se non si conosce l'utente. I profili di posta elettronica destinati ai gruppi di dispositivi (non ai gruppi di utenti) non possono essere ricevuti dal dispositivo.

    Ad esempio, se il profilo di posta elettronica è destinato a un gruppo che include tutti i dispositivi iOS/iPadOS, assicurarsi che tutti i dispositivi abbiano un utente. Se un dispositivo non ha un utente, il profilo di posta elettronica potrebbe non essere distribuito. Il profilo risulta quindi limitato e potrebbe non essere distribuito in alcuni dispositivi. Se il dispositivo ha un utente primario, la distribuzione nei gruppi di dispositivi dovrebbe funzionare.

    Per altre informazioni sui possibili problemi relativi all'uso di gruppi di dispositivi, vedere [Problemi comuni relativi ai profili di posta elettronica](troubleshoot-email-profiles-in-microsoft-intune.md).

## <a name="remove-an-email-profile"></a>Rimuovere un profilo di posta elettronica

Esistono diversi modi di rimuovere un profilo di posta elettronica da un dispositivo, anche quando è disponibile un solo profilo di posta elettronica nel dispositivo:

- **Opzione 1**: Aprire il profilo di posta elettronica (**Dispositivi** > **Profili di configurazione** > selezionare il profilo) e scegliere **Assegnazioni**. Nella scheda **Includi** sono visualizzati i gruppi assegnati al profilo. Fare clic con il pulsante destro del mouse sul gruppo > **Rimuovi**. Assicurarsi di **salvare** le modifiche.

- **Opzione 2**: [cancellare o ritirare il dispositivo](../remote-actions/devices-wipe.md). È possibile usare queste azioni per rimuovere completamente o in modo selettivo dati e impostazioni.

## <a name="secure-email-access"></a>Proteggere l'accesso alla posta elettronica

È possibile proteggere i profili di posta elettronica usando le opzioni seguenti:

- **Certificati**: quando si crea il profilo di posta elettronica, si sceglie un profilo di certificato creato in precedenza in Intune. Questo certificato è noto come certificato di identità. Esegue l'autenticazione in base a un profilo certificato attendibile o a un certificato radice per verificare che il dispositivo di un utente sia autorizzato a connettersi. Il certificato attendibile viene assegnato al computer che autentica la connessione alla posta elettronica. Questo computer è in genere il server di posta nativo.

  Se si usa l'autenticazione basata su certificati per il profilo di posta elettronica, è necessario distribuire il profilo di posta elettronica, il profilo certificato e il profilo radice attendibile agli stessi gruppi. Questa distribuzione assicura che ogni dispositivo possa riconoscere la legittimità dell'autorità di certificazione.

  Per altre informazioni su come creare e usare i profili di certificato in Intune, vedere [Come configurare i certificati con Intune](../protect/certificates-configure.md).

- **Nome utente e password**: l'utente esegue l'autenticazione al server di posta nativo immettendo nome utente e password. La password non esiste nel profilo di posta elettronica, quindi l'utente finale immette la password quando si connette alla posta elettronica.

## <a name="how-intune-handles-existing-email-accounts"></a>In che modo Intune gestisce gli account di posta elettronica esistenti

Se l'utente ha già configurato un account di posta elettronica, il profilo di posta elettronica viene assegnato in modo diverso, a seconda della piattaforma.

- **iOS/iPadOS**: Un profilo di posta elettronica duplicato esistente viene individuato in base al nome host e all'indirizzo di posta elettronica. Il profilo di posta elettronica duplicato blocca l'assegnazione di un profilo di Intune. In questo caso l'app Portale aziendale notifica all'utente finale che esiste un problema di conformità e richiede quindi di rimuovere il profilo. Per evitare questo scenario, indicare agli utenti finali di eseguire la registrazione *prima* di installare un profilo di posta elettronica e di consentire a Intune di impostarlo.

- **Windows:** Un profilo di posta elettronica duplicato esistente viene individuato in base al nome host e all'indirizzo di posta elettronica. Intune sovrascrive il profilo di posta elettronica esistente creato dall'utente finale.

- **Android Samsung Knox Standard**: Un profilo di posta elettronica duplicato esistente viene individuato in base all'indirizzo di posta elettronica e viene sovrascritto con il profilo di Intune. Android non usa il nome host per identificare il profilo. Non creare più profili di posta elettronica usando lo stesso indirizzo di posta elettronica in host diversi. I profili si sovrascrivono a vicenda.

- **Profili di lavoro Android**: Intune offre due profili di posta elettronica di lavoro Android, uno per l'app Gmail e uno per l'app Nine Work. Queste app sono disponibili in Google Play Store e vengono installate nel profilo di lavoro del dispositivo. Queste app non creano profili duplicati. Entrambe le app supportano le connessioni a Exchange. Per usare la connettività di posta elettronica, distribuire una di queste app di posta elettronica nei dispositivi degli utenti, quindi creare e distribuire il profilo di posta elettronica. È possibile usare i profili di configurazione di posta elettronica Gmail e Nine che funzionano per i tipi di registrazione Profilo di lavoro e Profilo di lavoro completamente gestito, dedicato e di proprietà aziendale, incluso l'uso di profili certificato per entrambi i tipi di configurazione di posta elettronica. Tutti i criteri Gmail o Nine creati nella configurazione del dispositivo per i profili di lavoro continueranno a essere applicato al dispositivo. Non è necessario spostarli nei criteri di configurazione delle app. Le app di posta elettronica, ad esempio Nine Work, potrebbero non essere gratuite. Rivedere i dettagli relativi alla licenza dell'app o contattare l'azienda produttrice per richiedere informazioni.

## <a name="changes-to-assigned-email-profiles"></a>Modifiche ai profili di posta elettronica assegnati

Se si apportano modifiche a un profilo di posta elettronica assegnato in precedenza, è possibile che un messaggio richieda agli utenti finali di approvare la riconfigurazione delle impostazioni di posta elettronica.

## <a name="next-steps"></a>Passaggi successivi

Dopo che il profilo è stato creato, non è ancora operativo. [Assegnare il profilo](device-profile-assign.md) e [monitorarne lo stato](device-profile-monitor.md).
