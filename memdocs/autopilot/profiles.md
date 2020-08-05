---
title: Configurare i profili di Autopilot
description: Informazioni su come configurare i profili di dispositivo durante l'esecuzione di una distribuzione di Windows Autopilot.
keywords: MDM, installazione, Windows, Windows 10, OOBE, gestione, distribuzione, Autopilot, ZTD, zero-touch, partner, msfb, Intune
ms.reviewer: mniehaus
manager: laurawi
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
ms.openlocfilehash: 0a18eb4020a32e752c9d3fa7988e411dc72be98e
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/04/2020
ms.locfileid: "87756613"
---
# <a name="configure-autopilot-profiles"></a>Configurare i profili di Autopilot

**Si applica a**

-   Windows 10

Per ogni dispositivo definito nel servizio di distribuzione di Windows Autopilot, è necessario applicare un profilo di impostazioni che specifichi il comportamento esatto del dispositivo quando viene distribuito. Per le procedure dettagliate su come configurare le impostazioni del profilo e registrare i dispositivi, vedere [registrazione di dispositivi](add-devices.md#registering-devices).

## <a name="profile-settings"></a>Impostazioni del profilo

Sono disponibili le impostazioni di profilo seguenti:

-   **Ignorare le pagine di configurazione per la registrazione di Cortana, OneDrive e OEM**. Tutti i dispositivi registrati con Autopilot ignoreranno automaticamente queste pagine durante il processo di configurazione guidata.

-   **Configurata automaticamente per l'ufficio o l'Istituto di istruzione**. Tutti i dispositivi registrati con Autopilot sono considerati automaticamente dispositivi aziendali o dell'Istituto di istruzione, pertanto questa domanda non verrà visualizzata durante il processo di configurazione guidata.

-   **Esperienza di accesso con informazioni personalizzate distintive dell'azienda**. Invece di presentare una pagina di accesso Azure Active Directory generica, tutti i dispositivi registrati con Autopilot presenteranno una pagina di accesso personalizzata con il nome dell'organizzazione, il logo e il testo della Guida aggiuntiva, come configurato nella Azure Active Directory. Per personalizzare queste impostazioni, vedere Aggiungere informazioni personalizzate distintive [dell'azienda alla directory](https://docs.microsoft.com/azure/active-directory/customize-branding#add-company-branding-to-your-directory) .

-   **Ignora le impostazioni di privacy**. Questa impostazione facoltativa del profilo di Autopilot consente alle organizzazioni di non richiedere informazioni sulle impostazioni della privacy durante il processo di configurazione guidata. Questa operazione è in genere auspicabile, in modo che l'organizzazione possa configurare queste impostazioni tramite Intune o altri strumenti di gestione.

-   **Disabilitare la creazione dell'account amministratore locale nel dispositivo**. Le organizzazioni possono decidere se l'utente che configura il dispositivo deve avere l'accesso come amministratore al termine del processo.

-   **Ignora il contratto di licenza con l'utente finale (EULA)**. In Windows 10 versione 1709 e successive, le organizzazioni possono decidere di ignorare la pagina EULA visualizzata durante il processo di configurazione guidata. Ciò significa che le organizzazioni accettano le condizioni di licenza per conto dei propri utenti.

-   **Disabilitare le funzionalità consumer di Windows**. In Windows 10 versione 1803 e successive, le organizzazioni possono disabilitare le funzionalità consumer di Windows in modo che il dispositivo non installi automaticamente eventuali app Microsoft Store aggiuntive quando l'utente accede per la prima volta al dispositivo. Per ulteriori informazioni, vedere la [documentazione di MDM](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsconsumerfeatures).

## <a name="related-topics"></a>Argomenti correlati

[Download del profilo](troubleshooting.md#profile-download)<br>
[Registrazione dei dispositivi](add-devices.md)
