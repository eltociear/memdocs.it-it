---
title: Usare Software Center per distribuire Windows in rete
titleSuffix: Configuration Manager
description: Distribuire un sistema operativo da Software Center per aggiornare un computer esistente con una nuova versione di Windows o eseguire l'aggiornamento di Windows alla versione più recente.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 919e3636-53fe-4119-ad14-2d03702b391b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6bd10240ebc7ec478efe122bf7f8a45d3afe9f10
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124602"
---
# <a name="use-software-center-to-deploy-windows-over-the-network-with-configuration-manager"></a>Usare Software Center per distribuire Windows in rete con Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

È possibile creare una sequenza di attività che consente di installare un sistema operativo disponibile in Software Center. Un utente può eseguire una sequenza di attività da Software Center per gli scenari di distribuzione del sistema operativo seguenti:

- [Aggiornare un computer esistente con una nuova versione di Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

- [Aggiornare Windows alla versione più recente](upgrade-windows-to-the-latest-version.md)

- [Creare una sequenza di attività per distribuzioni non di sistema operativo](create-a-task-sequence-for-non-operating-system-deployments.md)

Completare i passaggi in uno di questi scenari di distribuzione del sistema operativo. Usare quindi le sezioni seguenti per preparare le distribuzioni disponibili in Software Center.

## <a name="deploy-the-task-sequence"></a><a name="BKMK_Deploy"></a> Distribuire la sequenza di attività

Distribuire la sequenza di attività in una raccolta di destinazione. Per altre informazioni, vedere [Deploy a task sequence](deploy-a-task-sequence.md).

Nella pagina **Impostazioni distribuzione** della distribuzione, per l'impostazione **Rendi disponibile per**, selezionare una delle opzioni seguenti:

- Solo client di Configuration Manager

- Client di Configuration Manager, supporti e PXE

Specificare anche se la distribuzione è necessaria o disponibile:

- Distribuzione necessaria: le distribuzioni necessarie rendono disponibile la sequenza di attività in Software Center. Tale sequenza viene avviata automaticamente alla scadenza configurata.

- Distribuzione disponibile: la sequenza di attività è disponibile in Software Center e un utente può installarla su richiesta.

Dopo aver creato la distribuzione, i client inclusi nella raccolta di destinazione visualizzeranno la sequenza di attività in Software Center.

## <a name="next-steps"></a>Passaggi successivi

[Esperienze utente per la distribuzione del sistema operativo](../understand/user-experience.md#software-center)
