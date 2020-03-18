---
title: Proteggere i dispositivi con Microsoft Intune
titleSuffix: Microsoft Intune
description: Informazioni su alcuni dei metodi che consentono a Intune di proteggere i dispositivi da accessi non autorizzati e altre minacce.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/19/2018
ms.topic: conceptual
ms.subservice: protect
ms.service: microsoft-intune
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: c9ee00d13b32e1f52937489b86d29f075e5f580a
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79352306"
---
# <a name="protect-devices-with-microsoft-intune"></a>Proteggere i dispositivi con Microsoft Intune

Microsoft Intune consente di proteggere i dispositivi gestiti e i dati archiviati in tali dispositivi.

## <a name="device-configuration"></a>Configurazione del dispositivo
I [criteri di configurazione](../configuration/device-profiles.md) di Intune consentono di proteggere e configurare i dispositivi controllando una vasta gamma di funzionalità e impostazioni. Ad esempio:

- È possibile limitare l'uso delle funzionalità hardware del dispositivo, ad esempio la fotocamera o il Bluetooth.
- È possibile configurare app conformi e non conformi. Se viene installata un'app non conforme si riceverà un avviso (e in alcune piattaforme è possibile bloccare l'installazione).

## <a name="reset-passcodes-when-users-are-locked-out-of-their-devices"></a>Reimpostare i passcode quando gli utenti vengono bloccati dai dispositivi
Poiché il primo passaggio nella protezione dei dati aziendali nei dispositivi mobili prevede l'uso di un passcode per usare il dispositivo, a volte è necessario [reimpostare un passcode](../remote-actions/device-passcode-reset.md) o aiutare un utente a farlo rimuovendo il passcode o impostando in remoto un passcode temporaneo. È anche possibile [bloccare un dispositivo in remoto](../remote-actions/device-remote-lock.md) se viene smarrito o rubato.

## <a name="retire-devices-and-remove-data"></a>Ritirare i dispositivi e rimuovere i dati
Quando un dispositivo deve essere [rimosso dalla gestione Intune](../remote-actions/devices-wipe.md) (ad esempio, un utente lascia l'azienda o il dispositivo viene smarrito o rubato), è probabile che sia necessario rimuovere i dati dal dispositivo. Intune offre un'ampia gamma di metodi per garantire la sicurezza dei dati aziendali.

## <a name="require-devices-to-be-compliant"></a>Richiedere la conformità dei dispositivi
Intune offre [criteri di conformità dei dispositivi](device-compliance-get-started.md) che consentono di valutare (e in alcuni casi correggere) i dispositivi non conformi alle regole specificate. Ad esempio, è possibile ottenere report per:
- dispositivi iOS/iPadOS jailbroken
- dispositivi crittografati o non crittografati
- l'integrità dei dispositivi Windows 10 (come stabilito dal servizio di attestazione dell'integrità).

## <a name="protect-apps-and-the-data-they-use"></a>Proteggere le app e i dati che usano
Windows Intune offre una gamma di funzionalità che consentono di proteggere le app e i relativi dati. Ad esempio, i criteri di gestione di applicazioni mobili (MAM) consentono di:
- impedire il backup dei dati da un'app protetta
- limitare le operazioni di copia e incolla in altre app
- richiedere un PIN per accedere a un'app. Per altre informazioni, vedere [Proteggere app e dati con Microsoft Intune](../apps/app-protection-policy.md).

## <a name="add-an-additional-layer-of-protection-to-devices"></a>Aggiungere un ulteriore livello di protezione ai dispositivi
[Multi-Factor Authentication (MFA)](../enrollment/multi-factor-authentication.md) costituisce un modo più sicuro per autenticare gli utenti di dispositivi in rete.  Con MFA, oltre a specificare nome utente e password, gli utenti devono confermare la propria identità con una telefonata o un SMS.

## <a name="control-windows-hello-for-business-settings-on-windows-devices"></a>Controllare le impostazioni di Windows Hello for Business nei dispositivi Windows
Con Intune è possibile eseguire l'integrazione con [Windows Hello for Business](windows-hello.md), un metodo di accesso alternativo per Windows 10 e versioni successive che usa Active Directory o un account di Azure Active Directory in sostituzione di una password, una smart card o una smart card virtuale.

## <a name="disable-activation-lock-on-ios-devices"></a>Disabilitare il blocco attivazione sui dispositivi iOS
Blocco attivazione è una funzionalità che consente di proteggere i dispositivi degli utenti. La funzionalità richiede agli utenti di immettere l'ID e la password Apple prima che chiunque possa cancellare o riattivare il dispositivo. Tuttavia questa funzionalità può causare problemi, ad esempio se l'utente lascia l'azienda senza rimuovere il blocco. [Disabilitare il blocco attivazione di iOS/iPadOS](../remote-actions/device-activation-lock-disable.md) consente di rimuovere il blocco dai dispositivi iOS/iPadOS con supervisione e quindi di riallocarli o cancellarli.

## <a name="next-steps"></a>Passaggi successivi

Scoprire di più su [Mobile Threat Defense](mobile-threat-defense.md)
