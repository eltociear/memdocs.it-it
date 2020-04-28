---
title: Gestire le immagini di avvio
titleSuffix: Configuration Manager
description: Informazioni su come gestire le immagini d'avvio di Windows PE usate durante la distribuzione di un sistema operativo in Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 97f2d81a-2c58-442c-88bc-defd5a1cd48f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1166d4c674207ed3590901465ca90a98ce3ae78f
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075065"
---
# <a name="manage-boot-images-with-configuration-manager"></a>Gestire le immagini d'avvio con Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Un'immagine d'avvio in Configuration Manager è un'immagine [Windows PE](https://docs.microsoft.com/windows-hardware/manufacture/desktop/winpe-intro) (WinPE) che viene usata durante la distribuzione di un sistema operativo. Le immagini d'avvio si usano per avviare un computer in WinPE. Questo sistema operativo di base contiene servizi e componenti limitati. Configuration Manager usa WinPE per preparare il computer di destinazione per l'installazione di Windows.

## <a name="default-boot-images"></a><a name="BKMK_BootImageDefault"></a> Immagini d'avvio predefinite

In Configuration Manager sono disponibili due immagini d'avvio predefinite: una per il supporto delle piattaforme x86 e una per il supporto delle piattaforme x64. Queste immagini sono archiviate nelle cartelle *x64* o *i386* nella condivisione seguente nel server del sito: `\\<SiteServerName>\SMS_<sitecode>\osd\boot\`. Le immagini di avvio predefinite vengono aggiornate o rigenerate in base all'azione eseguita.

Tenere presente i comportamenti seguenti per le azioni descritte per le immagini d'avvio predefinite:

- Gli oggetti driver di origine devono essere validi. Questi oggetti includono i file di origine del driver. Se gli oggetti non sono validi, il sito non aggiunge i driver alle immagini d'avvio.  

- Le immagini d'avvio che non sono basate sulle immagini d'avvio predefinite, anche se usano la stessa versione di Windows PE, non vengono modificate.  

- Ridistribuire le immagini d'avvio modificate ai punti di distribuzione.  

- Ricreare i supporti che usano le immagini d'avvio modificate.  

- Se si preferisce non aggiornare automaticamente le immagini d'avvio personalizzate/predefinite, non archiviarle nella posizione predefinita.  

> [!NOTE]
> Lo strumento di log di Configuration Manager (**CMTrace**) viene aggiunto a tutte le immagini d'avvio presenti nella **Raccolta software**. In Windows PE, avviare lo strumento digitando `cmtrace` dal prompt dei comandi.
>
> CMTrace è il visualizzatore predefinito per i file di log in Windows PE.

### <a name="use-updates-and-servicing-to-install-the-latest-version-of-configuration-manager"></a>Usare gli aggiornamenti e le versioni di manutenzione per installare la versione più recente di Configuration Manager

Quando si aggiorna la versione di Windows Assessment and Deployment Kit (ADK) e quindi si usano gli aggiornamenti e le versioni di manutenzione per installare la versione più recente di Configuration Manager, il sito rigenera le immagini d'avvio predefinite. Questo aggiornamento include la nuova versione di WinPE contenuta nella versione aggiornata di Windows ADK, la nuova versione del client di Configuration Manager, i driver e le personalizzazioni. Il sito non modifica le immagini d'avvio personalizzate.

### <a name="upgrade-from-configuration-manager-2012-to-current-branch"></a>Eseguire l'aggiornamento da Configuration Manager 2012 a Current Branch

Quando si esegue l'aggiornamento di Configuration Manager 2012 alla versione Current Branch, il sito rigenera le immagini d'avvio predefinite. Questo aggiornamento include la nuova versione di WinPE contenuta nella versione aggiornata di Windows ADK e la nuova versione del client di Configuration Manager. Tutte le personalizzazioni delle immagini d'avvio rimangono invariate. Il sito non modifica le immagini d'avvio personalizzate.

### <a name="update-distribution-points-with-the-boot-image"></a>Aggiornare i punti di distribuzione con l'immagine d'avvio

