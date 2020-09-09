---
title: Pagina relativa allo stato della registrazione di Windows Autopilot
ms.reviewer: ''
manager: laurawi
description: Fornisce una panoramica delle funzionalità della pagina relativa allo stato della registrazione, configurazione
keywords: Plug and Forget di Autopilot, Windows 10
ms.technology: windows
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
ms.openlocfilehash: a7d368aef0b10fbe78e2c4ca141a39aa4ed6d803
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/09/2020
ms.locfileid: "89606606"
---
# <a name="windows-autopilot-enrollment-status-page"></a>Pagina relativa allo stato della registrazione di Windows Autopilot

**Si applica a**

-  Windows 10 versione 1803 e successive 

Quando un utente accede per la prima volta a un dispositivo, nella pagina stato della registrazione (ESP) viene visualizzato lo stato di avanzamento della configurazione del dispositivo. L'ESP garantisce inoltre che il dispositivo si trovi nello stato previsto prima che l'utente possa accedere al desktop per la prima volta.

L'ESP tiene traccia dell'installazione di applicazioni, criteri di sicurezza, certificati e connessioni di rete. Un amministratore può distribuire i profili ESP a un utente di Intune con licenza e configurare impostazioni specifiche all'interno del profilo ESP. Di seguito sono riportate alcune di queste impostazioni:
- Forzare l'installazione di applicazioni specifiche.
- Consente agli utenti di raccogliere i log per la risoluzione dei problemi.
- Specificare le azioni che possono essere eseguite dall'utente se l'installazione non viene eseguita.

Per altre informazioni, vedere come configurare la pagina relativa [allo stato della registrazione in Intune](/intune/windows-enrollment-status).  
 
![Pagina Stato registrazione](images/enrollment-status-page.png)
 

## <a name="more-information"></a>Altre informazioni

Per ulteriori informazioni sulla configurazione della pagina relativa allo stato della registrazione, vedere la [documentazione Microsoft Intune](/intune/windows-enrollment-status).<br>
Per informazioni dettagliate sull'implementazione sottostante, vedere i [Dettagli FirstSyncStatus nella documentazione di DMCLIENT CSP](/windows/client-management/mdm/dmclient-csp).<br>
Per ulteriori informazioni sul blocco per l'installazione di app:
- [Blocco per l'installazione di app tramite la pagina relativa allo stato della registrazione](/archive/blogs/mniehaus/blocking-for-app-installation-using-enrollment-status-page).
- [Suggerimento per il supporto: l'installazione di Office C2R viene ora rilevata durante ESP](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Office-C2R-installation-is-now-tracked-during-ESP/ba-p/295514).
