---
title: Trovare un nome di famiglia di pacchetti (PFN) per una rete VPN per app
titleSuffix: Configuration Manager
description: Informazioni sulle due modalità di reperimento di un nome di famiglia di pacchetti in modo che sia possibile configurare una rete VPN per app.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 47118499-3d26-4c25-bfde-b129de7eaa59
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f109e4ea4bee4a1de767508d62bc3f080d24f625
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697119"
---
# <a name="find-a-package-family-name-pfn-for-per-app-vpn"></a>Trovare un nome di famiglia di pacchetti (PFN) per una rete VPN per app

*Si applica a: Configuration Manager (Current Branch)*


Esistono due modi per trovare un PFN in modo tale da poter configurare una rete VPN per app.

## <a name="find-a-pfn-for-an-app-thats-installed-on-a-windows-10-computer"></a>Trovare un PFN per un'applicazione installata in un computer Windows 10

Se l'applicazione in uso è già installata in un computer Windows 10, è possibile usare il cmdlet [Get-AppxPackage](https://technet.microsoft.com/library/hh856044.aspx) di PowerShell per recuperare il PFN.

La sintassi per Get-AppxPackage è:

``` Syntax
Get-AppxPackage [[-Name] <String> ] [[-Publisher] <String> ] [-AllUsers] [-User <String> ] [ <CommonParameters>]
```

> [!NOTE]
> Può essere necessario eseguire PowerShell come amministratore per poter recuperare il PFN

Ad esempio, per ottenere informazioni su tutte le app universali installate nel computer usare `Get-AppxPackage`.

Per ottenere informazioni su un'applicazione di cui si conosce il nome, o parte del nome, usare `Get-AppxPackage *<app_name>`. Si noti l'utilizzo del carattere jolly, particolarmente utile se non si è certi del nome completo dell'applicazione. Ad esempio, per ottenere le informazioni per OneNote, usare `Get-AppxPackage *OneNote`.


Queste sono le informazioni recuperate per OneNote:

`Name                   : Microsoft.Office.OneNote`

`Publisher              : CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US`

`Architecture           : X64`

`ResourceId             :`

`Version                : 17.6769.57631.0`

`PackageFullName        : Microsoft.Office.OneNote_17.6769.57631.0_x64__8wekyb3d8bbwe`

`InstallLocation        : C:\Program Files\WindowsApps`

`\Microsoft.Office.OneNote_17.6769.57631.0_x64__8wekyb3d8bbwe`

`IsFramework            : False`

**`PackageFamilyName      : Microsoft.Office.OneNote_8wekyb3d8bbwe`**

`PublisherId            : 8wekyb3d8bbwe`



## <a name="find-a-pfn-if-the-app-is-not-installed-on-a-computer"></a>Trovare un PFN se l'applicazione non è installata in un computer

1. Passare a https://www.microsoft.com/store/apps
2. Immettere il nome dell'applicazione nella barra di ricerca. Nel nostro esempio cercare OneNote.
3. Fare clic sul collegamento all'applicazione. Si noti che l'URL a cui si accede ha una serie di lettere alla fine. Nel nostro esempio l'URL è simile al seguente: `https://www.microsoft.com/store/apps/onenote/9wzdncrfhvjl`
4. In un'altra scheda incollare l'URL seguente, `https://bspmts.mp.microsoft.com/v1/public/catalog/Retail/Products/<app id>/applockerdata`, sostituendo `<app id>` con l'ID dell'app ottenuto da https://www.microsoft.com/store/apps, la serie di lettere alla fine dell'URL nel passaggio 3. Nel nostro esempio con OneNote si deve incollare: `https://bspmts.mp.microsoft.com/v1/public/catalog/Retail/Products/9wzdncrfhvjl/applockerdata`.

In Microsoft Edge le informazioni richieste vengono visualizzate, in Internet Explorer fare clic su **Apri** per visualizzare le informazioni. Il valore PFN è indicato sulla prima riga. Ecco come appaiono i risultati di questo esempio:

``` JSON
{
  "packageFamilyName": "Microsoft.Office.OneNote_8wekyb3d8bbwe",
  "packageIdentityName": "Microsoft.Office.OneNote",
  "windowsPhoneLegacyId": "ca05b3ab-f157-450c-8c49-a1f127f5e71d",
  "publisherCertificateName": "CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US"
}
```
