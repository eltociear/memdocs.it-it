---
title: Flusso di lavoro di autenticazione di Azure AD
titleSuffix: Configuration Manager
description: Dettagli del processo di installazione del client Configuration Manager in un dispositivo Windows 10 con l'autenticazione di Azure Active Directory
ms.date: 07/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 9aaf466a-3f40-4468-b3cd-f0010f21f05a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9215688104b1a929cad7c172126387961851760b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694999"
---
# <a name="azure-ad-authentication-workflow"></a>Flusso di lavoro di autenticazione di Azure AD

*Si applica a: Configuration Manager (Current Branch)*

Questo articolo contiene informazioni tecniche per il processo di installazione del client Configuration Manager in un dispositivo Windows 10 aggiunto ad Azure Active Directory (Azure AD). Illustra in dettaglio il processo del flusso di lavoro per l'autenticazione del dispositivo e l'installazione del client.  
 

## <a name="azure-ad-token-request-workflow"></a>Flusso di lavoro di richiesta di token di AD Azure

![Diagramma del flusso di lavoro di Azure AD CCMSetup](media/azure-ad-install-workflow.png)  

### <a name="1-azure-ad-token-request"></a>1. Richiesta di token di AD Azure

Un client aggiunto a un dominio di AD Azure in Windows 10 usa i parametri di Azure AD per richiedere un token. Le voci seguenti vengono registrate in **ccmsetup.log**:

- Richiedere un token di dispositivo di Azure AD:

    ``` Log
    Getting AAD (device) token with: ClientId = 22ed38d9-XXXX-4036-XXXX-a98452fda4fc, ResourceUrl = https://ConfigMgrService, AccountId = https://login.microsoftonline.com/common/oauth2/token
    ```

- Se non riesce a ottenere un token di dispositivo, richiede un token utente di Azure AD:

    ``` Log
    Getting AAD (user) token with: ClientId = f1f9b14e-XXXX-4f17-XXXX-2593f6eee91e, ResourceUrl = https://ConfigMgrService, AccountId = X49FC29A-ECE3-XXX-A3C1-XXXXXXF035A6E
    ```

> [!NOTE]
> Un client deve ottenere un certificato di aggiunta alla rete aziendale quando viene aggiunto ad AD Azure. Se non viene trovato un certificato di aggiunta alla rete aziendale, il client non prova a creare la richiesta usando il canale di comunicazione del servizio token di sicurezza (CCM_STS). Questo comportamento è dovuto all'impossibilità per il client di aggiungere un token di Azure AD alla richiesta. Il dispositivo in genere non ha questo certificato quando il client non è aggiunto correttamente ad Azure AD.
>
> Inoltre, se il token non è valido, Cloud Management Gateway (CMG) non inoltra la richiesta ai ruoli del sito interno. Il token può non essere valido se il tenant non è registrato come servizio di gestione cloud in Configuration Manager.


### <a name="2-configuration-manager-client-token-request"></a>2. Richiesta di token del client Configuration Manager

Una volta che il client dispone di un token di Azure AD, richiede un token del client Configuration Manager.

Le voci seguenti vengono registrate in **ccmsetup.log** della macchina virtuale CMG:

``` Log
Getting CCM Token from STS server 'CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216'
Getting CCM Token from https://CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216/CCM_STS
```

#### <a name="21-cmg-gets-request"></a>2.1 CMG ottiene richiesta

Le voci seguenti vengono registrate in **IIS.log**:

``` Log
RD0003FF74XX2 10.0.0.4 GET /CCM_STS - 443 - HTTP/1.1 python-requests/2.20.0 - - 13.95.234.44 404 0 2 1477 154 15
```

#### <a name="22-cmg-forwards-request-to-cmg-connection-point"></a>2.2 CMG inoltra la richiesta al punto di connessione CMG

Le voci seguenti vengono registrate in **CMGService.log**:

``` Log
RequestUri: /CCM_PROXY_SERVERAUTH/XXXXXX037938216/CCM_STS  RequestCount: 769  RequestSize: 1081595 Bytes  ResponseCount: 769     ResponseSize: 36143 Bytes  AverageElapsedTime: 3945 ms
```

