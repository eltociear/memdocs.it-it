---
title: Sicurezza e privacy per l'amministrazione dei siti
titleSuffix: Configuration Manager
description: Ottimizzare protezione e privacy per l'amministrazione del sito in Configuration Manager
ms.date: 04/27/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1d58176e-abc0-4087-8583-ce70deb4dcf5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 923018e35fae1ec1f5e9c0869ef22d43b5de552b
ms.sourcegitcommit: 53bab52e42de28b87e53596646a3532e25eb9c14
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/28/2020
ms.locfileid: "82182260"
---
# <a name="security-and-privacy-for-site-administration-in-configuration-manager"></a>Protezione e privacy per l'amministrazione del sito in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Questo articolo contiene informazioni sulla privacy per i siti e la gerarchia di Configuration Manager.

## <a name="security-guidance-for-site-administration"></a><a name="BKMK_Security_Sites"></a> Indicazioni sulla sicurezza per l'amministrazione del sito

Usare le seguenti indicazioni per proteggere i siti e la gerarchia di Configuration Manager.  

### <a name="run-setup-from-a-trusted-source-and-secure-communication"></a>Eseguire l'installazione da un'origine attendibile e proteggere le comunicazioni

Per impedire la manomissione dei file di origine, eseguire l'installazione di Configuration Manager da un'origine attendibile. Se si archiviano i file in rete, proteggere il percorso di rete.  

Se si esegue l'installazione da un percorso di rete, per evitare che un utente malintenzionato manometta i file mentre vengono trasmessi in rete, utilizzare la firma IPsec o SMB tra il percorso di origine dei file di installazione e il server del sito.  

Se si usa il downloader di installazione per scaricare i file necessari richiesti dall'installazione, assicurarsi di proteggere il percorso in cui tali file vengono memorizzati. Proteggere anche il canale di comunicazione per questo percorso quando si esegue l'installazione.  

### <a name="extend-the-active-directory-schema-and-publish-sites-to-the-domain"></a>Estendere lo schema di Active Directory e pubblicare i siti nel dominio  

Le estensioni dello schema non sono necessarie per eseguire Configuration Manager, ma creano un ambiente più sicuro. I client e i server del sito possono recuperare le informazioni da un'origine attendibile.  

Se i client si trovano in un dominio non attendibile, distribuire i ruoli del sistema del sito seguenti nei domini dei client:  

- Punto di gestione  

- Punto di distribuzione  

> [!NOTE]  
> Un dominio trusted per Configuration Manager richiede l'autenticazione Kerberos. Se i client si trovano in un'altra foresta che non dispone di un trust tra foreste bidirezionale con la foresta del server del sito, i client vengono considerati in un dominio non attendibile. Un trust esterno non è sufficiente a questo scopo.  

### <a name="use-ipsec-to-secure-communications"></a>Usare IPsec per proteggere le comunicazioni

Anche se Configuration Manager protegge le comunicazioni tra il server del sito e il computer in cui è in esecuzione SQL Server, Configuration Manager non protegge le comunicazioni tra i ruoli del sistema del sito e SQL Server. È possibile configurare solo alcuni sistemi del sito con HTTPS per la comunicazione tra siti.  

Se non si usano controlli aggiuntivi per proteggere questi canali da server a server, gli utenti malintenzionati potrebbero utilizzare diversi attacchi di spoofing e man-in-the-middle contro i sistemi del sito. Usare la firma SMB quando non è possibile usare IPsec.  

> [!Important]  
> Proteggere il canale di comunicazione tra il server del sito e il server di origine del pacchetto. Questa comunicazione utilizza SMB. Se non è possibile usare IPsec per proteggere questa comunicazione, usare la firma SMB per assicurarsi che i file non vengano manomessi prima che i client li scarichino e li eseguano.  

### <a name="dont-change-the-default-security-groups"></a>Non modificare i gruppi di sicurezza predefiniti

Non modificare i seguenti gruppi di sicurezza che Configuration Manager crea e gestisce per la comunicazione del sistema del sito:

- **SMS_SiteSystemToSiteServerConnection_MP_&lt;Codicesito\>**  

- **SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;Codicesito\>**  

- **SMS_SiteSystemToSiteServerConnection_Stat_&lt;Codicesito\>**  

Configuration Manager crea e gestisce automaticamente questi gruppi di sicurezza. Questo comportamento include la rimozione degli account computer quando viene rimosso un ruolo del sistema del sito.  

Per garantire la continuità del servizio e dei privilegi minimi, non modificare manualmente questi gruppi.  

