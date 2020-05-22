---
title: Nuova versione 1702
titleSuffix: Configuration Manager
description: Informazioni dettagliate sulle modifiche e sulle nuove funzionalità introdotte nella versione 1702 di Configuration Manager.
ms.date: 05/02/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 409e26e1-7716-4f1d-a0ee-34feabf20792
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: eacf64245f4cfc779dc92be73e8d7e387b34f909
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83427932"
---
# <a name="what39s-new-in-version-1702-of-configuration-manager"></a>Novità della versione 1702 di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

L'aggiornamento 1702 per Configuration Manager Current Branch è disponibile come aggiornamento nella console per siti precedentemente installati che eseguono la versione 1602, 1606 o 1610. È disponibile anche come versione di base da usare durante l'installazione di una nuova distribuzione.

> [!TIP]  
> Per installare un nuovo sito, è necessario usare una versione base di Configuration Manager.  
>
> Sono disponibili altre informazioni su:    
> - [Installing new sites](../../servers/deploy/install/installing-sites.md) (Installare nuovi siti)  
> - [Installing updates at sites](../../servers/manage/updates.md) (Installare aggiornamenti nei siti)  
> - [Baseline and update versions](../../servers/manage/updates.md#bkmk_Baselines) (Versioni di base e di aggiornamento)

Le sezioni seguenti illustrano in dettaglio le modifiche e le nuove funzionalità introdotte nella versione 1702 di Configuration Manager.  

## <a name="deprecated-features-and-operating-systems"></a>Funzionalità e sistemi operativi deprecati
Informazioni sulle modifiche apportate al supporto prima dell'implementazione in [Elementi rimossi e deprecati](deprecated/removed-and-deprecated.md).

Nella versione 1702 viene eliminato il supporto per i prodotti seguenti:
- **SQL Server 2008 R2**, per i server di database del sito. Il [primo avviso](deprecated/removed-and-deprecated-server.md#sql-server) relativo al supporto deprecato risale al 10 luglio 2015. Questa versione di SQL Server rimane supportata quando si usa una versione di Configuration Manager precedente la 1702.
- **Windows Server 2008 R2**, per i server del sistema del sito e per la maggior parte dei ruoli del sistema del sito. Il [primo avviso](deprecated/removed-and-deprecated-server.md#server-os) relativo al supporto deprecato risale al 10 luglio 2015. Questa versione di Windows rimane supportata quando si usa una versione di Configuration Manager precedente la 1702.  
- **Windows Server 2008**, per i server del sistema del sito e per la maggior parte dei ruoli del sistema del sito. Il [primo avviso](deprecated/removed-and-deprecated-server.md#server-os) relativo al supporto deprecato risale al 10 luglio 2015.
- **Windows XP Embedded**, come sistema operativo client. Il [primo avviso](deprecated/removed-and-deprecated-client.md#deprecated-client-operating-systems) relativo alla deprecazione risale al 10 luglio 2015. Questa versione di Windows rimane supportata quando si usa una versione di Configuration Manager precedente la 1702.




## <a name="site-infrastructure"></a>Infrastruttura del sito

### <a name="improvements-for-in-console-search"></a>Miglioramenti per la ricerca nella console
Di seguito sono riportati i miglioramenti apportati all'uso della funzionalità di ricerca nella console di Configuration Manager:
- **Percorso oggetto:**  
  Molti oggetti ora supportano una colonna denominata **Percorso oggetto**.  Se si include questa colonna nella visualizzazione dei risultati, è possibile vedere il percorso di ogni oggetto. Se, ad esempio, si esegue la ricerca delle app nel nodo Applicazioni e la ricerca viene eseguita anche nei sottonodi, nella colonna *Percorso oggetto* del riquadro dei risultati verrà visualizzato il percorso di ogni oggetto restituito.   

- **Conservazione del testo della ricerca:**  
  Quando si immette testo nella casella di testo di ricerca e quindi si passa dalla ricerca in un sottonodo alla ricerca nel nodo corrente e viceversa, il testo digitato diventa permanente e rimane disponibile per una nuova ricerca senza che sia necessario immetterlo di nuovo.

- **Mantenimento della decisione relativa alla ricerca nei sottonodi:**  
  L'opzione selezionata per l'esecuzione della ricerca nel *nodo corrente* o in *tutti i sottonodi* ora viene mantenuta quando si modifica il nodo usato. Con il nuovo comportamento non è necessario reimpostare costantemente questa opzione ogni volta che ci si sposta all'interno della console. Per impostazione predefinita, quando si apre la console è impostata l'opzione per l'esecuzione di ricerche solo nel nodo corrente.


### <a name="send-feedback-from-the-configuration-manager-console"></a>Inviare commenti e suggerimenti dalla console di Configuration Manager

È possibile usare le opzioni di feedback dalla console per inviare commenti e suggerimenti direttamente al team di sviluppo.

È possibile trovare l'opzione **Commenti e suggerimenti**:
- Nella barra multifunzione, all'estrema sinistra della scheda Home di ogni nodo.  
  ![Barra multifunzione](./media/feedback-home.png)

- Facendo clic con il pulsante destro del mouse su qualsiasi oggetto nella console.   
   ![Opzione con clic con il pulsante destro del mouse](./media/feedback-option.png)   

  Quando si seleziona **Commenti e suggerimenti**, il browser visualizza il [sito Web UserVoice di Configuration Manager](https://configurationmanager.uservoice.com/forums/300492-ideas).


###  <a name="changes-for-updates-and-servicing"></a>Modifiche per Aggiornamenti e manutenzione
Di seguito sono riportate le modifiche relative ad Aggiornamenti e manutenzione:

- **Posizione del nodo**   
  Dopo l'installazione della versione 1702, il nodo **Aggiornamenti e manutenzione** viene visualizzato come nodo di livello superiore sotto **Amministrazione**. Non è più un nodo figlio di **Servizi cloud**.

- **Nuovi stati di aggiornamento**  
  Quando si visualizzano gli aggiornamenti disponibili nella console, sono presenti due nuovi stati:  
  - **Available for install** (Disponibile per l'installazione): l'aggiornamento è stato scaricato ed è pronto per l'installazione.
  - **Ready for download** (Pronto per il download): l'aggiornamento è disponibile, ma non è ancora stato scaricato. È possibile scegliere di eseguire il download, ma l'aggiornamento è stato sostituito da uno più recente.


- **Opzioni di aggiornamento più semplici**  
  Quando l'infrastruttura necessita di due o più aggiornamenti, viene scaricato solo l'aggiornamento più recente. Ad esempio, se la versione corrente del sito è più vecchia di due o più versioni rispetto alla versione più recente disponibile, viene scaricata automaticamente solo la versione più recente dell'aggiornamento.  

  È possibile scaricare e installare gli altri aggiornamenti disponibili, anche quando non sono la versione più recente. Se si scarica un aggiornamento precedente, verrà visualizzato un avviso in cui si notifica che l'aggiornamento è stato sostituito da una versione più recente. Per scaricare un aggiornamento *Disponibile per il download*, selezionare l'aggiornamento nella console e quindi fare clic su **Scarica**.

- **Miglioramento della pulizia degli aggiornamenti precedenti**   
  È stata aggiunta una funzione di pulizia automatica che elimina i download non necessari dalla cartella 'EasySetupPayload' nel server del sito. Poiché è stata introdotta con la versione 1702, la funzione di pulizia inizia a funzionare dopo l'installazione di un aggiornamento successivo, ad esempio un aggiornamento cumulativo, o una futura versione dell'aggiornamento.  


### <a name="data-warehouse-service-point"></a>Punto di servizio del data warehouse
Usare il punto di servizio del data warehouse per archiviare e creare report di dati cronologici a lungo termine per la distribuzione di Configuration Manager.

Il data warehouse supporta fino a 2 TB di dati, con timestamp per il rilevamento delle modifiche. L'archiviazione dei dati viene eseguita tramite sincronizzazioni automatizzate dal database del sito di Configuration Manager al database del data warehouse. Queste informazioni diventano quindi accessibili dal punto di Reporting Services.

Per altre informazioni, vedere [Punto di servizio del data warehouse](../../servers/manage/data-warehouse.md).


### <a name="peer-cache-improvements"></a>Miglioramenti della peer cache
A partire dalla versione 1702, il computer di origine della peer cache rifiuta le richieste di contenuti quando soddisfa una delle condizioni seguenti:  
-  È in modalità di batteria in esaurimento.
-  Il carico della CPU supera l'80% nel momento in cui il contenuto viene richiesto.
-  L'I/O disco ha un valore di *AvgDiskQueueLength* superiore a 10.
-  Non vi sono più connessioni disponibili al computer.   
Per altre informazioni, vedere la sezione **Accesso limitato a un'origine di peer cache** dell'argomento [Peer cache per i client di Configuration Manager](../hierarchy/client-peer-cache.md).   

Al punto di reporting, inoltre, sono stati aggiunti tre nuovi report. È possibile usare questi report per ottenere maggiori dettagli sulle richieste di contenuto rifiutate, inclusi il gruppo di limiti, il computer e il contenuto interessati. Vedere la sezione [Monitoring](../hierarchy/client-peer-cache.md#monitoring) (Monitoraggio) dell'argomento relativo alla peer cache.

### <a name="content-library-cleanup-tool"></a>Strumento di pulizia della raccolta contenuto
Usare lo [strumento per la pulizia della raccolta contenuto](../hierarchy/content-library-cleanup-tool.md) per rimuovere il contenuto dai punti di distribuzione quando tale contenuto non è più associato a un'applicazione.


### <a name="use-the-oms-connector-with-the-azure-government-cloud"></a>Usare OMS Connector con il cloud di Azure per enti pubblici
È possibile usare OMS Connector per connettersi a Log Analytics di OMS nel cloud di Microsoft Azure per enti pubblici. A questo scopo, è necessario modificare un file di configurazione prima di installare OMS Connector, in modo che quest'ultimo possa funzionare con il cloud di Azure per enti pubblici. Per altre informazioni, vedere [Usare OMS Connector con il cloud di Azure per enti pubblici](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm).

### <a name="software-update-points-are-added-to-boundary-groups"></a>Aggiunta di punti di aggiornamento software ai gruppi di limiti
A partire dalla versione 1702, i client usano i gruppi di limiti per trovare un nuovo punto di aggiornamento software se quello corrente non è più disponibile. È possibile aggiungere singoli punti di aggiornamento software a diversi gruppi di limiti per controllare quali server possono essere trovati da un client. Per altre informazioni, vedere la sezione [Punti di aggiornamento software](../../servers/deploy/configure/boundary-groups.md#software-update-points) dell'argomento [Configurare gruppi di limiti](../../servers/deploy/configure/boundary-groups.md).


<!-- ## Migration  -->

<!-- ## Client management  -->

## <a name="compliance-settings"></a>Impostazioni di conformità

### <a name="new-compliance-settings-for-ios"></a>Nuove impostazioni di conformità per iOS

Sono state aggiunte diverse nuove impostazioni per dispositivi iOS, corrispondenti a quelle disponibili con Microsoft Intune.


## <a name="application-management"></a>Gestione delle applicazioni

### <a name="improved-support-for-windows-store-for-business-apps"></a>Miglioramento del supporto per le app di Windows Store per le aziende

È ora possibile distribuire app con licenza online da Windows Store per le aziende a PC Windows 10 gestiti mediante il client di Configuration Manager.
Per altre informazioni, vedere [Gestire le app da Windows Store per le aziende](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).

### <a name="check-for-running-executable-files-before-installing-an-application"></a>Controllare l'esecuzione di file eseguibili prima di installare un'applicazione

Nella finestra di dialogo **Proprietà** di un tipo di distribuzione, nella scheda **Comportamento installazione**, è ora possibile specificare uno o più file eseguibili che, se in esecuzione, bloccano l'installazione del tipo di distribuzione. L'utente deve chiudere il file eseguibile in esecuzione, che in alternativa può essere chiuso automaticamente per le distribuzioni con scopo richiesto, prima dell'installazione del tipo di distribuzione.

Se l'applicazione è stata distribuita come **Disponibile** e un utente finale tenta di installare un'applicazione, verrà richiesto di chiudere tutti i file eseguibili in esecuzione specificati, prima di poter procedere con l'installazione.

Se l'applicazione è stata distribuita come **Richiesta** e l'opzione **Chiudi automaticamente eventuali file eseguibili in esecuzione specificati nella scheda Comportamento di installazione della finestra di dialogo relativa alle proprietà del tipo di distribuzione** è selezionata, verrà visualizzata una finestra di dialogo che informa che i file eseguibili specificati verranno chiusi automaticamente quando viene raggiunta la scadenza dell'installazione dell'applicazione.

### <a name="app-management-improvements-for-hybrid-mdm"></a>Miglioramenti alla gestione delle app per MDM ibrido

- [Distribuire app iOS acquistate con Volume Purchase Program a raccolte di dispositivi](#deploy-volume-purchased-ios-apps-to-device-collections)
- [Supporto per iOS Volume Purchase Program for Education](#support-for-ios-volume-purchase-program-for-education)
- [Supporto per più token di Volume Purchase Program](#support-for-multiple-volume-purchase-program-tokens)


## <a name="operating-system-deployment"></a>Distribuzione del sistema operativo

### <a name="expire-stand-alone-media"></a>Scadenza dei supporti autonomi
Quando si creano supporti autonomi, sono disponibili nuove opzioni per l'impostazione di date facoltative di inizio e scadenza nei supporti. Queste impostazioni sono disabilitate per impostazione predefinita. Le date vengono confrontate con l'ora di sistema nel computer prima che il supporto autonomo venga eseguito. Quando l'ora di sistema è precedente all'ora di inizio o successiva all'ora di scadenza, il supporto autonomo non viene avviato. Queste opzioni sono disponibili anche tramite il cmdlet PowerShell New-CMStandaloneMedia. Per informazioni dettagliate, vedere [Creare supporti autonomi](../../../osd/deploy-use/create-stand-alone-media.md).

### <a name="package-id-displayed-in-task-sequence-steps"></a>ID pacchetto visualizzato nei passaggi della sequenza di attività
I passaggi della sequenza di attività che fanno riferimento a un pacchetto, un pacchetto driver, un'immagine del sistema operativo, un'immagine d'avvio o un pacchetto di aggiornamento del sistema operativo visualizzano ora l'ID pacchetto dell'oggetto a cui viene fatto riferimento. Quando un passaggio della sequenza di attività fa riferimento a un'applicazione, viene visualizzato l'ID oggetto.

### <a name="support-for-additional-content-in-stand-alone-media"></a>Supporto per contenuto aggiuntivo nei supporti autonomi
È ora supportato contenuto aggiuntivo nei supporti autonomi. È possibile selezionare altri pacchetti, pacchetti driver e applicazioni da gestire nei supporti insieme ad altro contenuto cui viene fatto riferimento nella sequenza di attività. In precedenza, soltanto il contenuto cui veniva fatto riferimento nella sequenza di attività veniva gestito nei supporti autonomi. Per informazioni dettagliate, vedere [Creare supporti autonomi](../../../osd/deploy-use/create-stand-alone-media.md).

### <a name="hardware-inventory-collects-uefi-information"></a>L'inventario hardware raccoglie le informazioni UEFI
Una nuova classe di inventario hardware (**SMS_Firmware**) e una nuova proprietà (**UEFI**) sono disponibili per determinare se un computer viene avviato in modalità UEFI. Quando un computer viene avviato in modalità UEFI, la proprietà **UEFI** è impostata su **TRUE**. L'impostazione è abilitata nell'inventario hardware per impostazione predefinita. Per altre informazioni sull'inventario hardware, vedere [How to configure hardware inventory](../../clients/manage/inventory/configure-hardware-inventory.md) (Come configurare l'inventario hardware).

### <a name="improvements-to-software-center-warning-messages-for-high-impact-task-sequences"></a>Miglioramenti ai messaggi di avviso di Software Center per le sequenze di attività a impatto elevato
Questa versione include i miglioramenti seguenti ai messaggi di avviso di Software Center per le sequenze di attività di distribuzione a impatto elevato:

- Nelle proprietà per la sequenza di attività è ora possibile configurare qualsiasi sequenza di attività, comprese le sequenze di attività non del sistema operativo, come distribuzioni ad alto rischio. Qualsiasi sequenza di attività che soddisfi determinate condizioni viene definita automaticamente come a impatto elevato. Per altri dettagli, vedere [Gestire le distribuzioni ad alto rischio](../../servers/manage/settings-to-manage-high-risk-deployments.md).
- Nelle proprietà per la sequenza di attività è possibile scegliere di usare il messaggio di notifica predefinito o crearne uno personalizzato per le distribuzioni a impatto elevato.
- Nelle proprietà per la sequenza di attività è possibile configurare le proprietà di Software Center, tra cui l'obbligatorietà del riavvio, le dimensioni del download della sequenza di attività e il tempo di esecuzione stimato.
- Il messaggio predefinito di distribuzione a impatto elevato per gli aggiornamenti sul posto indica ora che la migrazione di applicazioni, dati e impostazioni è stata eseguita automaticamente. In precedenza il messaggio predefinito per qualsiasi installazione del sistema operativo indicava che tutte le applicazioni, i dati e le impostazioni sarebbero andati persi, il che non era vero per gli aggiornamenti sul posto.

Per informazioni dettagliate, vedere [Configure high-impact task sequence settings](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#set-a-task-sequence-as-a-high-impact-task-sequence) (Configurare impostazioni della sequenza di attività ad alto impatto).

### <a name="return-to-previous-page-when-a-task-sequence-fails"></a>Tornare alla pagina precedente quando si verifica un errore di una sequenza di attività
È ora possibile tornare alla pagina precedente quando si esegue una sequenza di attività e si verifica un errore. Prima di questa versione, se si verificava un errore era necessario riavviare la sequenza di attività. È ad esempio possibile usare il pulsante **Precedente** negli scenari seguenti:

- Quando un computer viene avviato in Windows PE, potrebbe essere visualizzata la finestra di dialogo di avvio della sequenza di attività prima che la sequenza stessa sia disponibile. Se in questo scenario si fa clic su Avanti, viene visualizzata la pagina finale della sequenza di attività che informa l'utente che non sono disponibili sequenze di attività. È ora possibile fare clic su **Precedente** per ripetere la ricerca di sequenze di attività. È possibile ripetere questo processo finché la sequenza di attività non è disponibile.
- Quando si esegue una sequenza di attività ma i pacchetti di contenuto dipendenti non sono ancora disponibili nei punti di distribuzione, la sequenza di attività ha esito negativo. È ora possibile distribuire il contenuto mancante, se non è stato ancora distribuito, o attendere che il contenuto sia disponibile nei punti di distribuzione e quindi fare clic su **Precedente** per ripetere la ricerca di contenuto con la sequenza di attività.

### <a name="pre-cache-content-for-available-deployments-and-task-sequences"></a>Pre-cache del contenuto per le distribuzioni e le sequenze di attività disponibili
A partire dalla versione 1702, per le distribuzioni di sequenze di attività disponibili è possibile scegliere di usare la memorizzazione anticipata nella cache del contenuto. Con la funzionalità di pre-cache del contenuto è possibile consentire al client di scaricare solo il contenuto applicabile non appena riceve la distribuzione. Pertanto quando l'utente fa clic su **Installa** in Software Center, il contenuto è pronto e l'installazione inizia rapidamente, dato che il contenuto si trova nel disco rigido locale. Per informazioni dettagliate, vedere [Configurare la pre-cache del contenuto](../../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md#configure-pre-cache-content).

### <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Conversione da BIOS a UEFI durante un aggiornamento sul posto
Windows 10 Creators Update introduce un semplice strumento di conversione che automatizza il processo di ripartizione del disco rigido per l'hardware abilitato per UEFI e integra lo strumento di conversione nel processo di aggiornamento sul posto da Windows 7 a Windows 10. Quando si usa questo strumento in combinazione con la sequenza di attività di aggiornamento del sistema operativo e con lo strumento OEM che converte il firmware da BIOS a UEFI, è possibile convertire i computer da BIOS a UEFI durante un aggiornamento sul posto a Windows 10 Creators Update. Per informazioni dettagliate, vedere [Passaggi della sequenza di attività per la gestione della conversione da BIOS a UEFI](../../../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md#bkmk_ipu).

### <a name="improvements-to-the-install-applications-task-sequence-step"></a>Miglioramenti della sequenza di attività Installa applicazioni
In questa versione sono stati introdotti i miglioramenti seguenti:
- Nel passaggio della sequenza di attività **Installa applicazioni** il numero massimo di applicazioni che è possibile installare è stato aumentato a 99. Il numero massimo precedente era di 9 applicazioni.
- Quando si aggiungono applicazioni al passaggio della sequenza di attività **Installa applicazioni** nell'editor delle sequenze di attività, è ora possibile selezionare più applicazioni dal riquadro **Seleziona l'applicazione da installare**.

### <a name="improvements-to-the-auto-apply-driver-task-sequence"></a>Miglioramenti della sequenza di attività Applica automaticamente i driver
Sono ora disponibili nuove variabili della sequenza di attività per la configurazione del valore di timeout nel passaggio della sequenza di attività Applica automaticamente i driver durante la creazione di richieste di catalogo HTTP. Sono disponibili le seguenti variabili e valori predefiniti (in secondi):
- SMSTSDriverRequestResolveTimeOut  
  Impostazione predefinita: 60
- SMSTSDriverRequestConnectTimeOut  
  Impostazione predefinita: 60
- SMSTSDriverRequestSendTimeOut  
  Impostazione predefinita: 60
- SMSTSDriverRequestReceiveTimeOut  
  Impostazione predefinita: 480

### <a name="windows-10-adk-tracked-by-build-version"></a>Windows 10 ADK rilevato dalla versione build
Windows 10 ADK viene ora rilevato dalla versione build per garantire maggior supporto durante la personalizzazione delle immagini d'avvio di Windows 10. Ad esempio, se il sito usa Windows ADK per Windows 10, versione 1607, possono essere personalizzate nella console soltanto le immagini d'avvio con versione 10.0.14393. Per informazioni dettagliate sulla personalizzazione delle versioni WinPE, vedere [Personalizzare le immagini d'avvio](../../../osd/get-started/customize-boot-images.md).

### <a name="default-boot-image-source-path-can-no-longer-be-changed"></a>Percorso di origine dell'immagine d'avvio predefinita non più modificabile
Le immagini d'avvio predefinite sono gestite da Configuration Manager e il percorso di origine dell'immagine d'avvio predefinita non può più essere modificato nella console di Configuration Manager o tramite Configuration Manager SDK. È possibile continuare a configurare un percorso di origine personalizzato per le immagini d'avvio personalizzate.

### <a name="default-boot-images-are-regenerated-after-upgrading-configuration-manager-to-a-new-version"></a>Le immagini di avvio predefinite vengono rigenerate dopo l'aggiornamento di Configuration Manager a una nuova versione
A partire da questa versione, quando si aggiorna la versione di Windows ADK e quindi si usano gli aggiornamenti e le versioni di manutenzione per installare la versione più recente di Configuration Manager, Configuration Manager rigenera le immagini di avvio predefinite. Ciò include la nuova versione di Windows PE dalla versione aggiornata di Windows ADK, la nuova versione del client di Configuration Manager, i driver, le personalizzazioni e così via. Le immagini di avvio personalizzate non vengono modificate. Per altri dettagli, vedere [Gestire le immagini di avvio](../../../osd/get-started/manage-boot-images.md#BKMK_BootImageDefault).

## <a name="software-updates"></a>Aggiornamenti software

### <a name="deploy-office-365-apps-to-clients"></a>Distribuire le app di Office 365 sui client
A partire dalla versione 1702, nel dashboard Gestione client di Office 365 è possibile avviare il programma di installazione di Office 365, che consente di configurare le impostazioni di installazione di Office 365, scaricare file dalle reti di distribuzione del contenuto (CDN) e distribuire i file come applicazione in Configuration Manager. Per informazioni dettagliate, vedere [Gestire gli aggiornamenti di Office 365 ProPlus](../../../sum/deploy-use/manage-office-365-proplus-updates.md#deploy-office-365-apps).

> [!IMPORTANT]
> L'app di Office 365 creata e distribuita mediante la Creazione guidata dell'applicazione di Office 365 in Configuration Manager non viene gestita automaticamente da Configuration Manager fino a quando non si abilita l'impostazione dell'agente client degli aggiornamenti software **Enable management of the Office 365 Client Again** (Abilita di nuovo la gestione del client Office 365). Per altre informazioni, vedere [Informazioni sulle impostazioni client](../../clients/deploy/about-client-settings.md).

### <a name="manage-express-installation-files-for-windows-10-updates"></a>Gestire i file di installazione rapida per gli aggiornamenti di Windows 10
A partire dalla versione 1702, Configuration Manager supporta i file di installazione rapida per gli aggiornamenti di Windows 10. Se si usa una versione supportata di Windows 10, è possibile usare le impostazioni di Configuration Manager per scaricare solo le differenze tra l'aggiornamento cumulativo di Windows 10 del mese corrente e l'aggiornamento cumulativo del mese precedente. Senza i file di installazione rapida, Configuration Manager scarica ogni mese l'aggiornamento cumulativo completo di Windows 10, inclusi tutti gli aggiornamenti dei mesi precedenti. Grazie ai file di installazione rapida sono possibili download più brevi e tempi di installazione più rapidi per i client. Per informazioni dettagliate, vedere [Gestire i file di installazione rapida per gli aggiornamenti di Windows 10](../../../sum/deploy-use/manage-express-installation-files-for-windows-10-updates.md).


<!-- ## Reporting  -->

<!-- ## Inventory  -->

## <a name="mobile-device-management"></a>Gestione di dispositivi mobili

### <a name="android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm"></a>Non è più necessario specificare le versioni di Android e iOS nella creazione guidata della gestione ibrida dei dispositivi mobili

A partire dalla versione1702 per la gestione ibrida dei dispositivi mobili, quando si creano nuovi criteri e profili per i dispositivi gestiti in Intune, non è più necessario indicare versioni specifiche di Android e iOS. È necessario però scegliere uno dei tipi di dispositivo seguenti:

- Android
- Samsung KNOX Standard 4.0 e versioni successive
- iPhone
- iPad

Questa modifica interessa la creazione guidata degli elementi seguenti:

- Elementi di configurazione
- Criteri di conformità
- Profili certificato
- Profili di posta elettronica
- Profili VPN
- Profili Wi-Fi

Con questa modifica, le distribuzioni ibride possono offrire il supporto più rapidamente per le nuove versioni di Android e iOS, senza attendere una nuova versione o un'estensione di Configuration Manager. Quando una nuova versione è supportata nella versione autonoma di Intune, gli utenti possono aggiornare i propri dispositivi mobili a tale versione.

Per evitare problemi durante l'aggiornamento da versioni precedenti di Configuration Manager, le versioni dei sistemi operativi dei dispositivi mobili sono ancora disponibili nelle pagine delle proprietà di tali elementi. Se è ancora necessario usare una versione specifica, è possibile creare il nuovo elemento e quindi specificare la versione nella pagina delle proprietà dell'elemento appena creato. 

> [!NOTE]
> L'ultima versione del sistema operativo per dispositivi mobili disponibile nelle pagine delle proprietà si applica a tale versione e a tutte quelle successive. Le pagine delle proprietà forniscono le seguenti opzioni per la definizione dei sistemi operativi successivi ad Android 7 e iOS 10: 
> - **Android 7 e versioni successive**
> - **Tutti i dispositivi iPhone o iPod touch iOS 10 e versioni successive**
> - **Tutti i dispositivi iPad iOS 10 e versioni successive**

### <a name="android-for-work-support"></a>Supporto per Android for Work
A partire dalla versione 1702, la gestione ibrida dei dispositivi mobili con Microsoft Intune supporta ora la registrazione e la gestione del dispositivo in Android for Work.

### <a name="deploy-volume-purchased-ios-apps-to-device-collections"></a>Distribuire app iOS acquistate con Volume Purchase Program a raccolte di dispositivi

È ora possibile distribuire app con licenza sia ai dispositivi che agli utenti. In base alla possibilità dell'app di supportare la gestione delle licenze dei dispositivi, al momento della distribuzione verrà richiesta una licenza appropriata, come indicato di seguito:

|||||
|-|-|-|-|
|Versione di Configuration Manager|Gestione delle licenze dei dispositivi supportata|Tipo di raccolta della distribuzione|Licenza richiesta|
|Precedente la 1702|Sì|Utente|Licenza utente|
|Precedente la 1702|No|Utente|Licenza utente|
|Precedente la 1702|Sì|Dispositivo|Licenza utente|
|Precedente la 1702|No|Dispositivo|Licenza utente|
|1702 e versioni successive|Sì|Utente|Licenza utente|
|1702 e versioni successive|No|Utente|Licenza utente|
|1702 e versioni successive|Sì|Dispositivo|Licenza dispositivo|
|1702 e versioni successive|No|Dispositivo|Licenza utente|

### <a name="support-for-ios-volume-purchase-program-for-education"></a>Supporto per iOS Volume Purchase Program for Education

È ora possibile anche distribuire e tenere traccia delle app acquistate tramite iOS Volume Purchase Program for Education.

### <a name="support-for-multiple-volume-purchase-program-tokens"></a>Supporto per più token di Volume Purchase Program

È ora possibile associare a Configuration Manager più token di Volume Purchase Program di Apple.

### <a name="support-for-line-of-business-apps-in-windows-store-for-business"></a>Supporto per app line-of-business in Windows Store per le aziende

È ora possibile sincronizzare app line-of-business personalizzate da Windows Store per le aziende.

### <a name="conditional-access-device-compliance-policy-improvements"></a>Miglioramento dei criteri di conformità dei dispositivi per l'accesso condizionale

È ora disponibile una nuova regola di criteri di conformità dei dispositivi per impedire l'accesso alle risorse aziendali che supportano l'accesso condizionale, quando gli utenti usano applicazioni incluse in un elenco di app non conformi. L'elenco di app non conformi può essere definito dall'amministratore quando si aggiunge la nuova regola conforme **App che non possono essere installate**. Questa regola richiede che l'amministratore immetta **Nome app**, **ID app** e **Autore app** (facoltativo) quando si aggiunge un'app all'elenco di app non conformi. Questa impostazione si applica solo a dispositivi iOS e Android.

Ciò consente alle organizzazioni di ridurre la perdita di dati da app non protette e di impedire l'uso eccessivo di dati in alcune applicazioni.


### <a name="new-mobile-threat-defense-monitoring-tools"></a>Nuovi strumenti di monitoraggio Mobile Threat Defense

A partire dalla versione 1702, sono disponibili nuovi strumenti per il monitoraggio dello stato di conformità con il provider di servizi Mobile Threat Defense.


## <a name="protect-devices"></a>Proteggere i dispositivi

### <a name="detect-outdated-antimalware-client-versions"></a>Rilevare le versioni client antimalware obsolete
A partire dalla versione 1702, è possibile configurare un avviso per verificare che i client Endpoint Protection non siano obsoleti. Per altre informazioni, vedere [Configurare gli avvisi di Endpoint Protection in Configuration Manager](../../../protect/deploy-use/endpoint-configure-alerts.md#alert-for-outdated-malware-client).

### <a name="device-health-attestation-updates"></a>Aggiornamenti dell'attestazione dell'integrità del dispositivo
Il servizio di attestazione dell'integrità del dispositivo per i client locali può ora essere configurato e gestito dal punto di gestione. Per altre informazioni, vedere [Attestazione dell'integrità](../../servers/manage/health-attestation.md).

### <a name="certificate-profiles-for-windows-hello-for-business"></a>Profili certificato per Windows Hello for Business

Se si vogliono archiviare i profili certificato nel contenitore chiave Windows Hello for Business e il profilo certificato usa l'EKU per l'accesso smart card, è necessario configurare le autorizzazioni per la registrazione delle chiavi per garantire che il certificato venga convalidato correttamente.
Per altre informazioni, vedere [Impostazioni di Windows Hello for Business](../../../protect/deploy-use/windows-hello-for-business-settings.md).

### <a name="new-windows-hello-for-business-notification-for-end-users"></a>Nuova notifica di Windows Hello for Business per gli utenti finali
Una nuova notifica di Windows 10 informa gli utenti che sono necessarie azioni aggiuntive per completare l'installazione di Windows Hello for Business, ad esempio l'impostazione di un PIN.
