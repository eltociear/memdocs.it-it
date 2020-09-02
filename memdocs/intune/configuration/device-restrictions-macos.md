---
title: Impostazioni dei dispositivi macOS in Microsoft Intune - Azure | Microsoft Docs
titleSuffix: ''
description: Aggiungere, configurare o creare le impostazioni nei dispositivi macOS per limitare l'uso delle funzionalità, tra cui impostare i requisiti per le password, controllare la schermata di blocco, usare le app predefinite, aggiungere app con restrizioni o approvate, gestire i dispositivi Bluetooth, connettersi al cloud per backup e archiviazione, abilitare la modalità tutto schermo, aggiungere domini e controllare il modo in cui gli utenti interagiscono con il Web browser Safari in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/06/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: kakyker; annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c068a092ad0f7087ad28b8424cc2640214972f82
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88996691"
---
# <a name="macos-device-settings-to-allow-or-restrict-features-using-intune"></a>Impostazioni dei dispositivi macOS per consentire o limitare l'uso delle funzionalità tramite Intune

Questo articolo descrive le diverse impostazioni che è possibile controllare nei dispositivi macOS. Usare queste impostazioni nella propria soluzione di gestione di dispositivi mobili (MDM) per abilitare o disabilitare funzionalità, impostare regole per le password, consentire o limitare l'uso di app specifiche e altro ancora.

Queste impostazioni vengono aggiunte a un profilo di configurazione del dispositivo in Intune e quindi assegnate o distribuite ai dispositivi macOS.

> [!NOTE]
> L'interfaccia utente potrebbe non corrispondere ai tipi di iscrizione indicati in questo articolo. Le informazioni contenute in questo articolo sono corrette. L'interfaccia utente verrà aggiornata in una versione futura.

## <a name="before-you-begin"></a>Prima di iniziare

[Creare un profilo di configurazione delle restrizioni del dispositivo macOS](device-restrictions-configure.md).

> [!NOTE]
> Queste impostazioni si applicano a diversi tipi di registrazione. Per altre informazioni sui diversi tipi di registrazione, vedere [Registrazione di macOS](../enrollment/macos-enroll.md).

## <a name="built-in-apps"></a>App predefinite

### <a name="settings-apply-to-all-enrollment-types"></a>Le impostazioni si applicano a: Tutti i tipi di registrazione

- **Blocca il riempimento automatico di Safari**: **Sì** disabilita la funzionalità di riempimento automatico in Safari sui dispositivi. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di modificare le impostazioni di completamento automatico nel Web browser.
- **Blocca l'uso della fotocamera**: **Sì** impedisce l'accesso alla fotocamera sui dispositivi. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'accesso alla fotocamera del dispositivo.

  Intune gestisce solo l'accesso alla fotocamera del dispositivo. Non ha accesso alle immagini o ai video.
  
- **Blocca Apple Music**: **Sì** ripristina la modalità classica per l'app Music e disabilita il servizio Music. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'uso dell'app Apple Music.
- **Blocca i suggerimenti in evidenza**: **Sì** impedisce a Spotlight di restituire risultati da una ricerca su Internet. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire alla ricerca Spotlight di connettersi a Internet per ottenere i risultati della ricerca.
- **Blocca il trasferimento di file con Finder o iTunes**: **Sì** disabilita i servizi di condivisione file dell'applicazione. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire i servizi di condivisione file dell'applicazione.

  Questa funzionalità si applica a:  
  - macOS 10.13 e versioni successive

## <a name="cloud-and-storage"></a>Cloud e risorse di archiviazione

### <a name="settings-apply-to-all-enrollment-types"></a>Le impostazioni si applicano a: Tutti i tipi di registrazione

