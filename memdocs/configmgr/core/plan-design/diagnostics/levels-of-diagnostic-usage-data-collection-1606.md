---
title: Dati di diagnostica per la versione 1606
titleSuffix: Configuration Manager
description: Informazioni sui livelli dei dati di diagnostica e di utilizzo raccolti da Configuration Manager versione 1606.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f7350d03-f440-4744-82d4-75f8c6c25028
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: cd58fb2ad105d3fb94fcc1d2fe56f0ae64f766f1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697069"
---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1606-of-configuration-manager"></a>Livelli di raccolta di dati per utilizzo diagnostico per la versione 1606 di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Configuration Manager versione 1606 raccoglie tre livelli di dati di diagnostica e utilizzo: **Di base**, **Avanzato** e **Completo**. Per impostazione predefinita, per questa funzionalità è impostato il livello avanzato. Le sezioni seguenti forniscono ulteriori dettagli sui dati raccolti in ogni livello.

Le modifiche rispetto alle versioni precedenti sono contrassegnate da ***[Nuovo]***, ***[Aggiornato]***, ***[Rimosso]*** o ***[Spostato]***.


> [!IMPORTANT]
>  Configuration Manager non raccoglie codici del sito, nomi di siti, indirizzi IP, nomi utente, nomi di computer, indirizzi fisici o indirizzi di posta elettronica per i livelli di base e avanzato. L'eventuale raccolta di tali informazioni per il livello completo non è intenzionale, ovvero dati potenzialmente inclusi nelle informazioni di diagnostica avanzate come file di log o snapshot di memoria. Le informazioni eventualmente raccolte non verranno usate da Microsoft per identificare l'utente, contattare l'utente o per fini pubblicitari.

##  <a name="how-to-change-the-level"></a><a name="bkmk_change"></a> Come cambiare il livello
 Gli amministratori con ambito amministrativo basato sui ruoli che include le autorizzazioni **Modifica** per la classe di oggetti **Sito** possono modificare il livello dei dati raccolti nelle impostazioni Dati di diagnostica e di utilizzo nella console di Configuration Manager.

   A tale scopo, nella console passare alla scheda Backstage (la scheda in alto a sinistra con la freccia a discesa), selezionare **Dati di utilizzo** e quindi selezionare il livello di dati che si vuole usare.  

##  <a name="level-1---basic"></a><a name="bkmk_level1"></a> Livello 1 - Di base
 Il livello di base include i dati sulla gerarchia ed è necessario per consentire il miglioramento dell'esperienza di installazione o aggiornamento, nonché per determinare quali aggiornamenti di Configuration Manager sono applicabili per la gerarchia.

 Per Configuration Manager versione 1606, questo livello include i dati seguenti:


-   Informazioni sull'installazione:
      - Build, tipo di installazione, Language Pack, funzionalità abilitate  

      -   Stato di distribuzione ed errori del pacchetto di aggiornamento, stato del download ed errori dei prerequisiti 

      -  Versione dello script post-aggiornamento

      -  Uso di Fast Ring di aggiornamento

