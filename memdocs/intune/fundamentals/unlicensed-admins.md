---
title: Iscriversi o accedere a Microsoft Intune
description: Come iscriversi per ottenere una sottoscrizione di Microsoft Intune o eseguire l'accesso per iniziare a usare la sottoscrizione.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 01/02/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: ae30e03a03b4d690bdaa9e6a4c73da6ab15226f7
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/19/2020
ms.locfileid: "85095820"
---
# <a name="unlicensed-admins"></a>Amministratori senza licenza

È possibile concedere l'accesso all'interfaccia di amministrazione di Intune/Microsoft Endpoint Manager agli amministratori senza licenze di Intune.

1. Accedere a [Interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Amministrazione tenant** > **Licenze per amministratore**.
2. Scegliere **Consenti l'accesso agli amministratori senza licenza** > **Sì**.
    >[!WARNING]
    >Non è possibile annullare questa impostazione dopo aver fatto clic su **Sì**.

3. Da questo momento, gli utenti che effettuano l'accesso all'interfaccia di amministrazione di Microsoft Endpoint Manager non richiedono una licenza di Intune. L'ambito di accesso è definito dai ruoli assegnati.

Intune supporta fino a 350 amministratori senza licenza per ogni gruppo di sicurezza. Per gli amministratori che superano questo limite si verificherà un comportamento imprevedibile.




