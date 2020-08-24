---
title: Livelli dei dati di diagnostica e utilizzo
titleSuffix: Configuration Manager
description: Informazioni sui livelli dei dati di diagnostica e di utilizzo raccolti da Configuration Manager
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 3c46bdb2-5bda-47c8-b5f4-9365a4b3521c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0d27e4a2f82de75cde853f3ce95c98ea8a12c465
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126506"
---
# <a name="levels-of-diagnostic-usage-data"></a>Livelli dei dati di diagnostica e utilizzo

*Si applica a: Configuration Manager (Current Branch)*

Configuration Manager raccoglie tre livelli di dati di diagnostica e utilizzo: **Di base**, **Avanzato** e **Completo**. Per impostazione predefinita, per questa funzionalità è impostato il livello avanzato.

> [!IMPORTANT]
> Configuration Manager non raccoglie codici del sito, nomi di siti, indirizzi IP, nomi utente, nomi di computer, indirizzi fisici o indirizzi di posta elettronica per i livelli di base e avanzato. Qualsiasi raccolta di queste informazioni al livello Completo non è intenzionale. Tali informazioni sono infatti potenzialmente incluse nelle informazioni diagnostiche avanzate quali i file di log o gli snapshot di memoria. Le informazioni eventualmente raccolte non vengono usate da Microsoft per identificare l'utente, contattare l'utente o per fini pubblicitari.

## <a name="levels"></a>Livelli

### <a name="basic"></a>Di base

Il livello Di base include i dati sulla gerarchia. È necessario per migliorare l'esperienza di installazione o aggiornamento. Questi dati consentono inoltre di determinare gli aggiornamenti di Configuration Manager applicabili per la gerarchia.

### <a name="enhanced"></a>Avanzato

Il livello avanzato è quello predefinito dopo l'installazione. Questo livello include dati raccolti nel livello Di base e dati specifici delle funzionalità. Mostra la frequenza e la durata di utilizzo delle diverse funzionalità. Include anche i dati delle impostazioni client di Configuration Manager: nome del componente, stato e alcune impostazioni come intervalli di polling. Le informazioni sugli aggiornamenti software si limitano all'utilizzo delle funzionalità, ma non includono i dati sulla conformità degli aggiornamenti a questo livello.

Microsoft consiglia di adottare questo livello, perché contiene la quantità minima di dati considerata necessaria per migliorare prodotti e servizi.

Di seguito sono riportati alcuni esempi di dati non raccolti con questo livello:

- Nomi di siti, utenti, computer o altri oggetti

- Dettagli degli oggetti correlati alla sicurezza

- Vulnerabilità come il numero di sistemi che richiedono aggiornamenti software

### <a name="full"></a>Completo

Il livello completo include tutti i dati dei livelli di base e avanzato. Include inoltre informazioni aggiuntive su Endpoint Protection, le percentuali di conformità degli aggiornamenti e informazioni sugli aggiornamenti software. Questo livello può includere anche informazioni di diagnostica avanzate, ad esempio file di sistema e snapshot di memoria. Questi dati avanzati possono contenere informazioni personali presenti in memoria o file di registro esistenti al momento dell'acquisizione.

## <a name="how-to-change-the-level"></a><a name="bkmk_change"></a> Come cambiare il livello

Per modificare il livello di raccolta dati, è necessario disporre di autorizzazioni **Modifica** per la classe oggetto **Site**.

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito** e selezionare **Siti**.
1. Selezionare **Impostazioni gerarchia** sulla barra multifunzione.
1. Passare alla scheda **Dati di utilizzo e di diagnostica** e quindi scegliere il livello di dati.

## <a name="version-specific-details"></a><a name="bkmk_versions"></a> Dettagli specifici della versione

Gli articoli seguenti illustrano in dettaglio i dati specifici raccolti da Configuration Manager a ogni livello con ogni versione supportata:

- [Dati di diagnostica e utilizzo per la versione 2006](levels-of-diagnostic-usage-data-collection-2006.md)
- [Dati di diagnostica e utilizzo per la versione 2002](levels-of-diagnostic-usage-data-collection-2002.md)
- [Dati di diagnostica e utilizzo per la versione 1910](levels-of-diagnostic-usage-data-collection-1910.md)
- [Dati di diagnostica e utilizzo per la versione 1906](levels-of-diagnostic-usage-data-collection-1906.md)
- [Dati di utilizzo e di diagnostica per la versione 1902](levels-of-diagnostic-usage-data-collection-1902.md)

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Domande frequenti](frequently-asked-questions.md)
