---
title: Personalizzare il profilo VPN per singole app per l'amministratore di dispositivi Android in Microsoft Intune - Azure | Microsoft Docs
description: Usare un profilo personalizzato per i profili VPN per singole app per l'amministratore di dispositivi Android con i tipi di connessione Pulse Secure o Citrix VPN in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 07/22/2020
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
ms.openlocfilehash: 3c8e09b6010f7fc846fd81281053eaaa722e5ef4
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/28/2020
ms.locfileid: "87262796"
---
# <a name="use-a-microsoft-intune-custom-profile-to-create-a-per-app-vpn-profile-for-android-devices"></a>Usare un profilo personalizzato di Microsoft Intune per creare un profilo VPN per ogni app per dispositivi Android

È possibile creare un profilo VPN per app specifiche per i dispositivi Android 5.0 e versione successiva gestiti da Intune. Creare prima un profilo VPN che usa il tipo di connessione Pulse Secure o Citrix. Definire quindi criteri di configurazione personalizzati che associano il profilo ad app specifiche.

Questa funzionalità si applica a:

- Amministratore dispositivo Android

Per usare la VPN per singole app nei dispositivi Android Enterprise, usare i [criteri di configurazione dell'app](../apps/app-configuration-vpn-ae.md). I criteri di configurazione dell'app supportano più app client VPN. Nei dispositivi Android Enterprise è possibile seguire la procedura descritta in questo articolo. Tuttavia, non è consigliabile e può essere usata solo con le connessioni Pulse Secure e Citrix VPN.

Dopo aver assegnato i criteri ai gruppi di utenti o ai dispositivi Android, gli utenti devono avviare la VPN Pulse Secure o Citrix. Il client VPN consente quindi il traffico solo dalle app specificate per usare la connessione VPN aperta.

> [!NOTE]
>
> Per l'amministratore di dispositivi Android sono supportati solo i tipi di connessione Pulse Secure e Citrix. Nei dispositivi Android Enterprise usare i [criteri di configurazione dell'app](../apps/app-configuration-vpn-ae.md).

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

    :::image type="content" source="./media/android-pulse-secure-per-app-vpn/android_per_app_vpn_oma_uri.png" alt-text="Criteri personalizzati della VPN per singole app per un amministratore di dispositivi Android":::

### <a name="set-your-blocked-and-allowed-app-list-optional"></a>Impostare l'elenco di app bloccate e consentite (facoltativo)

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
