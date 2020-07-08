---
title: Panoramica di Microsoft Endpoint Manager - Azure | Microsoft Docs
description: Endpoint Manager include Intune, Configuration Manager, la co-gestione, Desktop Analytics, Windows Autopilot e l'interfaccia di amministrazione per gestire tutti i dispositivi, incluso l'ambiente locale.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/21/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: ''
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2095fdd349437e03c673fb9f7906511c5e3af388
ms.sourcegitcommit: e713f8f4ba2ff453031c9dfc5bfd105ab5d00cd9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/08/2020
ms.locfileid: "86088378"
---
# <a name="microsoft-endpoint-manager-overview"></a>Panoramica di Microsoft Endpoint Manager

Microsoft Endpoint Manager offre strumenti moderni per l'area di lavoro e la gestione, che garantiscono la sicurezza dei dati sia nel cloud sia in locale. Endpoint Manager include servizi e strumenti che consentono di gestire e monitorare dispositivi mobili, computer desktop, macchine virtuali, dispositivi incorporati e server.

Endpoint Manager integra servizi noti e possibilmente già in uso, tra cui Microsoft Intune, Configuration Manager, Desktop Analytics, co-gestione e Windows Autopilot. Questi servizi fanno parte dello stack Microsoft 365 e contribuiscono a proteggere l'accesso e i dati e a contrastare e gestire i rischi.

Per iniziare, guardare questo video di due minuti di Brad Anderson, vicepresidente di Microsoft, per Microsoft 365:

> [!VIDEO https://www.youtube.com/embed/GS7oNPInFuw]

## <a name="what-you-get"></a>Componenti

Endpoint Manager include i servizi seguenti:

- **Microsoft Intune**: Microsoft Intune è un provider di gestione di dispositivi mobili (MDM, Mobile Device Management) e gestione di applicazioni mobili (MAM, Mobile Application Management) 100% cloud per app e dispositivi. Consente di gestire caratteristiche e impostazioni nei dispositivi Android, Android Enterprise, iOS/iPadOS, macOS e Windows 10. Si integra con altri servizi, tra cui Azure Active Directory (AD), servizi Mobile Threat Defender, modelli ADMX, app Win32 e LOB personalizzate e altro ancora.

  Se si ha un'infrastruttura locale, ad esempio Exchange o Active Directory, sono disponibili anche i connettori di Intune:

  - Il **Connettore di Intune per Active Directory** aggiunge voci al dominio dell'istanza locale di Active Directory per i computer che eseguono la registrazione usando Windows Autopilot. Per altre informazioni, vedere [Distribuire dispositivi aggiunti ad Azure AD ibrido](/mem/intune/enrollment/windows-autopilot-hybrid).
  - Il **Connettore di certificati di Intune** elabora le richieste di certificati di dispositivi che usano i certificati per l'autenticazione e la crittografia della posta elettronica S/MIME. Per altre informazioni, vedere [Usare i certificati per l'autenticazione](/mem/intune/protect/certificates-configure).

  Nel contesto di Endpoint Manager, è possibile usare Intune per creare e verificare la conformità e distribuire app, funzionalità e impostazioni ai dispositivi tramite il cloud.

  Per altre informazioni, vedere [Informazioni su Microsoft Intune](https://docs.microsoft.com/intune/fundamentals/what-is-intune).

- **Configuration Manager**: Configuration Manager è una soluzione di gestione locale per gestire desktop, server e computer portatili collegati nella rete aziendale o in Internet. È possibile abilitare la soluzione per il cloud e integrarla con Intune, Azure Active Directory (AD), Microsoft Defender ATP e altri servizi cloud. Usare Configuration Manager per distribuire app, aggiornamenti software e sistemi operativi. È anche possibile monitorare la conformità, eseguire query, intervenire sui client in tempo reale e molto altro ancora.

  Nel contesto di Endpoint Manager è possibile continuare a usare Configuration Manager come di consueto. Se si è pronti a spostare alcune attività nel cloud, prendere in considerazione la [co-gestione](https://docs.microsoft.com/configmgr/comanage/).

  Per altre informazioni, vedere [Che cos'è Configuration Manager](https://docs.microsoft.com/configmgr/core/understand/introduction).

- **Co-gestione**: la co-gestione integra l'investimento esistente in Configuration Manager locale con il cloud, tramite l'uso di Intune e di altri servizi cloud Microsoft 365. È possibile scegliere Configuration Manager o Intune come autorità di gestione per i sette diversi gruppi di carico di lavoro.

  Nel contesto di Endpoint Manager la co-gestione usa le funzionalità cloud, incluso l'accesso condizionale. Alcune attività restano in locale, mentre altre vengono eseguite nel cloud con Intune.

  Per altre informazioni, vedere [What is co-management?](https://docs.microsoft.com/configmgr/comanage/overview) (Informazioni sulla co-gestione).

- **Desktop Analytics**: Desktop Analytics è un servizio basato sul cloud che si integra con Configuration Manager. Offre dati analitici e intelligence per consentire agli utenti di prendere decisioni più informate sull'idoneità degli aggiornamenti dei client Windows. Combina i dati dell'organizzazione con i dati aggregati di milioni di dispositivi connessi al cloud Microsoft. Offre informazioni sulle patch di sicurezza, le app e i dispositivi dell'organizzazione e identifica i problemi di compatibilità con app e driver. È consigliabile creare un progetto pilota con i dispositivi che hanno maggior probabilità di restituire informazioni cognitive dettagliate relative alle risorse nell'intera organizzazione.

  Nel contesto di Endpoint Manager, usare le informazioni cognitive dettagliate basate sul cloud di Desktop Analytics per mantenere aggiornati i dispositivi Windows 10.

  Per altre informazioni, vedere [Che cos'è Desktop Analytics?](https://docs.microsoft.com/configmgr/desktop-analytics/overview).

- **Windows Autopilot**: questa soluzione configura e preconfigura i nuovi dispositivi, preparandoli per l'uso. È progettata per semplificare il ciclo di vita dei dispositivi Windows sia per l'ufficio IT che per gli utenti finali, dalla distribuzione iniziale fino alla fine della vita utile.

  Nel contesto di Endpoint Manager è possibile usare Autopilot per preconfigurare i dispositivi e registrarli automaticamente in Intune. È anche possibile integrare Autopilot con Configuration Manager e la co-gestione, per configurazioni di dispositivi più complesse (funzionalità in anteprima).

  Per altre informazioni, vedere [Panoramica di Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot) e [Registrare dispositivi Windows in Intune](/mem/intune/enrollment/enrollment-autopilot).

- **Azure Active Directory (AD)** : Azure AD viene usato da Endpoint Manager per l'identità di dispositivi, utenti, gruppi e autenticazione a più fattori (MFA). **Azure AD Premium**, che può essere un costo aggiuntivo, ha [funzionalità aggiuntive](https://azure.microsoft.com/pricing/details/active-directory/) per proteggere i dispositivi, le app e i dati, inclusi i gruppi dinamici, la registrazione automatica e l'accesso condizionale.

  Per altre informazioni, vedere [Aggiungere utenti](/mem/intune/fundamentals/users-add), [Configurare la registrazione automatica](/mem/intune/enrollment/windows-enroll) e [Informazioni sull'accesso condizionale](/mem/intune/protect/conditional-access).

- **Interfaccia di amministrazione di Endpoint Manager**: l'[interfaccia di amministrazione](https://go.microsoft.com/fwlink/?linkid=2109431) è un sito Web completo per tutte le operazioni di creazione criteri e gestione di dispositivi. Si integra con altri servizi chiave di gestione dei dispositivi, inclusi i gruppi, la sicurezza, l'accesso condizionale e la creazione di report. Questa interfaccia di amministrazione visualizza anche i dispositivi gestiti da Configuration Manager e Intune (in anteprima).

## <a name="choose-whats-right-for-you"></a>Scegliere la soluzione più adatta alle proprie esigenze

Esistono vari modi per determinare la soluzione ottimale per l'organizzazione. Le scelte successive dipendono dalle attività svolte dall'organizzazione. Considerare che cosa si vuole ottenere.

Ad esempio:

- Se si esegue costantemente il provisioning di nuovi dispositivi, iniziare con Windows Autopilot.
- Se si aggiungono regole e impostazioni di controllo per gli utenti, le app e i dispositivi, iniziare con Intune.
- Se si usa già Configuration Manager per distribuire le app e si vuole usare l'accesso condizionale basato su requisiti di sicurezza, iniziare con la co-gestione.
- Se si usa già Configuration Manager e si è responsabili dell'aggiornamento costante dei dispositivi Windows 10, iniziare Desktop Analytics.
- Se ci si sta avvicinando alla gestione di dispositivi mobili (MDM) e alla gestione di applicazioni mobili (MAM) o se si usano i modelli ADMX per controllare le impostazioni di Office, Microsoft Edge e Windows, iniziare con Intune.

È anche possibile pensare a Endpoint Manager come a un'entità in tre parti: cloud, locale e cloud + locale:

- **Cloud**: tutti i dati sono archiviati in Azure. I data center non vengono più usati. Questo approccio offre i vantaggi di mobilità del cloud e i vantaggi di sicurezza di Azure.

- **Infrastruttura locale**: se si ha un'infrastruttura locale che include Configuration Manager o non si è pronti a usare il cloud, è possibile conservare i sistemi esistenti.

- **Cloud + locale**: questo approccio unisce ambienti diversi ed è caratterizzato dal collegamento al cloud. Usa una combinazione di soluzioni cloud e locali. Per i nuovi dispositivi, sfruttare i vantaggi di Intune per accedere ai dati e proteggerli. Se si usa Configuration Manager, connettersi al cloud per ottenere funzionalità e analisi aggiuntive. Se si vuole spostare alcuni carichi di lavoro nel cloud, la co-gestione è una scelta efficace.

## <a name="what-you-need-to-get-started"></a>Passaggi preliminari

Microsoft Endpoint Manager è una piattaforma per soluzioni che riunisce diverse tecnologie. Non si tratta di una nuova licenza. I servizi vengono concessi in licenza in base alle singole condizioni di licenza. Per altre informazioni, vedere le [condizioni di licenza per il prodotto](https://www.microsoft.com/licensing/product-licensing/products).

Se si usa già Configuration Manager, si avrà a disposizione anche Microsoft Intune per la co-gestione dei dispositivi Windows. Per le altre piattaforme, come iOS/iPadOS e Android, è necessaria una licenza di Intune separata.

Nella maggior parte degli scenari l'opzione migliore è Microsoft 365, perché include Endpoint Manager e Office 365. Per altre informazioni, vedere [Microsoft 365](https://www.microsoft.com/licensing/product-licensing/microsoft-365-enterprise).

## <a name="next-steps"></a>Passaggi successivi

[Usare la potenza dell'intelligence cloud per semplificare e accelerare le procedure IT e implementare un'area di lavoro moderna](https://www.microsoft.com/microsoft-365/blog/2019/11/04/use-the-power-of-cloud-intelligence-to-simplify-and-accelerate-it-and-the-move-to-a-modern-workplace/)

[Microsoft Endpoint Manager](https://www.microsoft.com/microsoft-365/microsoft-endpoint-manager)

[Esercitazione: Procedura dettagliata per Intune in Microsoft Endpoint Manager](/intune/fundamentals/tutorial-walkthrough-endpoint-manager)

[Modulo di apprendimento - Che cos'è Microsoft 365](https://docs.microsoft.com/learn/modules/what-is-m365/index)
