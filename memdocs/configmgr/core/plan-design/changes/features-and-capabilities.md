---
title: Caratteristiche e funzionalità
titleSuffix: Configuration Manager
description: Informazioni sulle funzionalità di gestione principali di Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5d388399-07ca-431c-a9b2-56c69771aa87
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5cdd0a9497f07d80813aca5dc169c4d61944e85d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706399"
---
# <a name="features-and-capabilities-of-configuration-manager"></a>Caratteristiche e funzionalità di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Questo articolo include un riepilogo delle principali funzionalità di gestione di Configuration Manager. Poiché ogni funzionalità ha prerequisiti diversi, la modalità d'uso di ciascuna potrebbe influire sulla struttura e l'implementazione della gerarchia di Configuration Manager. Se, ad esempio, si vogliono distribuire gli aggiornamenti del software nei dispositivi della gerarchia, è necessario installare il ruolo del sistema del sito del punto di aggiornamento software.  

Per altre informazioni su come pianificare e installare Configuration Manager per supportare queste funzionalità di gestione nel proprio ambiente, vedere [Preparativi per Configuration Manager](../get-ready.md).  

## <a name="co-management"></a>Co-gestione

La co-gestione è uno dei modi principali per collegare la distribuzione di Configuration Manager esistente al cloud di Microsoft 365. Consente di gestire dispositivi Windows 10 contemporaneamente tramite Configuration Manager e Microsoft Intune. La co-gestione consente di collegare al cloud gli investimenti esistenti in Configuration Manager tramite l'aggiunta di nuove funzionalità, come l'accesso condizionale. Per altre informazioni, vedere [Informazioni sulla co-gestione](../../../comanage/overview.md).

## <a name="desktop-analytics"></a>Desktop Analytics

