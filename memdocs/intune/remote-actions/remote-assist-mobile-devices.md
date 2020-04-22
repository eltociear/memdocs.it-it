---
title: Assistenza remota ai dispositivi mobili gestiti da Intune
description: Per offrire assistenza da remoto agli utenti per i loro dispositivi mobili, è possibile usare quattro opzioni diverse.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 548f63dcbd1635c106573fda40f8cc7bf312866e
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "80086650"
---
# <a name="remotely-assist-mobile-devices-managed-by-microsoft-endpoint-manager"></a>Assistenza remota ai dispositivi mobili gestiti da Microsoft Endpoint Manager

Per l'amministrazione remota di dispositivi gestiti da Microsoft Endpoint Manager, sono disponibili quattro opzioni:

- [Microsoft Teams](https://products.office.com/microsoft-teams/) è l'hub per il lavoro in team in cui è possibile chattare, incontrarsi e collaborare ovunque ci si trovi.
- [Assistenza rapida](https://support.microsoft.com/help/4027243/windows-10-solve-pc-problems-with-quick-assist) è un'applicazione Windows 10 che consente a due persone di condividere un dispositivo attraverso una connessione remota.
- [TeamViewer](https://www.teamviewer.com/) è un programma di terze parti da acquistare separatamente. Offre un set completo di funzionalità di accesso remoto e di supporto. L'[integrazione di TeamViewer](teamviewer-support.md) e Intune consente il supporto remoto tramite TeamViewer con la gestione del connettore direttamente in Intune.
- [Controllo remoto](https://docs.microsoft.com/configmgr/core/clients/manage/remote-control/introduction-to-remote-control) è incluso in Microsoft Endpoint Configuration Manager. Viene usato per amministrare, assistere e visualizzare in remoto tutti i computer del gruppo di lavoro e i computer aggiunti a un dominio.

| Funzionalità, piattaforme, licenze | **Teams** | Assistenza rapida | TeamViewer (Intune) | Controllo remoto (ConfigMgr) |
|:---:|:---:|:---:|:---:|:---:|
| Visualizzazione e controllo remoti |![Segno di spunta](../enrollment/media/enrollment-method-capab/checkmark.png)|![Segno di spunta](../enrollment/media/enrollment-method-capab/checkmark.png)|![Segno di spunta](../enrollment/media/enrollment-method-capab/checkmark.png)|![Segno di spunta](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Chat |![Segno di spunta](../enrollment/media/enrollment-method-capab/checkmark.png)||![Segno di spunta](../enrollment/media/enrollment-method-capab/checkmark.png)||
| Trasferimento di file |![Segno di spunta](../enrollment/media/enrollment-method-capab/checkmark.png)|![Segno di spunta](../enrollment/media/enrollment-method-capab/checkmark.png)|![Segno di spunta](../enrollment/media/enrollment-method-capab/checkmark.png)|![Segno di spunta](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Accesso amministratore con privilegi elevati |||![Segno di spunta](../enrollment/media/enrollment-method-capab/checkmark.png)|![Segno di spunta](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Accesso automatico |||![Segno di spunta](../enrollment/media/enrollment-method-capab/checkmark.png)|![Segno di spunta](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Controllo remoto simultaneo |![Segno di spunta](../enrollment/media/enrollment-method-capab/checkmark.png)|![Segno di spunta](../enrollment/media/enrollment-method-capab/checkmark.png)|||
| Supporto di più utenti |||![Segno di spunta](../enrollment/media/enrollment-method-capab/checkmark.png)|![Segno di spunta](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Azioni remote ||![Segno di spunta](../enrollment/media/enrollment-method-capab/checkmark.png)|![Segno di spunta](../enrollment/media/enrollment-method-capab/checkmark.png)|![Segno di spunta](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Supporto via Internet |![Segno di spunta](../enrollment/media/enrollment-method-capab/checkmark.png)|![Segno di spunta](../enrollment/media/enrollment-method-capab/checkmark.png)|![Segno di spunta](../enrollment/media/enrollment-method-capab/checkmark.png)||
| Creazione di report di controllo |![Segno di spunta](../enrollment/media/enrollment-method-capab/checkmark.png)||![Segno di spunta](../enrollment/media/enrollment-method-capab/checkmark.png)|![Segno di spunta](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Supporto per tutte le piattaforme (Windows, iOS, Android, macOS) |![Segno di spunta](../enrollment/media/enrollment-method-capab/checkmark.png)||![Segno di spunta](../enrollment/media/enrollment-method-capab/checkmark.png)||
| Integrazione con Windows 10 senza app aggiuntive ||![Segno di spunta](../enrollment/media/enrollment-method-capab/checkmark.png)|||
| Necessità di co-gestione del dispositivo da parte di Configuration Manager e Intune ||||![Segno di spunta](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Necessità di licenze aggiuntive\* |![Segno di spunta](../enrollment/media/enrollment-method-capab/checkmark.png)||![Segno di spunta](../enrollment/media/enrollment-method-capab/checkmark.png)|![Segno di spunta](../enrollment/media/enrollment-method-capab/checkmark.png)|

\* Teams richiede una licenza O365 o M365. L'uso di TeamViewer e Intune richiede una licenza sia di TeamViewer che di Intune. Il controllo remoto è una funzionalità di Configuration Manager e richiede una licenza di Configuration Manager.
