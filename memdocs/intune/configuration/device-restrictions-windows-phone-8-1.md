---
title: Impostazioni relative alle restrizioni dei dispositivi per Windows Phone 8.1 in Microsoft Intune
titleSuffix: ''
description: Informazioni relative alle opzioni di Intune per il controllo delle impostazioni e funzionalità nei dispositivi che eseguono Windows Phone 8.1.
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
ms.openlocfilehash: 24fd2085839df35a486fcfa4cf817944b0d19944
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556252"
---
# <a name="microsoft-intune-windows-phone-81-device-restriction-settings"></a>Impostazioni relative alle restrizioni dei dispositivi Windows Phone 8.1 in Microsoft Intune

Questo articolo illustra le impostazioni relative alle restrizioni dei dispositivi di Microsoft Intune configurabili per i dispositivi che eseguono Windows Phone 8.1.

## <a name="before-you-begin"></a>Prima di iniziare

[Creare profilo di restrizioni dei dispositivi Windows Phone 8.1](device-restrictions-configure.md).

## <a name="general"></a>Generale

- **Fotocamera**: **Blocca** impedisce l'accesso alla fotocamera nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.

  Intune gestisce solo l'accesso alla fotocamera del dispositivo. Non ha accesso alle immagini o ai video.

- **Copia e Incolla**: **Blocca** impedisce di eseguire operazioni Copia e Incolla tra app nel dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.
- **Archivi rimovibili**: **Blocca** impedisce l'uso di dispositivi di archiviazione esterni nei dispositivi, ad esempio schede SD. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.
- **Georilevazione**: **Blocca** impedisce l'attivazione dei servizi di posizione nei dispositivi. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.
- **Account Microsoft**: **Blocca** impedisce agli utenti di associare un account Microsoft al dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.
- **Acquisizione schermo**: **Blocca** impedisce di ottenere screenshot nei dispositivi. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.
- **Invio di dati di diagnostica**: **Blocca** impedisce ai dispositivi di inviare dati di telemetria per la diagnostica e l'utilizzo a Microsoft. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.
- **Sincronizzazione degli account di posta elettronica personalizzati**: **Blocca** impedisce la connessione dei dispositivi ad account di posta elettronica non Microsoft. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.

## <a name="password"></a>Password

- **Password**: **Rendi obbligatorio** richiede agli utenti di immettere una password per accedere ai dispositivi. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Si applica solo agli account locali. Le password dell'account di dominio restano configurate da Active Directory (AD) e Azure AD.
  - **Tipo di password richiesto**: scegliere il tipo di password. Le opzioni disponibili sono:
    - **Impostazione predefinita dispositivo**: la password può includere lettere e numeri.
    - **Alfanumerica**: la password deve essere composta da una combinazione di lettere e numeri.
    - **Numerica**: la password deve essere composta solo da numeri.
  - **Lunghezza minima password**: immettere il numero minimo di caratteri necessari, da 4 a 16. Ad esempio, immettere `6` per richiedere una lunghezza della password di minimo sei caratteri.
  - **Password semplici**: **Blocca** impedisce agli utenti di creare password semplici, ad esempio `1234` o `1111`. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.
  - **Numero di errori di accesso prima della cancellazione dei dati del dispositivo**: immettere il numero di password non corrette consentite prima che i dispositivi vengano cancellati.
  - **Numero massimo di minuti di inattività fino al blocco dello schermo**: immettere il periodo di tempo per cui un dispositivo deve rimanere inattivo prima che lo schermo venga bloccato automaticamente. Ad esempio, immettere `5` per bloccare i dispositivi dopo 5 minuti di inattività. Quando questa opzione è impostata su **Non configurato** o lasciata vuota, Intune non modifica o aggiorna questa impostazione.
  - **Scadenza password (giorni)** : immettere il periodo di tempo in giorni dopo il quale è necessario modificare la password del dispositivo, da 1 a 255. Ad esempio, immettere `90` per impostare la scadenza della password dopo 90 giorni. Quando il valore è vuoto, Intune non modifica o aggiorna questa impostazione.
  - **Impedisci riutilizzo delle password precedenti**: immettere il numero di password usate in precedenza che non è possibile usare, da 1 a 24. Ad esempio, immettere `5` in modo che gli utenti non possano definire una nuova password uguale alla password corrente o a una qualsiasi delle quattro precedenti. Quando il valore è vuoto, Intune non modifica o aggiorna questa impostazione.
