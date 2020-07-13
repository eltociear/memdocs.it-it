---
title: Amministratori senza licenza in Microsoft Intune
description: Informazioni su come concedere agli amministratori senza licenza le autorizzazioni per accedere a Intune.
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
ms.openlocfilehash: c6dcd41377234bbb1b40e513f16c3393d763b17f
ms.sourcegitcommit: e713f8f4ba2ff453031c9dfc5bfd105ab5d00cd9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/08/2020
ms.locfileid: "86088191"
---
# <a name="unlicensed-admins"></a>Amministratori senza licenza

È possibile concedere l'accesso all'interfaccia di amministrazione di Intune/Microsoft Endpoint Manager agli amministratori senza licenze di Intune.

1. Accedere a [Interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Amministrazione tenant** > **Ruoli** > **Licenze per amministratore**.
2. Scegliere **Consenti l'accesso agli amministratori senza licenza** > **Sì**.
    >[!WARNING]
    >Non è possibile annullare questa impostazione dopo aver fatto clic su **Sì**.

3. Da questo momento, gli utenti che effettuano l'accesso all'interfaccia di amministrazione di Microsoft Endpoint Manager non richiedono una licenza di Intune. L'ambito di accesso è definito dai ruoli assegnati.

Intune supporta fino a 350 amministratori senza licenza per ogni gruppo di sicurezza e si applica solo ai membri diretti. Per gli amministratori che superano questo limite si verificherà un comportamento imprevedibile.




