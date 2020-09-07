---
title: Funzionalità deprecate
titleSuffix: Configuration Manager
description: Informazioni sulle funzionalità che Configuration Manager non supporta più.
ms.date: 08/28/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 287a6324-ae65-4d38-b2ef-198d47c91231
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: aca9dc5c2ff2d88155ab19656f391cf87a4e977f
ms.sourcegitcommit: 42882de75c8a984ba35951b1165c424a7e0ba42e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2020
ms.locfileid: "89068090"
---
# <a name="removed-and-deprecated-features-for-configuration-manager"></a>Funzionalità rimosse e deprecate per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

In questo articolo sono elencate le funzionalità deprecate o rimosse dal supporto per Configuration Manager. Le funzionalità deprecate verranno rimosse in un aggiornamento futuro. Queste future modifiche potrebbero influire sull'uso di Configuration Manager.  

Queste informazioni sono soggette a modifica nelle versioni future. È possibile che non tutte le funzionalità di Configuration Manager deprecate siano incluse.

## <a name="deprecated-features"></a>Funzionalità deprecate

Le funzionalità seguenti sono deprecate. È ancora possibile usarle al momento, ma Microsoft prevede di terminare il supporto in futuro.

|Funzionalità|Primo annuncio riguardo agli elementi deprecati|Supporto&nbsp;rimosso|
|-----------|---|--------------|
|Vista geografica nel nodo **Gerarchia siti** dell'area di lavoro **Monitoraggio** nella console di Configuration Manager.<!--8116777-->|Agosto 2020|TBD|
|È stata modificata l'implementazione per la condivisione del contenuto da Azure. Usare un gateway di gestione cloud abilitato per il contenuto. Non sarà possibile creare un punto di distribuzione cloud tradizionale in futuro.|Febbraio 2019|DA DEFINIRE<sup>[Nota 1](#bkmk_note1)</sup>|
|Distribuzione classica del servizio in Azure per il gateway di gestione cloud e il punto di distribuzione cloud. Per altre informazioni, vedere [Pianificare il gateway di gestione cloud](../../../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager).|Novembre 2018|DA DEFINIRE<sup>[Nota 1](#bkmk_note1)</sup>|

### <a name="note-1-support-removed-tbd"></a><a name="bkmk_note1"></a> Nota 1: Rimozione del supporto (da definire)

La tempistica specifica è ancora da definire. Microsoft consiglia di passare al nuovo processo o funzionalità, ma è possibile continuare a usare la funzionalità o il processo deprecato per il prossimo futuro.

## <a name="unsupported-and-removed-features"></a>Funzionalità non supportate e rimosse

Le funzionalità seguenti non sono più supportate. In alcuni casi, non sono più incluse nel prodotto.

|Funzionalità|Primo annuncio riguardo agli elementi deprecati|Supporto&nbsp;rimosso|  
|-----------|---|--------------|  
| Opzione di Desktop Analytics **Visualizza dati recenti** per la registrazione e gli aggiornamenti di sicurezza dei dispositivi.<!-- 7080949 --> Per altre informazioni, vedere [Latenza dei dati](../../../../desktop-analytics/troubleshooting.md#data-latency).|Maggio 2020|Luglio 2020|
| Integrazione di Windows Analytics e Preparazione aggiornamenti. Per altre informazioni, vedere [KB 4521815: Ritiro di Windows Analytics il 31 gennaio 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement). | 14 ottobre 2019 | 31 gennaio 2020 |
| Valutazione dell'attestazione dell'integrità dei dispositivi per i criteri di conformità dell'accesso condizionale <!--1235616 aka 3608202--> Per altre informazioni, vedere [Che ne è stato della gestione di dispositivi mobili ibrida?](../../../../mdm/understand/what-happened-to-hybrid.md).| 3 luglio 2019 | Versione 1910 |
| App Portale aziendale di Configuration Manager | 21 maggio 2019 | Versione 1910 |
| Catalogo applicazioni, che comprende i due ruoli del sistema del sito: il punto per siti Web del Catalogo applicazioni e il punto per servizi Web. Per altre informazioni, vedere [Rimuovere il catalogo applicazioni](../../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat). | 21 maggio 2019 | Versione 1910 |
|Autenticazione basata su certificato con le impostazioni di Windows Hello for Business in Configuration Manager<br>Per altre informazioni, vedere [Impostazioni di Windows Hello for Business](../../../../protect/deploy-use/windows-hello-for-business-settings.md).|Dicembre 2017|Versione 1910|
|System Center Endpoint Protection per Mac e Linux<br>Per altre informazioni, vedere il [post del blog sulla fine del supporto](https://techcommunity.microsoft.com/t5/configuration-manager-blog/end-of-support-for-scep-for-mac-and-scep-for-linux-on-december/ba-p/286257).|Ottobre 2018|31 dicembre 2018|
|Accesso condizionale in locale<br>Per altre informazioni, vedere [Che ne è stato della gestione di dispositivi mobili ibrida?](../../../../mdm/understand/what-happened-to-hybrid.md).|30 gennaio 2019|1 settembre 2019|
|Gestione di dispositivi mobili (MDM) ibrida<br>Per altre informazioni, vedere [Che ne è stato della gestione di dispositivi mobili ibrida?](../../../../mdm/understand/what-happened-to-hybrid.md).<br><br>A partire dalla versione 1902 del servizio Intune, prevista per la fine di febbraio 2019, i nuovi clienti non possono creare una nuova connessione ibrida.<!--Intune feature 2683117-->|14 agosto 2018|1 settembre 2019|
|Estensioni SCAP (Security Content Automation Protocol). <!--3607889--><br>La versione certificata precedente è ancora disponibile nell'[Area download Microsoft](https://www.microsoft.com/download/details.aspx?id=48741).|Settembre 2018|Versione 1810|
|L'**esperienza utente di Silverlight** per il ruolo Punto per siti Web del Catalogo applicazioni non è più supportato. Gli utenti devono usare il nuovo Software Center. Per altre informazioni, vedere [Configurare Software Center](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex).<!--1358309-->|11 agosto 2017| Versione 1806|
|Versione precedente di Software Center.<br><br>Per altre informazioni sulla nuova versione di Software Center, vedere [Pianificare e configurare la gestione delle applicazioni](../../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_userex).|13 dicembre 2016|Versione 1802|
|Gestione dei dischi rigidi virtuali in Configuration Manager. <br><br>Questa funzionalità deprecata include la rimozione delle opzioni per creare un nuovo disco rigido virtuale o per gestire un disco rigido virtuale con una sequenza di attività e la rimozione del nodo Dischi rigidi virtuali dalla console di Configuration Manager. <br><br>I dischi rigidi virtuali esistenti non vengono eliminati, ma non saranno più accessibili dalla console di Configuration Manager.  |6 gennaio 2017 |Versione 1710|
|Sequenze attività: <br /> - Converti il disco selezionato in disco dinamico <br /> - Installa strumenti di distribuzione |18 novembre 2016|Versione 1710|
|Strumento di valutazione aggiornamento<br><br>Lo strumento di valutazione dell'aggiornamento dipende da Configuration Manager e da Application Compatibility Toolkit (ACT) 6.x. La versione finale di ACT è stata fornita in Windows 10 v1511 ADK. Dal momento che non sono disponibili altri aggiornamenti di ACT, il supporto per lo strumento di valutazione dell'aggiornamento viene sospeso. L'avviso relativo alla deprecazione è stato aggiunto alla [pagina di download per UAT](https://www.microsoft.com/software-download/windows10) il 12 settembre 2016. | 12 settembre 2016  | 11 luglio 2017 |
|Punti di aggiornamento software con un cluster Bilanciamento carico di rete (NLB) | 27 febbraio 2016 | Versione 1702 |
|Sequenze attività: <br /> - OSDPreserveDriveLetter  <br /><br /> Durante la distribuzione del sistema operativo, per impostazione predefinita l'installazione di Windows ora stabilisce qual è la lettera di unità migliore da usare (in genere C:). Se si vuole specificare un'unità diversa da usare, è possibile modificare il percorso nella sequenza di passaggi dell'attività Applica sistema operativo. Passare all'impostazione **Selezionare il percorso in cui applicare questo sistema operativo**. Selezionare **Lettera unità logica specifica** e scegliere l'unità che si vuole usare. |20 giugno 2016 |Versione 1606 |
|Protezione accesso alla rete (NAP) inclusa in System Center 2012 Configuration Manager|10 luglio 2015|Versione 1511|  
|Gestione fuori banda in System Center 2012 Configuration Manager|16 ottobre 2015|Versione 1511|

### <a name="features-removed-in-version-1511"></a>Funzionalità rimosse nella versione 1511

Le sezioni seguenti includono altri dettagli relativi alle funzionalità rimosse con la versione 1511:

#### <a name="out-of-band-management"></a><a name="bkmk_amt"></a> Gestione fuori banda  

Con Configuration Manager, il supporto nativo per computer basati su AMT dalla console di Configuration Manager è stato rimosso.  

- I computer basati su AMT restano completamente gestiti quando si usa il [componente aggiuntivo Intel SCS per Configuration Manager](https://www.intel.com/content/www/us/en/software/setup-configuration-software.html). Il componente aggiuntivo consente di accedere alle funzionalità più recenti per gestire AMT, rimuovendo le limitazioni introdotte fino al momento in cui Configuration Manager è stato in grado di integrare queste modifiche.  

- La gestione fuori banda in System Center 2012 Configuration Manager non è interessata da questa modifica.  

#### <a name="network-access-protection"></a><a name="bkmk_nap"></a> Protezione accesso alla rete

Configuration Manager ha rimosso il supporto per Protezione accesso alla rete. Questa funzionalità è stata deprecata in Windows Server 2012 R2 ed è stata rimossa da Windows 10.  

Per alternative a Protezione accesso alla rete, vedere la sezione *Funzionalità deprecata* di [Panoramica dei criteri di rete e dei servizi di accesso](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831683(v=ws.11)).

## <a name="see-also"></a>Vedere anche

- [Elementi rimossi e deprecati](removed-and-deprecated.md)
- [Ciclo di vita del supporto Microsoft](https://support.microsoft.com/lifecycle)
- [Supporto per le versioni Current Branch di System Center Configuration Manager](../../../servers/manage/current-branch-versions-supported.md)