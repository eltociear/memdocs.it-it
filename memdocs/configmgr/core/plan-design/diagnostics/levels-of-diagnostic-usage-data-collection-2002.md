---
title: Dati di diagnostica e utilizzo per la versione 2002
titleSuffix: Configuration Manager
description: Informazioni sui dati specifici raccolti da Configuration Manager a ogni livello nella versione 2002.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
ms.assetid: 264ea96f-f26a-4fb7-a23f-ecf36054e54b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7db3c587d592f7ef972e53a8bbdc2b27da1abbf4
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126546"
---
# <a name="diagnostic-and-usage-data-for-version-2002"></a>Dati di diagnostica e utilizzo per la versione 2002

*Si applica a: Configuration Manager (Current Branch)*

Le sezioni seguenti forniscono ulteriori dettagli sui dati raccolti in ogni livello. Per altre informazioni sui livelli e su come modificarli, vedere [Livelli dei dati di diagnostica e utilizzo](levels-overview.md).

Le modifiche rispetto alle versioni precedenti sono contrassegnate da ***[Nuovo]***, ***[Aggiornato]***, ***[Rimosso]*** o ***[Spostato]***.

> [!IMPORTANT]
> Configuration Manager non raccoglie codici del sito, nomi di siti, indirizzi IP, nomi utente, nomi di computer, indirizzi fisici o indirizzi di posta elettronica per i livelli di base e avanzato. Qualsiasi raccolta di queste informazioni al livello Completo non è intenzionale. Tali informazioni sono infatti potenzialmente incluse nelle informazioni diagnostiche avanzate quali i file di log o gli snapshot di memoria. Le informazioni eventualmente raccolte non vengono usate da Microsoft per identificare l'utente, contattare l'utente o per fini pubblicitari.

## <a name="level-1---basic"></a><a name="bkmk_level1"></a> Livello 1 - Di base

Per Configuration Manager versione 2002, questo livello include i dati seguenti:

- Statistiche sulle connessioni della console di Configuration Manager: versione del sistema operativo, lingua, SKU e architettura, memoria di sistema, conteggio dei processori logici, ID del sito di connessione, versioni di .NET installate, language pack della console e livello di autenticazione supportato

- Conteggi di base per applicazioni e tipi di distribuzione: totale app, totale app con più tipi di distribuzione, totale app con dipendenze, totale app sostituite e numero delle tecnologie di distribuzione in uso

- ***[Aggiornato]*** Dati di base sulla gerarchia dei siti di Configuration Manager: elenco dei siti, tipo, versione, stato, numero di client, fuso orario e stato integrità

- Configurazione del database di base: processori, dimensioni della memoria, impostazioni della memoria, configurazione del database di Configuration Manager, dimensioni del database di Configuration Manager, configurazione cluster, configurazione delle viste distribuite e versione del rilevamento modifiche  

- Statistiche di individuazione di base: numero di individuazioni e dimensioni minime/massime/medie dei gruppi e anche quando il sito viene eseguito interamente con i servizi Azure Active Directory

- Informazioni di base su Endpoint Protection circa versioni client antimalware

- Numero di immagini della distribuzione del sistema operativo di base

- Informazioni di base sul server del sistema del sito: ruoli del sistema del sito usati, stato di Internet e SSL, sistema operativo, processori, computer fisico o macchina virtuale e utilizzo della disponibilità elevata dei server del sito

- Schema del database di Configuration Manager (hash di tutte le definizioni di oggetti)

- Livello configurato per dati di diagnostica e utilizzo, modalità online o offline e configurazione di aggiornamento rapido

- Numero delle lingue e delle impostazioni locali dei client

- Numero delle versioni client di Configuration Manager, delle versioni del sistema operativo e delle versioni di Office

- Numero dei sistemi operativi per i dispositivi gestiti e dei criteri impostati da Exchange Connector

- Numero di dispositivi Windows 10 per ramo, build e foresta Active Directory univoca  

- ***[Rimosso]*** Numero di client Windows 10 che usano Windows Update per le aziende  

