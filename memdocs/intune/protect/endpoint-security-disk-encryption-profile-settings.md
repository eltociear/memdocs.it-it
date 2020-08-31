---
title: Impostazioni dei criteri di crittografia del disco per la sicurezza degli endpoint di Intune | Microsoft Docs
description: Impostazioni dei criteri di crittografia del disco per la sicurezza degli endpoint per BitLocker e FileVault di Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 37e9f68951c3576393e6ed3eb3346847029736c4
ms.sourcegitcommit: 46d4bc4fa73b22ae2a6a17a2d1cc6ec933a50e89
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88663209"
---
# <a name="disk-encryption-policy-settings-for-endpoint-security-in-intune"></a>Impostazioni dei criteri di crittografia del disco per la sicurezza degli endpoint di Intune

Visualizzare le impostazioni che è possibile configurare nei profili per i criteri di *crittografia del disco* nel nodo Sicurezza degli endpoint di Intune come parte dei [criteri di sicurezza degli endpoint](../protect/endpoint-security-policy.md).

Piattaforme e profili supportati:

- **macOS**:
  - Profilo: **FileVault**
- **Windows 10 e versioni successive**:
  - Profilo: **BitLocker**

## <a name="filevault"></a>FileVault

### <a name="encryption"></a>Crittografia

**Abilita FileVault**  
- **Non configurato** (*impostazione predefinita*)
- **Sì**: abilita la crittografia del disco completo usando XTS-AES 128 con FileVault nei dispositivi che eseguono macOS 10.13 o versioni successive. FileVault è abilitato quando l'utente si disconnette dal dispositivo.

  Quando è impostato su *Sì*,è possibile configurare impostazioni aggiuntive per FileVault.

  - **Tipo di chiave di ripristino**
    Le chiavi di ripristino create per i dispositivi sono di tipo *chiave personale*. Configurare le impostazioni seguenti per la chiave personale:

    - **Rotazione della chiave di ripristino personale**  
      Consente di specificare la frequenza con cui verrà eseguita la rotazione della chiave di ripristino personale per un dispositivo. È possibile selezionare il valore predefinito **Non configurato** oppure un valore compreso tra **1** e **12** mesi.
    - **Descrizione della posizione del deposito della chiave di ripristino personale**  
      Consente di digitare un breve messaggio per l'utente per spiegare come e dove poter recuperare la chiave di ripristino personale. Il testo digitato viene inserito nel messaggio visualizzato nella schermata di accesso quando all'utente viene richiesto di immettere la chiave di ripristino personale nel caso in cui abbia dimenticato la password.

  - **Numero di volte per cui è consentito ignorare**  
    Consente di impostare il numero di volte per cui un utente può ignorare le richieste di abilitazione di FileVault prima che FileVault venga reso obbligatorio per l'accesso dell'utente.
    - **Non configurato** (*impostazione predefinita*): viene richiesta la crittografia del dispositivo prima che sia consentito l'accesso successivo.
    - Da **1** a **10** - Consente a un utente di ignorare la richiesta per un numero di volte compreso tra 1 e 10 prima che venga richiesta la crittografia nel dispositivo.
    - **Nessun limite, richiedi sempre**: all'utente viene richiesto di abilitare FileVault, ma non viene mai richiesta la crittografia.

  - **Consenti il differimento fino alla disconnessione**  
    - **Non configurato** (*impostazione predefinita*)
    - **Sì**: rinvia la richiesta di abilitazione di FileVault fino a quando l'utente non si disconnette.  

  - **Disabilita la richiesta alla disconnessione**  
    Consente di impedire che all'utente venga richiesta l'abilitazione di FileVault al momento della disconnessione. Se questo parametro è impostato su Disabilita, la richiesta non viene visualizzata al momento della disconnessione ma in fase di accesso.
    - **Non configurato** (*impostazione predefinita*)
    - **Sì**: disabilita la richiesta di abilitazione di FileVault visualizzata al momento della disconnessione.

  - **Nascondi la chiave di ripristino**  
     Nascondere la chiave di ripristino personale dall'utente del dispositivo macOS durante la crittografia. Dopo la crittografia del disco, un utente può usare qualsiasi dispositivo per visualizzare la chiave di ripristino personale tramite il sito Web Portale aziendale Intune o l'app Portale aziendale in una piattaforma supportata.
    - **Non configurato** (*impostazione predefinita*)
    - **Sì** - Consente di nascondere la chiave di ripristino personale durante la crittografia del dispositivo.