- **Blocca la sincronizzazione Keychain con iCloud**: **Sì** disattiva la sincronizzazione delle credenziali archiviate in Keychain con iCloud. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di sincronizzare queste credenziali.
- **Blocca la sincronizzazione iCloud di Scrivania e Documenti**: **Si** impedisce a iCloud di sincronizzare documenti e dati. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire la sincronizzazione di documenti e coppie chiave-valore nello spazio di archiviazione iCloud.
- **Blocca il backup della posta elettronica di iCloud**: **Si** impedisce la sincronizzazione di iCloud con l'app Mail di macOS. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire la sincronizzazione della posta su iCloud.
- **Blocca il backup dei contatti iCloud**: **Sì** impedisce a iCloud di sincronizzare i contatti sul dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire la sincronizzazione dei contatti usando iCloud.
- **Blocca il backup dei calendari di iCloud**: **Sì** impedisce la sincronizzazione di iCloud con l'app Calendario di macOS. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire la sincronizzazione del calendario su iCloud.
- **Blocca il backup dei promemoria di iCloud**: **Sì** impedisce la sincronizzazione di iCloud con l'app Promemoria di macOS. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire la sincronizzazione dei promemoria su iCloud.
- **Blocca il backup dei segnalibri di iCloud**: **Sì** impedisce a iCloud di sincronizzare i segnalibri sul dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire la sincronizzazione dei segnalibri su iCloud.
- **Blocca il backup delle note di iCloud**: **Sì** impedisce a iCloud di sincronizzare le note sul dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire la sincronizzazione delle note su iCloud.
- **Blocca il backup delle foto di iCloud**: **Sì** disabilita la Libreria foto di iCloud e impedisce a iCloud di sincronizzare le foto dei dispositivi. Eventuali foto non scaricate completamente dalla libreria foto di iCloud vengono rimosse dall'archivio locale nei dispositivi. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire la sincronizzazione delle foto tra il dispositivo e la libreria foto di iCloud.
- **Blocca l'handofff**: questa funzionalità consente agli utenti di avviare il lavoro in un dispositivo macOS e quindi continuare il lavoro avviato in un altro dispositivo iOS/iPadOS o macOS. **Sì** impedisce la funzionalità Handoff sul dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire questa funzionalità nei dispositivi.

  Questa funzionalità si applica a:  
  - macOS 10.15 e versioni successive

## <a name="connected-devices"></a>Dispositivi connessi

### <a name="settings-apply-to-all-enrollment-types"></a>Le impostazioni si applicano a: Tutti i tipi di registrazione

- **Blocca AirDrop**: **Sì** impedisce l'uso di AirDrop sui dispositivi. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'uso della funzionalità AirDrop per scambiare contenuti con dispositivi vicini.
- **Blocca lo sbocco automatico di Apple Watch**: **Sì** impedisce agli utenti di sbloccare il proprio dispositivo macOS con Apple Watch. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di sbloccare il proprio dispositivo macOS con Apple Watch.

## <a name="domains"></a>Domains

### <a name="settings-apply-to-all-enrollment-types"></a>Le impostazioni si applicano a: Tutti i tipi di registrazione

- **Domini di posta elettronica non contrassegnati**: immettere uno o più **URL dei domini di posta elettronica** nell'elenco. Quando gli utenti inviano o ricevono un messaggio di posta elettronica da domini diversi da quelli immessi, il messaggio di posta elettronica viene contrassegnato come non attendibile nell'app Mail di macOS.

## <a name="general"></a>Generale

### <a name="settings-apply-to-all-enrollment-types"></a>Le impostazioni si applicano a: Tutti i tipi di registrazione

