---
title: Funzionalità nella Technical Preview 1606
titleSuffix: Configuration Manager
description: Informazioni sulle funzionalità disponibili nella versione Technical Preview 1606 per Configuration Manager.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 134a2f60-811e-4dc9-a8f5-1ce0018c5c12
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: 0513c1908b1360a50653931dda57e5d148055240
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905682"
---
# <a name="capabilities-in-technical-preview-1606-for-configuration-manager"></a>Funzionalità della versione Technical Preview 1606 per Configuration Manager

*Si applica a: Configuration Manager (Technical Preview Branch)*

Questo articolo presenta le funzionalità disponibili nella Technical Preview per Configuration Manager versione 1606. È possibile installare questa versione per aggiornare e aggiungere nuove funzionalità al sito di Technical Preview di Configuration Manager.      Prima di installare questa versione Technical Preview, consultare l'argomento introduttivo [Technical Preview per Center Configuration Manager](../../core/get-started/technical-preview.md) per acquisire familiarità con i requisiti generali e con le limitazioni per l'uso di una versione Technical Preview, con le modalità di aggiornamento tra le versioni e con le modalità per offrire commenti e suggerimenti sulle funzionalità di una versione Technical Preview.    

**Problemi noti di questa versione Technical Preview:**  
*  Quando si esegue l'aggiornamento dalla versione Technical Preview 1604 alla 1605 e quindi alla 1606, l'aggiornamento potrebbe non riuscire e si potrebbe ottenere la registrazione di un errore simile al seguente in **cmupdate.log**:

    ``` Log
    ERROR: Failed to execute SQL Server command:  ~ ~-- Create site boundary group ~IF  dbo.fnIsCasOrStandalonePrimary() = 1 ~BEGIN ~   PRINT N'Create site boundary group during upgrade' ~   EXEC dbo.spBuildDefaultBoundaryGroups @UserName = N'SYSTEM' ~END
    ```

    In questo caso nel nodo **Aggiornamenti e manutenzione** fare clic su **Controlla aggiornamenti** e quindi su **Riprova** per ritentare l'installazione dell'aggiornamento.
    ***

**Di seguito sono riportate le nuove funzionalità disponibili con questa versione.**  

## <a name="automatically-categorize-devices-into-collections"></a><a name="dmp_category"></a> Categorizzazione automatica dei dispositivi in raccolte
È possibile creare categorie di dispositivi da usare per inserire automaticamente i dispositivi nelle raccolte di dispositivi quando si usa Configuration Manager con Microsoft Intune. Agli utenti verrà quindi richiesto di scegliere una categoria di dispositivo quando eseguono la registrazione di un dispositivo in Intune. È possibile modificare la categoria di un dispositivo dalla console di Configuration Manager.

**Importante:** Questa funzionalità può essere usata con la versione di Microsoft Intune di **giugno 2016**. Verificare che l'installazione sia aggiornata a questa versione prima di tentare tali procedure.

### <a name="try-it-out"></a>Verifica

### <a name="create-a-set-of-device-categories"></a>Creare un set di categorie di dispositivo
1.  Nell'area di lavoro **Asset e conformità** della console di Configuration Manager espandere **Panoramica** e fare clic su **Raccolte di dispositivi**.
2.  Sulla scheda **Home**, nel gruppo **Categorie**, fare clic su **Gestire le categorie di dispositivi**.
3.  Nella finestra di dialogo **Gestire le categorie di dispositivi** è possibile creare, modificare o rimuovere le categorie. Provare a creare una nuova categoria.