## <a name="bitlocker"></a>BitLocker

### <a name="bitlocker--base-settings"></a>Impostazioni di base di BitLocker

- **Abilita la crittografia completa del disco per le unità del sistema operativo e le unità dati fisse**  
  CSP: [RequireDeviceEncryption](https://go.microsoft.com/fwlink/?linkid=872523)

  Se l'unità è stata crittografata prima dell'applicazione di questo criterio, non viene eseguita alcuna azione aggiuntiva. Se le opzioni e il metodo di crittografia corrispondono a quelli di questo criterio, la configurazione dovrebbe avere esito positivo. Se un'opzione di configurazione BitLocker attiva non corrisponde a questo criterio, la configurazione restituirà probabilmente un errore.
  
  Per applicare questo criterio a un disco già crittografato, decrittografare l'unità e riapplicare i criteri MDM. Per impostazione predefinita, Windows non richiede la crittografia dell'unità BitLocker. Tuttavia per la registrazione o l'accesso con aggiunta ad Azure AD e ad account Microsoft (MSA) potrebbe essere applicata automaticamente la crittografia abilitando BitLocker con crittografia XTS-AES a 128 bit.

  - **Non configurato** (*impostazione predefinita*): BitLocker non viene imposto.
  - **Sì**: impone l'uso di BitLocker.

- **Richiedi la crittografia delle schede di memoria (solo dispositivi mobili)**  
  CSP: [RequireStorageCardEncryption](https://go.microsoft.com/fwlink/?linkid=872524)

  Questa impostazione si applica solo ai dispositivi con SKU Windows Mobile e Mobile Enterprise.
  - **Non configurato** (*impostazione predefinita*): viene ripristinata l'impostazione predefinita del sistema operativo, che non richiede la crittografia delle schede di memoria.
  - **Sì**: la crittografia delle schede di memoria è obbligatoria per i dispositivi mobili.

  > [!NOTE]
  > Il supporto per [Windows 10 Mobile](https://support.microsoft.com/help/4485197/windows-10-mobile-end-of-support-faq) e [Windows Phone 8.1](https://support.microsoft.com/help/4036480/windows-phone-8-1-end-of-support-faq) è terminato ad agosto 2020.

- **Nascondi richiesta di crittografia di terze parti**  
  CSP: [AllowWarningForOtherDiskEncryption](https://go.microsoft.com/fwlink/?linkid=872525)

  Se BitLocker è abilitato in un sistema già crittografato da un prodotto di crittografia di terze parti, potrebbe rendere inutilizzabile il dispositivo. Può verificarsi una perdita di dati e potrebbe essere necessario reinstallare Windows. Si consiglia di non abilitare mai BitLocker in un dispositivo in cui è installata o abilitata la crittografia di terze parti.

  Per impostazione predefinita, la configurazione guidata di BitLocker richiede agli utenti di confermare che non è presente alcuna crittografia di terze parti.

  - **Non configurato** (*impostazione predefinita*): la configurazione guidata di BitLocker visualizza un avviso e richiede agli utenti di confermare che non è presente alcuna crittografia di terze parti.
  - **Sì**: nasconde la richiesta di installazione guidata di BitLocker agli utenti.

  Se sono necessarie le funzionalità di abilitazione invisibile di BitLocker, l'avviso di crittografia di terze parti deve essere nascosto perché qualsiasi richiesta interrompe i flussi di lavoro di abilitazione invisibile all'utente.

  Se impostato su *Sì*, è possibile configurare le impostazioni seguenti:

  - **Consenti agli utenti standard di abilitare la crittografia durante Autopilot**  
    CSP: [AllowStandardUserEncryption](https://go.microsoft.com/fwlink/?linkid=2114200)
    - **Non configurato** (*impostazione predefinita*): durante gli scenari di abilitazione invisibile di Azure Active Directory Join (AADJ), non è necessario che gli utenti siano amministratori locali per abilitare BitLocker.
    - **Sì**: l'impostazione viene lasciata come impostazione predefinita del client, ovvero è richiesto l'accesso dell'amministratore locale per abilitare BitLocker.

    Per gli scenari di abilitazione e Autopilot non invisibili, l'utente deve essere un amministratore locale per completare la configurazione guidata di BitLocker.

- **Attivazione delle password di ripristino basata su client per**  
  CSP: [ConfigureRecoveryPasswordRotation](https://go.microsoft.com/fwlink/?linkid=2114201)

  Per la rotazione delle chiavi non sono supportati i dispositivi di aggiunta dell'account aziendale (AWA, formalmente aggiunti all'area di lavoro).
  - **Non configurato** (*impostazione predefinita*): il client non ruoterà le chiavi di ripristino di BitLocker.
  - **Disabilitato**
  - **Dispositivi aggiunti ad Azure AD**
  - **Dispositivi aggiunti ad Azure AD e ad AD ibrido**

### <a name="bitlocker---fixed-drive-settings"></a>Impostazioni dell'unità fissa di BitLocker

- **BitLocker - Impostazioni dell'unità fissa**  
  [Impostazioni di Criteri di gruppo di BitLocker](https://go.microsoft.com/fwlink/?linkid=2067018)

  - **Ripristino delle unità fisse**  
    CSP: [FixedDrivesRecoveryOptions](https://go.microsoft.com/fwlink/?linkid=872538)

    Controllare il modo in cui le unità dati fisse protette da BitLocker vengono ripristinate in assenza delle informazioni necessarie sulla chiave di avvio.

    - **Non configurato** (*impostazione predefinita*): le opzioni di ripristino predefinite sono supportate, compreso l'agente di recupero dei dati (DRA). L'utente finale può specificare le opzioni di ripristino e le informazioni di ripristino non sono salvate in Azure Active Directory.
    - **Configura**: abilita l'accesso per configurare diverse tecniche di ripristino delle unità.

    Con l'opzione *Configura* sono disponibili le impostazioni seguenti:

    - **Creazione della chiave di ripristino da parte dell'utente**  
      - **Bloccato** (*impostazione predefinita*)
      - **Richiesto**
      - **È consentito**

    - **Configura il pacchetto di ripristino di BitLocker**
      - **Password and key (Password e chiave)** (*impostazione predefinita*): include sia la password di ripristino di BitLocker usata dagli amministratori e dagli utenti per sbloccare le unità protette che i pacchetti della chiavi di ripristino usati dagli amministratori per ripristinare i dati in Active Directory.
      - **Password only (Solo password)** : i pacchetti della chiave di ripristino potrebbero non essere accessibili quando necessario.

    - **Richiedi il backup delle informazioni di ripristino in Azure AD al dispositivo**
      - **Non configurato** (*impostazione predefinita*): l'abilitazione di BitLocker verrà completata anche se il backup della chiave di ripristino in Azure AD non riesce. Questo può comportare che le informazioni di ripristino non siano archiviate all'esterno.
      - **Sì**: BitLocker non completerà l'abilitazione fino a quando le chiavi di ripristino non saranno state salvate correttamente in Azure Active Directory.

    - **Creazione della password di ripristino da parte dell'utente**  
      - **Bloccato** (*impostazione predefinita*)
      - **Richiesto**
      - **È consentito**

    - **Nascondi le opzioni di ripristino aggiuntive durante la configurazione di BitLocker**
      - **Non configurato** (*impostazione predefinita*): consente all'utente di accedere a opzioni di ripristino aggiuntive.
      - **Sì**: impedisce all'utente finale di scegliere opzioni di ripristino aggiuntive, ad esempio la stampa di chiavi di ripristino durante la configurazione guidata di BitLocker.

    - **Abilita BitLocker dopo il ripristino delle informazioni da archiviare**
      - **Non configurato** (*impostazione predefinita*)  
      - **Sì**

    - **Blocca l'uso dell'agente di recupero dati (DRA) basato su certificati**
      - **Non configurato** (*impostazione predefinita*): consente l'uso del DRA per la configurazione. Per configurare il DRA è necessario disporre di un'infrastruttura a chiave pubblica dell'organizzazione e di oggetti Criteri di gruppo per distribuire i certificati e l'agente DRA.
      - **Sì**: impedisce di usare l'agente di recupero dati per ripristinare le unità abilitate per BitLocker.

  - **Blocca l'accesso in scrittura alle unità dati fisse non protette tramite BitLocker**  
    CSP: [FixedDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872534)  
    Questa impostazione è disponibile quando *BitLocker - Impostazioni dell'unità fissa* è impostato su *Configura*.

    - **Non configurato** (*impostazione predefinita*) - I dati possono essere scritti in unità fisse non crittografate.
    - **Sì**: Windows non consente la scrittura di dati in unità fisse non protette da BitLocker. Se un'unità fissa non è crittografata, l'utente dovrà completare la configurazione guidata di BitLocker per l'unità prima che venga concesso l'accesso in scrittura.

  - **Configura il metodo di crittografia per le unità dati fisse**  
    CSP: [EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  

    Configurare il metodo di crittografia e il livello di codifica per i dischi di unità dati fisse. *XTS-AES a 128 bit* è il metodo di crittografia predefinito di Windows e il valore consigliato.

    - **Non configurato** (*impostazione predefinita*)
    - **AES 128bit CBC**
    - **AES 256bit CBC**
    - **AES 128bit XTS**
    - **AES 256bit XTS**

### <a name="bitlocker---os-drive-settings"></a>Impostazioni delle unità del sistema operativo di BitLocker

- **Criterio Unità di sistema BitLocker**  
  CSP: [Impostazioni di Criteri di gruppo di BitLocker](https://go.microsoft.com/fwlink/?linkid=2067025)

  - **Configura** (*impostazione predefinita*)  
  - **Non configurato**

  Se impostato su *Configura*, è possibile configurare le impostazioni seguenti:

  - **Autenticazione all'avvio obbligatoria**  
    CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

    - **Non configurato** (*impostazione predefinita*)
    - **Sì**: configura i requisiti di autenticazione aggiuntivi all'avvio del sistema, tra cui l'utilizzo di requisiti per Trusted Platform Module (TPM) o per il PIN di avvio.

    Se impostata su *Sì*, è possibile configurare le impostazioni seguenti:

    - **Avvio TPM compatibile**  
      CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      È consigliabile richiedere un TPM per BitLocker. Questa impostazione si applica solo quando si abilita prima BitLocker e non ha alcun effetto se BitLocker è già abilitato.

      - **Bloccato** (*impostazione predefinita*): BitLocker non usa il TPM.
      - **Richiesto**: BitLocker è abilitato sono in presenza di un TPM utilizzabile.
      - **È consentito**: BitLocker usa il TPM se è presente.

    - **PIN di avvio TPM compatibile**  
      CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      - **Bloccato** (*impostazione predefinita*): blocca l'uso di un PIN.
      - **Richiesto**: è necessario che siano presenti un PIN e un TPM per abilitare BitLocker.
      - **È consentito**: BitLocker usa il TPM se è presente e consente all'utente di configurare un PIN di avvio.

      Per gli scenari di abilitazione invisibile, è necessario impostare il valore su *Bloccato*. Gli scenari di abilitazione invisibile (incluso Autopilot) non avranno esito positivo quando è necessaria l'interazione dell'utente.

    - **Chiave di avvio TPM compatibile**  
      CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      - **Bloccato** (*impostazione predefinita*): blocca l'uso di chiavi di avvio.
      - **Richiesto**: è necessario che siano presenti una chiave di avvio e un TPM per abilitare BitLocker.
      - **È consentito**: BitLocker usa il TPM se è presente e consente la presenza di una chiave di avvio, ad esempio un'unità USB, per sbloccare le unità.

      Per gli scenari di abilitazione invisibile, è necessario impostare il valore su *Bloccato*. Gli scenari di abilitazione invisibile (incluso Autopilot) non avranno esito positivo quando è necessaria l'interazione dell'utente.

    - **Chiave di avvio e PIN TPM compatibile**  
      CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      - **Bloccato** (*impostazione predefinita*): impedisce l'uso di una combinazione di chiave di avvio e PIN.
      - **Richiesto**: è necessario che BitLocker disponga di una chiave di avvio e di un PIN per essere abilitato.
      - **È consentito**: BitLocker usa il TPM se è presente e consente la combinazione di un PIN di una chiave di avvio.

      Per gli scenari di abilitazione invisibile, è necessario impostare il valore su *Bloccato*. Gli scenari di abilitazione invisibile (incluso Autopilot) non avranno esito positivo quando è necessaria l'interazione dell'utente.

    - **Disabilita BitLocker nei dispositivi in cui TPM non è compatibile**  
    CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      Se non è presente alcun TPM, BitLocker richiede una password o un'unità USB per l'avvio.

      Questa impostazione si applica solo quando si abilita prima BitLocker e non ha alcun effetto se BitLocker è già abilitato.

      - **Non configurato** (*impostazione predefinita*)
      - **Sì**: impedisce la configurazione di BitLocker senza un chip TPM compatibile.

    - **Abilita il messaggio e l'URL di ripristino prima dell'avvio**  
      CSP: [SystemDrivesRecoveryMessage](https://go.microsoft.com/fwlink/?linkid=872530)configure

      - **Non configurato** (*impostazione predefinita*): usa le informazioni predefinite di ripristino preliminare BitLocker.
      - **Sì**: abilita la configurazione di un messaggio e un URL di ripristino prima dell'avvio personalizzati per aiutare gli utenti a trovare la password di ripristino. Il messaggio e l'URL prima dell'avvio vengono visualizzati dagli utenti quando sono bloccati dal PC in modalità di ripristino.

      Se impostata su *Sì*, è possibile configurare le impostazioni seguenti:

      - **Messaggio di ripristino prima dell'avvio**  
        Specificare un messaggio di ripristino prima dell'avvio personalizzato.

      - **URL di ripristino prima dell'avvio**  
        Specificare un URL di ripristino prima dell'avvio personalizzato.

    - **Ripristino delle unità di sistema**  
      CSP: [SystemDrivesRecoveryOptions](https://go.microsoft.com/fwlink/?linkid=872529)

      - **Non configurato** (*impostazione predefinita*)  
      - **Configurare**: abilita la configurazione di impostazioni aggiuntive.

      Con l'opzione *Configura* sono disponibili le impostazioni seguenti:

      - **Creazione della chiave di ripristino da parte dell'utente**  
        - **Bloccato** (*impostazione predefinita*)
        - **Richiesto**
        - **È consentito**

      - **Configura il pacchetto di ripristino di BitLocker**
        - **Password and key (Password e chiave)** (*impostazione predefinita*): include sia la password di ripristino di BitLocker usata dagli amministratori e dagli utenti per sbloccare le unità protette che i pacchetti della chiavi di ripristino usati dagli amministratori per ripristinare i dati in Active Directory.
        - **Password only (Solo password)** : i pacchetti della chiave di ripristino potrebbero non essere accessibili quando necessario.

      - **Richiedi il backup delle informazioni di ripristino in Azure AD al dispositivo**
        - **Non configurato** (*impostazione predefinita*): l'abilitazione di BitLocker verrà completata anche se il backup della chiave di ripristino in Azure AD non riesce. Questo può comportare che le informazioni di ripristino non siano archiviate all'esterno.
        - **Sì**: BitLocker non completerà l'abilitazione fino a quando le chiavi di ripristino non saranno state salvate correttamente in Azure Active Directory.

      - **Creazione della password di ripristino da parte dell'utente**  
        - **Bloccato** (*impostazione predefinita*)
        - **Richiesto**
        - **È consentito**

      - **Nascondi le opzioni di ripristino aggiuntive durante la configurazione di BitLocker**
        - **Non configurato** (*impostazione predefinita*): consente all'utente di accedere a opzioni di ripristino aggiuntive.
        - **Sì**: impedisce all'utente finale di scegliere opzioni di ripristino aggiuntive, ad esempio la stampa di chiavi di ripristino durante la configurazione guidata di BitLocker.

      - **Abilita BitLocker dopo il ripristino delle informazioni da archiviare**
        - **Non configurato** (*impostazione predefinita*)  
        - **Sì**

      - **Blocca l'uso dell'agente di recupero dati (DRA) basato su certificati**
        - **Non configurato** (*impostazione predefinita*): consente l'uso del DRA per la configurazione. Per configurare il DRA è necessario disporre di un'infrastruttura a chiave pubblica dell'organizzazione e di oggetti Criteri di gruppo per distribuire i certificati e l'agente DRA.
        - **Sì**: impedisce di usare l'agente di recupero dati per ripristinare le unità abilitate per BitLocker.

    - **Lunghezza minima del PIN**  
      CSP: [SystemDrivesMinimumPINLength](https://go.microsoft.com/fwlink/?linkid=872528)

      Specifica la lunghezza minima del PIN di avvio quando sono necessari TPM e PIN durante l'abilitazione di BitLocker. La lunghezza del PIN deve essere compresa tra 4 e 20 caratteri.

      Se tale impostazione non è configurata, gli utenti possono configurare un PIN di avvio di qualsiasi lunghezza compresa tra 4 e 20 cifre.

      Questa impostazione si applica solo quando si abilita prima BitLocker e non ha alcun effetto se BitLocker è già abilitato.

  - **Configura il metodo di crittografia per le unità del sistema operativo**  
   CSP: [EncryptionMethodByDriveType]( https://go.microsoft.com/fwlink/?linkid=872526)

    Configurare il metodo di crittografia e il livello di codifica per le unità di sistema. *XTS-AES a 128 bit* è il metodo di crittografia predefinito di Windows e il valore consigliato.

    - **Non configurato** (*impostazione predefinita*)
    - **AES 128bit CBC**
    - **AES 256bit CBC**
    - **AES 128bit XTS**
    - **AES 256bit XTS**

### <a name="bitlocker---removable-drive-settings"></a>Impostazioni dell'unità rimovibile di BitLocker

- **Configura il metodo di crittografia per le unità del sistema operativo**  
  CSP: [Impostazioni di Criteri di gruppo di BitLocker](https://go.microsoft.com/fwlink/?linkid=2067140)

  - **Non configurato** (*impostazione predefinita*)  
  - **Configurare un**

  Se impostato su *Configura*, è possibile configurare le impostazioni seguenti:

  - **Configura il metodo di crittografia per le unità dati rimovibili**  
    CSP: [EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)

    Selezionare il metodo di crittografia desiderato per le unità dati rimovibili.

    - **Non configurato** (*impostazione predefinita*)
    - **AES 128bit CBC**
    - **AES 256bit CBC**
    - **AES 128bit XTS**
    - **AES 256bit XTS**

  - **Blocca l'accesso in scrittura alle unità dati rimovibili non protette tramite BitLocker**  
    CSP: [RemovableDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872540)

    - **Non configurato** (*impostazione predefinita*) - I dati possono essere scritti in unità rimovibili non crittografate.
    - **Sì**: Windows non consente la scrittura di dati in unità rimovibili non protette da BitLocker. Se un'unità rimovibile non è crittografata, l'utente deve completare la configurazione guidata di BitLocker per l'unità prima che venga concesso l'accesso in scrittura.

    - **Blocca l'accesso in scrittura alle unità dati rimovibili non protette tramite BitLocker**  
      CSP: [RemovableDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872540)

      - **Non configurato** (*impostazione predefinita*): può essere usata qualsiasi unità BitLocker crittografata.
      - **Sì**: blocca l'accesso alle unità rimovibili a meno che non siano state crittografate in un computer di proprietà dell'organizzazione.

## <a name="next-steps"></a>Passaggi successivi

[Criteri di sicurezza degli endpoint per la crittografia del disco](../protect/endpoint-security-disk-encryption-policy.md)
