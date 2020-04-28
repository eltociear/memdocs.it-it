---
title: Creare dati utente ed elementi di configurazione dei profili
titleSuffix: Configuration Manager
description: È possibile usare gli elementi di configurazione di dati e profili in Configuration Manager per gestire il reindirizzamento delle cartelle, i file non in linea e profili mobili.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 9fcbcc81-cd6f-496e-b075-ef1afa2b8ccc
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 2a99384772895ff2675ade671076163b74cecee2
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075303"
---
# <a name="create-user-data-and-profiles-configuration-items-in-configuration-manager"></a>Creare elementi di configurazione profili e dati utente in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Gli elementi di configurazione di profili e dati utente in Configuration Manager contengono le impostazioni che consentono di gestire il reindirizzamento delle cartelle, i file offline e i profili mobili nei computer che eseguono Windows 8 e versioni successive per gli utenti della gerarchia. Ad esempio, è possibile:  

- Reindirizzare la cartella Documenti di un utente a una condivisione di rete.  

- Assicurarsi che file specifici archiviati in rete siano disponibili nel computer di un utente quando la connessione di rete non è disponibile.  

- Configurare i file del profilo mobile di un utente da sincronizzare con una condivisione di rete quando l'utente si connette e si disconnette.  

  A differenza di altri elementi di configurazione in Configuration Manager, gli elementi di configurazione di profili e dati utente non vengono aggiunti a una linea di base di configurazione da distribuire in un secondo momento. Al contrario, l'elemento di configurazione si distribuisce direttamente usando la finestra di dialogo **Distribuisci elemento di configurazione profili e dati utente** .  

> [!IMPORTANT]  
>  È possibile distribuire elementi di configurazione di profili e dati utente solo alle raccolte utenti.  

## <a name="enable-user-data-and-profiles-for-compliance-settings"></a>Abilitare profili e dati utente per le impostazioni di conformità  
 Usare la procedura seguente per configurare l'impostazione client predefinita per le impostazioni di conformità di profili e dati utente che verranno applicate a tutti i computer nella gerarchia. Per applicare queste impostazioni solo ad alcuni computer, creare un'impostazione client di dispositivo personalizzata e assegnarla a una raccolta contenente i computer per cui si vogliono usare le impostazioni di conformità di profili e dati utente. Per altre informazioni su come creare le impostazioni personalizzate del dispositivo, vedere [Come configurare le impostazioni client](../../core/clients/deploy/configure-client-settings.md).  

1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Impostazioni client** > **Impostazioni predefinite**.  

4.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

5.  Nella finestra di dialogo **Impostazioni predefinite** fare clic su **Impostazioni di conformità**.  

6.  Nell'elenco a discesa **Abilitare profili e dati utente** selezionare **Sì**.  

7.  Fare clic su **OK** per chiudere la finestra di dialogo **Impostazioni dispositivo** .  

## <a name="create-a-user-data-and-profiles-configuration-item"></a>Creare un elemento di configurazione di profili e dati utente  

1. Nella console di Configuration Manager fare clic su **Asset e conformità** > **Impostazioni di conformità** > **Profili e dati utente**.  

2. Nella gruppo **Crea** della scheda **Home** fare clic su **Crea elemento di configurazione profili e dati utente**.  

3. Nella pagina **Generale** della **Creazione guidata elemento di configurazione profili e dati utente**specificare le informazioni seguenti:  

   -   **Nome:** immettere un nome univoco per l'elemento di configurazione. È possibile usare un massimo di 256 caratteri.  

   -   **Descrizione:** fornire una descrizione che offra una panoramica dell'elemento di configurazione e altre informazioni rilevanti per identificarlo nella console di Configuration Manager. È possibile usare un massimo di 256 caratteri.  

   -   **Reindirizzamento cartelle:** selezionare questa casella di controllo per configurare le impostazioni per il reindirizzamento delle cartelle per questo elemento di configurazione.  

   -   **File offline:** selezionare questa casella di controllo per configurare le impostazioni per i file offline per questo elemento di configurazione.  

   -   **Profili utente mobili:** selezionare questa casella di controllo per configurare le impostazioni per i profili utente mobili per questo elemento di configurazione.  

