---
title: Azioni e opzioni di Intune supportate con la registrazione utente Apple
titleSuffix: Microsoft Intune
description: Informazioni sulle azioni e opzioni di Intune supportate con la registrazione utente Apple
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 2/14/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: aa78178f6649e0199aa2de96bac2725ba55208ae
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79359261"
---
# <a name="intune-actions-and-options-supported-with-apple-user-enrollment"></a>Azioni e opzioni di Intune supportate con la registrazione utente Apple

La registrazione utente supporta un subset di opzioni di gestione dei dispositivi. Se un profilo di configurazione preesistente viene applicato a un dispositivo di registrazione utente, solo le impostazioni supportate dalla registrazione utente verranno applicate al dispositivo.

> [!NOTE]
> Il supporto per la registrazione utente di Apple in Intune è attualmente in versione di anteprima per iOS e iPadOS.

## <a name="password-settings"></a>Impostazioni della password

Nei dispositivi di registrazione utente, se si configura qualsiasi impostazione della password, le impostazioni **Password semplici** vengono impostate automaticamente su **Blocca** e viene impostato un PIN a 6 cifre.

Si supponga ad esempio di configurare l'impostazione **Scadenza password** e di applicare questo criterio nei dispositivi registrati dall'utente. Nei dispositivi si verificherà quanto segue:
- L'impostazione **Scadenza password** viene ignorata.
- Le password semplici, ad esempio `111111` o `123456`, non sono consentite.
- Viene applicato un PIN di 6 cifre.

## <a name="administrator-remote-device-actions-and-options"></a>Azioni e opzioni dell'amministratore nei dispositivi remoti
Gli amministratori possono eseguire le azioni e le opzioni seguenti nei dispositivi di registrazione utente:
- Ritiro
- Elimina
- Blocco remoto
- Sincronizza

Tutte le altre azioni non sono supportate.

## <a name="end-user-actions"></a>Azioni dell'utente finale
Nei dispositivi di registrazione utente gli utenti finali possono eseguire le azioni seguenti nei propri dispositivi dall'applicazione Portale aziendale e dal sito Web:
- Ridenominazione. Questa azione si applica solo al nome visualizzato all'utente all'interno del portale aziendale. Il dispositivo non verrà rinominato al di fuori di tale contesto.
- Remove
- Blocco remoto
- Controllo dello stato

## <a name="app-deployment-options"></a>Opzioni per la distribuzione di app
I tipi di app seguenti possono essere distribuiti nei dispositivi di registrazione utente:
- App di Volume Purchasing Plan (VPP) con licenza utente, incluse le app personalizzate
- App line-of-business
- App Web

## <a name="other-supported-options"></a>Altre opzioni supportate

Le opzioni seguenti sono supportate in Intune per i dispositivi registrati con la registrazione utente Apple:
- VPN per singole app. Questo supporto esclude i domini Safari poiché la registrazione utente non supporta la configurazione delle impostazioni di Safari.
- Wi-Fi 
- Rimozione dell'app aziendale dopo l'annullamento della registrazione
- Rilevamento jailbreak

Sono supportate le restrizioni seguenti:
- Visualizzazione dei documenti aziendali nelle app non gestite
- Visualizzazione di documenti non aziendali nelle app aziendali
- Consenti alle app gestite di leggere da contatti in account di contatti non gestiti
- Considera AirDrop come destinazione non gestita
- Richiedi il backup crittografato
- Sincronizzazione delle app gestite nel cloud
- Accesso al centro di controllo durante il blocco del dispositivo
- Accesso al centro notifiche durante il blocco del dispositivo
- Visualizzazione Oggi durante il blocco del dispositivo
- Blocca le registrazioni di screenshot e di schermate
- Blocca il backup di libri aziendali
- Blocca la sincronizzazione di metadati di libri aziendali
- Richiedi backup crittografato
- Rilevamento del polso per l'Apple Watch associato
- Blocca Siri
- Blocca Siri durante il blocco del dispositivo
- Avvisi in caso di illeciti di Safari
- Blocco dell'invio dei dati di diagnostica ad Apple


## <a name="options-not-supported"></a>Opzioni non supportate
Le opzioni seguenti non sono supportate nei dispositivi registrati con la registrazione utente. Se sono necessarie queste opzioni, vedere la registrazione dei dispositivi per i dispositivi personali o la registrazione automatica dei dispositivi per i dispositivi aziendali.
- Raccogliere l'inventario delle app per le app al di fuori del volume APFS gestito.
- Raccogliere l'inventario dei certificati e i profili di provisioning al di fuori del volume APFS gestito.
- Raccogliere UDID e altri identificatori di dispositivo permanenti.
- Sebbene la registrazione utente supporti un ID registrazione univoco per ogni dispositivo registrato, questo ID non viene mantenuto dopo l'annullamento della registrazione.
- Le funzionalità di Intune seguenti non sono supportate a causa di questa limitazione:
- Profili utente SCEP con formato del nome soggetto del numero di serie.
- VPN a livello di dispositivo.
- Distribuzione di app VPP con licenza dispositivo.
- Installare app di App Store come app gestite.
- Controllo MDM di applicazioni al di fuori del volume APFS gestito.
- I criteri di protezione delle applicazioni verranno comunque applicati a queste app. Non sarà tuttavia possibile assumere la gestione o distribuire una versione gestita di queste app a meno che l'utente non le elimini dal dispositivo.
- Azioni, configurazioni, impostazioni e comandi che richiedono la supervisione. 


## <a name="known-issues-in-preview"></a>Problemi noti nell'anteprima
- Revoca della licenza VPP: non viene visualizzata una notifica che informa che la licenza è stata revocata. Nel comportamento corrente la revoca viene eseguita correttamente ma l'utente finale non riceve alcuna notifica. 
- Segnalazione applicazioni VPP: Nel report presente in App client > App > [Nome app] > Stato dell'installazione del dispositivo le applicazioni VPP distribuite nei dispositivi registrati dall'utente vengono segnalate come "non riuscite", anche quando l'applicazione viene distribuita correttamente nel dispositivo. 
- Segnalazione applicazioni: per i tipi di app non supportati dalla registrazione utenti, i report possono inviare messaggi di errore irrilevanti. 
- Esperienza dell'app Portale aziendale: gli utenti visualizzano tutte le applicazioni che sono loro destinate indipendentemente dal fatto che tali tipi di applicazioni siano supportati per i dispositivi registrati dall'utente. 
- Esperienza dell'app Portale aziendale: Gli utenti visualizzano lo stesso testo che specifica quali elementi relativi alla registrazione di utenti e dispositivi possono essere visualizzati dalle organizzazioni se l'amministratore ha personalizzato il testo che specifica gli elementi che le organizzazioni non possono visualizzare.


## <a name="next-steps"></a>Passaggi successivi

[Configurare la registrazione utente iOS/iPadOS e iPadOS](ios-user-enrollment.md)
