---
title: Limitare le funzionalità dei i dispositivi tramite i criteri in Microsoft Intune - Azure | Microsoft Docs
description: Aggiungere un profilo del dispositivo per limitare le funzionalità dell'amministratore di dispositivi Android e dei dispositivi Android Enterprise, macOS, iOS, iPadOS e Windows 10 in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/11/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: e710678e3ac4775f5737090b791446c7a6e8285c
ms.sourcegitcommit: 8999e197f10fb72d1b82f30a599d1e588db237b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/12/2020
ms.locfileid: "88146355"
---
# <a name="configure-device-restriction-settings-in-microsoft-intune"></a>Configurare le impostazioni relative alle restrizioni dei dispositivi in Microsoft Intune

Intune include criteri di limitazioni dei dispositivi che consentono agli amministratori di controllare i dispositivi Android, iOS/iPadOS, macOS e Windows. Queste limitazioni consentono di controllare una vasta gamma di impostazioni e funzionalità per proteggere le risorse dell'organizzazione. Gli amministratori sono ad esempio in grado di:

- Consente o blocca la fotocamera del dispositivo.
- Controllare l'accesso a Google Play, App Store, visualizzazione di documenti e giochi.
- Bloccare app predefinite o creare un elenco di app consentite o non consentite.
- Consentire o impedire il backup di file nel cloud e negli account di archiviazione.
- Impostare una lunghezza minima per le password e bloccare le password semplici.

Queste funzionalità sono disponibili in Intune e possono essere configurate dall'amministratore. Intune usa "profili di configurazione" per creare e personalizzare queste impostazioni per le esigenze dell'organizzazione. Dopo aver aggiunto queste funzionalità a un profilo, è possibile eseguire il push del profilo o distribuirlo nei dispositivi dell'organizzazione.

Questo articolo illustra come creare un profilo di limitazioni del dispositivo. È anche possibile visualizzare tutte le impostazioni disponibili per le varie piattaforme.

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
        - **Windows 8.1 e versioni successive**

    - **Profilo**: Selezionare **Limitazioni del dispositivo**.

        Per creare un profilo di restrizione per dispositivi Windows 10 Team come Surface Hub, scegliere **Limitazioni del dispositivo (Windows 10 Team)** .

4. Selezionare **Crea**.
5. In **Informazioni di base** immettere le proprietà seguenti:

    - **Nome**: immettere un nome descrittivo per il criterio. Assegnare ai criteri nomi che possano essere identificati facilmente in un secondo momento. Ad esempio, un nome di criterio valido è **iOS/iPadOS: Blocca fotocamera nei dispositivi**.
    - **Descrizione**: immettere una descrizione del criterio. Questa impostazione è facoltativa ma consigliata.

6. Selezionare **Avanti**.

7. In **Impostazioni di configurazione** le impostazioni configurabili variano in base alla piattaforma scelta. Scegliere la piattaforma per le impostazioni dettagliate:

    - [Amministratore di dispositivi Android](device-restrictions-android.md)
    - [Android Enterprise](device-restrictions-android-for-work.md)
    - [iOS/iPadOS](device-restrictions-ios.md)
    - [macOS](device-restrictions-macos.md)
    - [Windows 8.1](device-restrictions-windows-8-1.md)
    - [Windows 10 e versioni successive](device-restrictions-windows-10.md)
    - [Windows 10 Team](device-restrictions-windows-10-teams.md)
    - [Windows Holographic for Business](device-restrictions-windows-holographic.md)

8. Selezionare **Avanti**.
9. In **Tag ambito** (facoltativo) assegnare un tag per filtrare il profilo a gruppi IT specifici, ad esempio `US-NC IT Team` o `JohnGlenn_ITDepartment`. Per altre informazioni sui tag di ambito, vedere [Usare il controllo degli accessi in base al ruolo (RBAC) e i tag di ambito per l'infrastruttura IT distribuita](../fundamentals/scope-tags.md).

    Selezionare **Avanti**.

10. In **Assegnazioni** selezionare gli utenti o i gruppi che riceveranno il profilo. Per altre informazioni sull'assegnazione di profili, vedere [Assegnare profili utente e dispositivo](device-profile-assign.md).

    Selezionare **Avanti**.

11. In **Rivedi e crea** rivedere le impostazioni. Quando si seleziona **Crea**, le modifiche vengono salvate e il profilo viene assegnato. Il criterio viene visualizzato anche nell'elenco dei profili.

## <a name="next-steps"></a>Passaggi successivi

Dopo averlo creato, il profilo è pronto per l'assegnazione. [Assegnare il profilo](device-profile-assign.md) e [monitorarne lo stato](device-profile-monitor.md).

<!--  Removing image as part of design review; retaining source until we known the disposition.

## Example of device restriction settings

In this high-level example, you'll create a device restriction policy that blocks the use of the built-in camera app on Android devices.

![How to disable the camera on Android devices](./media/device-restrictions-configure/disable-android-camera.png)

-->
