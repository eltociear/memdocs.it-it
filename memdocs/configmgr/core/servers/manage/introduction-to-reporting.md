---
title: Introduzione ai report
titleSuffix: Configuration Manager
description: Informazioni sui set di strumenti e risorse disponibili per la gestione della creazione di report in Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 230be984-d2cd-4d53-bd7a-bc24dd93fc22
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: bfed31b820ac1f09b240122207b5bf27e432b10a
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/09/2020
ms.locfileid: "89607527"
---
# <a name="introduction-to-reporting-in-configuration-manager"></a>Introduzione alla creazione di report in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

La creazione di report in Configuration Manager offre un set di strumenti e risorse che consentono di usare le funzionalità di reporting avanzate di SQL Server Reporting Services (SSRS) e Server di report di Power BI. Entrambe le piattaforme offrono ricche esperienze per la creazione di report personalizzati. La creazione di report aiuta a raccogliere, organizzare e presentare informazioni sull'ampia gamma di dati di Configuration Manager presenti nell'organizzazione. Configuration Manager offre numerosi report predefiniti in Reporting Services che è possibile usare senza modifiche. È possibile duplicare e modificare i report predefiniti in base per adattarli alle proprie esigenze oppure creare report personalizzati.

## <a name="sql-server-reporting-services"></a>SQL Server Reporting Services

SQL Server Reporting Services fornisce una gamma completa di strumenti e servizi pronti per l'uso che consentono di creare, distribuire e gestire report per l'organizzazione. Dispone inoltre di funzionalità di programmazione che consentono di estendere e personalizzare la funzionalità di creazione di report. Reporting Services è una piattaforma per la creazione di report basata su server che fornisce funzionalità di creazione di report complete per diversi tipi di origini dati.

Configuration Manager usa SQL Server Reporting Services come soluzione principale per la creazione di report. L'integrazione con Reporting Services offre i seguenti vantaggi:  

- Usa un sistema di creazione di report standard di settore per eseguire query nel database di Configuration Manager.  

- Visualizza i report usando Visualizzatore report di Configuration Manager oppure Gestione report, che è una connessione al report basata su Web.  

- Fornisce scalabilità, disponibilità e prestazioni elevate.  

- Fornisce agli utenti la possibilità di sottoscrivere report. Ad esempio, un manager può eseguire una sottoscrizione per ricevere automaticamente tramite posta elettronica un report con i dettagli dello stato dell'implementazione di un aggiornamento software.

- Esporta report in una varietà dei formati più diffusi.  

