---
title: Creare ed eseguire script
titleSuffix: Configuration Manager
description: Creare ed eseguire script di PowerShell in dispositivi client.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1c15106eeecdac0377900d913160bc23614327db
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689659"
---
# <a name="create-and-run-powershell-scripts-from-the-configuration-manager-console"></a>Creare ed eseguire gli script di PowerShell dalla console di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

<!--1236459-->
La funzionalità di esecuzione degli script di PowerShell è integrata in Configuration Manager. Il vantaggio di PowerShell è che consente di creare script automatici sofisticati, intuitivi e condivisi con una vasta community. Gli script semplificano la creazione di strumenti personalizzati per amministrare il software e consentono di eseguire rapidamente attività pratiche, anche impegnative, in modo più semplice e coerente.  

> [!Note]  
> Configuration Manager non abilita questa funzionalità facoltativa per impostazione predefinita. Pertanto sarà necessario abilitarla prima di poterla usare. Per altre informazioni, vedere [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options) (Abilitare le funzioni facoltative dagli aggiornamenti).<!--505213-->  


Grazie a questa integrazione in Configuration Manager, è possibile usare la funzionalità *Esegui script* per:

- Creare e modificare script da usare con Configuration Manager.
- Gestire l'utilizzo degli script tramite ruoli e ambiti di protezione. 
- Eseguire gli script in raccolte o singoli PC Windows gestiti in locale.
- Ottenere rapidi risultati degli script aggregati dai dispositivi client.
- Monitorare l'esecuzione degli script e visualizzare i risultati restituiti dall'output degli script.

> [!WARNING]
> - Considerando la potenza degli script, è consigliabile usarli con attenzione e solo se intenzionalmente. Sono state integrate altre misure di sicurezza per supportare l'utente finale, come ruoli e ambiti segregati. Verificare l'accuratezza degli script prima di eseguirli e accertarsi che provengano da un'origine attendibile, per impedirne l'esecuzione accidentale. Prestare attenzione ai caratteri estesi o ad altri problemi di offuscamento e abituarsi a proteggere gli script. [Informazioni sulla sicurezza degli script PowerShell](learn-script-security.md)
> - Alcuni software antimalware possono attivare inavvertitamente eventi per le funzionalità Esegui script o CMPivot di Configuration Manager. È consigliabile escludere %windir%\CCM\ScriptStore in modo che il software antimalware consenta l'esecuzione di tali funzionalità senza interferenze.

## <a name="prerequisites"></a>Prerequisiti

- Per eseguire script PowerShell, nel client deve essere in esecuzione PowerShell versione 3.0 o successiva. Tuttavia, se lo script eseguito contiene funzionalità di una versione successiva di PowerShell, nel client in cui viene eseguito lo script deve essere installata questa versione.
- Per eseguire gli script, i client Configuration Manager devono avere in esecuzione il client della versione 1706 o successiva.
- Per usare gli script, l'utente deve essere membro del ruolo di sicurezza appropriato di Configuration Manager.
- Per importare e creare script, l'account deve avere autorizzazioni **Crea** per **Script SMS**.
- Per approvare o rifiutare script, l'account deve avere autorizzazioni **Approva** per **Script SMS**.
- Per eseguire gli script, l'account deve avere autorizzazioni **Esegui script** per **Raccolte**.

