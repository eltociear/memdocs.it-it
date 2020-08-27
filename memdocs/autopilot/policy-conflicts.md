---
title: Conflitti tra i criteri di Windows Autopilot
ms.reviewer: ''
manager: laurawi
description: Informazioni sui problemi noti che possono verificarsi durante la distribuzione di Windows Autopilot.
keywords: MDM, installazione, Windows, Windows 10, OOBE, gestione, distribuzione, Autopilot, ZTD, zero-touch, partner, msfb, Intune
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
ms.openlocfilehash: 23c5c9c0fd025279f1c97b6f19673f9e8b527adb
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/26/2020
ms.locfileid: "88907979"
---
# <a name="windows-autopilot---policy-conflicts"></a>Windows Autopilot-conflitti tra criteri

**Si applica a**

- Windows 10

Per Windows 10 è disponibile un numero significativo di impostazioni dei criteri, sia come criteri MDM nativi che come impostazioni di criteri di gruppo (con supporto di ADMX). Alcuni di questi possono causare problemi in determinati scenari di Windows Autopilot in seguito alla modifica del comportamento di Windows 10. Se si verifica uno di questi problemi, rimuovere il criterio in questione per risolvere il problema.

<table>
<th>Criteri<th>Ulteriori informazioni

<tr><td width="50%">Criteri di restrizione/ <a href="https://docs.microsoft.com/windows/client-management/mdm/devicelock-csp">password</a> del dispositivo</td>
<td>Quando determinati <a href="https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock">criteri di DeviceLock</a>, ad esempio la lunghezza minima della password e la complessità delle password, o eventuali impostazioni di criteri di gruppo simili, incluse quelle che disabilitano l'accesso automatico, vengono applicate a un dispositivo e il dispositivo viene riavviato durante la pagina relativa allo stato della registrazione del dispositivo, la configurazione guidata o l'accesso automatico desktop utente può avere esito negativo.  Questo vale soprattutto per gli scenari in modalità tutto schermo in cui vengono generate automaticamente le password.</td>

<tr><td width="50%"><a href="/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions">Comportamento della richiesta di elevazione</a> di sicurezza di Windows 10/amministratore
<br>Baseline per la sicurezza di Windows 10/ <a href="https://docs.microsoft.com/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions">Richiedi la modalità Approvazione amministratore per gli amministratori</a></td>
<td>Quando si modificano le impostazioni di controllo dell'account utente durante la configurazione guidata usando la pagina relativa allo stato della registrazione del dispositivo (ESP), è possibile che si verifichino richieste di controllo dell'account utente aggiuntive, soprattutto se il dispositivo viene riavviato dopo l'applicazione di questi criteri, consentendo loro di rendere effettivi.  Per ovviare a questo problema, i criteri possono essere assegnati agli utenti anziché ai dispositivi, in modo che vengano applicati in un secondo momento nel processo.</td>

<tr><td width="50%">Restrizioni del dispositivo/Cloud and Storage/ <a href="https://docs.microsoft.com/mem/intune/configuration/device-restrictions-windows-10#cloud-and-storage">Assistente per l'accesso all'account Microsoft</a></td>
<td>Se si imposta questo criterio su "disabilitato", il servizio Assistente per l'accesso Microsoft (wlidsvc) verrà disabilitato.  Questo servizio è richiesto da Windows Autopilot per ottenere il profilo di Windows Autopilot.</td>

</table>

## <a name="related-topics"></a>Argomenti correlati

[Risoluzione dei problemi di Windows Autopilot](troubleshooting.md)