Per altre informazioni, vedere [Che cos'è SQL Server Reporting Services (SSRS)?](/sql/reporting-services/create-deploy-and-manage-mobile-and-paginated-reports)

## <a name="power-bi-report-server"></a>Server di report di Power BI

<!-- 3721603 -->

A partire dalla versione 2002, è possibile integrare il Server di report di Power BI con la creazione di report di Configuration Manager. Questa integrazione offre una visualizzazione moderna e prestazioni migliori. Aggiunge il supporto della console per report di Power BI simili a quelli già esistenti con SQL Server Reporting Services. Per altre informazioni, vedere [Integrare il server di report di Power BI](powerbi-report-server.md).

Server di report di Power BI è un server di report locale con un portale Web in cui è possibile visualizzare e gestire i report. Include strumenti per creare report di Power BI, report impaginati, report per dispositivi mobili e indicatori KPI. Per altre informazioni, vedere [Che cos'è Server di report di Power BI?](/power-bi/report-server/get-started).

## <a name="reporting-services-point"></a>Punto di Reporting Services

Il punto di Reporting Services è un ruolo del sistema del sito che si aggiunge a un server che esegue Microsoft SQL Server Reporting Services. Il punto di Reporting Services svolge le funzioni seguenti:

- Copia le definizioni report di Configuration Manager in Reporting Services
- Crea cartelle report basate sulle categorie report
- Imposta criteri di sicurezza per le cartelle report e i report. Questi criteri sono basati sulle autorizzazioni basate su ruoli per gli utenti amministratori di Configuration Manager. In un intervallo di 10 minuti, il punto di Reporting Services si connette a Reporting Services per riapplicare i criteri di sicurezza se sono stati modificati.

Per altre informazioni su come pianificare e installare un punto di Reporting Services, vedere gli articoli seguenti:

- [Pianificare la creazione di report](planning-for-reporting.md)

- [Configurare la creazione di report](configuring-reporting.md)

## <a name="configuration-manager-reports"></a>Report di Configuration Manager

Configuration Manager fornisce le definizioni di oltre 400 report in oltre 50 cartelle report. Durante il processo di installazione del punto di Reporting Services, queste definizioni vengono copiate nella cartella report radice di SQL Server Reporting Services. I report vengono visualizzati nella console di Configuration Manager e organizzati in sottocartelle in base alla categoria.

I report non vengono propagati nella gerarchia di Configuration Manager in alcuna direzione. Vengono eseguiti solo per il database del sito in cui vengono creati. Poiché Configuration Manager replica i dati globali in tutta la gerarchia, nei report è possibile accedere alle informazioni a livello di gerarchia. Quando un report recupera dati dal database di un sito, ha accesso ai dati del sito per il sito corrente e i relativi siti figlio e ai dati globali per ciascun sito della gerarchia.

Come altri oggetti di Configuration Manager, per eseguire o modificare report un utente amministratore deve disporre delle autorizzazioni appropriate. Per eseguire un report, è necessario che un utente amministratore disponga dell'autorizzazione **Esegui report** per l'oggetto. Per creare o modificare un report, è necessario che un utente amministratore disponga dell'autorizzazione **Modifica report** per l'oggetto.

### <a name="create-and-modify-reports"></a>Creare e modificare report

Per i report basati su Reporting Services, Configuration Manager usa Generatore report di Microsoft SQL Server come strumento esclusivo di creazione e modifica per i report basati su modello e per quelli basati su SQL. Quando si crea o si modifica un report nella console di Configuration Manager, viene aperto Generatore report. Per altre informazioni, vedere [Operazioni e manutenzione per la creazione di report](operations-and-maintenance-for-reporting.md).

A partire dalla versione 2002, per creare o modificare report di Power BI la console si integra con Power BI Desktop. Per altre informazioni, vedere [Creare report di Power BI](powerbi-report-server.md#create-power-bi-reports).

### <a name="run-reports"></a>Esecuzione di report

Quando si esegue un report basato su Reporting Services nella console di Configuration Manager, il Visualizzatore report si apre e si connette a Reporting Services. Dopo aver specificato tutti i parametri di report richiesti, Reporting Services recupera i dati e visualizza i risultati nel Visualizzatore. È possibile inoltre connettersi a SQL Services Reporting Services, connettersi all'origine dati per il sito ed eseguire i report.

A partire dalla versione 2002, quando si esegue un report basato su Power BI, viene aperto nel Web browser.

### <a name="report-prompts"></a>Richieste di report

Quando si crea o si modifica un report, è possibile configurare una richiesta di report o un parametro di report. Creare richieste di report per limitare o assegnare i dati che recupera un report. Un report può contenere più di una richiesta. Assicurarsi che i nomi richiesta siano univoci e contengano solo caratteri alfanumerici conformi alle regole di SQL Server per gli identificatori.

Quando si esegue un report, la richiesta richiede un valore per un parametro obbligatorio. In base al valore, recupera i dati del report. Ad esempio, il report **Informazioni computer per un computer specifico** richiede un nome computer. Reporting Services passa il valore specificato a una variabile definita nell'istruzione SQL del report.

### <a name="report-links"></a>Collegamenti per il report

I collegamenti al report in Configuration Manager vengono usati in un report di origine per fornire un accesso semplice a dati aggiuntivi. È ad esempio possibile creare collegamenti a informazioni più dettagliate su ciascuno degli elementi del report di origine. Se il report di destinazione richiede uno o più richieste da eseguire, il report di origine deve contenere una colonna con i valori appropriati per ciascuna richiesta.

Il collegamento deve specificare il numero della colonna con il valore per la richiesta. Ad esempio:

- È disponibile un report che elenca i computer individuati di recente dal sito.
- È possibile collegarlo a un altro report che elenca gli ultimi messaggi ricevuti dal sito per un computer specifico.
- Si crea il collegamento e si specifica che la colonna `2` nel report di origine contiene il nome del computer. Questo valore è una richiesta obbligatoria per il report di destinazione.
- Si esegue il report di origine e a sinistra di ogni riga di dati compare un'icona di collegamento.
- Selezionando l'icona in una riga, il Visualizzatore report passa il valore nella colonna specificata per tale riga come valore di richiesta per il report di destinazione.

È possibile configurare un solo collegamento per un report, che collega a un singolo report di destinazione.

> [!WARNING]  
> Se si sposta un report di destinazione in una cartella report diversa, cambia il percorso del report di destinazione. Configuration Manager non aggiorna automaticamente il collegamento del report nel report di origine con il nuovo percorso e il collegamento non funzionerà nel report di origine.

## <a name="report-folders"></a>Cartelle report

Le cartelle report costituiscono un metodo per ordinare e filtrare i report che Configuration Manager archivia in Reporting Services. Le cartelle report sono utili quando si devono gestire numerosi report. Quando si installa un punto di Reporting Services, i report vengono copiati in Reporting Services e organizzati in più di 50 cartelle report. Le cartelle report sono di sola lettura. Non è possibile modificarle nella console di Configuration Manager.

## <a name="report-subscriptions"></a>Sottoscrizioni report

Una sottoscrizione report in Reporting Services è una richiesta ricorrente per recapitare un report a un orario specifico o in risposta a un evento. Nella sottoscrizione si specifica un formato di file dell'applicazione. Le sottoscrizione forniscono un'alternativa all'esecuzione di un report su richiesta. La creazione di report su richiesta richiede la selezione attiva del report ogni volta che si desidera visualizzare il report. Al contrario, le sottoscrizioni possono essere utilizzate per pianificare e quindi automatizzare il recapito di un report.

È possibile gestire le sottoscrizioni report nella console di Configuration Manager. Il server di report elabora le sottoscrizioni. Le distribuisce usando le estensioni per il recapito distribuite nel server. Per impostazione predefinita, è possibile creare sottoscrizioni che inviano report a una cartella condivisa o a un indirizzo di posta elettronica.

Per altre informazioni, vedere [Gestire le sottoscrizioni report](operations-and-maintenance-for-reporting.md#bkmk_subscription).

## <a name="report-builder"></a>Generatore report

Configuration Manager usa Generatore report di Microsoft SQL Server Reporting Services come strumento esclusivo di creazione e modifica per i report basati su modello e per quelli basati su SQL. Quando si crea o si modifica un report nella console di Configuration Manager, viene aperto Generatore report. Generatore report viene installato automaticamente quando si crea o si modifica un report per la prima volta. Quando si eseguono o modificano report viene aperta la versione di Generatore report associata alla versione installata di SQL Server.  

 L'installazione di Generatore report aggiunge il supporto per più di 20 lingue. Quando si esegue Generatore report, i dati vengono visualizzati nella lingua del sistema operativo del computer locale. Se Generatore report non supporta la lingua, visualizza i dati in inglese. Generatore report supporta tutte le funzionalità di SQL Server Reporting Services, tra cui:

- Offre un ambiente di creazione report intuitivo con un aspetto simile a Microsoft 365 Apps.  

- Offre il flessibile layout di report di SQL Server Report Definition Language (RDL).  

- Offre vari moduli di visualizzazione dei dati, compresi grafici e indicatori.  

- Fornisce caselle di testo con formattazione completa.  

- Effettua l'esportazione in formato Microsoft Word.  

È anche possibile aprire Generatore report direttamente da SQL Server Reporting Services.

## <a name="report-models-in-sql-server-reporting-services"></a>Modelli di report in SQL Server Reporting Services

SQL Reporting Services usa modelli di report per consentire agli utenti di selezionare dal database di Configuration Manager elementi da includere nei report basati su modello. Quando si crea un report, i modelli di report mostrano solo viste ed elementi specifici da selezionare. Per creare report basati su modello, deve essere disponibile almeno un modello.

I modelli di report dispongono delle seguenti funzionalità:

- Consentono di assegnare nomi aziendali logici a campi e viste del database. In questo modo, non è necessario conoscere la struttura del database di Configuration Manager per produrre report.

- Consente di raggruppare logicamente gli elementi.  

- Consente di definire relazioni tra elementi.  

- Consente di proteggere gli elementi del modello in modo che gli utenti amministratori possano vedere solo i dati che sono autorizzati a vedere.

Nonostante Configuration Manager fornisca modelli di report campione, è anche possibile definire modelli di report per soddisfare i requisiti della propria azienda. Per altre informazioni su come creare modelli di report, vedere [Creare modelli di report personalizzati](creating-custom-report-models-in-sql-server-reporting-services.md).

## <a name="next-steps"></a>Passaggi successivi

[Pianificare la creazione di report](planning-for-reporting.md)