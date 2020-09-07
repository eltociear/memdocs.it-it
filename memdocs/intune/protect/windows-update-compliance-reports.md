---
title: Usare i report di Conformità aggiornamenti per gli aggiornamenti di Windows in Microsoft Intune
titleSuffix: Microsoft Intune
description: Usare Conformità aggiornamenti di Operation Management Suite per visualizzare i dati dei report per gli aggiornamenti di Windows distribuiti con Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/01/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 297707da0afb03650eaab91b26abad9947c6a951
ms.sourcegitcommit: 75d6ea42a0f473dc5020ae7fcb667c9bdde7bd97
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/01/2020
ms.locfileid: "89286153"
---
# <a name="intune-compliance-reports-for-updates"></a>Report di conformità di Intune per gli aggiornamenti

Quando si usa Intune per distribuire aggiornamenti di Windows in dispositivi Windows 10, è possibile visualizzare i dettagli sulla conformità degli aggiornamenti tramite Intune o una soluzione gratuita denominata *Conformità aggiornamenti*. Conformità aggiornamenti fa parte di Microsoft Operations Management Suite (OMS).

## <a name="use-intune"></a>Usare Intune

Per esaminare un report sui criteri sullo stato di distribuzione per gli anelli di aggiornamento di Windows 10 configurati:

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selezionare **Dispositivi** > **Panoramica** > **Stato dell'aggiornamento software**. Vengono visualizzate informazioni generali sullo stato di tutti gli anelli di aggiornamento assegnati.

3. Per visualizzare ulteriori dettagli, selezionare **Monitoraggio**. Quindi, in **Aggiornamenti software** selezionare **Stato di distribuzione per ogni anello di aggiornamento** e scegliere l'anello di distribuzione da rivedere.

   Nella sezione **Monitoraggio** scegliere uno dei report seguenti per visualizzare informazioni dettagliate sull'anello di aggiornamento:

   - **Stato del dispositivo**: visualizza lo stato di configurazione del dispositivo. Per informazioni dettagliate, vedere [Aggiornare deviceConfigurationDeviceStatus]( /graph/api/intune-deviceconfig-deviceconfigurationdevicestatus-update?view=graph-rest-1.0).

   - **Stato dell'utente**: visualizza il nome utente, lo stato e la data dell'ultimo report. Per informazioni dettagliate, vedere [Visualizzare deviceConfigurationUserStatus](/graph/api/intune-deviceconfig-deviceconfigurationuserstatus-list?view=graph-rest-1.0).

   - **Stato di aggiornamento dell'utente finale**: visualizza lo stato di aggiornamento del dispositivo Windows. Per informazioni dettagliate, vedere [windowsUpdateState](/graph/api/resources/intune-shared-windowsupdatestate?view=graph-rest-beta).

## <a name="use-update-compliance"></a>Usare Conformità aggiornamenti

È possibile monitorare le implementazioni degli aggiornamenti di Windows 10 usando [Conformità aggiornamenti](/windows/deployment/update/update-compliance-monitor). Conformità aggiornamenti viene fornito tramite il portale di Azure ed è disponibile gratuitamente per i dispositivi che ne soddisfano i [prerequisiti](/windows/deployment/update/update-compliance-get-started#update-compliance-prerequisites).  

Quando si usa questa soluzione, è possibile distribuire un ID commerciale in uno qualsiasi dei dispositivi Windows 10 gestiti da Intune per cui si vuole creare report di conformità degli aggiornamenti.  

In Intune usare le impostazioni OMA-URI di un criterio personalizzato per configurare l'ID commerciale. Vedere [Usare le impostazioni personalizzate per dispositivi Windows 10 in Intune](../configuration/custom-settings-windows-10.md).

Il percorso OMA-URI (con distinzione tra maiuscole e minuscole) per configurare l'ID commerciale è: *./Vendor/MSFT/DMClient/Provider/MS DM Server/CommercialID*

È ad esempio possibile usare i valori seguenti in **Aggiungi o modifica impostazione URI OMA**:

- **Nome dell'impostazione**: ID commerciale di Windows Analytics
- **Descrizione dell'impostazione**: configurazione dell'ID commerciale per le soluzioni Windows Analytics
- **URI-OMA** (con distinzione tra maiuscole e minuscole): *./Vendor/MSFT/DMClient/Provider/ProviderID/CommercialID*
- **Tipo di dati**: Stringa
- **Valore**: \<Use the GUID shown on the Windows Telemetry tab in your OMS workspace>

> [!NOTE]
> Per altre informazioni su MS DM Server, vedere [DMClient configuration service provider (CSP)]( /windows/client-management/mdm/dmclient-csp) (Provider di servizi di configurazione per DMClient).

## <a name="next-steps"></a>Passaggi successivi

[Gestire gli aggiornamenti software in Intune](windows-update-for-business-configure.md)
