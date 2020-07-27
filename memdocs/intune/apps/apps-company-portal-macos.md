---
title: Aggiungere l'app Portale aziendale per macOS
titleSuffix: Microsoft Intune
description: Aggiungere l'app Portale aziendale macOS.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/16/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: a58e22af70a3cf119cb044a15b40ba581fe6452c
ms.sourcegitcommit: 5c15b59cde085787b85f032f88add70a11d8e9a2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/17/2020
ms.locfileid: "86452848"
---
# <a name="add-the-macos-company-portal-app"></a>Aggiungere l'app Portale aziendale macOS

Per gestire i dispositivi, installare app facoltative e ottenere l'accesso alle risorse protette dall'accesso condizionale nei dispositivi macOS con affinità utente, gli utenti devono installare l'app Portale aziendale e accedervi. È possibile fornire agli utenti istruzioni per installare l'app Portale aziendale per macOS o installarla nei dispositivi già registrati direttamente da Intune.

Per installare l'app Portale aziendale per macOS, è possibile usare una delle opzioni seguenti:
- [Dare istruzioni agli utenti di scaricare e installare l'app Portale aziendale](#instruct-users-to-download-and-install-company-portal)
- [Installare Portale aziendale per macOS come app LOB di macOS](#install-company-portal-for-macos-as-a-macos-lob-app)
- [Installare Portale aziendale per macOS usando uno script della shell macOS](#install-company-portal-for-macos-by-using-a-macos-shell-script)

Per mantenere le app più sicure e aggiornate una volta installate, l'app Portale aziendale viene fornita con Microsoft AutoUpdate (MAU).

> [!NOTE]
> L'app Portale aziendale può essere installata automaticamente solo nei dispositivi che usano Intune e sono già registrati usando la registrazione diretta o la registrazione automatica dei dispositivi. Per la registrazione manuale o di dispositivi personali, è necessario scaricare e installare l'app Portale aziendale per avviare la registrazione. Vedere [Dare istruzioni agli utenti di scaricare e installare l'app Portale aziendale](#instruct-users-to-download-and-install-company-portal).
## <a name="instruct-users-to-download-and-install-company-portal"></a>Dare istruzioni agli utenti di scaricare e installare l'app Portale aziendale

È possibile dare istruzioni agli utenti di scaricare, installare e accedere all'app Portale aziendale per macOS. Per istruzioni sul download, l'installazione e l'accesso all'app Portale aziendale, vedere [Registrare il dispositivo macOS con l'app Portale aziendale](https://docs.microsoft.com/mem/intune/user-help/enroll-your-device-in-intune-macos-cp).

##  <a name="install-company-portal-for-macos-as-a-macos-lob-app"></a>Installare Portale aziendale per macOS come app LOB di macOS

L'app Portale aziendale per macOS può essere scaricata e installata usando la funzionalità [app LOB di macOS](lob-apps-macos.md). La versione scaricata è la versione che verrà sempre installata e potrebbe essere necessario aggiornarla periodicamente per assicurarsi che gli utenti ottengano un'esperienza ottimale durante la registrazione iniziale.

1. Scaricare l'app Portale aziendale per macOS da https://go.microsoft.com/fwlink/?linkid=853070. 

2. Seguire le istruzioni per creare un'app LOB macOS in [App line-of-business di macOS](lob-apps-macos.md).

> [!NOTE]
> Dopo averla installata, l'app Portale aziendale per macOS verrà aggiornata automaticamente tramite Microsoft AutoUpdate (MAU).
## <a name="install-company-portal-for-macos-by-using-a-macos-shell-script"></a>Installare Portale aziendale per macOS usando uno script della shell macOS

L'app Portale aziendale per macOS può essere scaricata e installata usando la funzionalità [Script della shell macOS](macos-shell-scripts.md). Questa opzione installerà sempre la versione corrente dell'app Portale aziendale per macOS, ma non fornirà i report di installazione dell'applicazione a cui gli utentri potrebbero essere abituati per la distribuzione di applicazioni usando [app LOB di macOS](lob-apps-macos.md).

1. Scaricare uno script di esempio per installare l'app Portale aziendale per macOS da [Intune Shell Script Samples - Company Portal](https://github.com/microsoft/shell-intune-samples/tree/master/Apps/Company%20Portal) (Esempi di script della shell di Intun - Portale aziendale).

2. Seguire le istruzioni per distribuire lo script della shell macOS usando [script della shell macOS](macos-shell-scripts.md). 
    - Impostare **Esegui lo script come utente connesso** su **No** (per l'esecuzione le contesto del sistema).
    - Impostare **Numero massimo di nuovi tentativi in caso di errore dello script** su **3**.

> [!NOTE]
> Lo script richiederà l'accesso a Internet durante l'esecuzione per scaricare la versione corrente dell'app Portale aziendale per macOS. 
## <a name="next-steps"></a>Passaggi successivi
- Per altre informazioni sull'assegnazione di app, vedere [Assegnare app ai gruppi](apps-deploy.md).
- Per altre informazioni sulla configurazione della registrazione automatica dei dispositivi, vedere [Device Enrollment Program - Registrare dispositivi macOS](https://docs.microsoft.com/mem/intune/enrollment/device-enrollment-program-enroll-macos).
- Per altre informazioni sulla configurazione delle impostazioni di Microsoft AutoUpdate in macOS, vedere [Aggiornamenti Mac](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/mac-updates).