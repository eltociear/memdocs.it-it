---
title: Funzionalità nella Technical Preview 1612
titleSuffix: Configuration Manager
description: Informazioni sulle funzionalità disponibili nella versione Technical Preview 1612 per Configuration Manager.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bceab2e8-2f05-4a17-9ac8-a7a558670fb7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 0c2464bfba05d640868af7d5c8be7c32c0999946
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705409"
---
# <a name="capabilities-in-technical-preview-1612-for-configuration-manager"></a>Funzionalità della versione Technical Preview 1612 per Configuration Manager

*Si applica a: Configuration Manager (Technical Preview Branch)*



Questo articolo presenta le funzionalità disponibili nella Technical Preview per Configuration Manager versione 1612. È possibile installare questa versione per aggiornare e aggiungere nuove funzionalità al sito di Technical Preview di Configuration Manager. Prima di installare questa versione Technical Preview, consultare l'argomento introduttivo [Technical Preview per Center Configuration Manager](../../core/get-started/technical-preview.md) per acquisire familiarità con i requisiti generali e con le limitazioni per l'uso di una versione Technical Preview, con le modalità di aggiornamento tra le versioni e con le modalità per offrire commenti e suggerimenti sulle funzionalità di una versione Technical Preview.    


**Di seguito sono riportate le nuove funzionalità disponibili con questa versione.**  

## <a name="the-data-warehouse-service-point"></a>Punto di servizio Data Warehouse
A partire dalla versione Technical Preview 1612, il punto di servizio Data warehouse consente di archiviare e creare report sui dati cronologici a lungo termine per la distribuzione di Configuration Manager. Ciò è possibile tramite sincronizzazioni automatizzate dal database del sito di Configuration Manager a un database di data warehouse. Queste informazioni diventano quindi accessibili dal punto di Reporting Services.

Per impostazione predefinita, quando si installa il nuovo ruolo del sistema del sito, Configuration Manager crea il database del data warehouse nell'istanza di SQL Server specificata dall'utente. Il data warehouse supporta fino a 2 TB di dati, con timestamp per il rilevamento delle modifiche.  Per impostazione predefinita, i dati che vengono sincronizzati dal database del sito includono i gruppi di dati per i dati globali, i dati del sito, il proxy globale, i dati del cloud e le viste del database. È anche possibile modificare l'elenco degli elementi sincronizzati includendo tabelle aggiuntive o escludendo determinate tabelle appartenenti ai set di replica predefiniti.
I dati sincronizzati per impostazione predefinita includono informazioni su:
- Integrità dell'infrastruttura
- Sicurezza
- Conformità
- Malware   
- Distribuzioni software
- Dettagli relativi all'inventario. La cronologia dell'inventario, tuttavia, non è sincronizzata

Oltre all'installazione e alla configurazione del database del data warehouse, viene eseguita l'installazione di diversi nuovi report che semplificano la ricerca di questi dati e sono facili da generare.

### <a name="data-warehouse-dataflow"></a>Flusso dei dati del data warehouse   
![Datawarehouse_flow](./media/datawarehouse.png)

| Passaggio         | Dettagli  |
|:------:|-----------|  
| **1** | Il server del sito trasferisce e archivia i dati nel database del sito.  |  
| **2** | In base alla pianificazione e alla configurazione, il punto di servizio Data warehouse recupera dati dal database del sito.  |  
| **3** | Il punto di servizio Data warehouse trasferisce e archivia una copia dei dati sincronizzati nel database del data warehouse. |  
| **A** | Usando report predefiniti, viene creata una richiesta di dati, che viene passata al punto di Reporting Services tramite SQL Server Reporting Services. |  
| **B** | La maggior parte dei report sono usati per informazioni correnti e queste richieste vengono eseguite tramite il database del sito. |  
| **C** | Se un report richiede dati cronologici, tramite un report con *Categoria* corrispondente a **Data warehouse** la richiesta viene eseguita tramite il database del data warehouse.   |  

