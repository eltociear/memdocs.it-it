---
title: Icone per gli aggiornamenti software
titleSuffix: Configuration Manager
description: La console di Configuration Manager contiene le icone che indicano uno stato per il gruppo di aggiornamenti software o per l'aggiornamento sincronizzato.
manager: dougeby
ms.date: 10/06/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 63c5ef72-5715-4d86-85a2-71beba469fab
author: mestew
ms.author: mstewart
ms.openlocfilehash: 3843dd4ab4fe5a9aecaae8e6f207c3d037fc1950
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700049"
---
# <a name="icons-used-for-software-updates-in-configuration-manager"></a>Icone usate per gli aggiornamenti software in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Gli aggiornamenti software sincronizzati vengono visualizzati nella console di Configuration Manager e la prima colonna per ogni aggiornamento software contiene un'icona che indica uno stato specifico. I gruppi di aggiornamenti software sono rappresentati anche con un'icona che fornisce informazioni sullo stato degli aggiornamenti software contenuti nel gruppo. Questa sezione fornisce informazioni sulle icone di aggiornamento software e sul significato di ogni icona.  

## <a name="icons-for-software-updates"></a>Icone per gli aggiornamenti software  
 Gli aggiornamenti software sincronizzati sono rappresentati da una delle icone seguenti.  

### <a name="normal-icon"></a>Icona Normale  
 ![icona](../media/Normal.jpg "Icona Normale") L'icona con la freccia verde rappresenta un aggiornamento software normale.  

 **Descrizione:**  

 Gli aggiornamenti software normali sono stati sincronizzati e sono disponibili per la distribuzione software.  

 **Problemi operativi:**  

 Non sono presenti problemi operativi.  

### <a name="expired-icon"></a>Icona Scaduto  
 ![icon](../media/Expired.jpg "Icona Scaduto") L'icona con la X nera rappresenta un aggiornamento software scaduto. È possibile identificare gli aggiornamenti software scaduti anche visualizzando la colonna **Scaduto** per l'aggiornamento software quando questo viene visualizzato nella console di Configuration Manager.  

 **Descrizione:**  

 Gli aggiornamenti software scaduti erano in precedenza distribuibili ai computer client, ma dopo la scadenza di un aggiornamento software non è possibile creare nuove distribuzioni per gli aggiornamenti software. Gli aggiornamenti software scaduti vengono rimossi dalle distribuzioni attive e non saranno più disponibili per i client.  

 **Problemi operativi:**  

 Non sono presenti problemi operativi.

### <a name="superseded-icon"></a>Icona Sostituito  
 ![icon](../media/Superseded.jpg "Icona Sostituito") L'icona con la stella gialla rappresenta un aggiornamento software sostituito. È possibile identificare gli aggiornamenti software sostituiti anche visualizzando la colonna **Sostituito** per l'aggiornamento software quando questo viene visualizzato nella console di Configuration Manager.  

 **Descrizione:**  

 Gli aggiornamenti software sostituiti sono stati sostituiti con le versioni più recenti dell'aggiornamento software. In genere, un aggiornamento software che sostituisce un altro aggiornamento software offre uno o più dei seguenti vantaggi:  

- Migliora o incrementa la correzione fornita da uno o più aggiornamenti software rilasciati in precedenza.  

- Migliora l'efficienza del pacchetto dei file di aggiornamento software, che viene installato nei client se l'aggiornamento software viene approvato per l'installazione. Ad esempio, l'aggiornamento software sostituito potrebbe contenere file che non sono più rilevanti per la correzione o per i sistemi operativi ora supportati dal nuovo aggiornamento software e quindi tali file non sono inclusi nel pacchetto di file di aggiornamento software sostitutivo.  

