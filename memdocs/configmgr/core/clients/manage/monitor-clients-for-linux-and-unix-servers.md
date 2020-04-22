---
title: Monitorare i client Linux/UNIX
titleSuffix: Configuration Manager
description: Monitorare i client in server Linux e UNIX in Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d827cf91-b18f-4ee7-b538-24ba6f003ab9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d2ea3a0b630e1710aeaf74a4349f202806d45039
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696769"
---
# <a name="how-to-monitor-clients-for-linux-and-unix-servers-in-configuration-manager"></a>Come monitorare i client per i server Linux e UNIX in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

> [!Important]  
> A partire dalla versione 1902, Configuration Manager non supporta i client Linux o UNIX. 
> 
> Per la gestione dei server Linux, è possibile usare la gestione di Microsoft Azure. Le soluzioni di Azure includono un ampio supporto per Linux che nella maggior parte dei casi supera le funzionalità di Configuration Manager, inclusa la gestione end-to-end delle patch per Linux.

È possibile visualizzare le informazioni dei server Linux e UNIX nella console di Configuration Manager usando gli stessi metodi usati per visualizzare le informazioni dei client basati su Windows.  

 Le informazioni che è possibile visualizzare includono:  

- Dettagli sullo stato dei client, nei dashboard della console di Configuration Manager  

- Dettagli sui client nei report di Configuration Manager predefiniti  

- Dettagli sull'inventario in Esplora inventario risorse  

  Le sezioni seguenti descrivono come ottenere queste informazioni dettagliate da Esplora inventario risorse e dai report.  

##  <a name="use-resource-explorer-to-view-inventory-for-linux-and-unix-servers"></a><a name="BKMK_UseResourceExpforLnU"></a> Usare Esplora inventario risorse per visualizzare l'inventario per i server Linux e UNIX  

 Dopo che un client di Configuration Manager invia l'inventario hardware al sito di Configuration Manager, è possibile usare Esplora inventario risorse per visualizzare queste informazioni. Il client di Configuration Manager per Linux e UNIX non aggiunge nuove classi o visualizzazioni per l'inventario in Esplora inventario risorse. I dati di inventario di Linux e UNIX sono mappati a classi WMI esistenti. È possibile visualizzare i dettagli sull'inventario per i server Linux e UNIX nelle classificazioni basate su Windows usando Esplora inventario risorse.  

 Ad esempio, è possibile raccogliere l'elenco di tutti i programmi installati in modo nativo presenti nei server Linux e UNIX. Esempi di programmi installati in modo nativo includono **.rpms** in Linux o **.pkgs** in Solaris. Dopo che un inventario è stato inviato da un client Linux o UNIX, è possibile visualizzare l'elenco di tutti i programmi Linux o UNIX installati in modo nativo in Esplora inventario risorse nella console di Configuration Manager.  

 Per informazioni su come usare Esplora inventario risorse, vedere [Come usare Esplora inventario risorse per visualizzare l'inventario hardware](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md).  

##  <a name="how-to-use-reports-to-view-information-for-linux-and-unix-servers"></a><a name="BKMK_UseReportsforLnU"></a> Come usare i report per visualizzare informazioni per i server Linux e UNIX  
 I report per Configuration Manager includono informazioni dei server Linux e UNIX, insieme a informazioni dei computer basati su Windows. Non sono necessarie configurazioni aggiuntive per integrare i dati di Linux e UNIX nei report.  

 Ad esempio, se si esegue il report relativo al numero di versioni del sistema operativo, vengono visualizzati l'elenco dei diversi sistemi operativi e il numero dei client che eseguono ogni sistema operativo. Il report è basato sulle informazioni dell'inventario hardware inviate dai diversi client di Configuration Manager che eseguono sistemi operativi diversi.  

 È anche possibile creare report personalizzati specifici dei dati dei server Linux e UNIX. La proprietà **Didascalia** della classe di inventario hardware **Sistema operativo** è un attributo utile che è possibile usare per identificare sistemi operativi specifici nella query del report.  

 Per informazioni sui report in Configuration Manager, vedere [Introduzione ai report](../../servers/manage/introduction-to-reporting.md).  
