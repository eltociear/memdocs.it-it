---
title: Impostazioni di protezione per dispositivi Windows 10 in Microsoft Intune - Azure | Microsoft Docs
description: Nei dispositivi Windows 10 usare o configurare le impostazioni di Endpoint Protection per abilitare le funzionalità di Microsoft Defender, tra cui Application Guard, Firewall, SmartScreen, crittografia e BitLocker, Exploit Guard, controllo di applicazioni, Centro sicurezza e protezione dei dispositivi locali in Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/14/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 3af7c91b-8292-4c7e-8d25-8834fcf3517a
ms.reviewer: mattsha
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 69b4df0b5ceb947ab875f82a0d6f5ac59ce89eef
ms.sourcegitcommit: cb12dd341792c0379bebe9fd5f844600638c668a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/15/2020
ms.locfileid: "88252623"
---
# <a name="windows-10-and-later-settings-to-protect-devices-using-intune"></a>Impostazioni di Windows 10 (e versioni successive) per la protezione dei dispositivi con Intune

Microsoft Intune include diverse impostazioni utili per la protezione dei dispositivi. Questo articolo descrive tutte le impostazioni che è possibile abilitare e configurare nei dispositivi Windows 10 e versioni successive. Queste impostazioni vengono create in un profilo di configurazione di Endpoint Protection in Intune per controllare la sicurezza, inclusi BitLocker e Microsoft Defender.  

