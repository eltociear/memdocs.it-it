---
title: Send Schedule Tool
titleSuffix: Configuration Manager
description: Usare lo strumento Send Schedule Tool per attivare una programmazione in un client di Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d5ce547d-3b3b-47d3-bcd7-6ff94692c046
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 78e154c5361063224d9e8c99bc87ba117958edf4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707469"
---
# <a name="send-schedule-tool"></a>Send Schedule Tool

*Si applica a: Configuration Manager (Current Branch)*

Send Schedule Tool è uno [strumento di Configuration Manager](tools.md). Usarlo per attivare una pianificazione in un client o per attivare la valutazione di una linea di base di configurazione specificata. Funziona per il computer locale o è destinato a un client remoto.  

Ad esempio, usare lo strumento per attivare una pianificazione di inventario o una valutazione di conformità. Se diversi client di Configuration Manager non hanno segnalato di recente lo stato di inventario o di conformità, eseguire lo strumento per avviare la pianificazione necessaria in ogni client.



## <a name="usage"></a>Utilizzo

Eseguire **SendSchedule.exe** come amministratore. 

`SendSchedule /L [Computer Name]`
`SendSchedule "<Message GUID | DCM UID>" [Computer Name]` 

Dopo l'attivazione di un messaggio (GUID), consultare il file **SMSClientMethodProvider.log**. Per altre informazioni sui GUID dei messaggi disponibili, vedere [ID messaggi](#bkmk_sendschedule-guids).

Dopo l'attivazione della valutazione di una linea di base di configurazione (UID DCM), vedere **DCMAgent.log**.



## <a name="command-line-options"></a>Opzioni della riga di comando


### <a name="option-l"></a>Opzione: `/L` 
Elencare tutti i GUID dei messaggi o gli UID DCM disponibili per l'invio. Visualizzare il nome significativo dei messaggi nella tabella dati per ognuno di essi. Se manca il nome del computer, usa il computer locale. Se si specifica un messaggio senza un nome di computer, invia il messaggio al computer locale. 



## <a name="examples"></a>Esempi

#### <a name="list-the-available-messages-on-the-local-machine"></a>Elencare i messaggi disponibili nel computer locale 
`SendSchedule /L` 

#### <a name="list-the-available-messages-on-the-client-mypc"></a>Elencare i messaggi disponibili nel client MyPC: 
`SendSchedule /L MyPC`

#### <a name="trigger-hardware-inventory-on-the-local-machine"></a>Attivare l'inventario hardware nel computer locale
`SendSchedule {00000000-0000-0000-0000-000000000001}`

#### <a name="trigger-hardware-inventory-on-mypc"></a>Attivare l'inventario hardware in MyPC: 
`SendSchedule {00000000-0000-0000-0000-000000000001} MyPC` 

#### <a name="trigger-the-evaluation-of-a-specific-configuration-baseline-on-mypc"></a>Attivare la valutazione di una linea di base di configurazione specifica in MyPC: 
`SendSchedule ScopeId_611E8382-C064-4B62-B0DE-EFFB52AE8994/Baseline_36722778-69dd-4423-9632-b61148b2b67e MyPC` 



## <a name="message-ids"></a><a name="bkmk_sendschedule-guids"></a> ID messaggio

