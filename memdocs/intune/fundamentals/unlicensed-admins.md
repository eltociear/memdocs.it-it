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
ms.openlocfilehash: a5f479dcad0c293c547edec24f0f835a4fc987e1
ms.sourcegitcommit: cba06c182646cb6dceef304b35230bf728d5133e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/15/2020
ms.locfileid: "90574831"
---
# <a name="unlicensed-admins"></a>Amministratori senza licenza

> [!Important]
> Questa opzione rimuove solo il requisito della licenza per gli amministratori per accedere a Microsoft Endpoint Manager. L'uso di altre caratteristiche o servizi come Azure Active Directory Premium può comunque richiedere una licenza per l'amministratore.

È possibile concedere l'accesso all'interfaccia di amministrazione di Intune/Microsoft Endpoint Manager agli amministratori senza licenze di Intune.

1. Accedere a [Interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Amministrazione tenant** > **Ruoli** > **Licenze per amministratore**.
2. Scegliere **Consenti l'accesso agli amministratori senza licenza** > **Sì**.
    >[!WARNING]
    >Non è possibile annullare questa impostazione dopo aver fatto clic su **Sì**.

3. Da questo momento, gli utenti che effettuano l'accesso all'interfaccia di amministrazione di Microsoft Endpoint Manager non richiedono una licenza di Intune. L'ambito di accesso è definito dai ruoli assegnati.

Intune supporta fino a 350 amministratori senza licenza per ogni gruppo di sicurezza e si applica solo ai membri diretti. Per gli amministratori che superano questo limite si verificherà un comportamento imprevedibile.




