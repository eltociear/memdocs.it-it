---
title: Configurazioni supportate
titleSuffix: Configuration Manager
description: Identificare le configurazioni e i requisiti principali in modo da pianificare, distribuire e manutenere una distribuzione di Configuration Manager funzionale.
ms.date: 10/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 45a10878-ff48-4318-9c6d-c014b38a4039
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 09618acc1c0950c3eaae79cca59fcf71dc7ef61e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688519"
---
# <a name="supported-configurations-for-configuration-manager"></a>Configurazioni supportate per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Come soluzione locale, Configuration Manager usa server, client, configurazioni di rete e altri prodotti quali Microsoft Intune, SQL Server e Azure.

Le informazioni in questo e negli argomenti seguenti sono fondamentali per identificare le configurazioni, i requisiti e limitazioni principali per poter pianificare, distribuire e mantenere una distribuzione di Configuration Manager funzionale.  Queste informazioni sono specifiche per l'infrastruttura per i siti, le gerarchie e i dispositivi gestiti di Configuration Manager.

Quando una funzionalità di Configuration Manager richiede configurazioni più specifiche, queste informazioni vengono incluse nella documentazione specifica della funzionalità e vanno ad aggiungersi ai dettagli delle configurazioni generiche.  

 I prodotti e le tecnologie descritti negli argomenti seguenti sono supportati da Configuration Manager. Il loro inserimento in questo contesto, tuttavia, non implica un'estensione del normale ciclo di vita del supporto per il singolo prodotto. I prodotti che non rientrano nel ciclo di vita del supporto non sono supportati per l'uso con Configuration Manager. Sono inclusi tutti i prodotti coperti dal programma [ESU sugli aggiornamenti della sicurezza estesa](https://support.microsoft.com/help/4497181/lifecycle-faq-extended-security-updates). Per altre informazioni sui cicli di vita del supporto Microsoft, visitare il sito Web [Ciclo di vita del supporto Microsoft](https://go.microsoft.com/fwlink/p/?LinkId=208270) . Per altre informazioni sugli aggiornamenti della sicurezza estesa in Configuration Manager, vedere [Versioni dei sistemi operativi per client e dispositivi supportate da Configuration Manager](supported-operating-systems-for-clients-and-devices.md#bkmk_ESU).

> [!NOTE]  
>  Per informazioni sui criteri del ciclo di vita del supporto Microsoft, vedere le domande frequenti nel sito [Criteri relativi al ciclo di vita Microsoft](https://go.microsoft.com/fwlink/p/?LinkId=31976).  

 I prodotti e le versioni di prodotto non elencati negli argomenti seguenti non sono supportati con Configuration Manager a meno che non siano annunciati nel blog [Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/).  In alcuni casi è possibile che i contenuti del blog anticipino un aggiornamento alla documentazione.


-  [Numeri di ridimensionamento e scalabilità](../../../core/plan-design/configs/size-and-scale-numbers.md)  
Informazioni su quanti siti, quanti ruoli del sistema del sito per sito e quanti client o dispositivi sono supportati in diverse progettazioni di gerarchie di Configuration Manager.

-  [Prerequisiti del sito e del sistema del sito per System Center Configuration Manager](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)  
Informazioni sulle configurazioni necessarie in un server Windows per supportare diversi tipi di siti e di ruoli del sistema del sito.

-  [Sistemi operativi supportati per i server del sistema del sito di System Center Configuration Manager](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)  
Informazioni su quali sistemi operativi è possibile usare come server del sito o server del sistema del sito.

-  [Sistemi operativi supportati per client e dispositivi](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)  
Informazioni su quali sistemi operativi è possibile gestire con Configuration Manager, compresi Windows, Windows Embedded, Linux e UNIX, Mac e dispositivi mobili.

-  [Sistemi operativi supportati per le console](../../../core/plan-design/configs/supported-operating-systems-consoles.md)  
Informazioni su quali sistemi operativi possono ospitare la console di Configuration Manager per offrire un punto di accesso per la gestione della distribuzione.  

-  [Supporto per le versioni di SQL Server](../../../core/plan-design/configs/support-for-sql-server-versions.md)  
Informazioni sulle versioni di SQL Server che possono ospitare il database del sito e il database per la creazione di report, nonché sulle configurazioni obbligatorie e facoltative che è possibile usare.

-  [Opzioni di disponibilità elevata](../../servers/deploy/configure/high-availability-options.md)  
Informazioni sulle opzioni che è possibile implementare quando si progetta l'ambiente per mantenere un livello di disponibilità del servizio elevato per la distribuzione di Configuration Manager.

-  [Recommended hardware](../../../core/plan-design/configs/recommended-hardware.md) (Hardware consigliato)  
Informazioni sulle linee guida per identificare le configurazioni e i componenti hardware appropriati per l'hosting dei siti e dei servizi principali di Configuration Manager.

-  [Supporto per i domini di Active Directory](../../../core/plan-design/configs/support-for-active-directory-domains.md)  
Informazioni sulle configurazioni di dominio di Active Directory supportate, richieste e supportate da Configuration Manager.

-  [Supporto per le funzionalità e le reti Windows](../../../core/plan-design/configs/support-for-windows-features-and-networks.md)  
Informazioni sulle tecnologie Windows supportate (ad esempio BranchCache e la deduplicazione dati) e sulle limitazioni nel caso in cui debbano essere usate con Configuration Manager.

-  [Supporto per gli ambienti di virtualizzazione](../../../core/plan-design/configs/support-for-virtualization-environments.md)  
Informazioni su come usare le tecnologie per le macchine virtuali supportate.
