---
title: Novità di Desktop Analytics
titleSuffix: Configuration Manager
description: Riepilogo delle nuove funzionalità della versione mensile più recente del servizio cloud Desktop Analytics.
ms.date: 08/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: fa300181-86cb-4afe-8fbf-895a7572378d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: c41c6333cfee1b6a24bb84c0f020c14c303fd904
ms.sourcegitcommit: 62b451396eae660f2d5289ae3666b19ed1cc666d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/19/2020
ms.locfileid: "88614740"
---
# <a name="whats-new-in-desktop-analytics"></a>Novità di Desktop Analytics

Informazioni sulle novità mensili di Desktop Analytics.

> [!TIP]
> L'implementazione degli aggiornamenti mensili può richiedere fino a tre giorni. Alcune funzionalità possono essere implementate in diverse settimane e durante la prima è possibile che non siano disponibili per tutti i clienti.

Per ricevere una notifica quando questa pagina viene aggiornata, copiare e incollare l'URL seguente nel lettore di feed RSS: `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+desktop+analytics+-+Configuration+Manager%22&locale=en-us`
<!-- a locale is required for the RSS search string -->

## <a name="august-2020"></a>Agosto 2020

### <a name="apps-deployed-from-configuration-manager-are-important-by-default"></a>Le app distribuite da Configuration Manager sono importanti per impostazione predefinita

<!-- 4859763 -->

La configurazione dell'**importanza** di un'app è essenziale per consentire a Desktop Analytics di determinare i dispositivi da includere nelle distribuzioni pilota. Un amministratore doveva configurare manualmente l'importanza per tutte le app in Desktop Analytics. Solo dopo aver convalidato il progetto pilota era possibile continuare con una distribuzione di produzione.

Ora qualsiasi app distribuita con Configuration Manager viene automaticamente configurata come importante da Desktop Analytics per impostazione predefinita. Questo comportamento consente di configurare più rapidamente le app nell'ambiente per accelerare il percorso verso una distribuzione di produzione.