- Metriche delle prestazioni del database: informazioni sull'elaborazione della replica, principali stored procedure di SQL Server per processore e utilizzo del disco

- Tipi di punto di distribuzione e di punto di gestione e informazioni di base sulla configurazione: protetto, pre-installato, PXE, multicast, stato di SSL, punti di distribuzione pull/peer, abilitato per MDM e abilitato per SSL

- Elenco di estensioni con hash per le pagine delle proprietà e le procedure guidate della console di amministrazione

- Informazioni sull'installazione:  

  - Build, tipo di installazione, Language Pack, funzionalità abilitate

  - Uso delle versioni non definitive, tipo di supporto di installazione, tipo Branch  

  - Data di scadenza di Software Assurance  

  - Stato di distribuzione ed errori del pacchetto di aggiornamento, stato del download ed errori dei prerequisiti

  - Uso di Fast Ring di aggiornamento  

  - Versione dello script post-aggiornamento  

- Versione SQL, livello Service Pack, edizione, ID delle regole di confronto e set di caratteri  

- Statistiche sui dati di diagnostica e utilizzo: data/ora di esecuzione, runtime ed errori  

- Se l'individuazione di rete è abilitata o disabilitata  

- Numero di client aggiunti ad Azure Active Directory  

- ***[Rimosso]*** Numero di distribuzioni in più fasi create per tipo  

- Numero di client di interoperabilità estesa  

- Elenco con hash di proprietà dell'inventario hardware con più di 255 caratteri  

- Numero di client in base al metodo di registrazione di co-gestione  

- Statistiche degli errori per la registrazione di co-gestione  

- Numero di client in base all'età del sistema operativo Windows, fino all'intervallo di tre mesi più recente  

- Primi 10 nomi di processori usati nei client e nei server  

- Numero e velocità di elaborazione degli oggetti chiave di Configuration Manager: record di individuazione dati, messaggi sullo stato attuale, messaggi di stato, inventario hardware, inventario software e numero totale di file nelle cartelle Posta in arrivo  

- Informazioni sulle prestazioni dei processori e dei dischi del server del sito  

- Informazioni sul tempo di attività e sull'utilizzo della memoria per i processi del server del sito di Configuration Manager  

- Numero di arresti anomali per i processi del server del sito di Configuration Manager e ID firma di Watson, se disponibile  

- Elenco con hash delle principali query SQL in base a utilizzo di memoria e numero di blocchi  

- Statistiche di utilizzo aggregate relative alla co-gestione: numero di client registrati di sempre, numero di client registrati, numero di client in attesa di registrazione, client che ricevono criteri, stati dei carichi di lavoro, dimensioni delle raccolte di esclusioni/pilota ed errori di registrazione  

- Disponibilità delle estensioni sul lato server Microsoft BitLocker Administration and Monitoring (MBAM)  

- Numero di applicazioni con e senza categoria per Asset Intelligence

- Stato e integrità del servizio di amministrazione

- Hash degli attributi chiave del sito (ID sito, ID broker SQL e chiave di scambio tra siti)

- Numero di installazioni di Microsoft Edge

- ***[Spostato]*** Numero delle applicazioni e dei servizi di Azure Active Directory connessi a Configuration Manager

- ***[Nuovo]*** Informazioni sull'integrità del sito

- ***[Nuovo]*** Posizioni di arresto anomalo della console di Configuration Manager

- ***[Nuovo]*** Statistiche di utilizzo della console di Configuration Manager

- ***[Nuovo]*** Azioni di collegamento e scollegamento del cloud

- ***[Nuovo]*** Stato dell'ultima sincronizzazione con il servizio cloud di Intune

- ***[Nuovo]*** Numeri di errori dal servizio di amministrazione

- ***[Nuovo]*** Uso del token di registrazione in blocco

- ***[Nuovo]*** Numero di client in base al browser predefinito e preferito

## <a name="level-2---enhanced"></a><a name="bkmk_level2"></a> Livello 2 - Avanzato

Per Configuration Manager versione 2002, questo livello include i dati seguenti:

### <a name="application-management"></a>Gestione delle applicazioni  

