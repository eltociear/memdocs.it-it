---
title: Comandi di preavvio per supporti per sequenza di attività
titleSuffix: Configuration Manager
description: Creare un script da usare con il comando di preavvio, distribuire il contenuto associato al comando di preavvio e configurare il comando di preavvio nel supporto.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: ccc9f652-2953-4c38-8a90-c799484105ca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9dd921d58e6ef777017af3e2eb24dbf4bd611fab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81699769"
---
# <a name="prestart-commands-for-task-sequence-media-in-configuration-manager"></a>Comandi di preavvio del supporto per sequenza attività in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

È possibile creare un comando di preavvio in Configuration Manager da usare con i supporti di avvio, i supporti autonomi e i supporti preinstallati. Il comando di preavvio è uno script o un eseguibile che viene eseguito prima che la sequenza attività venga selezionata e possa interagire con l'utente in Windows PE. Il comando di preavvio può richiedere informazioni a un utente e salvarle nell'ambiente della sequenza attività oppure eseguire una query di una variabile della sequenza attività per le informazioni. All'avvio del computer di destinazione, la riga di comando viene eseguita prima che il criterio venga scaricato dal punto di gestione. Utilizzare le procedure seguenti per creare uno script da utilizzare per il comando di preavvio, distribuire il contenuto associato al comando di preavvio e configurare il comando di preavvio nei supporti.  

## <a name="create-a-script-file-to-use-for-the-prestart-command"></a>Creare un file di script da usare per il comando di preavvio  
 Le variabili della sequenza di attività possono essere lette e scritte usando l'oggetto COM Microsoft.SMS.TSEnvironment durante l'esecuzione della sequenza di attività. Nell'esempio che segue viene illustrato un file di script Visual Basic che esegue la query della variabile della sequenza attività _SMSTSLogPath per ottenere la posizione corrente del registro. Lo script imposta inoltre una variabile personalizzata.  

``` VBScript
dim osd: set env = CreateObject("Microsoft.SMS.TSEnvironment")  
dim logPath  
' You can query the environment to get an existing variable.  
logPath = env("_SMSTSLogPath")  
' You can also set a variable in the OSD environment.  
env("MyCustomVariable") = "varname"  
```  

## <a name="create-a-package-for-the-script-file-and-distribute-the-content"></a>Creare un pacchetto per il file di script e distribuire il contenuto  
 Dopo aver creato lo script o l'eseguibile per il comando di preavvio, occorre creare un'origine del pacchetto per ospitare i file per lo script o l'eseguibile, creare un pacchetto per i file (nessun programma richiesto), quindi distribuire il contenuto in un punto di distribuzione.  

 Per altre informazioni sulla creazione di un pacchetto, vedere [Pacchetti e programmi](../../apps/deploy-use/packages-and-programs.md).  

 Per altre informazioni sulla distribuzione di contenuto, vedere [Distribuire contenuto](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

## <a name="configure-the-prestart-command-in-media"></a>Configurare il comando di preavvio nei supporti  
 È possibile configurare il comando di preavvio nella Creazione guidata del supporto per la sequenza attività per supporti autonomi, supporti di avvio o supporti pre-installati. Per altre informazioni sui tipi di supporto, vedere [Creare supporti per le sequenza di attività](../deploy-use/create-task-sequence-media.md). Utilizzare la procedura seguente per creare un comando di preavvio nei supporti.  

#### <a name="to-create-a-prestart-command-in-media"></a>Per creare un comando di preavvio nei supporti  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi**, quindi fare clic su **Sequenze attività**.  

3.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea supporto per sequenza di attività** per avviare la Creazione guidata del supporto per la sequenza di attività.  

4.  Nella pagina **Seleziona tipo di supporto** , selezionare **Supporto autonomo**, **Supporto di avvio**o **Supporti preinstallati**, quindi fare clic su **Avanti**.  

5.  Spostarsi nella pagina **Personalizzazione** della procedura guidata. Per altre informazioni sulla configurazione delle altre pagine della procedura guidata, vedere [Creare supporti per le sequenza di attività](../deploy-use/create-task-sequence-media.md).  

6.  Nella pagina **Personalizzazione** specificare le informazioni seguenti e quindi fare clic su **Avanti**.  

    -   Selezionare **Attiva comando di preavvio**.  

    -   Nella casella di testo **Riga di comando** , inserire lo script o l'eseguibile creato per il comando di preavvio.  

        > [!IMPORTANT]  
        >  Usare **cmd /C <comando preavvio\>** per specificare il comando di preavvio. Ad esempio, se si è usato TSScript.vbs come nome dello script del comando di preavvio, è necessario immettere **cmd /C TSScript.vbs** per la riga di comando. Dove **cmd /C** apre una nuova finestra dell'interprete dei comandi di Windows e usa la variabile di ambiente Path per trovare lo script o l'eseguibile del comando di preavvio. È possibile inoltre specificare l'intero percorso al comando di preavvio, ma la lettera unità potrebbe essere diversa su computer con configurazioni unità diverse.  

    -   Selezionare **Includi file per il comando di preavvio**.  

    -   Fare clic su **Imposta** per selezionare il pacchetto associato con i file del comando di preavvio.  

    -   Fare clic su **Sfoglia** per selezionare il punto di distribuzione che ospita il contenuto per il comando di preavvio.  

7.  Completare la procedura guidata.  
