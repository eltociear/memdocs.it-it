---
title: Impostazioni dei criteri relativi all'antivirus in macOS per Microsoft Defender Antivirus per Intune | Microsoft Docs
description: Visualizzare l'elenco delle impostazioni nel profilo di Microsoft Defender Antivirus per macOS. Questo profilo fa parte del criterio Antivirus di Sicurezza degli endpoint per macOS in Microsoft Intune.
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
ms.reviewer: samyada
ms.openlocfilehash: a75fe5bac4bb99b30e21ec842dcbbe3be83e9e5b
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/26/2020
ms.locfileid: "88909449"
---
# <a name="settings-for-microsoft-defender-atp-for-mac-in-microsoft-intune"></a>Impostazioni per Microsoft Defender ATP per Mac in Microsoft Intune

È possibile visualizzare le impostazioni del profilo *Antivirus* configurabili per Microsoft Defender ATP per Mac in Microsoft Intune. Per altre informazioni su queste impostazioni, vedere [Microsoft Defender Advanced Threat Protection per Mac](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) nella documentazione di Windows.

Informazioni sull'uso dei [criteri di sicurezza degli endpoint](../protect/endpoint-security-policy.md) in Intune.

**Microsoft Defender ATP**

- **Protezione in tempo reale**  
  Consente di richiedere che nei dispositivi macOS Defender usi la funzionalità di monitoraggio in tempo reale. Il monitoraggio in tempo reale consente di individuare il malware e impedirne l'installazione o l'esecuzione nel dispositivo. È possibile disattivare questa impostazione per un breve periodo di tempo, dopo il quale si riattiva automaticamente.

  - **Non configurata** (*impostazione predefinita*): l'impostazione viene ripristinata sul valore predefinito di sistema
  - **Abilitata**: impone l'uso del monitoraggio in tempo reale. Gli utenti dei dispositivi non possono modificare questa impostazione.
  - **Disabilitata**: l'impostazione è disabilitata. Gli utenti dei dispositivi non possono modificare questa impostazione.

- **Protezione fornita dal cloud**  
  Per impostazione predefinita, Defender invia informazioni a Microsoft in merito a eventuali problemi riscontrati. Le informazioni vengono analizzate per acquisire altre informazioni sui problemi riscontrati dall'utente e da altri clienti e offrire soluzioni migliorate. La protezione funziona in modo più efficiente se l'opzione *Invio automatico di file di esempio* è attivata.

  - **Non configurata** (*impostazione predefinita*): l'impostazione viene ripristinata sul valore predefinito di sistema.
  - **Abilitata**: la protezione fornita dal cloud è attiva. Gli utenti dei dispositivi non possono modificare questa impostazione.
  - **Disabilitata**: l'impostazione è disabilitata. Gli utenti dei dispositivi non possono modificare questa impostazione.

- **Invio automatico di file di esempio**  
  Consente di inviare file di esempio a Microsoft per contribuire alla protezione degli utenti dei dispositivi e dell'organizzazione da minacce potenziali.

  - **Non configurata** (*impostazione predefinita*): l'impostazione viene ripristinata sul valore predefinito di sistema.
  - **Abilitata**: la protezione fornita dal cloud è attiva.  Gli utenti dei dispositivi non possono modificare questa impostazione.
  - **Disabilitata**: l'impostazione è disabilitata. Gli utenti dei dispositivi non possono modificare questa impostazione.

- **Raccolta dati di diagnostica**

  Consente di configurare la modalità di condivisione dei dati di diagnostica e di utilizzo con Microsoft.

  - **Non configurata** (*impostazione predefinita*): l'impostazione viene ripristinata sul valore predefinito di sistema.
  - **Richiesto**
  - **Facoltativo**

- **Cartelle escluse dall'analisi**  
  Selezionare **Aggiungi** e quindi specificare le cartelle da ignorare durante un'analisi.

- **File esclusi dall'analisi**  
  Selezionare **Aggiungi** e quindi specificare i file da ignorare durante un'analisi.

- **Tipi di file esclusi dall'analisi**  
  Selezionare **Aggiungi** e quindi specificare le estensioni di file da ignorare durante un'analisi.

- **Processi esclusi dall'analisi**  
  Selezionare **Aggiungi** e quindi specificare i processi da ignorare durante un'analisi.