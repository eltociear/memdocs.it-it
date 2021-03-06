---
title: Dati di utilizzo e di diagnostica per la versione 1810
titleSuffix: Configuration Manager
description: Informazioni sui dati specifici raccolti da Configuration Manager a ogni livello nella versione 1810.
ms.date: 05/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
ms.assetid: bce9e299-7b3a-4f51-8863-a322877daa2c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: afca31c224e40efa79638f05192259d0986e1e72
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88994634"
---
# <a name="diagnostic-and-usage-data-for-version-1810"></a>Dati di diagnostica e utilizzo per la versione 1810

*Si applica a: Configuration Manager (Current Branch)*

Le sezioni seguenti forniscono ulteriori dettagli sui dati raccolti in ogni livello. Per altre informazioni sui livelli e su come modificarli, vedere [Livelli dei dati di diagnostica e utilizzo](levels-overview.md).

Le modifiche rispetto alle versioni precedenti sono contrassegnate da ***[Nuovo]***, ***[Aggiornato]***, ***[Rimosso]*** o ***[Spostato]***.

> [!IMPORTANT]
> Configuration Manager non raccoglie codici del sito, nomi di siti, indirizzi IP, nomi utente, nomi di computer, indirizzi fisici o indirizzi di posta elettronica per i livelli di base e avanzato. Qualsiasi raccolta di queste informazioni al livello Completo non è intenzionale. Tali informazioni sono infatti potenzialmente incluse nelle informazioni diagnostiche avanzate quali i file di log o gli snapshot di memoria. Le informazioni eventualmente raccolte non vengono usate da Microsoft per identificare l'utente, contattare l'utente o per fini pubblicitari.

## <a name="level-1---basic"></a><a name="bkmk_level1"></a> Livello 1 - Di base

Per Configuration Manager versione 1810, questo livello include i dati seguenti:

- Statistiche sulle connessioni della console di Configuration Manager: versione del sistema operativo, lingua, SKU e architettura, memoria di sistema, conteggio dei processori logici, ID del sito di connessione, versioni di .NET installate e Language Pack della console

- Conteggi di base per applicazioni e tipi di distribuzione: totale app, totale app con più tipi di distribuzione, totale app con dipendenze, totale app sostituite e numero delle tecnologie di distribuzione in uso

- Dati di base sulla gerarchia dei siti di Configuration Manager: elenco dei siti, tipo, versione, stato, numero di client e fuso orario

- ***[Aggiornato]*** Configurazione del database di base: processori, dimensioni della memoria, impostazioni della memoria, configurazione del database di Configuration Manager, dimensioni del database di Configuration Manager, configurazione cluster, configurazione delle viste distribuite e versione del rilevamento modifiche  

- Statistiche di individuazione di base: numero di individuazioni e dimensioni minime/massime/medie dei gruppi e anche quando il sito viene eseguito interamente con i servizi Azure Active Directory

- Informazioni di base su Endpoint Protection circa versioni client antimalware

- Numero di immagini della distribuzione del sistema operativo di base

- Informazioni di base sul server del sistema del sito: ruoli del sistema del sito usati, stato di Internet e SSL, sistema operativo, processori, computer fisico o macchina virtuale e utilizzo della disponibilità elevata dei server del sito

- Schema del database di Configuration Manager (hash di tutte le definizioni di oggetti)

- Livello configurato per dati di diagnostica e utilizzo, modalità online o offline e configurazione di aggiornamento rapido

- Numero delle lingue e delle impostazioni locali dei client

- Numero delle versioni client di Configuration Manager, delle versioni del sistema operativo e delle versioni di Office

- Numero dei sistemi operativi per i dispositivi gestiti e dei criteri impostati da Exchange Connector

- ***[Aggiornato]*** Numero di dispositivi Windows 10 per ramo, build e foresta Active Directory univoca  

- Numero di client Windows 10 che usano Windows Update per le aziende  

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

