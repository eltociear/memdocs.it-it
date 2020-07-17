---
title: Creare elementi di configurazione figlio
titleSuffix: Configuration Manager
description: Creare elementi di configurazione figlio in Configuration Manager
ms.date: 05/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 113984fa-6150-41a1-89ed-d2a83b979732
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: 319f673200244d4451b957dcb778ce378f9569fa
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240321"
---
# <a name="how-to-create-child-configuration-items-in-configuration-manager"></a>Come creare elementi di configurazione figlio in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Gli elementi di configurazione figlio in Configuration Manager sono copie di elementi di configurazione che mantengono una relazione con l'elemento di configurazione originale e che quindi ereditano la configurazione originale dall'elemento di configurazione padre.  

Quando si visualizzano le proprietà di un elemento di configurazione figlio nella console di Configuration Manager, non è possibile modificare le impostazioni e gli oggetti ereditati con i relativi criteri di convalida. Tuttavia, è possibile aggiungere e quindi modificare criteri di convalida aggiuntivi per l'elemento di configurazione figlio, al quale è anche possibile aggiungere nuovi oggetti e impostazioni.
Un esempio della creazione e della modifica di un elemento di configurazione figlio è di solito quello di ottimizzare l'elemento di configurazione originale per soddisfare i requisiti aziendali.  

> [!NOTE]  
>  È possibile creare elementi di configurazione figlio solo da elementi di configurazione del tipo **Windows desktop o server (personalizzato)** .  

## <a name="to-create-a-child-configuration-item"></a>Per creare un elemento di configurazione figlio  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità** > **Impostazioni di conformità** > **Elementi di configurazione**.  

3.  Nell'elenco **Elementi di configurazione** selezionare l'elemento di configurazione per il quale si vuole creare un elemento di configurazione figlio e quindi nel gruppo **Elemento di configurazione** della scheda **Home** fare clic su **Crea elemento di configurazione figlio**.  

4.  Nella pagina **Generale** della **Creazione guidata dell'elemento di configurazione figlio**è possibile scegliere la revisione specifica dell'elemento di configurazione padre da usare per creare l'elemento figlio. Gli altri passaggi di questa procedura guidata sono identici a quelli eseguiti per creare un elemento di configurazione standard. Per altre informazioni, vedere [Come creare elementi di configurazione personalizzati per computer desktop e server Windows](../../compliance/deploy-use/create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-client.md).  

5.  Completare la procedura guidata. Il nuovo elemento di configurazione figlio verrà visualizzato nell'elenco **Elementi di configurazione** .  
