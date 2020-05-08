---
title: Informazioni di riferimento per l'installazione
titleSuffix: Configuration Manager
description: Esaminare le informazioni di riferimento seguenti che consentono di preparare l'installazione di un sito o di una gerarchia di Configuration Manager.
ms.date: 04/18/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cdb9fb0c-0912-41e4-b427-f40620971763
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ff2d5c6df0da6b25395858a55ef1ee8a3c0da00b
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906530"
---
# <a name="reference-for-configuration-manager-setup"></a>Informazioni di riferimento per l'installazione di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Il programma di installazione di Configuration Manager fa riferimento a diversi argomenti descritti in dettaglio nelle sezioni seguenti. Le informazioni presentate in questo argomento possono essere utili per preparare l'installazione di un sito o di una gerarchia di Configuration Manager e per prendere alcune delle decisioni necessarie durante l'installazione.  


##  <a name="before-you-begin"></a><a name="bkmk_start"></a> Prima di iniziare  
Prima di installare nuovi siti di Configuration Manager, verificare di avere esaminato le informazioni seguenti, utili per garantire una buona riuscita della distribuzione:  

-   [Nozioni fondamentali di Configuration Manager](../../../../core/understand/fundamentals.md)  
-   [Pianificare l'infrastruttura di Configuration Manage](../../../plan-design/network/configure-firewalls-ports-domains.md)r  
-   [Preparare l'installazione di siti di Configuration Manager](prepare-to-install-sites.md)  

##  <a name="assess-server-readiness"></a><a name="bkmk_assess"></a> Valutare la conformità dei server  
Prima di iniziare l'installazione di un nuovo sito, verificare che il server del sito e i server del sistema del sito remoti da usare per il sito (ad esempio il server che ospita il database del sito) soddisfino tutte le configurazioni dei prerequisiti. Possono essere utili gli argomenti seguenti della raccolta di documentazione:  

-   [Configurazioni supportate per Configuration Manager](../../../../core/plan-design/configs/supported-configurations.md)  
-   [Controllo prerequisiti](prerequisite-checker.md)  

##  <a name="clients-for-additional-operating-systems"></a><a name="bkmk_Addclients"></a> Client per altri sistemi operativi  
È possibile scaricare il software client per Configuration Manager dall'Area download Microsoft per i sistemi operativi seguenti:  

- macOS (Apple)
- UNIX
- Linux

Per scaricare i client per la versione di Configuration Manager in uso, usare i collegamenti seguenti:  

- [Microsoft Endpoint Configuration Manager - macOS Client (64-bit)](https://www.microsoft.com/download/details.aspx?id=100850)

- [Microsoft Configuration Manager - Client per altri sistemi operativi](https://www.microsoft.com/download/details.aspx?id=47719)

##  <a name="usage-data-levels-and-settings"></a><a name="bkmk_usage"></a> Impostazioni e livelli per i dati di utilizzo  
Quando si installa il primo sito di Configuration Manager, nel server del sito viene installato e configurato automaticamente un nuovo ruolo del sistema del sito, ovvero il **punto di connessione del servizio**, con le impostazioni predefinite seguenti:  

-   Modalità **Online** (è disponibile anche una modalità offline)  
-   Livello di raccolta dati **Avanzato** (sono disponibili altri due livelli di raccolta dati, Base e Completo)  

Quando è online, il ruolo del sistema del sito del punto di connessione del servizio consente a Microsoft di raccogliere automaticamente informazioni di utilizzo e di diagnostica in Internet. Le informazioni raccolte sono utili per:  

-   Identificare e risolvere i problemi  
-   Migliorare i prodotti e il servizio  
-   Identificare gli aggiornamenti per Configuration Manager applicabili alla versione in uso  

### <a name="levels-of-data-collection"></a>Livelli di raccolta dati  
La raccolta dati è articolata nei tre livelli seguenti:

-   **Base**: include i dati su installazione e aggiornamento, come il numero di siti e le funzionalità di Configuration Manager abilitate. Non vengono trasmesse informazioni personali.  

-   **Avanzato**: include i dati contenuti nell'impostazione del livello Base e trasmette dati sulla gerarchia, informazioni sulla modalità di utilizzo delle singole funzionalità, ad esempio frequenza e durata, e informazioni di diagnostica avanzata, come lo stato della memoria del server quando si verifica un arresto anomalo di un sistema o un'app. Non vengono trasmessi dati riservati.  

-   **Completo**: include i dati contenuti nelle impostazioni dei livelli Base e Avanzato e invia anche informazioni di diagnostica avanzate, ad esempio file di sistema e snapshot di memoria. Questa opzione può includere informazioni personali, che tuttavia non verranno usate per identificare o contattare l'utente o a fini pubblicitari.  

Per altre informazioni, tra cui la divulgazione dei dettagli raccolti da ogni livello, vedere [Dati di diagnostica e utilizzo per Configuration Manager](../../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md).  

Per altre informazioni, vedere l'[Informativa sulla privacy Microsoft](https://privacy.microsoft.com/privacystatement).
