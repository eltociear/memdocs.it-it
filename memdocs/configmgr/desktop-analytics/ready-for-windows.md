---
title: Ready for Windows
titleSuffix: Configuration Manager
description: Informazioni sul ritiro del sito Web Ready for Windows
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 3f09226c-4ca7-4e43-9ae8-5ee6e78e6bc2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ROBOTS: NOINDEX
ms.openlocfilehash: 484b1d808484984b4beaf434c0c27f2f1bec4e10
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88995195"
---
# <a name="ready-for-modern-desktop-retirement-faq"></a>Domande frequenti sul ritiro di Ready for modern desktop

<!-- placeholder -->

## <a name="ready-for-windows-adoption-status"></a>Stato di adozione Ready for Windows

Lo Stato di adozione si basa sulle informazioni provenienti da dispositivi commerciali che condividono dati con Microsoft. Lo stato è integrato con le istruzioni di supporto dei fornitori di software.

Desktop Analytics specifica lo stato di adozione per ogni versione di una risorsa presente nei dispositivi commerciali. Questo stato non include i dati di dispositivi consumer o dispositivi che non condividono dati. Lo stato potrebbe non essere rappresentativo della velocità di adozione in tutti i dispositivi Windows 10.

Le categorie possibili sono:

- **Ampiamente adottato**: almeno 100.000 dispositivi commerciali Windows 10 hanno installato l'app.

- **Adottato**: almeno 10.000 dispositivi commerciali Windows 10 hanno installato l'app.

- **Dati insufficienti**: il numero di dispositivi commerciali Windows 10 che stanno condividendo informazioni sull'app è troppo ridotto perché Microsoft possa classificarne l'adozione.

- **Contattare lo sviluppatore**: è possibile che si verifichino problemi di compatibilità con questa versione dell'app. Microsoft consiglia di contattare il provider del software per ottenere altre informazioni.

- **Sconosciuto**: non sono disponibili informazioni per questa versione dell'applicazione. Potrebbero essere disponibili informazioni per altre versioni dell'applicazione.

## <a name="general"></a>Generale

### <a name="what-happened-to-the-ready-for-windows-website"></a>Che cosa è successo al sito Web Ready for Windows?

Molti clienti hanno problemi a ottenere Windows 10 e Microsoft 365 Apps for enterprise e a mantenerli aggiornati. Il problema principale è quello di testare le applicazioni, in quanto si tratta in genere di un processo manuale. Per gli amministratori IT e i proprietari delle applicazioni analizzare continuamente le applicazioni esistenti e quindi correggere eventuali problemi è molto dispendioso in termini di tempo.

La directory *Ready for modern desktop* includeva un elenco delle soluzioni software supportate e usate nei dispositivi commerciali che eseguono Windows 10 e Microsoft 365 Apps for enterprise. La directory offre un valido aiuto ai responsabili IT che stanno prendendo in considerazione l'idea di adottare le versioni più recenti di Windows 10 e Microsoft 365 per le distribuzioni.

Il feedback dei responsabili IT è che vorrebbero che questi dati analitici si integrassero con gli strumenti che già usano per pianificare le distribuzioni. Per pianificare e gestire i progetti di aggiornamento di Windows 10 e Microsoft 365 Apps for enterprise, usare [Desktop Analytics](https://aka.ms/dadocs) e le [funzionalità di conformità di App di Microsoft 365](https://docs.microsoft.com/deployoffice/readiness-tools#office-365-proplus-readiness-features-in-configuration-manager-current-branch) in Configuration Manager. 

> [!Note]
> A partire dal 21 aprile 2020 Office 365 ProPlus viene rinominato come **App di Microsoft 365 per grandi imprese**. Per altre informazioni, vedere [Modifica del nome di Office 365 ProPlus](/deployoffice/name-change). È comunque possibile che vengano ancora visualizzati riferimenti al nome precedente nella console di Configuration Manager e nella documentazione di supporto mentre la console viene aggiornata.

### <a name="what-is-desktop-analytics"></a>Che cos'è Desktop Analytics?

[Desktop Analytics](https://aka.ms/dadocs) è un servizio basato su cloud che si integra con Configuration Manager. Il servizio offre dati analitici e intelligence per consentire agli utenti di prendere decisioni più informate sull'adozione degli aggiornamenti degli endpoint di Windows. Combina i dati specifici dell'organizzazione con dati analitici aggregati provenienti dai milioni di dispositivi Windows connessi ai servizi cloud Microsoft.

-    Consente di ottenere una vista completa degli endpoint, delle applicazioni e dei driver gestiti nella propria organizzazione.

-    Consente la valutazione della compatibilità di applicazioni e driver con gli aggiornamenti delle funzionalità Windows più recenti. Consente di ricevere consigli di mitigazione per i problemi noti, nonché dati analitici avanzati per le app line-of-business.

-    Usa l'intelligenza artificiale (IA) di Microsoft Cloud per ottimizzare il set di dispositivi pilota che rappresentano in modo adeguato l'ambiente globale dell'organizzazione.

### <a name="why-should-i-use-desktop-analytics-for-my-windows-deployment-plans"></a>Perché usare Desktop Analytics per i piani di distribuzione di Windows?

Desktop Analytics offre i vantaggi seguenti:

-    **Inventario di dispositivi e software**: Inventario dei fattori chiave, ad esempio le app e le versioni di Windows.

-    **Identificazione del progetto pilota**: Identificazione dell'insieme minimo di dispositivi che consentono la più ampia copertura di fattori. Vengono identificati i fattori ritenuti più importanti per un progetto pilota di aggiornamenti Windows. Assicurarsi che il progetto pilota sia ottimale consente di procedere in modo più rapido e sicuro a distribuzioni di grandi dimensioni in ambiente di produzione.

-    **Identificazione dei problemi**: Usando congiuntamente i dati di mercato aggregati e i dati dell'ambiente, il servizio esegue una previsione dei potenziali problemi per ottenere Windows e mantenerlo aggiornato. Suggerisce quindi eventuali mitigazioni.

-    **Integrazione di Configuration Manager**: Consente di abilitare l'infrastruttura locale esistente nel cloud. Usare questi dati e queste analisi per distribuire e gestire Windows nei dispositivi.

### <a name="what-does-the-ready-for-windows-status-mean-in-desktop-analytics"></a>Cosa significa lo stato *Ready for Windows* in Desktop Analytics?

Lo **Stato adozione**  si basa sulle informazioni provenienti da dispositivi commerciali che condividono dati con Microsoft. Lo stato è integrato con le istruzioni di supporto dei fornitori di software.

Desktop Analytics specifica lo stato di adozione per ogni versione di una risorsa presente nei dispositivi commerciali. Questo stato non include i dati di dispositivi consumer o dispositivi che non condividono dati. Lo stato potrebbe non essere rappresentativo della velocità di adozione in tutti i dispositivi Windows 10.

Per altre informazioni, vedere [Valutazione della compatibilità](compat-assessment.md).

### <a name="what-assets-get-the-ready-for-windows-status-in-desktop-analytics"></a>Quali risorse hanno lo stato *Ready for Windows* in Desktop Analytics? 

Le risorse hanno lo stato *Ready for Windows* in Desktop Analytics se:

-    Il provider del software dichiara il supporto della soluzione.
-    I clienti l'hanno distribuita su un numero significativo di dispositivi commerciali Windows 10 che condividono informazioni con Microsoft.
-    La risorsa è rilevante per gli utenti commerciali.

### <a name="what-additional-insights-do-i-get-in-desktop-analytics"></a>Quali sono i dati analitici supplementari disponibili in Desktop Analytics?

Desktop Analytics offre un inventario dei [dispositivi e delle app installate](about-assets.md), nonché [dati analitici avanzati](compat-assessment.md#advanced-insights) per le app line-of-business. 

## <a name="software-providers"></a>Provider di software

### <a name="can-i-still-list-my-software-solution-in-desktop-analytics"></a>È ancora possibile fare in modo che una soluzione software venga elencata in Desktop Analytics?

Pubblicare una dichiarazione di supporto per confermare che il prodotto funziona con Windows 10 a 32 o a 64 bit oppure con Microsoft 365 Apps for enterprise. Per presentare le soluzioni in Desktop Analytics, rivolgersi al proprio contatto Microsoft.

### <a name="how-can-listing-my-solutions-benefit-me"></a>Quali sono i vantaggi dell'avere soluzioni elencate in Desktop Analytics?

Migliaia di amministratori IT gestiscono milioni di dispositivi con Configuration Manager e Desktop Analytics. Usano questi strumenti per pianificare e aggiornare in modo sicuro le proprie organizzazioni alla versione più recente di Windows 10 e Microsoft 365 Apps for enterprise. Li usano anche per prendere decisioni di acquisto per le soluzioni software.

Microsoft integra le istruzioni di supporto dei fornitori di software con le informazioni di adozione ricevute dai dispositivi commerciali. Le organizzazioni in tutto il mondo usano questi dati negli strumenti di preparazione di Desktop Analytics e Office. 

Se le istruzioni di supporto non sono associate correttamente alle risorse, rivolgersi al proprio contatto Microsoft.

### <a name="can-i-see-detailed-performance-metrics-on-my-assets"></a>È possibile visualizzare le metriche delle prestazioni dettagliate per le risorse?

Valutare le prestazioni delle soluzioni con i report sull'integrità e sulle metriche tramite il centro per sviluppatori: 

- [Windows Store](/windows/uwp/publish/health-report)
- [Desktop](/windows/desktop/appxpkg/windows-desktop-application-program)
- [Componenti aggiuntivi per Office](/office/dev/store/update-unpublish-and-view-metrics) 

### <a name="how-can-i-develop-compatible-assets-for-windows-10-and-microsoft-365-apps-for-enterprise"></a>Come è possibile sviluppare asset compatibili per Windows 10 e Microsoft 365 Apps for enterprise?

Assicurarsi che le applicazioni desktop siano compatibili adesso e che rimangano compatibili con Windows 10 in futuro. Per informazioni, vedere [Compatibilità delle applicazioni per sviluppatori](https://developer.microsoft.com/windows/desktop/app-compatibility).

Se si sviluppano soluzioni per Microsoft 365 Apps for enterprise, vedere [Procedure consigliate per lo sviluppo di componenti aggiuntivi COM, VSTO e VBA in Office](https://docs.microsoft.com/visualstudio/vsto/development-best-practices-for-com-vsto-and-vba-add-ins-in-office).
