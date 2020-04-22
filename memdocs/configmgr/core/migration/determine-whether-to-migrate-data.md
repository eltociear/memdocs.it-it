---
title: Scegliere di che cosa eseguire la migrazione
titleSuffix: Configuration Manager
description: Informazioni su quali dati possono e non possono essere migrati a Configuration Manager Current Branch.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 99222dc8-0e1e-4513-8302-7a1acf671e9b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4b697df41490d1709782561cc59b43684fb60d16
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701769"
---
# <a name="determine-whether-to-migrate-data-to-configuration-manager-current-branch"></a>Determinare se eseguire la migrazione dei dati a Configuration Manager Current Branch

*Si applica a: Configuration Manager (Current Branch)*

In Configuration Manager Current Branch la migrazione offre un processo per trasferire i dati e le configurazioni creati dalle versioni supportate di Configuration Manager alla nuova gerarchia.  È possibile usare questo processo per:  

-   Combinare più gerarchie in una.  

-   Spostare dati e configurazioni da una distribuzione lab alla distribuzione di produzione.

-   Spostare i dati e la configurazione da una versione precedente di Configuration Manager, ad esempio Configuration Manager 2007 che non dispone di alcun percorso di aggiornamento per Configuration Manager Current Branch, o da System Center 2012 Configuration Manager, che supporta un percorso di aggiornamento a Configuration Manager Current Branch.  

A eccezione del ruolo di sistema del sito del punto di distribuzione e dei computer che ospitano i punti di distribuzione, nessuna infrastruttura (compresi siti, ruoli di sistema del sito o computer che ospitano un ruolo di sistema del sito) può eseguire migrazioni, trasferimenti o essere condivisa tra le gerarchie.  

 Anche se non è possibile migrare l'infrastruttura del server, è possibile migrare i client di Configuration Manager da una gerarchia all'altra. La migrazione client comporta la migrazione dei dati utilizzati dai client da una gerarchia di origine a una gerarchia di destinazione e, quindi, l'installazione o la riassegnazione del software client in modo che il client relazioni alla nuova gerarchia.

Dopo l'installazione di un client nella nuova gerarchia e l'invio dei dati da parte del client, l'ID univoco di Configuration Manager consente a Configuration Manager di associare i dati precedentemente migrati a ogni computer client.  

 La funzionalità offerta dalla migrazione consente di gestire gli investimenti nelle configurazioni e nelle distribuzioni, nonché di usufruire pienamente delle principali modifiche apportate al prodotto introdotte per la prima volta in System Center 2012 Configuration Manager e proseguite in Configuration Manager. Queste modifiche comprendono una gerarchia di Configuration Manager semplificata che usa un numero inferiore di siti e risorse, nonché una migliore elaborazione grazie all'uso di codice nativo a 64 bit eseguito su hardware a 64 bit.  

 Per informazioni sulle versioni di Configuration Manager supportate dalla migrazione, vedere [Prerequisiti per la migrazione](../../core/migration/prerequisites-for-migration.md).  

## <a name="data-that-you-can-migrate-to-configuration-manager-current-branch"></a><a name="Can_Migrate"></a> Dati di cui è possibile eseguire la migrazione a Configuration Manager Current Branch

La migrazione può essere applicata alla maggior parte degli oggetti delle gerarchie di Configuration Manager supportate. Le istanze migrate di alcuni oggetti di una versione supportata di Configuration Manager 2007 devono essere modificate per essere conformi al formato oggetti e allo schema di System Center 2012 Configuration Manager.

Queste modifiche non interessano i dati contenuti nel database del sito di origine. Gli oggetti di cui viene eseguita la migrazione da una versione supportata di System Center 2012 Configuration Manager o Configuration Manager Current Branch non richiedono alcuna modifica.  

