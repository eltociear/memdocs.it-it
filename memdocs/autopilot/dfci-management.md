---
title: Gestione DFCI
ms.reviewer: ''
manager: laurawi
description: Con la distribuzione di Windows Autopilot e Intune, è possibile gestire le impostazioni UEFI (BIOS) dopo che sono state registrate usando l'interfaccia di configurazione del firmware del dispositivo (DFCI)
keywords: Autopilot, DFCI, UEFI, Windows 10
ms.technology: windows
ms.prod: w10
ms.mktglfcycl: deploy
ms.sitesec: library
ms.pagetype: deploy
ms.localizationpriority: medium
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: 95979a3c53752bb77c31710e20de54dbc2781262
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/09/2020
ms.locfileid: "89606614"
---
# <a name="device-firmware-configuration-interface-dfci-management"></a>Gestione DFCI (device firmware Configuration Interface)

**Si applica a**

- Windows 10

Con la distribuzione di Windows Autopilot e Intune, è possibile gestire le impostazioni di Unified Extensible Firmware Interface (UEFI) dopo che sono state registrate usando device firmware Configuration Interface (DFCI). DFCI [consente a Windows di passare i comandi di gestione](/windows/client-management/mdm/uefi-csp) da INTUNE a UEFI per i dispositivi Autopilot distribuiti. Questa funzionalità consente di limitare il controllo dell'utente finale sulle impostazioni del BIOS. Ad esempio, è possibile bloccare le opzioni di avvio per impedire agli utenti di avviare un altro sistema operativo, ad esempio uno che non ha le stesse funzionalità di sicurezza.

Se un utente reinstalla una versione precedente di Windows, installare un sistema operativo separato o formattare il disco rigido, non può eseguire l'override della gestione DFCI. Questa funzionalità può anche impedire al malware di comunicare con processi del sistema operativo, inclusi processi del sistema operativo elevati. La catena di attendibilità di DFCI usa la crittografia a chiave pubblica e non dipende dalla sicurezza delle password UEFI locale. Questo livello di sicurezza impedisce agli utenti locali di accedere alle impostazioni gestite dai menu UEFI del dispositivo.

Per una panoramica di vantaggi, scenari e prerequisiti di DFCI, vedere Introduzione a [Device Firmware Configuration Interface (DFCI)](https://microsoft.github.io/mu/dyn/mu_plus/DfciPkg/Docs/Dfci_Feature/).

## <a name="dfci-management-lifecycle"></a>Ciclo di vita della gestione DFCI

Il ciclo di vita di gestione di DFCI include i processi seguenti:
- Integrazione UEFI
- Registrazione del dispositivo
- Creazione del profilo
- Registrazione
- Gestione
- Ritiro
- Ripristino

Vedere la figura seguente.

 ![Ciclo di vita](images/dfci.png)

## <a name="requirements"></a>Requisiti

- È necessario Windows 10, versione 1809 o successiva e un UEFI supportato.
- Il produttore del dispositivo deve avere DFCI aggiunto al firmware UEFI nel processo di produzione oppure come aggiornamento del firmware che si installa. Collaborare con i fornitori di dispositivi per determinare i [produttori che supportano DFCI](#oems-that-support-dfci)o la versione del firmware necessaria per l'uso di DFCI.
- Il dispositivo deve essere gestito con Microsoft Intune. Per altre informazioni, vedere [registrare i dispositivi Windows in Intune con Windows Autopilot](/intune/enrollment/enrollment-autopilot).
- Il dispositivo deve essere registrato per Windows Autopilot da un [partner Microsoft Cloud Solution Provider (CSP)](https://partner.microsoft.com/membership/cloud-solution-provider) o registrato direttamente dall'OEM. 

>[!IMPORTANT]
>I dispositivi registrati manualmente per Autopilot, ad esempio tramite [l'importazione da un file CSV](/intune/enrollment/enrollment-autopilot#add-devices), non possono usare DFCI. Per impostazione predefinita, la gestione DFCI richiede l'attestazione esterna dell'acquisizione commerciale del dispositivo tramite un OEM o una registrazione di partner Microsoft CSP per Windows Autopilot. Quando il dispositivo è registrato, il numero di serie viene visualizzato nell'elenco dei dispositivi Windows Autopilot.

## <a name="managing-dfci-profile-with-windows-autopilot"></a>Gestione del profilo DFCI con Windows Autopilot

Per la gestione del profilo DFCI con Windows Autopilot sono necessari quattro passaggi di base:

1. Creare un profilo di Autopilot
2. Creare un profilo della pagina relativa allo stato della registrazione
3. Creare un profilo DFCI
4. Assegnare i profili

Vedere [creare i profili](/intune/configuration/device-firmware-configuration-interface-windows#create-the-profiles) e [assegnare i profili e riavviare](/intune/configuration/device-firmware-configuration-interface-windows#assign-the-profiles-and-reboot) per i dettagli.

È anche possibile [modificare le impostazioni di DFCI esistenti](/intune/configuration/device-firmware-configuration-interface-windows#update-existing-dfci-settings) nei dispositivi in uso. Nel profilo DFCI esistente modificare le impostazioni e salvare le modifiche. Poiché il profilo è già assegnato, le nuove impostazioni di DFCI diventano effettive alla successiva sincronizzazione del dispositivo o al riavvio del dispositivo.

## <a name="oems-that-support-dfci"></a>OEM che supportano DFCI

- [Microsoft Surface](/surface/surface-manage-dfci-guide)

Sono in sospeso altri OEM.

## <a name="see-also"></a>Vedi anche

[Scenari di Microsoft DFCI](https://microsoft.github.io/mu/dyn/mu_plus/DfciPkg/Docs/Scenarios/DfciScenarios/)<br>
[Dispositivi Windows Autopilot e Surface](/surface/windows-autopilot-and-surface-devices)<br>