#### <a name="23-cmg-connection-point-transforms-cmg-client-request-to-management-point-client-request"></a>2.3 Il punto di connessione CMG trasforma la richiesta del client CMG in richiesta del client del punto di gestione

Le voci seguenti vengono registrate in **SMS_CLOUD_PROXYCONNECTOR.log**:

``` Log
MessageID: 3087bd34-b82c-4950-b972-e82bb0fb8385 RequestURI: https://MP.MYCORP.COM/CCM_STS EndpointName: CCM_STS ResponseHeader: HTTP/1.1 200 OK ~~ ResponseBodySize: 0 ElapsedTime: 2 ms
```

#### <a name="24-management-point-verifies-user-token-in-site-database"></a>2.4 Il punto di gestione verifica il token utente nel database del sito

Le voci seguenti vengono registrate in **CCM_STS.log**:

``` Log
Validated AAD token. TokenType: Device TenantId: XXXXe388-XXXX-485c-XXXX-e8e4eb41XXXX UserId: 00000000-0000-0000-0000-000000000000 DeviceId: 0XXXXX80-77XX-4XXa-X63X-67XXXXX64bb7 OnPrem_UserSid:  OnPrem_DeviceSid:

Return token to client, token type: UDA, hierarchyId: XXXX4f9c-XXXX-46a5-XXXX-7612c324XXXX, userId: 00000000-0000-0000-0000-000000000000, deviceId: GUID:XXXXaee9-cXXc-4ccd-XXXX-f1417d81XXX
```


## <a name="content-location-request"></a>Richiesta della posizione del contenuto

Una volta che il client ottiene una risposta con il token del client Configuration Manager, lo memorizza nella cache e lo usa per richiedere informazioni sul sito e la posizione del contenuto tramite CMG. Le voci seguenti vengono registrate in **ccmsetup.log**:

``` Log
Cached encrypted token for 'S-1-5-18'. Will expire at '00/99/2999 00:00:00'
Sending location request to 'CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216' with payload '< Request >
Appending CCM Token to the header.
```


## <a name="client-installation"></a>Installazione client

Il dispositivo scarica il contenuto del client e avvia l'installazione.

### <a name="communication-validation"></a>Convalida delle comunicazioni

- CMG convalida il token del client tramite CMG, HTTP(S) e il punto di gestione CMG e la richiesta del database del punto di gestione.
- Il client verifica il certificato di gestione o il certificato di servizio CMG
- PKI per il certificato di servizio CMG: il client richiede l'autorità di certificazione (CA) radice del certificato CMG nell'archivio locale
- Certificato di servizio CMG di terze parti: i client convalidano automaticamente un certificato con la CA radice pubblicata su Internet


## <a name="common-issues"></a>Problemi comuni

- CA radice non presente
- Controllo CRL abilitato: pubblicare l'elenco CRL su Internet o usare l'opzione **/NoCRLcheck** nella riga di comando
- Certificato di aggiunta alla rete aziendale non trovato: il client è registrato con Azure AD, ma non è aggiunto ad Azure AD

L'uso di /NoCRLCheck è adatto solo per il bootstrap ccmsetup. Perché i client siano completamente operativi, è consigliabile pubblicare l'elenco CRL su Internet. Come soluzione alternativa è possibile disabilitare il controllo CRL nella configurazione delle comunicazioni client del sito. In caso contrario, dopo che le impostazioni di sicurezza vengono aggiornate dal servizio di posizione, i client smettono di comunicare con il server.


## <a name="client-registration"></a>Registrazione client

![Diagramma del flusso di lavoro di registrazione di Azure AD](media/azure-ad-registration-workflow.png)  

### <a name="1-configuration-manager-client-request-registration"></a>1. Registrazione della richiesta del client di Configuration Manager

Le voci seguenti vengono registrate in **ClientIDManagerStartup.log**:

``` Log
[RegTask] - Client is not registered. Sending registration request for GUID:1XXXXXEF-5XX8-4XX3-XEDX-XXXFBFF78XXX ...
Registering client using AAD auth.
```

### <a name="2-configuration-manager-request-azure-ad-token-to-register-client"></a>2. Token di Azure AD della richiesta di Configuration Manager per registrare il client