### <a name="associate-a-collection-with-a-device-category"></a>Associare una raccolta a una categoria di dispositivo
Quando si associa una raccolta a una categoria di dispositivo, tutti i dispositivi della categoria specificata verranno aggiunti alla raccolta.
1.  Nella della finestra di dialogo **Proprietà** per una raccolta di dispositivi fare clic su **Aggiungi regola** > **Regola categoria di dispositivi**.
2.  Nella finestra di dialogo **Create Device Category Membership Rule** (Crea regola di appartenenza per la categoria di dispositivi) selezionare la categoria che sarà applicata a tutti i dispositivi della raccolta.
3.  Chiudere la finestra di dialogo **Create Device Category Membership Rule** (Crea regola di appartenenza per la categoria di dispositivi) e la finestra di dialogo delle proprietà della raccolta.

### <a name="change-the-category-of-a-device"></a>Cambiare la categoria di un dispositivo
1.  Nell'area di lavoro **Asset e conformità** della console di Configuration Manager espandere **Panoramica** e fare clic su **Dispositivi**.
2.  Selezionare un dispositivo nell'elenco **Dispositivi** quindi, sulla scheda **Home**, nel gruppo **Dispositivo**, fare clic su **Cambia categoria**.
3.  Nella finestra di dialogo **Modifica categoria di dispositivi** scegliere la categoria da applicare al dispositivo e fare clic su **OK**.

## <a name="enforcement-grace-period-for-required-application-and-software-update-deployments"></a><a name="dmp_grace"></a> Periodo di tolleranza di imposizione per le distribuzioni di applicazioni e aggiornamenti software obbligatori

In alcuni casi è possibile concedere agli utenti più tempo per l'installazione di distribuzioni di applicazioni o aggiornamenti del software obbligatori, superando eventuali scadenze configurate. In genere questo potrebbe essere necessario quando un computer è stato disattivato per un lungo periodo di tempo ed è necessario installare un numero elevato di distribuzioni di applicazioni o aggiornamenti.
Ad esempio, se un utente finale è appena tornato da una vacanza, potrebbe dover attendere un po' tempo mentre vengono installate le distribuzioni delle applicazioni scadute.
Per risolvere il problema ora è possibile definire un periodo di tolleranza di imposizione distribuendo le impostazioni del client di Configuration Manager a una raccolta.

### <a name="try-it-out"></a>Verifica

Per configurare il periodo di tolleranza eseguire le operazioni seguenti:

1.  Nella pagina **Agente computer** delle impostazioni del client configurare la nuova proprietà **Periodo di tolleranza per l'imposizione dopo la scadenza della distribuzione (ore)** con un valore compreso tra **1** e **120** ore.
2.  In una nuova distribuzione richiesta dell'applicazione o nelle proprietà di una distribuzione esistente, nella pagina **Pianificazione** selezionare la casella di controllo **Ritardare l'imposizione di questa distribuzione in base alle preferenze dell'utente**, fino al periodo di tolleranza definito nelle impostazioni client.
Tutte le distribuzioni con questa casella di controllo selezionata e che sono destinate a dispositivi in cui è stata distribuita anche l'impostazione del client useranno il periodo di tolleranza di imposizione.

Se si configura un periodo di tolleranza di imposizione e si seleziona la casella di controllo, quando si raggiunge la scadenza dell'installazione dell'applicazione, essa verrà installata nella prima finestra non aziendale che l'utente ha configurato fino al periodo di grazia. Tuttavia l'utente può comunque aprire Software Center e installare l'applicazione in qualsiasi momento. Una volta scaduto il periodo di tolleranza, le distribuzioni scadute torneranno al normale comportamento.
Opzioni simili sono state aggiunte alla procedura guidata di distribuzione degli aggiornamenti software, alla procedura guidata di creazione delle regole di distribuzione automatica e alle pagine delle proprietà.

##  <a name="using-configuration-manager-as-a-managed-installer-with-device-guard"></a><a name="dmp_devg"></a>Uso di Configuration Manager come programma di installazione gestito con Device Guard

Controllo dispositivo è una funzionalità di Windows 10 che usa funzioni hardware e software per controllare accuratamente ciò che può essere eseguita sul dispositivo.

