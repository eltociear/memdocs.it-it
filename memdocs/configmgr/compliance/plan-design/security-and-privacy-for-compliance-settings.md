---
title: Sicurezza e privacy per le impostazioni di conformità
titleSuffix: Configuration Manager
description: Informazioni sulle procedure di sicurezza consigliate per le impostazioni di conformità in Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 1c409244-6778-4970-a99c-d2508c9cf62b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: eae705b97add7515403549eb668e68f1489d6756
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692179"
---
# <a name="security-and-privacy-for-compliance-settings-in-configuration-manager"></a>Sicurezza e privacy per le impostazioni di conformità in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*


## <a name="security-best-practices-for-compliance-settings"></a>Procedure di sicurezza consigliate per le impostazioni di conformità  

|Procedura di sicurezza consigliata|Altre informazioni|  
|----------------------------|----------------------|  
|Non monitorare i dati sensibili.|Per evitare la divulgazione di informazioni, non configurare elementi di configurazione per il monitoraggio di informazioni potenzialmente riservate.|  
|Non configurare regole di conformità che usano dati modificabili dagli utenti finali.|Se si crea una regola di conformità in base a dati che gli utenti possono modificare, ad esempio le impostazioni del Registro di sistema per le scelte di configurazione, i risultati di conformità non saranno affidabili.|  
|Importare pacchetti di configurazione di Microsoft System Center e altri dati di configurazione da origini esterne solo se dispongono di una firma digitale valida da un autore attendibile.|I dati di configurazione pubblicati possono essere dotati di firma digitale, in modo che sia possibile verificare l'origine della pubblicazione e assicurarsi che i dati non siano stati manomessi. Se il controllo della verifica della firma digitale ha esito negativo, l'utente riceve un avviso e una richiesta di conferma dell'importazione. Non importare dati non firmati se non è possibile verificare l'origine e l'integrità dei dati stessi.|  
|Implementare i controlli di accesso per proteggere i computer di riferimento.|Quando un utente amministratore configura un'impostazione del Registro di sistema o del file system selezionando un computer di riferimento, assicurarsi che quest'ultimo non sia stato compromesso.|  
|Proteggere il canale di comunicazione quando si passa a un computer di riferimento.|Per impedire l'eventuale manomissione di dati durante il trasferimento in rete, usare IPsec (Internet Protocol security) o SMB (Server Message Block) tra il computer che esegue la console di Configuration Manager e il computer di riferimento.|  
|Limitare e monitorare gli utenti amministratori che dispongono del ruolo di sicurezza basato sui ruoli Gestione impostazioni di conformità.|Gli utenti amministratori che dispongono del ruolo **Gestione impostazioni di conformità** possono distribuire elementi di configurazione a tutti i dispositivi e a tutti gli utenti nella gerarchia. Gli elementi di configurazione possono essere molto potenti. Possono, ad esempio, includere script ed eseguire la riconfigurazione del Registro di sistema.|  

## <a name="privacy-information-for-compliance-settings"></a>Informazioni sulla privacy per le impostazioni di conformità  
 È possibile usare le impostazioni di conformità per valutare la conformità dei dispositivi client con gli elementi di configurazione distribuiti nelle linee di base di configurazione. Alcune impostazioni non conformi possono essere corrette automaticamente. Le informazioni sulla conformità vengono inviate al server del sito dal punto di gestione e memorizzate nel database del sito. Le informazioni vengono crittografate quando i dispositivi le inviano al punto di gestione, ma non vengono memorizzate in forma crittografata nel database del sito. Le informazioni vengono conservate nel database fino alla relativa eliminazione nell'ambito dell'attività di manutenzione del sito **Elimina dati di gestione configurazione obsoleti** eseguita ogni 90 giorni. È possibile configurare l'intervallo di eliminazione. Le informazioni sulla conformità non vengono inviate a Microsoft.  

 Per impostazione predefinita, i dispositivi non valutano le impostazioni di conformità. È anche necessario configurare gli elementi di configurazione e le linee di base di configurazione prima di distribuirli ai dispositivi.  
