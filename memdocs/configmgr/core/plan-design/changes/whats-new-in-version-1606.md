---
title: Novità della versione 1606
titleSuffix: Configuration Manager
description: Informazioni dettagliate sulle modifiche e sulle nuove funzionalità introdotte nella versione 1606 di Configuration Manager.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: df2e57b9-6445-4067-98e7-ace85d4e6aa6
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 4298a6a66d60d79d05f8b5cdc9ff8caa0e7f4426
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074028"
---
# <a name="what39s-new-in-version-1606-of-configuration-manager"></a>Novità della versione 1606 di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

L'aggiornamento 1606 per Configuration Manager è disponibile solo come aggiornamento nella console per i siti installati in precedenza che eseguono la versione 1511 o 1602. La versione 1511 è la versione di base iniziale usata per installare nuovi siti di Configuration Manager.
> [!TIP]  
> Sono disponibili altre informazioni su:  
>   
> - [Installing new sites](../../servers/deploy/install/prepare-to-install-sites.md) (Installazione di nuovi siti) (con una versione di base, ad esempio 1511)  
> - [Installing updates at sites](../../servers/manage/updates.md) (Installazione di aggiornamenti nei siti) (ad esempio versione 1602 o 1606)  

 Le sezioni seguenti illustrano in dettaglio le modifiche e le nuove funzionalità introdotte nella versione 1606 di Configuration Manager.  



## <a name="updates-and-servicing"></a><a name="updatesandservicing"></a>Aggiornamenti e manutenzione

### <a name="changes-for-the-updates-and-servicing-node"></a>Modifiche per il nodo Aggiornamenti e manutenzione
Di seguito sono riportate le modifiche del nodo Aggiornamenti e manutenzione nella console di Configuration Manager:
> [!NOTE]
> Le modifiche saranno disponibili solo dopo l'installazione della versione 1606.

- **Modifica del nome del nodo:**

    Nell'area di lavoro **Monitoraggio** il nodo dello stato **Manutenzione del sito** è stato rinominato in **Aggiornamenti e stato di manutenzione**.
- **Altri dettagli sullo stato di installazione:**

    Quando si visualizza lo stato di installazione dell'aggiornamento di un sito, nella console vengono ora mostrate informazioni distinte per le azioni seguenti:
    - **Download** (si applica solo al sito di livello superiore in cui è installato il ruolo del sistema del sito del punto di connessione del servizio.)
    - **Replica**
    - **Controllo dei prerequisiti**
    - **Installazione**

  Inoltre, sono ora presenti più informazioni dettagliate per ogni passaggio, incluso il file di log nel quale è possibile visualizzare altre informazioni.  
-   **Nuova opzione per ignorare i messaggi sui prerequisiti non soddisfatti:**

    In entrambe le aree di lavoro **Amministrazione** e **Monitoraggio** il nodo **Aggiornamenti e manutenzione** include un nuovo pulsante sulla barra multifunzione denominato **Ignora avvisi dei prerequisiti**.

    Se si installa un aggiornamento senza usare l'opzione Ignora avvisi dei prerequisiti dalla procedura guidata e l'installazione dell'aggiornamento viene interrotta a causa di un avviso, è possibile selezionare **Ignora avvisi dei prerequisiti** dalla barra multifunzione. In questo modo viene attivata la continuazione automatica dell'installazione dell'aggiornamento.  



- **Visualizzazione più chiara degli aggiornamenti:**

    Nel nodo **Aggiornamenti e manutenzione** è ora possibile visualizzare solo l'aggiornamento installato più recente ed eventuali nuovi aggiornamenti disponibili per l'installazione. Per visualizzare gli aggiornamenti installati in precedenza, fare clic sul nuovo pulsante **Cronologia** visualizzato nella barra multifunzione.  

-   **Opzioni ridenominate per la fase di pre-produzione:**

    Nel nodo **Aggiornamenti e manutenzione** il pulsante **Opzioni client** è ora denominato **Alza di livello il client di pre-produzione**.


###  <a name="pre-release-features"></a>Funzionalità di versioni non definitive
A partire dalla versione 1606, è necessario dare il consenso all'uso delle funzionalità di versioni non definitive in System Center Configuration Manager per poterle selezionare e abilitarne l'uso. Per altre informazioni, vedere la sezione relativa all'[abilitazione delle funzionalità facoltative dagli aggiornamenti](../../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease).