Per altre informazioni, vedere [Introduzione a Device Guard](https://docs.microsoft.com/windows/security/threat-protection/device-guard/introduction-to-device-guard-virtualization-based-security-and-windows-defender-application-control).

In questa versione Configuration Manager può interagire con Controllo dispositivo e [Windows AppLocker](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd723678(v=ws.10)) in modo che i file eseguibili e le DLL che vengono distribuite con Configuration Manager siano automaticamente attendibili, in quanto provenienti da un programma di installazione gestito, perciò sia consentita la loro esecuzione sul dispositivo di destinazione, mentre non sarà consentita agli altri software se non esplicitamente specificato da altre regole di AppLocker.  

Attualmente questa funzionalità non è configurabile dalla console di Configuration Manager. Per configurare i criteri è necessario configurare una chiave di registro su ciascun client e configurare servizi di Windows sul client.
Al termine configurare il file di criteri di AppLocker. Dopo aver configurato il file dei criteri è possibile distribuirlo a qualsiasi dispositivo compatibile con il client.


I criteri con regole del programma di installazione gestito, come tutti i criteri di AppLocker, possono essere eseguiti in due modalità:

- Modalità di controllo: non viene impedita l'esecuzione delle applicazioni ma tutte le applicazioni che sarebbero state bloccate vengono segnalate in un file di log (la funzionalità sarà supportata in una versione successiva di Configuration Manager).
- Imposizione abilitata: viene impedita l'esecuzione delle applicazioni.

Per altre informazioni, vedere gli articoli seguenti:

- [Introduzione a Controllo dispositivo](https://docs.microsoft.com/windows/security/threat-protection/device-guard/introduction-to-device-guard-virtualization-based-security-and-windows-defender-application-control)

- [Pianificazione e introduzione al processo di distribuzione di Controllo di applicazioni di Windows Defender](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control-deployment-guide)

  ##  <a name="multiple-device-management-points-for-on-premises-mobile-device-management"></a><a name="dmp_onprem"></a> Punti di gestione dei dispositivi multipli per la gestione dei dispositivi mobili locale  
  Con la versione Technical Preview 1606, Gestione dispositivi mobili locali supporta una nuova funzionalità di Windows 10 Anniversary Update che configura automaticamente un dispositivo registrato affinché usi più di un punto di gestione periferiche. Questa funzionalità consente al dispositivo il fallback su un altro punto di gestione periferiche quando quello che usa di solito non è disponibile. La funzionalità è operativa solo nei PC in cui è stato installato Windows 10 Anniversary Update.  

### <a name="try-it-out"></a>Verifica  

1.  Installare più di un punto di gestione dispositivi nella gerarchia.  

2.  Registrare un dispositivo Windows 10 Anniversary Update per Gestione dispositivi mobili locali.  

Per informazioni su come preparare il sito e registrare i dispositivi per Gestione dispositivi mobili locali, vedere [Gestire i dispositivi mobili con infrastruttura locale](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

## <a name="cloud-proxy-service-for-managing-clients-on-the-internet"></a><a name="cloud_proxy"></a>Servizio proxy cloud per la gestione dei client su Internet

Il servizio proxy cloud offre un modo semplice per gestire i client di Configuration Manager su Internet. Il servizio, che viene distribuito in Microsoft Azure e richiede una sottoscrizione di Azure, si connette all'infrastruttura di Configuration Manager locale usando un nuovo ruolo, denominato punto del connettore proxy cloud. Una volta che è stato completamente distribuito e configurato, i client saranno in grado di accedere ai ruoli di sistema del sito Configuration Manager locale indipendentemente dal fatto che siano connessi alla rete privata interna o su Internet.

Si usa la console di Configuration Manager per distribuire il servizio in Azure, aggiungere il ruolo punto di connessione proxy cloud e configurare i ruoli del sistema del sito per consentire il traffico del proxy cloud. Il servizio proxy cloud supporta attualmente solo i ruoli punto di gestione, punto di distribuzione e punto di aggiornamento software.

Per autenticare i computer e crittografare le comunicazioni tra i diversi livelli di servizio sono necessari certificati client e certificati Secure Socket Layer (SSL). I computer client ricevono in genere un certificato client mediante l'imposizione dei criteri di gruppo. Per crittografare il traffico tra i client e il server di sistema del sito che ospita i ruoli, è necessario creare un certificato SSL personalizzato mediante un'autorità di certificazione. Oltre a questi due tipi di certificati è inoltre necessario impostare un certificato di gestione in Azure che consente a Configuration Manager di distribuire il servizio proxy cloud.  

### <a name="requirements-for-cloud-proxy-service-in-tp-1606"></a>Requisiti per il servizio proxy cloud in TP 1606
- I computer client e il server di sistema del sito eseguono il punto di connessione del proxy cloud.
- Certificati SSL personalizzati dell'autorità di certificazione interna, utilizzati per crittografare le comunicazioni dai computer client e autenticare l'identità del servizio proxy cloud.
- Sottoscrizione di Azure per i servizi cloud.
- Certificato di gestione di Azure, utilizzato per l'autenticazione di Configuration Manager con Azure.

### <a name="limitations-of-cloud-proxy-service-in-tp-1606"></a>Limitazioni del servizio proxy cloud in TP 1606

- Supporta solo i ruoli punto di gestione, punto di distribuzione e punto di aggiornamento software.
- I criteri utente non sono supportati.
- Non è utilizzabile con [Gestione dispositivi mobili locali](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) in Configuration Manager.
- Supportato solo nella piattaforma cloud pubblica di Azure.


### <a name="try-it-out"></a>Verifica

La procedura per distribuire il servizio proxy cloud include i passaggi seguenti:

1. Creare ed emettere un certificato SSL personalizzato per il servizio proxy cloud.
1. Esportare la radice del certificato client.
2. Caricare il certificato di gestione in Azure.
3. Impostare il servizio proxy cloud nella console di Configuration Manager.
4. Configurare il sito primario per l'uso dell'autenticazione del client mediante certificato.
5. Aggiungere il punto di connessione del proxy cloud al sito.
6. Configurare i ruoli del sistema del sito per accettare il traffico del proxy cloud.

Le sezioni seguenti forniscono altre informazioni per completare questi passaggi.

#### <a name="create-a-custom-ssl-certificate"></a>Creare un certificato SSL personalizzato

È possibile creare un certificato SSL personalizzato per il servizio proxy cloud esattamente come si farebbe per un punto di distribuzione basato su cloud. Seguire le istruzioni per la [distribuzione del certificato di servizio per i punti di distribuzione basati su cloud](../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clouddp2008_cm2012) procedendo in modo diverso per le operazioni seguenti:

* Quando si configura il nuovo modello di certificato, assegnare le autorizzazioni **Lettura** e **Registrazione** al gruppo di protezione impostato per i server di Configuration Manager.

#### <a name="export-the-client-certificates-root"></a>Esportare la radice del certificato client

Il modo più semplice per ottenere l'esportazione della radice dei certificati client utilizzati nella rete è aprire un certificato client in uno dei computer appartenenti a un dominio che ne abbia uno e copiarlo.

>[!NOTE]
>I certificati client sono richiesti su qualsiasi computer che si vuole gestire con il servizio proxy cloud e sul server di sistema del sito che ospita il punto di connessione del proxy cloud. Se è necessario aggiungere un certificato client a uno di tali computer, vedere [Distribuzione del certificato client per computer Windows](../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clouddp2008_cm2012).

1. Nella finestra Esegui digitare **mmc** e premere INVIO.
2. Nel menu File della console di gestione fare clic su **Aggiungi/Rimuovi snap-in**.
3. Nella finestra di dialogo Aggiungi o rimuovi Snap-in fare clic su **Certificati**, fare clic su **Aggiungi >** , su **Account computer**, su **Avanti**, su **Computer locale**, quindi fare clic su **Fine**. Fare clic su **OK** per chiudere la finestra di dialogo.
4. Passare a **Certificati > Personale > Certificati**.
5. Fare doppio clic sul certificato per l'autenticazione client nel computer, fare clic sulla scheda Percorso certificazione e fare doppio clic sull'autorità radice (nella parte superiore del percorso).
6.  Fare clic sulla scheda Dettagli e fare clic su **Copia su file...** .
7. Completare l'Esportazione guidata certificati utilizzando il formato di certificato predefinito. Prendere nota del nome e percorso del certificato radice creato. Sarà necessario configurare il servizio proxy cloud in un passaggio successivo.

#### <a name="upload-the-management-certificate-to-azure"></a>Caricare il certificato di gestione in Azure

È necessario un certificato di gestione di Azure perché Configuration Manager possa accedere all'API di Azure e configurare il servizio proxy cloud. Per altre informazioni e istruzioni su come caricare un certificato di gestione, vedere gli articoli seguenti nella documentazione di Azure:
- [Panoramica sui certificati per i servizi cloud di Azure](https://azure.microsoft.com/documentation/articles/cloud-services-certs-create/)
- [Caricare un certificato di gestione dell'API di gestione di Azure](https://azure.microsoft.com/documentation/articles/azure-api-management-certs/).

Assicurarsi di copiare l'ID sottoscrizione associato al certificato di gestione. Sarà necessario per configurare il servizio proxy cloud nella console di Configuration Manager.

#### <a name="set-up-cloud-proxy-service"></a>Configurare il servizio proxy cloud

1. Aprire la console di Configuration Manager e passare ad **Amministrazione > Servizi cloud > Servizio proxy cloud**.
2. Fare clic su **Crea il servizio proxy cloud**.
3. Nella Creazione guidata del servizio proxy cloud immettere l'ID sottoscrizione di Azure (copiato dal portale di gestione di Azure), fare clic su Sfoglia e selezionare il file di certificato caricato come certificato di gestione di Azure. Fare clic su **Avanti**. Attendere qualche secondo affinché la console si connetta ad Azure.
4. Compilare i dettagli aggiuntivi nella procedura guidata:
    - Specificare la chiave privata (file con estensione .pfx) esportato dal certificato SSL personalizzato.
    - Specificare il certificato radice esportato dal certificato client.
    - Specificare lo stesso FQDN del nome del servizio utilizzato per creare il nuovo modello di certificato.
    - Deselezionare la casella accanto a **Verifica la revoca di certificato client** (a meno che non si intenda pubblicare le informazioni di CRL).
    - Al termine fare clic su **Avanti**.
5. Verificare le impostazioni e fare clic su **Avanti**. Configuration Manager avvia la configurazione del servizio. Al termine della procedura guidata è possibile fare clic su **Chiudi** ma saranno necessari da 5 a 15 minuti per completare il provisioning del servizio in Azure. Controllare la colonna **Stato** per il nuovo servizio proxy cloud configurato per determinare quando il servizio è pronto.

#### <a name="configure-primary-site-for-client-certification-authentication"></a>Configurare il sito primario per l'autenticazione con certificati client

1. Nella console di Configuration Manager passare ad **Amministrazione > Configurazione del sito > Siti**.
2. Selezionare il sito primario per i client che si vuole gestire tramite il servizio proxy cloud e fare clic su **Proprietà**.
3. Nella scheda Comunicazioni computer client della finestra delle proprietà del sito primario selezionare la casella accanto a **Utilizza certificato client PKI (funzionalità di autenticazione client) quando disponibile**.
4. Deselezionare la casella accanto a **Controllo client dell'elenco di revoche di certificati (CRL) per i sistemi del sito**. Questa opzione è necessaria solo quando si pubblicano i CRL.
5. Fare clic su **OK**.

#### <a name="add-the-cloud-proxy-connector-point"></a>Aggiungere il punto di connessione del proxy cloud

Il punto di connessione del proxy cloud è un nuovo ruolo del sistema del sito per la comunicazione con il servizio proxy cloud. Per aggiungere il punto di connessione del proxy cloud seguire le istruzioni in [Aggiungere ruoli del sistema del sito per Configuration Manager](../../core/servers/deploy/configure/add-site-system-roles.md).

#### <a name="configure-roles-for-cloud-proxy-traffic"></a>Configurare i ruoli per il traffico del proxy cloud

L'ultimo passaggio della configurazione del servizio proxy cloud consiste nel configurare i ruoli del sistema del sito per accettare il traffico del proxy cloud. Con la versione Technical Preview 1606 solo i ruoli punto di gestione, punto di distribuzione e aggiornamento del software sono supportati per il servizio proxy cloud. È necessario configurare separatamente ogni ruolo.

1. Nella console di Configuration Manager passare ad **Amministrazione > Configurazione del sito > Server e ruoli del sistema del sito**.
2. Fare clic sul server di sistema del sito per il ruolo che si vuole configurare per il traffico del proxy cloud.
3. Fare clic sul ruolo e quindi fare clic su **Proprietà**.
4. Nella finestra delle proprietà del ruolo, sotto Connessioni client, scegliere **HTTPS**, selezionare la casella accanto a **Consenti traffico proxy cloud di Configuration Manager** quindi fare clic su **OK**. Ripetere questi passaggi per i ruoli rimanenti.

#### <a name="check-status-on-a-client-on-the-internet"></a>Controllare lo stato in un client su Internet

Quando il servizio e i ruoli sono completamente configurati, i client interni otterranno la posizione del servizio proxy cloud alla successiva richiesta di percorso. I client con informazioni sul percorso aggiornate possono quindi comunicare con Configuration Manager su Internet. Il ciclo di polling per le richieste di percorso è di 24 ore. Se non si vuole attendere la richiesta di percorso della normale pianificazione, è possibile forzare la richiesta riavviando il servizio host agenti di SMS (ccmexec.exe) nel computer.

Quando i client hanno le nuove informazioni di percorso per il servizio proxy cloud, controllare lo stato dei client che non sono più nella rete privata interna ma hanno accesso a Internet. È inoltre possibile monitorare il traffico sul servizio proxy cloud passando ad **Amministrazione > Servizi cloud > Servizio proxy cloud**, selezionando il servizio nel riquadro dell'elenco e visualizzando le informazioni di traffico nel riquadro dei dettagli.   

## <a name="manage-the-office-365-client-agent-in-configuration-manager"></a><a name="manage_o365"></a> Gestione dell'agente del client Office 365 in Configuration Manager  

A partire dalla versione Technical Preview 1606 è possibile usare un'impostazione dell'agente client di Configuration Manager, invece dei criteri di gruppo, per consentire ai client di Office 365 di ricevere aggiornamenti da Configuration Manager. Dopo aver configurato questa impostazione e distribuito gli aggiornamenti di Office 365, l'agente client di Configuration Manager comunica con l'agente client di Office 365 al fine di scaricare gli aggiornamenti di Office 365 da un punto di distribuzione e installarli. Configuration Manager rileva inoltre l'impostazione dell'agente client.

Per altre informazioni, vedere [Manage Office 365 ProPlus updates](../../sum/deploy-use/manage-office-365-proplus-updates.md) (Gestire gli aggiornamenti di Office 365 ProPlus).

### <a name="set-the-configuration-manager-client-setting-to-manage-the-office-365-client-agent"></a>Definire l'impostazione del client di Configuration Manager per gestire l'agente client di Office 365
1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Panoramica** > **Impostazioni client**.
2. Aprire le impostazioni del dispositivo appropriato per abilitare l'agente client. Per altre informazioni su come configurare le impostazioni client predefinite e personalizzate, vedere [Come configurare le impostazioni client](../../core/clients/deploy/configure-client-settings.md).
3. Fare clic su **Aggiornamenti software** e selezionare **Sì** per l'impostazione **Abilita la gestione dell'agente client di Office 365**.  


## <a name="the-osdpreservedriveletter-task-sequence-variable-has-been-deprecated"></a><a name="osdpreservedriveletter"></a>La variabile della sequenza di attività OSDPreserveDriveLetter è stata deprecata
La variabile della sequenza di attività OSDPreserveDriveLetter determina se la sequenza di attività usa la lettera di unità acquisita nel file WIM dell'immagine del sistema operativo quando si applica tale immagine a un computer di destinazione.
- Questa variabile della sequenza di attività è stata deprecata nella versione Technical Preview 1606.

Durante la distribuzione del sistema operativo, per impostazione predefinita l'installazione di Windows ora stabilisce qual è la lettera di unità migliore da usare (in genere C:). Se si vuole specificare un'unità diversa da usare, è possibile modificare il percorso nella sequenza di passaggi dell'attività Applica sistema operativo. Passare all'impostazione **Selezionare il percorso in cui applicare questo sistema operativo**, selezionare **Lettera unità logica specifica** e scegliere l'unità che si vuole usare. Nel computer di destinazione deve essere presente un'unità assegnata alla lettera che si sceglie. 

## <a name="changes-for-the-updates-and-servicing-node"></a><a name="updatesandservicing"></a>Modifiche per il nodo Aggiornamenti e manutenzione
Con la versione Technical Preview 1606 sono state introdotte diverse modifiche che si applicano ad aggiornamenti e manutenzione nella console di Configuration Manager:
- **Modifica del nome del nodo:**

    Nell'area di lavoro **Monitoraggio** il nodo dello stato **Manutenzione del sito** è stato rinominato in **Aggiornamenti e stato di manutenzione**.
- **Altri stati di installazione:**

    Quando si visualizza lo stato di installazione dell'aggiornamento di un sito, nella console vengono ora mostrate informazioni distinte per le azioni seguenti:
    - **Download** (si applica solo al sito di livello superiore in cui è installato il ruolo del sistema del sito del punto di connessione del servizio)
    - **Replica**
    - **Controllo dei prerequisiti**
    - **Installazione**

  Inoltre, sono ora presenti più informazioni dettagliate per ogni passaggio, incluso il file di log nel quale è possibile visualizzare altre informazioni.  
-   **Nuova opzione per ignorare i messaggi sui prerequisiti non soddisfatti:**

    In entrambe le aree di lavoro **Amministrazione** e **Monitoraggio** il nodo **Aggiornamenti e manutenzione** include un nuovo pulsante sulla barra multifunzione denominato **Ignora avvisi dei prerequisiti**.

    Se si installa un aggiornamento senza usare l'opzione Ignora avvisi dei prerequisiti dalla procedura guidata e l'installazione dell'aggiornamento viene interrotta da un **avviso relativo ai prerequisiti** senza che si siano verificati errori, è possibile selezionare **Ignora avvisi dei prerequisiti** dalla barra multifunzione per riprendere automaticamente l'installazione ignorando gli avvisi dei prerequisiti.  



- **Visualizzazione più chiara degli aggiornamenti:**

    Quando si visualizza il nodo **Aggiornamenti e manutenzione**, ora è possibile visualizzare solo l'aggiornamento installato più recente e qualsiasi nuovo aggiornamento disponibile per l'installazione. Per visualizzare gli aggiornamenti installati in precedenza, fare clic sul nuovo pulsante **Cronologia** nella barra multifunzione.  

-   **Opzioni ridenominate per la fase di pre-produzione:**

    Nel nodo Aggiornamenti e manutenzione, il pulsante che era denominato **Opzioni client** è ora stato denominato **Alza di livello il client di pre-produzione**.
