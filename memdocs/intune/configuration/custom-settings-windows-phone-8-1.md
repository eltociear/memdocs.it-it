---
title: Aggiungere impostazioni personalizzate ai dispositivi Windows Phone 8.1 in Microsoft Intune - Azure | Microsoft Docs
titleSuffix: ''
description: Aggiungere o creare un profilo personalizzato per usare le impostazioni OMA-URI per i dispositivi che eseguono Windows Phone 8.1 in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ce8433ee87c0f5e4b397003b78c0ceb751eb46b7
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556269"
---
# <a name="use-custom-settings-for-windows-phone-81-devices-in-intune"></a>Usare le impostazioni personalizzate per i dispositivi Windows Phone 8.1 in Intune

Con Microsoft Intune è possibile aggiungere o creare impostazioni personalizzate per i dispositivi Windows Phone 8.1 usando i "profili personalizzati". I profili personalizzati sono una funzionalità di Intune. Sono progettati per aggiungere impostazioni dei dispositivi e funzionalità non incluse in Intune.

I profili personalizzati Windows Phone 8.1 usano impostazioni Open Mobile Alliance Uniform Resource Identifier (OMA-URI) per configurare funzionalità diverse. Tali impostazioni vengono in genere usate dai produttori di dispositivi mobili per controllare le funzionalità del dispositivo. Le impostazioni sono elencate nella [documentazione del protocollo MDM di Windows Phone 8.1](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-phone/dn499787(v=technet.10)).

Questo articolo descrive come creare un profilo personalizzato per i dispositivi Windows Phone 8.1. 

## <a name="before-you-begin"></a>Prima di iniziare

[Creare un profilo personalizzato Windows Phone 8.1](custom-settings-configure.md).

## <a name="custom-oma-uri-settings"></a>Impostazioni OMA-URI personalizzate

- **Impostazioni OMA-URI**: **Aggiungere** le seguenti impostazioni:

  - **Nome**: Immettere un nome univoco per l'impostazione OMA URI per identificarla nell'elenco delle impostazioni.
  - **Descrizione**: immettere una descrizione che offra una panoramica dell'impostazione e altre informazioni rilevanti per individuare il profilo.
  - **OMA-URI (maiuscole/minuscole)** : immettere l'OMA-URI da usare come impostazione.
  - **Tipo di dati**: selezionare il tipo di dati da usare per questa impostazione OMA-URI. Le opzioni disponibili sono:

    - Stringa
    - Stringa (file XML)
    - Data e ora
    - Intero
    - A virgola mobile
    - Boolean
    - Base64 (file)

  - **Valore**: immettere il valore dati da associare all'impostazione OMA-URI immessa. Il valore varia a seconda del tipo di dati selezionato. Ad esempio, se si seleziona **Data e ora**, selezionare il valore dalla selezione data.

  Dopo aver aggiunto alcune impostazioni, è possibile selezionare **Esporta**. **Esporta** crea un elenco di tutti i valori aggiunti in un file con valori delimitati da virgole (file con estensione csv).

## <a name="example"></a>Esempio

Nell'esempio seguente si impedisce ai dispositivi telefonici Windows 8.1 di cambiare rete cellulare quando si spostano all'esterno dell'area di copertura del gestore telefonico.

- **Nome**: Consenti rete dati durante il roaming
- **Descrizione**: consente o impedisce l'uso della rete dati durante il roaming
- **OMA-URI** (con distinzione di maiuscole e minuscole): ./Vendor/MSFT/PolicyManager/My/Connectivity/AllowCellularDataRoaming
- **Tipo di dati**: Intero
- **Valore**: 0

## <a name="next-steps"></a>Passaggi successivi

[Assegnare il profilo](device-profile-assign.md) e [monitorarne lo stato](device-profile-monitor.md).

Creare un [profilo personalizzato nei dispositivi Windows 10](custom-settings-windows-10.md).