Per altre informazioni, vedere [Asset - App](about-assets.md#apps).

## <a name="july-2020"></a>Luglio 2020

### <a name="windows-10-version-2004-now-available-in-desktop-analytics"></a>Windows 10, versione 2004, ora disponibile in Desktop Analytics

<!-- 7370207 -->

Nel portale di Desktop Analytics, quando si esegue il monitoraggio degli aggiornamenti della sicurezza e delle funzionalità, viene ora visualizzato Windows 10 versione 2004. Quando si crea un piano di distribuzione, è possibile selezionare Windows 10 versione 2004 come versione di destinazione.

### <a name="improved-support-for-viewing-the-portal-from-any-device"></a>Supporto migliorato per la visualizzazione del portale da qualsiasi dispositivo

<!-- 6270240 -->

È ora possibile visualizzare il portale di Desktop Analytics nell'interfaccia di amministrazione di Microsoft Endpoint Manager da diversi tipi di dispositivi. Ora soddisfa le linee guida per l'accessibilità del contenuto Web (WCAG) 2.1 per una risoluzione dello schermo di 320 x 256 pixel. Ad esempio, l'immagine seguente rappresenta il portale da un Apple iPhone 8:

:::image type="content" source="media/dashboard-iphone8.png" alt-text="Portale di Desktop Analytics in un iPhone 8":::

### <a name="notifications-for-service-impacting-events"></a>Notifiche per gli eventi con conseguenze sul servizio

<!-- 4982509 -->

Il portale di Desktop Analytics può ora visualizzare banner di notifica. Queste notifiche consentono a Microsoft di comunicare con l'utente in merito a eventi e problemi importanti. Ad esempio, problemi noti relativi al servizio o alla latenza dei dati o informazioni sui nuovi prerequisiti. Per altre informazioni, vedere [Notifiche del servizio](troubleshooting.md#service-notifications).

## <a name="june-2020"></a>Giugno 2020

### <a name="improvement-to-prerequisites"></a>Miglioramenti dei prerequisiti

Desktop Analytics non richiede più la distribuzione di un servizio di Office 365 nel tenant di Azure Active Directory (Azure AD). L'app **Amministratore client Office 365** in Azure AD è ora l'app **Desktop Analytics**, per abilitare il recupero delle informazioni e dello stato dal servizio da parte di Configuration Manager.

## <a name="may-2020"></a>Maggio 2020

### <a name="reduce-the-number-of-apps-for-review"></a>Ridurre il numero di app per la revisione

<!-- 5542186 -->

Per contribuire al consolidamento e alla riduzione del numero di app visualizzate nella pagina delle risorse del portale, questa combina tutte le versioni delle app che hanno lo stesso nome e lo stesso editore. Il numero di app nel riquadro **App degne di nota** riflette questa impostazione. Ad esempio, anziché un elenco di centinaia di istanze di Microsoft Edge, è presente una sola istanza per tutte le versioni. È possibile prendere decisioni una sola volta per tutte le versioni. Se è necessario prendere decisioni per versioni specifiche di un'app, questo comportamento è configurabile.

Per altre informazioni, vedere [Informazioni sugli asset - App](about-assets.md#apps).

## <a name="march-2020"></a>Marzo 2020

### <a name="support-for-multiple-hierarchies"></a>Supporto di più gerarchie

<!-- 4814075, 6079184 -->

È ora possibile connettere più gerarchie di Configuration Manager a un singolo tenant di Azure Active Directory con un unico ID commerciale per Desktop Analytics. Il portale categorizza i dispositivi da diverse gerarchie e migliora le esperienze per i progetti pilota globali e i piani di distribuzione.

- Quando si configura il progetto pilota globale, se si includono raccolte che contengono più del 20% dei dispositivi registrati totali, nel portale viene visualizzato un avviso.
- Quando si crea un piano di distribuzione, se si selezionano raccolte per più gerarchie, nel portale viene visualizzato un avviso.

> [!NOTE]
> Il supporto di più gerarchie richiede Configuration Manager versione 1910 o successiva.

Per altre informazioni, vedere gli articoli seguenti:

- [Progetto pilota globale](deploy-pilot.md#bkmk_GlobalPilot)
- [Come creare i piani di distribuzione](create-deployment-plans.md)

### <a name="identify-compatibility-safeguards"></a>Identificare le misure di sicurezza per la compatibilità

<!-- 5746559 -->

I dati di compatibilità di Windows classificano alcune app e driver con una *misura di sicurezza*, che può causare l'esito negativo o il rollback dell'aggiornamento a Windows 10. Desktop Analytics consente ora di identificare queste misure di sicurezza in anticipo, in modo da poter correggere la risorsa prima di distribuire l'aggiornamento. Per altre informazioni, vedere [Valutazione della compatibilità - Misure di sicurezza](compat-assessment.md#safeguards).

## <a name="january-2020"></a>Gennaio 2020

### <a name="additional-app-usage-detail"></a>Ulteriori dettagli sull'utilizzo delle app

<!-- 5533890 -->

Quando si seleziona un'app per visualizzare altre informazioni, nel riquadro dei dettagli sono ora incluse informazioni aggiuntive sull'utilizzo. È possibile usare questi dati per esaminare la gamma di installazioni per un'app, nonché i dispositivi in cui gli utenti usano regolarmente l'app. Per altre informazioni, vedere [Asset - App - Utilizzo](about-assets.md#usage).

### <a name="provide-feedback-on-desktop-analytics"></a>Inviare commenti e suggerimenti su Desktop Analytics

<!-- 5451636 -->

Per condividere i propri commenti e suggerimenti per Desktop Analytics, selezionare l'icona **Invia smile** nella parte superiore del portale sulla destra. Per altre informazioni, vedere [Condividere commenti e suggerimenti sul prodotto](get-support.md#bkmk_feedback).

## <a name="october-2019"></a>Ottobre 2019

### <a name="improvements-to-compatibility-recommendations"></a>Miglioramenti ai consigli per la compatibilità

<!-- 3594545 -->

Desktop Analytics offre ora maggiori dettagli quando rileva che l'aggiornamento di Windows causerà la rimozione completa o parziale di un'applicazione o un driver. Per altre informazioni, vedere [Valutazione della compatibilità](compat-assessment.md#asset-is-removed-during-upgrade).

### <a name="migrate-from-windows-analytics-to-existing-tenant"></a>Eseguire la migrazione da Windows Analytics al tenant esistente

<!-- 5202803 -->

È ora possibile migrare gli input da un'area di lavoro di Windows Analytics esistente dopo l'onboarding in Desktop Analytics.

## <a name="september-2019"></a>Settembre 2019

### <a name="migrate-inputs-from-windows-analytics"></a>Eseguire la migrazione degli input da Windows Analytics

<!-- 4252663 -->

Durante l'onboarding è ora possibile eseguire la migrazione degli input da un'area di lavoro di Windows Analytics esistente.

### <a name="offboard-from-desktop-analytics"></a>Eseguire l'offboarding da Desktop Analytics

<!-- 4972396 -->

Se si configura Desktop Analytics nell'ambiente ma si vuole smettere di usare il servizio, è ora possibile chiudere l'account. Se si cambia idea entro 90 giorni, è possibile riattivarlo. Per altre informazioni, vedere [Come chiudere l'account](account-close.md).

## <a name="august-2019"></a>Agosto 2019

### <a name="reset-your-account"></a>Reimpostare l'account

<!-- 3733897 -->

Se si configura Desktop Analytics nell'ambiente ma si vuole ricominciare con l'onboarding e la registrazione, è ora possibile reimpostare l'account. Per altre informazioni sul processo, vedere [Reimpostare l'account](account-reset.md).

### <a name="automatic-upgrade-decision-of-system-and-store-apps"></a>Decisione di aggiornamento automatico delle app di sistema e dello Store

<!-- 3587232 -->

Per facilitare l'annotazione di app importanti, alcuni tipi di app vengono contrassegnati automaticamente come *Non importante*. La decisione di aggiornamento del piano di distribuzione per queste app è contrassegnata anche con *Pronto*. Le app seguenti sono compatibili e continueranno a funzionare dopo l'aggiornamento di Windows:

- App di sistema e componenti pubblicati da Microsoft

- App gestite e aggiornate da Microsoft Store

Per altre informazioni, vedere [Decisione di aggiornamento automatico delle app di sistema e dello Store](about-assets.md#bkmk_plan-autoapp).

## <a name="whats-new-in-configuration-manager"></a>Novità di Configuration Manager

La documentazione di Desktop Analytics fa sempre riferimento alla funzionalità della versione più recente di Configuration Manager Current Branch. Per altre informazioni sulle modifiche più recenti di Configuration Manager, vedere gli articoli seguenti:

<!-- - [What's new in version 1910](../core/plan-design/changes/whats-new-in-version-1910.md#bkmk_da) -->

- [Novità della versione 1906](../core/plan-design/changes/whats-new-in-version-1906.md#bkmk_da)

## <a name="deprecated-features"></a>Funzionalità deprecate

Quando Microsoft prevede di rimuovere una funzionalità significativa del servizio Desktop Analytics, tale modifica viene annunciata in anticipo come funzionalità deprecata di Configuration Manager. Per altre informazioni, vedere [Funzionalità deprecate](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md#deprecated-features).
