---
title: Percorso di origine del contenuto
titleSuffix: Configuration Manager
description: Informazioni sulle impostazioni di Configuration Manager che consentono ai client di individuare contenuto in una rete lenta.
ms.date: 01/3/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 70b5cbc0-64ba-49bd-8b34-fb4c09b2b95b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 9d58138380263a7e7c3305ab2ad663a5246098b4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703659"
---
# <a name="content-source-location-scenarios-in-configuration-manager"></a>Scenari del percorso di origine del contenuto in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Nelle versioni precedenti alla versione 1610, Configuration Manager supportava diverse impostazioni che era possibile combinare per definire come e dove i client potessero trovare contenuto in caso di connessione a una rete lenta. Le combinazioni possibili influiscono sui percorsi del contenuto usati dai client e sulla possibilità di usare correttamente un percorso di fallback quando l'origine preferita del contenuto non è disponibile.  

> [!IMPORTANT]  
> **Se i siti eseguono la versione 1511, 1602 o 1606**, le informazioni contenute in questo argomento sono valide per l'infrastruttura in uso. Vedere anche [Gruppi di limiti per System Center Configuration Manager versioni 1511, 1602 e 1606](../../servers/deploy/configure/boundary-groups-for-1511-1602-and-1606.md) per informazioni specifiche per i gruppi di limiti con queste versioni di Configuration Manager.
>
> **Se i siti eseguono la versione 1610 o versioni successive**, usare le informazioni contenute in [Definire i limiti del sito e i gruppi di limiti per Configuration Manager](../../servers/deploy/configure/define-site-boundaries-and-boundary-groups.md) per comprendere in che modo i client individuano i punti di distribuzione con contenuto disponibile.





**Le tre impostazioni seguenti definiscono il comportamento quando i client richiedono contenuti:**

- **Consenti percorso origine di fallback per il contenuto** (opzione abilitata o non abilitata): questa opzione può essere abilitata nella scheda **Gruppi limite** di un punto di distribuzione. L'opzione consente al client di usare un punto di distribuzione configurato come percorso di fallback quando non è disponibile contenuto in un punto di distribuzione preferito.  

  - **Comportamento di distribuzione per la velocità di connessione di rete**: ogni distribuzione è configurata con uno dei comportamenti seguenti da usare quando la connessione al punto di distribuzione è lenta:  

    -   **Scarica il contenuto dal punto di distribuzione ed esegui in locale**  

    -   **Non scaricare il contenuto**: questa opzione viene usata solo quando un client usa un percorso di fallback per ottenere il contenuto.  

    La velocità di connessione per un punto di distribuzione è configurata nella scheda **Riferimenti** di un gruppo di limiti ed è specifica per tale gruppo.  

  - **Distribuzione di pacchetti su richiesta** (nei punti di distribuzione preferiti): questa opzione viene abilitata quando si seleziona l'opzione **Distribuisci il contenuto del pacchetto nei punti di distribuzione preferiti** nella scheda **Impostazioni distribuzione** delle proprietà delle applicazioni o di un pacchetto. Quando è abilitata, questa opzione fa in modo che Configuration Manager copi automaticamente il contenuto in un punto di distribuzione preferito in cui ancora non è presente dopo che un client richiede tale contenuto da tale punto di distribuzione.  


 **I requisiti seguenti si applicano a tutti gli scenari:**


-   Il contenuto è disponibile in un punto di distribuzione di fallback  

-   I punti di distribuzione sono online e accessibili  


## <a name="scenario-1"></a>Scenario 1  
 Si applica in presenza delle configurazioni seguenti:  

-   **Il contenuto è disponibile in un punto di distribuzione preferito**  

-   **Consenti fallback**: Non abilitato  

-   **Comportamento di distribuzione per rete lenta**: Qualsiasi configurazione  


**Dettagli:** la configurazione per la distribuzione di pacchetti su richiesta non è pertinente in questo scenario.  

1.  Il client invia una richiesta di contenuto al punto di gestione.  

2.  Al client viene restituito un elenco di percorsi del contenuto dal punto di gestione con i punti di distribuzione preferiti con contenuto.  

3.  Il client scarica il contenuto da un punto di distribuzione preferito nell'elenco.  

## <a name="scenario-2"></a>Scenario 2  
 In presenza delle configurazioni seguenti:  

-   **Il contenuto è disponibile in un punto di distribuzione preferito**  

-   **Consenti fallback**: Abilitato  

-   **Comportamento di distribuzione per rete lenta**: Non scaricare il contenuto  


**Dettagli:** la configurazione per la distribuzione di pacchetti su richiesta non è pertinente in questo scenario.  

1.  Il client invia una richiesta di contenuto al punto di gestione. Il client include un flag con la richiesta che indica che i punti di distribuzione di fallback sono consentiti.  

