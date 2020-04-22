---
title: Distribuire manualmente gli aggiornamenti software
titleSuffix: Configuration Manager
description: Creare manualmente le distribuzioni software per mantenere aggiornati i client con gli aggiornamenti software necessari o per distribuire gli aggiornamenti fuori programma.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 57184274-5fea-4d79-a2b4-22e08ed26daf
ms.openlocfilehash: b7d6640beb9353d5c613cf38e3f880e7fd76b393
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81699239"
---
# <a name="manually-deploy-software-updates"></a>Distribuire manualmente gli aggiornamenti software  

*Si applica a: Configuration Manager (Current Branch)*

La distribuzione manuale degli aggiornamenti software consiste nel processo di selezione degli aggiornamenti software dalla console di Configuration Manager e di avvio manuale del processo di distribuzione. In alternativa, è possibile aggiungere gli aggiornamenti software selezionati a un gruppo di aggiornamento, quindi distribuire manualmente il gruppo di aggiornamento. In genere si usano le distribuzioni manuali per mantenere aggiornati i client con gli aggiornamenti software necessari. È quindi possibile usare le regole di distribuzione automatica (ADR) per gestire le distribuzioni degli aggiornamenti software mensili in corso. Usare questo metodo manuale anche per distribuire gli aggiornamenti software fuori programma. Per altre informazioni sul metodo di distribuzione appropriato da usare, vedere [Distribuire gli aggiornamenti software](deploy-software-updates.md).



##  <a name="step-1-specify-search-criteria-for-software-updates"></a><a name="BKMK_1SearchCriteria"></a> Passaggio 1: Specificare i criteri di ricerca per gli aggiornamenti software  

A seconda delle combinazioni di prodotti e classificazioni sincronizzate dal sito, esistono potenzialmente migliaia di aggiornamenti software visualizzati nella console di Configuration Manager. Il primo passaggio del flusso di lavoro per la distribuzione manuale degli aggiornamenti software consiste nell'identificare gli aggiornamenti software che si desidera distribuire. Ad esempio, è possibile visualizzare tutti gli aggiornamenti software necessari in oltre 50 dispositivi client con **Sicurezza** o **Errore critico** come classificazione.  

> [!IMPORTANT]  
>  Per una singola distribuzione di aggiornamenti software è previsto un limite di 1.000 aggiornamenti software.  

### <a name="process-to-specify-search-criteria-for-software-updates"></a>Processo per specificare i criteri di ricerca per gli aggiornamenti software  

1.  Nella console di Configuration Manager passare all'area di lavoro **Raccolta software**, espandere **Aggiornamenti software** e fare clic su **Tutti gli aggiornamenti software**. Questo nodo visualizza gli aggiornamenti software sincronizzati.  

    > [!NOTE]  
    >  Il nodo **Tutti gli aggiornamenti software** visualizza solo gli aggiornamenti software con classificazione **Errore critico** e **Sicurezza** rilasciati negli ultimi 30 giorni.  

2.  Nel riquadro di ricerca applicare il filtro per identificare gli aggiornamenti software necessari. Usare una o entrambe le opzioni seguenti:  

    -   Nella casella di testo di ricerca digitare una stringa di ricerca che consenta di filtrare gli aggiornamenti software. Ad esempio, digitare l'ID articolo o l'ID bollettino per un aggiornamento software specifico. In alternativa, immettere una stringa visualizzata nel titolo di diversi aggiornamenti software.  

    -   Fare clic su **Aggiungi criteri** e selezionare i criteri per filtrare gli aggiornamenti software. Fare clic su **Aggiungi** e quindi fornire i valori per i criteri.  

3.  Fare clic su **Cerca** per filtrare gli aggiornamenti software.  

    > [!TIP]  
    >  Salvare i criteri di filtro usati di frequente. Nella barra multifunzione fare clic sull'opzione per **Salva ricerca corrente**. Recuperare le ricerche precedenti facendo clic su **Ricerche salvate**.   



##  <a name="step-2-create-a-software-update-group-that-contains-the-software-updates"></a><a name="BKMK_2UpdateGroup"></a> Passaggio 2: Creare un gruppo di aggiornamenti software che contiene gli aggiornamenti software   

