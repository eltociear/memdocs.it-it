---
title: Dati di diagnostica per la versione 1710 | Configuration Manager
titleSuffix: Configuration Manager
description: Informazioni sui livelli dei dati di diagnostica e di utilizzo raccolti da Configuration Manager versione 1710.
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8fce5391-8e75-4f99-813a-76f8842be5bc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: fcc3d2e34c9387e158b3b35cd104c9fc43136ace
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697039"
---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1710-of-configuration-manager"></a>Livelli di raccolta di dati per utilizzo diagnostico per la versione 1710 di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Configuration Manager versione 1710 raccoglie tre livelli di dati di diagnostica e utilizzo: **Di base**, **Avanzato** e **Completo**. Per impostazione predefinita, per questa funzionalità è impostato il livello avanzato. Le sezioni seguenti forniscono ulteriori dettagli sui dati raccolti in ogni livello.

Le modifiche rispetto alle versioni precedenti sono contrassegnate da ***[Nuovo]***, ***[Aggiornato]***, ***[Rimosso]*** o ***[Spostato]***.


> [!IMPORTANT]
>  Configuration Manager non raccoglie codici del sito, nomi di siti, indirizzi IP, nomi utente, nomi di computer, indirizzi fisici o indirizzi di posta elettronica per i livelli di base e avanzato. L'eventuale raccolta di tali informazioni per il livello completo non è intenzionale, ovvero dati potenzialmente inclusi nelle informazioni di diagnostica avanzate come file di log o snapshot di memoria. Le informazioni eventualmente raccolte non verranno usate da Microsoft per identificare l'utente, contattare l'utente o per fini pubblicitari.



##  <a name="how-to-change-the-level"></a><a name="bkmk_change"></a> Come cambiare il livello
 Gli amministratori con ambito amministrativo basato sui ruoli che include le autorizzazioni **Modifica** per la classe di oggetti **Sito** possono modificare il livello dei dati raccolti nelle impostazioni Dati di diagnostica e di utilizzo nella console di Configuration Manager.

È possibile modificare il livello di raccolta dati dall'interno della console, passando ad **Amministrazione** > **Panoramica** > **Configurazione del sito** > **Siti**. Aprire **Impostazioni gerarchia** e selezionare il livello di dati che si vuole usare.  



##  <a name="level-1---basic"></a><a name="bkmk_level1"></a> Livello 1 - Di base
Il livello di base include i dati sulla gerarchia ed è necessario per consentire il miglioramento dell'esperienza di installazione o aggiornamento, nonché per determinare quali aggiornamenti di Configuration Manager sono applicabili per la gerarchia.

Per Configuration Manager versione 1710, questo livello include quanto segue:

- Admin Console:
   - Statistiche sulle connessioni della console (versione del sistema operativo, lingua, SKU e architettura, memoria di sistema, conteggio dei processori logici, ID del sito di connessione, versioni di .NET installate e Language Pack della console)

- Conteggi di base per applicazioni e tipi di distribuzione (totale app, totale app con più tipi di distribuzione, totale app con dipendenze, totale app sostituite e numero delle tecnologie di distribuzione in uso)

- Dati di base sulla gerarchia dei siti di Configuration Manager (elenco dei siti, tipo, versione, stato, numero di client e fuso orario)

- Configurazione di base dei database (processori, configurazione del cluster e configurazione delle viste distribuite)

- Statistiche di individuazione di base (numero di individuazioni e dimensioni minime/massime/medie dei gruppi) anche quando il sito viene eseguito interamente con i servizi Azure Active Directory.

- Informazioni di base su Endpoint Protection (versioni client antimalware)

- Numero di distribuzioni del sistema operativo di base (immagini)

- Informazioni di base sul server del sistema del sito (ruoli del sistema del sito usati, stato di Internet e SSL, sistema operativo, processori, computer fisico o macchina virtuale e utilizzo della disponibilità elevata dei server del sito)

- Schema del database di Configuration Manager (hash di tutte le definizioni di oggetti)

- Livello di telemetria configurato, modalità online o offline e configurazione di aggiornamento rapido

- Numero delle lingue e delle impostazioni locali dei client

- ***[Aggiornato]*** Numero di versioni client di Configuration Manager, di versioni del sistema operativo e di versioni di Office

- Numero dei sistemi operativi per i dispositivi gestiti e dei criteri impostati da Exchange Connector

- Numero dei dispositivi Windows 10 per ramo e build

