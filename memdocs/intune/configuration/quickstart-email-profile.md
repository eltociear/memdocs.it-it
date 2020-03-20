---
title: 'Avvio rapido: creare un profilo di posta elettronica del dispositivo per dispositivi iOS/iPadOS'
titleSuffix: Microsoft Intune
description: Informazioni su come usare Microsoft Intune per creare un profilo di posta elettronica del dispositivo affinché i dispositivi iOS/iPadOS possano connettersi in modo sicuro alla posta elettronica aziendale.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 02/18/2020
ms.topic: quickstart
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7a6345afe4258ff7141228a7284932f083791c70
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79361484"
---
# <a name="quickstart-create-an-email-device-profile-for-iosipados"></a>Guida introduttiva: Creare un profilo di posta elettronica del dispositivo per iOS/iPadOS

In questo avvio rapido verrà illustrato come creare un profilo di posta elettronica per i dispositivi iOS/iPadOS. Questo profilo specifica le impostazioni necessarie per l'app di posta elettronica predefinita per consentire al dispositivo iOS/iPadOS di connettersi alla posta elettronica aziendale. I profili di posta elettronica del dispositivo facilitano l'omogeneità delle impostazioni tra i dispositivi e consentono agli utenti finali di accedere alla posta elettronica aziendale dai dispositivi personali senza alcuna configurazione manuale. Per proteggere ulteriormente la posta elettronica, è possibile usare un profilo di posta elettronica per determinare se i dispositivi sono conformi e quindi configurare l'accesso condizionale per consentire ai soli dispositivi conformi di accedere alla posta elettronica. Per altre informazioni sui profili di posta elettronica, vedere [Come configurare le impostazioni di posta elettronica in Microsoft Intune](email-settings-configure.md)

Se non si dispone di una sottoscrizione Intune, è possibile [iscriversi per ottenere un account di prova gratuito](../fundamentals/free-trial-sign-up.md).

## <a name="sign-in-to-intune"></a>Accedere a Intune

Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) come Amministratore globale o come Amministratore del servizio Intune. Se è stata creata una sottoscrizione della versione di valutazione di Intune, l'account creato con tale sottoscrizione sarà un amministratore globale.

## <a name="create-an-iosipados-email-profile"></a>Creare un profilo di posta elettronica iOS/iPadOS

1. Selezionare **Dispositivi** > **Profili di configurazione** > **Crea profilo**.

   ![Creare un profilo di posta elettronica per iOS/iPadOS in Intune](./media/quickstart-email-profile/ios-create-profile.png)

2. In **Nome** immettere un nome descrittivo per il nuovo profilo. Per questo esempio, immettere **Dispositivi iOS richiedono posta elettronica aziendale**.
3. Immettere le seguenti informazioni per il profilo:
    - Per **Descrizione** immettere **Richiedi che i dispositivi iOS/iPadOS usino la posta elettronica aziendale**.
    - Per **Piattaforma**, selezionare **iOS/iPadOS**.
    - Per **Tipo di profilo** selezionare **Posta elettronica**.

        ![Creare un profilo di posta elettronica da usare con i dispositivi iOS/iPadOS in Intune](./media/quickstart-email-profile/ios-email-profile-name.png)

4. Selezionare **Impostazioni** e immettere le impostazioni seguenti, lasciando i valori predefiniti per le altre:
   - **Server di posta elettronica**: per questa guida introduttiva, immettere **outlook.office365.com**. Questa impostazione specifica la posizione di Exchange (URL) del server di posta elettronica che l'app di posta elettronica iOS/iPadOS userà per connettersi alla posta elettronica.
   - **Nome account**: immettere **Indirizzo di posta elettronica dell'azienda**.
   - **Attributo nome utente da AAD**: questo nome è l'attributo che Intune ottiene da Azure Active Directory (Azure AD). Intune genera in modo dinamico il nome utente usato da questo profilo basandosi su questo nome. Per questo argomento di avvio rapido si presuppone che si voglia usare **Nome dell'entità utente** come nome utente per il profilo (ad esempio, user1@contoso.com).
   - **Attributo indirizzo di posta elettronica da AAD**: questa impostazione è l'indirizzo di posta elettronica di Azure AD che verrà usato per accedere a Exchange. Per questa guida introduttiva, selezionare **Nome dell'entità utente**.
   - **Metodo di autenticazione**: per questa guida introduttiva, selezionare **Nome utente e password**. In alternativa, è possibile scegliere **Certificato** se è già stato impostato un certificato per Intune.

        ![Creare un profilo di posta elettronica per l'uso con iOS/iPadOS](./media/quickstart-email-profile/ios-email-profile.png)

5. Selezionare **OK** > **Crea**. Il nuovo profilo compare nell'elenco dei profili con il dashboard visualizzato così da poter monitorare il modo in cui il profilo è stato assegnato ai dispositivi iOS/iPadOS e agli utenti iOS/iPadOS.
6. Selezionare **Assegnazioni**.
7. Selezionare la scheda **Includi** e quindi selezionare **Tutti gli utenti e tutti i dispositivi**. 
8. Selezionare **Salva**.

## <a name="clean-up-resources"></a>Pulizia delle risorse

Se non si prevede di usare il profilo creato per esercitazioni o test aggiuntivi, è possibile eliminarlo ora.

1. In Intune selezionare **Configurazione del dispositivo** e quindi **Profili**.
2. Selezionare il profilo di test appena creato **Dispositivi iOS/iPadOS richiedono posta elettronica aziendale**.
3. Selezionare i punti di sospensione ( **...** ) accanto al profilo, quindi fare clic su **Elimina**.

## <a name="next-steps"></a>Passaggi successivi

In questo avvio rapido è stato creato un profilo di posta elettronica per i dispositivi iOS/iPadOS. Ora è possibile usare questo profilo per determinare se un dispositivo iOS/iPadOS è conforme ai criteri di conformità che contrassegnano come non conformi tutti i dispositivi iOS/iPadOS che non corrispondono al profilo. Per un'ulteriore protezione, è possibile creare un criterio di accesso condizionale che impedisce ai dispositivi iOS/iPadOS non conformi di accedere alla posta elettronica. Per altre informazioni sui criteri di conformità dei dispositivi, vedere [Introduzione ai criteri di conformità dei dispositivi in Intune](../protect/device-compliance-get-started.md).

> [!div class="nextstepaction"]
> [Esercitazione: Proteggere la posta elettronica di Exchange Online nei dispositivi gestiti](../protect/tutorial-protect-email-on-enrolled-devices.md)
