---
title: Configurare le impostazioni della rete cablata 802.1x per dispositivi macOS in Microsoft Intune - Azure | Microsoft Docs
titleSuffix: ''
description: Creare o aggiungere un profilo di configurazione della rete cablata per i dispositivi computer desktop macOS. Vedere le diverse impostazioni, aggiungere certificati, scegliere un tipo EAP e selezionare un metodo di autenticazione in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/11/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f237daa5e95cb5428e707828f0104c697e338718
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/19/2020
ms.locfileid: "85095768"
---
# <a name="add-and-use-wired-networks-settings-on-your-macos-devices-in-microsoft-intune"></a>Aggiungere e usare le impostazioni delle reti cablate nei dispositivi macOS in Microsoft Intune

Le reti cablate vengono usate da molte organizzazioni per concedere l'accesso alla rete ai computer desktop. Microsoft Intune include impostazioni predefinite che possono essere distribuite agli utenti e ai dispositivi macOS dell'organizzazione. Questo gruppo di impostazioni è noto come "profilo". Nel profilo è possibile includere impostazioni comuni, ad esempio l'interfaccia di rete, i tipi EAP accettati e le impostazioni di attendibilità del server.

Quando il profilo è pronto, può essere assegnato a utenti e gruppi diversi. Quando viene assegnato, gli utenti ottengono l'accesso alla rete cablata dell'organizzazione senza doverla configurare autonomamente.

Come parte della soluzione di gestione dei dispositivi mobili (MDM), usare questa funzionalità per creare profili 802.1x per gestire le reti cablate. Distribuire quindi le reti cablate nei dispositivi macOS.

Questa funzionalità si applica a:

- macOS

Si supponga, ad esempio, di avere una rete cablata denominata **Rete cablata Contoso**. Si vogliono configurare tutti i desktop macOS per la connessione a questa rete. Questa è la procedura:

1. Creare un profilo di rete cablata contenente le impostazioni per connettersi a **Rete cablata Contoso**.
2. Assegnare il profilo a un gruppo che include tutti i computer desktop macOS degli utenti. Per consigli sull'uso dei tipi di gruppo, vedere [Gruppi di utenti e gruppi di dispositivi](device-profile-assign.md#user-groups-vs-device-groups).
3. Sui loro desktop, gli utenti trovano **Rete cablata Contoso** nell'elenco delle reti. Gli utenti potranno quindi connettersi alla rete usando il metodo di autenticazione scelto.

Questo articolo illustra la procedura per creare un profilo di rete cablata. Include anche un collegamento che descrive le diverse impostazioni.

## <a name="create-the-profile"></a>Creare il profilo

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selezionare **Dispositivi** > **Profili di configurazione** > **Crea profilo**.
3. Immettere le proprietà seguenti:

    - **Piattaforma**: Selezionare **macOS**.
    - **Profilo**: Selezionare **Rete cablata**.

4. Selezionare **Crea**.
5. In **Informazioni di base** immettere le proprietà seguenti:

    - **Nome**: immettere un nome descrittivo per il profilo. Assegnare ai profili nomi che possano essere identificati facilmente in un secondo momento. Un nome di profilo valido, ad esempio, è **Profilo di rete cablata per l'intera azienda nei dispositivi macOS**.
    - **Descrizione**: Immettere una descrizione del profilo. Questa impostazione è facoltativa ma consigliata.

6. Selezionare **Avanti**.
7. In **Impostazioni di configurazione** selezionare l'interfaccia di rete della rete e scegliere il tipo EAP (Extensible Authentication Protocol). Per un elenco di tutte le impostazioni e delle operazioni corrispondenti, vedere:

    - [macOS](wired-network-settings-macos.md)

8. Selezionare **Avanti**.
9. In **Assegnazioni** selezionare i gruppi di utenti o di dispositivi che riceveranno il profilo. Per altre informazioni sull'assegnazione di profili, vedere [Assegnare profili utente e dispositivo](device-profile-assign.md).

    Selezionare **Avanti**.

10. In **Rivedi e crea** rivedere le impostazioni. Quando si seleziona **Crea**, le modifiche vengono salvate e il profilo viene assegnato. Il criterio viene visualizzato anche nell'elenco dei profili.

> [!TIP]
> Se si usa l'autenticazione basata su certificati per il profilo di rete cablata, è necessario distribuire il profilo di rete cablata, il profilo certificato e il profilo radice attendibile agli stessi gruppi. Questa distribuzione assicura che ogni dispositivo possa riconoscere la legittimità dell'autorità di certificazione. Per altre informazioni, vedere [Configurare i certificati con Microsoft Intune](../protect/certificates-configure.md).

## <a name="next-steps"></a>Passaggi successivi

Il profilo è stato creato, ma potrebbe non essere operativo. Assicurarsi di [assegnare questo profilo](device-profile-assign.md) e di [monitorarne lo stato](device-profile-monitor.md).
