---
title: Aggiungere o configurare le impostazioni Istruzione in Microsoft Intune - Azure | Microsoft Docs
description: Usare l'app Test ed esami in un profilo di configurazione del dispositivo in Windows 10 e versioni successive in Microsoft Intune. Creare un profilo di configurazione usando le impostazioni Istruzione e immettere l'URL di un'app di test, scegliere la modalità di accesso degli utenti, monitorare lo schermo durante il test e consentire o impedire i suggerimenti di testo durante il test.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 11/04/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 6f4de4bd-3dde-4a8d-8e22-46c5d06c3eea
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 12d04869834691167c2f31be853029c9a939a338
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "79364331"
---
# <a name="use-the-take-a-test-app-on-windows-10-devices-in-microsoft-intune"></a>Usare l'app Test ed esami nei dispositivi Windows 10 in Microsoft Intune



I profili di formazione in Intune hanno lo scopo di consentire agli studenti di eseguire un test o un esame da un dispositivo. Questa funzionalità include l'app **Test ed esami** e le impostazioni per aggiungere un URL di test, scegliere la modalità di accesso degli utenti finali al test e altro ancora. Questa funzionalità supporta la piattaforma seguente:

- Windows 10 e versioni successive

Quando l'utente accede, l'app Test ed esami viene aperta automaticamente con il test da eseguire. Mentre il test è in corso, non è possibile eseguire altre applicazioni nel dispositivo. [Eseguire test in Windows 10](https://docs.microsoft.com/education/windows/take-tests-in-windows-10) offre altri dettagli dell'app Test ed esami.

Questo articolo elenca i passaggi per creare un profilo di configurazione del dispositivo in Microsoft Intune e include anche informazioni da leggere e imparare sulle impostazioni di formazione disponibili per i dispositivi Windows 10.

## <a name="create-a-device-profile"></a>Creare un profilo del dispositivo

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selezionare **Dispositivi** > **Profili di configurazione** > **Crea profilo**.
3. Immettere le proprietà seguenti:

    - **Nome**: immettere un nome descrittivo per il nuovo profilo.
    - **Descrizione**: Immettere una descrizione del profilo. Questa impostazione è facoltativa ma consigliata.
    - **Piattaforma**: scegliere **Windows 10 e versioni successive**.
    - **Profilo**: scegliere **Profilo di formazione**.

4. Immettere le impostazioni da configurare:

    - [Windows 10 e versioni successive](education-settings-windows.md)

5. Selezionare **OK** > **Crea** per salvare le modifiche.

Dopo aver immesso le impostazioni e creato il profilo, il profilo viene visualizzato nell'elenco dei profili. Ora [assegnare il profilo ad alcuni gruppi](device-profile-assign.md).

## <a name="next-steps"></a>Passaggi successivi

Visualizzare l'elenco delle [ impostazioni di formazione di Windows 10](education-settings-windows.md) e le relative descrizioni.

[Assegnare il profilo](device-profile-assign.md) e [monitorarne lo stato](device-profile-monitor.md).