-   Metriche delle prestazioni del database (informazioni sull'elaborazione della replica, principali stored procedure di SQL Server per processore e utilizzo del disco)

-   Configurazione di base dei database (processori, configurazione del cluster e configurazione delle viste distribuite)

-   Schema del database di Configuration Manager (hash di tutte le definizioni di oggetti)

-   Numero delle versioni client di Configuration Manager e delle versioni del sistema operativo

-   Numero dei sistemi operativi per i dispositivi gestiti e dei criteri impostati da Exchange Connector

-   Numero delle lingue e delle impostazioni locali dei client

-   Numero dei dispositivi Windows 10 per ramo e build

-   Dati di base sulla gerarchia dei siti di Configuration Manager (elenco dei siti, tipo, versione, stato, numero di client e fuso orario)

-   Informazioni di base sul server del sistema del sito (ruoli del sistema del sito usati, stato di Internet e SSL, sistema operativo, processori, computer fisico o macchina virtuale)

-   Statistiche di base di individuazione degli utenti (numero di individuazioni di utenti e dimensioni minime/massime/medie dei gruppi)

-   Informazioni di base su Endpoint Protection (versioni client antimalware)

-   Conteggi di base per applicazioni e tipi di distribuzione (totale app, totale app con più tipi di distribuzione, totale app con dipendenze, totale app sostituite e numero delle tecnologie di distribuzione in uso)

-   Numero di distribuzioni del sistema operativo di base (immagini)

-   Tipi di punto di distribuzione e di punto di gestione e informazioni di base sulla configurazione (protetto, pre-installato, PXE, multicast, stato di SSL, punti di distribuzione pull/peer, abilitato per MDM, abilitato per SSL e così via)

-   Statistiche di telemetria (data/ora di esecuzione, runtime ed errori)

-  Livello di telemetria configurato, modalità online o offline e configurazione di aggiornamento rapido

-  Uso di Network Discovery (abilitato o disabilitato)
-  Admin Console:

    -  Statistiche sulle connessioni della console (versione del sistema operativo, lingua, SKU e architettura, memoria di sistema, conteggio dei processori logici, ID del sito di connessione, versioni di .NET installate e Language Pack della console)    


- ***[Nuovo]*** Versione SQL, livello Service Pack, edizione, ID delle regole di confronto e set di caratteri


##  <a name="level-2---enhanced"></a><a name="bkmk_level2"></a> Livello 2 - Avanzato
Il livello avanzato è quello predefinito dopo l'installazione. Questo livello include i dati raccolti per il livello di base, oltre a dati specifici per le funzionalità (frequenza e durata d'uso), le impostazioni client di Configuration Manager (nome del componente, stato e alcune impostazioni come gli intervalli di polling) e le informazioni di base sugli aggiornamenti software.

Questo livello è consigliato perché offre a Microsoft i dati minimi necessari per apportare miglioramenti utili nelle versioni future di prodotti e servizi. Con questo livello non vengono raccolti i nomi degli oggetti (siti, utenti, computer o oggetti), dettagli sugli oggetti correlati alla sicurezza o informazioni sulle vulnerabilità come il numero di sistemi che richiedono aggiornamenti software.

Per Configuration Manager versione 1606, questo livello include i dati seguenti:

-   **Gestione delle applicazioni:**  

    -    Informazioni di base su utilizzo/destinazione per i tipi di distribuzione usati all'interno dell'organizzazione (utente e dispositivo di destinazione, richiesto o disponibile e app universali)  

    -   Informazioni sulla distribuzione delle applicazioni (installazione/disinstallazione, approvazione richiesta, interazione con l'utente abilitata o disabilitata, dipendenza e sostituzione)  

    -   Dati statistici sulle richieste di applicazioni disponibili  

    -   Numero di pacchetti per tipo  

    -   Numero di applicabilità delle applicazioni per sistema operativo  

    -   Numero di distribuzioni di pacchetti/programmi  

    -   Numero di ambienti e proprietà di distribuzione App-V  

    -   Numero di licenze per applicazioni con licenza Windows 10  

    -   Numero massimo/minimo/medio di distribuzioni di applicazioni per ogni utente o dispositivo per periodo

    -   Tipo e durata della finestra di manutenzione  

    -  Dimensioni criteri di applicazione e statistiche di complessità

    - ***[Nuovo]*** Conteggio delle app di Windows Store per le aziende e statistiche di sincronizzazione (incluso il riepilogo dei tipi di app)  

    - ***[Nuovo]*** Statistiche dei gruppi di limiti (numero di rapidi e lenti e conteggio per gruppo)

    - ***[Nuovo]*** Opzioni di configurazione MSI e conteggi

    - ***[Nuovo]*** Requisiti delle app (conteggio delle condizioni predefinite con riferimento per tecnologia di distribuzione)

    - ***[Nuovo]*** Sostituzione delle app, profondità massima della catena

    - ***[Nuovo]*** Uso e modalità di creazione di UDA (Universal Data Access)



-   **Client:**  

    -   Elenco/numero di agenti client abilitati  

    -   Numero di installazioni client da ogni tipo di posizione di origine  

    -   Numero di errori di installazioni client  

    -  ***[Nuovo]*** Configurazione della distribuzione degli aggiornamenti automatici dei client, incluso progetto pilota client

    -  ***[Nuovo]*** Statistiche dell'integrità dei client e riepilogo delle richieste principali

    - ***[Nuovo]*** Età del BIOS in anni

    - ***[Nuovo]*** Età del sistema operativo in mesi

    - ***[Nuovo]*** Conteggio delle azioni di Software Center

    - ***[Nuovo]*** Versione del client AMT (Active Management Technology)

    - ***[Nuovo]*** Errori di download della distribuzione client

    - ***[Nuovo]*** Stato dell'azione operazione di notifica client: numero di esecuzioni di ogni azione, numero massimo di client assegnati e frequenza media esecuzioni senza errori

    - ***[Nuovo]*** Metodi di distribuzione usati per il client e numero di client per metodo di distribuzione

    - ***[Nuovo]*** Configurazione della dimensione della cache del client



- ***[Nuovo]*** **Servizi cloud:**

  - ***[Nuovo]*** Numero di raccolte sincronizzate con Operations Management Suite

  - ***[Nuovo]*** Stato di abilitazione del connettore cloud di Operations Management Suite



- ***[Nuovo] Raccolte:***

    -  ***[Spostato]*** Statistiche di valutazione raccolte (durata query, conteggi assegnati e non assegnati, conteggi per tipo, rollover degli ID e uso delle regole)

    - ***[Nuovo]*** Raccolte senza distribuzione

    - ***[Nuovo]*** Utilizzo ID raccolte (senza esaurimento degli ID)



-   **Impostazioni di conformità:**  

    -   Numero di elementi di configurazione per tipo  

    -   Informazioni di base sulla linea di base di configurazione (numero, numero di distribuzioni e numero di riferimenti)  

    -   ***[Aggiornato]*** Numero di distribuzioni che fanno riferimento a impostazioni predefinite (ora con acquisizione dell'impostazione di correzione)  

    -   ***[Aggiornato]*** Conteggio delle regole e delle distribuzioni create per le impostazioni personalizzate (ora con acquisizione dell'impostazione di correzione)  
    -   Numero di certificati SCEP (Simple Certificate Enrollment Protocol), VPN, Wi-Fi, certificati (.pfx) e modelli dei criteri di conformità distribuiti

    -  Numero di certificati SCEP, VPN, Wi-Fi, certificati (.pfx) e distribuzioni dei criteri di conformità per piattaforma

    - ***[Nuovo]*** Criteri di Passport for Work (creati, distribuiti)



-   **Contenuto:**  

    -   Numero di limiti per tipo  

    -   Informazioni sui gruppi di limiti (numero di limiti e di sistemi del sito assegnati a ogni gruppo di limiti)  

    -   Informazioni sui gruppi di punti di distribuzione (numero di pacchetti e punti di distribuzione assegnati a ogni gruppo di punti di distribuzione)  

    -   Informazioni di configurazione sui punti di distribuzione (uso di BranchCache e monitoraggio dei punti di distribuzione)  

    -   Informazioni di configurazione di Distribution Manager (thread, intervallo tra tentativi, numero di tentativi e impostazioni dei punti di distribuzione pull)  


-   **Endpoint Protection:**  

    -   Utilizzo dei criteri antimalware di Endpoint Protection e di Windows Firewall (numero di criteri univoci assegnati al gruppo)<br /><br /> Non sono incluse informazioni sulle impostazioni contenute nei criteri.  

    -   Errori di distribuzione di Endpoint Protection (numero di codici di errore di distribuzione dei criteri di Endpoint Protection)  

    -   Numero di raccolte selezionate per la visualizzazione nel dashboard di Endpoint Protection  

    -   Numero di avvisi configurati per la funzionalità Endpoint Protection  

    - ***[Nuovo]*** Criteri avanzati di Advanced Threat Protection (ATP) (numero dei criteri e se i criteri sono distribuiti)


-   ***[Rimosso]*** **Gestione di applicazioni mobili (MAM):**  

    -   ***[Rimosso]*** Numero di applicazioni di Office e line-of-business e di criteri abilitati per MAM per sistema operativo  

    -   ***[Rimosso]*** Numero di distribuzioni di applicazioni/criteri MAM  

    -   ***[Rimosso]*** Numero di regole create per ogni impostazione MAM  


- ***[Nuovo]*** **Migrazione:**

  -  ***[Nuovo]*** Numero di oggetti migrati (utilizzo della procedura guidata di migrazione)



-   **Gestione di dispositivi mobili (MDM):**  

    -   Numero di azioni eseguite su dispositivi mobili (comandi di blocco, reimpostazione PIN, cancellazione e ritiro dati)  

    -   Numero di dispositivi mobili gestiti da Configuration Manager e Microsoft Intune e modalità di registrazione (in blocco o basata sull'utente)  

    -   Pianificazione del polling dei dispositivi mobili e statistiche della durata della registrazione dei dispositivi mobili  

    -   Numero di criteri per dispositivi mobili  

    -   Numero di utenti con più dispositivi mobili registrati  

-   **Risoluzione dei problemi di Microsoft Intune:**

    -   Numero e dimensioni dei messaggi relativi a stato, inventario, RDR, DDR, UDX, stato tenant, POL, LOG, Cert, CRP, risincronizzazione, CFD, RDO, BEX, ISM e conformità scaricati da Microsoft Intune

    -   Numero e dimensioni dei messaggi relativi ad azioni sui dispositivi (cancellazione, ritiro dati, blocco), telemetria e dati replicati in Microsoft Intune

    -   Statistiche della sincronizzazione degli utenti completa e differenziale per Microsoft Intune


-   **Gestione di dispositivi mobili (MDM) in locale:**  

    -   Statistiche di esito positivo o negativo della distribuzione per distribuzioni di applicazioni MDM in locale  

    -   Numero dei pacchetti e dei profili di registrazione in blocco di Windows 10  



-   **Distribuzione del sistema operativo:**  

    -   Numero di immagini di avvio, driver, pacchetti di driver, punti di distribuzione abilitati per il multicast, punti di distribuzione che supportano PXE e sequenze di attività  

    -   ***[Nuovo]*** Conteggi dell'utilizzo della procedura della sequenza di attività



-   **Aggiornamenti del sito:**

    - Versioni degli hotfix di Configuraton Manager installati




-   **Aggiornamenti del software:**  

    -   Numero totale/medio di raccolte con distribuzioni di aggiornamento del software e numero massimo/medio di aggiornamenti distribuiti  

    -   Numero di regole di distribuzione automatica associate alla sincronizzazione  

    -   Numero di regole di distribuzione automatica che aggiungono aggiornamenti o ne creano di nuovi in un gruppo esistente  

    -   Valori differenziali di disponibilità e scadenza usati nelle regole di distribuzione automatica  

    -   Numero medio e massimo di assegnazioni per ogni aggiornamento  

    -   Numero di aggiornamenti creati e distribuiti con System Center Update Publisher  

    -   Numero di gruppi e assegnazioni di aggiornamento  

    -   Numero di pacchetti di aggiornamento e numero massimo/minimo/medio dei punti di distribuzione assegnati con pacchetti  

    -   Numero di gruppi di aggiornamento e numero minimo/massimo/medio di aggiornamenti per ogni gruppo  

    -   Numero di aggiornamenti e percentuale di aggiornamenti distribuiti, scaduti, sostituiti, scaricati e contenenti EULA  

    -   Codici di errore e numero di computer per l'analisi per l'aggiornamento  

    -   Pianificazioni di valutazione e analisi per l'aggiornamento dei client  

    -   Pianificazione della sincronizzazione dei punti di aggiornamento software  

    -   Numero di regole di distribuzione automatica con più distribuzioni  

    -   Configurazioni usate per i piani di manutenzione attivi di Windows 10  

    -   Versioni del contenuto del dashboard di Windows 10  

    -   Numero di client Windows 10 che usano Windows Update per le aziende  

    -   Statistiche relative all'applicazione di patch al cluster  

    -   Numero di aggiornamenti di Office 365 distribuiti  

    -   Classificazioni sincronizzate dal punto di aggiornamento software

    -   ***[Nuovo]*** Statistiche di bilanciamento del carico del punto di aggiornamento software



-   **Dati SQL/prestazioni:**  

    -   Numero delle tabelle di database più grandi  

    -   Informazioni sulla replica SQL Always-On  

    -  Periodo di memorizzazione del rilevamento modifiche di SQL

    - ***[Nuovo]*** Tipi di individuazione, abilitazione e pianificazione (completa, incrementale)

    - ***[Nuovo]*** Statistiche operative di individuazione (numero di oggetti trovati)

    - ***[Nuovo]*** Problemi di prestazioni del rilevamento modifiche di SQL, periodo di memorizzazione e stato di pulizia automatica



- ***[Nuovo]*** **Varie**

    - ***[Nuovo]*** Numero dei siti con riattivazione LAN (WOL)



##  <a name="level-3---full"></a><a name="bkmk_level3"></a> Livello 3 - Completo
Il livello completo include tutti i dati dei livelli di base e avanzato. Include inoltre informazioni aggiuntive su Endpoint Protection, le percentuali di conformità degli aggiornamenti e informazioni sugli aggiornamenti software. Questo livello può includere anche informazioni di diagnostica avanzate, come file di sistema e snapshot di memoria, che possono contenere informazioni personali presenti in memoria o nei file di log al momento dell'acquisizione.

Per Configuration Manager versione 1606, questo livello include i dati seguenti:

-   Statistiche di valutazione e aggiornamento delle raccolte

-   Riepilogo dell'integrità di Endpoint Protection (incluso il numero di client protetti, a rischio, sconosciuti e non supportati)

-   Configurazione dei criteri di Endpoint Protection

-   Informazioni sulla distribuzione degli aggiornamenti software (percentuale di distribuzioni assegnate con client o ora UTC, aggiornamento obbligatorio o facoltativo ed eliminazione del riavvio)

-   Conformità generale delle distribuzioni degli aggiornamenti software

-   Informazioni sulla pianificazione di valutazione delle regole di distribuzione automatiche

-   ***[Rimosso]*** Numero di client con criteri di Protezione accesso alla rete

-   Codici e numero di errori di distribuzione degli aggiornamenti software

-   Numero minimo/massimo/medio dei client inattivi nelle raccolte di distribuzioni di aggiornamenti software

-   Numero di gruppi con aggiornamenti software scaduti

-   Numero minimo/massimo/medio di aggiornamenti software per ogni gruppo

-   Percentuali di analisi dell'aggiornamento software con esito positivo

-   Numero minimo/massimo/medio di ore dall'ultima analisi di aggiornamenti software

-    Prodotti di aggiornamento software sincronizzati dal punto di aggiornamento software
-    Impostazioni di conformità: dettagli di configurazione SCEP, VPN, Wi-Fi e del modello dei criteri di conformità

-    Tipo di criteri di accesso condizionale EAS (blocco o quarantena) per i dispositivi gestiti da Intune

-   ***[Nuovo]*** Prime 50 CPU dell'ambiente

-   ***[Nuovo]*** Utilizzo del pacchetto di configurazione DCM per Configuration Manager

-   ***[Nuovo]*** Codice prodotto MSI (app comuni distribuite dai clienti)

-   ***[Nuovo]*** Riepilogo dell'integrità ATP

-   ***[Nuovo]*** Errori di installazione della distribuzione client dettagliati
