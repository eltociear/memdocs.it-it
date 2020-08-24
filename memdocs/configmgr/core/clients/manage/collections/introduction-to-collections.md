---
title: Introduzione alle raccolte
titleSuffix: Configuration Manager
description: Informazioni introduttive sull'uso delle raccolte in Configuration Manager.
ms.date: 05/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d17e1188-d277-438f-9236-db9cd213b421
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4e43f5a36f2a1bf44959b9645c2fb48a22cc71f1
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126774"
---
# <a name="introduction-to-collections-in-configuration-manager"></a>Introduzione alle raccolte in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Le raccolte consentono di organizzare le risorse in unità gestibili. È possibile creare raccolte in base alle esigenze di gestione dei client e per eseguire operazioni su più risorse contemporaneamente. 

La maggior parte delle attività di gestione dipende o richiede l'uso di una o più raccolte. Sebbene sia possibile usare la raccolta predefinita Tutti i sistemi, l'uso di questa raccolta per le attività di gestione non è consigliato. Creare raccolte personalizzate per identificare in modo più specifico i dispositivi o gli utenti per un'attività.  

 Le raccolte predefinite e personalizzate vengono visualizzate nei nodi **Raccolte utenti** e **Raccolte dispositivi** nell'area di lavoro **Asset e conformità** nella console di Configuration Manager.  

 Le raccolte visualizzate di recente sono disponibili nel nodo **Utenti** e nel nodo **Dispositivi** nell'area di lavoro **Asset e conformità**.  

Di seguito sono descritti alcuni esempi di uso delle raccolte:  

|Operazione|Esempio|  
|---------|-------|  
|Raggruppamento di risorse|È possibile creare raccolte per il raggruppamento delle risorse in base alla gerarchia dell'organizzazione.<br /><br /> Ad esempio, si potrebbe creare una raccolta di tutti i computer nell'unità organizzativa (OU) di Active Directory "Sede centrale Milano". Per altre informazioni su come creare questo tipo di raccolta, vedere [Come creare le raccolte](../../../../core/clients/manage/collections/create-collections.md).<br /><br /> Si potrebbe usare questa raccolta per operazioni quali la configurazione delle impostazioni di Endpoint Protection, la configurazione delle impostazioni di risparmio energia per i dispositivi o l'installazione del client di Configuration Manager.|  
|Distribuzione delle applicazioni|È possibile creare una raccolta di tutti i computer in cui non è installato Microsoft Office 365 e quindi distribuirlo in tutti i computer di tale raccolta.<br /><br /> È anche possibile usare i requisiti dell'applicazione per eseguire questa attività. Per altre informazioni, vedere [Come creare applicazioni in Configuration Manager](../../../../apps/deploy-use/create-applications.md).|  
|[Gestione delle impostazioni client](../../../../core/clients/deploy/about-client-settings.md)|Sebbene le impostazioni client predefinite in Configuration Manager siano valide per tutti i dispositivi e tutti gli utenti, è possibile creare impostazioni client personalizzate applicabili a una raccolta di dispositivi o a una raccolta di utenti.<br /><br /> Ad esempio, se si vuole che il controllo remoto sia disponibile in tutti i dispositivi a parte alcuni, configurare impostazioni client predefinite per consentire il controllo remoto e quindi configurare impostazioni client personalizzate che non consentono il controllo remoto e distribuirle alla raccolta dei client che rappresentano l'eccezione. |  
|[Risparmio energia](../power/introduction-to-power-management.md)|È possibile configurare impostazioni di risparmio energia specifiche per ogni raccolta.|  
|[Amministrazione basata su ruoli](../../../../core/servers/deploy/configure/configure-role-based-administration.md)|Usare le raccolte per controllare i gruppi di utenti con accesso a varie funzionalità nella console di Configuration Manager.|  
|[Finestre di manutenzione](../../../../core/clients/manage/collections/use-maintenance-windows.md)|Con le finestre di manutenzione è possibile definire un periodo di tempo in cui eseguire diverse operazioni di Configuration Manager sui membri di una raccolta di dispositivi. |  


## <a name="collection-types-in-configuration-manager"></a>Tipi di raccolta in Configuration Manager  
 Configuration Manager include alcune raccolte predefinite per operazioni comuni ed è anche possibile creare raccolte personalizzate.   

### <a name="built-in-collections"></a>Raccolte predefinite  
 Per impostazione predefinita, Configuration Manager include le raccolte seguenti, che non possono essere modificate.  

|**Nome raccolta**|Descrizione|  
|-------------------------|-----------------|  
|**Tutti i gruppi utente**|Contiene i gruppi di utenti individuati tramite individuazione gruppo di protezione Active Directory.|  
|**Tutti gli utenti**|Contiene gli utenti individuati tramite individuazione utente Active Directory.|  
|**Tutti gli utenti e gruppi utente**|Contiene le raccolte Tutti gli utenti e Tutti i gruppi utente. Questa raccolta contiene l'ambito più grande di risorse utenti e gruppi di utenti.|  
|**Tutti i client desktop e di server**|Contiene i dispositivi desktop e server in cui è installato il client di Configuration Manager. L'appartenenza viene gestita tramite l'individuazione heartbeat.|  
|**Tutti i dispositivi mobili**|Contiene i dispositivi mobili gestiti da Configuration Manager. L'appartenenza è limitata ai dispositivi mobili assegnati correttamente a un sito o individuati dal connettore Exchange Server.|  
|**Tutti i sistemi**|Contiene le raccolte Tutti i client desktop e di server, Tutti i dispositivi mobili, Tutti i computer sconosciuti e tutti i dispositivi mobili registrati da Microsoft Intune. Questa raccolta contiene l'ambito più grande di risorse dispositivi.|  
|**Tutti i computer sconosciuti**|Contiene i record di computer generici per piattaforme di computer multiple. È possibile usare questa raccolta per distribuire un sistema operativo tramite una sequenza di attività e l'avvio PXE, un supporto di avvio o un supporto preinstallato.|  

### <a name="custom-collections"></a>Raccolte personalizzate  
 Quando si crea una raccolta personalizzata in Configuration Manager, l'appartenenza di tale raccolta viene determinata da una o più regole di raccolta, come descritto in [Come creare le raccolte](../../../../core/clients/manage/collections/create-collections.md). 

