---
title: Impostazioni relative alla modalità tutto schermo per Windows 10 in Microsoft Intune - Azure | Microsoft Docs
description: Configurare i dispositivi Windows 10 e versioni successive per l'esecuzione di una o più app in modalità tutto schermo, personalizzare il menu Start, aggiungere app, visualizzare la barra della applicazioni e configurare un Web browser in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/21/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6a37b94ee0e474e9e3da6aae359ba1b315212910
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/26/2020
ms.locfileid: "88911931"
---
# <a name="windows-10-and-later-device-settings-to-run-as-a-kiosk-in-intune"></a>Impostazioni dei dispositivi Windows 10 e versioni successive per l'esecuzione in modalità tutto schermo in Intune

È possibile configurare i dispositivi Windows 10 e versioni successive per l'esecuzione di una o più app in modalità tutto schermo.

Questo articolo descrive le diverse impostazioni che è possibile controllare nei dispositivi Windows 10 e versioni successive. Usare queste impostazioni nella propria soluzione di gestione di dispositivi mobili (MDM) per configurare i dispositivi Windows 10 e versioni successive da eseguire in modalità tutto schermo.

Come amministratore di Intune, è possibile creare e assegnare queste impostazioni ai dispositivi.

Per altre informazioni sulla funzionalità Modalità tutto schermo di Windows in Intune, vedere [Configurare le impostazioni a tutto schermo](kiosk-settings.md).

## <a name="before-you-begin"></a>Prima di iniziare

