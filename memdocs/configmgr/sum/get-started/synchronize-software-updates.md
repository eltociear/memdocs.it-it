---
title: Gestire la sincronizzazione degli aggiornamenti software
titleSuffix: Configuration Manager
description: Seguire questa procedura per pianificare, avviare manualmente e monitorare la sincronizzazione degli aggiornamenti software.
ms.date: 12/20/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: ea8698c4-9df5-4cf5-8b62-ab93115b4769
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: d1b47965fa5cc36b0c0eb6d47c2214d1dceb8ee8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692939"
---
#  <a name="synchronize-software-updates"></a><a name="BKMK_SUMSync"></a> sincronizzare gli aggiornamenti software

*Si applica a: Configuration Manager (Current Branch)*

 La sincronizzazione degli aggiornamenti software in Configuration Manager è il processo di recupero dei metadati degli aggiornamenti software in base ai criteri configurati. Questo include prodotti, classificazioni e lingue specifici. In genere il punto di aggiornamento software nel sito di amministrazione centrale o in un sito primario autonomo recupera i metadati da Microsoft Update. In seguito, il sito di livello superiore invierà una richiesta di sincronizzazione agli altri siti. Quando un sito riceve la richiesta di sincronizzazione da un sito padre, il punto di aggiornamento software per il sito recupera i metadati degli aggiornamenti software dall'[origine sincronizzazione](../plan-design/plan-for-software-updates.md#BKMK_SyncSource) upstream. Per altre informazioni sul processo di sincronizzazione degli aggiornamenti software, vedere [Sincronizzazione degli aggiornamenti software](../understand/software-updates-introduction.md#BKMK_Synchronization).

La sincronizzazione degli aggiornamenti software viene configurata per l'esecuzione in base a una pianificazione nelle proprietà per il punto di aggiornamento software nel sito di livello superiore. Una volta configurata la pianificazione della sincronizzazione, in genere la pianificazione non verrà modificata come parte del normale funzionamento. È tuttavia possibile avviare manualmente la sincronizzazione degli aggiornamenti software quando necessario.

  > [!NOTE]  
  >  Per sincronizzare gli aggiornamenti software, i punti di aggiornamento software devono essere connessi all'origine sincronizzazione upstream relativa. Quando un punto di aggiornamento software viene disconnesso dall'origine sincronizzazione upstream, è possibile utilizzare il metodo di esportazione e importazione per sincronizzare gli aggiornamenti software. Per altre informazioni, vedere [Sincronizzare gli aggiornamenti software da un punto di aggiornamento software disconnesso](synchronize-software-updates-disconnected.md).  

## <a name="schedule-software-updates-synchronization"></a>Pianificare la sincronizzazione degli aggiornamenti software
Quando viene configurata una pianificazione per la sincronizzazione degli aggiornamenti, il punto di aggiornamento software di livello superiore avvia la sincronizzazione con Microsoft Update alla data e ora pianificate. La pianificazione personalizzata consente di sincronizzare gli aggiornamenti software a una data e a un orario in cui le richieste dal server Windows Server Update Services (WSUS), dal server del sito e dalla rete sono ridotte. Ad esempio, è possibile impostare la pianificazione in modo che gli aggiornamenti software vengano sincronizzati ogni settimana alle 2:00 di notte. Durante la sincronizzazione pianificata, tutte le modifiche apportate ai metadati degli aggiornamenti software dall'ultima sincronizzazione pianificata vengono inserite nel database del sito. Sono inclusi nuovi metadati di aggiornamenti software o metadati che sono stati modificati, rimossi o scaduti.

Seguire queste procedure nel sito di livello superiore per pianificare la sincronizzazione degli aggiornamenti software.  

#### <a name="to-schedule-software-updates-synchronization"></a>Per pianificare la sincronizzazione degli aggiornamenti software  

  1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

  2.  Nell'area di lavoro Amministrazione espandere **Configurazione sito**, quindi fare clic su **Siti**.  

  3.  Nel riquadro dei risultati fare clic sul sito di amministrazione centrale o sul sito primario autonomo.  

  4.  Nella scheda **Home** , nel gruppo **Impostazioni** , espandere **Configura componenti sito**, quindi fare clic su **Punto di aggiornamento software**.  

  5.  Nella finestra di dialogo Proprietà del componente del punto di aggiornamento software selezionare **Abilita sincronizzazione su una pianificazione**e quindi specificare la pianificazione della sincronizzazione.  

## <a name="manually-start-software-updates-synchronization"></a>Avviare manualmente la sincronizzazione degli aggiornamenti software
È possibile avviare manualmente la sincronizzazione degli aggiornamenti software nel sito di livello superiore nella console di Configuration Manager dal nodo **Tutti gli aggiornamenti software** nell'area di lavoro **Raccolta software**.  

Seguire queste procedure nel sito di livello superiore per avviare manualmente la sincronizzazione degli aggiornamenti software.  

#### <a name="to-manually-start-software-updates-synchronization"></a>Per avviare manualmente la sincronizzazione degli aggiornamenti software  

1. Nella console di Configuration Manager che è connessa al sito di amministrazione centrale o al sito primario autonomo, fare clic su **Raccolta software**.  

