---
title: Preparare server Windows
titleSuffix: Configuration Manager
description: Assicurarsi che un computer soddisfi i prerequisiti per l'uso come server del sito o server di sistema del sito per Configuration Manager.
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2aca914f-641e-4bc8-98d4-bbf0a2a5276f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7e4e84b55c929dd878cb0720b3f61dfceedcf449
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82904102"
---
# <a name="prepare-windows-servers-to-support-configuration-manager"></a>Preparare i server di Windows per il supporto di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Per poter usare un computer Windows come server di sistema del sito per Configuration Manager, è necessario che il computer soddisfi i prerequisiti per l'uso previsto come server del sito o server di sistema del sito.  

- Questi prerequisiti includono spesso uno o più ruoli o funzionalità di Windows, che vengono abilitati usando Server Manager del computer.  

- Dal momento che il metodo per abilitare i ruoli e le funzionalità di Windows cambia in base alle versioni del sistema operativo, vedere la documentazione della versione del sistema operativo in uso per informazioni dettagliate sulla configurazione.  

Le informazioni contenute in questo articolo offrono una panoramica dei tipi di configurazioni Windows necessari per il supporto dei sistemi del sito Configuration Manager. Per informazioni dettagliate sulla configurazione dei ruoli di sistema del sito specifico, vedere [Prerequisiti del sito e del sistema del sito](../configs/site-and-site-system-prerequisites.md).

##  <a name="windows-features-and-roles"></a><a name="BKMK_WinFeatures"></a> Ruoli e funzionalità di Windows  
Quando si configurano i ruoli e le funzionalità di Windows in un computer, potrebbe essere necessario riavviare il computer per completare la configurazione. È quindi consigliabile identificare i computer che ospiteranno i ruoli del sistema del sito prima di installare un sito di Configuration Manager o un server del sistema del sito.

### <a name="features"></a>Caratteristiche  
le funzionalità di Windows seguenti sono richieste in alcuni server del sistema del sito e devono essere configurate prima di installare un ruolo del sistema del sito nel computer.  

- **.NET Framework**: inclusi  

    - ASP.NET  
    - Attivazione HTTP  
    - Attivazione non HTTP  
    - Servizi Windows Communication Foundation (WCF)  

    Per i diversi ruoli del sistema del sito sono necessarie versioni diverse di .NET Framework.  

    Dal momento che .NET Framework 4.0 e versioni successive non è compatibile con le versioni precedenti e non può sostituire la versione 3.5 e precedenti, quando sono richieste versioni diverse pianificare l'abilitazione di ogni versione nello stesso computer.  

- **Servizio trasferimento intelligente in background (BITS)** : I punti di gestione richiedono BITS (e le opzioni selezionate automaticamente) per supportare la comunicazione con i dispositivi gestiti.  

- **BranchCache**: i punti di distribuzione possono essere configurati con BranchCache per supportare i client che usano BranchCache.  

- **Deduplicazione dati**: i punti di distribuzione possono essere configurati con la deduplicazione dei dati, che offre dei vantaggi.  

- **Compressione differenziale remota (RDC)** : Ogni computer che ospita un server del sito o un punto di distribuzione richiede una compressione differenziale remota (RDC). La compressione differenziale remota viene usata per generare le firme dei pacchetti ed eseguire confronti tra le firme.  

### <a name="roles"></a>Ruoli  
I ruoli di Windows seguenti sono necessari per supportare specifiche funzionalità, ad esempio gli aggiornamenti software e le distribuzioni del sistema operativo, mentre IIS è richiesto per la maggior parte dei ruoli del sistema del sito più comuni.  

- **Servizio Registrazione dispositivi di rete** (in Servizi certificati Active Directory): questo ruolo di Windows è un prerequisito per l'uso dei profili dei certificati in Configuration Manager.  

