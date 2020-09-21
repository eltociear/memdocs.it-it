---
title: Informazioni sulla gestione delle app in Microsoft Intune
titleSuffix: ''
description: Informazioni sulle funzionalità di gestione delle app client per piattaforma in Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/03/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 1975a2dc-3a14-4cb9-9afb-e2ba01a1c51b
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 68336d252cb3d3d3d49cc0c7a32e49e94ba5cdd7
ms.sourcegitcommit: d6cbd1a1c2926064e074e3431471534eb142c905
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/11/2020
ms.locfileid: "90012664"
---
# <a name="what-is-microsoft-intune-app-management"></a>Informazioni sulla gestione delle app in Microsoft Intune

Gli amministratori IT possono usare Microsoft Intune per gestire le app client usate dai dipendenti dell'azienda. Questa funzionalità si aggiunge alla gestione dei dispositivi e alla protezione dei dati. Una delle priorità di un amministratore è fare in modo che gli utenti finali abbiano accesso alle app necessarie per lavorare. Non sempre questo obiettivo risulta semplice da raggiungere, perché:
- Esiste una vasta gamma di piattaforme per dispositivi e tipi di applicazione.
- Potrebbe essere necessario gestire le app sia nei dispositivi aziendali che nei dispositivi personali degli utenti.
- Occorre assicurarsi che rete e dati rimangano protetti.

In aggiunta, potrebbe essere necessario assegnare e gestire le app su dispositivi non registrati in Intune.

## <a name="mobile-application-management-mam-basics"></a>Informazioni di base sulle app per la gestione di applicazioni mobili (MAM)

[Gestione di applicazioni mobili (MAM) di Intune](app-lifecycle.md) indica la suite di funzionalità di gestione di Intune che consente di pubblicare, distribuire, configurare, proteggere, monitorare e aggiornare le app mobili degli utenti.

