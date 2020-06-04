---
title: Impostazioni del firewall per la sicurezza degli endpoint di Intune | Microsoft Docs
description: Impostazioni dei criteri del firewall per la sicurezza degli endpoint per Windows e macOS in Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
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
ms.openlocfilehash: d90870a60ea292939926816bb74b5d285dc6a09f
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431605"
---
# <a name="firewall-policy-settings-for-endpoint-security-in-intune"></a>Impostazioni dei criteri di riduzione del firewall per la sicurezza degli endpoint di Intune

Visualizzare le impostazioni che è possibile configurare nei profili per i criteri del *firewall* nel nodo Sicurezza degli endpoint di Intune come parte dei [criteri di sicurezza degli endpoint](../protect/endpoint-security-policy.md).

Piattaforme e profili supportati:

- **macOS**:
  - Profilo: **firewall macOS**

- **Windows 10 e versioni successive**:
  - Profilo: **Microsoft Defender Firewall**

## <a name="macos-firewall-profile"></a>Profilo firewall macOS

### <a name="firewall"></a>Firewall

Le impostazioni seguenti sono configurate come [Criteri di sicurezza degli endpoint per i firewall macOS](../protect/endpoint-security-firewall-policy.md)

- **Abilita il firewall**

  - **Non configurato** (*impostazione predefinita*)
  - **Sì** - Abilita il firewall.
  
  Se impostata su *Sì*, è possibile configurare le impostazioni seguenti.  

  - **Bloccare tutte le connessioni in ingresso**

    - **Non configurato** (*impostazione predefinita*)
    - **Sì** - Bloccare tutte le connessioni in ingresso tranne quelle necessarie per i servizi Internet di base, ad esempio DHCP, Bonjour e IPSec. Questa impostazione consente di bloccare tutti i servizi di condivisione.

  - **Abilita la modalità mascheramento**

    - **Non configurato** (*impostazione predefinita*)
    - **Sì** - Impedire che il computer risponde alle richieste di probe. Il computer risponde comunque alle richieste in ingresso provenienti da app autorizzate.

  - **App firewall** espandere l'elenco a discesa e quindi selezionare **Aggiungi** per specificare le app e le regole per le connessioni in ingresso per l'app.
    - **Consenti connessioni in ingresso**
      - Non configurato
      - Blocca
      - Consenti

    - **ID aggregazione** - L'ID identifica l'app. Ad esempio: *com.apple.app*

## <a name="microsoft-defender-firewall-profile"></a>Profilo Microsoft Defender Firewall

### <a name="microsoft-defender-firewall"></a>Microsoft Defender Firewall

Le impostazioni seguenti sono configurate come [Criteri di sicurezza degli endpoint per i firewall Windows 10](../protect/endpoint-security-firewall-policy.md).

