---
title: Introduzione alla gestione delle app
titleSuffix: Configuration Manager
description: È possibile individuare le informazioni di base necessarie per gestire e distribuire applicazioni in Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 08f711ba-83bf-4b5f-9520-a0778c6ae7eb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d3cd21fe4b1d53ecbb0bc60818405cb795a4f289
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690219"
---
# <a name="introduction-to-application-management-in-configuration-manager"></a>Introduzione alla gestione delle applicazioni in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

In questo argomento verranno fornite le informazioni di base necessarie prima di iniziare a usare le applicazioni di Configuration Manager.  

> [!TIP]  
> Se si ha già familiarità con la modalità di gestione delle applicazioni in Configuration Manager, ignorare questo articolo. Passare alla creazione di un'applicazione di esempio: [Creare e distribuire un'applicazione](../get-started/create-and-deploy-an-application.md).  

## <a name="what-is-an-application"></a>Che cos'è un'applicazione?

Anche se *applicazione* o *app* è un termine ampiamente usato in informatica, in Configuration Manager indica un concetto specifico. Pensare a un'applicazione come a una scatola. Questa scatola contiene uno o più set di file di installazione per un pacchetto software (chiamato *tipo di distribuzione*) e le istruzioni su come distribuire il software.  

Quando si distribuisce l'applicazione nei dispositivi, i **requisiti** stabiliscono quale tipo di distribuzione viene installato nel dispositivo da Configuration Manager.  

È possibile eseguire molte altre operazioni con un'applicazione. Altre informazioni su queste operazioni sono disponibili in questa guida. Le sezioni seguenti introducono alcuni concetti che è necessario conoscere prima di avviare un'analisi più approfondita:  

### <a name="deployment-type"></a>Tipo di distribuzione

Se l'*applicazione* è la scatola, il *tipo di distribuzione* corrisponde ai contenuti della scatola. Un'applicazione necessita di almeno un tipo di distribuzione, perché consente di determinare la modalità di installazione dell'app. Usare uno o più tipi di distribuzione per configurare contenuti e programmi di installazione diversi per la stessa applicazione.

Ad esempio, una società ha un'applicazione line-of-business denominata Astoria. Gli sviluppatori dell'applicazione forniscono le modalità seguenti per l'installazione dell'app:

- Pacchetto di Windows Installer per offrire funzionalità complete nei dispositivi Windows 10
- Pacchetto App-V da usare nella server farm
- App Web per utenti mobili  

È possibile creare una singola applicazione per Astoria in Configuration Manager. L'applicazione definisce i metadati generali relativi all'app che risultano comuni in tutti i metodi di installazione e in tutte le piattaforme. È quindi possibile creare tre tipi di distribuzione per i metodi di installazione disponibili e distribuire l'applicazione a tutti gli utenti. In base ai requisiti e ad altre configurazioni nei tipi di distribuzione, Configuration Manager determina il metodo corretto in ogni caso d'uso.

