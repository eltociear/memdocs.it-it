---
title: Intune gestito da 21Vianet in Cina
titleSuffix: ''
description: Intune gestito da 21Vianet in Cina.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 07/07/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: ''
ms.reviewer: amsaeedi
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 34f1aeb9ec265b7a6e09135bc931574732f5816d
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88994209"
---
# <a name="intune-operated-by-21vianet-in-china"></a>Intune gestito da 21Vianet in Cina  

Intune gestito da 21Vianet è progettato per assicurare servizi cloud sicuri, affidabili e scalabili in Cina. Intune come servizio si basa su Microsoft Azure. Microsoft Azure gestito da 21Vianet è un'istanza di servizi cloud che si trovano in Cina, fisicamente separata. Viene gestito e sottoposto a transazioni in modo indipendente da 21Vianet. Questo servizio si basa sulla tecnologia che Microsoft ha concesso in licenza a 21Vianet.

Microsoft non gestisce il servizio. 21Vianet controlla, offre e gestisce la fornitura del servizio. 21Vianet è un provider di servizi di data center Internet in Cina. Offre servizi di hosting, servizi di rete gestiti e servizi di infrastruttura di cloud computing. Grazie alle tecnologie in licenza offerte da Microsoft, 21Vianet gestisce i data center locali che consentono di usare il servizio Intune e al tempo stesso conservare i dati in Cina. 21Vianet offre anche i servizi di sottoscrizione, fatturazione e supporto tecnico dell'utente.

[!INCLUDE [GDPR-related guidance](../includes/gdpr-dsr-and-stp-note.md)]

## <a name="feature-differences-in-intune-operated-by-21vianet"></a>Differenze di funzionalità in Intune gestito da 21Vianet

Poiché i servizi in Cina sono gestiti da un partner che si trova in Cina, in Intune esistono alcune differenze in termini di funzionalità. 

- Intune gestito da 21Vianet supporta solo distribuzioni autonome. Il supporto per la co-gestione con System Center Configuration Manager è attualmente in fase di sviluppo.
- Le migrazioni da cloud pubblici a cloud sovrani non sono supportate. I clienti interessati a passare a Intune gestito da 21Vianet devono eseguire la migrazione manualmente.
- La funzionalità di collegamento del tenant (la sincronizzazione dei dispositivi in Intune senza registrazione per supportare scenari di console cloud) non è attualmente supportata.
- Le credenziali derivate non sono supportate con Intune gestito da 21Vianet.
- Intune gestito da 21Vianet non supporta l'agente di Intune, pertanto non supporta la gestione di computer legacy.
- La gestione di Windows 10 è supportata tramite l'uso del canale MDM moderno.
- Intune gestito da 21Vianet non supporta Exchange Connector locale.
- Le funzionalità di Windows Autopilot e Business Store non sono attualmente disponibili.
- Google Mobile Services non è disponibile in Cina. I clienti di Intune gestito da 21Vianet non possono pertanto usare le funzionalità che richiedono Google Mobile Services. Queste funzionalità comprendono:
  - Funzionalità di Google Play Protect, ad esempio l'attestazione del dispositivo SafetyNet.
  - Gestione delle app da Google Play Store.
  - Funzionalità di Android Enterprise. Per altre informazioni, vedere la [documentazione Google](https://support.google.com/work/android/answer/6270910?hl=en).
- L'app Portale aziendale Intune per Android usa Google Play Services per comunicare con il servizio Microsoft Intune. Poiché Google Play Services non è disponibile in Cina, per il completamento di alcune attività possono essere necessarie fino a 8 ore. Per altre informazioni, vedere questo [articolo](../apps/manage-without-gms.md#limitations-of-intune-device-administrator-management-when-gms-is-unavailable). 
- Per attenersi alle normative locali e offrire funzionalità migliorate, l'esperienza client di Intune (app Portale aziendale) potrebbe essere diversa in Cina.
- La limitazione della rete non è disponibile.
- La disponibilità della gestione di applicazioni mobili (MAM, Mobile Application Management) è condizionale alle app che sono disponibili nella Repubblica popolare cinese.

## <a name="you-control-customer-data"></a>Controllo dei dati dei clienti

In Microsoft Azure, Intune, Microsoft 365 e Power BI gestiti da 21Vianet si ha pieno controllo sui dati:
- Si sa dove si trovano i dati dei clienti.
- Si controlla l'accesso ai dati dei clienti.
- Si controllano i dati dei clienti se il servizio viene abbandonato.
- Si ha la possibilità di controllare la sicurezza dei dati dei clienti.

Con Microsoft Azure, Intune, Microsoft 365 e Power BI gestiti da 21Vianet, si è proprietari dei dati:
- 21Vianet non usa i dati dei clienti per la pubblicità.
- Si controlla chi ha accesso ai dati dei clienti.
- Si usa l'isolamento logico per separare i dati di ogni cliente.
- Sono disponibili criteri semplici e trasparenti per l'uso dei dati e controlli indipendenti.
- Per contratto, gli subappaltatori Microsoft devono rispettare i requisiti relativi alla tutela della privacy.

## <a name="data-subject-requests"></a>Richieste per gli interessati

Il ruolo Amministratore tenant per Intune gestito da 21Vianet può richiedere dati per gli interessati nei modi seguenti:

- Usando l'interfaccia di amministrazione di Azure Active Directory, un Amministratore tenant può eliminare definitivamente un interessato da Azure Active Directory e dai servizi correlati. Per altre informazioni, vedere [Richieste degli interessati per Azure -Eliminare](/microsoft-365/compliance/gdpr-dsr-azure?view=o365-worldwide#step-5-delete)
- I log generati dal sistema per i servizi Microsoft gestiti da 21Vianet possono essere esportati dagli Amministratori tenant usando l'esportazione dei log di dati. Per altre informazioni, vedere [Richieste degli interessati per Azure -Esportare](/microsoft-365/compliance/gdpr-dsr-azure?view=o365-worldwide#step-6-export).

## <a name="next-steps"></a>Passaggi successivi

[Altre informazioni sulle configurazioni supportate in Intune](supported-devices-browsers.md)