- Requisiti delle app: conteggio delle condizioni predefinite con riferimento per tecnologia di distribuzione  

- Sostituzione delle app, profondità massima della catena  

- Statistiche sull'approvazione delle applicazioni e frequenza di utilizzo  

- Statistiche sulle dimensioni del contenuto delle applicazioni  

- Informazioni sulla distribuzione delle applicazioni: uso dell'installazione rispetto alla disinstallazione, obbligatorietà dell'approvazione, abilitazione o disabilitazione dell'interazione con l'utente, dipendenza, sostituzione e numero di utilizzi della funzionalità relativa al comportamento dell'installazione  

- Dimensioni criteri di applicazione e statistiche di complessità  

- Dati statistici sulle richieste di applicazioni disponibili  

- Informazioni di configurazione di base per pacchetti e programmi: opzioni di distribuzione e flag di programma  

- Informazioni di base su utilizzo/destinazione per i tipi di distribuzione: utente e dispositivo di destinazione, richiesto o disponibile e app universali  

- Numero di ambienti e proprietà di distribuzione App-V  

- Numero di applicabilità delle applicazioni per sistema operativo  

- Numero di applicazioni a cui fa riferimento una sequenza di attività  

- Numero di personalizzazioni distinte per catalogo applicazioni  

- Numero di applicazioni di Office 365 create tramite il dashboard  

- Numero di pacchetti per tipo  

- Numero di distribuzioni di pacchetti/programmi  

- Numero di licenze per applicazioni con licenza Windows 10  

- Numero di tipi di distribuzione di Windows Installer in base alle impostazioni di disinstallazione del contenuto  

- Numero di app di Microsoft Store per le aziende e statistiche di sincronizzazione: riepilogo dei tipi di app, stato delle app con licenza e numero di app con licenza online e offline  

- Tipo e durata della finestra di manutenzione  

- Numero massimo/minimo/medio di distribuzioni di applicazioni per ogni utente o dispositivo per periodo  

- Codici di errore di installazione delle applicazioni più comuni per tecnologia di distribuzione  

- Opzioni di configurazione MSI e conteggi  

- Statistiche sull'interazione degli utenti finali con notifica per le distribuzioni software obbligatorie  

- Utilizzo di Universal Data Access, modalità di creazione  

- Statistiche aggregate sull'affinità utente-dispositivo  

- Numero massimo e medio di utenti primari per dispositivo  

- Utilizzo delle condizioni globali dell'applicazione per tipo  

- Configurazione della personalizzazione di Software Center  

- Conformità e conteggi di Package Conversion Manager  

- Numero di metodi di rilevamento dell'applicazione per tipo  

- Numero di errori di imposizione dell'applicazione  

- Proprietà del programma di installazione MSI  

- Statistiche delle richieste di installazione dell'utente  

- Statistiche aggregate relative all'uso della funzionalità di approvazione tramite posta elettronica  

- Numero di file, dimensioni del contenuto, numero di servizi e numero di azioni personalizzate dei file MSI nel catalogo applicazioni  

- Numero di dispositivi per stato di conformità di Office ProPlus

- Statistiche aggregate sull'uso di gruppi di applicazioni

- Statistiche aggregate su componenti aggiuntivi per Office, uso di Office Readiness Toolkit e numero di client con Office 365 ProPlus

- Statistiche aggregate sull'integrità del componente aggiuntivo per Office

- Numero e dimensioni delle raccolte pilota di Office Pro Plus

- ***[Nuovo]*** Numero di dispositivi Office Pro Plus che inviano dati di integrità Office

### <a name="client"></a>Client  

- Versione del client AMT (Active Management Technology)  

- Età del BIOS in anni  

- Numero di dispositivi con avvio protetto abilitato  

- Numero di dispositivi in base allo stato TPM  

- Aggiornamento automatico del client: configurazione della distribuzione inclusi la distribuzione pilota del client e l'utilizzo di esclusioni (client a interoperabilità estesa)  

- Configurazione della dimensione della cache del client  

- Errori di download della distribuzione client  

- Statistiche sull'integrità dei client e riepilogo dei principali problemi per versione client, componente, sistema operativo e carico di lavoro  

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

