---
title: Aggiungere e assegnare l'app Portale aziendale di Windows 10 per i dispositivi con provisioning tramite Autopilot
titleSuffix: Microsoft Intune
description: Aggiungere e assegnare l'app Portale aziendale di Windows 10 a Intune per i dispositivi con provisioning tramite Autopilot.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 08/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4d45d73f9c10c9bf7562def73b005c0dd63c7613
ms.sourcegitcommit: 91519f811b58a3e9fd116a4c28e39341ad8af11a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2020
ms.locfileid: "88559522"
---
# <a name="add-and-assign-the-windows-10-company-portal-app-for-autopilot-provisioned-devices"></a>Aggiungere e assegnare l'app Portale aziendale di Windows 10 per i dispositivi con provisioning tramite Autopilot

Per gestire i dispositivi e installare le app, gli utenti possono usare l'app Portale aziendale. È possibile assegnare l'app Portale aziendale di Windows 10 direttamente da Intune. 

## <a name="prerequisites"></a>Prerequisiti

Per i dispositivi di Windows 10 con provisioning tramite Autopilot, è consigliabile associare l'account Microsoft Store per le aziende a Intune. Per altre informazioni, vedere [Come gestire le app acquistate con Volume Purchase Program da Microsoft Store per le aziende con Microsoft Intune](windows-store-for-business.md).

È possibile scegliere di installare l'app **Portale aziendale (offline)** seguendo questa procedura. L'app Portale aziendale verrà installata nel contesto di dispositivo quando sarà assegnata al gruppo Autopilot e verrà installata nel dispositivo prima che l'utente esegua l'accesso.

## <a name="configure-the-store-settings-to-show-the-offline-app"></a>Configurare le impostazioni dello Store per visualizzare l'app offline

1. Accedere a [Microsoft Store per le aziende](https://www.microsoft.com/business-store) con l'account amministratore.
2. Selezionare la scheda **Manage** (Gestisci) nella parte superiore della finestra.
3. Nel riquadro di sinistra selezionare **Impostazioni**.
4. Impostare **Show offline apps** (Mostra app offline) in **Shopping experience** (Esperienza di acquisto) su **On** (Attivo).  
   Saranno visualizzate le app con licenza offline.

## <a name="get-the-offline-company-portal-app-from-the-store"></a>Ottenere l'app Portale aziendale offline dallo Store

1. Cercare e selezionare l'app **Portale aziendale**.
2. Impostare il **Tipo di licenza** su **Offline**.
3. Selezionare **Scarica l'app** per acquisire e aggiungere l'app Portale aziendale offline all'inventario.
   Affinché l'app venga elencata in Intune, è necessario attendere che la pianificazione della sincronizzazione venga completata o eseguire una sincronizzazione manuale dall'interfaccia di amministrazione di Microsoft Endpoint Manager.

## <a name="manually-sync-company-portal-app-with-intune"></a>Sincronizzare manualmente l'app Portale aziendale con Intune

1. Accedere all' [interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) con l'account amministratore.
2. Selezionare **Amministrazione del tenant** > **Connettori e token** > **Microsoft Store per le aziende**.
3. Fare clic su **Abilita**.
4. Se non è ancora stato fatto, fare clic sul collegamento per registrarsi a Microsoft Store per le aziende e associare il proprio account come descritto in precedenza.
5. Nell'elenco a discesa **Lingua** scegliere la lingua in cui visualizzare le app scaricate da Microsoft Store per le aziende nel portale di Azure. Indipendentemente dalla lingua in cui sono visualizzate, vengono installate nella lingua dell'utente finale, se disponibile.
6. Fare clic su **Sincronizza** per trasferire le app acquistate da Microsoft Store in Intune.

## <a name="assign-the-company-portal-app"></a>Assegnare l'app Portale aziendale

1. Accedere all' [interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) con l'account amministratore.
2. Selezionare **App** > **Windows**.
3. Nell'elenco delle app di Windows selezionare **Portale aziendale (offline)** .
4. [Assegnare](apps-deploy.md) l'app Portale aziendale come app obbligatoria ai gruppi di dispositivi Autopilot selezionati.

## <a name="next-steps"></a>Passaggi successivi

- Per altre informazioni sull'assegnazione di app, vedere [Assegnare app ai gruppi](apps-deploy.md).

