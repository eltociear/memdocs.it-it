---
title: Individuare risorse dei dispositivi e degli utenti
titleSuffix: Configuration Manager
description: Leggere la panoramica del processo di individuazione e dei record di dati dell'individuazione.
ms.date: 02/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 30844519-ce14-456f-bfb8-4318b578e9f6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1869c9e6de455b7086a051db91bb26bc00a91a5f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700989"
---
# <a name="run-discovery-for-configuration-manager"></a>Eseguire l'individuazione per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Usare uno o più metodi di individuazione in Configuration Manager per trovare le risorse del computer e dell'utente che è possibile gestire. I metodi di individuazione consentono anche di identificare l'infrastruttura di rete nell'ambiente in uso. Esistono diversi metodi che è possibile usare per trovare componenti differenti e ciascuno di essi presenta configurazioni e limitazioni specifiche.  

## <a name="overview-of-discovery"></a>Panoramica dell'individuazione  
 L'individuazione è il processo con cui Configuration Manager rileva ciò che è possibile gestire. Di seguito sono indicati i metodi di individuazione disponibili:  

-   Individuazione foresta Active Directory  

-   Individuazione gruppo Active Directory  

-   Individuazione sistema Active Directory  

-   individuazione utenti di Active Directory  

-   Individuazione heartbeat  

-   Individuazione rete  

-   Individuazione server  

> [!TIP]  
>  Informazioni sui singoli metodi di individuazione sono disponibili nell'argomento [Informazioni sui metodi di individuazione per Configuration Manager](../../../../core/servers/deploy/configure/about-discovery-methods.md).  
>   
>  Per assistenza nella scelta dei metodi da usare e dei siti della gerarchia, vedere l'argomento [Selezionare i metodi di individuazione per Configuration Manager](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md).  

 Per la maggior parte dei metodi di individuazione, è necessario abilitare il metodo scelto in un sito e quindi impostarlo per la ricerca in specifici percorsi di rete o di Active Directory. Durante l'esecuzione, vengono eseguite query nel percorso specificato per ottenere informazioni sui dispositivi o sugli utenti che Configuration Manager può gestire. Quando un metodo di individuazione rileva correttamente un'informazione su una risorsa, questa viene inserita in un file denominato record dei dati di individuazione. Tale file viene quindi elaborato da un sito di amministrazione centrale o primario. L'elaborazione di un record dei dati di individuazione crea un nuovo record nel database del sito per le risorse appena individuate oppure aggiorna i record esistenti con le nuove informazioni.  

 Alcuni metodi di individuazione possono generare un notevole volume di traffico di rete e i record dei dati di individuazione risultanti possono causare un uso significativo di risorse della CPU durante l'elaborazione. Di conseguenza, è consigliabile pianificare l'uso esclusivo dei metodi di individuazione necessari per il raggiungimento degli obiettivi prefissati. Si potrebbe iniziare a usare solo uno o due metodi di individuazione, quindi abilitare in seguito metodi aggiuntivi in modo controllato per estendere il livello di individuazione nel relativo ambiente.  

 Dopo essere state aggiunte al database del sito, le informazioni di individuazione vengono replicate in ogni sito della gerarchia, indipendentemente dal sito in cui sono state individuate o elaborate. Quindi, nonostante sia possibile configurare diverse pianificazioni e impostazioni per i metodi di individuazione nei diversi siti, è preferibile eseguire un metodo di individuazione in un solo sito. Questo accorgimento diminuisce l'uso della larghezza di banda mediante azioni di individuazione dei duplicati e riduce l'elaborazione dei dati di individuazione ridondanti in più siti.  

 È possibile usare i dati di individuazione per creare raccolte e query personalizzate che raggruppano in modo logico le risorse per attività di gestione. Ad esempio:  

-   Push o aggiornamento delle installazioni client.  

-   Distribuzione del contenuto a utenti o dispositivi.  

-   Distribuzione delle impostazioni client e delle configurazioni associate.

##  <a name="about-discovery-data-records"></a><a name="BKMK_DDRs"></a> Informazioni sui record dei dati di individuazione  
 I record dei dati di individuazione sono file creati da un metodo di individuazione. Tali file contengono informazioni su una risorsa che è possibile gestire in Configuration Manager, ad esempio computer, utenti e, in alcuni casi, l'infrastruttura di rete. Questi vengono elaborati nei siti primari o nei siti di amministrazione centrale. Dopo l'immissione nel database delle informazioni sulle risorse contenute nel record dei dati di individuazione, questo viene eliminato e le informazioni vengono replicate come dati globali in tutti i siti della gerarchia.  

 Il sito in cui viene elaborato un record dei dati di individuazione dipende dalle informazioni contenute:  

-   I record dei dati di individuazione per le nuove risorse individuate non presenti nel database vengono elaborati nel sito di livello superiore della gerarchia. Il sito di livello superiore crea un nuovo record di risorse nel database e assegna a tale record un identificatore univoco. I record dei dati di individuazione vengono trasferiti mediante replica basata su file fino a raggiungere il sito di livello superiore.  

-   I record dei dati di individuazione per gli oggetti rilevati in precedenza vengono elaborati nei siti primari. I siti primari figlio non trasferiscono i record dei dati di individuazione nel sito di amministrazione centrale se questi contengono informazioni su una risorsa già presente nel database.  

-   I siti secondari non elaborano i record dei dati di individuazione e li trasferiscono sempre al relativo sito primario padre con la replica basata su file.  

I file dei record dei dati di individuazione si distinguono mediante l'estensione DDR e solitamente hanno una dimensione di circa 1 KB.  

## <a name="get-started-with-discovery"></a>Introduzione all'individuazione:  
 Prima di usare la console di Configuration Manager per impostare l'individuazione, è necessario comprendere le differenze tra i metodi e le operazioni consentite. Per alcuni metodi è inoltre importante comprendere le relative limitazioni.  

Gli argomenti seguenti offrono informazioni basilari per l'uso corretto dei metodi di individuazione:  

-   [Informazioni sui metodi di individuazione per Configuration Manager](../../../../core/servers/deploy/configure/about-discovery-methods.md)  

-   [Selezionare i metodi di individuazione da usare per Configuration Manager](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md)  

Quindi, dopo aver stabilito quali metodi usare, vedere le informazioni relative all'impostazione di ogni metodo nell'argomento [Configurare i metodi di individuazione per Configuration Manager](../../../../core/servers/deploy/configure/configure-discovery-methods.md).  