MAM consente di gestire e proteggere i dati dell'organizzazione all'interno di un'applicazione. Con **MAM senza registrazione** (MAM-WE) un'app correlata all'istituto di istruzione o all'azienda contenente dati sensibili può essere gestita in quasi tutti i [dispositivi](app-management.md#app-management-capabilities-by-platform), inclusi i dispositivi personali in scenari **Bring-Your-Own-Device** (BYOD). La maggior parte delle app di produttività, ad esempio le app per Microsoft Office, può essere gestita da MAM di Intune. Vedere l'elenco ufficiale delle [app protette da Microsoft Intune](apps-supported-intune-apps.md) disponibili al pubblico.

MAM di Intune supporta due configurazioni:

- **MDM + MAM di Intune**: Gli amministratori IT possono gestire le app solo usando MAM e i criteri di protezione delle app nei dispositivi registrati con la gestione di dispositivi mobili (MDM) di Intune. Per gestire le app con MDM e MAM, i clienti devono usare Intune nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
- **MAM senza registrazione del dispositivo**: questa configurazione, detta anche MAM-WE, consente agli amministratori IT di gestire le app tramite MAM e i criteri di protezione delle app nei dispositivi non registrati con MDM di Intune. Ciò significa che le app possono essere gestite da Intune nei dispositivi registrati con provider EMM di terze parti. Per gestire le app con MAM-WE, i clienti devono usare Intune nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431). Le app possono essere gestite da Intune anche nei dispositivi registrati con provider EMM (Enterprise Mobility Management) di terze parti o non registrati affatto in un sistema MDM. Per altre informazioni su BYOD ed EMS di Microsoft, vedere [Decisioni in merito alla tecnologia per l'abilitazione di BYOD con Microsoft Enterprise Mobility + Security (EMS)](../fundamentals/byod-technology-decisions.md).

## <a name="app-management-capabilities-by-platform"></a>Funzionalità di gestione delle app per piattaforma

Intune offre un'ampia gamma di funzionalità che consente di usare le app necessarie nei dispositivi in cui le si vuole eseguire. Nella tabella seguente è disponibile un riepilogo delle funzionalità di gestione delle app.

| Funzionalità di gestione delle app | Android/Android Enterprise | iOS/iPadOS | macOS | Windows 10 |
|-------------------------- | -------------------------- | ---------- | ----- | ---------- |
| Aggiunta e assegnazione delle app a utenti e dispositivi | Sì | Sì | Sì | Sì |
| Assegnazione delle app a dispositivi non registrati con Intune | Sì | Sì | No | No |  |
| Uso dei criteri di configurazione delle app per controllare il comportamento di avvio delle app | Sì | Sì | No | No |
| Uso dei criteri di provisioning delle app per dispositivi mobili per rinnovare app scadute | No | Sì | No | No |
| Protezione dei dati aziendali in app con criteri di protezione delle app | Sì | Sì | No | No <sup>1</sup> |
| Rimozione solo dei dati aziendali da un'app installata (cancellazione selettiva di app) | Sì | Sì | No | Sì |
| Monitoraggio delle assegnazioni di app | Sì | Sì | Sì | Sì |
| Assegnazione e monitoraggio delle app acquistate con Volume Purchase Program da un App Store | No | No | No | Sì |
| Installazione obbligatoria delle app nei dispositivi (obbligatorio) <sup>2</sup> | Sì | Sì | Sì | Sì |
| Installazione facoltativa nei dispositivi dal Portale aziendale (installazione disponibile) | Sì <sup>3</sup> | Sì | Sì | Sì |
| Installazione di un collegamento a un'app sul Web (collegamento Web) | Sì <sup>4</sup> | Sì | Sì | Sì |
| App interne (line-of-business) | Sì | Sì | Sì | Sì |
| App da uno Store | Sì | Sì | No | Sì |
| Aggiornare le app | Sì | Sì | No | Sì |

<sup>1</sup> Considerare l'uso di [Windows Information Protection](../protect/windows-information-protection-configure.md) per proteggere le applicazioni sui dispositivi che eseguono Windows 10.<br>
<sup>2</sup> Si applica solo ai dispositivi gestiti da Intune.<br>
<sup>3</sup> Intune supporta le app disponibili in Google Play Store gestito per i dispositivi Android Enterprise.<br>
<sup>4</sup> Intune non supporta l'installazione di un collegamento a un'app come collegamento Web per i dispositivi Android Enterprise standard. Tuttavia, i collegamenti Web sono supportati per i [dispositivi Android Enterprise dedicati con più app](../configuration/device-restrictions-android-for-work.md#device-experience). 


## <a name="get-started"></a>Operazioni preliminari

Il carico di lavoro **App** contiene numerose informazioni sulle app ed è accessibile seguendo questa procedura:

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Selezionare **App**.

    ![Riquadro del carico di lavoro App](./media/app-management/apps-workload.png)

Il carico di lavoro App fornisce collegamenti per accedere alle informazioni e alle funzionalità comuni delle app. 

Nella parte superiore del menu di spostamento del carico di lavoro App sono disponibili i dettagli dell'app comunemente usati:
- **Informazioni generali**: selezionare questa opzione per visualizzare il nome del tenant, l'autorità MDM, il percorso del tenant, lo stato dell'account, lo stato di installazione dell'app e lo stato dei criteri di protezione delle app.
- **Tutte le app**: selezionare questa opzione per visualizzare un elenco di tutte le app disponibili. È possibile aggiungere altre app da questa pagina. È inoltre possibile visualizzare lo stato di ogni app e determinare se ogni app è assegnata. Per altre informazioni, vedere [Aggiungere app](apps-add.md) e [Assegnare app](apps-deploy.md).
- **Monitoraggio le applicazioni**
    - **Licenze dell'app**: consente di visualizzare, assegnare e monitorare le app acquistate con Volume Purchase Program dagli App Store. Per altre informazioni, vedere [App per iOS acquistate tramite Volume Purchase Program di Apple](vpp-apps-ios.md) e [App acquistate in base al volume tramite Microsoft Store per le aziende](windows-store-for-business.md).
    - **App individuate**: visualizza le app assegnate da Intune o installate in un dispositivo. Per altre informazioni, vedere [App individuate da Intune](app-discovered-apps.md).
    - **Stato di installazione dell'app**: visualizza lo stato di un'assegnazione di app creata. Per altre informazioni, vedere [Monitorare le informazioni sulle app e le assegnazioni con Microsoft Intune](apps-monitor.md#device-and-user-status-graphs).
    - **Stato di protezione dell'app**: visualizza lo stato dei criteri di protezione delle app per un utente selezionato.
- **Per piattaforma**: selezionare queste piattaforme per visualizzare le app disponibili in base alla piattaforma.
    - Windows
    - iOS
    - macOS
    - Android
- **Policy** (Criteri):
    - **Criteri di protezione delle app**: selezionare questa opzione per associare le impostazioni a un'app e proteggere i dati aziendali usati dall'app. Ad esempio, si potrebbero limitare le funzionalità di comunicazione di un'applicazione con altre applicazioni o richiedere all'utente di immettere un PIN per accedere a un'app aziendale. Per altre informazioni, vedere [Criteri di protezione delle app](app-protection-policies.md).
    - **Criteri di configurazione dell'app**: selezionare questa opzione per specificare le impostazioni che possono essere necessarie quando un utente esegue un'app. Per altre informazioni, vedere [Criteri di configurazione delle app](app-configuration-policies-use-ios.md), [Criteri di configurazione delle app per iOS](app-configuration-policies-use-ios.md) e [Criteri di configurazione delle app per Android](app-configuration-policies-overview.md).
    - **Profili di provisioning delle app iOS**: le app iOS includono un profilo di provisioning e codice firmato da un certificato. Quando il certificato scade, l'app non può più essere eseguita. Intune offre gli strumenti per assegnare in modo proattivo un nuovo criterio del profilo di provisioning ai dispositivi con app prossime alla scadenza. Per altre informazioni, vedere [Profili di provisioning delle app per iOS](app-provisioning-profile-ios.md).
    - **Criteri supplementari per la modalità S**: selezionare questa opzione per autorizzare l'esecuzione di applicazioni aggiuntive nei dispositivi gestiti in modalità S. Per altre informazioni, vedere [Criteri supplementari per la modalità S](apps-win32-s-mode.md).
    - **Criteri per le app di Office**: selezionare questa opzione per creare criteri di gestione delle app per dispositivi mobili per le app di Office per dispositivi mobili che si connettono ai servizi di Microsoft 365. È anche possibile proteggere l'accesso alle cassette postali locali di Exchange creando criteri di protezione delle app di Intune per Outlook per iOS/iPadOS e Android abilitati con l'autenticazione moderna ibrida. È necessario che siano soddisfatti i requisiti per l'uso dei criteri per le app di Office. Per altre informazioni sui requisiti, vedere [Requisiti per l'uso del servizio criteri cloud di Office](https://docs.microsoft.com/deployoffice/overview-office-cloud-policy-service#requirements-for-using-the-office-cloud-policy-service). I criteri di protezione delle app non sono supportati per le altre app che si connettono ai servizi locali di Exchange o SharePoint. Per informazioni correlate, vedere [Panoramica del servizio di criteri del cloud di Office per Microsoft 365 Apps for enterprise](https://docs.microsoft.com/deployoffice/overview-office-cloud-policy-service).
    - **Set di criteri**: selezionare questa opzione per creare una raccolta assegnabile di app, criteri e altri oggetti di gestione creati. Per altre informazioni, vedere [Set di criteri](../fundamentals/policy-sets.md).
- **Altro**:   
    - **Cancellazione selettiva di app**: selezionare questa opzione per rimuovere solo i dati aziendali dal dispositivo di un utente selezionato. Per altre informazioni, vedere [Cancellazione selettiva di app](apps-selective-wipe.md).
    - **Categorie di app**: consente di aggiungere ed eliminare nomi di categoria di app.
    - **E-book**: Alcuni App Store consentono di acquistare più licenze per app o libri da eseguire nell'azienda. Per altre informazioni, vedere [Gestire le app e i libri acquistati con Volume Purchase Program con Microsoft Intune](vpp-apps.md).
- **Guida e supporto tecnico**: consente di risolvere i problemi, richiedere supporto o visualizzare lo stato di Intune. Per altre informazioni, vedere [Risolvere i problemi](../fundamentals/help-desk-operators.md).

### <a name="try-the-interactive-guide"></a>Provare la guida interattiva
La guida interattiva [Gestire e proteggere le applicazioni per dispositivi mobili e desktop con Microsoft Endpoint Manager](https://mslearn.cloudguides.com/guides/Manage%20and%20protect%20mobile%20and%20desktop%20applications%20with%20Microsoft%20Endpoint%20Manager) presenta in modo dettagliato l'interfaccia di amministrazione di Microsoft Endpoint Manager per illustrare come gestire i dispositivi registrati in Intune, imporre la conformità con i criteri e proteggere i dati dell'organizzazione.</br></br>

<div align=”center”>
<iframe allowfullscreen width="95%" height="450" src="https://mslearn.cloudguides.com/guides/Manage%20and%20protect%20mobile%20and%20desktop%20applications%20with%20Microsoft%20Endpoint%20Manager" frameborder="0" scrolling="no" loading="lazy"/></iframe>
</div>

## <a name="additional-information"></a>Informazioni aggiuntive
Gli elementi seguenti all'interno della console offrono funzionalità correlate alle app:
- **Microsoft Store per le aziende**: consente di configurare l'integrazione di Microsoft Store per le aziende. In seguito è possibile sincronizzare le applicazioni acquistate con Intune, assegnarle e monitorare l'uso delle licenze. Per altre informazioni, vedere [App acquistate in base al volume tramite Microsoft Store per le aziende](windows-store-for-business.md).
- **Certificato Windows Enterprise**: consente di applicare o visualizzare lo stato di un certificato di firma del codice usato per distribuire le app line-of-business ai dispositivi Windows gestiti.
- **Certificato Symantec per Windows**: Applicare o visualizzare lo stato di un certificato di firma codice Symantec.
- **Chiavi di sideload Windows**: consente di aggiungere una chiave di sideload di Windows che può essere usata per installare un'app direttamente nei dispositivi, invece di pubblicare e scaricare l'app da Windows Store. Per altre informazioni, vedere [Sideload di un'app di Windows](app-sideload-windows.md).
- **Token VPP Apple**: consente di applicare e visualizzare le licenze Volume Purchase Program (VPP) di iOS. Per altre informazioni, vedere [App per iOS/iPadOS acquistate con Volume Purchase Program di Apple](vpp-apps-ios.md).
- **Google Play gestito**: Google Play gestito è lo store di app aziendali di Google e l'unica origine di applicazioni per Android Enterprise. Per altre informazioni, vedere [Aggiungere app di Google Play gestite a dispositivi Android Enterprise con Intune](apps-add-android-for-work.md).
- **Personalizzazione**: consente di personalizzare il Portale aziendale con il marchio dell'azienda. Per altre informazioni, vedere [Configurazione dell'app Portale aziendale](company-portal-app.md).

Per altre informazioni sulle app, vedere [Aggiungere app in Microsoft Intune](../apps/apps-add.md).

## <a name="next-steps"></a>Passaggi successivi

- [Aggiungere un'app a Microsoft Intune](apps-add.md)
