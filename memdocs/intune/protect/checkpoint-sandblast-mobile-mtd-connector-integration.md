---
title: Integrare Check Point SandBlast MTD
titleSuffix: Microsoft Intune
description: Come configurare CheckPoint SandBlast Mobile Threat Defense (MTD) con Intune per controllare l'accesso dei dispositivi mobili alle risorse aziendali.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/21/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 1e9b1576-b239-48cc-a672-da6b5fb7be0a
ms.reviewer: davidra
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: ed468bfd9a16bb231d29f21c545cd27f121d22e7
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79353372"
---
# <a name="integrate-check-point-sandblast-mobile-with-intune"></a>Integrare Check Point SandBlast Mobile con Intune

Seguire questa procedura per integrare la soluzione Mobile Threat Defense Check Point SandBlast con Intune.

> [!NOTE]
> Questo fornitore di Mobile Threat Defense non è supportato per i dispositivi non registrati.

## <a name="before-you-begin"></a>Prima di iniziare

Le istruzioni riportate in questo articolo devono essere eseguite nella [console di Check Point SandBlast Mobile](https://intune-4.eu1.locsec.net/). 

Prima di avviare il processo di integrazione di Check Point SandBlast Mobile con Intune, assicurarsi di disporre di quanto segue:

- Sottoscrizione di Microsoft Intune

- Credenziali di amministratore di Azure Active Directory per concedere le autorizzazioni seguenti:

  - Accesso e lettura del profilo utente

  - Accesso alla directory come utente connesso

  - Lettura dati directory

  - Invio di informazioni sul dispositivo a Intune

- Credenziali di amministratore per accedere alla console MTD di Check Point SandBlast Mobile.

### <a name="check-point-sandblast-app-authorization"></a>Verificare le autorizzazioni dell'app Check Point SandBlast

Il processo di autorizzazione dell'app Check Point SandBlast è costituito dai seguenti elementi:

- Consentire al servizio Check Point SandBlast Mobile di comunicare a Intune informazioni relative allo stato di integrità dei dispositivi.

- CheckPoint SandBlast Mobile esegue la sincronizzazione con l'appartenenza al gruppo di registrazione di Azure AD per popolare il relativo database del dispositivo.

- Consentire alla console di amministrazione di Check Point SandBlast di usare la funzionalità Single Sign-On (SSO) di Azure AD.

- Consentire all'app Check Point SandBlast Mobile di eseguire l'accesso tramite la funzionalità SSO di Azure AD.

## <a name="to-set-up-check-point-sandblast-mobile-integration"></a>Per configurare l'integrazione di Check Point SandBlast Mobile

1. Passare alla [console MTD di Check Point SandBlast Mobile](https://intune-4.eu1.locsec.net/) e accedere con le proprie credenziali.

2. Fare clic sulla scheda **Settings** (Impostazioni).

3. Scegliere **Device management** (Gestione dispositivi), quindi **Settings** (Impostazioni).

4. Scegliere **Microsoft Intune** dall'elenco a discesa **MDM Service** (Servizio MDM).

5. Dopo aver impostato Microsoft Intune come servizio MDM, verrà visualizzata la finestra **Microsoft Intune Configuration** (Configurazione di Microsoft Intune). Scegliere **Add to my organization** (Aggiungi alla mia organizzazione) per ogni piattaforma per i dispositivi (iOS/iPadOS, Android e Windows) per autorizzare Check Point SandBlast Mobile a comunicare con Intune e Azure AD.

    ![Immagine che illustra la configurazione di Check Point MTD in Intune](./media/checkpoint-sandblast-mobile-mtd-connector-integration/checkpoint-MTD-1.PNG)

    > [!IMPORTANT]
    > È necessario aggiungere tutte le piattaforme per i dispositivi per procedere al passaggio successivo.

6. Scegliere **Accept** (Accetta) per autorizzare l'app Check Point SandBlast Mobile a comunicare con Intune e Azure Active Directory.

7. Dopo avere abilitato tutte le piattaforme per i dispositivi, è necessario immettere il gruppo di sicurezza di Azure AD.

8. Scegliere **Verify** (Verifica). Dopo avere verificato correttamente il gruppo di sicurezza di Azure AD, scegliere **Save** (Salva).

## <a name="next-steps"></a>Passaggi successivi

- [Configurare le app di Check Point SandBlast Mobile](mtd-apps-ios-app-configuration-policy-add-assign.md)
