---
title: Profili VPN
titleSuffix: Configuration Manager
description: Di seguito viene illustrato come usare i profili VPN in Configuration Manager per distribuire impostazioni VPN agli utenti dell'organizzazione.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: c0f094f1-852e-4606-91db-97846d8f0772
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9463d857599e676da6267313df575c8881436f93
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706249"
---
# <a name="vpn-profiles-in-configuration-manager"></a>Profili VPN in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

<!--1283610-->
Per distribuire impostazioni VPN agli utenti dell'organizzazione, usare i profili VPN in Configuration Manager. La distribuzione di queste impostazioni consente di ridurre al minimo le operazioni che l'utente finale deve eseguire per connettersi alle risorse nella rete aziendale.  

Si supponga, ad esempio, di voler configurare tutti i dispositivi Windows 10 con le impostazioni necessarie per connettersi a una condivisione file nella rete interna. Creare un profilo VPN con le impostazioni necessarie per connettersi alla rete interna e quindi distribuire questo profilo a tutti gli utenti che dispongono di dispositivi che eseguono Windows 10. Tali utenti visualizzano la connessione VPN nell'elenco delle reti disponibili e possono connettersi con la massima facilità.

Quando si crea un profilo VPN, è possibile includere una vasta gamma di impostazioni di protezione. Queste impostazioni includono certificati per la convalida del server e l'autenticazione del client di cui viene eseguito il provisioning con i profili certificato di Configuration Manager. Per altre informazioni, vedere i [profili certificato](introduction-to-certificate-profiles.md).

> [!Note]
> Configuration Manager non abilita questa funzionalità facoltativa per impostazione predefinita. Pertanto sarà necessario abilitarla prima di poterla usare. Per altre informazioni, vedere [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options) (Abilitare le funzioni facoltative dagli aggiornamenti).<!--505213-->  

## <a name="supported-platforms"></a>Piattaforme supportate

Nella tabella seguente vengono descritti i profili VPN che possono essere configurati per diverse piattaforme per dispositivi.

|Tipo di connessione|Windows 8.1|Windows RT|Windows RT 8.1|Windows 10|
|---------------|-----------|----------|--------------|----------|
|**Pulse Secure**|Sì|No|Sì|Sì|
|**F5 Edge Client**|Sì|No|Sì|Sì|
|**Dell SonicWALL Mobile Connect**|Sì|No|Sì|Sì|
|**Check Point Mobile VPN**|Sì|No|Sì|Sì|
|**Microsoft SSL (SSTP)**|Sì|Sì|Sì|No|
|**Microsoft Automatico**|Sì|Sì|Sì|No|
|**IKEv2**|Sì|Sì|Sì|No|
|**PPTP**|Sì|Sì|Sì|No|
|**L2TP**|Sì|Sì|Sì|No|

## <a name="next-step"></a>Passaggio successivo

> [!div class="nextstepaction"]
> [Come creare profili VPN](create-vpn-profiles.md)

## <a name="see-also"></a>Vedere anche

- [Prerequisiti per i profili VPN](../plan-design/prerequisites-for-wifi-vpn-profiles.md)

- [Sicurezza e privacy per i profili VPN](../plan-design/security-and-privacy-for-wifi-vpn-profiles.md)