- Statistiche per l'attestazione dell'integrità del dispositivo: codici di errore più comuni, numero di server locali e numero di dispositivi nei vari stati  

- Numero di dispositivi per browser predefinito  

- Numero di certificati di autenticazione server generati da Configuration Manager  

- Numero di dispositivi Microsoft Surface per modello  

- Numero di errori di controllo integrità client per tipo di problema

### <a name="cloud-services"></a>Servizi cloud  

- Statistiche di individuazione di Azure Active Directory  

- Statistiche di configurazione e utilizzo di Cloud Management Gateway: numero delle aree e degli ambienti e statistiche di autenticazione e autorizzazione  

- Numero di raccolte sincronizzate con Azure Log Analytics  

- Numero di connettori di analisi degli aggiornamenti  

- Indica se il connettore cloud Azure Log Analytics è abilitato  

- Numero di punti di distribuzione pull con un punto di distribuzione cloud come percorso di origine

- ***[Nuovo]*** Utilizzo della procedura guidata di onboarding dei servizi cloud

### <a name="cmpivot"></a>CMPivot

- Statistiche di utilizzo di CMPivot  

- Numero di query CMPivot salvate  

- Numero di query per tipo di entità  

### <a name="co-management"></a>Co-gestione  

- Statistiche cronologiche e pianificazione della registrazione  

- Numero di client idonei per la co-gestione  

- Tenant di Microsoft Intune associato  

### <a name="collections"></a>Raccolte  

- Uso ID raccolte (senza esaurimento degli ID)  

- Statistiche di valutazione raccolte: durata query, conteggi assegnati e non assegnati, conteggi per tipo, rollover degli ID e utilizzo delle regole  

- Raccolte senza distribuzione  

- Numero di raccolte sincronizzate con Azure Active Directory

### <a name="compliance-settings"></a>Impostazioni di conformità  

- Informazioni di base sulla linea di base di configurazione: numero, numero di distribuzioni e numero di riferimenti  

- Statistiche degli errori relativi ai criteri di conformità  

- Numero di elementi di configurazione per tipo  

- Numero di distribuzioni che fanno riferimento a impostazioni predefinite, inclusa l'impostazione di correzione  

- Numero di regole e di distribuzioni create per le impostazioni personalizzate inclusa l'impostazione di correzione  

- Numero di certificati SCEP (Simple Certificate Enrollment Protocol), VPN, Wi-Fi, certificati (.pfx) e modelli dei criteri di conformità distribuiti  

- Numero di certificati SCEP, VPN, Wi-Fi, certificati (PFX) e distribuzioni dei criteri di conformità per piattaforma  

- Criteri di Windows Hello for Business (creati, distribuiti)  

- Numero di criteri del browser distribuiti della versione legacy di Microsoft Edge  

- Numero di criteri OneDrive (creati, distribuiti)

### <a name="configuration-manager-console"></a>Console di Configuration Manager

- Numero di notifiche della console non critiche

- Numero di cartelle

- ***[Nuovo]*** Informazioni sulle prestazioni della console

- ***[Nuovo]*** 25 azioni più comuni, procedure guidate, finestre delle proprietà e nodi dell'albero accessibili nella console

### <a name="content"></a>Content  

- Statistiche dei gruppi di limiti: numero di rapidi e lenti, conteggio per gruppo e relazioni di fallback  

- Informazioni sui gruppi di limiti: numero di limiti e di sistemi del sito assegnati a ogni gruppo di limiti  

- Relazioni di gruppi di limiti e configurazione del fallback  

- Statistiche di download dei contenuti client  

- Numero di limiti per tipo  

- Numero di client peer cache, statistiche di utilizzo e statistiche di download parziale  

- Informazioni di configurazione di Distribution Manager: thread, intervallo tra tentativi, numero di tentativi e impostazioni dei punti di distribuzione pull  

- Informazioni di configurazione sui punti di distribuzione: uso di BranchCache e monitoraggio dei punti di distribuzione  

- Informazioni sui gruppi di punti di distribuzione: numero di pacchetti e punti di distribuzione assegnati a ogni gruppo di punti di distribuzione  

