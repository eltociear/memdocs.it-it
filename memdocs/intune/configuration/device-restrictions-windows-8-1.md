---
title: Impostazioni relative alle restrizioni dei dispositivi Windows 8.1 in Microsoft Intune - Azure | Microsoft Docs
titleSuffix: ''
description: Informazioni relative alle opzioni di Intune per il controllo delle impostazioni e funzionalità nei dispositivi che eseguono Windows 8.1.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 36a74e503f15fe982eeaf1addfed40d0c599cb2c
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556235"
---
# <a name="microsoft-intune-windows-81-device-restriction-settings"></a>Impostazioni relative alle restrizioni dei dispositivi Windows 8.1 in Microsoft Intune

Questo articolo illustra le impostazioni relative alle restrizioni dei dispositivi di Microsoft Intune configurabili per i dispositivi che eseguono Windows 8.1.

## <a name="before-you-begin"></a>Prima di iniziare

[Creare un profilo di configurazione delle restrizioni del dispositivo Windows 8.1](device-restrictions-configure.md#create-the-profile).

## <a name="general"></a>Generale

- **Condividi i dati di utilizzo**: **Blocca** impedisce ai dispositivi di inviare dati di telemetria per diagnostica e utilizzo a Microsoft. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.
- **Firewall**: con **Rendi obbligatorio** viene richiesta l'attivazione di Windows Firewall. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.
- **Controllo dell'account utente**: configura Controllo dell'account utente. Scegliere la modalità di notifica agli utenti delle modifiche nei dispositivi. Le opzioni disponibili sono:
  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione.
  - **Notifica sempre**
  - **Notifica in caso di modifiche dell'app**
  - **Notifica in caso di modifiche dell'app (ma non attenuare il desktop)**
  - **Non inviare mai una notifica**

## <a name="password"></a>Password

- **Tipo di password richiesto**: scegliere se l'utente deve immettere una password per accedere al dispositivo. Le opzioni disponibili sono:
  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione.
  - **Alfanumerica**: la password deve essere composta da una combinazione di lettere e numeri.
  - **Numerica**: la password deve essere composta solo da numeri.
- **Lunghezza minima password**: immettere il numero minimo di caratteri necessari, da 6 a 16. Ad esempio, immettere `6` per richiedere una lunghezza della password di minimo sei numeri o caratteri.
- **Numero di errori di accesso prima della cancellazione dei dati del dispositivo**: immettere il numero di password non corrette consentite prima che il dispositivo venga cancellato, da 1 a 14.
- **Numero massimo di minuti di inattività fino al blocco dello schermo (in minuti)** : immettere il periodo di tempo per cui un dispositivo deve rimanere inattivo prima che lo schermo venga bloccato automaticamente, da 1 a 60 minuti. Ad esempio, immettere `5 Minutes` per bloccare il dispositivo dopo 5 minuti di inattività. Quando questa opzione è impostata su **Non configurato**, Intune non modifica o aggiorna questa impostazione.
- **Scadenza password (giorni)** : immettere il periodo di tempo in giorni dopo il quale è necessario modificare la password del dispositivo, da 1 a 255. Ad esempio, immettere `90` per impostare la scadenza della password dopo 90 giorni. Quando il valore è vuoto, Intune non modifica o aggiorna questa impostazione.
- **Impedisci riutilizzo delle password precedenti**: immettere il numero di password usate in precedenza che non è possibile usare, da 1 a 24. Ad esempio, immettere `5` in modo che gli utenti non possano definire una nuova password uguale alla password corrente o a una qualsiasi delle quattro precedenti. Quando il valore è vuoto, Intune non modifica o aggiorna questa impostazione.
- **Password grafica e PIN**: Una password grafica consente all'utente di accedere mediante movimenti su un'immagine. Un PIN consente all'utente di eseguire velocemente l'accesso con un codice di 4 cifre.

  **Blocca** impedisce l'uso di un'immagine o un PIN come password. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.

- **Crittografia**: con **Rendi obbligatorio** viene richiesta la crittografia nei dispositivi, inclusi i file. Non tutti i dispositivi supportano la crittografia. Quando questa opzione è impostata su **Non configurato**, Intune non modifica o aggiorna questa impostazione.

  Per configurare questa impostazione e segnalare correttamente la conformità, configurare anche:

  - **Tipo di password richiesto**: impostare almeno **Numerico**.
  - **Lunghezza minima password**: impostare almeno `6`.

  Per applicare la crittografia su dispositivi che eseguono Windows 8.1, è necessario installare il [dicembre 2014 MDM aggiornamento del client per Windows](https://support.microsoft.com/kb/3013816) su ogni dispositivo.

  Se si abilita questa impostazione per i dispositivi Windows 8.1, tutti gli utenti del dispositivo devono avere un account Microsoft.

  Perché la crittografia funzioni, i dispositivi devono soddisfare i requisiti di certificazione hardware di [Microsoft InstantGo](https://blogs.windows.com/windowsexperience/2014/06/19/instantgo-a-better-way-to-sleep/#IBHULcTfI4PokO8X.97).

  Quando si applica la crittografia in un dispositivo, è possibile visualizzare la chiave di ripristino solo dall'account Microsoft dell'utente, a cui è possibile accedere dall'account OneDrive di quest'ultimo. Non è possibile recuperare questa chiave per un utente.

## <a name="browser"></a>Browser

- **Riempimento automatico**: **Blocca** impedisce agli utenti di modificare le impostazioni di completamento automatico nel browser e di popolare automaticamente i campi del modulo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire il riempimento automatico.
- **Avvisi illeciti**: **Rendi obbligatorio** mostra gli avvisi di illeciti nel browser per i siti Web potenzialmente fraudolenti. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.
- **SmartScreen per Microsoft Edge**: **Blocca** disattiva Microsoft Defender SmartScreen. SmartScreen cerca potenziali truffe di phishing e malware durante l'accesso ai siti e i download di file. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe attivare SmartScreen.
- **Consenti JavaScript**: **Blocca** impedisce l'esecuzione di script come JavaScript nel browser. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire JavaScript.
- **Popup**: **Blocca** attiva Blocco popup per impedire popup nel Web browser. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.
- **Intestazioni DNT (Do Not Track)** : **Blocca** impedisce ai dispositivi di inviare intestazioni DNT (Do Not Track) ai siti Web che richiedono informazioni di rilevamento. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.
- **Plug-in**: **Blocca** impedisce agli utenti di aggiungere plug-in in Internet Explorer. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.
- **Immissione di una singola parola nel sito Intranet**: l'immissione di una singola parola consente agli utenti di accedere a un sito Intranet immettendo una singola parola, ad esempio `hr` o `benefits`. **Blocca** impedisce questa funzionalità. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.
- **Rilevamento automatico del sito Intranet**: **Blocca** impedisce al browser di rilevare automaticamente i siti Intranet. Le regole di mapping Intranet vengono bloccate. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.
- **Livello di sicurezza Internet**: imposta il livello di sicurezza per i siti Internet. Le opzioni disponibili sono:
  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione.
  - **Alta**
  - **Medio-alta**
  - **Media**
- **Livello di sicurezza Intranet**: imposta il livello di sicurezza per i siti Intranet. Le opzioni disponibili sono:
  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione.
  - **Bassa**
  - **Medio-bassa**
  - **Media**
  - **Medio-alta**
  - **Alta**
- **Livello di sicurezza dei siti attendibili**: Configura il livello di sicurezza per l'area siti attendibili. Le opzioni disponibili sono:
  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione.
  - **Bassa**
  - **Medio-bassa**
  - **Media**
  - **Medio-alta**
  - **Alta**
- **Sicurezza elevata per siti con restrizioni**: Configura il livello di sicurezza per l'area siti con restrizioni. **Configurato** impone il livello di sicurezza alto per i siti con restrizioni. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.
- **Accesso al menu di modalità Enterprise**: **Blocca** impedisce agli utenti di accedere alle opzioni di menu della modalità Enterprise in Internet Explorer. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.

  Quando questa opzione è impostata su **Non configurato** immettere anche:

  - **Posizione report di registrazione (URL)** : immettere un percorso URL in cui accedere ai report che mostrano i siti Web con accesso in modalità Enterprise attivato.

- **Posizione dell'elenco di siti con modalità Enterprise (solo desktop)** : immettere la posizione dell'elenco di siti Web che possono essere aperti in modalità Enterprise.

## <a name="cellular"></a>Cellulare

- **Dati in roaming**: **Blocca** impedisce il roaming dei dati quando i dispositivi si trovano in una rete cellulare. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.

## <a name="cloud-and-storage"></a>Cloud e risorse di archiviazione

- **URL cartelle di lavoro**: immettere l'URL della cartella di lavoro per consentire la sincronizzazione dei documenti tra i dispositivi. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita) o viene lasciata vuota, Intune non modifica o aggiorna questa impostazione.
- **Accedi all'app Windows Mail senza un account Microsoft**: **Blocca** impedisce l'accesso all'applicazione Windows Mail senza un account Microsoft. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.

## <a name="next-steps"></a>Passaggi successivi

Creare un profilo di restrizioni del dispositivo in [Windows 10 e versioni più recenti](device-restrictions-windows-10.md).
