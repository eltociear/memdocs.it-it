---
title: Come risolvere i problemi di distribuzione dei criteri di protezione delle app in Intune
description: Illustra come risolvere i problemi che possono verificarsi quando si distribuiscono i criteri di protezione delle app in Intune.
author: simonxjx
manager: dcscontentpm
localization_priority: Normal
search.appverid:
- MET150
audience: ITPro
ms.date: 4/17/2020
ms.service: microsoft-intune
ms.topic: troubleshooting
ms.author: v-six
ms.custom: CSSTroubleshoot
appliesto:
- Intune
ms.openlocfilehash: 8443ca01a0ca1647e8069fdccf1d71aef74c23d8
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989461"
---
# <a name="troubleshooting-app-protection-policy-deployment-in-intune"></a>Risoluzione dei problemi di distribuzione dei criteri di protezione delle app in Intune

## <a name="introduction"></a>Introduzione

Questo articolo aiuta a comprendere e risolvere i problemi che si verificano quando si distribuiscono i criteri di protezione delle app in Microsoft Intune. Seguire le sezioni adatte alla situazione.

## <a name="basic-steps"></a>Passaggi principali

### <a name="collect-initial-data"></a>Raccogliere dati iniziali

Prima di iniziare la risoluzione dei problemi, raccogliere alcune informazioni di base per comprendere meglio il problema e ridurre il tempo necessario per la ricerca di una soluzione.

Raccogliere le seguenti informazioni:

- Quale impostazione dei criteri non viene applicata? Alcuni criteri vengono applicati?
- Qual è l'esperienza utente? Gli utenti hanno installato e avviato l'app interessata?
- Quando è iniziato il problema? Hai mai funzionato la protezione delle app?
- Quale piattaforma (Android o iOS) presenta il problema?
- Quanti utenti sono interessati? Sono interessati tutti i dispositivi o solo alcuni?
- Quanti dispositivi sono interessati? Sono interessati tutti i dispositivi o solo alcuni?
- Sebbene i criteri di protezione delle app di Intune non richiedano un servizio di gestione di dispositivi mobili (MDM), gli utenti interessati usano Intune o EMM di terze parti?
- Sono interessate tutte le app gestite o solo app specifiche? Ad esempio, sono interessate le app line-of-business con [Intune App SDK](../developer/app-sdk-get-started.md) e non le app dello Store?

A questo punto, è possibile avviare la risoluzione dei problemi in base alle risposte date a queste domande.

### <a name="verify-prerequisites"></a>Verificare i prerequisiti

Il passaggio successivo per la risoluzione dei problemi consiste nel controllare se tutti i prerequisiti sono soddisfatti.

Sebbene sia possibile usare i criteri di protezione delle app di Intune indipendentemente da qualsiasi soluzione MDM, è necessario soddisfare i prerequisiti seguenti:

