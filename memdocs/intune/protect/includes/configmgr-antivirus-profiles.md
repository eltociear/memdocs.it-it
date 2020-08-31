---
author: brenduns
ms.author: brenduns
ms.service: microsoft-intune
ms.subservice: protect
ms.topic: include
ms.date: 08/24/2020
ms.openlocfilehash: ff48e8117437e45be42551ebffff7cdcf5bce184
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/25/2020
ms.locfileid: "88820299"
---
<!--Don't apply H2/H3 in this include file since they are context driven by article-->
Per i dispositivi gestiti con Configuration Manager (Current Branch) 2006 o versione successiva, sono supportati gli elementi seguenti tramite lo scenario di collegamento al tenant:
<!--The following profiles are supported for devices you manage with Configuration Manager Technical Preview 2007 or later, through the tenant attach scenario:-->

- Piattaforma: **Windows 10 e Windows Server**

  - Profilo: **Criteri di Microsoft Defender Antivirus (ConfigMgr)**
  
    Gestire le [impostazioni dei criteri antivirus per i dispositivi di Configuration Manager](../../protect/antivirus-microsoft-defender-settings-windows-tenant-attach.md) quando si usa il collegamento al tenant.

    Questo profilo è supportato con i dispositivi collegati al tenant che eseguono le piattaforme seguenti:
    - Windows 10 e versioni successive (x86, x64, ARM64)
    - Windows 8.1 (x84, x64)
    - Windows Server 2019 e versioni successive (x64)
    - Windows Server 2016 (x64)
    - Windows Server 2012 R2 (x64)
    - Windows Server 2008 R2 SP1 (x64)
