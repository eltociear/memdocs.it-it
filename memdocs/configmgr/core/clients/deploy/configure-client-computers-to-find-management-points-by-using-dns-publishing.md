---
title: Configurare i client per l'uso della pubblicazione DNS
titleSuffix: Configuration Manager
description: Configurare i computer client di Configuration Manager per trovare i punti di gestione tramite la pubblicazione DNS.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 03cec407-0f9f-454f-a360-b005af738d29
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d28a8a35f711dcef7e3f9adb6dccbabc4082ab28
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693539"
---
# <a name="configure-client-computers-to-find-management-points-by-using-dns-publishing"></a>Configurare i computer client per trovare i punti di gestione tramite la pubblicazione DNS

*Si applica a: Configuration Manager (Current Branch)*

I client in Configuration Manager devono individuare un punto di gestione per completare l'assegnazione del sito e per rimanere gestiti come processo in corso. Servizi di dominio Active Directory fornisce ai client della rete Intranet il metodo più sicuro per individuare i punti di gestione. Tuttavia, se i client non possono utilizzare questo metodo di individuazione del servizio (ad esempio, non hanno esteso lo schema di Active Directory oppure i client provengono da un gruppo di lavoro), utilizzare la pubblicazione DNS come metodo alternativo di individuazione del servizio preferito.  

> [!NOTE]  
>  Quando si installa il client per Linux e UNIX, è necessario specificare un punto di gestione da utilizzare come punto di contatto iniziale. Per informazioni su come installare il client per Linux e UNIX, vedere [Come distribuire i client nei server UNIX e Linux](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  

 Prima di utilizzare la pubblicazione DNS per i punti di gestione, assicurarsi che i server DNS nella Intranet dispongano dei record di risorse di individuazione del servizio (SRV RR) e dei relativi record di risorse dell'host (A o AAA) per i punti di gestione del sito. I record di risorse di posizione del servizio possono essere creati automaticamente da Configuration Manager o manualmente dall'amministratore DNS che crea i record in DNS.  

 Per altre informazioni sulla pubblicazione DNS come metodo di posizione del servizio per i client di Configuration Manager, vedere [Informazioni su come i client trovano i servizi e le risorse del sito per Configuration Manager](../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

 Per impostazione predefinita, i client cercano il DNS per i punti di gestione all'interno del loro dominio DNS. Tuttavia, se non sono presenti punti di gestione pubblicati nel dominio dei client, è necessario configurare i client manualmente con un suffisso DNS del punto di gestione. È possibile configurare il suffisso DNS sui client durante o dopo la loro l'installazione:  

-   Per configurare i client per un suffisso del punto di gestione durante l'installazione del client, configurare le proprietà CCMSetup per Client.msi.  

-   Per configurare i client per un suffisso del punto di gestione dopo aver installato il client, in Pannello di controllo configurare le **Proprietà di Configuration Manager**.  

#### <a name="to-configure-clients-for-a-management-point-suffix-during-client-installation"></a>Per configurare i client per un suffisso del punto di gestione durante l'installazione del client  

- Installare il client con la seguente proprietà Client.msi CCMSetup.:  

  - **DNSSUFFIX=** *&lt;dominio del punto di gestione\>*  

     Se il sito dispone di più punti di gestione e questi si trovano in più di un dominio, specificare un solo dominio. Quando si connettono a un punto di gestione in questo dominio, i client scaricano un elenco di punti di gestione disponibili, tra cui i punti di gestione provenienti da altri domini.  

    Per altre informazioni sulle proprietà della riga di comando CCMSetup, vedere [Informazioni sulle proprietà di installazione del client](../../../core/clients/deploy/about-client-installation-properties.md).  

#### <a name="to-configure-clients-for-a-management-point-suffix-after-client-installation"></a>Per configurare i client per un suffisso del punto di gestione dopo l'installazione del client  

1.  Nel Pannello di controllo del computer client passare a **Configuration Manager**, quindi fare doppio clic su **Proprietà**.  

2.  Nella scheda **Sito** specificare il suffisso DNS di un punto di gestione, quindi fare clic su **OK**.  

     Se il sito dispone di più punti di gestione e questi si trovano in più di un dominio, specificare un solo dominio. Quando si connettono a un punto di gestione in questo dominio, i client scaricano un elenco di punti di gestione disponibili, tra cui i punti di gestione provenienti da altri domini.
