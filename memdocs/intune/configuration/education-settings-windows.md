---
title: Impostazioni Istruzione di Windows 10 in Microsoft Intune - Azure | Microsoft Docs
description: Visualizzare un elenco di tutte le impostazioni Istruzione per i dispositivi Windows 10. Usare queste impostazioni in un profilo di configurazione del dispositivo con l'app Test ed esami, scegliere la modalità di accesso di utenti e studenti, monitorare lo schermo durante il test e altro ancora in Intune.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/03/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 6f4de4bd-3dde-4a8d-8e22-46c5d06c3eea
ms.reviewer: kakyker
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2c6648f66c585dac5b8913fdb13adfcb98cbf927
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/26/2020
ms.locfileid: "88912696"
---
# <a name="configure-the-take-a-test-app-on-windows-10-devices-using-intune"></a>Configurare l'app Test ed esami nei dispositivi Windows 10 tramite Intune

L'app Test ed esami consente di amministrare in modo sicuro i test online nei dispositivi Windows 10 della classe. Per configurare l'app Test ed esami, sarà necessario creare un profilo di configurazione del dispositivo in Intune e configurare le impostazioni di valutazione sicura. Questo articolo descrive le impostazioni disponibili per l'app Test ed esami. 

Dopo aver configurato il profilo, assegnarlo e distribuirlo agli studenti. 

L'[app Test ed esami in Intune](education-settings-configure.md) offre altre informazioni su questa funzionalità.

## <a name="before-you-begin"></a>Prima di iniziare

[Creare un profilo di configurazione del dispositivo](education-settings-configure.md#create-a-device-profile).

## <a name="take-a-test-settings"></a>Impostazioni di Test ed esami

- **Tipo di account**: scegliere la modalità di accesso degli utenti al test. Le opzioni disponibili sono:
  - Account di Azure AD
  - Account di dominio
  - Account locale
  - Account Guest locale: disponibile solo nei dispositivi che eseguono Windows 10, versione 1903 e successive.
- **Nome utente dell'account**: immettere il nome utente dell'account usato con l'app Test ed esami. È possibile immettere gli account nel formato seguente:
  - `user@contoso.com`
  - `domain\username`
  - `user@contoso.com`
  - `computerName\username`
- **Nome account**: per configurare un tipo di account Guest locale, immettere il nome dell'account usato con l'app Test ed esami. Il nome dell'account verrà visualizzato come riquadro nella schermata di accesso. Gli studenti fanno clic sul riquadro per avviare il test.  
- **URL della valutazione**: immettere l'URL del test che dovrà essere eseguito dagli utenti. Per altre informazioni su come ottenere l'URL, vedere la [documentazione relativa a Test ed esami](/education/windows/take-tests-in-windows-10).
- **Connessione stampanti**: **Rendi obbligatorio** consente l'accesso all'app Test ed esami solo dai dispositivi connessi a una stampante. Questa impostazione rende anche disponibile il pulsante Stampa dell'app per gli utenti che eseguono i test. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita il sistema operativo potrebbe consentire agli studenti di accedere all'app da dispositivi non connessi a una stampante.  
- **Monitoraggio dello schermo**: **Consenti** monitora l'attività dello schermo mentre gli utenti eseguono il test. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita il sistema operativo potrebbe impedire il monitoraggio dello schermo durante il test.
- **Suggerimenti di testo**: scegliere **Consenti** per consentire a chi esegue il test di visualizzare i suggerimenti di testo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita il sistema operativo potrebbe bloccare i suggerimenti di testo mentre gli utenti eseguono un test.

## <a name="next-steps"></a>Passaggi successivi

[Assegnare il profilo](device-profile-assign.md) e [monitorarne lo stato](device-profile-monitor.md).

Altre informazioni sull'[applicazione Test ed esami](education-settings-configure.md).