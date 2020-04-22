---
title: Selezionare i metodi di individuazione
titleSuffix: Configuration Manager
description: Considerazioni sui metodi da usare e sui siti in cui eseguirli.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 127ce713-d085-430f-ac7b-2701637fe126
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2f08ab44a11b48b4446a372c4f6065ea0d7c63e0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700959"
---
# <a name="select-discovery-methods-to-use-for-configuration-manager"></a>Selezionare i metodi di individuazione da usare per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Per usare in modo efficace l'individuazione di Configuration Manager, è necessario analizzare i metodi da usare e i siti in cui eseguirli.  

 Poiché l'individuazione può generare un ampio volume di traffico sulla rete e i record dei dati di individuazione risultanti possono causare un uso significativo di risorse della CPU durante l'elaborazione, è consigliabile usare solo i metodi di individuazione necessari per soddisfare gli obiettivi. Si potrebbe iniziare a usare solo uno o due metodi di individuazione, quindi abilitare in seguito metodi aggiuntivi in modo controllato per estendere il livello di individuazione nel relativo ambiente. Le informazioni contenute in questo argomento consentono di prendere decisioni informate.  

 Per informazioni sui vari metodi di individuazione, vedere [Informazioni sui metodi di individuazione per Configuration Manager](../../../../core/servers/deploy/configure/about-discovery-methods.md).  

## <a name="select-methods-to-discover-different-things"></a>Selezionare i metodi per individuare elementi diversi  
 Per individuare computer client o risorse utente potenziali di Configuration Manager, è necessario abilitare i metodi di individuazione appropriati. È possibile usare diverse combinazioni di metodi di individuazione per individuare risorse diverse e per ottenere informazioni aggiuntive su tali risorse. I metodi di individuazione usati determinano il tipo di risorse che viene individuato e i servizi e gli agenti di Configuration Manager usati nel processo di individuazione. È inoltre possibile determinare il tipo di informazioni sulle risorse che è possibile individuare.  

### <a name="discover-computers"></a>Individua computer   
Se si vuole individuare computer, è possibile usare **individuazione sistema Active Directory** o **individuazione di rete**.  

 Ad esempio, se si vuole individuare risorse che possano installare il client di Configuration Manager prima di usare l'installazione push client, è possibile eseguire l'individuazione sistema Active Directory. L'uso di questo metodo non solo si individua la risorsa, ma anche informazioni di base ed estese sulla risorsa da Active Directory Domain Services. Tali informazioni potrebbero essere utili nella creazione di query e raccolte complesse da utilizzare per l'assegnazione di impostazioni client o distribuzione di contenuto.

In alternativa, si potrebbe eseguire l'individuazione di rete e usare le relative opzioni per individuare il sistema operativo delle risorse (necessario per usare in seguito l'installazione push client). L'individuazione di rete offre informazioni sulla topologia di rete che non è possibile ottenere con altri metodi di individuazione. Questo metodo non offre tuttavia nessuna informazione sull'ambiente di Active Directory.

 È disponibile anche un metodo denominato **individuazione heartbeat**. È possibile usare l'individuazione heartbeat solo per forzare l'individuazione di client installati da metodi diversi dall'installazione push client. Diversamente da altri metodi di individuazione, l'individuazione heartbeat non può individuare computer che non hanno un client attivo di Configuration Manager. Questa individuazione restituisce un set limitato di informazioni con lo scopo di mantenere un record di database esistente, anziché essere la base di tale record. Le informazioni fornite dall'individuazione heartbeat potrebbero non essere sufficienti per creare query o raccolte complesse.  

 Se si usa l'**individuazione gruppo Active Directory** per individuare l'appartenenza di un gruppo specifico, è possibile individuare informazioni limitate sul sistema o sul computer. Questa individuazione non sostituisce un'individuazione completa di computer, ma può offrire informazioni di base. Tali informazioni sono insufficienti per l'installazione push client.  

### <a name="discover-users"></a>Individuare utenti   
Se si vuole individuare informazioni sugli utenti, è possibile usare **individuazione utente Active Directory**. Simile all'individuazione sistema Active Directory, questo metodo individua gli utenti da Active Directory. E include informazioni di base, oltre a informazioni più dettagliate su Active Directory. È possibile utilizzare queste informazioni per creare query e raccolte complesse simili a quelle per i computer.  

