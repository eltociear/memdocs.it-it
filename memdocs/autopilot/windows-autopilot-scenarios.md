---
title: Scenari e funzionalità di Windows Autopilot
description: Segui diversi scenari tipici di distribuzione di Windows Autopilot, ad esempio la ridistribuzione di un dispositivo in uno stato pronto per l'azienda.
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
ms.openlocfilehash: 063d791b4b2373f195625c996c6b4a1667015ad3
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/04/2020
ms.locfileid: "87756493"
---
# <a name="windows-autopilot-scenarios-and-capabilities"></a>Scenari e funzionalità di Windows Autopilot

**Si applica a: Windows 10**

## <a name="scenarios"></a>Scenari

Windows Autopilot include il supporto per un elenco in continua crescita di scenari, progettati per supportare esigenze aziendali comuni. Queste esigenze possono variare in base al tipo di organizzazione e al passaggio a Windows 10 e [alla gestione moderna](https://docs.microsoft.com/windows/client-management/manage-windows-10-in-your-organization-modern-management).

In questa guida vengono descritti gli scenari di Windows Autopilot seguenti:

| Scenario | Ulteriori informazioni |
| --- | --- |
| Distribuire i dispositivi da configurare da un membro dell'organizzazione e configurati per tale persona | [Modalità definita dall'utente di Windows Autopilot](user-driven.md) |
| Distribuire i dispositivi da configurare automaticamente per l'uso condiviso, come chiosco multimediale o come dispositivo di firma digitale.| [Modalità di distribuzione automatica di Windows Autopilot](self-deploying.md) |
| Ridistribuire un dispositivo in uno stato pronto per l'azienda.| [Ripristino di Windows Autopilot](windows-autopilot-reset.md) |
| Eseguire il pre-provisioning di un dispositivo con le applicazioni, i criteri e le impostazioni aggiornate.| [Trattamento esclusivo](white-glove.md) |
| Distribuire Windows 10 in un dispositivo Windows 7 o 8,1 esistente | [Windows Autopilot per dispositivi esistenti](existing-devices.md) |

Questi scenari sono riepilogati nel video seguente.

&nbsp;

> [!video https://www.microsoft.com/videoplayer/embed/RE4Ci1b?autoplay=false]

## <a name="windows-autopilot-capabilities"></a>Funzionalità di Windows Autopilot

### <a name="windows-autopilot-is-self-updating-during-oobe"></a>Windows Autopilot si aggiorna autonomamente durante la configurazione guidata

A partire da Windows 10, versione 1903, gli aggiornamenti critici e funzionali di Autopilot inizieranno a essere scaricati automaticamente durante la configurazione guidata dopo che un dispositivo è connesso a una rete e gli [aggiornamenti critici del driver e della patch di Windows Zero-Day (ZDP)](https://docs.microsoft.com/windows-hardware/customize/desktop/windows-updates-during-oobe) sono stati completati. L'utente o l'amministratore IT non può rifiutare esplicitamente questi aggiornamenti di Autopilot perché sono necessari per il corretto funzionamento della distribuzione di Windows Autopilot.  Windows segnalerà all'utente che il dispositivo sta controllando, scaricando e installando gli aggiornamenti.

Per ulteriori informazioni, vedere l' [aggiornamento di Windows Autopilot](autopilot-update.md) .

### <a name="cortana-voiceover-and-speech-recognition-during-oobe"></a>Cortana VoiceOver e riconoscimento vocale durante la configurazione guidata

In Windows 10, la versione 1903 e successive Cortana VoiceOver e riconoscimento vocale durante la configurazione guidata è DISABILITAto per impostazione predefinita per tutti gli SKU di Windows 10 Pro, Education ed Enterprise.

È anche possibile abilitare Cortana VoiceOver e riconoscimento vocale durante la configurazione guidata creando la chiave del registro di sistema seguente. Questa chiave non esiste per impostazione predefinita:

HKLM\Software\Microsoft\Windows\CurrentVersion\OOBE\EnableVoiceForAllEditions

Il valore della chiave è un DWORD con **0** = disabled e **1** = Enabled.

| valore | Description |
| --- | --- |
| 0 | Cortana VoiceOver è disabilitato |
| 1 | Cortana VoiceOver è abilitato |
| Nessun valore | Il dispositivo eseguirà il fallback al comportamento predefinito dell'edizione |

Per modificare questo valore di chiave, usare lo strumento WCD per creare come PPKG come descritto [qui](https://docs.microsoft.com/windows/configuration/wcd/wcd-oobe#nforce).

### <a name="bitlocker-encryption"></a>Crittografia BitLocker

Con Windows Autopilot è possibile configurare le impostazioni di crittografia di BitLocker da applicare prima dell'avvio della crittografia automatica. Per ulteriori informazioni, vedere [impostazione dell'algoritmo di crittografia BitLocker per i dispositivi Autopilot](bitlocker.md)

## <a name="related-topics"></a>Argomenti correlati

[Windows Autopilot: novità](windows-autopilot-whats-new.md)
