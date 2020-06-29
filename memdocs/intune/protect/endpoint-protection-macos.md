---
title: Configurare la protezione degli endpoint nei dispositivi macOS con Microsoft Intune | Microsoft Docs
description: Usare Intune per configurare i dispositivi macOS per l'uso del firewall integrato per consentire o bloccare app specifiche o per usare la modalità mascheramento, per usare Gatekeeper per determinare dove installare le app e per usare la crittografia del disco FileVault.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/19/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 506bb4672b84423204df5fce1401748ffbce0484
ms.sourcegitcommit: 3217778ebe7fd0318810696e8931e427a85da897
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/19/2020
ms.locfileid: "85107504"
---
# <a name="macos-endpoint-protection-settings-in-intune"></a>Impostazioni di Endpoint Protection per macOS in Intune

Questo articolo illustra le impostazioni di Endpoint Protection configurabili per i dispositivi che eseguono macOS. È possibile configurare queste impostazioni usando un profilo di configurazione di dispositivi macOS per [Endpoint Protection](endpoint-protection-configure.md) in Intune.

## <a name="before-you-begin"></a>Prima di iniziare

[Creare un profilo di Endpoint Protection macOS](endpoint-protection-configure.md).

## <a name="firewall"></a>Firewall

Usare il firewall per controllare le connessioni per ogni singola applicazione, anziché per ogni porta. L'uso delle impostazioni in base alle singole applicazione rende più facile sfruttare i vantaggi di protezione mediante firewall. Contribuisce, inoltre, a impedire che app indesiderate assumano il controllo delle porte di rete aperte per app legittime.

- **Abilita il firewall**

  Attivare l'uso del firewall in macOS e quindi configurare la modalità di gestione delle connessioni in ingresso nell'ambiente.

  - **Non configurato** (*impostazione predefinita*)
  - **Sì**