- All'utente deve essere assegnata una licenza di Intune.
- L'utente deve appartenere a un gruppo di sicurezza interessato dai criteri di protezione delle app. Gli stessi criteri di protezione delle app devono avere come destinazione l'app specifica in uso.
- Per i dispositivi Android, è necessaria l'app Portale aziendale per ricevere i criteri di protezione delle app.
- Se si usano le app [Word, Excel o PowerPoint](https://products.office.com/business/office), è necessario soddisfare i requisiti aggiuntivi seguenti:
    - L'utente deve avere una licenza per [App di Microsoft 365 Business o Enterprise](https://products.office.com/business/compare-more-office-365-for-business-plans) collegata all'account Azure Active Directory (Azure AD). La sottoscrizione deve includere le app di Office nei dispositivi mobili e può includere un account di archiviazione cloud con [OneDrive for Business](https://onedrive.live.com/about/business/). È possibile assegnare licenze di Office 365 nell'[interfaccia di amministrazione di Microsoft 365](https://admin.microsoft.com) seguendo [queste istruzioni](https://support.office.com/article/Assign-or-remove-licenses-for-Office-365-for-business-997596b5-4173-4627-b915-36abac6786dc).
    - L'utente deve avere un percorso gestito configurato usando la funzionalità granulare **Salva con nome**. Questo comando si trova nell'impostazione dei criteri di protezione delle applicazioni **Salva copie dei dati dell'organizzazione**. Se ad esempio il percorso gestito è OneDrive, l'app [OneDrive](https://onedrive.live.com/about/) deve essere configurata nell'app Word, Excel o PowerPoint dell'utente.
    - Se il percorso gestito è OneDrive, l'app deve essere impostata come destinazione dei criteri di protezione delle app distribuiti all'utente.

  > [!NOTE]
  > Le app per dispositivi mobili di Office attualmente supportano solo SharePoint Online e SharePoint locale.

- Se si usano i criteri di protezione delle app di Intune insieme a risorse locali (Microsoft Skype for Business e Microsoft Exchange Server), è necessario abilitare l'[autenticazione moderna ibrida per Skype for Business ed Exchange](https://docs.microsoft.com/office365/enterprise/hybrid-modern-auth-overview).

I criteri di protezione delle app di Intune richiedono coerenza dell'identità dell'utente tra l'app e [Intune App SDK](../developer/app-sdk-get-started.md). L'unico modo per assicurare coerenza è tramite l'autenticazione moderna. Esistono scenari in cui le app possono funzionare in una configurazione locale senza autenticazione moderna. Tuttavia, i risultati non sono coerenti o garantiti.

Per altre informazioni su come abilitare l'autenticazione moderna ibrida per le configurazioni ibride e locali di Skype for Business, vedere gli articoli seguenti:

- **Configurazione ibrida**<br>
[Disponibilità generale per l'autenticazione moderna ibrida per Skype for Business ed Exchange](https://techcommunity.microsoft.com/t5/Skype-for-Business-Blog/Hybrid-Modern-Auth-for-SfB-and-Exchange-goes-GA/ba-p/134756)

- **Configurazione locale**<br>
[Autenticazione moderna ibrida per Skype for Business con AAD](https://techcommunity.microsoft.com/t5/Skype-for-Business-Blog/Modern-Auth-for-SfB-OnPrem-with-AAD/ba-p/180910)

### <a name="check-app-protection-policy-status"></a>Controllare lo stato dei criteri di protezione delle app

Per controllare lo stato di protezione delle app, seguire questa procedura:

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selezionare **App** > **Monitor** > **Stato protezione app**e quindi selezionare il riquadro **Utenti assegnati**.
3. Nella pagina **Segnalazione app** selezionare **Selezionare l'utente** per visualizzare un elenco di utenti e gruppi.
4. Cercare e selezionare uno degli utenti interessati dall'elenco, quindi scegliere **Selezionare l'utente**. Nella parte superiore del riquadro Segnalazione app è possibile verificare se l'utente ha la licenza per la protezione delle app e dispone di una licenza per Office 365. È anche possibile visualizzare lo stato delle app per tutti i dispositivi dell'utente.
5. Prendere nota delle informazioni importanti, ad esempio app di destinazione, tipi di dispositivi, criteri, stato di archiviazione del dispositivo e ora dell'ultima sincronizzazione.

> [!NOTE]
> I criteri di protezione delle app si applicano solo quando le app vengono usate in un contesto di lavoro, ad esempio quando l'utente accede alle app usando un account aziendale.

Per altre informazioni, vedere [Come convalidare la configurazione dei criteri di protezione delle app in Microsoft Intune](../apps/app-protection-policies-validate.md).

### <a name="verify-that-user-identity-is-consistent-between-app-and-intune-app-sdk"></a>Verificare la coerenza dell'identità dell'utente tra app e Intune App SDK

Nella maggior parte degli scenari gli utenti accedono ai propri account usando il nome dell'entità utente (UPN, User Principal Name). Tuttavia, in alcuni ambienti, ad esempio in scenari locali, gli utenti potrebbero usare un altro tipo di credenziali di accesso. In questi casi si potrebbe notare che l'UPN usato nell'app non corrisponde all'oggetto UPN in Azure AD. Quando si verifica questo problema, i criteri di protezione delle app non vengono applicati come previsto.

Le procedure consigliate di Microsoft prevedono la corrispondenza tra il nome di accesso UPN e l'indirizzo SMTP primario. In questo modo gli utenti possono accedere alle app gestite, alla protezione delle app di Intune e ad altre risorse di Azure AD grazie a un'identità coerente. Per altre informazioni, vedere [Popolamento di UserPrincipalNamein in Azure AD](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-userprincipalname).

Se l'ambiente richiede metodi di accesso alternativi, vedere [Configurazione di un ID di accesso alternativo](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configuring-alternate-login-id), in particolare [Autenticazione moderna ibrida con ID alternativo](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configuring-alternate-login-id#hybrid-modern-authentication-with-alternate-id).

### <a name="verify-that-the-user-is-targeted"></a>Verificare la destinazione dell'utente

I criteri di protezione delle app di Intune devono essere destinati agli utenti. Se i criteri di protezione delle app non vengono assegnati a un utente o a un gruppo di utenti, i criteri non vengono applicati.

Per verificare che i criteri vengano applicati all'utente di destinazione, attenersi alla procedura seguente:

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selezionare **App** > **Monitor** > **Stato di protezione dell'app**, quindi selezionare il riquadro **Stato utente** (in base alla piattaforma del sistema operativo del dispositivo).
Nel riquadro **Segnalazione app** che si apre scegliere **Selezionare l'utente** per cercare un utente.
3. Selezionare un utente nell'elenco. È possibile visualizzare i dettagli dell'utente.

Quando si assegnano i criteri a un gruppo di utenti, verificare che l'utente sia presente nel gruppo di utenti. A tale scopo, attenersi alla seguente procedura:

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selezionare **Gruppi > Tutti i gruppi**, quindi cercare e selezionare il gruppo usato per l'assegnazione dei criteri di protezione delle app.
3. Selezionare **Membri** nella sezione **Gestisci**.
4. Se l'utente interessato non è presente nell'elenco, vedere [Gestire l'accesso ad app e risorse usando gruppi di Azure Active Directory](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-manage-groups) e le regole di appartenenza ai gruppi. Verificare che l'utente interessato sia incluso nel gruppo.
5. Assicurarsi che l'utente interessato non sia incluso in uno dei gruppi esclusi per i criteri.

> [!IMPORTANT]
> - I criteri di protezione delle app di Intune devono essere assegnati a gruppi di utenti e non a gruppi di dispositivi.
> - Se il dispositivo interessato usa Apple Device Enrollment Program (DEP), verificare che l'**affinità utente** sia abilitata. L'affinità utente è obbligatoria per qualsiasi app che richiede l'autenticazione utente nell'ambito del programma DEP.
> - Se il dispositivo interessato usa Android Enterprise, solo i profili di lavoro supporteranno i criteri di protezione delle app.


### <a name="verify-that-the-managed-app-is-targeted"></a>Verificare la destinazione dell'app gestita

Quando si configurano i criteri di protezione delle app di Intune, le app di destinazione devono usare [Intune App SDK](../developer/app-sdk-get-started.md). In caso contrario, i criteri di protezione delle app potrebbero non funzionare correttamente.

Assicurarsi che l'app di destinazione sia elencata in [App protette di Microsoft Intune](../apps/apps-supported-intune-apps.md). Per le app line-of-business o le app personalizzate, verificare che usino la versione più recente di [Intune App SDK](../developer/app-sdk-get-started.md). Tenere presente quanto segue:

Per iOS, questa procedura è importante perché ogni versione contiene correzioni che influiscono sul modo in cui i criteri vengono applicati e sul relativo funzionamento. Per altre informazioni, vedere [Versioni iOS di Intune App SDK](https://github.com/msintuneappsdk/ms-intune-app-sdk-ios/releases).
Per Android, questa procedura non è altrettanto importante. Gli utenti devono avere tuttavia la versione più recente dell'app Portale aziendale installata perché tale app funziona come agente per la gestione dei criteri.

> [!NOTE]
> A partire da settembre 2019, Intune supporterà le app iOS con Intune App SDK 8.1.1 e versioni successive. Le app compilate con versioni di SDK precedenti a 8.1.1 non saranno più supportate. 

## <a name="more-information"></a>Altre informazioni

### <a name="special-requirements-for-intune-mdm-managed-devices"></a>Requisiti speciali per i dispositivi gestiti da MDM di Intune

Quando si creano criteri di protezione delle app, è possibile destinarli a tutti i tipi di app o ai tipi di app seguenti:

- App in dispositivi non gestiti
- App in dispositivi gestiti da Intune
- App nel profilo di lavoro di Android

> [!NOTE] 
> Per specificare i tipi di app, impostare **Includi tutti i tipi di app** su **No**, quindi selezionare dall'elenco **Tipi di app**.

Per iOS, sono necessarie le [impostazioni di configurazione delle app](../apps/app-configuration-policies-use-ios.md) aggiuntive per assegnare le impostazioni dei criteri di protezione delle app alle app nei dispositivi registrati in Intune:

- È necessario configurare **IntuneMAMUPN** per tutte le applicazioni gestite da MDM (Intune o EMM di terze parti). Per altre informazioni, vedere Configurare l'impostazione UPN dell'utente per Microsoft Intune o soluzioni EMM di terze parti.
- È necessario configurare **IntuneMAMDeviceID** per tutte le applicazioni gestite da MDM line-of-business e di terze parti.
- È necessario configurare **IntuneMAMDeviceID** come token dell'ID del dispositivo. Ad esempio key=IntuneMAMDeviceID, value={{deviceID}}. Per altre informazioni, vedere [Aggiungere criteri di configurazione delle app per i dispositivi iOS gestiti](../apps/app-configuration-policies-use-ios.md).
- Se si configura solo il valore **IntuneMAMDeviceID**, l'app di Intune considererà il dispositivo come non gestito.

### <a name="scenario-policy-changes-are-not-working"></a>Scenario: le modifiche ai criteri non funzionano
[Intune App SDK](../developer/app-sdk-get-started.md) controlla regolarmente le modifiche ai criteri. Tuttavia, questo processo può essere ritardato per uno dei motivi seguenti:

- L'app non è sincronizzata con il servizio.
- L'app Portale aziendale è stata rimossa dal dispositivo.

I criteri di protezione delle app di Intune si basano sull'identità utente. Pertanto, è necessario un accesso valido che usa un account aziendale o dell'istituto di istruzione per l'app e una connessione coerente al servizio. Se l'utente non ha eseguito l'accesso all'app o l'app Portale aziendale è stata rimossa dal dispositivo, gli aggiornamenti dei criteri non verranno applicati.

Inoltre per l'applicazione di modifiche o aggiornamenti dei criteri di protezione delle app possono essere richieste fino a 8 ore. Se applicabile, la chiusura di tutte le app e il riavvio del dispositivo solitamente forzano l'applicazione dei criteri, che avviene in modo più veloce.

Per controllare lo stato di protezione dell'app, seguire questa procedura:

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selezionare **App** > **Monitor** > **Stato protezione app**e quindi selezionare il riquadro **Utenti assegnati**.
3. Nella pagina Segnalazione app scegliere **Selezionare l'utente** per aprire un elenco di utenti e gruppi.
4. Cercare e selezionare uno degli utenti interessati dall'elenco, quindi scegliere **Selezionare l'utente**.
5. Esaminare i criteri attualmente applicati, inclusi lo stato e l'ora dell'ultima sincronizzazione.
6. Se lo stato è **Sincronizzazione non eseguita** o se viene visualizzato che non è stata rilevata una sincronizzazione recente, controllare se l'utente dispone di una connessione di rete coerente. Per gli utenti Android, assicurarsi che sia installata la versione più recente dell'app Portale aziendale.

> [!IMPORTANT]
> [Intune App SDK](../developer/app-sdk-get-started.md) controlla la cancellazione selettiva ogni 30 minuti. Tuttavia, le modifiche ai criteri esistenti per gli utenti che hanno già eseguito l'accesso potrebbero non essere visualizzate prima di 8 ore. Per velocizzare questo processo, chiedere all'utente di disconnettersi dall'app, quindi di eseguire di nuovo l'accesso oppure riavviare i dispositivi.

I criteri di protezione delle app di Intune includono il supporto per più identità. Intune può applicare i criteri di protezione delle app solo all'account aziendale o dell'istituto di istruzione che ha eseguito l'accesso all'app. È tuttavia supportato un solo account aziendale o dell'istituto di istruzione per ogni dispositivo.

### <a name="scenario-the-policy-is-applied-but-ios-users-can-still-transfer-work-files-to-unmanaged-apps"></a>Scenario: i criteri sono applicati ma gli utenti iOS possono comunque trasferire i file di lavoro in app non gestite
La funzionalità **Open-in management** (Gestione Open-In) (![pulsante Open-in](media/troubleshoot-app-protection/troubleshoot-app-protection.jpg)) per i dispositivi iOS consente di limitare i trasferimenti di file tra le app distribuite tramite il canale MDM. L'utente può trasferire i file di lavoro da percorsi gestiti, ad esempio OneDrive ed Exchange, ad app o percorsi non gestiti, a seconda della configurazione. La funzionalità **Open-in management** (Gestione Open-In) di iOS funziona indipendentemente da altri metodi di trasferimento dei dati. Di conseguenza, non è influenzata dalle impostazioni **Salva con nome** e **Copia/Incolla**.

È possibile usare i criteri di protezione delle app di Intune insieme alla funzionalità **Open-in management** (Gestione Open-In) di iOS per proteggere i dati aziendali nei modi seguenti:

- **Dispositivi di proprietà dei dipendenti non gestiti da una soluzione MDM:** è possibile impostare i criteri di protezione delle app su **Consenti all'app di trasferire i dati ad altre app: App gestite da criteri**. Configurato in questo modo, il comportamento della funzionalità **Open-in** in un'app gestita da criteri propone come opzioni per la condivisione solo altre app gestite da criteri. Se ad esempio un utente tenta di inviare un file protetto come allegato da OneDrive all'app di posta nativa, il file risulterà illeggibile.

- **Dispositivi gestiti da soluzioni MDM**: per i dispositivi registrati in Intune o soluzioni MDM di terze parti, la condivisione dei dati tra app con criteri di protezione delle app e altre app iOS gestite distribuite tramite MDM è controllata dai criteri di protezione dell'app di Intune e dalla funzionalità **Open-in management** (Gestione Open-In) di iOS.<br/><br/>
Per assicurarsi che le app distribuite tramite una soluzione MDM siano anche associate ai criteri di protezione delle app di Intune, configurare l'impostazione UPN dell'utente come descritto in [Configurare l'impostazione UPN dell'utente](../apps/data-transfer-between-apps-manage-ios.md#configure-user-upn-setting-for-microsoft-intune-or-third-party-emm).<br/><br/>Per specificare come consentire il trasferimento di dati ad altre app, abilitare **Invia i dati dell'organizzazione ad altre app**, quindi selezionare il livello di condivisione preferito.<br/><br/>Per specificare come consentire a un'app di ricevere dati da altre app, abilitare **Ricevi dati da altre app**, quindi selezionare il livello di ricezione dei dati preferito.

Per altre informazioni su come ricevere e condividere i dati delle app, vedere [Impostazioni di rilocazione dei dati](../apps/app-protection-policy-settings-ios.md#data-protection).

Per altre informazioni, vedere [Come gestire il trasferimento di dati tra app iOS in Microsoft Intune](../apps/data-transfer-between-apps-manage-ios.md).

## <a name="references"></a>Riferimenti

Per trovare una soluzione a un problema correlato o per altre informazioni su Intune, pubblicare una domanda nel [forum di Microsoft Intune](https://social.technet.microsoft.com/Forums/en-US/home?category=microsoftintune&filter=alltypes&sort=lastpostdesc). I forum sono visitati da molti tecnici del supporto, MVP e membri del team di sviluppo Microsoft. Qui è possibile trovare l'utente che può dare le informazioni necessarie.

Per aprire una richiesta di supporto per il team del supporto tecnico di Microsoft Intune, vedere [Come ottenere supporto per Microsoft Intune](../fundamentals/get-support.md).

Per altre informazioni sui criteri di protezione delle app di Intune, vedere gli articoli seguenti:

- [Risolvere i problemi relativi alla gestione di applicazioni mobili](../apps/troubleshoot-mam.md)
- [Domande frequenti sulla gestione di applicazioni mobili e sulla protezione delle app](../apps/mam-faq.md)
- [Suggerimento per il supporto: Risoluzione dei problemi relativi ai criteri di protezione delle app di Intune tramite file di log nei dispositivi locali](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Troubleshooting-Intune-app-protection-policy-using/ba-p/330372)

Per tutte le ultime notizie, informazioni e suggerimenti tecnici, passare ai blog ufficiali:

- [Blog del team di supporto di Microsoft Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/bg-p/IntuneCustomerSuccess)
- [Blog di Microsoft Enterprise Mobility + Security](https://cloudblogs.microsoft.com/enterprisemobility)

## <a name="next-steps"></a>Passaggi successivi

- Per altre informazioni sulla risoluzione dei problemi di Intune, vedere [Usare il portale per la risoluzione dei problemi per offrire assistenza agli utenti aziendali](../fundamentals/help-desk-operators.md). 
- È possibile ottenere informazioni sui problemi noti in Microsoft Intune. Per altre informazioni, vedere il blog [Intune Customer Success](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/bg-p/IntuneCustomerSuccess).
- È possibile ottenere altre informazioni. Vedere [Come ottenere supporto per Microsoft Intune](../fundamentals/get-support.md).
