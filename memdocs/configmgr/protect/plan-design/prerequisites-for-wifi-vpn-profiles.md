---
title: Prerequisiti per i profili Wi-Fi e VPN
titleSuffix: Configuration Manager
description: Informazioni sui prerequisiti per gestire i profili Wi-Fi e VPN in Configuration Manager
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: d2dacb2d-ab3b-42a2-8dc8-94da31f993c2
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9e7a557bab6b41be6e6335e3aa2744e8627d285b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706069"
---
# <a name="prerequisites-for-wi-fi-and-vpn-profiles-in-configuration-manager"></a>Prerequisiti per i profili Wi-Fi e VPN in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

I profili Wi-Fi e VPN in Configuration Manager hanno solo dipendenze nel prodotto.

Per gestire le impostazioni di accesso alle risorse aziendali, quali profili certificato, Wi-Fi e VPN, sono necessarie le autorizzazioni di sicurezza seguenti:  

- Per visualizzare e gestire avvisi e report per i profili Wi-Fi e VPN: **Crea**, **Elimina**, **Modifica**, **Modifica report**, **Lettura** ed **Esegui report** per l'oggetto **Avvisi**.  

- Per creare e gestire i profili certificato: **Criteri autore**, **Modifica report**, **Lettura** ed **Esegui report** per l'oggetto **Profilo certificato**.  

- Per gestire le distribuzioni dei profili Wi-Fi, certificato e VPN: **Distribuisci criteri di configurazione**, **Modifica avviso stato client**, **Lettura** e **Leggi risorsa** per l'oggetto **Raccolta**.  

- Per gestire tutti i criteri di configurazione: **Crea**, **Elimina**, **Modifica**, **Lettura** e **Imposta ambito di protezione** per l'oggetto **Criteri di configurazione**.  

- Per eseguire query correlate ai profili Wi-Fi e VPN: autorizzazione **Lettura** per l'oggetto **Query**.  

- Per visualizzare le informazioni relative ai profili Wi-Fi e VPN nella console di Configuration Manager: Autorizzazione **Lettura** per l'oggetto **Sito**.  

- Per visualizzare i messaggi di stato per i profili Wi-Fi e VPN: autorizzazione **Lettura** per l'oggetto **Messaggi di stato**.  

- Per creare e modificare il profilo certificato CA attendibile: **Criteri autore**, **Modifica report**, **Lettura** ed **Esegui report** per l'oggetto **Profilo certificato CA attendibile**.  

- Per creare e gestire i profili VPN: **Criteri autore**, **Modifica report**, **Lettura** ed **Esegui report** per l'oggetto **Profilo VPN**.  

- Per creare e gestire i profili Wi-Fi: **Criteri autore**, **Modifica report**, **Lettura** ed **Esegui report** per l'oggetto **Profilo Wi-Fi**.  

Il ruolo di sicurezza predefinito **Gestione accesso risorse aziendali** include queste autorizzazioni necessarie per gestire i profili Wi-Fi in Configuration Manager. Per altre informazioni, vedere [Configurare la sicurezza](../../core/plan-design/security/configure-security.md).
