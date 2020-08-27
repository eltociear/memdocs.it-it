---
title: Pagina relativa allo stato della registrazione di Windows Autopilot
ms.reviewer: ''
manager: laurawi
description: Fornisce una panoramica delle funzionalità della pagina relativa allo stato della registrazione, configurazione
keywords: Plug and Forget di Autopilot, Windows 10
ms.prod: w10
ms.mktglfcycl: deploy
ms.sitesec: library
ms.pagetype: deploy
ms.localizationpriority: medium
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: dd60c47e0e22aa24cf1d4d4df3324f3b1bfed21c
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/26/2020
ms.locfileid: "88908255"
---
# <a name="windows-autopilot-enrollment-status-page"></a>Pagina relativa allo stato della registrazione di Windows Autopilot

**Si applica a**

-   Windows 10 versione 1803 e successive 

La pagina relativa allo stato della registrazione (ESP) Visualizza lo stato del processo di configurazione completo del dispositivo quando un utente gestito da MDM accede a un dispositivo per la prima volta.  ESP consente agli utenti di comprendere lo stato di avanzamento del provisioning dei dispositivi e garantisce che il dispositivo abbia soddisfatto lo stato desiderato per le organizzazioni prima che l'utente possa accedere al desktop per la prima volta.

L'ESP tiene traccia dell'installazione di applicazioni, criteri di sicurezza, certificati e connessioni di rete.  Con Intune, un amministratore può distribuire i profili ESP a un utente di Intune con licenza e configurare impostazioni specifiche all'interno del profilo ESP; Alcune di queste impostazioni sono: forzare l'installazione di applicazioni specifiche, consentire agli utenti di raccogliere i log di risoluzione dei problemi, specificare le operazioni che un utente può eseguire se l'installazione del dispositivo non riesce.  Per altre informazioni, vedere come configurare la pagina relativa [allo stato della registrazione in Intune](/intune/windows-enrollment-status).   
 
 ![Pagina Stato registrazione](images/enrollment-status-page.png)
 

## <a name="more-information"></a>Ulteriori informazioni

Per ulteriori informazioni sulla configurazione della pagina relativa allo stato della registrazione, vedere la [documentazione Microsoft Intune](/intune/windows-enrollment-status).<br>
Per informazioni dettagliate sull'implementazione sottostante, vedere i [Dettagli FirstSyncStatus nella documentazione di DMCLIENT CSP](/windows/client-management/mdm/dmclient-csp).<br>
Per ulteriori informazioni sul blocco per l'installazione di app:
- [Blocco per l'installazione di app tramite la pagina relativa allo stato della registrazione](/archive/blogs/mniehaus/blocking-for-app-installation-using-enrollment-status-page).
- [Suggerimento per il supporto: l'installazione di Office C2R viene ora rilevata durante ESP](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Office-C2R-installation-is-now-tracked-during-ESP/ba-p/295514).