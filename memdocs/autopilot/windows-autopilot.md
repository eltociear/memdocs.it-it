---
title: Panoramica di Windows Autopilot
description: Windows Autopilot è una raccolta di tecnologie che consentono di configurare e preconfigurare nuovi dispositivi, preparandoli per un uso produttivo.
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
ms.openlocfilehash: 8c339e2a55fd8876ce8a144bb72c7c0a37de8346
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/26/2020
ms.locfileid: "88907835"
---
# <a name="overview-of-windows-autopilot"></a>Panoramica di Windows Autopilot

**Si applica a**

-  Windows 10

Windows Autopilot è una raccolta di tecnologie che consentono di configurare e preconfigurare nuovi dispositivi, preparandoli per un uso produttivo. È anche possibile usare Windows Autopilot per reimpostare, reimpiegare e ripristinare i dispositivi. Questa soluzione consente a un reparto IT di raggiungere le versioni precedenti senza alcuna infrastruttura da gestire, con un processo semplice e semplice.

Windows Autopilot semplifica il ciclo di vita dei dispositivi Windows, sia per l'IT che per gli utenti finali, dalla distribuzione iniziale fino alla fine della vita. Uso di servizi basati sul cloud, Windows Autopilot:
- riduce il tempo impiegato per la distribuzione, la gestione e il ritiro dei dispositivi.
- riduce l'infrastruttura necessaria per gestire i dispositivi.
- ottimizza la semplicità di utilizzo per tutti i tipi di utenti finali.

Vedere il video e il diagramma seguenti:

&nbsp;

> [!video https://www.microsoft.com/videoplayer/embed/RE4C7G9?autoplay=false]

![Panoramica del processo](images/image1.png)

Quando inizialmente si distribuiscono nuovi dispositivi Windows, Windows Autopilot usa la versione ottimizzata per OEM di Windows 10. Questa versione è preinstallata nel dispositivo, quindi non è necessario mantenere le immagini e i driver personalizzati per ogni modello di dispositivo. Invece di ricreare l'immagine del dispositivo, l'installazione esistente di Windows 10 può essere trasformata in uno stato "pronto per l'azienda", che può:
- applicare impostazioni e criteri
- installare le app
- modificare l'edizione di Windows 10 in uso (ad esempio, da Windows 10 Pro a Windows 10 Enterprise) per supportare funzionalità avanzate.

Una volta distribuita, è possibile gestire i dispositivi Windows 10 con:
- Microsoft Intune
- Windows Update for Business
- Microsoft Endpoint Configuration Manager
- o altri strumenti simili.

Con Windows Autopilot è possibile preparare rapidamente un dispositivo per un nuovo utente con la reimpostazione di Windows Autopilot. È anche possibile usare Reimposta in scenari di interruzioni/correzioni per riportare rapidamente un dispositivo a uno stato pronto per l'azienda.

Windows Autopilot consente di:
* Aggiungere automaticamente i dispositivi a Azure Active Directory (Azure AD) o Active Directory (tramite Aggiunta ad Azure AD ibrido). Per ulteriori informazioni sulle differenze tra queste due opzioni di join, vedere [Introduzione alla gestione dei dispositivi in Azure Active Directory](/azure/active-directory/device-management-introduction).
* Registrare automaticamente i dispositivi nei servizi MDM, ad esempio Microsoft Intune ([*richiede una sottoscrizione Azure ad Premium per la configurazione*](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-Identity/Windows-10-Azure-AD-and-Microsoft-Intune-Automatic-MDM/ba-p/244067)).
* Limitare la creazione dell'account amministratore.
* Creare e assegnare automaticamente i dispositivi ai gruppi di configurazione in base al profilo del dispositivo.
* Personalizzare il contenuto della configurazione guidata specifico per l'organizzazione.

## <a name="benefits-of-windows-autopilot"></a>Vantaggi di Windows Autopilot

Tradizionalmente, i professionisti IT spendono molto tempo per creare e personalizzare le immagini che verranno distribuite in un secondo momento nei dispositivi. Windows Autopilot introduce un nuovo approccio.

Dal punto di vista dell'utente, sono necessarie solo alcune semplici operazioni per rendere il dispositivo pronto per l'uso.

Dal punto di vista del professionista IT, l'unica interazione richiesta dall'utente finale è la connessione a una rete e la verifica delle credenziali. Tutto il resto è automatizzato.

## <a name="requirements"></a>Requisiti

Per usare Windows Autopilot è necessaria una [versione supportata](/windows/release-information/) del canale semestrale di Windows 10. È supportato anche Windows 10 Enterprise LTSC 2019. Per ulteriori informazioni, vedere la pagina relativa ai requisiti per il software, la [rete](networking-requirements.md), la [configurazione](configuration-requirements.md)e le [licenze](licensing-requirements.md) di [Windows Autopilot](software-requirements.md).

## <a name="related-topics"></a>Argomenti correlati

[Registrare i dispositivi Windows in Intune usando Windows Autopilot](/intune/enrollment-autopilot)<br>
[Scenari e funzionalità di Windows Autopilot](windows-autopilot-scenarios.md)