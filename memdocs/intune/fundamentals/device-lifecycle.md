---
title: Panoramica del ciclo di vita di Microsoft Intune MDM
description: Informazioni su come Intune consente di gestire i dispositivi per l'intero ciclo di vita, dalla registrazione alla configurazione fino al ritiro finale.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 12/04/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0c8d60a4a943ba2af9ea99f9eb887a9b77a49fcf
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88693506"
---
# <a name="overview-of-the-microsoft-intune-mobile-device-management-mdm-lifecycle"></a>Panoramica del ciclo di vita di gestione di dispositivi mobili (MDM) di Microsoft Intune

Tutti i dispositivi gestiti hanno un *ciclo di vita*. Intune può aiutare a gestire il ciclo di vita del dispositivo, dalla registrazione alla configurazione e alla protezione fino al ritiro del dispositivo stesso quando non è più necessario. Ecco un esempio: un iPad acquistato dall'azienda deve prima essere registrato con l'account Microsoft Intune per consentire all'azienda di gestirlo, quindi deve essere configurato in base alle esigenze dell'azienda e i dati archiviati su di esso da un utente devono essere protetti, infine quando l'iPad non è più necessario, è indispensabile [ritirarlo o cancellarne](https://docs.microsoft.com/mem/intune/remote-actions/devices-wipe) tutti i dati sensibili.

![Ciclo di vita del dispositivo](./media/device-lifecycle/device-lifecycle.png "Ciclo di vita del dispositivo Intune")

## <a name="enroll"></a>Registrazione

Le moderne strategie di gestione di dispositivi mobili (MDM) riguardano una vasta gamma di telefoni, tablet e PC (iOS/iPadOS, Android, Windows e Mac OS X). Se si deve poter gestire il dispositivo, come nel caso dei dispositivi aziendali, il primo passaggio consiste nella [registrazione del dispositivo](../enrollment/device-enrollment.md). È anche possibile gestire i PC Windows registrandoli con Intune (MDM) oppure [installando il software client di Intune](manage-windows-pcs-with-microsoft-intune.md).

## <a name="configure"></a>Configura

La registrazione dei dispositivi costituisce il primo passaggio. Per poter usufruire di tutte le offerte di Intune e verificare che i dispositivi siano protetti e conformi agli standard aziendali, è possibile scegliere tra una vasta gamma di criteri che consentono di configurare quasi ogni aspetto correlato al funzionamento dei dispositivi gestiti. Ad esempio, gli utenti devono usare una password per i dispositivi che contengono dati aziendali? È possibile impostare questo requisito. È disponibile una rete Wi-Fi aziendale? È possibile configurarla automaticamente. Di seguito sono descritti i tipi di opzioni di configurazione disponibili:

- [**Configurazione del dispositivo**](../configuration/device-profiles.md). Questi criteri consentono di configurare le caratteristiche e le funzionalità dei dispositivi gestiti. Si potrebbe ad esempio richiedere l'uso di una password nei telefoni Android o disabilitare l'uso della fotocamera negli iPhone.
- [**Accesso alle risorse aziendali**](../configuration/device-profiles.md). Quando si consente agli utenti di accedere ai dati aziendali da un dispositivo personale, possono emergere alcuni rischi. Ad esempio, come è possibile garantire che tutti i dispositivi che devono accedere alla posta elettronica aziendale siano configurati correttamente? Come si può garantire l'accesso degli utenti alla rete aziendale con una connessione VPN senza conoscere le complesse impostazioni sottostanti? Con Intune è possibile semplificare il processo configurando automaticamente i dispositivi gestiti per l'accesso alle risorse aziendali comuni.
- [**Criteri di gestione di PC Windows (con il software client di Intune)** ](common-windows-pc-management-tasks-with-the-microsoft-intune-computer-client.md). Mentre la registrazione dei PC Windows con Intune fornisce la maggior parte delle funzionalità di gestione dei dispositivi, Intune continua a supportare la gestione dei PC Windows con il software client di Intune. Per altre informazioni su alcune delle attività che è possibile eseguire con i PC, iniziare da qui.

## <a name="protect"></a>Protezione

Al giorno d'oggi la protezione dei dispositivi da accessi non autorizzati è una delle attività più importanti. Oltre agli elementi descritti nel passaggio **Configurazione** del ciclo di vita del dispositivo, Intune fornisce altre funzionalità che consentono di proteggere i dispositivi gestiti da accessi non autorizzati o attacchi dannosi:

- [**Multi-Factor Authentication**](../enrollment/multi-factor-authentication.md). L'aggiunta di un ulteriore livello di autenticazione agli accessi dell'utente contribuisce a rendere i dispositivi ancora più sicuri. Molti dispositivi supportano l'autenticazione a più fattori che richiede un secondo livello di autenticazione per l'accesso, ad esempio una telefonata o un SMS.
- [**Impostazioni di Windows Hello for Business**](../protect/windows-hello.md). Windows Hello for Business è un metodo di accesso alternativo che consente agli utenti di usare un *movimento*, ad esempio un'impronta digitale o Windows Hello, per eseguire l'accesso senza dover immettere una password.
- [**Criteri per proteggere i PC Windows (con il software client di Intune)** ](policies-to-protect-windows-pcs-in-microsoft-intune.md). Quando si gestiscono i PC Windows con il software client di Intune, sono disponibili criteri che consentono di controllare le impostazioni per Endpoint Protection, gli aggiornamenti software e Windows Firewall nei PC gestiti.

## <a name="retire"></a>Ritiro

È opportuno [ritirare o cancellare](../remote-actions/device-management.md) il dispositivo quando viene smarrito o rubato e deve essere sostituito oppure quando gli utenti si trasferiscono altrove. Esistono diversi modi per eseguire questa operazione: dal ripristino del dispositivo alla rimozione dalla gestione o alla cancellazione dei dati aziendali contenuti.

## <a name="next-steps"></a>Passaggi successivi

- Informazioni sulla [gestione dei dispositivi in Microsoft Intune](../remote-actions/device-management.md)