- Numero di distribuzioni in più fasi create per tipo  

- Numero di client di interoperabilità estesa  

- Elenco con hash di proprietà dell'inventario hardware con più di 255 caratteri  

- Numero di client in base al metodo di registrazione di co-gestione  

- Statistiche degli errori per la registrazione di co-gestione  

- Numero di client in base all'età del sistema operativo Windows, fino all'intervallo di tre mesi più recente  

- ***[Aggiornato]*** Primi 10 nomi di processori usati nei client e nei server  

- Numero e velocità di elaborazione degli oggetti chiave di Configuration Manager: record di individuazione dati, messaggi sullo stato attuale, messaggi di stato, inventario hardware, inventario software e numero totale di file nelle cartelle Posta in arrivo  

- Informazioni sulle prestazioni dei processori e dei dischi del server del sito  

- Informazioni sul tempo di attività e sull'utilizzo della memoria per i processi del server del sito di Configuration Manager  

- Numero di arresti anomali per i processi del server del sito di Configuration Manager e ID firma di Watson, se disponibile  

- ***[Nuovo]*** Elenco con hash delle principali query SQL per utilizzo di memoria e conteggio blocchi  

- ***[Spostato, aggiornato]*** Statistiche di utilizzo aggregate relative alla co-gestione: numero di client registrati di sempre, numero di client registrati, numero di client in attesa di registrazione, client che ricevono criteri, stati dei carichi di lavoro, dimensioni delle raccolte di esclusioni/pilota ed errori di registrazione  



## <a name="level-2---enhanced"></a><a name="bkmk_level2"></a> Livello 2 - Avanzato

Per Configuration Manager versione 1810, questo livello include i dati seguenti:

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

- Numero di applicazioni Microsoft 365 create tramite il dashboard  

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

- ***[Nuovo]*** Statistiche aggregate sull'uso della funzionalità di approvazione tramite posta elettronica  

- ***[Nuovo]***  Numero di file, dimensioni del contenuto, numero di servizi e numero di azioni personalizzate dei file MSI nel catalogo applicazioni  


### <a name="client"></a>Client  

- Versione del client AMT (Active Management Technology)  

- Età del BIOS in anni  

- Numero di dispositivi con avvio protetto abilitato  

- Numero di dispositivi in base allo stato TPM  

- Aggiornamento automatico del client: configurazione della distribuzione inclusi la distribuzione pilota del client e l'utilizzo di esclusioni (client a interoperabilità estesa)  

- Configurazione della dimensione della cache del client  

- Errori di download della distribuzione client  

- Statistiche dell'integrità dei client e riepilogo delle richieste principali per versione client  

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


### <a name="cloud-services"></a>Servizi cloud  

- Statistiche di individuazione di Azure Active Directory  

- Statistiche di configurazione e utilizzo di Cloud Management Gateway: numero delle aree e degli ambienti e statistiche di autenticazione e autorizzazione  

- Numero di applicazioni e di servizi di Azure Active Directory connessi a Configuration Manager  

- Numero di raccolte sincronizzate con Azure Log Analytics  

- Numero di connettori di analisi degli aggiornamenti  

- Indica se il connettore cloud Azure Log Analytics è abilitato  

- Numero di punti di distribuzione pull con un punto di distribuzione cloud come percorso di origine  


### <a name="cmpivot"></a>CMPivot

- Statistiche di utilizzo di CMPivot  

- ***[Nuovo]*** Numero di query CMPivot salvate  

- ***[Nuovo]***  Numero di query per tipo di entità  


### <a name="co-management"></a>Co-gestione  

- Statistiche cronologiche e pianificazione della registrazione  

- Numero di client idonei per la co-gestione  

- Tenant di Microsoft Intune associato  


### <a name="collections"></a>Raccolte  

- Uso ID raccolte (senza esaurimento degli ID)  

