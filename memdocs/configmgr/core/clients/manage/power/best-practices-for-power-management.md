---
title: Suggerimenti per il risparmio energia
titleSuffix: Configuration Manager
description: Informazioni sulle raccomandazioni Microsoft per il risparmio energia in Configuration Manager.
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 9f7142e1-c972-4384-853b-2da1568cb3e3
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 02cfb32f9187ca5a0ae0ad70ffcb4b85db8afb1b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696629"
---
# <a name="recommendations-for-power-management-in-configuration-manager"></a>Raccomandazioni per il risparmio energia in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Seguire le raccomandazioni seguenti per il risparmio energia in Configuration Manager.  

## <a name="monitor-at-a-representative-time"></a>Eseguire il monitoraggio in un momento rappresentativo

La fase di monitoraggio del risparmio energia fornisce le informazioni seguenti dai computer dell'organizzazione:

- Consumo di energia elettrica
- Attività
- Capacità di risparmio energia
- Impatto ambientale

Scegliere un orario rappresentativo per il monitoraggio dei dispositivi. Ad esempio, eseguire il monitoraggio durante un giorno festivo non genera un report realistico del consumo energetico dei computer.

## <a name="create-a-control-collection"></a>Creare una raccolta di controllo

Creare due raccolte di computer per semplificare il monitoraggio degli effetti dell'applicazione delle combinazioni per il risparmio di energia ai computer. La prima raccolta deve contenere la maggior parte dei computer a cui si vogliono applicare le impostazioni di risparmio energia. La *raccolta di controllo* deve contenere i computer rimanenti. Applicare la combinazione di risparmio energia richiesta alla prima raccolta. Eseguire quindi i report per confrontare l'effetto tra le due raccolte.  

## <a name="run-reports-before-you-apply-a-plan"></a>Eseguire i report prima di applicare un piano

Prima di applicare una combinazione per il risparmio di energia a una raccolta di computer, eseguire il report **Impostazioni risparmio energia**. Usare questo report per esaminare le impostazioni di risparmio energia già configurate nei computer della raccolta. Se si applicano nuove impostazioni di risparmio energia ai computer senza prima esaminare le impostazioni esistenti, ciò potrebbe causare un aumento del consumo di energia.  

## <a name="exclude-servers"></a>Escludere i server

Il risparmio energia per i computer che eseguono Windows Server non è supportato. Aggiungere i server a una raccolta ed escluderla dal risparmio energia.  

> [!NOTE]
> Anche se Configuration Manager non supporta la gestione del risparmio energia di Windows Server, raccoglie comunque i dati sull'utilizzo di energia per analisi e report.

## <a name="exclude-other-computers"></a>Escludere altri computer

In presenza di computer che non si vuole gestire con il risparmio energia, aggiungerli a una raccolta di esclusioni.  

Potrebbe essere utile, ad esempio, escludere i tipi di computer seguenti dal risparmio energia:

- Computer che devono rimanere accesi.  

- Computer a cui gli utenti devono connettersi in remoto.  

- Computer che non possono usare il risparmio energia.  

- Computer con il ruolo del sistema del sito del punto di distribuzione.  

- Computer pubblici, ad esempio chioschi multimediali, display informativi o console di monitoraggio, in cui il computer e il monitor devono essere sempre accesi.  

Per altre informazioni, vedere [Configurare il risparmio energia](configuring-power-management.md).  

## <a name="apply-power-plans-to-a-test-collection"></a>Applicare combinazioni per il risparmio di energia a una raccolta di test

Analizzare sempre l'effetto dell'applicazione della combinazione per il risparmio di energia a una raccolta di test di computer prima di applicare tale combinazione a una raccolta più grande di computer.  

Quando si esclude un computer dal risparmio energia, per tutte le impostazioni di risparmio energia vengono ripristinati i valori originali. Non è possibile ripristinare i valori originali per singole impostazioni di risparmio energia.  

## <a name="apply-power-plan-settings-individually"></a>Applicare le impostazioni della combinazione per il risparmio di energia singolarmente

Monitorare l'effetto dell'applicazione di ogni impostazione di risparmio energia prima di applicare quella successiva. Questo processo assicura che ogni impostazione abbia l'effetto richiesto. Per altre informazioni sulle impostazioni della combinazione per il risparmio di energia, vedere [Impostazioni disponibili per le combinazioni per il risparmio di energia](create-and-apply-power-plans.md#BKMK_Plans).  

## <a name="regularly-monitor-computers-for-multiple-power-plans"></a>Monitorare regolarmente i computer con più combinazioni per il risparmio di energia

La funzionalità di risparmio energia include un report che visualizza i computer a cui sono applicate più combinazioni per il risparmio di energia: **Computer con più combinazioni per il risparmio di energia**.

Se un computer è un membro di più raccolte, ognuna delle quali applica combinazioni per il risparmio di energia diverse, i comportamenti sono i seguenti:  

- **Combinazione per il risparmio di energia**: se si applicano più valori per le impostazioni di risparmio energia a un computer, viene usato il valore meno restrittivo.  

- **Ora riattivazione:** se si applicano più ore di riattivazione a un computer desktop, viene usata l'ora più prossima alla mezzanotte.  

Per altre informazioni, vedere [Computer con più combinazioni per il risparmio di energia](monitor-and-plan-for-power-management.md#BKMK_Multiple).  

## <a name="save-or-export-power-management-information"></a>Salvare o esportare le informazioni relative al risparmio energia

Quando si eseguono i report durante le fasi di monitoraggio e conformità, salvare o esportare i risultati. Conservare i dati per confronti successivi, nel caso Configuration Manager rimuova i dati in seguito.  

Configuration Manager mantiene le informazioni sul risparmio energia seguenti nel database del sito:

- Informazioni sul risparmio energia usate dai report giornalieri: 31 giorni

- Informazioni sul risparmio energia usate dai report mensili: 13 mesi
