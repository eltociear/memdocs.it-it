---
title: Pianificare la creazione di report
titleSuffix: Configuration Manager
description: È importante pianificare la creazione di report in Configuration Manager a partire dalla installazione fino alla sicurezza e alla larghezza di banda di rete.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ff920c84-d5c8-458c-b67f-bc7219b05690
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 2621a6a364734a1146700aa8eef8fded3a6e58ab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694369"
---
# <a name="plan-for-reporting-in-configuration-manager"></a>Pianificazione per la creazione di report in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

La creazione di report in Configuration Manager offre un set di strumenti e risorse che consentono di usare le funzionalità di reporting avanzate di SQL Server Reporting Services (SSRS) o Server di report di Power BI. Usare le sezioni seguenti per la pianificazione della creazione di report in Configuration Manager.

## <a name="where-to-install-the-reporting-services-point"></a>Dove installare il punto di Reporting Services

Quando si eseguono i report di Configuration Manager in un sito, questi hanno accesso alle informazioni incluse nel database del sito a cui si connettono. Utilizzare le seguenti sezioni per determinare il percorso di installazione del punto di Reporting Services e l'origine dati da utilizzare.

> [!NOTE]
> Per altre informazioni sulla pianificazione dei sistemi del sito in Configuration Manager, vedere [Aggiungere ruoli di sistema del sito](../deploy/configure/add-site-system-roles.md).

### <a name="supported-site-system-servers"></a>Server di sistema del sito supportati

È possibile installare il punto di Reporting Services in un sito di amministrazione centrale (CAS) e in siti primari. Funziona in più sistemi di sito in un sito e in altri siti presenti nella gerarchia. Configuration Manager non supporta il punto di Reporting Services nei siti secondari. Il primo punto di Reporting Services in un sito viene impostato come server di report predefinito. Anche se è possibile aggiungere più punti di Reporting Services in un sito, Configuration Manager usa attivamente il server di report predefinito in ogni sito. Installare il punto di Reporting Services nel server del sito o in un sistema del sito remoto. Per ottenere prestazioni ottimali, usare SQL Server Reporting Services in un server di sistema del sito remoto.

### <a name="data-replication-considerations"></a>Considerazioni sulla replica dei dati

Tenere presenti i seguenti fattori per determinare dove installare i punti di Reporting Services:

- Un punto di Reporting Services con il database CAS come origine dati per i report ha accesso a tutti i dati globali e del sito presenti nella gerarchia di Configuration Manager. Se sono necessari report che contengano dati del sito per più siti in una gerarchia, prendere in considerazione l'installazione del punto di Reporting Services in un sistema del sito nel sito di amministrazione centrale. Usare quindi il database del sito di amministrazione centrale come origine dati per i report.

- Un punto di Reporting Services con un database del sito primario figlio come origine dei dati per i report ha accesso ai dati globali e ai dati del sito solo per il sito primario locale e per qualsiasi sito secondario figlio. I dati del sito per altri siti primari nella gerarchia di Configuration Manager non vengono replicati nel sito primario. Reporting Services non può accedere ai dati del sito per altri siti primari. Se sono necessari report che contengano dati del sito per un sito primario specifico o per dati globali ma non si vuole che l'utente abbia accesso ai dati del sito da altri siti primari, installare un punto di Reporting Services in un sistema del sito nel sito primario. Usare quindi il database del sito primario come origine dati per i report.

