---
title: Impostazioni relative alle restrizioni dei dispositivi per Android in Microsoft Intune - Azure | Microsoft Docs
description: Vedere un elenco di tutte le impostazioni per gli amministratori di dispositivi Android che è possibile controllare e limitare in Microsoft Intune. Usare queste impostazioni per controllare la password, accedere a Google Play, consentire o vietare app, controllare le impostazioni del browser, bloccare le app, eseguire il backup nel cloud Google e controllare le opzioni per messaggi, voce, roaming dei dati, Wi-Fi e connessione Bluetooth.
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
ms.reviewer: chmaguir, chrisbal
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4afc27680c464f67756340ebcb0958887ae6f795
ms.sourcegitcommit: e2877d21dfd70c4029c247275fa2b38e76bd22b8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/31/2020
ms.locfileid: "80407862"
---
# <a name="android-and-samsung-knox-standard-device-restriction-settings-lists-in-intune"></a>Elenchi delle impostazioni per le limitazioni dei dispositivi Android e Samsung Knox Standard in Intune

Questo articolo illustra tutte le impostazioni di restrizioni dei dispositivi di Microsoft Intune configurabili per i dispositivi che eseguono Android.

>[!TIP]
>Se le impostazioni desiderate non sono disponibili, per la configurazione dei dispositivi si potrebbe usare un [profilo personalizzato](custom-settings-android.md).

## <a name="before-you-begin"></a>Prima di iniziare

[Creare un profilo di configurazione del dispositivo](device-restrictions-configure.md).

## <a name="general"></a>Generale

- **Fotocamera**: **Blocca** impedisce l'accesso alla fotocamera nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'accesso alla fotocamera del dispositivo.

  Intune gestisce solo l'accesso alla fotocamera del dispositivo. Non ha accesso alle immagini o ai video.

- **Copia e incolla (solo Samsung Knox)** : **Blocca** impedisce operazioni di Copia e Incolla. **Non configurata** consente le funzioni Copia e Incolla nei dispositivi.
- **Condivisione degli Appunti tra app (solo Samsung Knox)** : **Blocca** impedisce l'uso degli Appunti per copiare e incollare tra app. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire le funzioni Copia e Incolla nei dispositivi.
- **Invio di dati di diagnostica (solo Samsung Knox)** : **Blocca** impedisce agli utenti di inviare segnalazioni di bug dai dispositivi. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di inviare i dati.
- **Cancellazione (solo per Samsung Knox)** : consente agli utenti di eseguire un'azione di [cancellazione](../remote-actions/devices-wipe.md) nei dispositivi. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.
- **Georilevazione (solo Samsung Knox)** : **Blocca** impedisce ai dispositivi di usare le informazioni sulla posizione. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire ai dispositivi di usare le informazioni sulla posizione.
- **Spegnimento (solo Samsung Knox)** : **Blocca** impedisce agli utenti di spegnere il dispositivo. Impedisce anche la configurazione e il funzionamento dell'impostazione **Numero di errori di accesso prima della cancellazione dei dati del dispositivo**. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di spegnere i dispositivi.
- **Acquisizione schermo (solo Samsung Knox)** : **Blocca** impedisce l'acquisizione di screenshot. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di acquisire il contenuto dello schermo come immagine.
- **Assistente vocale (solo Samsung Knox)** : **Blocca** disabilita il servizio S Voice. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'uso del servizio e dell'app S Voice nei dispositivi. Questa impostazione non si applica a Bixby o all'assistente vocale per l'accessibilità in grado di leggere a voce alta il contenuto dello schermo.
- **YouTube (solo Samsung Knox)** : **Blocca** impedisce agli utenti di usare l'app YouTube. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'uso dell'app YouTube nei dispositivi.
- **Consenti i dispositivi condivisi (solo Samsung Knox)** : configurare un dispositivo Samsung Knox Standard gestito come dispositivo condiviso. **Consenti** consente agli utenti di effettuare l'accesso e la disconnessione nei dispositivi con le credenziali di Azure AD. I dispositivi rimangono gestiti, indipendentemente dal fatto che siano in uso o meno.

  Quando viene usata con un profilo certificato SCEP, questa funzionalità consente agli utenti di condividere un dispositivo con le stesse app per tutti gli utenti. Ogni utente ha comunque il proprio certificato utente SCEP. Quando gli utenti si disconnettono, tutti i dati delle app vengono cancellati. Questa funzionalità è limitata alle app LOB.

  Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe impedire a più utenti di accedere all'app Portale aziendale nei dispositivi usando le credenziali di Azure AD.
