---
title: Distribuire contenuto
titleSuffix: Configuration Manager
description: Ecco come è possibile iniziare a distribuire contenuto ai punti di distribuzione per Configuration Manager dopo averli installati.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d50dcca0-4419-449d-a487-73abcadf328f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7478eff1a14eeffd4d12b1539df7c5573c6a7cb6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707259"
---
# <a name="deploy-and-manage-content-for-configuration-manager"></a>Distribuire e gestire contenuto per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

È possibile iniziare a distribuire contenuto ai punti di distribuzione per Configuration Manager dopo averli installati. In genere, il contenuto viene trasferito ai punti di distribuzione in rete, ma esistono altre opzioni per inviare il contenuto ai punti di distribuzione. Dopo che il contenuto è stato trasferito in un punto di distribuzione, è possibile aggiornare, ridistribuire, rimuovere e convalidare il contenuto nei punti di distribuzione.  

##  <a name="distribute-content"></a><a name="bkmk_distribute"></a> Distribuire il contenuto  
In genere, il contenuto viene distribuito ai punti di distribuzione in modo che sia disponibile per i computer client. Un'eccezione a questo comportamento si verifica quando si usa la distribuzione del contenuto su richiesta per una distribuzione specifica.  Quando si distribuisce il contenuto, Configuration Manager archivia i file di contenuto in un pacchetto e distribuisce il pacchetto al punto di distribuzione. È possibile distribuire diversi tipi di contenuto, tra cui:  

- Tipi di distribuzioni delle applicazioni  

- Pacchetti  

- Pacchetti di distribuzione  

- Pacchetti driver  

- Immagini del sistema operativo  

- Programmi di installazione del sistema operativo  

- Immagini d'avvio  

- Sequenze attività  

Quando si crea un pacchetto che contiene i file di origine, ad esempio un tipo di distribuzione di un'applicazione o un pacchetto di distribuzione, il sito in cui il pacchetto viene creato diventa il proprietario del sito o un tipo di distribuzione di applicazioni, il sito in cui viene creato il pacchetto diventa il sito proprietario dell'origine contenuto del pacchetto. Configuration Manager copia i file di origine dal percorso del file di origine specificato per l'oggetto nella raccolta contenuto nel server del sito che ha la proprietà dell'origine contenuto del pacchetto.  Configuration Manager replica quindi le informazioni nei siti aggiuntivi. Per altre informazioni sulla raccolta contenuto, vedere la pagina relativa alla [Raccolta contenuto](../../../../core/plan-design/hierarchy/the-content-library.md).  

Utilizzare la procedura seguente per distribuire contenuto nei punti di distribuzione.  

#### <a name="to-distribute-content-on-distribution-points"></a>Per distribuire contenuto nei punti di distribuzione  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** , selezionare uno dei seguenti passaggi per il tipo di contenuto che si desidera distribuire:  

    - **Applicazioni**: espandere **Gestione applicazioni** > **Applicazioni** e quindi selezionare le applicazioni da distribuire.  

    - **Pacchetti**: espandere **Gestione applicazioni** >  **Pacchetti** e quindi selezionare i pacchetti da distribuire.  

    - **Pacchetti di distribuzione**: espandere **Aggiornamenti software** >  **Pacchetti di distribuzione** e quindi selezionare i pacchetti di distribuzione da distribuire.  

    - **Pacchetti driver**: espandere **Sistemi operativi** >  **Pacchetti driver** e quindi selezionare i pacchetti driver da distribuire.  

    - **Immagini del sistema operativo**: espandere **Sistemi operativi** >  **Immagini del sistema operativo** e quindi selezionare le immagini del sistema operativo da distribuire.  

    - **Programmi di installazione sistema operativo**: espandere **Sistemi operativi** > **Programmi di installazione sistema operativo** e quindi selezionare i programmi di installazione del sistema operativo da distribuire.  

    - **Immagini d'avvio**: espandere **Sistemi operativi** >  **Immagini d'avvio** e quindi selezionare le immagini di avvio da distribuire.  

    - **Sequenze di attività**: espandere **Sistemi operativi** >  **Sequenze di attività** e quindi selezionare la sequenza di attività da distribuire. Anche se le sequenze attività non hanno contenuto, presentano delle dipendenze contenuto associate che vengono distribuite.  

      > [!NOTE]  
      > Se si modifica la sequenza attività, è necessario ridistribuire il contenuto.  

3.  Nella scheda **Home** , nel gruppo **Distribuzione** , fare clic su **Distribuisci contenuto**. Viene visualizzata la Distribuzione guidata contenuto.  

4.  Nella pagina **Generale** verificare che il contenuto in elenco sia il contenuto che si intende distribuire, scegliere se si vuole che Configuration Manager rilevi le dipendenze contenuto associate al contenuto selezionato e aggiunga le dipendenze alla distribuzione e fare clic su **Avanti**.  

    > [!NOTE]  
    > È presente l'opzione per configurare l'impostazione **Rileva le dipendenze contenuto associate e aggiungile alla distribuzione** solo per il tipo di contenuto dell'applicazione. Configuration Manager configura automaticamente questa impostazione per le sequenze di attività e l'impostazione non può essere modificata.  

