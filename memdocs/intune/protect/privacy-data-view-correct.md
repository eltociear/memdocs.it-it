---
title: Visualizzare e correggere i dati personali
titleSuffix: Microsoft Intune
description: Informazioni su come visualizzare e correggere i dati personali.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/18/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 1ba77bc7-505e-4eca-a49e-dcdaa75d0043
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d6cddd94400874c508a31b11b22fa4417798e2da
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/21/2020
ms.locfileid: "80084782"
---
# <a name="view-and-correct-personal-data"></a>Visualizzare e correggere i dati personali

Gli amministratori di Intune possono visualizzare alcuni dati personali in base alle relative autorizzazioni di accesso, ma solo gli utenti finali possono modificare i dati personali del loro dispositivo.

[!INCLUDE [GDPR-related guidance](../includes/gdpr-dsr-and-stp-note.md)]


## <a name="view-personal-data"></a>Visualizzare i dati personali

Gli amministratori possono visualizzare le informazioni personali dell'utente finale in diversi pannelli nell'interfaccia utente di Intune. Gli articoli seguenti illustrano le informazioni accessibili e non accessibili per gli amministratori:
- [Visualizzare i dettagli del dispositivo in Intune](../remote-actions/device-inventory.md) descrive in che modo è possibile esaminare i dettagli sul dispositivo di un utente finale.
- [Monitorare le informazioni sulle app e sulle assegnazioni](../apps/apps-monitor.md) spiega come visualizzare i dettagli sulle app installate nel dispositivo di un utente finale.
- L'articolo [Quali sono le informazioni visibili per l'azienda quando si registra il dispositivo?](https://docs.microsoft.com/mem/intune/user-help/what-info-can-your-company-see-when-you-enroll-your-device-in-intune) offre agli utenti finali un elenco dei dati visualizzabili o non visualizzabili dall'azienda. È consigliabile comunicare chiaramente agli utenti il tipo di dati che verranno raccolti e i motivi per cui vengono raccolti. Questo articolo può essere il primo passaggio per ottenere questa trasparenza.

### <a name="who-can-view-the-data"></a>Chi può visualizzare i dati?

Microsoft usa controlli rigorosi per gestire l'accesso ai dati dei clienti, concedendo il livello minimo di accesso necessario per completare le attività principali e revocando l'accesso quando non è più necessario. 

È possibile proteggere e controllare l'accesso ai dati personali degli utenti finali tramite il controllo degli accessi in base al ruolo. Per altre informazioni, vedere [Controllo degli accessi in base al ruolo con Microsoft Intune](../fundamentals/role-based-access-control.md).

Altre informazioni sulle procedure adottate da Microsoft per i dati sono disponibili nelle condizioni per i servizi online e nell'[Informativa sulla privacy dei Microsoft Online Services](https://go.microsoft.com/fwlink/p/?linkid=131004&clcid=0x409). 

## <a name="correct-end-user-personal-data"></a>Correggere i dati personali degli utenti finali

Gli amministratori non possono aggiornare informazioni specifiche del dispositivo o delle app. Se un utente finale vuole correggere i dati personali (ad esempio, il nome del dispositivo), deve farlo direttamente nel dispositivo. Tali modifiche vengono sincronizzate in occasione della connessione successiva a Intune.


## <a name="next-steps"></a>Passaggi successivi

Scoprire come [controllare, esportare o eliminare](privacy-data-audit-export-delete.md) i dati personali in Intune.
