---
title: Impostazioni della modalità tutto schermo per Windows Holographic for Business in Microsoft Intune - Azure | Microsoft Docs
description: Configurare i dispositivi Windows Holographic for Business per l'esecuzione di una o più app in modalità tutto schermo, personalizzare il menu Start, aggiungere app, visualizzare la barra della applicazioni e configurare un Web browser in Microsoft Intune.
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
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8127281069ce4209adfc2aec82a93f5a60669307
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/26/2020
ms.locfileid: "88911863"
---
# <a name="windows-holographic-for-business-device-settings-to-run-as-a-kiosk-in-intune"></a>Impostazioni dei dispositivi Windows Holographic for Business per l'esecuzione come dispositivo in modalità tutto schermo in Intune

È possibile configurare i dispositivi Windows Holographic for Business per l'esecuzione di una o più app in modalità tutto schermo. Alcune funzionalità non sono supportate in Windows Holographic for Business.

Questo articolo descrive le diverse impostazioni che è possibile controllare nei dispositivi Windows Holographic for Business. Usare queste impostazioni nella propria soluzione di gestione di dispositivi mobili (MDM) per configurare i dispositivi Windows Holographic for Business da eseguire in modalità tutto schermo.

Come amministratore di Intune, è possibile creare e assegnare queste impostazioni ai dispositivi.

Per altre informazioni sulla funzionalità Modalità tutto schermo di Windows in Intune, vedere [Configurare le impostazioni a tutto schermo](kiosk-settings.md).

## <a name="before-you-begin"></a>Prima di iniziare

