---
title: Impostazioni dei criteri antivirus di Microsoft Defender Antivirus in Windows 10 per i dispositivi collegati al tenant | Microsoft Docs
description: Vedere l'elenco delle impostazioni nel profilo di Microsoft Defender Antivirus per i dispositivi Windows 10 gestiti da Configuration Manager. È possibile configurare queste impostazioni nell'ambito dei criteri antivirus di sicurezza degli endpoint in Microsoft Intune dopo aver configurato il collegamento al tenant per Configuration Manager.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/24/2020
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
ms.openlocfilehash: 3bb1d4806271ab40c60f0ad419e4e708d36bbc97
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/31/2020
ms.locfileid: "89194124"
---
# <a name="settings-for-microsoft-defender-antivirus-policy-for-tenant-attached-devices-in-microsoft-intune"></a>Impostazioni dei criteri di Microsoft Defender Antivirus per i dispositivi collegati al tenant in Microsoft Intune

Visualizzare le impostazioni di Microsoft Defender Antivirus che è possibile gestire con il profilo dei **criteri di Microsoft Defender Antivirus (ConfigMgr)** da Intune. Il profilo è disponibile quando si configurano i [criteri antivirus di sicurezza degli endpoint](../protect/endpoint-security-antivirus-policy.md) di Intune, che vengono distribuiti ai dispositivi gestiti con Configuration Manager dopo aver configurato lo scenario di [collegamento al tenant](../protect/tenant-attach-intune.md).

## <a name="cloud-protection"></a>Protezione cloud

