---
title: Simulare le distribuzioni di applicazioni
titleSuffix: Configuration Manager
description: Valutare il metodo di individuazione, i requisiti e le dipendenze per un tipo di distribuzione senza installare l'applicazione.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 28b240a4-d358-40ce-8006-c697b1622ece
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: bed491b4800dd6ae8b53a837618abf3d8a5a597d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689979"
---
# <a name="simulate-application-deployments-with-configuration-manager"></a>Simulare distribuzioni di applicazioni con Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

È possibile usare distribuzioni simulate per testare la distribuzione di un'applicazione senza installare o disinstallare l'applicazione. Una distribuzione simulata valuta il metodo di rilevamento, i requisiti e le dipendenze per un tipo di distribuzione e raccoglie i risultati nel nodo **Distribuzioni** dell'area di lavoro **Monitoraggio**. Usare la procedura descritta in questo argomento per simulare una distribuzione di applicazioni in Configuration Manager.  

> [!NOTE]  
> Non è possibile usare le distribuzioni simulate per le raccolte di dispositivi mobili.  
>   
> Non è possibile distribuire un'applicazione con scopo di distribuzione **Disinstalla** se è attiva una distribuzione simulata della stessa applicazione.  

## <a name="configure-a-simulated-application-deployment"></a>Configurare la distribuzione simulata di un'applicazione

1.  Nella console di Configuration Manager selezionare uno degli elementi seguenti:  
    -   Una raccolta di utenti.  
    -   Una raccolta di dispositivi.  
    -   Un'applicazione di Configuration Manager.  

2.  Nella gruppo **Distribuzione** della scheda **Home** scegliere **Simula distribuzione**.  

3.  Nella simulazione guidata distribuzione applicazione impostare i dettagli seguenti per la distribuzione simulata:  

    -   **Applicazione**. Scegliere **Sfoglia** e selezionare l'applicazione per cui si vuole creare una distribuzione simulata.  

    -   **Raccolta**. Scegliere **Sfoglia** e selezionare la raccolta da usare per la distribuzione simulata.  

    -   **Azione**. Dall'elenco a discesa selezionare se si vuole simulare l'installazione o la disinstallazione dell'applicazione selezionata.  

    -   **Distribuisci automaticamente con o senza accesso utente**. Se questa opzione è selezionata, i client valutano la distribuzione simulata indipendentemente dal fatto che abbiano eseguito l'accesso.  

4.  Fare clic su **Avanti**, rivedere le informazioni nella pagina **Riepilogo** e completare la procedura guidata per creare la distribuzione dell'applicazione simulata.  

5.  Le applicazioni simulate vengono visualizzate nel nodo **Distribuzioni** dell'area di lavoro **Monitoraggio** con lo scopo **Simula**. Per altre informazioni su come monitorare le distribuzioni delle applicazioni, vedere [Monitorare le applicazioni dalla console di Configuration Manager](../../apps/deploy-use/monitor-applications-from-the-console.md).  