|ID messaggio  |Nome visualizzato  |
|---------|---------|
|{00000000-0000-0000-0000-000000000001}|Inventario hardware|
|{00000000-0000-0000-0000-000000000002}|Inventario software|
|{00000000-0000-0000-0000-000000000003}|Inventario di individuazione|
|{00000000-0000-0000-0000-000000000010}|Raccolta file|
|{00000000-0000-0000-0000-000000000011}|Raccolta IDMIF|
|{00000000-0000-0000-0000-000000000021}|Richiesta assegnazioni computer|
|{00000000-0000-0000-0000-000000000022}|Valutare i criteri computer|
|{00000000-0000-0000-0000-000000000023}|Aggiornare l'attività MP predefinita|
|{00000000-0000-0000-0000-000000000024}|Attività percorsi di aggiornamento LS (Location Service)|
|{00000000-0000-0000-0000-000000000025}|Attività di aggiornamento timeout LS|
|{00000000-0000-0000-0000-000000000026}|Assegnazione richiesta agente criteri (utente)|
|{00000000-0000-0000-0000-000000000027}|Valutazione richiesta agente criteri (utente)|
|{00000000-0000-0000-0000-000000000031}|Report sull'utilizzo della generazione controllo software|
|{00000000-0000-0000-0000-000000000032}|Messaggio aggiornamento origine|
|{00000000-0000-0000-0000-000000000037}|Cancellazione della cache impostazioni proxy|
|{00000000-0000-0000-0000-000000000040}|Pulizia di agente criteri computer|
|{00000000-0000-0000-0000-000000000041}|Pulizia di agente criteri utente|
|{00000000-0000-0000-0000-000000000042}|Criterio computer convalida agente criteri / assegnazione|
|{00000000-0000-0000-0000-000000000043}|Criterio utente convalida agente criteri / assegnazione|
|{00000000-0000-0000-0000-000000000051}|Nuovo tentativo / Aggiornamento certificati in Active Directory in MP|
|{00000000-0000-0000-0000-000000000061}|Creazione report sullo stato DP peer|
|{00000000-0000-0000-0000-000000000062}|Pianificazione della verifica del pacchetto in sospeso DP peer|
|{00000000-0000-0000-0000-000000000063}|Pianificazione installazione aggiornamenti SUM|
|{00000000-0000-0000-0000-000000000101}|Ciclo di raccolta inventario hardware|
|{00000000-0000-0000-0000-000000000102}|Ciclo di raccolta inventario software|
|{00000000-0000-0000-0000-000000000103}|Ciclo di recupero dati di rilevamento|
|{00000000-0000-0000-0000-000000000104}|Ciclo di recupero file|
|{00000000-0000-0000-0000-000000000105}|Ciclo di recupero IDMIF|
|{00000000-0000-0000-0000-000000000106}|Ciclo di report sull'utilizzo del controllo del software|
|{00000000-0000-0000-0000-000000000107}|Ciclo di aggiornamento elenco origine Windows Installer|
|{00000000-0000-0000-0000-000000000108}|Azione criteri aggiornamenti software Ciclo di valutazione assegnazioni aggiornamenti software|
|{00000000-0000-0000-0000-000000000109}|Attività di manutenzione punto di distribuzione secondario criteri di manutenzione PDP|
|{00000000-0000-0000-0000-000000000110}|Criterio DCM|
|{00000000-0000-0000-0000-000000000111}|Inviare messaggio di stato non inviato|
|{00000000-0000-0000-0000-000000000112}|Pulizia della cache dei criteri sistema di stato|
|{00000000-0000-0000-0000-000000000113}|Aggiornare criteri origine|
|{00000000-0000-0000-0000-000000000114}|Aggiornare criteri store|
|{00000000-0000-0000-0000-000000000115}|Trasmissione elevata criteri sistema di stato|
|{00000000-0000-0000-0000-000000000116}|Trasmissione ridotta criteri sistema di stato|
|{00000000-0000-0000-0000-000000000121}|Azione dei criteri di gestione dell'applicazione|
|{00000000-0000-0000-0000-000000000122}|Azione dei criteri utente di gestione dell'applicazione|
|{00000000-0000-0000-0000-000000000123}|Azione valutazione globale di gestione dell'applicazione|
|{00000000-0000-0000-0000-000000000131}|Riepilogo iniziale risparmio energia|
|{00000000-0000-0000-0000-000000000221}|Endpoint rivalutazione distribuzione|
|{00000000-0000-0000-0000-000000000222}|Endpoint rivalutazione criterio AM|
|{00000000-0000-0000-0000-000000000223}|Rilevamento evento esterno|



