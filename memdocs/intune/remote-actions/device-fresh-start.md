---
title: Reimpostare i dispositivi Windows 10 con Microsoft Intune - Azure | Microsoft Docs
description: Usare Fresh Start per rimuovere o disinstallare app nei PC Windows 10 tramite Microsoft Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 5aa5cfa3-c483-4099-b40f-578ff8dca425
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6a23b5de7ca83b92cc355858d762cce25157f694
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79349121"
---
# <a name="use-fresh-start-to-reset-windows-10-devices-with-intune"></a>Usare Fresh Start per ripristinare i dispositivi Windows 10 con Intune


[!INCLUDE [azure_portal](../includes/azure_portal.md)]

L'azione del dispositivo **Fresh Start** rimuove le eventuali app installate nei PC con Windows 10, versione 1703 o successive. Fresh Start consente di rimuovere le app (OEM) preinstallate in genere in un nuovo PC. 

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) e selezionare **Dispositivi** > **Tutti i dispositivi**.
2. Nell'elenco dei dispositivi gestiti scegliere un dispositivo desktop Windows 10.
3. Fare clic su **Fresh Start**. 
4. Selezionare **Mantieni i dati utente in questo dispositivo** per:
   * Mantenere il dispositivo aggiunto ad Azure AD
   * Il dispositivo viene nuovamente iscritto alla gestione di dispositivi mobili quando un utente abilitato per Azure Active Directory accede al dispositivo stesso.
   * Mantenere il contenuto della home directory dell'utente del dispositivo e rimuovere le app e le impostazioni

  > [!IMPORTANT]
 > Se non si mantengono i dati dell'utente, il dispositivo viene ripristinato allo stato predefinito della configurazione guidata mantenendo l'account amministratore predefinito.
 > La registrazione dei dispositivi personali (BYOD) in Azure AD e nella gestione di dispositivi mobili verrà annullata.
 > I dispositivi con accesso ad Azure AD verranno iscritti nuovamente alla gestione di dispositivi mobili quando un utente abilitato per Azure Active Directory accede al dispositivo.
 
5. Fare clic su **OK**.   
6. Per visualizzare lo stato di questa azione, tornare a **Dispositivi** e fare clic su **Azioni del dispositivo**.  
7. Il dispositivo viene ripristinato con la schermata di accesso iniziale.
