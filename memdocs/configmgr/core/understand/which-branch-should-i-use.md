---
title: Scegliere il ramo da usare
titleSuffix: Configuration Manager
description: Informazioni sulle differenze tra i rami disponibili di Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a3be4f8f-3d44-4e3c-9fa1-e85f30a36e72
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 542069b82ea4c68a48ccc47b79007fd2fa25322a
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906017"
---
# <a name="which-branch-of-configuration-manager-should-i-use"></a>Scelta del ramo di Configuration Manager da usare

*Si applica a: Configuration Manager (Current Branch e Technical Preview Branch) e System Center Configuration Manager (Long-Term Servicing Branch)*

Sono disponibili tre rami di Configuration Manager:

- Current Branch
- Long Term Servicing Branch
- Technical Preview Branch

Usare questo articolo per scegliere il ramo idoneo.

> [!TIP]  
> Tutti i siti in una gerarchia devono eseguire lo stesso ramo. Le gerarchie con rami differenti in siti diversi non sono supportate.

## <a name="current-branch"></a>Current Branch

Questo ramo ha una licenza per l'uso in un ambiente di produzione. Usare questo ramo per ottenere le funzioni e le funzionalità più recenti. Si può usare questo ramo se si dispone di una delle seguenti licenze:  

- System Center Datacenter
- System Center Standard
- System Center Configuration Manager
- Diritti di sottoscrizione equivalenti  

Per altre informazioni su Software Assurance e sulle opzioni di licenza, vedere [Licenze e rami per System Center Configuration Manager](learn-more-editions.md) e [Domande frequenti relative ai rami e alle licenze di Configuration Manager](product-and-licensing-faq.md).

Microsoft prevede di rilasciare diversi aggiornamenti per le versioni Current Branch di Configuration Manager ogni anno. Il supporto di ogni versione aggiornata dura 18 mesi dalla data di rilascio con disponibilità generale (GA). Il supporto tecnico viene garantito per l'intero periodo. Tuttavia, la struttura di supporto è dinamica e si evolve in due fasi di assistenza distinte che dipendono dalla disponibilità della versione Current Branch più recente. Per altre informazioni, vedere [Supporto per le versioni di Configuration Manager Current Branch](../servers/manage/current-branch-versions-supported.md). Gli aggiornamenti alle versioni più recenti sono disponibili come aggiornamenti nella console.

