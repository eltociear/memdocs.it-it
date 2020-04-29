---
title: Pianificare l'automazione delle attività
titleSuffix: Configuration Manager
description: Prevedere una pianificazione appropriata prima di creare sequenze di attività per automatizzare le attività con Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: fc497a8a-3c54-4529-8403-6f6171a21c64
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0348cc245efdfd5e4d1e0bad25a457ea3b1ca609
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708099"
---
# <a name="plan-for-automating-tasks-in-configuration-manager"></a>Pianificare l'automazione delle attività in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

È possibile creare sequenze di attività per automatizzare le attività nell'ambiente di Configuration Manager. Queste attività vanno dall'acquisizione di un sistema operativo in un computer di riferimento alla distribuzione del sistema operativo in uno o più computer di destinazione. Le azioni della sequenza di attività sono definite nei singoli passaggi della sequenza. Quando si esegue la sequenza di attività, le azioni di ogni passaggio vengono eseguite a livello di riga di comando nel contesto dell'account di sistema locale. Questo comportamento significa che la sequenza di attività viene eseguita in modo completamente automatizzato senza intervento dell'utente.

## <a name="task-sequence-steps-and-actions"></a><a name="BKMK_TSStepsActions"></a> Azioni e passaggi della sequenza di attività  

I passaggi sono i componenti di base di una sequenza di attività. I comandi possono includere, ad esempio:

- Configurare e acquisire il sistema operativo di un computer di riferimento
- Installare Windows, i driver hardware, il client di Configuration Manager e il software nel computer di destinazione

Le azioni del passaggio definiscono i comandi di un passaggio della sequenza di attività. Esistono due tipi di azioni:  

- Un'azione che viene definita usando una stringa della riga di comando viene definita *azione personalizzata*.  
- Un'azione predefinita da Configuration Manager viene definita *azione integrata*.  

Una sequenza di attività è in grado di eseguire qualsiasi combinazione di azioni predefinite e personalizzate.  

I passaggi della sequenza di attività possono includere anche condizioni che controllano il comportamento del passaggio. Questi comportamenti includono l'arresto della sequenza di attività o la continuazione della sequenza di attività in caso di errore. Un tipo di condizione è una variabile della sequenza di attività. Ad esempio, usare la variabile **SMSTSLastActionRetCode** per verificare la condizione del passaggio precedente. Aggiungere condizioni a un singolo passaggio o a un gruppo di passaggi.  

La sequenza di attività elabora i passaggi in sequenza. Questa sequenza include l'azione del passaggio e le eventuali condizioni per il passaggio. Quando Configuration Manager inizia a elaborare un passaggio della sequenza di attività, il passaggio successivo viene avviato solo dopo il completamento dell'azione precedente.

Una sequenza di attività viene considerata completa quando:

- Tutti i passaggi sono stati completati  
- Quando un passaggio non riuscito costringe Configuration Manager a interrompere l'esecuzione di una sequenza di attività prima del completamento di tutti i passaggi.  

Ad esempio, se il passaggio di una sequenza di attività non consente di individuare un'immagine o un pacchetto a cui viene fatto riferimento in un punto di distribuzione, la sequenza di attività include un riferimento interrotto. Configuration Manager arresta l'esecuzione della sequenza di attività a questo punto, a meno che il passaggio non riuscito non includa una condizione per continuare in caso di errore.  

> [!IMPORTANT]  
> Per impostazione predefinita, una sequenza di attività non riesce dopo che un passaggio o un'azione ha esito negativo. Per fare in modo che la sequenza di attività continui anche quando un passaggio non riesce, modificare la sequenza di attività, passare alla scheda **Opzioni** e selezionare **Continua in caso di errori**.  

Per altre informazioni sui passaggi che possono essere aggiunti a una sequenza di attività, vedere [Passaggi della sequenze di attività](../understand/task-sequence-steps.md).  

## <a name="task-sequence-groups"></a><a name="BKMK_TSGroups"></a> Gruppi di sequenze di attività  