- **Attiva la protezione fornita dal cloud**  
  CSP: [AllowCloudProtection](/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

  Per impostazione predefinita, nei dispositivi Windows 10 desktop Defender invia informazioni a Microsoft in merito a eventuali problemi riscontrati. Le informazioni vengono analizzate per acquisire altre informazioni sui problemi riscontrati dall'utente e da altri clienti e offrire soluzioni migliorate.

  - **Non configurata** (*impostazione predefinita*): l'impostazione viene ripristinata sul valore predefinito di sistema.
  - **Non consentiti.** Disattivazione di Microsoft Active Protection Service.
  - **Consentito**.  Attivazione di Microsoft Active Protection Service.

- **Livello di protezione fornita dal cloud**  
  CSP: [CloudBlockLevel](/windows/client-management/mdm/policy-csp-defender#defender-cloudblocklevel)

  Consente di configurare l'aggressività con cui Defender Antivirus deve bloccare e analizzare i file sospetti.
  - **Non configurata** (*impostazione predefinita*): livello di blocco predefinito di Defender.
  - **Alta**: blocco aggressivo degli elementi sconosciuti e ottimizzazione delle prestazioni del client, con una maggiore probabilità di falsi positivi.
  - **Alta +** : blocco aggressivo degli elementi sconosciuti, con misure di protezione aggiuntive che possono influire sulle prestazioni del client.
  - **Tolleranza zero**: blocco di tutti i file eseguibili sconosciuti.

- **Defender - Timeout esteso per il cloud in secondi**  
  CSP: [CloudExtendedTimeout](/windows/client-management/mdm/policy-csp-defender#defender-cloudextendedtimeout)

  Defender Antivirus blocca automaticamente i file sospetti per 10 secondi, in modo da poter analizzare i file nel cloud e assicurarsi che siano sicuri. Con questa impostazione è possibile aggiungere fino a 50 secondi a questo timeout.

## <a name="microsoft-defender-antivirus-exclusions"></a>Esclusioni di Antivirus Microsoft Defender

Per ogni impostazione in questo gruppo, è possibile espandere l'impostazione, selezionare **Aggiungi** e quindi specificare un valore per l'esclusione.

- **Defender - Processi da escludere**  
  CSP: [ExcludedProcesses](/windows/client-management/mdm/policy-csp-defender#defender-excludedprocesses)

  Consente di specificare un elenco di file aperti dai processi da ignorare durante un'analisi. Il processo stesso non viene escluso dall'analisi.

- **Estensioni di file da escludere dalle analisi e dalla protezione in tempo reale**  
  CSP: [ExcludedExtensions](/windows/client-management/mdm/policy-csp-defender#defender-excludedextensions)

  Consente di specificare un elenco di estensioni di tipi di file da ignorare durante un'analisi.

- **Defender - File e cartelle da escludere**  
  CSP: [ExcludedPaths](/windows/client-management/mdm/policy-csp-defender#defender-excludedpaths)

  Consente di specificare un elenco di file e percorsi di directory da ignorare durante un'analisi.

## <a name="real-time-protection"></a>Protezione in tempo reale

- **Attiva protezione in tempo reale**  
  CSP: [AllowRealtimeMonitoring](/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring)

  Richiede che nei dispositivi desktop Windows 10 Defender usi la funzionalità di monitoraggio in tempo reale.
  - **Non configurata** (*impostazione predefinita*): l'impostazione viene ripristinata sul valore predefinito di sistema
  - **Non consentiti.** Disattivazione del servizio di monitoraggio in tempo reale.di monitoraggio in tempo reale.
  - **Consentito**. Attivazione ed esecuzione del servizio di monitoraggio in tempo reale.

- **Abilita la protezione sempre attiva**  
  CSP: [AllowOnAccessProtection](https://go.microsoft.com/fwlink/?linkid=2113935)

  Consente di configurare la protezione da virus come continuamente attiva, invece che su richiesta.

  - **Non configurata** (*impostazione predefinita*): questo criterio non modifica lo stato di questa impostazione in un dispositivo. Lo stato esistente nel dispositivo rimane invariato.
  - **Non consentiti.** Disattivazione del servizio di monitoraggio in tempo reale.di monitoraggio in tempo reale.
  - **Consentito**.

- **Monitoraggio dei file in ingresso e in uscita**  
  CSP: [Defender/RealTimeScanDirection](https://go.microsoft.com/fwlink/?linkid=2113943)

  Configurare questa impostazione per determinare quale attività di file e programmi NTFS viene monitorata.
  - **Monitora tutti i file (bidirezionale).** (*impostazione predefinita*)
  - **Monitora i file in ingresso.**
  - **Monitora i file in uscita.**

- **Attiva monitoraggio comportamento**  
  CSP: [AllowBehaviorMonitoring](https://go.microsoft.com/fwlink/?linkid=2114048)

  Per impostazione predefinita, nei dispositivi desktop Windows 10 Defender usa la funzionalità Monitoraggio comportamento.

  - **Non configurata** (*impostazione predefinita*): l'impostazione viene ripristinata sul valore predefinito di sistema.
  - **Non consentiti.** Disattivazione del monitoraggio del comportamento.
  - **Consentito**. Attivazione del monitoraggio del comportamento in tempo reale.

- **Consenti il sistema di prevenzione intrusioni**  
  - **Non configurata** (*impostazione predefinita*): l'impostazione viene ripristinata sul valore predefinito di sistema.
  - **Non consentiti.**
  - **Consentito**.

- **Analizza tutti i file e gli allegati scaricati**  
  CSP: [EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=2113939)

  Consente di configurare Defender per l'analisi di tutti i file e di tutti gli allegati scaricati.

  - **Non configurata** (*impostazione predefinita*): l'impostazione viene ripristinata sul valore predefinito di sistema.
  - **Non consentiti.**
  - **Consentito**.

- **Analizza gli script usati nei browser Microsoft**  
  CSP: [AllowScriptScanning](https://go.microsoft.com/fwlink/?linkid=2114054)

  Consente di configurare Defender in modo che analizzi gli script.

  - **Non configurata** (*impostazione predefinita*): l'impostazione viene ripristinata sul valore predefinito di sistema.
  - **Non consentiti.**
  - **Consentito**.

- **Analizza file di rete**  
  CSP: [AllowScanningNetworkFiles](https://go.microsoft.com/fwlink/?linkid=2114049&)

  Consente di configurare Defender in modo che analizzi i file di rete.

  - **Non configurata** (*impostazione predefinita*): l'impostazione viene ripristinata sul valore predefinito di sistema.
  - **Non consentiti.** Disattivazione dell'analisi dei file di rete.
  - **Consentito**. Analisi dei file di rete.

- **Analizza i messaggi di posta elettronica**  
  CSP: [AllowEmailScanning](https://go.microsoft.com/fwlink/?linkid=2114052)

  Consente di configurare Defender in modo che analizzi la posta in arrivo.

  - **Non configurata** (*impostazione predefinita*): l'impostazione viene ripristinata sul valore predefinito di sistema.
  - **Non consentiti.** Disattivazione dell'analisi dei messaggi di posta elettronica.
  - **Consentito**. Attivazione dell'analisi dei messaggi di posta elettronica.

## <a name="remediation"></a>Soluzione

- **Numero di giorni (0-90) per la conservazione del malware in quarantena**  
  CSP: [DaysToRetainCleanedMalware](https://go.microsoft.com/fwlink/?linkid=2114055)

  Specificare il numero di giorni, da zero a 90, per i quali il sistema deve archiviare gli elementi in quarantena prima della loro rimozione automatica. Il valore zero mantiene gli elementi in quarantena e non li rimuove automaticamente.

- **Invia il consenso per i campioni**  

  - **Non configurato** (*impostazione predefinita*)
  - **Conferma sempre necessaria.**
  - **Invio automatico dei campioni sicuri.**
  - **Non inviare mai.**
  - **Invio automatico di tutti i campioni.**

- **Azione da eseguire in app potenzialmente indesiderate**  
  CSP: [PUAProtection](https://go.microsoft.com/fwlink/?linkid=2114051)

  Consente di specificare il livello di rilevamento per le applicazioni potenzialmente indesiderate (PUA, Potentially Unwanted Application). Defender avvisa gli utenti quando è in corso il download o il tentativo di installazione di software potenzialmente indesiderato in un dispositivo.

  - **Non configurata** (*impostazione predefinita*): l'impostazione viene ripristinata sul valore predefinito di sistema, ovvero la disattivazione della protezione PUA.
  - **La Protezione PUA è disattivata.** Windows Defender non proteggerà da applicazioni potenzialmente indesiderate.
  - **La Protezione PUA è attivata.** Gli elementi rilevati vengono bloccati. Verranno visualizzati nella cronologia insieme alle altre minacce.
  - **Modalità di controllo.** Defender rileverà le applicazioni potenzialmente indesiderate, ma non eseguirà alcuna azione. È possibile esaminare le informazioni sulle applicazioni per cui Defender avrebbe intrapreso un'azione cercando gli eventi creati in Visualizzatore eventi da Defender.

- **Crea un punto di ripristino di sistema prima di eseguire la pulizia dei computer**  
  - **Sì** (*impostazione predefinita*)
  - **No**
  - **Non configurato**

- **Azioni per le minacce rilevate**  
  CSP: [ThreatSeverityDefaultAction](https://go.microsoft.com/fwlink/?linkid=2113938)

  Consente di specificare l'azione che deve essere eseguita da Defender per il malware rilevato in base al livello di minaccia del malware.
  
  Defender classifica il malware rilevato in base a uno dei livelli di gravità seguenti:
  - **Minaccia bassa**
  - **Minaccia moderata**
  - **Minaccia elevata**
  - **Minaccia grave**

  Per ogni livello, specificare l'azione da eseguire. L'impostazione predefinita per ogni livello di gravità è *Non configurata*.

  - **Non configurato** (*impostazione predefinita*)
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
  - **Non consentito** Disattivazione dell'analisi sui file archiviati.
  - **Consentito**. Analisi dei file di archivio.

- **Usa la priorità CPU bassa per le analisi pianificate**  
  CSP: [EnableLowCPUPriority](https://go.microsoft.com/fwlink/?linkid=2113944)

  Configura la priorità della CPU per le analisi pianificate.
  - **Non configurata** (*impostazione predefinita*): l'impostazione torna al valore predefinito di sistema, secondo il quale la priorità della CPU non viene modificata.
  - **Disabilitato**
  - **Enabled**

- **Disabilita l'analisi completa di recupero**  
  CSP: [DisableCatchupFullScan](https://go.microsoft.com/fwlink/?linkid=2114042)

  Consente di configurare le analisi di recupero per le analisi complete pianificate. Le analisi di recupero vengono avviate nei casi in cui non è stato possibile eseguire regolarmente un'analisi pianificata. In genere, le analisi pianificate non vengono eseguite perché il computer era spento negli orari in cui dovevano avvenire.

  - **Non configurata** (*impostazione predefinita*): l'impostazione torna al valore predefinito del client, ovvero all'abilitazione delle analisi di recupero per le analisi complete, che tuttavia possono essere disattivate dall'utente.
  - **Disabilitato**
  - **Enabled**

- **Disabilita l'analisi veloce di recupero**  
  CSP: [DisableCatchupQuickScan](https://go.microsoft.com/fwlink/?linkid=2113941)

  Consente di configurare le analisi di recupero per le analisi veloci pianificate. Le analisi di recupero vengono avviate nei casi in cui non è stato possibile eseguire regolarmente un'analisi pianificata. In genere, le analisi pianificate non vengono eseguite perché il computer era spento negli orari in cui dovevano avvenire.

  - **Non configurata** (*impostazione predefinita*): l'impostazione torna al valore predefinito del client, ovvero all'abilitazione delle analisi veloci di recupero, che tuttavia possono essere disattivate dall'utente.
  - **Disabilitato**
  - **Enabled**

- **Limite di utilizzo della CPU (0-100%) per analisi**  
  CSP: [AvgCPULoadFactor](https://go.microsoft.com/fwlink/?linkid=2114046)

  Consente di specificare il fattore di carico medio della CPU per l'analisi di Defender sotto forma di percentuale da zero a 100.

- **Abilitazione dell'analisi delle unità di rete mappate durante un'analisi completa**  
  CSP: [AllowFullScanOnMappedNetworkDrives](https://go.microsoft.com/fwlink/?linkid=2113945)

  Consente di configurare Defender in modo che analizzi le unità di rete mappate.

  - **Non configurata** (*impostazione predefinita*): l'impostazione viene ripristinata sul valore predefinito di sistema, che disabilita l'analisi per le unità di rete mappate.
  - **Non consentiti.** Disabilitazione dell'analisi delle unità di rete mappate.
  - **Consentito**. Analisi delle unità di rete mappate.

- **Esegui l'analisi veloce giornaliera alle ore**  
  CSP: [ScheduleQuickScanTime](https://go.microsoft.com/fwlink/?linkid=2114053)

  Consente di selezionare l'ora del giorno in cui Defender deve eseguire le analisi veloci.
  Per impostazione predefinita, questa opzione è **Non configurata**

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
  - **Disabilitato**
  - **Enabled**

- **Scegli in modo casuale gli orari di inizio delle analisi pianificate e degli aggiornamenti dell'intelligence per la sicurezza**  
  -**Non configurata** (*impostazione predefinita*) -**Sì**
  -**No**

- **Analizza le unità rimovibili durante un'analisi completa**
  - **Non configurata** (*impostazione predefinita*)
  - **Non consentiti.** Disattivazione dell'analisi sulle unità rimovibili.
  - **Consentito**. Analisi delle unità rimovibili.

## <a name="updates"></a>Aggiornamenti

- **Immettere la frequenza (0-24 ore) per il controllo della disponibilità di aggiornamenti dell'intelligence sulla sicurezza**  
  CSP: [SignatureUpdateInterval](https://go.microsoft.com/fwlink/?linkid=2113936)

  Specificare l'intervallo in ore (da zero a 24) da usare per il controllo delle firme. Se il valore è zero, non viene verificata la disponibilità di nuove firme. Se il valore è 2, il controllo viene eseguito ogni due ore e così via.

- **Aggiornamento della firma - Ordine di fallback (dispositivo)**

- **Aggiornamento della firma - Origini delle condivisioni file (dispositivo)**

- **Posizione dell'intelligence sulla sicurezza (dispositivo)**  

## <a name="user-experience"></a>Esperienza utente

- **Blocca l'accesso utente all'app Microsoft Defender**  
  - **Non configurata** (*impostazione predefinita*)
  - **Non consentiti.** Blocco dell'accesso degli utenti all'interfaccia utente.
  - **Consentito**. Utenti autorizzati ad accedere all'interfaccia utente.

- **Mostra i messaggi di notifica nel computer client quando l'utente deve eseguire un'analisi completa, aggiornare l'intelligence per la sicurezza o eseguire Windows Defender Offline**  
  - **Non configurata** (*impostazione predefinita*)
  - **Sì**
  - **No**

- **Disabilita l'interfaccia utente client**  
  - **Non configurata** (*impostazione predefinita*)
  - **Sì**
  - **No**

- **Consenti agli utenti di visualizzare i risultati completi della Cronologia**
  - **Non configurata** (*impostazione predefinita*)
  - **Sì**
  - **No**