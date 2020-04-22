---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: include
ms.date: 05/28/2019
ms.openlocfilehash: e5c15556a7a8dd91db3ae2c4aa4f9830abc8e430
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708879"
---
## <a name="apply-software-updates-to-an-image"></a><a name="BKMK_OSImagesApplyUpdates"></a> Applicare aggiornamenti software a un'immagine

> [!Note]  
> Questa sezione si applica sia alle **immagini del sistema operativo** sia ai **pacchetti di aggiornamento del sistema operativo**. Il termine generale "immagine" viene usato per fare riferimento al file di immagine Windows (WIM). Entrambi questi oggetti prevedono un file WIM, che contiene i file di installazione di Windows. Gli aggiornamenti software sono applicabili a questi file in entrambi gli oggetti. Il comportamento di questo processo è uguale in entrambi gli oggetti.  

Ogni mese sono disponibili nuovi aggiornamenti software applicabili all'immagine. Prima di poter applicare gli aggiornamenti software all'immagine, sono necessari i prerequisiti seguenti:

- Infrastruttura di aggiornamento del software  
- Aggiornamenti software sincronizzati correttamente  
- Aggiornamenti software scaricati nella raccolta contenuto nel server del sito  

Per altre informazioni, vedere [Distribuire gli aggiornamenti software](../../../sum/deploy-use/deploy-software-updates.md).  

Applicare gli aggiornamenti software applicabili a un'immagine in base a una pianificazione specificata. Questo processo viene talvolta chiamato *installazione offline*. In questa pianificazione, Configuration Manager applica gli aggiornamenti software selezionati all'immagine. È quindi possibile ridistribuire anche l'immagine aggiornata ai punti di distribuzione.

> [!Important]  
> Nonostante sia possibile selezionare qualsiasi aggiornamento software applicabile all'immagine in base alla versione, DISM può applicare solo determinati tipi di aggiornamenti all'immagine. Il file **OfflineServicingMgr.log** mostra la voce seguente: `Not applying this update binary, it is not supported`.<!-- SCCMDocs issue 1324 -->

Le informazioni sull'immagine, inclusi gli aggiornamenti software applicati al momento dell'importazione, vengono archiviate nel database del sito. Anche gli aggiornamenti software applicati all'immagine dopo che è stata inizialmente aggiunta vengono archiviati nel database del sito. Quando si avvia la procedura guidata per applicare gli aggiornamenti software, viene recuperato l'elenco degli aggiornamenti software applicabili che il sito non ha ancora applicato all'immagine. Configuration Manager copia gli aggiornamenti software selezionati dalla raccolta contenuto nel server del sito. Gli aggiornamenti software vengono quindi applicati all'immagine.  

### <a name="servicing-process"></a>Processo di manutenzione

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**, espandere **Sistemi operativi** e selezionare **Immagini del sistema operativo** o **Pacchetti di aggiornamento del sistema operativo**.  

2. Selezionare l'oggetto a cui applicare gli aggiornamenti software.  

3. Selezionare **Pianifica aggiornamenti** sulla barra multifunzione per avviare la procedura guidata.  

4. Nella pagina **Scegli aggiornamenti** selezionare gli aggiornamenti software da applicare all'immagine. Potrebbe essere necessario qualche minuto prima che l'elenco degli aggiornamenti venga visualizzato nella procedura guidata. Usare il **Filtro** per cercare stringhe nei metadati. Usare l'elenco a discesa **Architettura di sistema** per applicare il filtro in base a **X86**, **X64** o **Tutti**. È possibile selezionare uno, molti o tutti gli aggiornamenti nell'elenco. Dopo aver completato la selezione degli aggiornamenti, selezionare **Avanti**.  

5. Nella pagina **Imposta pianificazione** specificare le seguenti impostazioni e quindi fare clic su **Avanti**.  

    1. **Pianificazione**: specificare il momento in cui si vuole che il sito applichi gli aggiornamenti software all'immagine.  

    2. **Continua in caso di errore**: selezionare questa opzione per continuare ad applicare gli aggiornamenti software all'immagine anche quando si verifica un errore.  

    3. **Aggiorna punti di distribuzione con l'immagine**: selezionare questa opzione per aggiornare l'immagine nei punti di distribuzione dopo che il sito ha applicato gli aggiornamenti software.  

6. Completare la procedura guidata pianificazione aggiornamenti.  

> [!NOTE]  
> Per ridurre al minimo le dimensioni del payload, il processo di manutenzione dei pacchetti di aggiornamento del sistema operativo e delle immagini del sistema operativo rimuove la versione precedente.  

### <a name="servicing-operations"></a>Operazioni di manutenzione

Nel nodo **Immagini sistema operativo** o **Pacchetti di aggiornamento del sistema operativo** della console di Configuration Manager aggiungere le colonne seguenti alla visualizzazione:

- **Data aggiornamenti pianificati**: questa proprietà indica la pianificazione successiva definita.  
- **Stato aggiornamenti pianificati**: questa proprietà indica lo stato. Ad esempio, **Completato** oppure **In elaborazione**.  

