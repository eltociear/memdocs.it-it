---
title: Distribuire molti profili OEMConfig nei dispositivi Zebra usando Microsoft Intune - Azure | Microsoft Docs
description: Usare Microsoft Intune per creare e distribuire più profili di configurazione dei dispositivi OEMConfig nei dispositivi Zebra che eseguono Android Enterprise. Usare le azioni e i passaggi di Zebra per ordinare i profili.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/12/2020
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
ms.openlocfilehash: 2227face347e6d82cf7807bea241eda4856c1d67
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988685"
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

Nei dispositivi Zebra è possibile avere molti profili in ogni dispositivo contemporaneamente. Questa funzionalità consente di suddividere le impostazioni OEMConfig di Zebra in profili più piccoli Lo schema OEMConfig di Zebra usa anche le **azioni**. Le azioni sono operazioni eseguite sul dispositivo. Non configurano alcuna impostazione. Usare queste azioni per attivare un download di file, cancellare gli Appunti e altro ancora. Per l'elenco completo di azioni supportate, vedere la [Documentazione di Zebra](https://techdocs.zebra.com/oemconfig/10-0/about/) (viene aperto il sito Web di Zebra).

Ad esempio, si crea un profilo OEMConfig di Zebra che applica alcune impostazioni al dispositivo. Un altro profilo OEMConfig di Zebra include un'azione che cancella gli Appunti. Il primo profilo viene assegnato a un gruppo di dispositivi Zebra. Successivamente, è necessario cancellare gli Appunti in questi dispositivi. Il secondo profilo viene assegnato allo stesso gruppo di dispositivi senza modificare il primo profilo. Gli Appunti del dispositivo vengono cancellati senza inviare di nuovo o influire sulle impostazioni di configurazione create nel primo profilo.

In un altro esempio, è stato assegnato un profilo OEMConfig che configura alcune impostazioni del dispositivo Zebra. Di recente, gli utenti hanno segnalato problemi con un'applicazione specifica e si vuole quindi cancellare la cache dell'app. Creare un nuovo profilo OEMConfig che include solo l'azione "Cancella cache". Assegnare il profilo ai dispositivi che lo necessitano.

## <a name="ordering"></a>Ordinamento

Con più profili in ogni dispositivo, l'ordine con cui vengono distribuiti i profili non è garantito. Questo comportamento è una limitazione di Google Play. Per eseguire le operazioni in sequenza, è possibile usare la [funzionalità Transazioni di Zebra](https://techdocs.zebra.com/oemconfig/9-1/mc/) (apre il sito Web di Zebra). Ecco un esempio.

Sono disponibili due profili:

- **Profilo 1**: attiva il Bluetooth. Questo profilo viene assegnato il lunedì al gruppo **Tutti i dispositivi**.
- **Profilo 2**: configura qualsiasi altra impostazione. Questo profilo viene assegnato il martedì al gruppo **Tutti i dispositivi**.

È necessario attivare il Bluetooth prima di configurare l'altra impostazione.

Il mercoledì vengono registrati 10 nuovi dispositivi Zebra con Intune. Il Profilo 1 e il Profilo 2 vengono assegnati al gruppo **Tutti i dispositivi**. Dopo la sincronizzazione dei nuovi dispositivi con Intune, essi ricevono i profili. È possibile che questi dispositivi ottengano il Profilo 2 prima del Profilo 1.

Usare la funzionalità **Passaggi** nello schema di Zebra per verificare che le operazioni vengano eseguite in sequenza. In questo caso, è possibile creare un profilo con due Passaggi Transazione. Il primo passaggio include le impostazioni Bluetooth e il secondo passaggio configura l'altra impostazione. Quando l'app OEMCong di Zebra riceve il profilo, esegue i passaggi in ordine, e ciò è garantito da Zebra.

Per altre informazioni, vedere i [passaggi della transazione di Zebra](https://techdocs.zebra.com/oemconfig/9-1/mc/) (apre il sito Web di Zebra).

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