- **Disabilita FTP (File Transfer Protocol) con stato**  
  CSP: [MdmStore/Global/DisableStatefulFtp](https://go.microsoft.com/fwlink/?linkid=872536)

  - **Non configurato** (*impostazione predefinita*) - Il firewall usa FTP per esaminare e filtrare le connessioni di rete secondarie. È quindi possibile che le regole del firewall vengono ignorate.
  - **Sì**
  
- **Numero di secondi per cui un'associazione di sicurezza può rimanere inattiva prima di essere eliminata**  
  CSP: [MdmStore/Global/SaIdleTime](https://go.microsoft.com/fwlink/?linkid=872539)

  Specificare un tempo tra 300 e 3600 secondo per impostare per quanto tempo le associazioni di sicurezza vengono mantenute dopo che il traffico di rete non viene più visualizzato.
  
  Se non si specifica nessun valore, il sistema elimina un'associazione di sicurezza dopo che è rimasta inattiva per 300 secondi.
  
- **Codifica chiave già condivisa**  
  CSP: [MdmStore/Global/PresharedKeyEncoding](https://go.microsoft.com/fwlink/?linkid=872541)

  Se la codifica *UTF-8* non è richiesta, le chiavi già condivise gengono inizialmente codificate con UTF-8. Successivamente, gli utenti del dispositivo possono scegliere un altro metodo di codifica.

  - **Non configurato** (*impostazione predefinita*)
  - **Nessuno**
  - **UTF8**

- **Firewall - Esenzioni da Ipsec - Individuazione router adiacenti consentita**  
  CSP: [MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

  - **Non configurato** (*impostazione predefinita*)
  - **Sì** - Firewall - Esenzioni da Ipsec - Individuazione router adiacenti consentita.

- **Firewall - Esenzioni da Ipsec - ICMP consentito**  
  CSP: [MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

  - **Non configurato** (*impostazione predefinita*)
  - **Sì** - Firewall - Esenzioni da Ipsec - ICMP consentito.

- **Firewall - Esenzioni da Ipsec - Individuazione router consentita**  
  CSP: [MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

  - **Non configurato** (*impostazione predefinita*)
  - **Sì** - Firewall - Esenzioni da Ipsec - Individuazione router consentita.

- **Firewall - Esenzioni da Ipsec - DHCP consentito**  
  CSP: [MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

  - **Non configurato** (*impostazione predefinita*)
  - **Sì** - Firewall - Esenzioni da Ipsec - DHCP consentito

- **Verifica dell'elenco di revoche di certificati**  
  CSP: [MdmStore/Global/CRLcheck](https://go.microsoft.com/fwlink/?linkid=872548)

   Specificare come applicare la verifica dell'elenco di revoche di certificati.
  - **Non configurato** (*impostazione predefinita*) - La verifica dell'elenco di revoche di certificati è disabilitata per impostazione predefinita del client.
  - **Nessuno**
  - **Tentativo**
  - **Richiedi**

- **Richiedi ai moduli di impostazione chiavi di ignorare solo le suite di autenticazione non supportate**  
  CSP: [MdmStore/Global/OpportunisticallyMatchAuthSetPerKM](https://go.microsoft.com/fwlink/?linkid=872550)

  - **Non configurato** (*impostazione predefinita*)
  - **Sì** - I moduli di impostazione chiavi ignorano le suite di autenticazione non supportate.

- **Accodamento di pacchetti**  
  CSP: [MdmStore/Global/EnablePacketQueue](https://go.microsoft.com/fwlink/?linkid=872551)

  Consente di specificare come abilitare il ridimensionamento per il software sul lato ricezione per la ricezione di testo crittografato e l'inoltro di testo normale per lo scenario relativo a gateway con tunnel IPsec. In questo modo si mantiene l'ordine dei pacchetti.
  - **Non configurato** (*impostazione predefinita*) - Viene ripristinata l'impostazione predefinita del client per l'accodamento di pacchetti, ovvero disabilitato.
  - **Disabilitato**
  - **Accoda in ingresso**
  - **Accoda in uscita**
  - **Accoda entrambi**

- **Attiva Microsoft Defender Firewall per le reti di dominio**  
  CSP: [EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

  - **Non configurato** (*impostazione predefinita*) - Il client ritorna all'impostazione predefinita, ovvero all'abilitazione del firewall.
  - **Sì** - Microsoft Defender Firewall per il tipo di rete di **dominio** è attivato e applicato.
  - **No** - Disabilita il firewall.

- **Attiva Microsoft Defender Firewall per le reti private**  
  CSP: [EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

  - **Non configurato** (*impostazione predefinita*) - Il client ritorna all'impostazione predefinita, ovvero all'abilitazione del firewall.
  - **Sì** - Microsoft Defender Firewall per il tipo di rete **privata** è attivato e applicato.
  - **No** - Disabilita il firewall.

- **Attiva Microsoft Defender Firewall per le reti pubbliche**  
  CSP: [EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

  - **Non configurato** (*impostazione predefinita*) - Il client ritorna all'impostazione predefinita, ovvero all'abilitazione del firewall.
  - **Sì** - Microsoft Defender Firewall per il tipo di rete **pubblica** è attivato e applicato.
  - **No** - Disabilita il firewall.

<!-- Microsoft Defender Firewall rules added in 2005  -->

### <a name="microsoft-defender-firewall-rules"></a>Regole di Microsoft Defender Firewall

*Questo profilo è in Anteprima*.

Le impostazioni seguenti sono configurate come [Criteri di sicurezza degli endpoint per i firewall Windows 10](../protect/endpoint-security-firewall-policy.md).

#### <a name="windows-firewall-rule"></a>Regola di Windows Firewall

- **Nome**  
  Specificare un nome descrittivo per la regola. Questo nome verrà visualizzato nell'elenco di regole per facilitarne l'identificazione.

- **Descrizione**  
  Fornire una descrizione della regola.

- **Direzione**  
  - **Non configurato** (*impostazione predefinita*) - Questa regola viene impostata sul traffico in uscita per impostazione predefinita.
  - **Out** - Questa regola viene applicata al traffico in uscita.
  - **In** - Questa regola viene applicata al traffico in ingresso.

- **Azione**  
  - **Non configurato** (*Impostazione predefinita*) - La regola consente il traffico per impostazione predefinita.
  - **Bloccato** - Il traffico viene bloccato nella*Direzione* configurata.
  - **Bloccato** - Il traffico viene bloccato nella*Direzione* configurata.

- **Tipo di rete**  
  Specifica il tipo di rete a cui appartiene la regola. È possibile scegliere una o più delle seguenti opzioni. Se non si seleziona un'opzione, la regola viene applicata a tutti i tipi di rete.
  - **Dominio**
  - **Privata**
  - **Pubblica**
  - **Non configurato**

- **Nome famiglia pacchetto**  
  [Get-AppxPackage](https://docs.microsoft.com/previous-versions//hh856044(v=technet.10))

  I nomi della famiglia di pacchetti possono essere recuperati mediante l'esecuzione del comando Get-AppxPackage da PowerShell.

- **Percorso file**  
  CSP: [FirewallRules/FirewallRuleName/App/FilePath](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#filepath)

  Per specificare il percorso del file di un'app, immettere il percorso delle app nel dispositivo client. Ad esempio: `C:\Windows\System\Notepad.exe` o `%WINDIR%\Notepad.exe`

- **Nome del servizio**  
  [FirewallRules/FirewallRuleName/App/ServiceName](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#servicename)

  Usare un nome breve per un servizio Windows quando un servizio, non un'applicazione, sta inviando o ricevendo traffico. I nomi brevi del servizio vengono recuperati eseguendo il comando `Get-Service` da PowerShell.

- **Protocollo**  
  CSP: [FirewallRules/FirewallRuleName/Protocol](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#protocol)

  Selezionare il protocollo per questa regola per le porte.
  - I protocolli TLS, *TCP(6)* e *UDP(17)* , consentono di specificare porte o intervalli di porte.
  - Per i protocolli personalizzati immettere un numero compreso tra *0* e *255* che rappresenta il protocollo IP.
  - Se non viene specificato alcun valore, l'impostazione predefinita è **Qualsiasi**.

- **Tipi di interfaccia**  
  Specifica i tipi di interfaccia a cui appartiene la regola. È possibile scegliere una o più delle seguenti opzioni. Se non si seleziona un'opzione, la regola viene applicata a tutti i tipi di interfaccia:
  - **Accesso remoto**
  - **Wireless**
  - **Rete locale**
  - **Non configurato**

- **Utenti autorizzati**  
  [FirewallRules/FirewallRuleName/LocalUserAuthorizationList](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#localuserauthorizedlist)

  Specificare un elenco di utenti locali autorizzati per questa regola. Non è possibile specificare un elenco di utenti autorizzati se il *Nome del servizio* in questo criterio è impostato come un servizio Windows. Se non viene specificato alcun utente autorizzato, il valore predefinito è *tutti gli utenti*.

- **Qualsiasi indirizzo locale**  
  **Non configurato** (*impostazione predefinita*) - Usare l'impostazione seguente *Intervalli di indirizzi locali** per configurare un intervallo di indirizzi da supportare.
  - **Sì** - Supporta qualsiasi indirizzo locale e non configura un intervallo di indirizzi.

- **Intervalli di indirizzi locali**  
  CSP: [FirewallRules/FirewallRuleName/LocalAddressRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#localaddressranges)  

  Aggiunge uno o più indirizzi come un elenco delimitato da virgole di indirizzi locali coperti dalla regola. Le voci valide (token) includono le opzioni seguenti:
  - **Un asterisco**- Un asterisco (\*) indica qualsiasi indirizzo locale. Se presente, l'asterisco deve essere l'unico incluso nel token.
  - **Una subnet** - Specificare una subnet usando la notazione con subnet mask o prefisso di rete. Se non si specifica una subnet mask o un prefisso di rete, viene usata la subnet mask predefinita 255.255.255.255.
  - **Un indirizzo IPv6 valido**
  - **Un intervallo di indirizzi IPv4** - Gli intervalli IPv4 devono essere nel formato *indirizzo iniziale-indirizzo finale* senza spazi inclusi, dove l'indirizzo iniziale è inferiore all'indirizzo finale.
  - **Un intervallo di indirizzi IPv6** - Gli intervalli IPv6 devono essere nel formato *indirizzo iniziale-indirizzo finale* senza spazi inclusi, dove l'indirizzo iniziale è inferiore all'indirizzo finale.

  Se non si specifica alcun valore, l'impostazione predefinita di questa impostazione è l'uso di *Qualsiasi indirizzo*.

- **Qualsiasi indirizzo remoto**  
  **Non configurato** (*impostazione predefinita*) - Usare l'impostazione seguente *Intervalli di indirizzi remoti** per configurare un intervallo di indirizzi da supportare.
  - **Sì** - Supporta qualsiasi indirizzo remoto e non configura un intervallo di indirizzi.

- **Intervalli di indirizzi remoti**  
  CSP: [FirewallRules/FirewallRuleName/RemoteAddressRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#remoteaddressranges)  

  Aggiunge uno o più indirizzi come un elenco delimitato da virgole di indirizzi remoti coperti dalla regola. Le voci valide (token) includono le opzioni seguenti e non distinguono tra maiuscole e minuscole:
  - **Un asterisco**- Un asterisco (\*) indica qualsiasi indirizzo remoto. Se presente, l'asterisco deve essere l'unico incluso nel token.
  - **Defaultgateway**
  - **DHCP**
  - **DNS**
  - **WINS**
  - **Intranet** - Supportato sui dispositivi che eseguono Windows 1809 o versione successiva.
  - **RmtIntranet** - Supportato sui dispositivi che eseguono Windows 1809 o versione successiva.
  - **Ply2Renders** - Supportato sui dispositivi che eseguono Windows 1809 o versione successiva.
  - **LocalSubnet** - Indica qualsiasi indirizzo locale nella subnet locale.
  - **Una subnet** - Specificare una subnet usando la notazione con subnet mask o prefisso di rete. Se non si specifica una subnet mask o un prefisso di rete, viene usata la subnet mask predefinita 255.255.255.255.
  - **Un indirizzo IPv6 valido**
  - **Un intervallo di indirizzi IPv4** - Gli intervalli IPv4 devono essere nel formato *indirizzo iniziale-indirizzo finale* senza spazi inclusi, dove l'indirizzo iniziale è inferiore all'indirizzo finale.
  - **Un intervallo di indirizzi IPv6** - Gli intervalli IPv6 devono essere nel formato *indirizzo iniziale-indirizzo finale* senza spazi inclusi, dove l'indirizzo iniziale è inferiore all'indirizzo finale.

  Se non si specifica alcun valore, l'impostazione predefinita di questa impostazione è l'uso di *Qualsiasi indirizzo*.

<!-- End of 2005 additions  -->

## <a name="next-steps"></a>Passaggi successivi

[Criteri di sicurezza degli endpoint per firewall](../protect/endpoint-security-firewall-policy.md)
