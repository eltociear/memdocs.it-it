---
title: Impostazioni relative alle restrizioni dei dispositivi per Android in Microsoft Intune - Azure | Microsoft Docs
description: Visualizzare un elenco di tutte le impostazioni per i dispositivi Android che è possibile controllare e limitare in Microsoft Intune. Usare queste impostazioni per controllare la password, accedere a Google Play, consentire o vietare app, controllare le impostazioni del browser, bloccare le app, eseguire il backup nel cloud Google e controllare le opzioni per messaggi, voce, roaming dei dati, Wi-Fi e connessione Bluetooth.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: ayesham, chrisbal
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: db3ceb67b0ada19d1679f3bf133305214af8fd9f
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/21/2020
ms.locfileid: "80087065"
---
# <a name="android-and-samsung-knox-standard-device-restriction-settings-lists-in-intune"></a>Elenchi delle impostazioni per le limitazioni dei dispositivi Android e Samsung Knox Standard in Intune

Questo articolo illustra tutte le impostazioni di restrizioni dei dispositivi di Microsoft Intune configurabili per i dispositivi che eseguono Android.

>[!TIP]
>Se le impostazioni desiderate non sono disponibili, per la configurazione dei dispositivi si potrebbe usare un [profilo personalizzato](custom-settings-android.md).

## <a name="before-you-begin"></a>Prima di iniziare

[Creare un profilo di configurazione del dispositivo](device-restrictions-configure.md).

## <a name="general"></a>Generale

- **Fotocamera**: scegliere **Blocca** per impedire l'accesso alla fotocamera. **Non configurata** consente l'accesso alla fotocamera del dispositivo.
- **Copia e incolla (solo Samsung Knox)** : scegliere **Blocca** per impedire operazioni di Copia/Incolla. **Non configurata** consente le funzioni Copia e Incolla nel dispositivo.
- **Condivisione degli Appunti tra app (solo Samsung Knox)** : scegliere **Blocca** per impedire l'uso degli Appunti per copiare e incollare tra app. **Non configurata** consente l'uso degli Appunti per copiare e incollare tra app.
- **Invio di dati di diagnostica (solo Samsung Knox)** : scegliere **Blocca** per impedire all'utente di inviare report sui bug dal dispositivo. **Non configurata** consente all'utente di inviare i dati.
- **Cancellazione (solo per Samsung Knox)** : consente all'utente di eseguire un'azione di [cancellazione](../remote-actions/devices-wipe.md) sul dispositivo.
- **Georilevazione (solo Samsung Knox)** : scegliere **Blocca** per disabilitare l'uso di informazioni sulla posizione nel dispositivo. **Non configurata** consente al dispositivo di usare le informazioni sulla posizione.
- **Spegnimento (solo Samsung Knox)** : scegliere **Blocca** per impedire all'utente di spegnere il dispositivo. Se questa impostazione è disabilitata, l'impostazione **Numero di errori di accesso prima della cancellazione dei dati del dispositivo** non può essere specificata e non funziona. **Non configurata** consente all'utente di spegnere il dispositivo.
- **Acquisizione schermo (solo Samsung Knox)** : scegliere **Blocca** per impedire la creazione di screenshot. **Non configurata** consente all'utente di acquisire il contenuto dello schermo come immagine.
- **Assistente vocale (solo Samsung Knox)** : scegliere **Blocca** per disabilitare il servizio S-Voice. **Non configurata** consente l'uso del servizio e dell'app S-Voice nel dispositivo. Questa impostazione non si applica a Bixby o all'assistente vocale per l'accessibilità in grado di leggere a voce alta il contenuto dello schermo.
- **YouTube (solo Samsung Knox)** : scegliere **Blocca** per impedire agli utenti di usare l'app YouTube. **Non configurata** consente l'uso dell'app YouTube nel dispositivo.
- **Consenti i dispositivi condivisi (solo Samsung Knox)** : configurare un dispositivo Samsung Knox Standard gestito come dispositivo condiviso. Con l'impostazione **Consenti**, gli utenti finali possono accedere e disconnettersi dal dispositivo con le credenziali di Azure AD e il dispositivo rimane gestito indipendentemente dal fatto che sia o meno in uso.</br>Quando viene usata con un profilo certificato SCEP, questa funzionalità consente agli utenti di condividere un dispositivo con le stesse app per tutti gli utenti. Ogni utente ha comunque il proprio certificato utente SCEP. Quando gli utenti si disconnettono, tutti i dati delle app vengono cancellati. Questa funzionalità è limitata alle app LOB. </br>**Non configurata** impedisce a più utenti finali di accedere all'app Portale aziendale nel dispositivo usando le credenziali personali di Azure AD.
- **Impedisci modifiche a data e ora (Samsung Knox)** : scegliere **Blocca** per impedire all'utente di modificare le impostazioni di data e ora nel dispositivo. **Non configurata** consente agli utenti di modificare le impostazioni di data e ora.