2. Nell'area di lavoro Raccolta software espandere **Aggiornamenti software** , quindi fare clic su **Tutti gli aggiornamenti software** o **Gruppo di aggiornamento software**.  

3. Nella scheda **Home** nel gruppo **Crea** fare clic su **Sincronizza aggiornamenti software**. Fare clic su **Sì** nella finestra di dialogo per confermare che si desidera avviare il processo di sincronizzazione.  

   Dopo aver avviato il processo di sincronizzazione nel punto di aggiornamento software, è possibile monitorarlo dalla console di Configuration Manager per tutti i punti di aggiornamento software della gerarchia. Utilizzare la procedura seguente per monitorare il processo di sincronizzazione degli aggiornamenti software.  


## <a name="monitor-software-updates-synchronization"></a>Monitorare la sincronizzazione degli aggiornamenti software
Dopo aver avviato il processo di sincronizzazione, è possibile usare la console di Configuration Manager per monitorare il processo per tutti i punti di aggiornamento software della gerarchia. Usare la seguente procedura per monitorare il processo di sincronizzazione degli aggiornamenti software. Per altre informazioni sul monitoraggio degli aggiornamenti software, compreso il processo di sincronizzazione, vedere [Monitor software updates](../deploy-use/monitor-software-updates.md) (Monitorare gli aggiornamenti software).

#### <a name="to-monitor-the-software-updates-synchronization-process"></a>Per monitorare il processo di sincronizzazione degli aggiornamenti software  

1. Nella console di Configuration Manager fare clic su **Monitoraggio**.  

2. Nell'area di lavoro **Monitoraggio** fare clic su **Stato di sincronizzazione del punto di aggiornamento software**.  

   I punti di aggiornamento software nella gerarchia di Configuration Manager vengono visualizzati nel riquadro dei risultati. In questa vista è possibile monitorare lo stato di sincronizzazione per tutti i punti di aggiornamento software. Se sono necessarie informazioni più dettagliate sul processo di sincronizzazione, è possibile esaminare il file wsyncmgr.log che si trova in <*PercorsoInstallMigrazioneConfig*>\Logs in ogni server del sito.  

## <a name="import-updates-from-the-microsoft-update-catalog"></a>Importare gli aggiornamenti da Microsoft Update Catalog

Il punto di aggiornamento software di livello superiore usa WSUS per ottenere informazioni sugli aggiornamenti software da Microsoft in Configuration Manager. In alcuni casi, potrebbe essere necessario un aggiornamento che non si sincronizza automaticamente in WSUS per i prodotti e le classificazioni selezionati, ma è disponibile in [Microsoft Update Catalog](https://catalog.update.microsoft.com). Gli aggiornamenti che non eseguono automaticamente la sincronizzazione in WSUS sono in genere progettati per risolvere problemi molto specifici. In genere, se un aggiornamento è disponibile nel catalogo, è possibile importarlo in WSUS. È quindi possibile sincronizzarlo in Configuration Manager e distribuirlo come qualsiasi altro aggiornamento.

### <a name="to-import-an-update-from-the-microsoft-update-catalog"></a>Per importare un aggiornamento da Microsoft Update Catalog

1. Aprire la console di amministrazione di WSUS e connetterla al server WSUS di livello superiore nella gerarchia.
   - Se Internet Explorer non è il Web browser predefinito del computer, impostarlo temporaneamente come predefinito.
2. Fare clic su **Aggiornamenti** oppure sul nome del server WSUS. 
3. Nel riquadro **Azioni** selezionare **Importa aggiornamenti...** . Verrà aperta una finestra del browser per [Microsoft Update Catalog](https://catalog.update.microsoft.com).
   ![Selezionare Importa aggiornamenti nella console di WSUS](media/wsus-console-import-updates.png)
4. Se richiesto, installare il controllo ActiveX Microsoft Update Catalog. Il controllo deve essere installato per importare gli aggiornamenti in WSUS. 
5. Nella finestra del browser cercare l'aggiornamento desiderato. Fare clic sul pulsante **Aggiungi*** per aggiungerlo al carrello.
6. Fare clic sul collegamento per **visualizzare il carrello**. Assicurarsi che l'opzione **Import directly into Windows Server Update Services** (Importa direttamente in Windows Server Update Services) sia selezionata. Fare quindi clic su **Importa**.
    ![Importare l'aggiornamento dal catalogo in WSUS](./media/import-catalog-update-into-wsus.png)
7. Al termine dell'importazione, fare clic su **Chiudi** nella finestra del browser.
     - Se necessario, reimpostare il browser predefinito.
8. Sincronizzare il punto di aggiornamento software di Configuration Manager.


## <a name="next-steps"></a>Passaggi successivi
Dopo aver sincronizzato gli aggiornamenti software per la prima volta o dopo che sono stati resi disponibili nuovi prodotti o classificazioni, è necessario [configurare le classificazioni e i prodotti nuovi](configure-classifications-and-products.md) per sincronizzare gli aggiornamenti software con i nuovi criteri.

Dopo aver sincronizzato gli aggiornamenti software con i criteri necessari, [gestire le impostazioni per gli aggiornamenti software](manage-settings-for-software-updates.md).  
