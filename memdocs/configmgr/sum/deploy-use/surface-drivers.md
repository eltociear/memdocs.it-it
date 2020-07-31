---
title: Gestire gli aggiornamenti dei driver di Surface
titleSuffix: Configuration Manager
description: Configuration Manager Sincronizza gli aggiornamenti dei driver di Surface per la distribuzione nei dispositivi Surface.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 06/18/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: e9f9f4e6-5b4f-4b8f-94d6-db9b2b239113
ms.openlocfilehash: f276db618a2e67832ffa5575622e00eea02c7422
ms.sourcegitcommit: 8a4a86ee8044f273dcece26155132a801f3d8f9a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/30/2020
ms.locfileid: "87438627"
---
# <a name="manage-surface-drivers-with-configuration-manager"></a>Gestire i driver di Surface con Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager consente di sincronizzare i driver per i dispositivi Surface e di distribuirli come aggiornamenti software. Questa funzionalità consente di verificare che i dispositivi Surface eseguano i driver più recenti disponibili. Questa sincronizzazione è stata introdotta per la prima volta nella versione 1706 come funzionalità di versione non definitiva ed è diventata una funzionalità nella versione 1710. <!--3684621, 3608197, 1098490-->

## <a name="prerequisites-for-synchronizing-surface-drivers"></a>Prerequisiti per la sincronizzazione dei driver di Surface

- Un punto di aggiornamento software di primo livello connesso a Internet.
- Tutti i punti di aggiornamento software devono eseguire Windows Server 2016 con l'aggiornamento cumulativo KB4025339 o successivo installato.
- Configuration Manager non abilita questa funzionalità facoltativa per impostazione predefinita. Abilitare questa funzionalità prima di usarla. Per altre informazioni, vedere [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options) (Abilitare le funzioni facoltative dagli aggiornamenti).<!--505213-->  

## <a name="enable-sync-for-surface-drivers"></a>Abilitare la sincronizzazione per i driver di Surface

Per abilitare la sincronizzazione dei driver di Surface, seguire questa procedura:

1. Connettere la console di Configuration Manager al server del sito principale.
1. Passare a **Amministrazione** > **Configurazione del sito** > **Siti** e fare clic sul sito principale.
1. Nella barra multifunzione selezionare **Impostazioni** > **Configura componenti del sito** > **Punto di aggiornamento software**.
1. Fare clic sulla scheda **Classificazioni**, quindi fare clic sulla casella di controllo **Includi i driver di Microsoft Surface e gli aggiornamenti del firmware** e fare clic su **Applica**.

     ![Abilitare i driver di Surface dalle proprietà del punto di aggiornamento software](media/enable-surface-driver-sync.png)

