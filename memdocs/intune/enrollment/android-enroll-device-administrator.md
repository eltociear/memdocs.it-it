---
title: Registrazione di tipo amministratore di dispositivi Android in Microsoft Intune
titleSuffix: ''
description: Registrare dispositivi Android in Intune tramite la registrazione di tipo amministratore di dispositivi.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 07/23/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8e44fa26c84537fdcf801192ce8cc22790f320b9
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "80438797"
---
# <a name="android-device-administrator-enrollment"></a>Registrazione di tipo amministratore di dispositivi Android

L'amministratore di dispositivi Android, a volte denominato gestione Android "legacy" e rilasciato con Android 2.2, è una modalità di gestione dei dispositivi Android. Funzionalità di gestione migliorate, tuttavia, sono ora disponibili in [Android Enterprise](https://www.android.com/enterprise/management/) (con la versione Android 5.0). Con l'obiettivo di passare a una gestione dei dispositivi moderna, più ricca e sicura, Google sta riducendo il supporto per l'amministratore di dispositivi nelle nuove versioni di Android.

Pertanto, al fine di evitare questa riduzione di funzionalità, non è consigliabile registrare nuovi dispositivi tramite il processo di amministratore di dispositivi descritto di seguito.

Per gli stessi motivi, è anche consigliabile eseguire la migrazione dei dispositivi dalla gestione di tipo amministratore di dispositivi se questi verranno aggiornati ad Android 10. 

Se si decide che gli utenti possano comunque registrare i propri dispositivi Android con la gestione di tipo amministratore di dispositivi, passare alla sezione successiva.  

Per altre informazioni sulle funzionalità di Android Enterprise di Google, vedere questi articoli:
- [Indicazioni di Google per la migrazione da amministratore di dispositivi ad Android Enterprise](http://static.googleusercontent.com/media/android.com/en/enterprise/static/2016/pdfs/enterprise/Android-Enterprise-Migration-Bluebook_2019.pdf)
- [Documentazione di Google sul piano per deprecare l'API amministratore di dispositivi](https://developers.google.com/android/work/device-admin-deprecation)

## <a name="set-up-device-administrator-enrollment"></a>Configurare la registrazione di tipo amministratore di dispositivi

1. Per preparare la gestione dei dispositivi mobili è necessario impostare l'autorità per la gestione dei dispositivi mobili su **Microsoft Intune**. Vedere [Impostare l'autorità MDM](../fundamentals/mdm-authority-set.md) per le istruzioni. Questo elemento viene impostato una sola volta quando si configura Intune per la gestione dei dispositivi mobili per la prima volta.
2. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) e scegliere > **Dispositivi** > **Android** > **Registrazione Android** > **Dispositivi personali e di proprietà aziendale con privilegi di amministratore di dispositivi** > **Usa l'amministratore di dispositivi per gestire i dispositivi**.
3. [Informare gli utenti su come registrare i loro dispositivi](../user-help/enroll-device-android-company-portal.md).  

Dopo che un utente ha eseguito la registrazione, è possibile iniziare a gestirne i dispositivi in Intune con attività quali, ad esempio, [l'assegnazione dei criteri di conformità](../protect/compliance-policy-create-android.md), [la gestione delle app](../apps/app-management.md) e così via.

Per informazioni su altre attività dell'utente, vedere gli articoli seguenti:
- [Informazioni sull'uso di Microsoft Intune per gli utenti finali](../fundamentals/end-user-educate.md)
- [Uso del dispositivo Android con Intune](https://docs.microsoft.com/mem/intune/user-help/why-enroll-android-device)


## <a name="block-device-administrator-enrollment"></a>Bloccare la registrazione di tipo amministratore di dispositivi
Per bloccare la registrazione dei dispositivi di tipo amministratore di dispositivi Android o soltanto quelli di proprietà personale, vedere [Impostare le restrizioni sul tipo di dispositivi](enrollment-restrictions-set.md).


## <a name="next-steps"></a>Passaggi successivi
- [Assegnare criteri di conformità](../protect/compliance-policy-create-android.md)
- [Gestione delle app](../apps/app-management.md)
