---
title: includere il file
description: Includere file
author: ErikjeMS
ms.service: microsoft-intune
ms.topic: include
ms.date: 06/02/2020
ms.author: erikje
ms.custom: include file
ms.openlocfilehash: bc8bb79d4f950edc303fb12504ef1a4a8dda9a64
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347255"
---
## <a name="apple-device-network-information"></a>Informazioni di rete dei dispositivi Apple

|**Uso**|**Nome host (indirizzo IP/subnet)**|**Protocollo**|**Porta**|
|------------|-----------|------------|-----------|
|Recupero e visualizzazione di contenuto dai server Apple|itunes.apple.com<br>\*.itunes.apple.com<br>\*.mzstatic.com<br>\*.phobos.apple.com<br>\*.phobos.itunes-apple.com.akadns.net|HTTP|80|
|Comunicazioni con i server APNS|#-courier.push.apple.com<br>'#' è un numero casuale compreso tra 0 e 50.|TCP|5223 e 443|
|Varie funzionalità tra cui l'acceso a Internet, iTunes Store, App Store macOS, iCloud, messaggistica e così via.|phobos.apple.com<br>ocsp.apple.com<br>ax.itunes.apple.com<br>ax.itunes.apple.com.edgesuite.net|HTTP/HTTPS|80 o 443|

Per altre informazioni, vedere:

- [Porte TCP e UDP usate dai prodotti software Apple](https://support.apple.com/HT202944)
- [Informazioni sui processi in background e le connessioni host ai server macOS, iOS/iPadOS e iTunes](https://support.apple.com/HT201999)
- [Se i tuoi client macOS e iOS/iPadOS non ricevono le notifiche push di Apple](https://support.apple.com/HT203609)