---
title: Criteri di configurazione per le app gestite senza registrazione dei dispositivi
titleSuffix: Microsoft Intune
description: Informazioni su come configurare i criteri per le app gestite senza registrazione dei dispositivi.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: E61C1618-79D0-41A1-B61F-4123FB6672FC
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b493443a86d7cd1769ce6f66c77acc87063521f6
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2020
ms.locfileid: "86461641"
---
# <a name="add-app-configuration-policies-for-managed-apps-without-device-enrollment"></a>Aggiungere criteri di configurazione delle app per le app gestite senza registrazione dei dispositivi

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

È possibile usare i criteri di configurazione delle app con le app gestite che supportano Intune App SDK anche su dispositivi non registrati. 

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Scegliere **App** > **Criteri di configurazione dell'app** > **Aggiungi** > **App gestite**.
3. Nella pagina **Informazioni di base** impostare i dettagli seguenti:
    - **Nome**: Il nome del profilo che verrà visualizzato nel portale di Azure.
    - **Descrizione**: La descrizione del profilo che verrà visualizzata nel portale di Azure.
    - **Tipo di registrazione del dispositivo**: sono selezionate le app gestite.
4. Scegliere **Selezionare app pubbliche** o **Selezionare app personalizzate** per scegliere l'app che si intende configurare. Selezionare l'app dall'elenco di app già approvate e sincronizzate con Intune.
5. Fare clic su **Avanti** per visualizzare la pagina **Impostazioni**.
6. La **pagina Impostazioni** include opzioni visualizzate in base all'app che si sta configurando:

    - **Impostazioni di configurazione generali** - Per ogni impostazione di configurazione generale supportata dall'app, digitare **Nome** e **Valore**. 
 
        Le app abilitate per Intune App SDK supportano le configurazioni in coppie chiave/valore. Per altre informazioni sulle configurazioni chiave-valore supportate, vedere la documentazione delle singole app. Si noti che è possibile usare token che verranno popolati in modo dinamico con i dati generati dall'applicazione. Per eliminare un'impostazione di configurazione generale, scegliere i puntini di sospensione ( **...** ) e selezionare **Elimina**. Per altre informazioni, vedere [Valori di configurazione per l'uso dei token](app-configuration-policies-managed-app.md#configuration-values-for-using-tokens). 

    - **Impostazioni di configurazione di Outlook** - Outlook per iOS e Android offre agli amministratori la possibilità di personalizzare la configurazione predefinita per diverse impostazioni in-app. Per altre informazioni, vedere [Outlook per iOS e Android - Scenari di configurazione delle app generali](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune#general-app-configuration-scenarios).
   
    - **S/MIME** - S/MIME (Secure Multipurpose Internet Mail Extensions) è una specifica che consente agli utenti di inviare e ricevere messaggi di posta elettronica con firma digitale e crittografati.
        - **Abilita S/MIME** - Specificare se i controlli S/MIME sono abilitati o meno durante la composizione di un messaggio di posta elettronica. Valore predefinito: **Non configurato**.
        - **Consenti all'utente di cambiare impostazione** - Specificare se l'utente è autorizzato a modificare l'impostazione. S/MIME deve essere abilitato. Valore predefinito: **Sì**.
        
    Per altre informazioni sulle impostazioni dei criteri di configurazione per l'app Outlook, vedere [Distribuzione delle impostazioni di configurazione delle app di Outlook per iOS e Android](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune).

7. Fare clic su **Avanti** per visualizzare la pagina **Assegnazioni**.
8. Fare clic su **Selezionare i gruppi da includere**.
9. Selezionare un gruppo nel riquadro **Selezionare i gruppi da includere** e fare clic su **Seleziona**.
10. Fare clic su **Selezionare i gruppi da escludere** per visualizzare il riquadro correlato.
11. Scegliere i gruppi da escludere e quindi fare clic su **Seleziona**.

    >[!NOTE]
    >Quando si aggiunge un gruppo, se sono già stati inclusi altri gruppi per un tipo di assegnazione specifico, tale gruppo risulterà preselezionato e non potrà essere modificato per gli altri tipi di assegnazione di inclusione. Di conseguenza, tale gruppo non potrà essere usato come gruppo escluso.

12. Fare clic su **Avanti** per visualizzare la pagina **Rivedi e crea**.
13. Fare clic su **Crea** per aggiungere i criteri di configurazione dell'app a Intune.

## <a name="configuration-values-for-using-tokens"></a>Valori di configurazione per l'uso dei token

Intune può generare token e inviarli all'app gestita. Se ad esempio la configurazione dell'app è in grado di usare un'impostazione di posta elettronica, è possibile aggiungere un indirizzo di posta elettronica dinamico usando un token. Digitare il nome previsto dall'app nel campo **Nome** e quindi digitare `\{\{mail\}\}` nel campo **Valore**.

Intune supporta i tipi di token seguenti nelle impostazioni di configurazione. Altre coppie chiave/valore personalizzate non sono supportate.

- \{\{userprincipalname\}\}, ad esempio John@contoso.com
- \{\{mail\}\}, ad esempio John@contoso.com
- \{\{partialupn\}\}, ad esempio John
- \{\{accountid\}\}, ad esempio fc0dc142-71d8-4b12-bbea-bae2a8514c81
- \{\{userid\}\}, ad esempio 3ec2c00f-b125-4519-acf0-302ac3761822
- \{\{username\}\}, ad esempio John Doe
- \{\{PrimarySMTPAddress\}\}, ad esempio testuser@ad.domain.com

> [!Note]  
> I caratteri \{\{ e \}\} vengono usati solo dai tipi di token e non devono essere usati per altri scopi.

## <a name="next-steps"></a>Passaggi successivi

Procedere ad [assegnare](apps-deploy.md) e [monitorare](apps-monitor.md) normalmente l'app.