I gruppi di aggiornamento software consentono di organizzare gli aggiornamenti software in preparazione per la distribuzione. Usare la procedura seguente per aggiungere manualmente gli aggiornamenti software in un nuovo gruppo di aggiornamento software.  

### <a name="process-to-manually-add-software-updates-to-a-new-software-update-group"></a>Processo per aggiungere manualmente gli aggiornamenti software a un nuovo gruppo di aggiornamento software  

1.  Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software** e selezionare **Aggiornamenti software**. Selezionare gli aggiornamenti software desiderati.  

2.  Fare clic su **Crea gruppo di aggiornamento software** nella barra multifunzione.  

3.  Specificare il nome per il gruppo di aggiornamento software e fornire una descrizione facoltativa. Usare un nome e una descrizione che forniscano informazioni sufficienti per determinare il tipo di aggiornamenti che si trovano nel gruppo di aggiornamento software. Scegliere **Crea**.  

4.  Selezionare il nodo **Gruppi di aggiornamenti software** e selezionare il nuovo gruppo di aggiornamento software. Per visualizzare l'elenco degli aggiornamenti nel gruppo, fare clic su **Mostra membri** nella barra multifunzione.  



##  <a name="step-3-download-the-content-for-the-software-update-group"></a><a name="BKMK_3DownloadContent"></a> Passaggio 3: Scaricare il contenuto per il gruppo di aggiornamenti software  

Prima di distribuire gli aggiornamenti software, scaricare il contenuto degli aggiornamenti software nel gruppo di aggiornamento software. Questo passaggio consente di verificare che il contenuto sia disponibile nei punti di distribuzione prima di distribuire gli aggiornamenti software. Consente inoltre di evitare eventuali problemi imprevisti con la distribuzione del contenuto. Se si ignora questo passaggio, come parte del processo di distribuzione il sito scarica il contenuto e lo distribuisce nei punti di distribuzione. Usare la procedura seguente per scaricare il contenuto per gli aggiornamenti software nel gruppo di aggiornamento software.  


### <a name="process-to-download-content-for-the-software-update-group"></a>Processo per scaricare il contenuto per il gruppo di aggiornamento software
[!INCLUDE [downloadupdates](../includes/downloadupdates.md)]

### <a name="process-to-monitor-content-status"></a>Processo per monitorare lo stato del contenuto
1. Per monitorare lo stato del contenuto per gli aggiornamenti software, passare all'area di lavoro **Monitoraggio** nella console di Configuration Manager. Espandere **Stato distribuzione** e quindi selezionare il nodo **Stato contenuto**.  

2. Selezionare il pacchetto di aggiornamento software precedentemente identificato per scaricare gli aggiornamenti software nel gruppo di aggiornamento software.  

3. Fare clic su **Visualizza stato** nella barra multifunzione.  



##  <a name="step-4-deploy-the-software-update-group"></a><a name="BKMK_4DeployUpdateGroup"></a> Passaggio 4: Distribuire il gruppo di aggiornamenti software  

Dopo avere determinato gli aggiornamenti da distribuire e averli aggiunti a un gruppo di aggiornamento software, distribuire manualmente il gruppo di aggiornamento software.  

### <a name="process-to-manually-deploy-the-software-updates-in-a-software-update-group"></a>Processo per distribuire manualmente gli aggiornamenti software in un gruppo di aggiornamento software  

1. Nella console di Configuration Manager passare all'area di lavoro **Raccolta software**, espandere **Aggiornamenti software** e selezionare il nodo **Gruppi di aggiornamenti software**.  

2. Selezionare il gruppo di aggiornamento software che si vuole distribuire. Fare clic su **Distribuisci** nella barra multifunzione.   

