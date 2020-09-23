---
title: Endpoint di rete per Microsoft Intune
titleSuffix: ''
description: Esaminare gli endpoint per Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 09/08/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: b8d9aef2-8757-4e22-9b24-a0833d27304c
ms.reviewer: kerimh
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: fbf157c50ce3ffd2e090c8e0c0310c40b9e26202
ms.sourcegitcommit: 6e488937039e8437866d55f2f23e5944a4b35a35
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2020
ms.locfileid: "91022352"
---
# <a name="network-endpoints-for-microsoft-intune"></a>Endpoint di rete per Microsoft Intune  

Questa pagina elenca gli indirizzi IP e le impostazioni delle porte necessarie per le impostazioni proxy nelle distribuzioni di Intune.

Essendo un servizio basato solo sul cloud, Intune non ha bisogno di un'infrastruttura locale come server o gateway.

## <a name="access-for-managed-devices"></a>Accesso per i dispositivi gestiti  

Per gestire i dispositivi protetti da firewall e i server proxy, è necessario abilitare le comunicazioni per Intune.

> [!NOTE]
> Le informazioni in questa sezione si applicano anche a Connettore di certificati di Microsoft Intune. Il connettore ha gli stessi requisiti di rete dei dispositivi gestiti

- Il server proxy deve supportare sia **HTTP (80)** che **HTTPS (443)** perché i client Intune usano entrambi i protocolli. Windows Information Protection usa la porta 444.
- Per alcune attività, ad esempio il download di aggiornamenti software per l'agente del computer classico, Intune richiede l'accesso del server proxy non autenticato a manage.microsoft.com

È possibile modificare le impostazioni del server proxy nei singoli computer client. È anche possibile usare le impostazioni di Criteri di gruppo per modificare le impostazioni di tutti i computer client protetti da un server proxy specificato.


<!--
> [!NOTE] If Windows 8.1 devices haven't cached proxy server credentials, enrollment might fail because the request doesn't prompt for credentials. Enrollment fails without warning as the request wait for a connection. If users might experience this issue, instruct them to open their browser settings and save proxy server settings to enable a connection.   -->

I dispositivi gestiti richiedono configurazioni che consentono a **Tutti gli utenti** di accedere ai servizi tramite i firewall.


Nelle tabelle seguenti sono elencati i servizi e le porte a cui accede il client di Intune:

|Domains    |Indirizzo IP      |
|-----------|----------------|
| login.microsoftonline.com <br> *.officeconfig.msocdn.com <br> config.office.com <br> graph.windows.net <br> enterpriseregistration.windows.net | Altre informazioni sono disponibili in [URL e intervalli di indirizzi IP per Office 365](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2) |
|portal.manage.microsoft.com<br> m.manage.microsoft.com |52.175.12.209<br>20.188.107.228<br>52.138.193.149<br>51.144.161.187<br>52.160.70.20<br>52.168.54.64 <br>13.72.226.202<br>52.189.220.232|
| sts.manage.microsoft.com | 13.93.223.241 <br>52.170.32.182 <br>52.164.224.159 <br>52.174.178.4 <br>13.75.122.143 <br>52.163.120.84<br>13.73.112.122<br>52.237.192.112|
|Manage.microsoft.com <br>i.manage.microsoft.com <br>r.manage.microsoft.com <br>a.manage.microsoft.com <br>p.manage.microsoft.com <br>EnterpriseEnrollment.manage.microsoft.com <br>EnterpriseEnrollment-s.manage.microsoft.com |40.83.123.72<br>13.76.177.110<br>52.169.9.87<br>52.174.26.23<br>104.40.82.191<br>13.82.96.212<br>52.147.8.239<br>40.115.69.185|
|portal.fei.msua01.manage.microsoft.com<br>m.fei.msua01.manage.microsoft.com<br>portal.fei.msua02.manage.microsoft.com<br>m.fei.msua02.manage.microsoft.com<br>portal.fei.msua04.manage.microsoft.com<br>m.fei.msua04.manage.microsoft.com<br>portal.fei.msua05.manage.microsoft.com<br>m.fei.msua05.manage.microsoft.com<br>portal.fei.amsua0502.manage.microsoft.com<br>m.fei.amsua0502.manage.microsoft.com<br>portal.fei.msua06.manage.microsoft.com<br>m.fei.msua06.manage.microsoft.com<br>portal.fei.amsua0602.manage.microsoft.com<br>m.fei.amsua0602.manage.microsoft.com<br>fei.amsua0202.manage.microsoft.com<br>portal.fei.amsua0202.manage.microsoft.com<br>m.fei.amsua0202.manage.microsoft.com<br>portal.fei.amsua0402.manage.microsoft.com<br>m.fei.amsua0402.manage.microsoft.com<br>portal.fei.amsua0801.manage.microsoft.com<br>portal.fei.msua08.manage.microsoft.com<br>m.fei.msua08.manage.microsoft.com<br>m.fei.amsua0801.manage.microsoft.com|52.160.70.20<br>52.168.54.64 |
|portal.fei.msub01.manage.microsoft.com<br>m.fei.msub01.manage.microsoft.com<br>portal.fei.amsub0102.manage.microsoft.com<br>m.fei.amsub0102.manage.microsoft.com<br>fei.msub02.manage.microsoft.com<br>portal.fei.msub02.manage.microsoft.com<br>m.fei.msub02.manage.microsoft.com<br>portal.fei.msub03.manage.microsoft.com<br>m.fei.msub03.manage.microsoft.com<br>portal.fei.msub05.manage.microsoft.com<br>m.fei.msub05.manage.microsoft.com<br>portal.fei.amsub0202.manage.microsoft.com<br>m.fei.amsub0202.manage.microsoft.com<br>portal.fei.amsub0302.manage.microsoft.com<br>m.fei.amsub0302.manage.microsoft.com<br>portal.fei.amsub0502.manage.microsoft.com<br>m.fei.amsub0502.manage.microsoft.com<br>portal.fei.amsub0601.manage.microsoft.com<br>m.fei.amsub0601.manage.microsoft.com|52.138.193.149<br>51.144.161.187|
|portal.fei.msuc01.manage.microsoft.com <br>m.fei.msuc01.manage.microsoft.com<br>portal.fei.msuc02.manage.microsoft.com <br>m.fei.msuc02.manage.microsoft.com<br>portal.fei.msuc03.manage.microsoft.com <br>m.fei.msuc03.manage.microsoft.com<br>portal.fei.msuc05.manage.microsoft.com <br>m.fei.msuc05.manage.microsoft.com|52.175.12.209<br>20.188.107.228|
|portal.fei.amsud0101.manage.microsoft.com<br>m.fei.amsud0101.manage.microsoft.com|13.72.226.202|
|fef.msua02.manage.microsoft.com|52.177.194.236|
|fef.msua04.manage.microsoft.com|23.96.112.28|
|fef.msua06.manage.microsoft.com|13.78.185.97|
|fef.msuc03.manage.microsoft.com|23.101.0.100|
|fef.amsua0502.manage.microsoft.com|13.85.68.142|
|fef.amsua0602.manage.microsoft.com|52.161.28.64|
|Admin.manage.microsoft.com|52.224.221.227<br>52.161.162.117<br>52.178.44.195<br>52.138.206.56<br>52.230.21.208<br>13.75.125.10|
|wip.mam.manage.microsoft.com|52.187.76.84<br>13.76.5.121<br>52.165.160.237<br>40.86.82.163<br>52.233.168.142<br>168.63.101.57<br>52.187.196.98<br>52.237.196.51|
|mam.manage.microsoft.com|104.40.69.125<br>13.90.192.78<br>40.85.174.177<br>40.85.77.31<br>137.116.229.43<br>52.163.215.232<br>52.174.102.180<br>52.187.196.173<br>52.156.162.48|
|*.manage.microsoft.com|40.82.248.224/28<br>20.189.105.0/24<br>20.37.153.0/24<br>20.37.192.128/25<br>20.38.81.0/24<br>20.41.1.0/24<br>20.42.1.0/24<br>20.42.130.0/24<br>20.42.224.128/25<br>20.43.129.0/24<br>40.119.8.128/25<br>40.74.25.0/24<br>40.82.249.128/25<br>40.80.184.128/25<br>52.150.137.0/25|


