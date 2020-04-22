1.  Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software** e selezionare il nodo **Aggiornamenti software**.  

2.  Scegliere l'aggiornamento software da scaricare usando uno dei seguenti metodi:  

    -   Selezionare uno o più gruppi di aggiornamento software dal nodo **Gruppi di aggiornamenti software**. Quindi fare clic su **Scarica** nella barra multifunzione.  

    -   Selezionare uno o più aggiornamenti software dal nodo **Tutti gli aggiornamenti software**. Quindi fare clic su **Scarica** nella barra multifunzione.  

        > [!NOTE]  
        >  Nel nodo **Tutti gli aggiornamenti software** Configuration Manager visualizza solo gli aggiornamenti software con classificazione **Critico** e **Sicurezza** rilasciati negli ultimi 30 giorni.  

        > [!TIP]  
        >  Fare clic su **Aggiungi criterio** per filtrare gli aggiornamenti software visualizzati nel nodo **Tutti gli aggiornamenti Software**. Salvare i criteri di ricerca usati con maggiore frequenza e quindi gestire le ricerche salvate nella scheda **Ricerca**.  


3.  Nella pagina **Pacchetto di distribuzione** della procedura Download guidato degli aggiornamenti software, configurare le impostazioni seguenti:  

    -  **Seleziona pacchetto di distribuzione**: scegliere questa impostazione per selezionare un pacchetto di distribuzione esistente per gli aggiornamenti software nella distribuzione.  

        > [!NOTE]  
        >  Gli aggiornamenti software già scaricati dal sito nel pacchetto di distribuzione selezionato non verranno scaricati nuovamente.  

    -  **Creare un nuovo pacchetto di distribuzione**: selezionare questa impostazione per creare un nuovo pacchetto di distribuzione per gli aggiornamenti software nella distribuzione. Configurare le seguenti impostazioni:  

        -   **Nome**: specifica il nome del pacchetto di distribuzione. Il pacchetto deve avere un nome univoco che descrive brevemente il contenuto del pacchetto. Il nome può contenere un massimo di 50 caratteri.  

        -   **Descrizione**: specificare una descrizione che fornisca informazioni sul pacchetto di distribuzione. La descrizione facoltativa può contenere un massimo di 127 caratteri.    

        -   **Origine pacchetto**: specifica il percorso dei file di origine dell'aggiornamento software. Digitare un percorso di rete per il percorso di origine, ad esempio `\\server\sharename\path`, oppure fare clic su **Sfoglia** per trovare il percorso di rete. Prima di procedere alla pagina successiva, è necessario creare la cartella condivisa per i file di origine del pacchetto di distribuzione.  

             - Non è possibile usare il percorso specificato come origine di un altro pacchetto di distribuzione software.  

             - È possibile modificare il percorso di origine del pacchetto nelle proprietà del pacchetto di distribuzione dopo che Configuration Manager ha creato il pacchetto di distribuzione. In tal caso, è necessario copiare prima il contenuto dell'origine del pacchetto originale nel nuovo percorso di origine del pacchetto.  

             -  L'account computer del provider SMS e l'utente che esegue la procedura guidata per scaricare gli aggiornamenti software devono disporre entrambi delle autorizzazioni di **Scrittura** per il percorso di download. Limitare l'accesso al percorso di download. Questa restrizione riduce il rischio che utenti malintenzionati possano manomettere i file di origine degli aggiornamenti software.  

        - **Abilita la replica differenziale binaria**: abilitare questa impostazione per ridurre al minimo il traffico di rete tra i siti. La replica differenziale binaria aggiorna soltanto il contenuto del pacchetto che è stato modificato e non l'intero contenuto. Per altre informazioni, vedere [Replica differenziale binaria](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#binary-differential-replication).  

4.  Nella pagina **Punti di distribuzione** specificare i punti di distribuzione o i gruppi di punti di distribuzione che ospiteranno i file di aggiornamento software. Per altre informazioni sui punti di distribuzione, vedere [Configurazioni dei punti di distribuzione](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs). Questa pagina è disponibile solo quando si crea un nuovo pacchetto di distribuzione di aggiornamento software.  