## <a name="password"></a>Password

- **Password**: selezionare **Rendi obbligatorio** per richiedere all'utente finale di immettere una password per accedere al dispositivo. **Non configurata** consente agli utenti di accedere al dispositivo senza immettere una password.

    > [!NOTE]
    > I dispositivi Samsung Knox richiedono automaticamente un PIN di 4 cifre durante la registrazione MDM. I dispositivi Android nativi possono richiedere automaticamente un PIN per risultare conformi all'accesso condizionale.

- **Lunghezza minima password**: Immettere la lunghezza minima della password che l'utente deve immettere, da 4 a 16 caratteri.
- **Numero massimo di minuti di inattività fino al blocco dello schermo**: immettere il numero massimo di minuti di inattività consentiti nel dispositivo prima del blocco dello schermo. In un dispositivo, un utente finale non può impostare un valore di tempo maggiore di quello configurato nel profilo. Un utente finale può impostare un valore di tempo inferiore. Ad esempio, se il profilo è impostato su 15 minuti, un utente finale può impostare il valore su 5 minuti, ma non può impostare il valore su 30 minuti. 
- **Numero di errori di accesso prima della cancellazione dei dati del dispositivo**: immettere il numero di errori di accesso consentiti prima della cancellazione del dispositivo.
- **Scadenza password (giorni)** : immettere il numero di giorni che devono trascorrere prima che sia necessario cambiare la password del dispositivo.
- **Tipo di password richiesto**: immettere il livello di complessità delle password necessario e se possono essere usati dispositivi biometrici. Le opzioni disponibili sono:
  - **Impostazione predefinita dispositivo**
  - **Protezione biometrica bassa**
  - **Almeno numerico**
  - **Complessa numerica**: i numeri consecutivi o ripetuti (ad esempio, "1111" o "1234") non sono consentiti.<sup>1</sup>
  - **Almeno alfabetico**
  - **Almeno alfanumerico**
  - **Almeno alfanumerico con simboli**
- **Impedisci riutilizzo delle password precedenti**: impedisce all'utente finale di creare una password che è già stata usata in precedenza.
- **Sblocco dell'impronta digitale (solo Samsung Knox)** : scegliere **Blocca** per impedire l'uso di un'impronta digitale per sbloccare il dispositivo. **Non configurata** consente all'utente di sbloccare il dispositivo tramite impronta digitale.
- **Smart Lock e altri agenti di attendibilità**: scegliere **Blocca** per impedire a Smart Lock o altri agenti di attendibilità di modificare le impostazioni della schermata di blocco (Samsung Knox Standard 5.0+). Questa funzionalità del telefono, nota anche come agente di attendibilità, consente di disabilitare o ignorare la password della schermata di blocco del dispositivo se il dispositivo si trova in una posizione attendibile. È possibile usare questa funzionalità, ad esempio, quando il dispositivo è connesso a un dispositivo Bluetooth specifico oppure quando è nelle vicinanze di un tag NFC. È possibile usare questa impostazione per impedire agli utenti di configurare Smart Lock.
- **Crittografia**: scegliere **Rendi obbligatorio** per crittografare i file nel dispositivo. Non tutti i dispositivi supportano la crittografia. Per usare questa funzionalità, è anche necessario: 
  1. Impostare **Password** su **Rendi obbligatorio**.
  2. Impostare **Tipo di password richiesto** su **Almeno numerico**.
  3. Impostare **Lunghezza minima password** su almeno 4 per ottenere la conformità per questa impostazione.

  > [!NOTE]
  > Se viene applicato un criterio di crittografia, i dispositivi Samsung Knox richiedono che gli utenti impostino una password complessa di sei caratteri come passcode del dispositivo.

<sup>1</sup> Prima di assegnare questa impostazione ai dispositivi, assicurarsi di aggiornare l'app Portale aziendale alla versione più recente in tali dispositivi.

Se si imposta l'opzione **Tipo di password richiesto** su **Complessa numerica** e quindi si assegna l'impostazione a un dispositivo che esegue una versione di Android precedente alla versione 5.0, si applica il comportamento seguente:

- Se l'app Portale aziendale esegue una versione precedente alla 1704, non vengono applicati criteri PIN al dispositivo e viene visualizzato un errore nell'interfaccia di amministrazione di Microsoft Endpoint Manager.
- Se l'app Portale aziendale esegue la versione 1704 o versioni successive, è possibile applicare solo un PIN semplice. Le versioni di Android precedenti alla 5.0 non supportano questa impostazione. Non viene visualizzato alcun errore nell'interfaccia di amministrazione di Microsoft Endpoint Manager.

## <a name="google-play-store"></a>Google Play Store

- **Google Play Store (solo Samsung Knox)** : scegliere **Blocca** per impedire agli utenti di usare Google Play Store. **Non configurata** consente all'utente di accedere a Google Play Store sul dispositivo.

## <a name="restricted-apps"></a>App con restrizioni

Usare queste impostazioni per consentire o bloccare app specifiche nel dispositivo. Questa funzionalità è supportata nei dispositivi Android e Samsung KNOX Standard:

- **App non consentite**: elenco di app non gestite da Intune di cui si vuole evitare l'installazione nel dispositivo. Se un utente installa un'app da questo elenco, si riceverà una notifica da Intune.
- **App approvate**: elenco di app che gli utenti sono autorizzati a installare. Per mantenere la conformità, gli utenti non devono installare altre app. Le app gestite da Intune sono automaticamente consentite.

Per aggiungere app a questi elenchi, è possibile:

- **Aggiungere** l'URL di Google Play Store dell'app in questione. Ad esempio, per aggiungere l'app Desktop remoto Microsoft per Android, immettere `https://play.google.com/store/apps/details?id=com.microsoft.rdc.android`. Per trovare l'URL di un'app, aprire [Google Play Store](https://play.google.com/store/apps) e cercare l'app. Ad esempio, cercare `Microsoft Remote Desktop Play Store` o `Microsoft Planner`. Selezionare l'app e copiare l'URL.
- Importare un file CSV con i dettagli sull'app, incluso l'URL. Usare il formato <*url app*>, <*nome app*>, <*autore app*>. In alternativa, **esportare** un elenco esistente che include l'elenco delle app con restrizioni nello stesso formato.

> [!IMPORTANT]
> I profili dispositivo che usano le impostazioni per app con restrizioni devono essere assegnati ai gruppi di utenti.

## <a name="browser"></a>Browser

- **Web browser (solo Samsung Knox)** : scegliere **Blocca** per impedire l'uso del Web browser predefinito nel dispositivo. **Non configurata** consente di usare il Web browser predefinito del dispositivo.
- **Riempimento automatico (solo Samsung Knox)** : scegliere **Blocca** per impedire il riempimento automatico del testo nel browser. **Non configurata** consente di usare la funzione di riempimento automatico del Web browser.
- **Cookie (solo Samsung Knox)** : scegliere come si vogliono gestire i cookie provenienti da siti Web nel dispositivo. Le opzioni disponibili sono:
  - Consenti
  - Blocca tutti i cookie
  - Consenti i cookie dai siti Web visitati
  - Consenti i cookie dal sito Web corrente
- **JavaScript (solo Samsung Knox)** : scegliere **Blocca** per impedire l'esecuzione di script Java nel Web browser. **Non configurata** consente al Web browser del dispositivo di eseguire script Java.
- **Popup (solo Samsung Knox)** : scegliere **Blocca** per impedire i popup nel Web browser. **Non configurata** consente i popup nel Web browser.

## <a name="allow-or-block-apps"></a>Consentire o bloccare le app

Usare queste impostazioni per consentire, bloccare o nascondere app specifiche nei dispositivi Samsung KNOX Standard. Le app nascoste non possono essere aperte o eseguite dall'utente.

Le opzioni disponibili sono:

- **App di cui è consentita l'installazione (solo Samsung Knox Standard)**
- **App di cui non è consentito l'avvio (solo Samsung Knox Standard)**
- **App nascoste all'utente (solo Samsung Knox Standard)**

Per ogni impostazione, aggiungere un elenco di app. Le opzioni disponibili sono:

- **Aggiungi app per nome del pacchetto**: usato principalmente per le app line-of-business. Immettere il nome dell'app e il nome del pacchetto dell'app.
- **Aggiungi app per URL**: immettere il nome e l'URL dell'app in Google Play Store.
- **Aggiungi l'app dello Store**: selezionare un'app nell'elenco esistente di app gestite in Intune.

## <a name="cloud-and-storage"></a>Cloud e risorse di archiviazione