- Aggiorna le versioni più recenti di un prodotto o, in altre parole, non è più applicabile alle versioni o configurazioni precedenti di un prodotto. Gli aggiornamenti software possono anche sostituire altri aggiornamenti software se sono state apportate modifiche per espandere il supporto della lingua. Ad esempio, una revisione recente di un aggiornamento prodotto per Microsoft Office potrebbe rimuovere il supporto per un sistema operativo precedente, ma potrebbe aggiungere supporto aggiuntivo per nuove lingue nel rilascio dell'aggiornamento software iniziale.  

  Nella scheda Regole di sostituzione delle proprietà del componente del punto di aggiornamento software è possibile specificare come gestire gli aggiornamenti software sostituiti. Per altre informazioni, vedere [Supersedence rules](../plan-design/plan-for-software-updates.md#BKMK_SupersedenceRules).  

  **Problemi operativi:**  

  Quando possibile, distribuire l'aggiornamento software sostitutivo ai computer client anziché l'aggiornamento software sostituito. È possibile visualizzare un elenco degli aggiornamenti software che sostituiscono l'aggiornamento software nella scheda **Informazioni di sostituzione** delle proprietà dell'aggiornamento software.  

### <a name="invalid-icon"></a>Icona Non valido  
 ![icona](../media/Invalid.jpg "Icona Non valido") L'icona con la X rossa rappresenta un aggiornamento software non valido.  

 **Descrizione:**  

 Gli aggiornamenti software non validi si trovano in una distribuzione attiva, ma per qualche motivo il contenuto (file di aggiornamento software) non è disponibile. Questo stato può verificarsi negli scenari seguenti:  

- L'aggiornamento software viene distribuito correttamente, ma il file di aggiornamento software viene rimosso dal pacchetto di distribuzione e non è più disponibile.  

- Si crea una distribuzione degli aggiornamenti software in un sito e l'oggetto di distribuzione viene replicato correttamente in un sito figlio, ma il pacchetto di distribuzione non viene replicato nel sito figlio.  

  **Problemi operativi:**  

  Quando non è disponibile contenuto per un aggiornamento software, i client non riescono a installare l'aggiornamento software finché il contenuto non diventa disponibile in un punto di distribuzione. È possibile ridistribuire il contenuto nei punti di distribuzione usando l'azione **Ridistribuisci** . Quando non è disponibile contenuto per un aggiornamento software in una distribuzione creata in un sito padre, l'aggiornamento software deve essere replicato o ridistribuito al sito figlio. Per altre informazioni sulla ridistribuzione di contenuto, vedere [Gestire il contenuto distribuito](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_manage).  

### <a name="metadata-only-icon"></a>Icona Solo metadati
 ![icona](../media/MetadataOnly.png "Icona Solo metadati") L'icona con la freccia blu rappresenta un aggiornamento software solo di metadati.

 **Descrizione:**  

 Gli aggiornamenti software solo di metadati sono disponibili nella console di Configuration Manager per la creazione di report. Non è possibile distribuire o scaricare gli aggiornamenti software solo di metadati perché un file di aggiornamento software non è associato ai metadati degli aggiornamenti software.  

 **Problemi operativi:**  

 Gli aggiornamenti software solo di metadati sono disponibili per la creazione di report e non sono destinati alla distribuzione di aggiornamenti software.  

## <a name="icons-for-software-update-groups"></a>Icone per gruppi di aggiornamenti software  
 I gruppi di aggiornamenti software sono rappresentati da una delle icone seguenti.  

### <a name="normal-icon"></a>Icona Normale  
 ![icona](../media/Normal.jpg "Icona Normale") L'icona con la freccia verde rappresenta un gruppo di aggiornamenti software che include solo gli aggiornamenti software normali.  

 **Problemi operativi:**  

 Non sono presenti problemi operativi.  

### <a name="expired-icon"></a>Icona Scaduto  
 ![icona](../media/Expired.jpg "Icona Scaduto") L'icona con la X nera rappresenta un gruppo di aggiornamenti software che include uno o più aggiornamenti software scaduti.  

 **Problemi operativi:**  

 Rimuovere o sostituire gli aggiornamenti software scaduti nel gruppo di aggiornamenti software, quando possibile.  

### <a name="superseded-icon"></a>Icona Sostituito  
 ![icona](../media/Superseded.jpg "Icona Sostituito") L'icona con la stella gialla rappresenta un gruppo di aggiornamenti software che include uno o più aggiornamenti software sostituiti.  

 **Problemi operativi:**  

 Sostituire l'aggiornamento software sostituito nel gruppo di aggiornamenti software con l'aggiornamento software sostitutivo, quando possibile.  

### <a name="invalid-icon"></a>Icona Non valido  
 ![icona](../media/Invalid.jpg "Icona Non valido") L'icona con la X rossa rappresenta un gruppo di aggiornamenti software che include uno o più aggiornamenti software non validi.  

 **Problemi operativi:**  

 Quando non è disponibile contenuto per un aggiornamento software, i client non riescono a installare l'aggiornamento software finché il contenuto non diventa disponibile in un punto di distribuzione. È possibile ridistribuire il contenuto nei punti di distribuzione usando l'azione **Ridistribuisci** . Quando non è disponibile contenuto per un aggiornamento software in una distribuzione creata in un sito padre, l'aggiornamento software deve essere replicato o ridistribuito al sito figlio. Per altre informazioni sulla ridistribuzione di contenuto, vedere [Gestire il contenuto distribuito](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_manage).  


## <a name="next-steps"></a>Passaggi successivi 

[Plan for software updates](../plan-design/plan-for-software-updates.md) (Pianificare gli aggiornamenti del software)