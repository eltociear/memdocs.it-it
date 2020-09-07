---
title: Requisiti delle password per dispositivi registrati in Intune | Microsoft Docs
description: Questo articolo descrive come soddisfare i requisiti dell'organizzazione per le password in modo che sia possibile accedere alla rete.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/27/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: efb3c261-1f6c-4d39-bfa4-18661f8c59c7
searchScope:
- User help
ROBOTS: ''
ms.custom: intune-enduser, contperfq1
ms.collection: ''
ms.openlocfilehash: b9bdada31e280c7fdc8a5d7a5a0a4a7ab7d36ae3
ms.sourcegitcommit: 41e6e6b7f5c2a87aaf7f23d90d0f175dd63c0579
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2020
ms.locfileid: "89057288"
---
# <a name="device-password-requirements"></a>Requisiti per le password dei dispositivi  

Se la password per il dispositivo non soddisfa i requisiti di sicurezza dell'organizzazione, si riceverà un messaggio da Portale aziendale. Lo scopo dei requisiti per le password è proteggere l'utente e i dati dell'organizzazione da accessi non autorizzati. Finché non si crea una password più sicura, potrebbe essere impedito l'accesso alla rete dell'organizzazione.  

Portale aziendale invia un messaggio per ogni requisito per le password, quindi si potrebbe ricevere più di un messaggio alla volta. Toccare un messaggio per visualizzare altri dettagli (se disponibili).  

Questo articolo elenca tutti i messaggi relativi alle password che è possibile ricevere e fornisce dettagli aggiuntivi su ogni requisito, in base alla piattaforma del sistema operativo.     

## <a name="change-password-passcode-pin"></a>Cambiare password, passcode, PIN  

In genere, per accedere alle impostazioni della password, è possibile aprire l'app delle impostazioni nel dispositivo e cercare *schermata di blocco* o *impostazioni di sicurezza*.  

Gli articoli seguenti descrivono come aggiornare la password per il dispositivo in base alla piattaforma del sistema operativo. Per ottenere le istruzioni più aggiornate per il dispositivo specifico, fare riferimento alla documentazione del produttore del dispositivo.  

- [Impostare la password del dispositivo in Windows 10](set-or-change-your-password-windows.md)  
- [Impostare il passcode del dispositivo in iOS](set-or-change-your-passcode-ios.md)  
- [Impostare il PIN o la password del dispositivo Android](set-your-pin-or-password-android.md)  


> [!IMPORTANT]
> Se la password è stata modificata per soddisfare i requisiti ma si ricevono comunque le notifiche, riavviare il dispositivo.  

Per domande specifiche sui requisiti per le password dell'organizzazione, contattare un membro del supporto IT.  

## <a name="windows-10-password-requirements"></a>Requisiti per le password in Windows 10

| Messaggio | Procedura di correzione |
|-----------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Password richiesta. | Impostare una password. L'organizzazione richiede l'immissione di una password per sbloccare il dispositivo. |
| La password è troppo breve. |  Assicurarsi che la password non contenga numeri in sequenza o ripetuti, come 1234 o 1111. |
| La password è troppo breve.| Aggiornare o impostare una password con più caratteri. L'organizzazione richiede una determinata lunghezza per la password. L'impostazione scelta può variare, ma la lunghezza minima che può essere richiesta è di 4 caratteri e quella massima è di 16. |
| La password deve contenere solo numeri. | Impostare una password che contenga solo numeri.|
| La password deve contenere solo caratteri alfanumerici. | Impostare una password che contenga una combinazione di numeri e lettere.|
| La password deve contenere caratteri complessi. | Aggiungere caratteri complessi, come numeri, lettere maiuscole e simboli come `$`, `%` e `#`. L'organizzazione richiede una combinazione di lettere, numeri e caratteri non alfanumerici per rendere più difficile l'individuazione della password.|  
| Password scaduta. | Impostare una nuova password. L'organizzazione richiede di modificare la password dopo un determinato numero di giorni. |
| La password è stata usata troppo di recente. | Scegliere una password non usata in precedenza. L'organizzazione richiede un periodo di tempo specifico prima di riutilizzare una password. |

## <a name="ios-passcode-requirements"></a>Requisiti per i passcode in iOS

