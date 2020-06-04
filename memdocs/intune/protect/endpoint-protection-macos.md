---
title: Aggiungere Endpoint Protection su macOS in Microsoft Intune - Azure | Documenti Microsoft
description: Nei dispositivi macOS utilizzare il gatekeeper per determinare dove è possibile installare le app, incluso il Mac App Store. Inoltre, abilitare o configurare un firewall per autorizzare app specifiche, bloccare app specifiche, utilizzare la modalità mascheramento e persino bloccare determinati tipi di connessioni in ingresso con Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/05/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: eaca235305507065cb716e3427e52c679c1a5dad
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83427799"
---
# <a name="macos-endpoint-protection-settings-in-intune"></a>Impostazioni di Endpoint Protection per macOS in Intune  

Questo articolo illustra le impostazioni di Endpoint Protection configurabili per i dispositivi che eseguono macOS. È possibile configurare queste impostazioni usando un profilo di configurazione di dispositivi macOS per [Endpoint Protection](endpoint-protection-configure.md) in Intune.  

## <a name="before-you-begin"></a>Prima di iniziare

[Creare un profilo di Endpoint Protection macOS](endpoint-protection-configure.md).

## <a name="filevault"></a>FileVault

Per altre informazioni sulle impostazioni di Apple FileVault, vedere [FDEFileVault](https://developer.apple.com/documentation/devicemanagement/fdefilevault) nei contenuti per sviluppatori Apple. 

> [!IMPORTANT]  
> A partire da macOS 10,15, la configurazione di FileVault richiede la registrazione MDM approvata dall'utente. 

- **Abilita FileVault**  
  È possibile *abilitare* la crittografia del disco completo usando XTS-AES 128 con FileVault nei dispositivi che eseguono macOS 10.13 o versione successiva.  
  - **Non configurato**  
  - **Sì**  

  **Impostazione predefinita**: Non configurato  

  - **Tipo di chiave di ripristino**  
    Le chiavi di ripristino create per i dispositivi sono di tipo *chiave personale*. Configurare le impostazioni seguenti per la chiave personale.  

    - **Descrizione della posizione del deposito della chiave di ripristino personale** - Digitare un breve messaggio per l'utente per spiegare come e dove poter recuperare la chiave di ripristino personale. Il testo digitato viene inserito nel messaggio visualizzato nella schermata di accesso quando all'utente viene richiesto di immettere la chiave di ripristino personale nel caso in cui abbia dimenticato la password.  

    - **Rotazione della chiave di ripristino personale** - Consente di specificare la frequenza con cui verrà eseguita la rotazione della chiave di ripristino personale per un dispositivo. È possibile selezionare il valore predefinito **Non configurato** oppure un valore compreso tra **1** e **12** mesi.  

  - **Disabilita la richiesta alla disconnessione**  
    Consente di impedire che all'utente venga richiesta l'abilitazione di FileVault al momento della disconnessione.  Se questo parametro è impostato su Disabilita, la richiesta non viene visualizzata al momento della disconnessione ma in fase di accesso.  
    - **Non configurato**  
    - **Sì** - Disabilita la richiesta alla disconnessione.

    **Impostazione predefinita**: Non configurato  

  - **Numero di volte per cui è consentito ignorare**  
  Consente di impostare il numero di volte per cui un utente può ignorare le richieste di abilitazione di FileVault prima che FileVault venga reso obbligatorio per l'accesso dell'utente. 

    > [!IMPORTANT]
    >
    > Esiste un problema noto con il valore **Nessun limite, richiedi sempre**. Anziché consentire a un utente di ignorare la crittografia al momento dell'accesso, questa impostazione richiede la crittografia del dispositivo all'accesso successivo. Questo problema dovrebbe essere risolto verso la fine di giugno ed è segnalato in MC210922.
    >
    > Dopo la correzione, questa impostazione avrà una nuova opzione zero (**0**), che richiederà ai dispositivi di applicare la crittografia all'accesso successivo di un utente al dispositivo. Inoltre, con l'aggiornamento di Intune per includere questa correzione, tutti i criteri impostati su **Nessun limite, richiedi sempre** verranno aggiornati in modo da usare il nuovo valore **0**, che mantiene il comportamento corrente che prevede la richiesta della crittografia.
    >
    > Dopo la correzione di questo problema, è possibile sfruttare la possibilità di ignorare la crittografia obbligatoria riconfigurando questa impostazione per impostare **Nessun limite, richiedi sempre** perché l'impostazione funzionerà come previsto in origine e consentirà agli utenti di ignorare la crittografia del dispositivo.
    >
    > In presenza di dispositivi macOS registrati, per visualizzare altre informazioni accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), passare ad **Amministrazione tenant** > **Stato tenant**, selezionare **Integrità del servizio e Centro messaggi** e cercare il messaggio con ID **MC210922**.

    - **Non configurato** - Viene richiesta la crittografia del dispositivo prima che sia consentito l'accesso successivo.  
    - Da **1** a **10** - Consente a un utente di ignorare la richiesta per un numero di volte compreso tra 1 e 10 prima che venga richiesta la crittografia nel dispositivo.  
    - **Nessun limite, richiedi sempre** - All'utente viene richiesto di abilitare FileVault, ma non viene mai richiesta la crittografia.  
 
    **Impostazione predefinita**: *Variabile* - Se il parametro *Disabilita la richiesta alla disconnessione* è impostato su **Non configurato**, l'impostazione predefinita è **Non configurato**. Se *Disabilita la richiesta alla disconnessione* è impostato su **Disabilita**, l'impostazione predefinita è **1** e il valore **Non configurato** non è disponibile.

