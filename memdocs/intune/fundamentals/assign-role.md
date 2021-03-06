---
title: Assegnare un ruolo a un utente di Intune
description: Informazioni su come assegnare un ruolo predefinito o personalizzato a un utente in Microsoft Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/26/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: pjain
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 31e73bd1c3ebed40865ea6c13952b91c3a672852
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988850"
---
# <a name="assign-a-role-to-an-intune-user"></a>Assegnare un ruolo a un utente di Intune

È possibile assegnare un ruolo [predefinito](role-based-access-control.md#built-in-roles) o [personalizzato](create-custom-role.md) a un utente di Intune.

Per creare, modificare o assegnare ruoli, l'account deve disporre di una delle seguenti autorizzazioni in Azure AD:
- **Amministratore globale**
- **Amministratore del servizio Intune**

1. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) scegliere **Amministrazione del tenant** > **Ruoli** > **Tutti i ruoli**.

2. Nel pannello **Ruoli di Intune - Tutti i ruoli** scegliere il ruolo predefinito da assegnare > **Assegnazioni** > **Assegna**.

5. Nella pagina **Informazioni di base** immettere un **Nome dell'assegnazione** e una **Descrizione dell'assegnazione** facoltativa e quindi scegliere **Avanti**.

6. Nella pagina **Gruppi amministrativi** scegliere il gruppo contenente l'utente a cui si vogliono assegnare le autorizzazioni. Scegliere **Avanti**

7. Nella pagina **Ambito (gruppi)** scegliere un gruppo contenente gli utenti/dispositivi che il membro indicato in precedenza è autorizzato a gestire. Scegliere **Avanti**.

8. Nella pagina **Ambito (tag)** scegliere i tag in cui verrà applicata questa assegnazione di ruolo. Scegliere **Avanti**.

9. Al termine, nella pagina **Rivedi e crea** scegliere **Crea**. La nuova assegnazione viene visualizzata nell'elenco di assegnazioni.

## <a name="next-steps"></a>Passaggi successivi
- [Informazioni sul controllo degli accessi in base al ruolo in Intune](role-based-access-control.md)
- [Creare un ruolo personalizzato](create-custom-role.md)


