---
title: Risoluzione dei problemi di CMPivot
titleSuffix: Configuration Manager
description: Informazioni su come risolvere i problemi di CMPivot in Configuration Manager.
ms.date: 10/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 36385bea-f05e-4300-947f-cb3927b3bac5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 69178f9ac1c1acb1ee2a2931c88a55a0784435b8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708019"
---
# <a name="troubleshoot-cmpivot"></a>Risoluzione dei problemi di CMPivot

CMPivot è uno strumento che offre l'accesso allo stato in tempo reale dei dispositivi nell'ambiente in uso. CMPivot esegue una query su tutti i dispositivi connessi nella raccolta di destinazione e restituisce i risultati.

Occasionalmente, potrebbe essere necessario risolvere problemi di CMPivot. Ad esempio, se un messaggio di stato da un client a CMPivot viene danneggiato, il server del sito non può elaborare il messaggio. Questo articolo aiuta a comprendere il flusso di informazioni per CMPivot.

## <a name="troubleshoot-cmpivot-in-version-1902-and-later"></a><a name="bkmk_CMPivot-1902"></a> Risoluzione dei problemi di CMPivot nelle versioni 1902 e successive

In Configuration Manager versioni 1902 e successive è possibile eseguire CMPivot dal sito di amministrazione centrale in una gerarchia. Il sito primario gestisce ancora la comunicazione con il client.

Quando si esegue CMPivot dal sito di amministrazione centrale, viene usato il canale di sottoscrizione dei messaggi ad alta velocità per comunicare con il sito primario. CMPivot non usa la replica SQL standard tra siti. Se l'istanza di SQL Server o il provider è remoto oppure se si usa SQL Server Always On, sarà presente uno scenario a doppio hop per CMPivot. Per informazioni su come definire la delega vincolata per uno scenario a doppio hop, vedere [CMPivot a partire dalla versione 1902](cmpivot.md#bkmk_cmpivot1902).