Le voci seguenti vengono registrate in **ADALOperationProvider.log**:

``` Log
Getting AAD (user) token with: ClientId = f1f9b14e-XXXX-4f17-XXXX-2593f6eee91e, ResourceUrl = https://ConfigMgrService, AccountId = X49FC29A-ECE3-XXX-A3C1-XXXXXXF035A6E
Retrieved AAD token for AAD user '00000000-0000-0000-0000-000000000000'
```

#### <a name="21-configuration-manager-client-is-registered"></a>2.1 Il client di Configuration Manager viene registrato  

Le voci seguenti vengono registrate in **ClientIDManagerStartup.log**:

``` Log
[RegTask] - Client is registered. Server assigned ClientID is GUID:1XXXXXEF-5XX8-4XX3-XEDX-XXXFBFF78XXX. Approval status 3
```

> [!NOTE]  
> Durante la registrazione del client viene sempre eseguita la convalida del certificato. Questo processo avviene anche se si usa il metodo di autenticazione di Azure AD per registrare il client.


### <a name="3-configuration-manager-client-token-request"></a>3. Richiesta di token del client Configuration Manager

Dopo che il sito esegue la registrazione del client, il client richiede un token CCM. Il token CCM viene crittografato per l'account sistema locale (S-1-5-18) e memorizzato nella cache per otto ore. Dopo otto ore, il token scade e il client richiede il rinnovo del token.

Le voci seguenti vengono registrate in **ClientIDManagerStartup.log**:

``` Log
Getting CCM Token from STS server 'MP.MYCORP.COM'
Getting CCM Token from https://MP.MYCORP.COM/CCM_STS
...
Cached encrypted token for 'S-1-5-18'. Will expire at 'XX/XX/XX XX:XX:XX'
```

#### <a name="31-cmg-gets-request"></a>3.1 CMG ottiene la richiesta

Le voci seguenti vengono registrate in **IIS.log**:

``` Log
RD0003FF74XX2 10.0.0.4 GET /CCM_STS - 443 - HTTP/1.1 python-requests/2.20.0 - - 13.95.234.44 404 0 2 1477 154 15
```

#### <a name="32-cmg-forwards-request-to-cmg-connection-point"></a>3.2 CMG inoltra la richiesta al punto di connessione CMG

Le voci seguenti vengono registrate in **CMGService.log**:

``` Log
RequestUri: /CCM_PROXY_SERVERAUTH/XXXXXX037938216/CCM_STS  RequestCount: 769  RequestSize: 1081595 Bytes  ResponseCount: 769     ResponseSize: 36143 Bytes  AverageElapsedTime: 3945 ms
```

#### <a name="33-cmg-connection-point-transforms-cmg-client-request-to-management-point-client-request"></a>3.3 Il punto di connessione CMG trasforma la richiesta del client CMG in richiesta del client del punto di gestione

Le voci seguenti vengono registrate in **SMS_CLOUD_PROXYCONNECTOR.log**:

``` Log
MessageID: 3087bd34-b82c-4950-b972-e82bb0fb8385 RequestURI: https://MP.MYCORP.COM/CCM_STS EndpointName: CCM_STS ResponseHeader: HTTP/1.1 200 OK ~~ ResponseBodySize: 0 ElapsedTime: 2 ms
```

#### <a name="34-management-point-verifies-user-token-in-site-database"></a>3.4 Il punto di gestione verifica il token utente nel database del sito

Le voci seguenti vengono registrate in **CCM_STS.log**:

``` Log
Validated AAD token. TokenType: Device TenantId: XXXXe388-XXXX-485c-XXXX-e8e4eb41XXXX UserId: 00000000-0000-0000-0000-000000000000 DeviceId: 0XXXXX80-77XX-4XXa-X63X-67XXXXX64bb7 OnPrem_UserSid:  OnPrem_DeviceSid:

Return token to client, token type: UDA, hierarchyId: XXXX4f9c-XXXX-46a5-XXXX-7612c324XXXX, userId: 00000000-0000-0000-0000-000000000000, deviceId: GUID:XXXXaee9-cXXc-4ccd-XXXX-f1417d81XXX
```
