---
title: Manuale dell'utente di Software Center
titleSuffix: Configuration Manager
description: Informazioni sulle funzionalità di Software Center
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 04/12/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 9e68de6e-2b33-442b-b674-a382728d9529
ms.openlocfilehash: c4fa0819bf6427d93adf44a7b6284a8266e3a6a5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706809"
---
# <a name="software-center-user-guide"></a>Manuale dell'utente di Software Center

*Si applica a: Configuration Manager (Current Branch)*

L'amministratore IT dell'organizzazione usa Software Center per installare le applicazioni e gli aggiornamenti dei prodotti software e di Windows. Questo manuale dell'utente illustra le funzionalità di Software Center per gli utenti del computer.

Note generali sulle funzionalità di Software Center:

- Questo articolo descrive le funzionalità più recenti di Software Center. Se l'organizzazione usa una versione precedente ma ancora supportata di Software Center, non sono disponibili tutte le funzionalità. Per altre informazioni, contattare l'amministratore IT.

- L'amministratore IT può disabilitare alcune funzionalità di Software Center. L'esperienza specifica può variare.

- Se più utenti usano un dispositivo nello stesso momento, ad esempio tramite più sessioni di desktop remoto, l'utente con l'ID di sessione più basso sarà l'unico a visualizzare tutte le distribuzioni disponibili in Software Center. Gli utenti con gli ID di sessione più elevati potrebbero non visualizzare alcune delle distribuzioni in Software Center. Ad esempio, gli utenti con ID di sessione superiore possono visualizzare le applicazioni distribuite, ma non i pacchetti distribuiti o le sequenze di attività. Nel frattempo, l'utente con l'ID di sessione più basso visualizzerà tutte le applicazioni, i pacchetti e le sequenze di attività distribuiti.

<!-- - Your IT admin may change the color of Software Center, and add your organization's logo. The images in this article show the default experience. -->

## <a name="how-to-open-software-center"></a><a name="bkmk_open"></a> Come aprire Software Center

Il metodo più semplice per avviare Software Center in un computer Windows 10 consiste nel premere **Start** e digitare `Software Center`. Può non essere necessario digitare l'intera stringa per consentire a Windows di trovare la migliore corrispondenza.

Se si scorre il menu Start, cercare l'icona **Software Center** nel gruppo **Microsoft Endpoint Manager**.

![Icone del menu Start di Microsoft Endpoint Manager](media/microsoft-endpoint-manager-start-menu.png)

> [!NOTE]
> Nella versione 1910 il percorso del menu Start è stato modificato. Nella versione 1906 e precedenti, il nome della cartella è **Microsoft System Center**. Quando si aggiorna Configuration Manager alla versione 1910 o successiva, assicurarsi di aggiornare la documentazione gestita internamente in modo da includere questo nuovo percorso.

## <a name="applications"></a>Applicazioni

Selezionare la scheda **Applicazioni** per trovare e installare le applicazioni che l'amministratore IT distribuisce all'utente o al computer.

- **Tutti**: visualizza tutte le applicazioni che è possibile installare
- **Richiesto**: l'amministratore IT richiede l'installazione di queste applicazioni. Se si disinstalla una di queste applicazioni, Software Center la reinstalla.
- **Filtri**: l'amministratore IT può creare categorie di applicazioni. Se disponibile, selezionare l'elenco a discesa per filtrare la visualizzazione e visualizzare solo le applicazioni di una categoria specifica. Selezionare **Tutte** per visualizzare tutte le applicazioni.
- **Ordina per**: consente di riordinare l'elenco delle applicazioni. Per impostazione predefinita questo elenco è ordinato per **Più recente**. Le applicazioni rese disponibili di recente sono elencate con un tag **Nuovo** visibile per 7 giorni.
- **Cerca**: l'elemento cercato non è stato trovato? Immettere parole chiave nella casella di ricerca per trovarlo.
- **Alternare la visualizzazione**: selezionare le icone per alternare tra la visualizzazione elenco e la visualizzazione affiancata. Per impostazione predefinita l'elenco delle applicazioni viene visualizzato sotto forma di elementi grafici affiancati.
    - Visualizzazione affiancata: l'amministratore IT può personalizzare le icone. Sotto ogni riquadro vengono visualizzati il nome dell'applicazione, l'editore e la versione.
    - Visualizzazione elenco: contiene l'icona dell'applicazione, il nome, l'editore, la versione e lo stato.

### <a name="install-multiple-applications"></a>Installare più applicazioni

<!-- 1357126 -->
È possibile installare più applicazioni contemporaneamente anziché attendere il completamento di un'installazione prima di iniziare quella successiva. Non tutte le applicazioni sono idonee:

- L'app deve essere visibile all'utente
- L'app non deve essere già installata o in fase di download
- Per installare l'app non è necessaria l'approvazione dell'admin IT

Per installare più applicazioni contemporaneamente:

1. Per accedere alla modalità di selezione multipla nella visualizzazione elenco, selezionare l'icona di selezione multipla ![Icona di selezione multipla del Software Center](media/software-center-multi-select-apps.png) nell'angolo superiore destro.
2. Selezionare due o più app da installare selezionando la casella di controllo a sinistra delle app nell'elenco.
3. Selezionare il pulsante di **installazione degli elementi selezionati**.

Le app vengono installate come di consueto, ma in successione.


## <a name="updates"></a>Aggiornamenti

