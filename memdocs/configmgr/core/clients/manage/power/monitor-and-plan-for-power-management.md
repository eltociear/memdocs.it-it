---
title: Monitorare e pianificare il risparmio energia
titleSuffix: Configuration Manager
description: Informazioni su come monitorare e pianificare il risparmio energia in Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 507bf676-2679-4e4d-8831-3ffc9cf8557e
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: a4e5ee9c35dd96f79ea1a88ab09200d4386a7535
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696559"
---
# <a name="how-to-monitor-and-plan-for-power-management-in-configuration-manager"></a>Come monitorare e pianificare il risparmio energia in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Usare le informazioni seguenti per facilitare il monitoraggio e la pianificazione del risparmio energia in Configuration Manager.  

##  <a name="how-to-use-reports-for-power-management"></a><a name="BKMK_How_to_use_reports"></a> Come usare i report per il risparmio energia  
 La funzionalità di risparmio energia in Configuration Manager include diversi report per agevolare l'analisi dei consumi e delle impostazioni di risparmio energia per i computer nell'organizzazione. I report possono anche essere usati per facilitare la risoluzione dei problemi.  

 Prima di poter usare i report di risparmio energia, è necessario configurare i report per la gerarchia. Per altre informazioni sulla creazione di report in Configuration Manager, vedere [Introduzione ai report](../../../servers/manage/introduction-to-reporting.md).  

> [!NOTE]  
>  Le informazioni relative al risparmio energia usate per i report giornalieri vengono conservate nel database del sito di Configuration Manager per 31 giorni.  
>           Le informazioni relative al risparmio energia usate per i report mensili vengono conservate nel database del sito di Configuration Manager per 13 mesi.  
>   
>  Quando si creano report durante le fasi di monitoraggio e pianificazione e di verifica della conformità per il risparmio energia, è necessario salvare o esportare i risultati dei report di cui si vuole conservare i dati per confronti successivi, nel caso vengano in seguito rimossi da Configuration Manager.  

## <a name="list-of-power-management-reports"></a>Elenco dei report di risparmio energia  
 L'elenco seguente include informazioni dettagliate sui report di risparmio energia disponibili in Configuration Manager.  

> [!NOTE]  
>  I report di risparmio energia visualizzano il numero di computer fisici e il numero di computer virtuali in una raccolta selezionata. Tuttavia, nei report di risparmio energia vengono visualizzate informazioni sul risparmio energia solo dai computer fisici.  

###  <a name="computer-activity-report"></a><a name="BKMK_Activity"></a> Report Attività computer  
 Il report **Attività computer** visualizza un grafico che mostra l'attività seguente per una raccolta specificata in un periodo di tempo specificato:  

- **Computer acceso** - Il computer è stato acceso.  

- **Monitor acceso** - Il monitor è stato acceso.  

- **Utente attivo** - È stata rilevata attività dal mouse del computer, dalla tastiera del computer o da una connessione Desktop remoto al computer  

  Questo report viene usato durante le fasi di monitoraggio, pianificazione e applicazione per analizzare l'andamento delle attività dei computer, dei monitor e degli utenti in un periodo di 24 ore. Se si esegue il report per alcuni giorni, i dati vengono aggregati per il periodo. Questo report può essere utile per determinare gli orari lavorativi (di punta) e non lavorativi (non di punta) tipici per una raccolta selezionata, in modo da poter decidere più facilmente quando applicare i piani di risparmio energia configurati.  

  Il grafico mostra i periodi di tempo durante i quali un computer potrebbe essere acceso, ma non è presente attività utente. Prendere in considerazione la possibilità di applicare impostazioni di risparmio energia più restrittive durante tali periodi per ridurre i costi energetici per i computer accesi, ma non usati. Un computer viene conteggiato come attivo in presenza di attività del computer, dell'utente o del monitor per più di un minuto per un'ora visualizzata nel grafico. Se un computer non restituisce dati relativi al risparmio energia, non verrà incluso nel report **Attività computer** .  

  Usare i parametri seguenti per configurare questo report.  

#### <a name="required-report-parameters"></a>Parametri obbligatori del report  
 I parametri seguenti devono essere specificati per eseguire il report.  

|Nome parametro|Descrizione|  
|--------------------|-----------------|  
|**Data inizio**|Nell'elenco a discesa selezionare la data di inizio per il report.|  
|**Data di fine (facoltativo)**|Nell'elenco a discesa selezionare una data di fine facoltativa per il report.|  
|**Nome raccolta**|Nell'elenco a discesa selezionare una raccolta da usare per il report.|  
|**Tipo di dispositivo**|Dall'elenco a discesa, selezionare il tipo di computer per cui si desidera un report. I valori validi sono **Tutti** (computer desktop e portatili), **Desktop** (solo computer desktop) e **Portatile** (solo computer portatili).|  

#### <a name="hidden-report-parameters"></a>Parametri nascosti del report  
 Per questo report non sono disponibili parametri nascosti che è possibile impostare.  

#### <a name="report-links"></a>Collegamenti per il report  
 Se non si specifica un valore per **Data di fine (facoltativo)** , questo report contiene un collegamento al report seguente che offre ulteriori informazioni.  