- [Creare un profilo di configurazione del dispositivo per chiosco multimediale di Windows 10](kiosk-settings.md#create-the-profile).

  Quando si crea un profilo di configurazione del dispositivo per chiosco multimediale di Windows 10, sono disponibili altre impostazioni rispetto a quelle elencate in questo articolo. I dispositivi Windows Holographic for Business supportano le impostazioni indicate in questo articolo.

- Questo profilo per la modalità tutto schermo è direttamente correlato al profilo di restrizioni per i dispositivi creato usando le [impostazioni della modalità tutto schermo di Microsoft Edge](device-restrictions-windows-holographic.md#microsoft-edge-browser). Per concludere:

  1. Creare questo profilo per la modalità tutto schermo per l'esecuzione del dispositivo in modalità tutto schermo.
  2. Creare il [profilo di restrizioni per i dispositivi](device-restrictions-windows-holographic.md#microsoft-edge-browser) e configurare le funzionalità e le impostazioni specifiche consentite in Microsoft Edge.

> [!IMPORTANT]
> Assicurarsi di assegnare questo profilo per la modalità tutto schermo agli stessi dispositivi del [profilo di Microsoft Edge](device-restrictions-windows-holographic.md#microsoft-edge-browser).

## <a name="single-app-full-screen-kiosk"></a>App singola per chiosco multimediale a schermo intero

Eseguire una sola app nel dispositivo. Quando l'utente accede, viene avviata un'app specifica. Questa modalità impedisce anche all'utente di aprire nuove app o modificare l'app in esecuzione.

- **Tipo di accesso utente**: selezionare il tipo di account che esegue l'app. Le opzioni disponibili sono:

  - **Accesso automatico (Windows 10, versione 1803 e successive)** : non supportato in Windows Holographic for Business.
  - **Account utente locale**: immettere l'account utente locale (per il dispositivo). In alternativa, immettere un account Microsoft (MSA) associato all'app chiosco multimediale. L'account immesso accede al chiosco multimediale.

    Per i chioschi multimediali in ambienti pubblici, è consigliabile usare un tipo di utente con privilegi minimi.

- **Tipo di applicazione**: selezionare **Aggiungi l'app dello Store**.

  - **App da eseguire in modalità tutto schermo**: selezionare un'applicazione dall'elenco.

    Se l'elenco non include app, aggiungerne qualcuna seguendo la procedura in [App client](../apps/apps-add.md).

## <a name="multi-app-kiosk"></a>Chiosco multimediale per più app

Le app in questa modalità sono disponibili nel menu Start. Sono le uniche app che l'utente può aprire. Se un'app presenta una dipendenza da un'altra app, entrambe devono essere incluse nell'elenco delle app consentite.

- **Specifica Windows 10 come destinazione nei dispositivi in modalità S**: selezionare **No**. La modalità S non è supportata in Windows Holographic for Business.

- **Tipo di accesso utente**: aggiungere uno o più account utente che possano usare le app aggiunte. Le opzioni disponibili sono:

  - **Accesso automatico (Windows 10, versione 1803 e successive)** : non supportato in Windows Holographic for Business.
  - **Account utente locali**: scegliere **Aggiungi** per l'account utente locale (per il dispositivo). L'account immesso accede al chiosco multimediale.
  - **Utente o gruppo di Azure AD (Windows 10, versione 1803+)** : richiede credenziali utente per l'accesso al dispositivo. Selezionare **Aggiungi** per scegliere utenti o gruppi di Azure AD nell'elenco. È possibile selezionare più utenti e gruppi. Scegliere **OK** per salvare le modifiche.
  - **Visitatore di HoloLens**: l'account del visitatore è un account Guest che non richiede credenziali utente o autenticazione, come descritto in [Concetti della modalità PC condiviso](/windows/configuration/set-up-shared-or-guest-pc#shared-pc-mode-concepts).

- **Browser e applicazioni**: aggiungere le app da eseguire nel dispositivo in modalità tutto schermo. Ricordarsi che è possibile aggiungere più app.

  - **Browser**
    - **Aggiungi Microsoft Edge**: Microsoft Edge viene aggiunto alla griglia delle app e tutte le applicazioni possono essere eseguite in questo chiosco multimediale. Selezionare il tipo di modalità tutto schermo di Microsoft Edge:

      - **Modalità normale (versione completa di Microsoft Edge)** : Esegue una versione completa di Microsoft Edge con tutte le funzionalità di esplorazione. I dati dell'utente e lo stato vengono salvati tra le sessioni.
      - **Esplorazione pubblica (InPrivate)** : esegue una versione con più schede di Microsoft Edge InPrivate con un'esperienza personalizzata per i chioschi multimediali eseguiti in modalità schermo intero.

      Per altre informazioni su queste opzioni, vedere [Distribuire la modalità tutto schermo di Microsoft Edge](/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-configuration-types).

      > [!NOTE]
      > Questa impostazione abilita il browser Microsoft Edge nel dispositivo. Per configurare le impostazioni specifiche di Microsoft Edge, creare un profilo di restrizioni del dispositivo (**Dispositivi** > **Profili di configurazione** > **Crea profilo** > **Windows 10** per la piattaforma > **Restrizioni del dispositivo** > **Browser Microsoft Edge**). Nel [browser Microsoft Edge](device-restrictions-windows-holographic.md#microsoft-edge-browser) sono elencate e descritte le impostazioni Windows Holographic for Business disponibili.

    - **Aggiungi un browser in modalità tutto schermo**: non supportato in Windows Holographic for Business.

  - **Applicazioni**
    - **Aggiungi l'app dello Store**: selezionare un'app esistente aggiunta o distribuita in Intune come [app client](../apps/apps-add.md), incluse le app line-of-business. Se non è elencata alcuna app, Intune supporta molti [tipi di app](../apps/apps-add.md) da [aggiungere a Intune](../apps/store-apps-windows.md).
    - **Aggiungi un'app di Win32**: non supportato in Windows Holographic for Business.
    - **Aggiungi in base all'ID modello utente applicazione**: usare questa opzione per aggiungere app predefinite di Windows come il Blocco note o la Calcolatrice. Immettere le proprietà seguenti:

      - **Nome applicazione**: Obbligatorio. Immettere un nome per l'applicazione.
      - **ID modello utente applicazione (AUMID)** : Obbligatorio. Immettere l'ID modello utente applicazione (AUMID) dell'app Windows. Per ottenere questo ID, vedere [Find the Application User Model ID of an installed app](/windows-hardware/customize/enterprise/find-the-application-user-model-id-of-an-installed-app) (Trovare l'ID modello utente dell'applicazione di un'app installata) per ottenere l'ID.

    - **AutoLaunch**: Facoltativo. Dopo aver aggiunto le app e il browser, selezionare un'app o un browser per aprirlo automaticamente quando l'utente accede. È possibile configurare una sola app o browser per l'avvio automatico.
    - **Dimensioni del riquadro**: Obbligatorio. Dopo aver aggiunto le app, selezionare una dimensione Piccola, Media, Larga o Grande del riquadro dell'app.

- **Usa un layout Start alternativo**: selezionare **Sì** per immettere un file XML che descrive come le app vengono visualizzate nel menu Start, incluso il relativo ordine. Usare questa opzione se è necessaria una maggiore personalizzazione nel menu Start. [Personalizzare ed esportare il layout della schermata Start](/hololens/hololens-kiosk#start-layout-for-hololens) offre alcune indicazioni e include un file XML specifico per i dispositivi Windows Holographic for Business.

- **Barra delle applicazioni di Windows**: non supportato in Windows Holographic for Business.
- **Consenti l'accesso alla cartella Download**: non supportato in Windows Holographic for Business.
- **Specificare la finestra di manutenzione per i riavvii dell'app**: non supportato in Windows Holographic for Business.

## <a name="next-steps"></a>Passaggi successivi

[Assegnare il profilo](device-profile-assign.md) e [monitorarne lo stato](device-profile-monitor.md).

È anche possibile creare profili in modalità tutto schermo per dispositivi [Android](device-restrictions-android.md#kiosk), [Android Enterprise](device-restrictions-android-for-work.md#device-experience) e [Windows 10 e versioni successive](kiosk-settings-windows.md).