Per configurare Antivirus Microsoft Defender, vedere [Impostazioni dei dispositivi Windows 10 (e versioni successive) per consentire o limitare l'uso delle funzionalità tramite Intune](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus).  

## <a name="before-you-begin"></a>Prima di iniziare  

[Creare un profilo di configurazione dispositivi di Endpoint Protection](endpoint-protection-configure.md).  

Per altre informazioni sui provider di servizi di configurazione, vedere [Informazioni di riferimento sul provider di servizi di configurazione](https://docs.microsoft.com/windows/client-management/mdm/configuration-service-provider-reference).  

## <a name="microsoft-defender-application-guard"></a>Microsoft Defender Application Guard  

Quando si usa Microsoft Edge, Microsoft Defender Application Guard protegge l'ambiente dai siti non considerati attendibili dall'organizzazione. Quando gli utenti visitano siti non elencati nei limiti della rete isolata, tali siti vengono aperti in una sessione del browser virtuale di Hyper-V. I siti attendibili vengono definiti da un limite di rete, configurato in Configurazione del dispositivo.  

Application Guard è disponibile solo per i dispositivi Windows 10 a 64 bit. Quando si usa questo profilo viene installato un componente Win32 per attivare Application Guard.  

- **Application Guard**  
  **Impostazione predefinita**: Non configurato  
   Provider di servizi di configurazione Application Guard: [Settings/AllowWindowsDefenderApplicationGuard](https://docs.microsoft.com/windows/client-management/mdm/windowsdefenderapplicationguard-csp#allowwindowsdefenderapplicationguard)  

  - **Abilitata per Edge**: attivare questa funzionalità, che consente di aprire siti non attendibili in un contenitore del browser virtuale di Hyper-V.  
  - **Non configurato**: tutti i siti (attendibili e non attendibili) possono essere aperti nel dispositivo.  

- **Comportamento degli Appunti**  
  **Impostazione predefinita**: Non configurato  
   Provider di servizi di configurazione Application Guard: [Settings/ClipboardSettings](https://go.microsoft.com/fwlink/?linkid=872351)  

  Consente di scegliere le azioni di copia/incolla consentite tra il computer locale e il browser virtuale di Application Guard.  
  - **Non configurato**  
  - **Consenti copia e incolla solo dal computer al browser**  
  - **Consenti copia e incolla solo dal browser al computer**  
  - **Consenti copia e incolla tra computer e browser**  
  - **Blocca copia e incolla tra computer e browser**  

- **Contenuto degli Appunti**  
  Questa impostazione è disponibile solo quando per l'opzione *Comportamento degli Appunti* viene usata una delle impostazioni *Consenti*.  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione Application Guard: [Settings/ClipboardFileType](https://docs.microsoft.com/windows/client-management/mdm/windowsdefenderapplicationguard-csp#clipboardfiletype)  

  Consente di selezionare il contenuto autorizzato degli Appunti.  
  - **Non configurato**  
  - **Text**  
  - **Immagini**  
  - **Testo e immagini**  

- **Contenuto esterno nei siti aziendali**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione Application Guard: [Settings/BlockNonEnterpriseContent](https://go.microsoft.com/fwlink/?linkid=872352)  

  - **Blocca**: impedisce il caricamento del contenuto dai siti Web non approvati.  
  - **Non configurato**: i siti non aziendali possono essere aperti nel dispositivo.  
 
- **Stampa dal browser virtuale**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione Application Guard: [Settings/PrintingSettings](https://go.microsoft.com/fwlink/?linkid=872354)  

  - **Consenti**: consente la stampa del contenuto selezionato dal browser virtuale.  
  - **Non configurato** disabilita tutte le funzionalità di stampa.  

  Quando si imposta *Consenti* per la stampa è possibile configurare l'impostazione seguente:
  - **Tipi di stampa** Selezionare una o più delle opzioni seguenti:  
    - PDF  
    - XPS  
    - Stampanti locali
    - Stampanti di rete  

- **Raccogli registri**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione Application Guard: [Audit/AuditApplicationGuard](https://go.microsoft.com/fwlink/?linkid=872418)  

  - **Consenti**: per raccogliere i registri degli eventi che si verificano in una sessione del browser di Application Guard.  
  - **Non configurato**: non vengono raccolti registri nella sessione del browser.  

- **Conserva i dati del browser generati dall'utente**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione Application Guard: [Settings/AllowPersistence](https://go.microsoft.com/fwlink/?linkid=872419)  

  - **Consenti**: per salvare i dati utente, ad esempio password, Preferiti e cookie, creati durante una sessione del browser virtuale di Application Guard.  
  - **Non configurato**: per eliminare i file e i dati scaricati dall'utente al riavvio del dispositivo o quando un utente si disconnette.  

- **Accelerazione grafica**  
 **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione Application Guard: [Settings/AllowVirtualGPU](https://go.microsoft.com/fwlink/?linkid=872420)  
      
  - **Abilita**: consente di caricare i siti Web con utilizzo intensivo di grafica e i video più velocemente ottenendo l'accesso a un'unità di elaborazione grafica virtuale.  
  - L'impostazione **Non configurata** usa la CPU del dispositivo per la grafica. Non usa l'unità di elaborazione grafica virtuale.  

- **Scarica i file nel file system dell'host**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione Application Guard: [Settings/SaveFilesToHost](https://go.microsoft.com/fwlink/?linkid=872421)  

  - **Abilita**: gli utenti possono scaricare i file dal browser virtualizzato nel sistema operativo host.  
  - **Non configurato**: consente di mantenere i file locali nel dispositivo e non scaricare i file nel file system host.  

## <a name="microsoft-defender-firewall"></a>Microsoft Defender Firewall  
 
### <a name="global-settings"></a>Impostazioni globali  

Queste impostazioni sono applicabili a tutti i tipi di rete.  

- **File Transfer Protocol**  
  **Impostazione predefinita**: Non configurato  
   Provider di servizi di configurazione Firewall: [MdmStore/Global/DisableStatefulFtp](https://go.microsoft.com/fwlink/?linkid=872536)  

  - **Blocca**: disabilita il protocollo FTP con stato.  
  - **Non configurato**: il firewall applica filtri FTP con stato per consentire connessioni secondarie.  

- **Tempo di inattività delle associazioni di sicurezza prima dell'eliminazione**  
  **Impostazione predefinita**: *Non configurato*  
   Provider di servizi di configurazione Firewall: [MdmStore/Global/SaIdleTime](https://go.microsoft.com/fwlink/?linkid=872539)  

   Consente di specificare un tempo di inattività in secondi, dopo il quale vengono eliminate le associazioni di sicurezza.   

- **Codifica delle chiavi precondivise**  
  **Impostazione predefinita**: Non configurato  
   Provider di servizi di configurazione Firewall: [MdmStore/Global/PresharedKeyEncoding](https://go.microsoft.com/fwlink/?linkid=872541)  

   - **Abilita** - Consente di codificare le chiavi precondivise con UTF-8.  
   - **Non configurata** - Consente di codificare le chiavi precondivise con il valore dell'archivio locale.  

- **Esenzioni da IPsec**  
  **Impostazione predefinita**: *0 selezionato*  
   Provider di servizi di configurazione Firewall: [MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

   Selezionare uno o più dei tipi di traffico seguenti da esentare da IPSec:  
   - **Codici di tipo ICMP IPv6 per Neighbor Discover**  
   - **ICMP**  
   - **Codici di tipo ICMP IPv6 per Router Discover**  
   - **Traffico DHCP IPv4 e IPv6**  

- **Verifica dell'elenco di revoche di certificati**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione Firewall: [MdmStore/Global/CRLcheck](https://go.microsoft.com/fwlink/?linkid=872548)  

  consente di scegliere il modo in cui il dispositivo verifica l'elenco di revoche di certificati. Le opzioni includono:  
  - **Disabilita la verifica dell'elenco di revoche di certificati**  
  - **Esito negativo della verifica dell'elenco di revoche di certificati solo in caso di certificato revocato**  
  - **Esito negativo della verifica dell'elenco di revoche di certificati per ogni errore rilevato**  
 

- **Corrispondenza opportunistica del set di autenticazione per ogni modulo per le chiavi**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione Firewall: [MdmStore/Global/OpportunisticallyMatchAuthSetPerKM](https://go.microsoft.com/fwlink/?linkid=872550)  
  
  - **Abilita**: i moduli per le chiavi devono ignorare solo le famiglie di prodotti di autenticazione non supportate.  
  - **Non configurato**: i moduli per le chiavi devono ignorare l'intera famiglia di prodotti di autenticazione se non supportano tutte le famiglie di prodotti di autenticazione specificate nel set.  


- **Accodamento di pacchetti**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione Firewall: [MdmStore/Global/EnablePacketQueue](https://go.microsoft.com/fwlink/?linkid=872551)  

  Specificare la modalità di abilitazione del ridimensionamento del software sul lato ricezione per la ricezione di testo crittografato e l'inoltro di testo normale per lo scenario relativo a gateway con tunnel IPSec, assicurando il mantenimento dell'ordine dei pacchetti. Le opzioni includono:  
  - **Non configurato**  
  - **Disabilita l'accodamento di tutti i pacchetti**  
  - **Accoda solo i pacchetti crittografati in ingresso**  
  - **Accoda i pacchetti solo dopo l'esecuzione della decrittografia per l'inoltro**  
  - **Configura i pacchetti in ingresso e in uscita**  

### <a name="network-settings"></a>Impostazioni di rete  

Le impostazioni seguenti sono elencate una sola volta in questo articolo, ma si applicano ai tre tipi di rete specifici:  
- **Rete di dominio (aziendale)**  
- **Rete privata (individuabile)**  
- **Rete pubblica (non individuabile)**  

#### <a name="general-settings"></a>Impostazioni generali  

- **Microsoft Defender Firewall**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione Firewall: [EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)  
  
  - **Abilita**: per attivare il firewall e la sicurezza avanzata. 
  - **Non configurato**: consente tutto il traffico di rete, indipendentemente dalle eventuali altre impostazioni dei criteri.  

- **Modalità mascheramento**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione Firewall: [DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)  
  - **Non configurato**  
  - **Blocca** - Impedisce il funzionamento del firewall in modalità mascheramento. Il blocco della modalità mascheramento consente di bloccare anche **Esenzione di pacchetti protetti da IPsec**.  
  - **Consenti** - Il firewall opera in modalità mascheramento, condizione utile per evitare risposte alle richieste di probe.  

- **Esenzione di pacchetti protetti da IPsec con la modalità mascheramento**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione Firewall: [DisableStealthModeIpsecSecuredPacketExemption](https://go.microsoft.com/fwlink/?linkid=872560)  

  Questa opzione viene ignorata se *Modalità mascheramento* è impostata su *Blocca*.  

  - **Non configurato**  
  - **Blocca**- I pacchetti protetti IPSec non ricevono esenzioni.  
  - **Consenti** - Consente di abilitare le esenzioni. La modalità mascheramento del firewall NON DEVE impedire al computer host di rispondere al traffico di rete indesiderato protetto da IPSec.  

- **Schermato**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione Firewall: [Schermato](https://go.microsoft.com/fwlink/?linkid=872561)  
    - **Non configurato**  
    - **Blocca** - Quando Microsoft Defender Firewall è attivo e questa impostazione è impostata su *Blocca*, tutto il traffico in ingresso viene bloccato, indipendentemente dalle altre impostazioni dei criteri. 
    - **Consenti** - Se impostata su *Consenti*, questa impostazione viene disattivata e il traffico in ingresso è consentito in base ad altre impostazioni dei criteri.

- **Risposte unicast a broadcast multicast**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione Firewall: [DisableUnicastResponsesToMulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)  
  
  In genere, si preferisce non ricevere risposte unicast a messaggi trasmessi o multicast. Queste risposte possono indicare un attacco Denial of Service (DoS) o il tentativo da parte di un utente malintenzionato di rilevare la presenza di un computer attivo noto.  
  - **Non configurato**  
  - **Blocca**: per disabilitare le risposte unicast ai broadcast multicast.  
  - **Consenti**: per consentire le risposte unicast ai broadcast multicast.  

- **Notifiche in ingresso**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione Firewall: [DisableInboundNotifications](https://go.microsoft.com/fwlink/?linkid=8725630)  

  - **Non configurato**  
  - **Blocca** - Vengono nascoste le notifiche agli utenti quando un'app non è autorizzata all'ascolto su una porta.  
  - **Consenti**: abilita questa impostazione e può visualizzare una notifica agli utenti quando un'app non è autorizzata all'ascolto su una porta.  

- **Azione predefinita per le connessioni in ingresso**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione Firewall: [DefaultOutboundAction](https://aka.ms/intune-firewall-outboundaction)  
  
  Consente di configurare l'azione predefinita eseguita dal firewall per le connessioni in uscita. Questa impostazione verrà applicata a Windows versione 1809 e successive.  

  - **Non configurato**  
  - **Blocca** - L'azione predefinita del firewall non viene eseguita per il traffico in uscita a meno che non venga specificato in modo esplicito di non applicare il blocco.  
  - **Consenti** - Le azioni predefinite del firewall vengono eseguite sulle connessioni in uscita.  

- **Azione predefinita per le connessioni in ingresso**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione Firewall: [DefaultInboundAction](https://go.microsoft.com/fwlink/?linkid=872564)  
 
  - **Non configurato**  
  - **Blocca**: l'azione del firewall predefinita non viene eseguita sulle connessioni in ingresso.  
  - **Consenti** - Le azioni predefinite del firewall vengono eseguite sulle connessioni in ingresso.  

#### <a name="rule-merging"></a>Unione delle regole  

- **Regole di Microsoft Defender Firewall per le applicazioni autorizzate dall'archivio locale**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione Firewall: [AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)  

  - **Non configurato**  
  - **Blocca**: le regole del firewall per le applicazioni autorizzate nell'archivio locale vengono ignorate e non applicate.  
  - **Consenti** -
   Scegliere **Abilita**, che applica le regole del firewall nell'archivio locale in modo che vengano riconosciute e applicate.  

- **Regole di Microsoft Defender Firewall per porte globali dall'archivio locale**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione Firewall: [GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)  

  - **Non configurato**  
  - **Blocca**: le regole del firewall per le porte globali nell'archivio locale vengono ignorate e non applicate.  
  - **Consenti**: le regole del firewall per le porte globali vengono applicate nell'archivio locale in modo che vengano riconosciute e applicate.  

- **Regole di Microsoft Defender Firewall dall'archivio locale**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione Firewall: [AllowLocalPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872567)  

  - **Non configurato**  
  - **Blocca**: le regole del firewall dall'archivio locale vengono ignorate e non vengono applicate.
  - **Consenti**: le regole del firewall vengono applicate nell'archivio locale per il riconoscimento e l'applicazione.  

- **Regole IPsec dall'archivio locale**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione Firewall: [AllowLocalIpsecPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872568)  

  - **Non configurato**  
  - **Blocca**: le regole di sicurezza della connessione dall'archivio locale vengono ignorate e non applicate, indipendentemente dalla versione dello schema o dalle versione delle regole di sicurezza della connessione.  
  - **Consenti**: applicare le regole di sicurezza della connessione dall'archivio locale, indipendentemente dalla versione dello schema o dalla versione delle regole di sicurezza della connessione.  

### <a name="firewall-rules"></a>Regole del firewall  

Selezionare **Aggiungi** per aggiungere una o più regole del firewall personalizzate. Per altre informazioni, vedere [Aggiungere regole del firewall personalizzate per dispositivi Windows 10](endpoint-protection-configure.md#add-custom-firewall-rules-for-windows-10-devices).  

Le regole del firewall personalizzate supportano le opzioni seguenti:  

#### <a name="general-settings"></a>Impostazioni generali:  

- **Nome**  
  **Impostazione predefinita**: *Nessun nome*  

  Specificare un nome descrittivo per la regola. Questo nome verrà visualizzato nell'elenco di regole per facilitarne l'identificazione.  

- **Descrizione**  
  **Impostazione predefinita**: *Nessuna descrizione*  

  Fornire una descrizione della regola.  

- **Direzione**   
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione Firewall: [FirewallRules/*FirewallRuleName*/Direction](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#direction)  
  
  Specificare se questa regola si applica al traffico **In ingresso** o **In uscita**. Con l'impostazione **Non configurata** la regola si applica automaticamente al traffico in uscita.  

- **Azione**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione Firewall: [FirewallRules/*FirewallRuleName*/Action](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#action) e [FirewallRules/*FirewallRuleName*/Action/Type](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#type)  

  Selezionare **Consenti** o **Blocca**. Con l'impostazione **Non configurata**, la regola consente il traffico per impostazione predefinita.  

- **Tipo di rete**  
  **Impostazione predefinita**: 0 selezionato  
  Provider di servizi di configurazione Firewall: [FirewallRules/*FirewallRuleName*/Profiles](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#profiles)  

  Selezionare un massimo di tre tipi di rete a cui appartiene questa regola. Le opzioni includono **Dominio**, **Privata** e **Pubblica**.  Se non viene selezionato alcun tipo di rete, la regola si applica a tutti e tre i tipi di rete.  

#### <a name="application-settings"></a>Impostazioni applicazione  

- **Applicazione/i**  
  **Impostazione predefinita**: All  

  Controllare le connessioni per un'app o un programma. Selezionare una delle opzioni seguenti e quindi completare la configurazione aggiuntiva:  
  - **Nome della famiglia di pacchetti**: specificare il nome della famiglia di pacchetti. Per trovare il nome della famiglia di pacchetti, usare il comando di PowerShell **Get-AppxPackage**.   
    Provider di servizi di configurazione Firewall: [FirewallRules/*FirewallRuleName*/App/PackageFamilyName](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#packagefamilyname)  
 
  - **Percorso file**: è necessario specificare un percorso di file per un'app nel dispositivo client, che può essere un percorso assoluto o un percorso relativo. Ad esempio:  C:\Windows\System\Notepad.exe o %WINDIR%\Notepad.exe.  
    Provider di servizi di configurazione Firewall: [FirewallRules/*FirewallRuleName*/App/FilePath](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#filepath)  

  - **Servizio Windows** - Specificare il nome breve del servizio Windows se si tratta di un servizio e non di un'applicazione che invia o riceve traffico. Per trovare il nome breve del servizio, usare il comando di PowerShell **Get-Service**.  
    Provider di servizi di configurazione Firewall: [FirewallRules/*FirewallRuleName*/App/ServiceName](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#servicename)  

  - **Tutto** - *Non è disponibile alcuna configurazione aggiuntiva*.  

#### <a name="ip-address-settings"></a>Impostazioni dell'indirizzo IP  

Specificare gli indirizzi locali e remoti a cui è applicabile questa regola.  

- **Indirizzi locali**    
  **Impostazione predefinita**: Qualsiasi indirizzo  
  Provider di servizi di configurazione Firewall: [FirewallRules/*FirewallRuleName*/LocalPortRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#localportranges)  

  Selezionare **Qualsiasi indirizzo** o **Indirizzo specificato**.  

  Quando si usa *Indirizzo specificato* è necessario aggiungere uno o più indirizzi come un elenco delimitato da virgole di indirizzi locali coperti dalla regola. I token validi includono:  
  - Usare un asterisco "*" per *qualsiasi* indirizzo locale. Se si usa un asterisco, deve essere l'unico token usato.  
  - Per specificare una subnet, usare la notazione con subnet mask o prefisso di rete. Se non si specifica una subnet mask o un prefisso di rete, viene usata la subnet mask predefinita 255.255.255.255.  
  - Un indirizzo IPv6 valido.  
  - Un intervallo di indirizzi IPv4 nel formato "indirizzo iniziale-indirizzo finale" senza spazi inclusi.  
  - Un intervallo di indirizzi IPv6 nel formato "indirizzo iniziale-indirizzo finale" senza spazi inclusi.  

- **Indirizzi remoti**  
  **Impostazione predefinita**: Qualsiasi indirizzo  
  Provider di servizi di configurazione Firewall: [FirewallRules/*FirewallRuleName*/RemoteAddressRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#remoteaddressranges)  
 
  Selezionare **Qualsiasi indirizzo** o **Indirizzo specificato**.  

  Quando si usa *Indirizzo specificato* è necessario aggiungere uno o più indirizzi come un elenco delimitato da virgole di indirizzi remoti coperti dalla regola. I token non fanno distinzione tra maiuscole e minuscole. I token validi includono:  
  - Usare un asterisco "*" per *qualsiasi* indirizzo remoto. Se si usa un asterisco, deve essere l'unico token usato.  
  - "Defaultgateway"  
  - "DHCP"  
  - "DNS"  
  - "WINS"  
  - "Intranet" (supportato in Windows versioni 1809 e successive)  
  - "RmtIntranet" (supportato in Windows versioni 1809 e successive)  
  - "Internet" (supportato in Windows versioni 1809 e successive)  
  - "Ply2Renders" (supportato in Windows versioni 1809 e successive)  
  - "LocalSubnet" indica qualsiasi indirizzo locale nella subnet locale.  
  - Per specificare una subnet, usare la notazione con subnet mask o prefisso di rete. Se non si specifica una subnet mask o un prefisso di rete, viene usata la subnet mask predefinita 255.255.255.255.  
  - Un indirizzo IPv6 valido.  
  - Un intervallo di indirizzi IPv4 nel formato "indirizzo iniziale-indirizzo finale" senza spazi inclusi.  
  - Un intervallo di indirizzi IPv6 nel formato "indirizzo iniziale-indirizzo finale" senza spazi inclusi.  

#### <a name="port-and-protocol-settings"></a>Impostazioni per porte e protocolli  
Specificare le porte locali e remote a cui è applicabile questa regola.  

- **Protocollo**  
  **Impostazione predefinita**: qualsiasi  
  Provider di servizi di configurazione Firewall: [FirewallRules/*FirewallRuleName*/Protocol](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#protocol)  
  Selezionare una delle opzioni seguenti e completare le configurazioni necessarie:  
  - **Tutto** - Non è disponibile alcuna configurazione aggiuntiva.  
  - **TCP** - Configurare le porte locali e remote. Entrambe le opzioni supportano Tutte le porte o Porte specificate. Immettere le porte specificate usando un elenco delimitato da virgole.  
    - **Porte locali** - Provider di servizi di configurazione Firewall: [FirewallRules/*FirewallRuleName*/LocalPortRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#localportranges)  
    - **Porte remote** - Provider di servizi di configurazione Firewall: [FirewallRules/*FirewallRuleName*/RemotePortRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#remoteportranges)  
  - **UDP** - Configurare le porte locali e remote. Entrambe le opzioni supportano Tutte le porte o Porte specificate. Immettere le porte specificate usando un elenco delimitato da virgole.  
    - **Porte locali** - Provider di servizi di configurazione Firewall: [FirewallRules/*FirewallRuleName*/LocalPortRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#localportranges)  
    - **Porte remote** - Provider di servizi di configurazione Firewall: [FirewallRules/*FirewallRuleName*/RemotePortRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#remoteportranges)  
  - **Personalizzato** - Specificare un numero di **protocollo** personalizzato compreso tra 0 e 255.  

#### <a name="advanced-configuration"></a>Configurazione avanzata  
- **Tipi di interfaccia**  
  **Impostazione predefinita**: 0 selezionato  
  Provider di servizi di configurazione Firewall: [FirewallRules/*FirewallRuleName*/InterfaceTypes](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#interfacetypes)  

  Selezionare una delle opzioni seguenti:  
  - **Accesso remoto**  
  - **Wireless**  
  - **Rete locale**  

- **Consenti connessioni solo da questi utenti**  
  **Impostazione predefinita**: Tutti gli utenti *(impostazione predefinita quando non viene specificato alcun elenco)*  
  Provider di servizi di configurazione Firewall: [FirewallRules/*FirewallRuleName*/LocalUserAuthorizationList](https://aka.ms/intunefirewallauthorizedusers)  

  Specificare un elenco di utenti locali autorizzati per questa regola. Non è possibile specificare un elenco di utenti autorizzati se questa regola si applica a un servizio Windows.  


## <a name="microsoft-defender-smartscreen-settings"></a>Impostazioni di Microsoft Defender SmartScreen  
 
Microsoft Edge deve essere installato nel dispositivo.  

- **SmartScreen per app e file**  
  **Impostazione predefinita**: Non configurato  
   Provider di servizi di configurazione SmartScreen: [SmartScreen/EnableSmartScreenInShell](https://go.microsoft.com/fwlink/?linkid=872784)  

  - **Non configurata**: disabilita l'uso di SmartScreen.  
  - **Abilita**: consente di abilitare Windows SmartScreen per l'esecuzione di file e di app. SmartScreen è un componente anti-phishing e anti-malware basato sul cloud.  

- **Esecuzione di file non verificati**  
  **Impostazione predefinita**: Non configurato  
   Provider di servizi di configurazione SmartScreen: [SmartScreen/PreventOverrideForFilesInShell](https://go.microsoft.com/fwlink/?linkid=872783)

  - **Non configurato**: disabilita questa funzionalità e consente agli utenti finali di eseguire i file che non sono stati verificati.  
  - **Blocca**: impedisce agli utenti finali di eseguire file non verificati da Windows SmartScreen.  

## <a name="windows-encryption"></a>Crittografia di Windows  
 
### <a name="windows-settings"></a>Impostazioni Windows  

- **Crittografa i dispositivi**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione BitLocker: [RequireDeviceEncryption](https://go.microsoft.com/fwlink/?linkid=872523)  

  - **Rendi obbligatorio**: per richiedere agli utenti di abilitare la crittografia del dispositivo. A seconda dell'edizione di Windows e della configurazione di sistema, è possibile che venga richiesto agli utenti:  
    - Di confermare che non è abilitata la crittografia di un altro fornitore.  
    - Di disattivare Crittografia unità BitLocker e quindi di riattivare BitLocker.  
  - **Non configurato**  
  
  Se la crittografia di Windows è attivata mentre è attivo un altro metodo di crittografia, il dispositivo potrebbe diventare instabile.  

<!-- Support Deprecated for Windows 10 Mobile as of August 2020

- **Encrypt storage card (mobile only)**  
  *This setting only applies to Windows 10 mobile.*  
  **Default**: Not configured  
  BitLocker CSP: [RequireStorageCardEncryption](https://go.microsoft.com/fwlink/?linkid=872524)  

  - **Require** to encrypt any removable storage cards used by the device.  
  - **Not configured** - Don't require storage card encryption, and don't prompt the user to turn it on.  
-->

### <a name="bitlocker-base-settings"></a>Impostazioni di base di BitLocker  

Le impostazioni di base sono impostazioni BitLocker universali per tutti i tipi di unità dati. Queste impostazioni gestiscono le attività di crittografia delle unità o le opzioni di configurazione che gli utenti finali possono modificare in tutti i tipi di unità dati.  

- **Avviso per la crittografia dischi di altro tipo**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione BitLocker: [AllowWarningForOtherDiskEncryption](https://go.microsoft.com/fwlink/?linkid=872525)  

  - **Blocca**: consente di disabilitare l'avviso se nel dispositivo è presente un altro servizio di crittografia del disco.  
  - **Non configurata**: consente di visualizzare l'avviso se nel dispositivo è presente un altro servizio di crittografia del disco.  

  > [!TIP]  
  > Per installare BitLocker in modo automatico e invisibile all'utente in un dispositivo aggiunto ad Azure AD che esegue Windows 1809 o versione successiva, questa impostazione deve essere impostata su *Blocca*. Per altre informazioni, vedere [Abilitare automaticamente BitLocker nei dispositivi](../protect/encrypt-devices.md#silently-enable-bitlocker-on-devices).

  Se impostata su *Blocca*, è possibile configurare l'impostazione seguente:  

  - **Consenti agli utenti standard di abilitare la crittografia durante un'aggiunta ad Azure AD**  
    *Questa impostazione si applica solo a dispositivi aggiunti ad Azure Active Directory (Azure ADJ) e dipende dall'impostazione precedente, `Warning for other disk encryption`.*  
    **Impostazione predefinita**: Non configurato  
    Provider di servizi di configurazione BitLocker: [AllowStandardUserEncryption](https://docs.microsoft.com/windows/client-management/mdm/bitlocker-csp#allowstandarduserencryption)

     - **Consenti**: gli utenti standard (non amministratori) possono abilitare la crittografia BitLocker dopo l'accesso.  
     - **Non configurato**: solo gli amministratori possono abilitare la crittografia BitLocker nel dispositivo.  

  > [!TIP]  
  > Per installare BitLocker in modo automatico e invisibile all'utente in un dispositivo aggiunto ad Azure AD che esegue Windows 1809 o versione successiva, questa impostazione deve essere impostata su *Consenti*. Per altre informazioni, vedere [Abilitare automaticamente BitLocker nei dispositivi](../protect/encrypt-devices.md#silently-enable-bitlocker-on-devices).

- **Configura i metodi di crittografia**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione BitLocker: [EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  

  - **Abilita**: consente di configurare gli algoritmi di crittografia per il sistema operativo, i dati e le unità rimovibili.  
  - **Non configurato**: BitLocker usa il metodo di crittografia predefinito XTS-AES 128 bit o il metodo di crittografia specificato da qualsiasi script di configurazione.  

  Se impostata su *Abilita*, è possibile configurare le impostazioni seguenti:  

  - **Crittografia per le unità del sistema operativo**  
    **Impostazione predefinita**: XTS-AES a 128 bit  
   
    scegliere il metodo di crittografia per le unità del sistema operativo. È consigliabile usare l'algoritmo XTS-AES.  
    - **AES-CBC a 128 bit**  
    - **AES-CBC a 256 bit**  
    - **XTS-AES a 128 bit**  
    - **XTS-AES a 256 bit**  

  - **Crittografia per unità dati fisse**  
    **Impostazione predefinita**: AES-CBC a 128 bit  
   
    scegliere il metodo di crittografia per le unità dati fisse (predefinite). È consigliabile usare l'algoritmo XTS-AES.  
    - **AES-CBC a 128 bit**  
    - **AES-CBC a 256 bit**  
    - **XTS-AES a 128 bit**  
    - **XTS-AES a 256 bit**  

  - **Crittografia per unità dati rimovibili**  
    **Impostazione predefinita**: AES-CBC a 128 bit  

    scegliere il metodo di crittografia per le unità dati rimovibili. Se l'unità rimovibile viene usata con dispositivi che non eseguono Windows 10, è consigliabile usare l'algoritmo AES-CBC.  
    - **AES-CBC a 128 bit**  
    - **AES-CBC a 256 bit**  
    - **XTS-AES a 128 bit**  
    - **XTS-AES a 256 bit**  

### <a name="bitlocker-os-drive-settings"></a>Impostazioni delle unità del sistema operativo di BitLocker  

Queste impostazioni si applicano in modo specifico alle unità dati del sistema operativo.  

- **Autenticazione aggiuntiva all'avvio**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione BitLocker: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)  

  - **Rendi obbligatorio**: consente di configurare i requisiti di autenticazione per l'avvio dei computer, incluso l'uso di Trusted Platform Module (TPM).  
  - **Non configurata**: consente di configurare solo le opzioni di base nei dispositivi con TPM.  

  Se impostata su *Rendi obbligatorio*, è possibile configurare le impostazioni seguenti:  

  - **BitLocker con chip TPM non compatibile**  
    **Impostazione predefinita**: Non configurato  

    - **Blocca**: disabilitare l'uso di BitLocker quando un dispositivo non dispone di un chip TPM compatibile.  
    - **Non configurato**: gli utenti possono usare BitLocker senza un chip TPM compatibile. BitLocker può richiedere una password o una chiave di avvio.  

  - **Avvio TPM compatibile**  
    **Impostazione predefinita**: Consenti TPM  

    Consente di stabilire se TPM è consentito, obbligatorio o non consentito.  

    - **Consenti TPM**  
    - **Non consentire TPM**  
    - **Richiedi TPM**  

  - **PIN di avvio TPM compatibile**  
    **Impostazione predefinita**: Consenti il PIN di avvio con TPM  

    scegliere se consentire, non consentire o rendere obbligatorio l'uso di un PIN di avvio con il chip TPM. L'abilitazione di un PIN di avvio richiede l'interazione dell'utente finale.  

    - **Consenti il PIN di avvio con TPM**  
    - **Non consentire il PIN di avvio con TPM**  
    - **Richiedere il PIN di avvio con TPM**

    > [!TIP]
    > Per installare BitLocker in modo automatico e invisibile all'utente in un dispositivo aggiunto ad Azure AD che esegue Windows 1809 o versione successiva, questa impostazione non deve essere impostata su *Richiedi PIN di avvio con TPM*. Per altre informazioni, vedere [Abilitare automaticamente BitLocker nei dispositivi](../protect/encrypt-devices.md#silently-enable-bitlocker-on-devices).

  - **Chiave di avvio TPM compatibile**  
    **Impostazione predefinita**: Consenti la chiave di avvio con TPM  

    scegliere se consentire, non consentire o rendere obbligatorio l'uso di una chiave di avvio con il chip TPM. L'abilitazione di una chiave di avvio richiede l'interazione dell'utente finale.  

    - **Consenti la chiave di avvio con TPM**  
    - **Non consentire la chiave di avvio con TPM**  
    - **Richiedi la chiave di avvio con TPM**  

    > [!TIP]
    > Per installare BitLocker in modo automatico e invisibile all'utente in un dispositivo aggiunto ad Azure AD che esegue Windows 1809 o versione successiva, questa impostazione non deve essere impostata su *Richiedi la chiave di avvio con TPM*. Per altre informazioni, vedere [Abilitare automaticamente BitLocker nei dispositivi](../protect/encrypt-devices.md#silently-enable-bitlocker-on-devices).

  - **Chiave di avvio e PIN TPM compatibile**  
    **Impostazione predefinita**: Consenti la chiave di avvio e il PIN con TPM  

    scegliere se consentire, non consentire o rendere obbligatorio l'uso di una chiave di avvio e di un PIN con il chip TPM. L'abilitazione di chiave di avvio e PIN richiede l'interazione dell'utente finale.  
    - **Consenti la chiave di avvio e il PIN con TPM**  
    - **Non consentire la chiave e il PIN di avvio con TPM**  
    - **Richiedi la chiave di avvio e il PIN con TPM**   

    > [!TIP]  
    > Per installare BitLocker in modo automatico e invisibile all'utente in un dispositivo aggiunto ad Azure AD che esegue Windows 1809 o versione successiva, questa impostazione non deve essere impostata su *Richiedi la chiave di avvio e il PIN con TPM*. Per altre informazioni, vedere [Abilitare automaticamente BitLocker nei dispositivi](../protect/encrypt-devices.md#silently-enable-bitlocker-on-devices).

- **Lunghezza minima del PIN**  
    **Impostazione predefinita**: Non configurato  
    Provider di servizi di configurazione BitLocker: [SystemDrivesMinimumPINLength](https://go.microsoft.com/fwlink/?linkid=872528)   

    - **Abilita** consente di configurare la lunghezza minima del PIN di avvio del TPM.  
    - **Non configurato**: gli utenti possono configurare un PIN di avvio di qualsiasi lunghezza compresa tra 6 e 20 cifre.  

  Se impostata su *Abilita*, è possibile configurare l'impostazione seguente:  

  - **Numero minimo di caratteri**  
    **Impostazione predefinita**: *Non configurata* Provider di servizi di configurazione BitLocker: [SystemDrivesMinimumPINLength](https://go.microsoft.com/fwlink/?linkid=872528)  

    immettere il numero di caratteri obbligatorio per il PIN di avvio, **4**-**20**.  

- **Ripristino delle unità del sistema operativo**  
  **Impostazione predefinita**: Non configurato   
  Provider di servizi di configurazione BitLocker: [SystemDrivesRecoveryOptions](https://go.microsoft.com/fwlink/?linkid=872529)  

  - **Abilita**: consente di controllare la modalità di ripristino delle unità del sistema operativo protette da BitLocker se le informazioni necessarie all'avvio non sono disponibili.  
  - **Non configurato**: le opzioni di ripristino predefinite sono supportate per il ripristino di BitLocker. Per impostazione predefinita, è consentito un agente di recupero dati, le opzioni di ripristino vengono scelte dall'utente, incluse la password di ripristino e la chiave di ripristino, e non viene eseguito il backup delle informazioni di ripristino in Active Directory Domain Services.  

  Se impostata su *Abilita*, è possibile configurare le impostazioni seguenti:  

  - **Agente di recupero dati basato su certificati**  
    **Impostazione predefinita**: Non configurato  
     
    - **Blocca** - Impedisce l'uso di un agente di recupero dati con le unità del sistema operativo protette da BitLocker.  
    - **Non configurata** - Consente l'uso degli agenti di recupero dati con unità del sistema operativo protette da BitLocker.  

  - **Creazione della password di ripristino da parte dell'utente**  
    **Impostazione predefinita**: Consenti la password di ripristino di 48 cifre  

    scegliere se per gli utenti è consentito, obbligatorio o non consentito generare una password di ripristino di 48 cifre.  
    - **Consenti la password di ripristino di 48 cifre**  
    - **Non consentire password di ripristino di 48 cifre**  
    - **Richiedi la password di ripristino di 48 cifre**  

  - **Creazione della chiave di ripristino da parte dell'utente**  
    **Impostazione predefinita**: Consenti la chiave di ripristino a 256 bit  

    scegliere se per gli utenti è consentito, obbligatorio o non consentito generare una chiave di ripristino a 256 bit.  
    - **Consenti la chiave di ripristino a 256 bit**  
    - **Non consentire la chiave di ripristino a 256 bit**  
    - **Richiedi la chiave di ripristino a 256 bit**  

  - **Opzioni di ripristino nell'installazione guidata di BitLocker**  
    **Impostazione predefinita**: Non configurato  

    - **Blocca**: gli utenti non possono visualizzare e modificare le opzioni di ripristino. Con l'impostazione 
    - **Non configurato**: gli utenti possono visualizzare e modificare le opzioni di ripristino dopo l'attivazione di BitLocker. 
 
  - **Salva le informazioni di ripristino di BitLocker in Azure Active Directory**  
    **Impostazione predefinita**: Non configurato  

    - **Abilita**: archiviare le informazioni di ripristino di BitLocker in Azure Active Directory (Azure AD).  
    - **Non configurata**: le informazioni di ripristino di BitLocker non vengono archiviate in Azure AD.  

  - **Informazioni di ripristino di BitLocker archiviate in Azure Active Directory**  
    **Impostazione predefinita**: Backup delle password di ripristino e dei pacchetti di chiavi  

    consente di configurare quali parti delle informazioni di ripristino di BitLocker devono essere archiviate in Azure AD. Scegliere tra:  
    - **Backup delle password di ripristino e dei pacchetti di chiavi**  
    - **Backup solo delle password di ripristino**  

  - **Rotazione delle password di ripristino basata su client**  
    **Impostazione predefinita**: La rotazione delle chiavi è abilitata per i dispositivi aggiunti ad Azure AD  
    Provider di servizi di configurazione BitLocker: [ConfigureRecoveryPasswordRotation](https://docs.microsoft.com/windows/client-management/mdm/bitlocker-csp)  
    
    Questa impostazione avvia una rotazione della password di ripristino basata sul client dopo un ripristino dell'unità del sistema operativo (tramite bootmgr o WinRE).  

    - Non configurato  
    - La rotazione delle chiavi è disabilitata  
    - La rotazione delle chiavi è abilitata per i dispositivi aggiunti ad Azure AD  
    - La rotazione delle chiavi è abilitata per i dispositivi aggiunti ad Azure AD e Azure AD ibrido  

  - **Archivia le informazioni di ripristino in Azure Active Directory prima di abilitare BitLocker**  
    **Impostazione predefinita**: Non configurato  
 
     Consente di impedire agli utenti di abilitare BitLocker se il computer non esegue correttamente il backup delle informazioni di ripristino di BitLocker in Azure Active Directory.  

    - **Rendi obbligatorio**: gli utenti possono attivare BitLocker solo se le informazioni di ripristino di BitLocker sono state archiviate in Azure AD.  
    - **Non configurato**: consente agli utenti di attivare BitLocker, anche se le informazioni di ripristino non vengono archiviate correttamente in Azure AD.  

- **URL e messaggio di ripristino prima dell'avvio**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione BitLocker: [SystemDrivesRecoveryMessage](https://go.microsoft.com/fwlink/?linkid=872530)  

  - **Abilita**: configurare il messaggio e l'URL visualizzati nella schermata di recupero della chiave prima dell'avvio.  
  - **Non configurato**: disabilitare questa funzionalità.  
  
  Se impostata su *Abilita*, è possibile configurare l'impostazione seguente:  
  - **Messaggio di ripristino prima dell'avvio**  
    **Impostazione predefinita**: Usa URL e messaggio di ripristino predefiniti   
 
    consente di configurare la modalità di visualizzazione del messaggio di ripristino prima dell'avvio. Scegliere tra:  
    - **Usa URL e messaggio di ripristino predefiniti**  
    - **Usa un messaggio di ripristino e un URL vuoti**  
    - **Usa messaggio di ripristino personalizzato**  
    - **Usa URL di ripristino personalizzato**  

### <a name="bitlocker-fixed-data-drive-settings"></a>Impostazioni delle unità dati fisse BitLocker  

Queste impostazioni si applicano in modo specifico alle unità dati fisse.  

- **Accesso in scrittura alle unità dati fisse non protette da BitLocker**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione BitLocker: [FixedDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872534)  

  - **Blocca**: per consentire l'accesso in sola lettura alle unità dati non protette da BitLocker.  
  - **Non configurata**: per impostazione predefinita, è disponibile l'accesso in lettura e scrittura alle unità dati non crittografate.  

- **Ripristino delle unità fisse**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione BitLocker: [FixedDrivesRecoveryOptions](https://go.microsoft.com/fwlink/?linkid=872538)  

  - **Abilita**: consente di stabilire in che modo vengono ripristinate le unità fisse protette da BitLocker se le informazioni necessarie all'avvio non sono disponibili.  
  - **Non configurato**: disabilitare questa funzionalità.  

  Se impostata su *Abilita*, è possibile configurare le impostazioni seguenti:  

  - **Agente di recupero dati**  
    **Impostazione predefinita**: Non configurato  
 
    - **Blocca**: per impedire l'uso di un agente di recupero dati con l'editor dei criteri delle unità fisse protette da BitLocker. 
    - **Non configurato**: consente l'uso di agenti di recupero di dati con le unità fisse protette da BitLocker.  

  - **Creazione della password di ripristino da parte dell'utente**  
    **Impostazione predefinita**: Consenti la password di ripristino di 48 cifre  

    scegliere se per gli utenti è consentito, obbligatorio o non consentito generare una password di ripristino di 48 cifre.  
    - **Consenti la password di ripristino di 48 cifre**  
    - **Non consentire password di ripristino di 48 cifre**  
    - **Richiedi la password di ripristino di 48 cifre**  

  - **Creazione della chiave di ripristino da parte dell'utente**  
    **Impostazione predefinita**: Consenti la chiave di ripristino a 256 bit

    scegliere se per gli utenti è consentito, obbligatorio o non consentito generare una chiave di ripristino a 256 bit.
    - **Consenti la chiave di ripristino a 256 bit**  
    - **Non consentire la chiave di ripristino a 256 bit**  
    - **Richiedi la chiave di ripristino a 256 bit**  

  - **Opzioni di ripristino nell'installazione guidata di BitLocker**  
    **Impostazione predefinita**: Non configurato  

    - **Blocca**: gli utenti non possono visualizzare e modificare le opzioni di ripristino. Con l'impostazione 
    - **Non configurato**: gli utenti possono visualizzare e modificare le opzioni di ripristino dopo l'attivazione di BitLocker.
 
  - **Salva le informazioni di ripristino di BitLocker in Azure Active Directory**  
    **Impostazione predefinita**: Non configurato  

    - **Abilita**: archiviare le informazioni di ripristino di BitLocker in Azure Active Directory (Azure AD).  
    - **Non configurata**: le informazioni di ripristino di BitLocker non vengono archiviate in Azure AD.

  - **Informazioni di ripristino di BitLocker archiviate in Azure Active Directory**  
    **Impostazione predefinita**: Backup delle password di ripristino e dei pacchetti di chiavi  

    consente di configurare quali parti delle informazioni di ripristino di BitLocker devono essere archiviate in Azure AD. Scegliere tra:  
    - **Backup delle password di ripristino e dei pacchetti di chiavi**  
    - **Backup solo delle password di ripristino**  

  - **Archivia le informazioni di ripristino in Azure Active Directory prima di abilitare BitLocker**  
    **Impostazione predefinita**: Non configurato  
 
    Consente di impedire agli utenti di abilitare BitLocker se il computer non esegue correttamente il backup delle informazioni di ripristino di BitLocker in Azure Active Directory.  

    - **Rendi obbligatorio**: gli utenti possono attivare BitLocker solo se le informazioni di ripristino di BitLocker sono state archiviate in Azure AD.  
    - **Non configurato**: consente agli utenti di attivare BitLocker, anche se le informazioni di ripristino non vengono archiviate correttamente in Azure AD.  

### <a name="bitlocker-removable-data-drive-settings"></a>Impostazioni delle unità dati rimovibili BitLocker  

Queste impostazioni si applicano in modo specifico alle unità dati rimovibili.  

- **Accesso in scrittura alle unità dati rimovibili non protette da BitLocker**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione BitLocker: [RemovableDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872540)  

  - **Blocca**: per consentire l'accesso in sola lettura alle unità dati non protette da BitLocker.  
  - **Non configurata**: per impostazione predefinita, è disponibile l'accesso in lettura e scrittura alle unità dati non crittografate.  

  Se impostata su *Abilita*, è possibile configurare l'impostazione seguente:  

  - **Accesso in scrittura ai dispositivi configurati in un'altra organizzazione**  
    **Impostazione predefinita**: Non configurato  

    - **Blocca**: consente l'accesso in scrittura ai dispositivi configurati in un'altra organizzazione.  
    - **Non configurata**: consente di negare l'accesso in scrittura.  
 
## <a name="microsoft-defender-exploit-guard"></a>Microsoft Defender Exploit Guard  

Usare la [protezione dagli exploit](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/exploit-protection) per gestire e ridurre la superficie di attacco delle app usate dai dipendenti.  

### <a name="attack-surface-reduction"></a>Riduzione della superficie di attacco  

Le regole per la riduzione della superficie di attacco consentono di evitare i comportamenti spesso usati da malware per infettare i computer con codice dannoso.  

#### <a name="attack-surface-reduction-rules"></a>Regole per la riduzione della superficie di attacco  

- **Contrassegna il furto di credenziali dal sottosistema dell'autorità di protezione locale Windows**  
  **Impostazione predefinita**: Non configurato  
  Regola: [Blocca il furto di credenziali dal sottosistema dell'autorità di protezione locale di Windows (lsass.exe)](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-credential-stealing-from-the-windows-local-security-authority-subsystem)

  Evitare azioni e app che generalmente vengono usate dal malware per infettare i computer.  

  - **Non configurato**  
  - **Abilita**: impostare flag per la sottrazione delle credenziali dal sottosistema dell'autorità di protezione locale Windows (lsass.exe).  
  - **Controlla soltanto**  

- **Creazione di processi da Adobe Reader (beta)**  
  **Impostazione predefinita**: Non configurato  
  Regola: [Block Adobe Reader from creating child processes](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-adobe-reader-from-creating-child-processes) (Impedisci ad Adobe Reader di creare processi figlio)  

  - **Non configurato**  
  - **Abilita** - Consente di impedire la creazione di processi figlio da Adobe Reader.  
  - **Controlla soltanto**  

#### <a name="rules-to-prevent-office-macro-threats"></a>Regole per impedire le minacce relative alle macro di Office  

Impedire alle app di Office di eseguire le azioni seguenti:  

- **Inserimento delle app di Office in altri processi (nessuna eccezione)**  
  **Impostazione predefinita**: Non configurato  
  Regola: [Impedisci alle applicazioni di Office di inserire codice in altri processi](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-office-applications-from-injecting-code-into-other-processes)  

  - **Non configurato**  
  - **Blocca** - Impedisce alle app di Office di inserire elementi in altri processi.  
  - **Controlla soltanto**  

- **Creazione di contenuto eseguibile in app/macro di Office**  
  **Impostazione predefinita**: Non configurato  
  Regola: [Impedisci alle applicazioni di Office di creare contenuto eseguibile](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-office-applications-from-creating-executable-content)  

  - **Non configurato**  
  - **Blocca** - Impedisce alle app e alle macro di Office di creare contenuto eseguibile.  
  - **Controlla soltanto**  

- **Avvio di processi figlio per le app di Office**  
  **Impostazione predefinita**: Non configurato  
  Regola: [Impedisci alle applicazioni di Office di creare processi figlio](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-all-office-applications-from-creating-child-processes)  

  - **Non configurato**  
  - **Blocca** - Impedisce alle app di Office di avviare processi figlio.  
  - **Controlla soltanto**  
  
- **Importazioni Win32 da codice delle macro in Office**  
  **Impostazione predefinita**: Non configurato  
  Regola: [Blocca le chiamate API Win32 dalle macro di Office](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-win32-api-calls-from-office-macros)  

  - **Non configurato**  
  - **Blocca** - Blocca le importazioni Win32 dal codice delle macro in Office.  
  - **Controlla soltanto**  
  
- **Creazione di processi dai prodotti di comunicazione di Office**  
  **Impostazione predefinita**: Non configurato  
  Regola: [Block Office communication application from creating child processes](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-office-communication-application-from-creating-child-processes) (Impedisci all'applicazione di comunicazione di Office di creare processi figlio)  

  - **Non configurato**  
  - **Abilita** - Consente di bloccare la creazione di processi figlio dalle app di comunicazione di Office.  
  - **Controlla soltanto**  

#### <a name="rules-to-prevent-script-threats"></a>Regole per impedire le minacce relative agli script  

Bloccare i seguenti elementi per contrastare le minacce basate su script:  

- **Codice js/vbs/ps/macro offuscato**  
  **Impostazione predefinita**: Non configurato  
  Regola: [Blocca l'esecuzione di script potenzialmente offuscati](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-execution-of-potentially-obfuscated-scripts)    

  - **Non configurato**  
  - **Blocca** - Blocca eventuale codice js/vbs/ps/macro offuscato.  
  - **Controlla soltanto**  

- **Esecuzione in js/vbs di payload scaricato da Internet (nessuna eccezione)**  
  **Impostazione predefinita**: Non configurato  
  Regola: [Impedisci a JavaScript o VBScript di avviare contenuto eseguibile scaricato](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-javascript-or-vbscript-from-launching-downloaded-executable-content)  

  - **Non configurato**  
  - **Blocca** - Impedisce a js/vbs di eseguire payload scaricato da Internet.  
  - **Controlla soltanto**  

- **Creazione di processi da comandi PSExec e WMI**  
  **Impostazione predefinita**: Non configurato  
  Regola: [Blocca le creazioni di processi generate da comandi PSExec e WMI](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-process-creations-originating-from-psexec-and-wmi-commands)  

  - **Non configurato**  
  - **Blocca**: bloccare le creazioni di processi originate dai comandi PSExec e WMI.  
  
  - **Controlla soltanto**  

- **Processi non attendibili e non firmati eseguiti da USB**  
  **Impostazione predefinita**: Non configurato  
  Regola: [Blocca processi non attendibili e non firmati eseguiti da USB](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-untrusted-and-unsigned-processes-that-run-from-usb)    

  - **Non configurato**  
  - **Blocca**: bloccare i processi non attendibili e non firmati eseguiti da USB.  
  - **Controlla soltanto**  
  
- **File eseguibili che non rispettano criteri di prevalenza, di validità o dell'elenco di elementi attendibili**  
  **Impostazione predefinita**: Non configurato  
  Regola: [Blocca l'esecuzione dei file eseguibili a meno che non rispettino criteri di prevalenza, di validità o dell'elenco di elementi attendibili](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-executable-files-from-running-unless-they-meet-a-prevalence-age-or-trusted-list-criterion)    

  - **Non configurato**  
  - **Blocca**: bloccare l'esecuzione dei file eseguibili se non soddisfano i criteri di prevalenza, età o elenco attendibile.  
  - **Controlla soltanto**  

#### <a name="rules-to-prevent-email-threats"></a>Regole per impedire le minacce tramite posta elettronica  

Bloccare gli elementi seguenti per contrastare le minacce tramite posta elettronica:  

- **Esecuzione del contenuto eseguibile (file con estensione exe, dll, ps, js, vbs e così via) non elaborato dalla posta elettronica (webmail/mail client) (nessuna eccezione)**  
  **Impostazione predefinita**: Non configurato  
  Regola: [Blocca il contenuto eseguibile dal client di posta elettronica e dalla posta sul Web](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-executable-content-from-email-client-and-webmail)  

  - **Non configurato**  
  - **Blocca**: esecuzione del contenuto eseguibile (file EXE, DLL, PS, JS, VBS e così via) non elaborato dalla posta elettronica (webmail/mail client).  
  - **Controlla soltanto**  

#### <a name="rules-to-protect-against-ransomware"></a>Regole per proteggersi dal ransomware  

- **Protezione ransomware avanzata**  
  Impostazione predefinita:  Non configurato  
  Regola: [Usa la protezione avanzata da ransomware](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#use-advanced-protection-against-ransomware)  

  - **Non configurato**  
  - **Abilita**: usare una protezione ransomware aggressiva.  
  - **Controlla soltanto**  

#### <a name="attack-surface-reduction-exceptions"></a>Eccezioni della riduzione della superficie di attacco

- **File e cartelle da escludere dalle regole di riduzione della superficie di attacco**  
  Provider di servizi di configurazione Defender: [AttackSurfaceReductionOnlyExclusions](https://go.microsoft.com/fwlink/?linkid=872981)  

  - **Importare** un file CSV che contiene file e cartelle da escludere dalle regole per la riduzione della superficie di attacco.  
  - **Aggiungere** manualmente file o cartelle locali.  

> [!IMPORTANT]  
> Per consentire la corretta installazione e l'esecuzione delle app line-of-business Win32, le impostazioni antimalware devono escludere l'analisi delle directory seguenti:  
> **Nei computer client X64**:  
> *C:\Programmi (x86)\Microsoft Intune Management Extension\Content*  
> *C:\windows\IMECache*  
>  
> **Nei computer client X86**:  
> *C:\Programmi\Microsoft Intune Management Extension\Content*  
> *C:\windows\IMECache*  
>
> Per altre informazioni, vedere [Raccomandazioni per la ricerca di virus per computer aziendali che eseguono versioni attualmente supportate di Windows](https://support.microsoft.com/help/822158/virus-scanning-recommendations-for-enterprise-computers).


### <a name="controlled-folder-access"></a>Accesso controllato alle cartelle  

È possibile [proteggere i dati importanti](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/controlled-folders) da app e minacce dannose, ad esempio il ransomware.  

- **Protezione delle cartelle**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione Defender: [EnableControlledFolderAccess](https://go.microsoft.com/fwlink/?linkid=872614)  

  Proteggere file e cartelle da modifiche non autorizzate eseguite da applicazioni non compatibili.  

  - **Non configurato**  
  - **Attiva**  
  - **Controlla soltanto**  
  - **Bloccare la modifica del disco**  
  - **Controllare la modifica del disco**  

  Quando si seleziona un'impostazione diversa da *Non configurata*, è possibile configurare:  
  - **Elenco di app con accesso alle cartelle protette**  
    Provider di servizi di configurazione Defender: [ControlledFolderAccessAllowedApplications](https://go.microsoft.com/fwlink/?linkid=872616)  

    - **Importare** un file CSV contenente un elenco di app.  
    - **Aggiungere** manualmente app a questo elenco.  

  - **Elenco di cartelle aggiuntive da proteggere**  
    Provider di servizi di configurazione Defender: [ControlledFolderAccessProtectedFolders](https://go.microsoft.com/fwlink/?linkid=872617)  

    - **Importare** un file CSV contenente un elenco di cartelle.  
    - **Aggiungere** manualmente cartelle a questo elenco.  

### <a name="network-filtering"></a>Filtri di rete  

Consente di bloccare le connessioni in uscita da qualsiasi app a indirizzi IP o domini con reputazione negativa. Il filtro di rete è supportato in modalità di controllo e blocco.  

- **Protezione di rete**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione Defender: [EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=872618)  

  Lo scopo di questa impostazione è quello di proteggere gli utenti finali dalle app con accesso a tentativi di phishing, siti che ospitano exploit e contenuto dannoso su Internet. Impedisce anche ai browser di terze parti di connettersi a siti pericolosi.  

  - **Non configurato**: disabilitare questa funzionalità. Non viene impedito a utenti e app di connettersi a domini pericolosi. Gli amministratori non possono visualizzare questa attività in Microsoft Defender Security Center.  
  - **Abilita** - Consente di attivare la protezione della rete e impedire a utenti e app di connettersi a domini pericolosi. Gli amministratori possono visualizzare questa attività in Microsoft Defender Security Center.  
  - **Solo controllo** - Non viene impedito a utenti e app di connettersi a domini pericolosi. Gli amministratori possono visualizzare questa attività in Microsoft Defender Security Center.  

### <a name="exploit-protection"></a>Protezione dagli exploit  

- **Carica XML**  
  **Impostazione predefinita**: *Non configurato*  

  Per usare la protezione dagli exploit per [proteggere i dispositivi dagli exploit](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection), creare un file XML che include le impostazioni di mitigazione desiderate per il sistema e le applicazioni. Esistono due metodi per creare il file XML:  

  - *PowerShell*: usare uno o più cmdlet di PowerShell *Get-ProcessMitigation*, *Set-ProcessMitigation* e *ConvertTo-ProcessMitigationPolicy*. I cmdlet configurano le impostazioni di mitigazione ed esportano la relativa rappresentazione XML.  

  - *Interfaccia utente di Microsoft Defender Security Center*: in Microsoft Defender Security Center fare clic su Controllo delle app e del browser e quindi scorrere fino alla parte inferiore della schermata visualizzata per trovare Protezione dagli exploit. Usare prima di tutto le schede Impostazioni di sistema e Impostazioni programmi per configurare le impostazioni di mitigazione. Trovare quindi il collegamento Esporta impostazioni nella parte inferiore della schermata per esportare la relativa rappresentazione XML.  

- **Modifica dell'interfaccia di protezione dagli exploit da parte degli utenti**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione ExploitGuard: [ExploitProtectionSettings](https://go.microsoft.com/fwlink/?linkid=872887)  


  - **Blocca** - Consente di caricare un file XML che consente di configurare le restrizioni per memoria, flusso di controllo e criteri. Le impostazioni nel file XML possono essere usate per proteggere un'applicazione dagli exploit.  
  - **Non configurata** - Non viene usata alcuna configurazione personalizzata.  

## <a name="microsoft-defender-application-control"></a>Controllo di applicazioni di Microsoft Defender  

Scegliere altre app che devono essere controllate o possono essere ritenute attendibili per l'esecuzione da parte del Controllo di applicazioni di Microsoft Defender. I componenti Windows e tutte le app di Windows Store sono ritenuti automaticamente attendibili per l'esecuzione.  


- **Criteri relativi all'integrità del codice di controllo dell'applicazione**  
  **Impostazione predefinita**: Non configurato  
   CSP: [Provider di servizi di configurazione AppLocker](https://go.microsoft.com/fwlink/?linkid=874543)  

  - **Imponi** - Scegliere i criteri relativi all'integrità del codice di controllo dell'applicazione per i dispositivi degli utenti.  
  
    Dopo l'abilitazione in un dispositivo, il controllo delle applicazioni può essere disabilitato solo passando dalla modalità *Imponi* alla modalità *Controlla soltanto*. Il passaggio dalla modalità *Imponi* alla modalità *Non configurato* fa sì che il controllo delle applicazioni continui a essere applicato nei dispositivi assegnati.  

  - **Non configurata** - Il controllo delle applicazioni non viene aggiunto ai dispositivi. Tuttavia, le impostazioni aggiunte in precedenza continuano a essere applicate ai dispositivi assegnati. 
 
  - **Solo controllo** - Le applicazioni non vengono bloccate. Tutti gli eventi vengono registrati nei log del client locale.  

## <a name="microsoft-defender-credential-guard"></a>Microsoft Defender Credential Guard  

Microsoft Defender Credential Guard protegge contro attacchi relativi al furto di credenziali. Isola i segreti in modo che possa accedervi solo il software di sistema con privilegi.  

- **Credential Guard**  
  **Impostazione predefinita**: Disabilitato  
  [Provider di servizi di configurazione DeviceGuard](https://go.microsoft.com/fwlink/?linkid=872424)  

  - **Disabilita**: consente di disattivare Credential Guard in modalità remota, se attivato precedentemente con l'opzione **Abilita senza blocco UEFI**.  

  - **Abilita con blocco UEFI**: Credential Guard non può essere disabilitato in modalità remota usando una chiave del Registro di sistema o Criteri di gruppo.  

    > [!NOTE]
    > Se si usa questa impostazione e in seguito si vuole disabilitare Credential Guard, è necessario impostare Criteri di gruppo su **Disabilitato**. e cancellare fisicamente le informazioni di configurazione UEFI da ogni computer. Credential Guard rimane abilitato fino a quando è presente la configurazione UEFI.  

  - **Abilita senza blocco UEFI**: consente di disabilitare Credential Guard in modalità remota usando Criteri di gruppo. È necessario che i dispositivi che usano questa impostazione eseguano Windows 10 versione 1511 e successive.  

  Quando si *abilita* Credential Guard, vengono abilitate anche le funzionalità obbligatorie seguenti:  
  
  - **Abilita la sicurezza basata su virtualizzazione**  
    viene attivata al riavvio successivo. La sicurezza basata sulla virtualizzazione usa Windows Hypervisor per offrire il supporto per i servizi di sicurezza.  
  - **Avvio protetto con accesso diretto alla memoria**  
    attiva la sicurezza basata su virtualizzazione con l'avvio protetto e l'accesso diretto alla memoria. Le protezioni DMA richiedono supporto hardware e vengono abilitate solo nei dispositivi configurati correttamente.  

## <a name="microsoft-defender-security-center"></a>Microsoft Defender Security Center  

Microsoft Defender Security Center funziona come un'app o un processo separato da ognuna delle singole funzionalità. Visualizza le notifiche tramite il centro notifiche. Funge da agente di raccolta o da posizione centralizzata per visualizzare lo stato ed eseguire alcune attività di configurazione per ogni funzionalità. Per altre informazioni, vedere la documentazione di [Microsoft Defender](https://docs.microsoft.com/windows/threat-protection/windows-defender-security-center/windows-defender-security-center).  

### <a name="microsoft-defender-security-center-app-and-notifications"></a>App e notifiche di Microsoft Defender Security Center  

È possibile bloccare l'accesso degli utenti finali alle diverse aree dell'app Microsoft Defender Security Center. Se si nasconde una sezione, vengono bloccate anche le notifiche correlate.  

- **Protezione da virus e minacce**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione WindowsDefenderSecurityCenter: [DisableVirusUI](https://go.microsoft.com/fwlink/?linkid=873662)  

  Configurare se gli utenti finali possono visualizzare l'area Protezione da virus e minacce in Microsoft Defender Security Center. Nascondendo questa sezione verranno bloccate anche tutte le notifiche correlate alla protezione da virus e minacce.  

  - **Non configurato**  
  - **Nascondi**  

- **Protezione ransomware**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione WindowsDefenderSecurityCenter: [HideRansomwareDataRecovery](https://go.microsoft.com/fwlink/?linkid=873664)  

  Configurare se gli utenti finali possono visualizzare l'area Protezione ransomware in Microsoft Defender Security Center. Nascondendo questa sezione verranno bloccate anche tutte le notifiche correlate alla protezione del ransomware.  

  - **Non configurato**  
  - **Nascondi**  

- **Protezione account**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione WindowsDefenderSecurityCenter: [DisableAccountProtectionUI](https://go.microsoft.com/fwlink/?linkid=873666)  

  Configurare se gli utenti finali possono visualizzare l'area Protezione account in Microsoft Defender Security Center. Nascondendo questa sezione verranno bloccate anche tutte le notifiche correlate alla protezione degli account.  

  - **Non configurato**  
  - **Nascondi**  

- **Protezione firewall e della rete**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione WindowsDefenderSecurityCenter: [DisableNetworkUI](https://go.microsoft.com/fwlink/?linkid=873668)  

  Configurare se gli utenti finali possono visualizzare l'area Protezione firewall e della rete in Microsoft Defender Security Center. Nascondendo questa sezione verranno bloccate anche tutte le notifiche correlate alla protezione di firewall e rete.  

  - **Non configurato**  
  - **Nascondi**  

- **Controllo delle app e del browser**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione WindowsDefenderSecurityCenter: [DisableAppBrowserUI](https://go.microsoft.com/fwlink/?linkid=873669)  

  Configurare se gli utenti finali possono visualizzare l'area Controllo delle app e del browser in Microsoft Defender Security Center. Nascondendo questa sezione verranno bloccate anche tutte le notifiche correlate al controllo di app e browser.  

  - **Non configurato**  
  - **Nascondi**  

- **Protezione hardware**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione WindowsDefenderSecurityCenter: [DisableDeviceSecurityUI](https://go.microsoft.com/fwlink/?linkid=873670)  

  Configurare se gli utenti finali possono visualizzare l'area Protezione hardware in Microsoft Defender Security Center. Nascondendo questa sezione verranno bloccate anche tutte le notifiche correlate alla protezione dell'hardware.  

  - **Non configurato**  
  - **Nascondi**  

- **Prestazioni e integrità del dispositivo**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione WindowsDefenderSecurityCenter: [DisableHealthUI](https://go.microsoft.com/fwlink/?linkid=873671)  

  Configurare se gli utenti finali possono visualizzare l'area Prestazioni e integrità del dispositivo in Microsoft Defender Security Center. Nascondendo questa sezione verranno bloccate anche tutte le notifiche correlate alle prestazioni e all'integrità dei dispositivi.  
  
  - **Non configurato**  
  - **Nascondi**  

- **Opzioni famiglia**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione WindowsDefenderSecurityCenter: [DisableFamilyUI](https://go.microsoft.com/fwlink/?linkid=873673)  

  Configurare se gli utenti finali possono visualizzare l'area Opzioni famiglia in Microsoft Defender Security Center. Nascondendo questa sezione verranno bloccate anche tutte le notifiche correlate alle opzioni per la famiglia.  
  
  - **Non configurato**  
  - **Nascondi**  

- **Notifiche dalle aree visualizzate dell'app**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione WindowsDefenderSecurityCenter: [DisableNotifications](https://go.microsoft.com/fwlink/?linkid=873675)  

  scegliere le notifiche da visualizzare agli utenti finali. Le notifiche non critiche includono riepiloghi dell'attività di Antivirus Microsoft Defender, comprese le notifiche relative al completamento delle analisi. Tutte le altre notifiche sono considerate critiche.  

  - **Non configurato**  
  - **Blocca le notifiche non critiche**  
  - **Blocca tutte le notifiche**  

- **Icona di Centro sicurezza PC Windows nell'area di notifica**  
  **Impostazione predefinita**: Non configurato  

  Consente di configurare la visualizzazione del controllo dell'area di notifica. L'utente deve disconnettersi e accedere o riavviare il computer per applicare l'impostazione.  
  
  - **Non configurato**  
  - **Nascondi**  

- **Pulsante Cancella TPM**  
  **Impostazione predefinita**: Non configurato  

  Consente di configurare la visualizzazione del pulsante Cancella TPM.  
  
  - **Non configurato**  
  - **Disabilitato**  

- **Avviso per l'aggiornamento del firmware TPM**  
  **Impostazione predefinita**: Non configurato  
  
  Consente di configurare la visualizzazione dell'aggiornamento del firmware TPM quando viene rilevato un firmware vulnerabile.  

  - **Non configurato**  
  - **Nascondi**  

- **Protezione antimanomissione**  
  **Impostazione predefinita**: Non configurato

  Consente di attivare o disattivare la protezione antimanomissione nei dispositivi. Per usare la protezione antimanomissione, è necessario [integrare Microsoft Defender Advanced Threat Protection con Intune](advanced-threat-protection.md) e avere [licenze Enterprise Mobility + Security E5](../fundamentals/licenses.md).  
  - **Non configurata** - Non vengono apportate modifiche alle impostazioni del dispositivo.
  - **Abilitata** - La protezione antimanomissione è attivata e le restrizioni vengono applicate nei dispositivi.
  - **Disabilitata** La protezione antimanomissione è disattivata e non vengono applicate le restrizioni.

### <a name="it-contact-information"></a>Informazioni di contatto del reparto IT  

Specificare le informazioni di contatto del reparto IT da visualizzare nell'app Microsoft Defender Security Center e nelle relative notifiche.  

È possibile scegliere **Visualizza nell'app e nelle notifiche**, **Visualizza solo nell'app**, **Visualizza solo nelle notifiche** o **Non visualizzare**. Immettere il **nome dell'organizzazione IT** e almeno una delle opzioni di contatto seguenti:  


- **Informazioni di contatto del reparto IT**  
  **Impostazione predefinita**: Non visualizzare  
  Provider di servizi di configurazione WindowsDefenderSecurityCenter: [EnableCustomizedToasts](https://go.microsoft.com/fwlink/?linkid=873676)  
  
  Consente di specificare dove visualizzare le informazioni di contatto del reparto IT per gli utenti finali.  
  
  - **Visualizza nell'app e nelle notifiche**  
  - **Visualizza solo nell'app**  
  - **Visualizza solo nelle notifiche**  
  - **Non visualizzare**  

  Quando è configurato per la visualizzazione, è possibile configurare le impostazioni seguenti:  

  - **Nome organizzazione IT**  
    **Impostazione predefinita**: *Non configurato*  
    Provider di servizi di configurazione WindowsDefenderSecurityCenter: [CompanyName](https://go.microsoft.com/fwlink/?linkid=873677)  

  - **Numero di telefono del reparto IT o ID Skype**  
    **Impostazione predefinita**: *Non configurato*  
    Provider di servizi di configurazione WindowsDefenderSecurityCenter: [Telefono](https://go.microsoft.com/fwlink/?linkid=873678) 

  - **Indirizzo di posta elettronica del reparto IT**  
    **Impostazione predefinita**: *Non configurato*  
    Provider di servizi di configurazione WindowsDefenderSecurityCenter: [Posta elettronica](https://go.microsoft.com/fwlink/?linkid=873679)  

  - **URL del sito Web del supporto tecnico IT**  
    **Impostazione predefinita**: *Non configurato*  
    Provider di servizi di configurazione WindowsDefenderSecurityCenter: [URL](https://go.microsoft.com/fwlink/?linkid=873680)  
 
## <a name="local-device-security-options"></a>Opzioni di sicurezza dei dispositivi locali  

Usare queste opzioni per configurare le impostazioni di sicurezza locali nei dispositivi Windows 10.  

### <a name="accounts"></a>Account  

- **Aggiungi nuovi account Microsoft**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione LocalPoliciesSecurityOptions: [Accounts_BlockMicrosoftAccounts](https://go.microsoft.com/fwlink/?linkid=867916)  


  - **Blocca**: consente di impedire agli utenti di aggiungere nuovi account Microsoft nel dispositivo.  
  - **Non configurata**: gli utenti possono usare gli account Microsoft nel dispositivo.  

- **Accesso remoto senza password**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione LocalPoliciesSecurityOptions: [Accounts_LimitLocalAccountUseOfBlankPasswordsToConsoleLogonOnly](https://go.microsoft.com/fwlink/?linkid=867890)  


   - **Blocca** consente solo agli account locali con password vuote di accedere tramite la tastiera del dispositivo.  
   - **Non configurato**: consente agli account locali con password vuote di eseguire l'accesso da percorsi diversi rispetto al dispositivo fisico.  

#### <a name="admin"></a>Amministratore  

- **Account amministratore locale**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione LocalPoliciesSecurityOptions: [Accounts_LimitLocalAccountUseOfBlankPasswordsToConsoleLogonOnly](https://go.microsoft.com/fwlink/?linkid=867850)  


  - **Blocca** consente di impedire l'uso di un account amministratore locale.  
  - **Non configurato**  

- **Rinomina l'account amministratore**  
  **Impostazione predefinita**: *Non configurato*  
  Provider di servizi di configurazione LocalPoliciesSecurityOptions: [Accounts_RenameAdministratorAccount](https://go.microsoft.com/fwlink/?linkid=867917)  
 

  Definire un nome account diverso da associare all'ID di sicurezza (SID) per l'account "Amministratore".  

 #### <a name="guest"></a>Guest  

- **Account Guest**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione LocalPoliciesSecurityOptions: [LocalPoliciesSecurityOptions](https://go.microsoft.com/fwlink/?linkid=867853)  

  - **Blocca** - Consente di impedire l'uso di un account Guest.  
  - **Non configurato**  

- **Rinomina l'account Guest**  
  **Impostazione predefinita**: *Non configurato*  
  Provider di servizi di configurazione LocalPoliciesSecurityOptions: [Accounts_RenameGuestAccount](https://go.microsoft.com/fwlink/?linkid=867918)  
  
  Definire un nome account diverso da associare all'ID di sicurezza (SID) per l'account "Guest".  

### <a name="devices"></a>Dispositivi  

- **Disancora il dispositivo senza accesso**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione LocalPoliciesSecurityOptions: [Devices_AllowUndockWithoutHavingToLogon](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-devices-allowundockwithouthavingtologon)  

  - **Blocca**: l'utente deve eseguire l'accesso al dispositivo per ricevere l'autorizzazione a disinserire il dispositivo dall'alloggiamento di espansione.
  - **Non configurato**: gli utenti possono premere il pulsante di espulsione fisico del dispositivo portatile inserito nell'alloggiamento di espansione per disinserire in modo sicuro il dispositivo.

- **Installa i driver della stampante per le stampanti condivise**  
  **Impostazione predefinita**:  Non configurato  
  Provider di servizi di configurazione LocalPoliciesSecurityOptions: [Devices_PreventUsersFromInstallingPrinterDriversWhenConnectingToSharedPrinters](https://go.microsoft.com/fwlink/?linkid=867921)  


  - **Abilitato**: qualsiasi utente può installare un driver della stampante durante la connessione a una stampante condivisa.  
  - **Non configurato**: solo gli amministratori possono installare un driver della stampante come parte della connessione a una stampante condivisa.  

- **Limita l'accesso al CD-ROM solo all'utente attivo locale**  
  **Impostazione predefinita**:  Non configurato  
  CSP: [Devices_RestrictCDROMAccessToLocallyLoggedOnUserOnly](https://go.microsoft.com/fwlink/?linkid=867922)  


  - **Abilitato**: solo gli utenti che hanno eseguito l'accesso in modo interattivo possono usare i supporti CD-ROM. Se questo criterio è abilitato e nessun utente è connesso in modo interattivo, l'accesso al CD-ROM avviene attraverso la rete.  
  - **Non configurata** - Chiunque può accedere al CD-ROM.  

- **Formatta e rimuovi supporti rimovibili**  
  **Impostazione predefinita**: Administrators  
  CSP: [Devices_AllowedToFormatAndEjectRemovableMedia](https://go.microsoft.com/fwlink/?linkid=867920)  
 

  consente di determinare chi è autorizzato a formattare e rimuovere i supporti rimovibili NTFS:  
  - **Non configurato**  
  - **Amministratori**  
  - **Amministratori e utenti esperti**  
  - **Amministratori e utenti interattivi**  

### <a name="interactive-logon"></a>Accesso interattivo  

- **Minuti di inattività della schermata di blocco prima dell'attivazione dello screen saver**  
  **Impostazione predefinita**: *Non configurato*  
  Provider di servizi di configurazione LocalPoliciesSecurityOptions: [InteractiveLogon_MachineInactivityLimit](https://go.microsoft.com/fwlink/?linkid=867891)  


  Immettere il numero massimo di minuti di inattività nella schermata di accesso del desktop interattivo prima dell'attivazione dello screen saver. (**0** - **99999**)  

- **Richiedi CTRL+ALT+CANC per accedere**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione LocalPoliciesSecurityOptions: [InteractiveLogon_DoNotRequireCTRLALTDEL](https://go.microsoft.com/fwlink/?linkid=867951)  


  - **Abilita**: agli utenti viene richiesto di premere CTRL+ALT+CANC prima di accedere a Windows.
  - **Non configurato**: gli utenti non devono premere CTRL+ALT+CANC per accedere.

- **Comportamento in caso di rimozione della smart card**  
  **Impostazione predefinita**: Blocca workstation   
  Provider di servizi di configurazione LocalPoliciesSecurityOptions: [InteractiveLogon_SmartCardRemovalBehavior](https://go.microsoft.com/fwlink/?linkid=868437)  
    
  determina le azioni che vengono eseguite quando la smart card di un utente connesso viene rimossa dal lettore di smart card. Le opzioni disponibili sono:  

  - **Blocca workstation**: quando la smart card viene rimossa, la workstation risulta bloccata. Questa opzione consente all'utente di allontanarsi, portare con sé la smart card e mantenere comunque una sessione protetta.  
  - **Nessuna azione**  
  - **Imponi disconnessione**: l'utente viene automaticamente disconnesso quando la smart card viene rimossa.  
  - **Disconnetti in caso di sessione dei Servizi Desktop remoto**: la rimozione della smart card determina la disconnessione della sessione senza disconnettere l'utente. Questa opzione consente all'utente di inserire la smart card e riprendere la sessione in un secondo momento oppure in un altro computer dotato di lettore di smart card, senza dover accedere di nuovo. Se la sessione è locale, questo criterio funziona in modo identico all'opzione Blocca workstation.  

#### <a name="display"></a>Schermo  

- **Informazioni utente nella schermata di blocco**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione LocalPoliciesSecurityOptions: [InteractiveLogon_DisplayUserInformationWhenTheSessionIsLocked](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-interactivelogon-displayuserinformationwhenthesessionislocked)  

  consente di configurare le informazioni utente visualizzate quando la sessione è bloccata. Se questa opzione non viene configurata, vengono mostrati il nome visualizzato dell'utente, il dominio e il nome utente.  

  - **Non configurato**  
  - **Nome visualizzato dell'utente, dominio e nome utente**  
  - **Solo nome visualizzato dell'utente**  
  - **Non visualizzare le informazioni utente**  

- **Nascondi l'ultimo utente connesso**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione LocalPoliciesSecurityOptions: [InteractiveLogon_DoNotDisplayLastSignedIn](https://go.microsoft.com/fwlink/?linkid=868437)  
  
  
  - **Abilita** - Il nome utente viene nascosto.  
  - **Non configurata** - Mostra l'ultimo nome utente.  

- **Nascondi il nome utente all'accesso**
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione LocalPoliciesSecurityOptions: [InteractiveLogon_DoNotDisplayUsernameAtSignIn](https://go.microsoft.com/fwlink/?linkid=867959)  

  
  - **Abilita** - Il nome utente viene nascosto.  
  - **Non configurata** - Mostra l'ultimo nome utente.  

- **Titolo del messaggio di accesso**  
  **Impostazione predefinita**: *Non configurato*  
  Provider di servizi di configurazione LocalPoliciesSecurityOptions: [InteractiveLogon_MessageTitleForUsersAttemptingToLogOn](https://go.microsoft.com/fwlink/?linkid=867964)  

  imposta il titolo del messaggio per gli utenti che eseguono l'accesso.  

- **Testo del messaggio di accesso**  
  **Impostazione predefinita**: *Non configurato*  
  Provider di servizi di configurazione LocalPoliciesSecurityOptions: [InteractiveLogon_MessageTextForUsersAttemptingToLogOn](https://go.microsoft.com/fwlink/?linkid=867962)  

  imposta il testo del messaggio per gli utenti che eseguono l'accesso.  
  
### <a name="network-access-and-security"></a>Accesso alla rete e sicurezza

- **Accesso anonimo alle named pipe e alle condivisioni**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione LocalPoliciesSecurityOptions: [NetworkAccess_RestrictAnonymousAccessToNamedPipesAndShares](https://go.microsoft.com/fwlink/?linkid=868432)  

  - **Non configurato**: consente di limitare l'accesso anonimo alle impostazioni di condivisioni e named pipe. Si applica alle impostazioni a cui è possibile accedere anonimamente.  
  - **Blocca**: disabilita questo criterio, rendendo disponibile l'accesso anonimo.  

- **Enumerazione anonima degli account SAM**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione LocalPoliciesSecurityOptions: [NetworkAccess_DoNotAllowAnonymousEnumerationOfSAMAccounts](https://go.microsoft.com/fwlink/?linkid=868434)  
  
  - **Non configurata**: gli utenti anonimi possono enumerare gli account SAM.  
  - **Blocca**: per impedire l'enumerazione anonima degli account SAM.  

- **Enumerazione anonima di account e condivisioni SAM**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione LocalPoliciesSecurityOptions: [NetworkAccess_DoNotAllowAnonymousEnumerationOfSamAccountsAndShares](https://go.microsoft.com/fwlink/?linkid=868435)  

  - **Non configurato**: consente agli utenti anonimi di enumerare i nomi di account di dominio e condivisioni di rete.  
  - **Blocca**: per impedire l'enumerazione anonima di account e condivisioni SAM. 

- **Valore hash di LAN Manager archiviato alla modifica della password**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione LocalPoliciesSecurityOptions: [NetworkSecurity_DoNotStoreLANManagerHashValueOnNextPasswordChange](https://go.microsoft.com/fwlink/?linkid=868431)  
   
  Determinare se il valore hash per le password viene archiviato la volta successiva che la password viene modificata. 
  - **Non configurata** - Il valore hash non viene archiviato.  
  - **Blocca**: LAN Manager (LM) archivia il valore hash per la nuova password.  

- **Richieste di autenticazione PKU2U**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione LocalPoliciesSecurityOptions: [NetworkSecurity_AllowPKU2UAuthenticationRequests](https://go.microsoft.com/fwlink/?linkid=867892)  

  - **Non configurata** - Consente le richieste PU2U.  
  - **Blocca** - Impedisce le richieste di autenticazione PKU2U al dispositivo.  

- **Limita le connessioni RPC remote a SAM**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione LocalPoliciesSecurityOptions: [NetworkAccess_RestrictClientsAllowedToMakeRemoteCallsToSAM](https://go.microsoft.com/fwlink/?linkid=867893)  
  
  - **Non configurata** - Viene usato il descrittore di sicurezza predefinito, che può consentire a utenti e gruppi di effettuare chiamate RPC remote a SAM.
  - **Consenti** - Impedisce a utenti e gruppi di effettuare chiamate RPC remote a Gestione account di protezione (SAM), in cui sono archiviati gli account utente e le password. **Consenti** consente anche di modificare la stringa SDDL (Security Descriptor Definition Language) predefinita per consentire o impedire in modo esplicito a utenti e gruppi di effettuare queste chiamate remote.  

    - **Descrittore di sicurezza**  
      **Impostazione predefinita**: *Non configurato*  
    
- **Sicurezza sessione minima per client basati su NTLM SSP**  
  **Impostazione predefinita**: Nessuno  
  Provider di servizi di configurazione LocalPoliciesSecurityOptions: [NetworkSecurity_MinimumSessionSecurityForNTLMSSPBasedClients](https://aka.ms/policy-csp-localpoliciessecurityoptions-networksecurity-minimumsessionsecurityforntlmsspbasedclients)  
  
  Questa impostazione di sicurezza consente ai server di richiedere la negoziazione della crittografia a 128 bit e/o della sicurezza di sessione NTLMv2.  

  - **Nessuno**  
  - **Richiedi sicurezza sessione NTLMv2**  
  - **Richiedi crittografia a 128 bit**  
  - **NTLM V2 e la crittografia a 128 bit**  
 
- **Sicurezza sessione minima per server basati su NTLM SSP**  
  **Impostazione predefinita**: Nessuno  
  Provider di servizi di configurazione LocalPoliciesSecurityOptions: [NetworkSecurity_MinimumSessionSecurityForNTLMSSPBasedServers](https://aka.ms/policy-csp-localpoliciessecurityoptions-networksecurity-minimumsessionsecurityforntlmsspbasedservers)  

  Questa impostazione di sicurezza specifica il protocollo di autenticazione Richiesta di verifica/Risposta usato per gli accessi di rete.  

  - **Nessuno**  
  - **Richiedi sicurezza sessione NTLMv2**  
  - **Richiedi crittografia a 128 bit**  
  - **NTLM V2 e la crittografia a 128 bit**  

- **Livello di autenticazione di LAN Manager**  
  **Impostazione predefinita**: LM e NTLM  
  Provider di servizi di configurazione LocalPoliciesSecurityOptions: [NetworkSecurity_LANManagerAuthenticationLevel](https://aka.ms/policy-csp-localpoliciessecurityoptions-lanmanagerauthenticationlevel)  


  - **LM e NTLM**  
  - **LM, NTLM e NTLMv2**  
  - **NTLM**  
  - **NTLMv2**  
  - **NTLMv2 ma non LM**  
  - **NTLMv2 ma non LM o NTLM**  
  
- **Accessi guest non sicuri**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione LanmanWorkstation: [LanmanWorkstation](https://aka.ms/policy-csp-lanmanworkstation-enableinsecureguestlogons)  

  Se si abilita questa impostazione, il client SMB rifiuterà gli accessi guest non sicuri.  

  - **Non configurato**  
  - **Blocca** - Il client SMB rifiuta gli accessi guest non sicuri.  

### <a name="recovery-console-and-shutdown"></a>Console di ripristino di emergenza e arresto  

- **Cancella il file di paging della memoria virtuale all'arresto**  
  **Impostazione predefinita**: Non configurato  
   Provider di servizi di configurazione LocalPoliciesSecurityOptions: [Shutdown_ClearVirtualMemoryPageFile](https://go.microsoft.com/fwlink/?linkid=867914)  


  - **Abilita**: consente di cancellare il file di paging della memoria virtuale quando il dispositivo viene spento.  
  - **Non configurato**: la memoria virtuale non viene cancellata.  

- **Arresta senza accesso**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione LocalPoliciesSecurityOptions: [Shutdown_AllowSystemToBeShutDownWithoutHavingToLogOn](https://go.microsoft.com/fwlink/?linkid=867912)  

  
  - **Blocca**: nasconde l'opzione di arresto del sistema nella schermata di accesso di Windows. Gli utenti devono accedere al dispositivo e quindi arrestarlo.  
  - **Non configurato**: consente agli utenti di arrestare il dispositivo dalla schermata di accesso di Windows.  

### <a name="user-account-control"></a>Controllo dell'account utente  

- **Integrità UIA senza posizione sicura**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione LocalPoliciesSecurityOptions: [UserAccountControl_OnlyElevateUIAccessApplicationsThatAreInstalledInSecureLocations](https://go.microsoft.com/fwlink/?linkid=867897)  
  
  - **Blocca** - Le app in una posizione sicura nel file system verranno eseguite solo con l'integrità UIAccess.  
  - **Non configurato**: consente l'esecuzione delle app con l'integrità UIAccess, anche se le app non sono in una posizione sicura nel file system.  

- **Virtualizzare gli errori di scrittura nel file e nel Registro di sistema in percorsi specifici per ogni utente**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione LocalPoliciesSecurityOptions: [UserAccountControl_VirtualizeFileAndRegistryWriteFailuresToPerUserLocations](https://go.microsoft.com/fwlink/?linkid=867900)  

  - **Abilitato**: le applicazioni che eseguono la scrittura dei dati in percorsi protetti genereranno errori.  
  - **Non configurato**: gli errori di scrittura delle applicazioni in fase di esecuzione vengono reindirizzati su percorsi utente definiti per il file system e per il Registro di sistema.  

- **Esegui con privilegi elevati solo i file eseguibili firmati e convalidati**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione LocalPoliciesSecurityOptions: [UserAccountControl_OnlyElevateUIAccessApplicationsThatAreInstalledInSecureLocations](https://go.microsoft.com/fwlink/?linkid=867965)  

  - **Abilitato**: applicare la convalida del percorso di certificazione PKI di un file eseguibile prima che possa essere eseguito.  
  - **Non configurato**: non applicare la convalida del percorso di certificazione PKI di un file eseguibile prima che possa essere eseguito.  

#### <a name="uia-elevation-prompt-behavior"></a>Comportamento della richiesta di elevazione dei privilegi UIA  

- **Richiesta di elevazione dei privilegi per amministratori**  
  **Impostazione predefinita**: Richiedi il consenso per file binari non Windows  
  Provider di servizi di configurazione LocalPoliciesSecurityOptions: [UserAccountControl_BehaviorOfTheElevationPromptForAdministrators](https://go.microsoft.com/fwlink/?linkid=867895)  

  Definire il comportamento della richiesta di elevazione dei privilegi per gli amministratori in modalità Approvazione amministratore.  

  - **Non configurato**  
  - **Esegui con privilegi elevati senza chiedere conferma**  
  - **Richiedi credenziali sul desktop sicuro**  
  - **Richiedi credenziali**  
  - **Richiedi consenso**  
  - **Richiedi consenso per file binari non Windows**  


- **Richiesta di elevazione dei privilegi per utenti standard**  
  **Impostazione predefinita**: Richiedi credenziali  
  Provider di servizi di configurazione LocalPoliciesSecurityOptions: [UserAccountControl_BehaviorOfTheElevationPromptForStandardUsers](https://go.microsoft.com/fwlink/?linkid=867896)  

  Definire il comportamento della richiesta di elevazione dei privilegi per gli utenti standard.  

  - **Non configurato**  
  - **Nega automaticamente richieste di elevazione**  
  - **Richiedi credenziali sul desktop sicuro**  
  - **Richiedi credenziali**  

- **Indirizza le richieste di elevazione dei privilegi al desktop interattivo dell'utente**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione LocalPoliciesSecurityOptions: [UserAccountControl_SwitchToTheSecureDesktopWhenPromptingForElevation](https://go.microsoft.com/fwlink/?linkid=867899)  


  - **Abilitata** - Tutte le richieste di elevazione dei privilegi vengano inviate al desktop dell'utente interattivo anziché al desktop protetto. Viene usata qualsiasi impostazione relativa ai criteri sul comportamento delle richieste per amministratori e utenti standard.  
  - **Non configurato**: tutte le richieste di elevazione dei privilegi vengono inviate al desktop sicuro, indipendentemente dalle impostazioni relative ai criteri sul comportamento delle richieste per amministratori e utenti standard.

- **Prompt con privilegi elevati per installazioni di app**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione LocalPoliciesSecurityOptions: [UserAccountControl_DetectApplicationInstallationsAndPromptForElevation](https://go.microsoft.com/fwlink/?linkid=867901)  

   - **Abilitato**: i pacchetti di installazione delle applicazioni non vengono rilevati e non viene richiesta l'elevazione dei privilegi.
   - **Non configurato**: all'utente vengono richiesti nome utente e password amministrativi quando un pacchetto di installazione di un'applicazione richiede privilegi elevati.

- **Richiesta di elevazione dei privilegi UIA senza desktop protetto**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione LocalPoliciesSecurityOptions: [UserAccountControl_AllowUIAccessApplicationsToPromptForElevation](https://go.microsoft.com/fwlink/?linkid=867894)  

- **Abilita**: consente alle app UIAccess di richiedere l'elevazione dei privilegi senza usare il desktop protetto.  
- **Non configurata** - Le richieste di elevazione dei privilegi usano un desktop protetto.  

#### <a name="admin-approval-mode"></a>Modalità Approvazione amministratore  

- **Modalità Approvazione amministratore per l'amministratore predefinito**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione LocalPoliciesSecurityOptions: [UserAccountControl_UseAdminApprovalMode](https://go.microsoft.com/fwlink/?linkid=867902)  

  - **Abilitato**: consente all'account predefinito Administrator di usare la modalità Approvazione amministratore. Per qualunque operazione che richiede l'elevazione dei privilegi viene richiesta l'approvazione dell'utente.  
  - **Non configurato**: tutte le app vengono eseguite con privilegi di amministratore completi.  

- **Esegui tutti gli amministratori in modalità Approvazione amministratore**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione LocalPoliciesSecurityOptions: [UserAccountControl_RunAllAdministratorsInAdminApprovalMode](https://go.microsoft.com/fwlink/?linkid=867898)  


  - **Abilitata**: la modalità Approvazione amministratore viene abilitata.  
  - **Non configurato**: consente di disabilitare la modalità Approvazione amministratore e tutte le impostazioni dei criteri correlati di Controllo dell'account utente.  

### <a name="microsoft-network-client"></a>Client di rete Microsoft  

- **Firma digitalmente le comunicazioni (se il server lo consente)**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione LocalPoliciesSecurityOptions: [MicrosoftNetworkClient_DigitallySignCommunicationsIfServerAgrees](https://go.microsoft.com/fwlink/?linkid=868423)  

  determina se il client SMB negozia la firma dei pacchetti SMB.  
  - **Blocca**: il client SMB non negozia mai la firma dei pacchetti SMB.
  - **Non configurato**: il client di rete Microsoft chiede al server di eseguire la firma dei pacchetti SMB al momento della configurazione della sessione. Se la firma dei pacchetti è abilitata nel server, questa verrà negoziata.  

- **Invia password non crittografate a server SMB di terze parti**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione LocalPoliciesSecurityOptions: [MicrosoftNetworkClient_SendUnencryptedPasswordToThirdPartySMBServers](https://go.microsoft.com/fwlink/?linkid=868426)  


  - **Blocca**: il redirector SMB (Server Message Block) può inviare password in testo non crittografato a server SMB non Microsoft che non supportano la crittografia della password durante l'autenticazione.  
  - **Non configurata**: impedisce l'invio di password come testo non crittografato. Le password vengono crittografate.  

- **Firma digitalmente le comunicazioni (sempre)**  
  **Impostazione predefinita**: Non configurato  
  Provider di servizi di configurazione LocalPoliciesSecurityOptions: [MicrosoftNetworkClient_DigitallySignCommunicationsAlways](https://go.microsoft.com/fwlink/?linkid=868425)  


  - **Abilita**: il server di rete Microsoft comunica con un client di rete Microsoft solo se tale client accetta l'esecuzione della firma dei pacchetti SMB.  
  - **Non configurata**: la firma dei pacchetti SMB viene negoziata tra il client e il server.  

### <a name="microsoft-network-server"></a>Server di rete Microsoft  
  
- **Firma digitalmente le comunicazioni (se il client lo consente)**  
  **Impostazione predefinita**: Non configurato  
  CSP: [MicrosoftNetworkServer_DigitallySignCommunicationsIfClientAgrees](https://go.microsoft.com/fwlink/?linkid=868429)  

  - **Abilita**: il server di rete Microsoft negozierà la firma dei pacchetti SMB in base a quanto richiesto dal client, ovvero se la firma dei pacchetti è abilitata sul client, la firma dei pacchetti sarà negoziata.  
  - **Non configurata**: il client SMB non negozia mai la firma dei pacchetti SMB.  

- **Firma digitalmente le comunicazioni (sempre)**  
  **Impostazione predefinita**: Non configurato  
  CSP: [MicrosoftNetworkServer_DigitallySignCommunicationsAlways](https://go.microsoft.com/fwlink/?linkid=868428)  

  - **Abilita**: il server di rete Microsoft comunica con un client di rete Microsoft solo se tale client accetta l'esecuzione della firma dei pacchetti SMB.  
  - **Non configurata**: la firma dei pacchetti SMB viene negoziata tra il client e il server.  

## <a name="xbox-services"></a>Servizi Xbox

- **Attività Salva gioco di Xbox**  
  **Impostazione predefinita**: Non configurato  
  CSP: [TaskScheduler/EnableXboxGameSaveTask](https://go.microsoft.com/fwlink/?linkid=875480)  
   
  Questa impostazione consente di determinare se l'attività Salva gioco di Xbox è Abilitata o Disabilitata.  
  - **Enabled**
  - **Non configurato**

- **Xbox Accessory Management Service**  
  **Impostazione predefinita**: Manuale  
  CSP: [SystemServices/ConfigureXboxAccessoryManagementServiceStartupMode](https://go.microsoft.com/fwlink/?linkid=875481)  

  Questa impostazione determina il tipo di avvio di Accessory Management Service.  
  - **Manuale**
  - **Automatic** (Automatica)
  - **Disabilitato**

- **Servizio Gestione autenticazione Xbox Live**  
  **Impostazione predefinita**: Manuale  
  CSP: [SystemServices/ConfigureXboxLiveAuthManagerServiceStartupMode](https://go.microsoft.com/fwlink/?linkid=875482)  
 
  Questa impostazione determina il tipo di avvio del servizio Gestione autenticazione Xbox Live.  
  - **Manuale**
  - **Automatic** (Automatica)
  - **Disabilitato**
 
- **Servizio Salva Gioco di Xbox Live**  
  **Impostazione predefinita**: Manuale  
  CSP: [SystemServices/ConfigureXboxLiveGameSaveServiceStartupMode](https://go.microsoft.com/fwlink/?linkid=875483)  

  Questa impostazione determina il tipo di avvio del servizio Salva Gioco di Xbox Live.  
  - **Manuale**
  - **Automatic** (Automatica)
  - **Disabilitato**

- **Servizio di rete Xbox Live**  
  **Impostazione predefinita**: Manuale  
  CSP: [SystemServices/ConfigureXboxLiveNetworkingServiceStartupMode](https://go.microsoft.com/fwlink/?linkid=875484)  

  Questa impostazione determina il tipo di avvio del servizio di rete.  
  - **Manuale**
  - **Automatic** (Automatica)
  - **Disabilitato**

## <a name="next-steps"></a>Passaggi successivi

Il profilo è stato creato, ma non è ancora operativo. [Assegnare il profilo](../configuration/device-profile-assign.md) e [monitorarne lo stato](../configuration/device-profile-monitor.md).  

Configurare le impostazioni di Endpoint Protection nei dispositivi [macOS](endpoint-protection-macos.md).  
