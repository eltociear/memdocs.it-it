---
title: Impostazioni delle baseline di sicurezza di Intune per Microsoft Defender Advanced Threat Protection
titleSuffix: Microsoft Intune
description: Impostazioni della baseline di sicurezza supportate da Intune per la gestione di Microsoft Defender Advanced Threat Protection
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/06/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: laarrizz
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
zone_pivot_groups: atp-baseline-versions
ms.openlocfilehash: 322e3be8e7421b0c622a8e656a3312791ed7feac
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/26/2020
ms.locfileid: "88913444"
---
<!-- Pivots in use: 
::: zone pivot="atp-april-2020"
::: zone-end

::: zone pivot="atp-march-2020"
::: zone-end

::: zone pivot="atp-march-2020,atp-april-2020"
::: zone-end
-->

# <a name="microsoft-defender-advanced-threat-protection-baseline-settings-for-intune"></a>Impostazioni della baseline di Microsoft Defender Advanced Threat Protection per Intune

Vedere le impostazioni della baseline di Microsoft Defender Advanced Threat Protection supportate da Microsoft Intune. Le impostazioni predefinite della baseline di Advanced Threat Protection (ATP) rappresentano la configurazione consigliata per ATP e potrebbero non corrispondere ai valori predefiniti della baseline per altre baseline di sicurezza.

::: zone pivot="atp-april-2020"

I dettagli in questo articolo si applicano alla versione 4 della baseline di Microsoft Defender ATP, rilasciata il 21 aprile 2020. Per informazioni su cosa è cambiato in questa versione della baseline rispetto alle versioni precedenti, usare l'azione [Compare baselines](../protect/security-baselines.md#compare-baseline-versions) (Confronta baseline) disponibile quando si visualizza il riquadro *Versioni* per questa baseline.

::: zone-end
::: zone pivot="atp-march-2020"

I dettagli in questo articolo si applicano alla versione 3 della baseline di Microsoft Defender ATP, rilasciata il 1° marzo 2020. Per informazioni su cosa è cambiato in questa versione della baseline rispetto alle versioni precedenti, usare l'azione [Compare baselines](../protect/security-baselines.md#compare-baseline-versions) (Confronta baseline) disponibile quando si visualizza il riquadro *Versioni* per questa baseline.

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"


