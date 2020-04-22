---
title: Interoperabilità della distribuzione del sistema operativo
titleSuffix: Configuration Manager
description: Conoscere i problemi di interoperabilità quando siti diversi di Configuration Manager in un'unica gerarchia usano versioni diverse.
ms.date: 05/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: e327ce38-6c07-4a27-b6eb-7e5bf74ed04b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5931c43f0f8513ea1819e00f4eac7ecfd35dc717
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708079"
---
# <a name="plan-for-os-deployment-interoperability"></a>Pianificare l'interoperabilità della distribuzione del sistema operativo

*Si applica a: Configuration Manager (Current Branch)*

Quando siti diversi di Configuration Manager in un'unica gerarchia usano versioni diverse, alcune funzionalità di Configuration Manager non sono disponibili. In genere, le funzionalità della versione più recente di Configuration Manager non sono accessibili in siti o da client che eseguono una versione precedente. Per altre informazioni, vedere [Interoperabilità tra versioni diverse di Configuration Manager](../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  


## <a name="objects"></a>Oggetti

Quando si aggiorna il sito principale nella gerarchia e quando altri siti nella gerarchia eseguono una versione precedente di Configuration Manager, è necessario considerare gli oggetti seguenti:  

### <a name="client-installation-package"></a>Pacchetto di installazione client  

- L'origine per il pacchetto di installazione client predefinito viene aggiornata automaticamente. Tutti i punti di distribuzione nella gerarchia vengono aggiornati con il nuovo pacchetto di installazione client. Questo comportamento si verifica anche nei punti di distribuzione in siti nella gerarchia di una versione precedente.  

- Non è possibile assegnare client della nuova versione a siti per i quali non è ancora stato eseguito l'aggiornamento alla nuova versione. Assegnazione bloccata nel punto di gestione.  

### <a name="boot-images"></a>Immagini d'avvio  

- Quando si aggiorna il sito principale alla versione più recente di Configuration Manager, esso aggiorna automaticamente le immagini d'avvio predefinite (x86 e x64). L'aggiornamento usa Windows ADK per Windows 10, che include Windows PE 10. I file associati alle immagini d'avvio predefinite vengono aggiornati con i file dell'ultima versione di Configuration Manager. Il sito non aggiorna automaticamente immagini d'avvio personalizzate. È necessario aggiornarle manualmente, incluse le versioni precedenti di Windows PE.  

- Se la gerarchia del sito contiene siti con versioni diverse di Configuration Manager, evitare l'uso di supporto dinamico. Usare invece supporti basati su sito per contattare un punto di gestione specifico. Dopo aver aggiornato tutti i siti alla stessa versione di Configuration Manager, è possibile usare nuovamente il supporto dinamico.

- Verificare che le immagini d'avvio di Configuration Manager più recenti includano le personalizzazioni. Aggiornare quindi tutti i punti di distribuzione nei siti della nuova versione con la versione più recente delle nuove immagini d'avvio.  

### <a name="user-state-migration-tool-usmt"></a>Utilità di migrazione stato utente (USMT)  

Quando si aggiorna il sito principale alla versione più recente di Configuration Manager, esso aggiorna automaticamente il pacchetto USMT predefinito alla versione più recente. I pacchetti USMT personalizzati non vengono aggiornati automaticamente. È necessario aggiornarli manualmente.  

### <a name="new-task-sequence-steps"></a>Nuovi passaggi della sequenza di attività  

Vengono introdotti periodicamente nuovi passaggi di sequenza di attività con le nuove versioni di Configuration Manager. Quando si distribuisce una sequenza di attività con un nuovo passaggio a client meno recenti, il passaggio della sequenza di attività avrà esito negativo. Prima di distribuire una sequenza di attività con un nuovo passaggio, assicurarsi che i client nella raccolta di destinazione siano aggiornati alla nuova versione.  

### <a name="os-deployment-media"></a>Supporti di distribuzione dei sistemi operativi  

Quando il sito viene aggiornato a una nuova versione, aggiornare tutti i supporti con il nuovo pacchetto client di Configuration Manager. Questi tipi di supporto includono i supporti di avvio, di acquisizione, pre-installati e autonomi.

### <a name="third-party-extensions-to-os-deployment"></a>Estensioni di terze parti per la distribuzione del sistema operativo  

Quando si hanno estensioni di terze parti per la distribuzione del sistema operativo e versioni diverse di siti di Configuration Manager o di client di Configuration Manager, si possono verificare problemi con le estensioni.  


## <a name="latest-version-of-configuration-manager-sites-in-a-mixed-hierarchy"></a>Ultime versioni dei siti di Configuration Manager in una gerarchia mista  

Quando un sito viene aggiornato con l'ultima versione di Configuration Manager, le sequenze di attività che fanno riferimento al pacchetto di installazione client predefinito iniziano automaticamente a distribuire l'ultima versione client di Configuration Manager.

Le sequenze di attività che fanno riferimento a un pacchetto di installazione client personalizzato continuano a distribuire la versione del client contenuta in tale pacchetto. È probabile che i pacchetti personalizzati includano una versione precedente del client di Configuration Manager. Per evitare errori nella distribuzione di sequenze di attività, aggiornare tutti i pacchetti di installazione client personalizzato alla versione più recente.

Quando si configura una sequenza di attività per usare un pacchetto di installazione client personalizzato, eseguire una delle azioni seguenti:

- Aggiornare il passaggio della sequenza di attività per usare la versione di Configuration Manager più recente del pacchetto di installazione client
- Aggiornare il pacchetto personalizzato per usare l'origine dell'installazione client Configuration Manager più recente

> [!IMPORTANT]  
> Non distribuire una sequenza di attività che fa riferimento al pacchetto di installazione client di Configuration Manager più recente nei client di un sito di Configuration Manager meno recente. Quando i client assegnati a un sito di Configuration Manager precedente vengono aggiornati con l'ultima versione client di Configuration Manager, l'assegnazione al sito di Configuration Manager precedente viene bloccata. Questi client non sono più assegnati ad alcun sito. Finché il client non viene assegnato manualmente al sito di Configuration Manager più recente o finché non si reinstalla la versione precedente del client di Configuration Manager nel computer, questi client non sono gestiti.


## <a name="older-versions-of-configuration-manager-in-a-mixed-hierarchy"></a>Versioni precedenti dei siti di Configuration Manager in una gerarchia mista  

Quando si aggiorna il sito di amministrazione centrale all'ultima versione di Configuration Manager, verificare che le sequenze di attività di distribuzione del sistema operativo che vengono distribuite non lascino tali client in uno stato non gestito. Si supponga ad esempio di eseguire la distribuzione a client assegnati a un sito di Configuration Manager meno recente che non è ancora stato ancora aggiornato alla versione più recente di Configuration Manager.

Creare una copia di una sequenza di attività usata per la distribuzione ai client nella versione più recente del sito di Configuration Manager. Modificare quindi la sequenza di attività in modo che sia possibile distribuirla ai client in un sito di Configuration Manager meno recente. Configurare la sequenza di attività in modo che faccia riferimento a un pacchetto di installazione client personalizzato che usa l'origine dell'installazione client di Configuration Manager meno recente. Se non si ha già a disposizione un pacchetto di installazione client personalizzato che fa riferimento all'origine dell'installazione client di Configuration Manager meno recente, crearlo manualmente.  

> [!Important]  
> A partire dalla versione 1902, non è possibile distribuire un pacchetto o una sequenza di attività in un client versione 5.7730 o precedente. Per aggirare questa limitazione, aggiornare il client a una versione successiva.<!-- SCCMDocs-pr issue #3493 -->
