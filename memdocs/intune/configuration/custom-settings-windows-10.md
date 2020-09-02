---
title: Aggiungere le impostazioni personalizzate per dispositivi Windows 10 in Microsoft Intune - Azure | Microsoft Docs
description: Aggiungere o creare un profilo personalizzato per usare le impostazioni OMA-URI per i dispositivi che eseguono Windows 10 in Microsoft Intune. Usare un profilo personalizzato per aggiungere le impostazioni personalizzate.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 28a867c735a05cfa4a4765534d200b806711f9b5
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/26/2020
ms.locfileid: "88913019"
---
# <a name="use-custom-settings-for-windows-10-devices-in-intune"></a>Usare le impostazioni personalizzate per dispositivi Windows 10 in Intune

Questo articolo descrive le diverse impostazioni personalizzate che è possibile controllare nei dispositivi Windows 10 e versioni successive. Usare queste impostazioni nella propria soluzione di gestione di dispositivi mobili (MDM) per configurare le impostazioni che non sono predefinite in Intune.

Per altre informazioni sui profili personalizzati vedere [Creare un profilo con impostazioni personalizzate](custom-settings-configure.md).

Queste impostazioni vengono aggiunte a un profilo di configurazione del dispositivo in Intune e quindi assegnate o distribuite ai dispositivi Windows 10.

Questa funzionalità si applica a:

- Windows 10 e versioni successive

I profili personalizzati Windows 10 usano impostazioni Open Mobile Alliance Uniform Resource Identifier (OMA-URI) per configurare funzionalità diverse. Tali impostazioni vengono in genere usate dai produttori di dispositivi mobili per controllare le funzionalità del dispositivo.

Windows 10 rende disponibili molte impostazioni CSP (Configuration Service Provider, provider di servizi di configurazione), ad esempio il [provider di servizi di configurazione dei criteri](/windows/configuration/provisioning-packages/how-it-pros-can-use-configuration-service-providers).

Se si sta cercando una determinata impostazione, tenere presente che il [profilo di restrizione del dispositivo Windows 10](device-restrictions-windows-10.md) contiene numerose impostazioni predefinite. Pertanto, potrebbe non essere necessario immettere valori personalizzati.

## <a name="before-you-begin"></a>Prima di iniziare

[Creare un profilo personalizzato di Windows 10](custom-settings-configure.md#create-the-profile).

## <a name="oma-uri-settings"></a>Impostazioni URI OMA

**Aggiungi**: Immettere le impostazioni seguenti:

- **Nome**: Immettere un nome univoco per l'impostazione OMA URI per identificarla nell'elenco delle impostazioni.
- **Descrizione**: immettere una descrizione che offra una panoramica dell'impostazione e altri dettagli importanti.
- **OMA-URI (maiuscole/minuscole)** : immettere l'OMA-URI da usare come impostazione.
- **Tipo di dati**: selezionare il tipo di dati da usare per questa impostazione OMA-URI. Le opzioni disponibili sono:

  - Base64 (file)
  - Boolean
  - Stringa (file XML)
  - Data e ora
  - Stringa
  - A virgola mobile
  - Intero

- **Valore**: immettere il valore dati da associare all'impostazione OMA-URI immessa. Il valore varia a seconda del tipo di dati selezionato. Ad esempio, se si seleziona **Data e ora**, selezionare il valore dalla selezione data.

Dopo aver aggiunto alcune impostazioni, è possibile selezionare **Esporta**. **Esporta** crea un elenco di tutti i valori aggiunti in un file con valori delimitati da virgole (file con estensione csv).

## <a name="find-the-policies-you-can-configure"></a>Individuare i criteri che è possibile configurare

Un elenco completo di tutti i provider di servizi di configurazione (CSP) supportati da Windows 10 è disponibile in [Configuration service provider reference](/windows/client-management/mdm/configuration-service-provider-reference) (Informazioni di riferimento sui provider di servizi di configurazione).

Non tutte le impostazioni sono compatibili con tutte le versioni di Windows 10. In [Configuration service provider reference](/windows/client-management/mdm/configuration-service-provider-reference) (Informazioni di riferimento sui provider di servizi di configurazione) sono indicate le versioni supportate per ogni provider CSP.

Inoltre, Intune non supporta tutte le impostazioni elencate in [Configuration service provider reference](/windows/client-management/mdm/configuration-service-provider-reference) (Informazioni di riferimento sui provider di servizi di configurazione). Per verificare se Intune supporta l'impostazione desiderata, aprire l'articolo relativo all'impostazione. La pagina di ogni impostazione mostra le operazioni supportate. Per usare Intune, l'impostazione deve supportare le operazioni **Add** o **Replace** e **Get**. Se il valore restituito dall'operazione **Get** non corrisponde al valore fornito dalle operazioni **Add** o **Replace**, Intune segnala un errore di conformità.

## <a name="next-steps"></a>Passaggi successivi

[Assegnare il profilo](device-profile-assign.md) e [monitorarne lo stato](device-profile-monitor.md).

[Altre informazioni sui profili personalizzati in Intune](custom-settings-configure.md).