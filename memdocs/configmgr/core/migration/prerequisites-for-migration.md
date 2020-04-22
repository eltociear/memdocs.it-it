---
title: Prerequisiti per la migrazione
titleSuffix: Configuration Manager
description: Individuare le versioni supportate di Configuration Manager, le lingue del sito di origine supportate e le configurazioni necessarie per la migrazione.
ms.date: 05/7/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ec976930-7467-4d3c-b33c-991bf408a74a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 229a8c7980933480a243278b2679d55f012490ce
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693419"
---
# <a name="prerequisites-for-migration-in-configuration-manager"></a>Prerequisiti per la migrazione in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Per eseguire la migrazione da una gerarchia di origine supportata, è necessario avere accesso a ogni sito di origine applicabile di Configuration Manager e le autorizzazioni per la configurazione e l'esecuzione delle operazioni di migrazione all'interno del sito di destinazione di Configuration Manager.  

 Usare le informazioni contenute nelle sezioni seguenti per individuare le versioni di Configuration Manager supportate per la migrazione e le configurazioni necessarie.  

-   [Versioni di Configuration Manager supportate per la migrazione](#BKMK_SupportedMigrationVersions)  

-   [Lingue del sito di origine supportate per la migrazione](#BKMK_SorceSiteLanguage)  

-   [Configurazioni necessarie per la migrazione](#BKMK_Required_Configurations)  

##  <a name="versions-of-configuration-manager-that-are-supported-for-migration"></a><a name="BKMK_SupportedMigrationVersions"></a> Versioni di Configuration Manager supportate per la migrazione  
 È possibile eseguire la migrazione di dati da una gerarchia di origine che esegue una delle versioni seguenti di Configuration Manager:  

- Configuration Manager 2007 SP2  (ai fini della migrazione, le versioni di Configuration Manager 2007 R2 o R3 nel sito di origine non sono prese in considerazione. Se il sito di origine esegue SP2, i siti in cui è installato il componente aggiuntivo R2 o R3 sono supportati per la migrazione a Configuration Manager Current Branch).  

- System Center 2012 Configuration Manager SP2 o System Center 2012 R2 Configuration Manager SP1.  

  > [!TIP]  
  >  Oltre alla migrazione, è possibile usare un aggiornamento sul posto dei siti che eseguono System Center 2012 Configuration Manager a Configuration Manager Current Branch.  

- Gerarchia di Configuration Manager della stessa versione o di una versione precedente di Configuration Manager.  

  Ad esempio, se è presente una gerarchia di destinazione che esegue Configuration Manager Current Branch 1606, è possibile usare la migrazione per copiare dati da una gerarchia di origine che esegue la versione 1606 o 1602. Non è tuttavia possibile copiare dati da una gerarchia di origine che esegue la versione 1610.  


##  <a name="source-site-languages-that-are-supported-for-migration"></a><a name="BKMK_SorceSiteLanguage"></a> Lingue del sito di origine supportate per la migrazione  
 Durante la migrazione dei dati da una gerarchia all'altra di Configuration Manager, i dati vengono archiviati nella gerarchia di destinazione nel formato indipendente dalla lingua per Configuration Manager. Dal momento che Configuration Manager 2007 non archivia i dati in un formato indipendente dalla lingua, il processo di migrazione deve convertire gli oggetti in questo formato durante la migrazione da Configuration Manager 2007. Di conseguenza, per la migrazione sono supportati solo i siti di origine di Configuration Manager 2007 installati con le seguenti lingue:  

-   Inglese  

-   Francese  

-   Tedesco  

-   Giapponese  

-   Coreano  

-   Russo  

-   Cinese semplificato  

-   Cinese tradizionale  

Quando si esegue la migrazione di dati da una gerarchia di System Center 2012 Configuration Manager o di Configuration Manager Current Branch, non ci sono limiti per le lingue del sito di origine. Gli oggetti nel database del sito di origine sono già in un formato indipendente dalla lingua.  

##  <a name="required-configurations-for-migration"></a><a name="BKMK_Required_Configurations"></a> Configurazioni necessarie per la migrazione  
Di seguito sono elencate le configurazioni necessarie per l'uso della migrazione e delle operazioni di migrazione:  

- **Per configurare, eseguire e monitorare la migrazione nella console di Configuration Manager:**  

   Nel sito di destinazione, all'account deve essere assegnato il ruolo di sicurezza di amministrazione basato su ruoli di **Amministratore infrastruttura**. Questo ruolo di sicurezza concede le autorizzazioni di gestione per tutte le operazioni di migrazione, tra cui la creazione dei processi di migrazione, la pulizia, il monitoraggio e l'azione di condivisione e aggiornamento dei punti di distribuzione.  

- **Raccolta dati:**  

   Per abilitare il sito di destinazione alla raccolta dei dati, è necessario configurare i due account di accesso al sito di origine che seguono per l'utilizzo con tutti i siti di origine:  

  -   **Account del sito di origine:** Questo account viene usato per l'accesso al provider SMS del sito di origine.  

      -   Per un sito di origine di Configuration Manager 2007 SP2, questo account richiede l'autorizzazione **Lettura** per tutti gli oggetti del sito di origine.  

      -   Per un sito di origine di System Center 2012 Configuration Manager o Configuration Manager Current Branch, questo account richiede l'autorizzazione **Lettura** per tutti gli oggetti del sito di origine. L'autorizzazione all'account viene concessa tramite l'amministrazione basata su ruoli. Per informazioni su come usare l'amministrazione basata su ruoli, vedere [Nozioni fondamentali di amministrazione basata su ruoli per Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

  -   **Account del database del sito di origine:** questo account viene usato per l'accesso al database SQL Server del sito di origine e richiede le autorizzazioni **Connect**, **Execute**e **Select** per il database del sito di origine.  

  È possibile configurare questi account durante la configurazione di una nuova gerarchia di origine, la raccolta dati per un sito di origine aggiuntivo o la riconfigurazione delle credenziali per un sito di origine. Questi account possono utilizzare un account utente di dominio oppure è possibile specificare l'account computer del sito di livello superiore della gerarchia di destinazione.  

  > [!IMPORTANT]  
  >  Se si usa l'account computer di Configuration Manager per un account di accesso, verificare che l'account appartenga al gruppo di sicurezza **Distributed COM Users** nel dominio in cui si trova il sito di origine.  

  Durante la raccolta dati vengono utilizzati le porte e i protocolli di rete seguenti:  

  -   NetBIOS/SMB - 445 (TCP)  

  -   RPC (WMI) - 135 (TCP)  

  -   SQL Server - porte TCP utilizzate dai database del sito di origine e di destinazione.  

- **Eseguire la migrazione degli aggiornamenti software:**  

   Prima di eseguire la migrazione degli aggiornamenti software, è necessario configurare la gerarchia di destinazione con un punto di aggiornamento software. Per altre informazioni, vedere [Pianificazione per eseguire la migrazione degli aggiornamenti software](../../core/migration/planning-for-the-migration-of-objects.md#Plan_migrate_Software_updates).  

- **Condividere i punti di distribuzione:**  

   Per condividere correttamente i punti di distribuzione da un sito di origine, è necessario che almeno un sito primario o il sito di amministrazione centrale nella gerarchia di destinazione utilizzi gli stessi numeri di porta per le richieste client del sito di origine. Per informazioni sulle porte di richiesta client, vedere [Come configurare porte di comunicazione client](../../core/clients/deploy/configure-client-communication-ports.md)  

   Per ogni sito di origine, vengono condivisi solo i punti di distribuzione installati nei server di sistema del sito configurati con un FQDN.  

   Per condividere un punto di distribuzione da un sito di origine di System Center 2012 Configuration Manager o di Configuration Manager Current Branch, l'**account del sito di origine** (che accede al provider SMS per il server del sito di origine) deve avere anche l'autorizzazione **Modifica** per l'oggetto **Sito** nel sito di origine. È possibile concedere questa autorizzazione all'account utilizzando l'amministrazione basata su ruoli. Per informazioni su come usare l'amministrazione basata su ruoli, vedere [Nozioni fondamentali di amministrazione basata su ruoli per Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  


- **Aggiornare o riassegnare i punti di distribuzione:**  

   L' **account di accesso al sito di origine** configurato per la raccolta dei dati dal provider SMS del sito di origine deve disporre delle seguenti autorizzazioni:  

  - Per aggiornare un punto di distribuzione di Configuration Manager 2007, l'account richiede le autorizzazioni **Lettura**, **Esecuzione** ed **Eliminazione** per la classe **Sito** nel server del sito di Configuration Manager 2007 per rimuovere correttamente il punto di distribuzione dal sito di origine di Configuration Manager 2007.  

  - Per riassegnare un punto di distribuzione di System Center 2012 Configuration Manager o Configuration Manager Current Branch, l'account deve avere l'autorizzazione **Modifica** per l'oggetto **Sito** nel sito di origine. È possibile concedere questa autorizzazione all'account utilizzando l'amministrazione basata su ruoli. Per informazioni su come usare l'amministrazione basata su ruoli, vedere [Nozioni fondamentali di amministrazione basata su ruoli per Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

    Per aggiornare o riassegnare correttamente un punto di distribuzione a una nuova gerarchia, le porte configurate per le richieste client nel sito che gestisce il punto di distribuzione nella gerarchia di origine devono corrispondere alla porte configurate per richieste client nel sito di destinazione che gestirà il punto di distribuzione. Per informazioni sulle porte di richiesta client, vedere [Come configurare porte di comunicazione client](../../core/clients/deploy/configure-client-communication-ports.md).  
