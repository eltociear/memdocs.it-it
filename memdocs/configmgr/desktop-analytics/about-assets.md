---
title: Asset in Desktop Analytics
titleSuffix: Configuration Manager
description: Informazioni su dispositivi, driver e app in Desktop Analytics.
ms.date: 08/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: d07198cf-49bb-4712-8c63-063b4302cc11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: d4328aee2bc08054fbeaa7147ceed30fe61b61a7
ms.sourcegitcommit: 62b451396eae660f2d5289ae3666b19ed1cc666d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/19/2020
ms.locfileid: "88614814"
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

> [!TIP]
> Per un piano di distribuzione specifico, è possibile configurare questo valore. Nelle proprietà di un piano di distribuzione, in **Regole di idoneità**, specificare il valore per **Definire una soglia di numero di installazioni basso per le proprie app**.

L'impostazione **Dettagli delle versioni dell'app** è disattivata per impostazione predefinita. Questa scheda, quindi, combina tutte le versioni delle app con lo stesso nome e lo stesso autore.<!-- 5542186 --> Il comportamento predefinito contribuisce a ridurre il numero totale di app visualizzate, consentendo di ridurre l'impegno richiesto per l'annotazione delle app. Il numero di app nel riquadro **App degne di nota** riflette anche questa impostazione. Ad esempio, anziché un elenco di centinaia di istanze di Microsoft Edge, è presente una sola istanza per tutte le versioni. È possibile prendere decisioni una volta per tutte le versioni. Se è necessario prendere decisioni per versioni specifiche di un'app, attivare questa impostazione. È possibile configurare questa impostazione anche quando si lavora con un piano di distribuzione. Per altre informazioni, vedere [Risorse del piano](about-deployment-plans.md#plan-assets).

Selezionare l'app dall'elenco e selezionare **Modifica**. Questa azione visualizza i dettagli per l'app. Selezionare il menu a discesa **Importanza** e impostare un valore. È anche possibile assegnare un **Proprietario**. Se si apportano modifiche, selezionare **Salva**.

Configurare l'**Importanza** delle app impostando una delle categorie seguenti:

- Critico
- Importante
- Ignora
- Verifica non effettuata
- Non importante<!-- 3587232 -->

> [!NOTE]
> Se si distribuisce l'app con Configuration Manager, Desktop Analytics la configura automaticamente come **importante** per impostazione predefinita. Questo comportamento consente di configurare più rapidamente le app nell'ambiente per accelerare il percorso verso una distribuzione di produzione.<!-- 4859763 -->

Quando l'impostazione **Dettagli delle versioni dell'app** è disattivata, il riquadro dei dettagli dell'app visualizza il numero di versioni e lingue delle app combinate. Se si salvano eventuali modifiche apportate ai dettagli dell'app, queste vengono applicate a tutte le versioni. Impostare, ad esempio, **Importanza** o **Proprietario**. Alcuni valori visualizzano "Più valori", che significa che non è presente un solo valore coerente in tutte le versioni.

### <a name="automatic-upgrade-decision-of-system-and-store-apps"></a><a name="bkmk_plan-autoapp"> </a> Decisione di aggiornamento automatico delle app di sistema e dello Store

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

In un piano di distribuzione è anche possibile impostare la **Decisione di aggiornamento**. Per altre informazioni, vedere [Risorse del piano](about-deployment-plans.md#plan-assets).

### <a name="usage"></a>Utilizzo

<!-- 5533890 -->

- **Totale installazioni**: questo valore indica il numero di installazioni dell'app selezionata in tutti i dispositivi registrati per Desktop Analytics.

- **Percentuale di installazione**: questo valore è la percentuale di installazione dell'app selezionata rispetto a tutti i dispositivi registrati per Desktop Analytics.

- **I dispositivi hanno avviato questa app negli ultimi 30 giorni**: questo valore corrisponde al numero di dispositivi in cui un utente ha avviato l'app selezionata. Include solo i dispositivi che hanno segnalato l'utilizzo negli ultimi 30 giorni. Questo conteggio è riferito a tutti i dispositivi registrati per Desktop Analytics in esecuzione in qualsiasi versione di Windows 10. Questo conteggio potrebbe variare per un piano di distribuzione.

## <a name="next-steps"></a>Passaggi successivi

- [Informazioni sui piani di distribuzione di Desktop Analytics](about-deployment-plans.md)  

- [Informazioni sugli aggiornamenti della sicurezza e delle funzionalità](about-updates.md)  

- [Valutazione della compatibilità in Desktop Analytics](compat-assessment.md)  
