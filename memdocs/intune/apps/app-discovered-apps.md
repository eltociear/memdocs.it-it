---
title: App individuate
titleSuffix: Microsoft Intune
description: Informazioni dettagliate sulle app individuate da Intune in un dispositivo.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 08/14/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 07dd262f-13e7-4cb2-9cc2-b755d1c276cf
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: 358d01a968c98262980f8e121d8e7e92e2880c6c
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/26/2020
ms.locfileid: "88907820"
---
# <a name="intune-discovered-apps"></a>App individuate da Intune

**App individuate** di Intune è un elenco di app rilevate nei dispositivi registrati in Intune nel tenant dell'utente. Svolge la funzione di inventario software per il tenant. **App individuate** è un report diverso dai report di [installazione delle app](apps-monitor.md). Per i dispositivi personali, Intune non raccoglie mai le informazioni sulle applicazioni non gestite. Nei dispositivi aziendali questo report rileva qualsiasi app, indipendentemente dal fatto che sia un'app gestita. Di seguito è riportata la tabella che mappa il comportamento previsto. In generale il report viene aggiornato ogni 7 giorni dal momento della registrazione (non viene eseguito un aggiornamento settimanale per l'intero tenant). L'unica eccezione a questo periodo di aggiornamento è costituita dalle informazioni sulle applicazioni che vengono raccolte tramite l'estensione di gestione di Intune per le app Win32. Questa raccolta di informazioni avviene ogni 24 ore.

## <a name="monitor-discovered-apps-with-intune"></a>Monitorare le app individuate con Intune

Intune offre un elenco aggregato di app rilevate nei dispositivi registrati in Intune nel tenant dell'utente.

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selezionare **App** > **Monitoraggio** > **App individuate**.

>[!NOTE]
>È possibile esportare l'elenco delle app individuate in un file con estensione csv selezionando **Esporta** nel riquadro **App individuate**.
>
>Per le app Win32 individuate, il conteggio aggregato non è attualmente disponibile. Questo tipo di dati può essere visualizzato solo per singolo dispositivo.

Intune offre anche l'elenco delle app individuate per il singolo dispositivo presente nel tenant.

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selezionare **Dispositivi** > **Tutti i dispositivi**.
3. Selezionare un dispositivo.
4. Per visualizzare le app rilevate per questo dispositivo, selezionare **App individuate** nella sezione **Monitoraggio**.

## <a name="details-of-discovered-apps"></a>Dettagli delle app individuate

L'elenco seguente include il tipo di piattaforma app, le app monitorate per i dispositivi personali, le app monitorate per i dispositivi di proprietà dell'azienda e il ciclo di aggiornamento. Per altre informazioni sui tipi di app supportati da Intune, vedere [Tipi di app in Microsoft Intune](apps-add.md#app-types-in-microsoft-intune).

| Piattaforma | Per i dispositivi di proprietà personale | Per i dispositivi di proprietà dell'azienda | Ciclo di aggiornamento |
|------------------------------------------------------------------------|----------------------------------|--------------------------------------------------|---------------------------------------|
| Nota per le app Windows 10 (app Win32): [Richiede l'estensione di gestione di Intune](intune-management-extension.md) nel dispositivo | Non applicabile | App installate tramite MSI sul dispositivo | Ogni 24 ore dalla registrazione del dispositivo |
| Windows 10 (app moderne) | Solo app moderne gestite | Tutte le app moderne installate nel dispositivo | Ogni 7 giorni dalla registrazione del dispositivo |
| Windows 8.1 | Solo le app gestite | Solo le app gestite | Ogni 7 giorni dalla registrazione del dispositivo |
| Windows RT | Solo le app gestite | Solo le app gestite | Ogni 7 giorni dalla registrazione del dispositivo |
| iOS/iPadOS | Solo le app gestite | Tutte le app installate nel dispositivo | Ogni 7 giorni dalla registrazione del dispositivo |
| macOS | Solo le app gestite | Tutte le app installate nel dispositivo | Ogni 7 giorni dalla registrazione del dispositivo |
| Android | Solo le app gestite | Tutte le app installate nel dispositivo | Ogni 7 giorni dalla registrazione del dispositivo |
| Android Enterprise | Solo le app gestite | Solo le app installate nel profilo di lavoro | Ogni 7 giorni dalla registrazione del dispositivo |

> [!NOTE]
> - I dispositivi Windows 10 con co-gestione, come indicato nel carico di lavoro delle [app client](../../configmgr/comanage/workloads.md#client-apps) in Configuration Manager, attualmente non raccolgono l'inventario delle app con l'estensione di gestione di Intune in base alla pianificazione precedente. Per attenuare questo problema, il carico di lavoro delle [app client](../../configmgr/comanage/workloads.md#client-apps) in Configuration Manager deve passare a Intune per consentire l'installazione dell'estensione di gestione di Intune nel dispositivo. Questa estensione è necessaria per l'inventario di Win32 e la distribuzione di PowerShell. Si noti che eventuali modifiche o aggiornamenti per questo comportamento vengono annunciati in [in fase di sviluppo](../fundamentals/in-development.md) e/o [novità](../fundamentals/whats-new.md).
> - I dispositivi macOS personali registrati prima di novembre 2019 possono continuare a mostrare tutte le app installate nel dispositivo fino a quando i dispositivi non vengono registrati nuovamente.
> - Android Enterprise completamente gestito e dedicato non visualizza le app individuate.

Il numero di app individuate potrebbe non corrispondere al conteggio degli stati di installazione delle app. Le possibilità delle incoerenze includono:

- Una modifica di destinazione di un'app gestita installata può far sì che il conteggio delle installazioni nel riquadro di stato diminuisca, mentre rimane segnalato nelle app individuate.
- Più istanze di destinazione della stessa app in un tenant comporterà conteggi diversi a causa della potenziale sovrapposizione di utenti o dispositivi. Ogni istanza dell'app includerà nel conteggio utenti sovrapposti, mentre le app individuate avranno conteggi duplicati.
- Le app individuate e lo stato delle app vengono raccolti con intervalli di tempo diversi causando una discrepanza nei conteggi delle app.

## <a name="next-steps"></a>Passaggi successivi

- [Tipi di app in Microsoft Intune](apps-add.md#app-types-in-microsoft-intune)
- [Monitorare le informazioni sulle app e le assegnazioni con Microsoft Intune](apps-monitor.md)