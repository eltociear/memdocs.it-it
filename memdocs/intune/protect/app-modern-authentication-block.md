---
title: Bloccare le app che non usano l'autenticazione moderna in Intune
titleSuffix: Microsoft Intune
description: Informazioni sulle applicazioni e l'autenticazione moderna (ADAL) in Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/22/2020
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.topic: conceptual
ms.technology: ''
ms.assetid: 73db3070-d033-40fb-a8f1-58b9d198021e
ms.reviewer: chrisgre
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure, has-adal-ref
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4703288faac219b40fae08c6551425d6f0d5e4f3
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/26/2020
ms.locfileid: "88909415"
---
# <a name="block-apps-that-dont-use-modern-authentication-adal"></a>Bloccare le app che non usano l'autenticazione moderna (ADAL)

> [!NOTE]
> Azure Active Directory (Azure AD) Authentication Library (ADAL) e l'API Graph di Azure AD saranno deprecate. Per altre informazioni, vedere [Aggiornare le applicazioni per usare Microsoft Authentication Library (MSAL) e l'API Microsoft Graph](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/update-your-applications-to-use-microsoft-authentication-library/ba-p/1257363).

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

L'accesso condizionale basato sulle app con i criteri di protezione delle app si basa su applicazioni che usano l'[autenticazione moderna](https://support.office.com/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a) che è un'implementazione di OAuth2. L'autenticazione moderna è usata dalle applicazioni desktop e per dispositivi mobili di Office più recenti. Tuttavia, esistono app di terze parti e app di Office meno recenti che usano altri metodi di autenticazione, ad esempio l'autenticazione di base e l'autenticazione basata su moduli.

## <a name="block-access-to-apps"></a>Bloccare l'accesso alle app

Per bloccare l'accesso alle app che non usano l'autenticazione moderna, usare i criteri di protezione delle app di Intune per implementare l'accesso condizionale. Per altre informazioni, vedere [Accesso condizionale basato su app con Intune](app-based-conditional-access-intune.md).

## <a name="additional-information"></a>Informazioni aggiuntive

Per altre informazioni sull'accesso condizionale di Azure AD, vedere gli argomenti seguenti:
- [Che cos'è l'accesso condizionale in Azure Active Directory?](/azure/active-directory/conditional-access/overview)
- [Funzionamento dell'accesso condizionale basato su app](app-based-conditional-access-intune.md#how-app-based-conditional-access-works)
- [Configurare SharePoint Online ed Exchange Online per l'accesso condizionale di Azure Active Directory](/azure/active-directory/conditional-access/conditional-access-for-exo-and-spo)

## <a name="next-steps"></a>Passaggi successivi

- [Accesso condizionale basato su app con Intune](app-based-conditional-access-intune.md)