- **Server Web (IIS)** : include:  
    - Funzionalità HTTP comuni  
          - Reindirizzamento HTTP  
    - Sviluppo applicazioni  
          - Estendibilità .NET  
          - ASP.NET  
          - Estensioni ISAPI  
          - Filtri ISAPI  
    - Strumenti di gestione  
          - Compatibilità Gestione IIS 6  
          - Compatibilità Metabase IIS 6  
          - Compatibilità di Windows Management Instrumentation (WMI) con IIS 6  
    - Sicurezza  
          - Filtro richieste  
          - Autenticazione di Windows  

  I ruoli del sistema del sito seguenti usano una o più delle configurazioni IIS elencate:  
  - Punto per servizi Web del Catalogo applicazioni  
  - Punto per siti Web del Catalogo applicazioni  
  - Punto di distribuzione  
  - Punto di registrazione  
  - Punto proxy di registrazione  
  - Punto di stato di fallback  
  - Punto di gestione  
  - Punto di aggiornamento software  
  - Punto di migrazione stato     

  La versione minima di IIS richiesta è la versione fornita dal sistema operativo del server del sito.  

  Oltre a queste configurazioni IIS, potrebbe essere necessario configurare [Filtro richieste IIS per i punti di distribuzione](#BKMK_IISFiltering).  

- **Servizi di distribuzione Windows**: questo ruolo viene usato con la distribuzione del sistema operativo.  

- **Windows Server Update Services**: questo ruolo è richiesto per gli aggiornamenti software.  


##  <a name="iis-request-filtering-for-distribution-points"></a><a name="BKMK_IISFiltering"></a> Filtro richieste IIS per i punti di distribuzione  
Per impostazione predefinita, IIS usa il filtro richieste per bloccare l'accesso di diverse estensioni di file e percorsi di cartelle con la comunicazione HTTP o HTTPS. In un punto di distribuzione questo impedisce ai client di scaricare i pacchetti con estensioni o percorsi di cartelle bloccati.  

Quando i file origine pacchetto contengono estensioni bloccate in IIS dalla configurazione del filtro richieste, è necessario configurare il filtro richieste per abilitarle. Per farlo, [modificare la funzionalità del filtro richieste](https://docs.microsoft.com/previous-versions/orphan-topics/ws.11/hh831621(v=ws.11)) in Gestione IIS nei computer del punto di distribuzione.  

Le estensioni di file seguenti vengono usate da Configuration Manager per applicazioni e pacchetti. Verificare che le configurazioni del filtro richieste non blocchino queste estensioni di file:  

- PCK  
- PKG  
- STA  
- TAR  

Ad esempio, i file di origine per una distribuzione software potrebbero includere una cartella denominata **bin**o un file con estensione **mdb**.  

- Per impostazione predefinita, il filtro richieste IIS blocca l'accesso a questi elementi (**bin** è bloccato perché è un segmento nascosto e **mdb** è bloccato in quanto estensione).  

- Quando si usa la configurazione IIS predefinita in un punto di distribuzione, i client che usano BITS non riescono a scaricare questa distribuzione del software dal punto di distribuzione e indicano che sono in attesa del contenuto.  

- Per consentire ai client di scaricare il contenuto, modificare il **filtro richieste** in Gestione IIS per ogni punto di distribuzione applicabile per consentire l'accesso alle estensioni di file e alle cartelle presenti nei pacchetti e nelle applicazioni distribuiti.  

> [!IMPORTANT]  
> Le modifiche al filtro richieste possono aumentare la superficie di attacco del computer.  
> 
> - Le modifiche apportate a livello di server si applicano a tutti i siti Web nel server.   
>     - Le modifiche ai singoli siti Web si applicano solo al sito Web specificato.  
> 
> La procedura di sicurezza consigliata è l'esecuzione di Configuration Manager in un server Web dedicato. Se è necessario eseguire altre applicazioni nel server Web, usare un sito Web personalizzato per Configuration Manager. Per informazioni, vedere [Siti Web per i server del sistema del sito](websites-for-site-system-servers.md).  

## <a name="http-verbs"></a>Verbi HTTP
**Punti di gestione:** per assicurarsi che i client possano comunicare correttamente con un punto di gestione, verificare che i verbi HTTP seguenti siano consentiti nel server del punto di gestione:  
- GET
- POST
- CCM_POST
- HEAD
- PROPFIND

**Punti di distribuzione:** i punti di distribuzione richiedono che i verbi HTTP seguenti siano consentiti:
- GET
- HEAD
- PROPFIND

Per altre informazioni, vedere [Configure request filtering in IIS](https://docs.microsoft.com/previous-versions/orphan-topics/ws.11/hh831621(v=ws.11)#http-verbs) (Configurare il filtro richieste in IIS). 
