---
title: Gestire i pacchetti di aggiornamento del sistema operativo
titleSuffix: Configuration Manager
description: Informazioni su come gestire i pacchetti di aggiornamento del sistema operativo in Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: b9b22655-b8c1-461f-8047-3a7e906f647a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a50592815ed4581c01489f90b6c3701e53bb4981
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124415"
---
# <a name="manage-os-upgrade-packages-with-configuration-manager"></a>Gestire i pacchetti di aggiornamento del sistema operativo in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Un pacchetto di aggiornamento in Configuration Manager contiene i file di origine dell'installazione di Windows per l'aggiornamento di un sistema operativo esistente in un computer. Questo articolo descrive come aggiungere, distribuire e gestire un pacchetto di aggiornamento del sistema operativo.

> [!NOTE]
> I pacchetti di aggiornamento del sistema operativo possono essere usati anche per le nuove installazioni di Windows. Ciò dipende, tuttavia, dalla compatibilità dei driver con questo metodo. Quando si eseguono nuove installazioni di Windows da un pacchetto di aggiornamento del sistema operativo, i driver vengono installati quando si trovano ancora in Windows PE, anziché essere semplicemente inseriti mentre sono in Windows PE. Alcuni driver non sono compatibili con l'installazione da Windows PE. Se i driver non sono compatibili per l'installazione mentre sono in Windows PE, usare invece un'[immagine del sistema operativo](manage-operating-system-images.md), ad esempio **install.wim**.

## <a name="add-an-os-upgrade-package"></a><a name="BKMK_AddOSUpgradePkgs"></a> Aggiungere pacchetto di aggiornamento del sistema operativo  

Prima di poter usare un pacchetto di aggiornamento del sistema operativo, è necessario aggiungerlo al sito di Configuration Manager.

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**, espandere **Sistemi operativi** e selezionare il nodo **Pacchetti di aggiornamento del sistema operativo**.  

2. Nella scheda **Home** della barra multifunzione, nel gruppo **Crea** selezionare **Aggiungi pacchetto di aggiornamento del sistema operativo**. Questa azione avvia l'Aggiunta guidata del pacchetto di aggiornamento del sistema operativo.  

3. Nella pagina **Origine dati** specificare le impostazioni seguenti:

    - In **Percorso** specificare il percorso di rete dei file di origine per l'installazione del pacchetto di aggiornamento del sistema operativo. Ad esempio, `\\server\share\path`  

        > [!NOTE]  
        >  I file di origine dell'installazione contengono Setup.exe e altri file e cartelle per installare il sistema operativo.  

        > [!IMPORTANT]  
        >  Limitare l'accesso a questi file di origine dell'installazione per impedire manomissioni indesiderate.  

    - **Estrarre un indice di immagine specifico dal file install.wim del pacchetto di aggiornamento selezionato** e quindi selezionare un indice di immagine dall'elenco.<!--4931110--> A partire dalla versione 1910, questa opzione importa automaticamente un solo indice anziché tutti gli indici delle immagini nel file. L'uso di questa opzione genera un file di immagine più piccolo e un'installazione offline più rapida. Supporta anche il processo [Servizio immagini ottimizzato](#bkmk_resetbase) che genera un file di immagine più piccolo dopo l'applicazione degli aggiornamenti software.  

        > [!IMPORTANT]  
        > Configuration Manager sovrascrive il file install.wim esistente nel pacchetto di aggiornamento del sistema operativo. Estrae l'indice dell'immagine in una posizione temporanea e quindi lo sposta nella directory di origine originale. Prima di importare un pacchetto di aggiornamento del sistema operativo e abilitare questa opzione, assicurarsi di eseguire il backup dei file di origine originali.

    - Se si desidera memorizzare in anteprima contenuto nella cache in un client, specificare **Architettura** e **Lingua** dell'immagine. Per altre informazioni, vedere [Configurare la pre-cache del contenuto](../deploy-use/configure-precache-content.md).  

4. Nella pagina **Generale** specificare le informazioni seguenti. Queste informazioni sono utili per scopi di identificazione quando sono presenti più pacchetti di aggiornamento del sistema operativo.  

    - **Nome**: nome univoco del pacchetto di aggiornamento del sistema operativo.  

    - **Versione**: identificatore di versione facoltativo. Questa proprietà non deve corrispondere alla versione del sistema operativo del pacchetto di aggiornamento. Si tratta spesso della versione assegnata dall'organizzazione al pacchetto.  

    - **Commento**: breve descrizione facoltativa.  

5. Completare la procedura guidata.  

Quindi distribuire il pacchetto di aggiornamento del sistema operativo ai punti di distribuzione.  

## <a name="distribute-content-to-a-distribution-point"></a><a name="BKMK_Distribute"></a> Distribuire il contenuto a un punto di distribuzione  

Distribuire i pacchetti di aggiornamento del sistema operativo nei punti di distribuzione, con le stesse modalità usate per altri contenuti. Prima di distribuire la sequenza di attività, distribuire il pacchetto di aggiornamento del sistema operativo ad almeno un punto di distribuzione. Per altre informazioni, vedere [Distribuire il contenuto](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

[!INCLUDE [Apply software updates to an image](includes/wim-apply-updates.md)]

## <a name="next-steps"></a>Passaggi successivi

[Creare una sequenza di attività per aggiornare un sistema operativo](../deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md)
