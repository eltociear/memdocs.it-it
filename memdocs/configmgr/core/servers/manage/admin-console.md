---
title: Console di Configuration Manager
titleSuffix: Configuration Manager
description: Informazioni sull'esplorazione tramite la console di Configuration Manager.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 463ce307-59dd-4abd-87b8-42ca9db178d7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: bcc1f8e93f4fb312b74fd7e5746928182b05710f
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126495"
---
# <a name="how-to-use-the-configuration-manager-console"></a>Come usare la console di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Gli amministratori usano la console di Configuration Manager per gestire l'ambiente di Configuration Manager. Questo articolo illustra le nozioni di base dell'esplorazione della console.  

## <a name="open-the-console"></a><a name="bkmk_open"></a> Aprire la console

La console di Configuration Manager viene sempre installata nel server del sito. È anche possibile installarla in altri computer. Per altre informazioni, vedere [Installare la console di Configuration Manager](../deploy/install/install-consoles.md).

Il metodo più semplice per aprire la console in un computer Windows 10 consiste nel premere **Start** e iniziare a digitare `Configuration Manager console`. Può non essere necessario digitare l'intera stringa per consentire a Windows di trovare la migliore corrispondenza.

Se si scorre il menu Start, cercare l'icona **Console di Configuration Manager** nel gruppo **Microsoft Endpoint Manager**.

![Icone del menu Start di Microsoft Endpoint Manager](media/microsoft-endpoint-manager-start-menu.png)

> [!NOTE]
> Nella versione 1910 il percorso del menu Start è stato modificato. Nella versione 1906 e precedenti, il nome della cartella è **System Center**. Quando si aggiorna Configuration Manager alla versione 1910 o successiva, assicurarsi di aggiornare la documentazione gestita internamente in modo da includere questo nuovo percorso.

## <a name="connect-to-a-site-server"></a>Connettersi a un server del sito

La console si connette al server di sito di amministrazione centrale o ai server del sito primario. Non è possibile connettere una console di Configuration Manager a un sito secondario. Durante l'installazione, è stato specificato il nome di dominio completo (FQDN) del server del sito a cui si connette la console.

Per connettersi a un server del sito diverso, eseguire questa procedura:

