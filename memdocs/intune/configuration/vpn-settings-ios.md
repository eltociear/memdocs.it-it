---
title: Configurare impostazioni VPN per dispositivi iOS/iPadOS in Microsoft Intune - Azure | Microsoft Docs
description: Aggiungere o creare un profilo di configurazione VPN nei dispositivi iOS/iPadOS usando le impostazioni di configurazione della rete privata virtuale (VPN). Configurare i dettagli della connessione, i metodi di autenticazione, lo split tunneling e le impostazioni VPN personalizzate con l'identificatore, le coppie chiave-valore, le impostazioni VPN per app che includono gli URL Safari e le VPN su richiesta con SSID o domini di ricerca DNS, nonché le impostazioni del proxy in modo che includa uno script di configurazione, un indirizzo IP o FQDN e una porta TCP in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/17/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c8aeab9ba7f6b6abd42793bf2af9452b4482edf4
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/26/2020
ms.locfileid: "88911829"
---
# <a name="add-vpn-settings-on-ios-and-ipados-devices-in-microsoft-intune"></a>Aggiungere impostazioni VPN in dispositivi iOS e iPadOS in Microsoft Intune

Microsoft Intune include molte impostazioni VPN che possono essere distribuite nei dispositivi iOS/iPadOS. Queste impostazioni vengono usate per creare e configurare le connessioni VPN nella rete dell'organizzazione. Questo articolo descrive queste impostazioni. Alcune impostazioni sono disponibili solo per alcuni client VPN, ad esempio Citrix, Zscaler e altri.

## <a name="before-you-begin"></a>Prima di iniziare

[Creare un profilo di configurazione del dispositivo](vpn-settings-configure.md).

> [!NOTE]
> Queste impostazioni sono disponibili per tutti i tipi di registrazione ad eccezione della registrazione utenti. La registrazione utenti può essere usata solo con [VPN per singole app](./vpn-setting-configure-per-app.md). Per altre informazioni sui tipi di registrazione, vedere [Registrazione iOS/iPadOS](../enrollment/ios-enroll.md).

## <a name="connection-type"></a>Tipo di connessione

Selezionare il tipo di connessione VPN dall'elenco di fornitori seguente:

- **Check Point Capsule VPN**
- **Cisco Legacy AnyConnect**: applicabile all'app [Cisco Legacy AnyConnect](https://itunes.apple.com/app/cisco-legacy-anyconnect/id392790924) 4.0.5x e versioni precedenti.
- **Cisco AnyConnect**: applicabile all'app [Cisco Legacy AnyConnect](https://itunes.apple.com/app/cisco-anyconnect/id1135064690) 4.0.7x e versioni successive.
- **SonicWall Mobile Connect**
- **F5 Access Legacy**: applicabile all'app F5 Access 2.1 e versioni precedenti.
- **F5 Access**: applicabile all'app F5 Access 3.0 e versioni successive.
- **Palo Alto Networks GlobalProtect (legacy)** : applicabile all'app Palo Alto Networks GlobalProtect 4.1 e versioni precedenti.
- **Palo Alto Networks GlobalProtect**: applicabile all'app Palo Alto Networks GlobalProtect 5.0 e versioni successive.
- **Pulse Secure**
- **Cisco (IPSec)**
- **VPN Citrix**
- **Citrix SSO**
- **Zscaler**: per usare l'accesso condizionale oppure consentire agli utenti di ignorare la schermata di accesso di Zscaler, è necessario integrare Zscaler Private Access (ZPA) con il proprio account Azure AD. Per informazioni dettagliate, vedere la [documentazione di Zscaler](https://help.zscaler.com/zpa/configuration-guide-microsoft-azure-ad).
- **NetMotion Mobility**
- **IKEv2**: le proprietà sono descritte in [Impostazioni IKEv2](#ikev2-settings) (in questo articolo).
- **VPN personalizzata**

> [!NOTE]
> Cisco, Citrix, F5 e Palo Alto hanno annunciato che i client legacy non funzionano in iOS 12. È necessario eseguire la migrazione alle nuove app appena possibile. Per altre informazioni, vedere il [blog del team di supporto di Microsoft Intune](https://go.microsoft.com/fwlink/?linkid=2013806&clcid=0x409).

## <a name="base-vpn-settings"></a>Impostazioni VPN di base

Le impostazioni visualizzate nell'elenco seguente sono determinate dal tipo di connessione VPN scelto.  

- **Nome della connessione**: Questo nome viene visualizzato dagli utenti finali quando cercano l'elenco delle connessioni VPN disponibili nel dispositivo.
- **Nome dominio personalizzato** (solo Zscaler): precompilare il campo di accesso dell'app Zscaler con il dominio a cui appartengono i propri utenti. Ad esempio, se un nome utente è `Joe@contoso.net`, il dominio `contoso.net` viene visualizzato nel campo in modo statico quando si apre l'app. Se non si specifica un nome di dominio, verrà usata la parte del dominio del nome dell'entità utente in Azure Active Directory.
- **Indirizzo IP o FQDN**: immettere l'indirizzo IP o il nome di dominio completo (FQDN) del server VPN a cui si connetteranno i dispositivi. Ad esempio, immettere `192.168.1.1` o `vpn.contoso.com`.
- **Nome cloud dell'organizzazione** (solo Zscaler): Immettere il nome del cloud in cui viene effettuato il provisioning dell'organizzazione. Il nome è presente nell'URL usato per accedere a Zscaler.  
- **Metodo di autenticazione**: scegliere il metodo di autenticazione dei dispositivi al server VPN. 
  - **Certificati**: in **Certificato di autenticazione** selezionare un profilo di certificato SCEP o PKCS esistente per autenticare la connessione. In [Configurare i certificati](../protect/certificates-configure.md) sono disponibili alcune indicazioni sui profili di certificato.
  - **Nome utente e password**: gli utenti finali devono immettere un nome utente e una password per accedere al server VPN.  

    > [!NOTE]
    > Se nome utente e password vengono usati come metodo di autenticazione per la VPN IPSec Cisco, devono fornire SharedSecret tramite un profilo personalizzato di Apple Configurator.

  - **Credenziale derivata**: usare un certificato derivato dalla smart card di un utente. Se non è configurata alcuna autorità emittente delle credenziali derivate, Intune richiede di aggiungerne una. Per altre informazioni, vedere [Usare le credenziali derivate in Microsoft Intune](../protect/derived-credentials.md).

- **URL esclusi** (solo Zscaler): quando si è connessi alla rete VPN di Zscaler, gli URL elencati sono accessibili dall'esterno del cloud di Zscaler. 

- **Split tunneling**: scegliere **Abilita** o **Disabilita** per consentire ai dispositivi di scegliere la connessione da usare in base al traffico. Ad esempio, un utente in un hotel userà la connessione VPN per accedere ai file di lavoro, ma userà la rete standard dell'hotel per la normale esplorazione sul Web.

- **Identificatore VPN** (VPN personalizzata, Zscaler e Citrix): identificatore per l'app VPN in uso, fornito dal provider VPN.
- **Immettere le coppie chiave/valore per gli attributi della VPN personalizzata dell'organizzazione** (VPN personalizzata, Zscaler e Citrix): Aggiungere o importare **chiavi** e **valori** per la personalizzazione della connessione VPN. Anche questi valori vengono in genere specificati dal provider VPN.

- **Abilita il controllo accesso alla rete** (Cisco AnyConnect, Citrix SSO, F5 Access): quando si sceglie **Accetto**, l'ID dispositivo viene incluso nel profilo VPN. Questo ID può essere usato per l'autenticazione della rete VPN per consentire o impedire l'accesso alla rete.

  **Quando si usa Cisco AnyConnect con ISE**, assicurarsi di:

  - Se non è già stato fatto, integrare ISE con Intune per NAC come descritto in **Configurare Microsoft Intune come server MDM** in [Cisco Identity Services Engine Administrator Guide](https://www.cisco.com/c/en/us/td/docs/security/ise/2-1/admin_guide/b_ise_admin_guide_21/b_ise_admin_guide_20_chapter_01000.html).
  - Abilitare il controllo accesso alla rete nel profilo VPN.

  **Quando si usa Citrix SSO con Gateway**, assicurarsi di:

  - Verificare che sia in uso Citrix Gateway 12.0.59 o versione successiva.
  - Verificare che gli utenti abbiano Citrix SSO 1.1.6 o versione successiva installato nei dispositivi.
  - Integrare Citrix Gateway con Intune per NAC. Vedere la guida alla distribuzione di Citrix [Integrating Microsoft Intune/Enterprise Mobility Suite with NetScaler (LDAP+OTP Scenario)](https://www.citrix.com/content/dam/citrix/en_us/documents/guide/integrating-microsoft-intune-enterprise-mobility-suite-with-netscaler.pdf) (Integrazione di Microsoft Intune/Enterprise Mobility Suite con NetScaler - scenario LDAP+OTP).
  - Abilitare il controllo accesso alla rete nel profilo VPN.

  **Quando si usa F5 Access**, assicurarsi di:

  - Verificare che sia in uso F5 BIG-IP 13.1.1.5 o versione successiva. 
  - Integrare BIG-IP con Intune per il controllo di accesso alla rete. Vedere la guida di F5 [Overview: Configuring APM for device posture checks with endpoint management systems](https://support.f5.com/kb/en-us/products/big-ip_apm/manuals/product/apm-client-configuration-7-1-6/6.html#guid-0bd12e12-8107-40ec-979d-c44779a8cc89) (Panoramica: configurazione di APM per i controlli del comportamento dei dispositivi con sistemi di gestione endpoint).
  - Abilitare il controllo accesso alla rete nel profilo VPN.

  Per i partner VPN che supportano l'ID dispositivo, il client VPN, ad esempio Citrix SSO, può ottenere l'ID. Quindi, può inviare una query a Intune per verificare se il dispositivo è registrato e se il profilo VPN è conforme o meno.

  - Per rimuovere questa informazione, creare nuovamente il profilo e non selezionare **Accetto**. Riassegnare quindi il profilo.

### <a name="ikev2-settings"></a>Impostazioni IKEv2

Queste impostazioni si applicano quando si sceglie **Tipo di connessione** > **IKEv2**.

- **Always-on VPN** (VPN sempre attiva): scegliere **Abilita** per impostare un client VPN in modo che si connetta e riconnetta automaticamente alla VPN. Le connessioni VPN sempre attive rimangono connesse o si connettono immediatamente quando l'utente blocca il dispositivo, il dispositivo viene riavviato o la rete wireless viene modificata. Se l'opzione è impostata su **Disabilita** (impostazione predefinita), la VPN sempre attiva per tutti i client VPN è disabilitata. Se abilitata, configurare anche:

  - **Interfaccia di rete**: tutte le impostazioni di IKEv2 sono valide solo per l'interfaccia di rete scelta. Le opzioni disponibili sono:
    - **Wi-Fi e rete dati** (impostazione predefinita): le impostazioni di IKEv2 si applicano alle interfacce Wi-Fi e cellulari del dispositivo.
    - **Rete cellulare**: le impostazioni di IKEv2 si applicano solo all'interfaccia di rete cellulare del dispositivo. Selezionare questa opzione se si esegue la distribuzione nei dispositivi con l'interfaccia Wi-Fi disabilitata o rimossa.
    - **Wi-Fi**: Le impostazioni di IKEv2 si applicano solo all'interfaccia Wi-Fi del dispositivo.
  - **Disabilitazione della configurazione VPN da parte dell'utente**: **Abilita** consente agli utenti di disattivare la VPN sempre attiva. **Disabilita** (impostazione predefinita) impedisce agli utenti di disattivarla. Il valore predefinito di tale impostazione è l'opzione più sicura.
  - **Segreteria telefonica**: consente di scegliere come gestire il traffico della segreteria telefonica quando la VPN sempre attiva è abilitata. Le opzioni disponibili sono:
    - **Imponi il traffico di rete attraverso la VPN** (impostazione predefinita): si tratta dell'impostazione con il livello di sicurezza più alto.
    - **Consenti il passaggio del traffico di rete all'esterno della VPN**
    - **Rilascia il traffico di rete**
  - **AirPrint**: consente di scegliere come gestire il traffico di AirPrint quando la VPN sempre attiva è abilitata. Le opzioni disponibili sono:
    - **Imponi il traffico di rete attraverso la VPN** (impostazione predefinita): si tratta dell'impostazione con il livello di sicurezza più alto.
    - **Consenti il passaggio del traffico di rete all'esterno della VPN**
    - **Rilascia il traffico di rete**
  - **Servizi per rete dati**: in iOS 13.0 e versioni successive consente di scegliere come gestire il traffico dati della rete cellulare quando la VPN sempre attiva è abilitata. Le opzioni disponibili sono:
    - **Imponi il traffico di rete attraverso la VPN** (impostazione predefinita): si tratta dell'impostazione con il livello di sicurezza più alto.
    - **Consenti il passaggio del traffico di rete all'esterno della VPN**
    - **Rilascia il traffico di rete**
  - **Consenti il passaggio del traffico da app di rete non native di tipo Captive all'esterno della VPN**: una rete captive fa riferimento a hotspot Wi-Fi in genere disponibili in ristoranti e hotel. Le opzioni disponibili sono:
    - **No**: forza tutto il traffico delle app della rete captive nel tunnel della VPN.
    - **Sì, tutte le app**: consente a tutto il traffico delle app della rete captive di ignorare la VPN.
    - **Sì, app specifiche**: **aggiunge** un elenco di app della rete captive il cui traffico può ignorare la VPN. Immettere gli identificatori del bundle dell'app della rete captive. Immettere ad esempio `com.contoso.app.id.package`.

  - **Passaggio del traffico di app di tipo Captive WebSheet all'esterno della VPN**: Captive WebSheet è un Web browser incorporato che gestisce l'accesso captive. **Abilita** consente al traffico dell'app browser di ignorare la VPN. **Disabilita** (impostazione predefinita) impone al traffico WebSheet di usare la VPN sempre attiva. Il valore predefinito è l'opzione più sicura.
  - **Intervallo keep-alive (secondi) per NAT (Network Address Translation)** : per rimanere connesso alla VPN, il dispositivo invia i pacchetti di rete per rimanere attivo. Immettere un valore in secondi per la frequenza di invio dei pacchetti, da 20 a 1440. Ad esempio, immettere il valore `60` per inviare i pacchetti di rete alla VPN ogni 60 secondi. Per impostazione predefinita, questo valore è configurato su `110` secondi.
  - **Esegui l'offload di keep-alive per NAT nell'hardware quando il dispositivo è in modalità sospensione**: quando un dispositivo è in stato di sospensione, **Abilita** (impostazione predefinita) fa sì che il protocollo NAT invii continuamente pacchetti keep-alive, in modo che il dispositivo rimanga connesso alla VPN. L'opzione **Disabilita** disattiva questa funzionalità.

- **Identificatore remoto**: immettere indirizzo IP di rete, FQDN, UserFQDN o ASN1DN del server IKEv2. Ad esempio, immettere `10.0.0.3` o `vpn.contoso.com`. In genere, viene immesso lo stesso valore di [**Nome della connessione**](#base-vpn-settings) (in questo articolo). Il valore tuttavia varia a seconda delle impostazioni del server IKEv2.

- **Tipo di autenticazione client**: scegliere la modalità di autenticazione del client VPN per la VPN. Le opzioni disponibili sono:
  - **Autenticazione utente** (impostazione predefinita): per l'autenticazione vengono usate le credenziali utente.
  - **Autenticazione del computer**: per l'autenticazione vengono usate le credenziali del dispositivo.

- **Metodo di autenticazione**: scegliere il tipo di credenziali del client da inviare al server. Le opzioni disponibili sono:
  - **Certificati**: usa un profilo certificato esistente per l'autenticazione per la VPN. Verificare che il profilo certificato sia già stato assegnato all'utente o al dispositivo. In caso contrario, la connessione VPN non viene stabilita.
    - **Tipo di certificato**: selezionare il tipo di crittografia usato dal certificato. Verificare che il server VPN sia configurato per accettare questo tipo di certificato. Le opzioni disponibili sono:
      - **RSA** (impostazione predefinita)
      - **ECDSA256**
      - **ECDSA384**
      - **ECDSA521**

  - **Nome utente e password** (solo autenticazione utente): quando gli utenti si connettono alla VPN, vengono richiesti il nome utente e la password.
  - **Segreto condiviso** (solo autenticazione del computer): consente di immettere un segreto condiviso da inviare al server VPN.
    - **Segreto condiviso**: immettere il segreto condiviso, noto anche come chiave precondivisa (PSK). Assicurarsi che il valore corrisponda al segreto condiviso configurato nel server VPN.

- **Nome comune dell'emittente del certificato del server**: consente al server VPN di eseguire l'autenticazione per il client VPN. Immettere il nome comune dell'autorità emittente del certificato del server VPN inviato al client VPN nel dispositivo. Verificare che il valore del nome comune corrisponda alla configurazione nel server VPN. In caso contrario, la connessione VPN non viene stabilita.
- **Nome comune del certificato del server**: immettere il nome comune (CN) per il certificato stesso. Se viene lasciato vuoto, viene usato il valore dell'identificatore remoto.

- **Frequenza di rilevamento di peer inattivi**: scegliere la frequenza con cui il client VPN controlla se il tunnel VPN è attivo. Le opzioni disponibili sono:
  - **Non configurata**: usa l'impostazione predefinita del sistema iOS/iPadOS che può corrispondere a **Media**.
  - **Nessuno**: disabilita il rilevamento dei peer inattivi.
  - **Bassa**: invia un messaggio keep-alive ogni 30 minuti.
  - **Media** (predefinita): invia un messaggio keep-alive ogni 10 minuti.
  - **Alta**: invia un messaggio keep-alive ogni 60 secondi.

- **Intervallo di versioni TLS - Minimo**: immettere la versione minima di TLS da usare. Immettere `1.0`, `1.1` o `1.2`. Se viene lasciato vuoto, viene usato il valore predefinito `1.0`.
- **Intervallo di versioni TLS - Massimo**: immettere la versione massima di TLS da usare. Immettere `1.0`, `1.1` o `1.2`. Se viene lasciato vuoto, viene usato il valore predefinito `1.2`.

> [!NOTE]
> Quando vengono usati l'autenticazione utente e i certificati, è necessario impostare l'intervallo di versioni TLS minimo e massimo.

- **PFS (Perfect Forward Secrecy)** : selezionare **Abilita** per attivare PFS (Perfect Forward Secrecy). PFS è una funzionalità di sicurezza IP che riduce l'impatto nel caso in cui una chiave di sessione venga compromessa. **Disabilita** (impostazione predefinita) non usa PFS.
- **Verifica della revoca del certificato**: selezionare **Abilita** per assicurarsi che i certificati non vengano revocati prima di consentire la connessione VPN. Questo controllo costituisce la procedura di massima efficacia. Se si verifica il timeout del server VPN prima di determinare se il certificato è stato revocato, viene concesso l'accesso. **Disabilita** (impostazione predefinita) non controlla la presenza di certificati revocati.

- **Configurare i parametri delle associazioni di sicurezza**: **Non configurata** (impostazione predefinita) usa l'impostazione predefinita del sistema iOS/iPadOS. Selezionare **Abilita** per immettere i parametri usati durante la creazione delle associazioni di sicurezza con il server VPN:
  - **Algoritmo di crittografia**: selezionare l'algoritmo desiderato:
    - DES
    - 3DES
    - AES-128
    - AES-256 (impostazione predefinita)
    - AES-128-GCM
    - AES-256-GCM
  - **Algoritmo di integrità**:  selezionare l'algoritmo desiderato:
    - SHA1-96
    - SHA1-160
    - SHA2-256 (impostazione predefinita)
    - SHA2-384
    - SHA2-512
  - **Gruppo Diffie-Hellman**: selezionare il gruppo desiderato. Il valore predefinito è `2`.
  - **Durata** (minuti): scegliere per quanto tempo l'associazione di sicurezza rimane attiva fino a quando le chiavi non vengono ruotate. Immettere un valore intero compreso tra `10` e `1440` (1440 minuti corrisponde a 24 ore). Il valore predefinito è `1440`.

- **Configurare un set di parametri separato per le associazioni di sicurezza figlio**: iOS/iPadOS consente di configurare parametri distinti per la connessione IKE ed eventuali connessioni figlio. 

  **Non configurato** (impostazione predefinita) usa i valori immessi nell'impostazione precedente **Configurare i parametri delle associazioni di sicurezza**. Selezionare **Abilita** per immettere i parametri usati durante la creazione delle associazioni di sicurezza *figlio* con il server VPN:
  - **Algoritmo di crittografia**: selezionare l'algoritmo desiderato:
    - DES
    - 3DES
    - AES-128
    - AES-256 (impostazione predefinita)
    - AES-128-GCM
    - AES-256-GCM
  - **Algoritmo di integrità**:  selezionare l'algoritmo desiderato:
    - SHA1-96
    - SHA1-160
    - SHA2-256 (impostazione predefinita)
    - SHA2-384
    - SHA2-512
  - **Gruppo Diffie-Hellman**: selezionare il gruppo desiderato. Il valore predefinito è `2`.
  - **Durata** (minuti): scegliere per quanto tempo l'associazione di sicurezza rimane attiva fino a quando le chiavi non vengono ruotate. Immettere un valore intero compreso tra `10` e `1440` (1440 minuti corrisponde a 24 ore). Il valore predefinito è `1440`.

## <a name="automatic-vpn-settings"></a>Impostazioni VPN automatico

- **VPN per singole app**: abilita la VPN per singole app. Consente l'attivazione automatica della connessione VPN all'apertura di alcune app. È anche possibile associare le app a questo profilo VPN. La VPN per app non è supportata in IKEv2. Per altre informazioni, vedere le [istruzioni per configurare la VPN per app per iOS/iPadOS](vpn-setting-configure-per-app.md). 
  - **Tipo di provider**: disponibile solo per Pulse Secure e VPN personalizzata.
  - Quando si usano i profili **VPN per app** iOS/iPadOS con Pulse Secure o una VPN personalizzata, scegliere il tunneling a livello di app (proxy delle app) o il tunneling a livello di pacchetto (tunnel di pacchetti). Impostare il valore **ProviderType** su **app-proxy** per il tunneling di livello app e su **packet-tunnel** per il tunneling di livello pacchetto. Se non si conosce il valore da usare, vedere la documentazione del provider VPN.
  - **URL Safari che attiveranno questa connessione VPN**: aggiungere uno o più URL di sito Web. Quando questi URL vengono visitati con il browser Safari nel dispositivo, viene stabilita automaticamente la connessione alla VPN.

- **VPN su richiesta**: configurare le regole condizionali che controllano l'avvio della connessione VPN. Ad esempio, creare una condizione per cui la connessione VPN viene usata solo quando un dispositivo non è connesso a una rete Wi-Fi aziendale. In alternativa, creare una nuova condizione. Ad esempio, se un dispositivo non può accedere a un dominio di ricerca DNS specificato, la connessione VPN non viene avviata.

  - **SSID o domini di ricerca DNS**: selezionare se la condizione usa o meno **SSID** della rete wireless o **Domini di ricerca DNS**. Scegliere **Aggiungi** per configurare uno o più SSID o domini di ricerca.
  - **Probe della stringa dell'URL**: Facoltativo. Immettere un URL che viene usato dalla regola come test. Se il dispositivo accede all'URL senza reindirizzamento, la connessione VPN viene avviata. Il dispositivo si connette quindi all'URL di destinazione. L'utente non visualizza il sito del probe della stringa dell'URL.

    Ad esempio, un probe della stringa dell'URL è l'URL di un server Web di controllo che verifica la conformità del dispositivo prima della connessione VPN. In alternativa, l'URL verifica la capacità della VPN di connettersi a un sito prima che il dispositivo si connetta all'URL di destinazione tramite la VPN.

  - **Azione del dominio**: scegliere una delle opzioni seguenti:
    - Connetti se necessario
    - Non connettere mai
  - **Azione**: scegliere una delle opzioni seguenti:
    - Connessione
    - Valuta la connessione
    - Ignora
    - Disconnetti

## <a name="proxy-settings"></a>Impostazioni proxy

Se si usa un proxy, configurare le impostazioni seguenti. Le impostazioni del proxy non sono disponibili per le connessioni VPN Zscaler.  

- **Script di configurazione automatica**: consente di usare un file per configurare il server proxy. Immettere l'**URL server proxy**, ad esempio `http://proxy.contoso.com`, contenente il file di configurazione.
- **Indirizzo**: immettere l'indirizzo IP del nome host completo del server proxy.
- **Numero porta**: immettere il numero di porta associato al server proxy.

## <a name="next-steps"></a>Passaggi successivi

Il profilo è stato creato, ma non è ancora operativo. [Assegnare il profilo](device-profile-assign.md) e [monitorarne lo stato](device-profile-monitor.md).

Configurare le impostazioni VPN nei dispositivi [Android](vpn-settings-android.md), [Android Enterprise](vpn-settings-android-enterprise.md), [macOS](vpn-settings-macos.md) e [Windows 10](vpn-settings-windows-10.md).