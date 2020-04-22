---
title: Testare l'aggiornamento del database
titleSuffix: Configuration Manager
description: Testare l'aggiornamento del database del sito durante l'installazione di aggiornamenti per Configuration Manager.
ms.date: 06/13/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: abb696f3-a816-4f12-a9f1-0503a81e1976
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 56c1422f4157b255f4f7a8624e36d10e01f28fc0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703289"
---
# <a name="test-the-database-upgrade-when-installing-an-update"></a>Testare l'aggiornamento del database quando si installa un aggiornamento

*Si applica a: Configuration Manager (Current Branch)*

Questo argomento descrive come eseguire il test dell'aggiornamento del database prima di installare un aggiornamento nella console per il Current Branch di Configuration Manager. Tuttavia, questo passaggio non è più necessario o consigliabile, a meno che la condizione del database sia sospetta o che il database sia stato modificato da personalizzazioni non supportate in modo esplicito da Configuration Manager.

## <a name="do-i-need-to-run-a-test-upgrade"></a>È necessario eseguire un test dell'aggiornamento?
La deprecazione di questo test dell'aggiornamento è stata possibile grazie alle modifiche introdotte con Configuration Manager. Queste modifiche semplificano il processo e la velocità con cui è possibile aggiornare un ambiente di produzione a versioni più recenti. Questa riprogettazione consente ora ai clienti di rimanere aggiornati con meno rischi e minori costi operativi durante l'installazione di ogni nuovo aggiornamento.

Le modifiche interessano la modalità di installazione degli aggiornamenti, inclusa la logica che esegue automaticamente il rollback di un aggiornamento non riuscito senza la necessità di eseguire un ripristino del sito. Queste modifiche consentono l'uso della console per gestire le installazioni degli aggiornamenti e includono un'opzione per [ripetere l'installazione di un aggiornamento non riuscito](install-in-console-updates.md#bkmk_retry).

> [!TIP]
> Quando si esegue l'aggiornamento a Configuration Manager Current Branch da una versione precedente, ad esempio System Center 2012 Configuration Manager, l'[esecuzione del test degli aggiornamenti del database è ancora un'operazione consigliata](../deploy/install/upgrade-to-configuration-manager.md#bkmk_test).

Se si intende testare l'aggiornamento di un database del sito quando si installa un aggiornamento nella console, le informazioni seguenti integrano il [materiale sussidiario sull'installazione di un aggiornamento nella console](install-in-console-updates.md#bkmk_install).

## <a name="prepare-to-run-a-test-database-upgrade"></a>Preparare l'esecuzione di un test dell'aggiornamento del database  
Prima di installare un nuovo aggiornamento nella gerarchia, ad esempio l'aggiornamento 1702, è possibile testare l'aggiornamento del database del sito.

Per eseguire il test dell'aggiornamento, usare l'installazione di Configuration Manager dai file di origine dalla [cartella CD.Latest](the-cd.latest-folder.md) di un sito che esegue la versione di Configuration Manager a cui si sta eseguendo l'aggiornamento. Questo requisito implica che per testare l'aggiornamento del database per l'aggiornamento alla versione 1702:
-   È necessario disporre di almeno un sito che esegue la versione 1702 da cui è possibile ottenere questa cartella CD.Latest.
-   Se non si dispone di un sito che esegue la versione richiesta, è consigliabile installare un sito in un ambiente lab e quindi aggiornare il sito alla nuova versione. Verrà creata la cartella CD.Latest con la versione corretta dei file di origine.

Il test dell'aggiornamento viene eseguito su un backup del database del sito che è stato ripristinato in un'istanza separata di SQL Server.  Si esegue l'installazione dalla cartella **CD.Latest** con l'opzione da riga di comando **testdbupgrade** per testare l'aggiornamento che ha ripristinato la copia del database. Al completamento del test dell'aggiornamento, il database aggiornato viene eliminato. Non può essere usato da un sito di Configuration Manager.

Se si verifica un errore in fase di aggiornamento, non è consigliabile ripristinare il sito. In alternativa, è possibile ritentare l'installazione dell'aggiornamento dall'interno della console.

##  <a name="run-the-test-upgrade"></a>Eseguire il test dell'aggiornamento    
1. Usare il programma di installazione di Configuration Manager e i file di origine dalla cartella **CD.Latest** di un sito che esegue la versione a cui si intende eseguire l'aggiornamento.  

2. Copiare la cartella **CD.Latest** in un percorso dell'istanza di SQL Server che verrà usata per eseguire l'aggiornamento di test del database.

3. Creare un backup del database del sito di cui di intende verificare l'aggiornamento. Ripristinare quindi una copia del database del sito in un'istanza di SQL Server che non ospita un sito di Configuration Manager. L'istanza di SQL Server deve usare la stessa edizione di SQL Server del database del sito.  

4. Dopo avere ripristinato la copia del database, eseguire **Installazione** dalla cartella CD.Latest che contiene i file di origine dalla versione a cui si sta eseguendo l'aggiornamento. Quando si esegue l'installazione, usare l'opzione della riga di comando **/TESTDBUPGRADE** . Se l'istanza di SQL Server che ospita la copia del database non è quella predefinita, fornire gli argomenti della riga di comando per identificare l'istanza che ospita la copia del database del sito.   

   Ad esempio, si dispone di un database del sito con il nome database *SMS_ABC*. Si ripristina una copia di questo database del sito in un'istanza supportata di SQL Server con il nome istanza *DBTest*. Per testare un aggiornamento di questa copia del database del sito, usare la riga di comando seguente: **Setup.exe /TESTDBUPGRADE DBtest\CM_ABC**.  

   È possibile trovare Setup.exe nel percorso seguente del supporto di origine per Configuration Manager: **SMSSETUP\BIN\X64**.  

5. Nell'istanza di SQL Server in cui si esegue il test di aggiornamento, monitorare *ConfigMgrSetup.log* nella radice dell'unità di sistema per l'avanzamento e il completamento.  

    Se il test dell'aggiornamento ha esito negativo, risolvere eventuali problemi associati all'errore di aggiornamento del database del sito. Creare quindi un nuovo backup del database del sito e testare l'aggiornamento della nuova copia del database.  



## <a name="next-steps"></a>Passaggi successivi
Dopo il corretto completamento del test dell'aggiornamento del database, eliminare il database aggiornato. Non può essere usato da un sito di Configuration Manager. È quindi possibile tornare al sito attivo e [iniziare l'installazione dell'aggiornamento](install-in-console-updates.md).