- **Impedisci modifiche a data e ora (Samsung Knox)** : **Blocca** impedisce agli utenti di modificare le impostazioni di data e ora nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di modificare le impostazioni di data e ora.

## <a name="password"></a>Password

- **Password**: **Rendi obbligatorio** richiede agli utenti di immettere una password per accedere ai dispositivi. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di accedere ai dispositivi senza immettere una password.

    > [!NOTE]
    > I dispositivi Samsung Knox richiedono automaticamente un PIN di 4 cifre durante la registrazione MDM. I dispositivi Android nativi possono richiedere automaticamente un PIN per risultare conformi all'accesso condizionale.

- **Lunghezza minima password**: immettere il numero minimo di caratteri necessari, da 4 a 16. Ad esempio, immettere `6` per richiedere una lunghezza della password di minimo sei numeri o caratteri.
- **Numero massimo di minuti di inattività fino al blocco dello schermo**: immettere il periodo di tempo per cui un dispositivo deve rimanere inattivo prima che lo schermo venga bloccato automaticamente. Ad esempio, immettere `5` per bloccare i dispositivi dopo 5 minuti di inattività. Quando il valore è vuoto o impostato su **Non configurato**, Intune non modifica o aggiorna questa impostazione.

  In un dispositivo, gli utenti non possono impostare un valore di tempo maggiore di quello configurato nel profilo. Gli utenti possono impostare un valore di tempo inferiore. Ad esempio, se il profilo è impostato su `15` minuti, gli utenti possono impostare il valore su 5 minuti, ma non possono impostare il valore su 30 minuti.

