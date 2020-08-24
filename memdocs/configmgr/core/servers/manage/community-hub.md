---
title: Hub della community e GitHub
titleSuffix: Configuration Manager
description: Abilitare e usare l'hub della community di Configuration Manager
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 88cead9a-64fe-471e-b57c-81707cefe46c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ae0abdd4a159759037768c8f27d5643bdf612f6e
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128172"
---
# <a name="community-hub-and-github"></a>Hub della community e GitHub
<!--3555935, 3555936-->

La community di amministratori IT ha sviluppato un patrimonio di conoscenze nel corso degli anni. Per offrire agli amministratori IT la possibilità di condividere le loro esperienze, evitando di reinventare da zero elementi come script e report, abbiamo creato l'**Hub della community di Configuration Manager**. Sfruttando il lavoro degli altri, è possibile risparmiare diverse ore di lavoro. L'hub della community incentiva la creatività offrendo la possibilità di condividere reciprocamente con gli altri i risultati del proprio lavoro. GitHub include già processi e strumenti a livello di settore destinati alla condivisione. Ora tramite l'hub della community questi strumenti potranno essere usati direttamente nella console di Configuration Manager come basi per lo sviluppo di questa nuova community. Per la versione iniziale, il contenuto reso disponibile nell'hub della community verrà caricato solo da Microsoft. In futuro gli amministratori IT potranno caricare il contenuto autonomamente usando il proprio account GitHub.

> [!Note]  
> L'hub della community è una funzionalità facoltativa basata sul cloud, introdotta per la prima volta nel giugno del 2020. Per informazioni su come acconsentire esplicitamente all'hub della community, vedere [Funzionalità facoltative](install-in-console-updates.md#bkmk_options).

## <a name="about-community-hub"></a>Informazioni sull'hub della community

L'hub della community supporta gli oggetti seguenti:

- Query CMPivot
- Applicazioni
- Sequenze attività
- Elementi di configurazione
- Script di PowerShell
- Report

## <a name="prerequisites"></a>Prerequisiti

- Il dispositivo che esegue la console di Configuration Manager usato per accedere all'hub della community deve soddisfare i requisiti seguenti:
   - .NET Framework versione 4.6 o successiva
   - Windows 10 build 17110 o versione successiva
      - Windows Server non è supportato, pertanto è necessario installare la console di Configuration Manager in un dispositivo Windows 10 separato dal server del sito.
   - L'account utente connesso non può essere l'account amministratore predefinito

- Il [servizio di amministrazione](../../../develop/adminservice/set-up.md) in Configuration Manager deve essere configurato e funzionante.

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


## <a name="direct-links-to-community-hub-items"></a><a name="bkmk_deeplink"></a> Collegamenti diretti agli elementi dell'hub della community
<!--4224406-->
*(Introdotto nella versione 2006)* È possibile esplorare facilmente e fare riferimento a elementi nel nodo dell'hub della community della console di Configuration Manager con un collegamento diretto. Questa funzionalità rende più semplice la collaborazione e consente di condividere i collegamenti agli elementi dell'hub della community con i colleghi. Questi collegamenti diretti sono attualmente disponibile solo per gli elementi del nodo dell'hub della console.

### <a name="prerequisites-for-direct-links"></a>Prerequisiti per i collegamenti diretti

- Console di Configuration Manager versione 2006 o successive
- Non è possibile usare l'account predefinito Administrator locale quando si segue un collegamento all'hub della community.

### <a name="sharing-and-opening-direct-links"></a>Condivisione e apertura di collegamenti diretti

Per condividere un elemento:
1. Passare all'elemento nell'hub e selezionare **Condividi**.
1. Incollare il collegamento copiato e condividerlo con altri utenti.

Per aprire un collegamento condiviso:
1. Fare clic sul collegamento da un computer in cui è installata la console di Configuration Manager.
   - Ad esempio, usare questo collegamento per condividere lo [script di configurazione dell'aggiornamento automatico di Edge](https://communityhub.microsoft.com/item/7200) (`https://communityhub.microsoft.com/item/7200`).
1. Selezionare **Avvia l'hub della community** quando viene richiesto.
1. La console viene aperta direttamente con lo script nell'hub della community.

## <a name="known-issues"></a><a name="bkmk_known"></a> Problemi noti

### <a name="unable-to-access-community-hub-node-when-running-console-as-a-different-user"></a>Non è possibile accedere al nodo dell'hub della community quando si esegue la console come utente diverso
<!--7826897-->
Se è stato eseguito l'accesso come utente con diritti inferiori e si sceglie **Esegui come** per eseguire l'accesso come utente diverso e aprire la console di Configuration Manager, potrebbe non essere possibile accedere al nodo **Hub della community**.

### <a name="downloaded-reports-dont-get-removed-from-your-downloads-page"></a>I report scaricati non vengono rimossi dalla pagina dei download
<!--7851305-->
Se si elimina un report scaricato dal nodo **Monitoraggio** > **Report**, il report non viene eliminato dalla pagina **Hub della community** > **Download personali** e non è possibile scaricare di nuovo il report. 

## <a name="next-steps"></a>Passaggi successivi

Altre informazioni sulla creazione e l'uso degli oggetti seguenti:

- [Creare ed eseguire script di PowerShell](../../../apps/deploy-use/create-deploy-scripts.md)
- [Introduzione alla creazione di report](introduction-to-reporting.md)
- [Creare e gestire le sequenze di attività](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md)
- [Creare e distribuire un'applicazione](../../../apps/get-started/create-and-deploy-an-application.md)
- [Creare elementi di configurazione](../../../compliance/deploy-use/create-configuration-items.md)