### <a name="discover-group-information"></a>Individuare informazioni sui gruppi   
Se si vuole individuare informazioni sui gruppi e le appartenenze ai gruppi, usare l'**individuazione gruppo Active Directory**. Questo metodo di individuazione consente di creare record di risorse per i gruppi di protezione.  

 È possibile usare questo metodo per eseguire la ricerca di un gruppo Active Directory specifico per individuare i membri di tale gruppo, oltre a tutti gli eventuali gruppi annidati nel gruppo. È anche possibile utilizzare questo metodo per effettuare la ricerca di gruppi in un percorso Active Directory e una ricerca ricorsiva di ogni contenitore figlio di tale percorso nei Servizi di dominio Active Directory.  

 Questo metodo di individuazione può inoltre effettuare la ricerca dell'appartenenza di gruppi di distribuzione. Ciò consente di identificare le relazioni di gruppo di utenti e computer.  

 Quando si individua un gruppo, è inoltre possibile individuare informazioni limitate sui relativi membri. Questa individuazione non sostituisce comunque i metodi di individuazione sistema o utente Active Directory. È in genere sufficiente per compilare query complesse e raccolte o servire come base di un'installazione push client.  

### <a name="discover-infrastructure"></a>Individuare infrastrutture   
Sono disponibili due metodi per individuare l'infrastruttura di rete, ovvero **individuazione foresta Active Directory** e **individuazione di rete**.  

 Usare l'individuazione foresta Active Directory per effettuare la ricerca in una foresta di Active Directory di informazioni sulle subnet e sulle configurazioni del sito di Active Directory. Queste configurazioni possono essere quindi immesse automaticamente in Configuration Manager come percorsi di limite.  

 Quando si desidera individuare la topologia di rete, utilizzare l'individuazione di rete. Mentre altri metodi di individuazione restituiscono informazioni relative a Active Directory Domain Services e possono identificare il percorso di rete corrente di un client, non offrono informazioni sull'infrastruttura basate sulle subnet e sulla topologia del router della rete.  

##  <a name="discovery-data-is-shared-among-sites"></a><a name="bkmk_shared"></a> I dati di individuazione vengono condivisi tra i siti  
 Dopo che Configuration Manager aggiunge i dati di individuazione a un database, questi vengono rapidamente condivisi in tutti i siti della gerarchia. Poiché l'individuazione delle stesse informazioni in più siti della gerarchia non offre nessun vantaggio, impostare un'istanza singola di ogni metodo di individuazione in un singolo sito. È consigliabile eseguire questa operazione invece di eseguire più istanze di un singolo metodo in siti diversi.  

 Tuttavia, per alcuni ambienti può essere utile assegnare lo stesso metodo di individuazione da eseguire in più siti, con configurazioni e pianificazioni distinte. Ad esempio, quando si usa l'individuazione di rete, potrebbe essere necessario impostare ogni sito per individuare la propria rete locale, anziché provare a individuare tutti i percorsi di rete in una WAN.

Se si configurano più istanze degli stessi metodi di individuazione da eseguire in siti diversi, pianificare attentamente la configurazione di ogni sito. Evitare che due o più siti individuino le stesse risorse dalla rete o da Active Directory. Questo metodo può usare larghezza di banda di rete aggiuntiva e creare record dei dati di individuazione duplicati.

La tabella seguente identifica in quali siti è possibile configurare i vari metodi di individuazione.  

