---
title: Privacy e sicurezza per Asset Intelligence
titleSuffix: Configuration Manager
description: Informazioni sulla sicurezza e la privacy per Asset Intelligence in Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d0c6f7a0-dcae-4e6d-aa28-35d464d97ff7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3cf35b050b110c655ac85e82a7990f9ea2ac3636
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695029"
---
# <a name="security-and-privacy-for-asset-intelligence-in-configuration-manager"></a>Sicurezza e privacy per Asset Intelligence in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Questo argomento contiene informazioni sulla sicurezza e la privacy per Asset Intelligence in Configuration Manager.  

##  <a name="security-best-practices-for-asset-intelligence"></a><a name="BKMK_Security_AI"></a> Procedura consigliate per la sicurezza per Asset Intelligence  
 Usare le procedure consigliate per la sicurezza seguenti per i casi in cui si usa Asset Intelligence.  

|Procedura di sicurezza consigliata|Altre informazioni|  
|----------------------------|----------------------|  
|Quando si importa un file di licenza (file Microsoft Volume Licensing o file di resoconto licenze generale), proteggere il file e il canale di comunicazione.|Usare le autorizzazioni del file system NTFS per garantire che solo gli utenti autorizzati possano accedere ai file di licenza e usare firme Server Message Block (SMB) per assicurare l'integrità dei dati quando vengono trasferiti al server del sito durante il processo di importazione.|  
|Usare il principio di autorizzazione con privilegi minimi per importare i file di licenza.|Usare l'amministrazione basata su ruoli per concedere l'autorizzazione Gestisci Asset Intelligence all'utente amministratore che importa i file di licenza. Il ruolo predefinito di Gestione asset include questa autorizzazione.|  

##  <a name="privacy-information-for-asset-intelligence"></a><a name="BKMK_Privacy_HardwareInventory"></a> Informazioni sulla privacy per Asset Intelligence  
 Asset Intelligence estende le funzionalità di inventario di Configuration Manager in modo da offrire un livello maggiore di visibilità delle risorse nell'azienda. La raccolta di informazioni di Asset Intelligence non è abilitata automaticamente. È possibile modificare il tipo di informazioni raccolte abilitando le classi di report di inventario hardware. Per altre informazioni, vedere [Configurazione di Asset Intelligence](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

 Le informazioni di Asset Intelligence vengono archiviate nel database di Configuration Manager analogamente alle informazioni relative all'inventario. Quando i client si connettono ai punti di gestione tramite HTTPS, i dati vengono sempre crittografati durante il trasferimento al punto di gestione. Quando i client si connettono tramite HTTP, è possibile configurare il trasferimento dei dati di inventario in modo che i dati siano firmati e crittografati. I dati di inventario non vengono archiviati in formato crittografato nel database. Le informazioni vengono mantenute nel database fino a quando non vengono eliminate, ogni 90 giorni, dall'attività di manutenzione del sito **Elimina cronologia inventario obsoleta** . È possibile configurare l'intervallo di eliminazione.  

 Asset Intelligence non invia a Microsoft informazioni su utenti e computer o sull'utilizzo delle licenze. È possibile scegliere di inviare a System Center Online richieste per la categorizzazione, ovvero contrassegnare uno o più titoli software non categorizzati e inviarli a System Center Online per la ricerca e la categorizzazione. Una volta caricato un titolo software, i ricercatori Microsoft identificano, categorizzano e rendono disponibili le informazioni a tutti i clienti che usano il servizio online. È consigliabile considerare le implicazioni per la privacy seguenti relative all'invio di informazioni a System Center Online:  

- Il caricamento si applica solo alle informazioni dei titoli software generiche (nome, autore e così via) che si sceglie di inviare a System Center Online. Le informazioni relative all'inventario non vengono inviate con un caricamento.  

- Il caricamento non avviene mai automaticamente e il sistema non è progettato per l'automatizzazione di questa attività. È necessario selezionare manualmente e approvare il caricamento di ogni titolo di software.  

- Prima che venga avviato il processo di caricamento, una finestra di dialogo mostra esattamente quali dati verranno caricati.  

- Le informazioni sulle licenze non vengono inviate a Microsoft. Le informazioni sulle licenze vengono archiviate in un'area separata del database di Configuration Manager e non possono essere inviate a Microsoft.  

- Tutti i titoli software caricati diventano pubblici, nel senso che le informazioni su una determinata applicazione e la relativa categorizzazione diventano parte del catalogo di Asset Intelligence in System Center Online e possono quindi essere scaricate da altri utenti del catalogo.  

- L'origine del titolo software non viene registrata nel catalogo di Asset Intelligence e non viene resa disponibile agli altri clienti. È comunque necessario verificare di non caricare alcun titolo di applicazione che contiene informazioni private.  

- Non è possibile annullare il caricamento dei dati selezionati.  

  Prima di configurare la raccolta dati di Asset Intelligence e di scegliere se inviare informazioni a System Center Online, prendere in considerazione i requisiti per la privacy della propria organizzazione.  
