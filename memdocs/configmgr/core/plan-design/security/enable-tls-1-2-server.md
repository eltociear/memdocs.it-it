---
title: Abilitare Transport Layer Security (TLS) 1.2 nei server del sito e nei sistemi del sito remoti
titleSuffix: Configuration Manager
description: Informazioni su come abilitare TLS 1.2 per i server del sito di Configuration Manager.
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0ce9b428-cb0f-46f3-bf69-c465e6623d6f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 15377520b76b9b3a3813e6ad4253548f29e011db
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704099"
---
# <a name="how-to-enable-tls-12-on-the-site-servers-and-remote-site-systems"></a>Come abilitare TLS 1.2 nei server del sito e nei sistemi del sito remoti

*Si applica a: Configuration Manager (Current Branch)*

Quando si abilita TLS 1.2 per l'ambiente di Configuration Manager, iniziare con l'[abilitazione di TLS 1.2 per i client](enable-tls-1-2-client.md). Abilitare poi TLS 1.2 nei server del sito e nei sistemi del sito remoti. Infine, testare le comunicazioni da client a sistema del sito prima di disabilitare potenzialmente i protocolli meno recenti sul lato server. Per abilitare TLS 1.2 nei server del sito e nei sistemi del sito remoti, sono necessarie le attività seguenti:

- Assicurarsi che TLS 1.2 sia abilitato come protocollo per SChannel a livello di sistema operativo
- Aggiornare e configurare .NET Framework per il supporto di TLS 1.2
- Aggiornare SQL Server e i componenti client
- Aggiornare Windows Server Update Services (WSUS)

Per altre informazioni sulle dipendenze per funzionalità e scenari specifici di Configuration Manager, vedere [informazioni sull'abilitazione di TLS 1.2](enable-tls-1-2.md). 

## <a name="ensure-that-tls-12-is-enabled-as-a-protocol-for-schannel-at-the-operating-system-level"></a><a name="bkmk_protocol"></a> Assicurarsi che TLS 1.2 sia abilitato come protocollo per SChannel a livello di sistema operativo

[!INCLUDE [Enable TLS 1.2 protocol as a security provider](includes/enable-tls-1-2-protocol-security-provider.md)]

## <a name="update-and-configure-the-net-framework-to-support-tls-12"></a><a name="bkmk_net"></a> Aggiornare e configurare .NET Framework per il supporto di TLS 1.2

[!INCLUDE [Update and configure the .NET framework to support TLS 1.2](includes/update-net-framework-to-support-tls-1-2.md)]


## <a name="update-sql-server-and-client-components"></a><a name="bkmk_sql"></a> Aggiornare SQL Server e i componenti client

Microsoft SQL Server 2016 e versioni successive supportano TLS 1.1 e TLS 1.2. Le versioni precedenti e le librerie dipendenti potrebbero richiedere aggiornamenti. Per altre informazioni, vedere [KB 3135244: Supporto di TLS 1.2 per Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server).

Per i server del sito secondario è necessario usare almeno SQL Server 2016 Express con Service Pack 2 (13.2.50.26) o versione successiva.

### <a name="sql-server-native-client"></a><a name="bkmk_sql-client"></a> SQL Server Native Client

> [!NOTE]
> L'[articolo KB 3135244](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server) descrive anche i requisiti per i componenti client di SQL Server.

Assicurarsi di aggiornare anche SQL Server Native Client almeno alla versione SQL 2012 SP4 (11.*.7001.0). A partire dalla versione 1810, questo requisito fa parte dei [controlli dei prerequisiti (avviso)](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).

Configuration Manager usa SQL Server Native Client nei seguenti ruoli del sistema del sito:

- Server di database del sito
- Server del sito: sito di amministrazione centrale, sito primario o sito secondario
- Punto di gestione
- Punto di gestione dei dispositivi
- Punto di migrazione stato
- Provider SMS
- Punto di aggiornamento software
- Punto di distribuzione abilitato per multicast
- Punto di servizio aggiornamento AI
- Punto di Reporting Services
- Servizio Web del Catalogo applicazioni
- Punto di registrazione
- Punto di Endpoint Protection
- punto di connessione del servizio
- Punto di registrazione certificati
- Punto di servizio del data warehouse


## <a name="update-windows-server-update-services-wsus"></a><a name="bkmk_wsus"></a> Aggiornare Windows Server Update Services (WSUS)

Per supportare TLS 1.2 nelle versioni precedenti di WSUS, installare l'aggiornamento seguente nel server WSUS:

- Per il server WSUS che esegue Windows Server 2012, installare l'[aggiornamento 4022721](https://support.microsoft.com/help/4022721) o un aggiornamento cumulativo successivo.
- Per il server WSUS che esegue Windows Server 2012 R2, installare l'[aggiornamento 4022720](https://support.microsoft.com/help/4022720) o un aggiornamento cumulativo successivo.

A partire da Windows Server 2016, TLS 1.2 è supportato per impostazione predefinita per WSUS.  Gli aggiornamenti di TLS 1.2 sono necessari solo nei server WSUS Windows Server 2012 e Windows Server 2012 R2.

## <a name="next-steps"></a>Passaggi successivi

- [Problemi comuni relativi all'abilitazione di TLS 1.2](enable-tls-1-2-troubleshoot.md)
