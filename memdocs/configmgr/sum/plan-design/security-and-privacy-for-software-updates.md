---
title: Sicurezza e privacy per gli aggiornamenti software
titleSuffix: Configuration Manager
description: Seguire queste procedure consigliate per gli aggiornamenti software ed esaminare le informazioni sulla modalità di gestione delle informazioni sulla privacy di Configuration Manager.
manager: dougeby
ms.date: 10/06/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 41d6d5d8-ba84-4efb-b105-4d1eed239824
author: mestew
ms.author: mstewart
ms.openlocfilehash: 5c7a1ac5e88aa669ae1d5e6bb9333e1f54fb5980
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708729"
---
# <a name="security-and-privacy-for-software-updates-in-configuration-manager"></a>Sicurezza e privacy per gli aggiornamenti software in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Questo argomento contiene informazioni sulla sicurezza e la privacy per gli aggiornamenti software in Configuration Manager.  

##  <a name="security-best-practices-for-software-updates"></a><a name="BKMK_Security_HardwareInventory"></a> Procedure di sicurezza consigliate per gli aggiornamenti software  
 Quando si distribuiscono gli aggiornamenti software ai client, utilizzare le seguenti procedure ottimali di protezione:  

-   Non modificare le autorizzazioni predefinite nei pacchetti di aggiornamento software.  

     Per impostazione predefinita, i pacchetti di aggiornamento software sono impostati in modo da consentire agli amministratori il **Controllo completo** e agli utenti l'accesso in **Lettura** . Se si modificano queste autorizzazioni, è possibile che un utente malintenzionato aggiunga, rimuova o elimini aggiornamenti software.  

-   Controllare l'accesso al percorso download per gli aggiornamenti software.  

     Per gli account computer per il provider SMS, il server del sito e l'utente amministratore che scaricherà gli aggiornamenti software nel percorso download è necessario disporre dell'accesso in **Scrittura** al percorso download. Limitare l'accesso al percorso download consente di ridurre il rischio di manomissioni da parte di utenti malintenzionati dei file origine degli aggiornamenti software nel percorso download.  

     Inoltre, se si utilizza una condivisione UNC per il percorso download, proteggere il canale di rete utilizzando una firma SMB o IPsec per impedire manomissioni dei file origine degli aggiornamenti software durante il trasferimento in rete.  

-   Per valutare la durata della distribuzione, utilizzare l'ora UTC.  

     Se gli utenti utilizzano l'ora locale invece dell'ora UTC potrebbero ritardare l'installazione di aggiornamenti software modificando il fuso orario nel computer  

-   Attivare SSL in WSUS (Windows Server Update Services) e seguire le procedure ottimali per la protezione di WSUS.  

     Individuare e seguire le procedure di sicurezza consigliate per la versione di WSUS in uso con Configuration Manager.  

    > [!IMPORTANT]  
    >  Se si configura il punto di aggiornamento software per attivare le comunicazioni SSL per il server WSUS, è necessario configurare radici virtuali per SSL nel server WSUS.  

-   Attivare il controllo CRL.  

     Per impostazione predefinita, Configuration Manager non controlla l'elenco di revoche di certificati (CRL) per verificare la firma degli aggiornamenti software prima della distribuzione nei computer. Il controllo dell'elenco CRL a ogni utilizzo del certificato offre una maggiore protezione dall'utilizzo di un certificato revocato, ma introduce un ritardo nella connessione e genera un'ulteriore elaborazione nel computer che esegue il controllo CRL.  

     Per altre informazioni su come attivare il controllo CRL per gli aggiornamenti software, vedere [Come abilitare il controllo CRL per gli aggiornamenti software](../get-started/manage-settings-for-software-updates.md#crl-checking-for-software-updates).  

-   Configurare WSUS per l'utilizzo di un sito Web personalizzato.  

     Quando si installa WSUS nel punto di aggiornamento software, è possibile scegliere di utilizzare il sito Web IIS predefinito o di creare un sito Web WSUS personalizzato. Creare un sito Web personalizzato per WSUS in modo che IIS ospiti i servizi WSUS in un sito Web virtuale dedicato invece di condividere lo stesso sito Web usato dagli altri sistemi del sito di Configuration Manager o da altre applicazioni.  

     Per altre informazioni, vedere [Configurare WSUS per l'uso di un sito Web personalizzato](plan-for-software-updates.md#BKMK_CustomWebSite).  

##  <a name="privacy-information-for-software-updates"></a><a name="BKMK_Privacy_HardwareInventory"></a> Informazioni sulla privacy per gli aggiornamenti software  
 Gli aggiornamenti software consentono di esaminare i computer del client per stabilire quali aggiornamenti software sono necessari, quindi reinviano le informazioni al database del sito. Durante il processo di aggiornamento del software, Configuration Manager può trasmettere le informazioni tra i client e i server che identificano gli account di accesso e del computer.  

 Configuration Manager mantiene le informazioni sullo stato relative al processo di distribuzione del software. Le informazioni sullo stato non vengono crittografate durante la trasmissione o l'archiviazione. Le informazioni sullo stato vengono archiviate nel database di Configuration Manager ed eliminate dalle attività di manutenzione del database stesso. Nessuna informazione sullo stato viene inviata a Microsoft.  

 L'uso degli aggiornamenti software di Configuration Manager per installare gli aggiornamenti software nei computer client può essere soggetto alle condizioni di licenza software per tali aggiornamenti, che si distinguono dalle condizioni di licenza software per Configuration Manager. Esaminare sempre e accettare le condizioni di licenza software prima di installare gli aggiornamenti software tramite Configuration Manager.  

 Per impostazione predefinita, Configuration Manager non implementa gli aggiornamenti software e richiede di eseguire diversi passaggi di configurazione prima di raccogliere le informazioni.  

 Prima di configurare gli aggiornamenti software, considerare i requisiti sulla privacy.  
