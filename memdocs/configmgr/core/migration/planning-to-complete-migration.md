---
title: Completare la migrazione
titleSuffix: Configuration Manager
description: Informazioni su come completare la migrazione a una gerarchia di destinazione di Configuration Manager Current Branch dopo che una gerarchia di origine non contiene più dati.
ms.date: 01/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f4854b50-2e8c-414c-a872-9579554dca98
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 76cf6b57a4bc1439f2aa9c2e0484271987f85748
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693409"
---
# <a name="plan-to-complete-migration-in-configuration-manager"></a>Pianificare il completamento della migrazione in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Con Configuration Manager è possibile completare il processo di migrazione quando una gerarchia di origine non contiene più dati per la migrazione alla gerarchia di destinazione. Il completamento della migrazione include i passaggi generali seguenti:  

-   Assicurarsi che sia stata eseguita la migrazione dei dati necessari. Prima di completare la migrazione dalla gerarchia di origine, assicurarsi che tutte le risorse richieste siano state migrate correttamente alla gerarchia di destinazione. Tra le risorse sono inclusi dati e client.  

-   Interrompere la raccolta di dati dai siti di origine. Per completare la migrazione da una gerarchia di origine, è necessario prima interrompere la raccolta di dati dai siti di origine.  

-   Pulire i dati di migrazione. Dopo aver interrotto la raccolta di dati da tutti i siti di origine in una gerarchia di origine, è possibile rimuovere i dati sul processo di migrazione e sulla gerarchia di origine dal database della gerarchia di destinazione.  

-   Rimuovere le autorizzazioni della gerarchia di origine. Dopo aver completato la migrazione da una gerarchia di origine e quando la gerarchia non contiene più le risorse gestite, è possibile rimuovere le autorizzazioni dei siti nella gerarchia di origine e la relativa infrastruttura dall'ambiente. Per informazioni sulla rimozione delle autorizzazioni dai siti e dalle gerarchie di origine, vedere la documentazione della relativa versione di Configuration Manager.  

Usare le sezioni seguenti per pianificare il completamento della migrazione da una gerarchia di origine arrestando la raccolta dati e pulendo i dati di migrazione:  

-   [Pianificare l'arresto della raccolta dati](#Plan_to_Stop_Data_Gath)  

-   [Pianificare la pulizia dei dati di migrazione](#Plan_to_clean_up)  

##  <a name="plan-to-stop-gathering-data"></a><a name="Plan_to_Stop_Data_Gath"></a> Pianificare l'arresto della raccolta dati  
 Prima di completare la migrazione ed eseguire la pulizia dei dati di migrazione, è necessario interrompere la raccolta dei dati da ciascun sito di origine nella gerarchia di origine. Per interrompere la raccolta dati da ciascun sito di origine, è necessario eseguire il comando **Interrompi raccolta dati** sui siti di origine di livello inferiore, quindi ripetere il processo su ciascun sito padre. L'interruzione della raccolta dati nel sito principale della gerarchia di origine deve rappresentare l'ultimo passaggio. È necessario interrompere la raccolta dati in ogni sito figlio prima di eseguire questo comando su un sito padre. In genere, si interrompe la raccolta dati solo quando si è pronti a completare il processo di migrazione.  

 Dopo aver interrotto la raccolta dati da un sito di origine, i punti di distribuzione condivisi da quel sito non sono più disponibili come percorsi del contenuto per i client nella gerarchia di destinazione. Pertanto, assicurarsi che qualsiasi contenuto migrato, per cui i client nella gerarchia di destinazione richiedono l'accesso, rimanga disponibile tramite una delle seguenti opzioni:  

-   Nella gerarchia di destinazione, distribuire il contenuto almeno a un punto di distribuzione.  

-   Prima di interrompere la raccolta dei dati da un sito di origine, aggiornare o riassegnare i punti di distribuzione condivisi con il contenuto richiesto. Per altre informazioni sull'aggiornamento o sulla riassegnazione dei punti di distribuzione condivisi, vedere le sezioni applicabili in [Pianificazione di una strategia di migrazione per la distribuzione del contenuto](../../core/migration/planning-a-content-deployment-migration-strategy.md).  

Dopo aver interrotto la raccolta dati da ogni sito di origine nella gerarchia di origine, è possibile pulire i dati di migrazione. Fino a quando non viene completata la pulizia dei dati di migrazione, ogni processo di migrazione eseguito o pianificato rimane accessibile nella console di Configuration Manager.  

Per altre informazioni sui siti di origine e sulla raccolta dati, vedere [Pianificazione di una strategia per la gerarchia di origine](../../core/migration/planning-a-source-hierarchy-strategy.md).  

##  <a name="plan-to-clean-up-migration-data"></a><a name="Plan_to_clean_up"></a> Pianificare la pulizia dei dati di migrazione  
 L'ultimo passaggio necessario per completare la migrazione consiste nella pulizia dei dati di migrazione. È possibile utilizzare il comando **Pulisci dati migrazione** dopo aver interrotto la raccolta dei dati per ogni sito di origine nella gerarchia di origine. Questa azione facoltativa determina la rimozione dei dati sulla gerarchia di origine corrente dal database della gerarchia di destinazione.  

 Durante la pulizia, la maggior parte dei dati sulla migrazione viene rimossa dal database della gerarchia di destinazione. Tuttavia, vengono conservati i dettagli sugli oggetti migrati. Con questi dettagli è possibile usare l'area di lavoro **Migrazione** per riconfigurare la gerarchia di origine che contiene i dati di cui è stata eseguita la migrazione per riprendere la migrazione dalla gerarchia di origine o rivedere gli oggetti e la proprietà sito degli oggetti di cui prima è stata eseguita la migrazione.  