- **Numero di errori di accesso prima della cancellazione dei dati del dispositivo**: immettere il numero di password non corrette consentite prima che i dispositivi vengano cancellati, da 4 a 11. `0` (zero) potrebbe disabilitare la funzionalità di cancellazione dei dispositivi. Quando il valore è vuoto, Intune non modifica o aggiorna questa impostazione.
- **Scadenza password (giorni)** : immettere il numero di giorni che devono trascorrere prima che sia necessario cambiare la password del dispositivo, da 1 a 365. Ad esempio, immettere `90` per impostare la scadenza della password dopo 90 giorni. Quando la password scade, agli utenti viene chiesto di creare una nuova password. Quando il valore è vuoto, Intune non modifica o aggiorna questa impostazione.
- **Tipo di password richiesto**: immettere il livello di complessità delle password necessario e se possono essere usati dispositivi biometrici. Le opzioni disponibili sono:
  - **Impostazione predefinita dispositivo**
  - **Protezione biometrica bassa**: [Biometrica complessa e vulnerabile a confronto](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (apre il sito Web Android)
  - **Almeno numerico**: include caratteri numerici, ad esempio `123456789`.
  - **Complessa numerica**: i numeri consecutivi o ripetuti (ad esempio, "1111" o "1234") non sono consentiti. Prima di assegnare questa impostazione ai dispositivi, assicurarsi di aggiornare l'app Portale aziendale alla versione più recente in tali dispositivi.

    Con l'impostazione **Complessa numerica** e quando si assegna l'impostazione a dispositivi che eseguono una versione di Android precedente alla 5.0, si applica il comportamento seguente:

    - Se l'app Portale aziendale esegue una versione precedente alla 1704, non vengono applicati criteri PIN ai dispositivi e viene visualizzato un errore nell'interfaccia di amministrazione di Microsoft Endpoint Manager.
    - Se l'app Portale aziendale esegue la versione 1704 o versioni successive, è possibile applicare solo un PIN semplice. Le versioni di Android precedenti alla 5.0 non supportano questa impostazione. Non viene visualizzato alcun errore nell'interfaccia di amministrazione di Microsoft Endpoint Manager.

  - **Almeno alfabetico**: include lettere dell'alfabeto. Numeri e simboli non sono richiesti.
  - **Almeno alfanumerico**: include lettere maiuscole, lettere minuscole e caratteri numerici.
  - **Almeno alfanumerico con simboli**: include lettere maiuscole, lettere minuscole, caratteri numerici, segni di punteggiatura e simboli.

- **Impedisci riutilizzo delle password precedenti**: usare questa impostazione per impedire agli utenti di creare password già usate in precedenza. immettere il numero di password usate in precedenza che non è possibile usare, da 1 a 24. Ad esempio, immettere `5` in modo che gli utenti non possano definire una nuova password uguale alla password corrente o a una qualsiasi delle quattro precedenti. Quando il valore è vuoto, Intune non modifica o aggiorna questa impostazione.
- **Sblocco dell'impronta digitale (solo Samsung Knox)** : **Blocca** impedisce l'uso di un'impronta digitale per sbloccare i dispositivi. Con l'impostazione predefinita **Non configurato** Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di sbloccare i dispositivi usando un'impronta digitale.
- **Smart Lock e altri agenti di attendibilità**: **Blocca** impedisce a Smart Lock o altri agenti di attendibilità di modificare le impostazioni della schermata di blocco. Se il dispositivo si trova in una posizione attendibile, questa funzionalità, chiamata anche agente di attendibilità, consente di disabilitare o ignorare la password della schermata di blocco del dispositivo. Ad esempio, usare questa funzionalità quando i dispositivi sono connessi a un dispositivo Bluetooth specifico oppure quando i dispositivi sono vicini a un tag NFC. È possibile usare questa impostazione per impedire agli utenti di configurare Smart Lock.

  Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.

  Questa impostazione si applica a:

  - Samsung KNOX Standard 5.0+

- **Crittografia**: scegliere **Rendi obbligatorio** per crittografare i file nel dispositivo. Non tutti i dispositivi supportano la crittografia. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per configurare questa impostazione e segnalare correttamente la conformità, configurare anche:
  1. **Password**: impostare su **Rendi obbligatorio**.
  2. **Tipo di password richiesto**: impostare su **Almeno numerico**.
  3. **Lunghezza minima password**: impostare almeno `4`.

  > [!NOTE]
  > Se viene applicato un criterio di crittografia, i dispositivi Samsung Knox richiedono che gli utenti impostino una password complessa di sei caratteri come passcode del dispositivo.

## <a name="google-play-store"></a>Google Play Store

- **Google Play Store (solo Samsung Knox)** : **Blocca** impedisce agli utenti di usare Google Play Store. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di accedere a Google Play Store nei dispositivi.

## <a name="restricted-apps"></a>App con restrizioni

Usare queste impostazioni per consentire o bloccare app specifiche nei dispositivi. Questa funzionalità è supportata nei dispositivi Android e Samsung KNOX Standard.

- **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione.
- **App non consentite**: elencare le app non gestite da Intune che gli utenti non sono autorizzati a installare ed eseguire. Se un utente installa un'app da questo elenco, si riceverà una notifica da Intune.
- **App approvate**: Elencare le app che gli utenti sono autorizzati a installare. Per mantenere la conformità, gli utenti non devono installare altre app.  Le app gestite da Intune sono consentite automaticamente, inclusa l'app Portale aziendale.
- **Elenco di app**: selezionare **Aggiungi** per l'aggiungere l'app.
  - **ID bundle dell'app**: immettere l'ID bundle dell'app.
  - **URL di App Store**: immettere l'URL di Google Play Store dell'app in questione. Ad esempio, per aggiungere l'app Desktop remoto Microsoft per Android, immettere `https://play.google.com/store/apps/details?id=com.microsoft.rdc.android`.

    Per trovare l'URL di un'app, aprire [Google Play Store](https://play.google.com/store/apps) e cercare l'app. Ad esempio, cercare `Microsoft Remote Desktop Play Store` o `Microsoft Planner`. Selezionare l'app e copiare l'URL.
  
  - **Nome app**: immettere il nome desiderato. Questo nome viene visualizzato agli utenti.
  - **Autore** (facoltativo): immettere l'autore dell'app, ad esempio `Microsoft`.

È anche possibile scegliere **Importa** per importare un file CSV con i dettagli sull'app, incluso l'URL. Usare il formato <*url app*>, <*nome app*>, <*autore app*>. In alternativa, **esportare** un elenco esistente che include l'elenco delle app con restrizioni nello stesso formato.

> [!IMPORTANT]
> I profili dispositivo che usano le impostazioni per app con restrizioni devono essere assegnati a gruppi di utenti e non a gruppi di dispositivi.

## <a name="browser"></a>Browser

- **Web browser (solo Samsung Knox)** : **Blocca** impedisce l'uso del Web browser predefinito nei dispositivi. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'uso del Web browser predefinito del dispositivo.
- **Riempimento automatico (solo Samsung Knox)** : **Blocca** impedisce al browser di compilare automaticamente il testo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire il riempimento automatico.
- **Cookie (solo Samsung Knox)** : scegliere come gestire i cookie dai siti Web nei dispositivi. Le opzioni disponibili sono:
  - Consenti
  - Blocca tutti i cookie
  - Consenti i cookie dai siti Web visitati
  - Consenti i cookie dal sito Web corrente
- **JavaScript (solo Samsung Knox)** : **Blocca** impedisce l'esecuzione di JavaScript nel browser. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire questi script.
- **Popup (solo Samsung Knox)** : **Blocca** attiva Blocco popup per impedire popup nel Web browser. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire i popup.

## <a name="allow-or-block-apps"></a>Consentire o bloccare le app

Usare queste impostazioni per consentire, bloccare o nascondere app specifiche nei dispositivi Samsung KNOX Standard. Le app nascoste non possono essere aperte o eseguite dagli utenti.

Le opzioni disponibili sono:

- **App di cui è consentita l'installazione (solo Samsung Knox Standard)** : aggiungere le app che gli utenti possono installare. Gli utenti non possono installare app che non sono presenti nell'elenco.
- **App di cui non è consentito l'avvio (solo Samsung Knox Standard)** : immettere le app che gli utenti non possono eseguire nei propri dispositivi.
- **App nascoste all'utente (solo Samsung Knox Standard)** : immettere le app nascoste nei dispositivi. Gli utenti non possono individuare o eseguire queste app.

Per ogni impostazione, aggiungere le app:

- **Aggiungi app per nome del pacchetto**: Immettere il nome dell'app e il nome del pacchetto dell'app. usato principalmente per le app line-of-business. 
- **Aggiungi app per URL**: immettere il nome e l'URL dell'app in Google Play Store.
- **Aggiungi l'app dello Store**: selezionare un'app nell'elenco esistente di app gestite in Intune.

## <a name="cloud-and-storage"></a>Cloud e risorse di archiviazione

- **Backup di Google (solo Samsung Knox)** : **Blocca** impedisce la sincronizzazione dei dispositivi con il backup di Google. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'uso del backup di Google.
- **Sincronizzazione automatica dell'account Google (solo Samsung Knox)** : **Blocca** impedisce l'uso della funzionalità di sincronizzazione automatica dell'account Google nei dispositivi. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire di sincronizzare automaticamente le impostazioni dell'account Google.
- **Archivi rimovibili (solo Samsung Knox)** : **Blocca** impedisce ai dispositivi di usare archivi rimovibili. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire ai dispositivi di usare archivi rimovibili, ad esempio una scheda SD.
- **Crittografia su schede di memoria (solo Samsung Knox)** : **Rendi obbligatorio** impone la crittografia delle schede di memoria. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'uso di schede di memoria non crittografate. Non tutti i dispositivi supportano la crittografia delle schede di archiviazione. Per verificare, rivolgersi al produttore del dispositivo.

## <a name="cellular-and-connectivity"></a>Rete cellulare e connettività

- **Dati in roaming (solo Samsung Knox)** : **Blocca** impedisce il roaming dei dati nella rete cellulare. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire il roaming dei dati.
- **Messaggi SMS/MMS (solo Samsung Knox)** : **Blocca** impedisce l'uso di SMS e MMS nei dispositivi. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'uso di SMS e MMS.
- **Chiamata vocale (solo Samsung Knox)** : **Blocca** impedisce agli utenti di usare la funzionalità di chiamata vocale nei dispositivi. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire le chiamate vocali.
- **Chiamate in roaming (solo Samsung Knox)** : **Blocca** impedisce le chiamate in roaming nella rete cellulare. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire le chiamate in roaming.
- **Bluetooth (solo Samsung Knox)** : **Blocca** impedisce l'uso di Bluetooth nei dispositivi. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'uso di Bluetooth.
- **NFC (solo Samsung Knox)** : **Blocca** disabilita le operazioni che usano NFC (Near Field Communication) nei dispositivi che la supportano. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire operazioni NFC.
- **Wi-Fi (solo Samsung Knox)** : **Blocca** impedisce l'uso del Wi-Fi nei dispositivi. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'uso del Wi-Fi.
- **Tethering Wi-Fi (solo Samsung Knox)** : **Blocca** impedisce l'uso del tethering Wi-Fi nei dispositivi. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'uso del tethering Wi-Fi.

## <a name="kiosk"></a>Modalità tutto schermo

Le impostazioni della modalità tutto schermo si applicano solo ai dispositivi Samsung Knox Standard e solo alle app gestite con Intune.

- Aggiungere le app che si vuole eseguire quando il dispositivo è in modalità tutto schermo. In modalità tutto schermo possono essere eseguite solo le app aggiunte. Le app non aggiunte non vengono eseguite. I browser preinstallati non vengono eseguiti come app quando il dispositivo è in modalità tutto schermo. Se è richiesto un browser, è consigliabile usare [Managed Browser](../apps/app-configuration-managed-browser.md).

  Opzioni per le app:

  - **Aggiungi app per nome del pacchetto**: usato principalmente per le app line-of-business. Immettere il nome dell'app e il nome del pacchetto dell'app.
  - **Aggiungi app per URL**: immettere il nome e l'URL dell'app in Google Play Store.
  - **Aggiungi l'app dello Store**: selezionare un'app nell'elenco esistente di app gestite in Intune.

- **Pulsante Sospensione schermo**: **Blocca** impedisce l'uso del pulsante di sospensione dello schermo o lo nasconde. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire il pulsante di riattivazione dalla sospensione dello schermo nei dispositivi.
- **Pulsanti volume**: **Blocca** impedisce agli utenti di regolare il volume disabilitando i pulsanti del volume. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'uso dei pulsanti del volume nei dispositivi.

## <a name="next-steps"></a>Passaggi successivi

[Assegnare il profilo](device-profile-assign.md) e [monitorarne lo stato](device-profile-monitor.md).

È anche possibile creare profili in modalità tutto schermo per dispositivi [Android Enterprise](device-restrictions-android-for-work.md#dedicated-devices) e [Windows 10](kiosk-settings.md).
