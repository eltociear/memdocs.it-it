---
title: Pianificare la gestione di BitLocker
titleSuffix: Configuration Manager
description: Pianificare la gestione di Crittografia unità BitLocker con Configuration Manager
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a4d8cda2-bc9b-4fb4-aa0d-23c31b4fc60b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 460c9dd503861ba9f45e85f471bb1cb1274754a0
ms.sourcegitcommit: 99a6e83219978433ec5a91d09beeaf69acbeb522
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82782119"
---
# <a name="plan-for-bitlocker-management"></a>Pianificare la gestione di BitLocker

*Si applica a: Configuration Manager (Current Branch)*

<!-- 3601034 -->

A partire dalla versione 1910, usare Configuration Manager per gestire Crittografia unità BitLocker (BDE) per i client Windows locali. Configuration Manager offre una gestione completa del ciclo di vita di BitLocker che può sostituire l'uso di Microsoft BitLocker Administration and Monitoring (MBAM).

> [!Note]  
> Configuration Manager non abilita questa funzionalità facoltativa per impostazione predefinita. Pertanto sarà necessario abilitarla prima di poterla usare. Per altre informazioni, vedere [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options) (Abilitare le funzioni facoltative dagli aggiornamenti).  

Per altre informazioni, vedere [Panoramica di BitLocker](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-overview).

> [!TIP]
> Per gestire la crittografia in dispositivi Windows 10 con co-gestione usando il servizio cloud Microsoft Endpoint Manager, spostare il [carico di lavoro **Endpoint Protection**](../../comanage/workloads.md#endpoint-protection) in Intune. Per altre informazioni sull'uso di Intune, vedere [Crittografia di Windows](/intune/protect/endpoint-protection-windows-10#windows-encryption).

## <a name="features"></a>Caratteristiche

Configuration Manager offre le funzionalità di gestione seguenti per Crittografia unità BitLocker:

### <a name="client-deployment"></a>Distribuzione client

Distribuire il client di BitLocker nei dispositivi Windows gestiti che eseguono Windows 10 o Windows 8.1

### <a name="manage-encryption-policies"></a>Gestire i criteri di crittografia

- Ad esempio: scegliere la crittografia delle unità e il livello di codifica, configurare i criteri di esenzione utente e le impostazioni di crittografia per unità dati fisse.

- Determinare gli algoritmi con cui crittografare il dispositivo e i dischi di destinazione per la crittografia.

- Forzare la conformità degli utenti con i nuovi criteri di sicurezza prima di usare il dispositivo.

- Personalizzare il profilo di sicurezza dell'organizzazione in base ai singoli dispositivi.

- Quando un utente sblocca l'unità del sistema operativo, specificare se sbloccare solo un'unità del sistema operativo o tutte le unità collegate.

### <a name="compliance-reports"></a>Report di conformità

Report predefiniti per:

- Stato di crittografia per volume o per dispositivo
- Utente primario del dispositivo
- Stato di conformità
- Motivi per la mancata conformità

### <a name="administration-and-monitoring-website"></a>Sito Web di amministrazione e monitoraggio

Consentire ad altri utenti dell'organizzazione all'esterno della console di Configuration Manager di fornire assistenza per il ripristino delle chiavi, inclusa la rotazione delle chiavi e altre attività di supporto correlate a BitLocker. Ad esempio, gli amministratori dell'help desk possono aiutare gli utenti con il recupero della chiave.

### <a name="user-self-service-portal"></a>Portale self-service degli utenti

Consentire agli utenti di ottenere in autonomia una chiave monouso per sbloccare un dispositivo crittografato con BitLocker. Una volta usata questa chiave, viene generata una nuova chiave per il dispositivo.

## <a name="prerequisites"></a>Prerequisiti

- Per creare un criterio di gestione di BitLocker, è necessario il ruolo di **amministratore completo** in Configuration Manager.

- Il servizio di ripristino di BitLocker richiede HTTPS per crittografare le chiavi di ripristino attraverso la rete dal client di Configuration Manager al punto di gestione. Sono disponibili due opzioni:

  - Abilitare il sito Web IIS per HTTPS nel punto di gestione che ospita il servizio di ripristino. Questa opzione si applica solo a Configuration Manager versione 2002.<!-- 5925660 -->

  - Configurare il punto di gestione per HTTPS. Questa opzione si applica a Configuration Manager versioni 1910 o 2002.

  Per altre informazioni, vedere [Crittografare i dati di ripristino](../deploy-use/bitlocker/encrypt-recovery-data.md).

- Per usare i report di gestione di BitLocker, installare il ruolo del sistema del sito del punto di Reporting Services. Per altre informazioni, vedere [Configurare la creazione di report in Reporting Manager](../../core/servers/manage/configuring-reporting.md).

    > [!NOTE]
    > Affinché il **report Controllo del ripristino** funzioni dal sito Web di amministrazione e monitoraggio, usare solo un punto di Reporting Services nel sito primario.

- Per usare il portale self-service o il sito Web di amministrazione e monitoraggio, è necessario un server Windows che esegue IIS. È possibile riutilizzare un sistema del sito di Configuration Manager oppure usare un server Web autonomo con connettività al server di database del sito. Usare una [versione del sistema operativo supportata per i server del sistema del sito](../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md).

    > [!NOTE]
    > Installare solo il portale self-service e il sito Web di amministrazione e monitoraggio con un database del sito primario. In una gerarchia installare questi siti Web per ogni sito primario.

- Nel server Web che ospiterà il portale self-service, installare [Microsoft ASP.NET MVC 4.0](https://docs.microsoft.com/aspnet/mvc/mvc4).

- Per l'account utente che esegue lo script del programma di installazione del portale sono necessari i diritti di **sysadmin** di SQL per il server di database del sito. Durante il processo di installazione, lo script imposta i diritti di accesso, utente e ruolo SQL per l'account del computer del server Web. È possibile rimuovere questo account utente dal ruolo sysadmin dopo aver completato l'installazione del portale self-service e del sito Web di amministrazione e monitoraggio.

- La gestione di BitLocker non è supportata nelle macchine virtuali o nei sistemi operativi server. Per questo motivo, alcune caratteristiche potrebbero non funzionare come previsto nelle macchine virtuali o nei sistemi operativi server. Ad esempio, nelle macchine virtuali la gestione di BitLocker non avvierà la crittografia nelle unità fisse. Inoltre le unità fisse aggiuntive delle macchine virtuali potrebbero essere visualizzate come conformi anche se non sono crittografate.

> [!TIP]
> Per impostazione predefinita, il passaggio della sequenza di attività **Attiva BitLocker** consente di crittografare solo lo *spazio usato* nell'unità. Gestione BitLocker usa la crittografia del *disco completo*. Configurare questo passaggio della sequenza di attività per abilitare l'opzione **Usa la crittografia del disco completo**. Per altre informazioni, vedere [Passaggi della sequenza di attività - Attiva BitLocker](../../osd/understand/task-sequence-steps.md#BKMK_EnableBitLocker).

## <a name="next-steps"></a>Passaggi successivi

[Crittografare i dati di ripristino](../deploy-use/bitlocker/encrypt-recovery-data.md) (un prerequisito facoltativo prima di distribuire i criteri per la prima volta)

[Distribuire il client di gestione di BitLocker](../deploy-use/bitlocker/deploy-management-agent.md)
