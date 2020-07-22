---
title: Versioni di Technical Preview
titleSuffix: Configuration Manager
description: Informazioni sulla versione Technical Preview che consente di testare nuove funzionalità e capacità in Configuration Manager.
ms.date: 07/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 64e784ec7313dfa778ee39f6e1f52e7c09fcfd95
ms.sourcegitcommit: 488db8a6ab272f5d639525d70718145c63d0de8f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/14/2020
ms.locfileid: "86384826"
---
# <a name="technical-preview-for-configuration-manager"></a>Technical Preview per Configuration Manager

*Si applica a: Configuration Manager (Technical Preview Branch)*

Questo articolo include informazioni dettagliate sul ramo Technical Preview mensile di Configuration Manager. La versione Technical Preview introduce nuove funzionalità su cui Microsoft sta lavorando. Vengono introdotte nuove funzionalità non ancora incluse in Current Branch di Configuration Manager. Queste funzionalità potrebbero essere alla fine incluse in un aggiornamento a Current Branch. Prima di finalizzare le funzionalità, Microsoft invita gli utenti a provarle e a inviare commenti e suggerimenti.

Poiché questa versione è una Technical Preview, dettagli e funzionalità sono soggetti a modifiche.

Queste informazioni si applicano a tutte le versioni del ramo Technical Preview di Configuration Manager. Questo articolo elenca ogni nuova funzionalità insieme alla versione Technical Preview in cui compare per la prima volta. Ad esempio, la versione **2001** per gennaio (`01`) del 2020 (`20`). Le singole funzionalità sono descritte in dettaglio in articoli separati dedicati a ogni versione di anteprima.

Per informazioni sulle novità della versione *Current Branch* di Configuration Manager, vedere [Novità delle versioni incrementali di Configuration Manager](../plan-design/changes/whats-new-incremental-versions.md).

> [!Tip]
> Per ricevere una notifica quando questa pagina viene aggiornata, copiare e incollare l'URL seguente nel lettore di feed RSS: `https://docs.microsoft.com/api/search/rss?search=%22technical+preview+releases+-+Configuration+Manager%22&locale=en-us`

## <a name="requirements-and-limitations"></a><a name="bkmk_reqs"></a> Requisiti e limitazioni

> [!IMPORTANT]
> La Technical Preview viene concessa in licenza per essere usata esclusivamente in un ambiente lab. Microsoft potrebbe non offrire supporto tecnico e alcune funzionalità potrebbero non essere disponibili nelle anteprime tecniche. Inoltre, il software in anteprima tecnica può essere caratterizzato da standard di sicurezza, privacy, accessibilità, disponibilità e affidabilità ridotti o diversi rispetto al software commercializzato.

Per la maggior parte dei prerequisiti del prodotto, usare le informazioni in [Configurazioni supportate](../plan-design/configs/supported-configurations.md). Per il ramo Technical Preview si applicano le eccezioni seguenti:

- Ogni installazione rimane attiva per 90 giorni prima di diventare inattiva.

- L'inglese è l'unica lingua supportata.

- Supporta solo i parametri della riga di comando di installazione seguenti:

  - `/silent`
  - `/testdbupgrade`

- Il punto di connessione del servizio viene installato in modalità online. e non supporta la modalità offline.

- Gli articoli separati per ogni versione specifica della Technical Preview includono ulteriori limitazioni o requisiti, secondo il caso.

- Le funzionalità seguenti non sono supportate con il ramo Technical Preview:

  - [Migrazione](../migration/migrate-data-between-hierarchies.md) da o verso questo ramo di anteprima.

  - [Aggiornamento](../servers/deploy/install/upgrade-to-configuration-manager.md) a questo ramo di anteprima.

  - [Ripristino di siti](../servers/manage/recover-sites.md) dalla cartella cd.latest.<!--507106-->

