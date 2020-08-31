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
ms.openlocfilehash: eb591206ad61878bc2637bf1a10c2a1cec17ddba
ms.sourcegitcommit: 41e6e6b7f5c2a87aaf7f23d90d0f175dd63c0579
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2020
ms.locfileid: "89057363"
---
# <a name="windows-autopilot-device-guidelines"></a>Linee guida sui dispositivi di Windows Autopilot

**Si applica a**

- Windows 10

## <a name="hardware-and-firmware-best-practice-guidelines-for-windows-autopilot"></a>Linee guida per le procedure consigliate per hardware e firmware per Windows Autopilot

Tutti i dispositivi che usano Windows Autopilot devono soddisfare i [requisiti hardware minimi](/windows-hardware/design/minimum/minimum-hardware-requirements-overview) per Windows 10.  

Le procedure consigliate seguenti assicurano che i dispositivi possano essere facilmente sottoposti a provisioning come parte del processo di distribuzione di Windows Autopilot: 
- TPM 2,0 è abilitato e in uno stato valido (non in **modalità funzionalità ridotta**) sui dispositivi destinati alla modalità di distribuzione automatica di Windows Autopilot.
- L'OEM deve effettuare il provisioning di una delle seguenti informazioni nei [campi SMBIOS](/windows-hardware/drivers/bringup/smbios). Le informazioni devono seguire le specifiche Microsoft (produttore, nome prodotto e numero di serie archiviato in SMBIOS Type 1 04h, digitare 1 05h e digitare 1 07h).
    - Informazioni univoche sulla tupla (SmbiosSystemManufacturer, SmbiosSystemProductName, SmbiosSystemSerialNumber)
    - PKID + SmbiosSystemSerialNumber
- Prima di distribuire i dispositivi a un cliente o a un partner di canale di Autopilot, l'OEM dovrebbe caricare gli hash hardware 4K a Microsoft usando il report CBR. Gli hash devono essere raccolti usando lo strumento OA3 RS3 + Esegui in modalità di controllo sul sistema operativo completo.
- Microsoft richiede che i driver di spedizione OEM vengano pubblicati per Windows Update entro 30 giorni dalla data di invio CBR. Gli aggiornamenti del firmware e del driver di sistema vengono pubblicati Windows Update entro 14 giorni.
- L'OEM garantisce che il PKID di cui è stato effettuato il provisioning in SMBIOS venga passato al canale.

## <a name="software-best-practice-guidelines-for-windows-autopilot"></a>Linee guida per le procedure consigliate del software per Windows Autopilot

- Il dispositivo Windows Autopilot deve essere preinstallato con solo un'immagine di base di Windows 10 e i driver.
- È possibile preinstallare la versione con licenza di Office, ad esempio [Microsoft 365 app per Enterprise](/deployoffice/about-office-365-proplus-in-the-enterprise).
- A meno che non venga richiesto esplicitamente dal cliente, non devono essere inclusi altri software preinstallati.
  - Per ogni criterio OEM, le funzionalità di Windows 10, incluse le app predefinite, non devono essere disabilitate o rimosse.

## <a name="next-steps"></a>Passaggi successivi

[Consenso del cliente di Windows Autopilot](registration-auth.md)<br>
[Informazioni aggiuntive sullo scenario di sostituzione della motherboard](autopilot-mbr.md)<br>