- Tipo di raccolta contenuto, locale o remota  

- Numero di gruppi di limiti per configurazione

- ***[Nuovo]*** Numero di subnet escluse dalla peer cache

### <a name="endpoint-protection"></a>Endpoint Protection  

- Criteri avanzati di Microsoft Defender Advanced Threat Protection (ATP) (noto in precedenza come Windows Defender ATP): numero dei criteri e avvenuta distribuzione o meno dei criteri.

- Numero di avvisi configurati per la funzionalità Endpoint Protection  

- Numero di raccolte selezionate per la visualizzazione nel dashboard di Endpoint Protection  

- Numero di criteri di Windows Defender Exploit Guard, distribuzioni e client di destinazione  

- Errori di distribuzione di Endpoint Protection: numero di codici di errore di distribuzione dei criteri di Endpoint Protection  

- Utilizzo dei criteri antimalware di Endpoint Protection e di Windows Firewall (numero di criteri univoci assegnati al gruppo). Non sono incluse informazioni sulle impostazioni contenute nei criteri.

- ***[Nuovo]*** Statistiche aggregate per i criteri di Microsoft Defender Advanced Threat Protection

### <a name="migration"></a>Migrazione  

- Numero di oggetti migrati (uso della procedura guidata di migrazione)  

### <a name="mobile-device-management-mdm"></a>Gestione di dispositivi mobili (MDM)  

- Numero di azioni eseguite su dispositivi mobili: comandi di blocco, reimpostazione PIN, cancellazione, ritiro e sincronizzazione immediata  

- Numero di criteri per dispositivi mobili  