- [Creare il profilo](kiosk-settings.md#create-the-profile).

- Questo profilo per la modalità tutto schermo è direttamente correlato al profilo di restrizioni per i dispositivi creato usando le [impostazioni della modalità tutto schermo di Microsoft Edge](device-restrictions-windows-10.md#microsoft-edge-browser). Per concludere:

  1. Creare questo profilo per la modalità tutto schermo per l'esecuzione del dispositivo in modalità tutto schermo.
  2. Creare il [profilo di restrizioni per i dispositivi](device-restrictions-windows-10.md#microsoft-edge-browser) e configurare le funzionalità e le impostazioni specifiche consentite in Microsoft Edge.

- Assicurarsi che tutti i file, gli script e i collegamenti siano nel sistema locale. Per altre informazioni, inclusi gli altri requisiti di Windows, vedere [Personalizzare ed esportare il layout Start](/windows/configuration/customize-and-export-start-layout).

> [!IMPORTANT]
> Assicurarsi di assegnare questo profilo per la modalità tutto schermo agli stessi dispositivi del [profilo di Microsoft Edge](device-restrictions-windows-10.md#microsoft-edge-browser).

## <a name="single-app-full-screen-kiosk"></a>App singola per chiosco multimediale a schermo intero

Eseguire una sola app nel dispositivo.

- **Selezionare una modalità tutto schermo**: scegliere **Single app, full-screen kiosk (App singola per chiosco multimediale a schermo intero)** .

- **Tipo di accesso utente**: selezionare il tipo di account che esegue l'app. Le opzioni disponibili sono:

  - **Accesso automatico (Windows 10, versione 1803 e successive)** : da usare per i dispositivi in modalità tutto schermo in ambienti pubblici che non richiedono all'utente di eseguire l'accesso, in modo simile a un account guest. Questa impostazione usa il [provider di servizi di configurazione AssignedAccess](/windows/client-management/mdm/assignedaccess-csp).
  - **Account utente locale**: immettere l'account utente locale (per il dispositivo). L'account immesso accede al chiosco multimediale.

- **Tipo di applicazione**: selezionare il tipo di applicazione. Le opzioni disponibili sono:

  - **Aggiungi il browser Microsoft Edge**: selezionare **Browser Microsoft Edge** e scegliere il **Tipo di modalità tutto schermo di Microsoft Edge**:

    - **Insegna digitale o schermo interattivo**: apre un URL a schermo intero e visualizza solo il contenuto di tale sito Web. [Set up digital signs](/windows/configuration/setup-digital-signage) (Configurare insegne digitali) offre altre informazioni su questa funzionalità.
    - **Esplorazione pubblica (InPrivate)** : esegue una versione a schede multiple limitata di Microsoft Edge. Gli utenti possono esplorare pubblicamente o terminare la sessione di esplorazione.

    Per altre informazioni su queste opzioni, vedere [Distribuire la modalità tutto schermo di Microsoft Edge](/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-configuration-types).

    > [!NOTE]
    > Questa impostazione abilita il browser Microsoft Edge nel dispositivo. Per configurare le impostazioni specifiche di Microsoft Edge, creare un profilo di restrizioni del dispositivo (**Dispositivi** > **Profili di configurazione** > **Crea profilo** > **Windows 10** per la piattaforma > **Restrizioni del dispositivo** > **Browser Microsoft Edge**). In [Browser Microsoft Edge](device-restrictions-windows-10.md#microsoft-edge-browser) sono elencate e descritte le impostazioni disponibili.

  - **Aggiungi un browser in modalità tutto schermo**: selezionare **Impostazioni del browser in modalità tutto schermo**. Queste impostazioni controllano un'app Web browser in modalità tutto schermo. Assicurarsi di ottenere l'[app browser in modalità tutto schermo](https://businessstore.microsoft.com/store/details/kiosk-browser/9NGB5S5XG2KP) dallo Store e aggiungerla a Intune come [app client](../apps/apps-add.md). Assegnare quindi l'app ai dispositivi in modalità tutto schermo.

    Immettere le impostazioni seguenti:

    - **URL della home page predefinita**: immettere l'URL predefinito visualizzato all'apertura o al riavvio del browser in modalità tutto schermo. Ad esempio, immettere `http://bing.com` o `http://www.contoso.com`.

    - **Pulsante Pagina iniziale**: scegliere **Mostra** o **Nascondi** per il pulsante Pagina iniziale del browser in modalità tutto schermo. Per impostazione predefinita, il pulsante non viene visualizzato.

    - **Pulsanti di spostamento**: scegliere **Mostra** o **Nascondi** per i pulsanti Avanti e Indietro. Per impostazione predefinita, i pulsanti di spostamento non sono visualizzati.

    - **Pulsante Termina sessione**: scegliere **Mostra** o **Nascondi** per il pulsante Termina sessione. Quando visualizzato, l'utente seleziona il pulsante e l'app chiede conferma della chiusura della sessione. Se confermata, il browser cancella tutti i dati di esplorazione (cookie, cache e così via) e quindi apre l'URL predefinito. Per impostazione predefinita, il pulsante non viene visualizzato.

    - **Aggiorna il browser dopo il tempo di inattività**: immettere la quantità di tempo di inattività da 1 a 1440 minuti, trascorso il quale il browser in modalità tutto schermo viene riavviato. Il tempo di inattività è il numero di minuti dopo l'ultima interazione dell'utente. Per impostazione predefinita, il valore è vuoto, ovvero non è configurato alcun timeout di inattività.

    - **Siti Web consentiti**: usare questa impostazione per consentire l'apertura di siti Web specifici. In altre parole, usare questa funzionalità per limitare o bloccare siti Web nel dispositivo. Ad esempio, è possibile consentire l'apertura di tutti i siti Web in `http://contoso.com`. Per impostazione predefinita, sono consentiti tutti i siti Web.

      Per consentire siti Web specifici, caricare un file che include un elenco dei siti Web consentiti in righe distinte. Se non si aggiunge un file, sono consentiti tutti i siti Web. Per impostazione predefinita, Intune consente tutti i sottodomini del sito Web. Ad esempio, si immette il dominio `sharepoint.com`. Intune consente automaticamente a tutti i sottodomini, ad esempio `contoso.sharepoint.com`, `my.sharepoint.com`e così via. Non immettere caratteri jolly, ad esempio l'asterisco (`*`).

      Il file di esempio sarà simile all'elenco seguente:

      `http://bing.com`  
      `https://bing.com`  
      `http://contoso.com`  
      `https://contoso.com`  
      `office.com`

    > [!NOTE]
    > I chioschi multimediali di Windows 10 con accesso automatico abilitato tramite Browser Microsoft in modalità tutto schermo devono usare una licenza offline di Microsoft Store per le aziende. Questo requisito è dovuto al fatto che l'accesso automatico usa un account utente locale senza credenziali di Azure Active Directory (AD), quindi le licenze online non vengono valutate. Per altre informazioni, vedere [Distribuire app offline](/microsoft-store/distribute-offline-apps).

  - **Aggiungi l'app dello Store**: scegliere **Aggiungi un'app dello Store** e scegliere un'app nell'elenco.

    Se l'elenco non include app, aggiungerne qualcuna seguendo la procedura in [App client](../apps/apps-add.md).

- **Specificare la finestra di manutenzione per i riavvii dell'app**: È necessario riavviare alcune app per completare l'installazione degli aggiornamenti o dell'app. **Rendi obbligatorio** crea una finestra di manutenzione. Se l'app richiede un riavvio, viene riavviata durante questa finestra.

  Specificare anche:

  - **Ora di inizio della finestra di manutenzione**: selezionare la data e l'ora del giorno in cui iniziare a cercare nei client eventuali aggiornamenti dell'app che richiedono il riavvio. L'ora di avvio predefinita è mezzanotte, ovvero zero minuti. Se il campo è vuoto, le app vengono riavviate dopo 3 giorni non pianificati dopo l'installazione di un aggiornamento dell'app.

  - **Ricorrenza della finestra di manutenzione**: il valore predefinito è ogni giorno. Selezionare la frequenza con cui vengono applicate le finestre di manutenzione per gli aggiornamenti dell'app. Per evitare riavvii dell'app non pianificati, è consigliabile **Giornaliera**.

  Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.

  [ApplicationManagement/ScheduleForceRestartForUpdateFailures CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-scheduleforcerestartforupdatefailures)

## <a name="multi-app-kiosk"></a>Più app in modalità tutto schermo

Le app in questa modalità sono disponibili nel menu Start. Sono le uniche app che l'utente può aprire. Se un'app presenta una dipendenza da un'altra app, entrambe devono essere incluse nell'elenco delle app consentite. Ad esempio, Internet Explorer a 64 bit ha una dipendenza da Internet Explorer a 32 bit, quindi è necessario consentire sia "C:\Programmi\internet explorer\iexplore.exe" che "C:\Programmi (x86)\Internet Explorer\iexplore.exe". 

- **Selezionare una modalità tutto schermo**: selezionare **Più app in modalità tutto schermo**.

- **Specifica Windows 10 come destinazione nei dispositivi in modalità S**:
  - **Sì**: consente le app dello Store e le app AUMID nel profilo in modalità tutto schermo. Esclude le app Win32.
  - **No**: consente le app dello Store, le app Win32 e le app AUMID nel profilo in modalità tutto schermo. Questo profilo per la modalità tutto schermo non viene distribuito nei dispositivi in modalità S.

- **Tipo di accesso utente**: selezionare il tipo di account che esegue le app. Le opzioni disponibili sono:

  - **Accesso automatico (Windows 10, versione 1803+)** : da usare per i dispositivi in modalità tutto schermo in ambienti pubblici che non richiedono all'utente di eseguire l'accesso, in modo simile a un account guest. Questa impostazione usa il [provider di servizi di configurazione AssignedAccess](/windows/client-management/mdm/assignedaccess-csp).
  - **Account utente locale**: scegliere **Aggiungi** per l'account utente locale (per il dispositivo). L'account immesso accede al chiosco multimediale.
  - **Utente o gruppo di Azure AD (Windows 10, versione 1803+)** : Selezionare **Aggiungi** e scegliere utenti o gruppi di Azure AD nell'elenco. È possibile selezionare più utenti e gruppi. Scegliere **OK** per salvare le modifiche.
  - **Visitatore di HoloLens**: l'account del visitatore è un account Guest che non richiede credenziali utente o autenticazione, come descritto in [Concetti della modalità PC condiviso](/windows/configuration/set-up-shared-or-guest-pc#shared-pc-mode-concepts).

- **Browser e applicazioni**: aggiungere le app da eseguire nel dispositivo in modalità tutto schermo. Ricordarsi che è possibile aggiungere più app.

  :::image type="content" source="./media/kiosk-settings-windows/multi-app-kiosk-add-applications-browser.png" alt-text="Aggiungere browser o app a un profilo con più app in modalità tutto schermo in Microsoft Intune.":::  

  - **Browser**

    - **Aggiungi Microsoft Edge**: Microsoft Edge viene aggiunto alla griglia delle app e tutte le applicazioni possono essere eseguite in questo chiosco multimediale. Selezionare il **Tipo di modalità tutto schermo di Microsoft Edge**:

      - **Modalità normale (versione completa di Microsoft Edge)** : Esegue una versione completa di Microsoft Edge con tutte le funzionalità di esplorazione. I dati dell'utente e lo stato vengono salvati tra le sessioni.
      - **Esplorazione pubblica (InPrivate)** : esegue una versione con più schede di Microsoft Edge InPrivate con un'esperienza personalizzata per i chioschi multimediali eseguiti in modalità schermo intero.

      Per altre informazioni su queste opzioni, vedere [Distribuire la modalità tutto schermo di Microsoft Edge](/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-configuration-types).

      > [!NOTE]
      > Questa impostazione abilita il browser Microsoft Edge nel dispositivo. Per configurare le impostazioni specifiche di Microsoft Edge, creare un profilo di restrizioni del dispositivo (**Dispositivi** > **Profili di configurazione** > **Crea profilo** > > **Windows 10** per la piattaforma > **Restrizioni del dispositivo** >  **Browser Microsoft Edge**). In [Browser Microsoft Edge](device-restrictions-windows-10.md#microsoft-edge-browser) sono elencate e descritte le impostazioni disponibili.

    - **Aggiungi un browser in modalità tutto schermo**: Queste impostazioni controllano un'app Web browser in modalità tutto schermo. Assicurarsi di distribuire un'app Web browser ai dispositivi in modalità tutto schermo usando [App client](../apps/apps-add.md).

      Immettere le impostazioni seguenti:

      - **URL della home page predefinita**: immettere l'URL predefinito visualizzato all'apertura o al riavvio del browser in modalità tutto schermo. Ad esempio, immettere `http://bing.com` o `http://www.contoso.com`.

      - **Pulsante Pagina iniziale**: scegliere **Mostra** o **Nascondi** per il pulsante Pagina iniziale del browser in modalità tutto schermo. Per impostazione predefinita, il pulsante non viene visualizzato.

      - **Pulsanti di spostamento**: scegliere **Mostra** o **Nascondi** per i pulsanti Avanti e Indietro. Per impostazione predefinita, i pulsanti di spostamento non sono visualizzati.

      - **Pulsante Termina sessione**: scegliere **Mostra** o **Nascondi** per il pulsante Termina sessione. Quando visualizzato, l'utente seleziona il pulsante e l'app chiede conferma della chiusura della sessione. Se confermata, il browser cancella tutti i dati di esplorazione (cookie, cache e così via) e quindi apre l'URL predefinito. Per impostazione predefinita, il pulsante non viene visualizzato.

      - **Aggiorna il browser dopo il tempo di inattività**: immettere la quantità di tempo di inattività (da 1 a 1440 minuti) trascorso il quale il browser in modalità tutto schermo viene riavviato. Il tempo di inattività è il numero di minuti dopo l'ultima interazione dell'utente. Per impostazione predefinita, il valore è vuoto, ovvero non è configurato alcun timeout di inattività.

      - **Siti Web consentiti**: usare questa impostazione per consentire l'apertura di siti Web specifici. In altre parole, usare questa funzionalità per limitare o bloccare siti Web nel dispositivo. Ad esempio, è possibile consentire l'apertura di tutti i siti Web in `contoso.com*`. Per impostazione predefinita, sono consentiti tutti i siti Web.

        Per consentire siti Web specifici, caricare un file CSV che include un elenco dei siti Web consentiti. Se non si aggiunge un file CSV, sono consentiti tutti i siti Web.

      > [!NOTE]
      > I chioschi multimediali di Windows 10 con accesso automatico abilitato tramite Browser Microsoft in modalità tutto schermo devono usare una licenza offline di Microsoft Store per le aziende. Questo requisito è dovuto al fatto che l'accesso automatico usa un account utente locale senza credenziali di Azure Active Directory (AD), quindi le licenze online non vengono valutate. Per altre informazioni, vedere [Distribuire app offline](/microsoft-store/distribute-offline-apps).

  - **Applicazioni**

    - **Aggiungi l'app dello Store**: aggiungere un'app da Microsoft Store per le aziende. Se l'elenco non include alcuna app, è possibile ottenerle e [aggiungerle a Intune](../apps/store-apps-windows.md). Ad esempio, è possibile aggiungere un browser in modalità tutto schermo, Excel, OneNote e altro ancora.

    - **Aggiungi un'app di Win32**: un'app Win32 è un'app desktop tradizionale, ad esempio Visual Studio Code o Google Chrome. Immettere le proprietà seguenti:

      - **Nome applicazione**: Obbligatorio. Immettere un nome per l'applicazione.
      - **Percorso locale per il file eseguibile dell'app**: Obbligatorio. Immettere il percorso del file eseguibile, ad esempio `C:\Program Files (x86)\Microsoft VS Code\Code.exe` o `C:\Program Files (x86)\Google\Chrome\Application\chrome.exe`.
      - **ID modello utente applicazione (AUMID)per l'app Win32**: Immettere l'ID modello utente applicazione (AUMID) dell'app Win32. Questa impostazione determina il layout iniziale del riquadro sul desktop. Per ottenere questo ID, vedere [Get-StartApps](/powershell/module/startlayout/get-startapps?view=win10-ps).

    - **Aggiungi in base all'ID modello utente applicazione**: usare questa opzione per aggiungere app predefinite di Windows come il Blocco note o la Calcolatrice. Immettere le proprietà seguenti:

      - **Nome applicazione**: Obbligatorio. Immettere un nome per l'applicazione.
      - **ID modello utente applicazione (AUMID)** : Obbligatorio. Immettere l'ID modello utente applicazione (AUMID) dell'app Windows. Per ottenere questo ID, vedere [Find the Application User Model ID of an installed app](/windows-hardware/customize/enterprise/find-the-application-user-model-id-of-an-installed-app) (Trovare l'ID modello utente dell'applicazione di un'app installata) per ottenere l'ID.

    - **AutoLaunch**: Facoltativo. Dopo aver aggiunto le app e il browser, selezionare un'app o un browser per aprirlo automaticamente quando l'utente accede. È possibile configurare una sola app o browser per l'avvio automatico.
    - **Dimensioni del riquadro**: Obbligatorio. Dopo aver aggiunto le app, selezionare una dimensione Piccola, Media, Larga o Grande del riquadro dell'app.

      :::image type="content" source="./media/kiosk-settings-windows/multi-app-kiosk-autolaunch-tiles.png" alt-text="Avviare automaticamente l'app o il browser e selezionare le dimensioni del riquadro in un profilo con più app in modalità tutto schermo in Microsoft Intune.":::

  > [!TIP]
  > Dopo aver aggiunto tutte le app, è possibile modificarne l'ordine di visualizzazione facendo clic e trascinando le app nell'elenco.  

- **Usa un layout Start alternativo**: selezionare **Sì** per immettere un file XML che descrive come le app vengono visualizzate nel menu Start, incluso il relativo ordine. Usare questa opzione se è necessaria una maggiore personalizzazione nel menu Start. Leggere [Personalizzare ed esportare il layout della schermata Start](/windows/configuration/customize-and-export-start-layout) per conoscere alcune linee guida e XML di esempio.

- **Barra delle applicazioni di Windows**: scegliere **Mostra** o **Nascondi** per la barra delle applicazioni. Per impostazione predefinita, la barra delle applicazioni non viene visualizzata. Vengono visualizzate delle icone, ad esempio l'icona del Wi-Fi, ma le impostazioni non possono essere modificate dagli utenti finali.

- **Consenti l'accesso alla cartella Download**: scegliere **Sì** per consentire agli utenti di accedere alla cartella Download in Esplora risorse. Per impostazione predefinita, l'accesso alla cartella Download è disabilitato. Questa funzionalità viene usata comunemente per consentire agli utenti finali di accedere agli elementi scaricati da un browser.

- **Specificare la finestra di manutenzione per i riavvii dell'app**: È necessario riavviare alcune app per completare l'installazione degli aggiornamenti o dell'app. **Rendi obbligatorio** crea una finestra di manutenzione. Se le app richiedono un riavvio, vengono riavviate durante questa finestra.

  Specificare anche:

  - **Ora di inizio della finestra di manutenzione**: selezionare la data e l'ora del giorno in cui iniziare a cercare nei client eventuali aggiornamenti dell'app che richiedono il riavvio. L'ora di avvio predefinita è mezzanotte, ovvero zero minuti. Se il campo è vuoto, le app vengono riavviate dopo 3 giorni non pianificati dopo l'installazione di un aggiornamento dell'app.

  - **Ricorrenza della finestra di manutenzione**: il valore predefinito è ogni giorno. Selezionare la frequenza con cui vengono applicate le finestre di manutenzione per gli aggiornamenti dell'app. Per evitare riavvii dell'app non pianificati, è consigliabile **Giornaliera**.

  Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.

  [ApplicationManagement/ScheduleForceRestartForUpdateFailures CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-scheduleforcerestartforupdatefailures)

## <a name="next-steps"></a>Passaggi successivi

[Assegnare il profilo](device-profile-assign.md) e [monitorarne lo stato](device-profile-monitor.md).

È anche possibile creare profili in modalità tutto schermo per dispositivi [Android](device-restrictions-android.md#kiosk), [Android Enterprise](device-restrictions-android-for-work.md#device-experience) e [Windows Holographic for Business](kiosk-settings-holographic.md).

Vedere anche [Configurare un'app singola in modalità tutto schermo](/windows/configuration/kiosk-single-app) o [Configurare più app in modalità tutto schermo](/windows/configuration/lock-down-windows-10-to-specific-apps) nella documentazione di Windows.