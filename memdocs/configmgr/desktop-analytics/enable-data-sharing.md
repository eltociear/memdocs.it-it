---
title: Abilitare la condivisione dei dati
titleSuffix: Configuration Manager
description: Guida di riferimento per la condivisione dei dati di diagnostica con Desktop Analytics.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: be680198-4cea-4378-a686-d52f382ba483
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 999d8441e8c97f0a4b7ad4a92c8175300dcc4ead
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88696447"
---
# <a name="enable-data-sharing-for-desktop-analytics"></a>Abilitare la condivisione dei dati per Desktop Analytics

Per registrare i dispositivi in Desktop Analytics, è necessario che i dispositivi inviino dati di diagnostica a Microsoft. Se l'ambiente usa un server proxy, usare queste informazioni per configurare il proxy.

## <a name="diagnostic-data-levels"></a>Livelli dei dati di diagnostica

:::image type="content" source="media/diagnostic-data-levels.png" alt-text="Diagramma dei livelli dei dati di diagnostica per Desktop Analytics":::

Quando si esegue l'integrazione di Configuration Manager con Desktop Analytics, Configuration Manager viene usato anche per gestire il livello dei dati di diagnostica nei dispositivi. Per un'esperienza ottimale, usare Configuration Manager.

> [!IMPORTANT]
> Nella maggior parte dei casi usare solo Configuration Manager per configurare queste impostazioni. Non applicare anche queste impostazioni negli oggetti criteri di gruppo del dominio. Per altre informazioni, vedere [Risoluzione dei conflitti](enroll-devices.md#conflict-resolution).

Le funzionalità di base di Desktop Analytics funzionano al [livello dei dati di diagnostica](/windows/privacy/configure-windows-diagnostic-data-in-your-organization#diagnostic-data-levels) **Richiesto**. Se non si configura il livello **Facoltativo (limitato)** in Configuration Manager, non si otterranno le funzionalità seguenti di Desktop Analytics:

- Uso dell'app
- [Informazioni dettagliate aggiuntive sull'app](compat-assessment.md#additional-insights)
- [Dati sullo stato della distribuzione](deploy-prod.md#address-deployment-alerts)
- [Dati di monitoraggio dell'integrità](health-status-monitoring.md)

Per ottimizzare i vantaggi offerti, Microsoft consiglia di abilitare il livello dei dati di diagnostica **Facoltativo (limitato)** con Desktop Analytics.

> [!TIP]
> L'impostazione **Facoltativo (limitato)** in Configuration Manager corrisponde all'impostazione dei criteri **Limita i dati di diagnostica avanzati al minimo richiesto da Windows Analytics** disponibile nei dispositivi che eseguono Windows 10, versione 1709 e successive.
>
> I dispositivi che eseguono Windows 10 versione 1703 e versioni precedenti, Windows 8.1 o Windows 7 non hanno questa impostazione dei criteri. Quando si configura l'impostazione **Facoltativo (limitato)** in Configuration Manager, questi dispositivi eseguono il fallback al livello **Richiesto**.
>
> I dispositivi che eseguono Windows 10 versione 1709 hanno questa impostazione dei criteri. Tuttavia, quando si configura l'impostazione **Facoltativo (limitato)** in Configuration Manager, anche questi dispositivi eseguono il fallback al livello **Richiesto**.
>
> In Configuration Manager versione 2002 e precedenti le impostazioni hanno nomi diversi:<!-- 7363467 -->
>
> | Versione 2006 e successive | Versione 2002 e precedenti |
> |---------|---------|
> | Obbligatoria | Basic |
> | Facoltativo (limitato) | Avanzata (con limitazioni) |
> | N/D | Avanzato |
> | Facoltativo | Full |
>
> Se in precedenza sono stati configurati dispositivi al livello **Avanzato**, quando si esegue l'aggiornamento alla versione 2006 verranno ripristinati al livello **Facoltativo (limitato)** . Invieranno quindi meno dati a Microsoft. Questa modifica non dovrebbe avere alcun effetto sui dati visualizzati in Desktop Analytics.

Per altre informazioni sui dati di diagnostica condivisi con Microsoft con il livello **Facoltativo (limitato)** , vedere [Eventi e campi dei dati di diagnostica avanzati di Windows 10](/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields).

> [!IMPORTANT]
> Microsoft è impegnata a offrire strumenti e risorse che consentono di controllare la privacy. Di conseguenza, sebbene Desktop Analytics supporti i dispositivi Windows 8.1, Microsoft non raccoglie i dati di diagnostica di Windows dai dispositivi Windows 8.1 situati in paesi europei (SEE e Svizzera).

Per altre informazioni, vedere [Privacy di Desktop Analytics](privacy.md).

Gli articoli seguenti sono anche risorse valide per comprendere meglio i livelli dei dati di diagnostica di Windows:

- [Windows 10 e GDPR: informazioni per amministratori IT e decision maker](/windows/privacy/gdpr-it-guidance)  

- [Configurare i dati di diagnostica di Windows nell'organizzazione](/windows/privacy/configure-windows-diagnostic-data-in-your-organization)  

> [!NOTE]
> Durante l'analisi completa iniziale i client configurati per l'invio di dati di diagnostica al livello **Facoltativo (limitato)** invieranno al cloud Microsoft circa 2 MB di dati. Il Delta giornaliero varia tra i 250 e i 400 kB al giorno.
>
> L'analisi Delta giornaliera viene eseguita alle 3:00 (ora locale del dispositivo). Alcuni eventi vengono inviati alla prima ora disponibile nel corso della giornata. Questi orari non sono configurabili.
>
> Per altre informazioni, vedere [Configure Windows diagnostic data in your organization](https://aka.ms/enterprisetelemetry) (Configurare i dati di diagnostica di Windows nell'organizzazione).  

## <a name="endpoints"></a>Endpoint

Per abilitare la condivisione dei dati, configurare il server proxy per consentire gli endpoint Internet seguenti.

> [!IMPORTANT]
> Per la privacy e l'integrità dei dati, Windows verifica la presenza di un certificato SSL Microsoft (associazione del certificato) durante la comunicazione con gli endpoint dei dati di diagnostica. L'intercettazione e l'ispezione SSL non sono possibili. Per usare Desktop Analytics, escludere questi endpoint dall'ispezione SSL.<!-- BUG 4647542 -->

A partire dalla versione 2002, se il server del sito di Configuration Manager non riesce a connettersi agli endpoint necessari per un servizio cloud, genera un messaggio di stato critico con ID 11488. Quando non è in grado di connettersi al servizio, lo stato del componente SMS_SERVICE_CONNECTOR diventa critico. Visualizzare lo stato dettagliato nel nodo [Stato componente](../core/servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus) della console di Configuration Manager.<!-- 5566763 -->

> [!NOTE]
> Per altre informazioni sugli intervalli di indirizzi IP Microsoft, vedere [Microsoft Public IP Space](https://www.microsoft.com/download/details.aspx?id=53602). Questi indirizzi vengono aggiornati regolarmente. Non esiste alcuna granularità in base al servizio, è possibile usare qualsiasi indirizzo IP compreso in questi intervalli.

[!INCLUDE [Internet endpoints for Desktop Analytics](../core/plan-design/network/includes/internet-endpoints-desktop-analytics.md)]

## <a name="proxy-server-authentication"></a>Autenticazione del server proxy

Se l'organizzazione usa l'autenticazione del server proxy per l'accesso a Internet, verificare che non blocchi i dati di diagnostica a causa dell'autenticazione. Se il proxy non consente ai dispositivi di inviare questi dati, non verranno visualizzati in Desktop Analytics.

### <a name="bypass-recommended"></a>Ignorare (scelta consigliata)

Configurare i server proxy in modo che non richiedano l'autenticazione proxy per il traffico verso gli endpoint dei dati di diagnostica. Questa opzione è la soluzione più completa. Può essere usata per tutte le versioni di Windows 10.  

### <a name="user-proxy-authentication"></a>Autenticazione proxy dell'utente

Configurare i dispositivi per l'uso del contesto dell'utente connesso per l'autenticazione proxy. Questo metodo richiede le configurazioni seguenti:

- Dispositivi con aggiornamento qualitativo corrente per una versione supportata di Windows

- Configurare il proxy a livello di utente (proxy WinINET) in **Impostazioni proxy** nel gruppo Rete e Internet delle Impostazioni di Windows. È anche possibile usare il pannello di controllo Opzioni Internet legacy.

- Verificare che gli utenti abbiano l'autorizzazione proxy per raggiungere gli endpoint dei dati di diagnostica. Poiché questa opzione richiede che i dispositivi abbiano utenti console con autorizzazioni proxy, non è possibile usare questo metodo con dispositivi senza intestazioni.

> [!IMPORTANT]
> L'approccio di autenticazione proxy dell'utente non è compatibile con l'uso di Microsoft Defender Advanced Threat Protection. Questo comportamento è dovuto al fatto che questa autenticazione si basa sulla chiave del Registro di sistema **DisableEnterpriseAuthProxy** impostata su `0`, mentre Microsoft Defender ATP richiede che sia impostata su `1`. Per altre informazioni, vedere [Configurare le impostazioni del proxy del computer e della connettività Internet in Microsoft Defender ATP](/windows/security/threat-protection/windows-defender-atp/configure-proxy-internet-windows-defender-advanced-threat-protection).

### <a name="device-proxy-authentication"></a>Autenticazione proxy del dispositivo

Questo approccio supporta gli scenari seguenti:

- Dispositivi senza intestazioni, in cui nessun utente esegue l'accesso o gli utenti del dispositivo non hanno accesso a Internet

- Proxy autenticati che non usano l'autenticazione integrata di Windows

- Se si usa anche Microsoft Defender Advanced Threat Protection

Questo approccio è il più complesso poiché richiede le configurazioni seguenti:

- Assicurarsi che i dispositivi possano raggiungere il server proxy tramite WinHTTP nel contesto del sistema locale. Usare una delle opzioni seguenti per configurare questo comportamento:

  - `netsh winhttp set proxy` sulla riga di comando

  - Protocollo WPAD (Web Proxy Auto-Discovery)

  - Proxy trasparente

  - Configurare il proxy WinINET a livello di dispositivo usando la seguente impostazione dei criteri di gruppo: **Specificare le impostazioni proxy per computer (anziché per utente)** (ProxySettingsPerUser = `1`)

  - Connessione indirizzata o che usa NAT (Network Address Translation)

- Configurare i server proxy per consentire agli account del computer in Active Directory di accedere agli endpoint dei dati di diagnostica. Questa configurazione richiede che i server proxy supportino l'Autenticazione integrata di Windows.