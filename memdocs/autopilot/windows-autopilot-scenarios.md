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
ms.openlocfilehash: 1755399ad67cd073c71f2a26ef4305bec5a53f51
ms.sourcegitcommit: 7037d2cd6b4e3d3e75471db33f22d475dfd89f5e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/19/2020
ms.locfileid: "90814873"
---
# <a name="windows-autopilot-scenarios-and-capabilities"></a>Scenari e funzionalità di Windows Autopilot

**Si applica a: Windows 10**

## <a name="scenarios"></a>Scenari

Windows Autopilot supporta un elenco in continua crescita di scenari in cui le organizzazioni necessitano in genere. Queste esigenze variano in base a:
- Tipo di organizzazione.
- Stato di avanzamento in Windows 10.
- Per quanto riguarda la [transizione alla gestione moderna](/windows/client-management/manage-windows-10-in-your-organization-modern-management).

In questa guida vengono descritti gli scenari di Windows Autopilot seguenti:

| Scenario | Altre informazioni |
| --- | --- |
| Distribuire e configurare i dispositivi in modo che un utente finale possa configurarlo autonomamente | [Modalità definita dall'utente di Windows Autopilot](user-driven.md) |
| Distribuire i dispositivi da configurare automaticamente per l'uso condiviso, come chiosco multimediale o come dispositivo di firma digitale.| [Modalità di distribuzione automatica di Windows Autopilot](self-deploying.md) |
| Ridistribuire un dispositivo in uno stato pronto per l'azienda.| [Ripristino di Windows Autopilot](windows-autopilot-reset.md) |
| Eseguire il pre-provisioning di un dispositivo con le applicazioni, i criteri e le impostazioni aggiornate.| [Trattamento esclusivo](white-glove.md) |
| Distribuire Windows 10 in un dispositivo Windows 7 o 8,1 esistente | [Windows Autopilot per dispositivi esistenti](existing-devices.md) |

Questi scenari sono riepilogati nel video seguente.

&nbsp;

> [!video https://www.microsoft.com/videoplayer/embed/RE4Ci1b?autoplay=false]

## <a name="windows-autopilot-capabilities"></a>Funzionalità di Windows Autopilot

### <a name="windows-autopilot-is-self-updating-during-oobe"></a>Windows Autopilot si aggiorna autonomamente durante la configurazione guidata

Per i dispositivi Windows 10, versione 1903 e successive, gli aggiornamenti funzionali e critici di Autopilot vengono scaricati automaticamente durante la configurazione guidata dopo:
- Il dispositivo è connesso a una rete.
- Sono stati completati gli [aggiornamenti critici del driver e della patch di Windows Zero-Day (ZDP)](/windows-hardware/customize/desktop/windows-updates-during-oobe) .

Non è possibile rifiutare esplicitamente questi aggiornamenti di Autopilot perché sono necessari per la distribuzione di Windows Autopilot. Windows avvisa l'utente che il dispositivo sta controllando, scaricando e installando gli aggiornamenti.

Per ulteriori informazioni, vedere l' [aggiornamento di Windows Autopilot](autopilot-update.md).

### <a name="cortana-voiceover-and-speech-recognition-during-oobe"></a>Cortana VoiceOver e riconoscimento vocale durante la configurazione guidata

In Windows 10, versione 1903 e successive, Cortana VoiceOver e riconoscimento vocale durante la configurazione guidata sono DISABILITAti per impostazione predefinita. Questa impostazione predefinita si applica a tutti gli SKU di Windows 10 Pro, Education ed Enterprise.

È anche possibile abilitare Cortana VoiceOver e riconoscimento vocale durante la configurazione guidata creando la chiave del registro di sistema seguente. Questa chiave non esiste per impostazione predefinita:

HKLM\Software\Microsoft\Windows\CurrentVersion\OOBE\EnableVoiceForAllEditions

Il valore della chiave è un DWORD con **0** = disabled e **1** = Enabled.

| Valore | Descrizione |
| --- | --- |
| 0 | Cortana VoiceOver è disabilitato |
| 1 | Cortana VoiceOver è abilitato |
| Nessun valore | Il dispositivo eseguirà il fallback al comportamento predefinito dell'edizione |

Per modificare questo valore di chiave, usare lo strumento WCD per creare come PPKG come descritto [qui](/windows/configuration/wcd/wcd-oobe#nforce).

### <a name="bitlocker-encryption"></a>Crittografia BitLocker

Con Windows Autopilot è possibile configurare le impostazioni di crittografia di BitLocker da applicare prima dell'avvio della crittografia automatica. Per ulteriori informazioni, vedere [impostazione dell'algoritmo di crittografia BitLocker per i dispositivi Autopilot](bitlocker.md)

## <a name="related-topics"></a>Argomenti correlati

[Windows Autopilot: novità](windows-autopilot-whats-new.md)