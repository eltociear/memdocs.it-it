---
title: Configurare Desktop Analytics
titleSuffix: Configuration Manager
description: Guida pratica per la configurazione e l'onboarding in Desktop Analytics.
ms.date: 02/06/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 7ff8d453-f24d-4230-a116-585190a663fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: a90f3260782f08fdf8f7424a95e09b34e38e97d3
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268149"
---
# <a name="how-to-set-up-desktop-analytics"></a>Come configurare Desktop Analytics

Usare questa procedura per accedere a Desktop Analytics e configurarlo nell'abbonamento. L'organizzazione deve configurare Desktop Analytics una sola volta.  

> [!Important]  
> Per informazioni sui prerequisiti generali per Desktop Analytics con Configuration Manager, vedere[Prerequisiti](overview.md#prerequisites).  

## <a name="initial-onboarding"></a>Onboarding iniziale

1. Aprire il [portale di Desktop Analytics](https://aka.ms/desktopanalytics) in Gestione dei dispositivi per Microsoft 365 come utente con il ruolo **Amministratore globale**. Selezionare **Inizio**. In alternativa, nella console di Configuration Manager passare all'area di lavoro **Raccolta software**, selezionare il nodo **Manutenzione di Desktop Analytics** e selezionare **Pianifica le distribuzioni**.

2. Nella pagina **Accetta il contratto di servizio** esaminare il contratto di servizio e selezionare **Accetta**.  

3. Nella pagina **Confermare l'abbonamento** esaminare l'elenco delle licenze valide necessarie. Impostare l'opzione su **Sì** accanto a **Si dispone di uno degli abbonamenti supportati o di uno di livello superiore?** , quindi selezionare **Avanti**.  

4. Nella pagina **Concedere l'accesso a utenti**:

    - **Consentire a Desktop Analytics di gestire i ruoli della directory per conto dell'utente**: Desktop Analytics assegna automaticamente ai **Proprietari dell'area di lavoro** il ruolo **Amministratore di Desktop Analytics**. Se ai gruppi è già assegnato un **Amministratore globale**, non vengono apportate modifiche.

        Se non si seleziona questa opzione, Desktop Analytics aggiunge comunque gli utenti come membri del gruppo di sicurezza. Un **Amministratore globale** deve assegnare manualmente il ruolo **Amministratore di Desktop Analytics** per gli utenti.

        Per altre informazioni sull'assegnazione delle autorizzazioni del ruolo di amministratore in Azure Active Directory e sulle autorizzazioni assegnate agli **Amministratori di Desktop Analytics**, vedere [Autorizzazioni del ruolo Amministratore in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles).  

    - Desktop Analytics preconfigura il gruppo di sicurezza **Proprietari dell'area di lavoro** in Azure Active Directory per creare e gestire aree di lavoro e piani di distribuzione.

        Per aggiungere un utente al gruppo, digitarne il nome o l'indirizzo di posta elettronica nella sezione **Immettere il nome o l'indirizzo di posta elettronica**. Al termine, selezionare **Avanti**.

5. Nella pagina **Configura la tua area di lavoro**:  

    > [!NOTE]  
    > Per completare questo passaggio, l'utente deve avere le autorizzazioni **Proprietario dell'area di lavoro** e l'accesso aggiuntivo alla sottoscrizione di Azure e al gruppo di risorse. Per altre informazioni, vedere i [prerequisiti](overview.md#prerequisites).  

    - Per usare un'area di lavoro esistente per Desktop Analytics, selezionarla e continuare con il passaggio successivo.  

        > [!TIP]  
        > È possibile avere solo un'area di lavoro di Desktop Analytics per ogni tenant di Azure AD. I dispositivi possono inviare i dati di diagnostica solo a un'area di lavoro.  

    - Per creare un'area di lavoro per Desktop Analytics, selezionare **Aggiungi area di lavoro**.  

        1. Immettere un **nome dell'area di lavoro** univoco globale.

        2. Selezionare l'elenco a discesa per **selezionare il nome dell'abbonamento di Azure per l'area di lavoro** e scegliere l'abbonamento di Azure per l'area di lavoro.  

        3. Per il gruppo di risorse, scegliere **Crea nuovo** o **Usa esistente**.

        4. Selezionare l'**Area** dall'elenco, quindi selezionare **Aggiungi**.  

6. Selezionare un'area di lavoro nuova o esistente, quindi selezionare **Set as Desktop Analytics workspace** (Imposta come area di lavoro di Desktop Analytics).  Quindi selezionare **Continua** nella finestra di dialogo **Conferma e concedi l'accesso**.  

7. Nella nuova scheda del browser selezionare un account da usare per l'accesso. Selezionare l'opzione **Acconsenti per conto dell'organizzazione** e selezionare **Accetta**.  

    > [!Note]  
    > Questo consenso assegna all'applicazione MALogAnalyticsReader il ruolo Lettore di Log Analytics per l'area di lavoro. Questo ruolo applicazione è richiesto da Desktop Analytics. Per altre informazioni, vedere [Ruolo applicazione MALogAnalyticsReader](troubleshooting.md#bkmk_MALogAnalyticsReader).  

8. Tornare alla pagina **Configura la tua area di lavoro** e selezionare **Avanti**.  

9. Nella pagina **Last steps** (Ultimi passaggi) selezionare **Vai a Desktop Analytics**.

Nel portale di Azure viene visualizzata la pagina **Home page** di Desktop Analytics.

## <a name="next-steps"></a>Passaggi successivi

Passare all'articolo successivo per connettere Configuration Manager a Desktop Analytics.
> [!div class="nextstepaction"]  
> [Connettere Configuration Manager](connect-configmgr.md)  