La baseline di Microsoft Defender Advanced Threat Protection è disponibile quando l'ambiente soddisfa i prerequisiti per l'uso di [Microsoft Defender Advanced Threat Protection](advanced-threat-protection.md#prerequisites).

Questa baseline è ottimizzata per i dispositivi fisici e attualmente se ne sconsiglia l'uso in macchine virtuali (VM) o endpoint VDI. Alcune impostazioni di base possono influire sulle sessioni interattive remote negli ambienti virtualizzati. Per altre informazioni, vedere [Incremento della conformità alla baseline di sicurezza di Microsoft Defender ATP](/windows/security/threat-protection/microsoft-defender-atp/configure-machines-security-baseline) nella documentazione di Windows.


## <a name="application-guard"></a>Application Guard

Per altre informazioni, vedere [WindowsDefenderApplicationGuard CSP](/windows/client-management/mdm/windowsdefenderapplicationguard-csp) (Provider dei servizi di configurazione di WindowsDefenderApplicationGuard) nella documentazione di Windows.  

Quando si usa Microsoft Edge, Microsoft Defender Application Guard protegge l'ambiente dai siti non considerati attendibili dall'organizzazione. Quando gli utenti visitano siti non elencati nei limiti della rete isolata, tali siti vengono aperti in una sessione del browser virtuale di Hyper-V. I siti attendibili sono definiti da un limite di rete.  

- **Attiva Application Guard per Microsoft Edge (opzioni)**  
  CSP: [Settings/AllowWindowsDefenderApplicationGuard](https://go.microsoft.com/fwlink/?linkid=872350)
  
  - **Abilitato per Microsoft Edge** (*impostazione predefinita*) - Application Guard apre siti non approvati in un contenitore del browser virtuale di Hyper-V.
  - **Non configurato** - Qualsiasi sito (attendibile e non attendibile) viene aperto nel dispositivo e non in un contenitore virtuale.  
  
  Con l'impostazione *Abilitato per Microsoft Edge* è possibile configurare *Blocca i contenuti esterni da siti approvati non aziendali* e *Comportamento degli Appunti*.

  - **Blocca i contenuti esterni da siti approvati non aziendali**  
    CSP: [Settings/BlockNonEnterpriseContent](https://go.microsoft.com/fwlink/?linkid=872352)

    - **Sì** (*impostazione predefinita*) - Impedisce il caricamento del contenuto dai siti Web non approvati.
    - **Non configurato** - I siti non aziendali possono essere aperti nel dispositivo.

  - **Comportamento degli Appunti**  
    CSP: [Settings/ClipboardSettings](https://go.microsoft.com/fwlink/?linkid=872351)

    Consente di scegliere le azioni di copia/incolla consentite tra il computer locale e il browser virtuale di Application Guard. Le opzioni includono:
    - **Non configurato**  
    - **Blocca copia e incolla tra computer e browser** (*impostazione predefinita*) - Blocca entrambi. I dati non possono essere trasferiti tra il PC e il browser virtuale.
    - **Consenti copia e incolla solo dal browser al computer** - I dati non possono essere trasferiti dal PC al browser virtuale.
    - **Consenti copia e incolla solo dal computer al browser** - I dati non possono essere trasferiti dal browser virtuale al PC host.
    - **Consenti copia e incolla tra computer e browser** - Nessun blocco dei contenuti.

- **Criterio di isolamento della rete Windows**  
  CSP: [CSP Criteri - NetworkIsolation](/windows/client-management/mdm/policy-csp-networkisolation)

  Specificare un elenco di *domini di rete*, ovvero le risorse aziendali ospitate nel cloud che Application Guard considera siti aziendali
  - **Configura** (*impostazione predefinita*)
  - **Non configurato**

  Con l'impostazione *Configura* è poi possibile definire i *Domini di rete*.

  - **Domini di rete**  
    Selezionare **Aggiungi** e specificare i domini, gli intervalli di indirizzi IP e i limiti di rete. Per impostazione predefinita, viene configurato il dominio *securitycenter.windows.com*.

## <a name="bitlocker"></a>BitLocker

Per altre informazioni, vedere [Impostazioni di Criteri di gruppo per BitLocker](/windows/security/information-protection/bitlocker/bitlocker-group-policy-settings) nella documentazione di Windows.

- **Richiedi la crittografia delle schede di memoria (solo dispositivi mobili)**  
  CSP: [RequireStorageCardEncryption](https://go.microsoft.com/fwlink/?linkid=872524)

  Questa impostazione si applica solo ai dispositivi con SKU Windows Mobile e Mobile Enterprise.
  - **Sì** (*impostazione predefinita*) - La crittografia delle schede di memoria è obbligatoria per i dispositivi mobili.
  - **Non configurato** - Viene ripristinata l'impostazione predefinita del sistema operativo, che non richiede la crittografia delle schede di memoria.

  > [!NOTE]
  > Il supporto per [Windows 10 Mobile](https://support.microsoft.com/help/4485197/windows-10-mobile-end-of-support-faq) e [Windows Phone 8.1](https://support.microsoft.com/help/4036480/windows-phone-8-1-end-of-support-faq) è terminato ad agosto 2020.

- **Abilita la crittografia completa del disco per le unità del sistema operativo e le unità dati fisse**  
  CSP: [RequireDeviceEncryption](https://go.microsoft.com/fwlink/?linkid=872523)

  Se l'unità è stata crittografata prima dell'applicazione di questo criterio, non viene eseguita alcuna azione aggiuntiva. Se le opzioni e il metodo di crittografia corrispondono a quelli di questo criterio, la configurazione dovrebbe avere esito positivo. Se un'opzione di configurazione BitLocker attiva non corrisponde a questo criterio, la configurazione restituirà probabilmente un errore.
  
  Per applicare questo criterio a un disco già crittografato, decrittografare l'unità e riapplicare i criteri MDM. L'impostazione predefinita di Windows non richiede la crittografia unità BitLocker, tuttavia per la registrazione o l'accesso con aggiunta ad Azure AD e account Microsoft (MSA) potrebbe essere applicata automaticamente la crittografia abilitando BitLocker con crittografia XTS-AES a 128 bit.

  - **Sì** (*impostazione predefinita*) - Impone l'uso di BitLocker.
  - **Non configurato** - BitLocker non viene imposto.

- **Criterio Unità di sistema BitLocker**  
  [Impostazioni di Criteri di gruppo di BitLocker](https://go.microsoft.com/fwlink/?linkid=2067025)

  - **Configura** (*impostazione predefinita*)
  - **Non configurato**

  Con l'impostazione *Configura* è poi possibile configurare l'impostazione *Configura il metodo di crittografia per le unità del sistema operativo*.

  - **Configura il metodo di crittografia per le unità del sistema operativo**  
    CSP: [EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  
    Questa impostazione è disponibile quando *BitLocker - Impostazioni dell'unità di sistema* è impostato su *Configura*.  

    Configurare il metodo di crittografia e il livello di codifica per le unità di sistema.  *XTS-AES a 128 bit* è il metodo di crittografia predefinito di Windows e il valore consigliato.

    - **Non configurato** (*impostazione predefinita*)
    - **AES 128bit CBC**
    - **AES 256bit CBC**
    - **AES 128bit XTS**
    - **AES 256bit XTS**

- **BitLocker - Impostazioni dell'unità fissa**  
  [Impostazioni di Criteri di gruppo di BitLocker](https://go.microsoft.com/fwlink/?linkid=2067018)

  - **Configura** (*impostazione predefinita*)
  - **Non configurato**

  Con l'impostazione *Configura* è poi possibile configurare *Blocca l'accesso in scrittura alle unità dati fisse non protette tramite BitLocker* e *Configura il metodo di crittografia per le unità dati fisse*.

  - **Blocca l'accesso in scrittura alle unità dati fisse non protette tramite BitLocker**  
    CSP: [FixedDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872534)  
    Questa impostazione è disponibile quando *BitLocker - Impostazioni dell'unità fissa* è impostato su *Configura*.

    - **Non configurato** (*impostazione predefinita*) - I dati possono essere scritti in unità fisse non crittografate.
    - **Sì** - Windows non consente la scrittura di dati in unità fisse non protette da BitLocker. Se un'unità fissa non è crittografata, l'utente dovrà completare la configurazione guidata di BitLocker per l'unità prima che venga concesso l'accesso in scrittura.

  - **Configura il metodo di crittografia per le unità dati fisse**  
    CSP: [EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  
    Questa impostazione è disponibile quando *BitLocker - Impostazioni dell'unità fissa* è impostato su *Configura*.

    Configurare il metodo di crittografia e il livello di codifica per i dischi di unità dati fisse. *XTS-AES a 128 bit* è il metodo di crittografia predefinito di Windows e il valore consigliato.

    - **Non configurato** (*impostazione predefinita*)
    - **AES 128bit CBC**
    - **AES 256bit CBC**
    - **AES 128bit XTS**
    - **AES 256bit XTS**

- **BitLocker - Impostazioni dell'unità rimovibile**  
  [Impostazioni di Criteri di gruppo di BitLocker](https://go.microsoft.com/fwlink/?linkid=2067140)

  - **Configura** (*impostazione predefinita*)
  - **Non configurato**

  Con l'impostazione *Configura* è poi possibile configurare *Configura il metodo di crittografia per le unità dati rimovibili* e *Blocca l'accesso in scrittura alle unità dati rimovibili non protette tramite BitLocker*.

  - **Configura il metodo di crittografia per le unità dati rimovibili**  
    CSP: [EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  
    Questa impostazione è disponibile quando *BitLocker - Impostazioni dell'unità rimovibile* è impostato su *Configura*.

    Configurare il metodo di crittografia e il livello di codifica per i dischi di unità dati rimovibili. *XTS-AES a 128 bit* è il metodo di crittografia predefinito di Windows e il valore consigliato.

    - **Non configurato**
    - **AES 128bit CBC**
    - **AES 256bit CBC** (*impostazione predefinita*)
    - **AES 128bit XTS**
    - **AES 256bit XTS**

  - **Blocca l'accesso in scrittura alle unità dati rimovibili non protette tramite BitLocker**  
    CSP: [RemovableDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872540)  
    Questa impostazione è disponibile quando *BitLocker - Impostazioni dell'unità rimovibile* è impostato su *Configura*.

    - **Non configurato** (*impostazione predefinita*) - I dati possono essere scritti in unità rimovibili non crittografate.  
    - **Sì** - Windows non consente la scrittura di dati in unità rimovibili non protette da BitLocker. Se un'unità rimovibile non è crittografata, l'utente deve completare la configurazione guidata di BitLocker per l'unità prima che venga concesso l'accesso in scrittura.

## <a name="browser"></a>Browser

- **Richiedere SmartScreen per Microsoft Edge**  
  CSP: [Browser/AllowSmartScreen](https://go.microsoft.com/fwlink/?linkid=2067029)

  - **Sì** (*impostazione predefinita*) - Usare SmartScreen per proteggere gli utenti da potenziali tentativi di phishing e da software dannoso.
  - **Non configurato**

- **Bloccare l'accesso a siti dannosi**  
  CSP: [Browser/PreventSmartScreenPromptOverride](https://go.microsoft.com/fwlink/?linkid=2067040)  

  - **Sì** (*impostazione predefinita*) - Impedisce agli utenti di ignorare gli avvisi del filtro Microsoft Defender SmartScreen e di accedere al sito.
  - **Non configurato**

- **Bloccare il download di file non verificati**  
  CSP: [Browser/PreventSmartScreenPromptOverrideForFiles](https://go.microsoft.com/fwlink/?linkid=2067023)  

  - **Sì** (*impostazione predefinita*) - Impedisce agli utenti di ignorare gli avvisi del filtro Microsoft Defender SmartScreen e di scaricare file non verificati.
  - **Non configurato**

## <a name="data-protection"></a>Protezione dati

- **Blocca l'accesso diretto alla memoria**  
  CSP: [DataProtection/AllowDirectMemoryAccess](https://go.microsoft.com/fwlink/?linkid=2067031)  

  L'impostazione di questo criterio viene applicata solo quando è abilitato BitLocker o la crittografia del dispositivo.

  - **Sì** (*impostazione predefinita*) - Impedisce l'accesso diretto alla memoria (Direct Memory Access, DMA) per tutte le porte downstream PCI collegabili a caldo finché un utente non accede a Windows. Dopo l'accesso di un utente, Windows enumera i dispositivi PCI connessi alle porte PCI collegabili a caldo. Ogni volta che l'utente blocca il computer, l'accesso diretto alla memoria viene bloccato sulle porte PCI collegabili a sistema acceso senza dispositivi figlio finché l'utente non accede di nuovo. I dispositivi già enumerati quando il computer era sbloccato continueranno a funzionare fino a quando non saranno scollegati.
  - **Non configurato**

## <a name="device-guard"></a>Device Guard  

- **Attiva Credential Guard**  
  CSP: [DeviceGuard/ConfigureSystemGuardLaunch](https://go.microsoft.com/fwlink/?linkid=872424)

  Credential Guard usa Windows Hypervisor per fornire protezioni e ciò richiede che l'avvio protetto e le protezioni DMA siano funzionanti e che siano soddisfatti specifici requisiti hardware.

  - **Non configurato** - Disabilita l'uso di Credential Guard, che è l'impostazione predefinita di Windows.
  - **Abilita con blocco UEFI** (*impostazione predefinita*) - Abilita Credential Guard e non ne consente la disabilitazione remota, perché la configurazione di UEFI permanente deve essere cancellata manualmente.
  - **Abilita senza blocco UEFI** - Abilita Credential Guard e ne consente la disattivazione senza accesso fisico al computer.

## <a name="device-installation"></a>Installazione di dispositivi

- **Installazione di dispositivi hardware per identificatori di dispositivo**  
  [DeviceInstallation/PreventInstallationOfMatchingDeviceIDs](https://go.microsoft.com/fwlink/?linkid=2066794)  
  
  L'impostazione di questo criterio consente di specificare un elenco di ID hardware Plug and Play e ID compatibili per i dispositivi la cui installazione non è consentita in Windows. L'impostazione di questo criterio ha la precedenza su qualsiasi altra impostazione di criteri che consente a Windows di installare un dispositivo.  Se si abilita l'impostazione di questo criterio in un server desktop remoto, l'impostazione del criterio influirà sul reindirizzamento dei dispositivi specificati da un client desktop remoto al server desktop remoto.

  - **Non configurato**
  - **Consenti l'installazione del dispositivo hardware** - I dispositivi possono essere installati o aggiornati in base a quanto consentito o impedito da altre impostazioni di criteri.
  - **Blocca l'installazione del dispositivo hardware** (*impostazione predefinita*) - A Windows non è consentito installare un dispositivo il cui ID hardware o ID compatibile viene visualizzato in un elenco definito dall'utente.

  Con l'impostazione *Blocca l'installazione del dispositivo hardware* è possibile configurare *Rimuovi i dispositivi hardware corrispondenti* e *Identificatori dei dispositivi hardware bloccati*.

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

## <a name="dma-guard"></a>DMA Guard

- **Enumerazione di dispositivi esterni non compatibili con la protezione DMA del kernel**  
  CSP: [DmaGuard/DeviceEnumerationPolicy](/windows/client-management/mdm/policy-csp-dmaguard#dmaguard-deviceenumerationpolicy)

  Questo criterio può offrire ulteriore sicurezza nei confronti di dispositivi esterni idonei per DMA. Consente inoltre maggiore controllo sull'enumerazione di dispositivi esterni idonei per DMA non compatibili con il remapping e/o l'isolamento e il sandboxing della memoria del dispositivo.
  
  Questo criterio viene applicato solo quando la protezione DMA del kernel è supportata e abilitata dal firmware del sistema. La protezione DMA del kernel è una funzionalità della piattaforma che deve essere supportata dal sistema al momento della produzione. Per verificare se il sistema supporta la protezione DMA del kernel, controllare il campo della protezione DMA del kernel nella pagina di riepilogo di MSINFO32.exe.

  - **Non configurato** - (*impostazione predefinita*)
  - **Blocca tutto**
  - **Consenti tutto**

## <a name="endpoint-detection-and-response"></a>Rilevamento endpoint e risposta

Per altre informazioni sulle impostazioni seguenti, vedere [Provider dei servizi di configurazione WindowsAdvancedThreatProtection](/windows/client-management/mdm/windowsadvancedthreatprotection-csp) nella documentazione di Windows.

- **Condivisione di esempi per tutti i file**  
  CSP: [Configuration/SampleSharing](/windows/client-management/mdm/windowsadvancedthreatprotection-csp)

  Restituisce o imposta il parametro di configurazione per la condivisione di esempi di Microsoft Defender Advanced Threat Protection.  
  
  - **Sì** (*impostazione predefinita*)
  - **Non configurato**

- **Accelera la frequenza di creazione di report di telemetria**  
  CSP: [Configuration/TelemetryReportingFrequency](/windows/client-management/mdm/windowsadvancedthreatprotection-csp)

  Consente di accelerare la frequenza di creazione di report di telemetria di Microsoft Defender Advanced Threat Protection.  

  - **Sì** (*impostazione predefinita*)
  - **Non configurato**

## <a name="firewall"></a>Firewall

Per altre informazioni, vedere [Firewall CSP](/windows/client-management/mdm/firewall-csp) (Provider dei servizi di configurazione del firewall) nella documentazione di Windows.

- **Disabilita FTP (File Transfer Protocol) con stato**  
  CSP: [MdmStore/Global/DisableStatefulFtp](https://go.microsoft.com/fwlink/?linkid=872536)  

  - **Sì** (*impostazione predefinita*)
  - **Non configurato** - Il firewall userà FTP per esaminare e filtrare le connessioni di rete secondarie. È quindi possibile che le regole del firewall vengono ignorate.

- **Numero di secondi per cui un'associazione di sicurezza può rimanere inattiva prima di essere eliminata**  
CSP: [MdmStore/Global/SaIdleTime](https://go.microsoft.com/fwlink/?linkid=872539)

  Specificare per quanto tempo le associazioni di sicurezza vengono mantenute dopo che il traffico di rete non viene più visualizzato. Quando non è configurato, il sistema elimina un'associazione di sicurezza dopo che è rimasta inattiva per *300* secondi (impostazione predefinita).
  
  Il numero deve essere compreso tra **300** e **3600** secondi.

- **Codifica chiave già condivisa**  
  CSP: [MdmStore/Global/PresharedKeyEncoding](https://go.microsoft.com/fwlink/?linkid=872541)

   Se la codifica UTF-8 non è richiesta, le chiavi già condivise verranno inizialmente codificate con UTF-8. Successivamente, gli utenti del dispositivo possono scegliere un altro metodo di codifica.

  - **Non configurato**
  - **Nessuno**
  - **UTF8** (*impostazione predefinita*)

- **Verifica dell'elenco di revoche di certificati**  
  CSP: [MdmStore/Global/CRLcheck](https://go.microsoft.com/fwlink/?linkid=872548)

  Specificare come applicare la verifica dell'elenco di revoche di certificati.  

  - **Non configurato** (*impostazione predefinita*) -La verifica dell'elenco di revoche di certificati è disabilitata.
  - **Nessuno**
  - **Tentativo**
  - **Richiedi**

- **Accodamento di pacchetti**  
  CSP: [MdmStore/Global/EnablePacketQueue](https://go.microsoft.com/fwlink/?linkid=872551)

  Consente di specificare la modalità di abilitazione del ridimensionamento per il software sul lato ricezione per la ricezione di testo crittografato e l'inoltro di testo normale per lo scenario relativo a gateway con tunnel IPsec. Questa impostazione assicura il mantenimento dell'ordine dei pacchetti.

  - **Non configurato** (*impostazione predefinita*) - Viene ripristinata l'impostazione predefinita del client per l'accodamento di pacchetti, ovvero disabilitato.
  - **Disabilitato**
  - **Accoda in ingresso**
  - **Accoda in uscita**
  - **Accoda entrambi**

- **Profilo privato del firewall**  
  [2.2.2 FW_PROFILE_TYPE](https://go.microsoft.com/fwlink/?linkid=2067041)

  - **Configura** (*impostazione predefinita*)
  - **Non configurato**

  Con l'impostazione *Configura* è possibile configurare le impostazioni aggiuntive seguenti.

  - **Connessioni in ingresso bloccate**  
    CSP: [/DefaultInboundAction](https://go.microsoft.com/fwlink/?linkid=872564)

    - **Sì** (*impostazione predefinita*)
    - **Non configurato**

  - **Risposte unicast a broadcast multicast obbligatorie**  
    CSP: [/DisableUnicastResponsesToMulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)

    - **Sì** (*impostazione predefinita*)
    - **Non configurato**

  - **Modalità mascheramento obbligatoria**  
    CSP: [/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **Sì** (*impostazione predefinita*)
    - **Non configurato**

  - **Connessioni in uscita obbligatorie**  
    CSP: [/DefaultOutboundAction](https://aka.ms/intune-firewall-outboundaction)

    - **Sì** (*impostazione predefinita*)
    - **Non configurato**

  - **Notifiche in ingresso bloccate**  
    CSP: [/DisableInboundNotifications](https://go.microsoft.com/fwlink/?linkid=872563)

    - **Sì** (*impostazione predefinita*)
    - **Non configurato**

  - **Regole per porte globali da Criteri di gruppo unite**  
    CSP: [/GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)

    - **Sì** (*impostazione predefinita*)
    - **Non configurato**

  - **Modalità mascheramento bloccata**  
    CSP: [/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **Sì** (*impostazione predefinita*)
    - **Non configurato**

  - **Firewall abilitato**  
    CSP: [/EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

    - **Non configurato**
    - **Bloccato**
    - **Consentito** (*impostazione predefinita*)

  - **Regole per applicazioni autorizzate da Criteri di gruppo non unite**  
    CSP: [/AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)

    - **Sì** (*impostazione predefinita*)
    - **Non configurato**

  - **Regole di sicurezza connessione da Criteri di gruppo non unite**  
    CSP: [/AllowLocalIpsecPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872568)

    - **Sì** (*impostazione predefinita*)
    - **Non configurato**

  - **Traffico in ingresso obbligatorio**  
    CSP: [/Shielded](https://go.microsoft.com/fwlink/?linkid=872561)

    - **Sì** (*impostazione predefinita*)
    - **Non configurato**

  - **Regole dei criteri da Criteri di gruppo non unite**  
    CSP: [/AllowLocalPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872567)

    - **Sì** (*impostazione predefinita*)
    - **Non configurato**

- **Profilo pubblico del firewall**  
  [2.2.2 FW_PROFILE_TYPE](https://go.microsoft.com/fwlink/?linkid=2067143)

  - **Configura** (*impostazione predefinita*)
  - **Non configurato**

  Con l'impostazione *Configura* è possibile configurare le impostazioni aggiuntive seguenti.

  - **Connessioni in ingresso bloccate**  
    CSP: [/DefaultInboundAction](https://go.microsoft.com/fwlink/?linkid=872564)

    - **Sì** (*impostazione predefinita*)
    - **Non configurato**

  - **Risposte unicast a broadcast multicast obbligatorie**  
    CSP: [/DisableUnicastResponsesToMulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)

    - **Sì** (*impostazione predefinita*)
    - **Non configurato**

  - **Modalità mascheramento obbligatoria**  
    CSP: [/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **Sì** (*impostazione predefinita*)
    - **Non configurato**

  - **Connessioni in uscita obbligatorie**  
    CSP: [/DefaultOutboundAction](https://aka.ms/intune-firewall-outboundaction)

    - **Sì** (*impostazione predefinita*)
    - **Non configurato**

  - **Regole per applicazioni autorizzate da Criteri di gruppo non unite**  
    CSP: [/AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)

    - **Sì** (*impostazione predefinita*)
    - **Non configurato**

  - **Notifiche in ingresso bloccate**  
    CSP: [/DisableInboundNotifications](https://go.microsoft.com/fwlink/?linkid=872563)

    - **Sì** (*impostazione predefinita*)
    - **Non configurato**

  - **Regole per porte globali da Criteri di gruppo unite**  
    CSP: [/GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)

    - **Sì** (*impostazione predefinita*)
    - **Non configurato**

  - **Modalità mascheramento bloccata**  
    CSP: [/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **Sì** (*impostazione predefinita*)
    - **Non configurato**

  - **Firewall abilitato**  
    CSP: [/EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

    - **Non configurato**
    - **Bloccato**
    - **Consentito** (*impostazione predefinita*)

  - **Regole di sicurezza connessione da Criteri di gruppo non unite**  
    CSP: [/AllowLocalIpsecPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872568)

    - **Sì** (*impostazione predefinita*)
    - **Non configurato**

  - **Traffico in ingresso obbligatorio**  
    CSP: [/Shielded](https://go.microsoft.com/fwlink/?linkid=872561)

    - **Sì** (*impostazione predefinita*)
    - **Non configurato**

  - **Regole dei criteri da Criteri di gruppo non unite**  
    CSP: [/AllowLocalPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872567)

    - **Sì** (*impostazione predefinita*)
    - **Non configurato**

- **Profilo di dominio del firewall**  
  CSP: [2.2.2 FW_PROFILE_TYPE](https://go.microsoft.com/fwlink/?linkid=2066796)

  - **Risposte unicast a broadcast multicast obbligatorie**  
    CSP: [/DisableUnicastResponsesToMulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)

  - **Regole per applicazioni autorizzate da Criteri di gruppo non unite**  
    CSP: [/AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)

    - **Sì** (*impostazione predefinita*)
    - **Non configurato**  

  - **Notifiche in ingresso bloccate**  
    CSP: [/DisableInboundNotifications](https://go.microsoft.com/fwlink/?linkid=872563)

    - **Sì** (*impostazione predefinita*)
    - **Non configurato**

  - **Regole per porte globali da Criteri di gruppo unite**  
    CSP: [/GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)

    - **Sì** (*impostazione predefinita*)
    - **Non configurato**

  - **Modalità mascheramento bloccata**  
    CSP: [/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **Sì** (*impostazione predefinita*)
    - **Non configurato**

  - **Firewall abilitato**  
    CSP: [/EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

    - **Non configurato**
    - **Bloccato**
    - **Consentito** (*impostazione predefinita*)

  - **Regole di sicurezza connessione da Criteri di gruppo non unite**  
    CSP: [/AllowLocalIpsecPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872568)

    - **Sì** (*impostazione predefinita*)
    - **Non configurato**

  - **Regole dei criteri da Criteri di gruppo non unite**  
    CSP: [/AllowLocalPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872567)

    - **Sì** (*impostazione predefinita*)
    - **Non configurato**

## <a name="microsoft-defender"></a>Microsoft Defender

- **Esegui l'analisi veloce giornaliera alle ore**  
  CSP: [Defender/ScheduleQuickScanTime](https://go.microsoft.com/fwlink/?linkid=2114053&clcid=0x409)
  
   Configurare quando viene eseguita l'analisi veloce giornaliera. Per impostazione predefinita, l'esecuzione dell'analisi è impostata sulle **2**.

- **Ora di inizio analisi pianificata**  
  
  Per impostazione predefinita, il valore è impostato sulle **2**.

- **Configura la priorità bassa per la CPU per le analisi pianificate**  
  CSP: [Defender/EnableLowCPUPriority](/windows/client-management/mdm/policy-csp-defender#defender-enablelowcpupriority)  

  -**Sì** (*impostazione predefinita*)
  - **Non configurato**

- **Impedisci alle app di comunicazione di Office di creare processi figlio**  
  [Proteggere i dispositivi dagli exploit](https://go.microsoft.com/fwlink/?linkid=874499)  

  Questa regola di ASR viene controllata tramite il GUID seguente: 26190899-1602-49e8-8b27-eb1d0a1ce869.
  - **Non configurato** - Viene ripristinata l'impostazione predefinita di Windows che non blocca la creazione di processi figlio.
  - **Definito dall'utente**
  - **Abilita** (*impostazione predefinita*) - Le applicazioni di comunicazione di Office non possono creare processi figlio.
  - **Modalità di controllo** - Vengono generati eventi Windows anziché bloccare i processi figlio.

- **Block Adobe Reader from creating child processes** (Impedisci ad Adobe Reader di creare processi figlio)  
  [Ridurre le superfici di attacco con le regole di riduzione della superficie di attacco](https://go.microsoft.com/fwlink/?linkid=853979)  

  - **Non configurato** - Viene ripristinata l'impostazione predefinita di Windows che non blocca la creazione di processi figlio.
  - **Definito dall'utente**
  - **Abilita** (*impostazione predefinita*) -La creazione di processi figlio è bloccata da Adobe Reader.
  - **Modalità di controllo** - Vengono generati eventi Windows anziché bloccare i processi figlio.

- **Analizza i messaggi di posta elettronica in ingresso**  
  CSP: [Defender/AllowEmailScanning](https://go.microsoft.com/fwlink/?linkid=2114052&clcid=0x409)

  - **Sì** (*impostazione predefinita*) - Vengono analizzati le cassette postali e i file di posta elettronica, ad esempio PST, DBX, MNX, MIME e BINHEX.
  - **Non configurato** - Con questa impostazione viene ripristinata l'impostazione predefinita del client, ovvero i file di posta elettronica che non vengono analizzati.

- **Attiva protezione in tempo reale**  
  CSP: [Defender/AllowRealtimeMonitoring](https://go.microsoft.com/fwlink/?linkid=2114050&clcid=0x409)

  - **Sì** (*impostazione predefinita*) - Il monitoraggio in tempo reale viene applicato e l'utente non può disabilitarlo.
  - **Non configurato** - Viene ripristinata l'impostazione predefinita del client, ovvero attivata, ma l'utente può modificarla. Per disabilitare il monitoraggio in tempo reale, usare un URI personalizzato.

- **Numero di giorni (0-90) per la conservazione del malware in quarantena**  
  CSP: [Defender/DaysToRetainCleanedMalware](https://go.microsoft.com/fwlink/?linkid=2114055&clcid=0x409)

  Configurare il numero di giorni di mantenimento degli elementi nella cartella di quarantena, prima della rimozione. Il valore predefinito è zero (**0**), ovvero i file in quarantena non vengono mai rimossi.

- **Defender - Pianificazione analisi del sistema**  
  CSP: [Defender/ScheduleScanDay](/windows/client-management/mdm/policy-csp-defender#defender-schedulescanday)

  Pianificare il giorno in cui Defender analizza i dispositivi. Per impostazione predefinita, l'analisi è **Definita dall'utente** ma può essere impostata su *Ogni giorno*, su qualsiasi giorno della settimana o su *Nessuna analisi pianificata*.

- **Quantità di tempo aggiuntiva (0-50 secondi) per l'estensione del timeout di protezione cloud**  
  CSP: [Defender/CloudExtendedTimeout](https://go.microsoft.com/fwlink/?linkid=2113940&clcid=0x409)

  Defender Antivirus blocca automaticamente i file sospetti per 10 secondi, in modo da poter analizzare i file nel cloud e assicurarsi che siano sicuri. Con questa impostazione è possibile aggiungere fino a 50 secondi a questo timeout.  L'impostazione predefinita del timeout è zero (**0**).

- **Analizza le unità di rete mappate durante un'analisi completa**  
  CSP: [Defender/AllowFullScanOnMappedNetworkDrives](https://go.microsoft.com/fwlink/?linkid=2113945&clcid=0x409)

  - **Sì** (*impostazione predefinita*) - Durante un'analisi completa vengono incluse le unità di rete mappate.
  - **Non configurato** - Viene ripristinata l'impostazione predefinita del cliente, ovvero viene disabilitata l'analisi per le unità di rete mappate.

- **Attiva la protezione di rete**  
  CSP: [Defender/EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=2113939&clcid=0x409)
  
  - **Sì** (*impostazione predefinita*) - Blocca il traffico dannoso rilevato dalle firme in Network Inspection System (NIS).
  - **Non configurato**

- **Analizza tutti i file e gli allegati scaricati**  
  CSP: [Defender/AllowIOAVProtection](https://go.microsoft.com/fwlink/?linkid=2113934&clcid=0x409)

  - **Sì** (*impostazione predefinita*) - Vengono analizzati tutti i file e gli allegati scaricati. Viene ripristinata l'impostazione predefinita del client, ovvero attivata, ma l'utente può modificarla. Per disabilitare questa impostazione, usare un URI personalizzato.
  - **Non configurato** - Viene ripristinata l'impostazione predefinita del client, ovvero attivata, ma l'utente può modificarla. Per disabilitare questa impostazione, usare un URI personalizzato.

::: zone-end
::: zone pivot="atp-april-2020"

- **Blocca la protezione all'accesso**  
  CSP: [Defender/AllowOnAccessProtection](https://go.microsoft.com/fwlink/?linkid=2113935&clcid=0x409)

  - **Sì**
  - **Non configurato** (*impostazione predefinita*)

::: zone-end
::: zone pivot="atp-march-2020"

- **Blocca la protezione all'accesso**  
  CSP: [Defender/AllowOnAccessProtection](https://go.microsoft.com/fwlink/?linkid=2113935&clcid=0x409)

  - **Sì** (*impostazione predefinita*)
  - **Non configurato**

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"

- **Analizza gli script del browser**  
  CSP: [Defender/AllowScriptScanning](https://go.microsoft.com/fwlink/?linkid=2114054&clcid=0x409)

  - **Sì** (*impostazione predefinita*) - La funzionalità di analisi degli script di Microsoft Defender viene applicata e l'utente non può disattivarla.
  - **Non configurato**- Viene ripristinata l'impostazione predefinita del client, ovvero l'analisi degli script è abilitata, tuttavia l'utente può disattivarla.

- **Blocca l'accesso utente all'app Microsoft Defender**  
  CSP: [Defender/AllowUserUIAccess](https://go.microsoft.com/fwlink/?linkid=2114043&clcid=0x409)

  - **Sì** (*impostazione predefinita*)- L'interfaccia utente di Microsoft Defender non è accessibile e le notifiche vengono soppresse.
  - **Non configurato** - Con l'impostazione Sì, l'interfaccia utente di Windows Defender non sarà accessibile e le notifiche verranno soppresse. Con l'impostazione Non configurato verrà ripristinata l'impostazione predefinita del client, ovvero saranno consentite sia l'interfaccia utente che le notifiche.

- **Utilizzo CPU massimo consentito (0-100%) per analisi**  
  CSP: [Defender/AvgCPULoadFactor](https://go.microsoft.com/fwlink/?linkid=2114046&clcid=0x409)

  Specificare come percentuale la quantità massima di CPU da usare per un'analisi. Il valore predefinito è **50**.

- **Tipo di analisi**  
  CSP: [Defender/ScanParameter](https://go.microsoft.com/fwlink/?linkid=2114045&clcid=0x409)

  - **Definito dall'utente**
  - **Disabilitato**
  - **Analisi veloce** (*impostazione predefinita*)
  - **Analisi completa**

- **Immettere la frequenza (0-24 ore) per il controllo della disponibilità di aggiornamenti dell'intelligence sulla sicurezza**  
  CSP: [Defender/SignatureUpdateInterval](https://go.microsoft.com/fwlink/?linkid=2113936&clcid=0x409)

  Specificare la frequenza con cui verificare la presenza di firme aggiornate, in ore. Ad esempio, con il valore 1 il controllo verrà eseguito ogni ora. Se il valore è 2, il controllo viene eseguito ogni due ore e così via.

  Se non viene definito alcun valore, i dispositivi usano l'impostazione predefinita del client, ovvero **8** ore.

- **Consenso per l'invio di campioni di Defender**  
  CSP: [Defender/SubmitSamplesConsent](https://go.microsoft.com/fwlink/?linkid=2067131)

  Verifica il livello di consenso utente in Microsoft Defender per l'invio di dati. Se il consenso necessario è già stato concesso, Microsoft Defender esegue l'invio. In caso contrario (e se l'utente ha specificato che non venga mai inviata una richiesta), viene richiesto il consenso utente (se *Abilita la protezione mediante cloud* è impostata su *Sì*) prima dell'invio dei dati.

  - **Invia i campioni sicuri automaticamente** (*impostazione predefinita*)
  - **Chiedi sempre conferma**
  - **Non inviare mai**
  - **Invia tutti i campioni automaticamente**

- **Livello di protezione fornita dal cloud**  
  CSP: [CloudBlockLevel](https://go.microsoft.com/fwlink/?linkid=2113942)

  Consente di configurare l'aggressività con cui Defender Antivirus deve bloccare e analizzare i file sospetti.
  - **Non configurata** (*impostazione predefinita*): livello di blocco predefinito di Defender.
  - **Alta**: blocco aggressivo degli elementi sconosciuti e ottimizzazione delle prestazioni del client, con una maggiore probabilità di falsi positivi.
  - **Alta +** : blocco aggressivo degli elementi sconosciuti, con misure di protezione aggiuntive che possono influire sulle prestazioni del client.
  - **Tolleranza zero**: blocco di tutti i file eseguibili sconosciuti.

- **Analizza file di archivio**  
  CSP: [Defender/AllowArchiveScanning](https://go.microsoft.com/fwlink/?linkid=2114047&clcid=0x409)

  - **Sì** (*impostazione predefinita*) - Viene applicata l'analisi dei file di archivio, ad esempio file ZIP o CAB.
  - **Non configurata** - Verrà ripristinata l'impostazione predefinita del client, ovvero l'analisi dei file archiviati, ma può essere disabilitata dall'utente.

- **Attiva monitoraggio comportamento**  
  CSP: [Defender/AllowBehaviorMonitoring](https://go.microsoft.com/fwlink/?linkid=2114048&clcid=0x409)

  - **Sì** (*impostazione predefinita*) - Il monitoraggio del comportamento viene applicato e l'utente non può disabilitarlo.
  - **Non configurato** - Viene ripristinata l'impostazione predefinita del client, ovvero attivata, ma l'utente può modificarla. Per disabilitare il monitoraggio in tempo reale, usare un URI personalizzato.
  
- **Analizza le unità rimovibili durante un'analisi completa**  
  CSP: [Defender/AllowFullScanRemovableDriveScanning](https://go.microsoft.com/fwlink/?linkid=2113946&clcid=0x409)

  - **Sì** (*impostazione predefinita*) - Durante un'analisi completa vengono analizzate le unità rimovibili, ad esempio le unità flash USB.
  - **Non configurato** - Viene ripristinata l'impostazione predefinita del client, che analizza le unità rimovibili, tuttavia l'utente può disabilitare questa analisi.
  
- **Analizza file di rete**  
  CSP: [Defender/AllowScanningNetworkFiles](https://go.microsoft.com/fwlink/?linkid=2114049&clcid=0x409)

  - **Sì** (*impostazione predefinita*) - Microsoft Defender analizza i file di rete.
  - **Non configurato** - Viene ripristinata l'impostazione predefinita del client, ovvero viene disabilitata l'analisi dei file di rete.
  
- **Azione della Protezione da applicazioni potenzialmente di Defender**  
  CSP: [Defender/PUAProtection](/windows/client-management/mdm/policy-csp-defender#defender-puaprotection)

  Consente di specificare il livello di rilevamento per le applicazioni potenzialmente indesiderate (PUA, Potentially Unwanted Application). Defender avvisa gli utenti quando è in corso il download o il tentativo di installazione di software potenzialmente indesiderato in un dispositivo.
  - **Impostazione predefinita dispositivo**
  - **Blocca** (*impostazione predefinita*) - Gli elementi rilevati vengono bloccati e visualizzati nella cronologia insieme ad altre minacce.
  - **Controlla** - Defender rileva le applicazioni potenzialmente indesiderate, ma non esegue alcuna azione. È possibile esaminare le informazioni sulle applicazioni per cui Defender avrebbe intrapreso un'azione cercando gli eventi creati in Visualizzatore eventi da Defender.

- **Attiva la protezione fornita dal cloud**  
  CSP: [AllowCloudProtection](/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

  Per impostazione predefinita, nei dispositivi Windows 10 desktop Defender invia informazioni a Microsoft in merito a eventuali problemi riscontrati. Le informazioni vengono analizzate per acquisire altre informazioni sui problemi riscontrati dall'utente e da altri clienti e offrire soluzioni migliorate.

  - **Sì** (*impostazione predefinita*) - La protezione fornita dal cloud è attiva.  Gli utenti dei dispositivi non possono modificare questa impostazione.
  - **Non configurata** -Viene ripristinata l'impostazione predefinita del sistema.

- **Impedisci alle applicazioni di Office di inserire codice in altri processi**  
  [Proteggere i dispositivi dagli exploit](https://go.microsoft.com/fwlink/?linkid=872974)

  Questa regola di ASR viene controllata tramite il GUID seguente: 75668C1F-73B5-4CF0-BB93-3ECF5CB7CC84
  - **Non configurato** - Viene ripristinata l'impostazione predefinita di Windows, ovvero disattivato.
  - **Blocca** (*impostazione predefinita*) - Le applicazioni di Office non possono inserire codice in altri processi.
  - **Modalità di controllo** - Vengono generati eventi di Windows anziché imporre il blocco.

- **Impedisci alle applicazioni di Office di creare contenuto eseguibile**  
  [Proteggere i dispositivi dagli exploit](https://go.microsoft.com/fwlink/?linkid=872975)

  Questa regola di ASR viene controllata tramite il GUID seguente: 3B576869-A4EC-4529-8536-B80A7769E899
  - **Non configurato** - Viene ripristinata l'impostazione predefinita di Windows, ovvero disattivato.
  - **Blocca** (*impostazione predefinita*) - Le applicazioni di Office non possono creare contenuto eseguibile.
  - **Modalità di controllo** - Vengono generati eventi di Windows anziché imporre il blocco.
  
- **Impedisci a JavaScript o VBScript di avviare contenuto eseguibile scaricato**  
  [Proteggere i dispositivi dagli exploit](https://go.microsoft.com/fwlink/?linkid=872979)

   Questa regola di ASR viene controllata tramite il GUID seguente: D3E037E1-3EB8-44C8-A917-57927947596D
  - **Non configurato** - Viene ripristinata l'impostazione predefinita di Windows, ovvero disattivato.
  - **Blocca** (*impostazione predefinita*) - Defender blocca l'esecuzione dei file JavaScript o VBScript scaricati da Internet.
  - **Modalità di controllo** - Vengono generati eventi di Windows anziché imporre il blocco.
  
- **Abilita la protezione di rete**  
  CSP: [Defender/EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=872618)

  - **Non configurato** - Viene ripristinata l'impostazione predefinita di Windows, ovvero disabilitato.
  - **Definito dall'utente**
  - **Abilita** - La protezione della rete è abilitata per tutti gli utenti del sistema.
  - **Modalità di controllo** (*impostazione predefinita*) - Gli utenti non vengono protetti da domini pericolosi e vengono invece generati eventi di Windows.

- **Blocca processi non attendibili e non firmati eseguiti da USB**  
  [Proteggere i dispositivi dagli exploit](https://go.microsoft.com/fwlink/?linkid=874502)

  Questa regola di ASR viene controllata tramite il GUID seguente: b2b3f03d-6a65-4F7B-A9C7-1c7ef74a9ba4
  - **Non configurato** - Viene ripristinata l'impostazione predefinita di Windows, ovvero disattivato.
  - **Blocca** (*impostazione predefinita*) - Vengono bloccati i processi non attendibili e non firmati eseguiti da un'unità USB.
  - **Modalità di controllo** - Vengono generati eventi di Windows anziché imporre il blocco.

- **Blocca il furto di credenziali dal sottosistema dell'autorità di protezione locale di Windows (lsass.exe)**  
  [Proteggere i dispositivi dagli exploit](https://go.microsoft.com/fwlink/?linkid=874499)

  Questa regola di ASR viene controllata tramite il GUID seguente: 9e6c4e1f-7d60-472f-ba1a-a39ef669e4b2
  - **Non configurato** - Viene ripristinata l'impostazione predefinita di Windows, ovvero disattivato.
  - **Definito dall'utente**
  - **Abilita** (*impostazione predefinita*) - Vengono bloccati i tentativi di furto delle credenziali tramite Lsass.exe.
  - **Modalità di controllo** - Gli utenti non vengono protetti da domini pericolosi e vengono invece generati eventi di Windows.

- **Blocca il download di contenuti eseguibili dai client di posta elettronica e posta sul Web**  
  [Proteggere i dispositivi dagli exploit](https://go.microsoft.com/fwlink/?linkid=872980)

  - **Non configurato** - Viene ripristinata l'impostazione predefinita di Windows, ovvero disattivato.
  - **Blocca** (*impostazione predefinita*) - Viene bloccato il contenuto eseguibile scaricato dai client di posta elettronica e posta sul Web.
  - **Modalità di controllo** - Vengono generati eventi di Windows anziché imporre il blocco.

- **Impedisci alle applicazioni di Office di creare processi figlio**  
  [Proteggere i dispositivi dagli exploit](https://go.microsoft.com/fwlink/?linkid=872976)

  Questa regola di ASR viene controllata tramite il GUID seguente: D4F940AB-401B-4EFC-AADC-AD5F3C50688A
  - **Non configurato** - Viene ripristinata l'impostazione predefinita di Windows, ovvero disattivato.
  - **Blocca** (*impostazione predefinita*)
  - **Modalità di controllo** - Vengono generati eventi di Windows anziché imporre il blocco.

- **Blocca l'esecuzione di script potenzialmente offuscati (js/vbs/ps)**  
  [Proteggere i dispositivi dagli exploit](https://go.microsoft.com/fwlink/?linkid=872978)

  Questa regola di ASR viene controllata tramite il GUID seguente: 5BEB7EFE-FD9A-4556-801D-275E5FFC04CC
  - **Non configurato** - Viene ripristinata l'impostazione predefinita di Windows, ovvero disattivato.
  - **Blocca** (*impostazione predefinita*) - Defender impedirà l'esecuzione di script offuscati.
  - **Modalità di controllo** - Vengono generati eventi di Windows anziché imporre il blocco.

- **Blocca le chiamate API Win32 dalle macro di Office**  
  [Proteggere i dispositivi dagli exploit](https://go.microsoft.com/fwlink/?linkid=872977)

  Questa regola di ASR viene controllata tramite il GUID seguente: 92E97FA1-2EDF-4476-BDD6-9DD0B4DDDC7B
  - **Non configurato** - Viene ripristinata l'impostazione predefinita di Windows, ovvero disattivato.
  - **Blocca** (*impostazione predefinita*) - Verrà impedito l'uso di chiamate API Win32 nelle macro di Office.
  - **Modalità di controllo** - Vengono generati eventi di Windows anziché imporre il blocco.

## <a name="microsoft-defender-security-center"></a>Microsoft Defender Security Center

- **Impedisce agli utenti di modificare l'interfaccia di protezione di Exploit Guard**  
  CSP: [WindowsDefenderSecurityCenter/DisallowExploitProtectionOverride](https://go.microsoft.com/fwlink/?linkid=2067239)

  - **Sì** (*impostazione predefinita*) -  Impedisce agli utenti di apportare modifiche nell'area delle impostazioni per la protezione dagli exploit in Microsoft Defender Security Center.
  - **Non configurato** - Gli utenti locali non possono apportare modifiche nell'area delle impostazioni per la protezione dagli exploit.

## <a name="smart-screen"></a>SmartScreen

- **Impedisci agli utenti di ignorare gli avvisi di SmartScreen**  
  CSP: [SmartScreen/PreventOverrideForFilesInShell](https://go.microsoft.com/fwlink/?linkid=872783)

   Questa impostazione richiede che l'opzione "Attiva Windows SmartScreen" sia impostata su Sì.
  - **Sì** (*impostazione predefinita*) - SmartScreen è abilitato e gli utenti non possono ignorare gli avvisi per i file o le app dannose.
  - **Non configurato**  - Gli utenti possono ignorare gli avvisi di SmartScreen per i file e le app dannose.

- **Richiedi app solo dallo Store**  

  - **Sì** (*impostazione predefinita*)
  - **Non configurato**

- **Attiva Windows SmartScreen**  
  CSP: [SmartScreen/EnableSmartScreenInShell](https://go.microsoft.com/fwlink/?linkid=872784)

  - **Sì** (*impostazione predefinita*) - Impone l'uso di SmartScreen per tutti gli utenti.
  - **Non configurato** - Viene ripristinata l'impostazione predefinita di Windows, che prevede l'abilitazione di SmartScreen, tuttavia gli utenti possono modificare questa impostazione. Per disabilitare SmartScreen, usare un URI personalizzato.

## <a name="windows-hello-for-business"></a>Windows Hello for Business

Per altre informazioni, vedere [PassportForWork CSP](/windows/client-management/mdm/passportforwork-csp) (Provider dei servizi di configurazione - PassportForWork) nella documentazione di Windows.

- **Blocca Windows Hello for Business**  

   Windows Hello for Business è un metodo alternativo per l'accesso a Windows che prevede la sostituzione di password, smart card e smart card virtuali.

  - **Non configurato** - I dispositivi effettuano il provisioning di Windows Hello for Business, ovvero l'impostazione predefinita di Windows.
  - **Disabilitato** (*impostazione predefinita*) - I dispositivi effettuano il provisioning di Windows Hello for Business.
  - **Abilitato** - I dispositivi non effettuano il provisioning di Windows Hello for Business per qualsiasi utente.

  Con l'impostazione *Disabilitato* è possibile configurare le impostazioni seguenti:

  - **Lettere minuscole nel PIN**  
    - **Non consentito**
    - **Richiesto**
    - **Consentito** (*impostazione predefinita*)

  - **Caratteri speciali nel PIN**
    - **Non consentito**
    - **Richiesto**
    - **Consentito** (*impostazione predefinita*)

  - **Lettere maiuscole nel PIN**
    - **Non consentito**
    - **Richiesto**
    - **Consentito** (*impostazione predefinita*)

::: zone-end

## <a name="next-steps"></a>Passaggi successivi

- [Informazioni sulle baseline di sicurezza](security-baselines.md)
- [Evitare conflitti](security-baselines.md#avoid-conflicts)
- [Risolvere problemi relativi a criteri e profili in Intune](../configuration/troubleshoot-policies-in-microsoft-intune.md)