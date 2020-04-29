---
title: Disponibilità elevata del server del sito
titleSuffix: Configuration Manager
description: Come configurare la disponibilità elevata per il server del sito di Configuration Manager aggiungendo un server del sito in modalità passiva.
ms.date: 02/07/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6dcef836-c0d1-40af-ad30-cd8d864b09a9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 395504f5ccc3635f580bca739f1c4b7273861123
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700899"
---
# <a name="site-server-high-availability-in-configuration-manager"></a>Disponibilità elevata del server del sito in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

<!--1128774-->

In passato, era possibile aggiungere ridondanza per la maggior parte dei ruoli in Configuration Manager definendo più istanze di questi ruoli nell'ambiente in uso. Fatta eccezione per il server del sito stesso. La disponibilità elevata per il ruolo del server del sito è una soluzione di base di Configuration Manager per installare un server del sito aggiuntivo in modalità *passiva*. I siti di amministrazione centrale e i siti primari figlio ora possono avere un altro server del sito in modalità passiva. Il server del sito in modalità passiva può essere locale o basato sul cloud in Azure.

Questa funzionalità offre i vantaggi seguenti

- Ridondanza e disponibilità elevata per il ruolo del server del sito  
- Modificare più facilmente l'hardware o il sistema operativo del server del sito  
- Spostare più facilmente il server del sito in un'infrastruttura IaaS di Azure  

Il server del sito in modalità passiva è un'aggiunta al server del sito primario esistente in modalità *attiva*. Un server del sito in modalità passiva è disponibile per l'uso immediato, quando necessario. Includere questo server del sito aggiuntivo come parte della progettazione complessiva per rendere il servizio Configuration Manager a [disponibilità elevata](high-availability-options.md).  

Un server del sito in modalità passiva:

- Usa lo stesso database del sito usato dal server del sito in modalità attiva.
- Non scrive dati nel database del sito quando si trova in modalità passiva.
- Usa la stessa raccolta contenuto usata dal server del sito in modalità attiva.

Per far diventare attivo il server del sito in modalità passiva, lo si *alza di livello* manualmente. Questa azione fa passare il server del sito dalla modalità passiva alla modalità attiva. I ruoli del sistema del sito che sono disponibili nel server in modalità Attivo originale rimangono disponibili fin a quando tale computer è accessibile. Solo il ruolo del server del sito viene commutato tra le modalità attiva e passiva.

Questa funzionalità è stata usata da Microsoft Core Services Engineering and Operations per eseguire la migrazione del sito di amministrazione a Microsoft Azure. Per altre informazioni, vedere l'[articolo di Microsoft IT Showcase](https://www.microsoft.com/itshowcase/Article/Content/1065/Migrating-System-Center-Configuration-Manager-onpremises-infrastructure-to-Microsoft-Azure).

## <a name="prerequisites"></a>Prerequisiti

