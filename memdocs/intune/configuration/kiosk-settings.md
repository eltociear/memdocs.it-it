---
title: Impostazioni della modalità tutto schermo per dispositivi Windows e Holographic in Microsoft Intune - Azure | Microsoft Docs
description: Configurare i dispositivi Windows 10 e versioni successive e Windows Holographic for Business per l'esecuzione di una o più app in modalità tutto schermo, personalizzare il menu Start, aggiungere app, visualizzare la barra della applicazioni e configurare un Web browser in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: f58e457a5868053a94e1f2c1185bbae0e4b69327
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/19/2020
ms.locfileid: "85093073"
---
# <a name="windows-10-and-windows-holographic-for-business-device-settings-to-run-as-a-dedicated-kiosk-using-intune"></a>Impostazioni dei dispositivi Windows 10 e Windows Holographic for Business per l'esecuzione come dispositivo in modalità tutto schermo dedicato tramite Intune

Nei dispositivi Windows 10 usare Intune per eseguire i dispositivi come chiosco multimediale, talvolta noto anche come dispositivo dedicato. Un dispositivo nella modalità tutto schermo può eseguire un'app o molte app. È possibile visualizzare e personalizzare un menu Start, aggiungere app diverse, incluse app Win32, aggiungere una specifica home page per un Web browser e molto altro. 

Questa funzionalità si applica a:

- Windows 10 e versioni successive
- Windows Holographic for Business

Per creare profili in modalità tutto schermo per altre piattaforme, vedere [Amministratore di dispositivi Android](device-restrictions-android.md#kiosk), [Android Enterprise](device-restrictions-android-for-work.md#device-experience) e [iOS/iPadOS](device-restrictions-ios.md#kiosk).

Intune supporta un profilo in modalità a tutto schermo per ogni dispositivo. Se servono più profili per la modalità tutto schermo in un singolo dispositivo, è possibile usare un [OMA-URI personalizzato](custom-settings-windows-10.md).

Intune usa "profili di configurazione" per creare e personalizzare queste impostazioni per le esigenze dell'organizzazione. Dopo aver aggiunto queste funzionalità in un profilo, eseguire il push o distribuire queste impostazioni ai gruppi nell'organizzazione.

Questo articolo illustra come creare un profilo di configurazione del dispositivo. Per un elenco di tutte le impostazioni e delle operazioni corrispondenti, vedere [Impostazioni della modalità tutto schermo per Windows 10](kiosk-settings-windows.md) e [Impostazioni della modalità tutto schermo per Windows Holographic for Business](kiosk-settings-holographic.md).

## <a name="create-the-profile"></a>Creare il profilo

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selezionare **Dispositivi** > **Profili di configurazione** > **Crea profilo**.
3. Immettere le proprietà seguenti:

   - **Piattaforma**: selezionare **Windows 10 e versioni successive**.
   - **Profilo**: selezionare **Modalità tutto schermo**.

4. Selezionare **Crea**.
5. In **Informazioni di base** immettere le proprietà seguenti:

   - **Nome**: immettere un nome descrittivo per il nuovo profilo.
   - **Descrizione**: Immettere una descrizione del profilo. Questa impostazione è facoltativa ma consigliata.

6. Selezionare **Avanti**.
7. In **Impostazioni di configurazione** > **selezionare una modalità tutto schermo**, scegliere il tipo di modalità tutto schermo supportata dai criteri. Le opzioni includono:

    - **Non configurata** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione. il criterio non abilita la modalità tutto schermo.
    - **App singola per chiosco multimediale a schermo intero**: il dispositivo viene eseguito con un singolo account utente e bloccato su una singola app dello Store. Pertanto, quando l'utente accede, viene avviata un'app specifica. Questa modalità impedisce anche all'utente di aprire nuove app o modificare l'app in esecuzione.
    - **App multiple per chiosco multimediale**: il dispositivo esegue più app dello Store, app Win32 o app predefinite di Windows tramite ID modello utente applicazione (AUMID). Solo le app aggiunte sono disponibili nel dispositivo.

        Il vantaggio di avere più app in modalità tutto schermo, o un dispositivo predefinito per uno scopo, consiste nel garantire un'esperienza semplice, consentendo di accedere solo alle app necessarie e rimuovendo dalla visualizzazione le app non necessarie.

    Per un elenco di tutte le impostazioni e delle operazioni corrispondenti, vedere:

      - [Impostazioni della modalità tutto schermo per Windows 10](kiosk-settings-windows.md)
      - [Impostazioni della modalità tutto schermo per Windows Holographic for Business](kiosk-settings-holographic.md)

8. Selezionare **Avanti**.

9. In **Tag ambito** (facoltativo) assegnare un tag per filtrare il profilo a gruppi IT specifici, ad esempio `US-NC IT Team` o `JohnGlenn_ITDepartment`. Per altre informazioni sui tag di ambito, vedere [Usare il controllo degli accessi in base al ruolo (RBAC) e i tag di ambito per l'infrastruttura IT distribuita](../fundamentals/scope-tags.md).

    Selezionare **Avanti**.

10. In **Assegnazioni** selezionare gli utenti o il gruppo utenti che riceveranno il profilo. Per altre informazioni sull'assegnazione di profili, vedere [Assegnare profili utente e dispositivo](device-profile-assign.md).

    Selezionare **Avanti**.

11. In **Rivedi e crea** rivedere le impostazioni. Quando si seleziona **Crea**, le modifiche vengono salvate e il profilo viene assegnato. Il criterio viene visualizzato anche nell'elenco dei profili.

Alla successiva sincronizzazione di ogni dispositivo viene applicato il criterio.

## <a name="next-steps"></a>Passaggi successivi

Dopo l'[assegnazione del profilo](device-profile-assign.md) [monitorarne lo stato](device-profile-monitor.md).

È possibile creare profili in modalità tutto schermo per i dispositivi che eseguono le piattaforme seguenti:

- [Amministratore di dispositivi Android](device-restrictions-android.md#kiosk)
- [Android Enterprise](device-restrictions-android-for-work.md#device-experience)
- [Windows 10 e versioni successive](kiosk-settings-windows.md)
- [Windows Holographic for Business](kiosk-settings-holographic.md)