- Numero di dispositivi mobili gestiti da Configuration Manager e modalità di registrazione (in blocco, basata sull'utente)  

- Numero di utenti con più dispositivi mobili registrati  

- Pianificazione del polling dei dispositivi mobili e statistiche della durata della registrazione dei dispositivi mobili  

### <a name="microsoft-intune-troubleshooting"></a>Risoluzione dei problemi di Microsoft Intune  

- Numero e dimensioni dei messaggi relativi ad azioni sui dispositivi (cancellazione, ritiro dati, blocco), dati di utilizzo e dati replicati in Microsoft Intune  

- Numero e dimensioni dei messaggi relativi a stato, inventario, RDR, DDR, UDX, stato tenant, POL, LOG, Cert, CRP, risincronizzazione, CFD, RDO, BEX, ISM e conformità scaricati da Microsoft Intune  

- Statistiche della sincronizzazione degli utenti completa e differenziale per Microsoft Intune  

### <a name="on-premises-mobile-device-management-mdm"></a>Gestione dei dispositivi mobili in locale (MDM)  

- Numero dei pacchetti e dei profili di registrazione in blocco di Windows 10  

- Statistiche di esito positivo o negativo della distribuzione per distribuzioni di applicazioni MDM in locale  

### <a name="os-deployment"></a>Distribuzione del sistema operativo  

- Numero di immagini di avvio, driver, pacchetti di driver, punti di distribuzione abilitati per il multicast, punti di distribuzione che supportano PXE e sequenze di attività  

- Numero di immagini di avvio per versione client di Configuration Manager  

- Numero di immagini di avvio per versione di Windows PE  

- Numero di criteri di aggiornamento dell'edizione  

- Numero di identificatori hardware esclusi da PXE  

- Numero di distribuzioni del sistema operativo in base alla versione del sistema operativo  

- Numero di aggiornamenti del sistema operativo nel tempo  

- Numero di distribuzioni di sequenze di attività che usano l'opzione di pre-download del contenuto  

- Numero uilizzi del passaggio della sequenza di attività  

- Versione di Windows ADK installata  

- Numero di attività di manutenzione delle immagini  

- Numero di computer importati  

- Numero di identificatori hardware duplicati (indirizzo MAC e GUID SMBIOS) esclusi da PXE e dalla registrazione client

- Numero di sequenze di attività per tipo (distribuzione del sistema operativo o sequenza di attività generiche)

- Numero di pacchetti con impostazioni per la memorizzazione anticipata del contenuto nella cache

### <a name="site-updates"></a>Aggiornamenti del sito  

- Versioni degli hotfix di Configuraton Manager installati  

### <a name="software-updates"></a>Aggiornamenti software  

- Valori differenziali di disponibilità e scadenza usati nelle regole di distribuzione automatica  

- Numero medio e massimo di assegnazioni per ogni aggiornamento  

- Pianificazioni di valutazione e analisi per l'aggiornamento dei client  

- Classificazioni sincronizzate dal punto di aggiornamento software  

- Statistiche relative all'applicazione di patch al cluster  

- ***[Rimosso]*** Configurazione degli aggiornamenti rapidi di Windows 10  

- Configurazioni usate per i piani di manutenzione attivi di Windows 10  

- Numero di aggiornamenti di Office 365 distribuiti  

- Numero di driver di Microsoft Surface sincronizzati  

- ***[Rimosso]*** Numero di gruppi e assegnazioni di aggiornamento  

- ***[Rimosso]*** Numero di pacchetti di aggiornamento e numero massimo/minimo/medio dei punti di distribuzione assegnati con pacchetti  

- ***[Rimosso]*** Numero di aggiornamenti creati e distribuiti con System Center Update Publisher  

- ***[Rimosso]*** Numero di criteri di Windows Update per le aziende creati e distribuiti  

- Statistiche aggregate delle configurazioni di Windows Update per le aziende  

- ***[Rimosso]*** Numero di regole di distribuzione automatica associate alla sincronizzazione  

- ***[Rimosso]*** Numero di regole di distribuzione automatica che aggiungono aggiornamenti o ne creano di nuovi in un gruppo esistente  

- Numero di regole di distribuzione automatica con più distribuzioni  

- Numero di gruppi di aggiornamento e numero minimo/massimo/medio di aggiornamenti per ogni gruppo  

- Numero di aggiornamenti e percentuale di aggiornamenti distribuiti, scaduti, sostituiti, scaricati e contenenti EULA  

- Statistiche di bilanciamento del carico del punto di aggiornamento software  

- Pianificazione della sincronizzazione dei punti di aggiornamento software  

- ***[Rimosso]*** Numero totale/medio di raccolte con distribuzioni di aggiornamento del software e numero massimo/medio di aggiornamenti distribuiti  

- Codici di errore e numero di computer per l'analisi per l'aggiornamento  

- Versioni del contenuto del dashboard di Windows 10  

- Numero di sottoscrizioni dei cataloghi di aggiornamenti software di terze parti e utilizzo  

- Numero di aggiornamenti software distribuiti con e senza contenuto  

- Statistiche aggregate relative al numero di aggiornamenti UUP necessari, distribuiti, scaduti, sostituiti e scaricati  

- Uso delle categorie di prodotto UUP  

- Numero di client che hanno distribuito almeno un aggiornamento qualitativo UUP o un aggiornamento delle funzionalità UUP  

- Principali codici di errore UUP e numero di dispositivi interessati  

- Elenco di sottoscrizioni di cataloghi di aggiornamento software di terze parti

- Uso delle impostazioni di manutenzione WSUS

- ***[Nuovo]*** Utilizzo del gruppo di orchestrazione

- ***[Nuovo]*** Impostazioni di configurazione di fallback di Windows Update

### <a name="sqlperformance-data"></a>Dati SQL/prestazioni  

- Configurazione e durata del riepilogo del sito  

- Numero delle tabelle di database più grandi  

- Statistiche operative di individuazione (numero di oggetti trovati)  

- Tipi di individuazione, abilitazione e pianificazione (completa, incrementale)  

- Stato d'integrità, utilizzo e informazioni sulla replica di SQL AlwaysOn  

- Problemi di prestazioni del rilevamento modifiche di SQL, periodo di memorizzazione e stato di pulizia automatica  

- Periodo di memorizzazione del rilevamento modifiche di SQL  

- Statistiche sullo stato e sulle prestazioni relative ai messaggi di stato, inclusi i tipi di messaggio più costosi e più comuni  

- Statistiche sul traffico del punto di gestione (byte totali inviati e ricevuti da ogni endpoint)  

- Misurazioni del contatore delle prestazioni del punto di gestione  

- Statistiche aggregate relative alle prestazioni delle chiamate effettuate agli endpoint di Software Center nel punto di gestione

- Configurazione e stato dell'attività di manutenzione di SQL

- ***[Nuovo]*** Stato delle richieste di reinizializzazione recenti

### <a name="miscellaneous"></a>Varie  

- Configurazione del punto di servizio del data warehouse, inclusi pianificazione della sincronizzazione, tempo medio e uso della funzionalità di tabelle personalizzate  

- Numero di script e statistiche di esecuzione/modifica  

- Numero di siti con riattivazione LAN (WOL)  

- Statistiche sull'utilizzo e sulle prestazioni dalla funzionalità di creazione di report  

- Statistiche di utilizzo delle distribuzioni in più fasi  

- Conteggi e stato degli elementi di informazioni dettagliate sulla gestione  

- Numero di arresti anomali per i processi non di Configuration Manager univoci sul server del sito e ID firma di Watson, se disponibile  

- Statistiche aggregate relative a errori di registrazione e utilizzo di Desktop Analytics

- Statistiche aggregate relative al tempo di avvio del sistema per sistema operativo, fattore di forma e tipo di unità

- Statistiche aggregate sull'uso di Desktop Analytics

- Utilizzo dello strumento di migrazione di Azure

- ***[Nuovo]*** Numero di client con utilizzo del browser

## <a name="level-3---full"></a><a name="bkmk_level3"></a> Livello 3 - Completo

Per Configuration Manager versione 2002, questo livello include i dati seguenti:

- ***[Rimosso]*** Informazioni sulla pianificazione di valutazione delle regole di distribuzione automatiche  

- Riepilogo dell'integrità ATP  

- Statistiche di valutazione e aggiornamento delle raccolte  

- Statistiche dei criteri di conformità per la conformità e gli errori  

- Impostazioni di conformità: dettagli di configurazione SCEP, VPN, Wi-Fi e del modello dei criteri di conformità  

- Utilizzo del pacchetto di configurazione DCM per Configuration Manager  

- Errori di installazione della distribuzione client dettagliati  

- Riepilogo dell'integrità di Endpoint Protection: numero di client protetti, a rischio, sconosciuti e non supportati  

- Configurazione dei criteri di Endpoint Protection  

- Elenco dei processi configurati con il comportamento di installazione per le applicazioni  

- ***[Rimosso]*** Numero minimo/massimo/medio di ore dall'ultima analisi di aggiornamenti software  

- ***[Rimosso]*** Numero minimo/massimo/medio dei client inattivi nelle raccolte di distribuzioni di aggiornamenti software  

- Numero minimo/massimo/medio di aggiornamenti software per ogni gruppo  

- Statistiche di distribuzione dei codici prodotto MSI  

- Conformità generale delle distribuzioni degli aggiornamenti software  

- ***[Rimosso]*** Numero di gruppi con aggiornamenti software scaduti  

- Codici e numero di errori di distribuzione degli aggiornamenti software  

- Informazioni sulla distribuzione degli aggiornamenti software: percentuale di distribuzioni assegnate con client o ora UTC, aggiornamento obbligatorio o facoltativo ed eliminazione del riavvio  

- Prodotti di aggiornamento software sincronizzati dal punto di aggiornamento software  

- Percentuali di analisi dell'aggiornamento software con esito positivo  

- Prime 50 CPU dell'ambiente  

- Tipo di criteri di accesso condizionale di Exchange Active Sync (EAS) (blocco o quarantena) per i dispositivi gestiti da Microsoft Intune  

- Dettagli delle applicazioni di Microsoft Store per le aziende: elenco non aggregato di applicazioni sincronizzate, che include l'ID dell'app, stato online o offline e numero totale di licenze acquistate  

- Numero dei client di cui è stato eseguito il push con l'opzione per non consentire il fallback a NTLM  

- Elenco di estensioni della console di Configuration Manager
