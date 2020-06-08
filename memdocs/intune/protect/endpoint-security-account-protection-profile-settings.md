---
title: Impostazioni dei criteri di protezione account per la sicurezza degli endpoint di Intune | Microsoft Docs
description: Impostazioni dei criteri di protezione account per la sicurezza degli endpoint di Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/17/2020
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
ms.openlocfilehash: f4e67c434af9eb7f88c3e7d3997ef7c7d829c860
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431995"
---
# <a name="account-protection-policy-settings-for-endpoint-security-in-intune"></a>Impostazione dei criteri di protezione account per la sicurezza degli endpoint di Intune

Visualizzare le impostazioni che è possibile configurare nei profili per i criteri di *protezione account* nel nodo Sicurezza degli endpoint di Intune come parte dei [criteri di sicurezza degli endpoint](../protect/endpoint-security-policy.md).

Piattaforme e profili supportati:

- **Windows 10 e versioni successive**:
  - Profilo: **protezione account** *(anteprima)*


## <a name="account-protection-profile"></a>Profilo di protezione account

### <a name="account-protection"></a>Protezione account

- **Blocca Windows Hello for Business**

  Windows Hello for Business è un metodo alternativo per l'accesso a Windows che prevede la sostituzione di password, smart card e smart card virtuali.
  - **Non configurato** (*impostazione predefinita*): i dispositivi effettuano il provisioning di Windows Hello for Business.
  - **Disattivato**: i dispositivi effettuano il provisioning di Windows Hello for Business.
  - **Attivato**: i dispositivi non effettuano il provisioning di Windows Hello for Business per qualsiasi utente.
  
- **Abilita l'uso delle chiavi di sicurezza per l'accesso**

  Abilita la chiave di sicurezza di Windows Hello come credenziale di accesso per tutti i PC nel tenant.
  - **Non configurato** (*impostazione predefinita*)
  - **Sì**

- **Attiva Credential Guard**  
  [CSP: []DeviceGuard](https://go.microsoft.com/fwlink/?linkid=872424)

  Credential Guard usa Windows Hypervisor per garantire protezione. Credential Guard richiede il supporto hardware per l’avvio protetto e le protezioni DMA. Questa impostazione ha esito positivo solo nei dispositivi che soddisfano i requisiti hardware.
  - **Non configurato** (*impostazione predefinita*): disabilita l'uso di Credential Guard, che è l'impostazione predefinita di Windows.
  - **Abilita con blocco UEFI**: abilita Credential Guard e non ne consente la disabilitazione remota, perché la configurazione di UEFI permanente deve essere cancellata manualmente.
  - **Abilita senza blocco UEFI** - Abilita Credential Guard e ne consente la disattivazione senza accesso fisico al computer.

## <a name="next-steps"></a>Passaggi successivi

[Criteri di sicurezza degli endpoint per la protezione account ](../protect/endpoint-security-account-protection-policy.md)
