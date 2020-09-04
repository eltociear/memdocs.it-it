---
title: Requisiti per l'accesso a Internet
titleSuffix: Configuration Manager
description: Informazioni sugli endpoint Internet a cui consentire l'accesso per usufruire delle funzionalità complete di Configuration Manager.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
ms.assetid: b34fe701-5d05-42be-b965-e3dccc9363ca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a71fcd23977cc105a8d64f59edc45333cbd8c451
ms.sourcegitcommit: 42882de75c8a984ba35951b1165c424a7e0ba42e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2020
ms.locfileid: "89068236"
---
# <a name="internet-access-requirements"></a>Requisiti per l'accesso a Internet

Alcune caratteristiche di Configuration Manager hanno bisogno della connettività Internet per funzionare completamente. Se l'organizzazione limita le comunicazioni della rete con Internet tramite un firewall o un dispositivo proxy, assicurarsi di consentire l'accesso a questi endpoint.

<!-- SCCMDocs-pr #3403 -->

Configuration Manager usa i seguenti servizi di inoltro URL Microsoft nell'intero prodotto:

- `https://aka.ms`
- `https://go.microsoft.com`

Anche se non sono esplicitamente elencati nelle sezioni seguenti, è necessario consentire sempre l'accesso a questi endpoint.

## <a name="service-connection-point"></a><a name="bkmk_scp"></a> Punto di connessione del servizio

Queste configurazioni si applicano al computer che ospita il punto di connessione del servizio e gli eventuali firewall posti tra il computer e Internet. Entrambe devono consentire le comunicazioni tramite la porta in uscita **TCP 443** per HTTPS e la porta in uscita **TCP 80** per HTTP ai percorsi Internet seguenti.

Il punto di connessione del servizio supporta l'uso di un proxy Web (con o senza autenticazione) per accedere a questi percorsi. Per altre informazioni, vedere [Supporto dei server proxy](proxy-server-support.md).

Per altre informazioni sul punto di connessione del servizio, vedere [Informazioni sul punto di connessione del servizio](../../servers/deploy/configure/about-the-service-connection-point.md).

Altre funzionalità di Configuration Manager possono richiedere endpoint aggiuntivi dal punto di connessione del servizio. Per altre informazioni, vedere le altre sezioni in questo articolo.