- Statistiche di valutazione raccolte: durata query, conteggi assegnati e non assegnati, conteggi per tipo, rollover degli ID e utilizzo delle regole  

- Raccolte senza distribuzione  


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

- ***[Nuovo]*** Numero di gruppi di limiti per configurazione  


### <a name="endpoint-protection"></a>Endpoint Protection  

- Criteri avanzati di Microsoft Defender Advanced Threat Protection (ATP) (noto in precedenza come Windows Defender ATP): numero dei criteri e avvenuta distribuzione o meno dei criteri. 

- Numero di avvisi configurati per la funzionalità Endpoint Protection  

- Numero di raccolte selezionate per la visualizzazione nel dashboard di Endpoint Protection  

- Numero di criteri di Windows Defender Exploit Guard, distribuzioni e client di destinazione  

- Errori di distribuzione di Endpoint Protection: numero di codici di errore di distribuzione dei criteri di Endpoint Protection  

- Utilizzo dei criteri antimalware di Endpoint Protection e di Windows Firewall (numero di criteri univoci assegnati al gruppo). Non sono incluse informazioni sulle impostazioni contenute nei criteri.  


### <a name="migration"></a>Migrazione  

- Numero di oggetti migrati (uso della procedura guidata di migrazione)  


### <a name="mobile-device-management-mdm"></a>Gestione di dispositivi mobili (MDM)  

- Numero di azioni eseguite su dispositivi mobili: comandi di blocco, reimpostazione PIN, cancellazione, ritiro e sincronizzazione immediata  

- Numero di criteri per dispositivi mobili  

