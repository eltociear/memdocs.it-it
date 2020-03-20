---
title: Avvio rapido - Criteri di conformità delle password per dispositivi Android
titleSuffix: Microsoft Intune
description: In questo avvio rapido si userà Microsoft Intune per impostare la lunghezza della password obbligatoria per i dispositivi Android.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 11/21/2019
ms.topic: quickstart
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 81b4fa08-5333-4c54-9f49-8db5f6984ed2
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b7330f50c61679ab91b5f364f718cefcc456435f
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79351266"
---
# <a name="quickstart-create-a-password-compliance-policy-for-android-devices"></a>Guida introduttiva: Creare un criterio di conformità della password per i dispositivi Android

In questo avvio rapido si userà Microsoft Intune per richiedere agli utenti del personale che usa Android di immettere una password di una lunghezza specifica prima di ottenere l'accesso alle informazioni nei dispositivi Android.

I criteri di conformità del dispositivo in Intune specificano le regole e le impostazioni che i dispositivi devono soddisfare per essere considerati conformi. È possibile usare criteri di conformità con l'accesso condizionale per consentire o bloccare l'accesso alle risorse aziendali. È anche possibile ottenere i report di dispositivo e intraprendere azioni per la mancata conformità.

> [!IMPORTANT]
> Oltre alle impostazioni della password, è consigliabile prendere in considerazione altre impostazioni di sicurezza del sistema per proteggere la forza lavoro. Per altre informazioni, vedere [Impostazioni di sicurezza del sistema](compliance-policy-create-android-for-work.md).

Se non si dispone di una sottoscrizione Intune, è possibile [iscriversi per ottenere un account di prova gratuito](../fundamentals/free-trial-sign-up.md).

## <a name="sign-in-to-intune"></a>Accedere a Intune

Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) come [Amministratore globale](../fundamentals/users-add.md#types-of-administrators) o come [Amministratore del servizio](../fundamentals/users-add.md#types-of-administrators) Intune.

## <a name="create-a-device-compliance-policy"></a>Creare criteri di conformità dei dispositivi

Creare questi criteri per richiedere agli utenti di immettere una password di una lunghezza specifica prima di ottenere l'accesso alle informazioni nei dispositivi Android.

1. In Intune selezionare **Dispositivi** > **Criteri di conformità** > **Crea criterio**.

2. Aggiungere **Conformità Android** come **Nome**. Aggiungere anche una **Descrizione**.

3. Per **Piattaforma** selezionare **Android Enterprise**.

4. Per **Tipo di profilo** selezionare **Profilo di lavoro**.

5. Selezionare **Impostazioni** > **Sicurezza del sistema** per visualizzare il pannello **Sicurezza del sistema** per Android.

6. Per **Richiedi una password per sbloccare i dispositivi mobili** selezionare **Rendi obbligatorio**.

7. In **Tipo di password richiesto** selezionare **Almeno numerico**.

8. Per **Lunghezza minima password** immettere **6**.

    ![Screenshot della creazione di un gruppo in Microsoft Intune](./media/quickstart-set-password-length-android/quickstart-set-password-length-android-01.png)

9. Al termine, selezionare **OK** > **OK** > **Crea** per creare il criterio.

Dopo averlo creato, il criterio sarà visualizzato nell'elenco dei criteri di conformità dei dispositivi.

## <a name="clean-up-resources"></a>Pulizia delle risorse

Quando non è più necessario, eliminare il criterio. A tale scopo, selezionare il criterio di conformità e fare clic su **Elimina**.

## <a name="next-steps"></a>Passaggi successivi

In questa guida introduttiva è stato usato Intune per creare criteri di conformità per i dispositivi Android della forza lavoro per richiedere una password di almeno sei caratteri. Per altre informazioni sulla creazione dei criteri di conformità, vedere [Introduzione ai criteri di conformità dei dispositivi in Intune](device-compliance-get-started.md).

Per seguire questa serie di guide introduttive di Intune, continuare con la guida introduttiva che segue.

> [!div class="nextstepaction"]
> [Avvio rapido: Inviare notifiche a dispositivi non conformi](quickstart-send-notification.md)
