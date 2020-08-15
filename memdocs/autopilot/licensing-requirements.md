---
title: Requisiti per le licenze di Windows Autopilot
ms.reviewer: ''
manager: laurawi
description: Informazioni sui requisiti di licenza per la distribuzione di Windows Autopilot.
keywords: MDM, installazione, Windows, Windows 10, OOBE, gestione, distribuzione, Autopilot, ZTD, zero-touch, partner, msfb, Intune
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.custom:
- CI 116757
- CSSTroubleshooting
ms.openlocfilehash: 911ff589acb5d215931dd4a2e72a05bff760a533
ms.sourcegitcommit: cb12dd341792c0379bebe9fd5f844600638c668a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/15/2020
ms.locfileid: "88253343"
---
# <a name="windows-autopilot-licensing-requirements"></a>Requisiti per le licenze di Windows Autopilot

**Si applica a: Windows 10**

Windows Autopilot dipende da funzionalità specifiche disponibili in Windows 10 e Azure Active Directory. Richiede anche un servizio MDM, ad esempio Microsoft Intune. Queste funzionalità possono essere ottenute tramite varie edizioni e programmi di sottoscrizione:

Per fornire Azure Active Directory necessarie (registrazione MDM automatica e funzionalità di personalizzazione dell'azienda) e funzionalità MDM, è necessaria una delle sottoscrizioni seguenti:
- [Sottoscrizione di Microsoft 365 Business Premium](https://www.microsoft.com/microsoft-365/business)
- [Microsoft 365 sottoscrizione F1 o F3](https://www.microsoft.com/microsoft-365/enterprise/firstline)
- [Sottoscrizione di Microsoft 365 Academic a1, a3 o a5](https://www.microsoft.com/education/buy-license/microsoft365/default.aspx)
- [Microsoft 365 Enterprise sottoscrizione E3 o E5](https://www.microsoft.com/microsoft-365/enterprise), che include tutte le funzionalità di Windows 10, Office 365 e em + S (Azure ad e Intune).
- [Enterprise Mobility + Security sottoscrizione E3 o E5](https://www.microsoft.com/cloud-platform/enterprise-mobility-security), che include tutte le funzionalità Azure ad e Intune necessarie.
- [Intune per Education sottoscrizione](https://docs.microsoft.com/intune-education/what-is-intune-for-education), che include tutte le funzionalità Azure ad e Intune necessarie.
- [Azure Active Directory Premium P1 o P2](https://azure.microsoft.com/services/active-directory/) e la [sottoscrizione Microsoft Intune](https://www.microsoft.com/cloud-platform/microsoft-intune) (o un servizio MDM alternativo).

> [!NOTE]
> Anche quando si usano Microsoft 365 sottoscrizioni, è comunque necessario [assegnare le licenze di Intune agli utenti](https://docs.microsoft.com/intune/fundamentals/licenses-assign).

Inoltre, è consigliabile anche quanto segue (ma non obbligatorio):
- [Microsoft 365 app per Enterprise](https://www.microsoft.com/p/office-365-proplus/CFQ7TTC0K8R0), che possono essere distribuite facilmente tramite Intune (o altri servizi MDM).
- [Attivazione della sottoscrizione di Windows](https://docs.microsoft.com/windows/deployment/windows-10-enterprise-subscription-activation), per eseguire automaticamente il passaggio dei dispositivi da Windows 10 Pro a Windows 10 Enterprise.

**Passaggi successivi**

[Requisiti per la configurazione di Windows Autopilot](configuration-requirements.md)

