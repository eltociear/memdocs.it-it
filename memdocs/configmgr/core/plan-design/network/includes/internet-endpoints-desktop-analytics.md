---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: include
ms.date: 08/11/2020
ms.openlocfilehash: 2ae953f6fb01f42c8140407c551ddeb3a9f39c70
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692681"
---
### <a name="server-connectivity-endpoints"></a>Endpoint di connettività del server

Il punto di connessione del servizio deve comunicare con gli endpoint seguenti:

| Endpoint  | Funzione  |
|-----------|-----------|
| `https://aka.ms` | Usato per individuare il servizio |
| `https://graph.windows.net` | Usato per recuperare automaticamente impostazioni come CommercialId quando si connette la gerarchia a Desktop Analytics (nel ruolo del server di Configuration Manager). Per altre informazioni, vedere [Configurare il proxy per un server del sistema del sito](../proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |
| `https://*.manage.microsoft.com` | Usato per sincronizzare l'appartenenza alla raccolta di dispositivi, i piani di distribuzione e lo stato di idoneità dei dispositivi con Desktop Analytics (solo nel ruolo del server di Configuration Manager). Per altre informazioni, vedere [Configurare il proxy per un server del sistema del sito](../proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |
| `https://dc.services.visualstudio.com` | Per i dati di diagnostica dal connettore servizio locale per ottenere informazioni dettagliate sull'integrità dei servizi connessi al cloud.<!--7541816--> |

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
| 3 | `https://watson.telemetry.microsoft.com` | [Segnalazione errori Windows](/windows/win32/wer/windows-error-reporting). Necessaria per monitorare lo stato di distribuzione in Windows 10 versione 1803 o versioni precedenti. |
| 4 | `https://umwatsonc.events.data.microsoft.com` | [Segnalazione errori Windows](/windows/win32/wer/windows-error-reporting). Necessaria per i report sull'integrità dei dispositivi in Windows 10 versione 1809 o successiva. |
| 5 | `https://ceuswatcab01.blob.core.windows.net` | [Segnalazione errori Windows](/windows/win32/wer/windows-error-reporting). Necessaria per monitorare lo stato di distribuzione in Windows 10 versione 1809 o successiva. |
| 6 | `https://ceuswatcab02.blob.core.windows.net` | [Segnalazione errori Windows](/windows/win32/wer/windows-error-reporting). Necessaria per monitorare lo stato di distribuzione in Windows 10 versione 1809 o successiva. |
| 7 | `https://eaus2watcab01.blob.core.windows.net` | [Segnalazione errori Windows](/windows/win32/wer/windows-error-reporting). Necessaria per monitorare lo stato di distribuzione in Windows 10 versione 1809 o successiva. |
| 8 | `https://eaus2watcab02.blob.core.windows.net` | [Segnalazione errori Windows](/windows/win32/wer/windows-error-reporting). Necessaria per monitorare lo stato di distribuzione in Windows 10 versione 1809 o successiva. |
| 9 | `https://weus2watcab01.blob.core.windows.net` | [Segnalazione errori Windows](/windows/win32/wer/windows-error-reporting). Necessaria per monitorare lo stato di distribuzione in Windows 10 versione 1809 o successiva. |
| 10 | `https://weus2watcab02.blob.core.windows.net` | [Segnalazione errori Windows](/windows/win32/wer/windows-error-reporting). Necessaria per monitorare lo stato di distribuzione in Windows 10 versione 1809 o successiva. |
| 11 | `https://kmwatsonc.events.data.microsoft.com` | [OCA (Online Crash Analysis)](/windows/win32/dxtecharts/crash-dump-analysis). Necessaria per i report sull'integrità dei dispositivi in Windows 10 versione 1809 o successiva. |
| 12 | `https://oca.telemetry.microsoft.com`  | [OCA (Online Crash Analysis)](/windows/win32/dxtecharts/crash-dump-analysis). Necessaria per monitorare lo stato di distribuzione in Windows 10 versione 1803 o versioni precedenti. |
| 13 | `https://login.live.com` | Necessaria per offrire un'identità del dispositivo più affidabile per Desktop Analytics. <br> <br>Per disabilitare l'accesso dell'account Microsoft dell'utente finale, usare le impostazioni dei criteri anziché bloccare l'endpoint. Per altre informazioni, vedere [Account Microsoft nell'organizzazione](/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication). |
| 14 | `https://v20.events.data.microsoft.com` | Esperienza utente connessa ed endpoint componente di diagnostica. |