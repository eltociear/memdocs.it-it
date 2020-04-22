---
title: Sicurezza e privacy per il risparmio energia
titleSuffix: Configuration Manager
description: Informazioni sulla sicurezza e la privacy per il risparmio energia in Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 469ff35f-59a1-484d-902b-107dd6070baf
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: c019faee1ffa035bde626778bb15b8f5feabc243
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696509"
---
# <a name="security-and-privacy-for-power-management-in-configuration-manager"></a>Sicurezza e privacy per il risparmio energia in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Questa sezione contiene informazioni sulla sicurezza e la privacy per il risparmio energia in Configuration Manager.  

## <a name="security-best-practices-for-power-management"></a>Procedure di sicurezza consigliate per il risparmio energia  
 Non esistono procedure consigliate correlate alla sicurezza per il risparmio energia.  

## <a name="privacy-information-for-power-management"></a>Informazioni sulla privacy per il risparmio energia  
 Risparmio di energia utilizza le funzionalità integrate di Windows per monitorare l'utilizzo di energia e applicare impostazioni di risparmio energia per computer durante le ore lavorative e le ore non lavorative. Configuration Manager raccoglie informazioni sul consumo di energia dai computer, compresi i dati relativi agli orari di uso dei computer da parte degli utenti. Anche se Configuration Manager esegue il monitoraggio del consumo di energia per una raccolta anziché per i singoli computer, una raccolta può contenere un solo computer. La funzionalità di risparmio energia non è abilitata per impostazione predefinita e deve essere configurata da un amministratore.  

 Le informazioni relative al consumo di energia vengono archiviate nel database di Configuration Manager e non vengono inviate a Microsoft. Informazioni dettagliate vengono conservate nel database per 31 giorni e le informazioni riepilogative vengono conservate per 13 mesi. Non è possibile configurare l'intervallo di eliminazione.  

 Prima di configurare il risparmio energia, prendere in considerazione i requisiti in vigore relativi alla privacy.  
