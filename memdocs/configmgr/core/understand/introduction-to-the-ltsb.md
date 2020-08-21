---
title: Introduzione a LTSB
titleSuffix: Configuration Manager
description: Informazioni su Long Term Servicing Branch di Configuration Manager.
ms.date: 08/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 694bc29f-a7fd-4e06-815a-1a9c5e9ac563
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1370c1bf80283ff30ad54378ad58ecd9a5d24d47
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699365"
---
# <a name="introduction-to-the-long-term-servicing-branch-of-configuration-manager"></a>Introduzione a Long Term Servicing Branch di Configuration Manager

*Si applica a: System Center Configuration Manager (Long-Term Servicing Branch)*

Long-Term Servicing Branch (LTSB) di Configuration Manager è un ramo distinto progettato come opzione di installazione disponibile per tutti i clienti. È tuttavia l'unica opzione disponibile per i clienti che hanno lasciato scadere Software Assurance o i diritti di sottoscrizione equivalenti per Configuration Manager.

In base a Configuration Manager versione 1606, LTSB offre funzionalità ridotte rispetto all'edizione Current Branch di Configuration Manager.

> [!TIP]   
> Configuration Manager LTSB non è correlato a Long-Term Servicing Channel (LTSC) della suite di System Center. Per altre informazioni, vedere [Panoramica delle opzioni di versione di System Center](/system-center/ltsc-and-sac-overview).

## <a name="features-that-arent-available"></a>Funzionalità non disponibili

Current Branch di Configuration Manager supporta le funzionalità seguenti, non disponibili quando si usa LTSB:

- Aggiornamenti nella console che aggiungono nuove funzionalità e miglioramenti.
- Supporto per sistemi operativi rilasciati di recente da usare come client e server del sito.
- Software MDM locale
- Dashboard di manutenzione di Windows 10 e i piani di manutenzione, incluso il supporto per le versioni recenti di Windows 10.  
- Supporto per versioni future di Windows Server e Windows 10 LTSB
- Asset Intelligence
- Punti di distribuzione basati su cloud
- Exchange Online come Exchange Connector    

Il supporto per queste funzionalità non è disponibile con LTSB. Alcune funzionalità, tuttavia, restano visibili nella console di Configuration Manager ma non possono essere selezionate o usate.

Le integrazioni cloud, così come tutte le funzionalità incluse nell'edizione Current Branch di Configuration Manager versione 1610 o versioni successive, non sono disponibili per LTSB. Queste funzionalità includono, tra le altre, quanto segue:<!--SCCMDocs#1823-->

- Co-gestione
- Desktop Analytics
- Gateway di gestione cloud
- Integrazione di Azure Active Directory
- App da Microsoft Store per le aziende

## <a name="find-ltsb-documentation"></a>Trovare la documentazione di LTSB

LTSB si basa su Current Branch versione 1606. Usare la [documentazione di Current Branch](../../index.yml) con le avvertenze e le limitazioni specifiche di LTSB. Tali avvertenze e limitazioni sono descritte negli articoli seguenti:

- [Installare LTSB](install-the-ltsb.md)
- [Aggiornare LTSB a Current Branch](convert-to-current-branch.md)
- [Configurazioni supportate per LTSB](supported-configurations-for-ltsb.md)
- [Gestire LTSB di Configuration Manager](manage-the-ltsb.md)

Quando si fa riferimento alla documentazione di Current Branch per LTSB, i dettagli validi per la versione 1606 o versioni precedenti sono validi anche per LTSB. Le funzionalità o i dettagli introdotti con la versione 1610 o con versioni successive non sono supportate da LTSB.

## <a name="licensing-overview-for-the-ltsb"></a>Panoramica della gestione delle licenze per LTSB   

I clienti con contratti Software Assurance attivi per le licenze di Configuration Manager, o con diritti di sottoscrizione equivalenti alla data 1 ottobre 2016, hanno diritto a usare la versione 1606 di ottobre 2016 di Configuration Manager. I clienti con diritti per Configuration Manager in data 1 ottobre 2016 o successiva, al momento dell'installazione avranno a disposizione due opzioni con licenza: Current Branch e Long-Term Servicing Branch (LTSB).

I clienti che dispongono di diritti perpetui su System Center Configuration Manager o che dopo il 1° ottobre lasciano scadere la sottoscrizione Software Assurance o equivalente possono installare la versione di System Center Configuration Manager LTSB corrente al momento della scadenza.

Per altre informazioni su queste licenze, vedere [I termini e le condizioni relativi ai prodotti acquistati tramite i programmi multilicenza Microsoft](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?mode=1).

Per altre informazioni sulla gestione delle licenze per i rami di Configuration Manager, vedere [Licenze e rami per Configuration Manager](learn-more-editions.md).

## <a name="next-steps"></a>Passaggi successivi

Se si decide che Configuration Manager LTSB è il ramo corretto per l'ambiente in uso, [installare un nuovo sito LTSB](install-the-ltsb.md#install-a-new-site) come parte di una nuova gerarchia o [aggiornare un sito e una gerarchia di System Center 2012 Configuration Manager](install-the-ltsb.md#upgrade-from-system-center-2012-configuration-manager).