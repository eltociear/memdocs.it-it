---
title: Updates Publisher
titleSuffix: Configuration Manager
description: Usare System Center Updates Publisher per gestire gli aggiornamenti personalizzati
ms.date: 11/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 2200b02b-e76b-4aa7-a77a-6dc5e70f1333
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: dc1e662eb8eca4740e70743d0971e2d65410f3f2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700029"
---
# <a name="system-center-updates-publisher"></a>System Center Updates Publisher

*Si applica a: System Center Updates Publisher*

System Center Updates Publisher (Updates Publisher) è uno strumento autonomo che consente ai fornitori di software indipendenti o agli sviluppatori di applicazioni line-of-business di gestire aggiornamenti personalizzati. Questa gestione personalizzata degli aggiornamenti include aggiornamenti con dipendenze, ad esempio i driver o le aggregazioni di aggiornamenti.

Updates Publisher consente di effettuare le operazioni seguenti:

-   Importare aggiornamenti da cataloghi esterni (cataloghi di aggiornamenti non Microsoft).
-   Modificare le definizioni di aggiornamento, incluse l'applicabilità e la distribuzione dei metadati.
-   Esportare aggiornamenti in cataloghi esterni.
-   Pubblicare aggiornamenti in un server di aggiornamento.

Dopo aver pubblicato aggiornamenti in un server di aggiornamento, è possibile usare Configuration Manager per rilevare e distribuire tali aggiornamenti ai dispositivi gestiti.

## <a name="workspaces"></a>Aree di lavoro
Quando si apre Updates Publisher, per impostazione predefinita viene visualizzato automaticamente il nodo Panoramica dell'*area di lavoro Aggiornamenti*.

![Console di Updates Publisher](media/console1.png)


Per organizzare Updates Publisher sono disponibili quattro aree di lavoro.


**Updates Workspace** (Area di lavoro Aggiornamenti): usare quest'area di lavoro per [creare](create-updates-with-updates-publisher.md) e [gestire](manage-updates-with-updates-publisher.md) aggiornamenti software e pacchetti di aggiornamenti. Questa area di lavoro include l'assegnazione di aggiornamenti e aggregazioni a una pubblicazione, nonché la pubblicazione e l'esportazione degli stessi in un altro repository di Updates Publisher.

**Publications Workspace** (Area di lavoro Pubblicazioni): usare quest'area di lavoro per [gestire le pubblicazioni](updates-publisher-publications.md). Una pubblicazione è gruppo di aggiornamenti creato per semplificare l'esportazione e la pubblicazione degli aggiornamenti stessi.

La gestione delle pubblicazioni include la pubblicazione di aggiornamenti in un server in modo che i client possano trovarli e installarli, l'esportazione di aggiornamenti e aggregazioni per l'uso da parte di altre installazioni di Updates Publisher e la modifica del contenuto o dei dettagli di una pubblicazione.

**Rules Workspace** (Area di lavoro Regole): usare quest'area per [gestire le regole di applicabilità](updates-publisher-applicability-rules.md) che è possibile salvare e quindi usare con gli aggiornamenti distribuiti. Esistono due tipi di regole:

-   Regole installabili: queste regole consentono di determinare se un client deve installare un aggiornamento.
-   Regole installate: queste regole verificano se un aggiornamento è già installato.

**Catalogs Workspace** (Area di lavoro Cataloghi): usare quest'area di lavoro per aggiungere e [gestire cataloghi di aggiornamenti software](updates-publisher-catalogs.md). Questa area di lavoro include l'importazione di aggiornamenti software da tali cataloghi nel repository di Updates Publisher.

## <a name="whats-new-in-system-center-updates-publisher"></a>Novità di System Center Updates Publisher

>[!NOTE] 
> La versione più recente di System Center Updates Publisher è stata rilasciata il 6 novembre 2019. Per altre informazioni, vedere la sezione sulla [Cronologia delle versioni](#release-history).

È disponibile una nuova modalità di creazione System Center Updates Publisher per facilitare la creazione degli aggiornamenti. Quando si abilita la modalità di creazione, viene aggiunta **un'area di lavoro categorie** alla schermata Start. Viene inoltre aggiunto un nuovo pulsante **Detectoid** all'**area di lavoro Aggiornamenti** quando è abilitata la modalità di creazione.

### <a name="to-enable-authoring-mode"></a>Per abilitare la modalità di creazione

1. Nell'angolo superiore sinistro della console fare clic sulla scheda **Updates Publisher** **Proprietà** e quindi scegliere **Opzioni**.
1. Passare alle opzioni **Creazione**.
1. Selezionare la casella per **abilitare la modalità di creazione**.

![Abilitare la modalità di creazione per Updates Publisher](media/scup-enable-authoring-mode.png)

### <a name="about-the-categories-workspace"></a>Informazioni sull'area di lavoro categorie

L'area di lavoro categorie consente agli autori degli aggiornamenti di organizzare gli aggiornamenti che rientrano in un unico gruppo. Ad esempio, se si è un OEM, potrebbe essere necessario organizzare gli aggiornamenti in base a modelli o linee di prodotti. È possibile definire più categorie e categorie figlio ma non le categorie figlio di figlio poiché vi è una limitazione a due livelli.

![Screenshot dell'area di lavoro Categorie](media/scup-categories-workspace.png)

### <a name="assign-an-update-to-a-category"></a>Assegnare un aggiornamento a una categoria

Dopo aver creato l'aggiornamento, è possibile assegnarlo a una categoria selezionando l'aggiornamento e quindi facendo clic sul pulsante **Categorizza**. È inoltre possibile fare clic con il pulsante destro del mouse sull'aggiornamento e scegliere **Categorizza**.

![Screenshot della categorizzazione di un aggiornamento](media/scup-categorize-update.png)

### <a name="about-detectoids"></a>Informazioni sui detectoid

Una volta abilitata la modalità di creazione, è possibile creare detectoid per gli aggiornamenti. I detectoid sono utili quando si hanno più aggiornamenti che usano la stessa regola (o una serie di regole) per determinare l'applicabilità. In queste istanze, è necessario creare un detectoid e assegnarlo come prerequisito per un aggiornamento. È possibile assegnare più detectoid a un aggiornamento creato.


### <a name="create-a-detectoid"></a>Creare un detectoid

1. Aprire l'**area di lavoro Aggiornamenti**.
1. Sulla barra multifunzione fare clic sul pulsante **Detectoid**.
1. Seguire le istruzioni della procedura guidata per creare il detectoid.



![Aggiornare i prerequisiti usando un detectoid](media/scup-detectoid-as-prerequisite.png)

## <a name="release-history"></a>Cronologia versioni

- [2019 RTW versione 6.0.394.0](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/SCUP-adds-support-for-update-categories/ba-p/990111). Data di rilascio: 6 novembre 2019
- [Aggiornamento cumulativo versione 6.0.283.0 da KB4462765](https://support.microsoft.com/help/4462765/update-rollup-for-system-center-updates-publisher). Data di rilascio: 7 settembre 2018
- [2017 RTW versione 6.0.276.0](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/System-Center-Updates-Publisher-adds-support-for-new-OSes/ba-p/274986). Data di rilascio: 26 marzo 2018


## <a name="next-steps"></a>Passaggi successivi
Per iniziare, [installare](install-updates-publisher.md), e quindi [configurare le opzioni](updates-publisher-options.md) per Updates Publisher.
