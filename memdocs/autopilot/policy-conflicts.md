---
title: Conflitti tra i criteri di Windows Autopilot
ms.reviewer: ''
manager: laurawi
description: Informazioni sui conflitti di criteri che possono verificarsi durante la distribuzione di Windows Autopilot.
keywords: MDM, installazione, Windows, Windows 10, OOBE, gestione, distribuzione, Autopilot, ZTD, zero-touch, partner, msfb, Intune
ms.technology: windows
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: mtniehaus
ms.author: mniehaus
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: 1f839f128dc869f7c9a4619237de0c33a21d66e1
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/09/2020
ms.locfileid: "89606581"
---
# <a name="windows-autopilot---policy-conflicts"></a>Windows Autopilot-conflitti tra criteri

**Si applica a**

- Windows 10

Per Windows 10 è disponibile un numero significativo di impostazioni dei criteri, tra cui:
- Criteri MDM nativi
- Impostazioni di criteri di gruppo (con supporto di ADMX)

Alcune impostazioni dei criteri possono causare problemi in alcuni scenari di Windows Autopilot. Questi problemi possono verificarsi a causa del modo in cui i criteri modificano il comportamento di Windows 10. Se si riscontra uno di questi problemi, rimuovere il criterio in questione per risolvere il problema.

<table>
<th>Criteri<th>Altre informazioni

<tr><td width="50%">Criteri di restrizione/ <a href="https://docs.microsoft.com/windows/client-management/mdm/devicelock-csp">password</a> del dispositivo</td>
<td>L'esperienza predefinita (OOBE) o l'accesso automatico desktop utente può avere esito negativo quando un dispositivo viene riavviato durante il riavvio della pagina relativa allo stato della registrazione del dispositivo (ESP). Questo errore può verificarsi quando vengono applicati determinati <a href="https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock">criteri DeviceLock</a> a un dispositivo. Tali criteri possono includere:<ul><li>Lunghezza minima password e complessità password</li><li>Eventuali impostazioni di criteri di gruppo simili (incluse quelle che disabilitano l'accesso automatico)</li></ul>
Questo possibile errore è particolarmente vero per gli scenari di chiosco multimediale in cui vengono generate automaticamente le password.</td>

<tr><td width="50%"><a href="/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions">Comportamento della richiesta di elevazione</a> di sicurezza di Windows 10/amministratore
<br>Baseline per la sicurezza di Windows 10/ <a href="https://docs.microsoft.com/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions">Richiedi la modalità Approvazione amministratore per gli amministratori</a></td>
<td>È possibile che vengano visualizzate altre richieste durante la modifica delle impostazioni di controllo dell'account utente durante la configurazione guidata usando la pagina relativa allo stato della registrazione del dispositivo (ESP). Un numero maggiore di richieste è più probabile se il dispositivo viene riavviato dopo l'applicazione dei criteri. Per ovviare a questo problema, i criteri possono essere assegnati agli utenti anziché ai dispositivi, in modo che vengano applicati in un secondo momento nel processo.</td>

<tr><td width="50%">Restrizioni del dispositivo/Cloud and Storage/ <a href="https://docs.microsoft.com/mem/intune/configuration/device-restrictions-windows-10#cloud-and-storage">Assistente per l'accesso all'account Microsoft</a></td>
<td>Se si imposta questo criterio su "disabilitato", il servizio Assistente per l'accesso Microsoft (wlidsvc) verrà disabilitato. Questo servizio è richiesto da Windows Autopilot per ottenere il profilo di Windows Autopilot.</td>

</table>

## <a name="related-topics"></a>Argomenti correlati

[Risoluzione dei problemi di Windows Autopilot](troubleshooting.md)
