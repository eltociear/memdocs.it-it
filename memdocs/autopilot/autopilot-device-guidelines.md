---
title: Linee guida sui dispositivi di Windows Autopilot
ms.reviewer: ''
manager: laurawi
description: Informazioni sulle procedure consigliate per l'hardware, il firmware e il software per la distribuzione di Windows Autopilot.
keywords: MDM, installazione, Windows, Windows 10, OOBE, gestione, distribuzione, Autopilot, ZTD, zero-touch, partner, msfb, Intune
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: 328886f0fac3fad55c2e8bc26769784fd3d8b910
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/04/2020
ms.locfileid: "87757425"
---
# <a name="windows-autopilot-device-guidelines"></a>Linee guida sui dispositivi di Windows Autopilot

**Si applica a**

- Windows 10

## <a name="hardware-and-firmware-best-practice-guidelines-for-windows-autopilot"></a>Linee guida per le procedure consigliate per hardware e firmware per Windows Autopilot

Tutti i dispositivi usati con Windows Autopilot devono soddisfare i [requisiti hardware minimi](https://docs.microsoft.com/windows-hardware/design/minimum/minimum-hardware-requirements-overview) per Windows 10.  

Le procedure consigliate seguenti assicurano che i dispositivi possano essere facilmente sottoposti a provisioning come parte del processo di distribuzione di Windows Autopilot: 
- Verificare che il TPM 2,0 sia abilitato e in uno stato valido (non in **modalità funzionalità ridotta**) sui dispositivi destinati alla modalità di distribuzione automatica di Windows Autopilot.
- OEM effettua il provisioning delle informazioni di tupla univoche (SmbiosSystemManufacturer, SmbiosSystemProductName, SmbiosSystemSerialNumber) o PKID + SmbiosSystemSerialNumber nei [campi SMBIOS](https://docs.microsoft.com/windows-hardware/drivers/bringup/smbios) per specifica Microsoft (produttore, nome prodotto e numero di serie archiviato in SMBIOS Type 1 04h, tipo 1 05h e tipo 1 07h).
- L'OEM carica gli hash hardware 4K ottenuti usando lo strumento OA3 RS3 + Esegui in modalità di controllo su sistema operativo completo a Microsoft tramite il report CBR prima di distribuire i dispositivi a un cliente o a un partner del canale.
- Microsoft richiede che i driver di spedizione OEM siano pubblicati per Windows Update entro 30 giorni dall'invio del CBR. Gli aggiornamenti del firmware e del driver di sistema vengono pubblicati Windows Update entro 14 giorni.
- L'OEM garantisce che il PKID di cui è stato effettuato il provisioning in SMBIOS venga passato al canale.

## <a name="software-best-practice-guidelines-for-windows-autopilot"></a>Linee guida per le procedure consigliate del software per Windows Autopilot

- Il dispositivo Windows Autopilot deve essere preinstallato con solo un'immagine di base di Windows 10 e i driver.
- È possibile preinstallare la versione con licenza di Office, ad esempio [Microsoft 365 app per Enterprise](https://docs.microsoft.com/deployoffice/about-office-365-proplus-in-the-enterprise).
- A meno che non venga richiesto esplicitamente dal cliente, non devono essere inclusi altri software preinstallati.
  - Per ogni criterio OEM, le funzionalità di Windows 10, incluse le app predefinite, non devono essere disabilitate o rimosse.

## <a name="related-topics"></a>Argomenti correlati

[Consenso del cliente di Windows Autopilot](registration-auth.md)<br>
[Informazioni aggiuntive sullo scenario di sostituzione della motherboard](autopilot-mbr.md)<br>