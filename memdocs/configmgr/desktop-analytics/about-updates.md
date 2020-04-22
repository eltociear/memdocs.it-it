---
title: Aggiornamenti in Desktop Analytics
titleSuffix: Configuration Manager
description: Informazioni sugli aggiornamenti della sicurezza e delle funzionalità in Desktop Analytics.
ms.date: 08/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 14ae894c-26fb-4fe3-b51d-e80700122df4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ec510414f11aa312e6c1a7d1d5bfa8126f473fe3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706579"
---
# <a name="updates-in-desktop-analytics"></a>Aggiornamenti in Desktop Analytics

Nel portale di Desktop Analytics visualizzare lo stato degli aggiornamenti della sicurezza e delle funzionalità. Selezionare questi nodi nel gruppo Monitoraggio del menu principale di Desktop Analytics. Questi nodi offrono informazioni dettagliate sullo stato di questi aggiornamenti nell'ambiente in uso.


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

Se un dispositivo Windows 10 *non è autenticato* con un account Microsoft, Windows non visualizza questi dati. Questa autenticazione viene in genere completata come parte della configurazione guidata dell'Installazione di Windows.<!-- 5148153 -->


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

Se un dispositivo Windows 10 *non è autenticato* con un account Microsoft, Windows non visualizza questi dati. Questa autenticazione viene in genere completata come parte della configurazione guidata dell'Installazione di Windows.<!-- 5148153 -->


## <a name="next-steps"></a>Passaggi successivi

- [Informazioni sugli asset di Desktop Analytics](about-assets.md): dispositivi, driver e app  

- [Informazioni sui piani di distribuzione](about-deployment-plans.md)  
