---
title: Risolvere i problemi di Exchange Connector
titleSuffix: Microsoft Intune
description: Risoluzione dei problemi correlati a Intune On-Premises Exchange Connector.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: a7e3c742-295b-40bb-9afa-17f243062500
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3e7f9c984b81bbe98269b0123371d8097d960ffb
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2020
ms.locfileid: "86462134"
---
# <a name="troubleshoot-the-intune-exchange-connector"></a>Risolvere i problemi di Intune Exchange Connector

Questo argomento descrive come risolvere i problemi relativi a Intune Exchange Connector.

> [!IMPORTANT]
>
> A partire da luglio 2020, il supporto per Exchange Connector è deprecato e viene sostituito con l'[autenticazione moderna ibrida](https://docs.microsoft.com/office365/enterprise/hybrid-modern-auth-overview) (HMA) di Exchange ed è stata rimossa la possibilità di aggiungere un connettore Exchange a Intune.
>
> I clienti che hanno configurato in precedenza Exchange Connector e lo usano potranno contare sul supporto continuativo per il connettore.


## <a name="before-you-start"></a>Prima di iniziare

Prima di iniziare la risoluzione dei problemi relativi a Exchange Connector in Intune, raccogliere alcune informazioni di base in modo da lavorare con dati affidabili. Questo approccio può essere utile per comprendere meglio la natura del problema e risolverlo più rapidamente.

- Verificare che il processo soddisfi i requisiti di installazione. Vedere [Configurare Intune Exchange Connector locale](exchange-connector-install.md).
- Verificare che l'account in uso disponga delle autorizzazioni di amministratore sia per Exchange che per Intune.
- Annotare esattamente e in modo completo il testo del messaggio di errore, i dettagli e la posizione in cui viene visualizzato il messaggio.
- Determinare quando ha avuto inizio il problema: 
  - Si sta configurando il connettore per la prima volta? 
  - Il connettore funzionava correttamente e in seguito è stato generato un errore?
  - Se funzionava, quali modifiche sono state apportate nell'ambiente Intune, nell'ambiente Exchange o nel computer in cui è in esecuzione il software del connettore?
- Che cos'è l'autorità MDM?
- Quale versione di Exchange è in uso?

### <a name="use-powershell-to-get-more-data-on-exchange-connector-issues"></a>Usare PowerShell per ottenere più dati sui problemi relativi a Exchange Connector

- Per ottenere un elenco di tutti i dispositivi mobili per una cassetta postale, usare `Get-ActiveSyncDeviceStatistics -mailbox mbx`
- Per ottenere un elenco degli indirizzi SMTP per una cassetta postale, usare `Get-Mailbox -Identity user | select emailaddresses | fl`
- Per ottenere informazioni dettagliate sullo stato di accesso di un dispositivo, usare `Get-CASMailbox <upn> | fl`

## <a name="review-the-connector-configuration"></a>Esaminare la configurazione del connettore

Esaminare i [requisiti di On-Premises Exchange Connector](exchange-connector-install.md#intune-exchange-connector-requirements) per verificare che l'ambiente e il connettore siano configurati correttamente. 

### <a name="general-considerations-for-the-connector"></a>Considerazioni generali sul connettore

- Verificare che il firewall e i server proxy consentano la comunicazione tra il server che ospita Intune Exchange Connector e il servizio Intune.

- Il computer che ospita Intune Exchange Connector e il server Accesso client di Exchange (CAS) devono essere aggiunti a un dominio e nella stessa rete LAN. Verificare che siano state aggiunte le autorizzazioni richieste per l'account usato da Intune Exchange Connector.

- L'account di notifica viene usato per recuperare le impostazioni di *individuazione automatica*. Per altre informazioni sull'individuazione automatica in Exchange, vedere [Servizio di individuazione automatica in Exchange Server](https://docs.microsoft.com/exchange/architecture/client-access/autodiscover?view=exchserver-2016).

- Intune Exchange Connector invia una richiesta all'URL di Servizi Web Exchange usando le credenziali dell'account di notifica per inviare i messaggi di posta elettronica di notifica con il collegamento *Per iniziare* (per la registrazione in Intune). L'uso del collegamento *Per iniziare* per la registrazione è un requisito per i dispositivi Android non Knox. In caso contrario, questi dispositivi verranno bloccati dall'accesso condizionale.

### <a name="common-issues-for-connector-configurations"></a>Problemi comuni per le configurazioni del connettore

- **Autorizzazioni account**: Nella finestra di dialogo di Microsoft Intune Exchange Connector, assicurarsi di avere specificato un account utente con le autorizzazioni appropriate per eseguire i [cmdlet necessari di Windows PowerShell Exchange](exchange-connector-install.md#exchange-cmdlet-requirements).
- **Messaggi di posta elettronica di notifica**: Abilitare le notifiche e specificare un account di notifica.
- **Sincronizzazione del server Accesso client**: Quando si configura Exchange Connector, specificare un server Accesso client con la minore latenza di rete possibile rispetto al server che ospita Exchange Connector. La latenza di comunicazione tra il server Accesso client ed Exchange Connector può determinare ritardi nell'individuazione dei dispositivi, specialmente quando si usa Exchange Online dedicato.
- **Pianificazione della sincronizzazione**: Un utente con un dispositivo appena registrato potrebbe riscontrare ritardi e ottenere l'accesso solo dopo il completamento della sincronizzazione di Exchange Connector e il server Accesso client di Exchange. Una sincronizzazione completa viene eseguita una volta al giorno, mentre una sincronizzazione delta (rapida) viene eseguita più volte al giorno. È possibile [forzare manualmente una sincronizzazione rapida o una sincronizzazione completa](exchange-connector-install.md#manually-force-a-quick-sync-or-full-sync) per ridurre al minimo i ritardi.

## <a name="next-steps"></a>Passaggi successivi
Gli articoli seguenti possono essere utili per risolvere problemi comuni ed errori specifici:

- [Risolvere i problemi comuni per Intune Exchange Connector](troubleshoot-exchange-connector-common-problems.md).
- [Correggere gli errori comuni per Intune Exchange Connector](troubleshoot-exchange-connector-common-errors.md).

Ottenere assistenza dal supporto tecnico o dalla community di Intune:

- Per informazioni su come usare la console di Intune per risolvere il problema o inviare una richiesta di supporto a Microsoft, vedere [Ottenere supporto](../fundamentals/get-support.md). 
- Pubblicare il problema nei [forum di Microsoft Intune](https://social.technet.microsoft.com/Forums/en-US/home?forum=microsoftintuneprod).  
