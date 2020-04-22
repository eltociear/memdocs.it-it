---
title: Prerequisiti per Asset Intelligence
titleSuffix: Configuration Manager
description: Informazioni sui prerequisiti per Asset Intelligence in Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 23ab4f94-7bfe-436e-8a6a-029409a2730c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: dfed0f2c2e8149abb05d4b21047d4d494f034e53
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695009"
---
# <a name="prerequisites-for-asset-intelligence-in-configuration-manager"></a>Prerequisiti per l'Asset Intelligence in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Asset Intelligence in Configuration Manager ha dipendenze esterne e dipendenze all'interno del prodotto.  

## <a name="dependencies-external-to-configuration-manager"></a>Dipendenze esterne a Configuration Manager  
 La tabella seguente elenca le dipendenze di Asset Intelligence esterne a Configuration Manager.  

|Dipendenza|Altre informazioni|  
|----------------|----------------------|  
|Controllo dei prerequisiti degli eventi di accesso con esito positivo|Quattro report di Asset Intelligence visualizzano informazioni raccolte dai registri eventi di sicurezza di Windows nei computer client. Se le impostazioni del registro eventi di sicurezza non sono configurate in modo da registrare tutti gli eventi di accesso con esito positivo, questi report non contengono dati anche se è abilitata la classe di report appropriata per l'inventario hardware.<br /><br /> I seguenti report di Asset Intelligence dipendono dalle informazioni del registro eventi di sicurezza di Windows raccolte:<br /><br /> Hardware 03A - Utenti computer primario<br />Hardware 03B - Computer per un utente console primario specifico<br />Hardware 04A - Computer condivisi (multiutente)<br />Hardware 05A - Utenti console in un computer specifico<br /><br /> Per abilitare Hardware Inventory Client Agent per l'esecuzione dell'inventario delle informazioni necessarie per supportare questi report, è prima necessario modificare le impostazioni del registro eventi di sicurezza di Windows nei client in modo da registrare tutti gli eventi di accesso con esito positivo e abilitare la classe di report per l'inventario hardware **SMS_SystemConsoleUser** . Per altre informazioni sulla modifica delle impostazioni del registro eventi di sicurezza per registrare tutti gli eventi di accesso con esito positivo, vedere [Attivare il controllo degli eventi di accesso riusciti](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md#BKMK_EnableSuccessLogonEvents).|  

> [!NOTE]  
>  La classe di report per l'inventario hardware **SMS_SystemConsoleUser** conserva i dati relativi agli eventi di accesso con esito positivo solo per i 90 giorni precedenti del registro eventi di sicurezza, indipendentemente dalla lunghezza del registro. Se il registro eventi di sicurezza contiene dati per meno di 90 giorni, viene letto l'intero registro.  

## <a name="dependencies-internal-to-configuration-manager"></a>Dipendenze interne a Configuration Manager  
 La tabella seguente elenca le dipendenze di Asset Intelligence interne a Configuration Manager.  

|Dipendenza|Altre informazioni|  
|----------------|----------------------|  
|Prerequisiti agente client|I report di Asset Intelligence si basano su informazioni relative ai client ottenute tramite report di inventario di hardware e software dei client. Per ottenere le informazioni necessarie per tutti i report di Asset Intelligence, è necessario abilitare gli agenti client seguenti:<br /><br /> Hardware Inventory Client Agent<br />Agente client controllo software|  
|Dipendenze di Hardware Inventory Client Agent|Per raccogliere i dati di inventario necessari per alcuni report di Asset Intelligence è necessario abilitare Hardware Inventory Client Agent. Inoltre, alcune classi di report per l'inventario hardware di Asset Intelligence devono essere abilitate nei computer server del sito primario.<br /><br /> Per informazioni sull'abilitazione di Hardware Inventory Client Agent, vedere [Come estendere l'inventario hardware](../../../../core/clients/manage/inventory/extend-hardware-inventory.md).|  
|Dipendenze dell'agente client controllo software|Un certo numero di report software di Asset Intelligence si basa sui dati dell'agente client controllo software. Per informazioni sull'abilitazione dell'Agente client controllo software, vedere [Monitorare l'utilizzo delle app con il controllo software](../../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).<br /><br /> I dati dei report di Asset Intelligence seguenti si basano sull'agente client controllo software:<br /><br /> Software 07A - programmi eseguibili usati di recente per numero di computer<br />Software 07B - computer che hanno usato di recente un programma eseguibile specifico<br />Software 07C - programmi eseguibili usati di recente in un computer specifico<br />Software 08A - programmi eseguibili usati di recente per numero di utenti<br />Software 08B - utenti che hanno usato di recente un programma eseguibile specifico<br />Software 08C - programmi eseguibili usati di recente da un utente specifico|  
|Prerequisiti delle classi di report per l'inventario hardware di Asset Intelligence|I report di Asset Intelligence in Configuration Manager dipendono da classi di report di inventario hardware specifiche. Finché le classi di report per l'inventario hardware sono abilitate e i client creano report per l'inventario hardware in base a queste classi, i report di Asset Intelligence associati non contengono dati. Per supportare i requisiti dei report di Asset Intelligence è possibile abilitare le classi di report per l'inventario hardware seguenti:<br /><br /> -   SMS_SystemConsoleUsage<sup>1</sup><br />-   SMS_SystemConsoleUser<sup>1</sup><br />SMS_InstalledSoftware<br />SMS_AutoStartSoftware<br />SMS_BrowserHelperObject<br />Win32_USBDevice<br />SMS_InstalledExecutable<br />SMS_SoftwareShortcut<br />SoftwareLicensingService<br />SoftwareLicensingProduct<br />SMS_SoftwareTag<br /><br /> <sup>1</sup> Per impostazione predefinita, le classi di report per l'inventario hardware **SMS_SystemConsoleUsage** e **SMS_SystemConsoleUser** sono abilitate.<br /><br /> È possibile modificare le classi di report di inventario hardware di Asset Intelligence nell'area di lavoro **Asset e conformità** della console di Configuration Manager, facendo clic sul nodo **Asset Intelligence**. Per altre informazioni, vedere la sezione [Abilitare le classi di report di inventario hardware di Asset Intelligence](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md#BKMK_EnableAssetIntelligence) nell'argomento [Configurazione di Asset Intelligence](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).|  
|Punto di Reporting Services|Perché sia possibile visualizzare i report degli aggiornamenti software, il ruolo del sistema del sito del punto di Reporting Services deve essere installato. Per altre informazioni su come creare un punto di Reporting Services, vedere [Configurazione della creazione di report in Configuration Manager](https://go.microsoft.com/fwlink/p/?LinkId=232661).|  