- **Backup di Google (solo Samsung Knox)** : scegliere **Blocca** per impedire la sincronizzazione del dispositivo con il backup di Google. **Non configurata** consente l'uso del backup di Google.
- **Sincronizzazione automatica dell'account Google (solo Samsung Knox)** : scegliere **Blocca** per impedire la funzionalità di sincronizzazione automatica dell'account Google nel dispositivo. **Non configurata** consente la sincronizzazione automatica delle impostazioni dell'account Google.
- **Archivi rimovibili (solo Samsung Knox)** : scegliere **Blocca** per impedire al dispositivo di usare archivi rimovibili. **Non configurata** consente al dispositivo di usare archivi rimovibili, ad esempio una scheda SD.
- **Crittografia su schede di memoria (solo Samsung Knox)** : **Rendi obbligatorio** impone la crittografia delle schede di memoria. **Non configurata** consente l'uso delle schede di archiviazione non crittografate. Non tutti i dispositivi supportano la crittografia delle schede di archiviazione. Per verificare, rivolgersi al produttore del dispositivo.

## <a name="cellular-and-connectivity"></a>Rete cellulare e connettività

- **Dati in roaming (solo Samsung Knox)** : scegliere **Blocca** per impedire il roaming dei dati nella rete cellulare. **Non configurata** consente il roaming dati quando il dispositivo si trova in una rete cellulare.
- **Messaggi SMS/MMS (solo Samsung Knox)** : scegliere **blocca** per impedire l'uso di messaggi SMS e MMS nel dispositivo. **Non configurata** consente l'uso di messaggi SMS e MMS sul dispositivo.
- **Chiamata vocale (solo Samsung Knox)** : scegliere **Blocca** per impedire agli utenti di usare la funzionalità di composizione vocale nel dispositivo. **Non configurata** consente la chiamata vocale nel dispositivo.
- **Chiamate in roaming (solo Samsung Knox)** : scegliere **Blocca** per impedire le chiamate in roaming nella rete cellulare. **Non configurata** consente il roaming vocale quando il dispositivo si trova in una rete cellulare.
- **Bluetooth (solo Samsung Knox)** : scegliere **Blocca** per impedire l'uso del Bluetooth nel dispositivo. **Non configurata** consente di usare Bluetooth nel dispositivo.
- **NFC (solo Samsung Knox)** : scegliere **Blocca** per bloccare la tecnologia NFC (Near Field Communication). **Non configurata** consente le operazioni che usano la tecnologia NFC (Near Field Communication) nei dispositivi supportati.
- **Wi-Fi (solo Samsung Knox)** : scegliere **Blocca** per impedire l'uso del Wi-Fi nel dispositivo. **Non configurata** consente l'uso delle funzionalità Wi-Fi del dispositivo.
- **Tethering Wi-Fi (solo Samsung Knox)** : scegliere **Blocca** per impedire l'uso del tethering Wi-Fi nel dispositivo. **Non configurata** consente di usare il tethering Wi-Fi nel dispositivo.

## <a name="kiosk"></a>Modalità tutto schermo

Le impostazioni della modalità tutto schermo si applicano solo ai dispositivi Samsung Knox Standard e solo alle app gestite con Intune.

- Aggiungere le app che si vuole eseguire quando il dispositivo è in modalità tutto schermo. In modalità tutto schermo possono essere eseguite solo le app aggiunte. Le app non aggiunte non vengono eseguite. I browser preinstallati non vengono eseguiti come app quando il dispositivo è in modalità tutto schermo. Se è richiesto un browser, è consigliabile usare [Managed Browser](../apps/app-configuration-managed-browser.md).

  Opzioni per le app:

  - **Aggiungi app per nome del pacchetto**: usato principalmente per le app line-of-business. Immettere il nome dell'app e il nome del pacchetto dell'app.
  - **Aggiungi app per URL**: immettere il nome e l'URL dell'app in Google Play Store.
  - **Aggiungi l'app dello Store**: selezionare un'app nell'elenco esistente di app gestite in Intune.

- **Pulsante Sospensione schermo**: scegliere **Blocca** per impedire o nascondere il pulsante di sospensione dello schermo. **Non configurata** consente il pulsante di riattivazione dalla sospensione dello schermo nel dispositivo.
- **Pulsanti volume**: scegliere **Blocca** per impedire all'utente di regolare il volume, disabilitando i pulsanti del volume. **Non configurata** consente l'uso di pulsanti del volume nel dispositivo.

## <a name="next-steps"></a>Passaggi successivi

[Assegnare il profilo](device-profile-assign.md) e [monitorarne lo stato](device-profile-monitor.md).

È anche possibile creare profili in modalità tutto schermo per dispositivi [Android Enterprise](device-restrictions-android-for-work.md#dedicated-device-settings) e [Windows 10](kiosk-settings.md).
