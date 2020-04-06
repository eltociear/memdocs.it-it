---
title: Impostazioni dei dispositivi macOS in Microsoft Intune - Azure | Microsoft Docs
titleSuffix: ''
description: Aggiungere, configurare o creare le impostazioni nei dispositivi macOS per limitare l'uso delle funzionalità, tra cui impostare i requisiti per le password, controllare la schermata di blocco, usare le app predefinite, aggiungere app con restrizioni o approvate, gestire i dispositivi Bluetooth, connettersi al cloud per backup e archiviazione, abilitare la modalità tutto schermo, aggiungere domini e controllare il modo in cui gli utenti interagiscono con il Web browser Safari in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/30/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 50dd3d245b9a89836e3858d71a7ad124189e0973
ms.sourcegitcommit: e2877d21dfd70c4029c247275fa2b38e76bd22b8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/31/2020
ms.locfileid: "80407859"
---
# <a name="macos-device-settings-to-allow-or-restrict-features-using-intune"></a>Impostazioni dei dispositivi macOS per consentire o limitare l'uso delle funzionalità tramite Intune

Questo articolo descrive le diverse impostazioni che è possibile controllare nei dispositivi macOS. Usare queste impostazioni nella propria soluzione di gestione di dispositivi mobili (MDM) per abilitare o disabilitare funzionalità, impostare regole per le password, consentire o limitare l'uso di app specifiche e altro ancora.

Queste impostazioni vengono aggiunte a un profilo di configurazione del dispositivo in Intune e quindi assegnate o distribuite ai dispositivi macOS.

## <a name="before-you-begin"></a>Prima di iniziare

[Creare un profilo di configurazione delle restrizioni del dispositivo](device-restrictions-configure.md).

> [!NOTE]
> Queste impostazioni si applicano a diversi tipi di registrazione. Per altre informazioni sui diversi tipi di registrazione, vedere [Registrazione di macOS](../enrollment/macos-enroll.md).

## <a name="general"></a>Generale

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Le impostazioni si applicano a: Registrazione dei dispositivi e registrazione automatica dei dispositivi

