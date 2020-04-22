---
title: Asset in Desktop Analytics
titleSuffix: Configuration Manager
description: Informazioni su dispositivi, driver e app in Desktop Analytics.
ms.date: 01/16/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: d07198cf-49bb-4712-8c63-063b4302cc11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fe1338781cbb16a8485de050a294e34e487a2ecc
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706649"
---
# <a name="assets-in-desktop-analytics"></a>Asset in Desktop Analytics

Dopo che i dispositivi hanno inviato i dati, Desktop Analytics offre un inventario degli asset seguenti:

- Dispositivi
- App installate  

Nel portale dei servizi selezionare **Asset** nel menu di Desktop Analytics.

## <a name="devices"></a>Dispositivi

La scheda **Dispositivi** visualizza le informazioni chiave su tutti i dispositivi dell'organizzazione registrati in Desktop Analytics. È possibile ordinare in base a qualsiasi colonna o applicare un filtro per determinati valori.

> [!NOTE]  
> Se la dashboard non visualizza il numero di dispositivi previsti per l'ambiente in uso, vedere [Risoluzione dei problemi di Desktop Analytics](troubleshooting.md).  

In un piano di distribuzione sono disponibili maggiori dettagli sui dispositivi. Per altre informazioni, vedere [Pianificare gli asset](about-deployment-plans.md#plan-assets)

## <a name="apps"></a>App

La scheda **App** mostra tutte le app installate che il servizio rileva nei dispositivi Windows.

Le app **importanti** sono installate in più del 2% dei dispositivi registrati.

Configurare l'**Importanza** delle app impostando una delle categorie seguenti:

- Critico
- Importante
- Ignora
- Verifica non effettuata
- Non importante<!-- 3587232 -->

Selezionare l'app dall'elenco e selezionare **Modifica**. Questa azione visualizza i dettagli per l'app. Selezionare il menu a discesa **Importanza** e impostare un valore. È anche possibile assegnare un **Proprietario**. Se si apportano modifiche, selezionare **Salva**.

### <a name="automatic-upgrade-decision-of-system-and-store-apps"></a><a name="bkmk_plan-autoapp" /> Decisione di aggiornamento automatico delle app di sistema e dello Store

<!-- 3587232 -->
Identificare l'**Importanza** e la **Decisione di aggiornamento** è fondamentale per tutte le app importanti nel flusso di lavoro di Desktop Analytics. Per facilitare l'annotazione di queste app, alcuni tipi di app vengono contrassegnati automaticamente come *Non importante*. La decisione di aggiornamento del piano di distribuzione per queste app è contrassegnata anche con *Pronto*. Le app seguenti sono compatibili e continueranno a funzionare dopo l'aggiornamento di Windows:

- App di sistema e componenti pubblicati da Microsoft

- App gestite e aggiornate da Microsoft Store

> [!TIP]
> Gestire gli input per qualsiasi app a livello globale o in base al piano di distribuzione.
>
> 1. Nel portale di Desktop Analytics nel menu **Gestisci** selezionare **Asset**. Quindi selezionare **App**.
>
> 2. Usare le colonne **Tipo** e **Categoria** per gestire queste categorie di app:
>
>    - Per le app dello Store, applicare il filtro **Moderno** a **Tipo**
>    - Per le app di sistema, applicare il filtro **Processo in background** o **Componente di Windows** a **Categoria**

In un piano di distribuzione è anche possibile impostare la **Decisione di aggiornamento**. Per altre informazioni, vedere [Pianificare gli asset](about-deployment-plans.md#plan-assets)

### <a name="usage"></a>Utilizzo

<!-- 5533890 -->

- **Totale installazioni**: questo valore indica il numero di installazioni dell'app selezionata in tutti i dispositivi registrati per Desktop Analytics.

- **Percentuale di installazione**: questo valore è la percentuale di installazione dell'app selezionata rispetto a tutti i dispositivi registrati per Desktop Analytics.

- **I dispositivi hanno avviato questa app negli ultimi 30 giorni**: questo valore corrisponde al numero di dispositivi in cui un utente ha avviato l'app selezionata. Include solo i dispositivi che hanno segnalato l'utilizzo negli ultimi 30 giorni. Questo conteggio è riferito a tutti i dispositivi registrati per Desktop Analytics in esecuzione in qualsiasi versione di Windows 10. Questo conteggio potrebbe variare per un piano di distribuzione.

## <a name="next-steps"></a>Passaggi successivi

- [Informazioni sui piani di distribuzione di Desktop Analytics](about-deployment-plans.md)  

- [Informazioni sugli aggiornamenti della sicurezza e delle funzionalità](about-updates.md)  

- [Valutazione della compatibilità in Desktop Analytics](compat-assessment.md)  