- Metriche delle prestazioni del database (informazioni sull'elaborazione della replica, principali stored procedure di SQL Server per processore e utilizzo del disco)

- Tipi di punto di distribuzione e di punto di gestione e informazioni di base sulla configurazione (protetto, pre-installato, PXE, multicast, stato di SSL, punti di distribuzione pull/peer, abilitato per MDM, abilitato per SSL e così via)

- Elenco di estensioni con hash per le pagine delle proprietà e le procedure guidate della console di amministrazione

- Informazioni sull'installazione:
     - Build, tipo di installazione, Language Pack, funzionalità abilitate   

     - Uso delle versioni non definitive, tipo di supporto di installazione, tipo Branch

     - Data di scadenza di Software Assurance      

     - Stato di distribuzione ed errori del pacchetto di aggiornamento, stato del download ed errori dei prerequisiti 

     - Uso di Fast Ring di aggiornamento

     - Versione dello script post-aggiornamento

- Versione SQL, livello Service Pack, edizione, ID delle regole di confronto e set di caratteri     
- Statistiche di telemetria (data/ora di esecuzione, runtime, errori)

- Uso di Network Discovery (abilitato o disabilitato)




##  <a name="level-2---enhanced"></a><a name="bkmk_level2"></a> Livello 2 - Avanzato
Il livello avanzato è quello predefinito dopo l'installazione. Questo livello include i dati raccolti per il livello di base e dati specifici per le funzionalità (frequenza e durata d'uso), le impostazioni client di Configuration Manager (nome del componente, stato e alcune impostazioni come gli intervalli di polling) e le informazioni di base sugli aggiornamenti software.

Questo livello è consigliato perché offre a Microsoft i dati minimi necessari per apportare miglioramenti utili nelle versioni future di prodotti e servizi. Con questo livello non vengono raccolti i nomi degli oggetti (siti, utenti, computer o oggetti), dettagli sugli oggetti correlati alla sicurezza o informazioni sulle vulnerabilità come il numero di sistemi che richiedono aggiornamenti software.

Per Configuration Manager versione 1710, questo livello include quanto segue:

- **Gestione delle applicazioni:**  

   - Requisiti delle app (conteggio delle condizioni predefinite con riferimento per tecnologia di distribuzione)

   - Sostituzione delle app, profondità massima della catena

   - Statistiche sull'approvazione delle applicazioni e frequenza di utilizzo

   - Statistiche sulle dimensioni del contenuto delle applicazioni

   - Informazioni sulla distribuzione delle applicazioni (uso dell'installazione rispetto alla disinstallazione, obbligatorietà dell'approvazione, abilitazione o disabilitazione dell'interazione con l'utente, dipendenza, sostituzione e numero di utilizzi della funzionalità relativa al comportamento dell'installazione)  

   - Dimensioni criteri di applicazione e statistiche di complessità

   - Dati statistici sulle richieste di applicazioni disponibili

   - Informazioni di configurazione di base per pacchetti e programmi (opzioni di distribuzione e flag di programma)

   - Informazioni di base su utilizzo/destinazione per i tipi di distribuzione usati all'interno dell'organizzazione (utente e dispositivo di destinazione, richiesto o disponibile e app universali)

   - Statistiche dei gruppi di limiti (numero di rapidi e lenti e conteggio per gruppo)

   - Numero di ambienti e proprietà di distribuzione App-V

   - Numero di applicabilità delle applicazioni per sistema operativo  

   - Numero di applicazioni a cui fa riferimento una sequenza di attività

   - Numero di personalizzazioni distinte per catalogo applicazioni

   - Numero di applicazioni di Office 365 create tramite il dashboard

   - Numero di pacchetti per tipo  

   - Numero di distribuzioni di pacchetti/programmi  

   - Numero di licenze per applicazioni con licenza Windows 10  

   - Numero di tipi di distribuzione di Windows Installer in base alle impostazioni di disinstallazione del contenuto

   - Numero di app di Microsoft Store per le aziende e statistiche di sincronizzazione, inclusi il riepilogo dei tipi di app, lo stato delle app con licenza e il numero di app con licenza online e offline  

   - Tipo e durata della finestra di manutenzione  

   - Numero massimo/minimo/medio di distribuzioni di applicazioni per ogni utente o dispositivo per periodo

   - Codici di errore di installazione delle applicazioni più comuni per tecnologia di distribuzione

   - Opzioni di configurazione MSI e conteggi

   - Statistiche sull'interazione degli utenti finali con notifica per le distribuzioni software obbligatorie   

   - Utilizzo di UDA (Universal Data Access), modalità di creazione




- **Client:**  

   - Versione del client AMT (Active Management Technology)

   - Età del BIOS in anni

   - Numero di dispositivi con avvio protetto abilitato

   - Numero di dispositivi in base allo stato TPM

   - Aggiornamento automatico del client: configurazione della distribuzione inclusi la distribuzione pilota del client e l'utilizzo di esclusioni (client a interoperabilità estesa)

   - Configurazione della dimensione della cache del client

   - Errori di download della distribuzione client

   - Statistiche dell'integrità dei client e riepilogo dei problemi principali

   - Stato dell'azione operazione di notifica client: numero di esecuzioni di ogni azione, numero massimo di client assegnati e frequenza media esecuzioni senza errori
   - Numero di installazioni client da ogni tipo di posizione di origine  

   - Numero di errori di installazioni client  

   - Numero di dispositivi virtualizzati tramite Hyper-V o Azure  

   - Conteggio delle azioni di Software Center   

   - Numero di dispositivi abilitati per UEFI

   - Metodi di distribuzione usati per il client e numero di client per metodo di distribuzione

   - Elenco/numero di agenti client abilitati  

   - Età del sistema operativo in mesi

   - Numero di classi di inventario hardware, regole dell'inventario software e regole di raccolta dei file

   - Statistiche per l'attestazione dell'integrità del dispositivo, inclusi i codici di errore più comuni, il numero di server locali e il numero di dispositivi nei vari stati.



- **Servizi cloud:**

  - Statistiche di individuazione di Azure Active Directory

  - Statistiche di configurazione e utilizzo di Cloud Management Gateway, inclusi il numero delle aree e degli ambienti e le statistiche di autenticazione e autorizzazione

  - Numero di applicazioni e di servizi di Azure Active Directory connessi a Configuration Manager

  - Numero di client aggiunti ai servizi Azure Active Directory

  - Numero di raccolte sincronizzate con Azure Log Analytics

  - Numero di connettori di analisi degli aggiornamenti

  - Indica se il connettore cloud Azure Log Analytics è abilitato


- ***[Nuovo]***  Co-gestione
  - ***[Nuovo]***  Statistiche di utilizzo aggregate relative alla co-gestione, incluso il numero di client registrati, client che ricevono criteri, stati dei carichi di lavoro, dimensioni delle raccolte di esclusioni/pilota ed errori di registrazione
  - ***[Nuovo]***  Numero dei client in base al metodo di registrazione di co-gestione
  - ***[Nuovo]***  Statistiche degli errori per la registrazione di co-gestione
  - ***[Nuovo]*** Statistiche cronologiche e pianificazione della registrazione
  - ***[Nuovo]***  Numero dei client idonei per la co-gestione
  - ***[Nuovo]***  Tenant di Intune associato


- **Raccolte:**

    - Uso ID raccolte (senza esaurimento degli ID)

    - Statistiche di valutazione raccolte (durata query, conteggi assegnati e non assegnati, conteggi per tipo, rollover degli ID e utilizzo delle regole)

    - Raccolte senza distribuzione




- **Impostazioni di conformità:**  

    - Informazioni di base sulla linea di base di configurazione (numero, numero di distribuzioni e numero di riferimenti)

    - Statistiche degli errori relativi ai criteri di conformità

    - Numero di elementi di configurazione per tipo  

    - Numero di distribuzioni che fanno riferimento a impostazioni predefinite (ora con acquisizione dell'impostazione di correzione)  

    - Numero di regole e di distribuzioni create per le impostazioni personalizzate (ora con acquisizione dell'impostazione di correzione)  

    - Numero di certificati SCEP (Simple Certificate Enrollment Protocol), VPN, Wi-Fi, certificati (.pfx) e modelli dei criteri di conformità distribuiti

    - Numero di certificati SCEP, VPN, Wi-Fi, certificati (.pfx) e distribuzioni dei criteri di conformità per piattaforma

    - Criteri di Passport for Work (creati, distribuiti)



- **Contenuto:**  

    - Informazioni sui gruppi di limiti (numero di limiti e di sistemi del sito assegnati a ogni gruppo di limiti)  

    - Relazioni di gruppi di limiti e configurazione del fallback

    - Statistiche di download dei contenuti client

    - Numero di limiti per tipo  

    - Numero di client peer cache, statistiche di utilizzo e statistiche di download parziale

    - Informazioni di configurazione di Distribution Manager (thread, intervallo tra tentativi, numero di tentativi e impostazioni dei punti di distribuzione pull)  

    - Informazioni di configurazione sui punti di distribuzione (uso di BranchCache e monitoraggio dei punti di distribuzione)

    - Informazioni sui gruppi di punti di distribuzione (numero di pacchetti e punti di distribuzione assegnati a ogni gruppo di punti di distribuzione)  



- **Endpoint Protection:**  

   - Criteri avanzati di Advanced Threat Protection (ATP) (numero dei criteri e se i criteri sono distribuiti)

   - Numero di avvisi configurati per la funzionalità Endpoint Protection  

   - Numero di raccolte selezionate per la visualizzazione nel dashboard di Endpoint Protection  

   - ***[Nuovo]*** Numero di criteri di Windows Defender Exploit Guard, distribuzioni e client di destinazione

   - Errori di distribuzione di Endpoint Protection (numero di codici di errore di distribuzione dei criteri di Endpoint Protection)  

   - Utilizzo dei criteri antimalware di Endpoint Protection e di Windows Firewall (numero di criteri univoci assegnati al gruppo)<br /><br /> Non sono incluse informazioni sulle impostazioni contenute nei criteri.  



- **Migrazione:**

  - Numero di oggetti migrati (uso della procedura guidata di migrazione)



- **Gestione di dispositivi mobili (MDM):**  

    - Numero di azioni eseguite su dispositivi mobili: comandi di blocco, reimpostazione PIN, cancellazione, ritiro e sincronizzazione immediata

    - Numero di criteri per dispositivi mobili  

    - Numero di dispositivi mobili gestiti da Configuration Manager e Microsoft Intune e modalità di registrazione (in blocco o basata sull'utente)  

    - Numero di utenti con più dispositivi mobili registrati  

    - Pianificazione del polling dei dispositivi mobili e statistiche della durata della registrazione dei dispositivi mobili  




- **Risoluzione dei problemi di Microsoft Intune:**

    - Numero e dimensioni dei messaggi relativi ad azioni sui dispositivi (cancellazione, ritiro dati, blocco), telemetria e dati replicati in Microsoft Intune

    - Numero e dimensioni dei messaggi relativi a stato, inventario, RDR, DDR, UDX, stato tenant, POL, LOG, Cert, CRP, risincronizzazione, CFD, RDO, BEX, ISM e conformità scaricati da Microsoft Intune

    - Statistiche della sincronizzazione degli utenti completa e differenziale per Microsoft Intune



- **Gestione di dispositivi mobili (MDM) in locale:**  

    - Numero dei pacchetti e dei profili di registrazione in blocco di Windows 10  

    - Statistiche di esito positivo o negativo della distribuzione per distribuzioni di applicazioni MDM in locale  




- **Distribuzione del sistema operativo:**  

    - Numero di immagini di avvio, driver, pacchetti di driver, punti di distribuzione abilitati per il multicast, punti di distribuzione che supportano PXE e sequenze di attività  

    - Numero di immagini di avvio per versione client di Configuration Manager

    - Numero di immagini di avvio per versione di Windows PE

    - Numero di criteri di aggiornamento dell'edizione

    - Numero di identificatori hardware esclusi da PXE

    - ***[Nuovo]***  Numero di distribuzioni del sistema operativo in base alla versione del sistema operativo

    - ***[Nuovo]***  Numero di aggiornamenti del sistema operativo nel tempo

    - Numero di distribuzioni di sequenze di attività che usano l'opzione di pre-download del contenuto

    - Numero uilizzi del passaggio della sequenza di attività

    - Versione di Windows ADK installata


- **Aggiornamenti del sito:**

    - Versioni degli hotfix di Configuraton Manager installati



- **Aggiornamenti del software:**  

    - Valori differenziali di disponibilità e scadenza usati nelle regole di distribuzione automatica  

    - Numero medio e massimo di assegnazioni per ogni aggiornamento  

    - Pianificazioni di valutazione e analisi per l'aggiornamento dei client  

    - Classificazioni sincronizzate dal punto di aggiornamento software

    - Statistiche relative all'applicazione di patch al cluster  

    - Configurazione degli aggiornamenti rapidi di Windows 10

    - Configurazioni usate per i piani di manutenzione attivi di Windows 10  

    - Numero di aggiornamenti di Office 365 distribuiti  

    - Numero di driver di Microsoft Surface sincronizzati

    - Numero di gruppi e assegnazioni di aggiornamento  

    - Numero di pacchetti di aggiornamento e numero massimo/minimo/medio dei punti di distribuzione assegnati con pacchetti  

    - Numero di aggiornamenti creati e distribuiti con System Center Update Publisher  

    - Numero di client Windows 10 che usano Windows Update per le aziende  

    - Numero di criteri di Windows Update per le aziende creati e distribuiti

    - Numero di regole di distribuzione automatica associate alla sincronizzazione  

    - Numero di regole di distribuzione automatica che aggiungono aggiornamenti o ne creano di nuovi in un gruppo esistente  

    - Numero di regole di distribuzione automatica con più distribuzioni  

    - Numero di gruppi di aggiornamento e numero minimo/massimo/medio di aggiornamenti per ogni gruppo  

    - Numero di aggiornamenti e percentuale di aggiornamenti distribuiti, scaduti, sostituiti, scaricati e contenenti EULA  

    - Statistiche di bilanciamento del carico del punto di aggiornamento software

    - Pianificazione della sincronizzazione dei punti di aggiornamento software  

    - Numero totale/medio di raccolte con distribuzioni di aggiornamento del software e numero massimo/medio di aggiornamenti distribuiti  

    - Codici di errore e numero di computer per l'analisi per l'aggiornamento  

    - Versioni del contenuto del dashboard di Windows 10  



- **Dati SQL/prestazioni:**  

    - Configurazione e durata del riepilogo del sito

    - Numero delle tabelle di database più grandi  

    - Statistiche operative di individuazione (numero di oggetti trovati)

    - Tipi di individuazione, abilitazione e pianificazione (completa, incrementale)

    - Stato d'integrità, utilizzo e informazioni sulla replica di SQL AlwaysOn

    - Problemi di prestazioni del rilevamento modifiche di SQL, periodo di memorizzazione e stato di pulizia automatica

    - Periodo di memorizzazione del rilevamento modifiche di SQL

    - Statistiche sullo stato e sulle prestazioni relative ai messaggi di stato, inclusi i tipi di messaggio più costosi e più comuni



- **Varie**

    - Configurazione del punto di servizio del data warehouse, inclusi il tempo medio e la pianificazione della sincronizzazione

    - Numero di script e statistiche di esecuzione

    - Numero dei siti con riattivazione LAN (WOL)

    - Statistiche sull'utilizzo e sulle prestazioni dalla funzionalità di creazione di report  



##  <a name="level-3---full"></a><a name="bkmk_level3"></a> Livello 3 - Completo
Il livello completo include tutti i dati dei livelli di base e avanzato. Include inoltre informazioni aggiuntive su Endpoint Protection, le percentuali di conformità degli aggiornamenti e informazioni sugli aggiornamenti software.  Questo livello può includere anche informazioni di diagnostica avanzate, come file di sistema e snapshot di memoria, che possono contenere informazioni personali presenti in memoria o nei file di log al momento dell'acquisizione.

Per Configuration Manager versione 1710, questo livello include quanto segue:

- Informazioni sulla pianificazione di valutazione delle regole di distribuzione automatiche

- Riepilogo dell'integrità ATP

- Statistiche di valutazione e aggiornamento delle raccolte

- Statistiche dei criteri di conformità per la conformità e gli errori

- Impostazioni di conformità: dettagli di configurazione SCEP, VPN, Wi-Fi e del modello dei criteri di conformità e numero di gruppi con aggiornamenti software scaduti

- Utilizzo del pacchetto di configurazione DCM per Configuration Manager

- Errori di installazione della distribuzione client dettagliati

- Riepilogo dell'integrità di Endpoint Protection (incluso il numero di client protetti, a rischio, sconosciuti e non supportati)

- Configurazione dei criteri di Endpoint Protection

- Elenco dei processi configurati con il comportamento di installazione per le applicazioni

- Numero minimo/massimo/medio di ore dall'ultima analisi di aggiornamenti software

- Numero minimo/massimo/medio dei client inattivi nelle raccolte di distribuzioni di aggiornamenti software

- Numero minimo/massimo/medio di aggiornamenti software per ogni gruppo

- Codice prodotto MSI (app comuni distribuite dai clienti)

- Conformità generale delle distribuzioni degli aggiornamenti software

- Codici e numero di errori di distribuzione degli aggiornamenti software

- Informazioni sulla distribuzione degli aggiornamenti software (percentuale di distribuzioni assegnate con client o ora UTC, aggiornamento obbligatorio o facoltativo ed eliminazione del riavvio)

- Prodotti di aggiornamento software sincronizzati dal punto di aggiornamento software

- Percentuali di analisi dell'aggiornamento software con esito positivo

- Prime 50 CPU dell'ambiente

- Tipo di criteri di accesso condizionale EAS (blocco o quarantena) per i dispositivi gestiti da Intune

- Dettagli delle applicazioni di Microsoft Store per le aziende, tra cui l'elenco non aggregato di applicazioni sincronizzate, che include l'ID dell'app, lo stato online o offline e il numero totale di licenze acquistate
