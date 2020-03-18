---
title: Accesso condizionale con Microsoft Intune
titleSuffix: Microsoft Intune
description: Informazioni su come definire le condizioni che utenti, dispositivi e app devono soddisfare per accedere alle risorse aziendali in Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/06/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: a1973f38-ea55-43eb-a151-505fb34a8afb
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0e2b8c8d715a7b60dd6111a6495b8f470cd92778
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79352670"
---
# <a name="learn-about-conditional-access-and-intune"></a>Informazioni sull'accesso condizionale e su Intune

Con l'accesso condizionale è possibile controllare i dispositivi e le app che possono connettersi alla posta elettronica e alle risorse aziendali. 

Enterprise Mobility + Security (EMS) non è un prodotto autonomo. È una soluzione che fa parte di tutti i servizi e i prodotti di EMS. L'accesso condizionale consente un controllo di accesso granulare per la sicurezza dei dati aziendali, oltre a offrire agli utenti un'esperienza che assicura loro di operare in modo ottimale da qualsiasi dispositivo e luogo.

È possibile definire condizioni che limitano l'accesso ai dati aziendali in base alla posizione, al dispositivo, allo stato dell'utente e alla sensibilità dell'applicazione.

> [!NOTE]
> Le funzionalità di accesso condizionale sono estese anche ai [servizi Office 365](https://docs.microsoft.com/office365/enterprise/office-365-client-support-conditional-access).

![Diagramma dell'accesso condizionale](./media/conditional-access/ca-diagram-1.png)

## <a name="use-conditional-access-with-intune"></a>Usare l'accesso condizionale con Intune

L'accesso condizionale è una funzionalità di Azure Active Directory inclusa con una licenza di Azure Active Directory Premium. Intune contribuisce a migliorare questa funzionalità aggiungendo la conformità dei dispositivi mobili e la gestione delle app per dispositivi mobili alla soluzione. 

![Intune e accesso condizionale quando si usa EMS](./media/conditional-access/intune-with-ca-1.png)

Modi per usare l'accesso condizionale con Intune:

- **Accesso condizionale basato sul dispositivo**

  - Accesso condizionale per Exchange locale

  - Accesso condizionale basato sul controllo di accesso alla rete

  - Accesso condizionale basato sul rischio di dispositivo

  - Accesso condizionale per i PC Windows

    - Dispositivi di proprietà dell'azienda

    - Bring Your Own Device (BYOD)

- **Accesso condizionale basato sulle app**

## <a name="next-steps"></a>Passaggi successivi

[Modi comuni per usare l'accesso condizionale con Intune](conditional-access-intune-common-ways-use.md)