Per altre informazioni sui dati globali e del sito, vedere [Tipi di dati](../../plan-design/hierarchy/database-replication.md#types-of-data).

### <a name="network-bandwidth-considerations"></a>Considerazioni sulla larghezza di banda di rete

I sistemi del sito all'interno dello stesso sito comunicano con tutti gli altri usando SMB (Server Message Block), HTTP o HTTPS a seconda della configurazione del sito. Configuration Manager non gestisce questa comunicazione. Può avvenire in qualsiasi momento senza il controllo della larghezza di banda di rete. Controllare la larghezza di banda di rete disponibile prima di installare il ruolo del punto di Reporting Services in un sistema del sito.

Per altre informazioni sulla pianificazione dei sistemi del sito, vedere [Aggiungere ruoli di sistema del sito](../deploy/configure/add-site-system-roles.md).

## <a name="plan-for-role-based-administration"></a>Pianificare l'amministrazione basata su ruoli

La sicurezza dei report è simile alla sicurezza di altri oggetti in Configuration Manager, in cui è possibile assegnare autorizzazioni e ruoli di sicurezza agli utenti amministratori. Gli utenti amministratori possono solo eseguire e modificare i report per cui dispongono dei privilegi di protezione appropriati. Per eseguire report nella console di Configuration Manager, gli utenti devono avere il diritto di **Lettura** per l'autorizzazione **Sito** e le autorizzazioni configurate per oggetti specifici.

A differenza di altri oggetti in Configuration Manager, i privilegi di sicurezza impostati per gli utenti amministratori nella console di Configuration Manager vengono configurati anche in Reporting Services. Quando si configurano i privilegi di sicurezza nella console di Configuration Manager, il punto di Reporting Services si connette a Reporting Services e imposta le autorizzazioni appropriate per i report.

Ad esempio, il ruolo di sicurezza **Amministratore aggiornamento software** dispone delle autorizzazioni **Esegui report** e **Modifica report**. Gli utenti con il ruolo **Amministratore aggiornamento software** possono solo eseguire e modificare i report per gli aggiornamenti software. La console di Configuration Manager non visualizza i report per gli altri oggetti di questo ruolo. L'eccezione a questo comportamento è che alcuni report non sono associati a oggetti specifici a protezione diretta di Configuration Manager. Per tali report, l'utente amministratore deve disporre del diritto di **Lettura** per l'autorizzazione **Sito** per eseguire i report e del diritto **Modifica** per l'autorizzazione **Sito** per modificare i report.  

> [!IMPORTANT]
> Perché gli utenti di un dominio diverso da quello dell'account del punto di Reporting Services possano eseguire correttamente i report, stabilire una relazione di trust bidirezionale tra i due domini.

I report sono completamente abilitati per l'amministrazione basata su ruoli. Configuration Manager filtra i dati per tutti i report inclusi in base alle autorizzazioni dell'utente che esegue il report. Gli utenti con ruoli specifici possono solo visualizzare le informazioni definite per i loro ruoli.

Per altre informazioni sui diritti di sicurezza per la creazione di report, vedere [Configurare la creazione di report](configuring-reporting.md).

Per altre informazioni sull'amministrazione basata su ruoli in Configuration Manager, vedere [Configurare l'amministrazione basata su ruoli](../deploy/configure/configure-role-based-administration.md).

## <a name="reporting-recommendations"></a>Consigli per la creazione di report

Tenere presenti i consigli e i suggerimenti seguenti per la creazione di report in Configuration Manager:

- Per ottenere prestazioni ottimali, installare il punto di Reporting Services in un sistema del sito remoto. Sebbene sia possibile installarlo nel server del sito, il punto di Reporting Services garantisce prestazioni ottimali quando lo si installa in un sistema del sito remoto. Quando questo ruolo esegue l'elaborazione in background, può competere con altri ruoli per l'utilizzo di risorse di sistema. Le variabili da considerare per quanto riguarda le prestazioni del sito e del ruolo sono numerose, ma in generale questa configurazione migliora la creazione di report e le prestazioni complessive del sito.

- Ottimizzare le query di SQL Server Reporting Services. In genere i ritardi nella creazione di report sono causati dal tempo necessario per eseguire le query e recuperare risultati. In Microsoft SQL Server, strumenti come Analizzatore query e Profiler consentono di ottimizzare le query.

- Pianificare l'elaborazione delle sottoscrizioni report per l'esecuzione in orari non lavorativi. Se possibile, pianificare l'elaborazione delle sottoscrizioni report per l'esecuzione in orari non lavorativi al fine di ridurre al minimo l'elaborazione della CPU nel server di database del sito di Configuration Manager. In questo modo è inoltre possibile incrementare la disponibilità per le richieste di report impreviste.

- Gli aggiornamenti del sito non incidono sui report predefiniti. Se si modifica un report standard, quando il sito viene aggiornato, il report viene rinominato con un prefisso di sottolineatura (`_`). Questo comportamento assicura che l'aggiornamento del sito non sovrascriva il report modificato dal report standard.

## <a name="security-and-privacy"></a>Sicurezza e privacy

Nei report di Configuration Manager vengono visualizzate le informazioni raccolte durante le operazioni standard di gestione di Configuration Manager. Ad esempio, è possibile visualizzare un report di informazioni che Configuration Manager ha raccolto dall'individuazione o dall'inventario. I report possono inoltre contenere informazioni sullo stato corrente per le operazioni di gestione client, come ad esempio la distribuzione software e la verifica della conformità.

Per altre informazioni sulla sicurezza e la privacy per le operazioni di Configuration Manager che possono generare dati visibili nei report, vedere [Sicurezza e privacy per Configuration Manager](../../plan-design/security/security-and-privacy.md).  

## <a name="next-steps"></a>Passaggi successivi

[Prerequisiti per la creazione di report](prerequisites-for-reporting.md)
