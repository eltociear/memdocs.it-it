---
title: Client di interoperabilità estesa
titleSuffix: Configuration Manager
description: Informazioni sull'uso del client di interoperabilità estesa per il supporto a lungo termine di un client di Configuration Manager statico con un sito Current Branch.
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 600086d5-bd9e-4ac1-8ace-c7a62de80dc2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 61296321251be45cfa0449a3e4f21ba79a024753
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706979"
---
# <a name="use-the-configuration-manager-client-software-for-extended-interoperability-with-future-versions-of-a-current-branch-site"></a>Usare il software client del supporto di Configuration Manager per l'interoperabilità estesa con le versioni future di un sito Current Branch

*Si applica a: Configuration Manager (Current Branch)*  

I requisiti aziendali potrebbero non consentire di aggiornare regolarmente il client di Configuration Manager in alcuni dispositivi. Ad esempio, potrebbe essere necessario rispettare i criteri di gestione delle modifiche oppure potrebbe trattarsi di un dispositivo cruciale. Soddisfare queste esigenze installando un nuovo client per l'uso a lungo termine denominato client di interoperabilità estesa. Usare il client di interoperabilità estesa solo per dispositivi specifici che non possono essere aggiornati di frequente, come dispositivi POS o chiosco multimediale. Continuare a usare l'[aggiornamento client automatico](../clients/manage/upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate) per la maggior parte dei client.

## <a name="how-it-works"></a>Come funziona

In genere, quando si installa un nuovo [aggiornamento nella console](../servers/manage/install-in-console-updates.md) per Configuration Manager, il software client dei computer client si aggiorna automaticamente in modo da poter usare le nuove funzionalità. In questo scenario si esegue comunque l'aggiornamento alla versione Current Branch che riceve i nuovi aggiornamenti e funzionalità. La maggior parte dei dispositivi aggiorna il software client di Configuration Manager a ogni aggiornamento di versione installato. Tuttavia, in un subset di sistemi critici per i quali non si vogliono ricevere aggiornamenti del software client si installa il client di interoperabilità estesa. Questi client non installano il nuovo software client fino a quando in essi non viene distribuita in modo esplicito una nuova versione del software client.

## <a name="supported-versions"></a>Versioni supportate

Nella tabella seguente sono elencate le versioni del client di Configuration Manager supportate per questo scenario:

| Version | Data di disponibilità | Data di fine supporto |
|---------|---------|---------|
| 1902<br/>5.00.8790 | 27 marzo 2019 | Non prima del 27 marzo 2021 |
| 1802<br/>5.00.8634 | 1° maggio 2018 | Non prima del 1° maggio 2020 |
| 1606<br/>5.00.8412 | 18 novembre 2016 | 1° maggio 2019 |

> [!TIP]  
> Il client di interoperabilità estesa viene supportato per almeno due anni dalla data di rilascio. Per altre informazioni sulle date di rilascio, vedere [Supporto per le versioni Current Branch di Configuration Manager](../servers/manage/current-branch-versions-supported.md).  

Pianificare l'aggiornamento del client di interoperabilità estesa nei dispositivi gestiti con Current Branch prima della scadenza del supporto. A tale scopo è necessario scaricare una nuova versione del client da Microsoft e quindi distribuire il software client aggiornato ai dispositivi che usano il client di interoperabilità estesa.

## <a name="how-to-use-the-eic"></a>Come usare il client di interoperabilità estesa

1. Aggiungere questi dispositivi a una raccolta ed escludere la raccolta dagli aggiornamenti automatici del client. Per altre informazioni, vedere [Come evitare l'aggiornamento dei client](../clients/manage/upgrade/exclude-clients-windows.md).  

1. Ottenere una versione supportata del client di interoperabilità estesa dalla cartella `\SMSSETUP\Client` del supporto di installazione dell'aggiornamento di Configuration Manager. Assicurarsi di copiare l'intero contenuto della cartella.  

    > [!TIP]  
    > Per trovare i supporti di Configuration Manager nel [Centro servizi per contratti multilicenza](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx), passare alla scheda **Downloads and Keys** (Download e codici), cercare `System Center Config` e quindi selezionare **System Center Config Mgr (Current Branch)** .

1. Installare manualmente il client di interoperabilità estesa in tali dispositivi. Per altre informazioni, vedere [Installare manualmente il client](../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual).  

    > [!Important]  
    > Quando si esegue l'aggiornamento dei client dalla versione 1606 alla versione 1802, usare l'opzione CCMSETUP **/AlwaysExcludeUpgrade:True**. In caso contrario, il client può ricevere criteri dal punto di gestione per l'aggiornamento automatico prima dei criteri di esclusione.  

## <a name="limitations"></a>Limitazioni

- Gli aggiornamenti per il software client di interoperabilità estesa non sono disponibili tramite gli aggiornamenti nella console. Per altre informazioni su come aggiornare il client di interoperabilità estesa, vedere [Come aggiornare un client escluso](../clients/manage/upgrade/exclude-clients-windows.md#bkmk_override).  

- Il client di interoperabilità estesa supporta solo le funzionalità seguenti:  

  - Aggiornamenti software  
  - Inventario hardware e software
  - Pacchetti e programmi

## <a name="next-steps"></a>Passaggi successivi

[Come evitare l'aggiornamento dei client](../clients/manage/upgrade/exclude-clients-windows.md)

Per verificare che i client siano installati correttamente nei dispositivi, vedere [Come monitorare i client](../clients/manage/monitor-clients.md).
