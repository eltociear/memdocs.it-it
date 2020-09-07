---
title: Gestione dei dispositivi in Microsoft 365
description: Microsoft 365 Enterprise include Microsoft Intune. Capire le funzionalità di gestione dei dispositivi e delle applicazioni mobili che Intune offre all'organizzazione. Leggere gli scenari comuni e usare Intune per distribuire Microsoft 365 nel proprio ambiente.
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/24/2020
ms.topic: overview
audience: microsoft-business
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.technology: ''
ms.assetid: 0649d310-43a7-4b01-85d2-da255d03e1da
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: microsoft-intune
ms.collection: M365-identity-device-management
ms.openlocfilehash: c7d5583addc4e76f5af0ea0b9780f20d8fa78a2c
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88996198"
---
# <a name="device-management-overview"></a>Panoramica della gestione dei dispositivi

Attività chiave che spettano a qualsiasi amministratore sono la protezione e la messa in sicurezza delle risorse e dei dati dell'organizzazione nei dispositivi degli utenti. Questa attività è la **gestione dei dispositivi**. Gli utenti ricevono e inviano messaggi di posta elettronica da account personali, esplorano siti Web da casa e da luoghi pubblici e installano app e giochi. Questi utenti sono anche dipendenti e studenti e quindi vogliono accedere con la massima rapidità dai propri dispositivi alle risorse di lavoro o di studio, ad esempio la posta elettronica o OneNote. L'obiettivo dell'amministratore è, allo stesso tempo, proteggere queste risorse e consentire agli utenti un accesso facile con tutti i dispositivi disponibili per loro.

La gestione dei dispositivi consente alle organizzazioni di proteggere e mettere in sicurezza le risorse e i dati di dispositivi diversi.

Tramite un provider per la gestione dei dispositivi, le organizzazioni possono assicurarsi che solo gli utenti e i dispositivi autorizzati riescano ad accedere alle informazioni proprietarie. Analogamente, gli utenti dei dispositivi possono accedere ai dati di lavoro dal proprio telefono in tutta tranquillità, perché sanno che il dispositivo soddisfa i requisiti di sicurezza dell'organizzazione. Un'organizzazione potrebbe chiedersi **che strumenti usare per proteggere le proprie risorse**.

La risposta è [Microsoft Intune](what-is-intune.md). Intune mette a disposizione servizi di gestione dei dispositivi mobili (MDM) e di gestione delle app mobili (MAM). Alcune attività chiave che deve poter svolgere qualsiasi soluzione MDM o MAM sono:

- Supportare un ambiente per dispositivi mobili eterogeneo e gestire i dispositivi iOS/iPadOS, Android, Windows e macOS in modo sicuro.
- Assicurarsi che i dispositivi e le app siano conformi ai requisiti di sicurezza aziendali.
- Creare criteri che consentano di proteggere i dati aziendali nei dispositivi personali e di proprietà dell'organizzazione.
- Usare una soluzione mobile singola e unificata per applicare questi criteri e facilitare la gestione di dispositivi, app, utenti e gruppi.
- Proteggere le informazioni aziendali grazie alla possibilità di controllare in che modo il personale può accedere e condividere i dati.

Intune è incluso con Microsoft Azure, Microsoft 365 e si integra con Azure Active Directory (Azure AD). Azure AD consente di controllare chi ha accesso e a cosa.

## <a name="microsoft-intune"></a>Microsoft Intune

Molte organizzazioni, come Microsoft, usano Intune per proteggere i dati proprietari a cui gli utenti accedono dai dispositivi mobili personali e aziendali. Intune include criteri di configurazione di dispositivi e app, criteri di aggiornamento software e stati dell'installazione, come grafici, tabelle e report, che consentono di proteggere e monitorare l'accesso ai dati.

È consueto per le persone utilizzare più dispositivi che usano piattaforme diverse. Ad esempio, un dipendente potrebbe usare Surface Pro per il lavoro e un dispositivo mobile Android per la vita privata. Ed è consueto per una persona accedere alle risorse aziendali, ad esempio Microsoft Outlook e SharePoint, da questi vari dispositivi.