## <a name="network-requirements-for-powershell-scripts-and-win32-apps"></a>Requisiti di rete per gli script di PowerShell e le app Win32  

Se si usa Intune per distribuire script di PowerShell o app Win32, è necessario anche concedere l'accesso agli endpoint in cui si trova attualmente il tenant.

|ASU | Nome archiviazione | Rete CDN |
| --- | --- |--- |
|AMSUA0601<br>AMSUA0602<br>AMSUA0101<br>AMSUA0102<br>AMSUA0201<br>AMSUA0202<br>AMSUA0401<br>AMSUA0402<br>AMSUA0501<br>AMSUA0502<br>AMSUA0701<br>AMSUA0702 | naprodimedatapri<br>naprodimedatasec<br>naprodimedatahotfix | naprodimedatapri.azureedge.net<br>naprodimedatasec.azureedge.net<br>naprodimedatahotfix.azureedge.net |
| AMSUB0101<br>AMSUB0102<br>AMSUB0201<br>AMSUB0202<br>AMSUB0301<br>AMSUB0302<br>AMSUB0501<br>AMSUB0502 | euprodimedatapri<br>euprodimedatasec<br>euprodimedatahotfix | euprodimedatapri.azureedge.net<br>euprodimedatasec.azureedge.net<br>euprodimedatahotfix.azureedge.net |
| AMSUC0101<br>AMSUC0201<br>AMSUC0301<br>AMSUC0501<br>AMSUD0101| approdimedatapri<br>approdimedatasec<br>approdimedatahotifx | approdimedatapri.azureedge.net<br>approdimedatasec.azureedge.net<br>approdimedatahotfix.azureedge.net |

## <a name="windows-push-notification-services-wns"></a>Servizi notifica push Windows (WNS)  

Per i dispositivi Windows gestiti da Intune che vengono gestiti tramite Gestione dispositivi mobili (MDM), le azioni dei dispositivi e altre attività immediate richiedono l'uso dei servizi notifica push Windows. Per altre informazioni, vedere [Consentire il traffico di notifica Windows attraverso i firewall dell'organizzazione](/windows/uwp/design/shell/tiles-and-notifications/firewall-allowlist-config).  

## <a name="delivery-optimization-port-requirements"></a>Requisiti delle porte per Ottimizzazione recapito  

### <a name="port-requirements"></a>Requisiti delle porte  

Per il traffico peer-to-peer, Ottimizzazione recapito usa la porta 7680 per TCP/IP o 3544 per l'attraversamento NAT (facoltativamente Teredo). Per la comunicazione tra client e servizio, usa il protocollo HTTP o HTTPS sulla porta 80 o 443.

### <a name="proxy-requirements"></a>Requisiti del proxy  

Per usare Ottimizzazione recapito, è necessario consentire le richieste di intervalli di byte. Per altre informazioni, vedere [Requisiti proxy per Windows Update](/windows/deployment/update/windows-update-troubleshooting).

### <a name="firewall-requirements"></a>Requisiti del firewall  

Consentire i nomi host seguenti nel firewall per supportare Ottimizzazione recapito.
Per la comunicazione tra client e il servizio cloud Ottimizzazione recapito:
- \*.do.dsp.mp.microsoft.com

Per i metadati di Ottimizzazione recapito:
- \*.dl.delivery.mp.microsoft.com
- \*.emdl.ws.microsoft.com

