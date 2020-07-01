---
title: Abilitare la condivisione dei dati
titleSuffix: Configuration Manager
description: Guida di riferimento per la condivisione dei dati di diagnostica con Desktop Analytics.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: be680198-4cea-4378-a686-d52f382ba483
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 7403dc26f5fe1789fcda6b3eddf30136a4cd6e68
ms.sourcegitcommit: c333fc6627f5577cde9d2fa8f59e642202a7027b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/16/2020
ms.locfileid: "84795652"
---
# <a name="enable-data-sharing-for-desktop-analytics"></a>Abilitare la condivisione dei dati per Desktop Analytics

Per registrare i dispositivi in Desktop Analytics, è necessario che i dispositivi inviino dati di diagnostica a Microsoft. Se l'ambiente usa un server proxy, usare queste informazioni per configurare il proxy.

## <a name="diagnostic-data-levels"></a>Livelli dei dati di diagnostica

![Diagramma dei livelli dei dati di diagnostica per Desktop Analytics](media/diagnostic-data-levels.png)

Quando si esegue l'integrazione di Configuration Manager con Desktop Analytics, Configuration Manager viene usato anche per gestire il livello dei dati di diagnostica nei dispositivi. Per un'esperienza ottimale, usare Configuration Manager.

> [!Important]  
> Nella maggior parte dei casi usare solo Configuration Manager per configurare queste impostazioni. Non applicare anche queste impostazioni negli oggetti criteri di gruppo del dominio. Per altre informazioni, vedere [Risoluzione dei conflitti](enroll-devices.md#conflict-resolution).

La funzionalità di base di Desktop Analytics funziona al [livello dei dati di diagnostica](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#diagnostic-data-levels) **Base**. Se non si configura il livello **Avanzata (con limitazioni)** in Configuration Manager, non si ottengono le funzionalità di Desktop Analytics seguenti:

- Uso dell'app
- [Informazioni dettagliate aggiuntive sull'app](compat-assessment.md#additional-insights)
- [Dati sullo stato della distribuzione](deploy-prod.md#address-deployment-alerts)
- [Dati di monitoraggio dell'integrità](health-status-monitoring.md)

Microsoft consiglia di abilitare il livello dei dati di diagnostica **Avanzata (con limitazioni)** con Desktop Analytics per ottimizzare i vantaggi offerti.

> [!Tip]
> L'impostazione **Avanzata (con limitazioni)** in Configuration Manager corrisponde all'impostazione dei criteri **Limita i dati di diagnostica avanzati al minimo richiesto da Windows Analytics** disponibili nei dispositivi che eseguono Windows 10 versione 1709 e successive.
>
> I dispositivi che eseguono Windows 10 versione 1703 e versioni precedenti, Windows 8.1 o Windows 7 non hanno questa impostazione dei criteri. Quando si configura l'impostazione **Avanzata (con limitazioni)** in Configuration Manager, questi dispositivi eseguono il fallback al livello **Base**.
>
> I dispositivi che eseguono Windows 10 versione 1709 hanno questa impostazione dei criteri. Tuttavia, quando si configura l'impostazione **Avanzata (con limitazioni)** in Configuration Manager, anche questi dispositivi eseguono il fallback al livello **Base**.

Per altre informazioni sui dati di diagnostica condivisi con Microsoft con **Avanzata (con limitazioni)** , vedere [Eventi e campi dei dati di diagnostica avanzati di Windows 10](https://docs.microsoft.com/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields).

> [!Important]
> Microsoft è impegnata a offrire strumenti e risorse che consentono di controllare la privacy. Di conseguenza, sebbene Desktop Analytics supporti i dispositivi Windows 8.1, Microsoft non raccoglie i dati di diagnostica di Windows dai dispositivi Windows 8.1 situati in paesi europei (SEE e Svizzera).

Per altre informazioni, vedere [Privacy di Desktop Analytics](privacy.md).

Gli articoli seguenti sono anche risorse valide per comprendere meglio i livelli dei dati di diagnostica di Windows:

- [Windows 10 e GDPR: informazioni per amministratori IT e decision maker](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance)  

- [Configurare i dati di diagnostica di Windows nell'organizzazione](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)  

> [!Note]  
> I client configurati per limitare i dati di diagnostica avanzati invieranno circa 2 MB di dati al cloud Microsoft nell'analisi completa iniziale. Il Delta giornaliero varia tra i 250 e i 400 kB al giorno.
>
> L'analisi Delta giornaliera viene eseguita alle 3:00 (ora locale del dispositivo). Alcuni eventi vengono inviati alla prima ora disponibile nel corso della giornata. Questi orari non sono configurabili.
>
> Per altre informazioni, vedere [Configure Windows diagnostic data in your organization](https://aka.ms/enterprisetelemetry) (Configurare i dati di diagnostica di Windows nell'organizzazione).  

## <a name="endpoints"></a>Endpoint

Per abilitare la condivisione dei dati, configurare il server proxy per consentire gli endpoint Internet seguenti.

> [!Important]  
> Per la privacy e l'integrità dei dati, Windows verifica la presenza di un certificato SSL Microsoft (associazione del certificato) durante la comunicazione con gli endpoint dei dati di diagnostica. L'intercettazione e l'ispezione SSL non sono possibili. Per usare Desktop Analytics, escludere questi endpoint dall'ispezione SSL.<!-- BUG 4647542 -->

A partire dalla versione 2002, se il server del sito di Configuration Manager non riesce a connettersi agli endpoint necessari per un servizio cloud, genera un messaggio di stato critico con ID 11488. Quando non è in grado di connettersi al servizio, lo stato del componente SMS_SERVICE_CONNECTOR diventa critico. Visualizzare lo stato dettagliato nel nodo [Stato componente](../core/servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus) della console di Configuration Manager.<!-- 5566763 -->

> [!NOTE]
> Per altre informazioni sugli intervalli di indirizzi IP Microsoft, vedere [Microsoft Public IP Space](https://www.microsoft.com/download/details.aspx?id=53602). Questi indirizzi vengono aggiornati regolarmente. Non esiste alcuna granularità in base al servizio, è possibile usare qualsiasi indirizzo IP compreso in questi intervalli.

### <a name="server-connectivity-endpoints"></a>Endpoint di connettività del server

Il punto di connessione del servizio deve comunicare con gli endpoint seguenti:

| Endpoint  | Funzione  |
|-----------|-----------|
| `https://aka.ms` | Usato per individuare il servizio |
| `https://graph.windows.net` | Usato per recuperare automaticamente impostazioni come CommercialId quando si connette la gerarchia a Desktop Analytics (nel ruolo del server di Configuration Manager). Per altre informazioni, vedere [Configurare il proxy per un server del sistema del sito](../core/plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |
| `https://*.manage.microsoft.com` | Usato per sincronizzare l'appartenenza alla raccolta di dispositivi, i piani di distribuzione e lo stato di idoneità dei dispositivi con Desktop Analytics (solo nel ruolo del server di Configuration Manager). Per altre informazioni, vedere [Configurare il proxy per un server del sistema del sito](../core/plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |

### <a name="user-experience-and-diagnostic-component-endpoints"></a>Esperienza utente ed endpoint componenti di diagnostica

I dispositivi client devono comunicare con gli endpoint seguenti:

| Endpoint  | Funzione  |
|-----------|-----------|
| `https://v10c.events.data.microsoft.com` | Esperienza utente connessa ed endpoint componente di diagnostica. Usato dai dispositivi che eseguono Windows 10 versione 1809 o successiva o versione 1803 con l'aggiornamento cumulativo 2018-09 o versione successiva installato. |
| `https://v10.events.data.microsoft.com` | Esperienza utente connessa ed endpoint componente di diagnostica. Usato dai dispositivi che eseguono Windows 10 versione 1803 _senza_ l'aggiornamento cumulativo 2018-09 installato. |
| `https://v10.vortex-win.data.microsoft.com` | Esperienza utente connessa ed endpoint componente di diagnostica. Usato dai dispositivi che eseguono Windows 10 versione 1709 o versioni precedenti. |
| `https://vortex-win.data.microsoft.com` | Esperienza utente connessa ed endpoint componente di diagnostica. Usato dai dispositivi che eseguono Windows 7 e Windows 8.1 |

### <a name="client-connectivity-endpoints"></a>Endpoint di connettività client

I dispositivi client devono comunicare con gli endpoint seguenti:

| Indice | Endpoint  | Funzione  |
|-------|-----------|-----------|
| 1 | `https://settings-win.data.microsoft.com` | Consente all'aggiornamento per la compatibilità di inviare i dati a Microsoft. |
| 2 | `http://adl.windows.com` | Consente all'aggiornamento per la compatibilità di ricevere i dati di compatibilità più recenti da Microsoft. |
| 3 | `https://watson.telemetry.microsoft.com` | [Segnalazione errori Windows](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Necessaria per monitorare lo stato di distribuzione in Windows 10 versione 1803 o versioni precedenti. |
| 4 | `https://umwatsonc.events.data.microsoft.com` | [Segnalazione errori Windows](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Necessaria per i report sull'integrità dei dispositivi in Windows 10 versione 1809 o successiva. |
| 5 | `https://ceuswatcab01.blob.core.windows.net` | [Segnalazione errori Windows](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Necessaria per monitorare lo stato di distribuzione in Windows 10 versione 1809 o successiva. |
| 6 | `https://ceuswatcab02.blob.core.windows.net` | [Segnalazione errori Windows](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Necessaria per monitorare lo stato di distribuzione in Windows 10 versione 1809 o successiva. |
| 7 | `https://eaus2watcab01.blob.core.windows.net` | [Segnalazione errori Windows](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Necessaria per monitorare lo stato di distribuzione in Windows 10 versione 1809 o successiva. |
| 8 | `https://eaus2watcab02.blob.core.windows.net` | [Segnalazione errori Windows](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Necessaria per monitorare lo stato di distribuzione in Windows 10 versione 1809 o successiva. |
| 9 | `https://weus2watcab01.blob.core.windows.net` | [Segnalazione errori Windows](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Necessaria per monitorare lo stato di distribuzione in Windows 10 versione 1809 o successiva. |
| 10 | `https://weus2watcab02.blob.core.windows.net` | [Segnalazione errori Windows](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Necessaria per monitorare lo stato di distribuzione in Windows 10 versione 1809 o successiva. |
| 11 | `https://kmwatsonc.events.data.microsoft.com` | [OCA (Online Crash Analysis)](https://docs.microsoft.com/windows/win32/dxtecharts/crash-dump-analysis). Necessaria per i report sull'integrità dei dispositivi in Windows 10 versione 1809 o successiva. |
| 12 | `https://oca.telemetry.microsoft.com`  | [OCA (Online Crash Analysis)](https://docs.microsoft.com/windows/win32/dxtecharts/crash-dump-analysis). Necessaria per monitorare lo stato di distribuzione in Windows 10 versione 1803 o versioni precedenti. |
| 13 | `https://login.live.com` | Necessaria per offrire un'identità del dispositivo più affidabile per Desktop Analytics. <br> <br>Per disabilitare l'accesso dell'account Microsoft dell'utente finale, usare le impostazioni dei criteri anziché bloccare l'endpoint. Per altre informazioni, vedere [Account Microsoft nell'organizzazione](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication). |
| 14 | `https://v20.events.data.microsoft.com` | Esperienza utente connessa ed endpoint componente di diagnostica. |

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
> L'approccio di autenticazione proxy dell'utente non è compatibile con l'uso di Microsoft Defender Advanced Threat Protection. Questo comportamento è dovuto al fatto che questa autenticazione si basa sulla chiave del Registro di sistema **DisableEnterpriseAuthProxy** impostata su `0`, mentre Microsoft Defender ATP richiede che sia impostata su `1`. Per altre informazioni, vedere [Configurare le impostazioni del proxy del computer e della connettività Internet in Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/configure-proxy-internet-windows-defender-advanced-threat-protection).

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
