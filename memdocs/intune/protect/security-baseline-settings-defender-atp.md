---
title: Impostazioni delle baseline di sicurezza di Intune per Microsoft Defender Advanced Threat Protection
titleSuffix: Microsoft Intune
description: Impostazioni della baseline di sicurezza supportate da Intune per la gestione di Microsoft Defender Advanced Threat Protection
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 12/05/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: shpate
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7ebea853ac536b182a9cfe35e8b291aea3a776f0
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79351201"
---
# <a name="microsoft-defender-advanced-threat-protection-baseline-settings-for-intune"></a>Impostazioni della baseline di Microsoft Defender Advanced Threat Protection per Intune

Vedere le impostazioni della baseline di Microsoft Defender Advanced Threat Protection (in precedenza Windows Defender Advanced Threat Protection) supportate da Microsoft Intune. Le impostazioni predefinite della baseline di Advanced Threat Protection (ATP) rappresentano la configurazione consigliata per ATP e potrebbero non corrispondere ai valori predefiniti della baseline per altre baseline di sicurezza.  

La baseline di Microsoft Defender Advanced Threat Protection è disponibile quando l'ambiente soddisfa i prerequisiti per l'uso di [Microsoft Defender Advanced Threat Protection](advanced-threat-protection.md#prerequisites). 

Questa baseline è ottimizzata per i dispositivi fisici e attualmente se ne sconsiglia l'uso in macchine virtuali (VM) o endpoint VDI. Alcune impostazioni di base possono influire sulle sessioni interattive remote negli ambienti virtualizzati. Per altre informazioni, vedere [Incremento della conformità alla baseline di sicurezza di Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-machines-security-baseline) nella documentazione di Windows.

## <a name="application-guard"></a>Application Guard  
Per altre informazioni, vedere [WindowsDefenderApplicationGuard CSP](https://docs.microsoft.com/windows/client-management/mdm/windowsdefenderapplicationguard-csp) (Provider dei servizi di configurazione di WindowsDefenderApplicationGuard) nella documentazione di Windows.  

Quando si usa Microsoft Edge, Microsoft Defender Application Guard protegge l'ambiente dai siti non considerati attendibili dall'organizzazione. Quando gli utenti visitano siti non elencati nei limiti della rete isolata, tali siti vengono aperti in una sessione del browser virtuale di Hyper-V. I siti attendibili sono definiti da un limite di rete.  

- **Application Guard** - *Impostazioni/AllowWindowsDefenderApplicationGuard*  
  Selezionare *Sì* per attivare questa funzionalità che consente di aprire siti non attendibili in un contenitore del browser virtuale di Hyper-V. Se il valore impostato è *Non configurato*, qualsiasi sito (attendibile e non attendibile) viene aperto nel dispositivo e non in un contenitore virtuale.  

  **Impostazione predefinita**: Sì
 
  - **Contenuto esterno nei siti aziendali** - *Impostazioni/BlockNonEnterpriseContent*  
    Selezionare *Sì* per bloccare il caricamento di contenuti provenienti da siti Web non approvati. Se il valore impostato è *Non configurato*, i siti non aziendali possono essere aperti sul dispositivo. 
 
    **Impostazione predefinita**: Sì

  - **Comportamento degli Appunti** - *Impostazioni/ClipboardSettings*  
    Consente di scegliere le azioni di copia/incolla consentite tra il computer locale e il browser virtuale di Application Guard.  Le opzioni includono:
    - Non configurato  
    - Blocca copia e incolla tra computer e browser - Blocca entrambi. I dati non possono essere trasferiti tra il PC e il browser virtuale.  
    - Consenti copia e incolla solo dal browser al computer - I dati non possono essere trasferiti dal PC al browser virtuale.
    - Consenti copia e incolla solo dal browser al computer - I dati non possono essere trasferiti dal browser virtuale al PC host.
    - Consenti copia e incolla tra computer e browser - Nessun blocco dei contenuti.  

    **Impostazione predefinita**: Blocca copia e incolla tra computer e browser  

- **Criteri di isolamento della rete di Windows - Nomi di dominio della rete aziendale**  
  Per altre informazioni, vedere [Policy CSP - NetworkIsolation](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-networkisolation) (Provider dei servizi di configurazione dei criteri - Network Isolation) nella documentazione di Windows.
  
  Specifica un elenco di risorse aziendali come domini, intervalli di indirizzi IP e limiti di rete ospitati nel cloud e considerati come siti aziendali da Application Guard.  

  **Impostazione predefinita**: securitycenter.windows.com

## <a name="application-reputation"></a>Reputazione delle applicazioni  

Per altre informazioni, vedere [Policy CSP - SmartScreen](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-smartscreen) (Provider di servizi di configurazione dei criteri - SmartScreen) nella documentazione di Windows.

- **Bloccare l'esecuzione di file non verificati**  
    Impedisce all'utente di eseguire file non verificati. Se il valore è impostato su *Non configurato*, i dipendenti possono ignorare gli avvisi di SmartScreen ed eseguire file dannosi. Impostare su *Sì* in modo che i dipendenti non possano ignorare gli avvisi di SmartScreen ed eseguire file dannosi.  
  
    **Impostazione predefinita**: Sì

- **Richiedere SmartScreen per app e file**  
  Impostare su *Sì* per abilitare SmartScreen per Windows.  

  **Impostazione predefinita**: Sì

## <a name="attack-surface-reduction"></a>Riduzione della superficie di attacco  

- **Avviare i processi di tipo figlio per le app di Office**  
  [Regola di riduzione della superficie di attacco](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#attack-surface-reduction-rules) - Impostare su *Blocca* per impedire alle app di Office di creare processi figlio. Le app di Office includono Word, Excel, PowerPoint, OneNote e Access. La creazione di un processo figlio è un comportamento tipico del malware, in particolare degli attacchi basati su macro che tentano di usare le app di Office per avviare o scaricare file eseguibili dannosi.  

  **Impostazione predefinita**: Blocca

- **Tipo di esecuzione del payload scaricato tramite script**  
  [Defender/PUAProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-puaprotection)- Specificare un livello di rilevamento per le applicazioni potenzialmente indesiderate scaricate o di cui si tenta l'installazione.  

  **Impostazione predefinita**: Blocca 

- **Impedire il tipo di intercettazione delle credenziali**  
  Impostare su *Abilita* per [proteggere le credenziali di dominio derivate con Windows Defender Credential Guard](https://docs.microsoft.com/windows/security/identity-protection/credential-guard/credential-guard). Microsoft Defender Credential Guard usa la sicurezza basata su virtualizzazione per isolare i segreti in modo che solo il software di sistema con privilegi possa accedervi. L'accesso non autorizzato a questi segreti può causare attacchi con furto di credenziali, ad esempio Pass-the-Hash o Pass-The-Ticket. Microsoft Defender Credential Guard impedisce questi attacchi proteggendo gli hash delle password NTLM, i Ticket Granting Ticket Kerberos e le credenziali archiviate dalle applicazioni come credenziali di dominio.  

  **Impostazione predefinita**: Abilitare

- **Esecuzione del contenuto del messaggio di posta elettronica**  
  [Regola di riduzione della superficie di attacco](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#attack-surface-reduction-rules) - Se impostata su *Blocca*, questa regola blocca l'esecuzione e l'avvio dei tipi di file seguenti da un messaggio di posta elettronica visualizzato in Microsoft Outlook o nella posta sul Web (ad esempio Gmail.com o Outlook.com):  

  - File eseguibili, ad esempio con estensione exe, dll o scr  
  - File di script, ad esempio file con estensione ps di PowerShell, con estensione vbs di VisualBasic o con estensione js di JavaScript  
  - File di archivio di script  

  **Impostazione predefinita**: Blocca

- **Avvio di Adobe Reader in un processo figlio**  
  [Regola di riduzione della superficie di attacco](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#attack-surface-reduction-rules) - *Abilitare* questa regola per impedire ad Adobe Reader di creare un processo figlio. Tramite tecniche di ingegneria sociale oppure exploit, il malware può scaricare e avviare payload aggiuntivi e uscire da Adobe Reader.  

  **Impostazione predefinita**: Abilitare

- **Codice macro offuscato in script**  
  [Regola di riduzione della superficie di attacco](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#attack-surface-reduction-rules) - Malware e altre minacce possono tentare di offuscare o nascondere il codice dannoso in alcuni file di script. Questa regola impedisce l'esecuzione degli script offuscati.  
    
  **Impostazione predefinita**: Blocca

- **Processo non attendibile in USB**  
  [Regola di riduzione della superficie di attacco](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#attack-surface-reduction-rules) - Se impostata su *Blocca*, i file eseguibili non firmati o non attendibili di unità USB rimovibili e schede SD non possono essere eseguiti.

  I file eseguibili includono:
  - File eseguibili, ad esempio con estensione exe, dll o scr
  - File di script, ad esempio file con estensione ps di PowerShell, con estensione vbs di VisualBasic o con estensione js di JavaScript  

  **Impostazione predefinita**: Blocca

- **Inserimento in altri processi per app di Office**  
  [Regola di riduzione della superficie di attacco](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#attack-surface-reduction-rules) - Se impostata su *Blocca*, le app di Office, ad esempio Word, Excel, PowerPoint e OneNote non possono inserire codice in altri processi. L'inserimento di codice è tipico comportamento del malware per eseguire codice malware nel tentativo di nascondere l'attività ai motori di analisi antivirus.  

  **Impostazione predefinita**: Blocca

- **Consentire importazioni Win32 da codice macro in Office**  
  [Regola di riduzione della superficie di attacco](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#attack-surface-reduction-rules) - Se impostata su *Blocca*, questa regola prova a bloccare l file di Office contenenti codice macro che può importare DLL Win32. I file di Office includono Word, Excel, PowerPoint e OneNote. Il malware può usare il codice della macro in file di Office per importare e caricare le DLL Win32, che vengono quindi usate per eseguire chiamate API e favorire altre infezioni in tutto il sistema.  

  **Impostazione predefinita**: Blocca

- **Avvio di app di comunicazione di Office in un processo figlio**  
  [Regola di riduzione della superficie di attacco](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#attack-surface-reduction-rules) - Se impostata su *Abilita*, questa regola impedisce a Outlook di creare processi figlio. Bloccando la creazione di un processo figlio, questa regola consente di proteggere il sistema da attacchi di ingegneria sociale e impedisce agli exploit di sfruttare una vulnerabilità in Outlook.  

  **Impostazione predefinita**: Abilitare

- **Contenuto per la creazione o l'avvio di eseguibile nelle app di Office**  
  [Regola di riduzione della superficie di attacco](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#attack-surface-reduction-rules) - Se impostata su *Blocca*, le app di Office non possono creare contenuto eseguibile. Le app di Office includono Word, Excel, PowerPoint, OneNote e Access.  

  Questa regola è rivolta ai tipici comportamenti usati da componenti aggiuntivi e script sospetti e dannosi (estensioni) che creano o avviano file eseguibili. Si tratta di una tipica tecnica malware. Le estensioni non possono essere usate dalle app di Office. Queste estensioni usano generalmente Windows Scripting Host (file con estensione wsh) per eseguire script che automatizzano determinate attività oppure aggiungono funzionalità create dall'utente.

  **Impostazione predefinita**: Blocca

## <a name="bitlocker"></a>BitLocker  

Per altre informazioni, vedere [Impostazioni di Criteri di gruppo per BitLocker](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-group-policy-settings) nella documentazione di Windows.  

- **Crittografa i dispositivi**  
  Selezionare *Sì* per abilitare la crittografia dei dispositivi BitLocker. In base all'hardware del dispositivo e alla versione di Windows, agli utenti potrebbe essere richiesto di confermare che non sia presente alcuna crittografia di terze parti nel dispositivo. L'attivazione della crittografia di Windows mentre è attiva la crittografia di terze parti rende instabile il dispositivo.  

   **Impostazione predefinita**: Sì

- **Criterio per le unità rimovibili BitLocker**  
  I valori per questo criterio determinano il livello di crittografia che BitLocker usa per la crittografia delle unità rimovibili. Per una maggiore sicurezza, le aziende controllano il livello di crittografia (AES-256 è un algoritmo più avanzato rispetto a AES-128). Se si seleziona *Sì* per abilitare questa impostazione, è possibile configurare individualmente un algoritmo di crittografia e un livello di codifica per unità dati fisse, unità del sistema operativo e unità dati rimovibili. Per le unità fisse e del sistema operativo è consigliabile usare l'algoritmo XTS-AES. Per le unità rimovibili è consigliabile usare AES-CBC a 128 bit o AES-CBC a 256 bit se l'unità viene usata in altri dispositivi che non eseguono Windows 10 versione 1511 o successiva. La modifica del metodo di crittografia non produce alcun effetto se l'unità è già crittografata o se la crittografia è in corso. In questi casi, l'impostazione di questo criterio viene ignorata. 

  Per i criteri di un'unità rimovibile BitLocker, configurare le impostazioni seguenti:

  - **Richiedere la crittografia per l'accesso in scrittura**  
    **Impostazione predefinita**: Sì

  - **Metodo di crittografia**  
    **Impostazione predefinita**: AES a 128 bit CBC

- **Crittografa la scheda di memoria (solo dispositivi mobili)** Selezionare *Sì* per crittografare la scheda di memoria del dispositivo mobile.  

   **Impostazione predefinita**: Sì

- **Criterio per le unità fisse BitLocker**  
  I valori per questo criterio determinano il livello di crittografia che BitLocker usa per la crittografia delle unità fisse. Per una maggiore sicurezza, le aziende possono controllare il livello di crittografia (AES-256 è un algoritmo più avanzato rispetto a AES-128). Se si abilita questa impostazione, è possibile configurare individualmente un algoritmo di crittografia e un livello di codifica per unità dati fisse, unità del sistema operativo e unità dati rimovibili. Per le unità fisse e del sistema operativo è consigliabile usare l'algoritmo XTS-AES. Per le unità rimovibili è consigliabile usare AES-CBC a 128 bit o AES-CBC a 256 bit se l'unità viene usata in altri dispositivi che non eseguono Windows 10 versione 1511 o successiva. La modifica del metodo di crittografia non produce alcun effetto se l'unità è già crittografata o se la crittografia è in corso. In questi casi, l'impostazione di questo criterio viene ignorata.

  Per i criteri di un'unità fissa BitLocker, configurare le impostazioni seguenti:

  - **Richiedere la crittografia per l'accesso in scrittura**  
    **Impostazione predefinita**: Sì

  - **Metodo di crittografia**  
    **Impostazione predefinita**: AES a 128 bit XTS

- **Criterio per le unità di sistema BitLocker**  
  I valori per questo criterio determinano il livello di crittografia che BitLocker usa per la crittografia delle unità di sistema. Per una maggiore sicurezza, le aziende potrebbero voler controllare il livello di crittografia (AES-256 è un algoritmo più avanzato rispetto a AES-128). Se si abilita questa impostazione, è possibile configurare individualmente un algoritmo di crittografia e un livello di codifica per unità dati fisse, unità del sistema operativo e unità dati rimovibili. Per le unità fisse e del sistema operativo è consigliabile usare l'algoritmo XTS-AES. Per le unità rimovibili è consigliabile usare AES-CBC a 128 bit o AES-CBC a 256 bit se l'unità viene usata in altri dispositivi che non eseguono Windows 10 versione 1511 o successiva. La modifica del metodo di crittografia non produce alcun effetto se l'unità è già crittografata o se la crittografia è in corso. In questi casi, l'impostazione di questo criterio viene ignorata.  

  Per i criteri di un'unità di sistema BitLocker, configurare le impostazioni seguenti:  

  - **Metodo di crittografia**  
    **Impostazione predefinita**: AES a 128 bit XTS

## <a name="device-control"></a>Controllo dei dispositivi  

- **Analizzare le unità rimovibili durante un'analisi completa**  
  [Defender/AllowFullScanRemovableDriveScanning](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanremovabledrivescanning) - Se impostato su *Sì*, Defender esegue la ricerca di software dannoso e indesiderato nelle unità rimovibili, ad esempio unità flash USB, durante un'analisi completa. Windows Defender Antivirus analizza tutti i file nei dispositivi USB prima che vengano eseguiti nel dispositivo stesso.

  Impostazione correlata in questo elenco: *Defender/AllowFullScanOnMappedNetworkDrives*  

  **Impostazione predefinita**: Sì

- **Enumerazione di dispositivi esterni non compatibili con la protezione DMA del kernel**  
   Vedere *DmaGuard/DeviceEnumerationPolicy* in [Policy CSP - DmaGuard](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-dmaguard#dmaguard-deviceenumerationpolicy) (Provider dei servizi di configurazione dei criteri - DmaGuard)

  Questo criterio offre ulteriore sicurezza nei confronti di dispositivi esterni idonei per DMA, nonché maggiore controllo sull'enumerazione di dispositivi esterni idonei per DMA non compatibili con isolamento e sandboxing della memoria del dispositivo.

  Questo criterio viene applicato solo quando la protezione DMA del kernel è supportata e abilitata dal firmware del sistema. La protezione DMA del kernel è una funzionalità della piattaforma che non può essere controllata tramite criteri o dall'utente finale di un dispositivo, ma deve essere supportata dal sistema in fase di produzione. 

  Per verificare se il sistema supporta la protezione DMA del kernel, eseguire MSINFO32.exe nel sistema e vedere il campo *Kernel DMA Protection* (Protezione DMA kernel) campo nella pagina di riepilogo.  

  Le opzioni includono: 
  - *Device default* (Dispositivo predefinito) - Dopo l'accesso o il blocco dello schermo, i dispositivi con unità compatibili con il nuovo mapping DMA possono essere enumerati in qualsiasi momento. I dispositivi con unità incompatibili con il nuovo mapping DMA vengono enumerati solo dopo lo sblocco dello schermo da parte dell'utente.
  - *Allow all* (Consenti tutto) - Tutti i dispositivi PCIe idonei per DMA vengono enumerati in qualsiasi momento
  - *Block all* (Blocca tutto) - I dispositivi con unità compatibili con il nuovo mapping DMA possono essere enumerati in qualsiasi momento. I dispositivi con unità incompatibili con il nuovo mapping DMA non potranno mai avviare né eseguire DMA in alcun momento.

  **Impostazione predefinita**: Impostazione predefinita dispositivo

- **Installazione di dispositivi hardware per identificatori di dispositivo**  
  [DeviceInstallation/PreventInstallationOfMatchingDeviceIDs](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-deviceinstallation#deviceinstallation-preventinstallationofmatchingdeviceids) - Questo criterio consente di specificare un elenco di ID di hardware Plug and Play e di ID compatibili per i dispositivi di cui si impedisce l'installazione in Windows. L'impostazione di questo criterio ha la precedenza su qualsiasi altra impostazione di criteri che consente a Windows di installare un dispositivo. Se si abilita questo criterio (impostato su *Blocca l'installazione del dispositivo hardware*), si impedisce l'installazione di un dispositivo il cui ID hardware o ID compatibile è presente nell'elenco creato. Se si abilita l'impostazione di questo criterio in un server desktop remoto, il criterio influirà sul reindirizzamento dei dispositivi specificati da un client desktop remoto al server desktop remoto. Se si disabilita o non si configura questo criterio (impostato su *Allow hardware device installation* - Consenti l'installazione del dispositivo hardware), i dispositivi possono essere installati e aggiornati in base a quanto consentito o impedito da altre impostazioni dei criteri.  

  **Impostazione predefinita**: Bloccare l'installazione del dispositivo hardware  

  Quando l'opzione *Blocca l'installazione del dispositivo hardware* è selezionata, sono disponibili le impostazioni seguenti.
  - **Rimuovere dispositivi hardware corrispondenti**  
    Questa impostazione è disponibile solo quando l'*installazione di dispositivi hardware per identificatori di dispositivo* è impostata su *Bloccare l'installazione del dispositivo hardware*.  

    **Impostazione predefinita**: Sì

  - **Identificatori di dispositivo hardware bloccati**  
    Questa impostazione è disponibile solo quando l'*installazione di dispositivi hardware per identificatori di dispositivo* è impostata su *Bloccare l'installazione del dispositivo hardware*. Per configurare questa impostazione, espandere l'opzione, selezionare **+ Aggiungi** e quindi specificare l'identificatore del dispositivo hardware da bloccare.  

    **Impostazione predefinita**: PCI\CC_0C0A

- **Blocca l'accesso diretto alla memoria**  
  [DataProtection/AllowDirectMemoryAccess](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-dataprotection#dataprotection-allowdirectmemoryaccess) - Questo criterio consente di bloccare l'accesso diretto alla memoria (DMA) per tutte le porte downstream PCI con collegamento a caldo in un dispositivo fino a quando l'utente non esegue l'accesso a Windows. Dopo l'accesso di un utente, Windows enumererà i dispositivi PCI connessi alle porte PCI collegabili a sistema acceso. Ogni volta che l'utente blocca il computer, l'accesso diretto alla memoria viene bloccato sulle porte PCI collegabili a sistema acceso senza dispositivi figlio finché l'utente non accede di nuovo. I dispositivi già enumerati quando il computer era sbloccato continueranno a funzionare fino a quando non saranno scollegati. 

  L'impostazione di questo criterio viene applicata solo quando è abilitato BitLocker o la crittografia del dispositivo.  

  **Impostazione predefinita**: Sì


- **Installazione di dispositivi hardware per classi di installazione**  
  [DeviceInstallation/AllowInstallationOfMatchingDeviceSetupClasses](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-deviceinstallation#deviceinstallation-allowinstallationofmatchingdevicesetupclasses) - Questo criterio consente di specificare un elenco di identificatori univoci globali (GUID) di classi di installazione di dispositivi per driver di dispositivo di cui si impedisce l'installazione in Windows. L'impostazione di questo criterio ha la precedenza su qualsiasi altra impostazione di criteri che consente a Windows di installare un dispositivo. Se si abilita questo criterio (impostato su *Blocca l'installazione del dispositivo hardware*), in Windows si impedisce di installare o di aggiornare i driver di dispositivo i cui GUID della classe di installazione sono presenti nell'elenco creato. Se si abilita l'impostazione di questo criterio in un server desktop remoto, l'impostazione del criterio influirà sul reindirizzamento dei dispositivi specificati da un client desktop remoto al server desktop remoto. Se si disabilita o non si configura questo criterio (impostato su *Allow hardware device installation* - Consenti l'installazione del dispositivo hardware), Windows può installare e aggiornare dispositivi possono essere installati e aggiornati in base a quanto consentito o impedito da altre impostazioni dei criteri.  

  **Impostazione predefinita**: Bloccare l'installazione del dispositivo hardware

  Quando l'opzione *Blocca l'installazione del dispositivo hardware* è selezionata, sono disponibili le impostazioni seguenti.  

  - **Rimuovere dispositivi hardware corrispondenti**  
    Questa impostazione è disponibile solo quando l'*installazione di dispositivi hardware per classi di installazione* è impostata su *Bloccare l'installazione del dispositivo hardware*.  
 
    **Impostazione predefinita**: Sì  

  - **Identificatori di dispositivo hardware bloccati**  
    Questa impostazione è disponibile solo quando l'installazione di dispositivi hardware per classi di installazione è impostata su Blocca l'installazione del dispositivo hardware. Per configurare questa impostazione, espandere l'opzione, selezionare **+ Aggiungi** e quindi specificare l'identificatore del dispositivo hardware da bloccare.  
 
    **Impostazione predefinita**: {d48179be-ec20-11d1-b6b8-00c04fa372a7}

## <a name="endpoint-detection-and-response"></a>Rilevamento endpoint e risposta  
Per altre informazioni, vedere [WindowsAdvancedThreatProtection CSP](https://docs.microsoft.com/windows/client-management/mdm/windowsadvancedthreatprotection-csp) (Provider dei servizi di configurazione - WindowsAdvancedThreatProtection) nella documentazione di Windows.  

- **Accelera la frequenza di creazione di report di telemetria** - *Configurazione/TelemetryReportingFrequency*

  Consente di accelerare la frequenza di creazione di report di telemetria di Microsoft Defender Advanced Threat Protection.  

  **Impostazione predefinita**: Sì

- **Condivisione di esempi per tutti i file** - *Configurazione/SampleSharing* 

  Restituisce o imposta il parametro di configurazione per la condivisione di esempi di Microsoft Defender Advanced Threat Protection.  

  **Impostazione predefinita**: Sì

## <a name="exploit-protection"></a>Protezione dagli exploit  

- **XML di Protezione dagli exploit**  
  Per altre informazioni, vedere [Importare, esportare e distribuire configurazioni di protezione dagli exploit](/windows/security/threat-protection/microsoft-defender-atp/import-export-exploit-protection-emet-xml) nella documentazione di Windows.  

  Consente all'amministratore IT di distribuire una configurazione che rappresenta il sistema desiderato e le opzioni di mitigazione delle applicazioni a tutti i dispositivi nell'organizzazione. La configurazione è rappresentata da un XML. 

  La Protezione dagli exploit consente di proteggere i dispositivi da malware che usa gli exploit per la diffusione e l'infezione. Usare l'app Sicurezza di Windows o PowerShell per creare un set di mitigazioni, chiamato configurazione. È quindi possibile esportare la configurazione come file XML e condividerla con più computer in rete in modo che abbiano lo stesso set di impostazioni di mitigazione.
 
  È anche possibile convertire e importare un file XML di configurazione EMET esistente in un file XML di configurazione di protezione dagli exploit.

- **Block exploit protection override** (Blocca modifica protezione dagli exploit)  
  [WindowsDefenderSecurityCenter/DisallowExploitProtectionOverride](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-windowsdefendersecuritycenter#windowsdefendersecuritycenter-disallowexploitprotectionoverride): impostare su *Sì* per impedire agli utenti di apportare modifiche nell'area delle impostazioni per la protezione dagli exploit in Microsoft Defender Security Center. Se si disabilita o non si configura questa impostazione, gli utenti locali è possono apportare modifiche nell'area delle impostazioni di protezione dagli exploit.  
  **Impostazione predefinita**: Sì  

## <a name="microsoft-defender-antivirus"></a>Microsoft Defender Antivirus  

Per altre informazioni, vedere [Policy CSP - Defender](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender) (Provider di servizi di configurazione dei criteri - Defender) nella documentazione di Windows.

- **Analizza gli script caricati nei Web browser Microsoft**  
  [Defender/AllowScriptScanning](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowscriptscanning): impostare su *Sì* per consentire la funzionalità di analisi degli script di Microsoft Defender.  

  **Impostazione predefinita**: Sì

- **Analizzare i messaggi di posta elettronica in arrivo**  
  [Defender/AllowEmailScanning](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowemailscanning): impostare su *Sì* per consentire a Microsoft Defender di analizzare i messaggi di posta elettronica.  

  **Impostazione predefinita**: Sì

- **Consenso per l'invio di campioni di Defender**  
  [Defender/SubmitSamplesConsent](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-submitsamplesconsent): controlla il livello di consenso utente in Microsoft Defender per inviare i dati. Se il consenso necessario è già stato concesso, Microsoft Defender esegue l'invio. In caso contrario (e se l'utente ha specificato che non venga mai inviata una richiesta), viene richiesto il consenso utente (se *Abilita la protezione mediante cloud* è impostata su *Sì*) prima dell'invio dei dati.  

  **Impostazione predefinita**: Invia automaticamente i campioni sicuri

- **Network Inspection System (NIS)**  
  [Defender/EnableNetworkProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection) - Blocca il traffico dannoso rilevato dalle firme in Network Inspection System (NIS).  
 
  **Impostazione predefinita**: Sì

- **Intervallo di aggiornamento della firma (in ore)**  
  [Defender/SignatureUpdateInterval](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-signatureupdateinterval) - Specifica, in ore, la frequenza con cui il dispositivo controlla i nuovi aggiornamenti delle firme in Defender.  
 
  **Impostazione predefinita**: 4

- **Configura la priorità bassa per la CPU per le analisi pianificate**  
  [Defender/EnableLowCPUPriority](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-enablelowcpupriority) - Se impostato su *Sì*, la priorità della CPU per le analisi è impostata sul valore basso. Se è impostato su *Non configurato*, alla priorità della CPU per le analisi pianificate non viene apportata alcuna modifica.  

    **Impostazione predefinita**: Sì

- **Blocco Defender per protezione all'accesso**  
  [Defender/AllowOnAccessProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowonaccessprotection): se impostato su *Sì*, la protezione all'accesso di Microsoft Defender è abilitata.  

  **Impostazione predefinita**: Sì

- **Tipo di analisi di sistema da eseguire**  
  [Defender/ScanParameter](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-scanparameter) - Tipo di analisi di Defender.  

  **Impostazione predefinita**: Analisi veloce

- **Analizza tutti i download**  
  [Defender/AllowIOAVProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowioavprotection) - Se impostato su *Sì*, Defender analizza tutti i file e gli allegati scaricati.  

  **Impostazione predefinita**: Sì

- **Giorni di attesa prima dell'eliminazione di malware in quarantena**  
  [Defender/DaysToRetainCleanedMalware](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-daystoretaincleanedmalware) - Specifica il numero di giorni in cui tenere in quarantena gli elementi nel sistema prima che vengano eliminati automaticamente. Se impostato su zero, gli elementi in quarantena non vengono mai eliminati automaticamente.  

  **Impostazione predefinita**: 0

- **Ora di inizio analisi pianificata**  
  [Defender/ScheduleScanTime](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-schedulescantime) - Pianifica un'ora del giorno per l'analisi dei dispositivi da parte di Defender. 
  
  Opzione correlata in questo elenco: *Defender/ScheduleScanDay*   

  **Impostazione predefinita**: 2

- **Protezione fornita dal cloud**  
  [Defender/AllowCloudProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection): se impostato su *Sì*, Microsoft Defender invia informazioni a Microsoft su qualsiasi problema rilevato. Le informazioni saranno analizzate, saranno raccolti altri dettagli sui problemi riscontrati dall'utente corrente e dagli altri clienti. Verranno quindi offerte soluzioni migliorate.

  Quando il criterio è impostato su *Yes*, è possibile usare *Tipo di consenso per l'invio di campioni di Defender* per consentire agli utenti di controllare l'invio di informazioni dal proprio dispositivo.  

  **Impostazione predefinita**: Sì

- **Azione della Protezione da applicazioni potenzialmente di Defender**  
  [Defender/PUAProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-puaprotection): Antivirus Microsoft Defender può identificare le *applicazioni potenzialmente indesiderate* e impedirne il download e l'installazione negli endpoint della rete. 
 
  - Se impostato su *Blocco*, Microsoft Defender blocca le applicazioni potenzialmente indesiderate e le inserisce in un elenco cronologico con altre minacce.
  - Se impostato su *Controllo*, Microsoft Defender rileva le applicazioni potenzialmente indesiderate, ma non le blocca. Per trovare le informazioni sulle applicazioni per cui Microsoft Defender avrebbe intrapreso un'azione, eseguire una ricerca degli eventi creati in Visualizzatore eventi da Microsoft Defender.  
  - Se impostato su *Dispositivo predefinito*, la protezione delle applicazioni potenzialmente indesiderate è disattivata.  
 
  **Impostazione predefinita**: Blocca

- **Defender - Timeout esteso per il cloud in secondi**  
  [Defender/CloudExtendedTimeout](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-cloudextendedtimeout): specifica la quantità massima di tempo aggiuntivo in cui Antivirus Microsoft Defender deve bloccare un file in attesa di un risultato dal cloud. La durata dell'attesa di base da parte di Microsoft Defender è di 10 secondi. Eventuale tempo aggiuntivo specificato qui (fino a 50 secondi) viene aggiunto ai 10 secondi. Nella maggior parte dei casi l'analisi richiede meno tempo rispetto alla quantità massima indicata. L'estensione della quantità di tempo consente al cloud di analizzare nel dettaglio i file sospetti.  

  Per impostazione predefinita, il valore di estensione è pari a 0 (disabilitato). È consigliabile abilitare questa impostazione e specificare almeno 20 secondi aggiuntivi.  
 
  **Impostazione predefinita**: 0

- **Analizza file di archivio**  
  [Defender/AllowArchiveScanning](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowarchivescanning): impostare su *Sì* per indicare a Microsoft Defender di analizzare i file di archivio.  

  **Impostazione predefinita**: Sì

- **Defender - Pianificazione analisi del sistema**  
  [Defender/ScheduleScanDay](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-schedulescanday) - Pianifica il giorno in cui Defender analizza i dispositivi. 
 
  Opzione correlata in questo elenco: *Defender/ScheduleScanTime*

  **Impostazione predefinita**: Definita dall'utente

- **Monitoraggio del comportamento**  
  [Defender/AllowBehaviorMonitoring](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowbehaviormonitoring): impostare su *Sì* per attivare la funzionalità di monitoraggio del comportamento di Microsoft Defender. Integrati in Windows 10, i sensori di monitoraggio del comportamento di Microsoft Defender raccolgono ed elaborano i segnali comportamentali dal sistema operativo e inviano i dati all'istanza cloud isolata privata di Microsoft Defender ATP.  

  **Impostazione predefinita**: Sì

- **Analizzare file aperti da cartelle di rete**  
  [Defender/AllowScanningNetworkFiles](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowscanningnetworkfiles): impostare su *Sì* per indicare a Microsoft Defender di analizzare i file nella rete. L'utente non sarà in grado di rimuovere il malware rilevato dai file di sola lettura.  

  **Impostazione predefinita**: Sì

- **Livello di blocco cloud di Defender**  
  [Defender/CloudBlockLevel](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-cloudblocklevel): questo criterio consente di determinare il livello di intervento da parte di Antivirus Microsoft Defender nel bloccare e analizzare i file sospetti. Le opzioni includono:

  - Alto - Protezione elevata e blocco aggressivo dei file sconosciuti durante l'ottimizzazione delle prestazioni del client (maggiori probabilità di falsi positivi)
  - Alta + - Protezione massima e blocco aggressivo dei file sconosciuti con misure di sicurezza aggiuntive (possibile impatto sulle prestazioni del client)
  - Tolleranza zero - Blocco di tutti i file eseguibili

  **Impostazione predefinita**: Non configurato

- **Monitoraggio in tempo reale**  
  [Defender/AllowRealtimeMonitoring](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring): impostare su *Sì* per consentire il monitoraggio in tempo reale di Microsoft Defender.  

  **Impostazione predefinita**: Sì

- **Limite di utilizzo della CPU durante un'analisi**  
  [Defender/AvgCPULoadFactor](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-avgcpuloadfactor): specifica la percentuale di utilizzo medio massimo della CPU che Microsoft Defender può usare durante un'analisi.  

  **Impostazione predefinita**: 50

- **Analizza le unità di rete mappate durante un'analisi completa**  
  [Defender/AllowFullScanOnMappedNetworkDrives](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanonmappednetworkdrives): impostare su *Sì* per indicare a Microsoft Defender di analizzare i file nella rete. L'utente non può rimuovere il malware rilevato dai file di sola lettura.

  Impostazione correlata in questo elenco: *Defender/AllowScanningNetworkFiles*

  **Impostazione predefinita**: Sì

- **Blocca l'accesso dell'utente finale a Defender**  
  [Defender/AllowUserUIAccess](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowuseruiaccess): impostare su *Sì* per bloccare l'accesso dell'utente finale all'interfaccia utente di Microsoft Defender nel dispositivo.  

  **Impostazione predefinita**: Sì

- **Ora di inizio analisi rapida**  
  [Defender/ScheduleQuickScanTime](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-schedulequickscantime) - Pianifica un'ora del giorno per l'analisi rapida da parte di Defender.  

  **Impostazione predefinita**: 2

## <a name="microsoft-defender-firewall"></a>Microsoft Defender Firewall
Per altre informazioni, vedere [Firewall CSP](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp) (Provider dei servizi di configurazione del firewall) nella documentazione di Windows.

- **Periodo di inattività delle associazioni di sicurezza prima dell'eliminazione** - *MdmStore/Global/SaIdleTime*   
  Le associazioni di sicurezza vengono eliminate dopo che il traffico di rete non viene visualizzato per il numero di secondi specificato.  
  **Impostazione predefinita**: 300

- **File Transfer Protocol** - *MdmStore/Global/DisableStatefulFtp*   
  Blocca il protocollo FTP (File Transfer Protocol) con stato.  
  **Impostazione predefinita**: Sì

- **Accodamento pacchetti** - *MdmStore/Global/EnablePacketQueue*    
  Consente di specificare la modalità di abilitazione del ridimensionamento per il software sul lato ricezione per la ricezione di testo crittografato e l'inoltro di testo normale per lo scenario relativo a gateway con tunnel IPsec. In questo modo si mantiene l'ordine dei pacchetti.  
  **Impostazione predefinita**: Impostazione predefinita dispositivo

- **Profilo dominio del firewall** - *FirewallRules/FirewallRuleName/Profiles*  
  Specifica i profili a cui appartiene la regola: Dominio, Privato o Pubblico. Questo valore rappresenta il profilo per le reti connesse ai domini.  

  Impostazioni disponibili:  
  - **Risposte unicast a broadcast multicast obbligatorie**  
    **Impostazione predefinita**: Sì

  - **Regole per applicazioni autorizzate da Criteri di gruppo unite**  
    **Impostazione predefinita**: Sì

  - **Notifiche in ingresso bloccate**  
    **Impostazione predefinita**: Sì

  - **Regole per porte globali da Criteri di gruppo unite**  
    **Impostazione predefinita**: Sì

  - **Modalità mascheramento bloccata**  
    **Impostazione predefinita**: Sì

  - **Firewall abilitato**  
    **Impostazione predefinita**: Consentito

  - **Regole di sicurezza connessione da Criteri di gruppo non unite**  
    **Impostazione predefinita**: Sì

  - **Regole dei criteri da Criteri di gruppo non unite**  
    **Impostazione predefinita**: Sì

- **Profilo pubblico del firewall** - *FirewallRules/FirewallRuleName/Profiles*  
  Specifica i profili a cui appartiene la regola: Dominio, Privato o Pubblico. Questo valore rappresenta il profilo per le reti pubbliche. Tali reti sono classificate come pubbliche dagli amministratori nell'host del server. La classificazione viene stabilita la prima volta che l'host si connette alla rete. Queste reti sono in genere quelle di aeroporti, bar e altri luoghi pubblici, in cui i peer nella rete o l'amministratore di rete non sono attendibili.  

  Impostazioni disponibili:

  - **Connessioni in ingresso bloccate**  
    **Impostazione predefinita**: Sì 

  - **Risposte unicast a broadcast multicast obbligatorie**  
    **Impostazione predefinita**: Sì  

  - **Modalità mascheramento obbligatoria**  
    **Impostazione predefinita**: Sì 
 
  - **Connessioni in uscita obbligatorie**  
    **Impostazione predefinita**: Sì  

  - **Regole per applicazioni autorizzate da Criteri di gruppo unite**  
    **Impostazione predefinita**: Sì  

  - **Notifiche in ingresso bloccate**  
    **Impostazione predefinita**: Sì  

  - **Regole per porte globali da Criteri di gruppo unite**  
    **Impostazione predefinita**: Sì

  - **Modalità mascheramento bloccata**  
    **Impostazione predefinita**: Sì

  - **Firewall abilitato**  
    **Impostazione predefinita**: Consentito  

  - **Regole di sicurezza connessione da Criteri di gruppo non unite**  
    **Impostazione predefinita**: Sì  

  - **Traffico in ingresso obbligatorio**  
    **Impostazione predefinita**: Sì

  - **Regole dei criteri da Criteri di gruppo non unite**  
    **Impostazione predefinita**: Sì  

- **Profilo privato del firewall** - *FirewallRules/FirewallRuleName/Profiles*  
  Specifica i profili a cui appartiene la regola: Dominio, Privato o Pubblico. Questo valore rappresenta il profilo per le reti private.  

  Impostazioni disponibili: 

  - **Connessioni in ingresso bloccate**  
    **Impostazione predefinita**: Sì

  - **Risposte unicast a broadcast multicast obbligatorie**  
    **Impostazione predefinita**: Sì

  - **Modalità mascheramento obbligatoria**  
    **Impostazione predefinita**: Sì

  - **Connessioni in uscita obbligatorie**  
    **Impostazione predefinita**: Sì

  - **Notifiche in ingresso bloccate**  
    **Impostazione predefinita**: Sì

  - **Regole per porte globali da Criteri di gruppo unite**  
    **Impostazione predefinita**: Sì

  - **Modalità mascheramento bloccata**  
    **Impostazione predefinita**: Sì  

  - **Firewall abilitato**  
    **Impostazione predefinita**: Consentito

  - **Regole per applicazioni autorizzate da Criteri di gruppo non unite**  
    **Impostazione predefinita**: Sì

  - **Regole di sicurezza connessione da Criteri di gruppo non unite**  
    **Impostazione predefinita**: Sì

  - **Traffico in ingresso obbligatorio**  
    **Impostazione predefinita**: Sì

  - **Regole dei criteri da Criteri di gruppo non unite**  
    **Impostazione predefinita**: Sì  

- **Metodo di codifica chiave pre-condivisa del firewall**  
  **Impostazione predefinita**: UTF8

- **Verifica dell'elenco di revoche di certificati**  
  **Impostazione predefinita**: Impostazione predefinita dispositivo

## <a name="web--network-protection"></a>Protezione del Web e della rete  

- **Tipo di protezione di rete**  
  [Defender/EnableNetworkProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection): questo criterio consente di attivare/disattivare la protezione della rete in Microsoft Defender Exploit Guard. La protezione di rete è una funzionalità di Microsoft Defender Exploit Guard che protegge i dipendenti che usano le app dall'accesso a tentativi di phishing, siti che ospitano exploit e contenuti dannosi in Internet. Impedisce anche ai browser di terze parti di connettersi a siti pericolosi.  

  Se impostato su *Abilita* o su *Modalità di controllo*, gli utenti non possono disattivare la protezione della rete ed è possibile usare Microsoft Defender Security Center per visualizzare le informazioni sui tentativi di connessione.  
 
  - L'impostazione *Abilitare* impedisce a utenti e app di connettersi a domini pericolosi.  
  - L'impostazione *Modalità di controllo* non impedisce a utenti e app di connettersi a domini pericolosi.  

  Se l'impostazione è *Definito dall'utente*, agli utenti e alle app non viene impedito di connettersi a domini pericolosi e le informazioni sulle connessioni non sono disponibili in Microsoft Defender Security Center.  

  **Impostazione predefinita**: Modalità di controllo

- **Richiedere SmartScreen per Microsoft Edge**  
  [Browser/AllowSmartScreen](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen): per impostazione predefinita, Microsoft Edge usa Microsoft Defender SmartScreen (attivato) per proteggere gli utenti da potenziali tentativi di phishing e software dannoso. Per impostazione predefinita, questo criterio è abilitato, ovvero è impostato su *Sì*, e impedisce agli utenti di disattivare Microsoft Defender SmartScreen.  Quando il criterio valido per un dispositivo è impostato su Non configurato, gli utenti possono disattivare Microsoft Defender SmartScreen, rimuovendo tuttavia la protezione dal dispositivo.  

  **Impostazione predefinita**: Sì
  
- **Bloccare l'accesso a siti dannosi**  
  [Browser/PreventSmartScreenPromptOverride](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride): per impostazione predefinita, Microsoft Edge consente agli utenti di ignorare gli avvisi di Microsoft Defender SmartScreen sui siti potenzialmente dannosi consentendo agli utenti di continuare a visitare il sito. Se il criterio è abilitato (impostato su *Sì*), Microsoft Edge impedisce agli utenti di ignorare gli avvisi e impedisce loro di continuare a visitare il sito.  

  **Impostazione predefinita**: Sì

- **Bloccare il download di file non verificati**  
  [Browser/PreventSmartScreenPromptOverrideForFiles](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles): per impostazione predefinita, Microsoft Edge consente agli utenti di ignorare gli avvisi di Microsoft Defender SmartScreen sui file potenzialmente dannosi, consentendo loro di continuare a scaricare file non verificati. Se questo criterio è abilitato (impostato su *Sì*), gli utenti non possono ignorare gli avvisi né scaricare file non verificati.  

  **Impostazione predefinita**: Sì

## <a name="windows-hello-for-business"></a>Windows Hello for Business  

Per altre informazioni, vedere [PassportForWork CSP](https://docs.microsoft.com/windows/client-management/mdm/passportforwork-csp) (Provider dei servizi di configurazione - PassportForWork) nella documentazione di Windows.

- **Configura Windows Hello for Business** - *IDTenant/Criteri/UsePassportForWork*    
  Windows Hello for Business è un metodo alternativo per l'accesso a Windows che prevede la sostituzione di password, smart card e smart card virtuali.  


  > [!IMPORTANT]
  > Le opzioni per questa impostazione sono invertite rispetto al significato implicito. Essendo invertito, il valore *Sì* non abilita Windows Hello e viene invece considerato come *Non configurato*. Con l'impostazione *Non configurato*, Windows Hello viene abilitato nei dispositivi che ricevono questa baseline.
  >
  > Le descrizioni seguenti sono state modificate per riflettere questo comportamento. L'inversione delle impostazioni verrà corretta in un aggiornamento futuro di questa baseline di sicurezza.

  - Con l'impostazione *Non configurato* Windows Hello viene abilitato e il dispositivo esegue il provisioning di Windows Hello for Business.
  - Con l'impostazione *Sì* la baseline non influisce sull'impostazione di criteri del dispositivo. Ciò significa che se Windows Hello for Business è disabilitato in un dispositivo, rimane disabilitato. Se è abilitato, rimane abilitato.
  <!-- expected behavior 
  - When set to *Yes*, you  enable this policy and the device provisions Windows Hello for Business.  
  - When set to *Not configured*, the baseline does not affect the policy setting of the device. This means that if Windows Hello for Business is disabled on a device, it remains disabled. If its enabled, it remains enabled. 
  -->

  Non è possibile disabilitare Windows Hello for Business tramite questa baseline. È possibile disabilitare Windows Hello for Business quando si configura la [registrazione di Windows](windows-hello.md) o come parte di un profilo di configurazione del dispositivo per la [protezione delle identità](identity-protection-configure.md).  

Windows Hello for Business è un metodo alternativo per l'accesso a Windows che prevede la sostituzione di password, smart card e smart card virtuali.  

  Se si abilita o non si configura questo criterio, il dispositivo esegue il provisioning di Windows Hello for Business. Se si disabilita questo criterio, il dispositivo non effettua il provisioning di Windows Hello for Business per alcun utente.

  Intune non supporta la disabilitazione di Windows Hello. In alternativa, è possibile impostare il criterio per abilitare Windows Hello for Business (Sì) o per non configurare Windows Hello direttamente (Non configurato). Se il criterio non è configurato, un dispositivo può ricevere la configurazione tramite altri criteri, che possono abilitare o disabilitare questa funzionalità.  

  **Impostazione predefinita**: Sì  

- **Richiedi lettere minuscole nel PIN** - *IDTenant/Criteri/PINComplexity/LowercaseLetters*  
  **Impostazione predefinita**: Consentito  

- **Richiedi caratteri speciali nel PIN** - *IDTenant/Criteri/PINComplexity/SpecialCharacters*  
  **Impostazione predefinita**: Consentito  

- **Richiedi lettere maiuscole nel PIN** - *TenantId/Policies/PINComplexity/UppercaseLetters*   
  **Impostazione predefinita**: Consentito  