Desktop Analytics è un servizio basato sul cloud che si integra con Configuration Manager. Il servizio offre dati analitici e intelligenza per consentire agli utenti di prendere decisioni più informate sull'idoneità degli aggiornamenti dei client Windows. Combina i dati dell'organizzazione con i dati aggregati di milioni di dispositivi connessi a servizi cloud Microsoft. Per altre informazioni, vedere [Che cos'è Desktop Analytics?](../../../desktop-analytics/overview.md)

## <a name="cloud-attached-management"></a>Gestione collegata al cloud

Usare funzionalità come Cloud Management Gateway, i punti di distribuzione basati sul cloud e Azure Active Directory per gestire i client basati su Internet.

Per altre informazioni, vedere gli articoli seguenti:

- [Gestire i client su Internet](../../clients/manage/manage-clients-internet.md)
- [Pianificare per Azure AD](../security/plan-for-security.md#bkmk_planazuread)
- [Servizi di Azure](../../servers/deploy/configure/azure-services-wizard.md)

## <a name="real-time-management"></a>Gestione in tempo reale

Con CMPivot è possibile eseguire immediatamente query sui dispositivi online e quindi filtrare e raggruppare i dati per informazioni dettagliate più approfondite. È inoltre possibile usare la console di Configuration Manager per gestire e distribuire script di Windows PowerShell nei client. Per altre informazioni, vedere [CMPivot](../../servers/manage/cmpivot.md) e [Creare ed eseguire script di PowerShell](../../../apps/deploy-use/create-deploy-scripts.md).

## <a name="application-management"></a>Gestione delle applicazioni

È disponibile un set di strumenti e risorse che consentono di creare, gestire, distribuire e monitorare le applicazioni in una vasta gamma di dispositivi gestiti. Dalla console di Configuration Manager è anche possibile distribuire, aggiornare e gestire Office 365. Configuration Manager si integra con il Microsoft Store per le aziende e la formazione per distribuire app basate sul cloud. Per altre informazioni, vedere [Introduzione alla gestione delle applicazioni](../../../apps/understand/introduction-to-application-management.md).

## <a name="os-deployment"></a>Distribuzione del sistema operativo

È possibile distribuire un aggiornamento sul posto di Windows 10 oppure acquisire e distribuire immagini del sistema operativo. Per la distribuzione di immagini è possibile usare supporti di avvio, PXE o multicast. Per la ridistribuzione di dispositivi esistenti può inoltre essere utile Windows AutoPilot. Per altre informazioni, vedere [Introduzione alla distribuzione del sistema operativo](../../../osd/understand/introduction-to-operating-system-deployment.md).  

## <a name="software-updates"></a>Aggiornamenti software

È possibile gestire, distribuire e monitorare gli aggiornamenti software nell'organizzazione. Questa funzionalità di aggiornamento del software può essere integrata con Ottimizzazione recapito di Windows e altre tecnologie di peer caching per facilitare il controllo dell'utilizzo della rete. Per altre informazioni, vedere [Introduzione agli aggiornamenti software](../../../sum/understand/software-updates-introduction.md).  

## <a name="company-resource-access"></a>Accesso alle risorse aziendali

Gli utenti dell'organizzazione hanno la possibilità di accedere a dati e applicazioni da postazioni remote. Include Wi-Fi, VPN, posta elettronica e profili di certificato. Per altre informazioni, vedere [Proteggere dati e infrastruttura e del sito](../../../protect/understand/protect-data-and-site-infrastructure.md).

## <a name="compliance-settings"></a>Impostazioni di conformità

È possibile valutare, rilevare e correggere la conformità della configurazione dei dispositivi client nell'organizzazione. Inoltre, è possibile usare le impostazioni di conformità per configurare una gamma di funzionalità e impostazioni di sicurezza nei dispositivi gestiti. Per altre informazioni, vedere [Garantire la conformità dei dispositivi](../../../compliance/understand/ensure-device-compliance.md).  

## <a name="endpoint-protection"></a>Endpoint Protection

Sono disponibili funzionalità di sicurezza, antimalware e gestione di Windows Firewall per i computer dell'organizzazione. Questa area consente la gestione e l'integrazione con le funzionalità seguenti di Windows Defender:

- Windows Defender Antivirus
- Microsoft Defender Advanced Threat Protection
- Windows Defender Exploit Guard
- Windows Defender Application Guard
- Controllo delle applicazioni di Windows Defender
- Windows Defender Firewall

Per altre informazioni, vedere [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md).  

## <a name="inventory"></a>Argomento

Consente di identificare e monitorare gli asset.

### <a name="hardware-inventory"></a>Inventario hardware

Raccoglie informazioni dettagliate sull'hardware dei dispositivi nell'organizzazione. Per altre informazioni, vedere [Introduzione all'inventario hardware](../../clients/manage/inventory/introduction-to-hardware-inventory.md).  

### <a name="software-inventory"></a>Inventario software

Raccoglie e segnala le informazioni sui file archiviati sui computer client dell'organizzazione. Per altre informazioni, vedere [Introduzione all'inventario software](../../clients/manage/inventory/introduction-to-software-inventory.md).  

### <a name="asset-intelligence"></a>Asset Intelligence

Sono disponibili strumenti per raccogliere i dati di inventario e monitorare l'utilizzo delle licenze software nell'organizzazione. Per altre informazioni, vedere [Introduzione ad Asset Intelligence](../../clients/manage/asset-intelligence/introduction-to-asset-intelligence.md).  

## <a name="on-premises-mobile-device-management"></a>Gestione di dispositivi mobili locale

È possibile registrare e gestire i dispositivi usando l'infrastruttura locale di Configuration Manager con la funzionalità di gestione integrata nelle piattaforme dei dispositivi. La modalità di gestione tipica prevede l'uso di un client di Configuration Manager installato separatamente. Questa funzionalità supporta attualmente la gestione dei dispositivi Windows 10 Enterprise e Windows 10 Mobile. Per altre informazioni, vedere [Gestire i dispositivi mobili con l'infrastruttura locale](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

## <a name="power-management"></a>Risparmio energia

Sono disponibili funzionalità per gestire e monitorare il consumo di energia dei computer client nell'organizzazione. È possibile configurare combinazioni per il risparmio di energia e usare la tecnologia di riattivazione LAN per eseguire gli interventi di manutenzione al di fuori dell'orario di lavoro. Per altre informazioni, vedere [Introduzione alle raccolte](../../clients/manage/power/introduction-to-power-management.md).  

## <a name="remote-control"></a>Controllo remoto

Offre strumenti per amministrare in remoto i computer client dalla console di Configuration Manager. Per altre informazioni, vedere [Introduzione al controllo remoto](../../clients/manage/remote-control/introduction-to-remote-control.md).  

## <a name="reporting"></a>Reporting

È possibile usare le funzionalità avanzate per la creazione di report di SQL Server Reporting Services dalla console di Configuration Manager. Sono disponibili centinaia di report predefiniti. Per altre informazioni, vedere [Introduzione ai report](../../servers/manage/introduction-to-reporting.md).  

## <a name="software-metering"></a>Controllo del software

Sono disponibili strumenti per monitorare e raccogliere i dati di utilizzo del software dai client di Configuration Manager. È possibile usare questi dati per determinare se il software viene usato dopo l'installazione. Per altre informazioni, vedere [Monitorare l'utilizzo delle app con la misurazione del software](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  
