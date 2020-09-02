---
title: Impostazioni di riduzione della superficie di attacco nella sicurezza degli endpoint di Intune | Microsoft Docs
description: Impostazioni dei criteri di riduzione della superficie di attacco nella sicurezza degli endpoint di Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/11/2020
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
ms.openlocfilehash: a2b404e1741c93a6dbf5023f394f3b9528020617
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/26/2020
ms.locfileid: "88913461"
---
# <a name="attack-surface-reduction-policy-settings-for-endpoint-security-in-intune"></a>Impostazioni dei criteri di riduzione della superficie di attacco nella sicurezza degli endpoint di Intune

Visualizzare le impostazioni che è possibile configurare nei profili per i criteri di *riduzione della superficie di attacco* nel nodo Sicurezza degli endpoint di Intune come parte dei [criteri di sicurezza degli endpoint](../protect/endpoint-security-policy.md).

Piattaforme e profili supportati:

- **Windows 10 e versioni successive**:
  - Profilo: **Isolamento di app e browser**
  - Profilo: **Protezione Web**
  - Profilo: **Controllo applicazione**
  - Profilo: **Regole per la riduzione della superficie di attacco**
  - Profilo: **Controllo del dispositivo**
  - Profilo: **Protezione dagli exploit**

## <a name="app-and-browser-isolation-profile"></a>Profilo Isolamento di app e browser

### <a name="app-and-browser-isolation"></a>Isolamento di app e browser