- Non è previsto alcun supporto per l'aggiornamento a Current Branch da questo ramo di anteprima.

    > [!Note]
    > Se sono disponibili aggiornamenti per una versione di anteprima, è ancora possibile trovarli e installarli dal nodo **Aggiornamenti e manutenzione** della console di Configuration Manager. Per un video relativo al processo di aggiornamento nella console, vedere [Installing Configuration Manager update packages](https://www.youtube.com/embed/KBd_EGFbUT8) (Installazione dei pacchetti di aggiornamento di Configuration Manager) su youtube.com.

- Supporta solo un sito primario autonomo. Non è disponibile alcun supporto per un sito di amministrazione centrale, più siti primari o i siti secondari.

I prodotti e tecnologie seguenti sono supportati dal ramo Technical Preview di Configuration Manager:

- Se non specificato diversamente, Technical Preview Branch supporta le stesse versioni di SQL Server di Current Branch. Per altre informazioni, vedere [Versioni di SQL Server supportate](../plan-design/configs/support-for-sql-server-versions.md).

- Il sito supporta fino a 10 client, che possono eseguire qualsiasi [versione supportata del sistema operativo client](../plan-design/configs/supported-operating-systems-for-clients-and-devices.md).<!-- SCCMDocs#1656 -->

> [!Note]
> L'inclusione di questi prodotti in questo contenuto non implica un'estensione del supporto per una versione oltre il ciclo di vita del supporto. Configuration Manager non supporta prodotti che non rientrano nel ciclo di vita del supporto. Per altre informazioni, vedere [Criteri relativi al ciclo di vita Microsoft](https://support.microsoft.com/lifecycle).

## <a name="install-and-update"></a><a name="bkmk_install"></a> Installare e aggiornare

Il ramo Technical Preview di Configuration Manager per l'uso in ambienti lab è diverso da Current Branch di Configuration Manager per l'uso in ambienti di produzione.

Prima di tutto installare una versione di base del ramo Technical Preview. Dopo l'installazione di una versione di base, eseguire gli aggiornamenti nella console per aggiornare l'installazione con la versione di anteprima più recente. In genere, le nuove versioni Technical Preview sono disponibili ogni mese.

Microsoft supporta ogni versione Technical Preview fino a quando diventano disponibili tre versioni successive. Ad esempio, quando è stata rilasciata la versione 1908, la versione 1904 è stata esclusa dal supporto. Le versioni 1905, 1906 e 1907 sono invece rimaste. Quando una versione di base non è più inclusa nel supporto, è ancora supportata per l'installazione di un nuovo sito Technical Preview, presupponendo che venga eseguito l'aggiornamento immediato a una versione supportata. La versione di base precedente è supportata fino a quando non diventa disponibile una nuova versione di base. Eseguire l'aggiornamento alla versione più recente disponibile dalla versione di base e quindi ripetere il processo di aggiornamento fino a installare l'ultima versione Technical Preview.

> [!TIP]
> Quando si installa un aggiornamento della Technical Preview, si aggiorna l'installazione di anteprima alla nuova versione Technical Preview. Un'installazione Technical Preview non prevede mai la possibilità di eseguire l'aggiornamento a un'installazione Current Branch, né di ricevere gli aggiornamenti dalla versione Current Branch corrente.
>
> Più volte nel corso dell'anno diventano disponibili versioni del ramo Technical Preview e Current Branch con lo stesso numero di versione. Ad esempio, una versione Technical Preview 1910 e una versione Current Branch 1910.

### <a name="active-baseline-versions"></a>Versioni di base attive

È possibile installare una versione di base al massimo per un anno dopo il rilascio. Quando si installa un nuovo sito Technical Preview usare la versione di base più recente. Le versioni seguenti di Configuration Manager Technical Preview Branch sono disponibili sia come aggiornamenti della console sia come nuove versioni di base:

- **Technical Preview versione 2007**
- **Technical Preview versione 2002**

Scaricare una versione di base da [Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).

## <a name="providing-feedback"></a><a name="BKMK_TPFeedback"></a> Invio di commenti e suggerimenti

Microsoft sarebbe lieta di ricevere commenti e suggerimenti sulle nuove funzionalità della Technical Preview. Per altre informazioni, vedere la sezione su [commenti e suggerimenti per i prodotti](../understand/find-help.md#product-feedback).

Microsoft è interessata a conoscere le idee degli utenti su nuove funzionalità che potrebbero essere implementate. È possibile inviare nuove idee e votare le idee di altri utenti: [UserVoice per Configuration Manager](https://configurationmanager.uservoice.com).

<!--
## <a name="bdmk_tpknownissues"></a> General changes introduced in technical preview branch

<!-- (explanatory comment)
Enable this section if needed to include any broad change to the tech preview branch
-->

## <a name="features-in-the-most-recent-version"></a><a name="bkmk_tpCaps"></a> Funzionalità nella versione più recente

<!-- (explanatory comment)
This is the full list of new features in the latest TP release

bullet format:
<!-- - [title](2020/technical-preview-2007.md) <!--ID-->

Le funzionalità seguenti sono disponibili con la versione Technical Preview di Configuration Manager più recente:

### <a name="technical-preview-version-2007"></a>Technical Preview versione 2007

- [Collegamento di tenant: Visualizzare l'inventario hardware nell'interfaccia di amministrazione di Microsoft Endpoint Manager](2020/technical-preview-2007.md#bkmk_mem) <!--6479284-->
- [Miglioramenti al dashboard origini dati client](2020/technical-preview-2007.md#bkmk_content) <!--7102084-->
- [Tipo di carattere a larghezza fissa attualmente usato in alcune aree della console](2020/technical-preview-2007.md#bkmk_font) <!--7632637-->
- [Gestione delle dimensioni dei criteri per le sequenze di attività](2020/technical-preview-2007.md#bkmk_tspol) <!--6888853-->
- [Miglioramenti alla sequenza temporale del dispositivo nell'interfaccia di amministrazione](2020/technical-preview-2007.md#bkmk_timeline)<!--7141381-->

> [!NOTE]
> Le funzionalità disponibili in una versione precedente della Technical Preview rimangono disponibili nelle versioni successive. Analogamente, le funzionalità aggiunte alla versione Current Branch di Configuration Manager rimangono disponibili nel ramo Technical Preview.

## <a name="features-in-recent-technical-previews"></a>Funzionalità nelle anteprime tecniche recenti

<!-- (explanatory comment)
This is the full list of new features in the past TP releases since the last CB release.
Each month, add features from the list above to a new H3 section at the top of this section.
When there's a new CB, add any features not in that CB to the table in H2 "Features in previous technical previews"
-->

Le funzionalità seguenti sono state rilasciate in versioni precedenti della Technical Preview Branch di Configuration Manager dopo la versione Current Branch 2002:

> [!TIP]
> Quando è disponibile una nuova versione Current Branch, le funzionalità presenti in tale versione sono elencate nella versione più recente dell'articolo *Novità*. Per altre informazioni, vedere [Novità delle versioni incrementali](../plan-design/changes/whats-new-incremental-versions.md#supported-versions).

### <a name="technical-preview-version-2006"></a>Technical Preview versione 2006

- [Usare l'app Portale aziendale in dispositivi con co-gestione](2020/technical-preview-2006.md#bkmk_portal) <!--3601237-->
- [Miglioramenti alle app disponibili tramite CMG](2020/technical-preview-2006.md#bkmk_availapp) <!--7033501-->
- [I client Intranet possono usare un punto di aggiornamento software CMG](2020/technical-preview-2006.md#bkmk_cmg-sup) <!--7102873-->
- [Miglioramenti alle sequenze di attività tramite CMG](2020/technical-preview-2006.md#bkmk_osdcmg) <!--6983320-->
- [Informazioni dettagliate sulla gestione per l'ottimizzazione dei ruoli di lavoro remoti](2020/technical-preview-2006.md#bkmk_wfhmi) <!--6982226-->
- [Miglioramenti al tipo di limite VPN](2020/technical-preview-2006.md#bkmk_vpn) <!--7020519-->
- [Collegamento di tenant: miglioramenti alle azioni di Configuration Manager nell'interfaccia di amministrazione di Microsoft Endpoint Manager](2020/technical-preview-2006.md#bkmk_apps) <!--7518897-->
- [Supporto di CMG per i criteri di protezione endpoint](2020/technical-preview-2006.md#bkmk_epcmg) <!--4773948-->
- [Importare un'applicazione di Azure AD creata in precedenza durante l'onboarding del collegamento al tenant](2020/technical-preview-2006.md#bkmk_aad-app) <!--6479246-->
- [Miglioramenti dell'aggiornamento client in una connessione a consumo](2020/technical-preview-2006.md#bkmk_meter) <!--6976145-->
- [Miglioramenti alla gestione dei riavvii dei dispositivi](2020/technical-preview-2006.md#bkmk_restart) <!--3601213-->
- [Miglioramenti al supporto per Desktop virtuale Windows](2020/technical-preview-2006.md#bkmk_wvd) <!--6527576-->
- [Collegamenti diretti agli elementi dell'hub della community di Configuration Manager](2020/technical-preview-2006.md#bkmk_deeplink) <!--4224406-->

### <a name="technical-preview-version-2005"></a>Technical Preview versione 2005

- [Collegamento di tenant: sequenza temporale del dispositivo nell'interfaccia di amministrazione](2020/technical-preview-2005.md#bkmk_timeline) <!--7141381-->
- [Collegamento di tenant: installare un'applicazione dall'interfaccia di amministrazione](2020/technical-preview-2005.md#bkmk_apps) <!--6024389-->
- [Collegamento di tenant: CMPivot dall'interfaccia di amministrazione](2020/technical-preview-2005.md#bkmk_cmpivot) <!--6024392-->
- [Collegamento di tenant: eseguire gli script dall'interfaccia di amministrazione](2020/technical-preview-2005.md#bkmk_scripts) <!--6234688-->
- [Tipo di limite VPN](2020/technical-preview-2005.md#bkmk_vpn) <!--7020519-->
- [Autenticazione di Azure AD in Software Center](2020/technical-preview-2005.md#bkmk_availapp) <!--6935376-->
- [Installare e aggiornare il client in una connessione a consumo](2020/technical-preview-2005.md#bkmk_meter) <!--6976145-->
- [Supporto per la sequenza di attività per i contenuti basati su cloud](2020/technical-preview-2005.md#bkmk_tsmedia) <!--6209223-->
- [Miglioramenti dei cmdlet di Cloud Management Gateway](2020/technical-preview-2005.md#bkmk_pwshcmg) <!--6978300-->
- [Hub della community e GitHub](2020/technical-preview-2005.md#community-hub-and-github) <!--3555935-->
- [Microsoft 365 Apps for enterprise](2020/technical-preview-2005.md#bkmk_365_apps) <!--6298093-->
- [Segnalare a Microsoft errori di configurazione e aggiornamento](2020/technical-preview-2005.md#report-setup-and-upgrade-failures-to-microsoft) <!--5622909-->
- [Notifica di scadenza della chiave privata dell'app Azure AD](2020/technical-preview-2005.md#bkmk_alertkey) <!--6386392-->
- [Miglioramenti dei passaggi della sequenza di attività di BitLocker](2020/technical-preview-2005.md#bkmk_tsbitlocker) <!--6995601-->
- [Miglioramenti dello strumento di pulizia della raccolta contenuto](2020/technical-preview-2005.md#bkmk_content) <!--6887878-->
- [Rimuovere il prompt dei comandi durante l'aggiornamento sul posto di Windows 10](2020/technical-preview-2005.md#bkmk_ipucmd) <!--2837795-->

### <a name="technical-preview-version-2004"></a>Technical Preview versione 2004

- [Collegamento del tenant di Microsoft Endpoint Manager: dettagli client ConfigMgr](2020/technical-preview-2004.md#bkmk_mem) <!--6374854-->
- [Notifiche da Microsoft](2020/technical-preview-2004.md#notifications-from-microsoft) <!--3953121-->
- [Copiare i dati di individuazione dalla console](2020/technical-preview-2004.md#bkmk_copydisco) <!--6890051-->
- [Miglioramenti di CMPivot](2020/technical-preview-2004.md#improvements-to-cmpivot) <!--6518631-->
- [Supporto per PowerShell versione 7](2020/technical-preview-2004.md#bkmk_pwsh7) <!--6023299-->
- [Miglioramento del passaggio Formato e disco partizione della sequenza di attività](2020/technical-preview-2004.md#bkmk_osdpart) <!--6610288-->
- [Regole di dati analitici per la gestione per la distribuzione del sistema operativo](2020/technical-preview-2004.md#bkmk_osdmi) <!--6982275-->
- [Cmdlet di PowerShell per i tipi di distribuzione della sequenza di attività](2020/technical-preview-2004.md#bkmk_osdpwsh) <!--7019342-->

### <a name="technical-preview-version-2003"></a>Technical Preview versione 2003

- [Eseguire l'onboarding di client di Configuration Manager in Microsoft Defender ATP tramite la console di Microsoft Endpoint Manager](2020/technical-preview-2003.md#bkmk_atp) <!--5691658-->
- [Tenere traccia delle correzioni per gli elementi di configurazione](2020/technical-preview-2003.md#bkmk_track) <!--4261411 in 2002-->
- [Visualizzare i gruppi di limiti per i dispositivi](2020/technical-preview-2003.md#bkmk_boundary) <!--6521835 in 2002-->
- [Nuova procedura guidata per l'invio di commenti e suggerimenti](2020/technical-preview-2003.md#bkmk_feedback) <!--3180826-->
- [Miglioramenti al dashboard Gestione di Microsoft Edge](2020/technical-preview-2003.md#bkmk_edge) <!--5907383-->
- [Miglioramenti di CMPivot](2020/technical-preview-2003.md#bkmk_cmpivot) <!--6518631-->
- [Query per i commenti e suggerimenti inviati a Microsoft](2020/technical-preview-2003.md#bkmk_smile) <!--6488450-->
- [Nuovo metodo SDK per lo stato della sequenza di attività](2020/technical-preview-2003.md#bkmk_tsapi) <!--6448458-->
- [Miglioramenti alla distribuzione del sistema operativo](2020/technical-preview-2003.md#bkmk_osd) <!--6452769-->

## <a name="features-in-previous-technical-previews"></a>Funzionalità nelle versioni Technical Preview precedenti

<!-- (explanatory comment)
This is the list of individual features that are still in TP (not in CB). 
Copy from the lists above any individual features that are still in TP and add to the top of this list
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

Le funzionalità seguenti sono state rilasciate con le versioni precedenti del ramo Technical Preview di Configuration Manager. Queste funzionalità rimangono disponibili nelle versioni successive, ma non sono ancora disponibili in Current Branch.

| Funzionalità        | Versione Technical Preview |
|----------------|---------------------------|
| Allegare file al feedback <!--3556011--> | [Tech Preview 1910](2019/technical-preview-1910.md#attach-files-to-feedback) |
| Miglioramenti ai punti di distribuzione abilitati per il multicast <!--3785535--> | [Tech Preview 1908.2](2019/technical-preview-1908-2.md#bkmk_multicast) |
| Modelli di distribuzione in più fasi <!--4961086--> | [Tech Preview 1908](2019/technical-preview-1908.md#phased-deployment-templates) |
| Controllo remoto tramite il gateway di gestione cloud <!--4575930--> | [Tech Preview 1906](2019/technical-preview-1906.md#remote-control-anywhere-using-cloud-management-gateway) |
| Miglioramento dell'hub della community <!--3555935--> | [Tech Preview 1906](2019/technical-preview-1906.md#bkmk_hub) |
| Miglioramento dell'hub della community <!--4224401--> | [Anteprima tecnica 1905](2019/technical-preview-1905.md#bkmk_hub) |
| Hub della community e GitHub <!--3555935--> | [Tech Preview 1904](2019/technical-preview-1904.md#community-hub-and-github) |
| Stima dei costi dei servizi cloud <!--3555774--> | [Tech Preview 1903](2019/technical-preview-1903.md#bkmk_cmg) |
| Scaricare report dall'hub della community <!--3555936--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_hub) |
| Hub della community <!--3556020, fka 1357766--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_hub) |
| Servizio risponditore PXE basato su client <!--3556018, fka 1357148--> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
| Supporto dell'avvio della rete PXE per IPv6 <!--3601254, fka 1269793--> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
| Uso di Azure Active Directory <!--3607315, fka 1322145--> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
| Miglioramenti ad Asset Intelligence <!--3601024, fka 1307390--> | [Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence) |

## <a name="see-also"></a>Vedere anche

Per altre informazioni, vedere gli articoli seguenti:

- [Valutare Configuration Manager in un lab](evaluate-with-lab-environment.md)
- [Novità delle versioni incrementali di System Center Configuration Manager](../plan-design/changes/whats-new-incremental-versions.md)
- [Introduzione a Configuration Manager](../understand/introduction.md)

> [!Tip]
> Per altre informazioni sulle funzionalità Current Branch che richiedono il consenso per l'abilitazione, vedere [Funzionalità di versioni non definitive](../servers/manage/pre-release-features.md).
>
> Per altre informazioni sulle funzionalità Current Branch che è necessario abilitare in prima istanza, vedere [Abilitare le funzionalità facoltative degli aggiornamenti](../servers/manage/install-in-console-updates.md#bkmk_options).
