---
title: Interoperabilità tra versioni
titleSuffix: Configuration Manager
description: Informazioni su come evitare i conflitti tra più gerarchie di Configuration Manager nella stessa rete.
ms.date: 05/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9b0a7859-747f-4495-a2f4-13fd5991f897
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d8d5eeeeafa775514bb46fa0906f22572343611d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693519"
---
# <a name="interoperability-between-different-versions-of-configuration-manager"></a>Interoperabilità tra versioni diverse di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

È possibile installare e usare più gerarchie indipendenti di Configuration Manager all'interno della stessa rete. Tuttavia, dal momento che più gerarchie di Configuration Manager non interagiscono al di fuori del processo di migrazione, per ogni gerarchia sono necessarie configurazioni che impediscono eventuali conflitti. È anche possibile creare determinate configurazioni per consentire alle risorse gestite di interagire con i sistemi del sito dalla gerarchia corretta.  

## <a name="interoperability-between-current-branch-and-earlier-versions"></a><a name="BKMK_SupConfigInterop"></a> Interoperabilità tra Current Branch e versioni precedenti  

Siti di versioni diverse non possono coesistere nella stessa gerarchia di Configuration Manager. Le uniche eccezioni si verificano durante il processo degli scenari di aggiornamento seguenti:

- Da System Center 2012 Configuration Manager a Configuration Manager Current Branch
- Da una versione di Configuration Manager Current Branch a una versione più recente tramite aggiornamenti nella console

È possibile distribuire un sito e una gerarchia di Configuration Manager Current Branch nella stessa destinazione di un sito o di una gerarchia di System Center 2012 Configuration Manager. È necessario impedire ai client delle due versioni di entrare a far parte di un sito dell'altra versione.

