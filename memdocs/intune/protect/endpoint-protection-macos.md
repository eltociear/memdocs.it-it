---
title: Aggiungere Endpoint Protection su macOS in Microsoft Intune - Azure | Documenti Microsoft
description: Nei dispositivi macOS utilizzare il gatekeeper per determinare dove è possibile installare le app, incluso il Mac App Store. Inoltre, abilitare o configurare un firewall per autorizzare app specifiche, bloccare app specifiche, utilizzare la modalità mascheramento e persino bloccare determinati tipi di connessioni in ingresso con Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/24/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5e857cdd7028851f14f607739ba7e37c744fa2f1
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "80359465"
---
# <a name="macos-endpoint-protection-settings-in-intune"></a>Impostazioni di Endpoint Protection per macOS in Intune  

Questo articolo illustra le impostazioni di Endpoint Protection configurabili per i dispositivi che eseguono macOS. È possibile configurare queste impostazioni usando un profilo di configurazione di dispositivi macOS per [Endpoint Protection](endpoint-protection-configure.md) in Intune.  

## <a name="before-you-begin"></a>Prima di iniziare

[Creare un profilo di Endpoint Protection macOS](endpoint-protection-configure.md).

## <a name="gatekeeper"></a>Gatekeeper  

- **Consenti le app scaricate da queste posizioni**  
  Limitare le app che possono essere avviate da un dispositivo a seconda della posizione da cui sono state scaricate. L'obiettivo è proteggere i dispositivi da malware e consentire solo le app da origini attendibili.  

  - **Non configurato**  
  - **Mac App Store**  
  - **Mac App Store e sviluppatori identificati**  
  - **Ovunque**  

  **Impostazione predefinita**: Non configurato  

- **L'utente può eseguire l'override di Gatekeeper**  
  Impedisce agli utenti di eseguire l'override dell'impostazione Gatekeeper e usare CTRL+clic per installare un'app. Quando è abilitata, gli utenti possono usare Clic+CTRL per installare qualsiasi app.  
 
  - **Non configurato** - Gli utenti possono usare Clic+CTRL per installare le app.  
  - **Bloccato** - Impedisce agli utenti di usare Clic+CTRL per installare le app.  

  **Impostazione predefinita**: Non configurato  

## <a name="firewall"></a>Firewall  

Usare il firewall per controllare le connessioni per ogni singola applicazione, anziché per ogni porta. L'uso delle impostazioni in base alle singole applicazione rende più facile sfruttare i vantaggi di protezione mediante firewall. Contribuisce, inoltre, a impedire che app indesiderate assumano il controllo delle porte di rete aperte per app legittime.  

**Generalee**
- **Firewall**  
  Abilitare il firewall per configurare in che modo le connessioni in ingresso devono essere gestite nell'ambiente in uso.  
  - **Non configurato**  
  - **Attiva**  

  **Impostazione predefinita**: Non configurato  

- **Connessioni in ingresso**  
  Bloccare tutte le connessioni in ingresso tranne le connessioni necessarie per i servizi Internet di base, ad esempio DHCP, Bonjour e IPSec. Questa opzione blocca anche tutti i servizi di condivisione, ad esempio Condivisione file e Condivisione schermo. Se si utilizzano servizi di condivisione, mantenere questa impostazione come *Non configurato*.  
  - **Non configurato**  
  - **Bloccato**  

  **Impostazione predefinita**: Non configurato  

**Consentire o bloccare le connessioni in ingresso per app specifiche.**  

  - **App consentite**  
    Selezionare le app che sono esplicitamente autorizzate a ricevere connessioni in ingresso.  

  - **App bloccate**  
    Selezionare le app che devono bloccare le connessioni in ingresso.  

  - **Modalità mascheramento**  
    Abilitare questa modalità per impedire che il computer risponde alle richieste di probe. Il dispositivo continua a rispondere alle richieste in ingresso provenienti da applicazioni autorizzate. Le richieste impreviste, ad esempio le richieste ICMP (ping), vengono ignorate.  
    - **Non configurato**  
    - **Attiva**  

    **Impostazione predefinita**: Non configurato  

## <a name="filevault"></a>FileVault  
Per altre informazioni sulle impostazioni di Apple FileVault, vedere [FDEFileVault](https://developer.apple.com/documentation/devicemanagement/fdefilevault) nei contenuti per sviluppatori Apple. 

> [!IMPORTANT]  
> A partire da macOS 10,15, la configurazione di FileVault richiede la registrazione MDM approvata dall'utente. 

- **FileVault**  
  È possibile *abilitare* la crittografia del disco completo usando XTS-AES 128 con FileVault nei dispositivi che eseguono macOS 10.13 o versione successiva.  
  - **Non configurato**  
  - **Attiva**  

  **Impostazione predefinita**: Non configurato  

  - **Tipo di chiave di ripristino**  
    Le chiavi di ripristino create per i dispositivi sono di tipo *chiave personale*. Configurare le impostazioni seguenti per la chiave personale.  

    - **Percorso della chiave di ripristino personale** - Digitare un breve messaggio per l'utente per spiegare come e dove poter recuperare la chiave di ripristino personale. Il testo digitato viene inserito nel messaggio visualizzato nella schermata di accesso quando all'utente viene richiesto di immettere la chiave di ripristino personale nel caso in cui abbia dimenticato la password.  

    - **Rotazione della chiave di ripristino personale** - Consente di specificare la frequenza con cui verrà eseguita la rotazione della chiave di ripristino personale per un dispositivo. È possibile selezionare il valore predefinito **Non configurato** oppure un valore compreso tra **1** e **12** mesi.  

  - **Disabilita la richiesta alla disconnessione**  
    Consente di impedire che all'utente venga richiesta l'abilitazione di FileVault al momento della disconnessione.  Se questo parametro è impostato su Disabilita, la richiesta non viene visualizzata al momento della disconnessione ma in fase di accesso.  
    - **Non configurato**  
    - **Disabilita** - Disabilita la richiesta alla disconnessione.

    **Impostazione predefinita**: Non configurato  

  - **Numero di volte per cui è consentito ignorare**  
  Consente di impostare il numero di volte per cui un utente può ignorare le richieste di abilitazione di FileVault prima che FileVault venga reso obbligatorio per l'accesso dell'utente. 

    - **Non configurato** - Viene richiesta la crittografia del dispositivo prima che sia consentito l'accesso successivo.  
    - Da **1** a **10** - Consente a un utente di ignorare la richiesta per un numero di volte compreso tra 1 e 10 prima che venga richiesta la crittografia nel dispositivo.  
    - **Nessun limite, richiedi sempre** - All'utente viene richiesto di abilitare FileVault, ma non viene mai richiesta la crittografia.  
 
    **Impostazione predefinita**: *Variabile* - Se il parametro *Disabilita la richiesta alla disconnessione* è impostato su **Non configurato**, l'impostazione predefinita è **Non configurato**. Se *Disabilita la richiesta alla disconnessione* è impostato su **Disabilita**, l'impostazione predefinita è **1** e il valore **Non configurato** non è disponibile.

Per altre informazioni su FileVault con Intune, vedere [Chiavi di ripristino di FileVault](encryption-monitor.md#filevault-recovery-keys).

## <a name="next-steps"></a>Passaggi successivi

[Assegnare il profilo](../configuration/device-profile-assign.md) e [monitorarne lo stato](../configuration/device-profile-monitor.md).

È anche possibile configurare Endpoint Protection in [dispositivi Windows 10 e versioni successive](endpoint-protection-windows-10.md).
