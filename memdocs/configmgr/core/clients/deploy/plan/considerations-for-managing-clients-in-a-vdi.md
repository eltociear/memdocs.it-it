---
title: Gestire i client VDI
titleSuffix: Configuration Manager
description: Gestire i client di Configuration Manager in un'infrastruttura VDI (Virtual Desktop Infrastructure).
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: abd45393-d84e-4583-bc80-74bbb3709577
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1d79edb5ad1a60c5876163281ec5c1d1c17eff0a
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692809"
---
# <a name="manage-configuration-manager-clients-in-a-virtual-desktop-infrastructure-vdi"></a>Gestire i client di Configuration Manager in un'infrastruttura VDI (Virtual Desktop Infrastructure)

*Si applica a: Configuration Manager (Current Branch)*

Configuration Manager supporta l'installazione del client di Configuration Manager nei seguenti scenari di infrastruttura VDI:

- **Macchine virtuali personali**: la macchina virtuale (VM) conserva le impostazioni e i dati dell'utente tra le sessioni.

- **Sessioni di Servizi Desktop remoto**: ospitano più sessioni client simultanee in un server centralizzato. Gli utenti si connettono a una sessione ed eseguono le applicazioni su tale server.

- **Macchine virtuali in pool**: la macchina virtuale non viene mantenuta tra le sessioni. Quando un utente chiude una sessione, l'ambiente virtuale elimina tutti i dati e le impostazioni. Le macchine virtuali in pool sono utili quando non è possibile usare Servizi Desktop remoto. Ad esempio, se un'applicazione richiesta non può essere eseguita nel server Windows che ospita le sessioni client.

- **Desktop virtuale Windows**: un servizio di virtualizzazione di desktop e app eseguito su Microsoft Azure. A partire dalla versione 1906, usare Configuration Manager per gestire questi dispositivi virtuali che eseguono Windows in Azure.

## <a name="personal-vms"></a>Macchine virtuali personali

Configuration Manager considera le macchine virtuali personali in modo identico a un computer fisico. È possibile preinstallare il client di Configuration Manager nell'immagine della macchina virtuale o dopo il provisioning.

Per altre informazioni, vedere [Supporto per gli ambienti di virtualizzazione](../../../plan-design/configs/support-for-virtualization-environments.md).

## <a name="remote-desktop-services"></a>Servizi Desktop remoto

È opportuno non installare il client di Configuration Manager per singole sessioni di Desktop remoto. È preferibile installarlo una volta nel server che ospita Servizi Desktop remoto. È possibile usare tutte le funzionalità di Configuration Manager nel server di Servizi Desktop remoto.

Per altre informazioni, vedere [Introduzione a Servizi Desktop remoto](/windows-server/remote/remote-desktop-services/welcome-to-rds).

## <a name="pooled-vms"></a>Macchine virtuali in pool

Quando si rimuove una macchina virtuale in pool, vengono perse tutte le modifiche apportate da Configuration Manager.

Poiché la macchina virtuale potrebbe essere operativa solo per un breve periodo di tempo, alcune funzionalità di Configuration Manager potrebbero non restituire dati rilevanti. Ad esempio, l'inventario hardware e software e la misurazione del software. Prendere in considerazione l'esclusione delle macchine virtuali in pool dalle attività di inventario.

## <a name="windows-virtual-desktop"></a>Desktop virtuale Windows

Per altre informazioni, vedere [Sistemi operativi supportati per client e dispositivi](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop).

## <a name="other-considerations"></a>Altre considerazioni

Poiché la virtualizzazione supporta l'esecuzione di più client di Configuration Manager nello stesso computer fisico, molte operazioni client hanno un ritardo casuale incorporato per azioni pianificate. Ad esempio, l'inventario hardware e software, le scansioni antimalware, le installazioni software e le scansioni di aggiornamento software. Questo ritardo consente di distribuire l'elaborazione della CPU e il trasferimento dei dati per un server che ha più macchine virtuali con il client di Configuration Manager in esecuzione.

Ad eccezione dei client di Windows Embedded che sono in modalità di manutenzione, anche i client di Configuration Manager che non si trovano in ambienti virtualizzati usano il ritardo casuale. Questo comportamento consente di evitare i picchi nella larghezza di banda della rete. Consente inoltre di ridurre l'elaborazione della CPU sui sistemi del sito, ad esempio il punto di gestione e il server del sito. L'intervallo di ritardo varia in base alle funzionalità di Configuration Manager. Vedere, ad esempio, [Informazioni sulle impostazioni client - Disabilitare sequenza casuale scadenza](../about-client-settings.md#disable-deadline-randomization).

Per semplificare le prestazioni del client di Configuration Manager in ambienti virtuali che supportano più sessioni utente, i criteri utente vengono disabilitati per impostazione predefinita. A partire dalla versione 1910, è possibile abilitare i criteri utente in questo scenario. Per altre informazioni, vedere [Informazioni sulle impostazioni client - Abilitare i criteri utente per più sessioni utente](../about-client-settings.md#enable-user-policy-for-multiple-user-sessions).