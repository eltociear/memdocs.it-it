---
title: Installare report di esempio di Power BI
titleSuffix: Configuration Manager
description: Informazioni su come installare i report di esempio di Power BI in Configuration Manager
ms.date: 08/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7e9bc22c-67ac-4a86-b613-944a4928e583
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 450c76617cf12a3201aa990c90843cb2e0f0edee
ms.sourcegitcommit: d1bfd5b8481439babc7eae43493f28edaebe647a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/13/2020
ms.locfileid: "88179435"
---
# <a name="install-power-bi-sample-reports"></a>Installare report di esempio di Power BI
<!--5679791-->
*Si applica a: Configuration Manager (Current Branch)*

A partire dalla versione 2002, è possibile integrare [Server di report di Power BI](https://docs.microsoft.com/power-bi/report-server/get-started) con la creazione di report di Configuration Manager. Sono disponibili per il download report di esempio da installare in Configuration Manager. Questo articolo illustra come installare report di esempio di Power BI in Configuration Manager.

## <a name="prerequisites"></a>Prerequisiti

- Punto di Reporting Services in Configuration Manager con il [server di report di Power BI integrato](powerbi-report-server.md)

- [Microsoft Power BI Desktop (ottimizzato per server di report di Power BI - settembre 2019)](https://www.microsoft.com/download/details.aspx?id=57271) o versioni successive

- L'[aggiornamento cumulativo (4560496) per la versione 2002](https://support.microsoft.com/help/4560496) è consigliato ma non obbligatorio.

    > [!IMPORTANT]
    > Usare solo le versioni di Power BI Desktop dall'[Area download Microsoft](https://www.microsoft.com/download/). Non usare una versione dal Microsoft Store.
    >
    > Usare solo una versione di Power BI Desktop [ottimizzata per Server di report di Power BI](https://docs.microsoft.com/power-bi/report-server/install-powerbi-desktop).

## <a name="download-the-sample-reports"></a>Scaricare i report di esempio

Per scaricare i report di esempio:

1. Scaricare i report di esempio di Power BI dall'[Area download Microsoft](https://www.microsoft.com/download/details.aspx?id=101452).

1. Salvare il file `ConfigMgrSamplePowerBIReports.exe`.

1. Spostare il file in un computer con Microsoft Power BI Desktop (ottimizzato per server di report di Power BI) installato se il file è stato scaricato da un dispositivo diverso.

1. Eseguire il file `ConfigMgrSamplePowerBIReports.exe` per estrarre i file con estensione pbit.

## <a name="install-the-sample-reports"></a>Installare i report di esempio

Per installare i report di esempio:

1. Nel server di report di Power BI creare una nuova cartella denominata `Sample Reports` nella cartella radice dei report di Configuration Manager.

    :::image type="content" source="media/create-sample-reports-folder.png" alt-text="Creazione della cartella dei report di esempio nella cartella radice dei report di Configuration Manager" lightbox="media/create-sample-reports-folder.png":::

1. Avviare Microsoft Power BI Desktop (ottimizzato per server di report di Power BI).

1. Selezionare **File** e quindi **Apri** e passare al percorso in cui sono stati estratti i file con estensione pbit.

1. Selezionare uno dei file con estensione pbit estratti dal file `ConfigMgrSamplePowerBIReports.exe`.

1. Specificare il nome del database di Configuration Manager e il nome del server di database quando richiesto, e selezionare **Carica**.

    Quando si carica o si applica il modello di dati, ignorare eventuali errori.

    :::image type="content" source="media/sample-report-database.png" alt-text="Specificare il nome del database e del server di database" lightbox="media/sample-report-database.png":::

1. Quando vengono caricati i dati del report, selezionare **File** > **Salva con nome** e quindi **Server di report di Power BI**.

    :::image type="content" source="media/save-powerbi-report-server.png" alt-text="Salvare con nome il server di report di Power BI" lightbox="media/save-powerbi-report-server.png":::

1. Salvare il report nella cartella `Sample Reports` creata nel punto di reporting.

    :::image type="content" source="media/save-sample-report.png" alt-text="Salvare nella cartella dei report di esempio" lightbox="media/save-sample-report.png":::

1. Ripetere la procedura per tutti gli altri report di esempio. Al termine, chiudere Microsoft Power BI Desktop (ottimizzato per server di report di Power BI).

1. Nella console di Configuration Manager passare a **Monitoraggio** > **Report di Power BI** > **Report di esempio**.

1. Fare clic con il pulsante destro del mouse su uno dei report e selezionare **Esegui nel browser** per avviare il report.

    :::image type="content" source="media/view-powerbi-report.png" alt-text="Eseguire il report di esempio dalla console di Configuration Manager" lightbox="media/view-powerbi-report.png":::
