---
title: Installazione guidata
titleSuffix: Configuration Manager
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1f703376-5f2c-4fd2-8209-7028c931ddc7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 22a70d2d1c779163d18e89e3ddb9b2371907ef56
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700369"
---
# <a name="use-the-setup-wizard-to-install-configuration-manager-sites"></a>Usare l'installazione guidata per installare i siti di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Per installare un nuovo sito di Configuration Manager tramite un'interfaccia utente guidata, usare l'installazione guidata di Configuration Manager (setup.exe). La procedura guidata supporta l'installazione di un sito primario o un sito di amministrazione centrale. È anche possibile usare la procedura guidata per [eseguire l'aggiornamento da un'installazione di valutazione](upgrade-an-evaluation-install-to-a-full-install.md) di Configuration Manager a un'installazione con licenza completa. Se non si vuole usare la procedura guidata, è possibile usare uno [script di installazione](use-a-command-line-to-install-sites.md) ed eseguire un'installazione automatica dalla riga di comando.

Installare un sito secondario dalla console di Configuration Manager. I siti secondari non supportano l'installazione con script dalla riga di comando.

> [!Note]  
> A partire dalla versione 1906, il file **splash.hta** non esiste più nella radice del supporto di installazione. Il file conteneva i collegamenti alle informazioni seguenti:<!--SCCMDocs-pr#3545-->
>
> - **Sito di installazione**: `smssetup\bin\x64\setup.exe`. Per altre informazioni, vedere [Installare un sito di amministrazione centrale o primario](#bkmk_primary).
> - **Prima di iniziare**: [Progettare una gerarchia di siti](../../../plan-design/hierarchy/design-a-hierarchy-of-sites.md) <!-- https://go.microsoft.com/fwlink/p/?LinkId=626543 -->
> - **Valutare la conformità dei server**: [Controllo prerequisiti](prerequisite-checker.md) <!-- https://go.microsoft.com/fwlink/p/?LinkId=626546 -->
> - **Scaricare i file di prerequisiti necessari**: `smssetup\bin\x64\setupdl.exe`. Per altre informazioni, vedere [Setup Downloader](setup-downloader.md) (Downloader di installazione).
> - **Installare la console di Configuration Manager**: `smssetup\bin\i386\consolesetup.exe`. Per altre informazioni, vedere [Installare le console](install-consoles.md).
> - [**Scaricare System Center Updates Publisher**](../../../../sum/tools/updates-publisher.md) <!-- https://go.microsoft.com/fwlink/p/?LinkId=626548 -->
> - **Scaricare client per altri sistemi operativi**: <!-- https://go.microsoft.com/fwlink/p/?LinkId=626550 -->
>   - [Microsoft Endpoint Configuration Manager - macOS Client (64-bit)](https://www.microsoft.com/download/details.aspx?id=100850)
>   - [Client per UNIX e Linux](https://www.microsoft.com/download/details.aspx?id=47719)
> - [**Note sulla versione**](release-notes.md) <!-- https://go.microsoft.com/fwlink/?LinkID=626571 -->
> - [**Leggere la documentazione**](https://docs.microsoft.com/sccm)<!-- https://go.microsoft.com/fwlink/p/?LinkId=626547 -->
> - **Ottenere assistenza per l'installazione**: [Forum TechNet: Configuration Manager (Current Branch) - Distribuzione del sito e del client](https://social.technet.microsoft.com/Forums/en-us/home?forum=ConfigMgrDeployment) <!--NOTE: this link requires en-us locale to work-->   <!-- https://go.microsoft.com/fwlink/p/?LinkId=626549 -->
> - **Community di Configuration Manager**: [Community di System Center: Come partecipare](https://social.technet.microsoft.com/wiki/contents/articles/11504.system-center-community-how-to-participate.aspx) <!-- https://go.microsoft.com/fwlink/p/?LinkId=626544 -->
> - [**Home page di Configuration Manager**](https://www.microsoft.com/cloud-platform/system-center-configuration-manager) <!-- https://go.microsoft.com/fwlink/p/?LinkId=626545 -->


## <a name="install-a-central-administration-or-primary-site"></a><a name="bkmk_primary"></a> Installare un sito di amministrazione centrale o primario

Usare la procedura seguente per installare un sito di amministrazione centrale o un sito primario. Usare questa procedura anche per eseguire l'aggiornamento di un sito di valutazione a un sito di Configuration Manager con licenza completa.

Prima di iniziare l'installazione del sito, è consigliabile acquisire familiarità con gli articoli seguenti:

- [Preparare l'installazione di siti](prepare-to-install-sites.md)
- [Prerequisiti per l'installazione di un sito](prerequisites-for-installing-sites.md)

Se si installa un sito di amministrazione centrale come parte di uno scenario di espansione del sito, vedere la sezione [Espandere un sito primario autonomo](use-the-setup-wizard-to-install-sites.md#bkmk_expand) prima di usare la procedura seguente.

### <a name="process-to-install-a-primary-or-central-administration-site"></a><a name="bkmk_installpri"></a> Processo di installazione di un sito primario o di amministrazione centrale

1. Nel computer in cui si vuole installare il sito, eseguire `<InstallationMedia>\SMSSETUP\BIN\X64\Setup.exe` per avviare l'**Installazione guidata di Configuration Manager**.  

    > [!NOTE]  
    > Quando si installa un sito di amministrazione centrale per espandere un sito primario autonomo o si installa un nuovo sito primario figlio in una gerarchia esistente, usare supporti di installazione (file di origine) corrispondenti alla versione del sito o dei siti esistenti. Se sono stati installati gli aggiornamenti nella console che hanno modificato la versione di siti installati in precedenza, non usare i supporti di installazione originale. Usare invece i file di origine dalla [cartella CD.Latest](../../manage/the-cd.latest-folder.md) di un sito aggiornato. Configuration Manager richiede l'uso di file di origine corrispondenti alla versione del sito esistente a cui si connetterà il nuovo sito.  

2. Nella pagina **Prima di iniziare** scegliere **Avanti**.  

3. Nella pagina **Riquadro attività iniziale** selezionare il tipo di sito che si vuole installare:  

    - **Sito di amministrazione centrale**, come primo sito di una nuova gerarchia o quando si espande un sito primario autonomo:  

        Selezionare **Installa un sito di amministrazione centrale di Configuration Manager**.  

        In un passaggio successivo di questa procedura, è possibile scegliere di installare un sito di amministrazione centrale come primo sito di una nuova gerarchia oppure installare un sito di amministrazione centrale per espandere un sito primario autonomo.  

    - **Sito primario**, come sito primario autonomo che è il primo sito di una nuova gerarchia o come sito primario figlio:  

        Selezionare **Installa un sito primario di Configuration Manager**.  

        > [!TIP]  
        > In genere, si seleziona l'opzione **Utilizza le opzioni di installazione tipiche per un sito primario autonomo** solo quando si vuole installare un sito primario autonomo in un ambiente di test. Quando si seleziona questa opzione, il programma di installazione esegue queste operazioni:  
        >
        > - Configura automaticamente il sito come sito primario autonomo.  
        > - Usa un percorso di installazione predefinito.  
        > - Usa un'installazione locale dell'istanza predefinita di SQL Server per il database del sito.  
        > - Installa un punto di gestione e un punto di distribuzione nel computer server del sito.  
        > - Configura il sito con la lingua inglese e con la lingua di visualizzazione del sistema operativo nel server del sito primario, se corrisponde a una delle lingue supportate da Configuration Manager.  

4. Nella pagina **Codice Product Key**:  

    - Scegliere se installare Configuration Manager come versione di valutazione o versione con licenza.  

        - Se si seleziona una versione con licenza, immettere il codice Product Key e fare clic su **Avanti**.  

        - Se si seleziona una versione di valutazione, fare clic su **Avanti**. È possibile eseguire successivamente l'aggiornamento di un'installazione di valutazione a un'installazione completa.  

    - È anche possibile specificare un valore per **Data di scadenza di Software Assurance** per il proprio contratto di licenza. Si tratta di un comodo promemoria per tale data. Se non si immette questa data durante l'installazione, è possibile specificarla in un secondo momento dalla console di Configuration Manager.  

        > [!NOTE]  
        > Microsoft non convalida la data di scadenza immessa e non usa tale data per la convalida della licenza. È possibile usarla come promemoria della data di scadenza. Questa data è utile perché Configuration Manager verifica periodicamente la disponibilità di nuovi aggiornamenti software online. Lo stato della licenza di Software Assurance deve essere valido per usufruire di tali aggiornamenti aggiuntivi.  

    Per altre informazioni, vedere [Licenze e rami](../../../understand/learn-more-editions.md).  

5. Nella pagina **Condizioni di licenza software Microsoft** leggere e accettare le condizioni di licenza.  

6. Nella pagina **Licenze prerequisite** leggere e accettare le condizioni di licenza per i prerequisiti software. Il programma di installazione scarica e installa automaticamente il software nei client o nei sistemi del sito quando è necessario. Prima di procedere alla pagina successiva, accettare tutte le condizioni.  

7. Nella pagina **Download prerequisiti** specificare se il programma di installazione deve scaricare da Internet i file ridistribuibili prerequisiti più recenti o se usare i file scaricati in precedenza:  

    - Se si vuole che il programma di installazione scarichi i file al momento dell'installazione, selezionare **Scarica file richiesti**. Specificare quindi un percorso in cui archiviare i file.  

    - Se i file sono stati scaricati in precedenza tramite il [downloader di installazione](setup-downloader.md), selezionare **Utilizza file scaricati precedentemente**. Specificare quindi la cartella di download.  

        > [!TIP]  
        > Se si usano i file scaricati in precedenza, verificare che il percorso alla cartella di download contenga la versione più recente dei file.  

8. Nella pagina **Selezione della lingua server** selezionare le lingue disponibili per la console di Configuration Manager e per i report. La lingua inglese è selezionata per impostazione predefinita e non può essere rimossa. Per altre informazioni, vedere [Language Pack](language-packs.md).  

9. Nella pagina **Selezione della lingua client** selezionare le lingue disponibili per i computer client. Specificare anche se si vuole abilitare tutte le lingue client per i client dei dispositivi mobili. La lingua inglese è selezionata per impostazione predefinita e non può essere rimossa.  

    > [!IMPORTANT]  
    > Quando si usa un sito di amministrazione centrale, assicurarsi che le lingue client configurate nel sito di amministrazione centrale includano tutte le lingue client configurate in ogni sito primario figlio. I client installati da un punto di distribuzione hanno accesso alle lingue client del sito di livello superiore, mentre i client installati da un punto di gestione hanno accesso alle lingue client del sito primario assegnato.  

10. Nella pagina **Impostazioni di installazione e del sito** specificare le impostazioni seguenti per il nuovo sito che si sta installando:  

    - **Codice del sito**: [Ogni codice del sito in una gerarchia deve essere univoco](prepare-to-install-sites.md#bkmk_sitecodes). Usare tre caratteri alfanumerici: da A a Z e da 0 a 9. Poiché il codice del sito viene usato nei nomi di cartella, non usare nomi riservati di Windows, ad esempio:  
        - AUX  
        - CON  
        - NUL  
        - PRN  
        - SMS  

        > [!NOTE]  
        > Il programma di installazione non verifica se il codice del sito specificato è già in uso o ha un nome riservato.  

    - **Nome sito**: ogni sito deve avere un nome descrittivo per poterlo facilmente individuare.  

    - **Cartella di installazione**: questa cartella indica il percorso di installazione di Configuration Manager. Non è possibile modificare il percorso dopo l'installazione del sito. Il percorso non può contenere spazi finali o caratteri Unicode.  

        > [!NOTE]  
        > Valutare se usare la cartella di installazione predefinita. Se si usa la partizione del sistema operativo predefinita in un ambiente di produzione, in futuro potrebbero verificarsi i problemi seguenti:  
        >
        > - Se Configuration Manager usa lo spazio su disco libero aggiuntivo nella partizione del sistema operativo, né Windows né Configuration Manager funzioneranno correttamente. Se si installa Configuration Manager in una partizione separata, l'utilizzo del disco non influirà sul sistema operativo.
        > - Le prestazioni di Configuration Manager sono migliori con un disco veloce. In alcune progettazioni di server la velocità del disco del sistema operativo non è ottimale.
        > - È possibile aggiornare, ripristinare o reinstallare il sistema operativo senza alcun impatto sull'installazione di Configuration Manager.  

11. Nella pagina **Installazione sito** usare l'opzione seguente che corrisponde allo scenario:  

    - **Installazione di un sito di amministrazione centrale:**  

        Nella pagina **Installazione del sito di amministrazione centrale** selezionare **Installa come primo sito in una nuova gerarchia** e quindi fare clic su **Avanti** per continuare.  

    - **Espansione di un sito primario autonomo in una gerarchia con un sito di amministrazione centrale:**  

        Nella pagina **Installazione del sito di amministrazione centrale** selezionare **Espandi un sito primario autonomo esistente in una gerarchia**. Specificare quindi il nome di dominio completo (FQDN) del server del sito primario autonomo e scegliere **Avanti** per continuare.  

        Il supporto usato per l'installazione del nuovo sito di amministrazione centrale deve corrispondere alla versione del sito primario.  

    - **Installazione di un sito primario autonomo:**  

        Nella pagina **Installazione del sito primario** selezionare **Installa il sito primario come sito autonomo** e quindi fare clic su **Avanti**.  

    - **Installazione di un sito primario figlio:**  

        Nella pagina **Installazione del sito primario** selezionare **Associa il sito primario a una gerarchia esistente**. Specificare quindi l'FQDN per il sito di amministrazione centrale e scegliere **Avanti**.  

12. Nella pagina **Informazioni database** specificare le informazioni seguenti:  

    - **Nome server SQL (FQDN)** : per impostazione predefinita, questo valore è impostato sul computer server del sito.  

        Se si usa una porta personalizzata, aggiungerla al nome FQDN di SQL Server. Dopo l'FQDN di SQL Server, aggiungere una virgola e quindi il numero di porta. Ad esempio, per il server *SQLServer1.fabrikam.com*, usare quanto segue per specificare la porta *1551*: `SQLServer1.fabrikam.com,1551`  

    - **Nome istanza**: per impostazione predefinita, questo valore è vuoto. Usa l'istanza predefinita di SQL nel computer server del sito.  

    - **Nome database**: Per impostazione predefinita, questo valore è impostato su `CM_<Sitecode>`. È possibile personalizzare tale valore.  

    - **Porta Service Broker:** : per impostazione predefinita, questo valore è impostato per usare la porta predefinita di SQL Server Service Broker (SSB) 4022. SQL la usa per comunicare direttamente con il database del sito in altri siti.  

13. Nella seconda pagina **Informazioni database** è possibile specificare percorsi personalizzati per il file di dati e il file di log di SQL Server per il database del sito:  

    - Per impostazione predefinita, vengono usati i percorsi file predefiniti per SQL Server.  

    - Quando si usa un cluster di SQL Server, l'opzione per specificare i percorsi file personalizzati non è disponibile.  

    - Il controllo dei prerequisiti non verifica lo spazio libero su disco per i percorsi file personalizzati.  

14. Nella pagina **Impostazioni del provider SMS** specificare il nome FQDN per il server in cui si vuole installare il provider SMS.  

    - Per impostazione predefinita, viene specificato il server del sito.  

    - Dopo l'installazione del sito, è possibile configurare altri provider SMS. Per altre informazioni, vedere [Piano per il provider SMS](../../../plan-design/hierarchy/plan-for-the-sms-provider.md).  

15. Nella pagina **Impostazioni di comunicazione client** scegliere se configurare tutti i sistemi del sito per l'accettazione esclusiva delle comunicazioni HTTPS dai client o per il metodo di comunicazione da configurare in ciascun ruolo del sistema del sito.  

    Quando si seleziona **Tutti i ruoli del sistema del sito accettano solo le comunicazioni HTTPS dai client**, il computer client deve avere un certificato PKI valido per l'autenticazione dei client. Per altre informazioni, vedere [requisiti dei certificati PKI](../../../plan-design/network/pki-certificate-requirements.md).  

    > [!NOTE]  
    > Questo passaggio si applica solo quando si installa un sito primario. Se si installa un sito di amministrazione centrale, ignorare questo passaggio.  

16. Nella pagina **Ruoli sistema del sito** scegliere se installare un punto di gestione o un punto di distribuzione. Per ogni ruolo che si è scelto di installare con il programma di installazione:  

    - Immettere il valore di **FQDN** per il server che ospiterà il ruolo. Scegliere quindi il metodo di connessione client che sarà supportato dal server: HTTP o HTTPS.  

    - Se nella pagina precedente è stata selezionata l'opzione **Tutti i ruoli del sistema del sito accettano solo le comunicazioni HTTPS dai client**, le impostazioni di connessione client vengono automaticamente configurate per HTTPS. Non è possibile modificare questa impostazione a meno di non tornare alla pagina precedente.  

    > [!NOTE]  
    > Questo passaggio si applica solo quando si installa un sito primario. Se si installa un sito di amministrazione centrale, ignorare questo passaggio.  

    > [!NOTE]  
    > Per installare i ruoli del sistema del sito, il programma di installazione usa l' **account di installazione del sistema del sito**. Per impostazione predefinita, quest'ultimo usa l'account computer del sito primario. Per installare il ruolo del sistema del sito, tale account deve corrispondere a un amministratore locale in un computer remoto. Se l'account non ha le autorizzazioni necessarie, deselezionare i ruoli del sistema del sito e installarli in un secondo momento dalla console di Configuration Manager, dopo aver configurato gli account aggiuntivi da usare come account di installazione del sistema del sito. Per altre informazioni, vedere [Account](../../../plan-design/hierarchy/accounts.md#site-system-installation-account).  

17. Nella pagina **Dati di utilizzo** rivedere le informazioni sui dati raccolti da Microsoft e quindi fare clic su **Avanti**. Per altre informazioni, vedere [Diagnostica e dati di utilizzo](../../../plan-design/diagnostics/diagnostics-and-usage-data.md).  

18. La pagina **Installazione del punto di connessione del servizio** è disponibile solo negli scenari seguenti:  

    - Quando si installa un sito primario autonomo.  

    - Quando si installa un sito di amministrazione centrale.  

    > [!NOTE]  
    > Se si sta eseguendo l'installazione di un sito primario figlio, ignorare questo passaggio.  

     Se si sta eseguendo l'installazione di un sito di amministrazione centrale come parte di uno scenario di espansione del sito e questo ruolo è già installato nel sito primario autonomo, è prima necessario disinstallare il ruolo dal sito primario autonomo. In una gerarchia è consentita solo un'istanza di questo ruolo, che è supportata solo nel sito di livello superiore della gerarchia.  

     Dopo aver selezionato una configurazione per il **punto di connessione del servizio** fare clic su **Avanti**. Al termine dell'installazione, è possibile modificare questa configurazione dalla console di Configuration Manager. Per altre informazioni, vedere [Informazioni sul punto di connessione del servizio](../configure/about-the-service-connection-point.md).  

19. Nella pagina **Riepilogo impostazioni** rivedere le impostazioni dell'aggiornamento selezionate. Quando si è pronti, scegliere **Avanti** per avviare il controllo dei prerequisiti.  

20. Nella pagina **Controllo prerequisiti dell'installazione** sono elencati i problemi identificati.  

    - Quando il controllo dei prerequisiti rileva un problema, fare clic su un elemento nell'elenco per informazioni dettagliate su come risolverlo.  

    - Prima di continuare a installare il sito, risolvere gli elementi con stato **Errore**. Provare anche a risolvere gli elementi con stato **Avviso**, che tuttavia non bloccano l'installazione del sito.  

    - Dopo la risoluzione dei problemi fare clic su **Esegui controllo** per eseguire nuovamente il controllo dei prerequisiti.  

        Se si esegue il controllo dei prerequisiti e a nessun controllo viene assegnato lo stato **Errore**, è possibile fare clic su **Inizia installazione** per avviare l'installazione del sito.  

    > [!TIP]  
    > Oltre al feedback fornito dalla procedura guidata, è possibile trovare altre informazioni sui problemi relativi ai prerequisiti nel file **ConfigMgrPrereq.log**. Tale file si trova nella radice dell'unità di sistema del computer in cui si sta installando il sito. Per altre informazioni, vedere [Elenco dei controlli dei prerequisiti](list-of-prerequisite-checks.md).  

21. Nella pagina **Installazione** viene visualizzato lo stato dell'installazione. Dopo aver completato l'installazione del server del sito principale, è possibile scegliere **Chiudi** per chiudere l'installazione guidata. Dopo aver chiuso la procedura guidata, l'installazione e la configurazione iniziale del sito continuano in background.  

    - È possibile connettere una console di Configuration Manager al sito prima del completamento dell'installazione. Questa console si connette in sola lettura e consente di visualizzare oggetti e impostazioni, ma non di apportare modifiche.  

    - Al termine dell'installazione, sarà possibile connettere una console che consente di modificare oggetti e impostazioni.  


## <a name="expand-a-stand-alone-primary-site"></a><a name="bkmk_expand"></a> Espandere un sito primario autonomo

Dopo aver installato un sito primario autonomo come primo sito, è possibile successivamente espanderlo in una gerarchia più ampia installando un sito di amministrazione centrale.

Quando si espande un sito primario autonomo, si installa un nuovo sito di amministrazione centrale che usa il database del sito primario autonomo esistente come riferimento. Dopo l'installazione del nuovo sito di amministrazione centrale, il sito primario autonomo agisce da sito primario figlio.

- È possibile espandere un sito primario autonomo solo in una nuova gerarchia.  

- È possibile espandere un solo sito primario autonomo in una gerarchia specifica. Non è possibile usare questa opzione per aggiungere altri siti primari autonomi nella stessa gerarchia. Usare invece la migrazione guidata per migrare i dati da una gerarchia a un'altra. Per altre informazioni, vedere [Eseguire la migrazione dei dati da una gerarchia all'altra](../../../migration/migrate-data-between-hierarchies.md).  

- In seguito all'espansione di un sito primario autonomo in una gerarchia con un sito di amministrazione centrale, è possibile aggiungere altri siti primari figlio.  

- Per rimuovere un sito primario da una gerarchia con un sito di amministrazione centrale, è prima necessario disinstallare il sito primario.  

Per espandere il sito, usare l'installazione guidata di Configuration Manager per installare un nuovo sito di amministrazione centrale in base alle indicazioni seguenti:  

- Installare il sito di amministrazione centrale usando la stessa versione di Configuration Manager del sito primario autonomo.  

- Nella pagina **Introduzione** dell'installazione guidata selezionare l'opzione per installare un sito di amministrazione centrale. In una fase successiva dell'installazione, scegliere un'opzione per espandere un sito primario autonomo esistente.  

- Quando si configura la pagina **Selezione della lingua client** per il nuovo sito di amministrazione centrale, selezionare le stesse lingue client configurate per il sito primario autonomo che si vuole espandere.  

- Nella pagina **Installazione sito** selezionare l'opzione per espandere il sito primario autonomo.  

Per espandere un sito primario autonomo, vedere prima i [prerequisiti per l'espansione di un sito primario autonomo](prerequisites-for-installing-sites.md#bkmk_expand). Usare quindi la procedura descritta nella sezione [Processo di installazione di un sito primario o di amministrazione centrale](use-the-setup-wizard-to-install-sites.md#bkmk_installpri) in precedenza in questo articolo.


## <a name="install-a-secondary-site"></a><a name="bkmk_secondary"></a> Installare un sito secondario

Usare la console di Configuration Manager per installare un sito secondario.  

- Se la console in uso non è connessa al sito primario che sarà il sito padre del nuovo sito secondario, il comando per installare il sito verrà replicato nel sito primario corretto.  

- Prima di avviare l'installazione del sito, assicurarsi che l'account utente abbia le autorizzazioni richieste dai prerequisiti. Assicurarsi anche che il server che ospiterà il nuovo sito secondario soddisfi tutti i prerequisiti per l'uso come server del sito secondario.  

- Quando si installa il sito secondario, Configuration Manager configura il nuovo sito per l'uso delle porte di comunicazione del client configurate nel sito primario padre.  

### <a name="process-to-install-a-secondary-site"></a><a name="bkmk_installsecondary"></a> Processo per installare un sito secondario  

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito** e selezionare **Siti**. Selezionare il sito che sarà il sito primario padre del nuovo sito secondario.  

2. Per avviare la **Creazione guidata sito secondario**, scegliere **Crea sito secondario** sulla barra multifunzione.  

3. Nella pagina **Prima di iniziare** verificare che il sito primario elencato sia quello che si vuole impostare come padre del nuovo sito secondario. Scegliere quindi **Avanti**.  

4. Nella pagina **Generale** specificare le impostazioni seguenti:  

    - **Codice del sito**: Ogni codice del sito in una gerarchia deve essere univoco. Usare tre caratteri alfanumerici: da A a Z e da 0 a 9. Poiché il codice del sito viene usato nei nomi di cartella, non usare nomi riservati di Windows, ad esempio:  

        - AUX  
        - CON  
        - NUL  
        - PRN  
        - SMS  

    > [!NOTE]  
    > Il programma di installazione non verifica se il codice del sito specificato è già in uso o ha un nome riservato.  

    - **Nome server sito**: questo valore è il nome di dominio completo (FQDN) del server in cui verrà installato il nuovo sito secondario.  

    - **Nome sito**: ogni sito deve avere un nome descrittivo per poterlo facilmente individuare.  

    - **Cartella di installazione**: questa cartella indica il percorso di installazione di Configuration Manager. Non è possibile modificare il percorso dopo l'installazione del sito. Il percorso non può contenere spazi finali o caratteri Unicode.  

    > [!IMPORTANT]  
    > Dopo aver specificato i dettagli in questa pagina, è possibile scegliere **Riepilogo** per passare direttamente alla pagina **Riepilogo** della procedura guidata. In questo modo, verranno usate le impostazioni predefinite per il resto delle opzioni del sito secondario.  
    > 
    > - Usare questa opzione solo se si ha familiarità con le impostazioni predefinite della procedura guidata e si vogliono usare tali impostazioni.  
    > - Quando si usano le impostazioni predefinite, i gruppi di limiti non sono associati al punto di distribuzione. Fino a quando non si configurano gruppi di limiti che includono il server del sito secondario, i client non useranno il punto di distribuzione installato in questo sito secondario come percorso di origine del contenuto.  

5. Nella pagina **File di origine dell'installazione** scegliere la modalità usata dal computer del sito secondario per ottenere i file di origine per l'installazione del sito.  

    Quando si usano i file di origine di CD.Latest condivisi in rete o copiati in locale nel server del sito secondario di destinazione:  

    - **Versione 1802 e precedenti**

        - Il percorso dei file di origine di CD.Latest include una cartella denominata **Redist**. Spostare questa cartella **Redist** come sottocartella di **SMSSETUP**.  

            > [!Note]  
            > Se si verificano errori di mancata corrispondenza di hash durante l'installazione, aggiornare la cartella **Redist**. Usare il [downloader di installazione](setup-downloader.md) per ottenere i file più recenti. Copiare inoltre tutti i file che causano un errore di mancata corrispondenza di hash dalla cartella **Redist** aggiornata alla cartella **SMSSETUP\BIN\X64**.

    - **Versione 1806 e successive**<!-- SCCMDocs-pr issue 3164 -->

        - Il percorso dei file di origine di CD.Latest include una cartella denominata **Redist**. Spostare questa cartella **Redist** come sottocartella di **SMSSETUP**.  

        - Copiare i file seguenti dalla cartella **Redist** alla cartella **SMSSETUP\BIN\X64**:  
            - SharedManagementObjects.msi
            - SQLSysClrTypes.msi
            - sqlncli.msi

    - Se i file della cartella **Redist** non sono disponibili, l'installazione del sito secondario avrà esito negativo.  

    - L'account computer del server del sito secondario deve avere le autorizzazioni di **lettura** per la condivisione e la cartella dei file di origine.  

6. Nella pagina **Impostazioni di SQL Server** specificare la versione di SQL Server da usare e quindi configurare le impostazioni correlate.  

    > [!NOTE]  
    > Il programma di installazione non convalida le informazioni immesse in questa pagina fino all'avvio dell'installazione. Prima di continuare, verificare queste impostazioni.  

    - **Installa e configura una copia locale di SQL Express nel computer del sito secondario**  

        - **Porta del servizio di SQL Server**: specificare la porta del servizio di SQL Server usata da SQL Server Express. La porta del servizio è in genere configurata per l'utilizzo della porta TCP 1433, ma è possibile configurare un'altra porta.  

        - **Porta di SQL Server Service Broker**: specificare la porta di SQL Server Service Broker (SSB) usata da SQL Server Express. La porta di Service Broker è in genere configurata per l'utilizzo della porta TCP 4022, ma è possibile configurare un'altra porta. Specificare una porta valida che non sia usata da nessun altro sito o servizio e che non sia soggetta ad alcuna restrizione del firewall.  

    - **Usa un'istanza di SQL Server esistente**  

        - **FQDN di SQL Server**: rivedere il nome FQDN del computer SQL Server. È necessario usare un server locale che esegue SQL Server per ospitare il database del sito secondario. Non è possibile modificare questa impostazione.  

        - **Istanza SQL Server**: specificare l'istanza di SQL Server da usare come database del sito secondario. Lasciare vuota questa opzione per usare l'istanza predefinita.  

        - **Nome database del sito di Configuration Manager**: specificare il nome da usare per il database del sito secondario.  

        - **Porta di SQL Server Service Broker**: specificare la porta di SQL Server Service Broker (SSB) usata da SQL Server. Specificare una porta valida che non sia usata da nessun altro sito o servizio e che non sia soggetta ad alcuna restrizione del firewall.  

    > [!TIP]  
    > Per un elenco delle versioni di SQL Server supportate da Configuration Manager, vedere [Versioni di SQL Server supportate](../../../plan-design/configs/support-for-sql-server-versions.md).  

7. Nella pagina **Punto di distribuzione** configurare le impostazioni per il punto di distribuzione che verranno installate sul server del sito secondario.  

    - **Impostazioni obbligatorie:**  

        - **Specificare la modalità di comunicazione dei dispositivi client con il punto di distribuzione**: scegliere HTTP o HTTPS.  

        - **Creare un certificato autofirmato o importare un certificato client PKI**: Scegliere se usare un certificato autofirmato o importare un certificato dall'infrastruttura a chiave pubblica (PKI). L'uso di un certificato autofirmato consente anche le connessioni anonime dai client di Configuration Manager alla raccolta contenuto. Il certificato viene usato per l'autenticazione tra il punto di distribuzione e un punto di gestione prima che il punto di distribuzione invii messaggi di stato. Per altre informazioni, vedere [requisiti dei certificati PKI](../../../plan-design/network/pki-certificate-requirements.md).  

    - **Impostazioni facoltative:**  

        - **Installa e configura IIS, se richiesto da Configuration Manager**: selezionare questa impostazione per fare in modo che Configuration Manager installi e configuri Internet Information Services (IIS) nel server, se non è già installato. IIS è necessario in tutti i punti di distribuzione.  

            > [!NOTE]  
            > Anche se questa impostazione è facoltativa, è necessario installare IIS nel server prima di poter installare un punto di distribuzione.  

        - **Abilita e configura BranchCache per questo punto di distribuzione**  

        - **Descrizione**: questo valore rappresenta una descrizione del punto di distribuzione, che aiuta a individuarlo.  

        - **Abilita questo punto di distribuzione per il contenuto pre-installato**  

8. Nella pagina **Impostazioni unità** specificare le impostazioni unità per il punto di distribuzione del sito secondario.  

    È possibile configurare fino a due unità disco per la raccolta contenuto e due unità disco per la condivisione dei pacchetti. Configuration Manager può usare unità aggiuntive nel caso in cui le prime due raggiungano il limite di spazio riservato nell'unità configurata. Nella pagina **Impostazioni unità** è possibile configurare la priorità per le unità disco e la quantità di spazio disponibile su disco da mantenere su ogni unità disco.  

    - **Spazio riservato nell'unità (MB)** : il valore configurato per questa impostazione determina la quantità di spazio disponibile in un'unità prima che Configuration Manager scelga un'altra unità e continui il processo di copia su tale unità. I file di contenuto possono estendersi su più unità.  

    - **Percorsi contenuto**: specificare i percorsi del contenuto per la condivisione di pacchetti e raccolte di contenuti. Configuration Manager copia i contenuti nel percorso del contenuto principale finché la quantità di spazio libero non raggiunge il valore specificato per **Spazio riservato nell'unità (MB)** .  

    Per impostazione predefinita, i percorsi contenuto sono impostati su **Automatico**. Il percorso del contenuto primario è impostato sull'unità disco con più spazio al momento dell'installazione. Il percorso secondario viene impostato per l'unità disco con lo spazio libero maggiore dopo l'unità principale. Quando le unità primaria e secondaria raggiungono il limite di spazio riservato, Configuration Manager seleziona un'altra unità disponibile con la maggiore quantità di spazio libero e continua il processo di copia.  

9. Nella pagina **Convalida contenuto** specificare se convalidare l'integrità dei file di contenuto nel punto di distribuzione.  

    - Quando si abilita la convalida del contenuto in base a una pianificazione, Configuration Manager avvia il processo all'orario pianificato Tutto il contenuto nel punto di distribuzione viene verificato.  

    - È anche possibile configurare la **priorità di convalida del contenuto**.  

    - Per visualizzare i risultati del processo di convalida del contenuto, nella console di Configuration Manager passare all'area di lavoro **Monitoraggio**, espandere **Stato distribuzione** e selezionare il nodo **Stato contenuto**. Verrà visualizzato il contenuto per ogni tipo di pacchetto. Questi tipi includono applicazioni, pacchetti di aggiornamento software e immagini di avvio.  

10. Nella pagina **Gruppi limite** gestire i gruppi di limiti ai quali viene assegnato questo punto di distribuzione:  

    - Durante la distribuzione del contenuto, i client devono trovarsi in un gruppo di limiti associato al punto di distribuzione per usarlo come percorso di origine per il contenuto.  

    - È possibile selezionare l'opzione **Consenti percorso origine di fallback per il contenuto** per consentire ai client al di fuori di questi gruppi di limiti di eseguire il fallback e usare il punto di distribuzione come un percorso di origine quando i punti di distribuzione preferiti non sono disponibili.  

        Per altre informazioni, vedere [Concetti di base per la gestione dei contenuti ](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

11. Nella pagina **Riepilogo** verificare le impostazioni, quindi fare clic su **Avanti** per installare il sito secondario. Quando la procedura guidata visualizza la pagina **Completamento**, è possibile chiudere la procedura guidata. L'installazione del sito secondario continua in background.  

### <a name="how-to-verify-the-secondary-site-installation-status"></a><a name="bkmk_verify"></a> Come verificare lo stato di installazione del sito secondario  

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito** e selezionare **Siti**.  

2. Selezionare il sito secondario che si sta installando e quindi scegliere **Mostra stato installazione** sulla barra multifunzione.  

    > [!TIP]  
    > Quando si installano più siti secondari simultaneamente, il controllo dei prerequisiti viene eseguito su un sito alla volta. Il controllo deve venire completato prima di passare al sito successivo.  