### <a name="prerequisites-for-the-data-warehouse-service-point-and-database"></a>Prerequisiti per il punto di servizio e per il database del data warehouse
- Nella gerarchia deve essere installato un ruolo del servizio del sito del punto di Reporting Services.
- Il computer in cui si installa il ruolo del sistema del sito richiede .NET Framework 4.5.2 o versioni successive.
- L'account computer del computer in cui si installa il ruolo del sistema del sito deve avere le autorizzazioni di amministratore locale per il computer che ospiterà il database del data warehouse.
- L'account amministrativo usato per installare il ruolo del sistema del sito deve essere un DBO nell'istanza di SQL Server che ospiterà il database del data warehouse.  
- Il database è supportato:
  - Con SQL Server 2012 o versione successiva, Enterprise Edition o Datacenter Edition.
  - In un'istanza predefinita o denominata
  - In un *cluster di SQL Server*. Questa configurazione dovrebbe funzionare, ma non è stata testata e il supporto viene offerto secondo il criterio del massimo sforzo.
  - Se condivide il percorso con il database del sito o con il database del punto di Reporting Services. È tuttavia consigliabile installarlo in un server separato.  
- L'account usato come *Account punto di Reporting Services* deve avere l'autorizzazione **db_datareader** per il database del data warehouse.  
- Il database non è supportato in un *gruppo di disponibilità SQL Server AlwaysOn*.

### <a name="install-the-data-warehouse"></a>Installare il data warehouse
Il ruolo del sistema del sito del data warehouse deve essere installato in un sito di amministrazione centrale o in un sito primario tramite la **Aggiunta guidata ruoli del sistema del sito** o la **Creazione guidata server del sistema sito**. Per altre informazioni, vedere [Installare ruoli del sistema del sito](../servers/deploy/configure/install-site-system-roles.md). Una gerarchia supporta più istanze di questo ruolo, ma presso ogni sito è supportata una sola istanza.  

