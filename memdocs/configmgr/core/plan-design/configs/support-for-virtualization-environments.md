---
title: Supporto della virtualizzazione
titleSuffix: Configuration Manager
description: Requisiti per l'installazione di ruoli del sistema del sito e dei client di Configuration Manager in un ambiente di virtualizzazione.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1098e8c5-9676-4c2b-841b-ec88bd04e495
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4d2977fc34e9c398e9e266cbc9b223ea74a1dd18
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700232"
---
# <a name="support-for-virtualization-environments-with-configuration-manager"></a>Supporto per gli ambienti di virtualizzazione per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Configuration Manager supporta l'installazione del client e dei ruoli del sistema del sito in sistemi operativi supportati eseguiti come macchina virtuale in determinati ambienti di virtualizzazione. Questo supporto è presente anche quando l'host virtuale (ambiente di virtualizzazione) non è supportato come client o server del sito.

Ad esempio, si usa Microsoft Hyper-V Server 2016 per ospitare una macchina virtuale che esegue Windows Server 2019. È possibile installare il client o i ruoli del sistema del sito nella macchina virtuale che esegue Windows Server 2019. Non è possibile installare il client nell'host che esegue Microsoft Hyper-V Server 2016.

## <a name="virtualization-environments"></a>Ambienti di virtualizzazione

- Windows Server 2019  
- Windows Server 2016 <sup>[Nota 1](#bkmk_note1)</sup>  
- Microsoft Hyper-V Server 2016 <sup>[Nota 1](#bkmk_note1)</sup>  
- R2 per Windows Server 2012  
- Microsoft Hyper-V Server 2012  
- Windows Server 2012  

<a name="bkmk_note1"></a>

> [!NOTE]
> Configuration Manager non supporta la [virtualizzazione annidata](/windows-server/virtualization/hyper-v/What-s-new-in-Hyper-V-on-Windows#nested-virtualization-new), introdotta con Windows Server 2016.

### <a name="virtualization-environment-support"></a>Supporto dell'ambiente di virtualizzazione

Per ogni computer virtuale è richiesta la stessa dotazione hardware e software (o superiore) che verrebbe usata per un computer Configuration Manager fisico.

Per verificare che Configuration Manager sia in grado di supportare l'ambiente di virtualizzazione, usare il programma SVVP (Server Virtualization Validation Program), che include una procedura guidata online per criteri di supporto del programma di virtualizzazione. Per altre informazioni, vedere [Windows Server Virtualization Validation Program](https://www.windowsservercatalog.com/svvp.aspx) (Programma SVVP - Server Virtualization Validation Program).

Configuration Manager non può gestire le macchine virtuali offline. Il client di Configuration Manager nel computer host non può gestire l'immagine di una macchina virtuale offline, ad esempio non può installare gli aggiornamenti software o raccogliere l'inventario hardware.

In generale, Configuration Manager non presta particolare attenzione alle macchine virtuali. Se ad esempio si arresta una macchina virtuale e non si salva il relativo stato, Configuration Manager può non essere in grado di stabilire se è necessario reinstallare un aggiornamento software.

Per migliorare le prestazioni del client di Configuration Manager in ambienti virtuali che supportano più sessioni utente, i criteri utente vengono disabilitati per impostazione predefinita. A partire dalla versione 1910, è possibile abilitare i criteri utente in questo scenario. Per altre informazioni, vedere [Informazioni sulle impostazioni client - Abilitare i criteri utente per più sessioni utente](../../clients/deploy/about-client-settings.md#enable-user-policy-for-multiple-user-sessions).

## <a name="microsoft-azure-vms"></a><a name="bkmk_Azure"></a> Macchine virtuali di Microsoft Azure

Configuration Manager può essere eseguito in macchine virtuali di Azure così come viene eseguito in locale all'interno del data center. Usare Configuration Manager con le macchine virtuali di Azure negli scenari seguenti:

- **Scenario 1**: eseguire Configuration Manager in una macchina virtuale di Azure. Usarlo per gestire i client in altre macchine virtuali di Azure.

- **Scenario 2**: eseguire Configuration Manager in una macchina virtuale di Azure. Usarlo per gestire i client che non sono in esecuzione in Azure.

- **Scenario 3:** eseguire ruoli diversi del sistema del sito di Configuration Manager in macchine virtuali di Azure. Eseguire altri ruoli nel data center locale, con la connessione appropriata ad Azure.

Gli stessi requisiti di Configuration Manager per le reti, le configurazioni supportate e i requisiti hardware si applicano anche alle macchine virtuali di Azure.

Per altre informazioni, vedere [Configuration Manager in Azure](../../understand/configuration-manager-on-azure.md).

> [!IMPORTANT]
> I siti e i client di Configuration Manager eseguiti nelle macchine virtuali di Azure sono soggetti agli stessi requisiti di licenza delle installazioni locali.

## <a name="windows-virtual-desktop"></a>Desktop virtuale Windows

[Desktop virtuale Windows](/azure/virtual-desktop/) è un servizio di virtualizzazione di desktop e app eseguito su Microsoft Azure. A partire dalla versione 1906, usare Configuration Manager per gestire questi dispositivi virtuali che eseguono Windows in Azure. Per altre informazioni, vedere [Sistemi operativi supportati per client e dispositivi](supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop).

## <a name="next-steps"></a>Passaggi successivi

[Gestire i client di Configuration Manager in un'infrastruttura VDI (Virtual Desktop Infrastructure)](../../clients/deploy/plan/considerations-for-managing-clients-in-a-vdi.md)