---
title: Scenario di esempio per la distribuzione e il monitoraggio degli aggiornamenti
titleSuffix: Configuration Manager
description: Come usare gli aggiornamenti software in Configuration Manager per distribuire e monitorare gli aggiornamenti software mensili.
ms.date: 10/21/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: c32f757a-02da-43f2-b055-5cfd097d8c43
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ea654c4ec13b95b78a65c85d9d36ce576619854e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696129"
---
# <a name="example-scenario-to-deploy-and-monitor-monthly-software-updates"></a>Scenario di esempio per la distribuzione e il monitoraggio degli aggiornamenti software mensili

*Si applica a: Configuration Manager (Current Branch)*

Questo argomento illustra uno scenario di esempio sull'uso degli aggiornamenti software in Configuration Manager per la distribuzione e il monitoraggio degli aggiornamenti software di sicurezza rilasciati ogni mese da Microsoft.  

 In questo scenario vengono analizzate le azioni dell'amministratore di Configuration Manager presso Woodgrove Bank. L'amministratore deve creare una strategia di distribuzione degli aggiornamenti software con i requisiti e le condizioni seguenti:  

- La distribuzione degli aggiornamenti del software attivo avviene una settimana dopo il rilascio da parte di Microsoft degli aggiornamenti del software di protezione il secondo martedì di ogni mese. In genere, questo evento viene definito Patch martedì.  

- Gli aggiornamenti software vengono scaricati e pre-installati nei punti di distribuzione. Una distribuzione viene quindi testata in un subset di client prima che l'amministratore di Configuration Manager distribuisca gli aggiornamenti software in un ambiente di produzione.  

- L'amministratore deve essere in grado di monitorare la conformità degli aggiornamenti software in base al mese o all'anno.  

  Questo scenario si presuppone che l'infrastruttura del punto di aggiornamento software sia già stata implementata. Usare le informazioni seguenti per pianificare e configurare gli aggiornamenti software in Configuration Manager.  

|Processo|Riferimento|  
|-------------|---------------|  
|Esaminare i concetti chiave per gli aggiornamenti software.|[Introduction to software updates](../understand/software-updates-introduction.md) (Introduzione agli aggiornamenti software)|  
|Pianificare gli aggiornamenti del software. Queste informazioni consentono di pianificare considerazioni relative alla capacità e di determinare l'infrastruttura del punto di aggiornamento software e le impostazioni di sincronizzazione e del client per gli aggiornamenti software.|[Plan for software updates](../plan-design/plan-for-software-updates.md) (Pianificare gli aggiornamenti del software)|  
|Configurare gli aggiornamenti software. Queste informazioni consentono di installare e configurare punti di aggiornamento software nella gerarchia e di configurare e sincronizzare gli aggiornamenti software.<br /><br /> In questo scenario l'amministratore di Configuration Manager configura la pianificazione di sincronizzazione degli aggiornamenti software in modo che venga eseguita il secondo mercoledì di ogni mese, così da assicurarsi di recuperare gli aggiornamenti software di sicurezza più recenti rilasciati da Microsoft.|[Synchronize software updates](../get-started/synchronize-software-updates.md) (Sincronizzare gli aggiornamenti software)|  

 Le sezioni seguenti di questo argomento includono procedure di esempio che consentono di distribuire e monitorare gli aggiornamenti software di sicurezza di Configuration Manager all'interno dell'organizzazione.

##  <a name="step-1-create-a-software-update-group-for-yearly-compliance"></a><a name="BKMK_Step1"></a> Passaggio 1: creare un gruppo di aggiornamento software per conformità annuale  
 L'amministratore di Configuration Manager crea un gruppo di aggiornamento software che può essere usato per monitorare la conformità di tutti gli aggiornamenti software di sicurezza rilasciati nel 2016. L'amministratore esegue quindi i passaggi indicati nella tabella seguente.  

