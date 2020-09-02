---
title: Funzionalità di Intune per i metodi di registrazione dei dispositivi Windows
titleSuffix: Microsoft Intune
description: Funzionalità per ogni metodo di registrazione dei dispositivi Windows.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 09/21/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 701794ba476f87aaf079e39c834f3e8e3f2c280d
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/26/2020
ms.locfileid: "88913886"
---
# <a name="intune-enrollment-method-capabilities-for-windows-devices"></a>Funzionalità di Intune per i metodi di registrazione dei dispositivi Windows
[!INCLUDE[azure_portal](../includes/azure_portal.md)]

Esistono diversi metodi per registrare i dispositivi del personale in Intune. Ogni metodo presenta procedure consigliate e funzionalità diverse, come illustrato nelle tabelle seguenti.

## <a name="best-practices-by-enrollment-method"></a>Procedure consigliate per metodo di registrazione
| **Procedure consigliate** | **[Aggiunto ad Azure AD](windows-enroll.md#enable-windows-10-automatic-enrollment)**|**[Aggiunto ad Azure AD con Autopilot (modalità definita dall'utente)](../../autopilot/enrollment-autopilot.md)** |**[Aggiunto ad Azure AD con Autopilot (modalità di distribuzione automatica)](../../autopilot/enrollment-autopilot.md)** |**[Bulk](windows-bulk-enroll.md)**|**[DEM](device-enrollment-manager-enroll.md)** | **[BYOD](device-enrollment.md#bring-your-own-device)** | **[Oggetto Criteri di gruppo](/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy)** | **[Co-gestione](/configmgr/core/clients/manage/co-management-overview)** |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Usato comunemente in EDU|![X](./media/enrollment-method-capab/xmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|
|I dispositivi possono essere condivisi|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|
|I dispositivi personali devono accedere alle risorse aziendali|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|
|Manutenzione automatica delle app|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|

## <a name="capabilities-by-enrollment-method"></a>Procedure consigliate per metodo di registrazione

| **Funzionalità** | **[Aggiunto ad Azure AD](windows-enroll.md#enable-windows-10-automatic-enrollment)**|**[Aggiunto ad Azure AD con Autopilot (modalità definita dall'utente)](../../autopilot/enrollment-autopilot.md)** |**[Aggiunto ad Azure AD con Autopilot (modalità di distribuzione automatica)](../../autopilot/enrollment-autopilot.md)** |**[Bulk](windows-bulk-enroll.md)**|**[DEM](device-enrollment-manager-enroll.md)** | **[BYOD](device-enrollment.md#bring-your-own-device)** | **[Oggetto Criteri di gruppo](/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy)** | **[Co-gestione](/configmgr/core/clients/manage/co-management-overview)** |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Accesso condizionale                                      |![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)\*\*|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|
|L'utente viene associato al dispositivo                    |![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|
|Richiede Azure AD Premium                               |![X](./media/enrollment-method-capab/xmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|
|Il dispositivo può accedere alle risorse protette da autorità di certificazione             |![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|
|Gli utenti non possono essere amministratori dei propri dispositivi               |![X](./media/enrollment-method-capab/xmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|
|Possibilità di configurare l'esperienza di installazione del dispositivo        |![X](./media/enrollment-method-capab/xmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|
|Possibilità di registrare i dispositivi senza intervento dell'utente      |![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|
|Possibilità di eseguire gli script di PowerShell                       |![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/checkmark.png)\*| 
|Supporta la registrazione automatica dopo l'aggiunta a un dominio AD      |![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|
|Supporta la registrazione automatica dopo l'aggiunta ad Azure AD ibrido|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|
|Supporta la registrazione automatica dopo l'aggiunta ad Azure AD       |![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![Segno di spunta](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|

\* I carichi di lavoro delle app client in Configuration Manager devono essere spostati nel progetto pilota di Intune o in Intune.

\** [I dispositivi sono bloccati per l'accesso condizionale ad eccezione di Windows 10 1803+.](device-enrollment-manager-enroll.md)

## <a name="next-steps"></a>Passaggi successivi

[Configurare la registrazione per Windows](windows-enroll.md)