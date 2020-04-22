---
title: Dashboard del ciclo di vita del prodotto
titleSuffix: Configuration Manager
description: Visualizzare i criteri del ciclo di vita Microsoft con il dashboard del ciclo di vita del prodotto in Configuration Manager.
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8b5b144a-0e5f-4fcc-87b2-33b9bcdb5655
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 178331865c8f3efd660e4a0037674eed3621fe6b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695169"
---
# <a name="manage-microsoft-lifecycle-policy-with-configuration-manager"></a>Gestire i criteri del ciclo di vita Microsoft con Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

A partire dalla versione 1806 è possibile usare il dashboard del ciclo di vita del prodotto di Configuration Manager per visualizzare i criteri del ciclo di vita Microsoft. Il dashboard mostra lo stato dei criteri del ciclo di vita Microsoft per i prodotti Microsoft installati nei dispositivi gestiti con Configuration Manager. Fornisce informazioni sui prodotti Microsoft in uso nell'ambiente, sullo stato del supporto e sulle date di fine del supporto. Usare il dashboard per conoscere la disponibilità del supporto per ogni prodotto. Queste informazioni consentono anche di pianificare l'aggiornamento dei prodotti Microsoft in uso prima del raggiungimento della fine del supporto.  

Per altre informazioni, vedere [Criteri relativi al ciclo di vita Microsoft](https://support.microsoft.com/lifecycle).

A partire dalla versione 1810, il dashboard include le informazioni per System Center 2012 Configuration Manager e versioni successive.<!--1358702-->  



## <a name="prerequisites"></a>Prerequisiti 

 Per visualizzare i dati nel dashboard del ciclo di vita del prodotto, sono necessari i componenti seguenti:  

- Internet Explorer 9 o versione successiva deve essere installato nel computer che esegue la console di Configuration Manager.  

- È necessario che sia installato e configurato un ruolo del punto di connessione del servizio. Per ottenere gli aggiornamenti per i dati in questo dashboard, il punto di connessione del servizio deve essere online oppure deve essere sincronizzato regolarmente se è offline. Per altre informazioni, vedere [Informazioni sul punto di connessione del servizio](../../../servers/deploy/configure/about-the-service-connection-point.md).

- Un punto di Reporting Services è necessario per la funzionalità di collegamento ipertestuale nel dashboard. Il dashboard è collegato ai report di SQL Server Reporting Services (SSRS). Per altre informazioni, vedere [Introduzione ai report](../../../servers/manage/introduction-to-reporting.md).  

- Il punto di sincronizzazione di Asset Intelligence deve essere configurato e sincronizzato. Il dashboard usa il catalogo di Asset Intelligence come metadati per i titoli dei prodotti. I metadati vengono confrontati con i dati di inventario nella gerarchia. Per altre informazioni, vedere [Configurare Asset Intelligence in Configuration Manager](configuring-asset-intelligence.md).  
  - Se si sta configurando il punto di sincronizzazione di Asset Intelligence per la prima volta, assicurarsi di [abilitare le classi di inventario hardware di Asset Intelligence](configuring-asset-intelligence.md#BKMK_EnableAssetIntelligence). Il dashboard del ciclo di vita dipende da tali classi di inventario hardware di Asset Intelligence. Il dashboard non mostrerà dati fino a quando i client non saranno stati analizzati e non sarà stato restituito l'inventario hardware.  
  - Per visualizzare informazioni sugli aggiornamenti della sicurezza estesa nel dashboard, abilitare la classe di inventario hardware **Prodotto con gestione licenze software - Asset Intelligence (SoftwareLicensingProduct)** . Per altre informazioni, vedere [Abilitare le classi di report per l'inventario hardware di Asset Intelligence](configuring-asset-intelligence.md#BKMK_EnableAssetIntelligence). <!--4962901-->



## <a name="use-the-product-lifecycle-dashboard"></a>Usare il dashboard del ciclo di vita del prodotto

In base ai dati di inventario che il sito raccoglie dai dispositivi gestiti, il dashboard visualizza informazioni su tutti i prodotti correnti. Tuttavia le informazioni visualizzate per i sistemi operativi e SQL Server sono limitate alle versioni seguenti:

- Windows Server 2008 e versioni successive
- Windows XP e versioni successive
- SQL Server 2008 e versioni successive

Per accedere al dashboard del ciclo di vita, nella console di Configuration Manager scegliere l'area di lavoro **Asset e conformità**, espandere **Asset Intelligence** e selezionare il nodo **Ciclo di vita del prodotto**.

> [!NOTE]  
> I dati del dashboard sono basati sul sito a cui la console di Configuration Manager si connette. Se la console si connette al sito di livello superiore, vengono visualizzati i dati dell'intera gerarchia. Se si connette a un sito figlio primario, vengono visualizzati solo i dati di quel sito.

### <a name="product-lifecycle-dashboard"></a>Dashboard del ciclo di vita del prodotto

![Screenshot del dashboard del ciclo di vita del prodotto nella console](media/product-lifecycle-dashboard.png)

Modificare la visualizzazione selezionando una delle opzioni seguenti dall'elenco **Categoria prodotto**:  
- **Tutti**: visualizza contemporaneamente tutti i prodotti  
- **Client Windows**: visualizza le versioni del sistema operativo dei client Windows  
- **Windows Server**: visualizza le versioni del sistema operativo Windows Server  
- **Database**: visualizza le versioni di SQL Server  
- **Configuration Manager**: a partire dalla versione 1810, visualizza le versioni di Configuration Manager 
- **Microsoft Office**: a partire dalla versione 1902, visualizza informazioni sulle versioni installate da Office 2003 a Office 2016 <!--3556026-->

Il dashboard include i riquadri seguenti:  

- **Primi 5 prodotti che hanno superato la scadenza**: questo riquadro è una visualizzazione dati consolidata dei prodotti trovati nell'ambiente che hanno superato la scadenza. Il grafico mostra il software installato scaduto rispetto al ciclo di vita del supporto dei sistemi operativi e dei prodotti SQL Server.  

- **Primi 5 prodotti che si avvicinano alla scadenza**: questo riquadro è una visualizzazione dati consolidata dei prodotti trovati nell'ambiente la cui scadenza è prevista nei 18 mesi successivi. Il grafico mostra il software installato che scadrà entro 18 mesi rispetto al ciclo di vita del supporto dei sistemi operativi e dei prodotti SQL Server.  

- **Dati sul ciclo di vita per i prodotti installati**: questo riquadro offre un'idea generale della transizione di un prodotto dallo stato supportato allo stato scaduto. Il grafico presenta in dettaglio il numero di client in cui il prodotto è installato, lo stato di disponibilità del supporto e un collegamento ad altre informazioni sui passaggi successivi da eseguire. Nel grafico sono incluse le informazioni seguenti:     
    - Tempo rimanente per il supporto tecnico
    - Numero nell'ambiente 
    - Data di fine del supporto Mainstream
    - Data di fine del supporto " Extended"
    - Passaggi successivi  

> [!IMPORTANT]  
> Le informazioni visualizzate in questo dashboard vengono fornite per agevolare l'utente e sono destinate solo all'uso interno all'azienda. Non fare affidamento esclusivamente su queste informazioni per accertare la conformità del proprio ambiente. Verificare l'esattezza delle informazioni fornite e la disponibilità delle informazioni sul supporto visitando la pagina [Criteri relativi al ciclo di vita Microsoft](https://support.microsoft.com/lifecycle).  



## <a name="reporting"></a>Reporting

Sono disponibili anche report aggiuntivi. Nella console di Configuration Manager passare all'area di lavoro **Monitoraggio**, espandere **Report** e quindi espandere **Report**. I nuovi report seguenti sono stati aggiunti alla categoria **Asset Intelligence**:  

- **Ciclo di vita 01A - Computer con un prodotto software specifico**: Visualizza un elenco dei computer in cui viene rilevato un prodotto specificato.  

- **Ciclo di vita 02A - Elenco di computer con prodotti scaduti nell'organizzazione**: Visualizza i computer con prodotti scaduti. È possibile filtrare questo report in base al nome del prodotto.

- **Ciclo di vita 03A - Elenco di prodotti scaduti rilevati nell'organizzazione**: Visualizza i dettagli relativi ai prodotti trovati nell'ambiente con date del ciclo di vita scadute.  

- **Ciclo di vita 04A - Panoramica generale del ciclo di vita del prodotto**: Visualizza un elenco di cicli di vita dei prodotti. Filtrare l'elenco in base al nome del prodotto e ai giorni mancanti alla scadenza.  

- **Ciclo di vita 05A - Dashboard Ciclo di vita del prodotto**: A partire dalla versione 1810, questo report include informazioni simili a quelle del dashboard nella console. Selezionare una categoria per visualizzare il numero di prodotti presenti nel proprio ambiente e i giorni di supporto rimanenti.  

Per altre informazioni, vedere [Elenco dei report](../../../servers/manage/list-of-reports.md#asset-intelligence).<!--SCCMDocs issue 997-->  
