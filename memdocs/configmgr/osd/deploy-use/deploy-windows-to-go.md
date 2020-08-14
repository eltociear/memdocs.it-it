---
title: Distribuire Windows to Go
titleSuffix: Configuration Manager
description: Informazioni su come eseguire il provisioning di Windows To Go in Configuration Manager per creare un'area di lavoro Windows To Go avviata da un'unità esterna.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 8eed50f5-80a4-422e-8aa6-a7ccb2171475
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a3cf735dfa2dd73ed39a24c2d674a966acddf05a
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125118"
---
# <a name="deploy-windows-to-go-with-configuration-manager"></a>Distribuire Windows To Go con Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

In questo argomento viene illustrato come eseguire il provisioning di Windows To Go in Configuration Manager. Windows To Go è una funzionalità aziendale di Windows 8 che permette di creare un'area di lavoro di Windows To Go che può essere avviata da un'unità esterna connessa tramite USB nei computer che soddisfano i requisiti di certificato di Windows 7 o Windows 8, indipendentemente dal sistema operativo in esecuzione nel computer. Le aree di lavoro di Windows To Go possono utilizzare la stessa immagine che utilizzano le organizzazioni per i desktop e laptop e possono essere gestite allo stesso modo.  

 Per altre informazioni su Windows To Go, vedere [Windows To Go: panoramica della funzionalità](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/hh831833(v=ws.11)).  

## <a name="provision-windows-to-go"></a>Provisioning di Windows To Go  
 Windows To Go è un sistema operativo archiviato in un'unità esterna con collegamento USB. È possibile eseguire il provisioning dell'unità di Windows To Go esattamente come viene eseguito per le distribuzioni di altri sistemi operativi. Tuttavia, poiché Windows To Go è progettato come soluzione altamente mobile e incentrata sull'utente, è necessario adottare un approccio leggermente diverso al provisioning di queste unità.  

 A un livello elevato, Windows To Go è una distribuzione in due fasi che consente di configurare il contenuto pre-installato e il dispositivo di Windows To Go per la distribuzione del sistema operativo. È possibile ottenere questo risultato con un intervento dell'utente e un tempo di inattività del computer ridotti al minimo. Dopo aver pre-installato il computer, è necessario completare il processo di provisioning per assicurarsi che il computer sia pronto per l'utente. Il processo di provisioning è simile al processo di distribuzione del sistema operativo corrente. Di seguito viene elencato il flusso di lavoro generale che consente di pre-installare il contenuto ed eseguire il provisioning di Windows To Go:  

