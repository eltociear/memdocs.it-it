---
title: Novità della versione 1910
titleSuffix: Configuration Manager
description: Informazioni dettagliate sulle modifiche e sulle nuove funzionalità introdotte nella versione 1910 di Configuration Manager Current Branch.
ms.date: 01/22/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3e1ddb65-1193-46ce-a7c0-a48dfd9fd833
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 86ee63564654d41b965cfc411eede273eeca4ef4
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/09/2020
ms.locfileid: "89607726"
---
# <a name="whats-new-in-version-1910-of-configuration-manager-current-branch"></a>Novità della versione 1910 di Configuration Manager Current Branch

*Si applica a: Configuration Manager (Current Branch)*

L'aggiornamento 1910 per Configuration Manager Current Branch è disponibile come aggiornamento nella console. Applicare questo aggiornamento ai siti con la versione 1806 o successiva. <!-- baseline only statement:When installing a new site, it's also available as a baseline version.--> Questo articolo offre un riepilogo delle modifiche e delle nuove funzionalità di Configuration Manager versione 1910.

Esaminare sempre l'elenco di controllo più recente per installare questo aggiornamento. Per altre informazioni, vedere [Elenco di controllo per l'installazione dell'aggiornamento 1910](../../servers/manage/checklist-for-installing-update-1910.md). Dopo aver aggiornato un sito, vedere anche [Elenco di controllo post-aggiornamento](../../servers/manage/checklist-for-installing-update-1910.md#post-update-checklist).

Per sfruttare i vantaggi delle nuove funzionalità di Configuration Manager, dopo l'aggiornamento del sito aggiornare anche i client alla versione più recente. Anche se le nuove funzionalità vengono visualizzate nella console di Configuration Manager quando si esegue l'aggiornamento del sito e della console, lo scenario completo risulta funzionante solo dopo l'aggiornamento alla versione più recente del client.

> [!TIP]
> Per ricevere una notifica quando questa pagina viene aggiornata, copiare e incollare l'URL seguente nel lettore di feed RSS: `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1910+-+Configuration+Manager%22&locale=en-us`

## <a name="microsoft-endpoint-configuration-manager"></a><a name="bkmk_mem"></a> Microsoft Endpoint Configuration Manager

<!--4960084-->

Configuration Manager è ora incluso in Microsoft Endpoint Manager.

![Microsoft Endpoint Configuration Manager](media/4960084-endpoint-manager-logo.png)

Microsoft Endpoint Manager è una soluzione integrata per la gestione di tutti i dispositivi. Microsoft riunisce Configuration Manager e Intune con una gestione delle licenze semplificata. È possibile continuare a sfruttare l'investimento esistente in Configuration Manager avvalendosi anche di alcuni vantaggi offerti dalla potenza del cloud Microsoft in base alle esigenze.

Le soluzioni di gestione Microsoft seguenti fanno ora parte del marchio Microsoft Endpoint Manager:

- [Configuration Manager](/configmgr)
- [Intune](/intune)
- [Desktop Analytics](../../../desktop-analytics/overview.md)
- [Autopilot](/intune/enrollment/enrollment-autopilot)
- Altre funzionalità della [console di amministrazione della gestione dei dispositivi](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/microsoft-intune-rolls-out-an-improved-streamlined-endpoint/ba-p/937760)

Per altre informazioni, vedere i post seguenti di Brad Anderson, vicepresidente di Microsoft, per Microsoft 365:

- [Post di blog sull'annuncio](https://aka.ms/cmannounce)
- [Documento sulla visione](https://aka.ms/MEMVisionPaper)
- [Video di riepilogo dell'annuncio](https://youtu.be/GS7oNPInFuw)

### <a name="what-things-change-in-configuration-manager-with-microsoft-endpoint-manager"></a>Che cosa cambia in Configuration Manager con l'introduzione di Microsoft Endpoint Manager?

Nella versione 1910, a parte il nuovo nome, Configuration Manager funziona allo stesso modo. Alcune modifiche apportate ai nomi possono avere effetto sull'uso dei componenti seguenti:

- **Console di Configuration Manager**: trovare i collegamenti alla console e al **visualizzatore controllo remoto** nel menu Start di Windows nella cartella **Microsoft Endpoint Manager**.

- **Software Center**: trovare il collegamento a Software Center nel menu Start di Windows nella cartella **Microsoft Endpoint Manager**.

![Icone del menu Start di Microsoft Endpoint Manager](media/microsoft-endpoint-manager-start-menu.png)

Assicurarsi di aggiornare la documentazione gestita internamente in modo da includere questi nuovi percorsi.

> [!TIP]
> Quando si apre il menu Start in Windows 10, è sufficiente iniziare a digitare il nome per trovare l'icona. Ad esempio, immettere `Configuration Manager` o `Software Center`.

## <a name="site-infrastructure"></a><a name="bkmk_infra"></a> Infrastruttura del sito

### <a name="reclaim-sedo-lock"></a>Richiamare il blocco SEDO

<!--4786915-->

A partire da [Current Branch versione 1906](whats-new-in-version-1906.md#reclaim-sedo-lock-for-task-sequences), è possibile cancellare il blocco su una sequenza di attività. È possibile cancellare il blocco su qualsiasi oggetto nella console di Configuration Manager.

Per altre informazioni, vedere [Uso della console di Configuration Manager](../../servers/manage/admin-console.md#bkmk_sedo).

### <a name="extend-and-migrate-on-premises-site-to-microsoft-azure"></a>Estendere ed eseguire la migrazione di un sito locale in Microsoft Azure
<!--3556022-->

Questo nuovo strumento consente di creare a livello di codice macchine virtuali di Azure per Configuration Manager. Consente di installare con impostazioni predefinite ruoli del sito come un server del sito passivo, punti di gestione e punti di distribuzione. Dopo aver convalidato i nuovi ruoli, è possibile usarli come sistemi del sito aggiuntivi per la disponibilità elevata. È anche possibile rimuovere il ruolo del sistema del sito locale e mantenere solo il ruolo VM di Azure.

Per altre informazioni, vedere [Estendere ed eseguire la migrazione di un sito locale in Microsoft Azure](../../support/azure-migration-tool.md).

<!-- ## <a name="bkmk_cloud"></a> Cloud-attached management -->

## <a name="desktop-analytics"></a><a name="bkmk_da"></a> Desktop Analytics

Per altre informazioni sulle modifiche mensili al servizio cloud Desktop Analytics, vedere [Novità di Desktop Analytics](../../../desktop-analytics/whats-new.md).

## <a name="real-time-management"></a><a name="bkmk_real"></a> Gestione in tempo reale

### <a name="optimizations-to-the-cmpivot-engine"></a>Ottimizzazioni per il motore CMPivot
<!--3197353-->
Sono state aggiunte alcune ottimizzazioni significative al motore CMPivot. È ora possibile spostare più operazioni di elaborazione nel client ConfigMgr. Le ottimizzazioni riducono drasticamente il carico della CPU del server e della rete necessario per eseguire le query CMPivot. Grazie a queste ottimizzazioni, è ora possibile analizzare diversi gigabyte di dati del client in tempo reale. 

Per altre informazioni, vedere [Ottimizzazioni per il motore CMPivot](../../servers/manage/cmpivot-changes.md#bkmk_optimization).

### <a name="additional-cmpivot-entities-and-enhancements"></a>Entità CMPivot aggiuntive e miglioramenti
<!--5410930-->
È stata aggiunta una serie di nuove entità CMPivot e sono stati introdotti miglioramenti alle entità per facilitare l'individuazione e la risoluzione dei problemi. Per eseguire una query sono state incluse le entità seguenti:

- Registri eventi di Windows ([WinEvent](../../servers/manage/cmpivot-changes.md#bkmk_WinEvent))
- Contenuto del file ([FileContent](../../servers/manage/cmpivot-changes.md#bkmk_File))
- DLL caricate dai processi ([ProcessModule](../../servers/manage/cmpivot-changes.md#bkmk_ProcessModule))
- Informazioni Azure Active Directory ([AADStatus](../../servers/manage/cmpivot-changes.md#bkmk_AadStatus))
- Stato di Endpoint Protection ([EPStatus](../../servers/manage/cmpivot-changes.md#bkmk_EPStatus))

Questa versione include anche diversi [altri miglioramenti](../../servers/manage/cmpivot-changes.md#bkmk_Other) a CMPivot. Per altre informazioni, vedere l'articolo su [CMPivot a partire dalla versione 1910](../../servers/manage/cmpivot-changes.md#bkmk_cmpivot1910).

## <a name="content-management"></a><a name="bkmk_content"></a> Gestione dei contenuti

### <a name="microsoft-connected-cache-support-for-intune-win32-apps"></a>Supporto di Microsoft Connected Cache per le app Win32 di Intune

<!--5032900-->

Quando si abilita Microsoft Connected Cache nei punti di distribuzione di Configuration Manager, questi possono ora essere usati per gestire le app Win32 di Microsoft Intune nei client co-gestiti.

Per altre informazioni, vedere [Microsoft Connected Cache in Configuration Manager](../hierarchy/microsoft-connected-cache.md#bkmk_intune).

> [!NOTE]
> La versione Current Branch di Configuration Manager 1906 include la [cache in rete di Ottimizzazione recapito](../hierarchy/microsoft-connected-cache.md), un'applicazione installata in Windows Server ancora in fase di sviluppo. A partire dalla versione Current Branch 1910, questa funzionalità è nota come Microsoft Connected Cache.
>
> Quando si installa Connected Cache in un punto di distribuzione di Configuration Manager, il traffico del servizio Ottimizzazione recapito viene scaricato nelle origini locali. Connected Cache esegue questa operazione memorizzando il contenuto nella cache in modo efficiente a livello di intervallo di byte.

## <a name="client-management"></a><a name="bkmk_client"></a> Gestione dei client

### <a name="include-custom-configuration-baselines-as-part-of-compliance-policy-assessment"></a>Includere linee di base di configurazione personalizzate come parte della valutazione dei criteri di conformità
<!--3608345-->

È ora possibile aggiungere la valutazione delle linee di base di configurazione personalizzate come regola di valutazione dei criteri di conformità. Quando si crea o si modifica una linea di base di configurazione, è possibile usare l'opzione **Valuta questa baseline come parte della valutazione dei criteri di conformità**. Quando si aggiunge o si modifica una regola dei criteri di conformità, è disponibile una nuova condizione denominata **Includi le baseline configurate in una valutazione dei criteri di conformità**.

Per i dispositivi con co-gestione, e quando si configura Intune per acquisire i risultati della valutazione della conformità di Configuration Manager come parte dello stato di conformità generale, queste informazioni vengono inviate ad Azure Active Directory. È quindi possibile usarle per l'accesso condizionale alle risorse di Microsoft 365.

Per altre informazioni, vedere [Includere linee di base di configurazione personalizzate come parte della valutazione dei criteri di conformità](../../../compliance/deploy-use/create-configuration-baselines.md#bkmk_CAbaselines).

### <a name="enable-user-policy-for-windows-10-enterprise-multi-session"></a>Abilitare i criteri utente per Windows 10 Enterprise multisessione

<!--4737447-->

Configuration Manager Current Branch versione 1906 ha introdotto il supporto per [Desktop virtuale Windows](../configs/supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop). Questo ambiente di Microsoft Azure supporta diverse versioni del sistema operativo, alcune delle quali consentono più sessioni utente attive simultanee. Ad esempio, Windows 10 Enterprise multisessione è una di queste versioni del sistema operativo.

Se in questi dispositivi multisessione è necessario usare criteri utente e si accettano le potenziali conseguenze sulle prestazioni, è ora possibile configurare un'impostazione client per abilitare i criteri utente. Nel gruppo **Criteri client** configurare l'impostazione **Abilita i criteri utente per più sessioni utente**.

Per altre informazioni, vedere [Come configurare le impostazioni client](../../clients/deploy/configure-client-settings.md).


<!-- ## <a name="bkmk_comgmt"></a> Co-management -->


## <a name="application-management"></a><a name="bkmk_app"></a> Gestione delle applicazioni

### <a name="deploy-microsoft-edge-version-77-and-later"></a>Distribuire Microsoft Edge versione 77 e successive
<!--4561024-->
Il nuovo Microsoft Edge è disponibile per le aziende. È ora possibile distribuire Microsoft Edge versione 77 e successive nei sistemi degli utenti. Gli amministratori possono scegliere tra il canale Beta, Dev e stabile, insieme a una versione del client Microsoft Edge da distribuire.

Per altre informazioni, vedere [Distribuire Microsoft Edge versione 77 e successive](../../../apps/deploy-use/deploy-edge.md).

### <a name="improvements-to-application-groups"></a>Miglioramenti ai gruppi di applicazioni

<!--4760058-->

A partire da Current Branch versione 1906, è possibile creare un gruppo di applicazioni da inviare a una raccolta di dispositivi come singola distribuzione. Questa versione introduce un miglioramento a questa funzionalità:

- Gli utenti possono selezionare **Disinstalla** per il gruppo di app in Software Center.
- È possibile distribuire un gruppo di app in una **raccolta utenti**.

Per altre informazioni di carattere generale, vedere [Creare gruppi di applicazioni](../../../apps/deploy-use/create-app-groups.md).


## <a name="os-deployment"></a><a name="bkmk_osd"></a> Distribuzione del sistema operativo

### <a name="improvements-to-the-task-sequence-editor"></a>Miglioramenti all'editor delle sequenze di attività

 L'editor delle sequenze di attività include i miglioramenti seguenti:

- **Ricerca nell'editor delle sequenze di attività:**<!--4621085--> Se si ha una sequenza di attività di grandi dimensioni con molti gruppi e passaggi, può essere difficile individuare passaggi specifici. È ora possibile eseguire ricerche nell'editor delle sequenze di attività. Questa azione consente di individuare più rapidamente i passaggi in una sequenza di attività.
- **Possibilità di copiare e incollare le condizioni della sequenza di attività:**<!--4621098--> Se si vogliono riutilizzare le condizioni da un passaggio della sequenza di attività a un altro, è ora possibile copiare e incollare le condizioni nell'editor.

Per altre informazioni, vedere il nuovo articolo su come [usare l'editor delle sequenze di attività](../../../osd/understand/task-sequence-editor.md).

### <a name="task-sequence-performance-improvements-power-plans"></a>Miglioramenti per le prestazioni delle sequenze di attività: Combinazioni per il risparmio di energia

<!--3555926-->

È ora possibile eseguire una sequenza di attività con la combinazione per il risparmio di energia per prestazioni elevate. Questa opzione migliora la velocità complessiva della sequenza di attività. Configura Windows in modo da usare la combinazione per il risparmio di energia per prestazioni elevate predefinita, che offre prestazioni massime a scapito di un consumo di energia superiore.

Per altre informazioni, vedere [Miglioramenti delle prestazioni per le combinazioni per il risparmio di energia](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#bkmk_perf).

### <a name="task-sequence-download-on-demand-over-the-internet"></a>Download della sequenza di attività su richiesta tramite Internet

<!--3601238-->

È ora possibile usare la sequenza di attività per distribuire un aggiornamento sul posto di Windows 10 tramite Cloud Management Gateway. Prima di avviare la sequenza di attività, tuttavia, è necessario che la distribuzione scarichi tutto il contenuto in locale.

A partire da questa versione, il motore della sequenza di attività può scaricare pacchetti su richiesta da un servizio CMG abilitato per il contenuto o da un punto di distribuzione cloud. Questa modifica offre ulteriore flessibilità con le distribuzioni di aggiornamento sul posto di Windows 10 ai dispositivi basati su Internet.

Per altre informazioni, vedere [Distribuire l'aggiornamento sul posto di Windows 10 mediante Cloud Management Gateway](../../../osd/deploy-use/deploy-a-task-sequence.md#deploy-windows-10-in-place-upgrade-via-cmg).

### <a name="improvements-to-os-deployment"></a>Miglioramenti della distribuzione del sistema operativo

Questa versione include i miglioramenti seguenti per la distribuzione del sistema operativo.

#### <a name="boot-image-keyboard-layout"></a>Layout della tastiera per l'immagine d'avvio

<!--4910348-->

Configurare il layout predefinito della tastiera per un'immagine d'avvio. Nella scheda **Personalizzazione** di un'immagine di avvio usare la nuova opzione per **Imposta il layout di tastiera predefinito in WinPE**. Se si seleziona una lingua diversa da en-US, Configuration Manager include ancora en-US nelle impostazioni locali di input disponibili. Nel dispositivo, il layout iniziale della tastiera corrisponde alle impostazioni locali selezionate, ma l'utente può passare a en-US se necessario.

Per altre informazioni, vedere [Manage boot images](../../../osd/get-started/manage-boot-images.md#customization) (Gestire le immagini d'avvio).

#### <a name="import-a-single-index-of-an-os-upgrade-package"></a>Importare un singolo indice di un pacchetto di aggiornamento del sistema operativo

<!--4931110-->

Quando si importa un pacchetto di aggiornamento del sistema operativo, è possibile usare l'opzione **Estrai un indice delle immagini specifico dal file install.wim del pacchetto di aggiornamento selezionato**. Questo comportamento è simile a quello delle [immagini del sistema operativo](../../../osd/get-started/manage-operating-system-images.md#BKMK_AddOSImages), con la differenza che sovrascrive il file install.wim esistente nel pacchetto di aggiornamento del sistema operativo. Estrae l'indice dell'immagine in una posizione temporanea e quindi lo sposta nella directory di origine originale.

Per altre informazioni, vedere [Gestire i pacchetti di aggiornamento del sistema operativo](../../../osd/get-started/manage-operating-system-upgrade-packages.md#BKMK_AddOSUpgradePkgs).

#### <a name="output-the-results-of-a-run-command-line-step-to-a-variable-during-a-task-sequence"></a>Output dei risultati di un passaggio Esegui riga di comando in una variabile durante una sequenza di attività

<!--user story 4977616/bug 4798352-->

Il passaggio **Esegui riga di comando** include ora l'opzione **Output nella variabile della sequenza di attività**. Quando si abilita questa opzione, la sequenza di attività salva l'output del comando in una variabile della sequenza di attività personalizzata specificata.

Per altre informazioni, vedere [Esegui riga di comando](../../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine).

#### <a name="improvements-to-task-sequence-debugger"></a>Miglioramenti al debugger delle sequenze di attività

Questa versione include i miglioramenti seguenti al debugger delle sequenze di attività:

- Usare la nuova variabile della sequenza di attività **TSDebugOnError** per avviare automaticamente il debugger quando la sequenza di attività restituisce un errore.<!-- 5012536 -->
- Se si crea un punto di interruzione nel debugger e quindi la sequenza di attività riavvia il computer, il debugger mantiene i punti di interruzione dopo il riavvio.<!-- 5012509 -->

Per altre informazioni, vedere [Debugger delle sequenze di attività](../../../osd/deploy-use/debug-task-sequence.md) e [Variabili della sequenza di attività - TSDebugOnError](../../../osd/understand/task-sequence-variables.md#TSDebugOnError).

#### <a name="improved-language-support-in-task-sequence"></a>Supporto delle lingue migliorato nella sequenza di attività

<!--5411057, 5138936-->

Questa versione consente un controllo maggiore della configurazione della lingua durante la distribuzione del sistema operativo. Se si stanno già applicando queste impostazioni della lingua, la modifica consente di semplificare la sequenza di attività di distribuzione del sistema operativo. Invece di usare più passaggi per lingua o script distinti, usare un'istanza per ogni lingua del passaggio **Applica impostazioni Windows** predefinito con una condizione per tale lingua.

Usare il passaggio **Applica impostazioni Windows** della sequenza di attività per configurare le nuove impostazioni seguenti:

- Impostazioni locali per l'input (layout di tastiera predefinito)
- Impostazioni locali di sistema
- Lingua dell'interfaccia utente
- Fallback della lingua dell'interfaccia utente
- Impostazioni locali dell'utente

Per altre informazioni, vedere [Applicare le impostazioni Windows](../../../osd/understand/task-sequence-steps.md#BKMK_ApplyWindowsSettings).

#### <a name="new-variable-for-windows-10-in-place-upgrade"></a>Nuova variabile per l'aggiornamento sul posto di Windows 10

<!--4680263-->

Per risolvere i problemi di temporizzazione con la sequenza di attività di aggiornamento sul posto di Windows 10 nei dispositivi con prestazioni elevate al termine dell'installazione di Windows, è ora possibile impostare la nuova variabile della sequenza di attività **SetupCompletePause**. Quando si assegna un valore in secondi a questa variabile, il processo di installazione di Windows ritarda questo intervallo di tempo prima di avviare la sequenza di attività. Questo timeout fornisce al client di Configuration Manager altro tempo per l'inizializzazione.

Per altre informazioni, vedere [Variabili della sequenza di attività - SetupCompletePause](../../../osd/understand/task-sequence-variables.md#SetupCompletePause).

<!-- ## <a name="bkmk_userxp"></a> Software Center -->

## <a name="software-updates"></a><a name="bkmk_sum"></a> Aggiornamenti software

### <a name="additional-options-for-third-party-update-catalogs"></a>Opzioni aggiuntive per i cataloghi di aggiornamenti di terze parti
<!--4469002-->
Sono ora disponibili controlli più granulari sulla sincronizzazione dei cataloghi di aggiornamenti di terze parti. A partire da Configuration Manager versione 1910, è possibile configurare la pianificazione della sincronizzazione per ogni catalogo in modo indipendente. Quando si usano cataloghi che includono aggiornamenti suddivisi per categorie, è possibile configurare la sincronizzazione in modo da includere solo determinate categorie di aggiornamenti per evitare di sincronizzare l'intero catalogo. Con i cataloghi suddivisi per categorie, quando si è certi di distribuire una categoria, è possibile configurarla per il download e la pubblicazione automatici in Windows Server Update Services (WSUS).

Per altre informazioni, vedere [Abilitare gli aggiornamenti di terze parti](../../../sum/deploy-use/third-party-software-updates.md#bkmk_1910).

### <a name="use-delivery-optimization-for-all-windows-updates"></a>Usare Ottimizzazione recapito per tutti gli aggiornamenti di Windows
<!--4699118-->
Nelle versioni precedenti la funzionalità Ottimizzazione recapito è disponibile solo per gli aggiornamenti rapidi. Con Configuration Manager versione 1910 è ora possibile usare Ottimizzazione recapito per la distribuzione di tutti i contenuti di Windows Update per i client che eseguono Windows 10 versione 1709 o successiva.

Per altre informazioni, vedere:
- [Ottimizzare il recapito degli aggiornamenti di Windows 10](../../../sum/deploy-use/optimize-windows-10-update-delivery.md#bkmk_DO-1910)
- [Impostazioni client per gli aggiornamenti software](../../clients/deploy/about-client-settings.md#software-updates)
- [Impostazioni client per Ottimizzazione recapito](../../clients/deploy/about-client-settings.md#delivery-optimization)

### <a name="additional-software-update-filter-for-adrs"></a>Filtro di aggiornamento software aggiuntivo per le regole di distribuzione automatica
<!--4852033-->
È ora possibile usare **Distribuito** come filtro di aggiornamento per le regole di distribuzione automatica. Questo filtro permette di identificare i nuovi aggiornamenti che può essere necessario distribuire nelle raccolte pilota o di test.

Per altre informazioni, vedere [Distribuire automaticamente gli aggiornamenti software](../../../sum/deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process).

## <a name="office-management"></a><a name="bkmk_o365"></a> Gestione di Office


### <a name="office-365-proplus-pilot-and-health-dashboard"></a>Dashboard sull'integrità e la distribuzione pilota di Office 365 ProPlus
<!--4488272, 4488301-->

Il dashboard per l'integrità e la distribuzione pilota di Office 365 ProPlus permette di pianificare e distribuire Office 365 ProPlus o di eseguirne una distribuzione pilota. Il dashboard fornisce informazioni dettagliate sull'integrità per i dispositivi con Office 365 ProPlus per identificare i possibili problemi che possono influire sui piani di distribuzione. Il dashboard per l'integrità e la distribuzione pilota di Office 365 ProPlus fornisce indicazioni per i dispositivi pilota in base all'inventario dei componenti aggiuntivi.

Per altre informazioni, vedere [Uso del dashboard sull'integrità e la distribuzione pilota di Office 365 ProPlus](../../../sum/deploy-use/office-365-dashboard.md#bkmk_pilot).

## <a name="protection"></a><a name="bkmk_protect"></a> Protezione

### <a name="bitlocker-management"></a>Gestione di BitLocker

<!--3601034-->

Configuration Manager offre ora le funzionalità di gestione seguenti per Crittografia unità BitLocker:

- Distribuzione del client BitLocker in dispositivi Windows gestiti.
- Gestione dei criteri di crittografia del dispositivo.
- Generazione di report di conformità.
- Uso di un sito Web di amministrazione e monitoraggio per il recupero chiave.
- Accesso a un portale self-service degli utenti.

Per altre informazioni, vedere [Pianificare la gestione di BitLocker](../../../protect/plan-design/bitlocker-management.md).

## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a> Console di Configuration Manager

### <a name="view-active-consoles-and-message-administrators-through-console-connections"></a>Visualizzare le console attive e inviare un messaggio agli amministratori tramite Connessioni di console
<!--4923997-->
Sono stati apportati i miglioramenti seguenti per **Connessioni di console**:

- Possibilità di inviare messaggi ad altri amministratori di Configuration Manager tramite Microsoft Teams.
- La colonna **Last Console Heartbeat** (Ultimo heartbeat colonna) ha sostituito la colonna **Ora dell'ultima connessione**.
  - Una console aperta in primo piano invia un heartbeat ogni 10 minuti per aiutare a determinare quali connessioni della console sono attualmente attive.

Per altre informazioni, vedere [Visualizzare le console connesse di recente](../../servers/manage/admin-console.md#bkmk_viewconnected) e [Inviare messaggi agli amministratori](../../servers/manage/admin-console.md#bkmk_message).

### <a name="client-diagnostics-actions"></a>Azioni di diagnostica client

<!--4433455-->

Sono disponibili nuove azioni del dispositivo per **Diagnostica client** nella console di Configuration Manager:

- **Abilita la registrazione dettagliata:** modifica il livello di registrazione per il componente CCM da globale a *dettagliata* e abilita la registrazione debug.
- **Disabilita la registrazione dettagliata:** modifica il livello di registrazione da globale a *predefinita* e disabilita la registrazione debug.

Per altre informazioni, vedere [Diagnostica client](../../clients/manage/client-notification.md#client-diagnostics).

### <a name="improvements-to-console-search"></a>Miglioramenti alla ricerca nella console
<!--4640570-->

Questa versione include i miglioramenti seguenti alla funzionalità di ricerca nella console di Configuration Manager:

- È ora possibile usare l'opzione di ricerca **Tutte le sottocartelle** dai nodi **Pacchetti driver** e **Query**.<!--2841181,5424892-->
- Quando una ricerca restituisce più di 1.000 risultati, è possibile selezionare il pulsante **OK** sulla barra di notifica per visualizzare altri risultati.<!--4640570-->

## <a name="other-updates"></a>Altri aggiornamenti

Per altre informazioni sulle modifiche apportate ai cmdlet di Windows PowerShell per Configuration Manager, vedere le [note sulla versione 1910 di PowerShell](/powershell/sccm/1910-release-notes).

Per altre informazioni sulle modifiche all'API REST del servizio di amministrazione, vedere le [note sulla versione del servizio di amministrazione](../../../develop/adminservice/release-notes.md#bkmk_1910).

A parte le nuove funzionalità, questa versione include anche ulteriori modifiche, ad esempio correzioni di bug. Per altre informazioni, vedere [Riepilogo delle modifiche in Configuration Manager Current Branch, versione 1910](https://support.microsoft.com/help/4535776).

<!--
As of this version, the following features are no longer pre-release:
- [SMS Provider administration service](../hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service)
- [Device Guard management](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md)
-->
L'aggiornamento cumulativo seguente (4537079) è disponibile nella console a partire dal 18 febbraio 2020: [Aggiornamento cumulativo per Microsoft Endpoint Configuration Manager Current Branch, versione 1910](https://support.microsoft.com/help/4537079).



<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4552181](https://support.microsoft.com/help/4552181) | Content distribution stalls in Configuration Manager current branch, version 1910 | 16 March 2020 | No |
| [4552430](https://support.microsoft.com/help/4552430) | Third-party update category synchronization resets to default in Configuration Manager | 18 March 2020 | No |

> [!NOTE]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](../../servers/manage/updates.md#bkmk_supersede).
-->

## <a name="next-steps"></a>Passaggi successivi

<!-- At this time, version 1910 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-1910.md#early-update-ring). -->
A partire dal 20 dicembre 2019, la versione 1910 è disponibile a livello globale per l'installazione per tutti i clienti.

Al momento di installare questa versione, vedere [Installazione degli aggiornamenti per Configuration Manager](../../servers/manage/updates.md) ed [Elenco di controllo per l'installazione dell'aggiornamento 1910](../../servers/manage/checklist-for-installing-update-1910.md).

> [!TIP]
> Per installare un nuovo sito, usare una versione base di Configuration Manager.
>
> Sono disponibili altre informazioni su:
>
> - [Installing new sites](../../servers/deploy/install/installing-sites.md) (Installare nuovi siti) 
> - [Baseline and update versions](../../servers/manage/updates.md#bkmk_Baselines) (Versioni di base e di aggiornamento) 

Per problemi noti e importanti, vedere [Note sulla versione](../../servers/deploy/install/release-notes.md).

Dopo aver aggiornato un sito, vedere anche [Elenco di controllo post-aggiornamento](../../servers/manage/checklist-for-installing-update-1910.md#post-update-checklist).