Quando si usa l'azione **Aggiorna punti di distribuzione** dal nodo **Immagini d'avvio** nella console, il sito aggiorna le immagini d'avvio di destinazione con i componenti client, i driver e le personalizzazioni.

È possibile ricaricare l'immagine d'avvio con la versione più recente di WinPE dalla directory di installazione di Windows ADK. La pagina **Generale** dell'Aggiornamento guidato punti di distribuzione contiene le informazioni seguenti:

- La versione corrente di Windows ADK installata nel server del sito
- La versione corrente del client di produzione
- La versione Windows ADK di WinPE nell'immagine d'avvio
- La versione del client di Configuration Manager nell'immagine d'avvio

Se le versioni nell'immagine d'avvio non sono aggiornate, usare l'opzione **Ricarica questa immagine d'avvio con la versione corrente di Windows PE da Windows ADK**.

> [!Important]  
> Questa azione è disponibile sia per le immagini d'avvio predefinite che per quelle personalizzate. Durante questo processo per ricaricare l'immagine d'avvio, il sito non mantiene eventuali personalizzazioni manuali eseguite di fuori di Configuration Manager. Queste personalizzazioni includono le estensioni di terze parti. Questa opzione consente di ricompilare l'immagine d'avvio usando la versione più recente di WinPE e l'ultima versione del client. Solo le configurazioni specificate nelle proprietà dell'immagine d'avvio vengono riapplicate. <!--SCCMDocs issue #1283-->

Il nodo **Immagini d'avvio** include anche una nuova colonna per (**Versione client**). Usare questa colonna per visualizzare rapidamente la versione del client di Configuration Manager in ogni immagine d'avvio.

## <a name="customize-a-boot-image"></a><a name="BKMK_BootImageCustom"></a> Personalizzare un'immagine d'avvio  

Quando un'immagine d'avvio è basata sulla versione di WinPE della versione supportata di Windows ADK, è possibile personalizzare o [modificare un'immagine d'avvio](#BKMK_ModifyBootImages) dalla console. Quando si aggiorna un sito e si installa una nuova versione di Windows ADK, le immagini d'avvio personalizzate non vengono aggiornate con la nuova versione di Windows ADK. In questi casi, non è possibile personalizzare le immagini d'avvio nella console di Configuration Manager. Queste immagini continueranno tuttavia a funzionare come prima dell'aggiornamento.  

Quando un'immagine d'avvio è basata su una versione di Windows ADK diversa da quella installata in un sito, è necessario personalizzarla. Per personalizzare queste immagini d'avvio usare un altro metodo, ad esempio lo strumento da riga di comando Gestione e manutenzione immagini distribuzione. Gestione e manutenzione immagini distribuzione è incluso in Windows ADK. Per altre informazioni, vedere [Customize boot images](customize-boot-images.md) (Personalizzare le immagini d'avvio).  

## <a name="add-a-boot-image"></a><a name="BKMK_AddBootImages"></a> Aggiungere un'immagine d'avvio  

Durante l'installazione del sito, Configuration Manager aggiunge automaticamente immagini d'avvio basate su una versione di WinPE dalla versione supportata di Windows ADK. A seconda della versione di Configuration Manager, è possibile aggiungere immagini d'avvio basate su una diversa versione di WinPE dalla versione supportata di Windows ADK. Quando si prova ad aggiungere un'immagine d'avvio che contiene una versione non supportata di WinPE si verifica un errore. L'elenco seguente include le versioni di Windows ADK e WinPE attualmente supportate:

|  |  |
|---------|---------|
| Versione di Windows ADK | Windows ADK per Windows 10 |
| Versioni di Windows PE per le immagini d'avvio personalizzabili dalla console di Configuration Manager | Windows PE 10 |
| Versioni di Windows PE supportate per le immagini d'avvio *non personalizzabili* dalla console di Configuration Manager | - Windows PE 3.1<sup>[Nota 1](#bkmk_note1)</sup> <br> - Windows PE 5 |

