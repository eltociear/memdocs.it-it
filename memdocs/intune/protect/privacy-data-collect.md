---
title: Raccolta di dati in Intune
titleSuffix: Microsoft Intune
description: Informazioni sulla raccolta dei dati personali in Intune.
keywords: privacy, dati personali
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 09/01/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: d1171740-936d-46a5-af37-f418bd6fa63e
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: bcd7ff1ae51314bc57be2bed39c7fe8ca7114d82
ms.sourcegitcommit: e2deac196e5e79a183aaf8327b606055efcecc82
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/14/2020
ms.locfileid: "90076108"
---
# <a name="data-collection-in-intune"></a>Raccolta di dati in Intune

Quando gli utenti registrano i propri dispositivi aziendali o personali con Intune, Intune raccoglie, elabora e condivide alcuni dati personali per supportare le operazioni aziendali, condurre attività commerciali con il cliente e supportare il servizio. Intune raccoglie i dati personali dalle origini seguenti:

- utilizzo di Intune da parte degli amministratori nell'interfaccia di amministrazione di Microsoft Endpoint Manager.
- Dispositivi degli utenti finali (quando vengono registrati per la gestione in Intune e durante l'utilizzo).
- Account dei clienti per servizi di terze parti (come da istruzioni dell'amministratore).
- Informazioni di diagnostica, sulle prestazioni e sull'utilizzo.

Da queste origini, Intune raccoglie le informazioni che rientrano nelle due categorie seguenti: [dati obbligatori](#required-data), [dati facoltativi](#optional-data). In ogni categoria i dati vengono suddivisi ulteriormente in base ai dati del cliente, ai dati personali, ai dati di diagnostica e ai dati generati dal servizio. 

> [!NOTE]
> Microsoft non vende per alcun motivo a terze parti i dati raccolti dal servizio.

## <a name="required-data"></a>Dati obbligatori

I dati nella categoria obbligatoria sono costituiti da dati necessari per il funzionamento del servizio come previsto dal cliente. La maggior parte dei dati raccolti da Intune sono dati obbligatori. Questi dati sono associati a un utente, un dispositivo o un'applicazione e sono essenziali per le finalità della gestione. I dati raccolti contengono dati personali e dati non personali. I dati personali includono i dati identificabili, che possono identificare direttamente l'utente finale o i dati pseudonimizzati con un identificatore univoco generato dal sistema, usati per distribuire il servizio Enterprise agli utenti, per supportare i dati e i dati dell'account. I dati non personali includono metadati di sistema generati dal servizio e informazioni aziendali/del tenant. Intune raccoglie inoltre dati di controllo di accesso per gestire l'accesso ai ruoli e alle funzioni amministrativi tramite funzionalità come il [controllo degli accessi in base al ruolo](../fundamentals/role-based-access-control.md).

I dati obbligatori raccolti da Intune possono includere, a titolo di esempio: 

- Informazioni utente
  - Nome del proprietario/nome visualizzato dell'utente (il nome registrato in Azure dell'utente identificato con l'ID utente di Azure)
  - Nome dell'entità utente o indirizzo di posta elettronica
  - Numero di telefono
  - Identificatore dell'utente di terze parti (ad esempio ID Apple)
- Informazioni sull'inventario hardware
  - Nome del dispositivo
  - Produttore
  - Sistema operativo
  - Numero di serie
  - Numero IMEI
  - Indirizzo IP
  - MacAddress Wi-Fi
  - ICCID
- Informazioni del log di controllo, compresi i dati sulle attività seguenti
  - Gestire
  - Creazione
  - Aggiornamento (modifica)
  - Elimina
  - Assegnazione
  - Attività remote
- Informazioni di supporto
  - Informazioni di contatto (nome, numero di telefono, indirizzo di posta elettronica)
  - Comunicazioni tramite posta elettronica con membri dei team Microsoft di supporto, del prodotto e/o dell'esperienza clienti
- Informazioni sul controllo di accesso 
  - Autenticatori statici (password del cliente)
  - Chiavi di privacy per i certificati 
- Informazioni su amministratore e account
  - Nome e cognome dell'amministratore
  - Nome utente dell'amministratore
  - UPN (posta elettronica)
  - Numero di telefono
  - Indirizzo di posta elettronica del proprietario dell'account
  - ID di Active Directory di ogni amministratore IT del cliente
  - Dati di pagamento per la fatturazione del cliente
  - Chiave di sottoscrizione
- Inventario delle applicazioni, ad esempio
  - nome dell'app
  - Versione
  - ID dell'app
  - size
  - percorso di installazione
  - I dati di inventario dell'applicazione vengono raccolti solo quando contrassegnati dall'amministratore come dispositivo aziendale o quando è attivata la funzionalità per le app conformi.  
- ID tenant di terze parti del cliente (ad esempio l'ID Apple)
- Dati del dispositivo
  - ID dispositivo Intune
  - ID dispositivo di Azure Active Directory
  - ID di gestione dei dispositivi in Intune
  - ID tenant
  - ID account
  - ID dispositivo EAS
  - ID specifici della piattaforma
  - ID Apple per dispositivi iOS/iPadOS
  - Indirizzo Mac per dispositivi Mac
  - ID Windows per dispositivi Windows
- Informazioni sulle applicazioni gestite
  - ID delle applicazioni gestite
  - Tag del dispositivo delle applicazioni gestite
  - ID di gestione dei dispositivi in Intune
  - ID dispositivo di Azure Active Directory
  - Chiavi di crittografia
- Dati di utilizzo amministrativi da tutti i tenant di Intune (ad esempio, controlli amministrativi selezionati durante le interazioni con la console di amministrazione)
- Informazioni sull'account tenant (questi dati sono disponibili nel pannello di Intune)
  - Numero di dispositivi o utenti registrati
  - Numero di piattaforme per dispositivi identificate  
  - Numero di dispositivi installati
  - installedDeviceCount: numero di dispositivi in cui è installata l'applicazione.
  - notApplicableDeviceCount: numero di dispositivi per cui è l'applicazione non è applicabile.
  - notInstalledDeviceCount: numero di dispositivi per cui l'applicazione è applicabile, ma non è installata.
  - pendingInstallDeviceCount: numero di dispositivi per cui l'applicazione è applicabile e l'installazione è in sospeso.

## <a name="optional-data"></a>Dati facoltativi

I dati nella categoria facoltativa non sono essenziali per il prodotto o l'esperienza del servizio. I clienti possono controllare la raccolta di dati facoltativi. Intune consente ai clienti di acconsentire o rifiutare esplicitamente la raccolta di dati facoltativi. Esempi di dati facoltativi sono costituiti dai dati raccolti da Intune per la diagnostica e la telemetria. Si noti che ci sono motivi validi per cui gli utenti condividono questi dati facoltativi, in quanto creano opportunità per esperienze nuove e più ricche; tuttavia si comprende l'importanza di fornire agli utenti la possibilità di effettuare queste scelte in autonomia. 

Esempi di dati di diagnostica facoltativi possono includere dati sull'utilizzo delle applicazioni, errori e dati sulle prestazioni. Tutti i dati di diagnostica raccolti da Microsoft durante l'uso di qualsiasi app di Microsoft 365 per i servizi e le applicazioni aziendali vengono pseudonimizzati come definito nello standard ISO/IEC 19944:2017 (sezione 8.3.3).

## <a name="certain-end-user-data-or-content-is-never-collected"></a>Determinati dati o contenuti dell'utente finale non vengono mai raccolti

Intune non raccoglie né consente a un amministratore di visualizzare la cronologia delle chiamate o dell'esplorazione Web di utenti finali, la posta elettronica personale, i messaggi di testo, i contatti, le password per gli account personali, gli eventi del calendario o le foto, comprese quelle di un'app per foto o della fotocamera. Vedere [Introduzione alla registrazione di dispositivi](../enrollment/device-enrollment.md).

Per ulteriori informazioni sui tipi di dati e sulle definizioni, vedere [Classificazione dei dati per i servizi online di Microsoft](https://www.microsoft.com/trust-center/privacy/customer-data-definitions). 

## <a name="next-steps"></a>Passaggi successivi

Altre informazioni su come Intune [archivia ed elabora](privacy-data-store-process.md) e [condivide](privacy-data-secure-share.md) i dati personali. 
