---
title: Criteri per le app di Office
titleSuffix: Microsoft Intune
description: Informazioni sui criteri disponibili per le app di Office.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: ca558b40ad3d006aa764819a0fbccc16a03fd0e2
ms.sourcegitcommit: d4ed7b4369389fd8ab07d28a7fa507797b6c6e57
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/10/2020
ms.locfileid: "89644027"
---
# <a name="policies-for-office-apps"></a>Criteri per le app di Office

Intune offre criteri specifici per le app di Microsoft Office. È possibile selezionare opzioni specifiche per creare criteri di gestione delle app per dispositivi mobili per le app di Office per dispositivi mobili che si connettono ai servizi di Microsoft 365. Esistono molti criteri per le app di Office che possono essere aggiunti a Microsoft Intune e si applicano ai gruppi di utenti finali.

Di seguito sono riportati alcuni esempi di criteri per le app di Office:
- Microsoft Word: *Disattiva Visualizzazione protetta per gli allegati aperti da Outlook*
- Microsoft Visio: *Blocca l'esecuzione delle macro nei file di Office provenienti da Internet*
- Microsoft Project: *Consenti percorsi attendibili in rete*
- Microsoft Publisher: *Livello sicurezza automazione di Publisher*
- Microsoft PowerPoint: *Disattiva Visualizzazione protetta per gli allegati aperti da Outlook*

> [!NOTE]
> Quando si sceglie di configurare ogni criterio specifico dell'app, vengono specificati dettagli aggiuntivi sui criteri. È possibile filtrare l'elenco dei criteri di Office per selezionare rapidamente i criteri della **baseline di sicurezza** consigliati.

È anche possibile proteggere l'accesso alle cassette postali locali di Exchange creando criteri di protezione delle app di Intune per Outlook per iOS/iPadOS e Android abilitati con l'autenticazione moderna ibrida. Prima di usare questa funzionalità, è necessario che siano soddisfatti i requisiti per l'uso del servizio di criteri del cloud di Office. I criteri di protezione delle app non sono supportati per le altre app che si connettono ai servizi locali di Exchange o SharePoint. Per informazioni correlate, vedere [Panoramica del servizio di criteri del cloud di Office per Microsoft 365 Apps for enterprise](https://docs.microsoft.com/deployoffice/overview-office-cloud-policy-service).

## <a name="prerequisites"></a>Prerequisiti

È necessario che siano soddisfatti i requisiti per l'uso dei criteri per le app di Office. Per altre informazioni, vedere [Requisiti per l'uso del servizio criteri cloud di Office](https://docs.microsoft.com/deployoffice/overview-office-cloud-policy-service#requirements-for-using-the-office-cloud-policy-service).

## <a name="to-add-an-office-app-policy"></a>Per aggiungere criteri per le app di Office

Dopo aver configurato Intune per l'organizzazione, è possibile creare criteri per le app di Office.

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selezionare **App** > **Criteri per le app di Office** > **Crea**.
3. Aggiungere i valori seguenti:
    - **Nome:** digitare un nome (obbligatorio) per i nuovi criteri.
    - **Descrizione:** (facoltativo) digitare una descrizione.
    - **Seleziona tipo:** consente di selezionare come verrà applicata questa configurazione dei criteri.
    - **Seleziona gruppo:** consente di selezionare il gruppo per questa configurazione dei criteri.
    - **Configura criteri:** consente di selezionare i criteri di Office da applicare. È possibile ordinare l'elenco visualizzato in base a criteri, piattaforma, applicazione, raccomandazione e stato.
4. Selezionare **Crea**. I criteri vengono creati e visualizzati nella tabella nel riquadro **Configurazioni dei criteri**.

   > [!TIP]
   > Il riquadro **Configurazioni dei criteri** visualizza lo **stato di integrità** per i singoli criteri.

## <a name="additional-information"></a>Informazioni aggiuntive

- [Panoramica del servizio di criteri del cloud di Office per Microsoft 365 Apps for enterprise](https://docs.microsoft.com/deployoffice/overview-office-cloud-policy-service)
- [Usare le impostazioni dei criteri per gestire i controlli della privacy per Microsoft 365 Apps for enterprise](https://docs.microsoft.com/deployoffice/privacy/manage-privacy-controls)
- [Usare le preferenze per gestire i controlli di privacy di Office per Mac](https://docs.microsoft.com/deployoffice/privacy/mac-privacy-preferences)
- [Usare le preferenze per gestire i controlli della privacy di Office sui dispositivi iOS](https://docs.microsoft.com/deployoffice/privacy/ios-privacy-preferences)
- [Usare le impostazioni dei criteri per gestire i controlli della privacy per Office nei dispositivi Android](https://docs.microsoft.com/deployoffice/privacy/android-privacy-controls)

## <a name="next-steps"></a>Passaggi successivi

- [Monitorare le informazioni sulle app e le assegnazioni con Microsoft Intune](apps-monitor.md)