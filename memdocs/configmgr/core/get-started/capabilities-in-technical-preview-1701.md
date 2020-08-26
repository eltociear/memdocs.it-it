---
title: Funzionalità nella Technical Preview 1701
titleSuffix: Configuration Manager
description: Informazioni sulle funzionalità disponibili nella versione Technical Preview 1701 per Configuration Manager.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 18598eaa-1131-44ff-8f8b-6093e87ac7a1
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: a9d0beeee1e00315a913adfc5dde6bd69f75cd6f
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692996"
---
# <a name="capabilities-in-technical-preview-1701-for-configuration-manager"></a>Funzionalità della versione Technical Preview 1701 per Configuration Manager

*Si applica a: Configuration Manager (Technical Preview Branch)*



Questo articolo presenta le funzionalità disponibili nella Technical Preview per Configuration Manager versione 1701. È possibile installare questa versione per aggiornare e aggiungere nuove funzionalità al sito di Technical Preview di Configuration Manager. Prima di installare questa versione Technical Preview, consultare l'argomento introduttivo [Technical Preview per Center Configuration Manager](../../core/get-started/technical-preview.md) per acquisire familiarità con i requisiti generali e con le limitazioni per l'uso di una versione Technical Preview, con le modalità di aggiornamento tra le versioni e con le modalità per offrire commenti e suggerimenti sulle funzionalità di una versione Technical Preview.    


**Di seguito sono riportate le nuove funzionalità disponibili con questa versione.**  

## <a name="boundary-groups-improvements-for-software-update-points"></a>Miglioramenti dei gruppi di limiti per i punti di aggiornamento software
A partire da questa versione di anteprima, vengono usati gruppi di limiti per associare i client ai punti di aggiornamento software. Questo fa parte di un'attività continua finalizzata a espandere le modifiche per i gruppi di limiti per gestire altri ruoli del sistema del sito.  Le modifiche per i gruppi di limiti sono state introdotte per la prima volta nella versione Technical Preview 1609 e in Current Branch nella versione 1610.  

In questa anteprima viene usato il nuovo comportamento dei gruppi di limiti per gestire i punti di aggiornamento software che possono essere usati da un client in modo simile a come viene gestito il punto di distribuzione che può essere usato da un client:  

- Vengono configurati i gruppi di limiti per associare uno o più server che ospitano un punto di aggiornamento software.
- I client che cercano un nuovo punto di aggiornamento software tenteranno di usare un punto associato al gruppo di limiti corrente.
- Quando un client non raggiunge il punto di aggiornamento software corrente e non ne individua uno del gruppo di limiti corrente, il client usa il comportamento di fallback per espandere il pool di punti di aggiornamento software disponibili utilizzabili.    

Per altre informazioni sui gruppi di limiti, vedere [Gruppi di limiti](../servers/deploy/configure/boundary-groups.md) nei contenuti relativi a Current Branch.

In questa anteprima, tuttavia, i gruppi di limiti per i punti di aggiornamento software sono implementati solo parzialmente. Sebbene sia possibile aggiungere punti di aggiornamento software e configurare gruppi di limiti adiacenti contenenti punti di aggiornamento software, il tempo di fallback per i punti di aggiornamento software non è ancora supportato e i client avranno un'attesa di due ore prima di iniziare il fallback.

Di seguito è descritto il funzionamento per i punti di aggiornamento software con la presente versione Technical Preview:  

- **I nuovi client usano i gruppi di limiti per selezionare i punti di aggiornamento software.** Un client installato dopo aver installato la versione 1701 seleziona un punto di aggiornamento software tra quelli associati al gruppo di limiti del client.

  Viene sostituito il comportamento precedente in cui i client selezionano un punto di aggiornamento software casuale da un elenco di punti che condividono la foresta dei client.   

- **I client installati in precedenza continuano a usare il punto di aggiornamento software corrente fino a quando non eseguono il fallback per trovare un nuovo punto.**
  I client installati in precedenza e che hanno già un punto di aggiornamento software continueranno a usare il punto di aggiornamento software fino a quando non eseguono il fallback. Sono inclusi i punti di aggiornamento software non associati al gruppo di limiti corrente del client. Non tentano immediatamente di trovare e usare un punto di aggiornamento software del gruppo di limiti corrente.

  Un client che ha già un punto di aggiornamento software inizia a usare questo nuovo comportamento dei gruppi di limiti solo dopo non aver raggiunto il punto di aggiornamento software corrente e aver iniziato il fallback.
  Questo ritardo nel passaggio al nuovo comportamento è intenzionale. Questo avviene perché una modifica del punto di aggiornamento software può comportare un utilizzo elevato della larghezza di banda di rete poiché il client sincronizza i dati con il nuovo punto di aggiornamento software. Il ritardo nella transizione può evitare la saturazione della rete nel caso in cui tutti i client passino a nuovi punti di aggiornamento software contemporaneamente.