3. Nella pagina **Generale** della Distribuzione guidata degli aggiornamenti software configurare le impostazioni seguenti:  

   -   **Nome**: specificare il nome per la distribuzione. La distribuzione deve avere un nome univoco che ne descriva lo scopo e la distingua da altre distribuzioni nel sito. Questo campo del nome prevede un limite di 256 caratteri. Per impostazione predefinita, Configuration Manager fornisce automaticamente un nome per la distribuzione nel formato seguente: `Microsoft Software Updates - YYYY-MM-DD <time>`  

   -   **Descrizione**: specificare una descrizione per la distribuzione. La descrizione è facoltativa, ma fornisce una panoramica della distribuzione. Includere eventuali altre informazioni rilevanti per identificare e distinguere la distribuzione dalle altre nel sito. Il campo della descrizione ha un limite di 256 caratteri e un valore vuoto per impostazione predefinita.  

   -   **Aggiornamento software/gruppo di aggiornamenti software**: verificare che il gruppo di aggiornamenti software o l'aggiornamento software visualizzato siano corretti.  

   -   **Seleziona modello di distribuzione**: specificare se applicare un modello di distribuzione precedentemente salvato. Configurare un modello di distribuzione per salvare le proprietà di distribuzione degli aggiornamenti software comuni. Applicare quindi il modello quando si distribuiscono gli aggiornamenti software in futuro. Questi modelli consentono di risparmiare tempo e garantire la coerenza tra le distribuzioni simili.  

   -   **Raccolta**: specificare la raccolta per questa distribuzione. I dispositivi nella raccolta ricevono gli aggiornamenti software di questa distribuzione.  

4. Nella pagina **Impostazioni distribuzione** configurare le impostazioni seguenti:  

   -   **Tipo di distribuzione**: specificare il tipo di distribuzione per la distribuzione degli aggiornamenti software.  

       > [!IMPORTANT]  
       >  Dopo aver creato la distribuzione degli aggiornamenti software, non è possibile modificare il tipo di distribuzione.  

        - Selezionare **Richiesto** per creare una distribuzione degli aggiornamenti software obbligatoria. Gli aggiornamenti software vengono installati automaticamente nei client prima della scadenza di installazione configurata.  

        - Selezionare **Disponibile** per creare una distribuzione degli aggiornamenti software facoltativa. Questa distribuzione è disponibile per l'installazione da parte degli utenti in Software Center.  

       > [!NOTE]  
       >  Quando si distribuisce un gruppo di aggiornamento software come **Richiesto**, i client scaricano il contenuto in background rispettando le impostazioni BITS, se configurate.  
       > 
       > Per i gruppi di aggiornamenti software distribuiti come **Disponibile** i client scaricano il contenuto in primo piano ignorando le impostazioni BITS.  

   -   **Usa riattivazione LAN per riattivare i client per le distribuzioni richieste**: specifica se abilitare la riattivazione LAN alla scadenza. La funzione di riattivazione LAN invia pacchetti di riattivazione ai computer che richiedono uno o più aggiornamenti software nella distribuzione. Il sito riattiva tutti i computer in modalità sospensione all'ora di scadenza dell'installazione in modo che l'installazione venga avviata. I client in modalità sospensione che non richiedono aggiornamenti software nella distribuzione non vengono avviati. Per impostazione predefinita, questa impostazione non è abilitata. È disponibile solo per le distribuzioni **obbligatorie**. Prima di usare questa opzione, configurare i computer e le reti per la riattivazione LAN. Per altre informazioni, vedere [Come configurare la riattivazione LAN](../../core/clients/deploy/configure-wake-on-lan.md).  

   -   **Livello dettaglio**: specificare il livello di dettaglio per i messaggi di stato segnalati dai client nel sito.  