Per altre informazioni, vedere [Creare tipi di distribuzione per l'applicazione](../deploy-use/create-applications.md#bkmk_create-dt).

### <a name="requirements"></a>Requisiti

Nelle versioni precedenti di Configuration Manager è necessario creare una raccolta di dispositivi in cui distribuire un'applicazione. Anche se è comunque possibile creare una raccolta, usare i *requisiti* per specificare criteri più dettagliati per la distribuzione di un'applicazione.

Ad esempio, è possibile indicare che un'applicazione può essere installata soltanto nei dispositivi che eseguono Windows 10. Quando si distribuisce l'applicazione in tutti i dispositivi, verrà installata solo nei dispositivi che eseguono Windows 10.

Configuration Manager valuta i requisiti per determinare se un'applicazione o uno dei tipi di distribuzione correlati verranno installati. Quindi, determina il tipo di distribuzione corretto usato per installare un'applicazione. Ogni sette giorni, per impostazione predefinita, il client di Configuration Manager ripete la valutazione delle regole dei requisiti per verificare la conformità in base all'impostazione **Pianificare nuova valutazione per le distribuzioni** del client.

Per altre informazioni, vedere [Creare e distribuire un'applicazione](../get-started/create-and-deploy-an-application.md) e [Requisiti per il tipo di distribuzione](../deploy-use/create-applications.md#bkmk_dt-require).

### <a name="global-conditions"></a>Condizioni globali

I requisiti vengono usati con uno specifico tipo di distribuzione in una singola applicazione, ma è anche possibile creare *condizioni globali*, ossia una raccolta di requisiti predefiniti che è possibile usare con qualsiasi applicazione e tipo di distribuzione. Configuration Manager include un set di condizioni globali predefinite ma consente anche di creare set personalizzati.

Per altre informazioni, vedere [Creare condizioni globali](../deploy-use/create-global-conditions.md).

### <a name="simulated-deployment"></a>Distribuzione simulata

Una *distribuzione simulata* valuta i requisiti, il metodo di rilevamento e le dipendenze di un'applicazione. Un client fornisce i risultati senza installare l'applicazione.

Per altre informazioni, vedere [Simulare distribuzioni di applicazioni ](../deploy-use/simulate-application-deployments.md).  

### <a name="deployment-action"></a>Azione di distribuzione

Un'*azione di distribuzione* specifica se installare o disinstallare l'applicazione che si sta distribuendo. Non tutti i tipi di distribuzione supportano l'azione di disinstallazione.

Per altre informazioni, vedere l'argomento relativo alla [distribuzione delle applicazioni](../deploy-use/deploy-applications.md).  

### <a name="deployment-purpose"></a>Scopo della distribuzione

Lo *scopo della distribuzione* specifica se l'app di distribuzione è di tipo **Richiesto** o **Disponibile**:  

- Il client installa automaticamente una distribuzione di tipo *richiesto* in base alla pianificazione configurata. Se l'applicazione non è nascosta, un utente può verificarne lo stato di distribuzione. Gli utenti possono anche usare Software Center per installare l'applicazione prima della scadenza.  

- Se si distribuisce l'applicazione a un utente come *disponibile*, l'applicazione viene visualizzata in Software Center e può essere installata su richiesta.  

Per altre informazioni, vedere l'argomento relativo alla [distribuzione delle applicazioni](../deploy-use/deploy-applications.md).  

### <a name="revisions"></a>Revisioni

Quando si eseguono *revisioni* per un'applicazione o un tipo di distribuzione, Configuration Manager crea una nuova versione dell'applicazione. Eseguire queste azioni nella console di Configuration Manager:

- Visualizzare la cronologia delle revisioni di ogni applicazione
- Visualizzare le rispettive proprietà
- Ripristinare una versione precedente di un'applicazione
- Eliminare una versione precedente

Per altre informazioni, vedere [Aggiornare e ritirare le applicazioni](../deploy-use/update-and-retire-applications.md).  

### <a name="detection-method"></a>Metodo di rilevamento

Usare i *metodi di rilevamento* per verificare se un dispositivo ha già installato un'applicazione. Se il metodo di rilevamento indica che l'applicazione è installata, Configuration Manager non prova a installarla nuovamente.

Per altre informazioni, vedere [Opzioni del metodo di rilevamento per il tipo di distribuzione](../deploy-use/create-applications.md#bkmk_dt-detect).

### <a name="dependencies"></a>Dipendenze

Le *dipendenze* definiscono uno o più tipi di distribuzione da un'altra applicazione che il client deve installare prima dell'installazione di questo tipo di distribuzione.

Per altre informazioni, vedere [Dipendenze per il tipo di distribuzione](../deploy-use/create-applications.md#bkmk_dt-depend).  

### <a name="supersedence"></a>Sostituzione

Configuration Manager consente di aggiornare o sostituire applicazioni esistenti usando una relazione di *sostituzione*. Quando si sostituisce un'applicazione, è possibile specificare un nuovo tipo di distribuzione che andrà a sostituire il tipo di distribuzione dell'applicazione sostituita. È anche possibile decidere se aggiornare o disinstallare l'applicazione sostituita prima che il client installi l'applicazione sostitutiva.

Per altre informazioni, vedere [Application revisions](../deploy-use/revise-and-supersede-applications.md#application-supersedence) (Sostituzione delle applicazioni).  

### <a name="user-centric-management"></a>Gestione incentrata sull'utente

Le applicazioni di Configuration Manager supportano la *gestione incentrata sull'utente*, che consente di associare utenti specifici a dispositivi specifici. Invece di dover ricordare il nome del dispositivo di un utente, è possibile distribuire le app all'utente e al dispositivo. Questa funzionalità consente di verificare che le app più importanti siano sempre disponibili in ogni dispositivo dell'utente. Se un utente acquisisce un nuovo computer, Configuration Manager installa automaticamente le rispettive app nel dispositivo prima dell'accesso.

Per altre informazioni, vedere [Collegare utenti e dispositivi mediante l'affinità utente dispositivo](../deploy-use/link-users-and-devices-with-user-device-affinity.md).  

### <a name="application-group"></a>Gruppo di applicazioni

A partire dalla versione 1906, creare un gruppo di applicazioni che è possibile inviare a un utente o a una raccolta di dispositivi come singola distribuzione. I metadati specificati in relazione al gruppo di app sono visualizzati in Software Center come una singola entità. È possibile ordinare le app del gruppo in modo che il client le installi in un ordine specifico.

Per altre informazioni, vedere [Creare gruppi di applicazioni](../deploy-use/create-app-groups.md).

## <a name="what-application-types-can-you-deploy"></a>Quali tipi di applicazione possono essere distribuiti?

Configuration Manager consente di distribuire i tipi di app seguenti:  

- Windows Installer (msi)  

- Pacchetto app e bundle di app Windows (appx, appxbundle, msix, msixbundle)  

- Pacchetto app Windows in Microsoft Store  

- Programma di installazione dello script per programmi di installazione di terze parti e wrapper di script

- Microsoft App-V v4 e v5  

- macOS  

- Sequenza di attività di distribuzione non del sistema operativo per app complesse

Inoltre, quando si gestiscono dispositivi tramite la [gestione di dispositivi locale](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) di Configuration Manager, è possibile gestire anche questi altri tipi di applicazione:  

- Pacchetto app per Windows Phone (xap)  

- Pacchetto app Windows Phone in Microsoft Store  

- Windows Installer tramite MDM (msi)  

- Applicazione Web

## <a name="state-based-applications"></a>Applicazioni basate sullo stato  

Le applicazioni di Configuration Manager usano il monitoraggio basato sullo stato. È possibile tenere traccia dello stato più recente della distribuzione dell'applicazione per utenti e dispositivi. I messaggi di stato visualizzano informazioni sui singoli dispositivi. Ad esempio, se si distribuisce un'applicazione a una raccolta di utenti, è possibile visualizzare lo stato di conformità e lo scopo della distribuzione nella console di Configuration Manager. È possibile monitorare la distribuzione di tutto il software dall'area di lavoro **Monitoraggio** nella console di Configuration Manager. Per altre informazioni, vedere l'argomento relativo al [monitoraggio delle applicazioni](../deploy-use/monitor-applications-from-the-console.md).  

Il client di Configuration Manager ripete regolarmente la valutazione delle distribuzioni dell'applicazione. Ad esempio:  

- Un utente disinstalla un'applicazione distribuita. Al ciclo di valutazione successivo Configuration Manager rileva che l'app non è presente. Il client reinstalla quindi automaticamente l'app.  

- Configuration Manager non ha installato un'applicazione in un dispositivo perché non rispetta i requisiti specificati. In seguito, viene apportata una modifica al dispositivo in modo che soddisfi i requisiti. Configuration Manager rileva la modifica apportata e il client installa l'applicazione.  

È possibile configurare l'intervallo di ripetizione della valutazione per le distribuzioni dell'applicazione. Usare l'impostazione **Pianificare nuova valutazione per le distribuzioni** del client disponibile nel gruppo **Distribuzione software**. Per altre informazioni, vedere [About client settings](../../core/clients/deploy/about-client-settings.md#software-deployment) (Informazioni sulle impostazioni client).  

## <a name="get-started-creating-an-application"></a>Introduzione alla creazione di un'applicazione  

Per iniziare a creare subito un'applicazione, usare la procedura dettagliata disponibile nell'articolo [Creare e distribuire un'applicazione](../get-started/create-and-deploy-an-application.md).  

Se si ha familiarità con le nozioni di base e si cercano informazioni di riferimento più dettagliate su tutte le opzioni disponibili, iniziare a [Creare applicazioni](../deploy-use/create-applications.md).  

## <a name="software-center"></a>Software Center  

Software Center è un'applicazione Windows installata con il client di Configuration Manager. Consente di eseguire le azioni seguenti:  

- Esplorare e richiedere applicazioni distribuite nel dispositivo o per l'utente
- Eseguire e pianificare le installazioni di software
- Visualizzare lo stato dell'installazione per applicazioni, aggiornamenti software e sistemi operativi
- Configurare le impostazioni per il controllo remoto
- Configurare il risparmio energia

Per altre informazioni, vedere gli articoli seguenti:  

- [Pianificare e configurare la gestione delle applicazioni](../plan-design/plan-for-and-configure-application-management.md)
- [Pianificare Software Center](../plan-design/plan-for-software-center.md)
- [Manuale dell'utente di Software Center](../../core/understand/software-center.md)

> [!Note]  
> Il supporto per i ruoli del Catalogo applicazioni termina con la versione 1910. Per altre informazioni, vedere [Rimuovere il catalogo applicazioni](../plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

## <a name="packages-and-programs"></a>Pacchetti e programmi  

Configuration Manager continua a supportare pacchetti e programmi usati nelle versioni precedenti del prodotto.

Per altre informazioni, vedere [Packages and programs](../deploy-use/packages-and-programs.md) (Pacchetti e programmi).  

## <a name="next-steps"></a>Passaggi successivi

Dopo avere compreso i concetti di base relativi alla gestione delle applicazioni in Configuration Manager, è possibile passare agli articoli seguenti:

- [Creare e distribuire un'applicazione di esempio](../get-started/create-and-deploy-an-application.md)
- [Pianificare e configurare la gestione delle applicazioni](../plan-design/plan-for-and-configure-application-management.md)
- [Creare applicazioni](../deploy-use/create-applications.md)
