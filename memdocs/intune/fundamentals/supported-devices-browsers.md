---
title: Sistemi operativi e browser supportati da Microsoft Intune
titleSuffix: ''
description: Questo articolo elenca le piattaforme di dispositivi e i browser supportati per la gestione dei dispositivi in Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/19/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 5d1ac59c-a885-4276-8576-f3cf81c2d268
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: a8bfddd247f2f86d8fc5a9162a5c68efd5e7ffb5
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88996283"
---
# <a name="supported-operating-systems-and-browsers-in-intune"></a>Sistemi operativi e browser supportati in Intune

Prima di installare Microsoft Intune, controllare quali sistemi operativi e browser sono supportati.

Per informazioni sull'installazione di Intune nel proprio dispositivo, vedere [Usare dispositivi gestiti per lo svolgimento del lavoro](../user-help/use-managed-devices-to-get-work-done.md) e [Requisiti di configurazione di rete di Intune e larghezza di banda](network-bandwidth-use.md).

Per altre informazioni sul supporto del provider di servizi di configurazione, vedere [Configuration service provider reference](/windows/client-management/mdm/configuration-service-provider-reference) (Informazioni di riferimento sul provider di servizi di configurazione).

> [!NOTE]
> Intune richiede ora Android 5.x (Lollipop) o versioni successive per l'accesso alle risorse aziendali da applicazioni e dispositivi tramite l'app Portale aziendale per Android e Intune App SDK per Android. Questo requisito NON si applica ai dispositivi Teams basati su Polycom Android che eseguono la versione 4.4. Questi dispositivi continueranno a essere supportati. 

## <a name="intune-supported-operating-systems"></a>Sistemi operativi supportati di Intune

È possibile gestire i dispositivi che eseguono i sistemi operativi seguenti:

[!INCLUDE [mdm-supported-devices](../includes/mdm-supported-devices.md)]

### <a name="supported-samsung-knox-standard-devices"></a>Dispositivi Samsung Knox Standard supportati

Per evitare errori di attivazione Knox che impediscono la registrazione MDM, l'app Portale aziendale tenta l'attivazione di Samsung Knox durante la registrazione MDM solo se il dispositivo da attivare è presente nell'[elenco dei dispositivi Knox supportati](https://www.samsungknox.com/knox-supported-devices/knox-workspace). I dispositivi che non supportano l'attivazione di Samsung Knox vengono registrati come dispositivi Android standard. Tra i dispositivi Samsung, non tutti hanno un numero di modello che supporta Knox. Verificare la compatibilità Knox presso il rivenditore del dispositivo prima dell'acquisto e della distribuzione di dispositivi Samsung.

