---
title: Panoramica dell'abilitazione di Transport Layer Security (TLS) 1.2
titleSuffix: Configuration Manager
description: Panoramica delle procedure per abilitare TLS 1.2 per Configuration Manager.
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 31de47c9-891b-4de7-8d5e-fbbc1bff7c60
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8e1334603bcf60ea3eb8c3d18b73d511570cdc5d
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699739"
---
# <a name="how-to-enable-tls-12"></a>Come abilitare TLS 1.2

*Si applica a: Configuration Manager (Current Branch)*

Transport Layer Security (TLS), come Secure Sockets Layer (SSL), è un protocollo di crittografia progettato per mantenere i dati sicuri durante il trasferimento in rete. Questi articoli descrivono i passaggi necessari per assicurarsi che le comunicazioni protette di Configuration Manager usino il protocollo TLS 1.2. Questi articoli descrivono anche i requisiti di aggiornamento per i componenti di uso comune e la risoluzione dei problemi comuni.

## <a name="enabling-tls-12"></a>Abilitazione di TLS 1.2

Configuration Manager si basa su molti componenti diversi per proteggere le comunicazioni. Il protocollo usato per una determinata connessione dipende dalle funzionalità dei componenti rilevanti sul lato client e server. Se un componente non è aggiornato o non è configurato correttamente, è possibile che la comunicazione usi un protocollo precedente, meno sicuro. Per la corretta abilitazione di Configuration Manager per supportare TLS 1.2 per tutte le comunicazioni protette, è necessario abilitare TLS 1.2 per tutti i componenti necessari. I componenti necessari variano a seconda dell'ambiente e dalle funzionalità di Configuration Manager in uso.

> [!IMPORTANT]
> Avviare il processo con i client, in particolare con le versioni precedenti di Windows. Prima di abilitare TLS 1.2 e disabilitare i protocolli meno recenti nei server Configuration Manager, assicurarsi che tutti i client supportino TLS 1.2. In caso contrario, i client non possono comunicare con i server e potranno restare orfani.


## <a name="tasks-for-configuration-manager-clients-site-servers-and-remote-site-systems"></a>Attività per client, server del sito e sistemi del sito remoti di Configuration Manager

Per abilitare TLS 1.2 per i componenti da cui dipende Configuration Manager per le comunicazioni protette, è necessario eseguire più attività sia nei client che nei server del sito.

### <a name="enable-tls-12-for-configuration-manager-clients"></a>Abilitare TLS 1.2 per i client di Configuration Manager

