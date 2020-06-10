---
title: Distribuire molti profili OEMConfig nei dispositivi Zebra usando Microsoft Intune - Azure | Microsoft Docs
description: Usare Microsoft Intune per creare e distribuire più profili di configurazione dei dispositivi OEMConfig nei dispositivi Zebra che eseguono Android Enterprise. Usare le azioni e i passaggi di Zebra per ordinare i profili.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/02/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: ''
ms.technology: ''
ms.assetid: ''
ms.reviewer: jieyan
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2a38c445018200d9fe80db19142f123aba783b60
ms.sourcegitcommit: 8a023e941d90c107c9769a1f7519875a31ef9393
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/03/2020
ms.locfileid: "84311165"
---
# <a name="deploy-multiple-oemconfig-profiles-to-zebra-devices-in-microsoft-intune"></a>Distribuire più profili OEMConfig nei dispositivi Zebra in Microsoft Intune

In Microsoft Intune usare OEMConfig per personalizzare le impostazioni specifiche dell'OEM per i dispositivi Android Enterprise. Queste impostazioni sono specifiche per il produttore del dispositivo e vengono distribuite usando i profili di configurazione in Intune.

Nei dispositivi Zebra è possibile distribuire o assegnare più profili allo stesso dispositivo. I profili OEMConfig esistenti possono usare questa funzionalità dopo la sincronizzazione successiva dei dispositivi con Intune.

Questa funzionalità si applica a:

- Dispositivi zebra che eseguono Android Enterprise

Per altre informazioni su OEMConfig, incluse le funzionalità e come usarla, vedere [Profilo di configurazione di OEMConfig](android-oem-configuration-overview.md).

Questo articolo descrive la distribuzione di più profili di OEMConfig nei dispositivi Zebra, l'ordinamento e l'uso delle funzionalità di creazione di report in Microsoft Intune.

## <a name="prerequisites"></a>Prerequisiti

Creare un [profilo di configurazione di OEMConfig](android-oem-configuration-overview.md).

## <a name="use-multiple-profiles"></a>Usare più profili

Nei dispositivi Zebra è possibile avere molti profili in ogni dispositivo contemporaneamente. Questa funzionalità consente di suddividere le impostazioni OEMConfig di Zebra in profili più piccoli Creare ad esempio un profilo baseline che influisce su tutti i dispositivi. Creare quindi altri profili che configurano impostazioni specifiche per un dispositivo.

Lo schema OEMConfig di Zebra usa anche le **azioni**. Le azioni sono operazioni eseguite sul dispositivo. Non configurano alcuna impostazione. Usare queste azioni per attivare un download di file, cancellare gli Appunti e altro ancora. Per l'elenco completo di azioni supportate, vedere la [Documentazione di Zebra](https://techdocs.zebra.com/oemconfig/10-0/about/) (viene aperto il sito Web di Zebra).

Ad esempio, si crea un profilo OEMConfig di Zebra che applica alcune impostazioni al dispositivo. Un altro profilo OEMConfig di Zebra include un'azione che cancella gli Appunti. Il primo profilo viene assegnato a un gruppo di dispositivi Zebra. Successivamente, è necessario cancellare gli Appunti in questi dispositivi. Il secondo profilo viene assegnato allo stesso gruppo di dispositivi senza modificare il primo profilo. Gli Appunti del dispositivo vengono cancellati senza inviare di nuovo o influire sulle impostazioni di configurazione create nel primo profilo.

In un altro esempio, è stato assegnato un profilo OEMConfig che configura alcune impostazioni del dispositivo Zebra. Di recente, gli utenti hanno segnalato problemi con un'applicazione specifica e si vuole quindi cancellare la cache dell'app. Creare un nuovo profilo OEMConfig che include solo l'azione "Cancella cache". Assegnare il profilo ai dispositivi che lo necessitano.

## <a name="ordering"></a>Ordinamento

Con più profili in ogni dispositivo, l'ordine con cui vengono distribuiti i profili non è garantito. Questo comportamento è una limitazione di Google Play. Per eseguire le operazioni in sequenza, è possibile usare la [funzionalità del passaggio transazioni di Zebra](https://techdocs.zebra.com/oemconfig/10-0/mc/), che consente di aprire il sito Web di Zebra. 

Per riepilogare, se l'ordine è rilevante, usare la [funzionalità del passaggio transazioni di Zebra](https://techdocs.zebra.com/oemconfig/10-0/mc/), che consente di aprire il sito Web di Zebra. Se l'ordine non è rilevante, usare più profili di Intune. 

È possibile esaminare alcuni esempi:

- Si vuole attivare il Bluetooth per tutti i dispositivi Zebra appena registrati prima di configurare eventuali altre impostazioni in questi dispositivi. Per eseguire le operazioni in sequenza, usare la funzionalità **Steps** (Passaggi) nello schema di Zebra.

  Creare un profilo di Intune che include due passaggi di transazioni. Il primo passaggio include le impostazioni Bluetooth e il secondo passaggio configura l'altra impostazione. Quando l'app OEMCong di Zebra riceve il profilo, esegue i passaggi in ordine.

  Per altre informazioni, vedere i [passaggi della transazione di Zebra](https://techdocs.zebra.com/oemconfig/10-0/mc/) (apre il sito Web di Zebra).

- Si vuole che tutti i dispositivi Zebra visualizzino l'ora nel formato 24 ore. Per alcuni di questi dispositivi si vuole disattivare la fotocamera. Le impostazioni relative a ora e fotocamera non dipendono l'una dall'altra.

  Creare due profili di Intune:

  - **Profilo 1**: visualizza l'ora nel formato 24 ore. Questo profilo viene assegnato il lunedì al gruppo **All Zebra AE devices** (Tutti i dispositivi Zebra AE).
  - **Profilo 2**: disattiva la fotocamera. Questo profilo viene assegnato il martedì al gruppo **Zebra AE factory devices** (Dispositivi Zebra AE predefiniti).

  Il mercoledì vengono registrati 10 nuovi dispositivi Zebra con Intune. Il Profilo 1 e il Profilo 2 vengono assegnati. Dopo la sincronizzazione dei nuovi dispositivi con Intune, essi ricevono i profili. È possibile che questi dispositivi ottengano il Profilo 2 prima del Profilo 1.

## <a name="enhanced-reporting"></a>Creazione di report avanzata

Viene distribuito un profilo e questo viene eseguito dall'app OEMConfig di Zebra sul dispositivo. L'app OEMConfig di Zebra segnala lo stato del profilo a Intune. Nell'interfaccia di amministrazione di Endpoint Manager è possibile vedere lo stato dei profili OEMConfig distribuiti e gli eventuali errori o avvisi.

1. Aprire l'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selezionare il profilo OEMConfig di Zebra > **Monitoraggio** > **Stato del dispositivo**. Questa opzione mostra i dispositivi a cui è assegnato il profilo OEMConfig.
3. Selezionare un dispositivo > **Configurazione del dispositivo** > Selezionare il profilo OEMConfig di Zebra. Questa opzione mostra le impostazioni del profilo che hanno avuto esito positivo o negativo.

    Selezionare una riga con esito negativo. Vengono mostrati i dettagli che contengono altre informazioni sul motivo dell'esito negativo.

## <a name="next-steps"></a>Passaggi successivi

- Altre informazioni sui [profili di configurazione OEMConfig](android-oem-configuration-overview.md).
- In Amministratore del dispositivo Android configurare [Mobility Extensions (MX)](android-zebra-mx-overview.md).
- [Monitorare lo stato del profilo](device-profile-monitor.md).
