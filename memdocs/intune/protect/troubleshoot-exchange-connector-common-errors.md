---
title: Risolvere gli errori comuni per Intune Exchange Connector
titleSuffix: Microsoft Intune
description: Risolvere i problemi e correggere gli errori comuni relativi a Microsoft Intune On-Premises Exchange Connector.
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/02/2019
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
ms.openlocfilehash: cb35fdc400c89c64b689f4695a48d201e50fc617
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "79350655"
---
# <a name="resolve-common-errors-for-the-intune-exchange-connector"></a>Correggere gli errori comuni per Intune Exchange Connector

Questo articolo può essere utile all'amministratore di Intune per risolvere errori e messaggi specifici relativi al funzionamento di Intune Exchange Connector.  

## <a name="configuration-failed-and-returned-error-code-0x0000001"></a>Configurazione non riuscita con codice di errore restituito 0x0000001

**Problema**:  
Quando si tenta di configurare Microsoft Intune Exchange Connector, viene visualizzato il messaggio di errore seguente:

```
   The Microsoft Intune Exchange Connector cannot connect to the Microsoft Exchange server.  
   The following Microsoft Exchange Server address could not be reached <Exchange server Name FQDN>  
   Verify that the FQDN of the exchange server address and credentials that you entered is correct and the server is running. The Microsoft Intune Exchange Connector does not support Exchange server arrays.  
   Error code: 0x0000001  
```

Questo problema può verificarsi se le impostazioni del proxy Internet non sono configurate correttamente.

**Risoluzione**:  
Configurare le impostazioni del proxy:
1. Contattare l'amministratore della rete locale per verificare che le impostazioni del proxy siano configurate correttamente. 
2. Usare il comando **Netsh winhttp** per configurare il server proxy e aggiungere l'elenco di esclusioni richiesto. Ad esempio:  

   ```
   Netsh winhttp set proxy proxy-server="http=proxy.corp.domain.com" bypass-list"34*.*;134.132.*.*;10.*.*;localhost;*.corp.domain.com;*.staging.domain.com"
   ```

## <a name="configuration-failed-and-returned-error-code-0x000000b"></a>Configurazione non riuscita con codice di errore restituito 0x000000b   

**Problema**:  
Quando si tenta di configurare Microsoft Intune Exchange Connector, viene visualizzato il messaggio di errore seguente:  

```
   The Microsoft Intune Exchange Connector experienced an error:  
   CertEnroll::CX509PrivateKey::Create: The system cannot find the file specified. 0x80070002 (WIN32: 2  
   ERROR_FILE_NOT_FOUND  
   Error code: 0x000000b  
```
Questo problema può verificarsi se l'account usato per accedere a Intune non è un account di amministratore globale di Intune.

**Risoluzione**:  
Accedere a Intune con un account di amministratore globale o aggiungere il proprio account al gruppo di amministratori globali. Per altre informazioni, vedere [Controllo degli accessi in base al ruolo (RBAC) con Microsoft Intune](../fundamentals/role-based-access-control.md).

## <a name="configuration-failed-and-returned-error-code-0x0000006"></a>Configurazione non riuscita con codice di errore restituito 0x0000006

**Problema**:  
Quando si tenta di configurare Microsoft Intune Exchange Connector, viene visualizzato il messaggio di errore seguente:  

```  
   The Microsoft Intune Exchange Connector cannot connect to Microsoft Intune  
   Verify that you are connected to the Internet, check the Microsoft Intune Service Status, and try to connect again.  
   Error code: 0x00000006  
```  
Questo errore può verificarsi se per la connessione a Internet viene usato un server proxy che blocca il traffico verso il servizio Intune. Per determinare se è in uso un proxy, passare a **Pannello di controllo** > **Opzioni Internet**, selezionare la scheda **Connessione** e quindi fare clic su **Impostazioni LAN**.

**Risoluzione**:  

- **Opzione 1**: rimuovere le impostazioni del proxy per consentire al computer di connettersi a Internet senza usare il proxy.  

- **Opzione 2**: configurare il server proxy per consentire la comunicazione con il servizio Intune, come documentato in [Requisiti per Intune Exchange Connector](exchange-connector-install.md#intune-exchange-connector-requirements).



## <a name="event-7000-or-7041-microsoft-intune-exchange-connector-service-wont-start"></a>Evento 7000 o 7041: avvio del servizio Microsoft Intune Exchange Connector non riuscito

**Problema**:  
Un dispositivo iOS non riesce a eseguire la registrazione in Intune e genera uno dei messaggi di errore seguenti:  

```  
   Log Name:      System
   Source:            Service Control Manager
   Date:               <time>
   Task Category: None
   Level:               Error
   Keywords:        Classic
   User:                N/A
   Computer:      <computer>
   Description:
   The Microsoft Intune Exchange Connector Service service failed to start because of the following error:  
   The service did not start because of a logon failure.
```  

```  
   Log Name:      System
   Source:            Service Control Manager
   Date:               <time>
   Event ID:          7041
   Task Category: None
   Level:               Error   
   Keywords:        Classic
   User:                N/A
   Computer:       <computer>
   Description:
   The WIEC service was unable to log on as .\WIEC_USER with the currently configured password because of the following error:
   Logon failure: the user has not been granted the requested logon type at this computer.
   Service: WIEC
   Domain and account: .\WIEC_USER
   This service account does not have the required user right "Log on as a service."  
```
Questo problema può verificarsi se l'account **WIEC_User** non dispone del diritto utente **Accesso come servizio** nei criteri locali.

**Risoluzione**:  
Nel computer in cui è in esecuzione Intune Exchange Connector assegnare il diritto utente **Accesso come servizio** all'account del servizio **WIEC_User**. Se il computer è un nodo di un cluster, assicurarsi di assegnare il diritto utente *Accesso come servizio* all'account del servizio cluster in tutti i nodi del cluster.  

Per assegnare il diritto utente **Accesso come servizio** direttamente all'account del servizio **WIEC_User** nel computer, attenersi alla seguente procedura:

1. Accedere al computer come amministratore o membro del gruppo Administrators.
2. Eseguire **secpol.msc** per aprire Criteri di sicurezza locali.
3. Passare a **Impostazioni sicurezza** > **Criteri locali** e quindi selezionare **Assegnazione diritti utente**.
4. Nel riquadro a destra fare doppio clic su **Accesso come servizio**.
5. Selezionare **Aggiungi utente o gruppo**, aggiungere **WIEC_USER** ai criteri e quindi selezionare due volte **OK**.

Se il diritto utente **Accesso come servizio** è stato assegnato a **WIEC_User** ma è stato rimosso in seguito, contattare l'amministratore di dominio per determinare se viene sovrascritto da un'impostazione di Criteri di gruppo.  

## <a name="next-steps"></a>Passaggi successivi  

L'articolo seguente può essere utile per risolvere errori specifici:
- [Risolvere i problemi comuni per Intune Exchange Connector](troubleshoot-exchange-connector-common-problems.md).git 

Ottenere assistenza dal supporto tecnico o dalla community di Intune.
- Per informazioni su come usare la console di Intune per risolvere il problema o inviare una richiesta di supporto a Microsoft, vedere [Ottenere supporto](../fundamentals/get-support.md). 
- Pubblicare il problema nei [forum di Microsoft Intune](https://social.technet.microsoft.com/Forums/en-US/home?forum=microsoftintuneprod).  
