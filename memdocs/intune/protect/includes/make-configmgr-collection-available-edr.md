---
author: brenduns
ms.author: brenduns
ms.service: microsoft-intune
ms.subservice: protect
ms.topic: include
ms.date: 08/24/2020
ms.openlocfilehash: 01179c35274ff14d4a91283e9a38aa5e6fee8e03
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/25/2020
ms.locfileid: "88823494"
---
<!--Don't apply H2/H3 in this include file since they are context driven by article-->
1. Da una console di Configuration Manager connessa al sito di livello superiore, fare clic con il pulsante destro del mouse su una raccolta di dispositivi sincronizzata con l'interfaccia di amministrazione di Microsoft Endpoint Manager e scegliere **Proprietà**.

2. Nella scheda **Cloud Sync** (Sincronizzazione cloud) abilitare l'opzione **Rendi disponibile questa raccolta per l'assegnazione dei criteri di sicurezza degli endpoint dall'interfaccia di amministrazione di Microsoft Endpoint Manager**.

   - Non è possibile selezionare questa opzione se la gerarchia di Configuration Manager non è collegata al tenant.
   - Le raccolte disponibili per questa opzione sono limitate dall'[ambito delle raccolte selezionato per il caricamento con collegamento al tenant](../../../configmgr/tenant-attach/device-sync-actions.md#bkmk_edit). <!--CM7423168-->
  
   ![Configurare la sincronizzazione cloud](../media/tenant-attach-intune/cloud-sync.png)

3. Selezionare **OK** per salvare la configurazione.

   È ora possibile eseguire l'onboarding dei dispositivi di questa raccolta con Microsoft Defender ATP ed è supportato l'uso dei criteri di sicurezza degli endpoint di Intune.
