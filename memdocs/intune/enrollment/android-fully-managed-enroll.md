---
title: Configurare la registrazione in Intune per dispositivi Android Enterprise completamente gestiti
titleSuffix: Microsoft Intune
description: Informazioni su come registrare i dispositivi Android Enterprise completamente gestiti in Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 1/15/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: priyar
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 78ed3fe234fb4ab236fe35b5e1778582f3eb731d
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2020
ms.locfileid: "86461709"
---
# <a name="set-up-intune-enrollment-of-android-enterprise-fully-managed-devices"></a>Configurare la registrazione in Intune di dispositivi Android Enterprise completamente gestiti 

I dispositivi Android Enterprise completamente gestiti sono dispositivi di proprietà aziendale associati a un utente singolo e usati esclusivamente per lavoro e non per uso personale. Gli amministratori possono gestire interamente tali dispositivi e applicare controlli di criteri non disponibili nei profili di lavoro, ad esempio:
- Consentire l'installazione di app solo da Google Play gestito.
- Bloccare la disinstallazione di app gestite.
- Impedire agli utenti di ripristinare le impostazioni predefinite dei dispositivi e così via.

Intune facilita la distribuzione di app e impostazioni nei dispositivi Android Enterprise, inclusi i dispositivi Android Enterprise completamente gestiti. Per informazioni dettagliate su Android Enterprise, vedere [Android enterprise requirements](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012) (Requisiti di Android Enterprise).

## <a name="technical-requirements"></a>Requisiti tecnici

Per gestire dispositivi Android Enterprise completamente gestiti, è necessario un tenant autonomo di Intune. La gestione di dispositivi completamente gestiti non è disponibile nella console di gestione legacy di Silverlight.

Per essere gestiti come dispositivi Android Enterprise completamente gestiti, i dispositivi devono soddisfare i requisiti seguenti:

- Sistema operativo Android versione 6.0 e successive.
- I dispositivi devono eseguire una build di Android dotata di connettività Google Mobile Services (GMS). I dispositivi devono includere GMS e devono essere in grado di connettersi a GMS.

Se i requisiti precedenti vengono soddisfatti, non esistono limitazioni relative al produttore o all'OEM del dispositivo.

## <a name="set-up-android-enterprise-fully-managed-device-management"></a>Configurare la gestione di dispositivi Android Enterprise completamente gestiti

Per configurare la gestione di dispositivi Android Enterprise completamente gestiti, seguire questa procedura:

1. Per preparare la gestione dei dispositivi mobili, è necessario [impostare l'autorità per la gestione dei dispositivi mobili (MDM) su **Microsoft Intune**](../fundamentals/mdm-authority-set.md). Questa opzione viene impostata una sola volta, ovvero quando si configura per la prima volta Intune per la gestione dei dispositivi mobili.
2. [Connettere l'account del tenant di Intune all'account Android Enterprise](connect-intune-android-enterprise.md).
3. [Abilitare i dispositivi utente di proprietà aziendale](#enable-corporate-owned-user-devices)
4. [Registrare i dispositivi completamente gestiti](#enroll-the-fully-managed-devices).

### <a name="enable-corporate-owned-user-devices"></a>Abilitare i dispositivi utente di proprietà aziendale

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) e scegliere **Dispositivi** > **Android** > **Registrazione Android**  > **Dispositivi utente completamente gestiti di proprietà aziendale**.
2. In **Consenti agli utenti di registrare dispositivi utente di proprietà aziendale** scegliere **Sì**.

> [!NOTE]
> Se sono stati definiti criteri di accesso condizionale di Azure AD che usano il controllo concessione *Richiedi che i dispositivi siano contrassegnati come conformi* o un criterio di blocco e si applicano a **Tutte le app cloud**, **Android** e **Browser**, è necessario escludere l'app cloud **Microsoft Intune** da questi criteri. Ciò è necessario poiché il processo di installazione di Android usa una scheda di Chrome per autenticare gli utenti durante la registrazione. Per altre informazioni, vedere [Documentazione di accesso condizionale di Azure AD](https://docs.microsoft.com/azure/active-directory/conditional-access/).

Se impostata su **Sì**, questa impostazione rende disponibile per il tenant di Intune un token di registrazione (una stringa casuale) e un codice a matrice. Questo token di registrazione singola è valido per tutti gli utenti e non scade. A seconda del sistema operativo Android e della versione del dispositivo, per registrare il dispositivo è possibile usare il token o il codice a matrice.

## <a name="enroll-the-fully-managed-devices"></a>Registrare i dispositivi completamente gestiti
Ora è possibile [registrare i dispositivi completamente gestiti](android-dedicated-devices-fully-managed-enroll.md) (ma solo se non usano account DEM).

## <a name="next-steps"></a>Passaggi successivi
- [Aggiungere criteri di configurazione dei dispositivi Android Enterprise completamente gestiti](../configuration/device-restrictions-android-for-work.md#fully-managed-dedicated-and-corporate-owned-work-profile)
- [Configurare criteri di configurazione delle app per dispositivi Android Enterprise completamente gestiti](../apps/app-configuration-policies-use-android.md)

