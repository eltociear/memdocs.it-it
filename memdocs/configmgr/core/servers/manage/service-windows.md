---
title: Manutenzione di Windows
titleSuffix: Configuration Manager
description: Usare gli intervalli di servizio per controllare quando i siti Configuration Manager installano gli aggiornamenti.
ms.date: 01/11/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ca4886d4-7173-46be-8dcd-1657d5b0deb9
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 669da2a04fe4e94b08fc426c32e0dbcc804a21d1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702049"
---
#  <a name="service-windows-for-site-servers"></a>Intervalli di servizio per i server del sito

*Si applica a: Configuration Manager (Current Branch)*

È possibile configurare gli intervalli di servizio nei siti di amministrazione centrale e in quelli primari per controllare quando possono essere installati gli aggiornamenti nella console.  È possibile configurare più intervalli e quello consentito per l'installazione degli aggiornamenti è determinato in base a una combinazione di tutti gli intervalli di servizio per lo specifico server del sito.

Quando non è configurato alcun intervallo di servizio:
- **Nel sito di livello superiore** (un sito di amministrazione centrale o un sito primario autonomo) scegliere quando avviare l'installazione dell'aggiornamento.
- **In un sito primario figlio** l'aggiornamento viene installato automaticamente al termine dell'installazione dell'aggiornamento nel sito di amministrazione centrale.
- **In un sito secondario** gli aggiornamenti non vengono mai avviati automaticamente. In alternativa, è necessario avviare manualmente l'installazione dell'aggiornamento dall'interno della console dopo che questo è stato installato nel sito primario padre.

Quando è configurato un intervallo di servizio:
- **Nel sito di livello superiore** non è possibile avviare l'installazione di un nuovo aggiornamento dall'interno della console di Configuration Manager. Anche quando è configurato un intervallo di servizio, il sito scarica automaticamente gli aggiornamenti in modo che siano pronti per l'installazione.  
- **In un sito primario figlio** gli aggiornamenti installati in un sito di amministrazione centrale vengono scaricati nel sito primario, ma non vengono avviati automaticamente. Non è possibile avviare manualmente l'installazione di un aggiornamento durante un periodo in cui questa è bloccata da un intervallo di servizio. Quando non è più bloccata da intervalli di servizio, l'installazione dell'aggiornamento viene avviata automaticamente.
- **I siti secondari** non supportano gli intervalli di servizio e non installano automaticamente gli aggiornamenti. Dopo che il sito primario padre di un sito secondario ha installato un aggiornamento, è possibile avviare l'aggiornamento del sito secondario dall'interno della console.

## <a name="to-configure-a-service-window"></a>Per configurare un intervallo di servizio

1.  Nella console di Configuration Manager aprire **Amministrazione** > **Configurazione del sito** > **Siti** e quindi selezionare il server del sito in cui si vuole configurare un intervallo di servizio.  

2.  Successivamente, modificare le **Proprietà** del server del sito e selezionare la scheda **Intervallo di servizio** in cui è possibile impostare uno o più intervalli di servizio per il server del sito.  