5. Nella pagina **Pianificazione** configurare le impostazioni seguenti:  

   -   **Pianificazione della valutazione**: specificare l'ora in cui Configuration Manager valuta il tempo disponibile e le scadenze dell'installazione. Scegliere se usare l'ora UTC (Coordinated Universal Time) oppure l'ora locale del computer in cui viene eseguita la console di Configuration Manager.  

       - Quando qui si seleziona **Ora locale client** e quindi **Appena possibile** come opzione di **Tempo disponibile software**, per valutare la disponibilità degli aggiornamenti viene usata l'ora corrente nel computer che esegue la console di Configuration Manager. Questo comportamento è analogo con l'opzione **Scadenza installazione** e l'ora in cui gli aggiornamenti vengono installati in un client. Se il client si trova in un fuso orario diverso, le azioni seguenti vengono eseguite quando l'ora del client corrisponde a quella impostata per la valutazione.  

   -   **Tempo disponibile software**: selezionare una delle seguenti impostazioni per specificare quando gli aggiornamenti software saranno disponibili per i client:  

       -   **Appena possibile**: questa impostazione consente di rendere disponibili prima possibile gli aggiornamenti software nella distribuzione per i client. Quando si crea la distribuzione con questa impostazione selezionata, Configuration Manager aggiorna i criteri client. Al successivo ciclo di polling dei criteri client, ai client viene comunicata la distribuzione e gli aggiornamenti software risultano disponibili per l'installazione.  

       -   **Orario specifico**: rende disponibili gli aggiornamenti software nella distribuzione per i client in una data e a un orario specifici. Quando si crea la distribuzione con questa impostazione attivata, Configuration Manager aggiorna i criteri client. La distribuzione viene comunicata ai client in occasione del successivo ciclo di polling dei criteri client. Gli aggiornamenti del software nella distribuzione non sono però disponibili per l'installazione prima della data e dell'orario configurati.  

   -   **Scadenza installazione**: queste opzioni sono disponibili solo per le distribuzioni **obbligatorie**. Selezionare una delle impostazioni seguenti per specificare la scadenza per l'installazione degli aggiornamenti software nella distribuzione.  

       -   **Appena possibile**: selezionare questa impostazione per installare automaticamente gli aggiornamenti software nella distribuzione appena possibile.  

       -   **Orario specifico**: selezionare questa impostazione per installare automaticamente gli aggiornamenti software nella distribuzione in una data e a un orario specifici.  

           - L'orario effettivo di scadenza dell'installazione corrisponde all'ora di scadenza visualizzata più una quantità di tempo casuale di massimo due ore. Questo valore casuale riduce il potenziale impatto di un'installazione simultanea degli aggiornamenti nella distribuzione da parte dei client nella raccolta.   

           - Per disabilitare il ritardo della sequenza casuale di installazione per gli aggiornamenti software obbligatori, configurare l'impostazione client **Disabilitare sequenza casuale scadenza** nel gruppo **Agente computer**. Per altre informazioni, vedere le impostazioni client di [Agente computer](../../core/clients/deploy/about-client-settings.md#computer-agent).  

   -  **Ritardare l'imposizione di questa distribuzione in base alle preferenze dell'utente, fino al periodo di tolleranza massimo definito nelle impostazioni del client**: Abilitare questa impostazione per concedere agli utenti più tempo per installare gli aggiornamenti software necessari, oltre la data di scadenza.  

       - Questo comportamento è in genere necessario quando un computer è stato disattivato per molto tempo ed è necessario installare molte applicazioni o aggiornamenti software, come nel caso, ad esempio, di un utente che, tornato da una vacanza, deve attendere parecchio tempo mentre il client installa le distribuzioni scadute.  

       - Configurare il periodo di tolleranza con la proprietà **Periodo di tolleranza per l'imposizione dopo la scadenza della distribuzione (ore)** nelle impostazioni del client. Per altre informazioni, vedere la sezione [Agente computer](../../core/clients/deploy/about-client-settings.md#computer-agent). Tale periodo di tolleranza si applica a tutte le distribuzioni con questa opzione abilitata e destinate a dispositivi in cui è stata distribuita anche l'impostazione del client.  

       - Dopo la scadenza il client installa gli aggiornamenti software nella prima finestra non lavorativa, configurata dall'utente, fino al termine del periodo di tolleranza. L'utente può però aprire comunque Software Center e installare gli aggiornamenti software in qualsiasi momento. Una volta scaduto il periodo di tolleranza, le distribuzioni scadute torneranno al normale comportamento.  