Di seguito sono elencati gli oggetti di cui è possibile eseguire la migrazione in base alla versione di Configuration Manager nella gerarchia di origine. Alcuni oggetti, ad esempio le query, non possono essere migrati. Per continuare a usare questi oggetti che non vengono migrati, è necessario ricrearli nella nuova gerarchia. Altri oggetti, tra cui alcuni dati client, vengono ricreati automaticamente nella nuova gerarchia durante la gestione dei client in tale gerarchia.  

### <a name="objects-that-you-can-migrate-from-system-center-2012-configuration-manager-or-configuration-manager-current-branch"></a>Oggetti di cui è possibile eseguire la migrazione da System Center 2012 Configuration Manager o Configuration Manager Current Branch

-   Applicazioni per System Center 2012 Configuration Manager e versioni successive  

-   Ambiente virtuale App-V di System Center 2012 Configuration Manager e versioni successive  

-   Personalizzazioni Asset Intelligence  

-   Limiti  

-   Raccolte: per eseguire la migrazione delle raccolte da una versione supportata di System Center 2012 Configuration Manager o Configuration Manager Current Branch, usare un processo di migrazione oggetti.  

-   Impostazioni di conformità:  

    -   Linee di base di configurazione  

    -   Elementi di configurazione  

-   Distribuzioni  

-   Distribuzione del sistema operativo:  

    -   Immagini d'avvio  

    -   Pacchetti driver  

    -   Driver  

    -   Immagini  

    -   Pacchetti  

    -   Sequenze attività  

-   Risultati della ricerca: criteri di ricerca salvati  

-   Aggiornamenti software:  

    -   Distribuzioni  

    -   Pacchetti di distribuzione  

    -   Modelli  

    -   Elenchi di aggiornamenti software  

-   Pacchetti di distribuzione software  

-   Regole di controllo software  

-   Pacchetti di applicazioni virtuali  

### <a name="objects-that-you-can-migrate-from-configuration-manager-2007-sp2"></a>Oggetti di cui è possibile eseguire la migrazione da Configuration Manager 2007 SP2

-   Annunci  

-   Applicazioni per System Center 2012 Configuration Manager e versioni successive  

-   Ambiente virtuale App-V di System Center 2012 Configuration Manager e versioni successive  

-   Personalizzazioni Asset Intelligence  

-   Limiti  

-   Raccolte: viene eseguita la migrazione delle raccolte da una versione supportata di Configuration Manager 2007 usando un processo di migrazione raccolte.  

-   Impostazioni di conformità (definite gestione configurazione desiderata in Configuration Manager 2007):  

    -   Linee di base di configurazione  

    -   Elementi di configurazione  

-   Distribuzione del sistema operativo:  

    -   Immagini d'avvio  

    -   Pacchetti driver  

    -   Driver  

    -   Immagini  

    -   Pacchetti  

    -   Sequenze attività  

-   Risultati della ricerca: cartelle di ricerca  

-   Aggiornamenti software:  

    -   Distribuzioni  

    -   Pacchetti di distribuzione  

    -   Modelli  

    -   Elenchi di aggiornamenti software  

-   Pacchetti di distribuzione software  

-   Regole di controllo software  

-   Pacchetti di applicazioni virtuali  

## <a name="data-that-you-cant-migrate-to-configuration-manager-current-branch"></a><a name="Cannot_migrate"></a> Dati di cui non è possibile eseguire la migrazione a Configuration Manager Current Branch

Non è possibile migrare i seguenti tipi di oggetti:  

-   Informazioni di provisioning client AMT  

-   File nei client, inclusi:  

    -   Dati cronologia e dati di inventario dei client  

    -   File nella cache del client  

-   Query  

-   Istanze e privilegi di protezione di Configuration Manager 2007 per il sito e gli oggetti  

-   Report di Configuration Manager 2007 provenienti da SQL Server Reporting Services  

-   Report Web di Configuration Manager 2007  

-   Report di System Center 2012 Configuration Manager e Configuration Manager Current Branch  

-   Amministrazione basata su ruoli di System Center 2012 Configuration Manager e Configuration Manager Current Branch:  

    -   ruoli di sicurezza  

    -   ambiti di protezione  
