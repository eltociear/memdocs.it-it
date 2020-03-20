---
title: Gestire le app dal sito Web del Portale aziendale Intune
description: Gestire e visualizzare le app disponibili e installate
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 06/27/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: ''
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 374b433ff6ee50f91343489ae36a1a190d87c7aa
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79347860"
---
# <a name="manage-apps-from-the-company-portal-website"></a>Gestire le app dal sito Web del portale aziendale 
Visitare il [sito Web Portale aziendale](https://portal.manage.microsoft.com) per visualizzare e gestire le app dell'organizzazione. 

## <a name="view-all-apps"></a>Visualizzare tutte le app  
Dal menu selezionare **App** per visualizzare tutte le app rese disponibili dall'organizzazione. 

   ![Screenshot della pagina App del sito Web Portale aziendale, che mostra le opzioni di affinamento.](./media/intune-view-apps-1907.png)  

In questa pagina sono elencati i dettagli seguenti su ogni app:  

* Nome: nome dell'app, con un collegamento alla pagina dei dettagli dell'app.
* Autore: nome dello sviluppatore o dell'azienda che ha distribuito l'app. Un autore è in genere un fornitore di software o la propria organizzazione.  
* Data di pubblicazione: data in cui l'app è stata resa disponibile per il download. La data di pubblicazione può indicare il rilascio iniziale di un'app o l'aggiornamento più recente di un'app.
* Stato: stato attuale dell'app nel dispositivo, inclusi Disponibile, Installata e Installazione in corso. 
* Categoria: funzione o scopo dell'app, ad esempio In primo piano, Progettazione, Istruzione e Produttività.  

### <a name="search-and-refine"></a>Ricerca e affinamento   

Usare la barra di ricerca per trovare le app. I risultati della ricerca sono ordinati automaticamente per pertinenza.  

   ![Screenshot della pagina App del sito Web Portale aziendale, che mostra le opzioni di affinamento.](./media/intune-refine-all-apps-1907.png)  

Selezionare **Rifinisci** per visualizzare le opzioni di filtro e ordinamento. Filtrare l'elenco per visualizzare le app con criteri specifici, ad esempio **Tipo**, **Disponibilità** e **Autori**. Selezionare **Ordina** per ridisporre le app in base a:

* Nome dell'app, in ordine alfabetico crescente o decrescente 
* Nome dell'autore, in ordine alfabetico crescente o decrescente 
* Data di pubblicazione, meno recente o più recente  

## <a name="view-installed-apps"></a>Visualizzare le app installate  
Dal menu selezionare **App installate** per visualizzare un elenco di tutte le app installate nel dispositivo.  

   ![Screenshot del sito Web del portale aziendale, pagina App installate.](./media/intune-installed-apps-1907.png)  


In questa pagina sono elencati i dettagli seguenti su ogni app:  

* Nome: nome dell'app, con un collegamento alla pagina dei dettagli dell'app.
* Tipo di assegnazione: modo in cui l'app viene assegnata e resa disponibile. Per altri dettagli, vedere App disponibili e obbligatorie. L'organizzazione può rendere disponibile un'app per l'installazione da parte dell'utente o può richiedere e installare automaticamente un'app nel dispositivo.  
* Autore: nome dello sviluppatore o dell'azienda che ha distribuito l'app. Un autore è in genere un fornitore di software o la propria organizzazione.  
* Data di pubblicazione: data in cui l'app è stata resa disponibile per il download. La data di pubblicazione può indicare il rilascio iniziale di un'app o l'aggiornamento più recente di un'app.
* Stato: stato attuale dell'installazione dell'app nel dispositivo. Le app possono essere contrassegnate come Installazione in corso, Installata e Installazione non riuscita. Per visualizzare lo stato aggiornato delle app obbligatorie, potrebbero essere necessari fino a 10 minuti.  

### <a name="search-and-refine"></a>Ricerca e affinamento  

Usare la barra di ricerca per trovare le app. I risultati della ricerca sono ordinati automaticamente per pertinenza.  

   ![Screenshot del sito Web del Portale aziendale, App installate, opzioni di affinamento.](./media/intune-installed-refine-1907.png)  

Selezionare **Rifinisci** per visualizzare le opzioni di filtro e ordinamento. Filtrare l'elenco per visualizzare le app con criteri specifici, ad esempio **Tipi**, **Autori** e **Stati**. Selezionare **Ordina** per ridisporre le app in base a:

* Nome dell'app, in ordine alfabetico crescente o decrescente  
* Nome dell'autore, in ordine alfabetico crescente o decrescente  
* Data di pubblicazione, meno recente o più recente  

Servono altre informazioni? Contattare l'amministratore IT. Per informazioni sul contatto vedere il [sito Web del portale aziendale](https://go.microsoft.com/fwlink/?linkid=2010980).  

### <a name="available-and-required-apps"></a>App disponibili e obbligatorie
Le app vengono assegnate dall'organizzazione e contrassegnate come disponibili o obbligatorie. Nella pagina **App installate** sono visualizzate le app presenti nella colonna **Tipo di assegnazione**. 


* App disponibili: queste app vengono selezionate dall'organizzazione e sono appropriate e utili all'interno dell'azienda o dell'istituto di istruzione. La loro installazione è facoltativa e sono le uniche app disponibili in Portale aziendale per l'installazione. 

* App obbligatorie: l'organizzazione potrebbe distribuire le app necessarie all'interno dell'azienda o dell'istituto di istruzione direttamente nel dispositivo dell'utente. Queste app vengono installate automaticamente senza alcun intervento da parte dell'utente. 

Le app sono inoltre disponibili in base al tipo di dispositivo. Ad esempio, se si usa il sito Web del portale aziendale in un dispositivo Windows, si avrà accesso alle app per Windows, ma non alle app per iOS.  

## <a name="view-app-details"></a>Visualizzare i dettagli delle app  
Selezionare un'app nella pagina **App** o **App installate** per visualizzarne i dettagli. Verrà visualizzata la schermata **Dettagli app**, in cui sono disponibili la descrizione e i requisiti dell'app. Se un'app non è già installata nel dispositivo, è possibile installarla da questa pagina. 


   ![Screenshot della pagina Dettagli app del sito Web Portale aziendale.](./media/intune-app-details-1907.png)  

## <a name="next-steps"></a>Passaggi successivi
Ulteriore assistenza? Contattare l'amministratore IT. Per informazioni sul contatto vedere il [sito Web del portale aziendale](https://go.microsoft.com/fwlink/?linkid=2010980).  