Se, ad esempio, due o più gerarchie di Configuration Manager hanno [limiti sovrapposti](../../servers/deploy/configure/boundary-groups.md#overlapping-boundaries) che includono gli stessi percorsi di rete, assegnare ogni nuovo client a un sito specifico anziché usare l'assegnazione sito automatica. Per altre informazioni, vedere [Come assegnare i client a un sito](../../clients/deploy/assign-clients-to-a-site.md).  

Non è possibile, poi, installare un client da System Center 2012 Configuration Manager in un computer che ospita un ruolo del sistema del sito da Configuration Manager Current Branch. Non è possibile neanche installare un client Configuration Manager Current Branch in un computer che ospita un ruolo del sistema del sito da System Center 2012 Configuration Manager.  

Non sono supportati i client e le connessioni seguenti:  

- Client di System Center Configuration Manager 2012 o versioni precedenti del client computer  

- Client di System Center Configuration Manager 2012 o versioni precedenti del client di gestione di dispositivi  

- Client per la gestione dispositivi Windows CE Platform Builder (qualsiasi versione)  

- Connessione VPN di System Center Mobile Device Manager  

### <a name="client-site-assignment-considerations"></a><a name="BKMK_SupConfigSiteAssignment"></a> Considerazioni sull'assegnazione sito dei client  

I client di Configuration Manager possono essere assegnati a un unico sito primario. Non è possibile prevedere l'assegnazione sito effettiva di un client quando si verificano tutte le condizioni seguenti:

- Si usa l'assegnazione sito automatica per assegnare i client a un sito durante l'installazione del client
- Più gruppi di limiti includono lo stesso limite
- I gruppi di limiti hanno siti assegnati diversi

Se i limiti si sovrappongono in più siti e gerarchie di Configuration Manager, i client potrebbero non essere assegnati al sito previsto o, addirittura, non essere assegnati ad alcun sito.  

I client Configuration Manager Current Branch controllano la versione del sito prima di completare l'assegnazione del sito. Se i limiti dei siti si sovrappongono, non è possibile assegnare i client a un sito con una versione precedente. I client System Center 2012 Configuration Manager precedenti, tuttavia, potrebbero essere assegnati erroneamente a un sito di Configuration Manager Current Branch successivo.  

Per evitare che i client vengano assegnati involontariamente al sito sbagliato in caso di sovrapposizione dei limiti in due gerarchie, configurare i parametri di installazione dei client per assegnare i client a un sito specifico.  

## <a name="configuration-manager-limitations-in-a-mixed-version-hierarchy"></a><a name="bkmk_mixed"></a> Limitazioni di Configuration Manager in una gerarchia con più versioni  

Durante l'aggiornamento di una gerarchia di Configuration Manager, in alcuni momenti siti diversi possono avere versioni diverse. Ad esempio, si esegue prima l'aggiornamento del sito di amministrazione centrale. A causa delle finestre di manutenzione del sito, i siti primari vengono aggiornati solo in un secondo momento.  

Quando più siti in un'unica gerarchia eseguono versioni diverse, alcune funzionalità non sono disponibili. Questo comportamento può influire sulla gestione degli oggetti di Configuration Manager nella console di Configuration Manager e sulle funzionalità disponibili per i client. In genere, le funzionalità della versione più recente di Configuration Manager non sono accessibili dai siti o dai client che eseguono una versione precedente del Service Pack.  

### <a name="network-access-account"></a>Account di accesso alla rete

Si esegue l'aggiornamento del sito di amministrazione centrale a Configuration Manager Current Branch. Si visualizzano i dettagli dell'account di accesso alla rete da una console di Configuration Manager connessa al sito aggiornato, che tuttavia non visualizza i dettagli dell'account dai siti che eseguono ancora System Center Configuration Manager 2012.

Dopo l'aggiornamento del sito primario alla stessa versione del sito di amministrazione centrale, i dettagli dell'account sono visibili nella console.

Lo stesso comportamento si applica quando si esegue l'aggiornamento tra versioni diverse di Configuration Manager.

### <a name="boot-images-for-os-deployment"></a>Immagini d'avvio per la distribuzione del sistema operativo

#### <a name="when-upgrading-from-system-center-2012-configuration-manager-to-configuration-manager-current-branch"></a>Quando si esegue l'aggiornamento da System Center 2012 Configuration Manager a Configuration Manager Current Branch

Quando il sito di livello superiore di una gerarchia viene aggiornato a Configuration Manager Current Branch, aggiorna automaticamente le immagini d'avvio predefinite per usare Windows Assessment and Deployment Kit (Windows ADK) versione 10. Usare queste immagini d'avvio solo per le distribuzioni ai client di siti di Configuration Manager Current Branch. Per altre informazioni, vedere [Pianificazione dell'interoperabilità della distribuzione del sistema operativo](../../../osd/plan-design/planning-for-operating-system-deployment-interoperability.md).

#### <a name="when-upgrading-between-configuration-manager-current-branch-versions"></a>Quando si esegue l'aggiornamento tra versioni Current Branch di Configuration Manager

se le nuove versioni di Configuration Manager non aggiornano la versione di Windows ADK in uso, non ci sono effetti sulle immagini d'avvio.

### <a name="new-task-sequence-steps"></a>Nuovi passaggi della sequenza di attività

Quando si crea una sequenza di attività con un passaggio introdotto in una versione di Configuration Manager, ma non disponibile in una versione precedente, possono verificarsi i problemi seguenti:

- Si verifica un errore quando si prova a modificare la sequenza di attività da un sito che esegue una versione precedente di Configuration Manager.

- La sequenza di attività non viene eseguita su un computer che esegue una versione precedente del client Configuration Manager.

### <a name="client-to-down-level-management-point-communications"></a>Comunicazioni tra client e punti di gestione di livello inferiore

Un client di Configuration Manager comunicante con un punto di gestione di un sito che esegue una versione precedente rispetto a quella usata dal client può usare soltanto le funzionalità supportate dalla versione di livello inferiore di Configuration Manager. Se ad esempio si distribuisce contenuto da un sito di Configuration Manager Current Branch aggiornato di recente a un client che comunica con un punto di gestione non ancora aggiornato a tale versione, il client non riesce a usare le nuove funzionalità dell'ultima versione.

### <a name="package-and-task-sequence-deployments-to-legacy-clients"></a>Distribuzioni di sequenze di attività e pacchetti nei client legacy

<!-- SCCMDocs-pr issue #3493 -->

A partire dalla versione 1902, non è possibile distribuire un pacchetto o una sequenza di attività in un client versione 5.7730 o precedente. Per aggirare questa limitazione, aggiornare il client a una versione successiva.

## <a name="software-updates"></a>Aggiornamenti software

### <a name="orchestration-groups"></a>Gruppi di orchestrazione

I gruppi di orchestrazione, introdotti nella versione 2002, non possono essere usati in una gerarchia con versioni miste. <!--SCCMDocs-pr issue ##5056, 6389000-->

## <a name="interoperability-for-the-configuration-manager-console"></a><a name="BKMK_ConsoleInterop"></a> Interoperabilità per la console di Configuration Manager  

Questa sezione contiene informazioni sull'uso della console di Configuration Manager in un ambiente che contiene una combinazione di versioni diverse di Configuration Manager.  

### <a name="an-environment-with-both-system-center-2012-configuration-manager-and-configuration-manager-current-branch"></a>Ambiente con System Center 2012 Configuration Manager e Configuration Manager Current Branch

Per gestire un sito di Configuration Manager, sia la console che il sito a cui si connette la console devono eseguire la stessa versione di Configuration Manager. Non è ad esempio possibile usare una console di System Center 2012 Configuration Manager per gestire un sito di Configuration Manager Current Branch o viceversa.

L'installazione della console di System Center 2012 Configuration Manager e della console di Configuration Manager Current Branch nello stesso computer non è supportata.

### <a name="an-environment-with-multiple-versions-of-configuration-manager"></a>Un ambiente con più versioni di Configuration Manager

Configuration Manager Current Branch non supporta l'installazione di più console di Configuration Manager in un solo computer. Per usare console di diverse versioni di Configuration Manager, installare le diverse console in computer separati.

Durante il processo di aggiornamento a una nuova versione dei siti in una gerarchia è possibile connettere un console a un sito che esegue una versione più recente e visualizzare le informazioni su altri siti in quella gerarchia. Questa configurazione, tuttavia, non è consigliata. È possibile che le differenze tra la versione della console e la versione del sito di Configuration Manager causino problemi di dati. Alcune funzionalità disponibili nell'ultima versione del prodotto non saranno disponibili nella console.

La gestione di un sito quando si usa una console la cui versione non corrisponde alla versione del sito non è supportata. Questa operazione potrebbe causare la perdita di dati e mettere a rischio il sito. Ad esempio, l'uso di una console della versione 1610 per gestire un sito che esegue la versione 1606 non è supportato.