Selezionare un oggetto immagine specifico e quindi passare alla scheda **Stato aggiornamento** nel riquadro dei dettagli. In questa scheda viene visualizzato l'elenco degli aggiornamenti nell'immagine.

Selezionare un pacchetto immagine specifico e selezionare **Proprietà** nella barra multifunzione. La scheda **Aggiornamenti installati** indica l'elenco degli aggiornamenti nell'immagine. La scheda **Manutenzione** offre una vista di sola lettura della pianificazione di manutenzione corrente e gli aggiornamenti pianificati da applicare.

Quando lo stato è **In elaborazione**, è possibile selezionare **Annulla aggiornamenti pianificati** sulla barra multifunzione. L'azione annulla il processo di manutenzione attivo.

Per risolvere i problemi di questo processo, visualizzare i file **OfflineServicingMgr.log** e **dism.log** nel server del sito. Per altre informazioni, vedere [File di log](../../../core/plan-design/hierarchy/log-files.md).

### <a name="specify-the-drive-for-offline-os-image-servicing"></a><a name="bkmk_servicing-drive"></a> Specificare l'unità per la manutenzione di immagini del sistema operativo offline

<!--1358924-->

A partire dalla versione 1810, specificare l'unità usata da Configuration Manager durante la manutenzione offline delle immagini del sistema operativo. Questo processo può occupare una grande quantità di spazio su disco con i file temporanei. Questa opzione la flessibilità di poter selezionare l'unità da usare.

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito** e selezionare **Siti**. Sulla barra multifunzione fare clic su **Configura componenti del sito** e selezionare **Distribuzione del sistema operativo**.  

2. Nella scheda **Installazione offline** specificare l'opzione per **Unità locale che deve essere usata dall'installazione offline delle immagini:** .  

L'impostazione predefinita di questa opzione è **Automatic** (Automatica). Con questo valore, Configuration Manager seleziona l'unità in cui è installato.

Se si seleziona un'unità che non esiste nel server del sito, Configuration Manager si comporta come se fosse selezionata l'opzione **Automatica**.

Durante l'installazione offline, Configuration Manager archivia i file temporanei nella cartella `<drive>:\ConfigMgr_OfflineImageServicing` e monta anche l'immagine del sistema operativo in questa cartella.

### <a name="optimized-image-servicing"></a><a name="bkmk_resetbase"></a> Servizio immagini ottimizzato

<!--3555951-->

A partire dalla versione 1902, quando si applicano aggiornamenti software a un'immagine del sistema operativo, è disponibile una nuova opzione che ottimizza l'output rimuovendo tutti gli aggiornamenti sostituiti. L'ottimizzazione per l'installazione offline si applica solo alle immagini con un indice singolo.

Quando si pianifica il sito per applicare aggiornamenti software a un'immagine del sistema operativo, viene usato lo strumento della riga di comando Gestione e manutenzione immagini distribuzione (DISM) di Windows. Durante il processo di manutenzione questa modifica introduce i due passaggi aggiuntivi seguenti:  

- Esegue DISM sull'immagine offline montata con i parametri `/Cleanup-Image /StartComponentCleanup /ResetBase`. Se questo comando non riesce, il processo di manutenzione corrente ha esito negativo. Non esegue il commit di nessuna modifica all'immagine.  

- Dopo il commit delle modifiche all'immagine e lo smontaggio dell'immagine dal file system, Configuration Manager esporta l'immagine in un altro file. Questo passaggio usa il parametro DISM `/Export-Image`. Rimuove i file non necessari dall'immagine e di conseguenza ne riduce le dimensioni.  

Microsoft consiglia di applicare periodicamente aggiornamenti alle immagini offline. Non è necessario usare questa opzione ogni volta che si esegue la manutenzione di un'immagine. Quando si esegue questo processo ogni mese, questa nuova opzione offre il massimo vantaggio. Per altre informazioni, vedere [Consigli per il passaggio Installa aggiornamenti software](../../understand/install-software-updates.md#recommendations).

Anche se l'opzione consente di ridurre le dimensioni complessive dell'immagine sottoposta a manutenzione, il completamento del processo richiede più tempo. Usare la procedura guidata per pianificare la manutenzione in orari appropriati. L'operazione richiede anche spazio di archiviazione aggiuntivo nel server del sito. È possibile personalizzare il sito per l'uso di un percorso alternativo. Per altre informazioni, vedere [Specificare l'unità per l'installazione offline dell'immagine del sistema operativo](#bkmk_servicing-drive).

#### <a name="process-to-optimize-image-servicing"></a>Processo per ottimizzare la manutenzione delle immagini

1. Avviare il [processo di manutenzione](#servicing-process).  

2. Nella pagina **Imposta pianificazione** selezionare l'opzione **Remove superseded updates after the image is updated** (Rimuovi aggiornamenti obsoleti dopo l'aggiornamento dell'immagine). Questa opzione non è abilitata automaticamente. Se l'immagine include più di un indice non è possibile usare questa opzione.  

3. Per pianificare la manutenzione dell'immagine, completare la procedura guidata.  

Convalidare e monitorare il processo mediante **OfflineServicing.log**.