>[!IMPORTANT]
> Durante la risoluzione dei problemi di CMPivot, abilitare la registrazione dettagliata nei punti di gestione e in SMS_MESSAGE_PROCESSING_ENGINE del server del sito per ottenere altre informazioni. Inoltre, se l'output del client è maggiore di 80 KB, abilitare la registrazione dettagliata nel punto di gestione e nel componente SMS_STATE_SYSTEM del server del sito. Per informazioni sull'abilitazione della registrazione dettagliata, vedere [Opzioni di registrazione del server del sito](../../plan-design/hierarchy/about-log-files.md#bkmk_reg-site).

### <a name="get-information-from-the-site-server"></a>Ottenere informazioni dal server del sito

Per impostazione predefinita, i file di log del server del sito si trovano in `C:\Program Files\Microsoft Configuration Manager\logs`. Questo percorso può essere diverso se è stata specificata una directory di installazione diversa da quella predefinita oppure se alcuni elementi, ad esempio il provider SMS, sono stati scaricati in un altro server. Se si esegue CMPivot dal sito di amministrazione centrale, i log sono disponibili nel server del sito primario.

Cercare in `smsprov.log` le righe seguenti:

- Configuration Manager versione 1906:
  <pre><code lang="Log">Auditing: User &ltusername> initiated client operation 145 to collection &ltCollectionId>. </code></pre>

- Configuration Manager versione 1902:
  <pre><code lang="Log">Type parameter is 135.
  Auditing: User &ltusername> ran script 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14 with hash dc6c2ad05f1bfda88d880c54121c8b5cea6a394282425a88dd4d8714547dc4a2 on collection &ltCollectionId>. </code></pre>

 `7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14` è il GUID di script per CMPivot. È anche possibile visualizzare questo GUID nei [Messaggi di stato di controllo di CMPivot](cmpivot.md#cmpivot-audit-status-messages).

Individuare quindi l'ID nella finestra di CMPivot. Questo ID corrisponde a `ClientOperationID`.

![Finestra di CMPivot con ClientOperationID evidenziato](media/cmpivot-client-operationid-1902.png)

Trovare `TaskID` della tabella ClientAction. `TaskID` corrisponde a `UniqueID` della tabella ClientAction.

``` SQL
select * from ClientAction where ClientOperationId=<id>
```

In `BgbServer.log` cercare `TaskID` raccolto da SQL e prendere nota di `PushID`. `TaskID` ha l'etichetta `TaskGUID`. Ad esempio:

<pre><code lang="Log">Starting to send push task (<b>PushID: 9</b> TaskID: 12 <b>TaskGUID: 9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0</b> TaskType: 15 TaskParam: PFNjcmlwdENvbnRlbnQgU2NyaXB0R3VpZD0nN0RDNkI2RjEtRTdGNi00M0MxL (truncated log entry)
Finished sending push task (<b>PushID: 9</b> TaskID: 12) to 2 clients
</code></pre>

### <a name="client-logs"></a>Log del client

Dopo aver raccolto le informazioni dal server del sito, controllare i log del client. Per impostazione predefinita, i log del client si trovano in `C:\Windows\CCM\Logs`.

In `CcmNotificationAgent.log` cercare le voci di log che hanno un aspetto simile a quello delle righe seguenti:  

<pre><code lang="Log">Receive task from server with <b>pushid=9</b>, taskid=12, <b>taskguid=9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0</b>, tasktype=15 and taskParam=PFNjcmlwdEhhc2ggU2NyaXB0SGF (truncated log entry)
Send Task response message &ltBgbResponseMessage TimeStamp="2019-09-13T17:29:09Z"><b>&ltPushID>5</b>&lt/PushID>&ltTaskID>4&lt/TaskID>&ltReturnCode>1&lt/ReturnCode>&lt/BgbResponseMessage> successfuly.
 </code></pre>

Cercare `Scripts.log` in `TaskID`. Nell'esempio seguente è visualizzato `Task ID` `{9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}`:

<pre><code lang="Log">Sending script state message (fast): <b>{9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}</b>
Result are sent for ScriptGuid: 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14 and <b>TaskID: {9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}</b>
</code></pre>

> [!NOTE]
> Se non viene visualizzato "(fast)" in `Scripts.log`, i dati probabilmente superano gli 80 KB. In questo caso, le informazioni vengono inviate al server del sito come messaggio di stato. Usare `StateMessage.log` del client e `Statesys.log` del server del sito.

### <a name="review-messages-on-the-site-server"></a>Rivedere i messaggi nel server del sito

Quando è abilitata la [registrazione dettagliata](../../plan-design/hierarchy/about-log-files.md#bkmk_reg-client) nel punto di gestione, è possibile visualizzare come vengono gestiti i messaggi client in ingresso. In `MP_RelayMsgMgr.log` cercare `TaskID`.

Nell'esempio di `MP_RelayMsgMgr.log` è visualizzato l'ID del client `(GUID:83F67728-2E6D-4E4F-8075-ED035C31B783)` e `Task ID {9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}`. Un ID messaggio viene assegnato alla risposta del client prima che venga inviata al motore di elaborazione dei messaggi:

<pre><code lang="Log">MessageKey: GUID:83F67728-2E6D-4E4F-8075-ED035C31B783<b>{9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}</b>
Create message succeeded for <b>message id 22f00adf-181e-4bad-b35e-d18912f39f89</b>
Add message payload succeeded for message id 22f00adf-181e-4bad-b35e-d18912f39f89
Put message succeeded for message id 22f00adf-181e-4bad-b35e-d18912f39f89
CRelayMsgMgrHandler::HandleMessage(): ExecuteTask() succeeded
</code></pre>

Quando la [registrazione dettagliata](../../plan-design/hierarchy/about-log-files.md#bkmk_logoptions) è abilitata in `SMS_MESSAGE_PROCESSING_ENGINE.log`, vengono elaborati i risultati del client. Usare l'ID messaggio trovato in `MP_RelayMsgMgr.log`. Le voci del log in elaborazione sono simili all'esempio seguente:

<pre><code lang="Log">Processing 2 messages with type Instant and IDs <b>22f00adf-181e-4bad-b35e-d18912f39f89[19]</b>, 434d80ae-09d4-4d84-aebf-28a4a29a9852[20]...
Processed 2 messages with type Instant. Failed to process 0 messages. All message IDs <b>22f00adf-181e-4bad-b35e-d18912f39f89[19]</b>, 434d80ae-09d4-4d84-aebf-28a4a29a9852[20]
</code></pre>

> [!TIP]
> Se si verifica un'eccezione durante l'elaborazione, è possibile esaminarla eseguendo la query SQL seguente ed esaminando la colonna Eccezione. Una volta elaborato, il messaggio non sarà più disponibile nella tabella `MPE_RequestMessages_Instant`.
>
> ```SQL
> select * from MPE_RequestMessages_Instant where MessageID=<ID from SMS_MESSAGE_PROCESSING_ENGINE.log>
> ```

In `BgbServer.log` cercare `PushID` per visualizzare il numero di client segnalati o non riusciti.

<pre><code lang="Log">Generated BGB task status report c:\ConfigMgr\inboxes\bgb.box\Bgb5c1db.BTS at 09/16/2019 16:46:39. (<b>PushID: 9</b> ReportedClients: 2 FailedClients: 0)
</code></pre>

Controllare la vista di monitoraggio per CMPivot da SQL usando `TaskID`.

``` SQL
select * from vSMS_CMPivotStatus where TaskID='{9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}'
```

[ ![Query SQL di CMPivot per la risoluzione dei problemi nella versione 1902](media/cmpivot-sql-queries-1902.png)](media/cmpivot-sql-queries-1902.png#lightbox)

## <a name="troubleshoot-cmpivot-in-1810-and-earlier"></a><a name="bkmk_CMPivot-1810"></a> Risoluzione dei problemi di CMPivot nelle versioni 1810 e precedenti

In Configuration Manager versione 1810 e precedenti il server del sito gestisce la comunicazione con il client.

### <a name="get-information-from-the-site-server"></a>Ottenere informazioni dal server del sito

Per impostazione predefinita, i file di log del server del sito si trovano in `C:\Program Files\Microsoft Configuration Manager\logs`. Questo percorso può essere diverso se è stata specificata una directory di installazione diversa da quella predefinita oppure se alcuni elementi, ad esempio il provider SMS, sono stati scaricati in un altro server.

Cercare in `smsprov.log` la riga seguente:

<pre><code lang="Log">Auditing: User <username> initiated client operation 135 to collection &ltCollectionId>.
</code></pre>

Trovare l'ID nella finestra di CMPivot. Questo ID corrisponde a `ClientOperationID`.

![Finestra di CMPivot con ClientOperationID evidenziato](media/cmpivot-clientoperationid.png)

Trovare `TaskID` della tabella ClientAction. `TaskID` corrisponde a `UniqueID` della tabella ClientAction.

``` SQL
select * from ClientAction where ClientOperationId=<id>
```

In `BgbServer.log` cercare il valore `TaskID` raccolto da SQL. Il valore ha l'etichetta `TaskGUID`. Ad esempio:

<pre><code lang="Log">Starting to send push task (PushID: 260 TaskID: 258 TaskGUID: <b>F8C7C37F-B42B-4C0A-B050-2BB44DF1098A</b> TaskType: 15
TaskParam: PFNjcmlwdEhhc2ggU2NyaXB0SGF...truncated...to 5 clients with throttling (strategy: 1 param: 42)
Finished sending push task (PushID: 260 TaskID: 258) to 5 clients
</code></pre>

### <a name="client-logs"></a>Log del client

Dopo aver raccolto le informazioni dal server del sito, controllare i log del client. Per impostazione predefinita, i log del client si trovano in `C:\Windows\CCM\Logs`.

In `CcmNotificationAgent.log` cercare log simili alla voce seguente:  

<pre><code lang="Log"><b>Error! Bookmark not defined.</b>+PFNjcmlwdEhhc2ggU2NyaXB0SGFzaEFsZz0nU0hBMjU2Jz42YzZmNDY0OGYzZjU3M2MyNTQyNWZiNT
g2ZDVjYTIwNzRjNmViZmQ1NTg5MDZlMWI5NDRmYTEzNmFiMDE0ZGNjPC9TY3JpcHRIYXNoPjxTY3Jp (truncated log entry)
</code></pre>

Cercare `Scripts.log` in `TaskID`. Nell'esempio seguente è visualizzato `Task ID {F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}`:

<pre><code lang="Log">Sending script state message: 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14
State message: Task Id <b>{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}</b>
</code></pre>

Cercare in `StateMessage.log`. Nell'esempio seguente `TaskID` è vicino alla parte inferiore del messaggio accanto a `<Param>`:

``` XML
StateMessage body: <?xml version="1.0" encoding="UTF-16"?>
<Report><ReportHeader><Identification><Machine><ClientInstalled>1</ClientInstalled><ClientType>1
</ClientType><ClientID>GUID:DBAC52C9-57E6-47D7-A8D6-E0A5A64B57E6</ClientID><ClientVersion>5.00.8670.1000</ClientVersion>
<NetBIOSName>R613924</NetBIOSName><CodePage>437</CodePage>
<SystemDefaultLCID>1033</SystemDefaultLCID><Priority>0</Priority></Machine></Identification>
<ReportDetails><ReportContent>State Message Data</ReportContent><ReportType>Full</ReportType>
<Date>20180703184447.673000+000</Date><Version>1.0</Version><Format>1.0</Format>
</ReportDetails></ReportHeader><ReportBody><StateMessage MessageTime="20180703184447.517000+000"><Topic ID="7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14" Type="9003" IDType="0" User="" UserSID=""/><State ID="1" Criticality="0"/>
<StateDetails Type="1"><![CDATA["PAA/AHgAbQBsACAAdgBlAHIAcwBpAG8AbgA9ACIAMQAuADAAIgAgAGUAbgBjAG8AZABpAG4AZwA9ACIAdQB0AGYALQAxADYAIgA/AD4APAByAGUAcwB1AGwAdAAgAFIAZQBzAHUAbAB0AEMAbwBkAGUAPQAiADAAIgA+ADwAZQAgAE4AYQBtAGUAPQAiAEkAbgB0AGUAbAAoAFIAKQAgAFgAZQBvAG4AKABSACkAIABDAFAAVQAgAEUANQAtADIANgA3ADMAIAB2ADQAIABAACAAMgAuADMAMABHAEgAegAiACAATQBhAG4AdQBmAGEAYwB0AHUAcgBlAHIAPQAiAEEAbQBlAHIAaQBjAGEAbgAgAE0AZQBnAGEAdAByAGUAbgBkAHMAIABJAG4AYwAuACIAIABWAGUAcgBzAGkAbwBuAD0AIgBWAFIAVABVAEEATAAgAC0AIAA2ADAAMAAxADcAMAAyACIAIABSAGUAbABlAGEAcwBlAEQAYQB0AGUAPQAiADIAMAAxADcALQAwADYALQAwADIAIAAwADAAOgAwADAAOgAwADAAIgAgAFMAZQByAGkAYQBsAE4AdQBtAGIAZQByAD0AIgAwADAAMAAwAC0AMAAwADEAOAAtADMANgA4ADIALQA0ADcAMAA4AC0ANwA2ADQAMAAtADcANgAwADAALQAzADMAIgAgAFMATQBCAEkATwBTAEIASQBPAFMAVgBlAHIAcwBpAG8AbgA9ACIAMAA5ADAAMAAwADcAIAAiACAALwA+ADwALwByAGUAcwB1AGwAdAA+AA=="~~]]></StateDetails><UserParameters Flags="0" Count="2">
<Param>{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}</Param><Param>0</Param></UserParameters></StateMessage></ReportBody></Report>

Successfully forwarded State Messages to the MP StateMessage 7/3/2018 11:44:47 AM 5036 (0x13AC)
```

### <a name="review-messages-on-the-site-server"></a>Rivedere i messaggi nel server del sito

Aprire `statesys.log` per verificare se il messaggio è stato ricevuto ed elaborato. Nell'esempio seguente `TaskID` è vicino alla parte inferiore del messaggio accanto a `<Param>`. Per visualizzare queste voci di log, abilitare la [registrazione dettagliata](../../plan-design/hierarchy/about-log-files.md#bkmk_logoptions) nel componente SMS_STATE_SYSTEM.

``` XML
CMessageProcessor - the cmdline to DB exec dbo.spProcessStateReport N'?<?xml version="1.0" encoding="UTF-
16"?>~~<Report><ReportHeader><Identification><Machine><ClientInstalled>1</ClientInstalled><ClientType>1
</ClientType><ClientID>GUID:DBAC52C9-57E6-47D7-A8D6-E0A5A64B57E6</ClientID><ClientVersion>5.00.8670.1000</ClientVersion>
<NetBIOSName>R613924</NetBIOSName><CodePage>437</CodePage>
<SystemDefaultLCID>1033</SystemDefaultLCID><Priority>0</Priority></Machine></Identification>
<ReportDetails><ReportContent>State Message Data</ReportContent><ReportType>Full</ReportType>
<Date>20180703184447.673000+000</Date><Version>1.0</Version><Format>1.0</Format>
</ReportDetails></ReportHeader><ReportBody><StateMessage MessageTime="20180703184447.517000+000"><Topic ID="7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14" Type="9003" IDType="0" User="" UserSID=""/><State ID="1" Criticality="0"/>
<StateDetails Type="1"><![CDATA["PAA/AHgAbQBsACAAdgBlAHIAcwBpAG8AbgA9ACIAMQAuADAAIgAgAGUAbgBjAG8AZABpAG4AZwA9ACIAdQB0AGYALQAxADYAIgA/AD4APAByAGUAcwB1AGwAdAAgAFIAZQBzAHUAbAB0AEMAbwBkAGUAPQAiADAAIgA+ADwAZQAgAE4AYQBtAGUAPQAiAEkAbgB0AGUAbAAoAFIAKQAgAFgAZQBvAG4AKABSACkAIABDAFAAVQAgAEUANQAtADIANgA3ADMAIAB2ADQAIABAACAAMgAuADMAMABHAEgAegAiACAATQBhAG4AdQBmAGEAYwB0AHUAcgBlAHIAPQAiAEEAbQBlAHIAaQBjAGEAbgAgAE0AZQBnAGEAdAByAGUAbgBkAHMAIABJAG4AYwAuACIAIABWAGUAcgBzAGkAbwBuAD0AIgBWAFIAVABVAEEATAAgAC0AIAA2ADAAMAAxADcAMAAyACIAIABSAGUAbABlAGEAcwBlAEQAYQB0AGUAPQAiADIAMAAxADcALQAwADYALQAwADIAIAAwADAAOgAwADAAOgAwADAAIgAgAFMAZQByAGkAYQBsAE4AdQBtAGIAZQByAD0AIgAwADAAMAAwAC0AMAAwADEAOAAtADMANgA4ADIALQA0ADcAMAA4AC0ANwA2ADQAMAAtADcANgAwADAALQAzADMAIgAgAFMATQBCAEkATwBTAEIASQBPAFMAVgBlAHIAcwBpAG8AbgA9ACIAMAA5ADAAMAAwADcAIAAiACAALwA+ADwALwByAGUAcwB1AGwAdAA+AA=="~~]]></StateDetails><UserParameters Flags="0" Count="2">
<Param>{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}</Param><Param>0</Param></UserParameters></StateMessage></ReportBody></Report>~~'
```

Se il messaggio non è stato elaborato, controllare la casella di posta in arrivo dei messaggi di stato. Il percorso predefinito della casella di posta in arrivo è `C:\Program Files\Microsoft Configuration Manager\inboxes\auth\statesys.box\`. Cercare i file nei percorsi seguenti:

- In arrivo
- Danneggiato
- Processo

Controllare la vista di monitoraggio per CMPivot da SQL usando `TaskID`.

``` SQL
select * from vSMS_CMPivotStatus where TaskID='{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}'
```

>[!NOTE]
>Per i client che usano la versione 1810 o una versione successiva, la messaggistica di stato non viene usata, a meno che l'output non sia superiore a 80 KB. Per la risoluzione dei problemi relativi a CMPivot in questi casi, abilitare la registrazione dettagliata nei punti di gestione e in SMS_MESSAGE_PROCESSING_ENGINE del server del sito per ottenere altre informazioni. Per informazioni sull'abilitazione della registrazione dettagliata, vedere [Opzioni di registrazione del server del sito](../../plan-design/hierarchy/about-log-files.md#bkmk_reg-site).
>
> Per la risoluzione dei problemi, fare riferimento ai log seguenti:
>
> - `MP_Relay.log`
> - `SMS_MESSAGE_PROCESSING_ENGINE.log`

## <a name="next-steps"></a>Passaggi successivi

- [Using CMPivot](cmpivot.md) (Uso di CMPivot)
- [Creare ed eseguire script di PowerShell](../../../apps/deploy-use/create-deploy-scripts.md)
