---
title: Impostazioni dei dispositivi iOS/iPadOS in Microsoft Intune - Azure | Microsoft Docs
titleSuffix: ''
description: Aggiungere, configurare o creare le impostazioni nei dispositivi iOS/iPadOS per limitare l'uso delle funzionalità, tra cui impostare i requisiti per le password, controllare la schermata di blocco, usare le app predefinite, aggiungere app con restrizioni o approvate, gestire i dispositivi Bluetooth, connettersi al cloud per backup e archiviazione, abilitare la modalità tutto schermo, aggiungere domini e controllare il modo in cui gli utenti interagiscono con il Web browser Safari in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/16/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: ea0968d15572fa9c3bde1e4d133dcb8b4c980274
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/21/2020
ms.locfileid: "80087041"
---
# <a name="ios-and-ipados-device-settings-to-allow-or-restrict-features-using-intune"></a>Impostazioni dei dispositivi iOS e iPadOS per consentire o limitare l'uso delle funzionalità tramite Intune

Questo articolo descrive le diverse impostazioni che è possibile controllare nei dispositivi iOS e iPadOS. Usare queste impostazioni nella propria soluzione di gestione di dispositivi mobili (MDM) per abilitare o disabilitare funzionalità, impostare regole per le password, consentire o limitare l'uso di app specifiche e altro ancora.

Queste impostazioni vengono aggiunte a un profilo di configurazione del dispositivo in Intune e quindi assegnate o distribuite ai dispositivi iOS/iPadOS.