- **Attiva Application Guard per Microsoft Edge (opzioni)**  
  CSP: [Settings/AllowWindowsDefenderApplicationGuard](https://go.microsoft.com/fwlink/?linkid=872350)

  - **Non configurato** (*impostazione predefinita*)
  - **Abilitato per Microsoft Edge** - Application Guard apre siti non approvati in un contenitore di esplorazione virtualizzato di Hyper-V.

  Con l'opzione *Abilitato per Microsoft Edge* sono disponibili le impostazioni seguenti:
  
  - **Comportamento degli Appunti**  
    CSP: [ClipboardSettings](https://go.microsoft.com/fwlink/?linkid=872351)

    Consente di scegliere le azioni di copia e incolla consentite tra il computer locale e un browser virtuale di Application Guard.
    - **Non configurato** (*impostazione predefinita*)
    - **Blocca copia e incolla tra computer e browser**
    - **Consenti copia e incolla solo dal browser al computer**
    - **Consenti copia e incolla solo dal computer al browser**
    - **Consenti copia e incolla tra computer e browser**

  - **Blocca i contenuti esterni da siti approvati non aziendali**  
    CSP: [BlockNonEnterpriseContent](https://go.microsoft.com/fwlink/?linkid=872352)

    - **Non configurato** (*impostazione predefinita*)
    - **Sì** - Impedisce il caricamento del contenuto dai siti Web non approvati.

  - **Raccogli i log per gli eventi che si verificano in una sessione di esplorazione di Application Guard**  
    CSP: [AuditApplicationGuard](https://go.microsoft.com/fwlink/?linkid=872418)

    - **Non configurato** (*impostazione predefinita*)
    - **Sì** - Consente di raccogliere log per gli eventi che si verificano in una sessione del browser virtuale di Application Guard.

  - **Allow user-generated browser data to be saved** (Consenti il salvataggio dei dati del browser generati dall'utente)  
    CSP: [AllowPersistence](https://go.microsoft.com/fwlink/?linkid=872419)

    - **Non configurato** (*impostazione predefinita*)
    - **Sì** - Consente di salvare i dati utente creati durante una sessione di esplorazione virtuale di Application Guard. Sono esempi di dati utente le password, i preferiti e i cookie.

  - **Abilita l'accelerazione grafica hardware**  
    CSP: [AllowVirtualGPU](https://go.microsoft.com/fwlink/?linkid=872420)

    - **Non configurato** (*impostazione predefinita*)
    - **Sì** - In una sessione del browser virtuale di Application Guard usare un'unità di elaborazione grafica virtuale per caricare più rapidamente i siti Web con numerosi elementi grafici.

  - **Consenti agli utenti di scaricare i file nell'host**  
    CSP: [SaveFilesToHost](https://go.microsoft.com/fwlink/?linkid=872421)

    - **Non configurato** (*impostazione predefinita*)
    - **Sì** - Consente agli utenti di scaricare file dal browser virtualizzato nel sistema operativo host.

- **Application Guard - Stampa su stampanti locali consentita**  

  - **Non configurato** (*impostazione predefinita*)
  - **Sì** - Stampa su stampanti locali consentita.

- **Application Guard - Stampa su stampanti di rete consentita**  

  - **Non configurato** (*impostazione predefinita*)
  - **Sì** - Consente la stampa sulle stampanti di rete.

- **Application Guard - Stampa su PDF consentita**  

  - **Non configurato** (*impostazione predefinita*)
  - **Sì** - Consente la stampa in formato PDF.

- **Application Guard - Stampa su XPS consentita**  

  - **Non configurato** (*impostazione predefinita*)
  - **Sì** - Consente la stampa in formato XPS.

- **Criterio di isolamento della rete Windows**  
  
  - **Non configurato** (*impostazione predefinita*)
  - **Sì** - Consente di configurare il criterio di isolamento della rete Windows.  
  
  Se impostata su *Sì*, è possibile configurare le impostazioni seguenti.

  - **Intervalli IP**  
    Espandere l'elenco a discesa, selezionare **Aggiungi** e specificare un *Indirizzo inferiore* e un *Indirizzo superiore*.

  - **Risorse cloud**  
    Espandere l'elenco a discesa, selezionare **Aggiungi** e specificare un *Indirizzo IP o FQDN* e un *Proxy*.

  - **Domini di rete**  
   Espandere l'elenco a discesa, selezionare **Aggiungi** e specificare *Domini di rete*.

  - **Server proxy**  
    Espandere l'elenco a discesa, selezionare **Aggiungi** e specificare *Server proxy*.

  - **Server proxy interni**  
    Espandere l'elenco a discesa, selezionare **Aggiungi** e specificare *Server proxy interni*.

  - **Risorse neutre**  
    Espandere l'elenco a discesa, selezionare **Aggiungi** e specificare *Risorse neutre*.

  - **Disabilita il rilevamento automatico di altri server proxy aziendali**  
    - **Non configurato** (*impostazione predefinita*)
    - **Sì** - Disabilita il rilevamento automatico di altri server proxy aziendali.

  - **Disabilita il rilevamento automatico di altri intervalli di indirizzi IP aziendali**  
    - **Non configurato** (*impostazione predefinita*)
    - **Sì** - Disabilita il rilevamento automatico di altri intervalli di indirizzi IP aziendali.

## <a name="web-protection-profile"></a>Profilo di protezione Web

### <a name="web-protection"></a>Protezione Web

- **Abilita la protezione di rete**  
  CSP: [EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=872618)

  - **Non configurato** (*impostazione predefinita*) - Viene ripristinata l'impostazione predefinita di Windows, ovvero disattivato.
  - **Definito dall'utente**
  - **Abilita** - La protezione della rete è abilitata per tutti gli utenti del sistema.
  - **Modalità di controllo** - Gli utenti non vengono protetti da domini pericolosi e vengono invece generati eventi di Windows.

- **Richiedere SmartScreen per Microsoft Edge**  
  CSP: [Browser/AllowSmartScreen](https://go.microsoft.com/fwlink/?linkid=2067029)

  - **Sì** - Usare SmartScreen per proteggere gli utenti da potenziali tentativi di phishing e da software dannoso.
  - **Non configurato** (*impostazione predefinita*)

- **Bloccare l'accesso a siti dannosi**  
  CSP: [Browser/PreventSmartScreenPromptOverride](https://go.microsoft.com/fwlink/?linkid=2067040)  

  - **Sì** - Impedisce agli utenti di ignorare gli avvisi del filtro Microsoft Defender SmartScreen e di accedere al sito.
  - **Non configurato** (*impostazione predefinita*)

- **Bloccare il download di file non verificati**  
  CSP: [Browser/PreventSmartScreenPromptOverrideForFiles](https://go.microsoft.com/fwlink/?linkid=2067023)  

  - **Sì** - Impedisce agli utenti di ignorare gli avvisi del filtro Microsoft Defender SmartScreen e di scaricare file non verificati.
  - **Non configurato** (*impostazione predefinita*)

## <a name="application-control-profile"></a>Profilo Controllo applicazione

### <a name="microsoft-defender-application-control"></a>Controllo di applicazioni di Microsoft Defender

- **Controllo applicazione di App Locker**  
  CSP: [AppLocker](/windows/client-management/mdm/applocker-csp)

  - **Non configurato** (*impostazione predefinita*)
  - **Imponi i componenti e le app dello Store**
  - **Controlla i componenti e le app dello Store**
  - **Imponi i componenti, le app dello Store e Smartlocker**
  - **Controlla i componenti, le app dello Store e Smartlocker**
   

- **Impedisci agli utenti di ignorare gli avvisi di SmartScreen**  
  CSP: [SmartScreen/PreventOverrideForFilesInShell](https://go.microsoft.com/fwlink/?linkid=872783)

  - **Non configurato**  (*impostazione predefinita*) - Gli utenti possono ignorare gli avvisi di SmartScreen per i file e le app dannose.
  - **Sì** - SmartScreen è abilitato e gli utenti non possono ignorare gli avvisi per i file o le app dannose.

- **Attiva Windows SmartScreen**  
  CSP: [SmartScreen/EnableSmartScreenInShell](https://go.microsoft.com/fwlink/?linkid=872784)

  - **Non configurato** (*impostazione predefinita*) - Viene ripristinata l'impostazione predefinita di Windows che prevede l'abilitazione di SmartScreen, tuttavia gli utenti possono modificare questa impostazione. Per disabilitare SmartScreen, usare un URI personalizzato.
  - **Sì** - Impone l'uso di SmartScreen per tutti gli utenti.

## <a name="attack-surface-reduction-rules-profile"></a>Profilo Regole per la riduzione della superficie di attacco

### <a name="attack-surface-reduction-rules"></a>Regole per la riduzione della superficie di attacco

- **Blocca il furto di credenziali dal sottosistema dell'autorità di protezione locale di Windows (lsass.exe)**  
  <!-- Defender ATP security baseline, Device configuration Endpoint protection profile -->
  [Proteggere i dispositivi dagli exploit](https://go.microsoft.com/fwlink/?linkid=874499)

  Questa regola per la riduzione della superficie di attacco (ASR) viene controllata tramite il GUID seguente: 9e6c4e1f-7d60-472f-ba1a-a39ef669e4b2
  - **Non configurato** (*impostazione predefinita*) - Viene ripristinata l'impostazione predefinita di Windows, ovvero disattivato.
  - **Definito dall'utente**
  - **Abilita** - Vengono bloccati i tentativi di furto delle credenziali tramite lsass.exe.
  - **Modalità di controllo** - Gli utenti non vengono protetti da domini pericolosi e vengono invece generati eventi di Windows.

- **Block Adobe Reader from creating child processes** (Impedisci ad Adobe Reader di creare processi figlio)  
  [Ridurre le superfici di attacco con le regole di riduzione della superficie di attacco](https://go.microsoft.com/fwlink/?linkid=853979)
  
  Questa regola di ASR viene controllata tramite il GUID seguente: 7674ba52-37eb-4a4f-a9a1-f0f9a1619a2c
  - **Non configurato** (*impostazione predefinita*) - Viene ripristinata l'impostazione predefinita di Windows che non blocca la creazione di processi figlio.
  - **Definito dall'utente**
  - **Abilita** - La creazione di processi figlio è bloccata da Adobe Reader.
  - **Modalità di controllo** - Vengono generati eventi Windows anziché bloccare i processi figlio.

- **Impedisci alle applicazioni di Office di inserire codice in altri processi**  
  [Proteggere i dispositivi dagli exploit](https://go.microsoft.com/fwlink/?linkid=872974)

  Questa regola di ASR viene controllata tramite il GUID seguente: 75668C1F-73B5-4CF0-BB93-3ECF5CB7CC84
  - **Non configurato** (*impostazione predefinita*) - Viene ripristinata l'impostazione predefinita di Windows, ovvero disattivato.
  - **Blocca** - Le applicazioni di Office non possono inserire codice in altri processi.
  - **Modalità di controllo** - Vengono generati eventi di Windows anziché imporre il blocco.

- **Impedisci alle applicazioni di Office di creare contenuto eseguibile**  
  [Proteggere i dispositivi dagli exploit](https://go.microsoft.com/fwlink/?linkid=872975)

  Questa regola di ASR viene controllata tramite il GUID seguente: 3B576869-A4EC-4529-8536-B80A7769E899
  - **Non configurato** (*impostazione predefinita*) - Viene ripristinata l'impostazione predefinita di Windows, ovvero disattivato.
  - **Blocca** - Viene impedito alle applicazioni Office di creare contenuto eseguibile.
  - **Modalità di controllo** - Vengono generati eventi di Windows anziché imporre il blocco.

- **Impedisci alle applicazioni di Office di creare processi figlio**  
  [Proteggere i dispositivi dagli exploit](https://go.microsoft.com/fwlink/?linkid=872976)

  Questa regola di ASR viene controllata tramite il GUID seguente: D4F940AB-401B-4EFC-AADC-AD5F3C50688A
  - **Non configurato** (*impostazione predefinita*) - Viene ripristinata l'impostazione predefinita di Windows, ovvero disattivato.
  - **Blocca** - Viene impedito alle applicazioni Office di creare processi figlio.
  - **Modalità di controllo** - Vengono generati eventi di Windows anziché imporre il blocco.

- **Blocca le chiamate API Win32 dalle macro di Office**  
  [Proteggere i dispositivi dagli exploit](https://go.microsoft.com/fwlink/?linkid=872977)

  Questa regola di ASR viene controllata tramite il GUID seguente: 92E97FA1-2EDF-4476-BDD6-9DD0B4DDDC7B
  - **Non configurato** (*impostazione predefinita*) - Viene ripristinata l'impostazione predefinita di Windows, ovvero disattivato.
  - **Blocca** - L'uso di chiamate API Win32 è bloccato per le macro di Office.
  - **Modalità di controllo** - Vengono generati eventi di Windows anziché imporre il blocco.

- **Impedisci alle app di comunicazione di Office di creare processi figlio**  
  [Proteggere i dispositivi dagli exploit](https://go.microsoft.com/fwlink/?linkid=874499)  

  Questa regola di ASR viene controllata tramite il GUID seguente: 26190899-1602-49e8-8b27-eb1d0a1ce869.
  - **Non configurato** (*impostazione predefinita*) - Viene ripristinata l'impostazione predefinita di Windows, che non blocca la creazione di processi figlio.
  - **Definito dall'utente**
  - **Abilita** - Le applicazioni di comunicazioni di Office non possono creare processi figlio.
  - **Modalità di controllo** - Vengono generati eventi Windows anziché bloccare i processi figlio.

- **Blocca l'esecuzione di script potenzialmente offuscati (js/vbs/ps)**  
  [Proteggere i dispositivi dagli exploit](https://go.microsoft.com/fwlink/?linkid=872978)

  Questa regola di ASR viene controllata tramite il GUID seguente: 5BEB7EFE-FD9A-4556-801D-275E5FFC04CC
  - **Non configurato** (*impostazione predefinita*) - Viene ripristinata l'impostazione predefinita di Windows, ovvero disattivato.
  - **Blocca** - Defender blocca l'esecuzione degli script offuscati.
  - **Modalità di controllo** - Vengono generati eventi di Windows anziché imporre il blocco.

- **Impedisci a JavaScript o VBScript di avviare contenuto eseguibile scaricato**  
  [Proteggere i dispositivi dagli exploit](https://go.microsoft.com/fwlink/?linkid=872979)

   Questa regola di ASR viene controllata tramite il GUID seguente: D3E037E1-3EB8-44C8-A917-57927947596D
  - **Non configurato** (*impostazione predefinita*) - Viene ripristinata l'impostazione predefinita di Windows, ovvero disattivato.
  - **Blocca** - Defender blocca l'esecuzione dei file JavaScript o VBScript scaricati da Internet.
  - **Modalità di controllo** - Vengono generati eventi di Windows anziché imporre il blocco.

- **Blocca le creazioni di processi generate da comandi PSExec e WMI**  
  [Proteggere i dispositivi dagli exploit](https://go.microsoft.com/fwlink/?linkid=874500)

  Questa regola di ASR viene controllata tramite il GUID seguente: d1e49aac-8f56-4280-b9ba-993a6d77406c
  - **Non configurato** (*impostazione predefinita*) - Viene ripristinata l'impostazione predefinita di Windows, ovvero disattivato.
  - **Blocca** - La creazione del processo tramite PSExec o i comandi WMI viene bloccata.
  - **Modalità di controllo** - Vengono generati eventi di Windows anziché imporre il blocco.

- **Blocca processi non attendibili e non firmati eseguiti da USB**  
  [Proteggere i dispositivi dagli exploit](https://go.microsoft.com/fwlink/?linkid=874502)

  Questa regola di ASR viene controllata tramite il GUID seguente: b2b3f03d-6a65-4F7B-A9C7-1c7ef74a9ba4
  - **Non configurato** (*impostazione predefinita*) - Viene ripristinata l'impostazione predefinita di Windows, ovvero disattivato.
  - **Blocca** - Vengono bloccati i processi non attendibili e non firmati eseguiti da un'unità USB.
  - **Modalità di controllo** - Vengono generati eventi di Windows anziché imporre il blocco.

- **Bloccare l'esecuzione dei file eseguibili se non soddisfano i criteri di prevalenza, età o elenco attendibile**  
  [Proteggere i dispositivi dagli exploit](https://go.microsoft.com/fwlink/?linkid=874503)

  Questa regola di ASR viene controllata tramite il GUID seguente: 01443614-cd74-433a-b99e-2ecdc07bfc25e
  - **Non configurato** (*impostazione predefinita*) - Viene ripristinata l'impostazione predefinita di Windows, ovvero disattivato.
  - **Bloccato**
  - **Modalità di controllo** - Vengono generati eventi di Windows anziché imporre il blocco.

- **Blocca il download di contenuti eseguibili dai client di posta elettronica e posta sul Web**  
  [Proteggere i dispositivi dagli exploit](https://go.microsoft.com/fwlink/?linkid=872980)

  - **Non configurato** (*impostazione predefinita*) - Viene ripristinata l'impostazione predefinita di Windows, ovvero disattivato.
  - **Blocca** - Viene bloccato il contenuto eseguibile scaricato dai client di posta elettronica e posta sul Web.
  - **Modalità di controllo** - Vengono generati eventi di Windows anziché imporre il blocco.

- **Usa la protezione avanzata da ransomware**  
   [Proteggere i dispositivi dagli exploit](https://go.microsoft.com/fwlink/?linkid=874504)

  Questa regola di ASR viene controllata tramite il GUID seguente: c1db55ab-c21a-4637-bb3f-a12568109d35
  - **Non configurato** (*impostazione predefinita*) - Viene ripristinata l'impostazione predefinita di Windows, ovvero disattivato.
  - **Definito dall'utente**
  - **Attiva**
  - **Modalità di controllo** - Vengono generati eventi di Windows anziché imporre il blocco.

- **Abilita la protezione delle cartelle**  
  CSP: [EnableControlledFolderAccess](https://go.microsoft.com/fwlink/?linkid=872614)

  - **Non configurato** (*impostazione predefinita*) - questa impostazione ripristina il valore predefinito, ovvero nessuna lettura o scrittura bloccata.
  - **Attiva** - Per le app non affidabili, Defender blocca i tentativi di modifica o eliminazione di file in cartelle protette o di scrittura in settori del disco. Defender determina automaticamente quali applicazioni possono essere considerate attendibili. In alternativa è possibile definire un proprio elenco di applicazioni attendibili.
  - **Modalità controllo** - Quando applicazioni non attendibili accedono alle cartelle controllate vengono attivati eventi di Windows, ma non viene applicato nessun blocco.
  - **Blocca la modifica del disco** - Vengono bloccati solo i tentativi di scrittura nei settori del disco.
  - **Controlla la modifica del disco** - Vengono attivati eventi di Windows anziché blocchi dei tentativi di scrittura nei settori del disco.
  
- **Escludi file e percorsi dalle regole per la riduzione della superficie di attacco**  
  CSP: [AttackSurfaceReductionOnlyExclusions](https://go.microsoft.com/fwlink/?linkid=872981)

  Espandere l'elenco a discesa e selezionare **Aggiungi** per definire il **Percorso** di un file o una cartella da escludere dalle regole per la riduzione della superficie di attacco.

## <a name="device-control-profile"></a>Profilo Controllo del dispositivo

### <a name="device-control"></a>Controllo dei dispositivi

- **Installazione di dispositivi hardware per identificatori di dispositivo**  
  [PreventInstallationOfMatchingDeviceIDs](https://go.microsoft.com/fwlink/?linkid=2066794)  
  
  Questa impostazione consente di specificare un elenco di ID hardware Plug and Play e ID compatibili per i dispositivi la cui installazione non è consentita in Windows. L'impostazione di questo criterio ha la precedenza su qualsiasi altra impostazione di criteri che consente a Windows di installare un dispositivo.  Se si abilita l'impostazione di questo criterio in un server desktop remoto, l'impostazione del criterio influirà sul reindirizzamento dei dispositivi specificati da un client desktop remoto al server desktop remoto.

  - **Non configurato**
  - **Consenti l'installazione del dispositivo hardware** - I dispositivi possono essere installati o aggiornati in base a quanto consentito o impedito da altre impostazioni di criteri.
  - **Blocca l'installazione del dispositivo hardware** (*impostazione predefinita*) - A Windows non è consentito installare un dispositivo il cui ID hardware o ID compatibile viene visualizzato in un elenco definito dall'utente.

  Se l'impostazione è *Blocca l'installazione del dispositivo hardware* è possibile configurare le seguenti opzioni:

  - **Rimuovere dispositivi hardware corrispondenti**

    Questa impostazione è disponibile solo quando l'*installazione di dispositivi hardware per identificatori di dispositivo* è impostata su *Bloccare l'installazione del dispositivo hardware*.
    - **Sì**
    - **Non configurato**

  - **Identificatori di dispositivo hardware bloccati**  

    Questa impostazione è disponibile solo quando l'*installazione di dispositivi hardware per identificatori di dispositivo* è impostata su *Bloccare l'installazione del dispositivo hardware*.

    Selezionare **Aggiungi** e quindi specificare l'identificatore del dispositivo hardware che si vuole bloccare.

- **Installazione di dispositivi hardware per classi di installazione**  
  CSP: [DeviceInstallation/AllowInstallationOfMatchingDeviceSetupClasses](https://go.microsoft.com/fwlink/?linkid=2067048)  
  
  L'impostazione di questo criterio consente di specificare un elenco di identificatori univoci globali (GUID) della classe di installazione del dispositivo per i driver di dispositivo la cui installazione non è consentita in Windows. L'impostazione di questo criterio ha la precedenza su qualsiasi altra impostazione di criteri che consente a Windows di installare un dispositivo. Se si abilita l'impostazione di questo criterio in un server desktop remoto, l'impostazione del criterio influirà sul reindirizzamento dei dispositivi specificati da un client desktop remoto al server desktop remoto.

  - **Non configurato**
  - **Consenti l'installazione del dispositivo hardware** - Windows può installare e aggiornare i dispositivi in base a quanto consentito o impedito da altre impostazioni di criteri.
  - **Blocca l'installazione del dispositivo hardware** (*impostazione predefinita*) - A Windows non è consentito installare un dispositivo i cui GUID di classe di installazione compaiono in un elenco definito dall'utente.

  Con l'impostazione *Blocca l'installazione del dispositivo hardware* è possibile configurare *Rimuovi i dispositivi hardware corrispondenti* e *Identificatori dei dispositivi hardware bloccati*.

  - **Rimuovere dispositivi hardware corrispondenti**

    Questa impostazione è disponibile solo quando l'*installazione di dispositivi hardware per identificatori di dispositivo* è impostata su *Bloccare l'installazione del dispositivo hardware*.
    - **Sì**
    - **Non configurato**

  - **Identificatori di dispositivo hardware bloccati**

    Questa impostazione è disponibile solo quando l'*installazione di dispositivi hardware per identificatori di dispositivo* è impostata su *Bloccare l'installazione del dispositivo hardware*.

    Selezionare **Aggiungi** e quindi specificare l'identificatore del dispositivo hardware che si vuole bloccare.

- **Analizza le unità rimovibili durante un'analisi completa**  
  CSP: [Defender/AllowFullScanRemovableDriveScanning](https://go.microsoft.com/fwlink/?linkid=2113946)

  - **Non configurato** (*impostazione predefinita*) - Viene ripristinata l'impostazione predefinita del client, che analizza le unità rimovibili, tuttavia l'utente può disabilitare questa analisi.
  - **Sì** - durante un'analisi completa vengono analizzate le unità rimovibili, ad esempio le unità flash USB.

- **Blocca l'accesso diretto alla memoria**  
  CSP: [DataProtection/AllowDirectMemoryAccess](https://go.microsoft.com/fwlink/?linkid=2067031)

  L'impostazione di questo criterio viene applicata solo quando è abilitato BitLocker o la crittografia del dispositivo.

  - **Non configurato** (*impostazione predefinita*)
  - **Sì** - Impedisce l'accesso diretto alla memoria (DMA, Direct Memory Access) per tutte le porte downstream PCI collegabili a caldo finché un utente non accede a Windows. Dopo l'accesso di un utente, Windows enumera i dispositivi PCI connessi alle porte PCI collegabili a caldo. Ogni volta che l'utente blocca il computer, l'accesso diretto alla memoria viene bloccato sulle porte PCI collegabili a sistema acceso senza dispositivi figlio finché l'utente non accede di nuovo. I dispositivi già enumerati quando il computer era sbloccato continueranno a funzionare fino a quando non saranno scollegati.

- **Enumerazione di dispositivi esterni non compatibili con la protezione DMA del kernel**  
  CSP: [DmaGuard/DeviceEnumerationPolicy](/windows/client-management/mdm/policy-csp-dmaguard#dmaguard-deviceenumerationpolicy)

  Questo criterio può offrire ulteriore sicurezza nei confronti di dispositivi esterni idonei per DMA. Consente inoltre maggiore controllo sull'enumerazione di dispositivi esterni idonei per DMA non compatibili con il remapping e/o l'isolamento e il sandboxing della memoria del dispositivo.

  Questo criterio viene applicato solo quando la protezione DMA del kernel è supportata e abilitata dal firmware del sistema. La protezione DMA del kernel è una funzionalità della piattaforma che deve essere supportata dal sistema al momento della produzione. Per verificare se il sistema supporta la protezione DMA del kernel, controllare il campo della protezione DMA del kernel nella pagina di riepilogo di MSINFO32.exe.

  - **Non configurato** - (*impostazione predefinita*)
  - **Blocca tutto**
  - **Consenti tutto**

- **Blocca le connessioni Bluetooth**  
  CSP: [Bluetooth/AllowDiscoverableMode](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowdiscoverablemode)

  - **Non configurato** (*impostazione predefinita*)
  - **Sì** - Blocca le connessioni Bluetooth verso e dal dispositivo.

- **Impedisci l'individuabilità Bluetooth**  
  CSP: [Bluetooth/AllowDiscoverableMode](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowdiscoverablemode)

  - **Non configurato** (*impostazione predefinita*)
  - **Sì** - Impedisce che il dispositivo sia individuabile da altri dispositivi Bluetooth.

- **Blocca la pre-associazione Bluetooth**  
  CSP: [Bluetooth/AllowPrepairing](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowprepairing)

  - **Non configurato** (*impostazione predefinita*)
  - **Sì** - Impedisce a dispositivi Bluetooth specifici l'associazione automatica al dispositivo host.

- **Blocca gli annunci con Bluetooth**  
  CSP: [Bluetooth/AllowAdvertising](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowadvertising)

  - **Non configurato** (*impostazione predefinita*)
  - **Sì** - Impedisce al dispositivo di inviare annunci Bluetooth.  

- **Blocca le connessioni di prossimità Bluetooth**  
  CSP: [Bluetooth/AllowPromptedProximalConnections](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowpromptedproximalconnections) - Impedisce agli utenti di usare Associazione rapida e altri scenari basati su prossimità

  - **Non configurato** (*impostazione predefinita*)
  - **Sì** - Impedisce a un utente del dispositivo di usare Associazione rapida e altri scenari basati sulla prossimità.  

  [CSP Bluetooth/AllowPromptedProximalConnections](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowpromptedproximalconnections)

- **Servizi Bluetooth consentiti**  
  CSP: [Bluetooth/ServicesAllowedList](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-servicesallowedlist).  
  Per altre informazioni sull'elenco di servizi, vedere [Guida all'utilizzo di ServicesAllowedList](/windows/client-management/mdm/policy-csp-bluetooth#servicesallowedlist-usage-guide).

  - **Aggiungi** - Specificare un elenco di servizi e profili Bluetooth consentiti in forma di stringhe esadecimali, ad esempio `{782AFCFC-7CAA-436C-8BF0-78CD0FFBD4AF}`.
  - **Importa** - Importare un file CSV contenente un elenco di servizi e profili Bluetooth come stringhe esadecimali, ad esempio `{782AFCFC-7CAA-436C-8BF0-78CD0FFBD4AF}`

## <a name="exploit-protection-profile"></a>Profilo Protezione dagli exploit

### <a name="exploit-protection"></a>Protezione dagli exploit

- **Carica XML**  
  CSP: [ExploitProtectionSettings](https://go.microsoft.com/fwlink/?linkid=2067035)

  Consente all'amministratore IT di distribuire una configurazione che rappresenta il sistema desiderato e le opzioni di mitigazione delle applicazioni a tutti i dispositivi nell'organizzazione. La configurazione è rappresentata da un file XML. Protezione dagli exploit aiuta a proteggere i dispositivi dal malware che usa gli exploit per la diffusione e l'infezione. Usare l'app Sicurezza di Windows o PowerShell per creare un set di mitigazioni, chiamato configurazione. È quindi possibile esportare la configurazione come file XML e condividerla con più computer in rete in modo che abbiano lo stesso set di impostazioni di mitigazione. È anche possibile convertire e importare un file XML di configurazione EMET esistente in un file XML di configurazione di protezione dagli exploit.

  Scegliere **Seleziona file XML**, specificare il file XML da caricare e fare clic su **Seleziona**.
  - **Non configurato** (*impostazione predefinita*)
  - **Sì**

- **Impedisce agli utenti di modificare l'interfaccia di protezione di Exploit Guard**  
  CSP: [DisallowExploitProtectionOverride](https://go.microsoft.com/fwlink/?linkid=2067239)

  - **Non configurato** (*impostazione predefinita*) - Gli utenti locali non possono apportare modifiche nell'area delle impostazioni per la protezione dagli exploit.
  - **Sì** - Impedisce agli utenti di apportare modifiche nell'area delle impostazioni per la protezione dagli exploit in Microsoft Defender Security Center.

## <a name="next-steps"></a>Passaggi successivi

[Criteri di sicurezza degli endpoint per ASR](../protect/endpoint-security-asr-policy.md)