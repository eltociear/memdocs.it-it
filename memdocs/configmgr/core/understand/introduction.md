---
title: Che cos'è Configuration Manager?
titleSuffix: Configuration Manager
description: Concetti di base relativi a Microsoft Endpoint Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3343eccf-bf09-41cd-9e68-03e893c7f904
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 78b9175c10d4389623bfa08ac7895df200944a13
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706909"
---
# <a name="what-is-configuration-manager"></a>Che cos'è Configuration Manager?

*Si applica a: Configuration Manager (Current Branch)*

A partire dalla versione 1910, Configuration Manager è incluso in Microsoft Endpoint Manager.

![Microsoft Endpoint Configuration Manager](media/4960084-endpoint-manager-logo.png)

Microsoft Endpoint Manager è una soluzione integrata per la gestione di tutti i dispositivi. Microsoft riunisce Configuration Manager e Intune, senza una migrazione complessa e con licenze semplificate. L'investimento esistente in Configuration Manager continua a essere valido e consente al contempo di sfruttare i vantaggi offerti dalla potenza del cloud Microsoft.

Le soluzioni di gestione Microsoft seguenti fanno ora parte del marchio **Microsoft Endpoint Manager**:

- [Configuration Manager](https://docs.microsoft.com/configmgr)
- [Intune](https://docs.microsoft.com/intune)
- [Desktop Analytics](../../desktop-analytics/overview.md)
- [Autopilot](https://docs.microsoft.com/intune/enrollment/enrollment-autopilot)
- Altre funzionalità della [console di amministrazione della gestione dei dispositivi](https://go.microsoft.com/fwlink/?linkid=2109094)

Per altre informazioni, vedere [Domande frequenti per Microsoft Endpoint Configuration Manager](microsoft-endpoint-manager-faq.md).

## <a name="introduction"></a>Introduzione

Usare Configuration Manager per semplificare le attività di gestione dei sistemi seguenti:

- Aumentare l'efficienza e la produttività IT riducendo le attività manuali e consentendo di concentrarsi sui progetti di alto valore.  
- Ottimizzare gli investimenti hardware e software.  
- Incrementare la produttività degli utenti fornendo il software più adatto al momento giusto.  

Configuration Manager consente di offrire servizi IT più efficienti abilitando le funzionalità seguenti:

- Distribuzione sicura e scalabile di applicazioni, aggiornamenti software e sistemi operativi.
- Azioni in tempo reale sui dispositivi gestiti.
- Analisi e gestione basate sul cloud per dispositivi locali e basati su Internet.
- Gestione delle impostazioni di conformità.  
- Gestione completa di server, desktop e computer portatili.

Configuration Manager si integra con le soluzioni e le tecnologie Microsoft esistenti e ne estende le funzionalità. Ad esempio, Configuration Manager si integra con:  

- Microsoft Intune per gestire un'ampia gamma di piattaforme per dispositivi mobili
- Microsoft Azure per ospitare i servizi cloud ed estendere i servizi di gestione
- Windows Server Update Services (WSUS) per gestire gli aggiornamenti software
- Servizi certificati
- Exchange Server e Exchange Online
- Criteri di gruppo
- DNS
- Windows Automated Deployment Kit (Windows ADK) e Utilità di migrazione stato utente (USMT).
- Servizi di distribuzione Windows (WDS)
- Desktop remoto e Assistenza remota

Configuration Manager usa anche:  

- Active Directory Domain Services e Azure Active Directory per la sicurezza, il percorso dei servizi, la configurazione e l'individuazione degli utenti e dei dispositivi da gestire.  
- Microsoft SQL Server come database di gestione delle modifiche distribuito e si integra con SQL Server Reporting Services (SSRS) per generare report per monitorare e tenere traccia delle attività di gestione.  
- I ruoli del sistema del sito che estendono le funzionalità di gestione e usano i servizi Web di Internet Information Services (IIS).
- Ottimizzazione recapito, Windows Low Extra Delay Background Transport (LEDBAT), Background Intelligent Transfer Service (BITS), BranchCache e altre tecnologie di peer caching per semplificare la gestione del contenuto nelle reti e tra dispositivi.

Per il corretto funzionamento di Configuration Manager in un ambiente di produzione, è innanzitutto necessario pianificare e testare attentamente le funzionalità di gestione. Configuration Manager è un'applicazione di gestione avanzata, che ha la capacità di influire su ogni computer dell'organizzazione. Se lo si distribuisce e lo si gestisce con un'attenta pianificazione e tenendo in considerazione i requisiti aziendali, Configuration Manager consente di ridurre il carico amministrativo e il costo totale di proprietà.  

## <a name="user-interfaces"></a>Interfacce utente

### <a name="the-configuration-manager-console"></a><a name="BKMK_Console"></a> Console di Configuration Manager

Dopo aver installato Configuration Manager usare la console di Configuration Manager per configurare siti e client e per eseguire e monitorare le attività di gestione. Questa console è il punto di amministrazione principale e consente di gestire più siti.  

È possibile installare la console di Configuration Manager in altri computer e limitare l'accesso e la visualizzazione degli elementi della console da parte degli utenti amministratori usando l'amministrazione basata su ruoli di Configuration Manager.  

Per altre informazioni, vedere [Usare la console di Configuration Manager](../servers/manage/admin-console.md).

### <a name="software-center"></a><a name="BKMK_ApplicationCatalog"></a> Software Center

**Software Center** è un'applicazione che viene installata automaticamente al momento dell'installazione del client di Configuration Manager in un dispositivo Windows. Gli utenti usano Software Center per richiedere e installare il software distribuito. Con Software Center, gli utenti possono eseguire le operazioni seguenti:  

- Cercare e installare applicazioni, aggiornamenti software e nuove versioni del sistema operativo
- Visualizzare la cronologia delle richieste di software
- Visualizzare la conformità dei dispositivi in base ai criteri dell'organizzazione

È anche possibile mostrare schede personalizzate in Software Center per soddisfare altri requisiti aziendali.

Per altre informazioni, vedere il [Manuale dell'utente di Software Center](software-center.md).

## <a name="next-steps"></a>Passaggi successivi

Prima di installare Configuration Manager, acquisire familiarità con i concetti e i termini di base:

- Se si ha familiarità con System Center 2012 Configuration Manager, iniziare con [Novità rispetto a System Center 2012 Configuration Manager](../plan-design/changes/what-has-changed-from-configuration-manager-2012.md).

- Per una panoramica tecnica di alto livello di Configuration Manager, vedere [Nozioni fondamentali di System Center Configuration Manager](fundamentals.md).

Dopo aver acquisito familiarità con i concetti di base, usare la documentazione di Configuration Manager per distribuire e usare con facilità questo strumento. Iniziare con gli articoli seguenti:

- [Caratteristiche e funzionalità di Configuration Manager](../plan-design/changes/features-and-capabilities.md)  
- [Scegliere una soluzione di gestione dei dispositivi](../plan-design/choose-a-device-management-solution.md)  
- [Valutare Configuration Manager creando un proprio ambiente lab](../get-started/set-up-your-lab.md)
- [Reperire informazioni sull'uso di Configuration Manager](find-help.md)  
