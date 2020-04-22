---
title: Configuration Manager e Windows as a Service
titleSuffix: Configuration Manager
description: Ottenere informazioni di base sull'adozione di Configuration Manager Current Branch per supportare Windows come servizio.
ms.date: 06/15/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c8534a1e-57b8-4688-b6e6-299d82cfcec9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e92a39a91c60734f212c7d1e99e266d0ec9a4008
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701249"
---
# <a name="configuration-manager-and-windows-as-a-service"></a>Configuration Manager e Windows as a Service

*Si applica a: Configuration Manager (Current Branch)*

Configuration Manager offre un controllo completo sugli aggiornamenti delle funzionalità per Windows 10. Per adottare interamente il modello Windows come servizio, è necessario usare anche il modello Configuration Manager Current Branch. Perché Windows 10 sia aggiornato, è necessario che lo sia anche Configuration Manager per garantire un'ottima esperienza. Per poter sfruttare al meglio le straordinarie funzionalità aziendali di Windows 10, sono necessarie le nuove versioni di Configuration Manager. Questo articolo è considerato una pagina di destinazione per gli articoli principali relativi all'adozione di Configuration Manager Current Branch. Configuration Manager Current Branch consente di implementare Windows come servizio.

## <a name="key-articles-about-adopting-configuration-manager-current-branch"></a>Articoli principali sull'adozione di Configuration Manager Current Branch

| Articolo        | Descrizione          | 
| ------------- |-------------|
|[Panoramica di Configuration Manager Current Branch](../plan-design/changes/whats-new-incremental-versions.md)|Offre un breve riepilogo dei punti chiave del nuovo modello di manutenzione di Configuration Manager (Current Branch)|
|[Ciclo di vita del supporto](../servers/manage/current-branch-versions-supported.md)|Illustra il nuovo modello di supporto e manutenzione.|
|[Elementi rimossi e deprecati](../plan-design/changes/deprecated/removed-and-deprecated.md)|Anticipa informazioni sulle future modifiche che potrebbero influire sull'uso di Configuration Manager.|
|[Aggiornamenti per Configuration Manager Current Branch](../servers/manage/updates.md)|Illustra il semplice metodo nella console per applicare gli aggiornamenti delle funzionalità in Configuration Manager.|
|[Ottenere gli aggiornamenti disponibili](../servers/manage/install-in-console-updates.md#get-available-updates)|Illustra due modalità per ottenere nuovi aggiornamenti delle funzionalità di Configuration Manager.|
|[Elenco di controllo per l'aggiornamento](../servers/manage/install-in-console-updates.md#bkmk_beforeinstall)|Illustra gli elenchi di controllo per l'aggiornamento specifici della versione, se disponibili.| 
|[Installare nuovi aggiornamenti delle funzionalità di Configuration Manager](../servers/manage/install-in-console-updates.md#bkmk_install)|Illustra la semplice procedura di installazione degli aggiornamenti delle funzionalità.|
|[Supporto per Windows 10](../plan-design/configs/support-for-windows-10.md)|Offre una matrice di supporto per le versioni di Windows 10 (e ADK).|
|[Technical Preview per Configuration Manager](../get-started/technical-preview.md)|Offre informazioni sul programma di Technical Preview per Configuration Manager.|


## <a name="key-articles-about-adopting-windows-as-a-service"></a>Articoli principali sull'adozione di Windows as a Service

| Articolo        | Descrizione          |
| ------------- |-------------|
|[Gestire Windows come servizio](../../osd/deploy-use/manage-windows-as-a-service.md)|Spiega come usare i piani di manutenzione per distribuire gli aggiornamenti delle funzionalità di Windows 10.|
|[Aggiornare Windows 10 tramite la sequenza di attività](../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md)|Dettagli di creazione di una sequenza di attività per aggiornare Windows 10 con elementi consigliati aggiuntivi.|
|[Distribuzioni in più fasi](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)|Le distribuzioni in più fasi automatizzano un'implementazione coordinata e in sequenza di una sequenza di attività in più raccolte.|  
|[Ottimizzare il recapito degli aggiornamenti di Windows 10](../../sum/deploy-use/optimize-windows-10-update-delivery.md)|Usare Configuration Manager per gestire il contenuto di aggiornamento per rimanere aggiornati con Windows 10.|
|[Usare Desktop Analytics](../../desktop-analytics/overview.md)|Desktop Analytics consente di valutare e analizzare l'idoneità dei dispositivi nell'ambiente per un aggiornamento a Windows 10.|
|[Integrazione con Windows Update for Business in Windows 10](../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md)|Spiega come definire e distribuire i criteri di Windows Update per le aziende tramite Configuration Manager.|
|[Usare la co-gestione con Microsoft Intune e Windows Update per le aziende (facoltativo)](../../comanage/overview.md)|Offre una panoramica sulla co-gestione|


## <a name="related-articles"></a>Articoli correlati

- [Aggiornamento sul posto a Configuration Manager Current Branch da System Center 2012 Configuration Manager](../servers/deploy/install/upgrade-to-configuration-manager.md)
- [Pianificare la migrazione a Configuration Manager Current Branch](../migration/planning-for-migration.md)
