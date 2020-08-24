---
title: Aggiornamenti e manutenzione
titleSuffix: Configuration Manager
description: Informazioni sul metodo di manutenzione nella console denominato Aggiornamenti e manutenzione che semplifica l'individuazione e l'installazione degli aggiornamenti consigliati.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3a832943-580a-4a40-b454-961d0854ac2b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3d8d9097b95a5daf06dc0260173e616fa2f88eb4
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126138"
---
# <a name="updates-and-servicing-for-configuration-manager"></a>Aggiornamenti e manutenzione per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Configuration Manager usa un metodo di manutenzione nella console denominato **Aggiornamenti e manutenzione**. Questo metodo nella console semplifica l'individuazione e l'installazione degli aggiornamenti consigliati per l'infrastruttura di Configuration Manager. La manutenzione nella console integra gli aggiornamenti fuori programma, come gli hotfix. Gli aggiornamenti fuori programma sono destinati ai clienti che devono risolvere problemi che potrebbero essere specifici dell'ambiente in uso.  

> [!TIP]  
> I termini *upgrade*, *aggiornamento* e *installazione* vengono usati per descrivere tre concetti separati in Configuration Manager. Per altre informazioni su come viene usato ogni termine, vedere [Informazioni su upgrade, aggiornamento e installazione](../../understand/upgrade-update-install.md).  

## <a name="baseline-and-update-versions"></a><a name="bkmk_Baselines"></a> Versioni di base e di aggiornamento  

Usare la versione di base più recente quando si installa un nuovo sito in una nuova gerarchia.

- Si usa una versione di base anche per eseguire l'aggiornamento da System Center 2012 Configuration Manager.  

- Dopo l'aggiornamento a Configuration Manager Current Branch, non usare le versioni di base per rimanere aggiornati. Usare invece solo [aggiornamenti nella console](install-in-console-updates.md) per eseguire l'aggiornamento alla versione più recente.  

- Periodicamente vengono rilasciate altre versioni baseline. Quando si usa la versione baseline più recente per installare una nuova gerarchia, si evita di installare una versione non aggiornata o non supportata di Configuration Manager, seguita da un aggiornamento aggiuntivo dell'infrastruttura per aggiornarla.  

Dopo avere installato una versione di base, altre versioni di Configuration Manager sono disponibili come aggiornamenti nella console. Gli aggiornamenti nella console aggiornano l'infrastruttura alla versione più recente di Configuration Manager.  

- Installare gli aggiornamenti nella console per aggiornare la versione del sito principale.  

- Nei siti primari figlio vengono installati automaticamente gli stessi aggiornamenti installati nel sito di amministrazione centrale. Controllare questa tempistica usando un intervallo di servizio nel sito primario. Per altre informazioni, vedere [Intervalli di servizio](service-windows.md).  

- Aggiornare manualmente i siti secondari a una nuova versione di aggiornamento dalla console.  

Quando si installa un aggiornamento, questo archivia i file di installazione per la versione nel server del sito, in una cartella denominata **CD.Latest**. Per altre informazioni su questi file, vedere [The CD.Latest folder](the-cd.latest-folder.md) (Cartella CD.Latest).  

- Usare i file nella cartella CD.Latest per il ripristino del sito. Inoltre, quando nella gerarchia non è più in esecuzione una versione di base, usare questi file per installare altri siti.  

- Non è possibile usare i file di installazione della cartella CD.Latest per installare il primo sito di una nuova gerarchia oppure per aggiornare un sito da System Center 2012 Configuration Manager.  

### <a name="version-details"></a>Dettagli sulla versione

Alcuni aggiornamenti per Configuration Manager sono disponibili sia come versione di aggiornamento nella console per l'infrastruttura esistente sia come nuova versione di base.  

#### <a name="supported-versions"></a>Versioni supportate

Le versioni supportate seguenti di Configuration Manager sono attualmente disponibili come versione di base, come aggiornamento oppure in entrambe le forme:  

