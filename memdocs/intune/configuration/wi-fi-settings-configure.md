---
title: Creare un profilo Wi-Fi per i dispositivi in Microsoft Intune - Azure | Microsoft Docs
description: Vedere la procedura per creare un profilo di configurazione Wi-Fi per i dispositivi in Microsoft Intune. Creare profili per Amministratore di dispositivi Android, Android Enterprise, Android in modalità tutto schermo, iOS, iPadOS, macOS, Windows 10 e versioni successive e Windows Holographic for Business. Usare questi profili per creare una connessione Wi-Fi per usare i certificati, scegliere un tipo EAP, selezionare un metodo di autenticazione, abilitare un proxy e altro ancora.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/19/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: maholdaa
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d1ff20db13a87faea41d262da5742a428ec4d28f
ms.sourcegitcommit: b7e5b053dfa260e7383a9744558d50245f2bccdc
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/29/2020
ms.locfileid: "82587297"
---
# <a name="add-and-use-wi-fi-settings-on-your-devices-in-microsoft-intune"></a>Aggiungere e usare le impostazioni Wi-Fi nei dispositivi in Microsoft Intune

Il Wi-Fi è una rete wireless usata da molti dispositivi mobili per ottenere accesso alla rete. Microsoft Intune include delle impostazioni Wi-Fi predefinite che possono essere distribuite agli utenti e ai dispositivi dell'organizzazione. Questo gruppo di impostazioni è denominato "profilo" e può essere assegnato a diversi utenti e gruppi. Quando viene assegnato, gli utenti ottengono l'accesso alla rete Wi-Fi dell'organizzazione senza configurarla autonomamente.

Si supponga, ad esempio, di installare una nuova rete Wi-Fi denominata Contoso Wi-Fi. Si vogliono quindi configurare tutti i dispositivi iOS/iPadOS per la connessione a questa rete. Questa è la procedura:

1. Creare un profilo Wi-Fi contenente le impostazioni per connettersi alla rete wireless Contoso Wi-Fi.
2. Assegnare il profilo a un gruppo contenente tutti gli utenti dei dispositivi iOS/iPadOS.
3. Nell'elenco delle reti wireless nel dispositivo gli utenti visualizzeranno la nuova rete Contoso Wi-Fi. Gli utenti potranno quindi connettersi alla rete usando il metodo di autenticazione scelto.

Questo articolo illustra la procedura per creare un profilo Wi-Fi e include i collegamenti che descrivono le diverse impostazioni per ogni piattaforma.

## <a name="supported-device-platforms"></a>Piattaforme per dispositivi supportate

I profili Wi-Fi supportano le piattaforme per dispositivi seguenti:

- Android 4 e versioni successive
- Android Enterprise e modalità tutto schermo
- iOS 8.0 e versioni successive
- iPadOS 13.0 e versioni successive
- macOS X 10.11 e versioni successive
- Windows 10 e versioni successive, Windows 10 Mobile e Windows Holographic for Business

> [!NOTE]
> Per i dispositivi che eseguono Windows 8.1, è possibile importare una configurazione Wi-Fi precedentemente esportata da un altro dispositivo.

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

    - **Profilo**: selezionare **Wi-Fi**.

      > [!TIP]
      >
      > - Per i dispositivi **Android Enterprise** eseguiti come dispositivi dedicati (modalità a tutto schermo) scegliere **Solo proprietario del dispositivo** > **Wi-Fi**.
      > - Per **Windows 8.1 e versioni successive** è possibile scegliere **Wi-Fi per importazione**. Questa opzione consente di importare le impostazioni Wi-Fi come un file XML precedentemente esportato da un altro dispositivo.

4. Selezionare **Crea**.
5. In **Informazioni di base** immettere le proprietà seguenti:

    - **Nome**: immettere un nome descrittivo per il profilo. Assegnare ai profili nomi che possano essere identificati facilmente in un secondo momento. Ad esempio, un buon nome di profilo è **Profilo WiFi per l'intera azienda**.
    - **Descrizione**: Immettere una descrizione del profilo. Questa impostazione è facoltativa ma consigliata.

6. Selezionare **Avanti**.
7. In **Impostazioni di configurazione** le impostazioni configurabili variano in base alla piattaforma scelta. Per impostazioni dettagliate, scegliere la piattaforma:

    - [Amministratore di dispositivi Android](wi-fi-settings-android.md)
    - [Android Enterprise](wi-fi-settings-android-enterprise.md), inclusi i dispositivi dedicati
    - [iOS/iPadOS](wi-fi-settings-ios.md)
    - [macOS](wi-fi-settings-macos.md)
    - [Windows 10 e versioni successive](wi-fi-settings-windows.md)
    - [Windows 8.1 e versioni successive](wi-fi-settings-import-windows-8-1.md), incluso Windows Holographic for Business

8. Selezionare **Avanti**.
9. In **Tag ambito** (facoltativo) assegnare un tag per filtrare il profilo a gruppi IT specifici, ad esempio `US-NC IT Team` o `JohnGlenn_ITDepartment`. Per altre informazioni sui tag di ambito, vedere [Usare il controllo degli accessi in base al ruolo (RBAC) e i tag di ambito per l'infrastruttura IT distribuita](../fundamentals/scope-tags.md).

    Selezionare **Avanti**.

10. In **Assegnazioni** selezionare l'utente o i gruppi che riceveranno il profilo. Per altre informazioni sull'assegnazione di profili, vedere [Assegnare profili utente e dispositivo](device-profile-assign.md).

    Selezionare **Avanti**.

11. In **Rivedi e crea** rivedere le impostazioni. Quando si seleziona **Crea**, le modifiche vengono salvate e il profilo viene assegnato. Il criterio viene visualizzato anche nell'elenco dei profili.

> [!TIP]
> Se si usa l'autenticazione basata su certificati per il profilo Wi-Fi, distribuire il profilo Wi-Fi, il profilo certificato e il profilo radice attendibile agli stessi gruppi per assicurarsi che ogni dispositivo sia in grado di riconoscere la legittimità dell'autorità di certificazione.  Per altre informazioni, vedere [Come configurare i certificati con Microsoft Intune](../protect/certificates-configure.md).


## <a name="next-steps"></a>Passaggi successivi

Il profilo viene creato, ma non è ancora operativo. [Assegnare il profilo](device-profile-assign.md) e [monitorarne lo stato](device-profile-monitor.md).

[Problemi dei profili Wi-Fi in Intune](troubleshoot-wi-fi-profiles.md).
