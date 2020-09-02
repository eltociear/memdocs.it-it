---
title: Aggiungere o configurare le impostazioni Istruzione in Microsoft Intune - Azure | Microsoft Docs
description: Usare l'app Test ed esami in un profilo di configurazione del dispositivo in Windows 10 e versioni successive in Microsoft Intune. Creare un profilo di configurazione usando le impostazioni Istruzione e immettere l'URL di un'app di test, scegliere la modalità di accesso degli utenti, monitorare lo schermo durante il test e consentire o impedire i suggerimenti di testo durante il test.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 05/13/2020
ms.topic: how-to
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
ms.openlocfilehash: 7b1a605e456edb525afec306ff594ba7cc3895aa
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/26/2020
ms.locfileid: "88912730"
---
# <a name="use-the-take-a-test-app-on-windows-10-devices-in-microsoft-intune"></a>Usare l'app Test ed esami nei dispositivi Windows 10 in Microsoft Intune

I profili di formazione in Intune hanno lo scopo di consentire agli studenti di eseguire un test o un esame da un dispositivo. Questa funzionalità include l'app **Test ed esami** e le impostazioni per aggiungere un URL di test, scegliere la modalità di accesso degli utenti finali al test e altro ancora. Questa funzionalità supporta la piattaforma seguente:

- Windows 10 e versioni successive

Quando l'utente accede, l'app Test ed esami viene aperta automaticamente con il test da eseguire. Mentre il test è in corso, non è possibile eseguire altre applicazioni nel dispositivo. [Eseguire test in Windows 10](/education/windows/take-tests-in-windows-10) offre altri dettagli dell'app Test ed esami.

Questo articolo elenca i passaggi per creare un profilo di configurazione del dispositivo in Microsoft Intune e include anche informazioni da leggere e imparare sulle impostazioni di formazione disponibili per i dispositivi Windows 10.

## <a name="create-a-device-profile"></a>Creare un profilo del dispositivo

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selezionare **Dispositivi** > **Profili di configurazione** > **Crea profilo**.
3. Immettere le proprietà seguenti:

    - **Piattaforma**: selezionare **Windows 10 e versioni successive**.
    - **Profilo**: Selezionare **Valutazione sicura (Education)** .

4. Selezionare **Crea**.
5. In **Informazioni di base** immettere le proprietà seguenti:

    - **Nome**: immettere un nome descrittivo per il nuovo profilo.
    - **Descrizione**: Immettere una descrizione del profilo. Questa impostazione è facoltativa ma consigliata.

6. Selezionare **Avanti**.
7. In **Impostazioni di configurazione** immettere le impostazioni da configurare:

    - [Windows 10 e versioni successive](education-settings-windows.md)

8. Selezionare **Avanti**.

9. In **Tag ambito** (facoltativo) assegnare un tag per filtrare il profilo a gruppi IT specifici, ad esempio `US-NC IT Team` o `JohnGlenn_ITDepartment`. Per altre informazioni sui tag di ambito, vedere [Usare il controllo degli accessi in base al ruolo (RBAC) e i tag di ambito per l'infrastruttura IT distribuita](../fundamentals/scope-tags.md).

    Selezionare **Avanti**.

10. In **Assegnazioni** selezionare gli utenti o il gruppo utenti che riceveranno il profilo. Per altre informazioni sull'assegnazione di profili, vedere [Assegnare profili utente e dispositivo](device-profile-assign.md).

    Selezionare **Avanti**.

11. In **Rivedi e crea** rivedere le impostazioni. Quando si seleziona **Crea**, le modifiche vengono salvate e il profilo viene assegnato. Il criterio viene visualizzato anche nell'elenco dei profili.

Il criterio viene applicato alla sincronizzazione successiva di ogni dispositivo.

## <a name="next-steps"></a>Passaggi successivi

Visualizzare l'elenco delle [ impostazioni di formazione di Windows 10](education-settings-windows.md) e le relative descrizioni.

Dopo l'[assegnazione del profilo](device-profile-assign.md), [monitorarne lo stato](device-profile-monitor.md).