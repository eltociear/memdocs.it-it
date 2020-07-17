---
title: Distribuire linee di base di configurazione
titleSuffix: Configuration Manager
description: Distribuire le linee di base di configurazione per definire le relative distribuzioni e aggiungere o rimuovere le linee di base dalle distribuzioni.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 9be8aaf3-075e-4acd-abd2-7459254e16e2
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: 94a5d0af5636236ffba3f15c05823ead083f2948
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240270"
---
# <a name="how-to-deploy-configuration-baselines-in-configuration-manager"></a>Come distribuire linee di base di configurazione in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Le linee di base di configurazione in Configuration Manager devono essere distribuite in una o più raccolte di utenti o dispositivi prima che i dispositivi client in tali raccolte possano valutare la relativa conformità in base alla linea di base di configurazione.  

Usare la finestra di dialogo **Distribuisci linee di base di configurazione** per definire le distribuzioni delle linee di base di configurazione, ad esempio aggiungendo o rimuovendo le linee di base di configurazione dalle distribuzioni e specificando la pianificazione di valutazione.  

## <a name="deploy-a-configuration-baseline"></a>Distribuire una linea di base di configurazione  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità** > **Impostazioni di conformità** > **Linee di base di configurazione**.  

3.  Nell'elenco **Distribuisci linee di base di configurazione** selezionare la linea di base di configurazione da distribuire e quindi nella scheda **Home** nel gruppo **Distribuzione** fare clic su **Distribuisci**.  

4.  Nella finestra di dialogo **Distribuisci linee di base di configurazione** selezionare le linee di base di configurazione da distribuire nell'elenco **Linee d base di configurazione disponibili** . Fare clic su **Aggiungi** per aggiungere gli elementi selezionati all'elenco **Linee di base di configurazione selezionate** .  

    > [!IMPORTANT]  
    >  Se si modifica un elemento di configurazione aggiunto a una linea di base di configurazione distribuita, la conformità dell'elemento di configurazione modificato non viene valutata fino alla successiva ora di valutazione pianificata.  

5.  Specificare le informazioni aggiuntive seguenti:  

    -   **Monitora e aggiorna le regole non conformi, se supportato**: consente di correggere automaticamente tutte le regole non conformi per Strumentazione gestione Windows (WMI), il Registro di sistema, gli script e tutte le impostazioni per i dispositivi mobili registrati da Configuration Manager.  

    -   **Consenti monitoraggio e aggiornamento fuori dalla finestra di manutenzione** : se è stata configurata una finestra di manutenzione per la raccolta in cui si distribuisce la linea di base di configurazione, abilitare questa opzione per consentire alle impostazioni di conformità di monitorare e aggiornare il valore fuori dalla finestra di manutenzione. Per altre informazioni sulle finestre di manutenzione, vedere [How to use maintenance windows](../../core/clients/manage/collections/use-maintenance-windows.md) (Come usare le finestre di manutenzione).  

6.  **Genera un avviso**: configura un avviso che viene generato se la conformità della linea di base di configurazione è inferiore a una percentuale specificata in base a una data e un orario specifici. È inoltre possibile specificare se si desidera che un avviso venga inviato a System Center Operations Manager.  

7.  **Raccolta** : fare clic su **Sfoglia** per selezionare la raccolta in cui si vuole distribuire la linea di base di configurazione.  

8.  **Specificare la pianificazione per la valutazione della conformità per questa linea di base di configurazione**: specifica la pianificazione in base alla quale la linea di base di configurazione distribuita viene valutata nei computer client. Può trattarsi di una pianificazione semplice o personalizzata.  

    > [!NOTE]  
    >  Se la linea di base di configurazione viene distribuita in un computer, la relativa conformità viene valutata entro due ore dall'ora di inizio pianificata. Se viene distribuita a un utente, la relativa conformità viene valutata quando l'utente effettua l'accesso.  

9. Fare clic su **OK** per chiudere la finestra di dialogo **Distribuisci linee di base di configurazione** e creare la distribuzione. Per altre informazioni su come monitorare la distribuzione, vedere [Monitor compliance settings](monitor-compliance-settings.md) (Monitorare le impostazioni di conformità).  
