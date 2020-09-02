---
title: Gestire le impostazioni di protezione account di attacco con i criteri di sicurezza degli endpoint in Microsoft Intune | Microsoft Docs
description: Configurare e distribuire criteri per i dispositivi gestiti con le impostazioni di criteri di protezione account per la sicurezza degli endpoint in Microsoft Endpoint Manager.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: f08282fe6bd8675474415290d50c0b07b4e1fc25
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915059"
---
# <a name="account-protection-policy-for-endpoint-security-in-intune"></a>Criteri di protezione account per la sicurezza degli endpoint di Intune

Usare i criteri di sicurezza degli endpoint di Intune per protezione account per proteggere l'identità e gli account degli utenti. I criteri di protezione account sono incentrati sulle impostazioni per Windows Hello e Credential Guard, che fanno parte della gestione di identità e accessi di Windows.

- *Windows Hello for business* sostituisce le password con l'autenticazione a due fattori avanzata su computer e dispositivi mobili.
- *Credential Guard* consente di proteggere le credenziali e i segreti usati con i dispositivi.

Per altre informazioni, vedere [Gestione di identità e accessi](/windows/security/identity-protection/) nella documentazione relativa alla gestione delle identità e degli accessi di Windows.

I criteri di sicurezza degli endpoint per protezione account sono disponibili in *Gestione* nel nodo **Endpoint security** (Sicurezza degli endpoint) dell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

Visualizzare le [impostazioni per i profili di protezione account](../protect/endpoint-security-asr-profile-settings.md).

## <a name="prerequisites-for-account-protection-profiles"></a>Prerequisiti per i profili di protezione account

- Windows 10 o versioni successive

## <a name="account-protection-profiles"></a>Profili di protezione account

*I profili di protezione account sono disponibili in anteprima*.

**Profili di Windows 10**:

- **Protezione account** *(anteprima)* : le impostazioni per i criteri di protezione account consentono di proteggere le credenziali utente.

## <a name="next-steps"></a>Passaggi successivi

[Configurare i criteri di sicurezza degli endpoint](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)