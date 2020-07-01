---
title: Manuale dell'utente di Software Center
titleSuffix: Configuration Manager
description: Informazioni sulle funzionalità di Software Center
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 06/10/2020
ms.topic: end-user-help
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 9e68de6e-2b33-442b-b674-a382728d9529
ms.openlocfilehash: 19b1b56c394fbf71e9117ad12fbe900e6f07e5fb
ms.sourcegitcommit: 2f1963ae208568effeb3a82995ebded7b410b3d4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/11/2020
ms.locfileid: "84715551"
---
# <a name="software-center-user-guide"></a>Manuale dell'utente di Software Center

*Si applica a: Configuration Manager (Current Branch)*

L'amministratore IT dell'organizzazione usa Software Center per installare le applicazioni e gli aggiornamenti dei prodotti software e di Windows. Questo manuale dell'utente illustra le funzionalità di Software Center per gli utenti del computer.

L'installazione di Software Center viene eseguita automaticamente nei dispositivi Windows gestiti dall'organizzazione IT. Per iniziare, vedere [Come aprire Software Center](#bkmk_open).

Note generali sulle funzionalità di Software Center:

- Questo articolo descrive le funzionalità più recenti di Software Center. Se l'organizzazione usa una versione precedente ma ancora supportata di Software Center, non sono disponibili tutte le funzionalità. Per altre informazioni, contattare l'amministratore IT.

- L'amministratore IT può disabilitare alcune funzionalità di Software Center. L'esperienza specifica può variare.

- Se più utenti usano un dispositivo nello stesso momento, l'utente con l'ID di sessione più basso sarà l'unico a visualizzare tutte le distribuzioni disponibili in Software Center, ad esempio, più utenti in un ambiente Desktop remoto. Gli utenti con gli ID di sessione più elevati potrebbero non visualizzare alcune delle distribuzioni in Software Center. Ad esempio, gli utenti con ID di sessione superiore possono visualizzare le applicazioni distribuite, ma non i pacchetti distribuiti o le sequenze di attività. Nel frattempo, l'utente con l'ID di sessione più basso visualizzerà tutte le applicazioni, i pacchetti e le sequenze di attività distribuiti. La scheda **Utenti** di Gestione attività di Windows visualizza tutti gli utenti e gli ID di sessione corrispondenti.

- L'amministratore IT può modificare il colore di Software Center e aggiungere il logo dell'organizzazione.

## <a name="how-to-open-software-center"></a><a name="bkmk_open"></a> Come aprire Software Center

L'installazione di Software Center viene eseguita automaticamente nei dispositivi Windows gestiti dall'organizzazione IT. Il metodo più semplice per avviare Software Center in un computer Windows 10 consiste nel premere **Start** e digitare `Software Center`. Può non essere necessario digitare l'intera stringa per consentire a Windows di trovare la migliore corrispondenza.

:::image type="content" source="media/start-menu-software-center.png" alt-text="Migliore corrispondenza di Software Center nel menu Start":::

Per esplorare il menu Start, cercare l'icona **Software Center** nel gruppo **Microsoft Endpoint Manager**.

:::image type="content" source="media/microsoft-endpoint-manager-start-menu.png" alt-text="Icone del menu Start di Microsoft Endpoint Manager":::

> [!NOTE]
> Il percorso del menu Start precedente è quello della versione di novembre 2019 (versione 1910) e successive. Nelle versioni precedenti, il nome della cartella è **Microsoft System Center**.

Se non si riesce a trovare Software Center nel menu Start, contattare l'amministratore IT.

## <a name="applications"></a>Applicazioni

:::image type="content" source="media/software-center-apps.png" alt-text="Scheda Applicazioni di Software Center" lightbox="media/software-center-apps.png":::

Selezionare la scheda **Applicazioni** (1) per trovare e installare le applicazioni che l'amministratore IT distribuisce all'utente o al computer.

- **Tutte** (2): visualizza tutte le applicazioni disponibili che è possibile installare.

- **Obbligatorie** (3): l'amministratore IT richiede l'installazione di queste applicazioni. Se si disinstalla una di queste applicazioni, Software Center la reinstalla.

- **Filtri** (4): l'amministratore IT può creare categorie di applicazioni. Se disponibile, selezionare l'elenco a discesa per filtrare la visualizzazione e visualizzare solo le applicazioni di una categoria specifica. Selezionare **Tutte** per visualizzare tutte le applicazioni.

- **Ordina per** (5): consente di riordinare l'elenco delle applicazioni. Per impostazione predefinita questo elenco è ordinato per **Più recente**. Le applicazioni disponibili da poco sono visualizzate con un banner **Novità** visibile per sette giorni.

- **Cerca** (6): l'elemento cercato non è stato trovato? Immettere parole chiave nella casella di ricerca per trovarlo.

- Alternare la visualizzazione (7): selezionare le icone per alternare tra la visualizzazione elenco e la visualizzazione affiancata. Per impostazione predefinita l'elenco delle applicazioni viene visualizzato sotto forma di elementi grafici affiancati.

|Icona|Visualizza|Descrizione|
|----|----|-----------|
|:::image type="icon" source="media/software-center-multi-select-apps.png" border="false":::|**Modalità selezione multipla**|Consente di installare più applicazioni contemporaneamente. Per altre informazioni, vedere [Installare più applicazioni](#install-multiple-applications).|
|:::image type="icon" source="media/software-center-apps-list-view.png" border="false":::|**Visualizzazione elenco**|contiene l'icona dell'applicazione, il nome, l'editore, la versione e lo stato.|
|:::image type="icon" source="media/software-center-apps-tile-view.png" border="false":::|**Visualizzazione affiancata**|l'amministratore IT può personalizzare le icone. Sotto ogni riquadro vengono visualizzati il nome dell'applicazione, l'editore e la versione.|

### <a name="install-an-application"></a>Installare un'applicazione

Selezionare un'applicazione dall'elenco per visualizzare altre informazioni su di essa. Selezionare **Installa** per installarla. Se un'app è già installata, è possibile scegliere di **disinstallarla**.

Alcune app possono richiedere l'approvazione prima dell'installazione.

- Quando si prova a eseguire l'installazione, è possibile immettere un commento e quindi **richiedere** l'app.

  :::image type="content" source="media/software-center-app-approval-request.png" alt-text="Richiesta di approvazione per l'installazione dell'app Software Center":::

- Software Center visualizza la cronologia delle richieste ed è possibile annullare la richiesta.

  :::image type="content" source="media/software-center-app-approval-status.png" alt-text="Installazione dell'app Software Center richiesta":::

- Quando un amministratore approva la richiesta, è possibile installare l'app. Se si attende, Software Center installa automaticamente l'app durante un orario non di ufficio.

  :::image type="content" source="media/software-center-app-approved.png" alt-text="Installazione dell'app Software Center approvata":::

### <a name="install-multiple-applications"></a>Installare più applicazioni

<!-- 1357126 -->
È possibile installare più applicazioni contemporaneamente anziché attendere il completamento di un'installazione prima di iniziare quella successiva. Le app selezionate devono soddisfare i requisiti seguenti:

- L'app deve essere visibile all'utente
- L'app non deve essere già installata o in fase di download
- Per installare l'app non è necessaria l'approvazione dell'admin IT

Per installare più applicazioni contemporaneamente:

1. Selezionare l'icona per la selezione multipla nell'angolo superiore destro: :::image type="icon" source="media/software-center-multi-select-apps.png" border="false":::

2. Selezionare due o più app da installare. Selezionare la casella di controllo a sinistra di ogni app nell'elenco.

3. Selezionare il pulsante di **installazione degli elementi selezionati** per avviare l'installazione.

Le app vengono installate come di consueto, ma in successione.

### <a name="share-an-application"></a>Condividere un'applicazione

Per condividere un collegamento a un'app specifica, dopo aver selezionato l'app, selezionare l'icona **Condividi** nell'angolo superiore destro: :::image type="icon" source="media/software-center-share-app-icon.png" border="false":::

:::image type="content" source="media/software-center-share-app-window.png" alt-text="Condividere un'applicazione da Software Center":::

**Copiare** la stringa e incollarla altrove, ad esempio in un messaggio di posta elettronica. Ad esempio, `softwarecenter:SoftwareID=ScopeId_73F3BB5E-5EDC-4928-87BD-4E75EB4BBC34/Application_b9e438aa-f5b5-432c-9b4f-6ebeeb132a5a` Tutti gli altri utenti dotati di Software Center nell'organizzazione potranno usare il collegamento per aprire la stessa applicazione.

## <a name="updates"></a>Aggiornamenti

:::image type="content" source="media/software-center-updates.png" alt-text="Scheda Aggiornamenti di Software Center" lightbox="media/software-center-updates.png":::

Selezionare la scheda **Aggiornamenti** (1) per visualizzare e installare gli aggiornamenti software che l'amministratore IT distribuisce al computer in uso.  

- **Tutti** (2): visualizza tutti gli aggiornamenti che è possibile installare

- **Obbligatori** (3): l'amministratore IT richiede l'installazione di questi aggiornamenti.

- **Ordina per** (4): consente di riordinare l'elenco degli aggiornamenti. Per impostazione predefinita questo elenco è ordinato per **Nome applicazione: da A a Z**.

- **Cerca** (5): l'elemento cercato non è stato trovato? Immettere parole chiave nella casella di ricerca per trovarlo.

Per installare gli aggiornamenti, selezionare **Installa Tutti** (6).

Per installare solo aggiornamenti specifici, selezionare l'icona che consente di passare alla modalità di selezione multipla (7): :::image type="icon" source="media/software-center-multi-select-apps.png" border="false":::
Selezionare gli aggiornamenti da installare e quindi selezionare il pulsante di **installazione degli elementi selezionati**.

## <a name="operating-systems"></a>Sistemi operativi

:::image type="content" source="media/software-center-os.png" alt-text="Scheda Sistemi operativi di Software Center" lightbox="media/software-center-os.png":::

Selezionare la scheda **Sistemi operativi** (1)per visualizzare e installare le versioni di Windows che l'amministratore IT distribuisce al computer in uso.  

- **Tutti** (2): visualizza tutte le versioni di Windows che è possibile installare

- **Obbligatori** (3): l'amministratore IT richiede l'installazione di questi aggiornamenti.

- **Ordina per** (4): consente di riordinare l'elenco degli aggiornamenti. Per impostazione predefinita questo elenco è ordinato per **Nome applicazione: da A a Z**.

- **Cerca** (5): l'elemento cercato non è stato trovato? Immettere parole chiave nella casella di ricerca per trovarlo.

## <a name="installation-status"></a>Stato installazione

Selezionare la scheda **Stato installazione** per visualizzare lo stato delle applicazioni. Possono essere visualizzati gli stati seguenti:

- **Installata**: Software Center ha già installato questa applicazione nel computer.

- **Download in corso**: Software Center sta scaricando il software da installare nel computer.

- **Operazione non riuscita**: Software Center non è stato in grado di installare il software.

- **Installazione pianificata dopo** : mostra la data e ora della successiva finestra di manutenzione del dispositivo per installare software futuri. Le finestre di manutenzione vengono definite dall'amministratore IT.<!--1358131-->

  - Lo stato può essere visualizzato nelle schede **Tutto** e **Imminente**.

  - È possibile eseguire l'installazione prima della data e dell'ora della finestra di manutenzione selezionando il pulsante **Installa adesso**.

## <a name="device-compliance"></a>Conformità del dispositivo

Selezionare la scheda **Conformità del dispositivo** per visualizzare lo stato di conformità del computer.

Selezionare **Controlla conformità** per confrontare le impostazioni del dispositivo con i criteri di sicurezza definiti dall'amministratore IT.

## <a name="options"></a>Options

Selezionare la scheda **Opzioni** per visualizzare le impostazioni aggiuntive per questo computer.

### <a name="work-information"></a>Informazioni di lavoro

Indicare l'orario di lavoro generico. L'amministratore IT può pianificare installazioni di software fuori dall'orario lavorativo. Prevedere almeno quattro ore al giorno per le attività di manutenzione del sistema. L'amministratore IT può installare comunque applicazioni e aggiornamenti critici durante l'orario di ufficio.

- Selezionare le ore in cui si inizia e si smette di usare il computer. Per impostazione predefinita questi valori sono compresi tra le **5.00** e le **22.00**.

- Selezionare i giorni della settimana nei quali in genere si usa il computer. Per impostazione predefinita, Software Center seleziona solo i giorni lavorativi.

Specificare se si usa regolarmente questo computer per lavorare. L'amministratore potrebbe installare automaticamente applicazioni o rendere disponibili altre applicazioni ai computer primari.<!--3485366--> Se il computer in uso è un computer primario, selezionare **Uso regolarmente il computer per lavorare**.

### <a name="power-management"></a>Risparmio energia

L'amministratore IT può impostare criteri di risparmio energia. Questi criteri aiutano l'organizzazione a risparmiare energia elettrica quando il computer non è in uso.

Per rendere il computer esente da questi criteri, selezionare **Non applicare le impostazioni di risparmio energia dal reparto IT a questo computer**. Per impostazione predefinita, questa impostazione è disabilitata e il computer applica le impostazioni di risparmio energia.

### <a name="computer-maintenance"></a>Manutenzione computer

Specificare in che modo Software Center deve applicare modifiche al software prima della scadenza.

- **Installare o disinstallare automaticamente il software richiesto e riavviare il computer solo fuori dall'orario di lavoro specificato**: Per impostazione predefinita, questa impostazione è disabilitata.

- **Sospendi le attività di Software Center quando il computer si trova in modalità presentazione**: Questa opzione è attivata per impostazione predefinita.

Quando richiesto dall'amministratore IT, selezionare **Sync Policy** (Criteri di sincronizzazione). Il computer verifica sui server la presenza di nuovi elementi, quali applicazioni, aggiornamenti software o sistemi operativi.

### <a name="remote-control"></a>Controllo remoto

Specificare le impostazioni di accesso remoto e di controllo remoto per il computer.

**Usa le impostazioni di accesso remoto del reparto IT**: per impostazione predefinita, il reparto IT definisce le impostazioni per l'assistenza remota. Le altre impostazioni in questa sezione visualizzano lo stato delle impostazioni definite dal reparto IT. Per modificare le impostazioni, disabilitare prima questa opzione.

- **Livello di accesso remoto consentito**
  - **Non consentire l'accesso remoto**: gli amministratori IT non possono accedere in remoto al computer per offrire assistenza.
  - **Solo visualizzazione**: un amministratore IT può solo visualizzare lo schermo in remoto.
  - **Completa**: un amministratore IT può controllare il computer in remoto. Questa è l'impostazione predefinita.

- **Consenti il controllo remoto del computer da parte degli amministratori in assenza dell'utente**. Per impostazione predefinita, questa opzione corrisponde a **Sì**.

- **Quando un amministratore tenta di controllare il computer in remoto**
  - **Chiedi sempre l'autorizzazione**: Questa è l'impostazione predefinita.
  - **Non richiedere autorizzazioni**

- **Mostra quanto segue durante il controllo remoto**: Queste notifiche visive sono entrambe abilitate per impostazione predefinita per comunicare che un amministratore si sta connettendo in remoto al dispositivo.
  - **Icona di stato nell'area di notifica**
  - **Una barra di connessione alla sessione sul desktop**

- **Riprodurre suono**: Questa notifica acustica informa che un amministratore si sta connettendo in remoto al dispositivo.
  - **All'inizio e alla fine della sessione**: Questa è l'impostazione predefinita.
  - **Ripetutamente nel corso della sessione**
  - **Mai**

## <a name="custom-tabs"></a>Schede personalizzate

L'amministratore IT può rimuovere le schede predefinite o aggiungere altre schede a Software Center. Le schede personalizzate, a cui viene assegnato un nome dall'amministratore, aprono un sito Web specificato dall'amministratore stesso. Una scheda denominata "Help desk", ad esempio, può aprire il sito Web dell'help desk dell'organizzazione IT. <!--1358132-->

## <a name="more-information-for-it-administrators"></a>Altre informazioni per gli amministratori IT

Per gli amministratori IT sono disponibili altre informazioni su come pianificare e configurare Software Center negli articoli seguenti:

- [Pianificare Software Center](../../apps/plan-design/plan-for-software-center.md)
- [Impostazioni client di Software Center](../clients/deploy/about-client-settings.md#software-center)
- [Notifiche di riavvio del dispositivo](../clients/deploy/device-restart-notifications.md)
- [Introduzione al controllo remoto](../clients/manage/remote-control/introduction-to-remote-control.md)
