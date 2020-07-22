---
title: Creare applicazioni
titleSuffix: Configuration Manager
description: Creare applicazioni con tipi di distribuzione, metodi di rilevamento e requisiti per installare software.
ms.date: 07/10/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 60ca31b73e31ea59b7a854f87262be7fdc4ab5c5
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240338"
---
# <a name="create-applications-in-configuration-manager"></a>Creare applicazioni in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Un'applicazione Configuration Manager definisce i metadati relativi all'applicazione. Un'applicazione ha uno o più tipi di distribuzione, che includono i file di installazione e le informazioni necessarie per installare il software nei dispositivi. Un tipo di distribuzione include anche regole, ad esempio i metodi di rilevamento e i requisiti. Queste regole specificano quando e come il client installa il software.  

Creare applicazioni usando i metodi seguenti:  

- Creare automaticamente un'applicazione e i tipi di distribuzione leggendo i file di installazione dell'applicazione:  
  - [Creare un'applicazione](#bkmk_create) e [rilevare automaticamente](#bkmk_auto-app) le informazioni sull'applicazione
  - [Creare un tipo di distribuzione](#bkmk_create-dt) e [identificare automaticamente](#bkmk_auto-dt) le informazioni sul tipo di distribuzione

- Creare manualmente un'applicazione e quindi aggiungere tipi di distribuzione in un secondo momento:  
  - [Creare un'applicazione](#bkmk_create) e [specificare manualmente](#bkmk_manual-app) le informazioni sull'applicazione
  - [Creare un tipo di distribuzione](#bkmk_create-dt) e [specificare manualmente](#bkmk_manual-dt) le informazioni sul tipo di distribuzione

- [Importare un'applicazione](#bkmk_import) da un file  

Questo articolo include anche le informazioni seguenti per configurare un tipo di distribuzione:  

- [Contenuto](#bkmk_dt-content)
- [Sequenza di attività](#bkmk_dt-ts)
- [Metodo di rilevamento](#bkmk_dt-detect)
- [Esperienza utente](#bkmk_dt-ux)
- [Requirements](#bkmk_dt-require)
- [Codici restituiti](#bkmk_dt-return)
- [Dipendenze](#bkmk_dt-depend)

## <a name="create-an-application"></a><a name="bkmk_create"></a> Creare un'applicazione  

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**, espandere **Gestione applicazioni** e selezionare il nodo **Applicazioni**.  

2. Nella scheda **Home** della barra multifunzione nel gruppo **Crea** selezionare **Crea applicazione**.  

Rilevare quindi automaticamente o specificare manualmente le informazioni sull'applicazione:  

- [Rilevare automaticamente](#bkmk_auto-app) le informazioni relative alle applicazioni per creare un'applicazione di base con un tipo di distribuzione singolo, ad esempio un file di Windows Installer privo di dipendenze o requisiti. Dopo avere creato un'applicazione seguendo questa procedura, modificarla in base alla necessità. È possibile aggiungere o modificare i tipi di distribuzione e aggiungere metodi di rilevamento, dipendenze o requisiti.  

- [Specificare manualmente](#bkmk_manual-app) le informazioni sull'applicazione per creare applicazioni più complesse. È possibile definire più di un tipo di distribuzione, dipendenza, metodo di rilevamento o requisito.  

### <a name="automatically-detect-application-information"></a><a name="bkmk_auto-app"></a> Rilevare automaticamente le informazioni sull'applicazione  

1. Nella pagina **Generale** della Creazione guidata applicazione selezionare **Rileva automaticamente le informazioni sull'applicazione dai file di installazione**.  

2. Dall'elenco a discesa **Tipo** , scegliere il tipo di file di installazione dell'applicazione che si desidera usare per rilevare le informazioni sull'applicazione. Per altre informazioni sui tipi di installazione disponibili, vedere [Tipi di distribuzione supportati da Configuration Manager](create-applications.md#bkmk_deploy-types).  

3. Nella casella **Posizione** specificare di file di installazione dell'applicazione da usare per rilevare le informazioni sull'applicazione. Questa posizione è un percorso di rete (`\\server\share\filename`) o un collegamento all'archivio. È necessario avere accesso al percorso di rete e alle eventuali sottocartelle che includono contenuto dell'applicazione.  

    > [!IMPORTANT]  
    > Quando si seleziona **Windows Installer (file \*.msi)** come tipo di applicazione, il sito importa tutti i file nella cartella specificata. I file vengono quindi inviati a punti di distribuzione. Assicurarsi che la cartella specificata contenga solo i file necessari per installare l'applicazione. Microsoft testa Configuration Manager in modo che siano supportati fino a 20.000 file nel pacchetto dell'applicazione. Se l'applicazione contiene più file, è consigliabile creare più applicazioni con meno file.  

4. Nella pagina **Importa informazioni** della Creazione guidata applicazione verificare le informazioni e quindi selezionare **Avanti**. Se necessario, selezionare **Indietro** per tornare indietro e correggere eventuali errori.  

5. Nella pagina **Informazioni generali** della Creazione guidata applicazione specificare le informazioni seguenti:  

    > [!NOTE]  
    > Se Configuration Manager rileva automaticamente queste informazioni dai file di installazione dell'applicazione, significa che sono già presenti. Inoltre, le opzioni visualizzate potrebbero essere diverse a seconda del tipo di applicazione creata.  

    - Informazioni generali sull'applicazione, ad esempio **Nome**, **Commenti amministratore**, **Autore** e **Versione del software** dell'applicazione. Per facilitare la ricerca dell'applicazione nella console di Configuration Manager, specificare un **Riferimento facoltativo** oppure selezionare **Categorie amministrative**.  

    - **Programma di installazione**: Specificare il programma di installazione e le eventuali proprietà necessarie per installare il tipo di distribuzione delle applicazioni.  

        > [!TIP]  
        > Se il programma di installazione non viene visualizzato, scegliere **Sfoglia** e selezionare il percorso del programma di installazione.  

    - **Comportamento di installazione**: selezionare una delle tre opzioni disponibili per la modalità di installazione di questo tipo di distribuzione da parte di Configuration Manager. Per altre informazioni su queste opzioni, vedere [Esperienza utente](#bkmk_dt-ux).  

    - **Usa una connessione VPN automatica (se configurata)** : se è stato distribuito un profilo VPN nel dispositivo in cui l'utente avvia l'app, connettersi alla VPN all'avvio dell'app. Questa opzione è disponibile solo per Windows 8.1 e Windows Phone 8.1. Le connessioni VPN non sono supportate nei dispositivi Windows Phone 8.1 se si distribuisce più di un profilo VPN nel dispositivo. Per altre informazioni, vedere [Profili VPN](../../protect/deploy-use/vpn-profiles.md).  

    - **Effettua il provisioning di questa applicazione per tutti gli utenti nel dispositivo**<!--1358310-->: Eseguire il provisioning di un'applicazione con un pacchetto di app Windows per tutti gli utenti nel dispositivo. Per altre informazioni, vedere [Creare applicazioni Windows](../get-started/creating-windows-applications.md#bkmk_provision).  

       > [!Tip]  
       > Se si modifica un'applicazione esistente, questa impostazione è disponibile nella scheda **Esperienza utente** delle proprietà del tipo di distribuzione del pacchetto app Windows.  

6. Scegliere **Avanti**, riesaminare le informazioni sull'applicazione nella pagina **Riepilogo** e quindi terminare la Creazione guidata applicazione.  

La nuova applicazione viene ora visualizzata nel nodo **Applicazioni** della console di Configuration Manager. La creazione di un'applicazione è stata completata.

Per aggiungere altri tipi di distribuzione o configurare altre impostazioni, vedere [Creare tipi di distribuzione per l'applicazione](#bkmk_create-dt).  

### <a name="manually-specify-application-information"></a><a name="bkmk_manual-app"></a> Specificare manualmente le informazioni sull'applicazione  

1. Nella pagina **Generale** della Creazione guidata applicazione, selezionare **Specifica manualmente le informazioni dell'applicazione** e quindi scegliere **Avanti**.  

2. Specificare **Informazioni generali** sull'applicazione:  

    - Il **Nome** dell'applicazione è obbligatorio e non può contenere più di 256 caratteri.  

    - **Commenti amministratore**, **Autore** e **Versione del software** sono metadati aggiuntivi per descrivere in modo più dettagliato l'applicazione.  

    - Per facilitare la ricerca dell'applicazione nella console di Configuration Manager, specificare un **Riferimento facoltativo** oppure selezionare **Categorie amministrative**.  

    - **Data di pubblicazione**  

    - Selezionare gli utenti o i gruppi responsabili per questa applicazione come **Proprietari** e **Contatti supporto**. Per impostazione predefinita, questi valori sono impostati sul nome dell'utente.  

3. Nella pagina **Software Center** della Creazione guidata applicazione specificare le informazioni seguenti:  

    > [!Note]  
    > Nella versione 1902 e in quelle precedenti questa pagina è denominata **Catalogo applicazioni**.

    - **Lingua selezionata**: dall'elenco a discesa, selezionare la versione della lingua dell'applicazione che si vuole configurare. Scegliere **Aggiungi/Rimuovi** per configurare più lingue per l'applicazione.  

    - **Nome dell'applicazione localizzata**: specificare il nome dell'applicazione nella lingua selezionata.  

        > [!IMPORTANT]  
        > Un nome dell'applicazione localizzata è necessario per ogni versione configurata per le diverse lingue.  

    - **Categorie utente**: scegliere **Modifica** per specificare le categorie dell'applicazione nella lingua selezionata. Gli utenti di Software Center usano queste categorie per filtrare e ordinare le applicazioni.  

        > [!Note]  
        > Nella versione 1902 e in quelle precedenti, le categorie utente sono valide solo per le distribuzioni disponibili nelle raccolte utenti. Se un'applicazione viene distribuita a una raccolta di computer, le categorie utente vengono ignorate.
        >
        > A partire dalla versione 1906, le categorie utente per le distribuzioni di applicazioni destinate a dispositivi vengono visualizzate come filtri in Software Center. Queste distribuzioni possono essere disponibili o obbligatorie.
        >
        > <!-- 4726793 -->La ridenominazione o l'eliminazione di una categoria non viene applicata automaticamente alle app con questa categoria. Queste modifiche vengono applicate alla versione successiva dell'app. Per risolvere questo problema per la ridenominazione o l'eliminazione:
        >
        > - Prima di tutto, deselezionare la casella di controllo accanto alla categoria in tutte le app che vi fanno riferimento. Quindi applicare la modifica, che consente di esaminare l'app.
        >     - Al posto dell'operazione di ridenominazione, creare quindi una nuova categoria con il nuovo nome e aggiungere la nuova categoria alle app pertinenti.
        >     - È possibile eliminare la categoria dopo aver esaminato l'app.

    - **Documentazione utente**: specificare il percorso di un file da cui gli utenti di Software Center possono ottenere altre informazioni su questa applicazione. Questo percorso è un indirizzo di sito Web o un percorso di rete con un nome file. Assicurarsi che gli utenti possano accedere a questo percorso.  

    - **Testo del collegamento**: specificare il testo visualizzato al posto di "Informazioni aggiuntive" quando viene specificata la documentazione dell'utente.  

    - **URL privacy**: specificare un indirizzo di sito Web per l'informativa sulla privacy per l'applicazione.  

    - **Descrizione localizzata**: immettere una descrizione per questa applicazione nella lingua selezionata.  

    - **Parole chiave**: immettere un elenco di parole chiave nella lingua selezionata. Queste parole chiave consentono agli utenti di Software Center di cercare l'applicazione.  

    - **Icona**: Selezionare **Sfoglia** per selezionare un'icona per questa applicazione. Se non si specifica un'icona, Configuration Manager usa un'icona predefinita. Le icone possono avere dimensioni massime pari a 512x512 pixel.  

4. Nella pagina **Tipi di distribuzione** della Creazione guidata applicazione scegliere **Aggiungi** per creare un nuovo tipo di distribuzione. Per altre informazioni, vedere [Creare tipi di distribuzione per l'applicazione](#bkmk_create-dt).  

5. Scegliere **Avanti**, riesaminare le informazioni sull'applicazione nella pagina **Riepilogo** e quindi terminare la Creazione guidata applicazione.  

La nuova applicazione viene ora visualizzata nel nodo **Applicazioni** della console di Configuration Manager.  

## <a name="create-deployment-types-for-the-application"></a><a name="bkmk_create-dt"></a> Creare tipi di distribuzione per l'applicazione  

Se vengono [rilevate automaticamente le informazioni sull'applicazione](#bkmk_auto-app), alcuni passaggi di questa sezione potrebbero non essere necessari.  

> [!Note]  
> Quando si visualizzano le proprietà di un tipo di distribuzione esistente, le sezioni seguenti corrispondono alle schede della finestra delle proprietà del tipo di distribuzione:  
>
> - [Contenuto](#bkmk_dt-content)
> - [Sequenza di attività](#bkmk_dt-ts)
> - [Metodo di rilevamento](#bkmk_dt-detect)
> - [Esperienza utente](#bkmk_dt-ux)
> - [Requirements](#bkmk_dt-require)
> - [Codici restituiti](#bkmk_dt-return)
> - [Dipendenze](#bkmk_dt-depend)
>  
> Per informazioni sulla scheda **Comportamento di installazione** nelle proprietà di un tipo di distribuzione, vedere [Controllare l'esecuzione di file eseguibili](deploy-applications.md#bkmk_exe-check).  

### <a name="start-the-create-deployment-type-wizard"></a>Avviare la Creazione guidata tipo di distribuzione  

È possibile avviare la Creazione guidata tipo di distribuzione in tre modi:

- **Nel nodo Applicazioni**: Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**, espandere **Gestione applicazioni** e selezionare il nodo **Applicazioni**. Selezionare un'applicazione e quindi selezionare **Crea tipo di distribuzione** nella barra multifunzione.  

- **Quando si crea un'applicazione**: Quando [si specificano manualmente le informazioni sull'applicazione](#bkmk_manual-app) nella Creazione guidata applicazione, selezionare **Aggiungi** nella pagina Tipi di distribuzione.  

- **Dalle proprietà dell'applicazione**: Selezionare un'applicazione esistente nel nodo **Applicazioni** e selezionare su **Proprietà**. Passare alla scheda **Tipi di distribuzione** e selezionare **Aggiungi**.

Seguire quindi una di queste procedure per [identificare automaticamente](#bkmk_auto-dt) o [specificare manualmente](#bkmk_manual-dt) le informazioni sul tipo di distribuzione.  

### <a name="automatically-identify-deployment-type-information"></a><a name="bkmk_auto-dt"></a> Identificare automaticamente le informazioni sul tipo di distribuzione  

1. Nella pagina **Generale** della Creazione guidata tipo di distribuzione:  

    1. Selezionare il **Tipo** di file di installazione dell'applicazione per rilevare le informazioni sul tipo di distribuzione.  

    2. Selezionare **Rileva automaticamente le informazioni sul tipo di distribuzione dai file di installazione**.  

    3. Nella casella **Posizione** specificare il file di installazione dell'applicazione da usare per rilevare le informazioni sul tipo di distribuzione. Questa posizione è un percorso di rete (`\\server\share\filename`) o un collegamento all'archivio. È necessario avere accesso al percorso di rete e alle eventuali sottocartelle che includono contenuto dell'applicazione.  

2. Nella pagina **Importa informazioni** della Creazione guidata tipo di distribuzione verificare le informazioni e quindi selezionare **Avanti**. Se necessario, selezionare **Indietro** per tornare indietro e correggere eventuali errori.  

3. Nella pagina **Informazioni generali** della Creazione guidata tipo di distribuzione, specificare le informazioni seguenti:  

    > [!NOTE]  
    > Alcune delle informazioni sul tipo di distribuzione potrebbero già essere presenti se sono state lette dai file di installazione dell'applicazione. Le opzioni visualizzate, poi, possono variare a seconda del tipo di distribuzione che si sta creando.  

    - **Informazioni generali** sul tipo di distribuzione:  
        - Il **Nome** è obbligatorio  

        - **Commenti amministratore** per una descrizione più dettagliata  

        - **Lingue** disponibili per questo tipo  

    - **Programma di installazione**: Specificare il programma di installazione e le eventuali proprietà necessarie per installare il tipo di distribuzione.  

    - **Comportamento di installazione**: selezionare una delle tre opzioni disponibili per la modalità di installazione di questo tipo di distribuzione da parte di Configuration Manager. Per altre informazioni su queste opzioni, vedere [Esperienza utente](#bkmk_dt-ux).  

    - **Usa una connessione VPN automatica (se configurata)** : se è stato distribuito un profilo VPN nel dispositivo in cui l'utente avvia l'app, connettersi alla VPN all'avvio dell'app. Questa opzione è disponibile solo per Windows 8.1 e Windows Phone 8.1. Le connessioni VPN non sono supportate nei dispositivi Windows Phone 8.1 se si distribuisce più di un profilo VPN nel dispositivo. Per altre informazioni, vedere [Profili VPN](../../protect/deploy-use/vpn-profiles.md).  

4. Scegliere **Avanti** e quindi passare alle [Opzioni del Contenuto per il tipo di distribuzione](#bkmk_dt-content).  

### <a name="manually-specify-the-deployment-type-information"></a><a name="bkmk_manual-dt"></a> Specificare manualmente le informazioni sul tipo di distribuzione  

1. Nella pagina **Generale** della Creazione guidata tipo di distribuzione, nell'elenco a discesa **Tipo**, scegliere il tipo di file di installazione dell'applicazione per questo tipo di distribuzione.

2. Selezionare **Specifica manualmente le informazioni sul tipo di distribuzione** e quindi selezionare **Avanti**.

3. Nella pagina **Informazioni generali** della Creazione guidata tipo di distribuzione specificare un **Nome** per il tipo di distribuzione. Facoltativamente, specificare **Commenti amministratore**, selezionare le **Lingue** per questo tipo di distribuzione e quindi selezionare **Avanti**.  

4. Passare alle [Opzioni del Contenuto per il tipo di distribuzione](#bkmk_dt-content).  

### <a name="deployment-type-content-options"></a><a name="bkmk_dt-content"></a> Opzioni del **Contenuto** per il tipo di distribuzione  

Nella pagina **Contenuto** specificare le informazioni seguenti:  

> [!Note]  
> Quando si visualizzano le proprietà di un tipo di distribuzione esistente, alcune opzioni vengono visualizzate nella scheda **Contenuto** e altre nella scheda **Programmi**.  

- **Percorso contenuto**: specificare il percorso del contenuto per questo tipo di distribuzione o selezionare **Sfoglia** per scegliere la cartella del contenuto del tipo di distribuzione.  

    > [!IMPORTANT]  
    > L'account di sistema del computer server del sito deve avere le autorizzazioni per il percorso del contenuto specificato.  

  - **Rendi permanente il contenuto nella cache client**: il client di Configuration Manager conserva per un periodo illimitato nella rispettiva cache il contenuto del tipo di distribuzione. Il client rende permanente il contenuto anche se l'app è già installata. Questa opzione è utile con alcune distribuzioni, ad esempio le distribuzioni di software basato su Windows Installer. Windows Installer richiede una copia locale del contenuto di origine per l'applicazione degli aggiornamenti. Questa opzione riduce lo spazio disponibile della cache. Se si seleziona questa opzione, una distribuzione di grandi dimensioni potrebbe non riuscire in un momento successivo se lo spazio disponibile della cache non è sufficiente.  

- **Programma di installazione**: specificare il nome del programma di installazione ed eventuali parametri di installazione necessari.  

  - **Avvio installazione da**: specificare la cartella che contiene il programma di installazione per il tipo di distribuzione (facoltativo). Questa cartella può corrispondere a un percorso assoluto nel client o al percorso della cartella del punto di distribuzione contenente i file di installazione.  

- **Programma di disinstallazione**: specificare facoltativamente il nome del programma di disinstallazione ed eventuali parametri obbligatori.  

  - **Avvio disinstallazione da**: specificare la cartella che contiene il programma di disinstallazione per il tipo di distribuzione (facoltativo). Questa cartella può corrispondere a un percorso assoluto nel client. Può anche essere un percorso relativo in un punto di distribuzione della cartella con il pacchetto.  

- **Ripristino programma**: per i tipi di distribuzione Windows Installer e Script Installer, è possibile specificare il nome del programma di ripristino ed eventuali parametri obbligatori.<!--1357866-->  

  - **Inizio ripristino in**: specificare la cartella che contiene il programma di ripristino per il tipo di distribuzione (facoltativo). Questa cartella può corrispondere a un percorso assoluto nel client. Può anche essere un percorso relativo in un punto di distribuzione della cartella con il pacchetto.  

- **Esegui l'installazione e la disinstallazione del programma come processo a 32 bit su client a 64 bit**: Usare i percorsi di file e registro di sistema a 32 bit nei computer basati su Windows per eseguire il programma di installazione per il tipo di distribuzione.  

#### <a name="deployment-type-properties-content-options"></a>Opzioni del **Contenuto** delle proprietà del tipo di distribuzione

Quando si visualizzano le proprietà di un tipo di distribuzione, le opzioni seguenti sono disponibili solo nella scheda **Contenuto**:

- **Impostazioni del contenuto di disinstallazione**:  

  - **Uguale al contenuto di installazione**: selezionare questa opzione se il contenuto di installazione e di disinstallazione è lo stesso. Questa opzione corrisponde all'impostazione predefinita.  

  - **Nessun contenuto di disinstallazione**: selezionare questa opzione se l'applicazione non richiede contenuti per la disinstallazione.  

  - **Diversa dal contenuto di installazione**: se il contenuto di disinstallazione è diverso dal contenuto di installazione, selezionare questa opzione.  

    - **Posizione del contenuto di disinstallazione**: specificare il percorso di rete per il contenuto usato per disinstallare l'applicazione.  

- **Consenti ai client di usare i punti di distribuzione dal gruppo di limiti del sito predefinito**: Specificare se i client devono scaricare e installare il software da un punto di distribuzione nel gruppo di limiti del sito predefinito quando il contenuto non è disponibile da un punto di distribuzione nel gruppo di limiti corrente o nei gruppi di limiti vicini.  

- **Opzioni di distribuzione**: specificare se i client devono scaricare l'applicazione quando usano un punto di distribuzione da un gruppo di limiti vicino o dai gruppi di limiti del sito predefiniti.  

- **Consenti ai client di condividere il contenuto con altri client nella stessa subnet**: specificare se consentire l'uso di BranchCache per i download del contenuto. Per altre informazioni, vedere [BranchCache](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache). BranchCache è sempre abilitato nei client. Questa impostazione è stata rimossa nella versione 1802 poiché i client usano BranchCache, se supportato dal punto di distribuzione.  

### <a name="deployment-type-task-sequence-options"></a><a name="bkmk_dt-ts"></a> Opzioni del tipo di distribuzione **Sequenza di attività**

<!--3555953-->

Per altre informazioni sul tipo di distribuzione sequenza di attività a partire dalla versione 2002, vedere [Tipo di distribuzione sequenza di attività](../get-started/creating-windows-applications.md#bkmk_tsdt).

Nella pagina **Sequenza di attività** specificare le impostazioni seguenti:

- **Sequenza di attività di installazione**: selezionare una sequenza di attività che esegue il processo di installazione per l'app.

- **Sequenza di attività di disinstallazione** (facoltativo): selezionare una sequenza di attività che rimuove l'app.

> [!TIP]  
> Se la sequenza di attività non è visualizzata, verificare che non includa passaggi di distribuzione del sistema operativo o di aggiornamento del sistema operativo. Verificare anche che non è contrassegnata come sequenza di attività a impatto elevato. Per altre informazioni, esaminare i prerequisiti per il [tipo di distribuzione sequenza di attività](../get-started/creating-windows-applications.md#bkmk_tsdt).

### <a name="deployment-type-detection-method-options"></a><a name="bkmk_dt-detect"></a> Opzioni del **Metodo di rilevamento** per il tipo di distribuzione

Questa procedura configura un metodo di rilevamento che indica la presenza del tipo di distribuzione. In altri termini, indica se l'applicazione è già installata nel dispositivo Windows. Usare uno dei due metodi seguenti per creare un metodo di rilevamento:

- [Configura le regole per rilevare la presenza di questo tipo di distribuzione](#bkmk_detect-rule)
- [Usa uno script personalizzato per rilevare la presenza di questo tipo di distribuzione](#bkmk_detect-script)

#### <a name="configure-rules-to-detect-the-presence-of-this-deployment-type"></a><a name="bkmk_detect-rule"></a> Configurare le regole per rilevare la presenza di questo tipo di distribuzione

1. Nella pagina **Metodo di rilevamento** l'opzione **Configura le regole per rilevare la presenza di questo tipo di distribuzione** è selezionata per impostazione predefinita. Selezionare **Aggiungi clausola**.  

2. Nella finestra di dialogo **Regola di rilevamento** selezionare un tipo in **Tipo di impostazione** per rilevare la presenza del tipo di distribuzione:  

    - **File System**: consente di rilevare se un file o una cartella specifica è presente in un dispositivo. In caso affermativo, l'applicazione è installata. Specificare i dettagli aggiuntivi seguenti:  

        - **Tipo**: selezionare se si tratta di un file o di una cartella.  

        - **Percorso** (obbligatorio): immettere o selezionare il percorso locale nel dispositivo che include il file o la cartella. Ad esempio, `C:\Program Files` Non è possibile specificare un percorso di rete condiviso. Se si seleziona **Sfoglia**, passare al file system locale o connettersi a un client rappresentativo per l'esplorazione.  

        - **Nome file o cartella** (obbligatorio): specificare il nome del file o della cartella da rilevare nel percorso indicato in precedenza. Se il client rileva questo file o questa cartella nel dispositivo, considererà l'applicazione come installata nel dispositivo.  

        - **Il file o la cartella sono associati a un'applicazione a 32 bit su sistemi a 64 bit**: Il client cerca prima di tutto la cartella o il file specificato nei percorsi di file a 32 bit. Se la cartella o il file non viene trovato, il client esegue quindi una ricerca nei percorsi a 64 bit.  

    - **Registro di sistema**: consente di rilevare se una chiave o un valore del Registro di sistema è presente in un dispositivo client. In caso affermativo, l'applicazione è installata. Specificare i dettagli aggiuntivi seguenti:  

        - **Hive** (obbligatorio): scegliere un hive del Registro di sistema dall'elenco a discesa. Ad esempio, `HKEY_LOCAL_MACHINE`  

        - **Chiave** (obbligatoria): specificare la chiave del Registro di sistema da cercare nell'hive indicato in precedenza. Ad esempio, `SOFTWARE\Microsoft\Office`  

        - **Valore** (facoltativo): immettere un valore specifico da rilevare nella chiave indicata in precedenza. Se si vuole che il client rilevi il valore predefinito, abilitare l'opzione **Usa il valore predefinito della chiave del Registro di sistema per il rilevamento**. Quando si immette un valore o si abilita questa opzione, è necessario selezionare un **Tipo di dati**.  

        - **La chiave del Registro di sistema è associata a un'applicazione a 32 bit su sistemi a 64 bit**: Selezionare questa opzione per cercare prima la chiave del Registro di sistema specificata nei percorsi del Registro di sistema a 32 bit. Se non è possibile trovare la chiave del Registro di sistema, il client cerca nei percorsi a 64 bit.  

    - **Windows Installer**: consente di rilevare se un file Windows Installer specifico è presente in un dispositivo client. In caso affermativo, l'applicazione è installata. Specificare il **Codice prodotto** MSI da rilevare nel client. Se si seleziona **Sfoglia**, scegliere il file MSI da cui leggere il codice del prodotto.

3. Nella parte inferiore della finestra Regola di rilevamento specificare se l'elemento deve esistere o deve soddisfare una regola. Se ad esempio si effettua il rilevamento tramite un file, per impostazione predefinita è selezionata l'opzione seguente: **L'impostazione del file system deve essere presente nel sistema di destinazione per indicare la presenza dell'applicazione**. Selezionare l'altra opzione per creare una regola per il rilevamento in base alle proprietà di un file o di una cartella. Queste proprietà includono Data modifica, Data creazione, Versione o Dimensioni. I criteri di queste regole sono diversi per ogni tipo di impostazione.  

4. Selezionare **OK** per chiudere la finestra di dialogo **Regola di rilevamento**.  

Quando si crea più di un metodo di rilevamento per un tipo di distribuzione, è possibile raggruppare le clausole per creare una logica più complessa.  

#### <a name="group-detection-clauses-optional"></a>Raggruppare le clausole di rilevamento *(facoltativo)*

1. Creare tre o più clausole per il metodo di rilevamento per un tipo di distribuzione.  

2. Selezionare due o più clausole consecutive e quindi selezionare **Raggruppa**. Alle colonne associate verranno aggiunte parentesi, che indicano dove inizia e finisce il gruppo.  

    Esempio:

    | Connettore  |  ( | Clausola           |  ).  |
    |------------|----|------------------|-----|
    |            |    | Codice prodotto MSI |     |
    | Oppure         | (  | file1.text esiste|     |
    | And        |    | file2.text esiste | ).   |

3. Per rimuovere il gruppo, selezionare le clausole raggruppate e quindi selezionare **Separa**.  

*Continuare* con la sezione successiva sull'uso di uno script personalizzato come metodo di rilevamento oppure [passare](#bkmk_dt-ux) alle opzioni di *Esperienza utente* per il tipo di distribuzione.

#### <a name="use-a-custom-script-to-check-for-the-presence-of-a-deployment-type"></a><a name="bkmk_detect-script"></a> Usare uno script personalizzato per rilevare la presenza di questo tipo di distribuzione  

1. Nella pagina **Metodo di rilevamento** selezionare la casella **Usa uno script personalizzato per rilevare la presenza di questo tipo di distribuzione**. Selezionare quindi **Modifica**.  

2. Nella finestra di dialogo **Editor dello script** selezionare un **tipo di script** per rilevare il tipo di distribuzione: PowerShell, VBScript o JScript.  

    > [!Note]  
    > Quando si esegue uno script di Windows PowerShell come metodo di rilevamento app, il client di Configuration Manager chiama PowerShell con il parametro `-NoProfile`. Questa opzione avvia PowerShell senza i profili. Un profilo di PowerShell è uno script che viene eseguito all'avvio di PowerShell. <!--3607762-->  

3. Nella casella **Contenuti script** immettere lo script da usare o incollare i contenuti di uno script esistente. Scegliere **Apri** per passare a uno script salvato esistente. Selezionare **Cancella** per rimuovere il test dal campo Contenuti script. Se necessario, abilitare l'opzione **Esegui lo script come processo a 32 bit nei client a 64 bit**.  

    > [!NOTE]  
    > Le dimensioni massime consentite per uno script sono 32 KB.  

4. Selezionare **OK** per salvare lo script e chiudere la finestra di dialogo **Editor dello script**. Nella Creazione guidata tipo di distribuzione i campi **Tipo di script** e **Lunghezza script** vengono aggiornati con informazioni dettagliate sullo script selezionato.

#### <a name="about-custom-script-detection-methods"></a>Informazioni sui metodi di rilevamento di script personalizzati  

Configuration Manager controlla i risultati dello script. Legge i valori scritti dallo script nel flusso di output standard (STDOUT) e nel flusso degli errori standard (STDERR), nonché il codice di uscita. Se il codice di uscita dello script è un valore diverso da zero, lo script non è riuscito e lo stato del rilevamento dell'applicazione è *Sconosciuto*. Se il codice di uscita è pari a zero e STDOUT contiene dati, lo stato di rilevamento dell'applicazione è *Installato*.

> [!TIP]
> Quando si crea uno script di rilevamento, se si restituisce un codice di uscita pari a zero ma non si restituisce nessun output (dati in STDOUT), l'applicazione non viene rilevata come installata. Per altre informazioni, vedere gli esempi seguenti.

Usare le tabelle seguenti per controllare se un'applicazione è installata usando l'output di uno script:  

##### <a name="zero-exit-code"></a>Codice di uscita uguale a zero

|STDOUT|STDERR|Risultato dello script|Stato di rilevamento dell'applicazione|
|---------|---------|---------|---------|
|Vuoto|Vuoto|Operazione completata|Non installato|
|Vuoto|Non vuoto|Errore|Sconosciuto|
|Non vuoto|Vuoto|Operazione completata|Installato|
|Non vuoto|Non vuoto|Operazione completata|Installato|

##### <a name="non-zero-exit-code"></a>Codice di uscita diverso da zero

|STDOUT|STDERR|Risultato dello script|Stato di rilevamento dell'applicazione|
|---------|---------|---------|---------|
|Vuoto|Vuoto|Errore|Sconosciuto|
|Vuoto|Non vuoto|Errore|Sconosciuto|
|Non vuoto|Vuoto|Errore|Sconosciuto|
|Non vuoto|Non vuoto|Errore|Sconosciuto|

##### <a name="examples"></a>Esempi

Usare gli esempi di PowerShell/VBScript seguenti per creare script personalizzati per il rilevamento di applicazioni:  

**Esempio 1**: Lo script restituisce un codice di uscita diverso da zero. Questo codice indica che l'esecuzione dello script ha avuto esito negativo. In questo caso, lo stato di rilevamento dell'applicazione è sconosciuto.  

``` PowerShell
Exit 1
```

``` VBScript
WScript.Quit(1)
```

**Esempio 2**: Lo script restituisce un codice di uscita pari a zero, ma il valore di STDERR non è vuoto. Questo risultato indica che l'esecuzione dello script ha avuto esito negativo. In questo caso, lo stato di rilevamento dell'applicazione è sconosciuto.  

``` PowerShell
Write-Error "Script failed"
Exit 0
```

``` VBScript
WScript.StdErr.Write "Script failed"
WScript.Quit(0)
```

**Esempio 3**: Lo script restituisce un valore del codice di uscita pari a zero, che indica un'esecuzione corretta dello script. Il valore di STDOUT è tuttavia vuoto e ciò indica che l'applicazione non è installata.  

``` PowerShell
Exit 0
```

``` VBScript
WScript.Quit(0)
```

**Esempio 4**: Lo script restituisce un valore del codice di uscita pari a zero, che indica un'esecuzione corretta dello script. Il valore per STDOUT non è vuoto e ciò indica che l'applicazione è installata.  

``` PowerShell
Write-Host "The application is installed"
Exit 0
```

``` VBScript
WScript.StdOut.Write "The application is installed"
WScript.Quit(0)
```

**Esempio 5**: Lo script restituisce un valore del codice di uscita pari a zero, che indica un'esecuzione corretta dello script. I valori per STDOUT e STDERR non sono vuoti e ciò indica che l'applicazione è installata.  

``` PowerShell
Write-Host "The application is installed"
Write-Error "Completed"
Exit 0
```

``` VBScript
WScript.StdOut.Write "The application is installed"
WScript.StdErr.Write "Completed"
WScript.Quit(0)
```

### <a name="deployment-type-user-experience-options"></a><a name="bkmk_dt-ux"></a> Opzioni di **User Experience** del tipo di distribuzione

Queste impostazioni specificano il modo in cui il client installa l'applicazione nei dispositivi e ciò che viene visualizzato per l'utente.  

Nella pagina **Esperienza utente** specificare le informazioni seguenti:  

- **Comportamento installazione**: Nell'elenco a discesa selezionare una delle seguenti opzioni:  

  - **Installa per utente**: il client installa l'applicazione solo per l'utente per cui viene distribuita l'applicazione.  

  - **Installa per sistema**: il client installa l'applicazione solo una volta. È disponibile per tutti gli utenti.  

  - **Installa per sistema se la risorsa è un dispositivo, altrimenti installa per utente**: Se si distribuisce l'applicazione per un dispositivo, il client la installa per tutti gli utenti. Se si distribuisce l'applicazione per un utente, il client la installa solo per tale utente.  

- **Requisiti di accesso**: Selezionare una delle opzioni seguenti:  

  - **Solo se un utente è connesso**  

  - **Indipendentemente dalla connessione degli utenti**  

  - **Solo se nessun utente è connesso**  

    > [!NOTE]  
    > Per impostazione predefinita, questa opzione è impostata su **Solo se un utente è connesso**. Se si seleziona **Installa per utente** nell'elenco a discesa **Comportamento installazione**, non è possibile modificare questa opzione.  

- **Visibilità del programma di installazione**: specificare la modalità in cui viene eseguito il tipo di distribuzione sui dispositivi client. Selezionare una delle opzioni seguenti:  

  - **Ingrandita**: Il tipo di distribuzione viene eseguito in modalità ingrandita sui dispositivi client. Gli utenti potranno seguire l'intera l'attività di installazione.  

  - **Normale**: Il tipo di distribuzione viene eseguito in modalità normale in base alle impostazioni predefinite del sistema e del programma. Questa è la modalità predefinita.  

  - **Ridotta a icona**: Il tipo di distribuzione viene eseguito in modalità ridotta nei dispositivi client. Gli utenti possono visualizzare l'attività di installazione nell'area di notifica o sulla barra delle applicazioni.  

  - **Nascosto**: l'esecuzione del tipo di distribuzione viene nascosta nei dispositivi client. Gli utenti non vedono alcuna attività di installazione.  

- **Consenti agli utenti di visualizzare e interagire con l'installazione del programma**: specifica se un utente può interagire con l'installazione del tipo di distribuzione per configurarne le opzioni.  

    Questa opzione viene abilitata per impostazione predefinita se è stata selezionata l'opzione **Installa per utente** nell'elenco a discesa **Comportamento installazione**.  

    > [!IMPORTANT]  
    > Quando si seleziona il comportamento **Installa per sistema** questa impostazione è facoltativa. Lo scopo principale di questa modifica è di consentire agli utenti finali di interagire con l'installazione durante una sequenza di attività, ad esempio per eseguire un processo di installazione che chiede all'utente finale diverse opzioni. Nei programmi di installazione di alcune applicazioni non è possibile disattivare le richieste all'utente, in quanto il processo di installazione può richiedere valori di configurazione specifici noti solo all'utente. <!--1356976-->  
    >  
    > L'installazione in un contesto di sistema e l'autorizzazione dell'interazione con l'installazione da parte degli utenti non consentono di ottenere una configurazione sicura. Per altre informazioni, vedere [Sicurezza e privacy per la gestione delle applicazioni](../plan-design/security-and-privacy-for-application-management.md#bkmk_interact).  

- **Tempo di esecuzione massimo consentito (minuti)** : specificare la durata massima di esecuzione in minuti prevista per il tipo di distribuzione nel computer client. È possibile specificare questa impostazione come numero intero maggiore di zero. Il valore predefinito è 120 minuti (due ore).  

    Usare questo valore per le azioni seguenti:  

  - Per monitorare i risultati dal tipo di distribuzione.  

  - Per verificare se un tipo di distribuzione è installato quando si definiscono finestre di manutenzione nei dispositivi client. Quando è attiva una finestra di manutenzione, un tipo di distribuzione viene avviato solo se il tempo disponibile nella finestra di manutenzione è sufficiente per il valore specificato nell'impostazione **Tempo esecuzione massimo consentito**.  

    > [!IMPORTANT]  
    > Potrebbe verificarsi un conflitto se il **Tempo di esecuzione massimo consentito** è maggiore della finestra di manutenzione pianificata. Se l'utente imposta il tempo di esecuzione massimo su una durata maggiore di quella di qualsiasi finestra di manutenzione disponibile, il tipo di distribuzione corrispondente non viene eseguito.  

- **Tempo previsto di installazione (minuti)** : specificare il tempo di installazione previsto del tipo di distribuzione. Gli utenti possono visualizzarlo in Software Center.  

#### <a name="deployment-type-properties-user-experience-options"></a>Opzioni di **Esperienza utente** delle proprietà del tipo di distribuzione

Quando si visualizzano le proprietà di un tipo di distribuzione, le opzioni seguenti sono disponibili solo nella scheda **Esperienza utente**:

È possibile imporre un comportamento specifico successivo all'installazione. Selezionare una delle opzioni seguenti:  

- **Determinare il comportamento in base ai codici restituiti**: è possibile gestire i riavvii in base ai codici configurati nella scheda [Codici restituiti](#bkmk_dt-return). Software Center visualizza che **potrebbe essere necessario un riavvio**. Se un utente esegue l'accesso durante l'installazione, viene visualizzata una richiesta in base alla configurazione di Esperienza utente della *distribuzione*.  

- **Nessuna azione specifica**: non è necessario il riavvio dopo l'installazione. Software Center segnala che non è necessario eseguire il riavvio.  

- **Il programma di installazione software potrebbe forzare il riavvio del dispositivo**: Configuration Manager non controlla o inizializza un riavvio, ma è possibile che l'installazione effettiva esegua questa operazione senza preavviso. Usare questa impostazione per impedire la segnalazione di errori di installazione di Configuration Manager quando il programma di installazione esegue un riavvio. Software Center visualizza che **potrebbe essere necessario un riavvio**.  

- **Il client Configuration Manager forzerà il riavvio obbligatorio del dispositivo**: Configuration Manager forza un riavvio del dispositivo al termine dell'installazione. Software Center segnala che è necessario eseguire il riavvio. Se un utente esegue l'accesso durante l'installazione, viene visualizzata una richiesta in base alla configurazione di Esperienza utente della *distribuzione*.  

### <a name="deployment-type-requirements"></a><a name="bkmk_dt-require"></a>**Requisiti** del tipo di distribuzione

Configuration Manager verifica i requisiti nei dispositivi prima di installare il tipo di distribuzione. È possibile usare i requisiti per perfezionare e controllare meglio i dispositivi o gli utenti che ricevono questa applicazione. Se ad esempio si distribuisce l'applicazione a una raccolta utenti, specificare qui i requisiti per l'hardware dell'app.

1. Nella pagina **Requisiti** selezionare **Aggiungi** per aprire la finestra di dialogo **Crea requisito**.  

2. Dall'elenco a discesa **Categoria** selezionare se questo requisito riguarda un **Dispositivo** o un **Utente**.  

    Selezionare **Personalizzata** per usare una condizione globale creata in precedenza. Quando si seleziona **Personalizzata**, è inoltre possibile fare clic su **Crea** per creare una nuova condizione globale. Per altre informazioni sulle condizioni globali, vedere [Come creare condizioni globali](create-global-conditions.md).  

    > [!IMPORTANT]  
    > Se si distribuisce l'applicazione a una raccolta dispositivi, il client ignora qualsiasi requisito della categoria **Utente** e la condizione **Dispositivo primario**.  

3. Nell'elenco a discesa **Condizione** selezionare la condizione per valutare se l'utente o il dispositivo soddisfano i requisiti di installazione. Il contenuto di questo elenco varia a seconda della categoria selezionata.  

4. Nell' elenco a discesa **Operatore** selezionare l'operatore da usare. Questo operatore confronta la condizione selezionata con il valore specificato, valutando se l'utente o il dispositivo soddisfa il requisito di installazione. Gli operatori disponibili variano a seconda della condizione selezionata. Quando si usa l'operatore `One Of`, il campo Valori contiene il codice di convalida che è necessario immettere per ogni riga.

    > [!Note]  
    > I requisiti disponibili variano a seconda del tipo di dispositivo usato dal tipo di distribuzione.  

5. Nella casella **Valore** specificare i valori da usare per il confronto. Questi valori, con la condizione e l'operatore selezionati, valutano se l'utente o il dispositivo soddisfa i requisiti di installazione. I valori disponibili variano a seconda della condizione e dell'operatore selezionati.  

6. Scegliere **OK** per salvare il requisito e chiudere la finestra di dialogo **Creazione requisito**.  

### <a name="deployment-type-dependencies"></a><a name="bkmk_dt-depend"></a>**Dipendenze** del tipo di distribuzione  

Le dipendenze definiscono uno o più tipi di distribuzione da un'altra applicazione che il client deve installare prima dell'installazione di questo tipo di distribuzione.

> [!IMPORTANT]  
> In alcuni casi, un tipo di distribuzione dipende dal tipo di distribuzione che contiene anche le dipendenze. Il numero massimo di dipendenze supportate nella catena è cinque.  

1. Nella pagina **Dipendenze** selezionare **Aggiungi**.  

2. Nella finestra Aggiungi dipendenza immettere il **Nome gruppo di dipendenze**. Questo nome fa riferimento al gruppo di dipendenze dell'applicazione.  

3. Nella finestra Aggiungi dipendenza selezionare **Aggiungi**.  

4. Nella finestra **Specifica applicazione richiesta** selezionare un'applicazione disponibile e almeno uno dei rispettivi tipi di distribuzione da usare come dipendenza.  

    > [!TIP]  
    > Selezionare **Visualizza** per visualizzare le proprietà del tipo di distribuzione o dell'applicazione selezionato.  

5. Selezionare **OK** per chiudere la finestra **Specifica applicazione richiesta**.  

6. Se si vuole che il client installi automaticamente l'applicazione dipendente, selezionare **Installazione automatica** accanto alla dipendenza.  

    > [!NOTE]  
    > Non è necessario distribuire un'applicazione dipendente per consentirne l'installazione automatica da parte del client.  

7. Se si aggiungono più dipendenze, usare i pulsanti **Aumenta priorità** e **Diminuisci priorità**. Queste azioni modificano l'ordine in cui il client valuta ogni dipendenza.  

8. Selezionare **OK** per chiudere la finestra **Aggiungi dipendenza**.  

### <a name="deployment-type-return-codes"></a><a name="bkmk_dt-return"></a>**Codici restituiti** del tipo di distribuzione

> [!Note]  
> Questa pagina non è disponibile nella Creazione guidata tipo di distribuzione. Si tratta di una scheda delle proprietà di un tipo di distribuzione esistente.  

Specificare i codici restituiti per controllare i comportamenti dopo il completamento del tipo di distribuzione. È ad esempio possibile segnalare che è necessario il riavvio e che l'installazione è stata completata.

1. Nella scheda **Codici restituiti** della finestra delle proprietà del tipo di distribuzione selezionare **Aggiungi**.  

2. Nella finestra Aggiungi codice restituito specificare il **Valore del codice restituito** previsto da questo tipo di distribuzione. Questo valore può essere un qualunque numero intero positivo o negativo compreso tra `-2147483648` e `2147483647`.  

3. Selezionare un **Tipo di codice** dall'elenco a discesa. Questa impostazione consente di definire il modo in cui Configuration Manager interpreta il codice restituito da questo tipo di distribuzione. I tipi disponibili dipendono dalla tecnologia del tipo di distribuzione.  

    - **Operazione riuscita (senza riavvio)** : il tipo di distribuzione è stato installato e non è necessario alcun riavvio.  

    - **Errore (senza riavvio)** : non è stato possibile installare il tipo di distribuzione.  

    - **Avvio a freddo**: il tipo di distribuzione è stato installato, ma richiede il riavvio del dispositivo. Non è possibile eseguire altre installazioni fino al riavvio del dispositivo.  

    - **Avvio a caldo**: il tipo di distribuzione è stato installato, ma richiede il riavvio del dispositivo. È possibile eseguire altre installazioni prima del riavvio del dispositivo.  

    - **Tentativo veloce**: un'altra installazione è già in corso nel dispositivo. Il client esegue nuovi tentativi ogni due ore, per un totale di 10 volte.  

4. È facoltativamente possibile immettere un **Nome** e una **Descrizione** per questo codice restituito.

5. Selezionare **OK** per chiudere la finestra Aggiungi codice restituito.  

#### <a name="example-non-zero-success"></a>Esempio: esito positivo diverso da zero

Viene distribuita un'applicazione che restituisce un codice di uscita pari a `1` se l'installazione ha esito positivo. Per impostazione predefinita, Configuration Manager rileva questo codice diverso da zero come errore. Specificare `1` per il Valore del codice restituito e selezionare **Operazione riuscita (senza riavvio)** per il Tipo di codice. Configuration Manager interpreta ora tale codice restituito come esito positivo per il tipo di distribuzione.

#### <a name="default-return-codes"></a>Codici restituiti predefiniti

Quando si creano alcuni tipi di distribuzione, Configuration Manager aggiunge automaticamente i codici restituiti seguenti comuni per la rispettiva tecnologia:  

##### <a name="windows-installer-msi-file"></a>Windows Installer (file \*.msi)

|Valore    |Tipo di codice|
|---------|---------|
|0        |Operazione riuscita (senza riavvio)|
|1707     |Operazione riuscita (senza riavvio)|
|3010     |Avvio a caldo|
|1641     |Avvio a freddo|
|1618     |Tentativo veloce|

##### <a name="script-installer"></a>Programma di installazione dello script

|Valore    |Tipo di codice|
|---------|---------|
|0        |Operazione riuscita (senza riavvio)|
|1641     |Avvio a freddo|
|3010     |Avvio a caldo|
|1618     |Tentativo veloce|

##### <a name="windows-app-package-appx-appxbundle-msix-msixbundle"></a>Pacchetto app Windows (\*.appx, \*.appxbundle, \*.msix, \*.msixbundle)

|Valore    |Tipo di codice|
|---------|---------|
|15605    |Tentativo veloce|
|15618    |Tentativo veloce|

## <a name="additional-options-for-app-v-deployment-types"></a><a name="bkmk_appv"></a> Opzioni aggiuntive per i tipi di distribuzione App-V  

È possibile configurare opzioni aggiuntive univoche per i tipi di distribuzione per le applicazioni virtuali (App-V).  

### <a name="app-v-deployment-type-content-options"></a><a name="bkmk_appv-content"></a> Opzioni del **Contenuto** per il tipo di distribuzione App-V  

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**, espandere **Gestione applicazioni** e selezionare il nodo **Applicazioni**.  

2. Selezionare un'applicazione con un tipo di distribuzione App-V e selezionare **Proprietà**.  

3. Nelle proprietà dell'applicazione passare alla scheda **Tipi di distribuzione**. Selezionare il tipo di distribuzione App-V e selezionare **Modifica**.  

4. Nelle proprietà del tipo di distribuzione passare alla scheda **Contenuto**. Configurare le opzioni seguenti in base alla necessità:  

    - **Rendi permanente il contenuto nella cache client**: il client di Configuration Manager non eliminerà dalla cache il contenuto per questo tipo di distribuzione.  

    - **Carica contenuto nella cache App-V prima dell'avvio**: prima dell'avvio dell'applicazione, il client di Configuration Manager carica nella cache di App-V tutto il contenuto per questo tipo di distribuzione. Il client non aggiunge il contenuto alla cache. Elimina il contenuto in base alla necessità.  

5. Selezionare **OK** per chiudere le proprietà del tipo di distribuzione. Quindi selezionare **OK** per chiudere le proprietà dell'applicazione.  

### <a name="app-v-deployment-type-publishing-options"></a><a name="bkmk_appv-pub"></a> Opzioni di **Pubblicazione** per il tipo di distribuzione App-V

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**, espandere **Gestione applicazioni** e selezionare il nodo **Applicazioni**.  

2. Selezionare un'applicazione con un tipo di distribuzione App-V e selezionare **Proprietà**.  

3. Nelle proprietà dell'applicazione passare alla scheda **Tipi di distribuzione**. Selezionare il tipo di distribuzione App-V e selezionare **Modifica**.  

4. Nelle proprietà del tipo di distribuzione passare alla scheda **Pubblicazione**. Selezionare gli elementi dell'applicazione virtuale da pubblicare.  

5. Selezionare **OK** per chiudere le proprietà del tipo di distribuzione. Quindi selezionare **OK** per chiudere le proprietà dell'applicazione.  

## <a name="import-an-application"></a><a name="bkmk_import"></a> Importare un'applicazione  

Seguire questa procedura per importare un'applicazione in Configuration Manager:

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**, espandere **Gestione applicazioni** e selezionare il nodo **Applicazioni**.  

2. Nella barra multifunzione nella scheda **Home** e nel gruppo **Crea** selezionare **Importa applicazione**.  

3. Nella pagina **Generale** dell'Importazione guidata applicazione specificare il percorso di rete del **File** da importare. Ad esempio, `\\server\share\file.zip` Questo file è un archivio compresso valido (formato ZIP) di un'applicazione esportata di Configuration Manager.  

4. Nella pagina **Contenuto file** selezionare l'azione da eseguire se l'applicazione è un duplicato di un'applicazione esistente. Creare una nuova applicazione oppure ignorare il duplicato e aggiungere una nuova revisione per l'applicazione esistente.  

5. Nella pagina **Riepilogo** esaminare le azioni e quindi terminare la procedura guidata.  

La nuova applicazione viene visualizzata nel nodo **Applicazioni**.  

> [!TIP]  
> Il cmdlet di Windows PowerShell **Import-CMApplication** ha la stessa funzione di questa procedura. Per altre informazioni, vedere [Import-CMApplication](https://docs.microsoft.com/powershell/module/configurationmanager/import-cmapplication?view=sccm-ps).  

Per altre informazioni su come esportare un'applicazione, vedere [Attività di gestione per applicazioni](management-tasks-applications.md).

## <a name="supported-deployment-types"></a><a name="bkmk_deploy-types"></a> Tipi di distribuzione supportati  

Configuration Manager supporta i tipi di distribuzione seguenti per le applicazioni:

| Nome del tipo di distribuzione | Descrizione |
|--------------------------|----------------------|  
| **Windows Installer (file \*.msi)** | Un file di Windows Installer. |  
| **Pacchetto app Windows (\*.appx, \*.appxbundle, \*.msix, \*.msixbundle)** | Un file di pacchetto di app Windows (con estensione appx), un pacchetto di bundle di app Windows (con estensione appxbundle), un pacchetto di app Windows 10 (con estensione msix) o un bundle di app Windows 10 (con estensione msixbundle).<!--1357427--> |  
| **Pacchetto app Windows (in Windows Store)** | Consente di specificare un collegamento all'app in Windows Store o esplorare lo Store per selezionare l'app.<sup>[Nota 1](#bkmk_note1)</sup> |  
| **Programma di installazione dello script** | Consente di specificare uno script o un programma che viene eseguito nei client Windows per installare contenuti o eseguire un'azione. Usare questo tipo di distribuzione per programmi di installazione di tipo setup.exe o wrapper di script. |  
| **Microsoft Application Virtualization 4** | Un manifesto di Microsoft App-V v4. |  
| **Microsoft Application Virtualization 5** | Un file del pacchetto Microsoft App-V v5. |  
| **Pacchetto app Windows Phone (file \*.xap)** | Un file del pacchetto app Windows Phone. |  
| **Pacchetto app Windows Phone (in Windows Phone Store)** | Consente di specificare un collegamento per l'app in Windows Store. |  
| **Mac OS X** | Per computer macOS che eseguono il client di Configuration Manager. Creare un file con estensione cmmac con lo strumento **CMAppUtil**. |  
| **Applicazione Web** | Consente di specificare un collegamento a un'applicazione Web. Il tipo di distribuzione installa un collegamento all'applicazione Web sul dispositivo dell'utente. |  
| **Windows Installer tramite MDM (\*.msi)** | Consente di creare e distribuire app basate su Windows Installer in dispositivi Windows 10. Per altre informazioni, vedere [Distribuire app Windows Installer nei PC Windows 10 registrati](../get-started/creating-windows-applications.md#bkmk_mdm-msi). |
| **Sequenza di attività** | A partire dalla versione 2002, installare o disinstallare applicazioni complesse usando le sequenze di attività. Per altre informazioni, vedere [Tipo di distribuzione sequenza di attività](../get-started/creating-windows-applications.md#bkmk_tsdt). <!--3555953--> |

> [!NOTE]
> La console di Configuration Manager può elencare altri tipi di distribuzione, ma si tratta di piattaforme che non sono più supportate. Per altre informazioni, vedere [Che cosa è successo alla MDM ibrida?](../../mdm/understand/what-happened-to-hybrid.md).

### <a name="note-1-windows-app-package-in-the-windows-store"></a><a name="bkmk_note1"></a> Nota 1: Pacchetto app Windows (in Windows Store)

Per distribuire l'app come collegamento a Windows Store, configurare l'impostazione **Disattiva applicazione Store** di Criteri di gruppo. Impostare il criterio su **Disabilitato** o **Non configurato**. Se questa impostazione è abilitata, i client non possono connettersi a Windows Store per scaricare e installare applicazioni.

I client Windows valutano sempre i tipi di distribuzione che usano un collegamento a uno Store prima di altri tipi di distribuzione. Il client valuta quindi i tipi di distribuzione in base alla priorità.

> [!TIP]
> Alcuni collegamenti allo store possono generare questo errore nella Creazione guidata applicazione: "Collegamento applicazione non valido". Ad esempio, alcune *App in evidenza* dello store possono provocare questo errore. È comunque possibile selezionare **Avanti** nella pagina **Generale** della procedura guidata. Configuration Manager crea correttamente l'app, che può quindi essere distribuita.<!-- SCCMDocs-pr #4716 -->

## <a name="next-steps"></a>Passaggi successivi

Dopo aver creato un'applicazione in Configuration Manager, il passaggio successivo consiste nella [distribuzione dell'applicazione](deploy-applications.md).

A partire dalla versione 1906, creare un gruppo di applicazioni che è possibile inviare a un utente o a una raccolta di dispositivi come singola distribuzione. Per altre informazioni, vedere [Creare gruppi di applicazioni](create-app-groups.md).

Per altre informazioni sulla creazione di applicazioni in piattaforme del sistema operativo diverse, vedere gli articoli seguenti:  

- [Creare applicazioni Windows](../get-started/creating-windows-applications.md)
- [Creare applicazioni Mac](../get-started/creating-mac-computer-applications.md)
- [Creazione di applicazioni server Linux e UNIX](../get-started/creating-linux-and-unix-server-applications.md)
- [Creazione di applicazioni Windows Embedded](../get-started/creating-windows-embedded-applications.md)
