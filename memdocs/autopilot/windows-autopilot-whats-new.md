---
title: Novità di Windows Autopilot
ms.reviewer: ''
manager: laurawi
description: Leggi le notizie e le risorse sugli aggiornamenti più recenti e le versioni precedenti di Windows Autopilot.
keywords: MDM, installazione, Windows, Windows 10, OOBE, gestione, distribuzione, Autopilot, ZTD, zero-touch, partner, msfb, Intune
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
ms.openlocfilehash: 736e01696cf503b63762c32a9acee3cb68c1e241
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/09/2020
ms.locfileid: "89606558"
---
# <a name="windows-autopilot-whats-new"></a>Windows Autopilot: novità

**Si applica a**

- Windows 10

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
- Windows Autopilot imposta il livello di dati di diagnostica su completo durante la configurazione guidata nei dispositivi che eseguono Windows 10 versione 1903 o successiva. 

## <a name="new-in-windows-10-version-1809"></a>Novità in Windows 10 versione 1809

La modalità di [distribuzione automatica](self-deploying.md) di Windows Autopilot è un processo di provisioning di dispositivi con zero touch. È sufficiente accendere il dispositivo, connettersi a Ethernet e Autopilot configura automaticamente il dispositivo. Gli utenti finali non devono premere il pulsante "Avanti" durante il processo di distribuzione. 

È possibile usare la modalità di distribuzione automatica di Windows Autopilot per registrare il dispositivo in un tenant AAD, iscriversi al provider MDM dell'organizzazione ed effettuare il provisioning di criteri e applicazioni. Non è richiesta l'autenticazione utente o l'interazione dell'utente.

>[!NOTE]
>La finestra 10, versione 1903 o successiva è necessaria per usare la modalità di distribuzione automatica a causa di problemi con l'attestazione del dispositivo TPM in Windows 10, versione 1809.

## <a name="related-topics"></a>Argomenti correlati

[Novità di Microsoft Intune](/intune/whats-new)<br>
[Novità in Windows 10](/windows/whats-new/)
