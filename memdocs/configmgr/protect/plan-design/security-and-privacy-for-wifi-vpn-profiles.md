---
title: Sicurezza e privacy per i profili Wi-Fi e VPN
titleSuffix: Configuration Manager
description: Informazioni sulle prassi di sicurezza consigliate per gestire i profili Wi-Fi e VPN per i dispositivi in Configuration Manager.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: ef3ab519-9cf7-47fc-8831-d400e0e96df8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a6f444e35e16a3b42414fdc6fbee50687cf76f2f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705979"
---
# <a name="security-and-privacy-for-wi-fi-and-vpn-profiles-in-configuration-manager"></a>Protezione e privacy per i profili Wi-Fi e VPN in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

## <a name="security-recommendations"></a>Suggerimenti relativi alla sicurezza

Usare le procedure di sicurezza consigliate seguenti per gestire i profili Wi-Fi e VPN per i dispositivi.

### <a name="choose-the-most-secure-options-that-your-wi-fi-and-vpn-infrastructure-and-client-operating-systems-can-support"></a>Se possibile, scegliere le opzioni più sicure supportate dall'infrastruttura Wi-Fi e VPN e dai sistemi operativi client

I profili Wi-Fi e VPN rappresentano un metodo pratico per distribuire e gestire in modo centralizzato le impostazioni Wi-Fi e VPN già supportate dai dispositivi in uso. Configuration Manager non aggiunge funzionalità Wi-Fi o VPN. Identificare, implementare e seguire le raccomandazioni sulla sicurezza per i dispositivi e l'infrastruttura.

## <a name="privacy-information"></a>Informazioni sulla privacy

È possibile usare i profili Wi-Fi e VPN per configurare i dispositivi client per la connessione ai server Wi-Fi e VPN. Usare quindi Configuration Manager per valutare se i dispositivi diventano conformi dopo che i profili sono stati applicati. Il punto di gestione invia informazioni sulla conformità al server del sito e le informazioni vengono memorizzate nel database del sito. Le informazioni vengono crittografate quando i dispositivi le inviano al punto di gestione, ma non vengono archiviate in formato crittografato nel database del sito. Il database conserva le informazioni fino a quando l'attività di manutenzione del sito **Elimina dati di gestione configurazione obsoleti** le elimina. L'intervallo di eliminazione predefinito è 90 giorni, ma è possibile modificarlo. Le informazioni sulla conformità non vengono inviate a Microsoft.

Per impostazione predefinita, i dispositivi non valutano i profili Wi-Fi e VPN. È necessario anche configurare i profili e quindi distribuirli agli utenti.  

Prima di configurare i profili Wi-Fi e VPN, considerare i requisiti sulla privacy.  
