---
title: Personalizzare il profilo VPN per app per Android in Microsoft Intune - Azure | Microsoft Docs
description: Informazioni su come creare un profilo VPN per app specifiche per i dispositivi amministratore di dispositivi Android gestiti da Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/19/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: d035ebf5-85f4-4001-a249-75d24325061a
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: a351255fa0574e9b92d096b3895f9469ed9ced2a
ms.sourcegitcommit: 678104677ad36b789630befdc5e0f1efc572c14b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/08/2020
ms.locfileid: "86137374"
---
# <a name="use-a-microsoft-intune-custom-profile-to-create-a-per-app-vpn-profile-for-android-devices"></a>Usare un profilo personalizzato di Microsoft Intune per creare un profilo VPN per ogni app per dispositivi Android

È possibile creare un profilo VPN per app specifiche per i dispositivi Android 5.0 e versione successiva gestiti da Intune. Creare prima un profilo VPN che usa il tipo di connessione Pulse Secure o Citrix. Definire quindi criteri di configurazione personalizzati che associano il profilo ad app specifiche.

> [!NOTE]
> Per usare la VPN per app nei dispositivi Android Enterprise, è anche possibile seguire questi passaggi. È tuttavia consigliabile usare i [criteri di configurazione dell'app](../apps/app-configuration-vpn-ae.md) per l'app client VPN.

Dopo aver assegnato i criteri ai gruppi di utenti o ai dispositivi Android, gli utenti devono avviare la VPN Pulse Secure o Citrix. Il client VPN consente quindi il traffico solo dalle app specificate per usare la connessione VPN aperta.

> [!NOTE]
>
> Per questo profilo sono supportati solo i tipi di connessione Pulse Secure e Citrix.

## <a name="step-1-create-a-vpn-profile"></a>Passaggio 1: Creare un profilo VPN

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selezionare **Dispositivi** > **Profili di configurazione** > **Crea profilo**.
3. Immettere le proprietà seguenti:

    - **Piattaforma**: Selezionare **Amministratore di dispositivi Android**.
    - **Profilo**: selezionare **VPN**.

4. Selezionare **Crea**.
5. In **Informazioni di base** immettere le proprietà seguenti:

    - **Nome**: immettere un nome descrittivo per il profilo. Assegnare ai profili nomi che possano essere identificati facilmente in un secondo momento. Ad esempio, un buon nome di profilo è **Profilo VPN amministratore di dispositivi Android per app per l'intera azienda**.
    - **Descrizione**: Immettere una descrizione del profilo. Questa impostazione è facoltativa ma consigliata.

6. Selezionare **Avanti**.
7. In **Impostazioni di configurazione** configurare le impostazioni del profilo:

    - [Impostazioni VPN per i dispositivi amministratore di dispositivi Android](vpn-settings-android.md).

    Prendere nota del valore **Nome connessione** specificato quando si crea il profilo VPN. Questo nome sarà necessario nel passaggio successivo. In questo esempio il nome della connessione è **MyAppVpnProfile**.

8. Selezionare **Avanti** e continuare a creare il profilo. Per altre informazioni, vedere [Creare profili VPN](vpn-settings-configure.md#create-the-profile).

## <a name="step-2-create-a-custom-configuration-policy"></a>Passaggio 2: Creare criteri di configurazione personalizzati

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selezionare **Dispositivi** > **Profili di configurazione** > **Crea profilo**.
3. Immettere le proprietà seguenti:

    - **Nome**: Immettere un nome descrittivo per il profilo personalizzato. Assegnare ai profili nomi che possano essere identificati facilmente in un secondo momento. Ad esempio un buon nome di profilo è **Profilo VPN Android OMA-URI personalizzato per l'intera azienda**.
    - **Descrizione**: Immettere una descrizione del profilo. Questa impostazione è facoltativa ma consigliata.
    - **Piattaforma**: Selezionare **Amministratore di dispositivi Android**.
    - **Tipo di profilo**: Selezionare **Personalizzato**.

4. Scegliere **Impostazioni** > **Configura**.
5. Nel riquadro **Impostazioni OMA-URI personalizzate** scegliere **Aggiungi**.
    - **Nome**: Immettere un nome per l'impostazione.
    - **Descrizione**: Immettere una descrizione del profilo. Questa impostazione è facoltativa ma consigliata.
    - **OMA-URI**: Immettere `./Vendor/MSFT/VPN/Profile/*Name*/PackageList` dove *Name* è il nome della connessione annotato nel passaggio 1. In questo esempio la stringa è `./Vendor/MSFT/VPN/Profile/MyAppVpnProfile/PackageList`.
    - **Tipo di dati**: Immettere **String**.
    - **Valore**: Immettere un elenco separato da punti e virgola dei pacchetti da associare al profilo. Se ad esempio si vuole che Excel e il browser Google Chrome usino la connessione VPN, immettere `com.microsoft.office.excel;com.android.chrome`.

    > [!div class="mx-imgBorder"]
    >![Esempio di criterio personalizzato della VPN per app di amministratore di dispositivi Android](./media/android-pulse-secure-per-app-vpn/android_per_app_vpn_oma_uri.png)

### <a name="set-your-app-list-to-blacklist-or-whitelist-optional"></a>Impostare l'elenco di app come blacklist o whitelist (facoltativo)

Usare il valore *BLACKLIST* per specificare un elenco di app che **non possono** usare la connessione VPN. Tutte le altre app si connettono mediante la VPN. Oppure usare il valore **WHITELIST** per specificare un elenco di app che *possono* usare la connessione VPN. Le app non incluse nell'elenco non si connettono tramite la VPN.

1. Nel riquadro **Impostazioni OMA-URI personalizzate** scegliere **Aggiungi**.
2. Immettere un nome per l'impostazione.
3. In **OMA-URI** immettere `./Vendor/MSFT/VPN/Profile/*Name*/Mode` dove *Name* è il nome del profilo VPN annotato nel passaggio 1. In questo esempio la stringa è `./Vendor/MSFT/VPN/Profile/MyAppVpnProfile/Mode`.
4. In **Tipo di dati** immettere **String**.
5. In **Valore** immettere **BLACKLIST** o **WHITELIST**.

## <a name="step-3-assign-both-policies"></a>Passaggio 3: Assegnare entrambi i criteri

[Assegnare entrambi i profili di dispositivo](device-profile-assign.md) agli utenti o ai dispositivi appropriati.

## <a name="next-steps"></a>Passaggi successivi

- Per un elenco di tutte le impostazioni VPN di amministratore di dispositivi Android, vedere [Impostazioni dei dispositivi Android per configurare la VPN](vpn-settings-android.md).
- Per altre informazioni sulle impostazioni VPN e Intune, vedere [Creare profili VPN per la connessione ai server VPN in Intune](vpn-settings-configure.md).
