---
title: Endpoint di rete per le distribuzioni in Cina - Microsoft Intune
titleSuffix: ''
description: Esaminare gli endpoint in Cina per Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/28/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: kerimh
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: fd52b34b70b71874a42486cbdc87cd3d7d2f9037
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88994243"
---
# <a name="china-endpoints-for-microsoft-intune"></a>Endpoint in Cina per Microsoft Intune

Questa pagina elenca gli endpoint in Cina necessari per le impostazioni proxy nelle distribuzioni di Intune.

Per gestire i dispositivi protetti da firewall e i server proxy, è necessario abilitare le comunicazioni per Intune.

- Il server proxy deve supportare sia **HTTP (80)** che **HTTPS (443)** perché i client di Intune usano entrambi i protocolli
- Per alcune attività, ad esempio il download di aggiornamenti software, Intune richiede l'accesso del server proxy non autenticato a manage.microsoft.com

È possibile modificare le impostazioni del server proxy nei singoli computer client. È anche possibile usare le impostazioni di Criteri di gruppo per modificare le impostazioni di tutti i computer client protetti da un server proxy specificato.

I dispositivi gestiti richiedono configurazioni che consentono a **Tutti gli utenti** di accedere ai servizi tramite i firewall.

Per altre informazioni sulla registrazione automatica di Windows 10 e sulla registrazione dei dispositivi per i clienti in Cina, vedere [Configurare la registrazione dei dispositivi Windows](../enrollment/windows-enroll.md#windows-10-auto-enrollment-and-device-registration).

Nelle tabelle seguenti sono elencati i servizi e le porte a cui accede il client di Intune:

|**Endpoint**|**Indirizzo IP**|
|---------------------|-----------|
|*.manage.microsoft.cn | 40.73.38.143<br>139.217.97.81<br>52.130.80.24<br>40.73.41.162<br>40.73.58.153<br>139.217.95.85 |


## <a name="intune-customer-designated-endpoints-in-china"></a>Endpoint designati per i clienti Intune in Cina
- Portale di Azure: https:\//portal.azure.cn/
- Microsoft 365: https:\//portal.partner.microsoftonline.cn/
- Portale aziendale Intune: https:\//portal.manage.microsoftonline.cn/
- Interfaccia di amministrazione di Microsoft Endpoint Manager: https:\//endpoint.microsoftonline.cn/


## <a name="partner-service-endpoints"></a>Endpoint di servizio di partner

Intune gestito da 21Vianet dipende dagli endpoint di servizio partner seguenti:
- Servizio Azure AD Sync: https:\//syncservice.partner.microsoftonline.cn/DirectoryService.svc
- Servizio token di sicurezza Evo: https:\//login.chinacloudapi.cn/
- Azure AD Graph: https:\//graph.chinacloudapi.us
- MS Graph: https:\//microsoftgraph.chinacloudapi.cn
- Regola di distribuzione automatica: https:\//enterpriseregistration.partner.microsoftonline.cn

[!INCLUDE [Intune notices](../includes/windows-push-notification-services.md)]

[!INCLUDE [Intune notices](../includes/apple-device-network-information.md)]

## <a name="next-steps"></a>Passaggi successivi
[Altre informazioni su Intune gestito da 21Vianet in Cina](china.md)

