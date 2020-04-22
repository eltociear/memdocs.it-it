---
title: Supporto per Windows 10
titleSuffix: Configuration Manager
description: Informazioni sulle versioni di Windows 10 supportate come client o per la distribuzione del sistema operativo con Configuration Manager
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7241db0220bf4adf9b55341514afb03de33c2589
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688599"
---
# <a name="support-for-windows-10-in-configuration-manager"></a>Supporto per Windows 10 in Configuration Manager  

*Si applica a: Configuration Manager (Current Branch)*

Informazioni sulle versioni di Windows 10 supportate da Configuration Manager, incluse:

- [Windows 10 come client](#windows-10-as-a-client)
- [Windows 10 ADK](#windows-10-adk)

> [!Tip]
> Sono supportate le stesse build di Windows Server come client della versione di Windows 10 associata. Ad esempio, Windows Server 2016 è la stessa versione build di Windows 10 LTSB 2016, mentre Windows Server versione 1803 è la stessa versione build di Windows 10 versione 1803.
>
> Per altre informazioni su Windows Server come sistema del sito, vedere [Sistemi operativi supportati per i server dei sistemi del sito di Configuration Manager](supported-operating-systems-for-site-system-servers.md#bkmk_core).

## <a name="windows-10-as-a-client"></a>Windows 10 come client

Configuration Manager tenta di garantire il supporto come client per ogni nuova versione di Windows 10 appena possibile dopo il rilascio. Poiché i prodotti hanno pianificazioni di sviluppo e rilascio separate, il supporto offerto da Configuration Manager dipende dalla data di disponibilità di ogni prodotto.

Una versione di Configuration Manager viene eliminata dalla matrice dopo che termina il [supporto per tale versione](../../servers/manage/current-branch-versions-supported.md). Analogamente, il supporto per le versioni di Windows 10 come Enterprise 2015 LTSB o 1511 viene eliminato dalla matrice quando queste vengono rimosse dal supporto.

- L'ultima versione di Configuration Manager Current Branch riceve aggiornamenti di sicurezza e critici che possono includere la correzione dei problemi con le versioni di Windows 10. Quando Microsoft rilascia una nuova versione di Configuration Manager Current Branch, le versioni precedenti ricevono solo aggiornamenti di sicurezza. Per altre informazioni, vedere [Supporto per le versioni di System Center Configuration Manager Current Branch](../../servers/manage/current-branch-versions-supported.md).  

    > [!Note]  
    > Il metodo migliore per mantenere aggiornato Windows 10 consiste nel mantenere aggiornato Configuration Manager. Per altre informazioni, vedere [Configuration Manager e Windows as a Service](../../understand/configuration-manager-and-windows-as-service.md).  

- Le informazioni seguenti sono a complemento dell'articolo [Sistemi operativi supportati per client e dispositivi](supported-operating-systems-for-clients-and-devices.md).  

- Se si usa Long-Term Servicing Branch di Configuration Manager, vedere [Configurazioni supportate per Long-Term Servicing Branch](../../understand/supported-configurations-for-ltsb.md).  

La tabella seguente elenca le versioni di Windows 10 che è possibile usare come client con versioni diverse di Configuration Manager.

| Versione di Windows 10 | ConfigMgr 1810 | ConfigMgr 1902 | ConfigMgr 1906 | ConfigMgr 1910 | ConfigMgr 2002 |
|---------------------|-----|-----|-----|-----|-----|
| **Enterprise 2015 LTSB** <!--10/14/2025-->   | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) |
| **Enterprise 2016 LTSB** <!--10/13/2026-->   | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) |
| **Enterprise LTSC 2019** <!--01/09/2029-->   | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) |
| **1709**<br>(10.0.16299)   <!--04/14/2020-->   | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) |
| **1803**<br>(10.0.17134)   <!--11/10/2020-->   | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) |
| **1809**<br>(10.0.17763)   <!--05/11/2021-->   | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) |
| **1903**<br>(10.0.18362)   <!--12/08/2020-->   | ![Non supportato](media/Red_X.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) |
| **1909**<br>(10.0.18363)   <!--05/11/2021-->   | ![Non supportato](media/Red_X.png) | ![Non supportato](media/Red_X.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) |

<!-- lifecycle reference: https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet -->

Per altre informazioni sul ciclo di vita di Windows, vedere [Date importanti nel ciclo di vita di Windows](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)

| Chiave |
|--|
| ![Supportato](media/green_check.png) = **Supportato**  |
| ![Non supportato](media/Red_X.png) = **Non supportato** |

### <a name="windows-10-client-support-notes"></a><a name="bkmk_win10-notes"></a> Note sul supporto del client Windows 10

- Il supporto delle versioni di canale semestrale Windows 10 include le edizioni seguenti: Enterprise, Pro, Education e Pro Education.  

- A partire dalla versione 1906 Configuration Manager supporta Windows 10 Pro for Workstations.

- Per Windows 10, versione 1909, il supporto di distribuzione del sistema operativo mostra la versione come 10.0.18362.418.

### <a name="windows-10-on-arm64"></a><a name="bkmk_arm64"></a> Windows 10 in ARM64

Configuration Manager supporta il client nei dispositivi ARM64 Windows 10. La distribuzione del sistema operativo non è supportata.<!-- 1353704 -->

A partire dalla versione 2002,<!--5954175--> La piattaforma **Tutti i dispositivi Windows 10 (ARM64)** è disponibile nell'elenco delle versioni dei sistemi operativi supportate per gli oggetti con regole di requisiti o elenchi di applicabilità.

> [!NOTE]
> Se in precedenza era stata selezionata la piattaforma **Windows 10** di primo livello, con questa azione sono state selezionate automaticamente entrambe le piattaforme **Tutti i dispositivi Windows 10 (64 bit)** e **Tutti i dispositivi Windows 10 (32 bit)** . Questa nuova piattaforma non viene selezionata automaticamente. Se si vuole aggiungere **Tutti i dispositivi Windows 10 (ARM64)** , selezionarla manualmente nell'elenco.

### <a name="support-for-windows-insider"></a><a name="bkmk_WIfB-support"></a> Supporto per Windows Insider

A partire da Configuration Manager versione 1906, è possibile [aggiornare e gestire le build di Windows Insider](../../../sum/get-started/configure-classifications-and-products.md#bkmk_WIfB). Questa funzionalità viene fornita per comodità ai clienti. In caso di problemi, è disponibile il supporto per questa funzionalità. Configuration Manager potrebbe non emettere un hotfix per questa funzionalità in caso di interruzione del funzionamento.  

Per inviare commenti e suggerimenti su Windows Insider, usare l'[hub di commenti e suggerimenti](https://docs.microsoft.com/windows-insider/at-work-pro/wip-4-biz-feedback).

## <a name="windows-10-adk"></a>Windows 10 ADK

Quando si distribuiscono sistemi operativi con Configuration Manager, Windows ADK è una dipendenza esterna obbligatoria. Per altre informazioni, vedere gli articoli seguenti:

- [Requisiti dell'infrastruttura per la distribuzione del sistema operativo](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md#windows-adk-for-windows-10)

- [Scaricare Windows ADK per Windows 10](https://docs.microsoft.com/windows-hardware/get-started/adk-install)

    > [!IMPORTANT]
    > A partire da Windows 10 versione 1809, Windows PE è un programma di installazione separato. Non ci sono altre differenze funzionali.
    >
    > Assicurarsi di scaricare sia **Windows ADK per Windows 10** che il **componente aggiuntivo Windows PE per l'ADK**.

La tabella seguente elenca le versioni di Windows ADK 10 che è possibile usare con versioni diverse di Configuration Manager.

| Versione di Windows 10 ADK  | ConfigMgr 1810 | ConfigMgr 1902 | ConfigMgr 1906 | ConfigMgr 1910 | ConfigMgr 2002 |
|--------------------|-----|-----|-----|-----|-----|
| **1709**<br>(10.1.16299) | ![Non supportato](media/Red_X.png)   | ![Non supportato](media/Red_X.png) | ![Non supportato](media/Red_X.png) | ![Non supportato](media/Red_X.png) | ![Non supportato](media/Red_X.png) |
| **1803**<br>(10.1.17134) | ![Compatibile con le versioni precedenti](media/blue_compat.png) | ![Compatibile con le versioni precedenti](media/blue_compat.png) | ![Non supportato](media/Red_X.png) | ![Non supportato](media/Red_X.png) | ![Non supportato](media/Red_X.png) |
| **1809**<br>(10.1.17763) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Compatibile con le versioni precedenti](media/blue_compat.png) | ![Compatibile con le versioni precedenti](media/blue_compat.png) | ![Non supportato](media/Red_X.png) |
| **1903**<br>(10.1.18362) | ![Non supportato](media/Red_X.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) |

|Chiave|
|--|
| ![Supportato](media/green_check.png) = **Supportato** <br/> Questa tabella mostra solo il supporto di Windows ADK in relazione alla versione di Configuration Manager. Microsoft consiglia l'uso della versione di Windows ADK corrispondente alla versione di Windows che si vuole distribuire. Quando si distribuisce la versione più recente di Windows 10, usare la versione più recente di Windows ADK. La versione più recente di Windows ADK può supportare la distribuzione di versioni del sistema operativo meno recenti, ad esempio Windows 8.1.<!-- SCCMDocs issue 1229 --> Per altre informazioni sul supporto del componente Windows ADK, vedere [Piattaforme supportate di Gestione e manutenzione immagini distribuzione](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms) e [Requisiti USMT](https://docs.microsoft.com/windows/deployment/usmt/usmt-requirements#bkmk-1). |
| ![Compatibile con le versioni precedenti](media/blue_compat.png)  = **Compatibile con le versioni precedenti** <br/> Questa combinazione non è stata testata ma dovrebbe funzionare. Verranno documentati eventuali problemi noti o avvertenze. |
| ![Non supportato](media/Red_X.png) = **Non supportato** |

### <a name="windows-10-adk-support-notes"></a><a name="bkmk_adk-notes"></a> Note sul supporto di Windows 10 ADK

- Configuration Manager supporta solo i componenti x86 e amd64 di Windows 10 ADK e attualmente non supporta i componenti ARM e ARM64.

- Le build di Windows Server hanno gli stessi requisiti Windows ADK della versione di Windows 10 associata. Ad esempio, Windows Server 2016 è la stessa versione build di Windows 10 LTSB 2016.
