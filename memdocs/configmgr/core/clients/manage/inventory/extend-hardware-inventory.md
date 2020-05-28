---
title: Estendere l'inventario hardware
titleSuffix: Configuration Manager
description: Informazioni su come estendere l'inventario hardware in Configuration Manager.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d5bfab4f-c55e-4545-877c-5c8db8bc1891
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 39e88debf5c25fb3a033c322e37663549ead29fd
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83427701"
---
# <a name="how-to-extend-hardware-inventory-in-configuration-manager"></a>Come estendere l'inventario hardware in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

L'inventario hardware legge le informazioni dai PC Windows usando Strumentazione gestione Windows (WMI). WMI è l'implementazione Microsoft di Web-Based Enterprise Management (WBEM), uno standard del settore per l'accesso alle informazioni di gestione in ambiente aziendale. Nelle versioni precedenti di Configuration Manager, per estendere l'inventario hardware si modificava il file sms_def.mof nel server del sito. Questo file contiene un elenco di classi WMI che può essere letto dall'inventario hardware. Modificando questo file, è possibile abilitare e disabilitare classi esistenti e creare anche nuove classi nell'inventario.  

Il file Configuration.mof, usato per definire le classi di dati da inserire nell'inventario hardware nel client, è rimasto lo stesso da Configuration Manager 2012. È possibile creare classi di dati per effettuare un inventario di classi di dati di repository WMI esistenti o personalizzate o chiavi del Registro di sistema presenti nei sistemi client.  

 Il file Configuration.mof definisce e registra anche i provider WMI che accedono alle informazioni durante l'inventario hardware. Registrazione dei provider definisce il tipo di provider da utilizzare e le classi supportate dal provider.  

 Quando i client di Configuration Manager richiedono criteri, si allega il file Configuration.mof al corpo dei criteri. Questo file viene quindi scaricato e compilato dai client. Quando si aggiungere, modificare o eliminano classi di dati dal file MOF, i client compilare automaticamente le modifiche apportate alle classi di dati correlati al magazzino. Non sono necessarie altre azioni per eseguire l'inventario di classi di dati nuove o modificate nei client di Configuration Manager. Questo file si trova in **<PercorsoInstallazioneCM\>\Inboxes\clifiles.src\hinv\\** sui server del sito primario.  

 In Configuration Manager non è più possibile modificare il file sms_def.mof come in Configuration Manager 2007. È invece possibile abilitare e disabilitare le classi WMI e aggiungere nuove classi che dovranno essere raccolte dall'inventario hardware usando le impostazioni client. Configuration Manager mette a disposizione i metodi seguenti per estendere l'inventario hardware.  

> [!NOTE]  
>  Se il file Configuration.mof è stato modificato manualmente per aggiungere classi di inventario personalizzate, queste modifiche vengono sovrascritte quando si esegue l'aggiornamento alla versione 1602. Per continuare a usare le classi personalizzate dopo l'aggiornamento, è necessario aggiungerle alla sezione relativa alle estensioni aggiunte del file Configuration.mof dopo l'aggiornamento alla versione 1602.  
> È tuttavia necessario evitare di modificare le sezioni che precedono questa, perché sono riservate alle modifiche da parte di Configuration Manager. Un backup del file Configuration.mof personalizzato è disponibile in:  
> **<Directory installazione CM\>\data\hinvarchive\\** .  

## <a name="methods"></a>Metodi

### <a name="enable-or-disable"></a>Abilitare o disabilitare

Abilitare o disabilitare alcuni degli attributi di una classe già esistente nel client. Questa azione indica all'agente di inventario hardware di raccogliere la classe nei client. È possibile eseguire questa azione in impostazioni client predefinite o impostazioni client dispositivo personalizzate. Per altre informazioni, vedere [Abilitare o disabilitare classi di inventario esistenti](#BKMK_Enable).

### <a name="add"></a>Aggiunta

