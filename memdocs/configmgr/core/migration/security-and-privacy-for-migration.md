---
title: Sicurezza e privacy per la migrazione
titleSuffix: Configuration Manager
description: Procedure consigliate per la sicurezza e informazioni sulla privacy per la migrazione all'ambiente Configuration Manager Current Branch.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6893fce1-7ad5-4151-9ba9-3096871e8e4a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f219c6c6d4c9a5cbf04b1295c99184f345e68b83
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692860"
---
# <a name="security-and-privacy-for-migration-to-configuration-manager-current-branch"></a>Sicurezza e privacy per la migrazione a Configuration Manager Current Branch

*Si applica a: Configuration Manager (Current Branch)*

In questo argomento vengono illustrate le procedure consigliate per la sicurezza e le informazioni sulla privacy per la migrazione all'ambiente Configuration Manager Current Branch.  

## <a name="security-best-practices-for-migration"></a>Procedure di protezione consigliate per la migrazione  
 Utilizzare la seguente procedura di protezione consigliata per la migrazione.  

|Procedura di sicurezza consigliata|Altre informazioni|  
|----------------------------|----------------------|  
|Utilizzare l'account computer per l'account del provider SMS del sito di origine e l'account di SQL Server del sito di origine invece dell'account utente.|Se è necessario utilizzare un account utente per la migrazione, rimuovere i dettagli dell'account al termine della migrazione.|  
|Utilizzare IPsec quando si esegue la migrazione del contenuto da un punto di distribuzione in un sito di origine a un punto di distribuzione nel sito di destinazione.|Sebbene venga eseguito l'hashing del contenuto migrato per rilevare un'eventuale manomissione, se i dati vengono modificati durante il trasferimento, la migrazione non sarà eseguita correttamente.|  
|Limitare e controllare gli utenti amministratori autorizzati a creare processi di migrazione.|L'integrità del database della gerarchia di destinazione dipende dall'integrità dei dati che l'utente amministratore sceglie di importare dalla gerarchia di origine. Inoltre, questo utente amministratore può leggere tutti i dati dalla gerarchia di origine.|  

### <a name="security-issues-for-migration"></a>Problemi di protezione per la migrazione  
La migrazione presenta i seguenti problemi di protezione:  

-   I client che sono bloccati da un sito di origine potrebbero essere correttamente assegnati alla gerarchia di destinazione prima della migrazione del relativo record client.  

     Sebbene Configuration Manager mantenga lo stato bloccato dei client in corso di migrazione, il client può essere correttamente assegnato alla gerarchia di destinazione se l'assegnazione avviene prima del completamento della migrazione del record client.  

-   I messaggi di controllo non vengono migrati.  

Quando si esegue la migrazione di dati da un sito di origine a un sito di destinazione, vengono perse le informazioni di controllo dalla gerarchia di origine.  

## <a name="privacy-information-for-migration"></a>Informazioni sulla privacy per la migrazione  
 Durante la migrazione vengono individuate delle informazioni dai database del sito identificate in un'infrastruttura di origine che vengono archiviate nel database della gerarchia di destinazione. Le informazioni che Configuration Manager è in grado di individuare da una gerarchia o un sito di origine dipendono dalle funzionalità abilitate nell'ambiente di origine e dalle operazioni di gestione eseguite in tale ambiente.  

 Per ulteriori informazioni sulla protezione e privacy, vedere uno degli argomenti seguenti:  

-   Per altre informazioni sulla privacy per Configuration Manager 2007, vedere [Protezione e privacy per Configuration Manager 2007](/previous-versions/system-center/configuration-manager-2007/bb680768(v=technet.10)) nella libreria della documentazione di Configuration Manager 2007.  

-   Per altre informazioni sulla privacy per System Center 2012 Configuration Manager, vedere [Protezione e privacy per System Center 2012 Configuration Manager](/previous-versions/system-center/system-center-2012-R2/gg682033(v=technet.10)) nella libreria della documentazione di System Center 2012 Configuration Manager.  

-   Per altre informazioni sulla privacy per Configuration Manager, vedere [Sicurezza e privacy per Configuration Manager](../../core/plan-design/security/security-and-privacy.md).  

È possibile migrare solo alcuni o tutti i dati supportati da un sito di origine a una gerarchia di destinazione.  

Per impostazione predefinita, la migrazione non è abilitata e richiede diversi passaggi di configurazione. Le informazioni di migrazione non vengono inviate a Microsoft.  

Prima di migrare i dati da una gerarchia di origine, considerare i requisiti di privacy.