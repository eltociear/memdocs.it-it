---
title: Impostazioni dei criteri relativi all'antivirus in Windows 10 per Microsoft Defender Antivirus per Intune | Microsoft Docs
description: Visualizzare l'elenco delle impostazioni nel profilo di Microsoft Defender Antivirus per Windows 10. È possibile configurare queste impostazioni nell'ambito dei criteri antivirus per la sicurezza degli endpoint in Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/05/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 7d8ea221b6c1768055e3ca1839c20ed64e2e3838
ms.sourcegitcommit: 14d7dd0a99ebd526c9274d5781c298c828323ebf
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82802022"
---
# <a name="settings-for-windows-10-microsoft-defender-antivirus-policy-in-microsoft-intune"></a>Impostazioni per i criteri di Microsoft Defender Antivirus per Windows 10 in Microsoft Intune

Consente di visualizzare le impostazioni dei criteri antivirus configurabili per il profilo di Microsoft Defender Antivirus per Windows 10 in Microsoft Intune.

## <a name="cloud-protection"></a>Protezione cloud

- **Attiva la protezione fornita dal cloud**  
  CSP: [AllowCloudProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

  Per impostazione predefinita, nei dispositivi Windows 10 desktop Defender invia informazioni a Microsoft in merito a eventuali problemi riscontrati. Le informazioni vengono analizzate per acquisire altre informazioni sui problemi riscontrati dall'utente e da altri clienti e offrire soluzioni migliorate.

  - **Non configurata** (*impostazione predefinita*): l'impostazione viene ripristinata sul valore predefinito di sistema.
  - **No**: l'impostazione è disabilitata. Gli utenti dei dispositivi non possono modificare questa impostazione.
  - **Sì**: la protezione fornita dal cloud è attiva.  Gli utenti dei dispositivi non possono modificare questa impostazione.

- **Livello di protezione fornita dal cloud**  
  CSP: [CloudBlockLevel](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-cloudblocklevel)

  Consente di configurare l'aggressività con cui Defender Antivirus deve bloccare e analizzare i file sospetti.
  - **Non configurata** (*impostazione predefinita*): livello di blocco predefinito di Defender.
  - **Alta**: blocco aggressivo degli elementi sconosciuti e ottimizzazione delle prestazioni del client, con una maggiore probabilità di falsi positivi.
  - **Alta +** : blocco aggressivo degli elementi sconosciuti, con misure di protezione aggiuntive che possono influire sulle prestazioni del client.
  - **Tolleranza zero**: blocco di tutti i file eseguibili sconosciuti.

- **Defender - Timeout esteso per il cloud in secondi**  
  CSP: [CloudExtendedTimeout](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-cloudextendedtimeout)

  Defender Antivirus blocca automaticamente i file sospetti per 10 secondi, in modo da poter analizzare i file nel cloud e assicurarsi che siano sicuri. Con questa impostazione è possibile aggiungere fino a 50 secondi a questo timeout.

## <a name="microsoft-defender-antivirus-exclusions"></a>Esclusioni di Antivirus Microsoft Defender

Per ogni impostazione in questo gruppo, è possibile espandere l'impostazione, selezionare **Aggiungi** e quindi specificare un valore per l'esclusione.

- **Defender - Processi da escludere**  
  CSP: [ExcludedProcesses](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-excludedprocesses)

  Consente di specificare un elenco di file aperti dai processi da ignorare durante un'analisi. Il processo stesso non viene escluso dall'analisi.

- **Estensioni di file da escludere dalle analisi e dalla protezione in tempo reale**  
  CSP: [ExcludedExtensions](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-excludedextensions)

  Consente di specificare un elenco di estensioni di tipi di file da ignorare durante un'analisi.

- **Defender - File e cartelle da escludere**  
  CSP: [ExcludedPaths](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-excludedpaths)

  Consente di specificare un elenco di file e percorsi di directory da ignorare durante un'analisi.

## <a name="real-time-protection"></a>Protezione in tempo reale

- **Attiva protezione in tempo reale**  
  CSP: [AllowRealtimeMonitoring](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring)

  Richiede che nei dispositivi desktop Windows 10 Defender usi la funzionalità di monitoraggio in tempo reale.
  - **Non configurata** (*impostazione predefinita*): l'impostazione viene ripristinata sul valore predefinito di sistema
  - **No**: l'impostazione è disabilitata. Gli utenti dei dispositivi non possono modificare questa impostazione.
  - **Sì**: impone l'uso del monitoraggio in tempo reale. Gli utenti dei dispositivi non possono modificare questa impostazione.

- **Abilita la protezione sempre attiva**  
  CSP: [AllowOnAccessProtection](https://go.microsoft.com/fwlink/?linkid=2113935)

  Consente di configurare la protezione da virus come continuamente attiva, invece che su richiesta.

  - **Non configurata** (*impostazione predefinita*): questo criterio non modifica lo stato di questa impostazione in un dispositivo. Lo stato esistente nel dispositivo rimane invariato.
  - **No**: blocca la protezione sempre attiva nei dispositivi. Gli utenti dei dispositivi non possono modificare questa impostazione.
  - **Sì**: nei dispositivi è attiva la protezione sempre attiva.

- **Monitoraggio dei file in ingresso e in uscita**  
  CSP: [Defender/RealTimeScanDirection](https://go.microsoft.com/fwlink/?linkid=2113943)

  Configurare questa impostazione per determinare quale attività di file e programmi NTFS viene monitorata.
  - **Monitora tutti i file** (*impostazione predefinita*)
  - **Monitora solo i file in ingresso**
  - **Monitora solo i file in uscita**

- **Attiva monitoraggio comportamento**  
  CSP: [AllowBehaviorMonitoring](https://go.microsoft.com/fwlink/?linkid=2114048)

  Per impostazione predefinita, nei dispositivi desktop Windows 10 Defender usa la funzionalità Monitoraggio comportamento.

  - **Non configurata** (*impostazione predefinita*): l'impostazione viene ripristinata sul valore predefinito di sistema.
  - **No**: l'impostazione è disabilitata. Gli utenti dei dispositivi non possono modificare questa impostazione.
  - **Sì**: impone l'uso del monitoraggio del comportamento in tempo reale. Gli utenti dei dispositivi non possono modificare questa impostazione.

- **Attiva la protezione di rete**  
  CSP: [EnableNetworkProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection)

  Protegge gli utenti dei dispositivi durante l'uso di qualsiasi app da tentativi di phishing, da siti che ospitano exploit e da contenuto dannoso su Internet. La protezione impedisce anche ai browser di terze parti di connettersi a siti pericolosi.

  - **Non configurata** (*impostazione predefinita*): l'impostazione viene ripristinata sul valore predefinito di sistema.
  - **No**: l'impostazione è disabilitata. Gli utenti dei dispositivi non possono modificare questa impostazione.
  - **Sì**: la protezione di rete è attivata. Gli utenti dei dispositivi non possono modificare questa impostazione.

- **Analizza tutti i file e gli allegati scaricati**  
  CSP: [EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=2113939)

  Consente di configurare Defender per l'analisi di tutti i file e di tutti gli allegati scaricati.

  - **Non configurata** (*impostazione predefinita*): l'impostazione viene ripristinata sul valore predefinito di sistema.
  - **No**: l'impostazione è disabilitata. Gli utenti dei dispositivi non possono modificare questa impostazione.
  - **Sì**: Defender analizza tutti i file e tutti gli allegati scaricati. Gli utenti dei dispositivi non possono modificare questa impostazione.

- **Analizza gli script usati nei browser Microsoft**  
  CSP: [AllowScriptScanning](https://go.microsoft.com/fwlink/?linkid=2114054)

  Consente di configurare Defender in modo che analizzi gli script.

  - **Non configurata** (*impostazione predefinita*): l'impostazione viene ripristinata sul valore predefinito di sistema.
  - **No**: l'impostazione è disabilitata. Gli utenti dei dispositivi non possono modificare questa impostazione.
  - **Sì**: Defender analizza gli script. Gli utenti dei dispositivi non possono modificare questa impostazione.

- **Analizza file di rete**  
  CSP: [AllowScanningNetworkFiles](https://go.microsoft.com/fwlink/?linkid=2114049&)

  Consente di configurare Defender in modo che analizzi i file di rete.

  - **Non configurata** (*impostazione predefinita*): l'impostazione viene ripristinata sul valore predefinito di sistema.
  - **No**: l'impostazione è disabilitata. Gli utenti dei dispositivi non possono modificare questa impostazione.
  - **Sì**: attiva l'analisi dei file di rete. Gli utenti dei dispositivi non possono modificare questa impostazione.

- **Analizza i messaggi di posta elettronica**  
  CSP: [AllowEmailScanning](https://go.microsoft.com/fwlink/?linkid=2114052)

  Consente di configurare Defender in modo che analizzi la posta in arrivo.

  - **Non configurata** (*impostazione predefinita*): l'impostazione viene ripristinata sul valore predefinito di sistema.
  - **No**: l'impostazione è disabilitata. Gli utenti dei dispositivi non possono modificare questa impostazione.
  - **Sì**: attiva l'analisi della posta elettronica. Gli utenti dei dispositivi non possono modificare questa impostazione.

## <a name="remediation"></a>Soluzione

- **Numero di giorni (0-90) per la conservazione del malware in quarantena**  
  CSP: [DaysToRetainCleanedMalware](https://go.microsoft.com/fwlink/?linkid=2114055)

  Specificare il numero di giorni, da zero a 90, per i quali il sistema deve archiviare gli elementi in quarantena prima della loro rimozione automatica. Il valore zero mantiene gli elementi in quarantena e non li rimuove automaticamente.

- **Invia il consenso per i campioni**  

  - **Non configurato** (*impostazione predefinita*)
  - **Invia i campioni sicuri automaticamente**
  - **Chiedi sempre conferma**
  - **Non inviare mai**
  - **Invia tutti i campioni automaticamente**

- **Azione da eseguire in app potenzialmente indesiderate**  
  CSP: [PUAProtection](https://go.microsoft.com/fwlink/?linkid=2114051)

  Consente di specificare il livello di rilevamento per le applicazioni potenzialmente indesiderate (PUA, Potentially Unwanted Application). Defender avvisa gli utenti quando è in corso il download o il tentativo di installazione di software potenzialmente indesiderato in un dispositivo.

  - **Non configurata** (*impostazione predefinita*): l'impostazione viene ripristinata sul valore predefinito di sistema, ovvero la disattivazione della protezione PUA.
  - **Disabilitato**
  - **Abilita**: gli elementi rilevati vengono bloccati e visualizzati nella cronologia insieme ad altre minacce.
  - **Modalità di controllo**: Defender rileva le applicazioni potenzialmente indesiderate, ma non esegue alcuna azione. È possibile esaminare le informazioni sulle applicazioni per cui Defender avrebbe intrapreso un'azione cercando gli eventi creati in Visualizzatore eventi da Defender.

- **Azioni per le minacce rilevate**  
  CSP: [ThreatSeverityDefaultAction](https://go.microsoft.com/fwlink/?linkid=2113938)

  Consente di specificare l'azione che deve essere eseguita da Defender per il malware rilevato in base al livello di minaccia del malware.
  
  Defender classifica il malware rilevato in base a uno dei livelli di gravità seguenti:
  - **Gravità bassa**
  - **Gravità moderata**
  - **Gravità alta**
  - **Gravità elevata**

  Per ogni livello, specificare l'azione da eseguire. L'impostazione predefinita per ogni livello di gravità è *Non configurata*.

  - **Non configurato**
  - **Pulizia**: il servizio tenta di ripristinare e disinfettare i file.
  - **Quarantena**: sposta i file in quarantena.
  - **Rimozione**: rimuove i file dal dispositivo.
  - **Consentire**: consente il file e non esegue altre azioni.
  - **Definito dall'utente**: l'azione da eseguire viene decisa dall'utente del dispositivo.
  - **Blocco**: blocca l'esecuzione del file.

## <a name="scan"></a>Analisi

- **Analizza file di archivio**  
  CSP: [AllowArchiveScanning](https://go.microsoft.com/fwlink/?linkid=2114047)

  Configura Defender per l'analisi dei file di archivio, ad esempio i file ZIP o CAB.

  - **Non configurata** (*impostazione predefinita*): l'impostazione torna all'impostazione predefinita del client, ovvero all'analisi dei file archiviati, ma può essere disabilitata dall'utente.
Altre informazioni
  - **No**: i file di archivio non vengono esaminati. Gli utenti dei dispositivi non possono modificare questa impostazione.
  - **Sì**: abilita l'analisi dei file di archivio. Gli utenti dei dispositivi non possono modificare questa impostazione.

- **Usa la priorità CPU bassa per le analisi pianificate**  
  CSP: [EnableLowCPUPriority](https://go.microsoft.com/fwlink/?linkid=2113944)

  Configura la priorità della CPU per le analisi pianificate.
  - **Non configurata** (*impostazione predefinita*): l'impostazione torna al valore predefinito di sistema, secondo il quale la priorità della CPU non viene modificata.
  - **No**: l'impostazione è disabilitata. Gli utenti dei dispositivi non possono modificare questa impostazione.
  - **Sì**: per le analisi pianificate la priorità usata per la CPU è bassa. Gli utenti dei dispositivi non possono modificare questa impostazione.

- **Disabilita l'analisi completa di recupero**  
  CSP: [DisableCatchupFullScan](https://go.microsoft.com/fwlink/?linkid=2114042)

  Consente di configurare le analisi di recupero per le analisi complete pianificate. Le analisi di recupero vengono avviate nei casi in cui non è stato possibile eseguire regolarmente un'analisi pianificata. In genere, le analisi pianificate non vengono eseguite perché il computer era spento negli orari in cui dovevano avvenire.

  - **Non configurata** (*impostazione predefinita*): l'impostazione torna al valore predefinito del client, ovvero all'abilitazione delle analisi di recupero per le analisi complete, che tuttavia possono essere disattivate dall'utente.
  - **No**: l'impostazione è disabilitata. Gli utenti dei dispositivi non possono modificare questa impostazione.
  - **Sì**: le analisi di recupero per le analisi complete pianificate vengono imposte e l'utente non può disabilitarle. Se un computer risulta offline per due analisi consecutive pianificate, viene avviata un'analisi di recupero in occasione dell'accesso successivo al computer. Se non è configurata alcuna analisi pianificata, non viene eseguita alcuna analisi di recupero. Gli utenti dei dispositivi non possono modificare questa impostazione.

- **Disabilita l'analisi veloce di recupero**  
  CSP: [DisableCatchupQuickScan](https://go.microsoft.com/fwlink/?linkid=2113941)

  Consente di configurare le analisi di recupero per le analisi veloci pianificate. Le analisi di recupero vengono avviate nei casi in cui non è stato possibile eseguire regolarmente un'analisi pianificata. In genere, le analisi pianificate non vengono eseguite perché il computer era spento negli orari in cui dovevano avvenire.

  - **Non configurata** (*impostazione predefinita*): l'impostazione torna al valore predefinito del client, ovvero all'abilitazione delle analisi veloci di recupero, che tuttavia possono essere disattivate dall'utente.
  - **No**: l'impostazione è disabilitata. Gli utenti dei dispositivi non possono modificare questa impostazione.
  - **Sì**: le analisi di recupero per le analisi veloci pianificate vengono imposte e l'utente non può disabilitarle. Se un computer risulta offline per due analisi consecutive pianificate, viene avviata un'analisi di recupero in occasione dell'accesso successivo al computer. Se non è configurata alcuna analisi pianificata, non viene eseguita alcuna analisi di recupero. Gli utenti dei dispositivi non possono modificare questa impostazione.

- **Limite di utilizzo della CPU per analisi**  
  CSP: [AvgCPULoadFactor](https://go.microsoft.com/fwlink/?linkid=2114046)

  Consente di specificare il fattore di carico medio della CPU per l'analisi di Defender sotto forma di percentuale da zero a 100.

- **Analizza le unità di rete mappate durante un'analisi completa**  
  CSP: [AllowFullScanOnMappedNetworkDrives](https://go.microsoft.com/fwlink/?linkid=2113945)

  Consente di configurare Defender in modo che analizzi le unità di rete mappate.

  - **Non configurata** (*impostazione predefinita*): l'impostazione viene ripristinata sul valore predefinito di sistema, che disabilita l'analisi per le unità di rete mappate.
  - **No**: l'impostazione è disabilitata. Gli utenti dei dispositivi non possono modificare questa impostazione.
  - **Sì**: abilita l'analisi delle unità di rete mappate. Gli utenti dei dispositivi non possono modificare questa impostazione.

- **Esegui l'analisi veloce giornaliera alle ore**  
  CSP: [ScheduleQuickScanTime](https://go.microsoft.com/fwlink/?linkid=2114053)

  Consente di selezionare l'ora del giorno in cui Defender deve eseguire le analisi veloci.
  L'impostazione predefinita corrisponde a **Non configurata**

- **Tipo di analisi**  
  CSP: [ScanParameter](https://go.microsoft.com/fwlink/?linkid=2114045)

  Consente di selezionare il tipo dell'analisi eseguita da Defender.

  - **Non configurata** (*impostazione predefinita*)
  - **Analisi veloce**
  - **Analisi completa**

- **Giorno della settimana per l'esecuzione di un'analisi pianificata**  
  - **Non configurata** (*impostazione predefinita*)

- **Ora del giorno per l'esecuzione di un'analisi pianificata**  
  - **Non configurata** (*impostazione predefinita*)

- **Verifica la disponibilità di aggiornamenti della firma prima dell'esecuzione dell'analisi**  
  - **Non configurata** (*impostazione predefinita*)
  - **No**
  - **Sì**

## <a name="updates"></a>Aggiornamenti

- **Immettere la frequenza (0-24 ore) per il controllo della disponibilità di aggiornamenti dell'intelligence sulla sicurezza**  
  CSP: [SignatureUpdateInterval](https://go.microsoft.com/fwlink/?linkid=2113936)

  Specificare l'intervallo in ore (da zero a 24) da usare per il controllo delle firme. Se il valore è zero, non viene verificata la disponibilità di nuove firme. Se il valore è 2, il controllo viene eseguito ogni due ore e così via.

## <a name="user-experience"></a>Esperienza utente

- **Consenti l'accesso utente all'app Microsoft Defender**  
  CSP: [AllowUserUIAccess](https://go.microsoft.com/fwlink/?linkid=2114043)  

  - **Non configurata** (*impostazione predefinita* ): l'impostazione torna al valore predefinito del client, in base al quale l'interfaccia utente e le notifiche sono consentite.
  - **No**: l'interfaccia utente di Defender non è accessibile e le notifiche sono state eliminate.
  - **Sì**

