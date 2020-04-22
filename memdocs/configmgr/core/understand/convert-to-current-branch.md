---
title: Aggiornare LTSB a Current Branch
titleSuffix: Configuration Manager
description: Informazioni su come convertire un sito LTSB (Long-Term Servicing Branch) in un sito Current Branch.
ms.date: 02/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ec5b54cf-62b7-4ed1-9bb3-e8c63b9641c8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b9f79eae1eee29fee33a9a841a303aae55686c55
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707229"
---
# <a name="upgrade-the-long-term-servicing-branch-to-the-current-branch"></a>Aggiornare Long-Term Servicing Branch a Current Branch

*Si applica a: System Center Configuration Manager (Long-Term Servicing Branch)*

Questo argomento illustra come aggiornare (convertire) un sito e una gerarchia che eseguono Long-Term Servicing Branch (LBTS) di Configuration Manager in Current Branch.

Se si è dotati di un contratto Software Assurance (o di diritti di licenza simili) in vigore, che concede il diritto di utilizzare Current Branch, è possibile convertire l'installazione di LTSB in Current Branch.  La conversione è mono direzionale poiché non viene offerto alcun supporto per convertire un sito Current Branch in LTSB.

Se si dispone di più siti, è sufficiente convertire il sito di livello superiore della gerarchia. Dopo aver convertito il sito di livello superiore:
- I siti primari figlio vengono convertiti automaticamente.
- È necessario aggiornare manualmente i siti secondari dalla console di Configuration Manager.

## <a name="run-setup-to-convert-the-long-term-servicing-branch"></a>Eseguire il programma di installazione per convertire Long-Term Servicing Branch
Nel sito di livello più alto della gerarchia è possibile eseguire l'installazione di Configuration Manager dal supporto di base originale e selezionare **Manutenzione sito**.  Quando viene visualizzata la pagina di gestione delle licenze, selezionare l'opzione Current Branch e completare la procedura guidata.

Quando il sito è stato convertito in Current Branch, è possibile usare le funzionalità e le caratteristiche precedentemente non disponibili.

> [!NOTE]  
> Un supporto di base valido presenta una versione uguale o successiva rispetto a quella dell'installazione LTSB.

Ad esempio, poiché LTSB è basato sulla versione 1606, non è possibile usare il supporto di base 1511 per eseguire la conversione a Current Branch. In questo caso, l'installazione viene eseguita dallo stesso supporto di base della versione 1606 usato per installare il sito LTSB, scegliendo l'opzione di gestione delle licenze relativa a Current Branch.  In alternativa, se è stata rilasciata una versione di base successiva di Current Branch, è possibile eseguire il programma di installazione da tale supporto di base.

Per un elenco delle versioni di base, vedere **Versioni di base e di aggiornamento** in [Updates for Configuration Manager](../servers/manage/updates.md) (Aggiornamenti per Configuration Manager).

## <a name="use-the-configuration-manager-console-to-convert-the-long-term-servicing-branch"></a>Usare la console di Configuration Manager per convertire Long Term Servicing Branch
Se il sito esegue LTSB, è possibile usare l'opzione seguente nella console di Configuration Manager per eseguire la conversione in Current Branch:

 1. Nella console passare ad **Amministrazione** > **Configurazione del sito** > **Siti** e quindi aprire **Impostazioni gerarchia**.  

 2. In **Impostazioni gerarchia** passare alla scheda **Licenze**. Selezionare l'opzione **Converti a Current Branch** e quindi scegliere **Applica**.  

Quando il sito è stato convertito in Current Branch, è possibile usare le funzionalità e le caratteristiche precedentemente non disponibili.
