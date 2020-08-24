---
title: Distribuire automaticamente gli aggiornamenti software
titleSuffix: Configuration Manager
description: Per distribuire automaticamente gli aggiornamenti software, si usano le regole di distribuzione automatica.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 07/10/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: b27682de-adf8-4edd-9572-54886af8f7fb
ms.openlocfilehash: 3f49d7d001de07a7d3d6a7bdbb5f9ff90de018c9
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699875"
---
#  <a name="automatically-deploy-software-updates"></a>Distribuire automaticamente gli aggiornamenti software  

*Si applica a: Configuration Manager (Current Branch)*

Usare una regola di distribuzione automatica invece di aggiungere nuovi aggiornamenti a un gruppo di aggiornamento software esistente. Solitamente si usano le regole di distribuzione automatica per distribuire mensilmente gli aggiornamenti software, comunemente noti anche come aggiornamenti Patch Tuesday, e per gestire gli aggiornamenti delle definizioni di Endpoint Protection. Per altre informazioni su come determinare il metodo di distribuzione da usare, vedere [Distribuire gli aggiornamenti software](deploy-software-updates.md).


##  <a name="create-an-automatic-deployment-rule-adr"></a><a name="BKMK_CreateAutomaticDeploymentRule"></a> Creare una regola di distribuzione automatica (ADR)  
Approvare e distribuire automaticamente gli aggiornamenti software usando una regola di distribuzione automatica. La regola può aggiungere gli aggiornamenti software a un nuovo gruppo di aggiornamento software ogni volta che la regola viene eseguita oppure aggiungere gli aggiornamenti software a un gruppo esistente. Quando una regola viene eseguita e aggiunge aggiornamenti software a un gruppo esistente, la regola rimuove tutti gli aggiornamenti software dal gruppo e quindi aggiunge al gruppo gli aggiornamenti che soddisfano i criteri definiti. 

> [!WARNING]  
>  Prima di creare una regola di distribuzione automatica per la prima volta, verificare che il sito abbia completato la sincronizzazione degli aggiornamenti software. Questo passaggio è importante quando si esegue Configuration Manager in una lingua diversa dall'inglese. Le classificazioni di aggiornamento software vengono visualizzate in lingua inglese prima della sincronizzazione iniziale e, al termine di tale operazione, sono visualizzate nelle lingue localizzate. Le regole create prima della sincronizzazione degli aggiornamenti software potrebbero non funzionare correttamente dopo la sincronizzazione perché la stringa di testo potrebbe non corrispondere.  


### <a name="process-to-create-an-adr"></a><a name="bkmk_adr-process"></a> Processo per creare una regola di distribuzione automatica  

1.  Nella console di Configuration Manager passare all'area di lavoro **Raccolta software**, espandere **Aggiornamenti software** e selezionare il nodo **Regole di distribuzione automatica**.  

2.  Nella barra multifunzione fare clic su **Crea regola di distribuzione automatica**.  

