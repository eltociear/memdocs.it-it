---
title: Language Pack
titleSuffix: Configuration Manager
description: Informazioni sul supporto per le lingue disponibile in Configuration Manager.
ms.date: 06/29/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cd74e5f5-33f6-4566-8c9d-d6a93bfe71ed
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2f07f1277a9e87ea3266473fc54dc96907a0f0e6
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88698974"
---
# <a name="language-packs-in-configuration-manager"></a>Language Pack in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Questo articolo offre dettagli tecnici sul supporto per le lingue in Configuration Manager. I server e i client del sito di Configuration Manager sono considerati indipendenti dalla lingua. Aggiungere il supporto per le lingue visualizzate installando i **Language Pack server** o i **Language Pack client** in un sito di amministrazione centrale e nei siti primari. Durante il processo di installazione di un sito si selezionano le lingue per server e client da supportare in quel sito scegliendole dai file dei Language Pack disponibili.
 
Installare più lingue in ogni sito. È sufficiente installare le lingue usate.  

- Ogni sito supporta più lingue per le console di Configuration Manager.  

- In ogni sito è possibile installare Language Pack client singoli, aggiungendo il supporto solo per le lingue client che si vuole supportare.  

Quando si installa il supporto per una lingua corrispondente ai componenti seguenti:  

- La lingua di visualizzazione di un computer: sia nella console di Configuration Manager che nell'interfaccia utente client in esecuzione in quel computer vengono visualizzate informazioni in tale lingua.  

- La lingua preferita usata dal Web browser di un computer: le connessioni alle informazioni basate sul Web, inclusi il Catalogo applicazioni o SQL Server Reporting Services, vengono visualizzate in tale lingua.  


Durante l'installazione di Configuration Manager vengono scaricati i file dei Language Pack come parte dei file di prerequisiti e ridistribuibili. È anche possibile usare il [downloader di installazione](setup-downloader.md) per scaricare questi file prima di eseguire il programma di installazione.   



## <a name="server-languages"></a>Lingue server  

Usare la seguente tabella per il mapping tra ID impostazioni locali e una lingua da supportare nei server. Per altre informazioni sugli ID impostazioni locali, vedere [ID impostazioni locali assegnati da Microsoft](/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c).  

|Lingua server|ID impostazioni locali (LCID)|Codice di tre lettere|  
|---------------------|------------------------|-----------------------|  
|Inglese (predefinito)|0409|ITA|  
|Cinese (semplificato)|0804|CHS|  
|Cinese (tradizionale, Taiwan)|0404|CHT|  
|Ceco|0405|CSY|  
|Olandese (Paesi Bassi)|0413|NLD|  
|Francese|040c|FRA|  
|Tedesco|0407|DEU|  
|Ungherese|040e|HUN|  
|Italiano - Italia|0410|ITA|  
|Giapponese|0411|JPN|  
|Coreano|0412|KOR|  
|Polacco|0415|PLK|  
|Portoghese (Brasile)|0416|PTB|  
|Portoghese (Portogallo)|0816|PTG|  
|Russo|0419|RUS|  
|Spagnolo (Spagna)|0c0a|ESN|  
|Svedese|041d|SVE|  
|Turco|041f|TRK|  



## <a name="client-languages"></a>Lingue client  

Usare la tabella seguente per eseguire il mapping di un ID impostazioni locali con una lingua da supportare nei computer client. Per altre informazioni sugli ID impostazioni locali, vedere [ID impostazioni locali assegnati da Microsoft](/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c).  

|Lingua client|ID impostazioni locali (LCID)|Codice di tre lettere|  
|---------------------|------------------------|-----------------------|  
|Inglese (predefinito)|0409|ITA|  
|Cinese (semplificato)|0804|CHS|  
|Cinese (tradizionale, Taiwan)|0404|CHT|  
|Ceco|0405|CSY|  
|Danese|0406|DAN|  
|Olandese (Paesi Bassi)|0413|NLD|  
|Finlandese|040b|FIN|  
|Francese|040c|FRA|  
|Tedesco|0407|DEU|  
|Greco|0408|ELL|  
|Ungherese|040e|HUN|  
|Italiano - Italia|0410|ITA|  
|Giapponese|0411|JPN|  
|Coreano|0412|KOR|  
|Norvegese|0414|NOR|  
|Polacco|0415|PLK|  
|Portoghese (Brasile)|0416|PTB|  
|Portoghese (Portogallo)|0816|PTG|  
|Russo|0419|RUS|  
|Spagnolo (Spagna)|0c0a|ESN|  
|Svedese|041d|SVE|  
|Turco|041f|TRK|  


### <a name="mobile-device-client-languages"></a>Lingue client per dispositivi mobili  
Quando si aggiunge il supporto per le lingue per dispositivi mobili, vengono incluse tutte le lingue client per dispositivi mobili supportate. Non è possibile selezionare singoli Language Pack per il supporto dei dispositivi mobili.  



## <a name="identify-installed-language-packs"></a>Identificare i Language Pack installati  
Per identificare i Language Pack installati in un computer che esegue il client di Configuration Manager, cercare l'ID impostazioni locali (LCID) dei Language Pack installati nel Registro di sistema del computer. Queste informazioni sono disponibili nel percorso del Registro di sistema seguente:  

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCMSetup\InstalledLangs`  

Personalizzare l'inventario hardware per raccogliere queste informazioni. Creare quindi un report personalizzato per visualizzare i dettagli per la lingua. Per altre informazioni sulla raccolta di un inventario hardware personalizzato, vedere [Come configurare l'inventario hardware](../../../clients/manage/inventory/configure-hardware-inventory.md). Per altre informazioni, vedere [Creare report](../../manage/operations-and-maintenance-for-reporting.md#create-reports).