1. In Proprietà del componente del punto di aggiornamento software fare clic sulla scheda **Prodotti**. Per altre informazioni, vedere le sezioni [Prodotti per i driver di Surface](#bkmk_prod) e [Modelli di dispositivi Surface](#bkmk_models).
1. Selezionare i prodotti per ogni versione di Windows 10 per la quale si vuole supportare i driver di Surface. Si noterà che sono disponibili due versioni diverse di ogni prodotto per i driver:

   - Windows 10 *versione* **Update and later Servicing Drivers**
   - Windows 10 *versione* **Update and later Upgrade & Servicing Drivers**.

     ![Elenco dei prodotti driver per le versioni di Windows 10](media/surface-driver-products-sup.png)

1. Al termine della selezione dei prodotti, fare clic su **OK**.
1. [Sincronizzare il punto di aggiornamento software](../get-started/synchronize-software-updates.md) per portare i driver di Surface in Configuration Manager.
1. Quando i driver di Surface sono sincronizzati, distribuirli con le stesse modalità usate per gli altri aggiornamenti.

## <a name="products-for-surface-drivers"></a><a name="bkmk_prod"></a> Prodotti per i driver di Surface

La maggior parte dei driver appartiene ai gruppi di prodotti seguenti:

- Windows 10 and later version drivers
- Windows 10 and later Upgrade & Servicing Drivers
- Windows 10 Anniversary Update and Later Servicing Drivers
- Windows 10 Anniversary Update and Later Upgrade & Servicing Drivers
- Windows 10 Creators Update and Later Servicing Drivers
- Windows 10 Creators Update and Later Upgrade & Servicing Drivers
- Windows 10 Fall Creators Update and Later Servicing Drivers
- Windows 10 Fall Creators Update and Later Upgrade & Servicing Drivers
- Windows 10 S and Later Servicing Drivers
- Windows 10 S Version 1709 and Later Servicing Drivers for testing
- Windows 10 S Version 1709 and Later Upgrade & Servicing Drivers for testing
- Windows 10 S Version 1803 and Later Servicing Drivers
- Windows 10 S Version 1803 and Later Upgrade & Servicing Drivers
- Windows 10 S version 1809 and later, Servicing Drivers
- Windows 10 S version 1809 and later, Upgrade & Servicing Drivers
- Windows 10 S version 1903 and later, Servicing Drivers
- Windows 10 S version 1903 and later, Upgrade & Servicing Drivers
- Windows 10 Version 1803 and Later Servicing Drivers
- Windows 10 Version 1803 and Later Upgrade & Servicing Drivers
- Windows 10 version 1809 and later, Servicing Drivers
- Windows 10 Version 1809 and later, Upgrade & Servicing Drivers
- Windows 10 version 1903 and later, Servicing Drivers
- Windows 10 Version 1903 and later, Upgrade & Servicing Drivers

> [!NOTE]
> La maggior parte dei driver di Surface appartiene a più gruppi di prodotti Windows 10. Potrebbe non essere necessario selezionare tutti i prodotti elencati qui. Per contribuire a ridurre il numero di prodotti che popolano il catalogo degli aggiornamenti, è consigliabile selezionare solo i prodotti richiesti dall'ambiente per la sincronizzazione.

## <a name="surface-models"></a><a name="bkmk_models"></a> Modelli di dispositivi Surface

La tabella seguente contiene i modelli di dispositivi Surface e le versioni di Windows 10 in cui Configuration Manager può installare i driver. Gli aggiornamenti dei driver di Surface non sono disponibili in Configuration Manager lo stesso giorno in cui vengono pubblicati nel catalogo di Microsoft Update. Configuration Manager gestisce un proprio elenco dei driver di Surface che verranno importati. Sono indicati i dispositivi che richiedono prodotti Windows 10 S. Microsoft prevede di aggiungere i driver di Surface all'elenco Consenti il secondo martedì ogni mese, in modo da renderli disponibili per la sincronizzazione con Configuration Manager. Per altre informazioni, vedere le [Domande frequenti](#bkmk_faq).

</br>

|Modello di dispositivo Surface|Windows 10 1709| Windows 10 1803|Windows 10 1809|Windows 10 1903|Windows 10 1909|
|----|----|----|----|----|----|
|Surface Pro 3|Sì| Sì| Sì |Sì|Sì|
|Surface Pro 4|Sì| Sì| Sì |Sì|Sì|
|Surface Pro 6|N/D| Sì| Sì |Sì|Sì|
|Surface Pro 7|N/D| N/D| N/D |Sì|Sì|
|Surface Pro X|N/D| N/D| N/D |Sì|Sì|
|Surface Book|Sì| Sì| Sì |Sì|Sì|
|Surface Book 2|Sì| Sì| Sì |Sì|Sì|
|Surface Book 3|N/D| N/D| N/D |Sì|Sì|
|Surface Laptop|Sì, con il prodotto "Windows 10 S version 1709 and later Servicing drivers" selezionato| Sì, con il prodotto "Windows 10 S version 1803 and later Servicing drivers" selezionato|Sì, con il prodotto "Windows 10 S version 1809 and later Upgrade & Servicing drivers" selezionato|Sì, con il prodotto "Windows 10 S version 1903 and later Upgrade & Servicing drivers" selezionato|Sì, con il prodotto "Windows 10 S version 1903 and later Upgrade & Servicing drivers" selezionato|
|Surface Laptop 2|N/D| Sì |Sì|Sì|Sì|
|Surface Laptop 3|N/D| N/D|N/D|Sì |Sì|
|Surface Go|N/D| Sì, con il prodotto "Windows 10 S version 1803 and later Servicing drivers" selezionato|Sì, con il prodotto "Windows 10 S version 1809 and later Upgrade & Servicing drivers" selezionato|Sì, con il prodotto "Windows 10 S version 1903 and later Upgrade & Servicing drivers" selezionato|Sì, con il prodotto "Windows 10 S version 1903 and later Upgrade & Servicing drivers" selezionato|
|Surface Go 2|N/D| N/D| Sì |Sì|Sì, con il prodotto "Windows 10 S version 1903 and later Upgrade & Servicing drivers" selezionato|
|Surface Studio|Sì| Sì| Sì |Sì|Sì|
|Surface Studio 2|N/D| Sì| Sì |Sì|Sì|

## <a name="verify-the-configuration"></a>Verificare la configurazione

Per verificare che il punto di aggiornamento software sia configurato correttamente, usare **WsyncMgr.log** e **WCM.log**.

1. Aprire WsyncMgr.log e controllare la voce di log seguente:

    ```text
    Surface Drivers can be supported in this hierarchy since all software update points are on Windows Server 2016, WCM SCF property Sync Catalog Drivers is set. 
    …
    Sync Catalog Drivers SCF value is set to : 1
    ```

1. Se una delle due voci seguenti è registrata in **WsyncMgr.log**, verificare che sia stata selezionata l'opzione **Includi i driver di Microsoft Surface e gli aggiornamenti del firmware** nelle proprietà del punto di aggiornamento software:
   - `Sync Surface Drivers option is not set`
   - `Sync Catalog Drivers SCF value is set to : 0`

1. Aprire il file **WCM.log** e cercare elementi simili alle voci seguenti:
   ```text
   <Categories>
   <Category Id="Product:05eebf61-148b-43cf-80da-1c99ab0b8699"><![CDATA[Windows 10 and later drivers]]></Category>
   <Category Id="Product:06da2f0c-7937-4e28-b46c-a37317eade73"><![CDATA[Windows 10 Creators Update and Later Upgrade & Servicing Drivers]]></Category>
   <Category Id="Product:c1006636-eab4-4b0b-b1b0-d50282c0377e"><![CDATA[Windows 10 S and Later Servicing Drivers]]></Category>
   … …
   </Categories>
   ```

   Questa voce è un elemento XML che elenca tutte le classificazioni e i gruppi di prodotti attualmente sincronizzati dal server del punto di aggiornamento software. Se non si trovano i prodotti selezionati, verificare che siano stati salvati i prodotti per il punto di aggiornamento software.
1. È anche possibile attendere il completamento della sincronizzazione successiva. Controllare quindi se gli aggiornamenti del driver di Surface e del firmware sono elencati in Aggiornamenti software nella console di Configuration Manager. Ad esempio la console potrebbe visualizzare le seguenti informazioni: ![Driver di Surface sincronizzati nella console di Configuration Manager](media/synchronized-surface-drivers.png)

##  <a name="frequently-asked-questions-faq"></a><a name="bkmk_faq"></a> Domande frequenti

### <a name="after-i-follow-the-steps-in-this-article-my-surface-drivers-are-still-not-synchronized-why"></a>Dopo aver seguito la procedura descritta in questo articolo, i driver di Surface non sono ancora sincronizzati. Perché?

Se si esegue la sincronizzazione da un server di Windows Server Update Services (WSUS) upstream anziché da Microsoft Update, assicurarsi che il server WSUS upstream sia configurato per supportare e sincronizzare gli aggiornamenti dei driver di Surface. Tutti i server downstream sono limitati agli aggiornamenti presenti nel database del server WSUS upstream.

Sono presenti più di 68.000 aggiornamenti classificati come driver in WSUS. Per impedire la sincronizzazione con Configuration Manager di driver non Surface, Microsoft filtra la sincronizzazione dei driver rispetto a un elenco Consenti. Dopo la pubblicazione e l'incorporamento del nuovo elenco Consenti in Configuration Manager, i nuovi driver vengono aggiunti alla console al termine della sincronizzazione successiva. Microsoft prevede di aggiungere i driver di Surface all'elenco Consenti il secondo martedì ogni mese, in modo da renderli disponibili per la sincronizzazione con Configuration Manager.

Se l'ambiente di Configuration Manager è offline, viene importato un nuovo elenco Consenti ogni volta che si importano [aggiornamenti del servizio](../../core/servers/manage/use-the-service-connection-tool.md) in Configuration Manager. È anche necessario importare un [nuovo catalogo WSUS](../get-started/synchronize-software-updates-disconnected.md) contenente i driver prima che gli aggiornamenti vengano visualizzati nella console di Configuration Manager. Poiché un ambiente WSUS autonomo contiene più driver rispetto a un SUP di Configuration Manager, è consigliabile definire un ambiente di Configuration Manager con funzionalità online e configurarlo per la sincronizzazione dei driver di Surface. Questa operazione restituisce un'esportazione WSUS più piccola, molto simile all'ambiente offline.

Se l'ambiente di Configuration Manager è online e in grado di rilevare nuovi aggiornamenti, si riceveranno automaticamente gli aggiornamenti all'elenco. Se i driver previsti non vengono visualizzati, verificare i file WCM.log e WsyncMgr.log per eventuali errori di sincronizzazione.

### <a name="my-configuration-manager-environment-is-offline-can-i-manually-import-surface-drivers-into-wsus"></a>L'ambiente Configuration Manager è offline: è possibile importare manualmente i driver di Surface in WSUS?

No. Anche se l'aggiornamento viene importato in WSUS, non verrà importato nella console di Configuration Manager per la distribuzione se non è incluso nell'elenco Consenti. Per importare gli aggiornamenti di manutenzione in Configuration Manager e aggiornare l'elenco Consenti è necessario usare lo [strumento di connessione del servizio](../../core/servers/manage/use-the-service-connection-tool.md).

### <a name="what-alternative-methods-do-i-have-to-deploy-surface-driver-and-firmware-updates"></a>Quali sono i metodi alternativi per distribuire gli aggiornamenti dei driver e del firmware di Surface?

Per informazioni su come distribuire gli aggiornamenti dei driver e del firmware di Surface tramite canali alternativi, vedere [Gestire gli aggiornamenti dei driver e del firmware di Surface](https://docs.microsoft.com/surface/manage-surface-driver-and-firmware-updates). Se si vuole scaricare il file con estensione msi o exe e quindi eseguire la distribuzione tramite i canali di distribuzione software tradizionali, vedere [Mantenere aggiornato il firmware di Surface con Configuration Manager](https://docs.microsoft.com/archive/blogs/thejoncallahan/keeping-surface-firmware-updated-with-configuration-manager).

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui driver di Surface, vedere i seguenti articoli:

- [Considerazioni su Surface e System Center Configuration Manager](https://docs.microsoft.com/surface/considerations-for-surface-and-system-center-configuration-manager#deploy-surface-app-with-configuration-manager)
- [Cronologia degli aggiornamenti di Surface](https://support.microsoft.com/help/4036283/surface-surface-update-history)
- [Scaricare il firmware e i driver più recenti per i dispositivi Surface](/surface/manage-surface-driver-and-firmware-updates)
