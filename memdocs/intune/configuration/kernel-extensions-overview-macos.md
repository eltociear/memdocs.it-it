---
title: Creare le estensioni del sistema e del kernel macOS con Microsoft Intune - Azure | Microsoft Docs
titleSuffix: ''
description: Aggiungere o creare un profilo di dispositivo macOS che configura le estensioni del sistema o le estensioni del kernel per consentire l'override dell'utente, aggiunge l'identificatore del team e un identificatore del bundle e del team in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/07/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: fce8218c9f8fb8757f0aef892f0854f1c386a8bd
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990296"
---
# <a name="add-macos-system-and-kernel-extensions-in-intune"></a>Aggiungere le estensioni del sistema e del kernel macOS in Intune

> [!NOTE]
> Le estensioni del kernel macOS verranno sostituite con estensioni di sistema. Per altre informazioni, vedere [Suggerimento per il supporto: Uso delle estensioni di sistema anziché delle estensioni del kernel per macOS Catalina 10.15 in Intune](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-using-system-extensions-instead-of-kernel-extensions/ba-p/1191413).

Nei dispositivi macOS è possibile aggiungere estensioni del kernel ed estensioni del sistema. Sia le estensioni del kernel sia le estensioni del sistema consentono agli utenti di installare estensioni delle app che incrementano la capacità nativa del sistema operativo. Le estensioni del kernel eseguono il codice a livello del kernel. Le estensioni del sistema vengono eseguite in uno spazio utente strettamente controllato.

Per aggiungere le estensioni a cui è sempre consentito il caricamento nei dispositivi, usare Microsoft Intune. Intune usa "profili di configurazione" per creare e personalizzare queste impostazioni per le esigenze dell'organizzazione. Dopo aver aggiunto queste funzionalità in un profilo, eseguire il push del profilo o distribuirlo nei dispositivi macOS nell'organizzazione.

Questo articolo descrive le estensioni del sistema e le estensioni del kernel. Inoltre, illustra come creare un profilo di configurazione del dispositivo usando le estensioni in Intune.

## <a name="system-extensions"></a>Estensioni del sistema

Le estensioni del sistema vengono eseguite nello spazio dell'utente e non accedono al kernel. L'obiettivo è aumentare la protezione, garantire un maggior controllo a livello dell'utente finale e limitare gli attacchi a livello del kernel. Queste estensioni possono essere:

- estensioni del driver, inclusi i driver per USB, le schede di interfaccia di rete (NIC), i controller seriali e dispositivi di interfaccia umana (HID)
- estensioni di rete, inclusi i filtri per contenuto, i proxy DNS e i client VPN
- estensioni di sicurezza degli endpoint, inclusi il rilevamento di endpoint, la risposta dell'endpoint e l'antivirus

Le estensioni del sistema sono incluse nel bundle di un'app e vengono installate dall'app.

