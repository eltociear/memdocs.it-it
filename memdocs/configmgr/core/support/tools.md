---
title: Strumenti di Configuration Manager
titleSuffix: Configuration Manager
description: Informazioni sugli strumenti che consentono di gestire e risolvere i problemi di infrastruttura di Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 395403dc-6997-4415-93fd-6b1eeb6ba31a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: cb2529dbbe923a5035f0b7586dab696cd6fc917e
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699416"
---
# <a name="configuration-manager-tools"></a>Strumenti di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Gli strumenti di Configuration Manager comprendono [strumenti basati su client](#client-tools) e [strumenti basati su server](#server-tools). Questi strumenti consentono di supportare e risolvere i problemi di infrastruttura di Configuration Manager.

A partire dalla versione 1806 di Configuration Manager, questi strumenti sono inclusi nella cartella `CD.Latest\SMSSETUP\Tools` nel server del sito. Non è necessaria un'ulteriore installazione.<!--1357145--> Usare queste versioni degli strumenti con Configuration Manager versione 1806 e versioni successive.

Tutti i sistemi operativi Windows indicati come client supportati in [Sistemi operativi supportati per client e dispositivi](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices) sono supportati per l'uso con questi strumenti.

> [!Note]  
> Il [System Center 2012 R2 Configuration Manager Toolkit](https://www.microsoft.com/download/details.aspx?id=50012) è ancora disponibile nell'Area download Microsoft. Per Configuration Manager versione 1806 e versioni successive, usare le versioni degli strumenti nella cartella CD.Latest nel server del sito. Alcuni strumenti erano precedentemente presenti nel toolkit ma non sono stati inclusi nella versione 1806. Questi strumenti legacy non sono più supportati.


## <a name="client-tools"></a>Strumenti client

Questi strumenti si trovano nella sottocartella `ClientTools`:

- [CMTrace](cmtrace.md): consente di visualizzare, monitorare e analizzare i file di log di Configuration Manager  

- [Client Spy](clispy.md): consente di risolvere i problemi relativi alla distribuzione del software, all'inventario e alla misurazione

- [Deployment Monitoring Tool](deployment-monitoring-tool.md): consente di risolvere i problemi di applicazioni, aggiornamenti e distribuzioni delle linee di base  

- [Policy Spy](policy-spy.md): consente di visualizzare le assegnazioni dei criteri  

- [Power Viewer Tool](power-viewer-tool.md): consente di visualizzare lo stato della funzionalità di risparmio energia  

- [Send Schedule Tool](send-schedule-tool.md): consente di attivare pianificazioni e valutazioni delle linee di base di configurazione  

> [!Note]  
> La cartella `ClientTools` include anche il file Microsoft.Diagnostics.Tracing.EventSource.dll. Diversi strumenti client richiedono questa libreria. Non è possibile utilizzarla direttamente.  


## <a name="server-tools"></a>Strumenti server

Questi strumenti si trovano nella sottocartella `ServerTools`:

- [DP Job Queue Manager](dp-job-manager.md): consente di risolvere i problemi dei processi di distribuzione del contenuto ai punti di distribuzione  

- [Collection Evaluation Viewer](ceviewer.md): consente di visualizzare informazioni dettagliate sulla valutazione della raccolta  

- [Content Library Explorer](content-library-explorer.md): consente di visualizzare il contenuto dell'archivio a istanza singola della raccolta contenuto  

- [Content Library Transfer](content-library-transfer.md): trasferisce la raccolta contenuto tra diverse unità  

- [Content Ownership Tool](content-ownership-tool.md): modifica la proprietà dei pacchetti orfani. Questi pacchetti sono presenti nel sito senza un server del sito proprietario.

- [Role-based Administration and Auditing Tool](rbaviewer.md): consente agli amministratori di controllare la configurazione dei ruoli  

- [Run Meter Summarization Tool](run-meter-summ.md): consente di eseguire l'attività di riepilogo misurazione e di analizzare i dati di misurazione

> [!Note]  
> La cartella ServerTools include anche i file seguenti:
>
> - AdminUI.WqlQueryEngine.dll
> - Microsoft.ConfigurationManagement.ManagementProvider.dll
> - Microsoft.Diagnostics.Tracing.EventSource.dll
>
> Diversi strumenti server richiedono queste librerie. Non è possibile utilizzarli direttamente.  

## <a name="other-tools-and-toolkits"></a>Altri strumenti e toolkit

- [Support Center](support-center.md): Raccogliere informazioni dai client per eseguire più facilmente l'analisi durante la risoluzione dei problemi.

    A partire dalla versione 1906 **OneTrace** è un nuovo visualizzatore log del Supporto tecnico. Funziona in modo analogo a CMTrace, con miglioramenti. Per altre informazioni, vedere [Supporto tecnico OneTrace](support-center-onetrace.md).

- [Estendi ed esegui la migrazione dell'ambiente locale di Configuration Manager in Microsoft Azure](azure-migration-tool.md): consente di creare a livello di codice macchine virtuali di Azure per Configuration Manager. <!--3556022--> 

- [Content Library Cleanup Tool](../plan-design/hierarchy/content-library-cleanup-tool.md): usare **ContentLibraryCleanup.exe** in `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` per rimuovere contenuto orfano da un punto di distribuzione.  

- [Strumento di manutenzione gerarchia](../servers/manage/hierarchy-maintenance-tool-preinst.exe.md): usare **Preinst.exe** nella cartella condivisa `\<SiteServerName>\SMS_<SiteCode>\bin\X64\00000409` nel server del sito per passare i comandi al componente di gestione della gerarchia.  

- [Strumento di reimpostazione dell'aggiornamento](../servers/manage/update-reset-tool.md): usare **CMUpdateReset.exe** in `CD.Latest\SMSSETUP\TOOLS\CMUpdateReset` per risolvere i problemi quando gli aggiornamenti nella console mostrano problemi di download o replica.  

- [Strumento di connessione del servizio](../servers/manage/hierarchy-maintenance-tool-preinst.exe.md): usare **ServiceConnectionTool.exe** in `CD.Latest\SMSSETUP\TOOLS\ServiceConnectionTool` per mantenere aggiornato il sito quando il punto di connessione del servizio è offline.   

- [Microsoft Deployment Toolkit (MDT)](../../mdt/use-the-mdt.md): Raccolta unificata di strumenti, processi e linee guida per l'automazione delle distribuzioni dei sistemi operativi desktop e server.

- [System Center Updates Publisher (SCUP)](../../sum/tools/updates-publisher.md): Strumento autonomo per gestire e importare aggiornamenti software personalizzati.

- [Package Conversion Manager](../../apps/pcm/package-conversion-manager.md): Convertire i pacchetti in applicazioni.