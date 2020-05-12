---
title: Percorsi personalizzati dei file di database
titleSuffix: Configuration Manager
description: Di seguito viene spiegato come specificare percorsi personalizzati per i file di database di SQL Server.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 500a9aa6-68aa-44eb-bf49-350c1314a697
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d3f01e54ba196ee9c27295d8f970a7dbe352f63f
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906183"
---
# <a name="custom-locations-for-configuration-manager-site-database-files"></a>Percorsi personalizzati per i file di database del sito di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

 Configuration Manager supporta percorsi personalizzati per i file di database di SQL Server.  

> [!NOTE]  
>  L'opzione per specificare percorsi file non predefiniti non è disponibile quando si usa un cluster SQL Server.  

 **Durante l'installazione** di un nuovo sito primario o di un sito di amministrazione centrale, è possibile:  

-   **Specificare percorsi dei file non predefiniti per il database del sito**: l'installazione di Configuration Manager crea quindi il database del sito usando tali percorsi.  

-   **Specificare l'uso di un database SQL Server creato in precedenza che usa percorsi dei file personalizzati**:  l'installazione di Configuration Manager usa quindi tale database creato in precedenza e i relativi percorsi di file preconfigurati.  

**Al termine dell'installazione**, è possibile modificare il percorso dei file di database del sito. A questo scopo, è necessario arrestare il sito e modificare il percorso file in SQL Server:  

-   Nel server del sito di Configuration Manager interrompere il servizio **SMS_Executive**.  

-   Per altre informazioni su come spostare un database utente, vedere [Spostare i database utente](https://docs.microsoft.com/sql/relational-databases/databases/move-user-databases?view=sql-server-2014).  

-   Al termine dello spostamento dei file di database, è necessario riavviare il servizio **SMS_Executive** sul server del sito di Configuration Manager.  