> [!TIP]  
> Il punto di connessione del servizio usa il servizio Microsoft Intune quando si connette a `go.microsoft.com` o a `manage.microsoft.com`. Esiste un problema noto per cui il connettore Intune riscontra problemi di connettività se il certificato radice Baltimore CyberTrust non è installato, è scaduto o è danneggiato nel punto di connessione del servizio. Per altre informazioni, vedere [KB 3187516: Il punto di connessione del servizio non scarica gli aggiornamenti](https://support.microsoft.com/help/3187516).  

A partire dalla versione 2002, se il server del sito di Configuration Manager non riesce a connettersi agli endpoint necessari per un servizio cloud, genera un messaggio di stato critico con ID 11488. Quando non è in grado di connettersi al servizio, lo stato del componente SMS_SERVICE_CONNECTOR diventa critico. Visualizzare lo stato dettagliato nel nodo [Stato componente](../../servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus) della console di Configuration Manager.<!-- 5566763 -->

### <a name="updates-and-servicing"></a><a name="bkmk_scp-updates"></a> Aggiornamenti e manutenzione

Per altre informazioni su questa funzione, vedere [Aggiornamenti e manutenzione per Configuration Manager](../../servers/manage/updates.md).

> [!Tip]  
> Abilitare questi endpoint per la regola delle [informazioni dettagliate sulla gestione](../../servers/manage/management-insights.md), **connettere il sito al cloud Microsoft per gli aggiornamenti di Configuration Manager**.

- `*.akamaiedge.net`  

- `*.akamaitechnologies.com`  

- `*.manage.microsoft.com`  

- `go.microsoft.com`  

- `*.blob.core.windows.net`  

- `download.microsoft.com`  

- `download.windowsupdate.com`  

- `sccmconnected-a01.cloudapp.net`  

- `configmgrbits.azureedge.net`  

### <a name="windows-10-servicing"></a>Manutenzione di Windows 10

Per altre informazioni su questa funzione, vedere [Gestire Windows come servizio](../../../osd/deploy-use/manage-windows-as-a-service.md).

- `download.microsoft.com`  

- `https://go.microsoft.com/fwlink/?LinkID=619849`  

- `dl.delivery.mp.microsoft.com`  

### <a name="azure-services"></a>Servizi di Azure

Per altre informazioni su questa funzione, vedere [Configurare i servizi di Azure da usare con Configuration Manager](../../servers/deploy/configure/azure-services-wizard.md).

- `management.azure.com` (cloud pubblico di Azure)
- `management.usgovcloudapi.net` (cloud Azure US Government)

## <a name="co-management"></a>Co-gestione

Se si registrano dispositivi di Windows 10 in Microsoft Intune per la co-gestione, assicurarsi che questi dispositivi possano accedere agli endpoint richiesti da Intune. Per altre informazioni, vedere [Endpoint di rete per Microsoft Intune](/intune/intune-endpoints).

## <a name="microsoft-store-for-business"></a>Microsoft Store per le aziende

Se si integra Configuration Manager con [Microsoft Store per le aziende](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md), assicurarsi che il punto di connessione del servizio e i dispositivi di destinazione siano in grado di accedere al servizio cloud. Per altre informazioni, vedere [Configurazione del proxy per Microsoft Store per le aziende](/microsoft-store/prerequisites-microsoft-store-for-business#proxy-configuration).

## <a name="delivery-optimization"></a>Ottimizzazione recapito

Se si usa l'ottimizzazione recapito, i client devono comunicare con il servizio cloud: `*.do.dsp.mp.microsoft.com`

Anche i punti di distribuzione che supportano Microsoft Connected Cache richiedono questi endpoint.

Per altre informazioni, vedere gli articoli seguenti:

- [Domande frequenti sull'ottimizzazione recapito](/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions)
- [Concetti di base per la gestione dei contenuti in Configuration Manager](../hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization)
- [Microsoft Connected Cache in Configuration Manager](../hierarchy/microsoft-connected-cache.md)

## <a name="cloud-services"></a><a name="bkmk_cloud"></a> Servizi cloud

<!-- SCCMDocs-pr #3402 -->

Questa sezione illustra le funzionalità seguenti:

- Cloud Management Gateway
- Punto di distribuzione cloud
- Integrazione di Azure Active Directory (Azure AD)
- Individuazione basata su Azure AD

Per altre informazioni su Cloud Management Gateway, vedere [Pianificare il gateway di gestione cloud in Configuration Manager](../../clients/manage/cmg/plan-cloud-management-gateway.md).

Le sezioni seguenti elencano gli endpoint in base al ruolo. Alcuni endpoint fanno riferimento a un servizio tramite `<name>`, ovvero il nome del servizio cloud di CMG o CDP. Ad esempio, se CMG è `GraniteFalls.CloudApp.Net`, l'endpoint di archiviazione effettivo è `GraniteFalls.blob.core.windows.net`.<!-- SCCMDocs#2288 -->

### <a name="service-connection-point"></a>punto di connessione del servizio

Per la distribuzione dei servizi CMG/CDP, il punto di connessione del servizio deve avere accesso a:

- Gli endpoint di Azure specifici sono diversi per ogni ambiente a seconda della configurazione. Configuration Manager archivia gli endpoint nel database del sito. Eseguire una query nella tabella **AzureEnvironments** in SQL Server per un elenco degli endpoint di Azure.

- [Servizi di Azure](#azure-services)

- Per l'individuazione utente Azure AD:

  - Versione 1902 e successive: Endpoint di Microsoft Graph `https://graph.microsoft.com/`

  - Versione 1810 e precedenti: Endpoint di Azure AD Graph `https://graph.windows.net/`  

### <a name="cmg-connection-point"></a>Punto di connessione del gateway di gestione cloud

Il punto di connessione CMG deve avere accesso agli endpoint di servizio seguenti:

- Nome del servizio cloud (per CMG o CDP):
  - `<name>.cloudapp.net` (cloud pubblico di Azure)
  - `<name>.usgovcloudapp.net` (cloud Azure US Government)

- Endpoint di gestione dei servizi: `https://management.core.windows.net/`  

- Endpoint di archiviazione (per CMG o CDP abilitato per il contenuto):
  - `<name>.blob.core.windows.net` (cloud pubblico di Azure)
  - `<name>.blob.core.usgovcloudapi.net` (cloud Azure US Government)
<!--  and `<name>.table.core.windows.net` per DC, only used internally -->

Il sistema del sito del punto di connessione del gateway di gestione cloud supporta l'uso di un proxy Web. Per altre informazioni sulla configurazione di questo ruolo per un proxy, vedere le [informazioni di supporto per server proxy](proxy-server-support.md#configure-the-proxy-for-a-site-system-server). Il punto di connessione di Cloud Management Gateway deve connettersi solo agli endpoint del servizio Cloud Management Gateway. Non ha bisogno dell'accesso ad altri endpoint di Azure.

### <a name="configuration-manager-client"></a>Client di Configuration Manager

- Nome del servizio cloud (per CMG o CDP):
  - `<name>.cloudapp.net` (cloud pubblico di Azure)
  - `<name>.usgovcloudapp.net` (cloud Azure US Government)

- Endpoint di archiviazione (per CMG o CDP abilitato per il contenuto):
  - `<name>.blob.core.windows.net` (cloud pubblico di Azure)
  - `<name>.blob.core.usgovcloudapi.net` (cloud Azure US Government)

- Per il recupero dei token di Azure AD, l'endpoint di Azure AD:
  - `login.microsoftonline.com` (cloud pubblico di Azure)
  - `login.microsoftonline.us` (cloud Azure US Government)

### <a name="configuration-manager-console"></a>Console di Configuration Manager

- Per il recupero dei token di Azure AD, l'endpoint di Azure AD:

  - Cloud pubblico di Azure
    - `login.microsoftonline.com`
    - `aadcdn.msauth.net`<!-- MEMDocs#351 -->
    - `aadcdn.msftauth.net`

  - Cloud Azure US Government
    - `login.microsoftonline.us`

## <a name="software-updates"></a><a name="bkmk_sum"></a> Aggiornamenti software

Consentire al punto di aggiornamento software attivo di accedere agli endpoint seguenti in modo che WSUS e Aggiornamenti automatici possano comunicare con il servizio cloud Microsoft Update:  

- `http://windowsupdate.microsoft.com`  

- `http://*.windowsupdate.microsoft.com`  

- `https://*.windowsupdate.microsoft.com`  

- `http://*.update.microsoft.com`  

- `https://*.update.microsoft.com`  

- `http://*.windowsupdate.com`  

- `http://download.windowsupdate.com`  

- `http://download.microsoft.com`  

- `http://*.download.windowsupdate.com`  

- `http://ntservicepack.microsoft.com`  

Per altre informazioni sugli aggiornamenti software, vedere [Pianificare gli aggiornamenti software](../../../sum/plan-design/plan-for-software-updates.md).

### <a name="intranet-firewall"></a>Firewall Intranet

Potrebbe essere necessario aggiungere endpoint a un firewall posto tra due sistemi del sito nei casi seguenti:

- Se i siti secondari hanno un punto di aggiornamento software
- Se è presente un punto di aggiornamento software basato su Internet attivo remoto in un sito

#### <a name="software-update-point-on-the-child-site"></a>Punto di aggiornamento software nel sito secondario

- `http://<FQDN for software update point on child site>`  

- `https://<FQDN for software update point on child site>`  

- `http://<FQDN for software update point on parent site>`  

- `https://<FQDN for software update point on parent site>`  

## <a name="manage-microsoft-365-apps"></a>Gestire Microsoft 365 Apps

> [!NOTE]
> A partire dal 21 aprile 2020, Office 365 ProPlus viene rinominato come **App di Microsoft 365 per grandi imprese**. Per altre informazioni, vedere [Modifica del nome di Office 365 ProPlus](/deployoffice/name-change). È comunque possibile che vengano ancora visualizzati riferimenti al nome precedente nella console di Configuration Manager e nella documentazione di supporto mentre la console viene aggiornata.

Se si usa Configuration Manager per distribuire e aggiornare App di Microsoft 365 per grandi imprese, abilitare gli endpoint seguenti:

<!-- SCCMDocs#929 -->

- `officecdn.microsoft.com` per sincronizzare il punto di aggiornamento software per gli aggiornamenti del client App di Microsoft 365 per grandi imprese

- `config.office.com` per creare configurazioni personalizzate per le distribuzioni di App di Microsoft 365 per grandi imprese

- `contentstorage.osi.office.net` per supportare la valutazione dell'idoneità dei componenti aggiuntivi per Office<!-- MEMDocs#410 -->

## <a name="configuration-manager-console"></a>Console di Configuration Manager

I computer con la console di Configuration Manager richiedono l'accesso agli endpoint Internet seguenti per funzionalità specifiche:

### <a name="in-console-feedback"></a>Feedback nella console

- `http://petrol.office.microsoft.com`

Per altre informazioni su questa funzionalità, vedere [Commenti e suggerimenti sul prodotto](../../understand/find-help.md#product-feedback).

### <a name="community-workspace"></a>Area di lavoro della community

#### <a name="documentation-node"></a>Nodo di documentazione

Per altre informazioni su questo nodo della console, vedere [Uso della console di Configuration Manager](../../servers/manage/admin-console.md).

- `https://aka.ms`

- `https://raw.githubusercontent.com`

#### <a name="community-hub"></a>Hub della community

Per altre informazioni su questa funzionalità, vedere l'[hub della community](../../servers/manage/community-hub.md).

- `https://github.com`

- `https://communityhub.microsoft.com`

## <a name="desktop-analytics"></a>Desktop Analytics

Per altre informazioni, vedere [Abilitare la condivisione dei dati](../../../desktop-analytics/enable-data-sharing.md#endpoints).

[!INCLUDE [Internet endpoints for Desktop Analytics](includes/internet-endpoints-desktop-analytics.md)]

## <a name="tenant-attach"></a>Collegamento di tenant

Per altre informazioni, vedere [Abilita Collegamento di tenant](../../../tenant-attach/device-sync-actions.md).

[!INCLUDE [Internet endpoints for tenant attach](includes/internet-endpoints-tenant-attach.md)]

## <a name="endpoint-analytics"></a>Analisi degli endpoint

Per altre informazioni, vedere [Configurazione dell'analisi degli endpoint](../../../../analytics/troubleshoot.md#bkmk_endpoints).

[!INCLUDE [Internet endpoints for Endpoint analytics](includes/internet-endpoints-endpoint-analytics.md)]

## <a name="asset-intelligence"></a>Asset intelligence

<!-- memdocs#470 -->
Se si usa [Asset Intelligence](../../clients/manage/asset-intelligence/introduction-to-asset-intelligence.md), consentire l'accesso agli endpoint seguenti per permettere la sincronizzazione del servizio:

- `https://sc.microsoft.com`
- `https://ssu2.manage.microsoft.com`

## <a name="microsoft-public-ip-addresses"></a>Indirizzi IP pubblici Microsoft

Per altre informazioni sugli intervalli di indirizzi IP Microsoft, vedere [Microsoft Public IP Space](https://www.microsoft.com/download/details.aspx?id=53602). Questi indirizzi vengono aggiornati regolarmente. Non esiste alcuna granularità in base al servizio, è possibile usare qualsiasi indirizzo IP compreso in questi intervalli.

## <a name="see-also"></a>Vedere anche

- [Porte usate in Configuration Manager](../hierarchy/ports.md)

- [Supporto dei server proxy in Configuration Manager](proxy-server-support.md)