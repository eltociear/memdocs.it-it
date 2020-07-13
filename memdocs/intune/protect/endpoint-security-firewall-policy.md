---
title: Gestire le impostazioni del firewall con i criteri di sicurezza degli endpoint in Microsoft Intune | Microsoft Docs
description: Configurare e distribuire criteri per i dispositivi gestiti con i criteri firewall per la sicurezza degli endpoint in Microsoft Endpoint Manager.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/15/2020
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
ms.openlocfilehash: 5b33be56975713c801d2ad3fdea17e6303687274
ms.sourcegitcommit: 03d2331876ad61d0a6bb1efca3aa655b88f73119
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/03/2020
ms.locfileid: "85946913"
---
# <a name="firewall-policy-for-endpoint-security-in-intune"></a>Criteri firewall per la sicurezza degli endpoint in Intune

Usare i criteri firewall per la sicurezza degli endpoint in Intune per configurare un firewall predefinito dei dispositivi per i dispositivi che eseguono macOS e Windows 10.

Sebbene sia possibile configurare le stesse impostazioni del firewall usando i profili Endpoint Protection per la configurazione del dispositivo, i profili di configurazione del dispositivo includono categorie aggiuntive di impostazioni. Queste impostazioni aggiuntive non sono correlate ai firewall e possono complicare l'attività di configurare solo le impostazioni del firewall dell'ambiente in uso.

I criteri di sicurezza degli endpoint per firewall sono disponibili in *Gestione* nel nodo **Sicurezza degli endpoint** dell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

Vedere le [impostazioni per i profili firewall](../protect/endpoint-security-Firewall-profile-settings.md).

## <a name="prerequisites-for-firewall-profiles"></a>Prerequisiti per i profili firewall

- Windows 10 o versioni successive
- Qualsiasi versione supportata di macOS

## <a name="firewall-profiles"></a>Profili firewall

**Profili macOS**:

- **Firewall macOS** - Abilita e configura le impostazioni per il firewall integrato su macOS.

**Profili di Windows 10**:

- **Microsoft Defender Firewall** - Configurare le impostazioni per Windows Defender Firewall con sicurezza avanzata. Windows Defender Firewall consente di filtrare il traffico di rete bidirezionale per un dispositivo e può bloccare il traffico di rete non autorizzato in entrata o in uscita dal dispositivo locale.

- **Regole di Windows Defender Firewall** *(Anteprima)* - Definire regole granulari per il firewall tra cui porte, applicazioni, reti e protocolli specifici per consentire o bloccare il traffico di rete. Ogni istanza di questo profilo supporta fino a 150 regole personalizzate.

## <a name="firewall-rule-mergers-and-policy-conflicts"></a>Fusioni di regole del firewall e conflitti tra criteri

Pianificare l'applicazione dei criteri firewall a un dispositivo usando un solo criterio. L'uso di una singola istanza di criteri e di un tipo di criteri consente di evitare la presenza di due criteri distinti che applicano configurazioni diverse alla stessa impostazione, che crea conflitti. Se esiste un conflitto tra due istanze di criteri o tipi di criteri che gestiscono la stessa impostazione con valori diversi, l'impostazione non viene inviata al dispositivo.

- Questo tipo di conflitto di criteri si applica al profilo di **Microsoft Defender Firewall**, che può essere in conflitto con altri profili di Microsoft Defender Firewall o una configurazione del firewall fornita da un tipo di criteri diverso, ad esempio la configurazione del dispositivo.

  I *profili di Microsoft Defender Firewall* non sono in conflitto con i profili delle *regole di Microsoft Defender Firewall*.

Quando si usano i profili delle **regole di Microsoft Defender Firewall**, è possibile applicare più profili di regole allo stesso dispositivo. Tuttavia, quando esistono regole diverse per la stessa operazione con configurazioni diverse, entrambe vengono inviate al dispositivo e creano un conflitto sul dispositivo.

- Se, ad esempio, una regola blocca *Teams.exe* attraverso il firewall e una seconda regola consente *Teams.exe*, entrambe le regole vengono recapitate al client. Questo risultato è diverso dai conflitti creati con altri criteri per le impostazioni del firewall.

Quando le regole di più profili di regole non sono in conflitto tra loro, i dispositivi uniscono le regole di ogni profilo per creare una configurazione combinata delle regole del firewall nel dispositivo. Questo comportamento consente di distribuire più di 150 regole supportate da ogni singolo profilo a un dispositivo.

- Ad esempio, si dispone di due profili di regole di Microsoft Defender Firewall. Il primo profilo consente *Teams.exe* attraverso il firewall. Il secondo profilo consente *Outlook.exe* attraverso il firewall. Quando un dispositivo riceve entrambi i profili, il dispositivo è configurato per consentire entrambe le app attraverso il firewall.

## <a name="next-steps"></a>Passaggi successivi

[Configurare i criteri di sicurezza degli endpoint](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