> [!NOTE]
> Per la registrazione dei dispositivi Samsung Knox potrebbe essere necessario [abilitare l'accesso ai server Samsung](https://support.samsungknox.com/hc/articles/115013833108-Our-corporate-devices-are-behind-a-firewall-How-do-I-enable-Knox-Workspace-devices-to-contact-Samsung-servers).

L'elenco seguente riporta i modelli di dispositivi Samsung che non supportano Knox. L'app Portale aziendale per Android li registra come dispositivi Android nativi:

| **Nome dispositivo** | **Numeri modello dispositivo** |
| --- | --- |
| Galaxy Avant | SM-G386T |
| Galaxy Core 2/Core 2 Duos | SM-G355H<br>SM-G355M |
| Galaxy Core Lite | SM-G3588V |
| Galaxy Core Prime | SM-G360H |
| Galaxy Core LTE | SM-G386F<br>SM-G386W |
| Galaxy Grand | GT-I9082L<br>GT-I9082<br>GT-I9080L |
| Galaxy Grand 3 | SM-G7200 |
| Galaxy Grand Neo | GT-I9060I |
| Galaxy Grand Prime Value Edition | SM-G531H |
| Galaxy J Max | SM-T285YD |
| Galaxy J1 | SM-J100H<br>SM-J100M<br>SM-J100ML |
| Galaxy J1 Ace | SM-J110F<br>SM-J110H |
| Galaxy J1 Mini | SM-J105M |
| Galaxy J2/J2 Pro | SM-J200H<br>SM-J210F |
| Galaxy J3 | SM-J320F<br>SM-J320FN<br>SM-J320H<br>SM-J320M |
| Galaxy K Zoom | SM-C115 |
| Galaxy Light | SGH-T399N |
| Galaxy Note 3 | SM-N9002<br>SM-N9009 |
| Galaxy Note 7/Note 7 Duos | SM-N930S<br>SM-N9300<br>SM-N930F<br>SM-N930T<br>SM-N9300<br>SM-N930F<br>SM-N930S<br>SM-N930T |
| Galaxy Note 10.1 3G | SM-P602 |
| Galaxy S2 Plus | GT-I9105P |
| Galaxy S3 Mini | SM-G730A<br>SM-G730V |
| Galaxy S3 Neo | GT-I9300<br>GT-I9300I |
| Galaxy S4 | SM-S975L |
| Galaxy S4 Neo | SM-G318ML |
| Galaxy S5 | SM-G9006W |
| Galaxy S6 Edge | 404SC |
| Galaxy Tab A 7.0&quot; | SM-T280<br>SM-T285 |
| Galaxy Tab 3 7&quot;/Tab 3 Lite 7&quot; | SM-T116<br>SM-T210<br>SM-T211 |
| Galaxy Tab 3 8.0&quot; | SM-T311 |
| Galaxy Tab 3 10.1&quot; | GT-P5200<br>GT-P5210<br>GT-P5220 |
| Galaxy Trend 2 Lite | SM-G318H |
| Galaxy V Plus | SM-G318HZ |
| Galaxy Young 2 Duos | SM-G130BU |

### <a name="windows-pc-software-client"></a>Client software PC Windows

Un [client software Intune](manage-windows-pcs-with-microsoft-intune.md) può essere distribuito e installato nei PC di Windows come metodo alternativo di registrazione. Questa funzionalità è disponibile solo nel portale classico di Intune. È possibile usare il client software di Intune per gestire PC con Windows 10 e versioni successive, ad eccezione dell'edizione Windows 10 Home.

> [!Note]
> Microsoft ha annunciato che il supporto di Windows 7 terminerà il 14 gennaio 2020. In questa data, terminerà anche il supporto di Intune per i dispositivi che eseguono Windows 7.
>
> Per altre informazioni, vedere [Modifica prevista per Intune: fine del supporto per Windows 7](whats-new.md#windows-7-ends-extended-support).
>
> Microsoft Intune ritirerà il supporto per la console di Intune basata su Silverlight il 15 ottobre 2020. Questo ritiro include l'interruzione del supporto per il client software PC configurato della console Silverlight (chiamato anche agente del computer).
>
> Per altre informazioni, vedere [Fine del supporto di Microsoft Intune per la console di amministrazione basata su Silverlight](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Take-Action-Microsoft-Intune-ending-support-for-the-Silverlight/ba-p/916249).

<!--  ### Exchange ActiveSync management

You can manage [Exchange ActiveSync devices](../enrollment/device-enrollment.md#mobile-device-management-with-exchange-activesync-and-intune) from the Intune console. This option provides a limited set of management capabilities when compared to the other methods. See [Capabilities of built-in Mobile Device Management in Microsoft 365](https://support.office.com/article/Capabilities-of-built-in-Mobile-Device-Management-for-Office-365-a1da44e5-7475-4992-be91-9ccec25905b0) for a list of supported devices.  -->

## <a name="intune-supported-web-browsers"></a>Web browser supportati da Intune

Per le svariate attività amministrative è necessario usare uno dei siti Web di amministrazione seguenti.

- [Interfaccia di amministrazione di Microsoft 365](https://go.microsoft.com/fwlink/p/?LinkId=698854)
- [Portale di Azure](https://portal.azure.com/)

Per questi portali sono supportati i browser seguenti:

- Microsoft Edge (versione più recente)
- Microsoft Internet Explorer 11
- Safari (versione più recente, solo Mac)
- Chrome (versione più recente)
- Firefox (versione più recente)

### <a name="intune-classic-portal"></a>Portale classico di Intune

Il portale classico di Intune viene usato solo per gestire i dispositivi registrati con il client software per PC di Intune (https://manage.microsoft.com). Per il portale classico di Intune è richiesto il supporto di un browser Silverlight.

La console di Intune è supportata dai browser Silverlight seguenti:

- Internet Explorer 10 o versione successiva
- Google Chrome (versioni precedenti alla versione 42)
- Mozilla Firefox con Silverlight abilitato (versioni precedenti alla versione 56)

> [!Note]
> Microsoft Edge e i browser per dispositivi mobili non sono supportati per il portale classico di Intune perché non supportano [Microsoft Silverlight](/previous-versions/windows/silverlight/dotnet-windows-silverlight/cc838158(v=vs.95)).

Solo gli utenti con autorizzazioni di amministratore del servizio o di amministratore tenant con il ruolo Amministratore globale possono accedere al portale. Per accedere alla console di amministrazione, è necessario che l'account abbia una licenza per l'uso di Intune e lo stato di accesso **Consentito**.