## <a name="apple-device-network-information"></a>Informazioni di rete dei dispositivi Apple  

|Utilizzato per|Nome host (indirizzo IP/subnet)|Protocollo|Porta|
|-----|--------|------|-------|
|Recupero e visualizzazione di contenuto dai server Apple|itunes.apple.com<br>\*.itunes.apple.com<br>\*.mzstatic.com<br>\*.phobos.apple.com<br> \*.phobos.itunes-apple.com.akadns.net |    HTTP    |      80      |
|Comunicazioni con i server del servizio APN|#-courier.push.apple.com<br>'#' è un numero casuale compreso tra 0 e 50.|    TCP     |  5223 e 443  |
|Diverse funzionalità, tra cui acceso al World Wide Web, iTunes Store, App Store macOS, iCloud, messaggistica e così via. |phobos.apple.com<br>ocsp.apple.com<br>ax.itunes.apple.com<br>ax.itunes.apple.com.edgesuite.net| HTTP/HTTPS |  80 o 443   |

Per altre informazioni, vedere gli articoli di Apple [Porte TCP e UDP usate dai prodotti software Apple](https://support.apple.com/HT202944), [Informazioni sui processi in background e le connessioni host ai server macOS, iOS/iPadOS e iTunes](https://support.apple.com/HT201999) e [Se i tuoi client macOS e iOS/iPadOS non ricevono le notifiche push di Apple](https://support.apple.com/HT203609).  

## <a name="android-port-information"></a>Informazioni sulle porte Android

A seconda di come si sceglie di gestire i dispositivi Android, potrebbe essere necessario aprire le porte Google Android Enterprise e/o la notifica push Android. Per altre informazioni sui metodi di gestione di Android supportati, vedere la [documentazione relativa alla registrazione di Android](../enrollment/android-enroll.md). 

> [!NOTE]
> Dato che Google Mobile Services non è disponibile in Cina, i dispositivi in Cina gestiti da Intune non possono usare le funzionalità che richiedono Google Mobile Services. Queste funzionalità comprendono: funzionalità Google Play Protect come l'attestazione del dispositivo SafetyNet, la gestione delle app da Google Play Store, le funzionalità Android Enterprise (vedere questa [documentazione di Google](https://support.google.com/work/android/answer/6270910)). Inoltre, l'app Portale aziendale Intune per Android usa Google Play Services per comunicare con il servizio Microsoft Intune. Poiché Google Play Services non è disponibile in Cina, per il completamento di alcune attività possono essere necessarie fino a 8 ore. Per altre informazioni, vedere questo [articolo](../apps/manage-without-gms.md#limitations-of-intune-device-administrator-management-when-gms-is-unavailable).

### <a name="google-android-enterprise"></a>Google Android Enterprise 

Google fornisce la documentazione relativa alle porte di rete e ai nomi host di destinazione richiesti nella guida [Android Enterprise Bluebook](https://static.googleusercontent.com/media/www.android.com/en//static/2016/pdfs/enterprise/Android-Enterprise-Migration-Bluebook_2019.pdf), nella sezione **Firewall** del documento. 

### <a name="android-push-notification"></a>Notifica push Android

Intune si avvale di Google Firebase Cloud Messaging (FCM) per la notifica push per attivare le azioni e le sincronizzazioni dei dispositivi. Questa operazione è necessaria sia per l'amministratore di dispositivi Android che per Android Enterprise. Per informazioni sui requisiti di rete FCM, vedere [FCM ports and your firewall](https://firebase.google.com/docs/cloud-messaging/concept-options#messaging-ports-and-your-firewall) (Porte FCM e firewall) di Google.

## <a name="endpoint-analytics"></a>Analisi degli endpoint

Per altre informazioni sugli endpoint necessari per l'analisi degli endpoint, vedere [Configurazione del proxy di analisi degli endpoint](../../analytics/troubleshoot.md#bkmk_endpoints).