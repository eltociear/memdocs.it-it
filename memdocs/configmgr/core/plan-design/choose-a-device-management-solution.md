---
title: Scegliere una soluzione di gestione dei dispositivi
titleSuffix: Configuration Manager
description: Informazioni sulle soluzioni offerte da Microsoft per la gestione di PC, server e dispositivi.
ms.date: 01/24/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 24633725-791a-4df7-8dce-2c24c1a19a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 877345e64045530193a4cdd735cdd399235b90c7
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700266"
---
# <a name="choose-a-device-management-solution"></a>Scegliere una soluzione di gestione dei dispositivi

Microsoft offre diverse soluzioni per la gestione di PC, server e dispositivi. Queste soluzioni sono disponibili in locale, basate sul cloud o una combinazione di entrambi. Scegliere la soluzione adatta ai requisiti aziendali della propria organizzazione. Basare la decisione sulle piattaforme di dispositivi da gestire e sulle funzionalità di gestione necessarie.

## <a name="overview"></a>Panoramica

Sono disponibili numerose soluzioni Microsoft che rappresentano la scelta ottimale in scenari diversi. Non è necessario sceglierne solo una.

- Per un'organizzazione di piccole dimensioni, uno strumento come Windows Admin Center potrebbe rivelarsi la scelta più appropriata.
- Circa il 75% delle organizzazioni IT usa Configuration Manager per gestire i propri dispositivi.
- Microsoft Azure offre diverse soluzioni basate sul cloud o in locale con Azure Stack destinate principalmente alla gestione del server.
- Microsoft Intune offre la gestione cloud dei client.
- È possibile combinare Configuration Manager e Intune con la co-gestione.

La tabella seguente consente di confrontare queste tecnologie di gestione:

|  | Solo cloud | Collegata al cloud | Infrastruttura locale | Disconnesso |
|---------|---------|---------|---------|---------|
| **Host Hyper-V** | Non applicabile | - Azure Stack<br/> - Windows Admin Center<br/> - Virtual Machine Manager | - Azure Stack<br/> - Windows Admin Center<br/> - Virtual Machine Manager | - Azure Stack<br/> - Windows Admin Center<br/> - Virtual Machine Manager |
| **Windows Server** | - Gestione Azure<br/> - Configuration Manager | - Gestione Azure<br/> - Configuration Manager | - Gestione Azure<br/> - Configuration Manager | Configuration Manager |
| **Server Linux** | Gestione Azure | Gestione Azure | Gestione Azure |  |
| **Windows 10** | - Intune<br/> - Configuration Manager | - Intune<br/> - Configuration Manager | - Intune<br/> - Configuration Manager | Configuration Manager |
| **Windows 7 o 8.1** | Configuration Manager | Configuration Manager | Configuration Manager | Configuration Manager |
| **Desktop virtuale Windows** | Configuration Manager | Non applicabile | Non applicabile | Non applicabile |

Per altre informazioni, vedere gli articoli seguenti:

- [Che cos'è Azure Stack?](/azure-stack/operator/azure-stack-overview)
- [Che cos'è Windows Admin Center?](/windows-server/manage/windows-admin-center/understand/what-is)
- [Descrizione di Virtual Machine Manager](/system-center/vmm/overview)
- [Prodotti di gestione Azure](/azure/)
- [Informazioni su Desktop virtuale Windows](/azure/virtual-desktop/overview)

Per altre informazioni sulle soluzioni Configuration Manager e Intune, passare alla sezione successiva.

## <a name="client-management"></a>Gestione dei client

In questa sezione vengono confrontate le quattro soluzioni di gestione client seguenti:

- [Client di Configuration Manager](#bkmk_sccm)
- [Gestione di dispositivi mobili (MDM) locale con Configuration Manager](#bkmk_opmdm)
- [Co-gestione con Microsoft Intune](#bkmk_comanage)
- [Microsoft Exchange](#bkmk_opmdm)

È possibile usare queste soluzioni da sole o in combinazione. È possibile ad esempio usare l'approccio alla gestione basata su client per gestire i computer e i server dell'organizzazione e usare anche la co-gestione per gestire i portatili basati su Internet. Combinando i due approcci in questo modo, è possibile coprire tutte le esigenze di gestione dei dispositivi.  

Sono disponibili anche due tabelle che consentono di confrontare le soluzioni di gestione in base ai fattori seguenti:

- [Piattaforme supportate](#bkmk_comp1)
- [Funzionalità di gestione](#bkmk_comp2)

### <a name="configuration-manager-client"></a><a name="bkmk_sccm"></a> Client di Configuration Manager  

Questa opzione richiede l'installazione del client di Configuration Manager nei dispositivi. Fornisce la maggior parte delle funzionalità per la gestione di PC, server e altri dispositivi nell'ambiente in uso.

Per altre informazioni, vedere [Metodi di installazione client](../clients/deploy/plan/client-installation-methods.md).  

### <a name="on-premises-mdm"></a><a name="bkmk_opmdm"></a> Software MDM locale  

Questa opzione usa le funzionalità di gestione dei dispositivi incorporate in Windows 10. Anche se non è completa come la gestione basata su client, la gestione dei dispositivi mobili locale offre un approccio più semplice. Usa le risorse di Configuration Manager in locale per gestire i dispositivi.  

Per altre informazioni, vedere [Gestire i dispositivi mobili con l'infrastruttura locale](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

### <a name="co-management-with-microsoft-intune"></a><a name="bkmk_comanage"></a> Co-gestione con Microsoft Intune

La co-gestione è uno dei modi principali per collegare la distribuzione di Configuration Manager esistente al cloud di Microsoft 365. Consente di gestire dispositivi Windows 10 contemporaneamente tramite Configuration Manager e Microsoft Intune. La co-gestione consente di collegare al cloud gli investimenti esistenti in Configuration Manager tramite l'aggiunta di nuove funzionalità.

Per altre informazioni, vedere [What is co-management?](../../comanage/overview.md) (Informazioni sulla co-gestione).  

### <a name="microsoft-exchange"></a><a name="bkmk_exchange"></a> Microsoft Exchange  

Questa opzione usa il connettore Exchange Server per connettere più server Exchange a Configuration Manager. Consente di centralizzare la gestione dei dispositivi che possono connettersi a Exchange ActiveSync. È possibile configurare le funzionalità di gestione dei dispositivi mobili di Exchange dalla console di Configuration Manager. Le funzionalità di esempio includono la cancellazione dei dati del dispositivo remota e il controllo delle impostazioni per più server Exchange.

Per altre informazioni, vedere [Gestire i dispositivi mobili con Configuration Manager ed Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

### <a name="compare-solutions-by-supported-platforms"></a><a name="bkmk_comp1"></a> Confrontare le soluzioni in base alle piattaforme supportate  

|Piattaforma|Client di Configuration Manager|Software MDM locale|Configuration Manager con Exchange| Intune |
|--------|----------------------------|---------------|-----------------------------------|--------|
|Android| | |sì| sì |
|iOS| | |sì| sì |
|Mac OS X|sì| |sì| sì |
|Windows 10|sì|sì|sì| sì |
|Windows 10 Mobile| |sì|sì| sì |
|Windows (versioni precedenti)|sì| |sì|  |
|Windows Server|sì| |sì|  |
|Windows Embedded|sì| | |  |

Per un elenco completo di piattaforme supportate, vedere gli articoli seguenti:

- [Sistemi operativi supportati per client e dispositivi per Configuration Manager](configs/supported-operating-systems-for-clients-and-devices.md)
- [Configurazione supportate in Intune](/intune/supported-devices-browsers)

Microsoft consiglia di usare Intune per gestire i dispositivi mobili Android, iOS e Windows 10. Per altre informazioni, vedere [Informazioni su Microsoft Intune](/intune/what-is-intune).

### <a name="compare-solutions-by-management-functionality"></a><a name="bkmk_comp2"></a> Confrontare le soluzioni in base alle funzionalità di gestione  

|Funzionalità di gestione|Client di Configuration Manager|Software MDM locale|Configuration Manager con Exchange|  
|--------|----------------------------|---------------|-----------------------------------|  
|Autenticazione reciproca basata su certificati|sì|sì| |
|Installazione client|sì| | |
|Supporto via Internet|sì| | |
|Individuazione|sì| |sì|
|Inventario hardware|sì|sì|sì|
|Inventario software|sì| |sì|
|Impostazioni|sì|sì|sì|
|Distribuzione software|sì|sì| |
|Gestione aggiornamenti software|sì| | |
|Distribuzione del sistema operativo|sì| | |
|Blocco da Configuration Manager|sì|sì| |
|Inserimento in quarantena e blocco da Exchange Server (e Configuration Manager)| | |sì|
|Cancellazione remota| |sì|sì|