2.  Al client viene restituito un elenco di percorsi del contenuto dal punto di gestione con i punti di distribuzione preferiti e i punti di distribuzione di fallback con contenuto.  

3.  Il client scarica il contenuto da un punto di distribuzione preferito nell'elenco.  

## <a name="scenario-3"></a>Scenario 3  
 In presenza delle configurazioni seguenti:  

-   **Il contenuto è disponibile in un punto di distribuzione preferito**  

-   **Consenti fallback**: Abilitato  

-   **Comportamento di distribuzione per rete lenta**: Scaricare e installare il contenuto  


**Dettagli:** la configurazione per la distribuzione di pacchetti su richiesta non è pertinente in questo scenario.  

1.  Il client invia una richiesta di contenuto al punto di gestione. Il client include un flag con la richiesta che indica che i punti di distribuzione di fallback sono consentiti.  

2.  Al client viene restituito un elenco di percorsi del contenuto dal punto di gestione con i punti di distribuzione preferiti e i punti di distribuzione di fallback con contenuto.  

3.  Il client scarica il contenuto da un punto di distribuzione preferito nell'elenco.  

## <a name="scenario-4"></a>Scenario 4  
 In presenza delle configurazioni seguenti:  

-   **Il contenuto non è disponibile in un punto di distribuzione preferito**  

-   **Distribuisci il contenuto del pacchetto nei punti di distribuzione preferiti**: opzione non abilitata  

-   **Consenti fallback**: Non abilitato  

-   **Comportamento di distribuzione per rete lenta**: Qualsiasi configurazione  


**Dettagli:**  

1.  Il client invia una richiesta di contenuto al punto di gestione.  

2.  Al client viene restituito un elenco di percorsi del contenuto dal punto di gestione con i punti di distribuzione preferiti con contenuto. Nell'elenco non sono disponibili punti di distribuzione preferiti.  

3.  Il client genera il messaggio di errore **Contenuto non disponibile** e passa in modalità Riprova. Ogni ora viene avviata una nuova richiesta di contenuto.  

## <a name="scenario-5"></a>Scenario 5  
 In presenza delle configurazioni seguenti:  

-   **Il contenuto non è disponibile in un punto di distribuzione preferito**  

-   **Distribuisci il contenuto del pacchetto nei punti di distribuzione preferiti**: opzione non abilitata  

-   **Consenti fallback**: Abilitato  

-   **Comportamento di distribuzione per rete lenta**: Non scaricare il contenuto  


**Dettagli:**  

1.  Il client invia una richiesta di contenuto al punto di gestione. Il client include un flag con la richiesta che indica che i punti di distribuzione di fallback sono consentiti.  

2.  Al client viene restituito un elenco di percorsi del contenuto dal punto di gestione con i punti di distribuzione preferiti e i punti di distribuzione di fallback con contenuto. Non esistono punti di distribuzione preferiti con contenuto, ma esiste almeno un punto di distribuzione di fallback con contenuto.  

3.  Il contenuto non viene scaricato perché la proprietà di distribuzione per quando il client usa un punto di distribuzione di fallback è impostata su **Non scaricare il contenuto** (opzione usata quando i client eseguono il fallback per ottenere il contenuto). Il client genera il messaggio di errore **Contenuto non disponibile** e passa in modalità Riprova. Il client effettua una nuova richiesta di contenuto ogni ora.  

## <a name="scenario-6"></a>Scenario 6  
 In presenza delle configurazioni seguenti:  

-   **Il contenuto non è disponibile in un punto di distribuzione preferito**  

-   **Distribuisci il contenuto del pacchetto nei punti di distribuzione preferiti**: opzione non abilitata  

-   **Consenti fallback**: Abilitato  

-   **Comportamento di distribuzione per rete lenta**: Scaricare e installare il contenuto  


**Dettagli:**  

1.  Il client invia una richiesta di contenuto al punto di gestione. Il client include un flag con la richiesta che indica che i punti di distribuzione di fallback sono abilitati.  

2.  Al client viene restituito un elenco di percorsi del contenuto dal punto di gestione con i punti di distribuzione preferiti e i punti di distribuzione di fallback con contenuto. Non esistono punti di distribuzione preferiti con contenuto, ma almeno un punto di distribuzione di fallback con contenuto.  

3.  Il contenuto viene scaricato da un punto di distribuzione di fallback nell'elenco perché la proprietà di distribuzione per quando il client usa un punto di distribuzione di fallback è impostata su **Scarica e installa il contenuto**.  

## <a name="scenario-7"></a>Scenario 7  
 In presenza delle configurazioni seguenti:  

-   **Il contenuto non è disponibile in un punto di distribuzione preferito**  

-   **Distribuisci il contenuto del pacchetto nei punti di distribuzione preferiti**: opzione abilitata  

-   **Consenti fallback**: Non abilitato  

-   **Comportamento di distribuzione per rete lenta**: Qualsiasi configurazione  


