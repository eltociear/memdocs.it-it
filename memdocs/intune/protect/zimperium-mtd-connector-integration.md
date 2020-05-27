---
title: Integrare Zimperium MTD con Microsoft Intune
titleSuffix: Microsoft Intune
description: Come configurare la soluzione Zimperium Mobile Threat Defense (MTD) con Microsoft Intune per controllare l'accesso dei dispositivi mobili alle risorse aziendali.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/21/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 363fd280-1865-4a61-855b-eb75c3c62753
ms.reviewer: davidra
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4666c8c765f15ddd103727ccf2a7d840cb69bd20
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989369"
---
# <a name="integrate-zimperium-with-intune"></a>Integrare Zimperium con Intune

Seguire questa procedura per integrare la soluzione Zimperium Mobile Threat Defense (MTD) con Intune.

## <a name="before-you-begin"></a>Prima di iniziare

I passaggi seguenti vengono eseguiti nella [console di Zimperium MTD](https://www.zimperium.com/platform) e consentiranno una connessione al servizio Zimperium per i dispositivi registrati in Intune (usando la conformità del dispositivo) e i dispositivi non registrati (usando i criteri di protezione delle app).

Prima di avviare il processo di integrazione di Zimperium con Intune, verificare che siano disponibili la sottoscrizione e le credenziali seguenti:

- Sottoscrizione di Microsoft Intune

- Credenziali di amministratore globale di Azure Active Directory per concedere le autorizzazioni seguenti:

  - Accesso e lettura del profilo utente

  - Accesso alla directory come utente connesso

  - Lettura dati directory

  - Invio di informazioni sul dispositivo a Intune

- Credenziali di amministratore per accedere alla console di Zimperium MTD.

### <a name="zimperium-app-authorization"></a>Autorizzazione dell'app Zimperium

Il processo di autorizzazione dell'app Zimperium è il seguente:

- Concedere al servizio Zimperium le autorizzazioni per comunicare a Intune informazioni relative allo stato di integrità dei dispositivi. Per concedere queste autorizzazioni è necessario usare le credenziali di amministratore globale. La concessione di autorizzazioni è un'operazione da eseguire una volta sola. Una volta concesse le autorizzazioni, le credenziali di amministratore globale non sono necessarie per le operazioni quotidiane.

- Zimperium esegue la sincronizzazione con l'appartenenza al gruppo di registrazione di Azure Active Directory (AD) per popolare il relativo database del dispositivo.

- Consentire alla console di amministrazione di Zimperium di usare la funzionalità Single Sign-On (SSO) di Azure AD.

- Consentire all'app Zimperium di accedere usando la funzionalità SSO di Azure AD.

Per altre informazioni sul consenso e sulle applicazioni di Azure Active Directory, vedere [Richiedere le autorizzazioni da un amministratore di directory](https://docs.microsoft.com/azure/active-directory/develop/v2-permissions-and-consent#request-the-permissions-from-a-directory-admin) nell'articolo di Azure Active Directory *Autorizzazioni e consenso nell'endpoint v2.0 di Azure Active Directory*.


## <a name="to-set-up-zimperium-integration"></a>Per configurare l'integrazione con Zimperium

1. Passare alla [console di Zimperium MTD](https://www.zimperium.com/platform) e accedere con le proprie credenziali. Per eseguire il processo di configurazione dell'integrazione con Zimperium, è necessario accedere con un account utente di Azure Active Directory dotato del ruolo di amministratore globale. Questa operazione di configurazione, da eseguire una volta sola, usa i diritti di amministratore globale per concedere all'interno dell'organizzazione l'autorizzazione necessaria per consentire alle app di Zimperium di comunicare con Intune. 

2. Scegliere **Management** (Gestione) nel menu a sinistra.

3. Scegliere la scheda **MDM Settings** (Impostazioni MDM).

4. Scegliere **Add MDM** (Aggiungi MDM), quindi selezionare **Microsoft Intune** dall'elenco **dei provider MDM**.

5. Dopo aver impostato Microsoft Intune come servizio di gestione dei dispositivi mobili (MDM), nella finestra di **configurazione di Microsoft Intune** visualizzata scegliere **Aggiungi Azure Active Directory** per ogni opzione: **Zimperium zConsole** e **app zIPS iOS e Android** per autorizzare Zimperium a comunicare con Intune e Azure AD usando la funzionalità Single Sign-On di Azure Active Directory.

    > [!IMPORTANT]  
    > È necessario aggiungere Zimperium zConsole e le app zIPS per iOS e Android per completare il processo di integrazione con Intune.

6. Scegliere **Accept** (Accetta) per autorizzare l'app Zimperium a comunicare con Intune e Azure Active Directory.

7. Dopo aver aggiunto **Zimperium zConsole** e le app **zIPS per iOS e Android** ad Azure AD, aggiungere i gruppi di sicurezza di Azure AD. In questo modo si consente a Zimperium di sincronizzare il gruppo di sicurezza di Azure AD con il proprio servizio.

8. Scegliere **Finish** (Fine) per salvare la configurazione e avviare la sincronizzazione del primo gruppo di sicurezza di Azure AD.

9. Disconnettersi dalla console di Zimperium MTD.

## <a name="next-steps"></a>Passaggi successivi

- [Configurare app Zimperium per i dispositivi registrati](mtd-apps-ios-app-configuration-policy-add-assign.md)
- [Configurare app Zimperium per i dispositivi non registrati](mtd-add-apps-unenrolled-devices.md)