- **Blocca la ricerca**: **Sì** impedisce all'utente di evidenziare una parola e quindi di cercarne la definizione sul dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire la funzionalità di ricerca della definizione.
- **Blocca la dettatura**: **Sì** impedisce agli utenti di immettere testo con l'input vocale. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di usare l'input tramite dettatura.
- **Blocca la memorizzazione del contenuto nella cache**: **Sì** impedisce la memorizzazione del contenuto nella cache. La memorizzazione del contenuto nella cache consente di archiviare i dati di app e Web browser, download e altro ancora localmente nei dispositivi. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe abilitare la memorizzazione del contenuto nella cache.

  Per altre informazioni sulla memorizzazione del contenuto nella cache in macOS, vedere [Gestire la cache dei contenuti sul Mac](https://support.apple.com/guide/mac-help/manage-content-caching-on-mac-mchl3b6c3720/mac) (viene aperto un altro sito Web).

  Questa funzionalità si applica a:  
  - macOS 10.13 e versioni successive

- **Rinvia gli aggiornamenti software**: **Sì** consente di posticipare la visualizzazione degli aggiornamenti software nei dispositivi, da 0 a 90 giorni. Questa impostazione non controlla quando gli aggiornamenti vengono installati o meno. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe visualizzare gli aggiornamenti nei dispositivi quando Apple li rilascia. Ad esempio, se un aggiornamento macOS viene rilasciato da Apple in una data specifica, questo viene normalmente visualizzato nei dispositivi in prossimità della data di rilascio. Gli aggiornamenti della seed build sono consentiti senza posticipazioni.  

  - **Posticipa la visibilità degli aggiornamenti software**: immettere un valore compreso tra 0 e 90 giorni. Quando l'intervallo di ritardo scade, gli utenti ricevono una notifica per l'aggiornamento alla versione del sistema operativo meno recente disponibile quando è stato attivato il ritardo.

    Ad esempio, se un aggiornamento di macOS è disponibile il **1° gennaio** e **Posticipa la visibilità** è impostato su **5 giorni**, l'aggiornamento non viene visualizzato come disponibile. Il **sesto giorno** dopo il rilascio, l'aggiornamento diventa disponibile e gli utenti possono installarlo.

    Questa funzionalità si applica a:  
    - macOS 10.13.4 e versioni successive

- **Blocca la registrazione di screenshot e di schermate**: il dispositivo deve essere registrato con la registrazione automatica dei dispositivi (DEP) di Apple. **Sì** impedisce agli utenti di salvare screenshot dello schermo. Inoltre, l'app Classroom non è in grado di osservare le schermate remote. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di acquisire gli screenshot e consente all'app Classroom di visualizzare le schermate remote.

  - **Disabilita AirPlay, la visualizzazione dello schermo da parte dell'app Classroom e la condivisione dello schermo**: **Sì** blocca AirPlay e impedisce la condivisione dello schermo con altri dispositivi. Impedisce anche ai docenti di usare l'app Classroom per visualizzare gli schermi degli studenti. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire ai docenti di visualizzare gli schermi degli studenti.

    Per usare questa impostazione impostare **Blocca screenshot e registrazioni dello schermo** su **Non configurato** (gli screenshot sono consentiti).

  - **Consenti all'app Classroom di eseguire AirPlay e visualizzare lo schermo senza chiedere conferma**: **Sì** consente ai docenti di visualizzare gli schermi degli studenti senza richiedere il loro consenso. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe richiedere agli studenti di dare il loro consenso prima che i docenti possano visualizzare gli schermi.

    Per usare questa impostazione impostare **Blocca screenshot e registrazioni dello schermo** su **Non configurato** (gli screenshot sono consentiti).

- **Richiedi l'autorizzazione del docente per abbandonare lezioni non gestite dell'app Classroom**: **Sì** impone agli studenti iscritti a un corso di Classroom non gestito di ottenere l'approvazione del docente per lasciare il corso. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli studenti di abbandonare il corso quando vogliono.

- **Consenti a Classroom di bloccare il dispositivo senza chiedere conferma**: **Sì** Consente ai docenti di bloccare il dispositivo o l'app di uno studente senza l'approvazione da parte dello studente. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe richiedere agli studenti di dare il loro consenso prima che i docenti possano bloccare il dispositivo o l'app.

- **Gli studenti possono partecipare automaticamente a una lezione di Classroom senza chiedere conferma**: **Sì** consente agli studenti di partecipare a una lezione senza inviare richieste al docente. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe richiedere l'approvazione del docente per la partecipazione a una lezione.

## <a name="password"></a>Password

### <a name="settings-apply-to-all-enrollment-types"></a>Le impostazioni si applicano a: Tutti i tipi di registrazione

- **Richiedi password**: **Sì** Impone agli utenti di immettere una password per accedere ai dispositivi. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe non richiedere una password. Non impone inoltre alcuna restrizione, ad esempio il blocco delle password semplici o l'impostazione di una lunghezza minima.
  - **Tipo di password richiesto**: immettere il livello di complessità della password richiesto dall'organizzazione. Quando il campo è vuoto, Intune non modifica o aggiorna questa impostazione. Le opzioni disponibili sono:
    - **Non configurata**: usa il valore predefinito del dispositivo.
    - **Alfanumerica**: include lettere maiuscole, lettere minuscole e caratteri numerici.
    - **Numerica**: la password deve essere composta solo da numeri, ad esempio 123456789.

    Questa funzionalità si applica a:  
    - macOS 10.10.3 e versioni successive

  - **Numero di caratteri non alfanumerici nella password**: immettere il numero di caratteri complessi richiesti per la password, da 0 a 4. Un carattere complesso è un simbolo, ad esempio `?`. Quando questa opzione è lasciata vuota o impostata su **Non configurato**, Intune non modifica o aggiorna questa impostazione.
  - **Lunghezza minima password**: immettere la lunghezza minima per la password, da 4 a 16 caratteri. Quando il campo è vuoto, Intune non modifica o aggiorna questa impostazione.
  - **Blocca le password semplici**: **Sì** consente l'uso di password semplici, ad esempio `0000` o `1234`. Quando il valore è vuoto o impostato su **Non configurato**, Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire password semplici.
  - **Numero massimo di minuti di inattività fino al blocco dello schermo**: immettere il periodo di tempo per cui i dispositivi devono rimanere inattivi prima che lo schermo venga bloccato automaticamente. Ad esempio, immettere `5` per bloccare i dispositivi dopo 5 minuti di inattività. Quando il valore è vuoto o impostato su **Non configurato**, Intune non modifica o aggiorna questa impostazione.
  - **Numero massimo di minuti dopo il blocco dello schermo prima che venga richiesta una password**: immettere il periodo di tempo per cui i dispositivi devono essere inattivi prima che venga richiesta una password per sbloccarli. Quando il valore è vuoto o impostato su **Non configurato**, Intune non modifica o aggiorna questa impostazione.
  - **Scadenza password (giorni)** : immettere il numero di giorni che devono trascorrere prima che sia necessario cambiare la password del dispositivo, da 1 a 65535. Ad esempio, immettere `90` per impostare la scadenza della password dopo 90 giorni. Quando la password scade, agli utenti viene chiesto di creare una nuova password. Quando il valore è vuoto o impostato su **Non configurato**, Intune non modifica o aggiorna questa impostazione.
  - **Impedisci riutilizzo delle password precedenti**: impedire agli utenti di creare password già usate in precedenza, immettere il numero di password usate in precedenza che non è possibile usare, da 1 a 24. Ad esempio, immettere 5 in modo che gli utenti non possano impostare una nuova password uguale alla password corrente o a una qualsiasi delle quattro precedenti. Quando il valore è vuoto, Intune non modifica o aggiorna questa impostazione.

- **Impedisci all'utente di modificare il passcode**: **Sì** impedisce la modifica, l'aggiunta o la rimozione del passcode. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'aggiunta, la modifica o la rimozione dei passcode.

- **Impedisci l'uso di Touch ID per sbloccare il dispositivo**: **Sì** impedisce l'uso di impronte digitali per sbloccare i dispositivi. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di sbloccare il dispositivo tramite impronta digitale.

- **Blocca il riempimento automatico delle password**: **Sì** impedisce l'uso della funzionalità di riempimento automatico delle password su macOS. La scelta **Si** comporta anche le conseguenze seguenti:

  - Agli utenti non viene richiesto di usare una password salvata in Safari o in qualsiasi app.
  - Le password complesse automatiche sono disabilitate e non vengono consigliate password complesse agli utenti.

  Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire queste funzionalità.

- **Blocca le richieste di prossimità password**: **Sì** impedisce ai dispositivi di richiedere password dai dispositivi nelle vicinanze. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire queste richieste di password.

- **Blocca la condivisione delle password**: **Sì** impedisce la condivisione delle password tra i dispositivi tramite AirDrop. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire la condivisione di queste password.

## <a name="privacy-preferences"></a>Preferenze per la privacy

Nei dispositivi macOS le app e i processi spesso richiedono agli utenti di consentire o negare l'accesso alle funzionalità del dispositivo, ad esempio la fotocamera, il microfono, il calendario, la cartella dei documenti e altro ancora. Queste impostazioni consentono agli amministratori di approvare o negare preventivamente l'accesso a queste funzionalità del dispositivo. Quando si configurano queste impostazioni è possibile gestire il consenso per l'accesso ai dati per conto degli utenti. Le impostazioni sostituiscono le decisioni precedenti.

L'obiettivo di queste impostazioni è ridurre il numero di richieste da parte di app e processi.

Questa funzionalità si applica a:

- macOS 10.14 e versioni successive
- Alcune impostazioni si applicano a macOS 10.15 e versioni successive.
- Queste impostazioni si applicano solo ai dispositivi in cui è installato il profilo delle preferenze di privacy prima di essere aggiornati.

### <a name="settings-apply-to-user-approved-device-enrollment-automated-device-enrollment"></a>Le impostazioni si applicano a: Registrazione dei dispositivi approvata dall'utente e registrazione automatica dei dispositivi

- **App e processi**: **Aggiungere** app o processi per configurare l'accesso. Specificare anche:
  - **Nome**: immettere un nome per l'app o il processo. Ad esempio, immettere `Microsoft Remote Desktop` o `Microsoft 365`.
  
  - **tipo di identificatore**: Le opzioni disponibili sono:
    - **Bundle ID**: selezionare questa opzione per le app.
    - **Percorso**: selezionare questa opzione per i file binari non in bundle, ovvero per processo o un eseguibile.

    Gli strumenti di supporto incorporati all'interno di un bundle di applicazioni ereditano automaticamente le autorizzazioni del bundle di applicazioni incluse.

  - **Identificatore**: immettere il bundle ID dell'app o il percorso del file di installazione del processo o dell'eseguibile. Immettere ad esempio `com.contoso.appname`.

    Per ottenere l'ID bundle dell'app, aprire l'app Terminal ed eseguire il `codesign`comando. Questo comando identifica la firma del codice. È quindi possibile ottenere contemporaneamente l'ID bundle e la firma del codice.

  - **Requisito del codice**: immettere la firma del codice per l'applicazione o il processo.

    Quando un'app o un file binario vengono firmati da un certificato di sviluppo viene creata una firma del codice. Per trovare la designazione eseguire manualmente il comando `codesign` nell'app Terminal: `codesign --display -r - /path/to/app/binary`. La firma del codice è l'unica cosa che viene visualizzata dopo `=>`.

  - **Abilita la convalida del codice statico**: scegliere **Sì** per l'app o il processo per convalidare in modo statico il requisito del codice. Quando questa opzione è impostata su **Non configurato**, Intune non modifica o aggiorna questa impostazione.

    Abilitare questa impostazione solo se il processo invalida la firma del codice dinamico. In caso contrario, usare l'opzione **Non configurato**.  

  - **Blocca la fotocamera**: **Sì** impedisce all'app di accedere alla fotocamera di sistema. Non è possibile consentire l'accesso alla fotocamera. Quando questa opzione è impostata su **Non configurato**, Intune non modifica o aggiorna questa impostazione.

  - **Blocca il microfono**: **Sì** impedisce all'app di accedere alla microfono di sistema. Non è possibile consentire l'accesso alla microfono. Quando questa opzione è impostata su **Non configurato**, Intune non modifica o aggiorna questa impostazione.

  - **Blocca la registrazione dello schermo**: **Sì** impedisce all'app di acquisire il contenuto della visualizzazione di sistema. Non è possibile consentire l'accesso alla registrazione dello schermo e all'acquisizione dello schermo. Quando questa opzione è impostata su **Non configurato**, Intune non modifica o aggiorna questa impostazione.

    Richiede macOS 10.15 e versioni successive.

  - **Blocca il monitoraggio degli input**: **Sì** impedisce all'app di usare le API CoreGraphics e HID per ascoltare CGEvents ed eventi HID da tutti i processi. **Sì** nega inoltre alle app e ai processi l'ascolto e la raccolta dei dati dai dispositivi di input, ad esempio mouse, tastiera o trackpad. Non è possibile consentire l'accesso alle API CoreGraphics e HID.

    Quando questa opzione è impostata su **Non configurato**, Intune non modifica o aggiorna questa impostazione.

    Richiede macOS 10.15 e versioni successive.

  - **Riconoscimento vocale**: Le opzioni disponibili sono:
    - **Non configurata**: Intune non modifica o aggiorna questa impostazione.
    - **Consenti**: consente all'app di accedere al riconoscimento vocale del sistema e consente l'invio di dati vocali ad Apple.
    - **Blocca**: impedisce all'app di accedere al riconoscimento vocale del sistema e impedisce l'invio di dati vocali ad Apple.

    Richiede macOS 10.15 e versioni successive.

  - **Accessibilità**: Le opzioni disponibili sono:
    - **Non configurata**: Intune non modifica o aggiorna questa impostazione.
    - **Consenti**: consente all'app di accedere all'app Accessibilità di sistema. Questa app include sottotitoli codificati, testo al passaggio del mouse e controllo vocale.
    - **Blocca**: impedisce all'app di accedere all'app Accessibilità di sistema.

  - **Contatti**: Le opzioni disponibili sono:
    - **Non configurata**: Intune non modifica o aggiorna questa impostazione.
    - **Consenti**: consente all'app di accedere alle informazioni di contatto gestite dall'app Contatti di sistema.  
    - **Blocca**: impedisce all'app di accedere a queste informazioni dei contatti.

  - **Calendario**: Le opzioni disponibili sono:
    - **Non configurata**: Intune non modifica o aggiorna questa impostazione.
    - **Consenti**: consente all'app di accedere alle informazioni del calendario gestite dall'app Calendario di sistema.
    - **Blocca**: impedisce all'app di accedere a queste informazioni del calendario.

  - **Promemoria**: Le opzioni disponibili sono:
    - **Non configurata**: Intune non modifica o aggiorna questa impostazione.
    - **Consenti**: consente all'app di accedere alle informazioni dei promemoria gestite dall'app Promemoria di sistema.
    - **Blocca**: impedisce all'app di accedere a queste informazioni dei promemoria.

  - **Foto**: Le opzioni disponibili sono:
    - **Non configurata**: Intune non modifica o aggiorna questa impostazione.
    - **Consenti**: consente all'app di accedere alle immagini gestite dall'app Foto di sistema in `~/Pictures/.photoslibrary`.
    - **Blocca**: impedisce all'app di accedere a queste foto.

  - **Catalogo multimediale**: Le opzioni disponibili sono:
    - **Non configurata**: Intune non modifica o aggiorna questa impostazione.
    - **Consenti**: consente all'app di accedere ad Apple Music, ad attività musicali e video e al catalogo multimediale.  
    - **Blocca**: impedisce all'app di accedere a questi media.

    Richiede macOS 10.15 e versioni successive.

  - **Presenza del file provider**: Le opzioni disponibili sono:
    - **Non configurata**: Intune non modifica o aggiorna questa impostazione.
    - **Consenti**: consente all'app di accedere all'app File Provider e di capire quando gli utenti usano i file gestiti dal File Provider. Un'app File Provider consente ad altre app File Provider di accedere a documenti e directory archiviati e gestiti dall'app in cui sono contenuti.
    - **Blocca**: impedisce all'app di accedere all'app File Provider.

    Richiede macOS 10.15 e versioni successive.

  - **Accesso completo al disco**: Le opzioni disponibili sono:
    - **Non configurata**: Intune non modifica o aggiorna questa impostazione.
    - **Consenti**: consente all'app di accedere a tutti i file protetti, inclusi i file di amministrazione di sistema. Applicare questa impostazione con cautela.
    - **Blocca**: impedisce all'app di accedere a questi file protetti.

  - **File di amministrazione di sistema**: Le opzioni disponibili sono:
    - **Non configurata**: Intune non modifica o aggiorna questa impostazione.
    - **Consenti**: consente all'app di accedere ad alcuni file usati nell'amministrazione di sistema.
    - **Blocca**: impedisce all'app di accedere a questi file.

  - **Cartella Desktop:** : Le opzioni disponibili sono:
    - **Non configurata**: Intune non modifica o aggiorna questa impostazione.
    - **Consenti**: consente all'app di accedere ai file nella cartella Desktop dell'utente.
    - **Blocca**: impedisce all'app di accedere a questi file.

    Richiede macOS 10.15 e versioni successive.

  - **Cartella Documenti**: Le opzioni disponibili sono:
    - **Non configurata**: Intune non modifica o aggiorna questa impostazione.
    - **Consenti**: consente all'app di accedere ai file nella cartella Documenti dell'utente.
    - **Blocca**: impedisce all'app di accedere a questi file.

    Richiede macOS 10.15 e versioni successive.

  - **Cartella Download:** : Le opzioni disponibili sono:
    - **Non configurata**: Intune non modifica o aggiorna questa impostazione.
    - **Consenti**: consente all'app di accedere ai file nella cartella Download dell'utente.
    - **Blocca**: impedisce all'app di accedere a questi file.

    Richiede macOS 10.15 e versioni successive.

  - **Volumi di rete**: Le opzioni disponibili sono:
    - **Non configurata**: Intune non modifica o aggiorna questa impostazione.
    - **Consenti**: consente all'app di accedere ai file nei volumi di rete.
    - **Blocca**: impedisce all'app di accedere a questi file.

    Richiede macOS 10.15 e versioni successive.

  - **Volumi rimovibili**: Le opzioni disponibili sono:
    - **Non configurata**: Intune non modifica o aggiorna questa impostazione.
    - **Consenti**: consente all'app di accedere ai file su volumi rimovibili, ad esempio un disco rigido.
    - **Blocca**: impedisce all'app di accedere a questi file.

    Richiede macOS 10.15 e versioni successive.

  - **Eventi di sistema**: Le opzioni disponibili sono:
    - **Non configurata**: Intune non modifica o aggiorna questa impostazione.
    - **Consenti**: consente all'app di usare le API CoreGraphics per inviare CGEvents al flusso di eventi di sistema.
    - **Blocca**: impedisce all'app di usare le API CoreGraphics per inviare CGEvents al flusso di eventi di sistema.

  - **Eventi Apple**: questa impostazione consente alle app di inviare un evento Apple con restrizioni a un'altra app o processo. Selezionare **Aggiungi** per aggiungere un'app o un processo di destinazione. Immettere le informazioni seguenti dell'app o del processo di destinazione:

    - **Tipo di identificatore**: selezionare **Bundle ID** se l'identificatore di destinazione è un'applicazione. Selezionare **Percorso** se l'identificatore di destinazione è un processo o un eseguibile.
    
    - **Identificatore**: immettere il bundle ID dell'app o il percorso di installazione del processo di destinazione dell'evento Apple.  

    - **Requisito del codice**: immettere la firma del codice per l'applicazione o il processo.

      Quando un'app o un file binario vengono firmati da un certificato di sviluppo viene creata una firma del codice. Per trovare la designazione eseguire manualmente il comando `codesign` nell'app Terminal: `codesign --display -r -/path/to/app/binary`. La firma del codice è l'unica cosa che viene visualizzata dopo `=>`.

    - **Accesso**: consente l'invio di un evento Apple macOS all'app o al processo di destinazione. Le opzioni disponibili sono:
      - **Non configurata**: Intune non modifica o aggiorna questa impostazione.
      - **Consenti**: consente all'app o al processo di inviare l'evento Apple con restrizioni all'app o al processo di destinazione.
      - **Blocca**: impedisce all'app o al processo di inviare l'evento Apple con restrizioni all'app o al processo di destinazione.

  - **Salvare** le modifiche.

## <a name="restricted-apps"></a>App con restrizioni

### <a name="settings-apply-to-all-enrollment-types"></a>Le impostazioni si applicano a: Tutti i tipi di registrazione

- **Elenco di tipi di app con restrizioni**: consente di creare un elenco di app che gli utenti non sono autorizzati a installare o usare. Le opzioni disponibili sono:

  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, gli utenti potrebbero avere accesso alle app assegnate e alle app predefinite.
  - **App approvate**: Elencare le app che gli utenti sono autorizzati a installare. Per mantenere la conformità, gli utenti non devono installare altre app. Le app gestite da Intune sono consentite automaticamente, inclusa l'app Portale aziendale. Agli utenti non viene impedito di installare un'app non inclusa nell'elenco approvato. Tuttavia, se lo fanno, verrà segnalato in Intune.
  - **App non consentite**: elencare le app non gestite da Intune che gli utenti non sono autorizzati a installare ed eseguire. Agli utenti non viene impedito di installare un'app vietata. Se un utente installa un'app da questo elenco, verrà segnalato in Intune.

- **Elenco di app**: **Aggiungere** app all'elenco:
  - **ID bundle dell'app**: immettere l'[ID bundle](bundle-ids-built-in-ios-apps.md) dell'app. È possibile mostrare o nascondere le applicazioni predefinite e le applicazioni line-of-business. Il sito Web di Apple include un elenco di [app Apple predefinite](https://support.apple.com/HT208094).

    Per trovare l'URL di un'app, aprire iTunes App Store e cercare l'app. Ad esempio, cercare `Microsoft Remote Desktop` o `Microsoft Word`. Selezionare l'app e copiare l'URL. È anche possibile usare iTunes per trovare l'app e quindi usare l'attività **Copia collegamento** per ottenere l'URL dell'app.

  - **Nome app**: immettere un nome descrittivo per facilitare l'identificazione dell'ID bundle. Immettere ad esempio `Intune Company Portal app`.
  - **Autore**: immettere l'autore dell'app.

- Scegliere **Importa** per importare un file CSV con i dettagli sull'app, incluso l'URL. Usare il formato `<app bundle ID>, <app name>, <app publisher>`. Oppure **Esporta** per creare un elenco delle app aggiunte, nello stesso formato.

## <a name="next-steps"></a>Passaggi successivi

[Assegnare il profilo](device-profile-assign.md) e [monitorarne lo stato](device-profile-monitor.md).

È possibile limitare funzionalità e impostazioni anche nei dispositivi [iOS/iPadOS](device-restrictions-ios.md).
