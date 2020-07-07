---
title: Aggiornamenti in Desktop Analytics
titleSuffix: Configuration Manager
description: Informazioni sugli aggiornamenti della sicurezza e delle funzionalità in Desktop Analytics.
ms.date: 04/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 14ae894c-26fb-4fe3-b51d-e80700122df4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 96a014f4919480854b57bae82e982ce783f5f59b
ms.sourcegitcommit: f3f2632df123cccd0e36b2eacaf096a447022b9d
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85590967"
---
# <a name="updates-in-desktop-analytics"></a>Aggiornamenti in Desktop Analytics

Nel portale di Desktop Analytics visualizzare lo stato degli aggiornamenti della sicurezza e delle funzionalità. Selezionare questi nodi nel gruppo Monitoraggio del menu principale di Desktop Analytics. Questi nodi offrono informazioni dettagliate sullo stato di questi aggiornamenti nell'ambiente in uso.

<!--7362999-->

> [!IMPORTANT]
> Desktop Analytics visualizza lo stato di aggiornamento della sicurezza e delle funzionalità per i dispositivi con l'ID commerciale associato all'area di lavoro di Desktop Analytics. Questo comportamento è indipendente dal fatto che i dispositivi siano stati registrati in Configuration Manager. Il numero di dispositivi totali in questi riquadri potrebbe non corrispondere al numero di dispositivi registrati in [**Servizi connessi**](monitor-connection-health.md#commercial-id-configuration).

## <a name="security-updates"></a>Aggiornamenti della sicurezza

Per verificare lo stato corrente degli aggiornamenti della sicurezza, selezionare **Aggiornamenti della sicurezza** nella sezione **Monitoraggio** di Desktop Analytics:

![Nodo Aggiornamenti della sicurezza di Desktop Analytics](media/security-updates.png)

Questa vista riepiloga gli aggiornamenti della *sicurezza* per i dispositivi che eseguono Windows 10. I dispositivi nel grafico a barre sono suddivisi in categorie in base alle etichette seguenti:

#### <a name="latest"></a>Più recente

I dispositivi eseguono l'aggiornamento della sicurezza più recente per la versione e il canale.

#### <a name="latest-1"></a>Più recente-1

I dispositivi eseguono un aggiornamento della sicurezza della versione precedente all'ultimo aggiornamento disponibile sul canale.

#### <a name="older"></a>Meno recente

I dispositivi eseguono un aggiornamento della sicurezza precedente alla versione Più recente-1.

#### <a name="not-measured"></a>Not measured (Non misurato)

Il dispositivo non è stato valutato da Desktop Analytics. Questo stato include i dispositivi che eseguono Windows 7, Windows 8.1 o Windows 10 registrati per il Programma Windows Insider.  

Per visualizzare le tendenze di adozione per gli aggiornamenti della sicurezza, selezionare **Visualizza altro** per una versione specifica di Windows. Il grafico ad area in pila categorizza i dispositivi in base all'aggiornamento della sicurezza installato nel tempo.

Per esaminare lo stato di distribuzione per gli aggiornamenti della sicurezza, selezionare **Visualizza tutto**. In questa visualizzazione i dispositivi sono elencati nelle categorie seguenti:

- Non avviato
- In corso
- Completed
- Richiede attenzione - Dispositivi (ordinati per nome dispositivo)
- Richiede attenzione - Problemi (ordinati per tipo di problema)

Per visualizzare i dispositivi con nuove informazioni che il servizio sta ancora elaborando, selezionare **Visualizza dati recenti**. Desktop Analytics visualizzerà queste informazioni dopo l'aggiornamento completo dei dati successivo.

  > [!IMPORTANT]
  > L'opzione di Desktop Analytics **Visualizza dati recenti** è deprecata. Questa azione verrà rimossa in una versione futura del servizio Desktop Analytics. Per altre informazioni, vedere [Funzionalità deprecate](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).<!--7080949-->  

## <a name="feature-updates"></a>Aggiornamenti delle funzionalità

Per verificare lo stato corrente degli aggiornamenti delle funzionalità, selezionare **Aggiornamenti delle funzionalità** nella sezione **Monitoraggio** di Desktop Analytics:

![Nodo Aggiornamenti delle funzionalità di Desktop Analytics](media/feature-updates.png)

Questa vista riepiloga gli aggiornamenti delle *funzionalità* per i dispositivi che eseguono Windows 10.

Per altre informazioni sui periodi di assistenza, vedere [Date importanti nel ciclo di vita di Windows](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet).  

I dispositivi nel grafico a barre sono suddivisi in categorie in base alle etichette seguenti:

#### <a name="in-service"></a>In servizio

I dispositivi eseguono l'aggiornamento delle funzionalità più recente per la versione e il canale.  

#### <a name="near-end-of-service"></a>Fine del servizio imminente

I dispositivi eseguono un aggiornamento delle funzionalità entro 90 giorni dalla fine del servizio.

#### <a name="end-of-service"></a>Fine del servizio

I dispositivi eseguono un aggiornamento delle funzionalità successivo alla data di fine del servizio. Queste date sono specifiche per le edizioni Enterprise ed Education di Windows. Non si applicano alle edizioni Home, Pro, Pro Education o Pro for Workstations. Per altre informazioni, vedere [Date importanti nel ciclo di vita di Windows](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet).

#### <a name="not-measured"></a>Not measured (Non misurato)

Il dispositivo non è stato valutato da Desktop Analytics. Questo stato include i dispositivi che eseguono Windows 7, Windows 8.1 o Windows 10 registrati per il Programma Windows Insider.

Selezionare il riquadro per visualizzare le tendenze di adozione per gli aggiornamenti delle funzionalità. Il grafico ad area in pila categorizza i dispositivi in base all'aggiornamento delle funzionalità installato nel tempo.

## <a name="next-steps"></a>Passaggi successivi

- [Informazioni sugli asset di Desktop Analytics](about-assets.md): dispositivi, driver e app  

- [Informazioni sui piani di distribuzione](about-deployment-plans.md)  
