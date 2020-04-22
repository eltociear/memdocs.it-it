---
title: 'Attività comuni per le linee di base di configurazione '
titleSuffix: Configuration Manager
description: Informazioni su come creare e distribuire linee di base di configurazione in Configuration Manager.
ms.date: 07/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 4bb6afeb-d267-4f9b-ade2-26e5400c223b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 52e83639029db9eeb4ef64657e70e3dc11aab8f2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692259"
---
# <a name="common-tasks-for-creating-and-deploying-configuration-baselines-with-configuration-manager"></a>Attività comuni per la creazione e la distribuzione di linee base di configurazione con Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Questo argomento descrive alcuni scenari comuni per scoprire come creare e distribuire le linee di base di configurazione di Configuration Manager.  

 Gli utenti che hanno già familiarità con le impostazioni di conformità possono trovare la documentazione dettagliata su tutte le funzionalità usate negli argomenti [Creare linee di base di configurazione](../../compliance/deploy-use/create-configuration-baselines.md) e [Distribuire linee di base di configurazione](../../compliance/deploy-use/deploy-configuration-baselines.md).  

 Prima di iniziare, leggere [Get started with compliance settings](../../compliance/get-started/get-started-with-compliance-settings.md) (Introduzione alle impostazioni di conformità) per apprendere alcune nozioni sulle impostazioni di conformità e [Plan for and configure compliance settings](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md) (Pianificare e configurare le impostazioni di conformità) per implementare i prerequisiti necessari.  

## <a name="create-a-configuration-baseline"></a>Creare una linea di base di configurazione  
 In questo esempio è stato creato un elemento di configurazione solo per i PC con Windows 10 che eseguono il client di Configuration Manager.  

 Questo elemento di configurazione impone una password obbligatoria di almeno 6 caratteri nei PC Windows 10. L'elemento di configurazione è denominato **Windows 10 Password Enforcement**.  

Usare la procedura seguente per apprendere come aggiungere questo elemento di configurazione a una linea di base di configurazione per prepararlo per la distribuzione.  

1. Nella console di Configuration Manager fare clic su **Asset e conformità** > **Impostazioni di conformità** > **Linee di base di configurazione**.  

2. Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea linea di base di configurazione**.  

3. Nella finestra di dialogo **Crea linea di base di configurazione** configurare le impostazioni seguenti:  

   -   **Nome** - Immettere **Password Windows 10** (o un altro nome a scelta).  

4. Fare clic su **Aggiungi** > **Elementi di configurazione**.  

5. Nella finestra di dialogo **Aggiungi elementi di configurazione** selezionare l'elemento di configurazione **Windows 10 Password Enforcement** creato in precedenza e quindi fare clic su **Aggiungi**.  

6. Fare clic su OK per chiudere la finestra di dialogo **Aggiungi elementi di configurazione** e tornare alla finestra di dialogo **Crea linea di base di configurazione**.

7. Fare clic su **OK** per chiudere la finestra di dialogo **Crea linea di base di configurazione** .  

   È ora possibile visualizzare la linea di base di configurazione nel nodo **Linee di base di configurazione** nella console di Configuration Manager.  

## <a name="deploy-the-configuration-baseline"></a>Distribuire la linea di base di configurazione  
 In questo esempio viene descritto come distribuire la linea di base di configurazione creata nella procedura precedente in una raccolta di computer.  

1. Nella console di Configuration Manager fare clic su **Asset e conformità** > **Impostazioni di conformità** > **Linee di base di configurazione**.  

2. Nell'elenco di linee di base di configurazione selezionare **Password Windows 10**.  

3. Nella scheda **Home** , nel gruppo **Distribuzione** , fare clic su **Distribuisci**.  

4. Nella finestra di dialogo **Distribuisci linee di base di configurazione** configurare le impostazioni seguenti:  

   -   **Linee di base di configurazione selezionate** - Assicurarsi che la linea di base di configurazione **Password Windows 10** sia stata aggiunta automaticamente all'elenco.  

   -   **Monitora e aggiorna le regole non conformi, se supportato** - Selezionare questa casella di controllo per assicurarsi che, in caso di assenza nei dispositivi di destinazione, le impostazioni corrette vengano monitorate e aggiornate da Configuration Manager.  

   -   **Raccolta** - Fare clic su **Sfoglia** per scegliere la raccolta di computer in cui la linea di base di configurazione viene valutata e monitorata e aggiornata per la conformità. In questo esempio, la linea di base di configurazione è stata distribuita nella raccolta predefinita **Tutti i client desktop e di server** .  

       > [!TIP]  
       >  Non occorre preoccuparsi se la raccolta scelta contiene computer o dispositivi che non eseguono Windows 10. Se nell'elemento di configurazione creato sono state configurate le piattaforme supportate, solo i PC Windows 10 vengono valutati per la conformità.  

   -   Se necessario, configurare la pianificazione per la valutazione della linea di base di configurazione. In caso contrario, usare il valore predefinito di **7 giorni**.  

5. Fare clic su **OK** per chiudere la finestra di dialogo **Distribuisci linee di base di configurazione** e creare la distribuzione.  

   Per esaminare rapidamente le statistiche di conformità per questa distribuzione, nell'area di lavoro **Monitoraggio** fare clic su **Distribuzioni**. Nella parte inferiore della schermata è visualizzato un grafico **Statistiche conformità**.  

## <a name="next-steps"></a>Passaggi successivi 

Per informazioni più dettagliate su come monitorare le linee di base di configurazione, vedere [Monitorare le impostazioni di conformità](../../compliance/deploy-use/monitor-compliance-settings.md).  