### <a name="manage-the-trusted-root-key-provisioning-process"></a>Gestire il processo di provisioning della chiave radice attendibile

Se i client non possono eseguire la query al server di catalogo globale per ottenere informazioni su Configuration Manager, devono basarsi sulla chiave radice attendibile per autenticare i punti di gestione validi. La chiave radice attendibile viene archiviata nel registro di sistema del client. Può essere impostata usando i criteri di gruppo o la configurazione manuale.  

Se il client non ha una copia della chiave radice attendibile prima di contattare un punto di gestione per la prima volta, si affida al primo punto di gestione con cui comunica. Per ridurre il rischio di un errato indirizzamento dei client a un punto di gestione non autorizzato da parte di un utente malintenzionato, è possibile eseguire il pre-provisioning dei client utilizzando la chiave radice attendibile. Per altre informazioni, vedere [Pianificare la chiave radice attendibile](../security/plan-for-security.md#BKMK_PlanningForRTK).  

### <a name="use-non-default-port-numbers"></a>Usare numeri di porta non predefiniti

L'uso di numeri di porta non predefiniti può aumentare il livello di protezione, poiché diventa più difficile per gli utenti malintenzionati esplorare l'ambiente per preparare un attacco. Se si decide di usare porte non predefinite, pianificarle prima di installare Configuration Manager e usarle in modo coerente in tutti i siti della gerarchia. Le porte di richiesta client e la riattivazione LAN sono esempi in cui è possibile usare numeri di porta non predefiniti.  

### <a name="use-role-separation-on-site-systems"></a>Usare la separazione dei ruoli per i sistemi del sito

Benché si possano installare tutti i ruoli del sistema del sito in un computer singolo, questa operazione viene usata raramente nelle reti di produzione. Crea un singolo punto di guasto.  

### <a name="reduce-the-attack-profile"></a>Ridurre il profilo di attacco

L'isolamento di ogni ruolo del sistema del sito in un server diverso riduce la possibilità che un attacco alle vulnerabilità in un sistema del sito possa essere usato contro un sistema del sito differente. Molti ruoli richiedono l'installazione di Internet Information Services (IIS) nel sistema del sito e questo aumenta la superficie di attacco. Se occorre combinare i ruoli per ridurre il consumo hardware, combinare ruoli IIS solo con altri ruoli che richiedono IIS.  

> [!IMPORTANT]  
> Il ruolo del punto di stato di fallback è un'eccezione. Poiché questo ruolo del sistema del sito accetta dati non autenticati dai client, non assegnare il ruolo del punto di stato di fallback ad altri ruoli del sistema del sito di Configuration Manager.  

### <a name="configure-static-ip-addresses-for-site-systems"></a>Configurare gli indirizzi IP statici per i sistemi del sito

Gli indirizzi IP statici sono più facili da proteggere da attacchi di risoluzione del nome.  

Anche gli indirizzi IP statici semplificano la configurazione di IPsec. L'uso di IPsec è una procedura consigliata per la protezione della comunicazione tra i sistemi dei siti in Configuration Manager.  

### <a name="dont-install-other-applications-on-site-system-servers"></a>Non installare altre applicazioni sui server del sistema del sito

Quando si installano altre applicazioni sui server del sistema del sito, si aumenta la superficie di attacco di Configuration Manager e si rischiano problemi di incompatibilità.  

### <a name="require-signing-and-enable-encryption-as-a-site-option"></a>Richiedere la firma e abilitare la crittografia come opzione del sito

Abilitare le opzioni di firma e crittografia per il sito. Assicurarsi che tutti i client possano supportare l'algoritmo hash SHA-256, quindi abilitare l'opzione **Richiedi SHA-256**.  

### <a name="restrict-and-monitor-administrative-users"></a>Limitare e monitorare gli utenti amministratori

Concedere l'accesso amministrativo a Configuration Manager solo agli utenti considerati attendibili. Quindi concedere loro le autorizzazioni minime usando i ruoli di protezione incorporati oppure personalizzando i ruoli di protezione. Gli utenti amministratori che possono creare, modificare e distribuire il software e le configurazioni possono potenzialmente controllare i dispositivi della gerarchia di Configuration Manager.  

Controllare periodicamente le assegnazioni degli utenti amministratori e il loro livello di autorizzazione per verificare le modifiche necessarie.  

Per altre informazioni, vedere [Configurare un'amministrazione basata su ruoli](../../servers/deploy/configure/configure-role-based-administration.md).  

### <a name="secure-configuration-manager-backups"></a>Proteggere i backup di Configuration Manager

Quando si esegue il backup di Configuration Manager, queste informazioni includono i certificati e altri dati sensibili che potrebbero essere usati da un utente malintenzionato a fini di impersonificazione.  

Utilizzare la firma SMB o IPsec quando si trasferiscono questi dati in rete e proteggere il percorso di backup.  

### <a name="secure-locations-for-exported-objects"></a>Percorsi sicuri per gli oggetti esportati

Quando si esportano o importano oggetti dalla console di Configuration Manager in un percorso di rete, proteggere il percorso stesso e il canale di rete.

Limitare l'accesso alla cartella di rete.  

Per impedire a un utente malintenzionato di manomettere i dati esportati, usare la firma SMB o IPsec tra il percorso di rete e il server del sito. Proteggere inoltre la comunicazione tra il computer che esegue la console di Configuration Manager e il server del sito. Utilizzare IPsec per crittografare i dati sulla rete per impedire la divulgazione di informazioni.  

### <a name="manually-remove-certificates-from-failed-servers"></a>Rimuovere manualmente i certificati dai server in cui si sono verificati errori

Se un sistema del sito non viene disinstallato correttamente o smette di funzionare e non può essere ripristinato, rimuovere manualmente i certificati di Configuration Manager per il server da altri server di Configuration Manager.

Per rimuovere il peer disponibile nell'elenco locale, originariamente stabilito con il sistema del sito e i ruoli del sistema del sito, rimuovere manualmente i certificati di Configuration Manager per il server che ha restituito l'errore nell'archivio certificati **Persone attendibili** su altri server del sistema del sito. Questa azione è importante se si riassegna il server senza riformattarlo.  

Per altre informazioni, vedere [Controlli crittografici per la comunicazione tra server](../security/cryptographic-controls-technical-reference.md#cryptographic-controls-for-server-communication).  

### <a name="dont-configure-internet-based-site-systems-to-bridge-the-perimeter-network"></a>Non configurare i sistemi del sito basati su Internet per effettuare il bridging della rete perimetrale

Non configurare i server del sistema del sito come multihomed in modo che si connettano alla rete perimetrale e alla Intranet. Benché consenta ai sistemi del sito basati su Internet di accettare connessioni client da Internet e dalla intranet, questa configurazione elimina i limiti di protezione tra la rete perimetrale e la intranet.  

### <a name="configure-the-site-server-to-initiate-connections-to-perimeter-networks"></a>Configurare il server del sito per avviare le connessioni alle reti perimetrali

Se un sistema del sito si trova su una rete non attendibile, ad esempio una rete perimetrale, configurare il server del sito per avviare connessioni al sistema del sito.

Per impostazione predefinita, i sistemi del sito avviano connessioni al server del sito per il trasferimento dei dati. Questa configurazione può costituire un rischio per la sicurezza quando si avvia la connessione da una rete non attendibile alla rete attendibile. Se i sistemi del sito accettano connessioni da Internet o risiedono in una foresta non attendibile, configurare l'opzione del sistema del sito su **Richiedi al server del sito di avviare le connessioni al sistema del sito**. Dopo l'installazione del sistema del sito e di tutti i ruoli, tutte le connessioni vengono avviate dal server del sito dalla rete attendibile.  

### <a name="use-ssl-bridging-and-termination-with-authentication"></a>Usare il bridging e la terminazione SSL con l'autenticazione

Se si usa un server proxy Web per la gestione client basata su Internet, usare il bridging SSL a SSL con la terminazione con autenticazione.

Quando si configura la terminazione SSL sul server Web proxy, i pacchetti provenienti da Internet sono soggetti a verifica prima di essere inoltrati alla rete interna. Il server Web proxy autentica la connessione dal client, la termina, quindi apre una nuova connessione autenticata ai sistemi del sito basati su Internet.  

Quando i computer client di Configuration Manager usano un server Web proxy per collegarsi ai sistemi del sito basati su Internet, l'identità client (GUID) viene contenuta in modo protetto all'interno del payload dei pacchetti. In questo modo il punto di gestione non considera il server Web proxy come client.

Se il server Web proxy non è in grado di supportare i requisiti per il bridging SSL, viene supportato anche il tunneling SSL. Questa opzione è meno sicura. I pacchetti SSL provenienti da Internet vengono inoltrati ai sistemi del sito senza terminazione. Non è quindi possibile verificare se sono presenti contenuti dannosi.  

> [!WARNING]  
> I dispositivi mobili che vengono registrati da Configuration Manager non sono in grado di usare il bridging SSL. Devono usare solo il tunneling SSL.  

### <a name="configurations-to-use-if-you-configure-the-site-to-wake-up-computers-to-install-software"></a>Configurazioni da usare se si configura il sito in modo da riattivare i computer per installare il software

- Se si utilizzano i tradizionali pacchetti di riattivazione, usare broadcast unicast anziché broadcast con riferimento a subnet.  

- Se è necessario usare broadcast con riferimento a subnet, configurare i router in modo che consentano broadcast con riferimento a IP provenienti solo dal server del sito e solo su un numero di porta non predefinito.  

Per altre informazioni sulle diverse tecnologie di riattivazione LAN, vedere [Pianificare la riattivazione dei client](../../clients/deploy/plan/plan-wake-up-clients.md).

### <a name="if-you-use-email-notification-configure-authenticated-access-to-the-smtp-mail-server"></a>Se si usa la notifica via posta elettronica, configurare l'accesso autenticato al server di posta SMTP.

Quando possibile, usare un server di posta elettronica che supporti l'accesso autenticato. Usare l'account computer del server del sito per l'autenticazione. Se è necessario specificare un account utente per l'autenticazione, utilizzare un account che disponga dei privilegi minimi. 

### <a name="enforce-ldap-channel-binding-and-ldap-signing"></a>Applicare il binding di canale LDAP e la firma LDAP

È possibile migliorare la sicurezza dei controller di dominio di Active Directory configurando il server per rifiutare i binding LDAP SASL (Simple Authentication and Security Layer) che non richiedono la firma o per rifiutare binding semplici LDAP eseguiti su una connessione con testo non crittografato. A partire dalla versione 1910, Configuration Manager supporta l'applicazione di binding di canale LDAP e della firma LDAP. Per altre informazioni, vedere [Requisito 2020 relativo al binding di canale LDAP e alla firma LDAP per Windows](https://support.microsoft.com/help/4520412/2020-ldap-channel-binding-and-ldap-signing-requirements-for-windows). <!--6244453-->


## <a name="security-guidance-for-the-site-server"></a><a name="BKMK_Security_SiteServer"></a> Indicazioni sulla sicurezza per il server del sito

Usare le seguenti indicazioni per proteggere il server del sito di Configuration Manager.  

### <a name="install-configuration-manager-on-a-member-server-instead-of-a-domain-controller"></a>Installare Configuration Manager in un server membro invece che in un controller di dominio

Il server e i sistemi del sito di Configuration Manager non richiedono l'installazione in un controller di dominio. I controller di dominio non hanno un database Gestione account di protezione (SAM) locale diverso da quello del dominio. Quando si installa Configuration Manager in un server membro, è possibile mantenere gli account di Configuration Manager nel database SAM locale piuttosto che nel database del dominio.  

Questa pratica riduce inoltre la superficie di attacco nei controller di dominio.  

### <a name="install-secondary-sites-without-copying-the-files-over-the-network"></a>Installare i siti secondari senza copiare i file in rete

Quando si esegue l'installazione e si crea un sito secondario, non selezionare l'opzione per copiare i file dal sito padre sul sito secondario. Non usare neanche un percorso di origine di rete. Quando si copiano dei file in rete, un utente malintenzionato esperto potrebbe assumere il controllo del pacchetto di installazione del sito secondario e manomettere i file prima che vengano installati. Far fronte a questo attacco può essere difficile. Questo attacco può essere ridotto utilizzando IPsec o SMB quando si trasferiscono i file.  

Anziché copiare i file in rete, nel server del sito secondario copiare i file di origine dalla cartella dei supporti a una cartella locale. In seguito, quando si esegue l'installazione per creare un sito secondario, nella pagina **File di origine dell'installazione** selezionare **Utilizza i file di origine nel seguente percorso del computer del sito secondario (più sicuro)** e specificare la cartella indicata.  

Per altre informazioni, vedere [Installare un sito secondario](../../servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_secondary).

### <a name="site-role-installation-inherits-permissions-from-drive-root"></a>L'installazione del ruolo del sito eredita le autorizzazioni dalla radice dell'unità

<!-- SCCMDocs#1380 -->
Assicurarsi di configurare correttamente le autorizzazioni dell'unità di sistema prima di installare il primo ruolo del sistema del sito in un server. Ad esempio, `C:\SMS_CCM` eredita le autorizzazioni da `C:\`. Se la radice dell'unità non è protetta correttamente, gli utenti con diritti limitati potrebbero essere in grado di accedere o modificare il contenuto nella cartella Configuration Manager.


## <a name="security-guidance-for-sql-server"></a><a name="BKMK_Security_SQLServer"></a> Indicazioni sulla sicurezza per SQL Server

Configuration Manager usa SQL Server come database back-end. Se il database è compromesso, gli utenti malintenzionati potrebbero bypassare Configuration Manager. Se accedono a SQL Server direttamente, possono avviare attacchi attraverso Configuration Manager. Gli attacchi contro SQL Server sono rischiosi e devono essere ridotti in modo appropriato.  

Usare le indicazioni relative alla sicurezza riportate di seguito per proteggere SQL Server per Configuration Manager.  

### <a name="dont-use-the-configuration-manager-site-database-server-to-run-other-sql-server-applications"></a>Non usare il server del database del sito di Configuration Manager per eseguire altre applicazioni di SQL Server

Se si aumenta l'accesso al server del database del sito di Configuration Manager, questa azione aumenta il rischio per i dati di Configuration Manager. Se il database del sito di Configuration Manager è compromesso, anche altre applicazioni nello stesso computer di SQL Server possono essere a rischio.  

### <a name="configure-sql-server-to-use-windows-authentication"></a>Configurare SQL Server per l'uso dell'autenticazione di Windows

Benché Configuration Manager acceda al database del sito usando un account Windows e l'autenticazione di Windows, è comunque possibile configurare SQL Server perché usi la modalità mista di SQL Server. SQL Server in modalità mista consente l'accesso al database da parte di altri accessi SQL. Questa configurazione non è obbligatoria e aumenta la superficie di attacco del computer.  

### <a name="update-sql-server-express-at-secondary-sites"></a>Aggiornare SQL Server Express nei siti secondari

Quando si installa un sito primario, Configuration Manager scarica SQL Server Express dall'Area download Microsoft e copia i file nel server del sito primario. Quando si installa un sito secondario e si seleziona l'opzione che installa SQL Server Express, Configuration Manager installa la versione precedentemente scaricata. Non verifica se sono disponibili nuove versioni. Per assicurarsi che il sito secondario includa le versioni più recenti, eseguire una delle operazioni seguenti:  

- Dopo aver installato il sito secondario, eseguire Windows Update sul server del sito secondario.  

- Prima di installare il sito secondario, installare manualmente SQL Server Express nel server del sito secondario. Assicurarsi di installare la versione più recente e gli eventuali aggiornamenti software. Quindi installare il sito secondario e selezionare l'opzione per l'uso di un'istanza di SQL Server esistente.  

Eseguire periodicamente Windows Update per tutte le versioni installate di SQL Server. Questa procedura assicura che siano disponibili gli aggiornamenti software più recenti.  

### <a name="follow-general-guidance-for-sql-server"></a>Seguire le indicazioni generali per SQL Server

Identificare e seguire le indicazioni generali per la versione di SQL Server in uso. Tuttavia, prendere in considerazione i seguenti requisiti per Configuration Manager:  

- L'account computer del server del sito deve essere membro del gruppo Administrators sul computer su cui è in esecuzione SQL Server. Se si segue il suggerimento di SQL Server di "eseguire il provisioning di tutte le entità admin esplicitamente", l'account che si usa per eseguire l'installazione nel server del sito deve essere membro del gruppo di utenti SQL.  

- Se si installa SQL Server utilizzando un account utente di dominio, verificare che l'account computer del server del sito sia configurato per un nome dell'entità di servizio (SPN) pubblicato nei Servizi di dominio Active Directory. Senza SPN, l'autenticazione Kerberos e l'installazione di Configuration Manager avranno esito negativo.  


## <a name="security-guidance-for-site-systems-that-run-iis"></a><a name="BKMK_Security_IIS"></a> Indicazioni sulla sicurezza per i sistemi del sito che eseguono IIS

Diversi ruoli del sistema del sito in Configuration Manager richiedono IIS. Il processo di protezione di IIS consente a Configuration Manager di funzionare correttamente e riduce il rischio di attacchi alla sicurezza. Quando è possibile, ridurre al minimo il numero di server che richiedono IIS. Ad esempio, eseguire solo il numero di punti di gestione richiesti per il supporto della base client, prendendo in considerazione l'alta disponibilità e l'isolamento di rete per la gestione client basata su Internet.  

Usare le indicazioni seguenti per proteggere i sistemi del sito che eseguono IIS.  

### <a name="disable-iis-functions-that-you-dont-require"></a>Disabilitare le funzioni IIS non necessarie

Installare solo le funzionalità IIS minime per il ruolo del sistema del sito che si installa. Per altre informazioni, vedere [Prerequisiti del sito e del sistema del sito](../configs/site-and-site-system-prerequisites.md).  

### <a name="configure-the-site-system-roles-to-require-https"></a>Configurare i ruoli del sistema del sito per richiedere HTTPS

Quando i client si connettono a un sistema del sito usando HTTP anziché HTTPS, usano l'autenticazione di Windows. Questo comportamento può comportare il fallback all'uso dell'autenticazione NTLM anziché dell'autenticazione Kerberos. Quando viene utilizzata l'autenticazione NTLM, i client potrebbero connettersi a un server non autorizzato.  

Un'eccezione può essere rappresentata dai punti di distribuzione. Gli account di accesso al pacchetto non funzionano quando il punto di distribuzione è configurato per HTTPS. Gli account di accesso al pacchetto forniscono l'autorizzazione al contenuto, in modo che è possibile limitare gli utenti che possono accedere al contenuto. Per altre informazioni, vedere [Procedure di sicurezza consigliate per la gestione del contenuto](security-and-privacy-for-content-management.md#BKMK_Security_ContentManagement).  

### <a name="configure-a-certificate-trust-list-ctl-in-iis-for-site-system-roles"></a>Configurare un elenco di certificati attendibili (CTL) in IIS per i ruoli del sistema del sito

Ruoli del sistema del sito:  

- Un punto di distribuzione configurato per HTTPS  

- Un punto di gestione configurato per HTTPS e abilitato per il supporto di dispositivi mobili

Un elenco CTL è un elenco definito di autorità di certificazione radice attendibile. Quando si usa un CTL con criteri di gruppo e una distribuzione di infrastruttura a chiave pubblica (PKI), un elenco CTL consente di integrare le autorità di certificazione (CA) radice attendibili esistenti configurate nella rete, ad esempio, le CA installate automaticamente con Microsoft Windows o aggiunte attraverso CA radice aziendali di Windows. Se configurato in IIS, l'elenco CTL definisce un sottoinsieme di tali CA radice attendibili.  

Questo sottoinsieme conferisce un maggiore controllo sulla sicurezza. L'elenco CTL limita i certificati client accettati solo a quelli emessi dalle autorità di certificazione indicate nell'elenco CTL. Ad esempio, Windows include diversi certificati di CA di terze parti come VeriSign e Thawte.

Per impostazione predefinita, il computer che esegue IIS ritiene attendibili i certificati concatenati a queste CA note. Quando IIS non viene configurato con un elenco CTL per i ruoli del sistema del sito in elenco, il sito accetta come client valido qualsiasi dispositivo con un certificato emesso da tali CA. Se IIS viene configurato con un elenco CTL che non comprendeva queste CA, il sito rifiuta le connessioni client se il certificato è concatenato a tali CA. Affinché i client di Configuration Manager vengano accettati per i ruoli del sistema del sito in elenco, occorre configurare IIS con un elenco CTL che specifichi le CA usate dai client di Configuration Manager.  

> [!NOTE]  
> Solo i ruoli del sistema del sito in elenco richiedono la configurazione di un elenco scopi consentiti ai certificati in IIS. L'elenco delle autorità che emettono certificati usato da Configuration Manager per i punti di gestione offre la stessa funzionalità per i computer client quando si collegano ai punti di gestione HTTPS.  

Per altre informazioni su come configurare un elenco di autorità di certificazione attendibili in IIS, consultare la documentazione di IIS.  

### <a name="dont-put-the-site-server-on-a-computer-with-iis"></a>Non usare il server del sito in un computer con IIS

La separazione dei ruoli consente di ridurre il profilo di attacco e di migliorare la capacità di ripristino. L'account computer del server del sito in genere ha privilegi amministrativi per tutti i ruoli del sistema del sito. Può anche avere questi privilegi per i client di Configuration Manager, se si usa l'installazione push client.  

### <a name="use-dedicated-iis-servers-for-configuration-manager"></a>Usare server IIS dedicati per Configuration Manager

Sebbene sia possibile ospitare più applicazioni basate su Web sui server IIS che sono usati anche da Configuration Manager, tale pratica può significativamente aumentare la superficie di attacco. Un'applicazione configurata male potrebbe consentire a un utente malintenzionato di prendere il controllo di un sistema del sito di Configuration Manager. Questa violazione potrebbe consentire a un utente malintenzionato di ottenere il controllo della gerarchia.  

Se è necessario eseguire altre applicazioni basate su Web nei sistemi del sito di Configuration Manager, creare un sito Web personalizzato per i sistemi del sito di Configuration Manager.  

### <a name="use-a-custom-website"></a>Usare un sito Web personalizzato

Per i sistemi del sito su cui è in esecuzione IIS, configurare Configuration Manager in modo da usare un sito Web personalizzato anziché il sito Web predefinito. Per poter eseguire altre applicazioni Web sul sistema del sito, è necessario usare un sito Web personalizzato. Questa impostazione si applica all'intero sito anziché al sistema del sito specifico.  

### <a name="when-you-use-custom-websites-remove-the-default-virtual-directories"></a>Quando si usano i siti Web personalizzati, rimuovere le directory virtuali predefinite

Se si passa dall'uso del sito Web predefinito all'uso di un sito Web personalizzato, Configuration Manager non rimuove le vecchie directory virtuali. Rimuovere le directory virtuali create in origine da Configuration Manager nel sito Web predefinito.  

Ad esempio, rimuovere le directory virtuali seguenti per un punto di distribuzione:  

- SMS_DP_SMSPKG$  

- SMS_DP_SMSSIG$  

- NOCERT_SMS_DP_SMSPKG$  

- NOCERT_SMS_DP_SMSSIG$  

### <a name="follow-iis-server-security-guidance"></a>Seguire le indicazioni sulla sicurezza per il server IIS

Identificare e seguire le indicazioni generali per la versione di IIS Server in uso. Prendere in considerazione tutti i requisiti di Configuration Manager riguardo ai ruoli del sistema del sito specifico. Per altre informazioni, vedere [Prerequisiti del sito e del sistema del sito](../configs/site-and-site-system-prerequisites.md).  


## <a name="security-guidance-for-the-management-point"></a><a name="BKMK_Security_ManagementPoint"></a> Indicazioni sulla sicurezza per il punto di gestione

I punti di gestione sono l'interfaccia primaria tra i dispositivi e Configuration Manager. Gli attacchi contro il punto di gestione e il server su cui è in esecuzione sono rischiosi e devono essere ridotti in modo appropriato. Applicare tutte le indicazioni sulla sicurezza appropriate e monitorare eventuali attività inconsuete.  

Usare le indicazioni seguenti per proteggere un punto di gestione in Configuration Manager.  

### <a name="assign-the-client-on-a-management-point-to-the-same-site"></a>Assegnare il client per un punto di gestione allo stesso sito

Evitare la situazione in cui il client di Configuration Manager che si trova in un punto di gestione viene assegnato a un sito diverso da quello del punto di gestione.  

Se si esegue la migrazione da una versione precedente a Configuration Manager Current Branch, eseguire la migrazione del client per il punto di gestione al nuovo sito appena possibile.  


## <a name="security-guidance-for-the-fallback-status-point"></a><a name="BKMK_Security_FSP"></a> Indicazioni sulla sicurezza per il punto di stato di fallback

Se si installa un punto di stato di fallback in Configuration Manager, usare le seguenti indicazioni sulla sicurezza:

Per altre informazioni sulla sicurezza quando si installa un punto di stato di fallback, vedere [Stabilire se è necessario un punto di stato di fallback](../../clients/deploy/plan/determine-the-site-system-roles-for-clients.md#fallback-status-point).  

### <a name="dont-run-any-other-roles-on-the-same-site-system"></a>Non eseguire altri ruoli per lo stesso sistema del sito

Il punto di stato di fallback è progettato per accettare comunicazioni non autenticate da qualsiasi computer. Se si esegue questo ruolo del sistema del sito con altri ruoli o un controller di dominio, il rischio per tale server aumenta significativamente.  

### <a name="install-the-fallback-status-point-before-you-install-clients-with-pki-certificates"></a>Installare il punto di stato di fallback prima di installare i client con i certificati PKI

Se i sistemi del sito di Configuration Manager non accettano la comunicazione client HTTP, è possibile che non si sappia che i client non sono gestiti a causa di problemi di certificato relativi alla PKI. Se i client sono assegnati a un punto di stato di fallback, segnalano questi problemi di certificato attraverso il punto di stato di fallback.  

Per ragioni di sicurezza, non è possibile assegnare un punto di stato di fallback ai client dopo l'installazione. Questo ruolo può invece essere assegnato durante l'installazione del client.  

### <a name="avoid-using-the-fallback-status-point-in-the-perimeter-network"></a>Evitare l'uso del punto di stato di fallback nella rete perimetrale

Per impostazione predefinita, il punto di stato di fallback accetta dati da qualsiasi client. Anche se un punto di stato di fallback nella rete perimetrale può agevolare la risoluzione dei problemi di client basati su Internet, bilanciare i vantaggi offerti dalla risoluzione dei problemi e il rischio di un sistema del sito che accetta dati non autenticati in una rete accessibile pubblicamente.  

Se si installa il punto di stato di fallback nella rete perimetrale o in una rete non attendibile, configurare il server del sito per avviare i trasferimenti di dati. Non usare l'impostazione predefinita che consente al punto di stato di fallback di avviare una connessione al server del sito.  


## <a name="security-issues-for-site-administration"></a><a name="BKMK_SecurityIssues_Clients"></a> Problemi di sicurezza per l'amministrazione del sito

Esaminare i problemi di sicurezza seguenti per Configuration Manager:  

- Configuration Manager non dispone di difese contro un utente amministratore autorizzato che usa Configuration Manager per attaccare la rete. Gli utenti amministrativi non autorizzati costituiscono un rischio elevato per la sicurezza. Potrebbero avviare molti attacchi, che includono le strategie seguenti:  

    - Usare la distribuzione di software per installare automaticamente ed eseguire malware in ogni computer client di Configuration Manager dell'organizzazione.  

    - Usare il controllo remoto per assumere il controllo di un client di Configuration Manager senza autorizzazioni.  

    - Configurare intervalli di polling rapidi e notevoli quantità di inventario. Questa azione crea attacchi Denial of Service contro i client e i server.  

    - Utilizzare un sito nella gerarchia per scrivere dati nei dati di Active Directory di un altro sito.  

    La gerarchia del sito è il limite di sicurezza. Considerare i siti solo come limiti di gestione.  

    Controllare tutte le attività degli utenti amministrativi ed esaminare periodicamente i registri di controllo. Eseguire un'indagine obbligatoria della storia personale di ogni utente amministratore di Configuration Manager prima dell'assunzione. Richiedere nuovi controlli periodici come condizione per l'impiego.  

- Se il punto di registrazione viene compromesso, un utente malintenzionato potrebbe ottenere i certificati per l'autenticazione e impadronirsi delle credenziali degli utenti che registrano il proprio dispositivo mobile.  

    Il punto di registrazione comunica con un'autorità di certificazione. Può creare, modificare ed eliminare oggetti Active Directory. Non installare mai il punto di registrazione nella rete perimetrale. Monitorare sempre le attività insolite.  

- Se si consentono i criteri utente per la gestione client basata su Internet, si aumenta il profilo di attacco.  

    Oltre a usare i certificati PKI per le connessioni tra client e server, queste configurazioni richiedono l'autenticazione di Windows e potrebbero eseguire il fallback all'uso dell'autenticazione NTLM anziché dell'autenticazione Kerberos. L'autenticazione NTLM è vulnerabile agli attacchi di riproduzione e di rappresentazione. Per autenticare correttamente un utente su Internet, è necessario consentire una connessione dal server di sistema del sito basato su Internet a un controller di dominio.  

- La condivisione **Admin$** è necessaria per i server di sistema del sito.  

    Il server del sito di Configuration Manager usa la condivisione Admin$ per la connessione e l'esecuzione di operazioni di servizio nei sistemi del sito. Non disabilitare o rimuovere questa condivisione.  

- Configuration Manager usa servizi di risoluzione dei nomi per connettersi ad altri computer. Questi servizi sono difficili da proteggere dagli attacchi di sicurezza seguenti:
    - Spoofing
    - Manomissione
    - Ripudio
    - Divulgazione di informazioni
    - Denial of Service
    - Elevazione dei privilegi

    Identificare e seguire le indicazioni sulla sicurezza per la versione di DNS usata per la risoluzione dei nomi.  

## <a name="privacy-information-for-discovery"></a><a name="BKMK_Privacy_Cliients"></a> Informazioni sulla privacy per l'individuazione

L'individuazione crea i record delle risorse di rete e li archivia nel database di Configuration Manager. I record di dati di individuazione contengono informazioni sui computer, ad esempio gli indirizzi IP, le versioni dei sistemi operativi e i nomi dei computer. I metodi di individuazione di Active Directory possono essere configurati anche per restituire eventuali informazioni memorizzate in Active Directory Domain Services.  

L'unico metodo di individuazione abilitato da Configuration Manager per impostazione predefinita è l'individuazione heartbeat. Questo metodo individua solo i computer in cui è già installato il software client di Configuration Manager.  

Le informazioni di individuazione non vengono inviate direttamente a Microsoft. Vengono archiviate nel database di Configuration Manager. Configuration Manager mantiene le informazioni nel database fino a quando non vengono eliminati i dati. Questo processo si verifica ogni 90 giorni con l'attività di manutenzione del sito **Elimina dati di individuazione obsoleti**.  
