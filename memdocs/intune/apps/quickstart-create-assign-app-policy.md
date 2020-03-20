---
title: Guida introduttiva - Creare e assegnare un criterio di protezione delle app
titleSuffix: Microsoft Intune
description: In questa guida introduttiva si userà Microsoft Intune per creare e assegnare un criterio di protezione delle app.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 11/26/2019
ms.topic: quickstart
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 2586fce0-5dca-4686-b9c4-791778838401
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: fb8b5eae3c88664caff76da597fc3ab9111f989c
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79343856"
---
# <a name="quickstart-create-and-assign-an-app-protection-policy"></a>Guida introduttiva: Creare e assegnare un criterio di protezione delle app

In questa guida introduttiva si userà Intune per creare e assegnare un criterio di protezione delle app a un'app client nel dispositivo dell'utente finale. Intune usa i criteri di protezione delle app per verificare che le app soddisfino i requisiti di protezione dei dati dell'organizzazione.

Se non si dispone di una sottoscrizione Intune, è possibile [iscriversi per ottenere un account di prova gratuito](../fundamentals/free-trial-sign-up.md).

## <a name="prerequisites"></a>Prerequisiti

- Per completare questa guida introduttiva è necessario [creare un utente](../fundamentals/quickstart-create-user.md), [creare un gruppo](../fundamentals/quickstart-create-group.md), [registrare un dispositivo](../enrollment/quickstart-setup-auto-enrollment.md) e [aggiungere e assegnare un'app](quickstart-add-assign-app.md).

## <a name="sign-in-to-intune"></a>Accedere a Intune

Accedere a [Intune](https://aka.ms/intuneportal) come [amministratore globale o come amministratore del servizio Intune](../fundamentals/users-add.md#types-of-administrators). Se è stata creata una sottoscrizione della versione di valutazione di Intune, l'account creato con tale sottoscrizione sarà un amministratore globale.

## <a name="create-an-app-protection-policy"></a>Creare un criterio di protezione delle app

Usare la procedura seguente per creare un criterio di protezione delle app:

1. In [Intune](https://aka.ms/intuneportal) selezionare **App** > **Criteri di protezione delle app** > **Crea criterio**. 
2. Immettere le informazioni seguenti:

    - **Nome**: *Protezione del contenuto Windows 10*
    - **Descrizione**: *Gli utenti associati a questo criterio non potranno tagliare, copiare o incollare contenuti tra l'app assegnata e altre app non gestite nel dispositivo.*
    - **Piattaforma**: *Windows 10*
    - **Stato registrazione**: *Con registrazione*

3. Selezionare **App protette** per selezionare le app che devono soddisfare il criterio.
4. Fare clic su **Aggiungi app**.
5. In **App consigliate** selezionare **Word Mobile**.
5. Fare clic su **OK** > **OK**. 
6. Selezionare **Impostazioni obbligatorie** per configurare l'app.
7. Fare clic su **Consenti sostituzioni** per impostare la modalità di Windows Information Protection. La selezione di questa opzione impedisce che i dati aziendali escano dall'app protetta.
8. Fare clic su **OK** > **Crea**.

I criteri di protezione delle app sono ora visibili in Intune.

### <a name="assign-the-app-protection-policy"></a>Assegnare i criteri di protezione delle app

Dopo aver creato un criterio di protezione delle app in Intune, è possibile assegnarlo ai gruppi. 

Usare la procedura seguente per assegnare il criterio di protezione delle app:

1. In [Intune](https://aka.ms/intuneportal) selezionare **Intune** > **App** > **Criteri di protezione delle app**. 
2. Selezionare il criterio di protezione delle app creato in precedenza. In questa guida introduttiva il criterio è **Protezione del contenuto Windows 10**.
3. Selezionare **Assegnazioni**.
4. Fare clic su **Selezionare i gruppi da includere** nella scheda **Includi**.
5. Selezionare **Contoso Testers** (Tester Contoso) come gruppo da includere.
6. Fare clic su **Seleziona** > **Salva**. 

Il criterio di protezione delle app è stato assegnato.

> [!NOTE]
> I criteri di protezione delle app possono essere applicati solo ai gruppi che contengono utenti e non ai gruppi che contengono dispositivi.

## <a name="next-steps"></a>Passaggi successivi

In questa guida introduttiva è stato creato e assegnato un criterio di protezione delle app. Gli utenti dell'app a cui è stato assegnato questo criterio non potranno tagliare, copiare o incollare contenuti tra l'app assegnata e altre app non gestite nel dispositivo. Questo tipo di protezione consente di proteggere i dati dell'organizzazione. Per altre informazioni sui criteri di protezione delle app, vedere [Che cosa sono i criteri di protezione delle app?](app-protection-policy.md)

Per seguire questa serie di guide introduttive di Intune, continuare con la guida introduttiva che segue.

> [!div class="nextstepaction"]
> [Avvio rapido: Creare e assegnare un ruolo personalizzato](../fundamentals/create-custom-role.md)
