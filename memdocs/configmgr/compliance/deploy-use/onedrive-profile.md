---
title: Profili di OneDrive for Business
titleSuffix: Configuration Manager
description: Reindirizzare cartelle note di Windows verso OneDrive for Business usando un profilo di OneDrive for Business in Configuration Manager.
ms.date: 04/11/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: e217699a-28b2-471a-b421-8fbd1d1fd638
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ca7d81ba112c9eb79fb8bcfff96fb213b87b44c3
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694815"
---
# <a name="onedrive-for-business-profiles"></a>Profili di OneDrive for Business

A partire da Configuration Manager versione 1902, è possibile creare profili di OneDrive for Business per spostare cartelle note di Windows in OneDrive for Business. Queste cartelle includono Desktop, Documenti e Immagini. In ogni profilo è possibile specificare impostazioni per lo spostamento delle cartelle note di Windows. Per altre informazioni su OneDrive for Business, vedere [Reindirizzare e spostare le cartelle note di Windows su OneDrive](/onedrive/redirect-known-folders). <!--3556021-->

## <a name="prerequisites"></a>Prerequisiti

- [Trovare l'ID del tenant di Microsoft 365](/onedrive/find-your-office-365-tenant-id)  

- Distribuire la versione 18.111.0603.0004 del client di sincronizzazione di OneDrive o una versione successiva. Per altre informazioni, vedere [Distribuire le app OneDrive mediante Configuration Manager](/onedrive/deploy-on-windows).  

## <a name="move-windows-known-folders-to-onedrive"></a><a name="bkmk_odfb"></a> Spostare cartelle note di Windows in OneDrive
<!--3556021-->
Usare Configuration Manager per spostare le cartelle note di Windows in OneDrive for Business. Queste cartelle includono Desktop, Documenti e Immagini. Per semplificare gli aggiornamenti di Windows 10, distribuire queste impostazioni ai client Windows 7 prima di distribuire una sequenza di attività. 

1. Nella console di Configuration Manager passare all'area di lavoro **Asset e conformità**, espandere **Impostazioni di conformità** e selezionare il nodo **OneDrive for Business Profiles** (Profili OneDrive for Business).  

   ![Nodo Profili di OneDrive for Business](media/onedrive-for-business-profiles-node.png)
2. Nella barra multifunzione selezionare **Crea un profilo di OneDrive for Business**.  

3. Specificare un nome per identificare questo criterio e selezionare **Avanti**.  

4. Selezionare le piattaforme di cui verrà effettuato il provisioning con il profilo di OneDrive for Business. Al termine della selezione delle piattaforme fare clic su **Avanti**.

    ![Selezionare le piattaforme per il profilo di OneDrive for Business](media/onedrive-for-business-profile-select-platforms.png) 

5. Nella pagina **Impostazioni**:

    1. Specificare l'ID del tenant di Microsoft 365.  

    2. Selezionare una delle opzioni seguenti per spostare le cartelle note in OneDrive:  

        - **Richiedi agli utenti di spostare le cartelle note di Windows in OneDrive**: con questa opzione, l'utente visualizza una procedura guidata per lo spostamento dei file. Se si sceglie di posticipare o rifiutare lo spostamento delle cartelle, OneDrive visualizza periodicamente un promemoria.  

        - **Sposta automaticamente le cartelle note di Windows in OneDrive**: quando questo criterio viene applicato al dispositivo, il client di OneDrive reindirizza automaticamente le cartelle note a OneDrive for Business.  

            - **Mostra una notifica agli utenti dopo il reindirizzamento delle cartelle**: se si abilita questa opzione, il client di OneDrive invia una notifica all'utente dopo lo spostamento delle cartelle.  

    3. **Impedisci agli utenti di reindirizzare le rispettive cartelle note di Windows al proprio computer**: disabilita l'opzione in OneDrive for Business nel client che consente agli utenti di spostare di nuovo queste cartelle nel dispositivo personale.  

       ![Impostazioni per lo spostamento di cartelle note di OneDrive for Business](media/onedrive-for-business-profile-move-folder-settings.png)

6. Completare la procedura guidata e quindi distribuire i criteri.  


## <a name="deploy-the-onedrive-for-business-profile"></a>Distribuire il profilo di OneDrive for Business

1. Nella console di Configuration Manager passare all'area di lavoro **Asset e conformità**, espandere **Impostazioni di conformità** e selezionare il nodo **OneDrive for Business Profiles** (Profili OneDrive for Business).  


2. Selezionare il profilo e quindi sulla barra multifunzione selezionare **Distribuisci**.

3. Specificare le impostazioni seguenti per la distribuzione:

   1. **Raccolta**: fare clic su **Sfoglia...** e quindi selezionare la raccolta per la quale si vuole distribuire il profilo.  
   1. **Genera un avviso**:

      - **Quando la conformità è inferiore a**: percentuale minima di conformità del client da mantenere. In caso contrario, viene generato un avviso.
      -  **Data e ora**: la data in cui deve iniziare la generazione degli avvisi in base alla conformità del profilo.
      - **Genera avviso di System Center Operations Manager**: consente di inviare un avviso di conformità a System Center Operations Manager.
   1. **Pianificazione**:

      - **Pianificazione semplice**: per impostazione predefinita, questa impostazione usa una pianificazione semplice per avviare la valutazione della conformità ogni sette giorni.
      - **Pianificazione personalizzata**: consente di definire i casi in cui eseguire la valutazione della conformità. L'ora di avvio si basa sull'ora locale del computer che esegue la Console di Configuration Manager al momento della creazione della pianificazione. In alternativa, è possibile usare l'ora UTC.
 
      ![Distribuire il profilo di OneDrive for Business](media/onedrive-for-business-deploy-profile.png)

4. Fare clic su **OK** per distribuire il profilo di OneDrive for Business.


## <a name="next-steps"></a>Passaggi successivi

[Create remote connection profiles](create-remote-connection-profiles.md) (Creare profili di connessione remota)