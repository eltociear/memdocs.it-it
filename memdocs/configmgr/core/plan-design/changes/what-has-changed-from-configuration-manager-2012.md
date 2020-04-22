---
title: Modifiche dalla versione 2012
titleSuffix: Configuration Manager
description: Identificare le modifiche e le nuove funzionalità di Configuration Manager rispetto a System Center 2012 Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3ae68fa6-8b30-45dd-9d12-50bb67cb4a9d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 0cd49eac95d9789fd11ba2bf1ca01b68b236628d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704439"
---
# <a name="whats-changed-from-system-center-2012-configuration-manager"></a>Novità rispetto a System Center 2012 Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Configuration Manager (Current Branch) introduce importanti modifiche rispetto a System Center 2012 Configuration Manager. Questo articolo identifica le modifiche significative e le nuove funzionalità disponibili nella versione di base originale 1511 di Configuration Manager Current Branch. Per informazioni sulle modifiche introdotte negli aggiornamenti recenti per Configuration Manager, vedere [Novità delle versioni incrementali di Configuration Manager](whats-new-incremental-versions.md).

> [!NOTE]
> A partire dalla versione 1910, Configuration Manager è incluso in Microsoft Endpoint Manager. Per altre informazioni, vedere [Microsoft Endpoint Configuration Manager](whats-new-in-version-1910.md#bkmk_mem).

La versione del mese di dicembre 2015 (1511) di System Center Configuration Manager è la versione iniziale dell'attuale prodotto Configuration Manager di Microsoft. È in genere indicata con il nome Configuration Manager Current Branch. *Current Branch* indica che si tratta di una versione che supporta aggiornamenti incrementali del prodotto e che può esservi una differenza rilevante tra questa e le versioni precedenti di Configuration Manager.  

Configuration Manager Current Branch:  

- Non usa un identificatore di anno o prodotto nel nome del prodotto, a differenza delle versioni precedenti come Configuration Manager 2007 o System Center 2012 Configuration Manager.  

- Supporta gli aggiornamenti di prodotto incrementali, definiti anche versioni di aggiornamento. La versione iniziale è la 1511. Le versioni successive vengono rilasciate più volte all'anno come aggiornamenti nella console, ad esempio la versione 1910.  

- Viene installato con una versione di base. La 1511 è la versione di base originale, ma occasionalmente vengono rilasciate nuove versioni di base, come la 2002. Queste versioni possono essere usate per installare un nuovo sito e una nuova gerarchia di Configuration Manager o per eseguire l'aggiornamento da una versione supportata di System Center 2012 Configuration Manager.  

## <a name="in-console-updates"></a><a name="bkmk_updates"></a> Aggiornamenti nella console

Configuration Manager usa un metodo di manutenzione nella console denominato **Aggiornamenti e manutenzione** che semplifica l'individuazione e l'installazione degli aggiornamenti consigliati.  

Alcune versioni sono disponibili solo come aggiornamenti per i siti esistenti dall'interno della console di Configuration Manager. Non possono essere usati per installare un nuovo sito di Configuration Manager. Ad esempio, l'aggiornamento 1910 è disponibile solo dalla console di Configuration Manager. Viene usato per aggiornare un sito che esegue già una versione di Configuration Manager.

Periodicamente, una versione di aggiornamento viene rilasciata anche come nuova versione *di base*, ad esempio la 2002. Per installare un nuovo sito o una nuova gerarchia usare una versione di base. Non iniziare con una versione di base precedente come la 1802 per poi eseguire l'aggiornamento alla versione più recente. Usare sempre la versione di base più recente.

Per altre informazioni, vedere gli articoli seguenti:

- [Aggiornamenti per Configuration Manager](../../servers/manage/updates.md)
- [Baseline and update versions](../../servers/manage/updates.md#bkmk_Baselines) (Versioni di base e di aggiornamento)

## <a name="service-connection-point"></a><a name="bkmk_servicepoint"></a> Punto di connessione del servizio  

Configuration Manager Current Branch include un nuovo ruolo del sistema del sito, il **punto di connessione del servizio**:  

- Offre un punto di contatto per molte funzionalità abilitate per il cloud

- Scarica gli aggiornamenti per il sito

- Carica nel cloud Microsoft i dati di diagnostica e utilizzo relativi al sito

Questo ruolo del sistema del sito supporta sia una modalità online che una offline di funzionamento. Per altre informazioni, vedere [Informazioni sul punto di connessione del servizio](../../servers/deploy/configure/about-the-service-connection-point.md).  

## <a name="diagnostics-and-usage-data"></a><a name="bkmk_usage"></a> Dati di diagnostica e utilizzo

Configuration Manager raccoglie i dati di diagnostica e utilizzo relativi ai siti e all'infrastruttura. Queste informazioni vengono compilate e inviate al servizio cloud Microsoft dal punto di connessione del servizio. Configuration Manager richiede questi dati per scaricare gli aggiornamenti applicabili all'ambiente. Quando si configura il punto di connessione del servizio, è possibile specificare sia il livello di dati raccolti sia la modalità di invio dei dati, che può essere automatica (modalità online) o manuale (modalità offline).

Per altre informazioni, vedere [Diagnostica e dati di utilizzo](../diagnostics/diagnostics-and-usage-data.md).  

## <a name="deprecated-functionality"></a><a name="bkmk_out"></a> Funzionalità obsolete  

Alcune funzionalità, ad esempio il [supporto nativo per i computer basati sulla tecnologia Intel AMT (Active Management Technology)](#bkmk_AMT), sono state rimosse dalla console di Configuration Manager, mentre altre funzionalità, come Protezione accesso alla rete, sono state rimosse completamente. Inoltre, alcuni prodotti Microsoft precedenti come Windows Vista, Windows Server 2008 e SQL Server 2008 non sono più supportati.  

Per un elenco delle funzionalità deprecate, vedere [Elementi rimossi e deprecati](deprecated/removed-and-deprecated.md).  

Per informazioni dettagliate sui prodotti, sulle configurazioni e sui sistemi operativi supportati, vedere [Configurazioni supportate](../configs/supported-configurations.md).  

### <a name="support-for-intel-active-management-technology-amt"></a><a name="bkmk_AMT"></a> Supporto per la tecnologia Intel AMT (Active Management Technology)  

Configuration Manager Current Branch rimuove il supporto nativo per computer basati su AMT dalla console di Configuration Manager. I computer basati su AMT restano completamente gestiti quando si usa il [componente aggiuntivo Intel SCS per Microsoft Configuration Manager](https://www.intel.com/content/www/us/en/software/setup-configuration-software.html). Il componente aggiuntivo consente di accedere alle funzionalità più recenti per gestire AMT, rimuovendo le limitazioni introdotte fino al momento in cui Configuration Manager è stato in grado di integrare queste modifiche.  

La rimozione della tecnologia AMT integrata per Configuration Manager include la gestione fuori banda. Il ruolo del sistema del sito per il punto di gestione fuori banda non è più disponibile.  

> [!Note]
> Questa modifica non ha effetto sulla gestione fuori banda in System Center 2012 Configuration Manager.

## <a name="changes-in-functionality"></a>Modifiche di funzionalità

Le sezioni seguenti includono un riepilogo di alcune modifiche significative introdotte nelle aree funzionali tra System Center 2012 R2 Configuration Manager e la versione 1511 di Configuration Manager Current Branch. Per altre informazioni sulle modifiche di funzionalità più recenti, vedere [Novità delle versioni incrementali](whats-new-incremental-versions.md).

### <a name="client-deployment"></a>Distribuzione client  

Configuration Manager introduce una nuova funzionalità per testare le nuove versioni del client di Configuration Manager prima di aggiornare il resto del sito con il nuovo software. È possibile configurare una raccolta di pre-produzione in cui eseguire la distribuzione pilota di un nuovo client. Quando si è soddisfatti del nuovo software client in fase di pre-produzione, è possibile promuovere il client per aggiornare automaticamente il resto del sito con la nuova versione.  

Per altre informazioni su come testare i client, vedere [Come testare gli aggiornamenti client in una raccolta di pre-produzione](../../clients/manage/upgrade/test-client-upgrades.md).  

### <a name="os-deployment"></a>Distribuzione del sistema operativo  

Tenere presente le seguenti modifiche per la distribuzione del sistema operativo:

- Nella Creazione guidata sequenza di attività è disponibile un nuovo tipo di sequenza di attività: **Aggiornare il sistema operativo da un pacchetto di aggiornamento**. Crea i passaggi per aggiornare i computer da Windows 7 o Windows 8.1 a Windows 10. Per altre informazioni, vedere [Aggiornare Windows alla versione più recente](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md).  

- La peer cache di Windows PE è ora disponibile quando si distribuiscono sistemi operativi. I computer che eseguono una sequenza di attività per distribuire un sistema operativo possono usare la peer cache di Windows PE per ottenere contenuto da un'origine peer cache, invece di scaricarlo da un punto di distribuzione. Questo comportamento contribuisce a ridurre al minimo il traffico WAN negli scenari con le filiali, in cui non esiste un punto di distribuzione locale. Per altre informazioni, vedere [Prepare Windows PE peer cache to reduce WAN traffic](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md) (Preparare la peer cache di Windows PE per ridurre il traffico della rete WAN)  

- Ora è possibile visualizzare lo stato di Windows come servizio nell'ambiente in uso. È anche possibile creare piani di manutenzione per formare circuiti di distribuzione e assicurarsi che i computer Windows 10 con la versione Current Branch siano mantenuti aggiornati quando vengono rilasciate nuove build. Inoltre, è possibile visualizzare avvisi quando i client Windows 10 si avvicinano alla scadenza del supporto per la build. Per altre informazioni, vedere [Gestire Windows come servizio](../../../osd/deploy-use/manage-windows-as-a-service.md).  

### <a name="application-management"></a>Gestione delle applicazioni  

Tenere presente le seguenti modifiche apportate alla gestione delle applicazioni:

- Configuration Manager consente di distribuire app della piattaforma UWP (Universal Windows Platform) per i dispositivi che eseguono Windows 10 e versioni successive. Per altre informazioni, vedere [Creare applicazioni Windows](../../../apps/get-started/creating-windows-applications.md).  

- Software Center ha un aspetto nuovo e moderno. Le app disponibili per gli utenti che in precedenza venivano visualizzate solo nel Catalogo applicazioni ora compaiono in Software Center nella scheda Applicazioni. In tal modo, queste distribuzioni sono maggiormente individuabili per gli utenti, che pertanto non dovranno più fare necessariamente riferimento al Catalogo applicazioni separato. Inoltre, non è più richiesto un browser abilitato per Silverlight. Per altre informazioni, vedere [Plan for and configure application management](../../../apps/plan-design/plan-for-and-configure-application-management.md) (Pianificare e configurare la gestione delle applicazioni).  

- Il nuovo tipo di applicazione Windows Installer tramite MDM consente di creare e distribuire app basate su Windows Installer nei PC registrati che eseguono Windows 10. Per altre informazioni, vedere [Creare applicazioni Windows](../../../apps/get-started/creating-windows-applications.md).  

- In Configuration Manager 2012, per specificare un collegamento a un'app in Windows Store, era possibile specificare direttamente il collegamento oppure passare a un computer remoto in cui era installata l'app. In Configuration Manager Current Branch è possibile immettere direttamente il collegamento, ma è anche possibile cercare l'app nell'archivio direttamente dalla console di Configuration Manager anziché passare a un computer di riferimento.  

### <a name="software-updates"></a>Aggiornamenti software  

Tenere presente le seguenti modifiche apportate agli aggiornamenti software:

- Configuration Manager ora può rilevare la differenza tra i metodi di gestione degli aggiornamenti software per i computer. In particolare, può distinguere tra un computer Windows 10 che si connette a Windows Update for Business (WUfB) e un computer connesso a WSUS. L'attributo **UseWUServer** è nuovo e specifica se il computer viene gestito con WUfB. È possibile usare questa impostazione in una raccolta per rimuovere questi computer dalla gestione degli aggiornamenti software. Per altre informazioni, vedere [Integration with Windows Update for Business in Windows 10](../../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md).  

- È ora possibile pianificare ed eseguire l'attività di pulizia WSUS dalla console di Configuration Manager. Nelle proprietà di **Componente punto di aggiornamento software**, quando si sceglie di eseguire l'attività di pulizia WSUS, questa viene eseguita alla successiva sincronizzazione degli aggiornamenti software. Gli aggiornamenti software scaduti vengono impostati su uno stato rifiutato nel server WSUS e l'Agente di Windows Update nei computer non esegue più la scansione di questi aggiornamenti software. Per ulteriori informazioni, vedere [Schedule and run the WSUS clean up task](../../../sum/deploy-use/software-updates-maintenance.md).  

### <a name="compliance-settings"></a>Impostazioni di conformità  

Tenere presente le seguenti modifiche apportate alle impostazioni di conformità:

- Configuration Manager ottimizza il flusso di lavoro per la creazione degli elementi di configurazione. Ora, quando si crea un elemento di configurazione e si selezionano le piattaforme supportate, sono disponibili solo le impostazioni rilevanti per tale piattaforma. Vedere [Introduzione alle impostazioni di conformità](../../../compliance/get-started/get-started-with-compliance-settings.md).  

- La **Creazione guidata dell'elemento di configurazione** semplifica la scelta del tipo di elemento di configurazione che si vuole creare. Inoltre, sono disponibili elementi di configurazione nuovi e aggiornati per:  

    - Dispositivi Windows 10 gestiti con il client di Configuration Manager  

    - Dispositivi OS X gestiti con il client di Configuration Manager  

    - Computer desktop e server Windows gestiti con il client di Configuration Manager  

    - Dispositivi Windows 8.1 e Windows 10 gestiti senza il client di Configuration Manager  

    Per altre informazioni, vedere [Come creare elementi di configurazione ](../../../compliance/deploy-use/create-configuration-items.md).  

- Supporto per la gestione delle impostazioni nei computer Mac OS X che vengono gestiti senza il client di Configuration Manager.

### <a name="on-premises-mobile-device-management"></a>Gestione di dispositivi mobili locale  

È ora possibile gestire i dispositivi mobili usando l'infrastruttura locale di Configuration Manager. Tutti i dati di gestione e dei dispositivi vengono gestiti in locale e non fanno parte di Microsoft Intune o altri servizi cloud. Questo tipo di gestione dei dispositivi non richiede il software client perché Configuration Manager gestisce i dispositivi con funzionalità integrate nel sistema operativo dei dispositivi.  

Per altre informazioni, vedere [Gestire i dispositivi mobili con l'infrastruttura locale](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).

## <a name="next-steps"></a>Passaggi successivi

[Novità delle versioni incrementali](whats-new-incremental-versions.md)