|Processo|Riferimento|  
|-------------|---------------|  
|Dal nodo **Tutti gli aggiornamenti software** nella console di Configuration Manager l'amministratore di Configuration Manager aggiunge i criteri per visualizzare solo gli aggiornamenti software di sicurezza rilasciati o rivisti nel corso del 2015 che soddisfano i requisiti seguenti:<br /><br /><ul><li>**Criteri**: Data rilascio o revisione</li><li>**Condizione**: è maggiore o uguale a una data specifica<br />**Valore**: 1/1/2015</li><li>**Criteri**: Classificazione aggiornamento<br />**Valore**: Aggiornamenti della sicurezza</li><li>**Criteri**: Scaduto <br />**Valore**: No</li></ul>|Nessuna informazione aggiuntiva|
|L'amministratore di Configuration Manager aggiunge tutti gli aggiornamenti software filtrati in un nuovo gruppo di aggiornamento software con i requisiti seguenti:<br /><br /><ul><li>**Nome**: Gruppo di conformità - Aggiornamenti della sicurezza Microsoft 2015</li><li>**Descrizione**: Aggiornamenti software|[Aggiungere aggiornamenti software a un gruppo di aggiornamento](add-software-updates-to-an-update-group.md)|  

##  <a name="step-2-create-an-automatic-deployment-rule-for-the-current-month"></a><a name="BKMK_Step2"></a> Passaggio 2: creare una regola di distribuzione automatica per il mese corrente  
 L'amministratore di Configuration Manager crea una regola di distribuzione automatica per gli aggiornamenti software di protezione rilasciati da Microsoft per il mese corrente. L'amministratore esegue quindi i passaggi indicati nella tabella seguente.  

|Processo|Riferimento|  
|-------------|---------------|  
|L'amministratore di Configuration Manager crea una regola di distribuzione automatica con i requisiti seguenti:<br /><br /><ol><li>Nella scheda **Generale** l'amministratore di Configuration Manager configura quanto segue:<br /> <ul><li>Specifica **Aggiornamenti mensili della sicurezza** come nome.</li><li>Seleziona una raccolta di test con client limitati.</li><li>Seleziona **Crea un nuovo gruppo di aggiornamento software**.</li><li>Verifica che l'opzione **Abilita la distribuzione dopo l'esecuzione della regola** non sia selezionata.</li></ul></li><li>Nella scheda **Impostazioni di distribuzione** l'amministratore di Configuration Manager seleziona le impostazioni predefinite.</li><li>Nella pagina **Aggiornamenti software** l'amministratore di Configuration Manager configura i filtri proprietà e i criteri di ricerca seguenti:<br /><ul><li>Data rilascio o revisione: **Ultimo mese**.</li><li>Classificazione aggiornamento: **Aggiornamenti della sicurezza**.</li></ul></li><li>Nella pagina **Valutazione** l'amministratore di Configuration Manager abilita la regola in modo che venga eseguita secondo pianificazione il **secondo giovedì** di ogni **mese**.  L'amministratore di Configuration Manager verifica anche che la pianificazione della sincronizzazione sia impostata per essere eseguita il **secondo mercoledì** di ogni **mese**.</li><li>L'amministratore di Configuration Manager usa le impostazioni predefinite nelle pagine Pianificazione della distribuzione, Esperienza utente, Avvisi e Impostazioni download.</li><li>Nella pagina **Pacchetto di distribuzione** l'amministratore di Configuration Manager specifica un nuovo pacchetto di distribuzione.</li><li>L'amministratore di Configuration Manager usa le impostazioni predefinite nelle pagine Percorso download e Selezione lingua.</li></ol>|[Distribuire automaticamente gli aggiornamenti software](automatically-deploy-software-updates.md)|  

##  <a name="step-3-verify-that-software-updates-are-ready-to-deploy"></a><a name="BKMK_Step3"></a> Passaggio 3: verificare che gli aggiornamenti software siano pronti per la distribuzione  
 Il secondo giovedì di ogni mese l'amministratore di Configuration Manager verifica che gli aggiornamenti software siano pronti per la distribuzione. L'amministratore esegue il passaggio seguente.  

|Processo|Riferimento|  
|-------------|---------------|  
|L'amministratore di Configuration Manager verifica che la sincronizzazione degli aggiornamenti software sia stata completata correttamente.|[Software updates synchronization status](monitor-software-updates.md#BKMK_SUSyncStatus) (Stato di sincronizzazione degli aggiornamenti software)|  

