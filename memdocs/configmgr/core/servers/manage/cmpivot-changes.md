---
title: Modifiche a CMPivot
titleSuffix: Configuration Manager
description: Informazioni sulle modifiche apportate a CMPivot tra le versioni di Configuration Manager.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
ms.assetid: a49a9564-0863-44c3-991e-a8e271fed586
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 32800284c415de6a36e856abf473bc6d8d729e6f
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/09/2020
ms.locfileid: "89608252"
---
# <a name="changes-to-cmpivot"></a>Modifiche a CMPivot

Usare le informazioni seguenti per informazioni sulle modifiche apportate a [CMPivot](cmpivot.md) tra le versioni di Configuration Manager:

## <a name="cmpivot-changes-for-version-2006"></a><a name="bkmk_2006"></a> Modifiche apportate a CMPivot per la versione 2006
<!--6518631-->

A partire dalla versione 2006, sono stati apportati i miglioramenti seguenti per CMPivot:

- È stata eseguita la convergenza di [CMPivot autonomo](cmpivot.md#bkmk_standalone) e CMPivot avviato dalla console di amministrazione. Quando si avvia CMPivot dalla console di amministrazione, viene usata la stessa tecnologia sottostante di CMPivot autonomo per offrire lo stesso scenario.

- Sono stati apportati miglioramenti per la navigazione tramite tastiera in CMPivot.

- È possibile eseguire CMPivot da un singolo dispositivo o da più dispositivi dal nodo dispositivi senza dover selezionare una raccolta. Questo miglioramento rende più semplice per gli utenti, ad esempio quelli che si occupano di supporto tecnico, la creazione di query CMPivot per dispositivi specifici al di fuori di una raccolta creata in precedenza.
   - Selezionare un singolo dispositivo o più dispositivi in una raccolta di dispositivi oppure selezionare **Avvia CMPivot**.

- Quando si restituiscono i dispositivi all'interno di una visualizzazione elenco query, è possibile selezionare **Pivot dispositivo** in uno o più dispositivi ed eseguire quindi pivot e query su tali dispositivi per un'analisi approfondita. Questa modifica consente di eseguire un'analisi approfondita senza eseguire query sull'intero set di dispositivi della raccolta originale. **Pivot dispositivo** ha sostituito **Pivot in**.
   - All'interno di un'operazione CMPivot esistente, selezionare un singolo dispositivo o più dispositivi dall'output. Fare clic con il pulsante destro del mouse ed eseguire pivot usando l'opzione **Pivot dispositivo**. Questa azione avvia un'istanza separata di CMPivot riferita solo ai dispositivi selezionati. In questo modo, è più semplice eseguire il pivot ed eseguire query solo sui dispositivi desiderati senza dover creare una raccolta.

- Quando si esegue CMPivot per un singolo dispositivo, il nome del dispositivo viene elencato nella parte superiore della finestra. Per più dispositivi, il numero di dispositivi selezionati è elencato nella parte superiore della finestra.
- L'opzione **Crea raccolta** nella scheda Riepilogo query è stata rimossa perché CMPivot non richiede più l'esecuzione di query su una raccolta. Eseguire **Pivot dispositivo** per aprire una nuova istanza di CMPivot riferita solo ai dispositivi su cui si vuole eseguire la query. **Crea raccolta** è ancora disponibile nel menu principale.

![Pivot dispositivo per più dispositivi con CMPivot](./media/6518631-cmpivot-multi-select.png)


## <a name="cmpivot-changes-for-version-2002"></a><a name="bkmk_2002"></a> Modifiche apportate a CMPivot per la versione 2002
<!--5870934-->
È stata semplificata l'esplorazione delle entità CMPivot. A partire da Configuration Manager versione 2002, è possibile cercare entità CMPivot. Sono state inoltre aggiunte nuove icone per distinguere facilmente le entità e i tipi di oggetto entità.

![Ricerca di entità CMPivot](./media/5870934-search-cmpivot-entities.png)


## <a name="cmpivot-changes-for-version-1910"></a><a name="bkmk_cmpivot1910"></a> Modifiche apportate a CMPivot per la versione 1910
<!--5410930, 3197353-->
A partire dalla versione 1910, CMPivot è stato notevolmente ottimizzato per ridurre il traffico di rete e il carico sui server. È stata inoltre aggiunta una serie di nuove entità e di miglioramenti alle entità per facilitare l'individuazione e la risoluzione dei problemi. Nella versione 1910 sono state introdotte le modifiche seguenti per CMPivot:

- [Ottimizzazioni per il motore CMPivot](#bkmk_optimization)
- Entità aggiuntive e miglioramenti delle entità:
  - Registri eventi di Windows ([WinEvent](#bkmk_WinEvent))
  - Contenuto del file ([FileContent](#bkmk_File))
  - DLL caricate dai processi ([ProcessModule](#bkmk_ProcessModule))
  - Informazioni Azure Active Directory ([AADStatus](#bkmk_AadStatus))
  - Stato di Endpoint Protection ([EPStatus](#bkmk_EPStatus))
- [Valutazione delle query sul dispositivo locale con CMPivot autonomo](#bkmk_local-eval)
- [Altri miglioramenti a CMPivot](#bkmk_Other)


### <a name="optimizations-to-the-cmpivot-engine"></a><a name="bkmk_optimization"></a> Ottimizzazioni per il motore di CMPivot
<!--3197353-->
Per ridurre il traffico di rete e il carico sui server, CMPivot è stato ottimizzato nella versione 1910. Molte operazioni di query vengono ora eseguite direttamente sul client anziché sui server. Per effetto di questa modifica, alcune operazioni di CMPivot restituiscono una quantità minima di dati la prima volta che viene eseguita la query. Se si decide di eseguire il drill-down per ottenere altre informazioni, potrebbe essere eseguita una nuova query per recuperare i dati aggiuntivi dal client. In precedenza, ad esempio, come riposta a una query di "conteggio di riepilogo" veniva restituito un set di dati di grandi dimensioni.  Il set di dati restituito consentiva il drill-down immediato, ma molte volte sarebbe stato sufficiente il conteggio di riepilogo. Nella versione 1910, quando si sceglie di eseguire il drill-down in un client specifico, per restituire i dati aggiuntivi richiesti viene eseguita un'altra raccolta. Questa modifica offre un maggiore livello di prestazioni e scalabilità per l'esecuzione di query su un numero elevato di client. <!--3197353, 5458337-->

#### <a name="examples"></a>Esempi

Le ottimizzazioni di CMPivot riducono drasticamente il carico della CPU del server e della rete necessario per eseguire le query di CMPivot. Con queste ottimizzazioni, è ora possibile eseguire operazioni su gigabyte di dati client in tempo reale. Le query seguenti illustrano queste ottimizzazioni:

- Eseguire una ricerca in tutti i registri eventi di tutti i client dell'organizzazione per trovare errori di autenticazione.

   ``` Kusto
   EventLog('Security')
   | where  EventID == 4673
   | summarize count() by Device
   | order by count_ desc
   ```

- Eseguire la ricerca di un file in base all'hash.

   ``` Kusto
   Device
   | join kind=leftouter ( File('%windir%\\system32\\*.exe')
   | where SHA256Hash == 'A92056D772260B39A876D01552496B2F8B4610A0B1E084952FE1176784E2CE77')
   | project Device, MalwareFound = iif( isnull(FileName), 'No', 'Yes')
   ```

### <a name="wineventlognametimespan"></a><a name="bkmk_WinEvent"></a> WinEvent(\<logname>,[\<timespan>])

Questa entità viene usata per ottenere gli eventi dai registri eventi e dai file di log di Event Tracing. L'entità ottiene i dati dai registri eventi generati dalla tecnologia del Registro eventi di Windows. L'entità ottiene anche gli eventi nei file di log generati da Event Tracing for Windows (ETW). WinEvent esamina gli eventi che si sono verificati nelle ultime 24 ore per impostazione predefinita. L'impostazione predefinita di 24 ore può tuttavia essere ignorata includendo un intervallo di tempo.

``` Kusto
WinEvent('Microsoft-Windows-HelloForBusiness/Operational', 1d)
| where LevelDisplayName =='Error'
| summarize count() by Device
```

### <a name="filecontentfilename"></a><a name="bkmk_File"></a> FileContent(\<filename>)

FileContent viene usato per ottenere il contenuto di un file di testo.

``` Kusto
FileContent('c:\\windows\\SMSCFG.ini')
| where Content startswith  'SMS Unique Identifier='
| project Device, SMSId= substring(Content,22)
```

### <a name="processmoduleprocessname"></a><a name="bkmk_ProcessModule"></a> ProcessModule(\<processname>)  

Questa entità viene usata per enumerare i moduli (dll) caricati da un determinato processo. ProcessModule è utile per la ricerca del malware nascosto in processi legittimi.  

``` Kusto
ProcessModule('powershell')
| summarize count() by ModuleName
| order by count_ desc
```

### <a name="aadstatus"></a><a name="bkmk_AadStatus"></a> AadStatus

Questa entità può essere usata per ottenere le informazioni di identità di Azure Active Directory correnti da un dispositivo.

``` Kusto
AadStatus
| project Device, IsAADJoined=iif( isnull(DeviceId),'No','Yes')
| summarize DeviceCount=count() by IsAADJoined
| render piechart
```

### <a name="epstatus"></a><a name="bkmk_EPStatus"></a> EPStatus

EPStatus viene usato per ottenere lo stato del software antimalware installato nel computer.

``` Kusto
EPStatus
| project Device, QuickScanAge=datetime_diff('day',now(),QuickScanEndTime)
| summarize DeviceCount=count() by QuickScanAge
| order by QuickScanAge
| render barchart
```

### <a name="local-device-query-evaluation-using-cmpivot-standalone"></a><a name="bkmk_local-eval"></a> Valutazione delle query sul dispositivo locale con la versione autonoma di CMPivot
<!--3197353-->
Quando si usa CMPivot all'esterno della console di Configuration Manager, è possibile eseguire query solo sul dispositivo locale senza la necessità dell'infrastruttura di Configuration Manager. È ora possibile sfruttare le query di Azure Log Analytics CMPivot per visualizzare rapidamente informazioni WMI sul dispositivo locale. Ciò consente anche di convalidare e perfezionare le query CMPivot, prima di eseguirle in un ambiente più esteso. La versione autonoma di CMPivot è disponibile solo in inglese. Per altre informazioni su CMPivot autonomo, vedere [Modalità autonoma per CMPivot](#bkmk_standalone).

#### <a name="known-issues-for-local-device-query-evaluation"></a>Problemi noti relativi alla valutazione delle query sul dispositivo locale

 - Se si esegue una query su **Questo PC** per trovare un'entità WMI a cui non si può accedere, ad esempio una classe WMI bloccata, può verificarsi un arresto anomalo in CMPivot. Eseguire CMPivot usando un account con privilegi elevati per eseguire query su tali entità. <!--5753242-->
- Se si esegue una query su entità non WMI in **Questo PC**, verrà restituito un messaggio di **Spazio dei nomi non valido** o un'eccezione ambigua.
- Eseguire la versione autonoma di CMPivot dal collegamento del menu Start e non direttamente dal percorso del file eseguibile. <!--5787962-->

### <a name="other-enhancements"></a><a name="bkmk_Other"></a> Altri miglioramenti

- È possibile eseguire query sui tipi di espressione regolare usando il nuovo operatore `like`. Ad esempio:<!--3056858-->
  
   ```kusto
   //Find BIOS manufacture that contains any word like Micro, such as Microsoft
   Bios
   | where Manufacturer like '%Micro%'
   ```

- Sono state aggiornate le entità **CcmLog()** e **EventLog()** per esaminare solo i messaggi nelle ultime 24 ore per impostazione predefinita. Questo comportamento può essere ignorato passando un intervallo di tempo facoltativo. Ad esempio, la query seguente esaminerà gli eventi che si sono verificati nell'ultima ora:

   ```kusto
   CcmLog('Scripts',1h)
   ```

- L'entità **File()** è stata aggiornata per raccogliere informazioni sui file di sistema e nascosti e includere l'hash MD5. Pur non essendo accurato come l'hash SHA256, un hash MD5 tende a essere l'hash comunemente segnalato nella maggior parte dei bollettini malware.  

- È possibile aggiungere commenti nelle query.<!-- 5431463 --> Questo comportamento è utile quando si condividono le query. Ad esempio:

    ``` Kusto
    //Get the top ten devices sorted by user
    Device
    | top 10 by UserName
    ```

- CMPivot si connette automaticamente all'ultimo sito.<!-- 5420395 --> Dopo l'avvio di CMPivot è possibile connettersi a un nuovo sito, se necessario.

- Dal menu **Esporta** selezionare la nuova opzione che consente di **collegare la query agli Appunti**.<!-- 5431577 --> Questa azione consente di copiare un collegamento negli Appunti per poterlo condividere con altri utenti. Ad esempio:

    `cmpivot:Ly8gU2FtcGxlIHF1ZXJ5DQpPcGVyYXRpbmdTeXN0ZW0NCnwgc3VtbWFyaXplIGNvdW50KCkgYnkgQ2FwdGlvbg0KfCBvcmRlciBieSBjb3VudF8gYXNjDQp8IHJlbmRlciBiYXJjaGFydA==`

    Questo collegamento apre la modalità autonoma per CMPivot con la query seguente:

    ``` Kusto
    // Sample query
    OperatingSystem
    | summarize count() by Caption
    | order by count_ asc
    | render barchart
    ```

    > [!TIP]
    > Per il funzionamento di questo collegamento, [installare la modalità autonoma per CMPivot](#bkmk_standalone).

- Nei risultati della query, se il dispositivo è registrato in Microsoft Defender Advanced Threat Protection (ATP), fare clic con il pulsante destro del mouse sul dispositivo per avviare il portale online **Microsoft Defender Security Center**.

### <a name="known-issues-for-cmpivot-in-version-1910"></a>Problemi noti relativi a CMPivot nella versione 1910

- Quando viene raggiunto il limite, è possibile che il banner relativo al numero massimo di risultati non venga visualizzato. <!--5431427-->
  - Ogni client può restituire al massimo 128 kB di dati per ogni query.
  - Se i risultati della query superano 128 kB, è possibile che vengano troncati.

## <a name="cmpivot-changes-for-version-1906"></a><a name="bkmk_cmpivot1906"></a> Modifiche apportate a CMPivot per la versione 1906

A partire dalla versione 1906, a CMPivot sono stati aggiunti gli elementi seguenti:

- [Join, operatori aggiuntivi e aggregatori](#bkmk_cmpivot_joins)
- [Autorizzazioni CMPivot aggiunte al ruolo Amministratore della protezione](#bkmk_cmpivot_secadmin1906)
- [Modalità autonoma per CMPivot](#bkmk_standalone)

### <a name="add-joins-additional-operators-and-aggregators-in-cmpivot"></a><a name="bkmk_cmpivot_joins"></a> Aggiungere join, operatori aggiuntivi e aggregatori in CMPivot
<!--4054074-->
Sono ora disponibili operatori aritmetici aggiuntivi, aggregatori e la possibilità di aggiungere join di query, ad esempio l'uso congiunto di Registry e File. Sono stati aggiunti i seguenti elementi:

#### <a name="table-operators"></a>Operatori di tabella

|Operatori di tabella| Descrizione|
|-----|-----|
| [join](https://docs.microsoft.com/azure/kusto/query/joinoperator)| Consente di unire le righe di due tabelle in modo da formare una nuova tabella tramite la corrispondenza della riga per lo stesso dispositivo|
|render|Esegue il rendering dei risultati come output grafico|

L'operatore render esiste già in CMPivot. Sono stati aggiunti il supporto per più serie e l'istruzione **with**. Per altre informazioni, vedere la sezione [Esempi](#bkmk_cmpivot_examples1906) e l'articolo sull'[operatore join](https://docs.microsoft.com/azure/kusto/query/joinoperator) di Kusto.

#### <a name="limitations-for-joins"></a>Limitazioni per i join

1. La colonna del join viene eseguita sempre in modo implicito nel campo **Dispositivo**.
1. È possibile usare un massimo di 5 join per ogni query.
1. È possibile usare un massimo di 64 colonne combinate.

#### <a name="scalar-operators"></a>Operatori scalari

|Operator| Descrizione|Esempio|
|-----|-----|-----|
| + | Aggiunta| `2 + 1, now() + 1d`|
| - |  Sottrazione| `2 - 1, now() - 1d`|
| * | Moltiplicazione| `2 * 2`|
| / | Divisione | `2 / 1`|
| % | Modulo | `2 % 1`

#### <a name="aggregation-functions"></a>Funzioni di aggregazione

|Funzione| Descrizione|
|-----|-----|
| percentile()| Restituisce una stima per il percentile specificato con classificazione più prossima della popolazione definita da Expr|
| sumif() | Restituisce una somma di espressioni per la quale il predicato restituisce true|

#### <a name="scalar-functions"></a>Funzioni scalari

|Funzione| Descrizione|
|-----|-----|
| case()| Valuta un elenco di predicati e restituisce la prima espressione di risultato per la quale il predicato è soddisfatto |
| iff() | Valuta il primo argomento e restituisce il valore del secondo o del terzo argomento, a seconda che il predicato restituisca true (secondo) o false (terzo)|
 | indexof() | Funzione che restituisce l'indice in base zero della prima ricorrenza di una stringa specificata nella stringa di input|
| strcat() | Concatena da 1 a 64 argomenti |
| strlen()| Restituisce la lunghezza in caratteri della stringa di input|
| substring() | Estrae una sottostringa da una stringa di origine a partire da un indice e fino alla fine della stringa |
| tostring() | Converte l'input in un'operazione stringa |

#### <a name="examples"></a><a name="bkmk_cmpivot_examples1906"></a> Esempi

- Visualizza dispositivo, produttore, modello e versione del sistema operativo:

   ``` Kusto
   ComputerSystem
   | project Device, Manufacturer, Model
   | join (OperatingSystem | project Device, OSVersion=Caption)
   ```

- Visualizza un grafico dei tempi di avvio per un dispositivo:

   ``` Kusto
   SystemBootData
   | where Device == 'MyDevice'
   | project SystemStartTime, BootDuration, OSStart=EventLogStart, GPDuration, UpdateDuration
   | order by SystemStartTime desc
   | render barchart with (kind=stacked, title='Boot times for MyDevice', ytitle='Time (ms)')
   ```

   ![Grafico a barre in pila che visualizza i tempi di avvio per un dispositivo in ms](./media/4054074-render-using-with-statement.png)

### <a name="added-cmpivot-permissions-to-the-security-administrator-role"></a><a name="bkmk_cmpivot_secadmin1906"></a> Autorizzazioni CMPivot aggiunte al ruolo Amministratore della protezione
<!--4683130-->

A partire dalla versione 1906, al ruolo **Amministratore della protezione** predefinito di Configuration Manager sono state aggiunte le autorizzazioni seguenti:

 - **Lettura** per script SMS
 - **Esegui CMPivot** per la raccolta
 - **Lettura** per report di inventario

>[!NOTE]
> **Esegui script** è un super set dell'autorizzazione **Esegui CMPivot**.

### <a name="cmpivot-standalone"></a><a name="bkmk_standalone"></a> Modalità autonoma per CMPivot

[!INCLUDE [CMPivot standalone](includes/cmpivot-standalone.md)] 

## <a name="cmpivot-changes-for-version-1902"></a><a name="bkmk_cmpivot1902"></a> Modifiche apportate a CMPivot per la versione 1902
<!--3610960-->
A partire dalla versione 1902 di Configuration Manager è possibile eseguire CMPivot dal sito di amministrazione centrale in una gerarchia. Il sito primario gestisce ancora la comunicazione con il client. Quando CMPivot viene eseguito dal sito di amministrazione centrale, comunica con il sito primario tramite il canale di sottoscrizione dei messaggi ad alta velocità. Questa comunicazione non si basa sulla replica SQL standard tra siti.

L'esecuzione di CMPivot nel sito di amministrazione centrale richiede autorizzazioni aggiuntive quando SQL o il provider non sono nello stesso computer o in caso di configurazione SQL Always On. Con queste configurazioni remote, è necessario uno scenario con "doppio hop" per CMPivot.

Per fare in modo che CMPivot funzioni nel sito di amministrazione centrale in uno "scenario con doppio hop", è possibile definire la delega vincolata. Per comprendere le implicazioni di sicurezza di questa configurazione, leggere l'articolo sulla [delega vincolata Kerberos](https://docs.microsoft.com/windows-server/security/kerberos/kerberos-constrained-delegation-overview). Kerberos deve operare su tutti gli hop tra i computer.<!--5746133--> Se si usa più di una configurazione remota, ad esempio un provider SQL o SMS che condivide o meno il percorso con il sistema di amministrazione centrale, oppure in presenza di più foreste trusted, potrebbe essere necessaria una combinazione di impostazioni di autorizzazione. Di seguito sono riportati i passaggi che potrebbe essere necessario eseguire:

### <a name="cas-has-a-remote-sql-server"></a>Il sistema di amministrazione centrale usa un'istanza remota di SQL Server

1. Passare all'istanza di SQL Server di ogni sito primario.
   1. Aggiungere l'istanza remota di SQL Server del sistema di amministrazione centrale e il server del sito del sistema di amministrazione centrale al gruppo [Configmgr_DviewAccess](../../plan-design/hierarchy/accounts.md#configmgr_dviewaccess).
   ![Gruppo Configmgr_DviewAccess in un'istanza di SQL Server del sito primario](media/cmpivot-dviewaccess-group.png)
1. Accedere a Utenti e computer di Active Directory.
   1. Per il server di ogni sito primario, fare clic con il pulsante destro del mouse e selezionare **Proprietà**.
      1. Nella scheda della delega scegliere la terza opzione, **Computer attendibile per la delega solo ai servizi specificati**. 
      1. Scegliere **Utilizza solo Kerberos**.
      1. Aggiungere il servizio SQL Server del sistema di amministrazione centrale con porta e istanza.
      1. Verificare che queste modifiche siano conformi ai criteri di sicurezza aziendali.
   1. Per il sito del sistema di amministrazione aziendale, fare clic con il pulsante destro del mouse e selezionare **Proprietà**.
      1. Nella scheda della delega scegliere la terza opzione, **Computer attendibile per la delega solo ai servizi specificati**. 
      1. Scegliere **Utilizza solo Kerberos**.
      1. Aggiungere il servizio SQL Server di ogni sito primario con porta e istanza.
      1. Verificare che queste modifiche siano conformi ai criteri di sicurezza aziendali.

   ![Esempio di delega AD di CMPivot per doppi hop](media/cmpivot-ad-delegation.png)

### <a name="cas-has-a-remote-provider"></a>Il sistema di amministrazione centrale ha un provider remoto

1. Passare all'istanza di SQL Server di ogni sito primario.
   1. Aggiungere l'account del computer del provider e il server del sito del sistema di amministrazione centrale al gruppo [Configmgr_DviewAccess](../../plan-design/hierarchy/accounts.md#configmgr_dviewaccess).
1. Accedere a Utenti e computer di Active Directory.
   1. Selezionare il computer del provider del sistema di amministrazione centrale, fare clic con il pulsante destro del mouse e selezionare **Proprietà**.
      1. Nella scheda della delega scegliere la terza opzione, **Computer attendibile per la delega solo ai servizi specificati**. 
      1. Scegliere **Utilizza solo Kerberos**.
      1. Aggiungere il servizio SQL Server di ogni sito primario con porta e istanza.
      1. Verificare che queste modifiche siano conformi ai criteri di sicurezza aziendali.
   1. Selezionare il server del sito del sistema di amministrazione centrale, fare clic con il pulsante destro del mouse e selezionare **Proprietà**.
      1. Nella scheda della delega scegliere la terza opzione, **Computer attendibile per la delega solo ai servizi specificati**. 
      1. Scegliere **Utilizza solo Kerberos**.
      1. Aggiungere il servizio SQL Server di ogni sito primario con porta e istanza.
      1. Verificare che queste modifiche siano conformi ai criteri di sicurezza aziendali.
1. Riavviare il computer del provider remoto del sistema di amministrazione centrale.

### <a name="sql-always-on"></a>SQL Always On

1. Passare all'istanza di SQL Server di ogni sito primario.
   1. Aggiungere il server del sito del sistema di amministrazione centrale al gruppo [Configmgr_DviewAccess](../../plan-design/hierarchy/accounts.md#configmgr_dviewaccess).
1. Accedere a Utenti e computer di Active Directory.
   1. Per il server di ogni sito primario, fare clic con il pulsante destro del mouse e selezionare **Proprietà**.
      1. Nella scheda della delega scegliere la terza opzione, **Computer attendibile per la delega solo ai servizi specificati**. 
      1. Scegliere **Utilizza solo Kerberos**.
      1. Aggiungere gli account del servizio SQL Server del sistema di amministrazione centrale con porta e istanza.
      1. Verificare che queste modifiche siano conformi ai criteri di sicurezza aziendali.
   1. Selezionare il server del sito del sistema di amministrazione centrale, fare clic con il pulsante destro del mouse e selezionare **Proprietà**.
      1. Nella scheda della delega scegliere la terza opzione, **Computer attendibile per la delega solo ai servizi specificati**. 
      1. Scegliere **Utilizza solo Kerberos**.
      1. Aggiungere il servizio SQL Server di ogni sito primario con porta e istanza.
      1. Verificare che queste modifiche siano conformi ai criteri di sicurezza aziendali.
1. Verificare che il [nome SPN sia pubblicato](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/listeners-client-connectivity-application-failover#SPNs) per il nome del listener SQL del sistema di amministrazione centrale e per ogni nome del listener SQL primario.
1. Riavviare le istanze di SQL Server primarie.
1. Riavviare il server del sito e le istanze di SQL Server del sistema di amministrazione centrale.


## <a name="cmpivot-changes-for-version-1810"></a><a name="bkmk_cmpivot"></a> Modifiche apportate a CMPivot per la versione 1810
<!--1359068, 3607759-->

CMPivot include i miglioramenti seguenti a partire da Configuration Manager versione 1810:

- [Utilità e prestazioni di CMPivot](#bkmk_cmpivot-perf)
- [Funzioni scalari](#bkmk_cmpivot-functions)  
- [Visualizzazioni di rendering](#bkmk_cmpivot-charts)  
- [Inventario hardware](#bkmk_cmpivot-hinv)  
- [Operatori scalari](#bkmk_cmpivot-operators)  
- [Riepilogo delle query](#bkmk_cmpivot-summary)  
- [Messaggi di stato di controllo](#cmpivot-audit-status-messages)

### <a name="cmpivot-utility-and-performance"></a><a name="bkmk_cmpivot-perf"></a> Utilità e prestazioni di CMPivot

- CMPivot restituisce fino a 100.000 celle anziché 20.000 righe.
  - Se l'entità ha 5 proprietà, ovvero 5 colonne, vengono visualizzate al massimo 20.000 righe.
  - Per un'entità con 10 proprietà, vengono visualizzate fino a 10.000 righe.
  - Il totale dei dati visualizzati sarà minore o uguale a 100.000 celle.
- Nella scheda Riepilogo delle query selezionare il totale dei dispositivi Con errori o Offline e quindi selezionare l'opzione **Crea una raccolta**. Questa opzione consente di impostare facilmente come destinazione i dispositivi con distribuzione della correzione.
   - Questa opzione è stata rimossa nella versione 2006 poiché CMPivot non richiede più l'esecuzione di query su una raccolta.
- Per salvare la query **preferita** fare clic sull'icona della cartella.
   ![Esempio di salvataggio di una query preferita in CMPivot](media/cmpivot-favorite.png)

- I client aggiornati alla versione 1810 restituiscono un output inferiore a 80 kB al sito su un canale di comunicazione rapida.
  - Questa modifica migliora le prestazioni di visualizzazione dell'output di script o query.
  - Se l'output di script o query è maggiore di 80 KB, il client invia i dati tramite un messaggio di stato.
  - Se non è aggiornato alla versione 1810, il client continua a usare i messaggi di stato.

- Quando si avvia CMPivot, è possibile che venga visualizzato l'errore seguente:  **Non è possibile usare subito CMPivot a causa di una versione dello script incompatibile. Questo problema può dipendere dal fatto che la gerarchia sta aggiornando un sito. Attendere che venga completato l'aggiornamento, quindi riprovare.**

  - Se viene visualizzato questo messaggio, potrebbe significare che:
    - L'ambito di sicurezza non è configurato correttamente.
    - Si sono verificati problemi durante l'aggiornamento nel processo.
    - Lo script CMPivot sottostante è incompatibile.


### <a name="scalar-functions"></a><a name="bkmk_cmpivot-functions"></a> Funzioni scalari
CMPivot supporta le seguenti funzioni scalari:
- **ago()** : sottrarre l'intervallo di tempo specificato dall'ora UTC corrente  
- **datetime_diff()** : calcola la differenza di calendario tra due valori DateTime  
- **now()** : restituisce l'ora UTC corrente  
- **bin()** : arrotonda per difetto i valori a un multiplo intero di una dimensione di contenitore specificata  

> [!Note]  
> Il tipo di dati datetime rappresenta un istante nel tempo, in genere espresso come data e ora del giorno. I valori di tempo sono misurati in unità di 1 secondo. Un valore datetime è sempre il fuso orario UTC. Esprimere sempre i valori letterali data e ora in formato ISO 8601, ad esempio `yyyy-mm-dd HH:MM:ss`  

#### <a name="examples"></a>Esempi
- `datetime(2015-12-31 23:59:59.9)`: un valore letterale data e ora specifico   
- `now()`: l'ora corrente  
- `ago(1d)`: l'ora corrente meno un giorno  


### <a name="rendering-visualizations"></a><a name="bkmk_cmpivot-charts"></a> Visualizzazioni di rendering

CMPivot include ora il supporto di base per l'[operatore di rendering](https://docs.microsoft.com/azure/kusto/query/renderoperator) del linguaggio di query Kusto. Questo supporto include i tipi seguenti:  
- **barchart**: la prima colonna è l'asse x e può essere testo, data/ora o numerica. La seconda colonna deve essere numerica e viene visualizzato come una striscia orizzontale.  
- **columnchart**: come barchart, con strisce verticali anziché strisce orizzontali.  
- **piechart**: la prima colonna è l'asse del colore, la seconda colonna è numerica.  
- **timechart**: grafico a linee. La prima colonna è l'asse x e deve essere datetime. La seconda colonna è l'asse y.  

#### <a name="example-bar-chart"></a>Esempio: grafico a barre
La query seguente esegue il rendering delle applicazioni usate più di recente come un grafico a barre:

``` Kusto
CCMRecentlyUsedApplications
| summarize dcount( Device ) by ProductName
| top 10 by dcount_
| render barchart
```

![Esempio di visualizzazione di grafico a barre CMPivot](media/1359068-cmpivot-barchart.png)

#### <a name="example-time-chart"></a>Esempio: grafico del tempo
Per visualizzare i grafici del tempo, usare il nuovo operatore **bin()** per raggruppare gli eventi nel tempo. La query seguente indica quando sono stati avviati i dispositivi negli ultimi sette giorni:

``` Kusto
OperatingSystem
| where LastBootUpTime <= ago(7d)
| summarize count() by bin(LastBootUpTime,1d)
| render timechart
```

![Esempio di visualizzazione di grafico del tempo CMPivot](media/1359068-cmpivot-timechart.png)

#### <a name="example-pie-chart"></a>Esempio: grafico a torta
La query seguente visualizza tutte le versioni del sistema operativo in un grafico a torta:

``` Kusto
OperatingSystem
| summarize count() by Caption
| render piechart
```

![Esempio di visualizzazione di grafico a torta CMPivot](media/1359068-cmpivot-piechart.png)


### <a name="hardware-inventory"></a><a name="bkmk_cmpivot-hinv"></a> Inventario hardware
Usare CMPivot per eseguire query sulle classi di inventario hardware. Queste classi includono eventuali estensioni personalizzate create per l'inventario hardware. CMPivot restituisce immediatamente i risultati memorizzati nella cache dell'ultima analisi dell'inventario hardware archiviata nel database del sito. Allo stesso tempo, se necessario aggiorna i risultati con i dati dinamici di tutti i client online.

La saturazione del colore dei dati nella tabella o nel grafico dei risultati indica se i dati sono dinamici o memorizzati nella cache. Ad esempio, blu scuro è un dato in tempo reale proveniente da un client online. Blu chiaro è un dato memorizzato nella cache.

#### <a name="example"></a>Esempio

``` Kusto
LogicalDisk
| summarize sum( FreeSpace ) by Device
| order by sum_ desc
| render columnchart
```

![Esempio di query sull'inventario CMPivot con visualizzazione di un istogramma](media/1359068-cmpivot-inventory.png)

#### <a name="limitations"></a>Limitazioni
- Le seguenti entità di inventario hardware non sono supportate:  
    - Proprietà della matrice, ad esempio l'indirizzo IP  
    - Real32/Real64 <!--example?-->  
    - Proprietà oggetti selezionati <!--example?-->  
- I nomi di entità di inventario devono iniziare con un carattere
- Non è possibile sovrascrivere le entità predefinite creando un'entità di inventario con lo stesso nome  


### <a name="scalar-operators"></a><a name="bkmk_cmpivot-operators"></a> Operatori scalari
CMPivot include i seguenti operatori scalari:  

> [!Note]  
> - LHS: stringa a sinistra dell'operatore  
> - RHS: stringa a destra dell'operatore  


|Operator|Descrizione|Esempio (restituisce true)|
|--------|-----------|---------------------|
|==|Uguale a|`"aBc" == "aBc"`|
|!=|Diverso da|`"abc" != "ABC"`|
|like|LHS contiene una corrispondenza per RHS|`"FabriKam" like "%Brik%"`|
|!like|LHS non contiene una corrispondenza per RHS|`"Fabrikam" !like "%xyz%"`|
|contains|RHS si verifica come sottosequenza di LHS|`"FabriKam" contains "BRik"`|
|!contains|RHS non si verifica in LHS|`"Fabrikam" !contains "xyz"`|
|startswith|RHS è una sottosequenza iniziale di LHS|`"Fabrikam" startswith "fab"`|
|!startswith|RHS non è una sottosequenza iniziale di LHS|`"Fabrikam" !startswith "kam"`|
|endswith|RHS è una sottosequenza di chiusura di LHS|`"Fabrikam" endswith "Kam"`|
|!endswith|RHS non è una sottosequenza di chiusura di LHS|`"Fabrikam" !endswith "brik"`|


### <a name="query-summary"></a><a name="bkmk_cmpivot-summary"></a> Riepilogo delle query

Selezionare la scheda **Riepilogo delle query** nella parte inferiore della finestra CMPivot. Questo stato consente di identificare i client che sono offline o di risolvere gli errori che possono verificarsi. Selezionare un valore nella colonna del conteggio per aprire un elenco di dispositivi specifici con tale stato. 

Ad esempio, selezionare il numero di dispositivi con uno stato di errore. Vedere il messaggio di errore specifico ed esportare un elenco di questi dispositivi. Se l'errore è che un cmdlet specifico non viene riconosciuto, creare una raccolta dall'elenco dei dispositivi esportati per distribuire un aggiornamento di Windows PowerShell.  

### <a name="cmpivot-audit-status-messages"></a>Messaggi di stato di controllo di CMPivot

A partire dalla versione 1810, quando si esegue CMPivot viene creato un messaggio di stato di controllo con **MessageID 40805**. Per visualizzare i messaggi di stato, andare a **Monitoraggio** > **Stato del sistema** > **Query messaggi di stato**. È possibile eseguire **tutti i messaggi di stato di controllo per un utente specifico**, **tutti i messaggi di stato di controllo per un sito specifico** o creare la propria query di messaggio di stato.

Per il messaggio viene usato il formato seguente:

MessageId 40805: L'utente &lt;NomeUtente> ha eseguito lo script &lt;GUID-script> con hash &lt;hash-script> nella raccolta &lt;ID-raccolta>.

- 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14 è il GUID dello script per CMPivot.
- Il codice hash dello script può essere visualizzato nel file scripts.log del client.
- È anche possibile visualizzare l'hash archiviato nello script client. Il nome file nel client è &lt;GUID-script>_&lt;hash-script>.
    - Esempio di nome file: C:\Windows\CCM\ScriptStore\7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14_abc1d23e45678901fabc123d456ce789fa1b2cd3e456789123fab4c56789d0123.ps
   

![Esempio di messaggio di stato di controllo di CMPivot](media/cmpivot-audit-status-message.png)

## <a name="next-steps"></a>Passaggi successivi
 
[Risoluzione dei problemi di CMPivot](cmpivot-tsg.md)