Intune consente di gestire più dispositivi per ogni persona e le diverse piattaforme in esecuzione in ogni dispositivo, tra cui iOS/iPadOS, macOS, Android e Windows. Intune separa i criteri e le impostazioni in base alla piattaforma del dispositivo. Pertanto è facile gestire e visualizzare i dispositivi di una piattaforma specifica.

**[Scenari comuni](common-scenarios.md)** è un'ottima risorsa per capire come Intune gestisce situazioni comuni in cui sono coinvolti dispositivi mobili. Sono disponibili scenari su:  

- Protezione della posta elettronica con Exchange locale
- Accesso a Microsoft 365 in modo sicuro e protetto
- Uso di dispositivi personali per accedere a risorse aziendali

Per altre informazioni su Intune, vedere [informazioni su Intune](what-is-intune.md).

## <a name="co-management"></a>Co-gestione

Molte organizzazioni usano Configuration Manager a livello locale per gestire dispositivi, inclusi i desktop e i server. È possibile associare tramite cloud l'istanza locale di Configuration Manager a Microsoft Intune. Quando si esegue l'associazione al cloud, si ottengono sia i vantaggi di Intune sia quelli del cloud, tra cui l'[accesso condizionale](../../configmgr/comanage/quickstart-conditional-access.md), l'[esecuzione di azioni remote](../../configmgr/comanage/quickstart-remote-actions.md), l'[uso di Windows Autopilot](../../configmgr/comanage/quickstart-autopilot.md), e altro ancora.

[Microsoft Endpoint Manager](../../endpoint-manager-overview.md) è una piattaforma di soluzioni che riunisce diverse tecnologie. Include [Microsoft Intune](what-is-intune.md) per la gestione dei dispositivi basati sul cloud e [Configuration Manager + Intune](../../configmgr/comanage/overview.md) per la gestione dei dispositivi associati al cloud.

Se si usa Configuration Manager e si è pronti a spostare alcune attività nel cloud, la co-gestione è la soluzione ottimale.

Per altre informazioni sull'associazione al cloud di Configuration Manager, vedere [Informazioni sulla co-gestione](../../configmgr/comanage/overview.md).

## <a name="integration-with-secure-and-protect-services"></a>Integrazione con servizi di sicurezza e protezione

Fornire sicurezza e protezione è un compito fondamentale che deve svolgere qualsiasi soluzione di gestione dei dispositivi. Intune svolge questo compito in modo particolarmente efficace integrandosi con altri servizi. Ad esempio:

- **Microsoft 365** è un componente chiave per semplificare le attività IT più comuni. Dall'interfaccia di amministrazione di Microsoft 365 è possibile creare utenti, gestire gruppi e accedere ad altri servizi, ad esempio Intune, Azure AD e così via.

  È ad esempio possibile creare un gruppo di dispositivi iOS/iPadOS in Microsoft 365 e usare Intune per eseguire il push dei criteri nel gruppo di dispositivi iOS/iPadOS che usano le funzionalità iOS, ad esempio l'accesso all'App Store, l'uso di AirDrop, il backup in iCloud, l'uso del filtro Web di Apple e così via.

- **Windows Defender** include molte funzionalità di sicurezza per proteggere i dispositivi Windows 10. Ad esempio, usando Intune e Windows Defender insieme, è possibile:

  - Abilitare [Windows Defender SmartScreen](../protect/endpoint-protection-windows-10.md) per individuare attività sospette nei file e nelle app dei dispositivi mobili.
  - Usare [Microsoft Defender Advanced Threat Protection](../protect/advanced-threat-protection.md) per prevenire le violazioni della sicurezza nei dispositivi mobili. Consente, inoltre, di limitare l'impatto di una violazione della sicurezza impedendo a un utente di accedere alle risorse aziendali.

- L'**accesso condizionale** è una funzionalità di Azure Active Directory che si integra perfettamente con Intune. Usando l'[accesso condizionale](../protect/conditional-access.md) è possibile fare in modo che solo i dispositivi conformi accedano alla posta elettronica, a SharePoint e ad altre app.