5.  Nella scheda **Contenuto** , se visualizzata, verificare che il contenuto in elenco sia il contenuto che si desidera distribuire, quindi fare clic su **Avanti**.  

    > [!NOTE]  
    > La pagina **Contenuto** viene visualizzata solo quando l'impostazione **Rileva le dipendenze contenuto associate e aggiungile alla distribuzione** viene selezionata nella pagina **Generale** della procedura guidata.  

6.  Nella pagina **Destinazione contenuto** , fare clic su **Aggiungi**, scegliere uno dei seguenti elementi, quindi seguire i relativi passaggi:  

    - **Raccolte**: selezionare **Raccolte utenti** o **Raccolte dispositivi**, fare clic sulla raccolta associata a uno o più gruppi di punti di distribuzione e quindi fare clic su **OK**.  

        > [!NOTE]  
        > Vengono visualizzate solo le raccolte associate a un gruppo di punti di distribuzione. Per altre informazioni su come associare le raccolte ai gruppi di punti di distribuzione, vedere [Gestire i gruppi di punti di distribuzione](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage) nell'argomento [Installare e configurare punti di distribuzione per Configuration Manager](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md).  

    - **Punto di distribuzione**: selezionare un punto di distribuzione esistente e quindi fare clic su **OK**. Non vengono visualizzati i punti di distribuzione che hanno ricevuto il contenuto in precedenza.  

    - **Gruppo di punti di distribuzione**: selezionare un gruppo di punti di distribuzione esistente e quindi fare clic su **OK**. Non vengono visualizzati i gruppi di punti di distribuzione che hanno ricevuto il contenuto in precedenza.  

    Dopo aver aggiunto le destinazioni del contenuto, fare clic su **Avanti**.  

7.  Nella pagina **Riepilogo** , rivedere le impostazioni per la distribuzione prima di continuare. Per distribuire il contenuto nelle destinazioni selezionate, fare clic su **Avanti**.  

8.  La pagina **Avanzamento** visualizza l'avanzamento della distribuzione.  

9. La pagina **Conferma** visualizza se il contenuto è stato correttamente assegnato ai punti. Per monitorare la distribuzione del contenuto, vedere [Monitorare il contenuto distribuito con Configuration Manager](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md).  

##  <a name="use-prestaged-content"></a><a name="bkmk_prestage"></a> Usare il contenuto pre-installazione  
È possibile pre-installare i file di contenuto per applicazioni e tipi di pacchetti:  

- Nella console di Configuration Manager si seleziona il contenuto necessario e si usa la **Creazione guidata file di contenuto pre-installazione** per creare un file di contenuto pre-installazione compresso che contiene i file e i metadati associati per il contenuto selezionato.  

- Quindi, è possibile importare manualmente il contenuto in un server del sito, in un sito secondario o in un punto di distribuzione.  

- Quando si importa il file di contenuto pre-installato in un server del sito, i file di contenuto vengono aggiunti alla raccolta contenuto nel server del sito e quindi registrati nel database del server del sito.  

- Quando si importa il file di contenuto pre-installato in un punto di distribuzione, i file di contenuto vengono aggiunti alla raccolta contenuto nel punto di distribuzione e un messaggio di stato viene inviato al server del sito che informa il sito che il contenuto è disponibile nel punto di distribuzione.  

**Limitazioni e considerazioni sui contenuti pre-installazione:**  