| Version | Data di disponibilità | [Data di fine supporto](current-branch-versions-supported.md) | Versione di base | Aggiornamento nella console |  
|-------------|-----------|------------|--------------|------------------------|  
| [**2006**](../../plan-design/changes/whats-new-in-version-2006.md)<br /> (5.00.9012) | 11 agosto 2020 | Febbraio 11, 2022 | No | Sì |
| [**2002**](../../plan-design/changes/whats-new-in-version-2002.md)<br /> (5.00.8968) | 1 aprile 2020 | 1 ottobre 2021 | Sì<sup>[Nota 1](#bkmk_note1)</sup> | Sì |
| [**1910**](../../plan-design/changes/whats-new-in-version-1910.md)<br /> (5.00.8913) | 29 novembre 2019 | 29 maggio 2021 | No | Sì |
| [**1906**](../../plan-design/changes/whats-new-in-version-1906.md)<br /> (5.00.8853) | 26 luglio 2019 | 26 gennaio 2021 | No | Sì |
| [**1902**](../../plan-design/changes/whats-new-in-version-1902.md)<br /> (5.00.8790) | 27 marzo 2019 | 27 settembre 2020 | Sì | Sì |
| [**1810**](../../plan-design/changes/whats-new-in-version-1810.md)<br /> (5.00.8740) | 27 novembre 2018 | 1 dicembre 2020 | No | Sì |

**Data disponibilità** si riferisce a quando viene rilasciato l'[anello di aggiornamento anticipato](checklist-for-installing-update-2006.md#early-update-ring). I supporti di base saranno disponibili in Volume License Service Center dopo che l'aggiornamento sarà disponibile a livello globale.

<a name="bkmk_note1"></a>

> [!Note]  
> <sup>**Nota 1:** </sup> Il supporto di base è disponibile come parte delle versioni seguenti in [Volume License Service Center](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx) (VLSC):
>
> - Microsoft Endpoint Configmgr (Current Branch)
> - System Center Datacenter
> - System Center Standard  
>
> Ad esempio, cercare `Microsoft Endpoint Configmgr (current branch)` in VLSC. Individuare il supporto di base nell'elenco dei file e scaricarlo per la versione specifica.  

#### <a name="historical-versions"></a>Versioni cronologiche

La tabella seguente elenca le versioni cronologiche di Configuration Manager Current Branch che non sono più supportate:

| Version | Data di disponibilità | Data di fine supporto | Versione di base | Aggiornamento nella console |  
|-------------|-----------|------------|--------------|------------------------|  
| **1806** <br /> (5.00.8692) | 31 luglio 2018 | 31 gennaio 2020 | No | Sì |
| **1802** <br /> (5.00.8634) | 22 marzo 2018 | 22 settembre 2019 | Sì | Sì |
| **1710** <br /> (5.00.8577) | 20 novembre 2017 | 20 maggio 2019 | No | Sì |
| **1706** <br /> (5.00.8540) | 31 luglio 2017 | 31 luglio 2018 | No | Sì |
| **1702** <br /> (5.00.8498) | 27 marzo 2017 | 27 marzo 2018 | Sì | Sì |
| **1610** <br /> (5.00.8458) | 18 novembre 2016 | 18 novembre 2017 | No | Sì |
| **1606** <br /> (5.00.8412.1000) | 22 luglio 2016 | 22 luglio 2017 | No | Sì |
| **1606 con KB3186654** <br />5.00.8412.1307) | 12 ottobre 2016 | 12 ottobre 2017 | Sì | No |
| **1602** <br /> (5.00.8355) | 11 marzo 2016 | 11 marzo 2017 | No | Sì |
| **1511** <br /> (5.00.8325) | 8 dicembre 2015 | 8 dicembre 2016 | Sì | No |  

#### <a name="how-to-check-the-version"></a>Come controllare la versione

Per controllare la versione del sito di Configuration Manager, nella console passare a **Informazioni su Configuration Manager** nell'angolo in alto a sinistra. Questa finestra di dialogo consente di visualizzare le versioni del sito e della console.  

> [!Note]  
> La versione della console è leggermente diversa da quella del sito. La versione secondaria della console corrisponde alla versione finale di Configuration Manager. Ad esempio, in Configuration Manager versione 1802 la versione iniziale del sito è 5.0.8634.1000 e la versione iniziale della console è 5.**1802**.1082.1700. Con i futuri hotfix è possibile che i numeri di build (1082) e revisione (1700) cambino.

## <a name="in-console-updates-and-servicing"></a><a name="bkmk_inconsole"></a> Aggiornamenti e manutenzione nella console  

Quando si usa un'installazione di Configuration Manager Current Branch pronta per l'ambiente di produzione, la maggior parte degli aggiornamenti è disponibile mediante il canale **Aggiornamenti e manutenzione**. Questo metodo identifica, scarica e rende disponibili gli aggiornamenti applicabili alla versione e alla configurazione correnti dell'infrastruttura. Include solo gli aggiornamenti consigliati da Microsoft a tutti i clienti.