| Messaggio | Procedura di correzione |
|-----------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Il passcode è obbligatorio.| Impostare un passcode. L'organizzazione richiede l'immissione di un passcode per sbloccare il dispositivo. |
| Il passcode è troppo semplice. |  Assicurarsi che il passcode non contenga numeri in sequenza o ripetuti, come 1234 o 1111. |
| Il passcode è troppo breve. | Aggiornare o impostare un passcode con più caratteri. L'organizzazione richiede una determinata lunghezza per il passcode. L'impostazione scelta può variare, ma la lunghezza minima che può essere richiesta è di 4 caratteri e quella massima è di 14. Quando si modifica il passcode, è possibile che venga visualizzato un messaggio di Apple che indica di immettere 6 o più caratteri. Questo messaggio è solo una raccomandazione del sistema Apple. Se l'organizzazione richiede solo un passcode di 4 o 5 caratteri, non è necessario immettere un passcode di 6 cifre.|  
| Il passcode deve contenere solo numeri. | Impostare un passcode che contenga solo numeri.|
| Il passcode deve contenere solo caratteri alfanumerici.| Impostare un passcode che contenga una combinazione di numeri e lettere.|
| Il passcode deve contenere caratteri non alfanumerici. | Aggiungere caratteri speciali, come `&`, `!`, `$`, `%` e `#`. L'organizzazione richiede una combinazione di lettere, numeri e caratteri non alfanumerici per rendere più difficile l'individuazione del passcode.|
| Il passcode è scaduto. | Impostare una nuova password. L'organizzazione richiede di modificare la password dopo un determinato numero di giorni. |
| Il passcode è stato usato troppo di recente.| Scegliere un passcode non usato in precedenza. L'organizzazione richiede un periodo di tempo specifico prima di riutilizzare un passcode. |
|È richiesta l'autenticazione con Touch ID o Face ID. | Configurare Touch ID o Face ID. L'organizzazione richiede di eseguire l'autenticazione con uno di questi metodi prima di usare il riempimento automatico per le password o le informazioni sulla carta di credito. | 

## <a name="macos-password-requirements"></a>Requisiti per le password macOS
| Messaggio | Procedura di correzione |
|-----------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Password richiesta. | Impostare una password. L'organizzazione richiede l'immissione di una password per sbloccare il dispositivo. |
| La password è troppo breve.|  Assicurarsi che la password non contenga numeri in sequenza o ripetuti, come 1234 o 1111. |
| La password è troppo breve. | Aggiornare o impostare una password con più caratteri. L'organizzazione richiede una determinata lunghezza per la password.|
| La password deve contenere solo numeri. | Impostare una password che contenga solo numeri.|
| La password deve contenere solo caratteri alfanumerici. | Impostare una password che contenga una combinazione di numeri e lettere.|
| La password deve contenere caratteri non alfanumerici. | Aggiungere caratteri speciali, come `&`, `!`, `$`, `%` e `#`. L'organizzazione richiede una combinazione di lettere, numeri e caratteri non alfanumerici per rendere più difficile l'individuazione della password.|
| Password scaduta. | Impostare una nuova password. L'organizzazione richiede di modificare la password dopo un determinato numero di giorni. |
| La password è stata usata troppo di recente. | Scegliere una password non usata in precedenza. L'organizzazione richiede un periodo di tempo specifico prima di riutilizzare una password. |

## <a name="android-password-requirements"></a>Requisiti per le password in Android
| Messaggio | Procedura di correzione |
|-----------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Password richiesta. | Impostare una password o un PIN. L'organizzazione richiede l'immissione di una password per sbloccare il dispositivo. |
| La password è troppo breve. |  Assicurarsi che la password o il PIN non contenga numeri in sequenza o ripetuti, come 1234 o 1111. |
| La password è troppo breve. | Aggiornare o impostare una password con più caratteri. L'organizzazione richiede una determinata lunghezza per la password.|
| La password deve contenere numeri. | Impostare una password o un PIN che contenga solo numeri.|
| La password deve contenere lettere. | Impostare una password che contenga lettere dall'alfabeto.|
| La password deve contenere caratteri alfanumerici. | Impostare una password che contenga una combinazione di numeri e lettere.|
| La password deve contenere caratteri alfanumerici e simboli. | Impostare una password che contenga una combinazione di lettere, numeri e caratteri speciali, come `&`, `!`, `$`, `%` e `#`. |
| La password deve usare la tecnologia biometrica.| Configurare il dispositivo per l'uso dell'autenticazione biometrica, ad esempio l'impronta digitale o il riconoscimento facciale.
| Password scaduta. | Impostare una nuova password. L'organizzazione richiede di modificare la password dopo un determinato numero di giorni. |
| La password è stata usata troppo di recente. | Scegliere una password non usata in precedenza. L'organizzazione richiede un periodo di tempo specifico prima di riutilizzare una password. |

## <a name="next-steps"></a>Passaggi successivi
Se dopo aver aggiornato la password si ricevono ancora messaggi relativi alla password, provare a riavviare il dispositivo. 

Serve ancora assistenza? Contattare il responsabile del supporto IT. Per informazioni sul contatto vedere il [sito Web del portale aziendale](https://go.microsoft.com/fwlink/?linkid=2010980).  