- **Crittografia**: con **Rendi obbligatorio** viene richiesta la crittografia nel dispositivo, inclusi i file. Non tutti i dispositivi supportano la crittografia. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per configurare questa impostazione e segnalare correttamente la conformità, configurare anche:
  - **Richiedi password**: impostare su **Rendi obbligatorio**.
  - **Tipo di password richiesto**: impostare almeno **Numerico**.
  - **Lunghezza minima password**: impostare almeno `4`.

## <a name="app-store"></a>App Store

- **App Store**: **Blocca** impedisce agli utenti di accedere all'App Store. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.

## <a name="restricted-apps"></a>App con restrizioni

Nell'elenco delle app con restrizioni è possibile configurare uno degli elenchi seguenti:

- **App bloccate**: Elencare le app non gestite da Intune che gli utenti non sono autorizzati a installare ed eseguire.
- **App consentite**: Elencare le app che gli utenti sono autorizzati a installare. Le app gestite da Intune sono automaticamente consentite.

Per configurare un elenco, fare clic su **Aggiungi** e quindi specificare il nome, facoltativamente l'autore dell'app e l'URL dell'app nell'App Store.

### <a name="how-to-specify-the-url-to-an-app-in-the-store"></a>Come specificare l'URL di un'app nello store

Per specificare un URL app nell'elenco di app consentite e bloccate, usare il formato seguente:

Nella pagina [Windows Phone Store](https://www.microsoft.com/store/apps/windows-phone) cercare l'applicazione che si vuole usare.

Aprire la pagina dell'app e copiare l'URL negli Appunti. A questo punto l'URL può essere usato in entrambi gli elenchi di app consentite o bloccate.

Esempio: cercare l'app Skype in Store. L'URL usato è `http://www.windowsphone.com/store/app/skype/c3f8e570-68b3-4d6a-bdbb-c0a3f4360a51`.

### <a name="additional-options"></a>Opzioni aggiuntive

È possibile anche fare clic su **Importa** per popolare l'elenco da un file CSV nel formato <*url app*>, <*nome app*>, <*autore app*> o fare clic su **Esporta** per creare un file CSV che abbia come contenuto l'elenco delle app con restrizioni nello stesso formato.

## <a name="browser"></a>Browser

- **Web browser**: **Blocca** disattiva il Web browser incorporato nei dispositivi. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.

## <a name="cellular-and-connectivity"></a>Rete cellulare e connettività

- **Wi-Fi**: **Blocca** disabilita la funzionalità Wi-Fi nei dispositivi. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.
- **Tethering Wi-Fi**: **Blocca** impedisce l'uso del tethering Wi-Fi nei dispositivi. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.
- **Connetti automaticamente a hotspot Wi-Fi**: consente ai dispositivi di connettersi automaticamente agli hotspot Wi-Fi gratuiti e accettare automaticamente le condizioni per l'uso.
- **Reporting hotspot Wi-Fi**: **Blocca** impedisce ai dispositivi di inviare informazioni di connessione hotspot Wi-Fi. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.
- **NFC**: **Blocca** disabilita le operazioni che usano NFC (Near Field Communication) nei dispositivi che la supportano. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.
- **Bluetooth**: **Blocca** impedisce agli utenti di abilitare Bluetooth. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.

## <a name="next-steps"></a>Passaggi successivi

Per una panoramica generale del profilo delle restrizioni dei dispositivi, vedere [Configurare le impostazioni relative alle restrizioni dei dispositivi in Microsoft Intune](device-restrictions-configure.md).