- **Configurazioni per l'orario di fallback:** le configurazioni relative al momento in cui i client iniziano il fallback per la ricerca di un nuovo punto di aggiornamento software non sono supportate in questa versione Technical Preview. Sono incluse le configurazioni per **Fallback times (in minutes)** (Tempi di fallback in minuti) e **Never fallback** (Nessun fallback) che è possibile configurare per relazioni di gruppi di limiti diverse.

  I client mantengono invece il comportamento corrente in cui il client tenta di connettersi al relativo punto di aggiornamento software corrente per due ore prima di iniziare il fallback per trovare un nuovo punto di aggiornamento software utilizzabile.

  Quando un client usa il fallback, userà le configurazioni dei gruppi di limiti per il fallback per creare un pool di punti di aggiornamento software disponibili. Il pool include tutti i punti di aggiornamento software del *gruppo di limiti corrente* dei client, dei *gruppi di limiti adiacenti* e del *gruppo di limiti predefinito del sito* dei client.

- **Configurare il gruppo di limiti del sito predefinito:**  
  Considerare l'aggiunta di un punto di aggiornamento software a *Default-Site-Boundary-Group&lt;codicesito>* . Ciò garantisce che i client che non sono membri di un altro gruppo di limiti possano eseguire il fallback per trovare un punto di aggiornamento software.


Per gestire i punti di aggiornamento software per i gruppi di limiti, usare le [procedure della documentazione di Current Branch](../servers/deploy/configure/boundary-group-procedures.md) ricordando che i tempi di fallback che potrebbero essere configurati non vengono ancora usati per i punti di aggiornamento software.


## <a name="hardware-inventory-collects-uefi-information"></a>L'inventario hardware raccoglie le informazioni UEFI
Una nuova classe di inventario hardware (**SMS_Firmware**) e una nuova proprietà (**UEFI**) sono disponibili per determinare se un computer viene avviato in modalità UEFI. Quando un computer viene avviato in modalità UEFI, la proprietà **UEFI** è impostata su **TRUE**. L'impostazione è abilitata nell'inventario hardware per impostazione predefinita. Per altre informazioni sull'inventario hardware, vedere [How to configure hardware inventory](../clients/manage/inventory/configure-hardware-inventory.md) (Come configurare l'inventario hardware).

## <a name="improvements-to-operating-system-deployment"></a>Miglioramenti alla distribuzione del sistema operativo
Sono stati apportati i miglioramenti seguenti alla distribuzione del sistema operativo, molti dei quali sono il risultato del feedback degli utenti.
- [**Supporto di più applicazioni per il passaggio della sequenza di attività Installa applicazioni**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17062207-task-sequence-allow-more-than-9-applications-in-t): nel passaggio della sequenza di attività **Installa applicazioni** il numero massimo di applicazioni che è possibile installare è stato aumentato a 99. Il numero massimo precedente era di 9 applicazioni.
- [**Selezionare più app nel passaggio della sequenza di attività Installa app**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15459978-when-adding-items-to-an-install-application-step): quando si aggiungono applicazioni al passaggio della sequenza di attività Installa applicazione nell'editor delle sequenze di attività, è ora possibile selezionare più applicazioni dal riquadro **Seleziona l'applicazione da installare**.
- [**Scadenza dei supporti autonomi**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/14448564-provide-a-method-for-expiring-standalone-media): Quando si creano supporti autonomi, sono disponibili nuove opzioni per l'impostazione di date facoltative di inizio e scadenza nei supporti. Queste impostazioni sono disabilitate per impostazione predefinita. Le date vengono confrontate con l'ora di sistema nel computer prima che il supporto autonomo venga eseguito. Quando l'ora di sistema è precedente all'ora di inizio o successiva all'ora di scadenza, il supporto autonomo non viene avviato. Queste opzioni sono disponibili anche tramite il cmdlet PowerShell New-CMStandaloneMedia.
- [**Supporto per contenuto aggiuntivo nei supporti autonomi**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8341257-support-installation-of-packages-apps-via-dynamic): È ora supportato contenuto aggiuntivo nei supporti autonomi. È possibile selezionare altri pacchetti, pacchetti driver e applicazioni da gestire nei supporti insieme ad altro contenuto cui viene fatto riferimento nella sequenza di attività. In precedenza, soltanto il contenuto cui veniva fatto riferimento nella sequenza di attività veniva gestito nei supporti autonomi.
- [**Timeout configurabile per il passaggio della sequenza di attività Applica automaticamente i driver**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17153660-auto-apply-driver-timeout): Sono ora disponibili nuove variabili della sequenza di attività per la configurazione del valore di timeout nel passaggio della sequenza di attività Applica automaticamente i driver durante la creazione di richieste di catalogo HTTP. Sono disponibili le seguenti variabili e valori predefiniti (in secondi):
   - SMSTSDriverRequestResolveTimeOut Default: 60
   - SMSTSDriverRequestConnectTimeOut Default: 60
   - SMSTSDriverRequestSendTimeOut Default: 60
   - SMSTSDriverRequestReceiveTimeOut Default: 480