- **Ricerca della definizione**: **Blocca** impedisce all'utente di evidenziare una parola e quindi di cercarne la definizione nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire la funzionalità di ricerca della definizione.
- **Dettatura**: **Blocca** impedisce agli utenti di immettere testo con l'input vocale. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di usare l'input tramite dettatura.
- **Memorizzazione nella cache dei contenuti**: **Blocca** impedisce la memorizzazione del contenuto nella cache. La memorizzazione del contenuto nella cache consente di archiviare i dati di app e Web browser, download e altro ancora localmente nei dispositivi. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe abilitare la memorizzazione del contenuto nella cache.

  Per altre informazioni sulla memorizzazione del contenuto nella cache in macOS, vedere [Gestire la cache dei contenuti sul Mac](https://support.apple.com/guide/mac-help/manage-content-caching-on-mac-mchl3b6c3720/mac) (viene aperto un altro sito Web).

  Questa funzionalità si applica a:  
  - macOS 10.13 e versioni successive

- **Rinvia gli aggiornamenti software**: **Abilita** consente di posticipare la visualizzazione degli aggiornamenti software nei dispositivi, da 0 a 90 giorni. Questa impostazione non controlla quando gli aggiornamenti vengono installati o meno. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe visualizzare gli aggiornamenti nei dispositivi quando Apple li rilascia. Ad esempio, se un aggiornamento macOS viene rilasciato da Apple in una data specifica, questo viene normalmente visualizzato nei dispositivi in prossimità della data di rilascio. Gli aggiornamenti della seed build sono consentiti senza posticipazioni.  

  - **Posticipa la visibilità degli aggiornamenti software**: immettere un valore compreso tra 0 e 90 giorni. Quando l'intervallo di ritardo scade, gli utenti ricevono una notifica per l'aggiornamento alla versione del sistema operativo meno recente disponibile quando è stato attivato il ritardo.

    Ad esempio, se un aggiornamento di macOS è disponibile il **1° gennaio** e **Posticipa la visibilità** è impostato su **5 giorni**, l'aggiornamento non viene visualizzato come disponibile. Il **sesto giorno** dopo il rilascio, l'aggiornamento diventa disponibile e gli utenti possono installarlo.

    Questa funzionalità si applica a:  
    - macOS 10.13.4 e versioni successive

- **Screenshot**: il dispositivo deve essere registrato con la registrazione automatica dei dispositivi (DEP) di Apple. **Blocca** impedisce agli utenti di salvare screenshot dello schermo. Inoltre, l'app Classroom non è in grado di osservare le schermate remote. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di acquisire gli screenshot e consente all'app Classroom di visualizzare le schermate remote.

### <a name="settings-apply-to-automated-device-enrollment"></a>Le impostazioni si applicano a: Registrazione automatica dei dispositivi

- **Osservazione in remoto dello schermo tramite l'app Classroom**: **Disabilita** impedisce ai docenti di usare l'app Classroom per visualizzare gli schermi degli studenti. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire ai docenti di visualizzare gli schermi degli studenti.

  Per usare questa impostazione, impostare **Screenshot** su **Non configurato** (gli screenshot sono consentiti).

- **Osservazione schermo non richiesta da parte dell'app Classroom**: **Consenti** consente ai docenti di visualizzare gli schermi degli studenti senza richiedere il loro consenso. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe richiedere agli studenti di dare il loro consenso prima che i docenti possano visualizzare gli schermi.

  Per usare questa impostazione, impostare **Screenshot** su **Non configurato** (gli screenshot sono consentiti).

- **Gli studenti devono richiedere l'autorizzazione per abbandonare la lezione di Classroom**: con l'impostazione **Rendi obbligatorio** gli studenti iscritti a un corso di Classroom non gestito devono ottenere l'approvazione del docente per abbandonare il corso. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli studenti di abbandonare il corso quando vogliono.

- **I docenti possono bloccare automaticamente dispositivi o app nell'app Classroom**: con l'impostazione **Consenti** i docenti possono bloccare il dispositivo o l'app di uno studente senza l'approvazione da parte dello studente. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe richiedere agli studenti di dare il loro consenso prima che i docenti possano bloccare il dispositivo o l'app.

- **Gli utenti possono partecipare automaticamente a una lezione di Classroom**: con l'impostazione **Consenti** gli studenti possono partecipare a una lezione senza inviare richieste al docente. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe richiedere l'approvazione del docente per la partecipazione a una lezione.

## <a name="password"></a>Password

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Le impostazioni si applicano a: Registrazione dei dispositivi e registrazione automatica dei dispositivi

- **Password**: **Rendi obbligatorio** richiede agli utenti di immettere una password per accedere ai dispositivi. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe non richiedere una password. Non impone inoltre alcuna restrizione, ad esempio il blocco delle password semplici o l'impostazione di una lunghezza minima.
  - **Tipo di password richiesto**: immettere il livello di complessità della password richiesto dall'organizzazione. Le opzioni disponibili sono:
    - **Non configurata**: Intune non modifica o aggiorna questa impostazione.
    - **Numerica**: la password deve essere composta solo da numeri, ad esempio 123456789.
    - **Alfanumerica**: include lettere maiuscole, lettere minuscole e caratteri numerici.

    Questa funzionalità si applica a:  
    - macOS 10.10.3 e versioni successive

  - **Numero di caratteri non alfanumerici nella password**: immettere il numero di caratteri complessi richiesti per la password, da 0 a 4. Un carattere complesso è un simbolo, ad esempio `?`
  - **Lunghezza minima password**: immettere la lunghezza minima per la password, da 4 a 16 caratteri.
  - **Password semplici**: consente l'uso di password semplici, ad esempio `0000` o `1234`.
  - **Numero massimo di minuti dopo il blocco dello schermo prima che venga richiesta una password**: immettere il periodo di tempo per cui i dispositivi devono essere inattivi prima che venga richiesta una password per sbloccarli. Quando il valore è vuoto o impostato su **Non configurato**, Intune non modifica o aggiorna questa impostazione.
  - **Numero massimo di minuti di inattività fino al blocco dello schermo**: immettere il periodo di tempo per cui i dispositivi devono rimanere inattivi prima che lo schermo venga bloccato automaticamente. Ad esempio, immettere 5 per bloccare i dispositivi dopo 5 minuti di inattività. Quando il valore è vuoto o impostato su **Non configurato**, Intune non modifica o aggiorna questa impostazione.
  - **Scadenza password (giorni)** : immettere il numero di giorni che devono trascorrere prima che sia necessario cambiare la password del dispositivo, da 1 a 65535. Ad esempio, immettere `90` per impostare la scadenza della password dopo 90 giorni. Quando la password scade, agli utenti viene chiesto di creare una nuova password. Quando il valore è vuoto, Intune non modifica o aggiorna questa impostazione.
  - **Impedisci riutilizzo delle password precedenti**: usare questa impostazione per impedire agli utenti di creare password già usate in precedenza. immettere il numero di password usate in precedenza che non è possibile usare, da 1 a 24. Ad esempio, immettere 5 in modo che gli utenti non possano impostare una nuova password uguale alla password corrente o a una qualsiasi delle quattro precedenti. Quando il valore è vuoto, Intune non modifica o aggiorna questa impostazione.

- **Impedisci all'utente di modificare il passcode**: **Blocca** impedisce la modifica, l'aggiunta o la rimozione del passcode. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'aggiunta, la modifica o la rimozione dei passcode.
- **Impedisci lo sblocco tramite impronta digitale**: **Blocca** impedisce l'uso di impronte digitali per sbloccare i dispositivi. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di sbloccare il dispositivo tramite impronta digitale.

- **Blocca il riempimento automatico delle password**: **Blocca** impedisce l'uso della funzionalità di riempimento automatico delle password in macOS. La scelta di **Blocca** comporta anche le conseguenze seguenti:

  - Agli utenti non viene richiesto di usare una password salvata in Safari o in qualsiasi app.
  - Le password complesse automatiche sono disabilitate e non vengono consigliate password complesse agli utenti.

  Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire queste funzionalità.

- **Blocca le richieste di prossimità password**: **Blocca** impedisce ai dispositivi di richiedere password dai dispositivi nelle vicinanze. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire queste richieste di password.

- **Blocca la condivisione delle password**: **Blocca** impedisce la condivisione delle password tra i dispositivi tramite AirDrop. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire la condivisione di queste password.

## <a name="built-in-apps"></a>App predefinite

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Le impostazioni si applicano a: Registrazione dei dispositivi e registrazione automatica dei dispositivi

- **Blocca il riempimento automatico di Safari**: **Blocca** disabilita la funzionalità di riempimento automatico in Safari nei dispositivi. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di modificare le impostazioni di completamento automatico nel Web browser.
- **Blocca la fotocamera**: **Blocca** impedisce l'accesso alla fotocamera nei dispositivi. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'accesso alla fotocamera del dispositivo.

  Intune gestisce solo l'accesso alla fotocamera del dispositivo. Non ha accesso alle immagini o ai video.

- **Blocca Apple Music**: **Blocca** ripristina la modalità classica per l'app Music e disabilita il servizio Music. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'uso dell'app Apple Music.
- **Blocca i risultati della ricerca Internet di Spotlight**: **Blocca** impedisce a Spotlight di restituire risultati da una ricerca su Internet. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire alla ricerca Spotlight di connettersi a Internet per ottenere i risultati della ricerca.
- **Impedisci il trasferimento di file con iTunes**: **Blocca** disabilita i servizi di condivisione file dell'applicazione. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire i servizi di condivisione file dell'applicazione.

  Questa funzionalità si applica a:  
  - macOS 10.13 e versioni successive

## <a name="restricted-apps"></a>App con restrizioni

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Le impostazioni si applicano a: Registrazione dei dispositivi e registrazione automatica dei dispositivi

- **Elenco di tipi di app con restrizioni**: consente di creare un elenco di app che gli utenti non sono autorizzati a installare o usare. Le opzioni disponibili sono:

  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, gli utenti potrebbero avere accesso alle app assegnate e alle app predefinite.
  - **App non consentite**: elencare le app non gestite da Intune che gli utenti non sono autorizzati a installare ed eseguire. Agli utenti non viene impedito di installare un'app vietata. Se un utente installa un'app da questo elenco, verrà segnalato in Intune.
  - **App approvate**: Elencare le app che gli utenti sono autorizzati a installare. Per mantenere la conformità, gli utenti non devono installare altre app. Le app gestite da Intune sono consentite automaticamente, inclusa l'app Portale aziendale. Agli utenti non viene impedito di installare un'app non inclusa nell'elenco approvato. Tuttavia, se lo fanno, verrà segnalato in Intune.

- **ID bundle dell'app**: immettere l'[ID bundle](bundle-ids-built-in-ios-apps.md) dell'app desiderata. È possibile mostrare o nascondere le app predefinite e le app line-of-business. Il sito Web di Apple include un elenco di [app Apple predefinite](https://support.apple.com/HT208094).
- **Nome app**: immettere il nome dell'app desiderata. È possibile mostrare o nascondere le app predefinite e le app line-of-business. Il sito Web di Apple include un elenco di [app Apple predefinite](https://support.apple.com/HT208094).
- **Autore**: immettere l'autore dell'app.

Per aggiungere app a questi elenchi, è possibile:

- **Aggiungi**: selezionare questa opzione per creare un elenco di app.
- Scegliere **Importa** per importare un file CSV con i dettagli sull'app, incluso l'URL. Usare il formato `<app bundle ID>, <app name>, <app publisher>`. Oppure **Esporta** per creare un elenco delle app aggiunte, nello stesso formato.

## <a name="connected-devices"></a>Dispositivi connessi

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Le impostazioni si applicano a: Registrazione dei dispositivi e registrazione automatica dei dispositivi

- **Blocca AirDrop**: **Blocca** impedisce l'uso di AirDrop nei dispositivi. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'uso della funzionalità AirDrop per scambiare contenuti con dispositivi vicini.
- **Blocca lo sbocco automatico di Apple Watch**: **Blocca** impedisce agli utenti di sbloccare il proprio dispositivo macOS con Apple Watch. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di sbloccare il proprio dispositivo macOS con Apple Watch.

## <a name="cloud-and-storage"></a>Cloud e risorse di archiviazione

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Le impostazioni si applicano a: Registrazione dei dispositivi e registrazione automatica dei dispositivi

- **Blocca la sincronizzazione Keychain con iCloud**: **Blocca** disattiva la sincronizzazione delle credenziali archiviate in Keychain con iCloud. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di sincronizzare queste credenziali.
- **Blocca la sincronizzazione dei documenti di iCloud**: **Blocca** impedisce a iCloud di sincronizzare documenti e dati. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire la sincronizzazione di documenti e coppie chiave-valore nello spazio di archiviazione iCloud.
- **Blocca il backup della posta elettronica di iCloud**: **Blocca** impedisce la sincronizzazione di iCloud nell'app di posta macOS. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire la sincronizzazione della posta su iCloud.
- **Blocca il backup dei contatti iCloud**: **Blocca** impedisce a iCloud di sincronizzare i contatti del dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire la sincronizzazione dei contatti usando iCloud.
- **Blocca il backup dei calendari di iCloud**: **Blocca** impedisce la sincronizzazione di iCloud nell'app calendario macOS. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire la sincronizzazione del calendario su iCloud.
- **Blocca il backup dei promemoria di iCloud**: **Blocca** impedisce la sincronizzazione di iCloud nell'app per i promemoria macOS. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire la sincronizzazione dei promemoria su iCloud.
- **Blocca il backup dei segnalibri di iCloud**: **Blocca** impedisce a iCloud di sincronizzare i segnalibri dei dispositivi. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire la sincronizzazione dei segnalibri su iCloud.
- **Blocca il backup delle note di iCloud**: **Blocca** impedisce a iCloud di sincronizzare le note dei dispositivi. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire la sincronizzazione delle note su iCloud.
- **Blocca la libreria foto iCloud**: **Blocca** disabilita la libreria foto di iCloud e impedisce a iCloud di sincronizzare le foto dei dispositivi. Eventuali foto non scaricate completamente dalla libreria foto di iCloud vengono rimosse dall'archivio locale nei dispositivi. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire la sincronizzazione delle foto tra il dispositivo e la libreria foto di iCloud.
- **Handoff**: questa funzionalità consente agli utenti di avviare il lavoro in un dispositivo macOS e quindi continuare il lavoro avviato in un altro dispositivo iOS/iPadOS o macOS. **Blocca** impedisce la funzionalità Handoff nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire questa funzionalità nei dispositivi.

  Questa funzionalità si applica a:  
  - macOS 10.15 e versioni successive

## <a name="domains"></a>Domains

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Le impostazioni si applicano a: Registrazione dei dispositivi e registrazione automatica dei dispositivi

- **URL del dominio di posta elettronica**: **Aggiungi** consente di aggiungere uno o più URL all'elenco. Quando gli utenti ricevono un messaggio di posta elettronica da un dominio diverso da quello configurato, il messaggio di posta elettronica viene contrassegnato come non attendibile nell'app di posta in macOS.

## <a name="next-steps"></a>Passaggi successivi

[Assegnare il profilo](device-profile-assign.md) e [monitorarne lo stato](device-profile-monitor.md).

È possibile limitare funzionalità e impostazioni anche nei dispositivi [iOS/iPadOS](device-restrictions-ios.md).
