---
title: Domande frequenti sui dati di diagnostica e di utilizzo
titleSuffix: Configuration Manager
description: Domande frequenti sui dati di diagnostica e di utilizzo per Configuration Manager
ms.date: 01/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3fe32aa2-d594-4ad0-a291-b8f5395ac50b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 60634ed8e275ff8496a08969054aa912a81b9d07
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688479"
---
# <a name="frequently-asked-questions-about-diagnostics-and-usage-data"></a>Domande frequenti sui dati di diagnostica e di utilizzo

*Si applica a: Configuration Manager (Current Branch)*

Questo articolo fornisce le risposte alle domande frequenti sui dati di diagnostica e di utilizzo in Configuration Manager.

## <a name="can-i-turn-off-diagnostic-and-usage-data"></a><a name="bkmk_off"></a> È possibile disattivare i dati di diagnostica e di utilizzo?

Per semplificare la gestione quando il sito invia dati, usare il punto di connessione del servizio in modalità offline. Usare quindi lo strumento di connessione del servizio per inviare manualmente i dati. Per altre informazioni, vedere gli articoli seguenti:

- [Informazioni sul punto di connessione del servizio](../../servers/deploy/configure/about-the-service-connection-point.md)
- [Usare lo strumento di connessione del servizio](../../servers/manage/use-the-service-connection-tool.md)

Per supportare le nuove versioni di Windows 10 e dei servizi cloud come Microsoft Intune, è necessario aggiornare regolarmente la versione Current Branch of Configuration Manager. Microsoft richiede almeno il livello base dei dati di diagnostica e di utilizzo. Questi dati vengono usati per mantenere aggiornato il prodotto, migliorare l'esperienza di aggiornamento e aumentare la qualità e la sicurezza del prodotto.

Nessun dato viene inviato al servizio quando il punto di connessione del servizio è in modalità offline. Quando si passa alla modalità online o si usa lo strumento di connessione del servizio, i dati vengono inviati al servizio per verificare la disponibilità di aggiornamenti.

È anche possibile scegliere il livello di dati raccolti da Configuration Manager. Per altre informazioni, vedere [Livelli dei dati di diagnostica e utilizzo](levels-overview.md).

## <a name="what-is-the-data-retention-period"></a><a name="bkmk_retention"></a> Qual è il periodo di conservazione dei dati?

Microsoft archivia i dati di diagnostica e di utilizzo di Configuration Manager per un anno.

## <a name="is-diagnostics-and-usage-data-sent-when-setup-runs"></a><a name="bkmk_update"></a> I dati di diagnostica e di utilizzo vengono inviati durante l'esecuzione del programma di installazione?

No. I dati di diagnostica e di utilizzo vengono inviati solo dopo che il sito è installato e funzionante.

## <a name="how-frequently-is-the-data-sent"></a><a name="bkmk_frequency"></a> Con quale frequenza vengono inviati i dati?

Le stored procedure SQL vengono eseguite ogni sette giorni dalla data di installazione del sito.

- In modalità online, il punto di connessione del servizio carica i dati dopo l'esecuzione delle query.

- In modalità offline è possibile usare lo strumento di connessione del servizio per caricare i dati. I dati non sono inizialmente disponibili per l'uso offline fino a sette giorni dopo l'installazione del sito.  

## <a name="can-the-data-be-used-to-form-a-network-map"></a><a name="bkmk_network"></a> È possibile usare i dati per formare una mappa di rete?

No. Tali dati non includono dettagli relativi alla rete, ad esempio indirizzi IP o informazioni geografiche dettagliate. Per altre informazioni, vedere [Livelli dei dati di diagnostica e di utilizzo](levels-overview.md#bkmk_versions) e trovare ulteriori dettagli per la versione in uso.

I dati includono informazioni sul fuso orario da ogni sito. Queste informazioni possono fornire indicazioni riguardo la georilevazione generale e la dispersione globale dei siti in una gerarchia.

## <a name="can-you-see-data-in-custom-sql-tables"></a><a name="bkmk_tables"></a> È possibile visualizzare i dati in tabelle SQL personalizzate?

No. Configuration Manager raccoglie i dati di diagnostica e di utilizzo tramite stored procedure SQL che vengono eseguite per tabelle di prodotti predefinite nel database. Tutte queste tabelle SQL sono precedute dal prefisso **TEL_** . Come parte della query di rilevamento dello schema SQL, viene eseguito l'hashing di tutti i nomi di tabella per il confronto con i valori predefiniti noti. Questo comportamento determina l'esistenza di tabelle personalizzate nel database. La presenza di tabelle personalizzate indica a Microsoft che è stato esteso lo schema di database rispetto all'impostazione predefinita. Non include i dati archiviati all'interno di tali tabelle.

## <a name="can-you-see-other-databases"></a><a name="bkmk_databases"></a> È possibile visualizzare altri database?

No. Le stored procedure per raccogliere i dati sono limitate al database del sito di Configuration Manager. Microsoft non può visualizzare i nomi di altri database o dati in altri database.

## <a name="is-any-data-sent-to-other-integrated-cloud-services"></a><a name="bkmk_cloud"></a> I dati vengono inviati ad altri servizi cloud integrati?

Sì, quando si integrano i servizi con Configuration Manager. Nell'ambito dell'interazione con qualsiasi servizio cloud, Configuration Manager invia alcuni dati a tale servizio. Questi dati sono specifici del servizio cloud e si differenziano dai dati di diagnostica e di utilizzo di Configuration Manager. Per altre informazioni sui dati specifici usati nell'interazione con un altro servizio cloud, vedere la documentazione relativa a tale servizio.

I servizi cloud seguenti, ad esempio, fanno parte di Microsoft Endpoint Manager:

- [Privacy dei dati di Desktop Analytics](../../../desktop-analytics/privacy.md)
- [Privacy e dati personali in Intune](https://docs.microsoft.com/intune/protect/privacy-personal-data)
- [Requisiti di Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot-requirements)

## <a name="does-configuration-manager-collect-any-personal-data"></a><a name="bkmk_personal"></a> Configuration Manager raccoglie dati personali?

No. Configuration Manager non raccoglie né trasmette dati personali o dati dei clienti. È un prodotto locale che è possibile distribuire, gestire e usare direttamente. I dati di diagnostica e di utilizzo che Microsoft raccoglie migliorano l'esperienza, la qualità e la sicurezza di installazione delle versioni future.

Per altre informazioni sui dati di Configuration Manager, vedere [Livelli dei dati di diagnostica e utilizzo](levels-overview.md).
