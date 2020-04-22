---
title: Usare dispositivi personalizzati in Microsoft Intune - Azure | Microsoft Docs
description: Aggiungere o creare un profilo per usare le impostazioni personalizzate per i dispositivi Windows Phone, Windows 8.1, Windows 10 e versioni successive, amministratore di dispositivi Android, Android Enterprise, macOS e iOS/iPadOS tramite Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/24/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: feb211b1de15aa0400e9ff71b428e2db02ef4b03
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "80551356"
---
# <a name="create-a-profile-with-custom-settings-in-intune"></a>Creare un profilo con impostazioni personalizzate in Intune

Microsoft Intune include molte impostazioni predefinite per controllare diverse funzionalità in un dispositivo. È anche possibile creare profili personalizzati in modo simile ai profili predefiniti. I profili personalizzati sono particolarmente utili quando si vuole usare impostazioni del dispositivo e funzionalità non incluse in Intune. Questi profili includono funzionalità e impostazioni che è possibile controllare nei dispositivi dell'organizzazione. Ad esempio, è possibile creare un profilo personalizzato che imposta la stessa funzionalità per tutti i dispositivi iOS/iPadOS.

Le impostazioni personalizzate sono configurate in modo diverso per ogni piattaforma. Ad esempio, per controllare le funzionalità nei dispositivi Android e Windows, è possibile specificare valori Open Mobile Alliance Uniform Resource Identifier (URI OMA). Per i dispositivi Apple è possibile importare un file creato con [Apple Configurator](https://itunes.apple.com/us/app/apple-configurator-2/id1037126344?mt=12) o [Apple Profile Manager](https://support.apple.com/profile-manager).

Per altre informazioni sui profili di configurazione, vedere [Informazioni sui profili di dispositivo in Microsoft Intune](device-profiles.md).

Questo articolo illustra come creare un profilo personalizzato per l'amministratore di dispositivi Android, Android Enterprise, iOS/iPados, macOS e Windows. È anche possibile visualizzare tutte le impostazioni disponibili per le varie piattaforme.

> [!NOTE]
> L'interfaccia utente di Intune verrà aggiornata a un'esperienza a schermo intero. Questa operazione può richiedere alcune settimane. Fino a quando il tenant in uso non riceve l'aggiornamento, il flusso di lavoro per la creazione o la modifica delle impostazioni descritte in questo articolo sarà leggermente diverso.

## <a name="create-the-profile"></a>Creare il profilo

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selezionare **Dispositivi** > **Profili di configurazione** > **Crea profilo**.
3. Immettere le proprietà seguenti:

    - **Piattaforma**: scegliere la piattaforma dei dispositivi. Le opzioni disponibili sono:  

        - **Amministratore di dispositivi Android**
        - **Android Enterprise**
        - **iOS/iPadOS**
        - **macOS**
        - **Windows 10 e versioni successive**
        - **Windows Phone 8.1**

    - **Profilo**: Selezionare **Personalizzato**.

4. Selezionare **Crea**.
5. In **Informazioni di base** immettere le proprietà seguenti:

    - **Nome**: immettere un nome descrittivo per il criterio. Assegnare ai criteri nomi che possano essere identificati facilmente in un secondo momento. Ad esempio, un nome di criterio valido è **Windows 10: Profilo personalizzato che abilita l'URI OMA AllowVPNOverCellular personalizzato**.
    - **Descrizione**: immettere una descrizione del criterio. Questa impostazione è facoltativa ma consigliata.

6. Selezionare **Avanti**.

7. In **Impostazioni di configurazione** le impostazioni configurabili variano in base alla piattaforma scelta. Scegliere la piattaforma per le impostazioni dettagliate:

    - [Amministratore di dispositivi Android](custom-settings-android.md)
    - [Android Enterprise](custom-settings-android-for-work.md)
    - [iOS/iPadOS](custom-settings-ios.md)
    - [macOS](custom-settings-macos.md)
    - [Windows 10](custom-settings-windows-10.md)
    - [Windows Holographic for Business](custom-settings-windows-holographic.md)
    - [Windows Phone 8.1](custom-settings-windows-phone-8-1.md)

8. Selezionare **Avanti**.
9. In **Tag ambito** (facoltativo) assegnare un tag per filtrare il profilo a gruppi IT specifici, ad esempio `US-NC IT Team` o `JohnGlenn_ITDepartment`. Per altre informazioni sui tag di ambito, vedere [Usare il controllo degli accessi in base al ruolo (RBAC) e i tag di ambito per l'infrastruttura IT distribuita](../fundamentals/scope-tags.md).

    Selezionare **Avanti**.

10. In **Assegnazioni** selezionare gli utenti o i gruppi che riceveranno il profilo. Per altre informazioni sull'assegnazione di profili, vedere [Assegnare profili utente e dispositivo](device-profile-assign.md).

    Selezionare **Avanti**.

11. In **Rivedi e crea** rivedere le impostazioni. Quando si seleziona **Crea**, le modifiche vengono salvate e il profilo viene assegnato. Il criterio viene visualizzato anche nell'elenco dei profili.

## <a name="example"></a>Esempio

Nell'esempio seguente l'impostazione **Connectivity/AllowVPNOverCellular** è abilitata. Questa impostazione consente a un dispositivo Windows 10 di aprire una connessione VPN quando si trova in una rete cellulare.

> [!div class="mx-imgBorder"]
> ![Esempio di un criterio personalizzato contenente le impostazioni VPN in Intune ed Endpoint Manager](./media/custom-settings-configure/custom-policy-example.png)

## <a name="next-steps"></a>Passaggi successivi

Il profilo è stato creato, ma potrebbe non essere ancora operativo. [Assegnare il profilo](device-profile-assign.md) e [monitorarne lo stato](device-profile-monitor.md).
