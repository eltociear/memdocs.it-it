---
title: Prerequisiti per il controllo remoto
titleSuffix: Configuration Manager
description: Informazioni sui prerequisiti per il controllo remoto in Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: c1b2057e-b74f-43fa-a293-763a8f866d3d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f19f8799dd90fc61c0bfeeee1dc60125ba491fef
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696419"
---
# <a name="prerequisites-for-remote-control-in-configuration-manager"></a>Prerequisiti per il controllo remoto in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Il controllo remoto in Configuration Manager ha dipendenze esterne e dipendenze all'interno del prodotto.  

## <a name="dependencies-external-to-configuration-manager"></a>Dipendenze esterne a Configuration Manager  

|Dipendenza|Altre informazioni|  
|----------------|----------------------|  
|Driver della scheda video del computer|Assicurarsi che nei computer client sia installato il driver della scheda video più aggiornato per garantire prestazioni di controllo remoto ottimali.|  

 I dispositivi che eseguono Windows Embedded, Windows Embedded per punto di servizio e Windows Fundamentals per PC legacy non supportano il visualizzatore controllo remoto, ma supportano il client di controllo remoto.  

 Il controllo remoto di Configuration Manager non può essere usato per amministrare in remoto computer client che eseguono Systems Management Server 2003 o Configuration Manager 2007.  

> [!NOTE]  
>  Nessun servizio Windows è necessario come una dipendenza esterna per il controllo remoto.  

### <a name="supported-operating-systems-for-the-remote-control-viewer"></a>Sistemi operativi supportati per il visualizzatore controllo remoto  
Il visualizzatore controllo remoto è supportato in tutti i sistemi operativi supportati per la console di Configuration Manager. Per altre informazioni, vedere [Configurazioni supportate per le console di Configuration Manager](../../../../core/plan-design/configs/supported-operating-systems-consoles.md).   

## <a name="configuration-manager-dependencies"></a>Dipendenze di Configuration Manager  

|Dipendenza|Altre informazioni|  
|----------------|----------------------|  
|Il controllo remoto deve essere abilitato per i client|Per impostazione predefinita, il controllo remoto non è abilitato quando si installa Configuration Manager. Per informazioni su come abilitare e configurare il controllo remoto, vedere [Configurazione del controllo remoto](../../../../core/clients/manage/remote-control/configuring-remote-control.md).|  
|Punto di Reporting Services|Prima di poter eseguire report per il controllo remoto, è necessario installare il ruolo del sistema del sito del punto di Reporting Services. Per altre informazioni, vedere [Introduzione ai report](../../../servers/manage/introduction-to-reporting.md).|  
|Autorizzazioni di sicurezza per la gestione del controllo remoto|Per accedere alle risorse della raccolta e avviare una sessione di controllo remoto dalla console di Configuration Manager: autorizzazioni **Lettura**, **Leggi risorsa** e **Controllo remoto** per l'oggetto **Raccolta**.<br /><br /> Il ruolo di sicurezza **Operatore strumenti remoti** include queste autorizzazioni necessarie per gestire il controllo remoto in Configuration Manager.<br /><br /> Per altre informazioni, vedere [Configurare l'amministrazione basata su ruoli per Configuration Manager](../../../../core/servers/deploy/configure/configure-role-based-administration.md).<br /><br /> Inoltre, agli utenti autorizzati alla visualizzazione è necessario concedere l'autorizzazione all'uso del controllo remoto aggiungendo tali utenti all'elenco **Visualizzatori autorizzati di controllo remoto e assistenza remota** nelle impostazioni client **Strumenti remoti**.