Per altre informazioni sui ruoli di sicurezza di Configuration Manager:</br>
[Ambiti di protezione per l'esecuzione di script](#security-scopes)</br>
[Ruoli di sicurezza per l'esecuzione di script](#bkmk_ScriptRoles)</br>
[Nozioni fondamentali sull'amministrazione basata su ruoli](../../core/understand/fundamentals-of-role-based-administration.md)

## <a name="limitations"></a>Limitazioni

La funzionalità Esegui script supporta attualmente:

- Linguaggi di scripting: PowerShell
- Tipi di parametro: intero, stringa ed elenco.


>[!WARNING]
>Tenere presente che quando si usano i parametri si apre una superficie di attacco con il rischio potenziale di attacchi PowerShell injection. Per ovviare al problema, esistono vari modi e soluzioni alternative, ad esempio l'uso di espressioni regolari per convalidare l'input del parametro o l'uso di parametri predefiniti. Una procedura consigliata comune consiste nel non includere segreti negli script di PowerShell, ad esempio password e così via. [Informazioni sulla sicurezza degli script PowerShell](learn-script-security.md) <!--There are external tools available to validate your PowerShell scripts such as the [PowerShell Injection Hunter](https://www.powershellgallery.com/packages/InjectionHunter/1.0.0) tool. -->


## <a name="run-script-authors-and-approvers"></a>Autori e responsabili dell'approvazione di script

La funzionalità Esegui script usa il concetto di *autore di script* e *responsabile dell'approvazione di script* come ruoli separati per l'implementazione e l'esecuzione di uno script. La separazione dei ruoli di autore e responsabile dell'approvazione consente un'importante verifica dei processi per lo strumento Esegui script. Un altro ruolo, *esecutori di script*, consente l'esecuzione di script, ma non la creazione o l'approvazione. Vedere [Creare ruoli di sicurezza per gli script](#bkmk_ScriptRoles).

### <a name="scripts-roles-control"></a>Controllo dei ruoli per gli script

Per impostazione predefinita, gli utenti non possono approvare uno script da loro stessi creato. Poiché gli script sono potenti e versatili e vengono potenzialmente distribuiti a molti dispositivi, è possibile separare i ruoli tra la persona che crea lo script e la persona che lo approva. Questi ruoli garantiscono un livello aggiuntivo di sicurezza, impedendo l'esecuzione di uno script senza supervisione. Per semplificare le attività di test, è possibile disattivare l'approvazione secondaria.

### <a name="approve-or-deny-a-script"></a>Approvare o rifiutare uno script

Gli script devono essere approvati dal ruolo *responsabile dell'approvazione di script* prima di poter essere eseguiti. Per approvare uno script:

1. Nella console di Configuration Manager fare clic su **Raccolta software**.
2. Nell'area di lavoro **Raccolta software** fare clic su **Script**.
3. Nell'elenco **Script** scegliere lo script che si desidera approvare o rifiutare e quindi scegliere la scheda **Home** nel gruppo **Script**, quindi fare clic su **Approve/Deny** (Approva/Rifiuta).
4. Nella finestra di dialogo **Approva o rifiuta script** selezionare **Approva** o **Nega** per lo script. Facoltativamente, immettere un commento sulla decisione.  Se si rifiuta uno script, questo non può essere eseguito nei dispositivi client. <br>
![Script - Approvazione](./media/run-scripts/RS-approval.png)
1. Completare la procedura guidata. Nell'elenco **Script** la colonna **Stato dell'approvazione** cambia a seconda dell'azione eseguita.

### <a name="allow-users-to-approve-their-own-scripts"></a>Consentire agli utenti di approvare i propri script

Questa approvazione viene usata principalmente per la fase di test dello sviluppo di script.

1. Nella console di Configuration Manager fare clic su **Amministrazione**.
2. Nell'area di lavoro **Amministrazione** , espandere **Configurazione sito**, quindi fare clic su **Siti**.
3. Nell'elenco dei siti selezionare il sito e quindi scegliere la scheda **Home** nel gruppo **Siti** e fare clic su **Impostazioni gerarchia**.
4. Nella scheda **Generale** della finestra di dialogo **Proprietà delle impostazioni di gerarchia** deselezionare la casella di controllo **Gli autori dello script richiedono un responsabile approvazione aggiuntivo per lo script**.

>[!IMPORTANT]
>Come procedura consigliata, non consentire a un autore di script di approvare i propri script. Ciò deve essere consentito solo in un ambiente di prova. Valutare con attenzione il potenziale impatto della modifica di questa impostazione in un ambiente di produzione.

## <a name="security-scopes"></a>ambiti di protezione
*Introdotti con la versione 1710*  
La funzionalità Esegui script usa gli ambiti di protezione, una caratteristica esistente di Configuration Manager, per controllare la creazione e l'esecuzione di script tramite l'assegnazione di tag che rappresentano gruppi di utenti. Per altre informazioni sull'uso degli ambiti di protezione, vedere [Configurare l'amministrazione basata su ruoli per Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).

## <a name="create-security-roles-for-scripts"></a><a name="bkmk_ScriptRoles"></a> Creare ruoli di sicurezza per gli script
I tre ruoli di sicurezza usati per l'esecuzione di script non vengono creati per impostazione predefinita in Configuration Manager. Per creare i ruoli di esecutori di script, autori di script e responsabili dell'approvazione di script seguire i passaggi descritti.

1. Nella console di Configuration Manager passare a **Amministrazione** >**Protezione** >**Ruoli di protezione**
2. Fare clic con il pulsante destro del mouse su un ruolo e selezionare **Copia**. Il ruolo copiato ha le autorizzazioni già assegnate. Verificare di includere solo le autorizzazioni desiderate. 
3. Assegnare al ruolo personalizzato un **nome** e una **descrizione**. 
4. Assegnare al ruolo di sicurezza le autorizzazioni indicate di seguito.  

### <a name="security-role-permissions"></a>Autorizzazioni del ruolo di sicurezza  

**Nome ruolo**: Esecutori di script  
- **Descrizione**: queste autorizzazioni consentono a questo ruolo solo di eseguire script precedentemente creati e approvati da altri ruoli.  
- **Autorizzazioni:** verificare che le autorizzazioni seguenti siano impostate su **Sì**.  

|Categoria|Autorizzazione|Stato|
|---|---|---|
|Raccolta|Esegui script|Sì|
|Sito|Lettura|Sì|
|Script SMS|Lettura|Sì|


**Nome ruolo**: Autori di script  
- **Descrizione**: queste autorizzazioni consentono a questo ruolo di creare script, ma non di approvarli o eseguirli.  
- **Autorizzazioni**: verificare che siano impostate le autorizzazioni seguenti.
 
|Categoria|Autorizzazione|Stato|
|---|---|---|
|Raccolta|Esegui script|No|
|Sito|Lettura|Sì|
|Script SMS|Creazione|Sì|
|Script SMS|Lettura|Sì|
|Script SMS|Elimina|Sì|
|Script SMS|Modifica|Sì|


**Nome ruolo**: Responsabili approvazione di script  
- **Descrizione**: queste autorizzazioni consentono a questo ruolo di approvare script, ma non di crearli o eseguirli.  
- **Autorizzazioni:** verificare che siano impostate le autorizzazioni seguenti.  

|Categoria|Autorizzazione|Stato|
|---|---|---|
|Raccolta|Esegui script|No|
|Sito|Lettura|Sì|
|Script SMS|Lettura|Sì|
|Script SMS|Approva|Sì|
|Script SMS|Modifica|Sì|

     
**Esempio di autorizzazioni Script SMS per il ruolo di autori di script**  

 ![Esempio di autorizzazioni Script SMS per il ruolo di autori di script](./media/run-scripts/script_authors_permissions.png)


## <a name="create-a-script"></a>Creare uno script

1. Nella console di Configuration Manager fare clic su **Raccolta software**.
2. Nell'area di lavoro **Raccolta software** fare clic su **Script**.
3. Nella scheda **Home** nel gruppo **Crea** fare clic su **Crea gruppo**.
4. Nella pagina **Script** della procedura guidata **Crea script** configurare le impostazioni seguenti:
    - In **Nome script** inserire il nome dello script. Anche se è possibile creare più script con lo stesso nome, l'uso di nomi duplicati rende più difficile individuare lo script necessario nella console di Configuration Manager.
    - **Lingua script**: attualmente sono supportati solo script di PowerShell.
    - **Importa**: importare uno script di PowerShell nella console. Lo script viene visualizzato nel campo **Script**.
    - **Cancella**: rimuove lo script corrente dal campo Script.
    - **Script**: visualizza lo script attualmente importato. È possibile modificare lo script in questo campo in base alle esigenze.
5. Completare la procedura guidata. Il nuovo script viene visualizzato nell'elenco **Script** con stato **In attesa di approvazione** . Prima di poter eseguire questo script nei dispositivi client, è necessario approvarlo. 

> [!IMPORTANT]
> Evitare di creare uno script per il riavvio del dispositivo o il riavvio dell'agente di Configuration Manager quando si usa la funzionalità Esegui script. Questa operazione potrebbe causare uno stato di riavvio continuo. Se necessario, sono disponibili miglioramenti delle funzionalità di notifica client che supportano il riavvio dei dispositivi, a partire da Configuration Manager versione 1710. La [colonna Riavvio in sospeso](../../core/clients/manage/manage-clients.md#restart-clients) può essere utile per identificare i dispositivi che richiedono un riavvio. 
> <!--SMS503978  -->

## <a name="script-parameters"></a>Parametri di script
*Introdotti con la versione 1710*  
L'aggiunta di parametri a uno script offre maggiore flessibilità per ogni attività. È possibile includere fino a 10 parametri. La sezione seguente descrive le attuali caratteristiche della funzionalità Esegui script con i parametri di script per tipi di dati *String* e *Integer*. Sono disponibili anche gli elenchi dei valori preimpostati. Se lo script ha tipi di dati non supportati, verrà generato un avviso.

Nella finestra di dialogo **Crea script** fare clic su **Parametri script** in **Script**.

Ognuno dei parametri di script è associato a una finestra di dialogo per l'aggiunta di altri dettagli e la convalida. Se è presente un parametro predefinito nello script, verrà enumerato nell'interfaccia utente dove può essere impostato. Configuration Manager non sovrascrive il valore predefinito perché non modifica mai lo script direttamente. I valori consigliati precompilati vengono forniti nell'interfaccia utente, ma Configuration Manager non consente l'accesso ai valori predefiniti in fase di esecuzione. È possibile ovviare a ciò modificando lo script in modo che contenga i valori predefiniti corretti. <!--17694323-->

>[!IMPORTANT]
> Nei valori dei parametri non è consentito l'apostrofo. </br></br>
> Esiste un problema noto in Configuration Manager versione 1802, a causa del quale i parametri con spazi non vengono passati allo script correttamente. Se nel parametro viene usato uno spazio, solo il primo elemento nel parametro viene passato allo script e tutti gli elementi dopo lo spazio non vengono passati. Gli amministratori possono creare uno script apposito sostituendo gli spazi con caratteri alternativi e convertendoli o usando altri metodi.


### <a name="parameter-validation"></a>Convalida dei parametri

Ogni parametro nello script ha una finestra di dialogo **Proprietà parametri script**, in cui è possibile aggiungere la convalida per il parametro. Dopo aver aggiunto la convalida, verranno restituiti errori quando si immette un valore che non soddisfa i requisiti di convalida per il parametro.

#### <a name="example-firstname"></a>Esempio: *FirstName*

In questo esempio è possibile impostare le proprietà del parametro stringa *FirstName*.

![Parametri di script - Stringa](./media/run-scripts/RS-parameters-string.png)


La sezione di convalida della finestra di dialogo **Proprietà dei parametri dello script** contiene i campi seguenti:

- **Lunghezza minima** - Numero minimo di caratteri del campo *FirstName*.
- **Lunghezza massima** - Numero massimo di caratteri del campo *FirstName*.
- **RegEx** - abbreviazione di *Espressione regolare*. Per altre informazioni sull'uso di espressioni regolari, vedere la sezione successiva *Uso della convalida con espressioni regolari*.
- **Errore personalizzato** - Utile per aggiungere un messaggio di errore personalizzato che sostituirà qualsiasi messaggio di errore di convalida del sistema.

#### <a name="using-regular-expression-validation"></a>Uso della convalida con espressioni regolari

Un'espressione regolare è una forma di programmazione compatta per controllare una stringa di caratteri rispetto a una convalida codificata. Ad esempio, si potrebbe verificare se manca un carattere alfabetico maiuscolo nel campo *FirstName* inserendo `[^A-Z]` nel campo *RegEx*.

L'elaborazione delle espressioni regolari per questa finestra di dialogo è supportata da .NET Framework. Per istruzioni sull'uso delle espressioni regolari, vedere [Espressione regolare .NET](https://docs.microsoft.com/dotnet/standard/base-types/regular-expressions) e [Linguaggio per le espressioni regolari](https://docs.microsoft.com/dotnet/standard/base-types/regular-expression-language-quick-reference).


## <a name="script-examples"></a>Esempi di script

Ecco alcuni esempi che mostrano gli script che è possibile usare con questa funzionalità.

### <a name="create-a-new-folder-and-file"></a>Creare una nuova cartella e un file

Questo script crea una nuova cartella e un file all'interno della cartella in base ai nomi specificati.

``` PowerShell
Param(
[Parameter(Mandatory=$True)]
[string]$FolderName,
[Parameter(Mandatory=$True)]
[string]$FileName
)

New-Item $FolderName -type directory
New-Item $FileName -type file
```

### <a name="get-os-version"></a>Recuperare la versione del sistema operativo

Questo script usa WMI per richiedere la versione del sistema operativo al computer.

``` PowerShell
Write-Output (Get-WmiObject -Class Win32_operatingSystem).Caption
```

## <a name="edit-or-copy-powershell-scripts"></a><a name="bkmk_psedit"></a> Modifica o copia degli script di PowerShell
<!--3705507-->
*Introdotti con la versione 1902*  
È possibile usare il comando **Modifica** o **Copia** per uno script di PowerShell esistente usato con la funzionalità **Esegui script**. Anziché ricreare uno script che è necessario modificare, ora è possibile modificarlo direttamente. Entrambe le azioni usano la stessa esperienza con procedura guidata presentata per la creazione di un nuovo script. Quando si modifica o si copia uno script, Configuration Manager non salva in modo permanente lo stato di approvazione.

> [!Tip]  
> Non modificare uno script che è in esecuzione nei client. L'esecuzione dello script originale non verrebbe completata e si potrebbero ottenere risultati diversi dal previsto da questi client.  

### <a name="edit-a-script"></a>Modificare uno script

1. Passare al nodo **Script** nell'area di lavoro **Raccolta software**.
1. Selezionare lo script da modificare e quindi fare clic su **Modifica** sulla barra multifunzione. 
1. Modificare o reimportare lo script nella pagina **Dettagli script**.
1. Fare clic su **Avanti** per visualizzare la pagina **Riepilogo** e quindi fare clic su **Chiudi** al termine della modifica.

### <a name="copy-a-script"></a>Copiare uno script

1. Passare al nodo **Script** nell'area di lavoro **Raccolta software**.
1. Selezionare lo script da copiare e quindi fare clic su **Copia** sulla barra multifunzione.
1. Rinominare lo script nel campo **Nome script** e apportare eventuali modifiche aggiuntive eventualmente necessarie.
1. Fare clic su **Avanti** per visualizzare la pagina **Riepilogo** e quindi fare clic su **Chiudi** al termine della modifica.


## <a name="run-a-script"></a>Esegui uno script

Dopo l'approvazione, uno script può essere eseguito su un singolo dispositivo o su una raccolta. Una volta avviata l'esecuzione, lo script viene eseguito rapidamente in un sistema ad alta priorità con timeout di un'ora. I risultati dello script vengono quindi restituiti tramite un sistema di messaggi di stato.

Per selezionare una raccolta di destinazioni per lo script:

1. Nella console di Configuration Manager fare clic su **Asset e conformità**.
2. Nell'area di lavoro Asset e conformità fare clic su **Raccolte dispositivi**.
3. Nell'elenco **Raccolte dispositivi** fare clic sulla raccolta di dispositivi in cui si desidera eseguire lo script.
4. Selezionare una raccolta a scelta e fare clic su **Esegui script**.
5. Nella pagina **Script** della procedura guidata **Esegui Script** scegliere uno script dall'elenco. Vengono visualizzati solo gli script approvati.
6. Fare clic su **Avanti** e completare la procedura guidata.

> [!IMPORTANT]
> Se lo script non viene eseguito, ad esempio perché il client di destinazione è spento entro il periodo di tempo di un'ora, è necessario eseguirlo di nuovo.

### <a name="target-machine-execution"></a>Esecuzione nel computer di destinazione

Lo script viene eseguito come account di *sistema* o *computer* nei client di destinazione. Questo account ha accesso di rete limitato. L'accesso dello script a posizioni e sistemi remoti deve essere eseguito di conseguenza.

## <a name="script-monitoring"></a>Monitoraggio dello script

Dopo aver avviato l'esecuzione di uno script in una raccolta di dispositivi, usare la procedura seguente per monitorare l'operazione. A partire dalla versione 1710, è possibile monitorare uno script in tempo reale durante la sua esecuzione ed è anche possibile restituire un report per un'esecuzione della funzionalità Esegui script specifica. I dati di stato dello script vengono puliti come parte dell'[attività di manutenzione Elimina operazioni client obsolete](../../core/servers/manage/reference-for-maintenance-tasks.md) o dell'eliminazione dello script.<br>

![Monitoraggio dello script - Stato di esecuzione dello script](./media/run-scripts/RS-monitoring-three-bar.png)

1. Nella console di Configuration Manager fare clic su **Monitoraggio**.
2. Nell'area di lavoro **Monitoraggio** fare clic su **Stato script**.
3. Nell'elenco **Stato script** sono visualizzati i risultati per ogni script eseguito nei dispositivi client. Un codice di uscita dello script uguale a **0** indica in genere che lo script è stato eseguito correttamente.
    - A partire da Configuration Manager 1802, l'output dello script viene troncato in corrispondenza di 4 KB per consentire una migliore esperienza di visualizzazione.  <!--510013-->
   
   ![Monitoraggio script - Script troncato](./media/run-scripts/Script-monitoring-truncated.png)

## <a name="script-output-in-1810"></a>Output dello script nella versione 1810

È possibile visualizzare l'output degli script dettagliato in formato JSON non elaborato o strutturato. Questo tipo di formattazione rende più facile leggere e analizzare l'output. Se lo script restituisce testo in formato JSON valido, è possibile visualizzare l'output dettagliato come **Output JSON** oppure **Output non elaborato**. In caso contrario, l'unica opzione è **Output dello script**.

### <a name="example-script-output-is-valid-json"></a>Esempio: output dello script in formato JSON valido
Comando: `$PSVersionTable.PSVersion`  

``` Output
Major  Minor  Build  Revision
-----  -----  -----  --------
5      1      16299  551
```

### <a name="example-script-output-isnt-valid-json"></a>Esempio: output dello script non in formato JSON valido
Comando: `Write-Output (Get-WmiObject -Class Win32_OperatingSystem).Caption`  

``` Output
Microsoft Windows 10 Enterprise
```

- I client 1810 restituiscono un output inferiore a 80 KB al sito su un canale di comunicazione rapida. Questa modifica migliora le prestazioni di visualizzazione dell'output di script o query.  

  - Se l'output di script o query è maggiore di 80 KB, il client invia i dati tramite un messaggio di stato.  
  - I client pre-1802 continuano a usare i messaggi di stato.

## <a name="script-output-pre-1810"></a>Output dello script pre-1810

- A partire da Configuration Manager versione 1802, l'output dello script viene restituito con la formattazione JSON. Questo formato restituisce in modo coerente un output dello script leggibile. 
- Gli script con un risultato sconosciuto o dove il client era offline, non vengono visualizzati nei grafici o nel set di dati. <!--507179-->
- Evitare di restituire un output troppo grande poiché verrà troncato in corrispondenza di 4 KB. <!--508488-->
- Alcune funzionalità con la formattazione dell'output dello script non sono disponibili quando si esegue Configuration Manager versione 1802 o successiva con una versione di livello inferiore del client. <!--508487-->
    - Con un client di Configuration Manager precedente alla versione 1802 viene restituito un output di stringhe.
    -  Con un client di Configuration Manager versione 1802 e successive viene restituita la formattazione JSON.
        - Ad esempio, si può ottenere il risultato TEXT in una versione del client e "TEXT", ovvero con l'output racchiuso tra virgolette doppie, in un'altra versione. Questi risultati verranno inseriti nel grafico come due categorie diverse.
        - Se questo comportamento costituisce un problema, prendere in considerazione l'esecuzione dello script su due raccolte diverse. Una con i client precedenti alla versione 1802 e un'altra con i client 1802 e versioni successive. In alternativa, è possibile convertire un oggetto enum in un valore stringa negli script in modo da visualizzarlo correttamente nella formattazione JSON. 
- Convertire un oggetto enum in un valore stringa negli script in modo da visualizzarlo correttamente nella formattazione JSON. <!--508377-->

   ![Convertire un oggetto enum in un valore stringa](./media/run-scripts/enum-tostring-JSON.png)

## <a name="log-files"></a>File di registro

A partire dalla versione 1810, la registrazione è stata estesa per agevolare la risoluzione dei problemi.

- Nel client, per impostazione predefinita in C:\Windows\CCM\logs:  
  - **Scripts.log**  
  - **CcmMessaging.log**  

- In MP, per impostazione predefinita in C:\SMS_CCM\Logs:
  - **MP_RelayMsgMgr.log**  

- Nel server del sito, per impostazione predefinita in C:\Programmi\Configuration Manager\Logs:
  - **SMS_Message_Processing_Engine.log**

## <a name="see-also"></a>Vedere anche

- [Configurare l'amministrazione basata su ruoli per Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md)
- [Nozioni fondamentali sull'amministrazione basata su ruoli](../../core/understand/fundamentals-of-role-based-administration.md)