- [**L'ID pacchetto viene ora visualizzato nei passaggi della sequenza di attività**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/16167430-display-packageid-when-viewing-a-task-sequence-ste): I passaggi della sequenza di attività che fanno riferimento a un pacchetto, un pacchetto driver, un'immagine del sistema operativo, un'immagine d'avvio o un pacchetto di aggiornamento del sistema operativo visualizzano ora l'ID pacchetto dell'oggetto a cui viene fatto riferimento. Quando un passaggio della sequenza di attività fa riferimento a un'applicazione viene visualizzato l'ID oggetto.
- **Windows 10 ADK rilevato dalla versione build**: Windows 10 ADK viene ora rilevato dalla versione build per garantire maggior supporto durante la personalizzazione delle immagini d'avvio di Windows 10. Ad esempio, se il sito usa Windows ADK per Windows 10, versione 1607, possono essere personalizzate nella console soltanto le immagini d'avvio con versione 10.0.14393. Per informazioni dettagliate sulla personalizzazione delle versioni WinPE, vedere [Personalizzare le immagini d'avvio](../../osd/get-started/customize-boot-images.md).
- **Percorso di origine dell'immagine d'avvio predefinita non più modificabile**: Le immagini d'avvio predefinite sono gestite da Configuration Manager e il percorso di origine dell'immagine d'avvio predefinita non può più essere modificato nella console di Configuration Manager o tramite Configuration Manager SDK. È possibile continuare a configurare un percorso di origine personalizzato per le immagini d'avvio personalizzate.

## <a name="host-software-updates-on-cloud-based-distribution-points"></a>Ospitare gli aggiornamenti software in punti di distribuzione basati sul cloud
A partire da questa versione di anteprima, è possibile usare un punto di distribuzione basato sul cloud per ospitare un pacchetto di aggiornamento software. Tuttavia, poiché è possibile configurare i client per scaricare gli aggiornamenti software direttamente da Microsoft Update, considerare i possibili costi aggiuntivi per la distribuzione di un pacchetto di aggiornamento software a un punto di distribuzione basato sul cloud.

Per informazioni sull'uso di punti di distribuzione basati sul cloud, vedere [Usare un punto di distribuzione basato sul cloud](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md) nel contenuto relativo a Current Branch di Configuration Manager.

## <a name="validate-device-health-attestation-data-via-management-points"></a>Convalidare i dati di attestazione dell'integrità del dispositivo tramite punti di gestione

A partire da questa versione di anteprima, è possibile configurare punti di gestione per convalidare i dati di reporting di attestazione dell'integrità per il servizio di attestazione dell'integrità cloud o locale. Una nuova scheda **Opzioni avanzate** della finestra di dialogo **Proprietà del componente del punto di gestione** consente di **aggiungere**, **modificare** o **rimuovere** l'**URL del servizio di attestazione dell'integrità del dispositivo locale**. È anche possibile specificare le **Impostazioni dispositivo personalizzate** per l'agente client per **usare il servizio di attestazione dell'integrità locale**.  Se l'opzione viene impostata su **Sì**, verrà abilitato il reporting nel punto di gestione locale anziché il servizio basato sul cloud.

### <a name="try-it-out"></a>Procedura

- **Abilitare l'attestazione dell'integrità del dispositivo locale in un punto di gestione**<br>  Nella console di Configuration Manager passare al punto di gestione e aprire **Proprietà del componente del punto di gestione** e quindi fare clic sulla scheda **Opzioni avanzate**. Fare clic su **Aggiungi** e specificare l'URL locale, ad esempio https://10.10.10.10), per **URL del servizio di attestazione dell'integrità locale**.
- **Abilitare il reporting di attestazione dell'integrità del punto di gestione locale per l'agente client**<br>Nella console di Configuration Manager scegliere **Amministrazione** > **Impostazioni client** e fare doppio clic o creare nuove **Impostazioni dispositivo personalizzate**. Selezionare **Agente computer** e impostare **Usare il servizio di attestazione dell'integrità locale** su **Sì**. Se **Abilita le comunicazioni con il servizio di attestazione dell'integrità** è impostata su **Sì** e **Usare il servizio di attestazione dell'integrità locale** è impostata su **No**, il punto di gestione userà il servizio di attestazione dell'integrità del dispositivo basato sul cloud.

## <a name="use-the-oms-connector-for-microsoft-azure-government-cloud"></a>Usare il connettore OMS per il cloud di Microsoft Azure per enti pubblici
Con questa versione Technical Preview è possibile usare il connettore Microsoft Operations Management Suite (OMS) per la connessione a un'area di lavoro OMS che si trova sul cloud di Microsoft Azure per enti pubblici.  

A tale scopo, modificare un file di configurazione in modo che punti al cloud per enti pubblici e quindi installare il connettore OMS.

### <a name="set-up-an-oms-connector-to-microsoft-azure-government-cloud"></a>Impostare un connettore OMS per il cloud di Microsoft Azure per enti pubblici
1. In un computer in cui è installata la console di Configuration Manager modificare il file di configurazione seguente in modo che punti al cloud per enti pubblici:  ***&lt;percorso di installazione CM>\AdminConsole\bin\Microsoft.configurationManagmenet.exe.config***

   **Modifiche:**

   Modificare il valore del nome dell'impostazione *FairFaxArmResourceID* in modo che sia uguale a "<https://management.usgovcloudapi.net/">

   - **Originale:** &lt;setting name="FairFaxArmResourceId" serializeAs="String">   
     &lt;value>&lt;/value>   
     &lt;/setting>

   - **Modificato:**      
     &lt;setting name="FairFaxArmResourceId" serializeAs="String"> &lt;value&gt;https://management.usgovcloudapi.net/&lt;/value&gt;  
     &lt;/setting>

   Modificare il valore del nome dell'impostazione *FairFaxAuthorityResource* in modo che sia uguale a "<https://login.microsoftonline.com/>"

   - **Originale:** &lt;setting name="FairFaxAuthorityResource" serializeAs="String">   
     &lt;value>&lt;/value>

   - **Modificato:** &lt;setting name="FairFaxAuthorityResource" serializeAs="String">   
     &lt;value&gt;[https://login.microsoftonline.com](https://login.microsoftonline.com)&lt; /value&gt;

2. Dopo aver salvato il file con le due modifiche, riavviare la console di Configuration Manager nello stesso computer e quindi usare la console per installare il connettore OMS. Per installare il connettore, usare le informazioni in [Sincronizzazione dei dati da Configuration Manager a Microsoft Operations Management Suite](/azure/azure-monitor/platform/collect-sccm) e selezionare l'**Area di lavoro di Operations Management Suite** che si trova nel cloud di Microsoft Azure per enti pubblici.

3. Dopo aver installato il connettore OMS, la connessione al cloud per enti pubblici sarà disponibile quando si usa qualsiasi console che si connette al sito.

## <a name="android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm"></a>Non è più necessario specificare le versioni di Android e iOS nella creazione guidata della gestione ibrida dei dispositivi mobili

A partire dalla presente Technical Preview, per la gestione ibrida dei dispositivi mobili non è più necessario indicare versioni specifiche di Android e iOS quando si creano nuovi criteri e profili per i dispositivi gestiti in Intune. È necessario però scegliere uno dei tipi di dispositivo seguenti:

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