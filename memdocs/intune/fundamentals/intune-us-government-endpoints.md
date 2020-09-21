---
title: Endpoint di rete per le distribuzioni US Government - Microsoft Intune
titleSuffix: ''
description: Esaminare gli endpoint US Government per Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/30/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 5f6682cb-5fcd-4018-b7f7-71768ad3152e
ms.reviewer: kerimh
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 032e6468ce326637e264b232cdd4e4d954ea70d8
ms.sourcegitcommit: dc2cca9eb70aef15037e8f7d18d671c513bfde85
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/14/2020
ms.locfileid: "90081808"
---
# <a name="us-government-endpoints-for-microsoft-intune"></a>Endpoint US Government per Microsoft Intune

Questa pagina elenca gli endpoint US Government, US Government Community (GCC) High e Department of Defense (DoD) necessari per le impostazioni proxy nelle distribuzioni di Intune.

Per gestire i dispositivi protetti da firewall e i server proxy, è necessario abilitare le comunicazioni per Intune.

- Il server proxy deve supportare sia **HTTP (80)** che **HTTPS (443)** perché i client di Intune usano entrambi i protocolli
- Per alcune attività, ad esempio il download di aggiornamenti software, Intune richiede l'accesso del server proxy non autenticato a manage.microsoft.com

È possibile modificare le impostazioni del server proxy nei singoli computer client. È anche possibile usare le impostazioni di Criteri di gruppo per modificare le impostazioni di tutti i computer client protetti da un server proxy specificato.

I dispositivi gestiti richiedono configurazioni che consentono a **Tutti gli utenti** di accedere ai servizi tramite i firewall.

Per altre informazioni sulla registrazione automatica di Windows 10 e sulla registrazione dei dispositivi per i clienti del governo degli Stati Uniti, vedere [Configurare la registrazione dei dispositivi Windows](../enrollment/windows-enroll.md#windows-10-auto-enrollment-and-device-registration).

Nelle tabelle seguenti sono elencati i servizi e le porte a cui accede il client di Intune:

|**Endpoint**|**Indirizzo IP**|
|---------------------|-----------|
|*.manage.microsoft.us | 52.243.26.209 <br> 52.247.173.11 <br> 52.227.183.12 <br>52.227.180.205 <br> 52.227.178.107 <br> 13.72.185.168 <br> 52.227.173.179 <br> 52.227.175.242 <br> 13.72.39.209 <br> 52.243.26.209 <br> 52.247.173.11 |
| enterpriseregistration.microsoftonline.us | 13.72.188.239 <br> 13.72.55.179 |

## <a name="us-government-customer-designated-endpoints"></a>Endpoint designati per i clienti delle distribuzioni US Government:
- Portale di Azure: https:\//portal.azure.us/ 
- Microsoft 365: https:\//portal.office365.us/ 
- Portale aziendale di Intune: https:\//portal.manage.microsoft.us/ 
- Interfaccia di amministrazione di Microsoft Endpoint Manager: https:\//endpoint.microsoft.us/

## <a name="partner-service-endpoints-that-intune-depends-on"></a>Endpoint dei servizi partner da cui dipende Intune:
- Servizio Azure AD Sync: https:\//syncservice.gov.us.microsoftonline.com/DirectoryService.svc
- Servizio token di sicurezza Evo: https:\//login.microsoftonline.us
- Proxy di directory: https:\//directoryproxy.microsoftazure.us/DirectoryProxy.svc
- Azure AD Graph: https:\//directory.microsoftazure.us and https:\//graph.microsoftazure.us
- MS Graph: https:\//graph.microsoft.us
- ADRS: https:\//enterpriseregistration.microsoftonline.us

[!INCLUDE [Intune notices](../includes/windows-push-notification-services.md)]

[!INCLUDE [Intune notices](../includes/apple-device-network-information.md)]

## <a name="next-steps"></a>Passaggi successivi
[Endpoint di rete per Microsoft Intune](intune-endpoints.md)

