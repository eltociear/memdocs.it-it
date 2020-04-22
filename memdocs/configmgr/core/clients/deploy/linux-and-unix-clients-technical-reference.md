---
title: Servizi componenti client e comandi UNIX/Linux
titleSuffix: Configuration Manager
description: Informazioni sui servizi componenti e sui comandi nei client Linux e UNIX in Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e5a8c79f-5791-49c5-8055-086d742e5559
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: de564595ce51a336b5f11d4050928fa812269601
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693889"
---
# <a name="linux-and-unix-clients-component-services-and-commands-for-configuration-manager"></a>Servizi componenti e comandi dei client Linux e UNIX per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

> [!Important]  
> A partire dalla versione 1902, Configuration Manager non supporta i client Linux o UNIX. 
> 
> Per la gestione dei server Linux, è possibile usare la gestione di Microsoft Azure. Le soluzioni di Azure includono un ampio supporto per Linux che nella maggior parte dei casi supera le funzionalità di Configuration Manager, inclusa la gestione end-to-end delle patch per Linux.


 Nella tabella seguente sono riportati i servizi componenti client del client di Configuration Manager per Linux e UNIX.  

|Nome file|Altre informazioni|  
|---------------|----------------------|  
|ccmexec.bin|Questo servizio è simile al servizio ccmexc in un client basato su Windows. È responsabile di tutte le comunicazioni con i ruoli del sistema del sito di Configuration Manager e comunica anche con il servizio omiserver.bin per raccogliere l'inventario hardware dal computer locale.<br /><br /> Per un elenco di argomenti della riga di comando supportati, eseguire `ccmexec -h`|  
|omiserver.bin|Questo servizio è il server CIM. Il server CIM fornisce un framework per i moduli software plug-in denominati provider. I provider interagiscono con le risorse dei computer Linux e UNIX e raccolgono i dati di inventario hardware. Ad esempio, il **provider process** per Linux computer raccoglie i dati associati ai processi del sistema operativo Linux.|  

 I seguenti comandi dell'elenco di tabelle che è possibile utilizzare per avviare, arrestare o riavviare i servizi client (CCMExec e omiserver) in ogni versione di Linux o UNIX. Quando si avvia o arresta il servizio ccmexec, viene avviato o arrestato anche il servizio omiserver.  

|Sistema operativo|Comandi|  
|----------------------|--------------|  
|Universal Agent<br /><br /> RHEL 4 e SLES 9|Avvia: `/etc/init d/ccmexecd start`<br /><br /> Arresta: `/etc/init d/ccmexecd stop`<br /><br /> Riavvia: `/etc/init d/ccmexecd restart`|  
|Solaris 9|Avvia: `/etc/init d/ccmexecd start`<br /><br /> Arresta: `/etc/init d/ccmexecd stop`<br /><br /> Riavvia: `/etc/init d/ccmexecd restart`|  
|Solaris 10|Avvia:<br /><br /> `svcadm enable -s svc:/application/management/omiserver`<br /><br /> `svcadm enable -s svc:/application/management/ccmexecd`<br /><br /> Arresta:<br /><br /> `svcadm disable -s svc:/application/management/ccmexecd`<br /><br /> `svcadm disable -s svc:/application/management/omiserver`|  
|Solaris 11|Avvia:<br /><br /> `svcadm enable -s svc:/application/management/omiserver`<br /><br /> `svcadm enable -s svc:/application/management/ccmexecd`<br /><br /> Arresta:<br /><br /> `svcadm disable -s svc:/application/management/ccmexecd`<br /><br /> `svcadm disable -s svc:/application/management/omiserver`|  
|AIX|Avvia:<br /><br /> `startsrc -s omiserver`<br /><br /> `startsrc -s ccmexec`<br /><br /> Arresta:<br /><br /> `stopsrc -s ccmexec`<br /><br /> `stopsrc -s omiserver`|  
|HP-UX|Avvia: `/sbin/init.d/ccmexecd start`<br /><br /> Arresta: `/sbin/init.d/ccmexecd stop`<br /><br /> Riavvia: `/sbin/init.d/ccmexecd restart`|  
