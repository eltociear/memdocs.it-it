---
title: Nozioni fondamentali su siti e gerarchie
titleSuffix: Configuration Manager
description: Informazioni di base su siti e gerarchie di Configuration Manager.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4db1e15f-e832-4cf9-be33-d3971e635a55
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 04ed22436d750572fed8ce898c5ed3a23b71f239
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707029"
---
# <a name="fundamentals-of-sites-and-hierarchies-for-configuration-manager"></a>Nozioni fondamentali su siti e gerarchie per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Una distribuzione di Configuration Manager deve essere installata in un dominio di Active Directory. La base della distribuzione include uno o più siti di Configuration Manager che formano una gerarchia di siti. Da un singolo sito a una gerarchia a più siti, il tipo e il percorso dei siti installati offrono la possibilità di espandere la distribuzione quando necessario per assicurare i servizi essenziali a utenti e dispositivi gestiti.

## <a name="hierarchies-of-sites"></a>Gerarchie di siti
Quando si installa Configuration Manager per la prima volta, il primo sito di Configuration Manager installato determina l'ambito della gerarchia. Il primo sito di Configuration Manager è la base da cui gestire i dispositivi e gli utenti nell'azienda. Questo primo sito deve essere un sito di amministrazione centrale o un sito primario autonomo.  

 Un *sito di amministrazione centrale* è ideale per distribuzioni su larga scala e offre un punto centrale di amministrazione, nonché la flessibilità necessaria per supportare i dispositivi distribuiti in un'infrastruttura di rete globale. Dopo aver installato un sito di amministrazione centrale, è necessario installare uno o più siti primari come siti figlio. Questa configurazione è necessaria perché un sito di amministrazione centrale non supporta direttamente la gestione dei dispositivi, che è invece la funzione di un sito primario. Un sito di amministrazione centrale supporta più siti primari figlio. I siti primari figlio vengono usati per gestire direttamente i dispositivi e controllare la larghezza di banda di rete quando i dispositivi gestiti si trovano in località geografiche diverse.  

 Un *sito primario autonomo* è ideale per distribuzioni di dimensioni minori e può essere usato per gestire i dispositivi senza dover installare siti aggiuntivi. Anche se un sito primario autonomo può limitare le dimensioni della distribuzione, supporta uno scenario di espansione successiva della gerarchia tramite l'installazione di un nuovo sito di amministrazione centrale. In questo scenario di espansione il sito primario autonomo diventa un sito primario figlio ed è quindi possibile installare altri siti primari figlio al di sotto del sito di amministrazione centrale. È quindi possibile espandere la distribuzione iniziale in base alla crescita futura dell'azienda.  

> [!TIP]  
>  Un sito primario autonomo e un sito primario figlio sono in realtà lo stesso tipo di sito, ovvero un sito primario. La differenza nel nome è basata sulla relazione gerarchica creata quando si usa anche un sito di amministrazione centrale. Questa relazione gerarchica può anche limitare l'installazione di certi ruoli del sistema del sito che estendono le funzionalità di Configuration Manager. Questa limitazione dei ruoli è dovuta al fatto che determinati ruoli del sistema del sito possono essere installati solo nel livello superiore della gerarchia, in un sito di amministrazione centrale o in un sito primario autonomo.  

 Dopo aver installato il primo sito, è possibile installarne altri. Se il primo sito è un sito di amministrazione centrale, è possibile installare uno o più siti primari figlio. Dopo aver installato un sito primario (autonomo o primario figlio), è possibile installare uno o più siti secondari.  

 Un *sito secondario* può essere installato solo come sito figlio al di sotto di un sito primario. Questo tipo di sito estende la copertura del sito primario per la gestione dei dispositivi in punti che hanno una connessione di rete lenta al sito primario. Anche se un sito secondario estende il sito primario, il sito primario gestisce tutti i client. Il sito secondario offre il supporto per i dispositivi nella posizione remota tramite la compressione e quindi la gestione del trasferimento in rete delle informazioni inviate (distribuite) ai client e restituite dai client al sito.  

 I diagrammi seguenti mostrano alcuni esempi di strutture di sito.  

 ![Esempi di gerarchia](media/Hierarchy_examples.png)  

 Per altre informazioni, vedere i seguenti argomenti:  

-   [Introduzione a Configuration Manager](../../core/understand/introduction.md)  

-   [Progettare una gerarchia di siti per Configuration Manager](../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md)  

-   [Installare i siti di Configuration Manager](../servers/deploy/install/installing-sites.md)  

## <a name="site-system-servers-and-site-system-roles"></a>Server di sistema del sito e ruoli del sistema del sito  
 Ogni sito di Configuration Manager installa *ruoli del sistema del sito* che supportano operazioni di gestione. Quando si installa un sito, per impostazione predefinita vengono installati i ruoli seguenti:

-   Il ruolo del server del sito viene assegnato al computer in cui si installa il sito.

-   Il ruolo di server di database del sito viene assegnato all'istanza di SQL Server che ospita il database del sito.

Altri ruoli del sistema del sito sono facoltativi e vengono usati solo quando si vuole usare la funzionalità attiva in un ruolo del sistema del sito. Qualsiasi computer che ospita un ruolo del sistema del sito viene chiamato server del sistema del sito.  

 Per una distribuzione di dimensioni minori di Configuration Manager , è possibile eseguire inizialmente tutti i ruoli del sistema del sito nel computer server del sito. Con l'aumentare delle esigenze e delle dimensioni dell'ambiente gestito, è quindi possibile installare altri server del sistema del sito per ospitare ulteriori ruoli del sistema del sito e migliorare l'efficienza del sito nel fornire servizi a più dispositivi.  

 Per informazioni sui diversi ruoli del sistema del sito, vedere [Ruoli del sistema del sito](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles) in [Pianificare i server e i ruoli del sistema del sito per Configuration Manager](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).

## <a name="publishing-site-information-to-active-directory-domain-services"></a>Pubblicazione di informazioni sul sito in Servizi di dominio Active Directory  
 Per semplificare la gestione di Configuration Manager, è possibile estendere lo schema di Active Directory in modo da supportare i dettagli usati da Configuration Manager e quindi fare in modo che i siti pubblichino le proprie informazioni principali in Active Directory Domain Services. I computer da gestire possono quindi recuperare in modo sicuro le informazioni correlate al sito da un'origine attendibile di Active Directory Domain Services. Le informazioni che possono essere recuperate dai client identificano i siti disponibili, i server del sistema del sito e i servizi forniti dai server del sistema del sito.  

 L'*estensione dello schema di Active Directory* avviene una sola volta per ogni foresta e può essere eseguita prima o dopo l'installazione di Configuration Manager.   Quando si estende lo schema, è necessario creare un nuovo contenitore di Active Directory denominato System Management in ogni dominio. Il contenitore include un sito di Configuration Manager che pubblicherà i dati a disposizione dei client. Per altre informazioni, vedere [Preparare Active Directory per la pubblicazione di siti](../../core/plan-design/network/extend-the-active-directory-schema.md).  

 La*pubblicazione dei dati del sito* migliora la sicurezza della gerarchia di Configuration Manager e riduce il sovraccarico amministrativo, ma non è necessaria per le funzionalità di base di Configuration Manager.  
