---
title: Requisiti per la configurazione di Windows Autopilot
ms.reviewer: ''
manager: laurawi
description: Informazioni sui requisiti di configurazione per la distribuzione di Windows Autopilot.
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
ms.openlocfilehash: 0a5ab9e2de31dfe48c6f569fb03c22a7206369d0
ms.sourcegitcommit: cb12dd341792c0379bebe9fd5f844600638c668a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/15/2020
ms.locfileid: "88253322"
---
# <a name="windows-autopilot-configuration-requirements"></a>Requisiti per la configurazione di Windows Autopilot

**Si applica a: Windows 10**

Prima di poter usare Windows Autopilot, è necessario eseguire alcune attività di configurazione per supportare gli scenari comuni di Autopilot. 

- Configurare Azure Active Directory la registrazione automatica. Per Microsoft Intune, vedere [abilitare la registrazione automatica di Windows 10](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment) per informazioni dettagliate. Se si usa un servizio MDM diverso, contattare il fornitore per gli URL specifici o per la configurazione necessaria per tali servizi.
- Configurare Azure Active Directory personalizzazione personalizzata. Per visualizzare una pagina di accesso specifica dell'organizzazione, è necessario configurare Azure Active Directory con le immagini e il testo che si desidera visualizzare. Per altre informazioni, vedere [Guida introduttiva: aggiungere informazioni personalizzate distintive dell'azienda alla pagina di accesso in Azure ad](https://docs.microsoft.com/azure/active-directory/fundamentals/customize-branding). Gli elementi chiave per Autopilot includono il "logo quadrato", "testo della pagina di accesso" e il nome del tenant Azure Active Directory. Il nome del tenant viene configurato separatamente nelle proprietà del tenant Azure AD.
- Facoltativo: per eseguire automaticamente l'istruzione da Windows 10 Pro a Windows 10 Enterprise, abilitare l' [attivazione della sottoscrizione di Windows](https://docs.microsoft.com/windows/deployment/windows-10-enterprise-subscription-activation).

Scenari specifici avranno quindi requisiti aggiuntivi. In genere, esistono due attività specifiche:

- Registrazione di dispositivi. I dispositivi devono essere aggiunti a Windows Autopilot per supportare la maggior parte degli scenari di Windows Autopilot. Per ulteriori informazioni, vedere [aggiunta di dispositivi a Windows Autopilot](add-devices.md).
- Configurazione del profilo. Una volta aggiunti i dispositivi a Windows Autopilot, è necessario applicare un profilo di impostazioni a ogni dispositivo. Per informazioni dettagliate, vedere [configurare i profili di Autopilot](profiles.md) .  Microsoft Intune possibile automatizzare l'assegnazione del profilo. Per altre informazioni, vedere [creare un gruppo di dispositivi Autopilot](https://docs.microsoft.com/intune/enrollment-Autopilot#create-an-Autopilot-device-group) e [assegnare un profilo di distribuzione Autopilot a un gruppo di dispositivi](https://docs.microsoft.com/intune/enrollment-Autopilot#assign-an-Autopilot-deployment-profile-to-a-device-group).

Per ulteriori informazioni, vedere [scenari di Windows Autopilot](windows-Autopilot-scenarios.md).

Per una procedura dettagliata relativa ad alcuni di questi e passaggi correlati, vedere questo video:

</br>

<iframe width="560" height="315" src="https://www.youtube.com/embed/KYVptkpsOqs" frameborder="0" allow="accelerometer; autoplay; encrypted-media" gyroscope; picture-in-picture" allowfullscreen></iframe>


Non sono previsti requisiti hardware aggiuntivi per l'utilizzo di Windows 10 Autopilot, oltre ai [requisiti per l'esecuzione di Windows 10](https://www.microsoft.com/windows/windows-10-specifications).

**Passaggi successivi**

[Panoramica di Windows Autopilot](windows-autopilot.md)