##  <a name="step-4-deploy-the-software-update-group"></a><a name="BKMK_Step4"></a> Passaggio 4: distribuire il gruppo di aggiornamenti software  
 Dopo aver verificato che gli aggiornamenti software siano pronti per la distribuzione, l'amministratore di Configuration Manager distribuisce gli aggiornamenti software. L'amministratore esegue quindi i passaggi indicati nella tabella seguente.  

|Processo|Riferimento|  
|-------------|---------------|  
|L'amministratore di Configuration Manager crea due distribuzioni di prova per il nuovo gruppo di aggiornamento software. Per ogni distribuzione, considera gli ambienti seguenti:<br /><br /> **Distribuzione di test delle workstation**: per la distribuzione di test delle workstation, l'amministratore di Configuration Manager considera quanto segue:<br /><br /><ul><li>Specifica una raccolta di distribuzioni che contiene un subset di client per workstation per la verifica della distribuzione.</li><li>Configura le impostazioni di distribuzione appropriate per i client per workstation presenti nell'ambiente.</li></ul><br />**Distribuzione di test dei server**: per la distribuzione di test dei server, l'amministratore di Configuration Manager considera quanto segue:<br /><br /><ul><li>Specifica una raccolta di distribuzioni che contiene un subset di client di server per la verifica della distribuzione.</li><li>Configura le impostazioni di distribuzione appropriate per i client di server presenti nell'ambiente.</li></ul>|[Distribuire gli aggiornamenti software](deploy-software-updates.md)|  
|L'amministratore di Configuration Manager verifica che le distribuzioni di prova siano state distribuite correttamente.|[Software updates deployment status](monitor-software-updates.md#BKMK_SUDeployStatus) (Stato di distribuzione degli aggiornamenti software)|  
|L'amministratore di Configuration Manager aggiorna le due distribuzioni con nuove raccolte che includono i server e le workstation di produzione.|Nessuna informazione aggiuntiva|  

##  <a name="step-5-monitor-compliance-for-deployed-software-updates"></a><a name="BKMK_Step5"></a> Passaggio 5: monitorare la conformità per gli aggiornamenti del software distribuito  
 L'amministratore di Configuration Manager monitora la conformità delle distribuzioni degli aggiornamenti software. L'amministratore esegue quindi il passaggio indicato nella tabella seguente.  

|Processo|Riferimento|  
|-------------|---------------|  
|L'amministratore di Configuration Manager esegue il monitoraggio dello stato della distribuzione degli aggiornamenti software nella console di Configuration Manager e controlla i relativi report disponibili nella console.|[Monitorare gli aggiornamenti software](../../sum/deploy-use/monitor-software-updates.md)|  

##  <a name="step-6-add-monthly-software-updates-to-the-yearly-update-group"></a><a name="BKMK_Step6"></a> Passaggio 6: aggiungere gli aggiornamenti software mensili al gruppo di aggiornamento annuale  
 L'amministratore di Configuration Manager aggiunge gli aggiornamenti software dal gruppo di aggiornamento software mensile al gruppo di aggiornamento software annuale. L'amministratore esegue quindi il passaggio indicato nella tabella seguente.  

|Processo|Riferimento|  
|-------------|---------------|  
|L'amministratore di Configuration Manager seleziona gli aggiornamenti software dal gruppo di aggiornamento mensile e li aggiunge al gruppo di aggiornamento creato per la conformità annuale. Tiene traccia della conformità degli aggiornamenti software e crea diversi report per la gestione.|[Add software updates to a deployed update group](add-software-updates-to-an-update-group.md) (Aggiungere gli aggiornamenti software a un gruppo di aggiornamento distribuito)|  

L'amministratore di Configuration Manager ha completato la distribuzione mensile per gli aggiornamenti del software di protezione. Continua a monitorare e a creare report relativi alla compatibilità degli aggiornamenti software per assicurarsi che i client presenti nell'ambiente rientrino nei livelli di conformità accettabili.  

##  <a name="recurring-monthly-process-to-deploy-software-updates"></a><a name="BKMK_MonthlyProcess"></a> Processo mensile ricorrente per la distribuzione degli aggiornamenti software  
 Dopo il primo mese di distribuzione degli aggiornamenti software, l'amministratore di Configuration Manager esegue la procedura (dal passaggio 3 al passaggio 6) per distribuire gli aggiornamenti mensili del software di protezione rilasciati da Microsoft.  
