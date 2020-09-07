---
title: Restrizioni per i dispositivi Windows 10 Team Surface Hub in Microsoft Intune - Azure | Microsoft Docs
titleSuffix: ''
description: Usare Intune per aggiungere o configurare le impostazioni dei dispositivi Surface Hub che eseguono Windows 10 Team.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/14/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: fdb3a3defbaab5f952a2a5636a30f9734418f841
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88993319"
---
# <a name="windows-10-team-settings-to-allow-or-restrict-features-on-surface-hub-devices-using-intune"></a>Impostazioni dei dispositivi Windows 10 Team per consentire o limitare l'uso delle funzionalità su dispositivi Surface Hub tramite Intune

Questo articolo illustra le impostazioni relative alle restrizioni dei dispositivi di Microsoft Intune configurabili per i dispositivi che eseguono Windows 10 Team, tra cui Surface Hub.

## <a name="before-you-begin"></a>Prima di iniziare

[Creare il profilo del dispositivo](device-restrictions-configure.md#create-the-profile).

## <a name="apps-and-experience"></a>App ed esperienza

Queste impostazioni usano il [CSP SurfaceHub](/windows/client-management/mdm/surfacehub-csp).

- **Attiva lo schermo quando qualcuno è presente nella stanza**: **Blocca** impedisce alla schermata di riattivarsi automaticamente quando il sensore rileva la presenza di qualcuno nella stanza. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.
- **Informazioni sulla riunione visualizzate nella schermata iniziale**: scegliere le informazioni visualizzate nel riquadro riunioni della schermata iniziale. Le opzioni disponibili sono:
  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione.
  - **Solo organizzatore e ora**
  - **Organizzatore, ora e oggetto (l'oggetto è nascosto per le riunioni private)**
- **URL dell'immagine di sfondo della schermata iniziale**: Immettere l'URL di un'immagine con estensione png che si vuole usare come sfondo personalizzato nella schermata **iniziale** sui dispositivi Windows 10 Team. L'immagine deve essere in formato png e l'URL deve iniziare con `https://`.
- **Avvio automatico di Connessione**: **Blocca** impedisce l'apertura automatica dell'app Connessione all'avvio di una proiezione. Se bloccato, gli utenti possono avviare manualmente l'app Connessione dalle impostazioni dell'hub. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.
- **Suggerimenti di accesso**: **Blocca** disabilita la compilazione automatica della finestra di accesso con gli invitati delle riunioni pianificate. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.
- **Riunioni e file**: **Blocca** disabilita la funzionalità **Riunioni e file** nel menu Start. Questa funzionalità mostra le riunioni e i file dell'utente connesso da Microsoft 365. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.

## <a name="azure-operational-insights"></a>Azure Operational Insights

- **Azure Operational Insights**: **Abilita** raccoglie, archivia e analizza i dati di log dai dispositivi Windows 10 Team con Operational Insights di Azure. Azure Operational Insights fa parte del gruppo Microsoft Operations Manager. Immettere l'**ID dell'area di lavoro** e la **chiave dell'area di lavoro** per connettersi ad Azure Operational Insights.

  Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo raccoglie i dati.

## <a name="maintenance"></a>Manutenzione

Queste impostazioni usano il [CSP SurfaceHub](/windows/client-management/mdm/surfacehub-csp).

- **Finestra di manutenzione per gli aggiornamenti**: **Abilita** crea una finestra di manutenzione quando è possibile installare gli aggiornamenti. Immettere l'**Ora inizio** e **Durata in ore** della finestra di manutenzione, da 1 a 5 ore.

  Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.

## <a name="session"></a>Sessione

Queste impostazioni usano il [CSP SurfaceHub](/windows/client-management/mdm/surfacehub-csp).

- **Volume**: immettere il valore predefinito del volume per una nuova sessione, da 0 a 100. Quando il campo è vuoto, Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe impostare il volume su 45.
- **Timeout schermo**: immettere il numero di minuti di attesa prima della disattivazione della schermata dell'hub.
- **Timeout sessione**: immettere il numero di minuti di attesa prima del timeout della sessione.
- **Timeout sospensione**: immettere il numero di minuti di attesa prima del passaggio alla modalità sospensione dell'hub.
- **Riprendi sessione**: **Blocca** impedisce agli utenti di riprendere una sessione quando si verifica il timeout della sessione. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.

## <a name="wireless-projection"></a>Proiezione wireless

Queste impostazioni usano il [CSP SurfaceHub](/windows/client-management/mdm/surfacehub-csp).

- **PIN per proiezione wireless**: **Rendi obbligatorio** impone agli utenti di immettere un PIN prima di usare le funzionalità di proiezione wireless del dispositivo. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.
- **Proiezione wireless Miracast**: **Blocca** impedisce l'uso di dispositivi abilitati per Miracast nel progetto. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione.
- **Canale di proiezione wireless Miracast**: selezionare il canale Miracast per stabilire la connessione.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni, vedere [Come configurare le impostazioni relative alle restrizioni dei dispositivi](device-restrictions-configure.md).

[Assegnare il profilo](device-profile-assign.md) e [monitorarne lo stato](device-profile-monitor.md).