**Dettagli:**  

1.  Il client invia una richiesta di contenuto al punto di gestione.  

2.  Al client viene restituito un elenco di percorsi del contenuto dal punto di gestione con i punti di distribuzione preferiti con contenuto. Non esistono punti di distribuzione preferiti con contenuto.  

3.  Il client genera il messaggio di errore **Contenuto non disponibile** e passa in modalità Riprova. Ogni ora viene effettuata una nuova richiesta di contenuto.  

4.  Il punto di gestione crea un trigger per Distribution Manager per distribuire il contenuto in tutti i punti di distribuzione preferiti per il client che ha effettuato la richiesta di contenuto.  

5.  Distribution Manager distribuisce il contenuto in tutti i punti di distribuzione preferiti. Nella maggior parte dei casi il contenuto viene distribuito correttamente nei punti di distribuzione preferiti entro un'ora.  

6.  Una nuova richiesta di contenuto viene avviata dal client al punto di gestione.  

7.  Al client viene restituito un elenco di percorsi del contenuto dal punto di gestione con i punti di distribuzione preferiti con contenuto. Il client scarica il contenuto da un punto di distribuzione preferito nell'elenco.  

## <a name="scenario-8"></a>Scenario 8  
 In presenza delle configurazioni seguenti:  

-   **Il contenuto non è disponibile in un punto di distribuzione preferito**  

-   **Distribuisci il contenuto del pacchetto nei punti di distribuzione preferiti**: opzione abilitata  

-   **Consenti fallback**: Abilitato  

-   **Comportamento di distribuzione per rete lenta**: Non scaricare il contenuto  


**Dettagli:**  

1.  Il client invia una richiesta di contenuto al punto di gestione. Il client include un flag con la richiesta che indica che i punti di distribuzione di fallback sono consentiti.  

2.  Al client viene restituito un elenco di percorsi del contenuto dal punto di gestione con i punti di distribuzione preferiti e i punti di distribuzione di fallback con contenuto. Non esistono punti di distribuzione preferiti con contenuto, ma esiste almeno un punto di distribuzione di fallback con contenuto.  

3.  Il contenuto non viene scaricato perché la proprietà di distribuzione per quando il client usa un punto di distribuzione di fallback è impostata su **Non scaricare**. Il client genera il messaggio di errore **Contenuto non disponibile** e passa in modalità Riprova. Il client effettua una nuova richiesta di contenuto ogni ora.  

4.  Il punto di gestione crea un trigger per Distribution Manager per distribuire il contenuto in tutti i punti di distribuzione preferiti per il client che ha effettuato la richiesta di contenuto.  

5.  Distribution Manager distribuisce il contenuto in tutti i punti di distribuzione preferiti. Nella maggior parte dei casi il contenuto viene distribuito correttamente nei punti di distribuzione preferiti entro un'ora.  

6.  Una nuova richiesta di contenuto viene avviata dal client al punto di gestione.  

7.  Al client viene restituito un elenco di percorsi del contenuto dal punto di gestione con i punti di distribuzione preferiti con contenuto.  

8.  Il client scarica il contenuto da un punto di distribuzione preferito nell'elenco.  

## <a name="scenario-9"></a>Scenario 9  
 In presenza delle configurazioni seguenti:  

-   **Il contenuto non è disponibile in un punto di distribuzione preferito**  

-   **Distribuisci il contenuto del pacchetto nei punti di distribuzione preferiti**: opzione abilitata  

-   **Consenti fallback**: Abilitato  

-   **Comportamento di distribuzione per rete lenta**: Scaricare e installare il contenuto  


**Dettagli:**  

1.  Il client invia una richiesta di contenuto al punto di gestione. Il client include un flag con la richiesta che indica che i punti di distribuzione di fallback sono consentiti.  

2.  Al client viene restituito un elenco di percorsi del contenuto dal punto di gestione con i punti di distribuzione preferiti e i punti di distribuzione di fallback con contenuto. Non esistono punti di distribuzione preferiti con contenuto, ma esiste almeno un punto di distribuzione di fallback con contenuto.  

3.  Il contenuto viene scaricato da un punto di distribuzione di fallback nell'elenco perché la proprietà di distribuzione per quando il client usa un punto di distribuzione di fallback è impostata su **Scarica e installa il contenuto**. Questa impostazione di distribuzione consente a un client che deve usare un percorso dei contenuti di fallback di ottenere il contenuto da tale percorso.  

4.  Il punto di gestione crea un trigger per Distribution Manager per distribuire il contenuto in tutti i punti di distribuzione preferiti per il client che ha effettuato la richiesta di contenuto.  

5.  Distribution Manager distribuisce il contenuto in tutti i punti di distribuzione preferiti, consentendo ai client aggiuntivi di ottenere il contenuto senza usare un punto di distribuzione di fallback.  
