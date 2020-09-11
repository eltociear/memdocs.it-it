---
title: Importare i dati di configurazione
titleSuffix: Configuration Manager
description: È possibile importare i dati di configurazione se in un formato di file CAB e conformi allo schema SML (Service Modeling Language) supportato.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 309b9a09-a611-4ba2-90ab-dde51582cf87
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: 7d9760a49815b9eb33c7886f4d9a8f9637dedd21
ms.sourcegitcommit: 9f072da27aa64f46a9409470b5dac5bfac3a0fe5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2020
ms.locfileid: "89468312"
---
# <a name="import-configuration-data-with-configuration-manager"></a>Importare dati di configurazione con Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Oltre a creare linee base ed elementi di configurazione nella console di Configuration Manager, è possibile importare dati di configurazione se questi si trovano all'interno di file in formato CAB (con estensione cab) e sono conformi allo schema SML (Service Modeling Language) supportato. È possibile importare i dati di configurazione da:  

- Dati di configurazione di procedure consigliate (pacchetti di configurazione) scaricati dal sito Microsoft o da altri siti di fornitori di software.  

- Dati di configurazione esportati da System Center Configuration Manager 2012 e versioni successive.  

- Dati di configurazione creati esternamente e conformi allo schema SML.  

Quando si importa una linea di base di configurazione, il file CAB potrebbe includere anche alcuni o tutti gli elementi di configurazione a cui si fa riferimento nella linea di base. Durante il processo di importazione Configuration Manager verifica che tutti gli elementi di configurazione a cui si fa riferimento nella linea di base di configurazione siano inclusi anche nel file CAB o esistano già nel sito di Configuration Manager. Il processo di importazione ha esito negativo se si tenta di importare una linea di base di configurazione che fa riferimento a dati di configurazione che Configuration Manager non riesce a individuare.  

Di seguito sono descritti altri scenari in cui il processo di importazione potrebbe avere esito negativo.  

-   I dati di configurazione fanno riferimento a dati di configurazione che Configuration Manager non riesce a individuare nel proprio database né nel file CAB stesso.  

-   I dati di configurazione sono già presenti nel database di Configuration Manager con lo stesso nome e la stessa versione di dati di configurazione, ma con versione di contenuto diversa.  

-   I dati di configurazione sono già presenti nel database di Configuration Manager con la stessa versione di contenuto, che però il calcolo hash identifica come diversa.  

-   Una versione più recente dei dati di configurazione con lo stesso nome è già presente nel database di Configuration Manager o è stata eliminata recentemente da tale database.  

-   In una gerarchia di Configuration Manager multisito i dati di configurazione sono stati originariamente importati da un sito padre. È necessario aggiornare i dati dallo stesso sito e non da un sito figlio.  

### <a name="import-configuration-data"></a>Importare i dati di configurazione  

1.  Nella console di Configuration Manager fare clic su **Assets e conformità** > **Elementi di configurazione** o **Linee di base di configurazione**
2.  Nella scheda **Home**, nel gruppo **Crea**, fare clic su **Importa dati di configurazione**.  
3.  Nella pagina **Selezione file** dell' **Importazione guidata dei dati di configurazione**fare clic su **Aggiungi**e quindi nella finestra di dialogo **Apri** selezionare i file con estensione cab che si vogliono importare.  
4.  Selezionare la casella di controllo **Creare una nuova copia delle linee di base e degli elementi di configurazione importati** se si vuole che i dati di configurazione importati siano modificabili nella console di Configuration Manager.  
5.  Nella pagina **Riepilogo** esaminare le azioni da eseguire e quindi completare la procedura guidata.  

I dati di configurazione importati vengono visualizzati nel nodo **Impostazioni di conformità** dell'area di lavoro **Asset e conformità**.  