1.  [Prerequisiti per il provisioning di Windows To Go](#BKMK_Prereqs)  

2.  [Creare supporti pre-installati](#BKMK_CreatePrestagedMedia)  

3.  [Creare un pacchetto Windows To Go Creator](#BKMK_CreatePackage)  

4.  [Aggiornare la sequenza di attività per attivare BitLocker per Windows To Go](#BKMK_UpdateTaskSequence)  

5.  [Distribuire la sequenza di attività e il pacchetto di Windows To Go Creator](#BKMK_Deployments)  

6.  [L'utente esegue Windows To Go Creator](#BKMK_UserExperience)  

7.  [Configuration Manager consente di configurare e preparare l'unità Windows To Go](#BKMK_ConfigureStageDrive)  

8.  [L'utente accede a Windows 8](#BKMK_UserLogsIn)  

###  <a name="prerequisites-to-provision-windows-to-go"></a><a name="BKMK_Prereqs"></a> Prerequisiti per il provisioning di Windows To Go  
 Prima di seguire il provisioning di Windows To Go, è necessario completare le operazioni seguenti in Configuration Manager:  

-   **Distribuire un'immagine di avvio in un punto di distribuzione**  

     prima di creare supporti pre-installati, è necessario distribuire l'immagine di avvio in un punto di distribuzione.  

    > [!NOTE]  
    >  Le immagini di avvio vengono usate per installare il sistema operativo nei computer di destinazione nell'ambiente di Configuration Manager. Queste immagini contengono una versione di Windows PE che installa il sistema operativo e i driver di dispositivo aggiuntivi richiesti. In Configuration Manager sono disponibili due immagini d'avvio: una per il supporto delle piattaforme x86 e una per il supporto delle piattaforme x64. È inoltre possibile creare le proprie immagini di avvio. Per altre informazioni, vedere [Manage boot images](../get-started/manage-boot-images.md) (Gestire le immagini d'avvio).  

-   **Distribuire l'immagine del sistema operativo Windows 8 in un punto di distribuzione**  

     prima di creare supporti pre-installati, è necessario distribuire l'immagine del sistema operativo di Windows 8 in un punto di distribuzione.  

    > [!NOTE]  
    >  Le immagini di sistema operativo sono file con formato .WIM e rappresentano una raccolta compressa di cartelle e file di riferimento necessari per installare e configurare un sistema operativo in un computer. Per altre informazioni, vedere [Manage operating system images](../get-started/manage-operating-system-images.md) (Gestire le immagini del sistema operativo).  

-   **Creare una sequenza attività per distribuire Windows 8**  

     è necessario creare una sequenza attività per una distribuzione di Windows 8 a cui si farà riferimento durante la creazione di supporti pre-installati. Per altre informazioni, vedere [Gestire le sequenze di attività per automatizzare le attività](manage-task-sequences-to-automate-tasks.md).  

###  <a name="create-prestaged-media"></a><a name="BKMK_CreatePrestagedMedia"></a> Creare supporti pre-installati  
 Il supporto pre-installato contiene l'immagine di avvio usata per avviare il computer di destinazione e l'immagine del sistema operativo applicata al computer di destinazione. Il computer di cui viene effettuato il provisioning con i supporti pre-installati può essere avviato con l'immagine di avvio. Il computer è quindi in grado di eseguire quindi una sequenza attività di distribuzione del sistema operativo esistente per installare una distribuzione completa del sistema operativo. La sequenza di attività che distribuisce il sistema operativo non è inclusa nel supporto.  

 È possibile aggiungere contenuto, ad esempio applicazioni e driver di dispositivo, oltre all'immagine del sistema operativo e all'immagine di avvio durante la fase di pre-installazione. Poiché il contenuto è già presente nell'unità, è possibile ridurre il tempo impiegato per distribuire un sistema operativo e il traffico di rete.  

 Utilizzare la seguente procedura per creare supporti pre-installati.  

#### <a name="to-create-prestaged-media"></a>Per creare supporti pre-installati  

1. Nella console di Configuration Manager fare clic su **Raccolta software**.  

2. Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi**, quindi fare clic su **Sequenze attività**.  

3. Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea supporto per sequenza di attività** per avviare la Creazione guidata del supporto per la sequenza di attività.  

4. Nella pagina **Seleziona tipo di supporto** specificare le seguenti informazioni e quindi fare clic su **Avanti**.  

   -   Selezionare **Supporti preinstallati**.  

   -   Selezionare **Consenti distribuzione automatica del sistema operativo** per avviare la distribuzione di Windows To Go senza l'intervento dell'utente.  

       > [!IMPORTANT]  
       >  Quando si utilizza questa opzione con la variabile personalizzata SMSTSPreferredAdvertID (impostata in seguito nel corso di questa procedura), non è necessario l'intervento dell'utente e il computer avvierà automaticamente la distribuzione di Windows To Go quando rileverà l'unità di Windows To Go. Tuttavia, all'utente viene richiesta una password se il supporto è configurato per la protezione con password. Se si utilizza l'impostazione **Consenti distribuzione automatica del sistema operativo** senza configurare la variabile SMSTSPreferredAdvertID, si verificherà un errore durante la distribuzione della sequenza attività.  

5. Nella pagina **Gestione del supporto** specificare le seguenti informazioni e quindi fare clic su **Avanti**.  

   -   Selezionare **Supporto dinamico** se si desidera consentire a un punto di gestione di reindirizzare il supporto a un altro punto di gestione, in base al percorso del client nei limiti del sito.  

   -   Selezionare **Supporto basato su sito** se si desidera che il supporto contatti solo il punto di gestione specificato.  

6. Nella pagina **Proprietà del supporto**  specificare le informazioni seguenti e fare clic su **Avanti**.  

   -   **Creato da**: specificare chi ha creato il supporto.  

   -   **Versione**: specificare il numero di versione del supporto.  

   -   **Commento**: specificare una descrizione univoca dello scopo per cui viene usato il supporto.  

   -   **File supporto**: specificare il nome e il percorso dei file di output. La procedura guidata scrive i file di output in questa posizione. Ad esempio: **\\\nomeserver\cartella\fileoutput.wim**  

7. Nella pagina **Sicurezza** specificare le seguenti informazioni e quindi fare clic su **Avanti**.  

   -   Selezionare **Abilita supporto per computer sconosciuti** per consentire al supporto di distribuire un sistema operativo a un computer non gestito da Configuration Manager. Non sono presenti record di questi computer nel database di Configuration Manager. I computer sconosciuti includono i seguenti:  

       -   Computer in cui non è installato il client di Configuration Manager  

       -   Computer che non sono stati importati in Configuration Manager  

       -   Un computer che non è stato rilevato da Configuration Manager  

   -   Selezionare **Proteggi supporto con password** e immettere una password complessa per proteggere il supporto da accesso non autorizzato. Quando si specifica una password l'utente deve immettere la password per usare il supporto pre-installato.  

       > [!IMPORTANT]  
       >  Come procedura consigliata di sicurezza, assegnare sempre una password per proteggere il supporto pre-installato.  

       > [!NOTE]  
       >  Quando si protegge il supporto pre-installato con una password all'utente viene richiesto di immettere la password anche se il supporto è stato configurato con l'impostazione **Consenti distribuzione automatica del sistema operativo** .  

   -   Per le comunicazioni HTTP, selezionare **Crea certificato del supporto autofirmato**e quindi specificare la data di inizio e di scadenza del certificato.  

   -   Per le comunicazioni HTTPS, selezionare **Importa certificato PKI**e quindi specificare il certificato da importare e la relativa password.  

        Per altre informazioni su questo certificato client usato per le immagini di avvio, vedere [Requisiti dei certificati PKI](../../core/plan-design/network/pki-certificate-requirements.md).  

   -   **Affinità utente dispositivo**: per supportare la gestione basata sugli utenti in Configuration Manager, specificare come si vuole che il supporto associ gli utenti al computer di destinazione. Per altre informazioni su come la distribuzione del sistema operativo supporti l'affinità utente dispositivo, vedere [Associare gli utenti a un computer di destinazione](../get-started/associate-users-with-a-destination-computer.md).  

       -   Specificare **Consenti affinità utente dispositivo con approvazione automatica** se si desidera che il supporto associ automaticamente gli utenti al computer di destinazione. Questa funzionalità si basa sulle azioni della sequenza di attività che distribuisce il sistema operativo. In questo scenario, la sequenza di attività crea una relazione tra gli utenti specificati e il computer di destinazione quando distribuisce il sistema operativo nel computer di destinazione.  

       -   Specificare **Consenti approvazione amministratore in sospeso per affinità utente dispositivo** se si desidera che il supporto associ gli utenti al computer di destinazione dopo la concessione dell'approvazione. Questa funzionalità si basa sull'ambito della sequenza di attività che distribuisce il sistema operativo. In questo scenario, la sequenza di attività crea una relazione tra gli utenti specificati e il computer di destinazione, ma attende l'approvazione di un utente amministratore prima di distribuire il sistema operativo.  

       -   Specificare **Non consentire affinità utente dispositivo** se non si desidera che il supporto associ gli utenti al computer di destinazione. In questo scenario, la sequenza di attività non associa gli utenti al computer di destinazione quando distribuisce il sistema operativo.  

8. Nella pagina **Sequenza attività** specificare la sequenza attività di Windows 8 creata nella sezione precedente.  

9. Nella pagina **Immagine di avvio** specificare le informazioni seguenti e quindi fare clic su **Avanti**.  

    > [!IMPORTANT]  
    >  L'architettura dell'immagine di avvio distribuita deve essere appropriata per l'architettura del computer di destinazione. Ad esempio, un computer di destinazione x64 può avviare ed eseguire un'immagine di avvio x86 o x64. Tuttavia, un computer di destinazione x86 può avviare ed eseguire solo un'immagine di avvio x86. Per i computer certificati Windows 8 in modalità EFI, è necessario utilizzare un'immagine di avvio x64.  

    -   **Immagine d'avvio**: specificare l'immagine di avvio per l'avvio del computer di destinazione.  

    -   **Punto di distribuzione**: specificare il punto di distribuzione che ospita l'immagine di avvio. La procedura guidata consente di recuperare l'immagine di avvio dal punto di distribuzione e di scriverla sul supporto.  

        > [!NOTE]  
        >  L'utente amministratore deve disporre dei diritti di accesso di **Lettura** per il contenuto dell'immagine di avvio nel punto di distribuzione. Per altre informazioni, vedere [Account di accesso al pacchetto](../../core/plan-design/hierarchy/accounts.md#package-access-account).  

    -   Se è stato selezionato **Supporto basato su sito** nella pagina **Gestione del supporto** di questa procedura guidata, nella casella **Punto di gestione** specificare un punto di gestione da un sito primario.  

    -   Se è stato selezionato **Supporto basato su sito** nella pagina **Gestione del supporto** di questa procedura guidata, nella casella **Punto di gestione** specificare un punto di gestione da un sito primario.  

10. Nella pagina **Immagini** specificare le seguenti informazioni e quindi fare clic su **Avanti**.  

    -   **Pacchetto immagine**: specificare il pacchetto che contiene l'immagine del sistema operativo Windows 8.  

    -   **Indice immagine**: specificare l'immagine da distribuire se il pacchetto contiene più immagini del sistema operativo.  

    -   **Punto di distribuzione**: specificare il punto di distribuzione che ospita il pacchetto di immagini del sistema operativo. La procedura guidata recupera l'immagine del sistema operativo dal punto di distribuzione e la scrive sul supporto.  

        > [!NOTE]  
        >  L'utente amministratore deve disporre dei diritti di accesso di **Lettura** per il contenuto dell'immagine del sistema operativo nel punto di distribuzione. Per altre informazioni, vedere [Account di accesso al pacchetto](../../core/plan-design/hierarchy/accounts.md#package-access-account).  

11. Nella pagina **Selezione applicazione** selezionare il contenuto dell'applicazione da includere nel file supporto e quindi fare clic su **Avanti**.  

12. Nella pagina **Seleziona pacchetto** selezionare il contenuto del pacchetto aggiuntivo da includere nel file supporto e quindi fare clic su **Avanti**.  

13. Nella pagina **Selezionare il pacchetto driver** selezionare il contenuto del pacchetto driver da includere nel file supporto e quindi fare clic su **Avanti**.  

14. Nella pagina **Punti di distribuzione** selezionare uno o più punti di distribuzione che includono il contenuto richiesto dalla sequenza attività e quindi fare clic su **Avanti**.  

15. Nella pagina **Personalizzazione** specificare le informazioni seguenti e quindi fare clic su **Avanti**.  

    - **Variabili**: Specificare le variabili usate dalla sequenza di attività per distribuire il sistema operativo. Per Windows To Go, utilizzare la variabile SMSTSPreferredAdvertID per selezionare automaticamente la distribuzione di Windows To Go utilizzando il seguente formato:  

       SMSTSPreferredAdvertID = {*IDDistribuzione*}, dove IDDistribuzione è l'ID distribuzione associato alla sequenza attività che verrà utilizzata dal processo di provisioning per l'unità di Windows To Go.  

      > [!TIP]  
      >  Quando si utilizza questa variabile con una sequenza attività impostata per l'esecuzione automatica (impostazione configurata in precedenza nella procedura), non è necessario l'intervento dell'utente e il computer avvierà automaticamente la distribuzione di Windows To Go quando rileverà l'unità di Windows To Go. Tuttavia, all'utente viene richiesta una password se il supporto è configurato per la protezione con password.  

    - **Comando di preavvio**: Specificare i comandi preavvio da eseguire prima dell'esecuzione della sequenza di attività. I comandi di preavvio possono essere uno script o un eseguibile che possono interagire con l'utente in Windows PE prima che venga eseguita la sequenza attività per l'installazione del sistema operativo. Configurare quanto segue per la distribuzione di Windows To Go:  

      - **OSDBitLockerPIN**: BitLocker per Windows To Go richiede una passphrase. Impostare la variabile di **OSDBitLockerPIN** come parte di un comando di preavvio per l'impostazione della passphrase di BitLocker per l'unità di Windows To Go.  

        > [!WARNING]  
        >  Dopo aver attivato BitLocker per la passphrase, l'utente deve immettere la passphrase a ogni riavvio del computer per l'unità di Windows To Go.  

      - **SMSTSUDAUsers**: Specifica l'utente primario del computer di destinazione. Utilizzare questa variabile per raccogliere il nome utente, che quindi può essere utilizzato per associare l'utente al dispositivo. Per altre informazioni, vedere [Associate users with a destination computer](../get-started/associate-users-with-a-destination-computer.md) (Associare gli utenti a un computer di destinazione).  

        > [!TIP]  
        >  Per recuperare il nome utente, è possibile creare una casella di immissione come parte del comando di preavvio, far immettere all'utente il relativo nome utente e quindi impostare la variabile con il valore. Ad esempio, è possibile aggiungere le seguenti righe al file script del comando di preavvio:  
        >   
        >  `UserID = inputbox("Enter Username" ,"Enter your username:","",400,0)`  
        >   
        >  `env("SMSTSUDAUsers") = UserID`  

        Per altre informazioni su come creare un file script da usare come comando di preavvio, vedere [Prestart commands for task sequence media](../understand/prestart-commands-for-task-sequence-media.md) (Comandi di preavvio del supporto per sequenza attività).  

16. Completare la procedura guidata.  

    > [!NOTE]  
    >  Il completamento del file dei supporti pre-installati da parte della procedura guidata può richiedere un periodo di tempo prolungato.  

###  <a name="create-a-windows-to-go-creator-package"></a><a name="BKMK_CreatePackage"></a> Creare un pacchetto Windows To Go Creator  
 Come parte della distribuzione di Windows To Go, è necessario creare un pacchetto per distribuire il file dei supporti pre-installati. Il pacchetto deve includere lo strumento che consente di configurare l'unità Windows Go e di estrarre il supporto pre-installato sull'unità. Utilizzare la seguente procedura per creare il pacchetto di Windows To Go Creator.  

#### <a name="to-create-the-windows-to-go-creator-package"></a>Per creare il pacchetto di Windows To Go Creator  

1. Nel server che ospiterà i file del pacchetto di Windows To Go Creator, creare una cartella di origine per i file di origine del pacchetto.  

   > [!NOTE]  
   >  L'account computer del server del sito deve disporre dei diritti di accesso in **Lettura** alla cartella di origine.  

2. Copiare il file supporto pre-installato creato nella sezione [Create prestaged media](#BKMK_CreatePrestagedMedia) nella cartella di origine del pacchetto.  

3. Copiare lo strumento Windows To Go Creator (WTGCreator.exe) nella cartella di origine del pacchetto. Lo strumento è disponibile in qualsiasi server del sito primario nel percorso seguente: <*CartellaInstallazioneConfigMgr*>\OSD\Tools\WTG\Creator.  

4. Creare un pacchetto e un programma utilizzando la Creazione guidata pacchetto e programma.  

5. Nella console di Configuration Manager fare clic su **Raccolta software**.  

6. Nell'area di lavoro **Raccolta software** espandere **Gestione applicazioni**, quindi fare clic su **Pacchetti**.  

7. Nella scheda **Home** nel gruppo **Crea** fare clic su **Crea pacchetto**.  

8. Nella pagina **Pacchetto** specificare il nome e la descrizione del pacchetto. Ad esempio, immettere **Windows To Go** per il nome del pacchetto e specificare **Package to configure a Windows To Go drive using Configuration Manager** per la descrizione del pacchetto.  

9. Selezionare **Questo pacchetto contiene file di origine**, specificare il percorso della cartella di origine del pacchetto creato nel passaggio 1, e quindi fare clic su **Avanti**.  

10. Nella pagina **Tipo di programma** selezionare **Programma standard**, quindi fare clic su **Avanti**.  

11. Nella **Programma standard** specificare quanto segue:  

    -   **Nome**: Specificare il nome del programma. Ad esempio, digitare **Creator** per il nome del programma.  

    -   **Riga di comando**: Digitare **WTGCreator.exe /wim:PrestageName.wim**, dove PrestageName è il nome del file pre-installato che è stato creato e copiato nella cartella di origine del pacchetto per il pacchetto di Windows To Go Creator.  

         Facoltativamente, è possibile aggiungere le seguenti opzioni:  

        -   **enableBootRedirect**: opzione della riga di comando per la modifica delle opzioni di avvio di Windows Go per consentire il reindirizzamento di avvio. Quando si utilizza questa opzione, il computer si avvierà da USB senza che sia necessario modificare l'ordine di avvio nel firmware del computer o che l'utente debba selezionare da un elenco di opzioni di avvio durante l'avvio. Se viene rilevata un'unità di Windows To Go, il computer avvia tale unità.  

    -   **Esegui**: Specificare **Normale** per eseguire il programma in base alle impostazioni predefinite del sistema e del programma.  

    -   **Requisiti per esecuzione programma**: specificare se il programma può essere eseguito solo quando un utente è connesso.  

    -   **Modalità esecuzione**: specificare se il programma verrà eseguito con le autorizzazioni degli utenti connessi o con autorizzazioni amministrative. Windows To Go Creator richiede autorizzazioni elevate per l'esecuzione.  

    -   Selezionare **Consenti agli utenti di visualizzare e interagire con l'installazione del programma**, quindi fare clic su **Avanti**.  

12. Nella pagina dei requisiti, specificare quanto segue:  

    - **Requisiti di piattaforma**: selezionare le piattaforme Windows 8 applicabili per consentire il provisioning.  

    - **Spazio su disco stimato**: specificare la dimensione della cartella di origine del pacchetto per Windows To Go Creator.  

    - **Tempo di esecuzione massimo consentito (minuti)** : specifica il tempo massimo che il programma prevede per l'esecuzione nel computer client. Per impostazione predefinita, il valore è impostato su 120 minuti.  

      > [!IMPORTANT]  
      >  Se si utilizzano finestre di manutenzione per la raccolta in cui viene eseguito il programma, è possibile che si verifichi un conflitto se il **Tempo di esecuzione massimo consentito** è superiore alla finestra di manutenzione pianificata. Se il tempo di esecuzione massimo è impostato su **Sconosciuto**, l'avvio avverrà all'interno della finestra di manutenzione, ma l'esecuzione proseguirà fino al completamento oppure non riuscirà se si chiude la finestra di manutenzione. Se si imposta il tempo di esecuzione massimo viene impostato su un periodo specifico (non su Sconosciuto) con durata superiore a quella di tutte le finestre di manutenzione disponibili, il programma non verrà eseguito.  

      > [!NOTE]  
      >  Se il valore è impostato come **sconosciuto**, Configuration Manager imposta un limite massimo di 12 ore (720 minuti).  

      > [!NOTE]  
      >  Se il tempo di esecuzione massimo (sia impostato dall'utente che come valore predefinito) viene superato, Configuration Manager arresta il programma se l'opzione **Esegui con diritti amministrativi** viene selezionata mentre l'opzione **Consenti agli utenti di visualizzare e interagire con l'installazione del programma** non viene selezionata nella pagina **Programma standard**.  

      Fare clic su **Avanti** e completare la procedura guidata.  

###  <a name="update-the-task-sequence-to-enable-bitlocker-for-windows-to-go"></a><a name="BKMK_UpdateTaskSequence"></a> Aggiornare la sequenza di attività per attivare BitLocker per Windows To Go  
 Windows To Go attiva BitLocker in un'unità di avvio esterne senza utilizzare TPM. Pertanto, è necessario utilizzare uno strumento separato per configurare BitLocker nell'unità di Windows To Go. Per attivare BitLocker, è necessario aggiungere un'azione alla sequenza attività dopo il passaggio **Imposta Windows e ConfigMgr** .  

> [!NOTE]  
>  BitLocker per Windows To Go richiede una passphrase. Nel passaggio [Create prestaged media](#BKMK_CreatePrestagedMedia) è possibile impostare la passphrase come parte di un comando di preavvio utilizzando la variabile OSDBitLockerPIN.  

 Utilizzare la seguente procedura per aggiornare la sequenza attività di Windows 8 per attivare BitLocker per Windows To Go.  

#### <a name="to-update-the-windows-8-task-sequence-to-enable-bitlocker"></a>Per aggiornare la sequenza attività di Windows 8 per attivare BitLocker  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** espandere **Gestione applicazioni**, quindi fare clic su **Pacchetti**.  

3.  Nella scheda **Home** nel gruppo **Crea** fare clic su **Crea pacchetto**.  

4.  Nella pagina **Pacchetto** specificare il nome e la descrizione del pacchetto. Ad esempio, digitare **BitLocker for Windows To Go** per il nome del pacchetto e specificare **Package to update BitLocker for Windows To Go** per la descrizione del pacchetto.  

5.  Selezionare **Questo pacchetto contiene file di origine**, specificare il percorso dello strumento di BitLocker per Windows To Go e quindi fare clic su **Avanti**. Lo strumento BitLocker è disponibile in qualsiasi server del sito primario di Configuration Manager nel percorso seguente: <*CartellaInstallazioneConfigMgr*>\OSD\Tools\WTG\BitLocker\  

6.  Nella pagina **Tipo di programma** selezionare **Non creare un programma**.  

7.  Fare clic su **Avanti** e completare la procedura guidata.  

8.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

9. Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi**, quindi fare clic su **Sequenze attività**.  

10. Selezionare la sequenza attività di Windows 8 a cui si fa riferimento nei supporti pre-installati.  

11. Nella scheda **Home** , nel gruppo **Sequenza di attività** , fare clic su **Modifica**.  

12. Fare clic sul passaggio **Imposta Windows e ConfigMgr** , fare clic su **Aggiungi**, quindi su **Generale**e infine su **Esegui riga di comando**. Il passaggio Esegui riga di comando viene aggiunto dopo il passaggio Imposta Windows e ConfigMgr.  

13. Nella scheda **Proprietà** per il passaggio **Esegui riga di comando** aggiungere quanto segue:  

    1.  **Nome**: specificare un nome per la riga di comando, ad esempio **Attiva BitLocker per Windows To Go**.  

    2.  **Riga di comando**: i386\osdbitlocker_wtg.exe /Enable /pwd:< *None&#124;AD*>  

         Parametri:  

        -   /pwd:<None&#124;AD> : specificare la modalità di ripristino della password di BitLocker. Questo parametro è obbligatorio. Utilizzare il parametro /Enable nella riga di comando.  

             Selezionare **AD** per configurare Crittografia unità BitLocker in modo che venga eseguito il backup delle informazioni di ripristino per le unità protette da BitLocker in Servizi di dominio Active Directory (AD DS). Il backup delle password di ripristino per un'unità protetta da BitLocker consente agli utenti amministratori di ripristinare l'unità se questa è bloccata. Ciò garantisce che i dati crittografati appartenenti all'azienda siano sempre accessibili dagli utenti autorizzati. Quando si specifica **None**l'utente ha la responsabilità di conservare una copia della password di ripristino o della chiave di ripristino. Se l'utente perde tali informazioni o non crittografa l'unità prima di lasciare l'azienda, gli utenti amministratori non potranno accedere all'unità.  

        -   /wait:<TRUE&#124;FALSE>: specificare se la sequenza di attività attende il completamento della crittografia per essere completata.  

    3.  Selezionare **Pacchetto**, quindi specificare il pacchetto creato all'inizio di questa procedura.  

    4.  Nella scheda **Opzioni** aggiungere le seguenti condizioni:  

        -   Condizione = Variabile della sequenza attività  

        -   Variabile = _SMSTSWTG  

        -   Condizione = Uguale a  

        -   Valore = True  

    > [!NOTE]  
    >  Il passaggio **Attiva BitLocker** , che è probabile dopo il passaggio della nuova riga di comando, non viene utilizzato per attivare BitLocker per Windows To Go. Tuttavia, è possibile mantenere questo passaggio nella sequenza attività per l'utilizzo con le distribuzioni di Windows 8 che non utilizzano un'unità Windows To Go.  

###  <a name="deploy-the-windows-to-go-creator-package-and-task-sequence"></a><a name="BKMK_Deployments"></a> Distribuire la sequenza di attività e il pacchetto di Windows To Go Creator  
 Windows To Go è un processo di distribuzione ibrida. Pertanto, è necessario distribuire il pacchetto di Windows To Go Creator e la sequenza attività di Windows 8. Utilizzare le seguenti procedure per completare il processo di distribuzione.  

#### <a name="to-deploy-the-windows-to-go-creator-package"></a>Per distribuire il pacchetto di Windows To Go Creator  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** espandere **Gestione applicazioni**, quindi fare clic su **Pacchetti**.  

3.  Selezionare il pacchetto di Windows To Go creato nel passaggio [Creare un pacchetto Windows To Go Creator](#BKMK_CreatePackage) .  

4.  Nella scheda **Home** , nel gruppo **Distribuzione** , fare clic su **Distribuisci**.  

5.  Nella pagina **Generale** specificare le impostazioni seguenti:  

    1.  **Software**: verificare che il pacchetto di Windows To Go sia stato selezionato.  

    2.  **Raccolta**: fare clic su **Sfoglia** per selezionare la raccolta in cui si desidera distribuire il pacchetto di Windows To Go.  

    3.  **Utilizza gruppi di punti di distribuzione predefiniti associati a questa raccolta**: selezionare questa opzione se si vuole archiviare il contenuto del pacchetto nel gruppo di punti di distribuzione predefiniti delle raccolte. Se la raccolta selezionata non è stata associata a un gruppo di punti di distribuzione, l'opzione non sarà disponibile.  

6.  Nella pagina **Contenuto** fare clic su **Aggiungi** e quindi selezionare i punti di distribuzione o i gruppi di punti di distribuzione in cui si desidera distribuire il contenuto associato a questo programma e pacchetto.  

7.  Nella pagina **Impostazioni distribuzione** selezionare **Disponibile** per il tipo di distribuzione e quindi fare clic su **Avanti**.  

8.  Nella **Pianificazione**configurare il momento in cui pacchetto e programma verranno distribuiti o resi disponibili ai dispositivi client.  

     Le opzioni presenti in questa pagina varieranno in base all'impostazione dell'azione di distribuzione, che può essere **Disponibile** o **Richiesto**.  

9. Nella **Pianificazione**configurare le seguenti informazioni e quindi fare clic su **Avanti**.  

    1.  **Pianifica quando questa distribuzione diventerà disponibile**: specificare la data e l'ora in cui pacchetto e programma saranno disponibili per l'esecuzione nel computer di destinazione. Quando si seleziona **UTC**questa impostazione assicura che pacchetto e programma siano disponibile per più computer di destinazione contemporaneamente anziché in momenti diversi, in base all'ora locale dei computer di destinazione.  

    2.  **Pianifica alla scadenza di questa distribuzione**: specificare la data e l'ora di scadenza di pacchetto e programma nel computer di destinazione. Quando si seleziona **UTC**, questa impostazione assicura che la sequenza attività scada in più computer di destinazione contemporaneamente anziché in momenti diversi, in base all'ora locale dei computer di destinazione.  

10. Nella pagina **Esperienza utente** della procedura guidata specificare le seguenti informazioni:  

    -   **Installazione software**: consente l'installazione del software al di fuori di tutte le finestre di manutenzione configurate.  

    -   **Riavvio del sistema (se necessario per completare l'installazione)** : consente il riavvio di un dispositivo al di fuori di una finestra di manutenzione configurata quando è necessario per l'installazione del software.  

    -   **Dispositivi integrati**: quando si distribuiscono pacchetti e programmi in dispositivi con Windows Embedded abilitati per i filtri di scrittura, è possibile specificare di installare i pacchetti e programmi nella sovrapposizione temporanea e confermare le modifiche in seguito oppure confermarle alla scadenza dell'installazione o all'interno di una finestra di manutenzione. Quando si confermano le modifiche alla scadenza dell'installazione o all'interno di una finestra di manutenzione, è necessario il riavvio per mantenere le modifiche nel dispositivo.  

11. Nella pagina **Punti di distribuzione** specificare le informazioni seguenti:  

    -   **Opzioni di distribuzione**: specificare **Scarica il contenuto dal punto di distribuzione ed esegui in locale**.  

    -   **Consenti ai client di condividere il contenuto con altri client nella stessa subnet**: selezionare questa opzione per ridurre il carico sulla rete, consentendo ai client di scaricare contenuto da altri client della rete che lo hanno già scaricato e memorizzato nella cache. Questa opzione utilizza Windows BranchCache e può essere utilizzata in computer che eseguono Windows Vista SP2 e versioni successive.  

    -   **Consenti ai client di utilizzare un percorso origine di fallback per il contenuto**: specificare se consentire ai client di eseguire il fallback e usare un punto di distribuzione non preferito come percorso di origine del contenuto quando il contenuto non è disponibile presso un punto di distribuzione preferito.  

12. Completare la procedura guidata.  

#### <a name="to-deploy-the-windows-8-task-sequence"></a>Per distribuire la sequenza attività per Windows 8  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi**, quindi fare clic su **Sequenze attività**.  

3.  Selezionare la sequenza di attività di Windows 8 creata al passaggio [Prerequisites to provision Windows To Go](#BKMK_Prereqs) .  

4.  Nella scheda **Home** , nel gruppo **Distribuzione** , fare clic su **Distribuisci**.  

5.  Nella pagina **Generale** specificare le impostazioni seguenti:  

    1.  **Sequenza di attività**: verificare che sia selezionata la sequenza di attività per Windows 8.  

    2.  **Raccolta**: fare clic su **Sfoglia** per selezionare la raccolta che include tutti i dispositivi per i quali un utente potrebbe eseguire il provisioning di Windows To Go.  

        > [!IMPORTANT]  
        >  Se il supporto preinstallato creato nella sezione [Creare supporti pre-installati](#BKMK_CreatePrestagedMedia) utilizza la variabile SMSTSPreferredAdvertID, è possibile distribuire la sequenza attività nella raccolta **Tutti i sistemi** e specificare l'impostazione **Solo Windows PE (nascosto)** nella pagina **Contenuto** . Poiché la sequenza attività è nascosta, sarà disponibile solo per il supporto.  

    3.  **Utilizza gruppi di punti di distribuzione predefiniti associati a questa raccolta**: selezionare questa opzione se si vuole archiviare il contenuto del pacchetto nel gruppo di punti di distribuzione predefiniti delle raccolte. Se la raccolta selezionata non è stata associata a un gruppo di punti di distribuzione, l'opzione non sarà disponibile.  

6.  Nella pagina **Impostazioni distribuzione** configurare le impostazioni seguenti e quindi fare clic su **Avanti**.  

    -   **Scopo**: selezionare **Disponibile**. Quando si distribuisce la sequenza attività a un utente, l'utente la vede pubblicata nel Catalogo applicazioni e può richiederla all'occorrenza. Se si distribuisce la sequenza attività in un dispositivo, l'utente la vede nel Software Center e può installarla all'occorrenza.  

    -   **Rendi disponibile per**: specificare se la sequenza di attività è disponibile per i client di Configuration Manager, i supporti o PXE.  

        > [!IMPORTANT]  
        >  Usare l'impostazione **Solo supporti e PXE (nascosto)** per le distribuzioni sequenza di attività automatiche. Selezionare **Consenti distribuzione automatica del sistema operativo** e impostare la variabile SMSTSPreferredAdvertID come parte del supporto preinstallato affinché il computer venga avviato automaticamente con la distribuzione Windows To Go senza alcuna interazione da parte dell'utente in presenza di un'unità Windows To Go. Per ulteriori informazioni sulle impostazioni relative ai supporti preinstallati, vedere la sezione [Create prestaged media](#BKMK_CreatePrestagedMedia) .  

7.  Nella pagina **Pianificazione** configurare le informazioni seguenti e quindi fare clic su **Avanti**.  

    1.  **Pianifica quando questa distribuzione diventerà disponibile**: specificare la data e l'ora in cui la sequenza di attività è disponibile per l'esecuzione nel computer di destinazione. Quando si seleziona **UTC**, questa impostazione assicura che la sequenza attività sia disponibile per più computer di destinazione contemporaneamente anziché in momenti diversi, in base all'ora locale dei computer di destinazione.  

    2.  **Pianifica alla scadenza di questa distribuzione**: specificare la data e l'ora di scadenza della sequenza di attività nel computer di destinazione. Quando si seleziona **UTC**, questa impostazione assicura che la sequenza attività scada in più computer di destinazione contemporaneamente anziché in momenti diversi, in base all'ora locale dei computer di destinazione.  

8.  Nella pagina **Esperienza utente** specificare le informazioni seguenti:  

    -   **Mostra stato sequenza di attività**: specificare se il client di Configuration Manager visualizza lo stato di avanzamento della sequenza di attività.  

    -   **Installazione software**: specificare se l'utente è autorizzato a installare il software al di fuori di una finestra di manutenzione configurata dopo l'orario pianificato.  

    -   **Riavvio del sistema (se necessario per completare l'installazione)** : consente il riavvio di un dispositivo al di fuori di una finestra di manutenzione configurata quando è necessario per l'installazione del software.  

    -   **Dispositivi integrati**: quando si distribuiscono pacchetti e programmi in dispositivi con Windows Embedded abilitati per i filtri di scrittura, è possibile specificare di installare i pacchetti e programmi nella sovrapposizione temporanea e confermare le modifiche in seguito oppure confermarle alla scadenza dell'installazione o all'interno di una finestra di manutenzione. Quando si confermano le modifiche alla scadenza dell'installazione o all'interno di una finestra di manutenzione, è necessario il riavvio per mantenere le modifiche nel dispositivo.  

    -   **Client basati su Internet**: specificare se la sequenza attività può essere eseguita in un client basato su Internet. Le operazioni di installazione di software, quale un sistema operativo, non sono supportate con questa impostazione. Usare questa opzione solo per le sequenze attività generiche basate su script che eseguono operazioni nel sistema operativo standard.  

9. Nella pagina **Avvisi** specificare le impostazioni di avviso desiderate per la distribuzione di questa sequenza di attività e quindi fare clic su **Avanti**.  

10. Nella pagina **Punti di distribuzione** specificare le informazioni seguenti e quindi fare clic su **Avanti**.  

    -   **Opzioni di distribuzione**: selezionare **Scaricare il contenuto localmente quando necessario eseguendo la sequenza attività**.  

    -   **Usare un punto di distribuzione remoto quando non sono disponibili punti di distribuzione locali**: specificare se i client possono scaricare il contenuto necessario per la sequenza di attività da punti di distribuzione disponibili in reti lente e inaffidabili.  

    -   **Consenti ai client di utilizzare un percorso origine di fallback per il contenuto**:
        - *Nelle versioni precedenti alla 1610* è possibile selezionare la casella di controllo Consenti percorso origine di fallback per il contenuto per consentire ai client esterni a questi gruppi di limiti di eseguire il fallback e usare il punto di distribuzione come percorso di origine per il contenuto in assenza di altri punti di distribuzione disponibili.
        - *A partire dalla versione 1610* non è più possibile configurare **Consenti percorso origine di fallback per il contenuto**.  È invece possibile configurare relazioni tra gruppi di limiti per determinare quando un client può iniziare la ricerca di gruppi di limiti aggiuntivi per un percorso di origine del contenuto valido. 

11. Completare la procedura guidata.  

###  <a name="user-runs-the-windows-to-go-creator"></a><a name="BKMK_UserExperience"></a> L'utente esegue Windows To Go Creator  
 Dopo la distribuzione del pacchetto Windows To Go e della sequenza attività per Windows 8, Windows To Go Creator sarà disponibile all'utente. L'utente può accedere al catalogo del software (o al Software Center, se Windows To Go Creator è stato distribuito nei dispositivi) ed eseguire il programma Windows To Go Creator. Al termine del download del pacchetto di Creator, viene visualizzata un'icona lampeggiante sulla barra delle applicazioni. Quando l'utente fa clic sull'icona, viene visualizzata una finestra di dialogo in cui è possibile selezionare l'unità Windows To Go di cui eseguire il provisioning (a meno che non venga utilizzata l'opzione della riga di comando /drive). Se l'unità non soddisfa i requisiti per Windows To Go o se l'unità non dispone di spazio sufficiente per l'installazione dell'immagine, verrà visualizzato un messaggio di errore. Nella pagina di conferma l'utente può verificare l'unità e l'immagine che verranno applicate. Durante la configurazione e la pre-installazione del contenuto nell'unità Windows To Go, viene visualizzata una finestra di dialogo di avanzamento. Al termine della pre-installazione, viene chiesto di riavviare il computer dall'unità Windows To Go.  

> [!NOTE]  
>  Se nella sezione [Creare un pacchetto Windows To Go Creator](#BKMK_CreatePackage) non è stato abilitato il reindirizzamento dell'avvio nella riga di comando del programma di creazione nella sezione, è possibile che l'utente debba eseguire manualmente l'avvio dall'unità Windows To Go ad ogni riavvio del sistema.  

###  <a name="configuration-manager-configures-and-stages-the-windows-to-go-drive"></a><a name="BKMK_ConfigureStageDrive"></a> Configuration Manager consente di configurare e preparare l'unità Windows To Go  
 Quando il computer viene riavviato dall'unità Windows To Go, l'unità esegue il riavvio in Windows PE ed esegue la connessione al punto di gestione per ottenere i criteri necessari per il completamento della distribuzione del sistema operativo. Configuration Manager configura e prepara l'unità Windows To Go. Quando Configuration Manager completa la preparazione dell'unità, l'utente può riavviare il computer per finalizzare il processo di provisioning, ad esempio mediante l'unione a un dominio o l'installazione di applicazioni. Questo processo è lo stesso per tutti i supporti preinstallati.  

###  <a name="user-logs-in-to-windows-8"></a><a name="BKMK_UserLogsIn"></a> L'utente accede a Windows 8  
 Quando Configuration Manager completa il processo di provisioning e viene visualizzata la schermata di blocco di Windows 8, l'utente può eseguire l'accesso al sistema operativo.  
