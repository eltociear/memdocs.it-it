---
title: Come abilitare Transport Layer Security (TLS) 1.2 nei client
titleSuffix: Configuration Manager
description: Informazioni su come abilitare TLS 1.2 per i client di Configuration Manager.
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5b094a02-a425-4b67-81d3-8455e4265512
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e5b525da4a58240b34c30403db618ea0d2ca85f1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704109"
---
# <a name="how-to-enable-tls-12-on-clients"></a>Come abilitare TLS 1.2 nei client

*Si applica a: Configuration Manager (Current Branch)*

Quando si abilita TLS 1.2 per l'ambiente di Configuration Manager, assicurarsi prima di tutto che i client siano idonei e configurati correttamente per l'uso di TLS 1.2 prima di abilitare TLS 1.2 e disabilitare i protocolli meno recenti nei server del sito e nei sistemi del sito remoto. Sono disponibili tre attività per l'abilitazione di TLS 1.2 nei client:

- Aggiornare Windows e WinHTTP
- Assicurarsi che TLS 1.2 sia abilitato come protocollo per SChannel a livello di sistema operativo
- Aggiornare e configurare .NET Framework per il supporto di TLS 1.2

Per altre informazioni sulle dipendenze per funzionalità e scenari specifici di Configuration Manager, vedere [informazioni sull'abilitazione di TLS 1.2](enable-tls-1-2.md).

## <a name="update-windows-and-winhttp"></a><a name="bkmk_winhttp"></a> Aggiornare Windows e WinHTTP

Windows 8.1, Windows 2012 R2, Windows 10, Windows Server 2016 e le versioni successive di Windows supportano in modo nativo TLS 1.2 per le comunicazioni client-server tramite WinHTTP. 

Le versioni precedenti di Windows, ad esempio Windows 7 o Windows Server 2012, non abilitano TLS 1.1 o 1.2 per impostazione predefinita per le comunicazioni sicure tramite WinHTTP. Per queste versioni precedenti di Windows, installare l'[aggiornamento 3140245](https://support.microsoft.com/help/3140245) per abilitare il valore del Registro di sistema riportato di seguito, che può essere impostato per aggiungere TLS 1.1 e TLS 1.2 all'elenco dei protocolli protetti predefiniti per WinHTTP. Con la patch installata, creare i valori del Registro di sistema seguenti:

> [!IMPORTANT]
> Abilitare queste impostazioni in tutti i client che eseguono versioni precedenti di Windows *prima* di abilitare TLS 1.2 e disabilitare i protocolli meno recenti nei server di Configuration Manager. In caso contrario, è possibile renderli inavvertitamente orfani.

Verificare il valore dell'impostazione del Registro di sistema `DefaultSecureProtocols`, ad esempio:

``` Registry
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
```

Se si modifica questo valore, riavviare il computer.

L'esempio precedente illustra il valore di `0xAA0` per l'impostazione `DefaultSecureProtocols` di WinHTTP. L'articolo [KB 3140245: Eseguire l'aggiornamento per abilitare TLS 1.1 e 1.2 TLS come protocolli sicuri predefiniti in WinHTTP in Windows](https://support.microsoft.com/help/3140245) elenca il valore esadecimale per ogni protocollo. Per impostazione predefinita in Windows, questo valore è `0x0A0` per abilitare SSL 3.0 e TLS 1.0 per WinHTTP. L'esempio precedente mantiene queste impostazioni predefinite e abilita anche TLS 1.1 e TLS 1.2 per WinHTTP. Questa configurazione assicura che la modifica non interrompa altre applicazioni che potrebbe essere ancora basate su SSL 3.0 o TLS 1.0. È possibile usare il valore di `0xA00` per abilitare solo TLS 1.1 e TLS 1.2. Configuration Manager supporta il protocollo più sicuro negoziato da Windows tra entrambi i dispositivi.

 Per disabilitare completamente SSL 3.0 e TLS 1.0, usare l'impostazione dei protocolli disabilitati da SChannel in Windows. Per altre informazioni, vedere [Come limitare l'uso di determinati algoritmi di crittografia e protocolli in Schannel.dll](https://support.microsoft.com/help/245030/how-to-restrict-the-use-of-certain-cryptographic-algorithms-and-protoc).

## <a name="ensure-that-tls-12-is-enabled-as-a-protocol-for-schannel-at-the-operating-system-level"></a><a name="bkmk_protocol"></a> Assicurarsi che TLS 1.2 sia abilitato come protocollo per SChannel a livello di sistema operativo

[!INCLUDE [Enable TLS 1.2 protocol as a security provider](includes/enable-tls-1-2-protocol-security-provider.md)]

## <a name="update-and-configure-the-net-framework-to-support-tls-12"></a><a name="bkmk_net"></a> Aggiornare e configurare .NET Framework per il supporto di TLS 1.2

[!INCLUDE [Update and configure the .NET framework to support TLS 1.2](includes/update-net-framework-to-support-tls-1-2.md)]


## <a name="next-steps"></a>Passaggi successivi

- [Abilitare TLS 1.2 nei server del sito e nei sistemi del sito remoti](enable-tls-1-2-server.md)
- [Problemi comuni relativi all'abilitazione di TLS 1.2](enable-tls-1-2-troubleshoot.md)