- La raccolta contenuto del sito deve essere in una condivisione di rete remota. Entrambi i server del sito necessitano di autorizzazioni di controllo completo per la condivisione e i relativi contenuti. Per altre informazioni, vedere [Gestire la raccolta contenuto](../../../plan-design/hierarchy/the-content-library.md#bkmk_remote).<!--1357525-->  

  - L'account computer del server del sito deve avere le autorizzazioni **Controllo completo** per il percorso di rete in cui deve essere spostata la raccolta contenuto. Questa autorizzazione è applicabile sia alla condivisione che al file system. Non sono installati componenti nel sistema remoto.

  - Il server del sito non può avere il ruolo di punto di distribuzione. Il punto di distribuzione usa anche la raccolta contenuto e questo ruolo non supporta una raccolta contenuto remota. Dopo aver spostato la raccolta contenuto, non è possibile aggiungere il ruolo di punto di distribuzione al server del sito.  

- Il server del sito in modalità passiva può essere locale o basato sul cloud in Azure.  

    > [!NOTE]
    > Un server del sito basato sul cloud in modalità passiva usa l'infrastruttura distribuita come servizio (IaaS) di Azure. Per altre informazioni, vedere gli articoli seguenti:
    >
    >   - [Macchine virtuali di Azure (per l'infrastruttura basata sul cloud)](../../../understand/use-cloud-services.md#azure-virtual-machines-for-cloud-based-infrastructure)
    >   - [Domande frequenti su Configuration Manager in Azure](../../../understand/configuration-manager-on-azure.md)  

- Entrambi i server del sito devono appartenere allo stesso dominio di Active Directory.  

- Configuration Manager supporta i server del sito in modalità passiva in una gerarchia. I siti di amministrazione centrale e i siti primari figlio ora possono avere un altro server del sito in modalità passiva.<!-- 3607755 -->  

- Entrambi i server del sito devono usare lo stesso database del sito.  

  - Il database può essere remoto rispetto a ogni server del sito. A partire dalla versione 1810, il programma di installazione di Configuration Manager non blocca più l'installazione del ruolo del server del sito in un computer con il ruolo Windows per il clustering di failover. Poiché SQL Always On richiede questo ruolo, non era possibile in precedenza inserire il database del sito nel server del sito. Con questa modifica, è possibile creare un sito a disponibilità elevata con un minor numero di server usando SQL Always On e un server del sito in modalità passiva.<!-- SCCMDocs issue 1074 -->  

  - L'istanza di SQL Server che ospita il database del sito può usare un'istanza predefinita, un'istanza denominata, un [cluster di SQL Server](use-a-sql-server-cluster-for-the-site-database.md) o un [gruppo di disponibilità Always On di SQL Server](sql-server-alwayson-for-a-highly-available-site-database.md).  

  - Entrambi i server del sito richiedono il ruolo di sicurezza **sysadmin** nell'istanza di SQL Server che ospita il database del sito. Il server del sito originale deve avere già questi ruoli, quindi aggiungerli per il nuovo server del sito. Ad esempio, lo script SQL seguente consente di aggiungere i ruoli seguenti per il nuovo server del sito **VM2** nel dominio Contoso:  

    ```SQL
    USE [master]
    GO
    CREATE LOGIN [contoso\vm2$] FROM WINDOWS WITH DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[us_english]
    GO
    ALTER SERVER ROLE [sysadmin] ADD MEMBER [contoso\vm2$]
    GO
    ```

  - Entrambi i server del sito devono avere accesso al database del sito nell'istanza di SQL Server. Il server del sito originale deve avere già questo accesso, quindi aggiungerlo per il nuovo server del sito. Ad esempio, lo script SQL seguente aggiunge un account di accesso al database **CM_ABC** per il nuovo server del sito **VM2** nel dominio Contoso:  

    ```SQL
    USE [CM_ABC]
    GO
    CREATE USER [contoso\vm2$] FOR LOGIN [contoso\vm2$] WITH DEFAULT_SCHEMA=[dbo]
    GO
    ```

  - Il server del sito in modalità passiva è configurato per usare lo stesso database del sito del server del sito in modalità attiva. Il server del sito in modalità passiva legge solo dal database. Non scrive nel database finché non viene alzato di livello alla modalità attiva.  

- Il server del sito in modalità passiva:  

  - Deve soddisfare i prerequisiti per l'installazione di un sito primario. Ad esempio, .NET Framework, la compressione differenziale remota e Windows ADK. Per l'elenco completo, vedere [Prerequisiti del sito e del sistema del sito](../../../plan-design/configs/site-and-site-system-prerequisites.md).<!-- SCCMDocs issue 765 -->  

    > [!NOTE]
    > Assicurarsi di installare SQL Server Native Client. Se non viene installato, il controllo prerequisiti durante l'installazione di Configuration Manager segnala un errore relativo alle autorizzazioni di SQL Server mancanti.<!-- SCCMDocs#2290 -->

  - Deve avere l'account computer nel gruppo di amministratori locale nel server del sito in modalità attiva.<!--516036-->

  - Deve eseguire l'installazione usando file di origine che corrispondono alla versione del server del sito in modalità attiva.  

  - Non può avere un ruolo del sistema del sito da qualsiasi sito installato nel server prima di installare il ruolo di server del sito in modalità passiva.  

- Entrambi i server del sito possono eseguire versioni diverse del sistema operativo o del Service Pack, purché entrambe siano [supportate da Configuration Manager](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md).  

- Non ospitare il ruolo punto di connessione del servizio nel server del sito configurato per la disponibilità elevata. Se è attualmente nel server del sito originale, rimuoverlo e installarlo in un altro server del sistema del sito. Per altre informazioni, vedere [Informazioni sul punto di connessione del servizio](about-the-service-connection-point.md).  

- Autorizzazioni per l'[account di installazione sistema del sito](../../../plan-design/hierarchy/accounts.md#site-system-installation-account)  

  - Per impostazione predefinita, molti clienti usano l'account computer del server del sito per installare nuovi sistemi del sito. Il requisito consiste quindi nell'aggiungere l'account computer del server del sito al gruppo **Amministratori** locale nel sistema del sito remoto. Se l'ambiente usa questa configurazione, assicurarsi di aggiungere l'account computer del nuovo server del sito a questo gruppo locale in tutti i sistemi del sito remoti. Ad esempio, tutti i punti di distribuzione remoti.  

  - La configurazione più sicura e consigliata consiste nell'usare un account del servizio per l'installazione del sistema del sito. La configurazione più sicura consiste nell'usare un account del servizio locale. Se l'ambiente usa questa configurazione, non è necessaria alcuna modifica.  

## <a name="limitations"></a>Limitazioni

- Ogni sito supporta un singolo server del sito in modalità passiva.  

- Un server del sito in modalità passiva non è supportato in un sito secondario.<!--SCCMDocs issue 680-->  

    > [!NOTE]  
    > I siti secondari sono ancora supportati in un sito primario con server del sito a disponibilità elevata.

- L'innalzamento di livello del server del sito in modalità passiva alla modalità attiva è manuale. Non si verificano failover automatici.  

- Non si possono installare ruoli del sistema del sito nel nuovo server prima di aggiungere il server del sito in modalità passiva.  

    > [!NOTE]
    > Dopo l'installazione del server del sito in modalità passiva, è possibile aggiungere altri ruoli in base alle esigenze, ad esempio un punto di gestione in un sito primario.

- Per ruoli come il punto di reporting, che usano un database, ospitare il database in un server remoto rispetto a entrambi i server del sito.  

- La console di Configuration Manager non viene installata automaticamente nel server del sito in modalità passiva.  

## <a name="add-a-site-server-in-passive-mode"></a>Aggiungere un server del sito in modalità Passivo

Per altre informazioni sul processo generale di aggiunta dei ruoli, vedere [Installare i ruoli del sistema del sito](install-site-system-roles.md).

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito**, selezionare il nodo **Siti** e fare clic su **Crea server di sistema sito** nella barra multifunzione.

2. Nella pagina **Generale** della Creazione guidata server del sistema sito specificare il server per ospitare il server del sito in modalità passiva. Il server specificato non può ospitare ruoli del sistema del sito prima di installare un server del sito in modalità passiva.  

3. Nella pagina **Selezione ruolo del sistema** selezionare solo **Server del sito in modalità passiva**.  

    > [!NOTE]  
    > La procedura guidata esegue i controlli dei prerequisiti iniziali seguenti in questa pagina:
    >
    > - Il server selezionato non è un server del sito secondario
    > - Il server selezionato non è già un server del sito in modalità passiva
    > - La raccolta contenuto del sito è in una posizione remota  
    >  
    > Se questi controlli dei prerequisiti iniziali hanno esito negativo, non è possibile proseguire oltre questa pagina della procedura guidata.  

4. Nella pagina **Server del sito in modalità passiva** fornire le informazioni seguenti che vengono usate per eseguire la configurazione e installare il ruolo del server del sito nel server specificato:

     - Scegliere una delle seguenti opzioni:  

         - **Copia i file di origine dell'installazione in rete dal server del sito in modalità attiva**: questa opzione crea un pacchetto compresso e lo invia al nuovo server del sito.  

         - **Usa i file di origine nel percorso seguente nel server del sito in modalità passiva**: ad esempio, un percorso locale in cui sono già stati copiati i file di origine. Assicurarsi che questo contenuto sia della stessa versione del server del sito in modalità attiva.  

         - (*Opzione consigliata*) **Utilizza i file di origine nel seguente percorso di rete**: specificare il percorso diretto al contenuto della cartella **CD.Latest** dal server del sito in modalità attiva. Ad esempio, `\\Server\SMS_ABC\CD.Latest`, dove "*Server*" è il nome del server del sito in modalità attiva e "*ABC*" è il codice del sito.  

     - Specificare il percorso locale in cui installare Configuration Manager nel nuovo server del sito. ad esempio `C:\Program Files\Configuration Manager`  

5. Completare la procedura guidata. Configuration Manager installa quindi il server del sito in modalità Passivo nel server specificato.

Per lo stato dettagliato dell'installazione, nella console andare all'area di lavoro **Monitoraggio** e selezionare il nodo **Stato del server del sito**. Lo stato del server del sito in modalità passiva viene visualizzato come **Installazione**. Per altre informazioni dettagliate, selezionare il server e fare clic su **Mostra stato**. Questa azione apre la finestra Stato dell'installazione del server del sito. Al termine del processo, lo stato viene visualizzato come **OK** per entrambi i server.

Per altre informazioni sul processo di configurazione, vedere [Diagramma di flusso - Configurare un server del sito in modalità passiva](passive-site-server-flowchart.md).

Dopo aver aggiunto un server del sito in modalità passiva, visualizzare entrambi i server del sito nella scheda **Nodi** nel nodo **Siti** della console.

Tutti i componenti del server del sito di Configuration Manager sono in standby nel server del sito in modalità passiva. I servizi Windows sono ancora in esecuzione.

## <a name="site-server-promotion"></a>Innalzamento di livello dei server del sito  

Come per il backup e ripristino, pianificare e provare il processo per modificare i server del sito. Prendere in considerazione i punti seguenti nel piano di innalzamento di livello:  

- Provare un innalzamento di livello pianificato, in cui entrambi i server del sito sono online. Provare anche un failover non pianificato, disconnettendo o arrestando in modo forzato il server del sito in modalità attiva.  

- Determinare i processi operativi durante il failover e che cosa comunicare agli altri amministratori di Configuration Manager.  

- Prima di un innalzamento di livello pianificato:  

  - Controllare lo stato generale del sito e i componenti del sito. Assicurarsi che tutto sia integro come di consueto per l'ambiente.  

  - Controllare lo stato del contenuto per i pacchetti che eseguono la replica attiva tra siti.  

  - Controllare lo stato del sito secondario e la replica del sito.

  - Non avviare nuovi processi di distribuzione del contenuto o di manutenzione nei server del sito figlio o secondari.

    > [!NOTE]
    > Se la replica di file o database tra siti è in corso durante il failover, il nuovo server del sito potrebbe non ricevere il contenuto replicato. In questo caso, ridistribuire il contenuto software quando il nuovo server del sito è attivo.<!--515436--> Per la replica di database, potrebbe essere necessario reinizializzare un sito secondario dopo il failover.<!-- SCCMDocs issue 808 -->

  - Ridurre o rimuovere altre attività pianificate nello stesso momento. Ad esempio, non pianificare la promozione di un server del sito subito dopo aver aggiornato il sito a una nuova versione. L'aggiornamento del sito include altre attività potenzialmente in conflitto con la promozione del server del sito.

    > [!TIP]
    > Di seguito è riportato un esempio di come altre attività possono essere in conflitto con la promozione del server del sito:
    >
    > - Lunedì: aggiornare il sito alla versione più recente. Abilitare l'aggiornamento automatico dei client con distribuzione in una raccolta pilota.
    > - Martedì: promuovere il server del sito in modalità passiva a server del sito attivo.
    >
    > Mercoledì o giovedì questa azione potrebbe causare l'aggiornamento di *tutti* i client, non solo della raccolta pilota. Questo comportamento può causare un utilizzo significativo della rete e un carico imprevisto nei punti di distribuzione.<!-- SCCMDocs-pr#4794 -->

### <a name="process-to-promote-the-site-server-in-passive-mode-to-active-mode"></a>Processo per alzare di livello il server del sito in modalità passiva alla modalità attiva

Questa sezione descrive come far passare il server del sito in modalità passiva alla modalità attiva. Per accedere al sito e apportare questa modifica, è necessario poter accedere a un'istanza del provider SMS. Per altre informazioni, vedere [Usare più provider SMS](../../../plan-design/hierarchy/plan-for-the-sms-provider.md#BKMK_MultiSMSProv).  

> [!IMPORTANT]  
> Se tutte le istanze del provider SMS sono offline, non è possibile connettersi al sito perché non è disponibile alcun provider. Quando si aggiunge il server del sito in modalità passiva, il programma di installazione installa un'istanza del provider SMS in questo server.<!-- SCCMDocs#1613 -->
>
> La console di Configuration Manager richiede l'elenco dei provider SMS disponibili da WMI sul server del sito. Quando si installano più provider SMS in un sito, il sito assegna in modo casuale ogni nuova richiesta di connessione per usare un provider SMS installato. Non è possibile specificare la posizione del provider SMS da usare con una sessione di connessione specifica. Se la console non riesce a connettersi al sito perché il server del sito corrente è offline, specificare l'altro server del sito nella finestra Connessione al sito.  

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito** e selezionare **Siti**. Selezionare il sito e quindi passare alla scheda **Nodi**. Selezionare il server del sito in modalità passiva e quindi fare clic su **Alza di livello su attivo** nella barra multifunzione. Fare clic su **Sì** per confermare e continuare.
  
2. Aggiornare il nodo della console. La colonna **Stato** per il server che si sta alzando di livello viene visualizzata nella scheda **Nodi** come **Innalzamento di livello**.  

3. Al termine dell'innalzamento di livello, nella colonna **Stato** viene visualizzato **OK** sia per il nuovo server del sito in modalità attiva che per il nuovo server del sito in modalità passiva. La colonna **Nome server** per il sito ora indica il nome del nuovo server del sito in modalità attiva.

Per lo stato dettagliato, andare all'area di lavoro **Monitoraggio** e selezionare il nodo **Stato del server del sito**. La colonna **Modalità** identifica quale server è *Attivo* o *Passivo*. Quando si alza di livello un server dalla modalità passiva alla modalità attiva, selezionare il server del sito che si sta alzando di livello alla modalità attiva e quindi scegliere **Mostra stato** dalla barra multifunzione. Questa azione apre la finestra Site Server Promotion Status (Stato innalzamento di livello server del sito) che mostra altri dettagli relativi al processo.

Quando un server del sito in modalità Attivo passa alla modalità Passivo, solo il ruolo del sistema del sito è reso passivo. Tutti gli altri ruoli del sistema del sito che vengono installati su quel computer restano attivi e accessibili ai client.

Per altre informazioni sul processo di innalzamento di livello *pianificato*, vedere [Diagramma di flusso - Alzare di livello il server del sito (con pianificazione)](promote-site-server-flowchart.md).

### <a name="unplanned-failover"></a>Failover non pianificato

Se il server del sito corrente in modalità attiva è offline, il server del sito per l'innalzamento di livello prova a contattare il server del sito corrente in modalità attiva per 30 minuti. Se il server offline torna disponibile entro questo intervallo di tempo, viene inviata una notifica e la modifica procede normalmente. In caso contrario, il server del sito per l'innalzamento di livello aggiorna in modo forzato la configurazione del sito per renderla attiva. Se il server offline torna disponibile dopo questo intervallo di tempo, verifica prima di tutto lo stato corrente nel database del sito, quindi si abbassa di livello al server del sito in modalità passiva.

Durante questi 30 minuti di attesa, il sito non ha server del sito in modalità attiva. I client comunicano ugualmente con i ruoli destinati ai client, ad esempio i punti di gestione, i punti di aggiornamento software e i punti di distribuzione. Gli utenti possono installare il software che è già stato distribuito. L'amministrazione del sito non è consentita in questo periodo di tempo. Per altre informazioni, vedere [Impatto degli errori del sito](../../manage/site-failure-impacts.md).  

Se il server offline è danneggiato e non può tornare disponibile, eliminare questo server del sito dalla console, quindi creare un nuovo server del sito in modalità passiva per ripristinare un servizio a disponibilità elevata.

Per altre informazioni sul processo di failover *non pianificato*, vedere [Diagramma di flusso - Alzare di livello il server del sito (senza pianificazione)](promote-site-server-unplanned-flowchart.md).

### <a name="additional-tasks-after-site-server-promotion"></a>Attività aggiuntive dopo l'innalzamento di livello server del sito  

Dopo aver commutato i server del sito, non occorre eseguire la maggior parte delle altre attività necessarie per il [ripristino di un sito](../../manage/recover-sites.md#post-recovery-tasks). Non è ad esempio necessario reimpostare le password o riconnettersi alla sottoscrizione di Microsoft Intune.

La procedura seguente potrebbe essere necessaria per l'ambiente specifico:  

- Se si importano i certificati PKI per i punti di distribuzione, reimportare il certificato per i server interessati. Per altre informazioni, vedere [Rigenerare i certificati per i punti di distribuzione](../../manage/recover-sites.md#regenerate-the-certificates-for-distribution-points).  

- Se si integra Configuration Manager con Microsoft Store per le aziende, riconfigurare tale connessione. Per altre informazioni, vedere [Gestire le app da Microsoft Store per le aziende](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).  

## <a name="daily-monitoring"></a>Monitoraggio giornaliero

Quando si ha un server del sito in modalità passiva, monitorarlo giornalmente. Assicurarsi che lo stato rimanga OK e che sia pronto per l'uso. Nella console di Configuration Manager andare all'area di lavoro **Monitoraggio** e selezionare il nodo **Stato del server del sito**. Visualizzare entrambi i server del sito e lo stato corrente. Visualizzare lo stato anche nell'area di lavoro **Amministrazione**. Espandere **Configurazione del sito** e selezionare il nodo **Siti**. Selezionare il sito e quindi passare alla scheda **Nodi**.

> [!NOTE]
> Quando si aggiorna il sito a una nuova versione di Configuration Manager, viene aggiornato anche il server del sito in modalità passiva. <!-- SCCMDocs-pr#4293 -->