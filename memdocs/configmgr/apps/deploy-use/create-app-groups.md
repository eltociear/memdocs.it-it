---
title: Creare gruppi di applicazioni
titleSuffix: Configuration Manager
description: Creare un gruppo di applicazioni che è possibile inviare a un utente o a una raccolta di dispositivi come singola distribuzione in Configuration Manager.
ms.date: 04/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: e67c691e-62ef-4f43-9cfb-0e957d1e7a5f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f63c52fcd2aaccbfbe04160581318126bc53db12
ms.sourcegitcommit: 2aa97d1b6409575d731c706faa2bc093c2b298c4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82643123"
---
# <a name="create-application-groups"></a>Creare gruppi di applicazioni

*Si applica a: Configuration Manager (Current Branch)*

<!--3555907-->

A partire dalla versione 1906, creare un gruppo di applicazioni che è possibile inviare a un utente o a una raccolta di dispositivi come singola distribuzione. I metadati specificati in relazione al gruppo di app sono visualizzati in Software Center come una singola entità. È possibile ordinare le app del gruppo in modo che il client le installi in un ordine specifico.

> [!Note]  
> In questa versione di Configuration Manager, i gruppi di app sono in una versione non definitiva. Per abilitarla, vedere [Funzionalità di versioni non definitive in System Center Configuration Manager](../../core/servers/manage/pre-release-features.md).  

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**. Espandere **Gestione applicazioni** e selezionare il nodo **Gruppo applicazioni**.  

1. In Crea gruppo sulla barra multifunzione selezionare **Crea gruppo di applicazioni**.

1. Nella pagina **Informazioni generali** specificare le informazioni sul gruppo di app.  

1. Nella pagina **Software Center** includere le informazioni visualizzate in Software Center.  

1. Nella pagina **Gruppo di applicazioni** selezionare **Aggiungi**. Selezionare una o più app per questo gruppo. Riordinarle usando le azioni **Sposta su** e **Sposta giù**.  

1. Completare la procedura guidata.  

Distribuire il gruppo di app seguendo la stessa procedura usata per un'applicazione. Per altre informazioni, vedere l'argomento relativo alla [distribuzione delle applicazioni](deploy-applications.md). A partire dalla versione 1910, è possibile distribuire un gruppo di app a raccolte di dispositivi o utenti.

Dopo aver distribuito il gruppo:

- Se si aggiunge una nuova app al gruppo, è necessario distribuire separatamente il contenuto della nuova app ai punti di distribuzione.

- Se si modifica un'app nel gruppo app, ridistribuire il contenuto.

Per risolvere i problemi relativi alla distribuzione di un gruppo di app, usare i file di log seguenti nel client:

- **AppGroupHandler.log**
- **AppEnforce.log**
- **SettingsAgent.log**

> [!Important]  
> Creare o distribuire un gruppo di app solo dopo aver aggiornato l'intera gerarchia e i client di destinazione almeno alla versione 1906.

### <a name="known-issues"></a>Problemi noti

- *Versione 1906*: Le app del gruppo possono contenere solo i tipi di distribuzione **Windows Installer** o **Script**.
  - *Versione 1906*: impostare il comportamento di installazione del tipo di distribuzione su **Installa per sistema**.
- Le opzioni di distribuzione seguenti potrebbero non funzionare: avvisi, approvazione, distribuzione in più fasi, ripristino.
- Non è possibile esportare o importare gruppi di app.
- Non includere nel gruppo le app che richiedono il riavvio. In caso contrario, la distribuzione del gruppo potrebbe non riuscire.
- *Versione 1906*: non è possibile distribuire un gruppo di app a una raccolta utenti.
- *Versione 1906*: Gli utenti non possono **disinstallare** il gruppo di app in Software Center.
- Se si elimina un'app che fa parte di un gruppo di app, alla successiva visualizzazione delle proprietà del gruppo di app verrà visualizzato l'avviso seguente: "Unable to load information about all applications in the group." (Non è possibile caricare informazioni su tutte le applicazioni nel gruppo) Apportare una modifica semplice al gruppo di app e salvarlo. Ad esempio, aggiungere uno spazio ai **Commenti amministratore**. Quando si salva la modifica, l'app eliminata viene rimossa dal gruppo.<!-- 7099542 -->
