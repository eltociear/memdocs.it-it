---
title: Download delle definizioni da Microsoft
titleSuffix: Configuration Manager
description: Informazioni su come abilitare il download delle definizioni malware di Endpoint Protection da Microsoft Updates per Configuration Manager.
ms.date: 11/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: ab7626ae-d4bf-4ca6-ab25-c61f96800a02
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1f0d8ac635d514e750584126458bfde6b5fc24ee
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697239"
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-microsoft-updates"></a>Abilitare le definizioni malware di Endpoint Protection da scaricare da Microsoft Updates

*Si applica a: Configuration Manager (Current Branch)*

Quando si sceglie di scaricare gli aggiornamenti delle definizioni da Microsoft Update, i client controlleranno il sito Microsoft Update con la frequenza definita nella sezione **Aggiornamenti dell'intelligence per la sicurezza** della finestra di dialogo dei criteri antimalware.

 Questo metodo può essere utile se il client non ha connettività al sito di Configuration Manager o se si vuole che gli utenti possano avviare gli aggiornamenti delle definizioni.

> [!IMPORTANT]
> - Per poter usare questo metodo per scaricare gli aggiornamenti delle definizioni, i client devono avere accesso a Microsoft Update in Internet.
> - La sezione **Aggiornamenti delle definizioni** è stata rinominata in **Aggiornamenti dell'intelligence per la sicurezza** a partire da Configuration Manager versione 1902.

## <a name="using-the-microsoft-malware-protection-center-to-download-definitions"></a>Uso di Microsoft Malware Protection Center per scaricare le definizioni
 È possibile configurare i client per scaricare gli aggiornamenti delle definizioni da Microsoft Malware Protection Center. Questa opzione è usata dai client di Endpoint Protection per scaricare gli aggiornamenti delle definizioni se non sono riusciti a scaricare gli aggiornamenti da un'altra origine. Questo metodo di aggiornamento può essere utile se si verifica un problema con l'infrastruttura di Configuration Manager che impedisce il recapito degli aggiornamenti.

> [!IMPORTANT]
>  Per poter usare questo metodo per scaricare gli aggiornamenti delle definizioni, i client devono avere accesso a Microsoft Update in Internet.
> 
> 
> [!div class="button"]
> [Passaggio successivo >](endpoint-antimalware-policies.md)
> 
> [!div class="button"]
> [Indietro >](endpoint-configure-alerts.md)