Se una classe WMI esiste nel client ed è nota al sito, questa azione la include nel set di classi di inventario hardware possibili. È possibile aggiungere una nuova classe di inventario dello spazio dei nomi WMI di un altro dispositivo. Questa azione è disponibile solo per le impostazioni client predefinite. Per altre informazioni, vedere [Aggiungere una nuova classe di inventario](#BKMK_Add).

### <a name="extend"></a>Extend

Aggiungere una nuova classe WMI al client. Per estendere manualmente l'inventario hardware, modificare il file configuration.mof nel sito di livello superiore.<!-- SCCMDocs#1073 -->

Se la classe WMI non esiste nel client, è necessario estendere lo schema WMI:

1. Modificare il file configuration.mof nel sito di livello superiore. Esaminare **dataldr.log** per visualizzare il sito in cui è stato aggiunto.

1. Aggiornare i criteri in un client e attendere che la nuova classe venga compilata.

1. Usare le impostazioni client predefinite per [aggiungere](#add) la nuova classe all'inventario hardware. Non è necessario abilitare questa classe nelle impostazioni client predefinite. È quindi possibile abilitarla in un'impostazione client di dispositivo personalizzata.

### <a name="import-and-export"></a>Importare ed esportare

Usare la console di Configuration Manager per importare ed esportare file Managed Object Format (MOF) che contengono le classi di inventario. Per altre informazioni, vedere [Importare classi di inventario hardware](#BKMK_Import) ed [Esportare classi di inventario hardware](#BKMK_Export).

### <a name="create-noidmif-files"></a>Creare file NOIDMIF

Usare file NOIDMIF per raccogliere informazioni sui dispositivi client che non possono essere inclusi nell'inventario da Configuration Manager. Ad esempio, raccogliere informazioni sui numeri delle risorse dispositivo che esistono solo come etichetta sul dispositivo. Inventario NOIDMIF viene associato automaticamente al dispositivo raccolti dai client. Per altre informazioni, vedere [Creare file NOIDMIF](#BKMK_NOIDMIF).

### <a name="create-idmif-files"></a>Creare i file IDMIF

Usare i file IDMIF per raccogliere informazioni sulle risorse dell'organizzazione non associate a un client di Configuration Manager, ad esempio proiettori, fotocopiatrici e stampanti di rete. Per altre informazioni, vedere [Creare file IDMIF](#BKMK_IDMIF).

## <a name="procedures-to-extend-hardware-inventory"></a>Procedure per estendere l'inventario hardware

Queste procedure consentono di configurare le impostazioni client predefinite per l'inventario hardware e si applicano a tutti i client nella gerarchia. Per applicare queste impostazioni solo ad alcuni client, creare un'impostazione di dispositivo client personalizzata e assegnarla a una raccolta di client specifici. Per altre informazioni, vedere [Come configurare le impostazioni client](../../../../core/clients/deploy/configure-client-settings.md).  

### <a name="enable-or-disable-existing-inventory-classes"></a><a name="BKMK_Enable"></a> Abilitare o disabilitare classi di inventario esistenti  

1. Nella console di Configuration Manager selezionare **Amministrazione** > **Impostazioni client** > **Impostazioni client predefinite**.  

1. Nella scheda **Home**, nel gruppo **Proprietà**, fare clic su **Proprietà**.  

1. Nella finestra di dialogo **Impostazioni client predefinite** scegliere **Inventario hardware**.  

1. Nell'elenco **Impostazioni dispositivo** selezionare **Imposta classi**.  

1. Nel **classi di inventario Hardware** finestra di dialogo selezionare o deselezionare le classi e proprietà della classe deve essere raccolto dall'inventario hardware. È possibile espandere le classi per selezionare o deselezionare le singole proprietà di tale classe. Utilizzare il **ricerca di classi di inventario** campo per la ricerca di singole classi.  

    > [!IMPORTANT]  
    >  Quando si aggiungono nuove classi all'inventario hardware di Configuration Manager, le dimensioni del file di inventario raccolto e inviato al server del sito aumentano. Ciò potrebbe influire negativamente sulle prestazioni della rete e del sito di Configuration Manager. Abilitare solo le classi di inventario che si desidera raccogliere.  

### <a name="add-a-new-inventory-class"></a><a name="BKMK_Add"></a> Aggiungere una nuova classe di inventario  

È possibile aggiungere classi di inventario solo dal server di livello superiore della gerarchia modificando le impostazioni client predefinite. Questa opzione non è disponibile quando si creano impostazioni dispositivo personalizzate.

1. Nella console di Configuration Manager selezionare **Amministrazione** > **Impostazioni client** > **Impostazioni client predefinite**.  

1. Nella scheda **Home**, nel gruppo **Proprietà**, fare clic su **Proprietà**.  

1. Nella finestra di dialogo **Impostazioni client predefinite** scegliere **Inventario hardware**.  

1. Nell'elenco **Impostazioni del dispositivo** scegliere **Imposta classi**.  

1. Nella finestra di dialogo **Classi di inventario hardware** scegliere **Aggiungi**.  

1. Nella finestra di dialogo **Aggiungi classe di inventario hardware** selezionare **Connetti**.  

1. Nella finestra di dialogo **Connetti a Windows Management Instrumentation (WMI)** specificare il nome del computer da cui si recupereranno le classi WMI e lo spazio dei nomi WMI da usare per recuperare le classi. Se si vogliono recuperare tutte le classi sotto lo spazio dei nomi WMI specificato, selezionare **Ricorsivo**. Se il computer cui si è connessi non è il computer locale, specificare le credenziali per un account con autorizzazione di accesso a WMI sul computer remoto.

1. Scegliere **Connetti**.  

1. Nell'elenco **Classi di inventario hardware** nella finestra di dialogo **Aggiungi classe di inventario hardware** selezionare le classi WMI da aggiungere all'inventario hardware di Configuration Manager.  

1. Se si vogliono modificare le informazioni sulla classe WMI selezionata, scegliere **Modifica** e immettere le informazioni seguenti nella finestra di dialogo **Qualificatori di classe**:  

    - **Nome visualizzato**: questo nome verrà visualizzato in Esplora inventario risorse.  

    - **Proprietà**: specificare le unità in cui verrà visualizzata ogni proprietà della classe WMI.  

      È anche possibile impostare proprietà come proprietà chiave per identificare in modo univoco ogni istanza della classe. Se è stata definita alcuna chiave per la classe e più istanze della classe vengono segnalate dal client, viene archiviata solo l'istanza più recente viene trovata nel database.  

      Al termine della configurazione delle proprietà, selezionare **OK** per chiudere la finestra di dialogo **Qualificatori di classe** e le altre finestre di dialogo aperte.

### <a name="import-hardware-inventory-classes"></a><a name="BKMK_Import"></a> Importare classi di inventario hardware

Quando si modificano le impostazioni client predefinite, è possibile importare solo le classi di inventario. È tuttavia possibile usare impostazioni client personalizzate per importare informazioni che non includano una modifica dello schema, ad esempio la modifica della proprietà di una classe esistente da **True** a **False**.  

1. Nella console di Configuration Manager selezionare **Amministrazione** >  **Impostazioni client** > **Impostazioni client predefinite**.

1. Nella scheda **Home**, nel gruppo **Proprietà**, fare clic su **Proprietà**.  

1. Nella finestra di dialogo **Impostazioni client predefinite** scegliere **Inventario hardware**.  

1. Nell'elenco **Impostazioni del dispositivo** scegliere **Imposta classi**.  

1. Nella finestra di dialogo **Classi di inventario hardware** scegliere **Importa**.  

1. Nella finestra di dialogo **Importa** selezionare il file Managed Object Format (MOF) che si vuole importare e quindi scegliere **OK**. Controllare gli elementi che verranno importati e selezionare **Importa**.  

### <a name="export-hardware-inventory-classes"></a><a name="BKMK_Export"></a> Esportare classi di inventario hardware  

1. Nella console di Configuration Manager selezionare **Amministrazione** > **Impostazioni client** > **Impostazioni client predefinite**.  

1. Nella scheda **Home**, nel gruppo **Proprietà**, fare clic su **Proprietà**.  

1. Nella finestra di dialogo **Impostazioni client predefinite** scegliere **Inventario hardware**.  

1. Nell'elenco **Impostazioni del dispositivo** scegliere **Imposta classi**.  

1. Nella finestra di dialogo **Classi di inventario hardware** scegliere **Esporta**.  

    > [!NOTE]  
    > Quando si esportano le classi, verranno esportate tutte le classi attualmente selezionate.  

1. Nella finestra di dialogo **Esporta** selezionare il file Managed Object Format (MOF) in cui esportare le classi e quindi scegliere **Salva**.  

### <a name="configure-hardware-inventory-to-collect-strings-larger-than-255-characters"></a><a name="bkmk_GreaterThan255"></a> Configurare l'inventario hardware per raccogliere stringhe maggiori di 255 caratteri

Per le proprietà dell'inventario hardware è possibile specificare che la lunghezza delle stringhe sia maggiore di 255 caratteri. Questa azione si applica solo alle nuove classi aggiunte e alle proprietà dell'inventario hardware diverse dalle chiavi. <!-- 1357389 -->

1. Nell'area di lavoro **Amministrazione** selezionare **Impostazioni client**. Scegliere un'impostazione del dispositivo client da modificare e selezionare **Proprietà**.

1. Selezionare **Inventario hardware**, quindi **Imposta classi** e **Aggiungi**.

1. Selezionare **Connetti**.

1. Compilare i campi **Nome computer**, **Spazio dei nomi WMI** e selezionare **ricorsivo** se necessario. Immettere le credenziali, se necessarie per la connessione. Selezionare **Connetti** per visualizzare le classi dello spazio dei nomi.

1. Selezionare una nuova classe e quindi **Modifica**.

1. Modificare il valore **Lunghezza** della proprietà stringa, che non sia la chiave, in modo che sia maggiore di 255. Selezionare **OK**.

1. Assicurarsi che la proprietà modificata sia selezionata per **Aggiungi classe di inventario hardware** e selezionare **OK**.

## <a name="use-mif-files-to-extend-hardware-inventory"></a>Usare file MIF per estendere l'inventario hardware

Usare file MIF per estendere le informazioni dell'inventario hardware che Configuration Manager ha raccolto dai client. Durante l'inventario hardware, le informazioni archiviate nel file MIF viene aggiunto al report di inventario client e archiviate nel database del sito, dove è possibile utilizzare i dati nello stesso modo di utilizzare dati di inventario client predefinito. Esistono due tipi di file MIF: NOIDMIF e IDMIF.

> [!IMPORTANT]  
> Prima di aggiungere al database di Configuration Manager informazioni dei file MIF, è necessario creare o importare informazioni relative alla classe per tali informazioni. Per altre informazioni, vedere le sezioni [Per aggiungere una nuova classe di inventario](#BKMK_Add) e [Per importare classi di inventario hardware](#BKMK_Import) in questo articolo.  

### <a name="create-noidmif-files"></a><a name="BKMK_NOIDMIF"></a> Creare file NOIDMIF

I file NOIDMIF possono essere usati per aggiungere a un inventario hardware client informazioni che normalmente Configuration Manager non riesce a raccogliere. Questi file sono associati a dispositivi client specifici. Molte società, ad esempio, etichettano ogni computer dell'organizzazione con un numero di asset e quindi li catalogano manualmente. Quando si crea un file NOIDMIF, è possibile aggiungere queste informazioni al database di Configuration Manager e usarle per le query e la creazione di report. Per informazioni sulla creazione di file NOIDMIF, vedere la documentazione di Configuration Manager SDK.  

> [!IMPORTANT]  
> Quando si crea un file NOIDMIF, è necessario salvarlo in un formato con codifica ANSI. I file NOIDMIF salvati in formato con codifica UTF-8 non sono leggibili per Configuration Manager.  

Dopo aver creato un file NOIDMIF, archiviarlo nella cartella `%Windir%\CCM\Inventory\Noidmifs` di ogni client. Configuration Manager raccoglierà informazioni dai file NODMIF in questa cartella durante il successivo ciclo di inventario hardware pianificato.  

### <a name="create-idmif-files"></a><a name="BKMK_IDMIF"></a> Creare file IDMIF

I file IDMIF possono essere usati per aggiungere al database di Configuration Manager informazioni sugli asset di cui Configuration Manager non può normalmente eseguire l'inventario e che non sono associati a un dispositivo client specifico. È possibile, ad esempio, usare file IDMIF per raccogliere informazioni su proiettori, lettori DVD, fotocopiatrici o altre apparecchiature che non hanno un client Configuration Manager. Per informazioni sulla creazione di file IDMIF, vedere la documentazione di Configuration Manager SDK.  

Dopo aver creato un file IDMIF, archiviarlo nella cartella `%Windir%\CCM\Inventory\Idmifs` dei computer client. Configuration Manager raccoglierà informazioni da questo file durante il successivo ciclo di inventario hardware pianificato. Dichiarare nuove classi per le informazioni contenute nel file aggiungendole o importandole.  

> [!NOTE]
> I file MIF potrebbero contenere grandi quantità di dati e la raccolta di tali dati potrebbe influire negativamente sulle prestazioni del sito. Abilitare la raccolta di file MIF solo quando necessario e configurare l'opzione **Dimensioni massime file MIF personalizzate (KB)** nelle impostazioni relative all'inventario hardware. Per altre informazioni, vedere [Introduzione all'inventario hardware](introduction-to-hardware-inventory.md).
