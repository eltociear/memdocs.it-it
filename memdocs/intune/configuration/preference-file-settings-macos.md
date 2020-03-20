---
title: Aggiungere le impostazioni di file delle preferenze per dispositivi macOS in Microsoft Intune - Azure | Microsoft Docs
titleSuffix: ''
description: Aggiungere un file con estensione xml o plist che includa le informazioni chiave sull'app. Usare un profilo di configurazione del dispositivo con file delle preferenze per modificare le informazioni chiave nel file di elenco delle proprietà e assegnarlo ai dispositivi macOS.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/09/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d226888c3d710a7b80357ebb92130b34ab2fef94
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79360756"
---
# <a name="add-a-property-list-file-to-macos-devices-using-microsoft-intune"></a>Aggiungere un file di elenco delle proprietà ai dispositivi macOS usando Microsoft Intune

Usando Microsoft Intune, è possibile aggiungere un file di elenco delle proprietà (con estensione plist) per i dispositivi macOS o per le app sui dispositivi macOS.

Questa funzionalità si applica a:

- Dispositivi macOS che eseguono la versione 10.7 e successive

I file di elenco delle proprietà includono in genere informazioni sulle applicazioni macOS. Per altre informazioni, vedere [About Information Property List Files](https://developer.apple.com/library/archive/documentation/General/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html) (Informazioni sui file di elenco delle proprietà - Sito Web di Apple) e [Impostazioni payload personalizzate](https://support.apple.com/guide/mdm/custom-mdm9abbdbe7/1/web/1).

Questo articolo descrive le diverse impostazioni del file di elenco delle proprietà che è possibile aggiungere ai dispositivi macOS. Usare queste impostazioni nella propria soluzione di gestione di dispositivi mobili (MDM) per aggiungere l'ID aggregazione dell'app (`com.company.application`) e aggiungere il file con estensione plist.

Queste impostazioni vengono aggiunte a un profilo di configurazione del dispositivo in Intune e quindi assegnate o distribuite ai dispositivi macOS.

## <a name="before-you-begin"></a>Prima di iniziare

[Creare il profilo](device-profile-create.md).

## <a name="what-you-need-to-know"></a>Informazioni importanti

- Queste impostazioni non vengono convalidate. Assicurarsi di testare le modifiche prima di assegnare il profilo ai dispositivi.
- Se non si è certi di come immettere una chiave dell'app, modificare l'impostazione all'interno dell'app. Esaminare quindi il file delle preferenze dell'app usando [Xcode](https://developer.apple.com/xcode/) per verificare come è configurata l'impostazione. Apple consiglia di rimuovere le impostazioni non gestibili usando Xcode prima di importare il file.
- Solo alcune app utilizzano le preferenze gestite e potrebbero non consentire la gestione di tutte le impostazioni.
- Assicurarsi di caricare i file di elenco delle proprietà che hanno come destinazione le impostazioni dei canali del dispositivo e non le impostazioni dei canali degli utenti. I file dell'elenco delle proprietà hanno come destinazione l'intero dispositivo.

## <a name="preference-file"></a>File delle preferenze

- **Preferenza per il nome di dominio**: i file di elenco delle proprietà in genere sono usati per Web browser (Microsoft Edge), [Microsoft Defender Advanced Threat Protection](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) e app personalizzate. Quando si crea una preferenza per il dominio, viene creato anche un ID di aggregazione. Immettere l'ID di aggregazione, ad esempio `com.company.application`. Ad esempio, immettere `com.Contoso.applicationName`, `com.Microsoft.Edge` o `com.microsoft.wdav`.
- **File di elenco proprietà**: selezionare il file di elenco delle proprietà associato all'app. Assicurarsi che sia un file `.plist` o `.xml`. Caricare, ad esempio, un file `YourApp-Manifest.plist` o `YourApp-Manifest.xml`.
- **Contenuti del file**: vengono visualizzate le informazioni sulla chiave nel file di elenco delle proprietà. Se è necessario modificare le informazioni sulla chiave, aprire il file di elenco in un altro editor e quindi caricare nuovamente il file in Intune.

Verificare che il file sia formattato correttamente. Il file deve contenere solo coppie chiave valore e non deve essere racchiuso tra i tag `<dict>`, `<plist>` o `<xml>`. Il file di elenco delle proprietà, ad esempio, sarà simile al seguente:

```xml
<key>SomeKey</key>
<string>someString</string>
<key>AnotherKey</key>
<false/>
...
```

Selezionare **OK** > **Crea** per salvare le modifiche. Il profilo verrà creato e visualizzato nell'elenco dei profili.

## <a name="next-steps"></a>Passaggi successivi

Il profilo è stato creato, ma non è ancora operativo. [Assegnare il profilo](device-profile-assign.md) e [monitorarne lo stato](device-profile-monitor.md).

Per altre informazioni sui file delle preferenze per Microsoft Edge, vedere [Configurare le impostazioni dei criteri di Microsoft Edge per macOS](https://docs.microsoft.com/deployedge/configure-microsoft-edge-on-mac).
