---
title: Informazioni sulle restrizioni sul limite di dispositivi in Intune e Azure
titleSuffix: ''
description: Informazioni sulle differenze tra le restrizioni sul limite di dispositivi in Intune e Azure AD.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 04/12/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 63c9d9e4752e4b0d317667162255e368fc5a099c
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/26/2020
ms.locfileid: "88908555"
---
# <a name="understand-intune-and-azure-ads-device-limit-restrictions"></a>Informazioni sulle restrizioni sul limite di dispositivi in Intune e Azure AD

Le restrizioni sul limite di dispositivi possono essere configurate tramite:
- Registrazione di Intune
- Registrazioni aggiunte ad Azure Active Directory (AD) o registrazioni ad Azure AD

Il presente articolo chiarisce quando vengono applicati questi limiti in base alla configurazione dell'utente.

## <a name="intune-device-limit-restrictions"></a>Restrizioni sul limite di dispositivi in Intune

Le restrizioni sul limite di dispositivi in Intune servono a impostare il numero massimo di dispositivi che un utente può controllare (impostazione massima: 15 dispositivi). Per impostare il **Limite di dispositivi**, accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Dispositivi** > **Restrizioni registrazione**. Per altre informazioni, vedere [Creare una restrizione sul limite di dispositivi](enrollment-restrictions-set.md#create-a-device-limit-restriction)

## <a name="azure-device-limit-restriction"></a>Restrizioni sul limite di dispositivi in Azure

Le restrizioni sul limiti di dispositivi in Azure servono a impostare il numero massimo di dispositivi aggiunti o registrati in Azure AD. Per impostare il **Numero massimo di dispositivi per utente**, accedere al portale di Azure > **Azure Active Directory** > **Dispositivi**. Per altre informazioni, vedere [Configurare le impostazioni del dispositivo](/azure/active-directory/devices/device-management-azure-portal)

## <a name="settings-applied-based-on-user-affinity"></a>Impostazioni applicate in base all'affinità utente

Se sono state impostate le restrizioni sul limite di dispositivi sia in Intune che in Azure, la tabella seguente mostra gli elementi applicati in base alle impostazioni di affinità utente.

| Piattaforma per i dispositivi | Affinità utente | Applicazione in Azure | Applicazione in Intune |
| ----- | ----- | ----- | ----- | ----- |
| Profilo di lavoro di Android Enterprise | Sì | Sì | Sì|
| Dispositivi dedicati Android Enterprise | No | No | No |
| Android Enterprise completamente gestito | Sì | Sì | Sì |
| Amministratore dispositivo Android | Sì | Sì | Sì |
| Amministratore dispositivo Android DEM | No | | No | 
| iOS/macOS BYOD | Sì | Sì | Sì |
| Registrazione automatica del dispositivo (ADE) per iOS/macOS | Sì | Sì | Sì |
| iOS/macOS ADE | No | Sì | No |
| Windows BYOD | Sì | Sì | Sì |
| Solo Windows MD | | Sì | Sì |
| Aggiunto a Windows Azure AD| Sì | Sì | No |
| Windows Autopilot | Sì | Sì | No |
| Aggiunto a Windows Azure AD ibrido | No | No | Sì |
| Co-gestione Windows | No | Sì | No |
| Windows DEM | No | Sì | No |
| Registrazione in blocco di Windows | No | Sì | No |


## <a name="android-and-ios-devices"></a>Dispositivi Android e iOS

### <a name="ios-or-android-devices-example-1"></a>Dispositivi iOS o Android, esempio 1

- L'impostazione **Numero massimo di dispositivi per utente** di Azure è impostata su 3.
- L'impostazione **Limite di dispositivi** di Intune è impostata su 5.
 
**Risultato:** il numero massimo è da considerarsi per utente. Ad esempio, se si registrano tre dispositivi in Intune, la registrazione di Azure del quarto dispositivo avrà esito negativo a causa delle impostazioni per limitare il numero di registrazioni dei dispositivi.

### <a name="ios-or-android-devices-example-2"></a>Dispositivi iOS o Android, esempio 2

- L'impostazione **Numero massimo di dispositivi per utente** di Azure è impostata su 20.
- L'impostazione **Limite di dispositivi** di Intune è impostata su 2.

**Risultato:** è possibile registrare correttamente due dispositivi. La registrazione di eventuali dispositivi aggiuntivi in Intune verrà bloccata. La registrazione automatica del dispositivo senza affinità utente è limitata dai limiti di registrazione dei dispositivi di Azure anche se non è associata a un utente.

## <a name="windows-devices"></a>Dispositivi Windows

Le restrizioni sul limite di dispositivi di Intune non si applicano ai tipi di registrazione di Windows seguenti:
- Registrazioni con co-gestione
- Registrazioni di oggetto Criteri di gruppo (GPO)
- Registrazioni aggiunte ad Azure AD
- Registrazioni in blocco aggiunte ad Azure AD
- Registrazioni di AutoPilot
- Registrazioni del manager di registrazione dispositivi

Non è possibile far rispettare le restrizioni sul limite di dispositivi per questi tipi di registrazione perché sono considerati scenari di dispositivi condivisi. È possibile impostare limiti rigidi per questi tipi di registrazione in Azure Active Directory.

Per la restrizione del limite di dispositivi in Azure, l'impostazione **Numero massimo di dispositivi per utente** si applica sia ai dispositivi aggiunti ad Azure AD che a quelli registrati in Azure AD. L'impostazione non si applica invece ai dispositivi ibridi aggiunti ad Azure AD.

### <a name="windows-10-example-1"></a>Windows 10, esempio 1

- L'impostazione **Numero massimo di dispositivi per utente** di Azure è impostata su 5.
- L'impostazione **Limite di dispositivi** di Intune è impostata su 3.
- I dispositivi sono ibridi aggiunti ad Azure AD e registrati automaticamente (configurati come GPO).

**Risultato:** poiché la registrazione è inviata tramite un oggetto Criteri di gruppo, il limite di registrazione di dispositivi in Azure non viene applicato.  Anche la restrizione del limite di dispositivi in Intune non è applicabile.

### <a name="windows-10-example-2"></a>Windows 10, esempio 2

- L'impostazione **Numero massimo di dispositivi per utente** di Azure è impostata su 5.
- L'impostazione **Limite di dispositivi** di Intune è impostata su 2.
- I dispositivi sono aggiunti a un dominio locale e registrati tramite **Impostazioni** > **Accedi all'azienda o all'istituto di istruzione** > **Connetti**.

**Risultato:** è possibile registrare solo due dispositivi prima che siano bloccati. È possibile registrare fino a cinque dispositivi.


## <a name="next-steps"></a>Passaggi successivi

- [Creare una restrizione sul limite di dispositivi.](/azure/active-directory/devices/device-management-azure-portal#configure-device-settings)
- [Configurare le impostazioni del dispositivo in Azure.](enrollment-restrictions-set.md#create-a-device-limit-restriction)
- [Altre informazioni sulla registrazione e l'aggiunta a un dominio.](/azure/active-directory/devices/overview#getting-devices-in-azure-ad)