### <a name="new-distribution-point-update-behavior"></a>Nuovo comportamento di aggiornamento dei punti di distribuzione
L'aggiornamento 1606 introduce modifiche che migliorano la disponibilità dei punti di distribuzione durante l'installazione degli aggiornamenti successivi.

Dopo l'installazione dell'aggiornamento 1606, quando nel sito verrà installato un aggiornamento che richiede la reinstallazione automatica dei ruoli del sistema del sito del punto di distribuzione standard e pull, i punti di distribuzione non andranno offline contemporaneamente. Al contrario, il server del sito usa le impostazioni di distribuzione del contenuto del sito per distribuire l'aggiornamento a un sottoinsieme di punti di distribuzione alla volta. Ne consegue che solo alcuni punti di distribuzione saranno offline per consentire l'installazione dell'aggiornamento. I punti di distribuzione per i quali non è stato avviato l'aggiornamento o che lo hanno completato restano online e continuano a fornire contenuto ai client.



## <a name="accessibility"></a><a name="accessibility"></a> Accessibilità
Per spostarsi tra i vari nodi di un'area di lavoro, è ora possibile immettere la prima lettera del nome di un nodo. Quando si preme il tasto, il cursore si sposta sul nodo successivo che inizia con tale lettera. Se si usa un'utilità per la lettura dello schermo, verrà letto il nome del nodo. Per altre informazioni sulle opzioni di accessibilità, vedere [Funzionalità di accessibilità](../../../core/understand/accessibility-features.md).

## <a name="administration"></a><a name="administration"></a>Amministrazione
Di seguito sono riportate le modifiche del nodo Amministrazione nella console di Configuration Manager:
### <a name="oms-connector"></a>Connettore OMS

