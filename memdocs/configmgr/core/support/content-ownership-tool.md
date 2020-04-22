---
title: Content Ownership Tool
titleSuffix: Configuration Manager
description: Usare Content Ownership Tool per modificare la proprietà dei pacchetti orfani in Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 753d2681-ea72-4f47-94d1-ac10188d9d5b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ee1a24a93bb71178af3a4cfbba2a406bdd958d19
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707849"
---
# <a name="content-ownership-tool"></a>Content Ownership Tool

*Si applica a: Configuration Manager (Current Branch)*

Content Ownership Tool è uno [strumento di Configuration Manager](tools.md). Modifica la proprietà dei pacchetti orfani in Configuration Manager. I pacchetti orfani non dispongono di un server del sito proprietario. I pacchetti possono diventare orfani rimuovendo il server del sito, mentre appartengono ancora al server di questo sito.

Eseguire Content Ownership Tool su qualsiasi server del sito nella gerarchia di Configuration Manager. Accedere come utente amministratore con autorizzazioni di pacchetto sufficienti.  

> [!Tip]  
> Usare **ContentLibraryCleanup.exe** in `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` per *rimuovere* contenuto orfano da un punto di distribuzione. Per altre informazioni, vedere [Strumento di pulizia della raccolta contenuto](../plan-design/hierarchy/content-library-cleanup-tool.md).  



## <a name="features"></a>Caratteristiche

- Visualizzare tutti i pacchetti orfani  

- Visualizzare tutti i pacchetti, anche se non sono orfani  

- Visualizzare lo stato della connessione a un sito  

- Filtrare i pacchetti per nome, codice del sito o tipo di pacchetto  

- Ordinare per qualsiasi colonna visualizzata  

- Modificare l'assegnazione di uno o più pacchetti con una singola azione  

- Visualizzare lo stato dell'attività di trasferimento della proprietà  



## <a name="usage"></a>Utilizzo

Eseguire **ContentOwnershipTool.exe** per avviare lo strumento. Per eseguire lo strumento non sono necessarie autorizzazioni di amministratore locale nel computer.

Parametri della riga di comando assenti.

> [!Important]   
> Questo strumento modifica la proprietà di un pacchetto orfano. Il pacchetto stesso non viene spostato dal punto di distribuzione in cui è archiviato. Questa modifica della proprietà non produce l'aggiornamento del pacchetto nei punti di distribuzione. Inoltre, non produce la rivalutazione da parte dei client dei criteri per la distribuzione del pacchetto. Dopo la modifica della proprietà, assicurarsi che il nuovo server del sito possa accedere ai file di origine. Deve avere almeno le autorizzazioni di **lettura** ai file di origine di ogni pacchetto. 



## <a name="see-also"></a>Vedere anche

- [Concetti di base sulla gestione dei contenuti](../plan-design/hierarchy/fundamental-concepts-for-content-management.md)
- [Raccolta contenuto](../plan-design/hierarchy/the-content-library.md)
