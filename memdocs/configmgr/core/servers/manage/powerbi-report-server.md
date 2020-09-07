---
title: Integrare il server di report di Power BI
titleSuffix: Configuration Manager
description: Integrare il server di report di Power BI con la creazione di report di Configuration Manager Reporting per una visualizzazione moderna e prestazioni migliori.
ms.date: 04/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 315e2613-dc71-46b1-80cb-26161d08103a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: dc8aa57bda5f5a29d72af854be9a18e4f32760f8
ms.sourcegitcommit: 7b656712cc9340d18211c7754cb99bcaae91b0ca
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/03/2020
ms.locfileid: "89432541"
---
# <a name="integrate-with-power-bi-report-server"></a>Integrare il server di report di Power BI

*Si applica a: Configuration Manager (Current Branch)*

<!--3721603-->

A partire dalla versione 2002, è possibile integrare [Server di report di Power BI](/power-bi/report-server/get-started) con la creazione di report di Configuration Manager. Questa integrazione offre una visualizzazione moderna e prestazioni migliori. Aggiunge il supporto della console per report di Power BI simili a quelli già esistenti con SQL Server Reporting Services.

Salvare i file di report di Power BI Desktop (con estensione PBIX) e distribuirli nel server di report di Power BI. Questo processo è simile a quello dei file di report di SQL Server Reporting Services (con estensione RDL). È anche possibile avviare i report nel browser direttamente dalla console di Configuration Manager.

## <a name="prerequisites"></a>Prerequisiti