Per installare la versione Current Branch come un nuovo sito, usare [Supporto della versione di base](../servers/manage/updates.md#bkmk_Baselines). Inoltre, usare il supporto di base per aggiornare System Center Configuration Manager 2012 con Service Pack 2 o System Center Configuration Manager 2012 R2 con Service Pack 1. L'accesso a questo supporto dipende dalla licenza scelta dalla propria organizzazione per Configuration Manager.

È anche possibile usare il supporto di base per installare un nuovo sito come copia di valutazione di Current Branch. La versione di valutazione non richiede una licenza. È possibile utilizzare la versione di valutazione per 180 giorni. Supporta l'aggiornamento a una versione con licenza di Current Branch. Per installare solo una copia di valutazione, scaricarla da [Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection).

> [!NOTE]
> Usare il supporto di base per installare siti per una nuova gerarchia di Configuration Manager. Se è stata precedentemente installata una versione di base, usare gli aggiornamenti nella console per aggiornare i siti a una nuova versione.  
>
> I siti che vengono aggiornati usando gli aggiornamenti nella console sono uguali al nuovo sito installato usando il supporto di base.
>
> Per altre informazioni, vedere [Aggiornamenti per Configuration Manager](../servers/manage/updates.md).  

### <a name="features-of-the-current-branch"></a>Funzionalità di Current Branch

- Riceve [aggiornamenti nella console](../servers/manage/install-in-console-updates.md) che rendono le nuove funzionalità disponibili per l'uso.
- Riceve aggiornamenti nella console che forniscono correzioni della sicurezza e qualità alle funzionalità esistenti.
- Supporta aggiornamenti fuori programma quando necessario. Per altre informazioni, vedere [Usare lo strumento di registrazione dell'aggiornamento](../servers/manage/use-the-update-registration-tool-to-import-hotfixes.md) o [Usare il programma di installazione degli hotfix](../servers/manage/use-the-hotfix-installer-to-install-updates.md).
- È integrabile con i servizi basati sul cloud.
- Supporta la [migrazione dei dati](../migration/migrate-data-between-hierarchies.md) da e verso altre installazioni di Configuration Manager.
- Supporta l'aggiornamento dalle versioni precedenti di Configuration Manager.
- Supporta l'installazione come copia di valutazione da cui è possibile eseguire un successivo aggiornamento a un'installazione con licenza completa.

Microsoft consiglia di eseguire l'aggiornamento alla versione più recente non appena viene rilasciata. Possono trascorrere fino 18 mesi prima dell'aggiornamento a una versione più recente. È anche possibile ignorare un aggiornamento per installare la versione più recente disponibile. Poiché ogni versione è cumulativa, se si ignora un aggiornamento e si installa la versione più recente, si otterrà comunque l'accesso a tutte le funzionalità e i miglioramenti delle versioni precedenti.

Per altre informazioni, vedere [Supporto per versioni di Current Branch](../servers/manage/current-branch-versions-supported.md).

### <a name="current-branch-update-options"></a>Opzioni di aggiornamento per le versioni Current Branch

- Con Software Assurance attivo, è possibile installare gli aggiornamenti nella console per le versioni di Current Branch.  
- Non è possibile convertire la versione Current Branch in Technical Preview Branch. Technical Preview Branch sono installazioni distinte che non richiedono una licenza.
- Non è possibile convertire la versione Current Branch in Long-Term Servicing Branch (LTSB). È necessario disinstallare Current Branch e quindi installare LTSB come una nuova installazione.

## <a name="long-term-servicing-branch"></a>Long Term Servicing Branch

Si tratta di un ramo con licenza destinato all'uso nell'ambiente di produzione da parte di clienti di Configuration Manager che usano Current Branch e che hanno lasciato scadere la sottoscrizione Configuration Manager Software Assurance (SA) o diritti di sottoscrizione equivalenti dopo il 1° ottobre 2016. Per altre informazioni su Software Assurance e sulle opzioni di licenza, vedere [Licenze e rami per System Center Configuration Manager](learn-more-editions.md) e [Domande frequenti relative ai rami e alle licenze di Configuration Manager](product-and-licensing-faq.md).

L'opzione LTSB è basata sulla versione 1606. Questo ramo non riceve aggiornamenti nella console che offrono nuove funzionalità o aggiornano funzionalità esistenti. Tuttavia, vengono fornite correzioni critiche per la protezione. Per installare LTSB è necessario usare il [supporto di base](../servers/manage/updates.md#bkmk_Baselines) della versione 1606 ricevuto con System Center 2016. Le versioni di base più recenti non supportano l'installazione di LTSB.

Per installare la versione LTSB come nuovo sito o come aggiornamento da un sito supportato di System Center 2012 Configuration Manager, usare il [supporto di base](../servers/manage/updates.md#bkmk_Baselines) della versione 1606 ricevuto con System Center 2016. È possibile usare il supporto di base per installare un nuovo sito che esegue la versione 1606 di Current Branch o che esegue Long-Term Servicing Branch.

> [!TIP]  
> Per informazioni su System Center 2016, vedere la relativa [documentazione](https://docs.microsoft.com/system-center/index). Questa documentazione indica inoltre come ottenere System Center 2016, che richiede un contratto di licenza Microsoft o diritti analoghi.  
>  
> Per trovare Configuration Manager versione 1606 in Volume Licensing Service Center (VLSC), passare alla scheda **Downloads and Keys** (Download e codici) di [VLSC](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx), cercare `System Center 2016` e selezionare **System Center 2016 Datacenter** o **System Center 2016 Standard**.  
>  
> È possibile ottenere una copia di valutazione di System Center 2016 anche da [Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-technical-preview).  

### <a name="features-of-the-ltsb"></a>Funzionalità di LTSB

- Riceve gli aggiornamenti nella console che forniscono correzioni critiche per la protezione.
- Fornisce un'opzione di installazione dopo che il contratto SA o i diritti equivalenti per Configuration Manager sono scaduti.
- Supporta l'aggiornamento (conversione) a Current Branch quando si dispone di un contratto SA o diritti equivalenti validi per Configuration Manager.

### <a name="ltsb-limitations"></a>Limitazioni di LTSB

LTSB si basa su Current Branch 1606, con le limitazioni seguenti:

- Dopo la disponibilità generale (ottobre 2016), l'opzione LTSB sarà supportata per 10 anni di aggiornamenti critici per la sicurezza, periodo dopo il quale il supporto per questo ramo scadrà. Per altre informazioni sul ciclo di vita del supporto, vedere [Criteri relativi al ciclo di vita Microsoft](https://support.microsoft.com/lifecycle).
- Supporta un elenco definito limitato di sistemi operativi client e server e tecnologie correlate come le versioni di SQL Server. Per altre informazioni, vedere [Configurazioni supportate per Long-Term Servicing Branch](supported-configurations-for-ltsb.md).
- Non riceve gli aggiornamenti per le nuove funzionalità
- Non supporta le seguenti funzionalità:
  - Funzionalità associate al cloud come la co-gestione o Desktop Analytics
  - Software MDM locale
  - Dashboard di manutenzione di Windows 10, piani di manutenzione o canale semestrale di Windows 10
  - Versioni future di LTSB di Windows 10 e Windows Server
  - Asset intelligence
  - Qualsiasi funzionalità di versioni non definitive

### <a name="ltsb-update-options"></a>Opzioni di aggiornamento di LTSB

- È possibile convertire l'installazione LTSB a un'installazione Current Branch. La conversione a Current Branch è supportata prima o dopo la scadenza del supporto per LTSB.

  Per eseguire la conversione, è necessario disporre di un contratto Software Assurance attivo con Microsoft. Per altre informazioni, vedere gli articoli seguenti:

  - [Aggiornare Long-Term Servicing Branch a Current Branch](convert-to-current-branch.md)
  - [Licenze e rami per Configuration Manager](learn-more-editions.md)
  - [Baseline and update versions](../servers/manage/updates.md#bkmk_Baselines) (Versioni di base e di aggiornamento)

- Non è possibile convertire LTSB in Technical Preview Branch. Technical Preview Branch sono installazioni distinte che non richiedono una licenza.

- Non è possibile aggiornare una copia di valutazione di Current Branch a un'installazione LTSB.

## <a name="technical-preview-branch"></a>Technical Preview Branch

Technical Preview Branch deve essere utilizzata in un ambiente lab. Informarsi sulle funzionalità più recenti in fase di sviluppo per Configuration Manager e provarle. Non è supportata in un ambiente di produzione e non è necessario disporre di un contratto di licenza Software Assurance.

Per installare un nuovo sito che esegue Technical Preview Branch, usare la versione più recente del [supporto di base per Technical Preview Branch](../get-started/technical-preview.md#bkmk_install). Dopo aver installato Technical Preview Branch, saranno disponibili ogni mese le nuove versioni come aggiornamenti nella console.

### <a name="features-of-the-technical-preview-branch"></a>Funzionalità di Technical Preview Branch

- Basata sulle versioni di base recenti di Current Branch
- Riceve gli aggiornamenti nella console per l'aggiornamento dell'installazione all'ultima versione Technical Preview Branch
- Include nuove funzionalità in fase di sviluppo e per le quali Microsoft desidera ricevere commenti e suggerimenti degli utenti
- Riceve gli aggiornamenti applicabili solo a Technical Preview Branch

### <a name="technical-preview-limitations"></a>Limitazioni della versione Technical Preview

- [Il supporto è limitato](../get-started/technical-preview.md#bkmk_reqs), tra cui un singolo sito primario e fino a 10 client.  
- Non è possibile eseguire l'aggiornamento o la migrazione a un'installazione Current Branch o LTSB.
- Non supporta i seguenti comportamenti:
  - L'uso della migrazione per importare o esportare dati in un'altra installazione di Configuration Manager
  - L'aggiornamento dalle versioni precedenti di Configuration Manager
  - L'installazione come copia di valutazione

Le funzionalità inizialmente introdotte in una Technical Preview Branch vengono spesso aggiunte a Current Branch in un aggiornamento successivo. Ogni nuova versione di Technical Preview Branch include le funzionalità delle versioni precedenti, anche dopo che tali funzioni sono state aggiunte a Current Branch.

Per altre informazioni, vedere [Technical Preview per Configuration Manager](../get-started/technical-preview.md).

### <a name="technical-preview-update-options"></a>Opzioni di aggiornamento di Technical Preview

- È possibile installare qualsiasi aggiornamento nella console per una nuova versione di Technical Preview Branch.

- Non è possibile convertire Technical Preview Branch in Current Branch o LTSB.

## <a name="identify-your-version-and-branch"></a>Individuare la versione e il ramo

### <a name="version"></a>Version

Per controllare la versione del sito, nella console passare a **Informazioni su Configuration Manager** nell'angolo in alto a sinistra. Questa finestra di dialogo consente di visualizzare la **Versione sito**. Per un elenco delle versioni del sito, vedere [Versioni di base e di aggiornamento](../servers/manage/updates.md#bkmk_Baselines).

### <a name="branch"></a>Ramo

Per verificare il ramo del sito, nella console passare ad **Amministrazione** > **Configurazione del sito** > **Siti** e aprire **Impostazioni gerarchia**. Se è attiva un'opzione per la conversione in Current Branch, il sito esegue la versione LTSB. Se il sito esegue la versione Current Branch, questa opzione è disabilitata.

Per altre informazioni sulle diverse versioni di Configuration Manager, vedere [Versioni di base e di aggiornamento](../servers/manage/updates.md#bkmk_Baselines).