- Numero di dispositivi mobili di Configuration Manager, gestioni di Microsoft Intune e modalità di registrazione (in blocco, basata sull'utente)  

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

- ***[Nuovo]*** Numero di computer importati  


### <a name="site-updates"></a>Aggiornamenti del sito  

- Versioni degli hotfix di Configuraton Manager installati  


### <a name="software-updates"></a>Aggiornamenti software  

- Valori differenziali di disponibilità e scadenza usati nelle regole di distribuzione automatica  

- Numero medio e massimo di assegnazioni per ogni aggiornamento  

- Pianificazioni di valutazione e analisi per l'aggiornamento dei client  

- Classificazioni sincronizzate dal punto di aggiornamento software  

- Statistiche relative all'applicazione di patch al cluster  

- Configurazione degli aggiornamenti rapidi di Windows 10  

- Configurazioni usate per i piani di manutenzione attivi di Windows 10  

- Numero di aggiornamenti di Microsoft 365 distribuiti  

- Numero di driver di Microsoft Surface sincronizzati  

- Numero di gruppi e assegnazioni di aggiornamento  

- Numero di pacchetti di aggiornamento e numero massimo/minimo/medio dei punti di distribuzione assegnati con pacchetti  

- Numero di aggiornamenti creati e distribuiti con System Center Update Publisher  

- Numero di criteri di Windows Update per le aziende creati e distribuiti  

- Statistiche aggregate delle configurazioni di Windows Update per le aziende  

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

- Numero di sottoscrizioni dei cataloghi di aggiornamenti software di terze parti e utilizzo  

- Numero di aggiornamenti software distribuiti con e senza contenuto  

- ***[Nuovo]*** Statistiche aggregate sul numero di aggiornamenti UUP necessari, distribuiti, scaduti, sostituiti e scaricati  

- ***[Nuovo]*** Utilizzo delle categorie di prodotto UUP  

- ***[Nuovo]***  Numero di client che hanno distribuito almeno un aggiornamento qualitativo UUP o un aggiornamento delle funzionalità UUP  

- ***[Nuovo]*** Principali codici di errore UUP e numero di dispositivi colpiti  


### <a name="sqlperformance-data"></a>Dati SQL/prestazioni  

- Configurazione e durata del riepilogo del sito  

- Numero delle tabelle di database più grandi  

- Statistiche operative di individuazione (numero di oggetti trovati)  

- Tipi di individuazione, abilitazione e pianificazione (completa, incrementale)  

- Stato d'integrità, utilizzo e informazioni sulla replica di SQL AlwaysOn  

- Problemi di prestazioni del rilevamento modifiche di SQL, periodo di memorizzazione e stato di pulizia automatica  

- Periodo di memorizzazione del rilevamento modifiche di SQL  

- Statistiche sullo stato e sulle prestazioni relative ai messaggi di stato, inclusi i tipi di messaggio più costosi e più comuni  

- ***[Nuovo]***  Statistiche sul traffico del punto di gestione (byte totali inviati e ricevuti dall'endpoint)  

- ***[Nuovo]*** Misurazioni del contatore delle prestazioni del punto di gestione  


### <a name="miscellaneous"></a>Varie  

- Configurazione del punto di servizio del data warehouse, inclusi il tempo medio e la pianificazione della sincronizzazione  

- Numero di script e statistiche di esecuzione  

- Numero di siti con riattivazione LAN (WOL)  

- Statistiche sull'utilizzo e sulle prestazioni dalla funzionalità di creazione di report  

- Statistiche di utilizzo delle distribuzioni in più fasi  

- Conteggi e stato degli elementi di informazioni dettagliate sulla gestione  

- Numero di arresti anomali per i processi non di Configuration Manager univoci sul server del sito e ID firma di Watson, se disponibile  



##  <a name="level-3---full"></a><a name="bkmk_level3"></a> Livello 3 - Completo

Per Configuration Manager versione 1810, questo livello include i dati seguenti:

- Informazioni sulla pianificazione di valutazione delle regole di distribuzione automatiche  

- Riepilogo dell'integrità ATP  

- Statistiche di valutazione e aggiornamento delle raccolte  

- Statistiche dei criteri di conformità per la conformità e gli errori  

- Impostazioni di conformità: dettagli di configurazione SCEP, VPN, Wi-Fi e del modello dei criteri di conformità  

- Utilizzo del pacchetto di configurazione DCM per Configuration Manager  

- Errori di installazione della distribuzione client dettagliati  

- Riepilogo dell'integrità di Endpoint Protection: numero di client protetti, a rischio, sconosciuti e non supportati  

- Configurazione dei criteri di Endpoint Protection  

- Elenco dei processi configurati con il comportamento di installazione per le applicazioni  

- Numero minimo/massimo/medio di ore dall'ultima analisi di aggiornamenti software  

- Numero minimo/massimo/medio dei client inattivi nelle raccolte di distribuzioni di aggiornamenti software  

- Numero minimo/massimo/medio di aggiornamenti software per ogni gruppo  

- Statistiche di distribuzione dei codici prodotto MSI  

- Conformità generale delle distribuzioni degli aggiornamenti software  

- Numero di gruppi con aggiornamenti software scaduti  

- Codici e numero di errori di distribuzione degli aggiornamenti software  

- Informazioni sulla distribuzione degli aggiornamenti software: percentuale di distribuzioni assegnate con client o ora UTC, aggiornamento obbligatorio o facoltativo ed eliminazione del riavvio  

- Prodotti di aggiornamento software sincronizzati dal punto di aggiornamento software  

- Percentuali di analisi dell'aggiornamento software con esito positivo  

- Prime 50 CPU dell'ambiente  

- Tipo di criteri di accesso condizionale di Exchange Active Sync (EAS) (blocco o quarantena) per i dispositivi gestiti da Microsoft Intune  

- Dettagli delle applicazioni di Microsoft Store per le aziende: elenco non aggregato di applicazioni sincronizzate, che include l'ID dell'app, stato online o offline e numero totale di licenze acquistate  

- ***[Nuovo]*** Conteggio dei client di cui è stato eseguito il push con l'opzione per non consentire il fallback a NTLM  