- Licenza del server di report di Power BI. Per altre informazioni, vedere [Licenze di Server di report di Power BI](/power-bi/report-server/get-started#licensing-power-bi-report-server).

- Scaricare [Server di report di Microsoft Power BI - settembre 2019](https://www.microsoft.com/download/details.aspx?id=57270) o versioni successive.

    > [!NOTE]
    > Non installare immediatamente Server di report di Power BI. Per il processo appropriato basato sull'ambiente, vedere [Configurare il punto di Reporting Services](#configure-the-reporting-services-point).

- Scaricare [Microsoft Power BI Desktop (ottimizzato per Server di report di Power BI - settembre 2019)](https://www.microsoft.com/download/details.aspx?id=57271) o versioni successive.

    > [!IMPORTANT]
    > - Usare solo le versioni di Power BI Desktop dall'[Area download Microsoft](https://www.microsoft.com/download/). Non usare una versione da Microsoft Store.
    > - Usare solo una versione di [Power BI Desktop dichiarata come **ottimizzata per Server di report di Power BI**](/power-bi/report-server/install-powerbi-desktop).

- L’integrazione di Power BI usa la stessa amministrazione basata su ruoli per la creazione di report.
    > [!NOTE]
    > Il server di report di Power BI non supporta i report abilitati per il controllo degli accessi in base al ruolo, pertanto tutti gli utenti dei report visualizzeranno gli stessi risultati indipendentemente dall'ambito assegnato.

## <a name="configure-the-reporting-services-point"></a>Configurare il punto di Reporting Services

Questo processo varia a seconda che il ruolo sia già presente nel sito.

### <a name="you-have-a-reporting-services-point"></a>È disponibile un punto di Reporting Services

Usare questo processo solo se si ha già un punto di Reporting Services nel sito. Eseguire tutti i passaggi di questo processo nello stesso server:

1. In **Configuration Manager del server di report** eseguire il backup delle **chiavi di crittografia**. Per altre informazioni, vedere [Chiavi di crittografia SSRS - Eseguire il backup e il ripristino delle chiavi di crittografia](/sql/reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys).

    > [!WARNING]
    > Se si ignora questo passaggio, si perderà l'accesso a tutti i report personalizzati in SQL Server Reporting Services.

1. Rimuovere il ruolo del punto di Reporting Services dal sito.

1. Disinstallare SQL Server Reporting Services, ma mantenere il database.

1. Installare il server di report di Power BI.

1. Configurare il server di report di Power BI

    1. Usare il database del server di report precedente.

    1. Usare **Configuration Manager del server di report** per ripristinare le **chiavi di crittografia**.

1. Aggiungere il ruolo del punto di Reporting Services in Configuration Manager.

### <a name="you-dont-have-a-reporting-services-point"></a>Non è disponibile un punto di Reporting Services

Usare questo processo solo se non si ha già un punto di Reporting Services nel sito. Eseguire tutti i passaggi di questo processo nello stesso server:

1. Installare il server di report di Power BI.

2. Aggiungere il ruolo del punto di Reporting Services in Configuration Manager. Per altre informazioni, vedere [Configurare la creazione di report in Reporting Manager](configuring-reporting.md).

## <a name="configure-the-configuration-manager-console"></a>Configurare la console di Configuration Manager

1. In un computer con la console di Configuration Manager aggiornare la console di Configuration Manager alla versione più recente.

1. Installare Power BI Desktop. Assicurarsi che la lingua sia la stessa.

1. Dopo l'installazione, avviare Power BI Desktop almeno una volta prima di aprire la console di Configuration Manager.

## <a name="create-power-bi-reports"></a>Creare report di Power BI

1. Nella console di Configuration Manager passare all'area di lavoro **Monitoraggio**, espandere **Report** e selezionare il nuovo nodo **Report di Power BI**.

1. Nella barra multifunzione selezionare **Crea report**. Questa azione consente di aprire Power BI Desktop.

1. Creare un report in Power BI Desktop.

    - In Power BI Desktop, quando ci si connette a un'origine dati, selezionare **DirectQuery** per le impostazioni di connessione.

    - Usare solo le viste SQL supportate in questi report. Per altre informazioni, vedere [Creazione di report personalizzati usando viste di SQL Server in Configuration Manager](../../../develop/core/understand/sqlviews/create-custom-reports-using-sql-server-views.md).

1. Quando il report è pronto per il salvataggio, passare al menu **File**, selezionare **Salva con nome** e quindi scegliere **Server di report di Power BI**.

1. Nella finestra **Selezione Server di report di Power BI** immettere l'URL per il punto di Reporting Services come **Nuovo indirizzo del server di report**. Ad esempio, `https://rsp.contoso.com/Reports` Selezionare **OK**.

1. Nella finestra **Salva report** fare doppio clic sulla cartella `ConfigMgr_<SiteCode>`. Ad esempio, `ConfigMgr_PS1`, dove `PS1` è il codice del sito ConfigMgr. Facoltativamente, è possibile scegliere o creare (dal server di report) una sottocartella in cui archiviarlo.
    > [!TIP]
    > I report e le cartelle di report con report di Power BI devono trovarsi nella cartella `ConfigMgr_<SiteCode>` nel server di report o non verranno visualizzati nella console di Configuration Manager.

1. In **Nome file** immettere un nome per il report.

Nella console di Configuration Manager viene visualizzato il nuovo report nell'elenco dei report di Power BI. Se i report non vengono visualizzati, verificare che i report siano stati salvati nella cartella `ConfigMgr_<SiteCode>`.

## <a name="next-steps"></a>Passaggi successivi

Dopo aver creato un report, usare le azioni seguenti nella console di Configuration Manager:

- **Esegui nel browser**: apre il report di Power BI nel Web browser. Condividere questo URL con altri utenti, ad esempio: `https://rsp.contoso.com/Reports/POWERBI/ConfigMgr_ABC/Windows%2010/Windows10%20Dashboard?rs:embed=true`

    > [!TIP]
    > È possibile visualizzare questi report solo nel Web browser.

- **Modifica**: apportare modifiche al report in Power BI Desktop. Per un report esistente, usare l'opzione **Salva** per salvare di nuovo le modifiche nel server di report.

Per altre informazioni sui file di log da usare per la creazione di report, vedere [Riferimento ai file di log - Creazione di report](../../plan-design/hierarchy/log-files.md#BKMK_ReportLog).