6. Nella pagina **Esperienza utente** è possibile configurare le impostazioni seguenti:  

   -   **Notifiche utente**: specificare se visualizzare la notifica in Software Center nell'orario configurato in **Tempo disponibile software**. Questa impostazione consente di stabilire anche se inviare notifiche agli utenti nei computer client. Per le distribuzioni **disponibili** non è possibile selezionare l'opzione **Nascondi in Software Center e nascondi tutte le notifiche**.  

   -   **Comportamento scadenza**: questa impostazione è configurabile solo per le distribuzioni **obbligatorie**. Specificare i comportamenti da adottare quando la distribuzione dell'aggiornamento software raggiunge la scadenza oltre qualsiasi finestra di manutenzione definita. Le opzioni disponibili consentono di scegliere se installare gli aggiornamenti software ed eseguire un riavvio del sistema dopo l'installazione. Per altre informazioni sulle finestre di manutenzione, vedere [Come usare le finestre di manutenzione](../../core/clients/manage/collections/use-maintenance-windows.md). 
  
       > [!Note]
       > Si applica solo quando la finestra di manutenzione è configurata per il dispositivo client. Se nel dispositivo non è definita una finestra di manutenzione, l'aggiornamento dell'installazione e il riavvio vengono sempre eseguiti dopo la scadenza.

   -   **Comportamento riavvio dispositivo**: questa impostazione è configurabile solo per le distribuzioni **obbligatorie**. Specificare se evitare un riavvio del sistema in server e workstation se è necessario un riavvio del sistema per completare l'installazione dell'aggiornamento.  

       > [!WARNING]  
       >  La disattivazione dei riavvii del sistema può essere utile in ambienti server o quando non si vuole che i computer di destinazione vengano riavviati per impostazione predefinita. Con tale impostazione, però, i computer potrebbero trovarsi in uno stato non protetto. Un riavvio forzato assicura il completamento immediato dell'installazione degli aggiornamenti software.  

   -   **Gestione filtri di scrittura per dispositivi con Windows Embedded**: questa impostazione controlla il comportamento di installazione nei dispositivi con Windows Embedded in cui è abilitato un filtro di scrittura. Scegliere l'opzione per eseguire il commit delle modifiche alla scadenza dell'installazione o durante una finestra di manutenzione. Quando si seleziona questa opzione, è necessario un riavvio e la modifica viene salvata in modo permanente nel dispositivo. In caso contrario, l'aggiornamento viene installato, applicato all'overlay temporaneo e sottoposto a commit successivamente.  

       -  Quando si distribuisce un aggiornamento software in un dispositivo con Windows Embedded, verificare che il dispositivo appartenga a una raccolta che ha una finestra di manutenzione configurata.  

   - **Comportamento di rivalutazione della distribuzione degli aggiornamenti software al riavvio**: selezionare questa impostazione per configurare le distribuzioni degli aggiornamenti software, in modo che i client eseguano un'analisi della conformità degli aggiornamenti software immediatamente dopo l'installazione degli aggiornamenti software e il riavvio. Questa impostazione consente al client di controllare la presenza di aggiornamenti aggiuntivi che diventano applicabili dopo il riavvio e di installarli durante la stessa finestra di manutenzione.  

7. Nella pagina **Avvisi** configurare la modalità di generazione degli avvisi per questa distribuzione in Configuration Manager. Esaminare gli avvisi recenti relativi agli aggiornamenti software nel nodo **Aggiornamenti software** dell'area di lavoro **Raccolta software**. Se si usa anche System Center Operations Manager, configurare i rispettivi avvisi. Configurare gli avvisi solo per le distribuzioni **obbligatorie**.  

8. Nella pagina **Impostazioni download** configurare le impostazioni seguenti:  

    > [!NOTE]  
    >  I client richiedono il percorso del contenuto da un punto di gestione per gli aggiornamenti software in una distribuzione. Il comportamento di download dipende dalla configurazione del punto di distribuzione, del pacchetto di distribuzione e delle impostazioni in questa pagina.  

    - Specificare se i client devono scaricare e installare gli aggiornamenti quando usano un punto di distribuzione da un gruppo di limiti vicino o dai gruppi di limiti del sito predefiniti.  

    - Specificare se i clienti devono scaricare e installare gli aggiornamenti da un punto di distribuzione nel gruppo di limiti del sito predefinito quando il contenuto degli aggiornamenti software non è disponibile da un punto di distribuzione nel gruppo di limiti corrente o nei gruppi di limiti vicini.  

    - **Consenti ai client di condividere il contenuto con altri client nella stessa subnet**: specificare se consentire l'uso di BranchCache per i download del contenuto. Per altre informazioni, vedere [BranchCache](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache). A partire dalla versione 1802, BranchCache è sempre abilitato nei client. Questa impostazione è stata rimossa perché i client usano BranchCache se supportato dal punto di distribuzione.  

    - **Se gli aggiornamenti software non sono disponibili nel punto di distribuzione nei gruppi di limiti correnti, vicini o del sito, scaricare il contenuto da Microsoft Update**: selezionare questa impostazione per consentire ai client connessi all'Intranet di scaricare gli aggiornamenti software da Microsoft Update se non sono disponibili nei punti di distribuzione. I client basati su Internet passano sempre a Microsoft Update per il contenuto degli aggiornamenti software.

    - Specificare se consentire ai client di eseguire il download dopo una scadenza dell'installazione quando usano connessioni Internet a consumo. I provider Internet talvolta applicano un addebito per il traffico dati in entrata e in uscita quando si usa una connessione a consumo.  