È possibile raggruppare più passaggi all'interno di una sequenza di attività. Un gruppo di sequenze di attività è costituito da un nome, una descrizione facoltativa e qualsiasi condizione facoltativa. La sequenza di attività valuta le condizioni del gruppo come un'unità prima di continuare con il passaggio successivo. Annidare i gruppi uno nell'altro oppure includere una combinazione di passaggi e sottogruppi. I gruppi sono utili per combinare più passaggi che condividono una condizione comune.  

Assegnare un nome ai gruppi di sequenze di attività. Non deve necessariamente essere univoco. È inoltre possibile fornire una descrizione facoltativa per il gruppo sequenza di attività.  

> [!IMPORTANT]  
> Per impostazione predefinita, un gruppo di sequenze attività ha esito negativo quando si verifica un errore in un passaggio o in un gruppo incorporato all'interno del gruppo. Per fare in modo che la sequenza di attività continui quando un passaggio o un gruppo incorporato non riesce, impostare l'opzione **Continua in caso di errori** nel passaggio o nel gruppo.  

La tabella seguente illustra il funzionamento dell'opzione **Continua in caso di errore** quando si raggruppano i passaggi.  

In questo esempio sono presenti due gruppi di sequenze di attività che includono ognuno tre passaggi di sequenza di attività.  

|Gruppo o passaggio di sequenza di attività|Impostazione Continua in caso di errore|  
|---------------------------------|-------------------------------|  
|**Gruppo di sequenze di attività 1**|**Continua in caso di errori** selezionata.|  
|Passaggio sequenza di attività 1|**Continua in caso di errori** selezionata.|  
|Passaggio sequenza di attività 2|Non impostata.|  
|Passaggio sequenza di attività 3|Non impostata.|  
|**Gruppo di sequenze di attività 2**|Non impostata.|  
|Passaggio sequenza di attività 4|Non impostata.|  
|Passaggio sequenza di attività 5|Non impostata.|  
|Passaggio sequenza di attività 6|Non impostata.|  

- Se il passaggio sequenza di attività 1 non riesce, la sequenza di attività continua con il passaggio sequenza di attività 2.  

- Se il passaggio della sequenza di attività 2 non riesce, la sequenza di attività non esegue il passaggio della sequenza di attività 3. Dato che per il gruppo di sequenze di attività 1 è configurata l'opzione **Continua in caso di errore**, la sequenza di attività continua con il gruppo di sequenze di attività 2, poi esegue il passaggio della sequenza di attività 4.  

- Se il passaggio della sequenza di attività 4 ha esito negativo, non vengono eseguiti altri passaggi. La sequenza di attività non riesce perché l'impostazione **Continua in caso di errore** non è stata configurata per il gruppo di sequenza di attività 2.  

## <a name="add-child-task-sequences-to-a-task-sequence"></a>Aggiungere sequenze di attività figlio a una sequenza di attività

<!--1261338-->

Aggiungere un nuovo passaggio della sequenza di attività che esegue un'altra sequenza di attività. Questo passaggio crea una relazione padre-figlio tra le sequenze di attività. Questo passaggio consente di creare più sequenze di attività modulari riusabili.  

