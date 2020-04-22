---
title: Run Meter Summarization Tool
titleSuffix: Configuration Manager
description: Run Meter Summarization Tool consente di avviare le attività di riepilogo della misurazione del software in Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d27f88fe-817f-4af4-b290-c16f2e46cf31
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 599cc2f552b975fa9b40c94ea413f6b80b04a1a3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707539"
---
# <a name="run-meter-summarization-tool"></a>Run Meter Summarization Tool

*Si applica a: Configuration Manager (Current Branch)*

Run Meter Summarization Tool è uno degli [strumenti di Configuration Manager](tools.md). Usarlo per avviare immediatamente le attività di manutenzione per il riepilogo della misurazione del software nei siti primari. Per impostazione predefinita, queste attività vengono eseguite in base alla pianificazione definita nelle attività di **Manutenzione sito**, che vengono avviate ogni giorno dopo le 12.00. 

Queste attività consentono di riepilogare i dati nella tabella SQL **MeterData** e di scrivere i risultati del riepilogo nelle tabelle **FileUsageSummary** e **MonthlyUsageSummary**. Il riepilogo dei risultati viene quindi visualizzato nei report di misurazione del software. Qualsiasi utente amministratore di Configuration Manager in grado di connettersi al database del sito primario può usare questo strumento per eseguire attività di riepilogo. 

Questo strumento esegue le attività di riepilogo dei dati della misurazione del software **Riepilogo utilizzo file** e **Riepilogo utilizzo mensile**. In particolare, riepiloga tutti i dati di misurazione esistenti senza attendere il normale periodo di attesa di 12 ore. Eseguirlo nel server SQL che ospita il database del sito. Se l'attività di riepilogo viene completata correttamente, il codice di uscita è impostato su `0`. In caso di errore, il codice di uscita è `1`.



## <a name="usage"></a>Utilizzo

### <a name="command-line"></a>Riga di comando

`runmetersumm  [sms database name]  <delay in hours for summarization <default=0>>`


### <a name="options"></a>Options

#### <a name="database-name"></a>Nome del database
Nome del database del sito nel server SQL.

#### <a name="delay-in-hours-for-summarization"></a>Ritardo in ore per l'attività di riepilogo
Lo strumento riepiloga l'utilizzo della misurazione del software generato prima del ritardo. Per impostazione predefinita, questo ritardo è pari a zero.


### <a name="example"></a>Esempio

#### <a name="summarize-the-software-metering-usage-generated-12-hours-ago"></a>Riepilogare l'utilizzo della misurazione del software generato 12 ore fa

`runmetersumm CCM_ABC <12>`



## <a name="see-also"></a>Vedere anche

- [Attività di manutenzione](../servers/manage/maintenance-tasks.md)
- [Monitorare l'uso delle app con la misurazione del software](../../apps/deploy-use/monitor-app-usage-with-software-metering.md)