9. Nella pagina **Pacchetto di distribuzione** selezionare una delle opzioni seguenti:  

    > [!Note]  
    > Se è stato già eseguito il [Passaggio 3: Scaricare il contenuto per il gruppo di aggiornamento software](#BKMK_3DownloadContent), la procedura guidata non visualizza le pagine **Pacchetto di distribuzione**, **Punti di distribuzione** e **Selezione lingua**. Andare alla pagina [Riepilogo](#bkmk_summary) della procedura guidata.  
    > 
    >  Gli aggiornamenti software precedentemente scaricati nella raccolta contenuto sul server del sito non vengono scaricati nuovamente. Questo comportamento vale anche quando si crea un nuovo pacchetto di distribuzione per gli aggiornamenti software. Se tutti gli aggiornamenti software sono stati già scaricati, la procedura guidata passa alla pagina [Riepilogo](#bkmk_summary).  

    - **Seleziona un pacchetto di distribuzione**: consente di aggiungere questi aggiornamenti a un pacchetto di distribuzione esistente.  

    - **Crea un nuovo pacchetto di distribuzione**: consente di aggiungere questi aggiornamenti a un nuovo pacchetto di distribuzione. Configurare le impostazioni aggiuntive seguenti:  

        -  **Nome**: specificare il nome del pacchetto di distribuzione. Usare un nome univoco che descrive il contenuto del pacchetto. Il nome può contenere un massimo di 50 caratteri.  

        -  **Descrizione**: specificare una descrizione che includa informazioni sul pacchetto di distribuzione. La descrizione facoltativa può contenere un massimo di 127 caratteri.  

        -  **Origine pacchetto**: specificare il percorso dei file di origine dell'aggiornamento software. Digitare un percorso di rete per il percorso di origine, ad esempio `\\server\sharename\path`, oppure fare clic su **Sfoglia** per trovare il percorso di rete. Prima di procedere alla pagina successiva, è necessario creare la cartella condivisa per i file di origine del pacchetto di distribuzione.  

            - Non è possibile usare il percorso specificato come origine di un altro pacchetto di distribuzione software.  

            - È possibile modificare il percorso di origine del pacchetto nelle proprietà del pacchetto di distribuzione dopo che Configuration Manager ha creato il pacchetto di distribuzione. In tal caso, è necessario copiare prima il contenuto dell'origine del pacchetto originale nel nuovo percorso di origine del pacchetto.  

            -  L'account computer del provider SMS e l'utente che esegue la procedura guidata per scaricare gli aggiornamenti software devono disporre entrambi delle autorizzazioni di **Scrittura** per il percorso di download. Limitare l'accesso al percorso di download. Questa restrizione riduce il rischio che utenti malintenzionati possano manomettere i file di origine degli aggiornamenti software.  

        -  **Priorità di invio**: specificare la priorità di invio per il pacchetto di distribuzione. Configuration Manager usa tale priorità quando invia il pacchetto di distribuzione ai punti di distribuzione. I pacchetti di distribuzione vengono inviati in ordine di priorità, ovvero Alta, Media o Bassa. I pacchetti con priorità identiche vengono inviati nell'ordine in cui sono stati creati. Se non esiste alcun backlog, il pacchetto esegue immediatamente l'elaborazione, indipendentemente dalla priorità configurata.  

        - **Abilita replica differenziale binaria**: selezionare questa impostazione per ridurre al minimo il traffico di rete tra siti. La replica differenziale binaria aggiorna soltanto il contenuto del pacchetto che è stato modificato e non l'intero contenuto. Per altre informazioni, vedere [Replica differenziale binaria](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#binary-differential-replication).  

    - **Nessun pacchetto di distribuzione**: a partire dalla versione 1806, è possibile distribuire gli aggiornamenti software nei dispositivi senza prima scaricare e distribuire il contenuto nei punti di distribuzione. Questa impostazione è utile quando il contenuto degli aggiornamenti è particolarmente esteso. Usarla anche quando si vuole che i client ottengano sempre i contenuti dal servizio cloud Microsoft Update. I client in questo scenario possono anche scaricare il contenuto da peer in cui è già presente il contenuto necessario. Il client Gestione configurazione continua a gestire il download del contenuto, quindi è in grado di usare la funzionalità peer cache di Configuration Manager o altre tecnologie, ad esempio Ottimizzazione recapito. Questa funzionalità supporta qualsiasi tipo di aggiornamento supportato dalla gestione degli aggiornamenti software di Configuration Manager, tra cui gli aggiornamenti di Windows e Office.<!--1357933-->  

10. Nella pagina **Punti di distribuzione** specificare i punti di distribuzione o i gruppi di punti di distribuzione che ospiteranno i file di aggiornamento software. Per altre informazioni sui punti di distribuzione, vedere [Configurazioni dei punti di distribuzione](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs).  

    > [!Note]  
    > Se è stato già eseguito il [Passaggio 3: Scaricare il contenuto per il gruppo di aggiornamento software](#BKMK_3DownloadContent), la procedura guidata non visualizza le pagine **Pacchetto di distribuzione**, **Punti di distribuzione** e **Selezione lingua**. Andare alla pagina [Riepilogo](#bkmk_summary) della procedura guidata.  

11. Nella pagina **Percorso download** specificare se scaricare i file di aggiornamento software da Internet o dalla rete locale. Configurare le seguenti impostazioni:  

    -   **Scarica aggiornamenti software da Internet**: selezionare questa impostazione per scaricare gli aggiornamenti software da un percorso specificato su Internet. Questa opzione è attivata per impostazione predefinita.  

    -   **Scarica aggiornamenti software dal seguente percorso nella rete locale**: selezionare questa impostazione per scaricare gli aggiornamenti software da una cartella condivisa o da una directory locale. Questa impostazione è utile quando il computer che esegue la procedura guidata non dispone di accesso a Internet. I computer con accesso a Internet possono scaricare preventivamente gli aggiornamenti e archiviarli in un percorso nella rete locale accessibile al computer che esegue la procedura guidata.  

12. Nella pagina **Selezione lingua** selezionare le lingue per le quali il sito scarica gli aggiornamenti software selezionati. Il sito scarica questi aggiornamenti solo se sono disponibili nelle lingue selezionate. Gli aggiornamenti software non specifici della lingua vengono sempre scaricati. Per impostazione predefinita, la procedura guidata consente di selezionare le lingue configurate nelle proprietà del punto di aggiornamento software. Prima di procedere alla pagina successiva, è necessario selezionare almeno una lingua. Quando si selezionano solo lingue non supportate da un aggiornamento software, il download dell'aggiornamento non riesce.  

    > [!Note]  
    > Se è stato già eseguito il [Passaggio 3: Scaricare il contenuto per il gruppo di aggiornamento software](#BKMK_3DownloadContent), la procedura guidata non visualizza le pagine **Pacchetto di distribuzione**, **Punti di distribuzione** e **Selezione lingua**. Andare alla pagina [Riepilogo](#bkmk_summary) della procedura guidata.  

13. <a name="bkmk_summary"></a> Nella pagina **Riepilogo** verificare le impostazioni. Per salvare le impostazioni in un modello di distribuzione, fare clic su **Salva come modello**. Immettere un nome e selezionare le impostazioni che si desidera includere nel modello, quindi fare clic su **Salva**. Per modificare un'impostazione configurata, fare clic sulla pagina della procedura guidata associata e modificare l'impostazione.  

    -  Il nome del modello può essere costituito da caratteri ASCII alfanumerici, nonché da `\` (barra rovesciata) o da `'` (virgoletta singola).  

14. Fare clic su **Avanti** per distribuire l'aggiornamento software.  

    Dopo aver completato la procedura guidata, Configuration Manager scarica gli aggiornamenti software nella raccolta contenuto del server del sito. Distribuisce quindi il contenuto nei punti di distribuzione configurati e distribuisce il gruppo di aggiornamento software nei client della raccolta di destinazione. Per altre informazioni sul processo di distribuzione, vedere [Software update deployment process](../understand/software-updates-introduction.md#BKMK_DeploymentProcess).  



## <a name="next-steps"></a>Passaggi successivi
[Monitorare gli aggiornamenti software](monitor-software-updates.md)