Per altre informazioni, vedere [Eseguire una sequenza di attività](../understand/task-sequence-steps.md#child-task-sequence).

> [!Note]  
> Configuration Manager non abilita questa funzionalità facoltativa per impostazione predefinita. Pertanto sarà necessario abilitarla prima di poterla usare. Per altre informazioni, vedere [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options) (Abilitare le funzioni facoltative dagli aggiornamenti).<!--505213-->  

## <a name="task-sequence-variables"></a><a name="BKMK_TSVariables"></a> Variabili della sequenza di attività  

Le variabili della sequenza di attività sono un set di coppie nome e valore che specificano le impostazioni di configurazione e distribuzione del sistema operativo per le attività di configurazione di computer, sistema operativo e stato utente in un client di Configuration Manager. Le variabili della sequenza di attività forniscono un meccanismo per configurare e personalizzare i passaggi in una sequenza di attività.  

Quando si esegue una sequenza di attività, molte delle impostazioni della sequenza di attività vengono archiviate come variabili di ambiente. È possibile accedere ai valori delle variabili della sequenza di attività predefinite o modificarli. È anche possibile creare nuove variabili della sequenza di attività per personalizzare il modo in cui una sequenza di attività viene eseguita in un computer di destinazione.  

Usare le variabili della sequenza di attività per eseguire le azioni seguenti:  

- Configurare le impostazioni per un'azione della sequenza di attività  

- Fornire gli argomenti della riga di comando per un passaggio della sequenza di attività  

- Valutare una condizione che determina se viene eseguito un passaggio o un gruppo della sequenza di attività  

- Fornire valori per gli script personalizzati usati in una sequenza di attività  

Ad esempio, si supponga di avere una sequenza di attività che include un passaggio di sequenza di attività **Aggiunta a dominio o gruppo di lavoro**. Distribuire la sequenza di attività in più raccolte, in cui l'appartenenza della raccolta viene determinata dall'appartenenza al dominio. Specificare una variabile della sequenza di attività per ogni raccolta per ogni nome di dominio della raccolta. Usare quindi la variabile della sequenza di attività per specificare il nome di dominio appropriato nella sequenza di attività.  

Per altre informazioni, vedere [How to use task sequence variables](../understand/using-task-sequence-variables.md) (Come usare le variabili della sequenza di attività).

## <a name="create-a-task-sequence"></a><a name="BKMK_TSCreate"></a> Creare una sequenza di attività  

Creare sequenze attività usando la Creazione guidata della sequenza di attività. La procedura guidata consente di creare sequenze attività predefinite che eseguono attività specifiche o sequenze attività personalizzate che possono eseguire molte attività differenti. Questa procedura guidata consente di creare i tipi seguenti di sequenze di attività:

- Installare un'immagine del sistema operativo esistente in un computer di destinazione  

- Creare e acquisire un'immagine del sistema operativo di un computer di riferimento  

- Eseguire l'aggiornamento a Windows 10 da un pacchetto di aggiornamento del sistema operativo in un computer di destinazione

- Creare una sequenza di attività personalizzata che esegue un'attività personalizzata o una distribuzione specializzata del sistema operativo  

Per altre informazioni, vedere [Creare sequenze di attività](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_CreateTaskSequence).  

## <a name="edit-a-task-sequence"></a><a name="BKMK_TSEdit"></a> Modificare una sequenza di attività  

Modificare la sequenza di attività tramite l'**editor delle sequenze di attività**. L'editor può apportare le seguenti modifiche alla sequenza di attività:  

- Aggiungere o rimuovere passaggi della sequenza di attività  

- Modificare l'ordine dei passaggi della sequenza di attività  

- Aggiungere o rimuovere gruppi di passaggi  

- Specificare se la sequenza di attività continua quando si verifica un errore  

- Aggiungere condizioni ai passaggi e ai gruppi di una sequenza di attività  

> [!IMPORTANT]  
> Se la sequenza di attività include riferimenti non associati a un oggetto come risultato della modifica, l'editor richiede di correggere il riferimento prima di chiudere. Le azioni possibili includono:  
>
> - Correggere il riferimento
> - Eliminare l'oggetto senza riferimenti dalla sequenza di attività  
> - Disabilitare temporaneamente il passaggio della sequenza di attività non riuscito fino alla correzione o rimozione del riferimento interrotto  

Per altre informazioni su come modificare una sequenza di attività, vedere [Usare l'editor delle sequenze di attività](../understand/task-sequence-editor.md).  

## <a name="deploy-a-task-sequence"></a><a name="BKMK_TSDeploy"></a> Distribuire una sequenza di attività  

Distribuire una sequenza di attività nei computer di destinazione che si trovano in qualsiasi raccolta di Configuration Manager. Usare la raccolta **Tutti i computer sconosciuti** predefinita per distribuire i sistemi operativi in computer sconosciuti. Non è possibile distribuire una sequenza di attività alle raccolte di utenti.  

> [!IMPORTANT]  
> Non distribuire sequenze attività che installano i sistemi operativi in raccolte non appropriate. Assicurarsi che la raccolta a cui si distribuisce la sequenza di attività includa solo i computer in cui si vuole installare il sistema operativo. Per evitare distribuzioni indesiderate del sistema operativo, configurare le impostazioni per le distribuzioni ad alto rischio. Per altre informazioni, vedere [Impostazioni per gestire distribuzioni ad alto rischio](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).  

Ciascun computer di destinazione che riceve la sequenza di attività la esegue in base alle impostazioni specificate nella distribuzione. La sequenza di attività stessa non contiene file o programmi associati. Qualsiasi file a cui fa riferimento una sequenza di attività deve essere già presente nel computer di destinazione oppure deve essere archiviato in un punto di distribuzione accessibile ai client.

> [!NOTE]  
> La sequenza di attività installa i pacchetti a cui fanno riferimento i programmi, anche se il programma o il pacchetto è già installato nel computer di destinazione.
>
> Se la sequenza di attività installa un'applicazione, l'applicazione viene installata solo se le regole relative ai requisiti per tale applicazione sono soddisfatte e l'applicazione non è già installata, in base al metodo di rilevamento specificato per l'applicazione.  

Il client di Configuration Manager esegue una distribuzione della sequenza di attività durante il download dei criteri del client. Per avviare l'azione anziché attendere fino al successivo ciclo di polling, vedere [Avviare il recupero criteri per un client di Configuration Manager](../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval).  

Quando si distribuiscono sequenze di attività in dispositivi con Windows Embedded abilitati con un filtro di scrittura, è possibile specificare se disabilitare il filtro di scrittura nel dispositivo durante la distribuzione e quindi riavviare il dispositivo al termine dell'operazione. Se il filtro di scrittura non è disabilitato, la sequenza di attività viene distribuita in una sovrapposizione temporanea e non sarà disponibile al riavvio del dispositivo.  

> [!NOTE]  
> Quando si distribuisce una sequenza di attività in un dispositivo con Windows Embedded, verificare che il dispositivo appartenga a una raccolta con una finestra di manutenzione configurata. Ciò consente di decidere quando abilitare o disabilitare il filtro di scrittura nonché quando riavviare il dispositivo.  
>
> Se i client scaricano sequenze attività al di fuori di una finestra di manutenzione, la sequenza di attività viene scaricata due volte. In questo scenario, il client scarica la sequenza di attività, disabilita il filtro di scrittura, riavvia il computer e quindi scarica nuovamente la sequenza di attività. Il motivo di questo comportamento è che la sequenza di attività era stata originariamente scaricata nella sovrapposizione temporanea, che viene cancellata al riavvio del dispositivo.  

Per altre informazioni su come distribuire sequenze di attività, vedere [Distribuire una sequenza di attività](../deploy-use/deploy-a-task-sequence.md).  

## <a name="export-and-import"></a><a name="BKMK_TSExportImport"></a> Esportazione e importazione

Configuration Manager consente di esportare e importare le sequenze di attività. Quando si esporta una sequenza di attività, è possibile includere gli oggetti cui fa riferimento tale sequenza.

Per altre informazioni, vedere [Esportare e importare sequenze di attività](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_ExportImport).  

## <a name="run-a-task-sequence"></a><a name="BKMK_TSRun"></a> Eseguire una sequenza di attività  

Le sequenze attività vengono sempre eseguite usando l'account di sistema locale. Quando si esegue la sequenza di attività, il client di Configuration Manager controlla la presenza di pacchetti con riferimenti prima di avviare i passaggi della sequenza di attività. Se non è possibile convalidare o scaricare un pacchetto con riferimenti, la sequenza di attività restituisce un errore per il passaggio della sequenza di attività associata.  

> [!Note]  
> Il passaggio della sequenza di attività **Esegui riga di comando** consente di eseguire un comando nel contesto di un account diverso.  

Se si configura una distribuzione della sequenza di attività per il download e l'esecuzione, il client di Configuration Manager scarica tutto il contenuto dipendente nella propria cache. Se le dimensioni della cache del client sono insufficienti o non è possibile trovare il contenuto, la sequenza di attività ha esito negativo. Il client genera un messaggio di stato.

È anche possibile specificare che il client scarichi il contenuto solo quando è necessario. Per eseguire questa azione, selezionare **Scaricare il contenuto localmente quando necessario eseguendo la sequenza di attività** nella distribuzione della sequenza di attività. Un'altra opzione è **Esegui programma dal punto di distribuzione**. Con questa opzione, il client installa i file direttamente dal punto di distribuzione senza scaricarli prima nella cache.

Quando si configura la distribuzione della sequenza di attività come **Disponibile**, se il client non riesce a individuare il contenuto dipendente per la sequenza di attività, invia immediatamente un errore. Per una distribuzione **Richiesta**, il client di Configuration Manager attende in questa situazione. Il client riprova a scaricare il contenuto fino alla scadenza, nel caso in cui quest'ultimo non sia già replicato in una posizione del contenuto accessibile al client.  

Quando una sequenza di attività viene completata correttamente o non riesce, Configuration Manager registra questo stato nella cronologia client.

Dopo l'avvio di una sequenza di attività in un computer, non è possibile annullarla o arrestarla.  

> [!IMPORTANT]  
> Se un passaggio di una sequenza di attività richiede il riavvio del computer, il client deve essere in grado di eseguire l'avvio di una partizione del disco formattato. In caso contrario, la sequenza di attività non riesce indipendentemente dalla gestione degli errori specificata nella sequenza di attività.  

Quando un oggetto dipendente di una sequenza di attività viene aggiornato a una nuova versione, le sequenze attività che fanno riferimento al pacchetto vengono automaticamente aggiornate e fanno riferimento alla versione più recente, indipendentemente dal numero di aggiornamenti distribuiti.  

## <a name="use-maintenance-windows"></a><a name="BKMK_TSMaintenanceWindow"></a> Usare finestre di manutenzione

È possibile specificare quando la sequenza di attività può essere eseguita definendo una finestra di manutenzione per la raccolta di dispositivi. Configurare le finestre di manutenzione con una data di inizio, un'ora di inizio e di fine e un criterio di ricorrenza. Quando si imposta la pianificazione della finestra di manutenzione, è possibile specificare che la finestra di manutenzione si applica solo alle sequenze di attività. Per altre informazioni, vedere [Come usare le finestre di manutenzione](../../core/clients/manage/collections/use-maintenance-windows.md).  

> [!IMPORTANT]  
> Quando si configura una finestra di manutenzione per l'esecuzione di una sequenza di attività, dopo l'avvio la sequenza di attività continua a essere eseguita anche se la finestra di manutenzione viene chiusa.  

Se a un dispositivo sono applicate più finestre di manutenzione, il client può ignorare una finestra **Tutte le distribuzioni**. A partire dalla versione 1810, usare l'impostazione client seguente per controllare questo comportamento: **Consenti l'installazione degli aggiornamenti software nella finestra di manutenzione "Tutte le distribuzioni" quando la finestra di manutenzione "Aggiornamento software" è disponibile**. Per altre informazioni, vedere [Informazioni sulle impostazioni client](../../core/clients/deploy/about-client-settings.md#bkmk_SUMMaint).<!-- SCCMDocs-pr #4596 -->


## <a name="task-sequences-and-the-network-access-account"></a><a name="BKMK_TSNetworkAccessAccount"></a> Sequenze di attività e account di accesso alla rete  

> [!Important]  
> Alcuni scenari di distribuzione del sistema operativo non richiedono l'uso dell'account di accesso alla rete. Per altre informazioni, vedere [HTTP migliorato](#enhanced-http).

Anche se le sequenze di attività vengono eseguite solo nel contesto dell'account di sistema locale, potrebbe essere necessario configurare l'[account di accesso alla rete](../../core/plan-design/hierarchy/accounts.md#network-access-account) nelle circostanze seguenti:  

- Se la sequenza di attività tenta di accedere al contenuto di Configuration Manager nei punti di distribuzione. Configurare correttamente l'account di accesso alla rete o la sequenza di attività avrà esito negativo.

- Quando si usa un'immagine di avvio per avviare una distribuzione del sistema operativo. In questo caso, Configuration Manager usa l'ambiente Windows PE, che non è un sistema operativo completo. L'ambiente Windows PE usa un nome casuale generato automaticamente che non è membro di nessun dominio. Se non si configura correttamente l'account di accesso alla rete, il computer non può accedere al contenuto necessario per la sequenza di attività.  

> [!NOTE]  
> L'account di accesso alla rete non viene mai usato come contesto di sicurezza per l'esecuzione di programmi, l'installazione di applicazioni, l'installazione di aggiornamenti o l'esecuzione di sequenze di attività. L'account di accesso alla rete viene usato solo per accedere alle risorse associate nella rete.  

Per altre informazioni sull'account di accesso alla rete, vedere [Account di accesso alla rete](../../core/plan-design/hierarchy/accounts.md#network-access-account).  

### <a name="enhanced-http"></a>HTTP avanzato
<!--1358278-->

Quando si abilita **HTTP avanzato**, gli scenari seguenti non richiedono un account di accesso alla rete per scaricare il contenuto da un punto di distribuzione:

- Sequenze di attività in esecuzione da supporti di avvio o PXE  
- Sequenze di attività in esecuzione da Software Center  

Queste sequenze di attività possono essere per la distribuzione del sistema operativo o personalizzate. Sono supportate anche per i computer del gruppo di lavoro.

Per altre informazioni, vedere [HTTP migliorato](../../core/plan-design/hierarchy/enhanced-http.md).  

> [!Note]  
> I seguenti scenari di distribuzione del sistema operativo richiedono ancora l'uso dell'account di accesso alla rete:
>  
> - L'[opzione di distribuzione](../deploy-use/deploy-a-task-sequence.md)**Accedere al contenuto direttamente da un punto di distribuzione quando necessario eseguendo la sequenza di attività** della sequenza di attività
> - L'opzione [Se l'account del computer non riesce a connettersi all'archiviazione stati, utilizzare l'account di accesso di rete](../understand/task-sequence-steps.md#BKMK_RequestStateStore) del passaggio **Richiedi archiviazione stati**
> - Quando si effettua la connessione con un dominio non trusted o in foreste di Active Directory
> - L'opzione [Accedi al contenuto direttamente dal punto di distribuzione](../understand/task-sequence-steps.md#BKMK_ApplyOperatingSystemImage) del passaggio **Applica immagine del sistema operativo**
> - L'[impostazione avanzata](../deploy-use/manage-task-sequences-to-automate-tasks.md#bkmk_prop-advanced)**Esegui prima un altro programma** della sequenza di attività
> - [Multicast](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md)  

## <a name="create-media"></a><a name="BKMK_TSCreateMedia"></a> Creare supporti

È possibile scrivere le sequenze attività e le dipendenze e i file correlati in diversi tipi di supporto. Configuration Manager supporta un supporto rimovibile, ad esempio un DVD o un'unità flash USB per i supporti di acquisizione, autonomi e di avvio. I supporti preinstallati usano un file di immagine (WIM) di Windows.  

Quando si creano supporti, specificare una password per controllare l'accesso. Una persona deve quindi immettere la password nel computer di destinazione per l'esecuzione della sequenza di attività.  

Quando si esegue una sequenza di attività dai supporti, l'architettura del processore specificata dei supporti non viene riconosciuta. Se l'architettura specificata non corrisponde al computer di destinazione, verrà comunque eseguito un tentativo di esecuzione della sequenza di attività. Se l'architettura dei supporti non corrisponde all'architettura del computer di destinazione, la sequenza di attività ha esito negativo.  

Per altre informazioni, vedere [Creare supporti per sequenza di attività](../deploy-use/create-task-sequence-media.md).  

### <a name="media-types"></a>Tipi di supporti

Configuration Manager supporta i tipi di supporti seguenti:  

#### <a name="capture-media"></a>Supporti di acquisizione

Questi supporti acquisiscono un'immagine del sistema operativo configurata e creata al di fuori dell'infrastruttura di Configuration Manager. I supporti di acquisizione possono contenere programmi personalizzati eseguibili prima dell'esecuzione di una sequenza di attività. Il programma personalizzato può interagire con il desktop, richiedere valori di input all'utente o creare variabili che verranno usate dalla sequenza di attività.  

Per altre informazioni, vedere [Creare supporti di acquisizione](../deploy-use/create-capture-media.md).  

#### <a name="stand-alone-media"></a>Supporti autonomi

I supporti autonomi contengono la sequenza di attività e tutti gli oggetti associati necessari per l'esecuzione della sequenza di attività. Le sequenze di attività dei supporti autonomi possono essere eseguite quando Configuration Manager ha limitata o nessuna connettività alla rete. Eseguire i supporti autonomi nei modi seguenti:  

- Se il computer di destinazione non viene avviato, viene usata l'immagine di Windows PE associata alla sequenza di attività a partire dai supporti autonomi e la sequenza di attività ha inizio.  

- Avviare manualmente i supporti autonomi. Se un utente è connesso al computer, può avviare la sequenza di attività dai supporti.  

> [!IMPORTANT]  
> I passaggi di una sequenza di attività su supporti autonomi devono poter essere eseguiti senza recuperare nessun dato dalla rete. In caso contrario, il passaggio della sequenza di attività che cerca di recuperare i dati ha esito negativo. Ad esempio, un passaggio di una sequenza di attività che richiede un punto di distribuzione per ottenere un pacchetto ha esito negativo. Se i supporti autonomi contengono il pacchetto necessario, il passaggio della sequenza di attività ha esito positivo.  

Per altre informazioni, vedere [Creare supporti autonomi](../deploy-use/create-stand-alone-media.md).  

#### <a name="bootable-media"></a>Supporto di avvio

I supporti di avvio contengono i file necessari per avviare un computer di destinazione in modo che possa connettersi all'infrastruttura di Configuration Manager per determinare quali sequenze di attività eseguire in base all'appartenenza a una raccolta. Questi supporti non includono la sequenza di attività o gli oggetti dipendenti. Al contrario, il client scarica il contenuto attraverso la rete. Questo metodo è utile per i nuovi computer o per le distribuzioni bare metal, quando nel computer di destinazione non è presente alcun sistema operativo.  

Per altre informazioni, vedere [Creare supporti di avvio](../deploy-use/create-bootable-media.md).  

#### <a name="prestaged-media"></a>Supporto pre-installato

I supporti pre-installati distribuiscono un'immagine del sistema operativo in un computer di destinazione di cui non viene effettuato il provisioning. I supporti pre-installati vengono archiviati come file di immagine (WIM) di Windows. Questo file può essere installato in un computer bare metal dal produttore o in un centro di gestione temporanea aziendale. Un vantaggio dei supporti pre-installati è che queste posizioni non richiedono una connessione all'ambiente di Configuration Manager.  

Per altre informazioni, vedere [Creare supporti preinstallati](../deploy-use/create-prestaged-media.md).  

## <a name="next-steps"></a>Passaggi successivi

- [Sicurezza e privacy per la distribuzione del sistema operativo](security-and-privacy-for-operating-system-deployment.md)

- [Preparare i ruoli del sistema del sito per le distribuzioni del sistema operativo](../get-started/prepare-site-system-roles-for-operating-system-deployments.md)