3.  Nella pagina **Generale** della Creazione guidata delle regole di distribuzione automatica configurare le impostazioni seguenti:  

    -   **Nome**: specificare il nome per la regola di distribuzione automatica. Il nome deve essere univoco, descrivere lo scopo della regola e contribuire a distinguerla dalle altre presenti nel sito di Configuration Manager.  

    -   **Descrizione**: specificare una descrizione per la regola di distribuzione automatica. La descrizione deve fornire una panoramica della regola di distribuzione, nonché le altre informazioni rilevanti per differenziare la regola dalle altre. Il campo della descrizione è facoltativo, ha un limite di 256 caratteri e un valore vuoto per impostazione predefinita.  

    -   **Modello**: selezionare un modello di distribuzione per specificare se devono essere applicate le configurazioni di regole di distribuzione automatica salvate in precedenza. Configurare un modello di distribuzione che contenga più proprietà di distribuzione degli aggiornamenti comuni utilizzabili durante la creazione delle regole di distribuzione automatica. Questi modelli consentono di risparmiare tempo e garantire la coerenza tra le distribuzioni simili. Scegliere uno dei modelli di distribuzione degli aggiornamenti software predefiniti elencati di seguito:  

         - Il modello **Patch martedì** offre impostazioni comuni da usare quando si distribuiscono aggiornamenti software su base ciclica mensile.  

         - Il modello **Aggiornamenti del client Office 365** offre impostazioni comuni da usare quando si distribuiscono aggiornamenti per client Microsoft 365 Apps.
             > [!Note]
             > A partire dal 21 aprile 2020 Office 365 ProPlus viene rinominato come **App di Microsoft 365 per grandi imprese**. Se le regole di distribuzione automatica si basano sulla proprietà "Titolo", a partire dal 9 giugno 2020 sarà necessario modificare questa proprietà. `Microsoft 365 Apps Update - Semi-annual Channel Version 1908 for x64 based Edition (Build 11929.50000)` è un esempio del nuovo titolo. Per altre informazioni sulla modifica delle regole di distribuzione automatica per la modifica del titolo, vedere [Aggiornare i canali per le app Microsoft 365](manage-office-365-proplus-updates.md#bkmk_channel). Per altre informazioni sulla modifica dei nomi, vedere [Modifica dei nomi di Office 365 ProPlus](/deployoffice/name-change).

         - Il modello **Aggiornamenti di SCEP e di Windows Defender Antivirus** offre impostazioni comuni da usare quando si distribuiscono aggiornamenti delle definizioni di Endpoint Protection.  

    -   **Raccolta**: specifica la raccolta di destinazione da usare per la distribuzione. I membri della raccolta ricevono gli aggiornamenti software che vengono definiti nella distribuzione.  

    -   Decidere se aggiungere gli aggiornamenti software a un gruppo di aggiornamento software nuovo o esistente. Nella maggior parte dei casi scegliere di creare un nuovo gruppo di aggiornamento software quando si esegue la regola di distribuzione automatica. Se la regola viene eseguita in una pianificazione più aggressiva, è possibile scegliere di usare un gruppo esistente. Ad esempio, se si esegue la regola ogni giorno per gli aggiornamenti delle definizioni, è possibile aggiungere gli aggiornamenti software a un gruppo di aggiornamento software esistente.  

    -   **Attiva la distribuzione dopo l'esecuzione di questa regola**: specificare se abilitare la distribuzione degli aggiornamenti software dopo l'esecuzione della regola di distribuzione automatica. Per questa impostazione prendere in considerazione le opzioni seguenti:  

        -   Quando si abilita la distribuzione, gli aggiornamenti che soddisfano i criteri definiti per la regola vengono aggiunti a un gruppo di aggiornamento software. Il contenuto dell'aggiornamento software viene scaricato in base alle necessità. Il contenuto viene copiato nei punti di distribuzione specificati e gli aggiornamenti vengono distribuiti ai client nella raccolta di destinazione.  

        -   Quando non si abilita la distribuzione, gli aggiornamenti che soddisfano i criteri definiti per la regola vengono aggiunti a un gruppo di aggiornamento software. Il contenuto della distribuzione dell'aggiornamento software viene scaricato in base alle necessità e distribuito ai punti di distribuzione specificati. Il sito crea una distribuzione disabilitata nel gruppo di aggiornamento software per impedire che gli aggiornamenti vengano distribuiti ai client. Questa opzione garantisce tempo sufficiente per predisporre la distribuzione degli aggiornamenti, verificare che gli aggiornamenti che soddisfano i criteri siano adeguati e, infine, abilitare la distribuzione.  

4.  Nella pagina **Impostazioni distribuzione** configurare le impostazioni seguenti:  

    -   **Usa riattivazione LAN per riattivare i client per le distribuzioni richieste**: specifica se abilitare la riattivazione LAN alla scadenza. La funzione di riattivazione LAN invia pacchetti di riattivazione ai computer che richiedono uno o più aggiornamenti software nella distribuzione. Il sito riattiva tutti i computer in modalità sospensione all'ora di scadenza dell'installazione in modo che l'installazione venga avviata. I client in modalità sospensione che non richiedono aggiornamenti software nella distribuzione non vengono avviati. Per impostazione predefinita, questa impostazione non è abilitata. Prima di usare questa opzione, configurare i computer e le reti per la riattivazione LAN. Per altre informazioni, vedere [Come configurare la riattivazione LAN](../../core/clients/deploy/configure-wake-on-lan.md).  

    -   **Livello dettaglio**: specificare il livello di dettaglio per i messaggi di stato di imposizione di aggiornamento segnalati dai client.  

        > [!IMPORTANT]  
        >  Quando si distribuiscono gli aggiornamenti delle definizioni, impostare il livello di dettaglio su **Solo errori** affinché il client segnali un messaggio di stato solo in caso un aggiornamento delle definizioni non riesca. In caso contrario, il client restituisce un numero elevato di messaggi di stato che potrebbe influire sulle prestazioni del server del sito.  
        
        > [!NOTE]  
        > Il livello di dettaglio **Solo errore** non invia i messaggi di stato di imposizione necessari per il rilevamento delle operazioni di riavvio in sospeso.

    -   **Impostazione condizioni di licenza**: specificare se si desidera distribuire automaticamente gli aggiornamenti software con le condizioni di licenza associate. Alcuni aggiornamenti software includono le condizioni di licenza. Quando si distribuiscono automaticamente gli aggiornamenti software, non vengono visualizzate le condizioni di licenza e non è disponibile un'opzione per accettare tali condizioni. Scegliere di distribuire automaticamente tutti gli aggiornamenti software indipendentemente dalle condizioni di licenza associate o di distribuire solo gli aggiornamenti a cui non sono associate tali condizioni.  

         - Per riesaminare le condizioni di licenza per un aggiornamento software, selezionare l'aggiornamento nel nodo **Tutti gli aggiornamenti software** dell'area di lavoro **Raccolta software**. Nella barra multifunzione fare clic su **Riesamina licenza**.    

         - Per individuare gli aggiornamenti software con le condizioni di licenza associate, aggiungere la colonna **Condizioni di licenza** al riquadro dei risultati nel nodo **Tutti gli aggiornamenti software**. Fare clic sull'intestazione per ordinare la colonna in base agli aggiornamenti software con condizioni di licenza.  

5.  Nella pagina **Aggiornamenti software** configurare i criteri per gli aggiornamenti software recuperati e aggiunti al gruppo di aggiornamento software dalla regola di distribuzione automatica.  

     - Il limite dell'ADR è di 1000 aggiornamenti software.  

     - Se necessario, filtrare le dimensioni del contenuto per gli aggiornamenti software nelle regole di distribuzione automatica. Per altre informazioni, vedere [Configuration Manager and Simplified Windows Servicing on Down Level Operating Systems](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configuration-manager-and-simplified-windows-servicing-on-down/ba-p/274056) (Configuration Manager e manutenzione Windows semplificata su sistemi operativi di livello inferiore).  

     - A partire dalla versione 1910, è possibile usare **Distribuito** come filtro di aggiornamento per le regole di distribuzione automatica. Questo filtro consente di identificare i nuovi aggiornamenti che potrebbero dover essere distribuiti nelle raccolte pilota o di test. Il filtro di aggiornamento software consente anche di evitare la ridistribuzione di aggiornamenti meno recenti. 
         - Quando si usa il filtro **Distribuito**, tenere presente che è possibile che l'aggiornamento sia già stato distribuito in un'altra raccolta, ad esempio una raccolta pilota o di test. <!--4852033-->
     - A partire dalla versione 1806, è disponibile un filtro proprietà per **Architettura**. Usare questo filtro per escludere architetture quali Itanium e ARM64, che sono meno comuni. Tenere presente che esistono applicazioni e componenti a 32 bit (x86) che vengono eseguiti in sistemi a 64 bit (x64). A meno che non si sia certi che x86 non è necessario, abilitare questa funzionalità anche quando si sceglie x64.<!--1322266-->  

    > [!NOTE]  
    > **Windows 10 versione 1903 e successive** è stato aggiunto a Microsoft Update come prodotto a sé stante, anziché all'interno del prodotto **Windows 10** come le versioni precedenti. A causa di questa modifica è necessario eseguire una serie di passaggi manuali per assicurarsi che i client visualizzino questi aggiornamenti. Si è cercato di ridurre il numero di passaggi manuali che è necessario eseguire per il nuovo prodotto in Configuration Manager versione 1906. Per altre informazioni, vedere [Configurazione dei prodotti per le versioni di Windows 10](../get-started/configure-classifications-and-products.md#windows-10-version-1903-and-later) <!--4682946-->


6. Nella pagina **Pianificazione valutazione** specificare se abilitare l'esecuzione della regola di distribuzione automatica in una pianificazione. Quando attivata, fare clic su **Personalizza** per impostare la pianificazione ricorrente.  

    - La configurazione dell'ora di avvio per la pianificazione si basa sull'ora locale del computer su cui è in esecuzione la console di Configuration Manager.  

    - La valutazione dell'ADR può essere eseguita per un massimo di tre volte al giorno.  

    - Non impostare mai la pianificazione per la valutazione con una frequenza superiore alla pianificazione della sincronizzazione degli aggiornamenti software. In questa pagina è visualizzata la pianificazione di sincronizzazione del punto di aggiornamento software che consente di determinare la frequenza della pianificazione per la valutazione.  

    - Per eseguire manualmente la regola di distribuzione automatica, selezionarla nel nodo **Regola di distribuzione automatica** della console e quindi fare clic su **Esegui** nella barra multifunzione.  

    - A partire dalla versione 1802, è possibile pianificare le regole di distribuzione automatica per valutare l'offset rispetto a un giorno di base. Se, ad esempio, il giorno di Patch Tuesday per l'utente cade in realtà di mercoledì, impostare la pianificazione della valutazione per il secondo martedì del mese con l'offset di un giorno.<!--1357133-->  
        - Quando si pianifica la valutazione con un offset durante l'ultima settimana del mese e si sceglie un offset che causa il passaggio al mese successivo, il sito pianifica la valutazione per l'ultimo giorno del mese.<!--506731-->  
        ![Offset rispetto al giorno base della pianificazione di valutazione personalizzata ADR](./media/ADR-evaluation-schedule-offset.PNG)

   
7.  Nella pagina **Pianificazione della distribuzione** configurare le impostazioni seguenti:  

    -   **Pianificazione della valutazione**: specificare l'ora in cui Configuration Manager valuta il tempo disponibile e le scadenze dell'installazione. Scegliere se usare l'ora UTC (Coordinated Universal Time) oppure l'ora locale del computer in cui viene eseguita la console di Configuration Manager.  

          - Quando qui si seleziona **Ora locale client** e quindi **Appena possibile** come opzione di **Tempo disponibile software**, per valutare la disponibilità degli aggiornamenti viene usata l'ora corrente nel computer che esegue la console di Configuration Manager. Questo comportamento è analogo con l'opzione **Scadenza installazione** e l'ora in cui gli aggiornamenti vengono installati in un client. Se il client si trova in un fuso orario diverso, le azioni seguenti vengono eseguite quando l'ora del client corrisponde a quella impostata per la valutazione.  

    -   **Tempo disponibile software**: selezionare una delle seguenti impostazioni per specificare quando gli aggiornamenti software saranno disponibili per i client:  

        -   **Appena possibile**: questa impostazione consente di rendere disponibili prima possibile gli aggiornamenti software nella distribuzione per i client. Quando si crea la distribuzione con questa impostazione selezionata, Configuration Manager aggiorna i criteri client. Al successivo ciclo di polling dei criteri client, ai client viene comunicata la distribuzione e gli aggiornamenti software risultano disponibili per l'installazione.  

        -   **Orario specifico**: rende disponibili gli aggiornamenti software nella distribuzione per i client in una data e a un orario specifici. Quando si crea la distribuzione con questa impostazione attivata, Configuration Manager aggiorna i criteri client. La distribuzione viene comunicata ai client in occasione del successivo ciclo di polling dei criteri client. Gli aggiornamenti del software nella distribuzione non sono però disponibili per l'installazione prima della data e dell'orario configurati.  

    -   **Scadenza installazione**: selezionare una delle impostazioni seguenti per specificare la scadenza per l'installazione degli aggiornamenti software nella distribuzione:  

        -   **Appena possibile**: selezionare questa impostazione per installare automaticamente gli aggiornamenti software nella distribuzione appena possibile.  

        -   **Orario specifico**: selezionare questa impostazione per installare automaticamente gli aggiornamenti software nella distribuzione in una data e a un orario specifici. Configuration Manager determina la scadenza per installare gli aggiornamenti software aggiungendo l'intervallo **Orario specifico** configurato a **Tempo disponibile software**.  

             - L'orario effettivo di scadenza dell'installazione corrisponde all'ora di scadenza visualizzata più una quantità di tempo casuale di massimo due ore. Questo valore casuale riduce il potenziale impatto di un'installazione simultanea degli aggiornamenti nella distribuzione da parte dei client nella raccolta.  

             - Per disabilitare il ritardo della sequenza casuale di installazione per gli aggiornamenti software obbligatori, configurare l'impostazione client **Disabilitare sequenza casuale scadenza** nel gruppo **Agente computer**. Per altre informazioni, vedere le impostazioni client di [Agente computer](../../core/clients/deploy/about-client-settings.md#computer-agent).  

    -  **Ritardare l'imposizione di questa distribuzione in base alle preferenze dell'utente, fino al periodo di tolleranza massimo definito nelle impostazioni del client**: Abilitare questa impostazione per concedere agli utenti più tempo per installare gli aggiornamenti software necessari, oltre la data di scadenza.  

        - Questo comportamento è in genere necessario quando un computer è stato disattivato per molto tempo ed è necessario installare molte applicazioni o aggiornamenti software, come nel caso, ad esempio, di un utente che, tornato da una vacanza, deve attendere parecchio tempo mentre il client installa le distribuzioni scadute.  

        - Configurare il periodo di tolleranza con la proprietà **Periodo di tolleranza per l'imposizione dopo la scadenza della distribuzione (ore)** nelle impostazioni del client. Per altre informazioni, vedere la sezione [Agente computer](../../core/clients/deploy/about-client-settings.md#computer-agent). Tale periodo di tolleranza si applica a tutte le distribuzioni con questa opzione abilitata e destinate a dispositivi in cui è stata distribuita anche l'impostazione del client.  

        - Dopo la scadenza il client installa gli aggiornamenti software nella prima finestra non lavorativa, configurata dall'utente, fino al termine del periodo di tolleranza. L'utente può però aprire comunque Software Center e installare gli aggiornamenti software in qualsiasi momento. Una volta scaduto il periodo di tolleranza, le distribuzioni scadute torneranno al normale comportamento.  

8. Nella pagina **Esperienza utente** è possibile configurare le impostazioni seguenti:  

    -   **Notifiche utente**: specificare se visualizzare la notifica in Software Center nell'orario configurato in **Tempo disponibile software**. Questa impostazione consente di stabilire anche se inviare notifiche agli utenti nei client.  

    -   **Comportamento scadenza**: Specificare i comportamenti da adottare quando la distribuzione dell'aggiornamento software raggiunge la scadenza oltre qualsiasi finestra di manutenzione definita. Le opzioni disponibili consentono di scegliere se installare gli aggiornamenti software ed eseguire un riavvio del sistema dopo l'installazione. Per altre informazioni sulle finestre di manutenzione, vedere [Come usare le finestre di manutenzione](../../core/clients/manage/collections/use-maintenance-windows.md).  
        
        > [!Note]
        > Si applica solo quando la finestra di manutenzione è configurata per il dispositivo client. Se nel dispositivo non è definita una finestra di manutenzione, l'aggiornamento dell'installazione e il riavvio vengono sempre eseguiti dopo la scadenza.

    -   **Comportamento riavvio dispositivo**: Specificare se evitare un riavvio del sistema in server e workstation se è necessario un riavvio del sistema per completare l'installazione dell'aggiornamento.  

        > [!WARNING]  
        >  La disattivazione dei riavvii del sistema può essere utile in ambienti server o quando non si vuole che i computer di destinazione vengano riavviati per impostazione predefinita. Con tale impostazione, però, i computer potrebbero trovarsi in uno stato non protetto. Un riavvio forzato assicura il completamento immediato dell'installazione degli aggiornamenti software.  

    -   **Gestione filtri di scrittura per dispositivi con Windows Embedded**: questa impostazione controlla il comportamento di installazione nei dispositivi con Windows Embedded in cui è abilitato un filtro di scrittura. Scegliere l'opzione per eseguire il commit delle modifiche alla scadenza dell'installazione o durante una finestra di manutenzione. Quando si seleziona questa opzione, è necessario un riavvio e la modifica viene salvata in modo permanente nel dispositivo. In caso contrario, l'aggiornamento viene installato, applicato all'overlay temporaneo e sottoposto a commit successivamente.  

           -  Quando si distribuisce un aggiornamento software in un dispositivo con Windows Embedded, verificare che il dispositivo appartenga a una raccolta che ha una finestra di manutenzione configurata.  

    - **Comportamento di rivalutazione della distribuzione degli aggiornamenti software al riavvio**: selezionare questa impostazione per configurare le distribuzioni degli aggiornamenti software, in modo che i client eseguano un'analisi della conformità degli aggiornamenti software immediatamente dopo l'installazione degli aggiornamenti software e il riavvio. Questa impostazione consente al client di controllare la presenza di aggiornamenti aggiuntivi che diventano applicabili dopo il riavvio e di installarli durante la stessa finestra di manutenzione.  

9. Nella pagina **Avvisi** configurare la modalità di generazione degli avvisi per questa distribuzione in Configuration Manager. Esaminare gli avvisi recenti relativi agli aggiornamenti software nel nodo **Aggiornamenti software** dell'area di lavoro **Raccolta software**. Se si usa anche System Center Operations Manager, configurare i rispettivi avvisi.  

10. Nella pagina **Impostazioni download** configurare le impostazioni seguenti:  

    - Specificare se i client devono scaricare e installare gli aggiornamenti quando usano un punto di distribuzione da un gruppo di limiti vicino o dai gruppi di limiti del sito predefiniti.  

    - Specificare se i clienti devono scaricare e installare gli aggiornamenti da un punto di distribuzione nel gruppo di limiti del sito predefinito quando il contenuto degli aggiornamenti software non è disponibile da un punto di distribuzione nel gruppo di limiti corrente o nei gruppi di limiti vicini.  

    - **Consenti ai client di condividere il contenuto con altri client nella stessa subnet**: specificare se consentire l'uso di BranchCache per i download del contenuto. Per altre informazioni, vedere [BranchCache](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache). A partire dalla versione 1802, BranchCache è sempre abilitato nei client. Questa impostazione è stata rimossa perché i client usano BranchCache se supportato dal punto di distribuzione.  

    - **Se gli aggiornamenti software non sono disponibili nel punto di distribuzione nei gruppi di limiti correnti, vicini o del sito, scaricare il contenuto da Microsoft Update**: selezionare questa impostazione per consentire ai client connessi all'Intranet di scaricare gli aggiornamenti software da Microsoft Update se non sono disponibili nei punti di distribuzione. I client basati su Internet passano sempre a Microsoft Update per il contenuto degli aggiornamenti software.  

    - Specificare se consentire ai client di eseguire il download dopo una scadenza dell'installazione quando usano connessioni Internet a consumo. I provider Internet talvolta applicano un addebito per il traffico dati in entrata e in uscita quando si usa una connessione a consumo.  

    > [!NOTE]  
    >  I client richiedono il percorso del contenuto da un punto di gestione per gli aggiornamenti software in una distribuzione. Il comportamento di download dipende dalla configurazione del punto di distribuzione, del pacchetto di distribuzione e delle impostazioni in questa pagina.   

11. Nella pagina **Pacchetto di distribuzione** selezionare una delle opzioni seguenti:  

    - **Seleziona un pacchetto di distribuzione**: consente di aggiungere questi aggiornamenti a un pacchetto di distribuzione esistente.  

    - **Crea un nuovo pacchetto di distribuzione**: consente di aggiungere questi aggiornamenti a un nuovo pacchetto di distribuzione. Configurare le impostazioni aggiuntive seguenti:  

        -  **Nome**: specificare il nome del pacchetto di distribuzione. Usare un nome univoco che descrive il contenuto del pacchetto. Il nome può contenere un massimo di 50 caratteri.  

        -  **Descrizione**: specificare una descrizione che includa informazioni sul pacchetto di distribuzione. La descrizione facoltativa può contenere un massimo di 127 caratteri.  

        -  **Origine pacchetto**: specifica il percorso dei file di origine dell'aggiornamento software. Digitare un percorso di rete per il percorso di origine, ad esempio `\\server\sharename\path`, oppure fare clic su **Sfoglia** per trovare il percorso di rete. Prima di procedere alla pagina successiva, è necessario creare la cartella condivisa per i file di origine del pacchetto di distribuzione.  

            - Non è possibile usare il percorso specificato come origine di un altro pacchetto di distribuzione software.  

            - È possibile modificare il percorso di origine del pacchetto nelle proprietà del pacchetto di distribuzione dopo che Configuration Manager ha creato il pacchetto di distribuzione. In tal caso, è necessario copiare prima il contenuto dell'origine del pacchetto originale nel nuovo percorso di origine del pacchetto.  

            -  L'account computer del provider SMS e l'utente che esegue la procedura guidata per scaricare gli aggiornamenti software devono disporre entrambi delle autorizzazioni di **Scrittura** per il percorso di download. Limitare l'accesso al percorso di download. Questa restrizione riduce il rischio che utenti malintenzionati possano manomettere i file di origine degli aggiornamenti software.  

        -  **Priorità di invio**: specificare la priorità di invio per il pacchetto di distribuzione. Configuration Manager usa tale priorità quando invia il pacchetto di distribuzione ai punti di distribuzione. I pacchetti di distribuzione vengono inviati in ordine di priorità, ovvero Alta, Media o Bassa. I pacchetti con priorità identiche vengono inviati nell'ordine in cui sono stati creati. Se non esiste alcun backlog, il pacchetto esegue immediatamente l'elaborazione, indipendentemente dalla priorità configurata.  

        - **Abilita replica differenziale binaria**: Abilitare questa impostazione per usare la replica differenziale binaria per il pacchetto di distribuzione. Per altre informazioni, vedere [Replica differenziale binaria](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#binary-differential-replication).  

    - **Nessun pacchetto di distribuzione**: a partire dalla versione 1806, è possibile distribuire gli aggiornamenti software nei dispositivi senza prima scaricare e distribuire il contenuto nei punti di distribuzione. Questa impostazione è utile quando il contenuto degli aggiornamenti è particolarmente esteso. Usarla anche quando si vuole che i client ottengano sempre i contenuti dal servizio cloud Microsoft Update. I client in questo scenario possono anche scaricare il contenuto da peer in cui è già presente il contenuto necessario. Il client Gestione configurazione continua a gestire il download del contenuto, quindi è in grado di usare la funzionalità peer cache di Configuration Manager o altre tecnologie, ad esempio Ottimizzazione recapito. Questa funzionalità supporta qualsiasi tipo di aggiornamento supportato dalla gestione degli aggiornamenti software di Configuration Manager, tra cui gli aggiornamenti di Microsoft 365 Apps.<!--1357933-->  

        > [!Note]  
        > Quando si seleziona questa opzione e si applicano le impostazioni, non è più modificare modificarle. Le altre opzioni sono disattivate.<!--SCCMDocs-pr issue 3003-->  

12. Nella pagina **Punti di distribuzione** specificare i punti di distribuzione o i gruppi di punti di distribuzione che ospiteranno i file di aggiornamento software. Per altre informazioni sui punti di distribuzione, vedere [Configurazioni dei punti di distribuzione](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs). Questa pagina è disponibile solo quando si crea un nuovo pacchetto di distribuzione di aggiornamento software.  
  

13. Nella pagina **Percorso download** specificare se scaricare i file di aggiornamento software da Internet o dalla rete locale. Configurare le seguenti impostazioni:  

    -   **Scarica aggiornamenti software da Internet**: selezionare questa impostazione per scaricare gli aggiornamenti software da un percorso specificato su Internet. Questa opzione è attivata per impostazione predefinita.  

    -   **Scarica aggiornamenti software dal seguente percorso nella rete locale**: selezionare questa impostazione per scaricare gli aggiornamenti software da una cartella condivisa o da una directory locale. Questa impostazione è utile quando il computer che esegue la procedura guidata non dispone di accesso a Internet. I computer con accesso a Internet possono scaricare preventivamente gli aggiornamenti e archiviarli in un percorso nella rete locale accessibile al computer che esegue la procedura guidata. Un altro scenario può verificarsi quando si scarica contenuto pubblicato tramite System Center Updates Publisher o tramite una soluzione di applicazione di patch di terze parti. La condivisione del contenuto WSUS nel punto di aggiornamento software di livello superiore può essere immessa come percorso di rete da cui eseguire il download, ad esempio `\\server\WsusContent`. <!--memdocs-issue-211-->

14. Nella pagina **Selezione lingua** selezionare le lingue per le quali il sito scarica gli aggiornamenti software selezionati. Il sito scarica questi aggiornamenti solo se sono disponibili nelle lingue selezionate. Gli aggiornamenti software non specifici della lingua vengono sempre scaricati. Per impostazione predefinita, la procedura guidata consente di selezionare le lingue configurate nelle proprietà del punto di aggiornamento software. Prima di procedere alla pagina successiva, è necessario selezionare almeno una lingua. Quando si selezionano solo lingue non supportate da un aggiornamento software, il download dell'aggiornamento non riesce.  

15. Nella pagina **Riepilogo** esaminare le impostazioni. Per salvare le impostazioni in un modello di distribuzione, fare clic su **Salva come modello**. Immettere un nome e selezionare le impostazioni che si desidera includere nel modello, quindi fare clic su **Salva**. Per modificare un'impostazione configurata, fare clic sulla pagina della procedura guidata associata e modificare l'impostazione.  

    -  Il nome del modello può essere costituito da caratteri ASCII alfanumerici, nonché da `\` (barra rovesciata) o da `'` (virgoletta singola).  

16. Fare clic su **Avanti** per creare l'ADR.  

Dopo il completamento della procedura guidata viene eseguita la regola di distribuzione automatica. Gli aggiornamenti software che soddisfano i criteri specificati vengono aggiunti a un gruppo di aggiornamento software. L'ADR scarica gli aggiornamenti nella raccolta contenuto del server del sito e li distribuisce ai punti di distribuzione configurati. L'ADR quindi distribuisce il gruppo di aggiornamenti software ai client nella raccolta di destinazione.  



##  <a name="add-a-new-deployment-to-an-existing-adr"></a><a name="BKMK_AddDeploymentToADR"></a> Aggiungere una nuova distribuzione a un'ADR esistente  

Dopo aver creato una regola di distribuzione automatica, aggiungere altre distribuzioni alla regola. Questa azione consente di gestire la complessità della distribuzione di aggiornamenti diversi in raccolte diverse. Ogni nuova distribuzione dispone dell'intera gamma di funzionalità e dell’esperienza di monitoraggio della distribuzione.  


### <a name="process-to-add-a-new-deployment-to-an-existing-adr"></a>Processo per aggiungere una nuova distribuzione a una regola di distribuzione automatica esistente  

1.  Nella console di Configuration Manager passare all'area di lavoro **Raccolta software**, espandere **Aggiornamenti software**, selezionare il nodo **Regole di distribuzione automatica** e quindi selezionare la regola desiderata.  

2.  Nella barra multifunzione fare clic su **Aggiungi distribuzione**.   

3.  Nella pagina **Raccolta** della procedura guidata Aggiungi distribuzione configurare le impostazioni disponibili in modo analogo alla pagina **Generale** della Creazione guidata delle regole di distribuzione automatica. Per altre informazioni, vedere la sezione precedente in [Processo per creare una regola di distribuzione automatica](#bkmk_adr-process). La parte restante della procedura guidata Aggiungi distribuzione include le pagine seguenti, che corrispondono anch'esse alle descrizioni dettagliate precedenti:  

     - Impostazioni di distribuzione
     - Pianificazione della distribuzione
     - Esperienza dell'utente
     - Avvisi
     - Impostazioni di download  

Le distribuzioni possono essere aggiunte anche a livello di codice usando i cmdlet di Windows PowerShell. Per una descrizione completa dell'uso di questo metodo, vedere [New-CMSoftwareUpdateDeployment](/powershell/module/configurationmanager/new-cmsoftwareupdatedeployment).

Per altre informazioni sul processo di distribuzione, vedere [Software update deployment process](../understand/software-updates-introduction.md#BKMK_DeploymentProcess).


## <a name="next-steps"></a>Passaggi successivi
[Monitorare gli aggiornamenti software](monitor-software-updates.md)