Ad esempio, usare la console di Configuration Manager per personalizzare le immagini d'avvio basate su Windows PE 10 di Windows ADK per Windows 10. Nel caso di un'immagine d'avvio basata su Windows PE 5, personalizzarla in un altro computer usando la versione di Gestione e manutenzione immagini distribuzione di Windows ADK per Windows 8. Aggiungere quindi l'immagine d'avvio personalizzata alla console di Configuration Manager. Per altre informazioni, vedere gli articoli seguenti:

- [Personalizzare le immagini di avvio](customize-boot-images.md)
- [Supporto per Windows 10 ADK](../../core/plan-design/configs/support-for-windows-10.md#windows-10-adk)
- [DISM supported platforms](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms) (Piattaforme supportate per Gestione e manutenzione immagini distribuzione)

<a name="bkmk_note1"></a>

> [!NOTE]
> **Nota 1: Supporto per Windows PE 3.1**
>
> Aggiungere un'immagine d'avvio a Configuration Manager solo se è basata su Windows PE *versione 3.1*. Aggiornare Windows AIK per Windows 7 (basato su Windows PE 3.0) con il supplemento Windows AIK per Windows 7 SP1 (basato su Windows PE 3.1). Scaricare il supplemento Windows AIK per Windows 7 SP1 dall'[Area download Microsoft](https://www.microsoft.com/download/details.aspx?id=5188).  

1. Nella console di Configuration Manager passare all'area di lavoro **Raccolta software**, espandere **Sistemi operativi** e quindi selezionare il nodo **Immagini d'avvio**.  

2. Nella scheda **Home** della barra multifunzione, nel gruppo **Crea** selezionare **Aggiungi immagine d'avvio**. Questa azione avvia l'Aggiunta guidata immagine d'avvio.  

3. Nella pagina **Origine dati** specificare le opzioni seguenti:  

    - Nella casella **Percorso** specificare il percorso del file WIM dell'immagine di avvio. Il percorso specificato deve essere un percorso di rete valido in formato UNC. ad esempio `\\ServerName\ShareName\BootImageName.wim`

    - Selezionare l'immagine di avvio dall'elenco a discesa **Immagine di avvio** . Se il file WIM contiene più immagini d'avvio, selezionare l'immagine appropriata.  

4. Nella pagina **Generale** specificare le opzioni seguenti:  

    - Nella casella **Nome** specificare un nome univoco per l'immagine di avvio.  

    - Nella casella **Versione** specificare un numero di versione per l'immagine di avvio.  

    - Nella casella **Commento** specificare una breve descrizione di come viene usata l'immagine d'avvio.  

5. Completare la procedura guidata.  

L'immagine d'avvio viene ora elencata nel nodo **Immagine d'avvio**. Prima di usare l'immagine d'avvio per distribuire un sistema operativo, distribuirla ai punti di distribuzione.

> [!Tip]  
> Nel nodo **Immagine d'avvio** della console la colonna **Dimensione (KB)** visualizza la dimensione decompressa per ogni immagine d'avvio. Quando il sito invia un'immagine d'avvio in rete, ne invia una copia compressa. Le dimensioni di questa copia sono in genere inferiori rispetto a quelle indicate nella colonna **Dimensione (KB)** .  

## <a name="distribute-boot-images"></a><a name="BKMK_DistributeBootImages"></a> Distribuire immagini d'avvio  

Le immagini di avvio vengono distribuite nei punti di distribuzione nello stesso modo in cui vengono distribuiti gli altri contenuti. Prima di distribuire un sistema operativo o creare un supporto, distribuire l'immagine d'avvio in almeno un punto di distribuzione.

Per altre informazioni su come distribuire un'immagine d'avvio, vedere [Distribuire il contenuto](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

Per usare PXE per la distribuzione di un sistema operativo, prima di distribuire l'immagine d'avvio tenere presente i punti seguenti:  

- Configurare il punto di distribuzione in modo che accetti le richieste PXE.  
- Distribuire un'immagine d'avvio x86 e una x64 abilitate per PXE in almeno un punto di distribuzione che supporta PXE.  
- Configuration Manager distribuisce l'immagine d'avvio nella cartella **RemoteInstall** del punto di distribuzione abilitato per PXE.  
  
Per altre informazioni sull'uso di PXE per la distribuzione di sistemi operativi, vedere [Usare PXE per distribuire Windows in rete](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

## <a name="modify-a-boot-image"></a><a name="BKMK_ModifyBootImages"></a> Modificare un'immagine d'avvio  

Aggiungere o rimuovere driver di dispositivo dall'immagine o modificare le proprietà dell'immagine d'avvio. I driver aggiunti o rimossi possono includere i driver di rete o di archiviazione. Quando si modificano le immagini di avvio, tenere presente quanto segue:  

- Prima di aggiungere driver all'immagine d'avvio, è necessario importarli e abilitarli nel catalogo dei driver di dispositivo.  

- Quando si modifica un'immagine d'avvio, l'immagine non modifica i pacchetti associati a cui fa riferimento.  

- Dopo aver apportato modifiche a un'immagine d'avvio, **aggiornarla** nei punti di distribuzione in cui è già presente. Grazie a questo processo, i client avranno a disposizione la versione più recente dell'immagine d'avvio. Per altre informazioni, vedere [Gestire il contenuto distribuito](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_manage).  

### <a name="modify-the-properties-of-a-boot-image"></a>Modificare le proprietà di un'immagine di avvio  

1. Nella console di Configuration Manager passare all'area di lavoro **Raccolta software**, espandere **Sistemi operativi** e quindi selezionare il nodo **Immagini d'avvio**.  

2. Selezionare l'immagine di avvio da modificare.  

3. Nella scheda **Home** della barra multifunzione selezionare **Proprietà** nel gruppo **Proprietà**.  

4. Impostare le seguenti impostazioni per modificare il comportamento dell'immagine di avvio:  

#### <a name="images"></a>Immagini

Nella scheda **Immagini**, se si modificano le proprietà dell'immagine d'avvio usando uno strumento esterno, selezionare **Ricarica**.  

#### <a name="drivers"></a>Driver

Nella scheda **Driver** aggiungere i driver di dispositivo di Windows richiesti per l'avvio di WinPE. Quando si aggiungono i driver di dispositivo, tenere presente i punti seguenti:  

- Verificare che i driver aggiunti all'immagine d'avvio corrispondano all'architettura dell'immagine d'avvio.  

- Per visualizzare solo i driver relativi all'architettura dell'immagine d'avvio, selezionare **Nascondi driver che non corrispondono all'architettura dell'immagine d'avvio**. L'architettura del driver è basata su quella indicata nel file INF fornito dal produttore.  

- WinPE include già molti driver predefiniti. Aggiungere solo i driver di rete e archiviazione che non sono inclusi in WinPE.  

- Aggiungere all'immagine d'avvio solo i driver di rete e di archiviazione, a meno che WinPE non richieda altri driver.  

- Per visualizzare solo i driver di archiviazione e di rete, selezionare **Nascondi driver non inclusi in una classe di archiviazione o di rete (per immagini d'avvio)** . Questa opzione consente di nascondere anche altri driver in genere non necessari per le immagini d'avvio, ad esempio i driver video o quelli per modem.  

- Per nascondere i driver privi di una firma digitale valida, selezionare **Nascondi driver senza firma digitale**.  

> [!NOTE]  
> Importare i driver di dispositivo nel catalogo dei driver prima di aggiungerli a un'immagine d'avvio. Per informazioni su come importare i driver di dispositivo, vedere [Gestire i driver](manage-drivers.md).  

#### <a name="customization"></a>Personalizzazione

Nella scheda **Personalizzazione** selezionare una delle seguenti impostazioni:  

- Selezionare l'opzione **Attiva comando di preavvio** per specificare un comando da eseguire prima della sequenza di attività. Quando si abilita questa opzione, specificare anche la riga di comando da eseguire e i file di supporto richiesti dal comando.  

    > [!WARNING]  
    > Aggiungere `cmd /c` all'inizio della riga di comando. Se non si specifica `cmd /c`, il comando non verrà chiuso al termine dell'esecuzione. La distribuzione continuerà ad attendere la fine del comando e non avvierà altri comandi o azioni configurati.  

    > [!TIP]  
    > Durante la creazione del supporto per la sequenza di attività, la procedura guidata scrive l'ID del pacchetto e la riga di comando di preavvio nel file **CreateTSMedia.log**. Queste informazioni includono il valore di tutte le variabili della sequenza di attività. Questo log si trova nel computer in cui viene eseguita la console di Configuration Manager. Esaminare questo file di log per verificare il valore per le variabili della sequenza di attività.  

- Configurare l'impostazione **Sfondo Windows PE** per specificare se si vuole usare lo sfondo Windows PE predefinito o uno sfondo personalizzato.  

- Configurare l'**area scratch di Windows PE (MB)** , ovvero l'archivio temporaneo (unità RAM) usato da WinPE. Ad esempio, quando un'applicazione viene eseguita in WinPE e richiede la scrittura di file temporanei, WinPE reindirizza tali file all'area scratch in memoria per simulare la presenza di un disco rigido. Per impostazione predefinita, questa quantità è 512 MB per i dispositivi con più di 1 GB di RAM. In caso contrario, il valore predefinito è 32 MB.  

- Selezionare **Abilita supporto comandi (solo test)** per aprire un prompt dei comandi usando il tasto **F8** mentre l'immagine d'avvio viene distribuita. Questa opzione è utile per la risoluzione dei problemi durante la verifica della distribuzione. A causa di problemi di sicurezza non è consigliabile usare questa impostazione in una distribuzione di produzione.  

- **Imposta il layout di tastiera predefinito in WinPE**: <!--4910348-->A partire dalla versione 1910, configurare il layout predefinito della tastiera per un'immagine d'avvio. Se si seleziona una lingua diversa da en-US, Configuration Manager include ancora en-US nelle impostazioni locali di input disponibili. Nel dispositivo, il layout iniziale della tastiera corrisponde alle impostazioni locali selezionate, ma l'utente può passare a en-US se necessario.

    > [!Tip]
    > Il cmdlet di PowerShell [Set-CMBootImage](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmbootimage?view=sccm-ps) include ora il nuovo parametro `-InputLocale`. Ad esempio:
    >
    > ```PowerShell
    > # Set boot image keyboard layout to Russian (Russia)
    > Set-CMBootimage -Id "CM100004" -InputLocale "ru-ru"`
    > ```

#### <a name="optional-components"></a>Componenti facoltativi

Nella scheda **Componenti facoltativi** specificare i componenti aggiunti a Windows PE per l'utilizzo con Configuration Manager. Per altre informazioni sui componenti facoltativi, vedere [WinPE: aggiungere pacchetti (informazioni di riferimento sui componenti facoltativi)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/winpe-add-packages--optional-components-reference).  

I componenti seguenti sono richiesti da Configuration Manager e vengono sempre aggiunti alle immagini d'avvio:

- Scripting (WinPE-Scripting)
- Startup (WinPE-SecureStartup)
- Network (WinPE-WDS-Tools)
- Scripting (WinPE-WMI)

L'elenco **Componenti** mostra gli elementi aggiuntivi che vengono aggiunti a questa immagine d'avvio. Per aggiungere altri componenti, selezionare l'asterisco color oro. Per rimuovere un componente, selezionarlo nell'elenco e quindi selezionare la X rossa.

I componenti seguenti vengono usati comunemente dai clienti:

- Microsoft .NET (WinPE-NetFX): questo componente è un prerequisito per PowerShell. È uno dei componenti facoltativi più grandi.  
- Windows PowerShell (WinPE-PowerShell): questo componente richiede .NET e aggiunge supporto limitato di PowerShell. Se si eseguono gli script di PowerShell personalizzati durante la fase WinPE della sequenza di attività, aggiungere questo componente. Esistono altri componenti che potrebbero essere necessari per altri cmdlet di PowerShell.
- HTML (WinPE-HTA): se si eseguono applicazioni HTML personalizzate durante la fase WinPE della sequenza di attività, aggiungere questo componente.

Per altre informazioni sull'aggiunta di ulteriori lingue, vedere [Configurare più lingue](#BKMK_BootImageLanguage).

#### <a name="data-source"></a>origine dati

Nella scheda **Origine dati** aggiornare le seguenti impostazioni:  

- Per modificare il file di origine dell'immagine d'avvio, impostare **Percorso immagine** e **Indice immagine**.  

- Per creare una pianificazione di aggiornamento dell'immagine d'avvio da parte del sito, selezionare **Aggiorna i punti di distribuzione in base alla pianificazione**.  

- Se non si vuole che il contenuto del pacchetto venga eliminato dalla cache del client per liberare spazio per altro contenuto, selezionare **Mantieni contenuto nella cache del client**.  

- Per specificare che il sito distribuisce solo i file modificati quando aggiorna il pacchetto dell'immagine d'avvio nel punto di distribuzione, selezionare **Abilita la replica differenziale binaria** (BDR). Questa impostazione riduce al minimo il traffico di rete tra siti. La replica differenziale binaria è particolarmente utile quando il pacchetto dell'immagine d'avvio è di grandi dimensioni e le modifiche sono piuttosto limitate.  

- Se l'immagine d'avvio viene usata in una distribuzione che supporta PXE, selezionare **Distribuire questa immagine d'avvio dal punto di distribuzione che supporta PXE**. Per altre informazioni, vedere [Usare PXE per distribuire Windows in rete](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

#### <a name="data-access"></a>Accesso dati

Nella scheda **Accesso dati** è possibile configurare le impostazioni di condivisione dei pacchetti. Se necessario nell'ambiente in uso, impostare l'opzione **Copia il contenuto del pacchetto in una condivisione pacchetto nei punti di distribuzione**. Sarà quindi disponibile l'opzione aggiuntiva **Usa un nome personalizzato per la condivisione pacchetto** e sarà possibile specificare il **Nome della condivisione** personalizzato. Se si abilita questa opzione, è necessario spazio aggiuntivo su disco nei punti di distribuzione. Si applica a tutti i punti di distribuzione che ricevono questa immagine d'avvio.

#### <a name="distribution-settings"></a>Impostazioni distribuzione

Nella scheda **Impostazioni distribuzione** selezionare una delle seguenti impostazioni:  

- Nell'elenco **Priorità di distribuzione** specificare il livello di priorità. Configuration Manager usa questo elenco delle priorità quando il sito distribuisce più pacchetti allo stesso punto di distribuzione.  

- Per abilitare la distribuzione del contenuto su richiesta nei punti di distribuzione preferiti, selezionare **Abilita per la distribuzione su richiesta**. Quando si abilita questa impostazione, se un client richiede il contenuto per il pacchetto e il contenuto non è disponibile in nessuno dei punti di distribuzione, il punto di gestione distribuisce il contenuto. Per altre informazioni, vedere [Distribuzione di contenuto su richiesta](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#on-demand-content-distribution).  

- Per specificare come il sito distribuirà l'immagine d'avvio ai punti di distribuzione abilitati per i contenuti in versione di preproduzione, selezionare **Impostazioni punto di distribuzione pre-installazione**. Per altre informazioni sui contenuti in versione di preproduzione, vedere [Prestage content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).  

#### <a name="content-locations"></a>Percorsi contenuto

Nella scheda **Percorsi contenuto** selezionare il punto di distribuzione o il gruppo di punti di distribuzione e usare le azioni seguenti:  

- **Convalida**: controllare l'integrità del pacchetto di immagini d'avvio nel punto di distribuzione o nel gruppo di punti di distribuzione selezionato.  

- **Ridistribuisci**: distribuire nuovamente l'immagine d'avvio nel punto di distribuzione o nel gruppo di punti di distribuzione selezionato.  

- **Rimuovi**: eliminare l'immagine d'avvio dal punto di distribuzione o dal gruppo di punti di distribuzione selezionato.  

#### <a name="security"></a>Sicurezza

Nella scheda **Sicurezza** è possibile visualizzare gli utenti amministratori che hanno le autorizzazioni per questo oggetto.

## <a name="configure-a-boot-image-for-pxe"></a><a name="BKMK_BootImagePXE"></a> Configurare un'immagine d'avvio per PXE  

Prima di poter usare un'immagine d'avvio per una distribuzione basata su PXE, è necessario configurare l'immagine d'avvio per la distribuzione da un punto di distribuzione abilitato per PXE.  

1. Nella console di Configuration Manager passare all'area di lavoro **Raccolta software**, espandere **Sistemi operativi** e quindi selezionare il nodo **Immagini d'avvio**.  

2. Selezionare l'immagine di avvio da modificare.  

3. Nella scheda **Home** della barra multifunzione selezionare **Proprietà** nel gruppo **Proprietà**.  

4. Nella scheda **Origine dati** selezionare **Distribuire questa immagine d'avvio dal punto di distribuzione che supporta PXE**. Per altre informazioni, vedere [Usare PXE per distribuire Windows in rete](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

## <a name="configure-multiple-languages"></a><a name="BKMK_BootImageLanguage"></a> Configurare più lingue

> [!TIP]
> A partire dalla versione 1910, configurare il layout di tastiera predefinito per le proprietà di un'immagine di avvio. Per altre informazioni, vedere [Personalizzazione](#customization).<!--4910348-->

Le immagini di avvio sono indipendenti dalla lingua. Questa funzionalità consente di usare un'immagine d'avvio per visualizzare il testo della sequenza di attività in più lingue all'interno di WinPE. Includere il supporto della lingua appropriato dalla scheda **Componenti facoltativi** dell'immagine d'avvio. Impostare quindi la variabile della sequenza di attività appropriata per indicare la lingua da visualizzare. La lingua del sistema operativo distribuito è indipendente dalla lingua usata in WinPE. La lingua che WinPE visualizza all'utente viene determinata nel modo seguente:  

- Quando un utente esegue la sequenza di attività da un sistema operativo esistente, Configuration Manager usa automaticamente la lingua configurata per l'utente. Quando la sequenza di attività viene eseguita automaticamente a causa della scadenza di una distribuzione obbligatoria, Configuration Manager usa la lingua del sistema operativo.  

- Per le distribuzioni di sistemi operativi avviate da PXE o da supporti, impostare il valore di ID lingua nella variabile **SMSTSLanguageFolder** all'interno di un comando di preavvio. Quando il computer si avvia in Windows PE, i messaggi vengono visualizzati nella lingua specificata nella variabile. Se si verifica un errore durante l'accesso al file di risorse della lingua nella cartella specificata o se la variabile non viene impostata, WinPE visualizza i messaggi nella lingua predefinita.  

    > [!NOTE]  
    > Quando il supporto è protetto da una password, il testo di richiesta di immissione della password viene sempre visualizzato nella lingua di WinPE.  

Usare la procedura seguente per impostare la lingua di WinPE per distribuzioni del sistema operativo avviate da PXE o da supporto.  

### <a name="set-the-windows-pe-language-for-a-pxe-or-media-initiated-os-deployment"></a>Impostare la lingua di Windows PE per una distribuzione del sistema operativo avviata da PXE o da supporto  

1. Prima di aggiornare l'immagine d'avvio, verificare che il file di risorse della sequenza di attività appropriato (tsres.dll) sia incluso nella cartella della lingua corrispondente nel server del sito. Ad esempio, il file di risorse inglese è nel percorso seguente: `<ConfigMgrInstallationFolder>\OSD\bin\x64\00000409\tsres.dll`  

2. Come parte del comando di preavvio, impostare la variabile di ambiente **SMSTSLanguageFolder** sull'ID lingua appropriato. L'ID lingua deve essere specificato usando il formato decimale e non esadecimale. Ad esempio, per impostare l'ID lingua su Inglese, specificare il valore decimale **1033** e non il valore esadecimale 00000409 del nome della cartella.  