- [Aggiornare Windows e WinHTTP in Windows 8.0, Windows Server 2012 (non R2) e versioni precedenti](enable-tls-1-2-client.md#bkmk_winhttp)
- [Assicurarsi che TLS 1.2 sia abilitato come protocollo per SChannel a livello di sistema operativo](enable-tls-1-2-client.md#bkmk_protocol)
- [Aggiornare e configurare .NET Framework per il supporto di TLS 1.2](enable-tls-1-2-client.md#bkmk_net)


### <a name="enable-tls-12-for-configuration-manager-site-servers-and-remote-site-systems"></a>Abilitare TLS 1.2 per i server del sito e i sistemi del sito remoti di Configuration Manager

- [Assicurarsi che TLS 1.2 sia abilitato come protocollo per SChannel a livello di sistema operativo](enable-tls-1-2-server.md#bkmk_protocol)
- [Aggiornare e configurare .NET Framework per il supporto di TLS 1.2](enable-tls-1-2-server.md#bkmk_net)
- [Aggiornare SQL Server e SQL Native Client](enable-tls-1-2-server.md#bkmk_sql)
- [Aggiornare Windows Server Update Services (WSUS)](enable-tls-1-2-server.md#bkmk_wsus)


## <a name="features-and-scenario-dependencies"></a>Dipendenze delle funzionalità e degli scenari

Questa sezione descrive le dipendenze per funzionalità e scenari specifici di Configuration Manager. Per determinare i passaggi successivi, individuare gli elementi che si applicano all'ambiente.

|Scenario o funzionalità|Attività di aggiornamento|
|--- |--- |
|Server del sito (centrale, primario o secondario)| - [Aggiornare .NET Framework](enable-tls-1-2-server.md#bkmk_net)<br/> - Verificare le impostazioni della crittografia complessa|
|Server di database del sito|[Aggiornare SQL Server e i componenti client](enable-tls-1-2-server.md#bkmk_sql)|
|Server del sito secondario|[Aggiornare SQL Server e i componenti client](enable-tls-1-2-server.md#bkmk_sql) a una versione conforme di SQL Express|
|Ruoli del sistema del sito| - [Aggiornare .NET Framework](enable-tls-1-2-server.md#bkmk_net) e verificare le impostazioni della crittografia complessa <br/> - [Aggiornare SQL Server e i componenti client](enable-tls-1-2-server.md#bkmk_sql) per i ruoli che lo richiedono, incluso [SQL Server Native Client](enable-tls-1-2-server.md#bkmk_sql-client)|
|Punto di Reporting Services|- [Aggiornare .NET Framework](enable-tls-1-2-server.md#bkmk_net) nel server del sito, nei server di SQL Reporting Services e nei computer con la console<br/> - Riavviare il servizio SMS_Executive in base alle esigenze|
|Punto di aggiornamento software|[Aggiornare WSUS](enable-tls-1-2-server.md#bkmk_wsus)|
|Gateway di gestione cloud|[Applicare TLS 1.2](../../clients/manage/cmg/security-and-privacy-for-cloud-management-gateway.md#bkmk_tls)|
|Console di Configuration Manager| - [Aggiornare .NET Framework](enable-tls-1-2-client.md#bkmk_net)<br/> - Verificare le impostazioni della crittografia complessa|
|Client Configuration Manager con ruoli del sistema del sito HTTPS|[Aggiornare Windows per supportare TLS 1.2 per le comunicazioni client-server usando WinHTTP](enable-tls-1-2-client.md#bkmk_winhttp)|
|Software Center| - [Aggiornare .NET Framework](enable-tls-1-2-client.md#bkmk_net)<br/> - Verificare le impostazioni della crittografia complessa|
|Client Windows 7| *Prima* di abilitare TLS 1.2 nei componenti server, [aggiornare Windows per supportare TLS 1.2 per le comunicazioni client-server usando WinHTTP](enable-tls-1-2-client.md#bkmk_winhttp). Se prima si abilita TLS 1.2 nei componenti server, è possibile rendere orfane le versioni precedenti dei client.|

## <a name="frequently-asked-questions"></a>Domande frequenti

### <a name="why-use-tls-12-with-configuration-manager"></a>Perché usare TLS 1.2 con Configuration Manager?

TLS 1.2 è più sicuro dei precedenti protocolli di crittografia, ad esempio SSL 2.0, SSL 3.0, TLS 1.0 e TLS 1.1. In sostanza, TLS 1.2 garantisce una maggiore sicurezza per i dati trasferiti in rete.

### <a name="where-does-configuration-manager-use-encryption-protocols-like-tls-12"></a>Dove vengono usati i protocolli di crittografia come TLS 1.2 in Configuration Manager?

Sono fondamentalmente cinque le aree in cui Configuration Manager usa i protocolli di crittografia come TLS 1.2:

- Le comunicazioni dei client con i ruoli del server del sito basati su IIS quando il ruolo è configurato per l'uso di HTTPS. Esempi di questi ruoli includono i punti di distribuzione, i punti di aggiornamento software e i punti di gestione.
- Comunicazioni del punto di gestione, di SMS Executive e del provider SMS con SQL. Configuration Manager crittografa sempre le comunicazioni SQL.
- Comunicazioni dal server del sito a WSUS se WSUS è configurato per l'uso di HTTPS.
- Comunicazioni dalla console di Configuration Manager a SQL Reporting Services (SSRS) se SSRS è configurato per l'uso di HTTPS.
- Tutte le connessioni a servizi basati su Internet. Ad esempio Cloud Management Gateway (CMG), la sincronizzazione del punto di connessione del servizio e la sincronizzazione dei metadati di aggiornamento da Microsoft Update.

### <a name="what-determines-which-encryption-protocol-is-used"></a>Che cosa determina la scelta del protocollo di crittografia da usare?

HTTPS negozierà sempre la versione del protocollo più elevata supportata dal client e dal server in una conversazione crittografata. Quando si stabilisce una connessione, il client invia un messaggio al server con il protocollo più elevato disponibile. Se il server supporta la stessa versione, invia un messaggio con tale versione. Questa versione negoziata è quella usata per la connessione. Se il server non supporta la versione presentata dal client, il messaggio del server specificherà la versione più recente che può usare. Per altre informazioni sul protocollo di handshake TLS, vedere [Stabilire una sessione protetta usando TLS](/windows/win32/secauthn/tls-handshake-protocol#establishing-a-secure-session-by-using-tls).

### <a name="what-determines-which-protocol-version-the-client-and-server-can-use"></a>Che cosa determina la versione del protocollo che può essere usata da client e server?

In genere, gli elementi seguenti possono determinare la versione del protocollo usata:

- L'applicazione può determinare le versioni specifiche del protocollo da negoziare.
  - Le procedure consigliate prevedono di evitare versioni di protocollo specifiche hardcoded a livello di applicazione e di seguire la configurazione definita a livello di protocollo per il componente e il sistema operativo.
  - Configuration Manager segue questa procedura consigliata.
- Per le applicazioni scritte con .NET Framework, le versioni del protocollo predefinite dipendono dalla versione del framework su cui sono state compilate.  
  - Per impostazione predefinita, le versioni di .NET precedenti alla 4.6.3 non includono TLS 1.1 e 1.2 nell'elenco di protocolli per la negoziazione.
- Le applicazioni che usano WinHTTP per le comunicazioni HTTPS, ad esempio il client di Configuration Manager, dipendono dalla versione del sistema operativo, dal livello di patch e dalla configurazione per il supporto della versione del protocollo.


## <a name="additional-resources"></a>Risorse aggiuntive

- [Riferimento tecnico per i controlli crittografici](cryptographic-controls-technical-reference.md)
- [Procedure consigliate per Transport Layer Security (TLS) con .NET Framework](/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry)
- [KB 3135244: Supporto di TLS 1.2 per Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)

## <a name="next-steps"></a>Passaggi successivi

- [Abilitare TLS 1.2 nei client](enable-tls-1-2-client.md)
- [Abilitare TLS 1.2 nei server del sito](enable-tls-1-2-server.md)