---
title: Bloccare le app che non usano l'autenticazione moderna in Intune
titleSuffix: Microsoft Intune
description: Informazioni sulle applicazioni e l'autenticazione moderna (ADAL) in Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/06/2020
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.topic: conceptual
ms.technology: ''
ms.assetid: 73db3070-d033-40fb-a8f1-58b9d198021e
ms.reviewer: chrisgre
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 662b0ab94004bf54d793d9a913157c53f36d0dcc
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989764"
---
# <a name="block-apps-that-dont-use-modern-authentication-adal"></a>Bloccare le app che non usano l'autenticazione moderna (ADAL)

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

L'accesso condizionale basato sulle app con i criteri di protezione delle app si basa su applicazioni che usano l'[autenticazione moderna](https://support.office.com/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a) che è un'implementazione di OAuth2. L'autenticazione moderna è usata dalle applicazioni desktop e per dispositivi mobili di Office più recenti. Tuttavia, esistono app di terze parti e app di Office meno recenti che usano altri metodi di autenticazione, ad esempio l'autenticazione di base e l'autenticazione basata su moduli.

## <a name="block-access-to-apps"></a>Bloccare l'accesso alle app

Per bloccare l'accesso alle app che non usano l'autenticazione moderna, usare i criteri di protezione delle app di Intune per implementare l'accesso condizionale. Per altre informazioni, vedere [Accesso condizionale basato su app con Intune](app-based-conditional-access-intune.md).

## <a name="additional-information"></a>Informazioni aggiuntive

Per altre informazioni sull'accesso condizionale di Azure AD, vedere gli argomenti seguenti:
- [Che cos'è l'accesso condizionale in Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)
- [Funzionamento dell'accesso condizionale basato su app](app-based-conditional-access-intune.md#how-app-based-conditional-access-works)
- [Configurare SharePoint Online ed Exchange Online per l'accesso condizionale di Azure Active Directory](https://docs.microsoft.com/azure/active-directory/conditional-access/conditional-access-for-exo-and-spo)

## <a name="next-steps"></a>Passaggi successivi

- [Accesso condizionale basato su app con Intune](app-based-conditional-access-intune.md)
