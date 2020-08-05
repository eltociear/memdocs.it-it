---
title: Novità di Windows Autopilot
ms.reviewer: ''
manager: laurawi
description: Leggi le notizie e le risorse sugli aggiornamenti più recenti e le versioni precedenti di Windows Autopilot.
keywords: MDM, installazione, Windows, Windows 10, OOBE, gestione, distribuzione, Autopilot, ZTD, zero-touch, partner, msfb, Intune
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
ms.openlocfilehash: d54377222f2e4ef3776e5a765d730f1e1ab38e37
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/04/2020
ms.locfileid: "87756498"
---
# <a name="windows-autopilot-whats-new"></a>Windows Autopilot: novità

**Si applica a**

-   Windows 10

## <a name="windows-autopilot-update-history"></a>Cronologia aggiornamenti di Windows Autopilot

Sono disponibili i seguenti [aggiornamenti di Windows Autopilot](autopilot-update.md) . **Nota**: gli aggiornamenti vengono scaricati e applicati automaticamente durante il processo di distribuzione di Windows Autopilot. 

Non sono ancora disponibili aggiornamenti. Per ulteriori informazioni, vedere di seguito.

## <a name="new-in-windows-10-version-2004"></a>Novità in Windows 10 versione 2004

Con questa versione, è possibile configurare l'ibrido [basato sugli utenti](user-driven.md) di Windows autopilot Azure Active Directory join con supporto VPN. Questo supporto viene anche sottoportato a backporting in Windows 10, versione 1909 e 1903.

Se si configurano le impostazioni della lingua nel profilo di Autopilot e il dispositivo è connesso a Ethernet, tutti gli scenari ignoreranno la lingua, le impostazioni locali e le pagine della tastiera. Nelle versioni precedenti, questa era supportata solo con i profili di distribuzione automatica.

## <a name="new-in-windows-10-version-1903"></a>Novità in Windows 10 versione 1903

[Windows Autopilot per la distribuzione del guanto bianco](white-glove.md) è una novità di Windows 10, versione 1903. Vedere il video seguente:

<br>

> [!VIDEO https://www.youtube.com/embed/nE5XSOBV0rI]

Inoltre, una novità di questa versione di Windows:
- La pagina relativa allo stato della registrazione di Intune (ESP) ora tiene traccia delle estensioni di gestione di Intune.
- [Cortana VoiceOver e riconoscimento vocale durante la configurazione guidata](windows-autopilot-scenarios.md#cortana-voiceover-and-speech-recognition-during-oobe) sono disabilitati per impostazione predefinita per tutti gli SKU di Windows 10 Pro Education e Enterprise.
- [Windows Autopilot si aggiorna autonomamente durante la configurazione guidata](windows-autopilot-scenarios.md#windows-autopilot-is-self-updating-during-oobe). A partire da Windows 10, la versione 1903, gli aggiornamenti critici e funzionali di Autopilot verranno avviati automaticamente durante la configurazione guidata.
- Windows Autopilot imposta il livello di dati di diagnostica su Full in Windows 10 versione 1903 e successive durante la configurazione guidata. 

## <a name="new-in-windows-10-version-1809"></a>Novità in Windows 10 versione 1809

La modalità di [distribuzione automatica](self-deploying.md) di Windows Autopilot consente un'esperienza di provisioning del dispositivo zero touch. È sufficiente accendere il dispositivo, connetterlo all'Ethernet e il dispositivo è completamente configurato da Windows Autopilot. Questa funzionalità di distribuzione automatica rimuove la necessità corrente di interagire con l'utente finale premendo il pulsante "Avanti" durante il processo di distribuzione. 

È possibile usare la modalità di distribuzione automatica di Windows Autopilot per registrare il dispositivo in un tenant AAD, iscriversi al provider MDM dell'organizzazione ed eseguire il provisioning di criteri e applicazioni, il tutto senza l'autenticazione utente o l'interazione dell'utente necessaria. 

>[!NOTE]
>La finestra 10, versione 1903 o successiva è necessaria per usare la modalità di distribuzione automatica a causa di problemi con l'attestazione del dispositivo TPM in Windows 10, versione 1809.

## <a name="related-topics"></a>Argomenti correlati

[Novità di Microsoft Intune](https://docs.microsoft.com/intune/whats-new)<br>
[Novità in Windows 10](https://docs.microsoft.com/windows/whats-new/)
