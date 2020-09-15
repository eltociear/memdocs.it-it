---
title: CMPivot per i dati in tempo reale
titleSuffix: Configuration Manager
description: Informazioni su come usare CMPivot in Configuration Manager per eseguire query sui client in tempo reale.
ms.date: 09/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 32e2d6b9-148f-45e2-8083-98c656473f82
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: fa96d09302b9b4cd908880e97e1735fff5f43743
ms.sourcegitcommit: d4ed7b4369389fd8ab07d28a7fa507797b6c6e57
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/10/2020
ms.locfileid: "89643580"
---
# <a name="cmpivot-for-real-time-data-in-configuration-manager"></a>CMPivot per i dati in tempo reale in Configuration Manager

<!--1358456-->

*Si applica a: Configuration Manager (Current Branch)*

Configuration Manager ha sempre fornito un archivio centralizzato di grandi dimensioni per i dati dei dispositivi, usato dai clienti per i report. Il sito in genere raccoglie questi dati su base settimanale. A partire dalla versione 1806, CMPivot è una nuova utilità inclusa nella console che ora consente l'accesso allo stato in tempo reale dei dispositivi nell'ambiente in uso. Esegue immediatamente una query su tutti i dispositivi connessi nella raccolta di destinazione e restituisce i risultati. Filtrare quindi e raggruppare questi dati nello strumento. La disponibilità di dati in tempo reale dai client online consente di rispondere alle domande aziendali, risolvere i problemi e rispondere agli eventi imprevisti di sicurezza in modo più veloce.

