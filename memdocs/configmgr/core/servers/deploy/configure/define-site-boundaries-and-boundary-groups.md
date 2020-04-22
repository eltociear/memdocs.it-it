---
title: Usare limiti e gruppi di limiti
titleSuffix: Configuration Manager
description: Usare i limiti e i gruppi di limiti per definire percorsi di rete e sistemi del sito accessibili per i dispositivi gestiti.
ms.date: 06/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 54aa20d5-791e-4416-9db4-5aaea472c0b7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 0b1a6bb6ff9fdffad65db884fe8c3b68d3fc3263
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690899"
---
# <a name="define-site-boundaries-and-boundary-groups"></a>Definire i limiti e i gruppi di limiti del sito

*Si applica a: Configuration Manager (Current Branch)*

Il termine *limiti* in Configuration Manager definisce percorsi di rete della Intranet. Questi percorsi includono i dispositivi che si vuole gestire. I *gruppi di limiti* sono gruppi logici di limiti che è possibile configurare.

Una gerarchia può includere un numero illimitato di gruppi di limiti. Ogni gruppo di limiti può contenere qualsiasi combinazione dei seguenti tipi di limiti:  

- Subnet IP  
- Nome del sito Active Directory  
- Prefisso IPv6  
- Intervallo indirizzi IP  

I client nella intranet valutano il relativo percorso di rete corrente e quindi usano tali informazioni per identificare i gruppi di limiti a cui appartengono.  

I client usano i gruppi di limiti per:  

- **Trovare un sito assegnato**: i gruppi di limiti consentono ai client di individuare un sito primario per l'assegnazione client. Questo comportamento è detto anche *assegnazione sito automatica*.  

- **Trovare specifici ruoli del sistema del sito che possono usare:** Associare un gruppo di limiti a determinati ruoli del sistema del sito. Il sito fornisce quindi ai client questo elenco di sistemi del sito nel gruppo di limiti. I client usano questi sistemi del sito per azioni come l'individuazione di contenuto o di un punto di gestione nelle vicinanze.  

I client in Internet o configurati come client solo per Internet non usano le informazioni relative ai limiti. Questi client non possono usare l'assegnazione sito automatica. Possono scaricare contenuto da un punto di distribuzione basato su Internet dal proprio sito assegnato o da un punto di distribuzione basato su cloud.  

A partire dalla versione 1902 è possibile associare un Cloud Management Gateway (CMG) a un gruppo di limiti. Per altre informazioni, vedere [Progettazione della gerarchia CMG](../../../clients/manage/cmg/plan-cloud-management-gateway.md#hierarchy-design).<!--3640932-->


## <a name="recommendations"></a><a name="BKMK_BoundaryBestPractices"></a> Consigli

### <a name="use-a-mix-of-the-fewest-boundaries-that-meet-your-needs"></a>Usare una combinazione del numero minimo di limiti che soddisfano le esigenze

Usare il tipo o i tipi di limiti più adatti per il proprio ambiente. Per semplificare le attività di gestione, usare tipi di limiti che consentano di usare il minor numero possibile di limiti.

### <a name="avoid-overlapping-boundaries-for-automatic-site-assignment"></a>Evitare la sovrapposizione dei limiti per l'assegnazione sito automatica

Anche se ogni gruppo di limiti supporta il riferimento sia all'assegnazione sito che al sistema del sito, creare un set separato di gruppi di limiti da usare solo per l'assegnazione sito. Verificare che ogni limite in un gruppo di limiti non sia membro di un altro gruppo di limiti con un'assegnazione sito diversa.

- Un singolo limite può essere incluso in più gruppi di limiti  

- Ogni gruppo di limiti può essere associato a un sito primario diverso per l'assegnazione del sito  

- Se un limite è membro di due diversi gruppi di limiti con assegnazioni sito diverse, i client selezionano in modo casuale un sito a cui aggiungersi. Questo comportamento potrebbe non corrispondere al sito a cui si vuole aggiungere il client. Questa configurazione è definita *a limiti sovrapposti*.  

    La sovrapposizione dei limiti non è un problema per il percorso del contenuto. Può essere una configurazione utile che fornisce ai client ulteriori risorse o percorsi di contenuto da usare.  


## <a name="next-steps"></a>Passaggi successivi

- [Definire percorsi di rete come limiti di System Center Configuration Manager](boundaries.md)

- [Configurare gruppi di limiti](boundary-groups.md)
