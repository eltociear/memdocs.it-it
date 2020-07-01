---
title: Hub della community e GitHub
titleSuffix: Configuration Manager
description: Abilitare e usare l'hub della community di Configuration Manager
ms.date: 06/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 88cead9a-64fe-471e-b57c-81707cefe46c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e0ef065cce691ce6f0b251d70ea8c4bd08904071
ms.sourcegitcommit: 9a8a9cc7dcb6ca333b87e89e6b325f40864e4ad8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/12/2020
ms.locfileid: "84740793"
---
# <a name="community-hub-and-github"></a>Hub della community e GitHub
<!--3555935, 3555936-->

La community di amministratori IT ha sviluppato un patrimonio di conoscenze nel corso degli anni. Per offrire agli amministratori IT la possibilità di condividere le loro esperienze, evitando di reinventare da zero elementi come script e report, abbiamo creato l'**Hub della community di Configuration Manager**. Sfruttando il lavoro degli altri, è possibile risparmiare diverse ore di lavoro. L'hub della community incentiva la creatività offrendo la possibilità di condividere reciprocamente con gli altri i risultati del proprio lavoro. GitHub include già processi e strumenti a livello di settore destinati alla condivisione. Ora tramite l'hub della community questi strumenti potranno essere usati direttamente nella console di Configuration Manager come basi per lo sviluppo di questa nuova community. Per la versione iniziale, il contenuto reso disponibile nell'hub della community verrà caricato solo da Microsoft. In futuro gli amministratori IT potranno caricare il contenuto autonomamente usando il proprio account GitHub.

> [!Note]  
> L'hub della community è una funzionalità facoltativa basata sul cloud, introdotta per la prima volta nel giugno del 2020. Per informazioni su come acconsentire esplicitamente all'hub della community, vedere [Funzionalità facoltative](install-in-console-updates.md#bkmk_options).

## <a name="about-community-hub"></a>Informazioni sull'hub della community

L'hub della community supporta gli oggetti seguenti:
- Script di PowerShell
- Report
- Sequenze attività
- Applicazioni
- Elementi di configurazione  

## <a name="prerequisites"></a>Prerequisiti

- Il dispositivo che esegue la console di Configuration Manager usato per accedere all'hub della community deve soddisfare i requisiti seguenti:
   - .NET Framework versione 4.6 o successiva
   - Windows 10 build 17110 o versione successiva
      - Windows Server non è supportato, pertanto è necessario installare la console di Configuration Manager in un dispositivo Windows 10 separato dal server del sito.
   - L'account utente connesso non può essere l'account amministratore predefinito

- Per scaricare i report, è necessario attivare l'opzione **Usa i certificati generati da Configuration Manager per sistemi del sito HTTP** nel sito in cui viene eseguita l'importazione. Per altre informazioni, vedere [HTTP migliorato](/sccm/core/plan-design/hierarchy/enhanced-http).
   1. Passare ad **Amministrazione** > **Configurazione del sito** > **Siti**.
   1. Selezionare il sito e scegliere **Proprietà** nella barra multifunzione.
   1. Nella scheda **Sicurezza delle comunicazioni** selezionare l'opzione **Usa i certificati generati da Configuration Manager per sistemi del sito HTTP**.

- Se l'organizzazione limita le comunicazioni della rete con Internet tramite un firewall o un dispositivo proxy, è necessario consentire alla console di Configuration Manager di accedere agli endpoint Internet. Per altre informazioni, vedere i [requisiti di accesso Internet](../../plan-design/network/internet-endpoints.md#community-hub).

## <a name="permissions"></a>Autorizzazioni

- Per importare uno script: autorizzazione di **creazione** per la classe **SMS_Scripts**.
- Per importare un report: ruolo di sicurezza Amministratore completo.


## <a name="use-the-community-hub"></a>Usare l'hub della community

1. Passare al nodo **Hub della community** dell'area di lavoro **Community**.
1. Selezionare un elemento da scaricare.
1. Per scaricare oggetti dall'hub e importarli nel sito, è necessario avere le autorizzazioni appropriate nel sito di Configuration Manager.
    - Per importare uno script: autorizzazione di **creazione** per la classe SMS_Scripts.
    - Per importare un report: ruolo di sicurezza Amministratore completo.
1. I report scaricati vengono distribuiti in una cartella denominata **hub** nel punto di Reporting Services. Gli script scaricati possono essere visualizzati nel nodo **Esegui script**.
1. Per visualizzare tutti gli elementi scaricati dall'hub dalla propria organizzazione, fare clic su **Your downloads** (Download) dal nodo **Hub della community**.

[![Tutti gli elementi scaricati dall'hub della community](./media/3555935-community-hub-downloads.png)](./media/3555935-community-hub-downloads.png#lightbox)


## <a name="next-steps"></a>Passaggi successivi

Altre informazioni sulla creazione e l'uso degli oggetti seguenti:

- [Creare ed eseguire script di PowerShell](../../../apps/deploy-use/create-deploy-scripts.md)
- [Introduzione alla creazione di report](introduction-to-reporting.md)
- [Creare e gestire le sequenze di attività](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md)
- [Creare e distribuire un'applicazione](../../../apps/get-started/create-and-deploy-an-application.md)
- [Creare elementi di configurazione](../../../compliance/deploy-use/create-configuration-items.md)