Per altre informazioni su FileVault con Intune, vedere [Gestire FileVault](../protect/encrypt-devices-filevault.md#manage-filevault).

## <a name="firewall"></a>Firewall  

Usare il firewall per controllare le connessioni per ogni singola applicazione, anziché per ogni porta. L'uso delle impostazioni in base alle singole applicazione rende più facile sfruttare i vantaggi di protezione mediante firewall. Contribuisce, inoltre, a impedire che app indesiderate assumano il controllo delle porte di rete aperte per app legittime.  

- **Abilita il firewall**  
  Abilitare il firewall per configurare in che modo le connessioni in ingresso devono essere gestite nell'ambiente in uso.  
  - **Non configurato**  
  - **Sì**  

  **Impostazione predefinita**: Non configurato  

- **Bloccare tutte le connessioni in ingresso**  
  Bloccare tutte le connessioni in ingresso tranne le connessioni necessarie per i servizi Internet di base, ad esempio DHCP, Bonjour e IPSec. Questa opzione blocca anche tutti i servizi di condivisione, ad esempio Condivisione file e Condivisione schermo. Se si utilizzano servizi di condivisione, mantenere questa impostazione come *Non configurato*.  
  - **Non configurato**  
  - **Sì**  

  **Impostazione predefinita**: Non configurato  

- **Consenti le connessioni in ingresso per le app seguenti**: Selezionare le app autorizzate alla ricezione di connessioni in ingresso. Le opzioni disponibili sono:
  - **Aggiungi app per ID pacchetto**: immettere l'[ID aggregazione](../configuration/bundle-ids-built-in-ios-apps.md) dell'app. Il sito Web di Apple include un elenco di [app Apple predefinite](https://support.apple.com/HT208094).
  - **Aggiungi l'app dello Store**: Selezionare un'app dello store aggiunta in precedenza a Intune. Per altre informazioni, vedere [Aggiungere app a Microsoft Intune](../apps/apps-add.md).

- **Blocca le connessioni in ingresso per le app seguenti**: Selezionare le app non autorizzate alla ricezione di connessioni in ingresso. Le opzioni disponibili sono:
  - **Aggiungi app per ID pacchetto**: immettere l'[ID aggregazione](../configuration/bundle-ids-built-in-ios-apps.md) dell'app. Il sito Web di Apple include un elenco di [app Apple predefinite](https://support.apple.com/HT208094).
  - **Aggiungi l'app dello Store**: Selezionare un'app dello store aggiunta in precedenza a Intune. Per altre informazioni, vedere [Aggiungere app a Microsoft Intune](../apps/apps-add.md).

- **Abilita la modalità mascheramento**  
  Abilitare questa modalità per impedire che il computer risponde alle richieste di probe. Il dispositivo continua a rispondere alle richieste in ingresso provenienti da applicazioni autorizzate. Le richieste impreviste, ad esempio le richieste ICMP (ping), vengono ignorate.  
  - **Non configurato**  
  - **Sì**  

  **Impostazione predefinita**: Non configurato  

## <a name="gatekeeper"></a>Gatekeeper  

- **Consenti le app scaricate da queste posizioni**  
  Limitare le app che possono essere avviate da un dispositivo a seconda della posizione da cui sono state scaricate. L'obiettivo è proteggere i dispositivi da malware e consentire solo le app da origini attendibili.  

  - **Non configurato**  
  - **Mac App Store**  
  - **Mac App Store e sviluppatori identificati**  
  - **Ovunque**  

  **Impostazione predefinita**: Non configurato  

- **Non consentire all'utente di eseguire l'override di Gatekeeper**  
  Impedisce agli utenti di eseguire l'override dell'impostazione Gatekeeper e usare CTRL+clic per installare un'app. Quando è abilitata, gli utenti possono usare Clic+CTRL per installare qualsiasi app.  

  - **Non configurato** - Gli utenti possono usare Clic+CTRL per installare le app.  
  - **Sì** - Impedisce agli utenti di usare Clic+CTRL per installare le app.  

  **Impostazione predefinita**: Non configurato  

## <a name="next-steps"></a>Passaggi successivi

[Assegnare il profilo](../configuration/device-profile-assign.md) e [monitorarne lo stato](../configuration/device-profile-monitor.md).

È anche possibile configurare Endpoint Protection in [dispositivi Windows 10 e versioni successive](endpoint-protection-windows-10.md).