## <a name="choose-the-device-management-solution-thats-right-for-you"></a>Scegliere la soluzione di gestione dei dispositivi adatta alle esigenze della propria azienda

Esistono un paio di metodi per affrontare la gestione dei dispositivi. In primo luogo, è possibile gestire vari aspetti dei dispositivi facendo leva sulle funzionalità integrate in Intune. Questo metodo si chiama **Gestione di dispositivi mobili (MDM)** . Gli utenti "registrano" i propri dispositivi e usano certificati per comunicare con Intune. Gli amministratori IT eseguono il push delle app nei dispositivi, limitano i dispositivi a un unico sistema operativo, bloccano i dispositivi personali e altro ancora. Se un dispositivo viene smarrito o rubato, sarà possibile anche rimuovere tutti i dati dal dispositivo.

Il secondo metodo, invece, prevede la gestione delle app nei dispositivi. Questo metodo si chiama **Gestione di applicazioni mobili (MAM)** . Gli utenti possono usare i propri dispositivi personali per accedere alle risorse aziendali. Quando gli utenti aprono un'app, ad esempio la posta elettronica o SharePoint, viene richiesta un'autenticazione aggiuntiva. Se un dispositivo viene smarrito o rubato, sarà anche possibile rimuovere tutti i dati dell'organizzazione dalle applicazioni gestite da Intune.

È anche possibile combinare tra loro [MDM e MAM](byod-technology-decisions.md).

Quando si configura Intune, è possibile scegliere di gestire i dispositivi esclusivamente nel portale di Azure oppure usando Intune e Microsoft 365 insieme. [Migrating mobile device management to Intune in the Azure portal](https://www.microsoft.com/itshowcase/Article/Content/1042/Migrating-mobile-device-management-to-Intune-in-the-Azure-portal) (Migrazione della gestione dei dispositivi mobili a Intune nel portale di Azure) è un case study di Microsoft IT. Nel case study si può vedere come Microsoft IT abbia scelto un approccio moderno alla gestione dei dispositivi e leggere l'analisi di fine progetto.

## <a name="simplify-it-tasks-using-the-device-management-admin-center"></a>Semplificare le attività IT usando il centro di amministrazione Gestione dei dispositivi

L'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) è una posizione centralizzata in cui gestire e completare tutte le attività relative ai dispositivi mobili. Questa area di lavoro include i servizi usati per la gestione dei dispositivi, tra cui Intune e Azure Active Directory, e per la gestione delle app client.

Nell'interfaccia di amministrazione di Gestione dei dispositivi è possibile eseguire le operazioni seguenti:

- [Registrare i dispositivi](../enrollment/device-enrollment.md)
- [Impostare la conformità dei dispositivi](../protect/device-compliance-get-started.md)
- [Gestire i dispositivi](../remote-actions/device-management.md)
- [Gestire le app](../apps/app-management.md)  
- [eBook iOS](../apps/vpp-ebooks-ios.md)  
- [Installare On-premises Exchange Connector](../protect/exchange-connector-install.md)  
- [Gestire i ruoli](role-based-access-control.md)  
- Gestire gli aggiornamenti software
  - [Gestire gli aggiornamenti di Windows 10](../protect/windows-update-for-business-configure.md)  
  - [Gestire gli aggiornamenti di iOS/iPadOS](../protect/software-updates-ios.md)  
- [Azure Active Directory](/azure/active-directory)  
- [Gestire gli utenti](/azure/active-directory/fundamentals/add-users-azure-active-directory)
- [Gestire gruppi e membri](/azure/active-directory/fundamentals/active-directory-manage-groups)
- [Risolvere i problemi](help-desk-operators.md)

## <a name="next-steps"></a>Passaggi successivi

Quando si è pronti per iniziare a usare una soluzione MDM o MAM, eseguire i vari passaggi per configurare Intune, registrare i dispositivi e iniziare a creare i criteri. Anche [Gestione dei dispositivi mobili per Microsoft 365](/microsoft-365/enterprise/mobility-infrastructure) è un'ottima risorsa.