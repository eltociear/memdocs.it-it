---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/13/2019
ms.openlocfilehash: 0f91860ad591e20c6f199e098a8c957f50294386
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88704453"
---
<!-- ## Update and configure the .NET Framework to support TLS 1.2 Note: the heading in in the 2 articles (enable-tls-1-2-client & enable-tls-1-2-server) to better facilitate linking. -->

### <a name="determine-net-version"></a>Determinare la versione di .NET

Determinare prima di tutto le versioni di .NET installate. Per altre informazioni, vedere [Come determinare quali versioni e livelli di Service Pack di Microsoft.NET Framework sono installati](https://support.microsoft.com/help/318785/how-to-determine-which-versions-and-service-pack-levels-of-the-microso).

### <a name="install-net-updates"></a>Installare gli aggiornamenti di .NET

Installare gli aggiornamenti di .NET in modo da poter abilitare la crittografia avanzata. Alcune versioni di .NET Framework potrebbero richiedere aggiornamenti per abilitare la crittografia complessa. Usare queste linee guida:

- NET Framework 4.6.2 e versioni successive supportano TLS 1.1 e TLS 1.2. Confermare le impostazioni del Registro di sistema, ma non sono richieste modifiche aggiuntive.

- Aggiornare NET Framework 4.6 e versioni precedenti per supportare TLS 1.1 e TLS 1.2. Per altre informazioni, vedere [Versioni e dipendenze di .NET Framework](/dotnet/framework/migration-guide/versions-and-dependencies).

- Se si usa .NET Framework 4.5.1 o 4.5.2 in Windows 8.1 o Windows Server 2012, gli aggiornamenti pertinenti e i dettagli sono disponibili anche nell'[Area download](https://www.microsoft.com/download/details.aspx?id=42883).


### <a name="configure-for-strong-cryptography"></a>Configurare la crittografia complessa

Configurare .NET Framework per supportare la crittografia complessa. Configurare l'impostazione del Registro di sistema `SchUseStrongCrypto` su `DWORD:00000001`, che disabilita la crittografia a flusso RC4 e richiede un riavvio. Per altre informazioni su questa impostazione, vedere [Avviso di sicurezza Microsoft 296038](/security-updates/SecurityAdvisories/2015/2960358).

Assicurarsi di impostare le chiavi del Registro di sistema seguenti in qualsiasi computer che comunica attraverso la rete con un sistema abilitato per TLS 1.2, ad esempio i client di Configuration Manager, i ruoli del sistema del sito remoto non installati nel server del sito e il server del sito stesso.

Per le applicazioni a 32 bit in esecuzione in sistemi operativi a 32 bit e per le applicazioni a 64 bit in esecuzione in sistemi operativi a 64 bit, aggiornare i valore di sottochiave seguenti:

``` Registry
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v2.0.50727]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
```

Per le applicazioni a 32 bit in esecuzione in sistemi operativi a 64 bit, aggiornare i valori di sottochiave seguenti:

``` Registry
[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v2.0.50727]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
```

> [!Note]  
> L'impostazione `SchUseStrongCrypto` consente a .NET di usare TLS 1.1 e TLS 1.2. L'impostazione `SystemDefaultTlsVersions` consente a .NET di usare la configurazione del sistema operativo. Per altre informazioni, vedere [Procedure consigliate per Transport Layer Security (TLS) con .NET Framework](/dotnet/framework/network-programming/tls).