Questi aggiornamenti includono:  

- Nuove versioni, ad esempio 1910, 2002 o 2006.

- Aggiornamenti che includono nuove funzionalità per la versione corrente.

- Hotfix per la versione in uso di Configuration Manager e di cui è consigliata l'installazione a tutti i clienti.

    > [!Note]  
    > A partire dalla versione 1902, gli hotfix nella console hanno ora relazioni di sostituzione. Per altre informazioni, vedere [Sostituzione per gli hotfix nella console](#bkmk_supersede).

Gli aggiornamenti nella console offrono maggiore stabilità e risolvono i problemi comuni. Sostituiscono i tipi di aggiornamento disponibili per le versioni precedenti del prodotto, come Service Pack, aggiornamenti cumulativi e hotfix applicabili a tutti i clienti, nonché l'estensione per Microsoft Intune.

Questi aggiornamenti nella console possono riguardare uno o più dei sistemi seguenti:  

- Server del sito di amministrazione centrale e dei siti primari  

- Ruoli del sistema del sito e server di sistema del sito  

- Istanze del provider SMS  

- Console di Configuration Manager  

- Client di Configuration Manager  

Configuration Manager individua automaticamente i nuovi aggiornamenti. Sincronizzare il punto di connessione del servizio Configuration Manager con il servizio Microsoft Cloud, tenendo presenti i comportamenti seguenti:  

- Quando il punto di connessione del servizio è in modalità online, il sito si sincronizza con Microsoft ogni giorno. Individua automaticamente i nuovi aggiornamenti applicabili alla propria infrastruttura. Per scaricare gli aggiornamenti e i file ridistribuibili, il computer che ospita il ruolo del sistema del sito punto di connessione del servizio usa il contesto di **sistema** per accedere ai percorsi Internet seguenti: go.microsoft.com e download.microsoft.com. Per altre informazioni su ulteriori percorsi usati dal punto di connessione del servizio, vedere i [requisiti di accesso Internet](../deploy/configure/about-the-service-connection-point.md#bkmk_urls).  

- Quando il punto di connessione del servizio è in modalità offline, è necessario usare lo strumento di connessione del servizio per eseguire manualmente la sincronizzazione con Microsoft Cloud. Per altre informazioni, vedere [Usare lo strumento di connessione del servizio](use-the-service-connection-tool.md).  

- Grazie agli aggiornamenti nella console non è necessario individuare e installare i singoli aggiornamenti, Service Pack e nuove funzionalità in modo indipendente.  

- Installare solo gli aggiornamenti nella console scelti. Durante l'installazione di alcuni aggiornamenti, è possibile selezionare singole funzionalità da abilitare e utilizzare. Per altre informazioni, vedere [Enable optional features from updates](install-in-console-updates.md#bkmk_options) (Abilitare le funzioni facoltative dagli aggiornamenti).  

Quando si installa un aggiornamento nella console, si verifica quanto segue:  

- Viene eseguito automaticamente un controllo dei prerequisiti. È anche possibile eseguire questo controllo manualmente prima dell'avvio dell'installazione.  

- Viene installato nel sito di livello superiore dell'ambiente in uso. Questo sito corrisponde al sito di amministrazione centrale, ove presente. In una gerarchia, l'aggiornamento viene installato automaticamente nei siti primari. Controllare quando ogni server del sito primario può essere aggiornato usando gli [intervalli di servizio per i server del sito](service-windows.md).  

- Dopo l'aggiornamento di un server del sito, tutti i ruoli di sistema del sito interessati vengono aggiornati automaticamente. Questi ruoli includono le istanze del provider SMS. Dopo l'installazione dell'aggiornamento nel sito, le console di Configuration Manager chiedono all'utente di aggiornare anche la console stessa.  

- Se un aggiornamento include il client di Configuration Manager, è possibile scegliere se testare l'aggiornamento in pre-produzione oppure applicare immediatamente l'aggiornamento a tutti i client.  

- Dopo l'aggiornamento di un sito primario, i siti secondari non vengono aggiornati automaticamente. È invece necessario avviare manualmente l'aggiornamento del sito secondario.  

> [!NOTE]  
> Configuration Manager Current Branch, Long-Term Servicing Branch e Technical Preview Branch sono rilasci diversi. Gli aggiornamenti relativi a un ramo non sono disponibili come aggiornamenti nella console per gli altri rami. Per altre informazioni sui rami disponibili, vedere [Scelta del ramo di Configuration Manager da usare](../../understand/which-branch-should-i-use.md).

### <a name="supersedence-for-in-console-hotfixes"></a><a name="bkmk_supersede"></a> Sostituzione per gli hotfix nella console

<!-- 3229613 -->
A partire dalla versione 1902, gli hotfix nella console hanno ora relazioni di sostituzione. Quando Microsoft pubblica un nuovo hotfix per Configuration Manager, la console non visualizza gli hotfix sostituiti dal nuovo hotfix. Questo nuovo comportamento consente di individuare meglio gli hotfix da installare.

### <a name="supersedence-example"></a>Esempio di sostituzione

Sono disponibili tre hotfix: Hotfix-A, Hotfix-B e Hotfix-C. Hotfix-A è sostituito da Hotfix-B, mentre Hotfix-B è sostituito da Hotfix-C.

|Hotfix-A|Hotfix-B|Hotfix-C|Visualizzazione nella console|
|--------|--------|--------|---------------|
|Non installato|Non installato|Non installato|Visualizza tutti e tre gli hotfix|
|Installato|Installato|Non installato|Hotfix-B è visualizzato come installato<br/>Hotfix-C è visualizzato come pronto per l'installazione|
|Non installato|Non installato|Installato|Hotfix-C è visualizzato come installato|

## <a name="out-of-band-hotfixes"></a><a name="bkmk_outofband"></a> Hotfix fuori programma  

Alcuni rilasci di hotfix con disponibilità limitata per risolvere problemi specifici. Altri hotfix sono applicabili a tutti i clienti, ma non possono essere installati usando il metodo nella console. Questi aggiornamenti sono rilasciati fuori programma e non vengono individuati dal servizio cloud Microsoft.  

Se si sta cercando di risolvere o correggere un problema relativo alla distribuzione di Configuration Manager, in genere è possibile trovare informazioni sugli hotfix fuori programma tramite i servizi di assistenza clienti Microsoft, in un articolo della Knowledge Base o nel [blog del team di Configuration Manager](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/bg-p/ConfigurationManagerBlog).

Installare questi aggiornamenti manualmente, usando uno dei due metodi seguenti:  

### <a name="update-registration-tool"></a>Strumento di registrazione dell'aggiornamento

Questo strumento importa manualmente l'hotfix nella console di Configuration Manager. Quindi installa l'aggiornamento come si installerebbero gli aggiornamenti nella console che vengono individuati automaticamente.  

Questo metodo è usato per gli hotfix con la struttura di nome file seguente:  
    `<Product>-<product version>-<KB article ID>-ConfigMgr.Update.exe`

Per altre informazioni, vedere [Use the Update Registration Tool to import hotfixes](use-the-update-registration-tool-to-import-hotfixes.md) (Usare lo strumento di registrazione dell'aggiornamento per importare gli hotfix).  

### <a name="hotfix-installer"></a>Programma di installazione di hotfix

Usare questo strumento per installare manualmente un hotfix che non è possibile installare usando il metodo nella console.  

Questo metodo è usato per gli aggiornamenti con la struttura di nome file seguente:  
    `<Product>-<product version>-<KB article ID>-<platform>-<language>.exe`  

Per altre informazioni, vedere [Use the Hotfix Installer to install updates](use-the-hotfix-installer-to-install-updates.md) (Usare il programma di installazione degli hotfix per installare gli aggiornamenti).  

## <a name="next-steps"></a>Passaggi successivi

Gli argomenti seguenti possono essere utili per capire come individuare e installare i diversi tipi di aggiornamenti per Configuration Manager:  

- [Installare gli aggiornamenti nella console](install-in-console-updates.md)  

- [Usare lo strumento di connessione del servizio](use-the-service-connection-tool.md)  

- [Usare lo strumento di registrazione dell'aggiornamento per importare gli hotfix](use-the-update-registration-tool-to-import-hotfixes.md)  

- [Usare il programma di installazione degli hotfix per installare gli aggiornamenti](use-the-hotfix-installer-to-install-updates.md)  

Per altre informazioni sul Technical Preview Branch, vedere [Technical Preview](../../get-started/technical-preview.md).
