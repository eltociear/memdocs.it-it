---
title: Problemi comuni relativi all'abilitazione di Transport Layer Security (TLS) 1.2
titleSuffix: Configuration Manager
description: Vengono descritti i problemi comuni relativi all'abilitazione di Transport Layer Security (TLS) 1.2
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 15083f28-8ff2-4e23-9f5e-b5dbd0859839
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7c07b0af1b3063619ac5f71965d96f611aefafd9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704069"
---
# <a name="common-issues-when-enabling-tls-12"></a>Problemi comuni relativi all'abilitazione di TLS 1.2

Questo articolo fornisce consigli per i problemi comuni che si verificano quando si abilita il supporto di TLS 1.2 in Configuration Manager.

## <a name="unsupported-platforms"></a>Piattaforme non supportate

Le piattaforme client seguenti sono supportate da Configuration Manager, ma non sono supportate in un ambiente TLS 1.2:

- Windows CE
- Apple OS X
- Dispositivi Windows 10 gestiti con MDM locale

## <a name="reports-dont-show-in-the-console"></a>I report non vengono visualizzati nella console

Se i report non vengono visualizzati nella console di Configuration Manager, assicurarsi di aggiornare il computer in cui si esegue la console. [Aggiornare .NET Framework](enable-tls-1-2-client.md#bkmk_net) e abilitare la crittografia complessa.

## <a name="fips-security-policy-enabled"></a>Criteri di sicurezza FIPS abilitati

Se si abilita l'impostazione dei criteri di sicurezza FIPS per il client o un server, la negoziazione di Secure Channel (Schannel) può comportare l'uso di TLS 1.0. Questo comportamento si verifica anche se si disabilita il protocollo nel Registro di sistema.

Per analizzare il problema, abilitare la registrazione eventi del canale sicuro e quindi esaminare gli eventi Schannel nel registro di sistema. Per altre informazioni, vedere [Come limitare l'uso di determinati algoritmi di crittografia e protocolli in Schannel.dll](https://support.microsoft.com/help/245030/how-to-restrict-the-use-of-certain-cryptographic-algorithms-and-protoc).

## <a name="sql-server-communication-failure"></a>Errore di comunicazione di SQL Server

Se la comunicazione di SQL Server non riesce e restituisce un errore **SslSecurityError**, verificare le impostazioni seguenti:

- [Aggiornare .NET Framework](enable-tls-1-2-server.md#bkmk_net) e abilitare la crittografia complessa in ogni computer
- [Aggiornare SQL Server](enable-tls-1-2-server.md#bkmk_sql) nel server host
- [Aggiornare i componenti client di SQL](enable-tls-1-2-server.md#bkmk_sql-client) in tutti i sistemi che comunicano con SQL, ad esempio i server del sito, il provider SMS e i server del ruolo del sito.

## <a name="configuration-manager-client-communication-failures"></a>Errori di comunicazione del client Configuration Manager

Se il client Configuration Manager non comunica con i ruoli del sito, verificare di aver [aggiornato Windows](enable-tls-1-2-client.md#bkmk_winhttp) per supportare TLS 1.2 per la comunicazione client-server usando WinHTTP. I ruoli del sito comuni includono i punti di distribuzione, i punti di gestione e i punti di migrazione stato.

## <a name="reporting-services-point-fails-and-returns-an-expected-error"></a>Il punto di Reporting Services ha esito negativo e restituisce un errore previsto

Se il punto di Reporting Services non configura i report, cercare il messaggio di errore seguente in **SRSRP.log**:

`The underlying connection was closed:`
`An expected error occurred on a receive.`

Per risolvere questo problema, seguire questa procedura:

1. [Aggiornare .NET Framework](enable-tls-1-2-client.md#bkmk_net) e abilitare la crittografia complessa in tutti i computer pertinenti.

1. Dopo aver installato eventuali aggiornamenti, riavviare il servizio SMS_Executive.

## <a name="application-catalog-doesnt-initialize"></a>Il Catalogo applicazioni non viene inizializzato

> [!Important]  
> Il supporto per i ruoli del Catalogo applicazioni termina con la versione 1910. Per altre informazioni, vedere [Funzionalità rimosse e deprecate](../changes/deprecated/removed-and-deprecated-cmfeatures.md).

Se il Catalogo applicazioni non viene inizializzato, cercare il messaggio di errore seguente nel file **ServicePortalWebSite.svclog**:

`SOAP security negotiation failed. The client and server can't communicate because they don't share a common algorithm.`

Per risolvere questo problema, seguire questa procedura:

1. [Aggiornare .NET Framework](enable-tls-1-2-client.md#bkmk_net) e abilitare la crittografia complessa in tutti i computer pertinenti.

1. Nella cartella `%WinDir%\System32\InetSrv` del server del Catalogo applicazioni creare un file **W2SP.exe.config** con il contenuto seguente:

    ``` XML
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <runtime>
      <AppContextSwitchOverrides value="Switch.System.ServiceModel.DisableUsingServicePointManagerSecurityProtocols=false;Switch.System.Net.DontEnableSchUseStrongCrypto=false" />
      </runtime>
    </configuration>
    ```

    > [!NOTE]
    > Questo è il file predefinito che viene creato se l'applicazione viene compilata usando .NET Framework 4.6.3.

1. Usare la sicurezza del trasporto HTTPS per i ruoli del Catalogo applicazioni.

    > [!Important]
    > Quando si usa la sicurezza del messaggio HTTP per i ruoli del Catalogo applicazioni, WCF è hardcoded in modo che sia possibile usare solo SSL 3.0 e TLS 1.0. Ciò impedisce l'uso di TLS 1.2.

1. Se sono state apportate modifiche, riavviare il computer.

## <a name="software-center-or-browser-doesnt-communicate-with-the-application-catalog"></a>Software Center o il browser non comunica con il Catalogo applicazioni

> [!Important]  
> Il supporto per i ruoli del Catalogo applicazioni termina con la versione 1910. Per altre informazioni, vedere [Funzionalità rimosse e deprecate](../changes/deprecated/removed-and-deprecated-cmfeatures.md).

Il metodo migliore per usare Software Center con le app disponibili per gli utenti in un sito abilitato per TLS 1.2 consiste nel rimuovere il ruolo del Catalogo applicazioni. Consentire quindi a Software Center di comunicare direttamente con un punto di gestione. Per altre informazioni, vedere [Rimuovere il catalogo applicazioni](../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat).

Se è necessario risolvere gli errori di comunicazione tra il Catalogo applicazioni e Software Center, verificare le condizioni seguenti:

- [Aggiornare .NET Framework](enable-tls-1-2-client.md#bkmk_net) e abilitare la crittografia complessa in ogni computer.

- Dopo aver apportato le modifiche, riavviare tutti i computer interessati.

<!-- - Configure the browser is configured to support TLS 1. Prior to Windows 10, this option was disabled by default. removing, Silverlight experience is out of support-->

## <a name="service-connection-point-upload-failures"></a>Errori di caricamento del punto di connessione del servizio

Se il punto di connessione del servizio non carica i dati in SCCMConnectedService, [aggiornare .NET Framework](enable-tls-1-2-server.md#bkmk_net) e abilitare la crittografia complessa in ogni computer. Ricordare di riavviare i computer dopo aver apportato le modifiche.

## <a name="configuration-manager-console-displays-intune-onboarding-dialog-box"></a>La console di Configuration Manager visualizza la finestra di dialogo di onboarding di Intune

Se la finestra di dialogo di onboarding di Intune viene visualizzata quando la console prova a connettersi al portale di Intune, [aggiornare .NET Framework](enable-tls-1-2-client.md#bkmk_net) e abilitare la crittografia complessa in ogni computer. Ricordare di riavviare i computer dopo aver apportato le modifiche.

## <a name="configuration-manager-console-displays-failure-to-sign-in-to-azure"></a>La console di Configuration Manager visualizza un errore di accesso ad Azure

Quando si prova a creare applicazioni di Azure AD (Azure AD), se la finestra di dialogo di onboarding dei servizi di Azure ha esito negativo subito dopo aver selezionato **Accedi**, [aggiornare .NET Framework](enable-tls-1-2-server.md#bkmk_net) e abilitare la crittografia complessa. Ricordare di riavviare i computer dopo aver apportato le modifiche.

## <a name="configuration-manager-cloud-services-and-tls-12"></a>Servizi cloud di Configuration Manager e TLS 1.2

Le macchine virtuali di Azure usate dal gateway di gestione cloud e dai punti di distribuzione cloud supportano TLS 1.2. Le versioni client supportate usano automaticamente TLS 1.2.

**SMSAdminui.log** può contenere un errore simile all'esempio seguente:

``` Log
Microsoft.ConfigurationManager.CloudBase.AAD.AADAuthenticationException
Service returned error. Check InnerException for more details
at Microsoft.ConfigurationManager.CloudBase.AAD.AADAuthenticationContext.GetAADAuthResultObject
...
Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException
Service returned error. Check InnerException for more details
at Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext.RunAsyncTask
...
System.Net.WebException
The underlying connection was closed: An unexpected error occurred on a receive.
at System.Net.HttpWebRequest.GetResponse
```

Nel registro eventi del sistema potrebbe essere registrato l'ID evento 36874 di SChannel con la descrizione seguente: `An TLS 1.2 connection request was received from a remote client application, but none of the cipher suites supported by the client application are supported by the server. The TLS connection request has failed.`
<!--SCCMDocs issue #1608-->

## <a name="additional-resources"></a>Risorse aggiuntive

- [Procedure consigliate per Transport Layer Security (TLS) con .NET Framework](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry)
- [KB 3135244: Supporto di TLS 1.2 per Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)
- [Riferimento tecnico per i controlli crittografici](cryptographic-controls-technical-reference.md)

## <a name="next-steps"></a>Passaggi successivi

- [Abilitare TLS 1.2 nei client](enable-tls-1-2-client.md)
- [Abilitare TLS 1.2 nei server del sito e nei sistemi del sito remoti](enable-tls-1-2-server.md)

