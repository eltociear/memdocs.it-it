---
title: Privacy e sicurezza per l'inventario software
titleSuffix: Configuration Manager
description: Informazioni sulla sicurezza e la privacy per l'inventario software in Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 8e68e1fb-a8ec-4543-bb8a-cbbaf184a418
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d64fd2ac98996a6a1ccadae78e5f9cc576b55444
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690089"
---
# <a name="security-and-privacy-for-software-inventory-in-configuration-manager"></a>Sicurezza e privacy per l'inventario software in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Questo argomento contiene informazioni sulla sicurezza e la privacy per l'inventario software in Configuration Manager.  

##  <a name="security-best-practices-for-software-inventory"></a><a name="BKMK_Security_HardwareInventory"></a> Procedure ottimali di protezione per l'inventario software  
 Usare le procedure ottimali di protezione seguenti quando vengono raccolti i dati dell'inventario software dai client:  

|Procedura di sicurezza consigliata|Altre informazioni|  
|----------------------------|----------------------|  
|Firmare e crittografare i dati dell'inventario|Quando i client comunicano con i punti di gestione tramite HTTPS, tutti i dati inviati sono crittografati mediante SSL. Tuttavia, quando i computer client usano HTTP per comunicare con i punti di gestione nella rete Intranet, i dati dell'inventario del client e i file raccolti possono essere inviati senza firma e non crittografati. Assicurarsi che la configurazione del sito preveda la firma obbligatoria e l'uso della crittografia. Inoltre, se i client possono supportare l'algoritmo SHA-256, selezionare l'opzione che richiede l'uso di SHA-256.|  
|Non usare la raccolta file per raccogliere file critici o informazioni riservate|L'inventario software di Configuration Manager usa tutti i diritti dell'account LocalSystem, che può raccogliere le copie dei file di sistema critici, ad esempio il Registro di sistema o un database degli account di sicurezza. Quando questi file sono disponibili nel server del sito, un utente con i diritti Leggi risorsa o i diritti NTFS per il percorso dei file archiviati può analizzare il contenuto e individuare informazioni importanti relative al client e in questo modo compromettere la sicurezza.|  
|Limitare i diritti amministrativi locali sui computer client|Un utente con diritti amministrativi locali può inviare dati non validi come informazioni di inventario.|  

### <a name="security-issues-for-software-inventory"></a>Problemi di sicurezza per l'inventario software  
 La raccolta dell'inventario espone potenziali vulnerabilità. Gli utenti malintenzionati possono eseguire le attività seguenti:  

- Inviare dati non validi, che verranno accettati dal punto di gestione anche quando l'impostazione client dell'inventario software è disabilitata e la raccolta di file non è abilitata.  

- Inviare quantità eccessivamente elevate di dati in un singolo file e in un numero elevato di file e potenzialmente causare un attacco Denial of Service .  

- Accedere a informazioni dell'inventario mentre vengono trasferite a Configuration Manager.  

  Se gli utenti sanno che è possibile creare un file nascosto denominato **Skpswi.dat** e posizionarlo nella radice di un disco rigido del client per escluderlo dall'inventario software, non sarà possibile raccogliere i dati dell'inventario software dal computer.  

  Poiché un utente con privilegi di amministratore locale può inviare qualsiasi informazione come dati di inventario, non considerare affidabili i dati di inventario raccolti da Configuration Manager.  

  L'inventario software è abilitato per impostazione predefinita come impostazione client.  

##  <a name="privacy-information-for-software-inventory"></a><a name="BKMK_Privacy_HardwareInventory"></a> Informazioni sulla privacy per l'inventario software  
 L'inventario hardware consente di recuperare le informazioni archiviate nel Registro di sistema e in WMI nei client di Configuration Manager. L'inventario software consente di individuare tutti i file di un tipo specificato o raccogliere tutti i file specificati dai client. Asset Intelligence migliora le funzionalità di inventario mediante l'estensione dell'inventario hardware e software e l'aggiunta di nuove funzionalità di gestione delle licenze.  

 L'inventario hardware è abilitato per impostazione predefinita come impostazione client e le informazioni di WMI raccolte sono determinate dalle opzioni selezionate. L'inventario software è abilitato per impostazione predefinita, ma i file non vengono raccolti per impostazione predefinita. La raccolta di dati di Asset Intelligence viene abilitata automaticamente, anche se è possibile selezionare le classi di report per l'inventario hardware da abilitare.  

 Le informazioni relative all'inventario non vengono inviate a Microsoft. Le informazioni relative all'inventario vengono archiviate nel database di Configuration Manager. Quando i client usano HTTPS per connettersi ai punti di gestione, i dati dell'inventario inviati al sito vengono crittografati durante il trasferimento. Se i client usano HTTP per connettersi ai punti di gestione, è possibile scegliere di abilitare la crittografia dei dati dell'inventario. I dati dell'inventario non vengono memorizzate in forma crittografata nel database. Le informazioni vengono conservate nel database fino alla relativa eliminazione nell'ambito delle attività di manutenzione del sito **Elimina cronologia inventario obsoleta** o **Elimina file raccolti obsoleti** eseguite ogni 90 giorni. È possibile configurare l'intervallo di eliminazione.  

 Prima di configurare l'inventario hardware, l'inventario software, la raccolta di file o la raccolta di dati di Asset Intelligence, considerare i requisiti sulla privacy.  
