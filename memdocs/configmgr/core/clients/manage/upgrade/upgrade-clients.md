---
title: Aggiornare i client
titleSuffix: Configuration Manager
description: Informazioni su come aggiornare i client in Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 446c83b5-c292-4e74-ba19-0792ac6b3472
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 95e6ebf1544951b71ca2b60615e3e01b27cc0f3b
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82076680"
---
# <a name="upgrade-clients-in-configuration-manager"></a>Aggiornare i client in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

È possibile usare diversi metodi per aggiornare il software client di Configuration Manager in computer Windows, server UNIX e Linux e computer Mac. Di seguito sono elencati i principali vantaggi e svantaggi di ogni metodo.  

> [!TIP]  
>  Se si esegue l'aggiornamento dell'infrastruttura di server da una versione precedente di Configuration Manager \(ad esempio Configuration Manager 2007 o System Center 2012 Configuration Manager\), è consigliabile completare gli aggiornamenti dei server, tra cui l'installazione di tutti gli aggiornamenti del ramo corrente, prima dell'aggiornamento dei client di Configuration Manager. In questo modo si disporrà anche della versione più recente del software client.  

## <a name="group-policy-installation"></a>Installazione tramite Criteri di gruppo  
 **Piattaforma client supportata:** Windows  

#### <a name="advantages"></a>Vantaggi  

- Non richiede l'individuazione dei computer prima di poter aggiornare il client.  

- Può essere utilizzato per le nuove installazioni di client o per gli aggiornamenti.  

- I computer possono leggere le proprietà di installazione client che sono state pubblicate in Servizi di dominio Active Directory.  

- Non richiede la configurazione e il mantenimento di un account di installazione per il computer client previsto.  

#### <a name="disadvantages"></a>Svantaggi  

- Può causare traffico di rete elevato se viene aggiornato un numero elevato di client.  

- Se lo schema di Active Directory non viene esteso per Configuration Manager, è necessario usare le [impostazioni di Criteri di gruppo](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientGP) per aggiungere le proprietà di installazione del client ai computer presenti nel sito.  


## <a name="logon-script-installation"></a>Installazione tramite script di accesso  
 **Piattaforma client supportata:** Windows  

#### <a name="advantages"></a>Vantaggi  

- Non richiede l'individuazione dei computer prima di poter installare il client.  

- Può essere utilizzato per le nuove installazioni di client o per gli aggiornamenti.  

- Supporta l'utilizzo di proprietà della riga di comando per CCMSetup.  

#### <a name="disadvantages"></a>Svantaggi  

- Può causare traffico di rete elevato se viene aggiornato un numero elevato di client in poco tempo.  

- L'aggiornamento di tutti i computer client può richiedere molto tempo se gli utenti non accedono spesso alla rete.  

  Per altre informazioni, vedere [Come installare i client di Configuration Manager usando script di accesso](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientLogonScript).  

## <a name="manual-installation"></a>Installazione manuale  
 **Piattaforma client supportata:** Windows, UNIX/Linux, Mac OS X  

#### <a name="advantages"></a>Vantaggi  

- Non richiede l'individuazione dei computer prima di poter aggiornare il client.  

- Può essere utile a scopo di test.  

- Supporta l'utilizzo di proprietà della riga di comando per CCMSetup.  

#### <a name="disadvantages"></a>Svantaggi  

- Non prevede automazione, pertanto risulta dispendioso in termini di tempo.  

  Per altre informazioni, vedere i seguenti argomenti:  

- [Come installare manualmente i client di Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual)  

- [Come aggiornare i client per i server Linux e UNIX](../../../../core/clients/manage/upgrade/upgrade-clients-for-linux-and-unix-servers.md)  

- [Come aggiornare i client in computer Mac](../../../../core/clients/manage/upgrade/upgrade-clients-on-mac-computers.md)  

## <a name="upgrade-installation-application-management"></a>Installazione aggiornamento (gestione applicazioni)  
 **Piattaforma client supportata:** Windows  

> [!NOTE]  
>  Non è possibile aggiornare i client di Configuration Manager 2007 con questo metodo. In questo scenario è possibile distribuire il client di Configuration Manager come pacchetto dal sito di Configuration Manager 2007 oppure è possibile usare l'aggiornamento automatico del client, che crea e distribuisce automaticamente un pacchetto contenente la versione più recente del client.  

#### <a name="advantages"></a>Vantaggi  

- Supporta l'utilizzo di proprietà della riga di comando per CCMSetup.  

#### <a name="disadvantages"></a>Svantaggi  

- Può causare elevato traffico di rete quando si esegue la distribuzione del client in raccolte di grandi dimensioni.  

- Può essere utilizzato solo per aggiornare il software client nei computer che sono stati individuati e assegnati al sito.  

  Per altre informazioni, vedere [Come installare i client di Configuration Manager usando un pacchetto e un programma](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientApp).  

## <a name="automatic-client-upgrade"></a>Aggiornamento automatico del client  

> [!NOTE]  
> È possibile usare l'aggiornamento automatico per aggiornare i client di Configuration Manager 2007 a client di Configuration Manager Current Branch. Un client di Configuration Manager 2007 può eseguire l'assegnazione a un sito di Configuration Manager. Non può tuttavia eseguire altre azioni oltre all'aggiornamento automatico del client.  

 **Piattaforma client supportata:** Windows  

#### <a name="advantages"></a>Vantaggi  

- Sulla base del fatto che il momento di installazione viene scelto in modo casuale nel corso del periodo specificato, l'aggiornamento automatico è l'unico metodo adatto agli aggiornamenti su larga scala. Altri metodi sono troppo lenti per la distribuzione su larga scala o non sono basati sul criterio di scelta casuale. 

    > [!Note]
    > La distribuzione pilota del client non è valida per gli aggiornamenti su larga scala perché non prevede il criterio di scelta casuale.  
- Può essere utilizzato per mantenere automaticamente i client presenti nel sito aggiornati alla versione più recente.  

- Richiede un livello di amministrazione minimo.  

#### <a name="disadvantages"></a>Svantaggi  

- Può essere utilizzato solo per aggiornare il software client e non per installare un nuovo client.  

- Si applica a tutti i client presenti nella gerarchia assegnati a un sito. Non può essere definito dalla raccolta.  

- Opzioni di programmazione limitate.  

  Per altre informazioni, vedere [Come aggiornare i client per i computer Windows in System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

## <a name="client-testing"></a>Test di client  
 **Piattaforma client supportata:** Windows  

#### <a name="advantages"></a>Vantaggi  

- Può essere usato per testare nuove versioni client in una raccolta di pre-produzione più piccola.  

- Al termine dei test, i client in pre-produzione vengono alzati di livello alla produzione e aggiornati automaticamente nel sito di Configuration Manager.  

#### <a name="disadvantages"></a>Svantaggi  

- Può essere utilizzato solo per aggiornare il software client e non per installare un nuovo client.  

  [Come testare gli aggiornamenti client in una raccolta di pre-produzione](../../../../core/clients/manage/upgrade/test-client-upgrades.md)  