|Nome report|Dettagli|  
|-----------------|-------------|  
|**Dettagli attività computer**|Fare clic sul collegamento **Fare clic per ulteriori informazioni** per visualizzare un elenco di computer attivi, inattivi e che non inviano informazioni per il report per la data specificata.<br /><br /> Per altre informazioni, vedere la sezione [Computer Activity Details Report](#BKMK_Activity_Details) in questo argomento.|  

###  <a name="computer-activity-by-computer-report"></a><a name="BKMK_Comp_Activity_by_computer"></a> Report Attività computer per computer  
 Il report **Attività computer per computer** visualizza un grafico che mostra l'attività seguente per un computer specificato in una data specificata:  

- **Computer acceso** - Il computer è stato acceso.  

- **Monitor acceso** - Il monitor è stato acceso.  

- **Utente attivo** - È stata rilevata attività dal mouse del computer, dalla tastiera del computer o da una connessione Desktop remoto al computer.  

  Questo report può essere eseguito in modo indipendente o chiamato dal report **Dettagli attività computer** .  

> [!NOTE]  
>  Le informazioni sull'attività del computer vengono raccolte dai computer client durante l'inventario hardware. A seconda dell'ora in cui viene eseguito l'inventario hardware, potrebbe essere raccolta l'attività mentre è applicata una combinazione per il risparmio di energia in ore di punta o fuori ore di punta.  

 Usare i parametri seguenti per configurare questo report.  

#### <a name="required-report-parameters"></a>Parametri obbligatori del report  
 I parametri seguenti devono essere specificati per eseguire il report.  

|Nome parametro|Descrizione|  
|--------------------|-----------------|  
|**Data report**|Nell'elenco a discesa selezionare una data per il report.|  
|**Nome computer**|Immettere il nome di un computer per cui si vuole ottenere un report.|  

#### <a name="hidden-report-parameters"></a>Parametri nascosti del report  
 Per questo report non sono disponibili parametri nascosti che è possibile impostare.  

#### <a name="report-links"></a>Collegamenti per il report  
 Questo report contiene collegamenti al report seguente che offre ulteriori informazioni sull'elemento selezionato.  

|Nome report|Dettagli|  
|-----------------|-------------|  
|**Dettagli computer**|Fare clic sul collegamento **Fare clic per ulteriori informazioni** per visualizzare informazioni su capacità di risparmio energia, impostazioni di risparmio energia e combinazioni per il risparmio di energia applicate per il computer selezionato.|  

###  <a name="computer-activity-details-report"></a><a name="BKMK_Activity_Details"></a> Computer Activity Details report  
 Il report **Dettagli attività computer** visualizza un elenco dei computer attivi o inattivi con le relative funzionalità di sospensione e riattivazione. Questo report viene chiamato il [Computer Activity Report](#BKMK_Activity) e non è progettato per essere eseguito direttamente dall'amministratore del sito.  

 Usare i parametri seguenti per configurare questo report.  

#### <a name="required-report-parameters"></a>Parametri obbligatori del report  
 I parametri seguenti devono essere specificati per eseguire il report.  

|Nome parametro|Descrizione|  
|--------------------|-----------------|  
|**Nome raccolta**|Nell'elenco a discesa selezionare una raccolta da usare per il report.|  
|**Data report**|Nell'elenco a discesa selezionare una data da usare per il report.|  
|**Ora report**|Nell'elenco a discesa selezionare un'ora nella data specificata per l'esecuzione del report. I valori validi sono compresi tra **00** e **23**.|  
|**Stato computer**|Nell'elenco a discesa selezionare lo stato del computer per cui si desidera eseguire il report. I valori validi sono **Tutti** (computer accesi o spenti), **Attivato** (computer accesi) e **Disattivato** (computer spenti, in sospensione o in ibernazione). Questi valori vengono restituiti solo per il periodo di reporting selezionato.|  
|**Tipo di dispositivo**|Dall'elenco a discesa, selezionare il tipo di computer per cui si desidera un report. I valori validi sono **Tutti** (computer desktop e portatili), **Desktop** (solo computer desktop) e **Portatile** (solo computer portatili). Questi valori vengono restituiti solo per il periodo di reporting selezionato.|  
|**Idoneo per essere sospeso**|Dall'elenco a discesa, selezionare se si desidera visualizzare i computer in grado di sospensione nel report. I valori validi sono **Tutti** (computer idonei e non idonei alla sospensione), **No** (computer non idonei alla sospensione) e **Sì** (computer idonei alla sospensione).|  
|**Idoneo per la riattivazione da sospensione**|Dall'elenco a discesa, selezionare se si desidera visualizzare i computer in grado di riattivazione dalla modalità di sospensione nel report. I valori validi sono **Tutti** (computer idonei e non idonei alla riattivazione da sospensione), **No** (computer non idonei alla riattivazione da sospensione) e **Sì** (computer idonei alla riattivazione da sospensione).|  
|**Combinazione per il risparmio di energia**|Dall'elenco a discesa, selezionare i tipi di piano di risparmio energia che si desidera visualizzare nel report. I valori validi sono **Tutti** (computer senza alcuna combinazione di risparmio energia applicata; computer con una combinazione di risparmio energia applicata; computer esclusi dal risparmio energia), **Non specificato** (computer senza alcuna combinazione di risparmio energia applicata), **Definito** (computer con una combinazione di risparmio energia applicata) ed **Escluso** (computer esclusi dal risparmio energia).|  
|**Sistema operativo**|Nell'elenco a discesa selezionare i sistemi operativi dei computer da visualizzare nel report oppure selezionare **Tutto** per visualizzare tutti i sistemi operativi.|  

#### <a name="hidden-report-parameters"></a>Parametri nascosti del report  
 Per questo report non sono disponibili parametri nascosti che è possibile impostare.  

#### <a name="report-links"></a>Collegamenti per il report  
 Questo report contiene collegamenti al report seguente che offre ulteriori informazioni sull'elemento selezionato.  

|Nome report|Dettagli|  
|-----------------|-------------|  
|**Attività computer per computer**|Fare clic su un nome di computer per visualizzare un'attività specifica del computer in un periodo di reporting selezionato. Le attività includono **Computer acceso** (il computer è stato acceso?), **Monitor acceso** (il monitor è stato acceso?) e **Attività utente** (è stata rilevata un'attività del mouse o della tastiera del computer o una connessione desktop remoto).<br /><br /> Per altre informazioni, vedere la sezione [Computer Activity by Computer Report](#BKMK_Comp_Activity_by_computer) in questo argomento.|  

###  <a name="computer-details-report"></a><a name="BKMK_Computer_Details"></a> Report Dettagli computer  
 Il report **Dettagli computer** visualizza informazioni dettagliate su capacità di risparmio energia, impostazioni del risparmio energia e combinazioni per il risparmio di energia applicate a un computer specificato. Questo report viene chiamato dai report **Attività computer per computer** , **Computer con più combinazioni per il risparmio di energia** , **Funzionalità alimentazione** e **Dettagli impostazioni risparmio energia** . Non è progettato per essere eseguito direttamente dall'amministratore del sito.  

#### <a name="required-report-parameters"></a>Parametri obbligatori del report  
 I parametri seguenti devono essere specificati per eseguire il report.  

|Nome parametro|Descrizione|  
|--------------------|-----------------|  
|**Nome computer**|Immettere il nome di un computer per cui si vuole ottenere un report.|  
|**Modalità risparmio di energia**|Nell'elenco a discesa selezionare il tipo di impostazioni di risparmio energia da visualizzare nei risultati del report. Selezionare **Alimentazione da rete elettrica** per visualizzare le impostazioni di risparmio energia configurate per quando il computer è collegato alla rete elettrica e **A batteria** per visualizzare le impostazioni di risparmio energia configurate per quando il computer è alimentato a batteria.|  

#### <a name="hidden-report-parameters"></a>Parametri nascosti del report  
 Per questo report non sono disponibili parametri nascosti che è possibile impostare.  

#### <a name="report-links"></a>Collegamenti per il report  
 Questo report non è collegato ad altri report relativi al risparmio energia.  

###  <a name="computer-not-reporting-details-report"></a><a name="BKMK_Not_Reporting"></a> Report Computer che non segnalano dettagli  
 Il report **Computer che non segnalano dettagli** visualizza un elenco di computer in una raccolta specificata che non hanno segnalato attività per il risparmio energia per una data e un'ora specificate. Questo report viene chiamato dal **Computer Activity Report** e non è progettato per essere eseguito direttamente dall'amministratore del sito.  

> [!NOTE]  
>  I computer restituiscono informazioni sul risparmio energia nell'ambito della pianificazione per l'inventario hardware. Prima di stabilire che un computer non sta inviando informazioni, assicurarsi che abbia segnalato l'inventario hardware.  

 Usare i parametri seguenti per configurare questo report.  

#### <a name="required-report-parameters"></a>Parametri obbligatori del report  
 I parametri seguenti devono essere specificati per eseguire il report.  

|Nome parametro|Descrizione|  
|--------------------|-----------------|  
|**Nome raccolta**|Nell'elenco a discesa selezionare una raccolta da usare per il report.|  
|**Data report**|Nell'elenco a discesa selezionare una data per il report.|  
|**Ora report**|Nell'elenco a discesa selezionare un'ora nella data specificata per l'esecuzione del report. I valori validi sono compresi tra **00** e **23**.|  
|**Tipo di dispositivo**|Dall'elenco a discesa, selezionare il tipo di computer per cui si desidera un report. I valori validi sono **Tutti** (computer desktop e portatili), **Desktop** (solo computer desktop) e **Portatile** (solo computer portatili). Questi valori vengono restituiti solo per il periodo di reporting selezionato.|  

#### <a name="hidden-report-parameters"></a>Parametri nascosti del report  
 Per questo report non sono disponibili parametri nascosti che è possibile impostare.  

#### <a name="report-links"></a>Collegamenti per il report  
 Questo report non è collegato ad altri report relativi al risparmio energia.  

###  <a name="computers-excluded"></a><a name="BKMK_Excluded"></a> Computer esclusi  
 Il report **Computer esclusi** visualizza un elenco di computer in una raccolta specificata che sono stati esclusi dal risparmio energia di Configuration Manager.  

 Usare i parametri seguenti per configurare questo report.  

#### <a name="required-report-parameters"></a>Parametri obbligatori del report  
 I parametri seguenti devono essere specificati per eseguire il report.  

|Nome parametro|Descrizione|  
|--------------------|-----------------|  
|**Raccolta**|Dall'elenco a discesa, selezionare una raccolta per il report.|  
|**Motivo**|Nell'elenco a discesa selezionare il motivo per cui i computer sono stati esclusi dal risparmio energia. È possibile visualizzare tutti i computer esclusi (**Tutti**), i computer esclusi da un utente amministratore (**Escluso dall'amministratore**) e i computer esclusi da un utente di Software Center (**Escluso dall'utente**).|  

#### <a name="hidden-report-parameters"></a>Parametri nascosti del report  
 Per questo report non sono disponibili parametri nascosti che è possibile impostare.  

#### <a name="report-links"></a>Collegamenti per il report  
 Questo report contiene collegamenti al report seguente che offre ulteriori informazioni sull'elemento selezionato.  

|Nome report|Dettagli|  
|-----------------|-------------|  
|**Dettagli computer**|Fare clic sul nome di un computer per visualizzare informazioni su capacità di risparmio energia, impostazioni di risparmio energia e combinazioni per il risparmio di energia applicate per il computer selezionato.<br /><br /> Per altre informazioni, vedere la sezione [Computer Details Report](#BKMK_Computer_Details) in questo argomento.|  

###  <a name="computers-with-multiple-power-plans"></a><a name="BKMK_Multiple"></a> Computer con più combinazioni per il risparmio di energia  
 Il report **Computer con più combinazioni per il risparmio di energia** visualizza un elenco di computer membri di più raccolte, ognuna delle quali applica combinazioni per il risparmio di energia diverse. Per ogni computer con impostazioni di risparmio energia potenzialmente in conflitto, il report visualizza il nome del computer e le combinazioni per il risparmio di energia applicate per ogni raccolta di cui è membro il computer.  

> [!IMPORTANT]  
>  Se un computer è membro di più raccolte e ogni raccolta include diverse combinazioni per il risparmio energia, verrà applicata la combinazione meno restrittiva.  
>   
>  Se un computer è membro di più raccolte e ogni raccolta include diverse ore di riattivazione, verrà applicata l'ora più prossima alla mezzanotte.  

 Usare i parametri seguenti per configurare questo report.  

#### <a name="required-report-parameters"></a>Parametri obbligatori del report  
 I parametri seguenti devono essere specificati per eseguire il report.  

|Nome parametro|Descrizione|  
|--------------------|-----------------|  
|**Nome raccolta**|Dall'elenco a discesa, selezionare una raccolta per il report.|  

#### <a name="hidden-report-parameters"></a>Parametri nascosti del report  
 Per questo report non sono disponibili parametri nascosti che è possibile impostare.  

#### <a name="report-links"></a>Collegamenti per il report  
 Questo report contiene collegamenti al report seguente che offre ulteriori informazioni sull'elemento selezionato.  

|Nome report|Dettagli|  
|-----------------|-------------|  
|**Dettagli computer**|Fare clic sul nome di un computer per visualizzare informazioni su capacità di risparmio energia, impostazioni di risparmio energia e combinazioni per il risparmio di energia applicate per il computer selezionato.<br /><br /> Per altre informazioni, vedere la sezione [Computer Details Report](#BKMK_Computer_Details) in questo argomento.|  

###  <a name="energy-consumption-report"></a><a name="BKMK_Consumption"></a> Report Consumo energia  
 Il report **Consumo energia** visualizza le informazioni seguenti:  

- Un grafico che mostra il consumo di energia mensile totale dei computer in kiloWatt per ora (kWh) nella raccolta specificata per il periodo di tempo specificato.  

- Un grafico che mostra il consumo di energia medio in kiloWatt per ora (kWh) di ogni computer nella raccolta specificata per il periodo di tempo specificato.  

- Una tabella che mostra il consumo di energia mensile totale in kiloWatt per ora (kWh) e il consumo di energia medio dei computer nella raccolta specificata per il periodo di tempo specificato.  

  Queste informazioni possono essere utili per individuare le tendenze di consumo di energia nell'ambiente in oggetto. Dopo aver applicato una combinazione per il risparmio di energia ai computer nella raccolta selezionata, il consumo di energia dei computer dovrebbe ridursi.  

> [!NOTE]  
>  L'aggiunta o la rimozione di membri nella raccolta dopo aver applicato una combinazione per il risparmio di energia influirà sui risultati visualizzati dal report **Consumo di energia** e potrebbe risultare più difficile confrontare i risultati della fase di monitoraggio e pianificazione con quelli della fase di imposizione.  

 Usare i parametri seguenti per configurare questo report.  

#### <a name="required-report-parameters"></a>Parametri obbligatori del report  
 I parametri seguenti devono essere specificati per eseguire il report.  

|Nome parametro|Descrizione|  
|--------------------|-----------------|  
|**Data inizio**|Nell'elenco a discesa selezionare una data di inizio per il report.|  
|**Data fine**|Nell'elenco a discesa selezionare una data di fine per il report.|  
|**Nome raccolta**|Dall'elenco a discesa, selezionare una raccolta per il report.|  
|**Tipo di dispositivo**|Dall'elenco a discesa, selezionare il tipo di computer per cui si desidera un report. I valori validi sono **Tutti** (computer desktop e portatili), **Desktop** (solo computer desktop) e **Portatile** (solo computer portatili). Questi valori vengono restituiti solo per il periodo di reporting selezionato.|  

#### <a name="hidden-report-parameters"></a>Parametri nascosti del report  
 I parametri nascosti seguenti possono essere specificati facoltativamente per modificare il comportamento di questo report.  

|Nome parametro|Descrizione|  
|--------------------|-----------------|  
|**Computer desktop acceso**|Specificare il consumo di energia di un computer desktop quando è acceso. Il valore predefinito è **0,07** kW all'ora.|  
|**Computer portatile acceso**|Specificare il consumo di energia di un computer portatile quando è acceso. Il valore predefinito è **0,02** kW all'ora.|  
|**Computer desktop sospeso**|Specificare il consumo di energia di un computer desktop entrato in sospensione. Il valore predefinito è **0,003** kW all'ora.|  
|**Computer portatile sospeso**|Specificare il consumo di energia di un computer portatile entrato in sospensione. Il valore predefinito è **0,001** kW all'ora.|  
|**Computer desktop spento**|Specificare il consumo di energia di un computer desktop quando è spento. Il valore predefinito è **0** kW all'ora.|  
|**Computer portatile spento**|Specificare il consumo di energia di un computer portatile quando è spento. Il valore predefinito è **0** kW all'ora.|  
|**Monitor desktop acceso**|Specificare il consumo di energia di un monitor di computer desktop quando è acceso. Il valore predefinito è **0,028** kW all'ora.|  
|**Monitor portatile acceso**|Specificare il consumo di energia di un monitor di computer portatile quando è acceso. Il valore predefinito è **0** kW all'ora.|  

#### <a name="report-links"></a>Collegamenti per il report  
 Questo report non è collegato ad altri report relativi al risparmio energia.  

###  <a name="energy-consumption-by-day-report"></a><a name="BKMK_Consumption_by_Day"></a> Report Consumo energia per giorno  
 Il report **Consumo energia per giorno** visualizza le informazioni seguenti:  

- Un grafico che mostra il consumo di energia giornaliero totale dei computer in kiloWatt per ora (kWh) nella raccolta specificata per gli ultimi 31 giorni.  

- Un grafico che mostra il consumo di energia medio giornaliero in kiloWatt per ora (kWh) di ogni computer nella raccolta specificata negli ultimi 31 giorni.  

- Una tabella che mostra il consumo di energia totale giornaliero in kiloWatt per ora (kWh) e il consumo di energia medio giornaliero dei computer nella raccolta specificata negli ultimi 31 giorni.  

  Queste informazioni possono essere utili per individuare le tendenze di consumo di energia nell'ambiente in oggetto. Dopo aver applicato una combinazione per il risparmio di energia ai computer nella raccolta selezionata, il consumo di energia dei computer dovrebbe ridursi.  

> [!NOTE]  
>  L'aggiunta o la rimozione di membri nella raccolta dopo aver applicato una combinazione per il risparmio di energia influirà sui risultati visualizzati dal report **Consumo di energia** e potrebbe risultare più difficile confrontare i risultati della fase di monitoraggio e pianificazione con quelli della fase di imposizione.  

 Usare i parametri seguenti per configurare questo report.  

#### <a name="required-report-parameters"></a>Parametri obbligatori del report  
 I parametri seguenti devono essere specificati per eseguire il report.  

|Nome parametro|Descrizione|  
|--------------------|-----------------|  
|**Raccolta**|Dall'elenco a discesa, selezionare una raccolta per il report.|  
|**Device Type**|Nell'elenco a discesa selezionare il tipo di computer per cui creare un report. I valori validi sono **Tutti** (computer desktop e portatili), **Desktop** (solo computer desktop) e **Portatile** (solo computer portatili). Questi valori vengono restituiti solo per il periodo di reporting selezionato.|  

#### <a name="hidden-report-parameters"></a>Parametri nascosti del report  
 I parametri nascosti seguenti possono essere specificati facoltativamente per modificare il comportamento di questo report.  

|Nome parametro|Descrizione|  
|--------------------|-----------------|  
|**Computer desktop acceso**|Specificare il consumo di energia di un computer desktop quando è acceso. Il valore predefinito è **0,07** kW all'ora.|  
|**Computer portatile acceso**|Specificare il consumo di energia di un computer portatile quando è acceso. Il valore predefinito è **0,02** kW all'ora.|  
|**Computer desktop sospeso**|Specificare il consumo di energia di un computer desktop entrato in sospensione. Il valore predefinito è **0,003** kW all'ora.|  
|**Computer portatile sospeso**|Specificare il consumo di energia di un computer portatile entrato in sospensione. Il valore predefinito è **0,001** kW all'ora.|  
|**Computer desktop spento**|Specificare il consumo di energia di un computer desktop quando è spento. Il valore predefinito è **0** kW all'ora.|  
|**Computer portatile spento**|Specificare il consumo di energia di un computer portatile quando è spento. Il valore predefinito è **0** kW all'ora.|  
|**Monitor desktop acceso**|Specificare il consumo di energia di un monitor di computer desktop quando è acceso. Il valore predefinito è **0,028** kW all'ora.|  
|**Monitor portatile acceso**|Specificare il consumo di energia di un monitor di computer portatile quando è acceso. Il valore predefinito è **0** kW all'ora.|  

#### <a name="report-links"></a>Collegamenti per il report  
 Questo report non è collegato ad altri report relativi al risparmio energia.  

###  <a name="energy-cost-report"></a><a name="BKMK_Cost"></a> Report Costo energia  
 Il report **Costo energia** visualizza le informazioni seguenti:  

- Un grafico che mostra il costo dell'energia totale mensile per i computer nella raccolta specificata per il periodo di tempo specificato.  

- Un grafico che mostra il costo dell'energia medio mensile per ogni computer nella raccolta specificata per il periodo di tempo specificato.  

- Una tabella che mostra il costo dell'energia totale mensile e il costo medio mensile per i computer nella raccolta specificata negli ultimi 31 giorni.  

  Queste informazioni possono essere utili per individuare le tendenze per i costi energetici nell'ambiente in oggetto. Dopo aver applicato una combinazione per il risparmio di energia ai computer nella raccolta selezionata, il costo energetico per i computer dovrebbe ridursi.  

  Usare i parametri seguenti per configurare questo report.  

#### <a name="required-report-parameters"></a>Parametri obbligatori del report  
 I parametri seguenti devono essere specificati per eseguire il report.  

|Nome parametro|Descrizione|  
|--------------------|-----------------|  
|**Data inizio**|Nell'elenco a discesa selezionare una data di inizio per il report.|  
|**Data fine**|Nell'elenco a discesa selezionare una data di fine per il report.|  
|**Costo di KwH**|Specificare il costo dell'elettricità per kWh. Il valore predefinito è **0,09**.<br /><br /> È possibile modificare la valuta usata per il report nella sezione dei parametri nascosti.|  
|**Nome raccolta**|Nell'elenco a discesa selezionare una raccolta da usare per il report.|  
|**Tipo di dispositivo**|Nell'elenco a discesa selezionare il tipo di computer per cui creare un report. I valori validi sono **Tutti** (computer desktop e portatili), **Desktop** (solo computer desktop) e **Portatile** (solo computer portatili). Questi valori vengono restituiti solo per il periodo di reporting selezionato.|  

#### <a name="hidden-report-parameters"></a>Parametri nascosti del report  
 I parametri nascosti seguenti possono essere specificati facoltativamente per modificare il comportamento di questo report.  

|Nome parametro|Descrizione|  
|--------------------|-----------------|  
|**Computer desktop acceso**|Specificare il consumo di energia di un computer desktop quando è acceso. Il valore predefinito è **0,07** kW all'ora.|  
|**Computer portatile acceso**|Specificare il consumo di energia di un computer portatile quando è acceso. Il valore predefinito è **0,02** kW all'ora.|  
|**Computer desktop sospeso**|Specificare il consumo di energia di un computer desktop entrato in sospensione. Il valore predefinito è **0,003** kW all'ora.|  
|**Computer portatile sospeso**|Specificare il consumo di energia di un computer portatile entrato in sospensione. Il valore predefinito è **0,001** kW all'ora.|  
|**Computer desktop spento**|Specificare il consumo di energia di un computer desktop quando è spento. Il valore predefinito è **0** kW all'ora.|  
|**Computer portatile spento**|Specificare il consumo di energia di un computer portatile quando è spento. Il valore predefinito è **0** kW all'ora.|  
|**Monitor desktop acceso**|Specificare il consumo di energia di un monitor di computer desktop quando è acceso. Il valore predefinito è **0,028** kW all'ora.|  
|**Monitor portatile acceso**|Specificare il consumo di energia di un monitor di computer portatile quando è acceso. Il valore predefinito è **0** kW all'ora.|  
|**Valuta**|Specificare l'etichetta di valuta da usare per il report. Il valore predefinito è **USD ($)** .|  

#### <a name="report-links"></a>Collegamenti per il report  
 Questo report non è collegato ad altri report relativi al risparmio energia.  

###  <a name="energy-cost-by-day-report"></a><a name="BKMK_Cost_by_Day"></a> Report Costo energia per giorno  
 Il report **Costo energia per giorno** visualizza le informazioni seguenti:  

- Un grafico che mostra il costo dell'energia totale giornaliero per i computer nella raccolta specificata negli ultimi 31 giorni.  

- Un grafico che mostra il costo dell'energia medio giornaliero per ogni computer nella raccolta specificata negli ultimi 31 giorni.  

- Una tabella che mostra il costo dell'energia totale giornaliero e il costo medio giornaliero per i computer nella raccolta specificata negli ultimi 31 giorni.  

  Queste informazioni possono essere utili per individuare le tendenze per i costi energetici nell'ambiente in oggetto. Dopo aver applicato una combinazione per il risparmio di energia ai computer nella raccolta selezionata, il costo energetico per i computer dovrebbe ridursi.  

  Usare i parametri seguenti per configurare questo report.  

#### <a name="required-report-parameters"></a>Parametri obbligatori del report  
 I parametri seguenti devono essere specificati per eseguire il report.  

|Nome parametro|Descrizione|  
|--------------------|-----------------|  
|**Nome raccolta**|Nell'elenco a discesa selezionare una raccolta da usare per il report.|  
|**Tipo di dispositivo**|Nell'elenco a discesa selezionare il tipo di computer per cui creare un report. I valori validi sono **Tutti** (computer desktop e portatili), **Desktop** (solo computer desktop) e **Portatile** (solo computer portatili). Questi valori vengono restituiti solo per il periodo di reporting selezionato.|  
|**Costo di KwH**|Specificare il costo dell'elettricità per kWh. Il valore predefinito è **0,09**.<br /><br /> È possibile modificare la valuta usata per il report nella sezione dei parametri nascosti.|  

#### <a name="hidden-report-parameters"></a>Parametri nascosti del report  
 I parametri nascosti seguenti possono essere specificati facoltativamente per modificare il comportamento di questo report.  

|Nome parametro|Descrizione|  
|--------------------|-----------------|  
|**Computer desktop acceso**|Specificare il consumo di energia di un computer desktop quando è acceso. Il valore predefinito è **0,07** kW all'ora.|  
|**Computer portatile acceso**|Specificare il consumo di energia di un computer portatile quando è acceso. Il valore predefinito è **0,02** kW all'ora.|  
|**Computer desktop sospeso**|Specificare il consumo di energia di un computer desktop entrato in sospensione. Il valore predefinito è **0,003** kW all'ora.|  
|**Computer portatile sospeso**|Specificare il consumo di energia di un computer portatile entrato in sospensione. Il valore predefinito è **0,001** kW all'ora.|  
|**Computer desktop spento**|Specificare il consumo di energia di un computer desktop quando è spento. Il valore predefinito è **0** kW all'ora.|  
|**Computer portatile spento**|Specificare il consumo di energia di un computer portatile quando è spento. Il valore predefinito è **0** kW all'ora.|  
|**Monitor desktop acceso**|Specificare il consumo di energia di un monitor di computer desktop quando è acceso. Il valore predefinito è **0,028** kW all'ora.|  
|**Monitor portatile acceso**|Specificare il consumo di energia di un monitor di computer portatile quando è acceso. Il valore predefinito è **0** kW all'ora.|  
|**Valuta**|Specificare l'etichetta di valuta da usare per il report. Il valore predefinito è **USD ($)** .|  

#### <a name="report-links"></a>Collegamenti per il report  
 Questo report non è collegato ad altri report relativi al risparmio energia.  

###  <a name="environmental-impact-report"></a><a name="BKMK_Environmental_Impact"></a> Report Impatto ambientale  
 Il report **Impatto ambientale** visualizza le informazioni seguenti:  

- Un grafico che mostra le emissioni di CO2 totali mensili (in tonnellate) per i computer nella raccolta specificata per il periodo di tempo specificato.  

- Un grafico che mostra le emissioni di CO2 medie mensili (in tonnellate) per ogni computer nella raccolta specificata per il periodo di tempo specificato.  

- Una tabella che mostra le emissioni di CO2 totali mensili e le emissioni di CO2 medie mensili generate per i computer nella raccolta specificata per il periodo di tempo specificato.  

  Il report **Impatto ambientale** calcola la quantità di CO2 generata (in tonnellate) in base al tempo di accensione di un computer o un monitor in un periodo di 24 ore.  

  Usare i parametri seguenti per configurare questo report.  

#### <a name="required-report-parameters"></a>Parametri obbligatori del report  
 I parametri seguenti devono essere specificati per eseguire il report.  

|Nome parametro|Descrizione|  
|--------------------|-----------------|  
|**Data di inizio report**|Nell'elenco a discesa selezionare una data di inizio per il report.|  
|**Data di fine report**|Nell'elenco a discesa selezionare una data di fine per il report.|  
|**Nome raccolta**|Dall'elenco a discesa, selezionare una raccolta per il report.|  
|**Tipo di dispositivo**|Dall'elenco a discesa, selezionare il tipo di computer per cui si desidera un report. I valori validi sono **Tutti** (computer desktop e portatili), **Desktop** (solo computer desktop) e **Portatile** (solo computer portatili). Questi valori vengono restituiti solo per il periodo di reporting selezionato.|  

#### <a name="hidden-report-parameters"></a>Parametri nascosti del report  
 I parametri nascosti seguenti possono essere specificati facoltativamente per modificare il comportamento di questo report.  

|Nome parametro|Descrizione|  
|--------------------|-----------------|  
|**Computer desktop acceso**|Specificare il consumo di energia di un computer desktop quando è acceso. Il valore predefinito è **0,07** kW all'ora.|  
|**Computer portatile acceso**|Specificare il consumo di energia di un computer portatile quando è acceso. Il valore predefinito è **0,02** kW all'ora.|  
|**Computer desktop sospeso**|Specificare il consumo di energia di un computer desktop entrato in sospensione. Il valore predefinito è **0,003** kW all'ora.|  
|**Computer portatile sospeso**|Specificare il consumo di energia di un computer portatile entrato in sospensione. Il valore predefinito è **0,001** kW all'ora.|  
|**Computer desktop spento**|Specificare il consumo di energia di un computer desktop quando è spento. Il valore predefinito è **0** kW all'ora.|  
|**Computer portatile spento**|Specificare il consumo di energia di un computer portatile quando è spento. Il valore predefinito è **0** kW all'ora.|  
|**Monitor desktop acceso**|Specificare il consumo di energia di un monitor di computer desktop quando è acceso. Il valore predefinito è **0,028** kW all'ora.|  
|**Monitor portatile acceso**|Specificare il consumo di energia di un monitor di computer portatile quando è acceso. Il valore predefinito è **0** kW all'ora.|  
|**Fattore carbonio (tonnellate/kWh)** (CO2Mix)|Specificare il valore per il fattore di carbonio (in tonnellate/kWh) che è in genere possibile ottenere dalla società fornitrice dell'energia elettrica. Il valore predefinito è **0,0015** tonnellate per kWh.|  

#### <a name="report-links"></a>Collegamenti per il report  
 Questo report non è collegato ad altri report relativi al risparmio energia.  

###  <a name="environmental-impact-by-day-report"></a><a name="BKMK_Environmental_Impact_by_Day"></a> Report Impatto ambientale per giorno  
 Il report **Impatto ambientale per giorno** report visualizza le informazioni seguenti:  

- Un grafico che mostra le emissioni di CO2 totali giornaliere (in tonnellate) per i computer nella raccolta specificata negli ultimi 31 giorni.  

- Un grafico che mostra le emissioni di CO2 medie giornaliere (in tonnellate) per ogni computer nella raccolta specificata negli ultimi 31 giorni.  

- Una tabella che mostra le emissioni di CO2 totali giornaliere e le emissioni di CO2 medie giornaliere generate per i computer nella raccolta specificata negli ultimi 31 giorni.  

  Il report **Impatto ambientale per giorno** calcola la quantità di CO2 generata (in tonnellate) in base al tempo di accensione di un computer o un monitor in un periodo di 24 ore.  

#### <a name="required-report-parameters"></a>Parametri obbligatori del report  
 I parametri seguenti devono essere specificati per eseguire il report.  

|Nome parametro|Descrizione|  
|--------------------|-----------------|  
|**Nome raccolta**|Dall'elenco a discesa, selezionare una raccolta per il report.|  
|**Tipo di dispositivo**|Nell'elenco a discesa selezionare il tipo di computer per cui creare un report. I valori validi sono **Tutti** (computer desktop e portatili), **Desktop** (solo computer desktop) e **Portatile** (solo computer portatili). Questi valori vengono restituiti solo per il periodo di reporting selezionato.|  

#### <a name="hidden-report-parameters"></a>Parametri nascosti del report  
 I parametri nascosti seguenti possono essere specificati facoltativamente per modificare il comportamento di questo report.  

|Nome parametro|Descrizione|  
|--------------------|-----------------|  
|**Computer desktop acceso**|Specificare il consumo di energia di un computer desktop quando è acceso. Il valore predefinito è **0,07** kWh.|  
|**Computer portatile acceso**|Specificare il consumo di energia di un computer portatile quando è acceso. Il valore predefinito è **0,02** kWh.|  
|**Computer desktop spento**|Specificare il consumo di energia di un computer desktop quando è spento. Il valore predefinito è **0** kWh.|  
|**Computer portatile spento**|Specificare il consumo di energia di un computer portatile quando è spento. Il valore predefinito è **0** kWh.|  
|**Computer desktop sospeso**|Specificare il consumo di energia di un computer desktop entrato in sospensione. Il valore predefinito è **0,003** kWh.|  
|**Computer portatile sospeso**|Specificare il consumo di energia di un computer portatile entrato in sospensione. Il valore predefinito è **0,001** kWh.|  
|**Monitor desktop acceso**|Specificare il consumo di energia di un monitor di computer desktop quando è acceso. Il valore predefinito è **0,028** kWh.|  
|**Monitor portatile acceso**|Specificare il consumo di energia di un monitor di computer portatile quando è acceso. Il valore predefinito è **0** kWh.|  
|**Fattore carbonio (tonnellate/kWh)** (CO2Mix)|Specificare un valore per il fattore di carbonio (in tonnellate/kWh) che è in genere possibile ottenere dalla società fornitrice dell'energia elettrica. Il valore predefinito è **0,0015** tonnellate per kWh.|  

#### <a name="report-links"></a>Collegamenti per il report  
 Questo report non è collegato ad altri report relativi al risparmio energia.  

###  <a name="insomnia-computer-details-report"></a><a name="BKMK_Insomnia_Computer_Details"></a> Report Dettagli errore sospensione del computer  
 Il report **Dettagli errore sospensione del computer** visualizza un elenco di computer che non è stato possibile mettere in stato di sospensione o ibernazione per un motivo specifico in un periodo di tempo specificato. Questo report viene chiamato dal **Report errore sospensione** e non è progettato per essere eseguito direttamente dall'amministratore del sito.  

 Il **Report errore sospensione** indica i computer come **Non idoneo per essere sospeso** quando non sono in grado di passare allo stato di sospensione e rimangono accesi per l'intero intervallo specificato per il report. Il report indica i computer come **Non idoneo per essere messo in stato di ibernazione** quando non sono in grado di passare allo stato di ibernazione e rimangono accesi per l'intero intervallo specificato per il report.  

> [!NOTE]  
>  Il report Risparmio energia può solo raccogliere le cause che hanno impedito di entrare in stato di sospensione o ibernazione ai computer che eseguono Windows 7 o Windows Server 2008 R2.  

 Usare i parametri seguenti per configurare questo report.  

#### <a name="required-report-parameters"></a>Parametri obbligatori del report  
 I parametri seguenti devono essere specificati per eseguire il report.  

|Nome parametro|Descrizione|  
|--------------------|-----------------|  
|**Nome raccolta**|Nell'elenco a discesa selezionare una raccolta da usare per il report.|  
|**Intervallo report (giorni)**|Specificare il numero di giorni per il report. Il valore predefinito è **7** giorni.|  
|**Causa di insonnia**|Dall'elenco a discesa, selezionare una delle cause che possono impedire ai computer di immissione di sospensione o ibernazione.|  

#### <a name="hidden-report-parameters"></a>Parametri nascosti del report  
 Per questo report non sono disponibili parametri nascosti che è possibile impostare.  

#### <a name="report-links"></a>Collegamenti per il report  
 Questo report contiene collegamenti al report seguente che offre ulteriori informazioni sull'elemento selezionato.  

|Nome report|Dettagli|  
|-----------------|-------------|  
|**Dettagli computer**|Fare clic sul collegamento **Fare clic per ulteriori informazioni** per visualizzare informazioni su capacità di risparmio energia, impostazioni di risparmio energia e combinazioni per il risparmio di energia applicate per il computer selezionato.<br /><br /> Per altre informazioni, vedere la sezione [Computer Details Report](#BKMK_Computer_Details) in questo argomento.|  

###  <a name="insomnia-report"></a><a name="BKMK_Insomnia"></a> Insomnia report  
 Il **Report errore sospensione** visualizza un elenco di cause comuni che hanno impedito ai computer di entrare in stato di sospensione o di ibernazione e il numero di computer interessati da ogni causa per un periodo di tempo specificato. Esistono una serie di cause che possono impedire a un computer di entrare in stato di sospensione o ibernazione, ad esempio un processo in esecuzione nel computer, una sessione di Desktop remoto aperta o il fatto che il computer non supporti la sospensione o l'ibernazione. Da questo report è possibile aprire il report **Dettagli errore sospensione del computer** che visualizza un elenco dei computer interessati da ogni causa.  

 Il report Report errore sospensione indica i computer come **Non idoneo per essere sospeso** quando non sono in grado di passare allo stato di sospensione e rimangono accesi per l'intero intervallo specificato per il report. Il report indica i computer come **Non idoneo per essere messo in stato di ibernazione** quando non sono in grado di passare allo stato di ibernazione e rimangono accesi per l'intero intervallo specificato per il report.  

> [!NOTE]  
>  Il report Risparmio energia può solo raccogliere le cause che hanno impedito di entrare in stato di sospensione o ibernazione ai computer che eseguono Windows 7 o Windows Server 2008 R2.  

 Usare i parametri seguenti per configurare questo report.  

#### <a name="required-report-parameters"></a>Parametri obbligatori del report  
 I parametri seguenti devono essere specificati per eseguire il report.  

|Nome parametro|Descrizione|  
|--------------------|-----------------|  
|**Nome raccolta**|Nell'elenco a discesa selezionare una raccolta da usare per il report.|  
|**Intervallo report (giorni)**|Specificare il numero di giorni per il report. Il valore predefinito è **7** giorni. Il valore massimo è **365** giorni. Specificare **0** per eseguire il report per la data odierna.|  

#### <a name="hidden-report-parameters"></a>Parametri nascosti del report  
 Per questo report non sono disponibili parametri nascosti che è possibile impostare.  

#### <a name="report-links"></a>Collegamenti per il report  
 Questo report contiene collegamenti al report seguente che offre ulteriori informazioni sull'elemento selezionato.  

|Nome report|Dettagli|  
|-----------------|-------------|  
|**Dettagli errore sospensione del computer**|Fare clic su un numero nella colonna **Computer interessati** per visualizzare un elenco di computer che non è stato possibile mettere in stato di sospensione o ibernazione a causa della causa selezionata.<br /><br /> Per altre informazioni, vedere la sezione [Insomnia Computer Details Report](#BKMK_Insomnia_Computer_Details) in questo argomento.|  

###  <a name="power-capabilities-report"></a><a name="BKMK_Capabilites"></a> Report Funzionalità alimentazione  
 Il report **Funzionalità alimentazione** visualizza le capacità hardware di risparmio energia dei computer nella raccolta specificata. Questo report viene in genere usato nella fase di monitoraggio del risparmio energia per determinare le funzionalità di risparmio energia dei computer nell'organizzazione. Le informazioni visualizzate nel report possono quindi essere usate per creare raccolte di computer a cui applicare combinazioni per il risparmio di energia oppure da escludere dal risparmio energia. Le funzionalità di risparmio energia visualizzate in questo report sono:  

- **Idoneo per essere sospeso** - Indica se il computer ha la possibilità di passare allo stato di sospensione se è stato configurato per farlo.  

- **Idoneo per essere messo in stato di ibernazione** - Indica se il computer può passare allo stato di ibernazione se è stato configurato per farlo.  

- **Riattivazione da sospensione** - Indica se il computer può essere riattivato dalla sospensione se è stato configurato per farlo.  

- **Riattivazione dallo stato di ibernazione** - Indica se il computer può essere riattivato dallo stato di ibernazione se è stato configurato per farlo.  

  I valori restituiti dal report **Funzionalità di alimentazione** indicano le capacità correlate alla sospensione e all'ibernazione dei computer segnalate da Windows. Tuttavia, i valori restituiti non riflettono i casi in cui le impostazioni di Windows o del BIOS impediscono il funzionamento di queste funzionalità.  

  Usare i parametri seguenti per configurare questo report.  

#### <a name="required-report-parameters"></a>Parametri obbligatori del report  
 I parametri seguenti devono essere specificati per eseguire il report.  

|Nome parametro|Descrizione|  
|--------------------|-----------------|  
|**Raccolta**|Dall'elenco a discesa, selezionare una raccolta per il report.|  
|**Filtro visualizzazione**|Dall'elenco a discesa selezionare **Non supportato** per visualizzare solo i computer nella raccolta specificata che non sono idonei alla sospensione, ibernazione, riattivazione dalla modalità di sospensione o riattivazione dalla modalità di sospensione. Selezionare **Mostra tutto** per visualizzare tutti i computer nella raccolta specificata.|  

#### <a name="hidden-report-parameters"></a>Parametri nascosti del report  
 Per questo report non sono disponibili parametri nascosti che è possibile impostare.  

#### <a name="report-links"></a>Collegamenti per il report  
 Questo report contiene collegamenti al report seguente che offre ulteriori informazioni sull'elemento selezionato.  

|Nome report|Dettagli|  
|-----------------|-------------|  
|**Dettagli computer**|Fare clic sul nome di un computer per visualizzare informazioni su capacità di risparmio energia, impostazioni di risparmio energia e combinazioni per il risparmio di energia applicate per il computer selezionato.<br /><br /> Per altre informazioni, vedere la sezione [Computer Details Report](#BKMK_Computer_Details) in questo argomento.|  

###  <a name="power-settings-report"></a><a name="BKMK_Settings"></a> Report Impostazioni risparmio energia  
 Il report **Impostazioni risparmio energia** visualizza un elenco aggregato delle impostazioni di risparmio energia usate dai computer nella raccolta specificata. Per ogni impostazione di risparmio energia, vengono visualizzati le modalità, i valori e le unità possibili, insieme al conteggio del numero di computer che usano tali valori. Questo report può essere usato durante la fase di monitoraggio del risparmio energia per consentire all'amministratore di conoscere le impostazioni di risparmio energia esistenti usate dai computer del sito e per facilitare la pianificazione delle impostazioni di risparmio energia ottimali da applicare tramite una combinazione per il risparmio di energia. Il report è utile anche durante la risoluzione dei problemi, per verificare la corretta applicazione delle impostazioni di risparmio energia.  

> [!NOTE]  
>  Le impostazioni visualizzate vengono raccolte dai computer client durante l'inventario hardware. A seconda dell'ora in cui viene eseguito l'inventario hardware, potrebbero essere raccolte le impostazioni dalle combinazioni per il risparmio di energia in ore di punta o fuori ore di punta.  

 Usare i parametri seguenti per configurare questo report.  

#### <a name="required-report-parameters"></a>Parametri obbligatori del report  
 I parametri seguenti devono essere specificati per eseguire il report.  

|Nome parametro|Descrizione|  
|--------------------|-----------------|  
|**Nome raccolta**|Dall'elenco a discesa, selezionare una raccolta per il report.|  

#### <a name="hidden-report-parameters"></a>Parametri nascosti del report  
 I parametri nascosti seguenti possono essere specificati facoltativamente per modificare il comportamento di questo report.  

|Nome parametro|Descrizione|  
|--------------------|-----------------|  
|**numberOfLocalizations**|Specificare il numero di lingue in cui si vogliono visualizzare i nomi delle impostazioni di risparmio energia segnalati dai computer client. Se si vuole visualizzare solo la lingua più usata, lasciare il valore predefinito **1**per questa impostazione. Per visualizzare tutte le lingue, impostare questo valore su **0**.|  

#### <a name="report-links"></a>Collegamenti per il report  
 Questo report contiene collegamenti al report seguente che offre ulteriori informazioni sull'elemento selezionato.  

|Nome report|Dettagli|  
|-----------------|-------------|  
|**Dettagli impostazioni risparmio energia**|Fare clic sul numero di computer nella colonna **Computer** per visualizzare un elenco di tutti i computer che usano le impostazioni di risparmio energia in tale riga.<br /><br /> Per altre informazioni, vedere la sezione [Power Settings Details Report](#BKMK_Settings_Details) in questo argomento.|  

###  <a name="power-settings-details-report"></a><a name="BKMK_Settings_Details"></a> Power Settings Details report  
 Il report **Dettagli impostazioni risparmio energia** visualizza ulteriori informazioni sui computer selezionati nel report **Impostazioni risparmio energia** . Questo report viene chiamato dal report **Impostazioni risparmio energia** e non è progettato per essere eseguito direttamente dall'amministratore del sito.  

#### <a name="required-report-parameters"></a>Parametri obbligatori del report  
 I parametri seguenti devono essere specificati per eseguire il report.  

|Nome parametro|Descrizione|  
|--------------------|-----------------|  
|**Raccolta**|Nell'elenco a discesa selezionare una raccolta da usare per il report.|  
|**GUID impostazione per il risparmio di energia**|Dall'elenco a discesa, selezionare del GUID in cui desidera ottenere un report. Per un elenco di tutte le impostazioni di risparmio energia e il relativo uso, vedere [Impostazioni disponibili per le combinazioni per il risparmio di energia](../../../../core/clients/manage/power/create-and-apply-power-plans.md#BKMK_Plans) nell'argomento [Come creare e applicare combinazioni per il risparmio di energia](../../../../core/clients/manage/power/create-and-apply-power-plans.md).|  
|**Power Mode**|Nell'elenco a discesa selezionare il tipo di impostazioni di risparmio energia da visualizzare nei risultati del report. Selezionare **Alimentazione da rete elettrica** per visualizzare le impostazioni di risparmio energia configurate per quando il computer è collegato alla rete elettrica e **A batteria** per visualizzare le impostazioni di risparmio energia configurate per quando il computer è alimentato a batteria.|  
|**Indice impostazione**|Nell'elenco a discesa selezionare il valore per il nome dell'impostazione di risparmio energia selezionata per cui creare il report. Ad esempio, per visualizzare tutti i computer con l'opzione **Disattiva disco rigido dopo** impostata su **10** minuti, selezionare **Disattiva disco rigido dopo** in **Nome impostazione per il risparmio di energia** e **10** in **Indice impostazione**.|  

#### <a name="hidden-report-parameters"></a>Parametri nascosti del report  
 I parametri nascosti seguenti possono essere specificati facoltativamente per modificare il comportamento di questo report.  

|Nome parametro|Descrizione|  
|--------------------|-----------------|  
|**numberOfLocalizations**|Specificare il numero di lingue in cui si vogliono visualizzare i nomi delle impostazioni di risparmio energia segnalati dai computer client. Se si vuole visualizzare solo la lingua più usata, lasciare il valore predefinito **1**per questa impostazione. Per visualizzare tutte le lingue, impostare questo valore su **0**.|  

#### <a name="report-links"></a>Collegamenti per il report  
 Questo report contiene collegamenti al report seguente che offre ulteriori informazioni sull'elemento selezionato.  

|Nome report|Dettagli|  
|-----------------|-------------|  
|**Dettagli computer**|Fare clic sul nome di un computer per visualizzare informazioni su capacità di risparmio energia, impostazioni di risparmio energia e combinazioni per il risparmio di energia applicate per il computer selezionato.<br /><br /> Per altre informazioni, vedere la sezione [Computer Details Report](#BKMK_Computer_Details) in questo argomento.|  