- **Bloccare tutte le connessioni in ingresso**

  Bloccare tutte le connessioni in ingresso tranne le connessioni necessarie per i servizi Internet di base, ad esempio DHCP, Bonjour e IPSec. Questa opzione blocca anche tutti i servizi di condivisione, ad esempio Condivisione file e Condivisione schermo. Se si utilizzano servizi di condivisione, mantenere questa impostazione come *Non configurato*.

  - **Non configurato** (*impostazione predefinita*)
  - **Sì**

  Quando si imposta *Bloccare tutte le connessioni in ingresso* su *Non configurato*, è quindi possibile configurare le app che possono o non possono ricevere connessioni in ingresso.

  **App consentite**: configurare un elenco di app autorizzate alla ricezione di connessioni in ingresso.

  - **Aggiungi app per ID pacchetto**: immettere l'[ID aggregazione](../configuration/bundle-ids-built-in-ios-apps.md) dell'app. Il sito Web di Apple include un elenco di [app Apple predefinite](https://support.apple.com/HT208094).
  - **Aggiungi l'app dello Store**: Selezionare un'app dello store aggiunta in precedenza a Intune. Per altre informazioni, vedere [Aggiungere app a Microsoft Intune](../apps/apps-add.md).

  **App bloccate**: configurare un elenco di app in cui le connessioni in ingresso sono bloccate.

  - **Aggiungi app per ID pacchetto**: immettere l'[ID aggregazione](../configuration/bundle-ids-built-in-ios-apps.md) dell'app. Il sito Web di Apple include un elenco di [app Apple predefinite](https://support.apple.com/HT208094).
  - **Aggiungi l'app dello Store**: Selezionare un'app dello store aggiunta in precedenza a Intune. Per altre informazioni, vedere [Aggiungere app a Microsoft Intune](../apps/apps-add.md).

- **Abilita la modalità mascheramento**

  Abilitare questa modalità per impedire che il computer risponde alle richieste di probe. Il dispositivo continua a rispondere alle richieste in ingresso provenienti da applicazioni autorizzate. Le richieste impreviste, ad esempio le richieste ICMP (ping), vengono ignorate.

  - **Non configurato** (*impostazione predefinita*)
  - **Sì**

## <a name="gatekeeper"></a>Gatekeeper

- **Consenti le app scaricate da queste posizioni**

  Limitare le app che possono essere avviate da un dispositivo a seconda della posizione da cui sono state scaricate. L'obiettivo è proteggere i dispositivi da malware e consentire solo le app da origini attendibili.

  - **Non configurato** (*impostazione predefinita*)
  - **Mac App Store**
  - **Mac App Store e sviluppatori identificati**
  - **Ovunque**

- **Non consentire all'utente di eseguire l'override di Gatekeeper**

  Impedisce agli utenti di eseguire l'override dell'impostazione Gatekeeper e usare CTRL+clic per installare un'app. Quando è abilitata, gli utenti possono usare Clic+CTRL per installare qualsiasi app.

  - **Non configurato** (*impostazione predefinita*) - Gli utenti possono usare Clic+CTRL per installare le app.
  - **Sì** - Impedisce agli utenti di usare Clic+CTRL per installare le app.

## <a name="filevault"></a>FileVault

Per altre informazioni sulle impostazioni di Apple FileVault, vedere [FDEFileVault](https://developer.apple.com/documentation/devicemanagement/fdefilevault) nei contenuti per sviluppatori Apple.

> [!IMPORTANT]
> A partire da macOS 10,15, la configurazione di FileVault richiede la registrazione MDM approvata dall'utente.

- **Abilita FileVault**  

  È possibile *abilitare* la crittografia del disco completo usando XTS-AES 128 con FileVault nei dispositivi che eseguono macOS 10.13 o versione successiva.

  - **Non configurato** (*impostazione predefinita*)
  - **Sì**

  Quando l'opzione *Abilita FileVault* è impostata su *Sì*, è possibile configurare le impostazioni seguenti:

  - **Tipo di chiave di ripristino**

    Le chiavi di ripristino create per i dispositivi sono di tipo *chiave personale*. Configurare le impostazioni seguenti per la chiave personale.

  - **Descrizione della posizione del deposito della chiave di ripristino personale**

    Specificare un breve messaggio per l'utente per spiegare come e dove può recuperare la chiave di ripristino personale. Il testo digitato viene inserito nel messaggio visualizzato nella schermata di accesso quando all'utente viene richiesto di immettere la chiave di ripristino personale nel caso in cui abbia dimenticato la password.

  - **Rotazione della chiave di ripristino personale**

    Consente di specificare la frequenza con cui verrà eseguita la rotazione della chiave di ripristino personale per un dispositivo. È possibile selezionare il valore predefinito **Non configurato** oppure un valore compreso tra **1** e **12** mesi.

  - **Nascondi la chiave di ripristino**

    Scegliere di nascondere la chiave personale da un utente del dispositivo durante la crittografia FileVault 2.

    - **Non configurato** (*impostazione predefinita*) - La chiave personale è visibile all'utente del dispositivo durante la crittografia.
    - **Sì** - La chiave personale è nascosta dall'utente del dispositivo durante la crittografia.

    Dopo la crittografia, gli utenti del dispositivo possono visualizzare la chiave di ripristino personale per un dispositivo macOS crittografato dalle posizioni seguenti:
    - App Portale aziendale iOS/iPadOS
    - App Intune
    - Sito Web del portale aziendale
    - App del portale aziendale Android

    Per visualizzare la chiave, dall'app o dal sito Web, passare ai dettagli del dispositivo macOS crittografato e selezionare *Ottieni la chiave di ripristino*.

  - **Disabilita la richiesta alla disconnessione**

    Consente di impedire che all'utente venga richiesta l'abilitazione di FileVault al momento della disconnessione.  Se questo parametro è impostato su Disabilita, la richiesta non viene visualizzata al momento della disconnessione ma in fase di accesso.

    - **Non configurato** (*impostazione predefinita*)
    - **Sì** - Disabilita la richiesta alla disconnessione.

  - **Numero di volte per cui è consentito ignorare**

    Consente di impostare il numero di volte per cui un utente può ignorare le richieste di abilitazione di FileVault prima che FileVault venga reso obbligatorio per l'accesso dell'utente.

    - **Non configurato** - Viene richiesta la crittografia del dispositivo prima che sia consentito l'accesso successivo.
    - **0** - Consente di richiedere la crittografia ai dispositivi all'accesso successivo da parte dell'utente.
    - Da **1** a **10** - Consente a un utente di ignorare la richiesta per un numero di volte compreso tra 1 e 10 prima che venga richiesta la crittografia nel dispositivo.
    - **Nessun limite, richiedi sempre** - All'utente viene richiesto di abilitare FileVault, ma non viene mai richiesta la crittografia.

    Il valore predefinito per questa impostazione dipende dalla configurazione di *Disabilita la richiesta alla disconnessione*. Se il parametro *Disabilita la richiesta alla disconnessione* è impostato su **Non configurato**, l'impostazione predefinita è **Non configurato**. Se *Disabilita la richiesta alla disconnessione* è impostato su **Sì**, l'impostazione predefinita è **1** e il valore **Non configurato** non è disponibile.

## <a name="next-steps"></a>Passaggi successivi

[Assegnare il profilo](../configuration/device-profile-assign.md) e [monitorarne lo stato](../configuration/device-profile-monitor.md).

È anche possibile configurare Endpoint Protection in [dispositivi Windows 10 e versioni successive](endpoint-protection-windows-10.md).
