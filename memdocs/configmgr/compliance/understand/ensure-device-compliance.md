---
title: Garantire la conformità dei dispositivi
titleSuffix: Configuration Manager
description: Gestire la configurazione e la conformità dei dispositivi nell'organizzazione usando Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 7568c9aa-b99e-4466-bfc8-0301aa376930
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: e9844c20373f2442be2c5c1f06f893eae3b0fe57
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692159"
---
# <a name="ensure-device-compliance-with-configuration-manager"></a>Garantire la conformità di dispositivi con Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Le impostazioni di conformità di Configuration Manager offrono gli strumenti e le risorse necessari per gestire la configurazione e la conformità dei dispositivi nell'organizzazione. Questo semplifica il supporto dei requisiti aziendali seguenti:  

-   Confrontare la configurazione di PC Windows, computer Mac, server e dispositivi mobili gestiti con le configurazioni consigliate create internamente oppure ottenute da altri fornitori.  

-   Identificare le configurazioni di dispositivo non autorizzate  

-   Creare report di conformità con criteri normativi e criteri di sicurezza interni  

-   Identificare le vulnerabilità di sicurezza  

-   Fornire all'help desk le informazioni necessarie per rilevare le possibili cause dei problemi e degli eventi imprevisti segnalati identificando le configurazioni non conformi  

-   Correggere automaticamente le impostazioni non conformi nei dispositivi mobili  

-   Correggere la mancata conformità con la distribuzione di applicazioni, pacchetti e programmi o script in una raccolta che viene automaticamente popolata con i dispositivi non conformi  


## <a name="get-started"></a>Operazioni preliminari  
 Informazioni sulle nozioni fondamentali relative alle impostazioni di conformità e alle attività che è possibile eseguire con esse.  

 [Introduzione alle impostazioni di conformità](../../compliance/get-started/get-started-with-compliance-settings.md)  

## <a name="plan-and-design"></a>Pianificare e progettare  
 Prima di iniziare a usare le impostazioni di conformità, assicurarsi di avere implementato i prerequisiti necessari disponibili in questo argomento.  

 [Plan for and configure compliance settings](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md) (Pianificare e configurare le impostazioni di conformità)  

## <a name="common-tasks"></a>Attività comuni  
 In questa sezione sono disponibili alcuni scenari comuni utili per imparare a usare le impostazioni di conformità in Configuration Manager.  

 [Attività comuni per la gestione della conformità](../../compliance/plan-design/common-tasks-for-managing-compliance.md)  

## <a name="remote-connection-profiles"></a>Profili di connessione remota  
 Il tipo di elemento di configurazione consente di configurare i PC degli utenti in modo da effettuare la connessione remota ai computer aziendali quando non sono connessi al dominio o se i computer personali sono connessi su Internet.  

 [Create remote connection profiles](../deploy-use/create-remote-connection-profiles.md) (Creare profili di connessione remota)  

## <a name="user-data-and-profiles"></a>Profili e dati utente  
 Questo tipo di elemento di configurazione contiene le impostazioni che consentono di gestire il reindirizzamento delle cartelle, i file offline e i profili mobili nei computer che eseguono Windows 8 e versioni successive per gli utenti della gerarchia.  

 [Create user data and profiles configuration items](../deploy-use/create-user-data-and-profiles-configuration-items.md) (Creare dati utente ed elementi di configurazione profili)  

## <a name="windows-edition-upgrade-policy"></a>Criteri di aggiornamento dell'edizione Windows  
 I criteri di aggiornamento edizione consentono di aggiornare automaticamente i dispositivi Windows 10 a una versione più recente. È possibile specificare un codice Product Key per aggiornare le versioni desktop di Windows 10 o usare un file di licenza per aggiornare i dispositivi che eseguono Windows 10 Mobile e Windows 10 Holographic.  

 [Upgrade Windows devices with the edition upgrade policy](../deploy-use/upgrade-windows-version.md) (Aggiornare i dispositivi Windows con i criteri di aggiornamento edizione)  
