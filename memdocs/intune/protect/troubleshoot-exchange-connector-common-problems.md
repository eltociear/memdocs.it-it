---
title: Risolvere i problemi comuni per Intune Exchange Connector
titleSuffix: Microsoft Intune
description: Risolvere i problemi e correggere gli errori comuni relativi a Microsoft Intune On-Premises Exchange Connector.
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/26/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 55f51f94cf26aa2486ef390d5fbb668eaf013e10
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79350629"
---
# <a name="resolve-common-problems-with-the-intune-exchange-connector"></a>Risolvere i problemi comuni di Intune Exchange Connector
 
Questo articolo può essere utile all'amministratore di Intune per risolvere i problemi comuni relativi al funzionamento di Intune Exchange Connector.

Prima di iniziare la risoluzione dei problemi, vedere [Risolvere i problemi di Intune On-Premises Exchange Connector](troubleshoot-exchange-connector.md) per informazioni di base sul connettore. Esaminare anche i problemi comuni per la configurazione del connettore.

## <a name="an-exchange-activesync-device-isnt-discovered-from-exchange"></a>Un dispositivo Exchange ActiveSync non viene individuato da Exchange

Quando un dispositivo Exchange ActiveSync non viene individuato da Exchange, [monitorare l'attività di Exchange Connector](exchange-connector-install.md#on-premises-intune-exchange-connector-high-availability-support) per verificare se Exchange Connector esegue la sincronizzazione con il server Exchange. Se non è stata eseguita alcuna sincronizzazione dopo l'aggiunta del dispositivo, raccogliere i log di sincronizzazione e allegarli a una richiesta di supporto. Se è stata completata una sincronizzazione completa o una sincronizzazione rapida dopo l'aggiunta del dispositivo, verificare se sussistono i seguenti problemi:

- Assicurarsi che gli utenti dispongano di una licenza di Intune. In caso contrario, Exchange Connector non riuscirà a individuare i relativi dispositivi.

- Se l'indirizzo SMTP primario dell'utente è diverso dal nome dell'entità utente (UPN) in Azure Active Directory (Azure AD), Exchange Connector non sarà in grado di individuare alcun dispositivo per tale utente. Risolvere l'indirizzo SMTP primario per risolvere il problema.

- Se l'ambiente include server di cassette postali sia di Exchange 2010 che di Exchange 2013, si consiglia di associare Exchange Connector a un server Accesso client (CAS) di Exchange 2013. Se Exchange Connector è configurato per comunicare con un CAS di Exchange 2010, Exchange Connector non individuerà i dispositivi degli utenti in Exchange 2013.

- Per gli ambienti Exchange Online dedicato, è necessario puntare Exchange Connector a un server Accesso client di Exchange 2013 (non Exchange 2010) nell'ambiente dedicato durante l'installazione iniziale. Il connettore comunicherà solo con un server Accesso client di Exchange 2013 durante l'esecuzione dei cmdlet di PowerShell.

## <a name="problems-with-the-notification-email-message"></a>Problemi relativi al messaggio di posta elettronica di notifica

Per supportare l'accesso condizionale per le cassette postali locali nei dispositivi che non eseguono Android Knox, assicurarsi che la registrazione di Intune venga avviata dal messaggio di posta elettronica "Per iniziare" inviato da Intune Exchange Connector. L'avvio della registrazione dal messaggio garantisce che il dispositivo riceva un ActiveSyncID univoco in tutte le piattaforme (Exchange, Azure AD, Intune).

Un utente potrebbe non ricevere il messaggio di posta elettronica di notifica perché:

- L'account di notifica è stato configurato in modo errato.
- L'individuazione automatica non è riuscita per l'account di notifica.
- La richiesta di Servizi Web Exchange per l'invio del messaggio di posta elettronica ha avuto esito negativo.

Esaminare le sezioni seguenti per risolvere i problemi relativi alle notifiche di posta elettronica.

### <a name="check-the-notification-account-that-retrieves-autodiscover-settings"></a>Controllare l'account di notifica che recupera le impostazioni di individuazione automatica

1. Verificare che il servizio di individuazione automatica e i servizi Web Exchange siano configurati nei servizi Accesso client di Exchange. Per altre informazioni, vedere [Servizi di accesso client](https://docs.microsoft.com/Exchange/architecture/client-access/client-access) e [Servizio di individuazione automatica in Exchange Server](https://docs.microsoft.com/Exchange/architecture/client-access/autodiscover?view=exchserver-2019).

2. Verificare che l'account di notifica soddisfi i requisiti seguenti:

   - L'account dispone di una cassetta postale attiva ospitata dal server Exchange locale.

   - Il nome UPN dell'account corrisponde all'indirizzo SMTP.

3. L'individuazione automatica richiede un server DNS con un record DNS per **Autodiscover.SMTPdomain.com** (ad esempio, Autodiscover.contoso.com) che punta al server Accesso client di Exchange. Per verificare la presenza del record, specificare il nome FQDN al posto di *Autodiscover.SMTPdomain.com* e seguire questa procedura:

   1. Al prompt dei comandi immettere *NSLOOKUP*.

   2. Immettere *Autodiscover.SMTPdomain.com*. L'output dovrebbe essere simile all'immagine seguente: risultati di ![Nslookup](./media/troubleshoot-exchange-connector-common-problems/nslookup-results.png
      )

   È anche possibile testare il servizio di individuazione automatica da Internet all'indirizzo https://testconnectivity.microsoft.com. In alternativa, è possibile testarlo da un dominio locale usando Microsoft Connectivity Analizer Tool. Per altre informazioni, vedere [Microsoft Connectivity Analyzer Tool](https://docs.microsoft.com/previous-versions/office/exchange-remote-connectivity/jj851141(v=exchg.80)).


### <a name="check-autodiscovery"></a>Controllare l'individuazione automatica

Se l'individuazione automatica ha esito negativo, provare a eseguire la procedura seguente:

1. [Configurare un record DNS di individuazione automatica valido](https://docs.microsoft.com/previous-versions/exchange-server/exchange-150/mt473798(v=exchg.150)).

2. Impostare come hardcoded l'URL di Servizi Web Exchange nel file di configurazione di Intune Exchange Connector:

   1. Determinare l'URL di Servizi Web Exchange. L'URL predefinito di Servizi Web Exchange per Exchange è `https://<mailServerFQDN>/ews/exchange.asmx`, ma l'URL potrebbe variare. Contattare l'amministratore di Exchange per verificare l'URL corretto per l'ambiente.

   2. Modificare il file *OnPremisesExchangeConnectorServiceConfiguration.xml*. Per impostazione predefinita, il file si trova in *%ProgramData%\Microsoft\Windows Intune Exchange Connector* nel computer in cui è in esecuzione Exchange Connector. Aprire il file in un editor di testo e quindi modificare la riga seguente in modo che corrisponda all'URL di Servizi Web Exchange per l'ambiente: `<ExchangeWebServiceURL>https://<YourExchangeHOST>/EWS/Exchange.asmx</ExchangeWebServiceURL>`

3. Salvare il file e quindi riavviare il computer o riavviare il servizio Microsoft Intune Exchange Connector.

>[!NOTE]
> In questa configurazione, Intune Exchange Connector interrompe l'uso dell'individuazione automatica e si connette direttamente all'URL di Servizi Web Exchange.

## <a name="next-steps"></a>Passaggi successivi

Per informazioni su errori specifici, provare [Risolvere gli errori comuni di Intune Exchange Connector](troubleshoot-exchange-connector-common-errors.md).

Per ottenere supporto o per ricevere assistenza dalla community di Intune:

- Per informazioni su come usare la console di Intune per risolvere il problema o inviare una richiesta di supporto a Microsoft, vedere [Ottenere supporto](../fundamentals/get-support.md).
- Pubblicare il problema nei [forum di Microsoft Intune](https://social.technet.microsoft.com/Forums/home?forum=microsoftintuneprod).