Per altre informazioni sulle estensioni del sistema, vedere [estensioni del sistema](https://developer.apple.com/documentation/systemextensions) (si aprirà il sito Web di Apple).

## <a name="kernel-extensions"></a>Estensioni del kernel

Le estensioni del kernel aggiungono funzionalità a livello del kernel. Queste funzionalità accedono a parti del sistema operativo a cui i normali programmi non possono accedere. È possibile che l'organizzazione abbia esigenze o requisiti specifici che non sono disponibili in un'app, una funzionalità del dispositivo e così via.

Si dispone, ad esempio, di un programma di scansione antivirus che analizza il dispositivo alla ricerca di contenuto dannoso. È possibile aggiungere l'estensione del kernel di questo programma di scansione antivirus come estensione del kernel consentita in Intune. "Assegnare" quindi l'estensione ai dispositivi macOS.

Con questa funzionalità gli amministratori possono consentire agli utenti di eseguire l'override delle estensioni del kernel, aggiungere identificatori del team e aggiungere estensioni del kernel specifiche in Intune.

Per altre informazioni sulle estensioni del kernel, vedere [estensioni del kernel](https://developer.apple.com/library/archive/documentation/Darwin/Conceptual/KernelProgramming/Extend/Extend.html) (si aprirà il sito Web di Apple).

## <a name="prerequisites"></a>Prerequisiti

- Questa funzionalità si applica a:

  - macOS 10.13.2 e versioni successive (estensioni del kernel)
  - macOS 10.15 e versioni successive (estensioni del sistema)

  Da macOS 10.15 a macOS 10.15.4, le estensioni del kernel e le estensioni del sistema possono essere eseguite simultaneamente.

- Per usare questa funzionalità, i dispositivi devono essere:

  - Registrati in Intune tramite il Device Enrollment Program (DEP) di Apple. In [Registrare automaticamente i dispositivi macOS](../enrollment/device-enrollment-program-enroll-macos.md) sono disponibili altre informazioni.

    OPPURE

  - Registrati in Intune con "Registrazione approvata dall'utente" (termine Apple). In [Come prepararsi alle modifiche apportate alle estensioni del kernel in macOS High Sierra](https://support.apple.com/en-us/HT208019) sono disponibili altre informazioni. Si aprirà il sito Web di Apple.

## <a name="what-you-need-to-know"></a>Informazioni importanti

- È possibile aggiungere estensioni del kernel ed estensioni del sistema legacy non firmate.
- Assicurarsi di immettere l'identificatore del team e l'ID bundle corretti dell'estensione. Intune non convalida i valori immessi. Se si immettono informazioni errate, l'estensione non funzionerà nel dispositivo. Un identificatore del team è esattamente di 10 caratteri alfanumerici.

> [!NOTE]
> Apple ha rilasciato informazioni relative alla firma e all'autenticazione per tutto il software. In macOS 10.14.5 e versioni successive le estensioni del kernel distribuite tramite Intune non devono soddisfare i criteri di autenticazione di Apple.
>
> Per informazioni sui criteri di autenticazione e sugli eventuali aggiornamenti o modifiche, vedere le risorse seguenti:
>
> - [Autenticazione dell'app prima della distribuzione](https://developer.apple.com/documentation/security/notarizing_your_app_before_distribution) (si aprirà il sito Web di Apple) 
> - [Come prepararsi alle modifiche apportate alle estensioni del kernel in macOS High Sierra](https://support.apple.com/en-us/HT208019) (si aprirà il sito Web di Apple)

## <a name="create-the-profile"></a>Creare il profilo

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selezionare **Dispositivi** > **Profili di configurazione** > **Crea profilo**.
3. Immettere le proprietà seguenti:

    - **Piattaforma**: Selezionare **macOS**.
    - **Profilo**: selezionare **Estensioni**.

4. Selezionare **Crea**.
5. In **Informazioni di base** immettere le proprietà seguenti:

    - **Nome**: immettere un nome descrittivo per il criterio. Assegnare ai criteri nomi che possano essere identificati facilmente in un secondo momento. Ad esempio, un nome di criterio valido è **macOS: Aggiungere l'analisi antivirus alle estensioni del kernel nei dispositivi**.
    - **Descrizione**: immettere una descrizione del criterio. Questa impostazione è facoltativa ma consigliata.

6. Selezionare **Avanti**.

7. In **Impostazioni di configurazione** configurare le impostazioni:

    - [macOS](kernel-extensions-settings-macos.md)

8. Selezionare **Avanti**.
9. In **Tag ambito** (facoltativo) assegnare un tag per filtrare il profilo a gruppi IT specifici, ad esempio `US-NC IT Team` o `JohnGlenn_ITDepartment`. Per altre informazioni sui tag di ambito, vedere [Usare il controllo degli accessi in base al ruolo (RBAC) e i tag di ambito per l'infrastruttura IT distribuita](../fundamentals/scope-tags.md).

    Selezionare **Avanti**.

10. In **Assegnazioni** selezionare gli utenti o i gruppi che riceveranno il profilo. Per altre informazioni sull'assegnazione di profili, vedere [Assegnare profili utente e dispositivo](device-profile-assign.md).

    Selezionare **Avanti**.

11. In **Rivedi e crea** rivedere le impostazioni. Quando si seleziona **Crea**, le modifiche vengono salvate e il profilo viene assegnato. Il criterio viene visualizzato anche nell'elenco dei profili.

## <a name="next-steps"></a>Passaggi successivi

Dopo averlo creato, il profilo è pronto per l'assegnazione. [Assegnare il profilo](device-profile-assign.md) e [monitorarne lo stato](device-profile-monitor.md).