> [!TIP]
> Queste impostazioni usano le impostazioni MDM di Apple. Per altre informazioni su queste impostazioni, vedere [Impostazioni per la gestione dei dispositivi mobili](https://support.apple.com/guide/mdm/welcome/web). Si aprirà il sito Web di Apple.

## <a name="before-you-begin"></a>Prima di iniziare

[Creare un profilo di configurazione delle restrizioni del dispositivo](device-restrictions-configure.md).

> [!NOTE]
> Queste impostazioni si applicano a diversi tipi di registrazione, con alcune impostazioni che si applicano a tutte le opzioni di registrazione. Per altre informazioni sui diversi tipi di registrazione, vedere [Registrazione di iOS/iPadOS](../enrollment/ios-enroll.md).

## <a name="general"></a>Generale

### <a name="settings-apply-to-all-enrollment-types"></a>Le impostazioni si applicano a: Tutti i tipi di registrazione

- **Condividi i dati di utilizzo**: **Blocca** impedisce al dispositivo di inviare dati di diagnostica e di utilizzo ad Apple. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'invio di questi dati.

- **Acquisizione schermo**: **Blocca** impedisce la creazione di screenshot o acquisizioni di schermate nel dispositivo. In iOS/iPadOS 9.0 e versioni successive blocca anche le registrazioni dello schermo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita il sistema operativo può consentire agli utenti di acquisire il contenuto dello schermo come immagine o come video.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Le impostazioni si applicano a: Registrazione del dispositivo, Registrazione automatica dei dispositivi (con supervisione)

- **Certificati TLS non attendibili**: **Blocca** non consente i certificati TLS (Transport Layer Security) non attendibili nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire i certificati TLS.
- **Blocca gli aggiornamenti PKI in modalità wireless**: **Blocca** impedisce agli utenti di ricevere gli aggiornamenti software a meno che il dispositivo non sia connesso a un computer. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire a un dispositivo di ricevere gli aggiornamenti software senza essere connesso a un computer.
- **Limita il rilevamento annunci**: scegliere **Limita** per disabilitare l'identificatore di annunci pubblicitari del dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe mantenere abilitata l'impostazione.
- **Attendibilità dell'app aziendale**: **Blocca** rimuove il pulsante **Attendibilità di Enterprise Developer** in Impostazioni > Generale > Gestione di profili e dispositivi nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di scegliere se considerare attendibili le app che non vengono scaricate da App Store.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Le impostazioni si applicano a: Registrazione automatica dei dispositivi (supervisione)

- **Modifica delle impostazioni di invio dei dati di diagnostica**: **Blocca** impedisce agli utenti di modificare le impostazioni di invio dei dati di diagnostica e di analisi delle app in **Diagnostica e utilizzo** (impostazioni del dispositivo). Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di modificare queste impostazioni del dispositivo.

  Per usare questa impostazione, impostare l'opzione **Condividi i dati di utilizzo** su **Blocca**.

  Questa funzionalità si applica a:  
  - iOS 9.3.2 e versioni successive
  - iPadOS 13.0 e versioni successive

- **Osservazione schermo remoto da parte dell'app Classroom**: **Blocca** impedisce all'app Classroom di visualizzare lo schermo del dispositivo da remoto. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire all'app Classroom di Apple di visualizzare lo schermo.

  Per usare questa impostazione, impostare l'opzione **Acquisizione schermo** su **Blocca**.

  Questa funzionalità si applica a:  
  - iOS 9.3 e versioni successive
  - iPadOS 13.0 e versioni successive

- **Osservazione schermo non richiesta da parte dell'app Classroom**: Se impostata su **Consenti**, gli insegnanti possono osservare lo schermo dei dispositivi iOS/iPadOS degli studenti con l'app Classroom senza che questi ne siano a conoscenza. I dispositivi degli studenti registrati in una classe con l'app Classroom concedono automaticamente l'autorizzazione al docente del corso. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe bloccare questa funzionalità.

  Per usare questa impostazione, impostare l'opzione **Acquisizione schermo** su **Blocca**.

- **Modifica dell'account**: se è impostata su **Blocca**, gli utenti non possono aggiornare le impostazioni specifiche del dispositivo dall'app delle impostazioni iOS/iPadOS. Ad esempio, gli utenti non possono creare nuovi account di dispositivo o modificare il nome utente o la password. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di modificare queste impostazioni.

  Questa funzionalità si applica anche alle impostazioni accessibili dall'app delle impostazioni iOS/iPadOS, ad esempio Posta elettronica, Contatti, Calendario, Twitter e altro ancora. Non si applica alle app con impostazioni dell'account non configurabili dall'app delle impostazioni iOS/iPadOS, ad esempio Microsoft Outlook.

- **Orario schermo**: **Blocca** impedisce agli utenti di impostare le proprie restrizioni in Orario schermo (impostazioni del dispositivo). Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di configurare restrizioni nel dispositivo, ad esempio il controllo genitori o le restrizioni relative a contenuti e privacy.

  Questa impostazione è stata rinominata da **Abilitazione delle restrizioni nelle impostazioni del dispositivo**. Impatto della modifica:  
  
  - iOS 11.4.1 e versioni precedenti: **Blocca** impedisce agli utenti di impostare le proprie restrizioni nelle impostazioni del dispositivo. Il comportamento rimane invariato. Non si verifica nessun cambiamento per gli utenti.
  - iOS 12.0 e versioni successive: **Blocca** impedisce agli utenti di impostare un **Orario schermo** personalizzato nelle impostazioni del dispositivo (Impostazioni > Generale > Orario schermo), incluse restrizioni relative a contenuti e privacy. Nei dispositivi aggiornati a iOS 12.0 non verrà più visualizzata la scheda delle restrizioni nelle impostazioni del dispositivo (Impostazioni > Generale > Gestione dei dispositivi > Profilo di gestione > Restrizioni). Queste impostazioni sono in **Orario schermo**.
  
- **Uso dell'opzione di cancellazione di tutti i contenuti e tutte le impostazioni sul dispositivo**: scegliere **Blocca** per impedire agli utenti di usare l'opzione di cancellazione di tutti i contenuti e tutte le impostazioni nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di accedere a queste impostazioni.
- **Modifica del nome dispositivo**: scegliere **Blocca** per impedire la modifica del nome del dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di modificare il nome del dispositivo.
- **Modifica delle impostazioni di notifica**: scegliere **Blocca** per impedire la modifica delle impostazioni di notifica. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di modificare le impostazioni di notifica del dispositivo.
- **Modifica dello sfondo**: **Blocca** impedisce di cambiare lo sfondo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di modificare lo sfondo del dispositivo.
- **Modifiche al profilo di configurazione**: **Blocca** impedisce di apportare modifiche al profilo di configurazione nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di installare profili di configurazione.
- **Blocco attivazione**: Scegliere **Consenti** per abilitare il blocco attivazione su dispositivi iOS/iPadOS con supervisione. Blocco attivazione rende più difficile la riattivazione di un dispositivo perso o rubato.
- **Blocca la rimozione di app**: **Blocca** impedisce agli utenti di rimuovere le app. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di rimuovere le app dal dispositivo.
- **Consenti gli accessori USB durante il blocco del dispositivo**: Selezionando **Consenti** gli accessori USB sono autorizzati a scambiare dati con un dispositivo che è rimasto bloccato per più di un'ora. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe non aggiornare la modalità con restrizioni USB nel dispositivo e impedire agli accessori USB di trasferire i dati dal dispositivo se questo rimane bloccato per più di un'ora.
- **Imponi data e ora automatiche**: **Rendi obbligatorio** impone ai dispositivi con supervisione di impostare la data e l'ora automaticamente. Il fuso orario del dispositivo viene aggiornato quando il dispositivo dispone di connessioni alla rete cellulare o Wi-Fi con i servizi di posizione abilitati.
- **Richiedi agli studenti di chiedere l'autorizzazione per lasciare un corso Classroom**: **Rendi obbligatorio** impone agli studenti registrati in un corso non gestito che usa l'app Classroom di richiedere l'autorizzazione al docente per lasciare il corso. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe non imporre agli studenti di richiedere l'autorizzazione.

  Questa funzionalità si applica a:  
  - iOS 11.3 e versioni successive
  - iPadOS 13.0 e versioni successive

- **Consenti a Classroom di bloccare un'app e bloccare il dispositivo senza prompt**: **Abilita** consente al docente di bloccare le app o bloccare il dispositivo usando l'app Classroom senza richiedere conferma allo studente. Con il blocco delle app, il dispositivo può accedere solo alle app specificate dal docente. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe impedire ai docenti di bloccare app o dispositivi usando l'app Classroom senza chiedere conferma allo studente.

  Questa funzionalità si applica a:  
  - iOS 11.0 e versioni successive
  - iPadOS 13.0 e versioni successive

- **Partecipa automaticamente alle lezioni di Classroom senza prompt**: **Abilita** consente automaticamente agli studenti di partecipare a una lezione nell'app Classroom senza chiedere conferma al docente. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe segnalare al docente quando gli studenti vogliono partecipare a una lezione nell'app Classroom.

  Questa funzionalità si applica a:  
  - iOS 11.0 e versioni successive
  - iPadOS 13.0 e versioni successive

- **Blocca la creazione di VPN**: **Blocca** impedisce agli utenti di creare le impostazioni di configurazione VPN. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di creare VPN nel dispositivo.
- **Modifica delle impostazioni di eSIM**: **Blocca** impedisce agli utenti di rimuovere o aggiungere un piano per telefoni cellulari alla eSIM presente nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di modificare queste impostazioni.

  Questa funzionalità si applica a:  
  - iOS 12.1 e versioni successive
  - iPadOS 13.0 e versioni successive

- **Rinvia gli aggiornamenti software**: Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe visualizzare gli aggiornamenti software sul dispositivo quando vengono rilasciati da Apple. Ad esempio, se un aggiornamento iOS/iPadOS viene rilasciato da Apple in una data specifica, questo viene normalmente visualizzato nel dispositivo in prossimità della data di rilascio.

  **Abilita** consente di posticipare la visualizzazione degli aggiornamenti software nei dispositivi, da 0 a 90 giorni. Questa impostazione non controlla quando gli aggiornamenti vengono installati o meno. 

  - **Posticipa la visibilità degli aggiornamenti software**: immettere un valore compreso tra 0 e 90 giorni. Quando l'intervallo di ritardo scade, gli utenti ricevono una notifica per l'aggiornamento alla versione del sistema operativo meno recente disponibile quando è stato attivato il ritardo.

    Ad esempio, se iOS 12.a è disponibile il **1° gennaio** e **Posticipa la visibilità** è impostata su **5 giorni**, iOS 12.a non viene visualizzato come aggiornamento disponibile nei dispositivi degli utenti. Il **sesto giorno** dopo il rilascio, l'aggiornamento diventa disponibile e gli utenti possono installarlo.

    Questa impostazione si applica a:  
    - iOS 11.3 e versioni successive
    - iPadOS 13.0 e versioni successive

## <a name="password"></a>Password

### <a name="settings-apply-to-all-enrollment-types"></a>Le impostazioni si applicano a: Tutti i tipi di registrazione

- **Password**: **Rendi obbligatorio** richiede all'utente finale di immettere una password per accedere al dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di accedere al dispositivo senza immettere una password.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Le impostazioni si applicano a: Registrazione del dispositivo, Registrazione automatica dei dispositivi (con supervisione)

> [!IMPORTANT]
> Nei dispositivi registrati dall'utente, se si configura qualsiasi impostazione della password, le impostazioni **Password semplici** vengono impostate automaticamente su **Blocco** e viene impostato un PIN a 6 cifre.
>
> Si supponga ad esempio di configurare l'impostazione **Scadenza password** e di applicare questo criterio nei dispositivi registrati dall'utente. Nei dispositivi si verificherà quanto segue:
>
> - L'impostazione **Scadenza password** viene ignorata.
> - Le password semplici, ad esempio `1111` o `1234`, non sono consentite.
> - Viene applicato un PIN di 6 cifre.

- **Password semplici**: **Blocca** richiede password più complesse. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire password semplici, come `0000` e `1234`.

- **Tipo di password richiesto**: scegliere il tipo di password richiesto dall'organizzazione. Le opzioni disponibili sono:
  - **Impostazione predefinita dispositivo**
  - **Numerica**
  - **Alfanumerica**
- **Numero di caratteri non alfanumerici nella password**: immettere il numero di simboli, ad esempio `#` o `@`, che è necessario includere nella password.

- **Lunghezza minima password**: immettere la lunghezza minima della password che l'utente deve immettere, da 4 a 14 caratteri. Nei dispositivi registrati dall'utente immettere una lunghezza compresa tra 4 e 6 caratteri.
  
  > [!NOTE]
  > Per i dispositivi registrati dall'utente, gli utenti possono impostare un PIN superiore a 6 cifre. Tuttavia, non vengono applicate più di 6 cifre sul dispositivo. Un amministratore, ad esempio, imposta una lunghezza minima di `8`. Nei dispositivi registrati dall'utente agli utenti viene richiesto di impostare solo un PIN di 6 cifre. Intune non impone un PIN superiore a 6 cifre nei dispositivi registrati dall'utente.

- **Numero di errori di accesso prima della cancellazione dei dati del dispositivo**: immettere il numero di accessi non riusciti consentiti prima della cancellazione del dispositivo (da 4 a 11).
  
  iOS/iPadOS ha una funzionalità di sicurezza incorporata che può influire su questa impostazione. Ad esempio, iOS/iPadOS può ritardare l'attivazione del criterio a seconda del numero di errori di accesso. Immettere ripetutamente lo stesso passcode può essere considerato un solo tentativo. La [Guida di sicurezza iOS/iPadOS](https://www.apple.com/business/site/docs/iOS_Security_Guide.pdf) di Apple è una valida risorsa e offre dettagli più specifici sui passcode (apre il sito Web di Apple).
  
- **Numero massimo di minuti dopo il blocco dello schermo prima che venga richiesta una password**<sup>1</sup>: specificare per quanto tempo il dispositivo rimane inattivo prima che gli utenti debbano immettere di nuovo la password. Se il tempo immesso è più lungo dell'impostazione corrente nel dispositivo, il dispositivo ignora il tempo immesso. Supportato nei dispositivi che eseguono iOS 8.0+ e iPadOS 13.0+.

- **Numero massimo di minuti di inattività fino al blocco dello schermo**<sup>1</sup>: immettere il numero massimo di minuti di inattività consentiti nel dispositivo prima del blocco dello schermo.

  **Opzioni iOS/iPadOS**:  

  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione.
  - **Immediatamente**: lo schermo si blocca dopo 30 secondi di inattività.
  - **1**: lo schermo si blocca dopo 1 minuto di inattività.
  - **2**: lo schermo si blocca dopo 2 minuti di inattività.
  - **3**: lo schermo si blocca dopo 3 minuti di inattività.
  - **4**: lo schermo si blocca dopo 4 minuti di inattività.
  - **5**: lo schermo si blocca dopo 5 minuti di inattività.

  **Opzioni iPadOS**:  

  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione.
  - **Immediatamente**: lo schermo si blocca dopo 2 minuti di inattività.
  - **2**: lo schermo si blocca dopo 2 minuti di inattività.
  - **5**: lo schermo si blocca dopo 5 minuti di inattività.
  - **10**: lo schermo si blocca dopo 10 minuti di inattività.
  - **15**: lo schermo si blocca dopo 15 minuti di inattività.

  Se un valore non è applicabile a iOS e iPadOS, Apple userà il valore *minimo* più prossimo. Se ad esempio si immette `4` minuti, i dispositivi iPadOS useranno il valore `2` minuti. Se si immette `10` minuti, i dispositivi iOS useranno il valore `5` minuti. Questa è una limitazione Apple.
  
  > [!NOTE]
  > L'interfaccia utente di Intune per questa impostazione non separa i valori supportati da iOS e iPadOS. L'interfaccia utente potrebbe essere aggiornata in una delle prossime versioni.

- **Scadenza password (giorni)** : immettere il numero di giorni che devono trascorrere prima che sia necessario cambiare la password del dispositivo.
- **Impedisci riutilizzo delle password precedenti**: immettere il numero di nuove password da usare prima che una password precedente possa essere usata di nuovo.
- **Sblocco di Touch ID e Face ID**: **Blocca** impedisce l'uso di un'impronta digitale o del riconoscimento del volto per sbloccare il dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di sbloccare il dispositivo con questi metodi.

  Il blocco di questa impostazione impedisce anche l'uso dell'autenticazione FaceID per sbloccare il dispositivo.

  Face ID si applica a:  
  - iOS 11.0 e versioni successive
  - iPadOS 13.0 e versioni successive

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Le impostazioni si applicano a: Registrazione automatica dei dispositivi (supervisione)

- **Modifica del passcode**: **Blocca** impedisce la modifica, l'aggiunta o la rimozione del passcode. Le modifiche alle restrizioni del passcode vengono ignorate nei dispositivi con supervisione dopo il blocco di questa funzionalità. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'aggiunta, la modifica o la rimozione dei passcode.

  - **Modifica di Touch ID e Face ID**: **Blocca** impedisce agli utenti di modificare, aggiungere o rimuovere le impronte digitali TouchID e Face ID. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di aggiornare le impronte digitali TouchID e Face ID nel dispositivo.

    Il blocco di questa impostazione impedisce anche agli utenti di modificare, aggiungere o rimuovere l'autenticazione FaceID.

    Face ID si applica a:  
    - iOS 11.0 e versioni successive
    - iPadOS 13.0 e versioni successive

- **Blocca il riempimento automatico delle password**: **Blocca** impedisce l'uso della funzionalità di riempimento automatico delle password in iOS/iPadOS. La scelta di **Blocca** comporta anche le conseguenze seguenti:

  - Agli utenti non viene richiesto di usare una password salvata in Safari o in qualsiasi app.
  - Le password complesse automatiche sono disabilitate e non vengono consigliate password complesse agli utenti.

  Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire queste funzionalità.

- **Blocca le richieste di prossimità password**: scegliere **Blocca** in modo che il dispositivo di un utente non richieda password dai dispositivi nelle vicinanze. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire queste richieste di password.
- **Blocca la condivisione delle password**: **Blocca** impedisce la condivisione delle password tra i dispositivi tramite AirDrop. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire la condivisione di queste password.
- **Richiedi l'autenticazione con Touch ID o Face ID per il riempimento automatico di password o informazioni della carta di credito**: se impostato su **Rendi obbligatorio**, gli utenti devono autenticarsi tramite TouchID o FaceID prima che le password o le informazioni della carta di credito possano essere immesse automaticamente in Safari e altre app. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di controllare questa funzionalità nelle impostazioni del dispositivo.

  Questa funzionalità si applica a:  
  - iOS 11.0 e versioni successive
  - iPadOS 13.0 e versioni successive
  
<sup>1</sup> Quando si configurano le impostazioni **Numero massimo di minuti di inattività fino al blocco dello schermo** e **Numero massimo di minuti dopo il blocco dello schermo prima che venga richiesta una password**, queste vengono applicate in sequenza. Ad esempio, se si imposta il valore di entrambe le impostazioni su **5** minuti, lo schermo si spegne automaticamente dopo cinque minuti e il dispositivo viene bloccato dopo altri cinque minuti. Se tuttavia gli utenti spengono manualmente lo schermo, la seconda impostazione viene applicata immediatamente. Nello stesso esempio il dispositivo viene bloccato cinque minuti dopo che gli utenti spengono lo schermo.

## <a name="locked-screen-experience"></a>Esperienza della schermata di blocco

### <a name="settings-apply-to-all-enrollment-types"></a>Le impostazioni si applicano a: Tutti i tipi di registrazione

- **Accesso al centro di controllo durante il blocco del dispositivo**: **Blocca** impedisce l'accesso all'app Centro di controllo quando il dispositivo è bloccato. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di accedere all'app Centro di controllo quando il dispositivo è bloccato.
- **Notifiche durante il blocco del dispositivo**: **Blocca** impedisce l'accesso alle notifiche quando il dispositivo è bloccato. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di accedere alle notifiche senza sbloccare il dispositivo.
- **Visualizzazione Oggi durante il blocco del dispositivo**: **Blocca** impedisce l'accesso alla visualizzazione Oggi quando il dispositivo è bloccato. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di accedere alla visualizzazione Oggi quando il dispositivo è bloccato.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Le impostazioni si applicano a: Registrazione del dispositivo, Registrazione automatica dei dispositivi (con supervisione)

- **Notifiche di Portafoglio durante il blocco del dispositivo**: **Blocca** impedisce l'accesso all'app Portafoglio quando il dispositivo è bloccato. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di accedere all'app Portafoglio mentre il dispositivo è bloccato.

## <a name="app-store-doc-viewing-gaming"></a>App Store, visualizzazione documenti, giochi

### <a name="settings-apply-to-all-enrollment-types"></a>Le impostazioni si applicano a: Tutti i tipi di registrazione

- **Visualizzazione dei documenti aziendali nelle app non gestite**: **Blocca** impedisce la visualizzazione di documenti aziendali in app non gestite. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di visualizzare documenti aziendali in qualsiasi app. Ad esempio, può essere necessario impedire agli utenti il salvataggio di file dall'app OneDrive a Dropbox. Configurare questa impostazione come **Blocca**. Dopo aver ricevuto i criteri, ad esempio dopo un riavvio, il dispositivo non consente più il salvataggio.


  > [!NOTE]
  > Quando questa impostazione è bloccata, vengono bloccate anche le tastiere di terze parti installate dall'App Store.

  - **Consenti alle app gestite di leggere da contatti in account di contatti non gestiti**: Quando questa opzione è impostata su **Consenti**, le app non gestite, ad esempio l'app Contatti di iOS/iPadOS predefinita, possono leggere e accedere alle informazioni dei contatti dalle app gestite, inclusa l'app per dispositivi mobili Outlook. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe impedire la lettura, inclusa la rimozione di duplicati, dall'app Contatti incorporata nel dispositivo.  
  
    Questa impostazione consente o impedisce la lettura delle informazioni dei contatti. Non controlla la sincronizzazione dei contatti tra le app.
  
    Per usare questa impostazione, impostare **Visualizzazione dei documenti aziendali nelle app non gestite** su **Blocca**.

  Per altre informazioni su queste due impostazioni e sull'effetto che producono sulla sincronizzazione per l'esportazione dei contatti di Outlook per iOS/iPadOS, vedere [Suggerimento per il supporto: Usare le impostazioni del profilo personalizzato di Intune con l'app Contatti nativa di iOS/iPadOS](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Use-Intune-custom-profile-settings-with-the-iOS/ba-p/298453).

- **Considera AirDrop come destinazione non gestita**: **Rendi obbligatorio** forza la considerazione di AirDrop come obiettivo di rilascio non gestito. Impedisce alle app gestite di inviare dati tramite Airdrop. 
- **Visualizzazione di documenti non aziendali nelle app aziendali**: **Blocca** impedisce la visualizzazione di documenti non aziendali in app aziendali. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di visualizzare qualsiasi documento nelle app aziendali gestite.

  **Blocca** impedisce anche la sincronizzazione per l'esportazione dei contatti in Outlook per iOS/iPadOS. Per altre informazioni, vedere [Suggerimento per il supporto: Abilitazione della sincronizzazione dei contatti di Outlook per iOS/iPadOS con i controlli MDM di iOS12](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Enabling-Outlook-iOS-Contact-Sync-with-iOS12-MDM/ba-p/298453).

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Le impostazioni si applicano a: Registrazione del dispositivo, Registrazione automatica dei dispositivi (con supervisione)

- **Richiedi la password di iTunes Store per tutti gli acquisti**: se si seleziona **Rendi obbligatorio**, gli utenti dovranno immettere la password dell'ID Apple per ogni acquisto in-app o su iTunes. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire gli acquisti senza richiedere ogni volta una password.
- **Acquisti in-app**: **Blocca** impedisce gli acquisti in-app dallo Store. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire gli acquisti dallo Store dall'interno di un'app in esecuzione.
- **Scarica da iBook Store i contenuti contrassegnati come 'Erotici'** : **Blocca** impedisce agli utenti di scaricare da iBook Store contenuti multimediali contrassegnati come erotici. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di scaricare libri della categoria "Erotici".
- **Consenti alle app gestite di scrivere contatti in account di contatti non gestiti**: Quando questa opzione è impostata su **Consenti**, le app gestite, ad esempio l'app per dispositivi mobili Outlook, possono salvare o sincronizzare le informazioni dei contatti, inclusi i contatti commerciali e aziendali, con l'app Contatti di iOS/iPadOS predefinita. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe impedire alle app gestite di salvare o sincronizzare le informazioni dei contatti con l'app Contatti di iOS/iPadOS predefinita nel dispositivo.
  
  Per usare questa impostazione, impostare **Visualizzazione dei documenti aziendali nelle app non gestite** su **Blocca**.

- **Area classificazioni**: scegliere l'area di classificazioni da usare per i download consentiti. Scegliere quindi le classificazioni consentite per **Film**, **Programmi TV** e **App**.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Le impostazioni si applicano a: Registrazione automatica dei dispositivi (supervisione)

- **App Store**: **Blocca** impedisce l'accesso all'App Store nei dispositivi con supervisione. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'accesso.

  A partire da iOS/iPadOS 13.0, questa impostazione richiede dispositivi con supervisione.

  - **Installazione di app dall'App Store**: scegliere **Blocca** per bloccare l'App Store nella schermata iniziale del dispositivo. Gli utenti possono continuare a usare iTunes o Apple Configurator per installare le app. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire App Store nella schermata iniziale.
  - **Download automatici delle app**: **Blocca** impedisce il download automatico delle app acquistate in altri dispositivi. Non influisce sugli aggiornamenti delle app esistenti. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire il download nel dispositivo di app acquistate in altri dispositivi iOS/iPadOS.

- **Musica di iTunes, podcast o notizie con contenuti espliciti**: **Blocca** impedisce la riproduzione di musica di iTunes, podcast o notizie con contenuti espliciti. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire al dispositivo di accedere ai contenuti classificati come per adulti dallo Store.

  A partire da iOS/iPadOS 13.0, questa impostazione richiede dispositivi con supervisione.

- **Aggiunta di amici al Game Center**: **Blocca** impedisce agli utenti di aggiungere amici al Game Center. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di aggiungere amici al Game Center.

  A partire da iOS/iPadOS 13.0, questa impostazione richiede dispositivi con supervisione.

- **Game Center**: **Blocca** impedisce l'uso dell'app Game Center. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'uso dell'app Game Center nel dispositivo.
- **Gioco multiplayer**: **Blocca** impedisce il gioco in modalità multiplayer. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di giocare in modalità multiplayer nel dispositivo.

  A partire da iOS/iPadOS 13.0, questa impostazione richiede dispositivi con supervisione.

- **Accesso all'unità di rete nell'app File**: usando il protocollo SMB (Server Message Block), i dispositivi possono accedere a file o ad altre risorse in un server di rete. **Disabilita** impedisce l'accesso ai file in un'unità SMB di rete. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'accesso.

  Questa funzionalità si applica a:  
  - iOS 13.0 e versioni successive
  - iPadOS 13.0 e versioni successive

## <a name="built-in-apps"></a>App predefinite

### <a name="settings-apply-to-all-enrollment-types"></a>Le impostazioni si applicano a: Tutti i tipi di registrazione

- **Siri**: **Blocca** impedisce l'accesso a Siri. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'uso dell'assistente vocale Siri nel dispositivo.
  - **Siri durante il blocco del dispositivo**: **Blocca** impedisce l'accesso a Siri quando il dispositivo è bloccato. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'uso dell'assistente vocale Siri quando il dispositivo è bloccato.

- **Avvisi in caso di illeciti di Safari**: **Rendi obbligatorio** abilita la visualizzazione degli avvisi di illeciti nel Web browser del dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe disabilitare questa funzionalità.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Le impostazioni si applicano a: Registrazione del dispositivo, Registrazione automatica dei dispositivi (con supervisione)

- **Ricerca Spotlight per la restituzione di risultati da Internet**: **Blocca** impedisce a Spotlight di restituire risultati da una ricerca su Internet. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire alla ricerca Spotlight di connettersi a Internet per restituire i risultati della ricerca.

- **Cookie di Safari**: scegliere la modalità di gestione dei cookie nel dispositivo. Le opzioni disponibili sono:
  - Consenti
  - Blocca tutti i cookie
  - Consenti i cookie dai siti Web visitati
  - Consenti i cookie dal sito Web corrente

- **JavaScript in Safari**: **Blocca** impedisce l'esecuzione degli script Java del browser nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'esecuzione degli script Java.

- **Popup di Safari**: **Blocca** disabilita il blocco popup nel Web browser. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire il blocco popup.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Le impostazioni si applicano a: Registrazione automatica dei dispositivi (supervisione)

- **Fotocamera**: **Blocca** impedisce l'accesso alla fotocamera nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'accesso alla fotocamera del dispositivo.

  A partire da iOS/iPadOS 13.0, questa impostazione richiede dispositivi con supervisione.

  - **FaceTime**: **Blocca** impedisce l'accesso all'app FaceTime. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'accesso all'app FaceTime nel dispositivo.

    A partire da iOS/iPadOS 13.0, questa impostazione richiede dispositivi con supervisione.

- **Filtro di Siri per le espressioni volgari**: **Rendi obbligatorio** impedisce a Siri di usare espressioni volgari.

  Per usare questa impostazione, impostare l'opzione **Siri** su **Blocca**.

- **Consenti a Siri di eseguire query sul contenuto generato dall'utente da Internet**: **Blocca** impedisce a Siri di accedere a siti Web per rispondere a domande. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire a Siri di accedere al contenuto generato dall'utente da Internet.

  Per usare questa impostazione, impostare l'opzione **Siri** su **Blocca**.

- **Apple News**: **Blocca** impedisce l'accesso all'app Apple News nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'uso dell'app Apple News.
- **iBooks Store**: **Blocca** impedisce l'accesso all'iBooks Store. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di cercare e acquistare libri da iBooks Store.
- **App Messages sul dispositivo**: **Blocca** impedisce agli utenti di usare l'app Messages per iMessage. Se il dispositivo supporta i messaggi di testo, gli utenti possono comunque inviare e ricevere messaggi di testo tramite SMS. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'uso dell'app Messages per inviare e leggere messaggi tramite Internet.
- **Podcast**: **Blocca** impedisce agli utenti di usare l'app Podcasts. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'uso dell'app Podcasts.
- **Servizio Music**: **Blocca** ripristina la modalità classica per l'app Music e disabilita il servizio Music. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'uso dell'app Apple Music.
- **Servizio iTunes Radio**: **Blocca** impedisce agli utenti di usare l'app iTunes Radio. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'uso dell'app iTunes Radio.
- **iTunes Store**: Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'uso di iTunes nei dispositivi. **Blocca** impedisce agli utenti di usare iTunes nel dispositivo.

  Questa funzionalità si applica a:  
  - iOS 4.0 e versioni successive
  - iPadOS 13.0 e versioni successive

- **Trova il mio iPhone**: Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire di usare la funzionalità dell'app Trova il mio per ottenere la posizione approssimativa del dispositivo. **Blocca** impedisce questa funzionalità nell'app Trova il mio. 

  Questa funzionalità si applica a:  
  - iOS 13.0 e versioni successive
  - iPadOS 13.0 e versioni successive

- **Trova i miei amici**: Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire di usare la funzionalità dell'app Trova il mio per trovare familiari e amici da un dispositivo Apple o da iCloud.com. **Blocca** impedisce questa funzionalità nell'app Trova il mio.

  Questa funzionalità si applica a:  
  - iOS 13.0 e versioni successive
  - iPadOS 13.0 e versioni successive

- **Modifiche alle impostazioni dell'app Trova i miei amici**: **Blocca** impedisce di apportare modifiche alle impostazioni dell'app Find My Friends. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di modificare le impostazioni per l'app Trova i miei amici.

- **Ricerca Spotlight per la restituzione di risultati da Internet**: **Blocca** impedisce a Spotlight di restituire risultati da una ricerca su Internet. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire alla ricerca Spotlight di connettersi a Internet per restituire i risultati della ricerca.

- **Impedisci la rimozione di app di sistema dal dispositivo**: **Blocca** impedisce la rimozione di app di sistema dal dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di rimuovere app di sistema dal dispositivo.

- **Safari**: **Blocca** impedisce l'uso del browser Safari nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di usare il browser Safari.

  A partire da iOS/iPadOS 13.0, questa impostazione richiede dispositivi con supervisione.

- **Riempimento automatico di Safari**: **Blocca** disabilita la funzionalità di riempimento automatico in Safari nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di modificare le impostazioni di completamento automatico nel Web browser.

  A partire da iOS/iPadOS 13.0, questa impostazione richiede dispositivi con supervisione.

## <a name="restricted-apps"></a>App con restrizioni

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Le impostazioni si applicano a: Registrazione del dispositivo, Registrazione automatica dei dispositivi (con supervisione)

- **Elenco di tipi di app con restrizioni**: consente di creare un elenco di app che gli utenti non sono autorizzati a installare o usare. Le opzioni disponibili sono:

  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione. Gli utenti hanno accesso alle app assegnate e alle app predefinite.
  - **App non consentite**: elenco di app non gestite da Intune di cui si vuole evitare l'installazione nel dispositivo. Agli utenti non viene impedito di installare un'app vietata. Tuttavia, se un utente installa un'app da questo elenco, verrà segnalato in Intune.
  - **App approvate**: app che gli utenti sono autorizzati a installare. Gli utenti non devono installare app che non sono elencate. Le app gestite da Intune sono automaticamente consentite. Agli utenti non viene impedito di installare un'app non inclusa nell'elenco approvato. Tuttavia, se lo fanno, verrà segnalato in Intune.

Per aggiungere app a questi elenchi, è possibile:

- Scegliere **Aggiungi** per aggiungere l'URL dell'App Store iTunes dell'app desiderata. Ad esempio, per aggiungere l'app Cartelle di lavoro Microsoft, immettere `https://itunes.apple.com/us/app/work-folders/id950878067?mt=8` o `https://apps.apple.com/us/app/work-folders/id950878067?mt=8`.

  Per trovare l'URL di un'app, aprire iTunes App Store e cercare l'app. Ad esempio, cercare `Microsoft Remote Desktop` o `Microsoft Word`. Selezionare l'app e copiare l'URL.

  È anche possibile usare iTunes per trovare l'app e quindi usare l'attività **Copia collegamento** per ottenere l'URL dell'app.

- Scegliere **Importa** per importare un file CSV con i dettagli sull'app, incluso l'URL. Usare il formato `<app url>, <app name>, <app publisher>`. In alternativa, **esportare** un elenco esistente che include l'elenco delle app con restrizioni nello stesso formato.

> [!IMPORTANT]
> I profili dispositivo che usano le impostazioni per app con restrizioni devono essere assegnati ai gruppi di utenti.

## <a name="show-or-hide-apps"></a>Mostrare o nascondere app

Si applica ai dispositivi che eseguono iOS 9.3+ e iPadOS 13.0+.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Le impostazioni si applicano a: Registrazione automatica dei dispositivi (supervisione)

- **Tipo di elenco di app**: consente di creare un elenco di app da mostrare o nascondere. È possibile mostrare o nascondere le app predefinite e le app line-of-business. Il sito Web di Apple include un elenco di [app Apple predefinite](https://support.apple.com/HT208094). Le opzioni disponibili sono:

  - **App nascoste**: immettere un elenco di app nascoste agli utenti. Gli utenti non possono visualizzare o aprire queste app.
  
    Apple impedisce di nascondere alcune app native. Ad esempio, non è possibile nascondere l'app **Impostazioni** nel dispositivo. In [Come eliminare le app Apple integrate](https://support.apple.com/HT208094) sono elencate le app che possono essere nascoste.
  
  - **App visibili**: immettere un elenco di app che gli utenti possono visualizzare e avviare. Non è possibile visualizzare o avviare altre app.

- **URL app**: immettere l'URL dell'App Store per l'app che si vuole mostrare o nascondere. Ad esempio:

  - Per aggiungere l'app Cartelle di lavoro Microsoft, immettere `https://itunes.apple.com/us/app/work-folders/id950878067?mt=8` o `https://apps.apple.com/us/app/work-folders/id950878067?mt=8`. 

  - Per aggiungere l'app Microsoft Word, immettere `https://itunes.apple.com/de/app/microsoft-word/id586447913` o `https://apps.apple.com/de/app/microsoft-word/id586447913`.

  Per trovare l'URL di un'app, aprire iTunes App Store e cercare l'app. Ad esempio, cercare `Microsoft Remote Desktop` o `Microsoft Word`. Selezionare l'app e copiare l'URL.

  È anche possibile usare iTunes per trovare l'app e quindi usare l'attività **Copia collegamento** per ottenere l'URL dell'app.

- **ID bundle dell'app**: immettere l'[ID bundle](bundle-ids-built-in-ios-apps.md) dell'app desiderata. È possibile mostrare o nascondere le app predefinite e le app line-of-business. Il sito Web di Apple include un elenco di [app Apple predefinite](https://support.apple.com/HT208094).
- **Nome app**: immettere il nome dell'app desiderata. È possibile mostrare o nascondere le app predefinite e le app line-of-business. Il sito Web di Apple include un elenco di [app Apple predefinite](https://support.apple.com/HT208094).
- **Autore**: immettere l'autore dell'app desiderata.

Per aggiungere le app, è possibile:

- **Aggiungi**: selezionare questa opzione per creare un elenco di app.
- Scegliere **Importa** per importare un file CSV con i dettagli sull'app, incluso l'URL. Usare il formato `<app url>, <app name>, <app publisher>`. In alternativa, scegliere **Esporta** per creare un elenco delle app con restrizioni aggiunte, nello stesso formato.

## <a name="wireless"></a>Wireless

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Le impostazioni si applicano a: Registrazione del dispositivo, Registrazione automatica dei dispositivi (con supervisione)

Nota necessaria per il roaming dei dati (suggerimento o nota importante per non creare confusione tra i clienti): questa impostazione non verrà visualizzata nel profilo di gestione del dispositivo di destinazione. Ciò è dovuto al fatto che questa impostazione viene considerata un'azione remota del dispositivo e ogni volta che lo stato del roaming dei dati cambia nel dispositivo, il servizio Intune la bloccherà nuovamente. Anche se questa impostazione non è presente nel profilo di gestione, funziona se nella console di amministrazione i report indicano un esito positivo. 
- **Dati in roaming**: **Blocca** impedisce il roaming dei dati nella rete cellulare. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire il roaming dei dati quando il dispositivo si trova in una rete cellulare.

  > [!IMPORTANT]
  > Questa impostazione viene considerata un'azione remota del dispositivo, pertanto non viene visualizzata nel profilo di gestione del dispositivo. Ogni volta che lo stato del roaming dei dati cambia nel dispositivo, l'opzione **Dati in roaming** viene bloccata dal servizio Intune. In Intune, se lo stato del report indica un esito positivo, l'impostazione funziona anche se non viene visualizzata nel profilo di gestione del dispositivo.

- **Recupero in background globale durante il roaming**: **Blocca** impedisce l'uso della funzionalità di recupero in background globale durante il roaming nella rete cellulare. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire al dispositivo di recuperare dati, ad esempio messaggi di posta elettronica, durante il roaming in una rete cellulare.
- **Composizione vocale**: **Blocca** impedisce agli utenti di usare la funzionalità di composizione vocale nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire la composizione vocale nel dispositivo.
- **Chiamate in roaming**: **Blocca** impedisce le chiamate in roaming nella rete cellulare. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire le chiamate in roaming quando il dispositivo è su una rete cellulare.
- **Hotspot personale**: **Blocca** disattiva l'hotspot personale nei dispositivi a ogni sincronizzazione del dispositivo. Questa impostazione potrebbe non essere compatibile con alcuni gestori. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe mantenere la configurazione dell'hotspot personale come configurazione predefinita impostata dall'utente.

  > [!IMPORTANT]
  > Questa impostazione viene considerata un'azione remota del dispositivo, pertanto non viene visualizzata nel profilo di gestione del dispositivo. Ogni volta che lo stato dell'hotspot personale cambia nel dispositivo, l'opzione **Hotspot personale** viene bloccata dal servizio Intune. In Intune, se lo stato del report indica un esito positivo, l'impostazione funziona anche se non viene visualizzata nel profilo di gestione del dispositivo.

- **Regole di utilizzo della rete cellulare (solo app gestite)** : consente di definire i tipi di dati che possono essere usati dalle app gestite nelle reti cellulari. Le opzioni disponibili sono:
  - **Blocca l'uso della rete dati**: consente di bloccare l'uso della rete dati selezionando **Tutte le app gestite** oppure **Scegliere app specifiche**.
  - **Blocca l'uso della rete dati durante il roaming**: consente di bloccare l'uso della rete dati durante il roaming selezionando **Tutte le app gestite** oppure **Scegliere app specifiche**.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Le impostazioni si applicano a: Registrazione automatica dei dispositivi (supervisione)

- **Modifiche alle impostazioni dell'utilizzo della rete dati dell'app**: **Blocca** impedisce di apportare modifiche alle impostazioni di utilizzo della rete dati dell'app. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire all'utente di controllare le app che possono usare la rete dati.
- **Modifiche alle impostazioni del piano per telefoni cellulari**: **Blocca** impedisce agli utenti di modificare le impostazioni nel piano cellulare. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di apportare modifiche.

  Questa funzionalità si applica a:  
  - iOS 11.0 e versioni successive
  - iPadOS 13.0 e versioni successive

- **Modifica utente dell'hotspot personale**: quando questa opzione è impostata su **Blocca**, gli utenti non possono modificare l'impostazione dell'hotspot personale. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti finali di abilitare o disabilitare l'hotspot personale.

  Se si blocca questa impostazione e si blocca l'opzione **Hotspot personale**, l'hotspot personale viene disattivato.

  Questa funzionalità si applica a:  
  - iOS 12.2 e versioni successive
  - iPadOS 13.0 e versioni successive

- **Aggiungi reti Wi-Fi solo tramite profili di configurazione**: **Rendi obbligatorio** forza il dispositivo a usare solo reti Wi-Fi configurate tramite profili di configurazione di Intune. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire al dispositivo di usare altre reti Wi-Fi.

  Quando questa opzione è impostata su **Rendi obbligatorio**, verificare che il dispositivo disponga di un profilo Wi-Fi. Se non si assegna un profilo Wi-Fi, questa impostazione potrebbe impedire la connessione del dispositivo a Internet. In altre parole, se il profilo di limitazioni del dispositivo viene assegnato prima di un profilo Wi-Fi, la connessione del dispositivo a Internet potrebbe essere bloccata.
  
  Se non è possibile connettersi, annullare la registrazione del dispositivo ed eseguirla nuovamente con un profilo Wi-Fi. Impostare quindi questa opzione su **Rendi obbligatorio** in un profilo di limitazioni del dispositivo e assegnare il profilo al dispositivo.

- **Wi-Fi sempre attivato**: quando questa opzione è impostata su **Rendi obbligatorio**, il Wi-Fi rimane attivo nell'app Impostazioni. Non può essere disattivato in Impostazioni o nel centro di controllo, anche quando il dispositivo è in modalità aereo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di controllare l'attivazione o la disattivazione del Wi-Fi.

  La configurazione di questa impostazione non impedisce agli utenti di selezionare una rete Wi-Fi.

  Questa funzionalità si applica a:  
  - iOS 13.0 e versioni successive
  - iPadOS 13.0 e versioni successive

## <a name="connected-devices"></a>Dispositivi connessi

### <a name="settings-apply-to-all-enrollment-types"></a>Le impostazioni si applicano a: Tutti i tipi di registrazione

- **Rilevamento del polso per l'Apple Watch associato**: **Rendi obbligatorio** forza l'uso del rilevamento del polso in un Apple Watch associato. Se richiesto, l'Apple Watch non visualizza notifiche se non è indossato. 

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Le impostazioni si applicano a: Registrazione del dispositivo, Registrazione automatica dei dispositivi (con supervisione)

- **Richiedi la password associata alle richieste AirPlay in uscita**: **Rendi obbligatorio** richiede una password di associazione quando gli utenti usano AirPlay per trasmettere contenuti ad altri dispositivi di Apple. **Non configurato** (impostazione predefinita) consente agli utenti di trasmettere contenuti con AirPlay senza immettere una password.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Le impostazioni si applicano a: Registrazione automatica dei dispositivi (supervisione)

- **AirDrop**: **Blocca** impedisce l'uso di AirDrop nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'uso della funzionalità AirDrop per scambiare contenuti con dispositivi vicini.
- **Associazione di Apple Watch**: **Blocca** impedisce l'associazione con un Apple Watch. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire al dispositivo l'associazione con un Apple Watch.
- **Modifica Bluetooth**: **Blocca** impedisce agli utenti finali di modificare le impostazioni Bluetooth nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di modificare queste impostazioni.
- **Associazione di host per controllare i dispositivi a cui può essere associato un dispositivo iOS/iPadOS**: Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'impostazione dell'associazione di host in modo che l'amministratore possa stabilire a quali dispositivi può essere associato un dispositivo iOS/iPadOS. **Blocca** impedisce l'associazione di host.
- **Blocca AirPrint**: **Blocca** impedisce l'uso della funzionalità AirPrint nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di usare AirPrint.
  - **Impedisci l'archiviazione di credenziali AirPrint in Keychain**: **Blocca** impedisce l'archiviazione Keychain di nome utente e password nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'archiviazione di nome utente e password per AirPrint nell'app Keychain.
  - **Richiedi un certificato TLS attendibile per AirPrint**: **Rendi obbligatorio** forza il dispositivo a usare certificati attendibili per le comunicazioni di stampa TLS.
  - **Impedisci l'individuazione iBeacon delle stampanti AirPrint**: **Blocca** impedisce ai beacon Bluetooth AirPrint dannosi di eseguire il phishing del traffico di rete. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'annuncio delle stampanti AirPrint nel dispositivo.
- **Blocca la configurazione di nuovi dispositivi vicini**: **Blocca** disabilita la richiesta per la configurazione di nuovi dispositivi che si trovano nelle vicinanze. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire le richieste che gli utenti possono usare per connettersi ad altri dispositivi Apple nelle vicinanze.

  Questa funzionalità si applica a:  
  - iOS 11.0 e versioni successive
  - iPadOS 13.0 e versioni successive

- **Accesso ai file in un'unità USB**: i dispositivi possono connettersi e aprire i file in un'unità USB. **Disabilita** impedisce l'accesso del dispositivo all'unità USB nell'app File quando un'unità USB è connessa al dispositivo. La disabilitazione di questa funzionalità impedisce anche agli utenti di trasferire file in un'unità USB connessa a un iPad. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'accesso a un'unità USB nell'app File.

  Questa funzionalità si applica a:  
  - iOS 13.0 e versioni successive
  - iPadOS 13.0 e versioni successive

## <a name="keyboard-and-dictionary"></a>Tastiera e dizionario

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Le impostazioni si applicano a: Registrazione automatica dei dispositivi (supervisione)

- **Ricerca della definizione della parola**: **Blocca** impedisce all'utente di evidenziare una parola e quindi di cercarne la definizione nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'accesso alla funzionalità di ricerca della definizione.
- **Tastiere predittive**: Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'uso di tastiere predittive per suggerire le parole desiderate dagli utenti. **Blocca** impedisce questa funzionalità.
- **Correzione automatica**: Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire al dispositivo di correggere automaticamente le parole errate. **Blocca** impedisce l'uso della correzione automatica.
- **Controllo ortografico tastiera**: Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'uso del controllo ortografico nel dispositivo. **Blocca** non consente il correttore ortografico.
- **Tasti di scelta rapida**: Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'uso di tasti di scelta rapida nel dispositivo. **Blocca** impedisce agli utenti di usare tasti di scelta rapida.
- **Dettatura**: **Blocca** impedisce agli utenti di immettere testo con l'input vocale. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di usare l'input tramite dettatura.
- **QuickPath**: Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di usare QuickPath, che permette un input continuo sulla tastiera del dispositivo. Gli utenti possono digitare scorrendo il dito sui tasti per creare le parole. **Blocca** impedisce agli utenti di usare QuickPath. 

  Questa funzionalità si applica a:  
  - iOS 13.0 e versioni successive
  - iPadOS 13.0 e versioni successive

## <a name="cloud-and-storage"></a>Cloud e risorse di archiviazione

### <a name="settings-apply-to-all-enrollment-types"></a>Le impostazioni si applicano a: Tutti i tipi di registrazione

- **Backup crittografato**: selezionare **Rendi obbligatorio** in modo che i backup del dispositivo debbano essere crittografati.
- **Sincronizzazione delle app gestite nel cloud**: Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire alle app gestite di Intune di sincronizzare i dati con l'account iCloud dell'utente. **Blocca** impedisce la sincronizzazione dei dati in iCloud.
- **Blocca il backup di libri aziendali**: **Blocca** impedisce agli utenti di eseguire il backup di libri aziendali. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire il backup di questi libri.
- **Blocca la sincronizzazione di metadati di libri aziendali (note e informazioni di rilievo)** : **Blocca** impedisce la sincronizzazione di note e informazioni di rilievo nei libri aziendali. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire la sincronizzazione.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Le impostazioni si applicano a: Registrazione del dispositivo, Registrazione automatica dei dispositivi (con supervisione)

- **Sincronizzazione dello streaming foto in iCloud**: Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di abilitare nel dispositivo la funzionalità **Il mio streaming foto**, per sincronizzare le foto in iCloud e renderle disponibili in tutti i dispositivi degli utenti. **Blocca** impedisce la sincronizzazione dello streaming foto in iCloud. Il blocco di questa funzionalità può causare la perdita di dati. 
- **Libreria foto di iCloud**: **Blocca** disattiva l'uso della libreria foto di iCloud per archiviare foto e video nel cloud. Eventuali foto non scaricate completamente dalla Libreria foto di iCloud nel dispositivo vengono rimosse dal dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'uso della libreria foto di iCloud.
- **Flusso di foto condivise**: **Blocca** disattiva **Condivisione foto iCloud** sul dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire il flusso di foto condivise.
- **Handoff**: Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di avviare il lavoro in un dispositivo iOS/iPadOS e quindi di continuare il lavoro avviato in un altro dispositivo iOS/iPadOS o macOS. **Blocca** impedisce l'handoff.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Le impostazioni si applicano a: Registrazione automatica dei dispositivi (supervisione)

- **Backup in iCloud**: Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di eseguire il backup del dispositivo iCloud. **Blocca** impedisce agli utenti di eseguire il backup del dispositivo in iCloud.

  A partire da iOS/iPadOS 13.0, questa impostazione richiede dispositivi con supervisione.

- **Blocca la sincronizzazione dei documenti di iCloud**: Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire la sincronizzazione di documenti e coppie chiave-valore nello spazio di archiviazione iCloud. **Blocca** impedisce a iCloud di sincronizzare documenti e dati.

  A partire da iOS/iPadOS 13.0, questa impostazione richiede dispositivi con supervisione.

- **Blocca la sincronizzazione Keychain con iCloud**: **Blocca** disattiva la sincronizzazione delle credenziali archiviate in Keychain con iCloud. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di sincronizzare queste credenziali.

  A partire da iOS/iPadOS 13.0, questa impostazione richiede dispositivi con supervisione.

## <a name="autonomous-single-app-mode"></a>Modalità applicazione singola autonoma

Usare queste impostazioni per configurare i dispositivi iOS/iPadOS in modo che eseguano specifiche app in modalità app singola autonoma. Quando questa modalità è configurata e gli utenti avviano una delle app configurate, il dispositivo viene bloccato per tale app. Il cambio di app/attività è disabilitato fino a quando gli utenti non escono dall'app autorizzata.

Ad esempio, in un ambiente scolastico o universitario, aggiungere un'app che consenta agli utenti di eseguire un test nel dispositivo. In alternativa, bloccare il dispositivo nell'app Portale aziendale fino all'autenticazione dell'utente. Quando gli utenti completano le azioni dell'app o si rimuovono questi criteri, il dispositivo torna allo stato normale.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Le impostazioni si applicano a: Registrazione automatica dei dispositivi (supervisione)

- **Nome app**: immettere il nome dell'app desiderata.
- **ID bundle dell'app**: immettere l'[ID bundle](bundle-ids-built-in-ios-apps.md) dell'app desiderata.
- **Aggiungi**: selezionare questa opzione per creare un elenco di app.

È anche possibile scegliere **Importa** per importare un file CSV con l'elenco dei nomi di app e i relativi ID bundle. Oppure **esportare** un elenco esistente che include le app.

## <a name="kiosk"></a>Modalità tutto schermo

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Le impostazioni si applicano a: Registrazione automatica dei dispositivi (supervisione)

- **App da eseguire in modalità tutto schermo**: scegliere il tipo di app da eseguire in modalità tutto schermo. Le opzioni disponibili sono:
  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe non applicare le impostazioni della modalità tutto schermo. Il dispositivo non viene eseguito in modalità tutto schermo.
  - **App dello Store**: immettere l'URL di un'app in iTunes App Store.
  - **App gestite**: scegliere un'app aggiunta a Intune.
  - **App predefinita**: immettere l'[ID bundle](bundle-ids-built-in-ios-apps.md) dell'app predefinita.

- **Tocco per l'accesso facilitato**: **Rendi obbligatorio** richiede la presenza dell'impostazione di accessibilità Tocco per l'accesso facilitato nel dispositivo. Questa funzionalità offre supporto agli utenti per i movimenti sullo schermo che potrebbero risultare difficili. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe non eseguire o abilitare questa funzionalità in modalità tutto schermo.
- **Inverti colori**: **Rendi obbligatorio** rende disponibile l'impostazione di accessibilità Inverti colori in modo che gli utenti con problemi visivi possano regolare la visualizzazione sullo schermo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe non eseguire o abilitare questa funzionalità in modalità tutto schermo.
- **Audio mono**: **Rendi obbligatorio** consente di rendere disponibile l'impostazione di accessibilità Audio mono nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe non eseguire o abilitare questa funzionalità in modalità tutto schermo.
- **Controllo vocale**: **Rendi obbligatorio** abilita il controllo vocale nel dispositivo e consente agli utenti di controllare completamente il sistema operativo usando i comandi di Siri. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe disabilitare il controllo vocale nel dispositivo.

  Questa impostazione si applica a:  
  - iOS 13.0 e versioni successive
  - iPadOS 13.0 e versioni successive
  
  > [!TIP]
  > Se sono disponibili app line-of-business per l'organizzazione e non sono abilitate per il **controllo vocale** il giorno 0 quando viene rilasciata la versione iOS 13.0, è consigliabile lasciare questa opzione impostata su **Non configurato**.

- **VoiceOver**: **Rendi obbligatorio** consente di rendere disponibile l'impostazione di accessibilità VoiceOver nel dispositivo per leggere a voce alta il testo sullo schermo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe non eseguire o abilitare questa funzionalità in modalità tutto schermo.
- **Zoom**: **Rendi obbligatorio** rende disponibile l'impostazione Zoom nel dispositivo per consentire agli utenti di usare il tocco per ingrandire la schermata. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe non eseguire o abilitare questa funzionalità in modalità tutto schermo.
- **Blocco automatico**: **Blocca** impedisce il blocco automatico del dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire questa funzionalità.
- **Commutatore suoneria**: **Blocca** disabilita il commutatore della suoneria nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire questa funzionalità.
- **Rotazione schermo**: **Blocca** impedisce la modifica dell'orientamento dello schermo quando gli utenti ruotano il dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire questa funzionalità.
- **Pulsante Sospensione schermo**: **Blocca** disabilita il pulsante di riattivazione dalla sospensione dello schermo del dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire questa funzionalità.
- **Tocco**: **Blocca** disabilita il touchscreen nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di usare il touchscreen.
- **Pulsanti volume**: **Blocca** impedisce l'uso dei pulsanti del volume nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'uso dei pulsanti del volume.
- **Controllo del tocco per l'accesso facilitato**: **Consenti** permette agli utenti di usare la funzione di tocco per l'accesso facilitato. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe disabilitare questa funzionalità.
- **Controllo dell'inversione colori**: **Consenti** abilita la regolazione dell'inversione colori per permettere agli utenti di modificare la funzione di inversione colori. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe disabilitare questa funzionalità.
- **Pronuncia per il testo selezionato**: **Consenti** rende disponibile le impostazioni di accessibilità Selezione comandi vocali nel dispositivo. Questa funzionalità legge ad alta voce il testo selezionato dagli utenti. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe disabilitare questa funzionalità.
- **Modifica del controllo vocale**: **Consenti** permette agli utenti di modificare lo stato del controllo vocale nei dispositivi in uso. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe impedire agli utenti di modificare lo stato del controllo vocale nei dispositivi.

  Questa impostazione si applica a:  
  - iOS 13.0 e versioni successive
  - iPadOS 13.0 e versioni successive

- **Controllo VoiceOver**: **Consenti** abilita le modifiche del VoiceOver in modo che gli utenti possano aggiornare la funzione VoiceOver, ad esempio la velocità con cui viene letto il testo sullo schermo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe impedire le modifiche alla funzione VoiceOver.
- **Controllo dello zoom**: **Consenti** permette agli utenti di modificare lo zoom. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe impedire le modifiche allo zoom.

> [!NOTE]
> Prima di poter configurare un dispositivo iOS/iPadOS per la modalità tutto schermo, è necessario usare lo strumento Apple Configurator o il programma di registrazione del dispositivo di Apple per attivare la modalità con supervisore del dispositivo. Vedere la Guida di Apple sull'uso dello strumento Apple Configurator.
> Se l'app per iOS/iPadOS specificata viene installata dopo aver assegnato il profilo, il dispositivo attiva la modalità tutto schermo solo dopo il riavvio.

## <a name="domains"></a>Domains

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Le impostazioni si applicano a: Registrazione del dispositivo, Registrazione automatica dei dispositivi (con supervisione)

- **Domini di posta elettronica non contrassegnati** > **URL del dominio di posta elettronica**: Aggiungere uno o più URL all'elenco. Quando gli utenti ricevono un messaggio di posta elettronica da un dominio diverso da quelli immessi, il messaggio di posta elettronica viene contrassegnato come non attendibile nell'app di posta in iOS/iPadOS.

- **Domini Web gestiti** > **URL del dominio Web**: aggiungere uno o più URL all'elenco. Quando i documenti vengono scaricati dai domini immessi, sono considerati come gestiti. Questa impostazione si applica solo ai documenti scaricati tramite Safari.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Le impostazioni si applicano a: Registrazione automatica dei dispositivi (supervisione)

- **Domini con compilazione automatica della password di Safari** > **URL del dominio**: Aggiungere uno o più URL all'elenco. Gli utenti possono salvare solo le password Web dagli URL in questo elenco. Questa impostazione si applica solo al browser Safari e ai dispositivi in modalità con supervisione. Se non si specificano URL, è possibile salvare le password da tutti i siti Web.

  Questa impostazione si applica a:  
  - iOS 9.3 e versioni successive
  - iPadOS 13.0 e versioni successive

## <a name="settings-that-require-supervised-mode"></a>Impostazioni che richiedono la modalità di supervisione

La modalità con supervisione iOS/iPadOS può essere abilitata solo durante l'installazione iniziale del dispositivo usando Device Enrollment Program di Apple o Apple Configurator. Dopo aver abilitato la modalità di supervisione, Intune può configurare un dispositivo con le funzionalità seguenti:

- Blocco dell'app (modalità app singola) 
- Proxy HTTP globale 
- Disabilitare Blocco attivazione 
- Modalità applicazione singola autonoma 
- Filtro contenuto Web 
- Impostazione dello sfondo e della schermata di blocco 
- Push app invisibile all'utente 
- VPN Always On 
- Installazione esclusivamente di app gestite 
- iBookstore 
- iMessages 
- Area giochi 
- AirDrop 
- AirPlay 
- Associazione di host 
- Sincronizzazione cloud 
- Ricerca Spotlight 
- Handoff 
- Cancellazione di dispositivi 
- Interfaccia utente restrizioni 
- Installazione di profili di configurazione tramite interfaccia utente 
- Notizie 
- Tasti di scelta rapida 
- Modifica del passcode 
- Modifica di nomi di dispositivo 
- Download automatici delle app 
- Apple Music 
- Mail Drop 
- Associazione con Apple Watch 

> [!NOTE]
> Apple ha confermato che nel 2019 alcune impostazioni passeranno alla modalità solo con supervisione. È consigliabile usare le impostazioni interessate tenendo conto di questo aspetto, anziché attendere che Apple effettui la migrazione alla modalità solo con supervisione:
>
> - Installazione di app da parte degli utenti finali
> - Rimozione di app
> - FaceTime
> - Safari
> - iTunes
> - Contenuti espliciti
> - Documenti e dati iCloud
> - Gioco multiplayer
> - Aggiungi amici dell'area giochi
> - Siri

## <a name="next-steps"></a>Passaggi successivi

[Assegnare il profilo](device-profile-assign.md) e [monitorarne lo stato](device-profile-monitor.md).

È possibile limitare funzionalità e impostazioni anche in dispositivi [macOS](device-restrictions-macos.md).
