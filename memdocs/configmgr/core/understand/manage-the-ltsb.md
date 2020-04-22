---
title: Gestire LTSB
titleSuffix: Configuration Manager
description: Differenze di gestione per LTSB di System Center Configuration Manager.
ms.date: 05/01/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8da2887a-fd8e-438c-b926-849c121f7fdf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 86e7579832a5a59c3609d24744eb646e1a4c1fd1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706869"
---
# <a name="manage-the-long-term-servicing-branch-of-configuration-manager"></a>Gestire Long Term Servicing Branch di Configuration Manager

*Si applica a: System Center Configuration Manager (Long-Term Servicing Branch)*

Quando si usa Long-Term Servicing Branch (LTSB) di System Center Configuration Manager, le informazioni riportate di seguito consentono di comprendere modifiche importanti che influiscono sulla modalità di gestione dell'infrastruttura.

Poiché LTSB è equivalente a Current Branch versione 1606 con alcune eccezioni, ad esempio l'integrazione di Intune e le funzionalità correlate al cloud, le attività usate per la pianificazione, la distribuzione, la configurazione e la gestione quotidiana sono per la maggior parte identiche.

LTSB, ad esempio, supporta lo stesso numero di siti, tipi di sito e client, nonché la stessa infrastruttura generale di Current Branch. È quindi possibile usare le indicazioni disponibili negli argomenti relativi alla pianificazione e alla progettazione dei siti e delle gerarchie per Current Branch. Analogamente, per le funzionalità con LTSB supportate da entrambi i rami, ad esempio gli aggiornamenti software o la distribuzione del sistema operativo, è possibile usare le indicazioni disponibili nelle sezioni corrispondenti della documentazione di Current Branch, tenendo presente che non sono illustrate le modifiche alle funzionalità introdotte dopo la versione 1606 di Current Branch.

Le sezioni seguenti offrono informazioni sulle attività di gestione che presentano delle differenze.

## <a name="updates-and-servicing"></a>Aggiornamenti e manutenzione
Solo gli aggiornamenti di sicurezza critici vengono resi disponibili come aggiornamenti nella console per LTSB.  

Le informazioni sugli aggiornamenti periodici per versioni di Current Branch successive sono visibili nella console, ma questi non vengono resi disponibili per LTSB. Non vengono scaricati e non possono essere installati.

Per supportare gli aggiornamenti di sicurezza critici all'interno della console, per i siti LTSB è necessario usare il [punto di connessione del servizio](../servers/deploy/configure/about-the-service-connection-point.md). È possibile configurare questo ruolo del sistema del sito in modalità offline o online, come avviene per Current Branch. LTSB raccoglie e invia gli stessi dati di telemetria e di utilizzo di Current Branch.

LTSB supporta l'uso del programma di installazione degli aggiornamenti rapidi e dello strumento di registrazione dell'aggiornamento, come documentato per Current Branch.

Per informazioni generali sugli aggiornamenti e sulla manutenzione, vedere [Updates for Configuration Manager](../servers/manage/updates.md) (Aggiornamenti per Configuration Manager).


## <a name="changes-for-site-expansion-and-the-cdlatest-folder"></a>Modifiche per l'espansione del sito e cartella CD.Latest
Quando si esegue LTSB e si espande un sito primario autonomo installando un nuovo sito di amministrazione centrale, è necessario usare il programma di installazione e i file di origine dal supporto di base della versione 1606. Per Current Branch si esegue il programma di installazione e si usano i file di origine della cartella CD.Latest.

Anche se non si esegue il programma di installazione per l'espansione del sito dalla cartella CD.Latest, si continua a usare questa cartella per il ripristino del sito e per installare un nuovo sito primario figlio se il primo sito LTSB è un sito di amministrazione centrale.

Per altre informazioni sull'espansione del sito, vedere [Espandere un sito primario autonomo](../servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand). Per altre informazioni sulla cartella CD.Latest, vedere [The CD.Latest folder](../servers/manage/the-cd.latest-folder.md) (Cartella CD.Latest).


## <a name="recovery"></a>Ripristino
Quando si esegue il ripristino, per il sito o il database del sito è necessario ripristinare il ramo originario. Non è possibile ripristinare un database del sito Current Branch con un'installazione LTSB o viceversa.
