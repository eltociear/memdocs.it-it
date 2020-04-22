---
title: Privacy e sicurezza per l'inventario hardware
titleSuffix: Configuration Manager
description: Informazioni sulla sicurezza e la privacy per l'inventario hardware in Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 62e20d86-db6d-4a1f-b14a-905a9de31698
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a5989c80818ac45bb8dd6a4f768595dbd56b846d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690109"
---
# <a name="security-and-privacy-for-hardware-inventory-in-configuration-manager"></a>Sicurezza e privacy per l'inventario hardware in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Questo argomento contiene informazioni sulla sicurezza e la privacy per l'inventario hardware in Configuration Manager.  

##  <a name="security-best-practices-for-hardware-inventory"></a><a name="BKMK_Security_HardwareInventory"></a> Procedure consigliate di sicurezza per l'inventario hardware  
 Usare le procedure consigliate di sicurezza seguenti quando vengono raccolti i dati dell'inventario hardware dai client:  

|Procedura di sicurezza consigliata|Altre informazioni|  
|----------------------------|----------------------|  
|Firmare e crittografare i dati dell'inventario|Quando i client comunicano con i punti di gestione tramite HTTPS, tutti i dati inviati sono crittografati mediante SSL. Tuttavia, quando i computer client usano HTTP per comunicare con i punti di gestione nella rete Intranet, i dati dell'inventario del client e i file raccolti possono essere inviati senza firma e non crittografati. Assicurarsi che la configurazione del sito preveda la firma obbligatoria e l'uso della crittografia. Inoltre, se i client possono supportare l'algoritmo SHA-256, selezionare l'opzione per richiedere SHA-256.|  
|Non raccogliere i file IDMIF e NOIDMIF negli ambienti a elevata sicurezza|È possibile utilizzare l'insieme di file IDMIF e NOIDMIF per estendere l'inventario hardware. Se necessario, Configuration Manager crea nuove tabelle o modifica tabelle esistenti nel database di Configuration Manager per contenere le proprietà nei file IDMIF e NOIDMIF. Tuttavia, Configuration Manager non convalida i file IDMIF e NOIDMIF, pertanto questi file potrebbero essere usati per modificare le tabelle che non si vuole modificate. Dati validi potrebbero essere sovrascritti da dati non validi. È anche possibile che vengano aggiunte grandi quantità di dati e l'elaborazione di tali dati potrebbe provocare ritardi in tutte le funzioni di Configuration Manager. Per limitare tali rischi, configurare l'impostazione client dell'inventario hardware **Raccogli file MIF** su **Nessuno**.|  

### <a name="security-issues-for-hardware-inventory"></a>Problemi di sicurezza per l'inventario hardware  
 La raccolta dell'inventario espone potenziali vulnerabilità. Gli utenti malintenzionati possono eseguire le attività seguenti:  

- Inviare dati non validi, che verranno accettati dal punto di gestione anche quando l'impostazione client dell'inventario software è disabilitata e la raccolta di file non è abilitata.  

- Inviare quantità eccessivamente elevate di dati in un singolo file e in un numero elevato di file e potenzialmente causare un attacco Denial of Service .  

- Accedere a informazioni dell'inventario mentre vengono trasferite a Configuration Manager.  

  Poiché un utente con privilegi di amministratore locale può inviare qualsiasi informazione come dati di inventario, non considerare affidabili i dati di inventario raccolti da Configuration Manager.  

  L'inventario hardware è abilitato per impostazione predefinita come impostazione client.  

##  <a name="privacy-information-for-hardware-inventory"></a><a name="BKMK_Privacy_HardwareInventory"></a> Informazioni sulla privacy per l'inventario hardware  
 L'inventario hardware consente di recuperare le informazioni archiviate nel Registro di sistema e in WMI nei client di Configuration Manager. L'inventario software consente di individuare tutti i file di un tipo specificato o raccogliere tutti i file specificati dai client. Asset Intelligence migliora le funzionalità di inventario mediante l'estensione dell'inventario hardware e software e l'aggiunta di nuove funzionalità di gestione delle licenze.  

 L'inventario hardware è abilitato per impostazione predefinita come impostazione client e le informazioni di WMI raccolte sono determinate dalle opzioni selezionate. L'inventario software è abilitato per impostazione predefinita, ma i file non vengono raccolti per impostazione predefinita. La raccolta di dati di Asset Intelligence viene abilitata automaticamente, anche se è possibile selezionare le classi di report per l'inventario hardware da abilitare.  

 Le informazioni relative all'inventario non vengono inviate a Microsoft. Le informazioni relative all'inventario vengono archiviate nel database di Configuration Manager. Quando i client usano HTTPS per connettersi ai punti di gestione, i dati dell'inventario inviati al sito vengono crittografati durante il trasferimento. Se i client usano HTTP per connettersi ai punti di gestione, è possibile scegliere di abilitare la crittografia dei dati dell'inventario. I dati dell'inventario non vengono memorizzate in forma crittografata nel database. Le informazioni vengono conservate nel database fino alla relativa eliminazione nell'ambito delle attività di manutenzione del sito **Elimina cronologia inventario obsoleta** o **Elimina file raccolti obsoleti** eseguite ogni 90 giorni. È possibile configurare l'intervallo di eliminazione.  

 Prima di configurare l'inventario hardware, l'inventario software, la raccolta di file o la raccolta di dati di Asset Intelligence, considerare i requisiti sulla privacy.  