5.  La pagina **Punti di distribuzione** è disponibile soltanto quando si crea un nuovo pacchetto di distribuzione degli aggiornamenti software. Specificare le impostazioni seguenti:  

    -   **Priorità di distribuzione**: usare questa impostazione per specificare la priorità di distribuzione per il pacchetto di distribuzione. La priorità di distribuzione si applica quando il pacchetto di distribuzione viene inviato ai punti di distribuzione nei siti figlio. I pacchetti di distribuzione vengono inviati in ordine di priorità, ovvero Alta, Media o Bassa. I pacchetti con priorità identiche vengono inviati nell'ordine in cui sono stati creati. Se non esiste alcun backlog, il pacchetto viene elaborato subito, indipendentemente dalla priorità. Per impostazione predefinita, il sito invia i pacchetti con priorità **Media**.  

    -   **Abilita per la distribuzione su richiesta**: usare questa impostazione per abilitare la distribuzione del contenuto su richiesta ai punti di distribuzione configurati per questa funzionalità e nel gruppo di limiti corrente del client. Quando questa impostazione è abilitata, il punto di gestione crea un trigger affinché il servizio di gestione della distribuzione distribuisca il contenuto a tutti i punti di distribuzione quando un client richiede il contenuto del pacchetto e questo non è disponibile. Per altre informazioni, vedere [Distribuzione di contenuto su richiesta](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#on-demand-content-distribution).  

    -   **Impostazioni punto di distribuzione pre-installazione**: usare questa impostazione per specificare come si desidera distribuire il contenuto nei punti di distribuzione pre-installati. Scegliere una delle seguenti opzioni:  

        -   **Scarica automaticamente il contenuto quando i pacchetti sono assegnati ai punti di distribuzione**: usare questa impostazione per ignorare le impostazioni di pre-installazione e distribuire il contenuto nel punto di distribuzione.   

        -   **Scarica solo le modifiche di contenuto nel punto di distribuzione**: usare questa impostazione per pre-installare il contenuto iniziale nel punto di distribuzione, quindi distribuire le modifiche di contenuto nel punto di distribuzione.  

        -   **Copia manualmente il contenuto del pacchetto nel punto di distribuzione**: usare questa impostazione per pre-installare sempre il contenuto nel punto di distribuzione. Questa opzione corrisponde all'impostazione predefinita.  

        Per altre informazioni sulla pre-installazione di contenuto nei punti di distribuzione, vedere [Use Prestaged content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage) (Usare contenuti in versione di preproduzione).  


6.  Nella pagina **Percorso download** specificare il percorso usato da Configuration Manager per scaricare i file di origine degli aggiornamenti software. Usare uno dei seguenti metodi:  

    -   **Scarica aggiornamenti software da Internet**: selezionare questa impostazione per scaricare gli aggiornamenti software dal percorso su Internet. Questa opzione corrisponde all'impostazione predefinita.  

    -   **Scaricare gli aggiornamenti software da un percorso di rete**: selezionare questa impostazione per scaricare gli aggiornamenti software da una directory locale o da una cartella condivisa. Questa impostazione è utile quando il computer che esegue la procedura guidata non dispone di accesso a Internet. I computer con accesso a Internet possono scaricare preventivamente gli aggiornamenti e archiviarli in un percorso nella rete locale accessibile al computer che esegue la procedura guidata.  


7.  Nella pagina **Selezione lingua** selezionare le lingue per le quali il sito scarica gli aggiornamenti software selezionati. Il sito scarica questi aggiornamenti solo se sono disponibili nelle lingue selezionate. Gli aggiornamenti software non specifici della lingua vengono sempre scaricati. Per impostazione predefinita, la procedura guidata consente di selezionare le lingue configurate nelle proprietà del punto di aggiornamento software. Prima di procedere alla pagina successiva, è necessario selezionare almeno una lingua. Quando si selezionano solo lingue non supportate da un aggiornamento, il download dell'aggiornamento non riesce.  

8. Nella pagina **Riepilogo** verificare le impostazioni selezionate nella procedura guidata e fare clic su **Avanti** per scaricare gli aggiornamenti software.  

9. Nella pagina **Completamento** verificare che gli aggiornamenti software siano stati scaricati correttamente e fare clic su **Chiudi**.  
