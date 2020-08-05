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
ms.openlocfilehash: 171070e1560796763f3c3851afe239237098f756
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/04/2020
ms.locfileid: "87756492"
---
# <a name="overview-of-windows-autopilot"></a>Panoramica di Windows Autopilot

**Si applica a**

-   Windows 10

Windows Autopilot è una raccolta di tecnologie che consentono di configurare e preconfigurare nuovi dispositivi, preparandoli per un uso produttivo. È anche possibile usare Windows Autopilot per reimpostare, reimpiegare e ripristinare i dispositivi. Questa soluzione consente a un reparto IT di raggiungere le versioni precedenti senza alcuna infrastruttura da gestire, con un processo semplice e semplice.

Windows Autopilot è progettato per semplificare tutte le parti del ciclo di vita dei dispositivi Windows, sia per l'IT che per gli utenti finali, dalla distribuzione iniziale fino alla fine del ciclo di vita finale. Sfruttando i servizi basati sul cloud, può ridurre i costi complessivi per la distribuzione, la gestione e la disattivazione dei dispositivi, riducendo la quantità di tempo che deve trascorrere per questi processi e la quantità di infrastruttura necessaria per la manutenzione, garantendo al tempo stesso la semplicità di utilizzo per tutti i tipi di utenti finali. Vedere il video e il diagramma seguenti:

&nbsp;

> [!video https://www.microsoft.com/videoplayer/embed/RE4C7G9?autoplay=false]

![Panoramica del processo](images/image1.png)

Quando inizialmente si distribuiscono nuovi dispositivi Windows, Windows Autopilot utilizza la versione ottimizzata per OEM di Windows 10 preinstallata nel dispositivo, evitando alle organizzazioni la necessità di mantenere le immagini e i driver personalizzati per ogni modello di dispositivo in uso. Invece di ricreare l'immagine del dispositivo, l'installazione esistente di Windows 10 può essere trasformata in uno stato "pronto per l'azienda", applicando impostazioni e criteri, installando app e persino cambiando l'edizione di Windows 10 in uso (ad esempio da Windows 10 Pro a Windows 10 Enterprise) per supportare funzionalità avanzate.

Una volta distribuiti, i dispositivi Windows 10 possono essere gestiti da strumenti come Microsoft Intune, Windows Update for business, Microsoft endpoint Configuration Manager e altri strumenti simili. È anche possibile usare Windows Autopilot per riutilizzare un dispositivo sfruttando il ripristino di Windows Autopilot per preparare rapidamente un dispositivo per un nuovo utente o in scenari di interruzioni/correzioni per consentire a un dispositivo di tornare rapidamente a uno stato pronto per l'uso aziendale.

Windows Autopilot consente di:
* Aggiungere automaticamente i dispositivi a Azure Active Directory (Azure AD) o Active Directory (tramite Aggiunta ad Azure AD ibrido).  Per ulteriori informazioni sulle differenze tra queste due opzioni di join, vedere [Introduzione alla gestione dei dispositivi in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/device-management-introduction) .
* Registrare automaticamente i dispositivi nei servizi MDM, ad esempio Microsoft Intune ([*richiede una sottoscrizione Azure ad Premium per la configurazione*](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-Identity/Windows-10-Azure-AD-and-Microsoft-Intune-Automatic-MDM/ba-p/244067)).
* Limitare la creazione dell'account amministratore.
* Creare e assegnare automaticamente i dispositivi ai gruppi di configurazione in base al profilo del dispositivo.
* Personalizzare il contenuto della configurazione guidata specifico per l'organizzazione.

## <a name="benefits-of-windows-autopilot"></a>Vantaggi di Windows Autopilot

Tradizionalmente, i professionisti IT dedicano molto tempo alla creazione e alla personalizzazione di immagini che verranno distribuite in un secondo momento nei dispositivi. Windows Autopilot introduce un nuovo approccio.

Dal punto di vista dell'utente, sono necessarie solo alcune semplici operazioni per rendere il dispositivo pronto per l'uso.

Dal punto di vista del professionista IT, l'unica interazione richiesta dall'utente finale è la connessione a una rete e la verifica delle credenziali. Tutto il resto è automatizzato.

## <a name="requirements"></a>Requisiti

Per usare Windows Autopilot è necessaria una [versione supportata](https://docs.microsoft.com/windows/release-information/) del canale semestrale di Windows 10. È supportato anche Windows 10 Enterprise LTSC 2019. Per informazioni dettagliate sui requisiti di software, configurazione, rete e licenze, vedere [requisiti di Windows Autopilot](windows-autopilot-requirements.md) .

## <a name="related-topics"></a>Argomenti correlati

[Registrare i dispositivi Windows in Intune usando Windows Autopilot](https://docs.microsoft.com/intune/enrollment-autopilot)<br>
[Scenari e funzionalità di Windows Autopilot](windows-autopilot-scenarios.md)
