---
title: Collegare utenti e dispositivi mediante l'affinità utente dispositivo
titleSuffix: Configuration Manager
description: Collegare gli utenti e i dispositivi mediante l'affinità utente-dispositivo e distribuire automaticamente le app a tutti i dispositivi associati a un utente.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 5b30b0d5-722d-4d4b-9ed7-5a43de315461
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8e1a55efa6b23aa489ea65b3296e33847163a5c4
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695240"
---
# <a name="link-users-and-devices-with-user-device-affinity-in-configuration-manager"></a>Collegare utenti e dispositivi con l'affinità utente-dispositivo in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

L'affinità utente-dispositivo in Configuration Manager associa un utente a uno o più dispositivi. Questo comportamento può eliminare la necessità di conoscere i nomi dei dispositivi di un utente per poter distribuire un'applicazione all'utente. Anziché distribuire l'applicazione a ogni dispositivo dell'utente, è possibile distribuire l'applicazione all'utente. L'affinità utente-dispositivo garantisce quindi automaticamente l'installazione dell'applicazione in tutti i dispositivi associati all'utente.  

Definire i dispositivi primari che gli utenti usano ogni giorno per il lavoro. Quando si crea un'affinità tra un utente e un dispositivo, si ottengono più opzioni di distribuzione delle app. Ad esempio, se un utente deve usare Microsoft Visio, è possibile installarlo nel dispositivo primario dell'utente usando una distribuzione di Windows Installer. Tuttavia, in un dispositivo non primario si potrebbe distribuire Visio come un'applicazione virtuale. È anche possibile usare l'affinità utente-dispositivo per pre-distribuire il software in un dispositivo dell'utente quando l'utente non è connesso. Quando l'utente esegue l'accesso, l'app è già installata e pronta per essere eseguita.  

È necessario gestire solo le informazioni sull'affinità utente-dispositivo per i computer. Configuration Manager gestisce automaticamente le affinità utente-dispositivo per i dispositivi mobili che registra.  

## <a name="manually-set-up-user-device-affinity"></a>Configurare manualmente l'affinità utente-dispositivo  

1. Nella console di Configuration Manager passare all'area di lavoro **Asset e conformità** e selezionare il nodo **Dispositivi**.  

1. Selezionare un dispositivo. Nella scheda **Home** nella barra multifunzione nel gruppo **Dispositivo** scegliere **Modifica utenti primari**.  

1. Nella finestra di dialogo **Modifica utenti primari** individuare e selezionare gli utenti da aggiungere come utenti primari per il dispositivo selezionato. Scegliere **Aggiungi**.  

    > [!NOTE]  
    > Nell'elenco **Utenti primari** vengono visualizzati gli utenti già configurati come utenti primari del dispositivo e il metodo con cui è stata assegnata ogni relazione utente-dispositivo.  

## <a name="set-up-primary-devices-for-a-user"></a>Configurare i dispositivi primari per un utente  

1. Nella console di Configuration Manager passare all'area di lavoro **Asset e conformità** e selezionare il nodo **Utenti**.  

1. Selezionare un utente. Nella scheda **Dispositivo** della barra multifunzione scegliere **Modifica dispositivi primari**.  

1. Nella finestra di dialogo **Modifica dispositivi primari** individuare e selezionare i dispositivi da aggiungere come dispositivi primari per l'utente selezionato. Scegliere **Aggiungi**.  

    > [!NOTE]  
    > Nell'elenco **Dispositivi primari** vengono visualizzati i dispositivi già configurati come dispositivi primari per l'utente e il metodo con cui è stata assegnata ogni relazione utente-dispositivo.  

## <a name="automatically-create-user-device-affinities-windows-pcs-only"></a>Creare automaticamente le affinità utente dispositivo (solo PC Windows)

Configuration Manager legge i dati sugli eventi di accesso utente dal registro eventi di Windows. Per creare automaticamente le affinità utente-dispositivo, attivare le due opzioni seguenti nei criteri di sicurezza locali nei computer client per archiviare gli eventi di accesso nel registro eventi di Windows:  

- **Controlla eventi di accesso account**  
- **Controlla eventi di accesso**  

Per configurare queste impostazioni, usare i criteri di gruppo di Windows.  

