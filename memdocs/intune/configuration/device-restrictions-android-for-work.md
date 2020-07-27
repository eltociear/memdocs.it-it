---
title: Impostazioni dei dispositivi Android Enterprise in Microsoft Intune - Azure | Microsoft Docs
description: Nei dispositivi Android Enterprise o Android for Work limitare le impostazioni del dispositivo, tra cui copia e incolla, visualizzazione delle notifiche, autorizzazioni delle app, condivisione dei dati, lunghezza della password, errori di accesso, uso dell'impronta digitale per sbloccare, riutilizzo delle password e abilitazione della condivisione dei contatti di lavoro con Bluetooth. Configurare i dispositivi come chiosco multimediale dedicato del dispositivo per eseguire una sola app o più App.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 07/16/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: chmaguir, chrisbal, priyar
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure, seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7f49ba4fffd84ffae3e5b47ad74088b65d599533
ms.sourcegitcommit: cb9b452f8e566fe026717b59c142b65f426e5033
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/20/2020
ms.locfileid: "86491253"
---
# <a name="android-enterprise-device-settings-to-allow-or-restrict-features-using-intune"></a>Impostazioni dei dispositivi Android Enterprise per consentire o limitare l'uso delle funzionalità tramite Intune

Questo articolo descrive le diverse impostazioni che è possibile controllare nei dispositivi Android Enterprise. Usare queste impostazioni nella propria soluzione di gestione di dispositivi mobili (MDM) per abilitare o disabilitare funzionalità, eseguire app in dispositivi dedicati, controllare le impostazioni di sicurezza e altro ancora.

## <a name="before-you-begin"></a>Prima di iniziare

[Creare un profilo di configurazione del dispositivo](device-restrictions-configure.md).

## <a name="fully-managed-dedicated-and-corporate-owned-work-profile"></a>Profilo di lavoro completamente gestito, dedicato e di proprietà aziendale

Queste impostazioni si applicano ai tipi di registrazione Android Enterprise in cui Intune controlla l'intero dispositivo, ad esempio i dispositivi Android Enterprise completamente gestiti, dedicati e di proprietà aziendale con profilo di lavoro.

Alcune impostazioni non sono supportate da tutti i tipi di registrazione. Per vedere quali impostazioni sono supportate per ogni tipo di registrazione, vedere l'interfaccia utente. Ogni impostazione è riportata sotto un'intestazione che indica i tipi di registrazione in cui può essere usata.

![Intestazioni delle impostazioni.](./media/device-restrictions-android-for-work/setting-headers.png)

Alcune impostazioni si applicano solo a livello di profilo di lavoro per i dispositivi di proprietà aziendale con un profilo di lavoro. Queste impostazioni si applicano sempre all'intero dispositivo per i dispositivi completamente gestiti e dedicati. Queste impostazioni sono contrassegnate dal descrittore *(livello di profilo di lavoro)* nell'interfaccia utente.

![Intestazioni delle impostazioni.](./media/device-restrictions-android-for-work/work-profile-level.png)


### <a name="general"></a>Generale

- **Acquisizione schermo**: **Blocca** impedisce la creazione di screenshot o acquisizioni di schermate nel dispositivo. Impedisce anche la visualizzazione del contenuto nei dispositivi di visualizzazione privi di output video protetto. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di acquisire il contenuto dello schermo come immagine.
- **Fotocamera**: **Blocca** impedisce l'accesso alla fotocamera nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'accesso alla fotocamera.

  Intune gestisce solo l'accesso alla fotocamera del dispositivo. Non ha accesso alle immagini o ai video.

- **Criteri di autorizzazione predefiniti**: questa impostazione definisce i criteri di autorizzazione predefiniti delle richieste delle autorizzazioni di runtime. Opzioni disponibili
  - **Impostazione predefinita dispositivo**: usare l'impostazione predefinita del dispositivo.
  - **Messaggio di richiesta**: agli utenti viene richiesto di approvare l'autorizzazione.
  - **Concedi automaticamente**: le autorizzazioni vengono concesse automaticamente.
  - **Nega automaticamente**: le autorizzazioni vengono negate automaticamente.
- **Modifiche a data e ora**: **Blocca** impedisce agli utenti di impostare manualmente la data e l'ora. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di impostare la data e l'ora nel dispositivo.
- **Modifiche al volume**: **Blocca**  impedisce agli utenti di modificare il volume del dispositivo e disattiva anche il volume principale. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'uso delle impostazioni del volume nel dispositivo.
- **Ripristino impostazioni predefinite**: **Blocca** impedisce agli utenti di usare l'opzione per il ripristino delle impostazioni predefinite nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di usare questa impostazione nel dispositivo.
- **Modalità provvisoria**: **Blocca** impedisce agli utenti di riavviare il dispositivo in modalità provvisoria. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di riavviare il dispositivo in modalità provvisoria.
- **Barra di stato**: **Blocca** impedisce l'accesso alla barra di stato, incluse le notifiche e le impostazioni rapide. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di accedere alla barra di stato.
- **Servizi per dati in roaming**: **Blocca** impedisce il roaming dei dati nella rete cellulare. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire il roaming dei dati quando il dispositivo si trova in una rete cellulare.
- **Modifiche alle impostazioni Wi-Fi**: **Blocca** impedisce agli utenti di modificare le impostazioni Wi-Fi create dal proprietario del dispositivo. Gli utenti possono creare configurazioni Wi-Fi personalizzate. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di modificare le impostazioni Wi-Fi nel dispositivo.
- **Configurazione del punto di accesso Wi-Fi**: **Blocca** impedisce agli utenti di creare o modificare configurazioni Wi-Fi. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di modificare le impostazioni Wi-Fi nel dispositivo.
- **Configurazione Bluetooth**: **Blocca** impedisce agli utenti di configurare Bluetooth nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'uso di Bluetooth nel dispositivo.
- **Tethering e accesso a hotspot**: **Blocca** impedisce il tethering e l'accesso a hotspot portatili. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire il tethering e l'accesso agli hotspot portatili.
- **Archiviazione USB**: scegliere **Consenti** per consentire l'accesso all'archiviazione USB nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe impedire l'accesso all'archiviazione USB.
- **Trasferimento di file su USB**: **Blocca** impedisce il trasferimento di file su USB. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire il trasferimento di file.
- **Supporti esterni**: **Blocca** impedisce l'uso o la connessione di qualsiasi supporto esterno nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire supporti esterni nel dispositivo.
- **Trasmetti dati con NFC**: **Blocca** impedisce l'uso della tecnologia NFC (Near Field Communication) per la trasmissione di dati dalle app. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'uso di NFC per condividere i dati tra dispositivi.
- **Funzionalità di debug**: scegliere **Consenti** per consentire agli utenti di usare le funzionalità di debug nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe impedire agli utenti di usare le funzionalità di debug nel dispositivo.
- **Regolazione del microfono**: **Blocca** impedisce agli utenti di riattivare il microfono e regolare il volume del microfono. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di usare e regolare il volume del microfono nel dispositivo.
- **Indirizzi di posta elettronica per la protezione dal ripristino delle impostazioni predefinite**: scegliere **Indirizzi di posta elettronica dell'account Google**. Immettere gli indirizzi di posta elettronica degli amministratori dei dispositivi che possono sbloccare il dispositivo dopo la cancellazione. Assicurarsi di separare gli indirizzi di posta elettronica con punti e virgola, ad esempio `admin1@gmail.com;admin2@gmail.com`. Se non viene immesso un indirizzo di posta elettronica, chiunque può sbloccare il dispositivo dopo il ripristino delle impostazioni predefinite. Questi indirizzi di posta elettronica si applicano solo quando viene eseguito un ripristino delle impostazioni predefinite non dell'utente, ad esempio l'esecuzione di un ripristino delle impostazioni di fabbrica tramite il menu di ripristino.

  Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.

