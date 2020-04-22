---
title: Introduzione al risparmio energia
titleSuffix: Configuration Manager
description: Informazioni introduttive sul risparmio energia in Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3ddff2a7-99eb-4ef8-b969-f3f7f24053db
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 400fe3113207217504317eeb8ef8bbce4ab6a298
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696569"
---
# <a name="introduction-to-power-management-in-configuration-manager"></a>Introduzione al risparmio energia in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Il risparmio energia in Configuration Manager soddisfa l'esigenza di molte organizzazioni di monitorare e ridurre il consumo di energia dei computer. Questa funzione per applica impostazioni pertinenti e coerenti ai computer dell'organizzazione sfruttando le funzionalità di risparmio energia di Windows. È possibile applicare ai computer impostazioni di risparmio energia diverse durante le ore lavorative e le ore non lavorative. È possibile, ad esempio, applicare una combinazione per il risparmio di energia più restrittiva durante l'orario non lavorativo. Nei casi in cui i computer devono rimanere sempre accesi, è possibile evitare l'attivazione delle impostazioni di risparmio energia.  

 La funzionalità di risparmio energia in Configuration Manager include diversi report per agevolare l'analisi dei consumi e delle impostazioni di risparmio energia per i computer nell'organizzazione. È anche possibile usare i report per risolvere i problemi relativi al risparmio energia.  

 Per un flusso di lavoro dettagliato della configurazione e dell'uso del risparmio energia, vedere [Elenco di controllo per gli amministratori per il risparmio energia](../../../../core/clients/manage/power/administrator-checklist-for-power-management.md).  

> [!IMPORTANT]  
>  Il risparmio energia di Configuration Manager non è supportato per le macchine virtuali. Non è possibile applicare combinazioni per il risparmio di energia alle macchine virtuali, né ottenere da queste dati o report relativi al risparmio energia.  

## <a name="the-power-management-workflow"></a>Flusso di lavoro del risparmio energia  
 Per pianificare e implementare il risparmio energia in Configuration Manager, eseguire le tre fasi seguenti.  

### <a name="monitoring-and-planning-phase"></a>Fase di monitoraggio e pianificazione  
 Il risparmio energia usa l'inventario hardware di Configuration Manager per raccogliere dati sull'utilizzo dei computer presenti presso il sito e sulle impostazioni per il risparmio energia attive per i computer stessi. Per analizzare questi dati e determinare le impostazioni di risparmio energia ottimali per i computer sono disponibili numerosi report. Ad esempio, durante la fase di monitoraggio e pianificazione del flusso di lavoro della funzionalità di risparmio energia è possibile creare raccolte basate sui dati del report **Funzionalità alimentazione** e usare tali dati per identificare i computer che non dispongono della funzionalità di risparmio energia. È quindi possibile escludere questi computer dalla gestione del risparmio energia.  

> [!IMPORTANT]  
>  Per applicare combinazioni per il risparmio di energia ai computer del sito attendere di aver raccolto e analizzato i dati relativi al risparmio energia dei computer client. Se si applicano nuove impostazioni di risparmio energia ai computer senza prima esaminare le impostazioni esistenti, si potrebbe riscontrare un aumento del consumo di energia.  

### <a name="enforcement-phase"></a>Fase di imposizione  
 Il risparmio energia consente di creare combinazioni per il risparmio di energia che sarà possibile applicare alle raccolte di computer del sito. Queste combinazioni eseguono la configurazione delle impostazioni di risparmio energia di Windows nei computer. È possibile usare le combinazioni per il risparmio di energia incluse in Configuration Manager oppure è possibile configurare combinazioni personalizzate. È possibile usare i dati relativi al risparmio energia raccolti durante la fase di monitoraggio e pianificazione come linea di base per la valutazione del risparmio energia dopo l'applicazione di una combinazione per il risparmio di energia ai computer. Per altre informazioni, vedere [Elenco di controllo per gli amministratori per il risparmio energia](../../../../core/clients/manage/power/administrator-checklist-for-power-management.md).  

### <a name="compliance-phase"></a>Fase di verifica della conformità  
 Nella fase di verifica della conformità è possibile eseguire report che consentono di valutare il consumo di energia e il risparmio sui costi dell'energia all'interno dell'organizzazione. È anche possibile eseguire report che descrivono i miglioramenti relativi alla quantità di CO2 generata dai computer. Sono disponibili anche report che consentono di verificare la corretta applicazione delle impostazioni del risparmio energia ai computer e di risolvere i problemi della funzionalità di risparmio energia.  
