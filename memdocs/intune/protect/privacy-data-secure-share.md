---
title: Sicurezza dei dati e condivisione in Intune
titleSuffix: Microsoft Intune
description: Informazioni sulla modalità di protezione e condivisione dei dati personali in Intune.
keywords: privacy, dati
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/18/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 68921fd6-5f50-456c-a3af-83d7bc4b134b
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: fba72c89676d8974f5e7f9aac25d3365b69f61c7
ms.sourcegitcommit: 75d6ea42a0f473dc5020ae7fcb667c9bdde7bd97
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/01/2020
ms.locfileid: "89286255"
---
# <a name="data-security-and-sharing-in-intune"></a>Sicurezza dei dati e condivisione in Intune


## <a name="data-security"></a>Sicurezza dei dati

Microsoft Intune è un componente fondamentale dell'offerta di servizi cloud Microsoft Enterprise Mobility + Security. Per supportare le [strategia di governance dei dati](https://www.microsoft.com/en-us/TrustCenter/Security/default.aspx), tutti i servizi cloud Microsoft sono sviluppati con le metodologie [Microsoft Privacy](https://www.microsoft.com/en-us/trustcenter/privacy) e [Microsoft Security](https://www.microsoft.com/en-us/trustcenter/security/).  

Microsoft Intune segue le stesse misure tecniche e organizzative adottate dai team dei servizi Microsoft Azure per la protezione da processi di violazione di dati.

Per altre informazioni, vedere [Service Trust Portal](https://www.microsoft.com/en-us/TrustCenter/stp).

### <a name="data-breach-reporting"></a>Segnalazione di violazioni dei dati

Quando viene identificato un evento imprevisto per la sicurezza segnalabile al cliente, i clienti ricevono una notifica. Questo processo include la collaborazione con il team di Microsoft 365 per la notifica delle violazioni per qualsiasi cliente di Microsoft 365 che usa Intune.

## <a name="data-sharing"></a>Condivisione dei dati

Quando gli amministratori del tenant attivano determinate funzionalità (ad esempio, il programma DEP di Apple), Microsoft Intune consente di ottenere il consenso dell'amministratore per la condivisione dei dati con le terze parti appropriate. In questi casi, Intune potrebbe condividere i dati personali con:

- Terze parti che operano come agenti di Microsoft.
- Terze parti che non operano come agenti di Microsoft, ma solo quando gli amministratori del tenant concedono in modo esplicito l'autorizzazione di Intune a tale scopo.

Tutte le terze parti che operano come agenti Microsoft sono incluse nell'[elenco dei subappaltatori per Online Services](https://aka.ms/Online_Serv_Subcontractor_List).

La condivisione dei dati con tali entità avviene allo scopo di agevolare il supporto tecnico e l'assistenza ai clienti, la manutenzione dei servizi e altre operazioni.

I dati personali di Intune mantenuti in un servizio di terze parti sono regolamentati dal contratto di un tenant con la terza parte. Tale contratto concede inoltre a Intune l'autorizzazione per trasmettere dati al servizio di terze parti.  

Per informazioni sui dati condivisi con alcune terze parti, vedere gli articoli seguenti:
- [Dati inviati da Intune ad Apple](data-intune-sends-to-apple.md)
- [Dati inviati da Intune a Google](data-intune-sends-to-google.md)
- [Dati inviati da Apple a Intune](data-apple-sends-to-intune.md)
- [Dati inviati da Google a Intune](data-google-sends-to-intune.md)
- [Dati inviati da Jamf Pro a Intune](data-jamf-sends-to-intune.md)

### <a name="microsoft-endpoint-configuration-manager-data-sharing"></a>Condivisione dei dati con Microsoft Endpoint Configuration Manager

Microsoft Intune non condivide i dati con Configuration Manager. Configuration Manager è un prodotto locale distribuito, gestito e amministrato direttamente dal cliente. I dati di diagnostica e utilizzo raccolti da Configuration Manager vengono usati esclusivamente per migliorare l'esperienza, la qualità e la sicurezza di installazione delle versioni future.

Per altre informazioni, vedere [Dati di diagnostica e di utilizzo per Configuration Manager](/configmgr/core/plan-design/diagnostics/diagnostics-and-usage-data). 


## <a name="next-steps"></a>Passaggi successivi

Scoprire come [visualizzare e correggere](privacy-data-view-correct.md) i dati personali in Intune.