4. Nella pagina **Reindirizzamento cartelle** della **Creazione guidata elemento di configurazione profili e dati utente**specificare come si vuole che i computer client degli utenti che ricevono questo elemento di configurazione gestiscano il reindirizzamento delle cartelle. È possibile configurare le impostazioni per qualsiasi dispositivo a cui l'utente accede o solo per i dispositivi primari dell'utente. Per altre informazioni sul reindirizzamento delle cartelle, vedere la documentazione di Windows Server.  

   > [!NOTE]  
   >  Questa pagina viene visualizzata solo se è stata selezionata la casella **Reindirizzamento cartelle** nella pagina **Generale** della procedura guidata.  

5. Nella pagina **File offline** della **Creazione guidata elemento di configurazione profili e dati utente**è possibile abilitare o disabilitare l'uso dei file offline per gli utenti che ricevono questo elemento di configurazione e quindi configurare le impostazioni per il comportamento dei file offline. È inoltre possibile specificare i file offline che saranno sempre disponibili in qualsiasi computer a cui l'utente esegue l'accesso. Per altre informazioni sui file offline, vedere la documentazione di Windows Server.  

   > [!NOTE]  
   >  Questa pagina viene visualizzata solo se è stata selezionata la casella **File offline** nella pagina **Generale** della procedura guidata.  

6. Nella pagina **Profili mobili** della **Creazione guidata elemento di configurazione profili e dati utente**è possibile configurare se i profili mobili sono disponibili nei computer a cui l'utente esegue l'accesso e anche configurare informazioni aggiuntive sul funzionamento di tali profili. Per altre informazioni sui profili mobili, vedere la documentazione di Windows Server.  

   > [!NOTE]  
   >  Questa pagina viene visualizzata solo se è stata selezionata la casella **Profili utente mobili** nella pagina **Generale** della procedura guidata.  

7. Completare la procedura guidata.  

   Il nuovo elemento di configurazione dei profili e dati utente viene visualizzato nel nodo **Profili e dati utente** dell'area di lavoro **Asset e conformità** .  

## <a name="deploy-a-user-data-and-profiles-configuration-item"></a>Distribuire un elemento di configurazione di profili e dati utente  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità** > **Impostazioni di conformità** > **Profili e dati utente**.  

3.  Selezionare l'elemento di configurazione dei profili e dati utente che si vuole distribuire e quindi nel gruppo **Distribuzione** della scheda **Home** fare clic su **Distribuisci**.  

4.  Nella finestra di dialogo **Distribuisci elemento di configurazione profili e dati utente** specificare le informazioni seguenti.  

    -   **Raccolta** : fare clic su **Sfoglia** per selezionare la raccolta di utenti in cui si vuole distribuire l'elemento di configurazione.  

        > [!IMPORTANT]  
        >  È possibile distribuire gli elementi di configurazione dei profili e dati utente solo alle raccolte di utenti.  

    -   **Monitora e aggiorna le regole non conformi, se supportato** : abilitare questa opzione per monitorare e aggiornare automaticamente le regole che vengono valutate come non conforme nei computer client.  

    -   **Consenti monitoraggio e aggiornamento fuori dalla finestra di manutenzione** : se è stata configurata una finestra di manutenzione per la raccolta in cui si distribuisce l'elemento di configurazione, abilitare questa opzione per consentire alle impostazioni di conformità di monitorare e aggiornare il valore fuori dalla finestra di manutenzione. Per altre informazioni sulle finestre di manutenzione, vedere [Come usare le finestre di manutenzione in Configuration Manager](../../core/clients/manage/collections/use-maintenance-windows.md).  

    -   **Genera un avviso** : abilitare questa opzione per configurare un avviso che viene generato se la conformità dell'elemento di configurazione è inferiore a una percentuale specificata in base a una data e un orario specifici. È inoltre possibile specificare se si desidera che un avviso venga inviato a System Center Operations Manager.  

    -   **Specificare la pianificazione per la valutazione della conformità per questo elemento di configurazione** : specifica la pianificazione in base alla quale l'elemento di configurazione distribuito viene valutato nei computer client. Può trattarsi di una pianificazione semplice o personalizzata.  

5.  Fare clic su **OK** per chiudere la finestra di dialogo **Distribuisci elemento di configurazione profili e dati utente** e creare la distribuzione.  

## <a name="monitor-a-user-data-and-profiles-configuration-item"></a>Monitorare un elemento di configurazione dei profili e dati utente  
 È possibile monitorare questo tipo di elemento di configurazione nello stesso modo in cui vengono monitorate altre impostazioni di conformità.  

 Per altre informazioni, vedere [Come monitorare le impostazioni di conformità](../../compliance/deploy-use/monitor-compliance-settings.md).  
