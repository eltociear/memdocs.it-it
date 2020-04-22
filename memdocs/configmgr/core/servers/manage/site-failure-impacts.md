---
title: Impatto degli errori del sito
titleSuffix: Configuration Manager
description: Comprendere gli effetti dei diversi errori di un sito di Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6f0e08f8-f2e1-4823-90f6-7b1f4341eb46
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bf56aee2e9f73ea8c3c69737c749f2a599e1ac37
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708569"
---
# <a name="site-failure-impacts-in-configuration-manager"></a>Impatto degli errori del sito in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

È possibile che si verifichi un errore nel server del sito e in uno degli altri sistemi del sito e che quindi i servizi forniti normalmente non siano più disponibili. Se si installano più sistemi del sito sullo stesso computer e si verifica un errore in questo computer, tutti i servizi forniti con regolarità da questi sistemi del sito non sono più disponibili.

Il processo di pianificazione dovrebbe includere il riconoscimento dell'impatto sul servizio fornito all'organizzazione. Poiché ogni sistema del sito nel sito fornisce funzionalità diverse, l'impatto di un errore sul sito varia in base al ruolo del sistema in cui si è verificato. 

Usare le [opzioni di disponibilità elevata](../deploy/configure/high-availability-options.md) per attenuare l'errore di un singolo sistema. Pianificare e attuare anche una strategia di [backup e ripristino](backup-and-recovery.md) per ridurre il tempo in cui il servizio non è disponibile.

Le sezioni seguenti descrivono l'impatto generato quando il sistema del sito specificato non è operativo:


### <a name="site-server"></a>Server del sito

- Non è possibile alcuna amministrazione del sito. Non è possibile connettere la console al sito.  

- Il punto di gestione raccoglie le informazioni del client e le memorizza nella cache fino a quando il server del sito è di nuovo online.  

- Gli utenti possono eseguire le distribuzioni esistenti e i client possono scaricare il contenuto dai punti di distribuzione.  


### <a name="site-database"></a>Database del sito

- Non è possibile alcuna amministrazione del sito.  

- Se il client di Configuration Manager dispone già di un'assegnazione di criteri con nuovi criteri e se il punto di gestione ha memorizzato nella cache il corpo dei criteri, il client può effettuare una richiesta del corpo di criteri e ricevere la relativa risposta. Tuttavia, il sito non è in grado di soddisfare nuove richieste di assegnazione di criteri.  

- I client possono eseguire le distribuzioni solo se hanno già ricevuto i criteri e i file di origine associati sono già memorizzati nella cache in locale sul client.  


### <a name="management-point"></a>Punto di gestione

- Sebbene sia possibile creare nuove distribuzioni, i client non le ricevono finché un punto di gestione non è di nuovo online.  

- I client continuano a raccogliere le informazioni sull'inventario, la misurazione del software e lo stato. I dati vengono archiviati in locale fino a quando il punto di gestione è di nuovo disponibile.  

- I client possono eseguire le distribuzioni solo se hanno già ricevuto i criteri e i file di origine associati sono già memorizzati nella cache in locale sul client.  


### <a name="distribution-point"></a>Punto di distribuzione

- I client di Configuration Manager possono eseguire le distribuzioni, solo se i file di origine associati sono già stati scaricati in locale o sono disponibili in un'origine peer.

