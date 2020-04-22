---
title: Strumento di registrazione dell'aggiornamento
titleSuffix: Configuration Manager
description: Informazioni su quando e come usare lo strumento di registrazione dell'aggiornamento per importare manualmente un aggiornamento nella console di Configuration Manager.
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8cc13635-85d6-4b07-a3ec-c42188bc5c74
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 420b13005e8f9ac3d79f7d94398e6aa0ddcc190c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690889"
---
# <a name="use-the-update-registration-tool-to-import-hotfixes-to-configuration-manager"></a>Usare lo strumento di registrazione dell'aggiornamento per importare hotfix in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Alcuni aggiornamenti per Configuration Manager non sono disponibili dal servizio cloud Microsoft e possono essere ottenuti solo come rilascio fuori programma. Questo si verifica, ad esempio, nel caso di un hotfix a rilascio limitato per la soluzione di un problema specifico.   
Quando è necessario installare un rilascio fuori programma e il nome file dell'aggiornamento o dell'hotfix termina con l'estensione **update.exe**, si usa lo **strumento di registrazione dell'aggiornamento** per importare manualmente l'aggiornamento nella console di Configuration Manager. Lo strumento consente di estrarre e trasferire il pacchetto di aggiornamento nel server del sito e di registrare l'aggiornamento con la console di Configuration Manager.  

 Se il file dell'hotfix ha estensione **exe** (non **update.exe**), vedere [Usare il programma di installazione di hotfix per installare gli aggiornamenti per Configuration Manager](../../../core/servers/manage/use-the-hotfix-installer-to-install-updates.md)  

> [!NOTE]  
>  Questo argomento fornisce indicazioni generali su come installare gli hotfix che aggiornano Configuration Manager. Per informazioni dettagliate su un aggiornamento o un hotfix specifico, vedere l'articolo corrispondente della Knowledge Base (KB) nel sito del supporto tecnico Microsoft.  

 **Prerequisiti per l'uso dello strumento di registrazione dell'aggiornamento:**  

-   Solo gli aggiornamenti fuori programma che terminano con l'estensione **update.exe** possono essere installati usando questo strumento  

-   Lo strumento gestisce autonomamente i singoli aggiornamenti ottenuti direttamente da Microsoft  

-   Lo strumento non dipende dalla modalità del punto di connessione del servizio  

-   Lo strumento deve essere eseguito nel computer che ospita il punto di connessione del servizio  

-   Nel computer in cui è in esecuzione lo strumento (il computer del punto di connessione del servizio) deve essere installato .NET Framework 4.52  

-   L'account usato per eseguire lo strumento deve avere le autorizzazioni di **amministratore locale** nel computer che ospita il punto di connessione del servizio dove viene eseguito lo strumento  

-   L'account usato per eseguire lo strumento deve avere le autorizzazioni di **scrittura** per la cartella seguente nel computer che ospita il punto di connessione del servizio:  **&lt;Directory di installazione di Configuration Manager\>\EasySetupPayload\offline**  

### <a name="to-use-the-update-registration-tool"></a>Per usare lo strumento di registrazione dell'aggiornamento  

1. Nel computer che ospita il punto di connessione del servizio:  

   -   Aprire un prompt dei comandi con privilegi amministrativi e quindi passare alle directory nel percorso che contiene **&lt;Prodotto\>-&lt;versione prodotto\>-&lt;ID articolo KB\>-ConfigMgr.Update.exe**  

2. Eseguire il comando seguente per avviare lo strumento di registrazione dell'aggiornamento:  

   -   **&lt;Prodotto\>-&lt;versione prodotto\>-&lt;ID articolo KB\>-ConfigMgr.Update.exe**  

   Dopo la registrazione, l'hotfix, viene visualizzato come nuovo aggiornamento nella console entro 24 ore.  È possibile accelerare il processo:

   - Aprire la console di Configuration Manager, passare ad **Amministrazione** > **Aggiornamenti e manutenzione** e quindi fare clic su **Verifica la disponibilità di aggiornamenti**. Nelle versioni precedenti la 1702, Aggiornamenti e manutenzione si trova in **Amministrazione** > **Servizi cloud**. 

   Lo strumento di registrazione dell'aggiornamento registra le azioni in un file con estensione log nel computer locale. Il file di log ha lo stesso nome del file EXE dell'hotfix e viene scritto nella cartella **%SystemRoot%/Temp**.  

    Dopo la registrazione dell'aggiornamento, è possibile chiudere lo strumento di registrazione.  

3. Aprire la console di Configuration Manager e passare ad **Amministrazione** > **Aggiornamenti e manutenzione**. Gli hotfix importati sono ora disponibili per l'installazione. Nelle versioni precedenti la 1702, Aggiornamenti e manutenzione si trova in **Amministrazione** > **Servizi cloud**.

   Per informazioni sull'installazione degli aggiornamenti, vedere [Installare gli aggiornamenti nella console per Configuration Manager](../../../core/servers/manage/install-in-console-updates.md)  