Quando si installa il ruolo, Configuration Manager crea il database del data warehouse nell'istanza di SQL Server specificata dall'utente. Se si specifica il nome di un database esistente, come si farebbe se si [spostasse il database del data warehouse in una nuova istanza di SQL Server](#move-the-data-warehouse-database), Configuration Manager non crea un nuovo database, ma usa invece quello specificato dall'utente.

#### <a name="configurations-used-during-installation"></a>Configurazioni usate durante l'installazione
Usare le informazioni seguenti per eseguire l'installazione del ruolo del sistema del sito:

Pagina **Selezione ruolo del sistema**:  
Prima che la procedura guidata visualizzi l'opzione di selezione e installazione del punto di servizio Data warehouse, è necessario avere installato un punto di Reporting Services.

Pagina **Generale**: sono necessarie le informazioni generali seguenti:
- **Impostazioni del database di Configuration Manager:**   
  - **Nome server**: specificare l'FQDN del server che ospita il database del sito. Se non si usa un'istanza predefinita di SQL Server, è necessario specificare l'istanza dopo l'FQDN nel formato seguente: ***&lt;FQDN_Sqlserver>\&lt;Nome_istanza>***
  - **Nome database**: specificare il nome del database del sito.
  - **Verifica** Fare clic su **Verifica** per verificare che la connessione al database del sito funzioni correttamente.
</br></br>
- **Impostazioni del database del data warehouse:**
  - **Nome server**: specificare l'FQDN del server che ospita il database e il punto di servizio del data warehouse. Se non si usa un'istanza predefinita di SQL Server, è necessario specificare l'istanza dopo l'FQDN nel formato seguente: ***&lt;FQDN_Sqlserver>\&lt;Nome_istanza>***
  - **Nome database**: specificare l'FQDN del database del data warehouse.  Configuration Manager creerà il database con questo nome. Se si specifica un nome di database già esistente nell'istanza di SQL Server, Configuration Manager userà il database corrispondente.
  - **Verifica** Fare clic su **Verifica** per verificare che la connessione al database del sito funzioni correttamente.

Pagina **Impostazioni di sincronizzazione**:   
- **Impostazioni per i dati:**
  - **Replication groups to synchronize** (Gruppi di replica da sincronizzare): selezionare i gruppi di dati da sincronizzare. Per informazioni sui diversi tipi di gruppi di dati, vedere [Replica di database](../plan-design/hierarchy/data-transfers-between-sites.md#bkmk_dbrep) e **Viste distribuite** in [Trasferimenti di dati tra siti](../plan-design/hierarchy/data-transfers-between-sites.md).
  - **Tables included to synchronize** (Tabelle incluse da sincronizzare): specificare il nome di ogni tabella aggiuntiva da sincronizzare. Separare più tabelle tramite la virgola. Queste tabelle verranno sincronizzate dal database del sito in aggiunta ai gruppi di replica selezionati.
  - **Tables excluded to synchronize** (Tabelle escluse da sincronizzare): specificare il nome di tabelle singole da escludere dai gruppi di replica da sincronizzare. Le tabelle specificate verranno escluse. Separare più tabelle tramite la virgola.
- **Impostazioni di sincronizzazione:**
  - **Intervallo di sincronizzazione (minuti)** : specificare un valore in minuti. Quando l'intervallo termina, viene avviata una nuova sincronizzazione. Supporta un intervallo compreso tra 60 e 1440 minuti (24 ore).
  - **Pianificazione**: specificare i giorni in cui si vuole eseguire la sincronizzazione.

**Accesso al punto di reporting**:   
Dopo aver installato il ruolo del data warehouse, assicurarsi che l'account usato come *Account punto di Reporting Services* abbia l'autorizzazione **db_datareader** per il database del data warehouse.

#### <a name="troubleshoot-installation-and-data-synchronization"></a>Risoluzione dei problemi di installazione e di sincronizzazione dei dati
Usare i registri seguenti per analizzare i problemi dell'installazione del punto di servizio Data warehouse o della sincronizzazione dei dati:
- **DWSSMSI.log** e **DWSSSetup.log**: usare questi registri per analizzare gli errori che si verificano durante l'installazione del punto di servizio Data warehouse.
- **Microsoft.ConfigMgrDataWarehouse.log**: usare questo registro per analizzare la sincronizzazione dei dati tra il database del sito e il database del data warehouse database.

### <a name="reporting"></a>Reporting
Dopo aver installato un ruolo del sistema del sito del Data Warehouse, nel punto di Reporting Services sono disponibili i report seguenti con *Categoria* corrispondente a **Data Warehouse:**

|Report                   | Dettagli                                  |
|-------------------------|------------------------------------------|
| **Report Distribuzione applicazioni** | Visualizza i dettagli per la distribuzione di applicazioni per un'applicazione e un computer specifici.|
| **Endpoint Protection and Software Update Compliance Report** (Report Endpoint Protection e di conformità agli aggiornamenti software)   | Visualizza i computer in cui mancano aggiornamenti software.|
| **Report dell'inventario generale dell'hardware**  | Visualizza tutto l'inventario dell'hardware per un computer specifico.|
| **Report dell'inventario generale del software**  | Visualizza tutto l'inventario del software per un computer specifico.|
| **Panoramica dell'integrità dell'infrastruttura**  |Visualizza una panoramica dell'integrità dell'infrastruttura di Configuration Manager.|
| **Elenco del malware rilevato**  |Visualizza il malware che è stato rilevato nell'organizzazione.|
| **Report riepilogativo distribuzione software** | Riepilogo della distribuzione del software per un annuncio e un computer specifici.|

### <a name="move-the-data-warehouse-database"></a>Spostare il database del data warehouse
Per spostare il database del data warehouse in un nuovo SQL Server, procedere come segue:

1. Esaminare la configurazione corrente del database e registrare i dettagli di configurazione, ad esempio:  
   - I gruppi di dati da sincronizzare
   - Le tabelle incluse o escluse dalla sincronizzazione       

   I gruppi di dati e le tabelle verranno riconfigurati dopo il ripristino del database in un nuovo server e la reinstallazione del ruolo del sistema del sito.  

2. Usare SQL Server Management Studio per eseguire il backup del database del data warehouse e quindi di nuovo per ripristinare il database all'interno di SQL Server nel nuovo computer che ospiterà il data warehouse.

   Dopo aver ripristinato il database nel nuovo server, assicurarsi che le autorizzazioni di accesso al database per il nuovo database del data warehouse siano le stesse del data warehouse originale.

3. Usare la console di Configuration Manager per rimuovere il ruolo del sistema del sito punto di servizio Data warehouse dal server corrente.

4. Installare un nuovo punto di servizio Data warehouse e specificare il nome del nuovo SQL Server e dell'istanza che ospita il database del data warehouse appena ripristinato.

5. Dopo l'installazione del ruolo del sistema del sito, lo spostamento è completato.

È possibile esaminare i registri di Configuration Manager seguenti per verificare che il ruolo del sistema del sito sia stato reinstallato correttamente:  
- **DWSSMSI.log** e **DWSSSetup.log**: usare questi registri per analizzare gli errori che si verificano durante l'installazione del punto di servizio Data warehouse.
- **Microsoft.ConfigMgrDataWarehouse.log**: questo log consente di analizzare la sincronizzazione dei dati tra il database del sito e il database del data warehouse.


## <a name="content-library-cleanup-tool"></a>Strumento di pulizia della raccolta contenuto
A partire dalla versione Technical Preview 1612 è possibile usare un nuovo strumento da riga di comando (**ContentLibraryCleanup.exe**) per rimuovere contenuto non più associato a un pacchetto o a un'applicazione da un punto di distribuzione (contenuto orfano). Questo strumento è detto strumento di pulizia della raccolta contenuto.

Questo strumento interessa solo il contenuto nel punto di distribuzione specificato quando si esegue lo strumento. Quest'ultimo non può rimuovere contenuto dalla raccolta contenuto nel server del sito.

Dopo aver installato la versione Technical Preview 1612, è possibile trovare il file **ContentLibraryCleanup.exe** nella cartella *%CM_Installation_Path%\cd.latest\SMSSETUP\TOOLS\ContentLibraryCleanup\* nel server del sito della versione Technical Preview.

Lo strumento rilasciato con questa versione Technical Preview è destinato a sostituire le versioni precedenti di strumenti simili rilasciati per i prodotti Configuration Manager precedenti. Questa versione dello strumento smetterà di funzionare dopo il 1° marzo 2017. Fino a quel momento, tuttavia, verranno rilasciate nuove versioni Technical Preview, dato che questo strumento viene rilasciato nell'ambito di Current Branch o di un rilascio fuori programma pronto per la produzione.

### <a name="requirements"></a>Requisiti  
- È possibile eseguire lo strumento direttamente nel computer che ospita il punto di distribuzione oppure in remoto da un altro server. Lo strumento può essere eseguito solo per un unico punto di distribuzione alla volta.
- Per la gerarchia di Configuration Manager l'account utente che esegue lo strumento deve disporre direttamente di autorizzazioni di amministrazione basate sui ruoli equivalenti a quelle di un amministratore completo.  Lo strumento non funziona se all'account utente sono state concesse autorizzazioni in quanto membro di un gruppo di sicurezza di Windows con autorizzazioni di amministratore completo.

### <a name="modes-of-operation"></a>Modalità di funzionamento
Lo strumento può essere eseguito in due modalità:
1. **Modalità di simulazione**:   
   Se non si specifica l'opzione **/delete**, lo strumento viene eseguito in modalità di simulazione e identifica il contenuto da eliminare dal punto di distribuzione, senza però eliminare effettivamente i dati.

   - Se si esegue lo strumento in questa modalità, le informazioni sul contenuto da eliminare vengono scritte automaticamente nel file di log dello strumento. All'utente non viene richiesto di confermare ogni eliminazione potenziale.
   - Per impostazione predefinita, il file di log viene scritto nella cartella Temp dell'utente nel computer in cui si esegue lo strumento. È tuttavia possibile usare l'opzione /log per reindirizzare il file di log in un'altra posizione.  
   </br>

   È consigliabile eseguire lo strumento in questa modalità e di esaminare il file di log prima di eseguire lo strumento con l'opzione /delete.  

2. **Modalità di eliminazione**: Se si attiva l'opzione **/delete**, lo strumento viene eseguito in modalità di eliminazione.

   - Se si esegue lo strumento in questa modalità, il contenuto orfano rilevato nel punto di distribuzione interessato può essere eliminato dalla raccolta contenuto del punto di distribuzione stesso.
   -  Prima di eliminare ogni file, all'utente viene richiesto di confermare l'eliminazione.  È possibile selezionare **S** per Sì, **N** per No o **Sì a tutti** per ignorare le altre richieste di conferma ed eliminare tutto il contenuto orfano.  
   </br>

   È consigliabile eseguire lo strumento in modalità di simulazione e di esaminare il file di log prima di eseguire lo strumento con l'opzione /delete.  

Quando si esegue lo strumento di pulizia della raccolta contenuto, indipendentemente dalla modalità, viene creato automaticamente un log il cui nome è composto dalla modalità in cui viene eseguito lo strumento, dal nome del punto di distribuzione, dalla data e dall'ora dell'operazione. Il file di log si apre automaticamente al termine dell'esecuzione dello strumento. Per impostazione predefinita, il log viene scritto nella cartella **Temp** dell'utente nel computer in cui si esegue lo strumento. È tuttavia possibile usare un'opzione della riga di comando per reindirizzare il file di log in un'altra posizione, compresa una condivisione di rete.   


### <a name="run-the-tool"></a>Eseguire lo strumento
Per eseguire lo strumento:
1. Aprire un prompt dei comandi amministrativo in una cartella contenente **ContentLibraryCleanup.exe**.  
2. Immettere quindi una riga di comando che includa le opzioni della riga di comando obbligatorie e le opzioni facoltative che si vogliono usare.

**Problema noto** Quando si esegue lo strumento, se un pacchetto o una distribuzione ha esito negativo o è in corso, è possibile che venga restituito un errore simile al seguente:
-  *System.InvalidOperationException: non è possibile eseguire la pulizia della raccolta contenuto perché il pacchetto \<packageID> non è installato completamente.*

**Soluzione alternativa:** Nessuna. Lo strumento non è in grado di identificare in modo affidabile i file orfani quando il contenuto è in corso o la sua distribuzione ha avuto esito negativo. Di conseguenza, lo strumento non consente di eseguire la pulizia del contenuto fino a quando il problema non viene risolto.



### <a name="command-line-switches"></a>Opzioni della riga di comando  
È possibile usare le opzioni della riga di comando seguenti in qualsiasi ordine.   

|Opzione|Dettagli|
|---------|-------|
|**/delete**  |**Facoltativo** </br> Usare questa opzione se si desidera eliminare contenuto dal punto di distribuzione. Prima dell'eliminazione viene richiesta la conferma. </br></br> Se questa opzione non viene utilizzata, lo strumento registra i risultati relativi al contenuto da eliminare, ma non elimina alcun contenuto dal punto di distribuzione. </br></br> Esempio: ***ContentLibraryCleanup.exe /dp server1.contoso.com /delete*** |
| **/q**       |**Facoltativa** </br> Eseguire lo strumento in modalità non interattiva. Tutte le richieste di conferma (ad esempio in caso di eliminazione di contenuto) vengono soppresse e il file di log non viene aperto automaticamente. </br></br> Esempio: ***ContentLibraryCleanup.exe /q /dp server1.contoso.com*** |
| **/dp &lt;FQDN punto di distribuzione>**  | **Richiesto** </br> Specificare il nome di dominio completo (FQDN) del punto di distribuzione che si desidera pulire. </br></br> Esempio:  ***ContentLibraryCleanup.exe /dp server1.contoso.com***|
| **/ps &lt;FQDN sito primario>**       | **Facoltativa** per la pulizia del contenuto di un punto di distribuzione in un sito primario.</br>**Obbligatoria** per la pulizia del contenuto di un punto di distribuzione in un sito secondario. </br></br> Specificare il nome FQDN del sito primario a cui appartiene il punto di distribuzione o del padre primario se il punto di distribuzione si trova in un sito secondario. </br></br> Esempio: ***ContentLibraryCleanup.exe /dp server1.contoso.com /ps siteserver1.contoso.com*** |
| **/sc &lt;codice del sito primario>**  | **Facoltativa** per la pulizia del contenuto di un punto di distribuzione in un sito primario.</br>**Obbligatoria** per la pulizia del contenuto di un punto di distribuzione in un sito secondario. </br></br> Specificare il codice del sito primario a cui appartiene il punto di distribuzione o del sito primario padre se il punto di distribuzione si trova in un sito secondario.</br></br> Esempio: ***ContentLibraryCleanup.exe /dp server1.contoso.com /sc ABC*** |
| **/log\<directory file di log>**       |**Facoltativo** </br> Specificare la directory in cui salvare i file di log. Può essere un'unità locale o una condivisione di rete.</br></br> Se questa opzione non viene usata, i file di log vengono salvati automaticamente nella cartella Temp dell'utente.</br></br> Esempio di unità locale: ***ContentLibraryCleanup.exe /dp server1.contoso.com /log C:\Users\Administrator\Desktop*** </br></br>Esempio di condivisione di rete: ***ContentLibraryCleanup.exe /dp server1.contoso.com /log \\&lt;condivisione>\&lt;cartella>***|


## <a name="improvements-for-in-console-search"></a>Miglioramenti per la ricerca nella console
In base ai commenti e ai suggerimenti di UserVoice, alla ricerca nella console sono stati apportati i miglioramenti seguenti:
- **Percorso oggetto:**  
  Molti oggetti ora supportano una nuova colonna denominata **Percorso oggetto**.  Se si include questa colonna nella visualizzazione dei risultati, è possibile vedere il percorso di ogni oggetto. Se ad esempio si esegue la ricerca delle app nel nodo Applicazioni e la ricerca viene eseguita anche nei sottonodi, la colonna *Percorso oggetto* nel riquadro dei risultati visualizzerà il percorso di ogni oggetto restituito.   

- **Conservazione del testo della ricerca:**  
  Quando si immette testo nella casella di testo di ricerca e quindi si passa dalla ricerca in un sottonodo alla ricerca nel nodo corrente e viceversa, il testo digitato diventa permanente e rimane disponibile per una nuova ricerca senza doverlo digitare di nuovo.

- **Mantenimento della decisione relativa alla ricerca nei sottonodi:**  
  L'opzione selezionata per l'esecuzione della ricerca nel *nodo corrente* o in *tutti i sottonodi* ora viene mantenuta quando si modifica il nodo usato.   Con il nuovo comportamento non è necessario reimpostare costantemente la decisione ogni volta che ci si sposta all'interno della console.  Per impostazione predefinita, quando si apre la console è impostata la ricerca solo nel nodo corrente.

## <a name="prevent-installation-of-an-application-if-a-specified-program-is-running"></a>Evitare l'installazione di un'applicazione se è in esecuzione un programma specifico.
È ora possibile configurare un elenco di file eseguibili (con estensione exe) nelle proprietà del tipo di distribuzione, in modo da bloccare l'installazione di un'applicazione se uno dei file eseguibili è in esecuzione. Dopo il tentativo di installazione viene visualizzata una finestra di dialogo con la richiesta di chiudere i processi che bloccano l'installazione.

### <a name="try-it-out"></a>Procedura
Per configurare un elenco di file eseguibili
1. Nella pagina delle proprietà di un qualsiasi tipo di distribuzione scegliere la scheda **Installer Handling** (Gestione programma di installazione).
2. Fare clic su **Aggiungi** per aggiungere uno o più file eseguibili all'elenco (ad esempio **Edge.exe**)
3. Fare clic su **OK** per chiudere la finestra di dialogo delle proprietà del tipo di distribuzione.

D'ora in avanti se si distribuisce questa applicazione a un utente o a un dispositivo e uno dei file eseguibili aggiunti viene eseguito, per l'utente finale viene visualizzata una finestra di dialogo di Software Center che informa dell'esito negativo dell'installazione a causa dell'esecuzione di un'applicazione.

## <a name="new-windows-hello-for-business-notification-for-end-users"></a>Nuova notifica di Windows Hello for Business per gli utenti finali

Una nuova notifica di Windows 10 informa gli utenti che sono necessarie azioni aggiuntive per completare l'installazione di Windows Hello for Business, ad esempio l'impostazione di un PIN.

## <a name="windows-store-for-business-support-in-configuration-manager"></a>Supporto di Windows Store for Business in Configuration Manager

È ora possibile distribuire app con licenza online con scopo della distribuzione **Disponibile** da Windows Store per le aziende a PC che eseguono il client di Configuration Manager.
Per altri dettagli, vedere [Gestire le app da Windows Store per le aziende con Configuration Manager](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).

Il supporto per questa funzionalità è attualmente disponibile solo per i PC che eseguono la versione di anteprima di Windows 10 RS2.

## <a name="return-to-previous-page-when-a-task-sequence-fails"></a>Tornare alla pagina precedente quando si verifica un errore di una sequenza di attività
È ora possibile tornare alla pagina precedente quando si esegue una sequenza di attività e si verifica un errore. Prima di questa versione, se si verificava un errore era necessario riavviare la sequenza di attività. È ad esempio possibile usare il pulsante **Precedente** negli scenari seguenti:

- Quando un computer viene avviato in Windows PE, potrebbe essere visualizzata la finestra di dialogo di avvio della sequenza di attività prima che la sequenza stessa sia disponibile. Se in questo scenario si fa clic su Avanti, viene visualizzata la pagina finale della sequenza di attività che informa l'utente che non sono disponibili sequenze di attività. È ora possibile fare clic su **Precedente** per ripetere la ricerca di sequenze di attività. È possibile ripetere questo processo finché la sequenza di attività non è disponibile.
- Quando si esegue una sequenza di attività ma i pacchetti di contenuto dipendenti non sono ancora disponibili nei punti di distribuzione, la sequenza di attività ha esito negativo. È ora possibile distribuire il contenuto mancante, se non è stato ancora distribuito, o attendere che il contenuto sia disponibile nei punti di distribuzione e quindi fare clic su **Precedente** per ripetere la ricerca di contenuto con la sequenza di attività.

## <a name="express-installation-files-support-for-windows-10-updates"></a>Supporto per i file di installazione rapida per gli aggiornamenti di Windows 10
In Configuration Manager è stato aggiunto il supporto dei file di installazione rapida per gli aggiornamenti di Windows 10. Se si usa una versione supportata di Windows 10, è ora possibile usare le impostazioni di Configuration Manager per scaricare solo le differenze tra l'aggiornamento cumulativo di Windows 10 del mese corrente e l'aggiornamento cumulativo del mese precedente. Attualmente in Current Branch di Configuration Manager l'aggiornamento cumulativo completo di Windows 10, inclusi tutti gli aggiornamenti dei mesi precedenti, vengono scaricati ogni mese. Grazie ai file di installazione rapida sono possibili download più brevi e tempi di installazione più rapidi per i client.

> [!IMPORTANT]
> Le impostazioni per il supporto dei file di installazione rapida sono disponibili in Configuration Manager. Questa funzionalità tuttavia è supportata solo da Windows 10 versione 1607 con l'aggiornamento dell'agente di Windows Update incluso negli aggiornamenti rilasciati il 10 gennaio 2017 (Patch Tuesday). Per altre informazioni su questi aggiornamenti, vedere [la pagina del supporto tecnico 10 gennaio 2017 - KB3213986](https://support.microsoft.com/help/4009938/january-10-2017-kb3213986-os-build-14393-693). Sarà possibile avvalersi dei file di installazione rapida dopo il rilascio del prossimo insieme di aggiornamenti, il 14 febbraio 2017. Windows 10 versione 1607 senza l'aggiornamento e le versioni precedenti di Windows non supportano i file di installazione rapida.


### <a name="to-enable-the-download-of-express-installation-files-for-windows-10-updates-on-the-server"></a>Per abilitare il download dei file di installazione rapida per gli aggiornamenti di Windows 10 nel server
Per avviare la sincronizzazione dei metadati per i file di installazione rapida di Windows 10 è necessario abilitarla nelle proprietà del punto di aggiornamento software.
1. Nella console di Configuration Manager passare a **Amministrazione** > **Configurazione del sito** > **Siti**.
2. Selezionare il sito di amministrazione centrale o il sito primario autonomo.
3. Nel gruppo **Impostazioni** della scheda **Home** fare clic su **Configura componenti sito**, quindi fare clic su **Punto di aggiornamento software**. Nella scheda **File di aggiornamento** selezionare **Download full files for all approved updates and express installation files for Windows 10** (Download di file completi per tutti gli aggiornamenti approvati e i file di installazione rapida per Windows 10).

### <a name="to-enable-support-for-clients-to-download-and-install-express-installation-files"></a>Per abilitare il supporto del download e dell'installazione di file di installazione rapida per i client
Per abilitare il supporto dei file di installazione rapida per i client, è necessario abilitare i file di installazione rapida nei client nella sezione Aggiornamenti rapidi delle impostazioni del client. Questa operazione crea un nuovo listener HTTP che attende le richieste di download dei file di installazione rapida sulla porta specificata. Dopo aver distribuito le impostazioni client per abilitare questa funzionalità nel client, la funzionalità tenterà di scaricare le differenze tra l'aggiornamento cumulativo di Windows 10 del mese corrente e l'aggiornamento cumulativo del mese precedente. Nei client deve essere in esecuzione una versione di Windows 10 che supporti i file di installazione rapida.
1. Abilitare il supporto per i file di installazione rapida nelle proprietà del componente del punto di aggiornamento software (procedura precedente).
2. Nella console di Configuration Manager passare ad **Amministrazione** > **Impostazioni client**.
3. Selezionare le impostazioni client appropriate e quindi nella scheda **Home** fare clic su **Proprietà**.
4. Selezionare la pagina **Aggiornamenti software** , selezionare **Sì** nell'impostazione **Abilita l'installazione di aggiornamenti rapidi nei client** e configurare la porta usata dal listener HTTP nel client per l'impostazione **Porta usata per scaricare contenuto per gli aggiornamenti rapidi**.


## <a name="odata-endpoint-data-access"></a>Accesso ai dati di endpoint OData

 Configuration Manager offre ora un endpoint RESTful OData per l'accesso ai dati di Configuration Manager. L'endpoint è compatibile con OData versione 4, che consente a strumenti come Excel e Power BI di accedere facilmente ai dati di Configuration Manager tramite un singolo endpoint. La versione Technical Preview 1612 di Configuration Manager supporta solo l'accesso agli oggetti in lettura.  

I dati attualmente disponibili nel [provider WMI di Configuration Manager](../../develop/reference/configuration-manager-reference.md) sono ora accessibili anche con il nuovo endpoint OData RESTful. I set di entità esposti dall'endpoint OData consentono di enumerare gli stessi dati su cui è possibile eseguire query con il provider WMI.

### <a name="try-it-out"></a>Procedura

Prima di usare l'endpoint OData, è necessario abilitarlo per il sito.

1.  Passare ad **Amministrazione** > **Configurazione del sito** > **Siti**.
2.  Selezionare il sito primario e fare clic su **Proprietà**.
3.  Nella scheda Generale del foglio delle proprietà del sito primario fare clic su **Enable REST endpoint for all providers on this site** (Abilita endpoint REST per tutti i provider nel sito) e quindi fare clic su **OK**.

Nel visualizzatore di query OData preferito provare a eseguire query simili agli esempi seguenti per restituire oggetti diversi in Configuration Manager:

| Scopo | Query OData |
|---|---|
| Recuperare tutte le raccolte | `http://localhost/CMRestProvider/Collection` |
| Recuperare una raccolta | `http://localhost/CMRestProvider/Collection('SMS00001')`
| Recuperare i primi 100 dispositivi nella raccolta | `http://localhost/CMRestProvider/Collection('SMS00001')/Device?$top=100` |
| Recuperare un dispositivo nella raccolta con l'ID risorsa specificato | `http://localhost/CMRestProvider/Collection('SMS00001')/Device(16777573)` |
| Recuperare il sistema operativo del dispositivo nella raccolta | `http://localhost/CMRestProvider/Collection('SMS00001')/Device(16777573)/OPERATING_SYSTEM` |
| Recuperare gli utenti nella raccolta | `http://localhost/CMRestProvider/Collection('SMS00001')/User` |

> [!NOTE]
> Le query di esempio illustrate nella tabella, che usano *localhost* come nome host nell'URL, possono essere usate nei computer che eseguono il provider SMS. Se le query vengono eseguite da un computer diverso, sostituire localhost con il nome FQDN del server in cui è installato il provider SMS.

## <a name="azure-active-directory-onboarding"></a>Onboarding di Azure Active Directory

L'onboarding di Azure Active Directory crea una connessione tra Configuration Manager e Azure Active Directory che può essere usata da altri servizi cloud. Questa funzionalità può attualmente essere usata per creare la connessione necessaria per il gateway di gestione cloud.

Eseguire questa attività con un amministratore di Azure, poiché saranno necessarie le credenziali di amministrazione di Azure.

#### <a name="to-create-the-connection"></a>Per creare la connessione:

2. Nell'area di lavoro **Amministrazione** scegliere **Servizi cloud** > **Azure Active Directory** > **Add Azure Active Directory** (Aggiungi Azure Active Directory).
2. Scegliere **Accedi** per creare la connessione con Azure AD.

#### <a name="configuration-manager-client-requirements"></a>Requisiti client di Configuration Manager

Esistono diversi requisiti per abilitare la creazione di criteri utente nel gateway di gestione cloud.

- Il processo di onboarding di Azure AD deve essere completato e il client deve essere inizialmente connesso alla rete aziendale per ottenere le informazioni di connessione.
- I client devono appartenere a un dominio (registrato in Active Directory) e a un dominio appartenente al cloud (registrato in Azure AD).
- È necessario eseguire l'[individuazione utente Active Directory](../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser).
- È necessario modificare il client di Configuration Manager per consentire le richieste di criteri utente via Internet e distribuire la modifica al client. Poiché questa modifica al client avviene *nel dispositivo client*, può essere distribuita tramite il gateway di gestione cloud anche se non sono state ancora completate le modifiche di configurazione necessarie per i criteri utente.
- Per proteggere il token nella rete, il punto di gestione deve essere configurato per l'uso del protocollo HTTPS. Nel punto di gestione deve anche essere installato .Net 4.5.

Dopo aver apportato queste modifiche alla configurazione, è possibile creare criteri utente e spostare i client in Internet per testare i criteri. Le richieste di criteri utente tramite il gateway di gestione cloud vengono autenticate tramite autenticazione basata su token di Azure AD.

## <a name="change-to-configuring-multi-factor-authentication-for-device-enrollment"></a>Modifica alla configurazione dell'autenticazione a più fattori per la registrazione dei dispositivi

Ora che è possibile configurare l'autenticazione a più fattori (MFA) per la registrazione del dispositivo nel portale di Azure, l'opzione di autenticazione a più fattori è stata rimossa nella console di Configuration Manager. Altre informazioni sull'impostazione dell'MFA per la registrazione sono disponibili [in questo argomento su Microsoft Intune](/mem/intune/enrollment/multi-factor-authentication).