È ora possibile connettere le raccolte di Configuration Manager da System Center Configuration Manager a [Microsoft Operations Management Suite (OMS)](https://azure.microsoft.com/documentation/articles/operations-management-suite-overview/). In questo modo i dati, ad esempio le raccolte delle distribuzioni di Configuration Manager, sono visibili in OMS. Per altre informazioni, vedere [Sincronizzazione dei dati da Configuration Manager a Microsoft Operations Management Suite](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm).

Il connettore OMS è una funzionalità di versione non definitiva. Per abilitarla, vedere [Usare le funzionalità di versioni non definitive degli aggiornamenti](../../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease).

### <a name="support-for-cache-size-in-client-settings"></a>Supporto per la dimensione della cache in Impostazioni client

È ora possibile configurare la dimensione della cartella cache nei computer client usando **Impostazioni client** nella console di Configuration Manager. In precedenza, era possibile impostare la dimensione della cache client soltanto durante l'installazione o la reinstallazione del software client. Ora è possibile specificare la dimensione della cache come impostazione client predefinita o personalizzata e quindi applicare tale impostazione al successivo aggiornamento dei criteri nel client, senza dover reinstallare il client stesso. Per ulteriori informazioni, vedere [Configurare la cache del client per i client di Configuration Manager](../../../core/clients/manage/manage-clients.md#BKMK_ClientCache).

## <a name="on-premises-mobile-device-management"></a>Gestione di dispositivi mobili locale

### <a name="support-for-multiple-device-management-points"></a>Supporto per più punti di gestione periferiche

Il sistema di gestione dei dispositivi mobili (MDM) locale supporta ora una nuova funzionalità nell'Aggiornamento dell'anniversario di Windows 10 che configura automaticamente un dispositivo registrato affinché usi più di un punto di gestione periferiche. Questa funzionalità consente al dispositivo il fallback su un altro punto di gestione periferiche quando quello che usa di solito non è disponibile. La funzionalità è operativa solo nei PC e nei dispositivi nei quali è stato installato l'Aggiornamento dell'anniversario di Windows 10.


## <a name="application-management"></a>Gestione delle applicazioni

### <a name="manage-apps-from-the-windows-store-for-business"></a>Gestire le app da Windows Store per le aziende

In [Windows Store per le aziende](https://www.microsoft.com/business-store) è possibile trovare e acquistare app Windows per l'organizzazione, singolarmente o con Volume Purchase Program. Collegando lo Store a Configuration Manager, è possibile sincronizzare l'elenco delle app acquistate, visualizzarle nella console di Configuration Manager e distribuirle come qualsiasi altra app.

Per informazioni dettagliate, vedere [Gestire le app da Windows Store per le aziende con Configuration Manager](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).

### <a name="manage-ios-volume-purchased-apps"></a>Gestione delle app iOS acquistate con Volume Purchase Program

Il flusso di lavoro per la gestione delle app iOS acquistate con Volume Purchase Program e per la loro distribuzione con Configuration Manager è stato migliorato.


### <a name="software-center-user-interface"></a>Interfaccia utente di Software Center

L'interfaccia utente di Software Center è stata ottimizzata per semplificare l'individuazione.
*  Le schede **Stato dell'installazione** e **Software installato** sono state unificate nella scheda **Stato dell'installazione**.
*  **Aggiornamenti**, **Sistemi operativi** e **Applicazioni** sono ora tre schede distinte.
* È possibile selezionare più aggiornamenti da installare singolarmente oppure installare tutti gli aggiornamenti contemporaneamente facendo clic sul pulsante **Installa tutto**.

### <a name="content-status-links"></a>Collegamenti allo stato del contenuto
Nelle proprietà di un'applicazione o di un pacchetto è ora presente un collegamento che indirizza allo stato dell'oggetto visualizzato.

## <a name="software-updates"></a>Aggiornamenti software

### <a name="client-setting-to-manage-the-office-365-client-agent"></a>Impostazione del client per la gestione dell'agente client di Office 365
È ora possibile utilizzare un'impostazione del client Configuration Manager per gestire l'agente client di Office 365. Dopo aver configurato questa impostazione e distribuito gli aggiornamenti di Office 365, l'agente client di Configuration Manager interagisce con l'agente client di Office 365 per scaricare e installare gli aggiornamenti di Office 365 da un punto di distribuzione.

Per informazioni dettagliate, vedere [Gestire gli aggiornamenti di Office 365 ProPlus con Configuration Manager](../../../sum/deploy-use/manage-office-365-proplus-updates.md).

### <a name="manually-switch-clients-to-a-new-software-update-point"></a>Passaggio manuale dei client a un nuovo punto di aggiornamento software
È possibile abilitare un'opzione che consente ai client di Configuration Manager di passare a un nuovo punto di aggiornamento software quando si verificano problemi con il punto di aggiornamento software attivo. Dopo che l'opzione è stata abilitata, in occasione dell'analisi successiva il client cercherà un altro punto di aggiornamento software.

Per informazioni dettagliate, vedere [Pianificare gli aggiornamenti software in Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md#BKMK_ManuallySwitchSUPs).

### <a name="restart-options-for-windows-10-clients-after-software-update-installation"></a>Opzioni di riavvio per i client Windows 10 dopo l'installazione degli aggiornamenti software
Quando un aggiornamento software che richiede il riavvio viene distribuito tramite Configuration Manager e viene installato in un computer, viene pianificato un riavvio in sospeso. Viene anche visualizzata una finestra di dialogo di riavvio. A partire da Configuration Manager versione 1606, ogni volta che è presente un riavvio in sospeso per un aggiornamento software di Configuration Manager, sono disponibili le opzioni **Aggiorna e riavvia**e **Aggiorna e arresta** . Queste opzioni sono incluse nelle opzioni di risparmio energia di Windows dei computer Windows 10. Dopo aver usato una di queste opzioni, la finestra di dialogo di riavvio non verrà visualizzata dopo il riavvio del computer.

Per informazioni dettagliate, vedere [Pianificare gli aggiornamenti software](../../../sum/plan-design/plan-for-software-updates.md#BKMK_RestartOptions).

### <a name="run-software-updates-compliance-scan-immediately-after-a-client-installs-software-updates-and-restarts"></a>Eseguire l'analisi conformità degli aggiornamenti software subito dopo l'installazione degli aggiornamenti e il riavvio di un client
È ora possibile eseguire un'analisi conformità degli aggiornamenti software subito dopo l'installazione degli aggiornamenti e il riavvio di un client. Per configurare questo comportamento per una distribuzione, nella pagina **Esperienza utente** della Distribuzione guidata degli aggiornamenti software selezionare **Se un aggiornamento di questa distribuzione richiede un riavvio del sistema, eseguire un ciclo di valutazione della distribuzione degli aggiornamenti dopo il riavvio**. In questo modo, il client controlla la presenza di aggiornamenti software aggiuntivi che diventano applicabili dopo il riavvio e che possono quindi essere installati (e resi conformi) durante la stessa finestra di manutenzione. Per informazioni dettagliate, vedere [Distribuire automaticamente gli aggiornamenti software](../../../sum/deploy-use/automatically-deploy-software-updates.md) o [Distribuire manualmente gli aggiornamenti software](../../../sum/deploy-use/manually-deploy-software-updates.md).

## <a name="operating-system-deployment"></a>Distribuzione del sistema operativo

### <a name="improvements-to-the-task-sequence-step-install-software-updates"></a>Miglioramenti al passaggio della sequenza di attività: Installa aggiornamenti software
Una nuova impostazione, **Valuta gli aggiornamenti software dai risultati di analisi memorizzati nella cache**, consente di eseguire un'analisi completa degli aggiornamenti software invece di usare i risultati dell'analisi memorizzati nella cache. Per informazioni dettagliate, vedere [Passaggi della sequenza di attività](../../../osd/understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates).

È anche disponibile la nuova variabile della sequenza di attività **SMSTSSoftwareUpdateScanTimeout**. Questa variabile consente di controllare il timeout per l'analisi degli aggiornamenti software durante il passaggio della sequenza di attività Installa aggiornamenti software. Il valore predefinito è 30 minuti. Per informazioni dettagliate, vedere [Variabili della sequenza di attività](../../../osd/understand/task-sequence-variables.md).

### <a name="osdpreservedriveletter-task-sequence-variable-has-been-deprecated"></a>La variabile della sequenza di attività OSDPreserveDriveLetter è stata deprecata
La variabile della sequenza di attività OSDPreserveDriveLetter è stata deprecata. A partire dalla versione 1606 di Configuration Manager, durante la distribuzione del sistema operativo, per impostazione predefinita l'installazione di Windows stabilisce qual è la lettera di unità migliore da usare (in genere C:).

Per informazioni dettagliate, vedere [Variabili della sequenza di attività](../../../osd/understand/task-sequence-variables.md).

### <a name="customize-the-ramdisk-tftp-window-size-for-pxe-enabled-distribution-points"></a>Personalizzazione delle dimensioni della finestra TFTP RamDisk nei punti di distribuzione abilitati per PXE
È ora possibile personalizzare le dimensioni della finestra nei punti di distribuzione abilitati per PXE. Se la rete è stata personalizzata, il download dell'immagine di avvio potrebbe non riuscire a causa di un errore di timeout perché le dimensioni della finestra sono troppo grandi. La personalizzazione delle dimensioni della finestra TFTP (Trivial File Transfer Protocol) RamDisk consente di ottimizzare il traffico TFTP quando si usa PXE per soddisfare requisiti di rete specifici.

Per informazioni dettagliate, vedere [Preparare i ruoli del sistema del sito per le distribuzioni del sistema operativo con Configuration Manager](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_RamDiskTFTP).

## <a name="compliance-settings"></a>Impostazioni di conformità

### <a name="smart-lock-setting-for-android-devices"></a>Impostazione di Smart Lock per dispositivi Android
La nuova impostazione **Consenti Smart Lock e altri agenti di attendibilità** è stata aggiunta all'elemento di configurazione Android e Samsung KNOX Standard.

L'impostazione consente di controllare la funzionalità Smart Lock su dispositivi compatibili con Android. Questa funzionalità del telefono, talvolta nota anche come "agenti di attendibilità", consente di disabilitare o ignorare la password della schermata di blocco del dispositivo se il dispositivo si trova in una posizione attendibile, ad esempio quando è connesso a un dispositivo Bluetooth specifico oppure quando è nelle vicinanze di un tag NFC. È possibile usare questa impostazione per impedire agli utenti di configurare Smart Lock.


## <a name="device-configuration-and-protection"></a>Configurazione e protezione del dispositivo

### <a name="product-name-changes"></a>Modifiche del nome del prodotto

* Microsoft Passport for Work è ora noto come **Windows Hello per le aziende**.
* Enterprise Data Protection è ora noto come **Windows Information Protection**.

### <a name="deployment-of-windows-hello-for-business-passport-for-work"></a>Distribuzione di Windows Hello per le aziende (Passport for Work)

È ora possibile distribuire i criteri di Windows Hello per le aziende su dispositivi appartenenti a un dominio Windows 10 e gestiti dal client di Configuration Manager.

La console di Configuration Manager è stata aggiornata per riflettere tali modifiche.

### <a name="ios-activation-lock"></a>Blocco attivazione di iOS
Configuration Manager consente di gestire il blocco attivazione iOS, una funzionalità dell'app Trova il mio iPhone per dispositivi iOS 7.1 e versioni successive. Quando il blocco attivazione iOS è abilitato, richiede l'immissione di un ID Apple e una password dell'utente prima che sia possibile:
* Disattivare Trova il mio iPhone.
* Cancellare il dispositivo.
* Riattivare il dispositivo.

Configuration Manager consente di gestire il blocco attivazione in due modi:

- Abilitando il blocco attivazione nei dispositivi con supervisione.
- Effettuando il bypass del blocco attivazione nei dispositivi con supervisione.


### <a name="microsoft-defender-advanced-threat-protection"></a>Microsoft Defender Advanced Threat Protection

Endpoint Protection facilita la gestione e il monitoraggio di Microsoft Defender Advanced Threat Protection (ATP). Microsoft Defender ATP è un nuovo servizio che consente alle aziende di rilevare, analizzare e rispondere agli attacchi avanzati sulle reti. I criteri di Configuration Manager possono essere utili per l'onboarding e il monitoraggio dei computer gestiti che eseguono Windows 10, versione 1607 (build 14328) o versione successiva.

Per informazioni dettagliate, vedere [Microsoft Defender Advanced Threat Protection](../../../protect/deploy-use/windows-defender-advanced-threat-protection.md).

### <a name="device-categories"></a>Categorie di dispositivi
È possibile creare categorie di dispositivi da usare per inserire automaticamente i dispositivi nelle raccolte di dispositivi quando si usa Configuration Manager con Microsoft Intune. Agli utenti verrà quindi richiesto di scegliere una categoria di dispositivi quando eseguono la registrazione di un dispositivo in Intune. È anche possibile modificare la categoria di un dispositivo dalla console di Configuration Manager.

Per informazioni dettagliate, vedere [Come classificare automaticamente i dispositivi in raccolte con Configuration Manager](../../../core/clients/manage/collections/automatically-categorize-devices-into-collections.md).

### <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>Predichiarare i dispositivi con i numeri di serie IMEI o iOS

È possibile identificare i dispositivi di proprietà dell'azienda importando i relativi codici IMEI (International station Mobile Equipment Identity) o i numeri di serie iOS. È possibile caricare un file con valori delimitati da virgole (CSV) contenente i codici IMEI o immettere manualmente le informazioni relative ai dispositivi. Le informazioni importate impostano la proprietà dei dispositivi registrati come "Corporate" negli elenchi di dispositivi. È tuttavia necessaria una licenza di Intune per ogni utente che accede al servizio.

### <a name="on-premises-health-attestation-service-communication"></a>Comunicazione del servizio di attestazione dell'integrità locale

È ora possibile abilitare il monitoraggio dei servizi di Attestazione dell'integrità per i PC Windows 10 usando solo l'infrastruttura locale, in modo che i computer senza accesso a Internet possano creare report di attestazione dell'integrità dei dispositivi.

Per informazioni dettagliate, vedere [Attestazione dell'integrità per Configuration Manager](../../../core/servers/manage/health-attestation.md#how-to-enable-health-attestation-service-communication-on-configuration-manager-client-computers).  

## <a name="remote-control"></a>Controllo remoto
Offre agli utenti la possibilità di accettare o rifiutare il trasferimento di file prima di trasferire il contenuto dagli Appunti condivisi in una sessione di controllo remoto. Gli utenti devono solo concedere l'autorizzazione una sola volta per sessione e il visualizzatore non ha la possibilità di concedere l'autorizzazione per procedere con il trasferimento dei file. È possibile trovare questa nuova impostazione nell'area di lavoro **Amministrazione**. Passare a **Impostazioni client** e quindi aprire il pannello **Strumenti remoti** in **Impostazioni predefinite**.