|Metodo di individuazione|Percorsi supportati|  
|----------------------|-------------------------|  
|Individuazione foresta Active Directory|Sito di amministrazione centrale<br /><br /> Sito primario|  
|Individuazione gruppo Active Directory|Sito primario|  
|Individuazione sistema Active Directory|Sito primario|  
|individuazione utenti di Active Directory|Sito primario|  
|Individuazione heartbeat<sup>1</sup>|Sito primario|  
|Individuazione rete|Sito primario<br /><br /> Sito secondario|  

 <sup>1</sup> I siti secondari non sono in grado di configurare l'individuazione heartbeat, ma possono ricevere i record dei dati di individuazione heartbeat da un client.  

 Quando i siti secondari eseguono l'individuazione di rete o ricevono i DDR dell'individuazione heartbeat, trasferiscono tali DDR mediante replica basata su file nel relativo sito primario padre. Infatti, solo i siti primari e i siti di amministrazione centrale possono elaborare i record dei dati di individuazione. Per altre informazioni su come vengono elaborati i record dei dati di individuazione, vedere [About Discovery Data Records](../../../../core/servers/deploy/configure/run-discovery.md#BKMK_DDRs) (Informazioni sui record dei dati di individuazione).  

## <a name="considerations-for-different-discovery-methods"></a>Considerazioni per i vari metodi di individuazione  
 Poiché ogni ambiente di rete e server del sito è diverso, è consigliabile limitare le configurazioni iniziali per l'individuazione. Monitorare quindi attentamente la capacità di ogni server del sito di elaborare i dati di individuazione generati.  

Quando si usa un metodo di individuazione **Active Directory** per sistemi, utenti o gruppi:  

-   Eseguire l'individuazione in un sito che dispone di una connessione di rete veloce ai controller di dominio.  

-   Prendere in considerazione la topologia di replica di Active Directory per garantire all'individuazione l'accesso alle informazioni più recenti.  

-   Valutare l'ambito della configurazione dell'individuazione e limitare l'individuazione solo ai gruppi e ai percorsi di Active Directory da individuare.  

Se si usa l'**individuazione di rete**:  

-   Per individuare la topografia di rete, utilizzare una configurazione iniziale limitata.  

-   Dopo aver individuato la topografia di rete, impostare l'individuazione di rete per l'esecuzione in siti specifici centrali rispetto alle aree di rete che si vuole individuare in modo più completo.  

Poiché l'**individuazione heartbeat** non viene eseguita in un sito specifico, non è necessario prenderla in considerazione in fase di pianificazione generale per stabilire dove eseguire l'individuazione.  

##  <a name="best-practices-for-discovery"></a><a name="bkmk_best"></a> Procedure consigliate per l'individuazione  
Per ottenere risultati ottimali con l'individuazione, è consigliabile eseguire quanto segue:

- **Prima di eseguire l'individuazione gruppo Active Directory, eseguire l'individuazione sistema Active Directory e l'individuazione utente Active Directory.**  

  In caso di individuazione di un computer o di un utente non individuato precedentemente come membro di un gruppo, l'individuazione gruppo Active Directory tenta di individuare dettagli di base relativi all'utente o al computer. Poiché l'individuazione gruppo Active Directory non è ottimizzata per questo tipo di individuazione, il processo può comprometterne la velocità di esecuzione. L'individuazione gruppo Active Directory individua solo i dettagli di base relativi agli utenti e ai computer individuati, ma non crea un record di individuazione utente o computer completo. Quando si esegue l'individuazione sistema Active Directory e l'individuazione utente Active Directory, sono disponibili gli attributi di Active Directory aggiuntivi relativi a ogni oggetto. Di conseguenza, l'individuazione gruppo Active Directory risulta più efficiente.  

- **Quando viene impostata l'individuazione gruppo Active Directory, è sufficiente specificare solo i gruppi usati con Configuration Manager.**  

  Per controllare l'uso delle risorse da parte dell'individuazione gruppo Active Directory, specificare solo i gruppi usati con Configuration Manager. L'individuazione gruppo Active Directory, infatti, esegue ricerche ricorsive in ogni gruppo individuato relativamente a utenti, computer e gruppi nidificati. La ricerca di ogni gruppo annidato può espandere l'ambito dell'individuazione gruppo Active Directory e ridurre le prestazioni. Se si configura anche l'individuazione differenziale per l'individuazione gruppo Active Directory, questo metodo di individuazione consente di monitorare le modifiche di ogni gruppo. Le prestazioni vengono ulteriormente ridotte quando il metodo deve eseguire ricerche di gruppi non necessari.  

- **Impostare metodi di individuazione con un intervallo maggiore tra le individuazioni complete e un periodo più frequente per le individuazioni differenziali.**  

  Poiché l'individuazione differenziale usa un numero inferiore di risorse rispetto a un ciclo di individuazione completa e può identificare risorse nuove o modificate in Active Directory, è possibile ridurre la frequenza dei cicli di individuazione completa a esecuzioni settimanali o meno frequenti. L'individuazione differenziale per l'individuazione sistema Active Directory, l'individuazione utente Active Directory e l'individuazione gruppo Active Directory identificano quasi tutte le modifiche apportate agli oggetti Active Directory e possono mantenere dati accurati di individuazione per le risorse.  

- **Eseguire i metodi di individuazione Active Directory in un sito primario che abbia un percorso di rete molto vicino al controller di dominio di Active Directory.**  

  Per migliorare le prestazioni dell'individuazione Active Directory, è consigliabile eseguire l'individuazione in un sito primario che abbia una connessione di rete veloce ai controller di dominio. Se si esegue lo stesso metodo di individuazione Active Directory in più siti, è consigliabile impostare ogni metodo di individuazione per evitare sovrapposizione. A differenza delle versioni precedenti di Configuration Manager, i dati di individuazione vengono condivisi tra i siti. Non è quindi necessaria l'individuazione delle stesse informazioni in più siti. Per altre informazioni, vedere [I dati di individuazione vengono condivisi tra i siti](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md#bkmk_shared).  

- **Se si prevede di creare automaticamente limiti dai dati di individuazione, è consigliabile eseguire l'individuazione foresta Active Directory in un unico sito.**  

  Se l'individuazione foresta Active Directory viene eseguita in più siti di una gerarchia, è consigliabile attivare solo le opzioni per la creazione automatica dei limiti in un unico sito. Quando l'individuazione foresta Active Directory viene eseguita in tutti i siti e crea i limiti, infatti, Configuration Manager non può unire tali limiti in un unico oggetto limite. Se l'individuazione foresta Active Directory viene configurata per la creazione automatica dei limiti in più siti, possono essere generati oggetti limite duplicati nella console di Configuration Manager.  