> [!IMPORTANT]  
> Se un errore causa la generazione di un numero elevato di voci da parte del registro eventi di Windows, è possibile che venga creato un nuovo registro eventi. Se si verifica questo comportamento, gli eventi di accesso esistenti potrebbero non essere disponibili per Configuration Manager.  

### <a name="set-up-the-site-to-automatically-create-user-device-affinities"></a>Configurare il sito per creare automaticamente le affinità utente-dispositivo  

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione** e selezionare il nodo **Impostazioni client**.  

1. Per modificare le impostazioni client predefinite, selezionare **Impostazioni client predefinite**. Nella scheda **Home** della barra multifunzione scegliere **Proprietà** nel gruppo **Proprietà**.

    Per creare impostazioni agente client personalizzate, nella scheda **Home** scegliere **Crea impostazioni dispositivo client personalizzate** nel gruppo **Crea**.

    > [!NOTE]  
    > Se si modificano le impostazioni client predefinite, le impostazioni verranno distribuite a tutti i computer nella gerarchia. Per altre informazioni, vedere [Come configurare le impostazioni client](../../core/clients/deploy/configure-client-settings.md).  

1. Specificare le impostazioni seguenti nel gruppo **Affinità dispositivi e utenti**:  

    - **Soglia di utilizzo di affinità utente dispositivo (minuti)** : Impostare il numero di minuti di utilizzo del dispositivo prima che il sito crei un'affinità utente-dispositivo.  

    - **Soglia di utilizzo di affinità utente dispositivo (giorni)** : impostare il numero di giorni in cui il sito misura la soglia di affinità in base all'utilizzo.  

    - **Configurare automaticamente l'affinità utente dispositivo dai dati di utilizzo**: Selezionare **True** per consentire al sito di creare automaticamente le affinità utente-dispositivo. Se si seleziona **False**, è necessario approvare manualmente tutte le assegnazioni di affinità utente-dispositivo.  

    > [!TIP]  
    > Ad esempio, se l'opzione **Soglia di utilizzo di affinità utente dispositivo (minuti)** viene impostata su **60** minuti e l'opzione **Soglia di utilizzo di affinità utente dispositivo (giorni)** viene impostata su **5** giorni, l'utente deve usare il dispositivo per almeno 60 minuti in un periodo di 5 giorni per creare automaticamente un'affinità utente-dispositivo.  

Dopo aver creato un'affinità utente-dispositivo automatica, Configuration Manager continua a monitorare le soglie di affinità utente-dispositivo. Se l'attività dell'utente per il dispositivo è inferiore alle soglie impostate, il sito rimuove l'affinità utente-dispositivo. Impostare **Soglia di utilizzo di affinità utente dispositivo (giorni)** su un valore di almeno sette giorni. Questa configurazione consente di evitare situazioni in cui un'affinità utente dispositivo configurata automaticamente possa andare persa mentre l'utente non è connesso, ad esempio durante il fine settimana.  


## <a name="import-user-device-affinities-from-a-file"></a>Importare le affinità utente dispositivo da un file

Per creare più relazioni contemporaneamente, importare un file contenente dettagli per più affinità utente-dispositivo. Verificare che i dispositivi di destinazione siano già individuati dal sito ed esistano come risorse nel database di Configuration Manager.  

1. Nella console di Configuration Manager passare all'area di lavoro **Asset e conformità** e selezionare il nodo **Utenti** o **Dispositivi**.  

1. Nella scheda **Home** della barra multifunzione nel gruppo **Crea** scegliere **Importa affinità utente dispositivo**.  

1. Nell'Importazione guidata affinità utente dispositivo nella pagina **Scegliere il mapping** specificare le informazioni seguenti:  

    - **Nome file**. Specificare un file con valori delimitati da virgole, con estensione CSV, che contenga un elenco di utenti e dispositivi tra cui si vuole creare un'affinità. In questo file ogni coppia utente-dispositivo deve trovarsi su una riga separata, con valori delimitati da una virgola. Usare questo formato: `<domain>\<username>,<device NetBIOS name>`  

    - **Questo file contiene intestazioni di colonna a scopo di riferimento**. Se il file CSV ha un'intestazione di riga superiore, selezionare questa opzione. Il sito ignora la riga di intestazione durante l'importazione.  