1. Selezionare la freccia nella parte superiore della [barra multifunzione](#ribbon) e scegliere **Connetti a un nuovo sito**.  

    ![Connettere la console a un nuovo sito](media/connect-to-a-new-site.png)  

2. Digitare il nome di dominio completo del server del sito. Se precedentemente ci si è connessi al server del sito, selezionare il server dall'elenco a discesa.  

    ![Nella finestra Connessione al sito immettere il nome di dominio completo del server del sito](media/site-server-fqdn.png)  

3. Selezionare **Connetti**.  

A partire dalla versione 1810, è possibile specificare il livello di autenticazione minimo per gli amministratori per l'accesso ai siti di Configuration Manager. Questa funzionalità impone agli amministratori di accedere a Windows con il livello richiesto. Per altre informazioni, vedere [Piano per il provider SMS](../../plan-design/hierarchy/plan-for-the-sms-provider.md#bkmk_auth). <!--1357013-->  

## <a name="navigation"></a>Spostamento

Alcune aree della console potrebbero non essere visibili a seconda del ruolo di sicurezza assegnato. Per altre informazioni sui ruoli, vedere [Nozioni fondamentali sull'amministrazione basata su ruoli](../../understand/fundamentals-of-role-based-administration.md).

### <a name="workspaces"></a>Aree di lavoro

La console di Configuration Manager ha quattro **aree di lavoro**:  

- **Asset e conformità**  

- **Raccolta software**  

- **Monitoraggio**  

- **Amministrazione**  

![Aree di lavoro di Configuration Manager con menu di scelta rapida](media/configuration-manager-workspaces.png)  

Riordinare i pulsanti delle aree di lavoro selezionando la freccia giù e scegliendo **Opzioni riquadro di spostamento**. Selezionare un elemento e fare clic su **Sposta su** o **Sposta giù**. Selezionare **Reimposta** per ripristinare l'ordine predefinito dei pulsanti.  

![Finestra Opzioni riquadro di spostamento per riordinare le aree di lavoro](media/navigation-pane-options.png)  

Ridurre a icona il pulsante di un'area di lavoro selezionando **Mostra meno pulsanti**. Prima viene ridotta a icona l'ultima area di lavoro dell'elenco. Selezionare un pulsante ridotto a icona e scegliere **Mostra più pulsanti** per ripristinare le dimensioni originali del pulsante.

![Aree di lavoro ridotte a icona nella console di Configuration Manager](media/workspace-buttons.png)  

### <a name="nodes"></a>Nodi

Le aree di lavoro sono una raccolta di **nodi**. Un esempio di nodo è il nodo **Gruppi di aggiornamenti software** nell'area di lavoro **Raccolta software**.

All'interno del nodo, è possibile selezionare la freccia per ridurre il riquadro di spostamento.  

![Nodo di esempio e freccia di riduzione evidenziata](media/software-update-groups-node.png)  

Usare la **barra di spostamento** per muoversi nella console quando si riduce a icona il riquadro di spostamento.  

![Riquadro di spostamento ridotto a icona di Configuration Manager](media/minimized-navigation-pane.png)  

Nella console i nodi in alcuni casi sono organizzati in cartelle. Quando si seleziona la cartella, in genere si visualizza un **indice di spostamento** o una **dashboard**.  

![Indice di spostamento degli aggiornamenti software per Configuration Manager](media/software-updates-navigation-index.png)  

### <a name="ribbon"></a>Barra multifunzione

La barra multifunzione è nella parte superiore della console di Configuration Manager. La barra multifunzione può avere più di una scheda e può essere ridotta a icona con la freccia sulla destra. I pulsanti sulla barra multifunzione sono diversi a seconda del nodo. La maggior parte dei pulsanti della barra multifunzione è disponibile anche nei menu di scelta rapida.  

![Barra multifunzione di esempio, evidenziazione di più schede e freccia di riduzione](media/ribbon.png)

### <a name="details-pane"></a>Riquadro dei dettagli

È possibile ottenere informazioni aggiuntive sugli elementi esaminando il riquadro dei dettagli. Il riquadro dei dettagli può avere una o più schede. Le schede variano a seconda del nodo.  

![Riquadro dei dettagli di esempio di Configuration Manager](media/details-pane.png)

### <a name="columns"></a>Colonne

È possibile aggiungere, rimuovere, riordinare e ridimensionare le colonne. Queste azioni consentono di visualizzare i dati che si preferisce. Le colonne disponibili variano a seconda del nodo. Per aggiungere o rimuovere una colonna dalla visualizzazione, fare clic con il pulsante destro del mouse sull'intestazione di una colonna esistente e selezionare un elemento. Riordinare le colonne trascinando l'intestazione di colonna nella posizione desiderata.  

![Aggiungere colonne in Configuration Manager](media/add-columns.png)  

Nella parte inferiore del menu di scelta rapida della colonna è possibile ordinare o raggruppare in base a una colonna. È anche possibile ordinare in base a una colonna selezionandone l'intestazione.  

![Raggruppare per colonna in Configuration Manager](media/column-group-by.png)  

## <a name="reclaim-lock-for-editing-objects"></a><a name="bkmk_sedo"></a> Richiamare il blocco per la modifica delle sequenze di attività

<!--4786915-->

Se la console di Configuration Manager non risponde, può essere bloccata la possibilità di apportare ulteriori modifiche fino al termine del blocco, dopo 30 minuti. Questo blocco fa parte del sistema di Configuration Manager SEDO (modifica serializzata di Distributed Objects). Per altre informazioni, vedere [Configuration Manager SEDO](../../../develop/core/understand/sedo.md).

A partire da [Current Branch versione 1906](../../plan-design/changes/whats-new-in-version-1906.md#reclaim-sedo-lock-for-task-sequences), è possibile cancellare il blocco su una sequenza di attività. A partire dalla versione 1910, è possibile cancellare il blocco su qualsiasi oggetto nella console di Configuration Manager.

Questa azione si applica solo al proprio account utente che ha il blocco e allo stesso dispositivo da cui il sito ha concesso il blocco. Quando si tenta di accedere a un oggetto bloccato, è ora possibile **rimuovere le modifiche** e continuare a modificare l'oggetto. Queste modifiche andrebbero perse comunque al termine del blocco.

## <a name="view-recently-connected-consoles"></a><a name="bkmk_viewconnected"></a> Visualizzare le console connesse di recente

<!--3699367-->
A partire dalla versione 1902, è possibile visualizzare le connessioni più recenti per la console di Configuration Manager. La visualizzazione include le connessioni attive e quelle stabilite di recente. Nell'elenco si vedrà sempre la connessione corrente alla console e si vedranno solo le connessioni dalla console di Configuration Manager. Non sarà possibile vedere le connessioni PowerShell o altre connessioni al provider SMS basate su SDK. Il sito rimuove dall'elenco le istanze anteriori a 30 giorni.

### <a name="prerequisites-to-view-connected-consoles"></a><a name="bkmk_connections-prereq"></a> Prerequisiti per visualizzare le console connesse

- Account con autorizzazione di **lettura** per l'oggetto **SMS_Site**

- Configurare l'API REST del servizio di amministrazione. Per altre informazioni, vedere [Che cos'è il servizio di amministrazione](../../../develop/adminservice/overview.md).

### <a name="view-connected-consoles"></a>Visualizzare le console connesse

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**.  

2. Espandere **Sicurezza** e selezionare il nodo **Connessioni di console**.  

3. Visualizzare le connessioni recenti, con le proprietà seguenti:  

    - Nome utente
    - Nome computer
    - Codice del sito connesso
    - Versione della console
    - Ora dell'ultima connessione: l'ultima volta che l'utente ha *aperto* la console
    - A partire dalla versione 1910, la colonna **Ultimo heartbeat della console** ha sostituito la colonna **Ora dell'ultima connessione**. <!--4923997-->
       - Una console aperta in primo piano invia un heartbeat ogni 10 minuti.

![Visualizzare le connessioni della console di Configuration Manager](media/console-connections.png)

## <a name="start-microsoft-teams-chat-from-console-connections"></a><a name="bkmk_message"></a> Avviare la chat di Microsoft Teams da connessioni della console
<!--4923997-->
*(Funzionalità introdotta nella versione 1910)*

A partire dalla versione 1910, è possibile inviare messaggi agli altri amministratori di Configuration Manager dal nodo **Connessioni di console** usando Microsoft Teams. Quando si sceglie **Avvia la chat di Microsoft Teams** per avviare una chat con un amministratore, viene avviato Microsoft Teams e viene aperta una chat con l'utente.

### <a name="prerequisites"></a>Prerequisiti

- Per avviare una chat con un amministratore, è necessario che l'account con cui si vuole chattare sia stato individuato con [Azure AD o l'individuazione dell'utente AD](../deploy/configure/about-discovery-methods.md#bkmk_aboutUser).
- Nel dispositivo da cui viene eseguita la console deve essere installato Microsoft Teams.
nota
- Tutti i [prerequisiti per visualizzare le console connesse](#bkmk_connections-prereq)

### <a name="start-microsoft-teams-chat"></a>Avviare la chat di Microsoft Teams

1. Passare ad **Amministrazione** > **Sicurezza** > **Connessioni di console**.
1. Fare clic con il pulsante destro del mouse sulla connessione di console di un utente e selezionare **Avvia la chat di Microsoft Teams**.
    - Se il nome dell'entità utente non viene trovato per l'amministratore selezionato, l'opzione **Avvia la chat di Microsoft Teams** è disattivata.
    - Viene visualizzato un messaggio di errore, incluso un collegamento per il download, se Microsoft Teams non è installato nel dispositivo da cui viene eseguita la console.
    - Se Microsoft Teams è installato nel dispositivo da cui viene eseguita la console, verrà aperta una chat con l'utente.

### <a name="known-issues"></a>Problemi noti

Il messaggio di errore che informa che Microsoft Teams non è installato non verrà visualizzato se la chiave del Registro di sistema seguente non esiste:

Computer\HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall

Per risolvere il problema, creare manualmente la chiave del Registro di sistema.

## <a name="in-console-documentation-dashboard"></a><a name="bkmk_doc-dashboard"></a> Dashboard della documentazione nella console

<!--3556019 FKA 1357546-->
A partire da Configuration Manager versione 1902, è disponibile il nodo **Documentazione** nella nuova area di lavoro **Community**. Questo nodo contiene informazioni aggiornate sulla documentazione di Configuration Manager e gli articoli del supporto tecnico. Include le sezioni seguenti:  

### <a name="product-documentation-library"></a>Libreria della documentazione del prodotto

- **Consigliato**: un elenco curato manualmente di articoli importanti.
- **Di tendenza**: gli articoli più visualizzati nell'ultimo mese.
- **Aggiornato di recente**: gli articoli rivisti nell'ultimo mese.

### <a name="support-articles"></a>Articoli del supporto tecnico

- **Articoli sulla risoluzione dei problemi**: procedure dettagliate guidate per la risoluzione dei problemi relativi a funzionalità e componenti di Configuration Manager.
- **Articoli del supporto tecnico nuovi e aggiornati**: articoli nuovi o aggiornati negli ultimi due mesi.

### <a name="troubleshooting-connection-errors"></a>Risoluzione dei problemi relativi agli errori di connessione
Il nodo **Documentazione** non ha configurazioni proxy esplicite. Usa qualsiasi proxy definito dal sistema operativo nell'applet del pannello di controllo **Opzioni Internet**. Per riprovare dopo un errore di connessione, aggiornare il nodo **Documentazione**.


## <a name="command-line-options"></a>Opzioni della riga di comando

La console di Configuration Manager include le seguenti opzioni della riga di comando:

|Opzione|Descrizione|  
|------------|-----------------|  
|`/sms:debugview=1`|Una DebugView viene inserita in tutte le ResultViews che specificano una visualizzazione. DebugView mostra le proprietà non elaborate (nomi e valori).|  
|`/sms:NamespaceView=1`|Mostra la visualizzazione dello spazio dei nomi nella console.|  
|`/sms:ResetSettings`|La console ignora la connessione permanente dell'utente e gli stati della visualizzazione. Le dimensioni della finestra non vengono reimpostate.|  
|`/sms:IgnoreExtensions`|Disabilita tutte le estensioni di Configuration Manager.|  
|`/sms:NoRestore`|La console ignora lo spostamento del nodo permanente precedente.|  


## <a name="next-steps"></a>Passaggi successivi

- [Notifiche della console](admin-console-notifications.md)
- [Suggerimenti sulla console](admin-console-tips.md)
- [Funzionalità di accesso facilitato](../../understand/accessibility-features.md)
- [Editor delle sequenze di attività](../../../osd/understand/task-sequence-editor.md#bkmk_conditions)