- **Rete di emergenza**: **Abilita** consente agli utenti di attivare la funzionalità di rete di emergenza. Se non è possibile creare una connessione di rete in fase di avvio del dispositivo, la rete di emergenza richiede all'utente di connettersi temporaneamente a una rete per aggiornare i criteri del dispositivo. Dopo aver applicato i criteri, la rete temporanea viene dimenticata e viene ripreso l'avvio del dispositivo. Questa funzionalità consente di connettere i dispositivi a una rete se:
  - Non è disponibile una rete idonea nei criteri più recenti.
  - Il dispositivo viene avviato in un'app in modalità di attività di blocco.
  - Gli utenti non sono in grado di raggiungere le impostazioni del dispositivo.

  Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe impedire agli utenti di attivare la funzionalità di rete di emergenza nel dispositivo.

- **Aggiornamento del sistema**: scegliere un'opzione per definire la modalità di gestione degli aggiornamenti in modalità wireless da parte del dispositivo. Opzioni disponibili
  - **Impostazione predefinita dispositivo**: usare l'impostazione predefinita del dispositivo.
  - **Automatico**: gli aggiornamenti vengono installati automaticamente senza l'intervento dell'utente. L'impostazione del criterio consente di installare immediatamente eventuali aggiornamenti in sospeso.
  - **Posposto**: gli aggiornamenti vengono rimandati di 30 giorni. Al termine dei 30 giorni, Android chiede agli utenti di installare l'aggiornamento. Ai produttori di dispositivi e ai gestori telefonici è consentito impedire il posticipo degli aggiornamenti della sicurezza. Per un aggiornamento esentato viene visualizzata una notifica di sistema agli utenti nel dispositivo.
  - **Finestra di manutenzione**: installa automaticamente gli aggiornamenti in una finestra di manutenzione giornaliera impostata in Intune. L'installazione viene tentata ogni giorno per 30 giorni e può non riuscire a causa di livelli di batteria o spazio insufficienti. Dopo 30 giorni, Android chiede agli utenti di eseguire l'installazione. Questa finestra viene usata anche per installare gli aggiornamenti per le app di Play. Usare questa opzione per i dispositivi dedicati, ad esempio i chioschi multimediali, in quanto consente di aggiornare le app in primo piano dei dispositivi dedicati per app singola.

- **Finestre di notifica**: se l'opzione è impostata su **Disabilita**, le notifiche, tra cui avvisi popup, chiamate in ingresso, chiamate in uscita, avvisi di sistema ed errori di sistema, non vengono visualizzate nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe visualizzare le notifiche.
- **Skip first use hints** (Ignora i suggerimenti al primo utilizzo): **Abilita** nasconde o ignora i suggerimenti dalle app che eseguono esercitazioni o i suggerimenti all'avvio dell'app. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe visualizzare questi suggerimenti all'avvio dell'app.

### <a name="system-security"></a>Protezione del sistema

- **Analisi delle minacce nelle app**: **Rendi obbligatorio** (impostazione predefinita) consente a Google Play Protect di analizzare le app prima e dopo la loro installazione. Se rileva una minaccia, può avvisare gli utenti di rimuovere l'app dal dispositivo. Quando questa opzione è impostata su **Non configurato**, Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe non abilitare o eseguire Google Play Protect per analizzare le app.

### <a name="device-experience"></a>Esperienza del dispositivo

Usare queste impostazioni per configurare un'esperienza di tipo chiosco multimediale nei dispositivi dedicati o per personalizzare le esperienze della schermata iniziale in quelli completamente gestiti. È possibile configurare i dispositivi per eseguire una sola app o per eseguire molte app. Quando un dispositivo è impostato in modalità tutto schermo, sono disponibili solo le app aggiunte.

**Tipo di profilo di registrazione**: selezionare un tipo di profilo di registrazione per avviare la configurazione di Microsoft Launcher o della schermata iniziale gestita da Microsoft nei dispositivi. Le opzioni disponibili sono:

- **Non configurata**: Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, gli utenti potrebbero visualizzare l'esperienza con la schermata iniziale predefinita del dispositivo.
- **Dispositivo dedicato**: configurare un'esperienza di tipo chiosco multimediale nei dispositivi dedicati. Prima di configurare queste impostazioni, assicurarsi di [aggiungere](../apps/apps-add-android-for-work.md) e [assegnare](../apps/apps-deploy.md) le app desiderate nei dispositivi.

  - **Modalità tutto schermo**: scegliere se il dispositivo eseguirà una sola app o più app. Le opzioni disponibili sono:

    - **Non configurata**: Intune non modifica o aggiorna questa impostazione.
    - **App singola**: gli utenti possono accedere a un'app singola nel dispositivo. All'avvio del dispositivo viene avviata solo l'app specifica. Gli utenti non possono aprire nuove app o modificare l'app in esecuzione.

      - **Selezionare un'app da usare per la modalità tutto schermo**: selezionare l'app Google Play gestita nell'elenco.

      > [!IMPORTANT]
      > quando si usa la modalità tutto schermo ad app singola, le app dialer o telefoniche potrebbero non funzionare correttamente.
  
    - **Più app**: gli utenti possono accedere a un set di app limitato nel dispositivo. All'avvio del dispositivo vengono avviate solio le app aggiunte. È anche possibile aggiungere alcuni collegamenti Web che gli utenti possono aprire. Quando viene applicato il criterio, gli utenti visualizzano le icone delle app consentite nella schermata iniziale.

      > [!IMPORTANT]
      > Per i dispositivi dedicati con più app, l'[app di schermata iniziale gestita](https://play.google.com/work/apps/details?id=com.microsoft.launcher.enterprise) da Google Play **deve essere**:
      >   - [Aggiunta in Intune](../apps/apps-add-android-for-work.md)
      >   - [Assegnata al gruppo di dispositivi](../apps/apps-deploy.md) creato per i dispositivi dedicati
      >
      > Non è richiesto che l'app di **schermata iniziale gestita** sia inclusa nel profilo di configurazione, ma è necessario che venga aggiunta come app. Quando l'app di **schermata iniziale gestita** viene aggiunta, qualsiasi altra app aggiunta nel profilo di configurazione viene visualizzata come icona nell'app di **schermata iniziale gestita**.
      >
      > Quando si usa la modalità tutto schermo con più app, le app dialer o telefoniche potrebbero non funzionare correttamente.
      >
      > Per altre informazioni sulla schermata iniziale gestita, vedere [Setup Microsoft Managed Home Screen on Dedicated devices in multi-app kiosk mode](https://techcommunity.microsoft.com/t5/intune-customer-success/how-to-setup-microsoft-managed-home-screen-on-dedicated-devices/ba-p/1388060) (Configurare la schermata iniziale gestita di Microsoft in dispositivi dedicati in modalità tutto schermo per più app).

      - **Aggiungi**: selezionare le app nell'elenco.

        Se l'app di **schermata iniziale gestita** non è inclusa nell'elenco, [aggiungerla da Google Play](https://play.google.com/work/apps/details?id=com.microsoft.launcher.enterprise). Assicurarsi di [assegnare l'app](../apps/apps-deploy.md) al gruppo di dispositivi creato per i dispositivi dedicati.

        È anche possibile aggiungere al dispositivo altre [app Android](../apps/apps-add-android-for-work.md) e [app Web](../apps/web-app.md) create dall'organizzazione. Assicurarsi di [assegnare l'app al gruppo di dispositivi creato per i dispositivi dedicati](../apps/apps-deploy.md).

      - **Icona cartella**: selezionare il colore e la forma dell'icona della cartella visualizzata nella schermata iniziale gestita. Le opzioni disponibili sono:
        - Non configurato 
        - Tema scuro - Rettangolo
        - Tema scuro - Cerchio
        - Tema chiaro - Rettangolo
        - Tema chiaro - Cerchio
      - **Dimensioni dell'icona per app e cartella**: selezionare le dimensioni dell'icona della cartella visualizzata nella schermata iniziale gestita. Le opzioni disponibili sono:
        - Non configurato 
        - Molto piccola
        - Piccola
        - Media
        - Grande
        - Molto grande

          A seconda delle dimensioni dello schermo, le dimensioni effettive dell'icona potrebbero essere diverse.

      - **Orientamento dello schermo**: selezionare la direzione in cui viene visualizzata la schermata iniziale gestita nei dispositivi. Le opzioni disponibili sono:
        - Non configurato
        - Verticale
        - Orizzontale
        - Rotazione automatica
      - **Badge per notifiche dell'app**: **Abilita** mostra il numero di notifiche nuove e non lette nelle icone dell'app. Quando questa opzione è impostata su **Non configurato**, Intune non modifica o aggiorna questa impostazione.
      - **Pulsante Pagina iniziale virtuale**: tasto softkey che riporta gli utenti alla schermata iniziale gestita in modo da potersi spostare tra le app. Le opzioni disponibili sono:
        - **Non configurato** (impostazione predefinita): non viene visualizzato un pulsante Pagina iniziale. Gli utenti devono usare il pulsante Indietro per spostarsi tra le app.
        - **Scorrimento rapido verso l'alto**: viene visualizzato un pulsante Pagina iniziale quando un utente scorre verso l'alto nel dispositivo.
        - **Mobile**: mostra un pulsante Pagina iniziale permanente e mobile nel dispositivo.

      - **Esci dalla modalità tutto schermo**: **Abilita** consente agli amministratori di sospendere temporaneamente la modalità tutto schermo per aggiornare il dispositivo. Per utilizzare questa funzionalità, l'amministratore esegue le operazioni seguenti:
  
        1. Continua a selezionare il pulsante Indietro fino a quando non viene visualizzato il pulsante **Exit kiosk** (Esci da modalità tutto schermo). 
        2. Seleziona il pulsante **Exit kiosk** (Esci da modalità tutto schermo) e immette il PIN per **Codice di uscita dalla modalità tutto schermo**.
        3. Al termine, selezionare l'**app di schermata iniziale gestita**. Questo passaggio blocca di nuovo il dispositivo in modalità tutto schermo con più app.

        Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe impedire agli amministratori di sospendere la modalità tutto schermo. Se l'amministratore continua a selezionare il pulsante Indietro e seleziona il pulsante **Exit kiosk** (Esci da modalità tutto schermo), un messaggio segnala che è richiesto un passcode.

      - **Codice di uscita dalla modalità tutto schermo**: immettere un PIN numerico da 4 a 6 cifre. L'amministratore usa questo PIN per sospendere temporaneamente la modalità tutto schermo.

      - **Imposta uno sfondo personalizzato per l'URL**: immettere un URL per personalizzare la schermata di sfondo nel dispositivo dedicato. Immettere ad esempio `http://contoso.com/backgroundimage.jpg`.

        > [!NOTE]
        > Nella maggior parte dei casi, è consigliabile iniziare almeno con immagini delle dimensioni seguenti:
        >
        > - Telefono: 1080x1920 px
        > - Tablet: 1920x1080 px
        >
        > Per ottenere la migliore esperienza e nitidezza dei dettagli, è consigliabile procedere alla creazione di asset per ogni immagine del dispositivo in base alle specifiche di visualizzazione.
        >
        > Gli schermi moderni hanno maggiori densità di pixel e consentono di visualizzare immagini con definizione equivalente a 2K/4K.

      - **Collegamento al menu Impostazioni**: **Disabilita** nasconde il collegamento Impostazioni gestite nella schermata iniziale gestita. Gli utenti possono comunque scorrere rapidamente verso il basso per accedere alle impostazioni. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il collegamento Impostazioni gestite viene visualizzato nei dispositivi. Gli utenti possono anche scorrere rapidamente verso il basso per accedere a queste impostazioni.

      - **Quick access to debug menu** (Accesso rapido al menu di debug): questa impostazione controlla il modo in cui gli utenti accedono al menu di debug. Le opzioni disponibili sono:

        - **Abilita**: gli utenti possono accedere al menu di debug più facilmente. In particolare, è possibile scorrere rapidamente verso il basso o usare il collegamento Impostazioni gestite. Come sempre, è possibile continuare a selezionare il pulsante Indietro 15 volte.
        - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, l'accesso facile al menu di debug è disattivato. Per aprire il menu di debug, gli utenti devono selezionare il pulsante Indietro 15 volte.

        Tramite il menu di debug gli utenti possono:

        - Vedere e caricare i log della schermata iniziale gestita
        - Aprire l'app Android Device Policy Manager di Google
        - Aprire l'app [Microsoft Intune](https://play.google.com/store/apps/details?id=com.microsoft.intune)
        - Uscire dalla modalità tutto schermo

      - **Configurazione Wi-Fi**: **Abilita** mostra il controllo Wi-Fi nella schermata iniziale gestita e consente agli utenti di connettere il dispositivo a diverse reti Wi-Fi. L’abilitazione di questa funzionalità attiva anche la posizione del dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe non visualizzare il controllo Wi-Fi nella schermata iniziale gestita. Impedisce agli utenti di connettersi alle reti Wi-Fi usando la schermata iniziale gestita.

        - **Elenco di reti consentite per Wi-Fi**: creare un elenco di nomi di rete wireless validi, noto anche come identificatore del set di servizi (SSID). Gli utenti della schermata iniziale gestita possono connettersi solo ai SSID immessi.

          Quando il campo è vuoto, Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, sono consentite tutte le reti Wi-Fi disponibili.

          Scegliere **Importa** per importare un file CSV che include un elenco di SSID validi.

          Scegliere **Esporta** per esportare l'elenco corrente in un file CSV.

        - **SSID**: è anche possibile immettere i nomi della rete Wi-Fi (SSID) a cui gli utenti della schermata iniziale gestita possono connettersi. Assicurarsi di immettere SSID validi.

      - **Configurazione Bluetooth**: **Abilita** mostra il controllo Bluetooth nella schermata iniziale gestita e consente agli utenti di associare i dispositivi tramite Bluetooth. L’abilitazione di questa funzionalità attiva anche la posizione del dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe non visualizzare il controllo Bluetooth nella schermata iniziale gestita. Impedisce agli utenti di configurare il Bluetooth e associare i dispositivi quando si trovano nella modalità schermata iniziale gestita.

      - **Accesso alla torcia**: **Abilita** mostra il controllo torcia nella schermata iniziale gestita e consente agli utenti di attivare o disattivare la torcia. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe non visualizzare il controllo torcia nella schermata iniziale gestita. Impedisce agli utenti di usare la torcia durante l'uso della schermata iniziale gestita.

      - **Controllo volume dei file multimediali**: **Abilita** mostra il controllo volume dei file multimediali nella schermata iniziale gestita e consente agli utenti di regolare il volume per i file multimediali del dispositivo usando un dispositivo di scorrimento. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe non visualizzare il controllo volume dei file multimediali nella schermata iniziale gestita. Impedisce agli utenti di regolare il volume dei file multimediali del dispositivo durante l'uso della schermata iniziale gestita, a meno che l'operazione non sia supportata tramite i pulsanti hardware.

      - **Quick access to device information** (Accesso rapido alle informazioni sul dispositivo): **Abilita** consente agli utenti di scorrere rapidamente verso il basso per visualizzare le informazioni sul dispositivo nella schermata iniziale gestita, ad esempio il numero di serie, la marca e il numero di modello e il livello SDK. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, le informazioni sul dispositivo potrebbero non essere visualizzate.

      - **Modalità screen saver**: **Abilita** mostra uno screen saver nella schermata iniziale gestita quando il dispositivo è bloccato o si verifica un timeout. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe non visualizzare uno screen saver nella schermata iniziale gestita.

        Se abilitata, configurare anche:

        - **Imposta l'immagine personalizzata per lo screen saver**: immettere l'URL di un file PNG, JPG, JPEG, GIF, BMP, WebP o ICOimage personalizzato. Se non si immette un URL, viene usata l'immagine predefinita del dispositivo, se è presente un'immagine predefinita.

          Immettere ad esempio:

          - `http://www.contoso.com/image.jpg`
          - `www.contoso.com/image.bmp`
          - `https://www.contoso.com/image.webp`

          > [!TIP]
          > È supportato qualsiasi URL di risorsa file che possa essere trasformato in una bitmap.

        - **Numero di secondi per cui viene visualizzato lo screen saver nel dispositivo prima dello spegnimento dello schermo**: scegliere per quanto tempo il dispositivo visualizza lo screensaver. Immettere un valore compreso tra 0 e 9999999 secondi. Il valore predefinito è `0` secondi. Se l'opzione viene lasciata vuota o viene impostata su zero (`0`), lo screen saver rimane attivo fino all'interazione di un utente con il dispositivo.
        - **Numero di secondi di inattività del dispositivo prima della visualizzazione dello screen saver**: scegliere per quanto tempo il dispositivo deve rimanere inattivo prima di visualizzare lo screensaver. Immettere un valore compreso tra 1 e 9999999 secondi. Il valore predefinito è `30` secondi. È necessario immettere un numero maggiore di zero (`0`).
        - **Rileva file multimediali prima di avviare lo screen saver**: l'impostazione predefinita **Abilita** non mostra lo screen saver se sono in riproduzione elementi audio o video nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe visualizzare le screen saver, anche se sono in riproduzione elementi audio o video.

- **Completamente gestito**: configura l'app Microsoft Launcher nei dispositivi completamente gestiti.

  - **Imposta Microsoft Launcher come utilità di avvio predefinita**: l'opzione **Abilita** imposta Microsoft Launcher come utilità di avvio predefinita nella schermata iniziale. Se si imposta l'utilità di avvio come predefinita, gli utenti non possono usare un'altra utilità di avvio. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, Microsoft Launcher non viene impostato forzatamene come utilità di avvio predefinita.
  - **Configura uno sfondo personalizzato**: **Abilita** consente di applicare una propria immagine come sfondo della schermata iniziale e di scegliere se gli utenti possono cambiare l'immagine. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il dispositivo mantiene lo sfondo corrente.
    - **Immettere l'URL dell'immagine di sfondo**: immettere l'URL dell'immagine di sfondo. Questa immagine viene visualizzata nella schermata iniziale del dispositivo. Immettere ad esempio `http://www.contoso.com/image.jpg`. 
    - **Consenti all'utente di modificare lo sfondo**: **Abilita** consente agli utenti di modificare l'immagine dello sfondo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, agli utenti viene impedito di modificare lo sfondo.
  - **Abilita il feed del launcher**: **Abilita** attiva il feed del launcher, che mostra i calendari, i documenti e le attività recenti. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, questo feed non viene visualizzato.
    - **Consenti all'utente di abilitare/disabilitare il feed**: **Abilita** consente agli utenti di abilitare o disabilitare il feed del launcher. **Abilita** forza questa impostazione solo alla prima assegnazione del profilo. Le eventuali assegnazioni di profilo future non forzano questa impostazione. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, agli utenti viene impedito di modificare le impostazioni del feed del launcher.
  - **Presenza della bacheca**: la bacheca consente agli utenti di accedere rapidamente alle app e agli strumenti. Le opzioni disponibili sono:
    - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione.
    - **Mostra**: la bacheca viene visualizzata nei dispositivi.
    - **Nascondi**: la bacheca viene nascosta. Gli utenti devono scorrere rapidamente verso l'alto per accedere alla bacheca.
    - **Disabilitato**: la bacheca non viene visualizzata nei dispositivi e agli utenti viene impedito di visualizzarla.

  - **Consenti all'utente di modificare la presenza della bacheca**: **Abilita** consente agli utenti di visualizzare o nascondere la bacheca. **Abilita** forza questa impostazione solo alla prima assegnazione del profilo. Le eventuali assegnazioni di profilo future non forzano questa impostazione. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, agli utenti non è consentito modificare la configurazione della bacheca del dispositivo.

  - **Posizionamento della barra di ricerca**: scegliere dove posizionare la barra di ricerca. Le opzioni disponibili sono:
    - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione.
    - **In alto**: la barra di ricerca viene visualizzata nella parte superiore dei dispositivi.
    - **In basso**: la barra di ricerca viene visualizzata nella parte inferiore dei dispositivi.
    - **Nascondi**: la barra di ricerca è nascosta.

<!-- MandiA (7.16.2020) The following settings may be in a future release. Per PM, we can leave it in GitHub, not live. Remove comment tags if/when it releases.
  - **Allow user to change search bar placement**: **Enable** allows users to change the location of the search bar. **Enable** only forces this setting the first time the profile is assigned. Any future profile assignments don't force this setting. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, users are prevented from changing the location.
End of comment -->

### <a name="password"></a>Password

- **Disabilita la schermata di blocco**: scegliere **Disabilita** per impedire agli utenti di usare la funzionalità della schermata di blocco di protezione della tastiera nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di usare le funzionalità di protezione della tastiera.
- **Funzionalità disabilitate della schermata di blocco**: se la protezione della tastiera è abilitata sul dispositivo, scegliere quali funzionalità disabilitare. Ad esempio, se è selezionata l'opzione **Secure camera** (Fotocamera sicura), la funzionalità fotocamera è disabilitata nel dispositivo. Le funzionalità non selezionate sono abilitate nel dispositivo.

  Queste funzionalità sono disponibili per gli utenti quando il dispositivo è bloccato. Gli utenti non potranno visualizzare o accedere alle funzionalità che sono selezionate.

- **Tipo di password richiesto**: immettere il livello di complessità delle password necessario e se possono essere usati dispositivi biometrici. Le opzioni disponibili sono:
  - **Impostazione predefinita dispositivo**
  - **Password obbligatoria, nessuna restrizione**
  - **Biometrica vulnerabile**: [Biometrica complessa e vulnerabile a confronto](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (apre il sito Web Android)
  - **Numerica**: la password contiene solo numeri, ad esempio `123456789`. Specificare anche:
    - **Lunghezza minima password**: immettere la lunghezza minima per la password che deve essere compresa tra da 4 e 16 caratteri.
  - **Complessa numerica**: i numeri consecutivi o ripetuti (ad esempio, "1111" o "1234") non sono consentiti. Specificare anche:
    - **Lunghezza minima password**: immettere la lunghezza minima per la password che deve essere compresa tra da 4 e 16 caratteri.
  - **Alfabetica**: è obbligatorio usare le lettere dell'alfabeto. Numeri e simboli non sono richiesti. Specificare anche:
    - **Lunghezza minima password**: immettere la lunghezza minima per la password che deve essere compresa tra da 4 e 16 caratteri.
  - **Alfanumerica**: include lettere maiuscole, lettere minuscole e caratteri numerici. Specificare anche:
    - **Lunghezza minima password**: immettere la lunghezza minima per la password che deve essere compresa tra da 4 e 16 caratteri.
  - **Alfanumerico con simboli**: include lettere maiuscole, lettere minuscole, caratteri numerici, segni di punteggiatura e simboli. Specificare anche:

    - **Lunghezza minima password**: immettere la lunghezza minima per la password che deve essere compresa tra da 4 e 16 caratteri.
    - **Numero di caratteri obbligatori**: immettere il numero di caratteri che deve contenere la password, compreso tra 0 e 16 caratteri.
    - **Numero di caratteri minuscoli obbligatori**: immettere il numero di caratteri minuscoli che deve contenere la password, compreso tra 0 e 16 caratteri.
    - **Numero di caratteri maiuscoli obbligatori**: immettere il numero di caratteri maiuscoli che deve contenere la password, compreso tra 0 e 16 caratteri.
    - **Numero di caratteri diversi da lettere obbligatori**: immettere il numero di caratteri (diversi dalle lettere dell'alfabeto) compreso tra 0 e 16 caratteri che la password deve contenere.
    - **Numero di caratteri numerici obbligatori**: immettere il numero di caratteri numerici (`1`, `2`, `3` e così via) compreso tra 0 e 16 caratteri che la password deve contenere.
    - **Numero di caratteri di tipo simbolo obbligatori**: immettere il numero di caratteri di tipo simbolo (`&`, `#`, `%` e così via) compreso tra 0 e 16 caratteri che la password deve contenere.

- **Numero di giorni rimanenti prima della scadenza della password**: immettere il numero di giorni che devono trascorrere prima che sia necessario cambiare la password del dispositivo, da 1 a 365. Ad esempio, immettere `90` per impostare la scadenza della password dopo 90 giorni. Quando la password scade, agli utenti viene chiesto di creare una nuova password. Quando il valore è vuoto, Intune non modifica o aggiorna questa impostazione.
- **Numero di password obbligatorie prima che un utente possa riutilizzare una password**: usare questa impostazione per impedire agli utenti di creare password già usate in precedenza. immettere il numero di password usate in precedenza che non è possibile usare, da 1 a 24. Ad esempio, immettere `5` in modo che gli utenti non possano definire una nuova password uguale alla password corrente o a una qualsiasi delle quattro precedenti. Quando il valore è vuoto, Intune non modifica o aggiorna questa impostazione.
- **Numero di errori di accesso prima della cancellazione dei dati del dispositivo**: immettere il numero di password non corrette consentite prima che il dispositivo venga cancellato, da 4 a 11. `0` (zero) potrebbe disabilitare la funzionalità di cancellazione dei dispositivi. Quando il valore è vuoto, Intune non modifica o aggiorna questa impostazione.

  > [!NOTE]
  > Ai dispositivi con profili di lavoro completamente gestiti, dedicati e di proprietà aziendale non verrà richiesto di impostare una password. Le impostazioni verranno applicate e sarà necessario impostare manualmente la password. Il criterio che impone questo segnalerà l'esito negativo fino a quando non si imposta la password che soddisfa i requisiti.

### <a name="power-settings"></a>Impostazioni di risparmio energia

- **Tempo per la schermata di blocco**: immettere il tempo massimo che un utente può impostare fino al blocco del dispositivo. Ad esempio, con l'impostazione `10 minutes`, gli utenti possono impostare il tempo da 15 secondi fino a 10 minuti. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.

- **Schermata attivata con dispositivo collegato**: scegliere i tipi di alimentazione che mantengono attiva la schermata del dispositivo collegato.

### <a name="users-and-accounts"></a>Utenti e account

- **Aggiungi nuovi utenti**: **Blocca** impedisce agli utenti di aggiungere nuovi utenti. Ogni utente dispone di uno spazio personale nel dispositivo per schermate iniziali, account, app e impostazioni personalizzati. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di aggiungere altri utenti al dispositivo.
- **Rimozione degli utenti**: **Blocca** impedisce agli utenti di rimuovere utenti. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di rimuovere altri utenti dal dispositivo.
- **Modifiche dell'account** (solo per dispositivi dedicati): **Blocca** impedisce agli utenti di modificare gli account. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di aggiornare gli account utente nel dispositivo.

  > [!NOTE]
  > Questa impostazione non viene rispettata nei dispositivi con profilo di lavoro completamente gestiti, dedicati e di proprietà aziendale. Se si configura questa impostazione, l'impostazione viene ignorata e non ha alcun effetto.

- **L'utente può configurare le credenziali**: **Blocca** impedisce agli utenti di configurare i certificati assegnati ai dispositivi, anche per i dispositivi non associati a un account utente. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di configurare o modificare le proprie credenziali quando accedono all'archivio chiavi.
- **Account Google personale**: **Blocca** impedisce agli utenti di aggiungere il proprio account Google personale al dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di aggiungere il proprio account Google personale.

### <a name="applications"></a>Applicazioni

- **Consenti l'installazione da origini sconosciute**: **Consenti** consente agli utenti di attivare **Origini sconosciute**. Questa impostazione consente di installare app da origini sconosciute, tra cui origini diverse da Google Play Store. Consente agli utenti di caricare le app nel dispositivo con metodi diversi da Google Play Store. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe impedire agli utenti di attivare **Origini sconosciute**.
- **Consenti l'accesso a tutte le app in Google Play Store**: con l'impostazione **Consenti** gli utenti ottengono l'accesso a tutte le app in Google Play Store. Non possono accedere alle app bloccate dall'amministratore in [App client](../apps/apps-add-android-for-work.md).

  Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe:
  
  - Imporre agli utenti di accedere solo alle app che l'amministratore rende disponibili in Google Play Store o alle app richieste in [App client](../apps/apps-add-android-for-work.md). 
  - Disinstallare automaticamente tutte le app rilevate come installate da utenti al di fuori di Google Play Store.

  Se si vuole abilitare il caricamento da altre origini, impostare le opzioni **Consenti l'installazione da origini sconosciute** e **Consenti l'accesso a tutte le app in Google Play Store** su **Consenti**.

- **Aggiornamenti automatici delle app**: i dispositivi controllano ogni giorno la disponibilità di aggiornamenti per le app. scegliere se gli aggiornamenti automatici vengono installati. Le opzioni disponibili sono:
  - **Non configurata**: Intune non modifica o aggiorna questa impostazione.
  - **Scelta utente**: il sistema operativo potrebbe usare questa opzione per impostazione predefinita. Gli utenti possono impostare le proprie preferenze nell'app Google Play gestita.
  - **Mai**: gli aggiornamenti non vengono mai installati. Questa opzione non è consigliata.
  - **Solo Wi-Fi**: gli aggiornamenti vengono installati solo quando il dispositivo è connesso a una rete Wi-Fi.
  - **Sempre**: gli aggiornamenti vengono installati quando sono disponibili.

### <a name="connectivity"></a>Connettività

- **Always-on VPN** (VPN sempre attiva): scegliere **Abilita** per impostare il client VPN in modo che si connetta e riconnetta automaticamente alla VPN. Le connessioni VPN sempre attive rimarranno connesse. In alternativa, connettersi immediatamente quando gli utenti bloccano il dispositivo, il dispositivo viene riavviato o la rete wireless cambia.

  Scegliere **Non configurata** per disabilitare la VPN sempre attiva per tutti i client VPN.

  > [!IMPORTANT]
  > Assicurarsi di distribuire una sola policy VPN sempre attiva in un singolo dispositivo. La distribuzione di più policy VPN sempre attive in un singolo dispositivo non è supportata.

- **VPN client** (Client VPN): scegliere un client VPN che supporta Always On. Le opzioni disponibili sono:
  - Cisco AnyConnect
  - F5 Access
  - Palo Alto Networks GlobalProtect
  - Pulse Secure
  - Personalizzato
    - **ID pacchetto**: immettere l'ID pacchetto dell'app in Google Play Store. Se ad esempio l'URL per l'app in Play Store è `https://play.google.com/store/details?id=com.contosovpn.android.prod`, l'ID pacchetto è `com.contosovpn.android.prod`.

  > [!IMPORTANT]
  > - Il client VPN scelto deve essere installato nel dispositivo e deve supportare la VPN per app nei profili di lavoro. In caso contrario si verificherà un errore. 
  > - È necessario approvare l'app client VPN in **Google Play Store gestito**, sincronizzare l'app con Intune e distribuire l'app nel dispositivo. Al termine di queste operazioni, l'app viene installata nel profilo di lavoro dell'utente.
  > - È comunque necessario configurare il client VPN con un [profilo VPN](vpn-settings-android-enterprise.md) o tramite un [profilo di configurazione dell'app](../apps/app-configuration-policies-use-android.md).
  > - Possono esistere problemi noti quando si usa una VPN per app con F5 Access per Android 3.0.4. Per altre informazioni, vedere le [note sulla versione di F5 per F5 Access per Android 3.0.4](https://support.f5.com/kb/en-us/products/big-ip_apm/releasenotes/related/relnote-f5access-android-3-0-4.html#relnotes_known_issues_f5_access_android).

- **Lockdown mode** (Modalità di blocco): **Abilita** impone l'uso del tunnel VPN per tutto il traffico di rete. Se non viene stabilita una connessione alla VPN, il dispositivo non avrà accesso alla rete. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire al traffico di passare attraverso il tunnel VPN o la rete per dispositivi mobili.

- **Proxy globale consigliato**: **Abilita** aggiunge un proxy globale ai dispositivi. Se abilitata, il traffico HTTP e HTTPS, incluse alcune app nel dispositivo, usano il proxy immesso. Questo proxy è solo un suggerimento. È possibile che alcune app non usino il proxy. **Non configurato** (impostazione predefinita) non aggiunge un proxy globale consigliato.

  Per altre informazioni su questa funzionalità, vedere [setRecommendedGlobalProxy](https://developer.android.com/reference/android/app/admin/DevicePolicyManager.html#setRecommendedGlobalProxy(android.content.ComponentName,%20android.net.ProxyInfo)) (apre un sito Android).

  Se abilitata, immettere anche il **Tipo** di proxy. Le opzioni disponibili sono:

  - **Diretto**: immettere manualmente i dettagli del server proxy, tra cui:
    - **Host**: immettere il nome host o l'indirizzo IP del server proxy. Ad esempio, immettere `proxy.contoso.com` o `127.0.0.1`.
    - **Numero porta**: immettere il numero della porta TCP usato dal server proxy. Immettere ad esempio `8080`.
    - **Host esclusi**: immettere un elenco di nomi host o indirizzi IP che non useranno il proxy. Questo elenco può includere un carattere jolly asterisco (`*`) e più host separati da punti e virgola (`;`) senza spazi. Immettere ad esempio `127.0.0.1;web.contoso.com;*.microsoft.com`.

  - **Configurazione automatica del proxy**: immettere l'**URL PAC** per uno script di configurazione automatica del proxy. Immettere ad esempio `https://proxy.contoso.com/proxy.pac`.

    Per altre informazioni, vedere l'articolo sul [file di configurazione automatica proxy (PAC)](https://developer.mozilla.org/docs/Web/HTTP/Proxy_servers_and_tunneling/Proxy_Auto-Configuration_(PAC)_file) (viene aperto un sito non Microsoft).

  Per altre informazioni su questa funzionalità, vedere [setRecommendedGlobalProxy](https://developer.android.com/reference/android/app/admin/DevicePolicyManager.html#setRecommendedGlobalProxy(android.content.ComponentName,%20android.net.ProxyInfo)) (apre un sito Android).

## <a name="work-profile-only"></a>Solo profilo di lavoro

Queste impostazioni si applicano ai tipi di registrazione Android Enterprise in cui Intune controlla solo il profilo di lavoro, ad esempio la registrazione del profilo di lavoro di Android Enterprise in un dispositivo personale o Bring Your Own Device (BYOD).

### <a name="work-profile-settings"></a>Impostazioni del profilo di lavoro

- **Copia e incolla tra il profilo di lavoro e il profilo personale**: **Blocca** impedisce le attività di tipo copia e incolla tra le app di lavoro e quelle personali. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di condividere i dati tramite copia e incolla con le app nel profilo personale.
- **Condivisione dei dati tra i profili di lavoro e personali**: scegliere se le app del profilo di lavoro possono condividere i dati con le app del profilo personale. Ad esempio, è possibile controllare le azioni di condivisione all'interno delle applicazioni, come l'opzione **Condividi** nell'app browser Chrome. Questa impostazione non si applica al comportamento di copia/incolla degli Appunti. Le opzioni disponibili sono:
  - **Impostazione predefinita dispositivo**: il comportamento di condivisione predefinito del dispositivo varia in base alla versione di Android:
    - nei dispositivi che eseguono Android 6.0 e versioni successive, la condivisione dal profilo di lavoro al profilo personale è bloccata. La condivisione dal profilo personale al profilo di lavoro è consentita.
    - Nei dispositivi che eseguono Android 5.0 e versioni precedenti, la condivisione tra il profilo di lavoro e il profilo personale è bloccata in entrambe le direzioni.
  - **Le app nel profilo di lavoro possono gestire una richiesta di condivisione dal profilo personale**: abilita la funzionalità di Android predefinita che consente la condivisione dal profilo personale a quello di lavoro. Quando questa opzione è abilitata, una richiesta di condivisione da un'app nel profilo personale supporta la condivisione con app nel profilo di lavoro. Questa impostazione rappresenta il comportamento predefinito per i dispositivi Android che eseguono versioni precedenti alla 6.0.
  - **Nessuna restrizione sulla condivisione**: abilita la condivisione tra i limiti del profilo di lavoro in entrambe le direzioni. Quando si seleziona questa impostazione, le app nel profilo di lavoro possono condividere dati con app senza badge nel profilo personale. Questa impostazione consente la condivisione tra le app gestite nel profilo di lavoro e le app nella parte non gestita del dispositivo. Usare quindi questa impostazione con cautela.

- **Notifiche del profilo di lavoro durante il blocco del dispositivo**: **Blocca** impedisce la visualizzazione delle notifiche nei dispositivi bloccati, tra cui avvisi popup, chiamate in ingresso, chiamate in uscita, avvisi di sistema ed errori di sistema. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe visualizzare le notifiche.
- **Autorizzazioni delle app predefinite**: Imposta i criteri di autorizzazione predefiniti per tutte le app del profilo di lavoro. A partire da Android 6, agli utenti viene richiesto di concedere alcune autorizzazioni richieste dalle app, all'avvio dell'app. Questa impostazione dei criteri consente di decidere se richiedere agli utenti di concedere autorizzazioni per tutte le app nel profilo di lavoro. Ad esempio, si può assegnare al profilo di lavoro un'app che richiede l'accesso alla posizione. In genere, un'app di questo tipo richiede agli utenti di concedere o negare l'accesso alla posizione all'app. Usare questo criterio per concedere o negare automaticamente le autorizzazioni senza richiesta oppure per lasciar decidere agli utenti. Le opzioni disponibili sono:
  - **Impostazione predefinita dispositivo**
  - **Messaggio di richiesta**
  - **Concedi automaticamente**
  - **Nega automaticamente**

  È anche possibile usare un criterio di configurazione dell'app per concedere le autorizzazioni per le singole app (**App client** > **Criteri di configurazione dell'app**).

- **Aggiungi o rimuovi account**: **Blocca** impedisce agli utenti di aggiungere o rimuovere manualmente account nel profilo di lavoro. Ad esempio, quando si distribuisce l'app Gmail in un profilo di lavoro Android, è possibile impedire agli utenti di aggiungere o rimuovere account in questo profilo di lavoro. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'aggiunta di account nel profilo di lavoro.  

  > [!NOTE]
  > Non è possibile aggiungere account Google a un profilo di lavoro.

- **Condivisione dei contatti tramite Bluetooth**: **Abilita** consente di condividere i contatti dei profili di lavoro e di accedervi da un altro dispositivo, inclusa l'automobile, associato tramite Bluetooth. L'abilitazione di questa impostazione può consentire a determinati dispositivi Bluetooth di memorizzare nella cache i contatti di lavoro al momento della prima connessione. Se si disabilita questo criterio dopo un'associazione/sincronizzazione iniziale, i contatti di lavoro potrebbero non essere rimossi da un dispositivo Bluetooth.

  Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe non condividere i contatti di lavoro.

  Questa impostazione si applica a:

  - Dispositivi con profilo di lavoro Android che eseguono il sistema operativo Android 6.0 e versioni successive

- **Acquisizione schermo**: **Blocca** impedisce screenshot o acquisizioni di schermate nel dispositivo nel profilo di lavoro. Impedisce anche la visualizzazione del contenuto nei dispositivi di visualizzazione privi di output video protetto. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'acquisizione di screenshot.

- **Mostra l'ID chiamante del contatto nel profilo personale**: **Blocca** non visualizza il numero del chiamante del contatto di lavoro nel profilo personale. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe visualizzare i dettagli del chiamante del contatto di lavoro.

  Questa impostazione si applica a:

  - Sistema operativo Android 6.0 e versioni successive

- **Cerca contatti di lavoro dal profilo personale**: **Blocca** impedisce agli utenti di cercare contatti di lavoro nelle app nel profilo personale. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire la ricerca di contatti di lavoro nel profilo personale.

- **Fotocamera**: **Blocca** impedisce l'accesso alla fotocamera nel dispositivo nel profilo di lavoro. Questa impostazione non interessa la fotocamera nel profilo personale. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'accesso alla fotocamera.

- **Consenti i widget dalle app nel profilo di lavoro**: **Abilita** consente agli utenti di inserire i widget esposti dalle app nella schermata iniziale. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe disabilitare questa funzionalità.

  Ad esempio, Outlook viene installato nei profili di lavoro degli utenti. Con l'impostazione **Abilitata** gli utenti possono inserire il widget dell'agenda nella schermata iniziale del dispositivo.

- **Richiedi la password del profilo di lavoro**: **Rendi obbligatorio** impone criteri di passcode applicabili solo alle app nel profilo di lavoro. Per impostazione predefinita, gli utenti possono usare due PIN definiti separatamente. In alternativa, gli utenti possono combinare i PIN nel più sicuro dei due PIN. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di usare app di lavoro senza immettere una password.

  Questa impostazione si applica a:

  - Android 7.0 e versioni successive con il profilo di lavoro abilitato

- **Lunghezza minima password**: immettere la lunghezza minima per la password che deve essere compresa tra da 4 e 16 caratteri.
- **Numero massimo di minuti di inattività fino al blocco del profilo di lavoro**: immettere il periodo di tempo per cui i dispositivi devono rimanere inattivi prima che lo schermo venga bloccato automaticamente. Gli utenti devono immettere le credenziali per riottenere l'accesso. Ad esempio, immettere `5` per bloccare il dispositivo dopo 5 minuti di inattività. Quando il valore è vuoto o impostato su **Non configurato**, Intune non modifica o aggiorna questa impostazione.

  Nei dispositivi, gli utenti non possono impostare un valore di tempo maggiore di quello configurato nel profilo. Gli utenti possono impostare un valore di tempo inferiore. Ad esempio, se il profilo è impostato su `15` minuti, gli utenti possono impostare il valore su 5 minuti, ma non possono impostare il valore su 30 minuti.

- **Numero di errori di accesso prima della cancellazione dei dati del dispositivo**: immettere il numero di password non corrette consentite prima che il dispositivo venga cancellato, da 4 a 11. `0` (zero) potrebbe disabilitare la funzionalità di cancellazione dei dispositivi. Quando il valore è vuoto, Intune non modifica o aggiorna questa impostazione.

- **Scadenza password (giorni)** : immettere il numero di giorni prima che sia necessario modificare le password utente (**1**-**365**).
- **Tipo di password richiesto**: immettere il livello di complessità delle password necessario e se possono essere usati dispositivi biometrici. Le opzioni disponibili sono:
  - **Impostazione predefinita dispositivo**
  - **Protezione biometrica bassa**: [Biometrica complessa e vulnerabile a confronto](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (apre il sito Web Android)
  - **Richiesto**
  - **Almeno numerico**: include caratteri numerici, ad esempio `123456789`.
  - **Complessa numerica**: i numeri consecutivi o ripetuti (ad esempio, `1111` o `1234`) non sono consentiti.
  - **Almeno alfabetico**: include lettere dell'alfabeto. Numeri e simboli non sono richiesti.
  - **Almeno alfanumerico**: include lettere maiuscole, lettere minuscole e caratteri numerici.
  - **Almeno alfanumerico con simboli**: include lettere maiuscole, lettere minuscole, caratteri numerici, segni di punteggiatura e simboli.

- **Impedisci riutilizzo delle password precedenti**: usare questa impostazione per impedire agli utenti di creare password già usate in precedenza. immettere il numero di password usate in precedenza che non è possibile usare, da 1 a 24. Ad esempio, immettere `5` in modo che gli utenti non possano definire una nuova password uguale alla password corrente o a una qualsiasi delle quattro precedenti. Quando il valore è vuoto, Intune non modifica o aggiorna questa impostazione.
- **Sblocco con impronta digitale**: **Blocca** impedisce agli utenti finali di usare lo scanner di impronta digitale del dispositivo per sbloccarlo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di sbloccare il dispositivo tramite impronta digitale.
- **Smart Lock e altri agenti di attendibilità**: **Blocca** impedisce a Smart Lock o altri agenti di attendibilità di modificare le impostazioni della schermata di blocco nei dispositivi compatibili. Questa funzionalità, chiamata anche agente di attendibilità, consente di disabilitare o ignorare la password della schermata di blocco del dispositivo se si trova in una posizione attendibile. Ad esempio, ignorare la password del profilo di lavoro quando i dispositivi sono connessi a un dispositivo Bluetooth specifico oppure quando si trovano nelle vicinanze di un tag NFC. Usare questa impostazione per impedire agli utenti di configurare Smart Lock.

  Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.

### <a name="password"></a>Password

Queste impostazioni per le password si applicano ai profili personali nei dispositivi che usano un profilo di lavoro.

- **Lunghezza minima password**: immettere la lunghezza minima per la password che deve essere compresa tra da 4 e 16 caratteri.
- **Numero massimo di minuti di inattività fino al blocco dello schermo**: immettere il periodo di tempo per cui i dispositivi devono rimanere inattivi prima che lo schermo venga bloccato automaticamente. Gli utenti devono immettere le credenziali per riottenere l'accesso. Ad esempio, immettere `5` per bloccare il dispositivo dopo 5 minuti di inattività. Quando il valore è vuoto o impostato su **Non configurato**, Intune non modifica o aggiorna questa impostazione.

  Nei dispositivi, gli utenti non possono impostare un valore di tempo maggiore di quello configurato nel profilo. Gli utenti possono impostare un valore di tempo inferiore. Ad esempio, se il profilo è impostato su `15` minuti, gli utenti possono impostare il valore su 5 minuti, ma non possono impostare il valore su 30 minuti.

- **Numero di errori di accesso prima della cancellazione dei dati del dispositivo**: immettere il numero di password non corrette consentite prima che il dispositivo venga cancellato, da 4 a 11. `0` (zero) potrebbe disabilitare la funzionalità di cancellazione dei dispositivi. Quando il valore è vuoto, Intune non modifica o aggiorna questa impostazione.
- **Scadenza password (giorni)** : immettere il numero di giorni che devono trascorrere prima che sia necessario cambiare la password del dispositivo, da 1 a 365. Ad esempio, immettere `90` per impostare la scadenza della password dopo 90 giorni. Quando la password scade, agli utenti viene chiesto di creare una nuova password. Quando il valore è vuoto, Intune non modifica o aggiorna questa impostazione.
- **Tipo di password richiesto**: immettere il livello di complessità delle password necessario e se possono essere usati dispositivi biometrici. Le opzioni disponibili sono:
  - **Impostazione predefinita dispositivo**
  - **Protezione biometrica bassa**: [Biometrica complessa e vulnerabile a confronto](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (apre il sito Web Android)
  - **Richiesto**
  - **Almeno numerico**: include caratteri numerici, ad esempio `123456789`.
  - **Complessa numerica**: i numeri consecutivi o ripetuti (ad esempio, `1111` o `1234`) non sono consentiti.
  - **Almeno alfabetico**: include lettere dell'alfabeto. Numeri e simboli non sono richiesti.
  - **Almeno alfanumerico**: include lettere maiuscole, lettere minuscole e caratteri numerici.
  - **Almeno alfanumerico con simboli**: include lettere maiuscole, lettere minuscole, caratteri numerici, segni di punteggiatura e simboli.

- **Impedisci riutilizzo delle password precedenti**: usare questa impostazione per impedire agli utenti di creare password già usate in precedenza. immettere il numero di password usate in precedenza che non è possibile usare, da 1 a 24. Ad esempio, immettere `5` in modo che gli utenti non possano definire una nuova password uguale alla password corrente o a una qualsiasi delle quattro precedenti. Quando il valore è vuoto, Intune non modifica o aggiorna questa impostazione.
- **Sblocco con impronta digitale**: **Blocca** impedisce agli utenti finali di usare lo scanner di impronta digitale del dispositivo per sbloccarlo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di sbloccare il dispositivo tramite impronta digitale.
- **Smart Lock e altri agenti di attendibilità**: **Blocca** impedisce a Smart Lock o altri agenti di attendibilità di modificare le impostazioni della schermata di blocco nei dispositivi compatibili. Questa funzionalità, chiamata anche agente di attendibilità, consente di disabilitare o ignorare la password della schermata di blocco del dispositivo se si trova in una posizione attendibile. Ad esempio, ignorare la password del profilo di lavoro quando i dispositivi sono connessi a un dispositivo Bluetooth specifico oppure quando si trovano nelle vicinanze di un tag NFC. Usare questa impostazione per impedire agli utenti di configurare Smart Lock.

  Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.

### <a name="system-security"></a>Protezione del sistema

- **Analisi delle minacce nelle app**: specificare **Rendi obbligatorio** per imporre l'abilitazione dell'impostazione **Verifica app** per i profili di lavoro e personali. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.

  Questa impostazione si applica a:

  - Android 8 (Oreo) e versioni successive

- **Impedisci le installazioni di app da origini sconosciute nel profilo personale**: per impostazione predefinita, i dispositivi con profilo di lavoro Android Enterprise non possono installare le app da origini diverse da Play Store. Questa impostazione consente agli amministratori di controllare maggiormente le installazioni di app da origini sconosciute. **Blocca** impedisce l'installazione di app da origini diverse da Google Play Store nel profilo personale. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire l'installazione di app da origini sconosciute nel profilo personale. Per definizione, i dispositivi con profilo di lavoro sono progettati per supportare due profili:

  - Un profilo di lavoro gestito tramite MDM.
  - Un profilo personale isolato dalla gestione MDM.

### <a name="connectivity"></a>Connettività

- **Always-on VPN** (VPN sempre attiva): scegliere **Abilita** per impostare un client VPN in modo che si connetta e riconnetta automaticamente alla VPN. Le connessioni VPN sempre attive rimarranno connesse. In alternativa, connettersi immediatamente quando gli utenti bloccano il dispositivo, il dispositivo viene riavviato o la rete wireless cambia.

  Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe disabilitare la VPN sempre attiva per tutti i client VPN.

  > [!IMPORTANT]
  > Assicurarsi di distribuire una sola policy VPN sempre attiva in un singolo dispositivo. La distribuzione di più policy VPN sempre attiva in un singolo dispositivo non è supportata.

- **VPN client** (Client VPN): scegliere un client VPN che supporta Always On. Le opzioni disponibili sono:
  - Cisco AnyConnect
  - F5 Access
  - Palo Alto Networks GlobalProtect
  - Pulse Secure
  - Personalizzato
    - **ID pacchetto**: immettere l'ID pacchetto dell'app in Google Play Store. Se ad esempio l'URL per l'app in Play Store è `https://play.google.com/store/details?id=com.contosovpn.android.prod`, l'ID pacchetto è `com.contosovpn.android.prod`.

  > [!IMPORTANT]
  > - Il client VPN scelto deve essere installato nel dispositivo e deve supportare la VPN per app nei profili di lavoro. In caso contrario si verificherà un errore.
  > - È necessario approvare l'app client VPN in **Google Play Store gestito**, sincronizzare l'app con Intune e distribuire l'app nel dispositivo. Al termine di queste operazioni, l'app viene installata nel profilo di lavoro dell'utente.
  > - Possono esistere problemi noti quando si usa una VPN per app con F5 Access per Android 3.0.4. Per altre informazioni, vedere le [note sulla versione di F5 per F5 Access per Android 3.0.4](https://support.f5.com/kb/en-us/products/big-ip_apm/releasenotes/related/relnote-f5access-android-3-0-4.html#relnotes_known_issues_f5_access_android).

- **Lockdown mode** (Modalità di blocco): **Abilita** impone l'uso del tunnel VPN per tutto il traffico di rete. Se non viene stabilita una connessione alla VPN, il dispositivo non avrà accesso alla rete.

  Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire al traffico di passare attraverso il tunnel VPN o la rete per dispositivi mobili.

## <a name="next-steps"></a>Passaggi successivi

[Assegnare il profilo](device-profile-assign.md) e [monitorarne lo stato](device-profile-monitor.md).

È anche possibile creare profili in modalità tutto schermo per dispositivi dedicati [Android](device-restrictions-android.md#kiosk) e [Windows 10](kiosk-settings.md).

[Configurare e risolvere i problemi dei dispositivi Android Enterprise in Microsoft Intune](https://support.microsoft.com/help/4476974).
