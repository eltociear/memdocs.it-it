---
title: Configurare i profili di Autopilot
description: Informazioni su come configurare i profili di dispositivo per la distribuzione di Windows Autopilot.
keywords: MDM, installazione, Windows, Windows 10, OOBE, gestione, distribuzione, Autopilot, ZTD, zero-touch, partner, msfb, Intune
ms.reviewer: mniehaus
manager: laurawi
ms.technology: windows
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: dddabd1408a3f00c472ae787f201f3998c323482
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/09/2020
ms.locfileid: "89606565"
---
# <a name="configure-autopilot-profiles"></a>Configurare i profili di Autopilot

**Si applica a**

-  Windows 10

È necessario applicare un profilo impostazioni a ogni dispositivo che usa il servizio di distribuzione di Windows Autopilot. Il profilo deve specificare il comportamento di distribuzione esatto del dispositivo. Per le procedure dettagliate su come configurare le impostazioni del profilo e registrare i dispositivi, vedere [registrazione di dispositivi](add-devices.md#registering-devices).

## <a name="profile-settings"></a>Impostazioni del profilo

Sono disponibili le impostazioni di profilo seguenti:

-  **Ignorare le pagine di configurazione per la registrazione di Cortana, OneDrive e OEM**. Tutti i dispositivi registrati con Autopilot ignoreranno automaticamente queste pagine durante il processo di configurazione guidata.

-  **Configurata automaticamente per l'ufficio o l'Istituto di istruzione**. Tutti i dispositivi registrati con Autopilot sono considerati automaticamente dispositivi aziendali o dell'Istituto di istruzione, quindi questa domanda non verrà visualizzata durante il processo di configurazione guidata.

-  **Esperienza di accesso con informazioni personalizzate distintive dell'azienda**. Invece di presentare una pagina di accesso Azure AD generica, tutti i dispositivi Autopilot registrati presenteranno una pagina di accesso personalizzata. In questa pagina vengono visualizzati il nome dell'organizzazione, il logo e il testo della Guida aggiuntiva, come configurato in Azure AD. Per personalizzare queste impostazioni, vedere Aggiungere informazioni personalizzate distintive [dell'azienda alla directory](/azure/active-directory/customize-branding#add-company-branding-to-your-directory) .

-  **Ignora le impostazioni di privacy**. Questa impostazione facoltativa del profilo di Autopilot consente alle organizzazioni di non richiedere informazioni sulle impostazioni della privacy durante il processo di configurazione guidata. Questa impostazione è in genere auspicabile, in modo che l'organizzazione possa configurare queste impostazioni tramite Intune o altri strumenti di gestione.

-  **Disabilitare la creazione dell'account amministratore locale nel dispositivo**. Le organizzazioni possono decidere se l'utente che configura il dispositivo deve avere l'accesso come amministratore al termine del processo.

-  **Ignora il contratto di licenza con l'utente finale (EULA)**. In Windows 10 versione 1709 e successive, le organizzazioni possono decidere di ignorare la pagina EULA visualizzata durante il processo di configurazione guidata. Ignorando la pagina EULA, le organizzazioni accettano le condizioni di licenza per gli utenti.

-  **Disabilitare le funzionalità consumer di Windows**. In Windows 10 versione 1803 e successive, le organizzazioni possono disabilitare le funzionalità consumer di Windows. Quando le funzionalità consumer di Windows sono disabilitate, il dispositivo non installa automaticamente eventuali app Microsoft Store aggiuntive quando l'utente accede per la prima volta al dispositivo. Per ulteriori informazioni, vedere la [documentazione di MDM](/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsconsumerfeatures).

## <a name="related-topics"></a>Argomenti correlati

[Download del profilo](troubleshooting.md#profile-download)<br>
[Registrazione dei dispositivi](add-devices.md)
