---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/13/2019
ms.openlocfilehash: f14713431c71c1f3625d13ea4be1d919b072e273
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88704252"
---
<!--## Enable Transport layer security (TLS) 1.2 protocol as a security provider Note: the heading in in the 2 articles (enable-tls-1-2-client & enable-tls-1-2-server) to better facilitate linking. -->

TLS 1.2 è abilitato per impostazione predefinita, quindi non è necessario apportare modifiche a queste chiavi per abilitarlo. È possibile apportare modifiche in `Protocols` per disabilitare TLS 1.0 e TLS 1.1 dopo aver seguito il resto delle indicazioni fornite in questi articoli e aver verificato che l'ambiente funzioni quando è abilitato solo TLS 1.2.

Verificare l'impostazione della sottochiave del Registro di sistema `\SecurityProviders\SCHANNEL\Protocols`, come illustrato in [Procedure consigliate per Transport Layer Security (TLS) con .NET Framework](/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry).