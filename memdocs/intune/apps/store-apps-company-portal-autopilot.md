---
title: Aggiungere e assegnare l'app Portale aziendale di Windows 10 per i dispositivi con provisioning tramite Autopilot
titleSuffix: Microsoft Intune
description: Aggiungere e assegnare l'app Portale aziendale di Windows 10 a Intune per i dispositivi con provisioning tramite Autopilot.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/21/2020
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
ms.openlocfilehash: ff08d1424866a0f18a44aa51b97ffc6f92e58789
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/28/2020
ms.locfileid: "87262694"
---
# <a name="add-and-assign-the-windows-10-company-portal-app-for-autopilot-provisioned-devices"></a>Aggiungere e assegnare l'app Portale aziendale di Windows 10 per i dispositivi con provisioning tramite Autopilot

Per gestire i dispositivi e installare le app, gli utenti possono usare l'app Portale aziendale. È possibile assegnare l'app Portale aziendale di Windows 10 direttamente da Intune. 

## <a name="prerequisites"></a>Prerequisiti

Per i dispositivi di Windows 10 con provisioning tramite Autopilot, è consigliabile associare l'account Microsoft Store per le aziende a Intune. Per altre informazioni, vedere [Come gestire le app acquistate con Volume Purchase Program da Microsoft Store per le aziende con Microsoft Intune](windows-store-for-business.md).

È possibile scegliere di installare il Portale aziendale (offline) tramite la procedura seguente. L'app Portale aziendale verrà installata nel contesto di dispositivo quando sarà assegnata al gruppo Autopilot e verrà installata nel dispositivo prima dell'accesso dell'utente. 

## <a name="configure-settings-to-show-offline-app"></a>Configurare le impostazioni per visualizzare l'app offline

1. Accedere a [Microsoft Store per le aziende](https://www.microsoft.com/business-store) con l'account amministratore.
2. Selezionare la scheda **Manage** (Gestisci) nella parte superiore della finestra.
3. Nel riquadro di sinistra selezionare **Impostazioni**.
4. Impostare **Show offline apps** (Mostra app offline) in **Shopping experience** (Esperienza di acquisto) su **On** (Attivo).  
    Saranno visualizzate le app con licenza offline.

## <a name="get-the-offline-company-portal-app"></a>Ottenere l'app Portale aziendale offline

1. Cercare e selezionare l'app **Portale aziendale**.
2. Impostare il **Tipo di licenza** su **Offline**.
3. Selezionare **Scarica l'app** per acquisire e aggiungere l'app Portale aziendale offline all'inventario.

## <a name="assign-the-company-portal-app"></a>Assegnare l'app Portale aziendale

1. Accedere all' [interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) con l'account amministratore. 
2. Selezionare la scheda **App** nel riquadro destro.
3. In **Piattaforma** selezionare **Windows**.
4. Selezionare **Portale aziendale (offline)** .
5. È necessario attendere che la pianificazione della sincronizzazione venga completata o eseguire una sincronizzazione manuale dall'interfaccia di amministrazione di Microsoft Endpoint Manager.
6. Assegnare l'app Portale aziendale come app obbligatoria al gruppo di dispositivi Autopilot selezionato.

## <a name="next-steps"></a>Passaggi successivi

- Per altre informazioni sull'assegnazione di app, vedere [Assegnare app ai gruppi](apps-deploy.md).

