---
title: Pianificare la migrazione
titleSuffix: Configuration Manager
description: Informazioni su siti e gerarchie prima di eseguire la migrazione di dati in una gerarchia di destinazione di Configuration Manager.
ms.date: 01/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b2bf493e-1e10-496f-a139-2646522703ed
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b514e2bb0843801cfa6f0f307af8a5013fc3f9e6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702829"
---
# <a name="plan-for-migration-to-configuration-manager-current-branch"></a>Pianificare la migrazione a Configuration Manager Current Branch

*Si applica a: Configuration Manager (Current Branch)*

Prima di eseguire la migrazione dei dati in una gerarchia di destinazione di Configuration Manager Current Branch, è importante avere una certa familiarità con i siti e le gerarchie in Configuration Manager. Per altre informazioni su siti e gerarchie, vedere [Nozioni fondamentali di Configuration Manager](../../core/understand/fundamentals.md).  

Installare una gerarchia di Configuration Manager Current Branch come gerarchia di destinazione, prima di eseguire la migrazione di dati da una gerarchia di origine supportata.  

Dopo l'installazione della gerarchia di destinazione, configurare le funzionalità e le funzioni di gestione che si vuole usare nella gerarchia di destinazione prima di avviare la migrazione dei dati.  

Potrebbe inoltre essere necessario pianificare la sovrapposizione tra la gerarchia di origine e la gerarchia di destinazione. È possibile, ad esempio, configurare la gerarchia di origine per l'uso degli stessi limiti o percorsi di rete della gerarchia di destinazione e quindi installare nuovi client nella gerarchia di destinazione e usare l'assegnazione sito automatica. In questo scenario, dal momento che un client Configuration Manager appena installato può selezionare un sito di qualsiasi gerarchia, potrebbe verificarsi un'assegnazione errata alla gerarchia di origine. Pianificare quindi l'assegnazione di ogni nuovo client nella gerarchia di destinazione a un sito specifico di tale gerarchia e non usare l'assegnazione sito automatica.  

Per altre informazioni sulle assegnazioni del sito, vedere [Considerazioni sull'assegnazione sito dei client](../../core/plan-design/hierarchy/interoperability-between-different-versions.md#BKMK_SupConfigSiteAssignment) in [Interoperabilità tra versioni diverse di Configuration Manager](../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  

Usare gli articoli seguenti per pianificare la migrazione di una gerarchia di origine supportata in una gerarchia di destinazione di Configuration Manager:

-   [Prerequisiti per la migrazione](../../core/migration/prerequisites-for-migration.md)  

-   [Elenchi di controllo per gli amministratori per la pianificazione della migrazione](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [Determinare se eseguire la migrazione dei dati a Configuration Manager Current Branch](../../core/migration/determine-whether-to-migrate-data.md)  

-   [Pianificare una strategia per la gerarchia di origine](../../core/migration/planning-a-source-hierarchy-strategy.md)  

-   [Elenchi di controllo per gli amministratori per la pianificazione della migrazione](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [Pianificare una strategia di migrazione client](../../core/migration/planning-a-client-migration-strategy.md)  

-   [Pianificare una strategia di migrazione per la distribuzione del contenuto](../../core/migration/planning-a-content-deployment-migration-strategy.md)  

-   [Pianificare la migrazione degli oggetti di Configuration Manager a Configuration Manager Current Branch](../../core/migration/planning-for-the-migration-of-objects.md)  

-   [Pianificare il monitoraggio dell'attività di migrazione](../../core/migration/planning-to-monitor-migration-activity.md)  

-   [Pianificare il completamento della migrazione](../../core/migration/planning-to-complete-migration.md)  