Ad esempio, perla [mitigazione delle vulnerabilità del canale laterale di esecuzione speculativa](https://techcommunity.microsoft.com/t5/configuration-manager-blog/additional-guidance-to-mitigate-speculative-execution-side/ba-p/274974), uno dei requisiti prevede l'aggiornamento del BIOS di sistema. È possibile usare CMPivot per eseguire rapidamente query sulle informazioni del BIOS di sistema e trovare i client non conformi.

 > [!IMPORTANT]  
 > - Alcuni software di sicurezza possono bloccare gli script in esecuzione da c:\windows\ccm\scriptstore. Ciò può impedire la corretta esecuzione delle query CMPivot. Alcuni software di sicurezza possono anche generare avvisi o eventi di controllo quando si esegue CMPivot con PowerShell.
 > - Alcuni software antimalware possono attivare inavvertitamente eventi per le funzionalità Esegui script o CMPivot di Configuration Manager. È consigliabile escludere %windir%\CCM\ScriptStore in modo che il software antimalware consenta l'esecuzione di tali funzionalità senza interferenze.


## <a name="prerequisites"></a>Prerequisiti

Per usare CMPivot sono necessari i componenti seguenti:

- Aggiornare i dispositivi di destinazione alla versione più recente del client Configuration Manager.  

- I client di destinazione richiedono almeno PowerShell versione 4.

- Per raccogliere dati per le entità seguenti, i client di destinazione richiedono PowerShell versione 5.0:  
  - Administrators
  - Connessioni
  - IPConfig
  - SMBConfig

- CMPivot e il programma di installazione di [Microsoft Edge](../../../apps/deploy-use/deploy-edge.md) sono firmati con il certificato di **firma del codice Microsoft**. Se il certificato non è elencato nell'archivio **Autori attendibili**, sarà necessario aggiungerlo. In caso contrario, CMPivot e il programma di installazione di Microsoft Edge non verranno eseguiti quando i criteri di esecuzione di PowerShell sono impostati su **AllSigned**. <!--7585106-->

## <a name="permissions"></a>Autorizzazioni

Le autorizzazioni seguenti sono necessarie per CMPivot:

- **Lettura** per l'oggetto **Script SMS**
- **Esecuzione degli script** per la **raccolta**
   - In alternativa, a partire dalla versione 1906, è possibile usare **Esegui CMPivot** per la **raccolta**.
- **Lettura** per i **report di inventario**
- L'ambito predefinito.

> [!NOTE]
> - **Esegui script** è un super set dell'autorizzazione **Esegui CMPivot**.
> - A partire dalla versione 1906, [sono state aggiunte le autorizzazioni per CMPivot](cmpivot-changes.md#bkmk_cmpivot_secadmin1906) al ruolo **Amministratore della protezione** predefinito di Configuration Manager.
 
## <a name="limitations"></a>Limitazioni

- In una gerarchia connettere la console di Configuration Manager a un *sito primario* per eseguire CMPivot. L'azione **Avvia CMPivot** non viene visualizzata nella console quando è connessa a un sito di amministrazione centrale.
  - A partire da Configuration Manager versione 1902, è possibile eseguire CMPivot da un sito di amministrazione centrale. In alcuni ambienti sono necessarie autorizzazioni aggiuntive. Per altre informazioni, vedere l'articolo sulle [modifiche a CMPivot nella versione 1902](cmpivot-changes.md#bkmk_cmpivot1902).

- CMPivot restituisce solo i dati per i client connessi al sito corrente.  

- Se una raccolta contiene dispositivi di un altro sito, i risultati di CMPivot provengono solo dai dispositivi nel sito corrente.  

- Non è possibile personalizzare le proprietà delle entità, le colonne per i risultati o le azioni sui dispositivi.  

- In un computer che esegue la console di Configuration Manager si può eseguire una sola istanza di CMPivot per volta.  

- Nella versione 1806, la query per l'entità **Administrators** funziona solo se il gruppo è denominato "Administrators". Non funziona se il nome del gruppo è localizzato. Ad esempio, "Administrateurs" in francese.<!--SCCMDocs issue 759-->  


## <a name="start-cmpivot"></a>Avviare CMPivot

1. Nella console di Configuration Manager connettersi al sito primario. Passare all'area di lavoro **Asset e conformità** e selezionare il nodo **Raccolte dispositivi**. Selezionare una raccolta di destinazione e fare clic su **Avvia CMPivot** sulla barra multifunzione per avviare lo strumento. Se questa opzione non è visualizzata, verificare le configurazioni seguenti:  
   - Verificare con un amministratore del sito che l'account abbia le autorizzazioni necessarie. Per altre informazioni, vedere [Prerequisiti](#prerequisites).  
   - Connettere la console a un *sito primario*.  

2. L'interfaccia fornisce ulteriori informazioni sull'uso dello strumento.  

     - Immettere manualmente le stringhe di query nella parte superiore oppure fare clic sui collegamenti nella documentazione in linea.  

     - Fare clic su una delle **Entità** per aggiungerla alla stringa di query.  

     - I collegamenti per **Operatori tabella**, **Funzioni di aggregazione** e **Funzioni scalari** consentono di aprire la documentazione di riferimento del linguaggio nel Web browser. CMPivot usa il [linguaggio di query Kusto](/azure/kusto/query/).  

3. Tenere la finestra CMPivot aperta per visualizzare i risultati dai client. Quando si chiude la finestra CMPivot, la sessione è completa.
   - Se la query è stata inviata, i client inviano comunque un messaggio di stato al server.  



## <a name="how-to-use-cmpivot"></a>Come usare CMPivot

![Esempio di finestra CMPivot](media/1358456-cmpivot-sample.png)

La finestra CMPivot presenta gli elementi seguenti:  

1. L'attuale raccolta di destinazione di CMPivot è visualizzata nella barra del titolo nella parte superiore e nella barra di stato nella parte inferiore della finestra. Ad esempio, "PM_Team_Machines" nello screenshot precedente.  

2. Nel riquadro a sinistra sono elencate le **entità** disponibili nei client. Alcune entità si basano su WMI, mentre altre usano PowerShell per ottenere i dati dai client.   

    - Fare clic con il pulsante destro del mouse su un'entità per le azioni seguenti:  

       - **Inserisci**: aggiunge l'entità alla query nella posizione corrente del cursore. La query non viene eseguita automaticamente. Questa azione è quella predefinita quando si fa doppio clic su un'entità. Usare questa azione quando si compila una query.  

       - **Esegui query su tutto**: esegue una query per questa entità includendo tutte le proprietà. Usare questa azione per eseguire rapidamente una query per una singola entità.  

       - **Query per dispositivo**: esegue una query per questa entità e raggruppa i risultati. Ad esempio: `Disk | summarize dcount( Device ) by Name`  

    - Espandere un'entità per visualizzare le proprietà specifiche disponibili per ogni entità. Fare doppio clic su una proprietà per aggiungerla alla query nella posizione corrente del cursore.  

3. La scheda **Home** contiene le informazioni generali su CMPivot, inclusi i collegamenti alle query di esempio e alla documentazione di supporto.  

4. La scheda **Query** contiene il riquadro della query, il riquadro dei risultati e la barra di stato. La scheda Query è selezionata nell'esempio dello screenshot precedente.  

5. Nel riquadro della query si compila o si digita una query da eseguire nei client della raccolta.  

    - CMPivot usa un subset del [linguaggio di query Kusto](/azure/kusto/query/).  

    - Tagliare, copiare o incollare il contenuto nel riquadro della query.  
    <!-- markdownlint-disable MD038 -->
    - Per impostazione predefinita, questo riquadro usa IntelliSense. Se ad esempio si inizia a digitare `D`, IntelliSense suggerisce tutte le entità che iniziano con tale lettera. Selezionare un'opzione e premere TAB per inserirla. Digitare un carattere barra verticale e uno spazio `| `. IntelliSense suggerirà tutti gli operatori di tabella. Inserire `summarize` e digitare uno spazio. IntelliSense suggerirà tutte le funzioni di aggregazione. Per altre informazioni su questi operatori e funzioni, fare clic sulla scheda **Home** in CMPivot.  

    - Il riquadro della query fornisce anche le opzioni seguenti:  

        - Eseguire la query.  

        - Spostarsi indietro e avanti nell'elenco della cronologia delle query.  

        - Creare una raccolta di appartenenze dirette.  

        - Esportare i risultati della query in un file CSV o negli Appunti.  

6. Il riquadro dei risultati visualizza i dati restituiti dai client attivi per la query.  

   - Le colonne disponibili variano a seconda dell'entità e della query.  

   - Fare clic su un nome di colonna per ordinare i risultati in base a tale proprietà.  

   - Fare clic con il pulsante destro del mouse su un nome di colonna per raggruppare i risultati in base alle stesse informazioni di tale colonna o per ordinare i risultati.  

   - Fare clic con il pulsante destro del mouse su un nome di dispositivo per eseguire le azioni aggiuntive seguenti sul dispositivo:  

      - **Pivot in**: esegue una query per un'altra entità su questo dispositivo.
         - A partire dalla versione 2006, **Pivot in** è stato sostituito da **Pivot dispositivo**. Per altre informazioni, vedere l'articolo sulle [modifiche a CMPivot nella versione 2006](cmpivot-changes.md#bkmk_2006).

      - **Esegui script**: avvia la procedura guidata Esegui script per eseguire uno script di PowerShell esistente su questo dispositivo. Per altre informazioni, vedere [Eseguire uno script](../../../apps/deploy-use/create-deploy-scripts.md#run-a-script).  

      - **Controllo remoto**: avvia una sessione di Controllo remoto di Configuration Manager su questo dispositivo. Per altre informazioni, vedere [Come amministrare un computer client Windows in remoto](../../clients/manage/remote-control/remotely-administer-a-windows-client-computer.md).  

      - **Esplora inventario risorse**: avvia Esplora inventario risorse di Configuration Manager per questo dispositivo. Per altre informazioni, vedere [Visualizzare l'inventario hardware](../../clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md) o [Visualizzare l'inventario software](../../clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

   - Fare clic con il pulsante destro del mouse su una cella non di dispositivo per eseguire le azioni aggiuntive seguenti:  

     - **Copia**: copia il testo della cella negli Appunti.  

     - **Mostra dispositivi con**: esegue una query dei dispositivi con questo valore della proprietà. Ad esempio, nei risultati della query `OS` selezionare questa opzione in una cella della riga Version: `OS | summarize countif( (Version == '10.0.17134') ) by Device | where (countif_ > 0)`  

     - **Mostra dispositivi senza**: esegue una query dei dispositivi senza questo valore della proprietà. Ad esempio, nei risultati della query `OS` selezionare questa opzione in una cella della riga Version: `OS | summarize countif( (Version == '10.0.17134') ) by Device | where (countif_ == 0) | project Device`  

     - **Usa Bing**: avvia il Web browser predefinito in https://www.bing.com con questo valore come stringa di query.  

   - Fare clic su un testo con collegamento ipertestuale per trasformare tramite Pivot la vista su tali informazioni specifiche.  

   - Il riquadro dei risultati non visualizza più di 20.000 righe. Modificare la query per filtrare ulteriormente i dati oppure riavviare CMPivot in una raccolta più piccola.  

7. La barra di stato mostra le informazioni seguenti (da sinistra a destra):  

   - Lo stato della query corrente per la raccolta di destinazione. Questo stato include:  
     - Il numero di client attivi che hanno completato la query (3)  
     - Il numero di client totali (5)  
     - Il numero di client offline (2)  
     - I client che hanno restituito un errore (0)  

       ad esempio `Query completed on 3 of 5 clients (2 clients offline and 0 failure)`  

   - L'ID dell'operazione client. ad esempio `id(16780221)`  

   - La raccolta corrente. ad esempio `PM_Team_Machines`  

   - Il numero totale di righe nel riquadro dei risultati. Ad esempio: `1 objects`  

> [!TIP]
> Per eseguire nuovamente la query CMPivot corrente nei client, tenere premuto **CTRL** e fare clic su **Esegui**.

## <a name="example-scenarios"></a>Scenari di esempio

Le sezioni seguenti forniscono esempi di come sia possibile usare CMPivot nell'ambiente:


### <a name="example-1-stop-a-running-service"></a>Esempio 1: Arrestare un servizio in esecuzione

L'amministratore della sicurezza chiede di arrestare e disabilitare il servizio Browser di computer al più presto su tutti i dispositivi del reparto contabilità. Si avvia CMPivot in una raccolta per tutti i dispositivi della contabilità e si seleziona **Esegui query su tutto** nell'entità **Service**. 

`Service`

Quando vengono visualizzati i risultati, si fa clic con il pulsante destro del mouse sulla colonna **Name** e si sceglie **Raggruppa per**. 

`Service | summarize dcount( Device ) by Name`

Nella riga del servizio **Browser** si fa clic sul numero con collegamento ipertestuale nella colonna **dcount_** . 

`Service | where (Name == 'Browser') | summarize count() by Device`

Si selezionano tutti i dispositivi, si fa clic con il pulsante destro del mouse sulla selezione e si sceglie **Esegui script**. Questa azione avvia la procedura guidata Esegui Script, da cui si esegue uno script esistente per arrestare e disabilitare un servizio. Con CMPivot si risponde rapidamente all'evento imprevisto di sicurezza per tutti i computer attivi, visualizzando i risultati nella procedura guidata Esegui Script. Si termina quindi con la creazione di una linea di base di configurazione per correggere gli altri computer della raccolta perché diventeranno attivi in futuro. 

![Esempio di CMPivot per il servizio Browser e l'azione Esegui script](media/cmpivot-example1.png)


### <a name="example-2-proactively-resolve-application-failures"></a>Esempio 2: Risolvere in modo proattivo gli errori delle applicazioni  

Per assicurare reazioni proattive con la manutenzione operativa, una volta alla settimana si esegue CMPivot su una raccolta di server gestiti e si seleziona **Esegui query su tutto** nell'entità **AppCrash**. Si fa clic con il pulsante destro del mouse sulla colonna **FileName** e si sceglie **Ordinamento crescente**. Un dispositivo restituisce sette risultati per sqlsqm.exe con un timestamp corrispondente alle 03:00 circa ogni giorno. Si seleziona il nome file in una delle righe, si fa clic con il pulsante destro del mouse e si sceglie **Usa Bing**. Esplorando i risultati della ricerca nel Web browser, si trova un articolo del supporto tecnico Microsoft su questo problema con la risoluzione e altre informazioni. 


### <a name="example-3-bios-version"></a>Esempio 3: Versione BIOS

Per [mitigare le vulnerabilità del canale laterale di esecuzione speculativa](https://techcommunity.microsoft.com/t5/configuration-manager-blog/additional-guidance-to-mitigate-speculative-execution-side/ba-p/274974), uno dei requisiti prevede l'aggiornamento del BIOS di sistema. Si inizia con una query dell'entità **BIOS**, quindi si **raggruppa in base alla** proprietà **Version**. Si fa quindi clic con il pulsante destro del mouse su un valore specifico, ad esempio "LENOVO - 1140", e si sceglie **Mostra dispositivi con**.  

`Bios | summarize countif( (Version == 'LENOVO - 1140') ) by Device | where (countif_ > 0)`


### <a name="example-4-free-disk-space"></a>Esempio 4: Spazio libero su disco

È necessario archiviare temporaneamente un file di grandi dimensioni in un file server di rete, ma non si è certi di quale abbia la capacità sufficiente. Avviare CMPivot su una raccolta di file server ed eseguire una query sull'entità **Disk**. Modificare la query in modo che CMPivot restituisca rapidamente un elenco dei server attivi con i dati di archiviazione in tempo reale:  

`Disk | where (Description == 'Local Fixed Disk') | where isnotnull( FreeSpace ) | order by FreeSpace asc`


## <a name="cmpivot-standalone"></a><a name="bkmk_standalone"></a> Modalità autonoma per CMPivot

[!INCLUDE [CMPivot standalone](includes/cmpivot-standalone.md)]


 
## <a name="inside-cmpivot"></a>Informazioni su CMPivot

CMPivot invia le query ai client usando il "canale rapido" di Configuration Manager. Questo canale di comunicazione dal server al client viene usato anche da altre funzionalità, ad esempio le azioni di notifica client, lo stato del client ed Endpoint Protection. I client restituiscono i risultati tramite il sistema di messaggi di stato in modo altrettanto rapido. I messaggi di stato vengono temporaneamente archiviati nel database. Per altre informazioni sulle porte usate per la notifica client, vedere l'articolo relativo alle [porte](../../plan-design/hierarchy/ports.md#BKMK_PortsClient-MP).

Le query e i risultati contengono solo testo. Le entità **InstallSoftware** e **Process** restituiscono alcuni dei set di risultati più grandi. Durante i test delle prestazioni, le dimensioni del file di un messaggio di stato da un client per queste query non hanno superato **1 KB**. Questa query monouso, eseguita a un ambiente di grandi dimensioni con 50.000 client attivi, genererebbe meno di 50 MB di dati in rete. Tutti gli elementi sottolineati nella home page restituiranno meno di 1 KB di informazioni per client.

![Esempio di entità sottolineate in CMPivot](media/cmpivot-underlined-entities.png)

A partire da Configuration Manager 1810, CMPivot è in grado di eseguire query sui dati di inventario hardware, incluse le classi di inventario hardware estese. Queste nuove entità (non sottolineate nella home page) possono restituire set di dati molto più grandi, a seconda della quantità di dati definita per una data proprietà di inventario hardware. Ad esempio, l'entità "InstalledExecutable" potrebbe restituire più MB di dati per ogni client, in base ai dati specifici su cui si esegue la query. Prestare attenzione alle prestazioni e alla scalabilità dei sistemi quando usando CMPivot le raccolte di dimensioni maggiori restituiscono set di dati di inventario hardware più grandi.

Una query raggiunge il timeout dopo un'ora. Ad esempio, una raccolta include 500 dispositivi e 450 client sono attualmente online. I dispositivi attivi ricevono la query e restituiscono i risultati quasi immediatamente. Se si lascia aperta la finestra CMPivot, anche gli altri 50 client, non appena passano online, ricevono la query e restituiscono i risultati. 

## <a name="log-files"></a>File di registro

 Le interazioni di CMPivot vengono registrate nei file di log seguenti:

**Lato server:**
- SmsProv.log
- BgbServer.log
- StateSys.log

**Lato client:**
- CcmNotificationAgent.log
- Scripts.log
- StateMessage.log

Per altre informazioni, vedere [File di log](../../plan-design/hierarchy/log-files.md) e [Risoluzione dei problemi di CMPivot](cmpivot-tsg.md).

## <a name="next-steps"></a>Passaggi successivi

- [Modifiche a CMPivot](cmpivot-changes.md)
- [Risoluzione dei problemi di CMPivot](cmpivot-tsg.md)
- [Creare ed eseguire script di PowerShell](../../../apps/deploy-use/create-deploy-scripts.md)