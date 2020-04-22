---
title: Usare i servizi cloud
titleSuffix: Configuration Manager
description: Il provisioning delle risorse cloud per Configuration Manager consente di integrare l'infrastruttura locale.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 24fca61e-9cdb-447a-ad7a-f4d2e4fd6704
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c191debd77502f7d594a77eb3bd0c50cd6854f66
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706699"
---
# <a name="use-cloud-services-with-configuration-manager"></a>Usare i servizi cloud con Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Configuration Manager supporta varie opzioni basate su cloud. Queste opzioni possono integrare l'infrastruttura locale e consentono di risolvere problemi aziendali quali:  

-   Come gestire la strategia BYOD usando Intune per la gestione dei dispositivi mobili.  

-   Come specificare risorse di contenuto per client isolati o risorse nella Intranet, all'esterno del firewall aziendale, usando i punti di distribuzione basati su cloud.  

-   Come aumentare il numero di istanze per l'infrastruttura quando l'hardware fisico non è disponibile o non è logicamente incluso per supportare le esigenze, usando macchine virtuali di Microsoft Azure.  

Anche se non è necessario eseguire il provisioning delle risorse cloud prima di distribuire Configuration Manager, può essere utile comprendere queste opzioni prima di addentrarsi troppo nella pianificazione della struttura della gerarchia. L'uso delle risorse cloud potrebbe ridurre costi e tempi risolvendo al contempo problemi aziendali non risolvibili con l'infrastruttura locale.  

## <a name="cloud-based-resources-you-can-use-with-configuration-manager"></a>Risorse basate su cloud che è possibile usare con Configuration Manager  
 Dal momento che ogni opzione ha requisiti diversi, analizzare ciascuna in modo più approfondito per comprendere i prerequisiti univoci, le limitazioni e la possibilità di costi aggiuntivi in base all'uso.  

-   Per informazioni sui punti di distribuzione basati su cloud, vedere [Installare punti di distribuzione basati su cloud](../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md).

-   Per altre informazioni su Azure, vedere [Azure](https://go.microsoft.com/fwlink/p/?LinkId=262965) in MSDN Library.  

### <a name="azure-virtual-machines-for-cloud-based-infrastructure"></a>Macchine virtuali di Azure (per l'infrastruttura basata su cloud)  
 Configuration Manager supporta l'uso di computer eseguiti in macchine virtuali di Azure analogamente a quando vengono eseguiti in locale all'interno della rete fisica aziendale. È possibile usare le macchine virtuali di Azure negli scenari seguenti:  

-   **Scenario 1:** è possibile eseguire Configuration Manager in una macchina virtuale e usarlo per gestire i client installati in altre macchine virtuali.  

-   **Scenario 2:** è possibile eseguire Configuration Manager in una macchina virtuale e usarlo per gestire i client che non vengono eseguiti in Azure.  

-   **Scenario 3:** è possibile eseguire diversi ruoli del sistema del sito di Configuration Manager nelle macchine virtuali e allo stesso tempo eseguire altri ruoli nella rete aziendale fisica con connettività di rete appropriata per le comunicazioni.  

Gli stessi requisiti per reti, sistemi operativi e requisiti hardware che si applicano all'installazione di Configuration Manager nella rete aziendale fisica si applicano anche all'installazione di Configuration Manager in Azure.  

È necessaria una sottoscrizione di Azure per usare macchine virtuali di Azure. I costi variano in base al numero di macchine virtuali usate, alla relativa configurazione e all'uso di risorse basate su cloud.  

I siti e i client di Configuration Manager eseguiti in macchine virtuali di Azure sono soggetti agli stessi requisiti di licenza delle installazioni locali.  

### <a name="azure-services-for-cloud-based-distribution-points"></a>Servizi di Azure per i punti di distribuzione basati su cloud  
 È possibile usare un servizio di Azure per ospitare un punto di distribuzione di Configuration Manager, definito punto di distribuzione basato su cloud. È possibile [usare i punti di distribuzione basati su cloud con Configuration Manager](../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md) insieme ai punti di distribuzione locali e ai punti di distribuzione distribuiti nelle macchine virtuali di Azure.  

 Questa situazione è diversa rispetto all'uso di una macchina virtuale di Azure, in cui si distribuisce un ruolo del sistema del sito. Punti di distribuzione basati su cloud:  

-   Vengono eseguiti come servizio in Azure, non in una macchina virtuale.  

-   Vengono ridimensionati automaticamente per soddisfare l'aumento delle richieste di contenuto dai client.  

-   Supportano client su Internet e intranet.  

È necessaria una sottoscrizione di Azure per usare Azure per ospitare punti di distribuzione. I costi variano in base alla quantità di dati trasferiti da e verso il servizio.  

### <a name="additional-configuration-manager-capabilities"></a>Funzionalità aggiuntive di Configuration Manager  
 Alcune funzionalità di Configuration Manager possono connettersi ai servizi basati su cloud, ad esempio:  

-   Windows Server Update Services (WSUS).  

-   Servizio cloud di Configuration Manager per scaricare gli aggiornamenti per Configuration Manager.  

Queste funzionalità aggiuntive non richiedono una sottoscrizione di Azure. Non è necessario configurare connessioni specifiche, certificati o servizi nel cloud. ma vengono gestite automaticamente da Configuration Manager. È sufficiente verificare che i dispositivi e i sistemi del sito applicabili possano accedere agli URL basati su Internet.  

##  <a name="security-for-cloud-based-services"></a><a name="BKMK_CloudSec"></a> Sicurezza dei servizi basati su cloud  
 Configuration Manager usa i certificati per il provisioning e l'accesso al contenuto di Azure e per la gestione dei servizi usati. Configuration Manager crittografa i dati archiviati in Azure, ma non introduce ulteriori controlli su dati o sicurezza oltre a quelli forniti da Azure.  

 Per altre informazioni, vedere i dettagli relativi ai diversi scenari di risorse basate su cloud. È anche possibile visualizzare gli argomenti seguenti per la sicurezza di Azure:  

-   [Azure: gestione degli account di protezione in Azure](https://go.microsoft.com/fwlink/p/?LinkId=262968)  

-   [Panoramica sulla protezione di Azure](https://go.microsoft.com/fwlink/p/?LinkId=262970)  

-   [Superare gli incroci di protezione nella migrazione cloud](https://go.microsoft.com/fwlink/p/?LinkId=262971)  

-   [Protezione dei dati in Azure (parte 1 di 2)](https://go.microsoft.com/fwlink/p/?LinkId=262974)  
