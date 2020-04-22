---
title: Uso dei dati di diagnostica
titleSuffix: Configuration Manager
description: Informazioni sulla modalità di impiego presso Microsoft dei dati di diagnostica e di utilizzo raccolti da Configuration Manager.
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a8021bc8-2799-41f4-83c2-e27d1242028c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f6a014d60c49b0ff7e10cd74c101294dd002266d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697129"
---
# <a name="how-microsoft-uses-configuration-manager-diagnostics-and-usage-data"></a>Come Microsoft usa i dati di diagnostica e di utilizzo di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

I dati di diagnostica e di utilizzo raccolti da Configuration Manager offrono un feedback quasi immediato a Microsoft sul funzionamento del prodotto e vengono usati per adeguare gli aggiornamenti futuri. Microsoft può anche vedere dati di configurazione utili per progettare e testare le configurazioni usate in produzione. Ad esempio:

- Versioni dei server Windows usate nei server del sito

- Language Pack installati

- Differenziale dello schema SQL rispetto all'impostazione predefinita del prodotto

Questi dati consentono al team di progettazione di pianificare test futuri per garantire un'esperienza ottimale con le configurazioni più comuni. Questi dati sono fondamentali per adattarsi rapidamente e adottare un ciclo di rilascio frequente.

Altrettanto importante è comprendere in quali situazioni questi dati non vengono usati. Microsoft non usa questi dati per:

- Controlli delle licenze, ad esempio per confrontare l'utilizzo di una licenza da parte dell'utente rispetto al contratto stipulato

- Controllo dei prodotti non supportati

- Pubblicità basata sui dati disponibili, ad esempio l'utilizzo delle funzionalità o la georilevazione (fuso orario)

Microsoft usa i dati disponibili per migliorare il prodotto. Ad esempio:

- Il supporto iniziale offerto da Configuration Manager Current Branch limitava la tempistica di supporto per Windows Server 2008 R2. Microsoft ha esaminato i dati di utilizzo dei clienti che hanno eseguito l'aggiornamento a Configuration Manager Current Branch e ha quindi identificato la necessità di modificare ed estendere questa tempistica allo scopo di supportare i clienti che usano ancora questo sistema operativo.

- Microsoft ha migliorato i controlli dei prerequisiti per l'installazione di un aggiornamento. Sono state rimosse regole obsolete, si è tenuto conto di ulteriori casi e sono stati risolti automaticamente alcuni problemi.  

> [!div class="nextstepaction"]
> [Come Configuration Manager raccoglie i dati](how-diagnostics-and-usage-data-is-collected.md)