Selezionare la scheda **Aggiornamenti** per visualizzare e installare gli aggiornamenti software che l'amministratore IT distribuisce a questo computer.  

- **Tutti**: visualizza tutti gli aggiornamenti che è possibile installare
- **Richiesto**: l'amministratore IT richiede l'installazione di questi aggiornamenti.
- **Ordina per**: consente di riordinare l'elenco degli aggiornamenti. Per impostazione predefinita questo elenco è ordinato per **Nome applicazione: da A a Z**.

Per installare gli aggiornamenti selezionare **Installa tutto**.

Per installare solo aggiornamenti specifici, selezionare l'icona che consente di passare alla modalità di selezione multipla. Selezionare gli aggiornamenti da installare e quindi selezionare il pulsante di **installazione degli elementi selezionati**.


## <a name="operating-systems"></a>Sistemi operativi

Selezionare la scheda **Sistemi operativi** per visualizzare e installare le versioni di Windows che l'amministratore IT distribuisce al computer.  

- **Tutti**: visualizza tutte le versioni di Windows che è possibile installare
- **Richiesto**: l'amministratore IT richiede l'installazione di questi aggiornamenti.
- **Ordina per**: consente di riordinare l'elenco degli aggiornamenti. Per impostazione predefinita questo elenco è ordinato per **Nome applicazione: da A a Z**.


## <a name="installation-status"></a>Stato installazione

Selezionare la scheda **Stato installazione** per visualizzare lo stato delle applicazioni. Possono essere visualizzati gli stati seguenti:

- **Installata**: Software Center ha già installato questa applicazione nel computer.
- **Download in corso**: Software Center sta scaricando il software da installare nel computer.
- **Operazione non riuscita**: Software Center ha riscontrato un errore nel tentativo di installare il software.
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

- Selezionare gli elenchi a discesa per selezionare le ore in cui si inizia e si smette di usare il computer. Per impostazione predefinita questi valori sono compresi tra **5.00** e **22.00**.

- Selezionare la casella di controllo accanto ai giorni della settimana nei quali in genere viene usato il computer. Per impostazione predefinita Software Center seleziona solo i giorni lavorativi.  

Specificare se si usa regolarmente questo computer per lavorare. L'amministratore potrebbe installare automaticamente applicazioni o rendere disponibili altre applicazioni ai computer primari. <!--3485366-->

- Selezionare **Uso regolarmente il computer per lavorare** se il computer in uso è un computer primario.

### <a name="power-management"></a>Risparmio energia

L'amministratore IT può impostare criteri di risparmio energia. Questi criteri aiutano l'organizzazione a risparmiare energia elettrica quando il computer non è in uso.

Per rendere il computer esente da questi criteri, selezionare la casella di controllo **Non applicare le impostazioni di risparmio energia del reparto IT al computer**. Questa impostazione è disabilitata per impostazione predefinita. Il computer applica le impostazioni di risparmio energia.

### <a name="computer-maintenance"></a>Manutenzione computer

Specifica come Software Center applica le modifiche al software prima della scadenza.

- **Installare o disinstallare automaticamente il software richiesto e riavviare il computer solo fuori dall'orario di lavoro specificato**: Per impostazione predefinita, questa impostazione è disabilitata.
- **Sospendi le attività di Software Center quando il computer si trova in modalità presentazione**: Questa opzione è attivata per impostazione predefinita.
- **Sincronizza criteri**: selezionare questo pulsante quando richiesto dall'amministratore IT. Il computer verifica sui server la presenza di nuovi elementi, quali applicazioni, aggiornamenti software o sistemi operativi.

### <a name="remote-control"></a>Controllo remoto

Specificare le impostazioni di accesso remoto e di controllo remoto per il computer

- **Usa le impostazioni di accesso remoto del reparto IT**: questa casella di controllo è selezionata per impostazione predefinita.
- **Livello di accesso remoto consentito**: selezionare una delle tre opzioni seguenti
    - **Non consentire l'accesso remoto**
    - **Solo visualizzazione**
    - **Completa**: questo livello è abilitato per impostazione predefinita.
- **Consenti il controllo remoto del computer da parte degli amministratori in assenza dell'utente**. Questa impostazione corrisponde a **Sì** per impostazione predefinita.
- **Quando un amministratore tenta di controllare il computer in remoto**: questa impostazione ha due opzioni
    - **Chiedi sempre l'autorizzazione**: Questa opzione è selezionata per impostazione predefinita.
    - **Non richiedere autorizzazioni**
- **Mostra quanto segue durante il controllo remoto**: entrambe le opzioni sono selezionate per impostazione predefinita
    - **Icona di stato nell'area di notifica**
    - **Una barra di connessione alla sessione sul desktop**
- **Riprodurre suono**: questa impostazione ha tre opzioni
    - **All'inizio e alla fine della sessione**: questa opzione è selezionata per impostazione predefinita.
    - **Ripetutamente nel corso della sessione**
    - **Mai**

    Per altre informazioni, vedere [Introduzione al controllo remoto](../clients/manage/remote-control/introduction-to-remote-control.md)
    

## <a name="custom-tab-in-software-center"></a>Scheda personalizzata in Software Center

L'amministratore IT potrebbe avere aggiunto una scheda aggiuntiva in Software Center. Questa scheda viene denominata dall'amministratore e porta a un sito Web specificato. Ad esempio, si potrebbe avere una scheda denominata "Help desk" che conduce al sito Web dell'help desk dell'organizzazione. <!--1358132-->
