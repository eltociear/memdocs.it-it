---
title: Impostazioni dei criteri antivirus in Windows 10 per l'esperienza di Sicurezza di Windows per Intune | Microsoft Docs
description: Impostazioni dei criteri antivirus per la sicurezza degli Endpoint per l'app Sicurezza di Windows in Microsoft Intune
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
ms.openlocfilehash: 78cc6182cf8682935ecaa6c319e30ee8261fc2fb
ms.sourcegitcommit: 0b30c8eb2f5ec2d60661a5e6055fdca8705b4e36
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2020
ms.locfileid: "84455260"
---
# <a name="settings-for-the-windows-security-experience-profile-in-microsoft-intune"></a>Impostazioni per il profilo dell'esperienza di Sicurezza di Windows in Microsoft Intune

Consente di visualizzare le impostazioni dei criteri antivirus che è possibile configurare per il profilo dell'**esperienza di Sicurezza di Windows**per Windows 10 in Microsoft Intune come parte di un [ criterio di sicurezza degli endpoint](../protect/endpoint-security-policy.md).

**Sicurezza di Windows**

- **Consenti a Protezione antimanomissione di impedire la disabilitazione di Microsoft Defender**  
  [Impedire modifiche alle impostazioni di sicurezza con Protezione antimanomissione](https://go.microsoft.com/fwlink/?linkid=2066083)

  - **Non configurato** (*impostazione predefinita*): quando in un client è presente lo stato *Attiva* o *Disattiva*, la distribuzione *Non configurato* non ha alcun effetto sull'impostazione. 
  - **Attiva**: attiva la restrizione per Protezione antimanomissione. Per modificare lo stato da attivato o disattivato, distribuire l'impostazione opposta in modo che abbia effetto.
  - **Disattiva**: disattiva la restrizione per Protezione antimanomissione. Per modificare lo stato da attivato o disattivato, distribuire l'impostazione opposta in modo che abbia effetto.

- **Nascondi l'area Protezione da virus e minacce nell'app Sicurezza di Windows**  
  CSP: [DisableVirusUI](https://go.microsoft.com/fwlink/?linkid=873662)

  - **Non configurato** (*impostazione predefinita*): l'impostazione torna al valore predefinito del client, in base al quale l'accesso utente e le notifiche sono consentite.
  - **Sì**: l'area Protezione da virus e minacce nell'app Sicurezza di Windows è nascosta agli utenti finali. Le notifiche relative a virus e protezione dalle minacce sono eliminate.

  - **Nascondi l'area Ripristino dati ransomware nell'app Sicurezza di Windows**  
    CSP: [HideRansomwareDataRecovery](https://go.microsoft.com/fwlink/?linkid=873664)

  - **Non configurato** (*impostazione predefinita*): l'impostazione torna al valore predefinito del client, in base al quale l'accesso utente e le notifiche sono consentite.
  - **Sì**: l'area Ripristino dati ransomware nell'app Sicurezza di Windows è nascosta agli utenti finali. Le notifiche relative ai ransomware sono eliminate.

- **Nascondi l'area Protezione account nell'app Sicurezza di Windows**  
  CSP: [DisableAccountProtectionUI](https://go.microsoft.com/fwlink/?linkid=873666)

  - **Non configurato** (*impostazione predefinita*): l'impostazione torna al valore predefinito del client, in base al quale l'accesso utente e le notifiche sono consentite.
  - **Sì**: l'area Protezione account nell'app Sicurezza di Windows è nascosta agli utenti finali. Le notifiche relative alla protezione account sono eliminate.

- **Nascondi l'area Protezione firewall e della rete nell'app Sicurezza di Windows**  
  CSP: [DisableNetworkUI](https://go.microsoft.com/fwlink/?linkid=873668)

  - **Non configurato** (*impostazione predefinita*): l'impostazione torna al valore predefinito del client, in base al quale l'accesso utente e le notifiche sono consentite.
  - **Sì**: l'area Protezione firewall e della rete nell'app Sicurezza di Windows sono nascoste agli utenti finali. Le notifiche relative al firewall e alla protezione della rete sono eliminate.

- **Nascondi l'area Controllo delle app e del browser nell'app Sicurezza di Windows**  
  CSP: [DisableAppBrowserUI](https://go.microsoft.com/fwlink/?linkid=873669)

  - **Non configurato** (*impostazione predefinita*): l'impostazione torna al valore predefinito del client, in base al quale l'accesso utente e le notifiche sono consentite.
  - **Sì**: l'area Controllo delle app e del browser nell'app Sicurezza di Windows è nascosta agli utenti finali. Le notifiche relative al controllo delle app e del browser sono eliminate.

- **Nascondi l'area Sicurezza dei dispositivi nell'app Sicurezza di Windows**  
  CSP: [DisableDeviceSecurityUI](https://go.microsoft.com/fwlink/?linkid=873670)

  - **Non configurato** (*impostazione predefinita*): l'impostazione torna al valore predefinito del client, in base al quale l'accesso utente e le notifiche sono consentite.
  - **Sì**: l'area Protezione hardware nell'app Sicurezza di Windows è nascosta agli utenti finali. Le notifiche relative alla protezione degli hardware sono eliminate.
  
- **Nascondi l'area Prestazioni e integrità del dispositivo nell'app Sicurezza di Windows**  
  CSP: [DisableHealthUI](https://go.microsoft.com/fwlink/?linkid=873671)

  - **Non configurato** (*impostazione predefinita*): l'impostazione torna al valore predefinito del client, in base al quale l'accesso utente e le notifiche sono consentite.
  - **Sì**: l'area Prestazioni e integrità del dispositivo nell'app Sicurezza di Windows è nascosta agli utenti finali. Le notifiche relative alle prestazioni e all'integrità del dispositivo sono state eliminate.

- **Nascondi l'area Opzioni famiglia nell'app Sicurezza di Windows**  
  CSP: [DisableFamilyUI](https://go.microsoft.com/fwlink/?linkid=873673)

  - **Non configurato** (*impostazione predefinita*): l'impostazione torna al valore predefinito del client, in base al quale l'accesso utente e le notifiche sono consentite.
  - **Sì**: l'area Opzioni famiglia nell'app Sicurezza di Windows è nascosta agli utenti finali. Inoltre, le notifiche relative alle opzioni famiglia sono eliminate.

- **Notifiche dell'app Sicurezza di Windows**  
  CSP: [DisableNotifications](https://go.microsoft.com/fwlink/?linkid=873675)

  Usare questa impostazione per bloccare le notifiche di Sicurezza di Windows agli utenti relative a tutte le impostazioni delle funzionalità precedenti. In alternativa, è possibile gestire le notifiche dell'app Sicurezza di Windows per funzionalità usando le impostazioni di avanzamento.

  - **Non configurato** (*impostazione predefinita*): tutte le notifiche dell'app Sicurezza di Windows non controllate da altre impostazioni sono consentite.
  - **Blocca notifiche non critiche**: le notifiche, ad esempio i completamenti di analisi, sono bloccate.
  - **Blocca tutte le notifiche**: le notifiche critiche e non critiche sono bloccate per tutte le funzionalità di Sicurezza di Windows.

- **Nascondi l'icona di Sicurezza di Windows dall'area di notifica**  
  CSP: [HideWindowsSecurityNotificationAreaControl](https://go.microsoft.com/fwlink/?linkid=2114313&clcid=0x409)

  L'utente deve disconnettersi e accedere o riavviare il computer per applicare l'impostazione.
  - **Non configurato** (*impostazione predefinita*): viene ripristinata l'impostazione predefinita del client, ovvero mostrare l'icona.
  - **Sì**: l'icona di Sicurezza di Windows è nascosta dall'area di notifica degli utenti.
  
- **Disabilita l'opzione Cancella TPM nell'app Sicurezza di Windows**  
  CSP: [DisableClearTpmButton](https://go.microsoft.com/fwlink/?linkid=2114125&clcid=0x409)

  - **Non configurato** (*impostazione predefinita* ): l'impostazione torna al valore predefinito del client, in base al quale l'accesso utente e le notifiche sono consentite.
  - **Sì**: l'accesso al pulsante Cancella TPM nell'app Sicurezza di Windows è disabilitato.

- **Richiedi agli utenti di aggiornare il firmware TPM se vengono rilevate vulnerabilità**  
  CSP: [DisableTpmFirmwareUpdateWarning](https://go.microsoft.com/fwlink/?linkid=2114212&clcid=0x409)

  - **Non configurato** (*impostazione predefinita*): viene ripristinata l'impostazione predefinita del client, in base alla quale non viene inviata una richiesta all'utente.
  - **Sì**: consente a Windows di chiedere agli utenti finali quando viene rilevata una potenziale vulnerabilità nel firmware TPM. È quindi consigliabile eseguire gli aggiornamenti del firmware per risolvere la vulnerabilità.

- **Informazioni di contatto per il supporto all'organizzazione**  
  CSP: [EnableCustomizedToasts](https://go.microsoft.com/fwlink/?linkid=873676)

  Dichiarare dove si desiderano visualizzare le informazioni relative all'organizzazione IT nell'app Sicurezza di Windows e le notifiche.
  - **Non configurato** (*impostazione predefinita*)
  - **Visualizza nell'app e nelle notifiche**
  - **Visualizza solo nell'app**
  - **Visualizza solo nelle notifiche**