1. Se il file che si sta importando contiene più di due elementi per riga, usare **Colonna** e **Assegna** per specificare le colonne che rappresentano gli utenti e i dispositivi e le colonne da ignorare durante l'importazione.  

1. Completare la procedura guidata.  


## <a name="let-users-create-their-own-device-affinities"></a>Consentire agli utenti di creare le proprie affinità dispositivo

Impostare un utente per creare un'affinità utente-dispositivo in Software Center.

### <a name="set-up-the-site-to-allow-user-created-user-device-affinity-requests"></a>Configurare il sito per consentire le richieste di affinità utente-dispositivo create dagli utenti  

1  Nella console di Configuration Manager passare all'area di lavoro **Amministrazione** e selezionare il nodo **Impostazioni client**.  

1. Per modificare le impostazioni client predefinite, selezionare **Impostazioni client predefinite**. Nella scheda **Home** della barra multifunzione scegliere **Proprietà** nel gruppo **Proprietà**.

    Per creare impostazioni agente client personalizzate, nella scheda **Home** scegliere **Crea impostazioni utente client personalizzate** nel gruppo **Crea**.

    > [!NOTE]  
    > Se si modificano le impostazioni client predefinite, le impostazioni verranno distribuite a tutti i computer nella gerarchia. Per altre informazioni, vedere [Configurare le impostazioni client](../../core/clients/deploy/configure-client-settings.md).  

1. Nel gruppo **Affinità dispositivi e utenti** abilitare l'impostazione **Consentire all'utente di definire i dispositivi primari**.  

### <a name="set-up-a-user-device-affinity-in-software-center"></a>Impostare un'affinità utente-dispositivo in Software Center

A partire dalla versione 1902, usare software Center per impostare l'affinità.

1. In Software Center passare alla scheda **Opzioni**.

1. Attivare l'opzione **Uso regolarmente il computer per lavorare** nella sezione **Informazioni di lavoro**.

### <a name="set-up-a-user-device-affinity-in-the-application-catalog"></a>Configurare un'affinità utente-dispositivo nel Catalogo applicazioni

> [!Important]
> L'esperienza utente di Silverlight per il catalogo applicazioni non è supportata a partire dalla versione Current Branch 1806. A partire dalla versione 1906, i client aggiornati usano automaticamente il punto di gestione per le distribuzioni di applicazioni disponibili per gli utenti. Non è inoltre possibile installare nuovi ruoli del Catalogo applicazioni. Il supporto per i ruoli del Catalogo applicazioni termina con la versione 1910.  
>
> Per altre informazioni, vedere gli articoli seguenti:
>
> - [Configurare Software Center](../plan-design/plan-for-software-center.md#bkmk_userex)
> - [Funzionalità rimosse e deprecate](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

1. Nel Catalogo applicazioni scegliere **My Systems** (Sistemi personali).  

1. Attivare l'opzione **Uso regolarmente il computer per lavorare**.  


## <a name="manage-user-device-affinity-requests-from-users"></a>Gestire le richieste di affinità utente dispositivo dagli utenti

Quando si disabilita l'impostazione client **Configurare automaticamente l'affinità utente dispositivo dai dati di utilizzo**, è necessario approvare manualmente tutte le assegnazioni affinità utente-dispositivo.  

### <a name="approve-or-reject-a-user-device-affinity-request"></a>Approvare o rifiutare una richiesta di affinità utente-dispositivo  

1. Nella console di Configuration Manager passare all'area di lavoro **Asset e conformità**.  

1. Selezionare la raccolta utenti o dispositivi per cui si vuole gestire le richieste di affinità.  

1. Nella scheda **Home** della barra multifunzione nel gruppo **Raccolta** scegliere **Gestisci richieste affinità**.  

1. Nella finestra di dialogo **Gestire le richieste di affinità utente dispositivo** selezionare una richiesta di affinità e quindi fare clic su **Approva** o **Rifiuta**.  


## <a name="next-steps"></a>Passaggi successivi

È anche possibile usare Microsoft Intune per trovare l'uso principale di un dispositivo registrato. Per altre informazioni, vedere [Trovare l'utente primario di un dispositivo Intune](/intune/find-primary-user) nella documentazione di Intune.