- **Quando il punto di distribuzione si trova sul server del sito**, non abilitare il punto di distribuzione per il contenuto pre-installazione. Usare invece la procedura descritta in [How to prestage content on a distribution point on a site server](#bkmk_dpsiteserver) (Come pre-installare il contenuto in un punto di distribuzione in un server del sito).  

- **Quando il punto di distribuzione è configurato come un punto di distribuzione pull**, non abilitarlo per il contenuto pre-installazione. La configurazione del contenuto di pre-installazione per un punto di distribuzione sostituisce la configurazione del punto di distribuzione pull. Un punto di distribuzione pull che è configurato per contenuto pre-installato non esegue il pull del contenuto dal punto di distribuzione di origine e non riceve contenuto dal server del sito.  

- **È necessario creare la raccolta contenuto nel punto di distribuzione prima di poter pre-installare il contenuto in tale punto**. Distribuire il contenuto nella rete almeno una volta prima di pre-installarlo nel punto di distribuzione.  

- **Quando si pre-installa il contenuto per un pacchetto con un percorso di origine lungo** (ad esempio più di 140 caratteri), lo strumento della riga di comando Estrai contenuto potrebbe non riuscire a estrarre correttamente il contenuto per tale pacchetto nella raccolta contenuto.  

Per informazioni sugli scenari di pre-installazione dei file di contenuto, vedere *Prestaged content* (Contenuto preinstallazione) nell'argomento [Manage network bandwidth for content management](../../../plan-design/hierarchy/manage-network-bandwidth.md) (Gestire la larghezza di banda di rete per la gestione dei contenuti).  

Utilizzare le sezioni seguenti per pre-installare il contenuto.  

###  <a name="step-1-create-a-prestaged-content-file"></a><a name="BKMK_CreatePrestagedContentFile"></a> Passaggio 1: Creare un file di contenuti in versione di preproduzione  
È possibile creare un file di contenuto pre-installazione compresso contenente i file e i metadati associati per il contenuto selezionato nella console di Configuration Manager. Utilizzare la procedura seguente per creare un file di contenuto pre-installato.  

##### <a name="to-create-a-prestaged-content-file"></a>Per creare un file di contenuto pre-installato  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** selezionare uno dei seguenti passaggi per il tipo di contenuto che si desidera pre-installare:  

    - **Applicazioni**: espandere **Gestione applicazioni**, fare clic su **Applicazioni** e quindi selezionare le applicazioni da pre-installare.  

    - **Pacchetti**: espandere **Gestione applicazioni**, fare clic su **Pacchetti** e quindi selezionare i pacchetti da pre-installare.  

    - **Pacchetti driver**: espandere **Sistemi operativi**, fare clic su **Pacchetti driver** e quindi selezionare i pacchetti driver da pre-installare.  

    - **Immagini del sistema operativo**: espandere **Sistemi operativi**, fare clic su **Immagini del sistema operativo** e quindi selezionare le immagini del sistema operativo da pre-installare.  

    - **Programmi di installazione sistema operativo**: espandere **Sistemi operativi**, fare clic su **Programmi di installazione sistema operativo** e quindi selezionare i programmi di installazione del sistema operativo da pre-installare.  

    - **Immagini d'avvio**: espandere **Sistemi operativi**, fare clic su **Immagini d'avvio** e quindi selezionare le immagini d'avvio da pre-installare.  

    - **Sequenze di attività**: espandere **Sistemi operativi**, fare clic su **Sequenze di attività** e quindi selezionare la sequenza di attività da pre-installare.  

3.  Nella scheda **Home** del gruppo **Distribuzione** , fare clic su **Crea file di contenuto di pre-installazione**. Si aprirà la Creazione guidata file di contenuto pre-installazione.  

    > [!NOTE]  
    > **Per le applicazioni:** nella scheda **Home**, nel gruppo **Applicazione**, fare clic su **Crea file di contenuto di pre-installazione**.  
    >   
    > **Per i pacchetti:** nella scheda **Home**, nel gruppo &lt;*NomePacchetto*>, fare clic su **Crea file di contenuto di pre-installazione**.  

4.  Nella pagina **Generale** , fare clic su **Sfoglia**, scegliere il percorso per il file di contenuto pre-installato e specificare il relativo nome, quindi fare clic su **Salva**. È possibile utilizzare questo file di contenuto pre-installato su server di siti primari, server di siti secondari o punti di distribuzione per importare il contenuto e i metadati.  

5.  Per le applicazioni selezionare **Esporta tutte le dipendenze** affinché Configuration Manager rilevi e aggiunga le dipendenze associate all'applicazione al file di contenuto pre-installazione. Questa opzione è selezionata per impostazione predefinita.  

6.  In **Commenti amministratore**, immettere i commenti facoltativi sul file di contenuto pre-installato, quindi fare clic su **Avanti**.  

7.  Nella pagina **Contenuto** verificare che il contenuto in elenco corrisponda a quello che si desidera aggiungere al file di contenuto pre-installato, quindi fare clic su **Avanti**.  

8.  Nella pagina **Posizioni contenuto** specificare i punti di distribuzione dai quali recuperare i file di contenuto per il file di contenuto pre-installato. È possibile selezionare più di un punto di distribuzione per recuperare il contenuto. I punti di distribuzione sono elencati nella sezione Posizioni contenuto. Nella colonna **Contenuto** viene visualizzata la quantità di applicazioni o pacchetti selezionati disponibili in ogni punto di distribuzione. Configuration Manager inizia a recuperare il contenuto selezionato partendo dal primo punto di distribuzione nell'elenco e prosegue nell'elenco per recuperare il restante contenuto necessario per il file di contenuto pre-installazione. Fare clic su **Sposta su** o **Sposta giù** per modificare l'ordine di priorità dei punti di distribuzione. Quando i punti di distribuzione dell'elenco non contengono tutto il contenuto selezionato, è necessario aggiungere punti di distribuzione all'elenco che includano il contenuto oppure uscire dalla procedura guidata, distribuire il contenuto ad almeno un punto di distribuzione e quindi riavviare la procedura.  

9. Nella pagina **Riepilogo** confermare i dettagli. È possibile tornare alle pagine precedenti e apportare modifiche. Fare clic su **Avanti** per creare il file di contenuto pre-installato.  

10. Nella pagina **Avanzamento** viene visualizzato il contenuto che si sta aggiungendo al file di contenuto pre-installato.  

11. Nella pagina **Completamento** verificare che il file di contenuto pre-installato sia stato creato correttamente, quindi fare clic su **Chiudi**.  

###  <a name="step-2-assign-the-content-to-distribution-points"></a><a name="BKMK_AssignContentToDistributionPoint"></a> Passaggio 2: Assegnare i contenuti ai punti di distribuzione  
 Dopo aver pre-installato il file di contenuto, assegnare il contenuto ai punti di distribuzione.  

> [!NOTE]  
> Quando si utilizza un file di contenuto pre-installato per recuperare la raccolta contenuto su un server del sito, e non è necessario pre-installare i file di contenuto in un punto di distribuzione, è possibile ignorare questa procedura.  

 Utilizzare la procedura seguente per assegnare il contenuto nel file di contenuto pre-installato ai punti di distribuzione.  

> [!IMPORTANT]  
> Verificare che i punti di distribuzione da pre-installare siano configurati come punti di distribuzione di pre-installazione o che il contenuto venga distribuito ai punti di distribuzione usando la rete.  

##### <a name="to-assign-the-content-to-distribution-points"></a>Per assegnare il contenuto ai punti di distribuzione  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** selezionare uno dei seguenti passaggi per il tipo di contenuto selezionato al momento della creazione del file di contenuto pre-installato:  

    - **Applicazioni**: espandere **Gestione applicazioni**, fare clic su **Applicazioni** e quindi selezionare le applicazioni pre-installate.  

    - **Pacchetti**: espandere **Gestione applicazioni**, fare clic su **Pacchetti** e quindi selezionare i pacchetti pre-installati.  

    - **Pacchetti di distribuzione**: espandere **Aggiornamenti software**, fare clic su **Pacchetti di distribuzione** e quindi selezionare i pacchetti di distribuzione pre-installati.  

    - **Pacchetti driver**: espandere **Sistemi operativi**, fare clic su **Pacchetti driver** e quindi selezionare i pacchetti driver pre-installati.  

    - **Immagini del sistema operativo**: espandere **Sistemi operativi**, fare clic su **Immagini del sistema operativo** e quindi selezionare le immagini del sistema operativo pre-installate.  

    - **Programmi di installazione sistema operativo**: espandere **Sistemi operativi**, fare clic su **Programmi di installazione sistema operativo** e quindi selezionare i programmi di installazione del sistema operativo pre-installati.  

    - **Immagini d'avvio**: espandere **Sistemi operativi**, fare clic su **Immagini d'avvio** e quindi selezionare le immagini d'avvio pre-installate.  

3.  Nella scheda **Home** , nel gruppo **Distribuzione** , fare clic su **Distribuisci contenuto**. Viene visualizzata la Distribuzione guidata contenuto.  

4.  Nella pagina **Generale** verificare che il contenuto in elenco corrisponda al contenuto pre-installazione, scegliere se si vuole che Configuration Manager rilevi le dipendenze contenuto associate al contenuto selezionato e aggiunga le dipendenze alla distribuzione e fare clic su **Avanti**.  

    > [!NOTE]  
    > È presente l'opzione per configurare l'impostazione **Rileva le dipendenze contenuto associate e aggiungile alla distribuzione** solo per il tipo di contenuto dell'applicazione. Configuration Manager configura automaticamente questa impostazione per le sequenze di attività e l'impostazione non può essere modificata.  

5.  Nella pagina **Contenuto** , se visualizzata, verificare che il contenuto in elenco corrisponda a quello che si desidera distribuire, quindi fare clic su **Avanti**.  

    > [!NOTE]  
    > La pagina **Contenuto** viene visualizzata solo quando l'impostazione **Rileva le dipendenze contenuto associate e aggiungile alla distribuzione** viene selezionata nella pagina **Generale** della procedura guidata.  

6.  Nella pagina **Destinazione contenuto** fare clic su **Aggiungi**, scegliere uno dei seguenti elementi, che include i punti di distribuzione da pre-installare, quindi seguire il passaggio associato:  

    - **Raccolte**: selezionare **Raccolte utenti** o **Raccolte dispositivi**, fare clic sulla raccolta associata a uno o più gruppi di punti di distribuzione e quindi fare clic su **OK**.  

      > [!NOTE]  
      > Vengono visualizzate solo le raccolte associate a un gruppo di punti di distribuzione.  Per altre informazioni, vedere [Gestire i gruppi di punti di distribuzione](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage) nell'argomento [Installare e configurare punti di distribuzione per Configuration Manager](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md).  

    - **Punto di distribuzione**: selezionare un punto di distribuzione esistente e quindi fare clic su **OK**. Non vengono visualizzati i punti di distribuzione che hanno ricevuto il contenuto in precedenza.  

    - **Gruppo di punti di distribuzione**: selezionare un gruppo di punti di distribuzione esistente e quindi fare clic su **OK**. Non vengono visualizzati i gruppi di punti di distribuzione che hanno ricevuto il contenuto in precedenza.  

    Dopo aver aggiunto le destinazioni del contenuto, fare clic su **Avanti**.  

7.  Nella pagina **Riepilogo** , rivedere le impostazioni per la distribuzione prima di continuare. Per distribuire il contenuto nelle destinazioni selezionate, fare clic su **Avanti**.  

8.  La pagina **Avanzamento** visualizza l'avanzamento della distribuzione.  

9. La pagina **Conferma** visualizza se il contenuto è stato correttamente assegnato ai punti di distribuzione oppure no. Per monitorare la distribuzione del contenuto, vedere [Monitorare il contenuto distribuito con Configuration Manager](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md).  

###  <a name="step-3-extract-the-content-from-the-prestaged-content-file"></a><a name="BKMK_ExportContentFromPrestagedContentFile"></a> Passaggio 3: Estrarre i contenuti dal file dei contenuti in versione di preproduzione  
Dopo aver creato il file di contenuto pre-installazione e aver assegnato il contenuto ai punti di distribuzione, è possibile estrarre i file di contenuto nella raccolta contenuto nel server del sito o in un punto di distribuzione. In genere, il file di contenuti in versione di preproduzione viene copiato in un'unità portatile, ad esempio un'unità USB, oppure il contenuto viene masterizzato in un supporto, ad esempio un DVD, ed è disponibile nel percorso del server del sito o nel punto di distribuzione che richiede il contenuto.  

Utilizzare la procedura seguente per esportare manualmente i file di contenuto dal file di contenuto pre-installazione utilizzando lo strumento della riga di comando Estrai contenuto.  

> [!IMPORTANT]  
> Quando si esegue lo strumento della riga di comando Estrai contenuto, lo strumento crea un file temporaneo durante la creazione del file di contenuto pre-installazione. Quindi, il file viene copiato nella cartella di destinazione e il file temporaneo viene eliminato. È necessario disporre di spazio su disco sufficiente per il file temporaneo, altrimenti il processo non verrà completato. Il file temporaneo viene creato nel percorso seguente:  
>   
> - Il file temporaneo viene creato nella stessa cartella specificata come cartella di destinazione per il file di contenuti in versione di preproduzione.  

> [!IMPORTANT]  
> L'utente che esegue lo strumento della riga di comando Estrai contenuto deve essere in possesso dei diritti di **Amministratore** nel computer da cui viene estratto il contenuto pre-installazione.  

##### <a name="to-extract-the-content-files-from-the-prestaged-content-file"></a>Per estrarre i file di contenuto dal file di contenuto pre-installazione  

1.  Copiare il file di contenuto pre-installazione nel computer da cui si desidera estrarre il contenuto.  

2.  Copiare lo strumento della riga di comando Estrai contenuto da &lt;*PercorsoInstallazioneConfigMgr*>\bin\\&lt;*piattaforma*> nel computer dal quale si intende estrarre il file di contenuto pre-installazione.  

3.  Aprire il prompt dei comandi e cercare il percorso della cartella del file di contenuto pre-installazione e dello strumento Estrai contenuto.  

    > [!NOTE]  
    > È possibile estrarre uno o più file contenuto pre-installazione in un server del sito, un server del sito secondario o un punto di distribuzione.  

4.  Digitare **extractcontent /P:** &lt;*PercorsoFilePre-installazione*> **\\** &lt;*NomeFilePre-installazione*>  **/S** per importare un unico file.  

    Digitare **extractcontent /P:** &lt;*PercorsoFilePre-installazione*>  **/S** per importare tutti i file pre-installazione nella cartella specificata.  

    Ad esempio, digitare **extractcontent /P:D:\PrestagedFiles\MyPrestagedFile.pkgx /S** in cui `D:\PrestagedFiles\` è il PercorsoFilePre-installazione, `MyPrestagedFile.pkgx` è il nome del file pre-installazione e `/S` informa Configuration Manager di estrarre solo i file contenuto più recenti rispetto a quelli attualmente nel punto di distribuzione.  

    Quando si estrae il file di contenuto pre-installato in un server del sito, i file di contenuto vengono aggiunti alla raccolta contenuto nel server del sito e quindi la disponibilità del contenuto viene registrata nel database del server del sito. Quando si esporta il file di contenuto pre-installato in un punto di distribuzione, i file di contenuto vengono aggiunti alla raccolta contenuto nel punto di distribuzione, il punto di distribuzione invia un messaggio di stato al server del sito primario padre e quindi la disponibilità del contenuto viene registrata nel database del sito.  

    > [!IMPORTANT]  
    > Nello scenario seguente è necessario aggiornare il contenuto che è stato estratto da un file di contenuto pre-installato quando il contenuto viene aggiornato a una versione più recente:  
    >   
    >  1.  È possibile creare un file di contenuto pre-installazione per la versione 1 di un pacchetto.  
    >  2.  È possibile aggiornare i file di origine per il pacchetto con la versione 2.  
    >  3.  È possibile estrarre il file di contenuto pre-installazione (versione 1 del pacchetto) in un punto di distribuzione.  
    >   
    > Configuration Manager non distribuisce automaticamente il pacchetto versione 2 nel punto di distribuzione. È necessario creare un nuovo file di contenuto pre-installazione che contiene la nuova versione file e quindi estrarre il contenuto, aggiornare il punto di distribuzione per distribuire i file che sono stati modificati o ridistribuire tutti i file nel pacchetto.  

###  <a name="how-to-prestage-content-on-a-distribution-point-on-a-site-server"></a><a name="bkmk_dpsiteserver"></a> Come pre-installare il contenuto in un punto di distribuzione situato in un server del sito  
Quando viene installato un punto di distribuzione in un server del sito, è necessario utilizzare la seguente procedura per pre-installare correttamente il contenuto. Questa situazione si verifica perché i file di contenuto sono già nella raccolta contenuto.  

Quando il punto di distribuzione non è abilitato per la pre-installazione del contenuto o quando non si trova su un server del sito, vedere la sezione [Usare il contenuto pre-installazione](#bkmk_prestage) in questo argomento.  

##### <a name="to-prestage-content-on-distribution-points-located-on-a-site-server"></a>Per pre-installare il contenuto nei punti di distribuzione situati in un server del sito  

1.  Utilizzare la seguente procedura per verificare che il punto di distribuzione non sia abilitato per il contenuto pre-installato.  

    1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

    2.  Nell'area di lavoro **Amministrazione** fare clic su **Punti di distribuzione**, quindi selezionare il punto di distribuzione situato nel server del sito.  

    3.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

    4.  Nella scheda **Generale** verificare che la casella di controllo **Abilita questo punto di distribuzione per il contenuto pre-installato** non sia selezionata.  

2.  Creare il file dei contenuti in versione di preproduzione usando la sezione [Passaggio 1: Creare un file di contenuto pre-installato](#BKMK_CreatePrestagedContentFile) in questo argomento.  

3.  Assegnare il contenuto al punto di distribuzione usando la sezione [Passaggio 2: Assegnare il contenuto ai punti di distribuzione](#BKMK_AssignContentToDistributionPoint) in questo argomento.  

4.  Nel server del sito estrarre il contenuto dal file di contenuto pre-installato usando la sezione [Passaggio 3: Estrarre il contenuto dal file di contenuto pre-installazione](#BKMK_ExportContentFromPrestagedContentFile) in questo argomento.  

    > [!NOTE]  
    > Quando il punto di distribuzione si trova su un sito secondario, attendere almeno 10 minuti e assegnare il contenuto al punto di distribuzione nel sito secondario usando una console di Configuration Manager connessa al sito primario padre.  

##  <a name="manage-the-content-you-have-distributed"></a><a name="bkmk_manage"></a> Gestire il contenuto distribuito  
Per gestire il contenuto sono disponibili le opzioni seguenti:  
- [Aggiornare il contenuto](#update-content)
- [Ridistribuire il contenuto](#redistribute-content)
- [Rimuovere il contenuto](#remove-content)
- [Convalidare il contenuto](#validate-content)

### <a name="update-content"></a>Aggiornare il contenuto
Quando il percorso del file di origine per una distribuzione viene aggiornato aggiungendo nuovi file o sostituendo i file esistenti con una versione più recente, è possibile aggiornare i file di contenuto nei punti di distribuzione usando l'azione **Aggiorna punti di distribuzione** oppure **Aggiorna contenuto**:  
- I file di contenuto vengono copiati dal percorso del file di origine alla raccolta contenuto nel sito proprietario dell'origine contenuto del pacchetto  
- La versione del pacchetto viene incrementata  
- Ogni istanza della raccolta contenuto nei server del sito e nei punti di distribuzione viene aggiornata solo con i file che sono stati modificati  

> [!WARNING]  
> La versione pacchetto per le applicazioni è sempre 1. Quando si aggiorna il contenuto per un tipo di distribuzione applicazione, Configuration Manager crea un nuovo ID contenuto per il tipo di distribuzione e il pacchetto fa riferimento al nuovo ID contenuto.  

#### <a name="to-update-content-on-distribution-points"></a>Per aggiornare il contenuto nei punti di distribuzione  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** , selezionare uno dei seguenti passaggi per il tipo di contenuto che si desidera distribuire:  

    - **Applicazioni**: espandere **Gestione applicazioni** > **Applicazioni** e quindi selezionare le applicazioni da distribuire. Fare clic sulla scheda **Tipi di distribuzione** , quindi selezionare il tipo di distribuzione che si desidera aggiornare.  

    - **Pacchetti**: espandere **Gestione applicazioni** > **Pacchetti** e quindi selezionare i pacchetti da aggiornare.  

    - **Pacchetti di distribuzione**: espandere **Aggiornamenti software** > **Pacchetti di distribuzione** e quindi selezionare i pacchetti di distribuzione da aggiornare.  

    - **Pacchetti driver**: espandere **Sistemi operativi** > **Pacchetti driver** e quindi selezionare i pacchetti driver da aggiornare.  

    - **Immagini del sistema operativo**: espandere **Sistemi operativi** > **Immagini del sistema operativo** e quindi selezionare le immagini del sistema operativo da aggiornare.  

    - **Programmi di installazione sistema operativo**: espandere **Sistemi operativi** > **Programmi di installazione sistema operativo** e quindi selezionare i programmi di installazione del sistema operativo da aggiornare.  

    - **Immagini d'avvio**: espandere **Sistemi operativi** >  **Immagini d'avvio** e quindi selezionare le immagini di avvio da aggiornare.  

3.  Nella scheda **Home** , nel gruppo **Distribuzione** , fare clic su **Aggiorna punti di distribuzione**, quindi fare clic su **OK** per confermare che si desidera aggiornare il contenuto.  

    > [!NOTE]  
    > Per aggiornare il contenuto per applicazioni, fare clic sulla scheda **Tipi di distribuzione** , fare clic con il tasto destro del mouse sul tipo di distribuzione, fare clic su **Aggiorna contenuto**, quindi fare clic su **OK** per confermare che si desidera aggiornare il contenuto.  

    > [!NOTE]  
    > Quando si aggiorna il contenuto per immagini di avvio, verrà aperto la gestione guidata punti di distribuzione. Rivedere le informazioni sulla pagina **Riepilogo** , quindi completare la procedura guidata per aggiornare il contenuto.  

### <a name="redistribute-content"></a>Ridistribuire il contenuto
È possibile ridistribuire un pacchetto per copiare tutti i file di contenuto del pacchetto nei punti di distribuzione oppure nei gruppi di punti di distribuzione, sovrascrivendo quindi i file esistenti.  

Usare questa operazione per ripristinare i file di contenuto del pacchetto o per inviare di nuovo il contenuto quando la distribuzione iniziale non riesce. È possibile ridistribuire un pacchetto da:  

- Proprietà del pacchetto  
- Proprietà dei punti di distribuzione  
- Proprietà del gruppo di punti di distribuzione.  


#### <a name="to-redistribute-content-from-package-properties"></a>Per ridistribuire il contenuto dalle proprietà del pacchetto  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** , selezionare uno dei seguenti passaggi per il tipo di contenuto che si desidera distribuire:  

    - **Applicazioni**: espandere **Gestione applicazioni** >  **Applicazioni** e quindi selezionare l'applicazione da ridistribuire.  

    - **Pacchetti**: espandere **Gestione applicazioni** > **Pacchetti** e quindi selezionare il pacchetto da ridistribuire.  

    - **Pacchetti di distribuzione**: espandere **Aggiornamenti software** >  **Pacchetti di distribuzione** e quindi selezionare il pacchetto di distribuzione da ridistribuire.  

    - **Pacchetti driver**: espandere **Sistemi operativi** > **Pacchetti driver** e quindi selezionare il pacchetto driver da ridistribuire.  

    - **Immagini del sistema operativo**: espandere **Sistemi operativi** > **Immagini del sistema operativo** e quindi selezionare l'immagine del sistema operativo da ridistribuire.  

    - **Programmi di installazione sistema operativo**: espandere **Sistemi operativi** > **Programmi di installazione sistema operativo** e quindi selezionare il programma di installazione del sistema operativo da ridistribuire.  

    - **Immagini d'avvio**: espandere **Sistemi operativi** >  **Immagini d'avvio** e quindi selezionare l'immagine di avvio da ridistribuire.  

3.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

4.  Fare clic sulla scheda **Posizioni contenuto** , selezionare il punto di distribuzione o il gruppo di punti di distribuzione in cui si desidera ridistribuire il contenuto, fare clic su **Ridistribuisci**, quindi su **OK**.  

#### <a name="to-redistribute-content-from-distribution-point-properties"></a>Per ridistribuire il contenuto dalle proprietà del punto di distribuzione  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** fare clic su **Punti di distribuzione**e quindi selezionare il punto di distribuzione in cui si desidera ridistribuire il contenuto.  

3.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

4.  Fare clic sulla scheda **Contenuto** , selezionare il contenuto da ridistribuire, fare clic su **Ridistribuisci**, quindi su **OK**.  

#### <a name="to-redistribute-content-from-distribution-point-group-properties"></a>Per ridistribuire il contenuto dalle proprietà del gruppo di punti di distribuzione  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** fare clic su **Gruppi di punti di distribuzione**e quindi selezionare il gruppo di punti di distribuzione in cui si desidera ridistribuire il contenuto.  

3.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

4.  Fare clic sulla scheda **Contenuto** , selezionare il contenuto da ridistribuire, fare clic su **Ridistribuisci**, quindi su **OK**.  

    > [!IMPORTANT]  
    > Il contenuto del pacchetto viene ridistribuito a tutti i punti di distribuzione nel gruppo di punti di distribuzione.  


#### <a name="use-the-sdk-to-force-replication-of-content"></a>Usare l'SDK per forzare la replica del contenuto
È possibile usare il metodo **RetryContentReplication** della classe Strumentazione gestione Windows (WMI) dall'SDK di Configuration Manager per forzare la gestione della distribuzione a copiare il contenuto dal percorso di origine alla raccolta contenuto.  

Usare solo questo metodo per forzare la replica quando è necessario ridistribuire il contenuto dopo che si sono verificati problemi con la normale replica del contenuto, che in genere si verificano usando il nodo di monitoraggio della console.   

Per altre informazioni su questa opzione SDK, vedere [RetryContentReplication Method in Class SMS_CM_UpdatePackages](https://msdn.microsoft.com/library/mt762092(CMSDK.16).aspx) (Metodo RetryContentReplication Method nella classe SMS_CM_UpdatePackages) su MSDN.Microsoft.com.

### <a name="remove-content"></a>Rimuovere il contenuto
Quando non è più richiesto contenuto nei punti di distribuzione, è possibile rimuovere i file di contenuto nel punto di distribuzione.  

- Proprietà del pacchetto  
- Proprietà dei punti di distribuzione  
- Proprietà del gruppo di punti di distribuzione.  

Quando, tuttavia, il contenuto è associato a un altro pacchetto che è stato distribuito nello stesso punto di distribuzione, non è possibile rimuovere il contenuto.  

#### <a name="to-remove-package-content-files-from-distribution-points"></a>Per rimuovere i file di contenuto del pacchetto dai punti di distribuzione  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** selezionare uno dei seguenti passaggi per il tipo di contenuto che si desidera eliminare:  

    - **Applicazioni**: espandere **Gestione applicazioni** > **Applicazioni** e quindi selezionare l'applicazione da rimuovere.  

    - **Pacchetti**: espandere **Gestione applicazioni** > **Pacchetti** e quindi selezionare il pacchetto da rimuovere.  

    - **Pacchetti di distribuzione**: espandere **Aggiornamenti software** > **Pacchetti di distribuzione** e quindi selezionare il pacchetto di distribuzione da rimuovere.  

    - **Pacchetti driver**: espandere **Sistemi operativi** > **Pacchetti driver** e quindi selezionare il pacchetto driver da rimuovere.  

    - **Immagini del sistema operativo**: espandere **Sistemi operativi** > **Immagini del sistema operativo** e quindi selezionare l'immagine del sistema operativo da rimuovere.  

    - **Programmi di installazione sistema operativo**: espandere **Sistemi operativi** > **Programmi di installazione sistema operativo** e quindi selezionare il programma di installazione del sistema operativo da rimuovere.  

    - **Immagini d'avvio**: espandere **Sistemi operativi** > **Immagini d'avvio** e quindi selezionare l'immagine di avvio da rimuovere.  

3.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

4.  Fare clic sulla scheda **Posizioni contenuto** , selezionare il punto di distribuzione o il gruppo di punti di distribuzione da cui si desidera rimuovere il contenuto, fare clic su **Rimuovi**, quindi su **OK**.  

#### <a name="to-remove-package-content-from-distribution-point-properties"></a>Per rimuovere il contenuto del pacchetto dalle proprietà del punto di distribuzione  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** fare clic su **Punti di distribuzione**e quindi selezionare il punto di distribuzione da cui si desidera eliminare il contenuto.  

3.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

4.  Fare clic sulla scheda **Contenuto** , selezionare il contenuto da rimuovere, fare clic su **Rimuovi**, quindi su **OK**.  

#### <a name="to-remove-content-from-distribution-point-group-properties"></a>Per rimuovere il contenuto dalle proprietà del gruppo di punti di distribuzione  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** fare clic su **Gruppi di punti di distribuzione**e quindi selezionare il gruppo di punti di distribuzione da cui si desidera rimuovere il contenuto.  

3.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

4.  Fare clic sulla scheda **Contenuto** , selezionare il contenuto da rimuovere, fare clic su **Rimuovi**, quindi su **OK**.  


### <a name="validate-content"></a>Convalidare il contenuto
Il processo di convalida del contenuto consente di verificare l'integrità dei file nei punti di distribuzione. È possibile abilitare la convalida del contenuto in base a una pianificazione oppure è possibile avviare manualmente la convalida del contenuto dalle proprietà dei pacchetti e punti di distribuzione.  

Quando il processo di convalida del contenuto viene avviato, Configuration Manager verifica i file di contenuto nei punti di distribuzione e se l'hash del file non è previsto per i file nel punto di distribuzione crea un messaggio di stato che è possibile verificare nell'area di lavoro **Monitoraggio**.  

Per altre informazioni sulla configurazione della pianificazione di convalida del contenuto, vedere [Configurazioni dei punti di distribuzione](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs) nell'argomento [Installare e configurare punti di distribuzione per Configuration Manager](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md).  


#### <a name="to-initiate-content-validation-for-all-content-on-a-distribution-point"></a>Per avviare la convalida del contenuto per tutti i contenuti in un punto di distribuzione  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** fare clic su **Punti di distribuzione**e quindi selezionare il gruppo di punti di distribuzione in cui si desidera convalidare il contenuto.  

3.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

4.  Nella scheda **Contenuto** selezionare il pacchetto in cui si desidera convalidare il contenuto, fare clic su **Convalida**, quindi su **OK**e infine di nuovo su **OK**. Il processo di convalida contenuto viene avviato per il pacchetto nel punto di distribuzione.  

5.  Per visualizzare i risultati del processo di convalida contenuto, nell'area di lavoro **Monitoraggio** espandere **Stato distribuzione**e fare clic sul nodo **Stato contenuto** . Viene visualizzato il contenuto per ogni tipo di pacchetto (ad esempio, applicazione, pacchetto di aggiornamento software e immagine di avvio). Per altre informazioni sul monitoraggio dello stato del contenuto, vedere [Monitorare il contenuto distribuito con Configuration Manager](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md).  

#### <a name="to-initiate-content-validation-for-a-package"></a>Per avviare la convalida del contenuto per un pacchetto  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** selezionare uno dei seguenti passaggi per il tipo di contenuto che si desidera convalidare:  

    - **Applicazioni**: espandere **Gestione applicazioni** > **Applicazioni** e quindi selezionare l'applicazione da convalidare.  

    - **Pacchetti**: espandere **Gestione applicazioni** > **Pacchetti** e quindi selezionare il pacchetto da convalidare.  

    - **Pacchetti di distribuzione**: espandere **Aggiornamenti software** > **Pacchetti di distribuzione** e quindi selezionare il pacchetto di distribuzione da convalidare.  

    - **Pacchetti driver**: espandere **Sistemi operativi** > **Pacchetti driver** e quindi selezionare il pacchetto driver da convalidare.  

    - **Immagini del sistema operativo**: espandere **Sistemi operativi** > **Immagini del sistema operativo** e quindi selezionare l'immagine del sistema operativo da convalidare.  

    - **Programmi di installazione sistema operativo**: espandere **Sistemi operativi** >  **Programmi di installazione sistema operativo** e quindi selezionare il programma di installazione del sistema operativo da convalidare.  

    - **Immagini d'avvio**: espandere **Sistemi operativi** > **Immagini d'avvio** e quindi selezionare l'immagine di avvio da pre-installare.  

3.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

4.  Nella scheda **Percorsi contenuto** selezionare il punto di distribuzione o il gruppo di punti di distribuzione in cui si desidera convalidare il contenuto, fare clic su **Convalida**, quindi su **OK**e infine di nuovo su **OK**. Il processo di convalida contenuto viene avviato per il contenuto nel punto di distribuzione selezionato o nel gruppo di punti di distribuzione.  

5.  Per visualizzare i risultati del processo di convalida contenuto, nell'area di lavoro **Monitoraggio** espandere **Stato distribuzione**e fare clic sul nodo **Stato contenuto** . Viene visualizzato il contenuto per ogni tipo di pacchetto (ad esempio, applicazione, pacchetto di aggiornamento software e immagine di avvio). Per altre informazioni sul monitoraggio dello stato del contenuto, vedere [Monitorare il contenuto distribuito con Configuration Manager](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md).  
